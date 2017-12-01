---
title: IMethodMalloc-Schnittstelle
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IMethodMalloc
api_location: mscorwks.dll
api_type: COM
f1_keywords: IMethodMalloc
helpviewer_keywords: IMethodMalloc interface [.NET Framework profiling]
ms.assetid: 8c8ab5dc-557c-473a-82f2-6e403eca7dac
topic_type: apiref
caps.latest.revision: "12"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: d246f329f80a76d2c93190fd663c7362418385f7
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="imethodmalloc-interface"></a><span data-ttu-id="da6c5-102">IMethodMalloc-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="da6c5-102">IMethodMalloc Interface</span></span>
<span data-ttu-id="da6c5-103">Bietet eine Methode zum Belegen von Arbeitsspeicher für einen neuen Microsoft intermediate Language (MSIL)-Funktionsrumpf.</span><span class="sxs-lookup"><span data-stu-id="da6c5-103">Provides a method to allocate memory for a new Microsoft intermediate language (MSIL) function body.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="da6c5-104">Die `IMethodMalloc` Schnittstelle ist eine einfache Speicherbelegungsfunktion.</span><span class="sxs-lookup"><span data-stu-id="da6c5-104">The `IMethodMalloc` interface is a simple memory allocator.</span></span> <span data-ttu-id="da6c5-105">Sie können Arbeitsspeicher belegt werden, jedoch nicht, um ihn freizugeben.</span><span class="sxs-lookup"><span data-stu-id="da6c5-105">It allows you to allocate memory, but not to free it.</span></span>  
  
## <a name="methods"></a><span data-ttu-id="da6c5-106">Methoden</span><span class="sxs-lookup"><span data-stu-id="da6c5-106">Methods</span></span>  
  
|<span data-ttu-id="da6c5-107">Methode</span><span class="sxs-lookup"><span data-stu-id="da6c5-107">Method</span></span>|<span data-ttu-id="da6c5-108">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="da6c5-108">Description</span></span>|  
|------------|-----------------|  
|[<span data-ttu-id="da6c5-109">Alloc-Methode</span><span class="sxs-lookup"><span data-stu-id="da6c5-109">Alloc Method</span></span>](../../../../docs/framework/unmanaged-api/profiling/imethodmalloc-alloc-method.md)|<span data-ttu-id="da6c5-110">Versucht, eine bestimmte Arbeitsspeichermenge für einen neuen Text des MSIL-Funktion zugeordnet werden.</span><span class="sxs-lookup"><span data-stu-id="da6c5-110">Attempts to allocate a specified amount of memory for a new MSIL function body.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="da6c5-111">Hinweise</span><span class="sxs-lookup"><span data-stu-id="da6c5-111">Remarks</span></span>  
 <span data-ttu-id="da6c5-112">Jede Zuweisung Modul spezifisch ist, und stellt sicher, dass der Hauptteil der Funktion mit einem positiven Offset von der Basisklasse des Moduls werden.</span><span class="sxs-lookup"><span data-stu-id="da6c5-112">Each allocator is module-specific and ensures that the function body will be at a positive offset from the base of the module.</span></span> <span data-ttu-id="da6c5-113">Arbeitsspeicher oberhalb der Basis eines Moduls kann wertvoll sein, damit die Zuweisung zum Reservieren von Speicher nur für einen Funktionsrumpf verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="da6c5-113">Memory above the base of a module can be precious, so the allocator should be used to allocate memory only for a function body.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="da6c5-114">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="da6c5-114">Requirements</span></span>  
 <span data-ttu-id="da6c5-115">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="da6c5-115">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="da6c5-116">**Header:** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="da6c5-116">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="da6c5-117">**Bibliothek:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="da6c5-117">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="da6c5-118">**.NET Framework-Versionen:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="da6c5-118">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="da6c5-119">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="da6c5-119">See Also</span></span>  
 [<span data-ttu-id="da6c5-120">Profilerstellungsschnittstellen</span><span class="sxs-lookup"><span data-stu-id="da6c5-120">Profiling Interfaces</span></span>](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)