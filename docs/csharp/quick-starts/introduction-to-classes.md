---
title: "Guides de démarrage rapide - Introduction aux classes - Guide C#"
description: "Créez votre premier programme C# et explorez les concepts orientés objet"
author: billwagner
ms.author: wiwagn
ms.date: 10/11/2017
ms.topic: get-started-article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.custom: mvc
ms.openlocfilehash: 4e15b1b12b9420ca1781eca3f2578fa24c9ec82a
ms.sourcegitcommit: 8bde7a3432f30fc771079744955c75c58c4eb393
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/20/2018
---
# <a name="introduction-to-classes"></a>Introduction aux classes

Ce guide de démarrage rapide suppose que vous disposez d’un ordinateur que vous pouvez utiliser pour le développement. La rubrique .NET [Bien démarrer en 10 minutes](https://www.microsoft.com/net/core) contient des instructions pour configurer votre environnement de développement local sur Mac, PC ou Linux. Une brève vue d’ensemble des commandes que vous utiliserez est disponible dans la [présentation des guides de démarrage rapide locaux](local-environment.md) avec des liens pour plus d’informations.

## <a name="create-your-application"></a>Créer une application

Dans une fenêtre de terminal, créez un répertoire nommé **classes**. Vous y créerez votre application. Sélectionnez ce répertoire et tapez `dotnet new console` dans la fenêtre de console. Cette commande crée votre application. Ouvrez **Program.cs**. Le résultat doit être semblable à ce qui suit :

```csharp
using System;

namespace classes
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

Dans ce guide de démarrage rapide, vous allez créer des types qui représentent un compte bancaire. Les développeurs définissent généralement chaque classe dans un fichier texte différent. Cela simplifie la gestion au fur et à mesure qu’un programme augmente en taille.  Créez un fichier nommé **BankAccount.cs** dans le répertoire **classes**. 

Ce fichier contiendra la définition d’un ***compte bancaire***. La programmation orientée objet organise le code en créant des types sous la forme de ***classes***. Ces classes contiennent le code qui représente une entité spécifique. La classe `BankAccount` représente un compte bancaire. Le code implémente des opérations spécifiques à travers des méthodes et des propriétés. Dans ce guide de démarrage rapide, le compte bancaire prend en charge le comportement suivant :

1. Il contient un numéro à 10 chiffres qui identifie le compte bancaire de manière unique.
1. Il contient une chaîne qui stocke le nom du ou des détenteurs.
1. Le solde peut être récupéré.
1. Il accepte les dépôts.
1. Il accepte les retraits.
1. Le solde initial doit être positif.
1. Les retraits ne peuvent pas générer un solde négatif.

## <a name="define-the-bank-account-type"></a>Définir le type de compte bancaire

Vous pouvez commencer par créer les éléments de base d’une classe définissant ce comportement. Le résultat doit être semblable à ce qui suit :

```csharp
using System;

namespace classes
{
    public class BankAccount
    {
        public string Number { get; }
        public string Owner { get; set; }
        public decimal Balance { get; }

        public void MakeDeposit(decimal amount, DateTime date, string note)
        {
        }

        public void MakeWithdrawal(decimal amount, DateTime date, string note)
        {
        }
    }
}
```

Avant de poursuivre, examinons ce que vous venez de créer.  La déclaration `namespace` permet d’organiser logiquement votre code. Ce guide de démarrage rapide étant relativement petit, vous allez placer tout le code dans un même espace de noms. 

`public class BankAccount` définit la classe ou le type que vous créez. Tout ce qui est situé entre `{` et `}` après la déclaration de classe définit le comportement de la classe. La classe `BankAccount` a cinq ***membres***. Les trois premiers sont des ***propriétés***. Les propriétés sont des éléments de données qui peuvent avoir un code qui applique la validation ou d’autres règles. Les deux derniers sont des ***méthodes***. Les méthodes sont des blocs de code qui effectuent une fonction unique. La lecture des noms de chacun des membres doit fournir suffisamment d’informations pour vous permettre (ou à tout autre développeur) de comprendre ce que fait la classe.

## <a name="open-a-new-account"></a>Ouvrir un nouveau compte

La première fonctionnalité à implémenter est l’ouverture d’un compte bancaire. Quand un client ouvre un compte, il doit fournir un solde initial, ainsi que des informations sur le ou les détenteurs du compte. 

La création d’un objet du type `BankAccount` suppose la définition d’un ***constructeur*** qui assigne ces valeurs. Un ***constructeur*** est un membre qui porte le même nom que la classe. Il est utilisé pour initialiser des objets de ce type de classe. Ajoutez le constructeur suivant au type `BankAccount` :

```csharp
public BankAccount(string name, decimal initialBalance)
{
    this.Owner = name;
    this.Balance = initialBalance;
}
```

Les constructeurs sont appelés quand vous créez un objet à l’aide de [`new`](../language-reference/keywords/new.md). Remplacez la ligne `Console.WriteLine("Hello World!");` dans ***program.cs*** par la ligne suivante (remplacez `<name>` par votre nom) :

```csharp
var account = new BankAccount("<name>", 1000);
Console.WriteLine($"Account {account.Number} was created for {account.Owner} with {account.Balance} initial balance.");
```

Tapez `dotnet run` pour observer ce qui se passe.  

Avez-vous remarqué que le numéro de compte est vide ? L’heure est venue de traiter ce point. Le numéro de compte doit être assigné une fois l’objet construit. Mais ce ne devrait pas être à l’appelant de le créer. Le code de la classe `BankAccount` devrait savoir comment assigner de nouveaux numéros de compte.  Un moyen simple de le faire consiste à commencer par un numéro à 10 chiffres. Incrémentez-le chaque fois qu’un compte est créé. Enfin, stockez le numéro de compte actuel quand un objet est construit.

Ajoutez la déclaration de membre suivante à la classe `BankAccount` :

```csharp
private static int accountNumberSeed = 1234567890;
```

Il s’agit d’un membre de données. Celui-ci est `private`, ce qui signifie qu’il est uniquement accessible par code dans la classe `BankAccount`. C’est un moyen de séparer les responsabilités publiques (comme disposer d’un numéro de compte) de l’implémentation privée (c’est-à-dire la façon dont les numéros de compte sont générés). Ajoutez les deux lignes suivantes au constructeur pour assigner le numéro de compte :

```csharp
this.Number = accountNumberSeed.ToString();
accountNumberSeed++;
```

Tapez `dotnet run` pour afficher les résultats.

## <a name="create-deposits-and-withdrawals"></a>Créer des dépôts et des retraits

La classe de votre compte bancaire doit accepter les dépôts et les retraits pour fonctionner correctement. Nous allons implémenter des dépôts et des retraits en créant un journal de chaque transaction du compte. Ce dernier présente plusieurs avantages par rapport à la simple mise à jour du solde à chaque transaction. L’historique peut être utilisé pour auditer toutes les transactions et gérer les soldes au quotidien. En calculant le solde à partir de l’historique de toutes les transactions lorsque nécessaire, toutes les erreurs d’une même transaction qui sont résolues apparaîtront correctement dans le solde dans le calcul suivant.

Commençons par créer un type pour représenter une transaction. Il s’agit d’un type simple qui n’a aucune responsabilité. Il a besoin de quelques propriétés. Créez un fichier nommé ***Transaction.cs***. Ajoutez-y le code suivant :

[!code-csharp[Transaction](../../../samples/csharp/classes-quickstart/Transaction.cs "Transaction declaration")]

Nous allons maintenant ajouter une <xref:System.Collections.Generic.List%601> d’objets `Transaction` à la classe `BankAccount`. Ajoutez la déclaration suivante :

[!code-csharp[TransactionDecl](../../../samples/csharp/classes-quickstart/BankAccount.cs#TransactionDeclaration "Transaction declaration")]

Avec la classe <xref:System.Collections.Generic.List%601>, vous devez importer un espace de noms différent. Ajoutez le code suivant au début de **BankAccount.cs** :

```csharp
using System.Collections.Generic;
```

Nous allons à présent modifier la façon dont le `Balance` est présenté.  Il peut être obtenu en additionnant les valeurs de toutes les transactions. Modifiez la déclaration de `Balance` dans la classe `BankAccount` comme suit :

[!code-csharp[BalanceComputation](../../../samples/csharp/classes-quickstart/BankAccount.cs#BalanceComputation "Computing the balance")]

Cet exemple montre un aspect important des ***propriétés***. Vous calculez à présent le solde quand un autre programmeur en demande la valeur. Votre calcul énumère toutes les transactions et retourne la somme en tant que solde actuel.

Implémentez ensuite les méthodes `MakeDeposit` et `MakeWithdrawal`. Ces méthodes appliquent les deux règles finales suivantes : le solde initial doit être positif et un retrait ne doit pas générer de solde négatif. 

Cela introduit le concept d’***exceptions***. Le moyen typique d’indiquer qu’une méthode ne peut pas effectuer correctement son travail consiste à lever une exception. Le type d’exception et le message associé décrivent l’erreur. Ici, la méthode `MakeDeposit` lève une exception si le montant du dépôt est négatif. La méthode `MakeWithdrawal` lève une exception si le montant du retrait est négatif ou si l’application du retrait génère un solde négatif :

[!code-csharp[DepositAndWithdrawal](../../../samples/csharp/classes-quickstart/BankAccount.cs#DepositAndWithdrawal "Make deposits and withdrawals")]

L’instruction [`throw`](../language-reference/keywords/throw.md) **lève** une exception. L’exécution de la méthode actuelle se termine et reprendra quand un bloc `catch` correspondant sera détecté. Vous ajouterez un bloc `catch` pour tester ce code un peu plus tard.

Le constructeur devrait obtenir une modification lui permettant d’ajouter une transaction initiale au lieu de mettre directement le solde à jour. Étant donné que vous avez déjà écrit la méthode `MakeDeposit`, appelez-la à partir de votre constructeur. Le constructeur terminé doit être semblable à ce qui suit :

[!code-csharp[Constructor](../../../samples/csharp/classes-quickstart/BankAccount.cs#Constructor "The final version of the constructor")]

<xref:System.DateTime.Now?displayProperty=nameWithType> est une propriété qui retourne la date et l'heure actuelles. Effectuez un essai en ajoutant des dépôts et des retraits dans votre méthode `Main` :

```csharp
account.MakeWithdrawal(500, DateTime.Now, "Rent payment");
Console.WriteLine(account.Balance);
account.MakeDeposit(100, DateTime.Now, "friend paid me back");
Console.WriteLine(account.Balance);
```

Vérifiez ensuite que vous interceptez bien les conditions d’erreur en essayant de créer un compte avec un solde négatif :

```csharp
// Test that the initial balances must be positive:
try
{
    var invalidAccount = new BankAccount("invalid", -55);
}
catch (ArgumentOutOfRangeException e)
{
    Console.WriteLine("Exception caught creating account with negative balance");
    Console.WriteLine(e.ToString());
}
```

Vous utilisez les [instructions `try` et `catch`](../language-reference/keywords/try-catch.md) pour marquer un bloc de code pouvant lever des exceptions et intercepter les erreurs que vous attendez. Vous pouvez utiliser la même technique pour tester le code qui lève une exception de solde négatif :

```csharp
// Test for a negative balance
try
{
    account.MakeWithdrawal(750, DateTime.Now, "Attempt to overdraw");
}
catch (InvalidOperationException e)
{
    Console.WriteLine("Exception caught trying to overdraw");
    Console.WriteLine(e.ToString());
}
```

Enregistrez le fichier et tapez `dotnet run` pour effectuer un essai.

## <a name="challenge---log-all-transactions"></a>Test : consigner toutes les transactions

Pour terminer ce guide de démarrage rapide, vous pouvez écrire la méthode `GetAccountHistory` qui crée une `string` pour l’historique des transactions. Ajoutez cette méthode au type `BankAccount` :

[!code-csharp[History](../../../samples/csharp/classes-quickstart/BankAccount.cs#History "Display transaction history")]

Cette méthode utilise la classe <xref:System.Text.StringBuilder> pour mettre en forme une chaîne contenant une ligne par transaction. Vous avez vu le code de mise en forme de chaîne précédemment dans ces guides de démarrage rapide. Vous pouvez observer le nouveau caractère `\t`. Celui-ci insère une tabulation pour mettre en forme la sortie.

Ajoutez cette ligne pour effectuer un essai dans **Program.cs** :

```csharp
Console.WriteLine(account.GetAccountHistory());
```

Tapez `dotnet run` pour afficher les résultats.

## <a name="next-steps"></a>Étapes suivantes

Si vous êtes bloqué, vous pouvez afficher la source de ce guide de démarrage rapide [dans notre dépôt GitHub](https://github.com/dotnet/docs/tree/master/samples/csharp/classes-quickstart/).

Félicitations, vous avez terminé tous nos guides de démarrage rapide. Si vous souhaitez en savoir plus, explorez nos [didacticiels](../tutorials/index.md).
