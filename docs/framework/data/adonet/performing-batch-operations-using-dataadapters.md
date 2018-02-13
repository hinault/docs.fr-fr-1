---
title: "Exécution d'opérations en lot à l'aide des DataAdapter"
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
ms.assetid: e72ed5af-b24f-486c-8429-c8fd2208f844
caps.latest.revision: "3"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: e5c584bcd825e390b24da6c95ecb159a8280c639
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/17/2018
---
# <a name="performing-batch-operations-using-dataadapters"></a>Exécution d'opérations en lot à l'aide des DataAdapter
La prise en charge des lots dans ADO.NET permet à un objet <xref:System.Data.Common.DataAdapter> de grouper des opérations INSERT, UPDATE et DELETE à partir d'un objet <xref:System.Data.DataSet> ou d'un objet <xref:System.Data.DataTable> pour le serveur, au lieu d'envoyer les opérations successivement. La réduction du nombre d'allers-retours vers le serveur entraîne généralement des gains de performances importants. Les mises à jour par lots sont prises en charge pour les fournisseurs de données .NET pour SQL Server (<xref:System.Data.SqlClient>) et Oracle (<xref:System.Data.OracleClient>).  
  
 Lors de la mise à jour d'une base de données avec les modifications d'un objet <xref:System.Data.DataSet> dans les versions précédentes d'ADO.NET, la méthode `Update` d'un objet `DataAdapter` apportait des mises à jour à la base de données ligne après ligne. Comme elle effectuait une itération dans les lignes de l'objet <xref:System.Data.DataTable> spécifié, elle examinait chaque objet <xref:System.Data.DataRow> pour voir s'il avait été modifié. Si la ligne avait été modifiée, elle appelait `UpdateCommand`, `InsertCommand` ou `DeleteCommand` en fonction de la valeur de la propriété <xref:System.Data.DataRow.RowState%2A> de cette ligne. Chaque mise à jour de ligne impliquait un aller-retour sur le réseau vers la base de données.  
  
 À partir d'ADO.NET 2.0, <xref:System.Data.Common.DbDataAdapter> expose une propriété <xref:System.Data.Common.DbDataAdapter.UpdateBatchSize%2A>. L'affection d'une valeur entière positive à la propriété `UpdateBatchSize` a pour effet d'envoyer les mises à jour de la base de données sous la forme de lots de la taille spécifiée. Par exemple, l'affectation de la valeur 10 à la propriété `UpdateBatchSize` groupe 10 instructions distinctes avant de les soumettre en tant que lot. Avec `UpdateBatchSize`la valeur 0<xref:System.Data.Common.DataAdapter>, l'objet utilise la taille de lot la plus grande que le serveur peut gérer. La valeur 1 désactive les mises à jour par lots car les lignes sont envoyées les unes après les autres.  
  
 L'exécution d'un lot très volumineux peut réduire les performances. Vous devez donc tester le paramètre de taille de lot optimal avant d'implémenter votre application.  
  
## <a name="using-the-updatebatchsize-property"></a>Utilisation de la propriété UpdateBatchSize  
 Lorsque les mises à jour par lots sont activées, la valeur <xref:System.Data.IDbCommand.UpdatedRowSource%2A> ou `UpdateCommand` doit être affectée à la propriété `InsertCommand` de `DeleteCommand`, <xref:System.Data.UpdateRowSource.None> et <xref:System.Data.UpdateRowSource.OutputParameters> du DataAdapter. Lors de l'exécution d'une mise à jour par lots, les valeurs <xref:System.Data.IDbCommand.UpdatedRowSource%2A> ou <xref:System.Data.UpdateRowSource.FirstReturnedRecord> de la propriété <xref:System.Data.UpdateRowSource.Both> de la commande ne sont pas valides.  
  
 La procédure suivante illustre l'utilisation de la propriété `UpdateBatchSize`. La procédure prend deux arguments, un <xref:System.Data.DataSet> objet comportant des colonnes représentant la **ProductCategoryID** et **nom** champs dans le **Production.ProductCategory**table et un entier qui représente la taille de lot (le nombre de lignes dans le lot). Le code crée un nouvel objet <xref:System.Data.SqlClient.SqlDataAdapter>, en définissant ses propriétés <xref:System.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A>, <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> et <xref:System.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A>. Le code est basé sur l'hypothèse que l'objet <xref:System.Data.DataSet> comporte des lignes modifiées. Il définit la propriété `UpdateBatchSize` et effectue la mise à jour.  
  
```vb  
Public Sub BatchUpdate( _  
  ByVal dataTable As DataTable, ByVal batchSize As Int32)  
    ' Assumes GetConnectionString() returns a valid connection string.  
    Dim connectionString As String = GetConnectionString()  
  
    ' Connect to the AdventureWorks database.  
    Using connection As New SqlConnection(connectionString)  
        ' Create a SqlDataAdapter.  
        Dim adapter As New SqlDataAdapter()  
  
        'Set the UPDATE command and parameters.  
        adapter.UpdateCommand = New SqlCommand( _  
          "UPDATE Production.ProductCategory SET " _  
          & "Name=@Name WHERE ProductCategoryID=@ProdCatID;", _  
          connection)  
        adapter.UpdateCommand.Parameters.Add("@Name", _  
          SqlDbType.NVarChar, 50, "Name")  
        adapter.UpdateCommand.Parameters.Add("@ProdCatID",  _  
          SqlDbType.Int, 4, " ProductCategoryID ")  
        adapter.UpdateCommand.UpdatedRowSource = _  
          UpdateRowSource.None  
  
        'Set the INSERT command and parameter.  
        adapter.InsertCommand = New SqlCommand( _  
          "INSERT INTO Production.ProductCategory (Name) VALUES (@Name);", _  
  connection)  
        adapter.InsertCommand.Parameters.Add("@Name", _  
          SqlDbType.NVarChar, 50, "Name")  
        adapter.InsertCommand.UpdatedRowSource = _  
          UpdateRowSource.None  
  
        'Set the DELETE command and parameter.  
        adapter.DeleteCommand = New SqlCommand( _  
          "DELETE FROM Production.ProductCategory " _  
          & "WHERE ProductCategoryID=@ProdCatID;", connection)  
        adapter.DeleteCommand.Parameters.Add("@ProdCatID", _  
           SqlDbType.Int, 4, " ProductCategoryID ")  
        adapter.DeleteCommand.UpdatedRowSource = UpdateRowSource.None  
  
        ' Set the batch size.  
        adapter.UpdateBatchSize = batchSize  
  
        ' Execute the update.  
        adapter.Update(dataTable)  
    End Using  
End Sub  
```  
  
```csharp  
public static void BatchUpdate(DataTable dataTable,Int32 batchSize)  
{  
    // Assumes GetConnectionString() returns a valid connection string.  
    string connectionString = GetConnectionString();  
  
    // Connect to the AdventureWorks database.  
    using (SqlConnection connection = new   
      SqlConnection(connectionString))  
    {  
  
        // Create a SqlDataAdapter.  
        SqlDataAdapter adapter = new SqlDataAdapter();  
  
        // Set the UPDATE command and parameters.  
        adapter.UpdateCommand = new SqlCommand(  
            "UPDATE Production.ProductCategory SET "  
            + "Name=@Name WHERE ProductCategoryID=@ProdCatID;",   
            connection);  
        adapter.UpdateCommand.Parameters.Add("@Name",   
           SqlDbType.NVarChar, 50, "Name");  
        adapter.UpdateCommand.Parameters.Add("@ProdCatID",   
           SqlDbType.Int, 4, "ProductCategoryID");  
         adapter.UpdateCommand.UpdatedRowSource = UpdateRowSource.None;  
  
        // Set the INSERT command and parameter.  
        adapter.InsertCommand = new SqlCommand(  
            "INSERT INTO Production.ProductCategory (Name) VALUES (@Name);",   
            connection);  
        adapter.InsertCommand.Parameters.Add("@Name",   
          SqlDbType.NVarChar, 50, "Name");  
        adapter.InsertCommand.UpdatedRowSource = UpdateRowSource.None;  
  
        // Set the DELETE command and parameter.  
        adapter.DeleteCommand = new SqlCommand(  
            "DELETE FROM Production.ProductCategory "  
            + "WHERE ProductCategoryID=@ProdCatID;", connection);  
        adapter.DeleteCommand.Parameters.Add("@ProdCatID",   
          SqlDbType.Int, 4, "ProductCategoryID");  
        adapter.DeleteCommand.UpdatedRowSource = UpdateRowSource.None;  
  
        // Set the batch size.  
        adapter.UpdateBatchSize = batchSize;  
  
        // Execute the update.  
        adapter.Update(dataTable);  
    }  
}  
```  
  
## <a name="handling-batch-update-related-events-and-errors"></a>Gestion des événements et des erreurs liés aux mises à jour par lots.  
 Le **DataAdapter** comporte deux événements liés à la mise à jour : **RowUpdating** et **RowUpdated**. Dans les versions précédentes d'ADO.NET, en cas de désactivation du traitement par lots, chacun de ces événements était généré une fois pour chaque ligne traitée. **RowUpdating** est généré avant la mise à jour se produit, et **RowUpdated** est généré après la mise à jour de la base de données a été effectuée.  
  
### <a name="event-behavior-changes-with-batch-updates"></a>Changements de comportement d'événement avec les mises à jour par lots  
 Lorsque le traitement par lots est activé, plusieurs lignes sont mises à jour en une seule opération de base de données. Par conséquent, un seul événement `RowUpdated` se produit pour chaque lot, tandis que l'événement `RowUpdating` se produit pour chaque ligne traitée. Lorsque le traitement par lots est désactivé, les deux événements sont déclenchés avec un entrelacement de un à un où un événement `RowUpdating` et un événement `RowUpdated` se déclenchent pour une ligne, puis un événement `RowUpdating` et un événement `RowUpdated` se déclenchent pour la ligne suivante, jusqu'à ce que toutes les lignes aient été traitées.  
  
### <a name="accessing-updated-rows"></a>Accès aux lignes mises à jour  
 Lorsque le traitement par lots est désactivé, la ligne mise à jour est accessible à l'aide de la propriété <xref:System.Data.Common.RowUpdatedEventArgs.Row%2A> de la classe <xref:System.Data.Common.RowUpdatedEventArgs>.  
  
 Lorsque le traitement par lots est activé, un simple événement `RowUpdated` est généré pour plusieurs lignes. C'est pourquoi la valeur de la propriété `Row` pour chaque ligne est null. Des événements `RowUpdating` sont encore générés pour chaque ligne. La méthode <xref:System.Data.Common.RowUpdatedEventArgs.CopyToRows%2A> de la classe <xref:System.Data.Common.RowUpdatedEventArgs> permet d'accéder aux lignes traitées en copiant les références aux lignes dans un tableau. Si aucune ligne n'est traitée, `CopyToRows` lève une exception <xref:System.ArgumentNullException>. Utilisez la propriété <xref:System.Data.Common.RowUpdatedEventArgs.RowCount%2A> pour retourner le nombre de lignes traitées avant d'appeler la méthode <xref:System.Data.Common.RowUpdatedEventArgs.CopyToRows%2A>.  
  
### <a name="handling-data-errors"></a>Gestion des erreurs de données  
 L'exécution par lots a le même effet que l'exécution des instructions individuelles. Les instructions sont exécutées dans l'ordre où elles ont été ajoutées au lot. Les erreurs sont gérées de la même manière, que le mode de traitement par lots soit activé ou non. Chaque ligne est traitée séparément. Seules les lignes traitées avec succès dans la base de données sont mises à jour dans l'objet <xref:System.Data.DataRow> correspondant à l'objet <xref:System.Data.DataTable>.  
  
 Le fournisseur de données et le serveur de base de données principal déterminent les constructions SQL prises en charge pour l'exécution par lots. Une exception peut être levée si une instruction non prise en charge est soumise pour exécution.  
  
## <a name="see-also"></a>Voir aussi  
 [DataAdapters et DataReaders](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)  
 [Mise à jour de sources de données avec des DataAdapters](../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md)  
 [Gestion des événements DataAdapter](../../../../docs/framework/data/adonet/handling-dataadapter-events.md)  
 [Fournisseurs managés ADO.NET et centre de développement DataSet](http://go.microsoft.com/fwlink/?LinkId=217917)
