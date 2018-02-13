---
title: "SByte, type de données (Visual Basic)"
ms.date: 04/20/2017
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.sbyte
helpviewer_keywords:
- numbers [Visual Basic], whole
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- data types [Visual Basic], integral
- SByte data type
ms.assetid: 5c38374a-18a1-4cc2-b493-299e3dcaa60f
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d391d7eea27ec7696dbb4c28da8916c744712f32
ms.sourcegitcommit: d2da0142247ef42a219a5d2907f153e62dc6ea0d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="sbyte-data-type-visual-basic"></a>SByte, type de données (Visual Basic)

Contient des entiers 8 bits (1 octet) de valeurs comprises entre -128 et 127 signés.  
  
## <a name="remarks"></a>Notes

Utilisez le `SByte` type de données pour contenir des valeurs entières qui ne nécessitent pas la largeur totale des données de `Integer` ou même la largeur de la moitié des données de `Short`. Dans certains cas, le common language runtime peut être en mesure de compresser vos `SByte` variables étroitement ensemble et d’enregistrer la consommation de mémoire.

La valeur par défaut de `SByte` est 0.

## <a name="literal-assignments"></a>Attributions de littéral
  
Vous pouvez déclarer et initialiser une `SByte` variable en lui assignant un décimal littéral, un littéral hexadécimal, un littéral octal, ou (à partir de Visual Basic 2017) un littéral binaire.

Dans l’exemple suivant, les entiers égal à-102 sont représentées sous forme de nombre décimal, hexadécimal, et les littéraux binaires sont affectés à `SByte` valeurs. Cet exemple nécessite que vous compilez avec le `/removeintchecks` commutateur du compilateur.

[!code-vb[SByte](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#SByte)]  

> [!NOTE] 
> Vous utilisez le préfixe `&h` ou `&H` pour désigner un littéral hexadécimal, le préfixe `&b` ou `&B` pour désigner un littéral binaire et le préfixe `&o` ou `&O` pour désigner un littéral octal. Les littéraux décimaux n’ont pas de préfixe.

À partir de Visual Basic 2017, vous pouvez également utiliser le caractère de soulignement, `_`, comme un séparateur de chiffres pour améliorer la lisibilité, comme l’exemple suivant montre le.

[!code-vb[SByteSeparator](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#SByteS)]  

À partir de Visual Basic 15.5, vous pouvez également utiliser le caractère de soulignement (`_`) comme séparateur de début entre le préfixe et les chiffres hexadécimaux, binaires ou octales. Exemple :

```vb
Dim number As SByte = &H_F9
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

Si le littéral entier est en dehors de la plage de `SByte` (autrement dit, s’il est inférieur à <xref:System.SByte.MinValue?displayProperty=nameWithType> ou supérieur à <xref:System.SByte.MaxValue?displayProperty=nameWithType>, une erreur de compilation se produit. Lorsqu’un littéral entier n’a aucun suffixe, un [entier](integer-data-type.md) est déduit. Si le littéral entier est en dehors de la plage de la `Integer` type, un [Long](long-data-type.md) est déduit. Cela signifie que, dans les exemples précédents, les littéraux numériques `0x9A` et `0b10011010` sont interprétées comme des entiers signés 32 bits avec la valeur 156, ce qui dépasse <xref:System.SByte.MaxValue?displayProperty=nameWithType>. Pour compiler le code à ce qui affecte un entier décimal non à un `SByte`, vous pouvez effectuer l’une des opérations suivantes :

- Désactiver les vérifications de limites d’entier en compilant avec le `/removeintchecks` commutateur du compilateur.

- Utilisez un [caractère de type](../../programming-guide\language-features\data-types/type-characters.md) pour définir explicitement la valeur littérale que vous souhaitez attribuer à la `SByte`. L’exemple suivant assigne un littéral négatif `Short` la valeur en un `SByte`. Notez que, pour les nombres négatifs, le bit de poids fort du mot de poids fort du littéral numérique doit être défini. Dans le cas de notre exemple, il est de type bit 15 du littéral `Short` valeur.

   [!code-vb[SByteTypeChars](../../../../samples/snippets/visualbasic/language-reference/data-types/sbyte-assignment.vb#1)]

## <a name="programming-tips"></a>Conseils de programmation
  
-   **Conformité CLS.** Le `SByte` type de données n’est pas dans le cadre de la [Common Language Specification](http://www.ecma-international.org/publications/standards/Ecma-335.htm) (CLS), un code conforme CLS ne peut pas consommer un composant qui l’utilise.

-   **Étendues.** Le `SByte` type de données s’étend à `Short`, `Integer`, `Long`, `Decimal`, `Single`, et `Double`. Cela signifie que vous pouvez convertir `SByte` à un de ces types sans rencontrer un <xref:System.OverflowException?displayProperty=nameWithType> erreur.
  
-   **Caractères de type.** `SByte`n’a aucun caractère de type littéral ou un caractère de type identificateur.  
  
-   **Type .NET Framework.** Le type correspondant dans le .NET Framework est la structure <xref:System.SByte?displayProperty=nameWithType>.
  
## <a name="see-also"></a>Voir aussi

 <xref:System.SByte?displayProperty=nameWithType>  
 [Types de données](../../../visual-basic/language-reference/data-types/data-type-summary.md)  
 [Fonctions de conversion de types](../../../visual-basic/language-reference/functions/type-conversion-functions.md)  
 [Liste des conversions](../../../visual-basic/language-reference/keywords/conversion-summary.md)  
 [Short (type de données)](../../../visual-basic/language-reference/data-types/short-data-type.md)  
 [Integer (type de données)](../../../visual-basic/language-reference/data-types/integer-data-type.md)  
 [Long (type de données)](../../../visual-basic/language-reference/data-types/long-data-type.md)  
 [Utilisation efficace des types de données](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
