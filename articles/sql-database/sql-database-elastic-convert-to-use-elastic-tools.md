---
title: "Eseguire la migrazione dei database esistenti per ottenere scalabilità orizzontale | Documentazione Microsoft"
description: Convertire database partizionati per l'uso di strumenti dei database elastici mediante la creazione di un gestore mappe partizioni
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 099f40d00753b7c86ba726a818f17d440a125221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-existing-databases-to-scale-out"></a><span data-ttu-id="09d5e-103">Eseguire la migrazione dei database esistenti per ottenere scalabilità orizzontale</span><span class="sxs-lookup"><span data-stu-id="09d5e-103">Migrate existing databases to scale-out</span></span>
<span data-ttu-id="09d5e-104">È possibile gestire facilmente i database partizionati con scalabilità orizzontale esistenti usando gli strumenti di database del database SQL di Azure, come ad esempio la [libreria client dei database elastici](sql-database-elastic-database-client-library.md).</span><span class="sxs-lookup"><span data-stu-id="09d5e-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as the [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> <span data-ttu-id="09d5e-105">Prima è necessario convertire un set di database esistente per l'uso del [gestore delle mappe partizioni](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="09d5e-105">You must first convert an existing set of databases to use the [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="09d5e-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="09d5e-106">Overview</span></span>
<span data-ttu-id="09d5e-107">Per eseguire la migrazione di un database partizionato esistente:</span><span class="sxs-lookup"><span data-stu-id="09d5e-107">To migrate an existing sharded database:</span></span> 

1. <span data-ttu-id="09d5e-108">Preparare il [database del gestore delle mappe partizioni](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="09d5e-108">Prepare the [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span></span>
2. <span data-ttu-id="09d5e-109">Creare la mappa partizioni.</span><span class="sxs-lookup"><span data-stu-id="09d5e-109">Create the shard map.</span></span>
3. <span data-ttu-id="09d5e-110">Preparare le singole partizioni.</span><span class="sxs-lookup"><span data-stu-id="09d5e-110">Prepare the individual shards.</span></span>  
4. <span data-ttu-id="09d5e-111">Aggiungere i mapping alla mappa partizioni.</span><span class="sxs-lookup"><span data-stu-id="09d5e-111">Add mappings to the shard map.</span></span>

<span data-ttu-id="09d5e-112">Queste tecniche possono essere implementate tramite la [libreria client .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) o gli script di PowerShell disponibili nella pagina relativa agli [script degli strumenti di database elastico del database SQL di Azure](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="09d5e-112">These techniques can be implemented using either the [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or the PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span> <span data-ttu-id="09d5e-113">Negli esempi in questo articolo vengono usati gli script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="09d5e-113">The examples here use the PowerShell scripts.</span></span>

<span data-ttu-id="09d5e-114">Per altre informazioni su ShardMapManager, vedere [Gestione mappe partizioni](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="09d5e-114">For more information about the ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="09d5e-115">Per una panoramica sugli strumenti di database elastici, vedere [Panoramica sulle funzionalità di database elastico](sql-database-elastic-scale-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="09d5e-115">For an overview of the elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span></span>

## <a name="prepare-the-shard-map-manager-database"></a><span data-ttu-id="09d5e-116">Preparare il database del gestore delle mappe partizioni</span><span class="sxs-lookup"><span data-stu-id="09d5e-116">Prepare the shard map manager database</span></span>
<span data-ttu-id="09d5e-117">Il gestore delle mappe partizioni è un database speciale che contiene i dati per la gestione dei database con un numero maggiore di istanze.</span><span class="sxs-lookup"><span data-stu-id="09d5e-117">The shard map manager is a special database that contains the data to manage scaled-out databases.</span></span> <span data-ttu-id="09d5e-118">È possibile usare un database esistente o crearne un nuovo.</span><span class="sxs-lookup"><span data-stu-id="09d5e-118">You can use an existing database, or create a new database.</span></span> <span data-ttu-id="09d5e-119">Si noti che il database che funge da gestore delle mappe partizioni non deve essere lo stesso della partizione.</span><span class="sxs-lookup"><span data-stu-id="09d5e-119">Note that a database acting as shard map manager should not be the same database as a shard.</span></span> <span data-ttu-id="09d5e-120">Si noti anche che lo script di PowerShell non crea automaticamente il database.</span><span class="sxs-lookup"><span data-stu-id="09d5e-120">Also note that the PowerShell script does not create the database for you.</span></span> 

## <a name="step-1-create-a-shard-map-manager"></a><span data-ttu-id="09d5e-121">Passaggio 1: Creare un gestore mappe partizioni</span><span class="sxs-lookup"><span data-stu-id="09d5e-121">Step 1: create a shard map manager</span></span>
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are the server name and database name 
    # for the new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="to-retrieve-the-shard-map-manager"></a><span data-ttu-id="09d5e-122">Per recuperare il gestore mappe partizioni</span><span class="sxs-lookup"><span data-stu-id="09d5e-122">To retrieve the shard map manager</span></span>
<span data-ttu-id="09d5e-123">Dopo la creazione, è possibile recuperare il gestore mappe partizioni con questo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="09d5e-123">After creation, you can retrieve the shard map manager with this cmdlet.</span></span> <span data-ttu-id="09d5e-124">Questo passaggio è necessario ogni volta che si deve usare l'oggetto ShardMapManager.</span><span class="sxs-lookup"><span data-stu-id="09d5e-124">This step is needed every time you need to use the ShardMapManager object.</span></span>

    # Try to get a reference to the Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-the-shard-map"></a><span data-ttu-id="09d5e-125">Passaggio 2: Creare la mappa partizioni</span><span class="sxs-lookup"><span data-stu-id="09d5e-125">Step 2: create the shard map</span></span>
<span data-ttu-id="09d5e-126">È necessario selezionare il tipo di mappa partizioni da creare.</span><span class="sxs-lookup"><span data-stu-id="09d5e-126">You must select the type of shard map to create.</span></span> <span data-ttu-id="09d5e-127">La scelta dipende dall'architettura del database:</span><span class="sxs-lookup"><span data-stu-id="09d5e-127">The choice depends on the database architecture:</span></span> 

1. <span data-ttu-id="09d5e-128">Singolo tenant per database. Per informazioni sui i termini, vedere il [glossario](sql-database-elastic-scale-glossary.md).</span><span class="sxs-lookup"><span data-stu-id="09d5e-128">Single tenant per database (For terms, see the [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
2. <span data-ttu-id="09d5e-129">Più tenant per database (due tipi):</span><span class="sxs-lookup"><span data-stu-id="09d5e-129">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="09d5e-130">Mapping di tipo elenco</span><span class="sxs-lookup"><span data-stu-id="09d5e-130">List mapping</span></span>
   2. <span data-ttu-id="09d5e-131">Mapping di tipo intervallo</span><span class="sxs-lookup"><span data-stu-id="09d5e-131">Range mapping</span></span>

<span data-ttu-id="09d5e-132">Per un modello a singolo tenant, creare una mappa partizioni con **mapping di tipo elenco** .</span><span class="sxs-lookup"><span data-stu-id="09d5e-132">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="09d5e-133">Il modello single-tenant assegna un database per tenant.</span><span class="sxs-lookup"><span data-stu-id="09d5e-133">The single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="09d5e-134">Si tratta di un modello efficace per gli sviluppatori SaaS in quanto semplifica la gestione.</span><span class="sxs-lookup"><span data-stu-id="09d5e-134">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Mapping di tipo elenco][1]

<span data-ttu-id="09d5e-136">Il modello multi-tenant assegna diversi tenant a un database singolo ed è possibile distribuire gruppi di tenant tra più database.</span><span class="sxs-lookup"><span data-stu-id="09d5e-136">The multi-tenant model assigns several tenants to a single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="09d5e-137">Usare questo modello quando si prevedono esigenze di dati ridotte per ogni tenant.</span><span class="sxs-lookup"><span data-stu-id="09d5e-137">Use this model when you expect each tenant to have small data needs.</span></span> <span data-ttu-id="09d5e-138">In questo modello viene assegnato un intervallo di tenant a un database usando il **mapping di tipo intervallo**.</span><span class="sxs-lookup"><span data-stu-id="09d5e-138">In this model, we assign a range of tenants to a database using **range mapping**.</span></span> 

![Mapping di tipo intervallo][2]

<span data-ttu-id="09d5e-140">In alternativa è possibile implementare un modello di database multi-tenant usando il *mapping di tipo elenco* per assegnare più tenant a un database singolo.</span><span class="sxs-lookup"><span data-stu-id="09d5e-140">Or you can implement a multi-tenant database model using a *list mapping* to assign multiple tenants to a single database.</span></span> <span data-ttu-id="09d5e-141">Ad esempio, DB1 viene usato per archiviare le informazioni sugli ID tenant 1 e 5 e DB2 archivia i dati per i tenant 7 e 10.</span><span class="sxs-lookup"><span data-stu-id="09d5e-141">For example, DB1 is used to store information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Tenant multipli su database singolo][3] 

<span data-ttu-id="09d5e-143">**In base alla scelta effettuata, procedere con una delle opzioni seguenti:**</span><span class="sxs-lookup"><span data-stu-id="09d5e-143">**Based on your choice, choose one of these options:**</span></span>

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a><span data-ttu-id="09d5e-144">Opzione 1: creare una mappa partizioni per un mapping di tipo elenco</span><span class="sxs-lookup"><span data-stu-id="09d5e-144">Option 1: create a shard map for a list mapping</span></span>
<span data-ttu-id="09d5e-145">Creare una mappa partizioni usando l'oggetto ShardMapManager.</span><span class="sxs-lookup"><span data-stu-id="09d5e-145">Create a shard map using the ShardMapManager object.</span></span> 

    # $ShardMapManager is the shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a><span data-ttu-id="09d5e-146">Opzione 2: creare una mappa partizioni per un mapping di tipo intervallo</span><span class="sxs-lookup"><span data-stu-id="09d5e-146">Option 2: create a shard map for a range mapping</span></span>
<span data-ttu-id="09d5e-147">Si noti che per usare questo modello di mapping, i valori dell'ID tenant devono essere a intervalli continui ed è accettabile avere gap negli intervalli semplicemente ignorando l'intervallo durante la creazione dei database.</span><span class="sxs-lookup"><span data-stu-id="09d5e-147">Note that to utilize this mapping pattern, tenant id values needs to be continuous ranges, and it is acceptable to have gap in the ranges by simply skipping the range when creating the databases.</span></span>

    # $ShardMapManager is the shard map manager object 
    # 'RangeShardMap' is the unique identifier for the range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a><span data-ttu-id="09d5e-148">Opzione 3: eseguire il mapping di tipo elenco in un database singolo</span><span class="sxs-lookup"><span data-stu-id="09d5e-148">Option 3: List mappings on a single database</span></span>
<span data-ttu-id="09d5e-149">Per l'impostazione di questo modello è necessario anche creare una mappa di tipo elenco, come illustrato nel passaggio 2, opzione 1.</span><span class="sxs-lookup"><span data-stu-id="09d5e-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span></span>

## <a name="step-3-prepare-individual-shards"></a><span data-ttu-id="09d5e-150">Passaggio 3: preparare le singole partizioni</span><span class="sxs-lookup"><span data-stu-id="09d5e-150">Step 3: Prepare individual shards</span></span>
<span data-ttu-id="09d5e-151">Aggiungere ciascuna partizione (database) al gestore mappe partizioni.</span><span class="sxs-lookup"><span data-stu-id="09d5e-151">Add each shard (database) to the shard map manager.</span></span> <span data-ttu-id="09d5e-152">Ciò consente di preparare i singoli database per l'archiviazione delle informazioni di mapping.</span><span class="sxs-lookup"><span data-stu-id="09d5e-152">This prepares the individual databases for storing mapping information.</span></span> <span data-ttu-id="09d5e-153">Eseguire questo metodo su ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="09d5e-153">Execute this method on each shard.</span></span>

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # The $ShardMap is the shard map created in step 2.


## <a name="step-4-add-mappings"></a><span data-ttu-id="09d5e-154">Passaggio 4: aggiungere mapping</span><span class="sxs-lookup"><span data-stu-id="09d5e-154">Step 4: Add mappings</span></span>
<span data-ttu-id="09d5e-155">L'aggiunta di mapping dipende dal tipo di mappa partizioni creato.</span><span class="sxs-lookup"><span data-stu-id="09d5e-155">The addition of mappings depends on the kind of shard map you created.</span></span> <span data-ttu-id="09d5e-156">Se è stata creata una mappa di tipo elenco, aggiungere mapping di tipo elenco.</span><span class="sxs-lookup"><span data-stu-id="09d5e-156">If you created a list map, you add list mappings.</span></span> <span data-ttu-id="09d5e-157">Se è stata creata una mappa di tipo intervallo, aggiungere mapping di tipo intervallo.</span><span class="sxs-lookup"><span data-stu-id="09d5e-157">If you created a range map, you add range mappings.</span></span>

### <a name="option-1-map-the-data-for-a-list-mapping"></a><span data-ttu-id="09d5e-158">Opzione 1: eseguire il mapping dei dati per il mapping di tipo elenco</span><span class="sxs-lookup"><span data-stu-id="09d5e-158">Option 1: map the data for a list mapping</span></span>
<span data-ttu-id="09d5e-159">Eseguire il mapping dei dati aggiungendo un mapping di tipo elenco per ogni tenant.</span><span class="sxs-lookup"><span data-stu-id="09d5e-159">Map the data by adding a list mapping for each tenant.</span></span>  

    # Create the mappings and associate it with the new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-the-data-for-a-range-mapping"></a><span data-ttu-id="09d5e-160">Opzione 2: eseguire il mapping dei dati per il mapping di tipo intervallo</span><span class="sxs-lookup"><span data-stu-id="09d5e-160">Option 2: map the data for a range mapping</span></span>
<span data-ttu-id="09d5e-161">Aggiungere il mapping di tipo intervallo per tutte le associazioni intervallo ID tenant - database:</span><span class="sxs-lookup"><span data-stu-id="09d5e-161">Add the range mappings for all the tenant id range - database associations:</span></span>

    # Create the mappings and associate it with the new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-the-data-for-multiple-tenants-on-a-single-database"></a><span data-ttu-id="09d5e-162">Passaggio 4, opzione 3: eseguire il mapping dei dati per più tenant su un database singolo</span><span class="sxs-lookup"><span data-stu-id="09d5e-162">Step 4 option 3: map the data for multiple tenants on a single database</span></span>
<span data-ttu-id="09d5e-163">Per ogni tenant eseguire Add-ListMapping (opzione 1, come riportato sopra).</span><span class="sxs-lookup"><span data-stu-id="09d5e-163">For each tenant, run the Add-ListMapping (option 1, above).</span></span> 

## <a name="checking-the-mappings"></a><span data-ttu-id="09d5e-164">Verifica dei mapping</span><span class="sxs-lookup"><span data-stu-id="09d5e-164">Checking the mappings</span></span>
<span data-ttu-id="09d5e-165">È possibile eseguire query per ottenere informazioni sulle partizioni esistenti e sui mapping a esse associati usando i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="09d5e-165">Information about the existing shards and the mappings associated with them can be queried using following commands:</span></span>  

    # List the shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a><span data-ttu-id="09d5e-166">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="09d5e-166">Summary</span></span>
<span data-ttu-id="09d5e-167">Dopo aver completato l'installazione, è possibile iniziare a usare la libreria client di database elastici.</span><span class="sxs-lookup"><span data-stu-id="09d5e-167">Once you have completed the setup, you can begin to use the Elastic Database client library.</span></span> <span data-ttu-id="09d5e-168">È anche possibile usare il [routing dipendente dai dati](sql-database-elastic-scale-data-dependent-routing.md) e le [query su più partizioni](sql-database-elastic-scale-multishard-querying.md).</span><span class="sxs-lookup"><span data-stu-id="09d5e-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09d5e-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="09d5e-169">Next steps</span></span>
<span data-ttu-id="09d5e-170">Gli script di PowerShell sono disponibili nella pagina relativa agli [script degli strumenti di database elastici del database SQL di Azure](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="09d5e-170">Get the PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

<span data-ttu-id="09d5e-171">Gli strumenti sono disponibili anche in GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span><span class="sxs-lookup"><span data-stu-id="09d5e-171">The tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span></span>

<span data-ttu-id="09d5e-172">Usare lo strumento di suddivisione-unione per spostare dati in o da un modello multi-tenant a un modello single-tenant.</span><span class="sxs-lookup"><span data-stu-id="09d5e-172">Use the split-merge tool to move data to or from a multi-tenant model to a single tenant model.</span></span> <span data-ttu-id="09d5e-173">Vedere la pagina relativa allo [strumento di divisione-unione](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="09d5e-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="09d5e-174">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="09d5e-174">Additional resources</span></span>
<span data-ttu-id="09d5e-175">Per informazioni sugli schemi di architettura dati comuni delle applicazioni di database multi-tenant software come un servizio (SaaS), vedere [Schemi progettuali per applicazioni SaaS multi-tenant con il database SQL di Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="09d5e-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span>

## <a name="questions-and-feature-requests"></a><span data-ttu-id="09d5e-176">Domande e richieste di funzionalità</span><span class="sxs-lookup"><span data-stu-id="09d5e-176">Questions and Feature Requests</span></span>
<span data-ttu-id="09d5e-177">Se ci sono domande, è possibile visitare il [forum sul database SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) mentre è possibile inserire le richieste di nuove funzionalità nel [forum relativo a commenti e suggerimenti sul database SQL](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="09d5e-177">For questions, please reach out to us on the [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them to the [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

