---
title: Tuples dans Visual Basic
ms.custom: 
ms.date: 04/23/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- tuples [Visual Basic]
ms.assetid: 3e66cd1b-3432-4e1d-8c37-5ebacae8f53f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2653b9dc8a6ecbcb718c20be8bd6275edf4cfb6e
ms.sourcegitcommit: be1fb5d9447ad459bef22b91a91c72e3e0b2d916
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/09/2018
---
# <a name="tuples-visual-basic"></a>Tuples (Visual Basic)

À partir de Visual Basic 2017, du langage Visual Basic propose une prise en charge intégrée pour les tuples qui permet de créer des tuples et accéder aux éléments de tuples plus facile. Un tuple est une structure de données de légers qui a un nombre spécifique et une séquence de valeurs. Lorsque vous instanciez le tuple, vous définissez le nombre et le type de données de chaque valeur (ou élément). Par exemple, un objet de 2 tuples (ou paire) a deux éléments. La première peut être un `Boolean` valeur, alors que le second est un `String`. Étant donné que les tuples permettent de stocker plusieurs valeurs dans un objet unique, ils sont souvent utilisés comme une solution légère pour retourner plusieurs valeurs à partir d’une méthode.

> [!IMPORTANT]
> Prise en charge de tuple nécessite le <xref:System.ValueTuple> type. Si le 4.7 Framework .NET n’est pas installé, vous devez ajouter le package NuGet `System.ValueTuple`, qui est disponible sur la galerie NuGet. Sans ce package, vous pouvez obtenir une erreur de compilation semblable à « Type prédéfini 'ValueTuple(Of,,,)' n’est pas défini ou importé. »

## <a name="instantiating-and-using-a-tuple"></a>Instanciation et l’utilisation d’un tuple

Vous instanciez un tuple en mettant ses parenthèses de messagerie instantanée de valeurs délimitées par des virgules. Chacune de ces valeurs devient alors un champ du tuple. Par exemple, le code suivant définit une triple (ou un objet de 3 tuples) avec un `Date` comme première valeur, un `String` en tant que le second et un `Boolean` en tant que son troisième.

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#1)]

Par défaut, le nom de chaque champ dans un tuple se compose de la chaîne `Item` , ainsi que la basée sur une position dans le tuple. Pour cet objet de 3 tuples, les `Date` champ est `Item1`, le `String` champ est `Item2`et le `Boolean` champ est `Item3`. L’exemple suivant affiche les valeurs des champs du tuple instanciée dans la ligne de code précédente

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#2)]

Les champs d’un tuple Visual Basic sont en lecture-écriture ; une fois que vous avez instancié un tuple, vous pouvez modifier ses valeurs. L’exemple suivant modifie deux des trois champs de tuple créés dans l’exemple précédent et affiche le résultat.

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#3)]

## <a name="instantiating-and-using-a-named-tuple"></a>Instanciation et l’utilisation d’un tuple nommé

Au lieu d’utiliser des noms par défaut pour les champs d’un tuple, vous pouvez instancier un *nommé tuple* en assignant vos propres noms pour les éléments du tuple. Les champs du tuple sont ensuite accessible par leurs noms attribués *ou* par leurs noms par défaut. L’exemple suivant instancie le tuple de 3 même comme précédemment, à ceci près qu’il nomme explicitement le premier champ `EventDate`, le deuxième `Name`et la troisième `IsHoliday`. Il affiche les valeurs de champ, les modifie et affiche les valeurs de champ à nouveau.

[!code-vb[Instantiate](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple1.vb#4)]

## <a name="inferred-tuple-element-names"></a>Noms d’élément de tuple déduit

À partir de Visual Basic 15.3, Visual Basic peut déduire les noms d’éléments de tuple ; vous n’avez pas à les assigner explicitement. Les noms de tuple déduits sont utiles lorsque vous initialisez un tuple à partir d’un ensemble de variables, et vous souhaitez que le nom d’élément de tuple pour être le même que le nom de variable. 

L’exemple suivant crée un `stateInfo` tuple qui contient trois explicitement des éléments, nommés `state`, `stateName`, et `capital`. Notez que, dans les éléments d’affectation de noms, l’instruction d’initialisation de tuple attribue simplement les éléments nommés les valeurs des variables portant le même nommés.

[!code-vb[ExplicitlyNamed](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/named-tuples/program.vb#1)]
 
Étant donné que les éléments et les variables ont le même nom, le compilateur Visual Basic peut déduire les noms des champs, comme le montre l’exemple suivant.

[!code-vb[ExplicitlyNamed](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/named-tuples/program.vb#2)]

Pour activer les noms d’élément de tuple interred, vous devez définir la version du compilateur Visual Basic à utiliser dans votre projet Visual Basic (\*.vbproj) fichier : 

```xml 
<PropertyGroup> 
  <LangVersion>15.3</LangVersion> 
</PropertyGroup> 

The version number can be any version of the Visual Basic compiler starting with 15.3. Rather than hard-coding a specific compiler version, you can also specify "Latest" as the value of `LangVersion` to compile with the most recent version of the Visual Basic compiler installed on your system.

In some cases, the Visual Basic compiler cannot infer the tuple element name from the candidate name, and the tuple field can only be referenced using its default name, such as `Item1`, `Item2`, etc. These include:

- The candidate name is the same as the name of a tuple member, such as `Item3`, `Rest`, or `ToString`.

- The candidate name is duplicated in the tuple.
 
When field name inference fails, Visual Basic does not generate a compiler error, nor is an exception thrown at runtime. Instead, tuple fields must be referenced by their predefined names, such as `Item1` and `Item2`. 
  
## Tuples versus structures

A Visual Basic tuple is a value type that is an instance of one of the a **System.ValueTuple** generic types. For example, the `holiday` tuple defined in the previous example is an instance of the <xref:System.ValueTuple%603> structure. It is designed to be a lightweight container for data. Since the tuple aims to make it easy to create an object with multiple data items, it lacks some of the features that a custom structure might have. These include:

- Customer members. You cannot define your own properties, methods, or events for a tuple.

- Validation. You cannot validate the data assigned to fields.

- Immutability. Visual Basic tuples are mutable. In contrast, a custom structure allows you to control whether an instance is mutable or immutable.

If custom members, property and field validation, or immutability are important, you should use the Visual Basic [Structure](../../../language-reference/statements/structure-statement.md) statement to define a custom value type.

A Visual Basic tuple does inherit the members of its **ValueTuple** type. In addition to its fields, these include the following methods:

| Member | Description |
| ---|---|
| CompareTo | Compares the current tuple to another tuple with the same number of elements. |
| Equals | Determines whether the current tuple is equal to another tuple or object. |
| GetHashCode | Calculates the hash code for the current instance. |
| ToString | Returns the string representation of this tuple, which takes the form `(Item1, Item2...)`, where `Item1` and `Item2` represent the values of the tuple's fields. |

In addition, the **ValueTuple** types implement <xref:System.Collections.IStructuralComparable> and <xref:System.Collections.IStructuralEquatable> interfaces, which allow you to define customer comparers.

## Assignment and tuples

Visual Basic supports assignment between tuple types that have the same number of fields. The field types can be converted if one of the following is true:

- The source and target field are of the same type.

- A widening (or implicit) conversion of the source type to the target type is defined. 

- `Option Strict` is `On`, and a narrowing (or explicit) conversion of the source type to the target type is defined. This conversion can throw an exception if the source value is outside the range of the target type.

Other conversions are not considered for assignments. Let's look at the kinds of assignments that are allowed between tuple types.

Consider these variables used in the following examples:

[!code-vb[Assign](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple3.vb#1)]

The first two variables, `unnamed` and `anonymous`, do not have semantic names provided for the fields. Their field names are the default `Item1` and `Item2`. The last two variables, `named` and `differentName` have semantic field names. Note that these two tuples have different names for the fields.

All four of these tuples have the same number of fields (referred to as 'arity'), and the types of those fields are identical. Therefore, all of these assignments work:

[!code-vb[Assign](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple3.vb#2)]

Notice that the names of the tuples are not assigned. The values of the fields are assigned following the order of the fields in the tuple.

Finally, notice that we can assign the `named` tuple to the `conversion` tuple, even though the first field of `named` is an `Integer`, and the first field of `conversion` is a `Long`. This assignment succeeds because converting an `Integer` to a `Long` is a widening conversion.

[!code-vb[Assign](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple3.vb#3)]

Tuples with different numbers of fields are not assignable:

```vb
' Does not compile.
' VB30311: Value of type '(Integer, Integer, Integer)' cannot be converted
'          to '(Answer As Integer, Message As String)'
var differentShape = (1, 2, 3)
named = differentShape
```

## <a name="tuples-as-method-return-values"></a>Tuples comme valeurs de retour de méthode

Une méthode peut retourner une seule valeur. Souvent, cependant, vous aimeriez un appel de méthode pour retourner plusieurs valeurs. Il existe plusieurs façons de contourner cette limitation :

- Vous pouvez créer une classe personnalisée ou une structure dont les propriétés ou champs représentent les valeurs retournées par la méthode. Par conséquent, est une solution de haute densité. Il requiert que vous définissez un type personnalisé dont seul objectif consiste à récupérer les valeurs à partir d’un appel de méthode.

- Vous pouvez retourner une valeur unique à partir de la méthode et renvoyer les valeurs restantes en les passant par référence à la méthode. Cela implique la surcharge de l’instanciation d’une variable et les risques par inadvertance en remplaçant la valeur de la variable que vous passez par référence.

- Vous pouvez utiliser un tuple, qui fournit une solution légère pour la récupération de plusieurs valeurs de retour.

Par exemple, le **TryParse** méthodes de retour de .NET un `Boolean` valeur qui indique si l’opération d’analyse a réussi. Le résultat de l’opération d’analyse est retourné dans une variable passée par référence à la méthode. Normalement, un appel à l’une méthode d’analyse comme <xref:System.Int32.TryParse%2A?displayProperty=nameWithType> présente l’aspect suivant :

[!code-vb[Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#1)]

Nous pouvons retourner un tuple à partir de l’opération d’analyse, si nous encapsulent l’appel à la <xref:System.Int32.TryParse%2A?displayProperty=nameWithType> méthode dans votre propre méthode. Dans l’exemple suivant, `NumericLibrary.ParseInteger` appelle la <xref:System.Int32.TryParse%2A?displayProperty=nameWithType> méthode et retourne un tuple nommé avec deux éléments. 

[!code-vb[Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#2)]

Vous pouvez ensuite appeler la méthode avec un code semblable au suivant :

[!code-vb[Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#3)]

## <a name="visual-basic-tuples-and-tuples-in-the-net-framework"></a>Les tuples de Visual Basic et les tuples dans le .NET Framework

Un tuple de Visual Basic est une instance de l’un de le **System.ValueTuple** des types génériques qui ont été introduits dans le 4.7 Framework .NET. Le .NET Framework inclut également un ensemble de génériques **System.Tuple** classes. Ces classes, toutefois, diffèrent des tuples de Visual Basic et le **System.ValueTuple** des types génériques dans de plusieurs façons :

- Les éléments de la **Tuple** les classes sont des propriétés nommées `Item1`, `Item2`, et ainsi de suite. Dans Visual Basic tuples et **ValueTuple** types d’éléments de tuple, sont des champs.

- Vous ne pouvez attribuer des noms explicites pour les éléments d’un **Tuple** instance ou d’un **ValueTuple** instance. Visual Basic vous permet d’attribuer des noms qui communiquent la signification des champs.

- Les propriétés d’un **Tuple** instance sont en lecture seule ; les tuples sont immuables. Dans Visual Basic tuples et **ValueTuple** , types de champs de tuple sont en lecture-écriture ; les tuples sont mutables.

- Le type générique **Tuple** types sont des types référence. L’utilisation de ces **Tuple** types signifie que de l’allocation d’objets. Sur des chemins réactifs, cela peut avoir un impact mesurable sur les performances de votre application. Visual Basic tuples et **ValueTuple** types sont des types valeur.

Méthodes d’extension dans le <xref:System.TupleExtensions> classe facilitent la conversion entre des tuples de Visual Basic et .NET **Tuple** objets. Le **ToTuple** méthode convertit un tuple de Visual Basic .NET **Tuple** objet et le **ToValueTuple** méthode convertit un .NET **Tuple** objet à un tuple de Visual Basic.

L’exemple suivant crée un tuple, le convertit en un .NET **Tuple** objet et convertit le retour à un tuple de Visual Basic. L’exemple compare ensuite ce tuple avec celui d’origine pour vous assurer qu’ils sont égaux.

[!code-vb[Convert](../../../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple2.vb#1)]

## <a name="see-also"></a>Voir aussi

[Informations de référence sur le langage Visual Basic](index.md)  
