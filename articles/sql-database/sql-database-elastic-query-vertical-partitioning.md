---
title: Eseguire query in database cloud con schemi diversi | Documentazione Microsoft
description: Informazioni su come configurare le query tra database su partizioni verticali.
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 84c261f2-9edc-42f4-988c-cf2f251f5eff
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: e9036f92f6c76e8c4738ee981efa8a7b9791dcc7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="4bb60-103">Eseguire query in database cloud con schemi diversi (anteprima)</span><span class="sxs-lookup"><span data-stu-id="4bb60-103">Query across cloud databases with different schemas (preview)</span></span>
![Eseguire una query tra tabelle in vari database][1]

<span data-ttu-id="4bb60-105">I database con partizionamento verticale usano set di tabelle diversi su database diversi.</span><span class="sxs-lookup"><span data-stu-id="4bb60-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="4bb60-106">Lo schema risulta quindi diverso nei diversi database.</span><span class="sxs-lookup"><span data-stu-id="4bb60-106">That means that the schema is different on different databases.</span></span> <span data-ttu-id="4bb60-107">Ad esempio, tutte le tabelle per l'inventario si trovano in un database, mentre le tabelle correlate alla contabilità si trovano in un altro database.</span><span class="sxs-lookup"><span data-stu-id="4bb60-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4bb60-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4bb60-108">Prerequisites</span></span>
* <span data-ttu-id="4bb60-109">L'utente deve disporre dell'autorizzazione ALTER ANY origine dei dati esterni.</span><span class="sxs-lookup"><span data-stu-id="4bb60-109">The user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="4bb60-110">Questa autorizzazione è inclusa nell'autorizzazione ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="4bb60-110">This permission is included with the ALTER DATABASE permission.</span></span>
* <span data-ttu-id="4bb60-111">Per il riferimento all'origine dati sottostante sono necessarie autorizzazioni ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="4bb60-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="4bb60-112">Panoramica</span><span class="sxs-lookup"><span data-stu-id="4bb60-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="4bb60-113">A differenza del partizionamento orizzontale, queste istruzioni DDL non dipendono dalla definizione di un livello dati con una mappa partizioni tramite la libreria client del database elastico.</span><span class="sxs-lookup"><span data-stu-id="4bb60-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through the elastic database client library.</span></span>
>

1. [<span data-ttu-id="4bb60-114">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="4bb60-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="4bb60-115">CREATE DATABASE SCOPED CREDENTIAL</span><span class="sxs-lookup"><span data-stu-id="4bb60-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="4bb60-116">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="4bb60-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="4bb60-117">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="4bb60-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="4bb60-118">Creare la chiave master e le credenziali con ambito database</span><span class="sxs-lookup"><span data-stu-id="4bb60-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="4bb60-119">Le credenziali vengono usate dalla query elastica per connettersi ai database remoti.</span><span class="sxs-lookup"><span data-stu-id="4bb60-119">The credential is used by the elastic query to connect to your remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="4bb60-120">Assicurarsi che `<username>` non includa alcun suffisso **"@servername"**.</span><span class="sxs-lookup"><span data-stu-id="4bb60-120">Ensure that the `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="4bb60-121">Creare origini dati esterne</span><span class="sxs-lookup"><span data-stu-id="4bb60-121">Create external data sources</span></span>
<span data-ttu-id="4bb60-122">Sintassi:</span><span class="sxs-lookup"><span data-stu-id="4bb60-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="4bb60-123">Il parametro TYPE deve essere impostato su **RDBMS**.</span><span class="sxs-lookup"><span data-stu-id="4bb60-123">The TYPE parameter must be set to **RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="4bb60-124">Esempio</span><span class="sxs-lookup"><span data-stu-id="4bb60-124">Example</span></span>
<span data-ttu-id="4bb60-125">Nell'esempio seguente viene illustrato l'utilizzo dell'istruzione CREATE per origini dati esterne.</span><span class="sxs-lookup"><span data-stu-id="4bb60-125">The following example illustrates the use of the CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="4bb60-126">Per recuperare l'elenco di origini dati esterne correnti:</span><span class="sxs-lookup"><span data-stu-id="4bb60-126">To retrieve the list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="4bb60-127">Tabelle esterne</span><span class="sxs-lookup"><span data-stu-id="4bb60-127">External Tables</span></span>
<span data-ttu-id="4bb60-128">Sintassi:</span><span class="sxs-lookup"><span data-stu-id="4bb60-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="4bb60-129">Esempio</span><span class="sxs-lookup"><span data-stu-id="4bb60-129">Example</span></span>
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

<span data-ttu-id="4bb60-130">Nell'esempio seguente viene illustrato come recuperare l'elenco di tabelle esterni dal database corrente:</span><span class="sxs-lookup"><span data-stu-id="4bb60-130">The following example shows how to retrieve the list of external tables from the current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="4bb60-131">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="4bb60-131">Remarks</span></span>
<span data-ttu-id="4bb60-132">La query elastica estende la sintassi esistente della tabella esterna per definire le tabelle esterne che usano origini dati esterne di tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="4bb60-132">Elastic query extends the existing external table syntax to define external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="4bb60-133">Una definizione di tabella esterna per il partizionamento verticale comprende gli aspetti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4bb60-133">An external table definition for vertical partitioning covers the following aspects:</span></span> 

* <span data-ttu-id="4bb60-134">**Schema**: il DDL della tabella esterna definisce uno schema che può essere usato dalle query.</span><span class="sxs-lookup"><span data-stu-id="4bb60-134">**Schema**: The external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="4bb60-135">Lo schema fornito nella definizione della tabella esterna deve corrispondere allo schema delle tabelle nel database remoto in cui sono archiviati i dati effettivi.</span><span class="sxs-lookup"><span data-stu-id="4bb60-135">The schema provided in your external table definition needs to match the schema of the tables in the remote database where the actual data is stored.</span></span> 
* <span data-ttu-id="4bb60-136">**Riferimento al database remoto**: il DDL della tabella esterna fa riferimento a un'origine dati esterna.</span><span class="sxs-lookup"><span data-stu-id="4bb60-136">**Remote database reference**: The external table DDL refers to an external data source.</span></span> <span data-ttu-id="4bb60-137">L'origine dati esterna specifica il nome del server logico e il nome del database remoto in cui sono archiviati i dati effettivi della tabella.</span><span class="sxs-lookup"><span data-stu-id="4bb60-137">The external data source specifies the logical server name and database name of the remote database where the actual table data is stored.</span></span> 

<span data-ttu-id="4bb60-138">Se si usa un'origine dati esterna, come illustrato nella sezione precedente, la sintassi per la creazione di tabelle esterne è la seguente:</span><span class="sxs-lookup"><span data-stu-id="4bb60-138">Using an external data source as outlined in the previous section, the syntax to create external tables is as follows:</span></span> 

<span data-ttu-id="4bb60-139">La clausola DATA_SOURCE definisce l'origine dati esterna, ovvero il database remoto nel caso del partizionamento verticale, usata per la tabella esterna.</span><span class="sxs-lookup"><span data-stu-id="4bb60-139">The DATA_SOURCE clause defines the external data source (i.e. the remote database in case of vertical partitioning) that is used for the external table.</span></span>  

<span data-ttu-id="4bb60-140">Le clausole SCHEMA_NAME e OBJECT_NAME consentono di mappare la definizione della tabella esterna a una tabella in uno schema diverso sul database remoto o a una tabella con un nome diverso, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="4bb60-140">The SCHEMA_NAME and OBJECT_NAME clauses provide the ability to map the external table definition to a table in a different schema on the remote database, or to a table with a different name, respectively.</span></span> <span data-ttu-id="4bb60-141">Ciò risulta utile se si vuole definire una tabella esterna per una vista del catalogo o una DMV nel database remoto o in qualsiasi altra situazione in cui il nome della tabella remota è già usato a livello locale.</span><span class="sxs-lookup"><span data-stu-id="4bb60-141">This is useful if you want to define an external table to a catalog view or DMV on your remote database - or any other situation where the remote table name is already taken locally.</span></span>  

<span data-ttu-id="4bb60-142">L'istruzione DDL seguente elimina una definizione di tabella esterna esistente da un catalogo locale.</span><span class="sxs-lookup"><span data-stu-id="4bb60-142">The following DDL statement drops an existing external table definition from the local catalog.</span></span> <span data-ttu-id="4bb60-143">Non ha alcun impatto sul database remoto.</span><span class="sxs-lookup"><span data-stu-id="4bb60-143">It does not impact the remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="4bb60-144">**Autorizzazioni per CREATE/DROP EXTERNAL TABLE**: le autorizzazioni di tipo ALTER ANY EXTERNAL DATA SOURCE sono necessarie per il DDL di tabelle esterne, che è richiesto anche per fare riferimento all'origine dati sottostante.</span><span class="sxs-lookup"><span data-stu-id="4bb60-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed to refer to the underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="4bb60-145">Considerazioni relative alla sicurezza</span><span class="sxs-lookup"><span data-stu-id="4bb60-145">Security considerations</span></span>
<span data-ttu-id="4bb60-146">Gli utenti con accesso alla tabella esterna ottengono automaticamente l'accesso alle tabelle remote sottostanti con le credenziali specificate nella definizione dell'origine dati esterna.</span><span class="sxs-lookup"><span data-stu-id="4bb60-146">Users with access to the external table automatically gain access to the underlying remote tables under the credential given in the external data source definition.</span></span> <span data-ttu-id="4bb60-147">È necessario gestire con attenzione l'accesso alla tabella esterna, in modo da evitare l'elevazione indesiderata dei privilegi tramite le credenziali dell'origine dati esterna.</span><span class="sxs-lookup"><span data-stu-id="4bb60-147">You should carefully manage access to the external table in order to avoid undesired elevation of privileges through the credential of the external data source.</span></span> <span data-ttu-id="4bb60-148">È possibile usare le normali autorizzazioni SQL per CONCEDERE o REVOCARE l'accesso a una tabella esterna, come se fosse una tabella normale.</span><span class="sxs-lookup"><span data-stu-id="4bb60-148">Regular SQL permissions can be used to GRANT or REVOKE access to an external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="4bb60-149">Esempio: esecuzione di query su database partizionati verticalmente</span><span class="sxs-lookup"><span data-stu-id="4bb60-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="4bb60-150">La query seguente esegue un join a tre vie tra le due tabelle locali per gli ordini e le righe di ordine e la tabella remota per i clienti.</span><span class="sxs-lookup"><span data-stu-id="4bb60-150">The following query performs a three-way join between the two local tables for orders and order lines and the remote table for customers.</span></span> <span data-ttu-id="4bb60-151">Ecco un esempio di caso di utilizzo dei dati di riferimento per la query elastica:</span><span class="sxs-lookup"><span data-stu-id="4bb60-151">This is an example of the reference data use case for elastic query:</span></span> 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="4bb60-152">Stored procedure per l'esecuzione remota di T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="4bb60-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="4bb60-153">La query elastica introduce anche una stored procedure che fornisce l'accesso diretto alle partizioni.</span><span class="sxs-lookup"><span data-stu-id="4bb60-153">Elastic query also introduces a stored procedure that provides direct access to the shards.</span></span> <span data-ttu-id="4bb60-154">La stored procedure è denominata [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) e può essere usata per eseguire stored procedure remote o codice T-SQL sui database remoti.</span><span class="sxs-lookup"><span data-stu-id="4bb60-154">The stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used to execute remote stored procedures or T-SQL code on the remote databases.</span></span> <span data-ttu-id="4bb60-155">È necessario specificare i seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="4bb60-155">It takes the following parameters:</span></span> 

* <span data-ttu-id="4bb60-156">Nome dell'origine dati (nvarchar): il nome dell'origine dati esterna di tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="4bb60-156">Data source name (nvarchar): The name of the external data source of type RDBMS.</span></span> 
* <span data-ttu-id="4bb60-157">Query (nvarchar): la query T-SQL da eseguire in ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="4bb60-157">Query (nvarchar): The T-SQL query to be executed on each shard.</span></span> 
* <span data-ttu-id="4bb60-158">Dichiarazione del parametro (nvarchar) - Facoltativo: stringa con definizioni del tipo di dati per i parametri usati nel parametro della query, ad esempio sp_executesql.</span><span class="sxs-lookup"><span data-stu-id="4bb60-158">Parameter declaration (nvarchar) - optional: String with data type definitions for the parameters used in the Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="4bb60-159">Elenco di valori dei parametri (facoltativo): elenco delimitato da virgole di valori dei parametri, ad esempio sp_executesql.</span><span class="sxs-lookup"><span data-stu-id="4bb60-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="4bb60-160">La stored procedure sp\_execute\_remote usa l'origine dati esterna specificata nei parametri di chiamata per eseguire l'istruzione T-SQL inclusa nei database remoti.</span><span class="sxs-lookup"><span data-stu-id="4bb60-160">The sp\_execute\_remote uses the external data source provided in the invocation parameters to execute the given T-SQL statement on the remote databases.</span></span> <span data-ttu-id="4bb60-161">Usa le credenziali dell'origine dati esterna per connettersi al database di gestione shardmap e ai database remoti.</span><span class="sxs-lookup"><span data-stu-id="4bb60-161">It uses the credential of the external data source to connect to the shardmap manager database and the remote databases.</span></span>  

<span data-ttu-id="4bb60-162">Esempio:</span><span class="sxs-lookup"><span data-stu-id="4bb60-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="4bb60-163">Connettività per gli strumenti</span><span class="sxs-lookup"><span data-stu-id="4bb60-163">Connectivity for tools</span></span>
<span data-ttu-id="4bb60-164">È possibile usare le normali stringhe di connessione di SQL Server per connettere gli strumenti di Business Intelligence e di integrazione dei dati ai database nel server del database SQL per cui sono abilitate le query elastiche e sono state definite tabelle esterne.</span><span class="sxs-lookup"><span data-stu-id="4bb60-164">You can use regular SQL Server connection strings to connect your BI and data integration tools to databases on the SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="4bb60-165">Assicurarsi che SQL Server sia supportato come origine dati per lo strumento.</span><span class="sxs-lookup"><span data-stu-id="4bb60-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="4bb60-166">Fare quindi riferimento al database elastico sottoposto a query e alle relative tabelle esterne come se fosse un qualsiasi altro database di SQL Server a cui ci si può connettere con lo strumento.</span><span class="sxs-lookup"><span data-stu-id="4bb60-166">Then refer to the elastic query database and its external tables just like any other SQL Server database that you would connect to with your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="4bb60-167">Procedure consigliate</span><span class="sxs-lookup"><span data-stu-id="4bb60-167">Best practices</span></span>
* <span data-ttu-id="4bb60-168">Assicurarsi che il database di endpoint della query elastica disponga di accesso al database remoto mediante l'abilitazione dell'accesso per i servizi di Azure nella rispettiva configurazione del firewall del database SQL.</span><span class="sxs-lookup"><span data-stu-id="4bb60-168">Ensure that the elastic query endpoint database has been given access to the remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="4bb60-169">Assicurarsi anche che le credenziali fornite nella definizione dell'origine dati esterna possano accedere correttamente al database remoto e abbiano le autorizzazioni necessarie per accedere alla tabella remota.</span><span class="sxs-lookup"><span data-stu-id="4bb60-169">Also ensure that the credential provided in the external data source definition can successfully log into the remote database and has the permissions to access the remote table.</span></span>  
* <span data-ttu-id="4bb60-170">La query elastica funziona in modo ottimale per le query in cui la maggior parte dei calcoli può essere eseguita sui database remoti.</span><span class="sxs-lookup"><span data-stu-id="4bb60-170">Elastic query works best for queries where most of the computation can be done on the remote databases.</span></span> <span data-ttu-id="4bb60-171">In genere si ottengono le prestazioni migliori per le query tramite i predicati di filtro selettivo, che possono essere valutati sui database remoti, o mediante join che possono essere eseguiti completamente nel database remoto.</span><span class="sxs-lookup"><span data-stu-id="4bb60-171">You typically get the best query performance with selective filter predicates that can be evaluated on the remote databases or joins that can be performed completely on the remote database.</span></span> <span data-ttu-id="4bb60-172">Altri modelli di query potrebbero richiedere il caricamento di quantità elevate di dati dal database remoto e potrebbero offrire prestazioni ridotte.</span><span class="sxs-lookup"><span data-stu-id="4bb60-172">Other query patterns may need to load large amounts of data from the remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4bb60-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4bb60-173">Next steps</span></span>

* <span data-ttu-id="4bb60-174">Per un approfondimento, vedere [Panoramica delle query elastiche](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4bb60-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="4bb60-175">Per un'esercitazione sul partizionamento verticale, vedere [Introduzione alle query tra database (partizionamento verticale)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="4bb60-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="4bb60-176">Per un'esercitazione sul partizionamento orizzontale, vedere la [guida introduttiva alle query elastiche per il partizionamento orizzontale](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="4bb60-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="4bb60-177">Per le query di esempio e sintassi per i dati con partizionamento orizzontale, vedere [Eseguire query su dati con partizionamento orizzontale](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="4bb60-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="4bb60-178">Vedere [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) per una stored procedure che esegue un'istruzione Transact-SQL su un singolo database SQL di Azure remoto o un set di database che fungono da partizioni in uno schema di partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="4bb60-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
