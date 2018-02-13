---
title: "Options du compilateur C# par catégorie"
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
helpviewer_keywords:
- Visual C# compiler, options listed by category
- compiler options [C#], listed by category
- Visual C#, compiler options listed by category
ms.assetid: 96437ecc-6502-4cd3-b070-e9386a298e83
caps.latest.revision: "17"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 410cad333b023e59d8c093d70d0e248504625dd6
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="c-compiler-options-listed-by-category"></a>Options du compilateur C# par catégorie
Les options du compilateur suivantes sont triées par catégorie. Pour en obtenir la liste alphabétique, consultez [Options du compilateur C# par ordre alphabétique](../../../csharp/language-reference/compiler-options/listed-alphabetically.md).  
  
### <a name="optimization"></a>Optimisation  
  
|Option|Objectif|  
|------------|-------------|  
|[-filealign](../../../csharp/language-reference/compiler-options/filealign-compiler-option.md)|Spécifie la taille des sections dans le fichier de sortie.|  
|[-optimize](../../../csharp/language-reference/compiler-options/optimize-compiler-option.md)|Active/désactive les optimisations.|  
  
### <a name="output-files"></a>Fichiers de sortie  
  
|Option|Objectif|  
|------------|-------------|  
|[-doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)|Spécifie un fichier XML dans lequel les commentaires de documentation traités doivent être écrits.|  
|[-out](../../../csharp/language-reference/compiler-options/out-compiler-option.md)|Spécifie le fichier de sortie.|  
|[/pdb](../../../csharp/language-reference/compiler-options/pdb-compiler-option.md)|Spécifie le nom et l'emplacement du fichier .pdb.|  
|[-platform](../../../csharp/language-reference/compiler-options/platform-compiler-option.md)|Spécifie la plateforme de sortie.|  
|[/preferreduilang](../../../csharp/language-reference/compiler-options/preferreduilang-compiler-option.md)|Spécifiez un langage pour les résultats de la compilation.|  
|[/refout](refout-compiler-option.md)|Génère un assembly de référence en plus de l’assembly principal.|  
|[-refonly](refonly-compiler-option.md)|Génère un assembly de référence au lieu d’un assembly principal.|  
|[-target](../../../csharp/language-reference/compiler-options/target-compiler-option.md)|Spécifie le format du fichier de sortie en utilisant l’une des cinq options suivantes : [-target:appcontainerexe](../../../csharp/language-reference/compiler-options/target-appcontainerexe-compiler-option.md), [-target:exe](../../../csharp/language-reference/compiler-options/target-exe-compiler-option.md), [-target:library](../../../csharp/language-reference/compiler-options/target-library-compiler-option.md), [-target:module](../../../csharp/language-reference/compiler-options/target-module-compiler-option.md), [-target:winexe](../../../csharp/language-reference/compiler-options/target-winexe-compiler-option.md) ou [-target:winmdobj](../../../csharp/language-reference/compiler-options/target-winmdobj-compiler-option.md).|  
|-modulename:\<string>|Spécifiez le nom du module source.|  
  
### <a name="net-framework-assemblies"></a>Assemblys .NET Framework  
  
|Option|Objectif|  
|------------|-------------|  
|[-addmodule](../../../csharp/language-reference/compiler-options/addmodule-compiler-option.md)|Spécifie un ou plusieurs modules à inclure dans cet assembly.|  
|[-delaysign](../../../csharp/language-reference/compiler-options/delaysign-compiler-option.md)|Indique au compilateur d'ajouter la clé publique mais de laisser l'assembly non signé.|  
|[-keycontainer](../../../csharp/language-reference/compiler-options/keycontainer-compiler-option.md)|Spécifie le nom du conteneur de la clé de chiffrement.|  
|[-keyfile](../../../csharp/language-reference/compiler-options/keyfile-compiler-option.md)|Spécifie le nom du fichier contenant la clé de chiffrement.|  
|[/lib](../../../csharp/language-reference/compiler-options/lib-compiler-option.md)|Spécifie l’emplacement des assemblys référencés par le biais de [-reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md).|  
|[-nostdlib](../../../csharp/language-reference/compiler-options/nostdlib-compiler-option.md)|Indique au compilateur de ne pas importer la bibliothèque standard (mscorlib.dll).|  
|[-reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)|Importe des métadonnées à partir d'un fichier qui contient un assembly.|  
|-analyzer|Exécutez les analyseurs à partir de cet assembly (forme abrégée : /a).|  
|-additionalfile|Nomme des fichiers supplémentaires qui n'affectent pas directement la génération de code, mais peuvent être utilisés par des analyseurs pour produire des erreurs ou des avertissements.|  
  
### <a name="debuggingerror-checking"></a>Débogage/vérification des erreurs  
  
|Option|Objectif|  
|------------|-------------|  
|[-bugreport](../../../csharp/language-reference/compiler-options/bugreport-compiler-option.md)|Crée un fichier qui contient des informations qui facilitent le signalement d'un bogue.|  
|[/checked](../../../csharp/language-reference/compiler-options/checked-compiler-option.md)|Indique si l'arithmétique sur les entiers qui dépasse les limites du type de données entraîne une exception au moment de l'exécution.|  
|[-debug](../../../csharp/language-reference/compiler-options/debug-compiler-option.md)|Indique au compilateur d'émettre des informations de débogage.|  
|[-errorreport](../../../csharp/language-reference/compiler-options/errorreport-compiler-option.md)|Définit le comportement de signalement d'erreurs.|  
|[/fullpaths](../../../csharp/language-reference/compiler-options/fullpaths-compiler-option.md)|Spécifie le chemin d’accès absolu au fichier de sortie du compilateur.|  
|[-nowarn](../../../csharp/language-reference/compiler-options/nowarn-compiler-option.md)|Supprime la génération par le compilateur des avertissements spécifiés.|  
|[/warn](../../../csharp/language-reference/compiler-options/warn-compiler-option.md)|Définit le niveau d'avertissement.|  
|[-warnaserror](../../../csharp/language-reference/compiler-options/warnaserror-compiler-option.md)|Transforme les avertissements en erreurs.|  
|-ruleset:\<file>|Spécifiez un fichier ruleset qui désactive des diagnostics spécifiques.|  
  
### <a name="preprocessor"></a>Préprocesseur  
  
|Option|Objectif|  
|------------|-------------|  
|[-define](../../../csharp/language-reference/compiler-options/define-compiler-option.md)|Définit les symboles du préprocesseur.|  
  
### <a name="resources"></a>Ressources  
  
|Option|Objectif|  
|------------|-------------|  
|[-link](../../../csharp/language-reference/compiler-options/link-compiler-option.md)|Rend les informations de type COM dans les assemblys spécifiés disponibles pour le projet.|  
|[-linkresource](../../../csharp/language-reference/compiler-options/linkresource-compiler-option.md)|Crée un lien à une ressource managée.|  
|[-resource](../../../csharp/language-reference/compiler-options/resource-compiler-option.md)|Incorpore une ressource .NET Framework dans le fichier de sortie.|  
|[-win32icon](../../../csharp/language-reference/compiler-options/win32icon-compiler-option.md)|Spécifie un fichier .ico à insérer dans le fichier de sortie.|  
|[/win32res:](../../../csharp/language-reference/compiler-options/win32res-compiler-option.md)|Spécifie une ressource Win32 à insérer dans le fichier de sortie.|  
  
### <a name="miscellaneous"></a>Divers  
  
|Option|Objectif|  
|------------|-------------|  
|[@](../../../csharp/language-reference/compiler-options/response-file-compiler-option.md)|Spécifie un fichier réponse.|  
|[-?](../../../csharp/language-reference/compiler-options/help-compiler-option.md)|Répertorie les options du compilateur dans stdout.|  
|[-baseaddress](../../../csharp/language-reference/compiler-options/baseaddress-compiler-option.md)|Spécifie l'adresse de base préférée à laquelle charger une DLL.|  
|[-codepage](../../../csharp/language-reference/compiler-options/codepage-compiler-option.md)|Spécifie la page de codes à utiliser pour tous les fichiers de code source inclus dans la compilation.|  
|[-help](../../../csharp/language-reference/compiler-options/help-compiler-option.md)|Répertorie les options du compilateur dans stdout.|  
|[-highentropyva](../../../csharp/language-reference/compiler-options/highentropyva-compiler-option.md)|Spécifie que le fichier exécutable prend en charge la randomisation du format d'espace d'adresse (ASLR).|  
|[-langversion](../../../csharp/language-reference/compiler-options/langversion-compiler-option.md)|Spécifie le mode de version de langage : Default, ISO-1, ISO-2, 3, 4, 5, 6, 7, 7.1 ou Latest |  
|[-main](../../../csharp/language-reference/compiler-options/main-compiler-option.md)|Spécifie l’emplacement de la méthode **Main**.|  
|[-noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md)|Indique au compilateur ne pas compiler avec csc.rsp.|  
|[-nologo](../../../csharp/language-reference/compiler-options/nologo-compiler-option.md)|Supprime les informations de bannière du compilateur.|  
|[-recurse](../../../csharp/language-reference/compiler-options/recurse-compiler-option.md)|Recherche des fichiers sources à compiler dans les sous-répertoires.|  
|[-subsystemversion](../../../csharp/language-reference/compiler-options/subsystemversion-compiler-option.md)|Spécifie la version minimale du sous-système utilisable par le fichier exécutable.|  
|[unsafe](../../../csharp/language-reference/compiler-options/unsafe-compiler-option.md)|Active la compilation du code qui utilise le mot clé [unsafe](../../../csharp/language-reference/keywords/unsafe.md).|  
|[-utf8output](../../../csharp/language-reference/compiler-options/utf8output-compiler-option.md)|Affiche les résultats de la compilation au format d'encodage UTF-8.|  
|-parallel[+&#124;-]|Indique s'il faut utiliser la build simultanée (+).|  
|-checksumalgorithm:\<alg>|Spécifiez l'algorithme de calcul de la somme de contrôle du fichier source stockée dans le fichier PDB.  Les valeurs prises en charge sont : SHA1 (par défaut) ou SHA256.|  
  
## <a name="obsolete-options"></a>Options obsolètes  
  
|Option|Objectif|  
|---|---|  
|-incremental|Active la compilation incrémentielle.|  
  
## <a name="see-also"></a>Voir aussi  
 [Options du compilateur C#](../../../csharp/language-reference/compiler-options/index.md)  
 [Options du compilateur C# par ordre alphabétique](../../../csharp/language-reference/compiler-options/listed-alphabetically.md)  
 [Comment : définir des variables d’environnement pour la ligne de commande Visual Studio](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)
