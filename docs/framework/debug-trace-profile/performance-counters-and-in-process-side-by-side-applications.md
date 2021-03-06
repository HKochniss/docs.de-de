---
title: Leistungsindikatoren und prozessinterne parallele Anwendungen
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- performance counters
- performance counters,and in-process side-by-side applications
- performance,.NET Framework applications
- performance monitoring,counters
ms.assetid: 6888f9be-c65b-4b03-a07b-df7ebdee2436
caps.latest.revision: "26"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: acbdf1ff1f2827bf607c2f838685d5161af61fd0
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="performance-counters-and-in-process-side-by-side-applications"></a>Leistungsindikatoren und prozessinterne parallele Anwendungen
Mithilfe des Systemmonitors (Perfmon.exe) können die Leistungsindikatoren pro Laufzeit unterschieden werden. Dieses Thema beschreibt die erforderlichen Registrierungsänderungen zur Aktivierung dieser Funktion.  
  
## <a name="the-default-behavior"></a>Das Standardverhalten  
 Standardmäßig zeigt der Systemmonitor Leistungsindikatoren für eine einzelne Anwendung an. Es gibt jedoch zwei Szenarios, in denen dies problematisch ist:  
  
-   Wenn Sie zwei Anwendungen überwachen, die den gleichen Namen haben. Wenn beispielsweise beide Anwendungen myapp.exe heißen, wird eine als **MyApp** und die andere als **MyApp#1** in der **Instanz**-Spalte angezeigt. In diesem Fall ist es schwierig, einen Leistungsindikator einer bestimmten Anwendung zuzuordnen. Es ist nicht klar, ob sich die Datensammlung für **MyApp#1** auf die erste oder zweite myapp.exe bezieht.  
  
-   Wenn eine Anwendung mehrere Instanzen der Common Language Runtime verwendet. Die [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] unterstützt prozessinterne parallele Hostingszenarios; d.h. ein einzelner Prozess oder eine Anwendung kann mehrere Instanzen der Common Language Runtime laden. Wenn eine einzelne Anwendung namens myapp.exe standardmäßig zwei Laufzeitinstanzen lädt, werden sie in der **Instanz**-Spalte als **MyApp** und **MyApp#1** festgelegt werden. In diesem Fall ist es nicht klar, ob **MyApp** und **MyApp#1** auf zwei Anwendungen mit dem gleichen Namen oder auf dieselbe Anwendung mit zwei Laufzeiten verweisen. Wenn mehrere Anwendungen mit dem gleichen Namen mehrere Laufzeiten laden, wird die Mehrdeutigkeit noch größer.  
  
 Sie können einen Registrierungsschlüssel festlegen, um diese Mehrdeutigkeit zu vermeiden. Für Anwendungen, die mit [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] entwickelt werden, fügt diese Registrierungsänderung einen Prozessbezeichner, gefolgt von einem Instanzbezeichner der Laufzeit, zum Anwendungsnamen in der **Instanz**-Spalte hinzu. Anstelle von *Anwendung* oder *Anwendung*#1 kann die Anwendung jetzt als *Anwendung*_`p`*ProcessID*\_`r`*RuntimeID* in der **Instanz**-Spalte identifiziert werden. Wenn eine Anwendung mit einer früheren Version der Common Language Runtime entwickelt wurde, wird diese Instanz als *Anwendung\_*`p`*ProcessID* dargestellt, vorausgesetzt, dass die [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] installiert ist.  
  
## <a name="performance-counters-for-in-process-side-by-side-applications"></a>Leistungsindikatoren für prozessinterne parallele Anwendungen  
 Um die Leistungsindikatoren für mehrere Versionen der Common Language Runtime zu behandeln, die in einer einzigen Anwendung gehostet werden, müssen Sie die Einstellungen eines einzelnen Registrierungsschlüssels ändern, wie in der folgenden Tabelle gezeigt.  
  
|||  
|-|-|  
|Schlüsselname|HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\\.NETFramework\Performance|  
|Wertname|ProcessNameFormat|  
|Werttyp|REG_DWORD|  
|Wert|1 (0x00000001)|  
  
 Der Wert 0 für `ProcessNameFormat` zeigt an, dass das Standardverhalten aktiviert ist; Perfmon.exe zeigt Leistungsindikatoren nach einzelnen Anwendungen an. Wenn Sie diesen Wert auf 1 festlegen, unterscheidet Perfmon.exe zwischen mehreren Versionen einer Anwendung und stellt Leistungsindikatoren pro Laufzeit zur Verfügung. Jeder andere Wert für die `ProcessNameFormat`-Registrierungsschlüsseleinstellung wird nicht unterstützt und für zukünftige Verwendung reserviert.  
  
 Nach der Aktualisierung der `ProcessNameFormat`-Registrierungsschlüsseleinstellung müssen Sie Perfmon.exe oder andere Consumer von Leistungsindikatoren neu starten, damit die neue namensgebende Funktion der Instanz ordnungsgemäß funktioniert.  
  
 Im folgenden Beispiel wird veranschaulicht, wie ein `ProcessNameFormat`-Wert programmgesteuert verändert werden kann.  
  
 [!code-csharp[Conceptual.PerfCounters.InProSxS#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.perfcounters.inprosxs/cs/regsetting1.cs#1)]
 [!code-vb[Conceptual.PerfCounters.InProSxS#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.perfcounters.inprosxs/vb/regsetting1.vb#1)]  
  
 Wenn Sie diese Registrierungsänderung vornehmen, zeigt Perfmon.exe die Namen der Anwendungen an, die auf die [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] als *Anwendung*_`p`*ProcessID*\_`r`*RuntimeID* abzielen, wobei *Anwendung* der Name der Anwendung, *ProcessID* der Prozess-ID für die Anwendung, und  *RuntimeID* ein Common Language Runtime-Bezeichner ist. Wenn beispielsweise eine Anwendung namens myapp.exe zwei Instanzen der Common Language Runtime lädt, wird Perfmon.exe möglicherweise eine Instanz als myapp_p1416_r10 und eine zweite als myapp_p3160_r10 identifizieren. Der Laufzeitbezeichner unterscheidet nur zwischen den Laufzeiten innerhalb eines Prozesses; er stellt keine andere Informationen über die Common Language Runtime bereit. (Die Common Language Runtime-ID hat beispielsweise keine Beziehung mit der Version oder der SKU der Laufzeit.)  
  
 Wenn die [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] installiert ist, wirkt sich die Registrierungsänderung auch auf Anwendungen aus, die mit früheren Versionen von .NET Framework entwickelt wurden. Diese werden in Perfmon.exe als *Application_*`p`*ProcessID* angezeigt, wobei *Anwendung* der Anwendungsname und *ProcessID* die Prozess-ID ist. Wenn die Leistungsindikatoren von zwei Anwendungen namens myapp.exe überwacht werden, wird eine möglicherweise als myapp_p23900 und die andere als myapp_p24908 angezeigt werden.  
  
> [!NOTE]
>  Die Prozess-ID beseitigt die Mehrdeutigkeit der Auflösung von zwei Anwendungen mit dem gleichen Namen, die frühere Versionen der Laufzeit verwenden. Ein Laufzeitbezeichner ist nicht für frühere Versionen erforderlich, da frühere Versionen der Common Language Runtime keine parallelen Szenarios unterstützen.  
  
 Wenn die [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] nicht vorhanden ist oder deinstalliert wurde, hat die Einstellung des Registrierungsschlüssels keine Auswirkungen. Dies bedeutet, dass zwei Anwendungen mit dem gleichen Namen in Perfmon.exe weiterhin als *Anwendung* und *Anwendung#1* angezeigt werden (z.B. **MyApp** und **MyApp#1**).
