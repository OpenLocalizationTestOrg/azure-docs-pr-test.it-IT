---
title: Aumentare il numero di istanze di un database SQL di Azure | Documentazione Microsoft
description: Come utilizzare ShardMapManager, libreria client dei database elastici
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
ms.openlocfilehash: f626cf417d8b3f1761f3c900d49039b3ff83b093
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="scale-out-databases-with-the-shard-map-manager"></a><span data-ttu-id="80f46-103">Aumentare il numero di istanze dei database con il gestore delle mappe partizioni</span><span class="sxs-lookup"><span data-stu-id="80f46-103">Scale out databases with the shard map manager</span></span>
<span data-ttu-id="80f46-104">Per aumentare facilmente il numero di istanze dei database in SQL Azure, usare un gestore delle mappe partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-104">To easily scale out databases on SQL Azure, use a shard map manager.</span></span> <span data-ttu-id="80f46-105">Il gestore delle mappe partizioni è un database speciale che gestisce le informazioni di mapping globale su tutte le partizioni (database) in un set di partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-105">The shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span></span> <span data-ttu-id="80f46-106">I metadati consentono all'applicazione di connettersi al database corretto in base al valore della **chiave di partizionamento orizzontale**.</span><span class="sxs-lookup"><span data-stu-id="80f46-106">The metadata allows an application to connect to the correct database based upon the value of the **sharding key**.</span></span> <span data-ttu-id="80f46-107">Inoltre, ogni partizione nel set contiene le mappe che tengono traccia dei dati delle partizioni locali (i cosiddetti **shardlet**).</span><span class="sxs-lookup"><span data-stu-id="80f46-107">In addition, every shard in the set contains maps that track the local shard data (known as **shardlets**).</span></span> 

![Gestione mappe partizioni](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

<span data-ttu-id="80f46-109">Per gestire le mappe partizioni, è fondamentale comprenderne il processo di creazione.</span><span class="sxs-lookup"><span data-stu-id="80f46-109">Understanding how these maps are constructed is essential to shard map management.</span></span> <span data-ttu-id="80f46-110">A questo scopo si usa la [classe ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), disponibile nella [libreria client dei database elastici](sql-database-elastic-database-client-library.md).</span><span class="sxs-lookup"><span data-stu-id="80f46-110">This is done using the [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in the [Elastic Database client library](sql-database-elastic-database-client-library.md) to manage shard maps.</span></span>  

## <a name="shard-maps-and-shard-mappings"></a><span data-ttu-id="80f46-111">Mappe partizioni e mapping di partizioni</span><span class="sxs-lookup"><span data-stu-id="80f46-111">Shard maps and shard mappings</span></span>
<span data-ttu-id="80f46-112">Per ogni partizione, è necessario selezionare il tipo di mappa partizioni da creare.</span><span class="sxs-lookup"><span data-stu-id="80f46-112">For each shard, you must select the type of shard map to create.</span></span> <span data-ttu-id="80f46-113">La scelta dipende dall'architettura del database:</span><span class="sxs-lookup"><span data-stu-id="80f46-113">The choice depends on the database architecture:</span></span> 

1. <span data-ttu-id="80f46-114">Singolo tenant per database</span><span class="sxs-lookup"><span data-stu-id="80f46-114">Single tenant per database</span></span>  
2. <span data-ttu-id="80f46-115">Più tenant per database (due tipi):</span><span class="sxs-lookup"><span data-stu-id="80f46-115">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="80f46-116">Mapping di tipo elenco</span><span class="sxs-lookup"><span data-stu-id="80f46-116">List mapping</span></span>
   2. <span data-ttu-id="80f46-117">Mapping di tipo intervallo</span><span class="sxs-lookup"><span data-stu-id="80f46-117">Range mapping</span></span>

<span data-ttu-id="80f46-118">Per un modello a singolo tenant, creare una mappa partizioni con **mapping di tipo elenco** .</span><span class="sxs-lookup"><span data-stu-id="80f46-118">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="80f46-119">Il modello single-tenant assegna un database per tenant.</span><span class="sxs-lookup"><span data-stu-id="80f46-119">The single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="80f46-120">Si tratta di un modello efficace per gli sviluppatori SaaS in quanto semplifica la gestione.</span><span class="sxs-lookup"><span data-stu-id="80f46-120">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Mapping di tipo elenco][1]

<span data-ttu-id="80f46-122">Il modello multi-tenant assegna diversi tenant a un database singolo ed è possibile distribuire gruppi di tenant tra più database.</span><span class="sxs-lookup"><span data-stu-id="80f46-122">The multi-tenant model assigns several tenants to a single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="80f46-123">Usare questo modello quando si prevedono esigenze di dati ridotte per ogni tenant.</span><span class="sxs-lookup"><span data-stu-id="80f46-123">Use this model when you expect each tenant to have small data needs.</span></span> <span data-ttu-id="80f46-124">In questo modello viene assegnato un intervallo di tenant a un database usando il **mapping di tipo intervallo**.</span><span class="sxs-lookup"><span data-stu-id="80f46-124">In this model, we assign a range of tenants to a database using **range mapping**.</span></span> 

![Mapping di tipo intervallo][2]

<span data-ttu-id="80f46-126">In alternativa è possibile implementare un modello di database multi-tenant usando il *mapping di tipo elenco* per assegnare più tenant a un database singolo.</span><span class="sxs-lookup"><span data-stu-id="80f46-126">Or you can implement a multi-tenant database model using a *list mapping* to assign multiple tenants to a single database.</span></span> <span data-ttu-id="80f46-127">Ad esempio, DB1 viene usato per archiviare le informazioni sugli ID tenant 1 e 5 e DB2 archivia i dati per i tenant 7 e 10.</span><span class="sxs-lookup"><span data-stu-id="80f46-127">For example, DB1 is used to store information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Tenant multipli su database singolo][3] 

### <a name="supported-net-types-for-sharding-keys"></a><span data-ttu-id="80f46-129">Tipi .NET supportati per le chiavi di partizionamento orizzontale</span><span class="sxs-lookup"><span data-stu-id="80f46-129">Supported .Net types for sharding keys</span></span>
<span data-ttu-id="80f46-130">Scalabilità elastica supporta i seguenti tipi di .NET Framework come chiavi di partizionamento orizzontale:</span><span class="sxs-lookup"><span data-stu-id="80f46-130">Elastic Scale support the following .Net Framework types as sharding keys:</span></span>

* <span data-ttu-id="80f46-131">numero intero</span><span class="sxs-lookup"><span data-stu-id="80f46-131">integer</span></span>
* <span data-ttu-id="80f46-132">long</span><span class="sxs-lookup"><span data-stu-id="80f46-132">long</span></span>
* <span data-ttu-id="80f46-133">guid</span><span class="sxs-lookup"><span data-stu-id="80f46-133">guid</span></span>
* <span data-ttu-id="80f46-134">byte[]</span><span class="sxs-lookup"><span data-stu-id="80f46-134">byte[]</span></span>  
* <span data-ttu-id="80f46-135">datetime</span><span class="sxs-lookup"><span data-stu-id="80f46-135">datetime</span></span>
* <span data-ttu-id="80f46-136">timespan</span><span class="sxs-lookup"><span data-stu-id="80f46-136">timespan</span></span>
* <span data-ttu-id="80f46-137">datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="80f46-137">datetimeoffset</span></span>

### <a name="list-and-range-shard-maps"></a><span data-ttu-id="80f46-138">Mappe partizioni di tipo elenco e intervallo</span><span class="sxs-lookup"><span data-stu-id="80f46-138">List and range shard maps</span></span>
<span data-ttu-id="80f46-139">Le mappe partizioni possono essere create usando **elenchi di singoli valori di chiavi di partizionamento orizzontale** oppure tramite **intervalli di valori di chiavi di partizionamento orizzontale**.</span><span class="sxs-lookup"><span data-stu-id="80f46-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span></span> 

### <a name="list-shard-maps"></a><span data-ttu-id="80f46-140">Mappe partizioni di tipo elenco</span><span class="sxs-lookup"><span data-stu-id="80f46-140">List shard maps</span></span>
<span data-ttu-id="80f46-141">Le **partizioni** includono **shardlet** e il mapping degli shardlet alle partizioni viene gestito da una mappa partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-141">**Shards** contain **shardlets** and the mapping of shardlets to shards is maintained by a shard map.</span></span> <span data-ttu-id="80f46-142">Una **mappa partizioni di tipo elenco** è un'associazione tra i singoli valori di chiave che identificano gli shardlet e i database che fungono da partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-142">A **list shard map** is an association between the individual key values that identify the shardlets and the databases that serve as shards.</span></span>  <span data-ttu-id="80f46-143">I **mapping di tipo elenco** sono espliciti. È possibile eseguire il mapping di valori di chiave diversi allo stesso database.</span><span class="sxs-lookup"><span data-stu-id="80f46-143">**List mappings** are explicit and different key values can be mapped to the same database.</span></span> <span data-ttu-id="80f46-144">Ad esempio, la chiave 1 è mappata al database A e i valori di chiave 3 e 6 fanno entrambi riferimento al database B.</span><span class="sxs-lookup"><span data-stu-id="80f46-144">For example, key 1 maps to Database A, and key values 3 and 6 both reference Database B.</span></span>

| <span data-ttu-id="80f46-145">Chiave</span><span class="sxs-lookup"><span data-stu-id="80f46-145">Key</span></span> | <span data-ttu-id="80f46-146">Percorso della partizione</span><span class="sxs-lookup"><span data-stu-id="80f46-146">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="80f46-147">1</span><span class="sxs-lookup"><span data-stu-id="80f46-147">1</span></span> |<span data-ttu-id="80f46-148">Database_A</span><span class="sxs-lookup"><span data-stu-id="80f46-148">Database_A</span></span> |
| <span data-ttu-id="80f46-149">3</span><span class="sxs-lookup"><span data-stu-id="80f46-149">3</span></span> |<span data-ttu-id="80f46-150">Database_B</span><span class="sxs-lookup"><span data-stu-id="80f46-150">Database_B</span></span> |
| <span data-ttu-id="80f46-151">4</span><span class="sxs-lookup"><span data-stu-id="80f46-151">4</span></span> |<span data-ttu-id="80f46-152">Database_C</span><span class="sxs-lookup"><span data-stu-id="80f46-152">Database_C</span></span> |
| <span data-ttu-id="80f46-153">6</span><span class="sxs-lookup"><span data-stu-id="80f46-153">6</span></span> |<span data-ttu-id="80f46-154">Database_B</span><span class="sxs-lookup"><span data-stu-id="80f46-154">Database_B</span></span> |
| <span data-ttu-id="80f46-155">...</span><span class="sxs-lookup"><span data-stu-id="80f46-155">...</span></span> |<span data-ttu-id="80f46-156">...</span><span class="sxs-lookup"><span data-stu-id="80f46-156">...</span></span> |

### <a name="range-shard-maps"></a><span data-ttu-id="80f46-157">Mappa partizioni di tipo intervallo</span><span class="sxs-lookup"><span data-stu-id="80f46-157">Range shard maps</span></span>
<span data-ttu-id="80f46-158">In una **mappa partizioni di tipo intervallo** l'intervallo chiave è descritto da una coppia di tipo **[Low Value, High Value)**, dove *Low Value* indica la chiave minima dell'intervallo e *High Value* è il primo valore superiore all'intervallo.</span><span class="sxs-lookup"><span data-stu-id="80f46-158">In a **range shard map**, the key range is described by a pair **[Low Value, High Value)** where the *Low Value* is the minimum key in the range, and the *High Value* is the first value higher than the range.</span></span> 

<span data-ttu-id="80f46-159">Ad esempio, **[0, 100)** include tutti i numeri interi superiori o uguali a 0 e inferiori a 100.</span><span class="sxs-lookup"><span data-stu-id="80f46-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span></span> <span data-ttu-id="80f46-160">Si noti che più intervalli possono fare riferimento allo stesso database e che sono supportati intervalli non contigui. Ad esempio, [100,200) e [400,600) fanno entrambi riferimento al Database C nel seguente esempio.</span><span class="sxs-lookup"><span data-stu-id="80f46-160">Note that multiple ranges can point to the same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point to Database C in the example below.)</span></span>

| <span data-ttu-id="80f46-161">Chiave</span><span class="sxs-lookup"><span data-stu-id="80f46-161">Key</span></span> | <span data-ttu-id="80f46-162">Percorso della partizione</span><span class="sxs-lookup"><span data-stu-id="80f46-162">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="80f46-163">[1, 50)</span><span class="sxs-lookup"><span data-stu-id="80f46-163">[1,50)</span></span> |<span data-ttu-id="80f46-164">Database_A</span><span class="sxs-lookup"><span data-stu-id="80f46-164">Database_A</span></span> |
| <span data-ttu-id="80f46-165">[50, 100)</span><span class="sxs-lookup"><span data-stu-id="80f46-165">[50,100)</span></span> |<span data-ttu-id="80f46-166">Database_B</span><span class="sxs-lookup"><span data-stu-id="80f46-166">Database_B</span></span> |
| <span data-ttu-id="80f46-167">[100, 200)</span><span class="sxs-lookup"><span data-stu-id="80f46-167">[100,200)</span></span> |<span data-ttu-id="80f46-168">Database_C</span><span class="sxs-lookup"><span data-stu-id="80f46-168">Database_C</span></span> |
| <span data-ttu-id="80f46-169">[400, 600)</span><span class="sxs-lookup"><span data-stu-id="80f46-169">[400,600)</span></span> |<span data-ttu-id="80f46-170">Database_C</span><span class="sxs-lookup"><span data-stu-id="80f46-170">Database_C</span></span> |
| <span data-ttu-id="80f46-171">...</span><span class="sxs-lookup"><span data-stu-id="80f46-171">...</span></span> |<span data-ttu-id="80f46-172">...</span><span class="sxs-lookup"><span data-stu-id="80f46-172">...</span></span> |

<span data-ttu-id="80f46-173">Ognuna delle tabelle precedenti è un esempio concettuale di un oggetto **ShardMap** .</span><span class="sxs-lookup"><span data-stu-id="80f46-173">Each of the tables shown above is a conceptual example of a **ShardMap** object.</span></span> <span data-ttu-id="80f46-174">Ogni riga costituisce un esempio semplificato di un singolo oggetto **PointMapping** (per la mappa partizioni di tipo elenco) o **RangeMapping** (per la mappa partizioni di tipo intervallo).</span><span class="sxs-lookup"><span data-stu-id="80f46-174">Each row is a simplified example of an individual **PointMapping** (for the list shard map) or **RangeMapping** (for the range shard map) object.</span></span>

## <a name="shard-map-manager"></a><span data-ttu-id="80f46-175">Gestore mappe partizioni</span><span class="sxs-lookup"><span data-stu-id="80f46-175">Shard map manager</span></span>
<span data-ttu-id="80f46-176">Il gestore mappe partizioni nella libreria client è una raccolta di mappe partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-176">In the client library, the shard map  manager is a collection of shard maps.</span></span> <span data-ttu-id="80f46-177">I dati gestiti da un'istanza di **ShardMapManager** sono conservati in tre posizioni:</span><span class="sxs-lookup"><span data-stu-id="80f46-177">The data managed by a **ShardMapManager** instance is kept in three places:</span></span> 

1. <span data-ttu-id="80f46-178">**Mappa globale partizioni**: si specifica un database da usare come repository per tutte le mappe partizioni e i mapping corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="80f46-178">**Global Shard Map (GSM)**: You specify a database to serve as the repository for all of its shard maps and mappings.</span></span> <span data-ttu-id="80f46-179">Vengono create automaticamente tabelle speciali e stored procedure per la gestione delle informazioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-179">Special tables and stored procedures are automatically created to manage the information.</span></span> <span data-ttu-id="80f46-180">Si tratta in genere di un database di piccole dimensioni e a cui si accede raramente ed è consigliabile non usarlo per altre esigenze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="80f46-180">This is typically a small database and lightly accessed, and it should not be used for other needs of the application.</span></span> <span data-ttu-id="80f46-181">Le tabelle si trovano in uno schema speciale denominato **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="80f46-181">The tables are in a special schema named **__ShardManagement**.</span></span> 
2. <span data-ttu-id="80f46-182">**Mappa locale partizioni**: ogni database specificato per l'uso come partizione viene modificato in modo da includere varie tabelle di piccole dimensioni e stored procedure speciali, che includono e gestiscono informazioni sulle mappe partizioni specifiche per la partizione.</span><span class="sxs-lookup"><span data-stu-id="80f46-182">**Local Shard Map (LSM)**: Every database that you specify to be a shard is modified to contain several small tables and special stored procedures that contain and manage shard map information specific to that shard.</span></span> <span data-ttu-id="80f46-183">Queste informazioni sono ridondanti rispetto alle informazioni nella mappa globale partizioni e permettono all'applicazione di convalidare le informazioni sulla mappa partizioni memorizzate nella cache, senza sovraccaricare la mappa globale partizioni. L'applicazione usa la mappa locale partizioni per determinare se un mapping memorizzato nella cache è ancora valido.</span><span class="sxs-lookup"><span data-stu-id="80f46-183">This information is redundant with the information in the GSM, and it allows the application to validate cached shard map information without placing any load on the GSM; the application uses the LSM to determine if a cached mapping is still valid.</span></span> <span data-ttu-id="80f46-184">Le tabelle corrispondenti alla mappa locale partizioni in ogni partizione sono disponibili anche nello schema **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="80f46-184">The tables corresponding to the LSM on each shard are also in the schema **__ShardManagement**.</span></span>
3. <span data-ttu-id="80f46-185">**Cache dell'applicazione**: ogni istanza di applicazione che accede a un oggetto **ShardMapManager** gestisce una cache in memoria locale dei rispettivi mapping,</span><span class="sxs-lookup"><span data-stu-id="80f46-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span></span> <span data-ttu-id="80f46-186">in cui vengono archiviate le informazioni di routing appena recuperate.</span><span class="sxs-lookup"><span data-stu-id="80f46-186">It stores routing information that has recently been retrieved.</span></span> 

## <a name="constructing-a-shardmapmanager"></a><span data-ttu-id="80f46-187">Creazione di un oggetto ShardMapManager</span><span class="sxs-lookup"><span data-stu-id="80f46-187">Constructing a ShardMapManager</span></span>
<span data-ttu-id="80f46-188">Un oggetto **ShardMapManager** viene creato con un modello [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) .</span><span class="sxs-lookup"><span data-stu-id="80f46-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span></span> <span data-ttu-id="80f46-189">Il metodo **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** accetta credenziali, inclusi il nome del server e il nome del database contenente la mappa globale partizioni, sotto forma di oggetto **ConnectionString** e restituisce un'istanza di **ShardMapManager**.</span><span class="sxs-lookup"><span data-stu-id="80f46-189">The **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including the server name and database name holding the GSM) in the form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span></span>  

<span data-ttu-id="80f46-190">**Nota:** è sufficiente creare una sola istanza di **ShardMapManager** per ogni dominio app, nel codice di inizializzazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="80f46-190">**Please Note:** The **ShardMapManager** should be instantiated only once per app domain, within the initialization code for an application.</span></span> <span data-ttu-id="80f46-191">La creazione di istanze aggiuntive di ShardMapManager nello stesso dominio comporterà un aumento dell'utilizzo della memoria e della CPU dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="80f46-191">Creation of additional instances of ShardMapManager in the same appdomain, will result in increased memory and CPU utilization of the application.</span></span> <span data-ttu-id="80f46-192">Un oggetto **ShardMapManager** può includere un numero qualsiasi di mappe partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-192">A **ShardMapManager** can contain any number of shard maps.</span></span> <span data-ttu-id="80f46-193">Anche se è possibile che una singola mappa partizioni sia sufficiente per molte applicazioni, in alcune situazioni vengono usati diversi set di database per schemi diversi o per finalità specifiche. In questi casi è preferibile usare più mappe partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span></span> 

<span data-ttu-id="80f46-194">Nel codice seguente un'applicazione prova ad aprire un oggetto **ShardMapManager** esistente con il [metodo TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="80f46-194">In this code, an application tries to open an existing **ShardMapManager** with the [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span></span>  <span data-ttu-id="80f46-195">Se gli oggetti che rappresentano un oggetto **ShardMapManager** globale non esistono ancora nel database, vengono creati dalla libreria client con il [metodo CreateSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="80f46-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside the database, the client library creates them there using the [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span></span>

    // Try to get a reference to the Shard Map Manager 
     // via the Shard Map Manager database.  
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
        // Create the Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // The connectionString contains server name, database name, and admin credentials 
        // for privileges on both the GSM and the shards themselves.
    } 

<span data-ttu-id="80f46-196">In alternativa, è possibile utilizzare Powershell per creare un nuovo gestore delle mappe di partizionamento.</span><span class="sxs-lookup"><span data-stu-id="80f46-196">As an alternative, you can use Powershell to create a new Shard Map Manager.</span></span> <span data-ttu-id="80f46-197">Un esempio è disponibile [qui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="80f46-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="get-a-rangeshardmap-or-listshardmap"></a><span data-ttu-id="80f46-198">Ottenere una mappa RangeShardMap o ListShardMap</span><span class="sxs-lookup"><span data-stu-id="80f46-198">Get a RangeShardMap or ListShardMap</span></span>
<span data-ttu-id="80f46-199">Dopo la creazione di un gestore mappe partizioni, è possibile ottenere [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) o [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) con il metodo [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx) o [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx).</span><span class="sxs-lookup"><span data-stu-id="80f46-199">After creating a shard map manager, you can get the [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using the [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), the [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or the [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span>

    /// <summary>
    /// Creates a new Range Shard Map with the specified name, or gets the Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try to get a reference to the Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // The Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a><span data-ttu-id="80f46-200">Credenziali di amministrazione delle mappe partizioni</span><span class="sxs-lookup"><span data-stu-id="80f46-200">Shard map administration credentials</span></span>
<span data-ttu-id="80f46-201">Le applicazioni che amministrano e modificano le mappe partizioni sono diverse da quelle che usano le mappe partizioni per il routing delle connessioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-201">Applications that administer and manipulate shard maps are different from those that use the shard maps to route connections.</span></span> 

<span data-ttu-id="80f46-202">Per amministrare le mappe partizioni (aggiunta o modifica di partizioni, mappe partizioni, mapping di partizioni e così via), è necessario creare istanze dell'oggetto **ShardMapManager** usando **credenziali con privilegi di lettura/scrittura per il database della mappa globale partizioni e per ogni database usato come partizione**.</span><span class="sxs-lookup"><span data-stu-id="80f46-202">To administer shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate the **ShardMapManager** using **credentials that have read/write privileges on both the GSM database and on each database that serves as a shard**.</span></span> <span data-ttu-id="80f46-203">Le credenziali devono permettere operazioni di scrittura nelle tabelle nella mappa globale partizioni e nella mappa locale partizioni durante l'immissione o la modifica delle informazioni sulle mappe partizioni, oltre che per la creazione di tabelle della mappa locale partizioni nelle nuove partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-203">The credentials must allow for writes against the tables in both the GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span></span>  

<span data-ttu-id="80f46-204">Vedere [Credenziali usate per accedere alla libreria client dei database elastici](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="80f46-204">See [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

### <a name="only-metadata-affected"></a><span data-ttu-id="80f46-205">Impatto solo sui metadati</span><span class="sxs-lookup"><span data-stu-id="80f46-205">Only metadata affected</span></span>
<span data-ttu-id="80f46-206">I metodi usati per popolare o modificare i dati di **ShardMapManager** non influiscono sui dati utente archiviati nelle partizioni stesse.</span><span class="sxs-lookup"><span data-stu-id="80f46-206">Methods used for populating or changing the **ShardMapManager** data do not alter the user data stored in the shards themselves.</span></span> <span data-ttu-id="80f46-207">Ad esempio, i metodi come **CreateShard**, **DeleteShard**, **UpdateMapping** e così via interessano solo i metadati della mappa partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect the shard map metadata only.</span></span> <span data-ttu-id="80f46-208">Essi non rimuovono, aggiungono o modificano i dati utente contenuti nelle partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-208">They do not remove, add, or alter user data contained in the shards.</span></span> <span data-ttu-id="80f46-209">Questi metodi sono stati invece progettati per l'uso insieme a operazioni separate eseguite per creare o rimuovere i database effettivi o per rimuovere righe da una partizione a un'altra, in modo da bilanciare nuovamente un ambiente partizionato</span><span class="sxs-lookup"><span data-stu-id="80f46-209">Instead, these methods are designed to be used in conjunction with separate operations you perform to create or remove actual databases, or that move rows from one shard to another to rebalance a sharded environment.</span></span>  <span data-ttu-id="80f46-210">(il servizio di **suddivisione-unione** incluso negli strumenti dei database elastici usa queste API, oltre a orchestrare lo spostamento effettivo dei dati tra le partizioni). Vedere [Scalabilità tramite lo strumento di suddivisione-unione del database elastico](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="80f46-210">(The **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using the Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

## <a name="populating-a-shard-map-example"></a><span data-ttu-id="80f46-211">Esempio di popolamento di una mappa partizioni</span><span class="sxs-lookup"><span data-stu-id="80f46-211">Populating a shard map example</span></span>
<span data-ttu-id="80f46-212">Di seguito è disponibile una sequenza di esempio delle operazioni necessarie per popolare una mappa partizioni specifica.</span><span class="sxs-lookup"><span data-stu-id="80f46-212">An example sequence of operations to populate a specific shard map is shown below.</span></span> <span data-ttu-id="80f46-213">Il codice esegue i seguenti passaggi:</span><span class="sxs-lookup"><span data-stu-id="80f46-213">The code performs these steps:</span></span> 

1. <span data-ttu-id="80f46-214">Creazione di una nuova mappa partizioni in un gestore delle mappe partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-214">A new shard map is created within a shard map manager.</span></span> 
2. <span data-ttu-id="80f46-215">Aggiunta di metadati per due partizioni diverse a una mappa partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-215">The metadata for two different shards is added to the shard map.</span></span> 
3. <span data-ttu-id="80f46-216">Aggiunta di diversi mapping di intervalli di chiavi e visualizzazione dei contenuti complessivi della mappa partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-216">A variety of key range mappings are added, and the overall contents of the shard map are displayed.</span></span> 

<span data-ttu-id="80f46-217">Il codice è scritto in modo che sia possibile rieseguire il metodo se si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="80f46-217">The code is written so that the method can be rerun if an error occurs.</span></span> <span data-ttu-id="80f46-218">Prima di tentare di creare una partizione o un mapping, ogni richiesta verifica se la partizione o il mapping esiste già.</span><span class="sxs-lookup"><span data-stu-id="80f46-218">Each request tests whether a shard or mapping already exists, before attempting to create it.</span></span> <span data-ttu-id="80f46-219">Il codice presuppone che i database denominati **sample_shard_0**, **sample_shard_1** e **sample_shard_2** siano già stati creati nel server al quale fa riferimento la stringa **shardServer**.</span><span class="sxs-lookup"><span data-stu-id="80f46-219">The code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in the server referenced by string **shardServer**.</span></span> 

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

            // List the shards and mappings 
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

<span data-ttu-id="80f46-220">In alternativa, è possibile usare script di PowerShell per ottenere lo stesso risultato.</span><span class="sxs-lookup"><span data-stu-id="80f46-220">As an alternative you can use PowerShell scripts to achieve the same result.</span></span> <span data-ttu-id="80f46-221">Alcuni degli esempi di PowerShell sono disponibili [qui](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="80f46-221">Some of the sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>     

<span data-ttu-id="80f46-222">Dopo il popolamento delle mappe partizioni, sarà possibile creare o modificare le applicazioni di accesso ai dati in modo che usino le mappe.</span><span class="sxs-lookup"><span data-stu-id="80f46-222">Once shard maps have been populated, data access applications can be created or adapted to work with the maps.</span></span> <span data-ttu-id="80f46-223">Sarà necessario popolare o modificare di nuovo le mappe solo se occorrerà modificare il **layout delle mappe** .</span><span class="sxs-lookup"><span data-stu-id="80f46-223">Populating or manipulating the maps need not occur again until **map layout** needs to change.</span></span>  

## <a name="data-dependent-routing"></a><span data-ttu-id="80f46-224">Routing dipendente dei dati</span><span class="sxs-lookup"><span data-stu-id="80f46-224">Data dependent routing</span></span>
<span data-ttu-id="80f46-225">Lo strumento di gestione delle mappe partizioni viene usato principalmente dalle applicazioni che per eseguire specifiche operazioni sui dati richiedono connessioni a database.</span><span class="sxs-lookup"><span data-stu-id="80f46-225">The shard map manager will be most used in applications that require database connections to perform the app-specific data operations.</span></span> <span data-ttu-id="80f46-226">Tali connessioni devono essere associate al database corretto.</span><span class="sxs-lookup"><span data-stu-id="80f46-226">Those connections must be associated with the correct database.</span></span> <span data-ttu-id="80f46-227">Questa procedura è nota come **routing dipendente dai dati**.</span><span class="sxs-lookup"><span data-stu-id="80f46-227">This is known as **Data Dependent Routing**.</span></span> <span data-ttu-id="80f46-228">Per queste applicazioni è necessario creare istanze di un oggetto gestore delle mappe partizioni dal factory, usando le credenziali con accesso di sola lettura per il database della mappa globale partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-228">For these applications, instantiate a shard map manager object from the factory using credentials that have read-only access on the GSM database.</span></span> <span data-ttu-id="80f46-229">Le singole richieste per connessioni successive forniscono le credenziali necessarie per la connessione al database partizioni appropriato.</span><span class="sxs-lookup"><span data-stu-id="80f46-229">Individual requests for later connections supply credentials necessary for connecting to the appropriate shard database.</span></span>

<span data-ttu-id="80f46-230">Si noti che queste applicazioni, che usano l'oggetto **ShardMapManager** aperto con credenziali di sola lettura, non possono apportare modifiche alle mappe o ai mapping.</span><span class="sxs-lookup"><span data-stu-id="80f46-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes to the maps or mappings.</span></span> <span data-ttu-id="80f46-231">A questo scopo è possibile creare applicazioni specifiche per l'amministrazione o script di PowerShell che forniscono credenziali con privilegi elevati, come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="80f46-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span></span> <span data-ttu-id="80f46-232">Vedere [Credenziali usate per accedere alla libreria client dei database elastici](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="80f46-232">See [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

<span data-ttu-id="80f46-233">Per informazioni dettagliate, vedere [Routing dipendente dei dati](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="80f46-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> 

## <a name="modifying-a-shard-map"></a><span data-ttu-id="80f46-234">Modifica di una mappa partizioni</span><span class="sxs-lookup"><span data-stu-id="80f46-234">Modifying a shard map</span></span>
<span data-ttu-id="80f46-235">È possibile modificare una mappa partizioni in molti modi diversi.</span><span class="sxs-lookup"><span data-stu-id="80f46-235">A shard map can be changed in different ways.</span></span> <span data-ttu-id="80f46-236">Tutti i seguenti metodi modificano i metadati che descrivono le partizioni e i rispettivi mapping, ma non modificano fisicamente i dati nelle partizioni e non creano o eliminano i database effettivi.</span><span class="sxs-lookup"><span data-stu-id="80f46-236">All of the following methods modify the metadata describing the shards and their mappings, but they do not physically modify data within the shards, nor do they create or delete the actual databases.</span></span>  <span data-ttu-id="80f46-237">Potrebbe essere necessario coordinare alcune operazioni sulla mappa partizioni descritte di seguito con le azioni amministrative che spostano fisicamente i dati o che aggiungono e rimuovono i database che fungono da partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-237">Some of the operations on the shard map described below may need to be coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span></span>

<span data-ttu-id="80f46-238">Questi metodi interagiscono tra loro come i blocchi predefiniti disponibili per la modifica della distribuzione complessiva dei dati nell'ambiente di database partizionati.</span><span class="sxs-lookup"><span data-stu-id="80f46-238">These methods work together as the building blocks available for modifying the overall distribution of data in your sharded database environment.</span></span>  

* <span data-ttu-id="80f46-239">Per aggiungere o rimuovere partizioni, usare **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** e **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** della [classe Shardmap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span><span class="sxs-lookup"><span data-stu-id="80f46-239">To add or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of the [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span></span> 
  
    <span data-ttu-id="80f46-240">Per permettere l'esecuzione di queste operazioni, è necessario che il server e il database che rappresentano la partizione di destinazione esistano già.</span><span class="sxs-lookup"><span data-stu-id="80f46-240">The server and database representing the target shard must already exist for these operations to execute.</span></span> <span data-ttu-id="80f46-241">Questi metodi non hanno alcun impatto sui database stessi. Influiscono solo sui metadati nella mappa partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-241">These methods do not have any impact on the databases themselves, only on metadata in the shard map.</span></span>
* <span data-ttu-id="80f46-242">Per creare o rimuovere punti o intervalli mappati alle partizioni, usare **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)** e **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** della [classe RangeShardMapping](https://msdn.microsoft.com/library/azure/dn807318.aspx) e **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** di [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx).</span><span class="sxs-lookup"><span data-stu-id="80f46-242">To create or remove points or ranges that are mapped to the shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of the [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of the [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span></span>
  
    <span data-ttu-id="80f46-243">È possibile mappare molti punti o intervalli diversi alla stessa partizione.</span><span class="sxs-lookup"><span data-stu-id="80f46-243">Many different points or ranges can be mapped to the same shard.</span></span> <span data-ttu-id="80f46-244">Questi metodi influiscono solo sui metadati, non sui dati eventualmente già presenti nelle partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span></span> <span data-ttu-id="80f46-245">Se è necessario rimuovere dati dal database per assicurare la coerenza con le operazioni di tipo **DeleteMapping** , occorrerà eseguire queste operazioni separatamente, ma insieme all'uso di questi metodi.</span><span class="sxs-lookup"><span data-stu-id="80f46-245">If data needs to be removed from the database in order to be consistent with **DeleteMapping** operations, you will need to perform those operations separately but in conjunction with using these methods.</span></span>  
* <span data-ttu-id="80f46-246">Per dividere in due gli intervalli esistenti o unire intervalli adiacenti in un unico intervallo, usare **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** e **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="80f46-246">To split existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span></span>  
  
    <span data-ttu-id="80f46-247">Si noti che le operazioni di suddivisione e unione **non modificano la partizione a cui sono mappati i valori di chiave**.</span><span class="sxs-lookup"><span data-stu-id="80f46-247">Note that split and merge operations **do not change the shard to which key values are mapped**.</span></span> <span data-ttu-id="80f46-248">Una suddivisione divide un intervallo esistente in due parti, ma ne mantiene il mapping alla stessa partizione.</span><span class="sxs-lookup"><span data-stu-id="80f46-248">A split breaks an existing range into two parts, but leaves both as mapped to the same shard.</span></span> <span data-ttu-id="80f46-249">Un'unione viene applicata a due intervalli adiacenti già mappati alla stessa partizione e li unisce in un singolo intervallo.</span><span class="sxs-lookup"><span data-stu-id="80f46-249">A merge operates on two adjacent ranges that are already mapped to the same shard, coalescing them into a single range.</span></span>  <span data-ttu-id="80f46-250">Lo spostamento di punti o degli stessi intervalli tra le partizioni deve essere coordinato tramite l'uso di **UpdateMapping** insieme allo spostamento effettivo dei dati.</span><span class="sxs-lookup"><span data-stu-id="80f46-250">The movement of points or ranges themselves between shards needs to be coordinated by using **UpdateMapping** in conjunction with actual data movement.</span></span>  <span data-ttu-id="80f46-251">È possibile usare il servizio di **suddivisione/unione** , incluso nello strumento dei database elastici, per coordinare le modifiche della mappa partizioni con lo spostamento dei dati, nei casi in cui lo spostamento è necessario.</span><span class="sxs-lookup"><span data-stu-id="80f46-251">You can use the **Split/Merge** service that is part of elastic database tools to coordinate shard map changes with data movement, when movement is needed.</span></span> 
* <span data-ttu-id="80f46-252">Per eseguire di nuovo il mapping o spostare singoli punti o intervalli in partizioni diverse, usare **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="80f46-252">To re-map (or move) individual points or ranges to different shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span></span>  
  
    <span data-ttu-id="80f46-253">Poiché potrebbe essere necessario spostare i dati da una partizione a un'altra per mantenerne la coerenza con le operazioni di tipo **UpdateMapping** , occorrerà eseguire separatamente lo spostamento, ma insieme all'uso di questi metodi.</span><span class="sxs-lookup"><span data-stu-id="80f46-253">Since data may need to be moved from one shard to another in order to be consistent with **UpdateMapping** operations, you will need to perform that movement separately but in conjunction with using these methods.</span></span>
* <span data-ttu-id="80f46-254">Per impostare i mapping come online e offline, usare **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** e **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** per controllare lo stato online di un mapping.</span><span class="sxs-lookup"><span data-stu-id="80f46-254">To take mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** to control the online state of a mapping.</span></span> 
  
    <span data-ttu-id="80f46-255">Alcune operazioni sui mapping di partizioni, incluse le operazioni **UpdateMapping** e **DeleteMapping**, sono consentite solo se lo stato del mapping è "offline".</span><span class="sxs-lookup"><span data-stu-id="80f46-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span></span> <span data-ttu-id="80f46-256">Quando un mapping è offline, una richiesta dipendente dai dati e basata su una chiave inclusa nel mapping restituirà un errore.</span><span class="sxs-lookup"><span data-stu-id="80f46-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span></span> <span data-ttu-id="80f46-257">Quando si porta offline per la prima volta un intervallo, inoltre, tutte le connessioni alla partizione interessata verranno terminate automaticamente per evitare risultati incoerenti o incompleti per le query dirette agli intervalli sottoposti a modifica.</span><span class="sxs-lookup"><span data-stu-id="80f46-257">In addition, when a range is first taken offline, all connections to the affected shard are automatically killed in order to prevent inconsistent or incomplete results for queries directed against ranges being changed.</span></span> 

<span data-ttu-id="80f46-258">I mapping sono oggetti non modificabili in .NET.</span><span class="sxs-lookup"><span data-stu-id="80f46-258">Mappings are immutable objects in .Net.</span></span>  <span data-ttu-id="80f46-259">Tutti i metodi precedenti che modificano i mapping invalidano anche tutti i riferimenti ad essi nel codice.</span><span class="sxs-lookup"><span data-stu-id="80f46-259">All of the methods above that change mappings also invalidate any references to them in your code.</span></span> <span data-ttu-id="80f46-260">Per semplificare l’esecuzione di sequenze di operazioni che modificano lo stato di un mapping, tutti i metodi che consentono di modificare un mapping restituiscono un nuovo riferimento di mapping, in modo che le operazioni possano essere concatenate.</span><span class="sxs-lookup"><span data-stu-id="80f46-260">To make it easier to perform sequences of operations that change a mapping’s state, all of the methods that change a mapping return a new mapping reference, so operations can be chained.</span></span> <span data-ttu-id="80f46-261">Ad esempio, per eliminare un mapping esistente in shardmap sm che contiene la chiave 25, è possibile eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="80f46-261">For example, to delete an existing mapping in shardmap sm that contains the key 25, you can execute the following:</span></span> 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a><span data-ttu-id="80f46-262">Aggiunta di una partizione</span><span class="sxs-lookup"><span data-stu-id="80f46-262">Adding a shard</span></span>
<span data-ttu-id="80f46-263">Le applicazioni devono spesso aggiungere semplicemente nuove partizioni per gestire i dati previsti dalle nuove chiavi o dai nuovi intervalli di chiavi, per una mappa partizioni già esistente.</span><span class="sxs-lookup"><span data-stu-id="80f46-263">Applications often need to simply add new shards to handle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="80f46-264">Ad esempio, è possibile che un'applicazione partizionata dall'ID tenant debba eseguire il provisioning di una nuova partizione per un nuovo tenant, oppure è possibile che i dati partizionati ogni mese richiedano il provisioning di una nuova partizione prima dell'inizio di ogni nuovo mese.</span><span class="sxs-lookup"><span data-stu-id="80f46-264">For example, an application sharded by Tenant ID may need to provision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before the start of each new month.</span></span> 

<span data-ttu-id="80f46-265">Se il nuovo intervallo di valori di chiave non è già incluso in un mapping esistente e non è necessario alcuno spostamento di dati, l'aggiunta della nuova partizione e l'associazione della nuova chiave o dell'intervallo a quella partizione risulteranno molto semplici.</span><span class="sxs-lookup"><span data-stu-id="80f46-265">If the new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple to add the new shard and associate the new key or range to that shard.</span></span> <span data-ttu-id="80f46-266">Per informazioni dettagliate sull'aggiunta di nuove partizioni, vedere [Aggiunta di una nuova partizione](sql-database-elastic-scale-add-a-shard.md).</span><span class="sxs-lookup"><span data-stu-id="80f46-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span></span>

<span data-ttu-id="80f46-267">Per gli scenari che richiedono lo spostamento di dati, tuttavia, il servizio di suddivisione-unione è necessario per l'orchestrazione dello spostamento di dati tra le partizioni insieme agli aggiornamenti necessari per la mappa partizioni.</span><span class="sxs-lookup"><span data-stu-id="80f46-267">For scenarios that require data movement, however, the split-merge tool is needed to orchestrate the data movement between shards in combination with the necessary shard map updates.</span></span> <span data-ttu-id="80f46-268">Per informazioni dettagliate sull'uso del servizio di suddivisione-unione, vedere [Panoramica del servizio di suddivisione-unione](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="80f46-268">For details on using the split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
