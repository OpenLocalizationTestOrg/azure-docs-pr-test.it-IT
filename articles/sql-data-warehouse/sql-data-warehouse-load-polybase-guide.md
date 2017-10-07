---
title: aaaGuide per l'utilizzo di PolyBase in SQL Data Warehouse | Documenti Microsoft
description: Linee guida e consigli per l'uso di PolyBase in scenari di SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="2af51-103">Guida per l'uso di PolyBase in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="2af51-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="2af51-104">Questa guida offre informazioni pratiche per l'uso di PolyBase in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2af51-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="2af51-105">tooget introduzione, vedere hello [caricano dati con PolyBase] [ Load data with PolyBase] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2af51-105">tooget started, see hello [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="2af51-106">Rotazione delle chiavi di archiviazione</span><span class="sxs-lookup"><span data-stu-id="2af51-106">Rotating storage keys</span></span>
<span data-ttu-id="2af51-107">Da ora tootime è l'archiviazione blob toochange hello accesso tooyour chiave per motivi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="2af51-107">From time tootime you will want toochange hello access key tooyour blob storage for security reasons.</span></span>

<span data-ttu-id="2af51-108">Hello più elegante tooperform modo che questa attività è toofollow un processo noto come "rotazione delle chiavi di hello".</span><span class="sxs-lookup"><span data-stu-id="2af51-108">hello most elegant way tooperform this task is toofollow a process known as "rotating hello keys".</span></span> <span data-ttu-id="2af51-109">Si sarà notato che siano due chiavi di archiviazione per l'account di archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="2af51-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="2af51-110">Si tratta in modo che è possibile eseguire la transizione</span><span class="sxs-lookup"><span data-stu-id="2af51-110">This is so that you can transition</span></span>

<span data-ttu-id="2af51-111">Ruotare le chiavi dell'account di archiviazione di Azure è un processo semplice tre passaggio</span><span class="sxs-lookup"><span data-stu-id="2af51-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="2af51-112">Creare seconda credenziali con ambito database basata sulla chiave di accesso di archiviazione secondaria hello</span><span class="sxs-lookup"><span data-stu-id="2af51-112">Create second database scoped credential based on hello secondary storage access key</span></span>
2. <span data-ttu-id="2af51-113">Creare una seconda origine dati esterna in base a questa nuova credenziale</span><span class="sxs-lookup"><span data-stu-id="2af51-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="2af51-114">Eliminare e creare tabelle esterne di hello verso toohello nuova origine dati esterna</span><span class="sxs-lookup"><span data-stu-id="2af51-114">Drop and create hello external table(s) pointing toohello new external data source</span></span>

<span data-ttu-id="2af51-115">Quando è stata eseguita la migrazione di tutte le tabelle esterne toohello nuova origine dati esterna, quindi è possibile eseguire hello eseguire la pulizia delle attività:</span><span class="sxs-lookup"><span data-stu-id="2af51-115">When you have migrated all your external tables toohello new external data source then you can perform hello clean up tasks:</span></span>

1. <span data-ttu-id="2af51-116">Eliminare prima origine dati esterna</span><span class="sxs-lookup"><span data-stu-id="2af51-116">Drop first external data source</span></span>
2. <span data-ttu-id="2af51-117">Credenziali basata sulla chiave di accesso di archiviazione primaria hello con ambito database prima di rilascio</span><span class="sxs-lookup"><span data-stu-id="2af51-117">Drop first database scoped credential based on hello primary storage access key</span></span>
3. <span data-ttu-id="2af51-118">Accedere ad Azure e rigenerare la chiave di accesso primaria hello pronto per hello successivo</span><span class="sxs-lookup"><span data-stu-id="2af51-118">Log into Azure and regenerate hello primary access key ready for hello next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="2af51-119">Eseguire query sui dati di archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="2af51-119">Query Azure blob storage data</span></span>
<span data-ttu-id="2af51-120">Le query su tabelle esterne è sufficiente utilizzano il nome di tabella hello come se fosse una tabella relazionale.</span><span class="sxs-lookup"><span data-stu-id="2af51-120">Queries against external tables simply use hello table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="2af51-121">Una query su una tabella esterna può avere esito negativo con errore hello *"Query interrotta--è stata raggiunta la soglia massima di rifiuti di hello durante la lettura da un'origine esterna"*.</span><span class="sxs-lookup"><span data-stu-id="2af51-121">A query on an external table can fail with hello error *"Query aborted-- hello maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="2af51-122">Indica che i dati esterni contengono record *sporchi* .</span><span class="sxs-lookup"><span data-stu-id="2af51-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="2af51-123">Un record di dati viene considerato come 'danneggiato' se i dati effettivi hello tipi/numero di colonne non corrispondono a definizioni di colonna hello della tabella esterna hello o se non è conforme il formato di file esterno specificato toohello dati hello.</span><span class="sxs-lookup"><span data-stu-id="2af51-123">A data record is considered 'dirty' if hello actual data types/number of columns do not match hello column definitions of hello external table or if hello data doesn't conform toohello specified external file format.</span></span> <span data-ttu-id="2af51-124">toofix, verificare che la tabella esterna e le definizioni di formato di file esterno siano corrette e che le definizioni di toothese è conforme ai dati esterni.</span><span class="sxs-lookup"><span data-stu-id="2af51-124">toofix this, ensure that your external table and external file format definitions are correct and your external data conforms toothese definitions.</span></span> <span data-ttu-id="2af51-125">Nel caso in cui un subset di record di dati esterni vengono modificati, è possibile scegliere tooreject questi record per le query utilizzando le opzioni di rifiuto hello CREATE EXTERNAL TABLE DDL.</span><span class="sxs-lookup"><span data-stu-id="2af51-125">In case a subset of external data records are dirty, you can choose tooreject these records for your queries by using hello reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="2af51-126">Caricare dati dall'archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="2af51-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="2af51-127">In questo esempio carica i dati dal database Data Warehouse tooSQL di archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="2af51-127">This example loads data from Azure blob storage tooSQL Data Warehouse database.</span></span>

<span data-ttu-id="2af51-128">L'archiviazione dei dati direttamente rimuove il tempo di trasferimento dati hello per le query.</span><span class="sxs-lookup"><span data-stu-id="2af51-128">Storing data directly removes hello data transfer time for queries.</span></span> <span data-ttu-id="2af51-129">L'archiviazione dei dati con un indice columnstore consente di migliorare le prestazioni delle query per le query di analisi da backup too10x.</span><span class="sxs-lookup"><span data-stu-id="2af51-129">Storing data with a columnstore index improves query performance for analysis queries by up too10x.</span></span>

<span data-ttu-id="2af51-130">In questo esempio utilizza i dati di tooload istruzione CREATE TABLE AS SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="2af51-130">This example uses hello CREATE TABLE AS SELECT statement tooload data.</span></span> <span data-ttu-id="2af51-131">nuova tabella Hello eredita le colonne di hello denominate query hello.</span><span class="sxs-lookup"><span data-stu-id="2af51-131">hello new table inherits hello columns named in hello query.</span></span> <span data-ttu-id="2af51-132">Eredita i tipi di dati hello di tali colonne dalla definizione della tabella esterna hello.</span><span class="sxs-lookup"><span data-stu-id="2af51-132">It inherits hello data types of those columns from hello external table definition.</span></span>

<span data-ttu-id="2af51-133">CREATE TABLE AS SELECT è un efficiente elevata istruzione Transact-SQL che carica i dati di hello in parallelo tooall hello calcolo i nodi del proprio SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2af51-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads hello data in parallel tooall hello compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="2af51-134">Questa è stata sviluppata per il motore di elaborazione parallela massiva (. MPP) hello nel sistema di piattaforma Analitica ed è ora in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2af51-134">It was originally developed for  hello massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

<span data-ttu-id="2af51-135">Vedere [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="2af51-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="2af51-136">Creare statistiche sui dati appena caricati</span><span class="sxs-lookup"><span data-stu-id="2af51-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="2af51-137">SQL Data Warehouse di Azure non supporta ancora le statistiche di creazione automatica o aggiornamento automatico.</span><span class="sxs-lookup"><span data-stu-id="2af51-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="2af51-138">Ordine tooget hello prestazioni migliori dalle query, è importante creare statistiche per tutte le colonne di tutte le tabelle dopo il primo caricamento hello o si verificano modifiche sostanziali in dati hello.</span><span class="sxs-lookup"><span data-stu-id="2af51-138">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="2af51-139">Per una spiegazione dettagliata delle statistiche, vedere hello [statistiche] [ Statistics] argomento nel gruppo di sviluppare hello degli argomenti.</span><span class="sxs-lookup"><span data-stu-id="2af51-139">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>  <span data-ttu-id="2af51-140">Di seguito è riportato un esempio di come statistiche toocreate sulla tabella hello caricati in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="2af51-140">Below is a quick example of how toocreate statistics on hello tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a><span data-ttu-id="2af51-141">Esportazione di archiviazione blob di dati tooAzure</span><span class="sxs-lookup"><span data-stu-id="2af51-141">Export data tooAzure blob storage</span></span>
<span data-ttu-id="2af51-142">Questa sezione illustra la modalità di archiviazione blob dati tooexport tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2af51-142">This section shows how tooexport data from SQL Data Warehouse tooAzure blob storage.</span></span> <span data-ttu-id="2af51-143">Questo esempio Usa CREATE EXTERNAL TABLE AS SELECT che è un elevata ad alte prestazioni di Transact-SQL istruzione tooexport hello dati in parallelo da tutti i nodi di calcolo di hello.</span><span class="sxs-lookup"><span data-stu-id="2af51-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement tooexport hello data in parallel from all hello compute nodes.</span></span>

<span data-ttu-id="2af51-144">Hello seguente viene creata una tabella esterna Weblogs2014 utilizzando le definizioni delle colonne e dati da dbo. Tabella di blog.</span><span class="sxs-lookup"><span data-stu-id="2af51-144">hello following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="2af51-145">definizione della tabella esterna Hello viene archiviato in SQL Data Warehouse e i risultati di hello dell'istruzione SELECT hello sono esportato toohello "/ / log2014/archiviare" directory nel contenitore blob hello specificato dall'origine dati hello.</span><span class="sxs-lookup"><span data-stu-id="2af51-145">hello external table definition is stored in SQL Data Warehouse and hello results of hello SELECT statement are exported toohello "/archive/log2014/" directory under hello blob container specified by hello data source.</span></span> <span data-ttu-id="2af51-146">Hello dati vengono esportati nel formato di file di testo specificato hello.</span><span class="sxs-lookup"><span data-stu-id="2af51-146">hello data is exported in hello specified text file format.</span></span>

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a><span data-ttu-id="2af51-147">Isolare il caricamento degli utenti</span><span class="sxs-lookup"><span data-stu-id="2af51-147">Isolate Loading Users</span></span>
<span data-ttu-id="2af51-148">Vi è spesso un toohave necessità più utenti che possono caricare dati in un data Warehouse SQL.</span><span class="sxs-lookup"><span data-stu-id="2af51-148">There is often a need toohave multiple users that can load data into a SQL DW.</span></span> <span data-ttu-id="2af51-149">Poiché hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] richiede autorizzazioni di controllo del database di hello, si finirà con più utenti con accesso di controllo su tutti gli schemi.</span><span class="sxs-lookup"><span data-stu-id="2af51-149">Because hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requires CONTROL permissions of hello database, you will end up with multiple users with control access over all schemas.</span></span> <span data-ttu-id="2af51-150">toolimit, è possibile utilizzare l'istruzione DENY controllo hello.</span><span class="sxs-lookup"><span data-stu-id="2af51-150">toolimit this, you can use hello DENY CONTROL statement.</span></span>

<span data-ttu-id="2af51-151">Esempio: si supponga che esistano gli schemi di database schema_A per reparto A e schema_B per reparto B e di consentire agli utenti di database utente_A e utente _B di effettuare caricamenti PolyBase rispettivamente in reparto A e B.</span><span class="sxs-lookup"><span data-stu-id="2af51-151">Example: Consider database schemas schema_A for dept A, and schema_B for dept B Let database users user_A and user_B be users for PolyBase loading in dept A and B, respectively.</span></span> <span data-ttu-id="2af51-152">A entrambi gli utenti sono state concesse le autorizzazioni di database CONTROL.</span><span class="sxs-lookup"><span data-stu-id="2af51-152">They both have been granted CONTROL database permissions.</span></span>
<span data-ttu-id="2af51-153">creatori di Hello dello schema A e B ora bloccare i relativi schemi utilizzando l'istruzione DENY:</span><span class="sxs-lookup"><span data-stu-id="2af51-153">hello creators of schema A and B now lock down their schemas using DENY:</span></span>

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 <span data-ttu-id="2af51-154">Con questa operazione, user_A ed user_B dovrebbe ora essere bloccato da hello dello schema di altro reparto.</span><span class="sxs-lookup"><span data-stu-id="2af51-154">With this, user_A and user_B should now be locked out from hello other dept’s schema.</span></span>
 


## <a name="next-steps"></a><span data-ttu-id="2af51-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2af51-155">Next steps</span></span>
<span data-ttu-id="2af51-156">toolearn ulteriori informazioni su tooSQL lo spostamento di dati Data Warehouse, vedere hello [Cenni preliminari sulla migrazione di dati][data migration overview].</span><span class="sxs-lookup"><span data-stu-id="2af51-156">toolearn more about moving data tooSQL Data Warehouse, see hello [data migration overview][data migration overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
