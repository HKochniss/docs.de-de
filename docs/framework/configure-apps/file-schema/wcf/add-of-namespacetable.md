---
title: '&lt;add&gt; von &lt;namespaceTable&gt;'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf7b5b75-63bd-49a6-abac-4bfdab377e36
caps.latest.revision: "2"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 394657abcebb42192fb7a8b57b0402bcacf37693
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="ltaddgt-of-ltnamespacetablegt"></a>&lt;add&gt; von &lt;namespaceTable&gt;
Stellt ein Konfigurationselement dar, das eine Namespace-/Präfix-Zuordnung enthält, die zu Routingzwecken in XPath-Filtern verwendet werden kann.  
  
 \<system.serviceModel >  
\<Routing >  
\<NamespaceTable >  
\<add>  
  
## <a name="syntax"></a>Syntax  
  
```xml  
   <routing>   <namespaceTable>  
     <add namespace="String" prefix="String" />    </namespaceTable></routing>  
```  
  
```csharp  
```  
  
## <a name="attributes-and-elements"></a>Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### <a name="attributes"></a>Attribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|namespace|Eine Zeichenfolge, die den Namespace enthält.|  
|prefix|Eine Zeichenfolge, die das Präfix für diesen Namespace enthält.|  
  
### <a name="child-elements"></a>Untergeordnete Elemente  
 Keine  
  
### <a name="parent-elements"></a>Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|[\<NamespaceTable >](../../../../../docs/framework/configure-apps/file-schema/wcf/namespacetable.md)|Stellt einen Konfigurationsabschnitt zum Definieren eines Satzes von Elementen dar, die Namespace-/Präfix-Zuordnungen enthalten, die zu Routingzwecken in XPath-Filtern verwendet werden können.|  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.ServiceModel.Routing.Configuration.NamespaceElement?displayProperty=nameWithType>    
