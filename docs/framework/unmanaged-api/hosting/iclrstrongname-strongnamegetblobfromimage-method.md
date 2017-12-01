---
title: ICLRStrongName::StrongNameGetBlobFromImage-Methode
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICLRStrongName.StrongNameGetBlobFromImage
api_location: mscoree.dll
api_type: COM
f1_keywords: ICLRStrongName::StrongNameGetBlobFromImage
helpviewer_keywords:
- StrongNameGetBlobFromImage method, ICLRStrongName interface [.NET Framework hosting]
- ICLRStrongName::StrongNameGetBlobFromImage method [.NET Framework hosting]
ms.assetid: 0f5a2ec8-e776-4fd8-bda6-937b6834575a
topic_type: apiref
caps.latest.revision: "7"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 80edfa333f73854869c3fa6786e038c796b09087
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="iclrstrongnamestrongnamegetblobfromimage-method"></a><span data-ttu-id="3f2b6-102">ICLRStrongName::StrongNameGetBlobFromImage-Methode</span><span class="sxs-lookup"><span data-stu-id="3f2b6-102">ICLRStrongName::StrongNameGetBlobFromImage Method</span></span>
<span data-ttu-id="3f2b6-103">Ruft eine binäre Darstellung des Assemblyabbilds an der angegebenen Speicheradresse.</span><span class="sxs-lookup"><span data-stu-id="3f2b6-103">Gets a binary representation of the assembly image at the specified memory address.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="3f2b6-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="3f2b6-104">Syntax</span></span>  
  
```  
HRESULT StrongNameGetBlobFromImage (  
    [in]  BYTE        *pbBase,  
    [in]  DWORD       dwLength,  
    [in]  BYTE        *pbBlob,  
    [in, out] DWORD   *pcbBlob  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="3f2b6-105">Parameter</span><span class="sxs-lookup"><span data-stu-id="3f2b6-105">Parameters</span></span>  
 `pbBase`  
 <span data-ttu-id="3f2b6-106">[in] Die Speicheradresse des zugeordneten Assemblymanifests.</span><span class="sxs-lookup"><span data-stu-id="3f2b6-106">[in] The memory address of the mapped assembly manifest.</span></span>  
  
 `dwLength`  
 <span data-ttu-id="3f2b6-107">[in] Die Größe in Bytes, der das Abbild `pbBase`.</span><span class="sxs-lookup"><span data-stu-id="3f2b6-107">[in] The size, in bytes, of the image at `pbBase`.</span></span>  
  
 `pbBlob`  
 <span data-ttu-id="3f2b6-108">[in] Ein Puffer, die binäre Darstellung des Bilds enthält.</span><span class="sxs-lookup"><span data-stu-id="3f2b6-108">[in] A buffer to contain the binary representation of the image.</span></span>  
  
 `pcbBlob`  
 <span data-ttu-id="3f2b6-109">[in, out] Die maximale Größe in Bytes, des angeforderten `pbBlob`.</span><span class="sxs-lookup"><span data-stu-id="3f2b6-109">[in, out] The requested maximum size, in bytes, of `pbBlob`.</span></span> <span data-ttu-id="3f2b6-110">Nach der Rückgabe der tatsächlichen Größe in Bytes, der `pbBlob`.</span><span class="sxs-lookup"><span data-stu-id="3f2b6-110">Upon return, the actual size, in bytes, of `pbBlob`.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="3f2b6-111">Rückgabewert</span><span class="sxs-lookup"><span data-stu-id="3f2b6-111">Return Value</span></span>  
 <span data-ttu-id="3f2b6-112">`S_OK`Wenn die Methode erfolgreich abgeschlossen. andernfalls ein HRESULT-Wert, der Fehler weist darauf hin (finden Sie unter [häufig auftretende HRESULT-Werte](http://go.microsoft.com/fwlink/?LinkId=213878) eine Liste).</span><span class="sxs-lookup"><span data-stu-id="3f2b6-112">`S_OK` if the method completed successfully; otherwise, an HRESULT value that indicates failure (see [Common HRESULT Values](http://go.microsoft.com/fwlink/?LinkId=213878) for a list).</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="3f2b6-113">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="3f2b6-113">Requirements</span></span>  
 <span data-ttu-id="3f2b6-114">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="3f2b6-114">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3f2b6-115">**Header:** MetaHost.h</span><span class="sxs-lookup"><span data-stu-id="3f2b6-115">**Header:** MetaHost.h</span></span>  
  
 <span data-ttu-id="3f2b6-116">**Bibliothek:** als Ressource in MSCorEE.dll enthalten</span><span class="sxs-lookup"><span data-stu-id="3f2b6-116">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="3f2b6-117">**.NET Framework-Versionen:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="3f2b6-117">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3f2b6-118">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="3f2b6-118">See Also</span></span>  
 [<span data-ttu-id="3f2b6-119">StrongNameGetBlob-Methode</span><span class="sxs-lookup"><span data-stu-id="3f2b6-119">StrongNameGetBlob Method</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamegetblob-method.md)  
 [<span data-ttu-id="3f2b6-120">ICLRStrongName-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="3f2b6-120">ICLRStrongName Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)