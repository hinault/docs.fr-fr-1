---
title: "Comment&#160;: s&#233;curiser un service avec un certificat X.509 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2d06c2aa-d0d7-4e5e-ad7e-77416aa1c10b
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# Comment&#160;: s&#233;curiser un service avec un certificat X.509
La sécurisation d'un service avec un certificat X.509 est une technique de base que la plupart des liaisons dans [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] utilisent.Cette rubrique décrit les étapes de la configuration d'un service auto\-hébergé avec un certificat X.509.  
  
 L'une des conditions préalables est de disposer d'un certificat valide pouvant être utilisé pour authentifier le serveur.Le certificat doit être envoyé au serveur par une autorité de certification approuvée.Si le certificat n'est pas valide, les clients qui essayeront d'utiliser le service ne lui feront pas confiance, et par conséquent aucune connexion ne sera établie.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] l'utilisation de certificats, consultez [Utilisation des certificats](../../../../docs/framework/wcf/feature-details/working-with-certificates.md).  
  
### Pour configurer un service avec un certificat à l'aide du code  
  
1.  Créez le contrat de service et le service implémenté.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Conception et implémentation de services](../../../../docs/framework/wcf/designing-and-implementing-services.md).  
  
2.  Créez une instance de la classe <xref:System.ServiceModel.WSHttpBinding> et affectez <xref:System.ServiceModel.SecurityMode> à son mode de sécurité, tel qu'indiqué dans le code suivant.  
  
     [!code-csharp[C_SecureWithCertificate#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#1)]
     [!code-vb[C_SecureWithCertificate#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#1)]  
  
3.  Créez deux variables <xref:System.Type>, une pour le type de contrat et l'autre pour le contrat implémenté, tel qu'indiqué dans le code suivant.  
  
     [!code-csharp[C_SecureWithCertificate#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#2)]
     [!code-vb[C_SecureWithCertificate#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#2)]  
  
4.  Créez une instance de la classe <xref:System.Uri> pour l'adresse de base du service.`WSHttpBinding` utilisant le transport HTTP, l'URI \(Uniform Resource Identifier\) doit commencer par ce schéma, sinon [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] lèvera une exception lors de l'ouverture du service.  
  
     [!code-csharp[C_SecureWithCertificate#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#3)]
     [!code-vb[C_SecureWithCertificate#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#3)]  
  
5.  Créez une nouvelle instance de la classe <xref:System.ServiceModel.ServiceHost> avec la variable de type de contrat implémentée et l'URI.  
  
     [!code-csharp[C_SecureWithCertificate#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#4)]
     [!code-vb[C_SecureWithCertificate#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#4)]  
  
6.  Ajoutez <xref:System.ServiceModel.Description.ServiceEndpoint> au service à l'aide de la méthode <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A>.Transmettez le contrat, la liaison et une adresse de point de terminaison au constructeur, tel qu'indiqué dans le code suivant.  
  
     [!code-csharp[C_SecureWithCertificate#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#5)]
     [!code-vb[C_SecureWithCertificate#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#5)]  
  
7.  Facultatif.Pour récupérer les métadonnées du service, créez un objet <xref:System.ServiceModel.Description.ServiceMetadataBehavior> et affectez `true` à la propriété <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A>.  
  
     [!code-csharp[C_SecureWithCertificate#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#6)]
     [!code-vb[C_SecureWithCertificate#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#6)]  
  
8.  Utilisez la méthode <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> de la classe <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential> pour ajouter le certificat valide au service.La méthode peut utiliser l'une des nombreuses options disponibles pour rechercher un certificat.Cet exemple utilise l'énumération <xref:System.Security.Cryptography.X509Certificates.X509FindType>.L'énumération spécifie que la valeur fournie est le nom de l'entité à laquelle le certificat a été envoyé.  
  
     [!code-csharp[C_SecureWithCertificate#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#7)]
     [!code-vb[C_SecureWithCertificate#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#7)]  
  
9. Appelez la méthode <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> pour commencer l'écoute du service.Si vous créez une application console, appelez la méthode <xref:System.Console.ReadLine%2A> pour maintenir l'écoute du service.  
  
     [!code-csharp[C_SecureWithCertificate#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#8)]
     [!code-vb[C_SecureWithCertificate#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#8)]  
  
## Exemple  
 L'exemple suivant utilise la méthode <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> pour configurer un service avec un certificat X.509.  
  
 [!code-csharp[C_SecureWithCertificate#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#9)]
 [!code-vb[C_SecureWithCertificate#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#9)]  
  
## Compilation du code  
 Les espaces de noms suivants sont requis pour compiler le code :  
  
-   <xref:System>  
  
-   <xref:System.ServiceModel>  
  
-   <xref:System.ServiceModel.Channels>  
  
-   <xref:System.Web.Services.Description>  
  
-   <xref:System.Security.Cryptography.X509Certificates>  
  
-   <xref:System.Runtime.Serialization>  
  
## Voir aussi  
 [Utilisation des certificats](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)