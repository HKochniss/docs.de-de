---
title: "Übersicht über das DomainUpDown-Steuerelement (Windows Forms)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- DomainUpDown
helpviewer_keywords:
- spin button control [Windows Forms], about spin button
- DomainUpDown control [Windows Forms], about DomainUpDown control
ms.assetid: 3f40f9c1-20ad-4331-b9b5-b0127eb36eb3
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: e5a86dc6c56c3afff8d8a3a4ca2c5d5efa8eac1a
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="domainupdown-control-overview-windows-forms"></a>Übersicht über das DomainUpDown-Steuerelement (Windows Forms)
Windows Forms <xref:System.Windows.Forms.DomainUpDown> -Steuerelement ist im Wesentlichen eine Kombination aus einem Textfeld und einem Paar von Schaltflächen für das Durchsuchen einer Liste nach oben oder unten. Das Steuerelement zeigt an, und legt eine Zeichenfolge aus einer Liste von Optionen. Der Benutzer kann die Zeichenfolge auswählen, indem Sie auf nach oben oder unten Schaltflächen, um eine Liste durchlaufen, durch Drücken der nach-oben und nach unten-Taste oder durch Eingabe eine Zeichenfolge, die ein Element in der Liste entspricht. Eine Verwendungsmöglichkeit für dieses Steuerelement ist für das Auswählen von Elementen aus einer alphabetisch sortierte Liste der Namen.  
  
> [!NOTE]
>  Um die Liste zu sortieren, legen die <xref:System.Windows.Forms.DomainUpDown.Sorted%2A> Eigenschaft `true`.  
  
 Die Funktion dieses Steuerelements wird im Listenfeld oder Kombinationsfeld sehr ähnlich, aber es nur sehr wenig Speicherplatz beanspruchen.  
  
## <a name="key-properties"></a>Wichtige Eigenschaften  
 Die wichtigsten Eigenschaften des Steuerelements sind <xref:System.Windows.Forms.DomainUpDown.Items%2A>, <xref:System.Windows.Forms.UpDownBase.ReadOnly%2A>, und <xref:System.Windows.Forms.DomainUpDown.Wrap%2A>. Die <xref:System.Windows.Forms.DomainUpDown.Items%2A> Eigenschaft enthält die Liste der Objekte, deren Text im Steuerelement angezeigt werden. Wenn <xref:System.Windows.Forms.UpDownBase.ReadOnly%2A> festgelegt ist, um `false`, das Steuerelement automatisch abgeschlossen wird, Text, dass der Benutzer eingibt, und es mit einem Wert in der Liste vergleicht. Wenn <xref:System.Windows.Forms.DomainUpDown.Wrap%2A> festgelegt ist, um `true`, Durchführen eines Bildlaufs hinter dem letzten Element gelangen Sie auf das erste Element in der Liste und umgekehrt. Die wichtigsten Methoden des Steuerelements sind <xref:System.Windows.Forms.DomainUpDown.UpButton%2A> und <xref:System.Windows.Forms.DomainUpDown.DownButton%2A>.  
  
 Dieses Steuerelement zeigt nur Textzeichenfolgen. Wenn Sie ein Steuerelement möchten, in dem numerische Werte angezeigt, verwenden die <xref:System.Windows.Forms.NumericUpDown> Steuerelement. Weitere Informationen finden Sie unter [Übersicht über das NumericUpDown-Steuerelement](../../../../docs/framework/winforms/controls/numericupdown-control-overview-windows-forms.md).  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Windows.Forms.DomainUpDown>  
 [DomainUpDown-Steuerelement](../../../../docs/framework/winforms/controls/domainupdown-control-windows-forms.md)
