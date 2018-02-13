---
title: "-target:winmdobj (Options du compilateur C#)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
ms.assetid: 1819a045-659d-498a-9457-c466e902986f
caps.latest.revision: "15"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 444fcd69db327ea9d9c3dc739b42520bb9472c4d
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="-targetwinmdobj-c-compiler-options"></a>-target:winmdobj (Options du compilateur C#)
Si vous utilisez l’option du compilateur **-target:winmdobj**, le compilateur crée un fichier .winmdobj intermédiaire que vous pouvez convertir en fichier binaire (.winmd) Windows Runtime. Le fichier .winmd peut ensuite être consommé par des programmes JavaScript et C++, en plus des programmes en langage managé.  
  
## <a name="syntax"></a>Syntaxe  
  
```console  
-target:winmdobj  
```  
  
## <a name="remarks"></a>Notes  
 Le paramètre **winmdobj** signale au compilateur qu’un module intermédiaire est requis. En réponse, Visual Studio compile la bibliothèque de classes C# comme fichier .winmdobj. Le fichier .winmdobj peut ensuite être acheminé via l'outil d'exportation <xref:Microsoft.Build.Tasks.WinMDExp> pour produire un fichier de métadonnées Windows (.winmd). Le fichier .winmd contient à la fois le code de la bibliothèque d'origine et les métadonnées WinMD utilisées par JavaScript ou C++ et par le Windows Runtime.  
  
 La sortie d’un fichier qui est compilé à l’aide de l’option du compilateur **-target:winmdobj** est conçue pour être utilisée uniquement comme entrée pour l’outil d’exportation WimMDExp ; le fichier .winmdobj proprement dit n’est pas référencé directement.  
  
 À moins que vous n’utilisiez l’option [-out](../../../csharp/language-reference/compiler-options/out-compiler-option.md), le fichier de sortie adopte le nom du premier fichier d’entrée. Une méthode [Main](../../../csharp/programming-guide/main-and-command-args/index.md) n’est pas nécessaire.  
  
 Si vous spécifiez l’option -target:winmdobj à une invite de commandes, tous les fichiers jusqu’à l’option **-out** ou [-target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md) suivante sont utilisés pour créer le programme Windows.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-ide-for-a-windows-store-app"></a>Pour définir cette option du compilateur dans l'IDE de Visual Studio pour une application Windows Store  
  
1.  Dans l’**Explorateur de solutions**, ouvrez le menu contextuel de votre projet et choisissez **Propriétés**.  
  
2.  Choisissez l’onglet **Application**.  
  
3.  Dans la liste **Type de sortie**, choisissez **Fichier WinMD**.  
  
     L’option **Fichier WinMD** est disponible uniquement pour les modèles d’application [!INCLUDE[win8_appname_long](~/includes/win8-appname-long-md.md)].  
  
 Pour plus d'informations sur la façon de définir cette option du compilateur par programme, consultez <xref:VSLangProj80.ProjectProperties3.OutputType%2A>.  
  
## <a name="example"></a>Exemple  
 La commande suivante compile `filename.cs` dans un fichier .winmdobj intermédiaire.  
  
```console  
csc -target:winmdobj filename.cs  
```  
  
## <a name="see-also"></a>Voir aussi  
 [-target (Options du compilateur C#)](../../../csharp/language-reference/compiler-options/target-compiler-option.md)  
 [Options du compilateur C#](../../../csharp/language-reference/compiler-options/index.md)
