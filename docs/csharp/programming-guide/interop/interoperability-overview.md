---
title: "Vue d'ensemble de l'interopérabilité (Guide de programmation C#)"
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
helpviewer_keywords:
- COM interop
- C# language, interoperability
- C++ Interop
- interoperability, about interoperability
- platform invoke
ms.assetid: c025b2e0-2357-4c27-8461-118f0090aeff
caps.latest.revision: "43"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 7e4bc1814ed5c86660b4333542a3dc4eb7462e89
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="interoperability-overview-c-programming-guide"></a>Vue d'ensemble de l'interopérabilité (Guide de programmation C#)
Cette rubrique décrit les méthodes qui permettent une interopérabilité entre le code managé C# et le code non managé.  
  
## <a name="platform-invoke"></a>Appel de plateforme  
 L’*appel de code non managé* est un service qui permet au code managé d’appeler des fonctions non managées implémentées dans des bibliothèques de liens dynamiques (DLL), telles que celles de l’API Win32 Microsoft. Il localise et appelle une fonction exportée, puis marshale ses arguments (entiers, chaînes, tableaux, structures, etc) au-delà des limites d’interopérabilité, selon les besoins.  
  
 Pour plus d’informations, consultez [Consommation de fonctions DLL non managées](../../../framework/interop/consuming-unmanaged-dll-functions.md) et [Guide pratique pour utiliser le code non managé pour lire un fichier audio](../../../csharp/programming-guide/interop/how-to-use-platform-invoke-to-play-a-wave-file.md).  
  
> [!NOTE]
>  Le [common language runtime](../../../standard/clr.md) (CLR) gère l’accès aux ressources système. Le fait d’appeler du code non managé extérieur au CLR contourne ce mécanisme, ce qui présente un risque de sécurité. Par exemple, du code non managé peut appeler directement des ressources dans du code non managé en contournant les mécanismes de sécurité CLR. Pour plus d’informations, consultez [Sécurité .NET Framework](http://go.microsoft.com/fwlink/?LinkId=37122).  
  
## <a name="c-interop"></a>Interopérabilité C++  
 Vous pouvez utiliser l’interopérabilité C++, également appelée It Just Works (IJW), pour encapsuler une classe C++ native de sorte qu’elle puisse être utilisée par du code créé en C# ou un autre langage du .NET Framework. Pour ce faire, écrivez du code C++ pour encapsuler un composant DLL ou COM natif. Contrairement à d’autres langages du .NET Framework, [!INCLUDE[vcprvc](~/includes/vcprvc-md.md)] comprend la prise en charge de l’interopérabilité qui permet à du code managé et à du code non managé de se trouver dans la même application et même dans le même fichier. Vous pouvez ensuite générer le code C++ à l’aide du commutateur de compilateur **/clr** pour créer un assembly managé. Enfin, ajoutez une référence à l’assembly dans votre projet C# et utilisez les objets encapsulés comme vous le feriez pour les autres classes managées.  
  
## <a name="exposing-com-components-to-c"></a>Exposition de composants COM au langage C#  
 Vous pouvez utiliser un composant COM d’un projet C#. Les étapes générales sont les suivantes :  
  
1.  Recherchez le composant COM à utiliser et enregistrez-le. Utilisez regsvr32.exe pour inscrire ou désinscrire une DLL COM.  
  
2.  Ajoutez au projet une référence au composant COM ou à la bibliothèque de types.  
  
     Quand vous ajoutez la référence, [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] utilise le fichier [Tlbimp.exe (Type Library Importer)](http://msdn.microsoft.com/library/ec0a8d63-11b3-4acd-b398-da1e37e97382), qui prend comme entrée une bibliothèque de types, pour générer un assembly d’interopérabilité .NET Framework. L’assembly, également appelé wrapper RCW, contient des classes et des interfaces managées qui encapsulent les classes et les interfaces COM qui se trouvent dans la bibliothèque de types. [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] ajoute au projet une référence à l’assembly généré.  
  
3.  Créez une instance d’une classe qui est définie dans le wrapper RCW. Une instance de l’objet COM est ainsi créée.  
  
4.  Utilisez l’objet comme vous utiliseriez tout autre objet managé. Lorsque l’objet est récupéré par le garbage collection, l’instance de l’objet COM est également libérée de la mémoire.  
  
 Pour plus d’informations, consultez [Exposition de composants COM au .NET Framework](http://msdn.microsoft.com/library/e78b14f1-e487-43cd-9c6d-1a07483f1730).  
  
## <a name="exposing-c-to-com"></a>Exposition du langage C# à COM  
 Les clients COM peuvent utiliser des types C# qui ont été correctement exposés. Les étapes de base pour exposer des types C# sont les suivantes :  
  
1.  Ajoutez des attributs d’interopérabilité dans le projet C#.  
  
     Vous pouvez rendre visible un assembly COM en modifiant les propriétés de projet [!INCLUDE[csprcs](~/includes/csprcs-md.md)]. Pour plus d’informations, consultez [Informations de l’assembly, boîte de dialogue](/visualstudio/ide/reference/assembly-information-dialog-box).  
  
2.  Générez une bibliothèque de types COM et inscrivez-la pour l’utilisation de COM.  
  
     Vous pouvez modifier les propriétés de projet [!INCLUDE[csprcs](~/includes/csprcs-md.md)] de manière à inscrire automatiquement l’assembly C# pour COM Interop. [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] utilise le fichier [Regasm.exe (outil Assembly Registration Tool)](http://msdn.microsoft.com/library/e190e342-36ef-4651-a0b4-0e8c2c0281cb) avec le commutateur de ligne de commande `/tlb`, qui prend comme entrée un assembly managé pour générer une bibliothèque de types. Cette bibliothèque de types décrit les types `public` de l’assembly et ajoute les entrées du Registre pour que les clients COM puissent créer des classes managées.  
  
 Pour plus d’informations, consultez [Exposition de composants .NET Framework à COM](http://msdn.microsoft.com/library/e42a65f7-1e61-411f-b09a-aca1bbce24c6) et [Exemple de classe COM](../../../csharp/programming-guide/interop/example-com-class.md).  
  
## <a name="see-also"></a>Voir aussi  
 [Amélioration des performances d’interopérabilité](http://go.microsoft.com/fwlink/?LinkId=99564)  
 [Introduction à COM Interop](http://go.microsoft.com/fwlink/?LinkId=112406)  
 [Marshaling entre du code managé et non managé](http://go.microsoft.com/fwlink/?LinkId=112398)  
 [Interopération avec du code non managé](../../../../docs/framework/interop/index.md)  
 [Interopérabilité COM avancée](http://msdn.microsoft.com/library/3ada36e5-2390-4d70-b490-6ad8de92f2fb)  
 [Guide de programmation C#](../../../csharp/programming-guide/index.md)
