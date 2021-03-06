---
title: IManagedObject::GetObjectIdentity-Methode
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
- IManagedObject.GetObjectIdentity
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- GetObjectIdentity
helpviewer_keywords:
- GetObjectIdentity method [.NET Framework hosting]
- IManagedObject::GetObjectIdentity method [.NET Framework hosting]
ms.assetid: b862ff3e-e480-4cdf-84e2-e1013334a467
topic_type:
- apiref
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: c5654865c557e6e004685f66753366d7cb575919
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="imanagedobjectgetobjectidentity-method"></a>IManagedObject::GetObjectIdentity-Methode
Ruft die Identität dieses verwalteten Objekts ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT GetObjectIdentity (  
    [out] BSTR*   pBSTRGUID,  
    [out] int*    AppDomainID,  
    [out] CCW_PTR pCCW  
);  
```  
  
#### <a name="parameters"></a>Parameter  
 `pBSTRGUID`  
 [out] Ein Zeiger auf die GUID des Prozesses, in dem sich das Objekt befindet.  
  
 `AppDomainID`  
 [out] Ein Zeiger auf die ID der Anwendungsdomäne des Objekts.  
  
 `pCCW`  
 [out] Ein Zeiger auf den Index des Objekts, in der klassischen COM-V-Tabelle.  
  
## <a name="remarks"></a>Hinweise  
 Die Identität eines verwalteten Objekts enthält die Prozess-GUID, Anwendungsdomänen-ID und der Index des Objekts in der klassischen COM-V-Tabelle.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** MSCorEE.h  
  
 **Bibliothek:** als Ressource in MSCorEE.dll enthalten  
  
 **.NET Framework-Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [IManagedObject-Schnittstelle](../../../../docs/framework/unmanaged-api/hosting/imanagedobject-interface.md)
