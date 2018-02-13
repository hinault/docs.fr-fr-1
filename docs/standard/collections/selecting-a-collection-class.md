---
title: "Sélection d’une classe de collection"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- last-in-first-out collections
- first-in-first-out collections
- collections [.NET Framework], selecting collection class
- indexed collections
- Collections classes
- grouping data in collections, selecting collection class
ms.assetid: ba049f9a-ce87-4cc4-b319-3f75c8ddac8a
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 05339b829262a6b9b3a0265e4fbd444c6d586ea3
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="selecting-a-collection-class"></a>Sélection d’une classe de collection
Veillez à choisir votre classe de collection avec soin. L'utilisation d'un type incorrect peut limiter votre utilisation de la collection. En règle générale, évitez d'utiliser les types de l'espace de noms <xref:System.Collections>, sauf si vous ciblez spécifiquement le .NET Framework version 1.1. Les versions génériques et simultanées des collections doivent être préférées en raison de leur sécurité supérieure des types et d'autres améliorations.  
  
 Considérez les questions suivantes :  
  
-   Avez-vous besoin d'une liste séquentielle où l'élément est en général abandonné une fois sa valeur récupérée ?  
  
    -   Si oui, envisagez d'utiliser la classe <xref:System.Collections.Queue> ou bien la classe générique <xref:System.Collections.Generic.Queue%601> si vous avez besoin d'un comportement premier entré, premier sorti (FIFO, First-In, First-Out). Envisagez d'utiliser la classe <xref:System.Collections.Stack> ou bien la classe générique <xref:System.Collections.Generic.Stack%601> si vous avez besoin d'un comportement dernier entré, premier sorti (LIFO, Last-In, First-Out). Pour un accès sécurisé à partir de plusieurs threads, utilisez les versions simultanées <xref:System.Collections.Concurrent.ConcurrentQueue%601> et <xref:System.Collections.Concurrent.ConcurrentStack%601>.  
  
    -   Si ce n'est pas le cas, envisagez d'utiliser les autres collections.  
  
-   Avez-vous besoin d'accéder aux éléments dans un certain ordre, comme FIFO ou LIFO, ou de façon aléatoire ?  
  
    -   La classe <xref:System.Collections.Queue> et la classe générique <xref:System.Collections.Generic.Queue%601> ou <xref:System.Collections.Concurrent.ConcurrentQueue%601> offrent un accès FIFO. Pour plus d’informations, consultez [Quand utiliser une collection thread-safe](../../../docs/standard/collections/thread-safe/when-to-use-a-thread-safe-collection.md).  
  
    -   La classe <xref:System.Collections.Stack> et la classe générique <xref:System.Collections.Generic.Stack%601> ou <xref:System.Collections.Concurrent.ConcurrentStack%601> offrent un accès LIFO. Pour plus d’informations, consultez [Quand utiliser une collection thread-safe](../../../docs/standard/collections/thread-safe/when-to-use-a-thread-safe-collection.md).  
  
    -   La classe générique <xref:System.Collections.Generic.LinkedList%601> autorise un accès séquentiel de haut en bas ou de bas en haut.  
  
-   Avez-vous besoin d'accéder à chaque élément selon son index ?  
  
    -   Les classes <xref:System.Collections.ArrayList> et <xref:System.Collections.Specialized.StringCollection>, ainsi que la classe générique <xref:System.Collections.Generic.List%601>, offrent un accès à leurs éléments via l'index de base zéro de l'élément.  
  
    -   Les classes <xref:System.Collections.Hashtable>, <xref:System.Collections.SortedList>, <xref:System.Collections.Specialized.ListDictionary> et <xref:System.Collections.Specialized.StringDictionary>, ainsi que les classes génériques <xref:System.Collections.Generic.Dictionary%602> et <xref:System.Collections.Generic.SortedDictionary%602>, offrent un accès à leurs éléments via la clé de l'élément.  
  
    -   Les classes <xref:System.Collections.Specialized.NameObjectCollectionBase> et <xref:System.Collections.Specialized.NameValueCollection>, ainsi que les classes génériques <xref:System.Collections.ObjectModel.KeyedCollection%602> et <xref:System.Collections.Generic.SortedList%602>, offrent un accès à leurs éléments via l'index de base zéro ou via la clé de l'élément.  
  
-   Chaque élément contiendra-t-il une valeur, une combinaison d'une clé et d'une valeur, ou une combinaison d'une clé et de plusieurs valeurs ?  
  
    -   Une valeur : utilisez une des collections basées sur l'interface <xref:System.Collections.IList> ou l'interface générique  <xref:System.Collections.Generic.IList%601>.  
  
    -   Une clé et une valeur : utilisez une des collections basées sur l'interface <xref:System.Collections.IDictionary> ou l'interface générique  <xref:System.Collections.Generic.IDictionary%602>.  
  
    -   Une valeur avec une clé incorporée : utilisez la classe générique <xref:System.Collections.ObjectModel.KeyedCollection%602>.  
  
    -   Une clé et plusieurs valeurs : utilisez la classe <xref:System.Collections.Specialized.NameValueCollection>.  
  
-   Avez-vous besoin de trier les éléments différemment de la façon dont ils ont été entrés ?  
  
    -   La classe <xref:System.Collections.Hashtable> trie ses éléments selon leur code de hachage.  
  
    -   La classe <xref:System.Collections.SortedList>, ainsi que les classes génériques <xref:System.Collections.Generic.SortedDictionary%602> et <xref:System.Collections.Generic.SortedList%602>, trient leurs éléments par clé, selon les implémentations de l'interface <xref:System.Collections.IComparer> et de l'interface générique <xref:System.Collections.Generic.IComparer%601>.  
  
    -   <xref:System.Collections.ArrayList> fournit une méthode <xref:System.Collections.ArrayList.Sort%2A> qui prend une implémentation de <xref:System.Collections.IComparer> comme paramètre. Sa contrepartie générique, la classe générique <xref:System.Collections.Generic.List%601>, fournit une méthode <xref:System.Collections.Generic.List%601.Sort%2A> qui prend une implémentation de l'interface générique <xref:System.Collections.Generic.IComparer%601> comme paramètre.  
  
-   Avez-vous besoin de recherches et d'une récupération rapides des informations ?  
  
    -   <xref:System.Collections.Specialized.ListDictionary> est plus rapide que <xref:System.Collections.Hashtable> pour les petites collections (10 éléments ou moins). La classe générique <xref:System.Collections.Generic.Dictionary%602> permet une recherche plus rapide que celle de la classe générique <xref:System.Collections.Generic.SortedDictionary%602>. L'implémentation multithread est <xref:System.Collections.Concurrent.ConcurrentDictionary%602>. <xref:System.Collections.Concurrent.ConcurrentBag%601> fournit une insertion multithread rapide pour les données non ordonnées. Pour plus d’informations sur les deux types multithread, consultez [Quand utiliser une collection thread-safe](../../../docs/standard/collections/thread-safe/when-to-use-a-thread-safe-collection.md).  
  
-   Avez-vous besoin de collections qui acceptent seulement des chaînes ?  
  
    -   <xref:System.Collections.Specialized.StringCollection> (basée sur <xref:System.Collections.IList>) et <xref:System.Collections.Specialized.StringDictionary> (basée sur <xref:System.Collections.IDictionary>) se trouvent dans l'espace de noms <xref:System.Collections.Specialized>.  
  
    -   En outre, vous pouvez utiliser toutes les classes de collection génériques dans l'espace de noms <xref:System.Collections.Generic> comme des collections de chaînes fortement typées en spécifiant la classe <xref:System.String> pour leurs arguments de types génériques.  
  
## <a name="linq-to-objects-and-plinq"></a>LINQ to Objects et PLINQ  
 La fonctionnalité LINQ to Objects permet aux développeurs d'utiliser des requêtes LINQ pour accéder aux objets en mémoire pour autant que le type d'objet implémente <xref:System.Collections.IEnumerable> ou <xref:System.Collections.Generic.IEnumerable%601>. Les requêtes LINQ fournissent un modèle commun pour accéder aux données. Elles sont généralement plus concises et plus lisibles que les boucles `foreach` standard et offrent des fonctions de filtrage, de classement et de regroupement. Pour plus d’informations, consultez [LINQ to Objects](http://msdn.microsoft.com/library/73cafe73-37cf-46e7-bfa7-97c7eea7ced9).  
  
 PLINQ fournit une implémentation parallèle de LINQ to Objects, qui peut offrir une exécution plus rapide des requêtes dans de nombreux scénarios, via une utilisation plus efficace des ordinateurs multicœurs. Pour plus d’informations, consultez [PLINQ (Parallel LINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md).  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Collections>  
 <xref:System.Collections.Specialized>  
 <xref:System.Collections.Generic>  
 [Collections thread-safe](../../../docs/standard/collections/thread-safe/index.md)
