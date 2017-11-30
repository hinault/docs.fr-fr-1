---
title: "ICorProfilerInfo7::ApplyMetaData (méthode)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: cpp
api_name: ICorProfilerInfo7.ApplyMetaData
api_location: mscorwks.dll
api_type: COM
ms.assetid: a1bfb649-4584-4d35-b3e6-8fe59b53992a
caps.latest.revision: "4"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: e3724555df58392e5ab59ccb4f52dd2de860b8d4
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="icorprofilerinfo7applymetadata-method"></a><span data-ttu-id="baabb-102">ICorProfilerInfo7::ApplyMetaData (méthode)</span><span class="sxs-lookup"><span data-stu-id="baabb-102">ICorProfilerInfo7::ApplyMetaData Method</span></span>
<span data-ttu-id="baabb-103">[Prise en charge dans le .NET Framework 4.6.1 et versions ultérieures]</span><span class="sxs-lookup"><span data-stu-id="baabb-103">[Supported in the .NET Framework 4.6.1 and later versions]</span></span>  
  
 <span data-ttu-id="baabb-104">Applique les métadonnées qui vient d’être définie par le `IMetadataEmit::Define*` méthodes à un module spécifié.</span><span class="sxs-lookup"><span data-stu-id="baabb-104">Applies the metadata newly defined by the `IMetadataEmit::Define*` methods to a specified module.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="baabb-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="baabb-105">Syntax</span></span>  
  
```cpp
HRESULT ApplyMetaData(  
        [in] ModuleID moduleID  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="baabb-106">Paramètres</span><span class="sxs-lookup"><span data-stu-id="baabb-106">Parameters</span></span>  
 `moduleID`  
 <span data-ttu-id="baabb-107">[in] Identificateur du module dont les métadonnées a été modifiée.</span><span class="sxs-lookup"><span data-stu-id="baabb-107">[in] The identifier of the module whose metadata was changed.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="baabb-108">Remarques</span><span class="sxs-lookup"><span data-stu-id="baabb-108">Remarks</span></span>  
 <span data-ttu-id="baabb-109">Si des modifications apportées aux métadonnées sont apportées après le [ModuleLoadFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleloadfinished-method.md) rappel, vous devez appeler cette méthode avant d’utiliser les nouvelles métadonnées.</span><span class="sxs-lookup"><span data-stu-id="baabb-109">If metadata changes are made after the [ModuleLoadFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-moduleloadfinished-method.md) callback, you must call this method before using the new metadata.</span></span>  
  
 <span data-ttu-id="baabb-110">`ApplyMetaData`prend en charge uniquement ajouter les types de métadonnées suivants :</span><span class="sxs-lookup"><span data-stu-id="baabb-110">`ApplyMetaData` only supports adding the following types of metadata:</span></span>  
  
-   <span data-ttu-id="baabb-111">`AssemblyRef`enregistrements que vous créez en appelant le [IMetaDataAssemblyEmit::DefineAssemblyRef](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-defineassemblyref-method.md).</span><span class="sxs-lookup"><span data-stu-id="baabb-111">`AssemblyRef` records, which you create by calling the [IMetaDataAssemblyEmit::DefineAssemblyRef](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-defineassemblyref-method.md).</span></span> <span data-ttu-id="baabb-112">.</span><span class="sxs-lookup"><span data-stu-id="baabb-112">method.</span></span>  
  
-   <span data-ttu-id="baabb-113">`TypeRef`enregistrements que vous créez en appelant le [IMetaDataEmit::DefineTypeRefByName](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definetyperefbyname-method.md) (méthode).</span><span class="sxs-lookup"><span data-stu-id="baabb-113">`TypeRef` records, which you create by calling the [IMetaDataEmit::DefineTypeRefByName](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definetyperefbyname-method.md) method.</span></span>  
  
-   <span data-ttu-id="baabb-114">`TypeSpec`enregistrements que vous créez en appelant le [IMetaDataEmit::GetTokenFromTypeSpec](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-gettokenfromtypespec-method.md) (méthode).</span><span class="sxs-lookup"><span data-stu-id="baabb-114">`TypeSpec` records, which you create by calling the [IMetaDataEmit::GetTokenFromTypeSpec](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-gettokenfromtypespec-method.md) method.</span></span>  
  
-   <span data-ttu-id="baabb-115">`MemberRef`enregistrements que vous créez en appelant le [IMetaDataEmit::DefineMemberRef](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definememberref-method.md) (méthode).</span><span class="sxs-lookup"><span data-stu-id="baabb-115">`MemberRef` records, which you create by calling the [IMetaDataEmit::DefineMemberRef](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definememberref-method.md) method.</span></span>  
  
-   <span data-ttu-id="baabb-116">`MemberSpec`enregistrements que vous créez en appelant le [IMetaDataEmit2::DefineMethodSpec](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-definemethodspec-method.md) (méthode).</span><span class="sxs-lookup"><span data-stu-id="baabb-116">`MemberSpec` records, which you create by calling the [IMetaDataEmit2::DefineMethodSpec](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-definemethodspec-method.md) method.</span></span>  
  
-   <span data-ttu-id="baabb-117">`UserString`enregistrements que vous créez en appelant le [IMetaDataEmit::DefineUserString](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-defineuserstring-method.md) (méthode).</span><span class="sxs-lookup"><span data-stu-id="baabb-117">`UserString` records, which you create by calling the [IMetaDataEmit::DefineUserString](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-defineuserstring-method.md) method.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="baabb-118">Spécifications</span><span class="sxs-lookup"><span data-stu-id="baabb-118">Requirements</span></span>  
 <span data-ttu-id="baabb-119">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="baabb-119">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="baabb-120">**En-tête :** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="baabb-120">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="baabb-121">**Bibliothèque :** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="baabb-121">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="baabb-122">**Versions du .NET Framework :** [!INCLUDE[net_current_v461plus](../../../../includes/net-current-v461plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="baabb-122">**.NET Framework Versions:** [!INCLUDE[net_current_v461plus](../../../../includes/net-current-v461plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="baabb-123">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="baabb-123">See Also</span></span>  
 [<span data-ttu-id="baabb-124">Interface de ICorProfilerInfo7</span><span class="sxs-lookup"><span data-stu-id="baabb-124">ICorProfilerInfo7 Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo7-interface.md)