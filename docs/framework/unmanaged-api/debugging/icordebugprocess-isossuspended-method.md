---
title: "ICorDebugProcess::IsOSSuspended, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugProcess.IsOSSuspended
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugProcess::IsOSSuspended
helpviewer_keywords:
- IsOSSuspended method [.NET Framework debugging]
- ICorDebugProcess::IsOSSuspended method [.NET Framework debugging]
ms.assetid: 83406cb2-5797-4402-872d-89c9516aefec
topic_type: apiref
caps.latest.revision: "11"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 97c394e3084007227cf157c62a12df3f5cfac8e6
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2017
---
# <a name="icordebugprocessisossuspended-method"></a>ICorDebugProcess::IsOSSuspended, méthode
Obtient une valeur qui indique si le thread spécifié a été interrompu suite à l’arrêt de ce processus de débogueur.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
HRESULT IsOSSuspended(  
    [in]  DWORD threadID,  
    [out] BOOL  *pbSuspended);  
```  
  
#### <a name="parameters"></a>Paramètres  
 `threadID`  
 [in] L’ID du thread en question.  
  
 `pbSuspended`  
 [out] Un pointeur vers une valeur booléenne qui est `true` si le thread spécifié a été suspendue ; sinon *`pbSuspended` est `false`.  
  
## <a name="remarks"></a>Notes  
 Quand le thread spécifié a été suspendu en raison de l’arrêt de ce processus de débogueur, le compteur de suspension Win32 du thread spécifié est incrémenté d’un. L’interface utilisateur (IU) du débogueur voudrez peut-être prendre en compte ces informations si elle affiche le système d’exploitation (OS) compteur de suspension du thread à l’utilisateur.  
  
 Le `IsOSSuspended` méthode de sens que dans le contexte de débogage non managé. Pendant le débogage managé, les threads sont en coopération suspendu au lieu du système d’exploitation suspendu.  
  
## <a name="requirements"></a>Configuration requise  
 **Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).  
  
 **En-tête :** CorDebug.idl, CorDebug.h  
  
 **Bibliothèque :** CorGuids.lib  
  
 **Versions du .NET framework :**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
