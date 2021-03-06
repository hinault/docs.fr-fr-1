---
title: "Hébergement dans le service d'activation de processus de Windows (WAS, Windows Process Activation Service)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: hosting services [WCF], WAS
ms.assetid: d2b9d226-15b7-41fc-8c9a-cb651ac20ecd
caps.latest.revision: "16"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 40122670c84f87590a31b79f39695e9626ea9883
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2017
---
# <a name="hosting-in-windows-process-activation-service"></a>Hébergement dans le service d'activation de processus de Windows (WAS, Windows Process Activation Service)
Le service d'activation de processus de Windows (WAS, Windows Process Activation Service) gère l'activation et la durée de vie des processus de travail qui contiennent des applications qui hébergent des services [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]. Le modèle de processus WAS généralise le modèle de processus [!INCLUDE[iis601](../../../../includes/iis601-md.md)] pour le serveur HTTP en supprimant la dépendance envers le protocole HTTP. Cela permet aux services [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] d'utiliser à la fois les protocoles HTTP et non-HTTP, tel que Net.TCP, dans un environnement d'hébergement qui prend en charge l'activation basée sur message et offre la capacité d'héberger un grand nombre d'applications sur un ordinateur donné.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]Création d’un [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] service qui s’exécute dans WAS qui héberge l’environnement, consultez [Comment : héberger un Service WCF dans WAS](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md).  
  
 Le modèle de processus WAS fournit plusieurs fonctionnalités qui permettent aux applications d’être hébergées de façon plus fiable, plus maniable et plus efficace au niveau de l’utilisation des ressources :  
  
-   L'activation basée sur message des applications et les applications de processus de travail démarrent et s'arrêtent dynamiquement en réponse aux éléments de travail entrants qui arrivent, via des protocoles réseau HTTP et non-HTTP.  
  
-   Application fiable et recyclage des processus de travail pour maintenir l'intégrité de l'exécution d'applications.  
  
-   Configuration et gestion centralisées de l'application.  
  
-   Permet aux applications de tirer parti du modèle de processus IIS sans requérir d'espace mémoire pour le déploiement d'une installation IIS complète.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]Fonctionnalités WAS, consultez [IIS 7.0 Beta : une Administration Web IIS 7.0](../../../../docs/framework/wcf/feature-details/hosting-in-windows-process-activation-service.md).  
  
 [Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkId=196496) fonctionne avec [!INCLUDE[iisver](../../../../includes/iisver-md.md)] et le Service de l’Activation des processus Windows (WAS) pour fournir une environnement de services aux services NET4 WCF et WF d’hébergement d’application riche. Ces avantages incluent la gestion du cycle de vie de processus, le recyclage de processus, l'hébergement partagé, la protection rapide contre les incidents, les processus parallèles, l'activation à la demande et le contrôle d'état. Pour plus d’informations, consultez [fonctionnalités d’hébergement AppFabric](http://go.microsoft.com/fwlink/?LinkId=196494) et [Concepts d’hébergement AppFabric](http://go.microsoft.com/fwlink/?LinkId=196495).  
  
## <a name="elements-of-the-was-addressing-model"></a>Éléments du modèle d'adressage WAS  
 Les applications ont des adresses d'URI (Uniform Resource Identifier) qui sont en fait des unités de code dont la durée de vie et l'environnement d'exécution sont gérés par le serveur. Une instance de serveur WAS unique peut loger de nombreuses applications différentes. Organisent les serveurs d’applications en groupes appelés *sites*. Dans un site, les applications sont réorganisées d'une façon hiérarchique reflétant la structure des URI qui servent d'adresses externes.  
  
 Les adresses d'application se composent de deux parties : un préfixe URI de base et une adresse relative spécifique à l'application (chemin d'accès) qui fournit l'adresse externe pour une application en cas d'association. Le préfixe URI de base est construit à partir de la liaison du site et est utilisé pour toutes les applications sous le site. Adresses d’application sont ensuite créées en prenant des fragments de chemin d’accès spécifiques à l’application (tel que « / /applicationone ») et en les ajoutant au préfixe URI de base (par exemple, « NET.TCP://localhost ») pour arriver à l’URI d’application complète.  
  
 Le tableau suivant illustre plusieurs scénarios d’adressage possibles pour les sites WAS avec des liaisons de site HTTP et non-HTTP.  
  
|Scénario|Liaisons de site|Chemin d'application|URI d'application de base|  
|--------------|-------------------|----------------------|---------------------------|  
|HTTP uniquement|http : * : 80 :\*|/appTwo|http://localhost/appTwo/|  
|À la fois HTTP et non-HTTP|http : * : 80 :\*<br /><br /> NET.TCP : 808 :\*|/appTwo|http://localhost/appTwo/<br />net.tcp://localhost/appTwo/|  
|Non-HTTP uniquement|net.pipe: *|/appThree|net.pipe://appThree/|  
  
 Les services et les ressources dans une application peuvent également être adressés. Dans une application, les ressources d'application sont adressées relativement au chemin d'accès d'application de base. Par exemple, supposez qu'un site sur un nom d'ordinateur contoso.com aie des liaisons de site pour les protocoles HTTP et Net.TCP à la fois. Supposez également que le site contienne une application située dans /Billing, qui expose un service à GetOrders.svc. Dans ce cas, si le service GetOrders.svc a exposé un point de terminaison avec une adresse relative de SecureEndpoint, le point de terminaison du service est exposé aux deux URI suivants :  
  
 http://contoso.com/Billing/GetOrders.svc/SecureEndpoint  
net.tcp://contoso.com/Billing/GetOrders.svc/SecureEndpoint  
  
## <a name="the-was-runtime"></a>Exécution WAS  
 Les applications sont organisées en sites pour les besoins d'adressage et de gestion. Au moment de l'exécution, les applications sont également groupées ensemble dans des pools d'applications. Un pool d'applications peut loger de nombreuses applications différentes à partir de nombreux sites différents. Toutes les applications à l'intérieur d'un pool d'applications partagent un jeu commun de caractéristiques d'exécution. Par exemple, elles s'exécutent toutes sous la même version CRL (Common Language Runtime) et elles partagent toutes une identité de processus commune. Chaque pool d'applications correspond à une instance d'un processus de travail (w3wp.exe). Chaque application gérée qui s'exécute dans un pool d'applications partagé est isolée des autres applications au moyen d'un AppDomain CLR.  
  
## <a name="see-also"></a>Voir aussi  
 [Architecture d’activation WAS](../../../../docs/framework/wcf/feature-details/was-activation-architecture.md)  
 [Configuration du service WAS pour une utilisation avec WCF](../../../../docs/framework/wcf/feature-details/configuring-the-wpa--service-for-use-with-wcf.md)  
 [Guide pratique pour installer et configurer des composants d’activation WCF](../../../../docs/framework/wcf/feature-details/how-to-install-and-configure-wcf-activation-components.md)  
 [How to: Host a WCF Service in WAS (Comment : héberger un service WCF dans WAS)](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md)  
 [Fonctionnalités d’hébergement de Windows Server App Fabric](http://go.microsoft.com/fwlink/?LinkId=201276)
