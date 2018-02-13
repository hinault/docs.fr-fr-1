---
title: Regsvcs.exe (outil .NET Services Installation)
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Regsvcs.exe
- .NET Services Installation tool
- loading assemblies
- assemblies [.NET Framework], registering
- type libraries
- registering assemblies
ms.assetid: 5220fe58-5aaf-4e8e-8bc3-b78c63025804
caps.latest.revision: "21"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: bfe7c3e34c2ceaf01f89c1e54f930991ee7e0a2b
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="regsvcsexe-net-services-installation-tool"></a>Regsvcs.exe (outil .NET Services Installation)
L'outil .NET Services Installation (Installation des services .NET) effectue les actions suivantes :  
  
-   Il charge et inscrit un assembly ;  
  
-   Il génère, inscrit et installe une bibliothèque de types dans l'application COM+ spécifiée ;  
  
-   Il configure les services que vous avez ajoutés à votre classe par programmation.  
  
 Pour exécuter l'outil, utilisez l'invite de commandes développeur (ou l'invite de commandes Visual Studio dans Windows 7). Pour plus d'informations, consultez [Invites de commandes](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 À l'invite de commandes, tapez le texte suivant :  
  
## <a name="syntax"></a>Syntaxe  
  
```  
      regsvcs [/c | /fc | /u] [/tlb:typeLibraryFile] [/extlb]  
[/reconfig] [/componly] [/appname:applicationName]  
[/nologo] [/quiet]assemblyFile.dll   
```  
  
#### <a name="parameters"></a>Paramètres  
  
|Argument|Description|  
|--------------|-----------------|  
|*assemblyFile.dll*|Fichier d'assembly source. L'assembly doit être signé avec un nom fort. Pour plus d’informations, consultez [Signature d’un assembly avec un nom fort](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md).|  
  
|Option|Description|  
|------------|-----------------|  
|**/appdir:** *path*|Spécifie le répertoire racine de l'application.|  
|**/appname:** *applicationName*|Spécifie le nom de l'application COM+ à rechercher ou à créer.|  
|**/c**|Crée l'application cible.|  
|**/componly**|Configure uniquement les composants ; ignore les méthodes et les interfaces.|  
|**/exapp**|Spécifie à l'outil qu'il doit attendre une application existante.|  
|**/extlb**|Utilise une bibliothèque de types existante.|  
|**/fc**|Recherche ou crée l'application cible.|  
|**/help**|Affiche la syntaxe et les options de commande de l'outil.|  
|**/noreconfig**|Ne reconfigure pas une application cible existante.|  
|**/nologo**|Supprime l'affichage de la bannière de démarrage Microsoft.|  
|**/parname:** *name*|Spécifie le nom ou l'identificateur de l'application COM+ à rechercher ou à créer.|  
|**/reconfig**|Reconfigure une application cible existante. Il s'agit de la valeur par défaut.|  
|**/tlb:** *typelibraryfile*|Spécifie le fichier bibliothèque de types à installer.|  
|**/u**|Désinstalle l'application cible.|  
|**/quiet**|Spécifie le mode silencieux ; supprime le logo et l'affichage des messages de réussite.|  
|**/?**|Affiche la syntaxe et les options de commande de l'outil.|  
  
## <a name="remarks"></a>Notes  
 Regsvcs.exe nécessite un fichier d’assembly source spécifié par *assemblyFile.dll*. Cet assembly doit être signé avec un nom fort. Pour plus d’informations sur la signature avec un nom fort, consultez [Signature d’un assembly avec un nom fort](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md). Le nom de l'application cible et le nom du fichier bibliothèque de types sont facultatifs. L’argument *applicationName* peut être généré à partir du fichier d’assembly source et sera créé par Regsvcs.exe, s’il n’existe pas déjà. L’argument *typelibraryfile* peut spécifier un nom de bibliothèque de types. Si vous ne spécifiez pas de nom de bibliothèque de types, Regsvcs.exe utilise alors par défaut le nom de l'assembly.  
  
 Quand Regsvcs.exe inscrit les méthodes d’un composant, il est soumis aux [demandes](http://msdn.microsoft.com/library/e5283e28-2366-4519-b27d-ef5c1ddc1f48) et aux [demandes de liaison](../../../docs/framework/misc/link-demands.md) sur ces méthodes. Étant donné que l'outil s'exécute dans un environnement de niveau de confiance total, la plupart des demandes d'autorisation aboutissent. Toutefois, Regsvcs.exe ne peut pas inscrire de composants avec des méthodes protégées par une demande ou une demande de liaison pour les autorisations <xref:System.Security.Permissions.StrongNameIdentityPermission> ou <xref:System.Security.Permissions.PublisherIdentityPermission>.  
  
 Vous devez détenir des privilèges d'administrateur sur l'ordinateur local pour utiliser Regsvcs.exe.  
  
 Si Regsvcs.exe échoue tandis qu'il effectue l'une de ces actions, il affiche les messages d'erreur correspondants.  
  
## <a name="examples"></a>Exemples  
 La commande suivante ajoute toutes les classes publiques figurant dans `myTest.dll` à `myTargetApp` (une application COM+ existante) et génère la bibliothèque de types `myTest.tlb`.  
  
```  
regsvcs /appname:myTargetApp myTest.dll  
```  
  
 La commande suivante ajoute toutes les classes publiques figurant dans `myTest.dll` à `myTargetApp` (une application COM+ existante) et génère la bibliothèque de types `newTest.tlb`.  
  
```  
regsvcs /appname:myTargetApp /tlb:newTest.tlb myTest.dll  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Outils](../../../docs/framework/tools/index.md)  
 [Comment : signer un assembly avec un nom fort](../../../docs/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name.md)  
 [Invites de commandes](../../../docs/framework/tools/developer-command-prompt-for-vs.md)
