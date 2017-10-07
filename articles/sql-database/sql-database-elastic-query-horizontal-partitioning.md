---
title: "aaaReporting tra i database di scalabilità orizzontale cloud | Documenti Microsoft"
description: come tooset elastico query su partizioni orizzontali
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="5ef5c-103">Creazione di report tra database cloud con scalabilità orizzontale (anteprima)</span><span class="sxs-lookup"><span data-stu-id="5ef5c-103">Reporting across scaled-out cloud databases (preview)</span></span>
![Eseguire una query tra partizioni][1]

<span data-ttu-id="5ef5c-105">I database partizionati distribuiscono righe su un livello di dati a scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="5ef5c-106">schema di Hello è identico in tutti i database partecipanti, noti anche come partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-106">hello schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="5ef5c-107">Con una query elastica è possibile creare report che si estendono a tutti i database di un database partizionato.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="5ef5c-108">Per l'avvio rapido, vedere [Creazione di report tra database cloud con scalabilità orizzontale](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="5ef5c-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="5ef5c-109">Per i database non partizionati, vedere [Eseguire query in database cloud con schemi diversi](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="5ef5c-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5ef5c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5ef5c-110">Prerequisites</span></span>
* <span data-ttu-id="5ef5c-111">Creare una mappa partizioni utilizzando hello libreria client di database elastico.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-111">Create a shard map using hello elastic database client library.</span></span> <span data-ttu-id="5ef5c-112">Vedere [Gestione mappe partizioni](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="5ef5c-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="5ef5c-113">Oppure usare app di esempio hello in [Introduzione agli strumenti di database elastico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5ef5c-113">Or use hello sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="5ef5c-114">In alternativa, vedere [esistenti di eseguire la migrazione di database database tooscaled-out](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="5ef5c-114">Alternatively, see [Migrate existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="5ef5c-115">utente Hello deve disporre dell'autorizzazione ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-115">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="5ef5c-116">Questa autorizzazione è inclusa con l'autorizzazione ALTER DATABASE hello.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-116">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="5ef5c-117">Le autorizzazioni ALTER ANY EXTERNAL DATA SOURCE sono necessari toorefer toohello origine dati sottostante.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="5ef5c-118">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5ef5c-118">Overview</span></span>
<span data-ttu-id="5ef5c-119">Queste istruzioni creano rappresentazione dei metadati hello del livello dati partizionati nel database di query elastico hello.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-119">These statements create hello metadata representation of your sharded data tier in hello elastic query database.</span></span> 

1. [<span data-ttu-id="5ef5c-120">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="5ef5c-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="5ef5c-121">CREATE DATABASE SCOPED CREDENTIAL</span><span class="sxs-lookup"><span data-stu-id="5ef5c-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="5ef5c-122">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="5ef5c-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="5ef5c-123">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="5ef5c-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="5ef5c-124">1.1 Creare la chiave master e le credenziali con ambito database</span><span class="sxs-lookup"><span data-stu-id="5ef5c-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="5ef5c-125">Hello credenziali vengono utilizzate dal database remoti tooyour tooconnect query elastico hello.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-125">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="5ef5c-126">Verificare che tale hello *"\<username\>"* non include alcun *"@servername"* suffisso.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-126">Make sure that hello *"\<username\>"* does not include any *"@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="5ef5c-127">1.2 Creare origini dati esterne</span><span class="sxs-lookup"><span data-stu-id="5ef5c-127">1.2 Create external data sources</span></span>
<span data-ttu-id="5ef5c-128">Sintassi:</span><span class="sxs-lookup"><span data-stu-id="5ef5c-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="5ef5c-129">Esempio</span><span class="sxs-lookup"><span data-stu-id="5ef5c-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="5ef5c-130">Recuperare l'elenco di hello delle origini dati esterne corrente:</span><span class="sxs-lookup"><span data-stu-id="5ef5c-130">Retrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="5ef5c-131">origine dati esterna Hello fa riferimento la mappa partizioni.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-131">hello external data source references your shard map.</span></span> <span data-ttu-id="5ef5c-132">Una query elastica utilizza quindi origine dati esterna hello e hello partizioni tooenumerate hello database delle mappe che fanno parte di livello dati hello sottostante.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-132">An elastic query then uses hello external data source and hello underlying shard map tooenumerate hello databases that participate in hello data tier.</span></span> <span data-ttu-id="5ef5c-133">stesse credenziali Hello sono mappa di partizioni utilizzate tooread hello e tooaccess hello dati su partizioni hello durante l'elaborazione di hello di una query elastica.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-133">hello same credentials are used tooread hello shard map and tooaccess hello data on hello shards during hello processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="5ef5c-134">1.3 Creare tabelle esterne</span><span class="sxs-lookup"><span data-stu-id="5ef5c-134">1.3 Create external tables</span></span>
<span data-ttu-id="5ef5c-135">Sintassi:</span><span class="sxs-lookup"><span data-stu-id="5ef5c-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="5ef5c-136">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="5ef5c-136">**Example**</span></span>

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

<span data-ttu-id="5ef5c-137">Recuperare l'elenco di hello delle tabelle esterne del database corrente hello:</span><span class="sxs-lookup"><span data-stu-id="5ef5c-137">Retrieve hello list of external tables from hello current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="5ef5c-138">tabelle esterne toodrop:</span><span class="sxs-lookup"><span data-stu-id="5ef5c-138">toodrop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="5ef5c-139">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="5ef5c-139">Remarks</span></span>
<span data-ttu-id="5ef5c-140">Hello dati\_clausola origine definisce l'origine dati esterna hello (una mappa partizioni) che viene utilizzato per la tabella esterna hello.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-140">hello DATA\_SOURCE clause defines hello external data source (a shard map) that is used for hello external table.</span></span>  

<span data-ttu-id="5ef5c-141">Hello SCHEMA\_nome e l'oggetto\_clausole nome mappa hello esterno definizione tooa tabella in uno schema diverso.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-141">hello SCHEMA\_NAME and OBJECT\_NAME clauses map hello external table definition tooa table in a different schema.</span></span> <span data-ttu-id="5ef5c-142">Se omesso, schema hello dell'oggetto remoto hello si presuppone che toobe "dbo" e il nome è nome della tabella esterna identici toohello toobe da definire.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-142">If omitted, hello schema of hello remote object is assumed toobe “dbo” and its name is assumed toobe identical toohello external table name being defined.</span></span> <span data-ttu-id="5ef5c-143">Ciò è utile se hello nome della tabella remota è già in uso nel database di hello in cui si desidera toocreate tabella esterna di hello.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-143">This is useful if hello name of your remote table is already taken in hello database where you want toocreate hello external table.</span></span> <span data-ttu-id="5ef5c-144">Ad esempio, si desidera toodefine un tooget tabella esterna, una vista aggregata di viste del catalogo o del livello DMV sui dati di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-144">For  example, you want toodefine an external table tooget an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="5ef5c-145">Poiché le viste del catalogo e DMV già esiste in locale, è possibile utilizzare i nomi per la definizione di tabella esterna hello.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-145">Since catalog views and DMVs already exist locally, you cannot use their names for hello external table definition.</span></span> <span data-ttu-id="5ef5c-146">In alternativa, utilizzare un nome diverso e utilizzare della vista del catalogo hello o hello Nome DMV in hello SCHEMA\_nome e/o oggetto\_clausole di nome.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-146">Instead, use a different name and use hello catalog view’s or hello DMV’s name in hello SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="5ef5c-147">(Vedere l'esempio hello riportato di seguito).</span><span class="sxs-lookup"><span data-stu-id="5ef5c-147">(See hello example below.)</span></span> 

<span data-ttu-id="5ef5c-148">clausola distribuzione Hello specifica distribuzione dei dati hello utilizzata per questa tabella.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-148">hello DISTRIBUTION clause specifies hello data distribution used for this table.</span></span> <span data-ttu-id="5ef5c-149">query processor di Hello utilizza informazioni hello disponibili in hello distribuzione clausola toobuild hello più efficace i piani di query.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-149">hello query processor utilizes hello information provided in hello DISTRIBUTION clause toobuild hello most efficient query plans.</span></span>  

1. <span data-ttu-id="5ef5c-150">**PARTIZIONATO** significa dati partizionati orizzontalmente tra database hello.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-150">**SHARDED** means data is horizontally partitioned across hello databases.</span></span> <span data-ttu-id="5ef5c-151">chiave di partizionamento per la distribuzione dei dati hello è hello Hello **< sharding_column_name >** parametro.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-151">hello partitioning key for hello data distribution is hello **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="5ef5c-152">**REPLICATI** significa che copie identiche di tabella hello siano presenti in ogni database.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-152">**REPLICATED** means that identical copies of hello table are present on each database.</span></span> <span data-ttu-id="5ef5c-153">È il tooensure responsabilità che le repliche hello siano identiche tra database hello.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-153">It is your responsibility tooensure that hello replicas are identical across hello databases.</span></span>
3. <span data-ttu-id="5ef5c-154">**ARROTONDAMENTO\_ROBIN** significa che la tabella hello è partizionata orizzontalmente utilizzando un metodo di distribuzione dipendenti dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-154">**ROUND\_ROBIN** means that hello table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="5ef5c-155">**Riferimento di livello dati**: tabella esterna hello DDL fa riferimento l'origine dati esterna tooan.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-155">**Data tier reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="5ef5c-156">origine dati esterna Hello specifica una mappa partizioni che fornisce la tabella esterna hello con hello informazioni necessarie toolocate tutti i database di hello nel livello dati.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-156">hello external data source specifies a shard map which provides hello external table with hello information necessary toolocate all hello databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="5ef5c-157">Considerazioni relative alla sicurezza</span><span class="sxs-lookup"><span data-stu-id="5ef5c-157">Security considerations</span></span>
<span data-ttu-id="5ef5c-158">Gli utenti con una tabella esterna toohello di accesso accedere automaticamente toohello tabelle remote sottostanti in credenziali hello specificata nella definizione dell'origine dati esterna hello.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-158">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="5ef5c-159">Evitare indesiderati l'elevazione dei privilegi tramite credenziali hello dell'origine dati esterna hello.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-159">Avoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="5ef5c-160">Usare GRANT o REVOKE per la tabella esterna, come se fosse una tabella comune.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="5ef5c-161">Dopo aver definito l'origine dati esterna e le tabelle esterne, è ora possibile usare la sintassi T-SQL completa sulle tabelle esterne.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="5ef5c-162">Esempio: esecuzione di query su database partizionati orizzontalmente</span><span class="sxs-lookup"><span data-stu-id="5ef5c-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="5ef5c-163">Hello nella query seguente esegue un join a tre vie tra magazzini, ordini e le righe dell'ordine e utilizza più funzioni di aggregazione e un filtro selettivo.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-163">hello following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="5ef5c-164">Si presuppone (1) partizionamento (partizionamento orizzontale) e (2) che data warehouse, ordini e le righe di ordine sono partizionate dalla colonna di id warehouse hello e query elastico hello può condividere il percorso dei join hello su partizioni hello ed elaborare hello costosa parte query hello su hello partizioni in parallelo.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by hello warehouse id column, and that hello elastic query can co-locate hello joins on hello shards and process hello expensive part of hello query on hello shards in parallel.</span></span> 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="5ef5c-165">Stored procedure per l'esecuzione remota di T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="5ef5c-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="5ef5c-166">Query elastico introduce inoltre una stored procedure che fornisce accesso diretto toohello partizioni.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-166">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="5ef5c-167">Hello stored procedure viene chiamata [sp\_eseguire \_remoto](https://msdn.microsoft.com/library/mt703714) e può essere utilizzato tooexecute stored procedure remote o il codice T-SQL nel database remoto hello.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-167">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="5ef5c-168">Avrà hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="5ef5c-168">It takes hello following parameters:</span></span> 

* <span data-ttu-id="5ef5c-169">Nome dell'origine dati (nvarchar): nome hello dell'origine dati esterna hello di tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-169">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="5ef5c-170">Query (nvarchar): toobe query hello T-SQL eseguito su ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-170">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="5ef5c-171">Dichiarazione di parametro (nvarchar) - facoltativa: stringa con definizioni dei tipi di dati per i parametri di hello utilizzati nel parametro di Query hello (ad esempio sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="5ef5c-171">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="5ef5c-172">Elenco di valori dei parametri (facoltativo): elenco delimitato da virgole di valori dei parametri, ad esempio sp_executesql.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="5ef5c-173">sp Hello\_eseguire\_remoto utilizza hello origine dati esterna cui hello chiamata parametri tooexecute hello dato istruzione T-SQL nel database remoto hello.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-173">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="5ef5c-174">Usa credenziali hello del database di gestione di hello dati esterni origine tooconnect toohello shardmap e database remoti hello.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-174">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="5ef5c-175">Esempio:</span><span class="sxs-lookup"><span data-stu-id="5ef5c-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="5ef5c-176">Connettività per gli strumenti</span><span class="sxs-lookup"><span data-stu-id="5ef5c-176">Connectivity for tools</span></span>
<span data-ttu-id="5ef5c-177">Regolare tooconnect di stringhe di connessione SQL Server utilizzare l'applicazione, BI e dati integrazione strumenti toohello database con le definizioni di tabella esterna.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-177">Use regular SQL Server connection strings tooconnect your application, your BI and data integration tools toohello database with your external table definitions.</span></span> <span data-ttu-id="5ef5c-178">Assicurarsi che SQL Server sia supportato come origine dati per lo strumento.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="5ef5c-179">Fare riferimento a database elastico query hello come qualsiasi altro strumento di toohello database connessi a SQL Server e usare tabelle esterne da strumento o l'applicazione come se fossero tabelle locali.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-179">Then reference hello elastic query database like any other SQL Server database connected toohello tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="5ef5c-180">Procedure consigliate</span><span class="sxs-lookup"><span data-stu-id="5ef5c-180">Best practices</span></span>
* <span data-ttu-id="5ef5c-181">Assicurarsi di che database elastico query endpoint hello ha toohello shardmap database e tutte le partizioni tramite hello che firewall di database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-181">Ensure that hello elastic query endpoint database has been given access toohello shardmap database and all shards through hello SQL DB firewalls.</span></span>  
* <span data-ttu-id="5ef5c-182">Convalidare o applicare la distribuzione dei dati hello definita tabella esterna hello.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-182">Validate or enforce hello data distribution defined by hello external table.</span></span> <span data-ttu-id="5ef5c-183">Se la distribuzione di dati effettivo è diversa dalla distribuzione hello specificata nella definizione di tabella, le query possono restituire risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-183">If your actual data distribution is different from hello distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="5ef5c-184">Query elastico attualmente non esegue l'eliminazione di partizioni quando predicati sulla chiave di partizionamento orizzontale hello consentirne toosafely escludere determinate partizioni dall'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-184">Elastic query currently does not perform shard elimination when predicates over hello sharding key would allow it toosafely exclude certain shards from processing.</span></span>
* <span data-ttu-id="5ef5c-185">Query elastico è ideale per le query in cui la maggior parte del calcolo hello può essere eseguita su partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-185">Elastic query works best for queries where most of hello computation can be done on hello shards.</span></span> <span data-ttu-id="5ef5c-186">In genere si ottiene hello migliori prestazioni di query con predicati del filtro selettivo che può essere valutata in partizioni hello o join su hello chiavi che possono essere eseguite in modo allineate alle partizioni in tutte le partizioni di partizionamento.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-186">You typically get hello best query performance with selective filter predicates that can be evaluated on hello shards or joins over hello partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="5ef5c-187">Altri modelli di query, potrebbe essere necessario grandi quantità di tooload dei dati dal nodo head di hello partizioni toohello e potrebbero essere scarse</span><span class="sxs-lookup"><span data-stu-id="5ef5c-187">Other query patterns may need tooload large amounts of data from hello shards toohello head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ef5c-188">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5ef5c-188">Next steps</span></span>

* <span data-ttu-id="5ef5c-189">Per un approfondimento, vedere [Panoramica delle query elastiche](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ef5c-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="5ef5c-190">Per un'esercitazione sul partizionamento verticale, vedere [Introduzione alle query tra database (partizionamento verticale)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="5ef5c-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="5ef5c-191">Per le query di esempio e sintassi per i dati con partizionamento verticale, vedere [Eseguire query su dati con partizionamento verticale](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="5ef5c-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="5ef5c-192">Per un'esercitazione sul partizionamento orizzontale, vedere la [guida introduttiva alle query elastiche per il partizionamento orizzontale](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="5ef5c-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="5ef5c-193">Vedere [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) per una stored procedure che esegue un'istruzione Transact-SQL su un singolo database SQL di Azure remoto o un set di database che fungono da partizioni in uno schema di partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="5ef5c-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
