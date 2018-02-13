---
title: -warn (Options du compilateur C#)
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
f1_keywords: /warn
helpviewer_keywords:
- warning level [C#]
- /w compiler option [C#]
- -w compiler option [C#]
- -warn compiler option [C#]
- /warn compiler option [C#]
- w compiler option [C#]
- warn compiler option [C#]
ms.assetid: 5f80ff59-4991-4382-9f9a-77da18446e71
caps.latest.revision: "17"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 6a1f2c55aa078adb213a93dc5aff7ced40793bfa
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="-warn-c-compiler-options"></a>-warn (Options du compilateur C#)
L’option **-warn** spécifie le niveau d’avertissement que le compilateur doit afficher.  
  
## <a name="syntax"></a>Syntaxe  
  
```console  
-warn:option  
```  
  
## <a name="arguments"></a>Arguments  
 `option`  
 Niveau d’avertissement que vous souhaitez afficher pour la compilation : les nombres inférieurs affichent uniquement les avertissements ayant un niveau de gravité élevé ; les nombres supérieurs affichent davantage d’avertissements. Les valeurs valides vont de 0 à 4 :  
  
|Niveau d’avertissement|Signification|  
|-------------------|-------------|  
|0|Désactive l’émission de tous les messages d’avertissement.|  
|1|Affiche les messages d’avertissement graves.|  
|2|Affiche les avertissements de niveau 1, ainsi que certains avertissements moins graves, tels que les avertissements concernant le masquage de membres de classe.|  
|3|Affiche les avertissements de niveau 2, ainsi que certains avertissements moins graves, tels que les avertissements concernant les expressions toujours évaluées à `true` ou `false`.|  
|4 (valeur par défaut)|Affiche les avertissements de niveau 3, ainsi que les avertissements d’information.|  
  
## <a name="remarks"></a>Notes  
 Pour obtenir des informations sur une erreur ou un avertissement, vous pouvez rechercher le code d’erreur dans l’index de l’aide. Il existe d’autres façons d’obtenir des informations sur une erreur ou un avertissement, qui sont décrites dans [Erreurs du compilateur C#](../../../csharp/language-reference/compiler-messages/index.md).  
  
 Utilisez [-warnaserror](../../../csharp/language-reference/compiler-options/warnaserror-compiler-option.md) pour traiter tous les avertissements comme des erreurs. Utilisez [-nowarn](../../../csharp/language-reference/compiler-options/nowarn-compiler-option.md) pour désactiver certains avertissements.  
  
 **-w** est la forme abrégée de **-warn**.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Pour définir cette option du compilateur dans l'environnement de développement Visual Studio  
  
1.  Ouvrez la page **Propriétés** du projet.  
  
2.  Cliquez sur la page de propriétés **Générer**.  
  
3.  Modifiez la propriété **Niveau d’avertissement**.  
  
 Pour plus d’informations sur la façon de définir cette option du compilateur par programmation, consultez <xref:VSLangProj80.CSharpProjectConfigurationProperties3.WarningLevel%2A>.  
  
## <a name="example"></a>Exemple  
 Compilez `in.cs` et faites en sorte que le compilateur n’affiche que les avertissements de niveau 1 :  
  
```console  
csc -warn:1 in.cs  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Options du compilateur C#](../../../csharp/language-reference/compiler-options/index.md)  
 [Gestion des propriétés des projets et des solutions](/visualstudio/ide/managing-project-and-solution-properties)
