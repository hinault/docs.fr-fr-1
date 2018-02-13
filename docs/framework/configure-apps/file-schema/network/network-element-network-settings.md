---
title: "&lt;réseau&gt; élément (paramètres réseau)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#network
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings/smtp/network
helpviewer_keywords:
- <network> element
- network element
ms.assetid: 2c2c6ad4-ed11-48ab-b28e-2bc0ba9b42c7
caps.latest.revision: 
author: mcleblanc
ms.author: markl
manager: markl
ms.workload:
- dotnet
ms.openlocfilehash: 913765a4d8ac12d25dff446439f6a7510e6067ae
ms.sourcegitcommit: cf22b29db780e532e1090c6e755aa52d28273fa6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="ltnetworkgt-element-network-settings"></a>&lt;réseau&gt; élément (paramètres réseau)
Configure les options réseau pour un serveur SMTP Simple Mail Transport Protocol () externe.  
  
 \<configuration>  
\<system.net>  
\<mailSettings>  
\<smtp>  
\<network>  
  
## <a name="syntax"></a>Syntaxe  
  
```xml  
<network  
  clientDomain="string"   
  defaultCredentials="true|false"  
  enableSsl="true|false"  
  host="string"   
  password="string"  
  port="integer"   
  targetName="string"  
  userName="string"  
/>  
```  
  
## <a name="attributes-and-elements"></a>Attributs et éléments  
 Les sections suivantes décrivent des attributs, des éléments enfants et des éléments parents.  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|  
|---------------|-----------------|  
|`clientDomain`|Spécifie le nom de domaine client à utiliser dans la requête initiale de protocole SMTP pour se connecter au serveur de messagerie SMTP. La valeur par défaut est le nom d’hôte local de l’ordinateur local envoie la demande.|  
|`defaultCredentials`|Spécifie si les informations d’identification des utilisateurs par défaut doivent être utilisées pour accéder au serveur de messagerie SMTP pour les transactions SMTP. La valeur par défaut est `false`.|  
|`enableSsl`|Indique si SSL est utilisé pour accéder à un serveur de messagerie SMTP. La valeur par défaut est `false`.|  
|`host`|Spécifie le nom d’hôte du serveur de messagerie SMTP à utiliser pour les transactions SMTP. Il n’y a aucune valeur par défaut pour cet attribut.|  
|`password`|Spécifie le mot de passe à utiliser pour l’authentification sur le serveur de messagerie SMTP. Il n’y a aucune valeur par défaut pour cet attribut.|  
|`port`|Spécifie le numéro de port à utiliser pour se connecter au serveur de messagerie SMTP. La valeur par défaut est 25.|  
|`targetName`|Spécifie le nom de fournisseur de Service (SPN) à utiliser pour l’authentification lors de l’utilisation de la protection étendue pour les transactions SMTP. Il n’y a aucune valeur par défaut pour cet attribut.|  
|`userName`|Spécifie le nom d’utilisateur à utiliser pour l’authentification sur le serveur de messagerie SMTP. Il n’y a aucune valeur par défaut pour cet attribut.|  
  
### <a name="child-elements"></a>Éléments enfants  
 Aucun.  
  
### <a name="parent-elements"></a>Éléments parents  
  
|Élément|Description|  
|-------------|-----------------|  
|[\<SMTP >, élément (paramètres réseau)](../../../../../docs/framework/configure-apps/file-schema/network/smtp-element-network-settings.md)|Configure les options d’envoi du courrier SMTP Simple Mail Transport Protocol ().|  
  
## <a name="remarks"></a>Notes  
 Certains serveurs SMTP exigent que vous vous authentifier auprès du serveur avant des utiliser. Si vous souhaitez vous authentifier en utilisant les informations d’identification de réseau par défaut sur votre ordinateur hôte, définissez le `defaultCredentials` attribut `true`. Le <xref:System.Net.Configuration.SmtpNetworkElement.DefaultCredentials%2A?displayProperty=nameWithType> propriété peut être utilisée pour obtenir la valeur actuelle de la `defaultCredentials` attribut à partir des fichiers de configuration applicables.  
  
 Vous pouvez également utiliser l’authentification de base (nom d’utilisateur et mot de passe) pour vous authentifier auprès du serveur SMTP. Pour utiliser cette option, vous devez spécifier un nom d’utilisateur valide et un mot de passe pour le serveur SMTP spécifié.  
  
> [!NOTE]
>  L’authentification de base envoie les `userName` et `password` valeurs non chiffrées au serveur. Toute personne analyse du trafic réseau peut afficher vos informations d’identification et les utiliser pour se connecter au serveur. Vous devez envisager d’utiliser un mécanisme d’authentification plus sécurisé, telles que Kerberos ou NT LAN Manager (NTLM). Si `defaultCredentials` est `true`, Kerberos ou NTLM sera utilisé si le serveur prend en charge ces protocoles.  
  
 Les options informations d’identification réseau par défaut et l’authentification de base s’excluent mutuellement ; Si vous définissez `defaultCredentials` à `true` et spécifiez un nom d’utilisateur et un mot de passe, les informations d’identification de réseau par défaut sont utilisée, et les données de l’authentification de base sont ignorées.  
  
 L’authentification de base si vous spécifiez un `userName`, vous devez également spécifier un `password` à l’authentification de vous-même au serveur de messagerie.  
  
 Le <xref:System.Net.Configuration.SmtpNetworkElement.UserName%2A?displayProperty=nameWithType> propriété peut être utilisée pour obtenir la valeur actuelle de la `userName` attribut à partir des fichiers de configuration applicables. Le <xref:System.Net.Configuration.SmtpNetworkElement.Password%2A?displayProperty=nameWithType> propriété peut être utilisée pour obtenir la valeur actuelle de la `password` attribut à partir des fichiers de configuration applicables. A `password` attribut ne serait pas entré normalement dans les fichiers de configuration pour des raisons de sécurité.  
  
 Le `clientDomain` attribut modifie le nom de domaine client utilisé dans la requête initiale de protocole SMTP à un serveur SMTP. Le `clientDomain` attribut peut être défini sur le nom de domaine complet de l’ordinateur local, plutôt que le nom d’hôte local qui est utilisé par défaut. Cela fournit une plus grande compatibilité avec les normes de protocole SMTP. La valeur par défaut est le nom d’hôte local de l’ordinateur local envoie la demande. Le <xref:System.Net.Configuration.SmtpNetworkElement.ClientDomain%2A?displayProperty=nameWithType> propriété peut être utilisée pour obtenir la valeur actuelle de la `clientDomain` attribut à partir des fichiers de configuration applicables.  
  
 Le `targetName` attribut est utilisé pour l’authentification lors de l’utilisation de la protection étendue. La valeur par défaut est de la forme « SMTPSVC /\<hôte > » où \<hôte > est le nom d’hôte du serveur de messagerie SMTP. Le <xref:System.Net.Configuration.SmtpNetworkElement.TargetName%2A?displayProperty=nameWithType> propriété peut être utilisée pour obtenir la valeur actuelle de la `targetName` attribut à partir des fichiers de configuration applicables.  
  
 Le `enableSsl` attribut spécifie si SSL est utilisé pour accéder à un serveur de messagerie SMTP. La <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType> classe uniquement prend en charge l’Extension du Service SMTP pour SMTP sécurisé sur le protocole TLS tel que défini dans RFC 3207. Dans ce mode, la session SMTP commence sur un canal non chiffré, puis une commande STARTTLS est émise par le client au serveur pour basculer vers une communication sécurisée à l’aide de SSL. Consultez la RFC 3207 publiée par l’IETF Internet Engineering Task Force () pour plus d’informations.  
  
 Une autre méthode de connexion est où une session SSL est établie au préalable avant un autre protocole que les commandes sont envoyées. Cette méthode de connexion est parfois appelée SMTPS et utilise par défaut le port 465. Cette autre méthode de connexion à l’aide de SSL n’est pas pris en charge actuellement.  
  
 Le <xref:System.Net.Configuration.SmtpNetworkElement.EnableSsl%2A?displayProperty=nameWithType> propriété peut être utilisée pour obtenir la valeur actuelle de la `enableSsl` attribut à partir des fichiers de configuration applicables.  
  
## <a name="example"></a>Exemple  
 L’exemple suivant spécifie les paramètres SMTP appropriés pour envoyer un courrier électronique à l’aide des informations d’identification de réseau par défaut.  
  
```xml  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="network">  
        <network  
          clientDomain="www.contoso.com"  
          defaultCredentials="true"  
          enableSsl="false"  
          host="mail.contoso.com"  
          port="25"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Net.Configuration.SmtpNetworkElement?displayProperty=nameWithType>  
 <xref:System.Net.Configuration.SmtpSection?displayProperty=nameWithType>  
 <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>  
 [Schéma des paramètres réseau](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
