---
title: Modellieren und Zuordnen
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ec8a9515-3708-4cde-a688-4d8e6975f150
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 0782d75aa44557ef87f1d59757b0d60873d8a949
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="modeling-and-mapping"></a>Modellieren und Zuordnen
In [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] können Sie das konzeptionelle Modell, das Speichermodell und die Zuordnung zwischen beiden auf die Weise definieren, die der Anwendung am besten entspricht. Das Entity Data Model-Tools in [!INCLUDE[vsprvs](../../../../../includes/vsprvs-md.md)] ermöglichen Ihnen die Erstellung einer.[ EDMX-Datei](http://msdn.microsoft.com/library/f4c8e7ce-1db6-417e-9759-15f8b55155d4) aus einer Datenbank oder einem grafischen Modell und aktualisieren Sie dann die Datei, wenn die Datenbank oder das Modell ändert.  
  
 Ab Entity Framework 4.1 können Sie ein Modell anhand der Code First-Entwicklung auch programmgesteuert erstellen. Es gibt zwei verschiedene Szenarien für die Code First-Entwicklung. In beiden Fällen definiert der Entwickler ein Modell, indem er .NET Framework-Klassendefinitionen codiert und dann optional zusätzliche Zuordnungen oder Konfigurationen mithilfe von Datenanmerkungen oder der Fluent-API angibt.  
  
 Weitere Informationen finden Sie unter [erstellen und Zuordnen eines konzeptionellen Modells](http://go.microsoft.com/fwlink/?LinkId=235016).  
  
 Sie können auch den EDM-Generator, der in der [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)]. EdmGen.exe generiert die CSDL-, SSDL- und MSL-Dateien aus einer vorhandenen Datenquelle. Sie können Modell- und Zuordnungsinhalte auch manuell erstellen. Weitere Informationen finden Sie unter [EDM Generator (EdmGen.exe)](../../../../../docs/framework/data/adonet/ef/edm-generator-edmgen-exe.md).
