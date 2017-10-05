---
title: "Creazione di report tra database cloud con scalabilità orizzontale | Documentazione Microsoft"
description: Come configurare query elastiche sui partizionamenti orizzontali
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
ms.openlocfilehash: 62b5bcd26aa1ed219fb38970916e0e8847ceb577
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="15c7c-103">Creazione di report tra database cloud con scalabilità orizzontale (anteprima)</span><span class="sxs-lookup"><span data-stu-id="15c7c-103">Reporting across scaled-out cloud databases (preview)</span></span>
![Eseguire una query tra partizioni][1]

<span data-ttu-id="15c7c-105">I database partizionati distribuiscono righe su un livello di dati a scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="15c7c-105">Sharded databases distribute rows across a scaled out data tier.</span></span> <span data-ttu-id="15c7c-106">Lo schema è identico in tutti i database partecipanti, ed è denominato anche partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="15c7c-106">The schema is identical on all participating databases, also known as horizontal partitioning.</span></span> <span data-ttu-id="15c7c-107">Con una query elastica è possibile creare report che si estendono a tutti i database di un database partizionato.</span><span class="sxs-lookup"><span data-stu-id="15c7c-107">Using an elastic query, you can create reports that span all databases in a sharded database.</span></span>

<span data-ttu-id="15c7c-108">Per l'avvio rapido, vedere [Creazione di report tra database cloud con scalabilità orizzontale](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="15c7c-108">For a quick start, see [Reporting across scaled-out cloud databases](sql-database-elastic-query-getting-started.md).</span></span>

<span data-ttu-id="15c7c-109">Per i database non partizionati, vedere [Eseguire query in database cloud con schemi diversi](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="15c7c-109">For non-sharded databases, see [Query across cloud databases with different schemas](sql-database-elastic-query-vertical-partitioning.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="15c7c-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="15c7c-110">Prerequisites</span></span>
* <span data-ttu-id="15c7c-111">Creare una mappa partizioni usando la libreria client dei database elastici.</span><span class="sxs-lookup"><span data-stu-id="15c7c-111">Create a shard map using the elastic database client library.</span></span> <span data-ttu-id="15c7c-112">Vedere [Gestione mappe partizioni](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="15c7c-112">see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="15c7c-113">In alternativa, usare l'app di esempio in [Introduzione agli strumenti del database elastico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="15c7c-113">Or use the sample app in [Get started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="15c7c-114">In alternativa, vedere [Migrate existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md)(Eseguire la migrazione di database esistenti per la scalabilità orizzontale).</span><span class="sxs-lookup"><span data-stu-id="15c7c-114">Alternatively, see [Migrate existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>
* <span data-ttu-id="15c7c-115">L'utente deve disporre dell'autorizzazione ALTER ANY origine dei dati esterni.</span><span class="sxs-lookup"><span data-stu-id="15c7c-115">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="15c7c-116">Questa autorizzazione è inclusa nell'autorizzazione ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="15c7c-116">This permission is included with the ALTER DATABASE permission.</span></span>
* <span data-ttu-id="15c7c-117">Per il riferimento all'origine dati sottostante sono necessarie autorizzazioni ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="15c7c-117">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="15c7c-118">Panoramica</span><span class="sxs-lookup"><span data-stu-id="15c7c-118">Overview</span></span>
<span data-ttu-id="15c7c-119">Queste istruzioni creano la rappresentazione dei metadati del livello dati con partizionamento orizzontale nel database elastico sottoposto a query.</span><span class="sxs-lookup"><span data-stu-id="15c7c-119">These statements create the metadata representation of your sharded data tier in the elastic query database.</span></span> 

1. [<span data-ttu-id="15c7c-120">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="15c7c-120">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="15c7c-121">CREATE DATABASE SCOPED CREDENTIAL</span><span class="sxs-lookup"><span data-stu-id="15c7c-121">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="15c7c-122">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="15c7c-122">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="15c7c-123">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="15c7c-123">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="15c7c-124">1.1 Creare la chiave master e le credenziali con ambito database</span><span class="sxs-lookup"><span data-stu-id="15c7c-124">1.1 Create database scoped master key and credentials</span></span>
<span data-ttu-id="15c7c-125">Le credenziali vengono usate dalla query elastica per connettersi ai database remoti.</span><span class="sxs-lookup"><span data-stu-id="15c7c-125">The credential is used by the elastic query to connect to your remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="15c7c-126">Assicurarsi che il *"\<nome utente\>"* non includa alcun suffisso *"@servername"*.</span><span class="sxs-lookup"><span data-stu-id="15c7c-126">Make sure that the *"\<username\>"* does not include any *"@servername"* suffix.</span></span> 
> 
> 

## <a name="12-create-external-data-sources"></a><span data-ttu-id="15c7c-127">1.2 Creare origini dati esterne</span><span class="sxs-lookup"><span data-stu-id="15c7c-127">1.2 Create external data sources</span></span>
<span data-ttu-id="15c7c-128">Sintassi:</span><span class="sxs-lookup"><span data-stu-id="15c7c-128">Syntax:</span></span>

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a><span data-ttu-id="15c7c-129">Esempio</span><span class="sxs-lookup"><span data-stu-id="15c7c-129">Example</span></span>
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

<span data-ttu-id="15c7c-130">Recuperare l'elenco di origini dati esterne correnti:</span><span class="sxs-lookup"><span data-stu-id="15c7c-130">Retrieve the list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

<span data-ttu-id="15c7c-131">L'origine dati esterna fa riferimento alla mappa partizioni.</span><span class="sxs-lookup"><span data-stu-id="15c7c-131">The external data source references your shard map.</span></span> <span data-ttu-id="15c7c-132">Una query elastica usa quindi l'origine dati esterna e la mappa partizioni sottostante per enumerare i database che partecipano al livello dati.</span><span class="sxs-lookup"><span data-stu-id="15c7c-132">An elastic query then uses the external data source and the underlying shard map to enumerate the databases that participate in the data tier.</span></span> <span data-ttu-id="15c7c-133">Le stesse credenziali vengono usate per leggere la mappa partizioni e per accedere ai dati nelle partizioni durante l'elaborazione di una query elastica.</span><span class="sxs-lookup"><span data-stu-id="15c7c-133">The same credentials are used to read the shard map and to access the data on the shards during the processing of an elastic query.</span></span> 

## <a name="13-create-external-tables"></a><span data-ttu-id="15c7c-134">1.3 Creare tabelle esterne</span><span class="sxs-lookup"><span data-stu-id="15c7c-134">1.3 Create external tables</span></span>
<span data-ttu-id="15c7c-135">Sintassi:</span><span class="sxs-lookup"><span data-stu-id="15c7c-135">Syntax:</span></span>  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

<span data-ttu-id="15c7c-136">**Esempio**</span><span class="sxs-lookup"><span data-stu-id="15c7c-136">**Example**</span></span>

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

<span data-ttu-id="15c7c-137">Recuperare l'elenco di tabelle esterne dal database corrente:</span><span class="sxs-lookup"><span data-stu-id="15c7c-137">Retrieve the list of external tables from the current database:</span></span> 

    SELECT * from sys.external_tables; 

<span data-ttu-id="15c7c-138">Per eliminare le tabelle esterne:</span><span class="sxs-lookup"><span data-stu-id="15c7c-138">To drop external tables:</span></span>

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a><span data-ttu-id="15c7c-139">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="15c7c-139">Remarks</span></span>
<span data-ttu-id="15c7c-140">La clausola \_DATA_SOURCE definisce l'origine dati esterna (una mappa partizioni) usata per la tabella esterna.</span><span class="sxs-lookup"><span data-stu-id="15c7c-140">The DATA\_SOURCE clause defines the external data source (a shard map) that is used for the external table.</span></span>  

<span data-ttu-id="15c7c-141">Le clausole SCHEMA\_NAME e OBJECT\_NAME eseguono il mapping della definizione della tabella esterna a una tabella in uno schema diverso.</span><span class="sxs-lookup"><span data-stu-id="15c7c-141">The SCHEMA\_NAME and OBJECT\_NAME clauses map the external table definition to a table in a different schema.</span></span> <span data-ttu-id="15c7c-142">Se queste clausole vengono omesse, si presupporrà che lo schema dell'oggetto remoto sia "dbo" e che il relativo nome sia identico al nome della tabella esterna in fase di definizione.</span><span class="sxs-lookup"><span data-stu-id="15c7c-142">If omitted, the schema of the remote object is assumed to be “dbo” and its name is assumed to be identical to the external table name being defined.</span></span> <span data-ttu-id="15c7c-143">Questo è utile se il nome della tabella remota è già in uso nel database in cui si vuole creare la tabella esterna.</span><span class="sxs-lookup"><span data-stu-id="15c7c-143">This is useful if the name of your remote table is already taken in the database where you want to create the external table.</span></span> <span data-ttu-id="15c7c-144">Ad esempio, si vuole definire una tabella esterna per ottenere una visualizzazione aggregata delle viste del catalogo o delle viste a gestione dinamica (DMV) nel livello dati con scalabilità orizzontale.</span><span class="sxs-lookup"><span data-stu-id="15c7c-144">For  example, you want to define an external table to get an aggregate view of catalog views or DMVs on your scaled out data tier.</span></span> <span data-ttu-id="15c7c-145">Poiché le viste del catalogo e le DMV esistono già localmente, non sarà possibile usare i rispettivi nomi per la definizione della tabella esterna.</span><span class="sxs-lookup"><span data-stu-id="15c7c-145">Since catalog views and DMVs already exist locally, you cannot use their names for the external table definition.</span></span> <span data-ttu-id="15c7c-146">Usare invece un nome diverso e usare il nome della vista del catalogo o della DMV nelle clausole SCHEMA\_NAME e/o OBJECT\_NAME.</span><span class="sxs-lookup"><span data-stu-id="15c7c-146">Instead, use a different name and use the catalog view’s or the DMV’s name in the SCHEMA\_NAME and/or OBJECT\_NAME clauses.</span></span> <span data-ttu-id="15c7c-147">Vedere l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="15c7c-147">(See the example below.)</span></span> 

<span data-ttu-id="15c7c-148">La clausola DISTRIBUTION specifica la distribuzione dei dati usata per questa tabella.</span><span class="sxs-lookup"><span data-stu-id="15c7c-148">The DISTRIBUTION clause specifies the data distribution used for this table.</span></span> <span data-ttu-id="15c7c-149">Query Processor utilizza le informazioni fornite nella clausola DISTRIBUTION per generare i piani di query più efficienti.</span><span class="sxs-lookup"><span data-stu-id="15c7c-149">The query processor utilizes the information provided in the DISTRIBUTION clause to build the most efficient query plans.</span></span>  

1. <span data-ttu-id="15c7c-150">**SHARDED** significa che i dati sono partizionati orizzontalmente tra i database.</span><span class="sxs-lookup"><span data-stu-id="15c7c-150">**SHARDED** means data is horizontally partitioned across the databases.</span></span> <span data-ttu-id="15c7c-151">La chiave di partizionamento per la distribuzione dei dati è il parametro **<sharding_column_name>**.</span><span class="sxs-lookup"><span data-stu-id="15c7c-151">The partitioning key for the data distribution is the **<sharding_column_name>** parameter.</span></span>
2. <span data-ttu-id="15c7c-152">**REPLICATED** indica che in ogni database sono presenti copie identiche della tabella.</span><span class="sxs-lookup"><span data-stu-id="15c7c-152">**REPLICATED** means that identical copies of the table are present on each database.</span></span> <span data-ttu-id="15c7c-153">Sarà quindi necessario assicurarsi che le repliche siano identiche in tutti i database.</span><span class="sxs-lookup"><span data-stu-id="15c7c-153">It is your responsibility to ensure that the replicas are identical across the databases.</span></span>
3. <span data-ttu-id="15c7c-154">**ROUND\_ROBIN** significa che la tabella è partizionata orizzontalmente con un metodo di distribuzione dipendente dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="15c7c-154">**ROUND\_ROBIN** means that the table is horizontally partitioned using an application-dependent distribution method.</span></span> 

<span data-ttu-id="15c7c-155">**Riferimento al livello dati**: il DDL della tabella esterna fa riferimento a un'origine dati esterna.</span><span class="sxs-lookup"><span data-stu-id="15c7c-155">**Data tier reference**: The external table DDL refers to an external data source.</span></span> <span data-ttu-id="15c7c-156">L'origine dati esterna specifica una mappa partizioni che fornisce alla tabella esterna le informazioni necessarie per individuare tutti i database nel livello dati.</span><span class="sxs-lookup"><span data-stu-id="15c7c-156">The external data source specifies a shard map which provides the external table with the information necessary to locate all the databases in your data tier.</span></span> 

### <a name="security-considerations"></a><span data-ttu-id="15c7c-157">Considerazioni relative alla sicurezza</span><span class="sxs-lookup"><span data-stu-id="15c7c-157">Security considerations</span></span>
<span data-ttu-id="15c7c-158">Gli utenti con accesso alla tabella esterna ottengono automaticamente l'accesso alle tabelle remote sottostanti con le credenziali specificate nella definizione dell'origine dati esterna.</span><span class="sxs-lookup"><span data-stu-id="15c7c-158">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span></span> <span data-ttu-id="15c7c-159">Evitare l'elevazione dei privilegi indesiderata mediante le credenziali dell'origine dati esterna.</span><span class="sxs-lookup"><span data-stu-id="15c7c-159">Avoid undesired elevation of privileges through the credential of the external data source.</span></span> <span data-ttu-id="15c7c-160">Usare GRANT o REVOKE per la tabella esterna, come se fosse una tabella comune.</span><span class="sxs-lookup"><span data-stu-id="15c7c-160">Use GRANT or REVOKE for an external table just as though it were a regular table.</span></span>  

<span data-ttu-id="15c7c-161">Dopo aver definito l'origine dati esterna e le tabelle esterne, è ora possibile usare la sintassi T-SQL completa sulle tabelle esterne.</span><span class="sxs-lookup"><span data-stu-id="15c7c-161">Once you have defined your external data source and your external tables, you can now use full T-SQL over your external tables.</span></span>

## <a name="example-querying-horizontal-partitioned-databases"></a><span data-ttu-id="15c7c-162">Esempio: esecuzione di query su database partizionati orizzontalmente</span><span class="sxs-lookup"><span data-stu-id="15c7c-162">Example: querying horizontal partitioned databases</span></span>
<span data-ttu-id="15c7c-163">La query seguente esegue un join a tre vie tra magazzini, ordini e righe di ordine e usa diverse funzioni di aggregazione e un filtro selettivo.</span><span class="sxs-lookup"><span data-stu-id="15c7c-163">The following query performs a three-way join between warehouses, orders and order lines and uses several aggregates and a selective filter.</span></span> <span data-ttu-id="15c7c-164">Presuppone che (1) venga usato il partizionamento orizzontale, che (2) i magazzini, gli ordini e le righe di ordine siano partizionati orizzontalmente in base alla colonna warehouse id e che la query elastica possa condividere i join sulle partizioni ed elaborare la parte più onerosa della query sulle partizioni in parallelo.</span><span class="sxs-lookup"><span data-stu-id="15c7c-164">It assumes (1) horizontal partitioning (sharding) and (2) that warehouses, orders and order lines are sharded by the warehouse id column, and that the elastic query can co-locate the joins on the shards and process the expensive part of the query on the shards in parallel.</span></span> 

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

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="15c7c-165">Stored procedure per l'esecuzione remota di T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="15c7c-165">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="15c7c-166">La query elastica introduce anche una stored procedure che fornisce l'accesso diretto alle partizioni.</span><span class="sxs-lookup"><span data-stu-id="15c7c-166">Elastic query also introduces a stored procedure that provides direct access to the shards.</span></span> <span data-ttu-id="15c7c-167">La stored procedure è denominata [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) e può essere usata per eseguire stored procedure remote o codice T-SQL sui database remoti.</span><span class="sxs-lookup"><span data-stu-id="15c7c-167">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote databases.</span></span> <span data-ttu-id="15c7c-168">È necessario specificare i seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="15c7c-168">It takes the following parameters:</span></span> 

* <span data-ttu-id="15c7c-169">Nome dell'origine dati (nvarchar): il nome dell'origine dati esterna di tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="15c7c-169">Data source name (nvarchar): The name of the external data source of type RDBMS.</span></span> 
* <span data-ttu-id="15c7c-170">Query (nvarchar): la query T-SQL da eseguire in ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="15c7c-170">Query (nvarchar): The T-SQL query to be executed on each shard.</span></span> 
* <span data-ttu-id="15c7c-171">Dichiarazione del parametro (nvarchar) - Facoltativo: stringa con definizioni del tipo di dati per i parametri usati nel parametro della query, ad esempio sp_executesql.</span><span class="sxs-lookup"><span data-stu-id="15c7c-171">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="15c7c-172">Elenco di valori dei parametri (facoltativo): elenco delimitato da virgole di valori dei parametri, ad esempio sp_executesql.</span><span class="sxs-lookup"><span data-stu-id="15c7c-172">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="15c7c-173">La stored procedure sp\_execute\_remote usa l'origine dati esterna specificata nei parametri di chiamata per eseguire l'istruzione T-SQL inclusa nei database remoti.</span><span class="sxs-lookup"><span data-stu-id="15c7c-173">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote databases.</span></span> <span data-ttu-id="15c7c-174">Usa le credenziali dell'origine dati esterna per connettersi al database di gestione shardmap e ai database remoti.</span><span class="sxs-lookup"><span data-stu-id="15c7c-174">It uses the credential of the external data source to connect to the shardmap manager database and the remote databases.</span></span>  

<span data-ttu-id="15c7c-175">Esempio:</span><span class="sxs-lookup"><span data-stu-id="15c7c-175">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a><span data-ttu-id="15c7c-176">Connettività per gli strumenti</span><span class="sxs-lookup"><span data-stu-id="15c7c-176">Connectivity for tools</span></span>
<span data-ttu-id="15c7c-177">Usare le normali stringhe di connessione di SQL Server per connettere l'applicazione, gli strumenti di Business Intelligence e di integrazione dei dati al database con le definizioni delle tabelle esterne.</span><span class="sxs-lookup"><span data-stu-id="15c7c-177">Use regular SQL Server connection strings to connect your application, your BI and data integration tools to the database with your external table definitions.</span></span> <span data-ttu-id="15c7c-178">Assicurarsi che SQL Server sia supportato come origine dati per lo strumento.</span><span class="sxs-lookup"><span data-stu-id="15c7c-178">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="15c7c-179">Fare quindi riferimento al database elastico sottoposto a query in modo analogo a qualsiasi altro database di SQL Server connesso allo strumento e usare le tabelle esterne dallo strumento o dall'applicazione come se fossero tabelle locali.</span><span class="sxs-lookup"><span data-stu-id="15c7c-179">Then reference the elastic query database like any other SQL Server database connected to the tool, and use external tables from your tool or application as if they were local tables.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="15c7c-180">Procedure consigliate</span><span class="sxs-lookup"><span data-stu-id="15c7c-180">Best practices</span></span>
* <span data-ttu-id="15c7c-181">Assicurarsi che il database di endpoint della query elastica abbia l'accesso al database di mappe partizioni e a tutte le partizioni attraverso i firewall del database SQL.</span><span class="sxs-lookup"><span data-stu-id="15c7c-181">Ensure that the elastic query endpoint database has been given access to the shardmap database and all shards through the SQL DB firewalls.</span></span>  
* <span data-ttu-id="15c7c-182">Convalidare o imporre la distribuzione di dati definita dalla tabella esterna.</span><span class="sxs-lookup"><span data-stu-id="15c7c-182">Validate or enforce the data distribution defined by the external table.</span></span> <span data-ttu-id="15c7c-183">Se la distribuzione di dati effettivo è diversa dalla distribuzione specificata nella definizione di tabella, le query possono restituire risultati imprevisti.</span><span class="sxs-lookup"><span data-stu-id="15c7c-183">If your actual data distribution is different from the distribution specified in your table definition, your queries may yield unexpected results.</span></span> 
* <span data-ttu-id="15c7c-184">La query elastica non esegue attualmente l'eliminazione di partizioni quando i predicati sulla chiave di partizionamento consentono l'esclusione sicura di alcune partizioni dall'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="15c7c-184">Elastic query currently does not perform shard elimination when predicates over the sharding key would allow it to safely exclude certain shards from processing.</span></span>
* <span data-ttu-id="15c7c-185">La query elastica funziona in modo ottimale per le query in cui la maggior parte dei calcoli può essere eseguita sulle partizioni.</span><span class="sxs-lookup"><span data-stu-id="15c7c-185">Elastic query works best for queries where most of the computation can be done on the shards.</span></span> <span data-ttu-id="15c7c-186">In genere si ottiene le migliori prestazioni di query con predicati del filtro selettivo che può essere valutata in join le partizioni tramite le chiavi di partizionamento che possono essere eseguite in modo su tutte le partizioni allineate alle partizioni.</span><span class="sxs-lookup"><span data-stu-id="15c7c-186">You typically get the best query performance with selective filter predicates that can be evaluated on the shards or joins over the partitioning keys that can be performed in a partition-aligned way on all shards.</span></span> <span data-ttu-id="15c7c-187">Altri modelli di query potrebbero richiedere il caricamento di quantità elevate di dati dalle partizioni al nodo head e potrebbero offrire prestazioni ridotte.</span><span class="sxs-lookup"><span data-stu-id="15c7c-187">Other query patterns may need to load large amounts of data from the shards to the head node and may perform poorly</span></span>

## <a name="next-steps"></a><span data-ttu-id="15c7c-188">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="15c7c-188">Next steps</span></span>

* <span data-ttu-id="15c7c-189">Per un approfondimento, vedere [Panoramica delle query elastiche](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="15c7c-189">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="15c7c-190">Per un'esercitazione sul partizionamento verticale, vedere [Introduzione alle query tra database (partizionamento verticale)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="15c7c-190">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="15c7c-191">Per le query di esempio e sintassi per i dati con partizionamento verticale, vedere [Eseguire query su dati con partizionamento verticale](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="15c7c-191">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="15c7c-192">Per un'esercitazione sul partizionamento orizzontale, vedere la [guida introduttiva alle query elastiche per il partizionamento orizzontale](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="15c7c-192">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="15c7c-193">Vedere [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) per una stored procedure che esegue un'istruzione Transact-SQL su un singolo database SQL di Azure remoto o un set di database che fungono da partizioni in uno schema di partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="15c7c-193">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
