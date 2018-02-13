---
title: "Tlbexp.exe (exportateur de bibliothèques de types)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- exporting type library [.NET Framework]
- exporter tool [.NET Framework]
- Tlbexp.exe
- Type Library Exporter
- type libraries [.NET Framework], exporting
ms.assetid: a487d61b-d166-467b-a7ca-d8b52fbff42d
caps.latest.revision: "35"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 47710b81de79a9dfbb6bddd39035be2986350b0e
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="tlbexpexe-type-library-exporter"></a>Tlbexp.exe (exportateur de bibliothèques de types)
L'outil Type Library Exporter (Exportateur de bibliothèques de types) génère une bibliothèque de types décrivant les types définis dans un assembly du Common Language Runtime.  
  
 Cet outil est installé automatiquement avec Visual Studio. Pour exécuter l'outil, utilisez l'invite de commandes développeur (ou l'invite de commandes Visual Studio dans Windows 7). Pour plus d'informations, consultez [Invites de commandes](../../../docs/framework/tools/developer-command-prompt-for-vs.md).  
  
 À l'invite de commandes, tapez le texte suivant :  
  
## <a name="syntax"></a>Syntaxe  
  
```  
tlbexp assemblyName [options]  
```  
  
#### <a name="parameters"></a>Paramètres  
  
|Argument|Description|  
|--------------|-----------------|  
|*assemblyName*|Assembly pour lequel exporter une bibliothèque de types.|  
  
|Option|Description|  
|------------|-----------------|  
|**/asmpath:** *répertoire*|Spécifie l'emplacement dans lequel rechercher des assemblys. Si vous utilisez cette option, vous devez spécifier explicitement les emplacements dans lesquels rechercher des assemblys référencés, y compris le répertoire actif.<br /><br /> Quand vous utilisez l’option **asmpath**, l’exportateur de bibliothèques de types ne recherche pas d’assembly dans le Global Assembly Cache (GAC).|  
|**/help**|Affiche la syntaxe et les options de commande de l'outil.|  
|**/names:** *nom_fichier*|Spécifie la mise en majuscules des noms figurant dans une bibliothèque de types. L’argument *nom_fichier* est un fichier texte. Chaque ligne du fichier spécifie la mise en majuscules d'un nom de la bibliothèque de types.|  
|**/nologo**|Supprime l'affichage de la bannière de démarrage Microsoft.|  
|**/oldnames**|Oblige Tlbexp.exe à exporter des noms de types décorés s'il y a un conflit de nom de type. Notez que c'était le comportement par défaut dans les versions antérieures à .NET Framework version 2.0.|  
|**/out:** *fichier*|Spécifie le nom du fichier bibliothèque de types à générer. Si vous omettez cette option, Tlbexp.exe génère une bibliothèque de types portant le même nom que celui de l’assembly (le véritable nom de l’assembly, pas nécessairement identique à celui du fichier comportant l’assembly), ainsi qu’une extension .tlb.|  
|**/silence:** `warningnumber`|Supprime l'affichage de l'avertissement spécifié. Cette option ne peut pas être utilisée avec **/silent**.|  
|**/silent**|Supprime l'affichage des messages indiquant la réussite des opérations. Cette option ne peut pas être utilisée avec **/silence**.|  
|**/tlbreference:** *nom_bibliothèque_types*|Oblige Tlbexp.exe à résoudre explicitement les références à la bibliothèque de types sans consulter le Registre. Par exemple, si l'assembly B référence l'assembly A, vous pouvez utiliser cette option pour fournir une référence à la bibliothèque de types explicites, plutôt que de vous appuyer sur la bibliothèque de types spécifiée dans le Registre. Tlbexp.exe contrôle la version pour s'assurer que la version de la bibliothèque de types correspond à la version de l'assembly ; dans le cas contraire, il génère une erreur.<br /><br /> Notez que l’option **tlbreference** consulte toujours le Registre dans les cas où l’attribut <xref:System.Runtime.InteropServices.ComImportAttribute> est appliqué à une interface qui est ensuite implémentée par un autre type.|  
|**/tlbrefpath:** *chemin*|Chemin complètement spécifié à une bibliothèque de types référencée.|  
|**/win32**|Lors de la compilation sur un ordinateur 64 bits, cette option spécifie que Tlbexp.exe doit générer une bibliothèque de types 32 bits.|  
|**/win64**|En cas de compilation sur un ordinateur 32 bits, cette option spécifie que Tlbexp.exe doit générer une bibliothèque de types 64 bits.|  
|**/verbose**|Spécifie le mode Commentaires ; affiche la liste de tous les assemblys référencés pour lesquels une bibliothèque de types doit être générée.|  
|**/?**|Affiche la syntaxe et les options de commande de l'outil.|  
  
> [!NOTE]
>  Les options de ligne de commande de Tlbexp.exe ne respectent pas la casse et peuvent être fournies dans n'importe quel ordre. Il vous suffit de spécifier les éléments de l'option nécessaires à son identification de manière unique. Par exemple, **/n** équivaut à **/nologo**, et **/o:** *outfile.tlb* à **/out:** *outfile.tlb*.  
  
## <a name="remarks"></a>Notes  
 Tlbexp.exe génère une bibliothèque de types comportant les définitions des types définis dans l'assembly. Des applications, telles que Visual Basic 6.0, peuvent utiliser la bibliothèque de types générée pour créer une liaison vers les types .NET définis dans l'assembly.  
  
> [!IMPORTANT]
>  Vous ne pouvez pas utiliser Tlbexp.exe pour exporter les fichiers de métadonnées Windows (.winmd). L'exportation des assemblys Windows Runtime n'est pas prise en charge.  
  
 La totalité de l'assembly est convertie immédiatement. Vous ne pouvez pas utiliser Tlbexp.exe pour générer des informations sur les types pour un sous-ensemble de types définis dans un assembly.  
  
 Vous ne pouvez pas utiliser Tlbexp.exe pour générer une bibliothèque de types à partir d’un assembly ayant été importé à l’aide de l’[importateur de bibliothèques de types (Tlbimp.exe)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md). À la place, vous devez faire référence à la bibliothèque de types d'origine importée avec Tlbimp.exe. Vous pouvez exporter une bibliothèque de types d'un assembly qui référence des assemblys importés à l'aide de Tlbimp.exe. Consultez la section des exemples ci-dessous.  
  
 Tlbexp.exe place les bibliothèques de types générées dans le répertoire de travail en cours ou dans le répertoire spécifié pour le fichier de sortie. Un seul assembly peut être à l'origine de plusieurs bibliothèques de types.  
  
 Tlbexp.exe génère une bibliothèque de types, mais ne l'inscrit pas. Par contre, l’[outil d’inscription d’assembly (Regasm.exe)](../../../docs/framework/tools/regasm-exe-assembly-registration-tool.md) génère et inscrit une bibliothèque de types. Utilisez par conséquent Regasm.exe pour générer et inscrire une bibliothèque de types avec COM.  
  
 Si vous ne spécifiez pas l'option `/win32` ou `/win64`, Tlbexp.exe génère une bibliothèque de types 32 bits ou 64 bits qui correspond au type d'ordinateur sur lequel vous exécutez la compilation (32 bits ou 64 bits). Pour les besoins de la compilation croisée, vous pouvez utiliser l'option `/win64` sur un ordinateur 32 bits pour générer une bibliothèque de types 64 bits et l'option `/win32` sur un ordinateur 64 bits pour générer une bibliothèque de types 32 bits. Dans les bibliothèques de types 32 bits, <xref:System.Runtime.InteropServices.ComTypes.SYSKIND> a la valeur <xref:System.Runtime.InteropServices.ComTypes.SYSKIND.SYS_WIN32>. Dans les bibliothèques de types 64 bits, <xref:System.Runtime.InteropServices.ComTypes.SYSKIND> a la valeur <xref:System.Runtime.InteropServices.ComTypes.SYSKIND.SYS_WIN64>. Toutes les transformations de type de données (par exemple, types de données classés selon la taille du pointeur comme `IntPtr` et `UIntPtr`) sont converties en conséquence.  
  
 Si vous utilisez l'attribut <xref:System.Runtime.InteropServices.MarshalAsAttribute> pour spécifier une valeur <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArraySubType> de `VT_UNKOWN` ou `VT_DISPATCH`, Tlbexp.exe ignore toute utilisation subséquente du champ <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArrayUserDefinedSubType>. Examinons, par exemple, les signatures suivantes :  
  
```  
[return:MarshalAs(UnmanagedType.SafeArray, SafeArraySubType=VarEnum.VT_UNKNOWN, SafeArrayUserDefinedSubType=typeof(ConsoleKeyInfo))] public Array StructUnkSafe(){return null;}  
[return:MarshalAs(UnmanagedType.SafeArray, SafeArraySubType=VarEnum.VT_DISPATCH, SafeArrayUserDefinedSubType=typeof(ConsoleKeyInfo))] public Array StructDispSafe(){return null;}  
```  
  
 la bibliothèque de types suivante est générée :  
  
```  
[id(0x60020004)]  
HRESULT StructUnkSafe([out, retval] SAFEARRAY(IUnknown*)* pRetVal);  
[id(0x60020005)]  
HRESULT StructDispSafe([out, retval] SAFEARRAY(IDispatch*)* pRetVal);  
```  
  
 Notez que Tlbexp.exe ignore le champ <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArrayUserDefinedSubType>.  
  
 Comme les bibliothèques de types ne peuvent pas contenir toutes les informations figurant dans les assemblys, Tlbexp.exe peut ignorer certaines données au cours du processus d'exportation. Pour plus d’informations sur le processus de transformation et l’identification de la source de chaque information émise vers une bibliothèque de types, consultez [Récapitulatif de la conversion d’un assembly en bibliothèque de types](http://msdn.microsoft.com/library/3a37eefb-a76c-4000-9080-7dbbf66a4896).  
  
 Notez que l'outil Type Library Exporter exporte des méthodes qui ont des paramètres <xref:System.TypedReference> en tant que `VARIANT`, bien que l'objet <xref:System.TypedReference> n'ait aucune signification dans le code non managé. Lorsque vous exportez des méthodes qui ont des paramètres <xref:System.TypedReference>, l'outil Type Library Exporter ne générera aucun avertissement ni aucune erreur et le code non managé qui utilise la bibliothèque de types résultante ne s'exécutera pas correctement.  
  
 L'outil Type Library Exporter est pris en charge sur Microsoft Windows 2000 et les versions ultérieures.  
  
## <a name="examples"></a>Exemples  
 La commande suivante génère une bibliothèque de types portant le même nom que celui de l'assembly figurant dans `myTest.dll`.  
  
```  
tlbexp myTest.dll  
```  
  
 La commande suivante génère une bibliothèque de types portant le nom `clipper.tlb`.  
  
```  
tlbexp myTest.dll /out:clipper.tlb  
```  
  
 L'exemple suivant illustre l'utilisation de Tlbexp.exe pour exporter une bibliothèque de types à partir d'un assembly faisant référence à des assemblys ayant été importés à l'aide de Tlbimp.exe.  
  
 Utilisez d'abord Tlbimp.exe pour importer la bibliothèque de types `myLib.tlb` et enregistrez-la sous `myLib.dll`.  
  
```  
tlbimp myLib.tlb /out:myLib.dll  
```  
  
 La commande suivante utilise le compilateur C# pour compiler `Sample.dll,` faisant référence à `myLib.dll` créé au cours de l'exemple précédent.  
  
```  
CSC Sample.cs /reference:myLib.dll /out:Sample.dll  
```  
  
 La commande suivante génère une bibliothèque de types pour `Sample.dll` faisant référence à `myLib.dll`.  
  
```  
tlbexp Sample.dll  
```  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.Runtime.InteropServices.TypeLibExporterFlags>  
 [Outils](../../../docs/framework/tools/index.md)  
 [Regasm.exe (outil d’inscription d’assemblys)](../../../docs/framework/tools/regasm-exe-assembly-registration-tool.md)  
 [Récapitulatif de la conversion d’un assembly en bibliothèque de types](http://msdn.microsoft.com/library/3a37eefb-a76c-4000-9080-7dbbf66a4896)  
 [Tlbimp.exe (importateur de bibliothèques de types)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md)  
 [Invites de commandes](../../../docs/framework/tools/developer-command-prompt-for-vs.md)
