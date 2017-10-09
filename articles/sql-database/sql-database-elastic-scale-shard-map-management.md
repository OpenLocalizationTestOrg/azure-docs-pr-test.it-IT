---
title: aaaScale un database SQL di Azure | Documenti Microsoft
description: Come toouse hello ShardMapManager, libreria client di database elastico
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a><span data-ttu-id="a68cc-103">Scalabilità orizzontale di database con gestore mappe partizioni di hello</span><span class="sxs-lookup"><span data-stu-id="a68cc-103">Scale out databases with hello shard map manager</span></span>
<span data-ttu-id="a68cc-104">scalabilità orizzontale tooeasily database in SQL Azure, utilizzare un gestore mappe partizioni.</span><span class="sxs-lookup"><span data-stu-id="a68cc-104">tooeasily scale out databases on SQL Azure, use a shard map manager.</span></span> <span data-ttu-id="a68cc-105">gestore mappe partizioni di Hello è un database speciale che gestisce le informazioni di mapping globale su tutte le partizioni (database) in un set di partizioni.</span><span class="sxs-lookup"><span data-stu-id="a68cc-105">hello shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span></span> <span data-ttu-id="a68cc-106">Hello metadati consentono a un database dell'applicazione tooconnect toohello corretto in base al valore di hello di hello **chiave di partizionamento orizzontale**.</span><span class="sxs-lookup"><span data-stu-id="a68cc-106">hello metadata allows an application tooconnect toohello correct database based upon hello value of hello **sharding key**.</span></span> <span data-ttu-id="a68cc-107">Inoltre, ogni partizione nel set di hello contiene le mappe che tengono traccia dei dati di partizione locale hello (noto come **shardlet**).</span><span class="sxs-lookup"><span data-stu-id="a68cc-107">In addition, every shard in hello set contains maps that track hello local shard data (known as **shardlets**).</span></span> 

![Gestione mappe partizioni](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

<span data-ttu-id="a68cc-109">Informazioni sulle modalità di costruzione queste mappe è Gestione mappa tooshard essenziali.</span><span class="sxs-lookup"><span data-stu-id="a68cc-109">Understanding how these maps are constructed is essential tooshard map management.</span></span> <span data-ttu-id="a68cc-110">Questa operazione viene eseguita utilizzando hello [ShardMapManager classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), trovato in hello [libreria client di Database elastico](sql-database-elastic-database-client-library.md) toomanage partizione viene mappata.</span><span class="sxs-lookup"><span data-stu-id="a68cc-110">This is done using hello [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in hello [Elastic Database client library](sql-database-elastic-database-client-library.md) toomanage shard maps.</span></span>  

## <a name="shard-maps-and-shard-mappings"></a><span data-ttu-id="a68cc-111">Mappe partizioni e mapping di partizioni</span><span class="sxs-lookup"><span data-stu-id="a68cc-111">Shard maps and shard mappings</span></span>
<span data-ttu-id="a68cc-112">Per ogni partizione, è necessario selezionare il tipo di hello di toocreate mappa partizioni.</span><span class="sxs-lookup"><span data-stu-id="a68cc-112">For each shard, you must select hello type of shard map toocreate.</span></span> <span data-ttu-id="a68cc-113">scelta di Hello dipende dall'architettura di database hello:</span><span class="sxs-lookup"><span data-stu-id="a68cc-113">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="a68cc-114">Singolo tenant per database</span><span class="sxs-lookup"><span data-stu-id="a68cc-114">Single tenant per database</span></span>  
2. <span data-ttu-id="a68cc-115">Più tenant per database (due tipi):</span><span class="sxs-lookup"><span data-stu-id="a68cc-115">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="a68cc-116">Mapping di tipo elenco</span><span class="sxs-lookup"><span data-stu-id="a68cc-116">List mapping</span></span>
   2. <span data-ttu-id="a68cc-117">Mapping di tipo intervallo</span><span class="sxs-lookup"><span data-stu-id="a68cc-117">Range mapping</span></span>

<span data-ttu-id="a68cc-118">Per un modello a singolo tenant, creare una mappa partizioni con **mapping di tipo elenco** .</span><span class="sxs-lookup"><span data-stu-id="a68cc-118">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="a68cc-119">modello single-tenant Hello assegna a un database per ogni tenant.</span><span class="sxs-lookup"><span data-stu-id="a68cc-119">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="a68cc-120">Si tratta di un modello efficace per gli sviluppatori SaaS in quanto semplifica la gestione.</span><span class="sxs-lookup"><span data-stu-id="a68cc-120">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Mapping di tipo elenco][1]

<span data-ttu-id="a68cc-122">modello multi-tenant Hello assegna diversi tenant tooa singolo database ed è possibile distribuire i gruppi di tenant tra più database.</span><span class="sxs-lookup"><span data-stu-id="a68cc-122">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="a68cc-123">Utilizzare questo modello quando si prevede che necessita di dati di dimensioni ridotte di toohave ogni tenant.</span><span class="sxs-lookup"><span data-stu-id="a68cc-123">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="a68cc-124">In questo modello viene assegnato un intervallo di tenant tooa database utilizzando **mapping intervallo**.</span><span class="sxs-lookup"><span data-stu-id="a68cc-124">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![Mapping di tipo intervallo][2]

<span data-ttu-id="a68cc-126">Oppure è possibile implementare un modello di database multi-tenant utilizzando un *mapping elenco* tooassign più singolo database tooa tenant.</span><span class="sxs-lookup"><span data-stu-id="a68cc-126">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="a68cc-127">Ad esempio, DB1 viene utilizzato toostore informazioni sull'id tenant 1 e 5 e DB2 archivia i dati di 10 di tenant e tenant 7.</span><span class="sxs-lookup"><span data-stu-id="a68cc-127">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Tenant multipli su database singolo][3] 

### <a name="supported-net-types-for-sharding-keys"></a><span data-ttu-id="a68cc-129">Tipi .NET supportati per le chiavi di partizionamento orizzontale</span><span class="sxs-lookup"><span data-stu-id="a68cc-129">Supported .Net types for sharding keys</span></span>
<span data-ttu-id="a68cc-130">Hello di supporto scala elastica seguenti di .net Framework i tipi come chiavi di partizionamento orizzontale:</span><span class="sxs-lookup"><span data-stu-id="a68cc-130">Elastic Scale support hello following .Net Framework types as sharding keys:</span></span>

* <span data-ttu-id="a68cc-131">numero intero</span><span class="sxs-lookup"><span data-stu-id="a68cc-131">integer</span></span>
* <span data-ttu-id="a68cc-132">long</span><span class="sxs-lookup"><span data-stu-id="a68cc-132">long</span></span>
* <span data-ttu-id="a68cc-133">guid</span><span class="sxs-lookup"><span data-stu-id="a68cc-133">guid</span></span>
* <span data-ttu-id="a68cc-134">byte[]</span><span class="sxs-lookup"><span data-stu-id="a68cc-134">byte[]</span></span>  
* <span data-ttu-id="a68cc-135">datetime</span><span class="sxs-lookup"><span data-stu-id="a68cc-135">datetime</span></span>
* <span data-ttu-id="a68cc-136">timespan</span><span class="sxs-lookup"><span data-stu-id="a68cc-136">timespan</span></span>
* <span data-ttu-id="a68cc-137">datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="a68cc-137">datetimeoffset</span></span>

### <a name="list-and-range-shard-maps"></a><span data-ttu-id="a68cc-138">Mappe partizioni di tipo elenco e intervallo</span><span class="sxs-lookup"><span data-stu-id="a68cc-138">List and range shard maps</span></span>
<span data-ttu-id="a68cc-139">Le mappe partizioni possono essere create usando **elenchi di singoli valori di chiavi di partizionamento orizzontale** oppure tramite **intervalli di valori di chiavi di partizionamento orizzontale**.</span><span class="sxs-lookup"><span data-stu-id="a68cc-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span></span> 

### <a name="list-shard-maps"></a><span data-ttu-id="a68cc-140">Mappe partizioni di tipo elenco</span><span class="sxs-lookup"><span data-stu-id="a68cc-140">List shard maps</span></span>
<span data-ttu-id="a68cc-141">**Partizioni** contengono **shardlet** e mapping hello di shardlet tooshards è gestito da una mappa partizioni.</span><span class="sxs-lookup"><span data-stu-id="a68cc-141">**Shards** contain **shardlets** and hello mapping of shardlets tooshards is maintained by a shard map.</span></span> <span data-ttu-id="a68cc-142">Oggetto **mappa partizioni elenco** è un'associazione tra hello singoli valori di chiave che identificano gli shardlet hello e database hello che fungono da partizioni.</span><span class="sxs-lookup"><span data-stu-id="a68cc-142">A **list shard map** is an association between hello individual key values that identify hello shardlets and hello databases that serve as shards.</span></span>  <span data-ttu-id="a68cc-143">**Elenca i mapping** , esplicite e diversi valori di chiave possono essere mappato toohello dello stesso database.</span><span class="sxs-lookup"><span data-stu-id="a68cc-143">**List mappings** are explicit and different key values can be mapped toohello same database.</span></span> <span data-ttu-id="a68cc-144">Ad esempio, viene eseguito il mapping A tooDatabase chiave 1 e B. Database fanno riferimento a valori di chiave, 3 e 6</span><span class="sxs-lookup"><span data-stu-id="a68cc-144">For example, key 1 maps tooDatabase A, and key values 3 and 6 both reference Database B.</span></span>

| <span data-ttu-id="a68cc-145">Chiave</span><span class="sxs-lookup"><span data-stu-id="a68cc-145">Key</span></span> | <span data-ttu-id="a68cc-146">Percorso della partizione</span><span class="sxs-lookup"><span data-stu-id="a68cc-146">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="a68cc-147">1</span><span class="sxs-lookup"><span data-stu-id="a68cc-147">1</span></span> |<span data-ttu-id="a68cc-148">Database_A</span><span class="sxs-lookup"><span data-stu-id="a68cc-148">Database_A</span></span> |
| <span data-ttu-id="a68cc-149">3</span><span class="sxs-lookup"><span data-stu-id="a68cc-149">3</span></span> |<span data-ttu-id="a68cc-150">Database_B</span><span class="sxs-lookup"><span data-stu-id="a68cc-150">Database_B</span></span> |
| <span data-ttu-id="a68cc-151">4</span><span class="sxs-lookup"><span data-stu-id="a68cc-151">4</span></span> |<span data-ttu-id="a68cc-152">Database_C</span><span class="sxs-lookup"><span data-stu-id="a68cc-152">Database_C</span></span> |
| <span data-ttu-id="a68cc-153">6</span><span class="sxs-lookup"><span data-stu-id="a68cc-153">6</span></span> |<span data-ttu-id="a68cc-154">Database_B</span><span class="sxs-lookup"><span data-stu-id="a68cc-154">Database_B</span></span> |
| <span data-ttu-id="a68cc-155">...</span><span class="sxs-lookup"><span data-stu-id="a68cc-155">...</span></span> |<span data-ttu-id="a68cc-156">...</span><span class="sxs-lookup"><span data-stu-id="a68cc-156">...</span></span> |

### <a name="range-shard-maps"></a><span data-ttu-id="a68cc-157">Mappa partizioni di tipo intervallo</span><span class="sxs-lookup"><span data-stu-id="a68cc-157">Range shard maps</span></span>
<span data-ttu-id="a68cc-158">In un **mappa partizioni intervallo**, intervalli di chiavi hello sono descritto da una coppia **[valore ridotto, valore massimo)** dove hello *valore ridotto* hello chiave minimo nell'intervallo hello e hello *Valore elevato* hello primo valore più elevato intervallo hello.</span><span class="sxs-lookup"><span data-stu-id="a68cc-158">In a **range shard map**, hello key range is described by a pair **[Low Value, High Value)** where hello *Low Value* is hello minimum key in hello range, and hello *High Value* is hello first value higher than hello range.</span></span> 

<span data-ttu-id="a68cc-159">Ad esempio, **[0, 100)** include tutti i numeri interi superiori o uguali a 0 e inferiori a 100.</span><span class="sxs-lookup"><span data-stu-id="a68cc-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span></span> <span data-ttu-id="a68cc-160">Si noti che sono supportati più intervalli può punto toohello stesso database e non contiguo di intervalli (ad esempio, [100,200) e [400,600) entrambi C punto tooDatabase nel seguente esempio hello.)</span><span class="sxs-lookup"><span data-stu-id="a68cc-160">Note that multiple ranges can point toohello same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point tooDatabase C in hello example below.)</span></span>

| <span data-ttu-id="a68cc-161">Chiave</span><span class="sxs-lookup"><span data-stu-id="a68cc-161">Key</span></span> | <span data-ttu-id="a68cc-162">Percorso della partizione</span><span class="sxs-lookup"><span data-stu-id="a68cc-162">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="a68cc-163">[1, 50)</span><span class="sxs-lookup"><span data-stu-id="a68cc-163">[1,50)</span></span> |<span data-ttu-id="a68cc-164">Database_A</span><span class="sxs-lookup"><span data-stu-id="a68cc-164">Database_A</span></span> |
| <span data-ttu-id="a68cc-165">[50, 100)</span><span class="sxs-lookup"><span data-stu-id="a68cc-165">[50,100)</span></span> |<span data-ttu-id="a68cc-166">Database_B</span><span class="sxs-lookup"><span data-stu-id="a68cc-166">Database_B</span></span> |
| <span data-ttu-id="a68cc-167">[100, 200)</span><span class="sxs-lookup"><span data-stu-id="a68cc-167">[100,200)</span></span> |<span data-ttu-id="a68cc-168">Database_C</span><span class="sxs-lookup"><span data-stu-id="a68cc-168">Database_C</span></span> |
| <span data-ttu-id="a68cc-169">[400, 600)</span><span class="sxs-lookup"><span data-stu-id="a68cc-169">[400,600)</span></span> |<span data-ttu-id="a68cc-170">Database_C</span><span class="sxs-lookup"><span data-stu-id="a68cc-170">Database_C</span></span> |
| <span data-ttu-id="a68cc-171">...</span><span class="sxs-lookup"><span data-stu-id="a68cc-171">...</span></span> |<span data-ttu-id="a68cc-172">...</span><span class="sxs-lookup"><span data-stu-id="a68cc-172">...</span></span> |

<span data-ttu-id="a68cc-173">Ognuna delle tabelle di hello illustrate sopra è riportato un esempio concettuale di un **ShardMap** oggetto.</span><span class="sxs-lookup"><span data-stu-id="a68cc-173">Each of hello tables shown above is a conceptual example of a **ShardMap** object.</span></span> <span data-ttu-id="a68cc-174">Ogni riga è un esempio semplificato dell'individuo **PointMapping** (per la mappa di partizioni elenco hello) o **RangeMapping** (per la mappa di partizioni intervallo hello) oggetto.</span><span class="sxs-lookup"><span data-stu-id="a68cc-174">Each row is a simplified example of an individual **PointMapping** (for hello list shard map) or **RangeMapping** (for hello range shard map) object.</span></span>

## <a name="shard-map-manager"></a><span data-ttu-id="a68cc-175">Gestore mappe partizioni</span><span class="sxs-lookup"><span data-stu-id="a68cc-175">Shard map manager</span></span>
<span data-ttu-id="a68cc-176">Nella libreria client hello, gestore mappe partizioni di hello è una raccolta di mappe partizioni.</span><span class="sxs-lookup"><span data-stu-id="a68cc-176">In hello client library, hello shard map  manager is a collection of shard maps.</span></span> <span data-ttu-id="a68cc-177">Hello dati gestiti da un **ShardMapManager** istanza viene mantenuta in tre posizioni:</span><span class="sxs-lookup"><span data-stu-id="a68cc-177">hello data managed by a **ShardMapManager** instance is kept in three places:</span></span> 

1. <span data-ttu-id="a68cc-178">**Mappa di partizioni globali (GSM)**: specificare un tooserve database come repository hello per tutte le mappe partizioni e i mapping.</span><span class="sxs-lookup"><span data-stu-id="a68cc-178">**Global Shard Map (GSM)**: You specify a database tooserve as hello repository for all of its shard maps and mappings.</span></span> <span data-ttu-id="a68cc-179">Stored procedure e tabelle speciali vengono create automaticamente le informazioni di hello toomanage.</span><span class="sxs-lookup"><span data-stu-id="a68cc-179">Special tables and stored procedures are automatically created toomanage hello information.</span></span> <span data-ttu-id="a68cc-180">Questo è in genere un database di piccole dimensioni e leggermente accessibili e non deve essere usato per altre esigenze di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a68cc-180">This is typically a small database and lightly accessed, and it should not be used for other needs of hello application.</span></span> <span data-ttu-id="a68cc-181">salve le tabelle sono in uno schema speciale denominato **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="a68cc-181">hello tables are in a special schema named **__ShardManagement**.</span></span> 
2. <span data-ttu-id="a68cc-182">**Mappa di partizioni locali (LSM)**: ogni database che si specifica una partizione è toobe modificato toocontain diverse tabelle di piccole dimensioni e stored procedure speciale che contengono e gestire partizioni di toothat specifiche informazioni mappa partizioni.</span><span class="sxs-lookup"><span data-stu-id="a68cc-182">**Local Shard Map (LSM)**: Every database that you specify toobe a shard is modified toocontain several small tables and special stored procedures that contain and manage shard map information specific toothat shard.</span></span> <span data-ttu-id="a68cc-183">Queste informazioni sono ridondanti con informazioni hello in GSM hello e consente le informazioni sulla mappa partizioni hello applicazione toovalidate memorizzati nella cache senza porre alcun carico sul hello GSM; un'applicazione Hello utilizza hello LSM toodetermine se un mapping memorizzati nella cache è ancora valido.</span><span class="sxs-lookup"><span data-stu-id="a68cc-183">This information is redundant with hello information in hello GSM, and it allows hello application toovalidate cached shard map information without placing any load on hello GSM; hello application uses hello LSM toodetermine if a cached mapping is still valid.</span></span> <span data-ttu-id="a68cc-184">Hello tabelle corrispondente toohello LSM in ogni partizione sono anche nello schema hello **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="a68cc-184">hello tables corresponding toohello LSM on each shard are also in hello schema **__ShardManagement**.</span></span>
3. <span data-ttu-id="a68cc-185">**Cache dell'applicazione**: ogni istanza di applicazione che accede a un oggetto **ShardMapManager** gestisce una cache in memoria locale dei rispettivi mapping,</span><span class="sxs-lookup"><span data-stu-id="a68cc-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span></span> <span data-ttu-id="a68cc-186">in cui vengono archiviate le informazioni di routing appena recuperate.</span><span class="sxs-lookup"><span data-stu-id="a68cc-186">It stores routing information that has recently been retrieved.</span></span> 

## <a name="constructing-a-shardmapmanager"></a><span data-ttu-id="a68cc-187">Creazione di un oggetto ShardMapManager</span><span class="sxs-lookup"><span data-stu-id="a68cc-187">Constructing a ShardMapManager</span></span>
<span data-ttu-id="a68cc-188">Un oggetto **ShardMapManager** viene creato con un modello [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a68cc-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span></span> <span data-ttu-id="a68cc-189">Hello  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  accetta le credenziali (nome del server hello e nome del database contenente hello GSM inclusi) in formato hello un  **ConnectionString** e restituisce un'istanza di un **ShardMapManager**.</span><span class="sxs-lookup"><span data-stu-id="a68cc-189">hello **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including hello server name and database name holding hello GSM) in hello form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span></span>  

<span data-ttu-id="a68cc-190">**Nota:** hello **ShardMapManager** deve essere creata un'istanza solo una volta per ogni dominio applicazione, all'interno di codice di inizializzazione hello per un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a68cc-190">**Please Note:** hello **ShardMapManager** should be instantiated only once per app domain, within hello initialization code for an application.</span></span> <span data-ttu-id="a68cc-191">Creazione di istanze aggiuntive di ShardMapManager in hello stesso appdomain, comporterà un aumento della memoria e di utilizzo della CPU di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="a68cc-191">Creation of additional instances of ShardMapManager in hello same appdomain, will result in increased memory and CPU utilization of hello application.</span></span> <span data-ttu-id="a68cc-192">Un oggetto **ShardMapManager** può includere un numero qualsiasi di mappe partizioni.</span><span class="sxs-lookup"><span data-stu-id="a68cc-192">A **ShardMapManager** can contain any number of shard maps.</span></span> <span data-ttu-id="a68cc-193">Anche se è possibile che una singola mappa partizioni sia sufficiente per molte applicazioni, in alcune situazioni vengono usati diversi set di database per schemi diversi o per finalità specifiche. In questi casi è preferibile usare più mappe partizioni.</span><span class="sxs-lookup"><span data-stu-id="a68cc-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span></span> 

<span data-ttu-id="a68cc-194">In questo codice, un'applicazione prova tooopen esistente **ShardMapManager** con hello [TryGetSqlShardMapManager metodo](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="a68cc-194">In this code, an application tries tooopen an existing **ShardMapManager** with hello [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span></span>  <span data-ttu-id="a68cc-195">Se gli oggetti che rappresentano un Global **ShardMapManager** (GSM) non sono ancora presenti all'interno del database di hello, libreria client hello vengono create sono utilizzando hello [CreateSqlShardMapManager metodo](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="a68cc-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside hello database, hello client library creates them there using hello [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span></span>

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

<span data-ttu-id="a68cc-196">In alternativa, è possibile utilizzare Powershell toocreate un nuovo gestore mappe partizioni.</span><span class="sxs-lookup"><span data-stu-id="a68cc-196">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="a68cc-197">Un esempio è disponibile [qui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="a68cc-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="get-a-rangeshardmap-or-listshardmap"></a><span data-ttu-id="a68cc-198">Ottenere una mappa RangeShardMap o ListShardMap</span><span class="sxs-lookup"><span data-stu-id="a68cc-198">Get a RangeShardMap or ListShardMap</span></span>
<span data-ttu-id="a68cc-199">Dopo aver creato una partizione gestore mappe, è possibile ottenere hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) o [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) utilizzando hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), o hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) metodo.</span><span class="sxs-lookup"><span data-stu-id="a68cc-199">After creating a shard map manager, you can get hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span>

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a><span data-ttu-id="a68cc-200">Credenziali di amministrazione delle mappe partizioni</span><span class="sxs-lookup"><span data-stu-id="a68cc-200">Shard map administration credentials</span></span>
<span data-ttu-id="a68cc-201">Le applicazioni che amministrano e modificare mappe partizioni sono diverse da quelli che utilizzano connessioni di tooroute mappe partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="a68cc-201">Applications that administer and manipulate shard maps are different from those that use hello shard maps tooroute connections.</span></span> 

<span data-ttu-id="a68cc-202">esegue il mapping di partizione tooadminister (aggiungere o modificare partizioni, mappe partizioni, i mapping delle partizioni, e così via) è necessario creare un'istanza di hello **ShardMapManager** utilizzando **le credenziali che dispongono di lettura/scrittura privilegi entrambi database GSM hello e in ogni database che funge da una partizione**.</span><span class="sxs-lookup"><span data-stu-id="a68cc-202">tooadminister shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate hello **ShardMapManager** using **credentials that have read/write privileges on both hello GSM database and on each database that serves as a shard**.</span></span> <span data-ttu-id="a68cc-203">le credenziali di Hello devono consentire di scritture su tabelle di hello entrambi hello GSM e LSM come informazioni relative alla mappa partizioni è inseriti o modificati, nonché per la creazione di tabelle LSM in nuove partizioni.</span><span class="sxs-lookup"><span data-stu-id="a68cc-203">hello credentials must allow for writes against hello tables in both hello GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span></span>  

<span data-ttu-id="a68cc-204">Vedere [utilizzate le credenziali della libreria client di Database elastico hello tooaccess](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="a68cc-204">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

### <a name="only-metadata-affected"></a><span data-ttu-id="a68cc-205">Impatto solo sui metadati</span><span class="sxs-lookup"><span data-stu-id="a68cc-205">Only metadata affected</span></span>
<span data-ttu-id="a68cc-206">Metodi usati per la compilazione o la modifica di hello **ShardMapManager** dati non si modificano i dati utente hello archiviati in partizioni hello autonomamente.</span><span class="sxs-lookup"><span data-stu-id="a68cc-206">Methods used for populating or changing hello **ShardMapManager** data do not alter hello user data stored in hello shards themselves.</span></span> <span data-ttu-id="a68cc-207">Ad esempio, i metodi, ad esempio **CreateShard**, **DeleteShard**, **UpdateMapping**e così via interessano solo metadati di mappa partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="a68cc-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect hello shard map metadata only.</span></span> <span data-ttu-id="a68cc-208">Non rimuovere, aggiungere o modificare i dati utente contenuti nelle partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="a68cc-208">They do not remove, add, or alter user data contained in hello shards.</span></span> <span data-ttu-id="a68cc-209">Questi metodi sono invece progettato toobe utilizzato in combinazione con operazioni separate eseguire toocreate o rimuovere un database effettivo, o che lo spostamento di righe da una partizione tooanother toorebalance un ambiente partizionato.</span><span class="sxs-lookup"><span data-stu-id="a68cc-209">Instead, these methods are designed toobe used in conjunction with separate operations you perform toocreate or remove actual databases, or that move rows from one shard tooanother toorebalance a sharded environment.</span></span>  <span data-ttu-id="a68cc-210">(hello **suddivisione unione** strumento incluso in strumenti di database elastico utilizza queste API con lo spostamento dei dati effettivi tra le partizioni di orchestrazione.) Vedere [scala utilizzando lo strumento di unione di Database elastico split hello](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="a68cc-210">(hello **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using hello Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

## <a name="populating-a-shard-map-example"></a><span data-ttu-id="a68cc-211">Esempio di popolamento di una mappa partizioni</span><span class="sxs-lookup"><span data-stu-id="a68cc-211">Populating a shard map example</span></span>
<span data-ttu-id="a68cc-212">Di seguito è riportata una sequenza di operazioni toopopulate una mappa partizioni specifiche di esempio.</span><span class="sxs-lookup"><span data-stu-id="a68cc-212">An example sequence of operations toopopulate a specific shard map is shown below.</span></span> <span data-ttu-id="a68cc-213">codice Hello esegue queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="a68cc-213">hello code performs these steps:</span></span> 

1. <span data-ttu-id="a68cc-214">Creazione di una nuova mappa partizioni in un gestore delle mappe partizioni.</span><span class="sxs-lookup"><span data-stu-id="a68cc-214">A new shard map is created within a shard map manager.</span></span> 
2. <span data-ttu-id="a68cc-215">mappa partizioni toohello vengono aggiunti metadati di Hello per due partizioni diverse.</span><span class="sxs-lookup"><span data-stu-id="a68cc-215">hello metadata for two different shards is added toohello shard map.</span></span> 
3. <span data-ttu-id="a68cc-216">Un'ampia gamma di mapping di intervalli di chiavi vengono aggiunti e hello contenuto globale della mappa partizioni hello viene visualizzati.</span><span class="sxs-lookup"><span data-stu-id="a68cc-216">A variety of key range mappings are added, and hello overall contents of hello shard map are displayed.</span></span> 

<span data-ttu-id="a68cc-217">codice Hello viene scritto in modo che sia possibile eseguire nuovamente il metodo hello se si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="a68cc-217">hello code is written so that hello method can be rerun if an error occurs.</span></span> <span data-ttu-id="a68cc-218">Ogni richiesta di verifica se una partizione o mapping esiste già, prima di tentare di toocreate è.</span><span class="sxs-lookup"><span data-stu-id="a68cc-218">Each request tests whether a shard or mapping already exists, before attempting toocreate it.</span></span> <span data-ttu-id="a68cc-219">Hello codice si presuppone che i database **sample_shard_0**, **sample_shard_1** e **sample_shard_2** sono già stati creati nel server di hello stringaacuifariferimento**shardServer**.</span><span class="sxs-lookup"><span data-stu-id="a68cc-219">hello code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in hello server referenced by string **shardServer**.</span></span> 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List hello shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

<span data-ttu-id="a68cc-220">Come alternativa è possibile utilizzare PowerShell script hello tooachieve stesso risultato.</span><span class="sxs-lookup"><span data-stu-id="a68cc-220">As an alternative you can use PowerShell scripts tooachieve hello same result.</span></span> <span data-ttu-id="a68cc-221">Alcuni degli esempi di PowerShell di esempio hello sono disponibili [qui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="a68cc-221">Some of hello sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>     

<span data-ttu-id="a68cc-222">Una volta mappe partizioni sono state popolate, applicazioni di accesso ai dati possono essere create o adattato toowork con mappe hello.</span><span class="sxs-lookup"><span data-stu-id="a68cc-222">Once shard maps have been populated, data access applications can be created or adapted toowork with hello maps.</span></span> <span data-ttu-id="a68cc-223">La compilazione o la modifica delle mappe di hello non devono necessariamente verificarsi finché **layout mappa** deve toochange.</span><span class="sxs-lookup"><span data-stu-id="a68cc-223">Populating or manipulating hello maps need not occur again until **map layout** needs toochange.</span></span>  

## <a name="data-dependent-routing"></a><span data-ttu-id="a68cc-224">Routing dipendente dei dati</span><span class="sxs-lookup"><span data-stu-id="a68cc-224">Data dependent routing</span></span>
<span data-ttu-id="a68cc-225">gestore mappe partizioni di Hello più utilizzato in applicazioni che richiedono operazioni di database connessioni tooperform hello dati specifici dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a68cc-225">hello shard map manager will be most used in applications that require database connections tooperform hello app-specific data operations.</span></span> <span data-ttu-id="a68cc-226">Tali connessioni devono essere associate al database corretto hello.</span><span class="sxs-lookup"><span data-stu-id="a68cc-226">Those connections must be associated with hello correct database.</span></span> <span data-ttu-id="a68cc-227">Questa procedura è nota come **routing dipendente dai dati**.</span><span class="sxs-lookup"><span data-stu-id="a68cc-227">This is known as **Data Dependent Routing**.</span></span> <span data-ttu-id="a68cc-228">Per queste applicazioni, creare un'istanza di un oggetto di gestione di partizioni della mappa da factory hello utilizzando le credenziali che dispongono dell'accesso di sola lettura sul database GSM hello.</span><span class="sxs-lookup"><span data-stu-id="a68cc-228">For these applications, instantiate a shard map manager object from hello factory using credentials that have read-only access on hello GSM database.</span></span> <span data-ttu-id="a68cc-229">Le singole richieste per le connessioni successive forniscono le credenziali necessarie per la connessione di database di partizione appropriato toohello.</span><span class="sxs-lookup"><span data-stu-id="a68cc-229">Individual requests for later connections supply credentials necessary for connecting toohello appropriate shard database.</span></span>

<span data-ttu-id="a68cc-230">Si noti che queste applicazioni (utilizzando **ShardMapManager** aperta con le credenziali di sola lettura) non è possibile apportare modifiche toohello mappe o i mapping.</span><span class="sxs-lookup"><span data-stu-id="a68cc-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes toohello maps or mappings.</span></span> <span data-ttu-id="a68cc-231">A questo scopo è possibile creare applicazioni specifiche per l'amministrazione o script di PowerShell che forniscono credenziali con privilegi elevati, come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="a68cc-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span></span> <span data-ttu-id="a68cc-232">Vedere [utilizzate le credenziali della libreria client di Database elastico hello tooaccess](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="a68cc-232">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

<span data-ttu-id="a68cc-233">Per informazioni dettagliate, vedere [Routing dipendente dei dati](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="a68cc-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> 

## <a name="modifying-a-shard-map"></a><span data-ttu-id="a68cc-234">Modifica di una mappa partizioni</span><span class="sxs-lookup"><span data-stu-id="a68cc-234">Modifying a shard map</span></span>
<span data-ttu-id="a68cc-235">È possibile modificare una mappa partizioni in molti modi diversi.</span><span class="sxs-lookup"><span data-stu-id="a68cc-235">A shard map can be changed in different ways.</span></span> <span data-ttu-id="a68cc-236">Tutti i seguenti metodi hello modificare hello metadati che descrivono le partizioni hello e i relativi mapping, ma fisicamente non modificano i dati all'interno di partizioni hello, né eseguire e creare o eliminare database effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="a68cc-236">All of hello following methods modify hello metadata describing hello shards and their mappings, but they do not physically modify data within hello shards, nor do they create or delete hello actual databases.</span></span>  <span data-ttu-id="a68cc-237">Alcune delle operazioni di hello nella mappa partizioni hello descritto di seguito potrebbe essere necessario toobe coordinati azioni amministrative che spostare fisicamente i dati o di aggiungere e rimuovere i database che funge da partizioni.</span><span class="sxs-lookup"><span data-stu-id="a68cc-237">Some of hello operations on hello shard map described below may need toobe coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span></span>

<span data-ttu-id="a68cc-238">Questi metodi funzionano insieme come blocchi predefiniti di hello disponibili per la modifica di hello distribuzione complessiva dei dati nell'ambiente di database partizionato.</span><span class="sxs-lookup"><span data-stu-id="a68cc-238">These methods work together as hello building blocks available for modifying hello overall distribution of data in your sharded database environment.</span></span>  

* <span data-ttu-id="a68cc-239">tooadd o Rimuovi partizioni: utilizzare  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  e  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  di hello [Shardmap classe](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span><span class="sxs-lookup"><span data-stu-id="a68cc-239">tooadd or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of hello [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span></span> 
  
    <span data-ttu-id="a68cc-240">Hello server e database che rappresenta il partizionamento di destinazione hello deve esistere per tooexecute queste operazioni.</span><span class="sxs-lookup"><span data-stu-id="a68cc-240">hello server and database representing hello target shard must already exist for these operations tooexecute.</span></span> <span data-ttu-id="a68cc-241">Questi metodi non hanno alcun impatto su hello database, solo nei metadati nella mappa partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="a68cc-241">These methods do not have any impact on hello databases themselves, only on metadata in hello shard map.</span></span>
* <span data-ttu-id="a68cc-242">toocreate o rimuovere punti o gli intervalli che sono mappati partizioni toohello: utilizzare  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  di hello [RangeShardMapping classe](https://msdn.microsoft.com/library/azure/dn807318.aspx), e  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  di hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span><span class="sxs-lookup"><span data-stu-id="a68cc-242">toocreate or remove points or ranges that are mapped toohello shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of hello [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span></span>
  
    <span data-ttu-id="a68cc-243">Molti punti diversi o gli intervalli possono essere mappata toohello stesso partizione.</span><span class="sxs-lookup"><span data-stu-id="a68cc-243">Many different points or ranges can be mapped toohello same shard.</span></span> <span data-ttu-id="a68cc-244">Questi metodi influiscono solo sui metadati, non sui dati eventualmente già presenti nelle partizioni.</span><span class="sxs-lookup"><span data-stu-id="a68cc-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span></span> <span data-ttu-id="a68cc-245">Se è necessario toobe rimosso dal database di hello in ordine toobe coerente con dati **DeleteMapping** operazioni, sarà necessario tooperform queste operazioni separatamente, ma in combinazione con i metodi seguenti.</span><span class="sxs-lookup"><span data-stu-id="a68cc-245">If data needs toobe removed from hello database in order toobe consistent with **DeleteMapping** operations, you will need tooperform those operations separately but in conjunction with using these methods.</span></span>  
* <span data-ttu-id="a68cc-246">toosplit intervalli esistenti in due o unione intervalli adiacenti in un unico: utilizzare  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  e  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="a68cc-246">toosplit existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span></span>  
  
    <span data-ttu-id="a68cc-247">Si noti che suddividere e le operazioni di unione **non cambiano chiave toowhich di hello partizione vengono eseguito il mapping di valori**.</span><span class="sxs-lookup"><span data-stu-id="a68cc-247">Note that split and merge operations **do not change hello shard toowhich key values are mapped**.</span></span> <span data-ttu-id="a68cc-248">Una divisione suddivide un intervallo esistente in due parti, ma non entrambi come toohello mappato stesso partizione.</span><span class="sxs-lookup"><span data-stu-id="a68cc-248">A split breaks an existing range into two parts, but leaves both as mapped toohello same shard.</span></span> <span data-ttu-id="a68cc-249">Un'operazione di unione opera su due intervalli adiacenti che sono già mappato toohello partizione stessa, li unione in un singolo intervallo.</span><span class="sxs-lookup"><span data-stu-id="a68cc-249">A merge operates on two adjacent ranges that are already mapped toohello same shard, coalescing them into a single range.</span></span>  <span data-ttu-id="a68cc-250">spostamento dei punti o gli stessi intervalli tra le partizioni Hello deve toobe coordinate mediante l'utilizzo **UpdateMapping** in combinazione con lo spostamento dei dati effettivi.</span><span class="sxs-lookup"><span data-stu-id="a68cc-250">hello movement of points or ranges themselves between shards needs toobe coordinated by using **UpdateMapping** in conjunction with actual data movement.</span></span>  <span data-ttu-id="a68cc-251">È possibile utilizzare hello **suddivisione/unione** strumenti del servizio che fa parte di database elastico toocoordinate modifiche alla mappa di partizioni con lo spostamento dei dati, quando è necessario lo spostamento.</span><span class="sxs-lookup"><span data-stu-id="a68cc-251">You can use hello **Split/Merge** service that is part of elastic database tools toocoordinate shard map changes with data movement, when movement is needed.</span></span> 
* <span data-ttu-id="a68cc-252">mappa toore (o spostamento) partizioni toodifferent singoli punti o intervalli: utilizzare  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="a68cc-252">toore-map (or move) individual points or ranges toodifferent shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span></span>  
  
    <span data-ttu-id="a68cc-253">Poiché i dati potrebbero essere spostato da una partizione tooanother in ordine toobe coerente con toobe **UpdateMapping** operazioni, sarà necessario tooperform tale spostamento separatamente, ma in combinazione con i metodi seguenti.</span><span class="sxs-lookup"><span data-stu-id="a68cc-253">Since data may need toobe moved from one shard tooanother in order toobe consistent with **UpdateMapping** operations, you will need tooperform that movement separately but in conjunction with using these methods.</span></span>
* <span data-ttu-id="a68cc-254">mapping tootake online e offline: utilizzare  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  e  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol hello online dello stato di un mapping.</span><span class="sxs-lookup"><span data-stu-id="a68cc-254">tootake mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** toocontrol hello online state of a mapping.</span></span> 
  
    <span data-ttu-id="a68cc-255">Alcune operazioni sui mapping di partizioni, incluse le operazioni **UpdateMapping** e **DeleteMapping**, sono consentite solo se lo stato del mapping è "offline".</span><span class="sxs-lookup"><span data-stu-id="a68cc-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span></span> <span data-ttu-id="a68cc-256">Quando un mapping è offline, una richiesta dipendente dai dati e basata su una chiave inclusa nel mapping restituirà un errore.</span><span class="sxs-lookup"><span data-stu-id="a68cc-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span></span> <span data-ttu-id="a68cc-257">Inoltre, quando un intervallo prima di tutto è offline, tutte le partizioni di toohello interessata le connessioni vengono terminate automaticamente nei risultati ordine tooprevent incomplete o per le query nei confronti di intervalli da modificare.</span><span class="sxs-lookup"><span data-stu-id="a68cc-257">In addition, when a range is first taken offline, all connections toohello affected shard are automatically killed in order tooprevent inconsistent or incomplete results for queries directed against ranges being changed.</span></span> 

<span data-ttu-id="a68cc-258">I mapping sono oggetti non modificabili in .NET.</span><span class="sxs-lookup"><span data-stu-id="a68cc-258">Mappings are immutable objects in .Net.</span></span>  <span data-ttu-id="a68cc-259">Tutti i metodi hello precedenti che modificare i mapping di invalidare anche qualsiasi toothem riferimenti nel codice.</span><span class="sxs-lookup"><span data-stu-id="a68cc-259">All of hello methods above that change mappings also invalidate any references toothem in your code.</span></span> <span data-ttu-id="a68cc-260">toomake it sequenze tooperform più semplice di operazioni che modificano lo stato del mapping, tutti i metodi di hello che modifica un mapping di restituiscono un nuovo mapping di riferimento, pertanto le operazioni possono essere concatenate.</span><span class="sxs-lookup"><span data-stu-id="a68cc-260">toomake it easier tooperform sequences of operations that change a mapping’s state, all of hello methods that change a mapping return a new mapping reference, so operations can be chained.</span></span> <span data-ttu-id="a68cc-261">Ad esempio, toodelete un mapping in sm shardmap che contiene la chiave hello 25 esistente, è possibile eseguire hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="a68cc-261">For example, toodelete an existing mapping in shardmap sm that contains hello key 25, you can execute hello following:</span></span> 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a><span data-ttu-id="a68cc-262">Aggiunta di una partizione</span><span class="sxs-lookup"><span data-stu-id="a68cc-262">Adding a shard</span></span>
<span data-ttu-id="a68cc-263">Le applicazioni spesso necessario toosimply aggiungere nuovi dati toohandle partizioni che si prevedono di nuove chiavi o intervalli di chiavi per una mappa partizioni è già esistente.</span><span class="sxs-lookup"><span data-stu-id="a68cc-263">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="a68cc-264">Ad esempio, un'applicazione partizionata in base l'ID Tenant potrebbe essere necessario tooprovision una nuova partizione per un nuovo tenant o mensile partizionati dati potrebbe essere una nuova partizione provisioning prima dell'inizio hello di ogni nuovo mese.</span><span class="sxs-lookup"><span data-stu-id="a68cc-264">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="a68cc-265">Se il nuovo intervallo di hello dei valori di chiave non è già parte di un mapping esistente e non lo spostamento dei dati è necessario, è una nuova partizione di hello tooadd molto semplice e associare una nuova chiave hello o partizioni toothat intervallo.</span><span class="sxs-lookup"><span data-stu-id="a68cc-265">If hello new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> <span data-ttu-id="a68cc-266">Per informazioni dettagliate sull'aggiunta di nuove partizioni, vedere [Aggiunta di una nuova partizione](sql-database-elastic-scale-add-a-shard.md).</span><span class="sxs-lookup"><span data-stu-id="a68cc-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span></span>

<span data-ttu-id="a68cc-267">Per gli scenari che richiedono lo spostamento dei dati, tuttavia, lo strumento di unione di menu combinato hello è lo spostamento dei dati di hello tooorchestrate necessarie tra le partizioni in combinazione con gli aggiornamenti delle mappe partizioni necessari hello.</span><span class="sxs-lookup"><span data-stu-id="a68cc-267">For scenarios that require data movement, however, hello split-merge tool is needed tooorchestrate hello data movement between shards in combination with hello necessary shard map updates.</span></span> <span data-ttu-id="a68cc-268">Per informazioni dettagliate sull'utilizzo hello yool unione di menu combinato, vedere [Panoramica di unione di menu combinato](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="a68cc-268">For details on using hello split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
