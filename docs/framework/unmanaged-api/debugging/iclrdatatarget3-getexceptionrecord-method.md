---
title: ICLRDataTarget3::GetExceptionRecord-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
dev_langs:
- cpp
api_name:
- ICLRDataTarget3.GetExceptionRecord
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 6643c2af-2ee6-4789-aa25-1d8eaf500c94
topic_type:
- apiref
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 3e78131eda9d10646a881dbbd4e3f7a4aaf8f607
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="iclrdatatarget3getexceptionrecord-method"></a>ICLRDataTarget3::GetExceptionRecord-Methode
Wird durch die Common Language Runtime (CLR)- Datenzugriffsdienste aufgerufen, um den Ausnahmedatensatz abzurufen, der dem Zielprozess zugordnet ist. Z. B. bei einem, wäre dies entspricht dem Ausnahmedatensatz, der über übergeben der `ExceptionParam` Argument an die [MiniDumpWriteDump](http://msdn.microsoft.com/library/windows/desktop/ms680360.aspx) -Funktion in der Windows Debug-Hilfe-Bibliothek (DbgHelp).  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT GetExceptionRecord(  
    [in] ULONG32 bufferSize,  
    [out] ULONG32* bufferUsed,  
    [out, size_is(bufferSize] BYTE* buffer  
);  
```  
  
#### <a name="parameters"></a>Parameter  
 `bufferSize`  
 [in] Die Eingabepuffergröße, in Bytes. Diese Angabe muss gleich `sizeof(` [MINIDUMP_EXCEPTION](http://msdn.microsoft.com/library/windows/desktop/ms680367.aspx)`)`.  
  
 `bufferUsed`  
 [out] Ein Zeiger auf ein `ULONG32`-Typ, der die Anzahl von Bytes empfängt, die tatsächlich in den Puffer geschrieben werden.  
  
 `buffer`  
 [out] Ein Zeiger zu einem Arbeitsspeicherpuffer, der eine Kopie des Ausnahmedatensatzes empfängt. Der Ausnahmedatensatz wird zurückgegeben, als eine [MINIDUMP_EXCEPTION](http://msdn.microsoft.com/library/windows/desktop/ms680367.aspx) Typ.  
  
## <a name="return-value"></a>Rückgabewert  
 Der Rückgabewert ist `S_OK` bei Erfolg oder ein Fehler-`HRESULT`-Code bei einem Fehler. Zu den `HRESULT`-Codes können u. a. folgende Codes gehören:  
  
|Rückgabecode|Beschreibung|  
|-----------------|-----------------|  
|`S_OK`|Methode war erfolgreich. Der Ausnahmedatensatz ist in den Ausgabepuffer kopiert worden.|  
|`HRESULT_FROM_WIN32(ERROR_NOT_FOUND)`|Kein Ausnahmedatensatz ist dem Ziel zugeordnet.|  
|`HRESULT_FROM_WIN32(ERROR_BAD_LENGTH)`|Die Eingabepuffergröße ist ungleich `sizeof(MINIDUMP_EXCEPTION)`.|  
  
## <a name="remarks"></a>Hinweise  
 [MINIDUMP_EXCEPTION](http://msdn.microsoft.com/library/windows/desktop/ms680367.aspx) ist eine Struktur, die in dbghelp.h und imagehlp.h im Windows SDK definiert.  
  
 Diese Methode wird vom Writer der Debuganwendung implementiert.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** ClrData.idl, ClrData.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:**[!INCLUDE[v451_update](../../../../includes/v451-update-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [ICLRDataTarget3-Schnittstelle](../../../../docs/framework/unmanaged-api/debugging/iclrdatatarget3-interface.md)  
 [GetExceptionContextRecord-Methode](../../../../docs/framework/unmanaged-api/debugging/iclrdatatarget3-getexceptioncontextrecord-method.md)  
 [GetExceptionThreadID-Methode](../../../../docs/framework/unmanaged-api/debugging/iclrdatatarget3-getexceptionthreadid-method.md)
