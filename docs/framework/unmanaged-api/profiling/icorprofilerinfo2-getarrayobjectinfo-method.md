---
title: ICorProfilerInfo2::GetArrayObjectInfo-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerInfo2.GetArrayObjectInfo
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerInfo2::GetArrayObjectInfo
helpviewer_keywords:
- ICorProfilerInfo2::GetArrayObjectInfo method [.NET Framework profiling]
- GetArrayObjectInfo method [.NET Framework profiling]
ms.assetid: bda75017-739f-4ce5-9000-f3b526e8473c
topic_type: apiref
caps.latest.revision: "11"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 1a1e0c986286483f8236de3a1c73f043691820d5
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="icorprofilerinfo2getarrayobjectinfo-method"></a><span data-ttu-id="85554-102">ICorProfilerInfo2::GetArrayObjectInfo-Methode</span><span class="sxs-lookup"><span data-stu-id="85554-102">ICorProfilerInfo2::GetArrayObjectInfo Method</span></span>
<span data-ttu-id="85554-103">Ruft ausführliche Informationen zu einem Arrayobjekt.</span><span class="sxs-lookup"><span data-stu-id="85554-103">Gets detailed information about an array object.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="85554-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="85554-104">Syntax</span></span>  
  
```  
HRESULT GetArrayObjectInfo(  
    [in] ObjectID objectId,  
    [in] ULONG32 cDimensions,  
    [out, size_is(cDimensions), length_is(cDimensions)] ULONG32 pDimensionSizes[],  
    [out, size_is(cDimensions), length_is(cDimensions)] int pDimensionLowerBounds[],  
    [out] BYTE **ppData);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="85554-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="85554-105">Parameters</span></span>  
 `objectId`  
 <span data-ttu-id="85554-106">[in] Die ID der ein gültiges Array-Objekt.</span><span class="sxs-lookup"><span data-stu-id="85554-106">[in] The ID of a valid array object.</span></span>  
  
 `cDimensions`  
 <span data-ttu-id="85554-107">[in] Der Rang (Anzahl der Dimensionen) des Arrays.</span><span class="sxs-lookup"><span data-stu-id="85554-107">[in] The rank (number of dimensions) of the array.</span></span>  
  
 `pDimensionSizes`  
 <span data-ttu-id="85554-108">[out] Ein Array mit ganzen Zahlen, jede die Größe einer Dimension des Arrays darstellt.</span><span class="sxs-lookup"><span data-stu-id="85554-108">[out] An array that contains integers, each representing the size of a dimension of the array.</span></span>  
  
 `pDimensionLowerBounds`  
 <span data-ttu-id="85554-109">[out] Ein Array, das ganze Zahlen enthält, die jeweils der niedrigere darstellen einer Dimension des Arrays gebunden werden.</span><span class="sxs-lookup"><span data-stu-id="85554-109">[out] An array that contains integers, each representing the lower bound of a dimension of the array.</span></span>  
  
 `ppData`  
 <span data-ttu-id="85554-110">[out] Ein Zeiger auf die Adresse des den unformatierten Puffer für das Array, das gemäß der C++-Konvention angeordnet ist.</span><span class="sxs-lookup"><span data-stu-id="85554-110">[out] A pointer to the address of the raw buffer for the array, which is laid out according to the C++ convention.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="85554-111">Hinweise</span><span class="sxs-lookup"><span data-stu-id="85554-111">Remarks</span></span>  
 <span data-ttu-id="85554-112">Die `pDimensionSizes` und `pDimensionLowerBounds` sind die Elemente, die im gleichen Index in jedem Array Merkmale derselben Entität sind parallele Arrays.</span><span class="sxs-lookup"><span data-stu-id="85554-112">The `pDimensionSizes` and `pDimensionLowerBounds` are parallel arrays, so the elements located at the same index in each array are characteristics of the same entity.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="85554-113">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="85554-113">Requirements</span></span>  
 <span data-ttu-id="85554-114">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="85554-114">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="85554-115">**Header:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="85554-115">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="85554-116">**Bibliothek:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="85554-116">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="85554-117">**.NET Framework-Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="85554-117">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="85554-118">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="85554-118">See Also</span></span>  
 [<span data-ttu-id="85554-119">ICorProfilerInfo-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="85554-119">ICorProfilerInfo Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)  
 [<span data-ttu-id="85554-120">ICorProfilerInfo2-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="85554-120">ICorProfilerInfo2 Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)