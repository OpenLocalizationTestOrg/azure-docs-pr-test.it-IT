---
title: dati aaaLoad da SQL Server in Azure SQL Data Warehouse (PolyBase) | Documenti Microsoft
description: Utilizza bcp tooexport dati da file tooflat di SQL Server, archiviazione blob di AZCopy tooimport dati tooAzure e dati di PolyBase tooingest hello in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 860c86e0-90f7-492c-9a84-1bdd3d1735cd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1346fb016e0538a44426671bf4e29358cb24f7ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a>Caricare dati con PolyBase in SQL Data Warehouse
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

Questa esercitazione viene illustrato come dati tooload in SQL Data Warehouse tramite AzCopy e PolyBase. Al termine, si sarà in grado di:

* Utilizzare l'archiviazione blob di AzCopy toocopy dati tooAzure
* Creare oggetti di database i dati di hello toodefine
* Eseguire una query di T-SQL tooload hello dati

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>Prerequisiti
toostep di questa esercitazione, è necessario

* Un database di SQL Data Warehouse.
* Un account di archiviazione di Azure di tipo Archiviazione con ridondanza locale Standard (Standard-LRS), Archiviazione con ridondanza geografica Standard (Standard-GRS) o Archiviazione con ridondanza geografica e accesso in lettura Standard (Standard-RAGRS).
* Utilità da riga di comando di AzCopy. Scaricare e installare hello [versione più recente di AzCopy] [ latest version of AzCopy] che viene installato con hello strumenti di archiviazione di Microsoft Azure.
  
    ![Strumenti di archiviazione di Azure](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a>Passaggio 1: Aggiungere archiviazione blob tooAzure dati di esempio
Dati tooload degli ordini, è necessario tooput alcuni dati di esempio in una risorsa di archiviazione blob di Azure. In questo passaggio un BLOB di Archiviazione di Azure viene popolato con dati di esempio. In un secondo momento, si utilizzerà PolyBase tooload dati di esempio nel database di SQL Data Warehouse.

### <a name="a-prepare-a-sample-text-file"></a>R. Preparare un file di testo di esempio
tooprepare un file di testo di esempio:

1. Aprire Blocco note e copiare hello seguenti righe di dati in un nuovo file. Salvare questa directory temporanea locale tooyour come temp%\DimDate2.txt %.

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="b-find-your-blob-service-endpoint"></a>B. Individuare l'endpoint di servizio BLOB
toofind l'endpoint del servizio blob:

1. Hello portale di Azure selezionare **Sfoglia** > **gli account di archiviazione**.
2. Fare clic su account di archiviazione hello da toouse.
3. Nel Pannello di account di archiviazione hello, fare clic su BLOB
   
    ![Selezione dei BLOB](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. Salvare l'URL dell'endpoint di servizio BLOB per un momento successivo.
   
    ![Endpoint di servizio BLOB](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a>C. Individuare la chiave di archiviazione di Azure
toofind la chiave di archiviazione di Azure:

1. Hello portale di Azure, selezionare **Sfoglia** > **gli account di archiviazione**.
2. Fare clic su account di archiviazione hello da toouse.
3. Selezionare **Tutte le impostazioni** > **Chiavi di accesso**.
4. Fare clic su hello copia casella toocopy uno degli Appunti toohello le chiavi di accesso.
   
    ![Copia della chiave di archiviazione di Azure](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a>D. Copiare l'archiviazione di blob tooAzure file esempio hello
toocopy dell'archiviazione blob tooAzure dei dati:

1. Aprire un prompt dei comandi e cambiare directory di installazione di directory toohello AzCopy. Questo comando Modifica toohello directory di installazione predefinita in un client di Windows a 64 bit.
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. Eseguire i seguenti file di comando tooupload hello hello. Specificare l'URL dell'endpoint di servizio BLOB per <blob service endpoint URL> e la chiave dell'account di archiviazione di Azure per <azure_storage_account_key>.
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

Vedere anche [introduzione hello utilità della riga di comando di AzCopy][latest version of AzCopy].

### <a name="e-explore-your-blob-storage-container"></a>E. Esplorare il contenitore di archiviazione BLOB
file hello toosee caricato tooblob archiviazione:

1. Tornare blade di tooyour Blob del servizio.
2. In Contenitori fare doppio clic su **datacontainer**.
3. dati di tooyour tooexplore hello del percorso, fare clic su cartella hello **datedimension** e verrà visualizzato il file caricato **DimDate2.txt**.
4. Fare clic su proprietà tooview, **DimDate2.txt**.
5. Si noti che nel Pannello proprietà di hello Blob, è possibile scaricare o eliminare file hello.
   
    ![Visualizzazione del BLOB di archiviazione di Azure](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a>Passaggio 2: Creare una tabella esterna per i dati di esempio hello
In questa sezione viene creata una tabella esterna che definisce i dati di esempio hello.

PolyBase utilizza i dati di tabelle esterne tooaccess nell'archiviazione blob di Azure. Poiché i dati di hello non vengono archiviati all'interno di SQL Data Warehouse, PolyBase gestisce i dati esterni toohello di autenticazione utilizzando le credenziali con ambito database.

esempio Hello in questo passaggio utilizza questi toocreate istruzioni Transact-SQL una tabella esterna.

* [Creare la chiave Master (Transact-SQL)] [ Create Master Key (Transact-SQL)] credenziali con ambito segreto hello tooencrypt del database.
* [Creare credenziali con ambito Database (Transact-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify informazioni di autenticazione per l'account di archiviazione di Azure.
* [Creare l'origine dati esterna (Transact-SQL)] [ Create External Data Source (Transact-SQL)] percorso hello toospecify dello spazio di archiviazione blob di Azure.
* [Creare un formato di File esterni (Transact-SQL)] [ Create External File Format (Transact-SQL)] formato hello toospecify dei dati.
* [Creare una tabella esterna (Transact-SQL)] [ Create External Table (Transact-SQL)] toospecify definizione della tabella hello e il percorso di hello dati.

Eseguire questa query nel database di SQL Data Warehouse. Crea una tabella esterna denominata DimDate2External nello schema dbo hello che punta a dati di esempio DimDate2.txt toohello nell'archiviazione blob di Azure hello.

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


-- D: Create an external file format
-- FORMAT_TYPE: Type of file format in Azure storage (supported: DELIMITEDTEXT, RCFILE, ORC, PARQUET).
-- FORMAT_OPTIONS: Specify field terminator, string delimiter, date format etc. for delimited text files.
-- Specify DATA_COMPRESSION method if data is compressed.

CREATE EXTERNAL FILE FORMAT TextFile
WITH (
    FORMAT_TYPE = DelimitedText,
    FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
);


-- E: Create hello external table
-- Specify column names and data types. This needs toomatch hello data in hello sample file.
-- LOCATION: Specify path toofile or directory that contains hello data (relative toohello blob container).
-- toopoint tooall files under hello blob container, use LOCATION='.'

CREATE EXTERNAL TABLE dbo.DimDate2External (
    DateId INT NOT NULL,
    CalendarQuarter TINYINT NOT NULL,
    FiscalQuarter TINYINT NOT NULL
)
WITH (
    LOCATION='/datedimension/',
    DATA_SOURCE=AzureStorage,
    FILE_FORMAT=TextFile
);


-- Run a query on hello external table

SELECT count(*) FROM dbo.DimDate2External;

```


In Esplora oggetti di SQL Server in Visual Studio, è possibile visualizzare il formato di file esterno hello, origine dati esterna e tabella DimDate2External hello.

![Visualizzazione della tabella esterna](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a>Passaggio 3: Caricare i dati in SQL Data Warehouse
Una volta creata la tabella esterna hello, è possibile caricare i dati di hello in una nuova tabella o inserirlo in una tabella esistente.

* dati hello tooload in una nuova tabella, eseguire hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] istruzione. nuova tabella Hello avranno le colonne di hello denominate query hello. i tipi di dati delle colonne hello Hello corrisponderà a tipi di dati hello nella definizione della tabella esterna hello.
* dati hello tooload in una tabella esistente, utilizzare hello [INSERT... SELECT (Transact-SQL)] [ INSERT...SELECT (Transact-SQL)] istruzione.

```sql
-- Load hello data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>Passaggio 4: Creare statistiche sui dati appena caricati
SQL Data Warehouse non crea automaticamente o aggiorna automaticamente le statistiche. Pertanto, tooachieve prestazioni elevate delle query, è importante innanzitutto caricano statistiche toocreate in ogni colonna di ogni tabella dopo hello. È inoltre importante tooupdate statistiche dopo aver apportato modifiche sostanziali in dati hello.

Questo esempio Crea statistiche a colonna singola nella tabella DimDate2 nuovo hello.

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

vedere, più toolearn [statistiche][Statistics].  

## <a name="next-steps"></a>Passaggi successivi
Vedere hello [Guida a PolyBase] [ PolyBase guide] per ulteriori informazioni che è necessario conoscere quando si sviluppa una soluzione che usa PolyBase.

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
[latest version of AzCopy]:../storage/common/storage-use-azcopy.md

<!--External references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx


[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]:https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189450.aspx
