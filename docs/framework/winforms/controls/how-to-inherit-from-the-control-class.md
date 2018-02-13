---
title: "Comment : hériter de la classe du contrôle"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- inheritance [Windows Forms], Windows Forms custom controls
- Control class [Windows Forms], inheriting from
- custom controls [Windows Forms], inheritance
- OnPaint method [Windows Forms]
- custom controls [Windows Forms], creating
ms.assetid: 46ba0df3-5cf7-443c-a3b4-a72660172476
caps.latest.revision: "11"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: bdc4a5c7f721fd350f5c604d4529f05afd62a42c
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-inherit-from-the-control-class"></a>Comment : hériter de la classe du contrôle
Si vous souhaitez créer un contrôle entièrement personnalisé à utiliser sur un Windows Form, vous devez hériter de la <xref:System.Windows.Forms.Control> classe. Lors de l’héritage à partir de la <xref:System.Windows.Forms.Control> classe exige que vous effectuez la planification et implémentation plus, il vous fournit également la plus grande plage d’options. Lorsque vous héritez de <xref:System.Windows.Forms.Control>, vous héritez de la fonctionnalité de base qui rend les contrôles. Les fonctionnalités inhérentes à la <xref:System.Windows.Forms.Control> classe gère l’entrée utilisateur via le clavier et souris, définissent les limites et la taille du contrôle, fournit un handle windows et fournit la sécurité et la gestion des messages. Elles n’intègrent pas la peinture, qui désigne ici le rendu réel de l’interface graphique du contrôle, ni les fonctionnalités d’interaction utilisateur spécifiques. Vous devez fournir tous ces aspects par le biais de code personnalisé.  
  
> [!NOTE]
>  Les boîtes de dialogue et les commandes de menu qui s'affichent peuvent être différentes de celles qui sont décrites dans l'aide, en fonction de vos paramètres actifs ou de l'édition utilisée. Pour modifier vos paramètres, choisissez **Importation et exportation de paramètres** dans le menu **Outils** . Pour plus d’informations, consultez [Personnalisation des paramètres de développement dans Visual Studio](http://msdn.microsoft.com/library/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### <a name="to-create-a-custom-control"></a>Pour créer un contrôle personnalisé  
  
1.  Créez un projet d’**application Windows** ou de **bibliothèque de contrôles Windows**.  
  
2.  Dans le menu **Projet** , choisissez **Ajouter une classe**.  
  
3.  Dans la boîte de dialogue **Ajouter un nouvel élément**, cliquez sur **Contrôle personnalisé**.  
  
     Un nouveau contrôle personnalisé est ajouté à votre projet.  
  
4.  Appuyez sur F7 pour ouvrir l’**éditeur de code** de votre contrôle personnalisé.  
  
5.  Recherchez le <xref:System.Windows.Forms.Control.OnPaint%2A> (méthode), qui doit être vide à l’exception d’un appel à la <xref:System.Windows.Forms.Control.OnPaint%2A> méthode de la classe de base.  
  
6.  Modifiez le code afin d’incorporer la peinture personnalisée pour votre contrôle.  
  
     Pour plus d’informations sur l’écriture de code permettant d’afficher des graphiques concernant les contrôles, consultez [Peinture et rendu personnalisés des contrôles](../../../../docs/framework/winforms/controls/custom-control-painting-and-rendering.md).  
  
7.  Implémentez les méthodes, les propriétés ou les événements personnalisés que votre contrôle intégrera.  
  
8.  Enregistrez et testez votre contrôle.  
  
## <a name="see-also"></a>Voir aussi  
 [Variétés de contrôles personnalisés](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)  
 [Comment : hériter de la classe UserControl](../../../../docs/framework/winforms/controls/how-to-inherit-from-the-usercontrol-class.md)  
 [Guide pratique pour hériter de contrôles Windows Forms existants](../../../../docs/framework/winforms/controls/how-to-inherit-from-existing-windows-forms-controls.md)  
 [Guide pratique pour créer des contrôles pour des Windows Forms](../../../../docs/framework/winforms/controls/how-to-author-controls-for-windows-forms.md)  
 [Dépannage des gestionnaires d’événements hérités en Visual Basic](~/docs/visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md)  
 [Développement de contrôles Windows Forms au moment du design](../../../../docs/framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)
