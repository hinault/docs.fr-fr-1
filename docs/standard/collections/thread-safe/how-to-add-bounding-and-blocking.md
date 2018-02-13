---
title: "Guide pratique : ajouter des fonctionnalités de délimitation et de blocage à une collection"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- thread-safe collections, custom blocking collections
ms.assetid: 4c2492de-3876-4873-b5a1-000bb404d770
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 7fe57d99382c3472d0af5e5f64f7b237692b921b
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="how-to-add-bounding-and-blocking-functionality-to-a-collection"></a>Guide pratique : ajouter des fonctionnalités de délimitation et de blocage à une collection
Cet exemple indique comment ajouter des fonctionnalités de délimitation et de blocage à une classe de collection personnalisée en implémentant l’interface <xref:System.Collections.Concurrent.IProducerConsumerCollection%601?displayProperty=nameWithType> dans la classe, puis en utilisant une instance de classe comme mécanisme de stockage interne pour un <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=nameWithType>. Pour plus d’informations sur la délimitation et le blocage, consultez [Vue d’ensemble de BlockingCollection](../../../../docs/standard/collections/thread-safe/blockingcollection-overview.md).  
  
## <a name="example"></a>Exemple  
 La classe de collection personnalisée est une file d’attente de priorité de base dans laquelle les niveaux de priorité sont représentés sous la forme d’un tableau d’objets <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=nameWithType>. Aucun classement supplémentaire n’est effectué au sein de chaque file d’attente.  
  
 Dans le code client, trois tâches sont démarrées. La première tâche demande juste aux touches du clavier de permettre l’annulation à tout moment pendant l’exécution. La deuxième tâche est le thread producteur. Elle ajoute de nouveaux éléments à la collection de blocage et donne à chaque élément une priorité basée sur une valeur aléatoire. La troisième tâche supprime des éléments de la collection à mesure qu’ils deviennent disponibles.  
  
 Vous pouvez ajuster le comportement de l’application en rendant un thread plus rapide qu’un autre. Si le thread producteur s’exécute plus rapidement, vous remarquerez les fonctionnalités de délimitation quand la collection de blocage empêche l’ajout d’éléments si elle contient déjà le nombre d’éléments spécifié dans le constructeur. Si le thread consommateur s’exécute plus rapidement, vous remarquerez les fonctionnalités de blocage quand le consommateur attend l’ajout d’un nouvel élément.  
  
 [!code-csharp[CDS_BlockingCollection#06](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/prodcon.cs#06)]  
  
 Par défaut, le stockage pour <xref:System.Collections.Concurrent.BlockingCollection%601?displayProperty=nameWithType> est <xref:System.Collections.Concurrent.ConcurrentQueue%601?displayProperty=nameWithType>.  
  
## <a name="see-also"></a>Voir aussi  
 [Collections thread-safe](../../../../docs/standard/collections/thread-safe/index.md)
