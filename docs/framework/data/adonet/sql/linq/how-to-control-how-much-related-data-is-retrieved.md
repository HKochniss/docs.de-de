---
title: 'Gewusst wie: Steuern, wie viel verbundene Daten abgerufen werden'
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
ms.assetid: efdc203e-3da9-4477-815e-54f10c3d7c6c
caps.latest.revision: "2"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 3beb6f6b019535e273df7103e2e22f1be669797a
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="how-to-control-how-much-related-data-is-retrieved"></a>Gewusst wie: Steuern, wie viel verbundene Daten abgerufen werden
Geben Sie mit der <xref:System.Data.Linq.DataLoadOptions.LoadWith%2A>-Methode an, welche mit Ihrem Hauptziel verbundenen Daten gleichzeitig abgerufen werden sollen. Wenn Sie beispielsweise Informationen über die Bestellungen eines Kunden benötigen, können Sie mithilfe von <xref:System.Data.Linq.DataLoadOptions.LoadWith%2A> sicherstellen, dass die Bestellinformationen zusammen mit den Kundeninformationen abgerufen werden. Dadurch können beide Informationssätze in einem Vorgang aus der Datenbank abgerufen werden.  
  
> [!NOTE]
>  Sie können Daten zum Hauptziel Ihrer Anfrage abrufen, indem Sie eine produktübergreifende Abfrage in Form einer großen Projektion abrufen (z. B. werden Bestellungen abgerufen, wenn Sie auf Kunden abzielen). Dieser Ansatz hat oft Nachteile. Die Ergebnisse sind beispielsweise nur Projektionen und keine Entitäten, die mit [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] geändert und erhalten werden können. Außerdem können Sie viele Daten abrufen, die Sie nicht benötigen.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel werden alle `Orders` (Bestellungen) für alle `Customers` (Kunden) in London abgerufen, wenn die Abfrage ausgeführt wird. Aufgrund dessen wird bei nachfolgenden Zugriffen auf die `Orders`-Eigenschaft für ein `Customer`-Objekt keine neue Datenbankabfrage ausgelöst.  
  
 [!code-csharp[System.Data.Linq.DataLoadOptions#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.dataloadoptions/cs/program.cs#2)]
 [!code-vb[System.Data.Linq.DataLoadOptions#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.dataloadoptions/vb/module1.vb#2)]  
  
## <a name="see-also"></a>Siehe auch  
 [Abfragen der Datenbank](../../../../../../docs/framework/data/adonet/sql/linq/querying-the-database.md)
