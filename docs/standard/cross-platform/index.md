---
title: "Développement pour plusieurs plateformes avec le .NET Framework"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b153baaa-130c-4169-860b-e580591de91e
caps.latest.revision: "13"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 9acceb04ea48ef7d9a99d8a82c63090ee344ea54
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="developing-for-multiple-platforms-with-the-net-framework"></a>Développement pour plusieurs plateformes avec le .NET Framework
Vous pouvez développer des applications pour les plateformes Microsoft et non-Microsoft à l'aide du .NET Framework et de Visual Studio.  
  
## <a name="options-for-cross-platform-development"></a>Options pour le développement interplateforme  
 Pour développer pour plusieurs plateformes, vous pouvez partager le code source ou les binaires, et effectuer des appels entre le code .NET Framework et les API Windows Runtime.  
  
|Pour...|Utilisez...|  
|-----------------------|------------|  
|Partager le code source entre les applications Windows Phone 8.1 et Windows 8.1|**Projets partagés** (modèle applications universelles dans Visual Studio 2013 Update 2).<br /><br /> -Actuellement aucune prise en charge Visual Basic.<br />-Vous pouvez séparer le code spécifique à une plateforme à l’aide de #`if` instructions.<br /><br /> Pour plus d'informations, consultez :<br /><br /> -   [Créer des applications qui ciblent Windows et Windows Phone à l’aide de Visual Studio](http://msdn.microsoft.com/library/windows/apps/dn609832.aspx) (article MSDN)<br />-   [À l’aide de Visual Studio pour créer des applications XAML universelles](http://blogs.msdn.com/b/visualstudio/archive/2014/04/14/using-visual-studio-to-build-universal-xaml-apps.aspx) (billet de blog)<br />-   [À l’aide de Visual Studio pour créer des applications XAML](http://channel9.msdn.com/Events/Build/2014/3-591) (vidéo)|  
|Partager les binaires entre des applications qui ciblent différentes plateformes|**Les projets de bibliothèque de classes portables** pour le code qui est indépendant de la plateforme.<br /><br /> -Cette approche est généralement utilisée pour le code qui implémente la logique métier.<br />-Vous pouvez utiliser Visual Basic ou c#.<br />-Prise en charge API varie selon la plate-forme.<br />-Les projets de bibliothèque de classes portables qui ciblent Windows 8.1 et Windows Phone 8.1 prennent en charge APIs Windows Runtime et XAML. Ces fonctionnalités ne sont pas disponibles pour les anciennes versions de la bibliothèque de classes portables.<br />-Si nécessaire, vous pouvez abstraire le code spécifique à une plateforme à l’aide des interfaces ou des classes abstraites.<br /><br /> Pour plus d'informations, consultez :<br /><br /> -   [Bibliothèque de classes portable](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md) (article MSDN)<br />-   [Comment effectuer le travail des bibliothèques de classe Portable vous](http://blogs.msdn.com/b/dsplaisted/archive/2012/08/27/how-to-make-portable-class-libraries-work-for-you.aspx) (billet de blog)<br />-   [À l’aide de la bibliothèque de classes portables avec MVVM](../../../docs/standard/cross-platform/using-portable-class-library-with-model-view-view-model.md) (article MSDN)<br />-   [Ressources d’application pour les bibliothèques que ciblent des plateformes multiples](../../../docs/standard/cross-platform/app-resources-for-libraries-that-target-multiple-platforms.md) (article MSDN)<br />-   [Analyseur de portabilité .NET](http://visualstudiogallery.msdn.microsoft.com/1177943e-cfb7-4822-a8a6-e56c7905292b) (extension de Visual Studio)|  
|Partager le code source entre des applications pour des plateformes autres que Windows 8.1 et Windows Phone 8.1|**Ajouter en tant que lien** fonctionnalité.<br /><br /> -Cette approche est appropriée pour la logique d’application qui est commune aux deux applications mais ne sont pas portables, pour une raison quelconque. Vous pouvez utiliser cette fonctionnalité pour du code C# ou Visual Basic.<br />     Par exemple, Windows Phone 8 et Windows 8 partagent des API Windows Runtime, mais les bibliothèques de classes portables ne prennent pas en charge Windows Runtime pour ces plateformes. Vous pouvez utiliser la fonctionnalité `Add as link` pour partager du code Windows Runtime entre une application Windows Phone 8 et une application Windows Store qui cible Windows 8.<br /><br /> Pour plus d'informations, consultez :<br /><br /> -   [Partager du code avec les ajouter en tant que lien](http://msdn.microsoft.com/library/windowsphone/develop/jj714082\(v=vs.105\).aspx) (article MSDN)<br />-   [Comment : ajouter des éléments existants à un projet](http://msdn.microsoft.com/library/vstudio/9f4t9t92\(v=vs.100\).aspx) (article MSDN)|  
|Écrire des applications Windows Store à l'aide du .NET Framework ou appeler des API Windows Runtime à partir d'un code .NET Framework|**Windows Runtime APIs** à partir de votre code .NET Framework c# ou Visual Basic et utilisez le .NET Framework pour créer des applications du Windows Store. Gardez à l'esprit que les API diffèrent entre les deux plateformes. Toutefois, certaines classes vous permettent de gérer ces différences.<br /><br /> Pour plus d'informations, consultez :<br /><br /> -   [.NET framework prise en charge pour les applications du Windows Store et Windows Runtime](../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md) (article MSDN)<br />-   [Transmission d’un URI au Windows Runtime](../../../docs/standard/cross-platform/passing-a-uri-to-the-windows-runtime.md) (article MSDN)<br />-   <!--zz <xref:System.IO.WindowsRuntimeStreamExtensions>-->`System.IO.WindowsRuntimeStreamExtensions` (Page de référence d’API MSDN)<br />-   <!--zz <xref:System.WindowsRuntimeSystemExtensions>-->`System.WindowsRuntimeSystemExtensions` (Page de référence d’API MSDN)|  
|Créer des applications .NET Framework pour des plateformes non-Microsoft|**Assemblys de référence de bibliothèque de classes portables** dans le .NET Framework et un outil de tiers ou extension de Visual Studio tels que Xamarin.<br /><br /> Pour plus d'informations, consultez :<br /><br /> -   [Bibliothèque de classes portables désormais disponible sur toutes les plateformes.](http://blogs.msdn.com/b/dotnet/archive/2013/10/14/portable-class-library-pcl-now-available-on-all-platforms.aspx) (publication de blog)<br />-   [Xamarin](http://xamarin.com/visual-studio) (site Web Xamarin)|  
|utiliser JavaScript et HTML pour le développement interplateforme|**Modèles application universelle** dans Visual Studio 2013, mise à jour 2 pour développer sur APIs Windows Runtime pour Windows 8.1 et Windows Phone 8.1. Actuellement, vous ne pouvez pas utiliser JavaScript et HTML avec des API .NET Framework pour développer des applications interplateformes.<br /><br /> Pour plus d'informations, consultez :<br /><br /> -   [Modèles de projet JavaScript](http://msdn.microsoft.com/library/windows/apps/hh758331.aspx)<br />-   [Portage d’une application Windows Runtime à l’aide de JavaScript pour Windows Phone](http://msdn.microsoft.com/library/windows/apps/dn636144.aspx)|
