---
title: Typäquivalenz und eingebettete Interop-Typen
ms.date: 03/30/2017
ms.prod: .net-framework
ms.technology:
- dotnet-clr
ms.topic: article
helpviewer_keywords:
- type equivalence
- embedded interop types
- primary interop assemblies,not necessary in CLR version 4
- NoPIA
ms.assetid: 78892eba-2a58-4165-b4b1-0250ee2f41dc
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 03b906c71b1b3e8f4817697edb520f8cfef1e009
ms.sourcegitcommit: c883637b41ee028786edceece4fa872939d2e64c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2018
---
# <a name="type-equivalence-and-embedded-interop-types"></a>Typäquivalenz und eingebettete Interop-Typen

Beginnend mit der [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], unterstützt die Common Language Runtime die Einbettung von Typinformationen für COM-Typen direkt in verwaltete Assemblys. Die verwalteten Assemblys müssen die Typinformationen für COM-Typen nicht aus Interop-Assemblys abrufen. Da die eingebettete Typinformation nur die Typen und Member enthält, die tatsächlich von einer verwalteten Assembly verwendet werden, können zwei verwaltete Assemblys möglicherweise sehr unterschiedliche Ansichten desselben COM-Typs haben. Jede verwaltete Assembly besitzt ein anderes <xref:System.Type>-Objekt, das eine Ansicht des COM-Typs darstellt. Die Common Language Runtime unterstützt Typäquivalenz zwischen diesen unterschiedlichen Ansichten für Schnittstellen, Strukturen, Enumerationen und Delegaten.

Typäquivalenz bedeutet, dass ein COM-Objekt, das von einer verwalteten Assembly an eine andere übergeben wird, für den entsprechenden verwalteten Typ in der empfangenden Assembly bereitgestellt werden kann.

> [!NOTE]
> Typäquivalenz und eingebettete Interop-Typen vereinfachen die Bereitstellung von Anwendungen und Add-Ins, die COM-Komponenten verwenden, da Interop-Assemblys nicht mit den Anwendungen bereitgestellt werden müssen. Entwickler von freigegebenen COM-Komponenten müssen noch primäre Interop-Assemblys (PIAs) erstellen, wenn ihre Komponenten von früheren Versionen von .NET Framework verwendet werden sollen.

## <a name="type-equivalence"></a>Typäquivalenz

 Die Äquivalenz von COM-Typen wird für Schnittstellen, Strukturen, Enumerationen und Delegaten unterstützt. COM-Typen gelten als äquivalent, wenn alle folgenden Bedingungen erfüllt sind:

- Beide Typen sind sowohl Schnittstellen, Strukturen, Enumerationen oder Delegaten.

- Beide Typen haben die gleiche Identität, wie im nächsten Abschnitt beschrieben wird.

- Beide Typen sind für Typäquivalenz, wie beschrieben in der [Markieren von COM-Typen für Typäquivalenz](#marking-com-types-for-type-equivalence) Abschnitt.

### <a name="type-identity"></a>Typidentität

Zwei Typen werden die gleiche Identität haben, wenn ihre Bereiche und Identitäten übereinstimmen, das heißt, wenn sie beide über das <xref:System.Runtime.InteropServices.TypeIdentifierAttribute>-Attribut verfügen, und die zwei Attribute übereinstimmende <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Scope%2A>- und <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Identifier%2A>-Eigenschaften aufweisen. Beim Vergleich für <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Scope%2A> wird die Groß- und Kleinschreibung nicht berücksichtigt.

Wenn ein Typ nicht über das <xref:System.Runtime.InteropServices.TypeIdentifierAttribute>-Attribut, oder über ein <xref:System.Runtime.InteropServices.TypeIdentifierAttribute>-Attribut verfügt, das Bereich und Bezeichner nicht angibt, kann der Typ folgendermaßen weiterhin für die Äquivalenz in Betracht gezogen werden:

- Für Schnittstellen wird der Wert von <xref:System.Runtime.InteropServices.GuidAttribute> anstelle der <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Scope%2A?displayProperty=nameWithType>-Eigenschaft verwendet, und die <xref:System.Type.FullName%2A?displayProperty=nameWithType>-Eigenschaft (d.h. Typnamen einschließlich Namespace) wird anstelle der <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Identifier%2A?displayProperty=nameWithType>-Eigenschaft verwendet.

- Bei Strukturen, Enumerationen und Delegaten wird die <xref:System.Runtime.InteropServices.GuidAttribute> der enthaltenden Assembly anstelle der <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Scope%2A>-Eigenschaft, und die <xref:System.Type.FullName%2A?displayProperty=nameWithType>-Eigenschaft anstelle der <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Identifier%2A>-Eigenschaft verwendet.

### <a name="marking-com-types-for-type-equivalence"></a>Markieren von COM-Typen für Typäquivalenz

 Sie können einen Typ auf zwei Arten für Typäquivalenz verfügbar kennzeichnen:

- Fügen Sie das <xref:System.Runtime.InteropServices.TypeIdentifierAttribute>-Attribut zum Typ hinzu.

- Machen Sie den Typ zu einem COM-Importtyp. Eine Schnittstelle ist eine COM-Importtyp, wenn es über das <xref:System.Runtime.InteropServices.ComImportAttribute>-Attribut verfügt. Eine Schnittstelle, Struktur, Enumeration oder ein Delegat ist ein COM-Importtyp, wenn die Assembly, in der sie definiert ist, über das <xref:System.Runtime.InteropServices.ImportedFromTypeLibAttribute>-Attribut verfügt.

## <a name="see-also"></a>Siehe auch

<xref:System.Type.IsEquivalentTo%2A>  
[Verwenden von COM-Typen in verwaltetem Code](http://msdn.microsoft.com/library/1a95a8ca-c8b8-4464-90b0-5ee1a1135b66(v=vs.100))  
[Importing a Type Library as an Assembly (Importieren einer Typbibliothek als Assembly)](importing-a-type-library-as-an-assembly.md)  
