---
title: "Design Patterns : List-Based Publish-Subscribe"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f4257abc-12df-4736-a03b-0731becf0fd4
caps.latest.revision: "16"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 9f5d9b334aae1607f4fb46e0b41155b50eb95a46
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="design-patterns-list-based-publish-subscribe"></a>Design Patterns : List-Based Publish-Subscribe
Cet exemple illustre le modèle de publication/abonnement basé sur une liste implémenté en tant que programme [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
> [!NOTE]
>  La procédure d'installation ainsi que les instructions de génération relatives à cet exemple figurent à la fin de cette rubrique.  
  
 Le modèle de conception basé sur liste publication-abonnement est décrit dans la publication Microsoft Patterns & Practices, [modèles d’intégration](http://go.microsoft.com/fwlink/?LinkId=95894). Le modèle de publication/abonnement transmet des informations à une collection des destinataires qui se sont abonnés une rubrique d’informations. Ce modèle gère une liste d'abonnés. Lorsque des informations doivent être partagées, une copie est envoyée à chaque abonné de la liste. Cet exemple illustre un modèle de publication/abonnement basé sur liste dynamique, où les clients peuvent s'abonner ou annuler leur abonnement aussi souvent que nécessaire.  
  
 Il se compose d'un client, d'un service et d'un programme de source de données. Il peut y avoir plusieurs clients et plusieurs programmes de source de données en cours d'exécution. Les clients s'abonnent au service, reçoivent des notifications et annulent leur abonnement. Les programmes de source de données envoient des informations au service à partager avec tous les abonnés actuels.  
  
 Dans cet exemple, le client et la source de données sont des programmes de console (fichiers .exe) et le service est une bibliothèque (.dll) hébergée par les services Internet (IIS). L'activité du client et de la source de données sont visibles sur le Bureau.  
  
 Le service utilise la communication duplex. Le contrat de service `ISampleContract` est associé à un contrat de rappel `ISampleClientCallback`. Le service implémente les opérations d'abonnement et d'annulation d'abonnement que les clients utilisent pour rejoindre ou quitter la liste des abonnés. Le service implémente également l'opération de service `PublishPriceChange` que le programme de source de données appelle pour fournir le service avec de nouvelles informations. Le logiciel client implémente l'opération de service `PriceChange` que le service appelle pour prévenir tous les abonnés d'une modification de prix.  
  
```  
// Create a service contract and define the service operations.  
// NOTE: The service operations must be declared explicitly.  
[ServiceContract(SessionMode=SessionMode.Required,  
      CallbackContract=typeof(ISampleClientContract))]  
public interface ISampleContract  
{  
    [OperationContract(IsOneWay = false, IsInitiating=true)]  
    void Subscribe();  
    [OperationContract(IsOneWay = false, IsTerminating=true)]  
    void Unsubscribe();  
    [OperationContract(IsOneWay = true)]  
    void PublishPriceChange(string item, double price,   
                                     double change);  
}  
  
public interface ISampleClientContract  
{  
    [OperationContract(IsOneWay = true)]  
    void PriceChange(string item, double price, double change);  
}  
```  
  
 Le service utilise un événement .NET Framework comme mécanisme pour informer tous les abonnés à propos des nouvelles informations. Lorsqu'un client rejoint le service en appelant l'opération d'abonnement, il fournit un gestionnaire d'événements. Lorsqu'un client part, il annule son gestionnaire d'événements de l'événement. Lorsqu'une source de données appelle le service pour signaler une modification de prix, le service déclenche l'événement. Il appelle chaque instance du service, une pour chaque client qui s'est abonné, et entraîne l'exécution de leurs gestionnaires d'événements. Chaque gestionnaire d'événements transmet les informations à son client via sa fonction de rappel.  
  
```  
public class PriceChangeEventArgs : EventArgs  
    {  
        public string Item;  
        public double Price;  
        public double Change;  
    }  
  
    // The Service implementation implements your service contract.  
    [ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]  
    public class SampleService : ISampleContract  
    {  
        public static event PriceChangeEventHandler PriceChangeEvent;  
        public delegate void PriceChangeEventHandler(object sender, PriceChangeEventArgs e);  
  
        ISampleClientContract callback = null;  
  
        PriceChangeEventHandler priceChangeHandler = null;  
  
        //Clients call this service operation to subscribe.  
        //A price change event handler is registered for this client instance.  
  
        public void Subscribe()  
        {  
            callback = OperationContext.Current.GetCallbackChannel<ISampleClientContract>();  
            priceChangeHandler = new PriceChangeEventHandler(PriceChangeHandler);  
            PriceChangeEvent += priceChangeHandler;  
        }  
  
        //Clients call this service operation to unsubscribe.  
        //The previous price change event handler is deregistered.  
  
        public void Unsubscribe()  
        {  
            PriceChangeEvent -= priceChangeHandler;  
        }  
  
        //Information source clients call this service operation to report a price change.  
        //A price change event is raised. The price change event handlers for each subscriber will execute.  
  
        public void PublishPriceChange(string item, double price, double change)  
        {  
            PriceChangeEventArgs e = new PriceChangeEventArgs();  
            e.Item = item;  
            e.Price = price;  
            e.Change = change;  
            PriceChangeEvent(this, e);  
        }  
  
        //This event handler runs when a PriceChange event is raised.  
        //The client's PriceChange service operation is invoked to provide notification about the price change.  
  
        public void PriceChangeHandler(object sender, PriceChangeEventArgs e)  
        {  
            callback.PriceChange(e.Item, e.Price, e.Change);  
        }  
  
    }  
```  
  
 Lorsque vous exécutez l'exemple, lancez plusieurs clients. Les clients s'abonnent au service. Exécutez ensuite le programme de source de données qui envoie des informations au service. Le service transmet les informations à tous les abonnés. Vous pouvez consulter l'activité sur chaque console cliente qui confirme que les informations ont été reçues. Appuyez sur Entrée dans la fenêtre du client pour l'arrêter.  
  
### <a name="to-set-up-and-build-the-sample"></a>Pour configurer et générer l'exemple  
  
1.  Assurez-vous d’avoir effectué la [procédure d’installation d’à usage unique pour les exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Pour générer l’édition C# ou Visual Basic .NET de la solution, conformez-vous aux instructions figurant dans [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
### <a name="to-run-the-sample-on-the-same-machine"></a>Pour exécuter l'exemple sur le même ordinateur  
  
1.  Assurez-vous que le service est accessible en saisissant l'adresse http://localhost/servicemodelsamples/service.svc dans un navigateur. Une page de confirmation doit s'afficher en réponse.  
  
2.  Exécutez Client.exe à partir de \client\bin\\, figurant dans le dossier de langue. L'activité du client s'affiche dans sa fenêtre de console. Lancez plusieurs clients.  
  
3.  Exécutez Datasource.exe à partir de \datasource\bin\\, figurant dans le dossier de langue. L'activité de source de données est affichée sur la fenêtre de console. Une fois que la source de données envoie des informations au service, elles doivent être transmises à chaque client.  
  
4.  Si le client, la source de données et les programmes de service ne sont pas en mesure de communiquer, consultez [conseils de dépannage](http://msdn.microsoft.com/library/8787c877-5e96-42da-8214-fa737a38f10b).  
  
### <a name="to-run-the-sample-across-machines"></a>Pour exécuter l'exemple sur plusieurs ordinateurs  
  
1.  Installez l'ordinateur de service:  
  
    1.  Créez un répertoire virtuel nommé ServiceModelSamples sur l'ordinateur de service. Le traitement du fichier Setupvroot.bat à partir de la [procédure d’installation d’à usage unique pour les exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md) peut être utilisé pour créer le répertoire de disque et le répertoire virtuel.  
  
    2.  Copiez les fichiers du programme de service depuis %SystemDrive%\Inetpub\wwwroot\servicemodelsamples vers le répertoire virtuel ServiceModelSamples. Assurez-vous d'intégrer les fichiers au répertoire \bin.  
  
    3.  Assurez-vous que le service est accessible depuis l'ordinateur du client en utilisant un navigateur.  
  
2.  Installez les ordinateurs clients :  
  
    1.  Copiez les fichiers de programme client du dossier \client\bin\ (situé dans le dossier correspondant à votre langue) sur l'ordinateur client.  
  
    2.  Dans chaque fichier de configuration client, modifiez l'adresse de la définition du point de terminaison afin qu'elle corresponde à la nouvelle adresse de votre service. Remplacez toutes les occurrences de « localhost » de l'adresse par un nom de domaine complet.  
  
3.  Installez l'ordinateur de source de données:  
  
    1.  Copiez les fichiers du programme de source de données du dossier \datasource\bin\ (dans le dossier correspondant à votre langue) sur l'ordinateur de source de données.  
  
    2.  Dans le fichier de configuration de la source de données, modifiez l'adresse de la définition du point de terminaison afin qu'elle corresponde à la nouvelle adresse de votre service. Remplacez toutes les occurrences de « localhost » de l'adresse par un nom de domaine complet.  
  
4.  Sur les ordinateurs clients, lancez Client.exe à partir d'une invite de commandes.  
  
5.  Sur l'ordinateur de source de données, lancez Datasource.exe à partir d'une invite de commandes.  
  
> [!IMPORTANT]
>  Les exemples peuvent déjà être installés sur votre ordinateur. Recherchez le répertoire (par défaut) suivant avant de continuer.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si ce répertoire n’existe pas, accédez à la page [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) pour télécharger tous les exemples [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] et [!INCLUDE[wf1](../../../../includes/wf1-md.md)] . Cet exemple se trouve dans le répertoire suivant.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Scenario\DesignPatterns/ListBasedPublishSubscribe`  
  
## <a name="see-also"></a>Voir aussi
