---
title: Laden von Daten in ein DataSet
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
ms.assetid: a53e5dc1-9669-49d4-828d-efa633237066
caps.latest.revision: "2"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 4be4c1aa449c3bd78774c6aafe1ec2b55b27b663
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="loading-data-into-a-dataset"></a>Laden von Daten in ein DataSet
Ein <xref:System.Data.DataSet>-Objekt muss zuerst aufgefüllt werden, bevor Sie es mit [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] abfragen können. Das Auffüllen des <xref:System.Data.DataSet>-Objekts kann auf verschiedene Art und Weise erfolgen. Beispielsweise können Sie [!INCLUDE[vbtecdlinq](../../../../includes/vbtecdlinq-md.md)] um die Datenbank abzufragen und lädt die Ergebnisse in die <xref:System.Data.DataSet>. Weitere Informationen finden Sie unter [LINQ to SQL](../../../../docs/framework/data/adonet/sql/linq/index.md).  
  
 Eine andere Möglichkeit, Daten in ein <xref:System.Data.DataSet> zu laden, besteht darin, Daten mithilfe der <xref:System.Data.Common.DataAdapter>-Klasse aus der Datenbank abzurufen. Dies wird im folgenden Beispiel illustriert.  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel wird ein <xref:System.Data.Common.DataAdapter> verwendet, um aus der <legacyBold>AdventureWorks</legacyBold>-Datenbank Verkaufsinformationen für das Jahr 2002 abzurufen und die Ergebnisse in ein <xref:System.Data.DataSet> zu laden. Nachdem das <xref:System.Data.DataSet> aufgefüllt wurde, können Sie mithilfe von [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)]-Abfragen Daten aus ihm abrufen. Die `FillDataSet` -Methode in diesem Beispiel werden in den Beispielabfragen in [LINQ to DataSet-Beispiele](../../../../docs/framework/data/adonet/linq-to-dataset-examples.md). Weitere Informationen finden Sie unter [Abfragen von DataSets](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md).  
  
 [!code-csharp[DP LINQ to DataSet Examples#FillDataSet](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/CS/Program.cs#filldataset)]
 [!code-vb[DP LINQ to DataSet Examples#FillDataSet](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP LINQ to DataSet Examples/VB/Module1.vb#filldataset)]  
  
## <a name="see-also"></a>Siehe auch  
 [Übersicht über LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset-overview.md)  
 [Abfragen von DataSets](../../../../docs/framework/data/adonet/querying-datasets-linq-to-dataset.md)  
 [Beispiele für LINQ to DataSet](../../../../docs/framework/data/adonet/linq-to-dataset-examples.md)
