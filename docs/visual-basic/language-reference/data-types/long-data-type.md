---
title: "Long, type de données (Visual Basic)"
ms.date: 01/31/2018
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Long
helpviewer_keywords:
- identifier type characters [Visual Basic], &
- numbers [Visual Basic], whole
- whole numbers
- integral data types [Visual Basic]
- '& identifier type character'
- integer numbers
- literal type characters [Visual Basic], L
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- L literal type character [Visual Basic]
- integers [Visual Basic], types
- Long keyword [Visual Basic]
- data types [Visual Basic], integral
- data types [Visual Basic], assigning
- Long data type
ms.assetid: b4770c34-1804-4f8c-b512-c10b0893e516
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 51cf03afc6b2e77ccca74fc26365fc50110e1f71
ms.sourcegitcommit: d2da0142247ef42a219a5d2907f153e62dc6ea0d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="long-data-type-visual-basic"></a>Type de données long (Visual Basic)

Contient des entiers (8 octets) de 64 bits dont la valeur de -9,223,372,036,854,775,808 à 9,223,372,036,854,775,807 signés (9.2... E + 18).  
  
## <a name="remarks"></a>Notes

 Utilisez le `Long` type de données pour contenir des nombres entiers qui sont trop volumineuses pour tenir la `Integer` type de données.  
  
 La valeur par défaut de `Long` est 0.

## <a name="literal-assignments"></a>Attributions de littéral 

Vous pouvez déclarer et initialiser une `Long` variable en lui assignant un décimal littéral, un littéral hexadécimal, un littéral octal, ou (à partir de Visual Basic 2017) un littéral binaire. Si le littéral entier est en dehors de la plage de `Long` (autrement dit, s’il est inférieur à <xref:System.Int64.MinValue?displayProperty=nameWithType> ou supérieur à <xref:System.Int64.MaxValue?displayProperty=nameWithType>, une erreur de compilation se produit.

Dans l’exemple suivant, les entiers égaux à 4 294 967 296 représentés comme des littéraux décimaux, hexadécimaux et binaires sont assignés aux valeurs `Long`.
  
[!code-vb[long](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#Long)]  

> [!NOTE]
> Vous utilisez le préfixe `&h` ou `&H` pour désigner un littéral hexadécimal, le préfixe `&b` ou `&B` pour désigner un littéral binaire et le préfixe `&o` ou `&O` pour désigner un littéral octal. Les littéraux décimaux n’ont pas de préfixe.

À partir de Visual Basic 2017, vous pouvez également utiliser le caractère de soulignement, `_`, comme un séparateur de chiffres pour améliorer la lisibilité, comme l’exemple suivant montre le.

[!code-vb[long](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#LongS)]

À partir de Visual Basic 15.5, vous pouvez également utiliser le caractère de soulignement (`_`) comme séparateur de début entre le préfixe et les chiffres hexadécimaux, binaires ou octales. Exemple :

```vb
Dim number As Long = &H_0FAC_0326_1489_D68C
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

Littéraux numériques peuvent également inclure le `L` [caractère de type](../../programming-guide\language-features\data-types/type-characters.md) pour désigner le `Long` type de données, comme le montre l’exemple suivant.

```vb
Dim number = &H_0FAC_0326_1489_D68CL
```

## <a name="programming-tips"></a>Conseils de programmation

-   **Considérations sur l’interopérabilité.** Si vous utilisez des composants non écrits pour le .NET Framework, par exemple des objets Automation ou COM, n’oubliez pas que `Long` a une largeur de données différente (32 bits) dans d’autres environnements. Si vous passez un argument de 32 bits à un tel composant, déclarez-le en tant que `Integer` au lieu de `Long` dans votre nouveau code Visual Basic.  
  
-   **Étendues.** Le `Long` type de données s’étend à `Decimal`, `Single`, ou `Double`. Cela signifie que vous pouvez convertir `Long` en l'un de ces types sans rencontrer d'erreur <xref:System.OverflowException?displayProperty=nameWithType>.  
  
-   **Caractères de type.** L'ajout du caractère de type littéral `L` à un littéral force ce dernier en type de données `Long`. L'ajout du caractère de type identificateur `&` à un identificateur force ce dernier en type `Long`.  
  
-   **Type .NET Framework.** Le type correspondant dans le .NET Framework est la structure <xref:System.Int64?displayProperty=nameWithType>.  

## <a name="see-also"></a>Voir aussi

<xref:System.Int64>[Des Types de données](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
[Type de données Integer](../../../visual-basic/language-reference/data-types/integer-data-type.md)   
[Type de données de type short](../../../visual-basic/language-reference/data-types/short-data-type.md)   
[Fonctions de Conversion de type](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
[Résumé de la conversion](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
[Utilisation efficace des types de données](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
