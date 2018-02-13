---
title: "Byte, type de données (Visual Basic)"
ms.date: 01/31/2018
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Byte
helpviewer_keywords:
- Byte data type
- data types [Visual Basic], assigning
ms.assetid: eed44dff-eaee-4937-a89f-444e418e74f6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 02234afc0dc51a2c1338cdd16d1f97765f64b45e
ms.sourcegitcommit: d2da0142247ef42a219a5d2907f153e62dc6ea0d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="byte-data-type-visual-basic"></a>Type de données Byte (Visual Basic)
Blocages entiers non signés 8 bits (1 octet) que de valeurs comprises entre 0 et 255.

## <a name="remarks"></a>Notes

Utilisez le `Byte` type de données pour contenir les données binaires.  
  
La valeur par défaut de `Byte` est 0.

## <a name="literal-assignments"></a>Attributions de littéral

Vous pouvez déclarer et initialiser une `Byte` variable en lui assignant un décimal littéral, un littéral hexadécimal, un littéral octal, ou (à partir de Visual Basic 2017) un littéral binaire. Si le littéral entier est en dehors de la plage d’un `Byte` (autrement dit, si elle est inférieure à <xref:System.Byte.MinValue?displayProperty=nameWithType> ou supérieur à <xref:System.Byte.MaxValue?displayProperty=nameWithType>), une erreur de compilation se produit.

Dans l’exemple suivant, les entiers égal à 201 sont représentées sous forme de nombre décimal, hexadécimal, et les littéraux binaires sont converties implicitement à partir [entier](integer-data-type.md) à `byte` valeurs.

[!code-vb[Byte](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#Byte)]

> [!NOTE]
> Vous utilisez le préfixe `&h` ou `&H` pour désigner un littéral hexadécimal, le préfixe `&b` ou `&B` pour désigner un littéral binaire et le préfixe `&o` ou `&O` pour désigner un littéral octal. Les littéraux décimaux n’ont pas de préfixe.

À partir de Visual Basic 2017, vous pouvez également utiliser le caractère de soulignement, `_`, comme un séparateur de chiffres pour améliorer la lisibilité, comme l’exemple suivant montre le.

[!code-vb[Byte](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#ByteS)]  

À partir de Visual Basic 15.5, vous pouvez également utiliser le caractère de soulignement (`_`) comme séparateur de début entre le préfixe et les chiffres hexadécimaux, binaires ou octales. Exemple :

```vb
Dim number As Byte = &H_6A
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

## <a name="programming-tips"></a>Conseils de programmation

-   **Nombres négatifs.** Étant donné que `Byte` est un type non signé, il ne peut pas représenter un nombre négatif. Si vous utilisez le moins unaire (`-`) opérateur sur une expression qui correspond au type `Byte`, Visual Basic convertit l’expression à `Short` première.
  
-   **Conversions de format.** Lorsque Visual Basic lit ou écrit des fichiers, ou lorsqu’il appelle la DLL, des méthodes et propriétés, il peut convertir automatiquement entre les formats de données. Données binaires stockées dans `Byte` tableaux et des variables sont conservées pendant les conversions de format. Vous ne devez pas utiliser un `String` variable pour les données binaires, car son contenu peut être endommagé lors de la conversion entre les formats Unicode et ANSI.

-   **Étendues.** Le `Byte` type de données s’étend à `Short`, `UShort`, `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single`, ou `Double`. Cela signifie que vous pouvez convertir `Byte` à un de ces types sans rencontrer un <xref:System.OverflowException?displayProperty=nameWithType> erreur.
  
-   **Caractères de type.** `Byte`n’a aucun caractère de type littéral ou un caractère de type identificateur.

-   **Type .NET Framework.** Le type correspondant dans le .NET Framework est la structure <xref:System.Byte?displayProperty=nameWithType>.

## <a name="example"></a>Exemple

 Dans l’exemple suivant, `b` est un `Byte` variable. Les instructions montrent la plage de la variable et l’application d’opérateurs de décalage de bits.

[!code-vb[VbVbalrDataTypes#16](../../../visual-basic/language-reference/data-types/codesnippet/VisualBasic/byte-data-type_1.vb)]  

## <a name="see-also"></a>Voir aussi

 <xref:System.Byte?displayProperty=nameWithType>  
 [Types de données](../../../visual-basic/language-reference/data-types/data-type-summary.md)  
 [Fonctions de conversion de types](../../../visual-basic/language-reference/functions/type-conversion-functions.md)  
 [Liste des conversions](../../../visual-basic/language-reference/keywords/conversion-summary.md)  
 [Utilisation efficace des types de données](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
