---
title: "Le mot clé Fixed (F #)"
description: "Découvrez comment vous pouvez « pin » locale sur la pile pour empêcher la collection avec F # « fixed » (mot clé)."
keywords: visual f#, f#, programmation fonctionnelle
author: cartermp
ms.author: phcart
ms.date: 04/24/2017
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 5795ce1f-11bf-4798-9f1f-6e44ffa1477e
ms.openlocfilehash: 1605603bc35941e21c798600140036fb678869b5
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="the-fixed-keyword"></a>Le mot clé Fixed

F # 4.1 introduit le `fixed` mot clé, qui vous permet de « épingler » locale sur la pile pour l’empêcher d’être collectées ou déplacé pendant le garbage collection.  Il est utilisé pour les scénarios de programmation de bas niveau.

## <a name="syntax"></a>Syntaxe

```fsharp
use ptr = fixed expression
```

## <a name="remarks"></a>Notes

Cela permet d’étendre la syntaxe des expressions pour permettre l’extraction d’un pointeur et le lier à un nom qui ne peut pas être collectées ou déplacé pendant le garbage collection.  

Un pointeur à partir d’une expression est fixe la `fixed` (mot clé) est liée à un identificateur via le `use` (mot clé).  La sémantique de cela est similaire à la gestion des ressources via les `use` (mot clé).  Le pointeur est fixe tandis qu’il est dans la portée, une fois qu’elle est hors de portée, il est fixe n’est plus.  `fixed`ne peut pas être utilisé en dehors du contexte d’un `use` liaison.  Vous devez lier le pointeur sur un nom avec `use`.

Utilisation de `fixed` doivent se produire dans une expression dans une fonction ou une méthode.  Il ne peut pas être utilisé avec une portée au niveau du script ou au niveau du module.

Comme tout code de pointeur, ceci est une fonctionnalité non sécurisée et émet un avertissement lorsqu’il est utilisé.

## <a name="example"></a>Exemple

```fsharp
open Microsoft.FSharp.NativeInterop

type Point = { mutable X: int; mutable Y: int}

let squareWithPointer (p: nativeptr<int>) =
    // Dereference the pointer at the 0th address.
    let mutable value = NativePtr.get p 0

    // Perform some work
    value <- value * value

    // Set the value in the pointer at the 0th address.
    NativePtr.set p 0 value

let pnt = { X = 1; Y = 2 }
printfn "pnt before - X: %d Y: %d" pnt.X pnt.Y // prints 1 and 2

// Note that the use of 'fixed' is inside a function.
// You cannot fix a pointer at a script-level or module-level scope.
let doPointerWork() =
    use ptr = fixed &pnt.Y

    // Square the Y value
    squareWithPointer ptr
    printfn "pnt after - X: %d Y: %d" pnt.X pnt.Y // prints 1 and 4

doPointerWork()
```

## <a name="see-also"></a>Voir aussi

[NativePtr (Module)](https://msdn.microsoft.com/visualfsharpdocs/conceptual/nativeinterop.nativeptr-module-%5Bfsharp%5D)
