
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a><span data-ttu-id="26144-101">Esempio di programma C#</span><span class="sxs-lookup"><span data-stu-id="26144-101">C# program example</span></span>

<span data-ttu-id="26144-102">Le sezioni successive di questo articolo presentano un programma C# che usa ADO.NET per inviare istruzioni Transact-SQL al database SQL.</span><span class="sxs-lookup"><span data-stu-id="26144-102">The next sections of this article present a C# program that uses ADO.NET to send Transact-SQL statements to the SQL database.</span></span> <span data-ttu-id="26144-103">Il programma C# esegue le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="26144-103">The C# program performs the following actions:</span></span>

1. <span data-ttu-id="26144-104">[Connessione al database SQL tramite ADO.NET](#cs_1_connect).</span><span class="sxs-lookup"><span data-stu-id="26144-104">[Connects to our SQL database using ADO.NET](#cs_1_connect).</span></span>
2. <span data-ttu-id="26144-105">[Creazione di tabelle](#cs_2_createtables).</span><span class="sxs-lookup"><span data-stu-id="26144-105">[Creates tables](#cs_2_createtables).</span></span>
3. <span data-ttu-id="26144-106">[Popolamento delle tabelle con dati, tramite l'emissione di istruzioni T-SQL INSERT](#cs_3_insert).</span><span class="sxs-lookup"><span data-stu-id="26144-106">[Populates the tables with data, by issuing T-SQL INSERT statements](#cs_3_insert).</span></span>
4. <span data-ttu-id="26144-107">[Aggiornamento dei dati tramite un join](#cs_4_updatejoin).</span><span class="sxs-lookup"><span data-stu-id="26144-107">[Updates data by use of a join](#cs_4_updatejoin).</span></span>
5. <span data-ttu-id="26144-108">[Eliminazione dei dati tramite un join](#cs_5_deletejoin).</span><span class="sxs-lookup"><span data-stu-id="26144-108">[Deletes data by use of a join](#cs_5_deletejoin).</span></span>
6. <span data-ttu-id="26144-109">[Selezione di righe di dati tramite join](#cs_6_selectrows).</span><span class="sxs-lookup"><span data-stu-id="26144-109">[Selects data rows by use of a join](#cs_6_selectrows).</span></span>
7. <span data-ttu-id="26144-110">Chiusura della connessione, con rilascio di eventuali tabelle temporanee da tempdb.</span><span class="sxs-lookup"><span data-stu-id="26144-110">Closes the connection (which drops any temporary tables from tempdb).</span></span>

<span data-ttu-id="26144-111">Il programma C# contiene:</span><span class="sxs-lookup"><span data-stu-id="26144-111">The C# program contains:</span></span>

- <span data-ttu-id="26144-112">Codice C# per la connessione al database.</span><span class="sxs-lookup"><span data-stu-id="26144-112">C# code to connect to the database.</span></span>
- <span data-ttu-id="26144-113">Metodi che restituiscono il codice sorgente di T-SQL.</span><span class="sxs-lookup"><span data-stu-id="26144-113">Methods that return the T-SQL source code.</span></span>
- <span data-ttu-id="26144-114">Due metodi che inviano il codice T-SQL al database.</span><span class="sxs-lookup"><span data-stu-id="26144-114">Two methods that submit the T-SQL to the database.</span></span>

#### <a name="to-compile-and-run"></a><span data-ttu-id="26144-115">Per la compilazione e l'esecuzione</span><span class="sxs-lookup"><span data-stu-id="26144-115">To compile and run</span></span>

<span data-ttu-id="26144-116">Questo programma C# è costituito logicamente da un file con estensione cs.</span><span class="sxs-lookup"><span data-stu-id="26144-116">This C# program is logically one .cs file.</span></span> <span data-ttu-id="26144-117">In questo caso il programma è suddiviso fisicamente in diversi blocchi di codice, in modo da semplificare la visualizzazione e la comprensione di ogni blocco.</span><span class="sxs-lookup"><span data-stu-id="26144-117">But here the program is physically divided into several code blocks, to make each block easier to see and understand.</span></span> <span data-ttu-id="26144-118">Per compilare ed eseguire questo programma, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="26144-118">To compile and run this program, do the following:</span></span>

1. <span data-ttu-id="26144-119">Creare un progetto C# in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26144-119">Create a C# project in Visual Studio.</span></span>
    - <span data-ttu-id="26144-120">Il tipo di progetto deve essere un *console* un'applicazione, da un elemento come la seguente gerarchia: **modelli** > **Visual c#** >  **Windows Desktop classico** > **Console App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="26144-120">The project type should be a *console* application, from something like the following hierarchy: **Templates** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
3. <span data-ttu-id="26144-121">Nel file **Program.cs** cancellare le brevi righe iniziali del codice.</span><span class="sxs-lookup"><span data-stu-id="26144-121">In the file **Program.cs**, erase the small starter lines of code.</span></span>
3. <span data-ttu-id="26144-122">In Program.cs copiare e incollare ogni blocco seguente nella stessa sequenza riportata.</span><span class="sxs-lookup"><span data-stu-id="26144-122">Into Program.cs, copy and paste each of the following blocks, in the same sequence they are presented here.</span></span>
4. <span data-ttu-id="26144-123">In Program.cs modificare i valori seguenti nel metodo **Main**:</span><span class="sxs-lookup"><span data-stu-id="26144-123">In Program.cs, edit the following values in the **Main** method:</span></span>

   - <span data-ttu-id="26144-124">**cb.DataSource**</span><span class="sxs-lookup"><span data-stu-id="26144-124">**cb.DataSource**</span></span>
   - <span data-ttu-id="26144-125">**cd.UserID**</span><span class="sxs-lookup"><span data-stu-id="26144-125">**cd.UserID**</span></span>
   - <span data-ttu-id="26144-126">**cb.Password**</span><span class="sxs-lookup"><span data-stu-id="26144-126">**cb.Password**</span></span>
   - <span data-ttu-id="26144-127">**InitialCatalog**</span><span class="sxs-lookup"><span data-stu-id="26144-127">**InitialCatalog**</span></span>

5. <span data-ttu-id="26144-128">Verificare che sia presente un riferimento all'assembly **System.Data.dll**.</span><span class="sxs-lookup"><span data-stu-id="26144-128">Verify that the assembly **System.Data.dll** is referenced.</span></span> <span data-ttu-id="26144-129">Per la verifica, espandere il nodo **Riferimenti** nel riquadro **Esplora soluzioni**.</span><span class="sxs-lookup"><span data-stu-id="26144-129">To verify, expand the **References** node in the **Solution Explorer** pane.</span></span>
6. <span data-ttu-id="26144-130">Per compilare il programma in Visual Studio, fare clic sul menu **Compila**.</span><span class="sxs-lookup"><span data-stu-id="26144-130">To build the program in Visual Studio, click the **Build** menu.</span></span>
7. <span data-ttu-id="26144-131">Per eseguire il programma da Visual Studio, fare clic sul pulsante **Start**.</span><span class="sxs-lookup"><span data-stu-id="26144-131">To run the program from Visual Studio, click the **Start** button.</span></span> <span data-ttu-id="26144-132">L'output del report viene visualizzato in una finestra di cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="26144-132">The report output is displayed in a cmd.exe window.</span></span>

> [!NOTE]
> <span data-ttu-id="26144-133">È possibile modificare il codice T-SQL per aggiungere un carattere **#** davanti ai nomi di tabella, in modo da crearle come tabelle temporanee in **tempdb**.</span><span class="sxs-lookup"><span data-stu-id="26144-133">You have the option of editing the T-SQL to add a leading **#** to the table names, which creates them as temporary tables in **tempdb**.</span></span> <span data-ttu-id="26144-134">Ciò può risultare utile per finalità dimostrative, quando non sono disponibili database di test.</span><span class="sxs-lookup"><span data-stu-id="26144-134">This can be useful for demonstration purposes, when no test database is available.</span></span> <span data-ttu-id="26144-135">Le tabelle temporanee vengono eliminate automaticamente alla chiusura della connessione.</span><span class="sxs-lookup"><span data-stu-id="26144-135">Temporary tables are deleted automatically when the connection closes.</span></span> <span data-ttu-id="26144-136">Eventuali parole chiave REFERENCES per chiavi esterne non vengono applicate per le tabelle temporanee.</span><span class="sxs-lookup"><span data-stu-id="26144-136">Any REFERENCES for foreign keys are not enforced for temporary tables.</span></span>
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a><span data-ttu-id="26144-137">Blocco C# 1: Connessione tramite ADO.NET</span><span class="sxs-lookup"><span data-stu-id="26144-137">C# block 1: Connect by using ADO.NET</span></span>

- [<span data-ttu-id="26144-138">Avanti</span><span class="sxs-lookup"><span data-stu-id="26144-138">Next</span></span>](#cs_2_createtables)


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
         Console.WriteLine("View the report output here, then press any key to end the program...");
         Console.ReadKey();
      }
```


<a name="cs_2_createtables"/>
### <a name="c-block-2-t-sql-to-create-tables"></a><span data-ttu-id="26144-139">Blocco C# 2: T-SQL per la creazione di tabelle</span><span class="sxs-lookup"><span data-stu-id="26144-139">C# block 2: T-SQL to create tables</span></span>

- <span data-ttu-id="26144-140">[Indietro](#cs_1_connect) &nbsp; / &nbsp; [Avanti](#cs_3_insert)</span><span class="sxs-lookup"><span data-stu-id="26144-140">[Previous](#cs_1_connect) &nbsp; / &nbsp; [Next](#cs_3_insert)</span></span>

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

#### <a name="entity-relationship-diagram-erd"></a><span data-ttu-id="26144-141">Diagramma entità-relazione</span><span class="sxs-lookup"><span data-stu-id="26144-141">Entity Relationship Diagram (ERD)</span></span>

<span data-ttu-id="26144-142">Le istruzioni CREATE TABLE precedenti usano la parola chiave **REFERENCES** per creare una relazione *chiavi esterne* tra le due tabelle.</span><span class="sxs-lookup"><span data-stu-id="26144-142">The preceding CREATE TABLE statements involve the **REFERENCES** keyword to create a *foreign key* (FK) relationship between two tables.</span></span>  <span data-ttu-id="26144-143">Se si usa tempdb, impostare come commento la parola chiave `--REFERENCES` usando una coppia di trattini iniziali.</span><span class="sxs-lookup"><span data-stu-id="26144-143">If you are using tempdb, comment out the `--REFERENCES` keyword using a pair of leading dashes.</span></span>

<span data-ttu-id="26144-144">Il diagramma entità-relazione mostra la relazione tra le due tabelle.</span><span class="sxs-lookup"><span data-stu-id="26144-144">Next is an ERD that displays the relationship between the two tables.</span></span> <span data-ttu-id="26144-145">I valori nella colonna #tabEmployee.DepartmentCode *figlio* sono limitati ai valori presenti nella colonna #tabDepartment.Department *padre*.</span><span class="sxs-lookup"><span data-stu-id="26144-145">The values in the #tabEmployee.DepartmentCode *child* column are limited to the values present in the #tabDepartment.Department *parent* column.</span></span>

![Diagramma entità-relazione che mostra una chiave esterna](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-to-insert-data"></a><span data-ttu-id="26144-147">Blocco C# 3: T-SQL per l'inserimento di dati</span><span class="sxs-lookup"><span data-stu-id="26144-147">C# block 3: T-SQL to insert data</span></span>

- <span data-ttu-id="26144-148">[Indietro](#cs_2_createtables) &nbsp; / &nbsp; [Avanti](#cs_4_updatejoin)</span><span class="sxs-lookup"><span data-stu-id="26144-148">[Previous](#cs_2_createtables) &nbsp; / &nbsp; [Next](#cs_4_updatejoin)</span></span>


```csharp
      static string Build_3_Tsql_Inserts()
      {
         return @"
-- The company has these departments.
INSERT INTO tabDepartment
   (DepartmentCode, DepartmentName)
      VALUES
   ('acct', 'Accounting'),
   ('hres', 'Human Resources'),
   ('legl', 'Legal');

-- The company has these employees, each in one department.
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
### <a name="c-block-4-t-sql-to-update-join"></a><span data-ttu-id="26144-149">Blocco C# 4: T-SQL per l'aggiornamento tramite join</span><span class="sxs-lookup"><span data-stu-id="26144-149">C# block 4: T-SQL to update-join</span></span>

- <span data-ttu-id="26144-150">[Indietro](#cs_3_insert) &nbsp; / &nbsp; [Avanti](#cs_5_deletejoin)</span><span class="sxs-lookup"><span data-stu-id="26144-150">[Previous](#cs_3_insert) &nbsp; / &nbsp; [Next](#cs_5_deletejoin)</span></span>


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
### <a name="c-block-5-t-sql-to-delete-join"></a><span data-ttu-id="26144-151">Blocco C# 5: T-SQL per l'eliminazione tramite join</span><span class="sxs-lookup"><span data-stu-id="26144-151">C# block 5: T-SQL to delete-join</span></span>

- <span data-ttu-id="26144-152">[Indietro](#cs_4_updatejoin) &nbsp; / &nbsp; [Avanti](#cs_6_selectrows)</span><span class="sxs-lookup"><span data-stu-id="26144-152">[Previous](#cs_4_updatejoin) &nbsp; / &nbsp; [Next](#cs_6_selectrows)</span></span>


```csharp
      static string Build_5_Tsql_DeleteJoin()
      {
         return @"
DECLARE @DName2  nvarchar(128);
SET @DName2 = @csharpParmDepartmentName;  --'Legal';


-- Right size the Legal department.
DELETE empl
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName2

-- Disband the Legal department.
DELETE tabDepartment
   WHERE DepartmentName = @DName2;
";
      }
```



<a name="cs_6_selectrows"/>
### <a name="c-block-6-t-sql-to-select-rows"></a><span data-ttu-id="26144-153">Blocco C# 6: T-SQL per la selezione di righe</span><span class="sxs-lookup"><span data-stu-id="26144-153">C# block 6: T-SQL to select rows</span></span>

- <span data-ttu-id="26144-154">[Indietro](#cs_5_deletejoin) &nbsp; / &nbsp; [Avanti](#cs_6b_datareader)</span><span class="sxs-lookup"><span data-stu-id="26144-154">[Previous](#cs_5_deletejoin) &nbsp; / &nbsp; [Next](#cs_6b_datareader)</span></span>


```csharp
      static string Build_6_Tsql_SelectEmployees()
      {
         return @"
-- Look at all the final Employees.
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
### <a name="c-block-6b-executereader"></a><span data-ttu-id="26144-155">Blocco C# 6b: ExecuteReader</span><span class="sxs-lookup"><span data-stu-id="26144-155">C# block 6b: ExecuteReader</span></span>

- <span data-ttu-id="26144-156">[Indietro](#cs_6_selectrows) &nbsp; / &nbsp; [Avanti](#cs_7_executenonquery)</span><span class="sxs-lookup"><span data-stu-id="26144-156">[Previous](#cs_6_selectrows) &nbsp; / &nbsp; [Next](#cs_7_executenonquery)</span></span>

<span data-ttu-id="26144-157">Questo metodo è progettato per l'esecuzione dell'istruzione T-SQL SELECT compilata dal metodo **Build_6_Tsql_SelectEmployees**.</span><span class="sxs-lookup"><span data-stu-id="26144-157">This method is designed to run the T-SQL SELECT statement that is built by the **Build_6_Tsql_SelectEmployees** method.</span></span>


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
### <a name="c-block-7-executenonquery"></a><span data-ttu-id="26144-158">Blocco C# 7: ExecuteNonQuery</span><span class="sxs-lookup"><span data-stu-id="26144-158">C# block 7: ExecuteNonQuery</span></span>

- <span data-ttu-id="26144-159">[Indietro](#cs_6b_datareader) &nbsp; / &nbsp; [Avanti](#cs_8_output)</span><span class="sxs-lookup"><span data-stu-id="26144-159">[Previous](#cs_6b_datareader) &nbsp; / &nbsp; [Next](#cs_8_output)</span></span>

<span data-ttu-id="26144-160">Questo metodo viene chiamato per operazioni che modificano il contenuto dei dati delle tabelle senza restituire alcuna riga di dati.</span><span class="sxs-lookup"><span data-stu-id="26144-160">This method is called for operations that modify the data content of tables without returning any data rows.</span></span>


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
         Console.WriteLine("T-SQL to {0}...", tsqlPurpose);

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
### <a name="c-block-8-actual-test-output-to-the-console"></a><span data-ttu-id="26144-161">Blocco C# 8: Output del test effettivo nella console</span><span class="sxs-lookup"><span data-stu-id="26144-161">C# block 8: Actual test output to the console</span></span>

- [<span data-ttu-id="26144-162">Indietro</span><span class="sxs-lookup"><span data-stu-id="26144-162">Previous</span></span>](#cs_7_executenonquery)

<span data-ttu-id="26144-163">Questa sezione acquisisce l'output inviato dal programma alla console.</span><span class="sxs-lookup"><span data-stu-id="26144-163">This section captures the output that the program sent to the console.</span></span> <span data-ttu-id="26144-164">Solo i valori GUID variano tra le esecuzioni dei test.</span><span class="sxs-lookup"><span data-stu-id="26144-164">Only the guid values vary between test runs.</span></span>


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
