---
title: Gestire i dati cronologici nelle tabelle temporali con criteri di conservazione | Microsoft Docs
description: Informazioni su come usare criteri di conservazione temporale per tenere sotto controllo i dati cronologici.
services: sql-database
documentationcenter: 
author: bonova
manager: drasumic
editor: 
ms.assetid: 76cfa06a-e758-453e-942c-9f1ed6a38c2a
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 10/12/2016
ms.author: bonova
ms.openlocfilehash: 8975d7a7d39114b2758d64a4df9f992cba6bf561
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a><span data-ttu-id="27483-103">Gestire i dati cronologici nelle tabelle temporali con criteri di conservazione</span><span class="sxs-lookup"><span data-stu-id="27483-103">Manage historical data in Temporal Tables with retention policy</span></span>
<span data-ttu-id="27483-104">Le tabelle temporali possono aumentare le dimensioni del database più delle tabelle normali, in particolare se si conservano i dati cronologici per un periodo di tempo più lungo.</span><span class="sxs-lookup"><span data-stu-id="27483-104">Temporal Tables may increase database size more than regular tables, especially if you retain historical data for a longer period of time.</span></span> <span data-ttu-id="27483-105">Di conseguenza, i criteri di conservazione per i dati cronologici sono un aspetto importante della pianificazione e della gestione del ciclo di vita di ogni tabella temporale.</span><span class="sxs-lookup"><span data-stu-id="27483-105">Hence, retention policy for historical data is an important aspect of planning and managing the lifecycle of every temporal table.</span></span> <span data-ttu-id="27483-106">Le tabelle temporali nel database SQL Azure sono dotate di un meccanismo di conservazione di facile uso che aiuta a eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="27483-106">Temporal Tables in Azure SQL Database come with easy-to-use retention mechanism that helps you accomplish this task.</span></span>

<span data-ttu-id="27483-107">Il periodo di conservazione della cronologia temporale può essere configurato a livello di singola tabella, per consentire agli utenti di creare criteri di giacenza flessibili.</span><span class="sxs-lookup"><span data-stu-id="27483-107">Temporal history retention can be configured at the individual table level, which allows users to create flexible aging polices.</span></span> <span data-ttu-id="27483-108">L'applicazione della conservazione temporale è semplice: è necessario configurare un solo parametro durante la creazione della tabella o la modifica dello schema.</span><span class="sxs-lookup"><span data-stu-id="27483-108">Applying temporal retention is simple: it requires only one parameter to be set during table creation or schema change.</span></span>

<span data-ttu-id="27483-109">Dopo aver definito i criteri di conservazione, il database SQL di Azure avvia una verifica periodica per controllare se sono presenti righe di cronologia idonee alla pulizia automatica dei dati.</span><span class="sxs-lookup"><span data-stu-id="27483-109">After you define retention policy, Azure SQL Database starts checking regularly if there are historical rows that are eligible for automatic data cleanup.</span></span> <span data-ttu-id="27483-110">L'identificazione delle righe corrispondenti e la loro rimozione della tabella di cronologia si verificano in modo trasparente, nell'attività in background pianificata ed eseguita dal sistema.</span><span class="sxs-lookup"><span data-stu-id="27483-110">Identification of matching rows and their removal from the history table occur transparently, in the background task that is scheduled and run by the system.</span></span> <span data-ttu-id="27483-111">Le condizioni di età per le righe della tabella della cronologia vengono controllate in base alla colonna che rappresenta la fine del periodo SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="27483-111">Age condition for the history table rows is checked based on the column representing end of SYSTEM_TIME period.</span></span> <span data-ttu-id="27483-112">Se, ad esempio, il periodo di conservazione definito è di sei mesi, le righe della tabella idonee per la pulizia soddisfano la condizione seguente:</span><span class="sxs-lookup"><span data-stu-id="27483-112">If retention period, for example, is set to six months, table rows eligible for cleanup satisfy the following condition:</span></span>

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

<span data-ttu-id="27483-113">L'esempio precedente presuppone che la colonna **ValidTo** corrisponda alla fine del periodo SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="27483-113">In the preceding example, we assumed that **ValidTo** column corresponds to the end of SYSTEM_TIME period.</span></span>

## <a name="how-to-configure-retention-policy"></a><span data-ttu-id="27483-114">Come si configurano i criteri di conservazione?</span><span class="sxs-lookup"><span data-stu-id="27483-114">How to configure retention policy?</span></span>
<span data-ttu-id="27483-115">Prima di configurare criteri di conservazione per una tabella temporale, innanzitutto è necessario controllare se la conservazione della cronologia temporale è abilitata *a livello di database*.</span><span class="sxs-lookup"><span data-stu-id="27483-115">Before you configure retention policy for a temporal table, check first whether temporal historical retention is enabled *at the database level*.</span></span>

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

<span data-ttu-id="27483-116">Il flag del database **is_temporal_history_retention_enabled** è impostato su ON per impostazione predefinita, tuttavia gli utenti possono sostituirlo con l'istruzione ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="27483-116">Database flag **is_temporal_history_retention_enabled** is set to ON by default, but users can change it with ALTER DATABASE statement.</span></span> <span data-ttu-id="27483-117">Inoltre, viene impostato automaticamente su OFF dopo l'operazione di [ripristino temporizzato](sql-database-recovery-using-backups.md).</span><span class="sxs-lookup"><span data-stu-id="27483-117">It is also automatically set to OFF after [point in time restore](sql-database-recovery-using-backups.md) operation.</span></span> <span data-ttu-id="27483-118">Per abilitare la pulizia della conservazione della cronologia temporale per il database, eseguire l'istruzione seguente:</span><span class="sxs-lookup"><span data-stu-id="27483-118">To enable temporal history retention cleanup for your database, execute the following statement:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> <span data-ttu-id="27483-119">È possibile configurare la conservazione per le tabelle temporali anche se **is_temporal_history_retention_enabled** è impostato su OFF. Tuttavia in questo caso la pulizia automatica delle righe obsolete non verrà attivata.</span><span class="sxs-lookup"><span data-stu-id="27483-119">You can configure retention for temporal tables even if **is_temporal_history_retention_enabled** is OFF, but automatic cleanup for aged rows is not triggered in that case.</span></span>
> 
> 

<span data-ttu-id="27483-120">I criteri di conservazione vengono configurati durante la creazione di una tabella specificando il valore per il parametro HISTORY_RETENTION_PERIOD:</span><span class="sxs-lookup"><span data-stu-id="27483-120">Retention policy is configured during table creation by specifying value for the HISTORY_RETENTION_PERIOD parameter:</span></span>

````
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
````

<span data-ttu-id="27483-121">Il database SQL di Azure consente di specificare il periodo di conservazione tramite unità di tempo diverse: DAYS, WEEKS, MONTHS e YEARS.</span><span class="sxs-lookup"><span data-stu-id="27483-121">Azure SQL Database allows you to specify retention period by using different time units: DAYS, WEEKS, MONTHS, and YEARS.</span></span> <span data-ttu-id="27483-122">Se HISTORY_RETENTION_PERIOD viene omesso, viene usata la conservazione INFINITE.</span><span class="sxs-lookup"><span data-stu-id="27483-122">If HISTORY_RETENTION_PERIOD is omitted, INFINITE retention is assumed.</span></span> <span data-ttu-id="27483-123">È inoltre possibile usare esplicitamente la parola chiave INFINITE.</span><span class="sxs-lookup"><span data-stu-id="27483-123">You can also use INFINITE keyword explicitly.</span></span>

<span data-ttu-id="27483-124">In alcuni scenari, è possibile configurare la conservazione dopo la creazione della tabella o per modificare un valore configurato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="27483-124">In some scenarios, you may want to configure retention after table creation, or to change previously configured value.</span></span> <span data-ttu-id="27483-125">In questo caso usare l'istruzione ALTER TABLE:</span><span class="sxs-lookup"><span data-stu-id="27483-125">In that case use ALTER TABLE statement:</span></span>

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> <span data-ttu-id="27483-126">Con l'impostazione di SYSTEM_VERSIONING su OFF il valore relativo al periodo di conservazione *non viene mantenuto*.</span><span class="sxs-lookup"><span data-stu-id="27483-126">Setting SYSTEM_VERSIONING to OFF *does not preserve* retention period value.</span></span> <span data-ttu-id="27483-127">Con l'impostazione di SYSTEM_VERSIONING su ON senza specificare esplicitamente HISTORY_RETENTION_PERIOD si ottiene come risultato un periodo di conservazione INFINITE.</span><span class="sxs-lookup"><span data-stu-id="27483-127">Setting SYSTEM_VERSIONING to ON without HISTORY_RETENTION_PERIOD specified explicitly results in the INFINITE retention period.</span></span>
> 
> 

<span data-ttu-id="27483-128">Per esaminare lo stato corrente del criterio di conservazione, usare la seguente query che unisce il flag di abilitazione della conservazione temporale a livello di database con i periodi di conservazione per le singole tabelle:</span><span class="sxs-lookup"><span data-stu-id="27483-128">To review current state of the retention policy, use the following query that joins temporal retention enablement flag at the database level with retention periods for individual tables:</span></span>

````
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
````


## <a name="how-sql-database-deletes-aged-rows"></a><span data-ttu-id="27483-129">In che modo vengono eliminate le righe obsolete dal database SQL?</span><span class="sxs-lookup"><span data-stu-id="27483-129">How SQL Database deletes aged rows?</span></span>
<span data-ttu-id="27483-130">Il processo di pulizia dipende dal layout indice della tabella di cronologia.</span><span class="sxs-lookup"><span data-stu-id="27483-130">The cleanup process depends on the index layout of the history table.</span></span> <span data-ttu-id="27483-131">È importante notare che *solo nelle tabelle di cronologia con un indice cluster (struttura B-tree o columnstore) è possibile avere la configurazione dei criteri di conservazione definiti*.</span><span class="sxs-lookup"><span data-stu-id="27483-131">It is important to notice that *only history tables with a clustered index (B-tree or columnstore) can have finite retention policy configured*.</span></span> <span data-ttu-id="27483-132">Viene creata un'attività in background per eseguire la pulizia dei dati obsoleti per tutte le tabelle temporali con periodo di conservazione definito.</span><span class="sxs-lookup"><span data-stu-id="27483-132">A background task is created to perform aged data cleanup for all temporal tables with finite retention period.</span></span>
<span data-ttu-id="27483-133">La logica di pulizia per l'indice in cluster rowstore (B-tree) elimina la riga obsoleta in blocchi più piccoli (fino a 10.000) riducendo al minimo pressione sul log del database e sul sottosistema I/O.</span><span class="sxs-lookup"><span data-stu-id="27483-133">Cleanup logic for the rowstore (B-tree) clustered index deletes aged row in smaller chunks (up to 10K) minimizing pressure on database log and I/O subsystem.</span></span> <span data-ttu-id="27483-134">Anche se la logica di pulizia usa un indice B-tree obbligatorio, l'ordine di eliminazione per le righe antecedenti il periodo di conservazione non può essere garantito saldamente.</span><span class="sxs-lookup"><span data-stu-id="27483-134">Although cleanup logic utilizes required B-tree index, order of deletions for the rows older than retention period cannot be firmly guaranteed.</span></span> <span data-ttu-id="27483-135">Di conseguenza, *non è consentito accettare le dipendenze nell'ordine di pulizia nelle applicazioni*.</span><span class="sxs-lookup"><span data-stu-id="27483-135">Hence, *do not take any dependency on the cleanup order in your applications*.</span></span>

<span data-ttu-id="27483-136">L'attività di pulizia per columnstore in cluster rimuove interi [gruppi di righe](https://msdn.microsoft.com/library/gg492088.aspx) in una sola volta (in genere ogni gruppo contiene un milione di righe); questa procedura è molto efficace, soprattutto quando vengono generati dati cronologici a ritmo elevato.</span><span class="sxs-lookup"><span data-stu-id="27483-136">The cleanup task for the clustered columnstore removes entire [row groups](https://msdn.microsoft.com/library/gg492088.aspx) at once (typically contain 1 million of rows each), which is very efficient, especially when historical data is generated at a high pace.</span></span>

![Conservazione di columnstore in cluster](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

<span data-ttu-id="27483-138">Un'ottima compressione dei dati e un'efficace pulizia per la conservazione fanno dell'indice columnstore in cluster la scelta ideale per gli scenari in cui il carico di lavoro genera rapidamente elevate quantità di dati cronologici.</span><span class="sxs-lookup"><span data-stu-id="27483-138">Excellent data compression and efficient retention cleanup makes clustered columnstore index a perfect choice for scenarios when your workload rapidly generates high amount of historical data.</span></span> <span data-ttu-id="27483-139">Tale modello è tipico per un l'[elaborazione transazionale intensiva dei carichi di lavoro che usano tabelle temporali](https://msdn.microsoft.com/library/mt631669.aspx) per il rilevamento delle modifiche e il controllo, l'analisi delle tendenze o l'inserimento dei dati IoT.</span><span class="sxs-lookup"><span data-stu-id="27483-139">That pattern is typical for intensive [transactional processing workloads that use temporal tables](https://msdn.microsoft.com/library/mt631669.aspx) for change tracking and auditing, trend analysis, or IoT data ingestion.</span></span>

## <a name="index-considerations"></a><span data-ttu-id="27483-140">Considerazioni sull'indice</span><span class="sxs-lookup"><span data-stu-id="27483-140">Index considerations</span></span>
<span data-ttu-id="27483-141">L'attività di pulizia per le tabelle con indice rowstore in cluster richiede che l'indice inizi con la colonna che corrisponde alla fine del periodo SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="27483-141">The cleanup task for tables with rowstore clustered index requires index to start with the column corresponding the end of SYSTEM_TIME period.</span></span> <span data-ttu-id="27483-142">Se questa colonna non esiste, non è possibile configurare un periodo di conservazione finito:</span><span class="sxs-lookup"><span data-stu-id="27483-142">If such index doesn't exist, you cannot configure a finite retention period:</span></span>

<span data-ttu-id="27483-143">*Msg 13765, Level 16, State 1 <br></br> L'impostazione del periodo di conservazione definito ha avuto esito negativo nella tabella temporale con controllo delle versioni del sistema 'temporalstagetestdb.dbo.WebsiteUserInfo' perché la tabella di cronologia 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' non contiene l'indice in cluster richiesto. È consigliabile creare un columnstore cluster o indice B-tree a partire dalla colonna che corrisponde alla fine del periodo SYSTEM_TIME nella tabella di cronologia.*</span><span class="sxs-lookup"><span data-stu-id="27483-143">*Msg 13765, Level 16, State 1 <br></br> Setting finite retention period failed on system-versioned temporal table 'temporalstagetestdb.dbo.WebsiteUserInfo' because the history table 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' does not contain required clustered index. Consider creating a clustered columnstore or B-tree index starting with the column that matches end of SYSTEM_TIME period, on the history table.*</span></span>

<span data-ttu-id="27483-144">È importante notare che la tabella di cronologia predefinito già creata dal database SQL di Azure dispone già dell'indice in cluster, che è conforme a criteri di conservazione.</span><span class="sxs-lookup"><span data-stu-id="27483-144">It is important to notice that the default history table created by Azure SQL Database already has clustered index, which is compliant for retention policy.</span></span> <span data-ttu-id="27483-145">Se si tenta di rimuovere l'indice in una tabella con periodo di conservazione definito, l'operazione ha esito negativo con l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="27483-145">If you try to remove that index on a table with finite retention period, operation fails with the following error:</span></span>

<span data-ttu-id="27483-146">*Msg 13766, Level 16, State 1 <br></br> Impossibile eliminare l'indice cluster 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' perché è usato per la pulizia automatica dei dati obsoleti. Si consiglia di impostare HISTORY_RETENTION_PERIOD su INFINITE nella corrispondente tabella temporale con controllo delle versioni del sistema se è necessario eliminare l'indice.*</span><span class="sxs-lookup"><span data-stu-id="27483-146">*Msg 13766, Level 16, State 1 <br></br> Cannot drop the clustered index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' because it is being used for automatic cleanup of aged data. Consider setting HISTORY_RETENTION_PERIOD to INFINITE on the corresponding system-versioned temporal table if you need to drop this index.*</span></span>

<span data-ttu-id="27483-147">La pulizia dell'indice columnstore in cluster funziona in modo ottimale se vengono inserite righe cronologiche in ordine crescente (ordinate in base alla fine della colonna del periodo); questo viene sempre applicato quando la tabella di cronologia viene popolata esclusivamente dal meccanismo SYSTEM_VERSIONIOING.</span><span class="sxs-lookup"><span data-stu-id="27483-147">Cleanup on the clustered columnstore index works optimally if historical rows are inserted in the ascending order (ordered by the end of period column), which is always the case when the history table is populated exclusively by the SYSTEM_VERSIONIOING mechanism.</span></span> <span data-ttu-id="27483-148">Se le righe della tabella di cronologia non sono ordinate in base alla fine della colonna del periodo (ad esempio in caso di migrazione dei dati cronologici esistenti), è necessario ricreare un indice columnstore in cluster sull'indice rowstore B-tree ordinato in modo corretto, per ottenere prestazioni ottimali.</span><span class="sxs-lookup"><span data-stu-id="27483-148">If rows in the history table are not ordered by end of period column (which may be the case if you migrated existing historical data), you should re-create clustered columnstore index on top of B-tree rowstore index that is properly ordered, to achieve optimal performance.</span></span>

<span data-ttu-id="27483-149">Evitare la ricompilazione dell'indice columnstore in cluster nella tabella di cronologia con il periodo di conservazione definito, perché può cambiare l'ordine nei gruppi di righe imposti naturalmente dall'operazione di controllo delle versioni di sistema.</span><span class="sxs-lookup"><span data-stu-id="27483-149">Avoid rebuilding clustered columnstore index on the history table with the finite retention period, because it may change ordering in the row groups naturally imposed by the system-versioning operation.</span></span> <span data-ttu-id="27483-150">Se è necessario ricompilare l'indice columnstore in cluster della tabella di cronologia, crearne uno nuovo al posto dell'indice B-tree conforme, mantenendo l'ordinamento in gruppi di righe necessario per la pulizia dei dati regolare.</span><span class="sxs-lookup"><span data-stu-id="27483-150">If you need to rebuild clustered columnstore index on the history table, do that by re-creating it on top of compliant B-tree index, preserving ordering in the rowgroups necessary for regular data cleanup.</span></span> <span data-ttu-id="27483-151">Lo stesso approccio deve essere adottato se si crea una tabella temporale con la tabella di cronologia esistente che dispone di un indice di colonna in cluster senza ordine dei dati garantito:</span><span class="sxs-lookup"><span data-stu-id="27483-151">The same approach should be taken if you create temporal table with existing history table that has clustered column index without guaranteed data order:</span></span>

````
/*Create B-tree ordered by the end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

<span data-ttu-id="27483-152">Quando viene configurato il periodo di conservazione definito per la tabella di cronologia con l'indice columnstore in cluster, non è possibile creare indici B-tree non in cluster aggiuntivi nella tabella:</span><span class="sxs-lookup"><span data-stu-id="27483-152">When finite retention period is configured for the history table with the clustered columnstore index, you cannot create additional non-clustered B-tree indexes on that table:</span></span>

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

<span data-ttu-id="27483-153">Un tentativo di eseguire l'istruzione sopra indicata avrà esito negativo con l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="27483-153">An attempt to execute above statement fails with the following error:</span></span>

<span data-ttu-id="27483-154">*Msg 13772, Level 16, State 1 <br></br> Impossibile creare un indice non in cluster in una tabella di cronologia temporale 'WebsiteUserInfoHistory' perché ha un periodo di conservazione definito e l'indice columnstore in cluster è definito.*</span><span class="sxs-lookup"><span data-stu-id="27483-154">*Msg 13772, Level 16, State 1 <br></br> Cannot create non-clustered index on a temporal history table 'WebsiteUserInfoHistory' since it has finite retention period and clustered columnstore index defined.*</span></span>

## <a name="querying-tables-with-retention-policy"></a><span data-ttu-id="27483-155">Esecuzione di query su tabelle con criteri di conservazione</span><span class="sxs-lookup"><span data-stu-id="27483-155">Querying tables with retention policy</span></span>
<span data-ttu-id="27483-156">Tutte le query sulla tabella temporale consentono di escludere automaticamente tramite filtro le righe cronolgiche definite corrispondenti, per evitare risultati imprevisti e incoerenti, poiché è possibile eliminare righe obsolete tramite l'attività di pulizia, *in qualsiasi momento e in ordine arbitrario*.</span><span class="sxs-lookup"><span data-stu-id="27483-156">All queries on the temporal table automatically filter out historical rows matching finite retention policy, to avoid unpredictable and inconsistent results, since aged rows can be deleted by the cleanup task, *at any point in time and in arbitrary order*.</span></span>

<span data-ttu-id="27483-157">Nell'immagine seguente viene illustrato il piano di query per una query semplice:</span><span class="sxs-lookup"><span data-stu-id="27483-157">The following picture shows the query plan for a simple query:</span></span>

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

<span data-ttu-id="27483-158">Il piano di query include un altro filtro applicato alla fine della colonna del periodo (ValidTo) nell'operatore Clustered Index Scan nella tabella di cronologia (evidenziata).</span><span class="sxs-lookup"><span data-stu-id="27483-158">The query plan includes additional filter applied to end of period column (ValidTo) in the Clustered Index Scan operator on the history table (highlighted).</span></span> <span data-ttu-id="27483-159">Questo esempio presuppone che il periodo di conservazione di un MONTH sia stato impostato nella tabella WebsiteUserInfo.</span><span class="sxs-lookup"><span data-stu-id="27483-159">This example assumes that one MONTH retention period was set on WebsiteUserInfo table.</span></span>

![Filtro di query di conservazione](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

<span data-ttu-id="27483-161">Tuttavia, se si esegue una query direttamente in una tabella di cronologia, è possibile vedere le righe precedenti al periodo di conservazione specificato, ma senza alcuna garanzia relativa ai risultati ripetibili.</span><span class="sxs-lookup"><span data-stu-id="27483-161">However, if you query history table directly, you may see rows that are older than specified retention period, but without any guarantee for repeatable query results.</span></span> <span data-ttu-id="27483-162">Nell'immagine seguente è mostrato il piano di esecuzione di query per la query nella tabella di cronologia senza altri filtri applicati:</span><span class="sxs-lookup"><span data-stu-id="27483-162">The following picture shows query execution plan for the query on the history table without additional filters applied:</span></span>

![Esecuzione di query senza filtro di conservazione](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

<span data-ttu-id="27483-164">Non affidare la logica di business alla lettura della tabella di cronologia oltre il periodo di conservazione, perché si potrebbero ottenere risultati incoerenti o imprevisti.</span><span class="sxs-lookup"><span data-stu-id="27483-164">Do not rely your business logic on reading history table beyond retention period as you may get inconsistent or unexpected results.</span></span> <span data-ttu-id="27483-165">È consigliabile usare query temporali con la clausola FOR SYSTEM_TIME per l'analisi dei dati nelle tabelle temporali.</span><span class="sxs-lookup"><span data-stu-id="27483-165">We recommend that you use temporal queries with FOR SYSTEM_TIME clause for analyzing data in temporal tables.</span></span>

## <a name="point-in-time-restore-considerations"></a><span data-ttu-id="27483-166">Considerazioni sul ripristino temporizzato</span><span class="sxs-lookup"><span data-stu-id="27483-166">Point in time restore considerations</span></span>
<span data-ttu-id="27483-167">Quando si crea un nuovo database attraverso il [ripristino di un database esistente in un punto specifico nel tempo](sql-database-recovery-using-backups.md), la conservazione temporale è disabilitata a livello di database.</span><span class="sxs-lookup"><span data-stu-id="27483-167">When you create new database by [restoring existing database to a specific point in time](sql-database-recovery-using-backups.md), it has temporal retention disabled at the database level.</span></span> <span data-ttu-id="27483-168">(Il flag **is_temporal_history_retention_enabled** è impostato su OFF).</span><span class="sxs-lookup"><span data-stu-id="27483-168">(**is_temporal_history_retention_enabled** flag set to OFF).</span></span> <span data-ttu-id="27483-169">Questa funzionalità consente di esaminare tutte le righe di cronologia al momento del ripristino, senza doversi preoccupare che le righe obsolete vengano rimosse prima di procedere con l'esecuzione di query.</span><span class="sxs-lookup"><span data-stu-id="27483-169">This functionality allows you to examine all historical rows upon restore, without worrying that aged rows are removed before you get to query them.</span></span> <span data-ttu-id="27483-170">È possibile usarla per *esaminare i dati cronologici oltre il periodo di conservazione configurato*.</span><span class="sxs-lookup"><span data-stu-id="27483-170">You can use it to *inspect historical data beyond configured retention period*.</span></span>

<span data-ttu-id="27483-171">Si supponga che per una tabella temporale sia specificato il periodo di conservazione MONTH.</span><span class="sxs-lookup"><span data-stu-id="27483-171">Say that a temporal table has one MONTH retention period specified.</span></span> <span data-ttu-id="27483-172">Se il database è stato creato al livello di servizio Premium, è possibile creare una copia del database con lo stato del database risalendo fino a 35 giorni prima.</span><span class="sxs-lookup"><span data-stu-id="27483-172">If your database was created in Premium Service tier, you would be able to create database copy with the database state up to 35 days back in the past.</span></span> <span data-ttu-id="27483-173">Una tale efficacia consentirebbe di analizzare le righe cronologiche risalenti anche a 65 giorni prima eseguendo una query direttamente nella tabella di cronologia.</span><span class="sxs-lookup"><span data-stu-id="27483-173">That effectively would allow you to analyze historical rows that are up to 65 days old by querying the history table directly.</span></span>

<span data-ttu-id="27483-174">Se si desidera attivare la pulizia della conservazione temporale, eseguire l'istruzione Transact-SQL seguente dopo il ripristino temporizzato:</span><span class="sxs-lookup"><span data-stu-id="27483-174">If you want to activate temporal retention cleanup, run the following Transact-SQL statement after point in time restore:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a><span data-ttu-id="27483-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="27483-175">Next steps</span></span>
<span data-ttu-id="27483-176">Per informazioni su come usare le tabelle temporali nelle applicazioni, consultare [Introduzione alle tabelle temporali nel database SQL di Azure](sql-database-temporal-tables.md).</span><span class="sxs-lookup"><span data-stu-id="27483-176">To learn how to use Temporal Tables in your applications, check out [Getting Started with Temporal Tables in Azure SQL Database](sql-database-temporal-tables.md).</span></span>

<span data-ttu-id="27483-177">Andare su Channel 9 per ascoltare una [storia di successo reale relativa all'implementazione temporale di un cliente](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) e guardare una [dimostrazione temporale in tempo reale](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="27483-177">Visit Channel 9 to hear a [real customer temporal implementation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

<span data-ttu-id="27483-178">Per informazioni dettagliate sulle tabelle temporali, esaminare la [documentazione su MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="27483-178">For detailed information about Temporal Tables, review [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>

