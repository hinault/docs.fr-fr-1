---
title: "Options du compilateur C# par ordre alphabétique"
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- compiler options [C#], listed alpabetically
- C# language, compiler options listed alphabitically
- Visual C# compiler, options listed alphabetically
- Visual C#, compiler options listed alphabetically
ms.assetid: 43535ea0-ca47-4a15-b528-615087a86092
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: f4d7f1b122d3481dc8c3c5256ee361965846a830
ms.sourcegitcommit: dd6ea7f0e581ac84e0a90d9b23c463fcf1ec3ce7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/23/2018
---
# <a name="c-compiler-options-listed-alphabetically"></a>Options du compilateur C# par ordre alphabétique
Les options du compilateur suivantes sont triées par ordre alphabétique. Pour obtenir la liste par catégorie, consultez [Options du compilateur C# par catégorie](../../../csharp/language-reference/compiler-options/listed-by-category.md).  
  
|Option|Objectif|  
|------------|-------------|  
|[@](../../../csharp/language-reference/compiler-options/response-file-compiler-option.md)|Lit un fichier réponse pour obtenir plus d'options.|  
|[-?](../../../csharp/language-reference/compiler-options/help-compiler-option.md)|Affiche un message d'utilisation dans stdout.|  
|-additionalfile|Nomme des fichiers supplémentaires qui n'affectent pas directement la génération de code, mais peuvent être utilisés par des analyseurs pour produire des erreurs ou des avertissements.|  
|[-addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md)|Lie les modules spécifiés dans cet assembly.|  
|-analyzer|Exécute les analyseurs à partir de cet assembly (forme abrégée : -a).|  
|[/appconfig](../../../csharp/language-reference/compiler-options/appconfig-compiler-option.md)|Spécifie l’emplacement du fichier app.config au moment de la liaison d’assembly.|  
|[-baseaddress](../../../csharp/language-reference/compiler-options/baseaddress-compiler-option.md)|Spécifie l'adresse de base de la bibliothèque à générer.|  
|[-bugreport](../../../csharp/language-reference/compiler-options/bugreport-compiler-option.md)|Crée un fichier de rapport de bogue. Ce fichier est envoyé avec les informations d’incident s’il est utilisé avec -errorprompt:prompt ou -errorreport:send.|  
|[/checked](../../../csharp/language-reference/compiler-options/checked-compiler-option.md)|Indique au compilateur de générer des contrôles de dépassement de capacité.|  
|-checksumalgorithm:\<alg>|Spécifiez l'algorithme de calcul de la somme de contrôle du fichier source stockée dans le fichier PDB.  Les valeurs prises en charge sont : SHA1 (par défaut) ou SHA256.|  
|[-codepage](../../../csharp/language-reference/compiler-options/codepage-compiler-option.md)|Spécifie la page de codes à utiliser à l'ouverture des fichiers sources.|  
|[-debug](../../../csharp/language-reference/compiler-options/debug-compiler-option.md)|Émet des informations de débogage.|  
|[-define](../../../csharp/language-reference/compiler-options/define-compiler-option.md)|Définit des symboles de compilation conditionnelle.|  
|[-delaysign](../../../csharp/language-reference/compiler-options/delaysign-compiler-option.md)|Diffère la signature de l'assembly en utilisant uniquement la partie publique de la clé de nom fort.|  
|[-doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)|Spécifie un fichier de documentation XML à générer.|  
|[-errorreport](../../../csharp/language-reference/compiler-options/errorreport-compiler-option.md)|Spécifie comment gérer les erreurs internes du compilateur : invite, envoi et aucune gestion. La valeur par défaut est aucune gestion.|  
|[-filealign](../../../csharp/language-reference/compiler-options/filealign-compiler-option.md)|Spécifie l'alignement utilisé pour les sections du fichier de sortie.|  
|[/fullpaths](../../../csharp/language-reference/compiler-options/fullpaths-compiler-option.md)|Indique au compilateur de générer des chemins d’accès complets.|  
|[-help](../../../csharp/language-reference/compiler-options/help-compiler-option.md)|Affiche un message d'utilisation dans stdout.|  
|[-highentropyva](../../../csharp/language-reference/compiler-options/highentropyva-compiler-option.md)|Spécifie que la randomisation du format d'espace d'adresse (ASLR) d'entropie élevée est prise en charge.|  
|-incremental|Active la compilation incrémentielle [obsolète].|  
|[-keycontainer](../../../csharp/language-reference/compiler-options/keycontainer-compiler-option.md)|Spécifie un conteneur de clé de nom fort.|  
|[-keyfile](../../../csharp/language-reference/compiler-options/keyfile-compiler-option.md)|Spécifie un fichier de clé de nom fort.|  
|[-langversion:\<string>](../../../csharp/language-reference/compiler-options/langversion-compiler-option.md)|Spécifie le mode de version de langage : Default, ISO-1, ISO-2, 3, 4, 5, 6, 7, 7.1 ou Latest |  
|[/lib](../../../csharp/language-reference/compiler-options/lib-compiler-option.md)|Spécifie les répertoires supplémentaires dans lesquels rechercher des références.|  
|[-link](../../../csharp/language-reference/compiler-options/link-compiler-option.md)|Rend les informations de type COM dans les assemblys spécifiés disponibles pour le projet.|  
|[-linkresource](../../../csharp/language-reference/compiler-options/linkresource-compiler-option.md)|Lie la ressource spécifiée à cet assembly.|  
|[-main](../../../csharp/language-reference/compiler-options/main-compiler-option.md)|Spécifie le type qui contient le point d'entrée (ignorez tous les autres points d'entrée possibles)|  
|[-moduleassemblyname](../../../csharp/language-reference/compiler-options/moduleassemblyname-compiler-option.md)|Spécifie un assembly dont les types non publics sont accessibles par un .netmodule.|  
|-modulename:\<string>|Spécifiez le nom du module source.|  
|[-noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md)|Indique au compilateur ne pas inclure automatiquement de fichier CSC.RSP.|  
|[-nologo](../../../csharp/language-reference/compiler-options/nologo-compiler-option.md)|Supprime le message de copyright du compilateur.|  
|[-nostdlib](../../../csharp/language-reference/compiler-options/nostdlib-compiler-option.md)|Indique au compilateur de ne pas référencer la bibliothèque standard (mscorlib.dll).|  
|[-nowarn](../../../csharp/language-reference/compiler-options/nowarn-compiler-option.md)|Désactive des messages d'avertissement spécifiques.|  
|[-nowin32manifest](../../../csharp/language-reference/compiler-options/nowin32manifest-compiler-option.md)|Indique au compilateur de ne pas incorporer un manifeste d'application dans le fichier exécutable.|  
|[-optimize](../../../csharp/language-reference/compiler-options/optimize-compiler-option.md)|Active/désactive les optimisations.|  
|[-out](../../../csharp/language-reference/compiler-options/out-compiler-option.md)|Spécifie le nom de fichier de sortie (par défaut : nom de base du fichier avec classe principale ou premier fichier).|  
|-parallel[+&#124;-]|Indique s'il faut utiliser la build simultanée (+).|  
|[/pdb](../../../csharp/language-reference/compiler-options/pdb-compiler-option.md)|Spécifie le nom et l'emplacement du fichier .pdb.|  
|[-platform](../../../csharp/language-reference/compiler-options/platform-compiler-option.md)|Limite les plateformes sur lesquelles ce code peut s'exécuter : x86, Itanium, x64, anycpu ou anycpu32bitpreferred. La valeur par défaut est anycpu.|  
|[/preferreduilang](../../../csharp/language-reference/compiler-options/preferreduilang-compiler-option.md)|Spécifie la langue à utiliser pour la sortie du compilateur.|  
|[-recurse](../../../csharp/language-reference/compiler-options/recurse-compiler-option.md)|Inclut tous les fichiers dans le répertoire et les sous-répertoires actuels en fonction des spécifications de caractères génériques.|  
|[-reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)|Référence les métadonnées à partir des fichiers d'assembly spécifiés.|  
|[/refout](refout-compiler-option.md)|Génère un assembly de référence en plus de l’assembly principal.|  
|[-refonly](refonly-compiler-option.md)|Génère un assembly de référence au lieu d’un assembly principal.|  
|[-resource](../../../csharp/language-reference/compiler-options/resource-compiler-option.md)|Incorpore la ressource spécifiée.|  
|-ruleset:\<file>|Spécifiez un fichier ruleset qui désactive des diagnostics spécifiques.|  
|[-subsystemversion](../../../csharp/language-reference/compiler-options/subsystemversion-compiler-option.md)|Spécifie la version minimale du sous-système utilisable par le fichier exécutable.|  
|[-target](../../../csharp/language-reference/compiler-options/target-compiler-option.md)|Spécifie le format du fichier de sortie en utilisant l’une des quatre options suivantes :[-target:appcontainerexe](../../../csharp/language-reference/compiler-options/target-appcontainerexe-compiler-option.md), [-target:exe](../../../csharp/language-reference/compiler-options/target-exe-compiler-option.md), [-target:library](../../../csharp/language-reference/compiler-options/target-library-compiler-option.md), [-target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md), [-target:winexe](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md), [-target:winmdobj](../../../csharp/language-reference/compiler-options/target-winmdobj-compiler-option.md).|  
|[unsafe](../../../csharp/language-reference/compiler-options/unsafe-compiler-option.md)|Autorise le code [unsafe](../../../csharp/language-reference/keywords/unsafe.md).|  
|[-utf8output](../../../csharp/language-reference/compiler-options/utf8output-compiler-option.md)|Génère des messages du compilateur encodés en UTF-8.|  
|[/warn](../../../csharp/language-reference/compiler-options/warn-compiler-option.md)|Définit le niveau d'avertissement (entre 0 et 4).|  
|[-warnaserror](../../../csharp/language-reference/compiler-options/warnaserror-compiler-option.md)|Signale des avertissements spécifiques en tant qu'erreurs.|  
|[-win32icon](../../../csharp/language-reference/compiler-options/win32icon-compiler-option.md)|Utilise cette icône pour la sortie.|  
|[-win32manifest](../../../csharp/language-reference/compiler-options/win32manifest-compiler-option.md)|Spécifie un fichier manifeste win32 personnalisé.|  
|[/win32res:](../../../csharp/language-reference/compiler-options/win32res-compiler-option.md)|Spécifie le fichier de ressources win32 (.res).|  
  
## <a name="see-also"></a>Voir aussi  
 [Options du compilateur C#](../../../csharp/language-reference/compiler-options/index.md)  
 [Options du compilateur C# par catégorie](../../../csharp/language-reference/compiler-options/listed-by-category.md)  
 [Guide pratique pour définir des variables d’environnement pour la ligne de commande Visual Studio](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)  
 [\<compiler> Element](../../../framework/configure-apps/file-schema/compiler/compiler-element.md)
