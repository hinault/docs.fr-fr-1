---
title: "-reference (Options du compilateur C#)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
f1_keywords: /reference
helpviewer_keywords:
- /r compiler option [C#]
- reference compiler option [C#]
- r compiler option [C#]
- /reference compiler option [C#]
- -r compiler option [C#]
- metadata import [C#]
- public type information [C#]
- -reference compiler option [C#]
ms.assetid: 8d13e5b0-abf6-4c46-bf71-2daf2cd0a6c4
caps.latest.revision: "28"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 60a00b1cd088a051e1a58d245c455b9678a74988
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="-reference-c-compiler-options"></a>-reference (Options du compilateur C#)
L’option **-reference** indique au compilateur d’importer des informations de type [public](../../../csharp/language-reference/keywords/public.md) dans le fichier spécifié du projet actuel, ce qui vous permet de référencer les métadonnées des fichiers d’assembly spécifiés.  
  
## <a name="syntax"></a>Syntaxe  
  
```console  
-reference:[alias=]filename  
-reference:filename  
```  
  
## <a name="arguments"></a>Arguments  
 `filename`  
 Nom d'un fichier comportant un manifeste d'assembly. Pour importer plusieurs fichiers, incluez une option **-reference** distincte pour chaque fichier.  
  
 `alias`  
 Un identificateur C# valide représentant un espace de noms racine qui contient tous les espaces de noms dans l’assembly.  
  
## <a name="remarks"></a>Notes  
 Pour importer à partir de plusieurs fichiers, incluez une option **-reference** pour chaque fichier.  
  
 Les fichiers que vous importez doivent contenir un manifeste ; le fichier de sortie doit être compilé avec une option [-target](../../../csharp/language-reference/compiler-options/target-compiler-option.md) autre que [-target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md).  
  
 **-r** est la forme abrégée de **-reference**.  
  
 Utilisez [-addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md) pour importer les métadonnées d’un fichier de sortie qui ne contient pas de manifeste d’assembly.  
  
 Si vous référencez un assembly (Assembly A) qui référence un autre assembly (Assembly B), vous devez référencer l’Assembly B si :  
  
-   Un type que vous utilisez de l’Assembly A hérite d’un type ou implémente une interface de l’Assembly B.  
  
-   Vous appelez un champ, une propriété, un événement ou une méthode qui a un type de retour ou un type de paramètre de l’Assembly B.  
  
 Utilisez [-lib](../../../csharp/language-reference/compiler-options/lib-compiler-option.md) pour spécifier le répertoire dans lequel se trouvent une ou plusieurs références d’assembly. La rubrique **-lib** décrit également les répertoires dans lesquels le compilateur recherche les assemblys.  
  
 Pour que le compilateur reconnaisse un type dans un assembly, et non dans un module, il doit être forcé à résoudre le type, ce que vous pouvez faire en définissant une instance du type. Il existe d’autres moyens de résoudre les noms de types dans un assembly pour le compilateur : par exemple, si vous héritez d’un type dans un assembly, le nom du type est ensuite reconnu par le compilateur.  
  
 Il est parfois nécessaire de référencer deux versions différentes du même composant dans un assembly. Pour ce faire, utilisez la sous-option d’alias du commutateur **-reference** pour chaque fichier afin de faire la différence entre les deux fichiers. Cet alias est utilisé comme qualificateur pour le nom du composant et se traduit par le composant dans l’un des fichiers.  
  
 Le fichier de réponse csc (.rsp), qui référence les assemblys .NET Framework couramment utilisés, est utilisé par défaut. Utilisez [-noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md) si vous ne voulez pas que le compilateur utilise csc.rsp.  
  
> [!NOTE]
> Dans Visual Studio, utilisez la boîte de dialogue **Ajouter une référence**. Pour plus d’informations, consultez [Guide pratique pour ajouter ou supprimer des références à l’aide du gestionnaire de références](/visualstudio/ide/how-to-add-or-remove-references-by-using-the-reference-manager). Pour garantir un comportement équivalent selon que vous ajoutez des références à l’aide de `-reference` ou à l’aide de la boîte de dialogue **Ajouter une référence**, définissez la propriété **Incorporer les types interop** sur **False** pour l’assembly que vous ajoutez. La valeur par défaut de la propriété est **True**.  
  
## <a name="example"></a>Exemple  
 Cet exemple montre comment utiliser la fonctionnalité de l’[alias extern](../../../csharp/language-reference/keywords/extern-alias.md).  
  
 Vous compilez le fichier source et importez les métadonnées à partir de `grid.dll` et `grid20.dll`, qui ont été compilés précédemment. Les deux DLL contiennent des versions séparées du même composant et vous devez utiliser deux **-reference** avec des options d’alias pour compiler le fichier source. Les options ressemblent à ce qui suit :  
  
 -reference:GridV1=grid.dll et -reference:GridV2=grid20.dll  
  
 Cela configure les alias externes « GridV1 » et « GridV2 » que vous utilisez dans votre programme au moyen d’une instruction extern :  
  
```csharp  
extern alias GridV1;  
extern alias GridV2;  
// Using statements go here.  
```  
  
 Une fois cette opération effectuée, vous pouvez référencer le contrôle de grille de grid.dll en ajoutant un préfixe au nom du contrôle GridV1, comme suit :  
  
```csharp  
GridV1::Grid  
```  
  
 Par ailleurs, vous pouvez référencer le contrôle de grille de grid20.dll en ajoutant un préfixe au nom du contrôle GridV2, comme suit :  
  
```csharp  
GridV2::Grid   
```  
  
## <a name="see-also"></a>Voir aussi  
 [Options du compilateur C#](../../../csharp/language-reference/compiler-options/index.md)  
 [Gestion des propriétés des projets et des solutions](/visualstudio/ide/managing-project-and-solution-properties)
