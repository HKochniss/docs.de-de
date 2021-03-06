---
title: "Gewusst wie: Verfügbarmachen der Eigenschaften konstituierender Steuerelemente"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- user controls [Windows Forms], exposing constituent controls
- controls [Windows Forms], constituent
- custom controls [Windows Forms], exposing properties
- constituent controls
ms.assetid: 5c1ec98b-aa48-4823-986e-4712551cfdf1
caps.latest.revision: "13"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: a970864a406f98477fa3e09bdefcf959d2078fe6
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-expose-properties-of-constituent-controls"></a>Gewusst wie: Verfügbarmachen der Eigenschaften konstituierender Steuerelemente
Die Steuerelemente, die ein zusammengesetztes Steuerelement bilden heißen *konstituierende Steuerelemente*. Diese Steuerelemente werden normalerweise als privat deklariert und kann daher nicht von der Entwickler zugegriffen werden. Wenn Sie die Eigenschaften dieser Steuerelemente zukünftigen Benutzern zur Verfügung stellen möchten, müssen Sie für den Benutzer verfügbar machen. Eine Eigenschaft eines konstituierenden Steuerelements wird verfügbar gemacht, durch eine Eigenschaft im Benutzersteuerelement erstellen und Verwenden der `get` und `set` Accessoren der Eigenschaft, um die Auswirkungen auf der Änderung in der privaten Eigenschaft des konstituierenden Steuerelements.  
  
 Betrachten Sie ein hypothetisches Benutzersteuerelement mit einer konstituierenden Schaltfläche mit dem Namen `MyButton`. In diesem Beispiel, wenn der Benutzer fordert die `ConstituentButtonBackColor` -Eigenschaft, die in gespeicherten Wert der <xref:System.Windows.Forms.Control.BackColor%2A> Eigenschaft `MyButton` übermittelt wird. Wenn der Benutzer diese Eigenschaft einen Wert zuweist, wird dieser Wert automatisch zum Übergeben der <xref:System.Windows.Forms.Control.BackColor%2A> Eigenschaft des `MyButton` und die `set` Code wird ausgeführt, ändern die Farbe des `MyButton`.  
  
 Im folgende Beispiel wird gezeigt, wie verfügbar machen die <xref:System.Windows.Forms.Control.BackColor%2A> Eigenschaft der konstituierenden Schaltfläche:  
  
```vb  
Public Property ButtonColor() as System.Drawing.Color  
   Get  
      Return MyButton.BackColor  
   End Get  
   Set(Value as System.Drawing.Color)  
      MyButton.BackColor = Value  
   End Set  
End Property  
```  
  
```csharp  
public Color ButtonColor  
{  
   get  
   {  
      return(myButton.BackColor);  
   }  
   set  
   {  
      myButton.BackColor = value;  
   }  
}  
```  
  
### <a name="to-expose-a-property-of-a-constituent-control"></a>Eine Eigenschaft eines konstituierenden Steuerelements verfügbar machen.  
  
1.  Erstellen Sie eine öffentliche Eigenschaft für das Benutzersteuerelement.  
  
2.  In der `get` Abschnitt der Eigenschaft, Schreiben Sie Code, der den Wert der Eigenschaft abruft, Sie verfügbar machen möchten.  
  
3.  In der `set` Abschnitt der Eigenschaft, Schreiben Sie Code, der den Wert der Eigenschaft an die verfügbar gemachte Eigenschaft des konstituierenden Steuerelements übergibt.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Windows.Forms.UserControl>  
 [Eigenschaften in Windows Forms-Steuerelementen](../../../../docs/framework/winforms/controls/properties-in-windows-forms-controls.md)  
 [Varieties of Custom Controls (Vielfalt benutzerdefinierter Steuerelemente)](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)
