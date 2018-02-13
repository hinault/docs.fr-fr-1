---
title: Vue d'ensemble de BlockingCollection
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- BlockingCollection, overview
ms.assetid: 987ea3d7-0ad5-4238-8b64-331ce4eb3f0b
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 5e2235c1a5bbe4a39cf029059290268faa5be154
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="blockingcollection-overview"></a>Vue d'ensemble de BlockingCollection
<xref:System.Collections.Concurrent.BlockingCollection%601> est une classe de collection thread-safe qui fournit les fonctionnalités suivantes :  
  
-   Implémentation du modèle producteur-consommateur.  
  
-   Ajout et reprise simultanés d’éléments à partir de plusieurs threads.  
  
-   Capacité maximale facultative.  
  
-   Opérations d’insertion et de suppression qui se bloquent quand la collection est vide ou complète.  
  
-   Opérations « d’essai » d’insertion et de suppression qui ne se bloquent pas ou qui se bloquent pendant une période spécifiée.  
  
-   Encapsule tout type de collection qui implémente <xref:System.Collections.Concurrent.IProducerConsumerCollection%601>  
  
-   Annulation avec jetons d’annulation.  
  
-   Deux types d’énumération avec `foreach` (`For Each` en Visual Basic) :  
  
    1.  Énumération en lecture seule.  
  
    2.  Énumération qui supprime des éléments à mesure qu’ils sont énumérés.  
  
## <a name="bounding-and-blocking-support"></a>Prise en charge de la délimitation et du blocage  
 <xref:System.Collections.Concurrent.BlockingCollection%601> prend en charge la délimitation et le blocage. La délimitation signifie que vous pouvez définir la capacité maximale de la collection. La délimitation est importante dans certains scénarios, car elle vous permet de contrôler la taille maximale de la collection en mémoire, et elle empêche les threads producteur de se déplacer trop loin avant les threads consommateur.  
  
 Plusieurs threads ou tâches peuvent ajouter simultanément des éléments à la collection, et si la collection atteint sa capacité maximale spécifiée, les threads producteur se bloquent jusqu’à ce qu’un élément soit supprimé. Plusieurs consommateurs peuvent supprimer des éléments simultanément, et si la collection devient vide, les threads consommateur se bloquent jusqu’à ce qu’un producteur ajoute un élément. Un thread producteur peut appeler <xref:System.Collections.Concurrent.BlockingCollection%601.CompleteAdding%2A> pour indiquer qu’aucun élément supplémentaire ne sera ajouté. Les consommateurs surveillent la propriété <xref:System.Collections.Concurrent.BlockingCollection%601.IsCompleted%2A> pour savoir quand la collection est vide et quand aucun autre élément ne sera ajouté. L’exemple suivant montre un BlockingCollection simple avec une capacité limitée de 100. Une tâche de producteur ajoute des éléments à la collection tant qu’une certaine condition externe est remplie, puis appelle <xref:System.Collections.Concurrent.BlockingCollection%601.CompleteAdding%2A>. La tâche du consommateur prend des éléments jusqu’à ce que la propriété <xref:System.Collections.Concurrent.BlockingCollection%601.IsCompleted%2A> ait la valeur true.  
  
 [!code-csharp[CDS_BlockingCollection#04](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/blockingcollection.cs#04)]
 [!code-vb[CDS_BlockingCollection#04](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/introsnippetsbc.vb#04)]  
  
 Pour obtenir un exemple complet, consultez [Guide pratique : ajouter et prendre des éléments individuellement dans un BlockingCollection](../../../../docs/standard/collections/thread-safe/how-to-add-and-take-items.md).  
  
## <a name="timed-blocking-operations"></a>Opérations de blocage temporisé  
 Dans les opérations <xref:System.Collections.Concurrent.BlockingCollection%601.TryAdd%2A> et <xref:System.Collections.Concurrent.BlockingCollection%601.TryTake%2A> de blocage temporisé sur les collections limitées, la méthode tente d’ajouter ou de prendre un élément. Si un élément est disponible, il est placé dans la variable qui a été passée par référence, et la méthode retourne la valeur true. Si aucun élément n’est récupéré après un délai d’attente spécifié, la méthode retourne la valeur false. Le thread est ensuite libre d’effectuer un autre travail utile avant de réessayer d’accéder à la collection. Pour obtenir un exemple d’accès à blocage temporisé, consultez le deuxième exemple de la rubrique [Guide pratique : ajouter et prendre des éléments individuellement dans un BlockingCollection](../../../../docs/standard/collections/thread-safe/how-to-add-and-take-items.md).  
  
## <a name="cancelling-add-and-take-operations"></a>Annulation d’opérations Add et Take  
 Les opérations Add et Take sont généralement effectuées dans une boucle. Vous pouvez annuler une boucle en passant un <xref:System.Threading.CancellationToken> à la méthode <xref:System.Collections.Concurrent.BlockingCollection%601.TryAdd%2A> ou <xref:System.Collections.Concurrent.BlockingCollection%601.TryTake%2A>, puis en vérifiant la valeur de la propriété <xref:System.Threading.CancellationToken.IsCancellationRequested%2A> du jeton à chaque itération. Si la valeur est true, vous pouvez, si vous le souhaitez, répondre à la demande d’annulation en nettoyant toutes les ressources et en quittant la boucle. L’exemple suivant montre une surcharge de <xref:System.Collections.Concurrent.BlockingCollection%601.TryAdd%2A> qui prend un jeton d’annulation, ainsi que le code qui l’utilise :  
  
 [!code-csharp[CDS_BlockingCollection#05](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/blockingcollection.cs#05)]
 [!code-vb[CDS_BlockingCollection#05](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/introsnippetsbc.vb#05)]  
  
 Pour obtenir un exemple d’ajout de prise en charge de l’annulation, consultez le deuxième exemple de la rubrique [Guide pratique : ajouter et prendre des éléments individuellement dans un BlockingCollection](../../../../docs/standard/collections/thread-safe/how-to-add-and-take-items.md).  
  
## <a name="specifying-the-collection-type"></a>Spécification du type de collection  
 Quand vous créez un <xref:System.Collections.Concurrent.BlockingCollection%601>, vous pouvez spécifier non seulement la capacité limitée, mais aussi le type de collection à utiliser. Par exemple, vous pouvez spécifier un <xref:System.Collections.Concurrent.ConcurrentQueue%601> pour un comportement premier entré, premier sorti (FIFO, First In-First Out), ou un <xref:System.Collections.Concurrent.ConcurrentStack%601> pour un comportement dernier entré, premier sorti (LIFO, Last In-First Out). Vous pouvez utiliser n’importe quelle classe de collection qui implémente l’interface <xref:System.Collections.Concurrent.IProducerConsumerCollection%601>. Le type de collection par défaut pour <xref:System.Collections.Concurrent.BlockingCollection%601> est <xref:System.Collections.Concurrent.ConcurrentQueue%601>. L’exemple de code suivant montre comment créer un <xref:System.Collections.Concurrent.BlockingCollection%601> de chaînes qui possède une capacité de 1000 et qui utilise un <xref:System.Collections.Concurrent.ConcurrentBag%601> :  
  
```vb  
Dim bc = New BlockingCollection(Of String)(New ConcurrentBag(Of String()), 1000)  
```  
  
```csharp  
BlockingCollection<string> bc = new BlockingCollection<string>(new ConcurrentBag<string>(), 1000 );  
```  
  
 Pour plus d’informations, consultez [Comment : ajouter des fonctionnalités de liaison et de blocage à une collection](../../../../docs/standard/collections/thread-safe/how-to-add-bounding-and-blocking.md).  
  
## <a name="ienumerable-support"></a>Prise en charge d’IEnumerable  
 <xref:System.Collections.Concurrent.BlockingCollection%601> fournit une méthode <xref:System.Collections.Concurrent.BlockingCollection%601.GetConsumingEnumerable%2A> qui permet aux consommateurs d’utiliser une instruction `foreach` (`For Each` en [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)]) pour supprimer des éléments jusqu’à ce que la collection soit terminée, ce qui signifie qu’elle est vide et qu’aucun autre élément ne sera plus ajouté. Pour plus d’informations, consultez [Guide pratique : utiliser la boucle ForEach pour supprimer les éléments d’un BlockingCollection](../../../../docs/standard/collections/thread-safe/how-to-use-foreach-to-remove.md).  
  
## <a name="using-many-blockingcollections-as-one"></a>Utilisation de nombreux BlockingCollections comme un seul  
 Pour les scénarios dans lesquels un consommateur doit prendre simultanément des éléments à partir de plusieurs collections, vous pouvez créer des tableaux de <xref:System.Collections.Concurrent.BlockingCollection%601> et utiliser les méthodes statiques telles que <xref:System.Collections.Concurrent.BlockingCollection%601.TakeFromAny%2A> et <xref:System.Collections.Concurrent.BlockingCollection%601.AddToAny%2A> qui effectuent un ajout ou une prise dans n’importe laquelle des collections du tableau. Si une collection bloque, la méthode en essaie immédiatement une autre jusqu’à ce qu’elle en trouve une qui peut effectuer l’opération. Pour plus d’informations, consultez [Guide pratique : utiliser des tableaux de collections de blocage dans un pipeline](../../../../docs/standard/collections/thread-safe/how-to-use-arrays-of-blockingcollections.md).  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Collections.Concurrent?displayProperty=nameWithType>  
 [Collections et structures de données](../../../../docs/standard/collections/index.md)  
 [Collections thread-safe](../../../../docs/standard/collections/thread-safe/index.md)
