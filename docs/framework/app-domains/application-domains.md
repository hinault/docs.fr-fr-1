---
title: Domaines d'application
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- process boundaries for isolation
- application isolation
- application domains, about
- common language runtime, application domains
- application domains
- runtime, application domains
- isolation between applications
- code, verification process
- verification testing code
ms.assetid: 113a8bbf-6875-4a72-a49d-ca2d92e19cc8
caps.latest.revision: "18"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: fe2d8ea8be2781e747398e18cc99cc6ce6cf6dc5
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="application-domains"></a>Domaines d'application
Les systèmes d'exploitation et les environnements d'exécution assurent généralement une certaine forme d'isolation entre les applications. Par exemple, Windows utilise des processus pour isoler des applications. Cette isolation est nécessaire pour que le code en cours d'exécution dans une application ne puisse pas affecter de manière négative d'autres applications non liées.  
  
 Les domaines d'application fournissent une limite d'isolation pour la sécurité, la fiabilité, le suivi des versions et le déchargement des assemblys. Les domaines d'application sont généralement créés par des hôtes de runtime qui sont chargés d'initialiser le Common Language Runtime avant l'exécution d'une application.  
  
 Les rubriques de cette section de la documentation expliquent comment utiliser des domaines d'application pour assurer l'isolation entre les assemblys.  
  
 Cette vue d'ensemble contient les sections suivantes :  
  
-   [Avantages de l’isolation des applications](#benefits)  
  
-   [Référence](#reference)  
  
<a name="benefits"></a>   
## <a name="the-benefits-of-isolating-applications"></a>Avantages de l'isolation des applications  
 Du point de vue historique, les limites de processus ont permis d'isoler les applications en cours d'exécution sur le même ordinateur. Chaque application est chargée dans un processus distinct, ce qui isole l'application des autres applications en cours d'exécution sur le même ordinateur.  
  
 Les applications sont isolées, car les adresses mémoire sont liées au processus ; un pointeur mémoire passé d'un processus à un autre ne peut pas être utilisé d'une manière significative dans le processus cible. De plus, vous ne pouvez pas établir d'appels directs entre deux processus. Vous devez à la place utiliser des proxys qui génèrent un niveau d'adressage indirect.  
  
 Le code managé doit passer par un processus de vérification avant de pouvoir être exécuté (sauf si l'administrateur a accordé l'autorisation d'ignorer la vérification). Le processus de vérification détermine si le code peut essayer d'accéder à des adresses mémoire non valides ou effectuer d'autres actions risquant d'empêcher le processus dans lequel il s'exécute de fonctionner correctement. Le code qui réussit le test de vérification est considéré comme étant de type sécurisé. La capacité à vérifier si le code est de type sécurisé permet au Common Language Runtime d'assurer un niveau d'isolation aussi élevé que celui de la limite de processus, à un coût de performances beaucoup plus réduit.  
  
 Les domaines d'application fournissent une unité de traitement davantage sécurisée et polyvalente que le Common Language Runtime peut utiliser pour assurer l'isolation entre les applications. Vous pouvez exécuter plusieurs domaines d'application dans un seul processus avec le même niveau d'isolation que dans des processus distincts, mais sans risquer une surcharge mémoire en établissant des appels interprocessus ou en passant d'un processus à un autre. La capacité à exécuter plusieurs applications dans un seul processus optimise considérablement l'extensibilité du serveur.  
  
 L'isolation des applications est également importante pour la sécurité des applications. Par exemple, vous pouvez exécuter des contrôles à partir de plusieurs applications Web dans un seul processus de navigateur, de telle sorte que les contrôles ne puissent pas accéder à leurs données et à leurs ressources respectives.  
  
 L'isolation assurée par les domaines d'application présente les avantages suivants :  
  
-   Les erreurs survenues dans une application ne peuvent pas affecter d'autres applications. Comme le code de type sécurisé ne risque pas de provoquer d'erreurs dans la mémoire, l'utilisation de domaines d'application permet d'empêcher le code en cours d'exécution dans un domaine d'affecter d'autres applications dans le processus.  
  
-   Des applications individuelles peuvent être arrêtées sans que le processus entier soit arrêté. L'utilisation des domaines d'application vous permet de décharger le code en cours d'exécution dans une seule application.  
  
    > [!NOTE]
    >  Vous ne pouvez pas décharger des assemblys ou des types individuels. Seul un domaine complet peut être déchargé.  
  
-   Le code en cours d'exécution dans une application ne peut pas directement accéder au code ou aux ressources d'une autre application. Le Common Language Runtime applique cette isolation en empêchant les appels directs entre les objets dans les différents domaines d'application. Les objets qui passent d'un domaine à un autre sont soit copiés, soit accédés par un proxy. Si l'objet est copié, l'appel à cet objet est alors local. Dans ce cas, l'appelant et l'objet référencé figurent dans le même domaine d'application. Si l'objet est accédé par un proxy, l'appel à cet objet est alors distant. Dans ce cas, l'appelant et l'objet référencé figurent dans des domaines d'application différents. Les appels interdomaines utilisent la même infrastructure d'appel distant que les appels entre deux processus ou deux ordinateurs. Les métadonnées de l'objet référencé doivent par conséquent être disponibles pour les deux domaines d'application pour que l'appel de méthode puisse faire l'objet d'une compilation JIT correcte. Si le domaine appelant n’a pas accès aux métadonnées pour l’objet qui est appelé, la compilation peut échouer avec une exception de type **System.IO.FileNotFound**. Pour plus d’informations, consultez [Objets distants](http://msdn.microsoft.com/library/515686e6-0a8d-42f7-8188-73abede57c58). Le mécanisme permettant de déterminer le mode d'accès des objets sur les domaines est défini par l'objet. Pour plus d'informations, consultez <xref:System.MarshalByRefObject?displayProperty=nameWithType>.  
  
-   La portée du comportement de code est définie par l'application dans laquelle il s'exécute. En d'autres termes, le domaine d'application fournit des paramètres de configuration tels que les stratégies de version d'application, l'emplacement des assemblys distants auxquels il accède et des informations sur l'emplacement où se trouvent les assemblys qui sont chargés dans le domaine.  
  
-   Les autorisations accordées au code peuvent être contrôlées par le domaine d'application dans lequel le code s'exécute.  
  
  
## <a name="application-domains-and-assemblies"></a>Domaines d'application et assemblys  
 Cette rubrique décrit la relation entre les domaines d'application et les assemblys. Vous devez charger un assembly dans un domaine d'application avant de pouvoir exécuter le code qu'il contient. L'exécution d'une application standard entraîne le chargement de plusieurs assemblys dans un domaine d'application.  
  
 La façon dont un assembly est chargé détermine si son code compilé juste-à-temps (JIT) peut être partagé par plusieurs domaines d'application dans le processus, et si l'assembly peut être déchargé du processus.  
  
-   Si un assembly est chargé comme indépendant du domaine, tous les domaines d'application qui partagent le même jeu d'autorisations de sécurité peuvent partager le même code compilé juste-à-temps, ce qui réduit la mémoire requise par l'application. Toutefois, l'assembly ne peut jamais être déchargé du processus.  
  
-   Si un assembly n'est pas chargé comme indépendant du domaine, il doit être compilé juste-à-temps dans chaque domaine d'application dans lequel il est chargé. Toutefois, l'assembly peut être déchargé du processus via le déchargement de tous les domaines d'application dans lesquels il est chargé.  
  
 L'hôte de runtime détermine s'il convient de charger des assemblys comme indépendants du domaine lorsqu'il charge le runtime dans un processus. Pour les applications managées, appliquez l'attribut <xref:System.LoaderOptimizationAttribute> à la méthode de point d'entrée pour le processus et spécifiez une valeur de l'énumération <xref:System.LoaderOptimization> associée. Pour les applications non managées qui hébergent le Common Language Runtime, spécifiez l’indicateur approprié quand vous appelez la méthode [Fonction CorBindToRuntimeEx](../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md).  
  
 Il existe trois options de chargement des assemblys indépendants du domaine :  
  
-   <xref:System.LoaderOptimization> ne charge aucun assembly comme indépendant du domaine, sauf Mscorlib, qui est toujours chargé comme indépendant du domaine. Ce paramètre est désigné par « domaine unique », car il est fréquemment utilisé lorsque l'hôte n'exécute qu'une seule application dans le processus.  
  
-   <xref:System.LoaderOptimization> charge tous les assemblys comme indépendants du domaine. Utilisez ce paramètre lorsque plusieurs domaines d'application figurent dans le processus et qu'ils exécutent tous le même code.  
  
-   <xref:System.LoaderOptimization> charge les assemblys avec nom fort comme indépendants du domaine s'ils ont été installés, ainsi que toutes leurs dépendances, dans le Global Assembly Cache. Les autres assemblys sont chargés et compilés juste-à-temps séparément pour chaque domaine d'application dans lequel ils sont chargés, et peuvent donc être déchargés du processus. Utilisez ce paramètre lors de l'exécution de plusieurs applications dans le même processus, ou si vous disposez d'un mélange d'assemblys partagés par de nombreux domaines d'application et d'assemblys qui doivent être déchargés du processus.  
  
 Le code compilé juste-à-temps ne peut pas être partagé pour les assemblys chargés dans le contexte de chargement, à l'aide de la méthode <xref:System.Reflection.Assembly.LoadFrom%2A> de la classe <xref:System.Reflection.Assembly>, ou chargés à partir d'images à l'aide de surcharges de la méthode <xref:System.Reflection.Assembly.Load%2A> qui spécifient des tableaux d'octets.  
  
 Les assemblys, compilés en code natif à l’aide de [Ngen.exe (le générateur d’images natives)](../../../docs/framework/tools/ngen-exe-native-image-generator.md), peuvent être partagés entre des domaines d’application s’ils sont chargés comme indépendants du domaine lors de leur premier chargement dans un processus.  
  
 Le code compilé juste-à-temps pour l'assembly contenant le point d'entrée de l'application est partagé uniquement si toutes ses dépendances peuvent être partagées.  
  
 Un assembly indépendant du domaine peut être compilé juste-à-temps plusieurs fois. Par exemple, lorsque les jeux d'autorisations de sécurité de deux domaines d'application sont différents, ils ne peuvent pas partager le même code compilé juste-à-temps. Toutefois, chaque copie de l'assembly compilé juste-à-temps peut être partagée avec d'autres domaines d'application disposant du même jeu d'autorisations.  
  
 Lorsque vous décidez de charger des assemblys comme indépendants du domaine, vous devez trouver un compromis entre la réduction de l'utilisation de la mémoire et d'autres facteurs de performances.  
  
-   L'accès aux données et méthodes statiques est plus lent pour les assemblys indépendants du domaine en raison de la nécessité d'assurer l'isolation des assemblys. Chaque domaine d'application qui accède à l'assembly doit disposer d'une copie distincte des données statiques, afin d'éviter que des références à des objets dans les champs statiques ne franchissent les limites de domaine. Le runtime contient par conséquent une logique supplémentaire pour orienter un appelant vers la copie appropriée des données statiques ou de la méthode statique. Cette logique supplémentaire ralentit l'appel.  
  
-   Toutes les dépendances d'un assembly doivent être localisées et chargées lorsque l'assembly est chargé comme indépendant du domaine, car une dépendance qui ne peut pas être chargée comme indépendante du domaine empêche le chargement de l'assembly comme indépendant du domaine.  
  
## <a name="application-domains-and-threads"></a>Domaines d'application et threads  
 Un domaine d'application forme une limite d'isolation pour la sécurité, le suivi des versions, la fiabilité et le déchargement de code managé. Un thread constitue la construction du système d'exploitation utilisée par le Common Language Runtime pour exécuter le code. Au moment de l'exécution, l'ensemble du code managé est chargé dans un domaine d'application et exécuté par un ou plusieurs threads managés.  
  
 Il n'existe pas de corrélation un-à-un entre les domaines d'application et les threads. Plusieurs threads peuvent s'exécuter dans un seul domaine d'application à tout moment donné et un thread particulier n'est pas limité à un seul domaine d'application. En d'autres termes, les threads sont libres de franchir les limites de domaine d'application et un nouveau n'est pas créé pour chaque domaine d'application.  
  
 À tout moment donné, chaque thread s'exécute dans un domaine d'application. Aucun, un ou plusieurs threads peuvent s'exécuter dans n'importe quel domaine d'application donné. Le runtime assure le suivi des threads s'exécutant dans les domaines d'application. Vous pouvez rechercher le domaine dans lequel un thread s'exécute à tout moment en appelant la méthode <xref:System.Threading.Thread.GetDomain%2A?displayProperty=nameWithType>.  
  
### <a name="application-domains-and-cultures"></a>Domaines d'application et cultures  
 La culture, représentée par un objet <xref:System.Globalization.CultureInfo>, est associée aux threads. Vous pouvez obtenir la culture associée au thread en cours d'exécution à l'aide de la propriété <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType> et vous pouvez obtenir ou définir la culture associée au thread en cours d'exécution à l'aide de la propriété <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType>. Si la culture associée à un thread a été définie explicitement à l'aide de la propriété <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType>, elle continue d'être associée à ce thread lorsque le thread traverse les limites du domaine d'application. Sinon, la culture associée au thread à un moment donné est déterminée par la valeur de la propriété <xref:System.Globalization.CultureInfo.DefaultThreadCurrentCulture%2A?displayProperty=nameWithType> dans le domaine d'application dans lequel le thread s'exécute :  
  
-   Si la valeur de la propriété n'est pas `null`, la culture retournée par la propriété est associée au thread (et, par conséquent, retournée par les propriétés <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType> et <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType>).  
  
-   Si la valeur de la propriété est `null`, la culture système en cours est associée au thread.  
  
## <a name="programming-with-application-domains"></a>Programmation avec des domaines d'application  
 Les domaines d'application sont généralement créés et manipulés par programme par des hôtes de runtime. Toutefois, un programme d'application peut parfois souhaiter travailler également avec des domaines d'application. Par exemple, un programme d'application pourrait charger un composant d'application dans un domaine pour pouvoir décharger le domaine (et le composant) sans devoir arrêter l'application entière.  
  
 La classe <xref:System.AppDomain> est l’interface de programmation des domaines d’application. Cette classe inclut des méthodes permettant de créer et de décharger des domaines, de créer des instances de types dans des domaines et de s'inscrire pour différentes notifications telles que le déchargement du domaine d'application. Le tableau suivant répertorie les méthodes <xref:System.AppDomain> fréquemment utilisées.  
  
|Méthode AppDomain|Description|  
|----------------------|-----------------|  
|<xref:System.AppDomain.CreateDomain%2A>|Crée un nouveau domaine d'application. Il est recommandé d'utiliser une surcharge de cette méthode qui spécifie un objet <xref:System.AppDomainSetup>. C'est la manière recommandée pour définir les propriétés d'un nouveau domaine, à savoir la base de l'application ou le répertoire racine pour l'application, l'emplacement du fichier de configuration pour le domaine et le chemin de recherche utilisé par le Common Language Runtime pour charger les assemblys dans le domaine.|  
|<xref:System.AppDomain.ExecuteAssembly%2A> et <xref:System.AppDomain.ExecuteAssemblyByName%2A>|Exécute un assembly dans le domaine d'application. Il s'agit d'une méthode d'instance, qui peut donc être utilisée pour exécuter du code dans un autre domaine d'application pour lequel vous avez une référence.|  
|<xref:System.AppDomain.CreateInstanceAndUnwrap%2A>|Crée une instance du type spécifié dans le domaine d'application, et retourne un proxy. Utilisez cette méthode pour éviter de charger l'assembly qui contient le type créé dans l'assembly appelant.|  
|<xref:System.AppDomain.Unload%2A>|Effectue un arrêt approprié du domaine. Le domaine d'application n'est pas déchargé tant que tous les threads en cours d'exécution dans le domaine ne sont pas arrêtés ou ne figurent plus dans le domaine.|  
  
> [!NOTE]
>  Le Common Language Runtime ne prend pas en charge la sérialisation de méthodes globales ; les délégués ne peuvent donc pas être utilisés pour exécuter des méthodes globales dans d'autres domaines d'application.  
  
 Les interfaces non managées décrites dans la spécification sur les interfaces d'hébergement du Common Language Runtime permettent également d'accéder aux domaines d'application. Les hôtes de runtime peuvent utiliser des interfaces à partir d'un code non managé pour créer des domaines d'application dans un processus et y accéder.  
  
## <a name="complusloaderoptimization-environment-variable"></a>COMPLUS_LoaderOptimization, variable d'environnement  
 Variable d'environnement qui définit la stratégie d'optimisation de chargeur par défaut d'une application exécutable.  
  
### <a name="syntax"></a>Syntaxe  
  
```  
COMPLUS_LoaderOptimization = 1  
```  
  
### <a name="remarks"></a>Notes  
 Une application typique charge plusieurs assemblys dans un domaine d'application avant que le code qu'ils contiennent ne puisse être exécuté.  
  
 La façon dont l'assembly est chargé détermine si son code compilé juste-à-temps (JIT) peut être partagé par plusieurs domaines d'application dans le processus.  
  
-   Si un assembly est chargé indépendamment du domaine, tous les domaines d'application qui partagent le même jeu d'autorisations de sécurité peuvent partager le même code compilé juste-à-temps. Cela réduit la quantité de mémoire requise par l'application.  
  
-   Si un assembly n'est pas chargé indépendamment du domaine, il doit être compilé juste-à-temps dans chaque domaine d'application dans lequel il est chargé et le chargeur ne doit pas partager de ressources internes entre les domaines d'application.  
  
 Lorsqu'il est défini avec la valeur 1, l'indicateur d'environnement COMPLUS_LoaderOptimization force l'hôte du runtime à charger tous les assemblys d'une manière dépendante du domaine, connue sous le nom de SingleDomain. SingleDomain ne charge aucun assembly comme indépendant du domaine, sauf Mscorlib, qui est toujours chargé comme indépendant du domaine. Ce paramètre est désigné par « domaine unique », car il est fréquemment utilisé lorsque l'hôte n'exécute qu'une seule application dans le processus.  
  
> [!CAUTION]
>  L'indicateur d'environnement COMPLUS_LoaderOptimization a été conçu pour être utilisé dans les scénarios de diagnostic et de test. L'activation de l'indicateur peut provoquer un net ralentissement et accroître l'utilisation de la mémoire.  
  
### <a name="code-example"></a>Exemple de code  
 Pour forcer tous les assemblys à ne pas se charger comme indépendants du domaine pour le service IISADMIN, ajoutez `COMPLUS_LoaderOptimization=1` à la chaîne de valeur multiple de l'environnement dans la clé HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\IISADMIN.  
  
```  
Key = HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\IISADMIN  
Name = Environment  
Type = REG_MULTI_SZ  
Value (to append) = COMPLUS_LoaderOptimization=1  
```  
  
<a name="reference"></a>   
## <a name="reference"></a>Référence  
 <xref:System.MarshalByRefObject?displayProperty=nameWithType>
