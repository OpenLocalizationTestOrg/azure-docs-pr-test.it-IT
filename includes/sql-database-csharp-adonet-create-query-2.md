
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a><span data-ttu-id="ee078-101">Esempio di programma C#</span><span class="sxs-lookup"><span data-stu-id="ee078-101">C# program example</span></span>

<span data-ttu-id="ee078-102">Hello nelle sezioni seguenti di questo articolo presentano un programma c# che utilizza le istruzioni Transact-SQL toosend ADO.NET toohello database SQL.</span><span class="sxs-lookup"><span data-stu-id="ee078-102">hello next sections of this article present a C# program that uses ADO.NET toosend Transact-SQL statements toohello SQL database.</span></span> <span data-ttu-id="ee078-103">programma Hello c# esegue hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="ee078-103">hello C# program performs hello following actions:</span></span>

1. <span data-ttu-id="ee078-104">[Si connette a database SQL tooour tramite ADO.NET](#cs_1_connect).</span><span class="sxs-lookup"><span data-stu-id="ee078-104">[Connects tooour SQL database using ADO.NET](#cs_1_connect).</span></span>
2. <span data-ttu-id="ee078-105">[Creazione di tabelle](#cs_2_createtables).</span><span class="sxs-lookup"><span data-stu-id="ee078-105">[Creates tables](#cs_2_createtables).</span></span>
3. <span data-ttu-id="ee078-106">[Popola tabelle hello con i dati, eseguendo le istruzioni T-SQL INSERT](#cs_3_insert).</span><span class="sxs-lookup"><span data-stu-id="ee078-106">[Populates hello tables with data, by issuing T-SQL INSERT statements](#cs_3_insert).</span></span>
4. <span data-ttu-id="ee078-107">[Aggiornamento dei dati tramite un join](#cs_4_updatejoin).</span><span class="sxs-lookup"><span data-stu-id="ee078-107">[Updates data by use of a join](#cs_4_updatejoin).</span></span>
5. <span data-ttu-id="ee078-108">[Eliminazione dei dati tramite un join](#cs_5_deletejoin).</span><span class="sxs-lookup"><span data-stu-id="ee078-108">[Deletes data by use of a join](#cs_5_deletejoin).</span></span>
6. <span data-ttu-id="ee078-109">[Selezione di righe di dati tramite join](#cs_6_selectrows).</span><span class="sxs-lookup"><span data-stu-id="ee078-109">[Selects data rows by use of a join](#cs_6_selectrows).</span></span>
7. <span data-ttu-id="ee078-110">Chiude connessione hello (che elimina tutte le tabelle temporanee da tempdb).</span><span class="sxs-lookup"><span data-stu-id="ee078-110">Closes hello connection (which drops any temporary tables from tempdb).</span></span>

<span data-ttu-id="ee078-111">contiene il programma Hello in c#:</span><span class="sxs-lookup"><span data-stu-id="ee078-111">hello C# program contains:</span></span>

- <span data-ttu-id="ee078-112">C# database toohello tooconnect del codice.</span><span class="sxs-lookup"><span data-stu-id="ee078-112">C# code tooconnect toohello database.</span></span>
- <span data-ttu-id="ee078-113">Metodi che restituiscono il codice sorgente hello T-SQL.</span><span class="sxs-lookup"><span data-stu-id="ee078-113">Methods that return hello T-SQL source code.</span></span>
- <span data-ttu-id="ee078-114">Due metodi che consentono di inviare database toohello hello T-SQL.</span><span class="sxs-lookup"><span data-stu-id="ee078-114">Two methods that submit hello T-SQL toohello database.</span></span>

#### <a name="toocompile-and-run"></a><span data-ttu-id="ee078-115">toocompile ed eseguire</span><span class="sxs-lookup"><span data-stu-id="ee078-115">toocompile and run</span></span>

<span data-ttu-id="ee078-116">Questo programma C# è costituito logicamente da un file con estensione cs.</span><span class="sxs-lookup"><span data-stu-id="ee078-116">This C# program is logically one .cs file.</span></span> <span data-ttu-id="ee078-117">Ma qui programma hello fisicamente è suddiviso in più blocchi di codice, toomake ciascun blocco toosee più semplice e comprendere.</span><span class="sxs-lookup"><span data-stu-id="ee078-117">But here hello program is physically divided into several code blocks, toomake each block easier toosee and understand.</span></span> <span data-ttu-id="ee078-118">toocompile ed eseguire il programma, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ee078-118">toocompile and run this program, do hello following:</span></span>

1. <span data-ttu-id="ee078-119">Creare un progetto C# in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ee078-119">Create a C# project in Visual Studio.</span></span>
    - <span data-ttu-id="ee078-120">tipo di progetto Hello deve essere un *console* un'applicazione, da un risultato simile hello seguente gerarchia: **modelli** > **Visual c#** > **Windows Desktop classico** > **Console App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="ee078-120">hello project type should be a *console* application, from something like hello following hierarchy: **Templates** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
3. <span data-ttu-id="ee078-121">Nel file hello **Program.cs**, cancellare hello starter small righe di codice.</span><span class="sxs-lookup"><span data-stu-id="ee078-121">In hello file **Program.cs**, erase hello small starter lines of code.</span></span>
3. <span data-ttu-id="ee078-122">In Program.cs, copia e Incolla di hello seguente i blocchi in hello stessa sequenza in cui vengono presentati di seguito.</span><span class="sxs-lookup"><span data-stu-id="ee078-122">Into Program.cs, copy and paste each of hello following blocks, in hello same sequence they are presented here.</span></span>
4. <span data-ttu-id="ee078-123">In Program.cs seguente hello Modifica valori hello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="ee078-123">In Program.cs, edit hello following values in hello **Main** method:</span></span>

   - <span data-ttu-id="ee078-124">**cb.DataSource**</span><span class="sxs-lookup"><span data-stu-id="ee078-124">**cb.DataSource**</span></span>
   - <span data-ttu-id="ee078-125">**cd.UserID**</span><span class="sxs-lookup"><span data-stu-id="ee078-125">**cd.UserID**</span></span>
   - <span data-ttu-id="ee078-126">**cb.Password**</span><span class="sxs-lookup"><span data-stu-id="ee078-126">**cb.Password**</span></span>
   - <span data-ttu-id="ee078-127">**InitialCatalog**</span><span class="sxs-lookup"><span data-stu-id="ee078-127">**InitialCatalog**</span></span>

5. <span data-ttu-id="ee078-128">Verificare l'assembly hello **System.Data.dll** fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="ee078-128">Verify that hello assembly **System.Data.dll** is referenced.</span></span> <span data-ttu-id="ee078-129">tooverify, espandere hello **riferimenti** nodo hello **Esplora** riquadro.</span><span class="sxs-lookup"><span data-stu-id="ee078-129">tooverify, expand hello **References** node in hello **Solution Explorer** pane.</span></span>
6. <span data-ttu-id="ee078-130">il programma hello toobuild in Visual Studio, fare clic su hello **compilare** menu.</span><span class="sxs-lookup"><span data-stu-id="ee078-130">toobuild hello program in Visual Studio, click hello **Build** menu.</span></span>
7. <span data-ttu-id="ee078-131">il programma hello toorun da Visual Studio, fare clic su hello **avviare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="ee078-131">toorun hello program from Visual Studio, click hello **Start** button.</span></span> <span data-ttu-id="ee078-132">output di Hello del report viene visualizzato in una finestra di cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="ee078-132">hello report output is displayed in a cmd.exe window.</span></span>

> [!NOTE]
> <span data-ttu-id="ee078-133">È possibile hello la modifica di T-SQL hello tooadd iniziale  **#**  toohello i nomi delle tabelle, che vengono create nelle tabelle temporanee come **tempdb**.</span><span class="sxs-lookup"><span data-stu-id="ee078-133">You have hello option of editing hello T-SQL tooadd a leading **#** toohello table names, which creates them as temporary tables in **tempdb**.</span></span> <span data-ttu-id="ee078-134">Ciò può risultare utile per finalità dimostrative, quando non sono disponibili database di test.</span><span class="sxs-lookup"><span data-stu-id="ee078-134">This can be useful for demonstration purposes, when no test database is available.</span></span> <span data-ttu-id="ee078-135">Tabelle temporanee vengono eliminate automaticamente quando si chiude la connessione hello.</span><span class="sxs-lookup"><span data-stu-id="ee078-135">Temporary tables are deleted automatically when hello connection closes.</span></span> <span data-ttu-id="ee078-136">Eventuali parole chiave REFERENCES per chiavi esterne non vengono applicate per le tabelle temporanee.</span><span class="sxs-lookup"><span data-stu-id="ee078-136">Any REFERENCES for foreign keys are not enforced for temporary tables.</span></span>
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a><span data-ttu-id="ee078-137">Blocco C# 1: Connessione tramite ADO.NET</span><span class="sxs-lookup"><span data-stu-id="ee078-137">C# block 1: Connect by using ADO.NET</span></span>

- [<span data-ttu-id="ee078-138">Avanti</span><span class="sxs-lookup"><span data-stu-id="ee078-138">Next</span></span>](#cs_2_createtables)


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
### <a name="c-block-2-t-sql-toocreate-tables"></a><span data-ttu-id="ee078-139">Blocco di c# 2: tabelle toocreate T-SQL</span><span class="sxs-lookup"><span data-stu-id="ee078-139">C# block 2: T-SQL toocreate tables</span></span>

- <span data-ttu-id="ee078-140">[Indietro](#cs_1_connect)&nbsp; / &nbsp;[Avanti](#cs_3_insert)</span><span class="sxs-lookup"><span data-stu-id="ee078-140">[Previous](#cs_1_connect) &nbsp; / &nbsp; [Next](#cs_3_insert)</span></span>

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

#### <a name="entity-relationship-diagram-erd"></a><span data-ttu-id="ee078-141">Diagramma entità-relazione</span><span class="sxs-lookup"><span data-stu-id="ee078-141">Entity Relationship Diagram (ERD)</span></span>

<span data-ttu-id="ee078-142">le istruzioni CREATE TABLE precedente Hello comportano hello **riferimenti** toocreate (parola chiave) un *chiave esterna* relazione (chiave esterna) tra due tabelle.</span><span class="sxs-lookup"><span data-stu-id="ee078-142">hello preceding CREATE TABLE statements involve hello **REFERENCES** keyword toocreate a *foreign key* (FK) relationship between two tables.</span></span>  <span data-ttu-id="ee078-143">Se si utilizza tempdb, impostare come commento hello `--REFERENCES` (parola chiave) utilizzando una coppia di trattini iniziali.</span><span class="sxs-lookup"><span data-stu-id="ee078-143">If you are using tempdb, comment out hello `--REFERENCES` keyword using a pair of leading dashes.</span></span>

<span data-ttu-id="ee078-144">Di seguito è riportato un disco di ripristino che visualizza hello relazione tra due tabelle hello.</span><span class="sxs-lookup"><span data-stu-id="ee078-144">Next is an ERD that displays hello relationship between hello two tables.</span></span> <span data-ttu-id="ee078-145">Hello valori hello #tabEmployee.DepartmentCode *figlio* colonna sono valori toohello limitato presenti in hello #tabDepartment.Department *padre* colonna.</span><span class="sxs-lookup"><span data-stu-id="ee078-145">hello values in hello #tabEmployee.DepartmentCode *child* column are limited toohello values present in hello #tabDepartment.Department *parent* column.</span></span>

![Diagramma entità-relazione che mostra una chiave esterna](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-tooinsert-data"></a><span data-ttu-id="ee078-147">Blocco di c# 3: dati tooinsert T-SQL</span><span class="sxs-lookup"><span data-stu-id="ee078-147">C# block 3: T-SQL tooinsert data</span></span>

- <span data-ttu-id="ee078-148">[Indietro](#cs_2_createtables)&nbsp; / &nbsp;[Avanti](#cs_4_updatejoin)</span><span class="sxs-lookup"><span data-stu-id="ee078-148">[Previous](#cs_2_createtables) &nbsp; / &nbsp; [Next](#cs_4_updatejoin)</span></span>


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
### <a name="c-block-4-t-sql-tooupdate-join"></a><span data-ttu-id="ee078-149">Blocco di c# 4: join tooupdate T-SQL</span><span class="sxs-lookup"><span data-stu-id="ee078-149">C# block 4: T-SQL tooupdate-join</span></span>

- <span data-ttu-id="ee078-150">[Indietro](#cs_3_insert)&nbsp; / &nbsp;[Avanti](#cs_5_deletejoin)</span><span class="sxs-lookup"><span data-stu-id="ee078-150">[Previous](#cs_3_insert) &nbsp; / &nbsp; [Next](#cs_5_deletejoin)</span></span>


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
### <a name="c-block-5-t-sql-toodelete-join"></a><span data-ttu-id="ee078-151">Blocco di c# 5: join toodelete T-SQL</span><span class="sxs-lookup"><span data-stu-id="ee078-151">C# block 5: T-SQL toodelete-join</span></span>

- <span data-ttu-id="ee078-152">[Indietro](#cs_4_updatejoin)&nbsp; / &nbsp;[Avanti](#cs_6_selectrows)</span><span class="sxs-lookup"><span data-stu-id="ee078-152">[Previous](#cs_4_updatejoin) &nbsp; / &nbsp; [Next](#cs_6_selectrows)</span></span>


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
### <a name="c-block-6-t-sql-tooselect-rows"></a><span data-ttu-id="ee078-153">Blocco di c# 6: righe tooselect T-SQL</span><span class="sxs-lookup"><span data-stu-id="ee078-153">C# block 6: T-SQL tooselect rows</span></span>

- <span data-ttu-id="ee078-154">[Indietro](#cs_5_deletejoin)&nbsp; / &nbsp;[Avanti](#cs_6b_datareader)</span><span class="sxs-lookup"><span data-stu-id="ee078-154">[Previous](#cs_5_deletejoin) &nbsp; / &nbsp; [Next](#cs_6b_datareader)</span></span>


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
### <a name="c-block-6b-executereader"></a><span data-ttu-id="ee078-155">Blocco C# 6b: ExecuteReader</span><span class="sxs-lookup"><span data-stu-id="ee078-155">C# block 6b: ExecuteReader</span></span>

- <span data-ttu-id="ee078-156">[Indietro](#cs_6_selectrows)&nbsp; / &nbsp;[Avanti](#cs_7_executenonquery)</span><span class="sxs-lookup"><span data-stu-id="ee078-156">[Previous](#cs_6_selectrows) &nbsp; / &nbsp; [Next](#cs_7_executenonquery)</span></span>

<span data-ttu-id="ee078-157">Questo metodo è progettato toorun hello T-SQL SELECT che viene compilato da hello **Build_6_Tsql_SelectEmployees** metodo.</span><span class="sxs-lookup"><span data-stu-id="ee078-157">This method is designed toorun hello T-SQL SELECT statement that is built by hello **Build_6_Tsql_SelectEmployees** method.</span></span>


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
### <a name="c-block-7-executenonquery"></a><span data-ttu-id="ee078-158">Blocco C# 7: ExecuteNonQuery</span><span class="sxs-lookup"><span data-stu-id="ee078-158">C# block 7: ExecuteNonQuery</span></span>

- <span data-ttu-id="ee078-159">[Indietro](#cs_6b_datareader)&nbsp; / &nbsp;[Avanti](#cs_8_output)</span><span class="sxs-lookup"><span data-stu-id="ee078-159">[Previous](#cs_6b_datareader) &nbsp; / &nbsp; [Next](#cs_8_output)</span></span>

<span data-ttu-id="ee078-160">Questo metodo viene chiamato per operazioni di modifica del contenuto delle tabelle dati hello senza restituzione di tutte le righe di dati.</span><span class="sxs-lookup"><span data-stu-id="ee078-160">This method is called for operations that modify hello data content of tables without returning any data rows.</span></span>


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
### <a name="c-block-8-actual-test-output-toohello-console"></a><span data-ttu-id="ee078-161">Blocco di c# 8: console di test effettivo output toohello</span><span class="sxs-lookup"><span data-stu-id="ee078-161">C# block 8: Actual test output toohello console</span></span>

- [<span data-ttu-id="ee078-162">Indietro</span><span class="sxs-lookup"><span data-stu-id="ee078-162">Previous</span></span>](#cs_7_executenonquery)

<span data-ttu-id="ee078-163">In questa sezione acquisisce l'output di hello hello viene inviato toohello console.</span><span class="sxs-lookup"><span data-stu-id="ee078-163">This section captures hello output that hello program sent toohello console.</span></span> <span data-ttu-id="ee078-164">Solo i valori guid hello variano tra le esecuzioni dei test.</span><span class="sxs-lookup"><span data-stu-id="ee078-164">Only hello guid values vary between test runs.</span></span>


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
