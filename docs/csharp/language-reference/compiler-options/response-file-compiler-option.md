---
title: '@ (Options du compilateur C#)'
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
f1_keywords: '@'
helpviewer_keywords:
- response files, specifying for compilation [C#]
- '@ compiler option'
ms.assetid: dda4fa9f-a02c-400f-8b6a-d58834e13d7f
caps.latest.revision: "9"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: fbb95e0619857f38260ae74366ba4bb860779530
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="-c-compiler-options"></a>@ (Options du compilateur C#)
L’option @ vous permet de spécifier un fichier qui contient les options du compilateur et les fichiers de code source à compiler.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
@response_file  
```  
  
## <a name="arguments"></a>Arguments  
 `response_file`  
 Fichier qui répertorie des options du compilateur ou des fichiers de code source à compiler.  
  
## <a name="remarks"></a>Notes  
 Les options du compilateur et les fichiers de code source seront traités par le compilateur exactement comme s’ils avaient été spécifiés sur la ligne de commande.  
  
 Pour spécifier plusieurs fichiers réponse dans une compilation, spécifiez plusieurs options de fichier réponse. Exemple :  
  
```  
@file1.rsp @file2.rsp  
```  
  
 Dans un fichier réponse, plusieurs options du compilateur et fichiers de code source peuvent apparaître sur une même ligne. En revanche, si vous spécifiez une seule option du compilateur, celle-ci doit obligatoirement figurer sur une seule et même ligne. Les fichiers réponse peuvent contenir des commentaires, précédés du symbole #.  
  
 La spécification d’options du compilateur à partir d’un fichier réponse est identique à la spécification de ces commandes sur la ligne de commande. Pour plus d’informations, consultez [Génération à partir de la ligne de commande](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md).  
  
 Le compilateur traite les options de commande au fur et à mesure qu’il les rencontre. Par conséquent, des arguments de ligne de commande peuvent substituer des options précédemment affichées dans des fichiers réponse. Inversement, les options d’un fichier réponse substituent les options affichées précédemment dans la ligne de commande ou dans d’autres fichiers réponse.  
  
 C# fournit le fichier csc.rsp, qui se trouve dans le même répertoire que le fichier csc.exe. Pour plus d’informations sur csc.rsp, consultez [-noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md).  
  
 Cette option du compilateur ne peut pas être définie dans l’environnement de développement Visual Studio, ni être modifiée par programmation.  
  
## <a name="example"></a>Exemple  
 Voici quelques lignes extraites d’un exemple de fichier réponse :  
  
```console  
# build the first output file  
-target:exe -out:MyExe.exe source1.cs source2.cs  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Options du compilateur C#](../../../csharp/language-reference/compiler-options/index.md)
