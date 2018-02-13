---
title: Ngen.exe (Native Image Generator)
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Native Image Generator
- images [.NET Framework], native
- side-by-side execution, native images
- assemblies [.NET Framework], native image
- Ngen.exe
- native image generation
- native image cache
- publisher policy applied for native images
- invalid images
- BypassNGenAttribute
- System.Runtime.BypassNGenAttribute
ms.assetid: 44bf97aa-a9a4-4eba-9a0d-cfaa6fc53a66
caps.latest.revision: "57"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 20c120323356171d78da35a490488f4654baece6
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="ngenexe-native-image-generator"></a>Ngen.exe (Native Image Generator)
L'outil Native Image Generator Tool (Ngen.exe) est un outil qui améliore les performances des applications managées. Ngen.exe crée des images natives, qui sont des fichiers contenant le code machine compilé spécifique au processeur, et les installe dans le cache des images natives sur l'ordinateur local. Le runtime peut utiliser des images natives du cache plutôt que le compilateur juste-à-temps (JIT) pour compiler l'assembly d'origine.  
  
 Modifications apportées à Ngen.exe dans le [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] :  
  
-   Ngen.exe compile maintenant des assemblys avec une confiance totale et la stratégie de sécurité d'accès du code (CAS) n'est plus évaluée.  
  
-   Les images natives générées avec Ngen.exe ne peuvent plus être chargées dans les applications qui s'exécutent avec une confiance partielle.  
  
 Modifications apportées à Ngen.exe dans le .NET Framework version 2.0 :  
  
-   L'installation d'un assembly installe également ses dépendances, en simplifiant la syntaxe de Ngen.exe.  
  
-   Les images natives peuvent maintenant être partagées entre les domaines d'application.  
  
-   Une nouvelle action, `update`, recrée des images qui ont été invalidées.  
  
-   L'exécution des actions peuvent être différées par un service qui utilise la durée d'inactivité de l'ordinateur pour générer et installer des images.  
  
-   Certaines causes d'invalidation d'images ont été éliminées.  
  
 Sur Windows 8, consultez [Tâche d’image native](http://msdn.microsoft.com/library/9b1f7590-4e0d-4737-90ef-eaf696932afb).  
  
 Pour plus d’informations sur l’utilisation de Ngen.exe et du service d’images natives, consultez [Service d’images natives][Native Image Service].  
  
> [!NOTE]
>  Vous trouverez la syntaxe de Ngen.exe pour les versions 1.0 et 1.1 du .NET Framework dans [Syntaxe héritée du générateur d’images natives (Ngen.exe)](http://msdn.microsoft.com/library/5a69fc7a-103f-4afc-8ab4-606adcb46324).  
  
 Cet outil est installé automatiquement avec Visual Studio. Pour exécuter l'outil, utilisez l'invite de commandes développeur (ou l'invite de commandes Visual Studio dans Windows 7). Pour plus d'informations, consultez [Invites de commandes](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 À l'invite de commandes, tapez le texte suivant :  
  
## <a name="syntax"></a>Syntaxe  
  
```  
ngen action [options]  
```  
  
```  
ngen /? | /help  
```  
  
## <a name="actions"></a>Actions  
 Le tableau ci-après décrit la syntaxe de chaque `action`. Pour obtenir une description de chaque partie d’une `action`, consultez les tableaux [Arguments](#ArgumentTable), [Niveaux de priorité](#PriorityTable), [Scénarios](#ScenarioTable) et [Config](#ConfigTable). Le tableau [Options](#OptionTable) décrit les `options` et les commutateurs d'aide.  
  
|Action|Description|  
|------------|-----------------|  
|`install` [`assemblyName` &#124; `assemblyPath`] [`scenarios`] [`config`] [`/queue`[`:`{`1`&#124;`2`&#124;`3`}]]|Générer des images natives pour un assembly et ses dépendances et installer les images dans le cache des images natives.<br /><br /> Si `/queue` est spécifié, l'action est mise en file d'attente pour le service d'images natives. La priorité par défaut est 3. Consultez le tableau [Niveaux de priorité](#PriorityTable).|  
|`uninstall` [`assemblyName` &#124; `assemblyPath`] [`scenarios`] [`config`]|Supprimer les images natives d'un assembly et ses dépendances du cache des images natives.<br /><br /> Pour désinstaller une seule image et ses dépendances, utilisez les mêmes arguments de ligne de commande que ceux utilisés pour installer l’image. **Remarque :** À compter du [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], l'action `uninstall` * n'est plus prise en charge.|  
|`update` [`/queue`]|Mettre à jour des images natives qui sont devenues non valides.<br /><br /> Si `/queue` est spécifié, les mises à jour sont mises en file d'attente pour le service d'images natives. Les mises à jour sont toujours planifiées à la priorité 3, de sorte qu'elles s'exécutent lorsque l'ordinateur est inactif.|  
|`display` [`assemblyName` &#124; `assemblyPath`]|Afficher l'état des images natives pour un assembly et ses dépendances.<br /><br /> Si aucun argument n’est fourni, tout dans le cache des images natives est affiché.|  
|`executeQueuedItems` [<code>1&#124;2&#124;3</code>]<br /><br /> - ou -<br /><br /> `eqi` [1&#124;2&#124;3]|Exécuter les travaux de compilation en attente.<br /><br /> Si une priorité est spécifiée, les travaux de compilation présentant une priorité supérieure ou égale sont exécutés. Si aucune priorité n'est spécifiée, tous les travaux de compilation en attente sont exécutés.|  
|`queue` {`pause` &#124; `continue` &#124; `status`}|Suspendre le service d'images natives, reprendre le service suspendu ou interroger l'état du service.|  
  
<a name="ArgumentTable"></a>   
## <a name="arguments"></a>Arguments  
  
|Argument|Description|  
|--------------|-----------------|  
|`assemblyName`|Nom complet de l'assembly. Par exemple, `"myAssembly, Version=2.0.0.0, Culture=neutral, PublicKeyToken=0038abc9deabfle5"`. **Remarque :** Vous pouvez fournir un nom d'assembly partiel, comme `myAssembly`, pour les actions `display` et `uninstall`. <br /><br /> Un seul assembly peut être spécifié par la ligne de commande Ngen.exe.|  
|`assemblyPath`|Chemin d’accès explicite de l’assembly. Vous pouvez spécifier un chemin d'accès complet ou relatif.<br /><br /> Si vous spécifiez un nom de fichier sans chemin d'accès, l'assembly doit se trouver dans le répertoire actif.<br /><br /> Un seul assembly peut être spécifié par la ligne de commande Ngen.exe.|  
  
<a name="PriorityTable"></a>   
## <a name="priority-levels"></a>Niveaux de priorité  
  
|Priorité|Description|  
|--------------|-----------------|  
|`1`|Les images natives sont générées et installées immédiatement, sans attendre la durée d'inactivité.|  
|`2`|Les images natives sont générées et installées sans attendre la durée d'inactivité, mais après la fin de toutes les actions de priorité 1 (et de leurs dépendances).|  
|`3`|Les images natives sont installées lorsque le service d'images natives détecte que l'ordinateur est inactif. Consultez [Service d’images natives][Native Image Service].|  
  
<a name="ScenarioTable"></a>   
## <a name="scenarios"></a>Scénarios  
  
|Scénario|Description|  
|--------------|-----------------|  
|`/Debug`|Générer des images natives qui peuvent être utilisées sous un débogueur.|  
|`/Profile`|Générer des images natives qui peuvent être utilisées sous un profileur.|  
|`/NoDependencies`|Générer le nombre minimal d'images natives requis par les options de scénario spécifiées.|  
  
<a name="ConfigTable"></a>   
## <a name="config"></a>Config  
  
|Configuration|Description|  
|-------------------|-----------------|  
|`/ExeConfig:` `exePath`|Utiliser la configuration de l'assembly exécutable spécifiée.<br /><br /> Ngen.exe doit prendre les mêmes décisions que le chargeur lors de la liaison avec les dépendances. Lorsqu'un composant partagé est chargé au moment de l'exécution, à l'aide de la méthode <xref:System.Reflection.Assembly.Load%2A>, le fichier de configuration de l'application détermine les dépendances qui sont chargées pour le composant partagé, par exemple, la version d'une dépendance qui est chargée. Le commutateur `/ExeConfig` donne à Ngen.exe des instructions sur les dépendances qui seraient chargées au moment de l'exécution.|  
|`/AppBase:` `directoryPath`|Lors de la localisation des dépendances, utilisez le répertoire spécifié comme base de l'application.|  
  
<a name="OptionTable"></a>   
## <a name="options"></a>Options  
  
|Option|Description|  
|------------|-----------------|  
|`/nologo`|Supprimer l'affichage de la bannière de démarrage Microsoft.|  
|`/silent`|Supprimer l'affichage des messages d'opération réussie.|  
|`/verbose`|Afficher des informations détaillées sur le débogage. **Remarque :** En raison des limitations du système d'exploitation, cette option n'affiche pas autant d'informations supplémentaires sur Windows 98 et Windows Millennium.|  
|`/help`, `/?`|Afficher la syntaxe de commande et les options de la version actuelle.|  
  
## <a name="remarks"></a>Notes  
 Pour exécuter Ngen.exe, vous devez disposer de privilèges d'administrateur.  
  
> [!CAUTION]
>  N'exécutez pas Ngen.exe sur les assemblys dont le niveau de confiance n'est pas suffisant. Si vous démarrez avec le [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], Ngen.exe compile des assemblys avec une confiance totale et la stratégie de sécurité d'accès du code (CAS) n'est plus évaluée.  
  
 Si vous démarrez avec le [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)], les images natives générées avec Ngen.exe ne peuvent plus être chargées dans les applications qui s'exécutent avec une confiance partielle. À la place, le compilateur juste-à-temps (JIT) est appelé.  
  
 Ngen.exe génère des images natives pour l'assembly spécifié par l’argument `assemblyname` passé à l’action `install` et toutes ses dépendances. Les dépendances sont déterminées à partir de références du manifeste d'assembly. Le seul scénario dans lequel vous devez installer une dépendance séparément est lorsque l'application la charge à l'aide de la réflexion, en appelant la méthode <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> par exemple.  
  
> [!IMPORTANT]
>  N'utilisez pas la méthode <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType> avec les images natives. Une image chargée avec cette méthode ne peut pas être utilisée par d'autres assemblys dans le contexte d'exécution.  
  
 Ngen.exe conserve un décompte des dépendances. Par exemple, supposons que `MyAssembly.exe` et `YourAssembly.exe` sont installés tous les deux dans le cache des images natives et qu'ils contiennent tous les deux des références à `OurDependency.dll`. Si `MyAssembly.exe` est désinstallé, `OurDependency.dll` n'est pas désinstallée. Il est supprimé uniquement lorsque `YourAssembly.exe` est également désinstallé.  
  
 Si vous générez une image native pour un assembly dans le Global Assembly Cache, spécifiez son nom complet. Consultez <xref:System.Reflection.Assembly.FullName%2A?displayProperty=nameWithType>.  
  
 Les images natives que Ngen.exe génère peuvent être partagées entre des domaines d'application. Cela signifie que vous ne pouvez pas utiliser Ngen.exe dans des scénarios d'application qui nécessitent que les assemblys soient partagés par des domaines d'application. Pour spécifier la neutralité de domaine :  
  
-   Appliquez l'attribut <xref:System.LoaderOptimizationAttribute> à votre application.  
  
-   Définissez la propriété <xref:System.AppDomainSetup.LoaderOptimization%2A?displayProperty=nameWithType> lorsque vous créez des informations de configuration pour un nouveau domaine d'application.  
  
 Utilisez toujours un code indépendant du domaine lors du chargement du même assembly dans plusieurs domaines d'application. Si une image native est chargée dans un domaine d'application non partagé après avoir été chargée dans un domaine partagé, elle ne peut pas être utilisée.  
  
> [!NOTE]
>  Le code indépendant du domaine ne peut pas être déchargé et les performances peuvent être légèrement plus lentes, en particulier lors de l'accès aux membres statiques.  
  
 Dans cette section Notes :  
  
-   [Génération d'images dans différents scénarios](#Scenarios)  
  
-   [Détermination des cas d'utilisation des images natives](#WhenToUse)  
  
    -   [Amélioration de l'utilisation de la mémoire](#Memory)  
  
    -   [Démarrage d'applications plus rapide](#Startup)  
  
    -   [Récapitulatif des considérations relatives à l'utilisation](#UsageSummary)  
  
-   [Importance des adresses de base d'assemblys](#BaseAddresses)  
  
-   [Liaison matérielle](#HardBinding)  
  
    -   [Spécification d’une indication sur la liaison d’une dépendance](#DependencyHint)  
  
    -   [Spécification d’une indication sur la liaison par défaut d’un assembly](#AssemblyHint)  
  
-   [Traitement différé](#Deferred)  
  
-   [Images natives et compilation JIT](#JITCompilation)  
  
    -   [Images non valides](#InvalidImages)  
  
-   [Résolution des problèmes](#Troubleshooting)  
  
    -   [Visionneuse du journal de liaison d’assembly](#Fusion)  
  
    -   [Assistant Débogage managé JITCompilationStart](#MDA)  
  
    -   [Désactivation de la génération des images natives](#OptOut)  
  
<a name="Scenarios"></a>   
## <a name="generating-images-for-----different-scenarios"></a>Génération d'images dans différents scénarios  
 Une fois que vous avez généré une image native pour un assembly, le runtime essaie automatiquement de la localiser et de l'utiliser chaque fois qu'il exécute l'assembly. Plusieurs images peuvent être générées, selon les scénarios d'utilisation.  
  
 Par exemple, si vous exécutez un assembly dans un scénario de débogage ou de profilage, le runtime recherche une image native générée à l'aide des options `/Debug` ou `/Profile`. S'il ne trouve pas d'image native correspondante, le runtime revient à la compilation JIT standard. La seule façon de déboguer des images natives consiste à créer une image native avec l'option `/Debug`.  
  
 L'action `uninstall` reconnaît également les scénarios, vous pouvez ainsi désinstaller tous les scénarios ou uniquement les scénarios sélectionnés.  
  
<a name="WhenToUse"></a>   
## <a name="determining-when-to-use-native-images"></a>Détermination des cas d'utilisation des images natives  
 Les images natives peuvent fournir des améliorations des performances dans deux domaines : l'amélioration de l'utilisation de la mémoire et la réduction du temps de démarrage.  
  
> [!NOTE]
>  Les performances des images natives dépendent de plusieurs facteurs qui rendent l'analyse difficile, tels que le code et les modèles d'accès aux données, le nombre d'appels effectués entre les limites de module et le nombre de dépendances déjà chargées par d'autres applications. La seule façon de déterminer si les images natives tirent parti de votre application consiste à effectuer des mesures de performances prudentes dans vos scénarios de déploiement clés.  
  
<a name="Memory"></a>   
### <a name="improved-memory-use"></a>Amélioration de l'utilisation de la mémoire  
 Les images natives peuvent considérablement améliorer l'utilisation de la mémoire lorsque le code est partagé entre des processus. Les images natives sont des fichiers PE Windows. Une seule copie d'un fichier .dll peut donc être partagée par plusieurs processus ; en revanche, le code natif produit par le compilateur JIT est stocké dans la mémoire privée et ne peut pas être partagé.  
  
 Les applications qui sont exécutées sous des services Terminal Server peuvent également bénéficier de pages de code partagées.  
  
 En outre, ne pas charger le compilateur JIT économise une quantité de mémoire fixe pour chaque instance d'application.  
  
<a name="Startup"></a>   
### <a name="faster-application-startup"></a>Démarrage d'applications plus rapide  
 La précompilation des assemblys avec Ngen.exe peut améliorer le temps de démarrage de certaines applications. En général, des progrès peuvent être réalisés lorsque les applications partagent des assemblys de composants, car après le démarrage de la première application, les composants partagés sont déjà chargés pour les applications suivantes. Le démarrage à froid, dans lequel tous les assemblys d'une application doivent être chargés à partir du disque dur, ne tire pas autant parti des images natives, car le temps d'accès au disque dur prédomine.  
  
 La liaison matérielle peut affecter le temps de démarrage, car toutes les images qui sont liées par une liaison matérielle à l'assembly d'application principale doivent être chargées en même temps.  
  
> [!NOTE]
>  Avant le [!INCLUDE[net_v35SP1_long](../../../includes/net-v35sp1-long-md.md)], vous devez mettre les composants partagés avec nom fort dans le Global Assembly Cache, étant donné que le chargeur exécute une validation supplémentaire sur les assemblys avec nom fort qui ne sont pas dans le Global Assembly Cache, en éliminant efficacement toute amélioration du temps de démarrage gagné à l'aide des images natives. Les optimisations présentées dans le [!INCLUDE[net_v35SP1_short](../../../includes/net-v35sp1-short-md.md)] ont supprimé la validation supplémentaire.  
  
<a name="UsageSummary"></a>   
### <a name="summary-of-usage-considerations"></a>Récapitulatif des considérations relatives à l'utilisation  
 Les considérations générales suivantes et celles sur l'application peuvent vous aider à décider si cela vaut la peine d'évaluer des images natives pour votre application :  
  
-   Les images natives se chargent plus vite que MSIL, car elles ne nécessitent pas beaucoup d'activités de démarrage, comme la compilation JIT et la vérification de la sécurité de type.  
  
-   Les images natives requièrent un jeu de travail initial réduit, car elles n'ont pas besoin d'un compilateur JIT.  
  
-   Les images natives activent le partage de code entre les processus.  
  
-   Les images natives requièrent plus d'espace de disque dur que les assemblys MSIL et leur génération peut nécessiter beaucoup de temps.  
  
-   Les images natives doivent être gérées.  
  
    -   Elles doivent être régénérées lorsque l'assembly d'origine ou l'une de ses dépendances est pris(e) en charge.  
  
    -   Un seul assembly peut avoir besoin de plusieurs images natives pour les utiliser dans différentes applications ou différents scénarios. Par exemple, les informations de configuration de deux applications peuvent donner lieu à des décisions différentes en matière de liaison pour le même assembly dépendant.  
  
    -   Les images natives doivent être générées par un administrateur, c'est-à-dire à partir d'un compte Windows du groupe Administrateurs.  
  
 Outre ces considérations générales, la nature de votre application doit être prise en compte lorsque vous déterminez si les images natives peuvent fournir un gain de performances :  
  
-   Si votre application s'exécute dans un environnement qui utilise beaucoup de composants partagés, les images natives permettent aux composants d'être partagés entre plusieurs processus.  
  
-   Si votre application utilise plusieurs domaines d'application, les images natives permettent à des pages de codes d'être partagées entre des domaines.  
  
    > [!NOTE]
    >  Dans les versions 1.0 et 1.1 du .NET Framework, les images natives ne peuvent pas être partagées entre des domaines d'application. Ce n'est pas le cas dans les versions 2.0 et ultérieures.  
  
-   Si votre application est exécutée sous Terminal Server, les images natives autorisent le partage des pages de code.  
  
-   Les applications volumineuses tirent généralement parti de la compilation dans des images natives. Les petites applications n'en tirent généralement pas parti.  
  
-   Pour les applications de longue durée, la compilation JIT à l'exécution est légèrement plus performante que les images natives. (La liaison matérielle peut atténuer cette différence de performances dans une certaine mesure.)  
  
<a name="BaseAddresses"></a>   
## <a name="importance-of-assembly-base-addresses"></a>Importance des adresses de base d'assemblys  
 Étant donné que les images natives sont des fichiers PE Windows, elles sont soumises aux mêmes problèmes de redéfinition que les autres fichiers exécutables. Le coût du réadressage en termes de performances est encore plus marqué si la liaison matérielle est utilisée.  
  
 Pour définir l'adresse de base d'une image native, utilisez l'option appropriée de votre compilateur pour définir l'adresse de base de l'assembly. Ngen.exe utilise cette adresse de base pour l'image native.  
  
> [!NOTE]
>  Les images natives sont plus volumineuses que les assemblys managés à partir desquels elles ont été créées. Les adresses de base doivent être calculées pour prendre en compte ces tailles plus grandes.  
  
 Vous pouvez utiliser un outil tel que dumpbin.exe pour visualiser l'adresse de base par défaut d'une image native.  
  
<a name="HardBinding"></a>   
## <a name="hard-binding"></a>Liaison matérielle  
 La liaison matérielle augmente le débit et réduit la taille du jeu de travail des images natives. L'inconvénient de la liaison matérielle réside dans le fait que toutes les images liées par une liaison matérielle à un assembly doivent être chargées lorsque l'assembly est chargé. Cela peut augmenter considérablement le temps de démarrage d'une application volumineuse.  
  
 La liaison matérielle convient aux dépendances qui sont chargées dans tous les scénarios de votre application dont les performances sont critiques. Comme dans tous les aspects de l'utilisation des images natives, les mesures de performances prudentes constituent le seul moyen de déterminer si la liaison matérielle améliore les performances de votre application.  
  
 Les attributs <xref:System.Runtime.CompilerServices.DependencyAttribute> et <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> vous permettent de fournir des indications sur la liaison matérielle à Ngen.exe.  
  
> [!NOTE]
>  Ces attributs sont des indications destinées à Ngen.exe et non des commandes. Leur utilisation ne garantit pas de liaison matérielle. La signification de ces attributs peut changer dans les versions ultérieures.  
  
<a name="DependencyHint"></a>   
### <a name="specifying-a-binding-hint-for-a-dependency"></a>Spécification d’une indication sur la liaison d’une dépendance  
 Appliquez <xref:System.Runtime.CompilerServices.DependencyAttribute> à un assembly pour indiquer la probabilité de chargement d'une dépendance spécifiée. <xref:System.Runtime.CompilerServices.LoadHint.Always?displayProperty=nameWithType> indique que la liaison matérielle est appropriée, <xref:System.Runtime.CompilerServices.LoadHint.Default> indique que la valeur par défaut de la dépendance doit être utilisée et <xref:System.Runtime.CompilerServices.LoadHint.Sometimes> indique que la liaison matérielle n'est pas appropriée.  
  
 Le code suivant affiche les attributs d'un assembly qui possède deux dépendances. La première dépendance (Assembly1) est un candidat approprié pour la liaison matérielle et la deuxième (Assembly2) ne l'est pas.  
  
```vb  
Imports System.Runtime.CompilerServices  
<Assembly:DependencyAttribute("Assembly1", LoadHint.Always)>  
<Assembly:DependencyAttribute("Assembly2", LoadHint.Sometimes)>  
```  
  
```csharp  
using System.Runtime.CompilerServices;  
[assembly:DependencyAttribute("Assembly1", LoadHint.Always)]  
[assembly:DependencyAttribute("Assembly2", LoadHint.Sometimes)]  
```  
  
```cpp  
using namespace System::Runtime::CompilerServices;  
[assembly:DependencyAttribute("Assembly1", LoadHint.Always)];  
[assembly:DependencyAttribute("Assembly2", LoadHint.Sometimes)];  
```  
  
 Le nom de l'assembly n'inclut pas l'extension de nom de fichier. Les noms complets peuvent être utilisés.  
  
<a name="AssemblyHint"></a>   
### <a name="specifying-a-default-binding-hint-for-an-assembly"></a>Spécification d’une indication sur la liaison par défaut d’un assembly  
 Les indications sur la liaison par défaut sont nécessaires uniquement pour les assemblys qui seront utilisés immédiatement et fréquemment par toute application qui possède une dépendance sur eux. Appliquez <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> avec <xref:System.Runtime.CompilerServices.LoadHint.Always?displayProperty=nameWithType> aux assemblys de ce type pour spécifier que la liaison matérielle doit être utilisée.  
  
> [!NOTE]
>  Il est inutile d'appliquer <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> aux assemblys .dll qui ne correspondent pas à cette catégorie, car l'application de l'attribut ayant une valeur autre que <xref:System.Runtime.CompilerServices.LoadHint.Always?displayProperty=nameWithType> a le même effet que de ne pas appliquer l'attribut du tout.  
  
 Microsoft utilise <xref:System.Runtime.CompilerServices.DefaultDependencyAttribute> pour spécifier que la liaison matérielle est la valeur par défaut d'un très petit nombre d'assemblys dans le .NET Framework, tel que mscorlib.dll.  
  
<a name="Deferred"></a>   
## <a name="deferred-processing"></a>Traitement différé  
 La génération d'images natives d'une application très volumineuse peut prendre beaucoup de temps. De même, les modifications apportées à un composant partagé ou aux paramètres de l'ordinateur peuvent nécessiter la mise à jour de nombreuses images natives. Les actions `install` et `update` possèdent une option `/queue` qui met en file d'attente l'opération en vue d'une exécution différée par le service d'images natives. En outre, Ngen.exe possède des actions `queue` et `executeQueuedItems` qui offrent un certain contrôle sur le service. Pour plus d’informations, consultez [Service d’images natives][Native Image Service].  
  
<a name="JITCompilation"></a>   
## <a name="native-images-and-jit-compilation"></a>Images natives et compilation JIT  
 Si, dans un assembly, Ngen.exe rencontre des méthodes qu'il ne peut pas générer, il les exclut de l'image native. Lorsque le runtime exécute cet assembly, il revient à la compilation JIT des méthodes non incluses dans l'image native.  
  
 En outre, les images natives ne sont pas utilisées si l'assembly a été mis à niveau ou si l'image a été invalidée pour une raison quelconque.  
  
<a name="InvalidImages"></a>   
### <a name="invalid-images"></a>Images non valides  
 Lorsque vous utilisez Ngen.exe pour créer une image native d'un assembly, le résultat dépend des options de ligne de commande spécifiées et de certains paramètres de votre ordinateur. Ces paramètres sont les suivants :  
  
-   Version du .NET Framework.  
  
-   Version du système d'exploitation, si vous passez de la famille Windows 9x à la famille Windows NT.  
  
-   Identité exacte de l'assembly (toute nouvelle compilation modifie l'identité).  
  
-   Identité exacte de tous les assemblys auxquels l'assembly fait référence (toute nouvelle compilation modifie l'identité).  
  
-   Facteurs de sécurité.  
  
 Ngen.exe enregistre ces informations lorsqu'il génère une image native. Lorsque vous exécutez un assembly, le runtime recherche l'image native générée à l'aide des options et des paramètres correspondant à l'environnement actif de l'ordinateur. Le runtime revient à la compilation JIT d'un assembly, s'il ne trouve pas d'image native correspondante. Les modifications suivantes des paramètres et de l'environnement d'un ordinateur entraînent la perte de validité des images natives :  
  
-   Version du .NET Framework.  
  
     Si vous appliquez une mise à jour au .NET Framework, toutes les images natives que vous avez créées à l'aide de Ngen.exe deviennent non valides. Pour cette raison, toutes les mises à jour du .NET Framework exécutent la commande `Ngen Update`, afin de s'assurer que toutes les images natives sont régénérées. Le .NET Framework crée automatiquement de nouvelles images natives pour les bibliothèques .NET Framework qu'il installe.  
  
-   Version du système d'exploitation, si vous passez de la famille Windows 9x à la famille Windows NT.  
  
     Par exemple, si la version du système d’exploitation s’exécutant sur un ordinateur passe de Windows 98 à Windows XP, toutes les images natives stockées dans le cache des images natives ne sont plus valides. Toutefois, si le système d’exploitation passe de Windows 2000 à Windows XP, les images restent valides.  
  
-   Identité exacte de l'assembly.  
  
     Si vous recompilez un assembly, l'image native correspondante de l'assembly devient non valide.  
  
-   Identité exacte des assemblys auxquels l'assembly fait référence.  
  
     Si vous mettez à jour un assembly managé, toutes les images natives qui dépendent directement ou indirectement de cet assembly deviennent non valides et doivent être régénérées. Cela inclut des références ordinaires et des dépendances liées par une liaison matérielle. Chaque fois qu'une mise à jour de logiciel est appliquée, le programme d'installation doit exécuter une commande `Ngen Update` pour garantir que toutes les images natives dépendantes sont régénérées.  
  
-   Facteurs de sécurité.  
  
     Le changement de stratégie de sécurité d'un ordinateur pour restreindre les autorisations précédemment accordées à un assembly peut entraîner la perte de validité d'une image native précédemment compilée de cet assembly.  
  
     Pour plus d'informations sur la façon dont le Common Language Runtime administre la sécurité d'accès du code et sur l'utilisation des autorisations, consultez [Sécurité d'accès du code](../../../docs/framework/misc/code-access-security.md).  
  
<a name="Troubleshooting"></a>   
## <a name="troubleshooting"></a>Résolution des problèmes  
 Les rubriques de résolution de problèmes suivantes vous permettent d’identifier les images natives qui sont utilisées par votre application et celles qui ne le peuvent pas, de déterminer quand le compilateur JIT commence à compiler une méthode, et montrent comment désactiver la compilation d’images natives des méthodes spécifiées.  
  
<a name="Fusion"></a>   
### <a name="assembly-binding-log-viewer"></a>visionneuse du journal de liaison d’assembly  
 Pour confirmer que les images natives sont utilisées par votre application, vous pouvez utiliser [Fuslogvw.exe (Visionneuse du journal de liaison d’assembly)](../../../docs/framework/tools/fuslogvw-exe-assembly-binding-log-viewer.md). Sélectionnez **Images natives** dans la zone **Catégories du journal** dans la fenêtre de la visionneuse du journal des liaisons. Fuslogvw.exe fournit des informations sur la raison pour laquelle une image native a été rejetée.  
  
<a name="MDA"></a>   
### <a name="the-jitcompilationstart-managed-debugging-assistant"></a>Assistant Débogage managé JITCompilationStart  
 Vous pouvez utiliser l'Assistant Débogage managé (MDA) [JITCompilationStart](../../../docs/framework/debug-trace-profile/jitcompilationstart-mda.md) pour déterminer quand le compilateur JIT commence à compiler une fonction.  
  
<a name="OptOut"></a>   
### <a name="opting-out-of-native-image-generation"></a>Désactivation de la génération des images natives  
 Dans certains cas, NGen.exe peut avoir des difficultés à générer une image native pour une méthode spécifique, ou vous pouvez préférer que la méthode soit compilée par JIT et non compilée dans une image native. Dans ce cas, vous pouvez utiliser l’attribut `System.Runtime.BypassNGenAttribute` pour éviter que NGen.exe génère une image native pour une méthode particulière. L’attribut doit être appliqué individuellement à chaque méthode dont vous ne voulez pas inclure le code dans l’image native. NGen.exe reconnaît l’attribut et ne génère pas de code dans l’image native pour la méthode correspondante.  
  
 Toutefois, notez que `BypassNGenAttribute` n’est pas défini comme un type dans la bibliothèque de classes .NET Framework. Pour pouvoir utiliser l’attribut dans votre code, vous devez d’abord le définir de la façon suivante :  
  
 [!code-csharp[System.Runtime.BypassNGenAttribute#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/System.Runtime.BypassNGenAttribute/cs/Optout1.cs#1)]
 [!code-vb[System.Runtime.BypassNGenAttribute#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/System.Runtime.BypassNGenAttribute/vb/Optout1.vb#1)]  
  
 Vous pouvez ensuite appliquer l’attribut selon la méthode. Dans l’exemple suivant, le générateur d’images natives reçoit l’instruction de ne pas générer d’image native pour la méthode `ExampleClass.ToJITCompile`.  
  
 [!code-csharp[System.Runtime.BypassNGenAttribute#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/System.Runtime.BypassNGenAttribute/cs/Optout1.cs#2)]
 [!code-vb[System.Runtime.BypassNGenAttribute#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/System.Runtime.BypassNGenAttribute/vb/Optout1.vb#2)]  
  
## <a name="examples"></a>Exemples  
 La commande suivante génère une image native de `ClientApp.exe`, située dans le répertoire actif, puis installe l'image dans le cache des images natives. S'il existe un fichier de configuration de l'assembly, Ngen.exe l'utilise. En outre, les images natives sont générées pour tous les fichiers .dll auxquels `ClientApp.exe` fait référence.  
  
```  
ngen install ClientApp.exe  
```  
  
 Une image installée avec Ngen.exe est également appelée une racine. Une racine peut être une application ou un composant partagé.  
  
 La commande suivante génère une image native de `MyAssembly.exe` en fonction du chemin d'accès spécifié.  
  
```  
ngen install c:\myfiles\MyAssembly.exe  
```  
  
 Lors de la localisation des assemblys et de leurs dépendances, Ngen.exe utilise la même logique de détection que celle utilisée par le Common Language Runtime. Par défaut, le répertoire qui contient `ClientApp.exe` est utilisé comme répertoire de base de l'application et toute la recherche d'assemblys commence dans ce répertoire. Vous pouvez remplacer ce comportement en utilisant l'option `/AppBase`.  
  
> [!NOTE]
>  Il s'agit là d'un changement par rapport au comportement de Ngen.exe dans les versions 1.0 et 1.1 du .NET Framework, dans lesquelles la base de l'application est définie sur le répertoire actif.  
  
 Un assembly peut posséder une dépendance sans référence, par exemple, s'il charge un fichier .dll en utilisant la méthode <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType>. Vous pouvez créer une image native d'un fichier .dll de ce type en utilisant des informations de configuration de l'assembly d'application, avec l'option `/ExeConfig`. La commande suivante génère une image native de `MyLib.dll,` à l'aide des informations de configuration de `MyApp.exe`.  
  
```  
ngen install c:\myfiles\MyLib.dll /ExeConfig:c:\myapps\MyApp.exe  
```  
  
 Les assemblys installés grâce à cette méthode ne sont pas supprimés lorsque l'application est supprimée.  
  
 Pour désinstaller une dépendance, utilisez les mêmes options de ligne de commande que celles qui ont servi à l'installer. La commande suivante désinstalle `MyLib.dll` de l'exemple précédent.  
  
```  
ngen uninstall c:\myfiles\MyLib.dll /ExeConfig:c:\myapps\MyApp.exe  
```  
  
 Pour créer une image native d'un assembly dans le Global Assembly Cache, utilisez le nom complet de l'assembly. Par exemple :  
  
```  
ngen install "ClientApp, Version=1.0.0.0, Culture=neutral,   
  PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL"  
```  
  
 NGen.exe génère un ensemble d'images séparé pour chaque scénario que vous installez. Par exemple, les commandes suivantes installent un jeu complet d'images natives pour les opérations normales, un autre jeu complet pour le débogage et un troisième pour le profilage :  
  
```  
ngen install MyApp.exe  
ngen install MyApp.exe /debug  
ngen install MyApp.exe /profile  
```  
  
### <a name="displaying-the-native-image-cache"></a>Affichage du cache des images natives  
 Une fois les images natives installées dans le cache, elles peuvent être affichées à l'aide de Ngen.exe. La commande suivante affiche toutes les images natives du cache des images natives.  
  
```  
ngen display  
```  
  
 L'action `display` répertorie d'abord tous les assemblys racine, puis toutes les images natives sur l'ordinateur.  
  
 Utilisez le nom simple d'un assembly pour afficher uniquement les informations de cet assembly. La commande suivante affiche toutes les images natives dans le cache des images natives qui correspondent au nom partiel `MyAssembly`, leurs dépendances et toutes les racines qui ont une dépendance sur `MyAssembly` :  
  
```  
ngen display MyAssembly  
```  
  
 Connaître les racines qui dépendent d'un assembly de composant partagé est utile pour mesurer l'impact d'une action `update` après la mise à niveau du composant partagé.  
  
 Si vous spécifiez l’extension de fichier d’un assembly, vous devez spécifier le chemin d’accès ou exécuter Ngen.exe à partir du répertoire qui contient l’assembly :  
  
```  
ngen display c:\myApps\MyAssembly.exe  
```  
  
 La commande suivante affiche toutes les images natives du cache des images natives avec le nom `MyAssembly` et la version 1.0.0.0.  
  
```  
ngen display "myAssembly, version=1.0.0.0"  
```  
  
### <a name="updating-images"></a>Mise à jour d'images  
 Les images sont généralement mises à jour après la mise à niveau d'un composant partagé. Pour mettre à jour toutes les images natives qui ont été modifiées ou dont les dépendances ont été modifiées, utilisez l'action `update` sans arguments.  
  
```  
ngen update  
```  
  
 La mise à jour de toutes les images peut prendre du temps. Vous pouvez mettre en file d'attente les mises à jour pour une exécution par le service d'images natives en utilisant l'option `/queue`. Pour plus d’informations sur l’option `/queue` et les priorités d’installation, consultez [Service d’images natives][Native Image Service].  
  
```  
ngen update /queue  
```  
  
### <a name="uninstalling-images"></a>Désinstallation d'images  
 Ngen.exe gère une liste de dépendances, de sorte que les composants partagés soient supprimés uniquement lorsque tous les assemblys qui dépendent d'eux ont été supprimés. En outre, un composant partagé n'est pas supprimé s'il a été installé comme racine.  
  
 La commande suivante désinstalle tous les scénarios de `ClientApp.exe` racine :  
  
```  
ngen uninstall ClientApp  
```  
  
 L'action `uninstall` peut être utilisée pour supprimer des scénarios spécifiques. La commande suivante désinstalle tous les scénarios de débogage de `ClientApp.exe` :  
  
```  
ngen uninstall ClientApp /debug  
```  
  
> [!NOTE]
>  La désinstallation de scénarios `/debug` ne désinstalle pas un scénario qui inclut `/profile` et `/debug.`  
  
 La commande suivante désinstalle tous les scénarios d'une version spécifique de `ClientApp.exe` :  
  
```  
ngen uninstall "ClientApp, Version=1.0.0.0"  
```  
  
 Les commandes suivantes désinstallent tous les scénarios de `"ClientApp, Version=1.0.0.0, Culture=neutral, PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL",` ou seulement le scénario de débogage de cet assembly :  
  
```  
ngen uninstall "ClientApp, Version=1.0.0.0, Culture=neutral,   
  PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL"  
ngen uninstall "ClientApp, Version=1.0.0.0, Culture=neutral,   
  PublicKeyToken=3c7ba247adcd2081, processorArchitecture=MSIL" /debug  
```  
  
 Comme avec l'action `install`, le fait de fournir une extension requiert d'exécuter Ngen.exe à partir du répertoire contenant l'assembly ou de spécifier un chemin d'accès complet.  
  
 Pour obtenir des exemples liés au service d’images natives, consultez [Service d’images natives][Native Image Service].  
  
## <a name="native-image-task"></a>Tâche d’image native  
 La tâche d'image native est une tâche Windows qui génère et conserve des images natives. La tâche d’image native génère et libère les images natives automatiquement pour les scénarios pris en charge. (Consultez [Création d'images natives](http://msdn.microsoft.com/library/2bc8b678-dd8d-4742-ad82-319e9bf52418).) Elle permet aussi aux programmes d'installation d'utiliser [Ngen.exe (Générateur d'images natives)](../../../docs/framework/tools/ngen-exe-native-image-generator.md) pour créer et mettre à jour des images natives à un moment différé.  
  
 La tâche d’image native est enregistrée une seule fois pour chaque architecture de processeur prise en charge sur un ordinateur, pour permettre la compilation des applications qui ciblent chaque architecture :  
  
|Nom de la tâche|Ordinateur 32 bits|Ordinateur 64 bits|  
|---------------|----------------------|----------------------|  
|.NET Framework NGEN v4.0.30319|Oui|Oui|  
|NET Framework NGEN v4.0.30319 64|Non|Oui|  
  
 La tâche d’image native est disponible dans le .NET Framework 4.5 et versions ultérieures, dans le cadre d’une exécution sur Windows 8 ou version ultérieure. Dans les versions antérieures de Windows, le .NET Framework utilise le [Service d’images natives][Native Image Service].  
  
### <a name="task-lifetime"></a>Durée de vie de la tâche  
 En général, le Planificateur de tâches Windows démarre la tâche d'image native chaque nuit quand l'ordinateur est inactif. La tâche recherche tout travail différé mis en attente par les programmes d'installation de l'application, toutes les demandes de mise à jour différée des images natives et toute création automatique d'images. La tâche termine les éléments de travail en attente, puis s'arrête. Si l'ordinateur cesse d'être inactif alors que la tâche s'exécute, celle-ci s'arrête.  
  
 Vous pouvez également démarrer la tâche d'image native manuellement à l'aide de l'interface utilisateur du Planificateur de tâches ou via des appels manuels à NGen.exe. Si la tâche est démarrée par le biais de ces méthodes, elle continue à s'exécuter quand l'ordinateur n'est plus inactif. Les images créées manuellement à l'aide de NGen.exe sont hiérarchisées pour activer un comportement prévisible pour les programmes d'installation de l'application.  
  
## <a name="native-image-service"></a>Service d'images natives  
 Le service d'images natives est un service Windows qui génère et conserve des images natives. Le service d'images natives permet au développeur de différer l'installation et la mise à jour d'images natives jusqu'au moment où l'ordinateur est inactif.  
  
 Normalement, le service d'images natives est lancé par le programme d'installation d'une application ou mise à jour. Pour les actions de priorité 3, le service s'exécute pendant que l'ordinateur est inactif. Le service enregistre son état et est capable de poursuivre après de multiples redémarrages si nécessaire. Plusieurs compilations d'images peuvent être mises en attente.  
  
 Le service interagit également avec la commande Ngen.exe manuelle. Les commandes manuelles sont prioritaires sur l'activité en arrière-plan.  
  
> [!NOTE]
>  Sur Windows Vista, le nom affiché pour le service d'images natives est « Microsoft.NET Framework NGEN v2.0.50727_X86 » ou « Microsoft.NET Framework NGEN v2.0.50727_X64 ». Sur toutes les versions antérieures de Microsoft Windows, le nom est « .NET Runtime Optimization Service v2.0.50727_X86 » ou « .NET Runtime Optimization Service v2.0.50727_X64 ».  
  
### <a name="launching-deferred-operations"></a>Lancement d'opérations différées  
 Avant de commencer une installation ou une mise à niveau, il est recommandé d'interrompre le service. Cette interruption garantit que le service ne s'exécute pas pendant que le programme d'installation copie des fichiers ou place des assemblys dans le Global Assembly Cache. La ligne de commande Ngen.exe suivante interrompt le service :  
  
```  
ngen queue pause  
```  
  
 Quand toutes les opérations différées ont été mises en attente, la commande suivante autorise le service à reprendre :  
  
```  
ngen queue continue  
```  
  
 Pour différer la génération d'images natives lors de l'installation d'une nouvelle application ou lors de la mise à jour d'un composant partagé, utilisez l'option `/queue` avec les actions `install` ou `update`. Les lignes de commande Ngen.exe suivantes installent une image native pour un composant partagé et effectuent une mise à jour de toutes les racines éventuellement affectées :  
  
```  
ngen install MyComponent /queue  
ngen update /queue  
```  
  
 L'action `update` régénère toutes les images natives qui ont été invalidées, pas uniquement celles qui utilisent `MyComponent`.  
  
 Si votre application se compose de nombreuses racines, vous pouvez contrôler la priorité des actions différées. Les commandes suivantes mettent en file d'attente l'installation de trois racines. `Assembly1` est installé en premier, sans attendre l'inactivité. `Assembly2` est également installé sans attendre l'inactivité, mais une fois que toutes les actions de priorité 1 sont terminées. `Assembly3` est installé quand le service détecte que l'ordinateur est inactif.  
  
```  
ngen install Assembly1 /queue:1  
ngen install Assembly2 /queue:2  
ngen install Assembly3 /queue:3  
```  
  
 Vous pouvez forcer des actions mises en file d'attente à se produire de façon synchrone à l'aide de l'action `executeQueuedItems`. Si vous fournissez la priorité facultative, cette action affecte uniquement les actions mises en file d'attente qui ont une priorité égale ou inférieure. La priorité par défaut est 3, donc la commande Ngen.exe suivante traite toutes les actions mises en file d'attente immédiatement et ne retourne pas de résultat tant qu'elles ne sont pas terminées :  
  
```  
ngen executeQueuedItems  
```  
  
 Les commandes synchrones sont exécutées par Ngen.exe et n'utilisent pas le service d'images natives. Vous pouvez exécuter des actions à l'aide de Ngen.exe pendant que le service d'images natives s'exécute.  
  
### <a name="service-shutdown"></a>Arrêt du service  
 Après avoir été initialisé par l'exécution d'une commande Ngen.exe qui inclut l'option `/queue`, le service s'exécute en arrière-plan jusqu'à ce que toutes les actions aient été effectuées. Le service enregistre son état pour pouvoir continuer via de multiples redémarrages si nécessaire. Quand le service détecte qu'il n'y aucune action en attente, il réinitialise son état afin de ne pas redémarrer la prochaine fois que l'ordinateur est démarré, puis il s'arrête.  
  
### <a name="service-interaction-with-clients"></a>Interaction du service avec les clients  
 Dans le .NET Framework version 2.0, la seule interaction avec le service d'images natives s'effectue via l'outil en ligne de commande Ngen.exe. Utilisez l'outil en ligne de commande dans les scripts d'installation pour mettre en file d'attente des actions pour le service d'images natives et interagir avec le service.  
  
## <a name="see-also"></a>Voir aussi  
 [Outils](../../../docs/framework/tools/index.md)  
 [Processus d'exécution managée](../../../docs/standard/managed-execution-process.md)  
 [Méthode de localisation des assemblys par le runtime](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)  
 [Invites de commandes](../../../docs/framework/tools/developer-command-prompt-for-vs.md)

[Native Image Service]: #native-image-service
