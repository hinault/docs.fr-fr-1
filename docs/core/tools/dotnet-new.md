---
title: Commande dotnet new - Interface CLI .NET Core
description: "La commande dotnet new crée des projets .NET Core basés sur le modèle spécifié."
keywords: "dotnet-new, CLI, commande CLI, .NET Core"
author: mairaw
ms.author: mairaw
ms.date: 08/13/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: fcc3ed2e-9265-4d50-b59e-dc2e5c190b34
ms.workload: dotnetcore
ms.openlocfilehash: cf65dc80f135badcb1580726a12a9ae9d94ae3d7
ms.sourcegitcommit: 8bde7a3432f30fc771079744955c75c58c4eb393
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/20/2018
---
# <a name="dotnet-new"></a>dotnet new

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>Name

`dotnet new` : crée un projet, un fichier de configuration ou une solution en fonction du modèle spécifié.

## <a name="synopsis"></a>Résumé

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)
```
dotnet new <TEMPLATE> [--force] [-i|--install] [-lang|--language] [-n|--name] [-o|--output] [-u|--uninstall] [Template options]
dotnet new <TEMPLATE> [-l|--list] [--type]
dotnet new [-h|--help]
```
# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
```
dotnet new <TEMPLATE> [-lang|--language] [-n|--name] [-o|--output] [-all|--show-all] [-h|--help] [Template options]
dotnet new <TEMPLATE> [-l|--list]
dotnet new [-all|--show-all]
dotnet new [-h|--help]
```
---

## <a name="description"></a>Description

La commande `dotnet new` offre un moyen pratique d’initialiser un projet .NET Core valide. 

La commande appelle le [moteur de modèles](https://github.com/dotnet/templating) pour créer les artefacts sur le disque en fonction du modèle et des options spécifiés.

## <a name="arguments"></a>Arguments

`TEMPLATE`

Modèle à instancier quand la commande est appelée. Vous pouvez passer des options spécifiques pour chaque modèle. Pour plus d'informations, consultez [Options de modèle](#template-options).

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

La commande contient une liste par défaut de modèles. Utilisez `dotnet new -l` pour obtenir une liste des modèles disponibles. Le tableau suivant présente les modèles préinstallés avec le SDK .NET Core 2.0. Le langage par défaut pour le modèle est indiqué entre crochets.

|Description du modèle                          | Nom du modèle | Langages     |
|----------------------------------------------|---------------|---------------|
| Application console                          | `console`     | [C#], F#, VB  |
| Bibliothèque de classes                                | `classlib`    | [C#], F#, VB  |
| Projet de test unitaire                            | `mstest`      | [C#], F#, VB  |
| Projet de test xUnit                           | `xunit`       | [C#], F#, VB  |
| ASP.NET Core vide                           | `web`         | [C#], F#      |
| Application web ASP.NET Core (Model-View-Controller) | `mvc`         | [C#], F#      |
| Application web ASP.NET Core                         | `razor`       | [C#]          |
| ASP.NET Core avec Angular                    | `angular`     | [C#]          |
| ASP.NET Core avec React.js                   | `react`       | [C#]          |
| ASP.NET Core avec React.js et Redux         | `reactredux`  | [C#]          |
| API web ASP.NET Core                         | `webapi`      | [C#], F#      |
| fichier global.json                             | `globaljson`  |               |
| Config NuGet                                 | `nugetconfig` |               |
| config web                                   | `webconfig`   |               |
| Fichier solution                                | `sln`         |               |
| Page Razor                                   | `page`        |               |
| MVC/ViewImports                              | `viewimports` |               |
| ViewStart MVC                                | `viewstart`   |               |

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

La commande contient une liste par défaut de modèles. Utilisez `dotnet new -all` pour obtenir une liste des modèles disponibles. Le tableau suivant présente les modèles préinstallés avec le SDK .NET Core 1.x. Le langage par défaut pour le modèle est indiqué entre crochets.

|Description du modèle  | Nom du modèle | Langages |
|----------------------|---------------|-----------|
| Application console  | `console`     | [C#], F#  |
| Bibliothèque de classes        | `classlib`    | [C#], F#  |
| Projet de test unitaire    | `mstest`      | [C#], F#  |
| Projet de test xUnit   | `xunit`       | [C#], F#  |
| ASP.NET Core vide   | `web`         | [C#]      |
| Application web ASP.NET Core | `mvc`         | [C#], F#  |
| API web ASP.NET Core | `webapi`      | [C#]      |
| Config NuGet         | `nugetconfig` |           |
| config web           | `webconfig`   |           |
| Fichier solution        | `sln`         |           |

---

## <a name="options"></a>Options

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`--force`

Force le contenu à être généré même s’il change les fichiers existants. Ceci est nécessaire quand le répertoire de sortie contient déjà un projet.

`-h|--help`

Affiche l’aide pour la commande. Elle peut être appelée pour la commande `dotnet new` elle-même ou pour n’importe quel modèle, par exemple, `dotnet new mvc --help`.

`-i|--install <PATH|NUGET_ID>`

Installe un pack source ou de modèle à partir du `PATH` ou `NUGET_ID` fourni. Pour plus d’informations sur la création de modèles personnalisés, consultez [Modèles personnalisés pour dotnet new](custom-templates.md).

`-l|--list`

Liste les modèles contenant le nom spécifié. Si elle est appelée pour la commande `dotnet new`, elle liste les modèles disponibles dans le répertoire donné. Par exemple, si le répertoire contient déjà un projet, elle ne liste pas tous les modèles de projet.

`-lang|--language {C#|F#|VB}`

Langage du modèle à créer. Le langage accepté diffère selon le modèle (voir les valeurs par défaut dans la section [arguments](#arguments)). Non valide pour certains modèles.

`-n|--name <OUTPUT_NAME>`

Le nom de la sortie créée. Si aucun nom n’est spécifié, le nom du répertoire actif est utilisé.

`-o|--output <OUTPUT_DIRECTORY>`

Emplacement où placer la sortie générée. La valeur par défaut correspond au répertoire actif.

`--type`

Filtre les modèles en fonction des types disponibles. Les valeurs prédéfinies sont « project », « item » ou « other ».

`-u|--uninstall <PATH|NUGET_ID>`

Désinstalle un pack source ou de modèle au `PATH` ou `NUGET_ID` fourni.

> [!NOTE]
> Pour désinstaller un modèle à l’aide de `PATH`, vous devez qualifier le chemin d’accès avec un nom complet. Par exemple, *C:/Users/\<USER>/Documents/Templates/GarciaSoftware.ConsoleTemplate.CSharp* fonctionne, mais *./GarciaSoftware.ConsoleTemplate.CSharp* à partir du dossier conteneur ne fonctionne pas.
> En outre, n’incluez pas de barre oblique finale après le répertoire dans votre chemin d’accès au modèle.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`-all|--show-all`

Affiche tous les modèles pour un type de projet spécifique lors de l’exécution dans le contexte de la commande `dotnet new` seule. Lors de l’exécution dans le contexte d’un modèle spécifique, comme `dotnet new web -all`, `-all` est interprété comme un indicateur de création forcée. Ceci est nécessaire quand le répertoire de sortie contient déjà un projet.

`-h|--help`

Affiche l’aide pour la commande. Elle peut être appelée pour la commande `dotnet new` elle-même ou pour n’importe quel modèle, par exemple, `dotnet new mvc --help`.

`-l|--list`

Liste les modèles contenant le nom spécifié. Si elle est appelée pour la commande `dotnet new`, elle liste les modèles disponibles dans le répertoire donné. Par exemple, si le répertoire contient déjà un projet, elle ne liste pas tous les modèles de projet.

`-lang|--language {C#|F#}`

Langage du modèle à créer. Le langage accepté diffère selon le modèle (voir les valeurs par défaut dans la section [arguments](#arguments)). Non valide pour certains modèles.

`-n|--name <OUTPUT_NAME>`

Le nom de la sortie créée. Si aucun nom n’est spécifié, le nom du répertoire actif est utilisé.

`-o|--output <OUTPUT_DIRECTORY>`

Emplacement où placer la sortie générée. La valeur par défaut correspond au répertoire actif.

---

## <a name="template-options"></a>Options de modèle

Chaque modèle de projet peut présenter d’autres options disponibles. Les modèles de base ont les options supplémentaires suivantes :

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

**console, angular, react, reactredux**

`--no-restore` : n’effectue pas de restauration implicite pendant la création du projet.

**classlib**

`-f|--framework <FRAMEWORK>` : spécifie le [framework](../../standard/frameworks.md) à cibler. Valeurs : `netcoreapp2.0` pour créer une bibliothèque de classes .NET Core ou `netstandard2.0` pour créer une bibliothèque de classes .NET Standard. La valeur par défaut est `netstandard2.0`.

`--no-restore` : n’effectue pas de restauration implicite pendant la création du projet.

**mstest, xunit**

`-p|--enable-pack` : permet l’empaquetage pour le projet à l’aide de [dotnet pack](dotnet-pack.md).

`--no-restore` : n’effectue pas de restauration implicite pendant la création du projet.

**globaljson**

`--sdk-version <VERSION_NUMBER>` : spécifie la version du SDK .NET Core à utiliser dans le fichier *global.json*.

**web**

`--use-launch-settings` : inclut *launchSettings.json* dans la sortie de modèle générée.

`--no-restore` : n’effectue pas de restauration implicite pendant la création du projet.

**webapi**

`-au|--auth <AUTHENTICATION_TYPE>` : type d’authentification à utiliser. Les valeurs possibles sont :

- `None` : aucune authentification (configuration par défaut).
- `IndividualB2C` : authentification individuelle avec Azure AD B2C.
- `SingleOrg` : authentification d’organisation pour un seul abonné.
- `Windows` : authentification Windows.

`--aad-b2c-instance <INSTANCE>` : instance d’Azure Active Directory B2C à laquelle se connecter. À utiliser avec l’authentification `IndividualB2C`. La valeur par défaut est `https://login.microsoftonline.com/tfp/`.

`-ssp|--susi-policy-id <ID>` : ID de la stratégie de connexion et d’inscription pour ce projet. À utiliser avec l’authentification `IndividualB2C`.

`--aad-instance <INSTANCE>` : instance d’Azure Active Directory à laquelle se connecter. À utiliser avec l’authentification `SingleOrg`. La valeur par défaut est `https://login.microsoftonline.com/`.

`--client-id <ID>` : ID client pour ce projet. À utiliser avec l’authentification `IndividualB2C` ou `SingleOrg`. La valeur par défaut est `11111111-1111-1111-11111111111111111`.

`--domain <DOMAIN>` : domaine de l’abonné d’annuaire. À utiliser avec l’authentification `SingleOrg` ou `IndividualB2C`. La valeur par défaut est `qualified.domain.name`.

`--tenant-id <ID>` : ID d’abonné de l’annuaire auquel se connecter. À utiliser avec l’authentification `SingleOrg`. La valeur par défaut est `22222222-2222-2222-2222-222222222222`.

`-r|--org-read-access` : accorde à cette application un accès en lecture au répertoire. S’applique uniquement à l’authentification `SingleOrg` ou `MultiOrg`.

`--use-launch-settings` : inclut *launchSettings.json* dans la sortie de modèle générée.

`-uld|--use-local-db` : spécifie que la base de données locale doit être utilisée à la place de SQLite. S’applique uniquement à l’authentification `Individual` ou `IndividualB2C`.

`--no-restore` : n’effectue pas de restauration implicite pendant la création du projet.

**mvc, razor**

`-au|--auth <AUTHENTICATION_TYPE>` : type d’authentification à utiliser. Les valeurs possibles sont :

- `None` : aucune authentification (configuration par défaut).
- `Individual` : authentification individuelle.
- `IndividualB2C` : authentification individuelle avec Azure AD B2C.
- `SingleOrg` : authentification d’organisation pour un seul abonné.
- `MultiOrg` : authentification d’organisation pour plusieurs abonnés.
- `Windows` : authentification Windows.

`--aad-b2c-instance <INSTANCE>` : instance d’Azure Active Directory B2C à laquelle se connecter. À utiliser avec l’authentification `IndividualB2C`. La valeur par défaut est `https://login.microsoftonline.com/tfp/`.

`-ssp|--susi-policy-id <ID>` : ID de la stratégie de connexion et d’inscription pour ce projet. À utiliser avec l’authentification `IndividualB2C`.

`-rp|--reset-password-policy-id <ID>` : ID de stratégie de réinitialisation du mot de passe pour ce projet. À utiliser avec l’authentification `IndividualB2C`.

`-ep|--edit-profile-policy-id <ID>` : ID de stratégie de modification du profil pour ce projet. À utiliser avec l’authentification `IndividualB2C`.

`--aad-instance <INSTANCE>` : instance d’Azure Active Directory à laquelle se connecter. À utiliser avec l’authentification `SingleOrg` ou `MultiOrg`. La valeur par défaut est `https://login.microsoftonline.com/`.

`--client-id <ID>` : ID client pour ce projet. À utiliser avec l’authentification `IndividualB2C`, `SingleOrg` ou `MultiOrg`. La valeur par défaut est `11111111-1111-1111-11111111111111111`.

`--domain <DOMAIN>` : domaine de l’abonné d’annuaire. À utiliser avec l’authentification `SingleOrg` ou `IndividualB2C`. La valeur par défaut est `qualified.domain.name`.

`--tenant-id <ID>` : ID d’abonné de l’annuaire auquel se connecter. À utiliser avec l’authentification `SingleOrg`. La valeur par défaut est `22222222-2222-2222-2222-222222222222`.

`--callback-path <PATH>` : chemin de demande dans le chemin de base de l’application de l’URI de redirection. À utiliser avec l’authentification `SingleOrg` ou `IndividualB2C`. La valeur par défaut est `/signin-oidc`.

`-r|--org-read-access` : accorde à cette application un accès en lecture au répertoire. S’applique uniquement à l’authentification `SingleOrg` ou `MultiOrg`.

`--use-launch-settings` : inclut *launchSettings.json* dans la sortie de modèle générée.

`--use-browserlink` : inclut BrowserLink dans le projet.

`-uld|--use-local-db` : spécifie que la base de données locale doit être utilisée à la place de SQLite. S’applique uniquement à l’authentification `Individual` ou `IndividualB2C`.

`--no-restore` : n’effectue pas de restauration implicite pendant la création du projet.

**page**

`-na|--namespace <NAMESPACE_NAME>` : espace de noms pour le code généré. La valeur par défaut est `MyApp.Namespace`.

`-np|--no-pagemodel` : crée la page sans modèle de page.

**viewimports**

`-na|--namespace <NAMESPACE_NAME>` : espace de noms pour le code généré. La valeur par défaut est `MyApp.Namespace`.

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

**console, xunit, mstest, web, webapi**

`-f|--framework` : spécifie le [framework](../../standard/frameworks.md) à cibler. Valeurs : `netcoreapp1.0` ou `netcoreapp1.1`. La valeur par défaut est `netcoreapp1.0`.

**classlib**

`-f|--framework` : spécifie le [framework](../../standard/frameworks.md) à cibler. Valeurs : `netcoreapp1.0`, `netcoreapp1.1` ou `netstandard1.0` à `netstandard1.6`. La valeur par défaut est `netstandard1.4`.

**mvc**

`-f|--framework` : spécifie le [framework](../../standard/frameworks.md) à cibler. Valeurs : `netcoreapp1.0` ou `netcoreapp1.1`. La valeur par défaut est `netcoreapp1.0`.

`-au|--auth` : type d’authentification à utiliser. Valeurs : `None` ou `Individual`. La valeur par défaut est `None`.

`-uld|--use-local-db` : spécifie s’il convient ou non d’utiliser LocalDB au lieu de SQLite. Valeurs : `true` ou `false`. La valeur par défaut est `false`.

---

## <a name="examples"></a>Exemples

Créez un projet d’application console F# dans le répertoire actif :

`dotnet new console -lang f#`

Créez un projet de bibliothèque de classes .NET Standard dans le répertoire spécifié (disponible uniquement avec le SDK .NET Core 2.0 ou ultérieur) :

`dotnet new classlib -lang VB -o MyLibrary`

Créez un projet d’application ASP.NET Core C# MVC dans le répertoire actif sans authentification ciblant .NET Core 2.0 :

`dotnet new mvc -au None -f netcoreapp2.0`

Créez une application xUnit ciblant .NET Core 2.0 :

`dotnet new xunit --framework netcoreapp2.0`

Répertoriez tous les modèles disponibles pour MVC :

`dotnet new mvc -l`

## <a name="see-also"></a>Voir aussi

[Modèles personnalisés pour dotnet new](custom-templates.md)  
[Créer un modèle personnalisé pour dotnet new](~/docs/core/tutorials/create-custom-template.md)  
[Dépôt GitHub dotnet/dotnet-template-samples](https://github.com/dotnet/dotnet-template-samples)  
[Modèles disponibles pour dotnet new](https://github.com/dotnet/templating/wiki/Available-templates-for-dotnet-new)
