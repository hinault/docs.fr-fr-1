---
title: "Remplissage d'un DataSet à partir d'un DataAdapter"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: 3fa0ac7d-e266-4954-bfac-3fbe2f913153
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: c0991398a28e491d381d10dea8a14ed463c67c89
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/17/2018
---
# <a name="populating-a-dataset-from-a-dataadapter"></a>Remplissage d'un DataSet à partir d'un DataAdapter
L’objet [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)]<xref:System.Data.DataSet> est une représentation résidente en mémoire de données, qui propose un modèle de programmation relationnel cohérent, indépendant de la source de données. Le `DataSet` représente un jeu de données complet qui comprend des tables, des contraintes et des relations entre les tables. Étant donné que le `DataSet` est indépendant de la source de données, le `DataSet` peut inclure des données locales par rapport à l'application ainsi que des données provenant de plusieurs sources. L'interaction avec les sources de données existantes est contrôlée par le `DataAdapter`.  
  
 La propriété `SelectCommand` du `DataAdapter` est un objet `Command` qui extrait les données de la source de données. Les propriétés `InsertCommand`, `UpdateCommand`et `DeleteCommand` du `DataAdapter` sont des objets `Command` qui gèrent les mises à jour des données dans la source de données conformément aux modifications apportées dans le `DataSet`. Ces propriétés sont abordées plus en détail dans [mise à jour des Sources de données avec DataAdapters](../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md).  
  
 La méthode `Fill` du `DataAdapter` sert à remplir un `DataSet` avec les résultats de la `SelectCommand` du `DataAdapter`. La méthode`Fill` prend comme arguments un `DataSet` à remplir, ainsi qu'un objet `DataTable` , ou le nom du `DataTable` à remplir avec les lignes retournées par `SelectCommand`.  
  
> [!NOTE]
>  L'utilisation du `DataAdapter` pour extraire une table dans son intégralité prend du temps, particulièrement si la table contient de nombreuses lignes. Cela vient du fait qu'accéder à la base de données, localiser et traiter les données, puis transférer les données au client prend du temps. L'extraction de l'intégralité de la table vers le client verrouille également toutes les lignes sur le serveur. Pour améliorer les performances, vous pouvez utiliser la clause `WHERE` pour réduire drastiquement le nombre de lignes retournées au client. Vous pouvez également réduire la quantité de données retournées au client en répertoriant de façon explicite uniquement les colonnes requises dans l'instruction `SELECT` . Une autre solution de contournement efficace consiste à extraire les lignes par lots, par exemple plusieurs centaines de lignes à la fois, et à extraire le lot suivant uniquement lorsque le client a terminé le traitement du lot actuel.  
  
 La méthode `Fill` utilise l'objet `DataReader` de manière implicite pour retourner les noms et les types de colonnes utilisés pour créer les tables du `DataSet`ainsi que les données pour remplir les lignes des tables du `DataSet`. Les tables et les colonnes ne sont créées que si elles n'existent pas encore ; sinon `Fill` utilise le schéma `DataSet` existant. Types de colonne sont créés en tant que [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] conformément aux tableaux dans les types [des mappages de Type de données dans ADO.NET](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md). Les clés primaires ne sont pas créées, sauf si elles existent dans la source de données et que `DataAdapter`**.**`MissingSchemaAction` a la valeur `MissingSchemaAction`**.**`AddWithKey`. Si `Fill` détecte qu'il existe une clé primaire pour une table, elle remplace les données du `DataSet` par celles de la source de données pour les lignes dont les valeurs de colonne de clé primaire correspondent à celles de la ligne retournée par la source de données. Si aucune clé primaire n'est trouvée, les données sont ajoutées à la table dans le `DataSet`. `Fill`utilise les mappages qui peuvent exister lorsque vous remplissez le `DataSet` (consultez [mappages DataAdapter DataTable et DataColumn](../../../../docs/framework/data/adonet/dataadapter-datatable-and-datacolumn-mappings.md)).  
  
> [!NOTE]
>  Si `SelectCommand` retourne les résultats d'une jointure externe, le `DataAdapter` ne définit pas de valeur `PrimaryKey` pour le `DataTable`obtenu. Vous devez définir vous-même la `PrimaryKey` pour garantir une résolution correcte des lignes dupliquées. Pour plus d’informations, consultez [définition des clés primaires](../../../../docs/framework/data/adonet/dataset-datatable-dataview/defining-primary-keys.md).  
  
 L'exemple de code suivant crée une instance d'un objet <xref:System.Data.SqlClient.SqlDataAdapter> qui utilise un objet <xref:System.Data.SqlClient.SqlConnection> sur la base de données `Northwind` Microsoft SQL Server et remplit un objet <xref:System.Data.DataTable> dans un `DataSet` avec la liste des clients. L'instruction SQL et les arguments <xref:System.Data.SqlClient.SqlConnection> passés au constructeur <xref:System.Data.SqlClient.SqlDataAdapter> sont utilisés pour créer la propriété <xref:System.Data.SqlClient.SqlDataAdapter.SelectCommand%2A> de l'objet <xref:System.Data.SqlClient.SqlDataAdapter>.  
  
## <a name="example"></a>Exemple  
  
```vb  
' Assumes that connection is a valid SqlConnection object.  
Dim queryString As String = _  
  "SELECT CustomerID, CompanyName FROM dbo.Customers"  
Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
  queryString, connection)  
  
Dim customers As DataSet = New DataSet  
adapter.Fill(customers, "Customers")  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection object.  
string queryString =   
  "SELECT CustomerID, CompanyName FROM dbo.Customers";  
SqlDataAdapter adapter = new SqlDataAdapter(queryString, connection);  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
```  
  
> [!NOTE]
>  Ce code n'ouvre pas et ne ferme pas la `Connection`de manière explicite. La méthode `Fill` ouvre implicitement la `Connection` que le `DataAdapter` utilise si la connexion n'est pas déjà ouverte. Si `Fill` a ouvert la connexion, `Fill` la ferme aussi lorsque son exécution est terminée. Cela peut simplifier votre code lorsque vous ne traitez qu'une seule opération comme `Fill` ou `Update`. Cependant, si vous effectuez plusieurs opérations qui nécessitent une connexion ouverte, vous pouvez améliorer les performances de votre application en appelant de manière explicite la méthode `Open` de `Connection`, en effectuant les opérations sur la source de données, puis en appelant la méthode `Close` de `Connection`. Vous devez tenter de réduire autant que possible le temps d'ouverture des connexions à la source de données pour libérer des ressources afin que d'autres applications clientes puissent les utiliser.  
  
## <a name="multiple-result-sets"></a>Jeux de résultats multiples  
 Si le `DataAdapter` détecte plusieurs jeux de résultats, il crée plusieurs tables dans le `DataSet`. Les tables reçoivent un nom incrémentiel par défaut de Table*N*, commençant par « Table » pour Table0. Si un nom de table est passé comme argument à la méthode `Fill` , les tables reçoivent le nom incrémentiel par défaut TableName*N*, commençant par « TableName » pour TableName0.  
  
## <a name="populating-a-dataset-from-multiple-dataadapters"></a>Remplissage d'un DataSet à partir de plusieurs DataAdapters  
 Un nombre quelconque de `DataAdapter` objets peuvent être utilisés avec un `DataSet`. Chaque `DataAdapter` peut être utilisé pour remplir un ou plusieurs objets `DataTable` et répercuter les mises à jour dans la source de données concernée. Les objets`DataRelation` et `Constraint` peuvent être ajoutés localement au `DataSet` , ce qui vous permet de relier des données provenant de sources de données hétérogènes. Par exemple, un `DataSet` peut contenir des données provenant d'une base de données Microsoft SQL Server, d'une base de données IBM DB2 exposée via OLE DB et d'une source de données qui diffuse le XML en continu. Un ou plusieurs objets `DataAdapter` peuvent gérer la communication vers chaque source de données.  
  
### <a name="example"></a>Exemple  
 L'exemple de code suivant remplit une liste de clients provenant de la base de données `Northwind` sur Microsoft SQL Server, ainsi qu'une liste de commandes provenant de la base de données `Northwind` stockée dans Microsoft Access 2000. Les tables remplies sont reliées par un `DataRelation`et la liste des clients est ensuite affichée avec les commandes du client concerné. Pour plus d’informations sur `DataRelation` , consultez [Ajout de DataRelations](../../../../docs/framework/data/adonet/dataset-datatable-dataview/adding-datarelations.md) et [navigation des DataRelations](../../../../docs/framework/data/adonet/dataset-datatable-dataview/navigating-datarelations.md).  
  
```vb  
' Assumes that customerConnection is a valid SqlConnection object.  
' Assumes that orderConnection is a valid OleDbConnection object.  
Dim custAdapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM dbo.Customers", customerConnection)  
  
Dim ordAdapter As OleDbDataAdapter = New OleDbDataAdapter( _  
  "SELECT * FROM Orders", orderConnection)  
  
Dim customerOrders As DataSet = New DataSet()  
custAdapter.Fill(customerOrders, "Customers")  
ordAdapter.Fill(customerOrders, "Orders")  
  
Dim relation As DataRelation = _  
  customerOrders.Relations.Add("CustOrders", _  
  customerOrders.Tables("Customers").Columns("CustomerID"), _   
  customerOrders.Tables("Orders").Columns("CustomerID"))  
  
Dim pRow, cRow As DataRow  
For Each pRow In customerOrders.Tables("Customers").Rows  
  Console.WriteLine(pRow("CustomerID").ToString())  
  
  For Each cRow In pRow.GetChildRows(relation)  
    Console.WriteLine(vbTab & cRow("OrderID").ToString())  
  Next  
Next  
```  
  
```csharp  
// Assumes that customerConnection is a valid SqlConnection object.  
// Assumes that orderConnection is a valid OleDbConnection object.  
SqlDataAdapter custAdapter = new SqlDataAdapter(  
  "SELECT * FROM dbo.Customers", customerConnection);  
OleDbDataAdapter ordAdapter = new OleDbDataAdapter(  
  "SELECT * FROM Orders", orderConnection);  
  
DataSet customerOrders = new DataSet();  
  
custAdapter.Fill(customerOrders, "Customers");  
ordAdapter.Fill(customerOrders, "Orders");  
  
DataRelation relation = customerOrders.Relations.Add("CustOrders",  
  customerOrders.Tables["Customers"].Columns["CustomerID"],  
  customerOrders.Tables["Orders"].Columns["CustomerID"]);  
  
foreach (DataRow pRow in customerOrders.Tables["Customers"].Rows)  
{  
  Console.WriteLine(pRow["CustomerID"]);  
   foreach (DataRow cRow in pRow.GetChildRows(relation))  
    Console.WriteLine("\t" + cRow["OrderID"]);  
}  
```  
  
## <a name="sql-server-decimal-type"></a>Type décimal SQL Server  
 Par défaut, le `DataSet` stocke les données à l'aide de types de données [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] . Pour la plupart des applications, ils fournissent une représentation pratique des informations de la source de données. Cette représentation peut néanmoins poser un problème lorsque le type de données dans la source de données est un decimal SQL Server ou un type de données numérique. Le type de données [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] `decimal` autorise un nombre maximal de 28 chiffres significatifs, tandis que le type de données `decimal` SQL Server en autorise 38. Si `SqlDataAdapter` détermine pendant une opération `Fill` que la précision d'un champ `decimal` SQL Server est supérieure à 28 caractères, la ligne actuelle n'est pas ajoutée au `DataTable`. Au lieu de cela, l'événement `FillError` se produit, ce qui vous permet de déterminer une éventuelle perte de précision et de répondre de manière appropriée. Pour plus d’informations sur la `FillError` événements, consultez [gestion des événements DataAdapter](../../../../docs/framework/data/adonet/handling-dataadapter-events.md). Pour obtenir la valeur `decimal` SQL Server, vous pouvez également utiliser un objet <xref:System.Data.SqlClient.SqlDataReader> et appeler la méthode <xref:System.Data.SqlClient.SqlDataReader.GetSqlDecimal%2A> .  
  
 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 2.0 a introduit une prise en charge avancée de <xref:System.Data.SqlTypes> dans le `DataSet`. Pour plus d'informations, consultez [SqlTypes and the DataSet](../../../../docs/framework/data/adonet/sql/sqltypes-and-the-dataset.md).  
  
## <a name="ole-db-chapters"></a>Chapitres OLE DB  
 Les jeux de lignes hiérarchiques ou chapitres (`DBTYPE_HCHAPTER` de type OLE DB, `adChapter` de type ADO) peuvent être utilisés pour remplir le contenu d'un `DataSet`. Lorsque l'objet <xref:System.Data.OleDb.OleDbDataAdapter> rencontre une colonne chapitre pendant une opération `Fill` , un `DataTable` est créé pour cette colonne et la table correspondante est remplie avec les colonnes et les lignes provenant du chapitre. La table créée pour la colonne chapitre est nommée à l'aide des noms de la table parente et de la colonne chapitre sous la forme «*ParentTableNameChapteredColumnName*». Si une table correspondant au nom de la colonne chapitre existe déjà dans le `DataSet` , la table actuelle est remplie avec les données du chapitre. S'il n'y a pas de colonne, dans une table existante, qui corresponde à une colonne trouvée dans le chapitre, une nouvelle colonne est ajoutée.  
  
 Avant que les tables du `DataSet` ne soient remplies avec les données des colonnes chapitres, une relation est créée entre les tables parent et enfant du jeu de lignes hiérarchique par l'ajout d'une colonne d'entiers aux deux tables, la définition de l'incrémentation automatique de la colonne parente et la création d'un `DataRelation` à l'aide des colonnes ajoutées des deux tables. La relation ajoutée est nommée à l'aide des noms de table parente et de colonne chapitre sous la forme «*ParentTableNameChapterColumnName*».  
  
 Notez que la colonne associée n'existe que dans le `DataSet`. Les remplissages suivants à partir de la source de données peuvent engendrer l'ajout de nouvelles lignes aux tables plutôt que la fusion des modifications dans les lignes existantes.  
  
 Notez par ailleurs que si vous utilisez la surcharge `DataAdapter.Fill` qui prend un `DataTable`, seule cette table sera remplie. Une colonne entier auto-incrémentée sera toujours ajoutée à la table mais aucune table enfant ne sera créée ni remplie et aucune relation ne sera créée.  
  
 L'exemple suivant utilise le fournisseur MSDataShape pour générer une colonne chapitre de commandes pour chaque client d'une liste de clients. Un `DataSet` est alors rempli avec les données.  
  
```vb  
Using connection As OleDbConnection = New OleDbConnection( _  
  "Provider=MSDataShape;Data Provider=SQLOLEDB;" & _  
  "Data Source=(local);Integrated " & _  
  "Security=SSPI;Initial Catalog=northwind")  
  
Dim adapter As OleDbDataAdapter = New OleDbDataAdapter( _  
  "SHAPE {SELECT CustomerID, CompanyName FROM Customers} " & _  
  "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS Orders " & _  
  "RELATE CustomerID TO CustomerID)", connection)  
  
Dim customers As DataSet = New DataSet()  
  
adapter.Fill(customers, "Customers")  
End Using  
```  
  
```csharp  
using (OleDbConnection connection = new OleDbConnection("Provider=MSDataShape;Data Provider=SQLOLEDB;" +  
  "Data Source=(local);Integrated Security=SSPI;Initial Catalog=northwind"))  
{  
OleDbDataAdapter adapter = new OleDbDataAdapter("SHAPE {SELECT CustomerID, CompanyName FROM Customers} " +  
  "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS Orders " +  
  "RELATE CustomerID TO CustomerID)", connection);  
  
DataSet customers = new DataSet();  
adapter.Fill(customers, "Customers");  
}  
```  
  
 Une fois l'opération `Fill` terminée, le `DataSet` contient deux tables : `Customers` et `CustomersOrders`, où `CustomersOrders` représente la colonne chapitre. Une colonne supplémentaire nommée `Orders` est ajoutée à la table `Customers` et une colonne supplémentaire nommée `CustomersOrders` est ajoutée à la table `CustomersOrders` . L'incrémentation automatique de la colonne `Orders` dans la table `Customers` est définie. Un `DataRelation`, `CustomersOrders`, est créé avec les colonnes ajoutées aux tables, `Customers` étant la table parente. Les tableaux suivants présentent certains résultats de l'exemple.  
  
### <a name="tablename-customers"></a>TableName: Customers  
  
|CustomerID|CompanyName|Orders|  
|----------------|-----------------|------------|  
|ALFKI|Alfreds Futterkiste|0|  
|ANATR|Ana Trujillo Emparedados y helados|1|  
  
### <a name="tablename-customersorders"></a>TableName: CustomersOrders  
  
|CustomerID|OrderID|CustomersOrders|  
|----------------|-------------|---------------------|  
|ALFKI|10643|0|  
|ALFKI|10692|0|  
|ANATR|10308|1|  
|ANATR|10625|1|  
  
## <a name="see-also"></a>Voir aussi  
 [DataAdapters et DataReaders](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)  
 [Mappages de types de données dans ADO.NET](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md)  
 [Modification des données avec un DbDataAdapter](../../../../docs/framework/data/adonet/modifying-data-with-a-dbdataadapter.md)  
 [MARS (Multiple Active Result Sets)](../../../../docs/framework/data/adonet/sql/multiple-active-result-sets-mars.md)  
 [Fournisseurs managés ADO.NET et centre de développement DataSet](http://go.microsoft.com/fwlink/?LinkId=217917)
