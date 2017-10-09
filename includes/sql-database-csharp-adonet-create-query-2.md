
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a>Esempio di programma C#

Hello nelle sezioni seguenti di questo articolo presentano un programma c# che utilizza le istruzioni Transact-SQL toosend ADO.NET toohello database SQL. programma Hello c# esegue hello seguenti azioni:

1. [Si connette a database SQL tooour tramite ADO.NET](#cs_1_connect).
2. [Creazione di tabelle](#cs_2_createtables).
3. [Popola tabelle hello con i dati, eseguendo le istruzioni T-SQL INSERT](#cs_3_insert).
4. [Aggiornamento dei dati tramite un join](#cs_4_updatejoin).
5. [Eliminazione dei dati tramite un join](#cs_5_deletejoin).
6. [Selezione di righe di dati tramite join](#cs_6_selectrows).
7. Chiude connessione hello (che elimina tutte le tabelle temporanee da tempdb).

contiene il programma Hello in c#:

- C# database toohello tooconnect del codice.
- Metodi che restituiscono il codice sorgente hello T-SQL.
- Due metodi che consentono di inviare database toohello hello T-SQL.

#### <a name="toocompile-and-run"></a>toocompile ed eseguire

Questo programma C# è costituito logicamente da un file con estensione cs. Ma qui programma hello fisicamente è suddiviso in più blocchi di codice, toomake ciascun blocco toosee più semplice e comprendere. toocompile ed eseguire il programma, hello seguenti:

1. Creare un progetto C# in Visual Studio.
    - tipo di progetto Hello deve essere un *console* un'applicazione, da un risultato simile hello seguente gerarchia: **modelli** > **Visual c#** > **Windows Desktop classico** > **Console App (.NET Framework)**.
3. Nel file hello **Program.cs**, cancellare hello starter small righe di codice.
3. In Program.cs, copia e Incolla di hello seguente i blocchi in hello stessa sequenza in cui vengono presentati di seguito.
4. In Program.cs seguente hello Modifica valori hello **Main** metodo:

   - **cb.DataSource**
   - **cd.UserID**
   - **cb.Password**
   - **InitialCatalog**

5. Verificare l'assembly hello **System.Data.dll** fa riferimento. tooverify, espandere hello **riferimenti** nodo hello **Esplora** riquadro.
6. il programma hello toobuild in Visual Studio, fare clic su hello **compilare** menu.
7. il programma hello toorun da Visual Studio, fare clic su hello **avviare** pulsante. output di Hello del report viene visualizzato in una finestra di cmd.exe.

> [!NOTE]
> È possibile hello la modifica di T-SQL hello tooadd iniziale  **#**  toohello i nomi delle tabelle, che vengono create nelle tabelle temporanee come **tempdb**. Ciò può risultare utile per finalità dimostrative, quando non sono disponibili database di test. Tabelle temporanee vengono eliminate automaticamente quando si chiude la connessione hello. Eventuali parole chiave REFERENCES per chiavi esterne non vengono applicate per le tabelle temporanee.
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a>Blocco C# 1: Connessione tramite ADO.NET

- [Avanti](#cs_2_createtables)


```csharp
using System;
using System.Data.SqlClient;   // System.Data.dll 
//using System.Data;           // For:  SqlDbType , ParameterDirection

namespace csharp_db_test
{
   class Program
   {
      static void Main(string[] args)
      {
         try
         {
            var cb = new SqlConnectionStringBuilder();
            cb.DataSource = "your_server.database.windows.net";
            cb.UserID = "your_user";
            cb.Password = "your_password";
            cb.InitialCatalog = "your_database";

            using (var connection = new SqlConnection(cb.ConnectionString))
            {
               connection.Open();

               Submit_Tsql_NonQuery(connection, "2 - Create-Tables",
                  Build_2_Tsql_CreateTables());

               Submit_Tsql_NonQuery(connection, "3 - Inserts",
                  Build_3_Tsql_Inserts());

               Submit_Tsql_NonQuery(connection, "4 - Update-Join",
                  Build_4_Tsql_UpdateJoin(),
                  "@csharpParmDepartmentName", "Accounting");

               Submit_Tsql_NonQuery(connection, "5 - Delete-Join",
                  Build_5_Tsql_DeleteJoin(),
                  "@csharpParmDepartmentName", "Legal");

               Submit_6_Tsql_SelectEmployees(connection);
            }
         }
         catch (SqlException e)
         {
            Console.WriteLine(e.ToString());
         }
         Console.WriteLine("View hello report output here, then press any key tooend hello program...");
         Console.ReadKey();
      }
```


<a name="cs_2_createtables"/>
### <a name="c-block-2-t-sql-toocreate-tables"></a>Blocco di c# 2: tabelle toocreate T-SQL

- [Indietro](#cs_1_connect)&nbsp; / &nbsp;[Avanti](#cs_3_insert)

```csharp
      static string Build_2_Tsql_CreateTables()
      {
         return @"
DROP TABLE IF EXISTS tabEmployee;
DROP TABLE IF EXISTS tabDepartment;  -- Drop parent table last.


CREATE TABLE tabDepartment
(
   DepartmentCode  nchar(4)          not null
      PRIMARY KEY,
   DepartmentName  nvarchar(128)     not null
);

CREATE TABLE tabEmployee
(
   EmployeeGuid    uniqueIdentifier  not null  default NewId()
      PRIMARY KEY,
   EmployeeName    nvarchar(128)     not null,
   EmployeeLevel   int               not null,
   DepartmentCode  nchar(4)              null
      REFERENCES tabDepartment (DepartmentCode)  -- (REFERENCES would be disallowed on temporary tables.)
);
";
      }
```

#### <a name="entity-relationship-diagram-erd"></a>Diagramma entità-relazione

le istruzioni CREATE TABLE precedente Hello comportano hello **riferimenti** toocreate (parola chiave) un *chiave esterna* relazione (chiave esterna) tra due tabelle.  Se si utilizza tempdb, impostare come commento hello `--REFERENCES` (parola chiave) utilizzando una coppia di trattini iniziali.

Di seguito è riportato un disco di ripristino che visualizza hello relazione tra due tabelle hello. Hello valori hello #tabEmployee.DepartmentCode *figlio* colonna sono valori toohello limitato presenti in hello #tabDepartment.Department *padre* colonna.

![Diagramma entità-relazione che mostra una chiave esterna](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-tooinsert-data"></a>Blocco di c# 3: dati tooinsert T-SQL

- [Indietro](#cs_2_createtables)&nbsp; / &nbsp;[Avanti](#cs_4_updatejoin)


```csharp
      static string Build_3_Tsql_Inserts()
      {
         return @"
-- hello company has these departments.
INSERT INTO tabDepartment
   (DepartmentCode, DepartmentName)
      VALUES
   ('acct', 'Accounting'),
   ('hres', 'Human Resources'),
   ('legl', 'Legal');

-- hello company has these employees, each in one department.
INSERT INTO tabEmployee
   (EmployeeName, EmployeeLevel, DepartmentCode)
      VALUES
   ('Alison'  , 19, 'acct'),
   ('Barbara' , 17, 'hres'),
   ('Carol'   , 21, 'acct'),
   ('Deborah' , 24, 'legl'),
   ('Elle'    , 15, null);
";
      }
```


<a name="cs_4_updatejoin"/>
### <a name="c-block-4-t-sql-tooupdate-join"></a>Blocco di c# 4: join tooupdate T-SQL

- [Indietro](#cs_3_insert)&nbsp; / &nbsp;[Avanti](#cs_5_deletejoin)


```csharp
      static string Build_4_Tsql_UpdateJoin()
      {
         return @"
DECLARE @DName1  nvarchar(128) = @csharpParmDepartmentName;  --'Accounting';


-- Promote everyone in one department (see @parm...).
UPDATE empl
   SET
      empl.EmployeeLevel += 1
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName1;
";
      }
```


<a name="cs_5_deletejoin"/>
### <a name="c-block-5-t-sql-toodelete-join"></a>Blocco di c# 5: join toodelete T-SQL

- [Indietro](#cs_4_updatejoin)&nbsp; / &nbsp;[Avanti](#cs_6_selectrows)


```csharp
      static string Build_5_Tsql_DeleteJoin()
      {
         return @"
DECLARE @DName2  nvarchar(128);
SET @DName2 = @csharpParmDepartmentName;  --'Legal';


-- Right size hello Legal department.
DELETE empl
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName2

-- Disband hello Legal department.
DELETE tabDepartment
   WHERE DepartmentName = @DName2;
";
      }
```



<a name="cs_6_selectrows"/>
### <a name="c-block-6-t-sql-tooselect-rows"></a>Blocco di c# 6: righe tooselect T-SQL

- [Indietro](#cs_5_deletejoin)&nbsp; / &nbsp;[Avanti](#cs_6b_datareader)


```csharp
      static string Build_6_Tsql_SelectEmployees()
      {
         return @"
-- Look at all hello final Employees.
SELECT
      empl.EmployeeGuid,
      empl.EmployeeName,
      empl.EmployeeLevel,
      empl.DepartmentCode,
      dept.DepartmentName
   FROM
      tabEmployee   as empl
      LEFT OUTER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   ORDER BY
      EmployeeName;
";
      }
```


<a name="cs_6b_datareader"/>
### <a name="c-block-6b-executereader"></a>Blocco C# 6b: ExecuteReader

- [Indietro](#cs_6_selectrows)&nbsp; / &nbsp;[Avanti](#cs_7_executenonquery)

Questo metodo è progettato toorun hello T-SQL SELECT che viene compilato da hello **Build_6_Tsql_SelectEmployees** metodo.


```csharp
      static void Submit_6_Tsql_SelectEmployees(SqlConnection connection)
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("Now, SelectEmployees (6)...");

         string tsql = Build_6_Tsql_SelectEmployees();

         using (var command = new SqlCommand(tsql, connection))
         {
            using (SqlDataReader reader = command.ExecuteReader())
            {
               while (reader.Read())
               {
                  Console.WriteLine("{0} , {1} , {2} , {3} , {4}",
                     reader.GetGuid(0),
                     reader.GetString(1),
                     reader.GetInt32(2),
                     (reader.IsDBNull(3)) ? "NULL" : reader.GetString(3),
                     (reader.IsDBNull(4)) ? "NULL" : reader.GetString(4));
               }
            }
         }
      }
```


<a name="cs_7_executenonquery"/>
### <a name="c-block-7-executenonquery"></a>Blocco C# 7: ExecuteNonQuery

- [Indietro](#cs_6b_datareader)&nbsp; / &nbsp;[Avanti](#cs_8_output)

Questo metodo viene chiamato per operazioni di modifica del contenuto delle tabelle dati hello senza restituzione di tutte le righe di dati.


```csharp
      static void Submit_Tsql_NonQuery(
         SqlConnection connection,
         string tsqlPurpose,
         string tsqlSourceCode,
         string parameterName = null,
         string parameterValue = null
         )
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("T-SQL too{0}...", tsqlPurpose);

         using (var command = new SqlCommand(tsqlSourceCode, connection))
         {
            if (parameterName != null)
            {
               command.Parameters.AddWithValue(  // Or, use SqlParameter class.
                  parameterName,
                  parameterValue);
            }
            int rowsAffected = command.ExecuteNonQuery();
            Console.WriteLine(rowsAffected + " = rows affected.");
         }
      }
   } // EndOfClass
}
```


<a name="cs_8_output"/>
### <a name="c-block-8-actual-test-output-toohello-console"></a>Blocco di c# 8: console di test effettivo output toohello

- [Indietro](#cs_7_executenonquery)

In questa sezione acquisisce l'output di hello hello viene inviato toohello console. Solo i valori guid hello variano tra le esecuzioni dei test.


```text
[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>> csharp_db_test.exe

=================================
Now, CreateTables (10)...

=================================
Now, Inserts (20)...

=================================
Now, UpdateJoin (30)...
2 rows affected, by UpdateJoin.

=================================
Now, DeleteJoin (40)...

=================================
Now, SelectEmployees (50)...
0199be49-a2ed-4e35-94b7-e936acf1cd75 , Alison , 20 , acct , Accounting
f0d3d147-64cf-4420-b9f9-76e6e0a32567 , Barbara , 17 , hres , Human Resources
cf4caede-e237-42d2-b61d-72114c7e3afa , Carol , 22 , acct , Accounting
cdde7727-bcfd-4f72-a665-87199c415f8b , Elle , 15 , NULL , NULL

[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>>
```
