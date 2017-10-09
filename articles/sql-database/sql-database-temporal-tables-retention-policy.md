---
title: aaaManage i dati cronologici nelle tabelle temporali con criteri di conservazione | Documenti Microsoft
description: Informazioni su come toouse conservazione temporale criteri tookeep dati cronologici sotto il proprio controllo.
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
ms.openlocfilehash: a72a6111a6cd7322d734d08bf3852e95f5ffea8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a><span data-ttu-id="251c6-103">Gestire i dati cronologici nelle tabelle temporali con criteri di conservazione</span><span class="sxs-lookup"><span data-stu-id="251c6-103">Manage historical data in Temporal Tables with retention policy</span></span>
<span data-ttu-id="251c6-104">Le tabelle temporali possono aumentare le dimensioni del database più delle tabelle normali, in particolare se si conservano i dati cronologici per un periodo di tempo più lungo.</span><span class="sxs-lookup"><span data-stu-id="251c6-104">Temporal Tables may increase database size more than regular tables, especially if you retain historical data for a longer period of time.</span></span> <span data-ttu-id="251c6-105">Di conseguenza, i criteri di conservazione dei dati cronologici sono un aspetto importante della pianificazione e gestione del ciclo di vita di hello di ogni tabella temporale.</span><span class="sxs-lookup"><span data-stu-id="251c6-105">Hence, retention policy for historical data is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="251c6-106">Le tabelle temporali nel database SQL Azure sono dotate di un meccanismo di conservazione di facile uso che aiuta a eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="251c6-106">Temporal Tables in Azure SQL Database come with easy-to-use retention mechanism that helps you accomplish this task.</span></span>

<span data-ttu-id="251c6-107">Periodo memorizzazione cronologia temporale può essere configurate a livello di singola tabella hello, che consente agli utenti di criteri di durata flessibile toocreate.</span><span class="sxs-lookup"><span data-stu-id="251c6-107">Temporal history retention can be configured at hello individual table level, which allows users toocreate flexible aging polices.</span></span> <span data-ttu-id="251c6-108">L'applicazione di memorizzazione temporale è semplice: è necessario un solo parametro toobe, impostato durante la modifica dello schema o di creazione tabella.</span><span class="sxs-lookup"><span data-stu-id="251c6-108">Applying temporal retention is simple: it requires only one parameter toobe set during table creation or schema change.</span></span>

<span data-ttu-id="251c6-109">Dopo aver definito i criteri di conservazione, il database SQL di Azure avvia una verifica periodica per controllare se sono presenti righe di cronologia idonee alla pulizia automatica dei dati.</span><span class="sxs-lookup"><span data-stu-id="251c6-109">After you define retention policy, Azure SQL Database starts checking regularly if there are historical rows that are eligible for automatic data cleanup.</span></span> <span data-ttu-id="251c6-110">Identificazione delle righe corrispondenti e la rimozione dalla tabella di cronologia hello si verificano in modo trasparente, attività in background pianificata, eseguire dal sistema hello hello.</span><span class="sxs-lookup"><span data-stu-id="251c6-110">Identification of matching rows and their removal from hello history table occur transparently, in hello background task that is scheduled and run by hello system.</span></span> <span data-ttu-id="251c6-111">Condizione di validità per le righe nella tabella di cronologia hello viene controllato in base colonna hello che rappresenta di fine del periodo SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="251c6-111">Age condition for hello history table rows is checked based on hello column representing end of SYSTEM_TIME period.</span></span> <span data-ttu-id="251c6-112">Se il periodo di memorizzazione, ad esempio, è impostato toosix mesi, le righe della tabella idonee per la pulizia soddisfano hello seguente condizione:</span><span class="sxs-lookup"><span data-stu-id="251c6-112">If retention period, for example, is set toosix months, table rows eligible for cleanup satisfy hello following condition:</span></span>

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

<span data-ttu-id="251c6-113">Nella finestra di hello sopra riportato, si presuppone che **ValidTo** colonna corrisponde toohello fine del periodo SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="251c6-113">In hello preceding example, we assumed that **ValidTo** column corresponds toohello end of SYSTEM_TIME period.</span></span>

## <a name="how-tooconfigure-retention-policy"></a><span data-ttu-id="251c6-114">Come criteri di conservazione tooconfigure?</span><span class="sxs-lookup"><span data-stu-id="251c6-114">How tooconfigure retention policy?</span></span>
<span data-ttu-id="251c6-115">Prima di configurare criteri di conservazione per una tabella temporale, controllare innanzitutto se è abilitato memorizzazione cronologia temporale *a livello di database hello*.</span><span class="sxs-lookup"><span data-stu-id="251c6-115">Before you configure retention policy for a temporal table, check first whether temporal historical retention is enabled *at hello database level*.</span></span>

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

<span data-ttu-id="251c6-116">Flag del database **is_temporal_history_retention_enabled** è tooON set per impostazione predefinita, ma gli utenti possono modificare con l'istruzione ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="251c6-116">Database flag **is_temporal_history_retention_enabled** is set tooON by default, but users can change it with ALTER DATABASE statement.</span></span> <span data-ttu-id="251c6-117">È inoltre automaticamente tooOFF set dopo [ripristino temporizzato](sql-database-recovery-using-backups.md) operazione.</span><span class="sxs-lookup"><span data-stu-id="251c6-117">It is also automatically set tooOFF after [point in time restore](sql-database-recovery-using-backups.md) operation.</span></span> <span data-ttu-id="251c6-118">pulizia di memorizzazione cronologia temporale tooenable per il database, eseguire hello seguente istruzione:</span><span class="sxs-lookup"><span data-stu-id="251c6-118">tooenable temporal history retention cleanup for your database, execute hello following statement:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> <span data-ttu-id="251c6-119">È possibile configurare la conservazione per le tabelle temporali anche se **is_temporal_history_retention_enabled** è impostato su OFF. Tuttavia in questo caso la pulizia automatica delle righe obsolete non verrà attivata.</span><span class="sxs-lookup"><span data-stu-id="251c6-119">You can configure retention for temporal tables even if **is_temporal_history_retention_enabled** is OFF, but automatic cleanup for aged rows is not triggered in that case.</span></span>
> 
> 

<span data-ttu-id="251c6-120">Criteri di conservazione viene configurato durante la creazione della tabella, specificando un valore per il parametro HISTORY_RETENTION_PERIOD hello:</span><span class="sxs-lookup"><span data-stu-id="251c6-120">Retention policy is configured during table creation by specifying value for hello HISTORY_RETENTION_PERIOD parameter:</span></span>

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

<span data-ttu-id="251c6-121">Database SQL di Azure consente il periodo di memorizzazione toospecify con unità di tempo diversi: giorni, settimane, mesi e anni.</span><span class="sxs-lookup"><span data-stu-id="251c6-121">Azure SQL Database allows you toospecify retention period by using different time units: DAYS, WEEKS, MONTHS, and YEARS.</span></span> <span data-ttu-id="251c6-122">Se HISTORY_RETENTION_PERIOD viene omesso, viene usata la conservazione INFINITE.</span><span class="sxs-lookup"><span data-stu-id="251c6-122">If HISTORY_RETENTION_PERIOD is omitted, INFINITE retention is assumed.</span></span> <span data-ttu-id="251c6-123">È inoltre possibile usare esplicitamente la parola chiave INFINITE.</span><span class="sxs-lookup"><span data-stu-id="251c6-123">You can also use INFINITE keyword explicitly.</span></span>

<span data-ttu-id="251c6-124">In alcuni scenari, è opportuno tooconfigure conservazione dopo la creazione della tabella o toochange precedentemente configurato come valore.</span><span class="sxs-lookup"><span data-stu-id="251c6-124">In some scenarios, you may want tooconfigure retention after table creation, or toochange previously configured value.</span></span> <span data-ttu-id="251c6-125">In questo caso usare l'istruzione ALTER TABLE:</span><span class="sxs-lookup"><span data-stu-id="251c6-125">In that case use ALTER TABLE statement:</span></span>

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> <span data-ttu-id="251c6-126">Impostazione dell'attributo SYSTEM_VERSIONING tooOFF *non mantiene* valore del periodo di memorizzazione.</span><span class="sxs-lookup"><span data-stu-id="251c6-126">Setting SYSTEM_VERSIONING tooOFF *does not preserve* retention period value.</span></span> <span data-ttu-id="251c6-127">Impostazione dell'attributo SYSTEM_VERSIONING tooON senza HISTORY_RETENTION_PERIOD specificato esplicitamente risultati nel periodo di conservazione infinito hello.</span><span class="sxs-lookup"><span data-stu-id="251c6-127">Setting SYSTEM_VERSIONING tooON without HISTORY_RETENTION_PERIOD specified explicitly results in hello INFINITE retention period.</span></span>
> 
> 

<span data-ttu-id="251c6-128">stato corrente di tooreview del criterio di conservazione hello, tale flag di abilitazione della memorizzazione temporale join a livello di database hello con periodi di memorizzazione per le singole tabelle di query utilizzare hello seguente:</span><span class="sxs-lookup"><span data-stu-id="251c6-128">tooreview current state of hello retention policy, use hello following query that joins temporal retention enablement flag at hello database level with retention periods for individual tables:</span></span>

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


## <a name="how-sql-database-deletes-aged-rows"></a><span data-ttu-id="251c6-129">In che modo vengono eliminate le righe obsolete dal database SQL?</span><span class="sxs-lookup"><span data-stu-id="251c6-129">How SQL Database deletes aged rows?</span></span>
<span data-ttu-id="251c6-130">il processo di pulizia Hello dipende dal layout indice hello della tabella di cronologia hello.</span><span class="sxs-lookup"><span data-stu-id="251c6-130">hello cleanup process depends on hello index layout of hello history table.</span></span> <span data-ttu-id="251c6-131">È importante toonotice che *solo le tabelle di cronologia con un indice cluster (albero B o columnstore) possono avere criteri di conservazione finito configurato*.</span><span class="sxs-lookup"><span data-stu-id="251c6-131">It is important toonotice that *only history tables with a clustered index (B-tree or columnstore) can have finite retention policy configured*.</span></span> <span data-ttu-id="251c6-132">Un'attività in background viene creata tooperform pulizia dei dati obsoleti per tutte le tabelle temporali con periodo di memorizzazione finito.</span><span class="sxs-lookup"><span data-stu-id="251c6-132">A background task is created tooperform aged data cleanup for all temporal tables with finite retention period.</span></span>
<span data-ttu-id="251c6-133">Logica di pulizia per l'indice cluster rowstore (albero B) di hello Elimina riga obsoleto in blocchi più piccoli (backup too10K) riducendo al minimo l'utilizzo nei log del database e il sottosistema dei / o.</span><span class="sxs-lookup"><span data-stu-id="251c6-133">Cleanup logic for hello rowstore (B-tree) clustered index deletes aged row in smaller chunks (up too10K) minimizing pressure on database log and I/O subsystem.</span></span> <span data-ttu-id="251c6-134">Anche se viene utilizzata la logica di pulizia necessarie indice B-tree, ordine di eliminazioni di righe hello anteriore al periodo di conservazione non può essere garantito sia ben.</span><span class="sxs-lookup"><span data-stu-id="251c6-134">Although cleanup logic utilizes required B-tree index, order of deletions for hello rows older than retention period cannot be firmly guaranteed.</span></span> <span data-ttu-id="251c6-135">Di conseguenza, *non accettano tutte le dipendenze nell'ordine di pulizia hello nelle applicazioni*.</span><span class="sxs-lookup"><span data-stu-id="251c6-135">Hence, *do not take any dependency on hello cleanup order in your applications*.</span></span>

<span data-ttu-id="251c6-136">Hello attività di pulizia per hello clustered columnstore rimuove intero [gruppi di righe](https://msdn.microsoft.com/library/gg492088.aspx) in una sola volta (in genere contiene 1 milione di righe ogni), che è molto efficiente, in particolare quando i dati cronologici viene generati a un ritmo elevato.</span><span class="sxs-lookup"><span data-stu-id="251c6-136">hello cleanup task for hello clustered columnstore removes entire [row groups](https://msdn.microsoft.com/library/gg492088.aspx) at once (typically contain 1 million of rows each), which is very efficient, especially when historical data is generated at a high pace.</span></span>

![Conservazione di columnstore in cluster](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

<span data-ttu-id="251c6-138">Un'ottima compressione dei dati e un'efficace pulizia per la conservazione fanno dell'indice columnstore in cluster la scelta ideale per gli scenari in cui il carico di lavoro genera rapidamente elevate quantità di dati cronologici.</span><span class="sxs-lookup"><span data-stu-id="251c6-138">Excellent data compression and efficient retention cleanup makes clustered columnstore index a perfect choice for scenarios when your workload rapidly generates high amount of historical data.</span></span> <span data-ttu-id="251c6-139">Tale modello è tipico per un l'[elaborazione transazionale intensiva dei carichi di lavoro che usano tabelle temporali](https://msdn.microsoft.com/library/mt631669.aspx) per il rilevamento delle modifiche e il controllo, l'analisi delle tendenze o l'inserimento dei dati IoT.</span><span class="sxs-lookup"><span data-stu-id="251c6-139">That pattern is typical for intensive [transactional processing workloads that use temporal tables](https://msdn.microsoft.com/library/mt631669.aspx) for change tracking and auditing, trend analysis, or IoT data ingestion.</span></span>

## <a name="index-considerations"></a><span data-ttu-id="251c6-140">Considerazioni sull'indice</span><span class="sxs-lookup"><span data-stu-id="251c6-140">Index considerations</span></span>
<span data-ttu-id="251c6-141">attività di pulizia Hello per le tabelle con indice cluster rowstore richiede indice toostart con estremità corrispondente hello hello colonna di periodo SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="251c6-141">hello cleanup task for tables with rowstore clustered index requires index toostart with hello column corresponding hello end of SYSTEM_TIME period.</span></span> <span data-ttu-id="251c6-142">Se questa colonna non esiste, non è possibile configurare un periodo di conservazione finito:</span><span class="sxs-lookup"><span data-stu-id="251c6-142">If such index doesn't exist, you cannot configure a finite retention period:</span></span>

<span data-ttu-id="251c6-143">*Msg 13765, livello 16, stato 1 <br> </br> impostazione periodo di memorizzazione finito non è riuscita nella tabella temporale con controllo delle versioni del sistema 'temporalstagetestdb.dbo.WebsiteUserInfo' perché la tabella di cronologia hello ' temporalstagetestdb.dbo.WebsiteUserInfoHistory' non contiene alcun indice cluster richiesto. È consigliabile creare una columnstore cluster o un indice albero B a partire dalla colonna hello corrispondente alla fine di SYSTEM_TIME period, nella tabella di cronologia hello.*</span><span class="sxs-lookup"><span data-stu-id="251c6-143">*Msg 13765, Level 16, State 1 <br></br> Setting finite retention period failed on system-versioned temporal table 'temporalstagetestdb.dbo.WebsiteUserInfo' because hello history table 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' does not contain required clustered index. Consider creating a clustered columnstore or B-tree index starting with hello column that matches end of SYSTEM_TIME period, on hello history table.*</span></span>

<span data-ttu-id="251c6-144">È importante toonotice che hello tabella di cronologia predefinita creata dal Database di SQL Azure è già un indice, che è conforme a criteri di conservazione è cluster.</span><span class="sxs-lookup"><span data-stu-id="251c6-144">It is important toonotice that hello default history table created by Azure SQL Database already has clustered index, which is compliant for retention policy.</span></span> <span data-ttu-id="251c6-145">Se si tenta di tooremove tale indice in una tabella con periodo di memorizzazione finito, operazione non riesce con hello errore seguente:</span><span class="sxs-lookup"><span data-stu-id="251c6-145">If you try tooremove that index on a table with finite retention period, operation fails with hello following error:</span></span>

<span data-ttu-id="251c6-146">*Msg 13766, livello 16, stato 1 <br> </br> non è possibile eliminare l'indice cluster hello 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' perché è utilizzato per la pulizia automatica dei dati obsoleti. Prendere in considerazione impostazione HISTORY_RETENTION_PERIOD tooINFINITE sulla tabella di temporale con controllo delle versioni del sistema corrispondente hello se è necessario toodrop questo indice.*</span><span class="sxs-lookup"><span data-stu-id="251c6-146">*Msg 13766, Level 16, State 1 <br></br> Cannot drop hello clustered index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' because it is being used for automatic cleanup of aged data. Consider setting HISTORY_RETENTION_PERIOD tooINFINITE on hello corresponding system-versioned temporal table if you need toodrop this index.*</span></span>

<span data-ttu-id="251c6-147">Pulizia sull'indice columnstore cluster hello funziona in modo ottimale se vengono inserite righe cronologiche in ordine crescente (ordinati in base al fine di hello della colonna periodo), che avviene sempre hello quando la tabella di cronologia hello viene popolata in modo esclusivo da hello System _ hello Meccanismo VERSIONIOING.</span><span class="sxs-lookup"><span data-stu-id="251c6-147">Cleanup on hello clustered columnstore index works optimally if historical rows are inserted in hello ascending order (ordered by hello end of period column), which is always hello case when hello history table is populated exclusively by hello SYSTEM_VERSIONIOING mechanism.</span></span> <span data-ttu-id="251c6-148">Se righe nella tabella di cronologia hello non vengono ordinate dalla fine della colonna periodo (che può essere case hello se sono stati migrati i dati cronologici esistenti), è necessario ricreare un indice columnstore cluster in indice rowstore con albero B ordinata correttamente, tooachieve ottimale prestazioni.</span><span class="sxs-lookup"><span data-stu-id="251c6-148">If rows in hello history table are not ordered by end of period column (which may be hello case if you migrated existing historical data), you should re-create clustered columnstore index on top of B-tree rowstore index that is properly ordered, tooachieve optimal performance.</span></span>

<span data-ttu-id="251c6-149">Evitare di ricompilare l'indice columnstore cluster nella tabella di cronologia hello con periodo di memorizzazione finito di hello, poiché potrebbe essere modificato l'ordinamento in gruppi di righe hello naturalmente imposti dall'operazione di controllo delle versioni di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="251c6-149">Avoid rebuilding clustered columnstore index on hello history table with hello finite retention period, because it may change ordering in hello row groups naturally imposed by hello system-versioning operation.</span></span> <span data-ttu-id="251c6-150">Se si desidera toorebuild l'indice columnstore cluster nella tabella di cronologia hello, a tale scopo crearne uno nuovo nella parte superiore conformi indice albero B, mantenendo l'ordinamento in rowgroup hello necessarie per la pulizia dei dati regolare.</span><span class="sxs-lookup"><span data-stu-id="251c6-150">If you need toorebuild clustered columnstore index on hello history table, do that by re-creating it on top of compliant B-tree index, preserving ordering in hello rowgroups necessary for regular data cleanup.</span></span> <span data-ttu-id="251c6-151">Hello stesso approccio deve essere eseguita se si crea una tabella temporale con tabella di cronologia esistente che dispone di un indice di colonna senza ordine dei dati garantita cluster:</span><span class="sxs-lookup"><span data-stu-id="251c6-151">hello same approach should be taken if you create temporal table with existing history table that has clustered column index without guaranteed data order:</span></span>

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

<span data-ttu-id="251c6-152">Quando il periodo di memorizzazione finito è configurato per la tabella di cronologia hello con indice columnstore cluster hello, è possibile creare indici albero B non cluster aggiuntivi in tale tabella:</span><span class="sxs-lookup"><span data-stu-id="251c6-152">When finite retention period is configured for hello history table with hello clustered columnstore index, you cannot create additional non-clustered B-tree indexes on that table:</span></span>

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

<span data-ttu-id="251c6-153">Un tentativo tooexecute prima istruzione non riesce con hello errore seguente:</span><span class="sxs-lookup"><span data-stu-id="251c6-153">An attempt tooexecute above statement fails with hello following error:</span></span>

<span data-ttu-id="251c6-154">*Msg 13772, Level 16, State 1 <br></br> Impossibile creare un indice non in cluster in una tabella di cronologia temporale 'WebsiteUserInfoHistory' perché ha un periodo di conservazione definito e l'indice columnstore in cluster è definito.*</span><span class="sxs-lookup"><span data-stu-id="251c6-154">*Msg 13772, Level 16, State 1 <br></br> Cannot create non-clustered index on a temporal history table 'WebsiteUserInfoHistory' since it has finite retention period and clustered columnstore index defined.*</span></span>

## <a name="querying-tables-with-retention-policy"></a><span data-ttu-id="251c6-155">Esecuzione di query su tabelle con criteri di conservazione</span><span class="sxs-lookup"><span data-stu-id="251c6-155">Querying tables with retention policy</span></span>
<span data-ttu-id="251c6-156">Tutte le query sulla tabella temporale hello filtrare automaticamente le righe di cronologia corrispondente di criteri di conservazione finito tooavoid risultati imprevedibili e incoerente, poiché è possono eliminare le righe obsolete tramite attività di pulizia hello, *in qualsiasi punto nel tempo e in ordine arbitrario*.</span><span class="sxs-lookup"><span data-stu-id="251c6-156">All queries on hello temporal table automatically filter out historical rows matching finite retention policy, tooavoid unpredictable and inconsistent results, since aged rows can be deleted by hello cleanup task, *at any point in time and in arbitrary order*.</span></span>

<span data-ttu-id="251c6-157">Hello immagine riportata di seguito viene illustrato il piano di query hello per una query semplice:</span><span class="sxs-lookup"><span data-stu-id="251c6-157">hello following picture shows hello query plan for a simple query:</span></span>

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

<span data-ttu-id="251c6-158">query Hello piano include ulteriore filtro applicato tooend della colonna periodo (ValidTo) nell'operatore Clustered Index Scan hello nella tabella di cronologia hello (evidenziata).</span><span class="sxs-lookup"><span data-stu-id="251c6-158">hello query plan includes additional filter applied tooend of period column (ValidTo) in hello Clustered Index Scan operator on hello history table (highlighted).</span></span> <span data-ttu-id="251c6-159">Questo esempio presuppone che il periodo di conservazione di un MONTH sia stato impostato nella tabella WebsiteUserInfo.</span><span class="sxs-lookup"><span data-stu-id="251c6-159">This example assumes that one MONTH retention period was set on WebsiteUserInfo table.</span></span>

![Filtro di query di conservazione](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

<span data-ttu-id="251c6-161">Tuttavia, se si esegue una query direttamente in una tabella di cronologia, è possibile vedere le righe precedenti al periodo di conservazione specificato, ma senza alcuna garanzia relativa ai risultati ripetibili.</span><span class="sxs-lookup"><span data-stu-id="251c6-161">However, if you query history table directly, you may see rows that are older than specified retention period, but without any guarantee for repeatable query results.</span></span> <span data-ttu-id="251c6-162">Hello immagine seguente viene illustrato un piano di esecuzione per query hello nella tabella di cronologia hello senza filtri aggiuntivi applicati:</span><span class="sxs-lookup"><span data-stu-id="251c6-162">hello following picture shows query execution plan for hello query on hello history table without additional filters applied:</span></span>

![Esecuzione di query senza filtro di conservazione](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

<span data-ttu-id="251c6-164">Non affidare la logica di business alla lettura della tabella di cronologia oltre il periodo di conservazione, perché si potrebbero ottenere risultati incoerenti o imprevisti.</span><span class="sxs-lookup"><span data-stu-id="251c6-164">Do not rely your business logic on reading history table beyond retention period as you may get inconsistent or unexpected results.</span></span> <span data-ttu-id="251c6-165">È consigliabile usare query temporali con la clausola FOR SYSTEM_TIME per l'analisi dei dati nelle tabelle temporali.</span><span class="sxs-lookup"><span data-stu-id="251c6-165">We recommend that you use temporal queries with FOR SYSTEM_TIME clause for analyzing data in temporal tables.</span></span>

## <a name="point-in-time-restore-considerations"></a><span data-ttu-id="251c6-166">Considerazioni sul ripristino temporizzato</span><span class="sxs-lookup"><span data-stu-id="251c6-166">Point in time restore considerations</span></span>
<span data-ttu-id="251c6-167">Quando si crea nuovo database da [ripristino esistente database tooa temporizzato nel tempo](sql-database-recovery-using-backups.md), dispone di conservazione temporale disabilitato a livello di database hello.</span><span class="sxs-lookup"><span data-stu-id="251c6-167">When you create new database by [restoring existing database tooa specific point in time](sql-database-recovery-using-backups.md), it has temporal retention disabled at hello database level.</span></span> <span data-ttu-id="251c6-168">(**is_temporal_history_retention_enabled** tooOFF impostato flag).</span><span class="sxs-lookup"><span data-stu-id="251c6-168">(**is_temporal_history_retention_enabled** flag set tooOFF).</span></span> <span data-ttu-id="251c6-169">Questa funzionalità consente tutte le righe di cronologia al momento del ripristino, senza doversi righe obsoleti vengono rimossi prima di ottenere tooquery tooexamine li.</span><span class="sxs-lookup"><span data-stu-id="251c6-169">This functionality allows you tooexamine all historical rows upon restore, without worrying that aged rows are removed before you get tooquery them.</span></span> <span data-ttu-id="251c6-170">È possibile utilizzare anche*controllare i dati cronologici supera il periodo di memorizzazione configurato*.</span><span class="sxs-lookup"><span data-stu-id="251c6-170">You can use it too*inspect historical data beyond configured retention period*.</span></span>

<span data-ttu-id="251c6-171">Si supponga che per una tabella temporale sia specificato il periodo di conservazione MONTH.</span><span class="sxs-lookup"><span data-stu-id="251c6-171">Say that a temporal table has one MONTH retention period specified.</span></span> <span data-ttu-id="251c6-172">Se il database è stato creato nel livello di servizio Premium, sarà in grado di toocreate copia del database con stato del database hello dei giorni too35 in hello precedente.</span><span class="sxs-lookup"><span data-stu-id="251c6-172">If your database was created in Premium Service tier, you would be able toocreate database copy with hello database state up too35 days back in hello past.</span></span> <span data-ttu-id="251c6-173">Che in modo efficace consentirebbe righe di cronologia tooanalyze di backup too65 giorni eseguendo una query sulla tabella di cronologia hello direttamente.</span><span class="sxs-lookup"><span data-stu-id="251c6-173">That effectively would allow you tooanalyze historical rows that are up too65 days old by querying hello history table directly.</span></span>

<span data-ttu-id="251c6-174">Se si desidera la pulizia di memorizzazione temporale tooactivate, eseguire hello seguente istruzione Transact-SQL dopo il ripristino temporizzato:</span><span class="sxs-lookup"><span data-stu-id="251c6-174">If you want tooactivate temporal retention cleanup, run hello following Transact-SQL statement after point in time restore:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a><span data-ttu-id="251c6-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="251c6-175">Next steps</span></span>
<span data-ttu-id="251c6-176">come le tabelle temporali toouse nelle applicazioni, estrarre toolearn [Introduzione alle tabelle temporali nel Database SQL di Azure](sql-database-temporal-tables.md).</span><span class="sxs-lookup"><span data-stu-id="251c6-176">toolearn how toouse Temporal Tables in your applications, check out [Getting Started with Temporal Tables in Azure SQL Database](sql-database-temporal-tables.md).</span></span>

<span data-ttu-id="251c6-177">Visita Channel 9 toohear un [reale implementazione temporale storie di successo](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) ed espressioni di controllo un [live dimostrazione temporale](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="251c6-177">Visit Channel 9 toohear a [real customer temporal implementation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

<span data-ttu-id="251c6-178">Per informazioni dettagliate sulle tabelle temporali, esaminare la [documentazione su MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="251c6-178">For detailed information about Temporal Tables, review [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>

