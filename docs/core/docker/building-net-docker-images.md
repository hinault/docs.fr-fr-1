---
title: "Création d’images Docker .NET Core"
description: "Présentation des images Docker et de .NET Core"
keywords: .NET, .NET Core, Docker
author: jralexander
ms.author: johalex
ms.date: 11/06/2017
ms.topic: tutorial
ms.prod: .net-core
ms.technology: dotnet-docker
ms.devlang: dotnet
ms.assetid: 03c28597-7e73-46d6-a9c3-f9cb55642739
ms.custom: mvc
manager: wpickett
ms.workload:
- dotnetcore
ms.openlocfilehash: 2b1a57fe264eda0a4d3186c7be8b0de01bd5f0a9
ms.sourcegitcommit: c1904b0437605a90e5aa65b4abd7e048000e349d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2018
---
# <a name="building-docker-images-for-net-core-applications"></a>Création d’images Docker pour les applications .NET Core

 Dans ce didacticiel, nous nous concentrons sur l’utilisation de .NET Core sur Docker. Tout d’abord, nous explorons les différentes images Docker proposées et gérées par Microsoft, ainsi que les cas d’usage. Nous découvrons ensuite comment générer et dockeriser une application ASP.NET Core.

Au cours de ce didacticiel, vous apprenez à :
> [!div class="checklist"]
> * Découvrir les images Docker Microsoft .NET Core 
> * Obtenir un exemple d’application ASP.NET Core à dockeriser
> * Exécuter l’exemple d’application ASP.NET localement
> * Générer et exécuter l’exemple avec Docker pour des conteneurs Linux
> * Générer et exécuter l’exemple avec Docker pour des conteneurs Windows

## <a name="docker-image-optimizations"></a>Optimisations des images Docker

Lors de la création d’images Docker pour les développeurs, nous nous sommes concentrés sur trois scénarios principaux :

* Images utilisées pour développer des applications .NET Core
* Images utilisées pour générer des applications .NET Core
* Images utilisées pour exécuter des applications .NET Core

Pourquoi trois images ?
Lors du développement, de la génération et de l’exécution d’applications en conteneur, nous avons des priorités différentes.

* **Développement :** la priorité porte sur la rapidité avec laquelle vous pouvez apporter des modifications de façon itérative, et la possibilité de déboguer les modifications. La taille de l’image est moins importante que la possibilité d’apporter des modifications à votre code et de les voir rapidement.

* **Génération :** cette image contient tous les éléments nécessaires pour compiler votre application, ce qui inclut le compilateur et toutes les autres dépendances pour optimiser les fichiers binaires.  L’image de build vous permet de créer les ressources que vous placez dans une image de production. Cette image est destinée à être utilisée dans une intégration continue ou dans un environnement de génération. Cette approche permet à un agent de build de compiler et générer l’application (avec toutes les dépendances requises) dans une instance d’image de build. L’agent de build doit seulement savoir comment exécuter cette image Docker.

* **Production :** la rapidité avec laquelle vous pouvez déployer et démarrer votre image. Comme cette image est de petite taille, les performances réseau entre votre Registre Docker et vos hôtes Docker sont optimisées. Le contenu est prêt à s’exécuter, ce qui permet d’obtenir le temps le plus court entre l’exécution Docker et les résultats du traitement. La compilation de code dynamique n’est pas nécessaire dans le modèle Docker. Le contenu que vous placez dans cette image est limité aux fichiers binaires et au contenu nécessaires pour exécuter l’application.

    Par exemple, la sortie `dotnet publish` contient :

    * les fichiers binaires compilés
    * les fichiers .js et .css


Il est utile d’inclure la sortie de la commande `dotnet publish` dans votre image de production si vous voulez conserver sa taille au minimum.

Certaines images .NET Core partagent des couches entre différentes balises pour que le téléchargement de la dernière balise soit un processus relativement simple. Si vous avez déjà une version antérieure sur votre ordinateur, cette architecture diminue l’espace disque nécessaire.

Quand plusieurs applications utilisent des images communes sur le même ordinateur, la mémoire est partagée entre ces images. Les images doivent être identiques pour être partagées.

## <a name="docker-image-variations"></a>Variantes des images Docker

Pour atteindre les objectifs ci-dessus, nous fournissons des variantes d’images sous [`microsoft/dotnet`](https://hub.docker.com/r/microsoft/dotnet/).

* `microsoft/dotnet:<version>-sdk`(`microsoft/dotnet:2.0.0-sdk`) Cette image contient le kit SDK .NET Core, qui inclut .NET Core et les outils en ligne de commande. Cette image est adaptée au **scénario de développement**. Vous utilisez cette image pour le développement local, le débogage et les tests unitaires. Cette image peut également être utilisée pour vos scénarios de **génération**. L’utilisation de `microsoft/dotnet:sdk` vous donne toujours la version la plus récente.

> [!TIP]
> Si vous ne savez pas de quoi vous avez besoin, vous pouvez utiliser l’image `microsoft/dotnet:<version>-sdk`. En tant qu’image « de facto », elle est conçue pour être utilisée comme conteneur jetable (montez votre code source et démarrez le conteneur pour démarrer votre application) et comme image de base à partir de laquelle générer d’autres images.

* `microsoft/dotnet:<version>-runtime` : cette image contient .NET Core (runtime et bibliothèques) et est optimisée pour l’exécution des applications .NET Core en **production**.

## <a name="alternative-images"></a>Images alternatives

En plus des scénarios de développement, de génération et de production optimisés, nous fournissons des images supplémentaires :

* `microsoft/dotnet:<version>-runtime-deps` : l’image **runtime-deps** contient le système d’exploitation avec toutes les dépendances natives nécessaires à .NET Core. Cette image est destinée aux [applications autonomes](https://docs.microsoft.com/dotnet/core/deploying/index).

Versions les plus récentes de chaque variante :

* `microsoft/dotnet` ou `microsoft/dotnet:latest` (alias pour l’image du kit SDK)
* `microsoft/dotnet:sdk`
* `microsoft/dotnet:runtime`
* `microsoft/dotnet:runtime-deps`

## <a name="samples-to-explore"></a>Exemples à explorer

* [Cet exemple d’ASP.NET Core Docker](https://github.com/dotnet/dotnet-docker-samples/tree/master/aspnetapp) montre un modèle des meilleures pratiques pour la création d’images Docker pour les applications ASP.NET Core pour la production. L’exemple s’applique aux conteneurs Linux et Windows.

* Cet exemple de Docker .NET Core montre un modèle des meilleures pratiques pour la [création d’images Docker pour les applications .NET Core pour la production.](https://github.com/dotnet/dotnet-docker-samples/tree/master/dotnetapp-prod)

## <a name="your-first-aspnet-core-docker-app"></a>Votre première application Docker ASP.NET Core

Pour ce didacticiel, utilisons un exemple d’application Docker ASP.NET Core pour l’application à dockeriser. Cet exemple d’application Docker ASP.NET Core montre un modèle de bonnes pratiques de création d’images Docker pour les applications ASP.NET Core destinées à la production. L’exemple s’applique aux conteneurs Linux et Windows.

L’exemple de fichier Dockerfile crée une image Docker d’application ASP.NET Core basée sur l’image de base Docker de runtime ASP.NET Core.

Il utilise la [fonctionnalité de build en plusieurs étapes Docker](https://docs.docker.com/engine/userguide/eng-image/multistage-build/) pour :

* Générer l’exemple dans un conteneur selon l’image de base Docker de build ASP.NET Core **la plus grande** 
* Copier le résultat de la build finale dans une image Docker basée sur l’image de base Docker de runtime ASP.NET Core **la plus petite**

> [!NOTE]
> L’image de build contient les outils requis pour créer des applications, contrairement à l’image de runtime.

### <a name="prerequisites"></a>Prérequis

Pour générer et exécuter, installez les éléments suivants :

#### <a name="net-core-20-sdk"></a>Kit SDK .NET Core 2.0

* Installez le [Kit SDK .NET Core 2.0](https://www.microsoft.com/net/core).

* Installez votre éditeur de code favori, si ce n’est pas déjà fait.

> [!TIP]
> Vous avez besoin d’installer un éditeur de code ? Essayez [Visual Studio](https://visualstudio.com/downloads) !

#### <a name="installing-docker-client"></a>Installation du client Docker

Installez la version [Docker 17.06](https://docs.docker.com/release-notes/docker-ce/) ou ultérieure du client Docker.

Le client Docker peut être installé dans :

* Distributions Linux

   * [CentOS](https://www.docker.com/docker-centos-distribution)

   * [Debian](https://www.docker.com/docker-debian)

   * [Fedora](https://www.docker.com/docker-fedora)

   * [Ubuntu](https://www.docker.com/docker-ubuntu)

* [macOS](https://docs.docker.com/docker-for-mac/)

* [Windows](https://docs.docker.com/docker-for-windows/).

#### <a name="installing-git-for-sample-repository"></a>Installation de Git pour un dépôt d’exemples

* Installez [git](https://git-scm.com/download) si vous souhaitez cloner le dépôt.

### <a name="getting-the-sample-application"></a>Obtention de l’exemple d’application

La façon la plus simple d’obtenir l’exemple consiste à cloner le [dépôt d’exemples](https://github.com/dotnet/dotnet-docker-samples) avec git, en utilisant les instructions suivantes : 

```console
git clone https://github.com/dotnet/dotnet-docker-samples/
```

Vous pouvez également télécharger le dépôt (qui est petit) comme un fichier zip à partir du dépôt d’exemples Docker .NET Core.

### <a name="run-the-aspnet-app-locally"></a>Exécuter l’application ASP.NET localement

Pour établir un point de référence, avant de mettre l’application dans un conteneur, exécutez l’application localement.

Vous pouvez générer et exécuter l’application localement avec le kit SDK .NET Core 2.0 à l’aide des commandes suivantes (les instructions supposent la racine du dépôt) :

```console
cd aspnetapp
dotnet run
```

Une fois que l’application démarre, accédez à **http://localhost:5000** dans votre navigateur web.

### <a name="build-and-run-the-sample-with-docker-for-linux-containers"></a>Générer et exécuter l’exemple avec Docker pour des conteneurs Linux

Vous pouvez générer et exécuter l’exemple dans Docker avec des conteneurs Linux à l’aide des commandes suivantes (les instructions supposent la racine du dépôt) :

```console
cd aspnetapp
docker build -t aspnetapp .
docker run -it --rm -p 5000:80 --name aspnetcore_sample aspnetapp
```

> [!NOTE]
> L’argument `docker run` '-p' mappe le port 5000 sur votre ordinateur local au port 80 dans le conteneur (la forme de mappage de port est `host:container`). Pour plus d’informations, consultez la référence [docker run](https://docs.docker.com/engine/reference/commandline/exec/) dans les paramètres de ligne de commande.

Une fois que l’application démarre, accédez à **http://localhost:5000** dans votre navigateur web.

### <a name="build-and-run-the-sample-with-docker-for-windows-containers"></a>Générer et exécuter l’exemple avec Docker pour des conteneurs Windows

Vous pouvez générer et exécuter l’exemple dans Docker avec des conteneurs Windows à l’aide des commandes suivantes (les instructions supposent la racine du dépôt) :

```console
cd aspnetapp
docker build -t aspnetapp .
docker run -it --rm --name aspnetcore_sample aspnetapp
```

> [!IMPORTANT]
> Vous devez accéder directement à **l’adresse IP de conteneur** (par opposition à http://localhost) dans votre navigateur lors de l’utilisation de conteneurs Windows. Vous pouvez obtenir l’adresse IP de votre conteneur en effectuant les étapes suivantes :

* Ouvrez une autre invite de commandes.
* Exécutez `docker ps` pour voir vos conteneurs en cours d’exécution. Le conteneur « aspnetcore_sample » doit être visible.
* Exécutez `docker exec aspnetcore_sample ipconfig`.
* Copiez l’adresse IP de conteneur et collez-la dans votre navigateur (par exemple, 172.29.245.43).

> [!NOTE]
> Docker exec prend en charge l’identification des conteneurs avec le nom ou le hachage. Dans notre exemple, le nom (aspnetcore_sample) est utilisé.

Consultez l’exemple suivant illustrant comment obtenir l’adresse IP d’un conteneur Windows en cours d’exécution.

```console
docker exec aspnetcore_sample ipconfig

Windows IP Configuration

Ethernet adapter Ethernet:

   Connection-specific DNS Suffix  . : contoso.com
   Link-local IPv6 Address . . . . . : fe80::1967:6598:124:cfa3%4
   IPv4 Address. . . . . . . . . . . : 172.29.245.43
   Subnet Mask . . . . . . . . . . . : 255.255.240.0
   Default Gateway . . . . . . . . . : 172.29.240.1
```

> [!NOTE]
> Docker exec exécute une nouvelle commande dans un conteneur en cours d’exécution. Pour plus d’informations, consultez la [référence docker exec](https://docs.docker.com/engine/reference/commandline/exec/) dans les paramètres de ligne de commande.

Vous pouvez générer une application qui est prête à être déployée en production localement à l’aide de la commande [dotnet publish](../tools/dotnet-publish.md).

```console
dotnet publish -c release -o published
```

> [!NOTE]
> L’argument -c release génère l’application en mode mise en production (la valeur par défaut est le mode débogage). Pour plus d’informations, consultez la [référence dotnet run](../tools/dotnet-run.md) dans les paramètres de ligne de commande.

Vous pouvez exécuter l’application sur **Windows** à l’aide de la commande suivante.

```console
dotnet published\aspnetapp.dll
```

Vous pouvez exécuter l’application sur **Linux** ou **macOS** à l’aide de la commande suivante.

```bash
dotnet published/aspnetapp.dll
```

### <a name="docker-images-used-in-this-sample"></a>Images Docker utilisées dans cet exemple

Les images Docker suivantes sont utilisées dans cet exemple

* `microsoft/aspnetcore-build:2.0`
* `microsoft/aspnetcore:2.0`

Félicitations ! Vous venez de :
> [!div class="checklist"]
> * Découvrir les images Docker Microsoft .NET Core
> * Obtenir un exemple d’application ASP.NET Core à dockeriser
> * Exécuter l’exemple d’application ASP.NET localement
> * Générer et exécuter l’exemple avec Docker pour des conteneurs Linux
> * Générer et exécuter l’exemple avec Docker pour des conteneurs Windows


**Étapes suivantes**

Voici quelques étapes suivantes que vous pouvez effectuer :

* [Utilisation des outils Docker dans Visual Studio](https://docs.microsoft.com/aspnet/core/publishing/visual-studio-tools-for-docker)
* [Déploiement d’images Docker à partir du Registre de conteneurs Azure dans Azure Container Instances](https://blogs.msdn.microsoft.com/stevelasker/2017/07/28/deploying-docker-images-from-the-azure-container-registry-to-azure-container-instances/)
* [Débogage avec Visual Studio Code](https://code.visualstudio.com/docs/nodejs/debugging-recipes#_nodejs-typescript-docker-container) 
* [Prise en main de Visual Studio pour Mac, les conteneurs et le code serverless dans le cloud](https://blogs.msdn.microsoft.com/visualstudio/2017/08/31/hands-on-with-visual-studio-for-mac-containers-serverless-code-in-the-cloud/#comments)
* [Bien démarrer avec Docker et Visual Studio pour Mac Lab](https://github.com/Microsoft/vs4mac-labs/tree/master/Docker/Getting-Started)

> [!NOTE]
> Si vous ne disposez pas d’abonnement Azure, [inscrivez-vous dès aujourd'hui](https://azure.microsoft.com/free/?b=16.48) pour obtenir un compte gratuit pendant 30 jours et 200 dollars US en crédits Azure pour essayer une combinaison quelconque de services Azure.
