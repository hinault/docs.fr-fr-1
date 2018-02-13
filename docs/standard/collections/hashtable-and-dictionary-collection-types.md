---
title: Types collection Hashtable et Dictionary
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Hashtable class, grouping data in collections
- Hashtable collection type
- hash tables
- grouping data in collections, Hashtable collection type
- hash function
- collections [.NET Framework], Hashtable collection type
ms.assetid: bfc20837-3d02-4fc7-8a8f-c5215b6b7913
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 5ab3a6bb2128a3753cb80a60836a781d987ca253
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="hashtable-and-dictionary-collection-types"></a>Types collection Hashtable et Dictionary
La classe <xref:System.Collections.Hashtable?displayProperty=nameWithType>, ainsi que les classes génériques <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType> et <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=nameWithType>, implémentent l'interface <xref:System.Collections.IDictionary?displayProperty=nameWithType>. La classe générique <xref:System.Collections.Generic.Dictionary%602> implémente également l'interface générique <xref:System.Collections.Generic.IDictionary%602>. Par conséquent, chaque élément de ces collections est une paire clé-valeur.  
  
 Un objet <xref:System.Collections.Hashtable> est constitué de compartiments contenant les éléments de la collection. Un compartiment est un sous-groupe virtuel d'éléments dans la <xref:System.Collections.Hashtable>, ce qui rend la recherche et la récupération plus facile et plus rapide que dans la plupart des collections. Chaque compartiment est associé à un code de hachage qui est généré à l'aide d'une fonction de hachage et qui est basé sur la clé de l'élément.  
  
 La classe générique <xref:System.Collections.Generic.HashSet%601> est une collection non ordonnée destinée à contenir des éléments uniques.  
  
 Une fonction de hachage est un algorithme qui retourne un code de hachage numérique basé sur une clé. La clé est la valeur d'une propriété de l'objet stocké. Une fonction de hachage doit toujours retourner le même code de hachage pour la même clé. Il est possible pour une fonction de hachage pour générer le même code de hachage pour deux clés différentes, mais une fonction de hachage qui génère un code de hachage unique pour chaque clé unique produit de meilleures performances lors de la récupération des éléments dans la table de hachage.  
  
 Chaque objet qui est utilisé comme un élément dans une table <xref:System.Collections.Hashtable> doit être en mesure de générer un code de hachage pour lui-même en utilisant une implémentation de la méthode <xref:System.Object.GetHashCode%2A>. Cependant, vous pouvez également spécifier une fonction de hachage pour tous les éléments d'une table <xref:System.Collections.Hashtable> en utilisant un constructeur <xref:System.Collections.Hashtable> qui accepte une implémentation de <xref:System.Collections.IHashCodeProvider> comme un de ses paramètres.  
  
 Quand un objet est ajouté à une table <xref:System.Collections.Hashtable>, il est stocké dans le compartiment associé au code de hachage qui correspond au code de hachage de l'objet. Quand une valeur est recherchée dans la <xref:System.Collections.Hashtable>, le code de hachage est généré pour cette valeur, et le compartiment associé à ce code de hachage est recherché.  
  
 Par exemple, une fonction de hachage pour une chaîne peut prendre les codes ASCII de chaque caractère de la chaîne et les additionner pour générer un code de hachage. La chaîne "pique-nique" aurait ainsi un code de hachage différent du code de hachage de la chaîne "basket". Les chaînes "pique-nique" et "basket" seraient donc dans des compartiments différents. Par contre, "ail" et "lia" auraient le même code de hachage et seraient dans le même compartiment.  
  
 Les classes <xref:System.Collections.Generic.Dictionary%602> et <xref:System.Collections.Concurrent.ConcurrentDictionary%602> ont les mêmes fonctionnalités que la classe <xref:System.Collections.Hashtable>. Un dictionnaire <xref:System.Collections.Generic.Dictionary%602> d'un type spécifique (autre que <xref:System.Object>) offre de meilleures performances qu'une table <xref:System.Collections.Hashtable> pour les types valeur. La raison en est que les éléments de <xref:System.Collections.Hashtable> sont de type <xref:System.Object>. Par conséquent, le boxing et la conversion unboxing se produisent généralement quand vous stockez ou que vous récupérez un type valeur. La classe <xref:System.Collections.Concurrent.ConcurrentDictionary%602> doit être utilisée quand plusieurs threads sont susceptibles d’accéder simultanément à la collection.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Collections.Hashtable>  
 <xref:System.Collections.IDictionary>  
 <xref:System.Collections.IHashCodeProvider>  
 <xref:System.Collections.Generic.Dictionary%602>  
 <xref:System.Collections.Generic.IDictionary%602?displayProperty=nameWithType>  
 <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=nameWithType>  
 [Types de collections couramment utilisés](../../../docs/standard/collections/commonly-used-collection-types.md)
