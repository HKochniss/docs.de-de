---
title: "Zuordnen von XML Schema (XSD)-Schlüsseleinschränkungen zu DataSet-Einschränkungen"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3d0d1a4b-9104-434f-ac04-6c01ab5716b5
caps.latest.revision: "4"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: f403dc974e4fe67d239688f587061cd23a8deff6
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="mapping-xml-schema-xsd-constraints-to-dataset-constraints"></a>Zuordnen von XML Schema (XSD)-Schlüsseleinschränkungen zu DataSet-Einschränkungen
Die XSD-Sprache (XML Schema Definition Language) ermöglicht Einschränkungen, die Sie für die Elemente und Attribute angeben können, die durch XSD definiert werden. Beim Zuordnen eines XML-Schemas zum relationalen Schema in einer <xref:System.Data.DataSet>, XML-schemaeinschränkungen zugeordnet sind, auf den entsprechenden relationalen Einschränkungen in den Tabellen und Spalten innerhalb der **DataSet**.  
  
 In diesem Abschnitt wird die Zuordnung der folgenden XML-Schemaeinschränkungen behandelt:  
  
-   Die Unique-Einschränkung angegeben wird, mit der **eindeutige** Element.  
  
-   Die Key-Einschränkung angegeben wird, mit der **Schlüssel** Element.  
  
-   Die Keyref-Einschränkung angegeben wird, mit der **Keyref** Element.  
  
 Mit einer Einschränkung für ein Element oder Attribut geben Sie bestimmte Beschränkungen für den Wert des Elements in einer beliebigen Instanz des Dokuments an. Z. B. eine schlüsseleinschränkung für ein **CustomerID** untergeordnetes Element von einer **Kunden** -Element im Schema gibt an, dass die Werte der der **CustomerID** untergeordnete Element muss sein in jeder Dokumentinstanz eindeutig und null-Werte nicht zulässig sind.  
  
 Einschränkungen können auch zwischen Elementen und Attributen in einem Dokument angegeben werden, um eine Beziehung innerhalb des Dokuments zu erstellen. Die key-Einschränkung und die keyref-Einschränkung werden im Schema verwendet, um Einschränkungen innerhalb des Dokuments anzugeben, die zu einer Beziehung zwischen Dokumentelementen und Attributen führen.  
  
 Der Zuordnungsprozess konvertiert diese schemaeinschränkungen in die entsprechenden Einschränkungen für die Tabellen erstellt, die innerhalb der **DataSet**.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Zuordnen von eindeutigen XML Schema-Einschränkungen (XSD)zu DataSet-Einschränkungen](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/map-unique-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 Beschreibt die XML-Schema-Elemente, die zum Erstellen von unique-Einschränkungen in einer **DataSet**.  
  
 [Zuordnen von XML Schema-Schlüsseleinschränkungen (XSD) zu DataSet-Einschränkungen](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/map-key-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 Beschreibt die XML-Schema-Elemente, die zum Erstellen der Key-Einschränkungen (unique-Einschränkungen, in denen null-Werte sind nicht zulässig) in einem **DataSet**.  
  
 [Zuordnen von keyref-XML Schema-Einschränkungen (XSD) zu DataSet-Einschränkungen](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/map-keyref-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 Beschreibt die XML-Schema-Elemente, die zum Erstellen von Keyref-Einschränkungen (Fremdschlüssel) in einem **DataSet**.  
  
## <a name="related-sections"></a>Verwandte Abschnitte  
 [Ableiten einer relationalen DataSet-Struktur aus einem XML-Schema (XSD)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 Beschreibt die relationale Struktur bzw. das Schema von einem **DataSet** , aus der XSD-Schema erstellt wird.  
  
 [Generieren von DataSet-Beziehungen aus einem XML-Schema (XSD)](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)  
 Beschreibt die XML-Schema-Elemente, die zum Erstellen von Beziehungen zwischen Tabellenspalten in einer **DataSet**.  
  
## <a name="see-also"></a>Siehe auch  
 [ADO.NET Managed Provider und DataSet Developer Center](http://go.microsoft.com/fwlink/?LinkId=217917)
