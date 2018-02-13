---
title: Noms d'assemblys et de DLL
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- names [.NET Framework], DLLs
- names [.NET Framework], assemblies
- assemblies [.NET Framework], names
- DLLs, names
ms.assetid: e800b610-31b4-4949-9c14-cb60e9f254be
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: f74c37821d730ec8dcaa74763967c662bafd6699
ms.sourcegitcommit: be1fb5d9447ad459bef22b91a91c72e3e0b2d916
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/09/2018
---
# <a name="names-of-assemblies-and-dlls"></a>Noms d'assemblys et de DLL
Un assembly est l’unité de déploiement et d’identité pour les programmes de code managé. Bien que les assemblys peuvent s’étendre sur un ou plusieurs fichiers, en général, un assembly mappe un à un avec une DLL. Par conséquent, cette section décrit les conventions d’affectation de noms d’uniquement DLL peuvent être mappées à des conventions d’affectation des noms d’assembly.  
  
 **✓ FAIRE** choisissez des noms pour vos DLL d’assembly qui suggèrent des grands segments de fonctionnalités, telles que System.Data.  
  
 Noms d’assembly et la DLL n’êtes pas obligé de correspondent aux noms d’espace de noms, mais il est conseillé d’utiliser l’espace de noms lorsque vous nommez des assemblys. Une règle empirique consiste pour nommer la DLL en fonction du préfixe commun des espaces de noms contenus dans l’assembly. Par exemple, un assembly avec deux espaces de noms, `MyCompany.MyTechnology.FirstFeature` et `MyCompany.MyTechnology.SecondFeature`, peut être appelée `MyCompany.MyTechnology.dll`.  
  
 **✓ Envisagez** nommer les DLL selon le modèle suivant :  
  
 `<Company>.<Component>.dll`  
  
 où `<Component>` contient une ou plusieurs clauses séparées par un point. Exemple :  
  
 `Litware.Controls.dll`.  
  
 *Portions © 2005, 2009 Microsoft Corporation. Tous droits réservés.*  
  
 *Réimprimées avec l’autorisation de Pearson éducation, Inc. à partir de [règles de conception d’infrastructure : Conventions, idiomes et des modèles pour les bibliothèques .NET réutilisable, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina et Brad Abrams, publié le 22 octobre 2008 par Addison-Wesley Professional dans le cadre de la série de développement Microsoft Windows.*  
  
## <a name="see-also"></a>Voir aussi  
 [Règles de conception de .NET Framework](../../../docs/standard/design-guidelines/index.md)  
 [Directives de nommage](../../../docs/standard/design-guidelines/naming-guidelines.md)
