---
title: Cast et conversions de types (Guide de programmation C#)
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
helpviewer_keywords:
- type conversion [C#]
- data type conversion [C#]
- numeric conversions [C#]
- conversions [C#], type
- casting [C#]
- converting types [C#]
ms.assetid: 568df58a-d292-4b55-93ba-601578722878
caps.latest.revision: "52"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 1361a7f115e2bae4b2d1f6271fa9020706581691
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="casting-and-type-conversions-c-programming-guide"></a>Cast et conversions de types (Guide de programmation C#)
C# est typé statiquement au moment de la compilation. Ainsi, quand une variable est déclarée, elle ne peut plus être redéclarée ou utilisée pour stocker des valeurs d’un autre type, sauf si ce type peut être converti au type de la variable. Par exemple, il est impossible de convertir un entier en chaîne arbitraire. Après avoir déclaré `i` comme entier, vous ne pouvez donc pas lui assigner la chaîne « Hello » comme le montre le code suivant.  
  
```csharp  
int i;  
i = "Hello"; // Error: "Cannot implicitly convert type 'string' to 'int'"  
```  
  
 Cependant, vous pouvez être amené à copier une valeur dans un paramètre de variable ou de méthode d’un autre type. C’est notamment le cas si vous avez une variable de type entier que vous devez passer à une méthode dont le paramètre est de type `double`. Il peut également arriver que vous deviez assigner une variable de classe à une variable de type interface. Les opérations de ce genre sont appelées « *conversions de types* ». En C#, vous pouvez effectuer les conversions suivantes :  
  
-   **Conversions implicites** : aucune syntaxe spéciale n’est requise, car la conversion est de type sécurisé et les données ne sont pas perdues. Citons par exemple les conversions de types intégraux en d’autres plus importants, et les conversions de classes dérivées en classes de base.  
  
-   **Conversions explicites (casts)** : les conversions explicites nécessitent un opérateur de cast. Un cast est exigé quand les informations peuvent être perdues durant la conversion, ou quand la conversion peut échouer pour d’autres raisons.  Exemples classiques : conversion numérique en type qui a moins de précision ou une plus petite plage, et conversion d’une instance de classe de base en classe dérivée.  
  
-   **Conversions définies par l’utilisateur** : les conversions définies par l’utilisateur sont effectuées par des méthodes spéciales que vous pouvez définir pour permettre des conversions explicites ou implicites entre des types personnalisés qui n’ont pas de relation classe de base/classe dérivée. Pour plus d’informations, consultez [Conversion, opérateurs](../../../csharp/programming-guide/statements-expressions-operators/conversion-operators.md).  
  
-   **Conversions avec les classes d’assistance** : pour effectuer une conversion entre des types non compatibles, tels que des entiers et des objets <xref:System.DateTime?displayProperty=nameWithType> ou des chaînes hexadécimales et des tableaux d’octets, vous pouvez utiliser la classe <xref:System.BitConverter?displayProperty=nameWithType>, la classe <xref:System.Convert?displayProperty=nameWithType> et les méthodes `Parse` des types numériques intégrés, comme <xref:System.Int32.Parse%2A?displayProperty=nameWithType>. Pour plus d’informations, consultez [Guide pratique pour convertir un tableau d’octets en int](../../../csharp/programming-guide/types/how-to-convert-a-byte-array-to-an-int.md), [Guide pratique pour convertir une chaîne en nombre](../../../csharp/programming-guide/types/how-to-convert-a-string-to-a-number.md) et [Guide pratique pour effectuer une conversion entre des chaînes hexadécimales et des types numériques](../../../csharp/programming-guide/types/how-to-convert-between-hexadecimal-strings-and-numeric-types.md).  
  
## <a name="implicit-conversions"></a>Conversions implicites  
 Pour les types numériques intégrés, une conversion implicite peut être effectuée quand la valeur à stocker peut tenir dans la variable sans être tronquée ni arrondie. Par exemple, une variable de type [long](../../../csharp/language-reference/keywords/long.md) (entier sur 8 octets) peut stocker n’importe quelle valeur stockée par un [int](../../../csharp/language-reference/keywords/int.md) (4 octets sur un ordinateur 32 bits). Dans l’exemple suivant, le compilateur convertit implicitement la valeur à droite en type `long` avant de l’assigner à `bigNum`.  
  
 [!code-csharp[csProgGuideTypes#34](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/casting-and-type-conversions_1.cs)]  
  
 Pour obtenir la liste complète de toutes les conversions numériques implicites, consultez [Tableau des conversions numériques implicites](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md).  
  
 Pour les types référence, il existe toujours une conversion implicite entre une classe et l’une de ses interfaces ou classes de base directes ou indirectes. Aucune syntaxe spéciale n’est nécessaire, car une classe dérivée contient toujours tous les membres d’une classe de base.  
  
```  
Derived d = new Derived();  
Base b = d; // Always OK.  
```  
  
## <a name="explicit-conversions"></a>Conversions explicites  
 Toutefois, si une conversion ne peut pas être réalisée sans risque de perte d’informations, le compilateur exige une conversion explicite, aussi appelée *cast*. Un cast est une façon d’informer explicitement le compilateur que vous prévoyez de faire la conversion et que vous savez qu’une perte de données peut se produire. Pour effectuer un cast, spécifiez le type voulu entre parenthèses devant la valeur ou la variable à convertir. Le programme suivant effectue un cast d’un [double](../../../csharp/language-reference/keywords/double.md) en [int](../../../csharp/language-reference/keywords/int.md). Le programme ne se compile pas sans le cast.  
  
 [!code-csharp[csProgGuideTypes#2](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/casting-and-type-conversions_2.cs)]  
  
 Pour obtenir la liste des conversions numériques explicites autorisées, consultez [Tableau des conversions numériques explicites](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md).  
  
 Pour les types référence, un cast explicite est exigé si vous devez effectuer une conversion d’un type de base en type dérivé :  
  
```csharp  
// Create a new derived type.  
Giraffe g = new Giraffe();  
  
// Implicit conversion to base type is safe.  
Animal a = g;  
  
// Explicit conversion is required to cast back  
// to derived type. Note: This will compile but will  
// throw an exception at run time if the right-side  
// object is not in fact a Giraffe.  
Giraffe g2 = (Giraffe) a;  
```  
  
 Une opération cast entre types référence ne change pas le type au moment de l’exécution de l’objet sous-jacent. Elle change seulement le type de la valeur utilisée comme référence à cet objet. Pour plus d’informations, consultez [Polymorphisme](../../../csharp/programming-guide/classes-and-structs/polymorphism.md).  
  
## <a name="type-conversion-exceptions-at-run-time"></a>Exceptions de conversion de type au moment de l’exécution  
 Dans certaines conversions de types référence, le compilateur ne peut pas déterminer si un cast sera valide. Il est possible qu’une opération cast dont la compilation fonctionne échoue au moment de l’exécution. Comme l’illustre l’exemple suivant, un cast de type qui échoue au moment de l’exécution provoque la levée d’une exception <xref:System.InvalidCastException>.  
  
 [!code-csharp[csProgGuideTypes#41](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/casting-and-type-conversions_3.cs)]  
  
 C# fournit les opérateurs [is](../../../csharp/language-reference/keywords/is.md) et [as](../../../csharp/language-reference/keywords/as.md) pour vous permettre de tester la compatibilité avant d’effectuer réellement un cast. Pour plus d’informations, consultez [Guide pratique pour effectuer sans risque un cast à l’aide des opérateurs as et is](../../../csharp/programming-guide/types/how-to-safely-cast-by-using-as-and-is-operators.md).  
  
## <a name="c-language-specification"></a>Spécification du langage C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  

## <a name="see-also"></a>Voir aussi  
 [Guide de programmation C#](../../../csharp/programming-guide/index.md)  
 [Types](../../../csharp/programming-guide/types/index.md)  
 [(), opérateur](../../../csharp/language-reference/operators/invocation-operator.md)  
 [explicit](../../../csharp/language-reference/keywords/explicit.md)  
 [implicit](../../../csharp/language-reference/keywords/implicit.md)  
 [Opérateurs de conversion](../../../csharp/programming-guide/statements-expressions-operators/conversion-operators.md)  
 [Conversion de type généralisée](http://msdn.microsoft.com/library/49253ae6-7657-4810-82ab-1176a6feeada)  
 [Conversion d’un type exporté](http://msdn.microsoft.com/library/1dfe55f4-07a2-4b61-aabf-a8cf65783a6b)  
 [Guide pratique pour convertir une chaîne en nombre](../../../csharp/programming-guide/types/how-to-convert-a-string-to-a-number.md)
