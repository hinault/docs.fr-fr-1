---
title: Ajout de rapports affichables aux applications Visual Studio
ms.date: 07/20/2015
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- printing [Visual Studio], reports
- reports [Visual Basic], printing in Visual Studio
ms.assetid: 93928405-ef41-495e-bce2-9d43d5a7080a
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 2b0300f31e4c75c72a72590ad22c19441acb7519
ms.sourcegitcommit: cf22b29db780e532e1090c6e755aa52d28273fa6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="adding-printable-reports-to-visual-studio-applications"></a>Ajout de rapports affichables aux applications Visual Studio
Visual Studio prend en charge une variété de solutions de création de rapports pour vous aider à ajouter des rapports de données à vos applications Visual Basic. Vous pouvez créer et ajouter des rapports à l’aide de contrôles ReportViewer, Crystal Reports ou SQL Server Reporting Services.  
  
> [!NOTE]
>  SQL Server Reporting Services fait partie de SQL Server 2005 plutôt que Visual Studio. Reporting Services non installés sur votre système, sauf si vous avez installé SQL Server 2005.  
  
## <a name="overview-of-microsoft-reporting-technology-in-visual-basic-applications"></a>Vue d’ensemble de Microsoft Reporting technologie dans les Applications Visual Basic  
 Choisissez l’une des approches suivantes pour utiliser une technologie dans votre application de création de rapports de Microsoft :  
  
-   Ajouter une ou plusieurs instances d’un contrôle ReportViewer à une application Windows Visual Basic.  
  
-   Intégrer SQL Server Reporting Services par programmation via des appels au service Web Report Server.  
  
-   Utiliser le contrôle ReportViewer et Microsoft SQL Server 2005 Reporting Services, à l’aide du contrôle comme une visionneuse de rapports et un serveur de rapports comme un processeur de rapports. (Notez que vous devez utiliser la version de SQL Server 2005 de Reporting Services si vous souhaitez utiliser un serveur de rapports et le contrôle ReportViewer ensemble).  
  
## <a name="using-reportviewer-controls"></a>À l’aide de contrôles ReportViewer  
 Pour incorporer la fonctionnalité de rapport dans une application Windows Visual Basic, le plus simple consiste à ajouter le contrôle ReportViewer à un formulaire dans votre application. Le contrôle ajoute directement à votre application des fonctionnalités de traitement des rapports et fournit un concepteur de rapports intégré qui permet de générer des rapports à l’aide des données à partir de n’importe quel objet de données ADO.NET. Une API complète fournit l’accès par programme au contrôle et les rapports afin que vous pouvez configurer les fonctionnalités d’exécution.  
  
 ReportViewer fournit le traitement des rapports intégrés et des capacités de visualisation dans un contrôle de données unique et librement distribuable. Choisissez que les contrôles ReportViewer si vous avez besoin des fonctionnalités de rapport suivantes :  
  
-   Traitement des rapports dans l’application cliente. Un rapport traité apparaît dans une zone d’affichage fournie par le contrôle.  
  
-   Liaison de données aux tables de données ADO.NET. Vous pouvez créer des rapports qui utilisent des <xref:System.Data.DataTable> instances fournies au contrôle. Vous pouvez également lier directement à des objets métier.  
  
-   Contrôles redistribuables que vous pouvez inclure dans votre application.  
  
-   Fonctionnalités de runtime telles que la navigation entre les pages, l’impression, la recherche et les formats d’exportation. Une barre d’outils ReportViewer prend en charge ces opérations.  
  
 Pour utiliser le contrôle ReportViewer, vous pouvez le faire glisser à partir de la **données** section de l’outils de Visual Studio sur un formulaire dans votre application Windows Visual Basic.  
  
### <a name="creating-reports-in-visual-studio-for-reportviewer-controls"></a>Création de rapports dans Visual Studio pour les contrôles ReportViewer  
 Pour générer un rapport qui s’exécute dans ReportViewer, ajoutez un **rapport** modèle à votre projet. Visual Studio crée un fichier de définition de rapport client (.rdlc), ajoute le fichier à votre projet et ouvre un concepteur de rapports intégré dans l’espace de travail de Visual Studio.  
  
 Le Concepteur de rapports Visual Studio s’intègre à la **des Sources de données** fenêtre. Lorsque vous faites glisser un champ à partir de la **des Sources de données** fenêtre pour le rapport, le Concepteur de rapports copie les métadonnées de la source de données dans le fichier de définition de rapport. Ces métadonnées sont utilisée par le contrôle ReportViewer pour générer automatiquement le code de liaison de données.  
  
 Le Concepteur de rapports Visual Studio n’inclut pas la fonctionnalité d’aperçu de rapport. Pour afficher un aperçu de votre rapport, exécutez l’application et afficher un aperçu du rapport est incorporé.  
  
|Pour ajouter des fonctionnalités de rapport de base à votre application|  
|---|    
|1.  Faites glisser un contrôle ReportViewer à partir de la **données** onglet de la **boîte à outils** vers votre formulaire.<br />2.  Dans le menu **Projet** , choisissez **Ajouter un nouvel élément**. Dans le **ajouter un nouvel élément** boîte de dialogue, sélectionnez le **rapport** icône et cliquez sur **ajouter**.<br />     Le Concepteur de rapports s’ouvre dans l’environnement de développement, et un fichier de rapport (.rdlc) est ajouté au projet.<br />3.  Faites glisser des éléments de rapport à partir de la **boîte à outils** sur la disposition du rapport et les réorganiser comme vous le souhaitez.<br />4.  Faites glisser les champs à partir de la **des Sources de données** fenêtre pour les éléments de rapport dans la disposition du rapport.|  
  
## <a name="using-reporting-services-in-visual-basic-applications"></a>Utilisation de Reporting Services dans les Applications Visual Basic  
 Reporting Services est une technologie de création de rapports basée sur le serveur qui est incluse avec SQL Server. Reporting Services comprend des fonctionnalités supplémentaires qui ne figurent pas dans les contrôles ReportViewer. Choisissez Reporting Services si vous avez besoin des fonctionnalités suivantes :  
  
-   Déploiement avec montée en puissance parallèle et au traitement de rapports côté serveur qui offre de meilleures performances pour les rapports complexes ou longues et pour l’activité des rapports de haut volume.  
  
-   Formats de sortie de données intégrées et traitement des rapports, avec prise en charge pour les contrôles de rapport personnalisé et de rendu rich.  
  
-   Planifier le traitement des rapports afin que vous puissiez spécifier exactement quand les rapports sont exécutés.  
  
-   Distribution d’un rapport basé sur l’abonné par courrier électronique ou à des emplacements de partage de fichiers.  
  
-   Rapport ad hoc afin que les utilisateurs professionnels peuvent créer des rapports en fonction des besoins.  
  
-   Abonnements pilotés par les données qui acheminer la sortie des rapports personnalisés à une liste dynamique de destinataires.  
  
-   Extensions personnalisées pour le traitement des données, la remise de rapports, authentification personnalisée et le rendu du rapport.  
  
 Le serveur de rapports est implémenté en tant que service Web. Code de votre application doit inclure des appels au service Web pour accéder aux rapports et autres métadonnées. Le service Web fournit l’accès par programme complète à une instance de serveur de rapports.  
  
 Étant donné que Reporting Services est une technologie de création de rapports basée sur le Web, la visionneuse par défaut affiche les rapports sont rendus au format HTML. Si vous ne souhaitez pas utiliser HTML comme format de présentation de rapport par défaut, vous devez écrire une visionneuse de rapports personnalisés pour votre application.  
  
### <a name="creating-reports-in-visual-studio-for-reporting-services"></a>Création de rapports dans Visual Studio pour Reporting Services  
 Pour générer des rapports qui s’exécutent sur un serveur de rapports, vous créez la définition de rapport (.rdl) fichiers dans Visual Studio via Business Intelligence Development Studio, qui est fourni avec SQL Server 2005.  
  
> [!NOTE]
>  Vous devez disposer de SQL Server 2005 est installé pour pouvoir utiliser SQL Server Reporting Services et Business Intelligence Development Studio.  
  
 Business Intelligence Development Studio ajoute des modèles de projet qui sont spécifiques aux composants SQL Server. Pour créer des rapports, vous pouvez choisir parmi les **projet Report Server** ou **Assistant Projet Report Server** modèles. Vous pouvez spécifier des connexions aux sources de données et des requêtes à une variété de types de sources de données, y compris SQL Server, Oracle, Analysis Services, XML et SQL Server Integration Services. A **données** onglet, **disposition** onglet, et **aperçu** permettent de définir des données, créer une disposition de rapport et afficher un aperçu du rapport dans le même espace de travail.  
  
 Les définitions de rapport que vous générez pour le contrôle ou le serveur de rapports peuvent être réutilisées dans chaque technologie.  
  
|Pour créer un rapport qui s’exécute sur un serveur de rapports|  
|---|    
|1.  Sur le **fichier** menu, choisissez **nouveau**.<br />     La boîte de dialogue **Nouveau projet** s'affiche.<br />2.  Dans le **types de projet** volet, cliquez sur **projets Business Intelligence**.<br />3.  Dans le volet Modèles, sélectionnez **projet Report Server** ou **Assistant Projet Report Server**.|  
  
## <a name="using-reportviewer-controls-and-sql-server-reporting-services-together"></a>À l’aide de contrôles ReportViewer et SQL Server Reporting Services ensemble  
 Les contrôles ReportViewer et SQL Server 2005 Reporting Services peuvent être utilisés ensemble dans la même application.  
  
-   Le contrôle ReportViewer fournit une visionneuse qui est utilisée pour afficher des rapports dans votre application.  
  
-   Reporting Services fournit les rapports et effectue tout le traitement sur un serveur distant.  
  
 Le contrôle ReportViewer peut être configuré pour afficher des rapports qui sont stockés et traités sur un serveur de rapports Reporting Services à distance. Ce type de configuration est appelé *mode de traitement distant*. En mode de traitement distant, le contrôle demande un rapport qui est stocké sur un serveur de rapports à distance. Le serveur de rapports effectue toutes les le traitement des rapports, le traitement des données et le rendu du rapport. Un rapport fini et rendu est retourné au contrôle et affiché dans la zone d’affichage.  
  
 Rapports qui s’exécutent sur un support de serveur de rapports supplémentaire formats d’exportation, ont une implémentation de paramétrage de rapport différent, utilisez les types de source de données qui sont pris en charge par le serveur de rapports et sont accessibles via le modèle d’autorisation basée sur le serveur de rapports.  
  
 Pour utiliser le mode de traitement distant, spécifiez l’URL et le chemin d’accès à un rapport de serveur lors de la configuration du contrôle ReportViewer.
