---
title: "-resource (Options du compilateur C#)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /resource
helpviewer_keywords:
- -resource compiler option [C#]
- /resource compiler option [C#]
- -res compiler option [C#]
- /res compiler option [C#]
- res compiler option [C#]
- resource compiler option [C#]
ms.assetid: 5212666e-98ab-47e4-a497-b5545ab15c7f
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: a305f98b09d390afbeba7b55ab44ff09abc74617
ms.sourcegitcommit: dd6ea7f0e581ac84e0a90d9b23c463fcf1ec3ce7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2018
---
# <a name="-resource-c-compiler-options"></a>-resource (Options du compilateur C#)
Incorpore la ressource spécifiée dans le fichier de sortie.  
  
## <a name="syntax"></a>Syntaxe  
  
```console  
-resource:filename[,identifier[,accessibility-modifier]]  
```  
  
## <a name="arguments"></a>Arguments  
 `filename`  
 Fichier de ressources .NET Framework que vous voulez incorporer dans le fichier de sortie.  
  
 `identifier`(facultatif)  
 Nom logique de la ressource. Il s’agit du nom utilisé pour charger la ressource. La valeur par défaut est le nom du fichier.  
  
 `accessibility-modifier`(facultatif)  
 Accessibilité de la ressource : publique ou privée. La valeur par défaut est « public ».  
  
## <a name="remarks"></a>Notes  
 Utilisez [-linkresource](../../../csharp/language-reference/compiler-options/linkresource-compiler-option.md) pour lier une ressource à un assembly sans ajouter le fichier de ressources au fichier de sortie.  
  
 Par défaut, les ressources sont publiques dans l’assembly quand elles sont créées à l’aide du compilateur C#. Pour rendre les ressources privées, spécifiez le modificateur d’accessibilité `private`. Aucune accessibilité autre `public` ou `private` n’est autorisée.  
  
 Si `filename` est un fichier de ressources .NET Framework créé, par exemple, par [Resgen.exe](../../../framework/tools/resgen-exe-resource-file-generator.md) ou dans l'environnement de développement, il est accessible à l'aide des membres de l'espace de noms <xref:System.Resources>. Pour plus d'informations, consultez <xref:System.Resources.ResourceManager?displayProperty=nameWithType>. Pour toutes les autres ressources, utilisez les méthodes `GetManifestResource` dans la classe <xref:System.Reflection.Assembly> pour accéder à la ressource au moment de l’exécution.  
  
 **-res** est la forme abrégée de **-resource**.  
  
 L’ordre des ressources dans le fichier de sortie est déterminé par l’ordre spécifié sur la ligne de commande.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Pour définir cette option du compilateur dans l'environnement de développement Visual Studio  
  
1.  Ajoutez un fichier de ressources à votre projet.  
  
2.  Sélectionnez le fichier que vous souhaitez incorporer dans l’**Explorateur de solutions**.  
  
3.  Sélectionnez **Action de génération** pour le fichier dans la fenêtre **Propriétés**.  
  
4.  Définissez **Action de génération**  sur **Ressource incorporée**.  
  
 Pour plus d'informations sur la façon de définir cette option du compilateur par programme, consultez <xref:VSLangProj80.FileProperties2.BuildAction%2A>.  
  
## <a name="example"></a>Exemple  
 Compilez `in.cs` et attachez le fichier de ressources `rf.resource` :  
  
```console  
csc -resource:rf.resource in.cs  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Options du compilateur C#](../../../csharp/language-reference/compiler-options/index.md)  
 [Gestion des propriétés des projets et des solutions](/visualstudio/ide/managing-project-and-solution-properties)
