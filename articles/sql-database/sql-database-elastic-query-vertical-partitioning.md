---
title: i database con schema diverso aaaQuery tra cloud | Documenti Microsoft
description: come tooset le query tra database in partizioni verticali
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
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a><span data-ttu-id="5a573-103">Eseguire query in database cloud con schemi diversi (anteprima)</span><span class="sxs-lookup"><span data-stu-id="5a573-103">Query across cloud databases with different schemas (preview)</span></span>
![Eseguire una query tra tabelle in vari database][1]

<span data-ttu-id="5a573-105">I database con partizionamento verticale usano set di tabelle diversi su database diversi.</span><span class="sxs-lookup"><span data-stu-id="5a573-105">Vertically-partitioned databases use different sets of tables on different databases.</span></span> <span data-ttu-id="5a573-106">Ciò significa che lo schema hello è diverso in database diversi.</span><span class="sxs-lookup"><span data-stu-id="5a573-106">That means that hello schema is different on different databases.</span></span> <span data-ttu-id="5a573-107">Ad esempio, tutte le tabelle per l'inventario si trovano in un database, mentre le tabelle correlate alla contabilità si trovano in un altro database.</span><span class="sxs-lookup"><span data-stu-id="5a573-107">For instance, all tables for inventory are on one database while all accounting-related tables are on a second database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5a573-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5a573-108">Prerequisites</span></span>
* <span data-ttu-id="5a573-109">utente Hello deve disporre dell'autorizzazione ALTER ANY EXTERNAL DATA SOURCE.</span><span class="sxs-lookup"><span data-stu-id="5a573-109">hello user must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="5a573-110">Questa autorizzazione è inclusa con l'autorizzazione ALTER DATABASE hello.</span><span class="sxs-lookup"><span data-stu-id="5a573-110">This permission is included with hello ALTER DATABASE permission.</span></span>
* <span data-ttu-id="5a573-111">Le autorizzazioni ALTER ANY EXTERNAL DATA SOURCE sono necessari toorefer toohello origine dati sottostante.</span><span class="sxs-lookup"><span data-stu-id="5a573-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="overview"></a><span data-ttu-id="5a573-112">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5a573-112">Overview</span></span>

> [!NOTE]
> <span data-ttu-id="5a573-113">A differenza con partizionamento orizzontale, queste istruzioni DDL non basarsi sulla definizione di un livello dati con una mappa partizioni tramite libreria client di database elastico hello.</span><span class="sxs-lookup"><span data-stu-id="5a573-113">Unlike with horizontal partitioning, these DDL statements do not depend on defining a data tier with a shard map through hello elastic database client library.</span></span>
>

1. [<span data-ttu-id="5a573-114">CREATE MASTER KEY</span><span class="sxs-lookup"><span data-stu-id="5a573-114">CREATE MASTER KEY</span></span>](https://msdn.microsoft.com/library/ms174382.aspx)
2. [<span data-ttu-id="5a573-115">CREATE DATABASE SCOPED CREDENTIAL</span><span class="sxs-lookup"><span data-stu-id="5a573-115">CREATE DATABASE SCOPED CREDENTIAL</span></span>](https://msdn.microsoft.com/library/mt270260.aspx)
3. [<span data-ttu-id="5a573-116">CREATE EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="5a573-116">CREATE EXTERNAL DATA SOURCE</span></span>](https://msdn.microsoft.com/library/dn935022.aspx)
4. [<span data-ttu-id="5a573-117">CREATE EXTERNAL TABLE</span><span class="sxs-lookup"><span data-stu-id="5a573-117">CREATE EXTERNAL TABLE</span></span>](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a><span data-ttu-id="5a573-118">Creare la chiave master e le credenziali con ambito database</span><span class="sxs-lookup"><span data-stu-id="5a573-118">Create database scoped master key and credentials</span></span>
<span data-ttu-id="5a573-119">Hello credenziali vengono utilizzate dal database remoti tooyour tooconnect query elastico hello.</span><span class="sxs-lookup"><span data-stu-id="5a573-119">hello credential is used by hello elastic query tooconnect tooyour remote databases.</span></span>  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> <span data-ttu-id="5a573-120">Verificare che hello `<username>` non include alcun **"@servername"** suffisso.</span><span class="sxs-lookup"><span data-stu-id="5a573-120">Ensure that hello `<username>` does not include any **"@servername"** suffix.</span></span> 
>

## <a name="create-external-data-sources"></a><span data-ttu-id="5a573-121">Creare origini dati esterne</span><span class="sxs-lookup"><span data-stu-id="5a573-121">Create external data sources</span></span>
<span data-ttu-id="5a573-122">Sintassi:</span><span class="sxs-lookup"><span data-stu-id="5a573-122">Syntax:</span></span>

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> <span data-ttu-id="5a573-123">è necessario impostare il parametro di tipo Hello troppo**RDBMS**.</span><span class="sxs-lookup"><span data-stu-id="5a573-123">hello TYPE parameter must be set too**RDBMS**.</span></span> 
>

### <a name="example"></a><span data-ttu-id="5a573-124">Esempio</span><span class="sxs-lookup"><span data-stu-id="5a573-124">Example</span></span>
<span data-ttu-id="5a573-125">Hello seguente viene illustrato hello utilizzo dell'istruzione CREATE hello per le origini dati esterne.</span><span class="sxs-lookup"><span data-stu-id="5a573-125">hello following example illustrates hello use of hello CREATE statement for external data sources.</span></span> 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

<span data-ttu-id="5a573-126">elenco di hello tooretrieve delle origini dati esterne corrente:</span><span class="sxs-lookup"><span data-stu-id="5a573-126">tooretrieve hello list of current external data sources:</span></span> 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a><span data-ttu-id="5a573-127">Tabelle esterne</span><span class="sxs-lookup"><span data-stu-id="5a573-127">External Tables</span></span>
<span data-ttu-id="5a573-128">Sintassi:</span><span class="sxs-lookup"><span data-stu-id="5a573-128">Syntax:</span></span>

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a><span data-ttu-id="5a573-129">Esempio</span><span class="sxs-lookup"><span data-stu-id="5a573-129">Example</span></span>
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

<span data-ttu-id="5a573-130">Hello di esempio seguente viene illustrato come tooretrieve hello elenco di tabelle esterne dal database corrente hello:</span><span class="sxs-lookup"><span data-stu-id="5a573-130">hello following example shows how tooretrieve hello list of external tables from hello current database:</span></span> 

    select * from sys.external_tables; 

### <a name="remarks"></a><span data-ttu-id="5a573-131">Osservazioni</span><span class="sxs-lookup"><span data-stu-id="5a573-131">Remarks</span></span>
<span data-ttu-id="5a573-132">Query elastico estende hello tabella esterna sintassi toodefine esterno tabelle esistenti che utilizzano origini dati esterne di tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="5a573-132">Elastic query extends hello existing external table syntax toodefine external tables that use external data sources of type RDBMS.</span></span> <span data-ttu-id="5a573-133">Una definizione di tabella esterna per il partizionamento verticale copre hello seguenti aspetti:</span><span class="sxs-lookup"><span data-stu-id="5a573-133">An external table definition for vertical partitioning covers hello following aspects:</span></span> 

* <span data-ttu-id="5a573-134">**Schema**: tabella esterna hello DDL definisce uno schema che è possono utilizzare le query.</span><span class="sxs-lookup"><span data-stu-id="5a573-134">**Schema**: hello external table DDL defines a schema that your queries can use.</span></span> <span data-ttu-id="5a573-135">schema di Hello fornito nella definizione della tabella esterna deve schema hello toomatch delle tabelle di hello nel database remoto di hello dove vengono archiviati dati effettivi hello.</span><span class="sxs-lookup"><span data-stu-id="5a573-135">hello schema provided in your external table definition needs toomatch hello schema of hello tables in hello remote database where hello actual data is stored.</span></span> 
* <span data-ttu-id="5a573-136">**Riferimento al database remoto**: tabella esterna hello DDL fa riferimento l'origine dati esterna tooan.</span><span class="sxs-lookup"><span data-stu-id="5a573-136">**Remote database reference**: hello external table DDL refers tooan external data source.</span></span> <span data-ttu-id="5a573-137">origine dati esterna Hello Specifica nome del server logico hello e nome del database remoto di hello dove vengono archiviati i dati di tabella effettiva hello.</span><span class="sxs-lookup"><span data-stu-id="5a573-137">hello external data source specifies hello logical server name and database name of hello remote database where hello actual table data is stored.</span></span> 

<span data-ttu-id="5a573-138">Le tabelle esterne hello sintassi toocreate utilizzando un'origine dati esterna, come descritto nella sezione precedente di hello, è come segue:</span><span class="sxs-lookup"><span data-stu-id="5a573-138">Using an external data source as outlined in hello previous section, hello syntax toocreate external tables is as follows:</span></span> 

<span data-ttu-id="5a573-139">clausola DATA_SOURCE Hello definisce l'origine dati esterna hello (ad esempio hello database remoto in caso di partizionamento verticale) che viene utilizzato per la tabella esterna hello.</span><span class="sxs-lookup"><span data-stu-id="5a573-139">hello DATA_SOURCE clause defines hello external data source (i.e. hello remote database in case of vertical partitioning) that is used for hello external table.</span></span>  

<span data-ttu-id="5a573-140">le clausole nome_schema e nome_oggetto Hello forniscono hello possibilità toomap hello tabella esterna tooa tabella per la definizione in un altro schema nel database remoto hello o tooa tabella con un nome diverso, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="5a573-140">hello SCHEMA_NAME and OBJECT_NAME clauses provide hello ability toomap hello external table definition tooa table in a different schema on hello remote database, or tooa table with a different name, respectively.</span></span> <span data-ttu-id="5a573-141">Ciò è utile se si desidera toodefine una vista del catalogo tooa tabella esterna o DMV del database remoto, o qualsiasi altra situazione in cui il nome di tabella remota hello è già in uso in locale.</span><span class="sxs-lookup"><span data-stu-id="5a573-141">This is useful if you want toodefine an external table tooa catalog view or DMV on your remote database - or any other situation where hello remote table name is already taken locally.</span></span>  

<span data-ttu-id="5a573-142">Hello istruzione DDL seguente elimina una definizione di tabella esterna esistente dal catalogo locale hello.</span><span class="sxs-lookup"><span data-stu-id="5a573-142">hello following DDL statement drops an existing external table definition from hello local catalog.</span></span> <span data-ttu-id="5a573-143">Non influisce sulla database remoto hello.</span><span class="sxs-lookup"><span data-stu-id="5a573-143">It does not impact hello remote database.</span></span> 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

<span data-ttu-id="5a573-144">**Le autorizzazioni per CREATE/DROP TABLE esterno**: sono necessarie le autorizzazioni ALTER ANY EXTERNAL DATA SOURCE per la tabella esterna DDL che è anche necessario toorefer toohello origine dei dati sottostante.</span><span class="sxs-lookup"><span data-stu-id="5a573-144">**Permissions for CREATE/DROP EXTERNAL TABLE**: ALTER ANY EXTERNAL DATA SOURCE permissions are needed for external table DDL which is also needed toorefer toohello underlying data source.</span></span>  

## <a name="security-considerations"></a><span data-ttu-id="5a573-145">Considerazioni relative alla sicurezza</span><span class="sxs-lookup"><span data-stu-id="5a573-145">Security considerations</span></span>
<span data-ttu-id="5a573-146">Gli utenti con una tabella esterna toohello di accesso accedere automaticamente toohello tabelle remote sottostanti in credenziali hello specificata nella definizione dell'origine dati esterna hello.</span><span class="sxs-lookup"><span data-stu-id="5a573-146">Users with access toohello external table automatically gain access toohello underlying remote tables under hello credential given in hello external data source definition.</span></span> <span data-ttu-id="5a573-147">È consigliabile gestire attentamente tabella esterna di accesso toohello elevazione tooavoid indesiderati di ordine dei privilegi tramite credenziali hello dell'origine dati esterna hello.</span><span class="sxs-lookup"><span data-stu-id="5a573-147">You should carefully manage access toohello external table in order tooavoid undesired elevation of privileges through hello credential of hello external data source.</span></span> <span data-ttu-id="5a573-148">Regolare autorizzazioni SQL possono essere utilizzato tooGRANT o tabella esterna tooan di revocare l'accesso come se fosse una normale tabella.</span><span class="sxs-lookup"><span data-stu-id="5a573-148">Regular SQL permissions can be used tooGRANT or REVOKE access tooan external table just as though it were a regular table.</span></span>  

## <a name="example-querying-vertically-partitioned-databases"></a><span data-ttu-id="5a573-149">Esempio: esecuzione di query su database partizionati verticalmente</span><span class="sxs-lookup"><span data-stu-id="5a573-149">Example: querying vertically partitioned databases</span></span>
<span data-ttu-id="5a573-150">Hello nella query seguente esegue un join a tre vie tra due tabelle locali hello per le righe dell'ordine e ordini e la tabella remota hello per i clienti.</span><span class="sxs-lookup"><span data-stu-id="5a573-150">hello following query performs a three-way join between hello two local tables for orders and order lines and hello remote table for customers.</span></span> <span data-ttu-id="5a573-151">Questo è un esempio di hello caso d'uso di dati di riferimento per query elastico:</span><span class="sxs-lookup"><span data-stu-id="5a573-151">This is an example of hello reference data use case for elastic query:</span></span> 

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


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a><span data-ttu-id="5a573-152">Stored procedure per l'esecuzione remota di T-SQL: sp\_execute_remote</span><span class="sxs-lookup"><span data-stu-id="5a573-152">Stored procedure for remote T-SQL execution: sp\_execute_remote</span></span>
<span data-ttu-id="5a573-153">Query elastico introduce inoltre una stored procedure che fornisce accesso diretto toohello partizioni.</span><span class="sxs-lookup"><span data-stu-id="5a573-153">Elastic query also introduces a stored procedure that provides direct access toohello shards.</span></span> <span data-ttu-id="5a573-154">Hello stored procedure viene chiamata [sp\_eseguire \_remoto](https://msdn.microsoft.com/library/mt703714) e può essere utilizzato tooexecute stored procedure remote o il codice T-SQL nel database remoto hello.</span><span class="sxs-lookup"><span data-stu-id="5a573-154">hello stored procedure is called [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) and can be used tooexecute remote stored procedures or T-SQL code on hello remote databases.</span></span> <span data-ttu-id="5a573-155">Avrà hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="5a573-155">It takes hello following parameters:</span></span> 

* <span data-ttu-id="5a573-156">Nome dell'origine dati (nvarchar): nome hello dell'origine dati esterna hello di tipo RDBMS.</span><span class="sxs-lookup"><span data-stu-id="5a573-156">Data source name (nvarchar): hello name of hello external data source of type RDBMS.</span></span> 
* <span data-ttu-id="5a573-157">Query (nvarchar): toobe query hello T-SQL eseguito su ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="5a573-157">Query (nvarchar): hello T-SQL query toobe executed on each shard.</span></span> 
* <span data-ttu-id="5a573-158">Dichiarazione di parametro (nvarchar) - facoltativa: stringa con definizioni dei tipi di dati per i parametri di hello utilizzati nel parametro di Query hello (ad esempio sp_executesql).</span><span class="sxs-lookup"><span data-stu-id="5a573-158">Parameter declaration (nvarchar) - optional: String with data type definitions for hello parameters used in hello Query parameter (like sp_executesql).</span></span> 
* <span data-ttu-id="5a573-159">Elenco di valori dei parametri (facoltativo): elenco delimitato da virgole di valori dei parametri, ad esempio sp_executesql.</span><span class="sxs-lookup"><span data-stu-id="5a573-159">Parameter value list - optional: Comma-separated list of parameter values (like sp_executesql).</span></span>

<span data-ttu-id="5a573-160">sp Hello\_eseguire\_remoto utilizza hello origine dati esterna cui hello chiamata parametri tooexecute hello dato istruzione T-SQL nel database remoto hello.</span><span class="sxs-lookup"><span data-stu-id="5a573-160">hello sp\_execute\_remote uses hello external data source provided in hello invocation parameters tooexecute hello given T-SQL statement on hello remote databases.</span></span> <span data-ttu-id="5a573-161">Usa credenziali hello del database di gestione di hello dati esterni origine tooconnect toohello shardmap e database remoti hello.</span><span class="sxs-lookup"><span data-stu-id="5a573-161">It uses hello credential of hello external data source tooconnect toohello shardmap manager database and hello remote databases.</span></span>  

<span data-ttu-id="5a573-162">Esempio:</span><span class="sxs-lookup"><span data-stu-id="5a573-162">Example:</span></span> 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a><span data-ttu-id="5a573-163">Connettività per gli strumenti</span><span class="sxs-lookup"><span data-stu-id="5a573-163">Connectivity for tools</span></span>
<span data-ttu-id="5a573-164">È possibile utilizzare l'integrazione strumenti toodatabases di BI e i dati regolari tooconnect di stringhe di connessione SQL Server nel server di database di SQL Server hello con query elastico abilitato e le tabelle esterne definite.</span><span class="sxs-lookup"><span data-stu-id="5a573-164">You can use regular SQL Server connection strings tooconnect your BI and data integration tools toodatabases on hello SQL DB server that has elastic query enabled and external tables defined.</span></span> <span data-ttu-id="5a573-165">Assicurarsi che SQL Server sia supportato come origine dati per lo strumento.</span><span class="sxs-lookup"><span data-stu-id="5a573-165">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="5a573-166">Fare riferimento a database elastico query toohello e le relative tabelle esterne come qualsiasi altro database di SQL Server si connetterà toowith dallo strumento.</span><span class="sxs-lookup"><span data-stu-id="5a573-166">Then refer toohello elastic query database and its external tables just like any other SQL Server database that you would connect toowith your tool.</span></span> 

## <a name="best-practices"></a><span data-ttu-id="5a573-167">Procedure consigliate</span><span class="sxs-lookup"><span data-stu-id="5a573-167">Best practices</span></span>
* <span data-ttu-id="5a573-168">Assicurarsi di che database elastico query endpoint hello ha database remoto di accesso toohello abilitando l'accesso per i servizi di Azure la configurazione di firewall di database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5a573-168">Ensure that hello elastic query endpoint database has been given access toohello remote database by enabling access for Azure Services in its SQL DB firewall configuration.</span></span> <span data-ttu-id="5a573-169">Assicurarsi inoltre che credenziali hello fornita in dati esterni hello definizione di origine può accedere senza problemi nel database remoto hello e ha una tabella remota hello tooaccess autorizzazioni hello.</span><span class="sxs-lookup"><span data-stu-id="5a573-169">Also ensure that hello credential provided in hello external data source definition can successfully log into hello remote database and has hello permissions tooaccess hello remote table.</span></span>  
* <span data-ttu-id="5a573-170">Query elastico è ideale per le query in cui la maggior parte del calcolo hello possono essere eseguita nel database remoto hello.</span><span class="sxs-lookup"><span data-stu-id="5a573-170">Elastic query works best for queries where most of hello computation can be done on hello remote databases.</span></span> <span data-ttu-id="5a573-171">In genere, si ottiene hello migliori prestazioni di query con predicati di filtro selettivo che possono essere valutati sul database remoto hello o join che possono essere eseguite completamente nel database remoto hello.</span><span class="sxs-lookup"><span data-stu-id="5a573-171">You typically get hello best query performance with selective filter predicates that can be evaluated on hello remote databases or joins that can be performed completely on hello remote database.</span></span> <span data-ttu-id="5a573-172">Altri modelli di query potrebbe essere necessario grandi quantità di tooload dei dati dal database remoto hello e potrebbero essere scarse.</span><span class="sxs-lookup"><span data-stu-id="5a573-172">Other query patterns may need tooload large amounts of data from hello remote database and may perform poorly.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5a573-173">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5a573-173">Next steps</span></span>

* <span data-ttu-id="5a573-174">Per un approfondimento, vedere [Panoramica delle query elastiche](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a573-174">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="5a573-175">Per un'esercitazione sul partizionamento verticale, vedere [Introduzione alle query tra database (partizionamento verticale)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="5a573-175">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="5a573-176">Per un'esercitazione sul partizionamento orizzontale, vedere la [guida introduttiva alle query elastiche per il partizionamento orizzontale](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="5a573-176">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="5a573-177">Per le query di esempio e sintassi per i dati con partizionamento orizzontale, vedere [Eseguire query su dati con partizionamento orizzontale](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="5a573-177">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="5a573-178">Vedere [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) per una stored procedure che esegue un'istruzione Transact-SQL su un singolo database SQL di Azure remoto o un set di database che fungono da partizioni in uno schema di partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="5a573-178">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
