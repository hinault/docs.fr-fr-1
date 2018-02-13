---
title: -lib (Options du compilateur C#)
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /lib
helpviewer_keywords:
- lib compiler option [C#]
- -lib compiler option [C#]
- /lib compiler option [C#]
ms.assetid: b0efcc88-e8aa-4df4-a00b-8bdef70b7673
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: b60c6028d4b3f72acc31fe6028f7f956e1037eb0
ms.sourcegitcommit: dd6ea7f0e581ac84e0a90d9b23c463fcf1ec3ce7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2018
---
# <a name="-lib-c-compiler-options"></a>-lib (Options du compilateur C#)
L’option **-lib** spécifie l’emplacement des assemblys référencés au moyen de l’option [-reference (Options du compilateur C#)](../../../csharp/language-reference/compiler-options/reference-compiler-option.md).  
  
## <a name="syntax"></a>Syntaxe  
  
```console  
-lib:dir1[,dir2]  
```  
  
## <a name="arguments"></a>Arguments  
 `dir1`  
 Un répertoire dans lequel le compilateur doit effectuer la recherche si un assembly référencé ne se trouve pas dans le répertoire de travail actuel (le répertoire à partir duquel vous appelez le compilateur) ou dans le répertoire système du common language runtime.  
  
 `dir2`  
 Un ou plusieurs répertoires supplémentaires où rechercher des références d’assembly. Séparez les noms des répertoires supplémentaires par une virgule, sans espace.  
  
## <a name="remarks"></a>Notes  
 Le compilateur recherche les références d’assembly qui ne sont pas complètes dans l’ordre suivant :  
  
1.  Répertoire de travail actuel. Il s’agit du répertoire à partir duquel le compilateur est appelé.  
  
2.  Répertoire système du common language runtime.  
  
3.  Répertoires spécifiés par **-lib**.  
  
4.  Répertoires spécifiés par la variable d’environnement LIB.  
  
 Utilisez **-reference** pour spécifier une référence d’assembly.  
  
 **-lib** est additif. Si vous le spécifiez plusieurs fois, il effectue un ajout aux valeurs précédentes.  
  
 Au lieu d’utiliser **-lib**, vous pouvez copier dans le répertoire de travail les assemblys nécessaires. De cette façon, vous passez simplement le nom de l’assembly à **-reference**. Vous pouvez ensuite supprimer les assemblys du répertoire de travail. Comme le chemin de l’assembly dépendant n’est pas spécifié dans le manifeste de l’assembly, l’application peut être démarrée sur l’ordinateur cible, et recherche et utilise l’assembly dans le Global Assembly Cache.  
  
 Le fait que le compilateur puisse référencer l’assembly n’implique pas que le common language runtime soit en mesure de rechercher et charger l’assembly au moment de l’exécution. Consultez [Méthode de localisation des assemblys par le runtime](../../../framework/deployment/how-the-runtime-locates-assemblies.md) pour plus d’informations sur la façon dont le runtime recherche des assemblys référencés.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Pour définir cette option du compilateur dans l'environnement de développement Visual Studio  
  
1.  Ouvrez la boîte de dialogue **Pages de propriété** du projet.  
  
2.  Cliquez sur la page de propriétés **Chemin aux références**.  
  
3.  Modifiez le contenu de la zone de liste.  
  
 Pour plus d’informations sur la définition de cette option du compilateur par programmation, consultez <xref:VSLangProj80.ProjectProperties3.ReferencePath%2A>.  
  
## <a name="example"></a>Exemple  
 Compilez t2.cs pour créer un fichier .exe. Le compilateur recherche les références d’assembly dans le répertoire de travail et dans le répertoire racine du lecteur C.  
  
```console  
csc -lib:c:\ -reference:t2.dll t2.cs  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Options du compilateur C#](../../../csharp/language-reference/compiler-options/index.md)  
 [Gestion des propriétés des projets et des solutions](/visualstudio/ide/managing-project-and-solution-properties)
