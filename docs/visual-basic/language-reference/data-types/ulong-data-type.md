---
title: "ULong, type de données (Visual Basic)"
ms.date: 01/31/2018
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.ulong
helpviewer_keywords:
- numbers [Visual Basic], whole
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- data types [Visual Basic], integral
- literal type characters [Visual Basic], UL
- ULong data type
- UL literal type characters [Visual Basic]
ms.assetid: 017e0702-774e-44ae-bedc-786b424ca84e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 606e0ef87b209bb2e75e28223f27d081713c1b7e
ms.sourcegitcommit: d2da0142247ef42a219a5d2907f153e62dc6ea0d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="ulong-data-type-visual-basic"></a>ULong, type de données (Visual Basic)

Contient des entiers 64 bits (8 octets) non signés dont la valeur comprise entre 0 et 18,446,744,073,709,551,615 (plus que 1,84 fois 10 ^ 19).  
  
## <a name="remarks"></a>Notes

Utilisez le `ULong` type de données pour contenir les données binaires trop grandes pour `UInteger`, ou le plus grand possible des valeurs entières non signées.  
  
La valeur par défaut de `ULong` est 0.

## <a name="literal-assignments"></a>Attributions de littéral

Vous pouvez déclarer et initialiser une `ULong` variable en lui assignant un décimal littéral, un littéral hexadécimal, un littéral octal, ou (à partir de Visual Basic 2017) un littéral binaire. Si le littéral entier est en dehors de la plage de `ULong` (autrement dit, s’il est inférieur à <xref:System.UInt64.MinValue?displayProperty=nameWithType> ou supérieur à <xref:System.UInt64.MaxValue?displayProperty=nameWithType>, une erreur de compilation se produit.

Dans l’exemple suivant, les entiers égaux à 7 934 076 125 représentés comme des littéraux décimaux, hexadécimaux et binaires sont assignés aux valeurs `ULong`.
  
[!code-vb[ULong](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#ULong)]

> [!NOTE] 
> Vous utilisez le préfixe `&h` ou `&H` pour désigner un littéral hexadécimal, le préfixe `&b` ou `&B` pour désigner un littéral binaire et le préfixe `&o` ou `&O` pour désigner un littéral octal. Les littéraux décimaux n’ont pas de préfixe.

À partir de Visual Basic 2017, vous pouvez également utiliser le caractère de soulignement, `_`, comme un séparateur de chiffres pour améliorer la lisibilité, comme l’exemple suivant montre le.

[!code-vb[ULong](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#LongS)]

À partir de Visual Basic 15.5, vous pouvez également utiliser le caractère de soulignement (`_`) comme séparateur de début entre le préfixe et les chiffres hexadécimaux, binaires ou octales. Exemple :

```vb
Dim number As ULong = &H_F9AC_0326_1489_D68C
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

Littéraux numériques peuvent également inclure le `UL` ou `ul` [caractère de type](../../programming-guide\language-features\data-types/type-characters.md) pour désigner le `ULong` type de données, comme le montre l’exemple suivant.

```vb
Dim number = &H_00_00_0A_96_2F_AC_14_D7ul
```

## <a name="programming-tips"></a>Conseils de programmation
  
-   **Nombres négatifs.** Étant donné que `ULong` est un type non signé, il ne peut pas représenter un nombre négatif. Si vous utilisez le moins unaire (`-`) opérateur sur une expression qui correspond au type `ULong`, Visual Basic convertit l’expression à `Decimal` première.  
  
-   **Conformité CLS.** Le `ULong` type de données n’est pas dans le cadre de la [Common Language Specification](http://www.ecma-international.org/publications/standards/Ecma-335.htm) (CLS), un code conforme CLS ne peut pas consommer un composant qui l’utilise.  
  
-   **Considérations sur l’interopérabilité.** Si vous utilisez des composants non écrits pour le .NET Framework, par exemple des objets Automation ou COM, gardez à l’esprit que les types tels que `ulong` peut avoir une largeur de données différente (32 bits) dans d’autres environnements. Si vous passez un argument de 32 bits à un tel composant, déclarez-le en tant que `UInteger` au lieu de `ULong` dans votre code managé de Visual Basic.  
  
     En outre, Automation ne prend pas en charge les entiers 64 bits sur Windows 95, Windows 98, Windows ME ou Windows 2000. Vous ne pouvez pas passer un Visual Basic `ULong` argument à un composant Automation sur ces plateformes.  
  
-   **Étendues.** Le `ULong` type de données s’étend à `Decimal`, `Single`, et `Double`. Cela signifie que vous pouvez convertir `ULong` à un de ces types sans rencontrer un <xref:System.OverflowException?displayProperty=nameWithType> erreur.  
  
-   **Caractères de type.** L’ajout de caractères de type littéral `UL` à un littéral force ce dernier à la `ULong` type de données. `ULong`n’a aucun caractère de type d’identificateur.
  
-   **Type .NET Framework.** Le type correspondant dans le .NET Framework est la structure <xref:System.UInt64?displayProperty=nameWithType>.  
  
## <a name="see-also"></a>Voir aussi

 <xref:System.UInt64>  
 [Types de données](../../../visual-basic/language-reference/data-types/data-type-summary.md)  
 [Fonctions de conversion de types](../../../visual-basic/language-reference/functions/type-conversion-functions.md)  
 [Liste des conversions](../../../visual-basic/language-reference/keywords/conversion-summary.md)  
 [Guide pratique : appeler une fonction Windows qui possède des types non signés](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)  
 [Utilisation efficace des types de données](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
