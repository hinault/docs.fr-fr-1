---
title: "Sécurité d'accès du code"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- named permission sets, code access security
- call stacks
- malicious code
- stack walk
- security [.NET Framework], code access security
- permissions [.NET Framework], code access security
- trusted code
- mobile code security
- unmanaged code, code access security
- granting permissions, code access security
- user authentication, code access security
- code access security
ms.assetid: 859af632-c80d-4736-8d6f-1e01b09ce127
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 04a46e30256b3b6df3de51346924cbb5fa057837
ms.sourcegitcommit: cf22b29db780e532e1090c6e755aa52d28273fa6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="code-access-security"></a>Sécurité d'accès du code
[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]  
  
 De nos jours, du fait d'une interconnexion extrême, les systèmes informatiques sont fréquemment exposés à du code provenant de diverses sources parfois inconnues. Code peut être jointe à la messagerie électronique, contenu dans des documents ou téléchargé via Internet. Malheureusement, de nombreux utilisateurs d’ordinateurs ont personnellement fait l’expérience de code mobile malveillant, y compris de virus et de vers, qui peuvent endommager ou détruire des données et coûter du temps et de l’argent.  
  
 La plupart des mécanismes de sécurité courants accordent des droits aux utilisateurs en fonction de leurs informations d'identification de connexion (généralement un mot de passe) et limitent les ressources (souvent des répertoires et fichiers) auxquelles ils peuvent accéder. Cependant, cette approche ne parvient pas à répondre à plusieurs situations : les utilisateurs peuvent obtenir du code provenant de nombreuses sources dont certaines peuvent ne pas être fiables, le code peut contenir des bogues ou des vulnérabilités qui permettent à du code nuisible de l'exploiter et le code fait parfois des choses dont l'utilisateur n'a pas conscience. Les systèmes informatiques peuvent donc être endommagés et des données confidentielles peuvent être divulguées si des utilisateurs prudents et dignes de confiance exécutent un logiciel malveillant ou rempli d'erreurs. La plupart des mécanismes de sécurité des systèmes d'exploitation nécessitent que chaque partie du code ait un niveau de confiance suffisant afin de s'exécuter, sauf peut-être pour les scripts d'une page web. Un mécanisme de sécurité largement applicable qui permette à du code provenant d'un système informatique de s'exécuter en toute sécurité sur un autre système est donc nécessaire, même s'il n'existe pas de relations de confiance entre les systèmes.  
  
 Le .NET Framework fournit un mécanisme de sécurité appelé sécurité d'accès du code, qui aide à protéger les systèmes informatiques contre du code mobile malveillant, pour permettre à du code d'origine inconnue de s'exécuter en toute sécurité et pour éviter que du code de confiance ne compromette la sécurité de manière intentionnelle ou accidentelle. La sécurité d'accès du code permet au code d'avoir un niveau de confiance à différents degrés, en fonction de son origine et d'autres aspects de son identité. La sécurité d'accès du code applique aussi différents niveaux de confiance au code, ce qui réduit la quantité de code dont le niveau de confiance doit être suffisant pour s'exécuter. L'utilisation de la sécurité d'accès du code peut diminuer la probabilité que votre code soit utilisé de manière abusive par du code malveillant ou rempli d'erreurs. Elle peut réduire votre responsabilité, car vous pouvez spécifier l'ensemble des opérations que votre code est autorisé à exécuter. La sécurité d'accès du code peut aussi aider à réduire les dommages qui peuvent résulter de la mise en danger de la sécurité dans votre code.  
  
> [!NOTE]
>  Des modifications importantes ont été apportées à la sécurité d'accès du code dans le [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]. La modification la plus notable a été [la transparence de sécurité](../../../docs/framework/misc/security-transparent-code.md), mais il existe d’autres modifications significatives qui affectent la sécurité d’accès du code. Pour plus d’informations sur ces modifications, consultez [modifications de sécurité](../../../docs/framework/security/security-changes.md).  
  
 La sécurité d'accès du code affecte principalement le code de bibliothèque et les applications partiellement fiables. Les développeurs de bibliothèques doivent protéger leur code contre l'accès non autorisé d'applications partiellement fiables, qui sont des applications chargées à partir de sources externes telles qu'Internet. Les applications installées sur votre poste de travail ou sur l'intranet local sont exécutées avec une confiance totale. Applications de confiance totale ne sont pas affectées par la sécurité d’accès du code, sauf si elles sont marquées comme [transparent de sécurité](../../../docs/framework/misc/security-transparent-code.md), car ils sont entièrement fiables. Leur seule limitation est que les applications marquées avec l'attribut <xref:System.Security.SecurityTransparentAttribute> ne peuvent pas appeler du code marqué avec l'attribut <xref:System.Security.SecurityCriticalAttribute>. Les applications partiellement fiables doivent être exécutées dans un bac à sable (sandbox) (par exemple, dans Internet Explorer) pour que la sécurité d'accès du code puisse être appliquée. Si vous téléchargez une application à partir d'Internet et essayez de l'exécuter sur votre poste de travail, vous obtiendrez une <xref:System.NotSupportedException> avec le message suivant : «Tentative de chargement d'un assembly à partir d'un emplacement réseau qui aurait entraîné l'utilisation de l'assembly en mode Bac à sable (sandbox) dans les versions antérieures du .NET Framework. Cette mise en production du .NET Framework n’activant pas la stratégie CAS par défaut, ce chargement peut être dangereux. » Si vous êtes sûr que l’application peut être approuvée, vous pouvez l’activer être exécuté avec une confiance totale à l’aide de la [ \<loadFromRemoteSources > élément](../../../docs/framework/configure-apps/file-schema/runtime/loadfromremotesources-element.md). Pour plus d’informations sur l’exécution d’une application dans un bac à sable, consultez [Comment : exécuter Partially Trusted Code dans un bac à sable](../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md).  
  
 Tout le code managé qui cible le Common Language Runtime bénéficie de la sécurité d'accès du code, même si ce code ne fait aucun appel de sécurité d'accès du code. Pour plus d’informations, consultez [Notions fondamentales de la sécurité d’accès du code](../../../docs/framework/misc/code-access-security-basics.md).  
  
<a name="key_functions"></a>   
## <a name="key-functions-of-code-access-security"></a>Fonctions clés de la sécurité d'accès du code  
 La sécurité d'accès du code permet de limiter l'accès du code aux ressources et opérations protégées. Dans le .NET Framework, la sécurité d'accès du code exécute les fonctions suivantes :  
  
-   Définit les autorisations et les jeux d'autorisations qui représentent le droit d'accéder à diverses ressources système.  
  
-   Permet au code de demander que ses appelants possèdent des autorisations spécifiques.  
  
-   Permet au code de demander que ses appelants possèdent une signature numérique, ce qui permet ainsi que l'appel du code protégé soit uniquement effectué par des appelants d'une organisation ou d'un site spécifique.  
  
-   Applique des restrictions sur le code au moment de l'exécution en comparant les autorisations accordées de chaque appelant sur la pile d'appels avec les autorisations que les appelants doivent posséder.  
  
<a name="walking_the_call_stack"></a>   
## <a name="walking-the-call-stack"></a>Parcours de la pile des appels  
 Pour déterminer si le code est autorisé à accéder à une ressource ou à exécuter une opération, le système de sécurité du runtime parcourt la pile des appels, en comparant les autorisations accordées de chaque appelant à l'autorisation demandée. Si un appelant dans la pile des appels n'a pas l'autorisation demandée, une exception de sécurité est levée et l'accès est refusé. Le parcours de la pile est conçu pour éviter les attaques malveillantes au cours desquelles du code ayant un niveau de confiance plus faible appelle du code ayant un niveau de confiance élevé et l'utilise pour exécuter des actions non autorisées. Demander les autorisations de tous les appelants au moment de l'exécution affecte les performances, mais est essentiel pour protéger le code contre les attaques malveillantes de code ayant un niveau de confiance plus faible. Pour optimiser les performances, vous pouvez faire en sorte que votre code effectue moins de parcours de pile ; vous devez cependant être sûr que vous ne mettez pas la sécurité en danger quand vous faites cela.  
  
 L'illustration suivante présente le parcours de la pile obtenu quand une méthode dans l'assembly A4 réclame que ses appelants bénéficient de l'autorisation P.  
  
 ![Sécurité d’accès du code](../../../docs/framework/misc/media/slide-10a.gif "slide_10a")  
Parcours de pile de sécurité  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>Rubriques connexes  
  
|Titre|Description|  
|-----------|-----------------|  
|[Notions fondamentales de la sécurité d’accès du code](../../../docs/framework/misc/code-access-security-basics.md)|Décrit la sécurité d'accès du code et ses principales utilisations.|  
|[Code Transparent de sécurité, niveau 2](../../../docs/framework/misc/security-transparent-code-level-2.md)|Décrit le modèle de transparence de sécurité dans le [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)].|  
|[Utilisation de bibliothèques à partir de code d’un niveau de confiance partiel](../../../docs/framework/misc/using-libraries-from-partially-trusted-code.md)|Décrit comment activer des bibliothèques en vue d'une utilisation avec du code non managé et comment utiliser des bibliothèques à partir d'un code non managé.|  
|[Concepts fondamentaux sur la sécurité](../../../docs/standard/security/key-security-concepts.md)|Offre une vue d'ensemble de nombreux termes et concepts clés utilisés dans le système de sécurité .NET Framework.|  
|[Sécurité basée sur les rôles](../../../docs/standard/security/role-based-security.md)|Décrit comment incorporer la sécurité basée sur les rôles.|  
|[Cryptographic Services](../../../docs/standard/security/cryptographic-services.md)|Décrit comment incorporer le chiffrement dans vos applications.|
