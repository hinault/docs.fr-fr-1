---
title: Guide pratique pour installer un assembly dans le Global Assembly Cache
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- assemblies [.NET Framework], global assembly cache
- Gacutil.exe
- strong-named assemblies, global assembly cache
- global assembly cache, installing assemblies
- Global Assembly Cache tool
ms.assetid: a7e6f091-d02c-49ba-b736-7295cb0eb743
caps.latest.revision: "24"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 98dd4d1e75fc37820a1b1f4eccfa48f978772687
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-install-an-assembly-into-the-global-assembly-cache"></a>Guide pratique pour installer un assembly dans le Global Assembly Cache
Il existe deux façons d'installer un assembly avec nom fort dans le Global Assembly Cache (GAC) :  
  
> [!IMPORTANT]
>  Seuls les assemblys avec noms forts peuvent être installés dans le GAC. Pour plus d’informations sur la façon de créer un assembly avec un nom fort, consultez [Guide pratique pour signer un assembly avec un nom fort](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md).  
  
-   Utilisation de [Windows Installer](http://msdn.microsoft.com/library/windows/desktop/cc185688.aspx).  
  
     Cela se fait dans Visual Studio 2012 et Visual Studio 2013 lorsque vous créez un projet InstallShield Limited Edition.  
  
     Il s'agit de la manière recommandée la plus commune pour ajouter des assemblys au Global Assembly Cache. Le programme d'installation fournit un décompte de références des assemblys dans le Global Assembly Cache, ainsi que d'autres avantages.  
  
-   Utilisation de l’[outil Global Assembly Cache (Gacutil.exe)](../../../docs/framework/tools/gacutil-exe-gac-tool.md).  
  
     Vous pouvez utiliser Gacutil.exe pour ajouter des assemblys avec nom fort au Global Assembly Cache et visualiser le contenu de ce cache.  
  
    > [!NOTE]
    >  Gacutil.exe ne sert qu'au développement. Il ne doit pas être utilisé pour installer des assemblys de production dans le Global Assembly Cache.  
  
> [!NOTE]
>  Dans les versions précédentes du .NET Framework, l'extension d'environnement Windows Shfusion.dll vous permettait de faire glisser des assemblys dans l'Explorateur Windows pour les installer. À partir de [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], Shfusion.dll est obsolète.  
  
### <a name="to-use-the-global-assembly-cache-tool-gacutilexe"></a>Pour utiliser l'outil Global Assembly Cache Tool (Gacutil.exe)  
  
1.  À l'invite de commandes, tapez la commande suivante :  
  
     **gacutil -i** \<*nom_assembly*>  
  
     Dans cette commande, *nom_assembly* est le nom de l’assembly à installer dans le Global Assembly Cache.  
  
 L'exemple suivant installe un assembly avec le nom de fichier `hello.dll` dans le Global Assembly Cache.  
  
```  
gacutil -i hello.dll  
```  
  
 Pour plus d’informations, consultez [Global Assembly Cache Tool (Gacutil.exe)](../../../docs/framework/tools/gacutil-exe-gac-tool.md).  
  
### <a name="to-use-an-installshield-limited-edition-project"></a>Pour utiliser un projet InstallShield Limited Edition  
  
1.  Ajoutez un package de configuration et de déploiement à votre solution en ouvrant le menu contextuel de votre solution, puis en choisissant **Ajouter**, **Nouveau projet**.  
  
2.  Dans la boîte de dialogue **Ajouter un nouveau projet**, dans le dossier **Installé**, choisissez **Autres types de projets**,  **Configuration et déploiement**, **InstallShield Limited Edition**, puis donnez un nom au projet. (Si le système vous y invite, téléchargez, installez et activez InstallShield.)  
  
3.  Effectuez la configuration générale de votre projet de configuration et de déploiement à l’aide de l’Assistant Projet de l’**Explorateur de solutions**, ou en choisissant les sous-étapes des étapes numérotées dans l’**Explorateur de solutions**. Paramétrez votre configuration comme si vous n’ajoutiez pas d’assemblys au GAC.  
  
4.  Pour démarrer le processus d’ajout d’un assembly au GAC, choisissez **Fichiers**, qui se trouve à l’étape **Spécifiez les données d’application** dans l’**Explorateur de solutions**.  
  
5.  Dans le volet **Dossiers de l’ordinateur de destination**, ouvrez le menu contextuel **Ordinateur de destination**, puis choisissez **Afficher le dossier prédéfini**, **[GlobalAssemblyCache]**.  
  
6.  Pour chaque projet de la solution qui contient un assembly à installer dans le Global Assembly Cache :  
  
    1.  Dans le volet **Dossiers de l’ordinateur de destination**, choisissez le projet.  
  
    2.  Dans le volet **Dossiers de l’ordinateur de destination**, choisissez **[GlobalAssemblyCache]**.  
  
    3.  Dans le volet **Fichiers de l’ordinateur source**, choisissez **Sortie principale de** *<nom_projet>*.  
  
    4.  Faites glisser le fichier à l’étape c vers le volet **Fichiers de l’ordinateur de destination** (ou utilisez les commandes **Copier** et **Coller** du menu contextuel du fichier).  
  
## <a name="see-also"></a>Voir aussi  
 [Utilisation d’assemblys et du Global Assembly Cache](../../../docs/framework/app-domains/working-with-assemblies-and-the-gac.md)  
 [Guide pratique pour supprimer un assembly du Global Assembly Cache](../../../docs/framework/app-domains/how-to-remove-an-assembly-from-the-gac.md)  
 [Gacutil.exe (outil Global Assembly Cache)](../../../docs/framework/tools/gacutil-exe-gac-tool.md)  
 [Comment : signer un assembly avec un nom fort](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md)  
 [Déploiement de Windows Installer](http://msdn.microsoft.com/library/121be21b-b916-43e2-8f10-8b080516d2a0)
