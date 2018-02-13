---
title: "Configuration simplifiée"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dcbe1f84-437c-495f-9324-2bc09fd79ea9
caps.latest.revision: "10"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 334dfce44b1f0a7b6b38f509f2f0a346ef90630f
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="simplified-configuration"></a>Configuration simplifiée
La configuration de services [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] peut s'avérer une tâche complexe. Il existe de nombreuses options différentes et il n'est pas toujours évident de déterminer les paramètres nécessaires. Bien que les fichiers de configuration augmentent la flexibilité des services [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], ils sont également la source de nombreux problèmes difficiles à détecter. [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] traite ces problèmes et permet de réduire la taille et la complexité de la configuration de service.  
  
## <a name="simplified-configuration"></a>Configuration simplifiée  
 Dans les fichiers de configuration de service [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], la section <`system.serviceModel`> contient un élément <`service`> pour chaque service hébergé. L'élément <`service`> contient une collection d'éléments <`endpoint`> qui spécifient les points de terminaison exposés pour chaque service et éventuellement un jeu de comportements de service. Les éléments <`endpoint`> spécifient l'adresse, la liaison et le contrat exposés par le point de terminaison, et éventuellement une configuration de liaison et des comportements de point de terminaison. La section <`system.serviceModel`> contient également un élément <`behaviors`> qui vous permet de spécifier des comportements de service ou de point de terminaison. L'exemple suivant présente la section <`system.serviceModel`> d'un fichier de configuration.  
  
```  
<system.serviceModel>  
  <behaviors>  
    <serviceBehaviors>  
      <behavior name="MyServiceBehavior">  
        <serviceMetadata httpGetEnabled="true">  
        <serviceDebug includeExceptionDetailInFaults="false">  
      </behavior>  
    </serviceBehaviors>  
  </behaviors>  
  <bindings>  
   <basicHttpBinding>  
      <binding name=MyBindingConfig"  
               maxBufferSize="100"  
               maxReceiveBufferSize="100" />  
   </basicHttpBinding>  
   </bindings>   <services>  
    <service behaviorConfiguration="MyServiceBehavior"  
             name="MyService">  
      <endpoint address=""  
                binding="basicHttpBinding"  
                contract="ICalculator"  
                bindingConfiguration="MyBindingConfig" />  
      <endpoint address="mex"  
                binding="mexHttpBinding"  
                contract="IMetadataExchange"/>  
    </service>  
  </services>  
</system.serviceModel>  
```  
  
 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] simplifie la configuration d'un service [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] en supprimant la nécessité de l'élément <`service`>. Si vous n'ajoutez pas de section <`service`> ou de points de terminaison dans la section <`service`> et si votre service ne définit aucun point de terminaison par programmation, un jeu de points de terminaison par défaut est automatiquement ajouté à votre service : un pour chaque adresse de base de service et pour chaque contrat implémenté par votre service. Dans chacun de ces points de terminaison, l'adresse du point de terminaison correspond à l'adresse de base, la liaison est déterminée par le schéma d'adresse de base et le contrat est celui implémenté par votre service. Si vous n'avez pas besoin de spécifier de comportements de point de terminaison ou de service, ni de modifier un paramètre de liaison, il est inutile de spécifier un fichier de configuration de service. Si un service implémente deux contrats et que l'hôte active à la fois les transports HTTP et TCP, l'hôte de service crée quatre points de terminaison par défaut, un pour chaque contrat utilisant chaque transport. Pour créer des points de terminaison par défaut, l'hôte de service doit savoir quelles liaisons utiliser. Ces paramètres sont spécifiés dans une section <`protocolMappings`> à l'intérieur de la section <`system.serviceModel`>. La section <`protocolMappings`> contient une liste de schémas de protocole de transport mappés aux types de liaison. L'hôte du service utilise les adresses de base qui lui sont transmises pour déterminer quelle liaison utiliser. L'exemple suivant utilise l'élément <`protocolMappings`>.  
  
> [!WARNING]
>  Le fait de modifier les éléments de configuration par défaut, comme les liaisons ou les comportements, peut affecter les services définis dans les niveaux inférieurs de la hiérarchie de configuration, car ces derniers peuvent utiliser ces liaisons et comportements par défaut. C'est pourquoi, la personne qui modifie les liaisons et comportements par défaut doit savoir que ces changements peuvent affecter d'autres services dans la hiérarchie.  
  
> [!NOTE]
>  Les services hébergés dans les services IIS (Internet Information Services) ou WAS (Windows Process Activation Service) utilisent le répertoire virtuel comme leur adresse de base.  
  
```xml  
<protocolMapping>  
  <add scheme="http"     binding="basicHttpBinding" bindingConfiguration="MyBindingConfiguration"/>  
  <add scheme="net.tcp"  binding="netTcpBinding"/>  
  <add scheme="net.pipe" binding="netNamedPipeBinding"/>  
  <add scheme="net.msmq" binding="netMSMQBinding"/>  
</protocolMapping>  
```  
  
 Dans l'exemple précédent, un point de terminaison avec une adresse de base commençant par le schéma « http » utilise la liaison <xref:System.ServiceModel.BasicHttpBinding>. Un point de terminaison avec une adresse de base commençant par le schéma « net.tcp » utilise la liaison <xref:System.ServiceModel.NetTcpBinding>. Vous pouvez remplacer des paramètres dans un fichier local App.config ou Web.config.  
  
 Chaque élément dans la section <`protocolMappings`> doit spécifier un schéma et une liaison. Éventuellement, il peut spécifier un attribut `bindingConfiguration` qui indique une configuration de liaison dans la section <`bindings`> du fichier de configuration. Si aucun attribut `bindingConfiguration` n'est spécifié, la configuration de liaison anonyme du type de liaison approprié est utilisée.  
  
 Les comportements de service sont configurés pour les points de terminaison par défaut à l'aide des sections <`behavior`> anonymes à l'intérieur des sections <`serviceBehaviors`>. Les éléments <`behavior`> sans nom dans <`serviceBehaviors`> sont utilisés pour configurer des comportements de service. Par exemple, le fichier de configuration suivant permet la publication de métadonnées de service pour tous les services qui se trouvent dans l'hôte.  
  
```xml  
<system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>    <!-- No <service> tag is necessary. Default endpoints are added to the service -->  
    <!-- The service behavior with name="" is picked up by the service -->  
 </system.serviceModel>  
```  
  
 Les comportements de point de terminaison sont configurés à l'aide des sections <`behavior`> anonymes à l'intérieur des sections <`serviceBehaviors`>.  
  
 L'exemple suivant est un fichier de configuration équivalent à celui qui se trouve au début de cette rubrique. Il utilise le modèle de configuration simplifié.  
  
```xml  
<system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="false"/>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>    <bindings>  
       <basicHttpBinding>  
          <binding maxBufferSize="100"  
                   maxReceiveBufferSize="100" />  
       </basicHttpBinding>  
    </bindings>    <!-- No <service> tag is necessary. Default endpoints will be added to the service -->  
    <!-- The service behavior with name="" will be picked up by the service -->  
    <protocolMapping>  
      <add scheme="http"     binding="basicHttpBinding" / </protocolMapping>  
  </system.serviceModel>  
```  
  
> [!IMPORTANT]
>  Cette fonctionnalité concerne uniquement la configuration du service WCF, non la configuration du client. La plupart de temps, la configuration cliente WCF est générée par un outil comme svcutil.exe ou en ajoutant une référence de service à partir de Visual Studio. Si vous configurez manuellement un client WCF, vous devrez ajouter un \<client > élément à la configuration et spécifiez les points de terminaison que vous souhaitez appeler.  
  
## <a name="see-also"></a>Voir aussi  
 [Configuration des services à l’aide de fichiers de configuration](../../../docs/framework/wcf/configuring-services-using-configuration-files.md)  
 [Configuration de liaisons pour les services](../../../docs/framework/wcf/configuring-bindings-for-wcf-services.md)  
 [Configuration des liaisons fournies par le système](../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)  
 [Configuration des services](../../../docs/framework/wcf/configuring-services.md)  
 [Configuration des applications Windows Communication Foundation](http://msdn.microsoft.com/library/13cb368e-88d4-4c61-8eed-2af0361c6d7a)  
 [Configuration des services WCF dans le code](../../../docs/framework/wcf/configuring-wcf-services-in-code.md)
