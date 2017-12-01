---
title: CorDebugUnmappedStop-Enumeration
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: CorDebugUnmappedStop
api_location: mscordbi.dll
api_type: COM
f1_keywords: CorDebugUnmappedStop
helpviewer_keywords: CorDebugUnmappedStop enumeration [.NET Framework debugging]
ms.assetid: a684f7d7-d0c2-4690-b721-639e613f11f8
topic_type: apiref
caps.latest.revision: "10"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: e75c827533a921c4cab31b2e8b0996dffa532fe2
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="cordebugunmappedstop-enumeration"></a><span data-ttu-id="7d44a-102">CorDebugUnmappedStop-Enumeration</span><span class="sxs-lookup"><span data-stu-id="7d44a-102">CorDebugUnmappedStop Enumeration</span></span>
<span data-ttu-id="7d44a-103">Gibt den Typ von nicht zugeordnetem Code an, der eine Unterbrechung der Codeausführung durch die Schritte auslösen kann.</span><span class="sxs-lookup"><span data-stu-id="7d44a-103">Specifies the type of unmapped code that can trigger a halt in code execution by the stepper.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="7d44a-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="7d44a-104">Syntax</span></span>  
  
```  
typedef enum CorDebugUnmappedStop {  
    STOP_NONE               = 0x0,  
    STOP_PROLOG             = 0x01,  
    STOP_EPILOG             = 0x02,  
    STOP_NO_MAPPING_INFO    = 0x04,  
    STOP_OTHER_UNMAPPED     = 0x08,  
    STOP_UNMANAGED          = 0x10,  
    STOP_ALL                = 0xffff,  
} CorDebugUnmappedStop;  
```  
  
## <a name="members"></a><span data-ttu-id="7d44a-105">Member</span><span class="sxs-lookup"><span data-stu-id="7d44a-105">Members</span></span>  
  
|<span data-ttu-id="7d44a-106">Member</span><span class="sxs-lookup"><span data-stu-id="7d44a-106">Member</span></span>|<span data-ttu-id="7d44a-107">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7d44a-107">Description</span></span>|  
|------------|-----------------|  
|`STOP_NONE`|<span data-ttu-id="7d44a-108">Nicht in jedem Typ von nicht zugeordnetem Code beendet.</span><span class="sxs-lookup"><span data-stu-id="7d44a-108">Do not stop in any type of unmapped code.</span></span>|  
|`STOP_PROLOG`|<span data-ttu-id="7d44a-109">In Prologcode anhalten.</span><span class="sxs-lookup"><span data-stu-id="7d44a-109">Stop in prolog code.</span></span>|  
|`STOP_EPILOG`|<span data-ttu-id="7d44a-110">Beenden Sie im Epilogcode.</span><span class="sxs-lookup"><span data-stu-id="7d44a-110">Stop in epilog code.</span></span>|  
|`STOP_NO_MAPPING_INFO`|<span data-ttu-id="7d44a-111">Beenden Sie im Code, der keine Zuordnungsinformationen enthält.</span><span class="sxs-lookup"><span data-stu-id="7d44a-111">Stop in code that has no mapping information.</span></span>|  
|`STOP_OTHER_UNMAPPED`|<span data-ttu-id="7d44a-112">Beenden Sie nicht zugeordnetem Code an, die nicht in der Prolog, Epilog, keine Zuordnungsinformationen oder nicht verwalteten Kategorien passen.</span><span class="sxs-lookup"><span data-stu-id="7d44a-112">Stop in unmapped code that does not fit into the prolog, epilog, no-mapping-information, or unmanaged category.</span></span>|  
|`STOP_UNMANAGED`|<span data-ttu-id="7d44a-113">Beenden Sie in nicht verwaltetem Code.</span><span class="sxs-lookup"><span data-stu-id="7d44a-113">Stop in unmanaged code.</span></span> <span data-ttu-id="7d44a-114">Dieser Wert ist nur gültig, wenn Interop-Debuggen.</span><span class="sxs-lookup"><span data-stu-id="7d44a-114">This value is valid only with interop debugging.</span></span>|  
|`STOP_ALL`|<span data-ttu-id="7d44a-115">Beenden Sie in allen Typen von nicht zugeordnetem Code an.</span><span class="sxs-lookup"><span data-stu-id="7d44a-115">Stop in all types of unmapped code.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="7d44a-116">Hinweise</span><span class="sxs-lookup"><span data-stu-id="7d44a-116">Remarks</span></span>  
 <span data-ttu-id="7d44a-117">Verwenden der [ICorDebugStepper:: SetUnmappedStopMask](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setunmappedstopmask-method.md) Methode, um die Flags festzulegen, nicht zugeordneten Code angeben, in dem die zugeordnetem wird beendet.</span><span class="sxs-lookup"><span data-stu-id="7d44a-117">Use the [ICorDebugStepper::SetUnmappedStopMask](../../../../docs/framework/unmanaged-api/debugging/icordebugstepper-setunmappedstopmask-method.md) method to set the flags that specify the unmapped code in which the stepper will stop.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="7d44a-118">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="7d44a-118">Requirements</span></span>  
 <span data-ttu-id="7d44a-119">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="7d44a-119">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="7d44a-120">**Header:** CorDebug.idl, CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="7d44a-120">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="7d44a-121">**Bibliothek:** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="7d44a-121">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="7d44a-122">**.NET Framework-Versionen:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="7d44a-122">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7d44a-123">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="7d44a-123">See Also</span></span>  
 [<span data-ttu-id="7d44a-124">Debuggen von Enumerationen</span><span class="sxs-lookup"><span data-stu-id="7d44a-124">Debugging Enumerations</span></span>](../../../../docs/framework/unmanaged-api/debugging/debugging-enumerations.md)