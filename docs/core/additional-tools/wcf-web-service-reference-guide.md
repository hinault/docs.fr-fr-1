---
title: Outil Microsoft WCF Web Service Reference Provider
description: "Vue d’ensemble de l’outil Microsoft WCF Web Service Reference Provider, qui ajoute des fonctionnalités pour les projets .NET Core et ASP.NET Core, de manière similaire à la fonctionnalité Ajouter une référence de service pour les projets .NET Framework."
author: mlacouture
manager: wpickett
ms.author: johalex
ms.date: 01/19/2018
ms.topic: article
ms.prod: .net-core
ms.custom: mvc
ms.openlocfilehash: e445361f9f4a858f4b34ca1008670fadc62b8b3c
ms.sourcegitcommit: dd6ea7f0e581ac84e0a90d9b23c463fcf1ec3ce7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2018
---
# <a name="microsoft-wcf-web-service-reference-provider-tool"></a>Outil Microsoft WCF Web Service Reference Provider

Au fil des années, de nombreux développeurs Visual Studio ont apprécié le gain de productivité offert par l’outil [**Ajouter une référence de service**](/visualstudio/data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference) quand leurs projets .NET Framework avaient besoin d’accéder à des services web.  L’outil **WCF Web Service Reference** est une extension de service connecté de Visual Studio qui fournit une expérience semblable à la fonctionnalité Ajouter une référence de service pour les projets .NET Core et ASP.NET Core. Cet outil récupère les métadonnées d’un service web dans la solution actuelle sur un emplacement réseau ou dans un fichier WSDL, puis génère un fichier source compatible .NET Core contenant du code de proxy client WCF (Windows Communication Foundation) que vous pouvez utiliser pour accéder au service web.

> [!IMPORTANT]
> Vous devez référencer des services uniquement à partir d’une source approuvée. L’ajout de références à partir d’une source non fiable peut compromettre la sécurité. 

## <a name="how-to-use-the-extension"></a>Comment utiliser l’extension

> [!NOTE]
> L’option **WCF Web Service Reference** s’applique aux projets créés à l’aide des modèles de projet suivants :
> * **Visual C#** > **.NET Core**
> * **Visual C#** > **.NET Standard**
> * **Visual C#** > **Web** > **Application web ASP.NET Core**

Prenant le modèle de projet **Application web ASP.NET Core** en guise d’exemple, cet article explique comment ajouter une référence de service WCF au projet :

1. Dans l’Explorateur de solutions, double-cliquez sur le nœud du projet **Services connectés** (pour un projet .NET Core ou .NET Standard, cette option est disponible quand vous cliquez avec le bouton droit sur le nœud **Dépendances** du projet dans l’Explorateur de solutions).

La page **Services connectés** s’affiche, comme illustré ci-dessous :

![Onglet Services connectés](./media/wcf-web-service-reference-guide/wcfcs-ConnectedServicesPage.png)

2. Dans la page **Services connectés**, cliquez sur **Microsoft WCF Web Service Reference Provider**. L’Assistant **Configurer la référence de services web WCF** apparaît :

![Onglet Point de terminaison de service](./media/wcf-web-service-reference-guide/wcfcs-ServiceEndpointPage.png)

3. Sélectionnez un service.

    3a. Plusieurs options de recherche de services sont disponibles dans l’Assistant **Configurer la référence de services web WCF** :
    
     * Pour rechercher parmi les services définis dans la solution actuelle, cliquez sur le bouton **Découvrir**. 
     * Pour rechercher parmi les services hébergés à une adresse spécifiée, entrez une URL de service dans la zone **Adresse**, puis cliquez sur le bouton **Envoyer**.
     * Pour sélectionner un fichier WSDL qui contient les informations de métadonnées de service web, cliquez sur le bouton **Parcourir**. 
     
    3b. Sélectionnez le service dans la liste des résultats de recherche dans la zone **Services**. Si nécessaire, entrez l’espace de noms du code généré dans la zone de texte **Espace de noms** correspondante.
    
    3c. Cliquez sur le bouton **Suivant** pour ouvrir les pages **Options du type de données** et **Options du client**. Vous pouvez aussi cliquer sur le bouton **Terminer** pour utiliser les options par défaut.


4. Le formulaire **Options du type de données** vous permet d’affiner les paramètres de configuration de référence de service générés :

![Onglet Options du type de données](./media/wcf-web-service-reference-guide/wcfcs-DataTypesPage.png)

> [!NOTE]
> La case à cocher **Réutiliser les types dans les assemblys référencés** est utile quand les types de données nécessaires pour la génération du code de référence de service sont définis dans l’un des assemblys référencés de votre projet.  Il est important de réutiliser ces types de données existants pour éviter les conflits de type au moment de la compilation ou les problèmes au moment de l’exécution.

Il peut y avoir un délai pendant le chargement des informations de type, en fonction du nombre de dépendances du projet et d’autres facteurs de performances système. Le bouton **Terminer** est désactivé pendant le chargement, sauf si la case **Réutiliser les types dans les assemblys référencés** est cochée.

5. Cliquez sur **Terminer** quand vous avez terminé.


Lors de l’affichage de la progression, l’outil :

* Télécharge les métadonnées à partir du service WCF. 
* Génère le code de référence de service dans un fichier nommé *reference.cs* et l’ajoute à votre projet sous le nœud **Services connectés**. 
* Met à jour le fichier projet (.csproj) avec les références de package NuGet nécessaires pour la compilation et l’exécution sur la plateforme cible.

![Fenêtre de progression](./media/wcf-web-service-reference-guide/wcfcs-ProgressWindow.png)

Une fois ces processus terminés, vous pouvez créer une instance du type de client WCF généré et appeler les opérations de service.

## <a name="next-steps"></a>Étapes suivantes

### <a name="feedback--questions"></a>Commentaires et questions
Si vous avez des questions ou des commentaires, [ouvrez un problème sur GitHub](https://github.com/dotnet/wcf/issues/new). Vous pouvez également consulter les questions ou problèmes existants dans le [dépôt WCF sur GitHub](https://github.com/dotnet/wcf/issues?utf8=%E2%9C%93&q=is:issue%20label:tooling).

### <a name="release-notes"></a>Notes de publication
* Pour obtenir des informations à jour sur les versions, notamment les problèmes connus, consultez les [Notes de publication](https://github.com/dotnet/wcf/blob/master/release-notes/WCF-Web-Service-Reference-notes.md). 
