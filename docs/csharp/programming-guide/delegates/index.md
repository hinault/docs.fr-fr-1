---
title: "Délégués (Guide de programmation C#)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
helpviewer_keywords:
- C# language, delegates
- delegates [C#]
ms.assetid: 97de039b-c76b-4b9c-a27d-8c1e1c8d93da
caps.latest.revision: "30"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: c78b06b23805082251db8bbd7b377ffd36c6ef03
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="delegates-c-programming-guide"></a>Délégués (Guide de programmation C#)
Un [délégué](../../../csharp/language-reference/keywords/delegate.md) est un type qui représente des références aux méthodes avec une liste de paramètres et un type de retour particuliers. Lorsque vous instanciez un délégué, vous pouvez associer son instance à toute méthode ayant une signature et un type de retour compatibles. Vous pouvez appeler la méthode par le biais l'instance de délégué.  
  
 Les délégués sont utilisés pour passer des méthodes comme arguments à d'autres méthodes. Les gestionnaires d'événements sont tout simplement des méthodes appelées par le biais de délégués. Vous créez une méthode personnalisée, et une classe telle qu'un contrôle Windows peut appeler votre méthode lorsqu'un certain événement se produit. L'exemple suivant illustre une déclaration de délégué :  
  
 [!code-csharp[csProgGuideDelegates#20](../../../csharp/programming-guide/delegates/codesnippet/CSharp/index_1.cs)]  
  
 Toute méthode de n'importe quelle classe ou structure accessible qui correspond au type de délégué, peut être assignée au délégué. La méthode peut être une méthode d'instance ou statique. Cela permet de modifier par programme les appels de méthode, mais également d'insérer du nouveau code dans les classes existantes.  
  
> [!NOTE]
>  Dans le contexte de surcharge de méthodes, la signature d'une méthode n'inclut pas la valeur de retour. Mais dans le contexte des délégués, la signature inclut la valeur de retour. En d'autres termes, une méthode doit avoir le même type de retour que le délégué.  
  
 Cette capacité à faire référence à une méthode en tant que paramètre fait des délégués les instruments idéaux pour définir des méthodes de rappel. Par exemple, une référence à une méthode qui compare deux objets peut être passée comme argument à un algorithme de tri. Étant donné que le code de comparaison est dans une procédure distincte, l'algorithme de tri peut être écrit de façon plus générale.  
  
## <a name="delegates-overview"></a>Vue d'ensemble des délégués  
 Les délégués ont les propriétés suivantes :  
  
-   Les délégués sont semblables aux pointeurs de fonction C++, mais ils sont de type sécurisé.  
  
-   Les délégués permettent aux méthodes d'être transmises comme des paramètres.  
  
-   Les délégués peuvent être utilisés pour définir des méthodes de rappel.  
  
-   Les délégués peuvent être chaînés ; par exemple, plusieurs méthodes peuvent être appelées sur un seul événement.  
  
-   Les méthodes ne doivent pas correspondre exactement au type du délégué. Pour plus d’informations, consultez [Utilisation de la variance dans les délégués](../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md).  
  
-   C# version 2.0 a introduit le concept de [Méthodes anonymes](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md), qui permet de passer des blocs de code en tant que paramètres à la place d'une méthode définie séparément. C# 3.0 a introduit les expressions lambda comme un moyen plus concis d’écrire des blocs de code inline. Les méthodes anonymes et les expressions lambda (dans certains contextes) sont toutes deux compilées en types de délégué. Ces fonctionnalités sont désormais conjointement désignées par l’expression « fonctions anonymes ». Pour plus d’informations sur les expressions lambda, consultez [Fonctions anonymes](../../../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md).  
  
## <a name="in-this-section"></a>Dans cette section  
  
-   [Utilisation de délégués](../../../csharp/programming-guide/delegates/using-delegates.md)  
  
-   [Quand utiliser des délégués à la place d’interfaces (Guide de programmation C#)](http://msdn.microsoft.com/library/2e759bdf-7ca4-4005-8597-af92edf6d8f0)  
  
-   [Délégués avec méthodes nommées et méthodes anonymes](../../../csharp/programming-guide/delegates/delegates-with-named-vs-anonymous-methods.md)  
  
-   [Méthodes anonymes](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)  
  
-   [Utilisation de la variance dans les délégués](../../../csharp/programming-guide/concepts/covariance-contravariance/using-variance-in-delegates.md)  
  
-   [Guide pratique pour combiner des délégués (délégués multicast)](../../../csharp/programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md)  
  
-   [Comment : déclarer, instancier et utiliser un délégué](../../../csharp/programming-guide/delegates/how-to-declare-instantiate-and-use-a-delegate.md)  
  
## <a name="c-language-specification"></a>Spécification du langage C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="featured-book-chapters"></a>Chapitres proposés  
 [Delegates, Events, and Lambda Expressions](http://go.microsoft.com/fwlink/?LinkId=195395) (Délégués, événements et expressions lambda) dans [C# 3.0 Cookbook, Third Edition: More than 250 solutions for C# 3.0 programmers](http://go.microsoft.com/fwlink/?LinkId=195369)  
  
 [Delegates and Events](http://go.microsoft.com/fwlink/?LinkId=195418) dans [Learning C# 3.0: Master the fundamentals of C# 3.0](http://go.microsoft.com/fwlink/?LinkId=195412)  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Delegate>  
 [Guide de programmation C#](../../../csharp/programming-guide/index.md)  
 [Événements](../../../csharp/programming-guide/events/index.md)
