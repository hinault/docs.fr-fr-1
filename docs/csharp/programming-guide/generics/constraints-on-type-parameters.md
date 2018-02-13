---
title: "Contraintes sur les paramètres de type (Guide de programmation C#)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
helpviewer_keywords:
- generics [C#], type constraints
- type constraints [C#]
- type parameters [C#], constraints
- unbound type parameter [C#]
ms.assetid: 141b003e-1ddb-4e1c-bcb2-e1c3870e6a51
caps.latest.revision: "41"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 6f7c80acdb3815af4b5d545297894778029a9104
ms.sourcegitcommit: 8bde7a3432f30fc771079744955c75c58c4eb393
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/20/2018
---
# <a name="constraints-on-type-parameters-c-programming-guide"></a>Contraintes sur les paramètres de type (Guide de programmation C#)
Quand vous définissez une classe générique, vous pouvez appliquer des restrictions aux genres de types que le code client peut utiliser pour les arguments de type lorsqu’il instancie votre classe. Si le code client essaie d’instancier votre classe à l’aide d’un type qui n’est pas autorisé par une contrainte, il en résulte une erreur de compilation. Ces restrictions sont appelées des contraintes. Les contraintes sont spécifiées à l’aide du mot clé contextuel `where`. Le tableau suivant liste les six types de contraintes :  
  
|Contrainte|Description|  
|----------------|-----------------|  
|`where T: struct`|L’argument de type doit être un type valeur. Tout type valeur, excepté <xref:System.Nullable>, peut être spécifié. Consultez [Utilisation de types Nullable](../../../csharp/programming-guide/nullable-types/using-nullable-types.md) pour plus d’informations.|  
|`where T : class`|L’argument de type doit être un type référence. Cela s’applique également à tout type de classe, d’interface, de délégué ou de tableau.|  
|`where T : new()`|L’argument de type doit avoir un constructeur sans paramètre public. Quand vous utilisez la contrainte `new()` avec d’autres contraintes, elle doit être spécifiée en dernier.|  
|`where T : `*\<nom_classe_de_base>*|L’argument de type doit être la classe de base spécifiée ou en dériver.|  
|`where T : `*\<nom_interface>*|L’argument de type doit être ou implémenter l’interface spécifiée. Plusieurs contraintes d’interface peuvent être spécifiées. L’interface qui impose les contraintes peut également être générique.|  
|`where T : U`|L’argument de type fourni pour T doit être l’argument fourni pour U ou en dériver.|  
  
## <a name="why-use-constraints"></a>Pourquoi utiliser des contraintes ?  
 Si vous souhaitez examiner un élément dans une liste générique afin de déterminer s’il est valide ou de le comparer à un autre élément, le compilateur doit avoir une certaine garantie que l’opérateur ou la méthode qu’il doit appeler par tous les arguments de type pouvant être spécifiés par le code client est pris en charge. Cette garantie est obtenue en appliquant une ou plusieurs contraintes à votre définition de classe générique. Par exemple, la contrainte de classe de base indique au compilateur que seuls les objets de ce type ou dérivés de ce type seront utilisés comme arguments de type. Une fois que le compilateur a cette garantie, il peut autoriser les méthodes de ce type à être appelées dans la classe générique. Les contraintes sont appliquées à l’aide du mot clé contextuel `where`. L’exemple de code suivant illustre la fonctionnalité que nous pouvons ajouter à la classe `GenericList<T>` (dans [Introduction aux génériques](../../../csharp/programming-guide/generics/introduction-to-generics.md)) en appliquant une contrainte de classe de base.  
  
 [!code-csharp[csProgGuideGenerics#11](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_1.cs)]  
  
 La contrainte permet à la classe générique d’utiliser la propriété `Employee.Name`, car il est garanti que tous les éléments de type T sont soit un objet `Employee`, soit un objet qui hérite d’`Employee`.  
  
 Plusieurs contraintes peuvent être appliquées au même paramètre de type, et les contraintes elles-mêmes peuvent être des types génériques, comme suit :  
  
 [!code-csharp[csProgGuideGenerics#12](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_2.cs)]  
  
 En limitant le paramètre de type, vous augmentez le nombre d’opérations et d’appels de méthode autorisés au niveau de celui pris en charge par le type de contrainte et tous les types dans sa hiérarchie d’héritage. Par conséquent, en concevant des classes ou des méthodes génériques, si vous exécutez des opérations sur les membres génériques au-delà de la simple assignation ou que vous appelez des méthodes non prises en charge par `System.Object`, vous devez appliquer des contraintes au paramètre de type.  
  
 En appliquant la contrainte `where T : class`, évitez d’utiliser les opérateurs `==` et `!=` sur le paramètre de type, car ces opérateurs testent uniquement l’identité des références, et non l’égalité des valeurs. C’est le cas même si ces opérateurs sont surchargés dans un type qui est utilisé comme argument. Le code suivant illustre ce point ; la sortie a la valeur false même si la classe <xref:System.String> surcharge l’opérateur `==`.  
  
 [!code-csharp[csProgGuideGenerics#13](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_3.cs)]  
  
 La raison à ce comportement réside dans le fait que le compilateur, au moment de la compilation, sait uniquement que T est un type référence et doit par conséquent utiliser les opérateurs par défaut, valides pour tous les types référence. Si vous devez tester l’égalité des valeurs, il est recommandé d’appliquer également la contrainte `where T : IComparable<T>` et d’implémenter cette interface dans toute classe qui sera utilisée pour construire la classe générique.  
  
## <a name="constraining-multiple-parameters"></a>Utilisation de contraintes dans plusieurs paramètres  
 Vous pouvez appliquer des contraintes à plusieurs paramètres et plusieurs contraintes à un seul paramètre, comme indiqué dans l’exemple suivant :  
  
 [!code-csharp[csProgGuideGenerics#64](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_4.cs)]  
  
## <a name="unbounded-type-parameters"></a>Paramètres de type unbounded  
 Les paramètres de type qui n’ont aucune contrainte, tels que T dans la classe publique `SampleClass<T>{}`, sont appelés paramètres de type unbounded. Les paramètres de type unbounded obéissent aux règles suivantes :  
  
-   Les opérateurs `!=` et `==` ne peuvent pas être utilisés, car il n’est pas garanti que l’argument de type concret les prendra en charge.  
  
-   Ils peuvent être convertis vers et depuis `System.Object` ou être explicitement convertis vers tout type d’interface.  
  
-   Vous pouvez les comparer à [null](../../../csharp/language-reference/keywords/null.md). Si un paramètre unbounded est comparé à `null`, la comparaison retourne toujours la valeur false si l’argument de type est un type valeur.  
  
## <a name="type-parameters-as-constraints"></a>Paramètres de type en tant que contraintes  
 L’utilisation d’un paramètre de type générique comme contrainte est utile quand une fonction membre dotée de son propre paramètre de type doit contraindre ce paramètre au paramètre du type conteneur, comme le montre l’exemple suivant :  
  
 [!code-csharp[csProgGuideGenerics#14](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_5.cs)]  
  
 Dans l’exemple précédent, `T` est une contrainte de type dans le contexte de la méthode `Add` et un paramètre de type unbounded dans le contexte de la classe `List`.  
  
 Les paramètres de type peuvent également être utilisés comme contraintes dans les définitions de classes génériques. Notez que le paramètre de type doit être déclaré entre crochets pointus, ainsi que tous les autres paramètres de type :  
  
 [!code-csharp[csProgGuideGenerics#15](../../../csharp/programming-guide/generics/codesnippet/CSharp/constraints-on-type-parameters_6.cs)]  
  
 L’utilité des paramètres de type en tant que contraintes avec les classes génériques est très limitée, car le compilateur ne peut rien deviner à propos du paramètre de type en dehors du fait qu’il dérive de `System.Object`. Utilisez des paramètres de type en tant que contraintes sur les classes génériques dans les scénarios dans lesquels vous souhaitez mettre en application une relation d’héritage entre deux paramètres de type.  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Collections.Generic>  
 [Guide de programmation C#](../../../csharp/programming-guide/index.md)  
 [Introduction aux génériques](../../../csharp/programming-guide/generics/introduction-to-generics.md)  
 [Classes génériques](../../../csharp/programming-guide/generics/generic-classes.md)  
 [new, contrainte](../../../csharp/language-reference/keywords/new-constraint.md)
