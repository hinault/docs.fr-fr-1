---
title: "Guide pratique pour définir et exécuter des méthodes dynamiques"
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
- reflection emit, dynamic methods
- dynamic methods
ms.assetid: 07d08a99-62c5-4254-bce2-2a75e55a18ab
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 7c2b3f1707aab1f83d8f8c6a06bc2efa909134d5
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-define-and-execute-dynamic-methods"></a>Guide pratique pour définir et exécuter des méthodes dynamiques
Les procédures suivantes montrent comment définir et exécuter une méthode dynamique simple et une méthode dynamique liée à une instance d’une classe. Pour plus d’informations sur les méthodes dynamiques, consultez la classe <xref:System.Reflection.Emit.DynamicMethod> et [Scénarios de méthodes dynamiques avec Émission de réflexion](http://msdn.microsoft.com/library/7c27ea3d-0f24-4bf3-8ceb-f49d33faca5e).  
  
### <a name="to-define-and-execute-a-dynamic-method"></a>Pour définir et exécuter une méthode dynamique  
  
1.  Déclarez un type délégué pour exécuter la méthode. Vous pouvez utiliser un délégué générique pour réduire le nombre de types délégués que vous devez déclarer. Le code suivant déclare deux types délégués qui peuvent être utilisés pour la méthode `SquareIt`, et l’un d’eux est générique.  
  
     [!code-cpp[DynamicMethodHowTo#2](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#2)]
     [!code-csharp[DynamicMethodHowTo#2](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#2)]
     [!code-vb[DynamicMethodHowTo#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#2)]  
  
2.  Créez un tableau qui spécifie les types de paramètre de la méthode dynamique. Dans cet exemple, le seul paramètre est un `int` (`Integer` en Visual Basic). Le tableau n’a donc qu’un seul élément.  
  
     [!code-cpp[DynamicMethodHowTo#3](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#3)]
     [!code-csharp[DynamicMethodHowTo#3](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#3)]
     [!code-vb[DynamicMethodHowTo#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#3)]  
  
3.  Créer un <xref:System.Reflection.Emit.DynamicMethod>. Dans cet exemple, la méthode se nomme `SquareIt`.  
  
    > [!NOTE]
    >  Il n’est pas nécessaire de nommer les méthodes dynamiques. Elles ne peuvent pas être appelées par nom. Plusieurs méthodes dynamiques peuvent avoir le même nom. Toutefois, le nom apparaît dans les piles des appels et peut être utile pour le débogage.  
  
     Le type de la valeur de retour est spécifié comme `long`. La méthode est associée au module qui contient la classe `Example`, qui contient l’exemple de code. Vous pourriez spécifier n’importe quel module chargé. La méthode dynamique agit comme une méthode `static` au niveau du module (`Shared` en Visual Basic).  
  
     [!code-cpp[DynamicMethodHowTo#4](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#4)]
     [!code-csharp[DynamicMethodHowTo#4](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#4)]
     [!code-vb[DynamicMethodHowTo#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#4)]  
  
4.  Émettez le corps de méthode. Dans cet exemple, un objet <xref:System.Reflection.Emit.ILGenerator> est utilisé pour émettre le code MSIL (Microsoft Intermediate Language). Vous pourriez également utiliser un objet <xref:System.Reflection.Emit.DynamicILInfo> conjointement avec des générateurs de code non managé pour émettre le corps de méthode pour un <xref:System.Reflection.Emit.DynamicMethod>.  
  
     Le code MSIL de cet exemple charge l’argument (qui est un `int`) dans la pile, le convertit en `long`, duplique le `long` et multiplie les deux nombres. Cela laisse le résultat au carré sur la pile, et il suffit à la méthode de retourner.  
  
     [!code-cpp[DynamicMethodHowTo#5](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#5)]
     [!code-csharp[DynamicMethodHowTo#5](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#5)]
     [!code-vb[DynamicMethodHowTo#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#5)]  
  
5.  Créez une instance du délégué (déclaré à l’étape 1) qui représente la méthode dynamique en appelant la méthode <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A>. La création du délégué achève la méthode, et toute tentative supplémentaire de changement de la méthode (par exemple l’ajout de code MSIL) est ignorée. Le code suivant crée le délégué et l’appelle, à l’aide d’un délégué générique.  
  
     [!code-cpp[DynamicMethodHowTo#6](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#6)]
     [!code-csharp[DynamicMethodHowTo#6](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#6)]
     [!code-vb[DynamicMethodHowTo#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#6)]  
  
### <a name="to-define-and-execute-a-dynamic-method-that-is-bound-to-an-object"></a>Pour définir et exécuter une méthode dynamique liée à un objet  
  
1.  Déclarez un type délégué pour exécuter la méthode. Vous pouvez utiliser un délégué générique pour réduire le nombre de types délégués que vous devez déclarer. Le code suivant déclare un type délégué générique qui peut être utilisé pour exécuter n’importe quelle méthode avec un paramètre et une valeur de retour, ou une méthode avec deux paramètres et une valeur de retour si le délégué est lié à un objet.  
  
     [!code-cpp[DynamicMethodHowTo#12](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#12)]
     [!code-csharp[DynamicMethodHowTo#12](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#12)]
     [!code-vb[DynamicMethodHowTo#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#12)]  
  
2.  Créez un tableau qui spécifie les types de paramètre de la méthode dynamique. Si le délégué représentant la méthode doit être lié à un objet, le premier paramètre doit correspondre au type auquel le délégué est lié. Cet exemple contient deux paramètres, de type `Example` et `int` (`Integer` en Visual Basic).  
  
     [!code-cpp[DynamicMethodHowTo#13](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#13)]
     [!code-csharp[DynamicMethodHowTo#13](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#13)]
     [!code-vb[DynamicMethodHowTo#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#13)]  
  
3.  Créer un <xref:System.Reflection.Emit.DynamicMethod>. Dans cet exemple, la méthode n’a pas de nom. Le type de la valeur de retour est spécifié comme `int` (`Integer` en Visual Basic). La méthode a accès aux membres privés et protégés de la classe `Example`.  
  
     [!code-cpp[DynamicMethodHowTo#14](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#14)]
     [!code-csharp[DynamicMethodHowTo#14](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#14)]
     [!code-vb[DynamicMethodHowTo#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#14)]  
  
4.  Émettez le corps de méthode. Dans cet exemple, un objet <xref:System.Reflection.Emit.ILGenerator> est utilisé pour émettre le code MSIL (Microsoft Intermediate Language). Vous pourriez également utiliser un objet <xref:System.Reflection.Emit.DynamicILInfo> conjointement avec des générateurs de code non managé pour émettre le corps de méthode pour un <xref:System.Reflection.Emit.DynamicMethod>.  
  
     Le code MSIL de cet exemple charge le premier argument, qui est une instance de la classe `Example`, et l’utilise pour charger la valeur d’un champ d’instance privé de type `int`. Le deuxième argument est chargé, et les deux nombres sont multipliés. Si le résultat est supérieur à `int`, la valeur est tronquée et les bits les plus significatifs sont ignorés. La méthode retourne, avec la valeur de retour sur la pile.  
  
     [!code-cpp[DynamicMethodHowTo#15](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#15)]
     [!code-csharp[DynamicMethodHowTo#15](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#15)]
     [!code-vb[DynamicMethodHowTo#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#15)]  
  
5.  Créez une instance du délégué (déclaré à l’étape 1) qui représente la méthode dynamique en appelant la surcharge de méthode <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%28System.Type%2CSystem.Object%29>. La création du délégué achève la méthode, et toute tentative supplémentaire de changement de la méthode (par exemple l’ajout de code MSIL) est ignorée.  
  
    > [!NOTE]
    >  Vous pouvez appeler la méthode <xref:System.Reflection.Emit.DynamicMethod.CreateDelegate%2A> plusieurs fois afin de créer des délégués liés à d’autres instances du type cible.  
  
     Le code suivant lie la méthode à une nouvelle instance de la classe `Example` dont le champ de test privé a la valeur 42. Autrement dit, chaque fois que le délégué est appelé, l’instance de `Example` est passée au premier paramètre de la méthode.  
  
     Le délégué `OneParameter` est utilisé, car le premier paramètre de la méthode reçoit toujours l’instance de `Example`. Quand le délégué est appelé, seul le deuxième paramètre est nécessaire.  
  
     [!code-cpp[DynamicMethodHowTo#16](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#16)]
     [!code-csharp[DynamicMethodHowTo#16](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#16)]
     [!code-vb[DynamicMethodHowTo#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#16)]  
  
## <a name="example"></a>Exemple  
 L’exemple de code suivant montre une méthode dynamique simple et une méthode dynamique liée à une instance d’une classe.  
  
 La méthode dynamique simple prend un argument, un entier 32 bits, et retourne le carré 64 bits de cet entier. Un délégué générique est utilisé pour appeler la méthode.  
  
 La deuxième méthode dynamique a deux paramètres, de type `Example` et `int` (`Integer` en Visual Basic). Quand la méthode dynamique a été créée, elle est liée à une instance de `Example`, à l’aide d’un délégué générique qui a un argument de type `int`. Le délégué n’a pas d’argument de type `Example`, car le premier paramètre de la méthode reçoit toujours l’instance liée de `Example`. Quand le délégué est appelé, seul l’argument `int` est fourni. Cette méthode dynamique accède à un champ privé de la classe `Example` et retourne le produit du champ privé et l’argument `int`.  
  
 L’exemple de code définit des délégués qui peuvent être utilisés pour exécuter les méthodes.  
  
 [!code-cpp[DynamicMethodHowTo#1](../../../samples/snippets/cpp/VS_Snippets_CLR/DynamicMethodHowTo/cpp/source.cpp#1)]
 [!code-csharp[DynamicMethodHowTo#1](../../../samples/snippets/csharp/VS_Snippets_CLR/DynamicMethodHowTo/cs/source.cs#1)]
 [!code-vb[DynamicMethodHowTo#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/DynamicMethodHowTo/vb/source.vb#1)]  
  
## <a name="compiling-the-code"></a>Compilation du code  
  
-   Le code contient les instructions `using` C# (`Imports` en Visual Basic) nécessaires à la compilation.  
  
-   Aucune référence d’assembly supplémentaire n’est nécessaire.  
  
-   Compilez le code sur la ligne de commande à l’aide de csc.exe, vbc.exe ou cl.exe. Pour compiler le code dans Visual Studio, placez-le dans un modèle de projet d’application console.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Reflection.Emit.DynamicMethod>  
 [Utilisation de l’émission de réflexion](http://msdn.microsoft.com/library/ccc6540d-0e2c-4d89-b456-eb7353f9e9ac)  
 [Scénarios de méthodes dynamiques avec Émission de réflexion](http://msdn.microsoft.com/library/7c27ea3d-0f24-4bf3-8ceb-f49d33faca5e)
