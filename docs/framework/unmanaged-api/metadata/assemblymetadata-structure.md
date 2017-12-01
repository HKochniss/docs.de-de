---
title: ASSEMBLYMETADATA-Struktur
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ASSEMBLYMETADATA
api_location: mscoree.dll
api_type: COM
f1_keywords: ASSEMBLYMETADATA
helpviewer_keywords: ASSEMBLYMETADATA structure [.NET Framework metadata]
ms.assetid: 1af98e57-9145-4d35-bb78-77d1da7c91a5
topic_type: apiref
caps.latest.revision: "12"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 5652907abc17868414c554cb5c87b0856d2c5a0c
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="assemblymetadata-structure"></a><span data-ttu-id="3855c-102">ASSEMBLYMETADATA-Struktur</span><span class="sxs-lookup"><span data-stu-id="3855c-102">ASSEMBLYMETADATA Structure</span></span>
<span data-ttu-id="3855c-103">Enthält Informationen über die referenzierte Assembly, z. B. die Version und die Ebene der Unterstützung für Gebietsschemas, Prozessoren und Betriebssysteme an.</span><span class="sxs-lookup"><span data-stu-id="3855c-103">Contains information about the referenced assembly, including its version and its level of support for locales, processors, and operating systems.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="3855c-104">Syntax</span><span class="sxs-lookup"><span data-stu-id="3855c-104">Syntax</span></span>  
  
```  
typedef struct {  
    USHORT  usMajorVersion;  
    USHORT  usMinorVersion;  
    USHORT  usBuildNumber;  
    USHORT  usRevisionNumber;  
    LPWSTR  szLocale;  
    ULONG   cbLocale;  
    DWORD*  rdwProcessor[];  
    ULONG   ulProcessor  
    OSINFO* rOS[];  
    ULONG   ulOS;  
} ASSEMBLYMETADATA;  
```  
  
## <a name="members"></a><span data-ttu-id="3855c-105">Member</span><span class="sxs-lookup"><span data-stu-id="3855c-105">Members</span></span>  
  
|<span data-ttu-id="3855c-106">Member</span><span class="sxs-lookup"><span data-stu-id="3855c-106">Member</span></span>|<span data-ttu-id="3855c-107">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="3855c-107">Description</span></span>|  
|------------|-----------------|  
|`usMajorVersion`|<span data-ttu-id="3855c-108">Die Hauptversionsnummer der Assembly, auf die verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="3855c-108">The major version number of the referenced assembly.</span></span> <span data-ttu-id="3855c-109">Dieser Wert darf nicht 0 (null) sein.</span><span class="sxs-lookup"><span data-stu-id="3855c-109">This value cannot be zero.</span></span> <span data-ttu-id="3855c-110">Wenn die Bits des `usMajorVersion` festgelegt ist, wird die Hauptversion nicht angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="3855c-110">If all the bits of `usMajorVersion` are set, the major version is not specified.</span></span>|  
|`usMinorVersion`|<span data-ttu-id="3855c-111">Die Nebenversionsnummer der Assembly, auf die verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="3855c-111">The minor version number of the referenced assembly.</span></span> <span data-ttu-id="3855c-112">Dieser Wert darf nicht 0 (null) sein.</span><span class="sxs-lookup"><span data-stu-id="3855c-112">This value cannot be zero.</span></span> <span data-ttu-id="3855c-113">Wenn die Bits des `usMinorVersion` festgelegt ist, wird die Nebenversion nicht angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="3855c-113">If all the bits of `usMinorVersion` are set, the minor version is not specified.</span></span>|  
|`usBuildNumber`|<span data-ttu-id="3855c-114">Die Buildnummer der Assembly, auf die verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="3855c-114">The build number of the referenced assembly.</span></span> <span data-ttu-id="3855c-115">Dieser Wert darf nicht 0 (null) sein.</span><span class="sxs-lookup"><span data-stu-id="3855c-115">This value cannot be zero.</span></span> <span data-ttu-id="3855c-116">Wenn die Bits des `usBuildNumber` festgelegt ist, wird die Buildnummer nicht angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="3855c-116">If all the bits of `usBuildNumber` are set, the build number is not specified.</span></span>|  
|`usRevisionNumber`|<span data-ttu-id="3855c-117">Die Revisionsnummer der Assembly, auf die verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="3855c-117">The revision number of the referenced assembly.</span></span> <span data-ttu-id="3855c-118">Dieser Wert darf nicht 0 (null) sein.</span><span class="sxs-lookup"><span data-stu-id="3855c-118">This value cannot be zero.</span></span> <span data-ttu-id="3855c-119">Wenn die Bits des `usRevisionNumber` festgelegt ist, wird die Revisionsnummer nicht angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="3855c-119">If all the bits of `usRevisionNumber` are set, the revision number is not specified.</span></span>|  
|`szLocale`|<span data-ttu-id="3855c-120">Eine Liste der Gebietsschemanamen RFC1766-Spezifikation, die durch Semikolons getrennt, Angeben der zu unterstützenden Gebietsschemas durch die referenzierte Assembly unterstützt.</span><span class="sxs-lookup"><span data-stu-id="3855c-120">A list of locale names conforming to the RFC1766 specification, separated by semicolons, specifying the locales supported by the referenced assembly.</span></span> <span data-ttu-id="3855c-121">Ein Nullwert zeigt Gebietsschemaunabhängigkeit an.</span><span class="sxs-lookup"><span data-stu-id="3855c-121">A null value indicates locale independence.</span></span> <span data-ttu-id="3855c-122">**Hinweis:** In .NET Framework, Version 1.0, die Sie nicht mehr als ein Gebietsschema angeben.</span><span class="sxs-lookup"><span data-stu-id="3855c-122">**Note:**  In the .NET Framework version 1.0 you cannot specify more than one locale.</span></span>|  
|`cbLocale`|<span data-ttu-id="3855c-123">Die Größe in Breitzeichen `szLocale`.</span><span class="sxs-lookup"><span data-stu-id="3855c-123">The size in wide characters of `szLocale`.</span></span>|  
|`rdwProcessor`|<span data-ttu-id="3855c-124">Ein Array von Bezeichnern, gemäß der Definition in "Winnt.h", für die Prozessortypen, die durch die referenzierte Assembly unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="3855c-124">An array of identifiers, as defined in Winnt.h, for the processor types that are supported by the referenced assembly.</span></span> <span data-ttu-id="3855c-125">Ein NULL-Wert gibt die Prozessorunabhängigkeit an.</span><span class="sxs-lookup"><span data-stu-id="3855c-125">A NULL value indicates processor independence.</span></span>|  
|`ulProcessor`|<span data-ttu-id="3855c-126">Die Länge der `rdwProcessor` Array.</span><span class="sxs-lookup"><span data-stu-id="3855c-126">The length of the `rdwProcessor` array.</span></span>|  
|`rOS`|<span data-ttu-id="3855c-127">Ein Array von [OSINFO](../../../../docs/framework/unmanaged-api/metadata/osinfo-structure.md) Instanzen angeben, die Betriebssysteme, die durch die referenzierte Assembly unterstützt werden.</span><span class="sxs-lookup"><span data-stu-id="3855c-127">An array of [OSINFO](../../../../docs/framework/unmanaged-api/metadata/osinfo-structure.md) instances specifying the operating systems that are supported by the referenced assembly.</span></span> <span data-ttu-id="3855c-128">Ein NULL-Wert gibt die Unabhängigkeit des Betriebssystems an.</span><span class="sxs-lookup"><span data-stu-id="3855c-128">A NULL value indicates operating-system independence.</span></span>|  
|`ulOS`|<span data-ttu-id="3855c-129">Die Länge der `rOS` Array.</span><span class="sxs-lookup"><span data-stu-id="3855c-129">The length of the `rOS` array.</span></span>|  
  
## <a name="requirements"></a><span data-ttu-id="3855c-130">Anforderungen</span><span class="sxs-lookup"><span data-stu-id="3855c-130">Requirements</span></span>  
 <span data-ttu-id="3855c-131">**Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="3855c-131">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="3855c-132">**Header:** Cor.h</span><span class="sxs-lookup"><span data-stu-id="3855c-132">**Header:** Cor.h</span></span>  
  
 <span data-ttu-id="3855c-133">**Bibliothek:** als Ressource in MsCorEE.dll verwendet</span><span class="sxs-lookup"><span data-stu-id="3855c-133">**Library:** Used as a resource in MsCorEE.dll</span></span>  
  
 <span data-ttu-id="3855c-134">**.NET Framework-Versionen:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="3855c-134">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="3855c-135">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="3855c-135">See Also</span></span>  
 [<span data-ttu-id="3855c-136">Metadatenstrukturen</span><span class="sxs-lookup"><span data-stu-id="3855c-136">Metadata Structures</span></span>](../../../../docs/framework/unmanaged-api/metadata/metadata-structures.md)  
 [<span data-ttu-id="3855c-137">IMetaDataAssemblyEmit-Schnittstelle</span><span class="sxs-lookup"><span data-stu-id="3855c-137">IMetaDataAssemblyEmit Interface</span></span>](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-interface.md)  
 [<span data-ttu-id="3855c-138">OSINFO-Struktur</span><span class="sxs-lookup"><span data-stu-id="3855c-138">OSINFO Structure</span></span>](../../../../docs/framework/unmanaged-api/metadata/osinfo-structure.md)