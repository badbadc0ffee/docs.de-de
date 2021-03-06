---
title: C#-Ausdrücke – Überblick über C#
description: Ausdrücke, Operanden und Operatoren sind Bausteine der Sprache C#.
ms.date: 04/25/2019
ms.assetid: 20d5eb10-7381-47b9-ad90-f1cc895aa27e
ms.openlocfilehash: 4866d12118518827c1f7032ac09933927f0f3c52
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/16/2019
ms.locfileid: "72395671"
---
# <a name="expressions"></a>Ausdrücke

*Ausdrücke* bestehen aus *Operanden* und *Operatoren*. Die Operatoren eines Ausdrucks geben an, welche Operationen auf die Operanden angewendet werden. Beispiele für Operatoren sind `+`, `-`, `*`, `/` und `new`. Beispiele für Operanden sind Literale, Felder, lokale Variablen und Ausdrücke.

Wenn ein Ausdruck mehrere Operatoren enthält, bestimmt die *Rangfolge* der Operatoren die Reihenfolge, in der die einzelnen Operatoren ausgewertet werden. Der Ausdruck `x + y * z` wird z.B. als `x + (y * z)` ausgewertet, da der `*`-Operator Vorrang vor dem `+`-Operator hat.

Tritt ein Operand zwischen zwei Operatoren mit gleicher Rangfolge auf, steuert die *Assoziativität* der Operatoren die Reihenfolge, in der die Vorgänge ausgeführt werden:

* Mit Ausnahme der Zuweisungs- und NULL-Sammeloperatoren sind alle binären Operatoren *linksassoziativ*, was bedeutet, dass Vorgänge von links nach rechts ausgeführt werden. `x + y + z` wird beispielsweise als `(x + y) + z` ausgewertet.
* Die Zuweisungsoperatoren, die NULL-Sammeloperatoren `??` und `??=` und der bedingte Operator `?:` sind *rechtsassoziativ*, d.h., die Operationen werden von rechts nach links ausgeführt. `x = y = z` wird beispielsweise als `x = (y = z)` ausgewertet.

Rangfolge und Assoziativität können mit Klammern gesteuert werden. In `x + y * z` wird beispielsweise zuerst `y` mit `z` multipliziert und dann das Ergebnis zu `x` addiert, aber in `(x + y) * z` werden zunächst `x` und `y` addiert, und dann wird das Ergebnis mit `z` multipliziert.

Die meisten Operatoren können [*überladen*](../language-reference/operators/operator-overloading.md) werden. Das Überladen von Operatoren ermöglicht die Angabe benutzerdefinierter Operatorimplementierungen für Vorgänge, in denen einer der Operanden oder beide einer benutzerdefinierten Klasse oder einem benutzerdefinierten Strukturtyp angehören.

C# bietet eine Reihe von Operatoren für [arithmetische](../language-reference/operators/arithmetic-operators.md), [logische](../language-reference/operators/boolean-logical-operators.md), [bitweise und Verschiebungsvorgänge](../language-reference/operators/bitwise-and-shift-operators.md) sowie Vergleiche von [Gleichheit](../language-reference/operators/equality-operators.md) und [Reihenfolge](../language-reference/operators/comparison-operators.md).

Die vollständige Liste der nach Rangfolgenebene sortierten C#-Operatoren finden Sie unter [C#-Operatoren](../language-reference/operators/index.md).

> [!div class="step-by-step"]
> [Zurück](types-and-variables.md)
> [Weiter](statements.md)
