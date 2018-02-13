---
title: "Démarrage rapide - Branches et boucles - Guide C#"
description: "Dans ce guide de démarrage rapide sur les branches et les boucles, vous écrivez du code en C# pour explorer la syntaxe de langage qui prend en charge les branches et boucles conditionnelles pour exécuter des instructions de manière répétée."
author: billwagner
ms.author: wiwagn
ms.date: 10/31/2017
ms.topic: get-started-article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.custom: mvc
ms.openlocfilehash: 609c8625b19025a20c1da1e767870eafbab4c4a0
ms.sourcegitcommit: 8bde7a3432f30fc771079744955c75c58c4eb393
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/20/2018
---
# <a name="branches-and-loops"></a>Branches et boucles

Ce guide de démarrage rapide vous explique comment écrire un code qui examine des variables et modifie un chemin d’exécution en fonction de ces variables. Vous allez écrire un code en C# et afficher les résultats de la compilation et de l’exécution du code. Le guide de démarrage rapide contient une série de leçons pour explorer la création de branches et de boucles en C#. Ces leçons présentent les concepts de base du langage C#.

Ce guide de démarrage rapide suppose que vous disposez d’un ordinateur que vous pouvez utiliser pour le développement. La rubrique .NET [Bien démarrer en 10 minutes](https://www.microsoft.com/net/core) contient des instructions pour configurer votre environnement de développement local sur Mac, PC ou Linux. Une brève vue d’ensemble des commandes que vous utiliserez est disponible dans la [présentation des guides de démarrage rapide locaux](local-environment.md) avec des liens pour plus d’informations.

## <a name="make-decisions-using-the-if-statement"></a>Prendre des décisions à l’aide de l’instruction `if`

Créez un répertoire nommé **branches-quickstart**. Faites-en le répertoire actuel et exécutez `dotnet new console -n BranchesAndLoops -o .`. Cette commande crée une nouvelle application console .NET Core dans le répertoire actuel. 

Ouvrez **Program.cs** dans votre éditeur favori, puis remplacez la ligne `Console.Writeline("Hello World!");` par le code qui suit :

```csharp
int a = 5;
int b = 6;
if (a + b > 10)
    Console.WriteLine("The answer is greater than 10.");
```

Essayez ce code en tapant `dotnet run` dans la fenêtre de console. Le message « La réponse est supérieure à 10 » doit s’afficher dans votre console.

Modifiez la déclaration de `b` pour que la somme soit inférieure à 10 : 

```csharp
int b = 3;
```

Tapez `dotnet run` à nouveau. La réponse étant inférieure à 10, rien ne s’affiche. La **condition** que vous testez a une valeur false. Vous n’avez pas de code à exécuter, car vous avez uniquement écrit l’une des branches possibles pour une instruction `if` : la branche true.

> [!TIP]
> Durant votre exploration de C# (ou de tout autre langage de programmation), vous commettrez des erreurs d’écriture du code. Le compilateur détectera et signalera les erreurs. Observez attentivement la sortie d’erreur et le code ayant généré l’erreur. L’erreur du compilateur peut en général vous aider à trouver le problème. 

Le premier exemple montre la puissance de l’instruction `if` et des types booléens. Un *booléen* est une variable qui peut avoir l’une des deux valeurs suivantes : `true` ou `false`. C# définit un type spécial, `bool`, pour les variables booléennes. L’instruction `if` vérifie la valeur d’un `bool`. Quand la valeur est `true`, l’instruction qui suit `if` s’exécute. Dans le cas contraire, elle est ignorée. 

Ce processus de vérification des conditions et d’exécution des instructions en fonction de ces conditions est très performant.


## <a name="make-if-and-else-work-together"></a>Utiliser if et else ensemble

Pour exécuter un code différent dans les branches true et false, vous créez une branche `else` qui s’exécute quand la condition a une valeur false. Essayez ceci. Ajoutez les deux dernières lignes dans le code ci-dessous à votre méthode `Main` (vous devriez déjà avoir les quatre premières lignes) :

```csharp
int a = 5;
int b = 3;
if (a + b > 10)
    Console.WriteLine("The answer is greater than 10");
else
    Console.WriteLine("The answer is not greater than 10");
```

L’instruction qui suit le mot clé `else` s’exécute uniquement quand la condition testée a une valeur `false`. La combinaison de `if` et `else` avec des conditions booléennes offre les hautes performances dont vous avez besoin pour traiter une condition `true` et une condition `false`.

> [!IMPORTANT]
> La mise en retrait sous les instructions `if` et `else` a simplement pour but de faciliter la lecture.
> Le langage C# ne considère pas la mise en retrait ou les espaces blancs comme des éléments significatifs. L’instruction qui suit le mot clé `if` ou `else` sera exécutée en fonction de la condition. Tous les exemples de ce guide de démarrage rapide suivent une pratique courante pour mettre en retrait les lignes en fonction du flux de contrôle des instructions.

Étant donné que la mise en retrait n’est pas significative, vous devez utiliser `{` et `}` pour indiquer quand vous souhaitez inclure plus d’une instruction dans le bloc qui s’exécute de manière conditionnelle. Les programmeurs C# utilisent généralement les accolades pour toutes les clauses `if` et `else`. L’exemple suivant est identique à celui que vous venez de créer. Modifiez votre code ci-dessus pour qu’il corresponde au code suivant :

```csharp
int a = 5;
int b = 3;
if (a + b > 10)
{
    Console.WriteLine("The answer is greater than 10");
}
else
{
    Console.WriteLine("The answer is not greater than 10");
}
```

> [!TIP]
> Dans le reste de ce guide de démarrage rapide, tous les exemples de code incluent les accolades, conformément aux pratiques acceptées.

Vous pouvez tester des conditions plus complexes. Ajoutez le code suivant à votre méthode `Main` après le code que vous avez écrit jusque-là :

```csharp
    int c = 4;
    if ((a + b + c > 10) && (a > b))
{
    Console.WriteLine("The answer is greater than 10");
    Console.WriteLine("And the first number is greater than the second");
}
else
{
    Console.WriteLine("The answer is not greater than 10");
    Console.WriteLine("Or the first number is not greater than the second");
}
```

`&&` représente « et ». Cela signifie que les deux conditions doivent être true pour que l’instruction s’exécute dans la branche true.  Ces exemples montrent également que vous pouvez avoir plusieurs instructions dans chaque branche conditionnelle, à condition de les mettre entre `{` et `}`.

Vous pouvez également utiliser `||` pour représenter « ou ». Ajoutez le code suivant après ce que vous avez écrit jusque-là :

```csharp
if ((a + b + c > 10) || (a > b))
{
    Console.WriteLine("The answer is greater than 10");
    Console.WriteLine("Or the first number is greater than the second");
}
else
{
    Console.WriteLine("The answer is not greater than 10");
    Console.WriteLine("And the first number is not greater than the second");
}
```

Vous avez terminé la première étape. Avant de passer à la section suivante, déplaçons le code actuel dans une méthode distincte. Cela nous permettra de travailler plus facilement avec un nouvel exemple. Renommez votre méthode `Main` `ExploreIf` et écrivez une nouvelle méthode `Main` qui appelle `ExploreIf`. Une fois terminé, votre code doit ressembler au code suivant :

```csharp
using System;

namespace BranchesAndLoops
{
    class Program
    {
        static void ExploreIf()
        {
            int a = 5;
            int b = 3;
            if (a + b > 10)
            {
                Console.WriteLine("The answer is greater than 10");
            }
            else
            {
                Console.WriteLine("The answer is not greater than 10");
            }

            if ((a + b + c > 10) && (a > b))
            {
                Console.WriteLine("The answer is greater than 10");
                Console.WriteLine("And the first number is greater than the second");
            }
            else
            {
                Console.WriteLine("The answer is not greater than 10");
                Console.WriteLine("Or the first number is not greater than the second");
            }

            if ((a + b + c > 10) || (a > b))
            {
                Console.WriteLine("The answer is greater than 10");
                Console.WriteLine("Or the first number is greater than the second");
            }
            else
            {
                Console.WriteLine("The answer is not greater than 10");
                Console.WriteLine("And the first number is not greater than the second");
            }            
        }

        static void Main(string[] args)
        {
            ExploreIf();
        }
    }
}
```

Commentez l’appel à `ExploreIf()`. La sortie est ainsi moins encombrée lorsque vous travaillez dans cette section :

```csharp
//ExploreIf();
```

`//` démarre un **commentaire** dans C#. Les commentaires correspondent à du texte que vous voulez conserver dans votre code source sans l’exécuter en tant que code. Le compilateur ne génère aucun fichier exécutable à partir des commentaires.

## <a name="use-loops-to-repeat-operations"></a>Utiliser des boucles pour répéter des opérations

Dans cette section vous utilisez des **boucles** pour répéter des instructions. Essayez ce code dans votre méthode `Main` :

```csharp
int counter = 0;
while (counter < 10)
{
    Console.WriteLine($"Hello World! The counter is {counter}");
    counter++;
}
```

L’instruction `while` vérifie une condition et exécute l’instruction ou le bloc d’instructions qui suit `while`. Elle répète la vérification de la condition et l’exécution de ces instructions jusqu'à ce que la condition soit false.

Cet exemple contient un nouvel opérateur. `++` après la variable `counter` est l’opérateur d’**incrémentation**. Il ajoute 1 à la valeur de `counter` et stocke cette valeur dans la variable de `counter`.

> [!IMPORTANT]
> Assurez-vous que la condition de boucle `while` devient false quand vous exécutez le code. Dans le cas contraire, vous allez créer une **boucle infinie** dans laquelle votre programme ne se terminera jamais. Ceci n’est pas démontré dans cet exemple, car vous devez forcer la fermeture de votre programme avec **CTRL-C** ou à l’aide d’autres moyens.

La boucle `while` teste la condition avant d’exécuter le code qui suit `while`. La boucle `do` ... `while` exécute d’abord le code, puis vérifie la condition. La boucle do while est illustrée dans l’exemple de code suivant :

```csharp
counter = 0;
do
{
    Console.WriteLine($"Hello World! The counter is {counter}");
    counter++;
} while (counter < 10);
```

Cette boucle `do` et la boucle antérieure `while` produisent la même sortie.

## <a name="work-with-the-for-loop"></a>Utiliser la boucle for

La boucle **for** est couramment utilisée dans C#. Essayez ce code dans votre méthode Main() :

```csharp
for(int index = 0; index < 10; index++)
{
    Console.WriteLine($"Hello World! The index is {index}");
} 
```

Cette boucle fonctionne de manière identique à la boucle `while` et la boucle `do` que vous avez déjà utilisées. L’instruction `for` comprend trois parties qui contrôlent son fonctionnement. 

La première partie est l’**initialiseur for** : `for index = 0;` déclare que `index` est la variable de boucle et définit sa valeur initiale sur `0`.

La partie centrale est la **condition for** : `index < 10` déclare que cette boucle `for` continue à s’exécuter tant que la valeur de compteur est inférieure à 10.

La dernière partie est l’**itérateur for** : `index++` indique comment modifier la variable de boucle après l’exécution du bloc qui suit l’instruction `for`. Il spécifie ici que `index` doit être incrémenté de 1 chaque fois que le bloc s’exécute.

Vérifiez-le par vous-même. Réalisez les essais suivants :

- Modifiez l’initialiseur pour définir le démarrage à une valeur différente.
- Modifiez la condition pour définir l’arrêt à une valeur différente.

Une fois terminé, vous allez vous-même écrire des codes pour mettre en pratique ce que vous avez appris.

## <a name="combine-branches-and-loops"></a>Combiner des branches et des boucles

Maintenant que vous avez vu l’instruction `if` et la création de boucles en langage C#, vérifiez si vous pouvez écrire un code C# pour obtenir la somme de tous les entiers de 1 à 20 divisibles par 3.  Voici quelques conseils :

- L’opérateur `%` vous donne le reste d’une opération de division.
- L’instruction `if` vous donne la condition pour vérifier si un nombre doit être inclus dans la somme.
- La boucle `for` peut vous aider à répéter une série d’étapes pour tous les nombres de 1 à 20.

Essayez par vous-même et vérifiez le résultat. Vous devriez obtenir 63 comme réponse. Vous pouvez voir une réponse possible en [consultant le code terminé sur GitHub](https://github.com/dotnet/docs/tree/master/samples/csharp/branches-quickstart/Program.cs#L46-L54).

Vous avez terminé le guide de démarrage rapide « Branches et boucles ».

Vous pouvez passer au démarrage rapide [Chaînes interpolées](interpolated-strings-local.md) dans votre propre environnement de développement.

Pour en savoir plus sur ces concepts, consultez les rubriques suivantes :

[Instruction if et else](../language-reference/keywords/if-else.md)   
[Instruction while](../language-reference/keywords/while.md)   
[Instruction do](../language-reference/keywords/do.md)   
[Instruction for](../language-reference/keywords/for.md)   
