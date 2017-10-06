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
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a>Caricare dati dall’archiviazione BLOB di Azure in un SQL Data Warehouse (PolyBase)
> [!div class="op_single_selector"]
> * [Data Factory](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [PolyBase](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

Utilizzare i dati di tooload comandi PolyBase e T-SQL dall'archiviazione blob di Azure in Azure SQL Data Warehouse. 

tookeep semplice, in questa esercitazione carica due tabelle da un Blob di archiviazione di Azure pubblico nello schema di Data Warehouse di Contoso Retail hello. tooload hello set di dati completo, eseguire l'esempio hello [carico hello completa del Data Warehouse di Contoso Retail] [ Load hello full Contoso Retail Data Warehouse] dal repository di Microsoft SQL Server Samples hello.

In questa esercitazione si apprenderà come:

1. Configurare PolyBase tooload dall'archiviazione blob di Azure
2. Caricare dati pubblici nel database
3. Eseguire ottimizzazioni dopo il completamento carico hello.

## <a name="before-you-begin"></a>Prima di iniziare
toorun questa esercitazione, è necessario un account di Azure che già dispone di un database di SQL Data Warehouse. In caso contrario, vedere l'articolo su come [creare un'istanza di SQL Data Warehouse][Create a SQL Data Warehouse].

## <a name="1-configure-hello-data-source"></a>1. Configurare l'origine dati hello
PolyBase Usa percorso hello toodefine oggetti esterni di T-SQL e degli attributi di dati esterni hello. le definizioni di oggetto esterno Hello vengono archiviate in SQL Data Warehouse. Hello dati vengono archiviati esternamente.

### <a name="11-create-a-credential"></a>1.1. Creare una credenziale
**Ignorare questo passaggio** se si siano caricando dati pubblici di hello Contoso. Non è necessario proteggere l'accesso toohello pubblica dati perché è già tooanyone accessibile.

**Non ignorare questo passaggio** se si utilizza questa esercitazione come modello per il caricamento dei dati personali. dati tooaccess tramite una credenziale, utilizzare hello seguenti script credenziali con ambito database toocreate e utilizzano quando si definisce una posizione di hello dell'origine dati di hello.

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

Ignorare toostep 2.

### <a name="12-create-hello-external-data-source"></a>1.2. Creare l'origine dati esterna hello
Utilizzare questo [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] comando percorso hello toostore di dati hello e hello tipo di dati. 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> Se si sceglie toomake il pubblico di contenitori di archiviazione blob di azure, tenere presente che il proprietario di dati di hello verranno addebitati per i dati di costi di uscita quando i dati lasciano centro dati hello. 
> 
> 

## <a name="2-configure-data-format"></a>2. Configurare il formato dei dati
Hello dati vengono archiviati nel file di testo nell'archiviazione blob di Azure e ogni campo è separato con un delimitatore. Eseguire questo [CREATE EXTERNAL FILE FORMAT] [ CREATE EXTERNAL FILE FORMAT] comando nel formato hello toospecify dei dati di hello nei file di testo hello. Hello Contoso dati non compresso e pipe delimitato.

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

## <a name="3-create-hello-external-tables"></a>3. Creare tabelle esterne di hello
Ora che è stata specificata l'origine e file di formato di dati di hello, si è pronti toocreate tabelle esterne di hello. 

### <a name="31-create-a-schema-for-hello-data"></a>3.1. Creare uno schema per i dati di hello.
toocreate un hello toostore sul posto Contoso dati nel database, creare uno schema.

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-hello-external-tables"></a>3.2. Creare tabelle esterne di hello.
Eseguire questo hello toocreate script DimProduct e FactOnlineSales tabelle esterne. Obiettivo qui è la definizione di nomi di colonna e tipi di dati e associarli toohello percorso e il formato di file di archiviazione blob di Azure hello. definizione di Hello viene archiviato in SQL Data Warehouse e dati hello sono ancora in hello Blob di archiviazione di Azure.

Hello **percorso** parametro è la cartella hello nella cartella radice hello hello Blob di archiviazione di Azure. Ogni tabella è in una cartella diversa.

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

## <a name="4-load-hello-data"></a>4. Caricare i dati di hello
Non sussiste dati esterni di tooaccess modi diversi.  È possibile eseguire query sui dati direttamente dalla tabella esterna hello, caricare i dati di hello in nuove tabelle di database o aggiungere tabelle di database tooexisting dati esterni.  

### <a name="41-create-a-new-schema"></a>4.1. Crea un nuovo schema
CTAS crea una nuova tabella contenente i dati.  Innanzitutto, creare uno schema per i dati di contoso hello.

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-hello-data-into-new-tables"></a>4.2. Caricamento dei dati hello nelle nuove tabelle
dati tooload da Azure nell'archiviazione blob e salvarlo in una tabella all'interno del database, utilizzare hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] istruzione. Caricamento con un'istruzione CTAS sfrutta hello tipizzata tabelle esterne si dispone di dati di hello created.tooload solo nelle nuove tabelle, utilizzare uno [un'istruzione CTAS] [ CTAS] istruzione per ogni tabella. 
 
Un'istruzione CTAS crea una nuova tabella e popolarla con i risultati di hello di un'istruzione select. Un'istruzione CTAS definisce hello nuova tabella toohave hello stessi colonne e tipi di dati come risultato di hello hello istruzione select. Se si selezionano tutte le colonne di hello da una tabella esterna, nuova tabella hello sarà una replica di colonne di hello e tipi di dati nella tabella esterna hello.

In questo esempio è creare dimensioni hello e tabella dei fatti di hello come hash tabelle distribuite. 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-hello-load-progress"></a>4.3 hello avanzamento carico
È possibile monitorare lo stato di avanzamento hello del carico utilizzando viste a gestione dinamica (DMV). 

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

## <a name="5-optimize-columnstore-compression"></a>5. Ottimizzare la compressione columnstore
Per impostazione predefinita, SQL Data Warehouse vengono archiviati nella tabella hello come un indice columnstore cluster. Al termine di un carico, alcune righe di dati hello potrebbe non compresso nel columnstore hello.  Esiste una serie di motivi per cui questo può verificarsi. vedere, più toolearn [gestire gli indici columnstore][manage columnstore indexes].

le prestazioni delle query toooptimize e la compressione columnstore dopo un caricamento, ricompilare tutte le righe di hello hello tabella tooforce hello columnstore indice toocompress. 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

Per ulteriori informazioni sulla gestione degli indici columnstore, vedere hello [gestire gli indici columnstore] [ manage columnstore indexes] articolo.

## <a name="6-optimize-statistics"></a>6. Ottimizzare le statistiche
Le statistiche di colonna singola toocreate è immediatamente dopo un carico. Sono disponibili alcune opzioni per le statistiche. Ad esempio, se si creano statistiche a colonna singola su tutte le colonne potrebbe richiedere un tempo toorebuild tutte le statistiche di hello. Se si è certi di che alcune colonne non stanno toobe nei predicati di query, è possibile ignorare la creazione di statistiche di tali colonne.

Se si decide di statistiche di colonna singola toocreate ogni colonna di ogni tabella, è possibile utilizzare l'esempio di codice hello stored procedure `prc_sqldw_create_stats` in hello [statistiche] [ statistics] articolo.

Hello di esempio seguente è un buon punto di partenza per la creazione di statistiche. Crea statistiche a colonna singola su ogni colonna nella tabella delle dimensioni hello e su ogni colonna di join nelle tabelle dei fatti hello. È sempre possibile aggiungere colonne della tabella dei fatti tooother le statistiche di uno o più colonne in un secondo momento.

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

## <a name="achievement-unlocked"></a>Obiettivo raggiunto
I dati pubblici sono stati caricati correttamente in Azure SQL Data Warehouse. Ottimo lavoro.

È ora possibile avviare una query sulle tabelle hello tramite query hello seguente:

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a>Passaggi successivi
tooload hello completa del Data Warehouse di Contoso Retail di dati, utilizzare script hello in per ulteriori suggerimenti per lo sviluppo, vedere [Cenni preliminari sullo sviluppo di SQL Data Warehouse][SQL Data Warehouse development overview].

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
