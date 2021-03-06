---
title: "ICLRProfiling::AttachProfiler, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IClrProfiling.AttachProfiler Method
api_location: Mscorwks.dll
api_type: COM
f1_keywords: IClrProfiling::AttachProfiler
helpviewer_keywords:
- AttachProfiler method [.NET Framework profiling]
- IClrProfiling::AttachProfiler method [.NET Framework profiling]
ms.assetid: 535a6839-c443-405b-a6f4-e2af90725d5b
topic_type: apiref
caps.latest.revision: "15"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 5b364ab407294b20ac2f2f830e3f875169a18b7b
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2017
---
# <a name="iclrprofilingattachprofiler-method"></a>ICLRProfiling::AttachProfiler, méthode
Attache le profileur spécifié au processus spécifié.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
HRESULT AttachProfiler(  
  [in] DWORD dwProfileeProcessID,  
  [in] DWORD dwMillisecondsMax,                     // optional  
  [in] const CLSID * pClsidProfiler,  
  [in] LPCWSTR wszProfilerPath,                     // optional  
  [in] size_is(cbClientData)] void * pvClientData,  // optional  
  [in] UINT cbClientData);                          // optional  
```  
  
#### <a name="parameters"></a>Paramètres  
 `dwProfileeProcessID`  
 [in] ID du processus auquel le profileur doit être attaché. Sur un ordinateur 64 bits, le nombre de bits du processus profilé doit correspondre au nombre de bits du processus déclencheur qui appelle `AttachProfiler`. Si le compte d'utilisateur sous lequel `AttachProfiler` est appelé dispose de privilèges d'administrateur, le processus cible peut être n'importe quel processus sur le système. Sinon, le processus cible doit appartenir au même compte d'utilisateur.  
  
 `dwMillisecondsMax`  
 [in] Durée d'attente, en millisecondes, pour qu'`AttachProfiler` se termine. Le processus déclencheur doit passer un délai d'attente suffisant pour permettre au profileur spécifique de terminer son initialisation.  
  
 `pClsidProfiler`  
 [in] Pointeur vers le CLSID du profileur à charger. Le processus déclencheur peut réutiliser cette mémoire suite au retour d'`AttachProfiler`.  
  
 `wszProfilerPath`  
 [in] Chemin d’accès complet au fichier DLL du profileur à charger. Cette chaîne ne doit pas comporter plus de 260 caractères, y compris le terminateur null. Si `wszProfilerPath` est null ou une chaîne vide, le Common Language Runtime (CLR) essaie de trouver l'emplacement du fichier DLL du profileur en recherchant le CLSID dans le Registre vers lequel `pClsidProfiler` pointe.  
  
 `pvClientData`  
 [in] Un pointeur vers les données à passer au profileur par la [ICorProfilerCallback3::InitializeForAttach](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback3-initializeforattach-method.md) (méthode). Le processus déclencheur peut réutiliser cette mémoire suite au retour d'`AttachProfiler`. Si `pvClientData` a la valeur null, `cbClientData` doit être égal à 0 (zéro).  
  
 `cbClientData`  
 [in] Taille, en octets, des données vers lesquelles `pvClientData` pointe.  
  
## <a name="return-value"></a>Valeur de retour  
 Cette méthode retourne les HRESULT suivants.  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|Le profileur spécifié est correctement attaché au processus cible.|  
|CORPROF_E_PROFILER_ALREADY_ACTIVE|Un profileur est déjà actif ou en cours d'attachement au processus cible.|  
|CORPROF_E_PROFILER_NOT_ATTACHABLE|Le profileur spécifié ne prend pas en charge l'attachement. Le processus déclencheur peut essayer d'attacher un profileur différent.|  
|CORPROF_E_PROFILEE_INCOMPATIBLE_WITH_TRIGGER|Impossible de demander un attachement de profileur, car la version du processus cible est incompatible avec le processus actuel qui appelle `AttachProfiler`.|  
|HRESULT_FROM_WIN32(ERROR_ACCESS_DENIED)|L'utilisateur du processus déclencheur n'a pas accès au processus cible.|  
|HRESULT_FROM_WIN32(ERROR_PRIVILEGE_NOT_HELD)|L'utilisateur du processus déclencheur ne dispose pas des privilèges nécessaires pour attacher un profileur au processus cible donné. Le journal des événements de l'application peut contenir des d'informations supplémentaires.|  
|CORPROF_E_IPC_FAILED|Un échec s'est produit lors de la communication avec le processus cible. Cela se produit généralement quand le processus cible s'arrête.|  
|HRESULT_FROM_WIN32(ERROR_FILE_NOT_FOUND)|Le processus cible n'existe pas ou n'exécute pas un CLR prenant en charge l'attachement. Cela peut indiquer que le CLR a été déchargé depuis l'appel à la méthode d'énumération du runtime.|  
|HRESULT_FROM_WIN32(ERROR_TIMEOUT)|Le délai d'attente a expiré avant le chargement du profileur. Vous pouvez réessayer l'opération d'attachement. L'expiration d'un délai d'attente se produit quand un finaliseur du processus cible s'exécute plus longtemps que la valeur du délai d'attente.|  
|E_INVALIDARG|Un ou plusieurs paramètres ont des valeurs non valides.|  
|E_FAIL|Un autre échec non spécifié s'est produit.|  
|Autres codes d'erreur|Si du profileur [ICorProfilerCallback3::InitializeForAttach](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback3-initializeforattach-method.md) méthode retourne un HRESULT qui indique un échec, `AttachProfiler` retourne ce même HRESULT. Dans ce cas, E_NOTIMPL est converti en CORPROF_E_PROFILER_NOT_ATTACHABLE.|  
  
## <a name="remarks"></a>Notes  
  
## <a name="memory-management"></a>Gestion de la mémoire  
 Conformément aux conventions COM, l'appelant d'`AttachProfiler` (par exemple, le code déclencheur créé par le développeur du profileur) est chargé de l'allocation et de la libération de la mémoire pour les données vers lesquelles le paramètre `pvClientData` pointe. Quand le CLR exécute l'appel `AttachProfiler`, il fait une copie de la mémoire vers laquelle `pvClientData` pointe et la transmet au processus cible. Quand le CLR à l'intérieur du processus cible reçoit sa propre copie du bloc `pvClientData`, il passe le bloc au générateur de profils via la méthode `InitializeForAttach`, puis libère sa copie du bloc `pvClientData` du processus cible.  
  
## <a name="requirements"></a>Configuration requise  
 **Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).  
  
 **En-tête :** CorProf.idl, CorProf.h  
  
 **Bibliothèque :** CorGuids.lib  
  
 **Versions du .NET framework :**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Voir aussi  
 [ICorProfilerCallback, interface](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)  
 [ICorProfilerInfo3, interface](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-interface.md)  
 [Interfaces de profilage](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
 [Profilage](../../../../docs/framework/unmanaged-api/profiling/index.md)
