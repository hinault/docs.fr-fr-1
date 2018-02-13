---
title: Passage des arguments par position et par nom (Visual Basic)
ms.custom: 
ms.date: 02/01/2018
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- arguments [Visual Basic], passing by name
- procedures [Visual Basic], arguments
- := passing arguments
- procedure arguments
- Visual Basic code, procedures
- named arguments [Visual Basic], passing arguments
- arguments [Visual Basic], passing by position
- Function procedures [Visual Basic], passing arguments
- named parameters [Visual Basic], passing arguments
- named arguments
- passing parameters [Visual Basic], named parameter arguments
- passing parameters [Visual Basic], by position
- procedures [Visual Basic], calling
- named parameters
- Sub procedures [Visual Basic], passing arguments
- argument passing
- passing parameters [Visual Basic], by name
- argument passing [Visual Basic], by position
- arguments [Visual Basic], listing by name
ms.assetid: 1ad7358f-1da9-48da-a95b-f3c7ed41eff3
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 13f5e5a8da6a899d4920a25b250ca88b2a21f559
ms.sourcegitcommit: 099aa20d9b6450d1b7452d782a55771a6ad8ff35
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/05/2018
---
# <a name="passing-arguments-by-position-and-by-name-visual-basic"></a>Passage des arguments par position et par nom (Visual Basic)
Lorsque vous appelez un `Sub` ou `Function` procédure, vous pouvez passer des arguments *par position* , dans l’ordre dans lequel elles apparaissent dans la définition de la procédure, ou vous pouvez passer les *par nom*, sans vu les positionner.  
  
 Lorsque vous passez un argument par nom, vous spécifiez l’argument déclaré de le nom suivi d’un signe deux-points et un signe égal (`:=`), suivi par la valeur d’argument. Vous pouvez fournir des arguments nommés dans n’importe quel ordre.  
  
 Par exemple, les éléments suivants `Sub` procédure prend trois arguments :  
  
 [!code-vb[SampleProcedure](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#1)]  
  
 Lorsque vous appelez cette procédure, vous pouvez fournir les arguments par position, par nom ou à l’aide d’une combinaison des deux.  
  
## <a name="passing-arguments-by-position"></a>Passage des Arguments par Position  
 Vous pouvez appeler la `Display` méthode avec des arguments passés par position et délimités par des virgules, comme indiqué dans l’exemple suivant :  
  
[!code-vb[ByPosition](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#2)] 
  
 Si vous omettez un argument facultatif dans une liste d’arguments positionnels, vous devez marquer son emplacement avec une virgule. L’exemple suivant appelle la `Display` méthode sans le `age` argument :  
  
[!code-vb[ByPositionWithOptionalArgument](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#3)] 
  
## <a name="passing-arguments-by-name"></a>Passage des Arguments par nom  
 Vous pouvez également appeler `Display` avec les arguments passés par nom, également délimitées par des virgules, comme indiqué dans l’exemple suivant :  
  
[!code-vb[ByName](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#4)] 

 Passer des arguments par nom de cette façon est particulièrement utile lorsque vous appelez une procédure qui possède plusieurs arguments facultatifs. Si vous fournissez des arguments par nom, vous n’avez pas à utiliser des virgules successives pour signaler l’absence d’arguments de position. Passer des arguments par nom facilite également suivre les arguments que vous passez et ceux qui sont omis.  
  
## <a name="mixing-arguments-by-position-and-by-name"></a>Mélange d’Arguments par Position et par nom  

Vous pouvez fournir des arguments par position et par nom dans un seul appel de procédure, comme indiqué dans l’exemple suivant :  
  
[!code-vb[ByNameAndPosition](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#5)] 
  
 Dans l’exemple précédent, aucune virgule supplémentaire n’est nécessaire pour marquer l’emplacement de l’indication `age` argument, étant donné que `birth` est passé par nom.  
  
Dans les versions de Visual Basic avant 15.5, lorsque vous fournissez des arguments par un mélange de position et le nom, les arguments positionnels doivent tous être placés premier. Une fois que vous fournissez un argument par nom, tous les autres arguments doivent tous être passés par nom.  Par exemple, l’appel suivant à la `Display` méthode affiche l’erreur du compilateur [BC30241 : argument attendu nommé](../../../misc/bc30241.md).

[!code-vb[ByNameAndPosition](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#6)] 

À partir de Visual Basic 15.5, des arguments de position peuvent suivre des arguments nommés si les arguments de position de fin se trouvent dans la position correcte. Si elles sont compilées sous 15.5 Visual Basic, l’appel précédent à la `Display` méthode se compile correctement et ne génère plus d’erreur du compilateur [BC30241](../../../misc/bc30241.md).  

Cette possibilité de combiner les arguments nommés et positionnels dans n’importe quel ordre est particulièrement utile lorsque vous souhaitez utiliser un argument nommé pour rendre votre code plus lisible. Par exemple, `Person` constructeur de classe requiert deux arguments de type `Person`, qui peuvent être `Nothing`. 

[!code-vb[ByNameAndPosition](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#7)] 

À l’aide des arguments nommés et positionnels mixtes afin que l’objectif du code permet de désactiver quand la valeur de la `father` et `mother` arguments est `Nothing`:

[!code-vb[ByNameAndPosition](../../../../../samples/snippets/visualbasic/programming-guide/language-features/passing-named-arguments/module1.vb#8)] 

Pour suivre des arguments de position avec des arguments nommés, vous devez ajouter l’élément suivant à votre projet Visual Basic (\*.vbproj) fichier :

```xml
<PropertyGroup>
  <LangVersion>15.5</LangVersion>
</PropertyGroup>
```

## <a name="restrictions-on-supplying-arguments-by-name"></a>Restrictions sur la fourniture des Arguments par nom  

Vous ne peut pas passer d’arguments par nom pour éviter d’entrer des arguments requis. Vous pouvez omettre que les arguments facultatifs.  
  
Vous ne pouvez pas passer un tableau de paramètres par nom. Il s’agit, car lorsque vous appelez la procédure, vous indiquez un nombre indéfini d’arguments de séparées par des virgules pour le tableau de paramètres, et le compilateur ne peut pas associer plusieurs arguments avec un nom unique.  
  
## <a name="see-also"></a>Voir aussi  
 [Procédures](./index.md)  
 [Paramètres et arguments d’une procédure](./procedure-parameters-and-arguments.md)  
 [Guide pratique : passer des arguments à une procédure](./how-to-pass-arguments-to-a-procedure.md)  
 [Passage d’un argument par valeur et par référence](./passing-arguments-by-value-and-by-reference.md)  
 [Paramètres facultatifs](./optional-parameters.md)  
 [tableaux de paramètres](./parameter-arrays.md)  
 [Optional](../../../../visual-basic/language-reference/modifiers/optional.md)  
 [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md)
