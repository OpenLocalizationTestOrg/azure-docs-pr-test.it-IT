---
title: Nell'esercitazione di SQL Data Warehouse aaaPolyBase | Documenti Microsoft
description: "Vengono illustrate le novità PolyBase e come toouse per scenari di data warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 0a0103b4-ddd6-4d1e-87be-4965d6e99f3f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/01/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 3e680ec407c1d920dd59ea922b82c9208b5e9a84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="d1021-103">Caricare dati con PolyBase in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d1021-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d1021-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="d1021-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="d1021-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="d1021-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="d1021-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="d1021-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="d1021-107">BCP</span><span class="sxs-lookup"><span data-stu-id="d1021-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="d1021-108">Questa esercitazione viene illustrato come dati tooload in SQL Data Warehouse tramite PolyBase e AzCopy.</span><span class="sxs-lookup"><span data-stu-id="d1021-108">This tutorial shows how tooload data into SQL Data Warehouse using AzCopy and PolyBase.</span></span> <span data-ttu-id="d1021-109">Al termine, si sarà in grado di:</span><span class="sxs-lookup"><span data-stu-id="d1021-109">When finished, you will know how to:</span></span>

* <span data-ttu-id="d1021-110">Utilizzare l'archiviazione blob di AzCopy toocopy dati tooAzure</span><span class="sxs-lookup"><span data-stu-id="d1021-110">Use AzCopy toocopy data tooAzure blob storage</span></span>
* <span data-ttu-id="d1021-111">Creare oggetti di database i dati di hello toodefine</span><span class="sxs-lookup"><span data-stu-id="d1021-111">Create database objects toodefine hello data</span></span>
* <span data-ttu-id="d1021-112">Eseguire una query di T-SQL tooload hello dati</span><span class="sxs-lookup"><span data-stu-id="d1021-112">Run a T-SQL query tooload hello data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d1021-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d1021-113">Prerequisites</span></span>
<span data-ttu-id="d1021-114">toostep di questa esercitazione, è necessario</span><span class="sxs-lookup"><span data-stu-id="d1021-114">toostep through this tutorial, you need</span></span>

* <span data-ttu-id="d1021-115">Un database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d1021-115">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="d1021-116">Un account di archiviazione di Azure di tipo Archiviazione con ridondanza locale Standard (Standard-LRS), Archiviazione con ridondanza geografica Standard (Standard-GRS) o Archiviazione con ridondanza geografica e accesso in lettura Standard (Standard-RAGRS).</span><span class="sxs-lookup"><span data-stu-id="d1021-116">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="d1021-117">Utilità da riga di comando di AzCopy.</span><span class="sxs-lookup"><span data-stu-id="d1021-117">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="d1021-118">Scaricare e installare hello [versione più recente di AzCopy] [ latest version of AzCopy] che viene installato con hello strumenti di archiviazione di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d1021-118">Download and install hello [latest version of AzCopy][latest version of AzCopy] which is installed with hello Microsoft Azure Storage Tools.</span></span>
  
    ![Strumenti di archiviazione di Azure](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a><span data-ttu-id="d1021-120">Passaggio 1: Aggiungere archiviazione blob tooAzure dati di esempio</span><span class="sxs-lookup"><span data-stu-id="d1021-120">Step 1: Add sample data tooAzure blob storage</span></span>
<span data-ttu-id="d1021-121">Dati tooload degli ordini, è necessario tooput alcuni dati di esempio in una risorsa di archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1021-121">In order tooload data, we need tooput some sample data into an Azure blob storage.</span></span> <span data-ttu-id="d1021-122">In questo passaggio un BLOB di Archiviazione di Azure viene popolato con dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="d1021-122">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="d1021-123">In un secondo momento, si utilizzerà PolyBase tooload dati di esempio nel database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d1021-123">Later, we will use PolyBase tooload this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="d1021-124">R.</span><span class="sxs-lookup"><span data-stu-id="d1021-124">A.</span></span> <span data-ttu-id="d1021-125">Preparare un file di testo di esempio</span><span class="sxs-lookup"><span data-stu-id="d1021-125">Prepare a sample text file</span></span>
<span data-ttu-id="d1021-126">tooprepare un file di testo di esempio:</span><span class="sxs-lookup"><span data-stu-id="d1021-126">tooprepare a sample text file:</span></span>

1. <span data-ttu-id="d1021-127">Aprire Blocco note e copiare hello seguenti righe di dati in un nuovo file.</span><span class="sxs-lookup"><span data-stu-id="d1021-127">Open Notepad and copy hello following lines of data into a new file.</span></span> <span data-ttu-id="d1021-128">Salvare questa directory temporanea locale tooyour come temp%\DimDate2.txt %.</span><span class="sxs-lookup"><span data-stu-id="d1021-128">Save this tooyour local temp directory as %temp%\DimDate2.txt.</span></span>

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

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="d1021-129">B.</span><span class="sxs-lookup"><span data-stu-id="d1021-129">B.</span></span> <span data-ttu-id="d1021-130">Individuare l'endpoint di servizio BLOB</span><span class="sxs-lookup"><span data-stu-id="d1021-130">Find your blob service endpoint</span></span>
<span data-ttu-id="d1021-131">toofind l'endpoint del servizio blob:</span><span class="sxs-lookup"><span data-stu-id="d1021-131">toofind your blob service endpoint:</span></span>

1. <span data-ttu-id="d1021-132">Hello portale di Azure selezionare **Sfoglia** > **gli account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="d1021-132">From hello Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="d1021-133">Fare clic su account di archiviazione hello da toouse.</span><span class="sxs-lookup"><span data-stu-id="d1021-133">Click hello storage account you want toouse.</span></span>
3. <span data-ttu-id="d1021-134">Nel Pannello di account di archiviazione hello, fare clic su BLOB</span><span class="sxs-lookup"><span data-stu-id="d1021-134">In hello Storage account blade, click Blobs</span></span>
   
    ![Selezione dei BLOB](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="d1021-136">Salvare l'URL dell'endpoint di servizio BLOB per un momento successivo.</span><span class="sxs-lookup"><span data-stu-id="d1021-136">Save your blob service endpoint URL for later.</span></span>
   
    ![Endpoint di servizio BLOB](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="d1021-138">C.</span><span class="sxs-lookup"><span data-stu-id="d1021-138">C.</span></span> <span data-ttu-id="d1021-139">Individuare la chiave di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d1021-139">Find your Azure storage key</span></span>
<span data-ttu-id="d1021-140">toofind la chiave di archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="d1021-140">toofind your Azure storage key:</span></span>

1. <span data-ttu-id="d1021-141">Hello portale di Azure, selezionare **Sfoglia** > **gli account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="d1021-141">From hello Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="d1021-142">Fare clic su account di archiviazione hello da toouse.</span><span class="sxs-lookup"><span data-stu-id="d1021-142">Click on hello storage account you want toouse.</span></span>
3. <span data-ttu-id="d1021-143">Selezionare **Tutte le impostazioni** > **Chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="d1021-143">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="d1021-144">Fare clic su hello copia casella toocopy uno degli Appunti toohello le chiavi di accesso.</span><span class="sxs-lookup"><span data-stu-id="d1021-144">Click hello copy box toocopy one of your access keys toohello clipboard.</span></span>
   
    ![Copia della chiave di archiviazione di Azure](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a><span data-ttu-id="d1021-146">D.</span><span class="sxs-lookup"><span data-stu-id="d1021-146">D.</span></span> <span data-ttu-id="d1021-147">Copiare l'archiviazione di blob tooAzure file esempio hello</span><span class="sxs-lookup"><span data-stu-id="d1021-147">Copy hello sample file tooAzure blob storage</span></span>
<span data-ttu-id="d1021-148">toocopy dell'archiviazione blob tooAzure dei dati:</span><span class="sxs-lookup"><span data-stu-id="d1021-148">toocopy your data tooAzure blob storage:</span></span>

1. <span data-ttu-id="d1021-149">Aprire un prompt dei comandi e cambiare directory di installazione di directory toohello AzCopy.</span><span class="sxs-lookup"><span data-stu-id="d1021-149">Open a command prompt, and change directories toohello AzCopy installation directory.</span></span> <span data-ttu-id="d1021-150">Questo comando Modifica toohello directory di installazione predefinita in un client di Windows a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="d1021-150">This command changes toohello default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="d1021-151">Eseguire i seguenti file di comando tooupload hello hello.</span><span class="sxs-lookup"><span data-stu-id="d1021-151">Run hello following command tooupload hello file.</span></span> <span data-ttu-id="d1021-152">Specificare l'URL dell'endpoint di servizio BLOB per <blob service endpoint URL> e la chiave dell'account di archiviazione di Azure per <azure_storage_account_key>.</span><span class="sxs-lookup"><span data-stu-id="d1021-152">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="d1021-153">Vedere anche [introduzione hello utilità della riga di comando di AzCopy][Getting Started with hello AzCopy Command-Line Utility].</span><span class="sxs-lookup"><span data-stu-id="d1021-153">See also [Getting Started with hello AzCopy Command-Line Utility][Getting Started with hello AzCopy Command-Line Utility].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="d1021-154">E.</span><span class="sxs-lookup"><span data-stu-id="d1021-154">E.</span></span> <span data-ttu-id="d1021-155">Esplorare il contenitore di archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="d1021-155">Explore your blob storage container</span></span>
<span data-ttu-id="d1021-156">file hello toosee caricato tooblob archiviazione:</span><span class="sxs-lookup"><span data-stu-id="d1021-156">toosee hello file you uploaded tooblob storage:</span></span>

1. <span data-ttu-id="d1021-157">Tornare blade di tooyour Blob del servizio.</span><span class="sxs-lookup"><span data-stu-id="d1021-157">Go back tooyour Blob service blade.</span></span>
2. <span data-ttu-id="d1021-158">In Contenitori fare doppio clic su **datacontainer**.</span><span class="sxs-lookup"><span data-stu-id="d1021-158">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="d1021-159">dati di tooyour tooexplore hello del percorso, fare clic su cartella hello **datedimension** e verrà visualizzato il file caricato **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="d1021-159">tooexplore hello path tooyour data, click hello folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="d1021-160">Fare clic su proprietà tooview, **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="d1021-160">tooview properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="d1021-161">Si noti che nel Pannello proprietà di hello Blob, è possibile scaricare o eliminare file hello.</span><span class="sxs-lookup"><span data-stu-id="d1021-161">Note that in hello Blob properties blade, you can download or delete hello file.</span></span>
   
    ![Visualizzazione del BLOB di archiviazione di Azure](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a><span data-ttu-id="d1021-163">Passaggio 2: Creare una tabella esterna per i dati di esempio hello</span><span class="sxs-lookup"><span data-stu-id="d1021-163">Step 2: Create an external table for hello sample data</span></span>
<span data-ttu-id="d1021-164">In questa sezione viene creata una tabella esterna che definisce i dati di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="d1021-164">In this section we create an external table that defines hello sample data.</span></span>

<span data-ttu-id="d1021-165">PolyBase utilizza i dati di tabelle esterne tooaccess nell'archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1021-165">PolyBase uses external tables tooaccess data in Azure blob storage.</span></span> <span data-ttu-id="d1021-166">Poiché i dati di hello non vengono archiviati all'interno di SQL Data Warehouse, PolyBase gestisce i dati esterni toohello di autenticazione utilizzando le credenziali con ambito database.</span><span class="sxs-lookup"><span data-stu-id="d1021-166">Since hello data is not stored within SQL Data Warehouse, PolyBase handles authentication toohello external data by using a database-scoped credential.</span></span>

<span data-ttu-id="d1021-167">esempio Hello in questo passaggio utilizza questi toocreate istruzioni Transact-SQL una tabella esterna.</span><span class="sxs-lookup"><span data-stu-id="d1021-167">hello example in this step uses these Transact-SQL statements toocreate an external table.</span></span>

* <span data-ttu-id="d1021-168">[Creare la chiave Master (Transact-SQL)] [ Create Master Key (Transact-SQL)] credenziali con ambito segreto hello tooencrypt del database.</span><span class="sxs-lookup"><span data-stu-id="d1021-168">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] tooencrypt hello secret of your database scoped credential.</span></span>
* <span data-ttu-id="d1021-169">[Creare credenziali con ambito Database (Transact-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify informazioni di autenticazione per l'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1021-169">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] toospecify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="d1021-170">[Creare l'origine dati esterna (Transact-SQL)] [ Create External Data Source (Transact-SQL)] percorso hello toospecify dello spazio di archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1021-170">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] toospecify hello location of your Azure blob storage.</span></span>
* <span data-ttu-id="d1021-171">[Creare un formato di File esterni (Transact-SQL)] [ Create External File Format (Transact-SQL)] formato hello toospecify dei dati.</span><span class="sxs-lookup"><span data-stu-id="d1021-171">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] toospecify hello format of your data.</span></span>
* <span data-ttu-id="d1021-172">[Creare una tabella esterna (Transact-SQL)] [ Create External Table (Transact-SQL)] toospecify definizione della tabella hello e il percorso di hello dati.</span><span class="sxs-lookup"><span data-stu-id="d1021-172">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] toospecify hello table definition and location of hello data.</span></span>

<span data-ttu-id="d1021-173">Eseguire questa query nel database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d1021-173">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="d1021-174">Crea una tabella esterna denominata DimDate2External nello schema dbo hello che punta a dati di esempio DimDate2.txt toohello nell'archiviazione blob di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d1021-174">It will create an external table named DimDate2External in hello dbo schema that points toohello DimDate2.txt sample data in hello Azure blob storage.</span></span>

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


<span data-ttu-id="d1021-175">In Esplora oggetti di SQL Server in Visual Studio, è possibile visualizzare il formato di file esterno hello, origine dati esterna e tabella DimDate2External hello.</span><span class="sxs-lookup"><span data-stu-id="d1021-175">In SQL Server Object Explorer in Visual Studio, you can see hello external file format, external data source, and hello DimDate2External table.</span></span>

![Visualizzazione della tabella esterna](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="d1021-177">Passaggio 3: Caricare i dati in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d1021-177">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="d1021-178">Una volta creata la tabella esterna hello, è possibile caricare i dati di hello in una nuova tabella o inserirlo in una tabella esistente.</span><span class="sxs-lookup"><span data-stu-id="d1021-178">Once hello external table is created, you can either load hello data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="d1021-179">dati hello tooload in una nuova tabella, eseguire hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] istruzione.</span><span class="sxs-lookup"><span data-stu-id="d1021-179">tooload hello data into a new table, run hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="d1021-180">nuova tabella Hello avranno le colonne di hello denominate query hello.</span><span class="sxs-lookup"><span data-stu-id="d1021-180">hello new table will have hello columns named in hello query.</span></span> <span data-ttu-id="d1021-181">i tipi di dati delle colonne hello Hello corrisponderà a tipi di dati hello nella definizione della tabella esterna hello.</span><span class="sxs-lookup"><span data-stu-id="d1021-181">hello data types of hello columns will match hello data types in hello external table definition.</span></span>
* <span data-ttu-id="d1021-182">dati hello tooload in una tabella esistente, utilizzare hello [INSERT... SELECT (Transact-SQL)] [ INSERT...SELECT (Transact-SQL)] istruzione.</span><span class="sxs-lookup"><span data-stu-id="d1021-182">tooload hello data into an existing table, use hello [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

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

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="d1021-183">Passaggio 4: Creare statistiche sui dati appena caricati</span><span class="sxs-lookup"><span data-stu-id="d1021-183">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="d1021-184">SQL Data Warehouse non crea automaticamente o aggiorna automaticamente le statistiche.</span><span class="sxs-lookup"><span data-stu-id="d1021-184">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="d1021-185">Pertanto, tooachieve prestazioni elevate delle query, è importante innanzitutto caricano statistiche toocreate in ogni colonna di ogni tabella dopo hello.</span><span class="sxs-lookup"><span data-stu-id="d1021-185">Therefore, tooachieve high query performance, it's important toocreate statistics on each column of each table after hello first load.</span></span> <span data-ttu-id="d1021-186">È inoltre importante tooupdate statistiche dopo aver apportato modifiche sostanziali in dati hello.</span><span class="sxs-lookup"><span data-stu-id="d1021-186">It's also important tooupdate statistics after substantial changes in hello data.</span></span>

<span data-ttu-id="d1021-187">Questo esempio Crea statistiche a colonna singola nella tabella DimDate2 nuovo hello.</span><span class="sxs-lookup"><span data-stu-id="d1021-187">This example creates single-column statistics on hello new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="d1021-188">vedere, più toolearn [statistiche][Statistics].</span><span class="sxs-lookup"><span data-stu-id="d1021-188">toolearn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="d1021-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d1021-189">Next steps</span></span>
<span data-ttu-id="d1021-190">Vedere hello [Guida a PolyBase] [ PolyBase guide] per ulteriori informazioni che è necessario conoscere quando si sviluppa una soluzione che usa PolyBase.</span><span class="sxs-lookup"><span data-stu-id="d1021-190">See hello [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
[Getting Started with hello AzCopy Command-Line Utility]:../storage/common/storage-use-azcopy.md
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
