---
title: "Vue d’ensemble du .NET Framework"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application development [.NET Framework]
- common language runtime
- common language runtime, about
- common language runtime, overview
ms.assetid: 29848c96-fc36-462d-8072-ba223a40b697
caps.latest.revision: "34"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: ffe4670ef07b0a9b541bf2099958aa943bba2f68
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="overview-of-the-net-framework"></a>Vue d’ensemble du .NET Framework

Le .NET Framework est une technologie qui prend en charge la création et l’exécution de la nouvelle génération d’applications et de services web XML. Le .NET Framework est conçu pour remplir les objectifs suivants :

- Fournir un environnement cohérent de programmation orientée objet que le code objet soit stocké et exécuté localement, exécuté localement mais distribué sur Internet ou exécuté à distance.

- Fournir un environnement d'exécution de code qui minimise le déploiement de logiciel et de conflits de versions.

- Fournir un environnement d'exécution de code qui promeut l'exécution sécurisée de code y compris le code créé par un tiers d'un niveau de confiance moyen ou un tiers inconnu.

- Fournir un environnement d'exécution de code qui élimine les problèmes de performance des environnements interprétés ou écrits en scripts.

- Fournir au développeur un environnement cohérent entre une grande variété de types d’applications comme les applications Windows et les applications web.

- Générer toutes les communications à partir des normes du secteur pour s’assurer que le code basé sur le .NET Framework s’intègre à n’importe quel autre code.

> [!NOTE]
> Pour une présentation générale du .NET Framework à destination des utilisateurs et des développeurs, consultez [Bien démarrer](../../../docs/framework/get-started/index.md).

Le .NET Framework se compose du Common Language Runtime (CLR) et de la bibliothèque de classes .NET Framework. Le Common Language Runtime est la base du .NET Framework. Le runtime est un agent qui manage le code au moment de l’exécution, fournit des services essentiels comme la gestion de la mémoire, la gestion des threads et la communication à distance. Il applique également une cohérence stricte des types et d’autres formes de précision qui favorisent un code sécurisé et robuste. En fait, le concept de gestion de code est un principe fondamental du runtime. Pour le code qui cible le runtime, on parle de code managé, tandis que pour le code qui ne cible pas le runtime, on parle de code non managé. La bibliothèque de classes est une collection complète orientée objet de types réutilisables que vous pouvez utiliser pour développer des applications, qu’il s’agisse d’applications en ligne de commande ou à interface graphique utilisateur traditionnelles ou d’applications basées sur les dernières innovations fournies par ASP.NET, comme les services web XML et Web Forms.

Le .NET Framework peut être hébergé par des composants non managés qui chargent le Common Language Runtime dans leurs processus et lancent l’exécution du code managé, créant ainsi un environnement logiciel qui exploite à la fois les fonctionnalités managées et non managées. Le .NET Framework fournit non seulement plusieurs hôtes de runtime, mais il prend également en charge le développement d’hôtes de runtime tiers.

Par exemple, ASP.NET héberge le runtime pour fournir un environnement côté serveur, évolutif pour le code managé. ASP.NET fonctionne directement avec le runtime pour activer des applications ASP.NET et des services web XML, deux sujets qui sont évoqués plus loin dans cette rubrique.

Internet Explorer est un exemple d’application non managée qui héberge le runtime (sous la forme d’une extension de type MIME). L'utilisation d'Internet Explorer pour héberger le runtime vous permet d'incorporer des composants managés ou des contrôles Windows Forms dans des documents HTML. Ainsi hébergé, le runtime rend possible le code mobile managé, avec toutefois des améliorations significatives que seul le code managé permet, telles que l’exécution d’un niveau de confiance partielle et le stockage de fichiers isolés.

L’illustration suivante montre les relations du Common Language Runtime et de la bibliothèque de classes avec vos applications et l’ensemble du système. L'illustration montre également comment le code managé opère au sein d'une architecture plus grande.

![Code managé dans une architecture plus grande](../../../docs/framework/get-started/media/circle.gif "cercle") .NET Framework en contexte

Les sections suivantes décrivent les principales fonctionnalités du .NET Framework.

## <a name="features-of-the-common-language-runtime"></a>Fonctionnalités du Common Language Runtime

Le Common Language Runtime gère la mémoire, l'exécution des threads, l'exécution du code, la vérification de la sécurité du code, la compilation et d'autres services du système. Ces fonctionnalités font partie intégrante du code managé qui s'exécute sous le Common Language Runtime.

Concernant la sécurité, les composants managés se voient attribuer divers niveaux de confiance en fonction d’un nombre de facteurs qui comprennent leur origine (comme Internet, un réseau d’entreprise ou un ordinateur local). Cela signifie qu’un composant managé peut ou ne peut pas effectuer des opérations d’accès au fichier, des opérations d’accès au Registre ou d’autres fonctions délicates, même si ce composant est utilisé dans la même application active.

Le runtime garantit également un code robuste en implémentant une infrastructure de vérification de code et de type stricte portant le nom de système de type commun (CTS, Common Type System). Le CTS garantit que le tout le code managé soit autodescriptif. Les différents compilateurs de langage Microsoft et tiers génèrent du code managé conforme au système de type commun (CTS, Common Type System). Cela signifie que le code managé peut consommer d'autres instances et types managés, tout en appliquant strictement le respect et la sécurité des types.

En outre, l'environnement managé du runtime élimine un grand nombre de problèmes logiciels courants. Par exemple, le runtime traite automatiquement la disposition des objets et gère les références aux objets, les libérant lorsqu'ils ne sont plus utilisés. Cette gestion automatique de la mémoire résout les deux erreurs d’application les plus courantes, le manque de mémoire et les références mémoire non valides.

Le runtime accélère également la productivité du développeur. Par exemple, les programmeurs peuvent écrire des applications dans le langage de développement de leur choix, tout en tirant pleinement parti du runtime, de la bibliothèque de classes, et de composants écrits dans d’autres langages par d’autres développeurs. Tout fournisseur de compilateur qui choisit de cibler le runtime peut en faire de même. Les compilateurs de langage qui ciblent le .NET Framework rendent les fonctionnalités du .NET Framework disponibles au code existant écrit dans ce langage, ce qui simplifie considérablement le processus de migration pour les applications existantes.

Si le runtime est conçu pour les logiciels du futur, il prend également en charge les logiciels d'aujourd'hui et d'hier. L'interopérabilité entre les codes managés et non managés permet aux développeurs de continuer à utiliser des composants COM et des DLL nécessaires.

Le runtime est conçu pour améliorer les performances. Bien que le Common Language Runtime fournisse de nombreux services de runtime standard, le code managé n'est jamais interprété. Une fonctionnalité connue sous le nom de compilation juste-à-temps (JIT, Just-In-Time) permet à tout le code managé de s’exécuter dans le langage machine natif du système sur lequel il s’exécute. De son côté, le gestionnaire de mémoire élimine les risques de mémoire fragmentée et augmente la localité de référence mémoire afin de décupler les performances.

Enfin, le runtime peut être hébergé par des applications côté serveur hautement performantes, comme Microsoft SQL Server et les Internet Information Services (IIS). Cette infrastructure vous permet d'utiliser du code managé pour écrire votre logique métier tout en profitant des performances supérieures du meilleur des serveurs d'entreprise prenant en charge l'hébergement runtime.

## <a name="net-framework-class-library"></a>Bibliothèque de classes .NET Framework

La bibliothèque de classes .NET Framework est une collection de types réutilisables qui s'intègrent parfaitement au Common Language Runtime. La bibliothèque de classes est orientée objet et fournit des types à partir desquels votre propre code managé dérive des fonctionnalités. Les types .NET Framework n’en sont que plus faciles à utiliser et vous pouvez apprendre les nouvelles fonctionnalités du .NET Framework plus rapidement. Par ailleurs, les composants tiers s’intègrent parfaitement aux classes du .NET Framework.

Par exemple, les classes de collection du .NET Framework implémentent un jeu d’interfaces pour développer vos propres classes de collection. Vos classes de collection s’intègrent parfaitement aux classes du .NET Framework.

Comme pour toute bibliothèque de classes orientée objet, les types .NET Framework vous permettent d'accomplir un éventail de tâches courantes de programmation y compris des tâches comme la gestion de chaînes, la collection de données, la connectivité de bases de données, et l'accès aux fichiers. En plus de ces tâches courantes, la bibliothèque de classes comprend des types qui prennent en charge une variété de scénarios de développement spécialisé. Utilisez le .NET Framework pour développer les types d’applications et de services suivants :

- Applications de console. Consultez [Génération d'applications console](../../../docs/standard/building-console-apps.md).

- Applications GUI Windows (Windows Forms). Consultez [Windows Forms](../../../docs/framework/winforms/index.md).

- Applications Windows Presentation Foundation (WPF). Consultez [Windows Presentation Foundation](../../../docs/framework/wpf/index.md).

- Applications ASP.NET. Consultez [Applications web avec ASP.NET](../../../docs/framework/develop-web-apps-with-aspnet.md).

- Les services Windows. Consultez [Introduction aux applications de service Windows](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md).

- Applications orientées service qui utilisent Windows Communication Foundation (WCF). Consultez [Applications orientées service avec WCF](../../../docs/framework/wcf/index.md).

- Applications prenant en charge les flux de travail et qui utilisent Windows Workflow Foundation (WF). Consultez [Génération de flux de travail dans le .NET Framework](http://msdn.microsoft.com/library/cbf3880f-dc7b-466d-b808-1109b1223f4a).

Les classes Windows Forms sont un ensemble complet de types réutilisables qui simplifient grandement le développement GUI Windows. Si vous écrivez une application Web Form ASP.NET, vous pouvez utiliser les classes Web Forms.

## <a name="see-also"></a>Voir aussi

[Configuration requise](../../../docs/framework/get-started/system-requirements.md)   
[Guide d’installation](../../../docs/framework/install/index.md)   
[Guide de développement](../../../docs/framework/development-guide.md)   
[Outils](../../../docs/framework/tools/index.md)   
[Exemples .NET Framework](http://msdn.microsoft.com/library/177055f8-4a1f-43e7-aee6-995c196079b1)   
[Bibliothèque de classes .NET Framework](http://go.microsoft.com/fwlink/?LinkID=227195)
