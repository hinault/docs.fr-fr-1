---
title: "Lecture de données XML à l’aide de XPathDocument et XmlDocument"
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
ms.assetid: 5711b225-6aa2-4e4f-9898-19f2d518ad1a
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 9282742669c8e3d8b4a856694c76db834282dbf9
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="reading-xml-data-using-xpathdocument-and-xmldocument"></a>Lecture de données XML à l’aide de XPathDocument et XmlDocument
Il existe deux manières de lire un document XML dans l'espace de noms <xref:System.Xml.XPath?displayProperty=nameWithType>. La première consiste à lire un document XML à l'aide de la classe <xref:System.Xml.XPath.XPathDocument> en lecture seule et la seconde à lire un document XML à l'aide de la classe <xref:System.Xml.XmlDocument> modifiable dans l'espace de noms <xref:System.Xml?displayProperty=nameWithType>.  
  
## <a name="reading-xml-documents-using-the-xpathdocument-class"></a>Lecture de documents XML à l'aide de la classe XPathDocument  
 La classe <xref:System.Xml.XPath.XPathDocument> fournit une représentation rapide, en lecture seule et en mémoire d'un document XML à l'aide du modèle de données XPath. Des instances de la classe <xref:System.Xml.XPath.XPathDocument> sont créées à l'aide de l'un de ses six constructeurs. Ces constructeurs permettent de lire un document XML à l'aide d'un objet <xref:System.IO.Stream>, <xref:System.IO.TextReader> ou <xref:System.Xml.XmlReader>, ainsi que le chemin d'accès `string` à un fichier XML.  
  
 L'exemple suivant illustre l'utilisation du constructeur <xref:System.Xml.XPath.XPathDocument> de la classe `string` en vue de la lecture d'un document XML.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
```  
  
## <a name="reading-xml-documents-using-the-xmldocument-class"></a>Lecture de documents XML à l'aide de la classe XmlDocument  
 La classe <xref:System.Xml.XmlDocument> est une représentation en mémoire modifiable d'un document XML qui implémente les recommandations du W3C sur les modèles objet de document (DOM) niveaux 1 et 2 (noyau). Des instances de la classe <xref:System.Xml.XmlDocument> sont créées à l'aide de l'un de ses trois constructeurs. Pour créer un nouvel objet <xref:System.Xml.XmlDocument> vide, vous pouvez appeler le constructeur de la classe <xref:System.Xml.XmlDocument> sans paramètres. Après avoir appelé le constructeur, utilisez la méthode <xref:System.Xml.XmlDocument.Load%2A> pour charger les données XML dans le nouvel objet <xref:System.Xml.XmlDocument> à partir d'un objet <xref:System.IO.Stream>, <xref:System.IO.TextReader> ou <xref:System.Xml.XmlReader>, ainsi que le chemin d'accès `string` à un fichier XML.  
  
 L'exemple suivant illustre l'utilisation du constructeur de la classe <xref:System.Xml.XmlDocument> sans paramètres et de la méthode <xref:System.Xml.XmlDocument.Load%2A> pour lire un document XML.  
  
```vb  
Dim document As XmlDocument = New XmlDocument()  
document.Load("books.xml")  
```  
  
```csharp  
XmlDocument document = new XmlDocument();  
document.Load("books.xml");  
```  
  
## <a name="determining-the-encoding-of-an-xml-document"></a>Détermination de l'encodage d'un document XML  
 Un objet <xref:System.Xml.XmlReader> peut permettre de lire un document XML et de créer des objets <xref:System.Xml.XPath.XPathDocument> et <xref:System.Xml.XmlDocument> comme expliqué dans les sections précédentes. Toutefois, un objet <xref:System.Xml.XmlReader> peut lire des données non encodées et donc ne fournir aucune information d'encodage.  
  
 La classe <xref:System.Xml.XmlTextReader> hérite de la classe <xref:System.Xml.XmlReader>, fournit des informations d'encodage à l'aide de sa propriété <xref:System.Xml.XmlTextReader.Encoding%2A> et peut permettre de créer un objet <xref:System.Xml.XPath.XPathDocument> ou <xref:System.Xml.XmlDocument>.  
  
 Pour plus d'informations sur les informations d'encodage fournies par la classe <xref:System.Xml.XmlTextReader>, voir la propriété <xref:System.Xml.XmlTextReader.Encoding%2A> dans la documentation de référence sur la classe <xref:System.Xml.XmlTextReader>.  
  
## <a name="creating-xpathnavigator-objects"></a>Création d’objet XPathNavigator  
 Après avoir lu un document XML dans un objet <xref:System.Xml.XPath.XPathDocument> ou <xref:System.Xml.XmlDocument>, vous pouvez créer un objet <xref:System.Xml.XPath.XPathNavigator> pour sélectionner, évaluer, parcourir et, dans certains cas, modifier les données XML sous-jacentes.  
  
 Les classes <xref:System.Xml.XPath.XPathDocument> et <xref:System.Xml.XmlDocument>, en plus de la classe <xref:System.Xml.XmlNode>, implémentent l'interface <xref:System.Xml.XPath.IXPathNavigable> de l'espace de noms <xref:System.Xml.XPath?displayProperty=nameWithType>. Par conséquent, ces trois classes fournissent une méthode <xref:System.Xml.XPath.IXPathNavigable.CreateNavigator%2A> qui retourne un objet <xref:System.Xml.XPath.XPathNavigator>.  
  
### <a name="editing-xml-documents-using-the-xpathnavigator-class"></a>Modification de documents XML à l’aide de la classe XPathNavigator  
 La classe <xref:System.Xml.XPath.XPathNavigator> permet non seulement de sélectionner, d'évaluer et de parcourir des données XML, mais également de modifier un document XML dans certains cas, selon l'objet qui l'a créé.  
  
 La classe <xref:System.Xml.XPath.XPathDocument> est en lecture seule tandis que la classe <xref:System.Xml.XmlDocument> peut être modifiée. Par conséquent, les objets <xref:System.Xml.XPath.XPathNavigator> créés à partir d'un objet <xref:System.Xml.XPath.XPathDocument> ne peuvent pas être utilisés pour modifier un document XML, contrairement à ceux créés par un objet <xref:System.Xml.XmlDocument>. La classe <xref:System.Xml.XPath.XPathDocument> doit être utilisée pour lire un document XML uniquement. Si vous devez modifier un document XML ou accéder à la fonctionnalité supplémentaire fournie par la classe <xref:System.Xml.XmlDocument>, vous devez utiliser la classe <xref:System.Xml.XmlDocument>, de même que pour la gestion des événements.  
  
 La propriété <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> de la classe <xref:System.Xml.XPath.XPathNavigator> spécifie si un objet <xref:System.Xml.XPath.XPathNavigator> peut modifier des données XML.  
  
 Le tableau suivant décrit la valeur de la propriété <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A> pour chaque classe.  
  
|Implémentation <xref:System.Xml.XPath.IXPathNavigable>|Valeur <xref:System.Xml.XPath.XPathNavigator.CanEdit%2A>|  
|--------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Xml.XPath.XPathDocument>|`false`|  
|<xref:System.Xml.XmlDocument>|`true`|  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Xml.XmlDocument>  
 <xref:System.Xml.XPath.XPathDocument>  
 <xref:System.Xml.XPath.XPathNavigator>  
 [Traitement des données XML à l’aide du modèle de données XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)  
 [Accès à des données XML à l’aide de XPathNavigator](../../../../docs/standard/data/xml/accessing-xml-data-using-xpathnavigator.md)  
 [Modification de données XML à l’aide de XPathNavigator](../../../../docs/standard/data/xml/editing-xml-data-using-xpathnavigator.md)  
 [Validation de schéma à l’aide de XPathNavigator](../../../../docs/standard/data/xml/schema-validation-using-xpathnavigator.md)
