---
title: "Activité personnalisée SendMail"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 947a9ae6-379c-43a3-9cd5-87f573a5739f
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 6086ca0ccb31603874feda6df1384b9346adb49d
ms.sourcegitcommit: cf22b29db780e532e1090c6e755aa52d28273fa6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="sendmail-custom-activity"></a>Activité personnalisée SendMail
Cet exemple montre comment créer une activité personnalisée dérivée de <xref:System.Activities.AsyncCodeActivity> pour envoyer du courrier à l'aide de SMTP afin de l'utiliser dans une application de workflow. L’activité personnalisée utilise les fonctionnalités de <xref:System.Net.Mail.SmtpClient> d’envoyer par courrier électronique de manière asynchrone et d’envoyer des messages avec l’authentification. Elle fournit aussi certaines fonctionnalités d’utilisateur final telles que le mode Test, le remplacement des jetons, les modèles de fichier et le chemin d’accès de dépôt de test.  
  
 Le tableau suivant décrit en détail les arguments pour l'activité `SendMail`.  
  
|Nom|Type|Description|  
|-|-|-|  
|Host|Chaîne|Adresse du serveur hôte SMTP.|  
|Port|Chaîne|Port du service SMTP dans l'hôte.|  
|EnableSsl|bool|Indique si <xref:System.Net.Mail.SmtpClient> utilise le protocole SSL (Secure Sockets Layer) pour chiffrer la connexion.|  
|UserName|Chaîne|Nom d'utilisateur pour définir les informations d'identification utilisées pour authentifier la propriété <xref:System.Net.Mail.SmtpClient.Credentials%2A> de l'expéditeur.|  
|Mot de passe|Chaîne|Mot de passe pour définir les informations d'identification utilisées pour authentifier la propriété <xref:System.Net.Mail.SmtpClient.Credentials%2A> de l'expéditeur.|  
|Objet|<xref:System.Activities.InArgument%601>\<string>|Sujet du message.|  
|Corps|<xref:System.Activities.InArgument%601>\<string>|Corps du message.|  
|Pièces jointes|<xref:System.Activities.InArgument%601>\<string>|Collection de pièces jointes utilisée pour stocker des données jointes à ce message électronique.|  
|From|<xref:System.Net.Mail.MailAddress>|Adresse d’origine de ce message électronique.|  
|À|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>>|Collection d’adresses qui contient les destinataires de ce message électronique.|  
|CC|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>>|Collection d’adresses qui contient les destinataires de copie carbone (CC) pour ce message électronique.|  
|BCC|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>>|Collection d’adresses qui contient les destinataires de copie carbone invisible (Cci) pour ce message électronique.|  
|jetons|<xref:System.Activities.InArgument%601><IDictionary\<string, string>>|Jetons à remplacer dans le corps. Cette fonctionnalité permet aux utilisateurs de spécifier certaines valeurs dans le corps qui peuvent être remplacées ultérieurement par les jetons fournis à l'aide de cette propriété.|  
|BodyTemplateFilePath|Chaîne|Chemin d'accès à un modèle de corps. L'activité `SendMail` copie le contenu de ce fichier dans sa propriété de corps.<br /><br /> Ce modèle peut contenir des jetons qui sont remplacés par le contenu de la propriété des jetons.|  
|TestMailTo|<xref:System.Net.Mail.MailAddress>|Lorsque cette propriété est définie, tous les messages électroniques sont envoyés à l’adresse spécifiée.<br /><br /> Cette propriété n'est pas conçue pour une utilisation lors du test des workflows. Par exemple, lorsque vous souhaitez vous assurer que tous les messages électroniques sont envoyés sans les envoyer aux destinataires réels.|  
|TestDropPath|Chaîne|Lorsque cette propriété est définie, tous les messages électroniques sont également enregistrés dans le fichier spécifié.<br /><br /> Cette propriété est destinée à être utilisée lorsque vous testez ou déboguer des workflows, pour vous assurer que le format et le contenu des messages électroniques sortants est appropriée.|  
  
## <a name="solution-contents"></a>Contenu de la solution  
 La solution contient deux projets.  
  
|Project|Description|Fichiers importants|  
|-------------|-----------------|---------------------|  
|SendMail|Activité SendMail|1.  SendMail.cs : implémentation pour l'activité principale<br />2.  SendMailDesigner.xaml et SendMailDesigner.xaml.cs : concepteur pour l'activité SendMail<br />3.  MailTemplateBody.htm : modèle pour le message électronique à envoyer.|  
|SendMailTestClient|Client pour tester l'activité SendMail.  Ce projet illustre deux façons d'appeler l'activité SendMail : déclarative et par programme.|1.  Sequence1.xaml : workflow qui appelle l'activité SendMail.<br />2.  Program.cs : appelle Sequence1 et crée par programmation un workflow qui utilise SendMail.|  
  
## <a name="further-configuration-of-the-sendmail-activity"></a>Configuration supplémentaire de l'activité SendMail  
 Bien qu'elle ne soit pas illustrée dans l'exemple, les utilisateurs peuvent effectuer une configuration supplémentaire de l'activité SendMail. Les trois sections suivantes montrent comment procéder.  
  
### <a name="sending-an-email-using-tokens-specified-in-the-body"></a>Envoi d'un message électronique à l'aide de jetons spécifiés dans le corps  
 Cet extrait de code montre comment envoyer un message électronique avec des jetons dans le corps. Notez la façon dont les jetons sont fournis dans la propriété de corps. Les valeurs pour ces jetons sont fournies à la propriété de jetons.  
  
```html  
IDictionary<string, string> tokens = new Dictionary<string, string>();  
tokens.Add("@name", "John Doe");  
tokens.Add("@date", DateTime.Now.ToString());  
tokens.Add("@server", "localhost");  
  
new SendMail  
{  
    From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
    To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
    Subject = "Test email",  
    Body = "Hello @name. This is a test email sent from @server. Current date is @date",  
    Host = "localhost",  
    Port = 25,  
    Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens)  
};  
```  
  
### <a name="sending-an-email-using-a-template"></a>Envoi d'un message électronique à l'aide d'un modèle  
 Cet extrait de code montre comment envoyer un message électronique à l'aide de jetons de modèle dans le corps. Notez que lorsque vous définissez la propriété `BodyTemplateFilePath`, il n'est pas nécessaire de fournir la valeur pour la propriété Body (le contenu du modèle sera copié dans le corps).  
  
```  
new SendMail  
{    
    From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
    To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
    Subject = "Test email",  
    Host = "localhost",  
    Port = 25,  
    Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens),  
    BodyTemplateFilePath = @"..\..\..\SendMail\Templates\MailTemplateBody.htm",   
};  
```  
  
### <a name="sending-mails-in-testing-mode"></a>Envoi de messages électronique en mode Test  
 Cet extrait de code montre comment définir les deux propriétés de tests : en définissant `TestMailTo` vers tous les messages seront envoyés à john.doe@contoso.con (sans tenir compte des valeurs de, Cc, Cci). En définissant TestDropPath, tous les messages électroniques sortants seront aussi enregistrés dans le chemin d’accès fourni. Ces propriétés peuvent être définies indépendamment (elles ne sont pas liées).  
  
```  
new SendMail  
{    
   From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
   To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
   Subject = "Test email",  
   Host = "localhost",  
   Port = 25,  
   Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens),  
   BodyTemplateFilePath = @"..\..\..\SendMail\Templates\MailTemplateBody.htm",  
   TestMailTo= new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
   TestDropPath = @"c:\Samples\SendMail\TestDropPath\",  
};  
```  
  
## <a name="set-up-instructions"></a>Instructions d'installation  
 Vous devez avoir accès à un serveur SMTP pour cet exemple.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] configuration d’un serveur SMTP, consultez les liens suivants.  
  
-   [Microsoft Technet](http://go.microsoft.com/fwlink/?LinkId=166060)  
  
-   [Configuration du Service SMTP (IIS 6.0)](http://go.microsoft.com/fwlink/?LinkId=150456)  
  
-   [IIS 7.0 : Configuration de courrier électronique SMTP](http://go.microsoft.com/fwlink/?LinkId=150457)  
  
-   [Comment installer le Service SMTP](http://go.microsoft.com/fwlink/?LinkId=150458)  
  
 Les émulateurs SMTP fournis par des tiers ne sont pas disponibles pour le téléchargement.  
  
##### <a name="to-run-this-sample"></a>Pour exécuter cet exemple  
  
1.  Dans [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)], ouvrez le fichier solution SendMail.sln.  
  
2.  Vérifiez que vous avez accès à un serveur SMTP valide. Consultez les instructions d'installation.  
  
3.  Configuration du programme avec l’adresse de votre serveur et à partir d’et vers les adresses de messagerie.  
  
     Pour exécuter correctement cet exemple, vous devrez peut-être configurer la valeur de depuis et vers les adresses de messagerie et l’adresse du serveur SMTP dans le fichier Program.cs et Sequence.xaml. Vous devrez modifier l'adresse à ces deux emplacements car le programme envoie les messages de différentes façons.  
  
4.  Pour générer la solution, appuyez sur Ctrl+Maj+B.  
  
5.  Pour exécuter la solution, appuyez sur Ctrl+F5.  
  
> [!IMPORTANT]
>  Les exemples peuvent déjà être installés sur votre ordinateur. Recherchez le répertoire (par défaut) suivant avant de continuer.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Si ce répertoire n’existe pas, accédez à la page [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) pour télécharger tous les exemples [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] et [!INCLUDE[wf1](../../../../includes/wf1-md.md)] . Cet exemple se trouve dans le répertoire suivant.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\SendMail`