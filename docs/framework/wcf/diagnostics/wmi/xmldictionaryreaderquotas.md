---
title: XmlDictionaryReaderQuotas
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9b4ca8b4-0a89-4758-97ab-528a8ce18f07
caps.latest.revision: "7"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 1a3afb9b8cfede60c773d146f4d1728d7fe02b75
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="xmldictionaryreaderquotas"></a>XmlDictionaryReaderQuotas
XmlDictionaryReaderQuotas  
  
## <a name="syntax"></a>Syntax  
  
```  
class XmlDictionaryReaderQuotas  
{  
  sint32 MaxArrayLength;  
  sint32 MaxBytesPerRead;  
  sint32 MaxDepth;  
  sint32 MaxNameTableCharCount;  
  sint32 MaxStringContentLength;  
};  
```  
  
## <a name="methods"></a>Methoden  
 Von der XmlDictionaryReaderQuotas-Klasse werden keine Methoden definiert.  
  
## <a name="properties"></a>Eigenschaften  
 Die XmlDictionaryReaderQuotas-Klasse weist die folgenden Eigenschaften auf:  
  
### <a name="maxarraylength"></a>MaxArrayLength  
 Datentyp: sint32  
  
 Zugriffstyp: Schreibgeschützt  
  
 Die maximal zulässige Arraylänge.  
  
### <a name="maxbytesperread"></a>MaxBytesPerRead  
 Datentyp: sint32  
  
 Zugriffstyp: Schreibgeschützt  
  
 Die maximal zulässigen Bytes, die bei jedem Lesevorgang zurückgegeben werden.  
  
### <a name="maxdepth"></a>MaxDepth  
 Datentyp: sint32  
  
 Zugriffstyp: Schreibgeschützt  
  
 Die maximale geschachtelte Knotentiefe für jeden Lesevorgang.  
  
### <a name="maxnametablecharcount"></a>MaxNameTableCharCount  
 Datentyp: sint32  
  
 Zugriffstyp: Schreibgeschützt  
  
 Die maximal zulässigen Zeichen in einem Tabellennamen.  
  
### <a name="maxstringcontentlength"></a>MaxStringContentLength  
 Datentyp: sint32  
  
 Zugriffstyp: Schreibgeschützt  
  
 Die maximale Zeichenanzahl, die in XML-Elementinhalten zulässig ist.  
  
## <a name="requirements"></a>Anforderungen  
  
|MOF|Deklariert in Servicemodel.mof.|  
|---------|-----------------------------------|  
|Namespace|Definiert in root\ServiceModel|  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Xml.XmlDictionaryReaderQuotas>  
 <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>
