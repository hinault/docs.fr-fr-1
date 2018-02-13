---
title: Tracing and Message Logging
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
- Tracing and logging
ms.assetid: a4f39bfc-3c5e-4d51-a312-71c5c3ce0afd
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: cae7d806ce68f6804f97195c9bf2571328af6dff
ms.sourcegitcommit: f28752eab00d2bd97e971542c0f49ce63cfbc239
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2018
---
# <a name="tracing-and-message-logging"></a>Tracing and Message Logging
Cet exemple illustre comment activer l'enregistrement des suivis et des messages. Les suivis résultants et les journaux de messages sont affichés à l’aide de la [outil Service Trace Viewer (SvcTraceViewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md). Cet exemple est basé sur le [mise en route](../../../../docs/framework/wcf/samples/getting-started-sample.md).  
  
> [!NOTE]
>  La procédure d'installation ainsi que les instructions de génération relatives à cet exemple figurent à la fin de cette rubrique.  
  
## <a name="tracing"></a>Traçage  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] utilise le mécanisme de suivi défini dans l'espace de noms <xref:System.Diagnostics>. Dans ce modèle de suivi, les données de suivi sont générées par les sources de suivi implémentées par les applications. Chacune de ces sources est identifiée à l'aide d'un nom. Les consommateurs de suivis créent des écouteurs pour les sources de suivi à partir desquelles ils souhaitent récupérer des informations. Pour recevoir des données de suivi d'une source, vous devez créer un écouteur pour cette source. Dans [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], l'une des solutions pour ce faire consiste à ajouter le code suivant au fichier de configuration du service ou du client en définissant la source de suivi du modèle de service `switchValue` :  
  
```xml  
<system.diagnostics>  
    <sources>  
      <source name="System.ServiceModel" switchValue="Information,ActivityTracing"  
        propagateActivity="true">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
      <source name="System.ServiceModel.MessageLogging">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add initializeData="C:\logs\TracingAndLogging-service.svclog" type="System.Diagnostics.XmlWriterTraceListener"  
        name="xml" />  
    </sharedListeners>  
    <trace autoflush="true" />  
</system.diagnostics>  
```  
  
 Pour plus d’informations sur les sources de trace, consultez la section de la Source de Trace dans le [configuration du suivi](../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md) rubrique.  
  
## <a name="activity-tracing-and-propagation"></a>Suivi et propagation d'activité  
 Ayant `ActivityTracing` activé et `propagateActivity` la valeur `true` dans les `system.ServiceModel` des sources de trace pour le client et le service fournissent une corrélation de suivis dans des unités logiques de traitement (activités), entre les activités au sein des points de terminaison ( à travers des transferts d’activité) et entre les activités couvrant plusieurs points de terminaison (via la propagation d’ID d’activité).  
  
 Ces trois mécanismes (activités, transfert et propagation) peuvent vous permettre de localiser plus facilement la cause racine d’une erreur, notamment en utilisant l’outil Service Trace Viewer. Pour plus d’informations, consultez [à l’aide de Service Trace Viewer pour afficher les suivis corrélés et dépannage](../../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md).  
  
 Il est possible d'étendre le suivi fourni par le ServiceModel en créant des suivis d'activité définis par l'utilisateur. Les suivis d'activité définis par l'utilisateur permettent :  
  
-   De regrouper les suivis dans des unités logiques de travail.  
  
-   De mettre en relation les activités à l'aide du transfert et de la propagation.  
  
-   D'atténuer les pertes en termes de performances du suivi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] (par exemple, de diminuer l'espace disque occupé par le stockage des journaux).  
  
 Pour plus d’informations sur la trace de l’activité défini par l’utilisateur, consultez la [extension suivi](../../../../docs/framework/wcf/samples/extending-tracing.md) exemple.  
  
## <a name="message-logging"></a>Journalisation des messages  
 L'enregistrement des messages peut être activé à la fois sur le client et le service de toute application [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. Pour activer l'enregistrement des messages, vous devez ajouter le code suivant au client ou au service :  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <diagnostics>  
      <!-- Enable Message Logging here. -->  
      <!-- log all messages received or sent at the transport or service model levels -->  
      <messageLogging logEntireMessage="true"  
                      maxMessagesToLog="300"  
                      logMessagesAtServiceLevel="true"  
                      logMalformedMessages="true"  
                      logMessagesAtTransportLevel="true" />  
    </diagnostics>  
  </system.serviceModel>  
</configuration>  
```  
  
 Lorsqu'un message est enregistré, le type de suivi généré pour ce message n'est pas le même si ce message est suivi au niveau du client ou du serveur. Par exemple, le suivi du message « Add » est assuré dans la catégorie « TransportWrite », au niveau du client alors que son suivi est assuré dans la catégorie « TransportRead », au niveau du service.  
  
 Configurez l'écouteur de suivi en ajoutant le code suivant à la section <xref:System.Diagnostics> du fichier App.config du client ou du fichier Web.config du service :  
  
```xml  
<system.diagnostics>  
    <sources>  
      <source name="System.ServiceModel" switchValue="Information,ActivityTracing"  
        propagateActivity="true">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
      <source name="System.ServiceModel.MessageLogging">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add initializeData="C:\logs\TracingAndLogging-client.svclog" type="System.Diagnostics.XmlWriterTraceListener"  
        name="xml" />  
    </sharedListeners>  
    <trace autoflush="true" />  
  </system.diagnostics>  
```  
  
 Les messages sont enregistrés au format XML dans le fichier de configuration stocké dans le répertoire cible spécifié.  
  
> [!NOTE]
>  Les fichiers de suivi ne peuvent pas être créés si un répertoire de journal n'est pas créé auparavant. Assurez-vous que le répertoire C:\logs\ existe ou définissez un autre répertoire d'enregistrement dans la configuration de l'écouteur. Consultez les instructions initiales de configuration figurant en fin de rubrique pour plus d'informations.  
  
 Pour plus d’informations sur la journalisation des messages, consultez le [configuration de la journalisation du Message](../../../../docs/framework/wcf/diagnostics/configuring-message-logging.md) rubrique.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>Pour configurer, générer et exécuter l'exemple  
  
1.  Assurez-vous d’avoir effectué la [procédure d’installation d’à usage unique pour les exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Avant d'exécuter l'exemple Tracing and Message Logging, créez le répertoire C:\logs\ dans lequel le service stockera les fichiers .svclog. Le nom de ce répertoire est défini dans le fichier de configuration sous la forme d'un chemin d'accès indiquant où les suivis et les messages doivent être enregistrés. Ce chemin peut être modifié. Accordez à l'utilisateur des droits d'accès en écriture de service réseau au répertoire des journaux.  
  
3.  Pour générer l’édition c#, C++ ou Visual Basic .NET de la solution, suivez les instructions de [génération des exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
4.  Pour exécuter l’exemple dans une configuration à un ou plusieurs ordinateurs, suivez les instructions de [en cours d’exécution les exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  Les exemples peuvent déjà être installés sur votre ordinateur. Recherchez le répertoire (par défaut) suivant avant de continuer.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si ce répertoire n’existe pas, accédez à la page [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) pour télécharger tous les exemples [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] et [!INCLUDE[wf1](../../../../includes/wf1-md.md)] . Cet exemple se trouve dans le répertoire suivant.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\TracingAndLogging`  
  
## <a name="see-also"></a>Voir aussi  
 [Suivi](../../../../docs/framework/wcf/diagnostics/tracing/index.md)  
 [Exemples d’analyse AppFabric](http://go.microsoft.com/fwlink/?LinkId=193959)
