---
title: CorFileMapping-Enumeration
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: CorFileMapping
api_location: mscoree.dll
api_type: COM
f1_keywords: CorFileMapping
helpviewer_keywords: CorFileMapping enumeration [.NET Framework metadata]
ms.assetid: 3ca41592-b8da-475a-8032-a15627730003
topic_type: apiref
caps.latest.revision: "8"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 6736f154ef6b03c0bfe34d16a419955324316273
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="corfilemapping-enumeration"></a><span data-ttu-id="0c1f2-102">CorFileMapping-Enumeration</span><span class="sxs-lookup"><span data-stu-id="0c1f2-102">CorFileMapping Enumeration</span></span>
<span data-ttu-id="0c1f2-103">Enthält Werte, die den Dateizuordnungstyp beschreiben, die von einem Aufruf zurückgegeben wird, das [IMetaDataInfo:: GetFileMapping](../../../../docs/framework/unmanaged-api/metadata/imetadatainfo-getfilemapping-method.md) Methode.</span><span class="sxs-lookup"><span data-stu-id="0c1f2-103">Contains values that describe the type of file mapping that is returned from a call to the [IMetaDataInfo::GetFileMapping](../../../../docs/framework/unmanaged-api/metadata/imetadatainfo-getfilemapping-method.md) method.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="0c1f2-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="0c1f2-104">Syntax</span></span>  
  
```  
typedef enum CorFileMapping {  
  
    fmFlat                  =   0x0000,  
    fmExecutableImage       =   0x0001  
  
} CorFileMapping;  
```  
  
## <a name="members"></a><span data-ttu-id="0c1f2-105">Member</span><span class="sxs-lookup"><span data-stu-id="0c1f2-105">Members</span></span>  
  
|<span data-ttu-id="0c1f2-106">Member</span><span class="sxs-lookup"><span data-stu-id="0c1f2-106">Member</span></span>|<span data-ttu-id="0c1f2-107">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="0c1f2-107">Description</span></span>|  
|------------|-----------------|  
|`fmFlat`|<span data-ttu-id="0c1f2-108">Die Datei wird als Datendatei zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="0c1f2-108">The file is mapped as a data file.</span></span> <span data-ttu-id="0c1f2-109">D. h. die `SEC_IMAGE` Flag wurde nicht übergeben, um die Microsoft Win32 `CreateFileMapping` Funktion.</span><span class="sxs-lookup"><span data-stu-id="0c1f2-109">That is, the `SEC_IMAGE` flag was not passed to the Microsoft Win32 `CreateFileMapping` function.</span></span>|  
|`fmExecutableImage`|<span data-ttu-id="0c1f2-110">Die Datei wird zur Ausführung zugeordnet, indem Sie entweder die `LoadLibrary` Funktion oder die `CreateFileMapping` -Funktion mit dem `SEC_IMAGE` Flag.</span><span class="sxs-lookup"><span data-stu-id="0c1f2-110">The file is mapped for execution, by using either the `LoadLibrary` function or the `CreateFileMapping` function with the `SEC_IMAGE` flag.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="0c1f2-111">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="0c1f2-111">Requirements</span></span>  
 <span data-ttu-id="0c1f2-112">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="0c1f2-112">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="0c1f2-113">**Header:** CorHdr.h</span><span class="sxs-lookup"><span data-stu-id="0c1f2-113">**Header:** CorHdr.h</span></span>  
  
 <span data-ttu-id="0c1f2-114">**.NET Framework-Versionen:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="0c1f2-114">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="0c1f2-115">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="0c1f2-115">See Also</span></span>  
 [<span data-ttu-id="0c1f2-116">Metadatenenumerationen</span><span class="sxs-lookup"><span data-stu-id="0c1f2-116">Metadata Enumerations</span></span>](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)  
 [<span data-ttu-id="0c1f2-117">GetFileMapping-Methode</span><span class="sxs-lookup"><span data-stu-id="0c1f2-117">GetFileMapping Method</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadatainfo-getfilemapping-method.md)