---
title: -linkresource (Options du compilateur C#)
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
f1_keywords: /linkresource
helpviewer_keywords:
- /linkresource compiler option [C#]
- linkres compiler option [C#]
- /linkres compiler option [C#]
- -linkres compiler option [C#]
- -linkresource compiler option [C#]
- linkresource compiler option [C#]
ms.assetid: 440c26c2-77c1-4811-a0a3-57cce3f5fc96
caps.latest.revision: "17"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 7da5a55fa96c11d79f8c616cf0f1f4e0ed109bfa
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="-linkresource-c-compiler-options"></a>-linkresource (Options du compilateur C#)
Crée un lien vers une ressource .NET Framework dans le fichier de sortie. Le fichier de ressources n’est pas ajouté au fichier de sortie. Cette option diffère de l’option [-resource](../../../csharp/language-reference/compiler-options/resource-compiler-option.md) qui incorpore un fichier de ressources dans le fichier de sortie.  
  
## <a name="syntax"></a>Syntaxe  
  
```console  
-linkresource:filename[,identifier[,accessibility-modifier]]  
```  
  
## <a name="arguments"></a>Arguments  
 `filename`  
 Fichier de ressources .NET Framework que vous voulez lier à l’assembly.  
  
 `identifier`(facultatif)  
 Nom logique de la ressource. Il s’agit du nom utilisé pour charger la ressource. La valeur par défaut est le nom du fichier.  
  
 `accessibility-modifier`(facultatif)  
 Accessibilité de la ressource : publique ou privée. La valeur par défaut est « public ».  
  
## <a name="remarks"></a>Notes  
 Par défaut, les ressources liées sont publiques dans l’assembly quand elles sont créées avec le compilateur C#. Pour rendre les ressources privées, spécifiez le modificateur d’accessibilité `private`. Aucun autre modificateur que `public` ou `private` n’est autorisé.  
  
 **-linkresource** nécessite une option [-target](../../../csharp/language-reference/compiler-options/target-compiler-option.md) autre que **-target:module**.  
  
 Si `filename` est un fichier de ressources .NET Framework créé, par exemple, par [Resgen.exe](../../../framework/tools/resgen-exe-resource-file-generator.md) ou dans l'environnement de développement, il est accessible à l'aide des membres de l'espace de noms <xref:System.Resources>. Pour plus d'informations, consultez <xref:System.Resources.ResourceManager?displayProperty=nameWithType>. Pour toutes les autres ressources, utilisez les méthodes `GetManifestResource` dans la classe <xref:System.Reflection.Assembly> pour accéder à la ressource au moment de l’exécution.  
  
 Le fichier spécifié dans `filename` peut avoir n’importe quel format. C’est le cas, par exemple, si vous voulez qu’une DLL native fasse partie de l'assembly pour qu’elle puisse être installée dans le Global Assembly Cache et accessible à partir du code managé dans l'assembly. Le deuxième des exemples suivants montre comment effectuer cette opération. Vous pouvez effectuer la même opération dans Assembly Linker. Le troisième des exemples suivants montre comment effectuer cette opération. Pour plus d’informations, consultez [Al.exe (Assembly Linker)](../../../framework/tools/al-exe-assembly-linker.md) et [Utilisation d’assemblys et du Global Assembly Cache](../../../framework/app-domains/working-with-assemblies-and-the-gac.md).  
  
 **-linkres** est la forme abrégée de **-linkresource**.  
  
 Cette option de compilateur n’est pas disponible dans Visual Studio et ne peut pas être changée par programmation.  
  
## <a name="example"></a>Exemple  
 Compiler `in.cs` et créer un lien vers le fichier de ressources `rf.resource` :  
  
```console  
csc -linkresource:rf.resource in.cs  
```  
  
## <a name="example"></a>Exemple  
 Compiler `A.cs` dans une DLL, créer un lien vers une DLL native N.dll et placer la sortie dans le Global Assembly Cache (GAC). Dans cet exemple, A.dll et N.dll résident dans le GAC.  
  
```console  
csc -linkresource:N.dll -t:library A.cs  
gacutil -i A.dll  
```  
  
## <a name="example"></a>Exemple  
 Cet exemple obtient le même résultat, mais en utilisant des options Assembly Linker.  
  
```console  
csc -t:module A.cs  
al -out:A.dll A.netmodule -link:N.dll   
gacutil -i A.dll  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Options du compilateur C#](../../../csharp/language-reference/compiler-options/index.md)  
 [Al.exe (Assembly Linker)](../../../framework/tools/al-exe-assembly-linker.md)  
 [Utilisation d’assemblys et du Global Assembly Cache](../../../framework/app-domains/working-with-assemblies-and-the-gac.md)  
 [Gestion des propriétés des projets et des solutions](/visualstudio/ide/managing-project-and-solution-properties)
