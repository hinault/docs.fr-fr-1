---
title: Automatic Memory Management
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- garbage collection, automatic memory management
- memory, allocating
- memory, automatic memory management
- memory, releasing
- common language runtime, automatic memory management
- automatic memory management
- managed heap
- runtime, automatic memory management
ms.assetid: d4850de5-fa63-4936-a250-5678d118acba
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 5405b6fc080696b7e507e70dd8b04f8ddcc4bbb2
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="automatic-memory-management"></a>Automatic Memory Management
La gestion automatique de la mémoire est un des services que le Common Language Runtime fournit au cours de [l'exécution managée](../../docs/standard/managed-execution-process.md). Le Garbage collector du Common Language Runtime gère l’allocation et la libération de mémoire pour une application. Les développeurs n’ont donc plus à écrire du code pour exécuter leurs tâches de gestion de mémoire lors du développement d’applications managées. La gestion automatique de la mémoire permet d'éliminer des problèmes fréquents tels que l'oubli de libération d'un objet ou les fuites de mémoire ou encore les tentatives d'accès à la mémoire à la recherche d'un objet qui a déjà été libéré. Cette section décrit la façon dont le « garbage collector » alloue et libère la mémoire.  
  
## <a name="allocating-memory"></a>Allocation de mémoire  
 Lorsque vous initialisez un nouveau processus, le runtime réserve une région d'espace d'adressage contigu pour le processus. Cet espace d'adressage est appelé le tas managé. Le tas managé garde un pointeur vers l'adresse qui sera allouée au nouvel objet du tas. À l’origine, ce pointeur indique l’adresse de base du tas managé. Tous les [types référence](../../docs/standard/base-types/common-type-system.md) sont alloués sur le tas managé. Lorsqu’une application crée le premier type référence, la mémoire est allouée pour le type à l’adresse de base du tas managé. Lorsque l'application crée l'objet suivant, le « garbage collector » lui alloue de la mémoire dans l'espace d'adressage qui suit immédiatement le premier objet. Aussi longtemps que de l'espace d'adressage est disponible, le « garbage collector » continue à allouer de l'espace pour de nouveaux objets selon la même procédure.  
  
 L'allocation de mémoire à partir du tas managé est plus rapide que l'allocation de mémoire non managée. Étant donné que le runtime alloue de la mémoire pour un objet en ajoutant une valeur à un pointeur, elle est pratiquement aussi rapide que l'allocation de mémoire à partir de la pile. En outre, puisque les nouveaux objets auxquels un espace mémoire est alloué sont stockés à la suite dans le tas managé, une application peut accéder très rapidement aux objets.  
  
<a name="cpconautomaticmemorymanagementreleasingmemoryanchor1"></a>   
## <a name="releasing-memory"></a>Libération de la mémoire  
 Le moteur d'optimisation du « garbage collector » détermine le meilleur moment pour lancer une opération garbage collection sur base des allocations de mémoire effectuées. Lorsque le « garbage collector » effectue une opération garbage collection, il libère la mémoire pour les objets qui ne sont plus utilisées par l'application. Il détermine les objets qui ne sont plus utilisés en examinant les racines de l'application. Chaque application possède un jeu de racines. Chaque racine fait référence à un objet du tas managé ou, à défaut, a la valeur Null. Les racines de l’application comprennent des champs statiques, des variables et des paramètres locaux sur la pile d’un thread et des Registres du processeur. Le Garbage collector a accès à la liste des racines actives entretenues par le [compilateur juste-à-temps (JIT)](../../docs/standard/managed-execution-process.md) et le runtime. En utilisant cette liste, il examine des racines d'application et crée, au cours du processus, un graphique qui contient tous les objets accessibles à partir des racines.  
  
 Les objets non compris dans le graphique ne sont pas accessibles à partir des racines de l'application. Le « garbage collector » examine les objets inaccessibles et libère la mémoire qui leur a été allouée. Au cours d'une opération garbage collection, le « garbage collector » examine le tas managé pour y détecter les blocs de mémoire occupés par des objets inaccessibles. Chaque fois qu'il détecte un objet inaccessible, il utilise une fonction de copie de mémoire pour compacter les objets accessibles en mémoire et libérer les blocs d'espaces d'adressage alloués aux objets inaccessibles. Lorsque la mémoire allouée aux objets accessibles a été réduite, le « garbage collector » procède aux corrections de pointeurs nécessaires pour que les racines des applications pointent vers les nouveaux emplacements des objets. Il positionne aussi le pointeur du tas managé après le dernier objet accessible. Vous remarquerez que la mémoire est compactée uniquement si une collection détecte un nombre significatif d'objets inaccessibles. Si tous les objets du tas managé survivent à une collection, il n'est pas nécessaire de procéder à un compactage de la mémoire.  
  
 Pour améliorer les performances, le runtime alloue de la mémoire pour les objets de grandes dimensions dans un tas séparé. Le « garbage collector » libère automatiquement la mémoire des objets de grande dimension. Cependant, pour éviter de déplacer de grands objets en mémoire, la mémoire n'est pas compactée.  
  
## <a name="generations-and-performance"></a>Générations et performances  
 Pour optimiser les performances du garbage collector, le tas managé est divisé en trois générations : 0, 1 et 2. L'algorithme de garbage collection du runtime est basé sur plusieurs généralisations que l'industrie informatique a observées en expérimentant des modèles de garbage collection. En premier lieu, il est plus rapide de compacter la mémoire pour une partie du tas managé que pour le tas tout entier. Deuxièmement, les nouveaux objets ont des durées de vie plus courtes que les objets plus anciens. Enfin, les nouveaux objets sont fréquemment liés entre eux et l'application y accède à peu près au même moment.  
  
 Le garbage collector du runtime stocke les nouveaux objets dans la génération 0. Les objets qui sont créés à un stade précoce de la durée de vie de l'application et qui survivent aux collectes sont promus et stockés dans les générations 1 et 2. Le processus de promotion d'objet est décrit ultérieurement dans cette rubrique. Parce qu'il est plus rapide de compacter une partie du tas managé que le tas tout entier, ce schéma permet au « garbage collector » de libérer la mémoire dans une génération spécifique plutôt que de libérer la mémoire de l'intégralité du tas managé chaque fois qu'une opération garbage collection est effectuée.  
  
 En fait, le « garbage collector » procède à une opération collection lorsque la génération 0 est complète. Si une application tente de créer un nouvel objet lorsque la génération 0 est complète, le « garbage collector » observe qu'il n'y a plus d'espace d'adressage disponible dans la génération 0 à allouer à l'objet. Le « garbage collector » effectue une opération garbage collection en essayant de libérer de l'espace d'adressage pour l'objet dans la génération 0. Le « garbage collector » commence par examiner les objets de la génération 0 plutôt que tous les objets du tas managé. Cette approche est la plus efficace parce que les nouveaux objets ont en règle générale une durée de vie courte et qu'une grande part des objets de la génération 0 ne seront plus utilisés par l'application lorsqu'une opération garbage collection sera effectuée. En outre, une opération garbage collection de la génération 0 récupère souvent à elle seule suffisamment de mémoire pour permettre à l’application de continuer à créer de nouveaux objets.  
  
 Après avoir effectué une collection de génération 0, le Garbage collector compacte la mémoire pour les objets accessibles comme expliqué dans la section [Libération de la mémoire](#cpconautomaticmemorymanagementreleasingmemoryanchor1), plus haut dans cette rubrique. Le garbage collector promeut ensuite ces objets et considère que cette partie du tas managé appartient à la génération 1. Étant donné que les objets qui survivent aux collectes ont tendance à avoir de plus longues durées de vie, il est logique de les promouvoir à une génération supérieure. En conséquence, le « garbage collector »n'a pas à réexaminer les objets des générations 1 et 2 chaque fois qu'il effectue une opération garbage collection de la génération 0.  
  
 Après avoir exécuté sa première opération garbage collection de la génération 0 et promu les objets accessibles à la génération 1, le garbage collector considère que le reste du tas managé appartient à la génération 0. Il continue à allouer de la mémoire pour les nouveaux objets de la génération 0 jusqu'à ce qu'elle soit complète et qu'il soit nécessaire d'effectuer une autre collecte. À ce stade, le moteur d'optimisation du « garbage collector » détermine s'il est nécessaire d'examiner les objets des générations plus anciennes. Par exemple, si une collecte de génération 0 ne libère pas assez de mémoire pour que l'application puisse terminer sa création d'objet, le garbage collector peut exécuter une collecte de génération 1, puis de génération 2. Si cela ne libère pas assez de mémoire, le garbage collector peut exécuter une collecte de génération 2, 1 et 0. Après chaque collecte, le garbage collector condense les objets accessibles dans la génération 0 et les promeut à la génération 1. Les objets qui survivent aux collectes sont promus et stockés dans les générations 1 et 2. Comme le garbage collector ne prend en charge que trois générations, les objets de génération 2 qui survivent à une collecte restent dans la génération 2 jusqu'à ce qu'ils soient considérés comme impossibles à atteindre lors d'une prochaine collecte.  
  
## <a name="releasing-memory-for-unmanaged-resources"></a>Libération de mémoire pour des ressources non managées  
 Pour la majorité des objets créés par votre application, vous pouvez laisser au « garbage collector » le soin de réaliser automatiquement les tâches de gestion de mémoire requises. Cependant, les ressources non managées requièrent un nettoyage explicite. Le type le plus répandu de ressource non managée est un objet qui enveloppe une ressource de système d'exploitation telle qu'un handle de fichier ou de fenêtre ou une connexion réseau. Bien que le « garbage collector » soit en mesure de suivre la durée de vie d'un objet managé qui encapsule une ressource non managée, il ne possède pas de connaissances spécifiques sur la façon de nettoyer une ressource. Lors de la création d'un objet qui encapsule une ressource non managée, il est recommandé de fournir le code nécessaire pour nettoyer la ressource non managée dans une méthode **Dispose** publique. En fournissant une méthode **Dispose**, vous donnez la possibilité aux utilisateurs de votre objet d'en libérer explicitement la mémoire lorsqu'ils ont fini de s'en servir. Lorsque vous utilisez un objet qui encapsule une ressource non managée, vous devez garder à l'esprit la méthode **Dispose** et l'appeler si nécessaire. Pour obtenir plus d’informations sur le nettoyage de ressources non managées et un exemple de modèle de conception pour l’implémentation de la méthode **Dispose**, consultez [Garbage collection](../../docs/standard/garbage-collection/index.md).  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.GC>  
 [Nettoyage de la mémoire](../../docs/standard/garbage-collection/index.md)  
 [Processus d'exécution managée](../../docs/standard/managed-execution-process.md)
