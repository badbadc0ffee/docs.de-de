---
title: 'Vorgehensweise: Verwenden der Bildkantenglättung mit Text'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- strings [Windows Forms], smoothing drawn
- antialiasing [Windows Forms], using with text
- text [Windows Forms], smoothing
- text [Windows Forms], antialiasing
- strings [Windows Forms], antialiasing when drawing
ms.assetid: 48fc34f3-f236-4b01-a0cb-f0752e6d22ae
ms.openlocfilehash: 080d946bd72da8b76ed846efdf149eb328d66336
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505732"
---
# <a name="how-to-use-antialiasing-with-text"></a>Vorgehensweise: Verwenden der Bildkantenglättung mit Text
*Antialiasing* bezieht sich auf das Glätten der gezackten Kanten des gezeichneten Grafiken und Text, um ihre Darstellung oder die Lesbarkeit zu verbessern. Mit den verwalteten GDI +-Klassen können Sie qualitativ hochwertige geglätteten Text als auch vom niedrigere Qualität Text rendern. Höhere Qualität Rendering dauert in der Regel mehr Verarbeitungszeit als vom niedrigere Qualität Rendering. Um die Qualität der Text festzulegen, legen Sie die <xref:System.Drawing.Graphics.TextRenderingHint%2A> Eigenschaft eine <xref:System.Drawing.Graphics> auf eines der Elemente von der <xref:System.Drawing.Text.TextRenderingHint> Enumeration  
  
## <a name="example"></a>Beispiel  
 Im folgenden Codebeispiel wird zeichnet Text mit zwei Einstellungen für unterschiedliche Qualität.  
  
 [!code-csharp[System.Drawing.FontsAndText#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.FontsAndText/CS/Class1.cs#21)]
 [!code-vb[System.Drawing.FontsAndText#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.FontsAndText/VB/Class1.vb#21)]  
 
 Die folgende Abbildung zeigt die Ausgabe des Beispielcodes:  
  
 ![Screenshot mit Text mit zwei Einstellungen für unterschiedliche Qualität.](./media/how-to-use-antialiasing-with-text/antialiasing-text-quality-settings.png)  
  
## <a name="compiling-the-code"></a>Kompilieren des Codes  
 Das vorherige Codebeispiel ist für die Verwendung mit Windows Forms konzipiert und erfordert <xref:System.Windows.Forms.PaintEventArgs> `e`, d.h. ein Parameter vom <xref:System.Windows.Forms.PaintEventHandler>.  
  
## <a name="see-also"></a>Siehe auch

- [Verwenden von Schriftarten und Text](using-fonts-and-text.md)
