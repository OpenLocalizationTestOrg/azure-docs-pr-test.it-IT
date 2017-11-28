---
title: strumento di migrazione aaaDatabase per Azure Cosmos DB | Documenti Microsoft
description: Informazioni su come toouse hello aprire origine Azure Cosmos DB dati migrazione strumenti tooimport dati tooAzure DB Cosmos da varie origini, inclusi i file di MongoDB, di SQL Server, archiviazione tabella, DynamoDB Amazon, CSV e JSON. Conversione di tooJSON CSV.
keywords: CSV toojson, strumenti di migrazione di database, convertire toojson csv
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
ms.openlocfilehash: 997648a31602d854db75bb6ce4e2ecff36fc1069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a><span data-ttu-id="8f6d7-105">Come dati tooimport in Azure Cosmos DB per hello API DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="8f6d7-105">How tooimport data into Azure Cosmos DB for hello DocumentDB API?</span></span>

<span data-ttu-id="8f6d7-106">In questa esercitazione vengono fornite istruzioni sull'utilizzo di hello Azure Cosmos DB: strumento di migrazione dei dati API DocumentDB, che è possibile importare dati da origini diverse, inclusi i file JSON, i file CSV, SQL, MongoDB, archiviazione tabelle di Azure, Amazon DynamoDB e Azure Cosmos DB DocumentDB Raccolte di API in raccolte per usare con Azure Cosmos DB e hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-106">This tutorial provides instructions on using hello Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and hello DocumentDB API.</span></span> <span data-ttu-id="8f6d7-107">strumento di migrazione dei dati Hello è utilizzabile anche durante la migrazione da una raccolta di più partizioni tooa raccolta singola partizione per hello API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-107">hello Data Migration tool can also be used when migrating from a single partition collection tooa multi-partition collection for hello DocumentDB API.</span></span>

<span data-ttu-id="8f6d7-108">strumento di migrazione dei dati Hello funziona solo se l'importazione di dati in Azure Cosmos DB per utilizzano con l'API DocumentDB hello.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-108">hello Data Migration tool only works when importing data into Azure Cosmos DB for use with hello DocumentDB API.</span></span> <span data-ttu-id="8f6d7-109">Importazione di dati per l'utilizzo con hello tabella API o l'API Graph non è supportato in questo momento.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-109">Importing data for use with hello Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="8f6d7-110">tooimport dati per l'utilizzo con hello MongoDB API, vedere [DB Cosmos Azure: come dati toomigrate per hello API MongoDB?](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-110">tooimport data for use with hello MongoDB API, see [Azure Cosmos DB: How toomigrate data for hello MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="8f6d7-111">Questa esercitazione sono trattati hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-111">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8f6d7-112">Installazione dello strumento di migrazione dei dati hello</span><span class="sxs-lookup"><span data-stu-id="8f6d7-112">Installing hello Data Migration tool</span></span>
> * <span data-ttu-id="8f6d7-113">Importazione di dati da diverse origini dati</span><span class="sxs-lookup"><span data-stu-id="8f6d7-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="8f6d7-114">Esportazione da Azure Cosmos DB tooJSON</span><span class="sxs-lookup"><span data-stu-id="8f6d7-114">Exporting from Azure Cosmos DB tooJSON</span></span>

## <span data-ttu-id="8f6d7-115"><a id="Prerequisites"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8f6d7-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="8f6d7-116">Prima di seguire le istruzioni di hello in questo articolo, assicurarsi di aver installato quanto segue hello:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-116">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="8f6d7-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="8f6d7-118"><a id="Overviewl"></a>Panoramica dello strumento di migrazione dei dati hello</span><span class="sxs-lookup"><span data-stu-id="8f6d7-118"><a id="Overviewl"></a>Overview of hello Data Migration tool</span></span>
<span data-ttu-id="8f6d7-119">strumento di migrazione dei dati Hello è una soluzione open source che importa dati tooAzure Cosmos DB da un'ampia gamma di origini, tra cui:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-119">hello Data Migration tool is an open source solution that imports data tooAzure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="8f6d7-120">File JSON</span><span class="sxs-lookup"><span data-stu-id="8f6d7-120">JSON files</span></span>
* <span data-ttu-id="8f6d7-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="8f6d7-121">MongoDB</span></span>
* <span data-ttu-id="8f6d7-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="8f6d7-122">SQL Server</span></span>
* <span data-ttu-id="8f6d7-123">File CSV</span><span class="sxs-lookup"><span data-stu-id="8f6d7-123">CSV files</span></span>
* <span data-ttu-id="8f6d7-124">Archiviazione tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="8f6d7-124">Azure Table storage</span></span>
* <span data-ttu-id="8f6d7-125">DynamoDB Amazon</span><span class="sxs-lookup"><span data-stu-id="8f6d7-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="8f6d7-126">HBase</span><span class="sxs-lookup"><span data-stu-id="8f6d7-126">HBase</span></span>
* <span data-ttu-id="8f6d7-127">Raccolte di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8f6d7-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="8f6d7-128">Mentre lo strumento di importazione hello include un'interfaccia utente grafica (dtui.exe), può essere controllato anche dalla riga di comando hello (dt.exe).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-128">While hello import tool includes a graphical user interface (dtui.exe), it can also be driven from hello command line (dt.exe).</span></span> <span data-ttu-id="8f6d7-129">È in realtà, un comando di hello associata toooutput opzione dopo aver impostato un'importazione tramite hello dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-129">In fact, there is an option toooutput hello associated command after setting up an import through hello UI.</span></span> <span data-ttu-id="8f6d7-130">I dati di origine tabulari (ad esempio, file CSV o SQL Server) possono essere trasformati in modo da poter creare relazioni gerarchiche (documenti secondari) durante l'importazione.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="8f6d7-131">Mantenere la lettura di toolearn ulteriori informazioni sulle opzioni di origine, tooimport righe di comando di esempio da ogni origine, le opzioni di destinazione e la visualizzazione, importare i risultati.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-131">Keep reading toolearn more about source options, sample command lines tooimport from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="8f6d7-132"><a id="Install"></a>Installare lo strumento di migrazione dei dati hello</span><span class="sxs-lookup"><span data-stu-id="8f6d7-132"><a id="Install"></a>Install hello Data Migration tool</span></span>
<span data-ttu-id="8f6d7-133">codice sorgente dello strumento di migrazione Hello è disponibile su GitHub in [questo repository](https://github.com/azure/azure-documentdb-datamigrationtool) ed è disponibile una versione compilata [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-133">hello migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="8f6d7-134">È possibile compilare la soluzione hello o semplicemente il download ed estrarre hello versione compilata tooa directory desiderata.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-134">You may either compile hello solution or simply download and extract hello compiled version tooa directory of your choice.</span></span> <span data-ttu-id="8f6d7-135">Eseguire quindi:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-135">Then run either:</span></span>

* <span data-ttu-id="8f6d7-136">**Dtui.exe**: versione con interfaccia grafica dello strumento hello</span><span class="sxs-lookup"><span data-stu-id="8f6d7-136">**Dtui.exe**: Graphical interface version of hello tool</span></span>
* <span data-ttu-id="8f6d7-137">**DT.exe**: la versione della riga di comando dello strumento hello</span><span class="sxs-lookup"><span data-stu-id="8f6d7-137">**Dt.exe**: Command-line version of hello tool</span></span>

## <a name="import-data"></a><span data-ttu-id="8f6d7-138">Importa dati</span><span class="sxs-lookup"><span data-stu-id="8f6d7-138">Import data</span></span>

<span data-ttu-id="8f6d7-139">Dopo aver installato lo strumento di hello, è ora tooimport i dati.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-139">Once you've installed hello tool, it's time tooimport your data.</span></span> <span data-ttu-id="8f6d7-140">Il tipo di dati si desidera tooimport?</span><span class="sxs-lookup"><span data-stu-id="8f6d7-140">What kind of data do you want tooimport?</span></span>

* [<span data-ttu-id="8f6d7-141">File JSON</span><span class="sxs-lookup"><span data-stu-id="8f6d7-141">JSON files</span></span>](#JSON)
* [<span data-ttu-id="8f6d7-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="8f6d7-142">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="8f6d7-143">File di esportazione MongoDB</span><span class="sxs-lookup"><span data-stu-id="8f6d7-143">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="8f6d7-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="8f6d7-144">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="8f6d7-145">File CSV</span><span class="sxs-lookup"><span data-stu-id="8f6d7-145">CSV files</span></span>](#CSV)
* [<span data-ttu-id="8f6d7-146">Archivio tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="8f6d7-146">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="8f6d7-147">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="8f6d7-147">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="8f6d7-148">BLOB</span><span class="sxs-lookup"><span data-stu-id="8f6d7-148">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="8f6d7-149">Raccolte di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8f6d7-149">Azure Cosmos DB collections</span></span>](#DocumentDBSource)
* [<span data-ttu-id="8f6d7-150">HBase</span><span class="sxs-lookup"><span data-stu-id="8f6d7-150">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="8f6d7-151">Importazione in blocco di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8f6d7-151">Azure Cosmos DB bulk import</span></span>](#DocumentDBBulkImport)
* [<span data-ttu-id="8f6d7-152">Importazione di record sequenziali di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8f6d7-152">Azure Cosmos DB sequential record import</span></span>](#DocumentDSeqTarget)


## <span data-ttu-id="8f6d7-153"><a id="JSON"></a>file JSON tooimport</span><span class="sxs-lookup"><span data-stu-id="8f6d7-153"><a id="JSON"></a>tooimport JSON files</span></span>
<span data-ttu-id="8f6d7-154">opzione dell'utilità di importazione dell'origine di file JSON Hello consente tooimport uno o più file JSON singolo documento o i file JSON, ciascuna delle quali contiene una matrice di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-154">hello JSON file source importer option allows you tooimport one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="8f6d7-155">Quando si aggiungono cartelle che contengono tooimport file JSON, è possibile hello in modo ricorsivo la ricerca dei file nelle sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-155">When adding folders that contain JSON files tooimport, you have hello option of recursively searching for files in subfolders.</span></span>

![Schermata delle opzioni dell'origine file JSON - Strumenti di migrazione del database](./media/import-data/jsonsource.png)

<span data-ttu-id="8f6d7-157">Ecco alcuni file JSON tooimport esempi della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-157">Here are some command line samples tooimport JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition hello data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <span data-ttu-id="8f6d7-158"><a id="MongoDB"></a>tooimport da MongoDB</span><span class="sxs-lookup"><span data-stu-id="8f6d7-158"><a id="MongoDB"></a>tooimport from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8f6d7-159">Se si importano account Azure Cosmos DB tooan con supporto per MongoDB, attenersi alla seguente [istruzioni](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-159">If you are importing tooan Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="8f6d7-160">opzione dell'utilità di importazione dell'origine di MongoDB Hello consente tooimport da un singolo insieme di MongoDB e, facoltativamente, filtrare i documenti utilizzando una query e/o modificare struttura del documento hello utilizzando una proiezione.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-160">hello MongoDB source importer option allows you tooimport from an individual MongoDB collection and optionally filter documents using a query and/or modify hello document structure by using a projection.</span></span>  

![Screenshot delle opzioni relative all'origine per MongoDB](./media/import-data/mongodbsource.png)

<span data-ttu-id="8f6d7-162">stringa di connessione Hello è nel formato standard di MongoDB hello:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-162">hello connection string is in hello standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="8f6d7-163">Utilizzare hello verificare comando tooensure che hello MongoDB istanza specificata nel campo stringa di connessione hello è accessibile.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-163">Use hello Verify command tooensure that hello MongoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="8f6d7-164">Immettere il nome di hello dell'insieme di hello da cui verranno importati i dati.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-164">Enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="8f6d7-165">È facoltativamente possibile specificare o fornire un file per una query (ad esempio {pop: {$gt: 5000}}) e/o proiezione (ad esempio {loc:0}) tooboth filtro e la forma hello dati toobe importati.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) tooboth filter and shape hello data toobe imported.</span></span>

<span data-ttu-id="8f6d7-166">Ecco alcuni tooimport esempi della riga di comando da MongoDB:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-166">Here are some command line samples tooimport from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="8f6d7-167"><a id="MongoDBExport"></a>file di esportazione tooimport MongoDB</span><span class="sxs-lookup"><span data-stu-id="8f6d7-167"><a id="MongoDBExport"></a>tooimport MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8f6d7-168">Se si importano account Azure Cosmos DB tooan con supporto per MongoDB, attenersi alla seguente [istruzioni](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-168">If you are importing tooan Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="8f6d7-169">opzione di esportazione JSON file sorgente dell'utilità di importazione MongoDB Hello consente tooimport uno o più file JSON generato dall'utilità mongoexport hello.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-169">hello MongoDB export JSON file source importer option allows you tooimport one or more JSON files produced from hello mongoexport utility.</span></span>  

![Screenshot delle opzioni relative all'origine per file di esportazione MongoDB](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="8f6d7-171">Quando si aggiungono cartelle contenenti file JSON di esportazione MongoDB per l'importazione, è possibile hello in modo ricorsivo la ricerca dei file nelle sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-171">When adding folders that contain MongoDB export JSON files for import, you have hello option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="8f6d7-172">Ecco un tooimport di esempio della riga di comando da esportazione MongoDB file JSON:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-172">Here is a command line sample tooimport from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="8f6d7-173"><a id="SQL"></a>tooimport da SQL Server</span><span class="sxs-lookup"><span data-stu-id="8f6d7-173"><a id="SQL"></a>tooimport from SQL Server</span></span>
<span data-ttu-id="8f6d7-174">opzione dell'utilità di importazione dell'origine SQL Hello consente tooimport da un singolo database di SQL Server e facoltativamente il filtro hello record toobe importati utilizzando una query.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-174">hello SQL source importer option allows you tooimport from an individual SQL Server database and optionally filter hello records toobe imported using a query.</span></span> <span data-ttu-id="8f6d7-175">Inoltre, è possibile modificare struttura del documento hello specificando un separatore di annidamento (ulteriori informazioni in proposito).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-175">In addition, you can modify hello document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Schermata delle opzioni dell'origine SQL - Strumenti di migrazione del database](./media/import-data/sqlexportsource.png)

<span data-ttu-id="8f6d7-177">Hello della stringa di connessione hello è hello standard SQL connessione stringa formato.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-177">hello format of hello connection string is hello standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="8f6d7-178">Utilizzare hello verificare comando tooensure che l'istanza di SQL Server specificato nel campo stringa di connessione hello hello è accessibile.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-178">Use hello Verify command tooensure that hello SQL Server instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="8f6d7-179">la nidificazione di proprietà separatore Hello è relazioni gerarchiche toocreate utilizzato (documenti secondari) durante l'importazione.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-179">hello nesting separator property is used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="8f6d7-180">Prendere in considerazione hello seguente query SQL:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-180">Consider hello following SQL query:</span></span>

<span data-ttu-id="8f6d7-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span><span class="sxs-lookup"><span data-stu-id="8f6d7-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="8f6d7-182">Restituisce hello successivo di risultati (parziali):</span><span class="sxs-lookup"><span data-stu-id="8f6d7-182">Which returns hello following (partial) results:</span></span>

![Schermata dei risultati della query SQL](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="8f6d7-184">Si noti, ad esempio Address.AddressType e Address.Location.StateProvinceName gli alias di hello.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-184">Note hello aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="8f6d7-185">Specificando un separatore di nidificazione '.', lo strumento di importazione hello Crea indirizzo e importare i documenti secondari Address.Location durante hello.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-185">By specifying a nesting separator of ‘.’, hello import tool creates Address and Address.Location subdocuments during hello import.</span></span> <span data-ttu-id="8f6d7-186">Ecco un esempio di documento risultante in Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="8f6d7-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span><span class="sxs-lookup"><span data-stu-id="8f6d7-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="8f6d7-188">Ecco alcuni tooimport esempi della riga di comando da SQL Server:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-188">Here are some command line samples tooimport from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="8f6d7-189"><a id="CSV"></a>file CSV tooimport e tooJSON CSV convert</span><span class="sxs-lookup"><span data-stu-id="8f6d7-189"><a id="CSV"></a>tooimport CSV files and convert CSV tooJSON</span></span>
<span data-ttu-id="8f6d7-190">opzione dell'utilità di importazione dell'origine di file CSV Hello consente si tooimport uno o più file CSV.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-190">hello CSV file source importer option enables you tooimport one or more CSV files.</span></span> <span data-ttu-id="8f6d7-191">Quando si aggiungono cartelle contenenti file CSV per l'importazione, è possibile hello in modo ricorsivo la ricerca dei file nelle sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-191">When adding folders that contain CSV files for import, you have hello option of recursively searching for files in subfolders.</span></span>

![Opzioni origine schermata di CSV - tooJSON CSV](media/import-data/csvsource.png)

<span data-ttu-id="8f6d7-193">Origine SQL toohello simile, hello nidificazione proprietà separatore può essere utilizzato toocreate relazioni gerarchiche (documenti secondari) durante l'importazione.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-193">Similar toohello SQL source, hello nesting separator property may be used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="8f6d7-194">Prendere in considerazione hello seguente riga di intestazione CSV e le righe di dati:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-194">Consider hello following CSV header row and data rows:</span></span>

![Record di esempio di schermata di CSV - tooJSON CSV](./media/import-data/csvsample.png)

<span data-ttu-id="8f6d7-196">Si noti, ad esempio DomainInfo.Domain_Name e RedirectInfo.Redirecting gli alias di hello.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-196">Note hello aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="8f6d7-197">Specificando un separatore di nidificazione '.', lo strumento di importazione hello creerà DomainInfo e importare i documenti secondari RedirectInfo durante hello.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-197">By specifying a nesting separator of ‘.’, hello import tool will create DomainInfo and RedirectInfo subdocuments during hello import.</span></span> <span data-ttu-id="8f6d7-198">Ecco un esempio di documento risultante in Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="8f6d7-199">*{"DomainInfo": {"Nome_dominio": "ACUS.GOV", "Domain_Name_Address": "http://www. ACUS.GOV"}"Agenzie federali":"Conferenza amministrativa di hello United States","RedirectInfo": {"Reindirizzamento":"0","Redirect_Destination":" "},"id":"9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d"}*</span><span class="sxs-lookup"><span data-stu-id="8f6d7-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of hello United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="8f6d7-200">lo strumento di importazione Hello tenterà tooinfer informazioni sul tipo per valori non racchiusi tra virgolette nei file CSV (valori tra virgolette vengono sempre considerati come stringhe).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-200">hello import tool will attempt tooinfer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="8f6d7-201">Tipi vengono identificati nel seguente ordine hello: numero, datetime, boolean.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-201">Types are identified in hello following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="8f6d7-202">Esistono due altri toonote operazioni sull'importazione di file CSV:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-202">There are two other things toonote about CSV import:</span></span>

1. <span data-ttu-id="8f6d7-203">Per impostazione predefinita, nei valori non racchiusi tra virgolette vengono sempre rimossi spazi e tabulazioni, mentre i valori tra virgolette vengono mantenuti così come sono.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="8f6d7-204">Questo comportamento può essere sostituito con hello che Trim racchiuso tra virgolette i valori casella di controllo o hello /s.TrimQuoted opzione riga di comando.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-204">This behavior can be overridden with hello Trim quoted values checkbox or hello /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="8f6d7-205">Per impostazione predefinita, un valore Null non racchiuso tra virgolette viene considerato come valore Null.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="8f6d7-206">Questo comportamento può essere ignorato (ovvero considerare un null non racchiusi tra virgolette come una stringa "null") con hello Treat non racchiusi tra virgolette NULL come stringa Casella di controllo o hello /s.NoUnquotedNulls opzione riga di comando.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with hello Treat unquoted NULL as string checkbox or hello /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="8f6d7-207">Ecco un esempio di riga di comando per l'importazione CSV:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="8f6d7-208"><a id="AzureTableSource"></a>tooimport dall'archiviazione tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="8f6d7-208"><a id="AzureTableSource"></a>tooimport from Azure Table storage</span></span>
<span data-ttu-id="8f6d7-209">Hello opzione dell'utilità di importazione di origine archiviazione tabelle di Azure consente tooimport da una singola tabella di archiviazione tabelle di Azure e, facoltativamente, filtrare hello tabella entità toobe importati.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-209">hello Azure Table storage source importer option allows you tooimport from an individual Azure Table storage table and optionally filter hello table entities toobe imported.</span></span> <span data-ttu-id="8f6d7-210">Si noti che non è possibile utilizzare dati di archiviazione Azure Table strumento tooimport hello migrazione dei dati in Azure Cosmos DB per l'utilizzo con hello API di tabella.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-210">Note that you cannot use hello Data Migration tool tooimport Azure Table storage data into Azure Cosmos DB for use with hello Table API.</span></span> <span data-ttu-id="8f6d7-211">Solo l'importazione tooAzure Cosmos DB da utilizzare con l'API DocumentDB hello è supportato in questo momento.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-211">Only importing tooAzure Cosmos DB for use with hello DocumentDB API is supported at this time.</span></span>

![Schermata delle opzioni dell'origine Archiviazione tabelle di Azure](./media/import-data/azuretablesource.png)

<span data-ttu-id="8f6d7-213">Hello formato di stringa di connessione di archiviazione Azure Table hello è:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-213">hello format of hello Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="8f6d7-214">Utilizzare hello verificare comando tooensure che l'istanza di archiviazione tabelle di Azure specificato nel campo stringa di connessione hello hello è accessibile.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-214">Use hello Verify command tooensure that hello Azure Table storage instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="8f6d7-215">Immettere il nome di hello di hello Azure da cui verranno importati i dati nella tabella.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-215">Enter hello name of hello Azure table from which data will be imported.</span></span> <span data-ttu-id="8f6d7-216">Se si preferisce, si può specificare un [filtro](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="8f6d7-217">opzione dell'utilità di importazione di tabelle di Azure storage origine Hello ha hello le opzioni aggiuntive seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-217">hello Azure Table storage source importer option has hello following additional options:</span></span>

1. <span data-ttu-id="8f6d7-218">Include Internal Fields</span><span class="sxs-lookup"><span data-stu-id="8f6d7-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="8f6d7-219">All: include tutti i campi interni (PartitionKey, RowKey e Timestamp)</span><span class="sxs-lookup"><span data-stu-id="8f6d7-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="8f6d7-220">None: esclude tutti i campi interni</span><span class="sxs-lookup"><span data-stu-id="8f6d7-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="8f6d7-221">RowKey - includere solo campi di hello RowKey</span><span class="sxs-lookup"><span data-stu-id="8f6d7-221">RowKey - Only include hello RowKey field</span></span>
2. <span data-ttu-id="8f6d7-222">Select Columns</span><span class="sxs-lookup"><span data-stu-id="8f6d7-222">Select Columns</span></span>
   1. <span data-ttu-id="8f6d7-223">I filtri di Archiviazione tabelle di Azure non supportano le proiezioni.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="8f6d7-224">Se si desidera tooonly importazione specifica tabelle di Azure le proprietà delle entità, aggiungerli toohello elenco di colonne selezionate.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-224">If you want tooonly import specific Azure Table entity properties, add them toohello Select Columns list.</span></span> <span data-ttu-id="8f6d7-225">Tutte le altre proprietà delle entità verranno ignorate.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="8f6d7-226">Di seguito è riportato un tooimport di esempio della riga di comando da Archiviazione tabelle di Azure:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-226">Here is a command line sample tooimport from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="8f6d7-227"><a id="DynamoDBSource"></a>tooimport da DynamoDB Amazon</span><span class="sxs-lookup"><span data-stu-id="8f6d7-227"><a id="DynamoDBSource"></a>tooimport from Amazon DynamoDB</span></span>
<span data-ttu-id="8f6d7-228">opzione dell'utilità di importazione dell'origine di Amazon DynamoDB Hello consente tooimport da una singola tabella DynamoDB Amazon e facoltativamente il filtro hello entità toobe importati.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-228">hello Amazon DynamoDB source importer option allows you tooimport from an individual Amazon DynamoDB table and optionally filter hello entities toobe imported.</span></span> <span data-ttu-id="8f6d7-229">Sono disponibili vari modelli in modo che l'impostazione di un'importazione è più semplice possibile.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Schermata delle opzioni dell'origine Amazon DynamoDB - Strumenti di migrazione del database](./media/import-data/dynamodbsource1.png)

![Schermata delle opzioni dell'origine Amazon DynamoDB - Strumenti di migrazione del database](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="8f6d7-232">Hello formato di stringa di connessione DynamoDB Amazon hello è:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-232">hello format of hello Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="8f6d7-233">Utilizzare hello verificare comando tooensure che hello Amazon DynamoDB istanza specificata nel campo stringa di connessione hello è accessibile.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-233">Use hello Verify command tooensure that hello Amazon DynamoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="8f6d7-234">Di seguito è riportato un tooimport di esempio della riga di comando da Amazon DynamoDB:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-234">Here is a command line sample tooimport from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="8f6d7-235"><a id="BlobImport"></a>tooimport file dall'archiviazione Blob di Azure</span><span class="sxs-lookup"><span data-stu-id="8f6d7-235"><a id="BlobImport"></a>tooimport files from Azure Blob storage</span></span>
<span data-ttu-id="8f6d7-236">Hello file JSON, i file di esportazione MongoDB e le opzioni dell'utilità di importazione di codice sorgente file CSV consentono tooimport uno o più file dall'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-236">hello JSON file, MongoDB export file, and CSV file source importer options allow you tooimport one or more files from Azure Blob storage.</span></span> <span data-ttu-id="8f6d7-237">Dopo aver specificato un URL del contenitore Blob e la chiave dell'Account, è sufficiente fornire un file tooimport di espressione regolare tooselect hello.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-237">After specifying a Blob container URL and Account Key, simply provide a regular expression tooselect hello file(s) tooimport.</span></span>

![Schermata delle opzioni dell'origine file JSON](./media/import-data/blobsource.png)

<span data-ttu-id="8f6d7-239">Ecco i file JSON di riga di comando esempio tooimport dall'archiviazione Blob di Azure:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-239">Here is command line sample tooimport JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="8f6d7-240"><a id="DocumentDBSource"></a>tooimport da un insieme di API di Azure Cosmos DB DocumentDB</span><span class="sxs-lookup"><span data-stu-id="8f6d7-240"><a id="DocumentDBSource"></a>tooimport from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="8f6d7-241">opzione dell'utilità di importazione di Azure Cosmos DB origine Hello consente tooimport dati da una o più raccolte di Azure Cosmos DB e, facoltativamente, filtrare i documenti utilizzando una query.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-241">hello Azure Cosmos DB source importer option allows you tooimport data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Screenshot delle opzioni relative all'origine per Azure Cosmos DB](./media/import-data/documentdbsource.png)

<span data-ttu-id="8f6d7-243">Hello formato di stringa di connessione Azure Cosmos DB hello è:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-243">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="8f6d7-244">Hello stringa di connessione di database di Azure Cosmos account può essere recuperato dal Pannello di chiavi hello di hello portale di Azure, come descritto in [come un account Azure Cosmos DB toomanage](manage-account.md), ma il nome di hello del database hello deve toohello toobe aggiunto stringa di connessione in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-244">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="8f6d7-245">Utilizzare hello verificare comando tooensure che hello Azure Cosmos DB istanza specificata nel campo stringa di connessione hello è accessibile.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-245">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="8f6d7-246">tooimport da una singola raccolta DB Cosmos Azure, immettere il nome di hello dell'insieme di hello da cui verranno importati i dati.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-246">tooimport from a single Azure Cosmos DB collection, enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="8f6d7-247">tooimport da più database di Azure Cosmos raccolte, fornire un toomatch di espressione regolare uno o più nomi di raccolta (ad esempio collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-247">tooimport from multiple Azure Cosmos DB collections, provide a regular expression toomatch one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="8f6d7-248">Facoltativamente, è possibile specificare, o fornire un file in un filtro di query tooboth e forma hello toobe di dati importati.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-248">You may optionally specify, or provide a file for, a query tooboth filter and shape hello data toobe imported.</span></span>

> [!NOTE]
> <span data-ttu-id="8f6d7-249">Poiché il campo raccolta hello accetta espressioni regolari, se si desidera importare da un'unica raccolta il cui nome contiene caratteri di espressioni regolari, devono pertanto escape tali caratteri.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-249">Since hello collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="8f6d7-250">opzione dell'utilità di importazione di Azure Cosmos DB origine Hello presenta opzioni avanzate seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-250">hello Azure Cosmos DB source importer option has hello following advanced options:</span></span>

1. <span data-ttu-id="8f6d7-251">Includere campi interni: Specifica se consentire o meno tooinclude Azure Cosmos DB documento proprietà del sistema hello Esporta (ad esempio RID, TS).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-251">Include Internal Fields: Specifies whether or not tooinclude Azure Cosmos DB document system properties in hello export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="8f6d7-252">Numero di tentativi in caso di errore: Specifica il numero di hello di volte in cui tooretry hello connessione tooAzure DB Cosmos in caso di errori temporanei (ad esempio, interruzione della connettività di rete).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-252">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="8f6d7-253">Intervallo tra tentativi: Specifica il tempo toowait tra tentativi di connessione di hello tooAzure DB Cosmos in caso di errori temporanei (ad esempio, interruzione della connettività di rete).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-253">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="8f6d7-254">Modalità di connessione: Specifica toouse modalità di connessione hello con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-254">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="8f6d7-255">le scelte disponibili Hello sono DirectTcp, DirectHttps e Gateway.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-255">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="8f6d7-256">modalità di connessione diretta Hello sono più velocemente, mentre la modalità di gateway di hello è firewall più descrittivo, in quanto utilizza solo la porta 443.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-256">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Screenshot delle opzioni avanzate per origini Azure Cosmos DB](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="8f6d7-258">Hello strumento predefinite tooconnection modalità importazione DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-258">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="8f6d7-259">Se si verificano problemi di firewall, passare in modalità tooconnection Gateway, poiché richiede solo la porta 443.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-259">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="8f6d7-260">Ecco alcuni tooimport esempi della riga di comando da Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-260">Here are some command line samples tooimport from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="8f6d7-261">Strumento di importazione di Azure Cosmos DB dati Hello supporta inoltre l'importazione di dati da hello [emulatore di Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-261">hello Azure Cosmos DB Data Import Tool also supports import of data from hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="8f6d7-262">Quando si importano dati da un emulatore locale, impostare endpoint hello troppo`https://localhost:<port>`.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-262">When importing data from a local emulator, set hello endpoint too`https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="8f6d7-263"><a id="HBaseSource"></a>tooimport da HBase</span><span class="sxs-lookup"><span data-stu-id="8f6d7-263"><a id="HBaseSource"></a>tooimport from HBase</span></span>
<span data-ttu-id="8f6d7-264">opzione dell'utilità di importazione dell'origine di HBase Hello consente tooimport dati da una tabella HBase e, facoltativamente, filtrare i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-264">hello HBase source importer option allows you tooimport data from an HBase table and optionally filter hello data.</span></span> <span data-ttu-id="8f6d7-265">Sono disponibili vari modelli in modo che l'impostazione di un'importazione è più semplice possibile.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Schermata di HBase opzioni del codice sorgente](./media/import-data/hbasesource1.png)

![Schermata di HBase opzioni del codice sorgente](./media/import-data/hbasesource2.png)

<span data-ttu-id="8f6d7-268">Hello formato di stringa di connessione di HBase Stargate hello è:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-268">hello format of hello HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="8f6d7-269">Utilizzare hello verificare comando tooensure che hello HBase istanza specificata nel campo stringa di connessione hello è accessibile.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-269">Use hello Verify command tooensure that hello HBase instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="8f6d7-270">Di seguito è riportato un tooimport di esempio della riga di comando da HBase:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-270">Here is a command line sample tooimport from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="8f6d7-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello API DocumentDB (importazione in blocco)</span><span class="sxs-lookup"><span data-stu-id="8f6d7-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="8f6d7-272">utilità di importazione Bulk di DB Cosmos Azure Hello consente tooimport da qualsiasi delle opzioni di origine disponibile hello, utilizzando una routine di Azure Cosmos DB archiviati per una maggiore efficienza.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-272">hello Azure Cosmos DB Bulk importer allows you tooimport from any of hello available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="8f6d7-273">strumento Hello supporta importazione tooone partizionata singolo Azure Cosmos DB raccolta, nonché importazione partizionati in base al quale i dati vengono partizionati in più raccolte di Azure Cosmos DB partizionata singolo.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-273">hello tool supports import tooone single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="8f6d7-274">Per altre informazioni sul partizionamento dei dati, vedere l'articolo relativo a [partizionamento e ridimensionamento in Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="8f6d7-275">strumento Hello crea, eseguire e quindi eliminare procedure hello archiviato dalle raccolte di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-275">hello tool will create, execute, and then delete hello stored procedure from hello target collection(s).</span></span>  

![Screenshot delle opzioni relative all'importazione in blocco di Azure Cosmos DB](./media/import-data/documentdbbulk.png)

<span data-ttu-id="8f6d7-277">Hello formato di stringa di connessione Azure Cosmos DB hello è:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-277">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="8f6d7-278">Hello stringa di connessione di database di Azure Cosmos account può essere recuperato dal Pannello di chiavi hello di hello portale di Azure, come descritto in [come un account Azure Cosmos DB toomanage](manage-account.md), ma il nome di hello del database hello deve toohello toobe aggiunto stringa di connessione in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-278">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="8f6d7-279">Utilizzare hello verificare comando tooensure che hello Azure Cosmos DB istanza specificata nel campo stringa di connessione hello è accessibile.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-279">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="8f6d7-280">tooimport tooa singola raccolta, immettere il nome di hello di hello toowhich di raccolta dati verranno importati e fare clic sul pulsante Aggiungi hello.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-280">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="8f6d7-281">raccolte toomultiple tooimport, immettere il nome di ogni raccolta singolarmente o utilizzare hello segue sintassi toospecify più raccolte: *collection_prefix*[inizio indice - indice finale].</span><span class="sxs-lookup"><span data-stu-id="8f6d7-281">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="8f6d7-282">Quando si specificano più raccolte tramite sintassi di hello menzionati in precedenza, tenere presente hello segue:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-282">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="8f6d7-283">Sono supportati solo criteri di denominazione con intervalli interi.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="8f6d7-284">Ad esempio, l'indicazione insieme [0-3] produrrà hello seguenti raccolte: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-284">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="8f6d7-285">È possibile usare una sintassi abbreviata: collection[3] restituirà lo stesso set di raccolte citato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="8f6d7-286">È possibile specificare più di una sostituzione.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-286">More than one substitution can be provided.</span></span> <span data-ttu-id="8f6d7-287">Ad esempio, collection[0-1] [0-9] genererà 20 nomi di raccolte con zeri iniziali (collection01, ..02, ..03).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="8f6d7-288">Una volta hello nomi di raccolta sono stati specificati, scegliere velocità effettiva desiderata hello di raccolte di hello (400 RUs too10, russo 000).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-288">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too10,000 RUs).</span></span> <span data-ttu-id="8f6d7-289">Per ottimizzare le prestazioni di importazione, scegliere una velocità effettiva superiore.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="8f6d7-290">Per altre informazioni sui livelli di prestazioni, vedere l'articolo relativo ai [livelli di prestazioni in Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8f6d7-291">impostazione della velocità effettiva delle prestazioni di Hello solo toocollection creazione.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-291">hello performance throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="8f6d7-292">Se hello specificato raccolta esiste già, la velocità effettiva non verrà modificata.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-292">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="8f6d7-293">Quando si importano toomultiple raccolte, lo strumento di importazione hello supporta il partizionamento orizzontale basato su hash.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-293">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="8f6d7-294">In questo scenario, specificare proprietà del documento hello desiderato toouse come chiave di partizione hello (se la chiave di partizione viene lasciata vuota, documenti verrà partizionati in modo casuale fra le raccolte di destinazione hello).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-294">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="8f6d7-295">Facoltativamente, è possibile specificare il campo nell'origine di importazione hello deve essere utilizzato come hello proprietà id di database di Azure Cosmos documento durante l'importazione di hello (si noti che se questa proprietà non contengono documenti, quindi lo strumento di importazione hello genererà un GUID come valore della proprietà id hello).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-295">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="8f6d7-296">Durante l'importazione sono disponibili numerose opzioni avanzate.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="8f6d7-297">Prima di tutto, mentre lo strumento hello include un blocco predefinito importare stored procedure (BulkInsert.js), è possibile scegliere toospecify importazione stored procedure personalizzate:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-297">First, while hello tool includes a default bulk import stored procedure (BulkInsert.js), you may choose toospecify your own import stored procedure:</span></span>

 ![Screenshot dell'opzione relativa alla stored procedure di inserimento in blocco per Azure Cosmos DB](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="8f6d7-299">Inoltre, quando si importano i tipi di data (ad esempio, da SQL Server o MongoDB), è possibile scegliere tra tre opzioni di importazione:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Screenshot delle opzioni di importazione relative a data e ora per Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="8f6d7-301">String: persiste come valore di stringa.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-301">String: Persist as a string value</span></span>
* <span data-ttu-id="8f6d7-302">Epoch: persiste come valore numerico di periodo.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="8f6d7-303">Both: persiste come valore di stringa e numerico di periodo.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="8f6d7-304">Questa opzione creerà un documento secondario, ad esempio: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="8f6d7-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="8f6d7-305">utilità di importazione Bulk di DB Cosmos Azure Hello è hello ulteriori opzioni avanzate seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-305">hello Azure Cosmos DB Bulk importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="8f6d7-306">Dimensione batch: hello strumento predefinite tooa dimensione di batch di 50.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-306">Batch Size: hello tool defaults tooa batch size of 50.</span></span>  <span data-ttu-id="8f6d7-307">Se hello documenti toobe importati è di grandi dimensioni, considerare la riduzione delle dimensioni del batch hello.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-307">If hello documents toobe imported are large, consider lowering hello batch size.</span></span> <span data-ttu-id="8f6d7-308">Al contrario hello documenti toobe importati è troppo piccoli, è consigliabile generare dimensioni batch hello.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-308">Conversely, if hello documents toobe imported are small, consider raising hello batch size.</span></span>
2. <span data-ttu-id="8f6d7-309">Max Script dimensione (byte): valore predefinito è lo strumento hello tooa dimensione massima di 512KB</span><span class="sxs-lookup"><span data-stu-id="8f6d7-309">Max Script Size (bytes): hello tool defaults tooa max script size of 512KB</span></span>
3. <span data-ttu-id="8f6d7-310">Disattiva generazione automatica di Id: Se toobe ogni documento importato contiene un campo id, questa opzione può migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-310">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="8f6d7-311">I documenti in cui manca un campo ID univoco non verranno importati.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="8f6d7-312">Documenti di aggiornamento esistente: hello strumento predefinite toonot sostituendo i documenti esistenti con id in conflitto.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-312">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="8f6d7-313">Questa opzione consentirà di sovrascrivere i documenti esistenti con ID corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="8f6d7-314">Questa funzionalità è utile per le migrazioni dei dati pianificate che aggiornano i documenti esistenti.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="8f6d7-315">Numero di tentativi in caso di errore: Specifica il numero di hello di volte in cui tooretry hello connessione tooAzure DB Cosmos in caso di errori temporanei (ad esempio, interruzione della connettività di rete).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-315">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="8f6d7-316">Intervallo tra tentativi: Specifica il tempo toowait tra tentativi di connessione di hello tooAzure DB Cosmos in caso di errori temporanei (ad esempio, interruzione della connettività di rete).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-316">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="8f6d7-317">Modalità di connessione: Specifica toouse modalità di connessione hello con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-317">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="8f6d7-318">le scelte disponibili Hello sono DirectTcp, DirectHttps e Gateway.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-318">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="8f6d7-319">modalità di connessione diretta Hello sono più velocemente, mentre la modalità di gateway di hello è firewall più descrittivo, in quanto utilizza solo la porta 443.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-319">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Screenshot delle opzioni avanzate di importazione in blocco di Azure Cosmos DB](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="8f6d7-321">Hello strumento predefinite tooconnection modalità importazione DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-321">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="8f6d7-322">Se si verificano problemi di firewall, passare in modalità tooconnection Gateway, poiché richiede solo la porta 443.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-322">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="8f6d7-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello API DocumentDB (importazione di Record sequenziali)</span><span class="sxs-lookup"><span data-stu-id="8f6d7-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="8f6d7-324">unità di importazione dei record sequenziali Hello Azure Cosmos DB consente tooimport da una qualsiasi delle opzioni di origine disponibile hello su una base di un record.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-324">hello Azure Cosmos DB sequential record importer allows you tooimport from any of hello available source options on a record by record basis.</span></span> <span data-ttu-id="8f6d7-325">È possibile scegliere questa opzione se si importano tooan la raccolta esistente che ha raggiunto la quota di stored procedure.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-325">You might choose this option if you’re importing tooan existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="8f6d7-326">importazione tooa di Hello strumento supporta una singola raccolta Azure Cosmos DB (singola partizione e più partizioni), nonché importazione partizionati in base al quale i dati vengono partizionati in più raccolte di Azure Cosmos DB singola partizione e/o più partizioni.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-326">hello tool supports import tooa single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="8f6d7-327">Per altre informazioni sul partizionamento dei dati, vedere l'articolo relativo a [partizionamento e ridimensionamento in Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Screenshot delle opzioni di importazione di record sequenziali per Azure Cosmos DB](./media/import-data/documentdbsequential.png)

<span data-ttu-id="8f6d7-329">Hello formato di stringa di connessione Azure Cosmos DB hello è:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-329">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="8f6d7-330">Hello stringa di connessione di database di Azure Cosmos account può essere recuperato dal Pannello di chiavi hello di hello portale di Azure, come descritto in [come un account Azure Cosmos DB toomanage](manage-account.md), ma il nome di hello del database hello deve toohello toobe aggiunto stringa di connessione in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-330">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="8f6d7-331">Utilizzare hello verificare comando tooensure che hello Azure Cosmos DB istanza specificata nel campo stringa di connessione hello è accessibile.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-331">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="8f6d7-332">tooimport tooa singola raccolta, immettere il nome di hello di hello toowhich di raccolta dati verranno importati e fare clic sul pulsante Aggiungi hello.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-332">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="8f6d7-333">raccolte toomultiple tooimport, immettere il nome di ogni raccolta singolarmente o utilizzare hello segue sintassi toospecify più raccolte: *collection_prefix*[inizio indice - indice finale].</span><span class="sxs-lookup"><span data-stu-id="8f6d7-333">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="8f6d7-334">Quando si specificano più raccolte tramite sintassi di hello menzionati in precedenza, tenere presente hello segue:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-334">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="8f6d7-335">Sono supportati solo criteri di denominazione con intervalli interi.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="8f6d7-336">Ad esempio, l'indicazione insieme [0-3] produrrà hello seguenti raccolte: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-336">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="8f6d7-337">È possibile usare una sintassi abbreviata: collection[3] restituirà lo stesso set di raccolte citato nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="8f6d7-338">È possibile specificare più di una sostituzione.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-338">More than one substitution can be provided.</span></span> <span data-ttu-id="8f6d7-339">Ad esempio, collection[0-1] [0-9] genererà 20 nomi di raccolte con zeri iniziali (collection01, ..02, ..03).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="8f6d7-340">Una volta hello nomi di raccolta sono stati specificati, scegliere velocità effettiva desiderata hello di raccolte di hello (400 RUs too250, russo 000).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-340">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too250,000 RUs).</span></span> <span data-ttu-id="8f6d7-341">Per ottimizzare le prestazioni di importazione, scegliere una velocità effettiva superiore.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="8f6d7-342">Per altre informazioni sui livelli di prestazioni, vedere l'articolo relativo ai [livelli di prestazioni in Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="8f6d7-343">Qualsiasi importazione toocollections con velocità effettiva > 10.000 RUs richiederà una chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-343">Any import toocollections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="8f6d7-344">Se si sceglie toohave 250.000 russo, occorre toofile una richiesta di hello portale toohave aumentato l'account.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-344">If you choose toohave more than 250,000 RUs, you will need toofile a request in hello portal toohave your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="8f6d7-345">impostazione della velocità effettiva di Hello solo toocollection creazione.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-345">hello throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="8f6d7-346">Se hello specificato raccolta esiste già, la velocità effettiva non verrà modificata.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-346">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="8f6d7-347">Quando si importano toomultiple raccolte, lo strumento di importazione hello supporta il partizionamento orizzontale basato su hash.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-347">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="8f6d7-348">In questo scenario, specificare proprietà del documento hello desiderato toouse come chiave di partizione hello (se la chiave di partizione viene lasciata vuota, documenti verrà partizionati in modo casuale fra le raccolte di destinazione hello).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-348">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="8f6d7-349">Facoltativamente, è possibile specificare il campo nell'origine di importazione hello deve essere utilizzato come hello proprietà id di database di Azure Cosmos documento durante l'importazione di hello (si noti che se questa proprietà non contengono documenti, quindi lo strumento di importazione hello genererà un GUID come valore della proprietà id hello).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-349">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="8f6d7-350">Durante l'importazione sono disponibili numerose opzioni avanzate.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="8f6d7-351">Innanzitutto, quando si importano i tipi di data (ad esempio, da SQL Server o MongoDB), è possibile scegliere tra tre opzioni di importazione:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Screenshot delle opzioni di importazione relative a data e ora per Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="8f6d7-353">String: persiste come valore di stringa.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-353">String: Persist as a string value</span></span>
* <span data-ttu-id="8f6d7-354">Epoch: persiste come valore numerico di periodo.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="8f6d7-355">Both: persiste come valore di stringa e numerico di periodo.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="8f6d7-356">Questa opzione creerà un documento secondario, ad esempio: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="8f6d7-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="8f6d7-357">Hello Azure Cosmos DB - utilità di importazione di record sequenziale ha hello ulteriori opzioni avanzate seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-357">hello Azure Cosmos DB - Sequential record importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="8f6d7-358">Numero di richieste in parallelo: strumento di hello per impostazione predefinita le richieste parallele too2.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-358">Number of Parallel Requests: hello tool defaults too2 parallel requests.</span></span> <span data-ttu-id="8f6d7-359">Se hello documenti toobe importati è troppo piccoli, prendere in considerazione elevamento hello numero di richieste in parallelo.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-359">If hello documents toobe imported are small, consider raising hello number of parallel requests.</span></span> <span data-ttu-id="8f6d7-360">Si noti che se questo numero viene generato eccessivamente elevato, hello importazione che verifichi la limitazione delle richieste.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-360">Note that if this number is raised too much, hello import may experience throttling.</span></span>
2. <span data-ttu-id="8f6d7-361">Disattiva generazione automatica di Id: Se toobe ogni documento importato contiene un campo id, questa opzione può migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-361">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="8f6d7-362">I documenti in cui manca un campo ID univoco non verranno importati.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="8f6d7-363">Documenti di aggiornamento esistente: hello strumento predefinite toonot sostituendo i documenti esistenti con id in conflitto.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-363">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="8f6d7-364">Questa opzione consentirà di sovrascrivere i documenti esistenti con ID corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="8f6d7-365">Questa funzionalità è utile per le migrazioni dei dati pianificate che aggiornano i documenti esistenti.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="8f6d7-366">Numero di tentativi in caso di errore: Specifica il numero di hello di volte in cui tooretry hello connessione tooAzure DB Cosmos in caso di errori temporanei (ad esempio, interruzione della connettività di rete).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-366">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="8f6d7-367">Intervallo tra tentativi: Specifica il tempo toowait tra tentativi di connessione di hello tooAzure DB Cosmos in caso di errori temporanei (ad esempio, interruzione della connettività di rete).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-367">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="8f6d7-368">Modalità di connessione: Specifica toouse modalità di connessione hello con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-368">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="8f6d7-369">le scelte disponibili Hello sono DirectTcp, DirectHttps e Gateway.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-369">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="8f6d7-370">modalità di connessione diretta Hello sono più velocemente, mentre la modalità di gateway di hello è firewall più descrittivo, in quanto utilizza solo la porta 443.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-370">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Screenshot delle opzioni avanzate di importazione di record sequenziali di Azure Cosmos DB](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="8f6d7-372">Hello strumento predefinite tooconnection modalità importazione DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-372">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="8f6d7-373">Se si verificano problemi di firewall, passare in modalità tooconnection Gateway, poiché richiede solo la porta 443.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-373">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="8f6d7-374"><a id="IndexingPolicy"></a>Specificare un criterio di indicizzazione durante la creazione di raccolte di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8f6d7-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="8f6d7-375">Quando si consentono la migrazione di hello raccolte toocreate strumento durante l'importazione, è possibile specificare criteri di indicizzazione hello di raccolte di hello.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-375">When you allow hello migration tool toocreate collections during import, you can specify hello indexing policy of hello collections.</span></span> <span data-ttu-id="8f6d7-376">In hello avanzate sezione Opzioni di importazione Bulk di DB Cosmos Azure hello e Azure Cosmos DB sequenziale opzioni di registrazione, passare toohello sezione relativa ai criteri di indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-376">In hello advanced options section of hello Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate toohello Indexing Policy section.</span></span>

![Screenshot delle opzioni avanzate relative ai criteri di indicizzazione di Azure Cosmos DB](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="8f6d7-378">Utilizza hello opzione criteri di indicizzazione avanzati, è possibile selezionare un file di criteri di indicizzazione, manualmente immettere criteri di indicizzazione o selezionare da un set di modelli predefiniti (facendo clic destro del mouse nella casella di testo criteri di indicizzazione hello).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-378">Using hello Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in hello indexing policy textbox).</span></span>

<span data-ttu-id="8f6d7-379">lo strumento hello fornisce modelli di criteri di Hello sono:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-379">hello policy templates hello tool provides are:</span></span>

* <span data-ttu-id="8f6d7-380">Default.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-380">Default.</span></span> <span data-ttu-id="8f6d7-381">Questo criterio è migliore quando si eseguono query di uguaglianza su stringhe e utilizzando ORDER BY, l'intervallo e le query di uguaglianza per i numeri.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="8f6d7-382">Questo criterio ha un overhead di archiviazione indice inferiore rispetto a intervallo.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="8f6d7-383">Intervallo.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-383">Range.</span></span> <span data-ttu-id="8f6d7-384">Questo criterio è consigliabile quando si sta utilizzando query ORDER BY, intervallo e uguaglianza su stringhe e numeri.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="8f6d7-385">Questo criterio ha un overhead di archiviazione indice superiore rispetto a predefinito o Hash.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Screenshot delle opzioni avanzate relative ai criteri di indicizzazione di Azure Cosmos DB](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="8f6d7-387">Se non si specifica un criterio di indicizzazione, verranno applicati criteri predefiniti hello.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-387">If you do not specify an indexing policy, then hello default policy will be applied.</span></span> <span data-ttu-id="8f6d7-388">Per altre informazioni sui criteri di indicizzazione, vedere l'articolo relativo ai [criteri di indicizzazione di Azure Cosmos DB](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-toojson-file"></a><span data-ttu-id="8f6d7-389">File di esportazione tooJSON</span><span class="sxs-lookup"><span data-stu-id="8f6d7-389">Export tooJSON file</span></span>
<span data-ttu-id="8f6d7-390">esportazione di Azure Cosmos DB JSON Hello consente tooexport qualsiasi hello disponibili opzioni tooa JSON file di origine che contiene una matrice di documenti JSON.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-390">hello Azure Cosmos DB JSON exporter allows you tooexport any of hello available source options tooa JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="8f6d7-391">strumento Hello gestirà esportazione hello automaticamente oppure è possibile scegliere il comando di migrazione tooview hello risultante ed eseguire il comando hello manualmente.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-391">hello tool will handle hello export for you, or you can choose tooview hello resulting migration command and run hello command yourself.</span></span> <span data-ttu-id="8f6d7-392">file JSON risultante Hello può essere archiviati in locale o nel servizio di archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-392">hello resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Screenshot dell'opzione di esportazione in file JSON locale di Azure Cosmos DB](./media/import-data/jsontarget.png)

![Screenshot dell'opzione di esportazione in file JSON in un archivio BLOB di Azure di Azure Cosmos DB](./media/import-data/jsontarget2.png)

<span data-ttu-id="8f6d7-395">Facoltativamente, è possibile scegliere hello tooprettify risultante JSON, che aumenta la dimensione hello del documento risultante hello mentre effettua hello contenuto più leggibili.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-395">You may optionally choose tooprettify hello resulting JSON, which will increase hello size of hello resulting document while making hello contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places toosee in Paris"}]}]

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
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places toosee in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="8f6d7-396">Configurazione avanzata</span><span class="sxs-lookup"><span data-stu-id="8f6d7-396">Advanced configuration</span></span>
<span data-ttu-id="8f6d7-397">Nella schermata di configurazione avanzate hello, specificare il percorso di hello di hello toowhich di file di log che si desidera che gli eventuali errori scritti.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-397">In hello Advanced configuration screen, specify hello location of hello log file toowhich you would like any errors written.</span></span> <span data-ttu-id="8f6d7-398">Hello seguendo regole si applica toothis pagina:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-398">hello following rules apply toothis page:</span></span>

1. <span data-ttu-id="8f6d7-399">Se non viene fornito un nome di file, verranno restituiti tutti gli errori nella pagina di risultati hello.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-399">If a file name is not provided, then all errors will be returned on hello Results page.</span></span>
2. <span data-ttu-id="8f6d7-400">Se viene specificato un nome di file senza una directory, quindi il file hello sarà creato (o sovrascritto) nella directory di ambiente corrente hello.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-400">If a file name is provided without a directory, then hello file will be created (or overwritten) in hello current environment directory.</span></span>
3. <span data-ttu-id="8f6d7-401">Se si seleziona un oggetto esistente verrà sovrascritto file, quindi il file hello, vi è alcuna possibilità di Accodamento.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-401">If you select an existing file, then hello file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="8f6d7-402">Quindi, scegliere se toolog tutti critico, o nessun messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-402">Then, choose whether toolog all, critical, or no error messages.</span></span> <span data-ttu-id="8f6d7-403">Infine, decidere di frequenza hello nel messaggio di trasferimento dello schermo verrà aggiornato con lo stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-403">Finally, decide how frequently hello on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="8f6d7-404">Confermare le impostazioni di importazione e visualizzare la riga di comando</span><span class="sxs-lookup"><span data-stu-id="8f6d7-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="8f6d7-405">Dopo aver specificato le informazioni sull'origine, le informazioni di destinazione e configurazione avanzata, verificare la migrazione di hello riepilogo e, facoltativamente, visualizzazione o copia hello risultante comando migration (copia comando hello è utile tooautomate operazioni di importazione):</span><span class="sxs-lookup"><span data-stu-id="8f6d7-405">After specifying source information, target information, and advanced configuration, review hello migration summary and, optionally, view/copy hello resulting migration command (copying hello command is useful tooautomate import operations):</span></span>
   
    ![Schermata della pagina di riepilogo](./media/import-data/summary.png)
   
    ![Schermata della pagina di riepilogo](./media/import-data/summarycommand.png)
2. <span data-ttu-id="8f6d7-408">Una volta verificate le opzioni di origine e di destinazione, fare clic su **Import**.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="8f6d7-409">tempo trascorso Hello, conteggio trasferito e informazioni sull'errore (se si non specifica un nome di file di configurazione avanzate hello) verranno aggiornati come importazione hello è in corso.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-409">hello elapsed time, transferred count, and failure information (if you didn't provide a file name in hello Advanced configuration) will update as hello import is in process.</span></span> <span data-ttu-id="8f6d7-410">Al termine dell'operazione, è possibile esportare risultati hello (ad esempio toodeal gli eventuali errori di importazione).</span><span class="sxs-lookup"><span data-stu-id="8f6d7-410">Once complete, you can export hello results (e.g. toodeal with any import failures).</span></span>
   
    ![Screenshot dell'opzione di esportazione in JSON di Azure Cosmos DB](./media/import-data/viewresults.png)
3. <span data-ttu-id="8f6d7-412">È possibile anche avviare una nuova importazione hello esistente le stesse impostazioni (ad esempio informazioni di origine e destinazione scelta di stringa di connessione e così via) o la reimpostazione di tutti i valori.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-412">You may also start a new import, either keeping hello existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Screenshot dell'opzione di esportazione in JSON di Azure Cosmos DB](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="8f6d7-414">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8f6d7-414">Next steps</span></span>

<span data-ttu-id="8f6d7-415">In questa esercitazione, effettuata seguente hello:</span><span class="sxs-lookup"><span data-stu-id="8f6d7-415">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8f6d7-416">Lo strumento di migrazione dei dati hello installato</span><span class="sxs-lookup"><span data-stu-id="8f6d7-416">Installed hello Data Migration tool</span></span>
> * <span data-ttu-id="8f6d7-417">Importazione di dati da diverse origini dati</span><span class="sxs-lookup"><span data-stu-id="8f6d7-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="8f6d7-418">Esportato da Azure Cosmos DB tooJSON</span><span class="sxs-lookup"><span data-stu-id="8f6d7-418">Exported from Azure Cosmos DB tooJSON</span></span>

<span data-ttu-id="8f6d7-419">È ora possibile continuare l'esercitazione successiva toohello e acquisire informazioni come dati tooquery tramite Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8f6d7-419">You can now proceed toohello next tutorial and learn how tooquery data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="8f6d7-420">Come tooquery dati?</span><span class="sxs-lookup"><span data-stu-id="8f6d7-420">How tooquery data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
