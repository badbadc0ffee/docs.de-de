---
title: Abrufen von Daten mit "DataReader"
ms.date: 10/29/2018
dev_langs:
- csharp
- vb
ms.assetid: 97afc121-fb8b-465b-bab3-6d844420badb
ms.openlocfilehash: f3add49d48a569664d4cbb6b5c26d5f3379b6f18
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794407"
---
# <a name="retrieve-data-using-a-datareader"></a>Abrufen von Daten mit einem DataReader
Erstellen Sie zum Abrufen von Daten mithilfe eines **DataReader**-Objekts eine Instanz des **Befehls** Objekts, und erstellen Sie dann einen **DataReader** , indem Sie **Command. ExecuteReader** aufrufen, um Zeilen aus einer Datenquelle abzurufen. Das **DataReader** -Objekt stellt einen nicht gepufferten Datenstrom bereit, der prozeduralen Logik die effiziente Verarbeitung von Ergebnissen aus einer Datenquelle in sequenziell ermöglicht. Der **DataReader** ist eine gute Wahl, wenn Sie große Datenmengen abrufen, da die Daten nicht im Arbeitsspeicher zwischengespeichert werden.

Das folgende Beispiel veranschaulicht die Verwendung eines **DataReader**, `reader` wobei einen gültigen DataReader darstellt `command` und ein gültiges Befehls Objekt darstellt.  

```csharp
reader = command.ExecuteReader();  
```

```vb
reader = command.ExecuteReader()
```  

Verwenden Sie die **DataReader. Read** -Methode, um eine Zeile aus den Abfrage Ergebnissen zu erhalten. Sie können auf jede Spalte der zurückgegebenen Zeile zugreifen, indem Sie den Namen oder die Ordinalzahl der Spalte an den **DataReader**übergeben. Um die bestmögliche Leistung zu erzielen, stellt der **DataReader** eine Reihe von Methoden bereit, mit denen Sie auf Spaltenwerte in ihren systemeigenen Datentypen (**GetDateTime**, **GetDouble**, **GetGuid**, **GetInt32**usw.) zugreifen können. Eine Liste der typisierten Accessormethoden für Datenanbieter spezifische **DataReaders**finden <xref:System.Data.OleDb.OleDbDataReader> Sie unter und <xref:System.Data.SqlClient.SqlDataReader>. Wenn Sie die typisierten Accessormethoden verwenden, wenn Sie wissen, dass der zugrunde liegende Datentyp beim Abrufen des Spaltenwerts die erforderliche Typkonvertierung reduziert.  
  
 Im folgenden Beispiel wird ein **DataReader** -Objekt durchlaufen, und es werden zwei Spalten aus jeder Zeile zurückgegeben.  
  
 [!code-csharp[DataWorks SqlClient.HasRows#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.HasRows/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.HasRows#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.HasRows/VB/source.vb#1)]  
  
## <a name="closing-the-datareader"></a>Schließen des "DataReader"  
 Verwenden Sie immer die **Close** -Methode, wenn Sie das **DataReader** -Objekt nicht mehr benötigen.  
  
 Wenn der **Befehl** Ausgabeparameter oder Rückgabewerte enthält, sind diese Werte erst nach dem Schließen des **DataReader** verfügbar.  
  
 Während ein **DataReader** geöffnet ist, wird die **Verbindung** exklusiv von diesem **DataReader**verwendet. Sie können keine Befehle für die **Verbindung**ausführen, einschließlich der Erstellung eines anderen **DataReader**, bis der ursprüngliche **DataReader** geschlossen wird.  
  
> [!NOTE]
> Führen Sie in der **Finalize** -Methode der Klasse nicht **Close** oder verwerfen für eine **Verbindung**, einen **DataReader** **oder ein** anderes verwaltetes Objekt aus. Geben Sie in einer Finalize-Methode nur nicht verwaltete Ressourcen frei, die der Klasse direkt gehören. Wenn Ihre Klasse keine nicht verwalteten Ressourcen besitzt, schließen Sie keine **Finalize** -Methode in die Klassendefinition ein. Weitere Informationen finden Sie unter [Garbage Collection](../../../standard/garbage-collection/index.md).  
  
## <a name="retrieving-multiple-result-sets-using-nextresult"></a>Abrufen mehrerer Resultsets mithilfe von NextResult  
 Wenn das **DataReader** -Objekt mehrere Resultsets zurückgibt, wird die **NextResult** -Methode aufgerufen, um die Resultsets sequenziell zu durchlaufen. Im folgenden Beispiel werden die Ergebnisse von zwei SELECT-Anweisungen mit der <xref:System.Data.SqlClient.SqlDataReader>-Methode von <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> verarbeitet.  
  
 [!code-csharp[DataWorks SqlClient.NextResult#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.NextResult/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.NextResult#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.NextResult/VB/source.vb#1)]  
  
## <a name="getting-schema-information-from-the-datareader"></a>Erhalten von Schema Informationen aus dem DataReader  
 Während ein **DataReader** geöffnet ist, können Sie Schema Informationen über das aktuelle Resultset mithilfe der **getschembare** -Methode abrufen. **Getschemabel** gibt ein <xref:System.Data.DataTable> -Objekt zurück, das mit Zeilen und Spalten aufgefüllt ist, die die Schema Informationen für das aktuelle Resultset enthalten. Die **Daten** Tabelle enthält eine Zeile für jede Spalte des Resultsets. Jede Spalte der Schema Tabelle ist einer Eigenschaft der Spalten zugeordnet, die in den Zeilen des Resultsets zurückgegeben werden, wobei **ColumnName** der Name der Eigenschaft und der Wert der Spalte der Wert der Eigenschaft ist. Im folgenden Beispiel werden die Schema Informationen für **DataReader**geschrieben.  
  
 [!code-csharp[DataWorks SqlClient.GetSchemaTable#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.GetSchemaTable/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.GetSchemaTable#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.GetSchemaTable/VB/source.vb#1)]  
  
## <a name="working-with-ole-db-chapters"></a>Arbeiten mit OLE DB Kapiteln  
 Hierarchische Rowsets oder Kapitel (OLE DB Type **DBTYPE_HCHAPTER**, ADO Type **adChapter**) können mithilfe von <xref:System.Data.OleDb.OleDbDataReader>abgerufen werden. Wenn eine Abfrage, die ein Kapitel enthält, als **DataReader**zurückgegeben wird, wird das Kapitel als Spalte in diesem **DataReader** zurückgegeben und als **DataReader** -Objekt verfügbar gemacht.  
  
 Das ADO.net- **DataSet** kann auch verwendet werden, um hierarchische Rowsets mithilfe von über-und untergeordneten Beziehungen zwischen Tabellen darzustellen. Weitere Informationen finden Sie unter [Datasets, DataTables und DataViews](./dataset-datatable-dataview/index.md).  
  
 Im folgenden Codebeispiel wird mit dem MSDataShape-Anbieter eine Kapitelspalte mit Bestellungen für jeden Kunden in einer Kundenliste generiert.  
  
```vb  
Using connection As OleDbConnection = New OleDbConnection(
    "Provider=MSDataShape;Data Provider=SQLOLEDB;" &
    "Data Source=localhost;Integrated Security=SSPI;Initial Catalog=northwind")

    Using custCMD As OleDbCommand = New OleDbCommand(
        "SHAPE {SELECT CustomerID, CompanyName FROM Customers} " &
        "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS CustomerOrders " &
        "RELATE CustomerID TO CustomerID)", connection)

        connection.Open()

        Using custReader As OleDbDataReader = custCMD.ExecuteReader()

            Do While custReader.Read()
                Console.WriteLine("Orders for " & custReader.GetString(1))
                ' custReader.GetString(1) = CompanyName  

                Using orderReader As OleDbDataReader = custReader.GetValue(2)
                    ' custReader.GetValue(2) = Orders chapter as DataReader  

                    Do While orderReader.Read()
                        Console.WriteLine(vbTab & orderReader.GetInt32(1))
                        ' orderReader.GetInt32(1) = OrderID  
                    Loop
                    orderReader.Close()
                End Using
            Loop
            ' Make sure to always close readers and connections.  
            custReader.Close()
        End Using
    End Using
End Using
```  
  
```csharp  
using (OleDbConnection connection = new OleDbConnection(
    "Provider=MSDataShape;Data Provider=SQLOLEDB;" +
    "Data Source=localhost;Integrated Security=SSPI;Initial Catalog=northwind"))
{
    using (OleDbCommand custCMD = new OleDbCommand(
        "SHAPE {SELECT CustomerID, CompanyName FROM Customers} " +
        "APPEND ({SELECT CustomerID, OrderID FROM Orders} AS CustomerOrders " +
        "RELATE CustomerID TO CustomerID)", connection))
    {
        connection.Open();

        using (OleDbDataReader custReader = custCMD.ExecuteReader())
        {

            while (custReader.Read())
            {
                Console.WriteLine("Orders for " + custReader.GetString(1));
                // custReader.GetString(1) = CompanyName  

                using (OleDbDataReader orderReader = (OleDbDataReader)custReader.GetValue(2))
                {
                    // custReader.GetValue(2) = Orders chapter as DataReader  

                    while (orderReader.Read())
                        Console.WriteLine("\t" + orderReader.GetInt32(1));
                    // orderReader.GetInt32(1) = OrderID  
                    orderReader.Close();
                }
            }
            // Make sure to always close readers and connections.  
            custReader.Close();
        }
    }
}
```  
  
## <a name="returning-results-with-oracle-ref-cursors"></a>Zurückgeben von Ergebnissen mit Oracle-REF Cursors  
 Der .NET Framework-Datenanbieter für Oracle unterstützt die Verwendung von Oracle-REF CURSORs zur Rückgabe eines Abfrageergebnisses. Ein Oracle-REF CURSOR wird als <xref:System.Data.OracleClient.OracleDataReader> zurückgegeben.  
  
 Sie können ein <xref:System.Data.OracleClient.OracleDataReader> Objekt, das einen Oracle-REF-Cursor darstellt, <xref:System.Data.OracleClient.OracleCommand.ExecuteReader%2A> mithilfe der-Methode abrufen. Sie <xref:System.Data.OracleClient.OracleCommand> können auch einen angeben, der einen oder mehrere Oracle-REF Cursors als **SelectCommand** für einen <xref:System.Data.OracleClient.OracleDataAdapter> zurückgibt, der zum Ausfüllen eines <xref:System.Data.DataSet>verwendet wird.  
  
 Um auf einen von einer Oracle-Datenquelle zurückgegebenen Verweis Cursor zuzugreifen <xref:System.Data.OracleClient.OracleCommand> , erstellen Sie einen für die Abfrage, und fügen Sie einen Output-Parameter <xref:System.Data.OracleClient.OracleCommand.Parameters> hinzu, der <xref:System.Data.OracleClient.OracleCommand>auf den Verweis Cursor auf die-Auflistung Ihres verweist. Der Name des Parameters muss mit dem Namen des REF CURSOR-Parameters in der Abfrage übereinstimmen. Legen Sie den Typ des Parameters <xref:System.Data.OracleClient.OracleType.Cursor?displayProperty=nameWithType>auf fest. Die <xref:System.Data.OracleClient.OracleCommand.ExecuteReader?displayProperty=nameWithType> -Methode <xref:System.Data.OracleClient.OracleCommand> des gibt einen <xref:System.Data.OracleClient.OracleDataReader> für den ref Cursor zurück.  
  
 Wenn Sie <xref:System.Data.OracleClient.OracleCommand> mehrere Ref Cursors zurückgibt, fügen Sie mehrere Ausgabeparameter hinzu. Sie können auf die verschiedenen REF CURSORs zugreifen, indem <xref:System.Data.OracleClient.OracleCommand.ExecuteReader?displayProperty=nameWithType> Sie die-Methode aufrufen. Der-Rückruf <xref:System.Data.OracleClient.OracleCommand.ExecuteReader> gibt einen <xref:System.Data.OracleClient.OracleDataReader> zurück, der auf den ersten Verweis Cursor verweist. Sie können dann die <xref:System.Data.OracleClient.OracleDataReader.NextResult?displayProperty=nameWithType> -Methode aufrufen, um auf nachfolgende Ref Cursors zuzugreifen. Obwohl die Parameter in <xref:System.Data.OracleClient.OracleCommand.Parameters?displayProperty=nameWithType> der Auflistung den REF CURSOR-Ausgabeparametern nach Namen entsprechen, greift der <xref:System.Data.OracleClient.OracleDataReader> in der Reihenfolge, in der <xref:System.Data.OracleClient.OracleCommand.Parameters> Sie der Auflistung hinzugefügt wurden, auf Sie zu.  
  
 Betrachten Sie z. B. das folgende Oracle-Paket und den Paketkörper.  
  
```sql
CREATE OR REPLACE PACKAGE CURSPKG AS   
  TYPE T_CURSOR IS REF CURSOR;   
  PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,   
    DEPTCURSOR OUT T_CURSOR);   
END CURSPKG;  
  
CREATE OR REPLACE PACKAGE BODY CURSPKG AS   
  PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,   
    DEPTCURSOR OUT T_CURSOR)   
  IS   
  BEGIN   
    OPEN EMPCURSOR FOR SELECT * FROM DEMO.EMPLOYEE;   
    OPEN DEPTCURSOR FOR SELECT * FROM DEMO.DEPARTMENT;   
  END OPEN_TWO_CURSORS;   
END CURSPKG;   
```  
  
 Der folgende Code erstellt eine <xref:System.Data.OracleClient.OracleCommand> , die die Ref Cursors aus dem vorherigen Oracle-Paket zurückgibt, indem der <xref:System.Data.OracleClient.OracleType.Cursor?displayProperty=nameWithType> <xref:System.Data.OracleClient.OracleCommand.Parameters?displayProperty=nameWithType> -Auflistung zwei Parameter des Typs hinzugefügt werden.  
  
```vb  
Dim cursCmd As OracleCommand = New OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn)  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
```  
  
```csharp  
OracleCommand cursCmd = new OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn);  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
```  
  
 Der folgende Code gibt die Ergebnisse des vorherigen Befehls mithilfe der <xref:System.Data.OracleClient.OracleDataReader.Read> -Methode und der- <xref:System.Data.OracleClient.OracleDataReader> <xref:System.Data.OracleClient.OracleDataReader.NextResult> Methode von zurück. Die REF CURSOR-Parameter werden der Reihe nach zurückgegeben.  
  
```vb  
oraConn.Open()  
  
Dim cursCmd As OracleCommand = New OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn)  
cursCmd.CommandType = CommandType.StoredProcedure  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output  
  
Dim reader As OracleDataReader = cursCmd.ExecuteReader()  
  
Console.WriteLine(vbCrLf & "Emp ID" & vbTab & "Name")  
  
Do While reader.Read()  
  Console.WriteLine("{0}" & vbTab & "{1}, {2}", reader.GetOracleNumber(0), reader.GetString(1), reader.GetString(2))  
Loop  
  
reader.NextResult()  
  
Console.WriteLine(vbCrLf & "Dept ID" & vbTab & "Name")  
  
Do While reader.Read()  
  Console.WriteLine("{0}" & vbTab & "{1}", reader.GetOracleNumber(0), reader.GetString(1))  
Loop  
' Make sure to always close readers and connections.  
reader.Close()  
oraConn.Close()  
```  
  
```csharp  
oraConn.Open();  
  
OracleCommand cursCmd = new OracleCommand("CURSPKG.OPEN_TWO_CURSORS", oraConn);  
cursCmd.CommandType = CommandType.StoredProcedure;  
cursCmd.Parameters.Add("EMPCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
cursCmd.Parameters.Add("DEPTCURSOR", OracleType.Cursor).Direction = ParameterDirection.Output;  
  
OracleDataReader reader = cursCmd.ExecuteReader();  
  
Console.WriteLine("\nEmp ID\tName");  
  
while (reader.Read())  
  Console.WriteLine("{0}\t{1}, {2}", reader.GetOracleNumber(0), reader.GetString(1), reader.GetString(2));  
  
reader.NextResult();  
  
Console.WriteLine("\nDept ID\tName");  
  
while (reader.Read())  
  Console.WriteLine("{0}\t{1}", reader.GetOracleNumber(0), reader.GetString(1));  
// Make sure to always close readers and connections.  
reader.Close();  
oraConn.Close();  
```  
  
 Im folgenden Beispiel wird der vorherige Befehl verwendet, um eine <xref:System.Data.DataSet> mit den Ergebnissen des Oracle-Pakets aufzufüllen.  
  
```vb  
Dim ds As DataSet = New DataSet()  
  
Dim adapter As OracleDataAdapter = New OracleDataAdapter(cursCmd)  
adapter.TableMappings.Add("Table", "Employees")  
adapter.TableMappings.Add("Table1", "Departments")  
  
adapter.Fill(ds)  
```  
  
```csharp  
DataSet ds = new DataSet();  
  
OracleDataAdapter adapter = new OracleDataAdapter(cursCmd);  
adapter.TableMappings.Add("Table", "Employees");  
adapter.TableMappings.Add("Table1", "Departments");  
  
adapter.Fill(ds);  
```

> [!NOTE]
> Um eine **OverflowException**zu vermeiden, empfiehlt es sich, jede beliebige Konvertierung vom Oracle-Nummertyp in einen gültigen .NET Framework Typ zu verarbeiten, bevor der <xref:System.Data.DataRow>Wert in einer gespeichert wird. Sie können das <xref:System.Data.Common.DataAdapter.FillError> -Ereignis verwenden, um zu bestimmen, ob eine **OverflowException** aufgetreten ist. Weitere Informationen <xref:System.Data.Common.DataAdapter.FillError> zum-Ereignis finden Sie unter [Handling DataAdapter-Ereignisse](handling-dataadapter-events.md).  
  
## <a name="see-also"></a>Siehe auch

- [DataAdapters und DataReaders](dataadapters-and-datareaders.md)
- [Befehle und Parameter](commands-and-parameters.md)
- [Abrufen von Datenbankschemainformationen](retrieving-database-schema-information.md)
- [Übersicht über ADO.NET](ado-net-overview.md)
