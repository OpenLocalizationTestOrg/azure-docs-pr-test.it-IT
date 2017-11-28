---
title: aaaMigrate esistente database tooscale-out | Documenti Microsoft
description: Convertire gli strumenti di database elastico toouse database partizionati mediante la creazione di un gestore mappe partizioni
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
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a><span data-ttu-id="74516-103">Eseguire la migrazione di database esistente tooscale-out</span><span class="sxs-lookup"><span data-stu-id="74516-103">Migrate existing databases tooscale-out</span></span>
<span data-ttu-id="74516-104">Gestire facilmente i database partizionati esistenti di scalabilità orizzontale utilizzando gli strumenti di database di Database SQL di Azure (ad esempio hello [libreria client di Database elastico](sql-database-elastic-database-client-library.md)).</span><span class="sxs-lookup"><span data-stu-id="74516-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as hello [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> <span data-ttu-id="74516-105">È prima necessario convertire un set esistente di hello toouse database [gestore mappe partizioni](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="74516-105">You must first convert an existing set of databases toouse hello [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="74516-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="74516-106">Overview</span></span>
<span data-ttu-id="74516-107">toomigrate un database partizionato esistente:</span><span class="sxs-lookup"><span data-stu-id="74516-107">toomigrate an existing sharded database:</span></span> 

1. <span data-ttu-id="74516-108">Preparare hello [il database di gestione di partizioni mapping](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="74516-108">Prepare hello [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span></span>
2. <span data-ttu-id="74516-109">Creare una mappa partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="74516-109">Create hello shard map.</span></span>
3. <span data-ttu-id="74516-110">Preparare singole partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="74516-110">Prepare hello individual shards.</span></span>  
4. <span data-ttu-id="74516-111">Aggiungere una mappa partizioni toohello di mapping.</span><span class="sxs-lookup"><span data-stu-id="74516-111">Add mappings toohello shard map.</span></span>

<span data-ttu-id="74516-112">Queste tecniche possono essere implementate usando entrambi hello [libreria client .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), o gli script di PowerShell hello trovato in [database SQL di Azure - script di strumenti di Database elastico](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="74516-112">These techniques can be implemented using either hello [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or hello PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span> <span data-ttu-id="74516-113">di seguito esempi di Hello utilizzano gli script di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="74516-113">hello examples here use hello PowerShell scripts.</span></span>

<span data-ttu-id="74516-114">Per ulteriori informazioni su hello ShardMapManager, vedere [gestione mappa partizioni](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="74516-114">For more information about hello ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="74516-115">Per una panoramica degli strumenti di database elastico hello, vedere [panoramica sulle funzionalità di Database elastico](sql-database-elastic-scale-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="74516-115">For an overview of hello elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span></span>

## <a name="prepare-hello-shard-map-manager-database"></a><span data-ttu-id="74516-116">Preparare il database di gestione di hello partizioni mappa</span><span class="sxs-lookup"><span data-stu-id="74516-116">Prepare hello shard map manager database</span></span>
<span data-ttu-id="74516-117">gestore mappe partizioni di Hello è un database speciale che contiene i database di scalabilità orizzontale di hello dati toomanage.</span><span class="sxs-lookup"><span data-stu-id="74516-117">hello shard map manager is a special database that contains hello data toomanage scaled-out databases.</span></span> <span data-ttu-id="74516-118">È possibile usare un database esistente o crearne un nuovo.</span><span class="sxs-lookup"><span data-stu-id="74516-118">You can use an existing database, or create a new database.</span></span> <span data-ttu-id="74516-119">Si noti che un database che funge da gestore mappe partizioni non deve essere hello stesso database come una partizione.</span><span class="sxs-lookup"><span data-stu-id="74516-119">Note that a database acting as shard map manager should not be hello same database as a shard.</span></span> <span data-ttu-id="74516-120">Si noti inoltre che uno script di PowerShell hello non crea database hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="74516-120">Also note that hello PowerShell script does not create hello database for you.</span></span> 

## <a name="step-1-create-a-shard-map-manager"></a><span data-ttu-id="74516-121">Passaggio 1: Creare un gestore mappe partizioni</span><span class="sxs-lookup"><span data-stu-id="74516-121">Step 1: create a shard map manager</span></span>
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a><span data-ttu-id="74516-122">gestore mappe partizioni di hello tooretrieve</span><span class="sxs-lookup"><span data-stu-id="74516-122">tooretrieve hello shard map manager</span></span>
<span data-ttu-id="74516-123">Dopo la creazione, è possibile recuperare gestore mappe partizioni di hello con questo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="74516-123">After creation, you can retrieve hello shard map manager with this cmdlet.</span></span> <span data-ttu-id="74516-124">Questo passaggio è necessario ogni volta che è necessario toouse hello ShardMapManager oggetto.</span><span class="sxs-lookup"><span data-stu-id="74516-124">This step is needed every time you need toouse hello ShardMapManager object.</span></span>

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a><span data-ttu-id="74516-125">Passaggio 2: creare una mappa partizioni hello</span><span class="sxs-lookup"><span data-stu-id="74516-125">Step 2: create hello shard map</span></span>
<span data-ttu-id="74516-126">È necessario selezionare il tipo di hello di toocreate mappa partizioni.</span><span class="sxs-lookup"><span data-stu-id="74516-126">You must select hello type of shard map toocreate.</span></span> <span data-ttu-id="74516-127">scelta di Hello dipende dall'architettura di database hello:</span><span class="sxs-lookup"><span data-stu-id="74516-127">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="74516-128">Single-tenant per ogni database (per i termini, vedere hello [glossario](sql-database-elastic-scale-glossary.md).)</span><span class="sxs-lookup"><span data-stu-id="74516-128">Single tenant per database (For terms, see hello [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
2. <span data-ttu-id="74516-129">Più tenant per database (due tipi):</span><span class="sxs-lookup"><span data-stu-id="74516-129">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="74516-130">Mapping di tipo elenco</span><span class="sxs-lookup"><span data-stu-id="74516-130">List mapping</span></span>
   2. <span data-ttu-id="74516-131">Mapping di tipo intervallo</span><span class="sxs-lookup"><span data-stu-id="74516-131">Range mapping</span></span>

<span data-ttu-id="74516-132">Per un modello a singolo tenant, creare una mappa partizioni con **mapping di tipo elenco** .</span><span class="sxs-lookup"><span data-stu-id="74516-132">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="74516-133">modello single-tenant Hello assegna a un database per ogni tenant.</span><span class="sxs-lookup"><span data-stu-id="74516-133">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="74516-134">Si tratta di un modello efficace per gli sviluppatori SaaS in quanto semplifica la gestione.</span><span class="sxs-lookup"><span data-stu-id="74516-134">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Mapping di tipo elenco][1]

<span data-ttu-id="74516-136">modello multi-tenant Hello assegna diversi tenant tooa singolo database ed è possibile distribuire i gruppi di tenant tra più database.</span><span class="sxs-lookup"><span data-stu-id="74516-136">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="74516-137">Utilizzare questo modello quando si prevede che necessita di dati di dimensioni ridotte di toohave ogni tenant.</span><span class="sxs-lookup"><span data-stu-id="74516-137">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="74516-138">In questo modello viene assegnato un intervallo di tenant tooa database utilizzando **mapping intervallo**.</span><span class="sxs-lookup"><span data-stu-id="74516-138">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![Mapping di tipo intervallo][2]

<span data-ttu-id="74516-140">Oppure è possibile implementare un modello di database multi-tenant utilizzando un *mapping elenco* tooassign più singolo database tooa tenant.</span><span class="sxs-lookup"><span data-stu-id="74516-140">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="74516-141">Ad esempio, DB1 viene utilizzato toostore informazioni sull'id tenant 1 e 5 e DB2 archivia i dati di 10 di tenant e tenant 7.</span><span class="sxs-lookup"><span data-stu-id="74516-141">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Tenant multipli su database singolo][3] 

<span data-ttu-id="74516-143">**In base alla scelta effettuata, procedere con una delle opzioni seguenti:**</span><span class="sxs-lookup"><span data-stu-id="74516-143">**Based on your choice, choose one of these options:**</span></span>

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a><span data-ttu-id="74516-144">Opzione 1: creare una mappa partizioni per un mapping di tipo elenco</span><span class="sxs-lookup"><span data-stu-id="74516-144">Option 1: create a shard map for a list mapping</span></span>
<span data-ttu-id="74516-145">Creare una mappa partizioni utilizzando hello ShardMapManager oggetto.</span><span class="sxs-lookup"><span data-stu-id="74516-145">Create a shard map using hello ShardMapManager object.</span></span> 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a><span data-ttu-id="74516-146">Opzione 2: creare una mappa partizioni per un mapping di tipo intervallo</span><span class="sxs-lookup"><span data-stu-id="74516-146">Option 2: create a shard map for a range mapping</span></span>
<span data-ttu-id="74516-147">Si noti che tooutilize questo schema di mapping, i valori di id tenant deve intervalli continui toobe e toohave accettabile gap negli intervalli hello è semplicemente ignorando intervallo hello quando si creano database hello.</span><span class="sxs-lookup"><span data-stu-id="74516-147">Note that tooutilize this mapping pattern, tenant id values needs toobe continuous ranges, and it is acceptable toohave gap in hello ranges by simply skipping hello range when creating hello databases.</span></span>

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a><span data-ttu-id="74516-148">Opzione 3: eseguire il mapping di tipo elenco in un database singolo</span><span class="sxs-lookup"><span data-stu-id="74516-148">Option 3: List mappings on a single database</span></span>
<span data-ttu-id="74516-149">Per l'impostazione di questo modello è necessario anche creare una mappa di tipo elenco, come illustrato nel passaggio 2, opzione 1.</span><span class="sxs-lookup"><span data-stu-id="74516-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span></span>

## <a name="step-3-prepare-individual-shards"></a><span data-ttu-id="74516-150">Passaggio 3: preparare le singole partizioni</span><span class="sxs-lookup"><span data-stu-id="74516-150">Step 3: Prepare individual shards</span></span>
<span data-ttu-id="74516-151">Aggiungere ogni gestore mappe partizioni di partizioni (database) toohello.</span><span class="sxs-lookup"><span data-stu-id="74516-151">Add each shard (database) toohello shard map manager.</span></span> <span data-ttu-id="74516-152">Questa funzione prepara i singoli database hello per archiviare le informazioni di mapping.</span><span class="sxs-lookup"><span data-stu-id="74516-152">This prepares hello individual databases for storing mapping information.</span></span> <span data-ttu-id="74516-153">Eseguire questo metodo su ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="74516-153">Execute this method on each shard.</span></span>

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a><span data-ttu-id="74516-154">Passaggio 4: aggiungere mapping</span><span class="sxs-lookup"><span data-stu-id="74516-154">Step 4: Add mappings</span></span>
<span data-ttu-id="74516-155">aggiunta di Hello di mapping dipende dal tipo di hello di mappa partizioni che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="74516-155">hello addition of mappings depends on hello kind of shard map you created.</span></span> <span data-ttu-id="74516-156">Se è stata creata una mappa di tipo elenco, aggiungere mapping di tipo elenco.</span><span class="sxs-lookup"><span data-stu-id="74516-156">If you created a list map, you add list mappings.</span></span> <span data-ttu-id="74516-157">Se è stata creata una mappa di tipo intervallo, aggiungere mapping di tipo intervallo.</span><span class="sxs-lookup"><span data-stu-id="74516-157">If you created a range map, you add range mappings.</span></span>

### <a name="option-1-map-hello-data-for-a-list-mapping"></a><span data-ttu-id="74516-158">Opzione 1: eseguire il mapping hello dati per il mapping di un elenco</span><span class="sxs-lookup"><span data-stu-id="74516-158">Option 1: map hello data for a list mapping</span></span>
<span data-ttu-id="74516-159">Eseguire il mapping hello dati aggiungendo un mapping di elenco per ogni tenant.</span><span class="sxs-lookup"><span data-stu-id="74516-159">Map hello data by adding a list mapping for each tenant.</span></span>  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a><span data-ttu-id="74516-160">Opzione 2: eseguire il mapping hello dati per il mapping di un intervallo</span><span class="sxs-lookup"><span data-stu-id="74516-160">Option 2: map hello data for a range mapping</span></span>
<span data-ttu-id="74516-161">Aggiungere i mapping di intervallo hello per tutti i hello tenant intervallo per l'id, le associazioni di database:</span><span class="sxs-lookup"><span data-stu-id="74516-161">Add hello range mappings for all hello tenant id range - database associations:</span></span>

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a><span data-ttu-id="74516-162">Passaggio 4 opzione 3: eseguire il mapping hello dati a più tenant su un singolo database</span><span class="sxs-lookup"><span data-stu-id="74516-162">Step 4 option 3: map hello data for multiple tenants on a single database</span></span>
<span data-ttu-id="74516-163">Per ogni tenant, eseguire Add-ListMapping hello (opzione 1, sopra).</span><span class="sxs-lookup"><span data-stu-id="74516-163">For each tenant, run hello Add-ListMapping (option 1, above).</span></span> 

## <a name="checking-hello-mappings"></a><span data-ttu-id="74516-164">Verifica mapping hello</span><span class="sxs-lookup"><span data-stu-id="74516-164">Checking hello mappings</span></span>
<span data-ttu-id="74516-165">Informazioni sulle partizioni esistenti hello e mapping hello associate possono eseguire una query utilizzando i seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="74516-165">Information about hello existing shards and hello mappings associated with them can be queried using following commands:</span></span>  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a><span data-ttu-id="74516-166">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="74516-166">Summary</span></span>
<span data-ttu-id="74516-167">Dopo aver completato l'installazione di hello, è possibile iniziare libreria client di Database elastico hello toouse.</span><span class="sxs-lookup"><span data-stu-id="74516-167">Once you have completed hello setup, you can begin toouse hello Elastic Database client library.</span></span> <span data-ttu-id="74516-168">È anche possibile usare il [routing dipendente dai dati](sql-database-elastic-scale-data-dependent-routing.md) e le [query su più partizioni](sql-database-elastic-scale-multishard-querying.md).</span><span class="sxs-lookup"><span data-stu-id="74516-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="74516-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="74516-169">Next steps</span></span>
<span data-ttu-id="74516-170">Ottenere gli script di PowerShell hello da [Database elastica di database SQL di Azure strumenti sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="74516-170">Get hello PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

<span data-ttu-id="74516-171">gli strumenti di Hello sono anche in GitHub: [/elastica-db-strumenti di Azure](https://github.com/Azure/elastic-db-tools).</span><span class="sxs-lookup"><span data-stu-id="74516-171">hello tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span></span>

<span data-ttu-id="74516-172">Utilizzare hello dello strumento di merge di divisione toomove dati tooor da un modello di modello multi-tenant tooa single-tenant.</span><span class="sxs-lookup"><span data-stu-id="74516-172">Use hello split-merge tool toomove data tooor from a multi-tenant model tooa single tenant model.</span></span> <span data-ttu-id="74516-173">Vedere la pagina relativa allo [strumento di divisione-unione](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="74516-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="74516-174">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="74516-174">Additional resources</span></span>
<span data-ttu-id="74516-175">Per informazioni sugli schemi di architettura dati comuni delle applicazioni di database multi-tenant software come un servizio (SaaS), vedere [Schemi progettuali per applicazioni SaaS multi-tenant con il database SQL di Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="74516-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span>

## <a name="questions-and-feature-requests"></a><span data-ttu-id="74516-176">Domande e richieste di funzionalità</span><span class="sxs-lookup"><span data-stu-id="74516-176">Questions and Feature Requests</span></span>
<span data-ttu-id="74516-177">Per domande, rivolgersi toous su hello [forum di Database SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) e per le richieste di funzionalità, aggiungerli toohello [forum sul feedback su Database SQL](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="74516-177">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

