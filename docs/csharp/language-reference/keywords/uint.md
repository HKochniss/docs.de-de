---
title: uint (C#-Referenz)
ms.date: 03/14/2017
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- uint
- uint_CSharpKeyword
helpviewer_keywords:
- uint keyword [C#]
ms.assetid: e93e42c6-ec72-4b0b-89df-2fd8d36f7a7b
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: d32f7146d1f9e13d8cf0f275f4fd78b693b09d31
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="uint-c-reference"></a>uint (C#-Referenz)

Das Schlüsselwort `uint` kennzeichnet einen ganzzahligen Typ, der Werte anhand der Größe und des Bereichs speichert, die in der folgenden Tabelle gezeigt werden.  
  
|Typ|Bereich|Größe|.NET Framework-Typ|  
|----------|-----------|----------|-------------------------|  
|`uint`|0 bis 4.294.967.295|32-Bit Ganzzahl ohne Vorzeichen|<xref:System.UInt32?displayProperty=nameWithType>|  
  
 **Hinweis** Der Typ `uint` ist nicht CLS-kompatibel. Verwenden Sie nach Möglichkeit `int`.  
  
## <a name="literals"></a>Literale  

Sie können eine `uint`-Variable deklarieren und initialisieren, indem Sie ihr ein dezimales Literal, ein hexadezimales Literal oder (beginnend mit C# 7) ein binäres Literal zuweisen. Wenn sich das Ganzzahlliteral außerhalb des Bereichs von `uint` befindet (sprich, wenn es kleiner als <xref:System.UInt32.MinValue?displayProperty=nameWithType> oder größer als <xref:System.UInt32.MaxValue?displayProperty=nameWithType> ist) tritt ein Kompilierfehler auf.

Im folgenden Beispiel werden Ganzzahlen wie 3.000.000.000, die als dezimale, hexadezimale und binäre Literale dargestellt werden, den `uint`-Werten zugewiesen.  
  
[!code-csharp[uint](../../../../samples/snippets/csharp/language-reference/keywords/numeric-literals.cs#UInt)]  

> [!NOTE] 
> Verwenden Sie das Präfix `0x` oder `0X` zum Kennzeichnen eines hexadezimalen Literals und das Präfix `0b` oder `0B` zum Kennzeichnen eines binären Literals. Dezimale Literale haben kein Präfix. 

Beginnend mit C#-7, eine Reihe von Features hinzugefügt wurden zur Verbesserung der Lesbarkeit. 
 - C#-7.0 ermöglicht die Verwendung des Zeichens Unterstrich `_`, als Trennzeichen für Ziffern.
 - 7.2 c# ermöglicht `_` als Trennzeichen für ein Literal binäre oder hexadezimale Ziffer nach dem Präfix verwendet werden soll. Ein decimal-Literal ist nicht berechtigt, auf einem führenden Unterstrich.

Einige Beispiele werden unten gezeigt.

[!code-csharp[uint](../../../../samples/snippets/csharp/language-reference/keywords/numeric-literals.cs#UIntS)]  
 
 Ganzzahlliterale können auch ein Suffix enthalten, das den Typ bezeichnet. Das Suffix `U` oder „u“ gibt entweder ein `uint` oder `ulong` an, abhängig vom numerischen Wert des Literals. Im folgenden Beispiel wird das `u`-Suffix verwendet, um eine ganze Zahl ohne Vorzeichen von beiden Typen zu kennzeichnen. Beachten Sie, dass das erste Literal ein `uint` ist, weil sein Wert kleiner als <xref:System.UInt32.MaxValue?displayProperty=nameWithType> ist, während das zweite ein `ulong` ist, weil sein Wert größer als <xref:System.UInt32.MaxValue?displayProperty=nameWithType> ist.

[!code-csharp[usuffix](../../../../samples/snippets/csharp/language-reference/keywords/numeric-suffixes.cs#1)]  
 
Wenn ein Ganzzahlliteral kein Suffix besitzt, ist sein Typ der erste dieser Typen, in dem sein Wert dargestellt werden kann: 

1. [int](int.md)
2. `uint`
3. [long](../../../csharp/language-reference/keywords/long.md)
4. [ulong](../../../csharp/language-reference/keywords/ulong.md) 
  
## <a name="conversions"></a>Konvertierungen  
 Es gibt eine vordefinierte implizite Konvertierung von `uint` in [long](../../../csharp/language-reference/keywords/long.md), [ulong](../../../csharp/language-reference/keywords/ulong.md), [float](../../../csharp/language-reference/keywords/float.md), [double](../../../csharp/language-reference/keywords/double.md) oder [decimal](../../../csharp/language-reference/keywords/decimal.md). Beispiel:  
  
```csharp  
float myFloat = 4294967290;   // OK: implicit conversion to float  
```  
  
 Es gibt eine vordefinierte implizite Konvertierung von [byte](../../../csharp/language-reference/keywords/byte.md), [ushort](../../../csharp/language-reference/keywords/ushort.md) oder [char](../../../csharp/language-reference/keywords/char.md) in `uint`. Andernfalls müssen Sie eine Umwandlung verwenden. Die folgende Anweisung erzeugt z.B. einen Kompilierungsfehler ohne Umwandlung:  
  
```csharp  
long aLong = 22;  
// Error -- no implicit conversion from long:  
uint uInt1 = aLong;   
// OK -- explicit conversion:  
uint uInt2 = (uint)aLong;  
```  
  
 Beachten Sie auch, dass es keine implizite Konvertierung von Gleitkomma-Datentypen in `uint` gibt. Die folgende Anweisung erzeugt z.B. einen Compilerfehler, außer es wird eine explizite Umwandlung verwendet:  
  
```csharp  
// Error -- no implicit conversion from double:  
uint x = 3.0;  
// OK -- explicit conversion:  
uint y = (uint)3.0;   
```  
  
 Informationen zu arithmetischen Ausdrücken mit ganzzahligen und Gleitkommatypen finden Sie unter [float](../../../csharp/language-reference/keywords/float.md) und [double](../../../csharp/language-reference/keywords/double.md).  
  
 Weitere Informationen zu impliziten numerischen Konvertierungsregeln finden Sie in der [Tabelle für implizite numerische Konvertierungen](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md).  
  
## <a name="c-language-specification"></a>C#-Programmiersprachenspezifikation  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.UInt32>  
 [C#-Referenz](../../../csharp/language-reference/index.md)  
 [C#-Programmierhandbuch](../../../csharp/programming-guide/index.md)  
 [C#-Schlüsselwörter](../../../csharp/language-reference/keywords/index.md)  
 [Tabelle ganzzahliger Typen](../../../csharp/language-reference/keywords/integral-types-table.md)  
 [Tabelle integrierter Typen](../../../csharp/language-reference/keywords/built-in-types-table.md)  
 [Tabelle für implizite numerische Konvertierungen](../../../csharp/language-reference/keywords/implicit-numeric-conversions-table.md)  
 [Tabelle für explizite numerische Konvertierungen](../../../csharp/language-reference/keywords/explicit-numeric-conversions-table.md)
