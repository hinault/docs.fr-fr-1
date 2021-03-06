---
title: Message Security Anonymous
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: WS Security
ms.assetid: c321cbf9-8c05-4cce-b5a5-4bf7b230ee03
caps.latest.revision: "52"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.workload: dotnet
ms.openlocfilehash: d6f3ac3ba51939f319d1d0e98265d7867233f2b6
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="message-security-anonymous"></a>Message Security Anonymous
Cette exemple illustre comment implémenter une application [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] qui utilise la sécurité de niveau message sans authentifier le client mais nécessite l'authentification du serveur à l'aide du certificat X.509 afférent. Tous les messages d'application échangés entre le client et le serveur sont signés et chiffrés. Cet exemple est basé sur le [WSHttpBinding](../../../../docs/framework/wcf/samples/wshttpbinding.md) exemple. Cet exemple se compose d'un programme de console client (.exe) et d'une bibliothèque de service (.dll) hébergés par les services IIS (Internet Information Services). Le service implémente un contrat qui définit un modèle de communication demande-réponse.  
  
> [!NOTE]
>  La procédure d'installation ainsi que les instructions de génération relatives à cet exemple figurent à la fin de cette rubrique.  
  
 Cet exemple ajoute une nouvelle opération à l'interface de calculatrice qui retourne la valeur `True` lorsque le client n'est pas authentifié.  
  
```  
public class CalculatorService : ICalculator  
{  
    public bool IsCallerAnonymous()  
    {  
        // ServiceSecurityContext.IsAnonymous returns true if the caller is not authenticated.  
        return ServiceSecurityContext.Current.IsAnonymous;  
    }  
    ...  
}  
```  
  
 Le service expose un point de terminaison unique de communication avec le service, lequel est défini à l'aide du fichier de configuration Web.config. Le point de terminaison se compose d'une adresse, d'une liaison et d'un contrat. La liaison est configurée à l'aide de la liaison `wsHttpBinding`. Le mode de sécurité par défaut pour la liaison `wsHttpBinding` correspond à `Message`. La valeur de l'attribut `clientCredentialType` est `None`.  
  
```xml  
<system.serviceModel>  
  
  <protocolMapping>  
    <add scheme="http" binding="wsHttpBinding" />  
  </protocolMapping>  
  
  <bindings>  
    <wsHttpBinding>  
     <!--   
     <!--This configuration defines the security mode as Message and-->  
     <!--the clientCredentialType as None. This mode provides -- >  
     <!--server authentication only using the service certificate.-->  
  
     <binding>  
       <security mode="Message">  
         <message clientCredentialType="None" />  
       </security>  
     </binding>  
    </wsHttpBinding>  
  </bindings>  
  ...  
</system.serviceModel>  
```  
  
 Les informations d’identification à utiliser pour l’authentification du service sont spécifiées dans le [ \<comportement >](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md). Dans le certificat du serveur, la valeur de `SubjectName` doit correspondre à la valeur spécifiée pour l'attribut `findValue`, tel qu'illustré par l'exemple de code suivant.  
  
```xml  
<behaviors>  
  <serviceBehaviors>  
    <behavior>  
      <!--   
    The serviceCredentials behavior allows you to define a service certificate.  
    A service certificate is used by a client to authenticate the service and provide message protection.  
    This configuration references the "localhost" certificate installed during the setup instructions.  
    -->  
      <serviceCredentials>  
        <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />  
      </serviceCredentials>  
      <serviceMetadata httpGetEnabled="True"/>  
      <serviceDebug includeExceptionDetailInFaults="False" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 La configuration du point de terminaison du client se compose d'une adresse absolue pour le point de terminaison du service, de la liaison et du contrat. Le mode de sécurité du client pour la liaison `wsHttpBinding` correspond à `Message`. La valeur de l'attribut `clientCredentialType` est `None`.  
  
```xml  
<system.serviceModel>  
  <client>  
    <endpoint name=""  
             address="http://localhost/servicemodelsamples/service.svc"   
             binding="wsHttpBinding"   
             behaviorConfiguration="ClientCredentialsBehavior"  
             bindingConfiguration="Binding1"   
             contract="Microsoft.ServiceModel.Samples.ICalculator" />  
  </client>  
  
  <bindings>  
    <wsHttpBinding>  
      <!--This configuration defines the security mode as -->  
      <!--Message and the clientCredentialType as None. -->  
      <binding name="Binding1">  
        <security mode = "Message">  
          <message clientCredentialType="None"/>  
        </security>  
      </binding>  
    </wsHttpBinding>  
  </bindings>   
  ...  
</system.serviceModel>  
```  
  
 L'exemple affecte au <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A> la valeur <xref:System.ServiceModel.Security.X509CertificateValidationMode.PeerOrChainTrust> pour authentifier le certificat du service. Cette opération s'effectue dans le fichier App.config du client à la section `behaviors`. Cela signifie que si le certificat se trouve dans le magasin de personnes de confiance de l'utilisateur, il est approuvé sans validation de sa chaîne d'émetteur. Ce paramètre est utilisé ici pour des raisons pratiques afin que l'exemple puisse s'exécuter sans nécessiter que les certificats soient publiés par une autorité de certification. Ce paramètre n'offre pas le même niveau de sécurité que la valeur par défaut, ChainTrust. C'est pourquoi, ses conséquences en termes de sécurité doivent être mûrement réfléchies avant d'utiliser `PeerOrChainTrust` dans le code de production.  
  
 L’implémentation du client ajoute un appel à la `IsCallerAnonymous` (méthode) et sinon ne diffère pas de la [WSHttpBinding](../../../../docs/framework/wcf/samples/wshttpbinding.md) exemple.  
  
```  
// Create a client with a client endpoint configuration.  
CalculatorClient client = new CalculatorClient();  
  
// Call the GetCallerIdentity operation.  
Console.WriteLine("IsCallerAnonymous returned: {0}", client.IsCallerAnonymous());  
  
// Call the Add service operation.  
double value1 = 100.00D;  
double value2 = 15.99D;  
double result = client.Add(value1, value2);  
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
...  
  
//Closing the client gracefully closes the connection and cleans up resources.  
client.Close();  
  
Console.WriteLine();  
Console.WriteLine("Press <ENTER> to terminate client.");  
Console.ReadLine();  
```  
  
 Lorsque vous exécutez l'exemple, les demandes et réponses d'opération s'affichent dans la fenêtre de console du client. Appuyez sur Entrée dans la fenêtre du client pour l'arrêter.  
  
```  
IsCallerAnonymous returned: True  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
Press <ENTER> to terminate client.  
```  
  
 Le fichier de commandes Setup.bat contenu dans l'exemple Message Security Anonymous vous permet de configurer le serveur à l'aide du certificat nécessaire à l'exécution d'une application hébergée utilisant une sécurité basée sur les certificats. Deux modes d'exécution sont disponibles pour ce fichier. Pour exécuter le fichier de commandes en mode ordinateur unique, tapez `setup.bat` dans la ligne de commande. Pour l'exécuter en mode service, tapez `setup.bat service`. Utilisez ce mode lorsque l'exemple est exécuté sur plusieurs ordinateurs. Pour plus d'informations, consultez la procédure d'installation figurant en fin de rubrique.  
  
 Les éléments suivants fournissent une vue d'ensemble des différentes sections des fichiers de commandes :  
  
-   Création du certificat de serveur  
  
     Les lignes suivantes du fichier de commandes Setup.bat créent le certificat de serveur à utiliser.  
  
    ```  
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
    ```  
  
     La variable %SERVER_NAME% spécifie le nom du serveur. Le certificat est stocké dans le magasin LocalMachine. Si le fichier de commandes d'installation est exécuté à l'aide d'un argument de service (tel que `setup.bat service`), la variable %SERVER_NAME% contient le nom de domaine complet de l'ordinateur. Dans le cas contraire, elle contient la valeur par défaut localhost.  
  
-   Installation du certificat de serveur dans le magasin de certificats approuvés du client.  
  
     La ligne suivante copie le certificat de serveur dans le magasin de personnes de confiance du client. Cette étape est requise car les certificats générés par Makecert.exe ne sont pas implicitement approuvés par le système client. Si vous disposez déjà d'un certificat associé à un certificat racine approuvé du client, par exemple d'un certificat émis par Microsoft, il n'est pas nécessaire d'ajouter le certificat du serveur au magasin de certificats du client.  
  
    ```  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
    ```  
  
-   Octroi d'autorisations sur la clé privée du certificat.  
  
     Les lignes suivantes du fichier de commandes Setup.bat permettent au processus de traitement [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] d'accéder au certificat du serveur stocké dans le magasin LocalMachine.  
  
    ```  
    echo ************  
    echo setting privileges on server certificates  
    echo ************  
    for /F "delims=" %%i in ('"%MSSDK%\bin\FindPrivateKey.exe" My LocalMachine -n CN^=%SERVER_NAME% -a') do set PRIVATE_KEY_FILE=%%i set WP_ACCOUNT=NT AUTHORITY\NETWORK SERVICE  
    (ver | findstr "5.1") && set WP_ACCOUNT=%COMPUTERNAME%\ASPNET  
    echo Y|cacls.exe "%PRIVATE_KEY_FILE%" /E /G "%WP_ACCOUNT%":R  
    iisreset  
    ```  
  
> [!NOTE]
>  Si vous utilisez une édition anglaise de Windows, vous devez modifier le fichier Setup.bat et remplacer le nom du compte `NT AUTHORITY\NETWORK SERVICE` par votre équivalent régional.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Pour configurer, générer et exécuter l'exemple  
  
1.  Assurez-vous d’avoir effectué la [procédure d’installation d’à usage unique pour les exemples Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Pour générer l’édition C# ou Visual Basic .NET de la solution, conformez-vous aux instructions figurant dans [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
### <a name="to-run-the-sample-on-the-same-computer"></a>Pour exécuter l'exemple sur le même ordinateur  
  
1.  Assurez-vous que le chemin d'accès contient le dossier dans lequel Makecert.exe et FindPrivateKey.exe se trouvent.  
  
2.  Ouvrez une fenêtre d'invite de commandes de Visual Studio avec des privilèges d'administrateur et exécutez Setup.bat à partir du dossier d'installation de l'exemple. Tous les certificats requis à l'exécution de l'exemple sont ainsi installés.  
  
    > [!NOTE]
    >  Le fichier de commandes d'installation est conçu pour être exécuté à partir d'une invite de commandes de [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)]. La variable d'environnement PATH doit pointer vers le répertoire d'installation du Kit de développement SDK. Cette variable est définie automatiquement dans une invite de commandes de [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
3.  Vérifiez l'accès au service à l'aide d'un navigateur en tapant l'adresse http://localhost/servicemodelsamples/service.svc.  
  
4.  Lancez Client.exe à partir de \client\bin. L'activité du client s'affiche sur son application de console.  
  
5.  Si le client et le service ne sont pas en mesure de communiquer, consultez [conseils de dépannage](http://msdn.microsoft.com/library/8787c877-5e96-42da-8214-fa737a38f10b).  
  
### <a name="to-run-the-sample-across-computers"></a>Pour exécuter l'exemple sur plusieurs ordinateurs  
  
1.  Créez un répertoire sur l'ordinateur de service. Créez une application virtuelle appelée servicemodelsamples pour ce répertoire à l'aide de l'outil de gestion IIS (Internet Information Services).  
  
2.  Copiez les fichiers programme du service de \inetpub\wwwroot\servicemodelsamples dans le répertoire virtuel sur l'ordinateur de service. Assurez-vous de copier les fichiers dans le sous-répertoire \bin. Copiez également les fichiers Setup.bat et Cleanup.bat sur l'ordinateur de service.  
  
3.  Créez un répertoire sur l'ordinateur client pour les fichiers binaires du client.  
  
4.  Copiez les fichiers programme du client dans le répertoire client de l'ordinateur client. Copiez également les fichiers Setup.bat, Cleanup.bat et ImportServiceCert.bat sur le client.  
  
5.  Sur le serveur, ouvrez une fenêtre d'invite de commandes de Visual Studio avec des privilèges d'administrateur et exécutez `setup.bat service`. En cours d’exécution `setup.bat` avec la `service` argument crée un certificat de service portant le nom de domaine complet de l’ordinateur et exporte le certificat de service dans un fichier nommé Service.cer.  
  
6.  Modifiez le fichier Web.config pour refléter le nouveau nom de certificat (dans le `findValue` d’attribut dans le [ \<serviceCertificate >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)), qui est le même que le nom de domaine complet de l’ordinateur.  
  
7.  Copiez le fichier Service.cer du répertoire de service vers le répertoire client sur l'ordinateur client.  
  
8.  Dans le fichier Client.exe.config de l'ordinateur client, modifiez la valeur d'adresse du point de terminaison afin qu'elle corresponde à la nouvelle adresse de votre service.  
  
9. Sur le client, ouvrez une fenêtre d'invite de commandes de Visual Studio avec des privilèges d'administrateur et exécutez ImportServiceCert.bat. Cette opération importe le certificat de service du fichier Service.cer dans le magasin CurrentUser - TrustedPeople.  
  
10. Sur l'ordinateur client, lancez Client.exe à partir d'une invite de commandes. Si le client et le service ne sont pas en mesure de communiquer, consultez [conseils de dépannage](http://msdn.microsoft.com/library/8787c877-5e96-42da-8214-fa737a38f10b).  
  
### <a name="to-clean-up-after-the-sample"></a>Pour procéder au nettoyage après exécution de l'exemple  
  
-   Exécutez Cleanup.bat dans le dossier exemples une fois que vous avez terminé d'exécuter l'exemple.  
  
> [!NOTE]
>  Ce script ne supprime pas de certificat de service sur un client lors de l'exécution de cet exemple sur plusieurs ordinateurs. Si vous avez exécuté des exemples [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] qui utilisent des certificats sur plusieurs ordinateurs, assurez-vous d'effacer les certificats de service installés dans le magasin CurrentUser - TrustedPeople. Pour ce faire, utilisez la commande suivante : `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`, par exemple : `certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com.`.  
  
## <a name="see-also"></a>Voir aussi
