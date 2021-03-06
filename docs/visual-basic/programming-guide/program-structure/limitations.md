---
title: "Beschränkungen in Visual Basic"
ms.custom: 
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- limits
- limitations [Visual Basic]
- limitations
- limits, Visual Basic code
- Visual Basic code, limitations
ms.assetid: cf1646b7-5d24-48c6-9616-bda8a4849d91
caps.latest.revision: "14"
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 97a2e162b9f1a673fbe805a5d2ef1421cd423a4f
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="visual-basic-limitations"></a>Beschränkungen in Visual Basic
Frühere Versionen von [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] erzwungen Grenzen in Code, z. B. die Länge der Variablennamen, die Anzahl der Variablen in Modulen und Modulgröße zulässig. In Visual Basic .NET und wurden diese Einschränkungen gelockert wurde und Sie haben mehr Freiheit beim Schreiben und Einfügen von Code.  
  
 Physische Grenzen sind mehr auf die Laufzeit Arbeitsspeicher als Zeitpunkt der Kompilierung Leistungsaspekten abhängig. Wenn umsichtige Programmierstil hin, und Sie große Anwendungen in mehrere Klassen und Module unterteilen, dann ist es sehr geringer Wahrscheinlichkeit eine interne [!INCLUDE[vbprvb](~/includes/vbprvb-md.md)] Einschränkung.  
  
 Es folgen einige Einschränkungen, die Sie in extremen Fällen auftreten:  
  
-   **Länge des Namens.** Es wird eine maximale Anzahl von Zeichen für den Namen jedes deklarierten Programmierelements. Dieser Maximalwert gilt für eine gesamte Qualifizierungspfad auf, wenn der Elementname qualifiziert wird. Finden Sie unter [deklarierte Elementnamen](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
-   **Zeilenlänge.** Es gibt ein Maximum von 65535 Zeichen in eine physische Zeile des Quellcodes. Die logische Quellcodezeile kann mehr Zeit, wenn Sie das Zeilenfortsetzungszeichen verwenden. Finden Sie unter [wie: umbrechen und Zusammenfassen von Anweisungen in Code](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md).  
  
-   **Dimensionen des Arrays.** Es wird eine maximale Anzahl von Dimensionen, die Sie für ein Array zu deklarieren. Dies schränkt wie viele Indizes, die Sie verwenden können, um ein Arrayelement anzugeben. Finden Sie unter [Dimensionen in Visual Basic-Array](../../../visual-basic/programming-guide/language-features/arrays/array-dimensions.md).  
  
-   **Länge der Zeichenfolge.** Es wird eine maximale Anzahl von Unicode-Zeichen, die in einer einzelnen Zeichenfolge gespeichert werden können. Finden Sie unter [Zeichenfolgendatentyp](../../../visual-basic/language-reference/data-types/string-data-type.md).  
  
-   **Umgebung String-length-Funktion.** Es ist ein Maximum von 32768 Zeichen für eine beliebige Umgebungszeichenfolge als Befehlszeilenargument verwendet. Dies ist eine Einschränkung auf allen Plattformen.  
  
## <a name="see-also"></a>Siehe auch  
 [Programmstruktur und Codekonventionen](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)  
 [Visual Basic-Benennungskonventionen](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)
