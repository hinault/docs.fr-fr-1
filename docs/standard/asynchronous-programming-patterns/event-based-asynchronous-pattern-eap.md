---
title: "Modèle asynchrone basé sur les événements (EAP)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- asynchronous calls
- asynchronous programming, design patterns
- asynchronous programming
ms.assetid: c6baed9f-2a25-4728-9a9a-53b7b14840cf
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 2a83d638255d27317ba5d566ab46b83526659365
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="event-based-asynchronous-pattern-eap"></a>Modèle asynchrone basé sur les événements (EAP)
Il existe plusieurs façons d’exposer des fonctionnalités asynchrones à du code client. Le modèle asynchrone basé sur les événements recommande une méthode pour obtenir des classes un comportement asynchrone.  
  
> [!NOTE]
>  À partir du [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], la bibliothèque parallèle de tâches fournit un nouveau modèle de programmation asynchrone et parallèle. Pour plus d’informations, consultez la page [Programmation parallèle](../../../docs/standard/parallel-programming/index.md).  
  
## <a name="in-this-section"></a>Dans cette section  
 [Vue d’ensemble du modèle asynchrone basé sur les événements](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)  
 Explique comment le modèle asynchrone basé sur les événements permet de profiter des avantages des applications multithread tout en masquant de nombreux problèmes complexes inhérents à la conception multithread.  
  
 [Implémentation du modèle asynchrone basé sur les événements](../../../docs/standard/asynchronous-programming-patterns/implementing-the-event-based-asynchronous-pattern.md)  
 Décrit la façon standardisée de placer dans un package une classe qui possède des fonctionnalités asynchrones.  
  
 [Meilleures pratiques pour implémenter le modèle asynchrone basé sur les événements](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)  
 Décrit les exigences liées à l’exposition de fonctionnalités asynchrones conformément au modèle asynchrone basé sur les événements.  
  
 [Choix du moment auquel implémenter le modèle asynchrone basé sur les événements](../../../docs/standard/asynchronous-programming-patterns/deciding-when-to-implement-the-event-based-asynchronous-pattern.md)  
 Explique dans quelles situations vous devez implémenter le modèle asynchrone basé sur les événements plutôt que le modèle <xref:System.IAsyncResult>.  
  
 [Procédure pas à pas : implémenter un composant qui prend en charge le modèle asynchrone basé sur les événements](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)  
 Illustre la création d’un composant qui implémente le modèle asynchrone basé sur les événements. Il est implémenté à l'aide de classes d'assistance à partir de l'espace de noms <xref:System.ComponentModel?displayProperty=nameWithType>, ce qui garantit le bon fonctionnement du composant avec n'importe quel modèle d'application.  
  
 [Guide pratique : utiliser des composants qui prennent en charge le modèle asynchrone basé sur les événements](../../../docs/standard/asynchronous-programming-patterns/how-to-use-components-that-support-the-event-based-asynchronous-pattern.md)  
 Explique comment créer un composant qui prend en charge le modèle asynchrone basé sur les événements.  
  
## <a name="reference"></a>Référence  
 <xref:System.ComponentModel.AsyncOperation>  
 Décrit la classe <xref:System.ComponentModel.AsyncOperation> et propose des liens vers tous ses membres.  
  
 <xref:System.ComponentModel.AsyncOperationManager>  
 Décrit la classe <xref:System.ComponentModel.AsyncOperationManager> et propose des liens vers tous ses membres.  
  
 <xref:System.ComponentModel.BackgroundWorker>  
 Décrit le composant <xref:System.ComponentModel.BackgroundWorker> et propose des liens vers tous ses membres.  
  
## <a name="related-sections"></a>Rubriques connexes  
 [La bibliothèque parallèle de tâches](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)  
 Décrit un modèle de programmation pour les opérations asynchrones et parallèles.  
  
 [Thread](../../../docs/standard/threading/index.md)  
 Décrit les fonctionnalités de multithreading du .NET Framework.  
  
 [Thread](http://msdn.microsoft.com/library/552f6c68-dbdb-4327-ae36-32cf9063d88c)  
 Décrit les fonctionnalités de multithreading des langages C# et Visual Basic.  
  
## <a name="see-also"></a>Voir aussi  
 [Bonnes pratiques de threading géré](../../../docs/standard/threading/managed-threading-best-practices.md)  
 [Événements](../../../docs/standard/events/index.md)  
 [Multithreading dans les composants](http://msdn.microsoft.com/library/2fc31e68-fb71-4544-b654-0ce720478779)  
 [Modèles de conception de la programmation asynchrone](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)
