---
title: "Génération et compilation du code source à partir d’un graphique CodeDOM"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- code compilers
- CodeDOM, generating source code
- Code Document Object Model, graphs
- templated code generation
- source code, generating
- dynamically representing source code
- generating CodeDOM graphs
- Code Document Object Model, generating source code
- translating language to language
- compiling assemblies
- generating source code in multiple languages
- graphing with CodeDOM
- dynamic compilation
- assemblies [.NET Framework], CodeDOM
- source code generation
- outputting source code by CodeDOM
- code generators
- compiling source code, multiple languages
- CodeDOM, graphs
ms.assetid: 6c864c8e-6dd3-4a65-ace0-36879d9a9c42
caps.latest.revision: "20"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: b99dacb5a30cd7b12a5a5dd96bf9fe25b32ab984
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="generating-and-compiling-source-code-from-a-codedom-graph"></a>Génération et compilation du code source à partir d’un graphique CodeDOM
L’espace de noms <xref:System.CodeDom.Compiler> fournit des interfaces pour la génération de code source à partir de graphiques d’objets CodeDOM et pour la gestion de la compilation avec les compilateurs pris en charge. Un fournisseur de code peut produire du code source dans un langage de programmation particulier en fonction d’un graphique CodeDOM. Une classe qui dérive de <xref:System.CodeDom.Compiler.CodeDomProvider> peut fournir en général des méthodes pour générer et compiler le code pour le langage pris en charge par le fournisseur.  
  
## <a name="using-a-codedom-code-provider-to-generate-source-code"></a>Utilisation d’un fournisseur de code CodeDOM pour générer du code source  
 Pour générer du code source dans un langage particulier, vous avez besoin d’un graphique CodeDOM qui représente la structure du code source à générer.  
  
 L’exemple suivant montre comment créer une instance de <xref:Microsoft.CSharp.CSharpCodeProvider> :  
  
 [!code-cpp[CodeDomExample#21](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source3.cpp#21)]
 [!code-csharp[CodeDomExample#21](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source3.cs#21)]
 [!code-vb[CodeDomExample#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source3.vb#21)]  
  
 Le graphique de génération du code est généralement contenu dans un <xref:System.CodeDom.CodeCompileUnit>. Pour générer le code pour un **CodeCompileUnit** qui contient un graphique CodeDOM, appelez la méthode <xref:System.CodeDom.Compiler.CodeDomProvider.GenerateCodeFromCompileUnit%2A> du fournisseur de code. Cette méthode a un paramètre pour un <xref:System.IO.TextWriter> qu’elle utilise pour générer le code source. Ainsi, il est parfois nécessaire de créer d’abord un **TextWriter** accessible en écriture. L’exemple suivant illustre la génération de code à partir d’un **CodeCompileUnit** et l’écriture du code source généré dans un fichier nommé HelloWorld.cs.  
  
 [!code-cpp[CodeDomExample#22](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source3.cpp#22)]
 [!code-csharp[CodeDomExample#22](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source3.cs#22)]
 [!code-vb[CodeDomExample#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source3.vb#22)]  
  
## <a name="using-a-codedom-code-provider-to-compile-assemblies"></a>Utilisation d’un fournisseur de code CodeDOM pour compiler des assemblys  
 **Appel de la compilation**  
  
 Pour compiler un assembly à l’aide d’un fournisseur CodeDom, vous devez disposer du code source à compiler dans un langage pour lequel vous avez un compilateur, ou d’un graphique CodeDOM à partir duquel ce code source à compiler peut être généré.  
  
 Si vous compilez un graphique CodeDOM, passez le <xref:System.CodeDom.CodeCompileUnit> contenant le graphique à la méthode <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromDom%2A> du fournisseur de code. Si vous avez un fichier de code source dans un langage que le compilateur comprend, passez le nom du fichier contenant le code source à la méthode <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromFile%2A> du fournisseur CodeDom. Vous pouvez aussi passer une chaîne contenant le code source dans un langage que le compilateur comprend à la méthode <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromSource%2A> du fournisseur CodeDom.  
  
 **Configuration des paramètres de compilation**  
  
 Toutes les méthodes d’appel de compilation standard d’un fournisseur CodeDom ont un paramètre de type <xref:System.CodeDom.Compiler.CompilerParameters> qui indique les options à utiliser pour la compilation.  
  
 Vous pouvez spécifier un nom de fichier pour l’assembly de sortie dans la propriété <xref:System.CodeDom.Compiler.CompilerParameters.OutputAssembly%2A> de **CompilerParameters**. Sinon, un nom de fichier de sortie par défaut est utilisé.  
  
 Par défaut, un nouveau **CompilerParameters** est initialisé avec sa propriété <xref:System.CodeDom.Compiler.CompilerParameters.GenerateExecutable%2A> définie sur **false**. Si vous compilez un programme exécutable, vous devez affecter la valeur **true** à la propriété **GenerateExecutable**. Quand **GenerateExecutable** a la valeur **false**, le compilateur génère une bibliothèque de classes.  
  
 Si vous compilez un exécutable à partir d’un graphique CodeDOM, un <xref:System.CodeDom.CodeEntryPointMethod> doit être défini dans le graphique. S’il existe plusieurs points d’entrée de code, il peut être nécessaire d’affecter à la propriété <xref:System.CodeDom.Compiler.CompilerParameters.MainClass%2A> de **CompilerParameters** le nom de la classe qui définit le point d’entrée à utiliser.  
  
 Pour inclure des informations de débogage dans un exécutable généré, affectez la valeur **true** à la propriété <xref:System.CodeDom.Compiler.CompilerParameters.IncludeDebugInformation%2A>.  
  
 Si votre projet référence des assemblys, vous devez spécifier les noms des assemblys en tant qu’éléments dans un <xref:System.Collections.Specialized.StringCollection> en tant que propriété <xref:System.CodeDom.Compiler.CompilerParameters.ReferencedAssemblies%2A> du **CompilerParameters** que vous utilisez pour appeler la compilation.  
  
 Vous pouvez compiler un assembly écrit en mémoire plutôt que sur disque en affectant la valeur **true** à la propriété <xref:System.CodeDom.Compiler.CompilerParameters.GenerateInMemory%2A>. Quand un assembly est généré en mémoire, votre code peut obtenir une référence à l’assembly généré à partir de la propriétés <xref:System.CodeDom.Compiler.CompilerResults.CompiledAssembly%2A> d’un <xref:System.CodeDom.Compiler.CompilerResults>. Si un assembly est écrit sur disque, vous pouvez obtenir le chemin de l’assembly généré à partir de la propriété <xref:System.CodeDom.Compiler.CompilerResults.PathToAssembly%2A> d’un **CompilerResults**.  
  
 Pour spécifier une chaîne d’arguments de ligne de commande personnalisée à utiliser lors de l’appel du processus de compilation, définissez la chaîne dans la propriété <xref:System.CodeDom.Compiler.CompilerParameters.CompilerOptions%2A>.  
  
 Si un jeton de sécurité Win32 est nécessaire pour appeler le processus de compilation, spécifiez-le dans la propriété <xref:System.CodeDom.Compiler.CompilerParameters.UserToken%2A>.  
  
 Pour lier un fichier de ressources Win32 dans l’assembly compilé, spécifiez le nom du fichier de ressources Win32 dans la propriété <xref:System.CodeDom.Compiler.CompilerParameters.Win32Resource%2A>.  
  
 Pour spécifier un niveau d’avertissement auquel il faut arrêter la compilation, affectez à la propriété <xref:System.CodeDom.Compiler.CompilerParameters.WarningLevel%2A> un entier qui représente le niveau d’avertissement. Vous pouvez également configurer le compilateur pour arrêter la compilation si des avertissements sont générés en affectant la valeur **true** à la propriété <xref:System.CodeDom.Compiler.CompilerParameters.TreatWarningsAsErrors%2A>.  
  
 L’exemple de code suivant illustre la compilation d’un fichier source à l’aide d’un fournisseur CodeDom dérivé de la classe <xref:System.CodeDom.Compiler.CodeDomProvider>.  
  
 [!code-cpp[CodeDomExample#23](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source3.cpp#23)]
 [!code-csharp[CodeDomExample#23](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source3.cs#23)]
 [!code-vb[CodeDomExample#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source3.vb#23)]  
  
## <a name="languages-with-initial-support"></a>Langages avec prise en charge initiale  
 Le .NET Framework fournit des compilateurs de code et des générateurs de code pour les langages suivants : C#, Visual Basic, C++ et JScript. La prise en charge de codeDOM peut être étendue à d’autres langages en implémentant des générateurs de code et des compilateurs de code propres au langage.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.CodeDom>  
 <xref:System.CodeDom.Compiler>  
 [Génération et compilation de code source dynamique](../../../docs/framework/reflection-and-codedom/dynamic-source-code-generation-and-compilation.md)  
 [Aide-mémoire de CodeDOM](http://msdn.microsoft.com/library/c77b8bfd-0a32-4e36-b59a-4f687f32c524)
