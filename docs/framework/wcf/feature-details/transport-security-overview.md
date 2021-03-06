---
title: "Vue d'ensemble de la sécurité des transports"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: 00959326-aa9d-44d0-af61-54933d4adc7f
caps.latest.revision: "23"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.workload: dotnet
ms.openlocfilehash: 71325089f2c72f6f01b2179bd150d21a98b3a8e2
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2017
---
# <a name="transport-security-overview"></a>Vue d'ensemble de la sécurité des transports
Les mécanismes de sécurité de transport dans [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] dépendent de la liaison et du transport utilisé. Par exemple, lors de l'utilisation de la classe <xref:System.ServiceModel.WSHttpBinding>, le transport correspond à HTTP et le mécanisme principal utilisé pour sécuriser ce transport correspond à SSL (Secure Sockets Layer) sur HTTP, c'est-à-dire à HTTPS. Cette rubrique aborde les principaux mécanismes de sécurité de transport utilisés dans les liaisons [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fournies par le système.  
  
> [!NOTE]
>  Lorsque la sécurité SSL est utilisée avec le .NET Framework version 3.5 et ultérieure, un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilise les certificats intermédiaires dans son magasin de certificats et les certificats intermédiaires reçus au cours de la négociation SSL pour effectuer la validation de chaîne de certificats sur le certificat du service. .NET Framework 3.0 n'utilise que les certificats intermédiaires installés dans le magasin de certificats local.  
  
> [!WARNING]
>  Lorsque la sécurité de transport est utilisée, le <!--zz <xref:System.Treading.Thread.CurrentPrincipal%2A> --> `CurrentPrincipal` propriété peut-être être remplacée. Pour éviter cela, affectez le <!--zz <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.PrincipalPermission%2A> --> `PrincipalPermission` None. <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior> est un comportement de service qui peut être défini dans la description du service.  
  
## <a name="basichttpbinding"></a>BasicHttpBinding  
 Par défaut, la classe <xref:System.ServiceModel.BasicHttpBinding> n'offre aucune sécurité. Cette liaison est conçue pour assurer l'interopérabilité avec les fournisseurs de services Web, lesquels n'implémentent pas de sécurité. Vous pouvez toutefois activer la sécurité en affectant à la propriété <xref:System.ServiceModel.BasicHttpSecurity.Mode%2A> toutes valeurs autres que <xref:System.ServiceModel.BasicHttpSecurityMode.None>. Pour activer la sécurité du transport, affectez à la propriété la valeur <xref:System.ServiceModel.BasicHttpSecurityMode.Transport>.  
  
### <a name="interoperation-with-iis"></a>Interaction avec IIS  
 La classe <xref:System.ServiceModel.BasicHttpBinding> est utilisée principalement pour interagir avec les services Web existants, hébergés pour un grand nombre d'entre eux par les services Internet (IIS). C'est pourquoi la sécurité de transport de cette liaison est conçue pour interagir de façon transparente avec les sites IIS. Pour permettre cette interaction, il suffit d'affecter au mode de sécurité <xref:System.ServiceModel.BasicHttpSecurityMode.Transport>, puis de définir le type d'informations d'identification du client. Les valeurs de ce type correspondent aux mécanismes de sécurité du répertoire IIS. Dans l'exemple de code suivant, le mode est en cours de définition et la valeur Windows est affectée au type d'informations d'identification. Vous pouvez utiliser cette configuration lorsque le client et le serveur figurent tous les deux dans le même domaine Windows.  
  
 [!code-csharp[c_ProgrammingSecurity#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#10)] 
 [!code-vb[c_ProgrammingSecurity#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#10)]  
  
 Ou dans la configuration :  
  
```xml  
<bindings>  
  <basicHttpBinding>  
    <binding name="SecurityByTransport">  
      <security mode="Transport">  
        <transport clientCredentialType="Windows" />  
       </security>  
     </binding>  
  </basicHttpBinding>  
</bindings>  
```  
  
 Les sections suivantes abordent d'autres types d'informations d'identification.  
  
#### <a name="basic"></a>De base  
 Il s'agit de la méthode d'authentification de base dans IIS. Lorsque ce mode est utilisé, le serveur IIS doit être configuré avec des comptes utilisateur Windows et les autorisations de système de fichiers NTFS adéquates. [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iis601](../../../../includes/iis601-md.md)], consultez [l’activation de l’authentification de base et la configuration du nom de domaine](http://go.microsoft.com/fwlink/?LinkId=88592). [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iisver](../../../../includes/iisver-md.md)], consultez [IIS 7.0 bêta : configurer l’authentification de base](http://go.microsoft.com/fwlink/?LinkId=88593).  
  
#### <a name="certificate"></a>Certificat  
 Sur les services IIS, une option permet de spécifier que les clients doivent se connecter en utilisant un certificat. Cette fonctionnalité permet également aux services IIS de mapper les certificats clients aux comptes Windows correspondants. [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iis601](../../../../includes/iis601-md.md)], consultez [activation des certificats Client dans IIS 6.0](http://go.microsoft.com/fwlink/?LinkId=88594). [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iisver](../../../../includes/iisver-md.md)], consultez [IIS 7.0 bêta : configuration des certificats de serveur dans IIS 7.0](http://go.microsoft.com/fwlink/?LinkId=88595).  
  
#### <a name="digest"></a>Digest  
 L’authentification Digest s’apparente à l’authentification de base tout en présentant l’avantage supplémentaire de permettre l’envoi des informations d’identification dans un texte haché plutôt qu’en texte clair. [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iis601](../../../../includes/iis601-md.md)], consultez [l’authentification Digest dans IIS 6.0](http://go.microsoft.com/fwlink/?LinkID=88443). [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iisver](../../../../includes/iisver-md.md)], consultez [IIS 7.0 bêta : configurer l’authentification Digest](http://go.microsoft.com/fwlink/?LinkId=88596).  
  
#### <a name="windows"></a>Windows  
 Il s'agit de l'authentification Windows intégrée à IIS. Lorsque ce mode d'authentification est activé, le serveur doit également figurer dans un domaine Windows utilisant le protocole Kerberos comme contrôleur. Dans le cas contraire ou si le système Kerberos connaît une défaillance, vous pouvez utiliser l'authentification NT LAN Manager (NTLM), abordée dans la section suivante. [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iis601](../../../../includes/iis601-md.md)], consultez [l’authentification Windows intégrée dans IIS 6.0](http://go.microsoft.com/fwlink/?LinkId=88597). [!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[iisver](../../../../includes/iisver-md.md)], consultez [IIS 7.0 bêta : configuration des certificats de serveur dans IIS 7.0](http://go.microsoft.com/fwlink/?LinkId=88595).  
  
#### <a name="ntlm"></a>NTLM  
 Cela permet au serveur d'utiliser NTLM pour l'authentification si le fournisseur Kerberos échoue. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]configuration d’IIS dans [!INCLUDE[iis601](../../../../includes/iis601-md.md)], consultez [authentification NTLM forcée](http://go.microsoft.com/fwlink/?LinkId=88598). Pour [!INCLUDE[iisver](../../../../includes/iisver-md.md)], l'authentification Windows intègre l'authentification NTLM. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][IIS 7.0 bêta : configuration des certificats de serveur dans IIS 7.0](http://go.microsoft.com/fwlink/?LinkID=88595).  
  
## <a name="wshttpbinding"></a>WsHttpBinding  
 La classe <xref:System.ServiceModel.WSHttpBinding> est conçue pour interagir avec les services qui implémentent les spécifications WS-*. La sécurité de transport de cette liaison correspond à Secure Sockets Layer (SSL) sur HTTP, c'est-à-dire à HTTPS. Pour créer une application [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] qui utilise SSL, utilisez les services IIS afin d'héberger cette application. Si vous créez une application auto-hébergée, vous pouvez également utiliser l'outil HttpCfg.exe afin d'attribuer un certificat X.509 à un port spécifique de l'ordinateur. Ce numéro de port est spécifié dans le cadre d'une application [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sous forme d'adresse de point de terminaison. Lorsqu'un mode de transport est utilisé, l'adresse de point de terminaison doit comporter le protocole HTTPS. Dans le cas contraire, une exception sera levée pendant l'exécution. [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Sécurité de Transport HTTP](../../../../docs/framework/wcf/feature-details/http-transport-security.md).  
  
 Pour l'authentification client, affectez à la propriété <xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A> de la classe <xref:System.ServiceModel.HttpTransportSecurity> l'une des valeurs d'énumération <xref:System.ServiceModel.HttpClientCredentialType>. Les valeurs d'énumération sont identiques aux types d'informations d'identification client pour <xref:System.ServiceModel.BasicHttpBinding> et sont conçues pour être hébergées dans les services IIS.  
  
 Dans l’exemple suivant, une liaison est utilisée avec un type d’informations d’identification client de Windows.  
  
 [!code-csharp[c_ProgrammingSecurity#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#11)]
 [!code-vb[c_ProgrammingSecurity#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#11)]  
  
## <a name="wsdualhttpbinding"></a>WSDualHttpBinding  
 Cette liaison offre uniquement une sécurité de niveau message et non une sécurité de niveau transport.  
  
## <a name="nettcpbinding"></a>NetTcpBinding  
 La classe <xref:System.ServiceModel.NetTcpBinding> utilise le transport TCP pour les messages. La sécurité de niveau transport est assurée par l'implémentation de la sécurité Transport Layer Security (TLS) sur TCP. L'implémentation TLS est assurée par le système d'exploitation.  
  
 Vous pouvez également spécifier le type d'informations d'identification client en affectant à la propriété <xref:System.ServiceModel.TcpTransportSecurity.ClientCredentialType%2A> de la classe <xref:System.ServiceModel.TcpTransportSecurity> l'une des valeurs <xref:System.ServiceModel.TcpClientCredentialType>, comme illustré dans l'exemple de code suivant.  
  
 [!code-csharp[c_ProgrammingSecurity#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#12)]
 [!code-vb[c_ProgrammingSecurity#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#12)]  
  
#### <a name="client"></a>Client  
 Côté client, vous devez spécifier un certificat à l'aide de la méthode <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> de la classe <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential>.  
  
> [!NOTE]
>  Si vous utilisez la sécurité Windows, aucun certificat n'est requis.  
  
 Le code suivant utilise l'empreinte numérique de certificat, propre à chaque certificat. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]les certificats, consultez [utilisation des certificats](../../../../docs/framework/wcf/feature-details/working-with-certificates.md).  
  
 [!code-csharp[c_ProgrammingSecurity#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#13)]
 [!code-vb[c_ProgrammingSecurity#13](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#13)]  
  
 Vous pouvez également spécifier le certificat dans la configuration du client à l’aide un [ \<clientCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md) élément dans la section des comportements.  
  
```xml  
<behaviors>  
  <behavior>  
   <clientCredentials>  
     <clientCertificate findValue= "101010101010101010101010101010000000000"   
      storeLocation="LocalMachine" storeName="My"   
      X509FindType="FindByThumbPrint"/>  
     </clientCertificate>  
   </clientCredentials>  
 </behavior>  
</behaviors>    
```  
  
## <a name="netnamedpipebinding"></a>NetNamedPipeBinding  
 La classe <xref:System.ServiceModel.NetNamedPipeBinding> est conçue pour assurer une communication interne efficace au sein des ordinateurs, c'est-à-dire entre les processus s'exécutant sur les mêmes ordinateurs, bien qu'il soit possible de créer des canaux nommés entre deux ordinateurs figurant sur le même réseau. Cette liaison offre uniquement une sécurité de niveau transport. Lorsque des applications sont créées à l'aide de cette liaison, les adresses de point de terminaison doivent comporter « net.pipe » dans leur protocole.  
  
## <a name="wsfederationhttpbinding"></a>WSFederationHttpBinding  
 Lorsqu'un transport de sécurité est utilisé, cette liaison utilise SSL sur HTTP, c'est-à-dire HTTPS avec un jeton émis (<xref:System.ServiceModel.WSFederationHttpSecurityMode.TransportWithMessageCredential>). [!INCLUDE[crabout](../../../../includes/crabout-md.md)]les applications de fédération, consultez [fédération et les jetons émis](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md).  
  
## <a name="netpeertcpbinding"></a>NetPeerTcpBinding  
 La classe <xref:System.ServiceModel.NetPeerTcpBinding> correspond à un transport sécurisé, conçu pour assurer une communication efficace à l'aide de la fonctionnalité de réseau pair à pair. Comme indiqué par le nom de la classe et de la liaison, TCP correspond au protocole. Lorsque le mode de sécurité a la valeur transport, la liaison implémente TLS sur TCP. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]la fonctionnalité pair à pair, consultez [mise en réseau pair à pair](../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md).  
  
## <a name="msmqintegrationbinding-and-netmsmqbinding"></a>MsmqIntegrationBinding et NetMsmqBinding  
 Pour une description complète de transport de sécurité avec Message Queuing (précédemment appelé MSMQ), consultez [sécurisation des Messages à l’aide de sécurité du Transport](../../../../docs/framework/wcf/feature-details/securing-messages-using-transport-security.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Programmation de la sécurité dans WCF](../../../../docs/framework/wcf/feature-details/programming-wcf-security.md)
