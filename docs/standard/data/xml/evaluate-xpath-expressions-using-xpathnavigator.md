---
title: "Évaluation d’expressions XPath à l’aide de XPathNavigator"
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
ms.assetid: 2913ccf3-f932-4363-8028-9e2d22ce6093
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 4d4515b8ebea338a153319dfd02eab8d389b843b
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="evaluate-xpath-expressions-using-xpathnavigator"></a>Évaluation d’expressions XPath à l’aide de XPathNavigator
La classe <xref:System.Xml.XPath.XPathNavigator> fournit la méthode <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> permettant d'évaluer une expression XPath. La méthode <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> prend une expression XPath, l'évalue et retourne le type XPath W3C booléen, nombre, chaîne ou collection de nœuds selon le résultat de l'expression XPath.  
  
## <a name="the-evaluate-method"></a>Méthode d'évaluation  
 La méthode <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> prend une expression XPath, l'évalue et retourne un résultat typé tel que booléen (<xref:System.Boolean>), nombre (<xref:System.Double>), chaîne (<xref:System.String>) ou collection de nœuds (<xref:System.Xml.XPath.XPathNodeIterator>). Par exemple, la méthode <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> peut être utilisée dans une méthode mathématique. L'exemple de code suivant calcule le prix total de tous les livres du fichier `books.xml`.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
Dim query As XPathExpression = navigator.Compile("sum(//price/text())")  
Dim total As Double = CType(navigator.Evaluate(query), Double)  
Console.WriteLine(total)  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
XPathExpression query = navigator.Compile("sum(//price/text())");  
Double total = (Double)navigator.Evaluate(query);  
Console.WriteLine(total);  
```  
  
 L'exemple prend le fichier `books.xml` comme entrée.  
  
 [!code-xml[XPathXMLExamples#1](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/books.xml#1)]  
  
### <a name="position-and-last-functions"></a>Fonctions position et last  
 La méthode <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> est surchargée. L'une des méthodes <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> prend un objet <xref:System.Xml.XPath.XPathNodeIterator> comme paramètre. Cette méthode <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> particulière est identique à la méthode <xref:System.Xml.XPath.XPathNavigator.Evaluate%2A> qui ne prend qu'un objet <xref:System.Xml.XPath.XPathExpression> comme paramètre, si ce n'est qu'elle permet à un argument node set de spécifier le contexte actuel sur lequel effectuer l'évaluation. Ce contexte est obligatoire pour les fonctions XPath `position()` et `last()` car celles-ci se rapportent au nœud de contexte actuel. À moins d'être utilisées comme prédicats dans une étape de localisation, l'évaluation des fonctions `position()` et `last()` nécessite une référence à une collection de nœuds, sinon les fonctions `position` et `last` retournent `0`.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Xml.XmlDocument>  
 <xref:System.Xml.XPath.XPathDocument>  
 <xref:System.Xml.XPath.XPathNavigator>  
 [Traitement des données XML à l’aide du modèle de données XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)  
 [Sélection de données XML à l’aide de XPathNavigator](../../../../docs/standard/data/xml/select-xml-data-using-xpathnavigator.md)  
 [Mise en correspondance de nœuds avec XPathNavigator](../../../../docs/standard/data/xml/matching-nodes-using-xpathnavigator.md)  
 [Types de nœuds reconnus avec les requêtes XPath](../../../../docs/standard/data/xml/node-types-recognized-with-xpath-queries.md)  
 [Requêtes et espaces de noms XPath](../../../../docs/standard/data/xml/xpath-queries-and-namespaces.md)  
 [Expressions XPath compilées](../../../../docs/standard/data/xml/compiled-xpath-expressions.md)
