---
title: Peverify.exe (outil PEVerify)
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- portable executable files, PEVerify
- verifying MSIL and metadata
- PEVerify tool
- type safety requirements
- MSIL
- PEverify.exe
- PE files, PEVerify
ms.assetid: f4f46f9e-8d08-4e66-a94b-0c69c9b0bbfa
caps.latest.revision: "18"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 5acb6da7c68f899daa4144e897e9ec31fcfa868a
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="peverifyexe-peverify-tool"></a>Peverify.exe (outil PEVerify)
L’outil PEVerify Tool permet aux développeurs générant du langage MSIL (Microsoft Intermediate Language) (tels que des développeurs de moteurs de script, writers de compilateur, etc.) de déterminer si leur code MSIL et les métadonnées qui y sont associées répondent aux exigences de sécurité de type. Certains compilateurs génèrent du code de type sécurisé vérifié uniquement si vous évitez d'utiliser certaines constructions de langage. Si, en tant que développeur, vous utilisez ce type de compilateur, vous pouvez souhaiter vérifier que vous n'avez pas compromis la sécurité de type de votre code. Vous pouvez dans ce cas exécuter l'outil PEVerify Tool sur vos fichiers pour vérifier le langage MSIL et les métadonnées.  
  
 Cet outil est installé automatiquement avec Visual Studio. Pour exécuter l'outil, utilisez l'invite de commandes développeur (ou l'invite de commandes Visual Studio dans Windows 7). Pour plus d'informations, consultez [Invites de commandes](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 À l'invite de commandes, tapez le texte suivant :  
  
## <a name="syntax"></a>Syntaxe  
  
```  
peverify filename [options]  
```  
  
#### <a name="parameters"></a>Paramètres  
  
|Argument|Description|  
|--------------|-----------------|  
|*filename*|Fichier exécutable portable dont le langage MSIL et les métadonnées sont à vérifier.|  
  
|Option|Description|  
|------------|-----------------|  
|**/break=** *maxErrorCount*|Abandonne la vérification si le nombre d’erreurs atteint *maxErrorCount* erreurs.<br /><br /> Ce paramètre n'est pas pris en charge dans les versions 2.0 et ultérieures du .NET Framework.|  
|**/clock**|Calcule et indique la durée des vérifications suivantes, en millisecondes :<br /><br /> **MD Val. cycle**<br /> Cycle de validation des métadonnées<br /><br /> **MD Val. pure**<br /> Validation simple des métadonnées<br /><br /> **IL Ver. cycle**<br /> Cycle de vérification MSIL<br /><br /> **IL Ver pure**<br /> Vérification MSIL simple<br /><br /> Les temps **MD Val. cycle** et **IL Ver. cycle** incluent le temps qu’il faut pour effectuer les procédures de démarrage et d’arrêt nécessaires. Les temps **MD Val. pure** et **IL Ver pure** reflètent le temps qu’il faut pour effectuer la validation ou la vérification uniquement.|  
|**/help**|Affiche la syntaxe et les options de commande de l'outil.|  
|**/hresult**|Affiche les codes d'erreur au format hexadécimal.|  
|**/ignore=** *hex.code* [, *hex.code*]|Ignore les codes d'erreur spécifiés.|  
|**/ignore=@** *responseFile*|Ignore les codes d'erreur répertoriés dans le fichier réponse spécifié.|  
|**/il**|Procède aux contrôles de vérification de la sécurité de type MSIL pour les méthodes implémentées dans l’assembly spécifié par *filename*. L’outil retourne les descriptions détaillées de chaque problème rencontré, sauf si vous spécifiez l’option **/quiet**.|  
|**/md**|Procède aux contrôles de validation des métadonnées sur l’assembly spécifié par *filename*. Parcourt l’intégralité de la structure des métadonnées figurant dans le fichier et fait état de tous les problèmes de validation rencontrés.|  
|**/nologo**|Supprime l'affichage de version de produit et d'informations de copyright.|  
|**/nosymbols**|Dans le .NET Framework version 2.0, il supprime les numéros de ligne pour la compatibilité descendante.|  
|**/quiet**|Spécifie le mode silencieux ; supprime la sortie des états sur les problèmes de vérification. Peverify.exe continue à indiquer si le fichier est de type sécurisé, mais ne fait pas état d'informations sur les problèmes empêchant la vérification de la sécurité de type.|  
|`/transparent`|Vérifiez uniquement les méthodes transparentes.|  
|**/unique**|Ignore les codes d'erreur récurrents.|  
|**/verbose**|Dans le .NET Framework version 2.0, il affiche des informations supplémentaires dans les messages de vérification MSIL.|  
|**/?**|Affiche la syntaxe et les options de commande de l'outil.|  
  
## <a name="remarks"></a>Notes  
 Le Common Language Runtime repose sur l'exécution de type sécurisé du code de l'application pour permettre de mettre en œuvre des mécanismes de sécurité et d'isolation. Le code qui n’est pas de [type sécurisé vérifié](http://msdn.microsoft.com/library/095cd1f6-d8db-4c0e-bce2-83ccb34dd5dc) ne peut normalement pas être exécuté, même si vous pouvez définir une stratégie de sécurité permettant l’exécution d’un code de confiance, mais non vérifiable.  
  
 Si ni l’option **/md** ni l’option **/il** ne sont spécifiées, Peverify.exe effectue ces deux types de contrôles. Peverify.exe procède en premier lieu aux contrôles **/md**. En l’absence d’erreurs, il effectue ensuite les contrôles **/il**. Si vous spécifiez à la fois les contrôles **/md** et **/il**, les contrôles **/il** sont effectués, y compris en cas d’erreurs dans les métadonnées. En l’absence d’erreurs dans les métadonnées, **peverify** *filename* équivaut alors à **peverify** *filename* **/md** **/il**.  
  
 Peverify.exe effectue des contrôles de vérification MSIL complets en fonction de l'analyse des flux de données et d'une liste de plusieurs centaines de règles sur la validité des métadonnées. Pour plus d'informations sur les contrôles effectués par Peverify.exe, consultez « Metadata Validation Specification » et « MSIL Instruction Set Specification » dans le dossier « Tool Developer's Guide » du [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)].  
  
 Notez que le .NET Framework version 2.0 ou ultérieure prend en charge les valeurs de retour `byref` vérifiables spécifiées à l'aide des instructions MSIL suivantes : `dup`, `ldsflda`, `ldflda`, `ldelema`, `call` et `unbox`.  
  
## <a name="examples"></a>Exemples  
 La commande suivante procède aux contrôles de validation des métadonnées et aux contrôles de vérification de la sécurité de type MSIL pour les méthodes implémentées dans l'assembly `myAssembly.exe`.  
  
```  
peverify myAssembly.exe /md /il  
```  
  
 Une fois les contrôles ci‑dessus terminés, Peverify.exe affiche le message suivant.  
  
```  
All classes and methods in myAssembly.exe Verified  
```  
  
 La commande suivante procède aux contrôles de validation des métadonnées et aux contrôles de vérification de la sécurité de type MSIL pour les méthodes implémentées dans l'assembly `myAssembly.exe`. L'outil affiche le temps requis pour effectuer ces vérifications.  
  
```  
peverify myAssembly.exe /md /il /clock  
```  
  
 Une fois les contrôles ci‑dessus terminés, Peverify.exe affiche le message suivant.  
  
```  
All classes and methods in myAssembly.exe Verified  
Timing: Total run     320 msec  
        MD Val.cycle  40 msec  
        MD Val.pure   10 msec  
        IL Ver.cycle  270 msec  
        IL Ver.pure   230 msec  
```  
  
 La commande suivante procède aux contrôles de validation des métadonnées et aux contrôles de vérification de la sécurité de type MSIL pour les méthodes implémentées dans l'assembly `myAssembly.exe`. Toutefois, Peverify.exe s'arrête lorsqu'il atteint le nombre d'erreurs maximal de 100. L'outil ignore également les codes d'erreur spécifiés.  
  
```  
peverify myAssembly.exe /break=100 /ignore=0x12345678,0xABCD1234  
```  
  
 La commande suivante aboutit au même résultat que dans l'exemple précédent, mais elle spécifie les codes d'erreur à ignorer dans le fichier réponse `ignoreErrors.rsp`.  
  
```  
peverify myAssembly.exe /break=100 /ignore@ignoreErrors.rsp  
```  
  
 Le fichier réponse peut comporter une liste de codes d'erreur avec la virgule comme séparateur.  
  
```  
0x12345678, 0xABCD1234  
```  
  
 Le fichier réponse peut également être mis en forme avec un code d'erreur par ligne.  
  
```  
0x12345678  
0xABCD1234  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Outils](../../../docs/framework/tools/index.md)  
 [NIB : Écriture de code de type sécurisé vérifié](http://msdn.microsoft.com/library/d18f10ef-3b48-4f47-8726-96714021547b)  
 [Cohérence des types et sécurité](http://msdn.microsoft.com/library/095cd1f6-d8db-4c0e-bce2-83ccb34dd5dc)  
 [Invites de commandes](../../../docs/framework/tools/developer-command-prompt-for-vs.md)
