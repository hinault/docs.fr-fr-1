---
title: StackTrace_SimpleContext
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: StackTrace_SimpleContext
api_location: diasymreader.dll
api_type: COM
f1_keywords: SimpleContext
helpviewer_keywords:
- SimpleContext structure [.NET Framework debugging]
- StackTrace_SimpleContext structure [.NET Framework debugging]
ms.assetid: d4cef11f-a8ca-49bc-a1b8-6631f9e28f3e
topic_type: apiref
caps.latest.revision: "13"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 756c1d4129aebedea46443613d286a51562a3896
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2017
---
# <a name="stacktracesimplecontext-structure"></a>StackTrace_SimpleContext
Fournit un contexte simple qui peut être utilisé à la place d'une structure `CONTEXT` complète.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
struct StackTrace_SimpleContext  
{  
    ULONG64 StackOffset;       // ESP on x86  
    ULONG64 FrameOffset;       // EBP on x86  
    ULONG64 InstructionOffset; // EIP on x86  
};  
```  
  
## <a name="members"></a>Membres  
  
|Membre|Description|  
|------------|-----------------|  
|`StackOffset`|Le pointeur de pile, ou le pointeur de pile d’entrée (ESP) sur x86 plateformes.|  
|`FrameOffset`|Offset de frame ou EBP sur x86 les plateformes.|  
|`InstructionOffset`|Le pointeur d’instruction, ou que le pointeur d’instruction (EIP) entrée sur x86 plateformes.|  
  
## <a name="remarks"></a>Notes  
 Étant donné que les fonctions de trace de pile doivent généralement retourner uniquement l’adresse offset de frame et adresse de la pile, vous pouvez éventuellement utiliser le `SimpleContext` structure au lieu d’un grand `CONTEXT` structure.  
  
## <a name="requirements"></a>Configuration requise  
 **Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).  
  
 **En-tête :** SOS_Stacktrace.h  
  
 **Versions du .NET framework :**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Voir aussi  
 [Structures de débogage](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)  
 [Débogage](../../../../docs/framework/unmanaged-api/debugging/index.md)
