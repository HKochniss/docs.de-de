---
title: ICorProfilerCallback::ObjectReferences-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name:
- ICorProfilerCallback.ObjectReferences
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ObjectReferences
helpviewer_keywords:
- ObjectReferences method [.NET Framework profiling]
- ICorProfilerCallback::ObjectReferences method [.NET Framework profiling]
ms.assetid: dd5e9b64-b4a3-4ba6-9be6-ddb540f4ffcf
topic_type:
- apiref
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 30b8f6b5f424ff81ace36baa8d2ae39e0a2f1d1e
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="icorprofilercallbackobjectreferences-method"></a>ICorProfilerCallback::ObjectReferences-Methode
Benachrichtigt den Profiler zu Objekten im Arbeitsspeicher, die vom angegebenen Objekt verwiesen wird.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT ObjectReferences(  
    [in]  ObjectID objectId,  
    [in]  ClassID  classId,  
    [in]  ULONG    cObjectRefs,  
    [in, size_is(cObjectRefs)] ObjectID objectRefIds[] );  
```  
  
#### <a name="parameters"></a>Parameter  
 `objectId`  
 [in] Die ID des Objekts, das auf Objekte verwiesen wird.  
  
 `classId`  
 [in] Die ID der Klasse, der das angegebene Objekt eine Instanz ist.  
  
 `cObjectRefs`  
 [in] Die Anzahl der Objekte, die vom angegebenen Objekt verwiesen wird (d. h. die Anzahl der Elemente in der `objectRefIds` Arrays).  
  
 `objectRefIds`  
 [in] Ein Array von IDs von Objekten, die von verwiesen wird, sind `objectId`.  
  
## <a name="remarks"></a>Hinweise  
 Die `ObjectReferences` Methode wird aufgerufen, für die einzelnen Objekte im Heap verbleibt, nachdem eine Garbagecollection abgeschlossen wurde. Wenn der Profiler von diesem Rückruf einen Fehler zurückgibt, werden der Profilerstellungsdienste Aufrufen von diesem Rückruf bis zur nächsten Garbagecollection eingestellt.  
  
 Die `ObjectReferences` Rückruf verwendet werden kann, zusammen mit den [ICorProfilerCallback:: RootReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-rootreferences-method.md) Rückruf, um ein vollständiges Objekt bezugsdiagramm für die Common Language Runtime zu erstellen. Die common Language Runtime (CLR) stellt sicher, dass jeder Objektverweis nur einmal gemeldet haben die `ObjectReferences` Methode.  
  
 Die Objekt-IDs zurückgegebenes `ObjectReferences` sind nicht während des Rückrufs selbst gültig, da die Garbagecollection sein kann, in der Mitte Verschieben von Objekten. Aus diesem Grund müssen Profiler nicht versuchen, Objekte beim Untersuchen einer `ObjectReferences` aufrufen. Wenn [ICorProfilerCallback2:: GarbageCollectionFinished](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback2-garbagecollectionfinished-method.md) aufgerufen wird, wird die Garbage Collection abgeschlossen ist und Überprüfung kann sicher erfolgen.  
  
 Ein NULL-Wert `ClassId` gibt an, dass `objectId` hat einen Typ, der entladen wird.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorProf.idl, CorProf.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [ICorProfilerCallback-Schnittstelle](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
