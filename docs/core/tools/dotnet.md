---
title: Commande dotnet - Interface CLI .NET Core
description: "Découvrez la commande dotnet (le pilote générique des outils .NET Core CLI) et comment l’utiliser."
author: mairaw
ms.author: mairaw
ms.date: 08/14/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.workload:
- dotnetcore
ms.openlocfilehash: 2eea7d13994bfddc89d8f3513308a6620c53c88c
ms.sourcegitcommit: f28752eab00d2bd97e971542c0f49ce63cfbc239
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2018
---
# <a name="dotnet-command"></a>Commande dotnet

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>Name

`dotnet` - Pilote général pour l’exécution des commandes de ligne de commande.

## <a name="synopsis"></a>Résumé

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)
```
dotnet [command] [arguments] [--additional-deps] [--additionalprobingpath] [-d|--diagnostics] [--fx-version] [-h|--help] [--info] [--roll-forward-on-no-candidate-fx] [-v|--verbose] [--version]
```
# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
```
dotnet [command] [arguments] [--additionalprobingpath] [-d|--diagnostics] [--fx-version] [-h|--help] [--info] [-v|--verbose] [--version]
```
---

## <a name="description"></a>Description

`dotnet` est un pilote générique pour la chaîne d’outils de l’interface de ligne de commande (CLI). Appelé seul, il fournit des instructions d’utilisation succinctes.

Chaque fonctionnalité est implémentée comme une commande. Pour utiliser la fonctionnalité, la commande est spécifiée après `dotnet`, comme dans [`dotnet build`](dotnet-build.md). Tous les arguments qui suivent la commande sont ses arguments propres.

Le seul cas où la commande `dotnet` est utilisée seule est l’exécution d’applications [dépendantes du framework](../deploying/index.md). Spécifiez une DLL d’application après le verbe `dotnet` pour exécuter l’application (par exemple, `dotnet myapp.dll`).

## <a name="options"></a>Options

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`--additional-deps <PATH>`

Chemin du fichier *deps.json* supplémentaire.

`--additionalprobingpath <PATH>`

Chemin d’accès contenant la stratégie de sondage et les assemblys à sonder.

`-d|--diagnostics`

Active la sortie de diagnostic.

`--fx-version <VERSION>`

Version du runtime .NET Core installé à utiliser pour exécuter l’application.

`-h|--help`

Affiche une aide brève pour la commande. Si vous l’utilisez avec `dotnet`, elle affiche également la liste des commandes disponibles.

`--info`

Affiche des informations détaillées sur l’environnement et les outils CLI, telles que le système d’exploitation actuel, le SHA de validation de la version, etc.

`--roll-forward-on-no-candidate-fx`

 Effectue une restauration par progression en l’absence de framework candidat partagé.

`-v|--verbose`

Active la sortie détaillée.

`--version`

Affiche la version du SDK .NET Core en cours d’utilisation.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`--additionalprobingpath <PATH>`

Chemin d’accès contenant la stratégie de sondage et les assemblys à sonder.

`-d|--diagnostics`

Active la sortie de diagnostic.

`--fx-version <VERSION>`

Version du runtime .NET Core installé à utiliser pour exécuter l’application.

`-h|--help`

Affiche une aide brève pour la commande. Si vous l’utilisez avec `dotnet`, elle affiche également la liste des commandes disponibles.

`--info`

Affiche des informations détaillées sur l’environnement et les outils CLI, telles que le système d’exploitation actuel, le SHA de validation de la version, etc.

`-v|--verbose`

Active la sortie détaillée.

`--version`

Affiche la version du SDK .NET Core en cours d’utilisation.

---

## <a name="dotnet-commands"></a>Commandes dotnet

### <a name="general"></a>Général

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

| Commande                             | Fonction                                                            |
| ----------------------------------- | ------------------------------------------------------------------- |
| [dotnet build](dotnet-build.md)     | Génère une application .NET Core.                                     |
| [dotnet clean](dotnet-clean.md)     | Nettoie les sorties de build.                                              |
| [dotnet help](dotnet-help.md)       | Affiche plus de documentation détaillée en ligne pour la commande.           |
| [dotnet migrate](dotnet-migrate.md) | Migre un projet Preview 2 valide vers un projet SDK .NET Core 1.0.  |
| [dotnet msbuild](dotnet-msbuild.md) | Fournit l’accès à la ligne de commande MSBuild.                        |
| [dotnet new](dotnet-new.md)         | Initialise un projet C# ou F# pour un modèle donné.                |
| [dotnet pack](dotnet-pack.md)       | Crée un package NuGet à partir de votre code.                               |
| [dotnet publish](dotnet-publish.md) | Publie une application .NET dépendante du framework ou autonome. |
| [dotnet restore](dotnet-restore.md) | Restaure les dépendances d’une application donnée.                  |
| [dotnet run](dotnet-run.md)         | Exécute l’application à partir de la source.                                   |
| [dotnet sln](dotnet-sln.md)         | Options pour ajouter, supprimer et lister des projets dans un fichier solution.       |
| [dotnet store](dotnet-store.md)     | Stocke les assemblys dans le magasin de packages de runtime.                     |
| [dotnet test](dotnet-test.md)       | Exécute des tests à l’aide d’un lanceur de tests.                                     |

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

| Commande                             | Fonction                                                            |
| ----------------------------------- | ------------------------------------------------------------------- |
| [dotnet build](dotnet-build.md)     | Génère une application .NET Core.                                     |
| [dotnet clean](dotnet-clean.md)     | Nettoie les sorties de build.                                              |
| [dotnet migrate](dotnet-migrate.md) | Migre un projet Preview 2 valide vers un projet SDK .NET Core 1.0.  |
| [dotnet msbuild](dotnet-msbuild.md) | Fournit l’accès à la ligne de commande MSBuild.                        |
| [dotnet new](dotnet-new.md)         | Initialise un projet C# ou F# pour un modèle donné.                |
| [dotnet pack](dotnet-pack.md)       | Crée un package NuGet à partir de votre code.                               |
| [dotnet publish](dotnet-publish.md) | Publie une application .NET dépendante du framework ou autonome. |
| [dotnet restore](dotnet-restore.md) | Restaure les dépendances d’une application donnée.                  |
| [dotnet run](dotnet-run.md)         | Exécute l’application à partir de la source.                                   |
| [dotnet sln](dotnet-sln.md)         | Options pour ajouter, supprimer et lister des projets dans un fichier solution.       |
| [dotnet test](dotnet-test.md)       | Exécute des tests à l’aide d’un lanceur de tests.                                     |

---

### <a name="project-references"></a>Références de projets

Commande | Fonction
--- | ---
[dotnet add reference](dotnet-add-reference.md) | Ajoute une référence de projet.
[dotnet list reference](dotnet-list-reference.md) | Liste les références du projet.
[dotnet remove reference](dotnet-remove-reference.md) | Supprime une référence de projet.

### <a name="nuget-packages"></a>Packages NuGet

Commande | Fonction
--- | ---
[dotnet add package](dotnet-add-package.md) | Ajoute un package NuGet.
[dotnet remove package](dotnet-remove-package.md) | Supprime un package NuGet.

### <a name="nuget-commands"></a>Commandes NuGet

Commande | Fonction
--- | ---
[dotnet nuget delete](dotnet-nuget-delete.md) | Supprime ou retire un package du serveur.
[dotnet nuget locals](dotnet-nuget-locals.md) | Efface ou liste les ressources NuGet locales telles que le cache de requête HTTP, le cache temporaire ou le dossier de packages globaux à l’échelle de l’ordinateur.
[dotnet nuget push](dotnet-nuget-push.md) | Effectue une transmission de type push d’un package sur le serveur et le publie.

## <a name="examples"></a>Exemples

Initialisez un exemple d’application console .NET Core qui peut être compilé et exécuté :

`dotnet new console`

Restaurez les dépendances d’une application donnée :

`dotnet restore`

[!INCLUDE[DotNet Restore Note](~/includes/dotnet-restore-note.md)]

Générez un projet et ses dépendances dans un répertoire donné :

`dotnet build`

Exécuter une application dépendante du framework nommée `myapp.dll` :

`dotnet myapp.dll`

## <a name="environment-variables"></a>Variables d’environnement

`DOTNET_PACKAGES`

Cache du package principal. S’il n’est pas défini, les valeurs par défaut sont `$HOME/.nuget/packages` sous Unix et `%HOME%\NuGet\Packages` sous Windows.

`DOTNET_SERVICING`

Spécifie l’emplacement de l’index de service que doit utiliser l’hôte partagé lors du chargement de l’exécution.

`DOTNET_CLI_TELEMETRY_OPTOUT`

Spécifie si les données concernant l’utilisation des outils .NET Core doivent être collectées et envoyées à Microsoft. Définie sur `true` pour ne pas adhérer à la fonctionnalité de télémétrie (valeurs acceptées : `1`, `yes` ou `false`) ; définie sur `true` pour adhérer aux fonctionnalités de télémétrie (valeurs acceptées : `false`, `0` ou `no`). Si elle n’est pas définie, la valeur par défaut est `false`, et la fonctionnalité de télémétrie est active.
