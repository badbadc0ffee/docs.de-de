---
title: 'Vorgehensweise: Ermitteln der von einem Encoder unterstützten Parameter'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- encoder parameters [Windows Forms], determining supported
ms.assetid: f47ae459-e3ce-4d41-a140-2f6c6aea3f44
ms.openlocfilehash: 3e5345180e0ff3321b9ef0b885b836d3e9456f28
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2019
ms.locfileid: "64643339"
---
# <a name="how-to-determine-the-parameters-supported-by-an-encoder"></a>Vorgehensweise: Ermitteln der von einem Encoder unterstützten Parameter
Sie können anpassen, Imageparameter, z. B. Qualität und der Komprimierung, jedoch müssen Sie wissen, welche Parameter von einem angegebenen Bildencoder unterstützt werden. Die <xref:System.Drawing.Image> -Klasse stellt die <xref:System.Drawing.Image.GetEncoderParameterList%2A> Methode, damit Sie bestimmen können, welche Parameter für einen bestimmten Encoder unterstützt werden. Sie geben den Encoder mit einer GUID. Die <xref:System.Drawing.Image.GetEncoderParameterList%2A> Methode gibt ein Array von <xref:System.Drawing.Imaging.EncoderParameter> Objekte.  
  
## <a name="example"></a>Beispiel  
 Der folgende Beispielcode gibt die unterstützten Parameter für den JPEG-Encoder. Verwenden Sie die Liste der Parameterkategorien und zugehörigen GUIDs in der <xref:System.Drawing.Imaging.Encoder> Übersicht über die Klasse aus, um die Kategorie für jeden Parameter zu bestimmen.  
  
 [!code-csharp[UsingImageEncodersDecoders#3](~/samples/snippets/csharp/VS_Snippets_Winforms/UsingImageEncodersDecoders/CS/Form1.cs#3)]
 [!code-vb[UsingImageEncodersDecoders#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/UsingImageEncodersDecoders/VB/Form1.vb#3)]  
  
## <a name="compiling-the-code"></a>Kompilieren des Codes  
 Für dieses Beispiel benötigen Sie Folgendes:  
  
- Eine Windows Forms-Anwendung  
  
- Ein <xref:System.Windows.Forms.PaintEventArgs>, d.h. ein Parameter vom <xref:System.Windows.Forms.PaintEventHandler>.  
  
## <a name="see-also"></a>Siehe auch

- [Vorgehensweise: Auflisten installierter Encoder](how-to-list-installed-encoders.md)
- [Typen von Bitmaps](types-of-bitmaps.md)
- [Verwenden von Bildencodern und -decodern in Managed GDI+](using-image-encoders-and-decoders-in-managed-gdi.md)
