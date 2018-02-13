---
title: "Modification de nœuds, de contenu et de valeurs dans un document XML"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 761773e0-db72-4986-b9f5-a522213d8397
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 72039faef3bcde4db830d110938266c63689219e
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="modifying-nodes-content-and-values-in-an-xml-document"></a>Modification de nœuds, de contenu et de valeurs dans un document XML
Il existe plusieurs façons de modifier les nœuds et le contenu d'un document. Vous pouvez :  
  
-   Modifier la valeur des nœuds à l'aide de la propriété <xref:System.Xml.XmlNode.Value%2A>.  
  
-   Modifier un ensemble complet de nœuds en les remplaçant par des nouveaux. Pour ce faire, utilisez la propriété <xref:System.Xml.XmlNode.InnerXml%2A>.  
  
-   Remplacer les nœuds existants à l'aide de la méthode <xref:System.Xml.XmlNode.RemoveChild%2A>.  
  
-   Ajouter des caractères supplémentaires aux nœuds héritant de la classe <xref:System.Xml.XmlCharacterData> à l'aide des méthodes <xref:System.Xml.XmlCharacterData.AppendData%2A>, <xref:System.Xml.XmlCharacterData.InsertData%2A> ou <xref:System.Xml.XmlCharacterData.ReplaceData%2A>.  
  
-   Modifier le contenu en supprimant une série de caractères à l'aide de la méthode <xref:System.Xml.XmlCharacterData.DeleteData%2A> sur les types de nœuds héritant de l'objet <xref:System.Xml.XmlCharacterData>.  
  
 Une technique simple de modification de la valeur d'un nœud consiste à utiliser `node.Value = "new value";`. Le tableau suivant répertorie les types de nœuds utilisés par cette ligne de code unique et les données exactes modifiées pour ce type de nœud.  
  
|Type de nœud|Données modifiées|  
|---------------|------------------|  
|Attribut|Valeur de l'attribut.|  
|CDATASection.|Contenu de CDATASection.|  
|Commentaire|Contenu du commentaire.|  
|ProcessingInstruction ;|Contenu, cible exclue.|  
|Texte|Contenu du texte.|  
|XmlDeclaration|Contenu de la déclaration, balisage `<?xml` et `?>` exclu.|  
|Whitespace|Valeur de l'espace blanc. Vous pouvez définir la valeur de l'un des quatre caractères d'espace blanc XML reconnus : espace, tabulation, CR ou LF.|  
|SignificantWhitespace|Valeur de l'espace blanc significatif. Vous pouvez définir la valeur de l'un des quatre caractères d'espace blanc XML reconnus : espace, tabulation, CR ou LF.|  
  
 Tout type de nœud absent de ce tableau n'est pas un type de nœud valide pour recevoir une valeur. La définition d'une valeur à ces types de nœud lève un objet <xref:System.InvalidOperationException>.  
  
 La propriété <xref:System.Xml.XmlNode.InnerXml%2A> modifie le balisage des nœuds enfants du nœud actuel. Sa définition remplace les nœuds enfants par le contenu analysé de la chaîne donnée. L'analyse est effectuée dans le contexte de l'espace de noms actuel. De plus, la propriété <xref:System.Xml.XmlNode.InnerXml%2A> supprime les déclarations d'espaces de noms redondantes. Par conséquent, de nombreuses opérations de couper-coller n'augmentent pas la taille du document avec des déclarations d'espaces de noms redondantes. Pour examiner un exemple de code illustrant l'effet des espaces de noms sur l'opération <xref:System.Xml.XmlNode.InnerXml%2A>, voir la propriété <xref:System.Xml.XmlDocument.InnerXml%2A>.  
  
 L'utilisation des méthodes <xref:System.Xml.XmlCharacterData.ReplaceData%2A> et <xref:System.Xml.XmlNode.RemoveChild%2A> retourne le nœud remplacé ou supprimé. Ce nœud peut ensuite être réinséré ailleurs dans le DOM (Document Object Model). La méthode <xref:System.Xml.XmlCharacterData.ReplaceData%2A> procède à deux contrôles de validation sur le nœud inséré dans le document. Le premier vérifie si le nœud en question devient un enfant d'un nœud pouvant comporter des nœuds enfants de ce type. Le second contrôle si le nœud inséré n'est pas un ancêtre du nœud dont il devient un enfant. Si l'une de ces deux conditions est enfreinte, un objet <xref:System.InvalidOperationException> est levé.  
  
 L'ajout ou la suppression d'un enfant en lecture seule d'un nœud modifiable est une opération valide. Cependant, toute tentative de modification de ce nœud en lecture seule à proprement parler lève un objet <xref:System.InvalidOperationException>. C'est le cas, par exemple, lorsque vous modifiez les enfants du nœud <xref:System.Xml.XmlEntityReference>. Ces enfants sont en lecture seule et ne peuvent donc pas être modifiés. Si vous tentez de les modifier, un objet <xref:System.InvalidOperationException> est levé.  
  
## <a name="see-also"></a>Voir aussi  
 [DOM (Document Object Model) XML](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
