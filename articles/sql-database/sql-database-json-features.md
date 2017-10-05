---
title: "Funzionalità JSON del database SQL di Azure | Documentazione Microsoft"
description: Il database SQL di Azure consente di analizzare, formattare ed eseguire query sui dati nella notazione JavaScript Object Notation (JSON).
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 55860105-2f5f-4b10-87a0-99faa32b5653
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.date: 11/15/2016
ms.author: jovanpop
ms.workload: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 883e661107dd838f5c381cdef2c7f891b9a9389c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a><span data-ttu-id="f623f-103">Introduzione alle funzionalità JSON nel database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="f623f-103">Getting started with JSON features in Azure SQL Database</span></span>
<span data-ttu-id="f623f-104">Il database SQL di Azure consente di analizzare ed eseguire query sui dati rappresentati in formato JavaScript Object Notation [(JSON)](http://www.json.org/) e di esportare i dati relazionali come testo JSON.</span><span class="sxs-lookup"><span data-stu-id="f623f-104">Azure SQL Database lets you parse and query data represented in JavaScript Object Notation [(JSON)](http://www.json.org/) format, and export your relational data as JSON text.</span></span>

<span data-ttu-id="f623f-105">JSON è un formato di dati diffuso usato per scambiare dati nelle moderne applicazioni Web e per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="f623f-105">JSON is a popular data format used for exchanging data in modern web and mobile applications.</span></span> <span data-ttu-id="f623f-106">JSON è usato anche per archiviare dati semistrutturati nei file di log o nei database NoSQL come [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="f623f-106">JSON is also used for storing semi-structured data in log files or in NoSQL databases like [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="f623f-107">Molti servizi Web REST restituiscono risultati formattati come testo JSON o accettano dati formattati come JSON.</span><span class="sxs-lookup"><span data-stu-id="f623f-107">Many REST web services return results formatted as JSON text or accept data formatted as JSON.</span></span> <span data-ttu-id="f623f-108">La maggior parte dei servizi di Azure come [Ricerca di Azure](https://azure.microsoft.com/services/search/), [Archiviazione di Azure](https://azure.microsoft.com/services/storage/) e [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) presentano endpoint REST che restituiscono o usano JSON.</span><span class="sxs-lookup"><span data-stu-id="f623f-108">Most Azure services such as [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), and [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) have REST endpoints that return or consume JSON.</span></span>

<span data-ttu-id="f623f-109">Il database SQL di Azure consente di lavorare facilmente con dati JSON e integrare il database con i servizi moderni.</span><span class="sxs-lookup"><span data-stu-id="f623f-109">Azure SQL Database lets you work with JSON data easily and integrate your database with modern services.</span></span>

## <a name="overview"></a><span data-ttu-id="f623f-110">Overview</span><span class="sxs-lookup"><span data-stu-id="f623f-110">Overview</span></span>
<span data-ttu-id="f623f-111">Il database SQL di Azure fornisce le funzioni seguenti per lavorare con i dati JSON:</span><span class="sxs-lookup"><span data-stu-id="f623f-111">Azure SQL Database provides the following functions for working with JSON data:</span></span>

![Funzioni di JSON](./media/sql-database-json-features/image_1.png)

<span data-ttu-id="f623f-113">Se si dispone di testo JSON, è possibile estrarre dati da JSON o verificare che JSON sia formattato correttamente usando le funzioni predefinite [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx) e [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span><span class="sxs-lookup"><span data-stu-id="f623f-113">If you have JSON text, you can extract data from JSON or verify that JSON is properly formatted by using the built-in functions [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), and [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span></span> <span data-ttu-id="f623f-114">La funzione [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) consente di aggiornare il valore all'interno del testo JSON.</span><span class="sxs-lookup"><span data-stu-id="f623f-114">The [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) function lets you update value inside JSON text.</span></span> <span data-ttu-id="f623f-115">Per query e analisi più avanzate, la funzione [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) può trasformare un array di oggetti JSON in un set di righe.</span><span class="sxs-lookup"><span data-stu-id="f623f-115">For more advanced querying and analysis, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) function can transform an array of JSON objects into a set of rows.</span></span> <span data-ttu-id="f623f-116">È possibile eseguire qualsiasi query SQL sul set di risultati restituito.</span><span class="sxs-lookup"><span data-stu-id="f623f-116">Any SQL query can be executed on the returned result set.</span></span> <span data-ttu-id="f623f-117">Infine, è disponibile una clausola [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) che consente di formattare i dati archiviati nelle tabelle relazionali come testo JSON.</span><span class="sxs-lookup"><span data-stu-id="f623f-117">Finally, there is a [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) clause that lets you format data stored in your relational tables as JSON text.</span></span>

## <a name="formatting-relational-data-in-json-format"></a><span data-ttu-id="f623f-118">Formattazione di dati relazionali in formato JSON</span><span class="sxs-lookup"><span data-stu-id="f623f-118">Formatting relational data in JSON format</span></span>
<span data-ttu-id="f623f-119">Se si dispone di un servizio Web che accetta dati dal livello di database e fornisce una risposta in formato JSON o framework JavaScript sul lato client o raccolte che accettano dati formattati come JSON, è possibile formattare il contenuto del database nel formato JSON direttamente in una query SQL.</span><span class="sxs-lookup"><span data-stu-id="f623f-119">If you have a web service that takes data from the database layer and provides a response in JSON format, or client-side JavaScript frameworks or libraries that accept data formatted as JSON, you can format your database content as JSON directly in a SQL query.</span></span> <span data-ttu-id="f623f-120">Non è più necessario scrivere il codice dell'applicazione che formatta i risultati dal database SQL di Azure come JSON o includere alcune librerie di serializzazione JSON per convertire i risultati della query in formato tabulare e quindi serializzare oggetti in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="f623f-120">You no longer have to write application code that formats results from Azure SQL Database as JSON, or include some JSON serialization library to convert tabular query results and then serialize objects to JSON format.</span></span> <span data-ttu-id="f623f-121">È possibile usare la clausola FOR JSON per formattare i risultati della query SQL come JSON nel database SQL di Azure e usarla direttamente nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f623f-121">Instead, you can use the FOR JSON clause to format SQL query results as JSON in Azure SQL Database and use it directly in your application.</span></span>

<span data-ttu-id="f623f-122">Nell'esempio seguente, le righe della tabella Sales.Customer vengono formattate come JSON usando la clausola FOR JSON:</span><span class="sxs-lookup"><span data-stu-id="f623f-122">In the following example, rows from the Sales.Customer table are formatted as JSON by using the FOR JSON clause:</span></span>

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

<span data-ttu-id="f623f-123">La clausola FOR JSON PATH formatta i risultati della query come testo JSON.</span><span class="sxs-lookup"><span data-stu-id="f623f-123">The FOR JSON PATH clause formats the results of the query as JSON text.</span></span> <span data-ttu-id="f623f-124">I nomi di colonna vengono usati come chiavi, mentre i valori di cella vengono generati come valori JSON:</span><span class="sxs-lookup"><span data-stu-id="f623f-124">Column names are used as keys, while the cell values are generated as JSON values:</span></span>

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

<span data-ttu-id="f623f-125">Il set di risultati viene formattato come array JSON in cui ogni riga viene formattata come un oggetto JSON separato.</span><span class="sxs-lookup"><span data-stu-id="f623f-125">The result set is formatted as a JSON array where each row is formatted as a separate JSON object.</span></span>

<span data-ttu-id="f623f-126">PATH indica che è possibile personalizzare il formato di output del risultato JSON usando la notazione del punto negli alias di colonna.</span><span class="sxs-lookup"><span data-stu-id="f623f-126">PATH indicates that you can customize the output format of your JSON result by using dot notation in column aliases.</span></span> <span data-ttu-id="f623f-127">La query seguente cambia il nome della chiave "CustomerName" nel formato JSON di output e inserisce i numeri di telefono e fax nell'oggetto secondario "Contatto":</span><span class="sxs-lookup"><span data-stu-id="f623f-127">The following query changes the name of the "CustomerName" key in the output JSON format, and puts phone and fax numbers in the "Contact" sub-object:</span></span>

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

<span data-ttu-id="f623f-128">L'output di questa query è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="f623f-128">The output of this query looks like this:</span></span>

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

<span data-ttu-id="f623f-129">In questo esempio viene restituito un singolo oggetto JSON anziché un array, specificando l'opzione [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx).</span><span class="sxs-lookup"><span data-stu-id="f623f-129">In this example we returned a single JSON object instead of an array by specifying the [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span></span> <span data-ttu-id="f623f-130">È possibile usare questa opzione se è noto che si sta restituendo un oggetto singolo come risultato della query.</span><span class="sxs-lookup"><span data-stu-id="f623f-130">You can use this option if you know that you are returning a single object as a result of query.</span></span>

<span data-ttu-id="f623f-131">Il valore principale della clausola FOR JSON è che consente di restituire dati gerarchici complessi dal database formattati come array o oggetti JSON annidati.</span><span class="sxs-lookup"><span data-stu-id="f623f-131">The main value of the FOR JSON clause is that it lets you return complex hierarchical data from your database formatted as nested JSON objects or arrays.</span></span> <span data-ttu-id="f623f-132">Nell'esempio seguente viene illustrato come includere gli ordini che appartengono al cliente come array annidato di ordini:</span><span class="sxs-lookup"><span data-stu-id="f623f-132">The following example shows how to include Orders that belong to the Customer as a nested array of Orders:</span></span>

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

<span data-ttu-id="f623f-133">Anziché inviare query separate per ottenere i dati dei clienti e quindi per recuperare un elenco di ordini correlati, è possibile ottenere tutti i dati necessari con una singola query, come illustrato nel seguente output di esempio:</span><span class="sxs-lookup"><span data-stu-id="f623f-133">Instead of sending separate queries to get Customer data and then to fetch a list of related Orders, you can get all the necessary data with a single query, as shown in the following sample output:</span></span>

```
{
  "Name":"Nada Jovanovic",
  "Phone":"(215) 555-0100",
  "Fax":"(215) 555-0101",
  "Orders":[
    {"OrderID":382,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":395,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":1657,"OrderDate":"2013-01-31","ExpectedDeliveryDate":"2013-02-01"}
]
}
```

## <a name="working-with-json-data"></a><span data-ttu-id="f623f-134">Uso dei dati JSON</span><span class="sxs-lookup"><span data-stu-id="f623f-134">Working with JSON data</span></span>
<span data-ttu-id="f623f-135">Se non si dispone di dati rigorosamente strutturati, se si dispone di oggetti secondari, array o dati gerarchici complessi, oppure se le strutture di dati si evolvono nel tempo, il formato JSON può essere utile per rappresentare una struttura di dati complessa.</span><span class="sxs-lookup"><span data-stu-id="f623f-135">If you don’t have strictly structured data, if you have complex sub-objects, arrays, or hierarchical data, or if your data structures evolve over time, the JSON format can help you to represent any complex data structure.</span></span>

<span data-ttu-id="f623f-136">JSON è un formato testuale che può essere usato come qualsiasi altro tipo di stringa nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="f623f-136">JSON is a textual format that can be used like any other string type in Azure SQL Database.</span></span> <span data-ttu-id="f623f-137">È possibile inviare o archiviare i dati JSON come NVARCHAR standard:</span><span class="sxs-lookup"><span data-stu-id="f623f-137">You can send or store JSON data as a standard NVARCHAR:</span></span>

```
CREATE TABLE Products (
  Id int identity primary key,
  Title nvarchar(200),
  Data nvarchar(max)
)
go
CREATE PROCEDURE InsertProduct(@title nvarchar(200), @json nvarchar(max))
AS BEGIN
    insert into Products(Title, Data)
    values(@title, @json)
END
```

<span data-ttu-id="f623f-138">I dati JSON usati in questo esempio vengono rappresentati con il tipo NVARCHAR(MAX).</span><span class="sxs-lookup"><span data-stu-id="f623f-138">The JSON data used in this example is represented by using the NVARCHAR(MAX) type.</span></span> <span data-ttu-id="f623f-139">Il formato JSON può essere inserito in questa tabella o fornito come argomento della stored procedure usando la sintassi Transact-SQL standard, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f623f-139">JSON can be inserted into this table or provided as an argument of the stored procedure using standard Transact-SQL syntax as shown in the following example:</span></span>

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

<span data-ttu-id="f623f-140">Qualsiasi lingua o raccolta client-side compatibile con i dati della stringa nel database SQL di Azure è compatibile anche con i dati JSON.</span><span class="sxs-lookup"><span data-stu-id="f623f-140">Any client-side language or library that works with string data in Azure SQL Database will also work with JSON data.</span></span> <span data-ttu-id="f623f-141">I dati JSON possono essere archiviati in qualsiasi tabella che supporta il tipo NVARCHAR, ad esempio una tabella con ottimizzazione per la memoria o una tabella con controllo delle versioni del sistema.</span><span class="sxs-lookup"><span data-stu-id="f623f-141">JSON can be stored in any table that supports the NVARCHAR type, such as a Memory-optimized table or a System-versioned table.</span></span> <span data-ttu-id="f623f-142">Il formato JSON non introduce alcun vincolo nel codice lato client o nel livello di database.</span><span class="sxs-lookup"><span data-stu-id="f623f-142">JSON does not introduce any constraint either in the client-side code or in the database layer.</span></span>

## <a name="querying-json-data"></a><span data-ttu-id="f623f-143">Query sui dati JSON</span><span class="sxs-lookup"><span data-stu-id="f623f-143">Querying JSON data</span></span>
<span data-ttu-id="f623f-144">Se si dispone di dati formattati come JSON archiviati in tabelle SQL di Azure, le funzioni JSON consentono di usare i dati in qualsiasi query SQL.</span><span class="sxs-lookup"><span data-stu-id="f623f-144">If you have data formatted as JSON stored in Azure SQL tables, JSON functions let you use this data in any SQL query.</span></span>

<span data-ttu-id="f623f-145">Le funzioni JSON disponibili nel database SQL di Azure consentono di trattare i dati formattati come JSON come qualsiasi altro tipo di dati SQL.</span><span class="sxs-lookup"><span data-stu-id="f623f-145">JSON functions that are available in Azure SQL database let you treat data formatted as JSON as any other SQL data type.</span></span> <span data-ttu-id="f623f-146">È facilmente possibile estrarre i valori dal testo JSON e usare dati JSON in qualsiasi query:</span><span class="sxs-lookup"><span data-stu-id="f623f-146">You can easily extract values from the JSON text, and use JSON data in any query:</span></span>

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

<span data-ttu-id="f623f-147">La funzione JSON_VALUE estrae un valore dal testo JSON archiviato nella colonna Data.</span><span class="sxs-lookup"><span data-stu-id="f623f-147">The JSON_VALUE function extracts a value from JSON text stored in the Data column.</span></span> <span data-ttu-id="f623f-148">Questa funzione usa un percorso in stile JavaScript per fare riferimento a un valore nel testo JSON da estrarre.</span><span class="sxs-lookup"><span data-stu-id="f623f-148">This function uses a JavaScript-like path to reference a value in JSON text to extract.</span></span> <span data-ttu-id="f623f-149">Il valore estratto può essere usato in qualsiasi parte di una query SQL.</span><span class="sxs-lookup"><span data-stu-id="f623f-149">The extracted value can be used in any part of SQL query.</span></span>

<span data-ttu-id="f623f-150">La funzione JSON_QUERY è simile a JSON_VALUE.</span><span class="sxs-lookup"><span data-stu-id="f623f-150">The JSON_QUERY function is similar to JSON_VALUE.</span></span> <span data-ttu-id="f623f-151">A differenza di JSON_VALUE, questa funzione estrae l'oggetto secondario complesso, ad esempio array o oggetti che vengono inseriti nel testo JSON.</span><span class="sxs-lookup"><span data-stu-id="f623f-151">Unlike JSON_VALUE, this function extracts complex sub-object such as arrays or objects that are placed in JSON text.</span></span>

<span data-ttu-id="f623f-152">La funzione JSON_MODIFY consente di specificare il percorso del valore nel testo JSON che deve essere aggiornato, nonché un nuovo valore che sovrascriverà quello precedente.</span><span class="sxs-lookup"><span data-stu-id="f623f-152">The JSON_MODIFY function lets you specify the path of the value in the JSON text that should be updated, as well as a new value that will overwrite the old one.</span></span> <span data-ttu-id="f623f-153">In questo modo è possibile aggiornare facilmente il testo JSON senza ripetere l'analisi dell'intera struttura.</span><span class="sxs-lookup"><span data-stu-id="f623f-153">This way you can easily update JSON text without reparsing the entire structure.</span></span>

<span data-ttu-id="f623f-154">Dal momento che il tasto JSON è archiviato in un testo standard, non vi sono garanzie che i valori archiviati nelle colonne di testo siano formattate correttamente.</span><span class="sxs-lookup"><span data-stu-id="f623f-154">Since JSON is stored in a standard text, there are no guarantees that the values stored in text columns are properly formatted.</span></span> <span data-ttu-id="f623f-155">È possibile verificare che il testo archiviato nella colonna JSON sia formattato correttamente usando i vincoli di controllo standard del database SQL di Azure e la funzione ISJSON:</span><span class="sxs-lookup"><span data-stu-id="f623f-155">You can verify that text stored in JSON column is properly formatted by using standard Azure SQL Database check constraints and the ISJSON function:</span></span>

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

<span data-ttu-id="f623f-156">Se il testo di input è formattato correttamente come JSON, la funzione ISJSON restituisce il valore 1.</span><span class="sxs-lookup"><span data-stu-id="f623f-156">If the input text is properly formatted JSON, the ISJSON function returns the value 1.</span></span> <span data-ttu-id="f623f-157">A ogni inserimento o aggiornamento della colonna JSON, questo vincolo verificherà che nuovo valore di testo non sia un formato JSON non corretto.</span><span class="sxs-lookup"><span data-stu-id="f623f-157">On every insert or update of JSON column, this constraint will verify that new text value is not malformed JSON.</span></span>

## <a name="transforming-json-into-tabular-format"></a><span data-ttu-id="f623f-158">Trasformazione del formato JSON in formato tabulare</span><span class="sxs-lookup"><span data-stu-id="f623f-158">Transforming JSON into tabular format</span></span>
<span data-ttu-id="f623f-159">Il database SQL di Azure consente anche di trasformare gli insiemi JSON in formato tabulare e di caricare o eseguire query sui dati JSON.</span><span class="sxs-lookup"><span data-stu-id="f623f-159">Azure SQL Database also lets you transform JSON collections into tabular format and load or query JSON data.</span></span>

<span data-ttu-id="f623f-160">OPENJSON è una funzione con valori di tabella che analizza il testo JSON, individua un array di oggetti JSON, scorre gli elementi dell'array e restituisce una riga nel risultato di output per ogni elemento dell'array.</span><span class="sxs-lookup"><span data-stu-id="f623f-160">OPENJSON is a table-value function that parses JSON text, locates an array of JSON objects, iterates through the elements of the array, and returns one row in the output result for each element of the array.</span></span>

![JSON tabulare](./media/sql-database-json-features/image_2.png)

<span data-ttu-id="f623f-162">Nell'esempio precedente, è possibile specificare dove si trova l'array JSON da aprire (nel percorso $ Orders), quali colonne devono essere restituite come risultato e dove trovare i valori JSON che verranno restituiti come celle.</span><span class="sxs-lookup"><span data-stu-id="f623f-162">In the example above, we can specify where to locate the JSON array that should be opened (in the $.Orders path), what columns should be returned as result, and where to find the JSON values that will be returned as cells.</span></span>

<span data-ttu-id="f623f-163">È possibile trasformare un array JSON nella variabile @orders in un set di righe, analizzare il set di risultati o inserire righe in una tabella standard:</span><span class="sxs-lookup"><span data-stu-id="f623f-163">We can transform a JSON array in the @orders variable into a set of rows, analyze this result set, or insert rows into a standard table:</span></span>

```
CREATE PROCEDURE InsertOrders(@orders nvarchar(max))
AS BEGIN

    insert into Orders(Number, Date, Customer, Quantity)
    select Number, Date, Customer, Quantity
    OPENJSON (@orders)
     WITH (
            Number varchar(200),
            Date datetime,
            Customer varchar(200),
            Quantity int
     )

END
```
<span data-ttu-id="f623f-164">La raccolta di ordini formattata come array JSON e fornita come parametro alla stored procedure può essere analizzata e inserita nella tabella Orders.</span><span class="sxs-lookup"><span data-stu-id="f623f-164">The collection of orders formatted as a JSON array and provided as a parameter to the stored procedure can be parsed and inserted into the Orders table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f623f-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f623f-165">Next steps</span></span>
<span data-ttu-id="f623f-166">Per informazioni su come integrare JSON nell'applicazione, consultare le seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="f623f-166">To learn how to integrate JSON into your application, check out these resources:</span></span>

* [<span data-ttu-id="f623f-167">Blog di TechNet</span><span class="sxs-lookup"><span data-stu-id="f623f-167">TechNet Blog</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [<span data-ttu-id="f623f-168">Documentazione di MSDN</span><span class="sxs-lookup"><span data-stu-id="f623f-168">MSDN documentation</span></span>](https://msdn.microsoft.com/library/dn921897.aspx)
* [<span data-ttu-id="f623f-169">Video di Channel 9</span><span class="sxs-lookup"><span data-stu-id="f623f-169">Channel 9 video</span></span>](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

<span data-ttu-id="f623f-170">Per altre informazioni sui vari scenari per l'integrazione di JSON nell'applicazione, vedere le dimostrazioni in questo [video di Channel 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) o trovare uno scenario corrispondente al caso d'uso nei [post del blog su JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span><span class="sxs-lookup"><span data-stu-id="f623f-170">To learn about various scenarios for integrating JSON into your application, see the demos in this [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) or find a scenario that matches your use case in [JSON Blog posts](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span></span>

