---
title: "funzionalità di SQL Database JSON aaaAzure | Documenti Microsoft"
description: Database SQL di Azure permette di tooparse, query e dati in formato in notazione JavaScript Object Notation (JSON).
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
ms.openlocfilehash: 30a31a1b01482ec276646b6fd6ca0c1f581168d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a><span data-ttu-id="962dd-103">Introduzione alle funzionalità JSON nel database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="962dd-103">Getting started with JSON features in Azure SQL Database</span></span>
<span data-ttu-id="962dd-104">Il database SQL di Azure consente di analizzare ed eseguire query sui dati rappresentati in formato JavaScript Object Notation [(JSON)](http://www.json.org/) e di esportare i dati relazionali come testo JSON.</span><span class="sxs-lookup"><span data-stu-id="962dd-104">Azure SQL Database lets you parse and query data represented in JavaScript Object Notation [(JSON)](http://www.json.org/) format, and export your relational data as JSON text.</span></span>

<span data-ttu-id="962dd-105">JSON è un formato di dati diffuso usato per scambiare dati nelle moderne applicazioni Web e per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="962dd-105">JSON is a popular data format used for exchanging data in modern web and mobile applications.</span></span> <span data-ttu-id="962dd-106">JSON è usato anche per archiviare dati semistrutturati nei file di log o nei database NoSQL come [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="962dd-106">JSON is also used for storing semi-structured data in log files or in NoSQL databases like [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="962dd-107">Molti servizi Web REST restituiscono risultati formattati come testo JSON o accettano dati formattati come JSON.</span><span class="sxs-lookup"><span data-stu-id="962dd-107">Many REST web services return results formatted as JSON text or accept data formatted as JSON.</span></span> <span data-ttu-id="962dd-108">La maggior parte dei servizi di Azure come [Ricerca di Azure](https://azure.microsoft.com/services/search/), [Archiviazione di Azure](https://azure.microsoft.com/services/storage/) e [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) presentano endpoint REST che restituiscono o usano JSON.</span><span class="sxs-lookup"><span data-stu-id="962dd-108">Most Azure services such as [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), and [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) have REST endpoints that return or consume JSON.</span></span>

<span data-ttu-id="962dd-109">Il database SQL di Azure consente di lavorare facilmente con dati JSON e integrare il database con i servizi moderni.</span><span class="sxs-lookup"><span data-stu-id="962dd-109">Azure SQL Database lets you work with JSON data easily and integrate your database with modern services.</span></span>

## <a name="overview"></a><span data-ttu-id="962dd-110">Panoramica</span><span class="sxs-lookup"><span data-stu-id="962dd-110">Overview</span></span>
<span data-ttu-id="962dd-111">Database SQL di Azure fornisce hello seguenti funzioni per l'utilizzo con i dati JSON:</span><span class="sxs-lookup"><span data-stu-id="962dd-111">Azure SQL Database provides hello following functions for working with JSON data:</span></span>

![Funzioni di JSON](./media/sql-database-json-features/image_1.png)

<span data-ttu-id="962dd-113">Se si dispone di testo JSON, è possibile estrarre dati da JSON o verificare che JSON viene formattato correttamente tramite le funzioni predefinite di hello [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), e [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx) .</span><span class="sxs-lookup"><span data-stu-id="962dd-113">If you have JSON text, you can extract data from JSON or verify that JSON is properly formatted by using hello built-in functions [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), and [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span></span> <span data-ttu-id="962dd-114">Hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) funzione consente di aggiornare valore all'interno del testo JSON.</span><span class="sxs-lookup"><span data-stu-id="962dd-114">hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) function lets you update value inside JSON text.</span></span> <span data-ttu-id="962dd-115">Per query e analisi più avanzate, la funzione [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) può trasformare un array di oggetti JSON in un set di righe.</span><span class="sxs-lookup"><span data-stu-id="962dd-115">For more advanced querying and analysis, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) function can transform an array of JSON objects into a set of rows.</span></span> <span data-ttu-id="962dd-116">Qualsiasi query SQL può essere eseguito in hello restituito set di risultati.</span><span class="sxs-lookup"><span data-stu-id="962dd-116">Any SQL query can be executed on hello returned result set.</span></span> <span data-ttu-id="962dd-117">Infine, è disponibile una clausola [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) che consente di formattare i dati archiviati nelle tabelle relazionali come testo JSON.</span><span class="sxs-lookup"><span data-stu-id="962dd-117">Finally, there is a [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) clause that lets you format data stored in your relational tables as JSON text.</span></span>

## <a name="formatting-relational-data-in-json-format"></a><span data-ttu-id="962dd-118">Formattazione di dati relazionali in formato JSON</span><span class="sxs-lookup"><span data-stu-id="962dd-118">Formatting relational data in JSON format</span></span>
<span data-ttu-id="962dd-119">Se si dispone di un servizio web che richiede dati dal database hello dei livelli e fornisce una risposta in JSON formattare o sul lato client Framework o librerie JavaScript che accettano dati formattati come JSON, è possibile formattare il contenuto del database nel formato JSON direttamente in una query SQL.</span><span class="sxs-lookup"><span data-stu-id="962dd-119">If you have a web service that takes data from hello database layer and provides a response in JSON format, or client-side JavaScript frameworks or libraries that accept data formatted as JSON, you can format your database content as JSON directly in a SQL query.</span></span> <span data-ttu-id="962dd-120">Non sono più codice di applicazione toowrite che formatta i risultati dal Database di SQL Azure come JSON, o includere alcuni risultati delle query tabulari tooconvert libreria serializzazione JSON e quindi serializzare formato tooJSON oggetti.</span><span class="sxs-lookup"><span data-stu-id="962dd-120">You no longer have toowrite application code that formats results from Azure SQL Database as JSON, or include some JSON serialization library tooconvert tabular query results and then serialize objects tooJSON format.</span></span> <span data-ttu-id="962dd-121">In alternativa, è possibile utilizzare hello dei risultati della query SQL tooformat clausola JSON in formato JSON in Database SQL di Azure e utilizzarlo direttamente nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="962dd-121">Instead, you can use hello FOR JSON clause tooformat SQL query results as JSON in Azure SQL Database and use it directly in your application.</span></span>

<span data-ttu-id="962dd-122">Nell'esempio seguente di hello, le righe dalla tabella Sales. Customer hello sono formattate come JSON tramite la clausola FOR JSON hello:</span><span class="sxs-lookup"><span data-stu-id="962dd-122">In hello following example, rows from hello Sales.Customer table are formatted as JSON by using hello FOR JSON clause:</span></span>

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

<span data-ttu-id="962dd-123">clausola FOR JSON PATH Hello formatta i risultati di hello di hello query come testo JSON.</span><span class="sxs-lookup"><span data-stu-id="962dd-123">hello FOR JSON PATH clause formats hello results of hello query as JSON text.</span></span> <span data-ttu-id="962dd-124">I nomi di colonna vengono utilizzati come chiavi, mentre i valori delle celle hello vengono generati come valori JSON:</span><span class="sxs-lookup"><span data-stu-id="962dd-124">Column names are used as keys, while hello cell values are generated as JSON values:</span></span>

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

<span data-ttu-id="962dd-125">set di risultati Hello viene formattato come matrice JSON in cui ogni riga viene formattato come un oggetto JSON separato.</span><span class="sxs-lookup"><span data-stu-id="962dd-125">hello result set is formatted as a JSON array where each row is formatted as a separate JSON object.</span></span>

<span data-ttu-id="962dd-126">PERCORSO indica che è possibile personalizzare il formato di output hello il risultato JSON tramite la notazione del punto nell'alias di colonna.</span><span class="sxs-lookup"><span data-stu-id="962dd-126">PATH indicates that you can customize hello output format of your JSON result by using dot notation in column aliases.</span></span> <span data-ttu-id="962dd-127">Ciao seguente query cambia hello nome della chiave "CustomerName" hello in formato JSON output di hello e inserisce i numeri di telefono e fax in hello "Contact" sotto-oggetto:</span><span class="sxs-lookup"><span data-stu-id="962dd-127">hello following query changes hello name of hello "CustomerName" key in hello output JSON format, and puts phone and fax numbers in hello "Contact" sub-object:</span></span>

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

<span data-ttu-id="962dd-128">output di Hello di questa query è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="962dd-128">hello output of this query looks like this:</span></span>

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

<span data-ttu-id="962dd-129">In questo esempio viene restituito un singolo oggetto JSON invece di una matrice specificando hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) opzione.</span><span class="sxs-lookup"><span data-stu-id="962dd-129">In this example we returned a single JSON object instead of an array by specifying hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span></span> <span data-ttu-id="962dd-130">È possibile usare questa opzione se è noto che si sta restituendo un oggetto singolo come risultato della query.</span><span class="sxs-lookup"><span data-stu-id="962dd-130">You can use this option if you know that you are returning a single object as a result of query.</span></span>

<span data-ttu-id="962dd-131">valore principale Hello hello clausola FOR JSON è che consente di restituire i dati gerarchici complessi dal database formattato come oggetti JSON annidati o matrici.</span><span class="sxs-lookup"><span data-stu-id="962dd-131">hello main value of hello FOR JSON clause is that it lets you return complex hierarchical data from your database formatted as nested JSON objects or arrays.</span></span> <span data-ttu-id="962dd-132">Hello nel seguente esempio viene illustrato come tooinclude ordini appartenenti a clienti toohello come una matrice annidata di ordini:</span><span class="sxs-lookup"><span data-stu-id="962dd-132">hello following example shows how tooinclude Orders that belong toohello Customer as a nested array of Orders:</span></span>

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

<span data-ttu-id="962dd-133">Anziché inviare i dati dei clienti tooget query separate e quindi toofetch un elenco di ordini correlati, è possibile ottenere tutti i dati necessari hello con una singola query, come illustrato nel seguente esempio di output di hello:</span><span class="sxs-lookup"><span data-stu-id="962dd-133">Instead of sending separate queries tooget Customer data and then toofetch a list of related Orders, you can get all hello necessary data with a single query, as shown in hello following sample output:</span></span>

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

## <a name="working-with-json-data"></a><span data-ttu-id="962dd-134">Uso dei dati JSON</span><span class="sxs-lookup"><span data-stu-id="962dd-134">Working with JSON data</span></span>
<span data-ttu-id="962dd-135">Se non è rigorosamente strutturato di dati, se si dispone di oggetti secondari complessi, matrici o i dati gerarchici, o se le strutture di dati cambiano nel tempo, il formato JSON hello consentono toorepresent qualsiasi struttura di dati complessi.</span><span class="sxs-lookup"><span data-stu-id="962dd-135">If you don’t have strictly structured data, if you have complex sub-objects, arrays, or hierarchical data, or if your data structures evolve over time, hello JSON format can help you toorepresent any complex data structure.</span></span>

<span data-ttu-id="962dd-136">JSON è un formato testuale che può essere usato come qualsiasi altro tipo di stringa nel database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="962dd-136">JSON is a textual format that can be used like any other string type in Azure SQL Database.</span></span> <span data-ttu-id="962dd-137">È possibile inviare o archiviare i dati JSON come NVARCHAR standard:</span><span class="sxs-lookup"><span data-stu-id="962dd-137">You can send or store JSON data as a standard NVARCHAR:</span></span>

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

<span data-ttu-id="962dd-138">Hello dati JSON utilizzati in questo esempio è rappresentato con tipo di hello nvarchar (max).</span><span class="sxs-lookup"><span data-stu-id="962dd-138">hello JSON data used in this example is represented by using hello NVARCHAR(MAX) type.</span></span> <span data-ttu-id="962dd-139">JSON può essere inserita in questa tabella o fornito come argomento di routine di hello archiviato utilizzando la sintassi Transact-SQL standard, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="962dd-139">JSON can be inserted into this table or provided as an argument of hello stored procedure using standard Transact-SQL syntax as shown in hello following example:</span></span>

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

<span data-ttu-id="962dd-140">Qualsiasi lingua o raccolta client-side compatibile con i dati della stringa nel database SQL di Azure è compatibile anche con i dati JSON.</span><span class="sxs-lookup"><span data-stu-id="962dd-140">Any client-side language or library that works with string data in Azure SQL Database will also work with JSON data.</span></span> <span data-ttu-id="962dd-141">JSON possono essere archiviati in qualsiasi tabella che supporta i tipi NVARCHAR di hello, ad esempio una tabella con ottimizzazione per la memoria o una tabella con controllo delle versioni del sistema.</span><span class="sxs-lookup"><span data-stu-id="962dd-141">JSON can be stored in any table that supports hello NVARCHAR type, such as a Memory-optimized table or a System-versioned table.</span></span> <span data-ttu-id="962dd-142">JSON non introduce alcun vincolo nel codice sul lato client hello o nel livello di database hello.</span><span class="sxs-lookup"><span data-stu-id="962dd-142">JSON does not introduce any constraint either in hello client-side code or in hello database layer.</span></span>

## <a name="querying-json-data"></a><span data-ttu-id="962dd-143">Query sui dati JSON</span><span class="sxs-lookup"><span data-stu-id="962dd-143">Querying JSON data</span></span>
<span data-ttu-id="962dd-144">Se si dispone di dati formattati come JSON archiviati in tabelle SQL di Azure, le funzioni JSON consentono di usare i dati in qualsiasi query SQL.</span><span class="sxs-lookup"><span data-stu-id="962dd-144">If you have data formatted as JSON stored in Azure SQL tables, JSON functions let you use this data in any SQL query.</span></span>

<span data-ttu-id="962dd-145">Le funzioni JSON disponibili nel database SQL di Azure consentono di trattare i dati formattati come JSON come qualsiasi altro tipo di dati SQL.</span><span class="sxs-lookup"><span data-stu-id="962dd-145">JSON functions that are available in Azure SQL database let you treat data formatted as JSON as any other SQL data type.</span></span> <span data-ttu-id="962dd-146">È facilmente possibile estrarre i valori dal testo JSON hello e utilizzare i dati JSON in qualsiasi query:</span><span class="sxs-lookup"><span data-stu-id="962dd-146">You can easily extract values from hello JSON text, and use JSON data in any query:</span></span>

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

<span data-ttu-id="962dd-147">funzione JSON_VALUE Hello estrae un valore dal testo JSON è archiviato nella colonna di dati hello.</span><span class="sxs-lookup"><span data-stu-id="962dd-147">hello JSON_VALUE function extracts a value from JSON text stored in hello Data column.</span></span> <span data-ttu-id="962dd-148">Questa funzione utilizza tooreference un percorso di tipo JavaScript valore tooextract testo JSON.</span><span class="sxs-lookup"><span data-stu-id="962dd-148">This function uses a JavaScript-like path tooreference a value in JSON text tooextract.</span></span> <span data-ttu-id="962dd-149">il valore di Hello estratto può essere utilizzato in qualsiasi parte della query SQL.</span><span class="sxs-lookup"><span data-stu-id="962dd-149">hello extracted value can be used in any part of SQL query.</span></span>

<span data-ttu-id="962dd-150">funzione JSON_QUERY Hello è tooJSON_VALUE simile.</span><span class="sxs-lookup"><span data-stu-id="962dd-150">hello JSON_QUERY function is similar tooJSON_VALUE.</span></span> <span data-ttu-id="962dd-151">A differenza di JSON_VALUE, questa funzione estrae l'oggetto secondario complesso, ad esempio array o oggetti che vengono inseriti nel testo JSON.</span><span class="sxs-lookup"><span data-stu-id="962dd-151">Unlike JSON_VALUE, this function extracts complex sub-object such as arrays or objects that are placed in JSON text.</span></span>

<span data-ttu-id="962dd-152">funzione JSON_MODIFY Hello consente di specificare il percorso di hello del valore di hello in testo JSON hello che deve essere aggiornato, nonché un nuovo valore sovrascriverà hello precedente.</span><span class="sxs-lookup"><span data-stu-id="962dd-152">hello JSON_MODIFY function lets you specify hello path of hello value in hello JSON text that should be updated, as well as a new value that will overwrite hello old one.</span></span> <span data-ttu-id="962dd-153">In questo modo è possibile aggiornare facilmente testo JSON senza vuoti intera struttura hello.</span><span class="sxs-lookup"><span data-stu-id="962dd-153">This way you can easily update JSON text without reparsing hello entire structure.</span></span>

<span data-ttu-id="962dd-154">Poiché JSON è archiviato in un testo standard, non vi sono garanzie che sono formattati correttamente i valori di hello archiviati nelle colonne di testo.</span><span class="sxs-lookup"><span data-stu-id="962dd-154">Since JSON is stored in a standard text, there are no guarantees that hello values stored in text columns are properly formatted.</span></span> <span data-ttu-id="962dd-155">È possibile verificare che il testo archiviato nella colonna JSON sia formattato correttamente utilizzando standard i vincoli check di Database SQL di Azure e la funzione ISJSON hello:</span><span class="sxs-lookup"><span data-stu-id="962dd-155">You can verify that text stored in JSON column is properly formatted by using standard Azure SQL Database check constraints and hello ISJSON function:</span></span>

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

<span data-ttu-id="962dd-156">Se il testo di input hello è formattato correttamente JSON, hello funzione ISJSON restituisce il valore di hello 1.</span><span class="sxs-lookup"><span data-stu-id="962dd-156">If hello input text is properly formatted JSON, hello ISJSON function returns hello value 1.</span></span> <span data-ttu-id="962dd-157">A ogni inserimento o aggiornamento della colonna JSON, questo vincolo verificherà che nuovo valore di testo non sia un formato JSON non corretto.</span><span class="sxs-lookup"><span data-stu-id="962dd-157">On every insert or update of JSON column, this constraint will verify that new text value is not malformed JSON.</span></span>

## <a name="transforming-json-into-tabular-format"></a><span data-ttu-id="962dd-158">Trasformazione del formato JSON in formato tabulare</span><span class="sxs-lookup"><span data-stu-id="962dd-158">Transforming JSON into tabular format</span></span>
<span data-ttu-id="962dd-159">Il database SQL di Azure consente anche di trasformare gli insiemi JSON in formato tabulare e di caricare o eseguire query sui dati JSON.</span><span class="sxs-lookup"><span data-stu-id="962dd-159">Azure SQL Database also lets you transform JSON collections into tabular format and load or query JSON data.</span></span>

<span data-ttu-id="962dd-160">OPENJSON è una funzione con valori di tabella che analizza il testo JSON, individua una matrice di oggetti JSON, scorre hello gli elementi della matrice hello e restituisce una riga nel risultato di output di hello per ogni elemento della matrice hello.</span><span class="sxs-lookup"><span data-stu-id="962dd-160">OPENJSON is a table-value function that parses JSON text, locates an array of JSON objects, iterates through hello elements of hello array, and returns one row in hello output result for each element of hello array.</span></span>

![JSON tabulare](./media/sql-database-json-features/image_2.png)

<span data-ttu-id="962dd-162">Nell'esempio hello sopra, è possibile specificare dove toolocate hello matrice JSON che deve essere aperte (in $ hello. Il percorso di ordini), le colonne devono essere restituite come risultato e dove toofind hello valori JSON che verranno restituiti come celle.</span><span class="sxs-lookup"><span data-stu-id="962dd-162">In hello example above, we can specify where toolocate hello JSON array that should be opened (in hello $.Orders path), what columns should be returned as result, and where toofind hello JSON values that will be returned as cells.</span></span>

<span data-ttu-id="962dd-163">È possibile trasformare una matrice JSON in hello @orders variabile in un set di righe, analizzare il set di risultati o inserire righe in una tabella standard:</span><span class="sxs-lookup"><span data-stu-id="962dd-163">We can transform a JSON array in hello @orders variable into a set of rows, analyze this result set, or insert rows into a standard table:</span></span>

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
<span data-ttu-id="962dd-164">raccolta di Hello di ordini formattato come matrice JSON e fornito come una stored procedure toohello archiviato parametro può essere analizzata e inserita nella tabella Orders hello.</span><span class="sxs-lookup"><span data-stu-id="962dd-164">hello collection of orders formatted as a JSON array and provided as a parameter toohello stored procedure can be parsed and inserted into hello Orders table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="962dd-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="962dd-165">Next steps</span></span>
<span data-ttu-id="962dd-166">toolearn come toointegrate JSON nell'applicazione, vedere queste risorse:</span><span class="sxs-lookup"><span data-stu-id="962dd-166">toolearn how toointegrate JSON into your application, check out these resources:</span></span>

* [<span data-ttu-id="962dd-167">Blog di TechNet</span><span class="sxs-lookup"><span data-stu-id="962dd-167">TechNet Blog</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [<span data-ttu-id="962dd-168">Documentazione di MSDN</span><span class="sxs-lookup"><span data-stu-id="962dd-168">MSDN documentation</span></span>](https://msdn.microsoft.com/library/dn921897.aspx)
* [<span data-ttu-id="962dd-169">Video di Channel 9</span><span class="sxs-lookup"><span data-stu-id="962dd-169">Channel 9 video</span></span>](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

<span data-ttu-id="962dd-170">toolearn sui vari scenari per l'integrazione JSON nell'applicazione, vedere demo hello in questo [video di Channel 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) o trovare uno scenario che corrisponde al caso di utilizzo in [post di Blog JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span><span class="sxs-lookup"><span data-stu-id="962dd-170">toolearn about various scenarios for integrating JSON into your application, see hello demos in this [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) or find a scenario that matches your use case in [JSON Blog posts](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span></span>

