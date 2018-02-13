---
title: "Compléments et extensibilité"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- extensibility [.NET Framework], add-ins
- add-ins [.NET Framework]
- add-ins [.NET Framework], about
- hosts [.NET Framework], compared to add-ins
- .NET Framework, add-ins
- add-in pipeline [.NET Framework], about
- add-ins [.NET Framework], compared to hosts
- .NET Framework, extensibility
- versioning [.NET Framework], add-ins
ms.assetid: 8dd45b02-7218-40f9-857d-40d7b98b850b
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 4d288d321063512f91ad94b417bb1a6bf38c9ef9
ms.sourcegitcommit: cf22b29db780e532e1090c6e755aa52d28273fa6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="add-ins-and-extensibility"></a>Compléments et extensibilité
<a name="top"></a> Les compléments fournissent des fonctionnalités ou des services étendus pour une application hôte. Le [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] fournit un modèle de programmation que les développeurs peuvent utiliser pour développer des compléments et les activer dans leur application hôte. Le modèle permet de réaliser ceci en construisant un pipeline de communication entre l'hôte et le complément. Le modèle est implémenté à l'aide des types des espaces de noms <xref:System.AddIn>, <xref:System.AddIn.Hosting>, <xref:System.AddIn.Pipeline>et <xref:System.AddIn.Contract> .  
  
 Cette vue d'ensemble contient les sections suivantes :  
  
-   [Modèle de complément](#addin_model)  
  
-   [Distinction entre les hôtes et les compléments](#distinguishing_between_addins_and_hosts)  
  
-   [Rubriques connexes](#related_topics)  
  
-   [Référence](#reference)  
  
> [!NOTE]
>  Vous trouverez des exemples de code supplémentaires et des aperçus des technologies des clients traitant des outils pour créer des pipelines de compléments sur le [site de l’extensibilité et des compléments gérés de Framework sur CodePlex](http://go.microsoft.com/fwlink/?LinkId=121190).  
  
<a name="addin_model"></a>   
## <a name="add-in-model"></a>Modèle de complément  
 Le modèle de complément se compose d'une série de segments qui constituent le pipeline de complément (également appelé pipeline de communication), qui est responsable de toutes les communications entre le complément et l'hôte. Le pipeline est un modèle de communication symétrique de segments qui échangent des données entre un complément et son hôte. Le développement de ces segments entre l'hôte et le complément fournit les couches d'abstraction requises qui prennent en charge le contrôle de version et l'isolation du complément.  
  
 L'illustration suivante présente le pipeline.  
  
 ![Ajouter &#45; dans le modèle de pipeline. ] (../../../docs/framework/add-ins/media/addin1.png "AddIn1")  
Pipeline de complément  
  
 Les assemblys pour ces segments ne doivent pas obligatoirement se trouver dans le même domaine d'application. Vous pouvez charger un complément dans son propre nouveau domaine d'application, dans un domaine d'application existant ou même dans le domaine d'application de l'hôte. Vous pouvez charger plusieurs compléments dans le même domaine d'application, ce qui permet aux compléments de partager des ressources et des contextes de sécurité.  
  
 Le modèle de complément prend en charge et recommande une frontière facultative entre l'hôte et le complément, qui est appelée la frontière d'isolement (également appelée la frontière de mise à distance). Cette frontière peut être une frontière de domaine d'application ou de processus.  
  
 Le segment de contrat au milieu du pipeline est chargé à la fois dans le domaine d'application de l'hôte et dans le domaine d'application du complément. Le contrat définit les méthodes virtuelles que l'hôte et le complément utilisent pour échanger des types entre eux.  
  
 Pour passer à travers la frontière d'isolement, les types doivent être des contrats ou des types sérialisables. Les types qui ne sont pas des contrats ou des types sérialisables doivent être convertis en contrats par les segments de l'adaptateur dans le pipeline.  
  
 Les segments de vue du pipeline sont des classes de base abstraites ou des interfaces qui fournissent à l'hôte et au complément une vue des méthodes qu'ils partagent, comme défini par le contrat.  
  
 Pour plus d’informations sur le développement de segments de pipeline, consultez [Pipeline Development](../../../docs/framework/add-ins/pipeline-development.md).  
  
 Les sections qui suivent décrivent les fonctionnalités du modèle de complément.  
  
### <a name="independent-versioning"></a>Contrôle de version indépendant  
 Le modèle de complément permet une gestion des versions indépendantes pour les hôtes et pour les compléments. Le modèle de complément permet donc les scénarios suivants :  
  
-   Création d'un adaptateur qui permet à un hôte d'utiliser un complément créé pour une version antérieure de l'hôte.  
  
-   Création d'un adaptateur qui permet à un hôte d'utiliser un complément créé pour une version ultérieure de l'hôte.  
  
-   Création d'un adaptateur qui permet à un hôte d'utiliser des compléments créés pour un autre hôte.  
  
### <a name="discovery-and-activation"></a>Découverte et activation  
 Vous pouvez activer un complément en utilisant un jeton d'une collection qui représente les compléments localisés dans une banque d'informations. Les compléments sont trouvés en recherchant le type qui définit la vue du complément de l'hôte. Vous pouvez aussi trouver un complément spécifique via le type qui définit le complément. La banque d'informations se compose de deux fichiers cache : le magasin de pipelines et le magasin de compléments.  
  
 Pour plus d’informations sur la mise à jour et la régénération de la banque d’informations, consultez [complément découverte](http://msdn.microsoft.com/library/5d268dde-11df-4c4d-a022-f58d88bbc421). Pour plus d’informations sur l’activation des compléments, consultez [Add-in Activation](http://msdn.microsoft.com/library/bedcbcdf-5964-4215-b5f3-3299798b2b3f) et [Comment : activer des compléments avec une sécurité et d’Isolation différent](http://msdn.microsoft.com/library/7afe7ec8-5158-4350-9119-5df0ecab8aa5).  
  
### <a name="isolation-levels-and-external-processes"></a>Niveaux d'isolement et processus externes  
 Le modèle de complément prend en charge plusieurs niveaux d'isolement entre un complément et son hôte, ou entre compléments. En commençant par le moins isolé, ces niveaux sont les suivants :  
  
-   Le complément s'exécute dans le même domaine d'application que l'hôte. Ceci n'est pas recommandé, car vous perdez l'isolement et les capacités de déchargement que vous obtenez quand vous utilisez différents domaines d'application.  
  
-   Plusieurs compléments sont chargés dans le même domaine d'application, qui est différent du domaine d'application utilisé par l'hôte.  
  
-   Chaque complément est chargé exclusivement dans son propre domaine d'application. Il s'agit du niveau d'isolement le plus courant.  
  
-   Plusieurs compléments sont chargés dans le même domaine d'application dans un processus externe.  
  
-   Chaque complément est chargé exclusivement dans son propre domaine d'application dans son processus externe. Il s'agit du scénario avec le plus d'isolement.  
  
 Pour plus d’informations sur l’utilisation de processus externes, consultez [Comment : activer des compléments avec une sécurité et d’Isolation différent](http://msdn.microsoft.com/library/7afe7ec8-5158-4350-9119-5df0ecab8aa5).  
  
### <a name="lifetime-management"></a>Gestion de la durée de vie  
 Étant donné que le modèle de complément couvre les limites des domaines d'application et des processus, le garbage collection en lui-même n'est pas suffisant pour libérer et récupérer des objets. Le modèle de complément fournit un mécanisme de gestion de la durée de vie qui utilise des jetons et un comptage des références, et ne requiert généralement pas de programmation supplémentaire. Pour plus d’informations, consultez [gestion de la durée de vie](http://msdn.microsoft.com/library/57a9c87e-394c-4fef-89f2-aa4223a2aeb5).  
  
 [Retour au début](#top)  
  
<a name="distinguishing_between_addins_and_hosts"></a>   
## <a name="distinguishing-between-add-ins-and-hosts"></a>Distinction entre les hôtes et les compléments  
 La différence entre un complément et un hôte est simplement que l'hôte est celui qui active le complément. L'hôte peut être le plus important des deux, par exemple une application de traitement de texte et ses vérificateurs d'orthographe, mais l'hôte peut aussi être le moins important des deux, comme un client de messagerie instantanée qui incorpore un lecteur multimédia. Le modèle de complément prend en charge des compléments dans des scénarios client et serveur. Des compléments serveur fournissant des serveurs de messagerie avec analyse antivirus, filtres anti-spam et protection IP sont des exemples de compléments serveur. Exemples de compléments client incluent des compléments de référence pour les traitements, fonctionnalités spécialisées pour les programmes graphiques et de jeux et d’une analyse antivirus pour les clients de messagerie local.  
  
 [Retour au début](#top)  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>Rubriques connexes  
  
|Titre|Description|  
|-----------|-----------------|  
|[Pipeline Development](../../../docs/framework/add-ins/pipeline-development.md)|Décrit le pipeline de communication de segments de l'application hôte vers le complément. Fournit des exemples de code dans des rubriques de procédure pas à pas qui décrivent comment construire le pipeline et déployer des segments vers le pipeline dans [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].|  
|[Domaines d'application et assemblys](http://msdn.microsoft.com/library/433b04ae-4ba8-4849-9dbd-79194f240346)|Décrit la relation entre les domaines d'application, qui fournissent une frontière d'isolement pour la sécurité, la fiabilité et le contrôle de version, et les assemblys.|  
  
 [Retour au début](#top)  
  
<a name="reference"></a>   
## <a name="reference"></a>Référence  
 <xref:System.AddIn?displayProperty=nameWithType>  
  
 <xref:System.AddIn.Contract?displayProperty=nameWithType>  
  
 <xref:System.AddIn.Hosting?displayProperty=nameWithType>  
  
 <xref:System.AddIn.Pipeline?displayProperty=nameWithType>  
  
 [Retour au début](#top)