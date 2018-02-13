---
title: "Arborescences d’expressions (C#)"
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
ms.assetid: 7d0ac21a-6d90-4e2e-8903-528cb78615b7
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 5554b9e923b0cc1da4906cda1b7ca4e6aac75f11
ms.sourcegitcommit: 099aa20d9b6450d1b7452d782a55771a6ad8ff35
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/05/2018
---
# <a name="expression-trees-c"></a>Arborescences d’expressions (C#)
Les arborescences d'expressions représentent du code dans une structure de données arborescente, où chaque nœud est une expression, par exemple un appel de méthode ou une opération binaire comme `x < y`.  
  
 Vous pouvez compiler et exécuter du code représenté par des arborescences d'expressions. Ceci permet la modification dynamique du code exécutable, l'exécution de requêtes LINQ dans différentes bases de données et la création de requêtes dynamiques. Pour plus d’informations sur les arborescences d’expressions dans LINQ, consultez [Guide pratique pour utiliser des arborescences d’expression pour générer des requêtes dynamiques](../../../../csharp/programming-guide/concepts/expression-trees/how-to-use-expression-trees-to-build-dynamic-queries.md).  
  
 Les arborescences d’expressions sont également utilisées dans l’environnement d’exécution de langage dynamique (DLR, Dynamic Language Runtime) pour fournir une interopérabilité entre les langages dynamiques et .NET Framework, ainsi que pour permettre aux writers de compilateur d’émettre des arborescences d’expressions au lieu d’utiliser le langage intermédiaire MSIL (Microsoft Intermediate Language). Pour plus d’informations sur le DLR, consultez [Vue d’ensemble du Dynamic Language Runtime](../../../../../docs/framework/reflection-and-codedom/dynamic-language-runtime-overview.md).  
  
 Le compilateur C# ou Visual Basic peut créer pour vous une arborescence d'expressions basée sur une expression lambda anonyme. Vous pouvez aussi créer manuellement des arborescences d'expressions en utilisant l'espace de noms <xref:System.Linq.Expressions>.  
  
## <a name="creating-expression-trees-from-lambda-expressions"></a>Création d'arborescences d'expressions à partir d'expressions lambda  
 Quand une expression lambda est affectée à une variable de type <xref:System.Linq.Expressions.Expression%601>, le compilateur produit du code pour générer une arborescence d'expressions qui représente l'expression lambda.  
  
 Le compilateur C# peut générer des arborescences d’expressions seulement à partir d’expressions lambda (ou de lambdas sur une seule ligne). Ils ne peuvent pas analyser des lambdas d'instruction (ou lambdas multilignes). Pour plus d’informations sur les expressions lambda en C#, consultez [Expressions lambda](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md).  
  
 Les exemples de code suivants montrent comment le compilateur C# crée une arborescence d’expressions qui représente l’expression lambda `num => num < 5`.  
  
```csharp  
Expression<Func<int, bool>> lambda = num => num < 5;  
```  
  
## <a name="creating-expression-trees-by-using-the-api"></a>Création d’arborescences d’expressions à l’aide de l’API  
 Pour créer des arborescences d'expressions à l'aide de l'API, utilisez la classe <xref:System.Linq.Expressions.Expression>. Cette classe contient des méthodes de fabrique statiques qui créent des nœuds d'arborescence d'expressions de types spécifiques, par exemple <xref:System.Linq.Expressions.ParameterExpression>, qui représente une variable ou un paramètre, ou <xref:System.Linq.Expressions.MethodCallExpression>, qui représente un appel de méthode. <xref:System.Linq.Expressions.ParameterExpression>, <xref:System.Linq.Expressions.MethodCallExpression> et les autres types spécifiques à une expression sont également définis dans l'espace de noms <xref:System.Linq.Expressions>. Ces types dérivent du type abstrait <xref:System.Linq.Expressions.Expression>.  
  
 L’exemple de code suivant montre comment créer une arborescence d’expressions qui représente l’expression lambda `num => num < 5` à l’aide de l’API.  
  
```csharp  
// Add the following using directive to your code file:  
// using System.Linq.Expressions;  
  
// Manually build the expression tree for   
// the lambda expression num => num < 5.  
ParameterExpression numParam = Expression.Parameter(typeof(int), "num");  
ConstantExpression five = Expression.Constant(5, typeof(int));  
BinaryExpression numLessThanFive = Expression.LessThan(numParam, five);  
Expression<Func<int, bool>> lambda1 =  
    Expression.Lambda<Func<int, bool>>(  
        numLessThanFive,  
        new ParameterExpression[] { numParam });  
```  
  
 Dans le .NET Framework 4 ou ultérieur, l’API des arborescences d’expressions prend également en charge les affectations et les expressions de flux de contrôle, comme les boucles, les blocs conditionnels et les blocs `try-catch`. À l’aide de l’API, vous pouvez créer des arborescences d’expressions qui sont plus complexes que celles qui peuvent être créées à partir d’expressions lambda par le compilateur C#. L’exemple suivant montre comment créer une arborescence d’expressions qui calcule la factorielle d’un nombre.  
  
```csharp  
// Creating a parameter expression.  
ParameterExpression value = Expression.Parameter(typeof(int), "value");  
  
// Creating an expression to hold a local variable.   
ParameterExpression result = Expression.Parameter(typeof(int), "result");  
  
// Creating a label to jump to from a loop.  
LabelTarget label = Expression.Label(typeof(int));  
  
// Creating a method body.  
BlockExpression block = Expression.Block(  
    // Adding a local variable.  
    new[] { result },  
    // Assigning a constant to a local variable: result = 1  
    Expression.Assign(result, Expression.Constant(1)),  
    // Adding a loop.  
        Expression.Loop(  
    // Adding a conditional block into the loop.  
           Expression.IfThenElse(  
    // Condition: value > 1  
               Expression.GreaterThan(value, Expression.Constant(1)),  
    // If true: result *= value --  
               Expression.MultiplyAssign(result,  
                   Expression.PostDecrementAssign(value)),  
    // If false, exit the loop and go to the label.  
               Expression.Break(label, result)  
           ),  
    // Label to jump to.  
       label  
    )  
);  
  
// Compile and execute an expression tree.  
int factorial = Expression.Lambda<Func<int, int>>(block, value).Compile()(5);  
  
Console.WriteLine(factorial);  
// Prints 120.  
```

Pour plus d’informations, consultez [Génération de méthodes dynamiques avec des arborescences d’expressions dans Visual Studio 2010](https://blogs.msdn.microsoft.com/csharpfaq/2009/09/14/generating-dynamic-methods-with-expression-trees-in-visual-studio-2010/) (ou version ultérieure).
  
## <a name="parsing-expression-trees"></a>Analyse des arborescences d’expressions  
 L’exemple de code suivant montre comment l’arborescence d’expressions qui représente l’expression lambda `num => num < 5` peut être décomposée selon ses différentes parties.  
  
```csharp  
// Add the following using directive to your code file:  
// using System.Linq.Expressions;  
  
// Create an expression tree.  
Expression<Func<int, bool>> exprTree = num => num < 5;  
  
// Decompose the expression tree.  
ParameterExpression param = (ParameterExpression)exprTree.Parameters[0];  
BinaryExpression operation = (BinaryExpression)exprTree.Body;  
ParameterExpression left = (ParameterExpression)operation.Left;  
ConstantExpression right = (ConstantExpression)operation.Right;  
  
Console.WriteLine("Decomposed expression: {0} => {1} {2} {3}",  
                  param.Name, left.Name, operation.NodeType, right.Value);  
  
// This code produces the following output:  
  
// Decomposed expression: num => num LessThan 5  
```  
  
## <a name="immutability-of-expression-trees"></a>Immuabilité des arborescences d’expressions  
 Les arborescences d'expressions doivent être immuables. Cela signifie que si vous voulez modifier une arborescence d'expressions, vous devez construire une nouvelle arborescence d'expressions en copiant l'arborescence existante et en y remplaçant les nœuds. Vous pouvez utiliser un visiteur d’arborescence d’expressions pour parcourir l’arborescence d’expressions existante. Pour plus d’informations, consultez [Guide pratique pour modifier des arborescences d’expressions (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-modify-expression-trees.md).  
  
## <a name="compiling-expression-trees"></a>Compilation des arborescences d’expressions  
 Le type <xref:System.Linq.Expressions.Expression%601> fournit la méthode <xref:System.Linq.Expressions.Expression%601.Compile%2A> qui compile le code représenté par une arborescence d'expressions en un délégué exécutable.  
  
 L’exemple de code suivant montre comment compiler une arborescence d’expressions et exécuter le code résultant.  
  
```csharp  
// Creating an expression tree.  
Expression<Func<int, bool>> expr = num => num < 5;  
  
// Compiling the expression tree into a delegate.  
Func<int, bool> result = expr.Compile();  
  
// Invoking the delegate and writing the result to the console.  
Console.WriteLine(result(4));  
  
// Prints True.  
  
// You can also use simplified syntax  
// to compile and run an expression tree.  
// The following line can replace two previous statements.  
Console.WriteLine(expr.Compile()(4));  
  
// Also prints True.  
```  
  
 Pour plus d’informations, consultez [Guide pratique pour exécuter des arborescences d’expressions (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md).  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Linq.Expressions>  
 [Guide pratique pour exécuter des arborescences d’expressions (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md)  
 [Guide pratique pour modifier des arborescences d’expressions (C#)](../../../../csharp/programming-guide/concepts/expression-trees/how-to-modify-expression-trees.md)  
 [Expressions lambda](../../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)  
 [Vue d’ensemble du Dynamic Language Runtime](../../../../../docs/framework/reflection-and-codedom/dynamic-language-runtime-overview.md)  
 [Concepts de programmation (C#)](../../../../csharp/programming-guide/concepts/index.md)
