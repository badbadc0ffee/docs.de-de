---
title: <elementname> ist veraltet (Visual Basic-Warnung)
ms.date: 07/20/2015
f1_keywords:
- vbc40008
- bc40008
helpviewer_keywords:
- BC40008
ms.assetid: 729e3eb5-76ac-4c55-9fdd-78350e0de55e
ms.openlocfilehash: d7d3d86f89ef3b76e958707dd0be2dce8a3e9bf2
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2019
ms.locfileid: "64659821"
---
# <a name="elementname-is-obsolete-visual-basic-warning"></a>"\<Elementname >' ist veraltet (Visual Basic-Warnung)
Eine Anweisung versucht, auf ein Programmierelement zuzugreifen, das mit dem <xref:System.ObsoleteAttribute> -Attribut und der Direktive gekennzeichnet wurde, den Zugriffsversuch als Warnung zu behandeln.  
  
 Sie können jedes beliebige Programmierelement als nicht mehr in Gebrauch kennzeichnen, indem Sie <xref:System.ObsoleteAttribute> darauf anwenden. Dabei können Sie die <xref:System.ObsoleteAttribute.IsError%2A> -Eigenschaft des Attributs entweder auf `True` oder `False`festlegen. Wenn Sie sie auf `True`festlegen, behandelt der Compiler den Versuch, das Element zu verwenden, als Fehler. Wenn Sie sie auf `False`festlegen oder die Standardeinstellung `False`übernehmen, gibt der Compiler bei dem Versuch, das Element zu verwenden, eine Warnung aus.  
  
 Diese Meldung ist standardmäßig eine Warnung, da die <xref:System.ObsoleteAttribute.IsError%2A> -Eigenschaft von <xref:System.ObsoleteAttribute> den Wert `False`aufweist. Weitere Informationen zum Ausblenden von Warnungen oder zum Behandeln von Warnungen als Fehler finden Sie unter [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **Fehler-ID:** BC40008  
  
## <a name="to-correct-this-error"></a>So beheben Sie diesen Fehler  
  
- Stellen Sie sicher, dass der Elementname im Quellcodeverweis richtig geschrieben ist.  
  
## <a name="see-also"></a>Siehe auch

- [Übersicht über Attribute](../../../visual-basic/programming-guide/concepts/attributes/index.md)
