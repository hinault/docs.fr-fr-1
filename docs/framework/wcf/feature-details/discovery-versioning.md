---
title: "Contrôle des versions de découverte"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f91c6d0a-3af2-45c5-9a5c-e75390619836
caps.latest.revision: "10"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: df5a15f740e9db4eb58ec4e410db9ef5e014fe0a
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2017
---
# <a name="discovery-versioning"></a>Contrôle des versions de découverte
Cette rubrique donne une rapide vue d’ensemble de l’implémentation de nouvelles fonctionnalités de découverte. Elle donne également une vue d'ensemble de la manière de sélectionner la version de découverte à utiliser.  
  
## <a name="discovery-versioning"></a>Contrôle des versions de découverte  
 La fonctionnalité de découverte inclut la prise en charge de trois versions du protocole WS_Discovery. Les API de découverte vous permettent de sélectionner la version du protocole que vous souhaitez utiliser. Ce document décrit brièvement les paramètres liés au contrôle des versions.  
  
 Les classes de découverte suivantes ont désormais une propriété <xref:System.ServiceModel.Discovery.DiscoveryVersion> et prennent un argument <xref:System.ServiceModel.Discovery.DiscoveryVersion> dans leurs constructeurs :  
  
-   <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>  
  
-   <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>  
  
-   <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>  
  
-   <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>  
  
### <a name="discoveryversionwsdiscoveryapril2005"></a>DiscoveryVersion.WSDiscoveryApril2005  
 Fournissant <xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscoveryApril2005> en tant que constructeur paramètre utilise l’implémentation de la version d’avril 2005 du protocole WS-Discovery. Cette version correspond à la version publiée de la spécification du protocole WS-Discovery. Cette version doit être utilisée pour interopérer avec une application héritée utilisant la version de WS-Discovery d'avril 2005.  
  
### <a name="discoveryversionwsdiscovery11"></a>DiscoveryVersion.WSDiscovery11  
 La version de découverte par défaut utilisée par les API est <xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscovery11>. C'est la version standardisée actuelle du protocole WS-Discovery.  
  
## <a name="discoveryversionwsdiscoverycd1"></a>DiscoveryVersion.WSDiscoveryCD1  
 Si vous spécifiez <xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscoveryCD1> comme paramètre de constructeur, l'implémentation utilise la version Committee Draft 1 du protocole WS-Discovery. Cette version du protocole doit être utilisée pour interopérer avec les implémentations exécutant la version CD1 du protocole WS-Discovery.  
  
## <a name="supporting-multiple-udp-discovery-endpoints-for-different-discovery-versions-on-a-single-service-host"></a>Prise en charge de plusieurs points de terminaison de découverte UDP pour différentes versions de découverte sur un hôte de service unique  
 Vous pouvez exposer plusieurs points de terminaison de découverte UDP pour différentes versions de découverte sur un hôte de service unique. Pour ce faire, vous devez spécifier une adresse unique pour chaque point de terminaison de découverte UDP. L'exemple suivant montre comment effectuer cette opération.  
  
```  
UdpDiscoveryEndpoint newVersionUdpEndpoint = new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscovery11);  
UdpDiscoveryEndpoint oldVersionUdpEndpoint = new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscoveryApril2005);  
  
newVersionUdpEndpoint.Address = new EndpointAddress(newVersionUdpEndpoint.Address.Uri.ToString() + "/version11");  
oldVersionUdpEndpoint.Address = new EndpointAddress(oldVersionUdpEndpoint.Address.Uri.ToString() + "/versionAril2005");  
  
serviceHost.AddServiceEndpoint(newVersionUdpEndpoint);  
serviceHost.AddServiceEndpoint(oldVersionUdpEndpoint);  
```
