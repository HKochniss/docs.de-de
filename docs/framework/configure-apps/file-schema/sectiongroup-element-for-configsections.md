---
title: "&lt;SectionGroup&gt; -Element für &lt;\"configSections\"&gt;"
ms.date: 05/01/2017
ms.prod: .net-framework
ms.technology:
- dotnet-clr
ms.topic: article
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/configSections/sectionGroup
helpviewer_keywords:
- sectionGroup Element
- <sectionGroup> Element
ms.assetid: 6c27f9e2-809c-4bc9-aca9-72f90360e7a3
author: guardrex
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 654a6e639a24120e1e0c993ebe36f14e75b46a12
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="sectiongroup-element-for-configsections"></a>\<SectionGroup >-Element für \<ConfigSections >

Definiert einen Namespace für Konfigurationsabschnitte.

[**\<configuration>**](~/docs/framework/configure-apps/file-schema/configuration-element.md)   
&nbsp;&nbsp;[**\<ConfigSections >**](~/docs/framework/configure-apps/file-schema/configsections-element-for-configuration.md)   
&nbsp;&nbsp;&nbsp;&nbsp;**\<SectionGroup >**

## <a name="syntax"></a>Syntax

```xml
<sectionGroup name="section group name">
  <!-- Configuration sections -->
</sectionGroup>
```

## <a name="attribute"></a>Attribut

|           | Beschreibung |
| --------- | ----------- |
| **name**  | Erforderliches Attribut.<br><br>Gibt den Namen der Abschnittsgruppe, die Sie definieren. |

## <a name="parent-element"></a>Übergeordnetes Element

|     | Beschreibung |
| --- | ----------- |
| [**\<ConfigSections >** Element](~/docs/framework/configure-apps/file-schema/configsections-element-for-configuration.md) | Enthält die Konfiguration im Abschnitt und Namespacedeklarationen. |

## <a name="child-elements"></a>Untergeordnete Elemente

|     | Beschreibung |
| --- | ----------- |
| [**\<Abschnitt >**](~/docs/framework/configure-apps/file-schema/section-element.md) | Enthält eine Deklaration der Konfiguration im Abschnitt. |

## <a name="remarks"></a>Hinweise

Deklarieren eine Abschnittsgruppe erstellt ein Containertag für Konfigurationsabschnitte und stellt sicher, dass keine Namenskonflikte mit Konfigurationsabschnitte, die von einer anderen Person definiert. Sie können schachteln  **\<SectionGroup >** Elemente in einem anderen.

## <a name="example"></a>Beispiel

Das folgende Beispiel zeigt, wie zum Deklarieren einer Abschnittsgruppe und Abschnitte innerhalb einer Abschnittsgruppe deklarieren:

```xml
<configuration>
  <configSections>
    <sectionGroup name="mySectionGroup">
      <section name="mySection"
               type="System.Configuration.NameValueSectionHandler,System" />
    </sectionGroup>
  </configSections>
  <mySectionGroup>
    <mySection>
      <add key="key1" value="value1" />
    </mySection>
  </mySectionGroup>
</configuration>
```

## <a name="configuration-file"></a>Konfigurationsdatei

Dieses Element kann in der Anwendungskonfigurationsdatei Computerkonfigurationsdatei verwendet werden (*"Machine.config"*), und *"Web.config"* Dateien, die nicht auf Anwendungsebene Verzeichnis sind.

## <a name="see-also"></a>Siehe auch

[Konfigurationsdateischema für .NET Framework](~/docs/framework/configure-apps/file-schema/index.md)
