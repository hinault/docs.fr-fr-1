---
title: "Comment : créer une interface utilisateur à plusieurs volets avec des Windows Forms à l'aide du concepteur"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- user interface [Windows Forms], multipane
- SplitContainer control [Windows Forms], using the designer
- multipane user interface
ms.assetid: c3f9294d-a26c-4198-9242-f237f55f7573
caps.latest.revision: "6"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 1752691b3cc6809f1a5da54a01e81de2d4037d19
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-create-a-multipane-user-interface-with-windows-forms-using-the-designer"></a>Comment : créer une interface utilisateur à plusieurs volets avec des Windows Forms à l'aide du concepteur
Dans la procédure suivante, vous allez créer une interface utilisateur à plusieurs volets semblable à celle utilisée dans Microsoft Outlook, avec une **dossier** liste, un **Messages** volet et un **aperçu** volet. Cette disposition est obtenue principalement par le biais d’ancrage de contrôles dans le formulaire.  
  
 Lorsque vous ancrez un contrôle, vous déterminez le bord du conteneur parent auquel un contrôle est attaché. Par conséquent, si vous définissez la <xref:System.Windows.Forms.SplitContainer.Dock%2A> propriété <xref:System.Windows.Forms.DockStyle.Right>, le bord droit du contrôle sera ancré sur le bord droit de son contrôle parent. En outre, le bord ancré du contrôle est redimensionné pour correspondre à celui de son contrôle conteneur. Pour plus d’informations sur la façon dont <xref:System.Windows.Forms.SplitContainer.Dock%2A> fonctionne de la propriété, consultez [Comment : ancrer des contrôles aux Windows Forms](../../../../docs/framework/winforms/controls/how-to-dock-controls-on-windows-forms.md).  
  
 Cette procédure se concentre sur la disposition du <xref:System.Windows.Forms.SplitContainer> et d’autres contrôles sur le formulaire, et non sur l’ajout de fonctionnalités pour que l’application ressemble à Microsoft Outlook.  
  
 Pour créer cette interface utilisateur, vous placez tous les contrôles dans un <xref:System.Windows.Forms.SplitContainer> contrôle, qui contient un <xref:System.Windows.Forms.TreeView> contrôle dans le volet gauche. Le volet droit de la <xref:System.Windows.Forms.SplitContainer> contrôle contient un deuxième <xref:System.Windows.Forms.SplitContainer> contrôler avec un <xref:System.Windows.Forms.ListView> contrôle ci-dessus un <xref:System.Windows.Forms.RichTextBox> contrôle. Ces <xref:System.Windows.Forms.SplitContainer> contrôles permettent un redimensionnement indépendant des autres contrôles sur le formulaire. Vous pouvez adapter les techniques présentées dans cette procédure pour élaborer les interfaces utilisateur de votre choix.  
  
> [!NOTE]
>  Les boîtes de dialogue et les commandes de menu qui s'affichent peuvent être différentes de celles qui sont décrites dans l'aide, en fonction de vos paramètres actifs ou de l'édition utilisée. Pour modifier vos paramètres, choisissez **Importation et exportation de paramètres** dans le menu **Outils** . Pour plus d’informations, consultez [Personnalisation des paramètres de développement dans Visual Studio](http://msdn.microsoft.com/library/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### <a name="to-create-an-outlook-style-user-interface-at-design-time"></a>Pour créer une interface utilisateur de style Outlook au moment du design  
  
1.  Créer un nouveau projet d’Application Windows. Pour plus d’informations, consultez l’article [Comment : créer un projet d’application Windows](http://msdn.microsoft.com/library/b2f93fed-c635-4705-8d0e-cf079a264efa).  
  
2.  Faites glisser un <xref:System.Windows.Forms.SplitContainer> contrôle depuis la **boîte à outils** au formulaire. Dans le **propriétés** , configurez la <xref:System.Windows.Forms.SplitContainer.Dock%2A> propriété <xref:System.Windows.Forms.DockStyle.Fill>.  
  
3.  Faites glisser un <xref:System.Windows.Forms.TreeView> contrôle depuis la **boîte à outils** vers le panneau gauche de la <xref:System.Windows.Forms.SplitContainer> contrôle. Dans le **propriétés** , configurez la <xref:System.Windows.Forms.SplitContainer.Dock%2A> propriété <xref:System.Windows.Forms.DockStyle.Left> en cliquant sur le panneau gauche de l’éditeur de valeurs affiché lorsque vous cliquez sur la flèche vers le bas.  
  
4.  Faites glisser une autre <xref:System.Windows.Forms.SplitContainer> contrôle depuis la **boîte à outils**; placer dans le volet droit de la <xref:System.Windows.Forms.SplitContainer> contrôle que vous avez ajouté à votre formulaire. Dans le **propriétés** , configurez la <xref:System.Windows.Forms.SplitContainer.Dock%2A> propriété <xref:System.Windows.Forms.DockStyle.Fill> et <xref:System.Windows.Forms.SplitContainer.Orientation%2A> propriété <xref:System.Windows.Forms.Orientation.Horizontal>.  
  
5.  Faites glisser un <xref:System.Windows.Forms.ListView> contrôle depuis la **boîte à outils** vers le panneau supérieur du deuxième <xref:System.Windows.Forms.SplitContainer> contrôle que vous avez ajouté à votre formulaire. Affectez à la propriété <xref:System.Windows.Forms.SplitContainer.Dock%2A> du contrôle <xref:System.Windows.Forms.ListView> la valeur <xref:System.Windows.Forms.DockStyle.Fill>.  
  
6.  Faites glisser un <xref:System.Windows.Forms.RichTextBox> contrôle depuis la **boîte à outils** vers le panneau inférieur du deuxième <xref:System.Windows.Forms.SplitContainer> contrôle. Affectez à la propriété <xref:System.Windows.Forms.SplitContainer.Dock%2A> du contrôle <xref:System.Windows.Forms.RichTextBox> la valeur <xref:System.Windows.Forms.DockStyle.Fill>.  
  
     À ce stade, si vous appuyez sur F5 pour exécuter l’application, le formulaire affiche une interface utilisateur en trois parties, semblable à celle de Microsoft Outlook.  
  
    > [!NOTE]
    >  Lorsque vous placez le pointeur de la souris sur un des séparateurs dans la <xref:System.Windows.Forms.SplitContainer> contrôles, vous pouvez modifier les dimensions internes.  
  
     À ce stade dans le développement d’applications, vous avez créé une interface utilisateur sophistiquée. L’étape suivante consiste à continuer avec la programmation de l’application elle-même, peut-être en connectant le <xref:System.Windows.Forms.TreeView> contrôle et <xref:System.Windows.Forms.ListView> contrôles à un certain type de source de données. Pour plus d’informations sur la connexion des contrôles aux données, consultez [une liaison de données et Windows Forms](../../../../docs/framework/winforms/data-binding-and-windows-forms.md).  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Windows.Forms.SplitContainer>  
 [SplitContainer, contrôle](../../../../docs/framework/winforms/controls/splitcontainer-control-windows-forms.md)
