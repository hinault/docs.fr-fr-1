---
title: Mise en route Tutorial1
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WCF [WCF], getting started
- Windows Communication Foundation [WCF], getting started
- getting started [WCF]
ms.assetid: df939177-73cb-4440-bd95-092a421516a1
caps.latest.revision: "47"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 74a322730c5e9fc205097da310a8db1fd7c50f82
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="getting-started-tutorial"></a>Didacticiel de mise en route
Les rubriques contenues dans cette section visent à vous donner un aperçu de la programmation de [!INCLUDE[indigo1](../../../includes/indigo1-md.md)]. Elles doivent être parcourues dans l'ordre de la liste indiquée au bas de cette rubrique. En suivant ce didacticiel, vous aurez une compréhension de base des étapes requises pour créer un service et des applications clientes [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]. Un service expose un ou plusieurs points de terminaison, chaque point de terminaison exposant une ou plusieurs opérations de service. Le *point de terminaison* d’un service spécifie une adresse où le service peut être trouvé, une liaison qui contient les informations qui décrivent comment un client doit communiquer avec le service et un contrat qui définit les fonctionnalités fournie par le service pour ses clients.  
  
 Une fois que vous aurez terminé la séquence de rubriques de ce didacticiel, vous disposerez d'un service opérationnel et d'un client qui appelle le service. Les trois premières rubriques décrivent comment définir un contrat de service, comment implémenter le contrat de service et comment héberger le service. Le service créé est auto-hébergé dans une application console. Les services peuvent également être hébergés sous IIS (Internet Information Services). [!INCLUDE[crabout](../../../includes/crabout-md.md)]comment procéder, consultez [Comment : héberger un Service WCF dans IIS](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md). Le service est configuré dans le code ; toutefois, les services peuvent également être configurés dans un fichier de configuration. [!INCLUDE[crabout](../../../includes/crabout-md.md)]reportez-vous à l’aide d’un fichier de configuration [fichiers de configuration des Services à l’aide de la Configuration](../../../docs/framework/wcf/configuring-services-using-configuration-files.md).  
  
 Les trois rubriques suivantes décrivent comment créer un proxy client, comment configurer l'application cliente et comment utiliser le proxy client pour appeler l'opération de service exposée par le service. Les services publient les métadonnées qui définissent les informations dont une application cliente a besoin pour communiquer avec le service. [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] automatise le processus d'accès à ces métadonnées et l'utilise pour créer et configurer l'application cliente pour le service. Si vous n’utilisez pas [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)], vous pouvez utiliser la [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) pour créer et configurer l’application cliente pour le service.  
  
 Toutes les rubriques de cette section partent du principe que vous utilisez Visual Studio 2011 comme environnement de développement. Si vous utilisez un autre environnement de développement, ignorez les instructions spécifiques à [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)].  
  
> [!NOTE]
>  Si vous exécutez [!INCLUDE[wv](../../../includes/wv-md.md)] ou versions ultérieures du système d’exploitation Windows, vous devez démarrer [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] en allant dans le menu Démarrer et en cliquant avec le bouton droit sur Visual Studio 2011 et en sélectionnant **exécuter en tant qu’administrateur**. Pour toujours lancer Visual Studio 2011 en tant qu’un administrateur, vous pouvez créer un raccourci, cliquez avec le bouton droit sur le raccourci, sélectionnez Propriétés, sélectionnez le **compatibilité** et vérifiez la **exécuter ce programme en tant qu’administrateur** case à cocher. Lorsque vous démarrez Visual Studio 2011 à partir de ce raccourci, l'application s'exécute systématiquement en tant qu'administrateur.  
  
 Pour des exemples d’applications qui peuvent être téléchargés sur votre disque dur et s’exécutent, consultez les rubriques de [exemples Windows Communication Foundation](http://msdn.microsoft.com/library/8ec9d192-5d81-4f64-bfd3-90c5e5858c91). Cette rubrique, consultez en particulier, la [mise en route](../../../docs/framework/wcf/samples/getting-started-sample.md).  
  
 Pour plus d’informations sur la création de services et les clients, consultez [programmation WCF de base](../../../docs/framework/wcf/basic-wcf-programming.md).  
  
## <a name="in-this-section"></a>Dans cette section  
 [Guide pratique pour définir un contrat de service](../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md)  
 Décrit comment créer un contrat [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] à l'aide d'une interface définie par l'utilisateur. Le contrat définit les fonctionnalités exposées par le service.  
  
 [Guide pratique pour implémenter un contrat de service](../../../docs/framework/wcf/how-to-implement-a-wcf-contract.md)  
 Décrit comment implémenter un contrat de service. Une fois qu'un contrat est défini, il doit être implémenté avec une classe de service.  
  
 [Guide pratique pour héberger et exécuter un service de base](../../../docs/framework/wcf/how-to-host-and-run-a-basic-wcf-service.md)  
 Décrit comment configurer un point de terminaison pour le service dans du code et comment héberger le service dans une application console. Pour qu'il devienne actif, un service doit être configuré et hébergé dans un environnement d'exécution. Cet environnement crée le service et contrôle son contexte et sa durée de vie.  
  
 [Guide pratique pour créer un client](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)  
 Décrit comment extraire les métadonnées utilisées pour créer un proxy client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] à partir d'un service [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]. Ce processus utilise la fonctionnalité Ajouter une référence de service dans Visual Studio 2011.  
  
 [Guide pratique pour configurer un client](../../../docs/framework/wcf/how-to-configure-a-basic-wcf-client.md)  
 Décrit comment configurer un client WCF. La configuration du client nécessite la spécification du point de terminaison que le client utilise pour accéder au service.  
  
 [Guide pratique pour utiliser un client](../../../docs/framework/wcf/how-to-use-a-wcf-client.md)  
 Décrit comment utiliser le proxy client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] pour appeler des opérations de service.  
  
## <a name="reference"></a>Référence  
 <xref:System.ServiceModel.ServiceContractAttribute>  
  
 <xref:System.ServiceModel.OperationContractAttribute>  
  
## <a name="related-sections"></a>Rubriques connexes  
 [Exemples Windows Communication Foundation](http://msdn.microsoft.com/library/8ec9d192-5d81-4f64-bfd3-90c5e5858c91)  
  
 [Cycle de vie de la programmation de base](../../../docs/framework/wcf/basic-programming-lifecycle.md)  
  
## <a name="see-also"></a>Voir aussi  
 [Vue d’ensemble conceptuelle](../../../docs/framework/wcf/conceptual-overview.md)  
 [Guide de la documentation](../../../docs/framework/wcf/guide-to-the-documentation.md)  
 [Présentation de Windows Communication Foundation](../../../docs/framework/wcf/whats-wcf.md)  
 [Informations détaillées sur les fonctionnalités de WCF](../../../docs/framework/wcf/feature-details/index.md)
