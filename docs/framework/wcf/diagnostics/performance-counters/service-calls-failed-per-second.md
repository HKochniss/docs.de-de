---
title: 'Dienst: Fehlerhafte Anrufe pro Sekunde'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5a2c7939-107d-4f0c-b43c-e02e079e8a9d
caps.latest.revision: "11"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 632c81b6ffd84202b7609dccb89887af01ae706e
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="service-calls-failed-per-second"></a>Dienst: Fehlerhafte Anrufe pro Sekunde
Indikatorname: Calls Failed Per Second  
  
## <a name="description"></a>Beschreibung  
 Die Anzahl von Aufrufen, die nicht behandelte Ausnahmen aufweisen und von diesem Dienst in einer Sekunde empfangen werden.  
  
 Dieser Indikator wird der Leistungsindikator vom Typ [PERF_COUNTER_COUNTER](http://go.microsoft.com/fwlink/?LinkID=94649), dessen Wert anhand der folgenden Formel berechnet wird.  
  
 (N 1 - N 0)/( (D 1 - D 0)/F)  
  
 In verwaltetem Code werden Ausnahmen bei Auftreten von Fehlerbedingungen ausgelöst.  
  
 In verwaltetem Code werden Ausnahmen bei Auftreten von Fehlerbedingungen ausgelöst.  
  
 Der Wert dieses Indikators erhöht sich jedes Mal, wenn in diesem Dienst eine nicht behandelte Ausnahme auftritt.  
  
## <a name="see-also"></a>Siehe auch  
 [Angeben und Behandeln von Fehlern in Verträgen und Diensten](../../../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)
