---
title: Utilisation du CodeDOM
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
- Code Document Object Model
- Code Document Object Model, graphs
- types, CodeDOM
- namespaces [.NET Framework], CodeDOM
- templated code generation
- dynamically representing source code
- source code models
- CodeDOM
- graphing with CodeDOM
- dynamic compilation
- code generators
- CodeDOM, graphs
ms.assetid: 0444ddf3-c3f6-44ed-a999-f710d9c3e0cf
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 2cd2b8e8ecb0e5d451ebf3c6823144e4a90e0d79
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="using-the-codedom"></a>Utilisation du CodeDOM
CodeDOM fournit des types qui représentent de nombreux types courants d’éléments du code source. Vous pouvez concevoir un programme qui génère un modèle de code source à l’aide d’éléments CodeDOM pour assembler un graphique d’objet. Ce graphique d’objet peut être rendu sous forme de code source à l’aide d’un générateur de code CodeDOM pour un langage de programmation pris en charge. CodeDOM permet également de compiler du code source dans un assembly binaire.  
  
 Voici quelques usages courants de CodeDOM :  
  
-   Génération d’un code modèle : génération du code pour ASP.NET, les proxies clients de services Web XML, les Assistants Code, les concepteurs ou d’autres mécanismes d’émission de code.  
  
-   Compilation dynamique : prise en charge de la compilation du code dans un ou plusieurs langages.  
  
## <a name="building-a-codedom-graph"></a>Génération d’un graphique CodeDOM  
 L’espace de noms <xref:System.CodeDom> fournit des classes représentant la structure logique du code source, indépendamment de la syntaxe d’un langage.  
  
### <a name="the-structure-of-a-codedom-graph"></a>Structure d’un graphique CodeDOM  
 La structure d’un graphique CodeDOM est comparable à une arborescence de conteneurs. Le conteneur de niveau supérieur, ou conteneur racine, de chaque graphique CodeDOM compilable est un <xref:System.CodeDom.CodeCompileUnit>. Chaque élément de votre modèle de code source doit être lié au graphique par le biais d’une propriété d’un <xref:System.CodeDom.CodeObject> du graphique.  
  
### <a name="building-a-source-code-model-for-a-sample-hello-world-program"></a>Génération d’un modèle de code source pour un exemple de programme Hello World  
 L’exemple ci-dessous montre comment générer un graphique d’objet CodeDOM représentant le code d’une application simple Hello World. Pour obtenir le code source complet pour cet exemple, consultez la rubrique <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=nameWithType>.  
  
#### <a name="creating-a-compile-unit"></a>Création d’une unité de compilation  
 CodeDOM définit un objet appelé <xref:System.CodeDom.CodeCompileUnit> qui peut référencer un graphique d’objet CodeDOM modélisant le code source à compiler. **CodeCompileUnit** a des propriétés pour le stockage des références aux attributs, espaces de noms et assemblys.  
  
 Les fournisseurs CodeDOM qui dérivent de la classe <xref:System.CodeDom.Compiler.CodeDomProvider> contiennent des méthodes qui traitent le graphique d’objet référencé par **CodeCompileUnit**.  
  
 Pour créer un graphique d’objet pour une application simple, vous devez assembler le modèle de code source et le référencer à partir de **CodeCompileUnit**.  
  
 Vous pouvez créer une unité de compilation avec la syntaxe illustrée dans l’exemple suivant :  
  
 [!code-cpp[CodeDomExample#12](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#12)]
 [!code-csharp[CodeDomExample#12](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#12)]
 [!code-vb[CodeDomExample#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#12)]  
  
 <xref:System.CodeDom.CodeSnippetCompileUnit> peut contenir une section de code source qui figure déjà dans le langage cible, mais ne peut pas être rendue dans un autre langage.  
  
#### <a name="defining-a-namespace"></a>Définition d’un espace de noms  
 Pour définir un espace de noms, créez un <xref:System.CodeDom.CodeNamespace> et nommez-le en utilisant le constructeur approprié ou en définissant sa propriété **Name**.  
  
 [!code-cpp[CodeDomExample#13](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#13)]
 [!code-csharp[CodeDomExample#13](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#13)]
 [!code-vb[CodeDomExample#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#13)]  
  
#### <a name="importing-a-namespace"></a>Importation d’un espace de noms  
 Pour ajouter une directive d’importation d’espace de noms à l’espace de noms, ajoutez un <xref:System.CodeDom.CodeNamespaceImport> qui spécifie l’espace de noms à importer dans la collection **CodeNamespace.Imports**.  
  
 Le code suivant ajoute une importation de l’espace de noms **System** à la collection **Imports** d’un **CodeNamespace** appelé `samples` :  
  
 [!code-cpp[CodeDomExample#14](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#14)]
 [!code-csharp[CodeDomExample#14](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#14)]
 [!code-vb[CodeDomExample#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#14)]  
  
#### <a name="linking-code-elements-into-the-object-graph"></a>Liaison d’éléments de code à l’intérieur du graphique d’objet  
 Tous les éléments de code qui forment un graphique CodeDOM doivent être liés au <xref:System.CodeDom.CodeCompileUnit> qui constitue l’élément racine de l’arborescence par une série de références entre des éléments directement référencés à partir des propriétés de l’objet racine du graphique. Affectez un objet à une propriété d’un objet conteneur pour établir une référence à partir de cet objet.  
  
 L’instruction suivante ajoute le **CodeNamespace** `samples` à la propriété de collection **Namespaces** du **CodeCompileUnit** racine.  
  
 [!code-cpp[CodeDomExample#15](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#15)]
 [!code-csharp[CodeDomExample#15](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#15)]
 [!code-vb[CodeDomExample#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#15)]  
  
#### <a name="defining-a-type"></a>Définition d’un type  
 Pour déclarer une classe, une structure, une interface ou une énumération à l’aide de CodeDOM, créez un <xref:System.CodeDom.CodeTypeDeclaration> et nommez-le. L’exemple suivant illustre cette opération à l’aide d’une surcharge de constructeur définissant la propriété **Name** :  
  
 [!code-cpp[CodeDomExample#16](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#16)]
 [!code-csharp[CodeDomExample#16](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#16)]
 [!code-vb[CodeDomExample#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#16)]  
  
 Pour ajouter un type à un espace de noms, ajoutez un <xref:System.CodeDom.CodeTypeDeclaration> représentant ce type à la collection **Types** d’un **CodeNamespace**.  
  
 L’exemple suivant montre comment ajouter une classe nommée `class1` à un **CodeNamespace** nommé `samples` :  
  
 [!code-cpp[CodeDomExample#17](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#17)]
 [!code-csharp[CodeDomExample#17](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#17)]
 [!code-vb[CodeDomExample#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#17)]  
  
#### <a name="adding-class-members-to-a-class"></a>Ajout de membres de classe à une classe  
 L’espace de noms <xref:System.CodeDom> propose divers éléments que vous pouvez utiliser pour représenter des membres de classe. Chaque membre de classe peut être ajouté à la collection **Members** d’un <xref:System.CodeDom.CodeTypeDeclaration>.  
  
#### <a name="defining-a-code-entry-point-method-for-an-executable"></a>Définition d’une méthode de point d’entrée de code pour un exécutable  
 Si vous créez le code d’un programme exécutable, il est nécessaire d’indiquer le point d’entrée du programme en créant un <xref:System.CodeDom.CodeEntryPointMethod> qui représente la méthode à laquelle doit commencer l’exécution du programme.  
  
 L’exemple suivant montre comment définir une méthode de point d’entrée qui contient un <xref:System.CodeDom.CodeMethodInvokeExpression> qui appelle **System.Console.WriteLine** pour imprimer « Hello World! » :  
  
 [!code-cpp[CodeDomExample#18](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#18)]
 [!code-csharp[CodeDomExample#18](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#18)]
 [!code-vb[CodeDomExample#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#18)]  
  
 L’instruction suivante ajoute la méthode de point d’entrée nommée `Start` à la collection **Members** de `class1` :  
  
 [!code-cpp[CodeDomExample#19](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#19)]
 [!code-csharp[CodeDomExample#19](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#19)]
 [!code-vb[CodeDomExample#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#19)]  
  
 À présent, le <xref:System.CodeDom.CodeCompileUnit> nommé `compileUnit` contient le graphique CodeDOM d’un programme Hello World simple. Pour plus d’informations sur la génération et la compilation de code à partir d’un graphique CodeDOM, consultez [Génération de code source et compilation d’un programme à partir d’un graphique CodeDOM](../../../docs/framework/reflection-and-codedom/generating-and-compiling-source-code-from-a-codedom-graph.md).  
  
### <a name="more-information-on-building-a-codedom-graph"></a>Complément d’information sur la génération d’un graphique CodeDOM  
 CodeDOM prend en charge les nombreux types communs d’éléments de code présents dans les langages de programmation compatibles avec le common language runtime. CodeDOM n’a pas été conçu pour fournir des éléments représentant toutes les fonctionnalités de langage de programmation possibles. Le code qui ne peut pas être facilement représenté à l’aide d’éléments CodeDOM peut être encapsulé dans un <xref:System.CodeDom.CodeSnippetExpression>, un <xref:System.CodeDom.CodeSnippetStatement>, un <xref:System.CodeDom.CodeSnippetTypeMember> ou un <xref:System.CodeDom.CodeSnippetCompileUnit>. Toutefois, certains extraits de code ne peuvent pas être traduits automatiquement dans d’autres langages par CodeDOM.  
  
 Pour plus d’informations sur chacun des types CodeDOM, consultez la documentation de référence pour l’espace de noms <xref:System.CodeDom>.  
  
 Pour obtenir un graphique permettant de retrouver rapidement l’élément CodeDOM à utiliser pour représenter un type d’élément de code particulier, consultez [Aide-mémoire de CodeDOM](http://msdn.microsoft.com/library/c77b8bfd-0a32-4e36-b59a-4f687f32c524).
