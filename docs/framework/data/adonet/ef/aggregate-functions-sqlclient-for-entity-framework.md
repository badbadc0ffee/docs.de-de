---
title: Aggregatfunktionen (SqlClient für Entity Framework)
ms.date: 03/30/2017
ms.assetid: 03303f01-b591-4efc-9875-f9c608edff0b
ms.openlocfilehash: 3dbd4c0a24a5fc41153ea16747325e824669b0e5
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700056"
---
# <a name="aggregate-functions-sqlclient-for-entity-framework"></a>Aggregatfunktionen (SqlClient für Entity Framework)
Der .NET Framework-Datenanbieter für SQL Server (SqlClient) stellt Aggregatfunktionen zur Verfügung. Aggregatfunktionen führen Berechnungen für eine Reihe von Eingabewerten aus und geben einen einzelnen Wert zurück. Diese Funktionen befinden sich im SQLServer-Namespace, der bei der Verwendung von SqlClient verfügbar ist. Anhand der Namespaceigenschaft des Anbieters kann Entity Framework ermitteln, welches Präfix von diesem Anbieter für spezifische Konstrukte, wie Typen und Funktionen, verwendet wird.  
  
 Im folgenden finden Sie die SqlClient-Aggregatfunktionen.  

## <a name="avgexpression"></a>AVG (Ausdruck)

Gibt den Durchschnitt aller Werte in einer Auflistung zurück. Nullwerte werden ignoriert.

**Argumente**

Eine `Int32`, `Int64`, `Double`und `Decimal`.

**Rückgabewert**

Der `expression`-Typ.

**Beispiel**

[!code-sql[DP EntityServices Concepts#SQLSERVER_AVG](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_avg)]

## <a name="checksum_aggcollection"></a>CHECKSUM_AGG (Sammlung)
 
 Gibt die Prüfsumme der Werte in einer Auflistung zurück. Nullwerte werden ignoriert.
 
 **Argumente**
 
 Eine-Auflistung (`Int32`).
 
 **Rückgabewert**
 
 Ein `Int32`.
 
 **Beispiel**
 
[!code-sql[DP EntityServices Concepts#SQLSERVER_CHECKSUM](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_checksum)]
   
## <a name="countexpression"></a>COUNT (Ausdruck)

Gibt die Anzahl der Elemente in einer Auflistung als `Int32` zurück.

**Argumente**

Eine Auflistung\<t >, wobei t einer der folgenden Typen ist:

|   |   |   |   |
|---|---|---|---|
|`Boolean`|`Double`|`DateTime`|`DateTimeOffset`|
|`Time`|`String`|`Binary`|`Guid` (nicht zurückgegeben in SQL Server 2000)|

**Rückgabewert**

Ein `Int32`.

**Beispiel**

[!code-sql[DP EntityServices Concepts#SQLSERVER_COUNT](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_count)]
 
## <a name="count_bigexpression"></a>COUNT_BIG (Ausdruck)
 
Gibt die Anzahl der Elemente in einer Auflistung als `bigint` zurück.
 
 **Argumente**
 
 Eine Auflistung (t), wobei t einer der folgenden Typen ist:
 
 |   |   |   |   |
|---|---|---|---|
|`Boolean`|`Double`|`DateTime`|`DateTimeOffset`|
|`Time`|`String`|`Binary`|`Guid` (nicht zurückgegeben in SQL Server 2000)|

**Rückgabewert**

Ein `Int64`.

**Beispiel**

[!code-sql[DP EntityServices Concepts#SQLSERVER_COUNTBIG](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_countbig)]

## <a name="maxexpression"></a>Max (Ausdruck)

Gibt den Maximalwert der Auflistung zurück.

**Argumente**

Eine Auflistung (t), wobei t einer der folgenden Typen ist: 

|   |   |   |   |
|---|---|---|---|
|`Boolean`|`Double`|`DateTime`|`DateTimeOffset`|
|`Time`|`String`|`Binary`||

**Rückgabewert**

Der `expression`-Typ.

**Beispiel**

[!code-sql[DP EntityServices Concepts#SQLSERVER_MAX](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_max)]

## <a name="minexpression"></a>MIN (Ausdruck)

Gibt den Minimalwert in einer Auflistung zurück.

**Argumente**

Eine Auflistung (t), wobei t einer der folgenden Typen ist: 

|   |   |   |   |
|---|---|---|---|
|`Boolean`|`Double`|`DateTime`|`DateTimeOffset`|
|`Time`|`String`|`Binary`||

**Rückgabewert**

Der `expression`-Typ.

**Beispiel**

[!code-sql[DP EntityServices Concepts#SQLSERVER_MIN](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_min)]

## <a name="stdevexpression"></a>StDev (Ausdruck)

Gibt die statistische Standardabweichung aller Werte im angegebenen Ausdruck zurück.

**Argumente**

Eine-Auflistung (`Double`).

**Rückgabewert**

Ein `Double`.

**Beispiel**

[!code-sql[DP EntityServices Concepts#SQLSERVER_STDEV](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_stdev)]

## <a name="stdevpexpression"></a>STDE VP (Ausdruck)

Gibt die statistische Standardabweichung für die Auffüllung für alle Werte des angegebenen Ausdrucks zurück.

**Argumente**

Eine-Auflistung (`Double`).

**Rückgabewert**

Ein `Double`.

**Beispiel**

[!code-sql[DP EntityServices Concepts#SQLSERVER_STDEVP](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_stdevp)]

## <a name="sumexpression"></a>Sum (Ausdruck)

Gibt die Summe aller Werte in der Auflistung zurück.

**Argumente**

Eine Auflistung (t), wobei t einer der folgenden Typen ist: `Int32`, `Int64`, `Double`, `Decimal`.

**Rückgabewert**

Der `expression`-Typ.

**Beispiel**

[!code-sql[DP EntityServices Concepts#SQLSERVER_SUM](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_sum)]

## <a name="varexpression"></a>VAR (Ausdruck)

Gibt die statistische Varianz aller Werte im angegebenen Ausdruck zurück.

**Argumente**

Eine-Auflistung (`Double`).

**Rückgabewert**

Ein `Double`.

**Beispiel**

[!code-sql[DP EntityServices Concepts#SQLSERVER_VAR](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_var)]

## <a name="varpexpression"></a>VarP (Ausdruck)

Gibt die statistische Varianz für die Auffüllung aller Werte im angegebenen Ausdruck zurück.

**Argumente**

Eine-Auflistung (`Double`).

**Rückgabewert**

Ein `Double`.

**Beispiel**

[!code-sql[DP EntityServices Concepts#SQLSERVER_VARP](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#sqlserver_varp)] 
  
## <a name="see-also"></a>Siehe auch

- [Aggregatfunktionen (Transact-SQL)](/sql/t-sql/functions/aggregate-functions-transact-sql)
- [Entity SQL Language (Entity SQL-Sprache)](./language-reference/entity-sql-language.md)
- [Aggregieren kanonischer Funktionen](./language-reference/aggregate-canonical-functions.md)
