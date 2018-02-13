---
title: "Guide pratique pour implémenter et appeler une méthode d’extension personnalisée (Guide de programmation C#)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
helpviewer_keywords: extension methods [C#], implementing and calling
ms.assetid: 7dab2a56-cf8e-4a47-a444-fe610a02772a
caps.latest.revision: "15"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: a277412c69d26f20721381d9cfa839c7f082f2f2
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-implement-and-call-a-custom-extension-method-c-programming-guide"></a>Guide pratique pour implémenter et appeler une méthode d’extension personnalisée (Guide de programmation C#)
Cette rubrique montre comment implémenter vos propres méthodes d’extension pour n’importe quel type .NET. Le code client peut utiliser vos méthodes d’extension en ajoutant une référence à la DLL qui les contient, et en ajoutant une directive [using](../../../csharp/language-reference/keywords/using-directive.md) qui spécifie l’espace de noms dans lequel les méthodes d’extension sont définies.  
  
## <a name="to-define-and-call-the-extension-method"></a>Pour définir et appeler la méthode d’extension  
  
1.  Définissez une [classe](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md) statique pour contenir la méthode d’extension.  
  
     La classe doit être visible par le code client. Pour plus d’informations sur les règles d’accessibilité, consultez [Modificateurs d’accès](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md).  
  
2.  Implémentez la méthode d’extension en tant que méthode statique avec au moins la même visibilité que la classe conteneur.  
  
3.  Le premier paramètre de la méthode spécifie le type sur lequel la méthode opère. Il doit être précédé du modificateur [this](../../../csharp/language-reference/keywords/this.md).  
  
4.  Dans le code appelant, ajoutez une directive `using` pour spécifier l’[espace de noms](../../../csharp/language-reference/keywords/namespace.md) qui contient la classe de méthode d’extension.  
  
5.  Appelez les méthodes comme s’il s’agissait de méthodes d’instance sur le type.  
  
     Notez que le premier paramètre n’est pas spécifié par le code appelant, car il représente le type sur lequel l’opérateur est appliqué, et le compilateur connaît déjà le type de votre objet. Vous devez fournir des arguments uniquement pour les paramètres 2 à `n`.  
  
## <a name="example"></a>Exemple  
 L’exemple suivant implémente une méthode d’extension nommée `WordCount` dans la classe `CustomExtensions.StringExtension`. La méthode opère sur la classe <xref:System.String>, qui est spécifiée comme premier paramètre de méthode. L’espace de noms `CustomExtensions` est importé dans l’espace de noms d’application, et la méthode est appelée à l’intérieur de la méthode `Main`.  
  
 [!code-csharp[csProgGuideExtensionMethods#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-implement-and-call-a-custom-extension-method_1.cs)]  
  
## <a name="compiling-the-code"></a>Compilation du code  
 Pour exécuter ce code, copiez et collez-le dans un projet d’application console Visual C# qui a été créé dans [!INCLUDE[vs_current_short](~/includes/vs-current-short-md.md)]. Par défaut, ce projet cible la version 3.5 du [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)], et il a une référence à System.Core.dll et une directive `using` pour System.Linq. Si un ou plusieurs de ces éléments sont manquants dans le projet, vous pouvez les ajouter manuellement.  
  
## <a name="net-framework-security"></a>Sécurité .NET Framework  
 Les méthodes d’extension ne présentent aucune faille de sécurité spécifique. Elles ne peuvent jamais être utilisées pour emprunter l’identité des méthodes existantes sur un type, car toutes les collisions de noms sont résolues en faveur de l’instance ou de la méthode statique définie par le type lui-même. Les méthodes d’extension ne peuvent pas accéder à des données privées dans la classe étendue.  
  
## <a name="see-also"></a>Voir aussi  
 [Guide de programmation C#](../../../csharp/programming-guide/index.md)  
 [Méthodes d’extension](../../../csharp/programming-guide/classes-and-structs/extension-methods.md)  
 [LINQ (Language Integrated Query)](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)  
 [Classes statiques et membres de classe statique](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)  
 [protected](../../../csharp/language-reference/keywords/protected.md)  
 [internal](../../../csharp/language-reference/keywords/internal.md)  
 [public](../../../csharp/language-reference/keywords/public.md)  
 [this](../../../csharp/language-reference/keywords/this.md)  
 [namespace](../../../csharp/language-reference/keywords/namespace.md)
