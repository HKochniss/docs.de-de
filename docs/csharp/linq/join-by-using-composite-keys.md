---
title: "Verknüpfen mithilfe eines zusammengesetzten Schlüssels"
description: "Vorgehensweise: Verknüpfen mithilfe eines zusammengesetzten Schlüssels."
keywords: .NET, .NET Core, C#
author: BillWagner
manager: wpickett
ms.author: wiwagn
ms.date: 12/1/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.assetid: da70b54d-3213-45eb-8437-fbe75cbcf935
ms.openlocfilehash: c285e768d64d1da7e428e29fc67838e87575500c
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="join-by-using-composite-keys"></a>Verknüpfen mithilfe eines zusammengesetzten Schlüssels

In diesem Beispiel erfahren Sie, wie sie Verknüpfungsvorgänge durchführen können, in denen Sie mehr als einen Schlüssel zur Definition einer Übereinstimmung verwenden möchten. Dies können Sie mithilfe eines zusammengesetzten Schlüssels machen. Ein zusammengesetzter Schlüssel wird als anonymer oder benannter Typ mit den Werten, die Sie vergleichen möchten, erstellt. Wenn die Abfragevariable methodengrenzenübergreifend übergeben wird, verwenden Sie einen benannten Typ, der <xref:System.Object.Equals%2A> und <xref:System.Object.GetHashCode%2A> für den Schlüssel außer Kraft setzt. Der Name der Eigenschaften und die Reihenfolge, in der diese auftreten, muss in jedem Schlüssel identisch sein.  
  
## <a name="example"></a>Beispiel  
 In folgendem Beispiel erfahren Sie, wie Sie einen zusammengesetzten Schlüssel verwenden können, um Daten aus drei Tabellen zu verknüpfen:  
  
```csharp  
var query = from o in db.Orders  
    from p in db.Products  
    join d in db.OrderDetails   
        on new {o.OrderID, p.ProductID} equals new {d.OrderID,        d.ProductID} into details  
        from d in details  
        select new {o.OrderID, p.ProductID, d.UnitPrice};  
```  
  
 Typrückschluss für zusammengesetzte Schlüssel hängt von den Namen der Eigenschaften in den Schlüsseln und deren Reihenfolge ab. Wenn die Eigenschaften der Quellsequenz nicht dieselben Namen haben, müssen Sie ihnen im Schlüssel neue Namen zuweisen. Wenn in den Tabellen `Orders` und `OrderDetails` beispielsweise unterschiedliche Namen für die Spalten verwendet werden, können Sie zusammengesetzte Schlüssel erstellen, indem Sie identische Namen in den anonymen Typen zuweisen:  
  
```csharp  
join...on new {Name = o.CustomerName, ID = o.CustID} equals   
    new {Name = d.CustName, ID = d.CustID }  
```  
  
 Zusammengesetzte Schlüssel können auch in einer `group`-Klausel verwendet werden.  

## <a name="see-also"></a>Siehe auch  
 [LINQ-Abfrageausdrücke](index.md)  
 [join-Klausel](../language-reference/keywords/join-clause.md)  
 [group-Klausel](../language-reference/keywords/group-clause.md)
