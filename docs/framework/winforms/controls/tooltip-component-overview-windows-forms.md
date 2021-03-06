---
title: "Übersicht über die ToolTip-Komponente (Windows Forms)"
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
- ToolTip
helpviewer_keywords:
- tooltips [Windows Forms], about tooltips
- ToolTip component [Windows Forms], about ToolTip component
ms.assetid: 3fbc6f08-c882-4acd-a960-a08efe3c7e6e
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: fce1cb5750197e52461b4883f1238325fa10fc5e
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2017
---
# <a name="tooltip-component-overview-windows-forms"></a>Übersicht über die ToolTip-Komponente (Windows Forms)
Die <xref:System.Windows.Forms.ToolTip>-Komponente in Windows Forms zeigt Text an, wenn der Benutzer auf Steuerelemente zeigt. Jedem Steuerelement kann eine QuickInfo zugeordnet werden. Ein Beispiel für die Verwendung dieser Komponente: um Speicherplatz auf einem Formular zu speichern, können Sie ein kleines Symbol auf einer Schaltfläche anzeigen und verwenden Sie eine QuickInfo, um die Funktion der Schaltfläche zu erklären.  
  
## <a name="working-with-the-tooltip-component"></a>Arbeiten mit der ToolTip-Komponente  
 Ein <xref:System.Windows.Forms.ToolTip> Komponente bietet eine `ToolTip` -Eigenschaft für mehrere Steuerelemente auf einem Windows Form oder einem anderen Container. Angenommen, wenn Sie eine ablegen <xref:System.Windows.Forms.ToolTip> Komponente auf einem Formular anzeigen "Geben Sie hier Ihren Namen" für eine <xref:System.Windows.Forms.TextBox> steuern und "Klicken Sie hier, um Änderungen zu speichern" für eine <xref:System.Windows.Forms.Button> Steuerelement.  
  
 Folgende Schlüsselmethoden der <xref:System.Windows.Forms.ToolTip> Komponente <xref:System.Windows.Forms.ToolTip.SetToolTip%2A> und <xref:System.Windows.Forms.ToolTip.GetToolTip%2A>. Sie können die <xref:System.Windows.Forms.ToolTip.SetToolTip%2A> -Methode zum Festlegen von QuickInfos für Steuerelemente angezeigt. Weitere Informationen finden Sie unter [Vorgehensweise: Festlegen von QuickInfos für Steuerelemente in einem Windows Form zur Entwurfszeit](../../../../docs/framework/winforms/controls/how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time.md). Die Schlüsseleigenschaften sind <xref:System.Windows.Forms.ToolTip.Active%2A>, dem muss festgelegt werden, um `true` für die QuickInfo angezeigt wird, und <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A>, wodurch die Zeitdauer, die die QuickInfo-Zeichenfolge angezeigt wird, wie lange die Benutzer auf das Steuerelement für die QuickInfo angezeigt wird, verweisen muss und wie er zu lang wird für nachfolgende QuickInfo-Fenster angezeigt werden. Weitere Informationen finden Sie unter [Vorgehensweise: Ändern der Verzögerung der ToolTip-Komponente in Windows Forms](../../../../docs/framework/winforms/controls/how-to-change-the-delay-of-the-windows-forms-tooltip-component.md).  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Windows.Forms.ToolTip>  
 [Gewusst wie: Festlegen von QuickInfos für Steuerelemente auf einem Windows Form zur Entwurfszeit](../../../../docs/framework/winforms/controls/how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time.md)  
 [Gewusst wie: Ändern der Verzögerung der ToolTip-Komponente in Windows Forms](../../../../docs/framework/winforms/controls/how-to-change-the-delay-of-the-windows-forms-tooltip-component.md)
