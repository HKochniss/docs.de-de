---
title: Angehaltene Instanzverwaltung
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f5ca3faa-ba1f-4857-b92c-d927e4b29598
caps.latest.revision: "6"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 6e04f1e2f334993975b2c4261efdc28ba318dfa3
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="suspended-instance-management"></a>Angehaltene Instanzverwaltung
In diesem Beispiel wird veranschaulicht, wie Workflowinstanzen, die angehalten wurden, verwaltet werden.  Die Standardaktion für <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> ist `AbandonAndSuspend`. Dies bedeutet, dass nicht behandelte Ausnahmen, die von einer Workflowinstanz ausgelöst werden, die im <xref:System.ServiceModel.WorkflowServiceHost> gehostet wird, standardmäßig dazu führen, dass die Instanz aus dem Speicher verworfen (abgebrochen) und dass die dauerhafte/persistente Version der Instanz als angehalten markiert wird. Eine angehaltene Workflowinstanz kann erst ausgeführt werden, nachdem sie fortgesetzt wurde.  
  
 Das Beispiel zeigt, wie ein Befehlszeilenprogramm implementiert werden kann, um angehaltene Instanzen abzufragen, und wie dem Benutzer die Option gegeben wird, um die Instanz fortzusetzen oder zu beenden. In diesem Beispiel löst ein Workflowdienst absichtlich eine Ausnahme aus, wodurch verursacht wird, dass er angehalten wird. Das Befehlszeilenprogramm kann dann verwendet werden, um die Instanz abzufragen und anschließend die Instanz fortzusetzen oder zu beenden.  
  
## <a name="demonstrates"></a>Veranschaulicht  
 <xref:System.ServiceModel.WorkflowServiceHost> mit <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> und <xref:System.ServiceModel.Activities.WorkflowControlEndpoint> in [!INCLUDE[wf](../../../../includes/wf-md.md)].  
  
## <a name="discussion"></a>Diskussion  
 Das in diesem Beispiel implementierte Befehlszeilenprogramm ist speziell auf die SQL-Instanzspeicherimplementierung ausgerichtet, die in [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] enthalten ist. Wenn Sie über eine benutzerdefinierte Implementierung des Instanzspeichers verfügen, können Sie dieses Hilfsprogramm anpassen, indem Sie die `WorkflowInstanceCommand`-Implementierungen im Beispiel durch Implementierungen speziell für Ihren Instanzspeicher ersetzen.  
  
 Die bereitgestellte Implementierung führt SQL-Befehle direkt für den SQL-Instanzspeicher aus, um angehaltene Instanzen direkt aufzuführen, und diese basiert auf einem <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>, der dem <xref:System.ServiceModel.WorkflowServiceHost> hinzugefügt wurde, um die Instanzen fortzusetzen oder zu beenden.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>So können Sie das Beispiel einrichten, erstellen und ausführen  
  
1.  Dieses Beispiel erfordert, dass die folgenden Windows-Komponenten aktiviert sind:  
  
    1.  Microsoft Message Queues (MSMQ) Server  
  
    2.  SQL Server Express  
  
2.  Richten Sie die SQL Server-Datenbank ein.  
  
    1.  Aus einer [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] Eingabeaufforderung führen Sie "setup.cmd" im Beispielverzeichnis SuspendedInstanceManagement, geschieht Folgendes:  
  
        1.  Erstellung einer Persistenzdatenbank mit SQL Server Express. Wenn die Persistenzdatenbank bereits vorhanden ist, dann wird diese gelöscht und neu erstellt.  
  
        2.  Einrichten der Datenbank für Persistenz.  
  
        3.  Fügt IIS der InstanceStoreUsers-Rolle, die beim Einrichten der Datenbank für Persistenz definiert wurde, APPPOOL\DefaultAppPool und NT AUTHORITY\Network Service hinzu.  
  
3.  Einrichten der Dienstwarteschlange.  
  
    1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)], mit der rechten Maustaste die **SampleWorkflowApp** Projekt, und klicken Sie auf **als Startprojekt festlegen**.  
  
    2.  Kompilieren und führen Sie die SampleWorkflowApp durch Drücken von **F5**. Dadurch wird die erforderliche Warteschlange erstellt.  
  
    3.  Drücken Sie **EINGABETASTE** um die SampleWorkflowApp zu beenden.  
  
    4.  Öffnen Sie die Computerverwaltungskonsole, indem Sie "Compmgmt.msc" an einer Eingabeaufforderung ausführen.  
  
    5.  Erweitern Sie **Dienste und Anwendungen**, **Message Queuing-**, **Private Warteschlangen**.  
  
    6.  Klicken Sie mit der rechten Maustaste auf die **ReceiveTx** Warteschlange eingefügt, und wählen Sie **Eigenschaften**.  
  
    7.  Wählen Sie die **Sicherheit** Registerkarte und ermöglichen **"Jeder"** Berechtigungen zum **Nachricht empfangen**, **Peek Message**, und  **Nachricht senden**.  
  
4.  Führen Sie nun das Beispiel aus.  
  
    1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)], führen Sie das Projekt "sampleworkflowapp" erneut ohne debugging drücken Sie **STRG + F5**. Zwei Endpunktadressen werden im Konsolenfenster ausgegeben: eine für den Anwendungsendpunkt und die andere vom <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>. Daraufhin wird eine Workflowinstanz erstellt, und Überwachungsdatensätze für diese Instanz werden im Konsolenfenster angezeigt. Die Workflowinstanz löst eine Ausnahme aus, die bewirkt, dass die Instanz angehalten und abgebrochen wird.  
  
    2.  Das Befehlszeilenprogramm kann dann verwendet werden, um weitere Aktionen für diese Instanzen auszuführen. Die Syntax für Befehlszeilenargumente ist wie folgt:  
  
         `SuspendedInstanceManagement -Command:[CommandName] -Server:[ServerName] -Database:[DatabaseName] -InstanceId:[InstanceId]`  
  
         Die unterstützten Befehle sind: `Query`, `Resume` und `Terminate`.  Der InstanceId-Schalter ist nur für `Resume`- und `Terminate`-Vorgänge erforderlich.  
  
#### <a name="to-cleanup-optional"></a>So führen Sie eine (optionale) Bereinigung durch  
  
1.  Öffnen Sie die Computerverwaltungskonsole, indem Sie "Compmgmt.msc" an einer `vs2010`-Eingabeaufforderung ausführen.  
  
2.  Erweitern Sie **Dienste und Anwendungen**, **Message Queuing-**, **Private Warteschlangen**.  
  
3.  Löschen der **ReceiveTx** Warteschlange.  
  
4.  Um die Persistenzdatenbank zu entfernen, führen Sie "cleanup.cmd" aus.  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert. Suchen Sie nach dem folgenden Verzeichnis (Standardverzeichnis), bevor Sie fortfahren.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, rufen Sie [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) auf, um alle [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] - und [!INCLUDE[wf1](../../../../includes/wf1-md.md)] -Beispiele herunterzuladen. Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Application\SuspendedInstanceManagement`
