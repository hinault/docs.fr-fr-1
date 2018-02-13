---
title: "Collaboration pair à pair"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b6216d88-bccb-4a59-9f1c-9f751708e811
caps.latest.revision: 
author: mcleblanc
ms.author: markl
manager: markl
ms.workload:
- dotnet
ms.openlocfilehash: 5060e12fb6a9fcc1bac1dfe6ccdcbaea9f2e6385
ms.sourcegitcommit: cf22b29db780e532e1090c6e755aa52d28273fa6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="peer-to-peer-collaboration"></a>Collaboration pair à pair
Les réseaux pair à pair utilisent des ordinateurs relativement puissants (des ordinateurs personnels) situés à la périphérie d’Internet et qui permettent davantage que de simples tâches de calcul basées sur le client. L’ordinateur personnel moderne (PC) a un processeur très rapide, une mémoire et un disque dur volumineux, qui sont entièrement utilisées lors de l’exécution des tâches informatiques courantes telles que la messagerie électronique et la navigation sur le Web. Les PC modernes peuvent facilement jouer le rôle de client et de serveur (pair) pour de nombreux types d’applications.  
  
-   L’infrastructure de collaboration pair à pair est une version simplifiée de l’infrastructure pair à pair de Microsoft Windows qui s’appuie sur le service Voisinage immédiat de Windows Vista et des plateformes ultérieures. Elle est particulièrement adaptée pour les applications pair à pair situées dans un sous-réseau pour lequel est exécuté le service Voisinage immédiat. Toutefois, elle peut également être utilisée pour les points de terminaison ou les contacts Internet. Elle comprend le Gestionnaire de contacts commun qui est utilisé par Live Messenger et les autres applications Live pour déterminer la présence, la disponibilité et les points de terminaison des contacts.  
  
-  
  
## <a name="collaboration-applications"></a>Applications de collaboration  
 Une application de collaboration pair à pair classique effectue les étapes suivantes :  
  
-   Le pair détermine l’identité d’un pair qui souhaite héberger une session de collaboration.  
  
-   Une demande d’hébergement de session est envoyée, et le pair hôte accepte de gérer les activités de collaboration.  
  
-   L’hôte invite les contacts du sous-réseau (y compris le demandeur) à une session.  
  
-   Tous les pairs qui souhaitent collaborer peuvent ajouter l’hôte dans leur gestionnaire de contacts.  
  
-   La plupart des pairs envoient une réponse à l’invitation du pair hôte (accepter/décliner) en temps voulu.  
  
-   Tous les pairs qui souhaitent collaborer s’inscrivent au pair hôte.  
  
-   Lorsque les pairs réalisent leur première activité de collaboration, le pair hôte peut ajouter des pairs distants dans son gestionnaire de contacts. Il traite également toutes les réponses à l’invitation pour déterminer qui a accepté, qui a décliné, et qui n’a pas répondu.  Il peut annuler l’invitation pour ceux qui n’ont pas répondu, ou effectuer une autre activité.  
  
-   À ce stade, le pair hôte peut démarrer une session de collaboration avec tous les pairs invités, ou inscrire une application dans l’infrastructure de collaboration.  Les applications P2P utilisent l’infrastructure de collaboration pair à pair et l’espace de noms <xref:System.Net.PeerToPeer.Collaboration> afin de coordonner les communications des jeux, des forums, des téléconférences et d’autres applications de présence sans serveur.  
  
-  
  
## <a name="peer-to-peer-networking-security"></a>Sécurité des réseaux pair à pair  
 Dans un domaine Active Directory, les contrôleurs de domaine fournissent des services d’authentification à l’aide de Kerberos. Dans un environnement pair à pair sans serveur, les pairs doivent fournir leur propre authentification. Pour les réseaux pair à pair, n’importe quel nœud peut servir d’autorité de certification. De cette façon, il n’est plus nécessaire qu’un certificat racine se trouve dans le magasin racine approuvé de chaque pair. L’authentification est assurée à l’aide de certificats auto-signés, au format X.509. Il s’agit des certificats qui sont créés par chaque pair, qui génère la paire clé publique/clé privée, et le certificat qui est signé à l’aide de la clé privée. Le certificat auto-signé est utilisé pour l’authentification et pour fournir des informations sur l’entité pair. Comme l’authentification X.509, l’authentification de réseau pair à pair s’appuie sur une chaîne de certificats liés à une même clé publique approuvée.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Net.PeerToPeer.Collaboration>  
 [À propos de l’espace de noms System.Net.PeerToPeer.Collaboration](../../../docs/framework/network-programming/about-the-system-net-peertopeer-collaboration-namespace.md)
