---
title: "Comment : ajouter un écran de démarrage dans une application WPF"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WPF [WPF], splash screen
- startup window [WPF]
- SplashScreen class [WPF]
- splash screen [WPF]
ms.assetid: d70a25c4-5fb9-4c27-b01d-b1b8ef39b3fd
caps.latest.revision: "14"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 121cbc1c07ea8f6458df81d861aea3f8e1f91086
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-add-a-splash-screen-to-a-wpf-application"></a>Comment : ajouter un écran de démarrage dans une application WPF
Cette rubrique montre comment ajouter une fenêtre de démarrage, ou *écran de démarrage*, à une application Windows Presentation Foundation (WPF).  
  
### <a name="to-add-an-existing-image-as-a-splash-screen"></a>Pour ajouter une image existante en tant qu’un écran de démarrage  
  
1.  Créez ou recherchez une image que vous souhaitez utiliser pour l’écran de démarrage. Vous pouvez utiliser n’importe quel format d’image pris en charge par le composant WIC (Windows Imaging). Par exemple, vous pouvez utiliser le format BMP, GIF, JPEG, PNG ou TIFF.  
  
2.  Ajoutez le fichier image au projet d’Application WPF. Pour plus d’informations, consultez [NIB : Comment : ajouter des éléments existants à un projet](http://msdn.microsoft.com/library/15f4cfb7-78ab-457f-9f14-099a25a6a2d3).  
  
3.  Dans l’Explorateur de solutions, sélectionnez l’image.  
  
4.  Dans la fenêtre Propriétés, cliquez sur la flèche déroulante pour le **Action de génération** propriété.  
  
5.  Sélectionnez **SplashScreen** dans la liste déroulante.  
  
    > [!NOTE]
    >  Si vous ne voyez pas le **SplashScreen** option, veillez à vérifier que vous utilisez [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)] SP1 ou version ultérieure.  
  
6.  Appuyez sur F5 pour générer et exécuter l'application.  
  
     Image de l’écran de démarrage s’affiche dans le centre de l’écran, puis disparaît lorsque la fenêtre principale de l’application s’affiche.  
  
### <a name="to-remove-the-splash-screen-from-an-application"></a>Pour supprimer l’écran de démarrage à partir d’une application  
  
1.  Dans l’Explorateur de solutions, sélectionnez l’image d’écran de démarrage.  
  
2.  Dans la fenêtre Propriétés, définissez la **Action de génération** à **aucun**.  
  
### <a name="to-remove-the-splash-screen-from-an-application"></a>Pour supprimer l’écran de démarrage à partir d’une application  
  
-   Dans l’Explorateur de solutions, supprimez l’image d’écran de démarrage.  
  
-   Excluez l’image d’écran de démarrage du projet.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Windows.SplashScreen>  
 [NIB : Comment : ajouter des éléments existants à un projet](http://msdn.microsoft.com/library/15f4cfb7-78ab-457f-9f14-099a25a6a2d3)
