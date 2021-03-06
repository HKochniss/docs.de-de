---
title: My.Resources-Objekt
ms.date: 07/20/2015
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- My.Resources
- My.Resources.MyResources.ResourceManager
- My.Resources.MyResources.Culture
helpviewer_keywords:
- My.Resources object
ms.assetid: 34c3f2dc-7b87-432c-9d5f-17ea666bb266
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 96e5b909d9945ed631cebe07e4cfc7d5dc2e019f
ms.sourcegitcommit: 34ec7753acf76f90a0fa845235ef06663dc9e36e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="myresources-object"></a>My.Resources-Objekt
Stellt Klassen und Eigenschaften für den Zugriff auf die Ressourcen der Anwendung bereit.  
  
## <a name="remarks"></a>Hinweise  
 Die `My.Resources` Objekt ermöglicht den Zugriff auf die Ressourcen der Anwendung und das dynamische Abrufen von Ressourcen für Ihre Anwendung. Weitere Informationen finden Sie unter [verwalten Anwendung Ressourcen (.NET)](/visualstudio/ide/managing-application-resources-dotnet).  
  
 Die `My.Resources` Objekt macht nur globale Ressourcen verfügbar. Es stellt nicht den Zugriff auf Formularen zugeordnete Ressourcendateien bereit. Sie müssen die Formularressourcen aus dem Formular zugreifen.  
  
 Sie erreichen die Anwendung kulturspezifische Ressourcendateien aus den `My.Resources` Objekt. Wird standardmäßig die `My.Resources` -Objekt sucht nach Ressourcen aus der Ressourcendatei, in das der Kultur entspricht, der <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.UICulture%2A> Eigenschaft. Allerdings können Sie dieses Verhalten überschreiben und angeben eine bestimmte Kultur für die Ressourcen verwendet. Weitere Informationen finden Sie unter [Ressourcen in Desktop-Apps](../../../framework/resources/index.md).  
  
## <a name="properties"></a>Eigenschaften  
 Die Eigenschaften der `My.Resources` Objekt bereitstellen, nur-Lese-Zugriff auf Ressourcen der Anwendung. Verwenden Sie zum Hinzufügen oder Entfernen von Ressourcen, die **Projekt-Designer**. Sie Zugriff auf Ressourcen, die hinzugefügt wird, über die **Projekt-Designer** mit `My.Resources.``resourceName`.  
  
 Sie können auch hinzufügen oder entfernen Sie dazu das Projekt in Ressourcendateien **Projektmappen-Explorer** und auf **neues Element hinzufügen** oder **vorhandenes Element hinzufügen** aus der  **Projekt** Menü. Sie können auf diese Weise mit hinzugefügten Ressourcen zugreifen `My.Resources.``resourceFileName`.`resourceName`.  
  
 Jede Ressource weist ein Name, Kategorie und Wert und die ressourceneinstellungen für diese zu bestimmen, wie in der Eigenschaft, um Zugriff auf die Ressource angezeigt wird der `My.Resources` Objekt. Für Ressourcen, die hinzugefügt werden, der **Projekt-Designer**:  
  
-   Der Name Legt den Namen der Eigenschaft,  
  
-   Die Ressourcendaten ist der Wert der Eigenschaft,  
  
-   Die Kategorie bestimmt den Typ der Eigenschaft:  
  
|Kategorie|Datentyp der Eigenschaft|  
|---|---|  
|**Zeichenfolgen**|[String](../../../visual-basic/language-reference/data-types/string-data-type.md)|  
|**Bilder**|<xref:System.Drawing.Bitmap>|  
|**Symbole**|<xref:System.Drawing.Icon>|  
|**Audio**|<xref:System.IO.UnmanagedMemoryStream><br /><br /> Die <xref:System.IO.UnmanagedMemoryStream> Klasse leitet sich von der <xref:System.IO.Stream> Klasse, damit es Methoden angewendet werden kann, die Datenströme, z. B. Annehmen der <xref:Microsoft.VisualBasic.Devices.Audio.Play%2A> Methode.|  
|**Dateien**|-   [Zeichenfolge](../../../visual-basic/language-reference/data-types/string-data-type.md) für Textdateien.<br />-   <xref:System.Drawing.Bitmap>für Bilddateien.<br />-   <xref:System.Drawing.Icon>Symbol "-Dateien.<br />-   <xref:System.IO.UnmanagedMemoryStream>für Audiodateien.|  
|**Andere**|Bestimmt, indem die Informationen in des Designers **Typ** Spalte.|  
  
## <a name="classes"></a>Klassen  
 Die `My.Resources` Objekt jede Ressourcendatei als Klasse mit freigegebenen Eigenschaften verfügbar macht. Der Klassenname ist identisch mit den Namen der Ressourcendatei. Wie im vorherigen Abschnitt beschrieben wird, werden die Ressourcen in einer Ressourcendatei als Eigenschaften in der Klasse verfügbar gemacht.  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel wird der Titel eines Formulars auf die Zeichenfolgenressource mit dem Namen `Form1Title` in der Ressourcendatei für die Anwendung. Damit das Beispiel funktioniert, die Anwendung muss eine Zeichenfolge mit dem Namen haben `Form1Title` in der Ressourcendatei.  
  
 [!code-vb[VbVbalrMyResources#1](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-resources-object_1.vb)]  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel wird das Symbol des Formulars auf das Symbol mit dem Namen `Form1Icon` im Ressourcendatei für die Anwendung gespeichert wird. Für das Beispiel funktioniert, muss die Anwendung ein Symbol mit dem Namen verfügen `Form1Icon` in der Ressourcendatei.  
  
 [!code-vb[VbVbalrMyResources#2](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-resources-object_2.vb)]  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel wird das Hintergrundbild eines Formulars auf die imageressource mit dem Namen `Form1Background`, die in der Ressourcendatei für die Anwendung ist. Für dieses Beispiel funktioniert, muss die Anwendung eine Bildressource mit dem Namen haben `Form1Background` in der Ressourcendatei.  
  
 [!code-vb[VbVbalrMyResources#3](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-resources-object_3.vb)]  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel gibt den Sound, der als ein audio-Ressource mit dem Namen gespeichert wird `Form1Greeting` die Anwendung die Ressourcendatei enthält. Für das Beispiel funktioniert, muss die Anwendung eine audio-Ressource mit dem Namen verfügen `Form1Greeting` in der Ressourcendatei. Die `My.Computer.Audio.Play` Methode ist nur für Windows Forms-Anwendungen verfügbar.  
  
 [!code-vb[VbVbalrMyResources#4](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-resources-object_4.vb)]  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel ruft die Kultur Französisch-Version einer Zeichenfolge Ressource der Anwendung ab. Die Ressource wird mit dem Namen `Message`. So ändern Sie die Kultur, die die `My.Resources` Objekt verwendet wird, verwendet das Beispiel <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase.ChangeUICulture%2A>.  
  
 Für dieses Beispiel funktioniert, muss die Anwendung eine Zeichenfolge mit dem Namen verfügen `Message` in Ihre einer Datei, und die Anwendung sollte die Kultur Französisch-Version der Ressourcendatei Ressourcen.fr-FR.resx haben. Wenn die Anwendung keine der Kultur Französisch-Version der Ressourcendatei, die `My.Resource` Objekt ruft die Ressource aus der Ressourcendatei für die Standardkultur ab.  
  
 [!code-vb[VbVbalrMyResources#10](../../../visual-basic/developing-apps/programming/app-settings/codesnippet/VisualBasic/my-resources-object_5.vb)]  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Anwendungsressourcen (.NET)](/visualstudio/ide/managing-application-resources-dotnet)  
 [Ressourcen in Desktop-Apps](../../../framework/resources/index.md)  

