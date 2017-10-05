---
title: Strumento di migrazione del database per Azure Cosmos DB | Microsoft Docs
description: Informazioni sull'uso degli strumenti open source di migrazione dati di Azure Cosmos DB per importare dati in Azure Cosmos DB da varie origini, tra cui file JSON, CSV, MongoDB, SQL Server, archivio tabelle e Amazon DynamoDB. Conversione da CSV a JSON.
keywords: da csv a json, strumenti di migrazione del database, convertire csv in json
services: cosmos-db
author: andrewhoh
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: d173581d-782a-445c-98d9-5e3c49b00e25
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 23a4a82dbdb611f4da90562af936fca28da9b24d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-data-into-azure-cosmos-db-for-the-documentdb-api"></a><span data-ttu-id="946d0-105">Come importare dati in Azure Cosmos DB per l'API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="946d0-105">How to import data into Azure Cosmos DB for the DocumentDB API?</span></span>

<span data-ttu-id="946d0-106">Questa esercitazione contiene istruzioni per l'uso dello strumento di migrazione dati dell'API DocumentDB di Azure Cosmos DB, che consente di importare dati da varie origini, tra cui file JSON, file CSV, SQL, MongoDB, l'archivio tabelle di Azure, Amazon DynamoDB e raccolte dell'API DocumentDB di Azure Cosmos DB, in raccolte utilizzabili con Azure Cosmos DB e l'API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="946d0-106">This tutorial provides instructions on using the Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and the DocumentDB API.</span></span> <span data-ttu-id="946d0-107">Lo strumento di migrazione dati può essere usato anche per la migrazione da una raccolta con partizione singola a una raccolta con più partizioni per l'API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="946d0-107">The Data Migration tool can also be used when migrating from a single partition collection to a multi-partition collection for the DocumentDB API.</span></span>

<span data-ttu-id="946d0-108">Lo strumento di migrazione dati può essere usato solo per l'importazione in Azure Cosmos DB di dati da usare con l'API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="946d0-108">The Data Migration tool only works when importing data into Azure Cosmos DB for use with the DocumentDB API.</span></span> <span data-ttu-id="946d0-109">L'importazione di dati da usare con l'API Table o l'API Graph non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="946d0-109">Importing data for use with the Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="946d0-110">Per importare dati da usare con l'API MongoDB, vedere l'articolo su [come eseguire la migrazione di dati per l'API MongoDB in Azure Cosmos DB](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="946d0-110">To import data for use with the MongoDB API, see [Azure Cosmos DB: How to migrate data for the MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="946d0-111">Questa esercitazione illustra le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="946d0-111">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="946d0-112">Installazione dello strumento di migrazione dati</span><span class="sxs-lookup"><span data-stu-id="946d0-112">Installing the Data Migration tool</span></span>
> * <span data-ttu-id="946d0-113">Importazione di dati da diverse origini dati</span><span class="sxs-lookup"><span data-stu-id="946d0-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="946d0-114">Esportazione da Azure Cosmos DB a JSON</span><span class="sxs-lookup"><span data-stu-id="946d0-114">Exporting from Azure Cosmos DB to JSON</span></span>

## <span data-ttu-id="946d0-115"><a id="Prerequisites"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="946d0-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="946d0-116">Prima di seguire le istruzioni di questo articolo, verificare che siano installati i seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="946d0-116">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="946d0-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="946d0-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="946d0-118"><a id="Overviewl"></a>Panoramica dello strumento di migrazione dati</span><span class="sxs-lookup"><span data-stu-id="946d0-118"><a id="Overviewl"></a>Overview of the Data Migration tool</span></span>
<span data-ttu-id="946d0-119">Lo strumento di migrazione dati è una soluzione open source che importa dati in Azure Cosmos DB da diverse origini, tra cui:</span><span class="sxs-lookup"><span data-stu-id="946d0-119">The Data Migration tool is an open source solution that imports data to Azure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="946d0-120">File JSON</span><span class="sxs-lookup"><span data-stu-id="946d0-120">JSON files</span></span>
* <span data-ttu-id="946d0-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="946d0-121">MongoDB</span></span>
* <span data-ttu-id="946d0-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="946d0-122">SQL Server</span></span>
* <span data-ttu-id="946d0-123">File CSV</span><span class="sxs-lookup"><span data-stu-id="946d0-123">CSV files</span></span>
* <span data-ttu-id="946d0-124">Archiviazione tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="946d0-124">Azure Table storage</span></span>
* <span data-ttu-id="946d0-125">DynamoDB Amazon</span><span class="sxs-lookup"><span data-stu-id="946d0-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="946d0-126">HBase</span><span class="sxs-lookup"><span data-stu-id="946d0-126">HBase</span></span>
* <span data-ttu-id="946d0-127">Raccolte di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="946d0-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="946d0-128">Lo strumento di importazione, anche se include un'interfaccia utente grafica (dtui.exe), può essere gestito anche dalla riga di comando (dt.exe).</span><span class="sxs-lookup"><span data-stu-id="946d0-128">While the import tool includes a graphical user interface (dtui.exe), it can also be driven from the command line (dt.exe).</span></span> <span data-ttu-id="946d0-129">Infatti, una speciale opzione consente di inviare il comando associato dopo aver configurato un'operazione di importazione nell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="946d0-129">In fact, there is an option to output the associated command after setting up an import through the UI.</span></span> <span data-ttu-id="946d0-130">I dati di origine tabulari (ad esempio, file CSV o SQL Server) possono essere trasformati in modo da poter creare relazioni gerarchiche (documenti secondari) durante l'importazione.</span><span class="sxs-lookup"><span data-stu-id="946d0-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="946d0-131">Continuare a leggere per saperne di più sulle opzioni di origine, sulle righe di comando di esempio per l'importazione da ogni origine, sulle opzioni di destinazione e sulla visualizzazione dei risultati di importazione.</span><span class="sxs-lookup"><span data-stu-id="946d0-131">Keep reading to learn more about source options, sample command lines to import from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="946d0-132"><a id="Install"></a>Installare lo strumento di migrazione dati</span><span class="sxs-lookup"><span data-stu-id="946d0-132"><a id="Install"></a>Install the Data Migration tool</span></span>
<span data-ttu-id="946d0-133">Il codice sorgente dello strumento di migrazione è disponibile su GitHub in [questo repository](https://github.com/azure/azure-documentdb-datamigrationtool) e una versione compilata è disponibile nell'[Area download Microsoft](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span><span class="sxs-lookup"><span data-stu-id="946d0-133">The migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="946d0-134">È possibile compilare la soluzione o semplicemente scaricare ed estrarre la versione compilata nella directory desiderata.</span><span class="sxs-lookup"><span data-stu-id="946d0-134">You may either compile the solution or simply download and extract the compiled version to a directory of your choice.</span></span> <span data-ttu-id="946d0-135">Eseguire quindi:</span><span class="sxs-lookup"><span data-stu-id="946d0-135">Then run either:</span></span>

* <span data-ttu-id="946d0-136">**Dtui.exe**: versione con interfaccia grafica dello strumento</span><span class="sxs-lookup"><span data-stu-id="946d0-136">**Dtui.exe**: Graphical interface version of the tool</span></span>
* <span data-ttu-id="946d0-137">**Dt.exe**: versione con riga di comando dello strumento</span><span class="sxs-lookup"><span data-stu-id="946d0-137">**Dt.exe**: Command-line version of the tool</span></span>

## <a name="import-data"></a><span data-ttu-id="946d0-138">Importa dati</span><span class="sxs-lookup"><span data-stu-id="946d0-138">Import data</span></span>

<span data-ttu-id="946d0-139">Dopo aver installato lo strumento, è necessario importare i dati.</span><span class="sxs-lookup"><span data-stu-id="946d0-139">Once you've installed the tool, it's time to import your data.</span></span> <span data-ttu-id="946d0-140">È possibile importare le tipologie di dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="946d0-140">What kind of data do you want to import?</span></span>

* [<span data-ttu-id="946d0-141">File JSON</span><span class="sxs-lookup"><span data-stu-id="946d0-141">JSON files</span></span>](#JSON)
* [<span data-ttu-id="946d0-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="946d0-142">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="946d0-143">File di esportazione MongoDB</span><span class="sxs-lookup"><span data-stu-id="946d0-143">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="946d0-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="946d0-144">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="946d0-145">File CSV</span><span class="sxs-lookup"><span data-stu-id="946d0-145">CSV files</span></span>](#CSV)
* [<span data-ttu-id="946d0-146">Archivio tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="946d0-146">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="946d0-147">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="946d0-147">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="946d0-148">BLOB</span><span class="sxs-lookup"><span data-stu-id="946d0-148">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="946d0-149">Raccolte di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="946d0-149">Azure Cosmos DB collections</span></span>](#DocumentDBSource)
* [<span data-ttu-id="946d0-150">HBase</span><span class="sxs-lookup"><span data-stu-id="946d0-150">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="946d0-151">Importazione in blocco di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="946d0-151">Azure Cosmos DB bulk import</span></span>](#DocumentDBBulkImport)
* [<span data-ttu-id="946d0-152">Importazione di record sequenziali di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="946d0-152">Azure Cosmos DB sequential record import</span></span>](#DocumentDSeqTarget)


## <span data-ttu-id="946d0-153"><a id="JSON"></a>Per importare file JSON</span><span class="sxs-lookup"><span data-stu-id="946d0-153"><a id="JSON"></a>To import JSON files</span></span>
<span data-ttu-id="946d0-154">L'opzione dell'utilità di importazione dell'origine file JSON consente di importare uno o più file JSON di singoli documenti o file JSON contenenti ciascuno una matrice di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="946d0-154">The JSON file source importer option allows you to import one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="946d0-155">Quando si aggiungono le cartelle contenenti i file JSON da importare, è possibile eseguire una ricerca ricorsiva dei file nelle sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="946d0-155">When adding folders that contain JSON files to import, you have the option of recursively searching for files in subfolders.</span></span>

![Schermata delle opzioni dell'origine file JSON - Strumenti di migrazione del database](./media/import-data/jsonsource.png)

<span data-ttu-id="946d0-157">Ecco alcuni esempi di riga di comando per importare file JSON:</span><span class="sxs-lookup"><span data-stu-id="946d0-157">Here are some command line samples to import JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition the data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <span data-ttu-id="946d0-158"><a id="MongoDB"></a>Per importare da MongoDB</span><span class="sxs-lookup"><span data-stu-id="946d0-158"><a id="MongoDB"></a>To import from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="946d0-159">Se si esegue l'importazione in un account Azure Cosmos DB con supporto per MongoDB, seguire queste [istruzioni](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="946d0-159">If you are importing to an Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="946d0-160">L'opzione dell'utilità di importazione dell'origine MongoDB consente di importare da una singola raccolta MongoDB e, facoltativamente, di filtrare i documenti usando una query e/o di modificare la struttura di documenti usando una proiezione.</span><span class="sxs-lookup"><span data-stu-id="946d0-160">The MongoDB source importer option allows you to import from an individual MongoDB collection and optionally filter documents using a query and/or modify the document structure by using a projection.</span></span>  

![Screenshot delle opzioni relative all'origine per MongoDB](./media/import-data/mongodbsource.png)

<span data-ttu-id="946d0-162">La stringa di connessione è nel formato standard di MongoDB:</span><span class="sxs-lookup"><span data-stu-id="946d0-162">The connection string is in the standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="946d0-163">Usare il comando Verify per assicurarsi che l'istanza di MongoDB specificata nel campo della stringa di connessione sia accessibile.</span><span class="sxs-lookup"><span data-stu-id="946d0-163">Use the Verify command to ensure that the MongoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="946d0-164">Immettere il nome della raccolta da cui verranno importati i dati.</span><span class="sxs-lookup"><span data-stu-id="946d0-164">Enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="946d0-165">Se si preferisce, si può specificare o fornire un file per una query (ad esempio, {pop: {$gt:5000}}) e/o la proiezione (ad esempio, {loc:0}) sia per filtrare che per determinare i dati da importare.</span><span class="sxs-lookup"><span data-stu-id="946d0-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) to both filter and shape the data to be imported.</span></span>

<span data-ttu-id="946d0-166">Ecco alcuni esempi di riga di comando per importare da MongoDB:</span><span class="sxs-lookup"><span data-stu-id="946d0-166">Here are some command line samples to import from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match the query and exclude the loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="946d0-167"><a id="MongoDBExport"></a>Per importare file di esportazione MongoDB</span><span class="sxs-lookup"><span data-stu-id="946d0-167"><a id="MongoDBExport"></a>To import MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="946d0-168">Se si esegue l'importazione in un account Azure Cosmos DB con supporto per MongoDB, seguire queste [istruzioni](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="946d0-168">If you are importing to an Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="946d0-169">L'opzione dell'utilità di importazione dell'origine file JSON di esportazione MongoDB consente di importare uno o più file JSON prodotti dall'utilità mongoexport.</span><span class="sxs-lookup"><span data-stu-id="946d0-169">The MongoDB export JSON file source importer option allows you to import one or more JSON files produced from the mongoexport utility.</span></span>  

![Screenshot delle opzioni relative all'origine per file di esportazione MongoDB](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="946d0-171">Quando si aggiungono le cartelle contenenti i file JSON di esportazione MongoDB da importare, è possibile eseguire una ricerca ricorsiva dei file nelle sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="946d0-171">When adding folders that contain MongoDB export JSON files for import, you have the option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="946d0-172">Ecco un esempio di riga di comando per importare dai file JSON di esportazione MongoDB:</span><span class="sxs-lookup"><span data-stu-id="946d0-172">Here is a command line sample to import from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="946d0-173"><a id="SQL"></a>Per importare da SQL Server</span><span class="sxs-lookup"><span data-stu-id="946d0-173"><a id="SQL"></a>To import from SQL Server</span></span>
<span data-ttu-id="946d0-174">L'opzione dell'utilità di importazione dell'origine SQL consente di importare da un singolo database SQL Server e, facoltativamente, di filtrare i record da importare usando una query.</span><span class="sxs-lookup"><span data-stu-id="946d0-174">The SQL source importer option allows you to import from an individual SQL Server database and optionally filter the records to be imported using a query.</span></span> <span data-ttu-id="946d0-175">Inoltre, è possibile modificare la struttura di documenti specificando un separatore di annidamento, di cui si parlerà tra poco.</span><span class="sxs-lookup"><span data-stu-id="946d0-175">In addition, you can modify the document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Schermata delle opzioni dell'origine SQL - Strumenti di migrazione del database](./media/import-data/sqlexportsource.png)

<span data-ttu-id="946d0-177">Il formato della stringa di connessione è il formato della stringa di connessione SQL standard.</span><span class="sxs-lookup"><span data-stu-id="946d0-177">The format of the connection string is the standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="946d0-178">Usare il comando Verify per assicurarsi che l'istanza di SQL Server specificata nel campo della stringa di connessione sia accessibile.</span><span class="sxs-lookup"><span data-stu-id="946d0-178">Use the Verify command to ensure that the SQL Server instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="946d0-179">La proprietà del separatore di annidamento viene usata per creare relazioni gerarchiche (documenti secondari) durante l'importazione.</span><span class="sxs-lookup"><span data-stu-id="946d0-179">The nesting separator property is used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="946d0-180">Considerare la query SQL seguente:</span><span class="sxs-lookup"><span data-stu-id="946d0-180">Consider the following SQL query:</span></span>

<span data-ttu-id="946d0-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span><span class="sxs-lookup"><span data-stu-id="946d0-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="946d0-182">Che restituisce i risultati (parziali) seguenti:</span><span class="sxs-lookup"><span data-stu-id="946d0-182">Which returns the following (partial) results:</span></span>

![Schermata dei risultati della query SQL](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="946d0-184">Si notino gli alias come Address.AddressType e Address.Location.StateProvinceName.</span><span class="sxs-lookup"><span data-stu-id="946d0-184">Note the aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="946d0-185">Specificando un separatore di annidamento ".", lo strumento di importazione crea i documenti secondari Address e Address.Location durante l'importazione.</span><span class="sxs-lookup"><span data-stu-id="946d0-185">By specifying a nesting separator of ‘.’, the import tool creates Address and Address.Location subdocuments during the import.</span></span> <span data-ttu-id="946d0-186">Ecco un esempio di documento risultante in Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="946d0-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="946d0-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span><span class="sxs-lookup"><span data-stu-id="946d0-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="946d0-188">Ecco alcuni esempi di riga di comando per importare da SQL Server:</span><span class="sxs-lookup"><span data-stu-id="946d0-188">Here are some command line samples to import from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="946d0-189"><a id="CSV"></a>Per importare file CSV ed eseguire la conversione da CSV a JSON</span><span class="sxs-lookup"><span data-stu-id="946d0-189"><a id="CSV"></a>To import CSV files and convert CSV to JSON</span></span>
<span data-ttu-id="946d0-190">L'opzione dell'utilità di importazione dell'origine file CSV consente di importare uno o più file CSV.</span><span class="sxs-lookup"><span data-stu-id="946d0-190">The CSV file source importer option enables you to import one or more CSV files.</span></span> <span data-ttu-id="946d0-191">Quando si aggiungono le cartelle contenenti i file CSV da importare, è possibile eseguire una ricerca ricorsiva dei file nelle sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="946d0-191">When adding folders that contain CSV files for import, you have the option of recursively searching for files in subfolders.</span></span>

![Schermata delle opzioni dell'origine CSV - Da CSV a JSON](media/import-data/csvsource.png)

<span data-ttu-id="946d0-193">Come per l'origine SQL, la proprietà del separatore di annidamento può essere usata per creare relazioni gerarchiche (documenti secondari) durante l'importazione.</span><span class="sxs-lookup"><span data-stu-id="946d0-193">Similar to the SQL source, the nesting separator property may be used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="946d0-194">Si consideri la seguente riga di intestazione CSV e le righe di dati:</span><span class="sxs-lookup"><span data-stu-id="946d0-194">Consider the following CSV header row and data rows:</span></span>

![Schermata dei record di esempio CSV - Da CSV a JSON](./media/import-data/csvsample.png)

<span data-ttu-id="946d0-196">Si notino gli alias come DomainInfo.Domain_Name e RedirectInfo.Redirecting.</span><span class="sxs-lookup"><span data-stu-id="946d0-196">Note the aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="946d0-197">Specificando un separatore di annidamento ".", lo strumento di importazione creerà i documenti secondari DomainInfo e RedirectInfo durante l'importazione.</span><span class="sxs-lookup"><span data-stu-id="946d0-197">By specifying a nesting separator of ‘.’, the import tool will create DomainInfo and RedirectInfo subdocuments during the import.</span></span> <span data-ttu-id="946d0-198">Ecco un esempio di documento risultante in Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="946d0-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="946d0-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span><span class="sxs-lookup"><span data-stu-id="946d0-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="946d0-200">Lo strumento di importazione proverà a dedurre le informazioni sul tipo per i valori non racchiusi tra virgolette nei file CSV (i valori tra virgolette vengono sempre considerati come stringhe).</span><span class="sxs-lookup"><span data-stu-id="946d0-200">The import tool will attempt to infer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="946d0-201">I tipi vengono identificati nell'ordine seguente: tipo numerico, datetime, booleano.</span><span class="sxs-lookup"><span data-stu-id="946d0-201">Types are identified in the following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="946d0-202">Esistono altri due aspetti da considerare per l'importazione CSV:</span><span class="sxs-lookup"><span data-stu-id="946d0-202">There are two other things to note about CSV import:</span></span>

1. <span data-ttu-id="946d0-203">Per impostazione predefinita, nei valori non racchiusi tra virgolette vengono sempre rimossi spazi e tabulazioni, mentre i valori tra virgolette vengono mantenuti così come sono.</span><span class="sxs-lookup"><span data-stu-id="946d0-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="946d0-204">È possibile eseguire l'override di questo comportamento con la casella di controllo Taglia valori tra virgolette o con l'opzione della riga di comando /s.TrimQuoted.</span><span class="sxs-lookup"><span data-stu-id="946d0-204">This behavior can be overridden with the Trim quoted values checkbox or the /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="946d0-205">Per impostazione predefinita, un valore Null non racchiuso tra virgolette viene considerato come valore Null.</span><span class="sxs-lookup"><span data-stu-id="946d0-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="946d0-206">È possibile eseguire l'override di questo comportamento (ad esempio considerando un valore Null non racchiuso tra virgolette come stringa "Null") con la casella di controllo Considera valore NULL non racchiuso tra virgolette come stringa o con l'opzione della riga di comando /s.NoUnquotedNulls.</span><span class="sxs-lookup"><span data-stu-id="946d0-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with the Treat unquoted NULL as string checkbox or the /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="946d0-207">Ecco un esempio di riga di comando per l'importazione CSV:</span><span class="sxs-lookup"><span data-stu-id="946d0-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="946d0-208"><a id="AzureTableSource"></a>Per importare dall'archivio tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="946d0-208"><a id="AzureTableSource"></a>To import from Azure Table storage</span></span>
<span data-ttu-id="946d0-209">L'opzione dell'utilità di importazione dell'origine Archiviazione tabelle di Azure consente di importare da una singola tabella di Archiviazione tabelle di Azure e, facoltativamente, di filtrare le entità tabelle da importare.</span><span class="sxs-lookup"><span data-stu-id="946d0-209">The Azure Table storage source importer option allows you to import from an individual Azure Table storage table and optionally filter the table entities to be imported.</span></span> <span data-ttu-id="946d0-210">Si noti che non è possibile usare lo strumento di migrazione dati per importare in Azure Cosmos DB dati dell'archivio tabelle di Azure da usare con l'API Table.</span><span class="sxs-lookup"><span data-stu-id="946d0-210">Note that you cannot use the Data Migration tool to import Azure Table storage data into Azure Cosmos DB for use with the Table API.</span></span> <span data-ttu-id="946d0-211">L'importazione in Azure Cosmos DB è attualmente supportata solo per l'uso con l'API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="946d0-211">Only importing to Azure Cosmos DB for use with the DocumentDB API is supported at this time.</span></span>

![Schermata delle opzioni dell'origine Archiviazione tabelle di Azure](./media/import-data/azuretablesource.png)

<span data-ttu-id="946d0-213">Il formato della stringa di connessione di Archiviazione tabelle di Azure è:</span><span class="sxs-lookup"><span data-stu-id="946d0-213">The format of the Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="946d0-214">Usare il comando Verify per assicurarsi che l'istanza di Archiviazione tabelle di Azure specificata nel campo della stringa di connessione sia accessibile.</span><span class="sxs-lookup"><span data-stu-id="946d0-214">Use the Verify command to ensure that the Azure Table storage instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="946d0-215">Immettere il nome della tabella di Azure da cui verranno importati i dati.</span><span class="sxs-lookup"><span data-stu-id="946d0-215">Enter the name of the Azure table from which data will be imported.</span></span> <span data-ttu-id="946d0-216">Se si preferisce, si può specificare un [filtro](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="946d0-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="946d0-217">L'opzione dell'utilità di importazione dell'origine Archiviazione tabelle di Azure presenta le seguenti opzioni aggiuntive:</span><span class="sxs-lookup"><span data-stu-id="946d0-217">The Azure Table storage source importer option has the following additional options:</span></span>

1. <span data-ttu-id="946d0-218">Include Internal Fields</span><span class="sxs-lookup"><span data-stu-id="946d0-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="946d0-219">All: include tutti i campi interni (PartitionKey, RowKey e Timestamp)</span><span class="sxs-lookup"><span data-stu-id="946d0-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="946d0-220">None: esclude tutti i campi interni</span><span class="sxs-lookup"><span data-stu-id="946d0-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="946d0-221">RowKey: include solo il campo RowKey</span><span class="sxs-lookup"><span data-stu-id="946d0-221">RowKey - Only include the RowKey field</span></span>
2. <span data-ttu-id="946d0-222">Select Columns</span><span class="sxs-lookup"><span data-stu-id="946d0-222">Select Columns</span></span>
   1. <span data-ttu-id="946d0-223">I filtri di Archiviazione tabelle di Azure non supportano le proiezioni.</span><span class="sxs-lookup"><span data-stu-id="946d0-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="946d0-224">Per importare solo specifiche proprietà delle entità tabelle di Azure, aggiungerle all'elenco Select Columns.</span><span class="sxs-lookup"><span data-stu-id="946d0-224">If you want to only import specific Azure Table entity properties, add them to the Select Columns list.</span></span> <span data-ttu-id="946d0-225">Tutte le altre proprietà delle entità verranno ignorate.</span><span class="sxs-lookup"><span data-stu-id="946d0-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="946d0-226">Ecco un esempio di riga di comando per importare da Archiviazione tabelle di Azure:</span><span class="sxs-lookup"><span data-stu-id="946d0-226">Here is a command line sample to import from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="946d0-227"><a id="DynamoDBSource"></a>Per importare da Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="946d0-227"><a id="DynamoDBSource"></a>To import from Amazon DynamoDB</span></span>
<span data-ttu-id="946d0-228">L'opzione dell'utilità di importazione DynamoDB Amazon origine consente di importare da una singola tabella DynamoDB Amazon e filtrare le entità da importare.</span><span class="sxs-lookup"><span data-stu-id="946d0-228">The Amazon DynamoDB source importer option allows you to import from an individual Amazon DynamoDB table and optionally filter the entities to be imported.</span></span> <span data-ttu-id="946d0-229">Sono disponibili vari modelli in modo che l'impostazione di un'importazione è più semplice possibile.</span><span class="sxs-lookup"><span data-stu-id="946d0-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Schermata delle opzioni dell'origine Amazon DynamoDB - Strumenti di migrazione del database](./media/import-data/dynamodbsource1.png)

![Schermata delle opzioni dell'origine Amazon DynamoDB - Strumenti di migrazione del database](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="946d0-232">Il formato della stringa di connessione DynamoDB di Amazon è:</span><span class="sxs-lookup"><span data-stu-id="946d0-232">The format of the Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="946d0-233">Usare il comando Verify per assicurarsi che l'istanza di MongoDB specificata nel campo della stringa di connessione sia accessibile.</span><span class="sxs-lookup"><span data-stu-id="946d0-233">Use the Verify command to ensure that the Amazon DynamoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="946d0-234">Ecco un esempio di riga di comando per importare da Amazon DynamoDB:</span><span class="sxs-lookup"><span data-stu-id="946d0-234">Here is a command line sample to import from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="946d0-235"><a id="BlobImport"></a>Per importare file dall'archivio BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="946d0-235"><a id="BlobImport"></a>To import files from Azure Blob storage</span></span>
<span data-ttu-id="946d0-236">Il file JSON, i file di esportazione MongoDB e le opzioni dell'utilità di importazione di codice sorgente file CSV consentono di importare uno o più file dall'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="946d0-236">The JSON file, MongoDB export file, and CSV file source importer options allow you to import one or more files from Azure Blob storage.</span></span> <span data-ttu-id="946d0-237">Dopo aver specificato una URL del contenitore Blob e una chiave di Account, è sufficiente fornire un'espressione regolare per selezionare i file da importare.</span><span class="sxs-lookup"><span data-stu-id="946d0-237">After specifying a Blob container URL and Account Key, simply provide a regular expression to select the file(s) to import.</span></span>

![Schermata delle opzioni dell'origine file JSON](./media/import-data/blobsource.png)

<span data-ttu-id="946d0-239">Ecco un esempio di riga di comando per importare file JSON dall'archiviazione Blob di Azure:</span><span class="sxs-lookup"><span data-stu-id="946d0-239">Here is command line sample to import JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="946d0-240"><a id="DocumentDBSource"></a>Per importare da una raccolta dell'API DocumentDB di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="946d0-240"><a id="DocumentDBSource"></a>To import from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="946d0-241">L'opzione dell'utilità di importazione per un'origine Azure Cosmos DB consente di importare dati da una o più raccolte di Azure Cosmos DB e, facoltativamente, filtrare i documenti usando una query.</span><span class="sxs-lookup"><span data-stu-id="946d0-241">The Azure Cosmos DB source importer option allows you to import data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Screenshot delle opzioni relative all'origine per Azure Cosmos DB](./media/import-data/documentdbsource.png)

<span data-ttu-id="946d0-243">Il formato della stringa di connessione di Azure Cosmos DB è il seguente:</span><span class="sxs-lookup"><span data-stu-id="946d0-243">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="946d0-244">La stringa di connessione dell'account Azure Cosmos DB può essere recuperata dal pannello Chiavi del portale di Azure, come descritto in [How to manage an Azure Cosmos DB account](manage-account.md) (Come gestire un account Azure Cosmos DB), ma è necessario aggiungere il nome del database alla stringa di connessione nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="946d0-244">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="946d0-245">Usare il comando Verifica per assicurarsi che l'istanza di Azure Cosmos DB specificata nel campo della stringa di connessione sia accessibile.</span><span class="sxs-lookup"><span data-stu-id="946d0-245">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="946d0-246">Per eseguire l'importazione da una singola raccolta di Azure Cosmos DB, immettere il nome della raccolta da cui verranno importati i dati.</span><span class="sxs-lookup"><span data-stu-id="946d0-246">To import from a single Azure Cosmos DB collection, enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="946d0-247">Per eseguire l'importazione da più raccolte di Azure Cosmos DB, specificare un'espressione regolare corrispondente a uno o più nomi di raccolta (ad esempio, collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="946d0-247">To import from multiple Azure Cosmos DB collections, provide a regular expression to match one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="946d0-248">Se si preferisce, si può specificare o fornire un file per una query sia per filtrare che per determinare i dati da importare.</span><span class="sxs-lookup"><span data-stu-id="946d0-248">You may optionally specify, or provide a file for, a query to both filter and shape the data to be imported.</span></span>

> [!NOTE]
> <span data-ttu-id="946d0-249">Poiché il campo della raccolta accetta le espressioni regolari, se si importa da un'unica raccolta il cui nome contiene caratteri di espressioni regolari, tali caratteri dovranno essere preceduti da un carattere di escape.</span><span class="sxs-lookup"><span data-stu-id="946d0-249">Since the collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="946d0-250">L'opzione dell'utilità di importazione per un'origine Azure Cosmos DB offre le opzioni avanzate seguenti.</span><span class="sxs-lookup"><span data-stu-id="946d0-250">The Azure Cosmos DB source importer option has the following advanced options:</span></span>

1. <span data-ttu-id="946d0-251">Include Internal Fields (Includi campi interni): specifica se includere o meno le proprietà di sistema dei documenti di Azure Cosmos DB (ad esempio, _rid, _ts) nell'esportazione.</span><span class="sxs-lookup"><span data-stu-id="946d0-251">Include Internal Fields: Specifies whether or not to include Azure Cosmos DB document system properties in the export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="946d0-252">Number of Retries on Failure (Numero di tentativi in caso di errore): specifica il numero di tentativi di connessione ad Azure Cosmos DB da effettuare in caso di errori temporanei (ad esempio, un'interruzione della connettività di rete).</span><span class="sxs-lookup"><span data-stu-id="946d0-252">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="946d0-253">Retry Interval (Intervallo tentativi): specifica l'intervallo di attesa tra i tentativi di connessione ad Azure Cosmos DB in caso di errori temporanei (ad esempio, un'interruzione della connettività di rete).</span><span class="sxs-lookup"><span data-stu-id="946d0-253">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="946d0-254">Connection Mode (Modalità connessione): specifica la modalità di connessione da usare con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="946d0-254">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="946d0-255">Le scelte disponibili sono DirectTcp, DirectHttps e Gateway.</span><span class="sxs-lookup"><span data-stu-id="946d0-255">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="946d0-256">Le modalità di connessione diretta sono più veloci, mentre la modalità gateway si integra più facilmente con il firewall perché usa solo la porta 443.</span><span class="sxs-lookup"><span data-stu-id="946d0-256">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Screenshot delle opzioni avanzate per origini Azure Cosmos DB](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="946d0-258">Per impostazione predefinita, la modalità di connessione dello strumento di importazione è DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="946d0-258">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="946d0-259">Se si verificano problemi con il firewall, passare alla modalità di connessione Gateway, che richiede solo la porta 443.</span><span class="sxs-lookup"><span data-stu-id="946d0-259">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="946d0-260">Ecco alcuni esempi di riga di comando per l'importazione da Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="946d0-260">Here are some command line samples to import from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection to another Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections to a single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection to a JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="946d0-261">Lo strumento di importazione dati di Azure Cosmos DB supporta anche l'importazione di dati dall'[emulatore di Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="946d0-261">The Azure Cosmos DB Data Import Tool also supports import of data from the [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="946d0-262">Quando si importano dati da un emulatore locale, impostare l'endpoint `https://localhost:<port>`.</span><span class="sxs-lookup"><span data-stu-id="946d0-262">When importing data from a local emulator, set the endpoint to `https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="946d0-263"><a id="HBaseSource"></a>Per importare da HBase</span><span class="sxs-lookup"><span data-stu-id="946d0-263"><a id="HBaseSource"></a>To import from HBase</span></span>
<span data-ttu-id="946d0-264">L'opzione dell'utilità di importazione HBase origine consente di importare dati da una tabella HBase e filtrare i dati.</span><span class="sxs-lookup"><span data-stu-id="946d0-264">The HBase source importer option allows you to import data from an HBase table and optionally filter the data.</span></span> <span data-ttu-id="946d0-265">Sono disponibili vari modelli in modo che l'impostazione di un'importazione è più semplice possibile.</span><span class="sxs-lookup"><span data-stu-id="946d0-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Schermata di HBase opzioni del codice sorgente](./media/import-data/hbasesource1.png)

![Schermata di HBase opzioni del codice sorgente](./media/import-data/hbasesource2.png)

<span data-ttu-id="946d0-268">Il formato della stringa di connessione HBase Stargate è:</span><span class="sxs-lookup"><span data-stu-id="946d0-268">The format of the HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="946d0-269">Utilizzare il comando verifica per garantire che l'istanza di HBase specificato nel campo della stringa di connessione sia accessibile.ssione sia accessibile.</span><span class="sxs-lookup"><span data-stu-id="946d0-269">Use the Verify command to ensure that the HBase instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="946d0-270">Ecco un esempio di riga di comando per importare da HBase:</span><span class="sxs-lookup"><span data-stu-id="946d0-270">Here is a command line sample to import from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="946d0-271"><a id="DocumentDBBulkTarget"></a>Per importare nell'API DocumentDB (importazione in blocco)</span><span class="sxs-lookup"><span data-stu-id="946d0-271"><a id="DocumentDBBulkTarget"></a>To import to the DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="946d0-272">L'utilità di importazione in blocco di Azure Cosmos DB consente di eseguire l'importazione da qualsiasi opzione di origine disponibile, usando una stored procedure di Azure Cosmos DB per una maggiore efficienza.</span><span class="sxs-lookup"><span data-stu-id="946d0-272">The Azure Cosmos DB Bulk importer allows you to import from any of the available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="946d0-273">Lo strumento supporta l'importazione in una raccolta di Azure Cosmos DB con partizione singola, nonché l'importazione partizionata con partizionamento dei dati in più raccolte di Azure Cosmos DB con partizione singola.</span><span class="sxs-lookup"><span data-stu-id="946d0-273">The tool supports import to one single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="946d0-274">Per altre informazioni sul partizionamento dei dati, vedere l'articolo relativo a [partizionamento e ridimensionamento in Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="946d0-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="946d0-275">Lo strumento creerà, eseguirà e quindi eliminerà la stored procedure dalla raccolta o dalle raccolte di destinazione.</span><span class="sxs-lookup"><span data-stu-id="946d0-275">The tool will create, execute, and then delete the stored procedure from the target collection(s).</span></span>  

![Screenshot delle opzioni relative all'importazione in blocco di Azure Cosmos DB](./media/import-data/documentdbbulk.png)

<span data-ttu-id="946d0-277">Il formato della stringa di connessione di Azure Cosmos DB è il seguente:</span><span class="sxs-lookup"><span data-stu-id="946d0-277">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="946d0-278">La stringa di connessione dell'account Azure Cosmos DB può essere recuperata dal pannello Chiavi del portale di Azure, come descritto in [How to manage an Azure Cosmos DB account](manage-account.md) (Come gestire un account Azure Cosmos DB), ma è necessario aggiungere il nome del database alla stringa di connessione nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="946d0-278">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="946d0-279">Usare il comando Verifica per assicurarsi che l'istanza di Azure Cosmos DB specificata nel campo della stringa di connessione sia accessibile.</span><span class="sxs-lookup"><span data-stu-id="946d0-279">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="946d0-280">Per importare in un'unica raccolta, immettere il nome della raccolta in cui verranno importati i dati e fare clic sul pulsante Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="946d0-280">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="946d0-281">Per importare in più raccolte, immettere il nome di ogni raccolta singolarmente o usare la sintassi seguente per specificare più raccolte: *prefisso_raccolta*[indice iniziale - indice finale].</span><span class="sxs-lookup"><span data-stu-id="946d0-281">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="946d0-282">Quando si specificano più raccolte tramite la sintassi menzionata in precedenza, tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="946d0-282">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="946d0-283">Sono supportati solo criteri di denominazione con intervalli interi.</span><span class="sxs-lookup"><span data-stu-id="946d0-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="946d0-284">Ad esempio, se si specifica collection[0-3], verranno restituite le raccolte seguenti: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="946d0-284">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="946d0-285">È possibile usare una sintassi abbreviata: collection[3] restituirà lo stesso set di raccolte citato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="946d0-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="946d0-286">È possibile specificare più di una sostituzione.</span><span class="sxs-lookup"><span data-stu-id="946d0-286">More than one substitution can be provided.</span></span> <span data-ttu-id="946d0-287">Ad esempio, collection[0-1] [0-9] genererà 20 nomi di raccolte con zeri iniziali (collection01, ..02, ..03).</span><span class="sxs-lookup"><span data-stu-id="946d0-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="946d0-288">Dopo aver specificato il nome della raccolta, scegliere la velocità effettiva desiderata della raccolta, da 400 UR a 10.000 UR.</span><span class="sxs-lookup"><span data-stu-id="946d0-288">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 10,000 RUs).</span></span> <span data-ttu-id="946d0-289">Per ottimizzare le prestazioni di importazione, scegliere una velocità effettiva superiore.</span><span class="sxs-lookup"><span data-stu-id="946d0-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="946d0-290">Per altre informazioni sui livelli di prestazioni, vedere l'articolo relativo ai [livelli di prestazioni in Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="946d0-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="946d0-291">L'impostazione della velocità effettiva delle prestazioni si applica solo alla creazione di raccolte.</span><span class="sxs-lookup"><span data-stu-id="946d0-291">The performance throughput setting only applies to collection creation.</span></span> <span data-ttu-id="946d0-292">Se la raccolta specificata esiste già, la velocità effettiva non verrà modificata.</span><span class="sxs-lookup"><span data-stu-id="946d0-292">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="946d0-293">Quando si importa in più raccolte, lo strumento di importazione supporta il partizionamento orizzontale basato su hash.</span><span class="sxs-lookup"><span data-stu-id="946d0-293">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="946d0-294">In questo scenario, specificare la proprietà di documento da usare come chiave di partizione (se la chiave di partizione viene lasciata vuota, i documenti verranno partizionati in modo casuale tra le raccolte di destinazione).</span><span class="sxs-lookup"><span data-stu-id="946d0-294">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="946d0-295">Facoltativamente, è possibile specificare il campo dell'origine di importazione da usare come proprietà ID del documento di Azure Cosmos DB durante l'importazione. Se i documenti non contengono questa proprietà, lo strumento di importazione genererà un GUID come valore della proprietà ID.</span><span class="sxs-lookup"><span data-stu-id="946d0-295">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="946d0-296">Durante l'importazione sono disponibili numerose opzioni avanzate.</span><span class="sxs-lookup"><span data-stu-id="946d0-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="946d0-297">Innanzitutto, anche se lo strumento include una stored procedure di importazione in blocco predefinita (BulkInsert.js), è possibile scegliere di specificare la propria stored procedure di importazione:</span><span class="sxs-lookup"><span data-stu-id="946d0-297">First, while the tool includes a default bulk import stored procedure (BulkInsert.js), you may choose to specify your own import stored procedure:</span></span>

 ![Screenshot dell'opzione relativa alla stored procedure di inserimento in blocco per Azure Cosmos DB](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="946d0-299">Inoltre, quando si importano i tipi di data (ad esempio, da SQL Server o MongoDB), è possibile scegliere tra tre opzioni di importazione:</span><span class="sxs-lookup"><span data-stu-id="946d0-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Screenshot delle opzioni di importazione relative a data e ora per Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="946d0-301">String: persiste come valore di stringa.</span><span class="sxs-lookup"><span data-stu-id="946d0-301">String: Persist as a string value</span></span>
* <span data-ttu-id="946d0-302">Epoch: persiste come valore numerico di periodo.</span><span class="sxs-lookup"><span data-stu-id="946d0-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="946d0-303">Both: persiste come valore di stringa e numerico di periodo.</span><span class="sxs-lookup"><span data-stu-id="946d0-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="946d0-304">Questa opzione creerà un documento secondario, ad esempio: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="946d0-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="946d0-305">L'utilità di importazione in blocco di Azure Cosmos DB offre le opzioni avanzate aggiuntive seguenti.</span><span class="sxs-lookup"><span data-stu-id="946d0-305">The Azure Cosmos DB Bulk importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="946d0-306">Batch Size: per impostazione predefinita, le dimensioni batch dello strumento sono pari a 50.</span><span class="sxs-lookup"><span data-stu-id="946d0-306">Batch Size: The tool defaults to a batch size of 50.</span></span>  <span data-ttu-id="946d0-307">Se i documenti da importare sono di grandi dimensioni, provare a ridurre le dimensioni batch.</span><span class="sxs-lookup"><span data-stu-id="946d0-307">If the documents to be imported are large, consider lowering the batch size.</span></span> <span data-ttu-id="946d0-308">Se invece i documenti da importare sono di piccole dimensioni, provare ad aumentare le dimensioni batch.</span><span class="sxs-lookup"><span data-stu-id="946d0-308">Conversely, if the documents to be imported are small, consider raising the batch size.</span></span>
2. <span data-ttu-id="946d0-309">Max Script Size (bytes): per impostazione predefinita, le dimensioni script massime dello strumento sono pari a 512 KB</span><span class="sxs-lookup"><span data-stu-id="946d0-309">Max Script Size (bytes): The tool defaults to a max script size of 512KB</span></span>
3. <span data-ttu-id="946d0-310">Disable Automatic Id Generation: se ogni documento da importare contiene un campo ID, selezionando questa opzione, le prestazioni possono migliorare.</span><span class="sxs-lookup"><span data-stu-id="946d0-310">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="946d0-311">I documenti in cui manca un campo ID univoco non verranno importati.</span><span class="sxs-lookup"><span data-stu-id="946d0-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="946d0-312">Update Existing Documents: per impostazione predefinita, lo strumento non sostituisce i documenti esistenti con conflitti tra ID.</span><span class="sxs-lookup"><span data-stu-id="946d0-312">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="946d0-313">Questa opzione consentirà di sovrascrivere i documenti esistenti con ID corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="946d0-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="946d0-314">Questa funzionalità è utile per le migrazioni dei dati pianificate che aggiornano i documenti esistenti.</span><span class="sxs-lookup"><span data-stu-id="946d0-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="946d0-315">Number of Retries on Failure (Numero di tentativi in caso di errore): specifica il numero di tentativi di connessione ad Azure Cosmos DB da effettuare in caso di errori temporanei (ad esempio, un'interruzione della connettività di rete).</span><span class="sxs-lookup"><span data-stu-id="946d0-315">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="946d0-316">Retry Interval (Intervallo tentativi): specifica l'intervallo di attesa tra i tentativi di connessione ad Azure Cosmos DB in caso di errori temporanei (ad esempio, un'interruzione della connettività di rete).</span><span class="sxs-lookup"><span data-stu-id="946d0-316">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="946d0-317">Connection Mode (Modalità connessione): specifica la modalità di connessione da usare con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="946d0-317">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="946d0-318">Le scelte disponibili sono DirectTcp, DirectHttps e Gateway.</span><span class="sxs-lookup"><span data-stu-id="946d0-318">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="946d0-319">Le modalità di connessione diretta sono più veloci, mentre la modalità gateway si integra più facilmente con il firewall perché usa solo la porta 443.</span><span class="sxs-lookup"><span data-stu-id="946d0-319">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Screenshot delle opzioni avanzate di importazione in blocco di Azure Cosmos DB](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="946d0-321">Per impostazione predefinita, la modalità di connessione dello strumento di importazione è DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="946d0-321">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="946d0-322">Se si verificano problemi con il firewall, passare alla modalità di connessione Gateway, che richiede solo la porta 443.</span><span class="sxs-lookup"><span data-stu-id="946d0-322">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="946d0-323"><a id="DocumentDBSeqTarget"></a>Per importare nell'API DocumentDB (importazione di record sequenziali)</span><span class="sxs-lookup"><span data-stu-id="946d0-323"><a id="DocumentDBSeqTarget"></a>To import to the DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="946d0-324">L'utilità di importazione di record sequenziali di Azure Cosmos DB consente di importare un record alla volta da qualsiasi opzione di origine disponibile.</span><span class="sxs-lookup"><span data-stu-id="946d0-324">The Azure Cosmos DB sequential record importer allows you to import from any of the available source options on a record by record basis.</span></span> <span data-ttu-id="946d0-325">È possibile scegliere questa opzione se si sta importando in una raccolta esistente che ha raggiunto la quota di stored procedure.</span><span class="sxs-lookup"><span data-stu-id="946d0-325">You might choose this option if you’re importing to an existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="946d0-326">Lo strumento supporta l'importazione in un'unica raccolta di Azure Cosmos DB, sia con partizione singola che con più partizioni, nonché l'importazione partizionata con partizionamento dei dati in più raccolte di Azure Cosmos DB con partizione singola e/o con più partizioni.</span><span class="sxs-lookup"><span data-stu-id="946d0-326">The tool supports import to a single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="946d0-327">Per altre informazioni sul partizionamento dei dati, vedere l'articolo relativo a [partizionamento e ridimensionamento in Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="946d0-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Screenshot delle opzioni di importazione di record sequenziali per Azure Cosmos DB](./media/import-data/documentdbsequential.png)

<span data-ttu-id="946d0-329">Il formato della stringa di connessione di Azure Cosmos DB è il seguente:</span><span class="sxs-lookup"><span data-stu-id="946d0-329">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="946d0-330">La stringa di connessione dell'account Azure Cosmos DB può essere recuperata dal pannello Chiavi del portale di Azure, come descritto in [How to manage an Azure Cosmos DB account](manage-account.md) (Come gestire un account Azure Cosmos DB), ma è necessario aggiungere il nome del database alla stringa di connessione nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="946d0-330">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="946d0-331">Usare il comando Verifica per assicurarsi che l'istanza di Azure Cosmos DB specificata nel campo della stringa di connessione sia accessibile.</span><span class="sxs-lookup"><span data-stu-id="946d0-331">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="946d0-332">Per importare in un'unica raccolta, immettere il nome della raccolta in cui verranno importati i dati e fare clic sul pulsante Aggiungi.</span><span class="sxs-lookup"><span data-stu-id="946d0-332">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="946d0-333">Per importare in più raccolte, immettere il nome di ogni raccolta singolarmente o usare la sintassi seguente per specificare più raccolte: *prefisso_raccolta*[indice iniziale - indice finale].</span><span class="sxs-lookup"><span data-stu-id="946d0-333">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="946d0-334">Quando si specificano più raccolte tramite la sintassi menzionata in precedenza, tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="946d0-334">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="946d0-335">Sono supportati solo criteri di denominazione con intervalli interi.</span><span class="sxs-lookup"><span data-stu-id="946d0-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="946d0-336">Ad esempio, se si specifica collection[0-3], verranno restituite le raccolte seguenti: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="946d0-336">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="946d0-337">È possibile usare una sintassi abbreviata: collection[3] restituirà lo stesso set di raccolte citato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="946d0-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="946d0-338">È possibile specificare più di una sostituzione.</span><span class="sxs-lookup"><span data-stu-id="946d0-338">More than one substitution can be provided.</span></span> <span data-ttu-id="946d0-339">Ad esempio, collection[0-1] [0-9] genererà 20 nomi di raccolte con zeri iniziali (collection01, ..02, ..03).</span><span class="sxs-lookup"><span data-stu-id="946d0-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="946d0-340">Dopo aver specificato il nome della raccolta, scegliere la velocità effettiva desiderata della raccolta, da 400 UR a 250.000 UR.</span><span class="sxs-lookup"><span data-stu-id="946d0-340">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 250,000 RUs).</span></span> <span data-ttu-id="946d0-341">Per ottimizzare le prestazioni di importazione, scegliere una velocità effettiva superiore.</span><span class="sxs-lookup"><span data-stu-id="946d0-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="946d0-342">Per altre informazioni sui livelli di prestazioni, vedere l'articolo relativo ai [livelli di prestazioni in Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="946d0-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="946d0-343">Eventuali importazioni nelle raccolte con una velocità effettiva > 10.000 UR richiederanno una chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="946d0-343">Any import to collections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="946d0-344">Se si sceglie di avere più di 250.000 UR, sarà necessario inviare una richiesta di nel portale per incrementare l'account.</span><span class="sxs-lookup"><span data-stu-id="946d0-344">If you choose to have more than 250,000 RUs, you will need to file a request in the portal to have your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="946d0-345">L'impostazione della velocità effettiva si applica solo alla creazione di raccolte.</span><span class="sxs-lookup"><span data-stu-id="946d0-345">The throughput setting only applies to collection creation.</span></span> <span data-ttu-id="946d0-346">Se la raccolta specificata esiste già, la velocità effettiva non verrà modificata.</span><span class="sxs-lookup"><span data-stu-id="946d0-346">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="946d0-347">Quando si importa in più raccolte, lo strumento di importazione supporta il partizionamento orizzontale basato su hash.</span><span class="sxs-lookup"><span data-stu-id="946d0-347">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="946d0-348">In questo scenario, specificare la proprietà di documento da usare come chiave di partizione (se la chiave di partizione viene lasciata vuota, i documenti verranno partizionati in modo casuale tra le raccolte di destinazione).</span><span class="sxs-lookup"><span data-stu-id="946d0-348">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="946d0-349">Facoltativamente, è possibile specificare il campo dell'origine di importazione da usare come proprietà ID del documento di Azure Cosmos DB durante l'importazione. Se i documenti non contengono questa proprietà, lo strumento di importazione genererà un GUID come valore della proprietà ID.</span><span class="sxs-lookup"><span data-stu-id="946d0-349">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="946d0-350">Durante l'importazione sono disponibili numerose opzioni avanzate.</span><span class="sxs-lookup"><span data-stu-id="946d0-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="946d0-351">Innanzitutto, quando si importano i tipi di data (ad esempio, da SQL Server o MongoDB), è possibile scegliere tra tre opzioni di importazione:</span><span class="sxs-lookup"><span data-stu-id="946d0-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Screenshot delle opzioni di importazione relative a data e ora per Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="946d0-353">String: persiste come valore di stringa.</span><span class="sxs-lookup"><span data-stu-id="946d0-353">String: Persist as a string value</span></span>
* <span data-ttu-id="946d0-354">Epoch: persiste come valore numerico di periodo.</span><span class="sxs-lookup"><span data-stu-id="946d0-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="946d0-355">Both: persiste come valore di stringa e numerico di periodo.</span><span class="sxs-lookup"><span data-stu-id="946d0-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="946d0-356">Questa opzione creerà un documento secondario, ad esempio: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="946d0-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="946d0-357">L'utilità di importazione di record sequenziali di Azure Cosmos DB offre le opzioni avanzate aggiuntive seguenti.</span><span class="sxs-lookup"><span data-stu-id="946d0-357">The Azure Cosmos DB - Sequential record importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="946d0-358">Number of Parallel Requests: per impostazione predefinita, nello strumento le richieste parallele sono 2.</span><span class="sxs-lookup"><span data-stu-id="946d0-358">Number of Parallel Requests: The tool defaults to 2 parallel requests.</span></span> <span data-ttu-id="946d0-359">Se i documenti da importare sono di piccole dimensioni, provare ad aumentare il numero di richieste parallele.</span><span class="sxs-lookup"><span data-stu-id="946d0-359">If the documents to be imported are small, consider raising the number of parallel requests.</span></span> <span data-ttu-id="946d0-360">Si noti che, se questo numero è troppo alto, durante l'importazione potrebbe venire applicata la limitazione delle richieste.</span><span class="sxs-lookup"><span data-stu-id="946d0-360">Note that if this number is raised too much, the import may experience throttling.</span></span>
2. <span data-ttu-id="946d0-361">Disable Automatic Id Generation: se ogni documento da importare contiene un campo ID, selezionando questa opzione, le prestazioni possono migliorare.</span><span class="sxs-lookup"><span data-stu-id="946d0-361">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="946d0-362">I documenti in cui manca un campo ID univoco non verranno importati.</span><span class="sxs-lookup"><span data-stu-id="946d0-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="946d0-363">Update Existing Documents: per impostazione predefinita, lo strumento non sostituisce i documenti esistenti con conflitti tra ID.</span><span class="sxs-lookup"><span data-stu-id="946d0-363">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="946d0-364">Questa opzione consentirà di sovrascrivere i documenti esistenti con ID corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="946d0-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="946d0-365">Questa funzionalità è utile per le migrazioni dei dati pianificate che aggiornano i documenti esistenti.</span><span class="sxs-lookup"><span data-stu-id="946d0-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="946d0-366">Number of Retries on Failure (Numero di tentativi in caso di errore): specifica il numero di tentativi di connessione ad Azure Cosmos DB da effettuare in caso di errori temporanei (ad esempio, un'interruzione della connettività di rete).</span><span class="sxs-lookup"><span data-stu-id="946d0-366">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="946d0-367">Retry Interval (Intervallo tentativi): specifica l'intervallo di attesa tra i tentativi di connessione ad Azure Cosmos DB in caso di errori temporanei (ad esempio, un'interruzione della connettività di rete).</span><span class="sxs-lookup"><span data-stu-id="946d0-367">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="946d0-368">Connection Mode (Modalità connessione): specifica la modalità di connessione da usare con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="946d0-368">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="946d0-369">Le scelte disponibili sono DirectTcp, DirectHttps e Gateway.</span><span class="sxs-lookup"><span data-stu-id="946d0-369">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="946d0-370">Le modalità di connessione diretta sono più veloci, mentre la modalità gateway si integra più facilmente con il firewall perché usa solo la porta 443.</span><span class="sxs-lookup"><span data-stu-id="946d0-370">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Screenshot delle opzioni avanzate di importazione di record sequenziali di Azure Cosmos DB](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="946d0-372">Per impostazione predefinita, la modalità di connessione dello strumento di importazione è DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="946d0-372">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="946d0-373">Se si verificano problemi con il firewall, passare alla modalità di connessione Gateway, che richiede solo la porta 443.</span><span class="sxs-lookup"><span data-stu-id="946d0-373">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="946d0-374"><a id="IndexingPolicy"></a>Specificare un criterio di indicizzazione durante la creazione di raccolte di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="946d0-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="946d0-375">Quando si consente all'utilità di migrazione di creare raccolte durante l'importazione, è possibile specificare i criteri di indicizzazione delle raccolte.</span><span class="sxs-lookup"><span data-stu-id="946d0-375">When you allow the migration tool to create collections during import, you can specify the indexing policy of the collections.</span></span> <span data-ttu-id="946d0-376">Nella sezione delle opzioni avanzate per l'importazione in blocco e l'importazione di record sequenziali di Azure Cosmos DB, passare alla sezione relativa ai criteri di indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="946d0-376">In the advanced options section of the Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate to the Indexing Policy section.</span></span>

![Screenshot delle opzioni avanzate relative ai criteri di indicizzazione di Azure Cosmos DB](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="946d0-378">Utilizzando i criteri di indicizzazione opzione avanzata, è possibile selezionare un file di criteri di indicizzazione, manualmente immettere un criterio di indicizzazione o selezionare da un set di modelli predefiniti (facendo clic nella casella di testo di indicizzazione criteri destro).</span><span class="sxs-lookup"><span data-stu-id="946d0-378">Using the Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in the indexing policy textbox).</span></span>

<span data-ttu-id="946d0-379">I modelli dei criteri che lo strumento fornisce sono:</span><span class="sxs-lookup"><span data-stu-id="946d0-379">The policy templates the tool provides are:</span></span>

* <span data-ttu-id="946d0-380">Default.</span><span class="sxs-lookup"><span data-stu-id="946d0-380">Default.</span></span> <span data-ttu-id="946d0-381">Questo criterio è migliore quando si eseguono query di uguaglianza su stringhe e utilizzando ORDER BY, l'intervallo e le query di uguaglianza per i numeri.</span><span class="sxs-lookup"><span data-stu-id="946d0-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="946d0-382">Questo criterio ha un overhead di archiviazione indice inferiore rispetto a intervallo.</span><span class="sxs-lookup"><span data-stu-id="946d0-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="946d0-383">Intervallo.</span><span class="sxs-lookup"><span data-stu-id="946d0-383">Range.</span></span> <span data-ttu-id="946d0-384">Questo criterio è consigliabile quando si sta utilizzando query ORDER BY, intervallo e uguaglianza su stringhe e numeri.</span><span class="sxs-lookup"><span data-stu-id="946d0-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="946d0-385">Questo criterio ha un overhead di archiviazione indice superiore rispetto a predefinito o Hash.</span><span class="sxs-lookup"><span data-stu-id="946d0-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Screenshot delle opzioni avanzate relative ai criteri di indicizzazione di Azure Cosmos DB](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="946d0-387">Se non si specifica un criterio di indicizzazione, verrà applicato il criterio predefinito.</span><span class="sxs-lookup"><span data-stu-id="946d0-387">If you do not specify an indexing policy, then the default policy will be applied.</span></span> <span data-ttu-id="946d0-388">Per altre informazioni sui criteri di indicizzazione, vedere l'articolo relativo ai [criteri di indicizzazione di Azure Cosmos DB](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="946d0-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-to-json-file"></a><span data-ttu-id="946d0-389">Esportare in file JSON</span><span class="sxs-lookup"><span data-stu-id="946d0-389">Export to JSON file</span></span>
<span data-ttu-id="946d0-390">L'utilità di esportazione JSON di Azure Cosmos DB consente di esportare qualsiasi opzione di origine disponibile in un file JSON contenente una matrice di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="946d0-390">The Azure Cosmos DB JSON exporter allows you to export any of the available source options to a JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="946d0-391">Sarà lo strumento a gestire l'esportazione, ma è anche possibile scegliere di visualizzare il comando di migrazione risultante ed eseguire il comando manualmente.</span><span class="sxs-lookup"><span data-stu-id="946d0-391">The tool will handle the export for you, or you can choose to view the resulting migration command and run the command yourself.</span></span> <span data-ttu-id="946d0-392">Il file JSON risultante può essere archiviato in locale o nel servizio di archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="946d0-392">The resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Screenshot dell'opzione di esportazione in file JSON locale di Azure Cosmos DB](./media/import-data/jsontarget.png)

![Screenshot dell'opzione di esportazione in file JSON in un archivio BLOB di Azure di Azure Cosmos DB](./media/import-data/jsontarget2.png)

<span data-ttu-id="946d0-395">Se si preferisce, si può scegliere di modificare il file JSON risultante, aumentando così le dimensioni del documento risultante e rendendone il contenuto più leggibile.</span><span class="sxs-lookup"><span data-stu-id="946d0-395">You may optionally choose to prettify the resulting JSON, which will increase the size of the resulting document while making the contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places to see in Paris"}]}]

    Prettified JSON export
    [
     {
    "id": "Sample",
    "Title": "About Paris",
    "Language": {
      "Name": "English"
    },
    "Author": {
      "Name": "Don",
      "Location": {
        "City": "Paris",
        "Country": "France"
      }
    },
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places to see in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="946d0-396">Configurazione avanzata</span><span class="sxs-lookup"><span data-stu-id="946d0-396">Advanced configuration</span></span>
<span data-ttu-id="946d0-397">Nella schermata Configurazione avanzata specificare il percorso del file di log in cui scrivere gli errori.</span><span class="sxs-lookup"><span data-stu-id="946d0-397">In the Advanced configuration screen, specify the location of the log file to which you would like any errors written.</span></span> <span data-ttu-id="946d0-398">In questa pagina vengono applicate le regole seguenti:</span><span class="sxs-lookup"><span data-stu-id="946d0-398">The following rules apply to this page:</span></span>

1. <span data-ttu-id="946d0-399">Se non viene fornito un nome di file, tutti gli errori verranno restituiti nella pagina dei risultati.</span><span class="sxs-lookup"><span data-stu-id="946d0-399">If a file name is not provided, then all errors will be returned on the Results page.</span></span>
2. <span data-ttu-id="946d0-400">Se viene fornito un nome di file senza una directory, il file sarà creato (o sovrascritto) nella directory dell'ambiente corrente.</span><span class="sxs-lookup"><span data-stu-id="946d0-400">If a file name is provided without a directory, then the file will be created (or overwritten) in the current environment directory.</span></span>
3. <span data-ttu-id="946d0-401">Se si seleziona un file esistente, il file verrà sovrascritto. Non è prevista l'opzione di accodamento.</span><span class="sxs-lookup"><span data-stu-id="946d0-401">If you select an existing file, then the file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="946d0-402">Quindi, scegliere se registrare tutti i messaggi di errore, quelli critici o nessuno.</span><span class="sxs-lookup"><span data-stu-id="946d0-402">Then, choose whether to log all, critical, or no error messages.</span></span> <span data-ttu-id="946d0-403">Infine, definire la frequenza con cui il messaggio di trasferimento su schermo verrà aggiornato con lo stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="946d0-403">Finally, decide how frequently the on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="946d0-404">Confermare le impostazioni di importazione e visualizzare la riga di comando</span><span class="sxs-lookup"><span data-stu-id="946d0-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="946d0-405">Dopo avere specificato le informazioni di origine e di destinazione e la configurazione avanzata, esaminare il riepilogo della migrazione e, facoltativamente, visualizzare/copiare il comando di migrazione risultante (copiare il comando è utile per automatizzare le operazioni di importazione):</span><span class="sxs-lookup"><span data-stu-id="946d0-405">After specifying source information, target information, and advanced configuration, review the migration summary and, optionally, view/copy the resulting migration command (copying the command is useful to automate import operations):</span></span>
   
    ![Schermata della pagina di riepilogo](./media/import-data/summary.png)
   
    ![Schermata della pagina di riepilogo](./media/import-data/summarycommand.png)
2. <span data-ttu-id="946d0-408">Una volta verificate le opzioni di origine e di destinazione, fare clic su **Import**.</span><span class="sxs-lookup"><span data-stu-id="946d0-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="946d0-409">Il tempo trascorso, il conteggio degli elementi trasferiti e le informazioni sugli errori (se non è stato fornito un nome file nella pagina Configurazione avanzata) verranno aggiornati mentre l'importazione è in corso.</span><span class="sxs-lookup"><span data-stu-id="946d0-409">The elapsed time, transferred count, and failure information (if you didn't provide a file name in the Advanced configuration) will update as the import is in process.</span></span> <span data-ttu-id="946d0-410">Una volta completata, è possibile esportare i risultati (ad esempio, per gestire gli eventuali errori di importazione).</span><span class="sxs-lookup"><span data-stu-id="946d0-410">Once complete, you can export the results (e.g. to deal with any import failures).</span></span>
   
    ![Screenshot dell'opzione di esportazione in JSON di Azure Cosmos DB](./media/import-data/viewresults.png)
3. <span data-ttu-id="946d0-412">È anche possibile avviare una nuova importazione, mantenendo le impostazioni esistenti (ad esempio, le informazioni della stringa di connessione, la scelta dell'origine e della destinazione, ecc.) o reimpostando tutti i valori.</span><span class="sxs-lookup"><span data-stu-id="946d0-412">You may also start a new import, either keeping the existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Screenshot dell'opzione di esportazione in JSON di Azure Cosmos DB](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="946d0-414">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="946d0-414">Next steps</span></span>

<span data-ttu-id="946d0-415">In questa esercitazione sono state eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="946d0-415">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="946d0-416">Installazione dello strumento di migrazione dati</span><span class="sxs-lookup"><span data-stu-id="946d0-416">Installed the Data Migration tool</span></span>
> * <span data-ttu-id="946d0-417">Importazione di dati da diverse origini dati</span><span class="sxs-lookup"><span data-stu-id="946d0-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="946d0-418">Esportazione da Azure Cosmos DB a JSON</span><span class="sxs-lookup"><span data-stu-id="946d0-418">Exported from Azure Cosmos DB to JSON</span></span>

<span data-ttu-id="946d0-419">È ora possibile passare all'esercitazione successiva per ottenere informazioni su come eseguire query sui dati usando Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="946d0-419">You can now proceed to the next tutorial and learn how to query data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="946d0-420">Come eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="946d0-420">How to query data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
