---
title: 'Gewusst wie: Bereitstellen von Modell- und Zuordnungsdateien als eingebettete Ressourcen'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 20dfae4d-e95a-4264-9540-f5ad23b462d3
caps.latest.revision: "3"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 60c17ebbdd4b7e7f460855d4888a922da9c953d2
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="how-to-make-model-and-mapping-files-embedded-resources"></a>Gewusst wie: Bereitstellen von Modell- und Zuordnungsdateien als eingebettete Ressourcen
Die [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] ermöglicht es Ihnen, Modell- und Zuordnungsdateien als eingebettete Ressourcen einer Anwendung bereitstellen. Die Assembly mit den eingebetteten Modell- und Zuordnungsdatendateien muss in derselben Anwendungsdomäne geladen werden wie die Entitätsverbindung. Weitere Informationen finden Sie in [Verbindungszeichenfolgen](../../../../../docs/framework/data/adonet/ef/connection-strings.md). Standardmäßig betten die [!INCLUDE[adonet_edm](../../../../../includes/adonet-edm-md.md)]-Tools die Modell- und Zuordnungsdateien ein. Wenn Sie die Modell- und Zuordnungsdateien manuell definieren, verwenden Sie diese Prozedur, um sicherzustellen, dass die Dateien als eingebettete Ressourcen zusammen mit einer [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]-Anwendung bereitgestellt werden.  
  
> [!NOTE]
>  Wiederholen Sie diese Prozedur, wenn Modell- und Zuordnungsdateien geändert werden, um eingebettete Ressourcen beizubehalten.  
  
### <a name="to-embed-model-and-mapping-files"></a>So betten Sie Modell- und Zuordnungsdateien ein  
  
1.  In **Projektmappen-Explorer**, wählen Sie die konzeptionelle (CSDL) Datei.  
  
2.  In der **Eigenschaften** Bereich festgelegt **Buildvorgang** auf **eingebettete Ressource**.  
  
3.  Wiederholen Sie die Schritte 1 und 2 für die SSDL-Speicherdatei und die MSL-Zuordnungsdatei.  
  
4.  In **Projektmappen-Explorer**, doppelklicken Sie auf die Datei "App.config", und ändern Sie die `Metadata` Parameter in der `connectionString` Attribut basierend auf einem der folgenden Formate:  
  
    -   `Metadata=` `res://<assemblyFullName>/<resourceName>;`  
  
    -   `Metadata=` `res://*/<resourceName>;`  
  
    -   `Metadata=res://*;`  
  
     Weitere Informationen finden Sie in [Verbindungszeichenfolgen](../../../../../docs/framework/data/adonet/ef/connection-strings.md).  
  
## <a name="example"></a>Beispiel  
 Die folgende Verbindungszeichenfolge verweist auf eingebettete Modell- und Zuordnungsdateien für die [AdventureWorks Sales-Modell](http://msdn.microsoft.com/library/f16cd988-673f-4376-b034-129ca93c7832). Diese Verbindungszeichenfolge wird in der Datei App.config des Projekts gespeichert.  
  
  
  
## <a name="see-also"></a>Siehe auch  
 [Modellieren und Zuordnen](../../../../../docs/framework/data/adonet/ef/modeling-and-mapping.md)  
 [Vorgehensweise: Definieren der Verbindungszeichenfolge](../../../../../docs/framework/data/adonet/ef/how-to-define-the-connection-string.md)  
 [Vorgehensweise: Erstellen einer EntityConnection-Verbindungszeichenfolge](../../../../../docs/framework/data/adonet/ef/how-to-build-an-entityconnection-connection-string.md)  
 [ADO.NET Entity Data Model Tools (ADO.NET Entity Data Model-Tools)](http://msdn.microsoft.com/library/91076853-0881-421b-837a-f582f36be527)
