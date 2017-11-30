---
title: ICorDebugDebugEvent, interface
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: a226737a-cb99-4e97-bd94-9a37094ded41
caps.latest.revision: "4"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: b4422b165f06b60dedff95fc3de58e5627db7fac
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="icordebugdebugevent-interface"></a><span data-ttu-id="f1989-102">ICorDebugDebugEvent, interface</span><span class="sxs-lookup"><span data-stu-id="f1989-102">ICorDebugDebugEvent Interface</span></span>
<span data-ttu-id="f1989-103">Définit l'interface de base de laquelle dérivent tous les événements de débogage `ICorDebug`.</span><span class="sxs-lookup"><span data-stu-id="f1989-103">Defines the base interface from which all `ICorDebug` debug events derive.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="f1989-104">Méthodes</span><span class="sxs-lookup"><span data-stu-id="f1989-104">Methods</span></span>  
  
|<span data-ttu-id="f1989-105">Méthode</span><span class="sxs-lookup"><span data-stu-id="f1989-105">Method</span></span>|<span data-ttu-id="f1989-106">Description</span><span class="sxs-lookup"><span data-stu-id="f1989-106">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="f1989-107">Geteventkind, méthode</span><span class="sxs-lookup"><span data-stu-id="f1989-107">GetEventKind Method</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugdebugevent-geteventkind-method.md)|<span data-ttu-id="f1989-108">Indique le type d'événement représenté par cet objet `ICorDebugDebugEvent`.</span><span class="sxs-lookup"><span data-stu-id="f1989-108">Indicates what kind of event this `ICorDebugDebugEvent` object represents.</span></span>|  
|[<span data-ttu-id="f1989-109">GetThread (méthode)</span><span class="sxs-lookup"><span data-stu-id="f1989-109">GetThread Method</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugdebugevent-getthread-method.md)|<span data-ttu-id="f1989-110">Obtient le thread sur lequel l'événement s'est produit.</span><span class="sxs-lookup"><span data-stu-id="f1989-110">Gets the thread on which the event occurred.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="f1989-111">Remarques</span><span class="sxs-lookup"><span data-stu-id="f1989-111">Remarks</span></span>  
 <span data-ttu-id="f1989-112">Les interfaces suivantes sont dérivées de l'interface `ICorDebugDebugEvent` :</span><span class="sxs-lookup"><span data-stu-id="f1989-112">The following interfaces are derived from the `ICorDebugDebugEvent` interface:</span></span>  
  
-   [<span data-ttu-id="f1989-113">ICorDebugExceptionDebugEvent</span><span class="sxs-lookup"><span data-stu-id="f1989-113">ICorDebugExceptionDebugEvent</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugexceptiondebugevent-interface.md)  
  
-   [<span data-ttu-id="f1989-114">ICorDebugModuleDebugEvent</span><span class="sxs-lookup"><span data-stu-id="f1989-114">ICorDebugModuleDebugEvent</span></span>](../../../../docs/framework/unmanaged-api/debugging/icordebugmoduledebugevent-interface.md)  
  
> [!NOTE]
>  <span data-ttu-id="f1989-115">L'interface est uniquement disponible avec .NET Native.</span><span class="sxs-lookup"><span data-stu-id="f1989-115">The interface is available with .NET Native only.</span></span> <span data-ttu-id="f1989-116">Une tentative d'appel à `QueryInterface` pour récupérer un pointeur d'interface retourne `E_NOINTERFACE` pour les scénarios ICorDebug en dehors de .NET Native.</span><span class="sxs-lookup"><span data-stu-id="f1989-116">Attempting to call `QueryInterface` to retrieve an interface pointer returns `E_NOINTERFACE` for ICorDebug scenarios outside of .NET Native.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="f1989-117">Spécifications</span><span class="sxs-lookup"><span data-stu-id="f1989-117">Requirements</span></span>  
 <span data-ttu-id="f1989-118">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="f1989-118">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="f1989-119">**En-tête :** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="f1989-119">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="f1989-120">**Bibliothèque :** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="f1989-120">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="f1989-121">**Versions du .NET framework :**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span><span class="sxs-lookup"><span data-stu-id="f1989-121">**.NET Framework Versions:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="f1989-122">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f1989-122">See Also</span></span>  
 [<span data-ttu-id="f1989-123">Interfaces de débogage</span><span class="sxs-lookup"><span data-stu-id="f1989-123">Debugging Interfaces</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)  
 [<span data-ttu-id="f1989-124">Débogage</span><span class="sxs-lookup"><span data-stu-id="f1989-124">Debugging</span></span>](../../../../docs/framework/unmanaged-api/debugging/index.md)