---
title: "UInteger, type de données"
ms.date: 01/31/2018
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.uinteger
helpviewer_keywords:
- numbers [Visual Basic], whole
- UInteger data type
- literal type characters [Visual Basic], UI
- whole numbers
- integral data types [Visual Basic]
- integer numbers
- numbers [Visual Basic], integer
- integers [Visual Basic], data types
- integers [Visual Basic], types
- UI literal type characters [Visual Basic]
- data types [Visual Basic], integral
ms.assetid: db7ddd34-4f23-46f5-84dd-8b0f83bb8729
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ea6d42a604e5a50fab62644034afc82e089792c7
ms.sourcegitcommit: d2da0142247ef42a219a5d2907f153e62dc6ea0d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="uinteger-data-type"></a>UInteger (type de données)

Contient des entiers 32 bits (4 octets) non signés dont la valeur comprise entre 0 et 4 294 967 295.  
  
## <a name="remarks"></a>Notes

 Le `UInteger` type de données fournit la plus grande valeur non signée dans la largeur des données la plus efficace.  
  
 La valeur par défaut de `UInteger` est 0.  
  
## <a name="literal-assignments"></a>Attributions de littéral

Vous pouvez déclarer et initialiser une `UInteger` variable en lui assignant un décimal littéral, un littéral hexadécimal, un littéral octal, ou (à partir de Visual Basic 2017) un littéral binaire. Si le littéral entier est en dehors de la plage de `UInteger` (autrement dit, s’il est inférieur à <xref:System.UInt32.MinValue?displayProperty=nameWithType> ou supérieur à <xref:System.UInt32.MaxValue?displayProperty=nameWithType>, une erreur de compilation se produit.

Dans l’exemple suivant, les entiers égaux à 3 000 000 000 représentés comme des littéraux décimaux, hexadécimaux et binaires sont assignés aux valeurs `UInteger`.
  
[!code-vb[UInteger](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#UInt)]  

> [!NOTE] 
> Vous utilisez le préfixe `&h` ou `&H` pour désigner un littéral hexadécimal, le préfixe `&b` ou `&B` pour désigner un littéral binaire et le préfixe `&o` ou `&O` pour désigner un littéral octal. Les littéraux décimaux n’ont pas de préfixe.

À partir de Visual Basic 2017, vous pouvez également utiliser le caractère de soulignement, `_`, comme un séparateur de chiffres pour améliorer la lisibilité, comme l’exemple suivant montre le.

[!code-vb[UInteger](../../../../samples/snippets/visualbasic/language-reference/data-types/numeric-literals.vb#UIntS)]  

À partir de Visual Basic 15.5, vous pouvez également utiliser le caractère de soulignement (`_`) comme séparateur de début entre le préfixe et les chiffres hexadécimaux, binaires ou octales. Exemple :

```vb
Dim number As UInteger = &H_0F8C_0326
```

[!INCLUDE [supporting-underscores](../../../../includes/vb-separator-langversion.md)]

Littéraux numériques peuvent également inclure le `UI` ou `ui` [caractère de type](../../programming-guide\language-features\data-types/type-characters.md) pour désigner le `UInteger` type de données, comme le montre l’exemple suivant.

```vb
Dim number = &H_0FAC_14D7ui
```

## <a name="programming-tips"></a>Conseils de programmation

 Le `UInteger` et `Integer` des types de données fournissent des performances optimales sur un processeur 32 bits, car les types d’entier plus petits (`UShort`, `Short`, `Byte`, et `SByte`), bien qu’ils utilisent moins de bits, prendre plus de temps charger, stocker et récupérer.  
  
-   **Nombres négatifs.** Étant donné que `UInteger` est un type non signé, il ne peut pas représenter un nombre négatif. Si vous utilisez le moins unaire (`-`) opérateur sur une expression qui correspond au type `UInteger`, Visual Basic convertit l’expression à `Long` première.  
  
-   **Conformité CLS.** Le `UInteger` type de données n’est pas dans le cadre de la [Common Language Specification](http://www.ecma-international.org/publications/standards/Ecma-335.htm) (CLS), un code conforme CLS ne peut pas consommer un composant qui l’utilise.
  
-   **Considérations sur l’interopérabilité.** Si vous utilisez des composants non écrits pour le .NET Framework, par exemple des objets Automation ou COM, gardez à l’esprit que les types tels que `uint` peut avoir une largeur de données différente (16 bits) dans d’autres environnements. Si vous passez un argument de 16 bits à un tel composant, déclarez-le en tant que `UShort` au lieu de `UInteger` dans votre code managé de Visual Basic.  
  
-   **Étendues.** Le `UInteger` type de données s’étend à `Long`, `ULong`, `Decimal`, `Single`, et `Double`. Cela signifie que vous pouvez convertir `UInteger` à un de ces types sans rencontrer un <xref:System.OverflowException?displayProperty=nameWithType> erreur.  
  
-   **Caractères de type.** L’ajout de caractères de type littéral `UI` à un littéral force ce dernier à la `UInteger` type de données. `UInteger`n’a aucun caractère de type d’identificateur.  
  
-   **Type .NET Framework.** Le type correspondant dans le .NET Framework est la structure <xref:System.UInt32?displayProperty=nameWithType>.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.UInt32>  
 [Types de données](../../../visual-basic/language-reference/data-types/data-type-summary.md)  
 [Fonctions de conversion de types](../../../visual-basic/language-reference/functions/type-conversion-functions.md)  
 [Liste des conversions](../../../visual-basic/language-reference/keywords/conversion-summary.md)  
 [Guide pratique : appeler une fonction Windows qui possède des types non signés](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)  
 [Utilisation efficace des types de données](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
