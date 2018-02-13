---
title: "Chargement de données à partir d'un lecteur"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7e74918c-bc72-4977-a49b-e1520a6d8f60
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 9e9f934d6bff2c9ff3733551bca89b43920f3104
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="load-data-from-a-reader"></a>Chargement de données à partir d'un lecteur
Si un document XML est chargé à l'aide de la méthode <xref:System.Xml.XmlDocument.Load%2A> et d'un paramètre d'objet <xref:System.Xml.XmlReader>, il existe des différences entre le comportement qui se produit et celui du chargement de données d'autres formats. Si le lecteur est dans son état initial, <xref:System.Xml.XmlDocument.Load%2A> utilise l'ensemble du contenu du lecteur et crée le DOM (Document Object Model) XML à partir de toutes les données du lecteur.  
  
 Si le lecteur est déjà positionné sur un nœud du document et s'il est ensuite transmis à la méthode <xref:System.Xml.XmlDocument.Load%2A>, <xref:System.Xml.XmlDocument.Load%2A> essaie de lire le nœud actuel et tous ses frères, jusqu'à la balise finale qui clôture la profondeur actuelle en mémoire. La réussite de la tentative <xref:System.Xml.XmlDocument.Load%2A> dépend du nœud sur lequel le lecteur est situé au moment du chargement, tandis que <xref:System.Xml.XmlDocument.Load%2A> vérifie que le XML provenant du lecteur est correctement construit. Si le XML n'est pas correctement construit, <xref:System.Xml.XmlDocument.Load%2A> lève une exception. Par exemple, la collection de nœuds suivante comporte deux éléments de niveau racine, le XML n'est pas correctement construit et <xref:System.Xml.XmlDocument.Load%2A> lève une exception.  
  
-   Nœud Comment, suivi d'un nœud Element, lui-même suivi d'un nœud Element, suivi d'un nœud EndElement.  
  
 La collection de nœuds suivante crée un DOM incomplet, car aucun élément de niveau racine n'existe.  
  
-   Nœud Comment, suivi d'un nœud ProcessingInstruction, lui-même suivi d'un nœud Comment, suivi d'un nœud EndElement.  
  
 Aucune exception n'est levée et les données sont chargées. Vous pouvez ajouter un élément racine au-dessus de ces nœuds et créer un XML correctement construit qui peut être enregistré sans erreur.  
  
 Si le lecteur est positionné sur un nœud sans descendant non valide pour le niveau racine d'un document (par exemple, un espace blanc ou un nœud d'attribut), le lecteur poursuit la lecture jusqu'à se positionner sur un nœud pouvant être utilisé pour la racine. Le chargement du document démarre à ce stade.  
  
 Par défaut, <xref:System.Xml.XmlDocument.Load%2A> ne vérifie pas si le XML est valide à l'aide de la définition de type de document (DTD) ou la validation de schéma. Il vérifie uniquement si le XML est correctement construit. Pour effectuer la validation, vous devez créer un objet <xref:System.Xml.XmlReader> à l'aide de la classe <xref:System.Xml.XmlReaderSettings>. La classe <xref:System.Xml.XmlReader> peut effectuer la validation à l'aide d'une DTD ou d'un schéma XSD (Schema definition language). La propriété <xref:System.Xml.ValidationType> de la classe <xref:System.Xml.XmlReaderSettings> détermine si l'instance de l'objet <xref:System.Xml.XmlReader> effectue la validation. Pour plus d'informations sur la validation des données XML, consultez la section Notes de la page de référence <xref:System.Xml.XmlReader>.  
  
## <a name="see-also"></a>Voir aussi  
 [DOM (Document Object Model) XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
