---
title: 'Gewusst wie: Verwenden von benutzerdefinierten Tabellenwertfunktionen'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: 5a4ae2b4-3290-4aa1-bc95-fc70c51b54cf
caps.latest.revision: "2"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: c8ec97e0d083ccdd17a97db571d58aae9afbeea8
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="how-to-use-table-valued-user-defined-functions"></a>Gewusst wie: Verwenden von benutzerdefinierten Tabellenwertfunktionen
Eine Tabellenwertfunktion gibt ein einzelnes Rowset (im Gegensatz zu gespeicherten Prozeduren, die mehrere Ergebnisformen zurückgeben können) zurück. Da der Rückgabetyp einer Tabellenwertfunktion `Table` lautet, können Sie eine Tabellenwertfunktion überall dort in SQL nutzen, wo Sie eine Tabelle verwenden können. Außerdem können Sie die Tabellenwertfunktion so wie eine Tabelle behandeln.  
  
## <a name="example"></a>Beispiel  
 Die folgende SQL-Funktion legt explizit fest, dass sie eine `TABLE` zurückgibt. Deshalb wird die zurückgegebene Rowsetstruktur implizit definiert.  
  
```  
CREATE FUNCTION ProductsCostingMoreThan(@cost money)  
RETURNS TABLE  
AS  
RETURN  
    SELECT ProductID, UnitPrice  
    FROM Products  
    WHERE UnitPrice > @cost  
```  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ordnet die Funktion wie folgt zu:  
  
 [!code-csharp[DLinqUDFS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqUDFS/cs/northwind-tfunc.cs#1)]
 [!code-vb[DLinqUDFS#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqUDFS/vb/northwind-tfunc.vb#1)]  
  
## <a name="example"></a>Beispiel  
 Der folgende SQL-Code zeigt, dass Sie einen Join zu der von der Funktion zurückgegebenen Tabelle herstellen können. Andernfalls erfolgt die Behandlung wie bei jeder anderen Tabelle:  
  
```  
SELECT p2.ProductName, p1.UnitPrice  
FROM dbo.ProductsCostingMoreThan(80.50)  
AS p1 INNER JOIN Products AS p2 ON p1.ProductID = p2.ProductID  
```  
  
 In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] würde die Abfrage wie folgt gerendert werden:  
  
 [!code-csharp[DLinqUDFS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqUDFS/cs/Program.cs#2)]
 [!code-vb[DLinqUDFS#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqUDFS/vb/Module1.vb#2)]  
  
## <a name="see-also"></a>Siehe auch  
 [Benutzerdefinierte Funktionen](../../../../../../docs/framework/data/adonet/sql/linq/user-defined-functions.md)
