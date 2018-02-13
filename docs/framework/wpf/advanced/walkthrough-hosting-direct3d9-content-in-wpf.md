---
title: "Procédure pas à pas : hébergement de contenu Direct3D9 dans WPF"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Direct3D9 [WPF interoperability], hosting Direct3D9 content
- WPF [WPF], hosting Direct3D9 content
ms.assetid: 60983736-0ab5-42cc-8b16-e9fbde261a43
caps.latest.revision: "16"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 5ad6ac99a77e3477499a871e269cc7faa7a59f12
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="walkthrough-hosting-direct3d9-content-in-wpf"></a>Procédure pas à pas : hébergement de contenu Direct3D9 dans WPF
Cette procédure pas à pas montre comment héberger du contenu Direct3D9 dans une application Windows Presentation Foundation (WPF).  
  
 Lors de cette procédure pas à pas, vous allez exécuter les tâches suivantes :  
  
-   Créez un projet WPF pour héberger le contenu Direct3D9.  
  
-   Importer le contenu Direct3D9.  
  
-   Afficher le contenu Direct3D9 à l’aide de la <xref:System.Windows.Interop.D3DImage> classe.  
  
 Lorsque vous avez terminé, vous saurez comment héberger du contenu Direct3D9 dans une application WPF.  
  
## <a name="prerequisites"></a>Prérequis  
 Pour exécuter cette procédure pas à pas, vous devez disposer des composants suivants :  
  
-   [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)].  
  
-   DirectX (SDK) 9 ou version ultérieure.  
  
-   Une DLL qui contient le contenu Direct3D9 dans un format compatible avec WPF. Pour plus d’informations, consultez [WPF et Direct3D9 interopérabilité](../../../../docs/framework/wpf/advanced/wpf-and-direct3d9-interoperation.md) et [procédure pas à pas : création de contenu Direct3D9 pour l’hébergement dans WPF](../../../../docs/framework/wpf/advanced/walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md).  
  
## <a name="creating-the-wpf-project"></a>Création du projet WPF  
 La première étape consiste à créer le projet d’application WPF.  
  
#### <a name="to-create-the-wpf-project"></a>Pour créer le projet WPF  
  
-   Créer un nouveau projet d’Application WPF dans Visual c# nommé `D3DHost`. Pour plus d'informations, consultez [Guide pratique pour créer un projet d'application WPF](http://msdn.microsoft.com/library/1f6aea7a-33e1-4d3f-8555-1daa42e95d82).  
  
     MainWindow.xaml s’ouvre dans le [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)].  
  
## <a name="importing-the-direct3d9-content"></a>L’importation du contenu Direct3D9  
 Vous importez le contenu Direct3D9 à partir d’une DLL non managée à l’aide de la `DllImport` attribut.  
  
#### <a name="to-import-direct3d9-content"></a>Pour importer le contenu Direct3D9  
  
1.  Ouvrez MainWindow.xaml.cs dans l’éditeur de Code.  
  
2.  Remplacez le code généré automatiquement par le code suivant.  
  
     [!code-csharp[System.Windows.Interop.D3DImage#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/CS/window1.xaml.cs#1)]  
  
## <a name="hosting-the-direct3d9-content"></a>Hébergement du contenu Direct3D9  
 Enfin, utilisez la <xref:System.Windows.Interop.D3DImage> classe pour héberger le contenu Direct3D9.  
  
#### <a name="to-host-the-direct3d9-content"></a>Pour héberger le contenu Direct3D9  
  
1.  Dans MainWindow.xaml, remplacez le code XAML généré automatiquement par le code XAML suivant.  
  
     [!code-xaml[System.Windows.Interop.D3DImage#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/CS/window1.xaml#10)]  
  
2.  Générez le projet.  
  
3.  Copiez la DLL qui contient le contenu Direct3D9 dans le dossier bin/Debug.  
  
4.  Appuyez sur F5 pour exécuter le projet.  
  
     Le contenu Direct3D9 s’affiche dans l’application WPF.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Windows.Interop.D3DImage>  
 [Considérations sur les performances de l'interopérabilité entre Direct3D9 et WPF](../../../../docs/framework/wpf/advanced/performance-considerations-for-direct3d9-and-wpf-interoperability.md)
