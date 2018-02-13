---
title: "Crée un client REST à l’aide de .NET Core"
description: "Ce didacticiel vous présente un certain nombre de fonctionnalités de .NET Core et du langage C#."
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 51033ce2-7a53-4cdd-966d-9da15c8204d2
ms.openlocfilehash: 6b0f3acc3a6dbed4f44497d92d3c518ee5a5d2a7
ms.sourcegitcommit: dd6ea7f0e581ac84e0a90d9b23c463fcf1ec3ce7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2018
---
# <a name="rest-client"></a>Client REST

## <a name="introduction"></a>Introduction
Ce didacticiel vous présente un certain nombre de fonctionnalités de .NET Core et du langage C#. Vous apprendrez à :
*   Principes de base de l’interface de ligne de commande (CLI) de .NET Core.
*   Une présentation des fonctionnalités du langage C#.
*   Gestion des dépendances avec NuGet
*   Communications HTTP
*   Traitement des informations JSON
*   Gestion de la configuration avec les attributs. 

Vous allez générer une application qui émet des requêtes HTTP vers un service REST sur GitHub. Vous lirez des informations au format JSON et convertirez ce paquet JSON en objets C#. Enfin, vous verrez comment travailler avec les objets C#.

Il existe un grand nombre de fonctionnalités dans ce didacticiel. Nous allons les construire une par une.

Si vous préférez utiliser l’[exemple final](https://github.com/dotnet/docs/tree/master/samples/csharp/getting-started/console-webapiclient) pour cette rubrique, vous pouvez le télécharger. Pour obtenir des instructions de téléchargement, consultez [Exemples et didacticiels](../../samples-and-tutorials/index.md#viewing-and-downloading-samples).

## <a name="prerequisites"></a>Prérequis
Vous devez configurer votre ordinateur pour exécuter .NET core. Vous trouverez les instructions d’installation sur la page de [.NET Core](https://www.microsoft.com/net/core). Vous pouvez exécuter cette application sur Windows, Linux, Mac OS ou dans un conteneur Docker. Vous devez installer l’éditeur de code de votre choix. Les descriptions ci-dessous utilisent [Visual Studio Code](https://code.visualstudio.com/), qui est un éditeur de plateforme open source, multiplateforme. Cependant, vous pouvez utiliser les outils avec lesquels vous êtes le plus à l’aise.
## <a name="create-the-application"></a>Création de l’application
La première étape consiste à créer une nouvelle application. Ouvrez une invite de commandes et créez un nouveau répertoire pour votre application. Réglez-le comme répertoire actuel. Saisissez la commande `dotnet new console` à l’invite. Elle crée les fichiers de démarrage d’une application « Hello World » de base.

Avant d’apporter des modifications, examinons les étapes nécessaires pour exécuter l’application simple Hello World. Après avoir créé l’application, tapez `dotnet restore` ([voir note](#dotnet-restore-note)) à l’invite de commandes. Cette commande exécute le processus de restauration de package NuGet. NuGet est un gestionnaire de packages .NET. Cette commande télécharge les dépendances manquantes pour votre projet. Comme il s’agit d’un nouveau projet, aucune des dépendances n’est en place, donc la première exécution téléchargera le framework .NET Core. Après cette étape initiale, vous devez exécuter `dotnet restore` ([voir note](#dotnet-restore-note)) lorsque vous ajoutez de nouveaux packages dépendants ou mettez à jour les versions de vos dépendances.  

Après la restauration des packages, vous exécutez `dotnet build`. Cela exécute le moteur de génération et crée votre application. Enfin, vous exécutez `dotnet run` pour lancer votre application.

## <a name="adding-new-dependencies"></a>Ajout de nouvelles dépendances
Un des objectifs de conception clés de .NET Core est de réduire la taille de l’installation du framework .NET. Le framework d’application .NET Core contient uniquement les éléments les plus courants du framework .NET complet. Si une application a besoin de bibliothèques supplémentaires pour certaines de ses fonctionnalités, vous ajoutez ces dépendances dans votre fichier projet (\*.csproj) en C#. Dans notre exemple, vous devez ajouter le package `System.Runtime.Serialization.Json` pour que votre application puisse traiter les réponses JSON.

Ouvrez votre fichier projet `csproj`. La première ligne du fichier devrait s’afficher comme :

```xml
<Project Sdk="Microsoft.NET.Sdk">
```

Ajoutez ce qui suit immédiatement après cette ligne : 

```xml
   <ItemGroup>
      <PackageReference Include="System.Runtime.Serialization.Json" Version="4.3.0" />
   </ItemGroup> 
```
La plupart des éditeurs de code fournissent la saisie semi-automatique pour différentes versions de ces bibliothèques. Vous souhaiterez généralement utiliser la dernière version d’un package que vous ajoutez. Toutefois, il est important de vous assurer que les versions de tous les packages correspondent et qu’ils correspondent également la version du framework d’application .NET Core.

Une fois que vous avez apporté ces modifications, vous devez réexécuter `dotnet restore` ([voir note](#dotnet-restore-note))afin que le package soit installé sur votre système.

## <a name="making-web-requests"></a>Effectuer des requêtes web
Vous êtes maintenant prêt à commencer la récupération des données à partir du web. Dans cette application, vous obtiendrez des informations à partir de [l’API GitHub](https://developer.github.com/v3/). Nous allons lire des informations sur les projets couverts par la [.NET Foundation](http://www.dotnetfoundation.org/). Vous allez commencer par créer la demande à l’API GitHub pour récupérer des informations sur les projets. Le point de terminaison que vous utiliserez : [https://api.github.com/orgs/dotnet/repos](https://api.github.com/orgs/dotnet/repos). Vous souhaitez récupérer toutes les informations sur ces projets, vous allez donc utiliser une requête HTTP GET.
Votre navigateur utilise également les requêtes HTTP GET, vous pouvez donc coller cette URL dans votre navigateur pour voir les informations que vous recevez et traitez.

Vous utilisez la classe <xref:System.Net.Http.HttpClient> pour effectuer des requêtes web. Comme toutes les API .NET modernes, <xref:System.Net.Http.HttpClient> prend en charge uniquement les méthodes async pour ses API les plus anciennes.
Commencez par créer une méthode async. Vous allez effectuer l’implémentation lors de la création des fonctionnalités de l’application. Commencez en ouvrant le fichier `program.cs` dans votre répertoire de projet et l’ajout de la méthode suivante à la classe `Program` :

```csharp
private static async Task ProcessRepositories()
{
    
}
```

Vous devrez ajouter une instruction `using` en haut de votre méthode `Main` afin que le compilateur C# reconnaisse le type <xref:System.Threading.Tasks.Task> :

```csharp
using System.Threading.Tasks;
```

Si vous générez votre projet à ce stade, vous obtiendrez un avertissement généré pour cette méthode, car elle ne contient aucun opérateur `await` et s’exécute de façon synchrone. Ignorez-le pour le moment. vous ajouterez des opérateurs `await` lorsque vous remplirez la méthode.

Ensuite, renommez l’espace de noms défini dans l’instruction `namespace` de sa valeur par défaut de `ConsoleApp` en `WebAPIClient`. Plus tard, nous allons définir une classe `repo` dans cet espace de noms.

Ensuite, mettez à jour la méthode `Main` pour appeler cette méthode. La méthode `ProcessRepositories` retourne une tâche, et vous ne devez pas quitter le programme avant la fin de cette tâche. Par conséquent, vous devez utiliser la méthode `Wait` pour bloquer et attendre la fin de la tâche :

```csharp
public static void Main(string[] args)
{
    ProcessRepositories().Wait();
}
```

À présent, vous disposez d’un programme qui ne fait rien, mais le fait de façon asynchrone. Nous allons l’améliorer.

Tout d’abord, vous avez besoin d’un objet pouvant récupérer des données à partir du web ; pour ce faire, vous pouvez utiliser <xref:System.Net.Http.HttpClient>. Cet objet gère la demande et les réponses. Instanciez une seule instance de ce type dans la classe `Program` dans le fichier Program.cs.

```csharp
namespace WebAPIClient
{
    class Program
    {
        private static readonly HttpClient client = new HttpClient();

        static void Main(string[] args)
        {
            //...
        }
    }
}
```

 Revenons à la méthode `ProcessRepositories` et créons sa première version :

```csharp
private static async Task ProcessRepositories()
{
    client.DefaultRequestHeaders.Accept.Clear();
    client.DefaultRequestHeaders.Accept.Add(
        new MediaTypeWithQualityHeaderValue("application/vnd.github.v3+json"));
    client.DefaultRequestHeaders.Add("User-Agent", ".NET Foundation Repository Reporter");

    var stringTask = client.GetStringAsync("https://api.github.com/orgs/dotnet/repos");

    var msg = await stringTask;
    Console.Write(msg);
}
```

Vous devrez également ajouter deux nouvelles instructions using en haut du fichier pour que cela compile :

```csharp
using System.Net.Http;
using System.Net.Http.Headers;
```

Cette première version effectue une requête web pour lire la liste de tous les dépôts de l’organisation dotnet foundation. (L’ID GitHub de la .NET Foundation est 'dotnet'). Les premières lignes configurent <xref:System.Net.Http.HttpClient> pour cette requête. Tout d’abord, il est configuré pour accepter les réponses JSON de GitHub.
Ce format est simplement du JSON. La ligne suivante ajoute un en-tête d’agent utilisateur à toutes les requêtes à partir de cet objet. Ces deux en-têtes sont vérifiés par le code du serveur GitHub et sont nécessaires pour récupérer des informations à partir de GitHub.

Une fois que vous avez configuré le <xref:System.Net.Http.HttpClient>, effectuez une requête web et récupérez la réponse. Dans cette première version, vous utilisez la méthode pratique <xref:System.Net.Http.HttpClient.GetStringAsync(System.String)?displayProperty=nameWithType>. Cette méthode démarre une tâche qui effectue la requête web, et, lorsque la demande est renvoyée, lit le flux de réponse puis extrait le contenu à partir du flux. Le corps de la réponse est renvoyé en tant que <xref:System.String>. La chaîne est disponible lorsque la tâche est terminée. 

Les deux dernières lignes de cette méthode attendent cette tâche et impriment la réponse dans la console.
Générez l'application et exécutez-la. L’avertissement de génération a disparu maintenant, car `ProcessRepositories` contient maintenant un opérateur `await`. Vous verrez long affichage de texte au format JSON.   

## <a name="processing-the-json-result"></a>Traitement du résultat JSON

À ce stade, vous avez écrit le code pour récupérer une réponse à partir d’un serveur web et afficher le texte contenu dans cette réponse. Ensuite, nous allons convertir cette réponse JSON en objets C#.

Le sérialiseur JSON convertit des données JSON en objets C#. Votre première tâche consiste à définir un type de classe C# pour contenir les informations à utiliser à partir de cette réponse. Nous allons prendre notre temps pour étudier cela, commençons donc par un type C# simple qui contient le nom du dépôt :

```csharp
using System;

namespace WebAPIClient
{
    public class repo
    {
        public string name;
    }
}
``` 

Placez le code ci-dessus dans un fichier nommé « repo.cs ». Cette version de la classe représente le chemin d’accès le plus simple pour traiter les données JSON. Le nom de classe et le nom du membre correspondent aux noms utilisés dans le paquet JSON, au lieu des conventions C# suivantes. Vous allez corriger cela en fournissant des attributs de configuration ultérieurement. Cette classe décrit une autre fonctionnalité importante de la sérialisation et de désérialisation JSON : tous les champs dans le paquet JSON font partie de cette classe.
Le sérialiseur JSON ignore les informations qui ne sont pas incluses dans le type de classe utilisé.
Cette fonctionnalité facilite la création de types qui fonctionnent avec uniquement un sous-ensemble des champs dans le paquet JSON.

Maintenant que vous avez créé le type, nous allons le désérialiser. Vous devez créer un objet <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>. Cet objet doit connaître le type CLR attendu pour le paquet JSON qu’il récupère. Le paquet de GitHub contient une séquence de dépôts, c’est pourquoi `List<repo>` est du bon type. Ajoutez la ligne suivante à votre méthode `ProcessRepositories` :

```csharp
var serializer = new DataContractJsonSerializer(typeof(List<repo>));
```

Vous utilisez deux nouveaux espaces de noms, vous devez donc les ajouter aussi :

```csharp
using System.Collections.Generic;
using System.Runtime.Serialization.Json;
```

Ensuite, vous utiliserez le sérialiseur pour convertir le JSON en objets C#. Remplacez l’appel à <xref:System.Net.Http.HttpClient.GetStringAsync(System.String)> dans votre méthode `ProcessRepositories` avec les deux lignes suivantes :

```csharp
var streamTask = client.GetStreamAsync("https://api.github.com/orgs/dotnet/repos");
var repositories = serializer.ReadObject(await streamTask) as List<repo>;
```

Notez que vous utilisez maintenant <xref:System.Net.Http.HttpClient.GetStreamAsync(System.String)> au lieu de <xref:System.Net.Http.HttpClient.GetStringAsync(System.String)>. Le sérialiseur utilise un flux plutôt qu’une chaîne comme source. Nous allons expliquer quelques fonctionnalités du langage C# qui sont utilisées dans la deuxième ligne ci-dessus. L’argument <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.ReadObject(System.IO.Stream)> est une expression `await`. Les expressions await peuvent apparaître quasiment n’importe où dans votre code, bien que jusqu'à présent, vous les avez uniquement vues dans le cadre d’une instruction d’assignation.

Deuxièmement, l’opérateur `as` convertit le type au moment de la compilation `object` en `List<repo>`. La déclaration de <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.ReadObject(System.IO.Stream)> déclare qu’un objet de type <xref:System.Object?displayProperty=nameWithType> est retourné. <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.ReadObject(System.IO.Stream)> retourne le type que vous avez spécifié une fois que vous l’avez construit (`List<repo>` dans ce didacticiel). Si la conversion échoue, l’opérateur `as` a la valeur `null`, au lieu de lever une exception.

Nous en avons presque terminé avec cette section. Maintenant que vous avez converti le JSON en objets C#, nous allons afficher le nom de chaque dépôt. Remplacez les lignes :

```csharp
var msg = await stringTask;   //**Deleted this
Console.Write(msg);
```

avec les éléments suivants :

```csharp
foreach (var repo in repositories)
    Console.WriteLine(repo.name);
```

Compilez et exécutez l'application. Cela affichera les noms des espaces de stockage qui font partie de la .NET Foundation.

## <a name="controlling-serialization"></a>Contrôle de la sérialisation

Avant d’ajouter plus de fonctionnalités, nous allons traiter le type `repo` et lui faire suivre les conventions standard C#. Vous verrez comment procéder en annotant le type `repo` avec des *attributs* qui contrôlent la manière dont fonctionne le sérialiseur JSON. Dans votre cas, vous utiliserez ces attributs pour définir un mappage entre les noms de clé JSON et la classe C# et les noms des membres. Les deux attributs utilisés sont l’attribut `DataContract` et l’attribut `DataMember`. Par convention, toutes les classes d’attributs se terminent par le suffixe `Attribute`. Toutefois, il est inutile d’utiliser ce suffixe lorsque vous appliquez un attribut. 

Les attributs `DataContract` et `DataMember` se trouvent dans une autre bibliothèque, vous devez donc ajouter cette bibliothèque à votre fichier de projet C# en tant que dépendance. Ajoutez la ligne suivante à la section `<ItemGroup>` de votre fichier projet :

```xml
<PackageReference Include="System.Runtime.Serialization.Primitives" Version="4.3.0" />
```

Après avoir enregistré le fichier, exécutez `dotnet restore` ([voir note](#dotnet-restore-note)) pour récupérer ce package.

Ensuite, ouvrez le fichier `repo.cs`. Nous allons modifier le nom pour adopter la casse Pascal, et entièrement épeler le nom `Repository`. Nous souhaitons toujours mapper des nœuds de « repo » JSON sur ce type, vous devez donc ajouter l’attribut `DataContract` à la déclaration de classe. Vous devez définir la propriété `Name` de l’attribut sur le nom des nœuds JSON qui correspondent à ce type :

```csharp
[DataContract(Name="repo")]
public class Repository
```

L’attribut <xref:System.Runtime.Serialization.DataContractAttribute> est un membre de l’espace de noms <xref:System.Runtime.Serialization>, vous devez donc l’instruction `using` appropriée au début du fichier :

```csharp
using System.Runtime.Serialization;
```

Vous avez modifié le nom de la classe `repo` en `Repository`, de sorte que vous devrez effectuer le même changement de nom dans le fichier Program.cs (certains éditeurs peuvent prendre en charge une refactorisation de changement de nom qui fera automatiquement cette modification :)

```csharp
var serializer = new DataContractJsonSerializer(typeof(List<Repository>));

// ...

var repositories = serializer.ReadObject(await streamTask) as List<Repository>;
```

Ensuite, nous allons apporter la même modification avec le champ `name` à l’aide de la classe <xref:System.Runtime.Serialization.DataMemberAttribute>. Apportez les modifications suivantes à la déclaration du champ `name` dans repo.cs :

```csharp
[DataMember(Name="name")]
public string Name;
```

Cette modification signifie que vous devez modifier le code qui écrit le nom de chaque dépôt dans program.cs :

```csharp
Console.WriteLine(repo.Name);
```

Effectuez un `dotnet build` suivi d’un `dotnet run` pour vous assurer que vous disposez des bons mappages. Vous devriez voir la même sortie que précédemment. Avant de traiter d’autres propriétés à partir du serveur web, apportons une dernière modification à la classe `Repository`. Le membre `Name` est un champ accessible publiquement. Cela n’est pas une bonne pratique pour les langages orientés objet, nous allons donc le changer en propriété. Pour ce que nous cherchons à faire, nous n’avons pas besoin de code spécifique à exécuter lors de l’obtention ou la définition de la propriété, mais la modification en propriété permettra d’apporter ces modifications plus facilement par la suite sans casser le code qui utilise la classe `Repository`.

Supprimez la définition de champ et remplacez-la par une [propriété implémentée automatiquement](../programming-guide/classes-and-structs/auto-implemented-properties.md) :

```csharp
public string Name { get; set; }
```

Le compilateur génère le corps des accesseurs `get` et `set`, mais aussi un champ privé pour stocker le nom. Cela est similaire au code suivant que vous pourriez taper manuellement :

```csharp
public string Name 
{ 
    get { return this._name; }
    set { this._name = value; }
}
private string _name;
```

Nous allons apporter une modification de plus avant d’ajouter de nouvelles fonctionnalités. La méthode `ProcessRepositories` peut faire le travail de façon asynchrone et renvoyer une collection des espaces de stockage. Nous allons renvoyer `List<Repository>` à partir de cette méthode et déplacer le code qui écrit les informations dans la méthode `Main`.

Modifiez la signature de `ProcessRepositories` pour retourner une tâche dont le résultat est une liste d’objets `Repository` :

```csharp
private static async Task<List<Repository>> ProcessRepositories()
```

Ensuite, retournez simplement les dépôts après le traitement de la réponse JSON :

```csharp
var repositories = serializer.ReadObject(await streamTask) as List<Repository>;
return repositories;
```

Le compilateur génère l’objet `Task<T>` pour la valeur de retour, car vous avez marqué cette méthode comme `async`.
Ensuite, nous allons modifier la méthode `Main` afin qu’elle capture les résultats et écrive le nom de chaque dépôt dans la console. Votre méthode `Main` se présente maintenant comme suit :

```csharp
public static void Main(string[] args)
{
    var repositories = ProcessRepositories().Result;

    foreach (var repo in repositories)
        Console.WriteLine(repo.Name);
}
```

L’accès à la propriété `Result` d’une tâche est bloqué jusqu'à la fin de la tâche. En règle générale, il serait préférable d’utiliser `await` pour attendre l’achèvement de la tâche, comme dans la méthode `ProcessRepositories`, mais cela n’est pas autorisé dans la méthode `Main`.

## <a name="reading-more-information"></a>Lire plus d'informations

Terminons par le traitement d’un certain nombre de propriétés dans le paquet JSON envoyé à partir de l’API GitHub. Vous ne voudrez pas récupérer tous les éléments, mais ajouter quelques propriétés vous permettra de découvrir d’autres fonctionnalités du langage C#.

Commençons par ajouter quelques autres types simples à la définition de classe `Repository`. Ajoutez ces propriétés à cette classe :

```csharp
[DataMember(Name="description")]
public string Description { get; set; }

[DataMember(Name="html_url")]
public Uri GitHubHomeUrl { get; set; }

[DataMember(Name="homepage")]
public Uri Homepage { get; set; }

[DataMember(Name="watchers")]
public int Watchers { get; set; }
```

Ces propriétés ont intégré des conversions intégrées du type chaîne (c’est ce que contiennent les paquets JSON) vers le type cible. Le type <xref:System.Uri> peut être nouveau pour vous. Il représente un URI, ou dans ce cas, une URL. Dans le cas des types `Uri` et `int`, si le paquet JSON contient des données qui ne sont pas convertibles dans le type cible, l’action de sérialisation lèvera une exception.

Une fois que vous avez ajouté cela, mettez à jour la méthode `Main` pour afficher ces éléments :

```csharp
foreach (var repo in repositories)
{
    Console.WriteLine(repo.Name);
    Console.WriteLine(repo.Description);
    Console.WriteLine(repo.GitHubHomeUrl);
    Console.WriteLine(repo.Homepage);
    Console.WriteLine(repo.Watchers);
    Console.WriteLine();
}
```
Dans la dernière étape, nous allons ajouter les informations de la dernière opération Push. Ces informations sont formatées de cette façon dans la réponse JSON :

```json
2016-02-08T21:27:00Z
```

Ce format ne suit pas les formats .NET <xref:System.DateTime> standard. Par conséquent, vous devez écrire une méthode de conversion personnalisée. En outre, vous ne souhaiterez probablement pas que la chaîne brute soit exposée aux utilisateurs de la classe `Repository`. Les attributs permettent aussi de contrôler cela. D’abord, définissez une propriété `private` qui contient la représentation sous forme de chaîne de date et d’heure dans votre classe `Repository` :

```csharp
[DataMember(Name="pushed_at")]
private string JsonDate { get; set; }
```

L’attribut `DataMember` informe le sérialiseur qu’elle doit être traitée, même si elle n’est pas un membre public. Ensuite, vous devez écrire une propriété publique en lecture seule qui convertit la chaîne en un objet <xref:System.DateTime> valide et retourne cette <xref:System.DateTime> :

```csharp
[IgnoreDataMember]
public DateTime LastPush
{
    get
    {
        return DateTime.ParseExact(JsonDate, "yyyy-MM-ddTHH:mm:ssZ", CultureInfo.InvariantCulture);
    }
}
```

Examinons les nouvelles constructions ci-dessus. L’attribut `IgnoreDataMember` indique au sérialiseur que ce type ne doit pas être lu ou écrit à partir de n’importe quel objet JSON. Cette propriété contient uniquement un accesseur `get`. Il n'existe aucun accesseur `set`. C’est la façon dont vous définissez une propriété *en lecture seule* en C#. (Oui, vous pouvez créer des propriétés *en écriture seule* en C#, mais leur intérêt est limité.) La méthode <xref:System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider)> analyse une chaîne et crée un objet <xref:System.DateTime> sous un format de date fourni, puis ajoute des métadonnées supplémentaires à `DateTime` en utilisant un objet `CultureInfo`. Si l’opération d’analyse échoue, l’accesseur de propriété lève une exception.

Pour utiliser <xref:System.Globalization.CultureInfo.InvariantCulture>, vous devez ajouter l’espace de noms <xref:System.Globalization> aux instructions `using` dans `repo.cs` :

```csharp
using System.Globalization;
```

Enfin, ajoutez une dernière instruction de sortie dans la console et vous êtes prêt à générer et exécuter de nouveau cette application :

```csharp
Console.WriteLine(repo.LastPush);
```

Votre version doit maintenant correspondre à l’[exemple terminé](https://github.com/dotnet/docs/tree/master/samples/csharp/getting-started/console-webapiclient).
 
## <a name="conclusion"></a>Conclusion

Ce didacticiel vous a montré comment effectuer des demandes web, analyser le résultat et afficher les propriétés de ces résultats. Vous avez également ajouté de nouveaux packages en tant que dépendances dans votre projet. Vous avez vu certaines des fonctionnalités du langage C# qui prennent en charge des techniques orientées objet.

<a name="dotnet-restore-note"></a>
[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]
