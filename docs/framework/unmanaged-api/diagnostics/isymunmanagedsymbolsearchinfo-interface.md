---
title: ISymUnmanagedSymbolSearchInfo, interface
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ISymUnmanagedSymbolSearchInfo
api_location: diasymreader.dll
api_type: COM
f1_keywords: ISymUnmanagedSymbolSearchInfo
helpviewer_keywords: ISymUnmanagedSymbolSearchInfo interface [.NET Framework debugging]
ms.assetid: 30817373-0a21-49c1-a0c4-8e8daeecb8db
topic_type: apiref
caps.latest.revision: "6"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 967511238dceb752ab30ce10dcaba8b65f4dd9fb
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2017
---
# <a name="isymunmanagedsymbolsearchinfo-interface"></a><span data-ttu-id="746eb-102">ISymUnmanagedSymbolSearchInfo, interface</span><span class="sxs-lookup"><span data-stu-id="746eb-102">ISymUnmanagedSymbolSearchInfo Interface</span></span>
<span data-ttu-id="746eb-103">Fournit des méthodes qui obtiennent des informations sur le chemin de recherche.</span><span class="sxs-lookup"><span data-stu-id="746eb-103">Provides methods that get information about the search path.</span></span> <span data-ttu-id="746eb-104">Obtenez cette interface en appelant `QueryInterface` sur un objet qui implémente le [ISymUnmanagedReader](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-interface.md) interface.</span><span class="sxs-lookup"><span data-stu-id="746eb-104">Obtain this interface by calling `QueryInterface` on an object that implements the [ISymUnmanagedReader](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedreader-interface.md) interface.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="746eb-105">Méthodes</span><span class="sxs-lookup"><span data-stu-id="746eb-105">Methods</span></span>  
  
|<span data-ttu-id="746eb-106">Méthode</span><span class="sxs-lookup"><span data-stu-id="746eb-106">Method</span></span>|<span data-ttu-id="746eb-107">Description</span><span class="sxs-lookup"><span data-stu-id="746eb-107">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="746eb-108">GetHRESULT (méthode)</span><span class="sxs-lookup"><span data-stu-id="746eb-108">GetHRESULT Method</span></span>](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedsymbolsearchinfo-gethresult-method.md)|<span data-ttu-id="746eb-109">Obtient la valeur HRESULT.</span><span class="sxs-lookup"><span data-stu-id="746eb-109">Gets the HRESULT.</span></span>|  
|[<span data-ttu-id="746eb-110">GetSearchPath (méthode)</span><span class="sxs-lookup"><span data-stu-id="746eb-110">GetSearchPath Method</span></span>](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedsymbolsearchinfo-getsearchpath-method.md)|<span data-ttu-id="746eb-111">Obtient le chemin de recherche.</span><span class="sxs-lookup"><span data-stu-id="746eb-111">Gets the search path.</span></span>|  
|[<span data-ttu-id="746eb-112">GetSearchPathLength (méthode)</span><span class="sxs-lookup"><span data-stu-id="746eb-112">GetSearchPathLength Method</span></span>](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedsymbolsearchinfo-getsearchpathlength-method.md)|<span data-ttu-id="746eb-113">Obtient la longueur de chemin d’accès de recherche.</span><span class="sxs-lookup"><span data-stu-id="746eb-113">Gets the search path length.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="746eb-114">Spécifications</span><span class="sxs-lookup"><span data-stu-id="746eb-114">Requirements</span></span>  
 <span data-ttu-id="746eb-115">**En-tête :** CorSym.idl, CorSym.h</span><span class="sxs-lookup"><span data-stu-id="746eb-115">**Header:** CorSym.idl, CorSym.h</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="746eb-116">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="746eb-116">See Also</span></span>  
 [<span data-ttu-id="746eb-117">Interfaces du magasin de symboles de Diagnostics</span><span class="sxs-lookup"><span data-stu-id="746eb-117">Diagnostics Symbol Store Interfaces</span></span>](../../../../docs/framework/unmanaged-api/diagnostics/diagnostics-symbol-store-interfaces.md)