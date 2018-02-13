---
title: "Modèles d’événement .NET standard"
description: "En savoir plus sur les modèles d’événement .NET et comment créer des sources d’événements standard, vous abonner à des événements standard dans votre code et traiter ces événements."
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 8a3133d6-4ef2-46f9-9c8d-a8ea8898e4c9
ms.openlocfilehash: ff36438ab02ae6822d7df8425a615aef2ddbf2f2
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/17/2018
---
# <a name="standard-net-event-patterns"></a>Modèles d’événement .NET standard

[Précédent](events-overview.md)

Les événements .NET respectent en général quelques modèles connus. La normalisation d’après ces modèles signifie que les développeurs peuvent exploiter les connaissances de ces modèles standard, qui peuvent être appliqués à n’importe quel programme d’événement .NET.

Un examen de ces modèles standard vous permettra d’acquérir toutes les connaissances nécessaires pour créer des sources d’événements standard, et pour traiter et vous abonner à des événements standard dans votre code.

## <a name="event-delegate-signatures"></a>Signatures de délégués d’événements

La signature standard d’un délégué d’événement .NET est la suivante :

```csharp
void OnEventRaised(object sender, EventArgs args);
```

Le type de retour est void. Les événements sont basés sur des délégués et il s’agit de délégués multicast. Cela permet de prendre en charge plusieurs abonnés pour toute source d’événement. La valeur de retour unique d’une méthode ne s’étend pas à plusieurs abonnés aux événements. Quelle valeur de retour la source de l’événement voit-elle après le déclenchement d’un événement ? Plus loin dans cet article, vous verrez comment créer des protocoles d’événements qui prennent en charge les abonnés aux événements qui signalent des informations à la source de l’événement.

La liste d’arguments contient deux arguments : l’expéditeur et les arguments de l’événement. Le type au moment de compilation de `sender` est `System.Object`, même si vous connaissez probablement un type plus dérivé qui serait toujours correct. Par convention, utilisez `object`.

Le deuxième argument était traditionnellement un type dérivé de `System.EventArgs`. (Vous verrez dans la [section suivante](modern-events.md) que cette convention n’est plus appliquée.) Si votre type d’événement n’a pas besoin d’autres arguments, vous fournirez quand même ces deux arguments.
Il existe une valeur spéciale, `EventArgs.Empty`, que vous devez utiliser pour indiquer que votre événement ne contient pas d’informations supplémentaires.

Commençons par créer une classe qui répertorie les fichiers contenus dans un répertoire ou dans l’un de ses sous-répertoires qui suivent un modèle. Ce composant déclenche un événement pour chaque fichier détecté qui correspond au modèle.

L’utilisation d’un modèle d’événement offre certains avantages en matière de conception. Vous pouvez créer plusieurs détecteurs d’événements qui effectuent des actions différentes quand un fichier recherché est trouvé. La combinaison des différents détecteurs permet de créer des algorithmes plus robustes.

Voici la déclaration d’argument d’événement initiale pour trouver un fichier recherché : 

```csharp
public class FileFoundArgs : EventArgs
{
    public string FoundFile { get; }

    public FileFoundArgs(string fileName)
    {
        FoundFile = fileName;
    }
}
```

Bien que ce type ressemble à un petit type « données uniquement », vous devez suivre la convention et faire de lui un type référence (`class`). Cela signifie que l’objet d’argument sera passé par référence, et que les mises à jour des données seront visibles par tous les abonnés. La première version est un objet immuable. Il vaut mieux rendre immuables les propriétés dans votre argument d’événement. Ainsi, un abonné ne peut pas changer les valeurs avant qu’un autre abonné ne les voit. (Il existe des exceptions, comme vous le verrez ci-dessous.)  

Ensuite, nous devons créer la déclaration d’événement dans la classe FileSearcher. L’utilisation du type `EventHandler<T>` nous évite de devoir créer une autre définition de type. Il suffit d’utiliser une spécialisation générique.

Nous allons remplir la classe FileSearcher pour rechercher les fichiers qui correspondent à un modèle et déclencher l’événement approprié quand une correspondance est détectée.

```csharp
public class FileSearcher
{
    public event EventHandler<FileFoundArgs> FileFound;

    public void Search(string directory, string searchPattern)
    {
        foreach (var file in Directory.EnumerateFiles(directory, searchPattern))
        {
            FileFound?.Invoke(this, new FileFoundArgs(file));
        }
    }
}
```

## <a name="definining-and-raising-field-like-events"></a>Définition et déclenchement d’événements de type champ

Pour ajouter un événement à votre classe, le plus simple consiste à déclarer cet événement en tant que champ public, comme dans l’exemple ci-dessous :

```csharp
public event EventHandler<FileFoundArgs> FileFound;
```

Ce code semble déclarer un champ public, ce qui semble être une mauvaise pratique orientée objet. Vous devez protéger l’accès aux données par l’intermédiaire des propriétés ou méthodes. Bien que cela semble être une mauvaise pratique, le code généré par le compilateur crée en fait des wrappers pour que les objets d’événements soient accessibles uniquement de manière sécurisée. Les seules opérations disponibles sur un événement de type champ sont l’ajout de gestionnaire :

```csharp
EventHandler<FileFoundArgs> onFileFound = (sender, eventArgs) =>
    Console.WriteLine(eventArgs.FoundFile);
lister.FileFound += onFileFound;
```

et la suppression de gestionnaire :

```csharp
lister.FileFound -= onFileFound;
```

Notez qu’il existe une variable locale pour le gestionnaire. Si vous utilisiez le corps de l’expression lambda, la suppression ne fonctionnerait pas correctement. Il s’agirait d’une autre instance du délégué, et l’opération ne ferait rien en mode silencieux.

Le code en dehors de la classe ne peut pas déclencher l’événement et ne peut pas non plus effectuer d’autres opérations.

## <a name="returning-values-from-event-subscribers"></a>Retour de valeurs à partir des abonnés aux événements

Notre version simple fonctionne correctement. Ajoutons maintenant une autre fonctionnalité : l’annulation.

Quand vous déclenchez l’événement détecté, les détecteurs doivent pouvoir arrêter le traitement si ce fichier est le dernier recherché.

Les gestionnaires d’événements ne retournant pas de valeur, vous devez communiquer cela par un autre moyen. Le modèle d’événement standard utilise l’objet EventArgs pour inclure des champs que les abonnés aux événements peuvent utiliser pour signaler une annulation.

Deux modèles différents peuvent être utilisés, en fonction de la sémantique du contrat d’annulation. Dans les deux cas, vous ajouterez un champ booléen aux arguments d’événements pour l’événement de fichier trouvé. 

L’un des modèles autorise n’importe quel abonné à annuler l’opération.
Pour ce modèle, le nouveau champ est initialisé avec la valeur `false`. Tout abonné peut le changer et lui affecter la valeur `true`. Une fois que tous les abonnés ont vu l’événement déclenché, le composant FileSearcher examine la valeur booléenne et effectue une action.

Le deuxième modèle annule l’opération uniquement si tous les abonnés souhaitent l’annuler. Dans ce modèle, le nouveau champ est initialisé pour indiquer que l’opération doit être annulée, et n’importe quel abonné peut le changer pour indiquer que l’opération doit continuer.
Une fois que tous les abonnés ont vu l’événement déclenché, le composant FileSearcher examine la valeur booléenne et effectue une action. Il existe une étape supplémentaire dans ce modèle : le composant doit savoir si des abonnés ont vu l’événement. S’il n’y a pas d’abonnés, le champ indique incorrectement une annulation.

Implémentons la première version pour cet exemple. Nous devons ajouter un champ booléen au type FileFoundEventArgs :

```csharp
public class FileFoundArgs : EventArgs
{
    public string FoundFile { get; }
    public bool CancelRequested { get; set; }

    public FileFoundArgs(string fileName)
    {
        FoundFile = fileName;
    }
}
```

Ce nouveau champ doit être initialisé avec la valeur false, afin de ne pas être annulé sans raison. Comme il s’agit de la valeur par défaut pour un champ booléen, cela se produit automatiquement. Le seul autre changement à apporter au composant consiste à vérifier l’indicateur après le déclenchement de l’événement, pour voir si l’un des abonnés a demandé une annulation :

```csharp
public void List(string directory, string searchPattern)
{
    foreach (var file in Directory.EnumerateFiles(directory, searchPattern))
    {
        var args = new FileFoundArgs(file);
        FileFound?.Invoke(this, args);
        if (args.CancelRequested)
            break;
    }
}
```

L’un des avantages de ce modèle est qu’il ne s’agit pas d’une modification avec rupture.
Aucun des abonnés n’a demandé d’annulation auparavant, et ils n’en demandent toujours pas. Aucun code d’abonné ne nécessite de mise à jour, sauf s’il souhaite prendre en charge le nouveau protocole d’annulation. Le couplage est très faible.

Nous allons maintenant mettre à jour l’abonné pour qu’il demande une annulation dès qu’il trouve le premier exécutable :

```csharp
EventHandler<FileFoundArgs> onFileFound = (sender, eventArgs) =>
{
    Console.WriteLine(eventArgs.FoundFile);
    eventArgs.CancelRequested = true;
};
```

## <a name="adding-another-event-declaration"></a>Ajout d’une autre déclaration d’événement

Nous allons ajouter une autre fonctionnalité et illustrer d’autres idiomes de langage pour les événements. Ajoutons une surcharge de la méthode `Search()` qui parcourt tous les sous-répertoires à la recherche de fichiers.

Cette opération pourrait prendre beaucoup de temps dans un répertoire contenant de nombreux sous-répertoires. Ajoutons un événement déclenché au début de chaque nouvelle recherche dans un répertoire. Cela permet aux abonnés de suivre la progression et de tenir l’utilisateur à jour. Tous les exemples que nous avons créés jusqu’à présent sont publics. Faisons de celui-ci un événement interne. Cela signifie que nous pouvons aussi rendre internes les types utilisés pour les arguments.

Nous allons commencer par créer la nouvelle classe dérivée EventArgs pour signaler le nouveau répertoire et la progression. 

```csharp
internal class SearchDirectoryArgs : EventArgs
{
    internal string CurrentSearchDirectory { get; }
    internal int TotalDirs { get; }
    internal int CompletedDirs { get; }

    internal SearchDirectoryArgs(string dir, int totalDirs, int completedDirs)
    {
        CurrentSearchDirectory = dir;
        TotalDirs = totalDirs;
        CompletedDirs = completedDirs;
    }
}
``` 

Là encore, nous pouvons suivre les recommandations pour créer un type référence immuable pour les arguments d’événements.

Maintenant, définissons l’événement. Cette fois-ci, nous utiliserons une syntaxe différente. En plus d’utiliser la syntaxe du champ, nous pouvons créer explicitement la propriété, avec des gestionnaires d’ajout et de suppression. Dans cet exemple, nous n’aurons pas besoin de code supplémentaire dans ces gestionnaires dans ce projet, mais cet exemple montre comment les créer.

```csharp
internal event EventHandler<SearchDirectoryArgs> DirectoryChanged
{
    add { directoryChanged += value; }
    remove { directoryChanged -= value; }
}
private EventHandler<SearchDirectoryArgs> directoryChanged;
```

Le code que nous écrivons ici reflète en grande partie le code généré par le compilateur pour les définitions d’événements de champs que nous avons vu précédemment. Nous créons l’événement à l’aide d’une syntaxe très similaire à celle utilisée pour les [propriétés](properties.md). Notez que les gestionnaires ont des noms différents : `add` et `remove`. Il sont appelés pour s’abonner à l’événement ou pour annuler un abonnement. Notez que vous devez également déclarer un champ de stockage privé pour stocker la variable d’événement. Il est initialisé avec la valeur null.

Ensuite, nous allons ajouter la surcharge de la méthode Search() qui parcourt les sous-répertoires et déclenche les deux événements. Le moyen le plus simple consiste à utiliser un argument par défaut pour indiquer que nous souhaitons rechercher dans tous les répertoires :

```csharp
public void Search(string directory, string searchPattern, bool searchSubDirs = false)
{
    if (searchSubDirs)
    {
        var allDirectories = Directory.GetDirectories(directory, "*.*", SearchOption.AllDirectories);
        var completedDirs = 0;
        var totalDirs = allDirectories.Length + 1;
        foreach (var dir in allDirectories)
        {
            directoryChanged?.Invoke(this,
                new SearchDirectoryArgs(dir, totalDirs, completedDirs++));
            // Recursively search this child directory:
            SearchDirectory(dir, searchPattern);
        }
        // Include the Current Directory:
        directoryChanged?.Invoke(this,
            new SearchDirectoryArgs(directory, totalDirs, completedDirs++));
        SearchDirectory(directory, searchPattern);
    }
    else
    {
        SearchDirectory(directory, searchPattern);
    }
}

private void SearchDirectory(string directory, string searchPattern)
{
    foreach (var file in Directory.EnumerateFiles(directory, searchPattern))
    {
        var args = new FileFoundArgs(file);
        FileFound?.Invoke(this, args);
        if (args.CancelRequested)
            break;
    }
}
```

À ce stade, nous pouvons exécuter l’application qui appelle la surcharge pour rechercher dans tous les sous-répertoires. Il n’existe aucun abonné sur le nouvel événement `ChangeDirectory`, mais l’utilisation de l’idiome `?.Invoke()` garantit que cela fonctionne correctement.

 Ajoutons un gestionnaire pour écrire une ligne qui affiche la progression dans la fenêtre de la console. 

```csharp
lister.DirectoryChanged += (sender, eventArgs) =>
{
    Console.Write($"Entering '{eventArgs.CurrentSearchDirectory}'.");
    Console.WriteLine($" {eventArgs.CompletedDirs} of {eventArgs.TotalDirs} completed...");
};
```

Nous avons vu des modèles qui sont suivis dans tout l’écosystème .NET.
En apprenant ces modèles et ces conventions, vous écrirez rapidement du code C# et .NET idiomatique.

Dans le prochain article, nous allons voir quelques changements apportés à ces modèles dans la version la plus récente de .NET.

[Next](modern-events.md)
