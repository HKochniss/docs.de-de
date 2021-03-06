---
title: "Gewusst wie: Ändern der Rahmen von Windows Forms"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Windows Forms, changing the borders
ms.assetid: b3d5fa56-80c6-4b10-b505-f9672307ed55
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: e977617f16ef882ad0dcfe1a96a6e8af73d2ae48
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-change-the-borders-of-windows-forms"></a>Gewusst wie: Ändern der Rahmen von Windows Forms
Sie können aus mehreren Rahmenformatvorlagen auswählen, wenn Sie das Aussehen und Verhalten Ihres Windows Forms-Elements festlegen möchten. Durch Ändern der <xref:System.Windows.Forms.Form.FormBorderStyle%2A>-Eigenschaft können Sie das Verhalten des Formulars bei das Größenanpassung steuern. Zudem wirkt sich das Festlegen von <xref:System.Windows.Forms.Form.FormBorderStyle%2A> darauf aus, wie die Titelleiste angezeigt wird und mit welchen Schaltflächen. Weitere Informationen finden Sie unter <xref:System.Windows.Forms.FormBorderStyle>.  
  
 In [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] wird diese Aufgabe umfassend unterstützt.  
  
 Siehe auch [Vorgehensweise: Ändern der Rahmen von Windows Forms mithilfe des Designers](http://msdn.microsoft.com/library/yettzh3e\(v=vs.110\)).  
  
### <a name="to-set-the-border-style-of-windows-forms-programmatically"></a>So legen Sie die Rahmenart von Windows Forms programmgesteuert fest  
  
-   Legen Sie die Eigenschaft <xref:System.Windows.Forms.Form.FormBorderStyle%2A> auf die gewünschte Rahmenart fest. Im folgenden Codebeispiel wird die Rahmenart des Formulars `DlgBx1` auf <xref:System.Windows.Forms.FormBorderStyle.FixedDialog>.  
  
    ```vb  
    DlgBx1.FormBorderStyle = System.Windows.Forms.FormBorderStyle.FixedDialog  
    ```  
  
    ```csharp  
    DlgBx1.FormBorderStyle = System.Windows.Forms.FormBorderStyle.FixedDialog;  
    ```  
  
    ```cpp  
    DlgBx1->FormBorderStyle =  
       System::Windows::Forms::FormBorderStyle::FixedDialog;  
    ```  
  
     Siehe auch [Vorgehensweise: Erstellen von Dialogfeldern zur Entwurfszeit](http://msdn.microsoft.com/library/55cz5x2c\(v=vs.110\)).  
  
     Darüber hinaus, wenn Sie eine Rahmenart für das Formular ausgewählt haben, die optionale Schaltflächen **Minimieren** und **Maximieren** Schaltflächen, können Sie angeben, ob eine oder beide Schaltflächen funktionsfähig sein sollen. Diese Schaltflächen sind hilfreich, wenn Sie die Benutzeroberfläche genau steuern möchten. Die **Minimieren** und **Maximieren** Schaltflächen sind standardmäßig aktiviert, und ihre Funktionalität wird über bearbeitet die **Eigenschaften** Fenster.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Windows.Forms.FormBorderStyle>  
 <xref:System.Windows.Forms.FormBorderStyle.FixedDialog>  
 [Erste Schritte mit Windows Forms](../../../docs/framework/winforms/getting-started-with-windows-forms.md)
