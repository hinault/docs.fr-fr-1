---
title: "enum (référence C#)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- enum
- enum_CSharpKeyword
helpviewer_keywords:
- enum keyword [C#]
ms.assetid: bbeb9a0f-e9b3-41ab-b0a6-c41b1a08974c
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 36d33387dda68270e0490eaa6c792f95d058651e
ms.sourcegitcommit: f28752eab00d2bd97e971542c0f49ce63cfbc239
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2018
---
# <a name="enum-c-reference"></a>enum (référence C#)
Le mot clé `enum` est utilisé pour déclarer une énumération. Il s’agit d’un type distinct qui se compose d’un ensemble de constantes nommées, appelé liste d’énumérateurs.  
  
 Il est généralement préférable de définir une énumération directement dans un espace de noms pour que toutes les classes de l’espace de noms puissent y accéder avec la même facilité. Toutefois, une énumération peut également être imbriquée dans une classe ou un struct.  
  
 Par défaut, le premier énumérateur a la valeur 0 et chaque énumérateur successif est augmenté de 1. Par exemple, dans l’énumération suivante, `Sat` est `0`, `Sun` est `1`, `Mon` est `2`, et ainsi de suite.  
  
```  
enum Day {Sat, Sun, Mon, Tue, Wed, Thu, Fri};  
```  
  
 Les énumérateurs peuvent utiliser des initialiseurs pour remplacer les valeurs par défaut, comme illustré dans l’exemple suivant.  
  
```  
enum Day {Sat=1, Sun, Mon, Tue, Wed, Thu, Fri};  
```  
  
 Dans cette énumération, le début de la séquence des éléments est forcé à `1` au lieu de `0`. Il est cependant recommandé d’inclure une constante qui a la valeur 0. Pour plus d’informations, consultez [Types énumération](../../../csharp/programming-guide/enumeration-types.md).  
  
 Chaque type énumération a un type sous-jacent qui peut être tout type intégral sauf [char](../../../csharp/language-reference/keywords/char.md). Le type sous-jacent par défaut des éléments de l’énumération est [int](../../../csharp/language-reference/keywords/int.md). Pour déclarer une énumération d’un autre type intégral, comme [byte](../../../csharp/language-reference/keywords/byte.md), utilisez un signe deux-points après l’identificateur, suivi du type, comme illustré dans l’exemple suivant.  
  
```  
enum Day : byte {Sat=1, Sun, Mon, Tue, Wed, Thu, Fri};  
```  
  
 Les types approuvés d’une énumération sont [byte](../../../csharp/language-reference/keywords/byte.md), [sbyte](../../../csharp/language-reference/keywords/sbyte.md), [short](../../../csharp/language-reference/keywords/short.md), [ushort](../../../csharp/language-reference/keywords/ushort.md), [int](../../../csharp/language-reference/keywords/int.md), [uint](../../../csharp/language-reference/keywords/uint.md), [long](../../../csharp/language-reference/keywords/long.md) ou [ulong](../../../csharp/language-reference/keywords/ulong.md).  
  
 Une variable de type `Day` peut être affectée de n’importe quelle valeur dans la plage du type sous-jacent ; les valeurs ne sont pas limitées aux constantes nommées.  
  
 La valeur par défaut de `enum E` est la valeur produite par l’expression `(E)0`.  
  
> [!NOTE]
>  Le nom d’un énumérateur ne peut pas contenir d’espaces.  
  
 Le type sous-jacent spécifie la quantité de stockage allouée pour chaque énumérateur. Cependant, un cast explicite est nécessaire pour convertir du type `enum` en un type intégral. Par exemple, l’instruction suivante affecte l’énumérateur `Sun` à une variable du type [int](../../../csharp/language-reference/keywords/int.md) en utilisant un cast pour convertir de `enum` en `int`.  
  
```  
int x = (int)Day.Sun;  
```  
  
 Quand vous appliquez <xref:System.FlagsAttribute?displayProperty=nameWithType> à une énumération qui contient des éléments qui peuvent être combinés avec une opération `OR` au niveau du bit, l’attribut affecte le comportement d’ `enum` quand elle est utilisée avec certains outils. Vous pouvez remarquer ces modifications quand vous utilisez des outils comme les méthodes de la classe <xref:System.Console> et l’évaluateur d’expression. (Voir le troisième exemple.)  
  
## <a name="robust-programming"></a>Programmation fiable  
 Tout comme avec n’importe quelle constante, toutes les références aux valeurs individuelles d’une énumération sont converties en littéraux numériques au moment de la compilation. Cette opération peut créer des problèmes potentiels de gestion de version, comme décrit dans [Constantes](../../../csharp/programming-guide/classes-and-structs/constants.md).  
  
 L’affectation de valeurs supplémentaires à de nouvelles versions d’énumérations ou la modification des valeurs des membres d’une énumération dans une nouvelle version peut entraîner des problèmes pour le code source dépendant. Les valeurs des énumérations sont souvent utilisées dans des instructions [switch](../../../csharp/language-reference/keywords/switch.md) . Si des éléments supplémentaires ont été ajoutées au type `enum` , la section par défaut de l’instruction switch peut être sélectionnée de façon inattendue.  
  
 Si d’autres développeurs utilisent votre code, vous devez fournir des instructions sur la manière dont leur code doit réagir si de nouveaux éléments sont ajoutés à des types `enum` .  
  
## <a name="example"></a>Exemple  
 Dans l’exemple suivant, une énumération, `Day`, est déclarée. Deux énumérateurs sont explicitement convertis en entiers et affectés à des variables entières.  
  
 [!code-csharp[csrefKeywordsTypes#10](../../../csharp/language-reference/keywords/codesnippet/CSharp/enum_1.cs)]  
  
## <a name="example"></a>Exemple  
 Dans l’exemple suivant, l’option de type de base est utilisée pour déclarer une `enum` dont les membres sont de type `long`. Notez que même si le type sous-jacent de l’énumération est `long`, les membres de l’énumération doivent toujours être explicitement convertis en type `long` en utilisant un cast.  
  
 [!code-csharp[csrefKeywordsTypes#11](../../../csharp/language-reference/keywords/codesnippet/CSharp/enum_2.cs)]  
  
## <a name="example"></a>Exemple  
 L’exemple de code suivant montre l’utilisation et l’effet de l’attribut <xref:System.FlagsAttribute?displayProperty=nameWithType> sur une déclaration `enum` .  
  
 [!code-csharp[csrefKeywordsTypes#12](../../../csharp/language-reference/keywords/codesnippet/CSharp/enum_3.cs)]  
  
## <a name="comments"></a>Commentaires  
 Si vous supprimez `Flags`, l’exemple affiche les valeurs suivantes :  
  
 `5`  
  
 `5`  
  
## <a name="c-language-specification"></a>Spécification du langage C#  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Voir aussi  
 [Référence C#](../../../csharp/language-reference/index.md)  
 [Types d’énumération](../../../csharp/programming-guide/enumeration-types.md)  
 [Mots clés C#](../../../csharp/language-reference/keywords/index.md)  
 [Tableau des types intégraux](../../../csharp/language-reference/keywords/integral-types-table.md)  
 [Tableau des types intégrés](../../../csharp/language-reference/keywords/built-in-types-table.md)  
 [Tableau des conversions numériques implicites](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)  
 [Tableau des conversions numériques explicites](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)  
 [Conventions de nommage des énumérations](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/names-of-classes-structs-and-interfaces#naming-enumerations)
