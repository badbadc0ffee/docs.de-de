---
title: char-Typ – C#-Referenz
ms.date: 11/22/2019
f1_keywords:
- char
- char_CSharpKeyword
helpviewer_keywords:
- char data type [C#]
ms.assetid: b51cf4fb-124c-4067-af48-afbac122b228
ms.openlocfilehash: b7ea52eaccda4599969a5d1e3b683d2d842b0d82
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2020
ms.locfileid: "77093239"
---
# <a name="char-c-reference"></a>char (C#-Referenz)

Das Schlüsselwort vom Typ `char` ist ein Alias für den .NET-<xref:System.Char?displayProperty=nameWithType>-Strukturtyp, der ein Unicode-UTF-16-Zeichen darstellt.

|Typ|Bereich|Größe|.NET-Typ|
|----------|-----------|----------|-------------------------|
|`char`|U+0000 in U+FFFF|16 Bit|<xref:System.Char?displayProperty=nameWithType>|

Der Standardwert des `char`-Typs ist `\0`, d. h. U+0000.

Der [string](reference-types.md#the-string-type)-Typ stellt Text als Sequenz von `char`-Werten dar.

## <a name="literals"></a>Literale

Sie können einen `char`-Wert mit Folgendem angeben:

- einem Zeichenliteral.
- einer Escapesequenz für Unicodezeichen, d. h. `\u` gefolgt von der aus vier Symbolen bestehenden Hexadezimaldarstellung eines Zeichencodes.
- einer Escapesequenz für Hexadezimalzahlen, d. h. `\x` gefolgt von der Hexadezimaldarstellung eines Zeichencodes.

[!code-csharp-interactive[char literals](~/samples/csharp/language-reference/builtin-types/CharType.cs#Literals)]

Wie das obige Beispiel zeigt, können Sie den Wert eines Zeichencodes auch in den entsprechenden `char`-Wert umwandeln.

> [!NOTE]
> Im Falle einer Escapesequenz für Unicodezeichen müssen Sie alle vier Hexadezimalziffern angeben. `\u006A` ist also eine gültige Escapesequenz, `\u06A` und `\u6A` sind hingegen nicht gültig.
>
> Bei einer Escapesequenz für Hexadezimalzahlen können Sie die führenden Nullen weglassen. Die Escapesequenzen `\x006A`, `\x06A` und `\x6A` sind also gültig und entsprechen demselben Zeichen.

## <a name="conversions"></a>Konvertierungen

Der `char`-Typ kann implizit in die folgenden [ganzzahligen](integral-numeric-types.md) Typen konvertiert werden: `ushort`, `int`, `uint`, `long` und `ulong`. Zudem lässt er sich auch implizit in diese integrierten numerischen [Gleitkommatypen](floating-point-numeric-types.md) konvertieren: `float`, `double` und `decimal`. Er kann explizit in die ganzzahligen Typen `sbyte`, `byte` und `short` konvertiert werden.

Es gibt keine impliziten Konvertierungen anderen Typen in Typ `char`. Alle [ganzzahligen](integral-numeric-types.md) numerischen Typen oder numerischen [Gleitkommatypen](floating-point-numeric-types.md) lassen sich jedoch explizit in `char` konvertieren.

## <a name="c-language-specification"></a>C#-Sprachspezifikation

Weitere Informationen finden Sie im Abschnitt [Integrale Typen](~/_csharplang/spec/types.md#integral-types) der [C#-Sprachspezifikation](~/_csharplang/spec/introduction.md).

## <a name="see-also"></a>Siehe auch

- [C#-Referenz](../index.md)
- [Werttypen](value-types.md)
- [Zeichenfolgen](../../programming-guide/strings/index.md)
- <xref:System.Text.Rune?displayProperty=nameWithType>
