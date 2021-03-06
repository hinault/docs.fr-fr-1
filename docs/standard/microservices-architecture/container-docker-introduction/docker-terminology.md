---
title: Terminologie de docker
description: Architecture de Microservices .NET pour les Applications .NET en conteneur | Terminologie de docker
keywords: Docker, microservices, ASP.NET, conteneur
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.openlocfilehash: 885b1fbd3369dec54ebde21a5378630c764f852d
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="docker-terminology"></a>Terminologie de docker

Cette section répertorie les termes et définitions, que vous devez connaître avant d’obtenir le plus profond dans Docker. Pour les autres définitions, consultez l’étendue [glossaire](https://docs.docker.com/v1.11/engine/reference/glossary/) fournie par Docker.

**Image de conteneur**: un package avec toutes les dépendances et les informations nécessaires pour créer un conteneur. Une image inclut toutes les dépendances (par exemple, des infrastructures) ainsi que de la configuration de déploiement et d’exécution à utiliser par un conteneur d’exécution. En règle générale, une image est dérivée de plusieurs images de base sont empilées les unes sur les autres pour former le système de fichiers du conteneur de couches. Une image est immuable une fois qu’elle a été créée.

**Conteneur**: une instance d’une image Docker. Un conteneur représente l’exécution d’une application unique, un processus ou un service. Il se compose du contenu d’une image Docker, un environnement d’exécution et un ensemble standard d’instructions. Lors de la mise à l’échelle un service, vous créez plusieurs instances d’un conteneur à partir de la même image. Ou un traitement par lots peut créer plusieurs conteneurs à partir de la même image, en passant des paramètres différents pour chaque instance.

**Balise**: une marque ou une étiquette, vous pouvez appliquer aux images afin que des images ou des versions de la même image (selon le numéro de version ou de l’environnement cible) peuvent être identifiées.

**Fichier Dockerfile**: un fichier texte qui contient des instructions pour la création d’une image Docker.

**Build**: l’action de création d’une image de conteneur en fonction des informations et du contexte fourni par son fichier Dockerfile, ainsi que des fichiers supplémentaires dans le dossier où l’image est créée. Vous pouvez créer des images avec la commande de génération docker Docker.

**Référentiel (référentiel)**: une collection d’images Docker connexes, identifié par une balise qui indique la version de l’image. Certains référentiels contiennent plusieurs variantes d’une image spécifique, par exemple une image contenant des kits de développement logiciel (plus), une image contenant des runtimes uniquement (le plus claires), un etc.. Ces variantes peuvent être marqués avec des balises. Un référentiel unique peut contenir des variantes de plateforme, par exemple une image Linux et une image système Windows.

**Registre**: un service qui fournit l’accès à des référentiels. Le Registre par défaut pour les images plus publics est [Hub d’ancrage](https://hub.docker.com/) (appartenant à Docker en tant qu’organisation). Un Registre contient généralement des référentiels à partir de plusieurs équipes. Les entreprises ont souvent des registres privés pour stocker et gérer des images, qu'ils ont créées. Registre de conteneur Azure est un autre exemple.

**Hub d’ancrage**: un registre public pour le téléchargement d’images et de les manipuler. Hub d’ancrage fournit Docker hébergement, registres publics ou privés, les déclencheurs de build et les raccordements web et l’intégration avec GitHub et Bitbucket.

**Registre de conteneur Azure**: une ressource publique pour travailler avec les images Docker et ses composants dans Azure. Cela fournit un Registre qui est proche de vos déploiements dans Azure et qui vous donne le contrôle sur l’accès, ce qui permet d’utiliser vos groupes Azure Active Directory et les autorisations.

**Docker Trusted Registre DTR ()**: service de Registre A Docker (à partir de Docker) qui peut être installé sur site afin qu’il se trouve dans le centre de données et le réseau de l’organisation. Il est pratique pour les images privées qui doivent être gérés au sein de l’entreprise. Registre de confiance docker est inclus dans le cadre du produit Docker de centre de données. Pour plus d’informations, consultez [Docker Trusted Registre DTR ()](https://docs.docker.com/docker-trusted-registry/overview/).

**Docker Community Edition (CE)**: outils de développement pour Windows et macOS pour générer, en cours d’exécution et tester localement des conteneurs. CE de docker pour Windows fournit des environnements de développement pour les conteneurs Linux et Windows. L’hôte Linux Docker sur Windows est basée sur un [Hyper-V](https://www.microsoft.com/en-us/server-cloud/solutions/virtualization.aspx) machine virtuelle. L’ordinateur hôte pour les conteneurs Windows est directement basé sur Windows. Docker CE pour Mac est basée sur l’infrastructure de l’hyperviseur d’Apple et le [xhyve hyperviseur](https://github.com/mist64/xhyve), qui fournit un ordinateur virtuel de hôte Linux Docker sur Mac OS X. Docker CE pour Windows et Mac remplace boîte à outils Docker, qui était basé sur Oracle VirtualBox.

**Docker Enterprise Edition (EE)**: une version de l’entreprise à l’échelle des outils de Docker pour le développement Linux et Windows.

**Composer**: un outil de ligne de commande et les YAML file format avec les métadonnées pour la définition et le conteneur de plusieurs applications en cours d’exécution. Vous définissez une application unique en fonction de plusieurs images avec un ou plusieurs fichiers .yml qui peuvent remplacer les valeurs en fonction de l’environnement. Après avoir créé les définitions, vous pouvez déployer l’application entière multi conteneur avec une seule commande (docker-composer des) qui crée un conteneur par image sur l’hôte Docker.

**Cluster**: une collection d’hôtes Docker exposé comme s’il s’agissait d’un seul hôte Docker virtuel, afin que l’application peut s’adapter à plusieurs instances des services répartis sur plusieurs hôtes au sein du cluster. Clusters de docker peuvent être créés avec Docker Swarm mésosphère DC/OS, Kubernetes et Azure Service Fabric. (Si vous utilisez la commande Docker Swarm pour la gestion d’un cluster, en général, reportez-vous au cluster en tant qu’un *swarm* au lieu d’un cluster.)

**Orchestrator**: un outil qui simplifie la gestion de clusters et hôtes de Docker. Orchestrators vous autorise à gérer leurs images, les conteneurs et les ordinateurs hôtes via une interface de ligne de commande (CLI) ou une interface utilisateur graphique. Vous pouvez gérer la mise en réseau de conteneur, configurations, l’équilibrage de charge, découverte des services, haute disponibilité, configuration de l’hôte Docker et bien plus encore. Orchestrateur est chargé d’en cours d’exécution, la distribution, la mise à l’échelle et la réparation des charges de travail sur une collection de nœuds. En règle générale, orchestrator produits sont les mêmes qui fournissent l’infrastructure de cluster, comme contrôleur de domaine/système d’exploitation de mésosphère, Kubernetes, Docker Swarm et Azure Service Fabric.


>[!div class="step-by-step"]
[Précédente] (docker-defined.md) [suivant] (docker-conteneurs-images-registries.md)
