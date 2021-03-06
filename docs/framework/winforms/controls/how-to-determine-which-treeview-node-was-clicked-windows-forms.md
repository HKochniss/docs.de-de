---
title: "Gewusst wie: Ermitteln des per Mausklick ausgewählten TreeView-Knotens (Windows Forms)"
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
f1_keywords:
- TreeNode
helpviewer_keywords:
- examples [Windows Forms], TreeView control
- tree nodes in TreeView control [Windows Forms], determining node clicked
- TreeView control [Windows Forms], determining node clicked
ms.assetid: 06a4a191-d918-42af-9f49-956c93eff261
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 2671d2790b3c5e476513cd5932d4684838aeceb6
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-determine-which-treeview-node-was-clicked-windows-forms"></a>Gewusst wie: Ermitteln des per Mausklick ausgewählten TreeView-Knotens (Windows Forms)
Bei der Arbeit mit Windows Forms <xref:System.Windows.Forms.TreeView> -Steuerelement, eine häufige Aufgabe besteht darin zu bestimmen, welcher Knoten geklickt wurde, und entsprechend reagieren.  
  
### <a name="to-determine-which-treeview-node-was-clicked"></a>Zum Ermitteln des per Mausklick ausgewählten TreeView-Knotens  
  
1.  Verwenden der <xref:System.EventArgs> Objekts, das einen Verweis auf die geklickt wurde Knotenobjekt zurückgegeben.  
  
2.  Bestimmen, welchen Knoten geklickt wurde, indem Sie überprüfen die <xref:System.Windows.Forms.TreeViewEventArgs> -Klasse, die Daten im Zusammenhang mit der das Ereignis enthält.  
  
    ```vb  
    Private Sub TreeView1_AfterSelect(ByVal sender As System.Object, _  
    ByVal e As System.Windows.Forms.TreeViewEventArgs) Handles TreeView1.AfterSelect  
       ' Determine by checking the Node property of the TreeViewEventArgs.  
       MessageBox.Show(e.Node.Text)  
    End Sub  
    ```  
  
    ```csharp  
    protected void treeView1_AfterSelect (object sender,   
    System.Windows.Forms.TreeViewEventArgs e)  
    {  
       // Determine by checking the Text property.  
       MessageBox.Show(e.Node.Text);  
    }  
    ```  
  
    ```cpp  
    private:  
       void treeView1_AfterSelect(System::Object ^  sender,  
          System::Windows::Forms::TreeViewEventArgs ^  e)  
       {  
          // Determine by checking the Text property.  
          MessageBox::Show(e->Node->Text);  
       }  
    ```  
  
    > [!NOTE]
    >  Als Alternative können Sie die <xref:System.Windows.Forms.MouseEventArgs> von der <xref:System.Windows.Forms.Control.MouseDown> oder <xref:System.Windows.Forms.Control.MouseUp> abzurufenden Ereignisses die <xref:System.Drawing.Point.X%2A> und <xref:System.Drawing.Point.Y%2A> -Koordinatenwerte von der <xref:System.Drawing.Point> , wo der Klick aufgetreten ist. Verwenden Sie dann die <xref:System.Windows.Forms.TreeView> des Steuerelements <xref:System.Windows.Forms.TreeView.GetNodeAt%2A> Methode, um zu bestimmen, welchen Knoten geklickt wurde.  
  
## <a name="see-also"></a>Siehe auch  
 [TreeView-Steuerelement](../../../../docs/framework/winforms/controls/treeview-control-windows-forms.md)
