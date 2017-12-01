---
title: ICorProfilerInfo2::GetStringLayout-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerInfo2.GetStringLayout
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerInfo2::GetStringLayout
helpviewer_keywords:
- GetStringLayout method [.NET Framework profiling]
- ICorProfilerInfo2::GetStringLayout method [.NET Framework profiling]
ms.assetid: 43189651-a535-4803-a1d1-f1c427ace2ca
topic_type: apiref
caps.latest.revision: "17"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 52a1b9218feb76f7653f747aa52c44284293221f
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="icorprofilerinfo2getstringlayout-method"></a><span data-ttu-id="b16ff-102">ICorProfilerInfo2::GetStringLayout-Methode</span><span class="sxs-lookup"><span data-stu-id="b16ff-102">ICorProfilerInfo2::GetStringLayout Method</span></span>
<span data-ttu-id="b16ff-103">Ruft Informationen zum Layout eines Zeichenfolgenobjekts ab.</span><span class="sxs-lookup"><span data-stu-id="b16ff-103">Gets information about the layout of a string object.</span></span> <span data-ttu-id="b16ff-104">Diese Methode ist veraltet, in der [!INCLUDE[net_v40_long](../../../../includes/net-v40-long-md.md)], und wird durch die [ICorProfilerInfo3:: Getstringlayout2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getstringlayout2-method.md) Methode.</span><span class="sxs-lookup"><span data-stu-id="b16ff-104">This method is deprecated in the [!INCLUDE[net_v40_long](../../../../includes/net-v40-long-md.md)], and is superseded by the [ICorProfilerInfo3::GetStringLayout2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-getstringlayout2-method.md) method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="b16ff-105">Syntax</span><span class="sxs-lookup"><span data-stu-id="b16ff-105">Syntax</span></span>  
  
```  
HRESULT GetStringLayout(  
    [out] ULONG *pBufferLengthOffset,  
    [out] ULONG *pStringLengthOffset,  
    [out] ULONG *pBufferOffset);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="b16ff-106">Parameter</span><span class="sxs-lookup"><span data-stu-id="b16ff-106">Parameters</span></span>  
 `pBufferLengthOffset`  
 <span data-ttu-id="b16ff-107">[out] Ein Zeiger auf den Offset des Speicherorts, relativ zu den `ObjectID` Zeiger, der die Länge der Zeichenfolge speichert.</span><span class="sxs-lookup"><span data-stu-id="b16ff-107">[out] A pointer to the offset of the location, relative to the `ObjectID` pointer, that stores the length of the string.</span></span> <span data-ttu-id="b16ff-108">Die Länge wird gespeichert, als eine `DWORD`.</span><span class="sxs-lookup"><span data-stu-id="b16ff-108">The length is stored as a `DWORD`.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="b16ff-109">Dieser Parameter gibt die Länge der Zeichenfolge selbst und nicht die Länge des Puffers zurück.</span><span class="sxs-lookup"><span data-stu-id="b16ff-109">This parameter returns the length of the string itself, not the length of the buffer.</span></span> <span data-ttu-id="b16ff-110">Die Länge des Puffers ist nicht mehr verfügbar.</span><span class="sxs-lookup"><span data-stu-id="b16ff-110">The length of the buffer is no longer available.</span></span>  
  
 `PStringLengthOffset`  
 <span data-ttu-id="b16ff-111">[out] Ein Zeiger auf den Offset des Speicherorts, relativ zu den `ObjectID` Zeiger, der die Länge der Zeichenfolge selbst speichert.</span><span class="sxs-lookup"><span data-stu-id="b16ff-111">[out] A pointer to the offset of the location, relative to the `ObjectID` pointer, that stores the length of the string itself.</span></span> <span data-ttu-id="b16ff-112">Die Länge wird gespeichert, als eine `DWORD`.</span><span class="sxs-lookup"><span data-stu-id="b16ff-112">The length is stored as a `DWORD`.</span></span>  
  
 `pBufferOffset`  
 <span data-ttu-id="b16ff-113">[out] Ein Zeiger auf den Offset des Puffers, relativ zu den `ObjectID` Zeiger, der die Zeichenfolge mit Breitzeichen speichert.</span><span class="sxs-lookup"><span data-stu-id="b16ff-113">[out] A pointer to the offset of the buffer, relative to the `ObjectID` pointer, that stores the string of wide characters.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="b16ff-114">Hinweise</span><span class="sxs-lookup"><span data-stu-id="b16ff-114">Remarks</span></span>  
 <span data-ttu-id="b16ff-115">Die `GetStringLayout` Methode ruft die Offsets relativ zu den `ObjectID` Zeiger, der die Speicherorte, in denen die folgenden gespeichert werden:</span><span class="sxs-lookup"><span data-stu-id="b16ff-115">The `GetStringLayout` method gets the offsets, relative to the `ObjectID` pointer, of the locations in which the following are stored:</span></span>  
  
-   <span data-ttu-id="b16ff-116">Die Länge des Puffers der Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="b16ff-116">The length of the string's buffer.</span></span>  
  
-   <span data-ttu-id="b16ff-117">Die Länge der Zeichenfolge selbst.</span><span class="sxs-lookup"><span data-stu-id="b16ff-117">The length of the string itself.</span></span>  
  
-   <span data-ttu-id="b16ff-118">Der Puffer, der die tatsächliche Breitzeichen-Zeichenfolge enthält.</span><span class="sxs-lookup"><span data-stu-id="b16ff-118">The buffer that contains the actual string of wide characters.</span></span>  
  
 <span data-ttu-id="b16ff-119">Zeichenfolgen können Null-terminiert sein.</span><span class="sxs-lookup"><span data-stu-id="b16ff-119">Strings may be null-terminated.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="b16ff-120">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="b16ff-120">Requirements</span></span>  
 <span data-ttu-id="b16ff-121">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="b16ff-121">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="b16ff-122">**Header:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="b16ff-122">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="b16ff-123">**Bibliothek:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="b16ff-123">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="b16ff-124">**.NET Framework-Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="b16ff-124">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="b16ff-125">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="b16ff-125">See Also</span></span>  
 [<span data-ttu-id="b16ff-126">ICorProfilerInfo-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="b16ff-126">ICorProfilerInfo Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)  
 [<span data-ttu-id="b16ff-127">ICorProfilerInfo2-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="b16ff-127">ICorProfilerInfo2 Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)