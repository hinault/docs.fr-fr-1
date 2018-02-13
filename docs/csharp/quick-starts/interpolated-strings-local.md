---
title: "Démarrage rapide - Chaînes interpolées - Guide C#"
description: "Dans ce guide de démarrage rapide sur les chaînes interpolées, vous écrivez du code C# de façon à inclure le résultat d’une expression dans une chaîne plus grande."
author: rpetrusha
ms.author: ronpet
ms.date: 01/11/2018
ms.topic: get-started-article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.custom: mvc
ms.openlocfilehash: 14185dd4e364f12756541ac6401d1c6ff3206fe9
ms.sourcegitcommit: 8bde7a3432f30fc771079744955c75c58c4eb393
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/20/2018
---
# <a name="interpolated-strings"></a>Chaînes interpolées

Ce guide de démarrage rapide explique comment utiliser des chaînes interpolées en C# pour insérer des valeurs dans une chaîne à sortie unique. Vous allez écrire un code en C# et afficher les résultats de la compilation et de l’exécution du code. Le guide de démarrage rapide contient une série de leçons qui insèrent des valeurs dans des chaînes et mettent en forme ces valeurs de différentes façons.

Ce guide de démarrage rapide suppose que vous disposez d’un ordinateur que vous pouvez utiliser pour le développement. La rubrique .NET [Bien démarrer en 10 minutes](https://www.microsoft.com/net/core) contient des instructions pour configurer votre environnement de développement local sur Mac, PC ou Linux. Une brève vue d’ensemble des commandes que vous utiliserez est disponible dans la [présentation des guides de démarrage rapide locaux](local-environment.md) avec des liens pour plus d’informations. 

## <a name="create-an-interpolated-string"></a>Créer une chaîne interpolée

Créez un répertoire nommé **interpolated-quickstart**. Faites-en le répertoire actif et exécutez la commande suivante à partir d’une fenêtre de console :

```console
dotnet new console -n interpolated -o .
```

Cette commande crée une nouvelle application console .NET Core dans le répertoire actuel.

Ouvrez **Program.cs** dans votre éditeur favori, puis remplacez la ligne `Console.WriteLine("Hello World!");` par le code qui suit, en remplaçant `<name>` par votre nom :

```csharp
var name = "<name>";
Console.WriteLine($"Hello, {name}. It's a pleasure to meet you!");
```
Essayez ce code en tapant `dotnet run` dans la fenêtre de console. Quand vous exécutez le programme, il affiche une chaîne unique qui inclut votre nom dans le message d’accueil. La chaîne incluse dans l’appel de méthode <xref:System.Console.WriteLine%2A> est une *chaîne interpolée*. C’est un genre de modèle qui vous permet de construire une chaîne unique (appelée *chaîne de résultat*) à partir d’une chaîne qui comprend du code incorporé. Les chaînes interpolées sont particulièrement utiles pour insérer des valeurs dans une chaîne ou pour concaténer (joindre) des chaînes. 
    
Cet exemple simple contient les deux éléments que chaque chaîne interpolée doit avoir : 

- Un littéral de chaîne qui commence par le caractère `$` avant ses guillemets ouvrants. Il ne peut pas y avoir d’espace entre le symbole `$` et les guillemets. (Si vous voulez voir ce qui se passe si vous en incluez un, insérez un espace après le caractère `$`, enregistrez le fichier et réexécutez le programme en tapant `dotnet run` dans la fenêtre de console. Le compilateur C# affiche un message d’erreur « Erreur CS1056 : caractère inattendu ’$’ ».) 

- Une ou plusieurs *expressions interpolées*. Une expression interpolée est indiquée par des accolades ouvrantes et fermantes (`{` et `}`). Vous pouvez placer n’importe quelle expression C# qui retourne une valeur (notamment `null`) à l’intérieur des accolades. 

Essayons quelques autres exemples de chaînes interpolées avec d’autres types de données.
    
## <a name="include-different-data-types"></a>Inclure différents types de données

Dans la section précédente, vous avez utilisé une chaîne interpolée pour insérer une chaîne à l’intérieur d’une autre. Une expression de chaîne interpolée peut toutefois être de n’importe quel type de données. Essayons une chaîne interpolée qui a des valeurs de plusieurs types de données. 
    
L’exemple suivant comprend des expressions interpolées avec un objet `Vegetable`, un membre de l’énumération `Unit`, une valeur <xref:System.DateTime> et une valeur <xref:System.Decimal>. Remplacez tout le code C# dans votre éditeur par le code suivant, puis utilisez la commande `console run` pour l’exécuter :

```csharp
using System;

public class Vegetable
{
   public Vegetable(string name) => Name = name;
   
   public string Name { get; }
   
   public override string ToString() => Name;
}

public class Example
{
   public enum Unit { item, pound, ounce, dozen };
   
   public static void Main()
   {
      var item = new Vegetable("eggplant");
      var date = DateTime.Now;
      var price = 1.99m;
      var unit = Unit.item;
      Console.WriteLine($"On {date}, the price of {item} was {price} per {unit}.");
   }
}
```
    
Notez que la deuxième expression interpolée comprend l’objet `item` dans la chaîne de résultat affichée dans la console, et dans ce cas la chaîne « eggplant » est insérée dans la chaîne de résultat. Cela est dû au fait que lorsque le type d’une expression interpolée n’est pas une chaîne, le compilateur Visual C# effectue les opérations suivantes :

- Si l’expression interpolée est `null`, elle retourne une chaîne vide (« », ou <xref:System.String.Empty?displayProperty=nameWithType>).

- Si l’expression interpolée n’est pas `null`, la méthode `ToString` du type de l’expression interpolée est appelée. Vous pouvez tester cela en commentant la définition de la méthode `Vegetable.ToString` dans l’exemple en plaçant un symbole de commentaire (`//`) devant elle. Dans la sortie, la chaîne « eggplant » est remplacée par le nom de type, « Vegetable », ce qui est le comportement par défaut de la méthode <xref:System.Object.ToString?displayProperty=nameWithType>.   

Dans la sortie de cet exemple, la date est trop précise (le prix des aubergines ne varie pas chaque seconde) et la valeur du prix n’indique pas de devise. Dans la section suivante, vous découvrirez comment résoudre ces problèmes en contrôlant le format des chaînes retournées par les expressions interpolées.

## <a name="control-the-formatting-of-interpolated-expressions"></a>Contrôler la mise en forme des expressions interpolées

Dans la section précédente, deux chaînes à la mise en forme incorrecte ont été insérées dans la chaîne de résultat. L’une était une valeur de date et d’heure pour laquelle seule la date était appropriée. La deuxième était un prix qui n’indiquait pas la devise. Ces deux problèmes sont faciles à résoudre. Les expressions interpolées peuvent inclure des *chaînes de format* qui contrôlent la mise en forme de types particuliers. Modifiez l’appel à `Console.WriteLine` dans l’exemple précédent de façon à inclure le spécificateur de format pour les champs de date et de prix, comme indiqué sur la ligne suivante :

```csharp
Console.WriteLine($"On {date:d}, the price of {item} was {price:C2} per {unit}.");
```
    
Vous spécifiez une chaîne de format en plaçant après l’expression interpolée un signe deux-points et la chaîne de format. « d » est une [chaîne de format de date et d’heure standard](../../standard/base-types/standard-date-and-time-format-strings.md#the-short-date-d-format-specifier) qui représente le format de date courte. « C2 » est une [chaîne de format numérique standard](../../standard/base-types/standard-numeric-format-strings.md#the-currency-c-format-specifier) qui représente un nombre sous forme de valeur monétaire avec deux chiffres après la virgule.

Plusieurs types dans les bibliothèques .NET Standard prennent en charge un ensemble prédéfini de chaînes de format. Il s’agit notamment de tous les types numériques et des types de date et d’heure. Pour obtenir une liste complète des types qui prennent en charge les chaînes de format, consultez [Chaînes de format et types de bibliothèque de classes .NET](../../standard/base-types/formatting-types.md#stringRef) dans l’article [Mise en forme des types dans .NET](../../standard/base-types/formatting-types.md). Tout type peut prendre en charge un ensemble de chaînes de format, et vous pouvez également développer des extensions de mise en forme personnalisées qui fournissent une mise en forme personnalisée pour des types existants. Pour plus d’informations sur la mise en forme personnalisée à l’aide d’une implémentation<xref:System.ICustomFormatter>, consultez [Mise en forme personnalisée avec ICustomFormatter](../../standard/base-types/formatting-types.md#custom-formatting-with-icustomformatter) dans l’article [Mise en forme des types dans .NET](../../standard/base-types/formatting-types.md).

Essayez de modifier les chaînes de format dans votre éditeur de texte et, chaque fois que vous apportez une modification, réexécutez le programme pour voir comment les modifications affectent la mise en forme de la date et de l’heure et la valeur numérique. Remplacez le « d » dans `{date:d}` par « t » (pour afficher le format d’heure courte), « y » (pour afficher l’année et mois) et « yyyy » (pour afficher l’année sous forme de nombre à quatre chiffres). Remplacez le « C2 » dans `{price:C2}` par « e » (pour la notation exponentielle) et « F3 » (pour une valeur numérique avec trois chiffres après la virgule).

En plus de la mise en forme, vous pouvez aussi contrôler la largeur de champ et l’alignement des chaînes retournées par une expression interpolée. Dans la section suivante, vous allez découvrir comment effectuer cette opération.

## <a name="control-the-field-width-and-alignment-of-interpolated-expressions"></a>Contrôler la largeur de champ et l’alignement des expressions interpolées

En règle générale, quand la chaîne retournée par une expression interpolée est comprise dans une chaîne de résultat, elle ne comporte aucun espace de début ou de fin. En particulier pour les instances dans lesquelles vous travaillez avec un jeu de données, les expressions interpolées vous permettent de spécifier la largeur d’un champ et son alignement. Pour voir cela, remplacez tout le code dans votre éditeur de texte par le code suivant, puis tapez `console run` pour exécuter le programme :
    
```csharp
using System;
using System.Collections.Generic;

public class Example
{
   public static void Main()
   {
      var titles = new Dictionary<string, string>();
      titles.Add("Doyle, Arthur Conan", "Hound of the Baskervilles, The");
      titles.Add("London, Jack", "Call of the Wild, The");
      titles.Add("Shakespeare, William", "Tempest, The");

      Console.WriteLine("Author and Title List");
      Console.WriteLine($"\n{"Author",-25}    {"Title",30}\n");
      foreach (var title in titles)
         Console.WriteLine($"{title.Key,-25}     {title.Value,30}");
   }
}
```
    
Les noms des auteurs sont alignés à gauche, et leurs titres sont alignés à droite. Vous spécifiez l’alignement en ajoutant une virgule (« , ») après l’expression et en spécifiant la largeur du champ. Si la largeur du champ est un nombre positif, le champ est aligné à droite :

```text
{expression, width}
```

Si la largeur du champ est un nombre négatif, le champ est aligné à gauche :

```text
{expression, -width}
```

Essayez de supprimer les signes négatifs des expressions interpolées `{"Author",-25}` et `{title.Key,-25}`, puis réexécutez l’exemple, comme avec le code suivant :

```csharp
Console.WriteLine($"\n{"Author",-25}    {"Title",30}\n");
foreach (var title in titles)
   Console.WriteLine($"{title.Key,-25}     {title.Value,30}");
```

Cette fois, les informations sur l’auteur sont alignées à droite.

Vous pouvez combiner une largeur de champ et une chaîne de format dans une même expression interpolée. La largeur du champ figure en premier, suivie d’un signe deux-points et de la chaîne de format. Remplacez tout le code à l’intérieur de la méthode `Main` par le code suivant, qui affiche trois chaînes mises en forme avec des largeurs de champ définies. Ensuite, exécutez le programme en entrant la commande `dotnet run`.

```csharp
Console.WriteLine($"{DateTime.Now,-20:d} Hour {DateTime.Now,-10:HH} {1063.342,15:N2} feet");
```
La sortie ressemble à ceci :

```console
1/11/2018            Hour 09                1,063.34 feet
```

Vous avez terminé le guide de démarrage rapide sur les chaînes interpolées. 
    
Vous pouvez passer au démarrage rapide [Tableaux et collections](arrays-and-collections.md) dans votre propre environnement de développement.

Plus d’informations sur l’utilisation des chaînes interpolées, consultez la rubrique [Chaînes interpolées](../language-reference/keywords/interpolated-strings.md) dans la référence de C#.

