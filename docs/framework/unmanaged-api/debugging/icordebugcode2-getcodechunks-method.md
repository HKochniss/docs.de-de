---
title: ICorDebugCode2::GetCodeChunks-Methode
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
- ICorDebugCode2.GetCodeChunks
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode2::GetCodeChunks
helpviewer_keywords:
- GetCodeChunks method [.NET Framework debugging]
- ICorDebugCode2::GetCodeChunks method [.NET Framework debugging]
ms.assetid: 210a2f02-2678-4555-bc4a-78a0408764c8
topic_type:
- apiref
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 4b90913f05cc2e0a3e98a5890f76a41eb2eafc6d
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="icordebugcode2getcodechunks-method"></a>ICorDebugCode2::GetCodeChunks-Methode
Ruft die Codeabschnitte ab, aus denen dieses Codeobjekt besteht.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT GetCodeChunks (  
    [in]  ULONG32     cbufSize,  
    [out] ULONG32     *pcnumChunks,  
    [out, size_is(cbufSize), length_is(*pcnumChunks)]   
        CodeChunkInfo chunks[]  
);  
```  
  
#### <a name="parameters"></a>Parameter  
 `cbufSize`  
 [in] Größe der `chunks` Array.  
  
 `pcnumChunks`  
 [out] Die Anzahl der Blöcke, die zurückgegeben werden, der `chunks` Array.  
  
 `chunks`  
 [out] Ein Array von "CodeChunkInfo"-Strukturen, von denen jedes einen einzelnen Codeabschnitt darstellt. Wenn der Wert des `cbufSize` gleich 0 ist, dieser Parameter kann null sein.  
  
## <a name="remarks"></a>Hinweise  
 Die Codeabschnitte werden nie überlappen, und befolgen sie die Reihenfolge, in dem sie von verkettet hätte [ICorDebugCode:: GetCode](../../../../docs/framework/unmanaged-api/debugging/icordebugcode-getcode-method.md). Ein Codeobjekt von Microsoft intermediate Language (MSIL) in .NET Framework, Version 2.0 wird ein einzelnes Code-Segment umfassen.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 
