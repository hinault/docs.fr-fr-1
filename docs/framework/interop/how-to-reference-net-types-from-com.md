---
title: "Comment : référencer des types .NET à partir de COM"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: cpp
helpviewer_keywords:
- importing type library
- COM interop, referencing .NET types
- interoperation with unmanaged code, referencing .NET types
- referencing .NET types
- interoperation with unmanaged code, importing type library
- type libraries
- COM interop, importing type library
ms.assetid: 54917f6f-cb18-4103-b622-856b55da93f3
caps.latest.revision: "7"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: b452dd686286ba0ddf648ee532e67a0c121f66eb
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-reference-net-types-from-com"></a>Comment : référencer des types .NET à partir de COM
Du point de vue du code client et serveur, les différences entre COM et le .NET Framework sont largement invisibles. Les clients Microsoft Visual Basic peuvent afficher un objet .NET dans l’Explorateur d’objets, qui expose la syntaxe et les méthodes de l’objet, les propriétés et les champs exactement comme s’il s’agissait de tout autre objet COM.  
  
 Le processus d’importation d’une bibliothèque de types est légèrement plus compliqué pour les clients C++, même si vous utilisez les mêmes outils pour exporter des métadonnées vers une bibliothèque de types COM. Pour référencer des membres d’objet .NET à partir d’un client C++ non managé, référencez le fichier TLB (produit à l’aide de Tlbexp.exe) avec la directive **#import**. Lors du référencement d’une bibliothèque de types à partir de C++, vous devez soit spécifier l’option **raw_interfaces_only**, soit importer les définitions dans la bibliothèque de classes de base Mscorlib.tlb.  
  
### <a name="to-import-a-library"></a>Pour importer une bibliothèque  
  
-   Spécifiez l’option **raw_interfaces_only** dans la directive **#import**. Exemple :  
  
    ```cpp  
    #import "..\LoanLib\LoanLib.tlb" raw_interfaces_only  
    ```  
  
     - ou -  
  
-   Ajoutez une directive #import pour Mscorlib.tlb. Exemple :  
  
    ```cpp  
    #import "mscorlib.tlb"  
    #import "..\LoanLib\LoanLib.tlb"  
    ```  
  
## <a name="see-also"></a>Voir aussi  
 [Exposition de composants .NET Framework à COM](../../../docs/framework/interop/exposing-dotnet-components-to-com.md)  
 [Inscription d’assemblys dans COM](../../../docs/framework/interop/registering-assemblies-with-com.md)  
 [Appel d’un objet .NET](http://msdn.microsoft.com/library/40c9626c-aea6-4bad-b8f0-c1de462efd33)  
 [Déploiement d’une application pour accéder à COM](http://msdn.microsoft.com/library/fb63564c-c1b9-4655-a094-a235625882ce)
