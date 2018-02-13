---
title: "Extraction de données XML à l’aide de XPathNavigator"
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
ms.assetid: 095b0987-ee4b-4595-a160-da1c956ad576
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: f80c21e7809e5b088582a51d9085a187bccae444
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="extract-xml-data-using-xpathnavigator"></a>Extraction de données XML à l’aide de XPathNavigator
Il existe différentes manières de représenter un document XML dans Microsoft .NET Framework. Ce peut être à l'aide d'une chaîne (<xref:System.String>) ou des classes <xref:System.Xml.XmlReader>, <xref:System.Xml.XmlWriter>, <xref:System.Xml.XmlDocument> ou <xref:System.Xml.XPath.XPathDocument>. Pour faciliter les déplacements entre ces différentes représentations d'un document XML, la classe <xref:System.Xml.XPath.XPathNavigator> offre diverses méthodes et propriétés d'extraction du XML en tant qu'objet <xref:System.String>, <xref:System.Xml.XmlReader> ou <xref:System.Xml.XmlWriter>.  
  
## <a name="convert-an-xpathnavigator-to-a-string"></a>Conversion d'un objet XPathNavigator en une chaîne  
 La propriété <xref:System.Xml.XPath.XPathNavigator.OuterXml%2A> de la classe <xref:System.Xml.XPath.XPathNavigator> permet d'obtenir le balisage de l'entièreté du document XML ou d'un seul nœud et de ses nœuds enfants.  
  
> [!NOTE]
>  La propriété <xref:System.Xml.XPath.XPathNavigator.InnerXml%2A> n'obtient le balisage que des nœuds enfants d'un nœud.  
  
 L'exemple de code suivant montre comment enregistrer en tant qu'objet <xref:System.Xml.XPath.XPathNavigator> l'entièreté d'un document XML contenu dans un objet <xref:System.String>, de même qu'un nœud unique et ses nœuds enfants.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("input.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Save the entire input.xml document to a string.  
Dim xml As String = navigator.OuterXml  
  
' Now save the Root element and its child nodes to a string.  
navigator.MoveToChild(XPathNodeType.Element)  
Dim root As String = navigator.OuterXml  
```  
  
```csharp  
XPathDocument document = new XPathDocument("input.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Save the entire input.xml document to a string.  
string xml = navigator.OuterXml;  
  
// Now save the Root element and its child nodes to a string.  
navigator.MoveToChild(XPathNodeType.Element);  
string root = navigator.OuterXml;  
```  
  
## <a name="convert-an-xpathnavigator-to-an-xmlreader"></a>Conversion d’un objet XPathNavigator en un objet XmlReader  
 La méthode <xref:System.Xml.XPath.XPathNavigator.ReadSubtree%2A> permet de transmettre l'ensemble du contenu d'un document XML ou un seul nœud et ses nœuds enfants à un objet <xref:System.Xml.XmlReader>.  
  
 Lorsque l'objet <xref:System.Xml.XmlReader> est créé avec le nœud actuel et ses nœuds enfants, la propriété <xref:System.Xml.XmlReader> de l'objet <xref:System.Xml.XmlReader.ReadState%2A> est définie sur <xref:System.Xml.ReadState.Initial>. Lorsque la méthode <xref:System.Xml.XmlReader> de l'objet <xref:System.Xml.XmlReader.Read%2A> est appelée pour la première fois, le <xref:System.Xml.XmlReader> est déplacé vers le nœud actuel du <xref:System.Xml.XPath.XPathNavigator>. Le nouvel objet <xref:System.Xml.XmlReader> poursuit la lecture jusqu'à la fin de l'arborescence XML. À ce stade, la méthode <xref:System.Xml.XmlReader.Read%2A> retourne `false` et la propriété <xref:System.Xml.XmlReader> de l'objet <xref:System.Xml.XmlReader.ReadState%2A> est définie sur <xref:System.Xml.ReadState.EndOfFile>.  
  
 La position de l'objet <xref:System.Xml.XPath.XPathNavigator> n'est pas modifiée par la création ou le déplacement de l'objet <xref:System.Xml.XmlReader>. La méthode <xref:System.Xml.XPath.XPathNavigator.ReadSubtree%2A> n'est valide que lorsque vous êtes positionné sur un élément ou un nœud racine.  
  
 L'exemple suivant montre comment obtenir un objet <xref:System.Xml.XmlReader> contenant l'entièreté du document XML dans un objet <xref:System.Xml.XPath.XPathDocument>, de même qu'un nœud unique et ses nœuds enfants.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Stream the entire XML document to the XmlReader.  
Dim xml As XmlReader = navigator.ReadSubtree()  
  
While xml.Read()  
    Console.WriteLine(xml.ReadInnerXml())  
End While  
  
xml.Close()  
  
' Stream the book element and its child nodes to the XmlReader.  
navigator.MoveToChild("bookstore", "")  
navigator.MoveToChild("book", "")  
  
Dim book As XmlReader = navigator.ReadSubtree()  
  
While book.Read()  
    Console.WriteLine(book.ReadInnerXml())  
End While  
  
book.Close()  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Stream the entire XML document to the XmlReader.  
XmlReader xml = navigator.ReadSubtree();  
  
while (xml.Read())  
{  
    Console.WriteLine(xml.ReadInnerXml());  
}  
  
xml.Close();  
  
// Stream the book element and its child nodes to the XmlReader.  
navigator.MoveToChild("bookstore", "");  
navigator.MoveToChild("book", "");  
  
XmlReader book = navigator.ReadSubtree();  
  
while (book.Read())  
{  
    Console.WriteLine(book.ReadInnerXml());  
}  
  
book.Close();  
```  
  
 L'exemple prend le fichier `books.xml` comme entrée.  
  
 [!code-xml[XPathXMLExamples#1](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/books.xml#1)]  
  
## <a name="converting-an-xpathnavigator-to-an-xmlwriter"></a>Conversion d’un objet XPathNavigator en un objet XmlWriter  
 La méthode <xref:System.Xml.XPath.XPathNavigator.WriteSubtree%2A> permet de transmettre l'ensemble du contenu d'un document XML ou un seul nœud et ses nœuds enfants à un objet <xref:System.Xml.XmlWriter>.  
  
 La position de l'objet <xref:System.Xml.XPath.XPathNavigator> n'est pas modifiée par la création de l'objet <xref:System.Xml.XmlWriter>.  
  
 L'exemple suivant montre comment obtenir un objet <xref:System.Xml.XmlWriter> contenant l'entièreté du document XML dans un objet <xref:System.Xml.XPath.XPathDocument>, de même qu'un nœud unique et ses nœuds enfants.  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
  
' Stream the entire XML document to the XmlWriter.  
Dim xml As XmlWriter = XmlWriter.Create("newbooks.xml")  
navigator.WriteSubtree(xml)  
xml.Close()  
  
' Stream the book element and its child nodes to the XmlWriter.  
navigator.MoveToChild("bookstore", "")  
navigator.MoveToChild("book", "")  
  
Dim book As XmlWriter = XmlWriter.Create("book.xml")  
navigator.WriteSubtree(book)  
book.Close()  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
  
// Stream the entire XML document to the XmlWriter.  
XmlWriter xml = XmlWriter.Create("newbooks.xml");  
navigator.WriteSubtree(xml);  
xml.Close();  
  
// Stream the book element and its child nodes to the XmlWriter.  
navigator.MoveToChild("bookstore", "");  
navigator.MoveToChild("book", "");  
  
XmlWriter book = XmlWriter.Create("book.xml");  
navigator.WriteSubtree(book);  
book.Close();  
```  
  
 L'exemple prend comme entrée le fichier `books.xml` mentionné précédemment dans cette rubrique.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Xml.XmlDocument>  
 <xref:System.Xml.XPath.XPathDocument>  
 <xref:System.Xml.XPath.XPathNavigator>  
 [Traitement des données XML à l’aide du modèle de données XPath](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)  
 [Navigation dans la collection de nœuds à l’aide de XPathNavigator](../../../../docs/standard/data/xml/node-set-navigation-using-xpathnavigator.md)  
 [Navigation entre les nœuds d’attribut et d’espace de noms à l’aide de XPathNavigator](../../../../docs/standard/data/xml/attribute-and-namespace-node-navigation-using-xpathnavigator.md)  
 [Accès à des données XML fortement typées à l’aide de XPathNavigator](../../../../docs/standard/data/xml/accessing-strongly-typed-xml-data-using-xpathnavigator.md)
