---
title: Aufgabenbasiertes asynchrones Muster (TAP, Task-based Asynchronous Pattern)
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- .NET Framework, and TAP
- asynchronous design patterns, .NET Framework
- TAP, .NET Framework support for
- Task-based Asynchronous Pattern, .NET Framework support for
- .NET Framework, asynchronous design patterns
ms.assetid: 8cef1fcf-6f9f-417c-b21f-3fd8bac75007
caps.latest.revision: 
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 3c3d768414a5cd8a8a9fd4a7e120f74d70827729
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/23/2017
---
# <a name="task-based-asynchronous-pattern-tap"></a>Aufgabenbasiertes asynchrones Muster (TAP, Task-based Asynchronous Pattern)
Das aufgabenbasierte asynchrone Muster (TAP) basiert auf den Typen <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> und <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> im <xref:System.Threading.Tasks?displayProperty=nameWithType>-Namespace, mit denen beliebige asynchrone Vorgänge dargestellt werden. TAP ist das empfohlene Entwurfsmuster für asynchrone Neuentwicklungen.  
  
## <a name="naming-parameters-and-return-types"></a>Benennung, Parameter und Rückgabetypen  
 TAP verwendet eine einfache Methode, um die Initiierung und den Abschluss eines asynchronen Vorgangs darzustellen. Dies steht im Gegensatz zum asynchronen Programmierungsmodell (APM oder `IAsyncResult`)-Muster, welches die Methoden `Begin` und `End` erfordert sowie im Gegensatz zum ereignisbasierten asynchronen Muster (EAP), das eine Methode mit `Async`-Suffix erfordert, sowie ein oder mehrere Ereignisse, Ereignishandler-Delegattypen und `EventArg`-abgeleitete Typen. Asynchrone Methoden im TAP umfassen das Suffix `Async` nach dem Vorgangsnamen, z.B. `GetAsync` für einen `Get`-Vorgang. Wenn Sie eine TAP-Methode zu einer Klasse hinzufügen, die bereits diese Methode mit dem `Async`-Suffix enthält, verwenden Sie stattdessen das Suffix `TaskAsync`. Wenn beispielsweise die Klasse bereits über eine `GetAsync`-Methode verfügt, verwenden Sie den Namen `GetTaskAsync`.  
  
 Die TAP-Methode gibt entweder <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> oder <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> zurück. Das hängt davon ab, ob die entsprechende synchrone Methode „void“ oder einen `TResult`-Typ zurückgibt.  
  
 Die Parameter einer TAP-Methode sollten mit den Parametern der synchronen Entsprechung übereinstimmen und in der gleichen Reihenfolge bereitgestellt werden.  Diese Regel gilt jedoch nicht für den `out`-Parameter und den `ref`-Parameter. Diese Parameter sollten vollständig vermieden werden. Alle Daten, die über einen `out`-Parameter oder einen `ref`-Parameter zurückgegeben werden, sollten stattdessen als Teil des von `TResult` zurückgegebenen <xref:System.Threading.Tasks.Task%601> zurückgegeben werden, wobei für die Verwendung mehrerer Werte ein Tupel oder eine benutzerdefinierte Datenstruktur genutzt wird. 
 
 Methoden, die ausschließlich zur Erstellung, Bearbeitung oder Kombination von Tasks dienen (wobei die asynchrone Verwendung der Methode im Methodennamen oder im Namen des Typs, zu dem die Methode gehört, angegeben wird), müssen nicht nach diesem Benennungsmuster benannt werden. Diese Methoden werden häufig als *Combinators* bezeichnet. Beispiele für Combinators umfassen <xref:System.Threading.Tasks.Task.WhenAll%2A> und <xref:System.Threading.Tasks.Task.WhenAny%2A> und werden im Abschnitt [Verwenden der integrierten taskbasierten Combinators](../../../docs/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md#combinators) des Artikels [Verwenden des taskbasierten asynchronen Musters](../../../docs/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md) erläutert.  
  
 Beispiele dafür, wie die TAP-Syntax sich von der Syntax in Legacyversionen des asynchronen Programmiermusters (beispielsweise dem asynchronen Programmiermodell (kurz APM) und dem ereignisbasierten asynchronen Muster (EAP)) unterscheidet, finden Sie unter [Muster für die asynchrone Programmierung](../../../docs/standard/asynchronous-programming-patterns/index.md).  
  
## <a name="initiating-an-asynchronous-operation"></a>Initiieren eines asynchronen Vorgangs  
 Eine asynchrone Methode, die auf TAP basiert, kann eine kleine Menge an Arbeit synchron ausführen, beispielsweise das Überprüfen von Argumenten und das Initiieren des asynchronen Vorgangs, bevor sie die resultierende Aufgabe zurückgibt. Synchrone Arbeiten sollten auf ein Minimum beschränkt werden, damit die asynchrone Methode schnell zurückgeben kann. Gründe für eine schnelle Rückgabe umfassen Folgendes:  
  
-   Asynchrone Methoden können von den Threads der Benutzeroberfläche aufgerufen werden und jede synchrone Arbeit mit langer Laufzeit kann die Reaktionszeit der Anwendung beeinträchtigen.  
  
-   Mehrere asynchrone Methoden können gleichzeitig ausgelöst werden. Daher kann jede Arbeit mit langer Laufzeit im synchronen Teil einer asynchronen Methode die Initiierung anderer asynchroner Operationen verzögern und so sie die Vorteile der Nebenläufigkeit verringern.  
  
 In einigen Fällen ist der Arbeitsaufwand, der erforderlich ist, um den Vorgang abzuschließen, kleiner als der Arbeitsaufwand, der erforderlich ist, um den Vorgang asynchron zu starten. Lesen aus einem Stream, bei dem der Lesevorgang durch Daten erfüllt werden kann, die bereits im Arbeitsspeicher gepuffert werden, ist ein Beispiel für ein solches Szenario. In solchen Fällen wird der Vorgang möglicherweise synchron abgeschlossen, und eine bereits abgeschlossene Aufgabe kann zurückgegeben werden.  
  
## <a name="exceptions"></a>Ausnahmen  
 Eine asynchrone Methode sollte nur Ausnahmen auslösen, die aufgrund eines Verwendungsfehlers beim Aufruf der asynchronen Methode ausgelöst werden. Verwendungsfehler sollten nie im Produktionscode auftreten. Verursacht beispielsweise die Übergabe eines NULL-Verweises (`Nothing` in Visual Basic) als eines der Argumente der Methode einen Fehlerzustand (normalerweise dargestellt durch eine <xref:System.ArgumentNullException>-Ausnahme), können Sie den Aufrufcode ändern, um sicherzustellen, dass nie ein NULL-Verweis übergeben wird. Für alle anderen Fehler sollten Ausnahmen, die beim Ausführen einer asynchronen Methode auftreten, der zurückgegebenen Aufgabe zugewiesen werden. Dies gilt auch dann, wenn die asynchrone Methode zufällig synchron abschließt, bevor die Aufgabe zurückgegeben wird. In der Regel enthält eine Aufgabe höchstens eine Ausnahme. Falls die Aufgabe jedoch mehrere Vorgänge darstellt (beispielsweise bei <xref:System.Threading.Tasks.Task.WhenAll%2A>), können einer einzelnen Aufgabe mehrere Ausnahmen zugeordnet werden.  
  
## <a name="target-environment"></a>Zielumgebung  
 Wenn Sie eine TAP-Methode implementieren, können Sie bestimmen, wo die asynchrone Ausführung auftritt. Sie können die Arbeitslast im Threadpool ausführen lassen, sie mithilfe einer asynchronen E/A implementieren (sodass sie für den Großteil der Ausführung des Vorgangs nicht an einen Thread gebunden ist), sie nach Bedarf in einem bestimmten Thread (z. B. dem UI-Thread) oder einer beliebigen Anzahl von anderen potenziellen Kontexten ausführen lassen. Es kann sogar vorkommen, dass eine TAP-Methode nichts ausführt und nur einen <xref:System.Threading.Tasks.Task> zurückgibt, der das Auftreten einer Bedingung an anderer Stelle im System darstellt (z.B. einen Task, der bei einer Datenstruktur in der Warteschlange eingehende Daten darstellt).
 
 Die aufrufende Funktion der TAP-Methode blockiert möglicherweise den Wartevorgang für die TAP-Methode, indem synchron auf den resultierenden Task gewartet wird, oder führt eventuell zusätzlichen (Fortsetzungs-)Code aus, wenn der asynchrone Vorgang abgeschlossen ist. Der Ersteller des Fortsetzungscodes steuert, wo dieser Code ausgeführt wird. Sie können diesen Fortsetzungscode entweder explizit durch Methoden der <xref:System.Threading.Tasks.Task>-Klasse (z. B. <xref:System.Threading.Tasks.Task.ContinueWith%2A>) oder implizit mithilfe von Sprachunterstützung erstellen, die auf Fortsetzungen aufbaut (zum Beispiel `await` in C#, `Await` in Visual Basic, `AwaitValue` in F#).  
  
## <a name="task-status"></a>Aufgabenstatus  
 Die <xref:System.Threading.Tasks.Task>-Klasse stellt einen Lebenszyklus für asynchrone Vorgänge bereit, und dieser Zyklus wird durch die <xref:System.Threading.Tasks.TaskStatus>-Enumeration dargestellt. Für die Unterstützung von Ausnahmefällen von Typen, die von <xref:System.Threading.Tasks.Task> und <xref:System.Threading.Tasks.Task%601> abgeleitet werden, sowie für die Unterstützung der Trennung von Erstellung und Planung macht die <xref:System.Threading.Tasks.Task>-Klasse eine <xref:System.Threading.Tasks.Task.Start%2A>-Methode verfügbar. Von den öffentlichen <xref:System.Threading.Tasks.Task>-Konstruktoren erstellte Tasks werden als *inaktive Tasks* bezeichnet, da ihr Lebenszyklus im nicht geplanten Zustand <xref:System.Threading.Tasks.TaskStatus.Created> beginnt und sie erst im geplanten Zustand sind, wenn <xref:System.Threading.Tasks.Task.Start%2A> für diese Instanzen aufgerufen wird. 
 
 Der Lebenszyklus aller anderen Aufgaben beginnt im aktiven Zustand. Dies bedeutet, dass die asynchronen Vorgänge, die sie darstellen, bereits initiiert wurden, und dass ihr Aufgabenzustand ein anderer Enumerationswert als <xref:System.Threading.Tasks.TaskStatus.Created?displayProperty=nameWithType> ist. Alle Aufgaben, die von TAP-Methoden zurückgegeben werden, müssen aktiviert sein. **Wenn eine TAP-Methode intern den zurückzugebenden Task mit dem Konstruktor des Tasks instanziiert, muss die TAP-Methode vor dem Zurückgeben des Tasks <xref:System.Threading.Tasks.Task.Start%2A> für das <xref:System.Threading.Tasks.Task>-Objekt aufrufen.** Consumer einer TAP-Methode können davon ausgehen, dass die zurückgegebene Aufgabe aktiv ist, und sollten nicht versuchen, <xref:System.Threading.Tasks.Task.Start%2A> für einen von einer TAP-Methode zurückgegebenen <xref:System.Threading.Tasks.Task> aufzurufen. Der Aufruf von <xref:System.Threading.Tasks.Task.Start%2A> für eine aktive Aufgabe führt zu einer <xref:System.InvalidOperationException>-Ausnahme.  
  
## <a name="cancellation-optional"></a>Abbruch (optional)  
 Im TAP ist Abbruch sowohl für Implementierer asynchroner Methoden als auch für Consumer asynchroner Methoden optional. Wenn ein Vorgang einen Abbruch zulässt, macht er eine Überladung der asynchronen Methode verfügbar, die ein Abbruchtoken akzeptiert (<xref:System.Threading.CancellationToken>-Instanz). Gemäß der Konvention lautet der Name des Parameters `cancellationToken`.  
  
 [!code-csharp[Conceptual.TAP#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap/cs/examples1.cs#1)]
 [!code-vb[Conceptual.TAP#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap/vb/examples1.vb#1)]  
  
 Der asynchrone Vorgang überwacht dieses Token auf Abbruchanforderungen. Wenn es eine Abbruchanforderung empfängt, kann es diese Anforderung erfüllen und den Vorgang abbrechen. Wenn die Abbruchanforderung dazu führt, dass die Arbeit vorzeitig beendet wird, gibt die TAP-Methode eine Aufgabe zurück, die im <xref:System.Threading.Tasks.TaskStatus.Canceled>-Zustand beendet wird. Es ist kein Ergebnis verfügbar und keine Ausnahme wird ausgelöst.  Der Zustand <xref:System.Threading.Tasks.TaskStatus.Canceled> gilt als endgültiger (abgeschlossener) Zustand einer Aufgabe, ebenso wie die Zustände <xref:System.Threading.Tasks.TaskStatus.Faulted> und <xref:System.Threading.Tasks.TaskStatus.RanToCompletion>. Wenn eine Aufgabe im Zustand <xref:System.Threading.Tasks.TaskStatus.Canceled> ist, gibt ihre <xref:System.Threading.Tasks.Task.IsCompleted%2A>-Eigenschaft `true` zurück. Wenn eine Aufgabe im <xref:System.Threading.Tasks.TaskStatus.Canceled>-Zustand abgeschlossen wird, werden alle mit der Aufgabe registrierten Fortsetzungen geplant oder ausgeführt, es sei denn, eine Fortsetzungsmöglichkeit wie <xref:System.Threading.Tasks.TaskContinuationOptions.NotOnCanceled> wurde angegeben, um die Fortsetzung zu beenden. Die Ausführung von jedem Code, der mithilfe von Sprachfunktionen asynchron auf eine abgebrochene Aufgabe wartet, wird weiter ausgeführt, aber der Code empfängt eine <xref:System.OperationCanceledException>-Ausnahme oder eine von ihr abgeleitete Ausnahme. Synchron blockierter Code, der durch Methoden wie <xref:System.Threading.Tasks.Task.Wait%2A> und <xref:System.Threading.Tasks.Task.WaitAll%2A> auf die Aufgabe wartet, wird ebenso weiter mit einer Ausnahme ausgeführt.  
  
 Wenn ein Abbruchtoken den Abbruch angefordert hat, bevor die TAP-Methode, die dieses Token akzeptiert, aufgerufen wurde, sollte die TAP-Methode eine <xref:System.Threading.Tasks.TaskStatus.Canceled>-Aufgabe zurückgeben.  Wenn jedoch der Abbruch während der Ausführung des asynchronen Vorgangs angefordert wird, muss der asynchrone Vorgang die Abbruchanforderung nicht erfüllen.  Die zurückgegebene Aufgabe sollte nur dann im <xref:System.Threading.Tasks.TaskStatus.Canceled>-Zustand enden, wenn der Vorgang aufgrund einer Abbruchanforderung beendet wird. Wird der Abbruch angefordert aber dennoch ein Ergebnis oder eine Ausnahme erzeugt, sollte die Aufgabe im Zustand <xref:System.Threading.Tasks.TaskStatus.RanToCompletion> oder <xref:System.Threading.Tasks.TaskStatus.Faulted> enden. 
 
 Für asynchrone Methoden, bei denen in erster Linie die Funktion zu deren Abbruch verfügbar gemacht werden soll, müssen Sie keine Überladung bereitstellen, die kein Abbruchtoken akzeptiert. Für Methoden, die nicht abgebrochen werden können, sollten keine Überladungen bereitgestellt werden, die ein Abbruchstoken akzeptieren. So lässt sich leichter dem Aufrufer mitteilen, ob die Zielmethode tatsächlich abgebrochen werden kann.  Consumercode, der keinen Abbruch wünscht, wird möglicherweise eine Methode aufrufen, die <xref:System.Threading.CancellationToken> akzeptiert und <xref:System.Threading.CancellationToken.None%2A> als den Argumentwert bereitstellen. <xref:System.Threading.CancellationToken.None%2A> ist zu dem standardmäßigen <xref:System.Threading.CancellationToken> funktional äquivalent.  
  
## <a name="progress-reporting-optional"></a>Statusberichterstellung (optional)  
 Mehrere asynchrone Vorgänge profitieren von dem Bereitstellen von Statusbenachrichtigungen. Diese werden in der Regel verwendet, um eine Benutzeroberfläche mit Informationen zum Status der asynchronen Operation zu aktualisieren. 
 
 In TAP wird der Status wird durch eine <xref:System.IProgress%601>-Schnittstelle behandelt, die der asynchronen Methode als Parameter übergeben wird, der normalerweise `progress` genannt wird.  Durch das Bereitstellen der Statusschnittstelle zum Zeitpunkt des Aufrufs der asynchronen Methode lassen sich leichter Racebedingungen vermeiden, die aus falscher Verwendung resultieren (d. h., wenn Ereignishandler, die nach dem Aufruf des Vorgangs nicht ordnungsgemäß registriert wurden, möglicherweise Updates verpassen).  Vor allem unterstützt die Statusschnittstelle jedoch verschiedene Implementierungen des Status, die durch den verwendeten Code bestimmt werden.  Beispielsweise sollte der verwendete Code sich möglicherweise nur für das neueste Statusupdate interessieren oder alle Updates puffern oder eine Aktion für jedes Update aufrufen oder steuern, ob der Aufruf eines bestimmten Thread gemarshallt wird. Diese Optionen werden erreicht, indem eine andere Implementierung der Schnittstelle verwendet wird, die an bestimmte Anforderungen des Consumers angepasst wird.  Wie bei einem Abbruch sollten auch TAP-Implementierungen nur dann einen <xref:System.IProgress%601>-Parameter bereitstellen, wenn die API Statusbenachrichtigungen unterstützt. 
 
 Wenn beispielsweise die weiter oben in diesem Artikel beschriebene `ReadAsync`-Methode in der Lage ist, einen Zwischenstatus in Form der Anzahl von bisher gelesenen Bytes zu melden, könnte der Statusrückruf eine <xref:System.IProgress%601>-Schnittstelle sein:  
  
 [!code-csharp[Conceptual.TAP#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap/cs/examples1.cs#2)]
 [!code-vb[Conceptual.TAP#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap/vb/examples1.vb#2)]  
  
 Wenn eine `FindFilesAsync`-Methode eine Liste aller Dateien zurückgegeben hat, die einem bestimmten Suchmuster entsprechen, kann der Statusrückruf einen geschätzten Prozentsatz der abgeschlossenen Arbeit sowie den aktuellen Satz von partiellen Ergebnissen bereitstellen.  Dies kann entweder mit einem Tupel erfolgen:  
  
 [!code-csharp[Conceptual.TAP#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap/cs/examples1.cs#3)]
 [!code-vb[Conceptual.TAP#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap/vb/examples1.vb#3)]  
  
 oder mit einem für die API spezifischen Datentyp:  
  
 [!code-csharp[Conceptual.TAP#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.tap/cs/examples1.cs#4)]
 [!code-vb[Conceptual.TAP#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.tap/vb/examples1.vb#4)]  
  
 In letzterem Fall wird an den speziellen Datentyp für gewöhnlich das Suffix `ProgressInfo` angefügt werden.  
  
 Wenn TAP-Implementierungen Überladungen bereitstellen, die einen Statusparameter akzeptieren, müssen sie den Wert `progress` für das Argument `null` zulassen. In diesem Fall wird kein Status gemeldet. TAP-Implementierungen sollten den Status synchron an das <xref:System.Progress%601>-Objekt melden, das die asynchrone Methode ermöglicht, um den Status schnell bereitzustellen und dem Consumer des Status ermöglichen, zu bestimmen wie und wo die Informationen am besten bearbeitet werden. Zum Beispiel kann die Statusinstanz Rückrufe marshallen und Ereignisse auf einem aufgezeichneten Synchronisierungskontext auslösen.  
  
## <a name="iprogresst-implementations"></a>IProgress\<T>-Implementierungen  
 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] stellt eine einzelne <xref:System.IProgress%601>-Implementierung bereit: <xref:System.Progress%601>. Die <xref:System.Progress%601>-Klasse wird folgendermaßen deklariert:  
  
```csharp  
public class Progress<T> : IProgress<T>  
{  
    public Progress();  
    public Progress(Action<T> handler);  
    protected virtual void OnReport(T value);  
    public event EventHandler<T> ProgressChanged;  
}  
```  
  
```vb  
Public Class Progress(Of T) : Inherits IProgress(Of T)  
    Public Sub New()  
    Public Sub New(handler As Action(Of T))  
    Protected Overridable Sub OnReport(value As T)  
    Public Event ProgressChanged As EventHandler(Of T>  
End Class  
```  
  
 Eine Instanz von <xref:System.Progress%601> macht ein <xref:System.Progress%601.ProgressChanged>-Ereignis verfügbar, das jedes Mal ausgelöst wird, wenn der asynchrone Vorgang ein Statusupdate meldet. Das <xref:System.Progress%601.ProgressChanged>-Ereignis wird auf das <xref:System.Threading.SynchronizationContext>-Objekt ausgelöst, das aufgezeichnet wurde, als die <xref:System.Progress%601>-Instanz instanziiert wurde. Wenn kein Synchronisierungskontext verfügbar war, wird ein Standardkontext, der auf den Threadpool abzielt, verwendet. Handler können mit diesem Ereignis registriert werden. Ein einzelner Handler kann auch dem <xref:System.Progress%601>-Konstruktor nach Wunsch bereitgestellt werden und verhält sich wie ein Ereignishandler für das <xref:System.Progress%601.ProgressChanged>-Ereignis. Statusupdates werden asynchron ausgelöst, um den asynchronen Vorgang zu verzögern, während der Ereignishandler ausgeführt wird. Eine andere <xref:System.IProgress%601>-Implementierung kann festlegen, dass andere Semantik anzuwenden ist.  
  
## <a name="choosing-the-overloads-to-provide"></a>Auswählen der bereitzustellenden Überladungen  
 Verwendet eine TAP-Implementierung sowohl den optionalen Parameter <xref:System.Threading.Tasks.TaskFactory.CancellationToken%2A> als auch den optionalen Parameter <xref:System.IProgress%601>, kann dies möglicherweise bis zu vier Überladungen erfordern:  
  
```csharp  
public Task MethodNameAsync(…);  
public Task MethodNameAsync(…, CancellationToken cancellationToken);  
public Task MethodNameAsync(…, IProgress<T> progress);   
public Task MethodNameAsync(…,   
    CancellationToken cancellationToken, IProgress<T> progress);  
```  
  
```vb  
Public MethodNameAsync(…) As Task  
Public MethodNameAsync(…, cancellationToken As CancellationToken cancellationToken) As Task  
Public MethodNameAsync(…, progress As IProgress(Of T)) As Task   
Public MethodNameAsync(…, cancellationToken As CancellationToken,   
                       progress As IProgress(Of T)) As Task  
```  
  
 Viele TAP-Implementierungen bieten jedoch weder Abbruchs- noch Statusfunktionen und erfordern daher eine einzelne Methode:  
  
```csharp  
public Task MethodNameAsync(…);  
```  
  
```vb  
Public MethodNameAsync(…) As Task  
```  
  
 Wenn eine TAP-Implementierung entweder Abbruch oder Status, jedoch nicht beides unterstützt, kann sie zwei Überladungen bereitstellen:  
  
```csharp  
public Task MethodNameAsync(…);  
public Task MethodNameAsync(…, CancellationToken cancellationToken);  
  
// … or …  
  
public Task MethodNameAsync(…);  
public Task MethodNameAsync(…, IProgress<T> progress);  
```  
  
```vb  
Public MethodNameAsync(…) As Task  
Public MethodNameAsync(…, cancellationToken As CancellationToken) As Task  
  
' … or …  
  
Public MethodNameAsync(…) As Task  
Public MethodNameAsync(…, progress As IProgress(Of T)) As Task  
```  
  
 Wenn eine TAP-Implementierung Abbruch und Status unterstützt, kann sie alle vier Überladungen verfügbar machen. Sie kann jedoch möglicherweise nur die Folgenden zwei bereitstellen:  
  
```csharp  
public Task MethodNameAsync(…);  
public Task MethodNameAsync(…,   
    CancellationToken cancellationToken, IProgress<T> progress);  
```  
  
```vb  
Public MethodNameAsync(…) As Task  
Public MethodNameAsync(…, cancellationToken As CancellationToken,   
                       progress As IProgress(Of T)) As Task  
```  
  
 Als Ausgleich für die zwei fehlenden Zwischenkombinationen können Entwickler <xref:System.Threading.CancellationToken.None%2A> oder ein standardmäßiges <xref:System.Threading.CancellationToken> für den `cancellationToken`-Parameter und `null` für den `progress`-Parameter übergeben.  
  
 Wenn Sie erwarten, dass jede Verwendung der TAP-Methode Abbruch oder Status unterstützt, können Sie die Überladungen, die den relevanten Parameter nicht akzeptieren, weglassen.  
  
 Wenn Sie sich dazu entschließen, mehrere Überladungen verfügbar zu machen, um Abbruch und/oder Status optional zu machen, sollte das Verhalten der Überladungen, die Abbruch und/oder Status nicht unterstützen, dem Verhalten einer Überladung entsprechen, die <xref:System.Threading.CancellationToken.None%2A> für Abbruch oder `null` für Status an die Überladung übergibt, die Abbruch bzw. Status unterstützt.  
  
## <a name="related-topics"></a>Verwandte Themen  
  
|Titel|description|  
|-----------|-----------------|  
|[Muster für die asynchrone Programmierung](../../../docs/standard/asynchronous-programming-patterns/index.md)|Stellt die drei Muster zum Ausführen von asynchronen Vorgängen vor: das aufgabenbasierte asynchrone Muster (TAP), das asynchrone Programmiermodell (APM) und das ereignisbasierte asynchrone Muster (EAP).|  
|[Implementieren des aufgabenbasierten asynchronen Entwurfsmusters](../../../docs/standard/asynchronous-programming-patterns/implementing-the-task-based-asynchronous-pattern.md)|Beschreibt, wie Sie das aufgabenbasierte asynchrone Muster (Task-based Asynchronous Pattern, TAP) auf drei Arten implementieren können: mit C# und den Visual Basic-Compilern in Visual Studio, manuell oder mit einer Kombination von Compilermethoden und manuellen Methoden.|  
|[Nutzen des aufgabenbasierten asynchronen Musters](../../../docs/standard/asynchronous-programming-patterns/consuming-the-task-based-asynchronous-pattern.md)|Beschreibt, wie Sie Aufgaben und Rückrufe verwenden können, um eine Verzögerung ohne Blockierung zu erreichen.|  
|[Interoperabilität mit anderen asynchronen Mustern und Typen](../../../docs/standard/asynchronous-programming-patterns/interop-with-other-asynchronous-patterns-and-types.md)|Beschreibt, wie das aufgabenbasierte asynchrone Muster (TAP) verwendet werden kann, um das asynchrone Programmiermodell (APM) und das ereignisbasierte asynchrone Muster (EAP) zu implementieren.|
