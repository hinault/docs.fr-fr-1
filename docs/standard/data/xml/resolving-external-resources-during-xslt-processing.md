---
title: "Résolution de ressources externes lors du traitement XSLT"
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
ms.assetid: 3a59d31c-0ec5-4de6-a2a9-558531c8116e
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 2bb115e14f8ff5d1065d87335d4d9021bd32ddd1
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="resolving-external-resources-during-xslt-processing"></a>Résolution de ressources externes lors du traitement XSLT
Lors d'une transformation XSLT, il peut s'avérer nécessaire de résoudre des ressources externes à plusieurs moments.  
  
## <a name="using-the-xmlresolver-class"></a>Utilisation de la classe XmlResolver  
 La classe <xref:System.Xml.XmlResolver> permet de résoudre des ressources externes. Le tableau suivant décrit l'implication de l'objet <xref:System.Xml.XmlResolver> dans le traitement XSLT.  
  
|Tâche XSLT|Utilité de XmlResolver|  
|---------------|--------------------------------------|  
|Compilation de la feuille de style|Résolution de l'URI de la feuille de style<br /><br /> -et-<br /><br /> Résolution des références URI dans tout élément `xsl:import` ou `xsl:include`|  
|Exécution de la feuille de style|Résolution de l'URI dans le document de contexte<br /><br /> -et-<br /><br /> Résolution des références URI dans toute fonction XSLT `document()`|  
  
 Les méthodes <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> et <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> comprennent des surcharges qui prennent un objet <xref:System.Xml.XmlResolver> comme l'un de leurs arguments. Si aucun <xref:System.Xml.XmlResolver> n'est spécifié, un <xref:System.Xml.XmlUrlResolver> par défaut sans informations d'identification est utilisé.  
  
 La liste suivante décrit les cas dans lesquels vous pouvez préférer spécifier un objet <xref:System.Xml.XmlResolver> :  
  
-   Si le traitement XSLT doit accéder à une ressource réseau qui nécessite une authentification, vous pouvez utiliser un objet <xref:System.Xml.XmlResolver> avec les informations d'identification nécessaires.  
  
-   Si vous souhaitez limiter les ressources auxquelles le traitement XSLT peut accéder, vous pouvez utiliser un objet <xref:System.Xml.XmlSecureResolver> avec toutes les autorisations correctes. La classe <xref:System.Xml.XmlSecureResolver> doit être utilisée si vous devez ouvrir une ressource non contrôlée ou non fiable.  
  
-   Pour personnaliser le comportement, vous pouvez implémenter votre propre classe <xref:System.Xml.XmlResolver> et l'utiliser pour résoudre les ressources.  
  
-   Pour vous assurer qu'aucune ressource externe n'est accessible, vous pouvez spécifier `null` pour l'argument <xref:System.Xml.XmlResolver>.  
  
## <a name="example"></a>Exemple  
 L'exemple suivant compile une feuille de style stockée sur une ressource réseau. Un objet <xref:System.Xml.XmlUrlResolver> spécifie les informations d'identification nécessaires pour accéder à la feuille de style.  
  
 [!code-csharp[XslCompiledTransform.Load#11](../../../../samples/snippets/csharp/VS_Snippets_Data/XslCompiledTransform.Load/CS/Xslt_Load_v2.cs#11)]
 [!code-vb[XslCompiledTransform.Load#11](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XslCompiledTransform.Load/VB/Xslt_Load_v2.vb#11)]  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Xml.Xsl.XslCompiledTransform>  
 <xref:System.Xml.Xsl.XsltSettings>  
 [Transformations XSLT](../../../../docs/standard/data/xml/xslt-transformations.md)
