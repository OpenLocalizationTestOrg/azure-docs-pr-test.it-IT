---
title: Guida per l'uso di PolyBase in SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: 6938b92d8e5b46d908dc5b2155bdfdc89bb1dc8c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="4b288-103">Guida per l'uso di PolyBase in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="4b288-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="4b288-104">Questa guida offre informazioni pratiche per l'uso di PolyBase in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4b288-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="4b288-105">Per iniziare, seguire l'esercitazione [Caricamento dei dati con PolyBase][Load data with PolyBase].</span><span class="sxs-lookup"><span data-stu-id="4b288-105">To get started, see the [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="4b288-106">Rotazione delle chiavi di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4b288-106">Rotating storage keys</span></span>
<span data-ttu-id="4b288-107">A volte si desidererà modificare la chiave di accesso per l'archiviazione blob per motivi di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="4b288-107">From time to time you will want to change the access key to your blob storage for security reasons.</span></span>

<span data-ttu-id="4b288-108">Il modo più elegante per eseguire questa operazione consiste nel seguire un processo noto come "ruotare le chiavi".</span><span class="sxs-lookup"><span data-stu-id="4b288-108">The most elegant way to perform this task is to follow a process known as "rotating the keys".</span></span> <span data-ttu-id="4b288-109">Si sarà notato che siano due chiavi di archiviazione per l'account di archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="4b288-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="4b288-110">Si tratta in modo che è possibile eseguire la transizione</span><span class="sxs-lookup"><span data-stu-id="4b288-110">This is so that you can transition</span></span>

<span data-ttu-id="4b288-111">Ruotare le chiavi dell'account di archiviazione di Azure è un processo semplice tre passaggio</span><span class="sxs-lookup"><span data-stu-id="4b288-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="4b288-112">Creare seconda credenziale con ambito database in base alla chiave di accesso di archiviazione secondario</span><span class="sxs-lookup"><span data-stu-id="4b288-112">Create second database scoped credential based on the secondary storage access key</span></span>
2. <span data-ttu-id="4b288-113">Creare una seconda origine dati esterna in base a questa nuova credenziale</span><span class="sxs-lookup"><span data-stu-id="4b288-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="4b288-114">Eliminare e creare le tabelle esterne che puntano alla nuova origine dati esterna</span><span class="sxs-lookup"><span data-stu-id="4b288-114">Drop and create the external table(s) pointing to the new external data source</span></span>

<span data-ttu-id="4b288-115">Dopo aver migrato esterno tutte le tabelle per la nuova origine dati esterna, quindi è possibile eseguire attività di pulizia:</span><span class="sxs-lookup"><span data-stu-id="4b288-115">When you have migrated all your external tables to the new external data source then you can perform the clean up tasks:</span></span>

1. <span data-ttu-id="4b288-116">Eliminare prima origine dati esterna</span><span class="sxs-lookup"><span data-stu-id="4b288-116">Drop first external data source</span></span>
2. <span data-ttu-id="4b288-117">Credenziali in base alla chiave di accesso di archiviazione primaria con ambito database primo di rilascio</span><span class="sxs-lookup"><span data-stu-id="4b288-117">Drop first database scoped credential based on the primary storage access key</span></span>
3. <span data-ttu-id="4b288-118">Accedere a Azure e rigenerare la chiave di accesso primaria pronta per la volta successiva</span><span class="sxs-lookup"><span data-stu-id="4b288-118">Log into Azure and regenerate the primary access key ready for the next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="4b288-119">Eseguire query sui dati di archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="4b288-119">Query Azure blob storage data</span></span>
<span data-ttu-id="4b288-120">Le query su tabelle esterne usano semplicemente il nome della tabella come se fosse una tabella relazionale.</span><span class="sxs-lookup"><span data-stu-id="4b288-120">Queries against external tables simply use the table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="4b288-121">Una query su una tabella esterna può avere esito negativo con l'errore *"Query interrotta: è stata raggiunta la soglia massima durante la lettura da un'origine esterna"*.</span><span class="sxs-lookup"><span data-stu-id="4b288-121">A query on an external table can fail with the error *"Query aborted-- the maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="4b288-122">Indica che i dati esterni contengono record *sporchi* .</span><span class="sxs-lookup"><span data-stu-id="4b288-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="4b288-123">Un record di dati viene considerato "sporco" se i tipi/numero dei dati effettivi delle colonne non corrispondono a definizioni di colonna della tabella esterna o se i dati non sono conformi al formato di file esterno specificato.</span><span class="sxs-lookup"><span data-stu-id="4b288-123">A data record is considered 'dirty' if the actual data types/number of columns do not match the column definitions of the external table or if the data doesn't conform to the specified external file format.</span></span> <span data-ttu-id="4b288-124">Per risolvere questo problema, assicurarsi che la tabella esterna e le definizioni del formato del file esterno siano corrette e i dati esterni siano conformi a queste definizioni.</span><span class="sxs-lookup"><span data-stu-id="4b288-124">To fix this, ensure that your external table and external file format definitions are correct and your external data conforms to these definitions.</span></span> <span data-ttu-id="4b288-125">Nel caso in cui un subset di record di dati esterni sia sporco, è possibile scegliere di rifiutare tali record per le query utilizzando le opzioni di rifiuto in CREATE EXTERNAL TABLE DDL.</span><span class="sxs-lookup"><span data-stu-id="4b288-125">In case a subset of external data records are dirty, you can choose to reject these records for your queries by using the reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="4b288-126">Caricare dati dall'archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="4b288-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="4b288-127">Questo esempio carica i dati dall'archiviazione BLOB di Azure nel database di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4b288-127">This example loads data from Azure blob storage to SQL Data Warehouse database.</span></span>

<span data-ttu-id="4b288-128">Archiviando i dati direttamente viene eliminato il tempo di trasferimento dei dati per le query.</span><span class="sxs-lookup"><span data-stu-id="4b288-128">Storing data directly removes the data transfer time for queries.</span></span> <span data-ttu-id="4b288-129">L'archiviazione dei dati con un indice columnstore migliora le prestazioni delle query di analisi fino a 10 volte.</span><span class="sxs-lookup"><span data-stu-id="4b288-129">Storing data with a columnstore index improves query performance for analysis queries by up to 10x.</span></span>

<span data-ttu-id="4b288-130">Questo esempio usa l'istruzione CREATE TABLE AS SELECT per caricare i dati.</span><span class="sxs-lookup"><span data-stu-id="4b288-130">This example uses the CREATE TABLE AS SELECT statement to load data.</span></span> <span data-ttu-id="4b288-131">La nuova tabella eredita le colonne indicate nella query.</span><span class="sxs-lookup"><span data-stu-id="4b288-131">The new table inherits the columns named in the query.</span></span> <span data-ttu-id="4b288-132">Eredita i tipi di dati di tali colonne dalla definizione della tabella esterna.</span><span class="sxs-lookup"><span data-stu-id="4b288-132">It inherits the data types of those columns from the external table definition.</span></span>

<span data-ttu-id="4b288-133">CREATE TABLE AS SELECT è un’istruzione con elevate prestazioni di Transact-SQL che carica i dati in parallelo per tutti i nodi di calcolo di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4b288-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads the data in parallel to all the compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="4b288-134">È stata sviluppata in origine per il motore di elaborazione a elevato parallelismo (MPP) nel sistema di piattaforma di analisi ed è ora inclusa in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="4b288-134">It was originally developed for  the massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage to SQL Data Warehouse

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

<span data-ttu-id="4b288-135">Vedere [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="4b288-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="4b288-136">Creare statistiche sui dati appena caricati</span><span class="sxs-lookup"><span data-stu-id="4b288-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="4b288-137">SQL Data Warehouse di Azure non supporta ancora le statistiche di creazione automatica o aggiornamento automatico.</span><span class="sxs-lookup"><span data-stu-id="4b288-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="4b288-138">Per ottenere le migliori prestazioni dalle query, è importante creare statistiche per tutte le colonne di tutte le tabelle dopo il primo caricamento o dopo eventuali modifiche sostanziali dei dati.</span><span class="sxs-lookup"><span data-stu-id="4b288-138">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="4b288-139">Per una spiegazione dettagliata delle statistiche, vedere l'argomento [Statistiche][Statistics] nel gruppo di argomenti sullo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="4b288-139">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>  <span data-ttu-id="4b288-140">Di seguito è possibile vedere un rapido esempio di come creare statistiche nella tabella caricata in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="4b288-140">Below is a quick example of how to create statistics on the tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-to-azure-blob-storage"></a><span data-ttu-id="4b288-141">Esportare i dati in archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="4b288-141">Export data to Azure blob storage</span></span>
<span data-ttu-id="4b288-142">Questa sezione illustra come esportare i dati da SQL Data Warehouse nella risorsa di archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="4b288-142">This section shows how to export data from SQL Data Warehouse to Azure blob storage.</span></span> <span data-ttu-id="4b288-143">In questo esempio si utilizza CREATE EXTERNAL TABLE AS SELECT che è un’istruzione con elevate prestazioni di Transact-SQL per esportare i dati in parallelo da tutti i nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="4b288-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement to export the data in parallel from all the compute nodes.</span></span>

<span data-ttu-id="4b288-144">Nell'esempio seguente si crea una tabella esterna Weblogs2014 utilizzando le definizioni delle colonne e dati dalla tabella dbo.Weblogs.</span><span class="sxs-lookup"><span data-stu-id="4b288-144">The following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="4b288-145">La definizione della tabella esterna viene archiviata in SQL Data Warehouse e i risultati dell’istruzione SELECT sono esportati nella directory "/ archiviazione/log2014 /" nel contenitore BLOB specificato dall'origine dati.</span><span class="sxs-lookup"><span data-stu-id="4b288-145">The external table definition is stored in SQL Data Warehouse and the results of the SELECT statement are exported to the "/archive/log2014/" directory under the blob container specified by the data source.</span></span> <span data-ttu-id="4b288-146">I dati vengono esportati nel formato di file di testo specificato.</span><span class="sxs-lookup"><span data-stu-id="4b288-146">The data is exported in the specified text file format.</span></span>

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
## <a name="isolate-loading-users"></a><span data-ttu-id="4b288-147">Isolare il caricamento degli utenti</span><span class="sxs-lookup"><span data-stu-id="4b288-147">Isolate Loading Users</span></span>
<span data-ttu-id="4b288-148">È spesso necessario fare in modo che più utenti possano caricare dati in un data warehouse SQL.</span><span class="sxs-lookup"><span data-stu-id="4b288-148">There is often a need to have multiple users that can load data into a SQL DW.</span></span> <span data-ttu-id="4b288-149">Dato che [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] richiede autorizzazioni CONTROL per il database, il risultato sarà la presenza di più utenti con accesso di controllo su tutti gli schemi.</span><span class="sxs-lookup"><span data-stu-id="4b288-149">Because the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requires CONTROL permissions of the database, you will end up with multiple users with control access over all schemas.</span></span> <span data-ttu-id="4b288-150">Per limitare questa situazione, è possibile usare l'istruzione DENY CONTROL.</span><span class="sxs-lookup"><span data-stu-id="4b288-150">To limit this, you can use the DENY CONTROL statement.</span></span>

<span data-ttu-id="4b288-151">Esempio: si supponga che esistano gli schemi di database schema_A per reparto A e schema_B per reparto B e di consentire agli utenti di database utente_A e utente _B di effettuare caricamenti PolyBase rispettivamente in reparto A e B.</span><span class="sxs-lookup"><span data-stu-id="4b288-151">Example: Consider database schemas schema_A for dept A, and schema_B for dept B Let database users user_A and user_B be users for PolyBase loading in dept A and B, respectively.</span></span> <span data-ttu-id="4b288-152">A entrambi gli utenti sono state concesse le autorizzazioni di database CONTROL.</span><span class="sxs-lookup"><span data-stu-id="4b288-152">They both have been granted CONTROL database permissions.</span></span>
<span data-ttu-id="4b288-153">Gli autori di schema A e B usano a questo punto DENY per bloccare i rispettivi schemi:</span><span class="sxs-lookup"><span data-stu-id="4b288-153">The creators of schema A and B now lock down their schemas using DENY:</span></span>

```sql
   DENY CONTROL ON SCHEMA :: schema_A TO user_B;
   DENY CONTROL ON SCHEMA :: schema_B TO user_A;
```   
 <span data-ttu-id="4b288-154">In questo modo, utente_A e utente_B dovrebbero ora essere esclusi dall'accesso allo schema del reparto dell'altro utente.</span><span class="sxs-lookup"><span data-stu-id="4b288-154">With this, user_A and user_B should now be locked out from the other dept’s schema.</span></span>
 


## <a name="next-steps"></a><span data-ttu-id="4b288-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4b288-155">Next steps</span></span>
<span data-ttu-id="4b288-156">Per ulteriori informazioni sullo spostamento di dati in SQL Data Warehouse, vedere [Panoramica sulla migrazione di dati][data migration overview].</span><span class="sxs-lookup"><span data-stu-id="4b288-156">To learn more about moving data to SQL Data Warehouse, see the [data migration overview][data migration overview].</span></span>

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
