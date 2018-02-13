---
title: "Modèle de programmation de revendications WIF"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 149cb875-9b1c-4695-b88a-fbf1725a02f9
caps.latest.revision: 
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.workload:
- dotnet
ms.openlocfilehash: 1bd84e6a1e6fb0d4808dca42af2e2916be1133a3
ms.sourcegitcommit: cf22b29db780e532e1090c6e755aa52d28273fa6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="wif-claims-programming-model"></a>Modèle de programmation de revendications WIF
Les développeurs ASP.NET et WCF (Windows Communication Foundation) utilisent généralement les interfaces IIdentity et IPrincipal pour traiter les informations d’identité de l’utilisateur. Dans .NET 4.5, WIF (Windows Identity Foundation) a été intégré pour que les revendications soient maintenant toujours présentes pour tous les principaux, comme illustré dans le diagramme suivant :  
  
 ![Modèle de programmation de revendications WIF](../../../docs/framework/security/media/wifclaimsprogrammingmodel.png "WIFClaimsProgrammingModel")  
  
 Dans .NET 4.5, System.Security.Claims contient les nouvelles classes ClaimsPrincipal et ClaimsIdentity (voir le diagramme ci-dessus). Tous les principaux dans .NET sont désormais dérivés de ClaimsPrincipal. Toutes les classes d’identité intégrées, comme FormsIdentity pour ASP.NET et WindowsIdentity, sont maintenant dérivées de ClaimsIdentity. De même, toutes les classes de principal intégrées comme GenericPrincipal et WindowsPrincipal, sont dérivées de ClaimsPrincipal.  
  
 Une revendication est représentée par la classe <xref:System.Security.Claims.Claim>. Cette classe a les propriétés importantes suivantes :  
  
-   <xref:System.Security.Claims.Claim.Type%2A> représente le type de revendication et est généralement un URI. Par exemple, la revendication d’adresse de messagerie est représentée en tant que `http://schemas.microsoft.com/ws/2008/06/identity/claims/email`.  
  
-   <xref:System.Security.Claims.Claim.Value%2A> contient la valeur de la revendication et est représenté sous forme de chaîne. Par exemple, l’adresse de messagerie peut être représentée en tant que «someone@contoso.com».  
  
-   <xref:System.Security.Claims.Claim.ValueType%2A> représente le type de la valeur de revendication et est généralement un URI. Par exemple, le type chaîne est représenté sous la forme `http://www.w3.org/2001/XMLSchema#string`. Le type valeur doit être un QName conforme au schéma XML. La valeur doit être au format `namespace#format` pour permettre à WIF de générer une valeur QName valide. Si l’espace de noms n’est pas défini correctement, le schéma du code XML généré ne pourra probablement pas être validé, car il n’y aura pas de fichier XSD publié pour cet espace de noms. Le type valeur par défaut est `http://www.w3.org/2001/XMLSchema#string`. Consultez [http://www.w3.org/2001/XMLSchema](http://go.microsoft.com/fwlink/?LinkId=209155) pour obtenir les types valeur connus que vous pouvez utiliser en toute sécurité.  
  
-   <xref:System.Security.Claims.Claim.Issuer%2A> est l’identificateur du service d’émission de jeton de sécurité (STS) qui a émis la revendication. Il peut être représenté sous la forme de l’URL du STS ou bien d’un nom représentant le STS, tel que `https://sts1.contoso.com/sts`.  
  
-   <xref:System.Security.Claims.Claim.OriginalIssuer%2A> est l’identificateur du STS qui a émis la revendication d’origine, quel que soit le nombre de STS spécifiés dans la chaîne. Il est représenté sous la forme <xref:System.Security.Claims.Claim.Issuer%2A>.  
  
-   <xref:System.Security.Claims.Claim.Subject%2A> est l’objet dont l’identité est vérifiée. Il contient un <xref:System.Security.Claims.ClaimsIdentity>.  
  
-   <xref:System.Security.Claims.Claim.Properties%2A> est un dictionnaire qui permet au développeur de fournir les données spécifiques à l’application qui doivent être transférées sur Internet avec les autres propriétés. Il peut être utilisé pour la validation personnalisée.  
  
## <a name="identity-delegation"></a>Délégation d’identité  
 <xref:System.Security.Claims.ClaimsIdentity.Actor%2A> est une propriété importante de <xref:System.Security.Claims.ClaimsIdentity>. Cette propriété permet d’utiliser la délégation des informations d’identification dans un système multiniveau dans lequel un niveau intermédiaire agit comme client pour effectuer des demandes à un service principal.  
  
### <a name="accessing-claims-through-threadcurrentprincipal"></a>Accès aux revendications par Thread.CurrentPrincipal  
 Pour accéder à l’ensemble des revendications de l’utilisateur actuel dans une application par partie de confiance, utilisez `Thread.CurrentPrincipal`.  
  
 L’exemple de code suivant montre comment utiliser cette méthode pour obtenir un System.Security.Claims.ClaimsIdentity :  
  
```  
ClaimsPrincipal claimsPrincipal = Thread.CurrentPrincipal as ClaimsPrincipal;  
```  
  
 Pour plus d'informations, consultez <xref:System.Security.Claims>.  
  
### <a name="role-claim-type"></a>Type de revendication de rôle  
 La configuration de votre application par partie de confiance nécessite aussi de déterminer le type de votre revendication de rôle. Ce type de revendication est utilisé par System.Security.Claims.ClaimsPrincipal.IsInRole(System.String). Le type de revendication par défaut est `http://schemas.microsoft.com/ws/2008/06/identity/claims/role`.  
  
### <a name="claims-extracted-by-windows-identity-foundation-from-different-token-types"></a>Revendications extraites par Windows Identity Foundation à partir de différents types de jetons  
 WIF prend en charge plusieurs combinaisons de mécanismes d’authentification intégrés. Le tableau suivant répertorie les revendications extraites par WIF à partir de différents types de jetons.  
  
|Type de jeton|Revendication générée|Correspondance avec le jeton d’accès Windows|  
|-|-|-|  
|SAML 1.1|1.  Toutes les revendications générées à partir de System.IdentityModel.SecurityTokenService.GetOutputClaimsIdentity(System.Security.Claims.ClaimsPrincipal,System.IdentityModel.Protocols.WSTrust.RequestSecurityToken,System.IdentityModel.Scope).<br />2.  La revendication `http://schemas.microsoft.com/ws/2008/06/identity/claims/confirmationkey` qui contient la sérialisation XML de la clé de confirmation, si le jeton contient un jeton de preuve.<br />3.  La revendication `http://schemas.microsoft.com/ws/2008/06/identity/claims/samlissuername` générée à partir de l’élément émetteur Issuer.<br />4.  Les revendications AuthenticationMethod et AuthenticationInstant, si le jeton contient une instruction d’authentification.|En plus des revendications répertoriées dans « SAML 1.1 », à l’exception des revendications de type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`, les revendications liées à l’authentification Windows sont générées et l’identité est représentée par WindowsClaimsIdentity.|  
|SAML 2.0|Identique à « SAML 1.1 ».|Identique à « SAML 1.1 mappé au compte Windows ».|  
|X509|1.  Les revendications avec les propriétés nom unique X500, emailName, dnsName, SimpleName, UpnName, UrlName, thumbprint, RsaKey (extraction à l’aide de la méthode RSACryptoServiceProvider.ExportParameters de la propriété X509Certificate2.PublicKey.Key), DsaKey (extraction à l’aide de la méthode DSACryptoServiceProvider.ExportParameters de la propriété X509Certificate2.PublicKey.Key) et SerialNumber générées à partir du certificat X509.<br />2.  La revendication AuthenticationMethod avec la valeur `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509`. La revendication AuthenticationInstant avec la valeur d’horodatage de la validation du certificat au format DateTime XMLSchema.|1.  Utilise le nom de domaine complet du compte Windows comme valeur de la revendication `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`. .<br />2.  Les revendications générées à partir du certificat X509 non mappé à Windows, et les revendications générées à partir du compte Windows en mappant le certificat à Windows.|  
|UPN|1.  Les revendications sont similaires aux revendications répertoriées dans la section de l’authentification Windows.<br />2.  La revendication AuthenticationMethod avec la valeur `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`. La revendication AuthenticationInstant avec la valeur d’horodatage de la validation du mot de passe au format DateTime XMLSchema.||  
|Windows (Kerberos ou NTLM)|1.  Les revendications générées à partir du jeton d’accès, telles que PrimarySID, DenyOnlyPrimarySID, PrimaryGroupSID, DenyOnlyPrimaryGroupSID, GroupSID, DenyOnlySID et Name.<br />2.  AuthenticationMethod avec la valeur `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows`. La revendication AuthenticationInstant avec la valeur d’horodatage de la création du jeton d’accès Windows au format DateTime XMLSchema.||  
|Paire de clés RSA|1.  La revendication `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/rsa` avec la valeur de RSAKeyValue.<br />2.  La revendication AuthenticationMethod avec la valeur `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/signature`. La revendication AuthenticationInstant avec la valeur d’horodatage de l’authentification de la clé RSA (vérification de la signature) au format DateTime XMLSchema.||  
  
|Type d’authentification|URI émis dans une revendication AuthenticationMethod|  
|-|-|  
|Mot de passe|`urn:oasis:names:tc:SAML:1.0:am:password`|  
|Kerberos|`urn:ietf:rfc:1510`|  
|SecureRemotePassword|`urn:ietf:rfc:2945`|  
|TLSClient|`urn:ietf:rfc:2246`|  
|X509|`urn:oasis:names:tc:SAML:1.0:am:X509-PKI`|  
|PGP|`urn:oasis:names:tc:SAML:1.0:am:PGP`|  
|Spki|`urn:oasis:names:tc:SAML:1.0:am:SPKI`|  
|XmlDSig|`urn:ietf:rfc:3075`|  
|Non spécifié|`urn:oasis:names:tc:SAML:1.0:am:unspecified`|
