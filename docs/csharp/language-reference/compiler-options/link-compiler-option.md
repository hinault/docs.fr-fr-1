---
title: -link (Options du compilateur C#)
ms.date: 07/20/2015
ms.prod: .net
ms.technology: devlang-csharp
ms.topic: article
helpviewer_keywords:
- /l compiler option [C#]
- /link compiler option [C#]
- -l compiler option [C#]
- EmbedInteropTypes
- l compiler option [C#]
- embed interop types [COM Interop]
- -link compiler option [C#]
- link compiler option [C#]
ms.assetid: 00da70c6-9ea1-43c2-86f2-aa7f26c03475
caps.latest.revision: "13"
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 12ba3762a1c514c52b844a30efc9f49648c51b46
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="-link-c-compiler-options"></a>-link (Options du compilateur C#)
Fait que le compilateur rend disponible pour le projet en cours de compilation les informations de type COM des assemblys spécifiés.  
  
## <a name="syntax"></a>Syntaxe  
  
```console  
-link:fileList  
// -or-  
-l:fileList  
```  
  
## <a name="arguments"></a>Arguments  
 `fileList`  
 Obligatoire. Liste délimitée par des virgules des noms de fichiers d’assembly. Si le nom de fichier contient un espace, placez-le entre des guillemets.  
  
## <a name="remarks"></a>Notes  
 L’option `-link` vous permet de déployer une application qui a des informations de type incorporées. L’application peut ensuite utiliser des types dans un assembly de runtime qui implémentent les informations de type incorporées sans nécessiter une référence à l’assembly de runtime. Si différentes versions de l’assembly de runtime sont publiées, l’application qui contient les informations de type incorporées peut fonctionner avec les différentes versions sans devoir être recompilée. Pour un exemple, consultez [Procédure pas à pas : incorporation de types provenant d’assemblys managés](../../programming-guide/concepts/assemblies-gac/walkthrough-embedding-types-from-managed-assemblies-in-visual-studio.md).  
  
 L’utilisation de l’option `-link` est particulièrement utile quand vous travaillez avec COM Interop. Vous pouvez incorporer des types COM afin que votre application ne nécessite plus un assembly PIA (Primary Interop Assembly) sur l’ordinateur cible. L’option `-link` indique au compilateur d’incorporer les informations de type COM provenant de l’assembly Interop référencé dans le code compilé résultant. Le type COM est identifié par la valeur du CLSID (GUID). Par conséquent, votre application peut s’exécuter sur un ordinateur cible où les mêmes types COM ont été installés avec les mêmes valeurs de CLSID. Les applications qui automatisent Microsoft Office sont un bon exemple. Étant donné que les applications comme Office gardent habituellement la même valeur de CLSID à travers différentes versions, votre application peut utiliser les types COM référencés dès lors que le .NET Framework 4 ou ultérieur est installé sur l’ordinateur cible, et que votre application utilise les méthodes, propriétés ou événements qui sont inclus dans les types COM référencés.  
  
 L’option `-link` incorpore seulement les interfaces, les structures et les délégués. L’incorporation de classes COM n’est pas prise en charge.  
  
> [!NOTE]
>  Quand vous créez une instance d’un type COM incorporé dans votre code, vous devez créer l’instance à l’aide de l’interface appropriée. Une tentative de création d’une instance d’un type COM incorporé à l’aide de la coclasse provoque une erreur.  
  
 Pour définir l’option `-link` dans [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)], ajoutez une référence d’assembly et définissez la propriété `Embed Interop Types` sur **true**. La valeur par défaut pour la propriété `Embed Interop Types` est **false**.  
  
 Si vous liez à un assembly COM (Assembly A) qui référence lui-même un autre assembly COM (Assembly B), vous devez également lier à l’Assembly B si une des conditions suivantes est vraie :  
  
-   Un type de l’Assembly A hérite d’un type ou implémente une interface de l’Assembly B.  
  
-   Un champ, une propriété, un événement ou une méthode qui a un type de retour ou un type de paramètre de l’Assembly B est appelé.  
  
 Comme l’option [-reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md) du compilateur, l’option `-link` du compilateur utilise le fichier réponse Csc.rsp, qui référence les assemblys [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] fréquemment utilisés. Utilisez l’option [-noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md) du compilateur si vous ne voulez pas que le compilateur utilise le fichier Csc.rsp.  
  
 La forme abrégée de `-link` est `-l`.  
  
## <a name="generics-and-embedded-types"></a>Types génériques et imbriqués  
 Les sections suivantes décrivent les limitations de l’utilisation de types génériques dans les applications qui incorporent des types interop.  
  
### <a name="generic-interfaces"></a>Interfaces génériques  
 Vous ne pouvez pas utiliser des interfaces génériques incorporées depuis un assembly d’interopérabilité. L'exemple suivant le démontre.  
  
 [!code-csharp[VbLinkCompilerCS#1](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_1.cs)]  
  
### <a name="types-that-have-generic-parameters"></a>Types ayant des paramètres génériques  
 Vous ne pouvez pas utiliser des types qui ont un paramètre générique dont le type est incorporé depuis un assembly d’interopérabilité si ce type provient d’un assembly externe. Cette restriction ne s’applique pas aux interfaces. Prenons l’exemple de l’interface <xref:Microsoft.Office.Interop.Excel.Range> qui est définie dans l’assembly <xref:Microsoft.Office.Interop.Excel>. Si une bibliothèque incorpore les types interop de l’assembly <xref:Microsoft.Office.Interop.Excel> et expose une méthode qui retourne un type générique qui a un paramètre dont le type est l’interface <xref:Microsoft.Office.Interop.Excel.Range>, cette méthode doit retourner une interface générique, comme dans l’exemple de code suivant.  
  
 [!code-csharp[VbLinkCompilerCS#2](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_2.cs)]  
[!code-csharp[VbLinkCompilerCS#3](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_3.cs)]  
[!code-csharp[VbLinkCompilerCS#4](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_4.cs)]  
  
 Dans l’exemple suivant, le code client peut appeler la méthode qui retourne l’interface générique <xref:System.Collections.IList> sans erreur.  
  
 [!code-csharp[VbLinkCompilerCS#5](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_5.cs)]  
  
## <a name="example"></a>Exemple  
 Le code suivant compile le fichier source `OfficeApp.cs` et des assemblys de référence à partir de `COMData1.dll` et de `COMData2.dll` pour produire `OfficeApp.exe`.  
  
```csharp  
csc -link:COMData1.dll,COMData2.dll -out:OfficeApp.exe OfficeApp.cs  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Options du compilateur C#](../../../csharp/language-reference/compiler-options/index.md)  
 [Procédure pas à pas : incorporation de types provenant d’assemblys managés](../../programming-guide/concepts/assemblies-gac/walkthrough-embedding-types-from-managed-assemblies-in-visual-studio.md)  
 [-reference (Options du compilateur C#)](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)  
 [-noconfig (Options du compilateur C#)](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md)  
 [Génération à partir de la ligne de commande avec csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)  
 [Vue d’ensemble de l’interopérabilité](../../../csharp/programming-guide/interop/interoperability-overview.md)
