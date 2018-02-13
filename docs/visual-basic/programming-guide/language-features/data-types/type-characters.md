---
title: "Caractères de type (Visual Basic)"
ms.custom: 
ms.date: 01/31/2018
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- '&H prefix for hexadecimal values'
- hexadecimal literals [Visual Basic]
- F literal type character [Visual Basic]
- '& identifier type character'
- type characters [Visual Basic]
- octal literals [Visual Basic]
- literals [Visual Basic], hexadecimal
- '&O prefix for octal values'
- literals [Visual Basic], default types
- defaults, literal types
- C literal type character [Visual Basic]
- type characters [Visual Basic], literal
- $ identifier type character
- L literal type character [Visual Basic]
- UI literal type characters [Visual Basic]
- default literal types [Visual Basic]
- D literal type character [Visual Basic]
- literals [Visual Basic], octal
- S literal type character [Visual Basic]
- '! identifier type character'
- US literal type characters [Visual Basic]
- '% identifier type character'
- data types [Visual Basic], type characters
- characters [Visual Basic], identifier type
- type characters [Visual Basic], identifier
- '# identifier type character'
- identifier type characters [Visual Basic]
- literal type characters [Visual Basic]
- I literal type character [Visual Basic]
- R literal type character [Visual Basic]
- '@ identifier type character'
- UL literal type characters [Visual Basic]
- literal types [Visual Basic], default
ms.assetid: 6353cb9b-6ee4-4af6-a5a8-88ce39f90cc5
author: rpetrusha
ms.author: ronpet
ms.manager: wpickett
ms.openlocfilehash: bdb675b9605d03829c95897382daa6d03cf1b041
ms.sourcegitcommit: d2da0142247ef42a219a5d2907f153e62dc6ea0d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="type-characters-visual-basic"></a>Tapez les caractères (Visual Basic)

En plus de spécifier un type de données dans une instruction de déclaration, vous pouvez forcer le type de données de certains éléments de programmation avec un *caractère de type*. Le caractère de type doit suivre immédiatement l’élément, sans les caractères de n’importe quel type.

Le caractère de type n’est pas partie du nom de l’élément. Un élément défini avec un caractère de type peut être référencé sans le caractère de type.

## <a name="identifier-type-characters"></a>Caractères de type d’identificateur

Visual Basic fournit un jeu de *caractères de type identificateur* que vous pouvez utiliser dans une déclaration pour spécifier le type de données d’une variable ou constante. Le tableau suivant présente les caractères de type identificateur disponible avec des exemples d’utilisation.
  
|Caractère de type identificateur|Type de données|Exemple|  
|-------------------------------|---------------|-------------|  
|`%`|`Integer`|`Dim L%`|  
|`&`|`Long`|`Dim M&`|  
|`@`|`Decimal`|`Const W@ = 37.5`|  
|`!`|`Single`|`Dim Q!`|  
|`#`|`Double`|`Dim X#`|  
|`$`|`String`|`Dim V$ = "Secret"`|  
  
 Il n’existe aucun caractère de type identificateur pour le `Boolean`, `Byte`, `Char`, `Date`, `Object`, `SByte`, `Short`, `UInteger`, `ULong`, ou `UShort` des types de données, ou pour toute types de données composites tels que les tableaux ou les structures.

Dans certains cas, vous pouvez ajouter la `$` de caractères à une fonction Visual Basic, par exemple `Left$` au lieu de `Left`, afin d’obtenir une valeur retournée de type `String`.

Dans tous les cas, le caractère de type identificateur doit suivre immédiatement le nom d’identificateur.

## <a name="literal-type-characters"></a>Caractères de type littéral

A *littéral* est une représentation textuelle d’une valeur particulière d’un type de données.  

### <a name="default-literal-types"></a>Types de littéral par défaut

La forme d’un littéral, tel qu’il apparaît dans votre code normalement détermine son type de données. Le tableau suivant présente les types par défaut.  
  
|Sous forme textuelle de littéral|Type de données par défaut|Exemple|  
|-----------------------------|-----------------------|-------------|  
|Numérique, aucune partie fractionnaire|`Integer`|`2147483647`|  
|Numérique, aucune partie fractionnaire, trop grand pour`Integer`|`Long`|`2147483648`|  
|Numérique, partie fractionnaire|`Double`|`1.2`|  
|Placé entre guillemets doubles|`String`|`"A"`|  
|Encadrées par des signes dièse|`Date`|`#5/17/1993 9:32 AM#`|  

### <a name="forced-literal-types"></a>Types de littéral forcés

Visual Basic fournit un jeu de *caractères de type littéral*, que vous pouvez utiliser pour forcer un littéral à prendre un type de données autre que celui de sa forme indique. Pour cela, vous devez l’ajout du caractère à la fin du littéral. Le tableau suivant présente les caractères de type de littéral disponibles avec des exemples d’utilisation.
  
|Caractère de type littéral|Type de données|Exemple|  
|----------------------------|---------------|-------------|  
|`S`|`Short`|`I = 347S`|
|`I`|`Integer`|`J = 347I`|
|`L`|`Long`|`K = 347L`|
|`D`|`Decimal`|`X = 347D`|
|`F`|`Single`|`Y = 347F`|
|`R`|`Double`|`Z = 347R`|
|`US`|`UShort`|`L = 347US`|
|`UI`|`UInteger`|`M = 347UI`|
|`UL`|`ULong`|`N = 347UL`|
|`C`|`Char`|`Q = "."C`|

Il n’existe aucun caractère de type de littéral pour les `Boolean`, `Byte`, `Date`, `Object`, `SByte`, ou `String` des types de données, ni pour les types de données composites tels que les tableaux ou les structures.

Les littéraux peuvent également utiliser les caractères de type identificateur (`%`, `&`, `@`, `!`, `#`, `$`), comme des variables, des constantes et des expressions. Toutefois, les caractères de type de littéral (`S`, `I`, `L`, `D`, `F`, `R`, `C`) peut être utilisé uniquement avec des littéraux.

Dans tous les cas, le caractère de type de littéral doit immédiatement suivre la valeur littérale.

## <a name="hexadecimal-binary-and-octal-literals"></a>Littéraux hexadécimaux, binaire et octales

Le compilateur interprète normalement un littéral d’entier dans le système de nombre décimal (base 10). Vous pouvez également définir un littéral d’entier comme un nombre hexadécimal (base 16) avec le `&H` préfixe, sous la forme d’un nombre binaire (base 2) avec le `&B` préfixe et comme octal (base 8) chez le `&O` préfixe. Les chiffres qui suivent le préfixe doivent être adaptés dans le système. Le tableau suivant illustre ce comportement.  
  
|Nombre de base|Préfixe|Valeurs de chiffre valide|Exemple|
|-----------------|------------|------------------------|-------------|
|Hexadécimale (base 16)|`&H`|0-9 et A-F|`&HFFFF`|
|Binaire (base 2)|`0B`|0-1|`&B01111100`|
|Octale (base 8)|`&O`|0-7|`&O77`|

À partir de Visual Basic 2017, vous pouvez utiliser le caractère de soulignement (`_`) comme séparateur de groupes pour améliorer la lisibilité d’un littéral intégral. L’exemple suivant utilise le `_` caractère pour regrouper un littéral binaire en groupes de 8 bits :

```vb
Dim number As Integer = &B00100010_11000101_11001111_11001101
```

Vous pouvez suivre un littéral préfixé par un caractère de type de littéral. L’exemple suivant illustre ce point.

```vb
Dim counter As Short = &H8000S
Dim flags As UShort = &H8000US
```

Dans l’exemple précédent, `counter` a la valeur décimale-32 768 et `flags` a la valeur décimale + 32 768.

À partir de Visual Basic 15.5, vous pouvez également utiliser le caractère de soulignement (`_`) comme séparateur de début entre le préfixe et les chiffres hexadécimaux, binaires ou octales. Exemple :

```vb
Dim number As Integer = &H_C305_F860
```

[!INCLUDE [supporting-underscores](../../../../../includes/vb-separator-langversion.md)]

## <a name="see-also"></a>Voir aussi

 [Types de données](../../../../visual-basic/programming-guide/language-features/data-types/index.md)  
 [Types de données élémentaires](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)  
 [Types valeur et types référence](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)  
 [Conversions de type dans Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)  
 [Dépannage des types de données](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)  
 [Déclaration de variable](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)  
 [Types de données](../../../../visual-basic/language-reference/data-types/data-type-summary.md)
