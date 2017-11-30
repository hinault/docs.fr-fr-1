---
title: "ICorDebugAppDomainEnum::Next, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugAppDomainEnum.Next
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugAppDomainEnum::Next method
helpviewer_keywords:
- ICorDebugAppDomainEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugAppDomainEnum interface [.NET Framework debugging]
ms.assetid: b8d1def7-0ebc-4314-a3a2-fd36a75973e7
topic_type: apiref
caps.latest.revision: "12"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 10d53ebac99942ac9376041f217df53965bdbb2f
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugappdomainenumnext-method"></a><span data-ttu-id="f4cfc-102">ICorDebugAppDomainEnum::Next, méthode</span><span class="sxs-lookup"><span data-stu-id="f4cfc-102">ICorDebugAppDomainEnum::Next Method</span></span>
<span data-ttu-id="f4cfc-103">Obtient le nombre spécifié de domaines d’application à partir de la collection, en commençant à la position actuelle du curseur.</span><span class="sxs-lookup"><span data-stu-id="f4cfc-103">Gets the specified number of application domains from the collection, starting at the current cursor position.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="f4cfc-104">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="f4cfc-104">Syntax</span></span>  
  
```  
HRESULT Next (  
    [in] ULONG celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
                           ICorDebugAppDomain *values[],  
    [out] ULONG *pceltFetched  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="f4cfc-105">Paramètres</span><span class="sxs-lookup"><span data-stu-id="f4cfc-105">Parameters</span></span>  
 `celt`  
 <span data-ttu-id="f4cfc-106">[in] Le nombre de domaines d’application à récupérer.</span><span class="sxs-lookup"><span data-stu-id="f4cfc-106">[in] The number of application domains to be retrieved.</span></span>  
  
 `values`  
 <span data-ttu-id="f4cfc-107">[out] Tableau de pointeurs, chacun pointant vers un objet ICorDebugAppDomain qui représente un domaine d’application.</span><span class="sxs-lookup"><span data-stu-id="f4cfc-107">[out] An array of pointers, each of which points to an ICorDebugAppDomain object that represents an application domain.</span></span>  
  
 `pceltFetched`  
 <span data-ttu-id="f4cfc-108">[out] Pointeur vers le nombre de domaines d’application réellement retournés.</span><span class="sxs-lookup"><span data-stu-id="f4cfc-108">[out] A pointer to the number of application domains actually returned.</span></span> <span data-ttu-id="f4cfc-109">Cette valeur peut être null si `celt` fait partie.</span><span class="sxs-lookup"><span data-stu-id="f4cfc-109">This value may be null if `celt` is one.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="f4cfc-110">Spécifications</span><span class="sxs-lookup"><span data-stu-id="f4cfc-110">Requirements</span></span>  
 <span data-ttu-id="f4cfc-111">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="f4cfc-111">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f4cfc-112">**En-tête :** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="f4cfc-112">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="f4cfc-113">**Bibliothèque :** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="f4cfc-113">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="f4cfc-114">**Versions du .NET framework :**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="f4cfc-114">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>