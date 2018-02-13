---
title: -delaysign (Options du compilateur C#)
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /delaysign
helpviewer_keywords:
- -delaysign compiler option [C#]
- delaysign compiler option [C#]
- /delaysign compiler option [C#]
ms.assetid: bcb058eb-2933-4e7f-b356-5c941db4de75
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: a931dccb2aebd2c898b55f0a007d9fac8da42f2e
ms.sourcegitcommit: dd6ea7f0e581ac84e0a90d9b23c463fcf1ec3ce7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2018
---
# <a name="-delaysign-c-compiler-options"></a>-delaysign (Options du compilateur C#)
Cette option fait en sorte que le compilateur réserve de l’espace dans le fichier de sortie afin qu’une signature numérique puisse être ajoutée ultérieurement.  
  
## <a name="syntax"></a>Syntaxe  
  
```console  
-delaysign[ + | - ]  
```  
  
## <a name="arguments"></a>Arguments  
 `+` &#124; `-`  
 Utilisez **-delaysign-** si vous souhaitez obtenir un assembly complètement signé. Utilisez **-delaysign+** si vous souhaitez uniquement placer la clé publique dans l’assembly. **-delaysign-** est l’option par défaut.  
  
## <a name="remarks"></a>Notes  
 L’option **-delaysign** est sans effet sauf si elle est utilisée avec [-keyfile](../../../csharp/language-reference/compiler-options/keyfile-compiler-option.md) ou [-keycontainer](../../../csharp/language-reference/compiler-options/keycontainer-compiler-option.md).  
  
 Quand vous demandez un assembly totalement signé, le compilateur hache le fichier qui contient le manifeste (métadonnées de l’assembly) et signe ce hachage avec la clé privée. La signature numérique obtenue est stockée dans le fichier qui contient le manifeste. Pour un assembly avec signature différée, le compilateur ne calcule pas, ni ne stocke la signature, mais réserve de l'espace dans le fichier pour que la signature puisse être ajoutée par la suite.  
  
 Par exemple, l’utilisation de **-delaysign+** permet à un testeur de placer l’assembly dans le cache global. Après un test, vous pouvez signer complètement l’assembly en plaçant la clé privée dans l’assembly à l’aide de l’utilitaire [Assembly Linker](../../../framework/tools/al-exe-assembly-linker.md).  
  
 Pour plus d’informations, consultez [Création et utilisation d’assemblys avec nom fort](../../../framework/app-domains/create-and-use-strong-named-assemblies.md) et [Différer la signature d’un assembly](../../../framework/app-domains/delay-sign-assembly.md).  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Pour définir cette option du compilateur dans l'environnement de développement Visual Studio  
  
1.  Ouvrez la page **Propriétés** du projet.  
  
2.  Modifiez la propriété **Différer la signature uniquement**.  
  
 Pour plus d’informations sur la façon de définir cette option du compilateur par programmation, consultez <xref:VSLangProj80.ProjectProperties3.DelaySign%2A>.  
  
## <a name="see-also"></a>Voir aussi  
 [Options du compilateur C#](../../../csharp/language-reference/compiler-options/index.md)  
 [Gestion des propriétés des projets et des solutions](/visualstudio/ide/managing-project-and-solution-properties)
