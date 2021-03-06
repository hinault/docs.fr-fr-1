---
title: "Protocoles de services Web pris en charge par des liaisons d'interopérabilité fournies par le système"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WS-protocols
- Web services protocols
- Windows Communication Foundation, Web service protocols
ms.assetid: 1f7fc4ff-30fe-4e46-adda-91caad3b06c6
caps.latest.revision: "39"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 4bfc4342435580796423056889b1c3bd22153740
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2017
---
# <a name="web-services-protocols-supported-by-system-provided-interoperability-bindings"></a>Protocoles de services Web pris en charge par des liaisons d’interopérabilité fournies par le système
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] a été conçu pour interagir avec les services Web qui prennent en charge un ensemble de spécifications connues sous le nom de spécifications de services Web. Pour simplifier la configuration de service afin d'obtenir les meilleures pratiques d'interopérabilité, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] introduit trois liaisons interopérables fournies par le système : <xref:System.ServiceModel.BasicHttpBinding?displayProperty=nameWithType>, <xref:System.ServiceModel.WSHttpBinding?displayProperty=nameWithType>et <xref:System.ServiceModel.WSDualHttpBinding?displayProperty=nameWithType>. Afin de permettre l'interopérabilité avec les standards OASIS (Organization for the Advancement of Structured Information Standards), [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] inclut une liaison interopérable fournie par le système : <xref:System.ServiceModel.WS2007HttpBinding?displayProperty=nameWithType>. Pour la publication des métadonnées, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] inclut deux liaisons interopérables fournies par le système : [ \<mexHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/mexhttpbinding.md) et [ \<mexHttpsBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/mexhttpsbinding.md). Cette rubrique répertorie les spécifications prises en charge par les liaisons interopérable fournies par le système.  
  
## <a name="web-services-protocols-supported-by-basichttpbinding-wshttpbinding-ws2007httpbinding-and-wsdualhttpbinding-bindings"></a>Protocoles de services Web pris en charge par basicHttpBinding, wsHttpBinding, ws2007HttpBinding et wsDualHttpBinding Bindings  
  
### <a name="all-bindings"></a>Toutes les liaisons  
 Le [ \<basicHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md), [ \<wsHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md), et [ \<ws2007HttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/ws2007httpbinding.md) prise en charge des liaisons le protocoles suivants.  
  
> [!NOTE]
>  Pour plus d’informations sur les liaisons utilisées pour publier des métadonnées, consultez la section « Liaisons de métadonnées fournies par le système » développée ultérieurement dans cette rubrique.  
  
|Category|Protocole|Spécification et utilisation|  
|--------------|--------------|-----------------------------|  
|Transport|HTTP 1.1|[PROTOCOLE HTTP 1.1](http://go.microsoft.com/fwlink/?LinkId=84048)<br /><br /> `BasicHttpBinding`, `WSHttpBinding` et `WS2007HttpBinding` utilisent les transports HTTP et HTTPS.|  
|Messagerie|MTOM|[MTOM](http://go.microsoft.com/fwlink/?LinkId=95326)<br /><br /> `basicHttpBinding`, `wsHttpBinding` et `ws2007HttpBinding` prennent en charge MTOM (Message Transmission Optimization Mechanism). Non utilisé par défaut. Pour utiliser MTOM, affectez `messageEncoding` à l'attribut `"Mtom"`.<br /><br /> Exemple :<br /><br /> `<wsHttpBinding> <binding messageEncoding="Mtom"/> </wsHttpBinding>`|  
|Métadonnées|WSDL 1.1|[WSDL 1.1](http://go.microsoft.com/fwlink/?LinkId=94859)<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilise WSDL (Web Services Description Language) pour décrire des services.|  
|Métadonnées|WS-Policy|[WS-Policy.](http://go.microsoft.com/fwlink/?LinkId=94864)<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilise la spécification WS-Policy avec des assertions spécifiques au domaine pour décrire des spécifications de service et des fonctions.|  
|Métadonnées|WS-Policy 1.5|[WS-Policy 1.5](http://go.microsoft.com/fwlink/?LinkId=95327)<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilise la spécification WS-Policy avec des assertions spécifiques au domaine pour décrire des spécifications de service et des fonctions.|  
|Métadonnées|WS-PolicyAttachment|[WS-PolicyAttachment](http://go.microsoft.com/fwlink/?LinkId=95328)<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implémente WS-PolicyAttachment pour joindre des expressions de stratégie à différentes portées dans WSDL (Web Services Description Language).|  
|Métadonnées|WS-MetadataExchange|[WS-MetadataExchange.](http://go.microsoft.com/fwlink/?LinkId=94868)<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implémente WS-MetadataExchange pour récupérer XML Schema, WSDL et WS-Policy.|  
  
### <a name="basichttpbinding"></a>basicHttpBinding  
  
|Category|Protocole|Spécification et utilisation|  
|--------------|--------------|-----------------------------|  
|Messagerie|SOAP 1,1|[SOAP 1.1](http://go.microsoft.com/fwlink/?LinkId=90520)<br /><br /> Conformément à Basic Profile 1.1, l'élément `basicHttpBinding` implémente le protocole de messagerie SOAP 1.1.|  
|Sécurité|WSS SOAP Message Security 1.0|[WSS SOAP Message Security 1.0](http://go.microsoft.com/fwlink/?LinkId=94684)<br /><br /> Conformément à Basic Security Profile, l'élément `basicHttpBinding` implémente la spécification WSS (Web Services Security) SOAP Message Security 1.0 pour le nom d'utilisateur/mot de passe et la sécurité basée sur les certificats X.509.<br /><br /> `<basicHttpBinding> <binding name="Binding1"> <security mode="TransportWithMessageCredential &#124;                     "Message" .../> </binding> </basicHttpBinding>`|  
|Sécurité|WSS SOAP Message Security UsernameToken Profile 1.0|[WSS SOAP Message Security UsernameToken Profile 1.0](http://go.microsoft.com/fwlink/?LinkId=95334)<br /><br /> `<basicHttpBinding> <binding name="Binding1"> <security mode="TransportWithMessageCredential"> <transport clientCredentialType="Basic"/> </security> </basicHttpBinding>`|  
|Sécurité|WSS SOAP Message Security X.509 Certificate Token Profile 1.0|[WSS SOAP Message Security X.509 Certificate Token Profile 1.0](http://go.microsoft.com/fwlink/?LinkId=95335)<br /><br /> `<basicHttpBinding>   <security mode="Message"> <message clientCredentialType="Certificate"/> </security> </basicHttpBinding>`|  
  
### <a name="wshttpbinding-ws2007httpbinding-and-wsdualhttpbinding"></a>wsHttpBinding, ws2007HttpBinding et wsDualHttpBinding  
  
|Category|Protocole|Spécification et utilisation|  
|--------------|--------------|-----------------------------|  
|Messagerie|SOAP 1.2|[Manuel de](http://go.microsoft.com/fwlink/?LinkId=48282)<br /><br /> [Infrastructure de messagerie](http://go.microsoft.com/fwlink/?LinkId=94664)<br /><br /> [Compléments (y compris la liaison HTTP)](http://go.microsoft.com/fwlink/?LinkId=95329)|  
|Messagerie|WS-Addressing 2005/08|[Web Services Addressing 1.0 - éléments principaux](http://go.microsoft.com/fwlink/?LinkId=90574)<br /><br /> [Les Services Web 1.0 - SOAP adressage](http://go.microsoft.com/fwlink/?LinkId=95330)<br /><br /> `wsHttpBinding`, `ws2007HttpBinding` et `wsDualHttpBinding` implémentent la recommandation W3C (World Wide Web Consortium) WS-Addressing pour activer la messagerie asynchrone, la corrélation de messages et les mécanismes d'adressage indépendant du transport.<br /><br /> WCF ne prend pas en charge le chiffrement des en-têtes WS-Addressing bien que cela soit autorisé par les spécifications WS-*.|  
|Messagerie|WS-Addressing 1.0 - Métadonnées|[Métadonnées de 1.0 WS-Addressing](http://www.w3.org/2007/05/addressing/metadata) prise en charge ce protocole est activé en définissant la version de stratégie dans le comportement ServiceMetadata - avec policyversion définie à la version 1.2 (la valeur par défaut), la description wsdl est conforme à WS-Addressing wsdl, avec policyversion définie sur la version 1.5, la description wsdl est compatible avec les métadonnées de ws-addressing.<br /><br /> WCF ne prend pas en charge le chiffrement des en-têtes WS-Addressing bien que cela soit autorisé par les spécifications WS-*.|  
|Sécurité|WSS SOAP Message Security 1.0|[WSS SOAP Message Security 1.0](http://go.microsoft.com/fwlink/?LinkId=94684)<br /><br /> Utilisé lorsque l'attribut `securityMode` a la valeur "wsSecurityOverHttp" (valeur par défaut) et que les paramètres sont configurés à l'aide d'un élément enfant `wsSecurity`.<br /><br /> `<wsHttpBinding>   <binding name="myBinding">      <security mode="Message" .../>   </binding> </wsHttpBinding>`|  
|Sécurité|WSS SOAP Message Security UsernameToken Profile 1.1|[WSS SOAP Message Security UsernameToken Profile 1.0](http://go.microsoft.com/fwlink/?LinkId=95331)<br /><br /> Utilisé lorsque l'attribut `wsSecurity` de l'élément `authenticationMode` a la valeur "Username".<br /><br /> `<wsHttpBinding>   <binding name="MyBinding">     <security mode="Message>       <message           clientCredentialType="UserName        negotiateServiceCredential="false"        establishSecurityContext="false"/>     </security> </binding> </wsHttpBinding>`|  
|Sécurité|WSS SOAP Message Security X.509 Certificate Token Profile 1.1|[WSS SOAP Message Security X.509 Certificate Token Profile 1.1](http://go.microsoft.com/fwlink/?LinkId=95332)<br /><br /> Utilisé pour la protection des messages lorsque l'attribut `wsSecurity` de l'élément `authenticationMode` a la valeur "Username", "Certificate" ou "None". Il est par ailleurs utilisé pour l'authentification du client lorsque l'attribut `wsSecurity` de l'élément `authenticationMode` a la valeur "Certificate".<br /><br /> `<wsHttpBinding>   <binding name="MyBinding">     <security mode="Message>       <message           clientCredentialType="Certificate"        negotiateServiceCredential="false"        establishSecurityContext="false"/>     </security>   </binding> </wsHttpBinding>`|  
|Sécurité|WSS SOAP Message Security Kerberos Token Profile 1.1|[WSS SOAP Message Security Kerberos Token Profile 1.1](http://go.microsoft.com/fwlink/?LinkId=95333)<br /><br /> Utilisé pour l'authentification et la protection des messages lorsque l'attribut `wsSecurity` de l'élément `authenticationMode` a la valeur "Windows".<br /><br /> `<wsHttpBinding>   <binding name="MyBinding">     <security mode="Message>       <message           clientCredentialType="Windows"        negotiateServiceCredential="false"        establishSecurityContext="false"/>     </security>   </binding> </wsHttpBinding>`|  
|Sécurité|WS-SecureConversation|[WS-SecureConversation.](http://go.microsoft.com/fwlink/?LinkId=95317)<br /><br /> Utilisé pour fournir une session sécurisée lorsque l'attribut `security/@mode` a la valeur "Message" et l'attribut `message/@establishSecurityContext` a la valeur "true" (valeur par défaut).|  
|Sécurité|WS-Trust|[WS-Trust.](http://go.microsoft.com/fwlink/?LinkId=95318)<br /><br /> Utilisé par WS-SecureConversation (voir ci-dessus).|  
|Messagerie fiable|WS-ReliableMessaging|[WS-ReliableMessaging.](http://go.microsoft.com/fwlink/?LinkId=95322)<br /><br /> Utilisé lorsque la liaison est configurée pour utiliser `reliableSession`.<br /><br /> `<wsHttpBinding>  <binding name="myBinding">    <reliableSession/>   </binding> </wsHttpBinding>`|  
|Transactions|WS-AtomicTransaction|[WS-AtomicTransaction](http://go.microsoft.com/fwlink/?LinkId=95323)<br /><br /> À utiliser pour la communication entre les gestionnaires de transactions. Les clients et les services [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilisent systématiquement les gestionnaires de transactions locaux.|  
|Transactions|WS-Coordination|[WS-Coordination.](http://go.microsoft.com/fwlink/?LinkId=95324)<br /><br /> Utilisé pour transmettre le contexte de transaction lorsque l'attribut `flowTransactions` a la valeur "Allowed" ou "Required".<br /><br /> `<wsHttpBinding>   <binding transactionFlow="true"/> </wsHttpBinding>`|  
  
## <a name="wsfederationhttpbinding-and-ws2007federationhttpbinding"></a>wsFederationHttpBinding et ws2007FederationHttpBinding  
 Le [ \<wsFederationHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md) et [ \<ws2007FederationHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/ws2007federationhttpbinding.md) éléments sont introduites pour prendre en charge les scénarios de fédération, où un tiers partie émet un jeton utilisé pour authentifier un client. Outre les protocoles utilisés par `wsHttpBinding`, `wsFederationHttpBinding` tire parti de :  
  
-   `WS-Trust` pour l'émission de jeton.  
  
-   WSS SAML (Security Assertions Markup Language) Token Profile 1.0 et 1.1 pour le format de jeton le plus fréquemment émis.  
  
 Exemple :  
  
```xml  
<wsFederationHttpBinding>  
  <binding name="myBinding">  
     <security mode="Message">  
       <message issuedKeyType="Symmetric"   
                issuedTokenType="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1">  
         <issuerMetadata address =   
         'http://localhost/FederationSample/HomeRealmSTS/STS.svc/mex'>  
       </message>  
     </security>  
  </binding>  
</wsFederationHttpBinding>  
```  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Fédération](../../../../docs/framework/wcf/feature-details/federation.md) .  
  
## <a name="system-provided-metadata-bindings"></a>Liaisons de métadonnées fournies par le système  
 Les tableaux suivants décrivent les protocoles pris en charge par les liaisons de métadonnées interopérables fournies par le système exposées par la classe <xref:System.ServiceModel.Description.MetadataExchangeBindings?displayProperty=nameWithType>.  
  
### <a name="mexhttpbinding"></a>mexHttpBinding  
 Le [ \<mexHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/mexhttpbinding.md) liaison prend en charge les protocoles suivants. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]à l’aide de cette liaison, consultez [publication des métadonnées](../../../../docs/framework/wcf/feature-details/publishing-metadata.md).  
  
|Category|Protocole|Spécification et utilisation|  
|--------------|--------------|-----------------------------|  
|Transport|HTTP 1.1|[PROTOCOLE HTTP 1.1](http://go.microsoft.com/fwlink/?LinkId=84048)|  
|Messagerie|SOAP 1.2|[Manuel de](http://go.microsoft.com/fwlink/?LinkId=48282)<br /><br /> [Infrastructure de messagerie](http://go.microsoft.com/fwlink/?LinkId=94664)<br /><br /> [Compléments (y compris la liaison HTTP)](http://go.microsoft.com/fwlink/?LinkId=95329)|  
|Messagerie|WS-Addressing 2005/08|[Web Services Addressing 1.0 - éléments principaux](http://go.microsoft.com/fwlink/?LinkId=90574)<br /><br /> [Les Services Web 1.0 - SOAP adressage](http://go.microsoft.com/fwlink/?LinkId=95330)|  
|Métadonnées|WS-MetadataExchange|[WS-MetadataExchange.](http://go.microsoft.com/fwlink/?LinkId=94868)<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implémente WS-MetadataExchange pour récupérer XML Schema, WSDL et WS-Policy.|  
  
### <a name="mexhttpsbinding"></a>mexHttpsBinding  
 [\<mexHttpsBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/mexhttpsbinding.md) prend en charge les protocoles suivants. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]à l’aide de cette liaison, consultez [publication des métadonnées](../../../../docs/framework/wcf/feature-details/publishing-metadata.md).  
  
|Category|Protocole|Spécification et utilisation|  
|--------------|--------------|-----------------------------|  
|Transport|HTTP 1.1|[PROTOCOLE HTTP 1.1](http://go.microsoft.com/fwlink/?LinkId=84048)<br /><br /> La sécurité de transport est activée.|  
|Messagerie|SOAP 1.2|[Manuel de](http://go.microsoft.com/fwlink/?LinkId=48282)<br /><br /> [Infrastructure de messagerie](http://go.microsoft.com/fwlink/?LinkId=94664)<br /><br /> [Compléments (y compris la liaison HTTP)](http://go.microsoft.com/fwlink/?LinkId=95329)|  
|Messagerie|WS-Addressing 2005/08|[Web Services Addressing 1.0 - éléments principaux](http://go.microsoft.com/fwlink/?LinkId=90574)<br /><br /> [Les Services Web 1.0 - SOAP adressage](http://go.microsoft.com/fwlink/?LinkId=95330)|  
|Métadonnées|WS-MetadataExchange|[WS-MetadataExchange.](http://go.microsoft.com/fwlink/?LinkId=94868)<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implémente WS-MetadataExchange pour récupérer XML Schema, WSDL et WS-Policy.|  
  
## <a name="see-also"></a>Voir aussi  
 [Liaisons fournies par le système](../../../../docs/framework/wcf/system-provided-bindings.md)  
 [\<basicHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)  
 [\<wsHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)  
 [\<wsDualHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md)  
 [\<mexHttpsBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/mexhttpsbinding.md)  
 [\<mexHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/mexhttpbinding.md)
