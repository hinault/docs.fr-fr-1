---
title: "Comment : installer et configurer des composants d'activation WCF"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: HTTP activation [WCF]
ms.assetid: 33a7054a-73ec-464d-83e5-b203aeded658
caps.latest.revision: "16"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 78c63fe58872097058292a8b100b376959a2a0b2
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-install-and-configure-wcf-activation-components"></a>Comment : installer et configurer des composants d'activation WCF
Cette rubrique décrit les étapes requises pour configurer le service d'activation de processus de Windows (également appelé service WAS) dans [!INCLUDE[wv](../../../../includes/wv-md.md)] pour héberger des services [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] qui ne communiquent pas sur des protocoles réseau HTTP. Les sections suivantes définissent les étapes pour cette configuration :  
  
-   Installer (ou vérifier l'installation) des composants d'activation [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
-   Configurer le service WAS pour prendre en charge un protocole non HTTP. La procédure suivante configure [!INCLUDE[wv](../../../../includes/wv-md.md)] pour l'activation TCP.  
  
 Une fois l’installation et configuration du service WAS, voir [Comment : héberger un Service WCF dans WAS](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md) pour les procédures pour créer un [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] service qui expose un point de terminaison non-HTTP qui utilise le service WAS.  
  
### <a name="to-install-the-wcf-non-http-activation-components"></a>Pour installer les composants d'activation non HTTP WCF  
  
1.  Cliquez sur le **Démarrer** bouton, puis cliquez sur **le panneau de configuration**.  
  
2.  Cliquez sur **programmes**, puis cliquez sur **programmes et fonctionnalités**.  
  
3.  Sur le **tâches** menu, cliquez sur **ou désactiver des fonctionnalités Windows d’activer**.  
  
4.  Recherchez le noeud [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)], sélectionnez-le puis développez-le.  
  
5.  Sélectionnez le **les composants d’Activation Non-Http WCF** zone et d’enregistrer le paramètre.  
  
### <a name="to-configure-the-was-to-support-tcp-activation"></a>Pour configurer le service WAS pour prendre en charge l'activation TCP  
  
1.  Pour assurer la prise en charge de l'activation de net.tcp, le site Web par défaut doit d'abord être lié à un port net.tcp. Vous pouvez utiliser Appcmd.exe installé avec l'ensemble d'outils de gestion [!INCLUDE[iisver](../../../../includes/iisver-md.md)]. Dans une fenêtre d'invite de commandes au niveau de l'administrateur, exécutez la commande suivante.  
  
    ```  
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site" -+bindings.[protocol='net.tcp',bindingInformation='808:*']  
    ```  
  
    > [!NOTE]
    >  Cette commande est une ligne unique de texte. Cette commande ajoute une liaison de site net.tcp au site web par défaut qui écoute sur le port TCP 808, quel que soit le nom d’hôte.  
  
2.  Bien que toutes les applications d’un site partagent la même liaison net.tcp, chacune d’elle peut activer de manière individuelle la prise en charge net.pipe. Afin d'activer net.tcp pour l'application, exécutez la commande suivante à partir d'une invite de commandes au niveau de l'administrateur.  
  
    ```  
    %windir%\system32\inetsrv\appcmd.exe set app   
    "Default Web Site/<WCF Application>" /enabledProtocols:http,net.tcp  
    ```  
  
    > [!NOTE]
    >  Cette commande est une ligne unique de texte. Cette commande active le /\<*Application WCF*> application accessible à l’aide de deux http://localhost*/\<Application WCF >* et net.tcp:// localhost /*\<Application WCF >*.  
  
     Supprimez la liaison de site net.tcp que vous avez ajoutée dans le cadre de cet exemple.  
  
     Pour des raisons pratiques, les deux étapes suivantes sont implémentées dans le fichier de commandes RemoveNetTcpSiteBinding.cmd situé dans le répertoire de l'exemple.  
  
    1.  Supprimez le protocole net.tcp de la liste des protocoles activés en exécutant la commande suivante dans une invite de commandes au niveau de l'administrateur.  
  
        ```  
        %windir%\system32\inetsrv\appcmd.exe set app   
        "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http  
        ```  
  
        > [!NOTE]
        >  Cette commande est une ligne unique de texte.  
  
    2.  Supprimez la liaison du site net.tcp en exécutant la commande suivante dans une invite de commandes de niveau élevé :  
  
        ```  
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"   
        --bindings.[protocol='net.tcp',bindingInformation='808:*']  
        ```  
  
        > [!NOTE]
        >  Cette commande est une ligne unique de texte.  
  
### <a name="to-remove-nettcp-from-the-list-of-enabled-protocols"></a>Pour supprimer net.tcp de la liste des protocoles actifs  
  
1.  Pour supprimer net.tcp de la liste des protocoles actifs, exécutez la commande suivante dans une invite de commandes au niveau de l'administrateur.  
  
    ```  
    %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http  
    ```  
  
    > [!NOTE]
    >  Cette commande est une ligne unique de texte.  
  
### <a name="to-remove-the-nettcp-site-binding"></a>Pour supprimer la liaison de site net.tcp  
  
1.  Pour supprimer la liaison de site net.tcp, exécutez la commande suivante dans une fenêtre d'invite de commandes au niveau de l'administrateur.  
  
    ```  
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"   
    -bindings.[protocol='net.tcp',bindingInformation='808:*']  
    ```  
  
    > [!NOTE]
    >  Cette commande est une ligne unique de texte.  
  
## <a name="see-also"></a>Voir aussi  
 [Activation TCP](../../../../docs/framework/wcf/samples/tcp-activation.md)  
 [Activation MSMQ](../../../../docs/framework/wcf/samples/msmq-activation.md)  
 [Activation de NamedPipe](../../../../docs/framework/wcf/samples/namedpipe-activation.md)  
 [Fonctionnalités d’hébergement de Windows Server App Fabric](http://go.microsoft.com/fwlink/?LinkId=201276)
