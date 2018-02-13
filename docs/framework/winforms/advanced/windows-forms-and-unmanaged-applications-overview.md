---
title: "Vue d'ensemble des applications Windows Forms et non managées"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- COM [Windows Forms]
- Windows Forms, unmanaged
- COM interop
- ActiveX controls [Windows Forms], about ActiveX controls
- Windows Forms, interop
ms.assetid: 0a26d99d-8135-4895-8760-c9a2b5f67f14
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 9ad64588727584a9b3de0a95e9bad252a3fb0581
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="windows-forms-and-unmanaged-applications-overview"></a>Vue d'ensemble des applications Windows Forms et non managées
Les contrôles et les applications Windows Forms peuvent interagir avec des applications non managées, avec certaines restrictions. Les sections suivantes décrivent les scénarios et les configurations pris en charge et non pris en charge par les applications et les contrôles Windows Forms.  
  
## <a name="windows-forms-controls-and-activex-applications"></a>Contrôles Windows Forms et Applications ActiveX  
 À l'exception de Microsoft Internet Explorer et de Microsoft Foundation Classes (MFC), les contrôles Windows Forms ne sont pas pris en charge dans les applications conçues pour héberger des contrôles ActiveX. Les autres applications et outils de développement capables d'héberger des contrôles ActiveX, y compris les conteneurs de test ActiveX des versions de Visual Studio antérieures à Visual Studio .NET 2003, ne sont pas des hôtes pris en charge pour les contrôles Windows Forms.  
  
 Ces contraintes s'appliquent également à l'utilisation des contrôles Windows Forms via l'interopérabilité COM Component Object Model. L'utilisation d'un contrôle Windows Forms via un wrapper CCW (COM Callable Wrapper) est prise en charge uniquement dans Internet Explorer. Pour plus d'informations sur l'interopérabilité COM, consultez  
  
 [COM Interop](../../../visual-basic/programming-guide/com-interop/index.md).  
  
 Le tableau suivant indique la prise en charge de l'hébergement ActiveX disponible pour les contrôles Windows Forms.  
  
|Version de Windows Forms|Prise en charge|  
|---------------------------|-------------|  
|.NET Framework version 1.0|Internet Explorer 5.01 et versions ultérieures|  
|.NET Framework version 1.1 et ultérieures|Internet Explorer 5.01 et versions ultérieures<br /><br /> Bibliothèque MFC (Microsoft Foundation Class) 7.0 et versions ultérieures|  
  
## <a name="hosting-windows-forms-components-as-activex-controls"></a>Hébergement de composants Windows Forms en tant que contrôles ActiveX  
 Dans .NET Framework 1.1, la prise en charge a été étendue pour inclure MFC 7.0 et versions ultérieures. Cette prise en charge comprend tout conteneur qui est entièrement compatible avec le conteneur de contrôles ActiveX MFC 7.0 et versions ultérieures.  
  
 Toutefois, l'inscription des contrôles Windows Forms en tant que contrôles ActiveX n'est pas prise en charge. En outre, l'appel de la méthode `com.ms.win32.Ole32.CoCreateInstance` pour les contrôles Windows Forms n'est pas prise en charge. Seule l'activation managée des contrôles Windows Forms est prise en charge. Une fois que vous avez créé un contrôle Windows Forms, vous pouvez l'héberger dans une application MFC comme tout contrôle ActiveX.  
  
 Pour utiliser des contrôles Windows Forms dans votre application non managée, vous devez soit héberger le CLR à l'aide des API d'hébergement CLR non managées, soit utiliser les fonctionnalités d'interopérabilité C++. L'utilisation des fonctionnalités d'interopérabilité C++ est la solution recommandée.  
  
## <a name="windows-forms-in-com-client-applications"></a>Windows Forms dans les applications clientes COM  
 Quand vous ouvrez un Windows Form à partir d'une application cliente COM, telle qu'une application Visual Basic 6.0 ou une application MFC, le formulaire peut se comporter de façon inattendue. Par exemple, quand vous appuyez sur la touche Tab, le focus ne passe pas d'un contrôle à un autre. Quand vous appuyez sur la touche Entrée pendant qu'un bouton de commande a le focus, l'événement <xref:System.Windows.Forms.Control.Click> du bouton n'est pas déclenché. Vous pouvez également constater un comportement inattendu pour les combinaisons de touches ou l'activité de la souris.  
  
 Ce comportement se produit car l'application non managée n'implémente pas la prise en charge de boucle de message dont Windows Forms a besoin pour fonctionner correctement. La boucle de message fournie par l'application cliente COM est fondamentalement différente de la boucle de message Windows Forms.  
  
 La boucle de message d'une application est une boucle de programme interne qui récupère les messages à partir de la file d'attente de messages d'un thread, les traduit, puis les envoie à l'application pour qu'ils soient gérés. La boucle de message pour un Windows Form n'a pas la même architecture que les boucles de messages fournies par les applications antérieures, telles que les applications Visual Basic 6.0 et les applications MFC. Les messages de fenêtre publiés dans la boucle de message peuvent être traités différemment de ce à quoi s'attend le Windows Form. Ainsi, un comportement inattendu peut se produire. Certaines combinaisons de touches peuvent ne pas fonctionner, certaines activités de la souris peuvent ne pas fonctionne ou certains événements peuvent ne pas être déclenchés comme prévu.  
  
## <a name="resolving-interoperability-issues"></a>Résolution des problèmes d'interopérabilité  
 Vous pouvez résoudre ces problèmes en affichant le formulaire sur une boucle de message [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], que vous pouvez créer à l'aide de la méthode <xref:System.Windows.Forms.Application.Run%2A?displayProperty=nameWithType>.  
  
 Pour qu'un Windows Form fonctionne correctement à partir d'une application cliente COM, vous devez l'exécuter sur une boucle de message Windows Forms. Pour cela, utilisez l'une des approches suivantes :  
  
-   Utilisez la méthode <xref:System.Windows.Forms.Form.ShowDialog%2A?displayProperty=nameWithType> pour afficher le Windows Form. Pour plus d'informations, consultez [How to: Support COM Interop by Displaying a Windows Form with the ShowDialog Method](../../../../docs/framework/winforms/advanced/com-interop-by-displaying-a-windows-form-shadow.md).  
  
-   Affichez chaque Windows Form sur un nouveau thread. Pour plus d’informations, consultez [Comment : prendre en charge l’interopérabilité COM en affichant chaque Windows Form sur son propre thread](../../../../docs/framework/winforms/advanced/how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Applications Windows Forms et non managées](../../../../docs/framework/winforms/advanced/windows-forms-and-unmanaged-applications.md)  
 [COM Interop](../../../visual-basic/programming-guide/com-interop/index.md)  
 [Interopérabilité COM dans les applications .NET Framework](~/docs/visual-basic/programming-guide/com-interop/com-interoperability-in-net-framework-applications.md)  
 [Exemples d’interopérabilité COM](http://msdn.microsoft.com/library/09c38567-6380-4d70-848a-e896a4ca05f4)  
 [Aximp.exe (importateur de contrôles Active X Windows Forms)](../../../../docs/framework/tools/aximp-exe-windows-forms-activex-control-importer.md)  
 [Exposition de composants .NET Framework à COM](../../../../docs/framework/interop/exposing-dotnet-components-to-com.md)  
 [Empaquetage d'un assembly pour COM](../../../../docs/framework/interop/packaging-an-assembly-for-com.md)  
 [Inscription d’assemblys dans COM](../../../../docs/framework/interop/registering-assemblies-with-com.md)  
 [Guide pratique pour prendre en charge COM Interop en affichant un Windows Form avec la méthode ShowDialog](../../../../docs/framework/winforms/advanced/com-interop-by-displaying-a-windows-form-shadow.md)  
 [Comment : prendre en charge l’interopérabilité COM en affichant chaque Windows Form sur son propre thread](../../../../docs/framework/winforms/advanced/how-to-support-com-interop-by-displaying-each-windows-form-on-its-own-thread.md)
