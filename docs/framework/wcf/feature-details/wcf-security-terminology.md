---
title: "Terminologie relative à la sécurité dans WCF"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [WCF], terminology
- security glossary [WCF]
- security terms [WCF]
ms.assetid: 68dde024-8e51-40ba-804f-ec52d85e9ca9
caps.latest.revision: 
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.workload:
- dotnet
ms.openlocfilehash: 352615238d95cf02788cf88ef412a11ffd2faf37
ms.sourcegitcommit: cf22b29db780e532e1090c6e755aa52d28273fa6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="wcf-security-terminology"></a>Terminologie relative à la sécurité dans WCF
La terminologie utilisée pour aborder la sécurité peut vous sembler peu familière. Cette rubrique explique rapidement certains des termes relatifs à la sécurité, mais ne fournit pas d'informations complètes pour chaque élément.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] les termes utilisés dans [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] plus d’informations, consultez [Concepts fondamentaux Windows Communication Foundation](../../../../docs/framework/wcf/fundamental-concepts.md).  
  
 liste de contrôle d'accès (ACL, Access Control List)  
 Liste des protections de sécurité qui s'appliquent à un objet. (Un objet peut être un fichier, un processus, un événement ou tout autre objet doté d'un descripteur de sécurité.) Une entrée dans une liste de contrôle d'accès (ACL) est une entrée de contrôle d'accès (ACE). Il y a deux types de listes ACL : discrétionnaire et système.  
  
 authentification  
 Processus de vérification qu'un utilisateur, ordinateur, service, ou processus est celui ou ce qu'il prétend être.  
  
 autorisation  
 Acte de contrôler l'accès et les droits à une ressource. Par exemple, permettre aux membres d'un groupe de lire un fichier, mais permettre uniquement aux membres d'un autre groupe de modifier le fichier.  
  
 certificat d'autorité de certification (Certificate Authority ou CA)  
 Identifie l'autorité de certification (CA) qui publie des certificats d'authentification serveur et client pour les serveurs et les clients qui les demandent. Car il contient une clé publique utilisée dans les signatures numériques, il est également appelé un *le certificat de signature*. Si l’autorité de certification est une autorité racine, le certificat d’autorité de certification peut être appelé une *certificat racine*. Également connu comme un *certificat de site*.  
  
 Hiérarchie d'autorités de certification  
 Une hiérarchie d'autorités de certification contient plusieurs CA. Elle est organisée afin que chaque autorité de certification est certifiée par une autre autorité de certification dans un niveau supérieur de la hiérarchie jusqu'à ce que le haut de la hiérarchie, également connu sous le *autorité racine*, est atteinte.  
  
 certificat  
 Déclaration signée numériquement qui contient des informations à propos d'une entité et la clé publique de l'entité, et lie donc ces deux renseignements ensemble. Un certificat est publié par une organisation approuvée (ou entité), appelée autorité de certification, après que l'autorité a vérifié que l'entité est qui elle prétend être.  
  
 Les certificats peuvent contenir des types différents de données. Par exemple, un certificat X.509 inclut le format du certificat, le numéro de série du certificat, l'algorithme utilisé pour signer le certificat, le nom de l'autorité de certification qui a publié le certificat, le nom et la clé publique de l'entité qui demande le certificat, et la signature de l'autorité de certification.  
  
 magasin de certificats  
 En général, magasin permanent dans lequel les certificats, les listes de révocation de certificats (CRL) et les listes de certificats de confiance (CTL) sont stockés. Toutefois, il est possible de créer et d'ouvrir un magasin de certificats en mémoire uniquement lors de l'utilisation de certificats qui ne doivent pas nécessairement être stockés de façon permanente.  
  
 revendications  
 Informations passées d'une entité à une autre et utilisées pour établir l'identité de l'expéditeur. Par exemple, un nom d'utilisateur et un jeton de mot de passe, ou un certificat X.509.  
  
 certificat de client  
 Fait référence à un certificat utilisé pour l'authentification du client, telle que l'authentification d'un navigateur Web sur un serveur Web. Lorsqu’un client de navigateur Web essaie d’accéder à un serveur web sécurisé, le client envoie son certificat au serveur pour lui permettre de vérifier son identité.  
  
 credentials  
 Données d'ouverture de session qu'un principal de sécurité utilise pour établir sa propre identité, telles qu'un mot de passe, ou un ticket de protocole Kerberos. Les informations d'identification sont utilisées pour contrôler l'accès aux ressources.  
  
 données condensées  
 Type de données défini par la norme de chiffrement de clé publique (PKCS) #7 qui se compose de tout type de données plus un hachage de message (condensat) du contenu.  
  
 signature numérique  
 Données qui lient l'identité d'un expéditeur aux informations qui sont envoyées. Une signature numérique peut être fournie avec tout message, fichier, ou autre information encodée numériquement, ou transmise séparément. Les signatures numériques sont utilisées dans les environnements de clé publique et fournissent des services d'authentification et d'intégrité.  
  
 encoding  
 Processus de transformation de données en un flux de bits. L'encodage fait partie du processus de sérialisation qui convertit des données en un flux de uns et zéros.  
  
 paire de clés d'échange  
 Paire de clés publique/privée utilisée pour chiffrer les clés de session de sorte qu'elles puissent être stockées et échangées sans risque avec d'autres utilisateurs.  
  
 hash  
 Valeur numérique de taille fixe obtenue en appliquant une fonction mathématique (voir algorithme de hachage) à une quantité arbitraire de données. Les données incluent généralement des données aléatoires, appelées un *nonce*. Le service et le client échangent des valeurs à usage unique pour augmenter la complexité du résultat. Le résultat est également appelé un *condensat du message*. L'envoi d'une valeur de hachage est plus sûr que l'envoi de données sensibles, telles qu'un mot de passe, même si le mot de passe est chiffré. L'expéditeur et le récepteur du hachage doivent se mettre d'accord sur l'algorithme de hachage et les valeurs à usage unique afin que, une fois reçu, le hachage puisse être vérifié.  
  
 algorithme de hachage  
 Algorithme utilisé pour produire une valeur de hachage d'un échantillon de données, tel qu'un message ou une clé de session. Les algorithmes de hachage typiques incluent MD2, MD4, MD5 et SHA-1.  
  
 protocole Kerberos  
 Protocole qui définit comment les clients interagissent avec un service d'authentification de réseau. Les clients obtiennent des tickets du centre de distribution de clés Kerberos (KDC), et ils présentent ces tickets aux serveurs lorsque les connexions sont établies. Les tickets Kerberos représentent les informations d'identification réseau du client.  
  
 autorité de sécurité locale (Local Security Authority ou LSA)  
 Sous-système protégé qui authentifie des utilisateurs et ouvre une session sur le système local. L'autorité de sécurité locale conserve également des informations à propos de tous les aspects de la sécurité locale sur un système, collectivement connus comme la stratégie de sécurité locale du système.  
  
 Par négociation  
 Fournisseur de prise en charge de la sécurité (SSP) qui agit comme une couche d'application entre le SSPI (Security Support Provider Interface) et d'autres SSP. Lorsqu'une application appelle un SSPI à se connecter à un réseau, il peut spécifier un SSP pour traiter la demande. Si l'application spécifie `Negotiate`, `Negotiate` analyse la demande et choisit le meilleur SSP pour gérer la demande selon la stratégie de sécurité configurée par client.  
  
 valeur à usage unique  
 Valeur générée aléatoirement utilisée pour lutter contre les attaques de « lecture ».  
  
 non répudiation  
 Capacité à identifier des utilisateurs qui ont exécuté certaines actions, donc à contrecarrer irréfutablement toute tentative par un utilisateur pour nier ses responsabilités. Par exemple, un système peut enregistrer l'ID d'un utilisateur à chaque fois qu'un fichier est supprimé.  
  
 norme de chiffrement à clé publique (Public Key Cryptography Standard ou PKCS)  
 Spécifications produites par RSA Data Security, Inc. en collaboration avec des développeurs de systèmes sécurisés dans le monde pour accélérer le déploiement du chiffrement à clé publique.  
  
 PKCS #7  
 Norme de syntaxe de message de chiffrement. Syntaxe générale des données auxquelles le chiffrement peut être appliqué, telles que les signatures numériques et le chiffrement. Elle fournit également la syntaxe pour diffuser au message des certificats ou des listes de révocation de certificats et d'autres attributs de message, tels que les horodatages.  
  
 texte brut  
 Message non chiffré. Messages texte en clair sont parfois appelés *en texte clair* messages.  
  
 privilège  
 Droit d'un utilisateur à exécuter différentes opérations relatives au système, telles que l'arrêt du système, le chargement de pilotes de périphériques, ou la modification de l'heure système. Le jeton d'accès d'un utilisateur contient une liste des privilèges détenus par l'utilisateur ou le groupe d'utilisateurs.  
  
 clé privée  
 Moitié secrète d'une paire de clés utilisée dans un algorithme de clé publique. Les clés privées sont utilisées en général pour chiffrer une clé de session symétrique, signer numériquement un message ou déchiffrer un message qui a été chiffré avec la clé publique correspondante. Consultez également « clé publique ».  
  
 process  
 Contexte de sécurité dans lequel une application s'exécute. En général, le contexte de sécurité est associé à un utilisateur, donc toutes les applications qui s'exécutent dans un processus donné récupèrent les autorisations et les privilèges de l'utilisateur à qui elles appartiennent.  
  
 paire de clés publique/privée  
 Jeu de clés de chiffrement utilisé pour le chiffrement à clé publique. Pour chaque utilisateur, un fournisseur de services de chiffrement (CSP) fournit habituellement deux paires de clés publique/privée : une paire de clés d'échange et une paire de clés de signature numérique. Les deux paires de clés sont conservées d'une session à une autre.  
  
 clé publique  
 Clé de chiffrement utilisée en général pour déchiffrer une clé de session ou une signature numérique. La clé publique peut également être utilisée pour chiffrer un message, ce qui garantit que seule la personne avec la clé privée correspondante peut déchiffrer le message.  
  
 chiffrement à clé publique  
 Chiffrement qui utilise une paire de clés, une clé pour chiffrer des données et une autre clé pour déchiffrer des données. Par opposition, algorithmes de chiffrement symétrique qui utilisent la même clé à la fois pour le chiffrement et le déchiffrement. En pratique, le chiffrement à clé publique est utilisé pour protéger la clé de session qu'un algorithme de chiffrement symétrique utilise. Dans ce cas, la clé publique est utilisée pour chiffrer la clé de session, qui a ensuite été utilisée pour chiffrer des données, et la clé privée est utilisée pour le déchiffrement. En plus de protéger les clés de session, le chiffrement à clé publique peut également être utilisé pour signer un message numériquement (à l'aide de la clé privée) et valider la signature (à l'aide de la clé publique).  
  
 infrastructure de clé publique (Public Key Infrastructure ou PKI)  
 Infrastructure qui fournit un jeu intégré de services et d'outils d'administration pour créer, déployer, et gérer des applications de clé publique.  
  
 répudiation  
 Capacité d'un utilisateur à nier l'exécution d'une action alors que les autres parties ne peuvent prouver le contraire. Par exemple, un utilisateur qui supprime un fichier et qui réussit à le nier.  
  
 autorité racine  
 Autorité de certification en haut d'une hiérarchie d'autorités de certification. L'autorité racine certifie les autorités de certification dans le niveau suivant de la hiérarchie.  
  
 algorithme de hachage sécurisé (Secure Hash Algorithm ou SHA)  
 Algorithme de hachage qui génère un résumé du message. L'algorithme de hachage est utilisé avec l'algorithme de signature numérique (DSA) dans la norme de signature numérique (DSS), entre autres. Il existe quatre types de SHA : SHA-1, SHA-256, SHA-384 et SHA-512. SHA-1 génère un résumé de message en 160 bits. SHA-256, SHA-384 et SHA-512 génèrent respectivement des condensats du message en 256, 384 et 512 bits. L'algorithme SHA a été développé par le National Institute of Standards and Technology (NIST) et par la National Security Agency (NSA).  
  
 SSL (Secure Sockets Layer)  
 Protocole pour les communications réseau sécurisées à l'aide d'une combinaison de technologies de clés publique et secrète.  
  
 contexte de sécurité  
 Attributs ou règles de sécurité actuellement en vigueur. Par exemple, l'utilisateur actuel connecté à l'ordinateur ou le code confidentiel entré par l'utilisateur d'une carte à puce. Pour le SSPI, un contexte de sécurité est une structure de données opaque qui contient des données de sécurité pertinentes à une connexion, telles qu'une clé de session ou une indication de la durée de la session.  
  
 principal de sécurité  
 Entité reconnue par le système de sécurité. Les entités peuvent inclure des utilisateurs humains ainsi que des processus autonomes.  
  
 fournisseur de la prise en charge de la sécurité (Security Support Provider ou SSP)  
 Bibliothèque de liens dynamiques (DLL) qui implémente le SSPI en rendant un ou plusieurs packages de sécurité disponibles aux applications. Chaque package de sécurité fournit des mappages entre les appels de fonction SSPI d'une application et les fonctions d'un modèle de sécurité réel. Les packages de sécurité prennent en charge des protocoles de sécurité tels que l'authentification Kerberos et le Microsoft LAN Manager (LanMan).  
  
 interface du fournisseur de la prise en charge de la sécurité (Security Support Provider Interface ou SSPI)  
 Interface commune entre des applications de niveau transport, telles que l'appel de procédure distante Microsoft (RPC), et des fournisseurs de sécurité, tels que la sécurité distribuée Windows. Le SSPI permet à une application de transport d'appeler l'un des fournisseurs de sécurité pour obtenir une connexion authentifiée. Ces appels ne requièrent pas une connaissance étendue des détails du protocole de sécurité.  
  
 service d'émission de jeton de sécurité  
 Services conçus pour publier et gérer des jetons de sécurité personnalisés (jetons émis) dans un scénario multiservices. Les jetons personnalisés sont en général des jetons SAML (Security Assertions Markup Language) qui incluent des informations d'identification personnalisées.  
  
 certificat de serveur  
 Fait référence à un certificat utilisé pour l’authentification du serveur, telle que l’authentification d’un serveur web sur un navigateur Web. Lorsqu’un client de navigateur Web essaie d’accéder à un serveur web sécurisé, le serveur envoie son certificat au navigateur pour lui permettre de vérifier son identité.  
  
 session  
 Échange de messages sous la protection d'un morceau unique d'élément de génération de clé. Par exemple, les sessions SSL utilisent une clé unique pour envoyer plusieurs messages sous cette clé.  
  
 clé de la session  
 Clé générée aléatoirement qui est utilisée une fois, puis est supprimée. Les clés de session sont symétriques (utilisées à la fois pour le chiffrement et le déchiffrement). Elles sont envoyées avec le message et protégées par chiffrement avec une clé publique auprès du destinataire souhaité. Une clé de session se compose d'un nombre aléatoire de bits, de 40 à 2000.  
  
 informations d'identification supplémentaires  
 Informations d'identification à utiliser pour authentifier un principal de sécurité auprès des domaines de sécurité étrangers.  
  
 chiffrement symétrique  
 Chiffrement qui utilise une clé unique à la fois pour le chiffrement et le déchiffrement. Le chiffrement symétrique est préférable lors du chiffrement de grandes quantités de données. Quelques-uns des algorithmes de chiffrement symétriques les plus communs sont RC2, RC4 et Data Encryption Standard (DES).  
  
 Consultez également « chiffrement à clé publique ».  
  
 clé symétrique  
 Clé unique utilisée à la fois pour le chiffrement et le déchiffrement. Les clés de session sont habituellement symétriques.  
  
 jeton (jeton d'accès)  
 Un jeton d'accès contient les informations de sécurité pour l'ouverture d'une session. Le système crée un jeton d'accès lorsqu'un utilisateur se connecte, et chaque processus exécuté de la part de l'utilisateur possède une copie du jeton. Le jeton identifie l'utilisateur, les groupes de l'utilisateur et les privilèges de l'utilisateur. Le système utilise le jeton pour contrôler l'accès aux objets sécurisables et contrôler la capacité de l'utilisateur à exécuter différentes opérations relatives au système sur l'ordinateur local. Il existe deux types de jetons d'accès, primaire et emprunt d'identité.  
  
 couche de transport  
 Couche réseau qui est responsable à la fois de la qualité du service et de la remise exacte des informations. Parmi les tâches exécutées dans cette couche, citons la détection et la correction des erreurs.  
  
 liste de confiance (liste de certificats de confiance ou CTL)  
 Liste prédéfinie des éléments signés par une entité approuvée. Il peut s'agir d'une liste de hachages de certificats, ou d'une liste de noms de fichiers, par exemple. Tous les éléments dans la liste sont authentifiés (approuvés) par l'entité de signature.  
  
 fournisseur d'approbation  
 Logiciel qui décide si un fichier donné est approuvé. Cette décision est basée sur le certificat associé au fichier.  
  
 nom d'utilisateur principal (User Principal Name ou UPN)  
 Un nom de compte d’utilisateur (parfois appelé le *nom d’utilisateur d’ouverture de session*) et le nom de domaine identifiant le domaine dans lequel se trouve le compte d’utilisateur. Il s'agit de la méthode de connexion standard à un domaine Windows. Le format est : someone@example.com (comme pour une adresse de messagerie).  
  
> [!NOTE]
>  En plus de la forme UPN standard, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] accepte les UPN de la forme de niveau inférieur, comme cohowinery.com\personne.  
  
 X.509  
 Norme reconnue internationalement pour les certificats qui définit leurs parties requises.  
  
## <a name="see-also"></a>Voir aussi  
 [Concepts fondamentaux de Windows Communication Foundation](../../../../docs/framework/wcf/fundamental-concepts.md)  
 [Concepts relatifs à la sécurité](../../../../docs/framework/wcf/feature-details/security-concepts.md)  
 [Modèle de sécurité pour Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
