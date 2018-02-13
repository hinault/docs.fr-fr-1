---
title: "Portage vers .NET Core - Bibliothèques"
description: "Découvrez comment porter des projets de bibliothèque de .NET Framework vers .NET Core."
keywords: .NET, .NET Core
author: cartermp
ms.author: mairaw
ms.date: 07/14/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: a0fd860d-d6b6-4659-b325-8a6e6f5fa4a1
ms.workload:
- dotnetcore
ms.openlocfilehash: 24c74f0396dd7bfdf19fc0e11a29110fdbf27173
ms.sourcegitcommit: cf22b29db780e532e1090c6e755aa52d28273fa6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="porting-to-net-core---libraries"></a>Portage vers .NET Core - Bibliothèques

Cet article décrit le portage de code de bibliothèque vers .NET Core dans le but de l’exécuter sur plusieurs plateformes.

## <a name="prerequisites"></a>Prérequis

Cet article suppose que vous :

- utilisez Visual Studio 2017 ou une version ultérieure
  - .NET Core n’est pas pris en charge dans les versions antérieures de Visual Studio
- comprenez le [processus de portage recommandé](index.md) ;
- avez résolu les problèmes des [dépendances tierces](third-party-deps.md).

Vous devez également vous familiariser avec le contenu des rubriques suivantes :

[.NET Standard](~/docs/standard/net-standard.md)   
Cette rubrique décrit la spécification formelle des API .NET qui sont destinées à être mises à disposition sur toutes les implémentations .NET.

[Packages, métapackages et frameworks](~/docs/core/packages.md)   
Cet article explique comment .NET Core définit et utilise les packages et comment ceux-ci prennent en charge le code qui s’exécute sur plusieurs implémentations .NET.

[Développer des bibliothèques avec des outils multiplateformes](~/docs/core/tutorials/libraries.md)   
Cette rubrique explique comment écrire des bibliothèques pour .NET à l’aide d’outils CLI multiplateformes.

[Ajouts au format *csproj* pour .NET Core](~/docs/core/tools/csproj.md)   
Cet article décrit les modifications qui ont été apportées au fichier projet dans le cadre du passage à *csproj* et à MSBuild.

[Porter du code vers .NET Core - Analyser les dépendances tierces](~/docs/core/porting/third-party-deps.md)   
Cette rubrique décrit la portabilité des dépendances tierces et explique quoi faire quand une dépendance de package NuGet ne s’exécute pas sur .NET Core.

## <a name="net-framework-technologies-unavailable-on-net-core"></a>Technologies .NET Framework non disponibles sur .NET Core

Certaines technologies mises à la disposition des bibliothèques .NET Framework ne sont pas utilisables avec .NET Core, notamment les AppDomains, Remoting, la sécurité d’accès du code (CAS) et la transparence de la sécurité. Si vos bibliothèques reposent sur une ou plusieurs de ces technologies, envisagez les autres approches décrites ci-dessous. Pour plus d’informations sur la compatibilité des API, l’équipe CoreFX conserve la [Liste des modifications de comportement/arrêts de compatibilité et des API déconseillées/héritées](https://github.com/dotnet/corefx/wiki/ApiCompat) sur GitHub.

Le fait qu’une technologie ou une API ne soit pas implémentée pour le moment ne signifie pas que l’absence de prise en charge soit intentionnelle. Soumettez un problème dans les [problèmes de référentiel dotnet/corefx](https://github.com/dotnet/corefx/issues) sur GitHub pour demander des API et des technologies spécifiques. Les [demandes de portage dans les problèmes](https://github.com/dotnet/corefx/labels/port-to-core) sont marquées avec l’étiquette `port-to-core`.

### <a name="appdomains"></a>AppDomains

Les AppDomains isolent les applications les unes des autres. Ils requièrent la prise en charge du runtime et sont généralement assez onéreux. Ils ne sont pas implémentés dans .NET Core. Nous ne prévoyons pas d’ajouter cette fonctionnalité par la suite. Pour l’isolation du code, nous recommandons d’utiliser des processus distincts ou des conteneurs à la place. Pour le chargement dynamique d’assemblys, nous recommandons la nouvelle classe <xref:System.Runtime.Loader.AssemblyLoadContext>.

Pour faciliter la migration du code à partir de .NET Framework, nous avons exposé quelques-unes des API <xref:System.AppDomain> dans .NET Core. Certaines API fonctionnent normalement (par exemple, <xref:System.AppDomain.UnhandledException?displayProperty=nameWithType>), certains membres ne font rien (par exemple, <xref:System.AppDomain.SetCachePath%2A>) et d’autres lèvent <xref:System.PlatformNotSupportedException> (par exemple, <xref:System.AppDomain.CreateDomain%2A>). Vérifiez les types que vous utilisez par rapport à la [source de référence `System.AppDomain`](https://github.com/dotnet/corefx/blob/master/src/System.Runtime.Extensions/src/System/AppDomain.cs) dans le [référentiel GitHub dotnet/corefx](https://github.com/dotnet/corefx), en veillant à sélectionner la branche correspondant à la version que vous avez implémentée.

### <a name="remoting"></a>Communication à distance

.NET Remoting a été identifié comme architecture problématique. Elle est utilisée pour la communication entre AppDomains, qui n’est plus prise en charge. Par ailleurs, Remoting requiert la prise en charge du runtime, dont la maintenance est coûteuse. C’est pourquoi .NET Remoting n’est pas pris en charge sur .NET Core, et nous ne prévoyons pas d’ajouter sa prise en charge à l’avenir.

Pour la communication entre processus, envisagez de mettre en place des mécanismes de communication interprocessus (IPC) à la place de Remoting, par exemple la classe <xref:System.IO.Pipes> ou la classe <xref:System.IO.MemoryMappedFiles.MemoryMappedFile>.

Pour la communication entre ordinateurs, utilisez plutôt une solution réseau. Choisissez de préférence un protocole de texte brut à faible charge, par exemple HTTP. Le [serveur web Kestrel](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel), utilisé par ASP.NET Core, est une possibilité. Vous pouvez également envisager d’utiliser <xref:System.Net.Sockets> pour les scénarios réseau sur différents ordinateurs. Pour plus d’options, consultez la page [Projets de développement .NET open source : messagerie](https://github.com/Microsoft/dotnet/blob/master/dotnet-developer-projects.md#messaging).

### <a name="code-access-security-cas"></a>sécurité d'accès du code (CAS, Code Access Security)

Le bac à sable (sandbox), qui repose sur le runtime ou l’infrastructure pour limiter les ressources utilisées ou exécutées par une application gérée ou une bibliothèque, [n’est pas pris en charge sur .NET Framework](~/docs/framework/misc/code-access-security.md) ni, par conséquent, sur .NET Core. Nous pensons qu’il y a trop de cas dans .NET Framework et le runtime où une élévation des privilèges se produit pour continuer à traiter la sécurité d’accès du code comme une limite de sécurité. En outre, la sécurité du code complique l’implémentation et a souvent a des implications en matière de performances d’exactitude pour les applications qui ne prévoient pas de l’utiliser.

Utilisez les limites de sécurité fournies par le système d’exploitation, comme la virtualisation, les conteneurs ou des comptes d’utilisateurs, pour exécuter des processus avec l’ensemble de privilèges le plus petit possible.

### <a name="security-transparency"></a>Transparence de la sécurité

Tout comme la sécurité d’accès du code, la transparence de la sécurité permet de séparer le code sandbox du code critique de sécurité d’une manière déclarative, mais [n’est plus prise en charge en tant que limite de sécurité](~/docs/framework/misc/security-transparent-code.md). Cette fonctionnalité est très utilisée par Silverlight. 

Utilisez les limites de sécurité fournies par le système d’exploitation, comme la virtualisation, les conteneurs ou des comptes d’utilisateurs, pour exécuter des processus avec l’ensemble de privilèges le plus petit possible.

### <a name="globaljson"></a>global.json

Le fichier *global.json* est un fichier facultatif qui permet de définir la version des outils .NET Core d’un projet. Si vous utilisez des builds nocturnes de .NET Core et que vous souhaitez spécifier une version précise du Kit SDK, spécifiez la version avec un fichier *global.json*. Il se trouve généralement dans le répertoire de travail actif ou un de ses répertoires parents. 

```json
{
  "sdk": {
    "version": "2.1.0-preview1-006491"
  }
}
```

## <a name="converting-a-pcl-project"></a>Convertir un projet PCL

Vous pouvez convertir les cibles d’un projet PCL vers .NET Standard en chargeant la bibliothèque dans Visual Studio 2017 et en suivant les étapes ci-dessous :

1. Cliquez avec le bouton droit sur le fichier projet et sélectionnez **Propriétés**.
1. Sous **Bibliothèque**, sélectionnez **Standard de la plateforme .NET cible**.

Si vos packages prennent en charge NuGet 3.0, le projet recible vers .NET Standard.

Si vos packages ne prennent pas en charge NuGet 3.0, une boîte de dialogue de Visual Studio vous demandera de désinstaller vos packages actuels. Si vous recevez cette notification, suivez les étapes ci-dessous :

1. Cliquez avec le bouton droit sur le projet et sélectionnez **Gérer les packages NuGet**.
1. Notez les packages du projet.
1. Désinstallez les packages un par un.
1. Vous devrez peut-être redémarrer Visual Studio pour terminer le processus de désinstallation. Dans ce cas, un bouton **Redémarrer** vous est présenté dans la fenêtre **Gestionnaire de package NuGet**.
1. Lorsque le projet se recharge, il cible .NET Standard. Ajoutez les packages que vous avez été invité à désinstaller.

## <a name="retargeting-your-net-framework-code-to-net-framework-462"></a>Recibler du code .NET Framework vers .NET Framework 4.6.2

Si votre code ne cible pas .NET Framework 4.6.2, nous vous recommandons de le recibler vers .NET Framework 4.6.2. Cela permet de garantir la disponibilité des dernières API de remplacement pour les cas où .NET Standard ne prend pas en charge les API existantes.

Pour chacun de vos projets dans Visual Studio que vous voulez porter, procédez comme suit :

1. Cliquez avec le bouton droit sur le projet et sélectionnez Propriétés.
1. Dans la liste déroulante **Version cible de .NET Framework**, sélectionnez **.NET Framework 4.6.2**.
1. Recompilez vos projets.

Dans la mesure où vos projets ciblent maintenant .NET Framework 4.6.2, utilisez cette version de .NET Framework comme base pour le portage du code.

## <a name="determining-the-portability-of-your-code"></a>Déterminer la portabilité du code

L’étape suivante consiste à exécuter l’outil API Portability Analyzer (ApiPort) pour générer un rapport de portabilité à des fins d’analyse.

Vérifiez que vous comprenez bien [l’outil API Portability Analyzer (ApiPort)](../../standard/analyzers/portability-analyzer.md) et que vous savez générer des rapports de portabilité pour cibler .NET Core. La façon de faire est susceptible de varier selon vos besoins et vos préférences personnelles. Voici différentes approches. Vous pourrez être amené à combiner les étapes de ces approches en fonction de la structuration de votre code.

### <a name="dealing-primarily-with-the-compiler"></a>Se concentrer principalement sur le compilateur

Cette approche peut être la meilleure pour les petits projets ou les projets qui n’utilisent pas beaucoup d’API du .NET Framework. Elle est simple :

1. Exécutez ApiPort sur votre projet (facultatif). Si vous exécutez ApiPort, prenez connaissance du rapport sur les problèmes que vous devrez résoudre.
1. Recopiez tout votre code dans un nouveau projet .NET Core.
1. Pendant que vous vous référez au rapport de portabilité (s’il a été généré), résolvez les erreurs du compilateur jusqu’à ce que le projet se compile intégralement.

Bien qu’elle ne soit pas structurée, l’approche centrée sur le code permet souvent de résoudre les problèmes rapidement ; c’est peut-être la meilleure pour les projets et les bibliothèques de petite taille. Un projet contenant uniquement des modèles de données pourrait constituer un candidat idéal à cette approche.

### <a name="staying-on-the-net-framework-until-portability-issues-are-resolved"></a>Rester sur .NET Framework jusqu’à ce que les problèmes de portabilité soient résolus

Cette approche est peut-être la meilleure si vous préférez avoir du code compilable pendant tout le processus. L’approche est la suivante :

1. Exécutez ApiPort sur un projet.
1. Résolvez les problèmes en utilisant différentes API portables.
1. Notez toutes les zones où vous n’avez pas la possibilité d’utiliser une solution de rechange directe.
1. Répétez les étapes précédentes pour tous les projets à porter jusqu’à ce que vous ayez la certitude que tous sont prêts à être copiés dans un nouveau projet .NET Core.
1. Copiez le code dans un nouveau projet .NET Core.
1. Résolvez tous les problèmes pour lesquels vous avez noté qu’il n’existe pas de solution de rechange directe.

Cette approche prudente est plus structurée que celle qui consiste à résoudre simplement les erreurs de compilation, mais elle reste relativement centrée sur le code et présente l’avantage de toujours conserver du code compilable. Les moyens de résoudre les problèmes qui n’ont pas pu être traités en utilisant simplement une autre API peuvent varier considérablement. Il peut être nécessaire de développer un plan plus complet pour certains projets, ce qui est couvert par l’approche suivante.

### <a name="developing-a-comprehensive-plan-of-attack"></a>Développer un plan d’attaque complet

Cette approche est peut-être la meilleure pour les projets complexes et de grande envergure, dans lesquels il peut être nécessaire de restructurer le code ou de réécrire complètement certains passages pour prendre en charge .NET Core. L’approche est la suivante :

1. Exécutez ApiPort sur un projet.
1. Déterminez les endroits où chaque type non portable est utilisé et l’impact sur la portabilité globale.
   - Déterminez la nature de ces types. Sont-ils peu nombreux mais fréquemment utilisés ? Sont-ils nombreux mais rarement utilisés ? Leur utilisation est-elle concentrée ou est-elle répartie à travers tout le code ?
   - Est-il facile d’isoler le code non portable, afin de le traiter plus facilement ?
   - Faut-il refactoriser le code ?
   - Pour les types qui ne sont pas portables, y a-t-il des API alternatives qui accomplissent la même tâche ? Par exemple, si vous utilisez la classe <xref:System.Net.WebClient>, vous pouvez peut-être utiliser la classe <xref:System.Net.Http.HttpClient> à la place.
   - Existe-t-il d’autres API portables permettant d’accomplir une tâche, même s’il ne s’agit pas d’un remplacement immédiat ? Par exemple, si vous utilisez <xref:System.Xml.Schema.XmlSchema> pour analyser le code XML, mais que vous n’avez pas besoin de la détection de schéma XML, vous pouvez utiliser les API <xref:System.Xml.Linq> et implémenter l’analyse par vous-même, plutôt que de dépendre d’une API.
1. Si vous avez des assemblys difficiles à porter, est-il intéressant de les laisser sur le .NET Framework pour l’instant ? Voici quelques éléments à prendre en compte :
   - Certaines des fonctionnalités de votre bibliothèque pourraient ne pas être compatibles avec .NET Core, car elles dépendent trop des fonctionnalités propres à .NET Framework ou à Windows. Est-il intéressant de laisser cette fonctionnalité de côté pour l’instant et de publier une version .NET Core de votre bibliothèque avec moins de fonctionnalités à titre temporaire, jusqu’à ce que les ressources nécessaires pour porter les fonctionnalités soient disponibles ?
   - Une refactorisation serait-elle utile ?
1. Est-il raisonnable d’écrire votre propre implémentation d’une API .NET Framework non disponible ?
   Vous pouvez envisager de copier, de modifier et d’utiliser du code provenant de la [Source de référence de .NET Framework](https://github.com/Microsoft/referencesource). Le code source de référence est sous [licence du MIT](https://github.com/Microsoft/referencesource/blob/master/LICENSE.txt), ce qui vous laisse la liberté d’utiliser la source comme base pour votre propre code. Veillez simplement à mentionner correctement ce qui est propriété de Microsoft dans votre code.
1. Répétez ce processus si nécessaire pour les différents projets.
 
La phase d’analyse peut prendre un certain temps, selon la taille de votre code base. Passer du temps sur cette phase pour déterminer précisément l’étendue des modifications nécessaires et pour développer un plan fait en général gagner du temps à long terme, en particulier en cas de code base complexe.

Votre plan peut impliquer des modifications importantes à votre code base tout en continuant à cibler le .NET Framework 4.6.2, ce qui fait de ceci une version plus structurée de l’approche précédente. La mise en œuvre du plan dépend du code base.

### <a name="mixing-approaches"></a>Combiner les approches

Il est probable que vous allez combiner les approches ci-dessus de façon différente selon les projets. Vous devez faire ce qui a le plus de sens pour vous et pour votre code base.

## <a name="porting-your-tests"></a>Porter les tests

La meilleure façon de vérifier que tout fonctionne quand vous avez porté votre code est de tester votre code quand vous l’avez porté sur .NET Core. Pour cela, vous devez utiliser une infrastructure de test qui génère et exécute des tests pour .NET Core. Vous avez actuellement trois options :

- [xUnit](https://xunit.github.io/)
  * [Prise en main](http://xunit.github.io/docs/getting-started-dotnet-core.html)
  * [Outil pour convertir un projet MSTest en xUnit](https://github.com/dotnet/codeformatter/tree/master/src/XUnitConverter)
- [NUnit](http://www.nunit.org/)
  * [Prise en main](https://github.com/nunit/docs/wiki/Installation)
  * [Billet de blog sur la migration de MSTest vers NUnit](http://www.florian-rappl.de/News/Page/275/convert-mstest-to-nunit)
- [MSTest](https://docs.microsoft.com/visualstudio/test/unit-test-basics)

## <a name="recommended-approach-to-porting"></a>Approche recommandée du portage

En définitive, le travail de portage dépend fortement de la structuration du code .NET Framework. Il est recommandé de commencer par la *base* de la bibliothèque, qui représente la composante essentielle du code. Il peut s’agir de modèles de données ou d’autres classes et méthodes fondamentales utilisées directement ou indirectement par tout le reste.

1. Portez le projet de test qui teste la couche en cours de portage de votre bibliothèque.
1. Copiez la base de votre bibliothèque dans un nouveau projet .NET Core et sélectionnez la version de .NET Standard que vous voulez prendre en charge.
1. Apportez les modifications nécessaires pour obtenir le code à compiler. Il est possible que la plupart nécessitent l’ajout de dépendances de package NuGet à votre fichier *csproj*.
1. Exécutez les tests et procédez aux ajustements nécessaires.
1. Sélectionnez la couche suivante de code à porter et répétez les étapes précédentes.

Si vous commencez par la base de votre bibliothèque et que vous vous déplacez vers l’extérieur en testant chaque couche au fur et à mesure, le portage devient un processus systématique où les problèmes sont isolés sur une seule couche de code à la fois.
