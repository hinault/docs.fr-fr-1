---
title: "Utilisation de gestionnaires filtrés par l'utilisateur"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- user-filtered exceptions
- exceptions, user-filtered
ms.assetid: aa80d155-060d-41b4-a636-1ceb424afee8
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 1f5eb735262ee7ef69e200b1249c7b1c4a1e2ac2
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="using-user-filtered-exception-handlers"></a>Utilisation de gestionnaires filtrés par l'utilisateur
Visual Basic prend actuellement en charge les exceptions filtrées par l’utilisateur. Les gestionnaires d’exceptions filtrés par l’utilisateur interceptent et gèrent les exceptions selon des critères que vous définissez pour l’exception. Ces gestionnaires utilisent l’instruction **Catch** avec le mot clé **When**.  
  
 Cette technique est utile lorsqu’un objet d’exception particulier correspond à plusieurs erreurs. Dans ce cas, l’objet possède généralement une propriété qui contient le code d’erreur associé à l’erreur. Vous pouvez utiliser la propriété de code d’erreur dans l’expression pour sélectionner uniquement l’erreur particulière que vous souhaitez gérer dans cette clause **Catch**.  
  
 L’exemple Visual Basic suivant illustre l’instruction **Catch/When**.  
  
```  
Try  
      'Try statements.  
   Catch When Err = VBErr_ClassLoadException  
      'Catch statements.  
End Try  
```  
  
 L’expression de la clause filtrée par l’utilisateur n’est pas limitée. Si une exception se produit pendant l’exécution de l’expression filtrée par l’utilisateur, cette exception est ignorée et l’expression filtrée est considérée comme ayant la valeur False. Dans ce cas, le common language runtime continue la recherche d’un gestionnaire pour l’exception actuelle.  
  
## <a name="combining-the-specific-exception-and-the-user-filtered-clauses"></a>Combinaison de l’exception spécifique et des clauses filtrées par l’utilisateur  
 Une instruction catch peut contenir à la fois l’exception spécifique et les clauses filtrées par l’utilisateur. Le runtime teste tout d’abord l’exception spécifique. Si l’exception spécifique réussit, le runtime exécute le filtre de l’utilisateur. Le filtre générique peut contenir une référence à la variable déclarée dans le filtre de la classe. Notez que l’ordre des deux clauses de filtre ne peut pas être inversé.  
  
 L’exemple Visual Basic suivant illustre l’exception spécifique `ClassLoadException` dans l’instruction **Catch** ainsi que la clause filtrée par l’utilisateur à l’aide du mot clé **When**.  
  
```  
Try  
      'Try statements.  
   Catch cle As ClassLoadException When cle.IsRecoverable()  
      'Catch statements.  
End Try  
```  

## <a name="see-also"></a>Voir aussi
[Exceptions](index.md)
