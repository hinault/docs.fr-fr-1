---
title: "Configuration requise pour le .NET Framework"
description: "Découvrez la configuration requise en termes de matériel, de système d’exploitation et de logiciels pour installer .NET Framework 4.5 et versions ultérieures."
ms.custom: updateeachrelease
ms.date: 02/02/2018
ms.prod: .net-framework
ms.technology:
- dotnet-clr
ms.topic: article
helpviewer_keywords:
- software requirements
- .NET Framework, system requirements
- system requirements
- operating systems supported
- hardware requirements
ms.assetid: 298275e2-da1d-4618-9f74-6a3567832350
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: a0cfbcbc4c2c0857c1fe4163484a43f4521444a3
ms.sourcegitcommit: be1fb5d9447ad459bef22b91a91c72e3e0b2d916
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/09/2018
---
# <a name="net-framework-system-requirements"></a>Configuration requise pour le .NET Framework

Les tableaux de cette rubrique indiquent la configuration matérielle et logicielle requise, ainsi que celle du système d'exploitation pour les versions .NET Framework suivantes :

* .NET Framework 4.5 et ses versions intermédiaires (4.5.1 et 4.5.2).
* .NET Framework 4.6 et ses versions intermédiaires (4.6.1 et 4.6.2).
* .NET Framework 4.7 et sa version intermédiaire (4.7.1).

Les environnements de développement qui vous permettent de développer des applications pour le .NET Framework ont des exigences différentes.

> [!IMPORTANT]
> Toutes les versions .NET Framework depuis la version .NET Framework 4 sont des mises à jour sur place, donc une seule version 4.x peut être présente sur un système.
> En outre, des versions .NET Framework spécifiques sont pré-installées sur certaines versions du système d’exploitation Windows. Cela signifie que :
>
> * Si une version ultérieure est déjà installée sur l’ordinateur, vous ne pouvez pas installer une version 4.x précédente.
> * Si une version .NET spécifique est pré-installée sur le système d’exploitation, vous ne pouvez pas installer une version 4.x précédente sur le même ordinateur.
> * Si vous installez une version ultérieure, il est inutile de désinstaller d’abord la version précédente.

Pour obtenir des informations et des liens pour le téléchargement, consultez [Installer le .NET Framework pour les développeurs](../../../docs/framework/install/guide-for-developers.md).

Pour plus d’informations sur le cycle de vie du support des versions du .NET Framework, consultez [Cycle de vie de support des produits Microsoft](https://support.microsoft.com/en-us/lifecycle/search?sort=PN&alpha=Microsoft%20.NET%20Framework&Filter=FilterNO).

## <a name="hardware-requirements"></a>Configuration matérielle requise

|                          |        |
| ------------------------ | ------ |
| **Processeur**            | 1 GHz  |
| **Mémoire vive**                  | 512 Mo |
| **Espace disque (minimum)** |        |
| 32 bits                   | 4,5 Go |
| 64 bits                   | 4,5 Go |

## <a name="installation-requirements"></a>Configuration requise pour l’installation

L’installation du .NET Framework nécessite des privilèges d’administrateur. Si vous n’avez pas de droits d’administrateur sur l’ordinateur sur lequel vous voulez installer le .NET Framework, contactez votre administrateur réseau.

## <a name="supported-client-operating-systems"></a>Systèmes d'exploitation clients pris en charge

| Système d'exploitation | Éditions prises en charge | Préinstallé avec le système d'exploitation | Installable séparément |
| ---------------- | ------------------ | ------------------------ | ---------------------- |
| Windows 10 Fall Creators Update | 32 bits et 64 bits | .NET Framework 4.7.1 | |
| Windows 10 Creators Update | 32 bits et 64 bits | .NET Framework 4.7 | .NET Framework 4.7.1 | 
| Mise à jour anniversaire Windows 10 | 32 bits et 64 bits | [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]|.NET Framework 4.7<br/><br/>.NET Framework 4.7.1 |
| Mise à jour de novembre de Windows 10 | 32 bits et 64 bits | .NET Framework 4.6.1 | .NET Framework 4.6.2 |
| Windows 10 | 32 bits et 64 bits | .NET Framework 4.6 | .NET Framework 4.6.1 <br/><br/> .NET Framework 4.6.2 |
| [!INCLUDE[win81](../../../includes/win81-md.md)] | 32 bits, 64 bits et ARM | [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] | [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]<br /><br /> [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]<br /><br />.NET Framework 4.7<br/><br/>.NET Framework 4.7.1 |
| [!INCLUDE[win8](../../../includes/win8-md.md)] | 32 bits, 64 bits et ARM | [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] | [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] |
| Windows 7 SP1|32 bits et 64 bits | -- | .NET Framework 4<br /><br /> [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]<br /><br /> [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]<br /><br /> [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]<br /><br />.NET Framework 4.7<br/><br/>.NET Framework 4.7.1|
| Windows Vista SP2|32 bits et 64 bits | -- | .NET Framework 4<br /><br /> [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]<br /><br /> [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] |
| Windows XP |32 bits et 64 bits | -- | .NET Framework 4 |

 **Remarques :**

- Sur les systèmes Windows 7, le .NET Framework nécessite Windows 7 SP1. Si vous êtes sur Windows 7 et que vous n’avez pas encore installé le Service Pack 1, vous devez le faire avant d’installer le .NET Framework.

- Le [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] est pris en charge sur l'environnement Windows PE (Windows Preinstallation Environment). Les fonctionnalités ne sont pas toutes prises en charge dans Windows PE.

- .NET Framework 4 prend également en charge la plateforme IA64.

- Pour toutes les plateformes, nous recommandons d’effectuer une mise à niveau vers le dernier Service Pack Windows et d’installer les mises à jour critiques disponibles à partir du [site web Windows Update](http://go.microsoft.com/fwlink/?LinkId=168461) afin de garantir une compatibilité et une sécurité optimales.

- Sur les systèmes d'exploitation 64 bits, le .NET Framework prend en charge WOW64 (processus 32 bits sur un ordinateur 64 bits) et le processus 64 bits natif.

## <a name="supported-server-operating-systems"></a>Systèmes d'exploitation serveurs pris en charge

| Système d'exploitation | Éditions prises en charge | Préinstallé avec le système d'exploitation | Installable séparément |
| ---------------- | ------------------ | ------------------------ | ---------------------- |
| Windows Server, version 1709 | 64 bits | .NET Framework 4.7.1 | -- |
| Windows Server 2016 | 64 bits | [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] | .NET Framework 4.7<br/><br/> .NET Framework 4.7.1 |
| Windows Server 2012 R2 | 64 bits | [!INCLUDE[net_v451](../../../includes/net-v451-md.md)] | [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]<br /><br /> [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]<br /><br />.NET Framework 4.7<br/><br/> .NET Framework 4.7.1 |
| Windows Server 2012 (édition 64 bits) | 64 bits| [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] | [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]<br /><br /> [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]<br /><br />.NET Framework 4.7<br/><br/>.NET Framework 4.7.1 |
| Windows Server 2008 R2 SP1|64 bits | -- | .NET Framework 4<br /><br /> [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]<br /><br /> [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]<br /><br /> [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]<br /><br /> [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]<br /><br />.NET Framework 4.7<br/><br/>.NET Framework 4.7.1 |
| Windows Server 2008 SP2|32 bits et 64 bits | -- | .NET Framework 4<br /><br /> [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]<br /><br /> [!INCLUDE[net_v451](../../../includes/net-v451-md.md)]<br /><br /> [!INCLUDE[net_v452](../../../includes/net-v452-md.md)]<br /><br /> [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] |

 **Remarques :**

- [!INCLUDE[winserver8](../../../includes/winserver8-md.md)] inclut le [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], il n’est donc pas nécessaire de l’installer séparément. De même, [!INCLUDE[winblue_server_2](../../../includes/winblue-server-2-md.md)] inclut le [!INCLUDE[net_v451](../../../includes/net-v451-md.md)].

- Le .NET Framework offre une prise en charge limitée du rôle Server Core avec Windows Server 2008 R2 SP1 ou ultérieur. Pour obtenir la liste des API non prises en charge, consultez la [fonctionnalité .NET Server Core](https://msdn.microsoft.com/library/ee391632.aspx).

- Le .NET Framework n’est pas pris en charge sur Windows Server 2008 R2 pour les systèmes Itanium.

- Sur Windows Server 2008 SP2, le .NET Framework n’est pas pris en charge dans le rôle principal du serveur.

- Pour toutes les plateformes, nous recommandons une mise à niveau vers le dernier Service Pack Windows et le téléchargement des mises à jour critiques disponibles depuis le [site web Windows Update](http://go.microsoft.com/fwlink/?LinkId=168461) afin de garantir une compatibilité et une sécurité optimales. L'installation du dernier Service Pack Windows peut être obligatoire sur certains systèmes d'exploitation.

- Sur les systèmes d'exploitation 64 bits, le .NET Framework prend en charge WOW64 (processus 32 bits sur un ordinateur 64 bits) et le processus 64 bits natif.

## <a name="see-also"></a>Voir aussi

[Guide d’installation](../../../docs/framework/install/index.md)   
[Bien démarrer](../../../docs/framework/get-started/index.md)   
[Résolution des problèmes liés aux installations et désinstallations bloquées du .NET Framework](../../../docs/framework/install/troubleshoot-blocked-installations-and-uninstallations.md)
