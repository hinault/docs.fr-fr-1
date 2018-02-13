---
title: -win32res (Options du compilateur C#)
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
f1_keywords: /win32res
helpviewer_keywords:
- win32res compiler option
- /win32res compiler option [C#]
- -win32res compiler option [C#]
- win32res compiler option [C#]
ms.assetid: 3c33f750-6948-4c7e-a27e-bef98f77255b
caps.latest.revision: "16"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 4c24da8bb745847612d882d00eff7f03dbc60475
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="-win32res-c-compiler-options"></a>-win32res (Options du compilateur C#)
L’option **-win32res** insère une ressource Win32 dans le fichier de sortie.  
  
## <a name="syntax"></a>Syntaxe  
  
```console  
-win32res:filename  
```  
  
## <a name="arguments"></a>Arguments  
 `filename`  
 Fichier de ressources que vous voulez ajouter à votre fichier de sortie.  
  
## <a name="remarks"></a>Notes  
 Un fichier de ressources Win32 peut être créé avec le [compilateur de ressources](../../language-reference/compiler-options/resource-compiler-option.md). Le compilateur de ressources est appelé lorsque vous compilez un programme Visual C++ ; un fichier .res est alors créé à partir du fichier .rc.  
  
 Une ressource Win32 peut contenir des informations sur la version ou le fichier bitmap (icône) qui permettent d’identifier votre application dans l’Explorateur de fichiers. Si vous ne spécifiez pas l’option **-win32res**, le compilateur génère des informations de version en fonction de la version de l’assembly.  
  
 Consultez [-linkresource](../../../csharp/language-reference/compiler-options/linkresource-compiler-option.md) pour référencer ou [-resource](../../../csharp/language-reference/compiler-options/resource-compiler-option.md) pour attacher un fichier de ressources .NET Framework.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Pour définir cette option du compilateur dans l'environnement de développement Visual Studio  
  
1.  Ouvrez la page **Propriétés** du projet.  
  
2.  Cliquez sur la page de propriétés **Application**.  
  
3.  Cliquez sur le bouton **Fichier de ressources** et choisissez un fichier à l’aide de la zone de liste modifiable.  
  
## <a name="example"></a>Exemple  
 Compilez `in.cs` et attachez un fichier de ressources Win32 `rf.res` afin de générer le fichier `in.exe` :  
  
```console  
csc -win32res:rf.res in.cs  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Options du compilateur C#](../../../csharp/language-reference/compiler-options/index.md)  
 [Gestion des propriétés des projets et des solutions](/visualstudio/ide/managing-project-and-solution-properties)
