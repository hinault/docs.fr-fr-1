---
title: "abstract (référence C#)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- abstract
- abstract_CSharpKeyword
helpviewer_keywords:
- abstract keyword [C#]
ms.assetid: b0797770-c1f3-4b4d-9441-b9122602a6bb
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 9c6dbb03a05ff1c86752983d130691ce23e341d7
ms.sourcegitcommit: be1fb5d9447ad459bef22b91a91c72e3e0b2d916
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/09/2018
---
# <a name="abstract-c-reference"></a>abstract (référence C#)
Le modificateur `abstract` indique que l’élément en cours de modification a une implémentation manquante ou incomplète. Le modificateur abstract peut être utilisé avec des classes, des méthodes, des propriétés, des indexeurs et des événements. Dans une déclaration de classe, utilisez le modificateur `abstract` pour indiquer qu’une classe doit uniquement servir de classe de base pour d’autres classes. Les membres définis comme abstraits, ou inclus dans une classe abstraite, doivent être implémentés par des classes dérivées de la classe abstraite.  
  
## <a name="example"></a>Exemple  
 Dans cet exemple, la classe `Square` doit fournir une implémentation de `Area`, car elle dérive de la classe `ShapesClass` :  
  
 [!code-csharp[csrefKeywordsModifiers#1](../../../csharp/language-reference/keywords/codesnippet/CSharp/abstract_1.cs)]  
  
 Les classes abstraites présentent les caractéristiques suivantes :  
  
-   Une classe abstraite ne peut pas être instanciée.  
  
-   Une classe abstraite peut contenir des méthodes et accesseurs abstraits.  
  
-   Il n’est pas possible de modifier une classe abstraite à l’aide du modificateur [sealed](../../../csharp/language-reference/keywords/sealed.md), car les deux modificateurs ont des significations opposées. Le modificateur `sealed` empêche qu’une classe soit héritée et le modificateur `abstract` exige qu’une classe soit héritée.  
  
-   Une classe non abstraite dérivée d’une classe abstraite doit inclure des implémentations réelles de tous les accesseurs et méthodes abstraits hérités.  
  
 Dans une déclaration de méthode ou de propriété, utilisez le modificateur `abstract` pour indiquer que la méthode ou la propriété ne contient pas d’implémentation.  
  
 Les méthodes abstraites présentent les caractéristiques suivantes :  
  
-   Une méthode abstraite est implicitement une méthode virtuelle.  
  
-   Les déclarations de méthodes abstraites sont autorisées uniquement dans les classes abstraites.  
  
-   Comme une déclaration de méthode abstraite ne fournit pas d’implémentation réelle, il n’y a pas de corps de méthode ; la déclaration de méthode se termine simplement par un point-virgule, et la signature n’est pas suivie d’accolades ({ }). Exemple :  
  
    ```csharp  
    public abstract void MyMethod();  
    ```  
  
     L’implémentation est fournie par une méthode de substitution ([override](../../../csharp/language-reference/keywords/override.md)), qui est membre d’une classe non abstraite.  
  
-   L’utilisation des modificateurs [static](../../../csharp/language-reference/keywords/static.md) ou [virtual](../../../csharp/language-reference/keywords/virtual.md) dans une déclaration de méthode abstraite serait une erreur.  
  
 Les propriétés abstraites se comportent comme les méthodes abstraites, à l’exception des différences dans la syntaxe de déclaration et d’appel.  
  
-   L’utilisation du modificateur `abstract` sur une propriété statique serait une erreur.  
  
-   Une propriété abstraite héritée peut être substituée dans une classe dérivée en incluant une déclaration de propriété qui utilise le modificateur [override](../../../csharp/language-reference/keywords/override.md).  
  
 Pour plus d’informations sur les classes abstraites, consultez [Classes abstract et sealed et membres de classe](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md).  
  
 Une classe abstraite doit fournir une implémentation pour tous les membres d’interface.  
  
 Une classe abstraite qui implémente une interface peut mapper les méthodes d’interface à des méthodes abstraites. Exemple :  
  
 [!code-csharp[csrefKeywordsModifiers#2](../../../csharp/language-reference/keywords/codesnippet/CSharp/abstract_2.cs)]  
  
## <a name="example"></a>Exemple  
 Dans cet exemple, la classe `DerivedClass` est dérivée de la classe abstraite `BaseClass`. La classe abstraite contient une méthode abstraite, `AbstractMethod`, et deux propriétés abstraites, `X` et `Y`.  
  
 [!code-csharp[csrefKeywordsModifiers#3](../../../csharp/language-reference/keywords/codesnippet/CSharp/abstract_3.cs)]  
  
 Dans l’exemple précédent, si vous tentez d’instancier la classe abstraite en utilisant une instruction comme celle-ci :  
  
```csharp
BaseClass bc = new BaseClass();   // Error  
```  
  
Vous obtenez une erreur indiquant que le compilateur ne peut pas créer une instance de la classe abstraite BaseClass.  
  
## <a name="c-language-specification"></a>Spécification du langage C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Voir aussi  
 [Référence C#](../../../csharp/language-reference/index.md)  
 [Guide de programmation C#](../../../csharp/programming-guide/index.md)  
 [Modificateurs](../../../csharp/language-reference/keywords/modifiers.md)  
 [virtual](../../../csharp/language-reference/keywords/virtual.md)  
 [override](../../../csharp/language-reference/keywords/override.md)  
 [Mots clés C#](../../../csharp/language-reference/keywords/index.md)
