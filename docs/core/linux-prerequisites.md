---
title: "Prérequis pour .NET Core sur Linux"
description: "Versions Linux et dépendances .NET Core prises en charge pour développer, déployer et exécuter des applications .NET Core sur des ordinateurs Linux."
keywords: .NET, .NET Core, Linux, debian, ubuntu, RHEL, centOS,
author: jralexander
ms.author: johalex
ms.date: 12/06/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: c33b1241-ab66-4583-9eba-52cf51146f5a
ms.workload: dotnetcore
ms.openlocfilehash: d3c5dde443f848831f7c0585633339c35213357b
ms.sourcegitcommit: 8bde7a3432f30fc771079744955c75c58c4eb393
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/20/2018
---
# <a name="prerequisites-for-net-core-on-linux"></a>Prérequis pour .NET Core sur Linux

Cet article montre les dépendances nécessaires pour développer des applications .NET Core sur Linux. Les distributions/versions Linux et les dépendances prises en charge ci-après s’appliquent aux deux façons de développer des applications .NET Core sur Linux :

* [Ligne de commande avec votre éditeur favori](tutorials/using-with-xplat-cli.md)
* [Visual Studio Code](https://code.visualstudio.com/)

## <a name="supported-linux-versions"></a>Versions de Linux prises en charge

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

.NET Core 2.0 traite Linux comme un seul système d’exploitation. Il existe une seule version Linux (par architecture de puce) pour les distributions Linux prises en charge.

NET Core 2.x est pris en charge sur les distributions/versions Linux 64 bits suivantes (`x86_64` ou `amd64`) :

 * Red Hat Enterprise Linux 7
 * CentOS 7
 * Oracle Linux 7
 * Fedora 25, Fedora 26
 * Debian 8.7 ou versions ultérieures 
 * Ubuntu 17.04, Ubuntu 16.04, Ubuntu 14.04
 * Linux Mint 18, Linux Mint 17
 * openSUSE 42.2 ou versions ultérieures
 * SUSE Enterprise Linux (SLES) 12 SP2 ou versions ultérieures

Consultez [.NET Core 2.x - Versions des systèmes d’exploitation prises en charge](https://github.com/dotnet/core/blob/master/release-notes/2.0/2.0-supported-os.md) pour obtenir la liste complète des systèmes d’exploitation pris en charge par .NET Core 2.x, les systèmes d’exploitation non pris en charge et des liens sur la politique concernant le cycle de vie.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

.NET Core 1.x est pris en charge sur les distributions/versions Linux 64 bits suivantes (`x86_64` ou `amd64`) :

* Red Hat Enterprise Linux 7
* CentOS 7
* Oracle Linux 7
* Fedora 24
* Debian 8.2 ou versions ultérieures
* Ubuntu 14.04, Ubuntu 16.04, Ubuntu 16.10\*
 * Ubuntu 16.10 est pris en charge par la dernière version de correctif logiciel de .NET Core 1.1
* Linux Mint 17
* openSUSE 42.1 ou versions ultérieures (.NET Core 1.1)

Consultez [.NET Core 1.x - Versions des systèmes d’exploitation prises en charge](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0-supported-os.md) pour obtenir la liste complète des systèmes d’exploitation pris en charge par .NET Core 1.x, les systèmes d’exploitation non pris en charge et des liens sur la politique concernant le cycle de vie.

---

## <a name="linux-distribution-dependencies"></a>Dépendances des distributions Linux

Les éléments suivants sont destinés à être des exemples. Les versions et les noms exacts peuvent varier légèrement sur la distribution Linux que vous choisissez.

### <a name="ubuntu"></a>Ubuntu

Les distributions Ubuntu nécessitent l’installation des bibliothèques suivantes :

* libunwind8
* liblttng-ust0
* libcurl3
* libssl1.0.0
* libuuid1
* libkrb5-3
* zlib1g
* libicu52 (pour 14.X)
* libicu55 (pour 16.X)
* libicu57 (pour 17.X)

### <a name="centos"></a>CentOS

Les distributions CentOS nécessitent l’installation des bibliothèques suivantes :

* libunwind
* lttng-ust
* libcurl
* openssl-libs
* libuuid
* krb5-libs
* libicu
* zlib

Pour plus d’informations sur les dépendances, consultez [Applications Linux autonomes](https://github.com/dotnet/core/blob/master/Documentation/self-contained-linux-apps.md) (en anglais).

## <a name="installing-net-core-dependencies-with-the-native-installers"></a>Installation des dépendances .NET Core avec les programmes d’installation natifs

Les programmes d’installation natifs .NET Core sont disponibles pour les distributions/versions Linux prises en charge. Les programmes d’installation natifs requièrent un accès administrateur (sudo) au serveur. L’avantage d’utiliser un programme d’installation natif est que toutes les dépendances natives .NET Core sont installées. En outre, les programmes d’installation natifs installent le SDK .NET Core à l’échelle du système.

Sur Linux, il existe deux choix pour le package de programme d’installation :

* Utilisation d’un gestionnaire de package basé sur le flux, tel qu’apt-get pour Ubuntu, ou yum pour CentOS/RHEL.
* Utilisation des packages eux-mêmes, DEB ou RPM

### <a name="scripting-installs-with-the-net-core-installer-script"></a>Script d’installation avec le script de programme d’installation de .NET Core

Les scripts `dotnet-install` sont utilisés pour effectuer une installation non administrateur de la chaîne d’outils CLI et du runtime partagé. Vous pouvez télécharger le script à partir de : https://dot.net/v1/dotnet-install.sh

Le script bash du programme d’installation est utilisé dans les scénarios d’automatisation et dans les installations non administratives. Comme ce script lit également les commutateurs PowerShell, ces derniers peuvent être utilisés avec le script sur les systèmes Linux/OS X.

> [!IMPORTANT]
> Avant d’exécuter le script, installez les [dépendances](https://github.com/dotnet/core/blob/master/Documentation/prereqs.md) nécessaires.

## <a name="install-net-core-for-red-hat-enterprise-linux-rhel-7"></a>Installer .NET Core pour Red Hat Enterprise Linux (RHEL) 7

Pour installer .NET Core sur RHEL 7 :

1. Activez le canal Red Hat .NET, disponible dans votre abonnement RHEL 7.
    * Pour Red Hat Enterprise Server 7, utilisez :
    
         ```bash
         subscription-manager repos --enable=rhel-7-server-dotnet-rpms
         ```
    
    * Pour Red Hat Enterprise 7 Workstation, utilisez :
    
        ```bash
        subscription-manager repos --enable=rhel-7-workstation-dotnet-rpms
         ```
    
    * Pour Red Hat Enterprise 7 HPC Compute Node, utilisez :
    
        ```bash
        subscription-manager repos --enable=rhel-7-hpc-node-dotnet-rpms
        ```

2. Installez l’outil scl.

    ```bash
    yum install scl-utils
    ```
    
3. Installer .NET Core

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

Installez le runtime et le kit SDK .NET Core 2.0 :

   ```bash
   yum install rh-dotnet20
   ```

Activez le runtime/kit SDK .NET Core 2.0 pour votre environnement :

   ```bash
   scl enable rh-dotnet20 bash
   ```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

**.NET Core 1.1**

Installez le runtime et le kit SDK .NET Core 1.1 :

   ```bash
   yum install rh-dotnetcore11
   ```

Activez le runtime et le kit SDK .NET Core 1.1 pour votre environnement :

   ```bash
   scl enable rh-dotnetcore11 bash
   ```

**.NET Core 1.0**

Installez le runtime et le kit SDK .NET Core 1.0 :

   ```bash
   yum install rh-dotnetcore10
   ```

Activez le runtime et le kit SDK .NET Core 1.0 pour votre environnement :

   ```bash
   scl enable rh-dotnetcore10 bash
   ```

---
4. Exécutez la commande `dotnet --version` pour vérifier que l’installation a réussi.

     ```bash
     dotnet --version
     ```

Pour obtenir de l’aide sur l’inscription à l’accès au canal Red Hat .NET, consultez le [chapitre 1 du guide de prise en main de .NET Core 1.1](https://access.redhat.com/documentation/en/net-core/1.1/paged/getting-started-guide/) sur Red Hat.

## <a name="install-net-core-for-ubuntu-1404-ubuntu-1604-ubuntu-1610--linux-mint-17-linux-mint-18-64-bit"></a>Installer .NET Core pour Ubuntu 14.04, Ubuntu 16.04, Ubuntu 16.10, Linux Mint 17 et Linux Mint 18 (64 bits)

1. Supprimez du système toute **version antérieure** de .NET Core.

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

2. Enregistrez la clé de produit Microsoft approuvée.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
   sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
   ```

3. Configurez le flux de package hôte de version souhaité.

   **Ubuntu 17.10**

   ```bash
   sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-artful-prod artful main" > /etc/apt/sources.list.d/dotnetdev.list'
   sudo apt-get update
   ```
   **Ubuntu 17.04**

   ```bash
   sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-zesty-prod zesty main" > /etc/apt/sources.list.d/dotnetdev.list'
   sudo apt-get update
   ```

   **Ubuntu 16.04 / Linux Mint 18**

   ```bash
   sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-xenial-prod xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
   sudo apt-get update
   ```

   **Ubuntu 14.04 / Linux Mint 17**

   ```bash
   sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-trusty-prod trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
   sudo apt-get update
   ```

4. Installez .NET Core.

   ```bash
   sudo apt-get install dotnet-sdk-2.1.3
   ```

4. Exécutez la commande `dotnet --version` pour vérifier que l’installation a réussi.

   ```bash
   dotnet --version
   ```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

2. Configurez le flux de package hôte de version souhaité.

   **Ubuntu 16.10**
   
   ```bash
   sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ yakkety main" > /etc/apt/sources.list.d/dotnetdev.list'
   sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys B02C46DF417A0893
   sudo apt-get update
   ```

  **Ubuntu 16.04 / Linux Mint 18**

   ```bash
   sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
   sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys B02C46DF417A0893
   sudo apt-get update
   ```
    
   **Ubuntu 14.04 / Linux Mint 17**

   ```bash
   sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
   sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys B02C46DF417A0893
   sudo apt-get update
   ```

3. Installez .NET Core 1.x sur Ubuntu ou Linux Mint :

   ```bash
   sudo apt-get install dotnet-dev-1.0.4
   ```

4. Exécutez la commande `dotnet --version` pour vérifier que l’installation a réussi.

   ```bash
   dotnet --version
   ```

---

 ## <a name="install-net-core-for-debian-8-or-debian-9-64-bit"></a>Installer .NET Core pour Debian 8 ou Debian 9 (64 bits)

Pour installer .NET Core sur Debian 8 ou Debian 9 (64 bits) :

1. Supprimez du système toute **version antérieure** de .NET Core.

> [!NOTE]
> Un répertoire contrôlé par l’utilisateur est requis pour les installations du système Linux système depuis tar.gz.

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

2. Installez les composants du système.

   ```bash
   sudo apt-get update
   sudo apt-get install curl libunwind8 gettext apt-transport-https
   ```
   
3. Enregistrez la clé de produit Microsoft approuvée.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
   sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
   ```
   
4. Enregistrez le flux de produit Microsoft approuvé.

   **Debian 9 (Stretch)**

   ```bash
   sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" > /etc/apt/sources.list.d/dotnetdev.list'
   ```
   
   **Debian 8 (Jessie)**
   
   ```bash
   sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-jessie-prod jessie main" > /etc/apt/sources.list.d/dotnetdev.list'
   ```
   
5. Installez le SDK .NET Core.

   ```bash
   sudo apt-get update
   sudo apt-get install dotnet-sdk-2.0.0
   ```

6. Ajoutez dotnet au chemin.

   ```bash
   export PATH=$PATH:$HOME/dotnet
   ```
   
7. Exécutez la commande `dotnet --version` pour vérifier que l’installation a réussi.

   ```bash
   dotnet --version
   ```   
  

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

2. Vérifier les prérequis.

   ```bash
   sudo apt-get install curl libunwind8 gettext
   ```

3. Téléchargez les fichiers binaires du SDK .NET Core (tarball).

   ```bash
   curl -sSL -o dotnet.tar.gz https://go.microsoft.com/fwlink/?linkid=848826
   ```

4. Extrayez les fichiers binaires du SDK .NET Core.

   ```bash
   sudo mkdir -p /opt/dotnet && sudo tar zxf dotnet.tar.gz -C /opt/dotnet
   ```

5. Ajoutez dotnet au chemin.

   ```bash
   sudo ln -s /opt/dotnet/dotnet /usr/local/bin
   ```

6. Exécutez la commande `dotnet --version` pour vérifier que l’installation a réussi.

   ```bash
   dotnet --version
   ```

---

## <a name="install-net-core-for-fedora-24-fedora-25-or-fedora-26-64-bit"></a>Installer .NET Core pour Fedora 24, Fedora 25 ou Fedora 26 (64 bits)

Pour installer .NET Core 2.x sur Fedora 26 ou Fedora 25, ou .NET Core 1.x sur Fedora 24 :

1. Supprimez du système toute **version antérieure** de .NET Core.

> [!NOTE]
> Un répertoire contrôlé par l’utilisateur est requis pour les installations du système Linux système depuis tar.gz.

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

**Fedora 26 ou Fedora 25**

2. Enregistrez la clé de signature Microsoft approuvée.

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

3. Ajoutez le flux de produit dotnet.

   ```bash
   sudo sh -c 'echo -e "[packages-microsoft-com-prod]\nname=packages-microsoft-com-prod \nbaseurl=https://packages.microsoft.com/yumrepos/microsoft-rhel7.3-prod\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/dotnetdev.repo'
   ```

4. Installez le SDK .NET Core.

   ```bash
   sudo dnf update
   sudo dnf install libunwind libicu
   sudo dnf install dotnet-sdk-2.0.0
   ```

5. Ajoutez dotnet au chemin.

   ```bash
   export PATH=$PATH:$HOME/dotnet
   ```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

**Fedora 24**

2. Vérifier les prérequis.

   ```bash
   sudo dnf install libunwind libicu
   ```

3. Téléchargez le fichier binaire du SDK .NET Core (tarball).

   ```bash
   curl -sSL -o dotnet.tar.gz https://go.microsoft.com/fwlink/?linkid=848833
   ```

4. Extrayez les fichiers binaires du SDK .NET Core.

   ```bash
   sudo mkdir -p /opt/dotnet && sudo tar zxf dotnet.tar.gz -C /opt/dotnet
   ```

5. Ajoutez dotnet au chemin.

   ```bash
   sudo ln -s /opt/dotnet/dotnet /usr/local/bin
   ```
   
---

6. Exécutez la commande `dotnet --version` pour vérifier que l’installation a réussi.

   ```bash
   dotnet --version
   ```

## <a name="install-net-core-for-centos-71-64-bit--oracle-linux-71-64-bit"></a>Installer .NET Core pour CentOS 7.1 (64 bits) et Oracle Linux 7.1 (64 bits)

Pour installer .NET Core pour CentOS 7.1 (64 bits) et Oracle Linux 7.1 (64 bits) :

1. Supprimez du système toute **version antérieure** de .NET Core.

> [!NOTE]
> Un répertoire contrôlé par l’utilisateur est requis pour les installations du système Linux système depuis tar.gz.

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

2. Enregistrez la clé de signature Microsoft approuvée.

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

3. Ajoutez le flux de produit Microsoft.

   ```bash
   sudo sh -c 'echo -e "[packages-microsoft-com-prod]\nname=packages-microsoft-com-prod \nbaseurl=https://packages.microsoft.com/yumrepos/microsoft-rhel7.3-prod\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/dotnetdev.repo'
   ```

4. Installez le SDK .NET Core.

   ```bash
   sudo yum update
   sudo yum install libunwind libicu
   sudo yum install dotnet-sdk-2.0.0
   ```

5. Ajoutez dotnet au chemin.

   ```bash
   export PATH=$PATH:$HOME/dotnet
   ```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

2. Vérifier les prérequis.

   ```bash
   sudo yum install libunwind libicu
   ```
   
3. Téléchargez le fichier binaire du SDK .NET Core (tarball).

   ```bash
   curl -sSL -o dotnet.tar.gz https://go.microsoft.com/fwlink/?linkid=848821
   ```

4. Extrayez les fichiers binaires du SDK .NET Core.

   ```bash
   sudo mkdir -p /opt/dotnet && sudo tar zxf dotnet.tar.gz -C /opt/dotnet
   ```

5. Ajoutez dotnet au chemin.

   ```bash
   sudo ln -s /opt/dotnet/dotnet /usr/local/bin
   ```

---

6. Exécutez la commande `dotnet --version` pour vérifier que l’installation a réussi.

   ```bash
   dotnet --version
   ```

## <a name="install-net-core-for-suse-linux-enterprise-server-64-bit"></a>Installer .NET Core pour SUSE Linux Enterprise Server (64 bits)

Pour installer .NET Core 2.x pour SUSE Linux Enterprise Server (SLES) 12 SP2 (64 bits) :

1. Supprimez du système toute **version antérieure** de .NET Core.

2. Ajoutez le flux de produit dotnet.

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   sudo sh -c 'echo -e "[packages-microsoft-com-prod]\nname=packages-microsoft-com-prod \nbaseurl=https://packages.microsoft.com/yumrepos/microsoft-rhel7.3-prod\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/dotnetdev.repo'
   ```

3. Installez le SDK .NET Core.

   ```bash
   sudo zypper update
   sudo zypper install libunwind libicu
   sudo zypper install dotnet-sdk-2.0.0
   ```

4. Ajoutez dotnet au chemin.

   ```bash
   export PATH=$PATH:$HOME/dotnet
   ```

5. Exécutez la commande `dotnet --version` pour vérifier que l’installation a réussi.

   ```bash
   dotnet --version
   ```
   
## <a name="install-net-core-for-opensuse-64-bit"></a>Installer .NET Core pour openSUSE (64 bits)

Pour installer .NET Core 2.x pour openSUSE ou .NET Core 1.x pour openSUSE (64 bits) :

1. Supprimez du système toute **version antérieure** de .NET Core.

> [!NOTE]
> Un répertoire contrôlé par l’utilisateur est requis pour les installations du système Linux système depuis tar.gz.

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

2. Enregistrez la clé de signature Microsoft approuvée.

   ```bash
   sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
   ```

3. Ajoutez le flux de produit dotnet.

   ```bash
   sudo sh -c 'echo -e "[packages-microsoft-com-prod]\nname=packages-microsoft-com-prod \nbaseurl=https://packages.microsoft.com/yumrepos/microsoft-rhel7.3-prod\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/dotnetdev.repo'
   ``` 

4. Installez le SDK .NET Core.

   ```bash
   sudo zypper update
   sudo zypper install libunwind libicu
   sudo zypper install dotnet-sdk-2.0.0
   ```

5. Ajoutez dotnet au chemin.

   ```bash
   export PATH=$PATH:$HOME/dotnet
   ```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

2. Vérifier les prérequis.

   ```bash
   sudo zypper install libunwind libicu
   ```

3. Téléchargez le fichier binaire du SDK .NET Core (tarball).

   ```bash
   curl -sSL -o dotnet.tar.gz https://go.microsoft.com/fwlink/?linkid=848824
   ```

4. Extrayez les fichiers binaires du SDK .NET Core.
   
   ```bash
   sudo mkdir -p /opt/dotnet && sudo tar zxf dotnet.tar.gz -C /opt/dotnet
   ```

5. Ajoutez dotnet au chemin.

   ```bash
   sudo ln -s /opt/dotnet/dotnet /usr/local/bin
   ```
   
---

6. Exécutez la commande `dotnet --version` pour vérifier que l’installation a réussi.

   ```bash
   dotnet --version
   ```

> [!IMPORTANT]
> En cas de problème avec l’installation de .NET Core 2.x sur une distribution/version Linux prise en charge, consultez la rubrique correspondante traitant des [problèmes connus avec la version 2.0](https://github.com/dotnet/core/tree/master/release-notes/2.0). 
>
> En cas de problème avec l’installation de .NET Core 1.x sur une distribution/version Linux prise en charge, consultez la rubrique correspondante traitant des [problèmes connus avec la version 1.0.0](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.0-known-issues.md) ou des [problèmes connus avec la version 1.0.1](https://github.com/dotnet/core/blob/master/release-notes/1.0/1.0.1-known-issues.md).
