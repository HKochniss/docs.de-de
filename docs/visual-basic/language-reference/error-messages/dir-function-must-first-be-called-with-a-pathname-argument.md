---
title: '&#39; Dir &#39; Funktion muss zuerst aufgerufen werden, mit einer &#39; PathName &#39; Argument'
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrDIR_IllegalCall
ms.assetid: 7b5d149f-be91-4ac3-8262-86a360894e7d
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 843918fe9cb0b9dece076b5dc1373c3571588caa
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/18/2017
---
# <a name="39dir39-function-must-first-be-called-with-a-39pathname39-argument"></a>&#39; Dir &#39; Funktion muss zuerst aufgerufen werden, mit einer &#39; PathName &#39; Argument
Einem ersten Aufruf der `Dir` Funktion schließt nicht die `PathName` Argument. Der erste Aufruf von `Dir` umfasst eine `PathName`, aber nachfolgende Aufrufe `Dir` müssen nicht enthalten Parameter, um das nächste Element abzurufen.  
  
## <a name="to-correct-this-error"></a>So beheben Sie diesen Fehler  
  
1.  Geben Sie einen `PathName` Argument im Funktionsaufruf.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.VisualBasic.FileSystem.Dir%2A>
