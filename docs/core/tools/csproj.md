---
title: Ajouts au format csproj pour .NET Core
description: "Découvrir les différences entre les fichiers csproj existants et les fichiers csproj .NET Core"
keywords: "référence, csproj, .NET Core"
author: blackdwarf
ms.author: mairaw
ms.date: 09/22/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: bdc29497-64f2-4d11-a21b-4097e0bdf5c9
ms.workload:
- dotnetcore
ms.openlocfilehash: d2a318f099eaa67912c2cecd1c67ceebaee8629e
ms.sourcegitcommit: dd6ea7f0e581ac84e0a90d9b23c463fcf1ec3ce7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2018
---
# <a name="additions-to-the-csproj-format-for-net-core"></a>Ajouts au format csproj pour .NET Core

Ce document décrit les modifications qui ont été ajoutées aux fichiers projet dans le cadre du passage de *project.json* à *csproj* et [MSBuild](https://github.com/Microsoft/MSBuild). Pour plus d’informations de référence ou syntaxiques générales sur les fichiers projet, consultez la documentation sur les [fichiers projet MSBuild](/visualstudio/msbuild/msbuild-project-file-schema-reference).  

## <a name="implicit-package-references"></a>Références de package implicites
Les métapackages sont référencés implicitement en fonction du ou des frameworks cibles spécifiés dans la propriété `<TargetFramework>` ou `<TargetFrameworks>` de votre fichier projet. `<TargetFrameworks>` est ignoré si `<TargetFramework>` est spécifié, indépendamment de l’ordre.

```xml
 <PropertyGroup>
   <TargetFramework>netcoreapp1.1</TargetFramework>
 </PropertyGroup>
 ```
 
 ```xml
 <PropertyGroup>
   <TargetFrameworks>netcoreapp1.1;net462</TargetFrameworks>
 </PropertyGroup>
 ```

### <a name="recommendations"></a>Recommandations
Comme les métapackages `Microsoft.NETCore.App` ou `NetStandard.Library` sont implicitement référencés, voici les bonnes pratiques que nous recommandons :

* Quand vous ciblez .NET Core ou .NET Standard, n’incluez jamais de référence explicite aux métapackages `Microsoft.NETCore.App` ou `NetStandard.Library` via un élément `<PackageReference>` dans votre fichier projet.
* Si vous avez besoin d’une version spécifique du runtime quand vous ciblez .NET Core, vous devez utiliser la propriété `<RuntimeFrameworkVersion>` dans votre projet (par exemple, `1.0.4`) au lieu de référencer le métapackage.
    * Cela peut se produire si vous utilisez des [déploiements autonomes](../deploying/index.md#self-contained-deployments-scd) et que vous devez utiliser une version de correctif spécifique du runtime 1.0.0 LTS, par exemple.
* Si vous avez besoin d’une version spécifique du métapackage `NetStandard.Library` quand vous ciblez .NET Standard, vous pouvez utiliser la propriété `<NetStandardImplicitPackageVersion>` et définir la version dont vous avez besoin.
* Vous ne devez pas ajouter ni mettre à jour explicitement les références au métapackage `Microsoft.NETCore.App` ou `NetStandard.Library` dans les projets .NET Framework. Si une version de `NetStandard.Library` est nécessaire lors de l’utilisation d’un package NuGet basé sur .NET Standard, NuGet installe automatiquement cette version.

## <a name="default-compilation-includes-in-net-core-projects"></a>Inclusions de compilation par défaut dans les projets .NET Core
Dans le cadre du passage au format *csproj* dans les dernières versions du SDK, nous avons déplacé les inclusions et exclusions par défaut pour les éléments de compilation et les ressources incorporées dans les fichiers de propriétés du SDK. Cela signifie que vous n’avez plus besoin de spécifier ces éléments dans votre fichier projet. 

La principale raison de cette modification est de réduire l’encombrement de votre fichier projet. Les valeurs par défaut qui sont présentes dans le SDK doivent couvrir la plupart des cas d’utilisation courants, il est donc inutile de les répéter dans chaque projet que vous créez. Il en résulte des fichiers projet moins volumineux qui sont beaucoup plus faciles à comprendre et à modifier à la main, si nécessaire. 

Le tableau suivant montre les éléments et les modèles [Glob](https://en.wikipedia.org/wiki/Glob_(programming)) inclus et exclus dans le SDK : 

| Élément           | Inclure Glob                              | Exclure Glob                                                  | Supprimer Glob                |
|-------------------|-------------------------------------------|---------------------------------------------------------------|----------------------------|
| Compile           | \*\*/\*.cs (ou autres extensions de langage) | \*\*/\*.user ;  \*\*/\*.\*proj ;  \*\*/\*.sln ;  \*\*/\*.vssscc  | N/A                        |
| EmbeddedResource  | \*\*/\*.resx                              | \*\*/\*.user ; \*\*/\*.\*proj ; \*\*/\*.sln ; \*\*/\*.vssscc     | N/A                        |
| Aucun.              | \*\*/\*                                   | \*\*/\*.user ; \*\*/\*.\*proj ; \*\*/\*.sln ; \*\*/\*.vssscc     | - \*\*/\*.cs ; \*\*/\*.resx |

Si vous avez des modèles Glob dans votre projet et que vous essayez de le générer à l’aide du dernier SDK, vous obtenez l’erreur suivante :

> Des éléments de compilation en double ont été inclus. Le SDK .NET inclut des éléments de compilation de votre répertoire de projet par défaut. Vous pouvez supprimer ces éléments de votre fichier projet ou définir la propriété 'EnableDefaultCompileItems' sur 'false' si vous voulez explicitement les inclure dans votre fichier projet. 

Pour contourner cette erreur, vous pouvez supprimer les éléments `Compile` explicites qui correspondent à ceux répertoriés dans le tableau précédent ou vous pouvez définir la propriété `<EnableDefaultCompileItems>` sur `false`, comme ceci :

```xml
<PropertyGroup>
    <EnableDefaultCompileItems>false</EnableDefaultCompileItems>
</PropertyGroup>
```
La définition de cette propriété sur `false` remplace l’inclusion implicite et le comportement est rétabli à celui des SDK précédents dans lesquels vous deviez spécifier les modèles Glob par défaut dans votre projet. 

Ce changement ne modifie pas le mécanisme principal des autres inclusions. Toutefois, si vous voulez, par exemple, spécifier certains fichiers à publier avec votre application, vous pouvez toujours utiliser les mécanismes connus dans *csproj* correspondants (par exemple, l’élément `<Content>`).

`<EnableDefaultCompileItems>` désactive uniquement les modèles Glob `Compile`, mais n’affecte pas les autres modèles Glob, comme le modèle Glob implicite `None`, qui s’applique également aux éléments \*.cs. Par conséquent, **l’Explorateur de solutions** continue d’afficher des éléments \*.cs dans le cadre du projet, inclus en tant qu’éléments `None`. De la même façon, vous pouvez utiliser `<EnableDefaultNoneItems>` pour désactiver le modèle Glob implicite `None`.

Pour désactiver **tous les modèles Glob implicites**, vous pouvez affecter à la propriété `<EnableDefaultItems>` la valeur `false` comme dans l’exemple suivant :
```xml
<PropertyGroup>
    <EnableDefaultItems>false</EnableDefaultItems>
</PropertyGroup>
```

### <a name="recommendation"></a>Recommandation
Avec csproj, nous vous recommandons de supprimer les modèles Glob par défaut de votre projet et d’ajouter uniquement des chemins de fichier avec des modèles Glob pour les artefacts dont votre application/bibliothèque a besoin dans différents scénarios (par exemple, runtime et mise en package NuGet).

## <a name="how-to-see-the-whole-project-as-msbuild-sees-it"></a>Comment afficher la totalité du projet tel qu’il est perçu par MSBuild ?

Même si ces modifications csproj simplifient considérablement les fichiers projet, vous pouvez souhaiter voir le projet entièrement développé tel qu’il est perçu par MSBuild une fois le kit SDK et ses cibles inclus. Prétraitez le projet avec [le commutateur `/pp`](/visualstudio/msbuild/msbuild-command-line-reference#preprocess) de la commande [`dotnet msbuild`](dotnet-msbuild.md), qui affiche les fichiers qui sont importés, leurs sources et leurs contributions à la build sans réellement générer le projet :

`dotnet msbuild /pp:fullproject.xml`

Si le projet comporte plusieurs frameworks cibles, les résultats de la commande ne doivent se concentrer que sur un seul d'entre eux en le spécifiant en tant que propriété MSBuild :

`dotnet msbuild /p:TargetFramework=netcoreapp2.0 /pp:fullproject.xml`

## <a name="additions"></a>Ajouts

### <a name="sdk-attribute"></a>Attribut Sdk 
L’élément `<Project>` du fichier *.csproj* a un nouvel attribut nommé `Sdk`. `Sdk` spécifie le SDK à utiliser par le projet. Le SDK, comme le décrit le [document de superposition](cli-msbuild-architecture.md), est un ensemble de [tâches](/visualstudio/msbuild/msbuild-tasks) et de [cibles](/visualstudio/msbuild/msbuild-targets) MSBuild pouvant générer du code .NET Core. Nous fournissons deux principaux SDK dans les outils .NET Core :

1. Le SDK .NET Core avec l’ID `Microsoft.NET.Sdk`
2. Le SDK .NET Core avec l’ID `Microsoft.NET.Sdk.Web`

Vous devez définir l’attribut `Sdk` sur un de ces ID pour l’élément `<Project>` afin d’utiliser les outils .NET Core et générer votre code. 

### <a name="packagereference"></a>PackageReference
Élément qui spécifie une dépendance NuGet dans le projet. L’attribut `Include` spécifie l’ID du package. 

```xml
<PackageReference Include="<package-id>" Version="" PrivateAssets="" IncludeAssets="" ExcludeAssets="" />
```

#### <a name="version"></a>Version
`Version` spécifie la version du package à restaurer. L’attribut respecte les règles du schéma de [contrôle de version de NuGet](/nuget/create-packages/dependency-versions#version-ranges). Le comportement par défaut est une correspondance exacte entre les versions. Par exemple, la spécification `Version="1.2.3"` est équivalente à la notation `[1.2.3]` de NuGet pour la version du package 1.2.3 précisément.

#### <a name="includeassets-excludeassets-and-privateassets"></a>IncludeAssets, ExcludeAssets et PrivateAssets
L’attribut `IncludeAssets` spécifie quelles ressources appartenant au package spécifié par l’élément `<PackageReference>` doivent être utilisées. 

L’attribut `ExcludeAssets` spécifie quelles ressources appartenant au package spécifié par l’élément `<PackageReference>` ne doivent pas être utilisées.

L’attribut `PrivateAssets` spécifie quelles ressources appartenant au package spécifié par l’élément `<PackageReference>` doivent être utilisées, mais sans être reprises dans le projet suivant. 

> [!NOTE]
> `PrivateAssets` est équivalent à l’élément *project.json*/*xproj* `SuppressParent`.

Ces attributs peuvent contenir un ou plusieurs des éléments suivants :

* `Compile` : Le contenu du dossier lib est disponible pour la compilation.
* `Runtime` : Le contenu du dossier runtime est distribué.
* `ContentFiles` : Le contenu du dossier *contentfiles* est utilisé.
* `Build` : Les propriétés/cibles du dossier de génération sont utilisées.
* `Native` : Le contenu des ressources natives est copié dans le dossier de sortie de l’exécution.
* `Analyzers` : Les analyseurs sont utilisés.

Sinon, l’attribut peut contenir :

* `None` : Aucune ressource n’est utilisée.
* `All` : Toutes les ressources sont utilisées.

### <a name="dotnetclitoolreference"></a>DotNetCliToolReference
L’élément `<DotNetCliToolReference>` spécifie l’outil CLI que l’utilisateur veut restaurer dans le contexte du projet. Il constitue une alternative au nœud `tools` dans *project.json*. 

```xml
<DotNetCliToolReference Include="<package-id>" Version="" />
```

#### <a name="version"></a>Version
`Version` spécifie la version du package à restaurer. L’attribut respecte les règles du schéma de [contrôle de version de NuGet](/nuget/create-packages/dependency-versions#version-ranges). Le comportement par défaut est une correspondance exacte entre les versions. Par exemple, la spécification `Version="1.2.3"` est équivalente à la notation `[1.2.3]` de NuGet pour la version du package 1.2.3 précisément.

### <a name="runtimeidentifiers"></a>RuntimeIdentifiers
L’élément `<RuntimeIdentifiers>` permet de spécifier une liste délimitée par des points-virgules d’[identificateurs de runtime (RID)](../rid-catalog.md) pour le projet. Les RID permettent de publier des déploiements autonomes. 

```xml
<RuntimeIdentifiers>win10-x64;osx.10.11-x64;ubuntu.16.04-x64</RuntimeIdentifiers>
```

### <a name="runtimeidentifier"></a>RuntimeIdentifier
L’élément `<RuntimeIdentifier>` vous permet de spécifier un seul [identificateur de runtime (RID)](../rid-catalog.md) pour le projet. Les RID permettent de publier un déploiement autonome. 

```xml
<RuntimeIdentifier>ubuntu.16.04-x64</RuntimeIdentifier>
```

### <a name="packagetargetfallback"></a>PackageTargetFallback 
L’élément `<PackageTargetFallback>` vous permet de spécifier un jeu de cibles compatibles à utiliser lors de la restauration des packages. Il est conçu pour permettre aux packages qui utilisent le [moniker du framework cible](/nuget/schema/target-frameworks) dotnet de fonctionner avec les packages qui ne déclarent pas de moniker du framework cible dotnet. Si votre projet utilise le moniker du framework cible dotnet, tous les packages dont il dépend doivent également avoir un moniker du framework cible dotnet, sauf si vous ajoutez `<PackageTargetFallback>` à votre projet pour permettre aux plateformes autres que dotnet d’être compatibles avec dotnet. 

L’exemple suivant fournit les solutions de secours pour toutes les cibles dans votre projet : 

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win8+wpa81+wp8
</PackageTargetFallback >
```

L’exemple suivant spécifie les solutions de secours uniquement pour la cible `netcoreapp1.0` :

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netcoreapp1.0'">
    $(PackageTargetFallback);portable-net45+win8+wpa81+wp8
</PackageTargetFallback >
```

## <a name="nuget-metadata-properties"></a>Propriétés de métadonnées NuGet
Avec le passage à MSbuild, nous avons transféré les métadonnées d’entrée utilisées lors de la compression d’un package NuGet des fichiers *project.json* vers les fichiers *csproj*. Les entrées sont des propriétés MSBuild qui doivent donc être placées dans un groupe `<PropertyGroup>`. Voici la liste des propriétés qui sont utilisées comme entrées dans le processus de compression lors de l’utilisation de la commande `dotnet pack` ou de la cible MSBuild `Pack` qui fait partie du SDK. 

### <a name="ispackable"></a>IsPackable
Valeur booléenne qui spécifie si le projet peut être compressé. La valeur par défaut est `true`. 

### <a name="packageversion"></a>PackageVersion
Spécifie la version du package obtenu. Accepte toutes les formes de la chaîne de version NuGet. La valeur par défaut est la valeur de `$(Version)`, autrement dit, de la propriété `Version` dans le projet. 

### <a name="packageid"></a>PackageId
Spécifie le nom du package obtenu. Si non spécifié, l’opération `pack` utilise par défaut le `AssemblyName` ou le nom du répertoire comme nom du package. 

### <a name="title"></a>Titre
Titre convivial du package, généralement utilisé dans les affichages de l’interface utilisateur comme sur nuget.org et dans le gestionnaire de package de Visual Studio. Si non spécifié, l’ID de package est utilisé à la place.

### <a name="authors"></a>Auteurs
Liste séparée par des points-virgules des auteurs de packages, qui correspondent aux noms de profil sur nuget.org. Ceux-ci sont affichés dans la galerie NuGet sur nuget.org et servent à croiser les références des packages de mêmes auteurs.

### <a name="description"></a>Description
Description longue du package pour l’affichage de l’interface utilisateur.

### <a name="copyright"></a>Copyright
Détails de copyright pour le package.

### <a name="packagerequirelicenseacceptance"></a>PackageRequireLicenseAcceptance
Valeur booléenne qui spécifie si le client doit inviter l’utilisateur à accepter la licence du package avant d’installer le package. La valeur par défaut est `false`.

### <a name="packagelicenseurl"></a>PackageLicenseUrl
URL vers la licence applicable au package.

### <a name="packageprojecturl"></a>PackageProjectUrl
URL de la page d’accueil du package, souvent affichée dans l’interface utilisateur ainsi que sur nuget.org.

### <a name="packageiconurl"></a>PackageIconUrl
URL d’une image 64 x 64 avec un arrière-plan transparent à utiliser comme icône pour le package dans l’affichage de l’interface utilisateur.

### <a name="packagereleasenotes"></a>PackageReleaseNotes
Notes de publication du package.

### <a name="packagetags"></a>PackageTags
Liste de balises séparées par un point-virgule qui désigne le package.

### <a name="packageoutputpath"></a>PackageOutputPath
Détermine le chemin de sortie dans lequel le package compressé est déposé. La valeur par défaut est `$(OutputPath)`. 

### <a name="includesymbols"></a>IncludeSymbols
Cette valeur booléenne indique si le package doit créer un package de symboles supplémentaire quand le projet est compressé. Ce package a une extension *.symbols.nupkg* et copie les fichiers PDB avec la DLL et d’autres fichiers de sortie.

### <a name="includesource"></a>IncludeSource
Cette valeur booléenne indique si le processus de compression doit créer un package source. Le package source contient le code source de la bibliothèque ainsi que les fichiers PDB. Les fichiers sources sont placés dans le répertoire `src/ProjectName` dans le fichier de package obtenu. 

### <a name="istool"></a>IsTool
Spécifie si tous les fichiers de sortie sont copiés dans le dossier *tools* au lieu du dossier *lib*. Notez que cela est différent d’un `DotNetCliTool` qui est spécifié en définissant `PackageType` dans le fichier *.csproj*.

### <a name="repositoryurl"></a>RepositoryUrl
Spécifie l’URL du dépôt où réside le code source du package et/ou à partir de laquelle il est généré. 

### <a name="repositorytype"></a>RepositoryType
Spécifie le type de dépôt. La valeur par défaut est « git ». 

### <a name="nopackageanalysis"></a>NoPackageAnalysis
Spécifie que le pack ne doit pas exécuter d’analyse du package après sa génération.

### <a name="minclientversion"></a>MinClientVersion
Spécifie la version minimale du client NuGet qui peut installer ce package, appliquée par nuget.exe et le gestionnaire de package Visual Studio.

### <a name="includebuildoutput"></a>IncludeBuildOutput
Ces valeurs booléennes spécifient si les assemblys de sortie de génération doivent être compressés dans le fichier *.nupkg* ou non.

### <a name="includecontentinpack"></a>IncludeContentInPack
Cette valeur booléenne indique si tous les éléments qui ont un type `Content` sont automatiquement inclus dans le package obtenu. La valeur par défaut est `true`. 

### <a name="buildoutputtargetfolder"></a>BuildOutputTargetFolder
Spécifie le dossier où placer les assemblys de sortie... Les assemblys de sortie (et les autres fichiers de sortie) sont copiés dans les dossiers de leur framework respectif.

### <a name="contenttargetfolders"></a>ContentTargetFolders
Cette propriété spécifie l’emplacement par défaut où placer tous les fichiers de contenu si `PackagePath` n’est pas spécifié pour eux. La valeur par défaut est « content;contentFiles ».

### <a name="nuspecfile"></a>NuspecFile
Chemin relatif ou absolu du fichier *.nuspec* utilisé pour la compression. 

> [!NOTE]
> Si le fichier *.nuspec* est spécifié, il est utilisé **exclusivement** pour les informations de packaging et toutes les informations non utilisées dans les projets. 

### <a name="nuspecbasepath"></a>NuspecBasePath
Chemin de base pour le fichier *.nuspec*.

### <a name="nuspecproperties"></a>NuspecProperties
Liste de paires clé=valeur séparées par un point-virgule.
