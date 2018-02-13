---
title: "Integer, type de données (Visual Basic)"
ms.date: 01/31/2018
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Integer
- Integer
helpviewer_keywords:
- numbers [Visual Basic], whole
- enumerated values [Visual Basic]
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- literal type characters [Visual Basic], I
- integers [Visual Basic], types
- data types [Visual Basic], integral
- '% identifier type character'
- data types [Visual Basic], assigning
- identifier type characters [Visual Basic], %
- I literal type character [Visual Basic]
- Integer data type
ms.assetid: a8f233b4-4be3-455c-861b-05af2fbb6c60
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ba700cac58c96b3d6d2f5ed3c74fdd7e95761352
ms.sourcegitcommit: d2da0142247ef42a219a5d2907f153e62dc6ea0d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="integer-data-type-visual-basic"></a>Type de données Integer (Visual Basic)
Contient des entiers 32 bits (4 octets) signés dont la valeur est comprise entre -2 147 483 648 et 2 147 483 647.  
  
## <a name="remarks"></a>Notes
 Le type de données `Integer` offre des performances optimales sur un processeur 32 bits. Les autres types intégraux sont plus lents à charger et à stocker en provenance et à destination de la mémoire.  
  
 La valeur par défaut de `Integer` est 0.  

## <a name="literal-assignments"></a>Attributions de littéral

Vous pouvez déclarer et initialiser une `Integer` variable en lui assignant un décimal littéral, un littéral hexadécimal, un littéral octal, ou (à partir de Visual Basic 2017) un littéral binaire. Si le littéral entier est en dehors de la plage de `Integer` (autrement dit, s’il est inférieur à <xref:System.Int32.MinValue?displayProperty=nameWithType> ou supérieur à <xref:System.Int32.MaxValue?displayProperty=nameWithType>, une erreur de compilation se produit.

Dans l’exemple suivant, les entiers égaux à 16 342 représentés comme des littéraux décimaux, hexadécimaux et binaires sont assignés aux valeurs `Integer`.

[!code-vb[integer](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#Int)]  

> [!NOTE]
> Vous utilisez le préfixe `&h` ou `&H` pour désigner un littéral hexadécimal, le préfixe `&b` ou `&B` pour désigner un littéral binaire et le préfixe `&o` ou `&O` pour désigner un littéral octal. Les littéraux décimaux n’ont pas de préfixe.

À partir de Visual Basic 2017, vous pouvez également utiliser le caractère de soulignement, `_`, comme un séparateur de chiffres pour améliorer la lisibilité, comme l’exemple suivant montre le.

[!code-vb[integer](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#IntS)]  

À partir de Visual Basic 15.5, vous pouvez également utiliser le caractère de soulignement (`_`) comme séparateur de début entre le préfixe et les chiffres hexadécimaux, binaires ou octales. Exemple :

```vb
Dim number As Integer = &H_C305_F860
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

Littéraux numériques peuvent également inclure le `I` [caractère de type](../../programming-guide\language-features\data-types/type-characters.md) pour désigner le `Integer` type de données, comme le montre l’exemple suivant.

```vb
Dim number = &H_035826I
```

## <a name="programming-tips"></a>Conseils de programmation

-   **Considérations sur l’interopérabilité.** Si vous utilisez des composants non écrits pour le .NET Framework, tels que des objets Automation ou COM, n’oubliez pas que `Integer` a une largeur de données différente (16 bits) dans d’autres environnements. Si vous passez un argument de 16 bits à un tel composant, déclarez-le en tant que type de données `Short` et non `Integer` dans votre nouveau code Visual Basic.  
  
-   **Étendues.** Le type de données `Integer` s'étend à `Long`, `Decimal`, `Single` ou `Double`. Cela signifie que vous pouvez convertir `Integer` en l'un de ces types sans rencontrer d'erreur <xref:System.OverflowException?displayProperty=nameWithType>.  
  
-   **Caractères de type.** L'ajout du caractère de type littéral `I` à un littéral force ce dernier en type de données `Integer`. L'ajout du caractère de type identificateur `%` à un identificateur force ce dernier en type `Integer`.  
  
-   **Type .NET Framework.** Le type correspondant dans le .NET Framework est la structure <xref:System.Int32?displayProperty=nameWithType>.  
  
## <a name="range"></a>Plage

Si vous essayez d'assigner à une variable de type intégral un nombre situé hors de la plage de ce type, une erreur se produit. Si vous essayez de lui assigner une fraction, le nombre est arrondi à la valeur entière supérieure ou inférieure la plus proche. Si le nombre est proche à l'identique de deux valeurs entières, la valeur est arrondie à l'entier pair le plus proche. Ce comportement réduit les erreurs d'arrondi qui résultent de l'arrondissement cohérent d'une valeur du milieu dans un seul sens. Le code suivant présente des exemples d'arrondi.  

```vb  
' The valid range of an Integer variable is -2147483648 through +2147483647.  
Dim k As Integer  
' The following statement causes an error because the value is too large.  
k = 2147483648  
' The following statement sets k to 6.  
k = 5.9  
' The following statement sets k to 4  
k = 4.5  
' The following statement sets k to 6  
' Note, Visual Basic uses banker’s rounding (toward nearest even number)  
k = 5.5  
```

## <a name="see-also"></a>Voir aussi

<xref:System.Int32?displayProperty=nameWithType>   
 [Types de données](../../../visual-basic/language-reference/data-types/data-type-summary.md)  
 [Long (type de données)](../../../visual-basic/language-reference/data-types/long-data-type.md)  
 [Short (type de données)](../../../visual-basic/language-reference/data-types/short-data-type.md)  
 [Fonctions de conversion de types](../../../visual-basic/language-reference/functions/type-conversion-functions.md)  
 [Liste des conversions](../../../visual-basic/language-reference/keywords/conversion-summary.md)  
 [Utilisation efficace des types de données](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
