---
title: "Transaktionsaktivitäten in WF"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fb33378e-82c6-4ea0-870f-76dc77e7f0fe
caps.latest.revision: "10"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 0b12cfa1cecde648e66872784eb1e353f8c16da8
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="transaction-activities-in-wf"></a>Transaktionsaktivitäten in WF
[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] verfügt über mehrere vom System bereitgestellte Aktivitäten, um Transaktionen, Kompensationen und Abbrüche zu modellieren. Diese Programmiermodelle ermöglichen es dem Workflow, sich weiter vorwärts zu bewegen, falls Änderungen in der Geschäftslogik auftreten oder eine Fehlerbehandlung ausgeführt wird. [!INCLUDE[crabout](../../../includes/crabout-md.md)]Transaktionen, kompensationen und Abbrüche, finden Sie unter [Transaktionen](../../../docs/framework/windows-workflow-foundation/workflow-transactions.md), [Kompensierung](../../../docs/framework/windows-workflow-foundation/compensation.md), und [Abbruch](../../../docs/framework/windows-workflow-foundation/modeling-cancellation-behavior-in-workflows.md).  
  
## <a name="transaction-activities"></a>Transaktionsaktivitäten  
  
|||  
|-|-|  
|<xref:System.Activities.Statements.CancellationScope>|Ordnet Abbruchlogik in Form einer Aktivität einem Hauptausführungspfad zu. Wird auch als Aktivität ausgedrückt.|  
|<xref:System.Activities.Statements.CompensableActivity>|Unterstützt die Kompensation der untergeordneten Aktivitäten.|  
|<xref:System.Activities.Statements.Compensate>|Ruft den Kompensationshandler einer <xref:System.Activities.Statements.CompensableActivity> explizit auf|  
|<xref:System.Activities.Statements.Confirm>|Ruft den Bestätigungshandler einer <xref:System.Activities.Statements.CompensableActivity> explizit auf|  
|<xref:System.Activities.Statements.TransactionScope>|Demarkiert eine Transaktionsgrenze.|  
|<xref:System.ServiceModel.Activities.TransactedReceiveScope>|Legt Bereiche für die Lebensdauer einer Transaktion fest, die von einer empfangenen Meldung initiiert wird. Die Transaktion kann in den Workflow der initiierenden Meldung übergeben oder vom Verteiler erstellt werden, wenn die Meldung empfangen wird. **Hinweis:** der <xref:System.ServiceModel.Activities.TransactedReceiveScope> befindet sich der **Messaging** Teil der **Toolbox**.|
