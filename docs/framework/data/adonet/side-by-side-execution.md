---
title: "Exécution côte à côte dans ADO.NET"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9f9ba96d-9f89-4f65-bb2f-6860879f4393
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: bdb12ce6f697bbc42052e35c252c9cad6a5e962e
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/17/2018
---
# <a name="side-by-side-execution-in-adonet"></a>Exécution côte à côte dans ADO.NET
L'exécution côte à côte dans le [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] représente la capacité à exécuter une application sur un ordinateur sur lequel plusieurs versions du[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] sont installées, en utilisant exclusivement la version pour laquelle l'application a été compilée. Pour plus d’informations sur la configuration de l’exécution de côte à côte, consultez [côte-à-côte exécution](../../../../docs/framework/deployment/side-by-side-execution.md).  
  
 Une application compilée en utilisant une version du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] peut s'exécuter sur une autre version du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]. Toutefois, nous vous conseillons de compiler une version de l'application pour chaque version du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] installée et de les exécuter séparément. Dans l'un ou l'autre cas de figure, vous devez tenir compte des modifications apportées dans [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] entre les versions, qui peuvent affecter la compatibilité ascendante ou descendante de votre application.  
  
## <a name="forward-compatibility-and-backward-compatibility"></a>Compatibilités descendante et ascendante  
 La compatibilité ascendante signifie qu'une application peut être compilée avec une version antérieure du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] et qu'elle fonctionnera correctement avec une version ultérieure du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]. Le code [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] écrit pour le [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] version 1.1 sera compatible avec les versions ultérieures.  
  
 La compatibilité descendante signifie qu'une application est compilée pour une version plus récente du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] et qu'elle continue de s'exécuter sur des versions antérieures de la [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] sans dégradation des fonctionnalités. Évidemment, ce ne sera pas le cas pour les fonctions introduites dans une nouvelle version du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].  
  
## <a name="the-net-framework-data-provider-for-odbc"></a>Fournisseur de données .NET Framework pour ODBC  
 Le fournisseur de données [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] pour ODBC (<xref:System.Data.Odbc>), à partir de la version 1.1, fait partie intégrante du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]. Le fournisseur de données ODBC est disponible pour [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] téléchargement des développeurs de la version 1.0 comme un site Web à partir de la [accès aux données et le centre de développement](http://go.microsoft.com/fwlink/?linkid=4173). L’espace de noms téléchargé [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] fournisseur de données pour ODBC est **Microsoft.Data.Odbc**.  
  
 Si vous avez une application développée pour la [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] version 1.0 utilise le fournisseur de données ODBC pour se connecter à votre source de données et que vous voulez exécuter cette application sur le [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] version 1.1 ou une version ultérieure, vous devez mettre à jour l’espace de noms pour ODBC fournisseur de données de **System.Data.Odbc**. Vous devez ensuite le recompiler pour la version plus récente du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].  
  
 Si une application développée pour la version 2.0 ou ultérieure du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] utilise le fournisseur de données ODBC pour se connecter à votre source de données alors que vous voulez exécuter cette application sur la version 1.0 du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], vous devez télécharger le fournisseur de données ODBC et l'installer sur le système [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] version 1.0. Vous devez ensuite modifier l’espace de noms pour le fournisseur de données ODBC à **Microsoft.Data.Odbc**et recompiler l’application pour le [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] version 1.0.  
  
## <a name="the-net-framework-data-provider-for-oracle"></a>Fournisseur de données .NET Framework pour Oracle  
 Le fournisseur de données [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] pour Oracle (<xref:System.Data.OracleClient>), à partir de la version 1.1, fait partie intégrante du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]. Le fournisseur de données est disponible pour [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] téléchargement des développeurs de la version 1.0 comme un site Web à partir de la [accès aux données et le centre de développement](http://go.microsoft.com/fwlink/?linkid=4173).  
  
 Si vous avez une application développée pour la [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] version 2.0 ou ultérieure qui utilise le fournisseur de données pour se connecter à votre source de données et que vous voulez exécuter cette application sur le [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] version 1.0, vous devez télécharger le fournisseur de données et l’installer sur le < C4 > [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]  système version 1.0.  
  
## <a name="code-access-security"></a>Sécurité d'accès du code  
 Les fournisseurs de données [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] contenus dans la version 1.0 du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] (<xref:System.Data.SqlClient>, <xref:System.Data.OleDb>) doivent être exécutés avec l'autorisation FullTrust (confiance totale). Toute tentative d’utiliser le [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] fournisseurs de données à partir de la [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] version 1.0 dans une zone comportant moins de causes d’autorisation FullTrust un <xref:System.Security.SecurityException>.  
  
 Toutefois, avec la version 2.0 du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], tous les fournisseurs de données [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] peuvent être utilisés dans des zones de confiance partielle. En outre, une nouvelle fonction de sécurité a été ajoutée aux fournisseurs de données [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] dans la version 1.1 du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]. Cette fonction vous permet de restreindre les chaînes de connexion qui peuvent être utilisées dans une zone de sécurité particulière. Vous pouvez également désactiver l'utilisation des mots de passe vides pour une zone de sécurité particulière. Pour plus d'informations, consultez [Code Access Security and ADO.NET](../../../../docs/framework/data/adonet/code-access-security.md).  
  
 Dans la mesure où chaque installation du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] possède un fichier Security.config distinct, il n'existe pas de problème de compatibilité ascendante ou descendante avec les paramètres de sécurité. Toutefois, si votre application dépend des fonctionnalités de sécurité supplémentaires de [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] incluses dans le [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] version 1.1 et ultérieure, vous ne pourrez pas la distribuer sur un système doté d'une version 1.0.  
  
## <a name="sqlcommand-execution"></a>Exécution de SqlCommand  
 À partir de la version 1.1 du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], la manière dont la méthode <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> exécute les commandes à la source de données a été modifiée.  
  
 Dans le [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] version 1.0, <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> exécutée toutes les commandes dans le contexte de la **sp_executesql** procédure stockée. Par conséquent, les commandes qui affectent l'état de la connexion (SET NOCOUNT ON, par exemple) ne s'appliquent qu'à l'exécution de la commande actuelle. L'état de la connexion n'est pas modifié pour les commandes suivantes qui sont exécutées pendant que la connexion est ouverte.  
  
 Dans le [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] version 1.1 et ultérieure, <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> s’exécute uniquement une commande dans le contexte de la **sp_executesql** procédure stockée si la commande contient des paramètres, ce qui améliore les performances. Par conséquent, si une commande affectant l'état de la connexion est incluse dans une commande non paramétrée, elle modifie l'état de la connexion pour toutes les commandes suivantes exécutées pendant que la connexion est ouverte.  
  
 Considérez le lot de commandes suivant exécuté dans un appel à <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A>.  
  
```  
SET NOCOUNT ON;  
SELECT * FROM dbo.Customers;  
```  
  
 Dans le [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] version 1.1 et ultérieure, NOCOUNT conserve la valeur ON pour toutes les commandes suivantes qui sont exécutées pendant que la connexion est ouverte. Dans la version 1.0 du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], NOCOUNT ne garde la valeur ON que pour l'exécution de la commande actuelle.  
  
 Ce changement peut avoir une incidence sur la compatibilité descendante et ascendante de votre application si vous dépendez du comportement de la méthode <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> pour l'une ou l'autre version du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].  
  
 Pour les applications qui s'exécutent sur des versions antérieures ou ultérieures du [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], vous pouvez écrire du code pour garantir que le comportement restera le même, quelle que soit la version utilisée. Si vous souhaitez vous assurer qu'une commande modifie l'état de la connexion pour toutes les commandes suivantes, nous vous recommandons d'exécuter votre commande à l'aide de la méthode <xref:System.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A>. Si vous souhaitez vous assurer qu'une commande ne modifie pas la connexion pour toutes les commandes suivantes, nous vous recommandons d'inclure les commandes qui rétablissent l'état de la connexion dans votre commande. Exemple :  
  
```  
SET NOCOUNT ON;  
SELECT * FROM dbo.Customers;  
SET NOCOUNT OFF;  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Vue d’ensemble d’ADO.NET](../../../../docs/framework/data/adonet/ado-net-overview.md)  
 [Extraction et modification de données dans ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)  
 [Fournisseurs managés ADO.NET et centre de développement DataSet](http://go.microsoft.com/fwlink/?LinkId=217917)
