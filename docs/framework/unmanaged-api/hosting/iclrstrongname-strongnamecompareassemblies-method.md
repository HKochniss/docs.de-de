---
title: ICLRStrongName::StrongNameCompareAssemblies-Methode
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
- ICLRStrongName.StrongNameCompareAssemblies
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameCompareAssemblies
helpviewer_keywords:
- ICLRStrongName::StrongNameCompareAssemblies method [.NET Framework hosting]
- StrongNameCompareAssemblies method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: b1fb356c-72cf-4aa4-8376-f291a6d97c01
topic_type:
- apiref
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 96fbeccf76de87a3582bf8c2084d0ca9ad7d27f4
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="iclrstrongnamestrongnamecompareassemblies-method"></a>ICLRStrongName::StrongNameCompareAssemblies-Methode
Bestimmt, ob zwei Assemblys nur durch die Signaturen ihrer starken Namen unterscheiden.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT StrongNameCompareAssemblies (  
    [in]  LPCWSTR   wszAssembly1,  
    [in]  LPCWSTR   wszAssembly2,  
    [out] DWORD     *pdwResult  
);  
```  
  
#### <a name="parameters"></a>Parameter  
 `wszAssembly1`  
 [in] Der Pfad zur ersten Assembly.  
  
 `wszAssembly2`  
 [in] Der Pfad auf die zweite Assembly.  
  
 `pdwResult`  
 [out] Einer der folgenden Werte:  
  
-   `SN_CMP_DIFFERENT`(0) – gibt an, dass die Assemblys verschiedene Daten enthalten.  
  
-   `SN_CMP_IDENTICAL`(1) – gibt an, dass die Assemblys identisch, einschließlich ihrer Signaturen und die Prüfsumme sind.  
  
-   `SN_CMP_SIGONLY`(2) – gibt an, dass die Assemblys nur durch Signatur und Prüfsumme unterscheiden.  
  
## <a name="return-value"></a>Rückgabewert  
 `S_OK`Wenn die Methode erfolgreich abgeschlossen. andernfalls ein HRESULT-Wert, der Fehler weist darauf hin (finden Sie unter [häufig auftretende HRESULT-Werte](http://go.microsoft.com/fwlink/?LinkId=213878) eine Liste).  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** MetaHost.h  
  
 **Bibliothek:** als Ressource in MSCorEE.dll enthalten  
  
 **.NET Framework-Versionen:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="remarks"></a>Hinweise  
 Die starke Namenssignatur einer Assembly besteht aus der Assembly aneinander gehängt Textnamen, Version, Kultur und öffentliches Schlüsseltoken.  
  
## <a name="see-also"></a>Siehe auch  
 [ICLRStrongName-Schnittstelle](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
