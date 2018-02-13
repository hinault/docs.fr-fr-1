---
title: "Télémétrie des outils CLI .NET Core"
description: "Découvrez les fonctionnalités de télémétrie des outils .NET Core, qui collectent des informations d’utilisation à des fins d’analyse, les types de données collectées et comment désactiver la télémétrie."
keywords: ".NET,.NET Core,télémétrie"
author: richlander
ms.author: mairaw
ms.date: 08/04/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 480df976-7568-4df4-9d26-9911357b5a31
ms.workload:
- dotnetcore
ms.openlocfilehash: 9a78ec370fd53260f26a5d8c15707a5d611e458f
ms.sourcegitcommit: be1fb5d9447ad459bef22b91a91c72e3e0b2d916
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/09/2018
---
# <a name="net-core-cli-tools-telemetry"></a>Télémétrie des outils CLI .NET Core

Le [SDK .NET Core](index.md) inclut une [fonctionnalité de télémétrie](https://github.com/dotnet/cli/pull/2145) qui recueille des informations d’utilisation. Il est important pour l’équipe .NET de comprendre la façon dont les outils sont utilisés, afin de pouvoir les améliorer. Pour plus d’informations, consultez les [enseignements tirés de la fonctionnalité de télémétrie du SDK .NET Core](https://blogs.msdn.microsoft.com/dotnet/2017/07/21/what-weve-learned-from-net-core-sdk-telemetry/).

Les données collectées sont anonymes et publiées sous forme regroupée en vue d’être utilisées par Microsoft et la communauté, sous la [licence Creative Commons Attribution](https://creativecommons.org/licenses/by/4.0/). 

## <a name="scope"></a>Portée

La commande `dotnet` permet de lancer des applications et l’interface CLI .NET Core. La commande `dotnet` ne permet pas de collecter des données de télémétrie. Les commandes de l’interface CLI .NET Core exécutées par la commande `dotnet` collectent les données de télémétrie.

La télémétrie *n’est pas activée* quand vous utilisez la commande `dotnet` sans commande attachée :

- `dotnet`
- `dotnet [path-to-app]`

La télémétrie *est activée* quand vous utilisez les [commandes de l’interface CLI .NET Core](index.md), telles que les suivantes :

- `dotnet build`
- `dotnet pack`
- `dotnet restore`
- `dotnet run`


## <a name="behavior"></a>Comportement

La fonctionnalité de télémétrie de l’interface CLI .NET Core est activée par défaut. Pour ne pas l’utiliser, définissez la variable d’environnement `DOTNET_CLI_TELEMETRY_OPTOUT` sur `1` ou `true`.

## <a name="data-points"></a>Points de données

La fonctionnalité recueille les données suivantes :

- horodatage de l’appel&#8224;
- Commande appelée (par exemple, « build »)&#8224;
- Adresse IP de trois octets utilisée pour déterminer l’emplacement géographique&#8224;
- `ExitCode` de la commande
- Exécuteur de tests (pour les projets de test)
- Système d’exploitation et version&#8224;
- Si des ID d’exécution se trouvent sous le nœud runtimes
- Version du SDK .NET Core&#8224;

&#8224;Cette métrique est publiée.

À compter du SDK .NET Core 2.0, de nouveaux points de données sont collectés :

- Arguments et options de la commande `dotnet` : seuls les arguments et options connus sont collectés (pas les chaînes arbitraires).
- Si le SDK est en cours d’exécution dans un conteneur.
- Frameworks cibles.
- Adresse MAC hachée : ID unique et anonyme chiffré (SHA256) pour une machine. Cette métrique n’est pas publiée.
- Répertoire de travail actuel haché.

La fonctionnalité ne collecte pas les informations personnelles, telles que les noms d’utilisateurs et les adresses e-mail. Elle n’analyse pas votre code et n’extrait pas de données sensibles au niveau du projet, telles que le nom, le dépôt ou l’auteur. Les données sont envoyées en toute sécurité à des serveurs Microsoft à l’aide de la technologie [Microsoft Azure Application Insights](https://azure.microsoft.com/services/application-insights/), stockées à un emplacement dont l’accès est strictement limité et publiées conformément à des contrôles de sécurité stricts à partir de systèmes [Azure Storage](https://azure.microsoft.com/services/storage/) sécurisés.

Nous souhaitons savoir comment vous utilisez les outils et s’ils fonctionnent correctement, et non ce que vous créez avec les outils. Si vous pensez que la fonctionnalité de télémétrie collecte des données sensibles ou que nous gérons des données de manière non sécurisée ou incorrecte, [soumettez un problème dans la page des problèmes du dépôt dotnet/cli](https://github.com/dotnet/cli/issues) afin que nous effectuions un examen plus approfondi.

## <a name="published-data"></a>Données publiées

Les données publiées sont disponibles tous les trimestres et sont répertoriées dans la page [.NET Core SDK Usage Data](https://github.com/dotnet/core/blob/master/release-notes/cli-usage-data.md) (Données d’utilisation du SDK .NET Core). Les colonnes d’un fichier de données sont les suivantes :
- Horodateur
- Occurrences&#8224;
- Commande
- Geography&#8225;
- OSFamily
- RuntimeID
- OSVersion
- SDKVersion

&#8224;La colonne *Occurrences* totalise le nombre d’utilisations de la commande concernée pour les métriques de la ligne donnée le jour indiqué. 

&#8225;En règle générale, la colonne *Geography* affiche le nom d’un pays. Dans certains cas, le continent Antarctica (Antarctique) apparaît dans cette colonne si .NET Core est utilisé dans ce continent ou que les données de localisation sont incorrectes.

### <a name="example"></a>Exemple

| Horodateur      | Occurrences | Commande | Geography | OSFamily | RuntimeID     | OSVersion | SDKVersion |
| -------------- | ----------- | ------- | --------- | -------- | ------------- | --------- | ---------- |
| 4/16/2017 0:00 | 8           | run     | Uganda    | Darwin   | osx.10.12-x64 | 10.12     | 1.0.1      |

### <a name="datasets"></a>Groupes de données

[2016 - T3](https://dotnetcli.blob.core.windows.net/usagedata/dotnet-cli-usage-2016-q3.tsv)  
[2016 - T4](https://dotnetcli.blob.core.windows.net/usagedata/dotnet-cli-usage-2016-q4.tsv)  
[2017 - T1](https://dotnetcli.blob.core.windows.net/usagedata/dotnet-cli-usage-2017-q1.tsv)  
[2017 - T2](https://dotnetcli.blob.core.windows.net/usagedata/dotnet-cli-usage-2017-q2.tsv)

Des jeux de données supplémentaires sont publiés à l’aide d’un format d’URL standard. Remplacez `<YEAR>` par l’année, et `<QUARTER>` par le trimestre de l’année (utilisez `1`, `2`, `3` ou `4`). Les fichiers sont au format *TSV* (valeurs séparées par une tabulation). 

```
https://dotnetcli.blob.core.windows.net/usagedata/dotnet-cli-usage-<YEAR>-q<QUARTER>.tsv
```

## <a name="license"></a>Licence

La distribution Microsoft de .NET Core est concédée sous licence avec le [CLUF de la BIBLIOTHÈQUE .NET MICROSOFT](https://aka.ms/dotnet-core-eula). Cette licence comprend la section « DATA » qui permet d’activer la télémétrie (ci-dessous).

Les [packages NuGet .NET](https://www.nuget.org/profiles/dotnetframework) utilisent la même licence, mais ne permettent pas la télémétrie (voir la section [Portée](#scope)).

> 2. DONNÉES. Le logiciel peut collecter des informations sur vous et votre utilisation du logiciel et les envoyer à Microsoft. Microsoft peut utiliser ces informations pour améliorer ses produits et services. Vous pouvez en savoir plus sur la collecte et l’utilisation des données dans la documentation d’aide et la déclaration de confidentialité http://go.microsoft.com/fwlink/?LinkId=528096. Votre utilisation du logiciel est considérée comme votre acceptation de ces pratiques.

## <a name="disclosure"></a>Divulgation d’informations

Les outils CLI .NET Core affichent le texte suivant quand vous exécutez une commande pour la première fois (par exemple, `dotnet restore`). Le texte peut varier légèrement selon la version du SDK que vous exécutez. Lors de cette première exécution, Microsoft vous informe sur la collecte de données.

```console
Welcome to .NET Core!
---------------------
Learn more about .NET Core @ https://aka.ms/dotnet-docs. Use dotnet --help to see available commands or go to https://aka.ms/dotnet-cli-docs.
 
Telemetry
--------------
The .NET Core tools collect usage data in order to improve your experience. The data is anonymous and does not include command-line arguments. The data is collected by Microsoft and shared with the community.
You can opt out of telemetry by setting a DOTNET_CLI_TELEMETRY_OPTOUT environment variable to 1 using your favorite shell.
You can read more about .NET Core tools telemetry @ https://aka.ms/dotnet-cli-telemetry.
```

## <a name="see-also"></a>Voir aussi

[What we've learned from .NET Core SDK Telemetry](https://blogs.msdn.microsoft.com/dotnet/2017/07/21/what-weve-learned-from-net-core-sdk-telemetry/) (Enseignements tirés de la fonctionnalité de télémétrie du SDK .NET Core)  
[Source de référence de télémétrie (dotnet/cli repo ; branche release/2.0.0)](https://github.com/dotnet/cli/tree/release/2.0.0/src/dotnet/Telemetry)   
[.NET Core SDK Usage Data](https://github.com/dotnet/core/blob/master/release-notes/cli-usage-data.md) (Données d’utilisation du SDK .NET Core)
