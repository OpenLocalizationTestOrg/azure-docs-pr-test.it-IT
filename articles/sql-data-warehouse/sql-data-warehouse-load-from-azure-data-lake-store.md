---
title: aaaLoad - archivio Azure Data Lake tooSQL Data Warehouse | Documenti Microsoft
description: Informazioni su come toouse PolyBase esterne nelle tabelle dati tooload dall'archivio Azure Data Lake in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 01/25/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 50ef23b3eba5f58bc9974095f84140dc5c11fa4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a><span data-ttu-id="2a50f-103">Caricare dati da Azure Data Lake Store a SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="2a50f-103">Load data from Azure Data Lake Store into SQL Data Warehouse</span></span>
<span data-ttu-id="2a50f-104">Questo documento offre tutte le operazioni necessarie tooload i propri dati da Azure Data Lake archivio (ADLS) in SQL Data Warehouse con PolyBase.</span><span class="sxs-lookup"><span data-stu-id="2a50f-104">This document gives you all steps you  need tooload your own data from Azure Data Lake Store (ADLS) into SQL Data Warehouse using PolyBase.</span></span>
<span data-ttu-id="2a50f-105">Mentre si è query ad hoc in grado di toorun sui dati hello archiviati in ADLS utilizzando le tabelle esterne hello, come procedura consigliata è consigliabile importare dati hello in hello SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2a50f-105">While you are able toorun adhoc queries over hello data stored in ADLS using hello External Tables, as a best practice we suggest importing hello data into hello SQL Data Warehouse.</span></span>
<span data-ttu-id="2a50f-106">Tempo stimato: 10 minuti, se che si dispone di prerequisiti hello necessario toocomplete.</span><span class="sxs-lookup"><span data-stu-id="2a50f-106">Time Estimate: 10 minutes assuming you have hello prerequisites need toocomplete.</span></span>
<span data-ttu-id="2a50f-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="2a50f-107">In this tutorial you will learn how to:</span></span>

1. <span data-ttu-id="2a50f-108">Creare tooload gli oggetti di Database esterno dall'archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2a50f-108">Create External Database objects tooload from Azure Data Lake Store.</span></span>
2. <span data-ttu-id="2a50f-109">Connettersi tooan Directory dell'archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="2a50f-109">Connect tooan Azure Data Lake Store Directory.</span></span>
3. <span data-ttu-id="2a50f-110">Caricare i dati in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2a50f-110">Load data into Azure SQL Data Warehouse.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2a50f-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="2a50f-111">Before you begin</span></span>
<span data-ttu-id="2a50f-112">toorun questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="2a50f-112">toorun this tutorial, you need:</span></span>

* <span data-ttu-id="2a50f-113">Azure toouse di applicazione di Active Directory per l'autenticazione al servizio.</span><span class="sxs-lookup"><span data-stu-id="2a50f-113">Azure Active Directory Application toouse for Service-to-Service authentication.</span></span> <span data-ttu-id="2a50f-114">toocreate, seguire [l'autenticazione di Active directory](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span><span class="sxs-lookup"><span data-stu-id="2a50f-114">toocreate, follow [Active directory authentication](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span></span>

>[!NOTE] 
> <span data-ttu-id="2a50f-115">È necessario l'ID client hello, chiave e valore Endpoint Token OAuth 2.0 di tooyour di tooconnect l'applicazione di Active Directory Azure Data Lake SQL Data warehouse.</span><span class="sxs-lookup"><span data-stu-id="2a50f-115">You need hello client ID, Key, and OAuth2.0 Token Endpoint Value of your Active Directory Application tooconnect tooyour Azure Data Lake from SQL Data Warehouse.</span></span> <span data-ttu-id="2a50f-116">Dettagli per la modalità tooget questi valori sono nel collegamento hello precedente.</span><span class="sxs-lookup"><span data-stu-id="2a50f-116">Details for how tooget these values are in hello link above.</span></span>
><span data-ttu-id="2a50f-117">Nota per la registrazione di App di Azure Active Directory utilizzare "ID applicazione" hello come hello ID Client.</span><span class="sxs-lookup"><span data-stu-id="2a50f-117">Note for Azure Active Directory App Registration use hello 'Application ID' as hello Client ID.</span></span>

* <span data-ttu-id="2a50f-118">SQL Server Management Studio o SQL Server Data Tools, toodownload SQL Server Management Studio e connettersi vedere [Query SQL Server Management Studio](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span><span class="sxs-lookup"><span data-stu-id="2a50f-118">SQL Server Management Studio or SQL Server Data Tools, toodownload SSMS and connect see [Query SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span></span>

* <span data-ttu-id="2a50f-119">Un Data Warehouse SQL Azure, toocreate uno seguire: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span><span class="sxs-lookup"><span data-stu-id="2a50f-119">An Azure SQL Data Warehouse, toocreate one follow: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span></span>

* <span data-ttu-id="2a50f-120">Un'istanza di Azure Data Lake Store, con o senza crittografia abilitata.</span><span class="sxs-lookup"><span data-stu-id="2a50f-120">An Azure Data Lake Store, with or without encryption enabled.</span></span> <span data-ttu-id="2a50f-121">una seguire toocreate: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="2a50f-121">toocreate one follow: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span></span>




## <a name="configure-hello-data-source"></a><span data-ttu-id="2a50f-122">Configurare l'origine dati hello</span><span class="sxs-lookup"><span data-stu-id="2a50f-122">Configure hello data source</span></span>
<span data-ttu-id="2a50f-123">PolyBase Usa percorso hello toodefine oggetti esterni di T-SQL e degli attributi di dati esterni hello.</span><span class="sxs-lookup"><span data-stu-id="2a50f-123">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="2a50f-124">gli oggetti esterni Hello vengono archiviati in SQL Data Warehouse e hello dati di riferimento che th vengono archiviati esternamente.</span><span class="sxs-lookup"><span data-stu-id="2a50f-124">hello external objects are stored in SQL Data Warehouse and reference hello data th is stored externally.</span></span>


###  <a name="create-a-credential"></a><span data-ttu-id="2a50f-125">Creare una credenziale</span><span class="sxs-lookup"><span data-stu-id="2a50f-125">Create a credential</span></span>
<span data-ttu-id="2a50f-126">Archiviare la Data Lake di Azure tooaccess, sarà necessario toocreate tooencrypt una chiave Master del Database il segreto di credenziale utilizzato nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="2a50f-126">tooaccess your Azure Data Lake Store, you will need toocreate a Database Master Key tooencrypt your credential secret used in hello next step.</span></span>
<span data-ttu-id="2a50f-127">È quindi possibile creare una credenziale con ambito Database, che memorizza credenziali dell'entità servizio hello configurate in AAD.</span><span class="sxs-lookup"><span data-stu-id="2a50f-127">You then create a Database scoped credential, which stores hello service principal credentials set up in AAD.</span></span> <span data-ttu-id="2a50f-128">Per gli utenti che hanno utilizzato PolyBase tooconnect tooWindows BLOB di archiviazione di Azure, si noti che le credenziali hello sintassi è diversa.</span><span class="sxs-lookup"><span data-stu-id="2a50f-128">For those of you who have used PolyBase tooconnect tooWindows Azure Storage Blobs, note that hello credential syntax is different.</span></span>
<span data-ttu-id="2a50f-129">tooconnect tooAzure archivio Data Lake, è necessario **prima** creare un'applicazione di Azure Active Directory, creare una chiave di accesso e concedere una risorsa di Azure Data Lake toohello accesso dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2a50f-129">tooconnect tooAzure Data Lake Store, you must **first** create an Azure Active Directory Application, create an access key, and grant hello application access toohello Azure Data Lake resource.</span></span> <span data-ttu-id="2a50f-130">Instrucitons tooperform questi passaggi si trovano [qui](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span><span class="sxs-lookup"><span data-stu-id="2a50f-130">Instrucitons tooperform these steps are located [here](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span></span>

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass hello client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
-- SECRET: Provide your AAD Application Service Principal key.
-- For more information on Create Database Scoped Credential: https://msdn.microsoft.com/en-us/library/mt270260.aspx

CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '<client_id>@<OAuth_2.0_Token_EndPoint>',
    SECRET = '<key>'
;

-- It should look something like this:
CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token',
    SECRET = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI='
;
```


### <a name="create-hello-external-data-source"></a><span data-ttu-id="2a50f-131">Creare l'origine dati esterna hello</span><span class="sxs-lookup"><span data-stu-id="2a50f-131">Create hello external data source</span></span>
<span data-ttu-id="2a50f-132">Utilizzare questo [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] comando percorso hello toostore di dati hello e hello tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="2a50f-132">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span>
<span data-ttu-id="2a50f-133">È possibile trovare hello ADL URI nel portale di Azure hello e www.portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="2a50f-133">You can find hello ADL URI in hello Azure portal and www.portal.azure.com.</span></span>

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a><span data-ttu-id="2a50f-134">Configurare il formato dei dati</span><span class="sxs-lookup"><span data-stu-id="2a50f-134">Configure data format</span></span>
<span data-ttu-id="2a50f-135">dati di hello tooimport di ADLS, è necessario toospecify formato di file esterno hello.</span><span class="sxs-lookup"><span data-stu-id="2a50f-135">tooimport hello data from ADLS, you need toospecify hello external file format.</span></span> <span data-ttu-id="2a50f-136">Questo comando è toodescribe opzioni relative al formato dei dati.</span><span class="sxs-lookup"><span data-stu-id="2a50f-136">This command has format-specific options toodescribe your data.</span></span>
<span data-ttu-id="2a50f-137">Di seguito è riportato un esempio di formato file comunemente usato, ovvero un file di testo delimitato da barre verticali.</span><span class="sxs-lookup"><span data-stu-id="2a50f-137">Below is an example of a commonly used file format that is a pipe-delimited text file.</span></span>
<span data-ttu-id="2a50f-138">Esaminare la documentazione di T-SQL per un elenco completo di [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span><span class="sxs-lookup"><span data-stu-id="2a50f-138">Look at our T-SQL documentation for a complete list of [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span></span>

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks hello end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies hello field terminator for data of type string in hello text-delimited file.
-- DATE_FORMAT: Specifies a custom format for all date and time data that might appear in a delimited text file.
-- Use_Type_Default: Store all Missing values as NULL

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

## <a name="create-hello-external-tables"></a><span data-ttu-id="2a50f-139">Creare tabelle esterne di hello</span><span class="sxs-lookup"><span data-stu-id="2a50f-139">Create hello external tables</span></span>
<span data-ttu-id="2a50f-140">Ora che è stata specificata l'origine e file di formato di dati di hello, si è pronti toocreate tabelle esterne di hello.</span><span class="sxs-lookup"><span data-stu-id="2a50f-140">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> <span data-ttu-id="2a50f-141">Le tabelle esterne rappresentano la modalità di interazione con i dati esterni.</span><span class="sxs-lookup"><span data-stu-id="2a50f-141">External tables are how you interact with external data.</span></span> <span data-ttu-id="2a50f-142">PolyBase, viene utilizzato per tutti i file in tutte le sottodirectory della directory hello specificata nel parametro di percorso hello ricorsiva directory attraversamento tooread.</span><span class="sxs-lookup"><span data-stu-id="2a50f-142">PolyBase uses recursive directory traversal tooread all files in all subdirectories of hello directory specified in hello location parameter.</span></span> <span data-ttu-id="2a50f-143">Inoltre, hello di esempio seguente viene illustrato come toocreate hello oggetto.</span><span class="sxs-lookup"><span data-stu-id="2a50f-143">Also, hello following example shows how toocreate hello object.</span></span> <span data-ttu-id="2a50f-144">È necessario toocustomize hello istruzione toowork dati hello che dispongono di ADLS.</span><span class="sxs-lookup"><span data-stu-id="2a50f-144">You need toocustomize hello statement toowork with hello data you have in ADLS.</span></span>

```sql
-- D: Create an External Table
-- LOCATION: Folder under hello ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object toouse.
-- FILE_FORMAT: Specifies which File Format Object toouse
-- REJECT_TYPE: Specifies how you want toodeal with rejected rows. Either Value or percentage of hello total
-- REJECT_VALUE: Sets hello Reject value based on hello reject type.

-- DimProduct
CREATE EXTERNAL TABLE [dbo].[DimProduct_external] (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL
)
WITH
(
    LOCATION='/DimProduct/'
,   DATA_SOURCE = AzureDataLakeStore
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

```

## <a name="external-table-considerations"></a><span data-ttu-id="2a50f-145">Considerazioni sulle tabelle esterne</span><span class="sxs-lookup"><span data-stu-id="2a50f-145">External Table Considerations</span></span>
<span data-ttu-id="2a50f-146">Creazione di una tabella esterna è semplice, ma sono presenti alcuni aspetti correlati necessari toobe descritto.</span><span class="sxs-lookup"><span data-stu-id="2a50f-146">Creating an external table is easy, but there are some nuances that need toobe discussed.</span></span>

<span data-ttu-id="2a50f-147">Il caricamento dei dati con PolyBase è fortemente tipizzato.</span><span class="sxs-lookup"><span data-stu-id="2a50f-147">Loading data with PolyBase is strongly typed.</span></span> <span data-ttu-id="2a50f-148">Ciò significa che ogni riga di dati hello il caricamento deve soddisfare definizione dello schema di tabella hello.</span><span class="sxs-lookup"><span data-stu-id="2a50f-148">This means that each row of hello data being ingested must satisfy hello table schema definition.</span></span>
<span data-ttu-id="2a50f-149">Se una determinata riga non corrisponde alla definizione dello schema hello, riga hello viene rifiutata dal carico hello.</span><span class="sxs-lookup"><span data-stu-id="2a50f-149">If a given row does not match hello schema definition, hello row is rejected from hello load.</span></span>

<span data-ttu-id="2a50f-150">Hello REJECT_TYPE e REJECT_VALUE opzioni consentono di toodefine il numero di righe o la percentuale di dati hello deve essere presente nella tabella finale hello.</span><span class="sxs-lookup"><span data-stu-id="2a50f-150">hello REJECT_TYPE and REJECT_VALUE options allow you toodefine how many rows or what percentage of hello data must be present in hello final table.</span></span>
<span data-ttu-id="2a50f-151">Durante il caricamento, se viene raggiunto il valore di rifiuto di hello, hello caricamento non riesce.</span><span class="sxs-lookup"><span data-stu-id="2a50f-151">During load, if hello reject value is reached, hello load fails.</span></span> <span data-ttu-id="2a50f-152">causa più comune di Hello di righe rifiutate è una mancata corrispondenza della definizione dello schema.</span><span class="sxs-lookup"><span data-stu-id="2a50f-152">hello most common cause of rejected rows is a schema definition mismatch.</span></span>
<span data-ttu-id="2a50f-153">Ad esempio, se una colonna in modo non corretto di schema hello di int quando i dati di hello nel file hello sono una stringa, ogni riga avrà esito negativo tooload.</span><span class="sxs-lookup"><span data-stu-id="2a50f-153">For example, if a column is incorrectly given hello schema of int when hello data in hello file is a string, every row will fail tooload.</span></span>

<span data-ttu-id="2a50f-154">Hello percorso Specifica directory hello in primo piano da dati tooread da.</span><span class="sxs-lookup"><span data-stu-id="2a50f-154">hello Location specifies hello topmost directory that you want tooread data from.</span></span>
<span data-ttu-id="2a50f-155">In questo caso, se si sono verificati sottodirectory /DimProduct/ PolyBase importazione tutti i dati all'interno di sottodirectory di hello hello.</span><span class="sxs-lookup"><span data-stu-id="2a50f-155">In this case, if there were subdirectories under /DimProduct/ PolyBase would import all hello data within hello subdirectories.</span></span>

## <a name="load-hello-data"></a><span data-ttu-id="2a50f-156">Caricare i dati di hello</span><span class="sxs-lookup"><span data-stu-id="2a50f-156">Load hello data</span></span>
<span data-ttu-id="2a50f-157">dati tooload dall'archivio Azure Data Lake utilizzano hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] istruzione.</span><span class="sxs-lookup"><span data-stu-id="2a50f-157">tooload data from Azure Data Lake Store use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="2a50f-158">Caricamento con un'istruzione CTAS utilizza hello fortemente tipizzati tabella esterna che è stata creata.</span><span class="sxs-lookup"><span data-stu-id="2a50f-158">Loading with CTAS uses hello strongly typed external table you have created.</span></span>

<span data-ttu-id="2a50f-159">Un'istruzione CTAS crea una nuova tabella e popolarla con i risultati di hello di un'istruzione select.</span><span class="sxs-lookup"><span data-stu-id="2a50f-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="2a50f-160">Un'istruzione CTAS definisce hello nuova tabella toohave hello stessi colonne e tipi di dati come risultato di hello hello istruzione select.</span><span class="sxs-lookup"><span data-stu-id="2a50f-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="2a50f-161">Se si selezionano tutte le colonne di hello da una tabella esterna, nuova tabella hello è una replica di colonne di hello e tipi di dati nella tabella esterna hello.</span><span class="sxs-lookup"><span data-stu-id="2a50f-161">If you select all hello columns from an external table, hello new table is a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="2a50f-162">In questo esempio viene creata una tabella con distribuzione hash chiamata DimProduct dalla tabella esterna DimProduct_external.</span><span class="sxs-lookup"><span data-stu-id="2a50f-162">In this example, we are creating a hash distributed table called DimProduct from our External Table DimProduct_external.</span></span>

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a><span data-ttu-id="2a50f-163">Ottimizzare la compressione columnstore</span><span class="sxs-lookup"><span data-stu-id="2a50f-163">Optimize columnstore compression</span></span>
<span data-ttu-id="2a50f-164">Per impostazione predefinita, SQL Data Warehouse vengono archiviati nella tabella hello come un indice columnstore cluster.</span><span class="sxs-lookup"><span data-stu-id="2a50f-164">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="2a50f-165">Al termine di un carico, alcune righe di dati hello potrebbe non compresso nel columnstore hello.</span><span class="sxs-lookup"><span data-stu-id="2a50f-165">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="2a50f-166">Esiste una serie di motivi per cui questo può verificarsi.</span><span class="sxs-lookup"><span data-stu-id="2a50f-166">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="2a50f-167">vedere, più toolearn [gestire gli indici columnstore][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="2a50f-167">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="2a50f-168">le prestazioni delle query toooptimize e la compressione columnstore dopo un caricamento, ricompilare tutte le righe di hello hello tabella tooforce hello columnstore indice toocompress.</span><span class="sxs-lookup"><span data-stu-id="2a50f-168">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span>

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

<span data-ttu-id="2a50f-169">Per ulteriori informazioni sulla gestione degli indici columnstore, vedere hello [gestire gli indici columnstore] [ manage columnstore indexes] articolo.</span><span class="sxs-lookup"><span data-stu-id="2a50f-169">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="optimize-statistics"></a><span data-ttu-id="2a50f-170">Ottimizzare le statistiche</span><span class="sxs-lookup"><span data-stu-id="2a50f-170">Optimize statistics</span></span>
<span data-ttu-id="2a50f-171">Le statistiche di colonna singola toocreate è immediatamente dopo un carico.</span><span class="sxs-lookup"><span data-stu-id="2a50f-171">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="2a50f-172">Sono disponibili alcune opzioni per le statistiche.</span><span class="sxs-lookup"><span data-stu-id="2a50f-172">There are some choices for statistics.</span></span> <span data-ttu-id="2a50f-173">Ad esempio, se si creano statistiche a colonna singola su tutte le colonne potrebbe richiedere un tempo toorebuild tutte le statistiche di hello.</span><span class="sxs-lookup"><span data-stu-id="2a50f-173">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="2a50f-174">Se si è certi di che alcune colonne non stanno toobe nei predicati di query, è possibile ignorare la creazione di statistiche di tali colonne.</span><span class="sxs-lookup"><span data-stu-id="2a50f-174">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="2a50f-175">Se si decide di statistiche di colonna singola toocreate ogni colonna di ogni tabella, è possibile utilizzare l'esempio di codice hello stored procedure `prc_sqldw_create_stats` in hello [statistiche] [ statistics] articolo.</span><span class="sxs-lookup"><span data-stu-id="2a50f-175">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="2a50f-176">Hello di esempio seguente è un buon punto di partenza per la creazione di statistiche.</span><span class="sxs-lookup"><span data-stu-id="2a50f-176">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="2a50f-177">Crea statistiche a colonna singola su ogni colonna nella tabella delle dimensioni hello e su ogni colonna di join nelle tabelle dei fatti hello.</span><span class="sxs-lookup"><span data-stu-id="2a50f-177">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="2a50f-178">È sempre possibile aggiungere colonne della tabella dei fatti tooother le statistiche di uno o più colonne in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="2a50f-178">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>


## <a name="achievement-unlocked"></a><span data-ttu-id="2a50f-179">Obiettivo raggiunto</span><span class="sxs-lookup"><span data-stu-id="2a50f-179">Achievement unlocked!</span></span>
<span data-ttu-id="2a50f-180">I dati sono stati caricati correttamente in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2a50f-180">You have successfully loaded data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="2a50f-181">Ottimo lavoro.</span><span class="sxs-lookup"><span data-stu-id="2a50f-181">Great job!</span></span>

##<a name="next-steps"></a><span data-ttu-id="2a50f-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2a50f-182">Next Steps</span></span>
<span data-ttu-id="2a50f-183">Il caricamento dei dati è hello primo passaggio toodeveloping una soluzione di data warehouse con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2a50f-183">Loading data is hello first step toodeveloping a data warehouse solution using SQL Data Warehouse.</span></span> <span data-ttu-id="2a50f-184">Vedere le risorse di sviluppo in [Tabelle](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) e [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span><span class="sxs-lookup"><span data-stu-id="2a50f-184">Check out our development resources on [Tables](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) and [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span></span>


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
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
