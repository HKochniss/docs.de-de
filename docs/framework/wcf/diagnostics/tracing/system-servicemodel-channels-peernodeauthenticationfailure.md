---
title: System.ServiceModel.Channels.PeerNodeAuthenticationFailure
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b50f782-ca06-4a82-aa7f-71f78ddc5177
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 4ffca9a587bdb32afc252f9719eb35e3139dd3f8
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="systemservicemodelchannelspeernodeauthenticationfailure"></a>System.ServiceModel.Channels.PeerNodeAuthenticationFailure
Der Sicherheitshandshake mit einem potenziellen Nachbarn war nicht erfolgreich.  
  
## <a name="description"></a>Beschreibung  
 Diese Ablaufverfolgung tritt beim Herstellen einer sicheren Nachbarverbindung auf. Dies kann aufgrund ungenügender oder falscher Anmeldeinformationen geschehen.  
  
 PeerChannel erkennt einen einzelnen Tokentyp für eine starke Identifizierung, X.509-Zertifikate, die ein starkes Identifikationsmodell bereitstellen, das auf dem Typ der Authentifizierung und der Autorisierung basiert, der implementiert werden kann. PeerChannel unterstützt darüber hinaus einfache Anwendungen durch die Verwendung von Kennwörtern. Kennwörter können nur verwendet werden, um Zugang zu einer Sitzung zu erhalten. Die Durchführung von Nachrichtenauthentifizierung über Kennwörter ist nicht möglich. Grund hierfür ist, dass ein symmetrischer Token, den sich eine Peergruppe teilt, für die Quellenauthentifizierung schwierig und ungeeignet ist.  
  
## <a name="troubleshooting"></a>Problembehandlung  
 Stellen Sie sicher, dass alle Nachbarn über geeignete Sicherheitsanmeldeinformationen verfügen.  
  
## <a name="see-also"></a>Siehe auch  
 [Peerkanalsicherheit](../../../../../docs/framework/wcf/feature-details/peer-channel-security.md)  
 [Ablaufverfolgung](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)  
 [Verwenden der Ablaufverfolgung zum Beheben von Anwendungsfehlern](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)  
 [Verwaltung und Diagnose](../../../../../docs/framework/wcf/diagnostics/index.md)
