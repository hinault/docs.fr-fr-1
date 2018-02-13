---
title: "Démarrage rapide - Nombres en C# - Guide C#"
description: "Découvrez C# en explorant les types numériques, leurs propriétés et méthodes."
author: billwagner
ms.author: wiwagn
ms.date: 10/31/2017
ms.topic: get-started-article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.custom: mvc
ms.openlocfilehash: 9a7f061de23c632560f40ac5eb46defd4537da16
ms.sourcegitcommit: 8bde7a3432f30fc771079744955c75c58c4eb393
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/20/2018
---
# <a name="numbers-in-c-quick-start"></a>Démarrage rapide Nombres en C# #

Ce guide de démarrage rapide vous permet de découvrir de manière interactive les types numériques en C#. Vous allez écrire de petites quantités de code, puis vous compilerez et exécuterez ce code. Ce guide de démarrage rapide contient une série de leçons pour explorer les nombres et les opérations mathématiques en C#. Ces leçons présentent les concepts de base du langage C#.

Ce guide de démarrage rapide suppose que vous disposez d’un ordinateur que vous pouvez utiliser pour le développement. La rubrique .NET [Bien démarrer en 10 minutes](https://www.microsoft.com/net/core) contient des instructions pour configurer votre environnement de développement local sur Mac, PC ou Linux. Une brève vue d’ensemble des commandes que vous utiliserez est disponible dans la [présentation des guides de démarrage rapide locaux](local-environment.md) avec des liens pour plus d’informations.

## <a name="explore-integer-math"></a>Explorer les mathématiques avec des entiers

Créez un répertoire nommé **numbers-quickstart**. Faites-en le répertoire actuel et exécutez `dotnet new console -n NumbersInCSharp -o .`.

Ouvrez **Program.cs** dans votre éditeur favori, puis remplacez la ligne `Console.Writeline("Hello World!");` par ce qui suit :

```csharp
int a = 18;
int b = 6;
int c = a + b;
Console.WriteLine(c);
```

Exécutez ce code en tapant `dotnet run` dans votre fenêtre de commande. 

Vous venez d’observer l’une des opérations mathématiques de base avec des entiers. Le type `int` représente un **entier**, qui peut être positif ou négatif. Vous utilisez le symbole `+` pour effectuer une addition. Les autres opérations mathématiques courantes avec des entiers sont les suivantes :

- `-` pour la soustraction
- `*` pour la multiplication
- `/` pour la division

Commencez par explorer ces différentes opérations. Ajoutez ces lignes après la ligne qui écrit la valeur de `c` :

```csharp
c = a - b;
Console.WriteLine(c);
c = a * b;
Console.WriteLine(c);
c = a / b;
Console.WriteLine(c);
```

Exécutez ce code en tapant `dotnet run` dans votre fenêtre de commande. 
    
Vous pouvez également, si vous le souhaitez, effectuer des essais en réalisant plusieurs opérations mathématiques dans la même ligne. Essayez `c = a + b - 12 * 17;` par exemple. La combinaison de variables et de nombres constants est autorisée.

> [!TIP]
> Durant votre exploration de C# (ou de tout autre langage de programmation), vous commettrez des erreurs d’écriture du code. Le **compilateur** détectera ces erreurs et vous les signalera. Si la sortie contient des messages d’erreur, vérifiez attentivement l’exemple de code ainsi que le code dans votre fenêtre pour identifier les corrections à apporter.
> Cet exercice vous aidera à mieux comprendre la structure du code C#.     

Vous avez terminé la première étape. Avant de passer à la section suivante, déplaçons le code actuel dans une méthode distincte. Cela nous permettra de travailler plus facilement avec un nouvel exemple. Renommez votre méthode `Main` `WorkingWithIntegers` et écrivez une nouvelle méthode `Main` qui appelle `WorkingWithIntegers`. Une fois terminé, votre code doit ressembler au code suivant :

```csharp
using System;

namespace NumbersInCSharp
{
    class Program
    {
        static void WorkingWithIntegers()
        {
            int a = 18;
            int b = 6;
            int c = a + b;
            Console.WriteLine(c);
            c = a - b;
            Console.WriteLine(c);
            c = a * b;
            Console.WriteLine(c);
            c = a / b;
            Console.WriteLine(c);
        }

        static void Main(string[] args)
        {
            WorkingWithIntegers();
        }
    }
}
```

## <a name="explore-order-of-operations"></a>Explorer l’ordre des opérations

Commentez l’appel à `WorkingWithIntegers()`. La sortie est ainsi moins encombrée lorsque vous travaillez dans cette section :

```csharp
//WorkingWithIntegers();
```

`//` démarre un **commentaire** dans C#. Les commentaires correspondent à du texte que vous voulez conserver dans votre code source sans l’exécuter en tant que code. Le compilateur ne génère aucun fichier exécutable à partir des commentaires.

Le langage C# définit la priorité des différentes opérations mathématiques avec à l’aide de règles cohérentes avec les règles mathématiques que vous avez apprises.
La multiplication et la division ont priorité sur l’addition et la soustraction.
Explorez ce concept en ajoutant le code suivant à votre méthode `Main` et en exécutant `dotnet run` :

```csharp
int a = 5;
int b = 4;
int c = 2;
int d = a + b * c;
Console.WriteLine(d);
 ```

La sortie montre que la multiplication est effectuée avant l’addition.

Vous pouvez appliquer un ordre de calcul différent en mettant entre parenthèses la ou les opérations à exécuter en premier. Ajoutez les lignes suivantes et exécutez à nouveau :

```csharp
d = (a  + b) * c;
Console.WriteLine(d);
```

Pratiquez en combinant plusieurs opérations différentes. Ajoutez quelque chose ressemblant aux lignes suivantes au bas de votre méthode `Main`. Essayez `dotnet run` à nouveau.

```csharp
d = (a + b) - 6 * c + (12 * 4) / 3 + 12;
Console.WriteLine(d);
```

Vous avez peut-être observé un comportement intéressant des entiers. La division d’entiers produit toujours un résultat entier, même quand vous pensez que le résultat devrait inclure une partie décimale ou fractionnaire.

Si vous n’avez pas observé ce comportement, essayez le code qui suit à la fin de votre méthode `Main` :

```csharp
int e = 7;
int f = 4;
int g = 3;
int h = (e  + f) / g;
Console.WriteLine(h);
```

Tapez `dotnet run` à nouveau pour afficher les résultats.

Avant de continuer, prenez tout le code que vous avez écrit dans cette section et placez-le dans une nouvelle méthode. Nommez cette nouvelle méthode `OrderPrecedence`.
Vous devriez obtenir un résultat similaire à celui-ci :

```csharp
using System;

namespace NumbersInCSharp
{
    class Program
    {
        static void WorkingWithIntegers()
        {
            int a = 18;
            int b = 6;
            int c = a + b;
            Console.WriteLine(c);
            c = a - b;
            Console.WriteLine(c);
            c = a * b;
            Console.WriteLine(c);
            c = a / b;
            Console.WriteLine(c);
        }

        static void OrderPrecedence()
        {   
            int a = 5;
            int b = 4;
            int c = 2;
            int d = a + b * c;
            Console.WriteLine(d);

            d = (a  + b) * c;
            Console.WriteLine(d);

            d = (a + b) - 6 * c + (12 * 4) / 3 + 12;
            Console.WriteLine(d);

            int e = 7;
            int f = 4;
            int g = 3;
            int h = (e  + f) / g;
            Console.WriteLine(h);
        }

        static void Main(string[] args)
        {
            WorkingWithIntegers();

            OrderPrecedence();

        }
    }
}
```

## <a name="explore-integer-precision-and-limits"></a>Explorer la précision et les limites des entiers
Ce dernier exemple a montré que la division d’entiers tronque le résultat.
Vous pouvez obtenir le **reste** à l’aide de l’opérateur **modulo**, à savoir le caractère `%`. Essayez le code suivant dans votre méthode `Main` :

```csharp
int a = 7;
int b = 4;
int c = 3;
int d = (a  + b) / c;
int e = (a + b) % c;
Console.WriteLine($"quotient: {d}");
Console.WriteLine($"remainder: {e}");
```

Le type d’entier C# diffère des entiers mathématiques d’une autre manière : le type `int` a des limites minimale et maximale. Ajoutez ce code à votre méthode `Main` pour voir ces limites :
    
```csharp
int max = int.MaxValue;
int min = int.MinValue;
Console.WriteLine($"The range of integers is {min} to {max}");
```

Si un calcul produit une valeur qui dépasse ces limites, vous obtenez une condition de **dépassement négatif** ou **dépassement positif**. La réponse affichée indique la plage (d’une limite à l’autre). Ajoutez ces deux lignes à votre méthode `Main` pour voir un exemple :

```csharp
int what = max + 3;
Console.WriteLine($"An example of overflow: {what}");
```
    
Notez que la réponse est très proche de l’entier minimal (négatif). Il en est de même pour `min + 2`. L’addition a produit un **dépassement négatif** des valeurs autorisées pour les entiers.
La réponse est un très grand nombre négatif, car un dépassement négatif « inclut » de la plus grande valeur d’entier possible à la plus petite.

Il existe d’autres types numériques avec une précision et des limites différentes que vous pouvez utiliser quand le type `int` ne répond pas à vos besoins. Nous les explorerons à l’étape suivante.

Encore une fois, déplaçons le code que vous avez écrit dans cette section vers une autre méthode. Nommez-le `TestLimits`. 

## <a name="work-with-the-double-type"></a>Utiliser le type double

Le type numérique `double` représente un nombre à virgule flottante double précision. Ces termes vous sont peut-être inconnus. Un nombre **à virgule flottante** est utile pour représenter de très grands ou petits nombres non intégraux. La **double précision** signifie que ces nombres sont stockés avec une précision supérieure à la **simple précision**. Sur les ordinateurs modernes, les nombres double précision sont généralement plus utilisés que les nombres simple précision.
Explorons ce type double. Ajoutez le code suivant et affichez le résultat :

```csharp
double a = 5;
double b = 4;
double c = 2;
double d = (a  + b) / c;
Console.WriteLine(d);
```

Notez que la réponse inclut la partie décimale du quotient. Essayez avec une expression légèrement plus complexe utilisant des doubles :

```csharp
double e = 19;
double f = 23;
double g = 8;
double h = (e  + f) / g;
Console.WriteLine(h);
```

La plage d’une valeur double est nettement supérieure à celle de valeurs entières. Essayez le code suivant sous ce que vous avez écrit jusque-là :

```csharp
double max = double.MaxValue;
double min = double.MinValue;
Console.WriteLine($"The range of double is {min} to {max}");
```

Ces valeurs s’affichent sous forme de notation scientifique. Le nombre à gauche du `E` est le nombre significatif. Le nombre à droite est l’exposant, en puissance de 10. 

Tout comme les nombres décimaux en mathématiques, les doubles en C# peuvent présenter des erreurs d’arrondi. Exécutez le code suivant :

```csharp
double third = 1.0 / 3.0;
Console.WriteLine(third);
```

Vous savez que la valeur extensible `0.3` ne correspond pas exactement à `1/3`.

***Test***

Effectuez d’autres calculs avec des grands nombres, des petits nombres, des multiplications et des divisions à l’aide du type `double`.  Effectuez des calculs plus complexes.

Après avoir consacré plus de temps au test, placez le code que vous avez écrit dans une nouvelle méthode. Nommez cette nouvelle méthode `WorkWithDoubles`.

## <a name="work-with-fixed-point-types"></a>Utiliser des types de virgule fixe

Vous avez vu les types numériques de base en C#, à savoir les entiers et les doubles.  Il existe un autre type à découvrir : le type `decimal`. Le type `decimal` a une plage plus petite, mais une précision supérieure à celle du type `double`. Le terme **virgule fixe** signifie que la virgule décimale (ou virgule binaire) ne se déplace pas. Étudions cela d’un peu plus près :

```csharp
decimal min = decimal.MinValue;
decimal max = decimal.MaxValue;
Console.WriteLine($"The range of the decimal type is {min} to {max}");
```

Notez que la plage est plus petite que celle du type `double`. Vous pouvez observer la plus haute précision du type décimal en exécutant le code suivant :

```csharp
double a = 1.0;
double b = 3.0;
Console.WriteLine(a / b);

decimal c = 1.0M;
decimal d = 3.0M;
Console.WriteLine(c / d);
```

Le suffixe `M` des nombres permet d’indiquer comment une constante doit utiliser le type `decimal`.

Notez que le calcul utilisant le type décimal a plus de chiffres à droite de la virgule décimale. 

***Test***

Maintenant que vous avez vu les différents types numériques, écrivez un code qui calcule la surface d’un cercle avec un rayon de 2,5 pouces. Rappelez-vous que la surface d’un cercle est le rayon au carré multiplié par PI. Conseil : .NET contient une constante pour PI, à savoir <xref:System.Math.PI?displayProperty=nameWithType>, que vous pouvez utiliser pour cette valeur. 

Vous devriez obtenir une réponse comprise entre 19 et 20.
Vous pouvez vérifier votre réponse en [consultant l’exemple de code terminé sur GitHub](https://github.com/dotnet/docs/tree/master/samples/csharp/numbers-quickstart/Program.cs#L104-L106)

Si vous le voulez, essayez d’autres formules. 

Vous avez terminé le guide de démarrage rapide « Nombres en C# ». Vous pouvez passer au démarrage rapide [Branches et boucles](branches-and-loops-local.md) dans votre propre environnement de développement.

Pour en savoir plus sur les nombres en C#, consultez les rubriques suivantes :

[Tableau des types intégraux](../language-reference/keywords/integral-types-table.md)   
[Tableau des types virgule flottante](../language-reference/keywords/floating-point-types-table.md)   
[Tableau des types intégrés](../language-reference/keywords/built-in-types-table.md)   
[Tableau des conversions numériques implicites](../language-reference/keywords/implicit-numeric-conversions-table.md)   
[Tableau des conversions numériques explicites](../language-reference/keywords/explicit-numeric-conversions-table.md)

