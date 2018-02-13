---
title: "Guide pratique pour définir un type générique avec l'émission de réflexion"
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
- generics [.NET Framework], reflection emit
- generics [.NET Framework], dynamic types
- reflection emit, generic types
ms.assetid: 07d5f01a-7b5b-40ea-9b15-f21561098fe4
caps.latest.revision: "14"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: d6096a54c6a530035bd32c24d427ba047f905476
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-define-a-generic-type-with-reflection-emit"></a>Guide pratique pour définir un type générique avec l'émission de réflexion
Cette rubrique montre comment créer un type générique simple avec deux paramètres de type, comment appliquer des contraintes de classe, des contraintes d’interface et des contraintes spéciales aux paramètres de type, et comment créer des membres qui utilisent les paramètres de type de la classe comme types de paramètres et types de retour.  
  
> [!IMPORTANT]
>  Une méthode n’est pas générique simplement car elle appartient à un type générique et utilise les paramètres de type de ce type. Une méthode est générique uniquement si elle a sa propre liste de paramètres de type. La plupart des méthodes sur les types génériques ne sont pas génériques, comme dans cet exemple. Pour obtenir un exemple d’émission de méthode générique, consultez [Guide pratique pour définir une méthode générique avec l’émission de réflexion](../../../docs/framework/reflection-and-codedom/how-to-define-a-generic-method-with-reflection-emit.md).  
  
### <a name="to-define-a-generic-type"></a>Pour définir un type générique  
  
1.  Définissez un assembly dynamique nommé `GenericEmitExample1`. Dans cet exemple, l’assembly est exécuté et enregistré sur le disque. <xref:System.Reflection.Emit.AssemblyBuilderAccess.RunAndSave?displayProperty=nameWithType> est donc spécifié.  
  
     [!code-cpp[EmitGenericType#2](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#2)]
     [!code-csharp[EmitGenericType#2](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#2)]
     [!code-vb[EmitGenericType#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#2)]  
  
2.  Définissez un module dynamique. Un assembly est composé de modules exécutables. Pour un assembly à module unique, le nom du module est identique au nom de l’assembly, et le nom de fichier est le nom du module suivi d’une extension.  
  
     [!code-cpp[EmitGenericType#3](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#3)]
     [!code-csharp[EmitGenericType#3](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#3)]
     [!code-vb[EmitGenericType#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#3)]  
  
3.  Définissez une classe. Dans cet exemple, la classe se nomme `Sample`.  
  
     [!code-cpp[EmitGenericType#4](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#4)]
     [!code-csharp[EmitGenericType#4](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#4)]
     [!code-vb[EmitGenericType#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#4)]  
  
4.  Définissez les paramètres de type générique de `Sample` en passant un tableau de chaînes contenant les noms des paramètres à la méthode <xref:System.Reflection.Emit.TypeBuilder.DefineGenericParameters%2A?displayProperty=nameWithType>. Cela fait de la classe un type générique. La valeur de retour est un tableau d’objets <xref:System.Reflection.Emit.GenericTypeParameterBuilder> représentant les paramètres de type, qui peut être utilisé dans votre code émis.  
  
     Dans le code suivant, `Sample` devient un type générique avec les paramètres de type `TFirst` et `TSecond`. Pour faciliter la lecture du code, chaque <xref:System.Reflection.Emit.GenericTypeParameterBuilder> est placé dans une variable du même nom que le paramètre de type.  
  
     [!code-cpp[EmitGenericType#5](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#5)]
     [!code-csharp[EmitGenericType#5](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#5)]
     [!code-vb[EmitGenericType#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#5)]  
  
5.  Ajoutez des contraintes spéciales aux paramètres de type. Dans cet exemple, le paramètre de type `TFirst` est limité aux types qui ont des constructeurs sans paramètre et aux types référence.  
  
     [!code-cpp[EmitGenericType#6](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#6)]
     [!code-csharp[EmitGenericType#6](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#6)]
     [!code-vb[EmitGenericType#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#6)]  
  
6.  Ajoutez éventuellement des contraintes de classe et d’interface aux paramètres de type. Dans cet exemple, le paramètre de type `TFirst` est limité aux types qui dérivent de la classe de base représentée par l’objet <xref:System.Type> contenu dans la variable `baseType`, et qui implémentent les interfaces dont les types sont contenus dans les variables `interfaceA` et `interfaceB`. Pour plus d’informations sur la déclaration et l’assignation de ces variables, consultez l’exemple de code.  
  
     [!code-cpp[EmitGenericType#7](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#7)]
     [!code-csharp[EmitGenericType#7](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#7)]
     [!code-vb[EmitGenericType#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#7)]  
  
7.  Définissez un champ. Dans cet exemple, le type du champ est spécifié par le paramètre de type `TFirst`. <xref:System.Reflection.Emit.GenericTypeParameterBuilder> dérive de <xref:System.Type>. Vous pouvez donc utiliser des paramètres de type générique partout où un type peut être utilisé.  
  
     [!code-cpp[EmitGenericType#21](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#21)]
     [!code-csharp[EmitGenericType#21](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#21)]
     [!code-vb[EmitGenericType#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#21)]  
  
8.  Définissez une méthode qui utilise les paramètres de type du type générique. Notez que ces méthodes ne sont génériques que si elles ont leurs propres listes de paramètres de type. Le code suivant définit une méthode `static` (`Shared` en Visual Basic) qui prend un tableau de `TFirst` et retourne un `List<TFirst>` (`List(Of TFirst)` en Visual Basic) contenant tous les éléments du tableau. Pour définir cette méthode, vous devez créer le type `List<TFirst>` en appelant <xref:System.Type.MakeGenericType%2A> sur la définition de type générique, `List<T>`. (Le `T` est omis quand vous utilisez l’opérateur `typeof` (`GetType` en Visual Basic) pour obtenir la définition de type générique.) Le type de paramètre est créé à l’aide de la méthode <xref:System.Type.MakeArrayType%2A>.  
  
     [!code-cpp[EmitGenericType#22](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#22)]
     [!code-csharp[EmitGenericType#22](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#22)]
     [!code-vb[EmitGenericType#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#22)]  
  
9. Émettez le corps de méthode. Le corps de la méthode se compose de trois opcodes qui chargent le tableau d’entrée sur la pile, appellent le constructeur `List<TFirst>` qui accepte `IEnumerable<TFirst>` (qui fait tout le travail nécessaire pour placer les éléments d’entrée dans la liste), et retournent (en laissant le nouvel objet <xref:System.Collections.Generic.List%601> sur la pile). La partie difficile de l’émission de ce code consiste à obtenir le constructeur.  
  
     La méthode <xref:System.Type.GetConstructor%2A> n’étant pas prise en charge sur un <xref:System.Reflection.Emit.GenericTypeParameterBuilder>, vous ne pouvez pas obtenir directement le constructeur de `List<TFirst>`. Vous devez d’abord obtenir le constructeur de la définition de type générique `List<T>`, puis appeler une méthode qui le convertit en constructeur de `List<TFirst>` correspondant.  
  
     Le constructeur utilisé pour cet exemple de code prend un `IEnumerable<T>`. Notez cependant qu’il ne s’agit pas de la définition de type générique de l’interface générique <xref:System.Collections.Generic.IEnumerable%601>. Au lieu de cela, le paramètre de type `T` de `List<T>` doit remplacer le paramètre de type `T` de `IEnumerable<T>`. (Cela peut paraître déroutant uniquement car les deux types ont des paramètres de type nommés `T`. C’est pourquoi cet exemple de code utilise les noms `TFirst` et `TSecond`.) Pour obtenir le type de l’argument du constructeur, commencez avec la définition de type générique `IEnumerable<T>` et appelez <xref:System.Type.MakeGenericType%2A> avec le premier paramètre de type générique de `List<T>`. La liste d’arguments de constructeur doit être passée en tant que tableau, avec un seul argument dans ce cas.  
  
    > [!NOTE]
    >  La définition de type générique est exprimée en tant que `IEnumerable<>` quand vous utilisez l’opérateur `typeof` en C#, ou `IEnumerable(Of )` quand vous utilisez l’opérateur `GetType` en Visual Basic.  
  
     Il est désormais possible d’obtenir le constructeur de `List<T>` en appelant <xref:System.Type.GetConstructor%2A> sur la définition de type générique. Pour convertir ce constructeur en constructeur correspondant de `List<TFirst>`, transmettez `List<TFirst>` et le constructeur de `List<T>` à la méthode statique <xref:System.Reflection.Emit.TypeBuilder.GetConstructor%28System.Type%2CSystem.Reflection.ConstructorInfo%29?displayProperty=nameWithType>.  
  
     [!code-cpp[EmitGenericType#23](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#23)]
     [!code-csharp[EmitGenericType#23](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#23)]
     [!code-vb[EmitGenericType#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#23)]  
  
10. Créez le type et enregistrez le fichier.  
  
     [!code-cpp[EmitGenericType#8](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#8)]
     [!code-csharp[EmitGenericType#8](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#8)]
     [!code-vb[EmitGenericType#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#8)]  
  
11. Appelez la méthode. `ExampleMethod` n’est pas générique, mais le type auquel elle appartient est générique. Ainsi, pour obtenir un <xref:System.Reflection.MethodInfo> qui peut être appelé, vous devez créer un type construit à partir de la définition de type pour `Sample`. Le type construit utilise la classe `Example`, ce qui satisfait aux contraintes sur `TFirst` car il s’agit d’un type référence avec un constructeur sans paramètre par défaut, et la classe `ExampleDerived` qui satisfait aux contraintes sur `TSecond`. (Le code de `ExampleDerived` se trouve dans la section Exemple de code.) Ces deux types sont passés à <xref:System.Type.MakeGenericType%2A> pour créer le type construit. <xref:System.Reflection.MethodInfo> est ensuite obtenu à l’aide de la méthode <xref:System.Type.GetMethod%2A>.  
  
     [!code-cpp[EmitGenericType#9](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#9)]
     [!code-csharp[EmitGenericType#9](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#9)]
     [!code-vb[EmitGenericType#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#9)]  
  
12. Le code suivant crée un tableau d’objets `Example`, place ce tableau dans un tableau de type <xref:System.Object> représentant les arguments de la méthode à appeler, puis les passe à la méthode <xref:System.Reflection.MethodBase.Invoke%28System.Object%2CSystem.Object%5B%5D%29>. Le premier argument de la méthode <xref:System.Reflection.MethodBase.Invoke%2A> est une référence null car la méthode est `static`.  
  
     [!code-cpp[EmitGenericType#10](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#10)]
     [!code-csharp[EmitGenericType#10](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#10)]
     [!code-vb[EmitGenericType#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#10)]  
  
## <a name="example"></a>Exemple  
 L’exemple de code suivant définit une classe nommée `Sample`, ainsi qu’une classe de base et deux interfaces. Le programme définit deux paramètres de type générique pour `Sample`, ce qui en fait un type générique. Les paramètres de type sont la seule chose qui rend un type générique. Le programme l’indique en affichant un message de test avant et après la définition des paramètres de type.  
  
 Le paramètre de type `TSecond` sert à illustrer les contraintes de classe et d’interface, à l’aide des interfaces et de la classe de base, et le paramètre de type `TFirst` sert à illustrer des contraintes spéciales.  
  
 L’exemple de code définit un champ et une méthode à l’aide des paramètres de type de la classe pour le type de champ et pour le paramètre et le type de retour de la méthode.  
  
 Une fois la classe `Sample` créée, la méthode est appelée.  
  
 Le programme inclut une méthode qui répertorie les informations sur un type générique, et une méthode qui répertorie les contraintes spéciales sur un paramètre de type. Ces méthodes sont utilisées pour afficher des informations sur la classe `Sample` finie.  
  
 Le programme enregistre le module fini sur le disque en tant que `GenericEmitExample1.dll`. Ainsi, vous pouvez l’ouvrir avec [Ildasm.exe (désassembleur IL)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) et examiner le code MSIL de la classe `Sample`.  
  
 [!code-cpp[EmitGenericType#1](../../../samples/snippets/cpp/VS_Snippets_CLR/EmitGenericType/CPP/source.cpp#1)]
 [!code-csharp[EmitGenericType#1](../../../samples/snippets/csharp/VS_Snippets_CLR/EmitGenericType/CS/source.cs#1)]
 [!code-vb[EmitGenericType#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/EmitGenericType/VB/source.vb#1)]  
  
## <a name="compiling-the-code"></a>Compilation du code  
  
-   Le code contient les instructions `using` C# (`Imports` en Visual Basic) nécessaires à la compilation.  
  
-   Aucune référence d’assembly supplémentaire n’est nécessaire.  
  
-   Compilez le code sur la ligne de commande à l’aide de csc.exe, vbc.exe ou cl.exe. Pour compiler le code dans Visual Studio, placez-le dans un modèle de projet d’application console.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Reflection.Emit.GenericTypeParameterBuilder>  
 [Utilisation de l’émission de réflexion](http://msdn.microsoft.com/library/ccc6540d-0e2c-4d89-b456-eb7353f9e9ac)  
 [Scénarios d’assemblys dynamiques avec émission de réflexion](http://msdn.microsoft.com/library/e1cc6750-e20f-473b-bb4e-f43bc66aecce)
