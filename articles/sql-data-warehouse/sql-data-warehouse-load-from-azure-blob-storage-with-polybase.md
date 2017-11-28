---
title: aaaLoad dal data warehouse di blob di Azure tooAzure | Documenti Microsoft
description: Informazioni su come dati di tooload toouse PolyBase da Azure nell'archiviazione blob in SQL Data Warehouse. Caricare alcune tabelle di dati pubblici nello schema di Data Warehouse di Contoso Retail hello.
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
ms.openlocfilehash: 4b4978ccefa4d55ff5c89fba84c5e705422ddbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a><span data-ttu-id="4a065-104">Caricare dati dall’archiviazione BLOB di Azure in un SQL Data Warehouse (PolyBase)</span><span class="sxs-lookup"><span data-stu-id="4a065-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4a065-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="4a065-105">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="4a065-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="4a065-106">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

<span data-ttu-id="4a065-107">Utilizzare i dati di tooload comandi PolyBase e T-SQL dall'archiviazione blob di Azure in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4a065-107">Use PolyBase and T-SQL commands tooload data from Azure blob storage into Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="4a065-108">tookeep semplice, in questa esercitazione carica due tabelle da un Blob di archiviazione di Azure pubblico nello schema di Data Warehouse di Contoso Retail hello.</span><span class="sxs-lookup"><span data-stu-id="4a065-108">tookeep it simple, this tutorial loads two tables from a public Azure Storage Blob into hello Contoso Retail Data Warehouse schema.</span></span> <span data-ttu-id="4a065-109">tooload hello set di dati completo, eseguire l'esempio hello [carico hello completa del Data Warehouse di Contoso Retail] [ Load hello full Contoso Retail Data Warehouse] dal repository di Microsoft SQL Server Samples hello.</span><span class="sxs-lookup"><span data-stu-id="4a065-109">tooload hello full data set, run hello example [Load hello full Contoso Retail Data Warehouse][Load hello full Contoso Retail Data Warehouse] from hello Microsoft SQL Server Samples repository.</span></span>

<span data-ttu-id="4a065-110">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="4a065-110">In this tutorial you will:</span></span>

1. <span data-ttu-id="4a065-111">Configurare PolyBase tooload dall'archiviazione blob di Azure</span><span class="sxs-lookup"><span data-stu-id="4a065-111">Configure PolyBase tooload from Azure blob storage</span></span>
2. <span data-ttu-id="4a065-112">Caricare dati pubblici nel database</span><span class="sxs-lookup"><span data-stu-id="4a065-112">Load public data into your database</span></span>
3. <span data-ttu-id="4a065-113">Eseguire ottimizzazioni dopo il completamento carico hello.</span><span class="sxs-lookup"><span data-stu-id="4a065-113">Perform optimizations after hello load is finished.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4a065-114">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="4a065-114">Before you begin</span></span>
<span data-ttu-id="4a065-115">toorun questa esercitazione, è necessario un account di Azure che già dispone di un database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4a065-115">toorun this tutorial, you need an Azure account that already has a SQL Data Warehouse database.</span></span> <span data-ttu-id="4a065-116">In caso contrario, vedere l'articolo su come [creare un'istanza di SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="4a065-116">If you don't already have this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>

## <a name="1-configure-hello-data-source"></a><span data-ttu-id="4a065-117">1. Configurare l'origine dati hello</span><span class="sxs-lookup"><span data-stu-id="4a065-117">1. Configure hello data source</span></span>
<span data-ttu-id="4a065-118">PolyBase Usa percorso hello toodefine oggetti esterni di T-SQL e degli attributi di dati esterni hello.</span><span class="sxs-lookup"><span data-stu-id="4a065-118">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="4a065-119">le definizioni di oggetto esterno Hello vengono archiviate in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4a065-119">hello external object definitions are stored in SQL Data Warehouse.</span></span> <span data-ttu-id="4a065-120">Hello dati vengono archiviati esternamente.</span><span class="sxs-lookup"><span data-stu-id="4a065-120">hello data itself is stored externally.</span></span>

### <a name="11-create-a-credential"></a><span data-ttu-id="4a065-121">1.1.</span><span class="sxs-lookup"><span data-stu-id="4a065-121">1.1.</span></span> <span data-ttu-id="4a065-122">Creare una credenziale</span><span class="sxs-lookup"><span data-stu-id="4a065-122">Create a credential</span></span>
<span data-ttu-id="4a065-123">**Ignorare questo passaggio** se si siano caricando dati pubblici di hello Contoso.</span><span class="sxs-lookup"><span data-stu-id="4a065-123">**Skip this step** if you are loading hello Contoso public data.</span></span> <span data-ttu-id="4a065-124">Non è necessario proteggere l'accesso toohello pubblica dati perché è già tooanyone accessibile.</span><span class="sxs-lookup"><span data-stu-id="4a065-124">You don't need secure access toohello public data since it is already accessible tooanyone.</span></span>

<span data-ttu-id="4a065-125">**Non ignorare questo passaggio** se si utilizza questa esercitazione come modello per il caricamento dei dati personali.</span><span class="sxs-lookup"><span data-stu-id="4a065-125">**Don't skip this step** if you are using this tutorial as a template for loading your own data.</span></span> <span data-ttu-id="4a065-126">dati tooaccess tramite una credenziale, utilizzare hello seguenti script credenziali con ambito database toocreate e utilizzano quando si definisce una posizione di hello dell'origine dati di hello.</span><span class="sxs-lookup"><span data-stu-id="4a065-126">tooaccess data through a credential, use hello following script toocreate a database-scoped credential, and then use it when defining hello location of hello data source.</span></span>

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication tooAzure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);
```

<span data-ttu-id="4a065-127">Ignorare toostep 2.</span><span class="sxs-lookup"><span data-stu-id="4a065-127">Skip toostep 2.</span></span>

### <a name="12-create-hello-external-data-source"></a><span data-ttu-id="4a065-128">1.2.</span><span class="sxs-lookup"><span data-stu-id="4a065-128">1.2.</span></span> <span data-ttu-id="4a065-129">Creare l'origine dati esterna hello</span><span class="sxs-lookup"><span data-stu-id="4a065-129">Create hello external data source</span></span>
<span data-ttu-id="4a065-130">Utilizzare questo [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] comando percorso hello toostore di dati hello e hello tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="4a065-130">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span> 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> <span data-ttu-id="4a065-131">Se si sceglie toomake il pubblico di contenitori di archiviazione blob di azure, tenere presente che il proprietario di dati di hello verranno addebitati per i dati di costi di uscita quando i dati lasciano centro dati hello.</span><span class="sxs-lookup"><span data-stu-id="4a065-131">If you choose toomake your azure blob storage containers public, remember that as hello data owner you will be charged for data egress charges when data leaves hello data center.</span></span> 
> 
> 

## <a name="2-configure-data-format"></a><span data-ttu-id="4a065-132">2. Configurare il formato dei dati</span><span class="sxs-lookup"><span data-stu-id="4a065-132">2. Configure data format</span></span>
<span data-ttu-id="4a065-133">Hello dati vengono archiviati nel file di testo nell'archiviazione blob di Azure e ogni campo è separato con un delimitatore.</span><span class="sxs-lookup"><span data-stu-id="4a065-133">hello data is stored in text files in Azure blob storage, and each field is separated with a delimiter.</span></span> <span data-ttu-id="4a065-134">Eseguire questo [CREATE EXTERNAL FILE FORMAT] [ CREATE EXTERNAL FILE FORMAT] comando nel formato hello toospecify dei dati di hello nei file di testo hello.</span><span class="sxs-lookup"><span data-stu-id="4a065-134">Run this [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] command toospecify hello format of hello data in hello text files.</span></span> <span data-ttu-id="4a065-135">Hello Contoso dati non compresso e pipe delimitato.</span><span class="sxs-lookup"><span data-stu-id="4a065-135">hello Contoso data is uncompressed and pipe delimited.</span></span>

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

## <a name="3-create-hello-external-tables"></a><span data-ttu-id="4a065-136">3. Creare tabelle esterne di hello</span><span class="sxs-lookup"><span data-stu-id="4a065-136">3. Create hello external tables</span></span>
<span data-ttu-id="4a065-137">Ora che è stata specificata l'origine e file di formato di dati di hello, si è pronti toocreate tabelle esterne di hello.</span><span class="sxs-lookup"><span data-stu-id="4a065-137">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> 

### <a name="31-create-a-schema-for-hello-data"></a><span data-ttu-id="4a065-138">3.1.</span><span class="sxs-lookup"><span data-stu-id="4a065-138">3.1.</span></span> <span data-ttu-id="4a065-139">Creare uno schema per i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="4a065-139">Create a schema for hello data.</span></span>
<span data-ttu-id="4a065-140">toocreate un hello toostore sul posto Contoso dati nel database, creare uno schema.</span><span class="sxs-lookup"><span data-stu-id="4a065-140">toocreate a place toostore hello Contoso data in your database, create a schema.</span></span>

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-hello-external-tables"></a><span data-ttu-id="4a065-141">3.2.</span><span class="sxs-lookup"><span data-stu-id="4a065-141">3.2.</span></span> <span data-ttu-id="4a065-142">Creare tabelle esterne di hello.</span><span class="sxs-lookup"><span data-stu-id="4a065-142">Create hello external tables.</span></span>
<span data-ttu-id="4a065-143">Eseguire questo hello toocreate script DimProduct e FactOnlineSales tabelle esterne.</span><span class="sxs-lookup"><span data-stu-id="4a065-143">Run this script toocreate hello DimProduct and FactOnlineSales external tables.</span></span> <span data-ttu-id="4a065-144">Obiettivo qui è la definizione di nomi di colonna e tipi di dati e associarli toohello percorso e il formato di file di archiviazione blob di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4a065-144">All we are doing here is defining column names and data types, and binding them toohello location and format of hello Azure blob storage files.</span></span> <span data-ttu-id="4a065-145">definizione di Hello viene archiviato in SQL Data Warehouse e dati hello sono ancora in hello Blob di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a065-145">hello definition is stored in SQL Data Warehouse and hello data is still in hello Azure Storage Blob.</span></span>

<span data-ttu-id="4a065-146">Hello **percorso** parametro è la cartella hello nella cartella radice hello hello Blob di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4a065-146">hello  **LOCATION** parameter is hello folder under hello root folder in hello Azure Storage Blob.</span></span> <span data-ttu-id="4a065-147">Ogni tabella è in una cartella diversa.</span><span class="sxs-lookup"><span data-stu-id="4a065-147">Each table is in a different folder.</span></span>

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

## <a name="4-load-hello-data"></a><span data-ttu-id="4a065-148">4. Caricare i dati di hello</span><span class="sxs-lookup"><span data-stu-id="4a065-148">4. Load hello data</span></span>
<span data-ttu-id="4a065-149">Non sussiste dati esterni di tooaccess modi diversi.</span><span class="sxs-lookup"><span data-stu-id="4a065-149">There's different ways tooaccess external data.</span></span>  <span data-ttu-id="4a065-150">È possibile eseguire query sui dati direttamente dalla tabella esterna hello, caricare i dati di hello in nuove tabelle di database o aggiungere tabelle di database tooexisting dati esterni.</span><span class="sxs-lookup"><span data-stu-id="4a065-150">You can query data directly from hello external table, load hello data into new database tables, or add external data tooexisting database tables.</span></span>  

### <a name="41-create-a-new-schema"></a><span data-ttu-id="4a065-151">4.1.</span><span class="sxs-lookup"><span data-stu-id="4a065-151">4.1.</span></span> <span data-ttu-id="4a065-152">Crea un nuovo schema</span><span class="sxs-lookup"><span data-stu-id="4a065-152">Create a new schema</span></span>
<span data-ttu-id="4a065-153">CTAS crea una nuova tabella contenente i dati.</span><span class="sxs-lookup"><span data-stu-id="4a065-153">CTAS creates a new table that contains data.</span></span>  <span data-ttu-id="4a065-154">Innanzitutto, creare uno schema per i dati di contoso hello.</span><span class="sxs-lookup"><span data-stu-id="4a065-154">First, create a schema for hello contoso data.</span></span>

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-hello-data-into-new-tables"></a><span data-ttu-id="4a065-155">4.2.</span><span class="sxs-lookup"><span data-stu-id="4a065-155">4.2.</span></span> <span data-ttu-id="4a065-156">Caricamento dei dati hello nelle nuove tabelle</span><span class="sxs-lookup"><span data-stu-id="4a065-156">Load hello data into new tables</span></span>
<span data-ttu-id="4a065-157">dati tooload da Azure nell'archiviazione blob e salvarlo in una tabella all'interno del database, utilizzare hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] istruzione.</span><span class="sxs-lookup"><span data-stu-id="4a065-157">tooload data from Azure blob storage and save it in a table inside of your database, use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="4a065-158">Caricamento con un'istruzione CTAS sfrutta hello tipizzata tabelle esterne si dispone di dati di hello created.tooload solo nelle nuove tabelle, utilizzare uno [un'istruzione CTAS] [ CTAS] istruzione per ogni tabella.</span><span class="sxs-lookup"><span data-stu-id="4a065-158">Loading with CTAS leverages hello strongly typed external tables you have just created.tooload hello data into new tables, use one [CTAS][CTAS] statement per table.</span></span> 
 
<span data-ttu-id="4a065-159">Un'istruzione CTAS crea una nuova tabella e popolarla con i risultati di hello di un'istruzione select.</span><span class="sxs-lookup"><span data-stu-id="4a065-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="4a065-160">Un'istruzione CTAS definisce hello nuova tabella toohave hello stessi colonne e tipi di dati come risultato di hello hello istruzione select.</span><span class="sxs-lookup"><span data-stu-id="4a065-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="4a065-161">Se si selezionano tutte le colonne di hello da una tabella esterna, nuova tabella hello sarà una replica di colonne di hello e tipi di dati nella tabella esterna hello.</span><span class="sxs-lookup"><span data-stu-id="4a065-161">If you select all hello columns from an external table, hello new table will be a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="4a065-162">In questo esempio è creare dimensioni hello e tabella dei fatti di hello come hash tabelle distribuite.</span><span class="sxs-lookup"><span data-stu-id="4a065-162">In this example, we create both hello dimension and hello fact table as hash distributed tables.</span></span> 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-hello-load-progress"></a><span data-ttu-id="4a065-163">4.3 hello avanzamento carico</span><span class="sxs-lookup"><span data-stu-id="4a065-163">4.3 Track hello load progress</span></span>
<span data-ttu-id="4a065-164">È possibile monitorare lo stato di avanzamento hello del carico utilizzando viste a gestione dinamica (DMV).</span><span class="sxs-lookup"><span data-stu-id="4a065-164">You can track hello progress of your load using dynamic management views (DMVs).</span></span> 

```sql
-- toosee all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- toosee a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- tootrack bytes and files
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

## <a name="5-optimize-columnstore-compression"></a><span data-ttu-id="4a065-165">5. Ottimizzare la compressione columnstore</span><span class="sxs-lookup"><span data-stu-id="4a065-165">5. Optimize columnstore compression</span></span>
<span data-ttu-id="4a065-166">Per impostazione predefinita, SQL Data Warehouse vengono archiviati nella tabella hello come un indice columnstore cluster.</span><span class="sxs-lookup"><span data-stu-id="4a065-166">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="4a065-167">Al termine di un carico, alcune righe di dati hello potrebbe non compresso nel columnstore hello.</span><span class="sxs-lookup"><span data-stu-id="4a065-167">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="4a065-168">Esiste una serie di motivi per cui questo può verificarsi.</span><span class="sxs-lookup"><span data-stu-id="4a065-168">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="4a065-169">vedere, più toolearn [gestire gli indici columnstore][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="4a065-169">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="4a065-170">le prestazioni delle query toooptimize e la compressione columnstore dopo un caricamento, ricompilare tutte le righe di hello hello tabella tooforce hello columnstore indice toocompress.</span><span class="sxs-lookup"><span data-stu-id="4a065-170">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span> 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

<span data-ttu-id="4a065-171">Per ulteriori informazioni sulla gestione degli indici columnstore, vedere hello [gestire gli indici columnstore] [ manage columnstore indexes] articolo.</span><span class="sxs-lookup"><span data-stu-id="4a065-171">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="6-optimize-statistics"></a><span data-ttu-id="4a065-172">6. Ottimizzare le statistiche</span><span class="sxs-lookup"><span data-stu-id="4a065-172">6. Optimize statistics</span></span>
<span data-ttu-id="4a065-173">Le statistiche di colonna singola toocreate è immediatamente dopo un carico.</span><span class="sxs-lookup"><span data-stu-id="4a065-173">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="4a065-174">Sono disponibili alcune opzioni per le statistiche.</span><span class="sxs-lookup"><span data-stu-id="4a065-174">There are some choices for statistics.</span></span> <span data-ttu-id="4a065-175">Ad esempio, se si creano statistiche a colonna singola su tutte le colonne potrebbe richiedere un tempo toorebuild tutte le statistiche di hello.</span><span class="sxs-lookup"><span data-stu-id="4a065-175">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="4a065-176">Se si è certi di che alcune colonne non stanno toobe nei predicati di query, è possibile ignorare la creazione di statistiche di tali colonne.</span><span class="sxs-lookup"><span data-stu-id="4a065-176">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="4a065-177">Se si decide di statistiche di colonna singola toocreate ogni colonna di ogni tabella, è possibile utilizzare l'esempio di codice hello stored procedure `prc_sqldw_create_stats` in hello [statistiche] [ statistics] articolo.</span><span class="sxs-lookup"><span data-stu-id="4a065-177">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="4a065-178">Hello di esempio seguente è un buon punto di partenza per la creazione di statistiche.</span><span class="sxs-lookup"><span data-stu-id="4a065-178">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="4a065-179">Crea statistiche a colonna singola su ogni colonna nella tabella delle dimensioni hello e su ogni colonna di join nelle tabelle dei fatti hello.</span><span class="sxs-lookup"><span data-stu-id="4a065-179">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="4a065-180">È sempre possibile aggiungere colonne della tabella dei fatti tooother le statistiche di uno o più colonne in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="4a065-180">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>

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

## <a name="achievement-unlocked"></a><span data-ttu-id="4a065-181">Obiettivo raggiunto</span><span class="sxs-lookup"><span data-stu-id="4a065-181">Achievement unlocked!</span></span>
<span data-ttu-id="4a065-182">I dati pubblici sono stati caricati correttamente in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4a065-182">You have successfully loaded public data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="4a065-183">Ottimo lavoro.</span><span class="sxs-lookup"><span data-stu-id="4a065-183">Great job!</span></span>

<span data-ttu-id="4a065-184">È ora possibile avviare una query sulle tabelle hello tramite query hello seguente:</span><span class="sxs-lookup"><span data-stu-id="4a065-184">You can now start querying hello tables using queries like hello following:</span></span>

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a><span data-ttu-id="4a065-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4a065-185">Next steps</span></span>
<span data-ttu-id="4a065-186">tooload hello completa del Data Warehouse di Contoso Retail di dati, utilizzare script hello in per ulteriori suggerimenti per lo sviluppo, vedere [Cenni preliminari sullo sviluppo di SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="4a065-186">tooload hello full Contoso Retail Data Warehouse data, use hello script in For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
