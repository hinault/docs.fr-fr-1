---
title: Types valeur Nullable (Visual Basic)
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
f1_keywords: vb.Nullable
helpviewer_keywords:
- nullable types [Visual Basic]
- '? [Visual Basic]'
- types [Visual Basic], nullable
- nullable types [Visual Basic]
- data types [Visual Basic], nullable
ms.assetid: 9ac3b602-6f96-4e6d-96f7-cd4e81c468a6
caps.latest.revision: "23"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 8734114b9d657066a0ef0b2d648f0290c03b1cbf
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="nullable-value-types-visual-basic"></a>Types valeur Nullable (Visual Basic)
Parfois, vous travaillez avec un type valeur qui n’a pas une valeur définie dans certaines circonstances. Par exemple, un champ dans une base de données peut-être faire la distinction entre une valeur assignée est explicite et n’ayant ne pas une valeur assignée. Types de valeur peuvent être étendus pour prendre leurs valeurs normales ou une valeur null. Cette extension est appelée un *type nullable*.  
  
 Chaque type nullable est construit à partir de l’objet générique <xref:System.Nullable%601> structure. Envisagez d’une base de données qui effectue le suivi des activités liées au travail. L’exemple suivant construit nullable `Boolean` tapez et déclare une variable de ce type. Vous pouvez écrire la déclaration de trois manières :  
  
 [!code-vb[VbVbalrNullableValue#1](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_1.vb)]  
  
 La variable `ridesBusToWork` peut contenir une valeur de `True`, une valeur de `False`, ou aucune valeur. Sa valeur par défaut initiale n’est pas de valeur, qui dans ce cas activée peut signifier que les informations n’ont pas encore été obtenues pour cette personne. En revanche, `False` peut signifier que les informations ont été obtenues et que la personne ne pas le bus pour aller au travail.  
  
 Vous pouvez déclarer des variables et des propriétés avec des types nullables, et vous pouvez déclarer un tableau avec les éléments d’un type nullable. Vous pouvez déclarer des procédures avec des types nullables comme paramètres, et vous pouvez retourner un type nullable à partir d’un `Function` procédure.  
  
 Vous ne pouvez pas construire un type nullable sur un type référence tel qu’un tableau, un `String`, ou une classe. Le type sous-jacent doit être un type valeur. Pour plus d’informations, consultez [les Types valeur et Types référence](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md).  
  
## <a name="using-a-nullable-type-variable"></a>À l’aide d’une Variable de Type Nullable  
 Les membres les plus importants d’un type nullable sont ses <xref:System.Nullable%601.HasValue%2A> et <xref:System.Nullable%601.Value%2A> propriétés. Pour une variable de type nullable, <xref:System.Nullable%601.HasValue%2A> vous indique si la variable contient une valeur définie. Si <xref:System.Nullable%601.HasValue%2A> est `True`, vous pouvez lire la valeur de <xref:System.Nullable%601.Value%2A>. Notez que les deux <xref:System.Nullable%601.HasValue%2A> et <xref:System.Nullable%601.Value%2A> sont `ReadOnly` propriétés.  
  
### <a name="default-values"></a>Valeurs par défaut  
 Lorsque vous déclarez une variable avec un type nullable, sa <xref:System.Nullable%601.HasValue%2A> propriété a la valeur par défaut `False`. Cela signifie que, par défaut, la variable n’a aucune valeur définie, au lieu de la valeur par défaut de son type valeur sous-jacent. Dans l’exemple suivant, la variable `numberOfChildren` a d’initialement aucune valeur définie, même si la valeur par défaut de la `Integer` type est 0.  
  
 [!code-vb[VbVbalrNullableValue#2](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_2.vb)]  
  
 Une valeur null est utile pour indiquer une valeur inconnue ou non définie. Si `numberOfChildren` a été déclaré comme `Integer`, aucune valeur ne peuvent indiquer que les informations ne sont pas disponibles actuellement.  
  
### <a name="storing-values"></a>Stockage de valeurs  
 Vous stockez une valeur dans une variable ou une propriété d’un type nullable de la manière habituelle. L’exemple suivant assigne une valeur à la variable `numberOfChildren` déclaré dans l’exemple précédent.  
  
 [!code-vb[VbVbalrNullableValue#3](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_3.vb)]  
  
 Si une variable ou une propriété d’un type nullable contient une valeur définie, vous pouvez provoquer pour rétablir l’état initial de n’ayant ne pas de valeur assignée. Pour cela en définissant la variable ou la propriété `Nothing`, comme le montre l’exemple suivant.  
  
 [!code-vb[VbVbalrNullableValue#4](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_4.vb)]  
  
> [!NOTE]
>  Bien que vous puissiez attribuer `Nothing` à une variable d’un type nullable, vous ne pouvez pas tester pour `Nothing` à l’aide du signe égal. Comparaison qui utilise le signe égal, `someVar = Nothing`, a toujours la valeur `Nothing`. Vous pouvez tester la variable <xref:System.Nullable%601.HasValue%2A> propriété `False`, ou de test à l’aide de la `Is` ou `IsNot` opérateur.  
  
### <a name="retrieving-values"></a>Extraction de valeurs  
 Pour récupérer la valeur d’une variable d’un type nullable, vous devez d’abord tester son <xref:System.Nullable%601.HasValue%2A> pour confirmer qu’il possède une valeur de propriété. Si vous essayez de lire la valeur lorsque <xref:System.Nullable%601.HasValue%2A> est `False`, [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] lève une <xref:System.InvalidOperationException> exception. L’exemple suivant montre la méthode recommandée pour lire la variable `numberOfChildren` des exemples précédents.  
  
 [!code-vb[VbVbalrNullableValue#5](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_5.vb)]  
  
## <a name="comparing-nullable-types"></a>Comparaison des Types Nullable  
 Lorsque nullable `Boolean` variables sont utilisées dans les expressions booléennes, le résultat peut être `True`, `False`, ou `Nothing`. Voici la table de vérité pour `And` et `Or`. Étant donné que `b1` et `b2` ont maintenant des trois valeurs possibles, il existe neuf combinaisons à évaluer.  
  
|B1|B2|B1 et b2|B1 ou b2|  
|--------|--------|---------------|--------------|  
|`Nothing`|`Nothing`|`Nothing`|`Nothing`|  
|`Nothing`|`True`|`Nothing`|`True`|  
|`Nothing`|`False`|`False`|`Nothing`|  
|`True`|`Nothing`|`Nothing`|`True`|  
|`True`|`True`|`True`|`True`|  
|`True`|`False`|`False`|`True`|  
|`False`|`Nothing`|`False`|`Nothing`|  
|`False`|`True`|`False`|`True`|  
|`False`|`False`|`False`|`False`|  
  
 Lorsque la valeur d’une variable ou expression booléenne est `Nothing`, il n’est ni `true` ni `false`. Prenons l'exemple suivant.  
  
 [!code-vb[VbVbalrNullableValue#6](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_6.vb)]  
  
 Dans cet exemple, `b1 And b2` prend la valeur `Nothing`. Par conséquent, le `Else` clause est exécutée dans chaque `If` instruction et la sortie est la suivante :  
  
 `Expression is not true`  
  
 `Expression is not false`  
  
> [!NOTE]
>  `AndAlso`et `OrElse`, qui utilisent l’évaluation de court-circuit doit évaluer leurs seconds opérandes lorsque le premier prend la valeur de `Nothing`.  
  
## <a name="propagation"></a>Propagation  
 Si un ou les deux opérandes d’une opération arithmétique, comparaison, MAJ ou d’une opération de type est nullable, le résultat de l’opération est également nullable. Si les deux opérandes ont des valeurs qui ne sont pas `Nothing`, l’opération est effectuée sur les valeurs sous-jacentes des opérandes, comme si aucune n’était un type nullable. Dans l’exemple suivant, les variables `compare1` et `sum1` sont implicitement typées. Si vous placez le pointeur de la souris au-dessus d’eux, vous verrez que le compilateur déduit les types nullable pour les deux.  
  
 [!code-vb[VbVbalrNullableValue#7](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_7.vb)]  
  
 Si un ou deux opérandes ont la valeur `Nothing`, le résultat sera `Nothing`.  
  
 [!code-vb[VbVbalrNullableValue#8](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_8.vb)]  
  
## <a name="using-nullable-types-with-data"></a>Utilisation des Types Nullable avec des données  
 Une base de données est un des emplacements plus importants pour utiliser des types nullables. Pas tous les objets de base de données charge actuellement les types nullable, mais les cartes générées par le concepteur. Consultez « Prise en charge pour les Types Nullable le TableAdapter » dans [vue d’ensemble de TableAdapter](/visualstudio/data-tools/tableadapter-overview).  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.InvalidOperationException>  
 <xref:System.Nullable%601.HasValue%2A>  
 [Utilisation de types Nullable](../../../../csharp/programming-guide/nullable-types/using-nullable-types.md)  
 [Types de données](../../../../visual-basic/programming-guide/language-features/data-types/index.md)  
 [Types valeur et types référence](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)  
 [Dépannage des types de données](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)  
 [Vue d’ensemble de TableAdapter](/visualstudio/data-tools/tableadapter-overview)  
 [If (opérateur)](../../../../visual-basic/language-reference/operators/if-operator.md)  
 [Inférence de type local](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)  
 [Is (opérateur)](../../../../visual-basic/language-reference/operators/is-operator.md)  
 [IsNot (opérateur)](../../../../visual-basic/language-reference/operators/isnot-operator.md)
