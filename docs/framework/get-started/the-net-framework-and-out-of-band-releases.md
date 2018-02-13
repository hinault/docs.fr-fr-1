---
title: Versions finales hors plage de .NET Framework
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 721f10fa-3189-4124-a00d-56ddabd889b3
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 83c3688afb3fe509d9a57eba8765cbd13bf581c8
ms.sourcegitcommit: f28752eab00d2bd97e971542c0f49ce63cfbc239
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2018
---
# <a name="the-net-framework-and-out-of-band-releases"></a>Versions finales hors plage de .NET Framework
.NET Framework évolue pour s'adapter aux différentes plateformes telles que les applications Windows Phone et Windows Store, ainsi qu'aux applications bureautiques et web traditionnelles, et pour optimiser la réutilisation du code. En plus de nos versions .NET Framework classiques, nous diffuserons de nouvelles fonctionnalités hors plage (OOB) pour améliorer le développement multiplateforme ou pour introduire une nouvelle fonctionnalité. Cette rubrique décrit l'orientation future de .NET Framework et de ses versions OOB.  
  
## <a name="advantages-of-oob-releases"></a>Avantages des versions OOB  
 La livraison de nouveaux composants ou mises à jour de composants hors plage permet à Microsoft de fournir des mises à jour plus fréquentes de .NET Framework. De plus, nous pouvons nous réunir et répondre aux commentaires des clients plus rapidement.  
  
 Lorsque vous utilisez une fonctionnalité OOB dans votre application, il n'est pas nécessaire que les utilisateurs installent la version la plus récente de .NET Framework pour exécuter votre application, car les assemblys OOB se déploient avec votre package d'application.  
  
## <a name="how-oob-packages-are-distributed"></a>Mode de distribution des packages OOB  
Les versions OOB des principaux composants du Common Langage Runtime (CLR) sont fournies via le [NuGet](https://www.nuget.org/), qui est un gestionnaire de package pour .NET. NuGet vous permet de parcourir et d’ajouter facilement des bibliothèques à vos projets .NET Framework à partir de l’Explorateur de solutions de Visual Studio. NuGet est inclus avec toutes les éditions Visual Studio à partir de Visual Studio 2012. Pour savoir si NuGet est installé, recherchez **Gestionnaire de package de bibliothèques** dans le menu **Outils** de Visual Studio. S'il n'est pas installé :  
  
1.  Dans la barre de menus de Visual Studio, choisissez **Outils**, **Extensions et mises à jour** (dans Visual Studio 2010, choisissez **Gestionnaire d’extensions**).  
  
     La boîte de dialogue **Extensions et mises à jour** s’ouvre.  
  
2.  Sélectionnez **En ligne**, **Gestionnaire de package NuGet**, puis choisissez **Télécharger**.  
  
3.  Une fois le téléchargement terminé, redémarrez Visual Studio.  
  
 Pour obtenir des instructions d'installation complètes, consultez [Installation NuGet](http://docs.nuget.org/docs/start-here/installing-nuget) sur le site Web de la documentation NuGet. Pour plus d'informations sur NuGet, consultez la [documentation NuGet](http://docs.nuget.org/).  
  
## <a name="using-a-nuget-oob-package"></a>Utilisation d’un package OOB NuGet  
 Après avoir installé NuGet, vous pouvez parcourir et ajouter des références aux packages de NuGet à l’aide de l’Explorateur de solutions dans Visual Studio :  
  
1.  Ouvrez le menu contextuel de votre projet dans Visual Studio, puis choisissez **Gérer les packages NuGet**. (Cette option est également disponible dans le menu **Projet**.)  
  
2.  Dans le volet gauche, cliquez sur **En ligne**.  
  
3.  Si vous souhaitez utiliser des packages de version préliminaire, dans la zone de liste déroulante du volet central, sélectionnez l’option **Inclure la version préliminaire** au lieu de **Stable uniquement**.  
  
4.  Dans le volet droit, utilisez la zone **Rechercher** pour localiser le package que vous souhaitez utiliser. Certains packages Microsoft sont identifiés par le logo Microsoft .NET Framework, et tous identifient Microsoft en tant qu'éditeur.  
  
 ![Gestionnaire de package NuGet](../../../docs/framework/get-started/media/clrnugetdialog.png "clrNugetDialog")  
  
 Comme mentionné précédemment, lorsque vous déployez une application qui utilise un package OOB, les assemblys OOB sont fournis avec votre package d'application.  
  
## <a name="types-of-oob-releases"></a>Types de versions OOB  
 En général, un package OOB a une ou plusieurs versions préliminaires et une version stable. La licence qui accompagne une version préliminaire n'autorise généralement pas la redistribution, mais vous permet de tester un package et de fournir des commentaires. Les commentaires sont incorporés dans toutes les mises à jour apportées au package. Une version finale est distribuée comme package stable avec NuGet et inclut une licence qui vous permet de redistribuer le package NuGet avec votre application. Les packages stables sont pris en charge par Microsoft. Microsoft fournit la prise en charge IntelliSense, ainsi que d'autres types de documentation tels que les publications de blog et les réponses de forum pour tous les packages. De plus, le code source peut ne pas être disponible avec tous les packages. Pour être tenu informé sur les packages nouveaux et mis à jour, inscrivez-vous sur le [blog du .NET Framework](http://blogs.msdn.com/b/dotnet/).  
  
 Pour rechercher à la fois les versions préliminaires et les packages stables, choisissez **Inclure la version préliminaire** dans le Gestionnaire de package NuGet.  
  
 Si vous voulez être informé de la publication de packages stables, abonnez-vous au [flux .NET Framework](https://nuget.org/api/v2/curated-feeds/dotnetframework/Packages/).  
  
## <a name="see-also"></a>Voir aussi  
 [Prise en main](../../../docs/framework/get-started/index.md)
