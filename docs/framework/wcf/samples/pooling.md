---
title: Pooling
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 688dfb30-b79a-4cad-a687-8302f8a9ad6a
caps.latest.revision: "29"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 0bdd1874004af1ebbde69c622853d5fdcd982005
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="pooling"></a>Pooling
In diesem Beispiel wird veranschaulicht, wie [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] erweitert wird, um Objektpooling zu unterstützen. Das Beispiel veranschaulicht die Erstellung eines Attributs, das syntaktisch und semantisch ähnlich zur `ObjectPoolingAttribute`-Attributfunktionalität von Enterprise Services ist. Durch Objektpooling lässt sich die Leistung einer Anwendung u.&#160;U. drastisch steigern. Es kann jedoch auch einen gegenteiligen Effekt haben, wenn es nicht ordnungsgemäß verwendet wird. Objektpooling hilft dabei, den Mehraufwand zu reduzieren, der durch die Neuerstellung häufig verwendeter Objekte, die eine umfangreiche Initialisierung erfordern, entsteht. Wenn das Aufrufen einer Methode in einem gepoolten Objekt jedoch sehr lange dauert, werden durch das Objektpooling zusätzliche Anforderungen in einer Warteschlange platziert, sobald die maximale Poolgröße erreicht ist. Daher werden u.&#160;U. einige Anforderungen zur Objekterstellung nicht erfüllt, indem eine Timeoutausnahme ausgelöst wird.  
  
> [!NOTE]
>  Die Setupprozedur und die Buildanweisungen für dieses Beispiel befinden sich am Ende dieses Themas.  
  
 Der erste Schritt beim Erstellen einer [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Erweiterung besteht darin, den zu verwendenden Erweiterungspunkt auszuwählen.  
  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] der Begriff *Dispatcher* bezieht sich auf eine Laufzeitkomponente verantwortlich, konvertieren eingehende Nachrichten in Methodenaufrufe für den Dienst des Benutzers konvertiert und Rückgabewerte von dieser Methode zu einer ausgehenden Nachricht. Ein [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Dienst erstellt für jeden Endpunkt einen Verteiler. Ein [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Client muss einen Verteiler verwenden, wenn es sich bei dem diesem Client zugeordneten Vertrag um einen Duplexvertrag handelt.  
  
 Der Kanal- und der Endpunktverteiler bieten eine kanal- und vertragsweite Erweiterbarkeit, indem sie verschiedene Eigenschaften, die das Verhalten des Verteilers steuern, verfügbar machen. Die <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.DispatchRuntime%2A>-Eigenschaft ermöglicht es Ihnen außerdem, den Verteilungsprozess zu überprüfen, zu ändern oder anzupassen. In diesem Beispiel wird in erster Linie die <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A>-Eigenschaft behandelt, die auf das Objekt zeigt, das die Instanzen der Dienstklasse bereitstellt.  
  
## <a name="the-iinstanceprovider"></a>Der IInstanceProvider  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] erstellt der Verteiler mithilfe von <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A>, der die <xref:System.ServiceModel.Dispatcher.IInstanceProvider>-Schnittstelle implementiert, Instanzen der Dienstklasse. Diese Schnittstelle verfügt über drei Methoden:  
  
-   <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%28System.ServiceModel.InstanceContext%2CSystem.ServiceModel.Channels.Message%29>: Wenn eine Nachricht eingeht, ruft der Verteiler die <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%28System.ServiceModel.InstanceContext%2CSystem.ServiceModel.Channels.Message%29>-Methode auf, um eine Instanz der Dienstklasse zum Verarbeiten der Nachricht zu erstellen. Die Häufigkeit der Aufrufe dieser Methode wird von der <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>-Eigenschaft bestimmt. Wenn die <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>-Eigenschaft beispielsweise auf <xref:System.ServiceModel.InstanceContextMode.PerCall> festgelegt ist, wird eine neue Instanz der Dienstklasse erstellt, um alle eingehenden Nachrichten zu verarbeiten. Daher wird <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%28System.ServiceModel.InstanceContext%2CSystem.ServiceModel.Channels.Message%29> immer dann aufgerufen, wenn eine Nachricht eingeht.  
  
-   <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%28System.ServiceModel.InstanceContext%29>: Diese Methode ist identisch zur vorherigen Methode, nur mit dem Unterschied, dass sie aufgerufen wird, wenn kein Argument für die Nachricht vorhanden ist.  
  
-   <xref:System.ServiceModel.Dispatcher.IInstanceProvider.ReleaseInstance%28System.ServiceModel.InstanceContext%2CSystem.Object%29>: Wenn die Lebensdauer einer Dienstinstanz verstrichen ist, ruft der Verteiler die <xref:System.ServiceModel.Dispatcher.IInstanceProvider.ReleaseInstance%28System.ServiceModel.InstanceContext%2CSystem.Object%29>-Methode auf. Wie bei der <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%28System.ServiceModel.InstanceContext%2CSystem.ServiceModel.Channels.Message%29>-Methode wird die Häufigkeit der Aufrufe dieser Methode von der <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>-Eigenschaft bestimmt.  
  
## <a name="the-object-pool"></a>Der Objektpool  
 Eine benutzerdefinierte <xref:System.ServiceModel.Dispatcher.IInstanceProvider>-Implementierung stellt die erforderliche Objektpoolingsemantik für einen Dienst bereit. Deshalb verfügt dieses Beispiel über einen `ObjectPoolingInstanceProvider`-Typ, der eine benutzerdefinierte Implementierung von <xref:System.ServiceModel.Dispatcher.IInstanceProvider> für das Pooling bereitstellt. Wenn der `Dispatcher` die <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%28System.ServiceModel.InstanceContext%2CSystem.ServiceModel.Channels.Message%29>-Methode aufruft, erstellt die benutzerdefinierte Implementierung keine neue Instanz, sondern sucht ein vorhandenes Objekt in einem Speicherpool. Wenn eines verfügbar ist, wird es zurückgegeben. Andernfalls wird ein neues Objekt erstellt. Die Implementierung für `GetInstance` wird im folgenden Beispielcode dargestellt.  
  
```  
object IInstanceProvider.GetInstance(InstanceContext instanceContext, Message message)  
{  
    object obj = null;  
  
    lock (poolLock)  
    {  
        if (pool.Count > 0)  
        {  
            obj = pool.Pop();  
        }  
        else  
        {  
            obj = CreateNewPoolObject();  
        }  
        activeObjectsCount++;  
    }  
  
    WritePoolMessage(ResourceHelper.GetString("MsgNewObject"));  
  
    idleTimer.Stop();  
  
    return obj;            
}  
```  
  
 Die benutzerdefinierte `ReleaseInstance`-Implementierung fügt die freigegebene Instanz dem Pool erneut hinzu und dekrementiert den `ActiveObjectsCount`-Wert. Der `Dispatcher` kann diese Methoden von unterschiedlichen Threads aus aufrufen. Daher ist ein synchronisierter Zugriff auf die Member der Klassenebene in der `ObjectPoolingInstanceProvider`-Klasse erforderlich.  
  
```  
void IInstanceProvider.ReleaseInstance(InstanceContext instanceContext, object instance)  
{  
    lock (poolLock)  
    {  
        pool.Push(instance);  
        activeObjectsCount--;  
  
        WritePoolMessage(  
        ResourceHelper.GetString("MsgObjectPooled"));  
  
        // When the service goes completely idle (no requests   
        // are being processed), the idle timer is started  
        if (activeObjectsCount == 0)  
            idleTimer.Start();                       
    }  
}  
```  
  
 Die `ReleaseInstance` Methode stellt eine Funktion "bereinigungsinitialisierung" bereit. Normalerweise wird im Pool eine Mindestanzahl von Objekten für die Lebensdauer des Pools beibehalten. Es kann jedoch Zeiten mit übermäßiger Auslastung geben, für die im Pool zusätzliche Objekte erstellt werden müssen, um die in der Konfiguration festgelegte Höchstgrenze zu erreichen. Wenn der Pool weniger aktiv ist, stellen diese überzähligen Objekte einen zusätzlichen Aufwand dar. Wenn `activeObjectsCount` daher 0 (null) erreicht, wird ein Leerlaufzeitgeber gestartet, der einen Bereinigungszyklus auslöst und ausführt.  
  
## <a name="adding-the-behavior"></a>Hinzufügen des Verhaltens  
 Verteilerschicht-Erweiterungen werden mithilfe der folgenden Verhaltensweisen verknüpft:  
  
-   Dienstverhaltensweisen. Diese ermöglichen die Anpassung der gesamten Dienstlaufzeit.  
  
-   Endpunktverhaltensweisen. Diese ermöglichen die Anpassung von Dienstendpunkten, insbesondere eines Kanal- und Endpunktverteilers.  
  
-   Vertragsverhaltensweisen. Diese ermöglichen die Anpassung sowohl der <xref:System.ServiceModel.Dispatcher.ClientRuntime>-Klasse als auch der <xref:System.ServiceModel.Dispatcher.DispatchRuntime>-Klasse im Client bzw. Dienst.  
  
 Für den Zweck einer Objektpoolingerweiterung muss ein Dienstverhalten erstellt werden. Dienstverhaltensweisen werden durch Implementieren der <xref:System.ServiceModel.Description.IServiceBehavior>-Schnittstelle erstellt. Es gibt mehrere Möglichkeiten, das Dienstmodell auf die benutzerdefinierten Verhaltensweisen hinzuweisen:  
  
-   Verwenden eines benutzerdefinierten Attributs.  
  
-   Imperatives Hinzufügen zur Verhaltensauflistung der Dienstbeschreibung.  
  
-   Erweitern der Konfigurationsdatei.  
  
 In diesem Beispiel wird ein benutzerdefiniertes Attribut verwendet. Beim Erstellen von <xref:System.ServiceModel.ServiceHost> werden die in der Typdefinition des Diensts verwendeten Attribute untersucht, und die verfügbaren Verhaltensweisen werden der Verhaltensauflistung der Dienstbeschreibung hinzugefügt.  
  
 Die Schnittstelle <xref:System.ServiceModel.Description.IServiceBehavior> verfügt über drei Methoden &#150; <xref:System.ServiceModel.Description.IServiceBehavior.Validate%2A>, <xref:System.ServiceModel.Description.IServiceBehavior.AddBindingParameters%2A> und <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A>. Die <xref:System.ServiceModel.Description.IServiceBehavior.Validate%2A>-Methode wird verwendet, um sicherzustellen, dass das Verhalten für den Dienst übernommen werden kann. In diesem Beispiel stellt die Implementierung sicher, dass der Dienst nicht mit <xref:System.ServiceModel.InstanceContextMode.Single> konfiguriert wird. Die <xref:System.ServiceModel.Description.IServiceBehavior.AddBindingParameters%2A>-Methode dient dazu, die Bindungen des Diensts zu konfigurieren. Sie ist für dieses Szenario nicht erforderlich. <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A> wird dazu verwendet, die Verteiler des Diensts zu konfigurieren. Diese Methode wird von [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] aufgerufen, wenn <xref:System.ServiceModel.ServiceHost> initialisiert wird. Die folgenden Parameter werden an diese Methode übergeben:  
  
-   `Description`: Dieses Argument stellt die Dienstbeschreibung für den gesamten Dienst bereit. Dies kann dazu verwendet werden, Beschreibungsdaten über die Endpunkte, Verträge und Bindungen des Diensts und andere Daten zu überprüfen.  
  
-   `ServiceHostBase`: Dieses Argument stellt die <xref:System.ServiceModel.ServiceHostBase> bereit, die gerade initialisiert wird.  
  
 In der benutzerdefinierten <xref:System.ServiceModel.Description.IServiceBehavior>-Implementierung wird eine neue Instanz von `ObjectPoolingInstanceProvider` instanziiert und der <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A>-Eigenschaft in jeder <xref:System.ServiceModel.Dispatcher.DispatchRuntime> in der ServiceHostBase zugewiesen.  
  
```  
void IServiceBehavior.ApplyDispatchBehavior(ServiceDescription description, ServiceHostBase serviceHostBase)  
{  
    // Create an instance of the ObjectPoolInstanceProvider.  
    ObjectPoolingInstanceProvider instanceProvider = new  
           ObjectPoolingInstanceProvider(description.ServiceType,   
                                                    minPoolSize);  
  
    // Forward the call if we created a ServiceThrottlingBehavior.  
    if (this.throttlingBehavior != null)  
    {  
        ((IServiceBehavior)this.throttlingBehavior).ApplyDispatchBehavior(description, serviceHostBase);  
    }  
  
    // In case there was already a ServiceThrottlingBehavior   
    // (this.throttlingBehavior==null), it should have initialized   
    // a single ServiceThrottle on all ChannelDispatchers.    
    // As we loop through the ChannelDispatchers, we verify that   
    // and modify the ServiceThrottle to guard MaxPoolSize.  
    ServiceThrottle throttle = null;  
  
    foreach (ChannelDispatcherBase cdb in   
            serviceHostBase.ChannelDispatchers)  
    {  
        ChannelDispatcher cd = cdb as ChannelDispatcher;  
        if (cd != null)  
        {  
            // Make sure there is exactly one throttle used by all   
            // endpoints. If there were others, we could not enforce   
            // MaxPoolSize.  
            if ((this.throttlingBehavior == null) &&   
                        (this.maxPoolSize != Int32.MaxValue))  
            {  
                if (throttle == null)  
                {  
                    throttle = cd.ServiceThrottle;  
                }  
                if (cd.ServiceThrottle == null)  
                {  
                    throw new   
InvalidOperationException(ResourceHelper.GetString("ExNullThrottle"));  
                }  
                if (throttle != cd.ServiceThrottle)  
                {  
                    throw new InvalidOperationException(ResourceHelper.GetString("ExDifferentThrottle"));  
                }  
             }  
  
             foreach (EndpointDispatcher ed in cd.Endpoints)  
             {  
                 // Assign it to DispatchBehavior in each endpoint.  
                 ed.DispatchRuntime.InstanceProvider =   
                                      instanceProvider;  
             }  
         }  
     }  
  
     // Set the MaxConcurrentInstances to limit the number of items   
     // that will ever be requested from the pool.  
     if ((throttle != null) && (throttle.MaxConcurrentInstances >   
                                      this.maxPoolSize))  
     {  
         throttle.MaxConcurrentInstances = this.maxPoolSize;  
     }  
}  
```  
  
 Neben einer <xref:System.ServiceModel.Description.IServiceBehavior>-Implementierung verfügt die <xref:System.EnterpriseServices.ObjectPoolingAttribute>-Klasse über mehrere Member zum Anpassen des Objektpools mithilfe der Attributargumente. Diese Members umfassen <xref:System.EnterpriseServices.ObjectPoolingAttribute.MaxPoolSize%2A>, <xref:System.EnterpriseServices.ObjectPoolingAttribute.MinPoolSize%2A> und <xref:System.EnterpriseServices.ObjectPoolingAttribute.CreationTimeout%2A> für die Übereinstimmung mit dem von .NET Enterprise Services bereitgestellten Objektpooling-Featuresatz.  
  
 Das Objektpoolingverhalten kann nun einem [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]-Dienst hinzugefügt werden, indem der Dienstimplementierung mit dem neu erstellten, benutzerdefinierten `ObjectPooling`-Attribut eine Anmerkung hinzugefügt wird.  
  
```  
[ObjectPooling(MaxPoolSize=1024, MinPoolSize=10, CreationTimeout=30000)]      
public class PoolService : IPoolService  
{  
  // …  
}  
```  
  
## <a name="running-the-sample"></a>Ausführen des Beispiels  
 Das Beispiel veranschaulicht die Leistungsvorteile, die durch die Verwendung von Objektpooling in bestimmten Szenarios erzielt werden können.  
  
 Die Dienstanwendung implementiert zwei Dienste, `WorkService` und `ObjectPooledWorkService`. Beide Dienste teilen dieselbe Implementierung. Sie erfordern beide eine kostenintensive Initialisierung und machen dann eine `DoWork()`-Methode verfügbar, die relativ billig ist. Der einzige Unterschied ist, dass für `ObjectPooledWorkService` ein Objektpooling konfiguriert ist:  
  
```  
[ObjectPooling(MinPoolSize = 0, MaxPoolSize = 5)]  
public class ObjectPooledWorkService : IDoWork  
{  
    public ObjectPooledWorkService()  
    {  
        Thread.Sleep(5000);  
        ColorConsole.WriteLine(ConsoleColor.Blue, "ObjectPooledWorkService instance created.");  
    }  
  
    public void DoWork()  
    {  
        ColorConsole.WriteLine(ConsoleColor.Blue, "ObjectPooledWorkService.GetData() completed.");  
    }          
}  
```  
  
 Wenn Sie den Client ausführen, stoppt er die Zeit, die benötigt wird, um `WorkService` 5-mal aufzurufen. Er stoppt dann die Zeit, die benötigt wird, um `ObjectPooledWorkService` 5-mal aufzurufen. Dann wird der Zeitunterschied angezeigt:  
  
```  
Press <ENTER> to start the client.  
  
Calling WorkService:  
1 - DoWork() Done  
2 - DoWork() Done  
3 - DoWork() Done  
4 - DoWork() Done  
5 - DoWork() Done  
Calling WorkService took: 26722 ms.  
Calling ObjectPooledWorkService:  
1 - DoWork() Done  
2 - DoWork() Done  
3 - DoWork() Done  
4 - DoWork() Done  
5 - DoWork() Done  
Calling ObjectPooledWorkService took: 5323 ms.  
Press <ENTER> to exit.  
```  
  
> [!NOTE]
>  Wenn der Client zum ersten Mal ausgeführt wird, scheinen beide Dienste etwa gleich viel Zeit zu benötigen. Wenn Sie das Beispiel erneut ausführen, können Sie sehen, dass `ObjectPooledWorkService` wesentlich schneller zurückkehrt, da im Pool bereits eine Instanz dieses Objekts vorhanden ist.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>So können Sie das Beispiel einrichten, erstellen und ausführen  
  
1.  Stellen Sie sicher, dass Sie ausgeführt haben die [Setupprozedur für die Windows Communication Foundation-Beispiele zum einmaligen](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Führen Sie zum Erstellen der Projektmappe die Anweisungen im [Erstellen der Windows Communication Foundation-Beispiele](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Um das Beispiel in einer einzelnen oder computerübergreifenden Konfiguration ausführen möchten, folgen Sie den Anweisungen [Ausführen der Windows Communication Foundation-Beispiele](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!NOTE]
>  Wenn Sie zur Neugenerierung der Konfiguration für dieses Beispiel die Datei Svcutil.exe verwenden, müssen Sie den Endpunktnamen in der Clientkonfiguration so ändern, dass er mit dem Clientcode übereinstimmt.  
  
> [!IMPORTANT]
>  Die Beispiele sind möglicherweise bereits auf dem Computer installiert. Suchen Sie nach dem folgenden Verzeichnis (Standardverzeichnis), bevor Sie fortfahren.  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Wenn dieses Verzeichnis nicht vorhanden ist, rufen Sie [Windows Communication Foundation (WCF) and Windows Workflow Foundation (WF) Samples for .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) auf, um alle [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] - und [!INCLUDE[wf1](../../../../includes/wf1-md.md)] -Beispiele herunterzuladen. Dieses Beispiel befindet sich im folgenden Verzeichnis.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Instancing\Pooling`  
  
## <a name="see-also"></a>Siehe auch
