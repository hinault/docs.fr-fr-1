---
title: "Quand utiliser les collections génériques"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- collections [.NET Framework], generic
- generic collections [.NET Framework]
ms.assetid: e7b868b1-11fe-4ac5-bed3-de68aca47739
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: fe09b2fa156575c7843f8b32bf758c44086b5ca8
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="when-to-use-generic-collections"></a>Quand utiliser les collections génériques
L'utilisation de collections génériques est généralement recommandée, car elle permet de bénéficier immédiatement de la cohérence des types sans avoir à dériver d'un type de collection de base et à implémenter des membres spécifiques au type. Les types de collections génériques sont généralement plus performants que leurs équivalents non génériques (et mieux que les types dérivés de types de collections de base non génériques) quand les éléments de collection sont des types valeur, car grâce aux génériques, aucun boxing d'éléments n'est nécessaire.  
  
 Pour les programmes qui ciblent le [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] ou version ultérieure, vous devez utiliser les classes de collections génériques dans l'espace de noms <xref:System.Collections.Concurrent> quand plusieurs threads sont susceptibles d'ajouter ou de supprimer simultanément des éléments de la collection.  
  
 Les types génériques suivants correspondent à des types de collections existants :  
  
-   <xref:System.Collections.Generic.List%601> est la classe générique qui correspond à <xref:System.Collections.ArrayList>.  
  
-   <xref:System.Collections.Generic.Dictionary%602> et <xref:System.Collections.Concurrent.ConcurrentDictionary%602> sont les classes génériques qui correspondent à <xref:System.Collections.Hashtable>.  
  
-   <xref:System.Collections.ObjectModel.Collection%601> est la classe générique qui correspond à <xref:System.Collections.CollectionBase>. <xref:System.Collections.ObjectModel.Collection%601> peut être utilisée comme classe de base, mais contrairement à <xref:System.Collections.CollectionBase>, elle n'est pas abstraite. Cela la rend plus facile à utiliser.  
  
-   <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> est la classe générique qui correspond à <xref:System.Collections.ReadOnlyCollectionBase>. <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> n'est pas abstraite et possède un constructeur qui facilite l'exposition d'une <xref:System.Collections.Generic.List%601> existante sous la forme d'une collection en lecture seule.  
  
-   Les classes génériques <xref:System.Collections.Generic.Queue%601>, <xref:System.Collections.Concurrent.ConcurrentQueue%601>, <xref:System.Collections.Generic.Stack%601>, <xref:System.Collections.Concurrent.ConcurrentStack%601>et <xref:System.Collections.Generic.SortedList%602> correspondent aux classes non génériques qui portent le même nom.  
  
## <a name="additional-types"></a>Autres types  
 Plusieurs types de collections génériques n'ont pas d'équivalents non génériques. Il s'agit notamment des types suivants :  
  
-   <xref:System.Collections.Generic.LinkedList%601> est une liste liée à usage général qui fournit des opérations d'insertion et de suppression O(1).  
  
-   <xref:System.Collections.Generic.SortedDictionary%602> est un dictionnaire trié avec des opérations d'insertion et d'extraction O(log `n`), ce qui en fait une alternative pratique à <xref:System.Collections.Generic.SortedList%602>.  
  
-   <xref:System.Collections.ObjectModel.KeyedCollection%602> est un hybride entre une liste et un dictionnaire qui permet de stocker des objets qui contiennent leurs propres clés.  
  
-   <xref:System.Collections.Concurrent.BlockingCollection%601> implémente une classe de collection avec une fonctionnalité d'englobement et de blocage.  
  
-   <xref:System.Collections.Concurrent.ConcurrentBag%601> permet une insertion et une suppression rapides des éléments non triés.  
  
## <a name="linq-to-objects"></a>LINQ to Objects  
 La fonctionnalité LINQ to Objects permet d'utiliser des requêtes LINQ pour accéder aux objets en mémoire tant que le type d'objet implémente l'interface <xref:System.Collections.IEnumerable?displayProperty=nameWithType> ou <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> . Les requêtes LINQ fournissent un modèle commun pour accéder aux données, sont généralement plus concises et lisibles que les boucles `foreach` standard et intègrent des fonctions de filtrage, de classement et de regroupement. Les requêtes LINQ peuvent également améliorer les performances. Pour plus d’informations, consultez [LINQ to Objects](http://msdn.microsoft.com/library/73cafe73-37cf-46e7-bfa7-97c7eea7ced9) et [Parallel LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md).  
  
## <a name="additional-functionality"></a>Autres fonctionnalités  
 Certains types génériques ont des fonctionnalités que n'ont pas les types de collections non génériques. Par exemple, la classe <xref:System.Collections.Generic.List%601> , qui correspond à la classe non générique <xref:System.Collections.ArrayList> , possède plusieurs méthodes acceptant des délégués génériques, telles que le délégué <xref:System.Predicate%601> qui permet de spécifier des méthodes pour effectuer des recherches dans la liste, le délégué <xref:System.Action%601> , qui représente des méthodes qui agissent sur chaque élément de la liste, et le délégué <xref:System.Converter%602> qui permet de définir des conversions de types.  
  
 La classe <xref:System.Collections.Generic.List%601> permet de spécifier vos propres implémentations d'interface générique <xref:System.Collections.Generic.IComparer%601> pour trier et parcourir des listes. Les classes <xref:System.Collections.Generic.SortedDictionary%602> et <xref:System.Collections.Generic.SortedList%602> possèdent également cette fonctionnalité. De plus, ces classes permettent de spécifier des comparateurs au moment de la création de la collection. De la même façon, les classes <xref:System.Collections.Generic.Dictionary%602> et <xref:System.Collections.ObjectModel.KeyedCollection%602> permettent de spécifier vos propres comparateurs d'égalité.  
  
## <a name="see-also"></a>Voir aussi  
 [Collections et structures de données](../../../docs/standard/collections/index.md)  
 [Types de collections couramment utilisés](../../../docs/standard/collections/commonly-used-collection-types.md)  
 [Génériques](../../../docs/standard/generics/index.md)
