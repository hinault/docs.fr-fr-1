---
title: "Génération et compilation de code source dynamique"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Code Document Object Model
- System.CodeDom namespace
- language-independent source code modeling
- CodeDOM
- multiple languages supported by CodeDOM
- source code in multiple languages
- languages, multiple language support by CodeDOM
ms.assetid: d077a3e8-bd81-4bdf-b6a3-323857ea30fb
caps.latest.revision: "15"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 535a60aa1a174319a4db3403a64c3998784bbb58
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="dynamic-source-code-generation-and-compilation"></a>Génération et compilation de code source dynamique
Le .NET Framework inclut un mécanisme appelé CodeDOM (Code Document Object Model) qui permet aux développeurs d’émettre du code source pour générer du code source dans plusieurs langages de programmation au moment de l’exécution, en fonction d’un modèle unique qui représente le code à restituer.  
  
 Pour représenter le code source, les éléments CodeDOM sont liés entre eux pour former une structure de données appelée graphique CodeDOM, qui modélise la structure d’un code source.  
  
 L’espace de noms `System.CodeDom` définit les types qui peuvent représenter la structure logique du code source, indépendamment d’un langage de programmation spécifique. L’espace de noms `System.CodeDom.Compiler` définit les types pour la génération du code source à partir des graphiques CodeDOM et la gestion de la compilation du code source dans les langages pris en charge. Les fournisseurs de compilateurs ou les développeurs peuvent étendre l’ensemble des langages pris en charge.  
  
 La modélisation de code source indépendante du langage peut s’avérer précieuse quand un programme a besoin de générer du code source pour un modèle de programme dans plusieurs langages ou pour un langage cible indéterminé. Par exemple, certains concepteurs utilisent le CodeDOM comme interface d’abstraction de langage pour produire du code source dans le langage de programmation approprié, si la prise en charge CodeDOM de ce langage est disponible.  
  
 Le .NET Framework inclut des générateurs et des compilateurs de code pour <xref:Microsoft.CSharp.CSharpCodeProvider>, <xref:Microsoft.JScript.JScriptCodeProvider> et <xref:Microsoft.VisualBasic.VBCodeProvider>.  
  
## <a name="in-this-section"></a>Dans cette section  
 [Utilisation du CodeDOM](../../../docs/framework/reflection-and-codedom/using-the-codedom.md)  
 Décrit les utilisations courantes et illustre la création d’un graphique d’objet simple à l’aide du CodeDOM.  
  
 [Génération de code source et compilation d’un programme à partir d’un graphique CodeDOM](../../../docs/framework/reflection-and-codedom/generating-and-compiling-source-code-from-a-codedom-graph.md)  
 Décrit comment générer du code source et compiler le code généré avec un compilateur externe à l’aide de classes définies dans l’espace de noms `System.CodeDom.Compiler`.  
  
 [Guide pratique pour créer un fichier de documentation XML à l’aide de CodeDOM](../../../docs/framework/reflection-and-codedom/how-to-create-an-xml-documentation-file-using-codedom.md)  
 Décrit comment utiliser CodeDOM pour générer du code avec des commentaires de documentation XML, et compiler le code généré afin qu’il crée la sortie de documentation XML.  
  
 [Guide pratique pour créer une classe à l’aide de CodeDOM](../../../docs/framework/reflection-and-codedom/how-to-create-a-class-using-codedom.md)  
 Décrit comment utiliser CodeDOM pour générer une classe contenant des champs, des propriétés, une méthode, un constructeur et un point d’entrée.  
  
## <a name="reference"></a>Référence  
 <xref:System.CodeDom>  
 Définit les éléments qui représentent des éléments de code dans les langages de programmation qui ciblent le Common Language Runtime.  
  
 <xref:System.CodeDom.Compiler>  
 Définit les interfaces de génération et de compilation du code au moment de l’exécution.  
  
## <a name="related-sections"></a>Rubriques connexes  
 [Aide-mémoire de CodeDOM](http://msdn.microsoft.com/library/c77b8bfd-0a32-4e36-b59a-4f687f32c524)  
 Fournit aux développeurs un moyen de trouver rapidement des éléments CodeDOM qui représentent des éléments du code source.
