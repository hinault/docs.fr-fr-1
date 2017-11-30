---
title: ICorDebugUnmanagedCallback, interface
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugUnmanagedCallback
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugUnmanagedCallback
helpviewer_keywords: ICorDebugUnmanagedCallback interface [.NET Framework debugging]
ms.assetid: bc71cbca-7d73-40e5-84dd-2109fade3c2a
topic_type: apiref
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: aa104bee5171b3b28731cf18a4d26e32f49169ed
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugunmanagedcallback-interface"></a><span data-ttu-id="f464a-102">ICorDebugUnmanagedCallback, interface</span><span class="sxs-lookup"><span data-stu-id="f464a-102">ICorDebugUnmanagedCallback Interface</span></span>
<span data-ttu-id="f464a-103">Fournit une notification des événements natifs qui ne sont pas directement liées pour le common language runtime (CLR).</span><span class="sxs-lookup"><span data-stu-id="f464a-103">Provides notification of native events that are not directly related to the common language runtime (CLR).</span></span>  
  
## <a name="methods"></a><span data-ttu-id="f464a-104">Méthodes</span><span class="sxs-lookup"><span data-stu-id="f464a-104">Methods</span></span>  
  
|<span data-ttu-id="f464a-105">Méthode</span><span class="sxs-lookup"><span data-stu-id="f464a-105">Method</span></span>|<span data-ttu-id="f464a-106">Description</span><span class="sxs-lookup"><span data-stu-id="f464a-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="f464a-107">DebugEvent (méthode)</span><span class="sxs-lookup"><span data-stu-id="f464a-107">DebugEvent Method</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugunmanagedcallback-debugevent-method.md)|<span data-ttu-id="f464a-108">Notifie le débogueur qu’un événement natif a été déclenché.</span><span class="sxs-lookup"><span data-stu-id="f464a-108">Notifies the debugger that a native event has been fired.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="f464a-109">Remarques</span><span class="sxs-lookup"><span data-stu-id="f464a-109">Remarks</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="f464a-110">Cette interface ne prend pas en charge l'appel à distance, que ce soit entre ordinateurs ou entre processus.</span><span class="sxs-lookup"><span data-stu-id="f464a-110">This interface does not support being called remotely, either cross-machine or cross-process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="f464a-111">Spécifications</span><span class="sxs-lookup"><span data-stu-id="f464a-111">Requirements</span></span>  
 <span data-ttu-id="f464a-112">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="f464a-112">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f464a-113">**En-tête :** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="f464a-113">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="f464a-114">**Bibliothèque :** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="f464a-114">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="f464a-115">**Versions du .NET framework :**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="f464a-115">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f464a-116">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f464a-116">See Also</span></span>  
 [<span data-ttu-id="f464a-117">Interfaces de débogage</span><span class="sxs-lookup"><span data-stu-id="f464a-117">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)