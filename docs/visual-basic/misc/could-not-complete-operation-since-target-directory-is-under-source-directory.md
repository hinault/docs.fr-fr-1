---
title: "Impossible d’achever l’opération, car le répertoire cible se situe sous le répertoire source"
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-visual-basic
ms.topic: article
f1_keywords: vbrIO_CyclicOperation
ms.assetid: 850d3a24-5d51-4ac8-a912-630efcd75278
caps.latest.revision: "10"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 0a17877b2335ee010a97f0b522bd4c399867cd7d
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="could-not-complete-operation-since-target-directory-is-under-source-directory"></a>Impossible d’achever l’opération, car le répertoire cible se situe sous le répertoire source
Une opération cyclique a échoué. Les opérations cycliques se répètent et, par conséquent, ne peuvent pas s’achever. Par exemple, l’objet A peut essayer d’hériter de l’objet B qui hérite, à son tour, de l’objet A.  
  
## <a name="to-correct-this-error"></a>Pour corriger cette erreur  
  
-   Lors d’un héritage, vérifiez qu’il n’existe aucune référence cyclique.  
  
## <a name="see-also"></a>Voir aussi  
 [Types d’erreurs](../../visual-basic/programming-guide/language-features/error-types.md)  
 [Éléments fondamentaux du débogage : points d’arrêt](http://msdn.microsoft.com/library/752a02c2-0ac7-4c8b-aa1b-4b2b3b21152e)
