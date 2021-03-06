---
title: "Nouveautés du .NET Framework"
ms.custom: updateeachrelease
ms.date: 05/02/2017
ms.prod: .net-framework
ms.technology: dotnet-clr
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords: what's new [.NET Framework]
ms.assetid: 1d971dd7-10fc-4692-8dac-30ca308fc0fa
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: e2aa6e67fc45aa02421433a295fdbf5657e4e551
ms.sourcegitcommit: 2142a4732bb4ff519b9817db4c24a237b9810d4b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/05/2018
---
# <a name="whats-new-in-the-net-framework"></a>Nouveautés du .NET Framework
<a name="introduction"></a> Cet article résume les principales nouvelles fonctionnalités et améliorations des versions suivantes du .NET Framework :  
 
[.NET Framework 4.7.1](#v471)    
[.NET Framework 4.7](#v47)   
[.NET Framework 4.6.2](#v462)   
[.NET Framework 4.6.1](#v461)   
[.NET 2015 et .NET Framework 4.6](#v46)   
[.NET Framework 4.5.2](#v452)   
[.NET Framework 4.5.1](#v451)   
[.NET Framework 4.5](#v45)   

Cet article ne fournit pas d'informations complètes sur chacune des nouvelles fonctionnalités et peut faire l'objet de modifications. Pour obtenir des informations générales sur le .NET Framework, consultez [Prise en main](../../../docs/framework/get-started/index.md). Pour connaître les plateformes prises en charge, consultez [Configuration requise](~/docs/framework/get-started/system-requirements.md). Pour obtenir des liens de téléchargement et des instructions d’installation, consultez [Guide d’installation](../../../docs/framework/install/guide-for-developers.md).

> [!NOTE]
> L’équipe .NET Framework publie aussi des fonctionnalités hors bande avec NuGet pour étendre la prise en charge des plateformes et introduire des nouveautés, telles que les collections immuables et les types de vecteurs compatibles SIMD. Pour plus d’informations, consultez [Autres bibliothèques de classes et API](../additional-apis/index.md) et [Versions finales hors plage de .NET Framework](~/docs/framework/get-started/the-net-framework-and-out-of-band-releases.md). Consultez la [liste complète des packages NuGet](https://blogs.msdn.microsoft.com/dotnet/p/nugetpackages/) pour le .NET Framework, ou abonnez-vous à [notre flux](https://nuget.org/api/v2/curated-feeds/dotnetframework/Packages/).

<a name="v471"></a> 
## <a name="introducing-the-net-framework-471"></a>Présentation du .NET Framework 4.7.1

Le .NET Framework 4.7.1 repose sur le .NET Framework versions 4.6, 4.6.1, 4.6.2 et 4.7, auxquelles il ajoute un grand nombre de nouveaux correctifs et plusieurs nouvelles fonctionnalités, tout en restant un produit très stable.

### <a name="downloading-and-installing-the-net-framework-471"></a>Téléchargement et installation du .NET Framework 4.7.1
 
Vous pouvez télécharger le .NET Framework 4.7.1 aux emplacements suivants :

- [Programme d’installation web du .NET Framework 4.7.1](http://go.microsoft.com/fwlink/?LinkId=852095)

- [Programme d’installation hors connexion du .NET Framework 4.7.1](http://go.microsoft.com/fwlink/?LinkId=852107)

Le .NET Framework 4.7.1 peut être installé sur Windows 10, Windows 8.1, Windows 7 SP1 et les plateformes de serveur correspondantes à partir de Windows Server 2008 R2 SP1. Vous pouvez installer le .NET Framework 4.7.1 à l’aide du programme d’installation web ou du programme d’installation hors connexion. Le programme d’installation web constitue la méthode recommandée pour la plupart des utilisateurs.

Vous pouvez cibler le .NET Framework 4.7.1 dans Visual Studio 2012 ou ultérieur en installant le [.NET Framework 4.7.1 Developer Pack](http://go.microsoft.com/fwlink/?LinkId=852105). 

### <a name="whats-new-in-the-net-framework-471"></a>Nouveautés du .NET Framework 4.7.1

Le .NET Framework 4.7.1 apporte de nouvelles fonctionnalités dans les domaines suivants :
 
- [Fonctionnalités de base](#core471)
- [Common Language Runtime (CLR)](#clr)
- [Mise en réseau](#net471)
- [ASP.NET](#asp-net471) 

Le .NET Framework 4.7.1 met l’accent sur l’amélioration de l’accessibilité pour qu’une application puisse fournir une expérience appropriée aux utilisateurs de technologies d’assistance. Pour plus d’informations sur les améliorations apportées au .NET Framework 4.7.1 dans le domaine de l’accessibilité, consultez [Nouveautés du .NET Framework dans le domaine de l’accessibilité](whats-new-in-accessibility.md). 

<a name="core471" />
#### <a name="core"></a>Principal

**Prise en charge de .NET Standard 2.0**

[.NET Standard](~/docs/standard/net-standard.md) définit un ensemble d’API qui doivent être disponibles sur chaque implémentation .NET prenant en charge cette version de la norme. Le .NET Framework 4.7.1 prend entièrement en charge .NET Standard 2.0 et ajoute [environ 200 API](https://github.com/dotnet/standard/blob/master/netstandard/src/ApiCompatBaseline.net461.txt) définies dans .NET Standard 2.0 qui ne figurent pas dans le .NET Framework 4.6.1, 4.6.2 et 4.7. (Notez que ces versions du .NET Framework prennent en charge .NET Standard 2.0 uniquement si d’autres fichiers de prise en charge .NET Standard sont également déployés sur le système cible.) Pour plus d’informations, consultez « BCL - .NET Standard 2.0 Support » dans le billet de blog [.NET Framework 4.7.1 Runtime and Compiler Features](https://blogs.msdn.microsoft.com/dotnet/2017/09/28/net-framework-4-7-1-runtime-and-compiler-features).

**Prise en charge des générateurs de configuration**

Les générateurs de configuration permettent aux développeurs d’injecter et de générer dynamiquement des paramètres de configuration pour les applications au moment de l’exécution. Des générateurs de configuration personnalisés peuvent être utilisés pour modifier des données existantes dans une section de configuration ou générer une section de configuration entièrement nouvelle. Sans les générateurs de configuration, les fichiers .config sont statiques, et leurs paramètres sont définis avant le lancement d’une application.

Pour créer un générateur de configuration personnalisé, dérivez votre générateur de la classe abstraite <xref:System.Configuration.ConfigurationBuilder> et substituez <xref:System.Configuration.ConfigurationBuilder.ProcessConfigurationSection%2A?displayProperty=nameWithType> et <xref:System.Configuration.ConfigurationBuilder.ProcessRawXml%2A?displayProperty=nameWithType>. Vous pouvez également définir vos générateurs dans votre fichier .config. Pour plus d’informations, consultez la section « Configuration Builders » dans le billet de blog [.NET Framework 4.7.1 ASP.NET and Configuration Features](https://blogs.msdn.microsoft.com/dotnet/2017/09/13/net-framework-4-7-1-asp-net-and-configuration-features). 

**Détection des fonctionnalités au moment de l’exécution**

La classe <xref:System.Runtime.CompilerServices.RuntimeFeature?displayProperty=fullName> fournit un mécanisme pour déterminer si une fonctionnalité prédéfinie est prise en charge sur une implémentation .NET donnée au moment de la compilation ou de l’exécution. Au moment de la compilation, un compilateur peut vérifier l’existence d’un champ spécifié pour déterminer si la fonctionnalité est prise en charge. Dans l’affirmative, il peut émettre du code qui exploite cette fonctionnalité. Au moment de l’exécution, une application peut appeler la méthode <xref:System.Runtime.CompilerServices.RuntimeFeature.IsSupported%2A?displayProperty=nameWithType> avant d’émettre du code. Pour plus d’informations, consultez [Ajouter une méthode d’assistance pour décrire les fonctionnalités prises en charge par le runtime](https://github.com/dotnet/corefx/issues/17116).

**Les types tuple de valeur sont sérialisables**

À compter du .NET Framework 4.7.1, <xref:System.ValueTuple?displayProperty=fullName> et ses types génériques associés sont marqués comme [Serializable](xref:System.SerializableAttribute), ce qui permet la sérialisation binaire. Cela doit faciliter la migration des types Tuple, comme <xref:System.Tuple%603> et <xref:System.Tuple%604>, vers des types tuple de valeur. Pour plus d’informations, consultez « Compiler -- ValueTuple is Serializable » dans le billet de blog [.NET Framework 4.7.1 Runtime and Compiler Features](https://blogs.msdn.microsoft.com/dotnet/2017/09/28/net-framework-4-7-1-runtime-and-compiler-features).

**Prise en charge des références en lecture seule**

<xref:System.Runtime.CompilerServices.IsReadOnlyAttribute?displayProperty=fullName> a été ajouté au .NET Framework 4.7.1. Cet attribut est utilisé par les compilateurs de langage pour marquer les membres qui ont des paramètres ou des types de retour de référence en lecture seule. Pour plus d’informations, consultez « Compiler -- Support for ReadOnlyReferences » dans le billet de blog [.NET Framework 4.7.1 Runtime and Compiler Features](https://blogs.msdn.microsoft.com/dotnet/2017/09/28/net-framework-4-7-1-runtime-and-compiler-features). Pour plus d’informations sur les valeurs de retour de référence, consultez [Valeurs de retour de référence et variables locales ref (Guide C#)](~/docs/csharp/programming-guide/classes-and-structs/ref-returns.md) et [Valeurs de retour de référence (Visual Basic)](../../visual-basic/programming-guide/language-features/procedures/ref-return-values.md).

<a name="clr" />
#### <a name="common-language-runtime-clr"></a>Common Language Runtime (CLR)

**Amélioration des performances du garbage collection**

Les changements apportés au garbage collection (GC) dans le .NET Framework 4.7.1 améliorent les performances d’ensemble, en particulier pour les allocations de tas d’objets volumineux (LOH). Dans le .NET Framework 4.7.1, des verrous distincts sont utilisés pour les allocations de tas de petits objets (SOH) et LOH, ce qui permet aux allocations LOH d’avoir lieu quand le GC en arrière-plan (BGC) nettoie le SOH. Les applications qui créent un grand nombre d’allocations LOH bénéficient donc d’une réduction de la contention de verrouillage des allocations et de meilleures performances. Pour plus d’informations, consultez la section « Runtime -- GC Performance Improvements » dans le billet de blog [.NET Framework 4.7.1 Runtime and Compiler Features](https://blogs.msdn.microsoft.com/dotnet/2017/09/28/net-framework-4-7-1-runtime-and-compiler-features/). 

**Prise en charge des fichiers PDB portables**

À compter de la version 4.7.1, le .NET Framework prend en charge les fichiers PDB portables. Alors que les fichiers PDB standards sont propres à Windows, les fichiers PDB portables peuvent être créés et lus sur toutes les plateformes. Dans la plupart des cas, le format de fichier est transparent pour l’application en cours d’exécution sur une implémentation particulière de .NET. Une application qui émet dynamiquement un assembly au moment de l’exécution constitue une exception. Dans ce cas, la possibilité d’émettre un fichier PDB portable peut améliorer les performances et réduire l’encombrement mémoire de l’application. 

Pour déterminer au moment de l’exécution si les fichiers PDB portables sont pris en charge sur l’implémentation actuelle de .NET, passez la chaîne « PortablePdb » à la méthode <xref:System.Runtime.CompilerServices.RuntimeFeature.IsSupported(System.String)?displayProperty=nameWithType> avant d’émettre l’assembly.  
 
<a name="net471"/>
#### <a name="networking"></a>Réseau

**Prise en charge de SHA-2 pour Message.HashAlgorithm**

Dans le .NET Framework 4.7 et versions antérieures, la propriété <xref:System.Messaging.Message.HashAlgorithm%2A?displayProperty=nameWithType> prenait uniquement en charge les valeurs de <xref:System.Messaging.HashAlgorithm.Md5?displayProperty=nameWithType> et <xref:System.Messaging.HashAlgorithm.Sha?displayProperty=nameWithType>. À compter du .NET Framework 4.7.1, <xref:System.Messaging.HashAlgorithm.Sha256?displayProperty=nameWithType>, <xref:System.Messaging.HashAlgorithm.Sha384?displayProperty=nameWithType> et <xref:System.Messaging.HashAlgorithm.Sha512?displayProperty=nameWithType> sont également pris en charge. MSMQ détermine si cette valeur est utilisée ou non, puisque l’instance de <xref:System.Messaging.Message> n’effectue elle-même aucun hachage et passe simplement les valeurs à MSMQ. Pour plus d’informations, consultez la section « SHA-2 support for Message.HashAlgorithm » dans le billet de blog [.NET Framework 4.7.1 ASP.NET and Configuration features](https://blogs.msdn.microsoft.com/dotnet/2017/09/13/net-framework-4-7-1-asp-net-and-configuration-features/).

<a name="asp-net471" />
#### <a name="aspnet"></a>ASP.NET

**Étapes d’exécution dans les applications ASP.NET**

ASP.NET traite les demandes dans un pipeline prédéfini comprenant 23 événements. ASP.NET exécute chaque gestionnaire d’événements sous forme d’étape d’exécution. Dans les versions d’ASP.NET jusqu’au .NET Framework 4.7, ASP.NET ne peut pas passer le contexte d’exécution en raison de la commutation entre threads natifs et threads managés. Au lieu de cela, ASP.NET passe uniquement <xref:System.Web.HttpContext> de manière sélective. À compter du .NET Framework 4.7.1, la méthode <xref:System.Web.HttpApplication.OnExecuteRequestStep(System.Action{System.Web.HttpContextBase,System.Action})?displayProperty=nameWithType> permet également aux modules de restaurer les données ambiantes. Cette fonctionnalité est destinée aux bibliothèques préoccupées par le traçage, le profilage, les diagnostics ou les transactions qui, par exemple, tiennent compte du flux d’exécution de l’application. Pour plus d’informations, consultez « ASP.NET Execution Step Feature » dans le billet de blog [.NET Framework 4.7.1 ASP.NET and Configuration Features](https://blogs.msdn.microsoft.com/dotnet/2017/09/13/net-framework-4-7-1-asp-net-and-configuration-features). 

**Analyse HttpCookie ASP.NET**

Le .NET Framework 4.7.1 comprend une nouvelle méthode, <xref:System.Web.HttpCookie.TryParse%2A?displayProperty=nameWithType>, qui offre un moyen normalisé de créer un objet <xref:System.Web.HttpCookie> à partir d’une chaîne et d’affecter avec précision des valeurs de cookie telles que la date d’expiration et le chemin. Pour plus d’informations, consultez « ASP.NET HttpCookie parsing » dans le billet de blog [.NET Framework 4.7.1 ASP.NET and Configuration Features](https://blogs.msdn.microsoft.com/dotnet/2017/09/13/net-framework-4-7-1-asp-net-and-configuration-features). 

**Options de hachage SHA-2 pour les informations d’identification de l’authentification par formulaires ASP.NET**

Dans le .NET Framework 4.7 et versions antérieures, ASP.NET permettait aux développeurs de stocker les informations d’identification des utilisateurs avec des mots de passe hachés dans des fichiers de configuration en utilisant MD5 ou SHA1. À compter du .NET Framework 4.7.1, ASP.NET prend en charge de nouvelles options de hachage SHA-2 sécurisées, notamment SHA256, SHA384 et SHA512. SHA1 reste la valeur par défaut, et un algorithme de hachage autre que celui par défaut peut être défini dans le fichier de configuration web. Exemple :

```xml
<system.web>
    <authentication mode="Forms">
        <forms loginUrl="~/login.aspx">
          <credentials passwordFormat="SHA512">
            <user name="jdoe" password="6D003E98EA1C7F04ABF8FCB375388907B7F3EE06F278DB966BE960E7CBBD103DF30CA6D61F7E7FD981B2E4E3A64D43C836A4BEDCA165C33B163E6BCDC538A664" />
          </credentials>
        </forms>
    </authentication>
</system.web>
```

<a name="v47"></a> 
### <a name="whats-new-in-the-net-framework-47"></a>Nouveautés dans le .NET Framework 4.7

Le .NET Framework 4.7 apporte de nouvelles fonctionnalités dans les domaines suivants :

- [Fonctionnalités de base](#Core47)
- [Mise en réseau](#net47)
- [ASP.NET](#ASP-NET47)
- [Windows Communication Foundation (WCF)](#wcf47)
- [Windows Forms](#wf47)
- [Windows Presentation Foundation (WPF)](#WPF47)

Pour obtenir la liste des nouvelles API ajoutées au .NET Framework 4.7, consultez la page [Changements au niveau des API du .NET Framework 4.7](https://github.com/Microsoft/dotnet/blob/master/releases/net47/dotnet47-api-changes.md) sur GitHub. Pour obtenir la liste des fonctionnalités améliorées et des correctifs de bogues apportés au .NET Framework 4.7, consultez la page [Liste des changements du .NET Framework 4.7](http://github.com/Microsoft/dotnet/blob/master/releases/net47/dotnet47-changes.md) sur GitHub.  Pour plus d’informations, consultez [Announcing the .NET Framework 4.7](https://blogs.msdn.microsoft.com/dotnet/2017/04/05/announcing-the-net-framework-4-7/) sur le blog .NET.

<a name="Core47" />
#### <a name="core"></a>Principal

Le .NET Framework 4.7 améliore la sérialisation par le <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> :

**Fonctionnalités améliorées avec chiffrement à courbe elliptique (ECC)***

Dans le .NET Framework 4.7, des méthodes `ImportParameters(ECParameters)` ont été ajoutées aux classes <xref:System.Security.Cryptography.ECDsa> et <xref:System.Security.Cryptography.ECDiffieHellman> pour permettre à un objet de représenter une clé déjà établie. En outre, une méthode `ExportParameters(Boolean)` a été ajoutée pour exporter la clé à l’aide de paramètres de courbes explicites.

Le .NET Framework 4.7 ajoute également la prise en charge de courbes supplémentaires (notamment la série de courbes Brainpool) et intègre des définitions prédéfinies pour faciliter la création via les nouvelles méthodes de fabrique <xref:System.Security.Cryptography.ECDsa.Create%2A> et <xref:System.Security.Cryptography.ECDiffieHellman.Create%2A>.

Vous pouvez voir un [exemple des améliorations apportées au chiffrement de .NET Framework 4.7](https://gist.github.com/richlander/5a182899895a87a296c21ada97f7a54e) sur GitHub.

**Meilleure prise en charge des caractères de contrôle par le DataContractJsonSerializer**

Dans le .NET Framework 4.7, le <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> sérialise les caractères de contrôle conformément à la norme ECMAScript 6. Ce comportement est activé par défaut pour les applications qui ciblent le .NET Framework 4.7, et cette fonctionnalité doit être activée pour les applications qui s’exécutent sous le .NET Framework 4.7 mais qui ciblent une version antérieure du .NET Framework. Pour plus d'informations, consultez [Modifications de reciblage dans le .NET Framework 4.7](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-7.md).

<a name="net47" />
#### <a name="networking"></a>Réseau

Le .NET Framework 4.7 ajoute les fonctionnalités liées au réseau suivantes :

**Prise en charge du système d’exploitation par défaut pour les protocoles TLS***

La pile TLS, qui est utilisée par <xref:System.Net.Security.SslStream?displayProperty=nameWithType> et les composants au-dessus de la pile, comme HTTP, FTP et SMTP, permet aux développeurs d’utiliser les protocoles TLS par défaut pris en charge par le système d’exploitation. Les développeurs n’ont plus besoin de coder en dur une version TLS.

<a name="ASP-NET47" />
#### <a name="aspnet"></a>ASP.NET

Dans le .NET Framework 4.7, ASP.NET propose les nouvelles fonctionnalités suivantes :

**Extensibilité du cache d’objets**

À compter du .NET Framework 4.7, ASP.NET ajoute un nouvel ensemble d’API permettant aux développeurs de remplacer les implémentations ASP.NET par défaut pour la mise en cache d’objets en mémoire et la surveillance de la mémoire. Les développeurs peuvent maintenant remplacer un des trois composants suivants si l’implémentation ASP.NET n’est pas appropriée :

- **Object Cache Store**. À l’aide de la nouvelle section de configuration des fournisseurs de cache, les développeurs peuvent incorporer de nouvelles implémentations d’un cache d’objets pour une application ASP.NET en utilisant la nouvelle interface **ICacheStoreProvider**.
 
- **Surveillance de la mémoire**. Le moniteur de mémoire par défaut dans ASP.NET avertit les applications lorsqu’elles approchent la limite en octets privés définie pour le processus, ou lorsque la machine manque de mémoire RAM physique disponible. Lorsque ces limites sont proches, des notifications sont déclenchées. Pour certaines applications, les notifications sont déclenchées trop près des limites configurées pour permettre des réactions opportunes. Les développeurs peuvent désormais écrire leurs propres moniteurs de mémoire pour remplacer le moniteur par défaut en utilisant la propriété <xref:System.Web.Hosting.ApplicationMonitors.MemoryMonitor%2A?displayProperty=nameWithType>.

- **Memory Limit Reactions**. Par défaut, ASP.NET tente de tronquer le cache d’objets et appelle régulièrement <xref:System.GC.Collect%2A?displayProperty=nameWithType> quand la limite en octets privés du processus est proche. Pour certaines applications, la fréquence des appels à <xref:System.GC.Collect%2A?displayProperty=nameWithType> ou la quantité de mémoire cache tronquée sont inefficaces. Les développeurs peuvent maintenant remplacer ou compléter le comportement par défaut en souscrivant des implémentations **IObserver** auprès du moniteur de mémoire de l’application.

<a name="wcf47" />
#### <a name="windows-communication-foundation-wcf"></a>Windows Communication Foundation (WCF)

Windows Communication Foundation (WFC) ajoute les fonctionnalités et modifications suivantes :

**Possibilité de configurer les paramètres de sécurité de message par défaut avec TLS 1.1 ou TLS 1.2**

À compter du .NET Framework 4.7, WCF vous permet de configurer TSL 1.1 ou TLS 1.2 en plus de SSL 3.0 et TSL 1.0 en tant que protocole de sécurité de message par défaut. Il s’agit d’un paramètre à activer ; pour cela, vous devez ajouter l’entrée suivante à votre fichier de configuration d’application :

```xml
<runtime>
   <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" /> 
</runtime>
```

**Amélioration de la fiabilité des applications WCF et de la sérialisation WCF**

WCF inclut plusieurs modifications du code qui éliminent la concurrence critique, améliorant ainsi les performances et la fiabilité des options de sérialisation. à savoir :

- Meilleure prise en charge pour le mélange de code synchrone et asynchrone dans les appels à **SocketConnection.BeginRead** et à **SocketConnection.Read**.
- Meilleure fiabilité lors de l’abandon d’une connexion avec **SharedConnectionListener** et **DuplexChannelBinder**.
- Meilleure fiabilité des opérations de sérialisation lors de l’appel de la méthode <xref:System.Runtime.Serialization.FormatterServices.GetSerializableMembers%28System.Type%29?displayProperty=nameWithType>.
- Meilleure fiabilité lors de la suppression d’un objet waiter en appelant la méthode **ChannelSynchronizer.RemoveWaiter**.

<a name="wf47" />
#### <a name="windows-forms"></a>Windows Forms

Dans le .NET Framework 4.7, Windows Forms améliore la prise en charge pour les moniteurs à haute résolution.

**Prise en charge de la haute résolution**

À partir des applications qui ciblent le .NET Framework 4.7, le .NET Framework prend en charge la haute résolution et la haute résolution dynamique pour les applications Windows Forms. La prise en charge de la haute résolution améliore la disposition et l’apparence des formulaires et des contrôles sur les moniteurs à haute résolution. La haute résolution dynamique change la disposition et l’apparence des formulaires et contrôles lorsque l’utilisateur modifie la haute résolution ou le facteur d’échelle d’affichage d’une application en cours d’exécution.

La prise en charge de la haute résolution est une fonctionnalité à activer que vous configurez en définissant une section [ \<System.Windows.Forms.ConfigurationSection >](../configure-apps/file-schema/winforms/index.md) dans votre fichier de configuration d’application. Pour plus d’informations sur l’ajout de la prise en charge de la haute résolution et de la haute résolution dynamique à votre application Windows Forms, consultez [Prise en charge de la haute résolution dans Windows Forms](../winforms/high-dpi-support-in-windows-forms.md).

<a name="WPF47"></a> 
#### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)

Dans le .NET Framework 4.7, WPF propose les améliorations suivantes :

**Prise en charge d’une pile tactile/de stylet basée sur les messages Windows WM_POINTER**

Vous pouvez désormais utiliser une fonction tactile ou stylet basée sur les [messages WM_POINTER](https://msdn.microsoft.com/library/windows/desktop/hh454903.aspx), au lieu de la plateforme WISP (Windows Ink Services Platform). Il s’agit d’une fonctionnalité à activer dans le .NET Framework. Pour plus d'informations, consultez [Modifications de reciblage dans le .NET Framework 4.7](../migration-guide/retargeting-changes-in-the-net-framework-4-7.md).

**Nouvelle implémentation pour l’impression d’API WPF**

Les API d’impression de WPF de la classe <xref:System.Printing.PrintQueue?displayProperty=nameWithType> appellent l’[API Print Document Package](https://msdn.microsoft.com/library/windows/desktop/hh448418(v=vs.85).aspx) de Windows au lieu de l’[API d’impression XPS](https://msdn.microsoft.com/library/windows/desktop/ff686814(v=vs.85).aspx) dépréciée. Pour connaître l’impact de cette modification sur la compatibilité des applications, consultez [Reciblage des modifications dans le .NET Framework 4.7](../migration-guide/retargeting-changes-in-the-net-framework-4-7.md). 

<a name="v462"></a> 
## <a name="whats-new-in-the-net-framework-462"></a>Nouveautés du .NET Framework 4.6.2

[!INCLUDE[net_v462](../../../includes/net-v462-md.md)] inclut de nouvelles fonctionnalités dans les domaines suivants :

- [ASP.NET](#ASPNET462)

- [Catégories de caractères](#Strings)

- [Chiffrement](#Crypto462)

- [SQLClient](#SQLClient)

- [Windows Communication Foundation](#WCF)

- [Windows Presentation Foundation (WPF)](#WPF462)

- [Windows Workflow Foundation (WF)](#WF462)

- [ClickOnce](#ClickOnce)

- [Conversion des Windows Forms et des applications WPF en applications UWP](#UWPConvert)

- [Améliorations du débogage](#Debug462)

Pour obtenir la liste des nouvelles API ajoutées au .NET Framework 4.6.2, consultez l’article qui détaille les [changements au niveau des API du .NET Framework 4.6.2](https://github.com/Microsoft/dotnet/blob/master/releases/net462/dotnet462-api-changes.md) sur GitHub. Pour obtenir la liste des fonctionnalités améliorées et des correctifs de bogues apportés au .NET Framework 4.6.2, consultez la page [Liste des changements du .NET Framework 4.6.2](http://go.microsoft.com/fwlink/?LinkId=708778) sur GitHub.  Pour plus d’informations, consultez [Announcing .NET Framework 4.6.2](https://blogs.msdn.microsoft.com/dotnet/2016/08/02/announcing-net-framework-4-6-2/) sur le blog .NET.

<a name="ASPNET462"></a> 
### <a name="aspnet"></a>ASP.NET
 Dans le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], ASP.NET propose les améliorations suivantes :

 **Prise en charge améliorée des messages d’erreur localisés dans les validateurs d’annotations de données** : les validateurs d’annotations de données vous permettent d’effectuer une validation en ajoutant un ou plusieurs attributs à une propriété de classe. L’élément <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=nameWithType> de l’attribut définit le texte du message d’erreur en cas d’échec de la validation. À compter du [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], ASP.NET facilite la localisation des messages d’erreur. Les messages d’erreur sont localisés si les conditions suivantes sont réunies :

1.  L’élément <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=nameWithType> est fourni dans l’attribut de validation.

2.  Le fichier de ressources est stocké dans le dossier App_LocalResources.

3.  Le nom du fichier de ressources localisées se présente sous la forme `DataAnnotation.Localization.{`*nom*`}.resx`, où *nom* est le nom de culture au format *code_languepays*`-`*code_région* ou *code_langue*.

4.  Le nom de clé de la ressource est la chaîne assignée à l’attribut <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=nameWithType>, et sa valeur correspond au message d’erreur localisé.

 Par exemple, l’attribut d’annotation de données suivant définit le message d’erreur de la culture par défaut pour une note non valide.

```csharp
public class RatingInfo
{
   [Required(ErrorMessage = "The rating must be between 1 and 10.")]
   [Display(Name = "Your Rating")]
   public int Rating { get; set; }
}
```

```vb
Public Class RatingInfo
   <Required(ErrorMessage = "The rating must be between 1 and 10.")>
   <Display(Name = "Your Rating")>
   Public Property Rating As Integer = 1
End Class
```

 Vous pouvez ensuite créer un fichier de ressources DataAnnotation.Localization.fr.resx, dont la clé est la chaîne de message d’erreur et dont la valeur est le message d’erreur localisé. Le fichier doit se trouver dans le dossier `App.LocalResources`. Par exemple, voici la clé et sa valeur dans un message d’erreur localisé en français (fr) :

| Name                                 | Value                                     |
| ------------------------------------ | ----------------------------------------- |
| The rating must be between 1 and 10. | La note doit être comprise entre 1 et 10. |

 Ce fichier peut ensuite

 De plus, la localisation des annotations de données est extensible. Les développeurs peuvent incorporer leur propre fournisseur de localisation de chaînes en implémentant l’interface <xref:System.Web.Globalization.IStringLocalizerProvider> pour stocker la chaîne de localisation ailleurs que dans un fichier de ressources.

 **Prise en charge asynchrone avec les fournisseurs de magasins d’état de session** : ASP.NET autorise désormais l’utilisation de méthodes retournant des tâches avec les fournisseurs de magasins d’état de session, ce qui permet aux applications ASP.NET de profiter de la scalabilité des opérations asynchrones. Pour prendre en charge les opérations asynchrones avec les fournisseurs de magasins d’état de session, ASP.NET propose une nouvelle interface, <xref:System.Web.SessionState.ISessionStateModule?displayProperty=nameWithType>, qui hérite de <xref:System.Web.IHttpModule> et permet aux développeurs d’implémenter leurs propres fournisseurs de modules d’état de session et de magasins de sessions asynchrones. L’interface se définit comme suit :

```csharp
public interface ISessionStateModule : IHttpModule {
    void ReleaseSessionState(HttpContext context);
    Task ReleaseSessionStateAsync(HttpContext context);
}
```

 Par ailleurs, la classe <xref:System.Web.SessionState.SessionStateUtility> comporte deux nouvelles méthodes, <xref:System.Web.SessionState.SessionStateUtility.IsSessionStateReadOnly%2A> et <xref:System.Web.SessionState.SessionStateUtility.IsSessionStateRequired%2A>, qui peuvent être utilisées pour prendre en charge les opérations asynchrones.

 **Prise en charge asynchrone pour les fournisseurs de cache de sortie** : à compter du [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], il est possible d’utiliser des méthodes qui retournent des tâches avec les fournisseurs de cache de sortie, de façon à profiter de la scalabilité des opérations asynchrones.  Les fournisseurs qui implémentent ces méthodes réduisent le blocage de threads sur un serveur web et améliorent la scalabilité d’un service ASP.NET.

 Les API suivantes ont été ajoutées pour assurer la prise en charge des fournisseurs de cache de sortie asynchrones :

- La classe <xref:System.Web.Caching.OutputCacheProviderAsync?displayProperty=nameWithType>, qui hérite de <xref:System.Web.Caching.OutputCacheProvider?displayProperty=nameWithType> et permet aux développeurs d’implémenter un fournisseur de cache de sortie asynchrone.

- La classe <xref:System.Web.Caching.OutputCacheUtility>, qui fournit les méthodes d’assistance pour configurer le cache de sortie.

- Les 18 nouvelles méthodes de la classe <xref:System.Web.HttpCachePolicy?displayProperty=nameWithType>, à savoir : <xref:System.Web.HttpCachePolicy.GetCacheability%2A>, <xref:System.Web.HttpCachePolicy.GetCacheExtensions%2A>, <xref:System.Web.HttpCachePolicy.GetETag%2A>, <xref:System.Web.HttpCachePolicy.GetETagFromFileDependencies%2A>, <xref:System.Web.HttpCachePolicy.GetMaxAge%2A>, <xref:System.Web.HttpCachePolicy.GetMaxAge%2A>, <xref:System.Web.HttpCachePolicy.GetNoStore%2A>, <xref:System.Web.HttpCachePolicy.GetNoTransforms%2A>, <xref:System.Web.HttpCachePolicy.GetOmitVaryStar%2A>, <xref:System.Web.HttpCachePolicy.GetProxyMaxAge%2A>, <xref:System.Web.HttpCachePolicy.GetRevalidation%2A>, <xref:System.Web.HttpCachePolicy.GetUtcLastModified%2A>, <xref:System.Web.HttpCachePolicy.GetVaryByCustom%2A>, <xref:System.Web.HttpCachePolicy.HasSlidingExpiration%2A> et <xref:System.Web.HttpCachePolicy.IsValidUntilExpires%2A>.

- Les deux nouvelles méthodes de la classe <xref:System.Web.HttpCacheVaryByContentEncodings?displayProperty=nameWithType> : <xref:System.Web.HttpCacheVaryByContentEncodings.GetContentEncodings%2A> et <xref:System.Web.HttpCacheVaryByContentEncodings.SetContentEncodings%2A>.

- Les deux nouvelles méthodes de la classe <xref:System.Web.HttpCacheVaryByHeaders?displayProperty=nameWithType> : <xref:System.Web.HttpCacheVaryByHeaders.GetHeaders%2A> et <xref:System.Web.HttpCacheVaryByHeaders.SetHeaders%2A>.

- Les deux nouvelles méthodes de la classe <xref:System.Web.HttpCacheVaryByParams?displayProperty=nameWithType> : <xref:System.Web.HttpCacheVaryByParams.GetParams%2A> et <xref:System.Web.HttpCacheVaryByParams.SetParams%2A>.

- Dans la classe <xref:System.Web.Caching.AggregateCacheDependency?displayProperty=nameWithType>, la méthode <xref:System.Web.Caching.AggregateCacheDependency.GetFileDependencies%2A>.

- Dans la classe <xref:System.Web.Caching.CacheDependency>, la méthode <xref:System.Web.Caching.CacheDependency.GetFileDependencies%2A>.

<a name="Strings"></a> 
### <a name="character-categories"></a>Catégories de caractères
 Dans le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], les caractères sont classés d’après la [norme Unicode, version 8.0.0](http://www.unicode.org/versions/Unicode8.0.0/). Dans le [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] et le [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], les caractères étaient classés en fonction des catégories de caractères Unicode 6.3.

 La prise en charge d’Unicode 8.0 se limite à la classification des caractères de la classe <xref:System.Globalization.CharUnicodeInfo> et aux types et méthodes qui en dépendent. Il s’agit notamment de la classe <xref:System.Globalization.StringInfo>, de la méthode <xref:System.Char.GetUnicodeCategory%2A?displayProperty=nameWithType> surchargée et des [classes de caractères](../../../docs/standard/base-types/character-classes-in-regular-expressions.md) reconnues par le moteur d’expressions régulières du .NET Framework.  La comparaison et le tri des caractères et des chaînes ne sont pas affectés par cette évolution et continuent de s’appuyer sur le système d’exploitation sous-jacent ou bien, dans le cas des systèmes Windows 7, sur les données de caractères fournies par le .NET Framework.

 Pour en savoir plus sur l’évolution des catégories de caractères entre Unicode 6.0 et Unicode 7.0, consultez l’article traitant de la [norme Unicode, version 7.0.0](http://www.unicode.org/versions/Unicode7.0.0/) sur le site web du consortium Unicode. Pour en savoir plus sur les changements intervenus entre Unicode 7.0 et Unicode 8.0, consultez l’article traitant de la [norme Unicode, version 8.0.0](http://www.unicode.org/versions/Unicode8.0.0/) sur le site web du consortium Unicode.

<a name="Crypto462"></a> 
### <a name="cryptography"></a>Chiffrement
 **Prise en charge des certificats X509 contenant l’algorithme DSA FIPS 186-3** : le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] ajoute la prise en charge des certificats X509 DSA(Digital Signature Algorithm) dont les clés dépassent la limite de 1 024 bits de la norme FIPS 186-2.

 En plus de prendre en charge les clés plus volumineuses de FIPS 186-3, le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] autorise le calcul de signatures à l’aide des algorithmes de hachage de la famille SHA-2 (SHA256, SHA384 et SHA512). La prise en charge de FIPS 186-3 est assurée par la nouvelle classe <xref:System.Security.Cryptography.DSACng?displayProperty=nameWithType>.

 Dans la logique des récentes évolutions de la classe <xref:System.Security.Cryptography.RSA> dans le .NET Framework 4.6 et de la classe <xref:System.Security.Cryptography.ECDsa> dans le .NET Framework 4.6.1, la classe de base abstraite <xref:System.Security.Cryptography.DSA> du [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] propose des méthodes supplémentaires qui permettent aux appelants d’utiliser cette fonctionnalité sans opération de cast. Vous pouvez appeler la méthode d’extension <xref:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPrivateKey%2A?displayProperty=nameWithType> pour signer des données, comme le montre l’exemple suivant.

```csharp
public static byte[] SignDataDsaSha384(byte[] data, X509Certificate2 cert)
{
    using (DSA dsa = cert.GetDSAPrivateKey())
    {
        return dsa.SignData(data, HashAlgorithmName.SHA384);
    }
}
```

```vb 
Public Shared Function SignDataDsaSha384(data As Byte(), cert As X509Certificate2) As Byte()
    Using DSA As DSA = cert.GetDSAPrivateKey()
        Return DSA.SignData(data, HashAlgorithmName.SHA384)
    End Using
End Function
```

 Vous pouvez également appeler la méthode d’extension <xref:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPublicKey%2A?displayProperty=nameWithType> pour vérifier les données signées, comme le montre l’exemple suivant.

```csharp
public static bool VerifyDataDsaSha384(byte[] data, byte[] signature, X509Certificate2 cert)
{
    using (DSA dsa = cert.GetDSAPublicKey())
    {
        return dsa.VerifyData(data, signature, HashAlgorithmName.SHA384);
    }
}
```

```vb
 Public Shared Function VerifyDataDsaSha384(data As Byte(), signature As Byte(), cert As X509Certificate2) As Boolean
    Using dsa As DSA = cert.GetDSAPublicKey()
        Return dsa.VerifyData(data, signature, HashAlgorithmName.SHA384)
    End Using
End Function
```

 **Plus de clarté pour les entrées dans les routines de dérivation de clé ECDiffieHellman** : la prise en charge de l’accord d’échange de clés Diffie-Hellman basé sur les courbes elliptiques a été ajoutée au .NET Framework 3.5 avec trois routines différentes de fonction de dérivation de clés (KDF). Les entrées à destination de ces routines, tout comme les routines proprement dites, étaient configurées via les propriétés de l’objet <xref:System.Security.Cryptography.ECDiffieHellmanCng>. Mais comme les routines ne pouvaient pas toutes lire chaque propriété d’entrée, la confusion était de mise auprès des développeurs.

 Pour résoudre ce problème dans le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], les trois méthodes suivantes ont été ajoutées à la classe de base <xref:System.Security.Cryptography.ECDiffieHellman> de façon à représenter plus clairement ces routines KDF et leurs entrées :

|Méthode ECDiffieHellman|Description|
|----------------------------|-----------------|
|<xref:System.Security.Cryptography.ECDiffieHellman.DeriveKeyFromHash%28System.Security.Cryptography.ECDiffieHellmanPublicKey%2CSystem.Security.Cryptography.HashAlgorithmName%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%29>|Dérive le matériel de clé à l’aide de la formule<br /><br /> HASH(secretPrepend &#124;&#124; *x* &#124;&#124; secretAppend)<br /><br /> HASH(secretPrepend OrElse *x* OrElse secretAppend)<br /><br /> où *x* représente le résultat du calcul de l’algorithme EC Diffie-Hellman.|
|<xref:System.Security.Cryptography.ECDiffieHellman.DeriveKeyFromHmac%28System.Security.Cryptography.ECDiffieHellmanPublicKey%2CSystem.Security.Cryptography.HashAlgorithmName%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%29>|Dérive le matériel de clé à l’aide de la formule<br /><br /> HMAC(hmacKey, secretPrepend &#124;&#124; *x* &#124;&#124; secretAppend)<br /><br /> HMAC(hmacKey, secretPrepend OrElse *x* OrElse secretAppend)<br /><br /> où *x* représente le résultat du calcul de l’algorithme EC Diffie-Hellman.|
|<xref:System.Security.Cryptography.ECDiffieHellman.DeriveKeyTls%28System.Security.Cryptography.ECDiffieHellmanPublicKey%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%29>|Dérive le matériel de clé à l’aide de l’algorithme de dérivation de la fonction pseudo-aléatoire (PRF) TLS.|

 **Prise en charge du chiffrement symétrique des clés persistantes** : la bibliothèque de chiffrement Windows (CNG) a ajouté la prise en charge du stockage de clés symétriques persistantes et de l’utilisation des clés symétriques stockées sur du matériel, et le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] a permis aux développeurs d’utiliser cette fonctionnalité.  Sachant que la notion de noms de clés et de fournisseurs de clés est spécifique à l’implémentation, cette fonctionnalité impose l’utilisation du constructeur des types d’implémentation concrets plutôt que l’approche par défaut privilégiée (comme l’appel de `Aes.Create`).

 La prise en charge du chiffrement symétrique des clés persistantes existe pour les algorithmes AES (<xref:System.Security.Cryptography.AesCng>) et 3DES (<xref:System.Security.Cryptography.TripleDESCng>). Exemple :

```csharp
public static byte[] EncryptDataWithPersistedKey(byte[] data, byte[] iv)
{
    using (Aes aes = new AesCng("AesDemoKey", CngProvider.MicrosoftSoftwareKeyStorageProvider))
    {
        aes.IV = iv;

        // Using the zero-argument overload is required to make use of the persisted key
        using (ICryptoTransform encryptor = aes.CreateEncryptor())
        {
            if (!encryptor.CanTransformMultipleBlocks)
            {
                throw new InvalidOperationException("This is a sample, this case wasn’t handled...");
            }

            return encryptor.TransformFinalBlock(data, 0, data.Length);
        }
    }
}
```

```vb 
Public Shared Function EncryptDataWithPersistedKey(data As Byte(), iv As Byte()) As Byte()
    Using Aes As Aes = New AesCng("AesDemoKey", CngProvider.MicrosoftSoftwareKeyStorageProvider)
        Aes.IV = iv

        ' Using the zero-argument overload Is required to make use of the persisted key
        Using encryptor As ICryptoTransform = Aes.CreateEncryptor()
            If Not encryptor.CanTransformMultipleBlocks Then
                Throw New InvalidOperationException("This is a sample, this case wasn’t handled...")
            End If
            Return encryptor.TransformFinalBlock(data, 0, data.Length)
        End Using
    End Using
End Function
```

 **Prise en charge de SignedXml pour le hachage SHA-2** : le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] ajoute à la classe <xref:System.Security.Cryptography.Xml.SignedXml> la prise en charge des méthodes de signature pour RSA-SHA256, RSA-SHA384 et RSA-SHA512 PKCS#1, et des algorithmes Digest de référence SHA256, SHA384 et SHA512.

 Les constantes d’URI sont toutes exposées dans <xref:System.Security.Cryptography.Xml.SignedXml> :

|Champ SignedXml|Constante|
|---------------------|--------------|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA256Url>|"http://www.w3.org/2001/04/xmlenc#sha256"|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA256Url>|"http://www.w3.org/2001/04/xmldsig-more#rsa-sha256"|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA384Url>|"http://www.w3.org/2001/04/xmldsig-more#sha384"|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA384Url>|"http://www.w3.org/2001/04/xmldsig-more#rsa-sha384"|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA512Url>|"http://www.w3.org/2001/04/xmlenc#sha512"|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA512Url>|"http://www.w3.org/2001/04/xmldsig-more#rsa-sha512"|

 Les programmes qui ont inscrit un gestionnaire <xref:System.Security.Cryptography.SignatureDescription> personnalisé dans <xref:System.Security.Cryptography.CryptoConfig> dans le but d’ajouter la prise en charge de ces algorithmes continueront de fonctionner comme par le passé. Cependant, comme il y a désormais les valeurs par défaut de la plateforme, l’inscription <xref:System.Security.Cryptography.CryptoConfig> n’est plus nécessaire.

<a name="SQLClient"></a> 
### <a name="sqlclient"></a>SqlClient
 Le fournisseur de données .NET Framework pour SQL Server (<xref:System.Data.SqlClient?displayProperty=nameWithType>) inclut les nouvelles fonctionnalités suivantes dans le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] :

 **Regroupement et délais d’expiration des connexions délai avec les bases de données Azure SQL** : quand le regroupement de connexions est activé, et qu’une erreur de dépassement de délai d’expiration ou une autre erreur de connexion se produit, une exception est mise en cache ; cette exception est levée chaque fois qu’une nouvelle tentative de connexion intervient entre 5 secondes et 1 minute après.  Pour plus d’informations, consultez [Regroupement de connexions (ADO.NET)](../../../docs/framework/data/adonet/sql-server-connection-pooling.md).

 Ce comportement n’est pas souhaitable quand il s’agit d’établir des connexions à des bases de données Azure SQL Database, car les tentatives de connexion peuvent échouer avec des erreurs transitoires qui sont en général récupérées rapidement. Pour des nouvelles tentatives de connexion plus abouties, le comportement de période de blocage de pool de connexions est supprimé quand les connexions aux bases de données Azure SQL Database échouent.

 L’ajout du nouveau mot clé `PoolBlockingPeriod` vous permet de sélectionner la période de blocage qui convient le mieux à votre application. Les valeurs incluent :

 `Auto` : la période de blocage du pool de connexions pour une application qui se connecte à une base de données Azure SQL Database est désactivée, alors que cette période pour une application qui se connecte à une autre instance SQL Server est activée. Valeur par défaut. Si le nom de point de terminaison d’un serveur se termine par l’un des éléments suivants, il est considéré comme une base de données Azure SQL Database :

- .database.windows.net

- .database.chinacloudapi.cn

- .database.usgovcloudapi.net

- .database.cloudapi.de

 `AlwaysBlock` La période de blocage de pool de connexion est toujours activée.

 `NeverBlock` La période de blocage de pool de connexion est toujours désactivée.

 **Améliorations pour Always Encrypted** SQLClient inaugure deux améliorations pour Always Encrypted :

- Pour améliorer les performances des requêtes paramétrables sur des colonnes de base de données chiffrées, les métadonnées de chiffrement sont désormais mises en cache pour les paramètres des requêtes. Dans la mesure où la propriété <xref:System.Data.SqlClient.SqlConnection.ColumnEncryptionQueryMetadataCacheEnabled%2A?displayProperty=nameWithType> est définie sur `true` (valeur par défaut), si une même requête est appelée plusieurs fois, le client ne récupère les métadonnées des paramètres qu’une seule fois sur le serveur.

- Les entrées de clés de chiffrement de colonnes présentes dans le cache de clés sont désormais supprimées au bout d’un délai configurable, qui est défini à l’aide de la propriété <xref:System.Data.SqlClient.SqlConnection.ColumnEncryptionKeyCacheTtl%2A?displayProperty=nameWithType>.

<a name="WCF"></a> 
### <a name="windows-communication-foundation"></a>Windows Communication Foundation
 Dans le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], Windows Communication Foundation a été amélioré dans les domaines suivants :

 **Prise en charge des certificats stockés à l’aide de CNG par la sécurité du transport WCF**: la sécurité du transport WCF prend en charge les certificats stockés à l’aide de la bibliothèque de chiffrement Windows (CNG). Dans le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], cette prise en charge se limite à l’utilisation de certificats avec une clé publique dont l’exposant ne dépasse pas 32 bits de longueur. Quand une application cible le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], cette fonctionnalité est activée par défaut.

 Pour les applications qui ciblent le [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] ou des versions antérieures, mais qui s’exécutent sur le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], cette fonctionnalité peut être activée en ajoutant la ligne suivante à la section [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) du fichier app.config ou web.config.

```xml
<AppContextSwitchOverrides
    value="Switch.System.ServiceModel.DisableCngCertificates=false"
/>
```

Vous pouvez en faire autant par programmation avec un code de ce type :

```csharp
private const string DisableCngCertificates = @"Switch.System.ServiceModel.DisableCngCertificates";
AppContext.SetSwitch(disableCngCertificates, false);
```

```vb
Const DisableCngCertificates As String = "Switch.System.ServiceModel.DisableCngCertificates"
AppContext.SetSwitch(disableCngCertificates, False)
```

 **Meilleure prise en charge de plusieurs règles d’ajustement à l’heure d’été par la classe DataContractJsonSerializer** : les clients peuvent utiliser un paramètre de configuration d’application pour déterminer si la classe <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> prend en charge plusieurs règles d’ajustement pour un même un fuseau horaire. Il est nécessaire d'accepter cette fonctionnalité. Pour l’activer, ajoutez le paramètre suivant à votre fichier app.config :

```xml
<runtime>
     <AppContextSwitchOverrides value="Switch.System.Runtime.Serialization.DoNotUseTimeZoneInfo=false" />
</runtime>
```

Quand cette fonctionnalité est activée, un objet <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> utilise le type <xref:System.TimeZoneInfo> à la place du type <xref:System.TimeZone> pour désérialiser les données de date et d’heure. <xref:System.TimeZoneInfo> prend en charge plusieurs règles d’ajustement, ce qui permet d’utiliser des données de fuseau horaire historiques ; ce n’est pas le cas de <xref:System.TimeZone>.

Pour plus d’informations sur la structure <xref:System.TimeZoneInfo> et les ajustements de fuseau horaire, consultez [Vue d’ensemble des fuseaux horaires](../../../docs/standard/datetime/time-zone-overview.md).

**Prise en charge de la conservation d’une heure UTC pendant la sérialisation et la désérialisation avec la classe XMLSerializer** D’ordinaire, quand la classe <xref:System.Xml.Serialization.XmlSerializer> est utilisée pour sérialiser une valeur <xref:System.DateTime> UTC, elle crée une chaîne de date/heure sérialisée qui conserve la date et l’heure, mais considère que l’heure est locale.  Par exemple, si vous instanciez une date et une heure UTC en appelant le code suivant :

```csharp
DateTime utc = new DateTime(2016, 11, 07, 3, 0, 0, DateTimeKind.Utc);
```

```vb
Dim utc As New Date(2016, 11, 07, 3, 0, 0, DateTimeKind.Utc)
```

Vous obtenez la chaîne d’heure sérialisée « 03:00:00.0000000-08:00 » pour un système avec huit heures de moins par rapport à l’heure UTC.  Et les valeurs sérialisées sont toujours désérialisées comme valeurs de date et d’heure locales.

 Vous pouvez utiliser un paramètre de configuration d’application pour déterminer si <xref:System.Xml.Serialization.XmlSerializer> conserve les informations de fuseau horaire UTC pendant la sérialisation et la désérialisation des valeurs <xref:System.DateTime> :

```xml 
<runtime>
     <AppContextSwitchOverrides 
          value="Switch.System.Runtime.Serialization.DisableSerializeUTCDateTimeToTimeAndDeserializeUTCTimeToUTCDateTime=false" />
</runtime>
```

Quand cette fonctionnalité est activée, un objet <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> utilise le type <xref:System.TimeZoneInfo> à la place du type <xref:System.TimeZone> pour désérialiser les données de date et d’heure. <xref:System.TimeZoneInfo> prend en charge plusieurs règles d’ajustement, ce qui permet d’utiliser des données de fuseau horaire historiques ; ce n’est pas le cas de <xref:System.TimeZone>.

Pour plus d’informations sur la structure <xref:System.TimeZoneInfo> et les ajustements de fuseau horaire, consultez [Vue d’ensemble des fuseaux horaires](../../../docs/standard/datetime/time-zone-overview.md).

 **Meilleure correspondance de NetNamedPipeBinding**: WCF a un nouveau paramètre d’application qui peut être défini sur les applications clientes de telle sorte qu’elles se connectent toujours au service écoutant l’URI qui correspond le mieux à celui qu’elles demandent. Dans la mesure où ce paramètre d’application est défini sur `false` (valeur par défaut), les clients utilisant <xref:System.ServiceModel.NetNamedPipeBinding> peuvent tenter de se connecter à un service écoutant un URI qui est une sous-chaîne de l’URI demandé.

 Par exemple, un client tente de se connecter à un service à l’écoute de `net.pipe://localhost/Service1`, mais un autre service de cet ordinateur s’exécutant avec des privilèges d’administrateur écoute `net.pipe://localhost`. Si ce paramètre d’application est défini sur `false`, le client tente de se connecter au mauvais service. Une fois le paramètre d’application défini sur `true`, le client se connecte systématiquement au service le plus approprié.

> [!NOTE]
>  Les clients qui utilisent <xref:System.ServiceModel.NetNamedPipeBinding> recherchent les services à partir de leur adresse de base (s’ils en ont une) et non de l’adresse complète du point de terminaison. Pour faire en sorte que ce paramètre fonctionne toujours, le service doit utiliser une adresse de base unique.

 Pour permettre cette modification, ajoutez le paramètre d’application suivant au fichier App.config ou Web.config de votre application cliente :

```xml
<configuration>
    <appSettings>
        <add key="wcf:useBestMatchNamedPipeUri" value="true" />
    </appSettings>
</configuration>
```

 **SSL 3.0 n’est pas un protocole par défaut** : quand vous utilisez NetTcp avec la sécurité du transport et un type de certificat avec des informations d’identification, SSL 3.0 n’est plus le protocole utilisé par défaut quand il s’agit de négocier une connexion sécurisée. Dans la majorité des cas, cela ne devrait pas avoir de conséquences sur les applications existantes, car TLS 1.0 est inclus dans la liste de protocoles pour NetTcp. Tous les clients existants doivent pouvoir négocier une connexion en utilisant au moins TLS 1.0. Si Ssl3 est exigé, utilisez l’un des mécanismes de configuration suivants pour l’ajouter à la liste des protocoles négociés.

- La propriété <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement.SslProtocols%2A?displayProperty=nameWithType>

- La propriété <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A?displayProperty=nameWithType>

- La section [\<transport>](../../../docs/framework/configure-apps/file-schema/wcf/transport-of-nettcpbinding.md) de la section [\<netTcpBinding>](../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md)

- La section [\<sslStreamSecurity>](../../../docs/framework/configure-apps/file-schema/wcf/sslstreamsecurity.md) de la section [\<customBinding>](../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)

<a name="WPF462"></a> 
### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)
 Dans le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], Windows Presentation Foundation a été amélioré dans les domaines suivants :

 **Tri des groupes** : une application qui utilise un objet <xref:System.Windows.Data.CollectionView> pour regrouper les données peut désormais déclarer explicitement comment trier les groupes. Le tri explicite résout le problème du classement non intuitif qui se produit quand une application ajoute ou supprime dynamiquement des groupes ou quand elle modifie la valeur de propriétés d’élément impliquées dans le regroupement. Il peut aussi améliorer l’efficacité de la création de groupes en comparant les propriétés de regroupement non pas au niveau du tri de la collection complète mais du tri des groupes.

 Pour prendre en charge le tri des groupes, les nouvelles propriétés <xref:System.ComponentModel.GroupDescription.SortDescriptions%2A?displayProperty=nameWithType> et <xref:System.ComponentModel.GroupDescription.CustomSort%2A?displayProperty=nameWithType> décrivent le mode de tri de la collection de groupes produite par l’objet <xref:System.ComponentModel.GroupDescription>. Ce comportement est analogue à la façon dont les propriétés <xref:System.Windows.Data.ListCollectionView> de même nom décrivent le mode de tri des éléments de données.

 Il est possible d’utiliser les deux nouvelles propriétés statiques de la classe <xref:System.Windows.Data.PropertyGroupDescription>, <xref:System.Windows.Data.PropertyGroupDescription.CompareNameAscending%2A> et <xref:System.Windows.Data.PropertyGroupDescription.CompareNameDescending%2A>, pour les cas les plus courants.

 Par exemple, le code XAML suivant regroupe les données par âge, trie les groupes d’âge par ordre croissant, puis regroupe les éléments de chaque groupe d’âge par nom de famille.

```xaml
<GroupDescriptions>
     <PropertyGroupDescription 
         PropertyName="Age" 
         CustomSort= 
              "{x:Static PropertyGroupDescription.CompareNamesAscending}"/>
     </PropertyGroupDescription>
</GroupDescriptions>

<SortDescriptions>
     <SortDescription PropertyName="LastName"/>
</SortDescriptions>
```

 **Prise en charge des claviers logiciels**: la prise en charge des claviers logiciels permet d’assurer le suivi du focus dans les applications WPF en appelant et en masquant automatiquement le nouveau clavier logiciel dans Windows 10 dès lors que l’entrée tactile est reçue par un contrôle qui peut prendre une entrée sous forme de texte.

 Dans les versions précédentes du .NET Framework, les applications WPF ne peuvent pas opter pour le suivi du focus sans désactiver la prise en charge du stylo et des entrées tactiles WPF.  Par conséquent, les applications WPF doivent soit choisir la prise en charge complète des entrées tactiles WPF, soit privilégier la souris Windows.

 **Résolution par moniteur** : pour faire face à la prolifération récente des environnements à haute résolution et à résolution hybride pour les applications WPF, WPF permet une prise en charge par moniteur dans le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]. Pour savoir comment permettre à votre application WPF de prendre en charge la résolution par moniteur, consultez les [exemples et le guide du développeur](https://github.com/Microsoft/WPF-Samples/tree/master/PerMonitorDPI) sur GitHub.

 Dans les versions précédentes du .NET Framework, les applications WPF prennent en charge la résolution au niveau du système. En d’autres termes, l’interface utilisateur de l’application est éventuellement mise à l’échelle par le système d’exploitation, en fonction de la résolution du moniteur sur lequel l’application est affichée. ,

 Pour les applications s’exécutant sous le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], vous pouvez désactiver les changements de résolution par moniteur dans les applications WPF en ajoutant une instruction de configuration à la section [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) du fichier de configuration de votre application, comme suit :

```xml
<runtime>
   <AppContextSwitchOverrides value="Switch.System.Windows.DoNotScaleForDpiChanges=false"/>
</runtime>
```

<a name="WF462"></a> 
### <a name="windows-workflow-foundation-wf"></a>Windows Workflow Foundation (WF)
 Dans le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], Windows Workflow Foundation a été amélioré dans les domaines suivants :

 **Prise en charge des expressions C# et d’IntelliSense dans le concepteur WF réhébergé** : à compter du [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], WF prend en charge les expressions C# dans le concepteur Visual Studio et dans les flux de travail de code. Le Concepteur de flux de travail réhébergé est une fonctionnalité clé de WF qui autorise la présence du Concepteur de flux de travail dans une application extérieure à Visual Studio (par exemple, dans WPF).  Windows Workflow Foundation permet de prendre en charge les expressions C# et IntelliSense dans le Concepteur de flux de travail réhébergé. Pour plus d’informations, consultez le [blog Windows Workflow Foundation](http://go.microsoft.com/fwlink/?LinkID=809042&clcid=0x409).

 `Availability of IntelliSense when a customer rebuilds a workflow project from Visual Studio` : dans les versions du .NET Framework antérieures au [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], la fonctionnalité IntelliSense du concepteur WFest inopérante quand un client recrée un projet de flux de travail à partir de Visual Studio. Quand la génération du projet aboutit, les types de flux de travail ne se trouvent pas dans le concepteur, et IntelliSense affiche des avertissements dans la fenêtre **Liste d’erreurs** par rapport aux types de flux de travail manquants. Le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] résout ce problème et donne accès à IntelliSense.

 **Les applications Workflow V1 pour lesquelles le suivi de flux de travail est activé s’exécutent désormais en mode FIPS** : les ordinateurs pour lesquels le mode de conformité FIPS est activé peuvent désormais exécuter correctement une application de type Workflow version 1 avec le suivi de flux de travail activé. Pour permettre ce cas de figure, vous devez apporter la modification suivante à votre fichier app.config :

```xml
<add key="microsoft:WorkflowRuntime:FIPSRequired" value="true" />
```

 Si ce scénario n’est pas autorisé, l’exécution de l’application continue de générer une exception avec le message « Cette implémentation ne fait pas partie des algorithmes de chiffrement validés FIPS pour les plateformes Windows ».

 **Amélioration des flux de travail quand la mise à jour dynamique est utilisée avec le Concepteur de flux de travail Visual Studio** : le Concepteur de flux de travail, le Concepteur d’activités d’organigramme et les autres Concepteurs d’activité de flux de travail peuvent désormais charger et afficher correctement les flux de travail qui ont été enregistrés après l’appel de la méthode <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=nameWithType>. Dans les versions du .NET Framework antérieures au [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], le fait de charger un fichier XAML dans Visual Studio pour un flux de travail enregistré après un appel de <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=nameWithType> peut occasionner les problèmes suivants :

- Le Concepteur de flux de travail ne peut pas charger le fichier XAML correctement (quand <xref:System.Activities.Presentation.ViewState.ViewStateData.Id%2A?displayProperty=nameWithType> est en fin de ligne).

- Le Concepteur d’activités d’organigramme ou les autres Concepteurs d’activités de flux de travail peuvent afficher tous les objets à leurs emplacements par défaut plutôt que les valeurs de propriétés jointes.

<a name="ClickOnce"></a> 
### <a name="clickonce"></a>ClickOnce
 ClickOnce a été mis à jour pour prendre en charge TLS 1.1 et TLS 1.2 en plus du protocole 1.0, qu’il prend déjà en charge. ClickOnce détecte automatiquement le protocole exigé ; aucune mesure supplémentaire n’est à prendre dans l’application ClickOnce pour activer la prise en charge de TLS 1.1 et 1.2.

<a name="UWPConvert"></a> 
### <a name="converting-windows-forms-and-wpf-apps-to--uwp-apps"></a>Conversion des Windows Forms et des applications WPF en applications UWP
 Windows permet désormais de porter les applications de bureau Windows, dont les applications WPF et Windows Forms, sur la plateforme Windows universelle (UWP). Cette technologie fait office de pont en vous permettant de migrer progressivement votre base de code existante vers UWP, et ainsi de porter votre application sur tous les appareils Windows 10.

 Les applications de bureau converties obtiennent une identité d’application comparable à celle des applications UWP, ce qui rend les API UWP accessibles pour activer certaines fonctionnalités, telles que les vignettes dynamiques et les notifications. L’application continue de se comporter comme auparavant et s’exécute comme une application entièrement approuvée. Une fois l’application convertie, un processus de conteneur d’application peut être ajouté au processus d’approbation complète existant pour ajouter une interface utilisateur adaptative. Quand toutes les fonctionnalités sont déplacées vers le processus de conteneur d’application, le processus d’approbation complète peut être supprimé et la nouvelle application UWP peut être mise à la disposition de tous les appareils Windows 10.

<a name="Debug462"></a> 
### <a name="debugging-improvements"></a>Améliorations du débogage
 L’*API de débogage non managé* a été améliorée dans le [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] de façon à effectuer des analyses supplémentaires quand une <xref:System.NullReferenceException> est levée, dans le but de permettre l’identification de la variable qui a la valeur `null` dans une même ligne de code source.   Pour favoriser ce scénario, les API ci-dessous ont été ajoutées à l’API de débogage non managé.

- Les interfaces [ICorDebugCode4](../../../docs/framework/unmanaged-api/debugging/icordebugcode4-interface.md), [ICorDebugVariableHome](../../../docs/framework/unmanaged-api/debugging/icordebugvariablehome-interface.md) et [ICorDebugVariableHomeEnum](../../../docs/framework/unmanaged-api/debugging/icordebugvariablehomeenum-interface.md), qui exposent les dossiers natifs des variables managées. Les débogueurs peuvent ainsi effectuer des analyses de flux de code quand une exception <xref:System.NullReferenceException> se produit et revenir en arrière pour identifier la variable managée qui correspond à l’emplacement natif qui avait la valeur `null`.

- La méthode [ICorDebugType2::GetTypeID](../../../docs/framework/unmanaged-api/debugging/icordebugtype2-gettypeid-method.md) propose un mappage de ICorDebugType à [COR_TYPEID](../../../docs/framework/unmanaged-api/debugging/cor-typeid-structure.md), ce qui permet au débogueur d’obtenir un [COR_TYPEID](../../../docs/framework/unmanaged-api/debugging/cor-typeid-structure.md) sans instance de ICorDebugType. Les API existantes sur [COR_TYPEID](../../../docs/framework/unmanaged-api/debugging/cor-typeid-structure.md) peuvent ensuite servir à déterminer la disposition de classe du type.

<a name="v461"></a> 
## <a name="whats-new-in-the-net-framework-461"></a>Nouveautés dans le .NET Framework 4.6.1
 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] inclut de nouvelles fonctionnalités dans les domaines suivants :

- [Chiffrement](#Crypto)

- [ADO.NET](#ADO.NET461)

- [Windows Presentation Foundation (WPF)](#WPF461)

- [Windows Workflow Foundation](#WWF461)

- [Profilage](#Profile461)

- [NGen](#NGEN461)

 Pour plus d’informations sur [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], consultez les rubriques suivantes :

- La [liste des modifications du .NET Framework 4.6.1](http://go.microsoft.com/fwlink/?LinkId=622964)

- [Compatibilité des applications dans la version 4.6.1](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6-1.md)

- [Différences de l’API .NET Framework](http://go.microsoft.com/fwlink/?LinkId=622989) (sur GitHub)

<a name="Crypto"></a> 
### <a name="cryptography-support-for-x509-certificates-containing-ecdsa"></a>Chiffrement : prise en charge des certificats X509 contenant l’algorithme ECDSA
 .NET Framework 4.6 a ajouté la prise en charge de l’algorithme RSACng pour les certificats X509. [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] ajoute la prise en charge des certificats X509 ECDSA (Elliptic Curve Digital Signature Algorithm).

 ECDSA offre de meilleures performances et constitue un algorithme de chiffrement plus sécurisé que RSA. Il constitue un excellent choix quand les performances et la scalabilité de la sécurité de la couche de transport (TLS) constituent une préoccupation. L’implémentation du .NET Framework encapsule les appels dans les fonctionnalités Windows existantes.

 L’exemple de code suivant montre combien il est facile de générer une signature pour un flux d’octets à l’aide de la nouvelle prise en charge des certificats X509 ECDSA inclus dans [!INCLUDE[net_v461](../../../includes/net-v461-md.md)].

 [!code-csharp[whatsnew.461.crypto#1](../../../samples/snippets/csharp/VS_Snippets_CLR/whatsnew.461.crypto/cs/Code46.cs#1)]
 [!code-vb[whatsnew.461.crypto#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.461.crypto/vb/Code461.vb#1)]

 Cela contraste fortement avec le code nécessaire pour générer une signature dans .NET Framework 4.6.

 [!code-csharp[whatsnew.461.crypto#2](../../../samples/snippets/csharp/VS_Snippets_CLR/whatsnew.461.crypto/cs/Code46.cs#2)]
 [!code-vb[whatsnew.461.crypto#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.461.crypto/vb/Code46.vb#2)]

<a name="ADO.NET461"></a> 
### <a name="adonet"></a>ADO.NET
 Les éléments suivants ont été ajoutés à ADO.NET :

 Prise en charge de la fonctionnalité Always Encrypted pour les clés matérielles protégées ADO.NET prend désormais en charge le stockage des clés principales de colonnes Always Encrypted en mode natif dans les modules de sécurité matériels (HSM, Hardware Security Module). Cette prise en charge permet aux clients de tirer profit des clés asymétriques stockées dans les modules HSM sans avoir à écrire des fournisseurs de magasins de clés principales de colonnes personnalisés et sans les inscrire dans les applications.

 Les clients doivent installer le fournisseur CSP fourni par le fabricant des modules HSM ou les fournisseurs de magasin de clés CNG sur les serveurs d’applications ou les ordinateurs clients pour accéder aux données Toujours chiffré protégées par des clés principales de colonnes stockées dans un module HSM.

 Amélioration du comportement de la connexion <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A> SqlClient fournit désormais automatiquement une connexion plus rapide à un groupe de disponibilité AlwaysOn. Il détecte de façon transparente si votre application se connecte à un groupe de disponibilité AlwaysOn sur un autre sous-réseau, détecte rapidement le serveur actif actuel et fournit une connexion au serveur. Avant cette mise en production, une application devait définir la chaîne de connexion à inclure `"MultisubnetFailover=true"` pour indiquer qu’elle était connectée à un groupe de disponibilité AlwaysOn. Si le mot clé de connexion n’était pas défini sur `true`, une application pouvait rencontrer un dépassement du délai lors de la connexion à un groupe de disponibilité AlwaysOn. Avec cette version, une application *n’a plus* besoin de définir <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A> sur `true`. Pour plus d’informations sur la prise en charge de SqlClient pour les groupes de disponibilité AlwaysOn, consultez [Prise en charge de SqlClient pour la haute disponibilité et la récupération d’urgence](../../../docs/framework/data/adonet/sql/sqlclient-support-for-high-availability-disaster-recovery.md).

<a name="WPF461"></a> 
### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)
 Windows Presentation Foundation inclut un certain nombre d’améliorations et de modifications.

 Performances améliorées Le retard de déclenchement d’événements tactiles a été résolu dans le [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]. En outre, la saisie dans un contrôle <xref:System.Windows.Controls.RichTextBox> ne mobilise plus le thread de rendu pendant la saisie rapide.

 Améliorations de la vérification orthographique Le vérificateur orthographique de WPF a été mis à jour sur Windows 8.1 et les versions ultérieures pour tirer parti de la prise en charge, par le système d’exploitation, de la vérification orthographique de langues supplémentaires.  Aucune fonctionnalité n’a été modifiée sur les versions de Windows antérieures à Windows 8.1.

 Comme dans les versions précédentes du .NET Framework, la langue d’un contrôle <xref:System.Windows.Controls.TextBox> ou d’un bloc <xref:System.Windows.Controls.RichTextBox> est détectée en recherchant des informations dans l’ordre suivant :

- `xml:lang`, le cas échéant.

- Langue d’entrée actuelle.

- Culture de thread actuelle.

 Pour plus d’informations sur la prise en charge linguistique dans WPF, consultez le [billet de blog WPF sur les fonctionnalités de .NET Framework 4.6.1](http://go.microsoft.com/fwlink/?LinkID=691819).

 Prise en charge supplémentaire des dictionnaires personnalisés par utilisateur Dans [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], WPF reconnaît les dictionnaires personnalisés qui sont inscrits de manière globale. Cette fonctionnalité est disponible en plus de la possibilité de les inscrire par contrôle.

 Dans les versions précédentes de WPF, les dictionnaires personnalisés ne reconnaissaient pas les listes Mots exclus et Correction automatique. Ils sont pris en charge sur Windows 8.1 et Windows 10 via l’utilisation de fichiers qui peuvent être placés sous le répertoire `%AppData%\Microsoft\Spelling\<language tag>`.  Les règles suivantes s’appliquent à ces fichiers :

- Les fichiers doivent avoir l’extension .dic (pour les mots ajoutés), .exc (pour les mots exclus) ou .acl (pour la correction automatique).

- Les fichiers doivent être en texte brut UTF-16 LE qui commence par la marque d’ordre d’octet.

- Chaque ligne doit comporter un mot (dans les listes de mots ajoutés et exclus) ou une paire de corrections automatiques avec les mots séparés par une barre verticale (« &#124; ») (dans la liste de mots Correction automatique).

- Ces fichiers sont considérés en lecture seule et ne sont pas modifiés par le système.

> [!NOTE]
>  Ces nouveaux formats de fichier ne sont pas directement pris en charge par les API de correction orthographique WPF, et les dictionnaires personnalisés fournis à WPF dans les applications doivent continuer à utiliser les fichiers .lex.

 Exemples Plusieurs [exemples WPF](https://msdn.microsoft.com/library/ms771633.aspx) sont disponibles sur MSDN. Plus de 200 des exemples les plus populaires (en fonction de leur utilisation) seront déplacés vers un [référentiel Open Source GitHub](https://github.com/Microsoft/WPF-Samples). Aidez-nous à améliorer nos exemples en nous envoyant une requête d’extraction ou en ouvrant un [problème GitHub](https://github.com/Microsoft/WPF-Samples/issues).

 WPF inclut un [package NuGet](http://go.microsoft.com/fwlink/?LinkID=691342) qui fournit de nouvelles implémentations de <xref:System.Windows.Interop.D3DImage> facilitant l’interaction avec du contenu DX10 et Dx11. Le code de ce package a été mis en open source et est disponible [sur GitHub](https://github.com/Microsoft/WPFDXInterop).

<a name="WWF461"></a> 
### <a name="windows-workflow-foundation-transactions"></a>Windows Workflow Foundation : Transactions
 La méthode <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A?displayProperty=nameWithType> peut maintenant utiliser un gestionnaire de transactions distribuées autre que MSDTC pour promouvoir la transaction. Pour ce faire, spécifiez un identificateur de promoteur de transaction GUID pour la nouvelle surcharge <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%28System.Transactions.IPromotableSinglePhaseNotification%2CSystem.Guid%29?displayProperty=nameWithType>. Si cette opération réussit, des limitations sont placées sur les fonctionnalités de la transaction. Une fois qu’un promoteur de transaction non MSDTC est inscrit, les méthodes suivantes lèvent un <xref:System.Transactions.TransactionPromotionException>, car elles requièrent une promotion vers MSDTC :

- <xref:System.Transactions.Transaction.EnlistDurable%2A?displayProperty=nameWithType>

- <xref:System.Transactions.TransactionInterop.GetDtcTransaction%2A?displayProperty=nameWithType>

- <xref:System.Transactions.TransactionInterop.GetExportCookie%2A?displayProperty=nameWithType>

- <xref:System.Transactions.TransactionInterop.GetTransmitterPropagationToken%2A?displayProperty=nameWithType>

 Une fois qu’un promoteur de transaction non MSDTC est inscrit, il doit être utilisé pour les futures inscriptions durables en utilisant les protocoles qu’il définit. Vous pouvez obtenir le <xref:System.Guid> du promoteur de transaction à l’aide de la propriété <xref:System.Transactions.Transaction.PromoterType%2A>. Lorsque la transaction est promue, le promoteur de transaction fournit un tableau d’octets (<xref:System.Byte> qui représente le jeton promu. Une application peut obtenir le jeton promu pour une transaction non MSDTC promue à l’aide de la méthode <xref:System.Transactions.Transaction.GetPromotedToken%2A>.

 Les utilisateurs de la nouvelle surcharge <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%28System.Transactions.IPromotableSinglePhaseNotification%2CSystem.Guid%29?displayProperty=nameWithType> doit suivre une séquence d’appel spécifique pour que l’opération de promotion se termine correctement. Ces règles sont documentées dans la documentation de la méthode.

<a name="Profile461"></a> 
### <a name="profiling"></a>Profilage
 L’API de profilage non managée a été améliorée comme suit :

 Meilleure prise en charge de l’accès aux fichiers PDB dans l’interface [ICorProfilerInfo7](../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo7-interface.md) Dans ASP.Net 5, la compilation des assemblys en mémoire par Roslyn est beaucoup plus courante. Pour les développeurs qui créent des outils de profilage, cela signifie que les fichiers PDB qui étaient historiquement sérialisés sur le disque risquent de ne plus être présents. Les outils de profilage utilisent souvent des fichiers PDB pour remapper du code aux lignes sources pour des tâches telles que la couverture du code ou l’analyse des performances ligne par ligne. L’interface [ICorProfilerInfo7](../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo7-interface.md) inclut désormais deux nouvelles méthodes, [ICorProfilerInfo7::GetInMemorySymbolsLength](../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo7-getinmemorysymbolslength-method.md) et [ICorProfilerInfo7::ReadInMemorySymbols](../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo7-readinmemorysymbols.md), qui permettent de fournir ces outils de profilage avec un accès aux données PDB en mémoire. En utilisant les nouvelles API, un profileur peut obtenir le contenu d’un fichier PDB en mémoire sous la forme d’un tableau d’octets, puis le traiter ou le sérialiser sur le disque.

 Meilleure instrumentation avec l’interface ICorProfiler Les profileurs qui utilisent la fonctionnalité ReJit de l’API `ICorProfiler` pour l’instrumentation dynamique peuvent maintenant modifier certaines métadonnées. Précédemment, ces outils pouvaient instrumenter le langage intermédiaire à tout moment, mais les métadonnées ne pouvaient être modifiées qu’au moment du chargement du module. Étant donné que le langage intermédiaire fait référence aux métadonnées, cela limitait les types d’instrumentation qui pouvaient être effectuées. Nous avons levé certaines de ces limites en ajoutant la méthode [ICorProfilerInfo7::ApplyMetaData](../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo7-applymetadata-method.md) pour prendre en charge un sous-ensemble des modifications de métadonnées après le chargement du module, notamment en ajoutant de nouveaux enregistrements `AssemblyRef`, `TypeRef`, `TypeSpec`, `MemberRef`, `MemberSpec` et `UserString`. Cette modification permet une plus large gamme d’instrumentations instantanées possibles.

<a name="NGEN461"></a> 
### <a name="native-image-generator-ngen-pdbs"></a>Fichiers PDB du générateur d’images natives (NGen)
 Le suivi d’événements entre ordinateurs permet aux clients de profiler un programme sur l’Ordinateur A et d’examiner les données de profilage avec le mappage des lignes sources sur l’Ordinateur B. Avec les versions antérieures du .NET Framework, l’utilisateur devait copier tous les modules et les images natives de l’ordinateur profilé vers l’ordinateur d’analyse qui contenait le fichier PDB en langage intermédiaire pour créer le mappage du code source au code natif. Ce processus peut fonctionner correctement lorsque les fichiers sont relativement petits, comme pour les applications de téléphone. Toutefois, les fichiers peuvent être très volumineux sur des systèmes de bureau et leur copie peut prendre beaucoup de temps.

 Avec les fichiers PDB de NGen, NGen peut créer un fichier PDB qui contient le mappage du langage intermédiaire au code natif sans dépendance sur le fichier PDB en langage intermédiaire. Dans notre scénario de suivi d’événements entre ordinateurs, il suffit de copier le fichier PDB de l’image native généré par l’Ordinateur A sur l’Ordinateur B et d’utiliser les [API Debug Interface Access](/visualstudio/debugger/debug-interface-access/debug-interface-access-sdk-reference) pour lire le mappage du code source au code en langage intermédiaire du fichier PDB en langage intermédiaire et le mappage du code en langage intermédiaire au code natif du fichier PDB de l’image native. La combinaison des deux mappages fournit un mappage du code source au code natif. Étant donné que le fichier PDB de l’image native est beaucoup plus petit que l’ensemble des modules et images natives, le processus de copie de l’Ordinateur A vers l’Ordinateur B est beaucoup plus rapide.

<a name="v46"></a> 
## <a name="whats-new-in-net-2015"></a>Nouveautés du .NET 2015
 .NET 2015 introduit le [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] et .NET Core. Certaines nouvelles fonctionnalités s'appliquent aux deux infrastructures, alors que d'autres sont spécifiques à [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] ou [!INCLUDE[net_core](../../../includes/net-core-md.md)].

- **ASP.NET 5**

     .NET 2015 inclut ASP.NET 5, qui est une implémentation .NET pour la création d’applications cloud modernes. ASP.NET 5 est modulable, ce qui vous permet d’inclure uniquement les fonctionnalités nécessaires dans votre application. Elle peut être hébergée sur IIS ou auto-hébergée dans un processus personnalisé. Par ailleurs, vous pouvez exécuter les applications avec différentes versions du .NET Framework sur le même serveur. Elle inclut un nouveau système de configuration d'environnement conçu pour le déploiement cloud.

     MVC, les API web et les pages web sont unifiés dans une infrastructure unique appelée MVC 6. Vous créez des applications ASP.NET 5 via les nouveaux outils de Visual Studio 2015. Vos applications existantes fonctionneront sur le nouveau .NET Framework. Toutefois, pour générer une application qui utilise MVC 6 ou SignalR 3, vous devez utiliser le système de projet de Visual Studio 2015.

     Pour plus d’informations, consultez [ASP.NET 5](http://go.microsoft.com/fwlink/?LinkId=518238).

- **Mises à jour ASP.NET**

    - **API basée sur des tâches pour le vidage de réponse asynchrone**

         ASP.NET fournit désormais une API simple basée sur des tâches pour le vidage de réponse asynchrone, <xref:System.Web.HttpResponse.FlushAsync%2A?displayProperty=nameWithType>, qui autorise les réponses à être vidées de façon asynchrone à l'aide du support `async/await` de votre langue.

    - `Model binding supports task-returning methods`

         Dans le [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], ASP.NET a ajouté une fonctionnalité de liaison de modèle qui autorise une approche extensible, axée sur le code pour les opérations de données CRUD dans les contrôles utilisateur et les pages Web Forms. Le système de liaison de modèle prend désormais en charge les méthodes de liaison de modèle avec renvoi de <xref:System.Threading.Tasks.Task>. Cette fonctionnalité permet aux développeurs de Web Forms d'obtenir les avantages de la scalabilité du modèle asynchrone et la simplicité du système de liaison de données lorsqu'ils utilisent les versions plus récentes des ORM, y compris l'Entity Framework.

         La liaison de modèle asynchrone est contrôlée par le paramètre de configuration `aspnet:EnableAsyncModelBinding`.

        ```xml
        <appSettings>
           <add key=" aspnet:EnableAsyncModelBinding" value="true|false" />
        </appSettings>
        ```

         Sur les applications qui ciblent le [!INCLUDE[net_v46](../../../includes/net-v46-md.md)], sa valeur par défaut est `true`. Sur les applications s'exécutant sur le [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] qui ciblent une version antérieure du .NET Framework, sa valeur par défaut est `false`. Son activation s'obtient en définissant le paramètre de configuration avec la valeur `true`.

    - **Prise en charge de HTTP/2 (Windows 10)**

         [HTTP/2](http://www.wikipedia.org/wiki/HTTP/2) est une nouvelle version du protocole HTTP qui offre une bien meilleure utilisation de la connexion (moins d’allers-retours entre le client et le serveur), ce qui réduit la latence pendant le chargement des pages web pour les utilisateurs.  Ce sont les pages web (par opposition aux services) qui profitent le plus de HTTP/2, car le protocole optimise les demandes de plusieurs artefacts dans une expérience unique. La prise en charge de HTTP/2 a été ajoutée à ASP.NET dans le .NET Framework 4.6. Étant donné que les fonctionnalités réseau existent sur plusieurs couches, de nouvelles fonctionnalités ont dû être rajoutées dans Windows, IIS et ASP.NET pour activer HTTP/2. Vous devez exécuter Windows 10 pour utiliser HTTP/2 avec ASP.NET.

         HTTP/2 est également pris en charge et activé par défaut sur les applications UWP Windows 10 qui utilisent l'API <xref:System.Net.Http.HttpClient?displayProperty=nameWithType>.

         Afin de fournir un moyen d’utiliser la fonctionnalité [PUSH_PROMISE](http://http2.github.io/http2-spec/#PUSH_PROMISE) dans les applications ASP.NET, une nouvelle méthode avec deux surcharges, <xref:System.Web.HttpResponse.PushPromise%28System.String%29> et <xref:System.Web.HttpResponse.PushPromise%28System.String%2CSystem.String%2CSystem.Collections.Specialized.NameValueCollection%29>, a été ajoutée à la classe <xref:System.Web.HttpResponse>.

        > [!NOTE]
        >  Alors qu’ASP.NET 5 prend en charge HTTP/2, la prise en charge de la fonctionnalité PUSH PROMISE n’a pas encore été ajoutée.

         Le navigateur et le serveur web (IIS sur Windows) effectuent tout le travail. Vous n'avez pas de tâches lourdes à effectuer pour vos utilisateurs.

         La plupart des [principaux navigateurs prennent en charge HTTP/2](http://www.wikipedia.org/wiki/HTTP/2). Il est donc probable que vos utilisateurs bénéficient de la prise en charge de HTTP/2 si tel est le cas de votre serveur.

    - **Prise en charge du protocole de liaison de jeton**

         Microsoft et Google ont travaillé en collaboration sur une nouvelle approche de l’authentification, appelée le [Protocole de liaison de jeton](https://github.com/TokenBinding/Internet-Drafts). Cette approche part du principe que les jetons d’authentification (dans le cache de votre navigateur) peuvent être volés et utilisés par des personnes mal intentionnées pour accéder à des ressources sécurisées (par exemple, votre compte bancaire) sans avoir besoin de connaître votre mot de passe ou toute autre information confidentielle. Le nouveau protocole vise à contenir ce problème.

         Le protocole de liaison de jeton sera implémenté dans Windows 10 en tant que fonctionnalité du navigateur. Les applications ASP.NET participeront au protocole, en validant les jetons d'authentification pour qu'ils soient légitimes. Les implémentations côté client et serveur établissent la protection de bout en bout spécifiée par le protocole.

    - **Algorithmes de hachage de chaîne aléatoire**

         Le .NET Framework 4.5 a introduit un [algorithme de hachage de chaîne aléatoire](../configure-apps/file-schema/runtime/userandomizedstringhashalgorithm-element.md). Cependant, il n'est pas pris en charge par ASP.NET en raison de certaines fonctionnalités ASP.NET fondées sur un code de hachage stable. Dans [!INCLUDE[net_v46](../../../includes/net-v46-md.md)], les algorithmes de hachage de chaîne aléatoire sont désormais pris en charge. Pour activer cette fonctionnalité, utilisez le paramètre de configuration `aspnet:UseRandomizedStringHashAlgorithm`.

        ```xml
        <appSettings>
           <add key="aspnet:UseRandomizedStringHashAlgorithm" value="true|false" />
        </appSettings>
        ```

- **ADO.NET**

     ADO .NET prend désormais en charge la fonctionnalité Toujours chiffré disponible dans SQL Server 2016 version préliminaire CTP2 (Community Technology Preview 2). Avec la fonctionnalité Toujours chiffré, SQL Server peut effectuer des opérations sur des données chiffrées, et surtout, la clé de chiffrement est stockée avec l'application à l'intérieur de l'environnement approuvé du client, et non pas sur le serveur. La fonctionnalité Toujours chiffré sécurise les données du client de sorte que les administrateurs de base de données n'ont pas accès aux données en texte brut. Le chiffrement et le déchiffrement de données se produit de manière transparente au niveau du pilote, ce qui réduit des modifications à apporter aux applications existantes. Pour plus d’informations, consultez [Always Encrypted (moteur de base de données)](/sql/relational-databases/security/encryption/always-encrypted-database-engine) et [Always Encrypted (développement client)](/sql/relational-databases/security/encryption/always-encrypted-client-development).

- **Compilateur JIT 64 bits pour le code managé**

     Le .NET Framework 4.6 propose une nouvelle version du compilateur JIT 64 bits (anciennement RyuJIT). Le nouveau compilateur 64 bits offre des améliorations significatives des performances par rapport à l'ancien compilateur JIT 64 bits. Le nouveau compilateur 64 bits est activé pour les processus 64 bits qui s'exécutent au-dessus du .NET Framework 4.6. Votre application s'exécute dans un processus 64 bits s'il est compilé en mode 64 bits ou AnyCPU, et s'exécute sur un système d'exploitation 64 bits. Bien que toutes les mesures nécessaires aient été prises pour que la transition vers le nouveau compilateur soit aussi transparente que possible, des modifications du comportement sont possibles. Nous aimerions connaître directement les problèmes que vous pourriez rencontrer lorsque vous utilisez le nouveau compilateur JIT. Veuillez nous contacter par l’intermédiaire de [Microsoft Connect](http://connect.microsoft.com/) pour tout problème susceptible d’être lié au nouveau compilateur JIT 64 bits.

     Le nouveau compilateur JIT 64 bits inclut également des fonctionnalités d'accélération matérielle SIMD en cas d'association aux types SIMD de l'espace de noms <xref:System.Numerics>, ce qui peut produire une bonne amélioration des performances.

- **Améliorations du chargeur d’assembly**

     Le chargeur d'assembly utilise désormais la mémoire plus efficacement en déchargeant les assemblys IL après le chargement d'une image NGEN correspondante. Cette modification réduit la mémoire virtuelle, ce qui est particulièrement utile pour les grandes applications 32 bits (tels que Visual Studio), et économise aussi la mémoire physique.

- **Changements des bibliothèques de classes de base**

     Plusieurs nouvelles API ont été ajoutées à [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] pour des scénarios clés. Vous remarquerez les changements et les ajouts suivants :

    - **Implémentations d’IReadOnlyCollection\<T>**

         Des collections supplémentaires implémentent <xref:System.Collections.Generic.IReadOnlyCollection%601>, comme <xref:System.Collections.Generic.Queue%601> et <xref:System.Collections.Generic.Stack%601>.

    - **CultureInfo.CurrentCulture et CultureInfo.CurrentUICulture**

         Les propriétés <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> et <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> sont désormais en lecture et en écriture, et non plus en lecture seule. Si vous affectez un nouvel objet <xref:System.Globalization.CultureInfo> à ces propriétés, la culture du thread actuel définie par la propriété `Thread.CurrentThread.CurrentCulture` et la culture du thread d'interface utilisateur actuel définie par les propriétés `Thread.CurrentThread.CurrentUICulture` changent également.

    - **Améliorations apportées au garbage collection (GC)**

         La classe <xref:System.GC> inclut désormais les méthodes <xref:System.GC.TryStartNoGCRegion%2A> et <xref:System.GC.EndNoGCRegion%2A>, qui vous permettent d'interdire le garbage collection durant l'exécution d'un chemin critique.

         Une nouvelle surcharge de la méthode <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%2CSystem.Boolean%29?displayProperty=nameWithType> vous permet de contrôler si le tas de petits objets et le tas d'objets volumineux sont rangés et compactés, ou rangés uniquement.

    - **Types SIMD**

         L'espace de noms <xref:System.Numerics> inclut désormais un certain nombre de types SIMD, tels que <xref:System.Numerics.Matrix3x2>, <xref:System.Numerics.Matrix4x4>, <xref:System.Numerics.Plane>, <xref:System.Numerics.Quaternion>, <xref:System.Numerics.Vector2>, <xref:System.Numerics.Vector3> et <xref:System.Numerics.Vector4>.

         Comme le nouveau compilateur JIT 64 bits inclut également des fonctionnalités d'accélération matérielle SIMD, il en découle une amélioration des performances particulièrement significative lorsque vous utilisez les types SIMD avec le nouveau compilateur JIT 64 bits.

    - **Mises à jour du chiffrement**

         L’API <xref:System.Security.Cryptography?displayProperty=nameWithType> est mise à jour pour prendre en charge les [API de chiffrement CNG de Windows](https://msdn.microsoft.com/library/windows/desktop/aa376214.aspx). Jusqu’à présent, le .NET Framework reposait entièrement sur une [version antérieure des API de chiffrement Windows](https://msdn.microsoft.com/library/windows/desktop/aa380255.aspx) comme base d’implémentation de <xref:System.Security.Cryptography?displayProperty=nameWithType>. Nous avons reçu des demandes pour la prise en charge de l’API CNG, car elle prend en charge les [algorithmes de chiffrement modernes](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx#suite_b_support), qui sont importants pour certaines catégories d’applications.

         Le .NET Framework 4.6 inclut les améliorations suivantes pour prendre en charge l'API de chiffrement CNG de Windows :

        - Un ensemble de méthodes d'extension pour les certificats X509, `System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPublicKey(System.Security.Cryptography.X509Certificates.X509Certificate2)` et `System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey(System.Security.Cryptography.X509Certificates.X509Certificate2)`, qui retourne une implémentation CNG plutôt qu'une implémentation CAPI lorsque cela est possible. (Certaines cartes à puce, etc., nécessitent toujours CAPI, et les API gèrent le secours).

        - La classe <xref:System.Security.Cryptography.RSACng?displayProperty=nameWithType>, qui fournit une implémentation CNG de l'algorithme RSA.

        - Améliorations apportées à l'API RSA afin que les opérations courantes ne nécessitent plus de conversion. Par exemple, le chiffrement des données utilisant un objet <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> nécessite un code comme celui qui suit dans les versions antérieures du .NET Framework.

             [!code-csharp[WhatsNew.Casting#1](../../../samples/snippets/csharp/VS_Snippets_CLR/whatsnew.casting/cs/program.cs#1)]
             [!code-vb[WhatsNew.Casting#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.casting/vb/module1.vb#1)]

             Le code qui utilise les nouvelles API de chiffrement dans le .NET Framework 4.6 peut être réécrit comme suit pour éviter la conversion.

             [!code-csharp[WhatsNew.Casting#2](../../../samples/snippets/csharp/VS_Snippets_CLR/whatsnew.casting/cs/program.cs#2)]
             [!code-vb[WhatsNew.Casting#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.casting/vb/module1.vb#2)]

    - **Prise en charge de la conversion des dates et heures vers ou à partir d’Unix**

         Les nouvelles méthodes suivantes ont été ajoutées à la structure <xref:System.DateTimeOffset> pour prendre en charge la conversion des valeurs de date et d'heure vers ou depuis Unix :

        - <xref:System.DateTimeOffset.FromUnixTimeSeconds%2A?displayProperty=nameWithType>

        - <xref:System.DateTimeOffset.FromUnixTimeMilliseconds%2A?displayProperty=nameWithType>

        - <xref:System.DateTimeOffset.ToUnixTimeSeconds%2A?displayProperty=nameWithType>

        - <xref:System.DateTimeOffset.ToUnixTimeMilliseconds%2A?displayProperty=nameWithType>

    - **Commutateurs de compatibilité**

         La nouvelle classe <xref:System.AppContext> ajoute une fonctionnalité de compatibilité qui permet aux auteurs de bibliothèque de fournir un mécanisme de désactivation uniforme des nouvelles fonctionnalités pour les utilisateurs. Elle établit un contrat souple entre les composants pour la communication des demandes de désactivation. Cette fonctionnalité est particulièrement importante quand une modification est apportée aux fonctionnalités existantes. À l'inverse, il existe déjà une activation implicite des nouvelles fonctionnalités.

         Avec <xref:System.AppContext>, les bibliothèques définissent et exposent des commutateurs de compatibilité, tandis que le code qui en dépend peut définir ces commutateurs pour qu'ils aient un impact sur le comportement de la bibliothèque. Par défaut, les bibliothèques fournissent la nouvelle fonctionnalité et ne peuvent la modifier (c'est-à-dire fournir la version antérieure) que si le commutateur est défini.

         Une application (ou une bibliothèque) peut déclarer la valeur d'un commutateur (qui est toujours une valeur <xref:System.Boolean>) définie par une bibliothèque dépendante. Le commutateur a toujours implicitement la valeur `false`. En définissant le commutateur avec la valeur `true`, vous l'activez. En définissant explicitement le commutateur avec la valeur `false`, vous obtenez le nouveau comportement.

        ```csharp
        AppContext.SetSwitch("Switch.AmazingLib.ThrowOnException", true);
        ```

         La bibliothèque doit vérifier si un consommateur a déclaré la valeur du commutateur et s'il l'utilise ensuite correctement.

        ```csharp
        if (!AppContext.TryGetSwitch("Switch.AmazingLib.ThrowOnException", out shouldThrow)) 
        {
           // This is the case where the switch value was not set by the application. 
           // The library can choose to get the value of shouldThrow by other means. 
           // If no overrides nor default values are specified, the value should be 'false'. 
           // A false value implies the latest behavior.
        }

           // The library can use the value of shouldThrow to throw exceptions or not.
           if (shouldThrow) 
           {
              // old code
           }
           else {
              // new code
           }
        }
        ```

         Il est préférable d'utiliser un format homogène pour les commutateurs, car ils constituent un contrat formel exposé par une bibliothèque. Voici les deux formats évidents.

        - *Commutateur*.*espace de noms*.*nom_commutateur*

        - *Commutateur*.*bibliothèque*.*nom_commutateur*

    - **Changements apportés au modèle asynchrone basé sur les tâches (TAP)**

         Pour les applications qui ciblent le [!INCLUDE[net_v46](../../../includes/net-v46-md.md)], les objets <xref:System.Threading.Tasks.Task> et <xref:System.Threading.Tasks.Task%601> héritent de la culture et de la culture d'interface utilisateur du thread appelant. Le comportement des applications qui ciblent les versions antérieures du .NET Framework, ou qui ne ciblent pas une version spécifique du .NET Framework n'est pas affecté. Pour plus d'informations, consultez la section « Culture et opérations asynchrones basées sur les tâches » de la rubrique relative à la classe <xref:System.Globalization.CultureInfo>.

         La classe <xref:System.Threading.AsyncLocal%601?displayProperty=nameWithType> permet de représenter les données ambiantes locales à un flux de contrôle asynchrone donné, par exemple une méthode `async`. Elle peut être utilisée pour conserver les données entre plusieurs threads. Vous pouvez également définir une méthode de rappel qui est avertie chaque fois que les données ambiantes changent, soit parce que la propriété <xref:System.Threading.AsyncLocal%601.Value%2A?displayProperty=nameWithType> a été modifiée explicitement, soit parce que le thread a rencontré une transition de contexte.

         Trois méthodes pratiques, <xref:System.Threading.Tasks.Task.CompletedTask%2A?displayProperty=nameWithType>, <xref:System.Threading.Tasks.Task.FromCanceled%2A?displayProperty=nameWithType> et <xref:System.Threading.Tasks.Task.FromException%2A?displayProperty=nameWithType>, ont été ajoutées au modèle asynchrone basé sur des tâches (TAP) pour retourner les tâches terminées dans un état particulier.

         La classe <xref:System.IO.Pipes.NamedPipeClientStream> prend désormais en charge la communication asynchrone avec sa nouvelle méthode <xref:System.IO.Pipes.NamedPipeClientStream.ConnectAsync%2A> .

    - **EventSource prend désormais en charge l’écriture dans le journal des événements**

         Vous pouvez maintenant utiliser la classe <xref:System.Diagnostics.Tracing.EventSource> pour enregistrer les messages administratifs ou opérationnels dans le journal des événements, en plus des sessions ETW existantes créées sur l'ordinateur. Par le passé, vous deviez utiliser le package Microsoft.Diagnostics.Tracing.EventSource NuGet pour cette fonctionnalité. Cette fonctionnalité est désormais intégrée au .NET Framework 4.6.

         Le package NuGet et le 4.6 Framework .NET ont tous deux été mis à jour avec les fonctionnalités suivantes :

        - **Événements dynamiques**

             Permet que les événements soient définis « à la volée », sans créer de méthodes d'événement.

        - **Charges utiles enrichies**

             Permet que les tableaux et les classes avec attributs spécifiques, ainsi que les types primitifs, soient transmis comme charge utile

        - **Suivi des activités**

             Tous les événements entre les événements de début et de fin sont marqués avec un ID qui représente toutes les activités en cours.

         Pour prendre en charge ces fonctionnalités, la méthode <xref:System.Diagnostics.Tracing.EventSource.Write%2A> surchargée a été ajoutée à la classe <xref:System.Diagnostics.Tracing.EventSource>.

- **Windows Presentation Foundation (WPF)**

    - **Améliorations HDPI**

         La prise en charge HDPI dans WPF est désormais mieux assurée dans le [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]. Des améliorations ont été apportées à l'arrondi de disposition pour réduire les instances de découpage dans les contrôles avec bordures. Par défaut, cette fonctionnalité est activée uniquement si votre <xref:System.Runtime.Versioning.TargetFrameworkAttribute> a la valeur .NET 4.6.  Les applications qui ciblent les versions antérieures du framework mais qui s’exécutent sur le [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] peuvent adopter le nouveau comportement en ajoutant la ligne suivante à la section [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) du fichier app.config :

        ```xml
        <AppContextSwitchOverrides
        value="Switch.MS.Internal.DoNotApplyLayoutRoundingToMarginsAndBorderThickness=false"
        />
        ```

         Les fenêtres WPF chevauchant plusieurs écrans avec différents paramètres DPI (programme d'installation multi-DPI) sont à présent restituées entièrement sans zones obscurcies. Vous pouvez désactiver ce comportement en ajoutant la ligne suivante à la section `<appSettings>` du fichier app.config :

        ```xml
        <add key="EnableMultiMonitorDisplayClipping" value="true"/>
        ```

         La prise en charge du chargement automatique du curseur approprié selon le paramètre DPI a été ajoutée à <xref:System.Windows.Input.Cursor?displayProperty=nameWithType>.

    - **Meilleure interaction tactile**

         Les rapports de clients sur [Connect](https://connect.microsoft.com/VisualStudio/feedback/details/903760/) selon lesquels l’interaction tactile produisait un comportement imprévisible ont été traités dans [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]. Le seuil de double appui pour les applications du Windows Store et les applications WPF est maintenant le même que dans Windows 8.1 et versions ultérieures.

    - **Prise en charge transparente des fenêtres enfants**

         WPF dans le [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] prend en charge les fenêtres enfants transparentes dans Windows 8.1 et versions ultérieures. Cela vous permet de créer des fenêtres enfants non rectangulaires et transparentes dans vos fenêtres de niveau supérieur. Vous pouvez désactiver cette fonctionnalité en affectant à la propriété <xref:System.Windows.Interop.HwndSourceParameters.UsesPerPixelTransparency%2A?displayProperty=nameWithType> la valeur `true`.

- **Windows Communication Foundation (WCF)**

    - **Prise en charge SSL**

         WCF prend désormais en charge la version TLS 1.1 et TLS 1.2 de SSL, en plus de SSL 3.0 et TLS 1.0, lorsque vous utilisez NetTcp avec l'authentification client et la sécurité de transport. Il est désormais possible de sélectionner le protocole à utiliser, ou de désactiver les anciens protocoles moins sécurisés. Cela peut être effectué en définissant la propriété <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A> ou en ajoutant le code suivant à un fichier de configuration.

        ```xml
        <netTcpBinding>
           <binding>
              <security mode= "None|Transport|Message|TransportWithMessageCredential" >
                 <transport clientCredentialType="None|Windows|Certificate"
                            protectionLevel="None|Sign|EncryptAndSign"
                            sslProtocols="Ssl3|Tls1|Tls11|Tls12">
                    </transport>
              </security>
           </binding>
        </netTcpBinding>
        ```

    - **Envoi de messages à l’aide de différentes connexions HTTP**

         WCF permet désormais aux utilisateurs de s'assurer que certains messages sont envoyés à l'aide de différentes connexions HTTP sous-jacentes. Il existe deux façons d'effectuer cette opération :

        - **Utilisation d’un préfixe de nom de groupe de connexion**

             Les utilisateurs peuvent spécifier une chaîne que WCF utilisera comme préfixe du nom de groupe de connexion. Deux messages avec des préfixes différents sont envoyés à l'aide de différentes connexions HTTP sous-jacentes. Vous définissez le préfixe en ajoutant une paire clé/valeur à la propriété <xref:System.ServiceModel.Channels.Message.Properties%2A?displayProperty=nameWithType> du message. La clé est « HttpTransportConnectionGroupNamePrefix » ; la valeur est le préfixe souhaité.

        - **Utilisation de différentes fabriques de canaux**

             Les utilisateurs peuvent aussi activer une fonctionnalité qui permet de s'assurer que les messages envoyés à l'aide de canaux créés par différentes fabriques de canaux utilisent différentes connexions HTTP sous-jacentes. Pour activer cette fonctionnalité, les utilisateurs doivent définir la propriété `appSetting` suivante avec la valeur `true` :

            ```xml
            <appSettings>
               <add key="wcf:httpTransportBinding:useUniqueConnectionPoolPerFactory" value="true" />
            </appSettings>
            ```

- **Windows Workflow Foundation (WWF)**

     Vous pouvez maintenant spécifier le nombre de secondes pendant lesquelles un service de workflow maintient une demande d'opération exceptionnelle quand il existe un signet « non-protocole » en attente avant l'expiration de la demande. Un signet « non-protocole » est un signet qui n'est pas lié à des activités de réception en attente. Comme certaines activités créent des signets non-protocole dans leur implémentation, il peut ne pas être évident qu'un signet non-protocole existe. Ceux-ci incluent État et Prélèvement. Par conséquent, si vous avez un service de workflow mis en œuvre avec une machine à états ou contenant une activité de prélèvement, vous aurez probablement des signets non-protocole. Vous spécifiez l'intervalle en ajoutant la ligne suivante à la section `appSettings` de votre fichier app.config :

    ```xml
    <add key="microsoft:WorkflowServices:FilterResumeTimeoutInSeconds" value="60"/>
    ```

     La valeur par défaut est 60 secondes. Si `value` a la valeur 0, les demandes exceptionnelles sont immédiatement rejetées comme erreur avec un texte tel que le suivant :

    ```
    Operation 'Request3|{http://tempuri.org/}IService' on service instance with identifier '2b0667b6-09c8-4093-9d02-f6c67d534292' cannot be performed at this time. Please ensure that the operations are performed in the correct order and that the binding in use provides ordered delivery guarantees. 
    ```

     C'est le même message que vous recevez en cas d'opération exceptionnelle et d'absence de signet non-protocole.

     Si la valeur de l'élément `FilterResumeTimeoutInSeconds` est différente de zéro, il existe des signets non-protocole, l'intervalle de délai d'attente expire et l'opération échoue avec un message d'expiration.

- **Transactions**

     Vous pouvez maintenant inclure l'identificateur de transaction distribuée pour la transaction ayant provoqué la levée d'une exception dérivée de <xref:System.Transactions.TransactionException>. Pour ce faire, ajoutez la clé suivante à la section `appSettings` de votre fichier app.config :

    ```xml
    <add key="Transactions:IncludeDistributedTransactionIdInExceptionMessage" value="true"/> 
    ```

     La valeur par défaut est `false`.

- **Mise en réseau**

    - **Réutilisation de socket**

         Windows 10 inclut un nouvel algorithme de mise en réseau à haute scalabilité qui améliore l'utilisation des ressources de l'ordinateur en réutilisant les ports locaux pour les connexions TCP sortantes. Le .NET Framework 4.6 prend en charge le nouvel algorithme, permettant aux applications .NET de tirer parti du nouveau comportement. Dans les précédentes versions de Windows, il y avait une limite artificielle de connexions simultanées (généralement 16 384, taille par défaut de la plage de ports dynamiques), ce qui pouvait limiter la scalabilité d'un service en provoquant l'épuisement du port sous charge.

         Dans le [!INCLUDE[net_v46](../../../includes/net-v46-md.md)], deux nouvelles API ont été ajoutées pour permettre la réutilisation de port, ce qui supprime la limite de 64 Ko sur les connexions simultanées :

        - Valeur de l'énumération <xref:System.Net.Sockets.SocketOptionName?displayProperty=nameWithType>.

        - La propriété <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=nameWithType>.

         Par défaut, la propriété <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=nameWithType> est `false` sauf si la valeur `HWRPortReuseOnSocketBind` de la clé de Registre `HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319` est définie sur 0x1. Pour activer la réutilisation de port local sur les connexions HTTP, définissez la propriété <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=nameWithType> avec la valeur `true`. Toutes les connexions de socket TCP sortantes de <xref:System.Net.Http.HttpClient> et <xref:System.Net.HttpWebRequest> sont alors contraintes d’utiliser une nouvelle option de socket Windows 10, [SO_REUSE_UNICASTPORT](https://msdn.microsoft.com/library/windows/desktop/ms740532.aspx), qui permet la réutilisation du port local.

         Les développeurs écrivant une application de sockets uniquement peuvent spécifier l'option <xref:System.Net.Sockets.SocketOptionName?displayProperty=nameWithType> lors de l'appel d'une méthode telle que <xref:System.Net.Sockets.Socket.SetSocketOption%2A?displayProperty=nameWithType> afin que les sockets sortants réutilisent les ports locaux lors de la liaison.

    - **Prise en charge des noms de domaine internationaux et PunyCode**

         Une nouvelle propriété, <xref:System.Uri.IdnHost%2A>, a été ajoutée à la classe <xref:System.Uri> pour mieux prendre en charge les noms de domaine internationaux et PunyCode.

- **Redimensionnement dans les contrôles Windows Forms.**

     Cette fonctionnalité a été développée dans [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] pour inclure les types <xref:System.Windows.Forms.DomainUpDown>, <xref:System.Windows.Forms.NumericUpDown>, <xref:System.Windows.Forms.DataGridViewComboBoxColumn>, <xref:System.Windows.Forms.DataGridViewColumn> et <xref:System.Windows.Forms.ToolStripSplitButton>, et le rectangle spécifié par la propriété <xref:System.Drawing.Design.PaintValueEventArgs.Bounds%2A> utilisée durant le dessin de <xref:System.Drawing.Design.UITypeEditor>.

     Il est nécessaire d'accepter cette fonctionnalité. Pour l'activer, affectez à l'élément `EnableWindowsFormsHighDpiAutoResizing` la valeur `true` dans le fichier de configuration de l'application (app.config) :

    ```xml
    <appSettings>
       <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />
    </appSettings>
    ```

- **Prise en charge des codages de pages de codes**

      [!INCLUDE[net_core](../../../includes/net-core-md.md)] primarily supports the Unicode encodings and by default provides limited support for code page encodings. You can add support for code page encodings available in the .NET Framework but unsupported in [!INCLUDE[net_core](../../../includes/net-core-md.md)] by registering code page encodings with the <xref:System.Text.Encoding.RegisterProvider%2A?displayProperty=nameWithType> method. For more information, see <xref:System.Text.CodePagesEncodingProvider?displayProperty=nameWithType>.

- **.NET Native**

     Les applications Windows pour Windows 10 qui ciblent le [!INCLUDE[net_core](../../../includes/net-core-md.md)] et sont écrites en C# ou Visual Basic peuvent désormais tirer parti d'une nouvelle technologie qui compile les applications en code natif plutôt qu'en code IL (Intermediate Language). Il en résulte des applications caractérisées par un démarrage plus rapide et un temps d'exécution accéléré. Pour plus d’informations, consultez [Compilation d’applications avec .NET Native](../../../docs/framework/net-native/index.md). Pour obtenir une vue d’ensemble de .NET Native illustrant sa différence par rapport à la compilation JIT et NGEN, et pour connaître ses implications au niveau de votre code, consultez [Compilation et .NET Native](../../../docs/framework/net-native/net-native-and-compilation.md).

     Vos applications sont compilées en code natif par défaut dans Visual Studio 2015. Pour plus d’informations, consultez [Prise en main de .NET Native](../../../docs/framework/net-native/getting-started-with-net-native.md).

     Pour permettre la prise en charge du débogage des applications .NET Native, un certain nombre de nouvelles interfaces et d'énumérations ont été ajoutées à l'API de débogage non managée. Pour plus d’informations, consultez la rubrique [Débogage (Référence des API non managées)](../../../docs/framework/unmanaged-api/debugging/index.md).

- **Packages du .NET Framework open source**

      [!INCLUDE[net_core](../../../includes/net-core-md.md)] packages such as the immutable collections, [SIMD APIs](http://go.microsoft.com/fwlink/?LinkID=518639), and networking APIs such as those found in the <xref:System.Net.Http> namespace are now available as open source packages on [GitHub](https://github.com/). To access the code, see [NetFx on GitHub](http://go.microsoft.com/fwlink/?LinkID=518634). For more information and how to contribute to these packages, see [.NET Core and Open-Source](../../../docs/framework/get-started/net-core-and-open-source.md), [.NET Home Page on GitHub](http://go.microsoft.com/fwlink/?LinkID=518635).

 [Retour au début](#introduction)

<a name="v452"></a> 
## <a name="whats-new-in-the-net-framework-452"></a>Nouveautés dans le .NET Framework 4.5.2

- **Nouvelles API pour les applications ASP.NET.** Les nouvelles méthodes <xref:System.Web.HttpResponse.AddOnSendingHeaders%2A?displayProperty=nameWithType> et <xref:System.Web.HttpResponseBase.AddOnSendingHeaders%2A?displayProperty=nameWithType> vous permettent d'inspecter et de modifier les en-têtes de réponse et le code d'état au moment où la réponse est vidée dans l'application cliente. Envisagez d'utiliser ces méthodes au lieu des événements <xref:System.Web.HttpApplication.PreSendRequestHeaders> et <xref:System.Web.HttpApplication.PreSendRequestContent> ; elles sont plus efficaces et fiables.

     La méthode <xref:System.Web.Hosting.HostingEnvironment.QueueBackgroundWorkItem%2A?displayProperty=nameWithType> vous permet de planifier des petits éléments de travail en arrière-plan. ASP.NET effectue le suivi de ces éléments et empêche IIS de mettre fin brutalement au processus de traitement tant que tous les éléments de travail en arrière-plan ne sont pas terminés. Cette méthode ne peut pas être appelée en dehors d'un domaine d'application managée ASP.NET.

     Les nouvelles propriétés <xref:System.Web.HttpResponse.HeadersWritten?displayProperty=nameWithType> et <xref:System.Web.HttpResponseBase.HeadersWritten?displayProperty=nameWithType> retournent des valeurs booléennes qui indiquent si les en-têtes de réponse ont été écrits. Vous pouvez utiliser ces propriétés pour vous assurer que les appels d'API comme <xref:System.Web.HttpResponse.StatusCode%2A?displayProperty=nameWithType> (qui lèvent des exceptions si les en-têtes ont été écrits) vont réussir.

- **Redimensionnement dans les contrôles Windows Forms.** Cette fonctionnalité a été étendue. Vous pouvez maintenant utiliser le paramètre PPP système pour redimensionner les composants des contrôles supplémentaires suivants (par exemple, la flèche déroulante vers le bas dans les zones de liste modifiable) :

     <xref:System.Windows.Forms.ComboBox>    <xref:System.Windows.Forms.ToolStripComboBox>    <xref:System.Windows.Forms.ToolStripMenuItem>    <xref:System.Windows.Forms.Cursor>    <xref:System.Windows.Forms.DataGridView>    <xref:System.Windows.Forms.DataGridViewComboBoxColumn>

     Il est nécessaire d'accepter cette fonctionnalité. Pour l'activer, affectez à l'élément `EnableWindowsFormsHighDpiAutoResizing` la valeur `true` dans le fichier de configuration de l'application (app.config) :

    ```xml
    <appSettings>
       <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />
    </appSettings>
    ```

- **Nouvelle fonctionnalité de flux de travail.** Un gestionnaire de ressources qui utilise la méthode <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> (et qui implémente donc l'interface <xref:System.Transactions.IPromotableSinglePhaseNotification>) peut utiliser la nouvelle méthode <xref:System.Transactions.Transaction.PromoteAndEnlistDurable%2A?displayProperty=nameWithType> pour demander :

    - La promotion de la transaction en transaction MSDTC (Microsoft Distributed Transaction Coordinator)

    - le remplacement de <xref:System.Transactions.IPromotableSinglePhaseNotification> par <xref:System.Transactions.ISinglePhaseNotification>, qui correspond à une inscription durable qui prend en charge les validations en une seule phase.

     Ces demandes peuvent être faites au sein du même domaine d'application et ne nécessitent pas de code non managé supplémentaire pour interagir avec MSDTC pour effectuer la promotion. La nouvelle méthode peut uniquement être appelée quand il existe un appel en suspens de <xref:System.Transactions?displayProperty=nameWithType> à la méthode <xref:System.Transactions.IPromotableSinglePhaseNotification> `Promote` qui est implémentée par l’inscription pouvant être promue.

- **Améliorations du profilage.** Les nouvelles API de profilage non managées suivantes proposent un profilage plus robuste :

     [COR_PRF_ASSEMBLY_REFERENCE_INFO, structure](../../../docs/framework/unmanaged-api/profiling/cor-prf-assembly-reference-info-structure.md) [COR_PRF_HIGH_MONITOR, énumération](../../../docs/framework/unmanaged-api/profiling/cor-prf-high-monitor-enumeration.md) [GetAssemblyReferences, méthode](../../../docs/framework/unmanaged-api/profiling/icorprofilercallback6-getassemblyreferences-method.md) [GetEventMask2, méthode](../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo5-geteventmask2-method.md) [SetEventMask2, méthode](../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo5-seteventmask2-method.md) [AddAssemblyReference, méthode](../../../docs/framework/unmanaged-api/profiling/icorprofilerassemblyreferenceprovider-addassemblyreference-method.md)

     Les implémentations précédentes d'`ICorProfiler` prenaient en charge le chargement tardif des assemblys dépendants. Les nouvelles API de profilage ont besoin que les assemblys dépendants soient injectés par le profileur pour qu'ils puissent être chargés immédiatement, plutôt qu'une fois que l'application est entièrement initialisée. Cette modification ne concerne pas les utilisateurs des API `ICorProfiler` existantes.

- **Améliorations du débogage.** Les nouvelles API de débogage non managées suivantes améliorent l'intégration à un profileur. Vous pouvez à présent accéder aux métadonnées insérées par le profileur ainsi qu'aux variables locales et au code produit par les demandes ReJIT du compilateur pendant le débogage de dump.

     [SetWriteableMetadataUpdateMode, méthode](../../../docs/framework/unmanaged-api/debugging/icordebugprocess7-setwriteablemetadataupdatemode-method.md) [EnumerateLocalVariablesEx, méthode](../../../docs/framework/unmanaged-api/debugging/icordebugilframe4-enumeratelocalvariablesex-method.md) [GetLocalVariableEx, méthode](../../../docs/framework/unmanaged-api/debugging/icordebugilframe4-getlocalvariableex-method.md) [GetCodeEx, méthode](../../../docs/framework/unmanaged-api/debugging/icordebugilframe4-getcodeex-method.md) [GetActiveReJitRequestILCode, méthode](../../../docs/framework/unmanaged-api/debugging/icordebugfunction3-getactiverejitrequestilcode-method.md) [GetInstrumentedILMap, méthode](../../../docs/framework/unmanaged-api/debugging/icordebugilcode2-getinstrumentedilmap-method.md)

- **Modifications du suivi d’événements.** .NET Framework 4.5.2 permet le traçage des activités de type Suivi d'événements pour Windows (ETW) hors processus pour une surface d'exposition plus importante. Ce dernier permet aux fournisseurs de gestion avancée de l'alimentation (APM) de fournir des outils légers qui suivent avec précision les coûts des demandes et activités individuelles qui traversent les threads.  Ces événements sont déclenchés uniquement quand les contrôleurs ETW les autorisent ; par conséquent, les modifications ne concernent pas le code ETW écrit auparavant ni le code qui s'exécute avec la fonctionnalité ETW désactivée.

- **Promotion d’une transaction et sa conversion en une inscription durable**

     <xref:System.Transactions.Transaction.PromoteAndEnlistDurable%2A?displayProperty=nameWithType> est une nouvelle API ajoutée au .NET Framework 4.5.2 et 4.6 :

    ```csharp
    [System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]
    public Enlistment PromoteAndEnlistDurable(Guid resourceManagerIdentifier,
                                              IPromotableSinglePhaseNotification promotableNotification,
                                              ISinglePhaseNotification enlistmentNotification,
                                              EnlistmentOptions enlistmentOptions)
    ```

     La méthode peut être utilisée par une inscription précédemment créée par <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A?displayProperty=nameWithType> en réponse à la méthode <xref:System.Transactions.ITransactionPromoter.Promote%2A?displayProperty=nameWithType>. Elle demande à `System.Transactions` de promouvoir la transaction en une transaction MSDTC et de « convertir » l'inscription à promouvoir en une inscription durable. Après que la méthode s'est terminée avec succès, l'interface <xref:System.Transactions.IPromotableSinglePhaseNotification> n'est plus référencée par `System.Transactions` et toutes les futures notifications parviennent sur l'interface <xref:System.Transactions.ISinglePhaseNotification> fournie. L'inscription en question doit agir comme inscription durable, en prenant en charge la récupération et la journalisation des transactions. Consultez <xref:System.Transactions.Transaction.EnlistDurable%2A?displayProperty=nameWithType> pour plus d'informations. En outre, l'inscription doit prendre en charge <xref:System.Transactions.ISinglePhaseNotification>.  Cette méthode peut être appelée *seulement* lors du traitement d’un appel <xref:System.Transactions.ITransactionPromoter.Promote%2A?displayProperty=nameWithType>. Si tel n'est pas le cas, une exception <xref:System.Transactions.TransactionException> est levée.

 [Retour au début](#introduction)

<a name="v451"></a> 
## <a name="whats-new-in-the-net-framework-451"></a>Nouveautés dans le .NET Framework 4.5.1
 **Mises à jour d’avril 2014** :

- [Visual Studio 2013 Update 2](http://go.microsoft.com/fwlink/p/?LinkId=393658) inclut les mises à jour des modèles de la bibliothèque de classes portable pour prendre en charge les scénarios suivants :

    - Vous pouvez utiliser les API Windows Runtime dans les bibliothèques portables qui ciblent Windows 8.1, Windows Phone 8.1, et Windows Phone Silverlight 8.1.

    - Vous pouvez inclure du code XAML (type Windows.UI.XAML) dans les bibliothèques portables quand vous ciblez Windows 8.1 ou Windows Phone 8.1. Les modèles XAML suivants sont pris en charge : Page vierge, Dictionnaire de ressources, Contrôle basé sur un modèle et Contrôle utilisateur.

    - Vous pouvez créer un composant Windows Runtime portable (fichier .winmd) à utiliser dans les applications du Windows Store qui ciblent Windows 8.1 et Windows Phone 8.1.

    - Vous pouvez recibler une bibliothèque de classes du Windows Store ou du Windows Phone Store, par exemple une bibliothèque de classes portable.

     Pour plus d’informations sur ces modifications, consultez [Bibliothèque de classes portable](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md).

- Le jeu de contenus du .NET Framework inclut à présent la documentation relative à [!INCLUDE[net_native](../../../includes/net-native-md.md)], une technologie de précompilation qui permet de générer et déployer des applications Windows. [!INCLUDE[net_native](../../../includes/net-native-md.md)] compile directement vos applications en code natif, plutôt qu'en langage intermédiaire, pour de meilleures performances. Pour plus d’informations, consultez [Compilation d’applications avec .NET Native](../../../docs/framework/net-native/index.md).

- Le site [.NET Framework Reference Source](http://referencesource.microsoft.com/) propose une nouvelle expérience de navigation et des fonctionnalités améliorées. Vous pouvez à présent parcourir le code source .NET Framework en ligne, [télécharger la référence](http://referencesource.microsoft.com/download.html) à des fins de consultation hors connexion et parcourir les sources (notamment les correctifs et mises à jour) pendant le débogage. Pour plus d’informations, consultez l’entrée de blog qui présente [le nouvel aspect de la source de référence .NET](https://blogs.msdn.microsoft.com/dotnet/2014/02/24/a-new-look-for-net-reference-source/).

 Les principales fonctionnalités et améliorations nouvelles dans le .NET Framework 4.5.1 sont les suivantes :

- Redirection de liaison automatique des assemblys. Depuis [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], lorsque vous compilez une application qui cible [!INCLUDE[net_v451](../../../includes/net-v451-md.md)], il est possible d'ajouter des redirections de liaison au fichier de configuration de l'application, si votre application ou ses composants référencent plusieurs versions du même assembly. Vous pouvez également activer cette fonctionnalité pour les projets qui ciblent des versions antérieures du .NET Framework. Pour plus d’informations, consultez [Guide pratique pour activer et désactiver la redirection de liaison automatique](../../../docs/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md).

- Capacité à collecter des informations de diagnostic pour aider les développeurs à améliorer les performances des applications serveur et cloud. Pour plus d'informations, consultez les méthodes <xref:System.Diagnostics.Tracing.EventSource.WriteEventWithRelatedActivityId%2A> et <xref:System.Diagnostics.Tracing.EventSource.WriteEventWithRelatedActivityIdCore%2A> de la classe <xref:System.Diagnostics.Tracing.EventSource>.

- Capacité à compacter explicitement le tas d'objets volumineux (LOH) pendant un garbage collection. Pour plus d'informations, consultez la propriété <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode%2A?displayProperty=nameWithType>.

- Autres améliorations des performances, telles que la suspension d'application ASP.NET, les améliorations JIT multicœurs et le démarrage accéléré des applications après une mise à jour du .NET Framework. Pour plus d’informations, consultez l’article [Annonce de .NET Framework 4.5.1](https://blogs.msdn.microsoft.com/dotnet/2013/06/26/announcing-the-net-framework-4-5-1-preview/) et le billet de blog [ASP.NET app suspend](https://blogs.msdn.microsoft.com/dotnet/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting/).

 Les améliorations apportées à Windows Forms incluent :

- Redimensionnement dans les contrôles Windows Forms. Vous pouvez utiliser le paramètre PPP système pour redimensionner les composants des contrôles (par exemple, les icônes qui apparaissent dans une grille des propriétés) en choisissant de l'utiliser pour votre application grâce à une entrée dans le fichier de configuration de l'application (app.config). Cette fonctionnalité est actuellement prise en charge dans les contrôles Windows Forms suivants :

     <xref:System.Windows.Forms.PropertyGrid>    <xref:System.Windows.Forms.TreeView>    Certains aspects de <xref:System.Windows.Forms.DataGridView> (consultez [Nouvelles fonctionnalités dans 4.5.2](#v452) pour connaître les autres contrôles pris en charge)

     Pour activer cette fonctionnalité, ajoutez un nouvel élément \<appSettings> au fichier de configuration (app.config) et affectez la valeur `true` à l'élément `EnableWindowsFormsHighDpiAutoResizing` :

    ```xml
    <appSettings>
       <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />
    </appSettings>
    ```

 Les améliorations lors du débogage de vos applications .NET Framework dans [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)] incluent :

- Valeurs de retour dans le débogueur Visual Studio. Lorsque vous déboguez une application managée dans [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], la Fenêtre Automatique affiche les types et les valeurs de retour pour les méthodes. Ces informations sont disponibles pour les applications de bureau, Windows Store et Windows Phone. Pour plus d’informations, consultez [Examiner les valeurs de retour des appels de méthode](http://msdn.microsoft.com/library/e3245b37-8e2e-4200-ba84-133726e95f1f\(v=vs.120\).aspx) dans MSDN Library.

- Modifier & Continuer pour applications 64 bits. [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)] prend en charge la fonctionnalité Modifier & Continuer pour les applications managées 64 bits pour le Bureau, Windows Store et Windows Phone. Les limitations existantes restent effectives pour les applications 32 bits et 64 bits (consultez la dernière section de l’article [Modifications de code prises en charge (C#)](/visualstudio/debugger/supported-code-changes-csharp)).

- Débogage asynchrone. Pour simplifier le débogage des applications asynchrones dans [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], la pile d'appels masque le code d'infrastructure fourni par les compilateurs pour prendre en charge la programmation asynchrone. Elle chaîne également les trames parentes logiques afin que vous puissiez suivre plus clairement l'exécution logique du programme. Une fenêtre Tâches remplace la fenêtre Tâches parallèles et affiche les tâches relatives à un point d'arrêt particulier, ainsi que toutes les autres tâches qui sont actuellement actives ou planifiées dans l'application. Vous pouvez en savoir plus sur cette fonctionnalité en lisant la section sur le débogage asynchrone de l’[annonce relative à .NET Framework 4.5.1](https://blogs.msdn.microsoft.com/dotnet/2013/06/26/announcing-the-net-framework-4-5-1-preview/).

- Meilleure prise en charge des exceptions pour les composants Windows Runtime. Dans [!INCLUDE[win81](../../../includes/win81-md.md)], une exception qui provient des applications Windows Store conserve les informations sur l'erreur qui a provoqué l'exception, même au-delà des limites du langage. Vous pouvez en savoir plus sur cette fonctionnalité en lisant la section sur le développement d’applications du Windows Store dans l’[annonce relative au .NET Framework 4.5.1](https://blogs.msdn.microsoft.com/dotnet/2013/06/26/announcing-the-net-framework-4-5-1-preview/). 

 Depuis [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], vous pouvez utiliser [Mpgo.exe (Outil d'optimisation guidée par profil managé)](../../../docs/framework/tools/mpgo-exe-managed-profile-guided-optimization-tool.md) pour optimiser les applications [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)], ainsi que les applications de bureau.

 Pour découvrir les nouvelles fonctionnalités d’ASP.NET 4.5.1, consultez [ASP.NET 4.5.1 et Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=309094) sur le site ASP.NET.

 [Retour au début](#introduction)

<a name="v45"></a> 
## <a name="whats-new-in-the-net-framework-45"></a>Nouveautés dans le .NET Framework 4.5

### <a name="core-new-features-and-improvements"></a>Principales fonctionnalités et améliorations nouvelles

- Capacité à réduire les redémarrages du système en détectant et en fermant les applications .NET Framework 4 pendant le déploiement. Consultez [Réduction des redémarrages système durant les installations de .NET Framework 4.5](../../../docs/framework/deployment/reducing-system-restarts.md).

- Prise en charge de tableaux supérieurs à 2 gigaoctets (Go) sur les plateformes 64 bits. Cette fonctionnalité peut être activée dans le fichier de configuration de l'application. Consultez l’[élément \<gcAllowVeryLargeObjects>](../../../docs/framework/configure-apps/file-schema/runtime/gcallowverylargeobjects-element.md), qui répertorie également d’autres restrictions sur la taille des objets et la taille des tableaux.

- Meilleures performances via une opération garbage collection en arrière-plan pour les serveurs. Lorsque vous utilisez le garbage collection de serveur dans [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], le garbage collection en arrière-plan est automatiquement activé. Consultez la section Garbage collection de serveur en arrière-plan, dans la rubrique [Notions de base du garbage collection](../../../docs/standard/garbage-collection/fundamentals.md).

- Compilation juste-à-temps (JIT) en arrière-plan, disponible en option sur les processeurs multicœurs pour améliorer les performances de l'application. Consultez <xref:System.Runtime.ProfileOptimization>.

- Capacité à limiter la durée pendant laquelle le moteur d'expressions régulières tentera de résoudre une expression régulière avant d'expirer. Voir la propriété <xref:System.Text.RegularExpressions.Regex.MatchTimeout%2A?displayProperty=nameWithType>.

- Capacité à définir la culture par défaut d'un domaine d'application. Voir la classe <xref:System.Globalization.CultureInfo>.

- Prise en charge de la console pour l'encodage Unicode (UTF-16). Voir la classe <xref:System.Console>.

- Prise en charge du versioning des données de classement et de comparaison des chaînes culturelles. Voir la classe <xref:System.Globalization.SortVersion>.

- Meilleures performances lors de l'extraction des ressources. Consultez [Empaquetage et déploiement de ressources](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md).

- Améliorations de la compression Zip pour réduire la taille d'un fichier compressé. Voir l'espace de noms <xref:System.IO.Compression?displayProperty=nameWithType>.

- Possibilité de personnaliser un contexte de réflexion pour remplacer le comportement de réflexion par défaut par l'intermédiaire de la classe <xref:System.Reflection.Context.CustomReflectionContext>.

- Prise en charge de la version 2008 de la norme IDNA (Internationalized Domain Names in Applications) lorsque la classe <xref:System.Globalization.IdnMapping?displayProperty=nameWithType> est utilisée dans [!INCLUDE[win8](../../../includes/win8-md.md)].

- Délégation de comparaison de chaînes au système d'exploitation, qui implémente Unicode 6.0, lorsque .NET Framework est utilisé dans [!INCLUDE[win8](../../../includes/win8-md.md)]. Lorsqu'il s'exécute sur d'autres plateformes, .NET Framework inclut ses propres données de comparaison de chaînes, qui implémentent Unicode 5.x. Voir la classe <xref:System.String> et la section Notes de la classe <xref:System.Globalization.SortVersion>.

- Possibilité de calculer les codes de hachage des chaînes par domaine d'application. Voir [\<UseRandomizedStringHashAlgorithm>, élément](../../../docs/framework/configure-apps/file-schema/runtime/userandomizedstringhashalgorithm-element.md).

- Prise en charge de la réflexion de type fractionnée entre les classes <xref:System.Type> et <xref:System.Reflection.TypeInfo>. Consultez [Réflexion dans le .NET Framework pour les applications du Windows Store](../../../docs/framework/reflection-and-codedom/reflection-for-windows-store-apps.md).

### <a name="managed-extensibility-framework-mef"></a>Managed Extensibility Framework (MEF)
 Dans [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], le package Managed Extensibility Framework (MEF) fournit les nouvelles fonctionnalités suivantes :

- Prise en charge des types génériques.

- Modèle de programmation basé sur les conventions qui permet de créer des parties basées sur les conventions d'appellation, plutôt que sur les attributs.

- Portées multiples.

- Sous-ensemble MEF que vous pouvez utiliser lorsque vous créez des applications [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]. Ce sous-ensemble est disponible sous la forme d’un [package téléchargeable](http://go.microsoft.com/fwlink/?LinkId=256238) à partir de la galerie NuGet. Pour installer ce package, ouvrez votre projet dans Visual Studio, dans le menu **Projet** choisissez **Gérer les packages NuGet**, puis recherchez en ligne le package `Microsoft.Composition`.

 Pour plus d’informations, consultez [Vue d’ensemble de Managed Extensibility Framework](../../../docs/framework/mef/index.md).

### <a name="asynchronous-file-operations"></a>Opérations asynchrones sur les fichiers
 Dans [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], de nouvelles fonctionnalités asynchrones ont été ajoutées aux langages C# et Visual Basic. Ces fonctionnalités ajoutent un modèle basé sur les tâches pour exécuter des opérations asynchrones. Pour utiliser ce nouveau modèle, utilisez les méthodes asynchrones dans les classes d'E/S. Consultez [E/S de fichier asynchrone](../../../docs/standard/io/asynchronous-file-i-o.md).

<a name="tools"></a> 
### <a name="tools"></a>Outils
 Dans [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], l'outil Resource File Generator (Resgen.exe) vous permet de créer un fichier .resw à utiliser dans les applications [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] à partir d'un fichier .resources incorporé dans un assembly .NET Framework. Pour plus d’informations, consultez [Resgen.exe (Resource File Generator)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md).

 L'outil d'optimisation guidée par profil managé (Mpgo.exe) vous permet d'améliorer le temps de démarrage de l'application, l'utilisation de la mémoire (taille du jeu de travail) et le débit en optimisant les assemblys d'image natifs. L'outil en ligne de commande génère des données de profil pour les assemblys natifs d'application graphique. Consultez [Mpgo.exe (Outil d’optimisation guidée par profil managé)](../../../docs/framework/tools/mpgo-exe-managed-profile-guided-optimization-tool.md). Depuis [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], vous pouvez utiliser Mpgo.exe pour optimiser les applications [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)], ainsi que les applications de bureau.

<a name="parallel"></a> 
### <a name="parallel-computing"></a>Calcul parallèle
 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] fournit plusieurs nouvelles fonctionnalités et améliorations pour le calcul parallèle. Il s'agit notamment de performances améliorées, d'un contrôle accru, d'une prise en charge améliorée pour la programmation asynchrone, d'une nouvelle bibliothèque de flux de données et d'une prise en charge améliorée pour le débogage parallèle et l'analyse des performances. Consultez l’entrée relative aux [nouveautés en matière de parallélisme dans .NET 4.5](http://go.microsoft.com/fwlink/?LinkId=235061) dans le blog consacré à la programmation parallèle avec .NET.

<a name="web"></a> 
### <a name="web"></a>Web
 ASP.NET 4.5 et 4.5.1 ajoutent la liaison de modèle pour Web Forms, la prise en charge de WebSocket, les gestionnaires asynchrones, les améliorations de performances et de nombreuses autres fonctionnalités. Pour plus d'informations, reportez-vous aux ressources suivantes :

- [ASP.NET 4.5 et Visual Studio 2012](http://msdn.microsoft.com/library/ac9bb7f6-f094-4af7-bad0-acf49a5dbc55) dans MSDN Library.

- [ASP.NET 4.5.1 et Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=309094) sur le site ASP.NET.

<a name="networking"></a> 
### <a name="networking"></a>Réseau
 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] fournit une nouvelle interface de programmation pour les applications HTTP. Pour plus d'informations, consultez les nouveaux espaces de noms <xref:System.Net.Http?displayProperty=nameWithType> et <xref:System.Net.Http.Headers?displayProperty=nameWithType>.

 La prise en charge d'une nouvelle interface de programmation permettant d'accepter et d'interagir avec une connexion de WebSocket à l'aide de la classe <xref:System.Net.HttpListener> existante et des classes associées est également incluse. Pour plus d'informations, consultez le nouvel espace de noms <xref:System.Net.WebSockets> et la classe <xref:System.Net.HttpListener>.

 En outre, [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] inclut les améliorations de mise en réseau suivantes :

- Prise en charge URI conforme aux documents RFC. Pour plus d'informations, consultez <xref:System.Uri> et les classes associées.

- Prise en charge des analyses du nom de domaine international (IDN, Internationalized Domain Name). Pour plus d'informations, consultez <xref:System.Uri> et les classes associées.

- Prise en charge de l'internationalisation des adresses de messagerie. Pour plus d'informations, consultez l'espace de noms <xref:System.Net.Mail>.

- Prise en charge d'IPv6 améliorée. Pour plus d'informations, consultez l'espace de noms <xref:System.Net.NetworkInformation>.

- Prise en charge du socket en mode double. Pour plus d'informations, consultez la classe <xref:System.Net.Sockets.Socket> et <xref:System.Net.Sockets.TcpListener>.

<a name="client"></a> 
### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)
 Dans [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], Windows Presentation Foundation (WPF) présente des modifications et des améliorations dans les domaines suivants :

- Le nouveau contrôle <xref:System.Windows.Controls.Ribbon.Ribbon>, qui vous permet d'implémenter une interface utilisateur de type ruban hébergeant une barre d'outils Accès rapide, un menu d'application et des onglets.

- La nouvelle interface <xref:System.ComponentModel.INotifyDataErrorInfo>, qui prend en charge la validation synchrone et asynchrone des données.

- Nouvelles fonctionnalités des classes <xref:System.Windows.Controls.VirtualizingPanel> et <xref:System.Windows.Threading.Dispatcher>.

- Performances améliorées lors de l'affichage de grands ensembles de données groupées et lors de l'accès aux collections sur les threads autres que ceux d'interface utilisateur.

- Liaison de données aux propriétés statiques, liaison de données aux types personnalisés qui implémentent l'interface <xref:System.Reflection.ICustomTypeProvider> et extraction des informations de liaison de données à partir d'une expression de liaison.

- Repositionnement des données au fur et à mesure du changement des valeurs (mise en forme active).

- Possibilité de vérifier si le contexte de données d'un conteneur d'éléments est déconnecté.

- Possibilité de définir la durée qui doit s'écouler entre les modifications de propriété et les mises à jour de la source de données.

- Prise en charge améliorée pour implémenter des modèles d'événement faible. De plus, les événements peuvent maintenant accepter des extensions de balisage.

<a name="windows_communication_foundation"></a> 
### <a name="windows-communication-foundation-wcf"></a>Windows Communication Foundation (WCF)
 Dans [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], les fonctionnalités suivantes ont été ajoutées pour faciliter l'écriture et l'entretien des applications Windows Communication Foundation (WCF) :

- Simplification des fichiers de configuration générés.

- Prise en charge du développement Contrat en premier.

- Possibilité de configurer plus facilement le mode de compatibilité ASP.NET.

- Modifications des valeurs de propriété de transport par défaut pour réduire la probabilité d'avoir à les définir.

- Mises à jour de la classe <xref:System.Xml.XmlDictionaryReaderQuotas> afin de réduire la probabilité d'avoir à configurer manuellement les quotas pour les lecteurs de dictionnaire XML.

- Validation des fichiers de configuration WCF par Visual Studio dans le cadre du processus de génération, afin que vous puissiez détecter les erreurs de configuration avant d'exécuter votre application.

- Nouvelle prise en charge de la diffusion en continu asynchrone.

- Nouveau mappage de protocole HTTPS pour simplifier l'exposition d'un point de terminaison via HTTPS à l'aide des services Internet (IIS).

- Possibilité de générer des métadonnées dans un document WSDL unique en ajoutant `?singleWSDL` à l'URL de service.

- Prise en charge Websockets pour activer une véritable communication bidirectionnelle sur les ports 80 et 443 avec des caractéristiques de performances semblables à celles du transport TCP.

- Prise en charge de la configuration des services dans le code.

- Info-bulles de l'éditeur XML.

- Prise en charge de la mise en cache de <xref:System.ServiceModel.ChannelFactory>.

- Prise en charge de la compression d'encodage binaire.

- Prise en charge d'un transport UDP qui permet aux développeurs d'écrire des services qui utilisent une messagerie de type « Fire and Forget » (déclenché et oublié). Un client envoie un message à un service et n'attend aucune réponse de ce dernier.

- Possibilité de prendre en charge plusieurs modes d'authentification sur un point de terminaison WCF unique lors de l'utilisation du transport HTTP et de la sécurité du transport.

- Prise en charge des services WCF qui utilisent des noms IDN.

 Pour plus d’informations, consultez [Nouveautés dans Windows Communication Foundation](http://go.microsoft.com/fwlink/?LinkId=228173).

<a name="windows_workflow_foundation"></a> 
### <a name="windows-workflow-foundation-wf"></a>Windows Workflow Foundation (WF)
 Dans [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], plusieurs nouvelles fonctionnalités ont été ajoutées à Windows Workflow Foundation (WF), notamment :

- Flux de travail de la machine à états, qui ont été introduits pour la première fois dans le cadre de .NET Framework 4.0.1 ([.NET Framework 4 Platform Update 1](http://go.microsoft.com/fwlink/?LinkID=215092)). Cette mise à jour comprenait plusieurs classes et activités nouvelles qui permettaient aux développeurs de créer des flux de travail de machine à états. Ces classes et activités ont été mises à jour pour que [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] inclue les fonctionnalités suivantes :

    - Possibilité de définir des points d'arrêt sur les états.

    - Possibilité de copier et coller des transitions dans le concepteur de workflow.

    - Prise en charge du concepteur pour la création de transitions de déclencheur partagées.

    - Activités de création de flux de travail de machine à états, notamment : <xref:System.Activities.Statements.StateMachine>, <xref:System.Activities.Statements.State> et <xref:System.Activities.Statements.Transition>.

- Fonctionnalités améliorées du Concepteur de flux de travail, dont notamment :

    - Fonctions de recherche de flux de travail améliorées dans Visual Studio, notamment **Recherche rapide** et **Rechercher dans les fichiers**.

    - Possibilité de créer automatiquement une activité de séquence lorsqu'une deuxième activité enfant est ajoutée à une activité de conteneur, et d'inclure les deux activités dans l'activité de séquence.

    - Prise en charge des panoramiques, ce qui permet à la partie visible d'un flux de travail d'être modifiée sans utiliser les barres de défilement.

    - Nouvelle vue **Structure du document** qui affiche les composants d’un flux de travail en mode Plan sous forme d’arborescence et vous permet de sélectionner un composant dans la vue **Structure du document**.

    - Possibilité d'ajouter des annotations aux activités.

    - Possibilité de définir et d'utiliser des délégués d'activité à l'aide du Concepteur de flux de travail.

    - Connexion automatique et insertion automatique des activités et des transitions dans les flux de travail de machine à états et d'organigramme.

- Stockage des informations d'état d'affichage pour un flux de travail dans un élément unique du fichier XAML, afin que vous puissiez facilement localiser et modifier les informations sur l'état d'affichage.

- Activité de conteneur NoPersistScope pour empêcher les activités enfants de devenir persistantes.

- Prise en charge des expressions C# :

    - Les projets de flux de travail qui utilisent Visual Basic utiliseront les expressions Visual Basic et les projets de flux de travail C# utiliseront les expressions C#.

    - Les projets de flux de travail C# qui ont été créés dans Visual Studio 2010 et qui possèdent des expressions Visual Basic sont compatibles avec les projets de flux de travail C# qui utilisent des expressions C#.

- Améliorations du contrôle de version :

    - Nouvelle classe <xref:System.Activities.WorkflowIdentity>, qui fournit un mappage entre une instance de flux de travail rendue persistante et sa définition de flux de travail.

    - Exécution côte à côte de plusieurs versions de flux de travail dans le même hôte, y compris <xref:System.ServiceModel.Activities.WorkflowServiceHost>.

    - Dans une mise à jour dynamique, capacité à modifier la définition d'une instance de flux de travail rendue persistante.

- Développement de services de workflow « Contrat en premier », ce qui permet de générer automatiquement les activités correspondants à un contrat de service existant.

 Pour plus d’informations, consultez [Nouveautés de Windows Workflow Foundation](http://go.microsoft.com/fwlink/?LinkId=228176).

<a name="tailored"></a> 
### [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]
 Les applications [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] sont conçues pour des facteurs de forme spécifiques et tirent parti de la puissance du système d'exploitation Windows. Un sous-ensemble de [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] ou 4.5.1 est disponible pour générer des applications [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] pour Windows à l'aide de C# ou de Visual Basic. Ce sous-ensemble s’appelle [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] et est décrit dans une [vue d’ensemble](http://go.microsoft.com/fwlink/?LinkId=228491) disponible dans le Centre de développement Windows.

<a name="portable"></a> 
### <a name="portable-class-libraries"></a>Bibliothèques de classes portables
 Le projet Bibliothèque de classes portable dans [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)] (et les versions ultérieures) vous permet d'écrire et de générer des assemblys managés qui fonctionnent sur plusieurs plateformes .NET Framework. Un projet Bibliothèque de classes portable vous permet de choisir les plateformes (telles que Windows Phone et [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]) à cibler. Les types et les membres disponibles dans votre projet sont automatiquement restreints aux types et aux membres communs entre ces plateformes. Pour plus d’informations, consultez [Bibliothèque de classes portable](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md).

## <a name="see-also"></a>Voir aussi
 [Versions finales hors plage du .NET Framework](../../../docs/framework/get-started/the-net-framework-and-out-of-band-releases.md)   
 [Nouveautés du .NET Framework dans le domaine de l’accessibilité](whats-new-in-accessibility.md)   
 [Nouveautés de Visual Studio 2017](/visualstudio/ide/whats-new-in-visual-studio)   
 [ASP.NET](/aspnet)   
 [Nouveautés de Visual C++](/cpp/what-s-new-for-visual-cpp-in-visual-studio) 
