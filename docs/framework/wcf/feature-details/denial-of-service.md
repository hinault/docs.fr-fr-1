---
title: Refus de service
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: denial of service [WCF]
ms.assetid: dfb150f3-d598-4697-a5e6-6779e4f9b600
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 5d5f67790abad5dcf6311de1817b4ea093e703d9
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2017
---
# <a name="denial-of-service"></a>Refus de service
Un déni de service se produit lorsqu'un système est saturé au point que le traitement des messages est impossible ou extrêmement lent.  
  
## <a name="excess-memory-consumption"></a>Consommation de mémoire excessive  
 La lecture d'un document XML contenant un grand nombre de noms locaux uniques, d'espaces de noms ou de préfixes peut poser problème. Si vous utilisez une classe dérivée de <xref:System.Xml.XmlReader> et que vous appelez la propriété <xref:System.Xml.XmlReader.LocalName%2A>, <xref:System.Xml.XmlReader.Prefix%2A> ou <xref:System.Xml.XmlReader.NamespaceURI%2A> pour chaque élément, la chaîne retournée est ajoutée à <xref:System.Xml.NameTable>. La collection détenue par <xref:System.Xml.NameTable> ne diminue jamais en taille et crée une « fuite de mémoire » virtuelle des handles de chaîne.  
  
 Les solutions d'atténuation des risques sont les suivantes :  
  
-   Dérivez de la classe <xref:System.Xml.NameTable> et appliquez un quota de taille maximale. (Vous ne pouvez pas empêcher l'utilisation d'un <xref:System.Xml.NameTable> ou basculer <xref:System.Xml.NameTable> lorsqu'il est plein.)  
  
-   Évitez également d'employer les propriétés mentionnées et utilisez plutôt la méthode <xref:System.Xml.XmlReader.MoveToAttribute%2A> avec la méthode <xref:System.Xml.XmlReader.IsStartElement%2A> dans la mesure du possible ; ces méthodes ne retournant pas de chaînes, la collection <xref:System.Xml.NameTable> n'est pas saturée.  
  
## <a name="malicious-client-sends-excessive-license-requests-to-service"></a>Envoi d'un nombre excessif de demandes de licence à un service par un client malveillant  
 Si un client malveillant bombarde un service de demandes de licence, il peut induire une utilisation excessive de la mémoire par le serveur.  
  
 Atténuation : utilisez les propriétés suivantes de la classe <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings> :  
  
-   <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.MaxCachedCookies%2A> : contrôle le nombre maximal de `SecurityContextToken`s limités par le temps que le serveur met en cache après une négociation `SPNego` ou `SSL`.  
  
-   <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.IssuedCookieLifetime%2A> : contrôle la durée de vie des `SecurityContextTokens` que le serveur émet après une négociation `SPNego` ou `SSL`. Le serveur met en cache les `SecurityContextToken`s pendant cette période.  
  
-   <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.MaxPendingSessions%2A> : contrôle le nombre maximal de conversations sécurisées établies au niveau du serveur mais pour lesquelles aucun message d'application n'a été traité. Ce quota empêche les clients d'établir des conversations sécurisées au niveau du service, en forçant ainsi le service à conserver un état par client, sans jamais les utiliser.  
  
-   <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.InactivityTimeout%2A> : contrôle la durée maximale pendant laquelle le service garde une conversation sécurisée active sans recevoir de message d'application du client pour la conversation. Ce quota empêche les clients d'établir des conversations sécurisées au niveau du service, en forçant ainsi le service à conserver un état par client, sans jamais les utiliser.  
  
## <a name="wsdualhttpbinding-or-dual-custom-bindings-require-client-authentication"></a>Les liaisons WSDualHttpBinding ou les liaisons personnalisées doubles requièrent l'authentification du client  
 Par défaut, la sécurité est activée pour <xref:System.ServiceModel.WSDualHttpBinding>. Toutefois, si l'authentification du client est désactivée en affectant à la propriété <xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A> la valeur <xref:System.ServiceModel.MessageCredentialType.None>, il est possible qu'un utilisateur malveillant provoque une attaque par déni de service sur un service tiers. Ce risque existe car un client malveillant peut commander au service d'envoyer un flux de messages à un service tiers.  
  
 Pour atténuer ce risque, n'attribuez pas à la propriété la valeur `None`. Par ailleurs, ayez ce risque en tête lorsque vous créez une liaison personnalisée avec un modèle de message double.  
  
## <a name="auditing-event-log-can-be-filled"></a>Risque de saturation du journal des événements d'audit  
 Si un utilisateur malveillant se rend compte que l'audit est activé, l'intrus peut envoyer des messages non valides pour forcer l'écriture d'entrées d'audit. Si le journal d'audit se remplit de cette manière, le système d'audit échoue.  
  
 Pour minimiser ce problème, affectez à la propriété <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> la valeur `true` et utilisez les propriétés de l'Observateur d'événements pour contrôler le comportement d'audit. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]à l’aide de l’Observateur d’événements pour afficher et gérer les journaux des événements, consultez [Observateur d’événements](http://go.microsoft.com/fwlink/?LinkId=186123). [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Audit](../../../../docs/framework/wcf/feature-details/auditing-security-events.md).  
  
## <a name="invalid-implementations-of-iauthorizationpolicy-can-cause-service-hangs"></a>Une implémentation non valide de la stratégie IAuthorizationPolicy peut provoquer le blocage du service  
 L'appel de la méthode <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%2A> sur une implémentation défaillante de l'interface <xref:System.IdentityModel.Policy.IAuthorizationPolicy> peut provoquer le blocage du service.  
  
 Atténuation : utilisez uniquement un code de confiance. Autrement dit, utilisez uniquement un code que vous avez vous-même écrit et testé, ou qui provient d'un fournisseur approuvé. N'autorisez pas les extensions non fiables de <xref:System.IdentityModel.Policy.IAuthorizationPolicy> à s'intégrer à votre code sans prendre toutes les précautions requises. Cela s'applique à toutes les extensions utilisées dans une implémentation de service. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ne fait pas de distinction entre du code d'application et du code étranger intégré à l'aide de points d'extensibilité.  
  
## <a name="kerberos-maximum-token-size-may-need-resizing"></a>La taille maximale de jeton Kerberos peut devoir être redimensionnée  
 Si un client appartient à un grand nombre de groupes (approximativement 900, bien que le nombre réel varie selon les groupes), un problème peut se produire lorsque le bloc d'un en-tête de message dépasse 64 kilo-octets. Dans ce cas, vous pouvez augmenter la taille maximale de jeton Kerberos, comme décrit dans l’article du Support technique de Microsoft «[l’authentification Kerberos d’Internet Explorer ne fonctionne pas en raison d’une mémoire tampon insuffisante, se connectant à IIS](http://go.microsoft.com/fwlink/?LinkId=89176). » Vous devrez peut-être également augmenter la taille maximale des messages [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] pour l'adapter au jeton Kerberos le plus volumineux.  
  
## <a name="autoenrollment-results-in-multiple-certificates-with-same-subject-name-for-machine"></a>L'inscription automatique provoque la création de plusieurs certificats avec le même nom de sujet pour l'ordinateur  
 *L’inscription automatique* est la capacité de [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] pour inscrire automatiquement des utilisateurs et ordinateurs pour les certificats. Lorsqu’un ordinateur se trouve sur un domaine dans lequel cette fonctionnalité est activée, un certificat X.509, dont le rôle prévu est d’authentifier les clients, est créé automatiquement et inséré dans le magasin de certificats personnels de l’ordinateur local à chaque fois qu’un nouvel ordinateur est joint au réseau. Toutefois, l'inscription automatique utilise le même nom de sujet pour tous les certificats qu'il crée dans le cache.  
  
 Par conséquent, les services [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] risquent de ne pas pouvoir s'ouvrir sur les domaines dans lesquels l'inscription automatique est activée. Cela est dû au fait que les critères de recherche d'informations d'identification X.509 du service par défaut peuvent être ambigus car il existe plusieurs certificats portant le nom DNS (Domain Name System) complet de l'ordinateur. Un certificat peut provenir de l'inscription automatique tandis qu'un autre peut être un certificat auto-publié.  
  
 Pour atténuer ce risque, référence le certificat exact à utiliser à l’aide d’un critère de recherche plus précis sur le [ \<serviceCredentials >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md). Par exemple, utilisez l'option <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindByThumbprint> et spécifiez le certificat par son empreinte numérique unique (hachage).  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]la fonctionnalité d’inscription automatique, consultez [inscription automatique des certificats dans Windows Server 2003](http://go.microsoft.com/fwlink/?LinkId=95166).  
  
## <a name="last-of-multiple-alternative-subject-names-used-for-authorization"></a>Dernier des noms de sujet de remplacement utilisés pour l'autorisation  
 Dans les rares cas où un certificat X.509 contient plusieurs noms de sujet de remplacement, et que vous autorisez l'utilisation du nom de sujet de remplacement, l'autorisation peut échouer.  
  
## <a name="protect-configuration-files-with-acls"></a>Protection des fichiers de configuration avec des listes ACL  
 Vous pouvez spécifier des revendications requises et facultatives dans des fichiers de code et de configuration pour des jetons émis par [!INCLUDE[infocard](../../../../includes/infocard-md.md)]. Cette procédure entraîne l'émission d'éléments correspondants dans les messages `RequestSecurityToken` envoyés au service de jeton de sécurité. Un intrus peut modifier un code ou une configuration pour supprimer des revendications requises ou facultatives et éventuellement faire en sorte que le service de jeton de sécurité publie un jeton qui n'autorise pas l'accès au service cible.  
  
 Pour atténuer ce risque : imposez l'obligation d'accéder à l'ordinateur pour pouvoir modifier le fichier de configuration. Utilisez les listes de contrôle d'accès au fichier (ACL) pour sécuriser les fichiers de configuration. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] exige que le code soit placé dans le répertoire de l'application ou le Global Assembly Cache avant d'autoriser son chargement à partir de la configuration. Utilisez des listes ACL de répertoire pour sécuriser des répertoires.  
  
## <a name="maximum-number-of-secure-sessions-for-a-service-is-reached"></a>Atteinte du nombre maximal de sessions sécurisées pour un service  
 Lorsqu'un client est correctement authentifié par un service et qu'une session sécurisée est établie avec ce dernier, le service effectue le suivi de la session jusqu'à ce qu'elle soit annulée par le client ou qu'elle expire. Chaque session établie est décomptée du nombre maximal de sessions simultanées actives pour un service. Lorsque cette limite est atteinte, les clients qui essaient de créer une session avec ce service sont rejetés jusqu'à ce qu'une ou plusieurs sessions actives expirent ou soient annulées par un client. Un client peut ouvrir plusieurs sessions sur un service, chacune de ces sessions étant décomptée du nombre limite.  
  
> [!NOTE]
>  Lorsque vous utilisez des sessions avec état, le paragraphe précédent ne s’applique pas. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]les sessions avec état, consultez [Comment : créer un jeton de contexte de sécurité pour une Session sécurisée](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md).  
  
 Pour atténuer ce risque, paramétrez le nombre maximal de sessions actives et la durée de vie maximale d'une session en définissant la propriété <xref:System.ServiceModel.Channels.SecurityBindingElement> de la classe <xref:System.ServiceModel.Channels.SecurityBindingElement>.  
  
## <a name="see-also"></a>Voir aussi  
 [Considérations relatives à la sécurité](../../../../docs/framework/wcf/feature-details/security-considerations-in-wcf.md)  
 [Divulgation d’informations](../../../../docs/framework/wcf/feature-details/information-disclosure.md)  
 [Élévation de privilèges](../../../../docs/framework/wcf/feature-details/elevation-of-privilege.md)  
 [Déni de service](../../../../docs/framework/wcf/feature-details/denial-of-service.md)  
 [Attaques par relecture](../../../../docs/framework/wcf/feature-details/replay-attacks.md)  
 [Falsification](../../../../docs/framework/wcf/feature-details/tampering.md)  
 [Scénarios non pris en charge](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md)
