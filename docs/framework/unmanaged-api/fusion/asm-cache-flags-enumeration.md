---
title: ASM_CACHE_FLAGS-Enumeration
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
- ASM_CACHE_FLAGS
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- ASM_CACHE_FLAGS
helpviewer_keywords:
- ASM_CACHE_FLAGS enumeration [.NET Framework fusion]
ms.assetid: 82e9a7da-321b-48b8-b239-52eaffda6be8
topic_type:
- apiref
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 87dce9a2daf7067409d78a9f389695b6b01f23c6
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="asmcacheflags-enumeration"></a>ASM_CACHE_FLAGS-Enumeration
Gibt die Quelle einer Assembly, die von dargestellte [IAssemblyCacheItem](../../../../docs/framework/unmanaged-api/fusion/iassemblycacheitem-interface.md) im globalen Assemblycache.  
  
## <a name="syntax"></a>Syntax  
  
```  
typedef enum {  
    ASM_CACHE_ZAP       = 0x01,  
    ASM_CACHE_GAC       = 0x02,  
    ASM_CACHE_DOWNLOAD  = 0x04,  
    ASM_CACHE_ROOT      = 0x08  
    ASM_CACHE_ROOT_EX   = 0x80  
} ASM_CACHE_FLAGS;  
```  
  
## <a name="members"></a>Member  
  
|Member|Beschreibung|  
|------------|-----------------|  
|`ASM_CACHE_ZAP`|Listet den Cache von vorkompilierten Assemblys mit Ngen.exe an.|  
|`ASM_CACHE_GAC`|Listet die im globalen Assemblycache.|  
|`ASM_CACHE_DOWNLOAD`|Listet die Assemblys bei Bedarf heruntergeladen wurden oder worden, die Schattenkopie.|  
|`ASM_CACHE_ROOT`|Gibt an, dass die [GetCachePath](../../../../docs/framework/unmanaged-api/fusion/getcachepath-function.md) Funktion sollte den Pfad zurückgeben, im globalen Assemblycache für die common Language Runtime (CLR), Version 2.0. Nur im Kontext eines Aufrufs von [GetCachePath](../../../../docs/framework/unmanaged-api/fusion/getcachepath-function.md).|  
|`ASM_CACHE_ROOT_EX`|Gibt an, dass die [GetCachePath](../../../../docs/framework/unmanaged-api/fusion/getcachepath-function.md) Funktion sollte den Pfad zum globalen Assemblycache für CLR-Version 4 zurückgeben. Nur im Kontext eines Aufrufs von [GetCachePath](../../../../docs/framework/unmanaged-api/fusion/getcachepath-function.md).|  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** Fusion.h  
  
 **Bibliothek:** als Ressource in MsCorEE.dll enthalten  
  
 **.NET Framework-Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [GetCachePath-Funktion](../../../../docs/framework/unmanaged-api/fusion/getcachepath-function.md)  
 [IAssemblyCacheItem-Schnittstelle](../../../../docs/framework/unmanaged-api/fusion/iassemblycacheitem-interface.md)  
 [Fusion-Enumerationen](../../../../docs/framework/unmanaged-api/fusion/fusion-enumerations.md)
