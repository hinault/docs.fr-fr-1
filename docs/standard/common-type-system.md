---
title: "Système de type commun (CTS, Common Type System) et spécification CLS (Common Language Specification)"
description: "Découvrez comment CTS et CLS permettent à .NET de prendre en charge plusieurs langages."
keywords: .NET, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 3b1f5725-ac94-4f17-8e5f-244442438a4d
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: d7626b0a6a902465416187b2c09d624dfe9a9773
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/23/2017
---
# <a name="common-type-system--common-language-specification"></a>Système de type commun (CTS, Common Type System) et spécification CLS (Common Language Specification)

Là encore, ce sont deux termes largement utilisés dans l’environnement .NET ; ils sont véritablement essentiels pour comprendre comment une implémentation de .NET permet le développement dans plusieurs langages et comment elle fonctionne.

## <a name="common-type-system"></a>Système de type commun

Pour commencer, n’oubliez pas qu’une implémentation de .NET est _indépendante du langage_. Cela ne signifie pas seulement qu’un programmeur peut écrire son code dans n’importe quel langage compilable en langage intermédiaire. Cela signifie également qu’il doit être en mesure d’interagir avec le code écrit dans d’autres langages utilisables sur une implémentation de .NET.

Pour que cela se fasse de manière transparente, il doit exister un moyen commun de décrire tous les types pris en charge. C’est ce que fait le système de type commun (CTS). Il a été créé pour effectuer plusieurs opérations :

*   Établir un framework pour l’exécution multilingue.
*   Fournir un modèle orienté objet pour prendre en charge l’implémentation de différents langages sur une implémentation de .NET.
*   Définir un ensemble de règles que tous les langages doivent respecter pour utiliser les types.
*   Fournir une bibliothèque contenant les types primitifs de base utilisés dans le développement d’applications (par ex., `Boolean`, `Byte`, `Char`, etc.)

CTS définit deux grandes sortes de types qui doivent être pris en charge : les types valeur et référence. Leur nom pointe sur leur définition.

Les objets des types référence sont représentés par une référence à la valeur réelle de l’objet. Ici, une référence s’apparente à un pointeur en C/C++. Ils référencent simplement un emplacement de mémoire où se trouvent les valeurs des objets. Cela a un profond impact sur l’utilisation de ces types. Si vous attribuez un type référence à une variable et que vous passez ensuite cette variable dans une méthode, par exemple, les modifications de l’objet sont reflétées sur l’objet principal, il n’y a pas de copie.

Les types valeur sont l’opposé, c’est-à-dire que les objets sont représentés par leurs valeurs. Si vous attribuez un type valeur à une variable, vous copiez en fait une valeur de l’objet.

CTS définit plusieurs catégories de types, chacun avec une sémantique et une utilisation propres :

*   Classes
*   Structures
*   Enums
*   Interfaces
*   Délégués

CTS définit également toutes les autres propriétés des types, comme les modificateurs d’accès, les membres de type valides, le fonctionnement de l’héritage et de la surcharge, et ainsi de suite. Malheureusement, cet article de présentation n’a pas pour but d’approfondir davantage, mais vous pouvez consulter la section [Autres ressources](#more-resources) à la fin pour obtenir des liens vers un contenu plus détaillé qui couvre ces rubriques.

## <a name="common-language-specification"></a>CLS (Common Language Specification)

Pour permettre des scénarios d’interopérabilité complète, tous les objets qui sont créés dans le code doivent s’appuyer sur certains points communs entre les langages qui les consomment (leurs _appelants_). Comme il existe de nombreux langages différents, .NET a défini ces points communs dans ce que l’on appelle la **spécification CLS (Common Language Specification)**. CLS définit un ensemble de fonctionnalités nécessaires pour de nombreuses applications courantes. Il fournit également une sorte de recette pour n’importe quel langage implémenté sur .NET qui explique ce qu’il doit prendre en charge.

CLS est un sous-ensemble du système CTS. Cela signifie que toutes les règles du CTS s’appliquent également à la spécification CLS, sauf si les règles CLS sont plus strictes. Si un composant est créé uniquement à l’aide des règles CLS, autrement dit, s’il expose uniquement les fonctionnalités CLS dans son API, il est considéré comme étant **conforme CLS**. Par exemple, les `<framework-librares>` sont conformes CLS justement parce qu’ils ont besoin d’utiliser tous les langages pris en charge sur .NET.

Vous pouvez consulter les documents de la section [Autres ressources](#more-resources) ci-dessous pour obtenir une vue d’ensemble de toutes les fonctionnalités de la spécification CLS.

## <a name="more-resources"></a>Autres ressources

*   [Système de type commun](./base-types/common-type-system.md)
*   [CLS (Common Language Specification)](language-independence-and-language-independent-components.md)
