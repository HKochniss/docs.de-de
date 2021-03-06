---
title: Was ist Docker?
description: Lebenszyklus von Docker-Containeranwendungen mit der Microsoft-Plattform und Tools
keywords: Docker, Microservices, ASP.NET, Container
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/21/2017
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: c75b2fa87e5aad93693c76c3bbd135044b36525f
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/19/2018
---
# <a name="what-is-docker"></a>Was ist Docker?

[Docker](https://www.docker.com/) ist ein [Open Source-Projekts](https://github.com/docker/docker) zum Automatisieren der Bereitstellung von Anwendungen als portable, eigenständiger Container, die in der Cloud oder lokal ausgeführt werden kann (siehe Abbildung 1 - 2). Docker ist auch eine [Unternehmen](https://www.docker.com/) , stuft und diese Technologie, arbeiten in Zusammenarbeit mit der Cloud, Linux und Windows-Herstellern, einschließlich Microsoft entwickelt.

![](./media/image2.png)

Abbildung 1-2: Docker stellt Container auf allen Ebenen der hybridcloud

Docker-Image-Container können systemintern auf Linux- und Windows ausgeführt. Allerdings Windows-Images können nur auf Windows-Hosts ausführen und Linux-Images können nur auf Linux-Hosts, d. h. eine Hostserver oder einem virtuellen Computer ausgeführt.

Entwickler können entwicklungsumgebungen auf Windows, Linux oder MacOS verwenden. Auf dem Entwicklungscomputer führt der Entwickler einen Docker-Host, auf welche, den docker Images bereitgestellt werden, einschließlich der app und die zugehörigen Abhängigkeiten, an. Entwickler, die unter Linux oder auf dem Mac arbeiten, verwenden einen Docker-Host, der auf Linux basierende ist, und sie können Bilder, die nur für Linux-Container erstellen. (Entwickler, die auf dem Mac arbeiten können Code bearbeiten, oder führen Sie die Docker-Befehlszeilenschnittstelle \[CLI\] aus MacOS, jedoch Verfassung dieses Dokuments, Container führen nicht direkt auf MacOS.) Entwickler, die unter Windows zusammenarbeiten können Bilder für Linux- oder Windows-Container erstellen.

Zum Hosten von Containern in entwicklungsumgebungen, und geben Sie zusätzliche Entwicklertools, Docker geliefert wird [Docker Community Edition (CE)](https://www.docker.com/community-edition) für Windows oder MacOS. Diese Produkte installieren die erforderliche VM (die Docker-Host) zum Hosten der Container an. Docker stellt auch zur Verfügung [Docker Enterprise Edition (EE)](https://www.docker.com/enterprise-edition), die ist für die Entwicklung für Unternehmen konzipiert und werden vom IT-Teams erstellen, liefern und große unternehmenswichtige Anwendungen unter Produktionsbedingungen ausführen.

Auszuführende [Windows-Containern](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview), es gibt zwei Arten von Laufzeiten:

-   **Windows Server-Container** dieser Laufzeit bietet Anwendungsisolation mittels einer isolationstechnologie für Prozesse und Namespaces. Windows Server-Container teilt sich einen Kernel mit dem containerhost und allen Container, die auf dem Host ausgeführt.

-   **Hyper-V-Container** erstreckt sich auf die Isolierung durch Windows Server-Container, indem jeder Container in einem hochgradig optimierten virtuellen Computer ausgeführt wird. In dieser Konfiguration wird der Kernel des containerhosts nicht gemeinsam mit Hyper-V-Container, eine bessere Isolierung bereitstellen.

Die Images für diese Container werden auf die gleiche Weise erstellt und sind funktional gleich. Der Unterschied besteht darin, wie der Container aus dem Image erstellt wird – einen zusätzlichen Parameter erfordert ein Hyper-V-Container ausgeführt wird. Weitere Informationen finden Sie unter [Hyper-V-Container](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview).

## <a name="comparing-docker-containers-with-vms"></a>Vergleich von Docker-Containern mit virtuellen Computern

Abbildung 1 bis 3 zeigt einen Vergleich zwischen virtuellen Computern und die Docker Container.

Da Container wesentlich weniger Ressourcen benötigen (z. B. sie ist nicht erforderlich, eine Vollversion des Betriebssystems), werden einfach bereitzustellen und schnell beginnen. Dies ermöglicht es Ihnen höhere Dichte, was bedeutet, dass Sie auf der gleichen Hardware-Einheit, gesenkt und Kosten mehr Dienste ausführen können.

Als Nebeneffekt des auf den gleichen Kernel ausgeführt wird erzielen Sie weniger Isolation als virtuelle Computer.

Der Hauptzweck eines Bilds ist, dass der Umgebung (Abhängigkeiten) die gleiche über verschiedene Bereitstellungen vereinfacht. Dies bedeutet, dass Sie auf Ihrem Computer debuggen und dann mit der gleichen Umgebung sichergestellt, dass auf einen anderen Computer bereitstellen können.

Ein Container-Abbild ist eine Möglichkeit zum Verpacken einer Anwendung oder einem Dienst und zuverlässige und reproduzierbare Weise bereitstellen. In dieser Hinsicht Docker nicht nur eine Technologie, es ist auch eine Philosophie und einen Prozess.

Wenn Sie Docker verwenden zu können, Sie sagen Entwickler nicht hören, "Funktionsweise auf meinem Computer Warum nicht in der Produktion?" Sie können einfach nehmen "Docker Ausführung auf" daran, dass die verpackte Docker-Anwendung auf jeder unterstützten Docker-Umgebung ausgeführt werden kann, und führt es die Möglichkeit, die für alle Bereitstellungsziele (Dev, QA, staging, Produktion usw..), beabsichtigt war.

![](./media/image3.png)

Abbildung 1 bis 3: Vergleich der traditionellen VMs in Docker-Containern


>[!div class="step-by-step"]
[Vorherigen] (index.md) [weiter] (Docker-terminology.md)
