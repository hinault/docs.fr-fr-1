---
title: "Programmation multithread avec le modèle asynchrone basé sur les événements"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET Framework], asynchronous
- AsyncOperationManager class
- threading [.NET Framework], asynchronous features
- components [.NET Framework], asynchronous
- AsyncOperation class
- AsyncCompletedEventArgs class
ms.assetid: 958d6617-5e70-4b36-b5db-63c16dc35e43
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 557d639cc8a4e7ade2cfbd1f5d7264bca226d273
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="multithreaded-programming-with-the-event-based-asynchronous-pattern"></a>Programmation multithread avec le modèle asynchrone basé sur les événements
Il existe plusieurs façons d’exposer des fonctionnalités asynchrones à du code client. Le modèle asynchrone basé sur les événements prescrit la méthode recommandée pour que les classes présentent un comportement asynchrone.  
  
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
  
## <a name="see-also"></a>Voir aussi  
 [Bonnes pratiques de threading géré](../../../docs/standard/threading/managed-threading-best-practices.md)  
 [Événements](../../../docs/standard/events/index.md)  
 [Multithreading dans les composants](http://msdn.microsoft.com/library/2fc31e68-fb71-4544-b654-0ce720478779)  
 [Modèle asynchrone basé sur les événements (EAP)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)
