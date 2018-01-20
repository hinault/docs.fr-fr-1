---
title: "Qu’est Docker ?"
description: "Architecture de Microservices .NET pour les Applications .NET en conteneur | Qu’est Docker ?"
keywords: Docker, microservices, ASP.NET, conteneur
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.openlocfilehash: aa9cb379628fa91e5dc5b1b529f92db98fa59305
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="what-is-docker"></a>Qu’est Docker ?

[Docker](https://www.docker.com/) est un [projet open source](https://github.com/docker/docker) pour automatiser le déploiement d’applications en tant que conteneurs portables et autonomes qui peuvent s’exécuter sur le cloud ou localement. Docker est également une [société](https://www.docker.com/) qui promeut et fait évoluer cette technologie. Docker fonctionne en collaboration avec le cloud, Linux et les fournisseurs de Windows, notamment Microsoft.

![](./media/image2.png)

**Figure 2-2**. Docker déploie des conteneurs à toutes les couches du cloud hybride

Docker image conteneurs sont exécutés en mode natif sur Linux et Windows. Les images Windows s’exécutent uniquement sur des hôtes Windows et Linux images s’exécutent uniquement sur les hôtes Linux. L’hôte est un serveur ou une machine virtuelle.

Vous pouvez développer sur Windows, Linux ou macOS. L’ordinateur de développement s’exécute à un hôte Docker où les images Docker sont déployés, y compris l’application et ses dépendances. Sur Linux ou macOS, vous utilisez un hôte Docker est Linux peut créer des images uniquement pour les conteneurs Linux. (Sur Mac OS, vous pouvez modifier le code ou exécuter l’interface CLI de Docker, mais au moment de la rédaction, conteneurs ne s’exécutent pas directement sur macOS.) Sur Windows, vous pouvez créer des images pour les conteneurs Windows ou Linux.

Sur Windows ou macOS, [Docker Community Edition (CE)](https://www.docker.com/community-edition) héberge des conteneurs dans un environnement de développement et fournit des outils de développement supplémentaires. [Docker Enterprise Edition (EE)](https://www.docker.com/enterprise-edition) est utilisé par les équipes informatiques générer, sont fournis et exécutent des applications critiques volumineuses. ~ Les deux produits installent VM nécessaire (hôte Docker) pour héberger les conteneurs. ~ 

[Les conteneurs Windows](https://msdn.microsoft.com/en-us/virtualization/windowscontainers/about/about_overview) fonctionnent avec les deux types de runtime :

-   Les conteneurs Windows Server fournissent l’isolation des applications via une technologie d’isolation des processus et l’espace de noms. Un conteneur Windows Server partage un noyau avec l’hôte de conteneur et tous les conteneurs en cours d’exécution sur l’ordinateur hôte.

-   Conteneurs Hyper-V développent l’isolation fournie par les conteneurs Windows Server en exécutant chaque conteneur dans une machine virtuelle hautement optimisée. Dans cette configuration, le noyau de l’hôte de conteneur n’est pas partagé avec les conteneurs Hyper-V, qui fournit une meilleure isolation. Autoriser les conteneurs Hyper-V non approuvés et *mutualisée hostile* applications à s’exécuter sur le même hôte. Conteneurs Hyper-V ont un peu moins efficacité dans les temps de démarrage et la densité de conteneurs Windows Server.

Les images de ces conteneurs sont créés et fonctionnent de la même façon. Elles diffèrent dans la manière dont le conteneur est créé. Pour plus d’informations, consultez [conteneurs Hyper-V](https://msdn.microsoft.com/en-us/virtualization/windowscontainers/about/about_overview).

## <a name="comparing-docker-containers-with-virtual-machines"></a>Comparaison des conteneurs Docker avec des machines virtuelles

Figure 2-3 indique une comparaison entre les machines virtuelles et Docker conteneurs.

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Machines virtuelles****conteneurs Docker** 
                                                                                                                                                                                        
  ![](./media/image3.png)                                                                                                                                ![](./media/image4.png)
                                                                                                                                                                                        
  Machines virtuelles incluent le système d’exploitation invité complète ou binaires, l’application et les bibliothèques requises. Virtualisation complète nécessite plus de ressources que la CONTENEURISATION des données. Les conteneurs incluent l’application et toutes ses dépendances. Toutefois, les conteneurs partagent le noyau du système d’exploitation avec d’autres conteneurs. Conteneurs sont exécutés en tant que processus isolés dans l’espace de l’utilisateur sur le système d’exploitation hôte. Sauf dans les conteneurs Hyper-V, où chaque conteneur s’exécute à l’intérieur d’un ordinateur virtuel spécial par conteneur.
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Figure 2-3**. Comparaison des machines virtuelles traditionnelles dans des conteneurs Docker

Étant donné que les conteneurs nécessitent beaucoup moins de ressources (par exemple, il est inutile un système d’exploitation complet), démarrage rapide et sont faciles à déployer. Faible utilisation des ressources permet une densité plus élevée. Vous pouvez exécuter les services plus sur la même unité de matériel et réduire les coûts.

En cours d’exécution sur les mêmes résultats noyau dans moins d’isolation présentent de machines virtuelles.

L’objectif principal d’une image est qu’elle rend l’environnement (dépendances) identiques entre les différents déploiements. Cela signifie que vous pouvez déboguer sur votre ordinateur et puis le déployer sur un autre ordinateur avec le même environnement garanti.

Une image de conteneur est un moyen pour empaqueter une application ou un service et le déployer de manière fiable et reproductible. Vous pouvez dire que Docker est non seulement une technologie, mais également une philosophie et un processus.

Les développeurs de docker ne dites, « Il fonctionne sur mon ordinateur, pourquoi ne pas en production ? » Ils affirment, « Il s’exécute sur Docker ». Les applications empaquetées de docker peuvent être exécutées sur n’importe quel environnement Docker pris en charge. Docker empaquetées des applications de s’exécuter de façon cohérente sur toutes les cibles de déploiement (développement, assurance qualité, de mise en lots, production).

>[!div class="step-by-step"]
[Précédente] (index.md) [suivant] (docker-terminology.md)
