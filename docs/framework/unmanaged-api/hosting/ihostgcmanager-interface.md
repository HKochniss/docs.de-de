---
title: IHostGCManager-Schnittstelle
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
- IHostGCManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostGCManager
helpviewer_keywords:
- IHostGCManager interface [.NET Framework hosting]
ms.assetid: 820330a4-244c-4f67-ab5e-f24b0b3c2080
topic_type:
- apiref
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 7452f49df6970bf2ca49781f6a38874186bec64f
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="ihostgcmanager-interface"></a>IHostGCManager-Schnittstelle
Enthält Methoden, die den Host der Ereignisse in die Garbage Collection-Mechanismus implementiert, die von der common Language Runtime (CLR) zu benachrichtigen.  
  
## <a name="members"></a>Member  
  
|Member|Beschreibung|  
|------------|-----------------|  
|[SuspensionEnding-Methode](../../../../docs/framework/unmanaged-api/hosting/ihostgcmanager-suspensionending-method.md)|Benachrichtigt den Host, dass die CLR die Ausführung von Aufgaben in Threads fortgesetzt wird, die für eine Garbagecollection unterbrochen wurden.|  
|[SuspensionStarting-Methode](../../../../docs/framework/unmanaged-api/hosting/ihostgcmanager-suspensionstarting-method.md)|Benachrichtigt den Host, dass die CLR unterbricht die Ausführung von Aufgaben auf, um eine Garbagecollection auszuführen.|  
|[ThreadIsBlockingForSuspension-Methode](../../../../docs/framework/unmanaged-api/hosting/ihostgcmanager-threadisblockingforsuspension-method.md)|Benachrichtigt den Host, der Thread aus dem Aufruf der Methode eingegangen ist, bald für eine Garbagecollection zu blockieren.|  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** MSCorEE.h  
  
 **Bibliothek:** als Ressource in MSCorEE.dll enthalten  
  
 **.NET Framework-Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [ICLRTask-Schnittstelle](../../../../docs/framework/unmanaged-api/hosting/iclrtask-interface.md)  
 [ICLRTaskManager-Schnittstelle](../../../../docs/framework/unmanaged-api/hosting/iclrtaskmanager-interface.md)  
 [IHostTask-Schnittstelle](../../../../docs/framework/unmanaged-api/hosting/ihosttask-interface.md)  
 [IHostTaskManager-Schnittstelle](../../../../docs/framework/unmanaged-api/hosting/ihosttaskmanager-interface.md)  
 [Hosten von Schnittstellen](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
