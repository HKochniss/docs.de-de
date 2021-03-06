---
title: Handles-Klausel (Visual Basic)
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- Handles
- vb.Handles
helpviewer_keywords:
- Handles keyword [Visual Basic]
ms.assetid: 1b051c0e-f499-42f6-acb5-6f4f27824b40
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: a23b3d96052ad179ea25150bb570461a9e764977
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="handles-clause-visual-basic"></a>Handles-Klausel (Visual Basic)
Deklariert, dass eine Prozedur ein angegebenes Ereignis behandelt.  
  
## <a name="syntax"></a>Syntax  
  
```  
proceduredeclaration Handles eventlist  
```  
  
## <a name="parts"></a>Teile  
 `proceduredeclaration`  
 Die `Sub`-Prozedurdeklaration für die Prozedur, die das Ereignis verarbeitet.  
  
 `eventlist`  
 Listet die Ereignisse für `proceduredeclaration` für die Verarbeitung auf, durch Kommas getrennt. Die Ereignisse müssen durch die Basisklasse für die aktuelle Klasse oder durch ein mithilfe des Schlüsselworts `WithEvents` deklariertes Objekt ausgelöst werden.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie das `Handles` -Schlüsselwort am Ende der Prozedurdeklaration, damit sie Ereignisse verarbeitet, die durch eine mithilfe des Schlüsselworts `WithEvents` deklarierte Objektvariable ausgelöst wurden. Das Schlüsselwort `Handles` kann zudem in einer abgeleiteten Klasse verwendet werden, um Ereignisse aus einer Basisklasse zu verarbeiten.  
  
 Mit dem Schlüsselwort `Handles` und der Anweisung `AddHandler` können Sie angeben, dass diese bestimmten Prozeduren bestimmte Ereignisse verarbeiten. Es bestehen jedoch keine Unterschiede. Verwenden Sie das Schlüsselwort `Handles`, wenn Sie eine Prozedur definieren, um anzugeben, dass sie ein bestimmtes Ereignis verarbeitet.  Die Anweisung `AddHandler` verbindet Prozeduren zur Laufzeit mit Ereignissen. Weitere Informationen finden Sie unter [AddHandler-Anweisung](../../../visual-basic/language-reference/statements/addhandler-statement.md).  
  
 Für benutzerdefinierte Ereignisse ruft die Anwendung den `AddHandler`-Accessor des Ereignisses auf, wenn die Prozedur als ein Ereignishandler hinzugefügt wird. Weitere Informationen zu benutzerdefinierten Ereignissen finden Sie unter [Event-Anweisung](../../../visual-basic/language-reference/statements/event-statement.md).  
  
## <a name="example"></a>Beispiel  
 [!code-vb[VbVbalrEvents#2](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/handles-clause_1.vb)]  
  
 Im folgenden Beispiel wird gezeigt, wie eine abgeleitete Klasse die `Handles`-Anweisung zum Verarbeiten eines Ereignisses aus einer Basisklasse verwenden kann.  
  
 [!code-vb[VbVbalrEvents#3](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/handles-clause_2.vb)]  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel enthält zwei Tastenereignishandler für ein **WPF-Anwendung** Projekt.  
  
 [!code-vb[VbVbalrEvents#41](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/handles-clause_3.vb)]  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel entspricht dem vorherigen Beispiel. Die `eventlist` in der `Handles`-Klausel enthält die Ereignisse für beide Tasten.  
  
 [!code-vb[VbVbalrEvents#42](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/handles-clause_4.vb)]  
  
## <a name="see-also"></a>Siehe auch  
 [WithEvents](../../../visual-basic/language-reference/modifiers/withevents.md)  
 [AddHandler-Anweisung](../../../visual-basic/language-reference/statements/addhandler-statement.md)  
 [RemoveHandler-Anweisung](../../../visual-basic/language-reference/statements/removehandler-statement.md)  
 [Event-Anweisung](../../../visual-basic/language-reference/statements/event-statement.md)  
 [RaiseEvent-Anweisung](../../../visual-basic/language-reference/statements/raiseevent-statement.md)  
 [Ereignisse](../../../visual-basic/programming-guide/language-features/events/index.md)
