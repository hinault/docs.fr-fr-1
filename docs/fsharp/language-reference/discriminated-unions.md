---
title: "Unions discriminées (F#)"
description: "Découvrez comment utiliser F # unions discriminées."
keywords: visual f#, f#, programmation fonctionnelle
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 16e2a011-c785-48c8-859f-79df7f3a0e29
ms.openlocfilehash: b7a02512ce4a63885e771be56f106bc66cc2743e
ms.sourcegitcommit: cf22b29db780e532e1090c6e755aa52d28273fa6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2018
---
# <a name="discriminated-unions"></a>Unions discriminées

Les unions discriminées prennent en charge pour les valeurs qui peuvent s’agir d’un nombre de cas nommés, éventuellement chacun avec des types et des valeurs différentes. Les unions discriminées sont utiles pour les données hétérogènes ; données qui peuvent avoir des cas spéciaux, y compris les valide et les cas d’erreur ; données qui varie selon le type d’une instance à une autre ; et comme alternative pour les hiérarchies de petits objets. En outre, discriminée récursive unions sont utilisées pour représenter des structures de données d’arborescence.

## <a name="syntax"></a>Syntaxe

```fsharp
[ attributes ]
type type-name =
    | case-identifier1 [of [ fieldname1 : ] type1 [ * [ fieldname2 : ] type2 ...]
    | case-identifier2 [of [fieldname3 : ]type3 [ * [ fieldname4 : ]type4 ...]
...
```

## <a name="remarks"></a>Notes
Les unions discriminées sont semblables aux types union dans d’autres langages, mais il existe des différences. Comme avec un type union en C++ ou un type variant en Visual Basic, les données stockées dans la valeur ne sont pas fixe ; Il peut être une des options distinctes. Contrairement aux unions de ces autres langages, toutefois, chacune des options possibles reçoit un *identificateur de cas*. Les identificateurs de cas sont des noms pour les différents types de valeurs susceptibles d’entraîner des objets de ce type ; les valeurs sont facultatives. Si les valeurs ne sont pas présents, le cas est équivalent à un cas d’énumération. Si les valeurs sont présentes, chaque valeur peut être une valeur unique d’un type spécifié, ou un tuple qui regroupe plusieurs champs des mêmes ou de types différents. À compter de F # 3.1, vous pouvez nommer un champ individuel, mais le nom est facultatif, même si d’autres champs dans la même casse sont nommés.

Par exemple, considérez la déclaration suivante d’un type de forme.

```fsharp
type Shape =
    | Rectangle of width : float * length : float
    | Circle of radius : float
    | Prism of width : float * float * height : float
```

Le code précédent déclare une union discriminée forme, ce qui peut avoir des valeurs d’un des trois cas : Rectangle, cercle et prisme. Chaque cas a un autre ensemble de champs. Le Rectangle cas a le nom de deux champs, les deux de type `float`, dont la largeur de noms et la longueur. Le cas du cercle a un seul champ nommé, radius. Le cas de prisme a trois champs, deux des quels (largeur et hauteur) sont des champs nommés. Les champs sans nom sont désignés en tant que champs anonymes.

Pour construire des objets en fournissant des valeurs pour les champs nommés et anonymes selon les exemples suivants.

```fsharp
let rect = Rectangle(length = 1.3, width = 10.0)
let circ = Circle (1.0)
let prism = Prism(5., 2.0, height = 3.0)
```

Ce code montre que vous pouvez utiliser les champs nommés lors de l’initialisation, ou vous pouvez s’appuient sur l’ordre des champs dans la déclaration et simplement fournir les valeurs pour chaque champ à son tour. L’appel de constructeur pour `rect` dans le code précédent utilise les champs nommés, mais l’appel de constructeur pour `circ` utilise le classement. Vous pouvez combiner les champs ordonnées et champs nommés, comme dans la construction de `prism`.

Le `option` type est une union discriminée simple dans la bibliothèque principale F #. Le `option` type est déclaré comme suit.

```fsharp
// The option type is a discriminated union.
type Option<'a> =
    | Some of 'a
    | None
```

Le code précédent Spécifie que le type `Option` est une union discriminée qui a deux cas, `Some` et `None`. Le `Some` cas a une valeur associée qui se compose d’un seul champ anonyme dont le type est représenté par le paramètre de type `'a`. Le `None` cas n’a aucune valeur associée. Par conséquent, le `option` type spécifie un type générique qui a soit une valeur d’un type ou aucune valeur. Le type `Option` a également un alias de type en minuscules, `option`, qui est plus couramment utilisées.

Les identificateurs de cas peuvent être utilisés comme constructeurs pour le type union discriminée. Par exemple, le code suivant est utilisé pour créer des valeurs de la `option` type.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2001.fs)]

Les identificateurs de cas sont également utilisés dans les expressions de critères spéciaux. Dans une expression de critères spéciaux, les identificateurs sont fournis pour les valeurs associées à chaque cas. Par exemple, dans le code suivant, `x` est l’identificateur qui reçoit la valeur qui est associée à la `Some` cas de la `option` type.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2002.fs)]

Dans les expressions de critères spéciaux, vous pouvez utiliser les champs nommés pour spécifier les correspondances unions discriminées. Pour le type de forme qui a été déclaré précédemment, vous pouvez utiliser les champs nommés, comme le montre le code suivant pour extraire les valeurs des champs.

```fsharp
let getShapeHeight shape =
    match shape with
    | Rectangle(height = h) -> h
    | Circle(radius = r) -> 2. * r
    | Prism(height = h) -> h
```

Normalement, les identificateurs de cas peuvent être utilisés sans les qualifier par le nom de l’union. Si vous souhaitez que le nom soit toujours qualifié avec le nom de l’union, vous pouvez appliquer la [RequireQualifiedAccess](https://msdn.microsoft.com/library/8b9b6ade-0471-4413-ac5d-638cd0de5f15) d’attribut à la définition du type d’union.

### <a name="unwrapping-discriminated-unions"></a>Unions discriminées désencapsuler

Dans les Unions discriminées F # sont souvent utilisés dans la modélisation de domaine pour un seul type d’habillage. Il est facile extraire la valeur sous-jacente via la recherche de correspondance ainsi. Vous n’avez pas besoin d’utiliser une expression de correspondance pour un seul cas :
```fsharp
let ([UnionCaseName] [values]) = [UnionValue]
```

Cela est illustré par l'exemple suivant :

```fsharp
type ShaderProgram = | ShaderProgram of id:int

let someMethodUsingShaderProgram shaderProgram =
    let (ShaderProgram id) = shaderProgram
    // Use the unwrapped value
    ..
```

## <a name="struct-discriminated-unions"></a>Unions discriminées de struct

À compter de F # 4.1, vous pouvez également représenter les Unions discriminées en tant que structures.  Cette opération s’effectue avec la `[<Struct>]` attribut.

```fsharp
[<Struct>]
type SingleCase = Case of string

[<Struct>]
type Multicase =
    | Case1 of Case1 : string
    | Case2 of Case2 : int
    | Case3 of Case3 : double
```

Étant donné que ceux-ci sont des types valeur et les types de référence pas, il existe supplémentaire unions discriminées de considérations par rapport à la référence :

1. Ils sont copiés en tant que types valeur et ont une sémantique de type valeur.
2. Vous ne pouvez pas utiliser une définition de type récursif à un struct multicase discriminées Union.
3. Vous devez fournir le nom de cas unique pour un struct multicase discriminées Union.

## <a name="using-discriminated-unions-instead-of-object-hierarchies"></a>Utilisation d’Unions discriminées au lieu de hiérarchies d’objets
Vous pouvez souvent utiliser une union discriminée comme une alternative plus simple à une hiérarchie de petits objets. Par exemple, l’union discriminée suivante peut servir à la place d’un `Shape` classe de base qui a des types dérivés pour cercle, carré, et ainsi de suite.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2003.fs)]

À la place d’une méthode virtuelle pour calculer une zone ou un périmètre, que vous utiliseriez dans une implémentation orientée objet, vous pouvez utiliser des critères spéciaux pour créer une branche vers les formules appropriées pour calculer ces quantités. Dans l’exemple suivant, des formules différentes sont utilisées pour calculer la zone, en fonction de la forme.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2004.fs)]

La sortie est la suivante :

```
Area of circle that has radius 15.000000: 706.858347
Area of square that has side 10.000000: 100.000000
Area of rectangle that has height 5.000000 and width 10.000000 is 50.000000
```

## <a name="using-discriminated-unions-for-tree-data-structures"></a>Utilisation d’Unions discriminées pour les Structures de données d’arborescence
Les unions discriminées peuvent être récursives, c'est-à-dire que l’union elle-même peut être incluse dans le type d’un ou plusieurs cas. Récursive les unions discriminées peuvent être utilisées pour créer des arborescences, qui sont utilisés pour modeler des expressions dans les langages de programmation. Dans le code suivant, une récursive discriminée union est utilisé pour créer une structure de données d’arborescence binaire. L’union se compose de deux cas, `Node`, qui est un nœud avec une valeur entière et des sous-arborescences gauche et droite, et `Tip`, qui termine l’arborescence.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2005.fs)]

Dans le code précédent, `resultSumTree` a la valeur 10. L’illustration suivante montre la structure d’arborescence de `myTree`.

![Arborescence pour myTree](../media/TreeStructureDiagram.png)

Les unions discriminées fonctionnent bien si les nœuds de l’arborescence sont hétérogènes. Dans le code suivant, le type `Expression` représente l’arborescence de syntaxe abstraite d’une expression dans un langage de programmation simple qui prend en charge d’addition et multiplication des nombres et des variables. Parmi les cas d’union ne sont pas récursifs et représentent des nombres (`Number`) ou des variables (`Variable`). Autres cas sont récursifs et représentent des opérations (`Add` et `Multiply`), où les opérandes sont également des expressions. Le `Evaluate` fonction utilise une expression de correspondance pour traiter de manière récursive l’arborescence de syntaxe.

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2006.fs)]

Lorsque ce code est exécuté, la valeur de `result` est 5.

## <a name="common-attributes"></a>Attributs courants

Les attributs suivants sont communément dans les unions discriminées :

* `[RequireQualifiedAccess]`
* `[NoEquality]`
* `[NoComparison]`
* `[Struct]`(F # 4.1 et versions ultérieures)

## <a name="see-also"></a>Voir aussi
[Informations de référence du langage F#](index.md)
