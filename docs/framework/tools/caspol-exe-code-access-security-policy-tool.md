---
title: "Caspol.exe (outil Stratégie de sécurité d'accès du code)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permission sets, modifying security policy
- security policy [.NET Framework], Code Access Security Policy tool
- enterprise security policy
- referencing code groups and permission sets
- user security policy
- Caspol.exe
- Code Access Security Policy tool
- code groups, modifying security policy
- application development [.NET Framework], security
- machine security policy
- security policy [.NET Framework], modifying
- manually editing security configuration files
ms.assetid: d2bf6123-7b0c-4e60-87ad-a39a1c3eb2e0
caps.latest.revision: "44"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 6ab363e833ecde86a17d9adea3fcd26351725868
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="caspolexe-code-access-security-policy-tool"></a>Caspol.exe (outil Stratégie de sécurité d'accès du code)
L'outil Stratégie de sécurité d'accès du code (CAS) (Caspol.exe) permet aux utilisateurs et aux administrateurs de modifier la stratégie de sécurité au niveau de l'ordinateur, de l'utilisateur et de l'entreprise.  
  
> [!IMPORTANT]
>  À compter de [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], Caspol.exe n'affecte pas la stratégie CAS, sauf si l'[\<élément <legacyCasPolicy>](../../../docs/framework/configure-apps/file-schema/runtime/netfx40-legacysecuritypolicy-element.md) est défini sur `true`. Tous les paramètres affichés ou modifiés par CasPol.exe affectent uniquement les applications qui choisissent d'utiliser la stratégie CAS. Pour plus d’informations, consultez [Changements en matière de sécurité](../../../docs/framework/security/security-changes.md).  
  
> [!NOTE]
>  Les ordinateurs 64 bits comprennent des versions 64 bits et 32 bits de stratégie de sécurité. Pour garantir que vos modifications de stratégie s'appliquent aux applications 32 bits et 64 bits, exécutez les versions 32 bits et 64 bits de Caspol.exe.  
  
 Cet outil est automatiquement installé avec le .NET Framework et Visual Studio. Vous trouverez Caspol.exe dans le répertoire %windir%\Microsoft.NET\Framework\\*version* sur les systèmes 32 bits ou %windir%\Microsoft.NET\Framework64\\*version* sur les systèmes 64 bits. (Par exemple, l'emplacement est %windir%\Microsoft.NET\Framework64\v4.030319\caspol.exe pour .NET Framework 4 sur un système 64 bits.) Si l'ordinateur exécute plusieurs versions du .NET Framework côte-à-côte, plusieurs versions de l'outil peuvent être installées. Vous pouvez exécuter l'outil depuis le répertoire d'installation. Toutefois, nous vous recommandons d'utiliser les [Invites de commandes](../../../docs/framework/tools/developer-command-prompt-for-vs.md), qui vous évitent de devoir accéder au dossier d’installation.  
  
 À l'invite de commandes, tapez le texte suivant :  
  
## <a name="syntax"></a>Syntaxe  
  
```  
caspol [options]  
```  
  
#### <a name="parameters"></a>Paramètres  
  
|Option|Description|  
|------------|-----------------|  
|**-addfulltrust** *assembly_file*<br /><br /> ou<br /><br /> **-af** *assembly_file*|Ajoute un assembly qui implémente un objet de sécurité personnalisé (autorisation personnalisée ou condition d'appartenance personnalisée) à la liste des assemblys de confiance pour un niveau de stratégie précis. L’argument *assembly_file* spécifie l’assembly à ajouter. Ce fichier doit être signé avec un [nom fort](../../../docs/framework/app-domains/strong-named-assemblies.md). Vous pouvez signer un assembly avec un nom fort à l'aide de l’[outil Strong Name (Sn.exe)](../../../docs/framework/tools/sn-exe-strong-name-tool.md).<br /><br /> Lorsqu'un jeu d'autorisations contenant une autorisation personnalisée est ajouté à la stratégie, l'assembly implémentant cette autorisation personnalisée doit être ajouté à la liste des assemblys de confiance totale pour le niveau de stratégie considéré. Les assemblys qui implémentent des objets de sécurité personnalisés (groupes de codes ou conditions d'appartenance personnalisés) et utilisés dans une stratégie de sécurité (stratégie de l'ordinateur notamment) doivent toujours être ajoutés à la liste des assemblys de confiance totale. **Attention :** Si l'assembly qui implémente l'objet de sécurité personnalisé référence d'autres assemblys, vous devez d'abord ajouter les assemblys référencés à la liste des assemblys de confiance totale. Les objets de sécurité personnalisés créés à l'aide de Visual Basic, C++ et JScript référencent Microsoft.VisualBasic.dll, Microsoft.VisualC.dll ou Microsoft.JScript.dll, respectivement. Ces assemblys ne sont pas par défaut dans la liste des assemblys de confiance totale. Vous devez ajouter l'assembly approprié à la liste de confiance totale avant d'ajouter un objet de sécurité personnalisé. Dans le cas contraire, vous risquez de perturber le système de sécurité et de provoquer l'échec du chargement de tous les assemblys. Dans ce cas, l'option **-all -reset** de Caspol.exe ne répare pas la sécurité. Pour corriger la sécurité, vous devez manuellement modifier les fichiers de sécurité pour supprimer l'objet de sécurité personnalisé.|  
|**-addgroup** {*parent_label &#124; parent_name*} *mship pset_name* [*flags*]<br /><br /> ou<br /><br /> **-ag** {*parent_label &#124; parent_name*} *mship pset_name* [*flags*]|Ajoute un nouveau groupe de codes à la hiérarchie des groupes de codes. Vous pouvez spécifier l'argument *parent_label* ou *parent_name*. L'argument *parent_label* indique l'étiquette (par ex., 1. ou 1.1.) du groupe de codes parent du groupe de codes ajouté. L'argument *parent_name* indique le nom du groupe de codes parent du groupe de codes ajouté. Comme *parent_label* et *parent_name* peuvent être utilisés indifféremment, Caspol.exe doit être capable de faire la distinction entre les deux. Par conséquent, *parent_name* ne peut pas commencer par un chiffre. Par ailleurs, *parent_name* ne peut contenir que les lettres de A à Z, les chiffres de 0 à 9 et le caractère de soulignement.<br /><br /> L'argument *mship* spécifie la condition d'appartenance au nouveau groupe de codes. Pour plus d’informations, consultez le tableau des arguments *mship*, plus loin dans cette section.<br /><br /> L’argument *pset_name* est le nom du jeu d’autorisations associé au nouveau groupe de codes. Vous pouvez également définir un ou plusieurs *flags* pour le nouveau groupe. Pour plus d’informations, consultez le tableau des arguments *flags*, plus loin dans cette section.|  
|**-addpset** {*psfile* &#124; *psfile* p*set_name*}<br /><br /> ou<br /><br /> **-ap** {*named*_*psfile* &#124; *psfile* *pset_name*}|Ajoute un nouveau jeu d'autorisations nommé à la stratégie. Ce jeu d'autorisations doit être créé au format XML et stocké dans un fichier .xml. Si le fichier XML contient le nom du jeu d'autorisations, seul ce fichier (*psfile*) est spécifié. Si le fichier XML ne contient pas le nom du jeu d'autorisations, vous devez spécifier à la fois le nom du fichier XML (*psfile*) et le nom du jeu d'autorisations (*pset_name*).<br /><br /> Notez que toutes les autorisations utilisées dans un jeu d'autorisations doivent être définies dans les assemblys contenus dans le Global Assembly Cache.|  
|**-a**[**ll**]|Indique que toutes les options qui suivent celle-ci s'appliquent aux stratégies de l'ordinateur, de l'utilisateur et de l'entreprise. L'option **-all** fait toujours référence à la stratégie de l'utilisateur actuellement connecté. Pour faire référence à la stratégie d'un autre utilisateur que l'utilisateur actuel, utilisez l'option **-customall**.|  
|**-chggroup** {*label &#124;name*} {*mship* &#124; *pset_name* &#124;<br /><br /> *flags* `}`<br /><br /> ou<br /><br /> **-cg** {*label &#124;name*} {*mship* &#124; *pset_name* &#124;<br /><br /> *flags* `}`|Change la condition d'appartenance ou le jeu d'autorisations d'un groupe de codes ou change les paramètres des indicateurs **exclusive**, **levelfinal**, **name** et **description**. Vous pouvez spécifier l'argument *label* ou l'argument *name*. L'argument *label* indique l'étiquette (par ex., 1. ou 1.1.) du groupe de codes. L'argument *name* indique le nom du groupe de codes à modifier. Comme *label* et *name* peuvent être utilisés indifféremment, Caspol.exe doit être capable de faire la distinction entre les deux. Par conséquent, *name* ne peut pas commencer par un chiffre. Par ailleurs, *name* ne peut contenir que les lettres de A à Z, les chiffres de 0 à 9 et le caractère de soulignement.<br /><br /> L’argument *pset_name* indique le nom du jeu d’autorisations à associer au groupe de codes. Consultez les tableaux fournis plus loin dans cette section pour plus d’informations sur les arguments *mship* et *flags*.|  
|**-chgpset**  *psfile pset_name*<br /><br /> ou<br /><br /> **-cp** *psfile pset_name*|Change le jeu d'autorisations nommé. L’argument *psfile* fournit la nouvelle définition du jeu d’autorisations ; il s’agit d’un fichier de jeu d’autorisations sérialisé au format XML. L’argument *pset_name* spécifie le nom du jeu d’autorisations que vous souhaitez remplacer.|  
|**-customall**  *path*<br /><br /> ou<br /><br /> **-ca**  *path*|Indique que toutes les options qui suivent celle-ci s'appliquent aux stratégies de l'ordinateur, de l'entreprise et de l'utilisateur personnalisé spécifié. Vous devez spécifier l’emplacement du fichier de configuration de sécurité associé à l’utilisateur personnalisé dans l’argument *path*.|  
|**-cu**[**stomuser**] *path*|Permet d'administrer une stratégie d'utilisateur personnalisée qui n'appartient pas à l'utilisateur pour lequel Caspol.exe s'exécute. Vous devez spécifier l’emplacement du fichier de configuration de sécurité associé à l’utilisateur personnalisé dans l’argument *path*.|  
|**-enterprise**<br /><br /> ou<br /><br /> **-en**|Indique que toutes les options qui suivent celle-ci s'appliquent à la stratégie de niveau entreprise. Les utilisateurs qui ne sont pas des administrateurs de l'entreprise ne bénéficient pas d'autorisations suffisantes pour modifier la stratégie de l'entreprise, même s'ils peuvent l'afficher. Dans les scénarios qui ne se situent pas au niveau de l'entreprise, cette stratégie n'a, par défaut, aucune incidence sur les stratégies de niveau ordinateur et utilisateur.|  
|**-e**[**xecution**] {**on** &#124; **off**}|Active ou désactive le mécanisme qui vérifie l'autorisation à mettre en œuvre avant que le code ne commence à s'exécuter. **Remarque :** Ce commutateur est supprimé du [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] et des versions ultérieures. Pour plus d’informations, consultez [Changements en matière de sécurité](../../../docs/framework/security/security-changes.md).|  
|**-f**[**orce**]|Supprime le test d'autodestruction de l'outil et modifie la stratégie selon les instructions de l'utilisateur. Normalement, Caspol.exe vérifie si les changements de stratégie sont susceptibles de nuire à son exécution correcte. Le cas échéant, Caspol.exe n'enregistre pas la modification et imprime un message d'erreur. Pour obliger Caspol.exe à modifier la stratégie même si cela l'empêche de s'exécuter, utilisez l'option **–force**.|  
|**-h**[**elp**]|Affiche la syntaxe de commande et les options de Caspol.exe.|  
|**-l**[**ist**]|Affiche la hiérarchie des groupes de codes et les jeux d'autorisations définis pour l'ordinateur, l'utilisateur ou l'entreprise spécifiés ou pour tous les niveaux de stratégie. Caspol.exe affiche d'abord l'étiquette du groupe de codes, puis son nom s'il n'est pas nul.|  
|**-listdescription**<br /><br /> ou<br /><br /> **-ld**|Affiche les descriptions de tous les groupes de codes définis pour le niveau de stratégie spécifié.|  
|**-listfulltrust**<br /><br /> ou<br /><br /> **-lf**|Affiche le contenu de la liste des assemblys de confiance totale pour le niveau de stratégie spécifié.|  
|**-listgroups**<br /><br /> ou<br /><br /> **-lg**|Affiche les groupes de codes du niveau de stratégie spécifié ou de tous les niveaux de stratégie. Caspol.exe affiche d'abord l'étiquette du groupe de codes, puis son nom s'il n'est pas nul.|  
|**-listpset** ou **-lp**|Affiche les jeux d'autorisations associés au niveau de stratégie spécifié ou à tous les niveaux de stratégie.|  
|**-m**[**achine**]|Indique que toutes les options qui suivent celle-ci s'appliquent à la stratégie de niveau ordinateur. Les utilisateurs qui ne sont pas des administrateurs ne bénéficient pas d'autorisations suffisantes pour modifier la stratégie de l'ordinateur, même s'ils peuvent l'afficher. Pour les administrateurs, **-machine** est l'option par défaut.|  
|**-polchgprompt** {**on** &#124; **off**}<br /><br /> ou<br /><br /> **-pp** {**on** &#124; **off**}|Active ou désactive l'invite de commandes qui s'affiche lorsque Caspol.exe est exécuté avec une option susceptible d'entraîner des changements de stratégie.|  
|**-quiet**<br /><br /> ou<br /><br /> **-q**|Désactive temporairement l'invite normalement affichée pour une option entraînant des changements de stratégie. Le paramètre de l'invite de modification globale ne change pas. Utilisez l'option pour une seule commande à la fois afin d'éviter de désactiver l'invite pour toutes les commandes Caspol.exe.|  
|**-r**[**ecover**]|Restaure une stratégie à partir d'un fichier de sauvegarde. Dès qu'une stratégie est modifiée, Caspol.exe stocke l'ancienne stratégie dans un fichier de sauvegarde.|  
|**-remfulltrust** *assembly_file*<br /><br /> ou<br /><br /> **-rf**  *assembly_file*|Supprime un assembly de la liste des assemblys de confiance totale associée à un niveau de stratégie donné. Cette opération s'impose lorsqu'un jeu d'autorisations contenant une autorisation personnalisée n'est plus utilisé par la stratégie. Toutefois, vous ne devez supprimer un assembly qui implémente une autorisation personnalisée de la liste des assemblys de confiance totale que si cet assembly n'implémente aucune autre autorisation personnalisée en cours d'utilisation. Lorsque vous supprimez un assembly de la liste, vous devez également supprimer les assemblys dont il dépend.|  
|**-remgroup** {*label &#124;name*}<br /><br /> ou<br /><br /> **-rg** {l*abel &#124; name*}|Supprime le groupe de codes spécifié par son étiquette ou son nom. Si le groupe de codes spécifié comprend des groupes de codes enfants, Caspol.exe supprime également ces groupes enfants.|  
|**-rempset** *pset_name*<br /><br /> ou<br /><br /> **-rp** *pset_name*|Supprime de la stratégie le jeu d'autorisations spécifié. L'argument *pset_name* indique le jeu d'autorisations à supprimer. Caspol.exe ne supprime le jeu d'autorisations que s'il n'est pas associé à un groupe de codes. Il n'est pas possible de supprimer les jeux d'autorisations par défaut (intégrés).|  
|**-reset**<br /><br /> ou<br /><br /> **-rs**|Retourne l'état par défaut de la stratégie et l'enregistre sur le disque. Cette option est utile lorsqu'une stratégie modifiée semble irréparable et que vous souhaitez recommencer avec les paramètres d'installation par défaut. Il peut également être commode de procéder à une réinitialisation pour utiliser la stratégie par défaut comme point de départ et apporter ensuite des modifications à des fichiers de configuration de sécurité spécifiques. Pour plus d'informations, consultez [Modification manuelle des fichiers de configuration de sécurité](#cpgrfcodeaccesssecuritypolicyutilitycaspolexeanchor1).|  
|**-resetlockdown**<br /><br /> ou<br /><br /> **-rsld**|Retourne la version plus restrictive de l'état par défaut de la stratégie et l'enregistre sur le disque ; crée une sauvegarde de la stratégie antérieure de l'ordinateur et l'enregistre sur un fichier `security.config.bac`.  La stratégie verrouillée est similaire à la stratégie par défaut, mais elle n'accorde aucune autorisation pour coder à partir des zones `Local Intranet`, `Trusted Sites` et `Internet` et les groupes de codes correspondants n'ont pas de groupes de codes enfants.|  
|**-resolvegroup** *assembly_file*<br /><br /> ou<br /><br /> **-rsg**  *assembly_file*|Affiche les groupes de codes auxquels appartient un assembly particulier (*assembly_file*). Par défaut, cette option affiche la stratégie de niveau ordinateur, utilisateur et entreprise auxquels appartient l'assembly. Pour afficher un seul niveau de stratégie, utilisez cette option avec l'option **-machine**, **-user** ou **-enterprise**.|  
|**-resolveperm** *assembly_file*<br /><br /> ou<br /><br /> **-rsp** *assembly_file*|Affiche toutes les autorisations que le niveau de stratégie de sécurité spécifié (ou par défaut) accorderait à l'assembly si ce dernier avait la possibilité de s'exécuter. L’argument *assembly_file* spécifie l’assembly. Si vous spécifiez l'option **-all**, Caspol.exe calcule les autorisations de l'assembly sur la base de la stratégie de l'utilisateur, de l'ordinateur et de l'entreprise ; sinon, les règles de comportement par défaut s'appliquent.|  
|**-s**[**ecurity**] {**on** &#124; **off**}|Active ou désactive la sécurité d'accès du code. L'option **-s off** ne désactive pas la sécurité basée sur les rôles. **Remarque :** Ce commutateur est supprimé du [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] et des versions ultérieures. Pour plus d’informations, consultez [Changements en matière de sécurité](../../../docs/framework/security/security-changes.md). **Attention :** Quand la sécurité d'accès du code est désactivée, toutes les demandes d'accès au code aboutissent. La désactivation de la sécurité expose le système aux attaques de code nuisible tel que les virus et les vers. La désactivation de la sécurité permet d'améliorer les performances, mais ne doit être utilisée que lorsque d'autres mesures de sécurité ont été prises pour permettre de s'assurer que la sécurité globale du système ne sera pas compromise. Ces autres mesures de sécurité consistent notamment à déconnecter les réseaux publics, à sécuriser physiquement les ordinateurs, etc.|  
|**-u**[**ser**]|Indique que toutes les options qui suivent celle-ci s'appliquent à la stratégie de niveau utilisateur associée à l'utilisateur pour le compte duquel Caspol.exe est exécuté. Pour les utilisateurs qui ne sont pas des administrateurs, **-user** est l'option par défaut.|  
|**-?**|Affiche la syntaxe de commande et les options de Caspol.exe.|  
  
 L'argument *mship* qui spécifie la condition d'appartenance d’un groupe de codes peut être utilisé avec les options **-addgroup** et **-chggroup**. Chaque argument *mship* est implémenté comme classe .NET Framework. Pour spécifier *mship*, utilisez l’une des solutions suivantes.  
  
|Argument|Description|  
|--------------|-----------------|  
|**-allcode**|Spécifie l'ensemble du code. Pour plus d’informations sur cette condition d’appartenance, consultez <xref:System.Security.Policy.AllMembershipCondition>.|  
|**-appdir**|Spécifie le répertoire de l'application. Si vous spécifiez **–appdir** comme condition d'appartenance, la preuve fournie par l'URL du code est comparée à la preuve fournie par le répertoire d'application du même code. Si les deux preuves sont identiques, la condition d'appartenance est satisfaite. Pour plus d’informations sur cette condition d’appartenance, consultez <xref:System.Security.Policy.ApplicationDirectoryMembershipCondition>.|  
|**-custom**  *xmlfile*|Ajoute une condition d'appartenance personnalisée. L’argument obligatoire *xmlfile* spécifie le fichier .xml qui contient la sérialisation XML de la condition d’appartenance personnalisée.|  
|**-hash** *hashAlg* {**-hex** *hashValue* &#124; **-file** *assembly_file* }|Spécifie un code qui contient la valeur de hachage de l'assembly donné. Pour utiliser une valeur de hachage comme condition d'appartenance à un groupe de codes, vous devez spécifier la valeur de hachage ou le fichier d'assembly. Pour plus d’informations sur cette condition d’appartenance, consultez <xref:System.Security.Policy.HashMembershipCondition>.|  
|**-pub** { **-cert** *cert_file_name* &#124;<br /><br /> **-file** *signed_file_name* &#124; **-hex**  *hex_string* }|Spécifie un code qui présente l'éditeur de logiciel indiqué par un fichier de certificat, une signature sur un fichier ou la représentation hexadécimale d'un certificat X509. Pour plus d’informations sur cette condition d’appartenance, consultez <xref:System.Security.Policy.PublisherMembershipCondition>.|  
|**-site** *website*|Spécifie un code qui présente le site d'origine donné. Exemple :<br /><br /> **-site** www.proseware.com<br /><br /> Pour plus d’informations sur cette condition d’appartenance, consultez <xref:System.Security.Policy.SiteMembershipCondition>.|  
|**-strong -file** *file_name* {*name* &#124; **-noname**} {*version* &#124; **-noversion**}|Spécifie un code avec un nom fort spécifique désigné par son nom de fichier, le nom de l'assembly (chaîne) et la version de l'assembly au format *major*.*minor*.*build*.*revision*. Exemple :<br /><br /> **-strong -file** myAssembly.exe myAssembly 1.2.3.4<br /><br /> Pour plus d’informations sur cette condition d’appartenance, consultez <xref:System.Security.Policy.StrongNameMembershipCondition>.|  
|**-url** *URL*|Spécifie un code qui provient de l'URL donnée. L'URL doit contenir un protocole, tel que http:// ou ftp://. Par ailleurs, un caractère générique (\*) peut être utilisé pour spécifier plusieurs assemblys pour une même URL. **Remarque :** Parce qu'une URL peut être identifiée à l'aide de plusieurs noms, l'utilisation d'une URL comme condition d'appartenance n'est pas un moyen sûr d'établir l'identité du code. Lorsque cela est possible, utilisez une condition d'appartenance à nom fort, une condition d'appartenance d'un éditeur ou la condition d'appartenance de hachage. <br /><br /> Pour plus d’informations sur cette condition d’appartenance, consultez <xref:System.Security.Policy.UrlMembershipCondition>.|  
|**-zone** *zonename*|Spécifie un code qui présente la zone d'origine donnée. L'argument *zonename* peut avoir l'une des valeurs suivantes : **MyComputer**, **Intranet**, **Trusted**, **Internet** ou **Untrusted**. Pour plus d'informations sur cette condition d'appartenance, reportez-vous à la classe <xref:System.Security.Policy.ZoneMembershipCondition>.|  
  
 L’argument *flags* qui peut être utilisé avec les options **–addgroup** et **–chggroup** est spécifié de la façon suivante.  
  
|Argument|Description|  
|--------------|-----------------|  
|**-description "** *description* **"**|S’il est utilisé avec l'option **–addgroup**, spécifie la description d'un groupe de codes à ajouter. S’il est utilisé avec l'option **–chggroup**, spécifie la description d'un groupe de codes à modifier. L’argument *description* doit être entouré de guillemets doubles.|  
|**-exclusive** {**on**&#124;**off**}|Quand cette option est définie sur **on**, indique que seul le jeu d'autorisations associé au groupe de codes que vous ajoutez ou modifiez est pris en compte quand un code satisfait la condition d'appartenance du groupe de codes. Quand cette option est définie sur **off**, Caspol.exe tient compte des jeux d'autorisations de tous les groupes de codes correspondants du niveau de stratégie.|  
|**-levelfinal** {**on**&#124;**off**}|Quand cette option est définie sur **on**, cela indique qu’aucun des niveaux de stratégie inférieurs au niveau du groupe de codes ajouté ou modifié n'est pris en compte. Cette option est généralement utilisée au niveau de la stratégie de l'ordinateur. Par exemple, si vous définissez cet indicateur pour un groupe de codes au niveau de l'ordinateur et qu'il existe un code satisfaisant à la condition d'appartenance de ce groupe de codes, Caspol.exe ne calcule pas (ni n'applique) la stratégie de niveau utilisateur pour ce code.|  
|**-name "** *name* **"**|S’il est utilisé avec l'option **–addgroup**, spécifie le nom de script d'un groupe de codes à ajouter. S’il est utilisé avec l'option **–chggroup**, spécifie le nom de script d'un groupe de codes à modifier. L’argument *name* doit être entouré de guillemets doubles. L’argument *name* ne doit pas commencer par un chiffre et ne peut contenir que les lettres de A à Z, les chiffres de 0 à 9 et le caractère de soulignement. Vous pouvez faire référence aux groupes de codes par cet argument *name* au lieu d'utiliser leur étiquette numérique. L'argument *name* est également très utile dans les scripts.|  
  
## <a name="remarks"></a>Notes  
 La stratégie de sécurité se définit sur trois niveaux : ordinateur, utilisateur et entreprise. Le jeu d'autorisations dont bénéficie un assembly est déterminé par l'intersection entre les jeux d'autorisations accordés par ces trois niveaux de stratégie. Chaque niveau de stratégie est représenté par une structure hiérarchique de groupes de codes. Chaque groupe de codes possède une condition d'appartenance qui détermine quel code est membre de ce groupe. Un jeu d'autorisations nommé est également associé à chaque groupe de codes. Ce jeu d'autorisations spécifie les autorisations que peut accorder le runtime au code qui satisfait à la condition d'appartenance. Une hiérarchie de groupes de codes et les jeux d'autorisations nommés associés définissent et gèrent chaque niveau de la stratégie de sécurité. Vous pouvez utiliser les options **–user**, **-customuser**, **–machine** et **-enterprise** pour définir le niveau de stratégie de sécurité.  
  
 Pour plus d'informations sur les stratégies de sécurité et sur la manière dont le runtime détermine les autorisations à accorder au code, consultez [Gestion de la stratégie de sécurité](http://msdn.microsoft.com/library/d754e05d-29dc-4d3a-a2c2-95eaaf1b82b9).  
  
## <a name="referencing-code-groups-and-permission-sets"></a>Références aux groupes de codes et aux jeux d'autorisations  
 Pour faciliter les références aux groupes de codes d'une hiérarchie, l'option **-list** affiche une liste des groupes de codes avec des retraits et les étiquettes numériques correspondantes (1, 1.1, 1.1.1, etc.). Les autres opérations effectuées depuis la ligne de commande qui ciblent les groupes de codes utilisent également les étiquettes numériques pour faire référence à des groupes de codes particuliers.  
  
 Les jeux d'autorisations nommés sont référencés par leurs noms. L'option **–list** affiche la liste des groupes de codes suivie d'une liste des jeux d'autorisations nommés disponibles dans cette stratégie.  
  
## <a name="caspolexe-behavior"></a>Comportement de Caspol.exe  
 Toutes les options sauf **-s**[**ecurity**] {**on** &#124; **off**} utilisent la version du .NET Framework avec laquelle Caspol.exe a été installé. Si vous exécutez Caspol.exe installé avec la version *X* du runtime, les modifications s'appliquent uniquement à cette version. Les autres installations côte-à-côte du runtime, si elles existent, ne sont pas affectées. Si vous exécutez Caspol.exe à partir de la ligne de commande sans être dans un répertoire d’une version spécifique du runtime, l’outil est exécuté à partir du premier répertoire de version du runtime du chemin (généralement la version la plus récente du runtime installée).  
  
 L’option **-s**[**ecurity**] {**on** &#124; **off**} est une opération à l'échelle de l'ordinateur. La désactivation de la sécurité d'accès du code met fin aux contrôles de sécurité pour tout le code managé et tous les utilisateurs sur l'ordinateur. Si des versions côte-à-côte de .NET Framework sont installées, cette commande désactive la sécurité pour chaque version installée sur l'ordinateur. Bien que l'option **-list** indique que la sécurité est désactivée, rien d'autre ne l'indique clairement aux autres utilisateurs.  
  
 Quand un utilisateur sans droit d'administration exécute Caspol.exe, toutes les options concernent la stratégie de niveau utilisateur, sauf si l'option **–machine** est spécifiée. Quand un administrateur exécute Caspol.exe, toutes les options concernent la stratégie de niveau ordinateur, sauf si l'option **–user** est spécifiée.  
  
 Pour fonctionner, Caspol.exe doit bénéficier d'une autorisation équivalente à **Everything**. Cet outil est muni d'un mécanisme de protection qui interdit toute modification de stratégie susceptible d'empêcher l'octroi des autorisations indispensables à l'exécution de Caspol.exe. Si vous essayez d'effectuer de telles modifications, Caspol.exe vous envoie une notification indiquant que la modification de stratégie demandée détruit l'objet et qu'elle est par conséquent refusée. Vous pouvez désactiver ce mécanisme de protection pour une commande donnée à l'aide de l'option **–force**.  
  
<a name="cpgrfcodeaccesssecuritypolicyutilitycaspolexeanchor1"></a>   
## <a name="manually-editing-the-security-configuration-files"></a>Modification manuelle des fichiers de configuration de sécurité  
 Il existe trois fichiers de configuration de sécurité qui correspondent aux trois niveaux de sécurité pris en charge par Caspol.exe : ordinateur, utilisateur et entreprise. Ces fichiers sont créés uniquement sur le disque lorsque la stratégie de l'ordinateur, de l'utilisateur ou de l'entreprise est modifiée à l'aide de Caspol.exe. Vous pouvez utiliser l'option **–reset** de Caspol.exe pour enregistrer la stratégie de sécurité par défaut sur le disque, si nécessaire.  
  
 Dans la plupart des cas, il n'est pas recommandé de modifier manuellement les fichiers de configuration de sécurité. Il existe cependant des situations où ces modifications sont indispensables, par exemple lorsqu'un administrateur veut modifier la configuration de sécurité d'un utilisateur particulier.  
  
## <a name="examples"></a>Exemples  
 **-addfulltrust**  
  
 Supposez qu'un jeu d'autorisations contenant une autorisation personnalisée a été ajouté à la stratégie de l'ordinateur. Cette autorisation personnalisée est implémentée dans `MyPerm.exe`, et `MyPerm.exe` fait référence aux classes de `MyOther.exe`. Les deux assemblys doivent être ajoutés à la liste des assemblys de confiance totale. La commande suivante ajoute l'assembly `MyPerm.exe` à la liste des assemblys de confiance totale pour la stratégie de l'ordinateur.  
  
```  
caspol -machine -addfulltrust MyPerm.exe  
```  
  
 La commande suivante ajoute l'assembly `MyOther.exe` à la liste des assemblys de confiance totale pour la stratégie de l'ordinateur.  
  
```  
caspol -machine -addfulltrust MyOther.exe  
```  
  
 **-addgroup**  
  
 La commande suivante ajoute un groupe de codes enfant à la racine de la hiérarchie des groupes de codes de la stratégie de l'ordinateur. Le nouveau groupe de codes est membre de la zone **Internet** et il est associé au jeu d'autorisations **Execution**.  
  
```  
caspol -machine -addgroup 1.  -zone Internet Execution  
```  
  
 La commande suivante ajoute un groupe de codes enfant qui donne des autorisations sur l’intranet local au partage \\\netserver\netshare.  
  
```  
caspol -machine -addgroup 1. -url \\netserver\netshare\* LocalIntranet  
```  
  
 **-addpset**  
  
 La commande suivante ajoute le jeu d'autorisations `Mypset` à la stratégie de l'utilisateur.  
  
```  
caspol -user -addpset Mypset.xml Mypset  
```  
  
 **-chggroup**  
  
 La commande suivante change le jeu d'autorisations défini dans la stratégie d'utilisateur du groupe de codes étiqueté 1.2. en jeu d’autorisations **Execution**.  
  
```  
caspol -user -chggroup 1.2. Execution  
```  
  
 La commande suivante change la condition d'appartenance dans la stratégie par défaut du groupe de codes étiqueté 1.2.1. et change le paramètre de l’indicateur **exclusive**. La condition d'appartenance est définie comme un code qui provient de la zone **Internet** avec l'indicateur **exclusive** activé.  
  
```  
caspol -chggroup 1.2.1. -zone Internet -exclusive on  
```  
  
 **-chgpset**  
  
 La commande suivante substitue au jeu d'autorisations `Mypset` le jeu d'autorisations contenu dans `newpset.xml`. Notez que la version actuelle ne prend pas en charge la modification des jeux d’autorisations utilisés par la hiérarchie des groupes de codes.  
  
```  
caspol -chgpset Mypset newpset.xml  
```  
  
 **-force**  
  
 La commande suivante entraîne l'association du groupe de codes racine de la stratégie d'utilisateur (étiqueté 1) au jeu d'autorisations nommé **Nothing**. Cela empêche l'exécution de Caspol.exe.  
  
```  
caspol -force -user -chggroup 1 Nothing  
```  
  
 **-recover**  
  
 La commande suivante récupère la stratégie d'ordinateur enregistrée le plus récemment.  
  
```  
caspol -machine -recover  
```  
  
 **-remgroup**  
  
 La commande suivante supprime le groupe de codes étiqueté 1.1. Si ce groupe de codes comprend des groupes de codes enfants, ces derniers sont également supprimés.  
  
```  
caspol -remgroup 1.1.  
```  
  
 **-rempset**  
  
 La commande suivante supprime le jeu d'autorisations **Execution** de la stratégie d'utilisateur.  
  
```  
caspol -user -rempset Execution  
```  
  
 La commande suivante supprime `Mypset` du niveau de stratégie de l'utilisateur.  
  
```  
caspol -rempset MyPset  
```  
  
 **-resolvegroup**  
  
 La commande suivante affiche tous les groupes de codes de la stratégie d'ordinateur à laquelle appartient `myassembly`.  
  
```  
caspol -machine -resolvegroup myassembly  
```  
  
 La commande suivante affiche tous les groupes de codes de la stratégie d'ordinateur, d'entreprise et d'utilisateur personnalisé à laquelle appartient `myassembly`.  
  
```  
caspol -customall "c:\config_test\security.config" -resolvegroup myassembly  
```  
  
 **-resolveperm**  
  
 La commande suivante calcule les autorisations de `testassembly` en fonction des niveaux de stratégie d'ordinateur et d'utilisateur.  
  
```  
caspol -all -resolveperm testassembly  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Outils](../../../docs/framework/tools/index.md)  
 [Invites de commandes](../../../docs/framework/tools/developer-command-prompt-for-vs.md)
