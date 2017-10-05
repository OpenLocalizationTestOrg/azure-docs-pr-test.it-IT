---
title: Caricare dati da un archivio BLOB di Azure ad Azure Data Warehouse | Documentazione Microsoft
description: Informazioni su come utilizzare PolyBase per caricare i dati dall'archivio BLOB di Azure in SQL Data Warehouse. Caricare alcune tabelle dai dati pubblici nello schema del Data Warehouse di Contoso Retail.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: faca0fe7-62e7-4e1f-a86f-032b4ffcb06e
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 2859c1144f72fd685af89f83024df1409902ab0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a><span data-ttu-id="8f025-104">Caricare dati dall’archiviazione BLOB di Azure in un SQL Data Warehouse (PolyBase)</span><span class="sxs-lookup"><span data-stu-id="8f025-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f025-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="8f025-105">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="8f025-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="8f025-106">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

<span data-ttu-id="8f025-107">Usare i comandi PolyBase e T-SQL per caricare i dati dall'archivio BLOB di Azure in un Data Warehouse di Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="8f025-107">Use PolyBase and T-SQL commands to load data from Azure blob storage into Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="8f025-108">In parole brevi, in questa esercitazione vengono caricate due tabelle da un BLOB di Archiviazione di Azure pubblico nello schema del Data Warehouse di Contoso Retail.</span><span class="sxs-lookup"><span data-stu-id="8f025-108">To keep it simple, this tutorial loads two tables from a public Azure Storage Blob into the Contoso Retail Data Warehouse schema.</span></span> <span data-ttu-id="8f025-109">Per caricare il set di dati completo, eseguire l'esempio per [caricare l'intero data warehouse di Contoso Retail][Load the full Contoso Retail Data Warehouse] dal repository di esempi di Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f025-109">To load the full data set, run the example [Load the full Contoso Retail Data Warehouse][Load the full Contoso Retail Data Warehouse] from the Microsoft SQL Server Samples repository.</span></span>

<span data-ttu-id="8f025-110">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="8f025-110">In this tutorial you will:</span></span>

1. <span data-ttu-id="8f025-111">Configurare PolyBase per caricare dall'archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="8f025-111">Configure PolyBase to load from Azure blob storage</span></span>
2. <span data-ttu-id="8f025-112">Caricare dati pubblici nel database</span><span class="sxs-lookup"><span data-stu-id="8f025-112">Load public data into your database</span></span>
3. <span data-ttu-id="8f025-113">Una volta completato il caricamento, effettuare le ottimizzazioni.</span><span class="sxs-lookup"><span data-stu-id="8f025-113">Perform optimizations after the load is finished.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8f025-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="8f025-114">Before you begin</span></span>
<span data-ttu-id="8f025-115">Per eseguire questa esercitazione, è necessario un account di Azure che già dispone di un database SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8f025-115">To run this tutorial, you need an Azure account that already has a SQL Data Warehouse database.</span></span> <span data-ttu-id="8f025-116">In caso contrario, vedere l'articolo su come [creare un'istanza di SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="8f025-116">If you don't already have this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>

## <a name="1-configure-the-data-source"></a><span data-ttu-id="8f025-117">1. Configurare l'origine dati</span><span class="sxs-lookup"><span data-stu-id="8f025-117">1. Configure the data source</span></span>
<span data-ttu-id="8f025-118">PolyBase utilizza oggetti esterni T-SQL per definire il percorso e gli attributi dei dati esterni.</span><span class="sxs-lookup"><span data-stu-id="8f025-118">PolyBase uses T-SQL external objects to define the location and attributes of the external data.</span></span> <span data-ttu-id="8f025-119">Le definizioni degli oggetti esterni vengono archiviate in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8f025-119">The external object definitions are stored in SQL Data Warehouse.</span></span> <span data-ttu-id="8f025-120">I dati vengano archiviati esternamente.</span><span class="sxs-lookup"><span data-stu-id="8f025-120">The data itself is stored externally.</span></span>

### <a name="11-create-a-credential"></a><span data-ttu-id="8f025-121">1.1.</span><span class="sxs-lookup"><span data-stu-id="8f025-121">1.1.</span></span> <span data-ttu-id="8f025-122">Creare una credenziale</span><span class="sxs-lookup"><span data-stu-id="8f025-122">Create a credential</span></span>
<span data-ttu-id="8f025-123">**Ignorare questo passaggio** se si desidera caricare i dati pubblici di Contoso.</span><span class="sxs-lookup"><span data-stu-id="8f025-123">**Skip this step** if you are loading the Contoso public data.</span></span> <span data-ttu-id="8f025-124">Poiché sono già accessibili a tutti, non è necessario un accesso sicuro ai dati pubblici.</span><span class="sxs-lookup"><span data-stu-id="8f025-124">You don't need secure access to the public data since it is already accessible to anyone.</span></span>

<span data-ttu-id="8f025-125">**Non ignorare questo passaggio** se si utilizza questa esercitazione come modello per il caricamento dei dati personali.</span><span class="sxs-lookup"><span data-stu-id="8f025-125">**Don't skip this step** if you are using this tutorial as a template for loading your own data.</span></span> <span data-ttu-id="8f025-126">Per accedere ai dati tramite una credenziale, utilizzare lo script seguente per creare una credenziale con ambito di database, quindi utilizzarla quando si definisce il percorso dell'origine dati.</span><span class="sxs-lookup"><span data-stu-id="8f025-126">To access data through a credential, use the following script to create a database-scoped credential, and then use it when defining the location of the data source.</span></span>

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required to encrypt the credential secret in the next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication to Azure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide the credential created in the previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);
```

<span data-ttu-id="8f025-127">Andare al passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="8f025-127">Skip to step 2.</span></span>

### <a name="12-create-the-external-data-source"></a><span data-ttu-id="8f025-128">1.2.</span><span class="sxs-lookup"><span data-stu-id="8f025-128">1.2.</span></span> <span data-ttu-id="8f025-129">Creare un'origine dati esterna.</span><span class="sxs-lookup"><span data-stu-id="8f025-129">Create the external data source</span></span>
<span data-ttu-id="8f025-130">Usare questo comando [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] per archiviare il percorso e il tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="8f025-130">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command to store the location of the data, and the type of data.</span></span> 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> <span data-ttu-id="8f025-131">Se si sceglie di rendere pubblici i contenitori di archiviazione BLOB di Azure, tenere presente che i costi per l’uscita dei dati dal data center verranno addebitati al proprietario dei dati.</span><span class="sxs-lookup"><span data-stu-id="8f025-131">If you choose to make your azure blob storage containers public, remember that as the data owner you will be charged for data egress charges when data leaves the data center.</span></span> 
> 
> 

## <a name="2-configure-data-format"></a><span data-ttu-id="8f025-132">2. Configurare il formato dei dati</span><span class="sxs-lookup"><span data-stu-id="8f025-132">2. Configure data format</span></span>
<span data-ttu-id="8f025-133">I dati vengono archiviati in file di testo nell'archiviazione BLOB di Azure e ogni campo è separato con un delimitatore.</span><span class="sxs-lookup"><span data-stu-id="8f025-133">The data is stored in text files in Azure blob storage, and each field is separated with a delimiter.</span></span> <span data-ttu-id="8f025-134">Eseguire questo comando [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] per specificare il formato dei dati nei file di testo.</span><span class="sxs-lookup"><span data-stu-id="8f025-134">Run this [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] command to specify the format of the data in the text files.</span></span> <span data-ttu-id="8f025-135">I dati di Contoso sono delimitati da barre verticali e non sono compressi.</span><span class="sxs-lookup"><span data-stu-id="8f025-135">The Contoso data is uncompressed and pipe delimited.</span></span>

```sql
CREATE EXTERNAL FILE FORMAT TextFileFormat 
WITH 
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE 
                    )
);
``` 

## <a name="3-create-the-external-tables"></a><span data-ttu-id="8f025-136">3. Creare le tabelle esterne.</span><span class="sxs-lookup"><span data-stu-id="8f025-136">3. Create the external tables</span></span>
<span data-ttu-id="8f025-137">Ora che sono stati specificati l’origine dei dati e il formato dei file, si è pronti per creare le tabelle esterne.</span><span class="sxs-lookup"><span data-stu-id="8f025-137">Now that you have specified the data source and file format, you are ready to create the external tables.</span></span> 

### <a name="31-create-a-schema-for-the-data"></a><span data-ttu-id="8f025-138">3.1.</span><span class="sxs-lookup"><span data-stu-id="8f025-138">3.1.</span></span> <span data-ttu-id="8f025-139">Creare uno schema per i dati.</span><span class="sxs-lookup"><span data-stu-id="8f025-139">Create a schema for the data.</span></span>
<span data-ttu-id="8f025-140">Per creare un percorso in cui archiviare i dati di Contoso nel database, creare uno schema.</span><span class="sxs-lookup"><span data-stu-id="8f025-140">To create a place to store the Contoso data in your database, create a schema.</span></span>

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-the-external-tables"></a><span data-ttu-id="8f025-141">3.2.</span><span class="sxs-lookup"><span data-stu-id="8f025-141">3.2.</span></span> <span data-ttu-id="8f025-142">Creare le tabelle esterne.</span><span class="sxs-lookup"><span data-stu-id="8f025-142">Create the external tables.</span></span>
<span data-ttu-id="8f025-143">Eseguire questo script per creare le tabelle esterne DimProduct e FactOnlineSales.</span><span class="sxs-lookup"><span data-stu-id="8f025-143">Run this script to create the DimProduct and FactOnlineSales external tables.</span></span> <span data-ttu-id="8f025-144">Tutto quello che stiamo facendo qui è definire i nomi delle colonne e i tipi di dati e associarli al percorso e al formato dei file dell’archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f025-144">All we are doing here is defining column names and data types, and binding them to the location and format of the Azure blob storage files.</span></span> <span data-ttu-id="8f025-145">La definizione viene archiviata in SQL Data Warehouse e i dati sono ancora nel BLOB di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f025-145">The definition is stored in SQL Data Warehouse and the data is still in the Azure Storage Blob.</span></span>

<span data-ttu-id="8f025-146">Il parametro **LOCATION** corrisponde alla cartella sotto la cartella radice nel BLOB di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f025-146">The  **LOCATION** parameter is the folder under the root folder in the Azure Storage Blob.</span></span> <span data-ttu-id="8f025-147">Ogni tabella è in una cartella diversa.</span><span class="sxs-lookup"><span data-stu-id="8f025-147">Each table is in a different folder.</span></span>

```sql

--DimProduct
CREATE EXTERNAL TABLE [asb].DimProduct (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL,
    [ProductDescription] [nvarchar](400) NULL,
    [ProductSubcategoryKey] [int] NULL,
    [Manufacturer] [nvarchar](50) NULL,
    [BrandName] [nvarchar](50) NULL,
    [ClassID] [nvarchar](10) NULL,
    [ClassName] [nvarchar](20) NULL,
    [StyleID] [nvarchar](10) NULL,
    [StyleName] [nvarchar](20) NULL,
    [ColorID] [nvarchar](10) NULL,
    [ColorName] [nvarchar](20) NOT NULL,
    [Size] [nvarchar](50) NULL,
    [SizeRange] [nvarchar](50) NULL,
    [SizeUnitMeasureID] [nvarchar](20) NULL,
    [Weight] [float] NULL,
    [WeightUnitMeasureID] [nvarchar](20) NULL,
    [UnitOfMeasureID] [nvarchar](10) NULL,
    [UnitOfMeasureName] [nvarchar](40) NULL,
    [StockTypeID] [nvarchar](10) NULL,
    [StockTypeName] [nvarchar](40) NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [AvailableForSaleDate] [datetime] NULL,
    [StopSaleDate] [datetime] NULL,
    [Status] [nvarchar](7) NULL,
    [ImageURL] [nvarchar](150) NULL,
    [ProductURL] [nvarchar](150) NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/DimProduct/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

--FactOnlineSales
CREATE EXTERNAL TABLE [asb].FactOnlineSales 
(
    [OnlineSalesKey] [int]  NOT NULL,
    [DateKey] [datetime] NOT NULL,
    [StoreKey] [int] NOT NULL,
    [ProductKey] [int] NOT NULL,
    [PromotionKey] [int] NOT NULL,
    [CurrencyKey] [int] NOT NULL,
    [CustomerKey] [int] NOT NULL,
    [SalesOrderNumber] [nvarchar](20) NOT NULL,
    [SalesOrderLineNumber] [int] NULL,
    [SalesQuantity] [int] NOT NULL,
    [SalesAmount] [money] NOT NULL,
    [ReturnQuantity] [int] NOT NULL,
    [ReturnAmount] [money] NULL,
    [DiscountQuantity] [int] NULL,
    [DiscountAmount] [money] NULL,
    [TotalCost] [money] NOT NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/FactOnlineSales/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;
```

## <a name="4-load-the-data"></a><span data-ttu-id="8f025-148">4. Caricare i dati</span><span class="sxs-lookup"><span data-stu-id="8f025-148">4. Load the data</span></span>
<span data-ttu-id="8f025-149">È possibile accedere ai dati esterni in diversi modi.</span><span class="sxs-lookup"><span data-stu-id="8f025-149">There's different ways to access external data.</span></span>  <span data-ttu-id="8f025-150">Si può eseguire una query sui dati direttamente dalla tabella esterna, caricare i dati in nuove tabelle di database o aggiungere dati esterni alle tabelle dei database esistenti.</span><span class="sxs-lookup"><span data-stu-id="8f025-150">You can query data directly from the external table, load the data into new database tables, or add external data to existing database tables.</span></span>  

### <a name="41-create-a-new-schema"></a><span data-ttu-id="8f025-151">4.1.</span><span class="sxs-lookup"><span data-stu-id="8f025-151">4.1.</span></span> <span data-ttu-id="8f025-152">Crea un nuovo schema</span><span class="sxs-lookup"><span data-stu-id="8f025-152">Create a new schema</span></span>
<span data-ttu-id="8f025-153">CTAS crea una nuova tabella contenente i dati.</span><span class="sxs-lookup"><span data-stu-id="8f025-153">CTAS creates a new table that contains data.</span></span>  <span data-ttu-id="8f025-154">Innanzitutto, creare uno schema per i dati di Contoso.</span><span class="sxs-lookup"><span data-stu-id="8f025-154">First, create a schema for the contoso data.</span></span>

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-the-data-into-new-tables"></a><span data-ttu-id="8f025-155">4.2.</span><span class="sxs-lookup"><span data-stu-id="8f025-155">4.2.</span></span> <span data-ttu-id="8f025-156">Caricare i dati in nuove tabelle</span><span class="sxs-lookup"><span data-stu-id="8f025-156">Load the data into new tables</span></span>
<span data-ttu-id="8f025-157">Per caricare i dati dall'archivio BLOB di Azure e salvarli in una tabella all'interno del database, usare l'istruzione [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="8f025-157">To load data from Azure blob storage and save it in a table inside of your database, use the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="8f025-158">Il caricamento con CTAS sfrutta le tabelle esterne fortemente tipizzate appena create. Per caricare i dati in nuove tabelle, usare un'istruzione [CTAS][CTAS] per ogni tabella.</span><span class="sxs-lookup"><span data-stu-id="8f025-158">Loading with CTAS leverages the strongly typed external tables you have just created.To load the data into new tables, use one [CTAS][CTAS] statement per table.</span></span> 
 
<span data-ttu-id="8f025-159">CTAS crea una nuova tabella e la popola con i risultati di un'istruzione SELECT.</span><span class="sxs-lookup"><span data-stu-id="8f025-159">CTAS creates a new table and populates it with the results of a select statement.</span></span> <span data-ttu-id="8f025-160">CTAS definisce la nuova tabella in modo che abbia le stesse colonne e gli stessi tipi di dati dei risultati dell'istruzione SELECT.</span><span class="sxs-lookup"><span data-stu-id="8f025-160">CTAS defines the new table to have the same columns and data types as the results of the select statement.</span></span> <span data-ttu-id="8f025-161">Se si selezionano tutte le colonne da una tabella esterna, la nuova tabella sarà una replica delle colonne e dei tipi di dati della tabella esterna.</span><span class="sxs-lookup"><span data-stu-id="8f025-161">If you select all the columns from an external table, the new table will be a replica of the columns and data types in the external table.</span></span>

<span data-ttu-id="8f025-162">In questo esempio, creiamo sia la dimensione sia la tabella dei fatti come hash di tabelle distribuite.</span><span class="sxs-lookup"><span data-stu-id="8f025-162">In this example, we create both the dimension and the fact table as hash distributed tables.</span></span> 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-the-load-progress"></a><span data-ttu-id="8f025-163">4.3. Monitorare l'avanzamento del caricamento</span><span class="sxs-lookup"><span data-stu-id="8f025-163">4.3 Track the load progress</span></span>
<span data-ttu-id="8f025-164">È possibile monitorare l'avanzamento del caricamento con le viste a gestione dinamica (DMV).</span><span class="sxs-lookup"><span data-stu-id="8f025-164">You can track the progress of your load using dynamic management views (DMVs).</span></span> 

```sql
-- To see all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- To see a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- To track bytes and files
SELECT
    r.command,
    s.request_id,
    r.status,
    count(distinct input_name) as nbr_files, 
    sum(s.bytes_processed)/1024/1024/1024 as gb_processed
FROM
    sys.dm_pdw_exec_requests r
    inner join sys.dm_pdw_dms_external_work s
        on r.request_id = s.request_id
WHERE 
    r.[label] = 'CTAS : Load [cso].[DimProduct]             '
    OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
GROUP BY
    r.command,
    s.request_id,
    r.status
ORDER BY
    nbr_files desc,
    gb_processed desc;
```

## <a name="5-optimize-columnstore-compression"></a><span data-ttu-id="8f025-165">5. Ottimizzare la compressione columnstore</span><span class="sxs-lookup"><span data-stu-id="8f025-165">5. Optimize columnstore compression</span></span>
<span data-ttu-id="8f025-166">Per impostazione predefinita, SQL Data Warehouse archivia le tabelle come un indice columnstore cluster.</span><span class="sxs-lookup"><span data-stu-id="8f025-166">By default, SQL Data Warehouse stores the table as a clustered columnstore index.</span></span> <span data-ttu-id="8f025-167">Al termine di un caricamento, alcune delle righe di dati potrebbero non essere compresse nel columnstore.</span><span class="sxs-lookup"><span data-stu-id="8f025-167">After a load completes, some of the data rows might not be compressed into the columnstore.</span></span>  <span data-ttu-id="8f025-168">Esiste una serie di motivi per cui questo può verificarsi.</span><span class="sxs-lookup"><span data-stu-id="8f025-168">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="8f025-169">Per altre informazioni, vedere l'articolo su come [gestire gli indici columnstore][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="8f025-169">To learn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="8f025-170">Per ottimizzare le prestazioni delle query e la compressione columnstore dopo un'operazione di caricamento, ricompilare la tabella per forzare l'indice columnstore per comprimere tutte le righe.</span><span class="sxs-lookup"><span data-stu-id="8f025-170">To optimize query performance and columnstore compression after a load, rebuild the table to force the columnstore index to compress all the rows.</span></span> 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

<span data-ttu-id="8f025-171">Per altre informazioni sulla gestione di tali indici, vedere l'articolo su come [gestire gli indici columnstore][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="8f025-171">For more information on maintaining columnstore indexes, see the [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="6-optimize-statistics"></a><span data-ttu-id="8f025-172">6. Ottimizzare le statistiche</span><span class="sxs-lookup"><span data-stu-id="8f025-172">6. Optimize statistics</span></span>
<span data-ttu-id="8f025-173">È consigliabile creare statistiche a colonna singola subito dopo un caricamento.</span><span class="sxs-lookup"><span data-stu-id="8f025-173">It is best to create single-column statistics immediately after a load.</span></span> <span data-ttu-id="8f025-174">Sono disponibili alcune opzioni per le statistiche.</span><span class="sxs-lookup"><span data-stu-id="8f025-174">There are some choices for statistics.</span></span> <span data-ttu-id="8f025-175">Ad esempio, se si creano statistiche a colonna singola su ogni colonna, ricompilare tutte le statistiche potrebbe richiedere molto tempo.</span><span class="sxs-lookup"><span data-stu-id="8f025-175">For example, if you create single-column statistics on every column it might take a long time to rebuild all the statistics.</span></span> <span data-ttu-id="8f025-176">Se si sa che alcune colonne non si aggiungeranno ai predicati di query, è possibile ignorare la creazione delle statistiche su tali colonne.</span><span class="sxs-lookup"><span data-stu-id="8f025-176">If you know certain columns are not going to be in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="8f025-177">Per creare statistiche a colonna singola su ogni colonna di ogni tabella, è possibile usare l'esempio di codice di stored procedure `prc_sqldw_create_stats` riportato nell'articolo relativo alle [statistiche][statistics].</span><span class="sxs-lookup"><span data-stu-id="8f025-177">If you decide to create single-column statistics on every column of every table, you can use the stored procedure code sample `prc_sqldw_create_stats` in the [statistics][statistics] article.</span></span>

<span data-ttu-id="8f025-178">L'esempio seguente è un buon punto di partenza per la creazione delle statistiche.</span><span class="sxs-lookup"><span data-stu-id="8f025-178">The following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="8f025-179">Qui vengono create statistiche a colonna singola su ogni colonna nella tabella della dimensione e su ogni colonna di join nelle tabelle dei fatti.</span><span class="sxs-lookup"><span data-stu-id="8f025-179">It creates single-column statistics on each column in the dimension table, and on each joining column in the fact tables.</span></span> <span data-ttu-id="8f025-180">È sempre possibile aggiungere in un secondo momento statistiche a colonna singola o a più colonne per altre colonne delle tabelle dei fatti.</span><span class="sxs-lookup"><span data-stu-id="8f025-180">You can always add single or multi-column statistics to other fact table columns later on.</span></span>

```sql
CREATE STATISTICS [stat_cso_DimProduct_AvailableForSaleDate] ON [cso].[DimProduct]([AvailableForSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_BrandName] ON [cso].[DimProduct]([BrandName]);
CREATE STATISTICS [stat_cso_DimProduct_ClassID] ON [cso].[DimProduct]([ClassID]);
CREATE STATISTICS [stat_cso_DimProduct_ClassName] ON [cso].[DimProduct]([ClassName]);
CREATE STATISTICS [stat_cso_DimProduct_ColorID] ON [cso].[DimProduct]([ColorID]);
CREATE STATISTICS [stat_cso_DimProduct_ColorName] ON [cso].[DimProduct]([ColorName]);
CREATE STATISTICS [stat_cso_DimProduct_ETLLoadID] ON [cso].[DimProduct]([ETLLoadID]);
CREATE STATISTICS [stat_cso_DimProduct_ImageURL] ON [cso].[DimProduct]([ImageURL]);
CREATE STATISTICS [stat_cso_DimProduct_LoadDate] ON [cso].[DimProduct]([LoadDate]);
CREATE STATISTICS [stat_cso_DimProduct_Manufacturer] ON [cso].[DimProduct]([Manufacturer]);
CREATE STATISTICS [stat_cso_DimProduct_ProductDescription] ON [cso].[DimProduct]([ProductDescription]);
CREATE STATISTICS [stat_cso_DimProduct_ProductKey] ON [cso].[DimProduct]([ProductKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductLabel] ON [cso].[DimProduct]([ProductLabel]);
CREATE STATISTICS [stat_cso_DimProduct_ProductName] ON [cso].[DimProduct]([ProductName]);
CREATE STATISTICS [stat_cso_DimProduct_ProductSubcategoryKey] ON [cso].[DimProduct]([ProductSubcategoryKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductURL] ON [cso].[DimProduct]([ProductURL]);
CREATE STATISTICS [stat_cso_DimProduct_Size] ON [cso].[DimProduct]([Size]);
CREATE STATISTICS [stat_cso_DimProduct_SizeRange] ON [cso].[DimProduct]([SizeRange]);
CREATE STATISTICS [stat_cso_DimProduct_SizeUnitMeasureID] ON [cso].[DimProduct]([SizeUnitMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_Status] ON [cso].[DimProduct]([Status]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeID] ON [cso].[DimProduct]([StockTypeID]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeName] ON [cso].[DimProduct]([StockTypeName]);
CREATE STATISTICS [stat_cso_DimProduct_StopSaleDate] ON [cso].[DimProduct]([StopSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_StyleID] ON [cso].[DimProduct]([StyleID]);
CREATE STATISTICS [stat_cso_DimProduct_StyleName] ON [cso].[DimProduct]([StyleName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitCost] ON [cso].[DimProduct]([UnitCost]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureID] ON [cso].[DimProduct]([UnitOfMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureName] ON [cso].[DimProduct]([UnitOfMeasureName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitPrice] ON [cso].[DimProduct]([UnitPrice]);
CREATE STATISTICS [stat_cso_DimProduct_UpdateDate] ON [cso].[DimProduct]([UpdateDate]);
CREATE STATISTICS [stat_cso_DimProduct_Weight] ON [cso].[DimProduct]([Weight]);
CREATE STATISTICS [stat_cso_DimProduct_WeightUnitMeasureID] ON [cso].[DimProduct]([WeightUnitMeasureID]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CurrencyKey] ON [cso].[FactOnlineSales]([CurrencyKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CustomerKey] ON [cso].[FactOnlineSales]([CustomerKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_DateKey] ON [cso].[FactOnlineSales]([DateKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_OnlineSalesKey] ON [cso].[FactOnlineSales]([OnlineSalesKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_ProductKey] ON [cso].[FactOnlineSales]([ProductKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_PromotionKey] ON [cso].[FactOnlineSales]([PromotionKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_StoreKey] ON [cso].[FactOnlineSales]([StoreKey]);
```

## <a name="achievement-unlocked"></a><span data-ttu-id="8f025-181">Obiettivo raggiunto</span><span class="sxs-lookup"><span data-stu-id="8f025-181">Achievement unlocked!</span></span>
<span data-ttu-id="8f025-182">I dati pubblici sono stati caricati correttamente in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8f025-182">You have successfully loaded public data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="8f025-183">Ottimo lavoro.</span><span class="sxs-lookup"><span data-stu-id="8f025-183">Great job!</span></span>

<span data-ttu-id="8f025-184">Ora è possibile iniziare a eseguire le query sulle tabelle prendendo spunto dalle query seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f025-184">You can now start querying the tables using queries like the following:</span></span>

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a><span data-ttu-id="8f025-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8f025-185">Next steps</span></span>
<span data-ttu-id="8f025-186">Per caricare i dati completi del data warehouse di Contoso Retail, usare lo script disponibile nei suggerimenti per lo sviluppo e vedere la [panoramica sullo sviluppo per SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="8f025-186">To load the full Contoso Retail Data Warehouse data, use the script in For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/en-us/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/en-us/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load the full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
