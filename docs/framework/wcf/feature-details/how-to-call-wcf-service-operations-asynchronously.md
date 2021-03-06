---
title: "Vorgehensweise: Asynchrones Aufrufen von WCF-Dienstvorgängen"
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
ms.assetid: 0face17f-43ca-417b-9b33-737c0fc360df
caps.latest.revision: "18"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 9f8a22a5a5b9f388cdfb7b5e5edfa0a54b628aa0
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-call-wcf-service-operations-asynchronously"></a>Vorgehensweise: Asynchrones Aufrufen von WCF-Dienstvorgängen
In diesem Thema wird beschrieben, wie ein Client auf einen Dienstvorgang asynchron zugreifen kann. Der in diesem Thema behandelte Dienst implementiert die `ICalculator`-Schnittstelle. Der Client kann mithilfe des ereignisgesteuerten asynchronen Aufrufmodells die Vorgänge asynchron an dieser Schnittstelle aufrufen. (Weitere Informationen über die das ereignisbasierte asynchrone Aufrufmodell finden Sie unter [Multithreadprogrammierung mit dem ereignisbasierten asynchronen Muster](http://go.microsoft.com/fwlink/?LinkId=248184)). Ein Beispiel, das veranschaulicht, wie einen Vorgang asynchron in einem Dienst zu implementieren, finden Sie unter [Vorgehensweise: Implementieren eines asynchronen Dienstvorgangs](../../../../docs/framework/wcf/how-to-implement-an-asynchronous-service-operation.md). Weitere Informationen zu synchronen und asynchronen Vorgängen finden Sie unter [synchrone und asynchrone Vorgänge](../../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md).  
  
> [!NOTE]
>  Bei Verwendung einer <xref:System.ServiceModel.ChannelFactory%601> wird das ereignisgesteuerte asynchrone Aufrufmodell nicht unterstützt. Informationen zum asynchronen Aufrufe mithilfe der <xref:System.ServiceModel.ChannelFactory%601>, finden Sie unter [Vorgehensweise: Aufrufen mithilfe Vorgänge asynchron eine Kanalfactory](../../../../docs/framework/wcf/feature-details/how-to-call-operations-asynchronously-using-a-channel-factory.md).  
  
## <a name="procedure"></a>Prozedur  
  
#### <a name="to-call-wcf-service-operations-asynchronously"></a>So rufen Sie WCF-Dienstvorgänge asynchron auf  
  
1.  Führen Sie die [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) Tool mit der `/async` und die `/tcv:Version35` zusammen Befehlsoptionen wie in den folgenden Befehl gezeigt.  
  
    ```  
    svcutil /n:http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples http://localhost:8000/servicemodelsamples/service/mex /a /tcv:Version35  
    ```  
  
     Damit wird neben den synchronen Vorgängen und den standardmäßigen delegatenbasierten asynchronen Vorgängen eine [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Clientklasse erstellt, die Folgendes enthält:  
  
    -   Zwei <`operationName` > `Async` Vorgänge für die Verwendung mit dem ereignisbasierten asynchronen aufrufenden Ansatz. Zum Beispiel:  
  
         [!code-csharp[EventAsync#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/generatedclient.cs#1)]
         [!code-vb[EventAsync#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/generatedclient.vb#1)]  
  
    -   Vorgang wurde abgeschlossen, Ereignisse im Format <`operationName` > `Completed` für die Verwendung mit dem ereignisbasierten asynchronen aufrufenden Ansatz. Zum Beispiel:  
  
         [!code-csharp[EventAsync#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/generatedclient.cs#2)]
         [!code-vb[EventAsync#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/generatedclient.vb#2)]  
  
    -   <xref:System.EventArgs?displayProperty=nameWithType>Typen, die für jeden Vorgang (im Format <`operationName`>`CompletedEventArgs`) für die Verwendung mit dem ereignisbasierten asynchronen aufrufenden Ansatz. Zum Beispiel:  
  
         [!code-csharp[EventAsync#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/generatedclient.cs#3)]
         [!code-vb[EventAsync#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/generatedclient.vb#3)]  
  
2.  Erstellen Sie in der aufrufenden Anwendung eine Rückrufmethode, die aufgerufen wird, wenn der asynchrone Vorgang abgeschlossen ist, wie im folgenden Beispielcode dargestellt.  
  
     [!code-csharp[EventAsync#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/client.cs#4)]
     [!code-vb[EventAsync#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/client.vb#4)]  
  
3.  Vor dem Aufrufen des Vorgangs, verwenden Sie eine neue generische <xref:System.EventHandler%601?displayProperty=nameWithType> vom Typ <`operationName` > `EventArgs` die Handlermethode (im vorherigen Schritt erstellt) zum Hinzufügen der <`operationName` > `Completed` Ereignis. Rufen Sie anschließend die <`operationName` > `Async` Methode. Zum Beispiel:  
  
     [!code-csharp[EventAsync#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/client.cs#5)]
     [!code-vb[EventAsync#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/client.vb#5)]  
  
## <a name="example"></a>Beispiel  
  
> [!NOTE]
>  Die Entwurfsrichtlinien für das ereignisbasierte asynchrone Modell besagen, dass in den Fällen, in denen mehr als ein Wert zurückgegeben wird, ein Wert in der `Result`-Eigenschaft und die übrigen Werte in Eigenschaften des <xref:System.EventArgs>-Objekts zurückgegeben werden sollen. Wenn ein Client Metadaten mithilfe der ereignisbasierten asynchronen Befehlsoptionen importiert und der Vorgang mehr als einen Wert zurückgibt, dann gibt das <xref:System.EventArgs>-Objekt infolgedessen einen Wert in der `Result`-Eigenschaft zurück, und die übrigen Werte werden in Eigenschaften des <xref:System.EventArgs>-Objekts zurückgegeben. Wenn das Nachrichtenobjekt in der `Result`-Eigenschaft und die Rückgabewerte als Eigenschaften dieses Objekts übermittelt werden sollen, verwenden Sie die Befehlsoption `/messageContract`. Damit wird eine Signatur generiert, bei der die Antwortnachricht in der `Result`-Eigenschaft des <xref:System.EventArgs>-Objekts zurückgegeben wird. Alle internen Rückgabewerte sind dann Eigenschaften des Antwortnachrichtenobjekts.  
  
 [!code-csharp[EventAsync#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/eventasync/cs/client.cs#6)]
 [!code-vb[EventAsync#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/eventasync/vb/client.vb#6)]  
  
## <a name="see-also"></a>Siehe auch  
 [Vorgehensweise: Implementieren eines asynchronen Dienstvorgangs](../../../../docs/framework/wcf/how-to-implement-an-asynchronous-service-operation.md)
