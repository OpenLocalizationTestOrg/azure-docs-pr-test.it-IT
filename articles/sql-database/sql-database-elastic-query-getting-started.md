---
title: "aaaReport tra i database di cloud di scalabilità orizzontale (partizionamento orizzontale) | Documenti Microsoft"
description: come toouse tra le query di database di database
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="eed9c-103">Creare report in database cloud con numero maggiore di istanze (anteprima)</span><span class="sxs-lookup"><span data-stu-id="eed9c-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="eed9c-104">È possibile creare report da più database SQL di Azure da un unico punto di connessione usando una [query elastica](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eed9c-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="eed9c-105">Hello database deve essere partizionata orizzontalmente (anche noto come "partizionati").</span><span class="sxs-lookup"><span data-stu-id="eed9c-105">hello databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="eed9c-106">Se si dispone di un database esistente, vedere [esistente migrazione database database tooscaled-out](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="eed9c-106">If you have an existing database, see [Migrating existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="eed9c-107">gli oggetti SQL hello toounderstand necessari tooquery, vedere [Query tra database partizionati orizzontalmente](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="eed9c-107">toounderstand hello SQL objects needed tooquery, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eed9c-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="eed9c-108">Prerequisites</span></span>
<span data-ttu-id="eed9c-109">Scaricare ed eseguire hello [Guida introduttiva a esempio di strumenti di Database elastico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eed9c-109">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="eed9c-110">Creare una mappa partizioni gestione tramite app di esempio hello</span><span class="sxs-lookup"><span data-stu-id="eed9c-110">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="eed9c-111">Di seguito si creerà una mappa partizioni manager insieme a diverse partizioni, seguita dall'inserimento di dati in partizioni hello.</span><span class="sxs-lookup"><span data-stu-id="eed9c-111">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="eed9c-112">Se si è verificata tooalready con l'installazione di partizioni con dati partizionati, è possibile passare alla procedura seguente hello e spostare toohello nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="eed9c-112">If you happen tooalready have shards setup with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="eed9c-113">Compilare ed eseguire hello **Introduzione agli strumenti di Database elastico** applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="eed9c-113">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="eed9c-114">Seguire i passaggi di hello fino al passaggio 7 nella sezione hello [scaricare ed eseguire app di esempio hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="eed9c-114">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="eed9c-115">Al fine di hello del passaggio 7, verrà visualizzato un hello prompt dei comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="eed9c-115">At hello end of Step 7, you will see hello following command prompt:</span></span>

    ![Aprire il prompt dei comandi.][1]
2. <span data-ttu-id="eed9c-117">Nella finestra di comando hello, digitare "1" e premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="eed9c-117">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="eed9c-118">Questo gestore mappe partizioni di hello crea e aggiunge due partizioni toohello server.</span><span class="sxs-lookup"><span data-stu-id="eed9c-118">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="eed9c-119">Quindi digitare "3" e premere **invio**; ripetere azione hello quattro volte.</span><span class="sxs-lookup"><span data-stu-id="eed9c-119">Then type "3" and press **Enter**; repeat hello action four times.</span></span> <span data-ttu-id="eed9c-120">Consente di inserire righe di dati di esempio nelle partizioni.</span><span class="sxs-lookup"><span data-stu-id="eed9c-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="eed9c-121">Hello [portale di Azure](https://portal.azure.com) devono essere visualizzati tre nuovi database nel server:</span><span class="sxs-lookup"><span data-stu-id="eed9c-121">hello [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Conferma di Visual Studio][2]

   <span data-ttu-id="eed9c-123">Query tra database a questo punto, sono supportate tramite le librerie client di Database elastico hello.</span><span class="sxs-lookup"><span data-stu-id="eed9c-123">At this point, cross-database queries are supported through hello Elastic Database client libraries.</span></span> <span data-ttu-id="eed9c-124">Nella finestra di comando hello, ad esempio, utilizzare l'opzione 4.</span><span class="sxs-lookup"><span data-stu-id="eed9c-124">For example, use option 4 in hello command window.</span></span> <span data-ttu-id="eed9c-125">Hello risultati da una query su più partizioni sono sempre un **UNION ALL** dei risultati di hello da tutte le partizioni.</span><span class="sxs-lookup"><span data-stu-id="eed9c-125">hello results from a multi-shard query are always a **UNION ALL** of hello results from all shards.</span></span>

   <span data-ttu-id="eed9c-126">Nella sezione successiva hello, si crea un endpoint di database di esempio che supporta più l'esecuzione di query di dati hello tra partizioni.</span><span class="sxs-lookup"><span data-stu-id="eed9c-126">In hello next section, we create a sample database endpoint that supports richer querying of hello data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="eed9c-127">Creare un database di query elastico</span><span class="sxs-lookup"><span data-stu-id="eed9c-127">Create an elastic query database</span></span>
1. <span data-ttu-id="eed9c-128">Aprire hello [portale di Azure](https://portal.azure.com) ed effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="eed9c-128">Open hello [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="eed9c-129">Creare un nuovo database SQL di Azure in hello nello stesso server di configurazione del partizionamento.</span><span class="sxs-lookup"><span data-stu-id="eed9c-129">Create a new Azure SQL database in hello same server as your shard setup.</span></span> <span data-ttu-id="eed9c-130">Nome database hello "ElasticDBQuery".</span><span class="sxs-lookup"><span data-stu-id="eed9c-130">Name hello database "ElasticDBQuery."</span></span>

    ![Portale di Azure e il livello di prezzo][3]

    > [!NOTE]
    > <span data-ttu-id="eed9c-132">È possibile usare un database esistente.</span><span class="sxs-lookup"><span data-stu-id="eed9c-132">you can use an existing database.</span></span> <span data-ttu-id="eed9c-133">Se è possibile farlo, non deve essere una delle partizioni hello che si desidera tooexecute nella query.</span><span class="sxs-lookup"><span data-stu-id="eed9c-133">If you can do so, it must not be one of hello shards that you would like tooexecute your queries on.</span></span> <span data-ttu-id="eed9c-134">Questo database verrà utilizzato per la creazione di oggetti di metadati per una query di database elastico hello.</span><span class="sxs-lookup"><span data-stu-id="eed9c-134">This database will be used for creating hello metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="eed9c-135">Creare oggetti di database</span><span class="sxs-lookup"><span data-stu-id="eed9c-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="eed9c-136">Chiave master con ambito database e credenziali</span><span class="sxs-lookup"><span data-stu-id="eed9c-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="eed9c-137">Si tratta di gestore mappe partizioni di toohello tooconnect utilizzato e partizioni hello:</span><span class="sxs-lookup"><span data-stu-id="eed9c-137">These are used tooconnect toohello shard map manager and hello shards:</span></span>

1. <span data-ttu-id="eed9c-138">Apri SQL Server Management Studio e SQL Server Data Tools in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eed9c-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="eed9c-139">La connessione a database tooElasticDBQuery ed eseguire hello comandi T-SQL seguente:</span><span class="sxs-lookup"><span data-stu-id="eed9c-139">Connect tooElasticDBQuery database and execute hello following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="eed9c-140">"nomeutente" e "password" deve essere hello stesso come informazioni di accesso utilizzate nel passaggio 6 di [scaricare ed eseguire app di esempio hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Introduzione agli strumenti di database elastico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eed9c-140">"username" and "password" should be hello same as login information used in step 6 of [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="eed9c-141">DROP EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="eed9c-141">External data sources</span></span>
<span data-ttu-id="eed9c-142">toocreate un'origine dati esterna, eseguire comando seguente sul database ElasticDBQuery hello hello:</span><span class="sxs-lookup"><span data-stu-id="eed9c-142">toocreate an external data source, execute hello following command on hello ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="eed9c-143">"CustomerIDShardMap" è il nome di hello della mappa partizioni hello, se è stato creato mappa partizioni hello e mappa partizioni manager utilizzando l'esempio di strumenti di database elastico hello.</span><span class="sxs-lookup"><span data-stu-id="eed9c-143">"CustomerIDShardMap" is hello name of hello shard map, if you created hello shard map and shard map manager using hello elastic database tools sample.</span></span> <span data-ttu-id="eed9c-144">Tuttavia, se si utilizza il programma di installazione personalizzato per questo esempio, deve essere nome mappa partizioni di hello che scelto nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eed9c-144">However, if you used your custom setup for this sample, then it should be hello shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="eed9c-145">Tabelle esterne</span><span class="sxs-lookup"><span data-stu-id="eed9c-145">External tables</span></span>
<span data-ttu-id="eed9c-146">Creare una tabella esterna corrispondente tabella Customers hello su partizioni hello eseguendo hello comando seguente sul database ElasticDBQuery:</span><span class="sxs-lookup"><span data-stu-id="eed9c-146">Create an external table that matches hello Customers table on hello shards by executing hello following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="eed9c-147">Eseguire una query di esempio elastica database T-SQL</span><span class="sxs-lookup"><span data-stu-id="eed9c-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="eed9c-148">Dopo aver definito l'origine dati esterna e le tabelle esterne è ora possibile utilizzare T-SQL completa tramite le tabelle esterne.</span><span class="sxs-lookup"><span data-stu-id="eed9c-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="eed9c-149">Eseguire la query sul database ElasticDBQuery hello:</span><span class="sxs-lookup"><span data-stu-id="eed9c-149">Execute this query on hello ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="eed9c-150">Si noterà che eseguono query hello aggrega i risultati di tutte le partizioni hello e offre hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="eed9c-150">You will notice that hello query aggregates results from all hello shards and gives hello following output:</span></span>

![Dettagli dell'output][4]

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="eed9c-152">Importare tooExcel risultati query di database elastico</span><span class="sxs-lookup"><span data-stu-id="eed9c-152">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="eed9c-153">È possibile importare i risultati di hello da di un file di Excel tooan query.</span><span class="sxs-lookup"><span data-stu-id="eed9c-153">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="eed9c-154">Avviare Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="eed9c-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="eed9c-155">Passare toohello **dati** della barra multifunzione.</span><span class="sxs-lookup"><span data-stu-id="eed9c-155">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="eed9c-156">Fare clic su **Da altre origini** e quindi su **Da SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="eed9c-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importazione di Excel da altre origini][5]
4. <span data-ttu-id="eed9c-158">In hello **connessione guidata dati** digitare le credenziali di nome e l'account di accesso server hello.</span><span class="sxs-lookup"><span data-stu-id="eed9c-158">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="eed9c-159">Quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="eed9c-159">Then click **Next**.</span></span>
5. <span data-ttu-id="eed9c-160">Nella finestra di dialogo hello **database selezionare hello che contiene dati hello da**selezionare hello **ElasticDBQuery** database.</span><span class="sxs-lookup"><span data-stu-id="eed9c-160">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="eed9c-161">Seleziona hello **clienti** tabella nella visualizzazione elenco hello e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="eed9c-161">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="eed9c-162">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="eed9c-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="eed9c-163">In hello **l'importazione dei dati** del modulo **selezionare la modalità tooview questi dati nella cartella di lavoro**selezionare **tabella** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="eed9c-163">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="eed9c-164">Tutte le righe di hello **clienti** tabella, archiviata in partizioni diverse popolare un foglio di Excel hello.</span><span class="sxs-lookup"><span data-stu-id="eed9c-164">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

<span data-ttu-id="eed9c-165">È ora possibile utilizzare funzioni di visualizzazione avanzata dei dati di Excel.</span><span class="sxs-lookup"><span data-stu-id="eed9c-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="eed9c-166">È possibile utilizzare la stringa di connessione hello con il nome del server, nome del database e credenziali tooconnect BI e dati integrazione strumenti toohello elastico query database.</span><span class="sxs-lookup"><span data-stu-id="eed9c-166">You can use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="eed9c-167">Assicurarsi che SQL Server sia supportato come origine dati per lo strumento.</span><span class="sxs-lookup"><span data-stu-id="eed9c-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="eed9c-168">È possibile fare riferimento a database elastico query toohello e le tabelle esterne come qualsiasi altro database di SQL Server e le tabelle di SQL Server si connetterà toowith lo strumento.</span><span class="sxs-lookup"><span data-stu-id="eed9c-168">You can refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="eed9c-169">Costi</span><span class="sxs-lookup"><span data-stu-id="eed9c-169">Cost</span></span>
<span data-ttu-id="eed9c-170">Non è senza costi aggiuntivi per l'utilizzo di funzionalità di Query di Database elastico hello.</span><span class="sxs-lookup"><span data-stu-id="eed9c-170">There is no additional charge for using hello Elastic Database Query feature.</span></span>

<span data-ttu-id="eed9c-171">Per informazioni sui prezzi, vedere [Dettagli prezzi del database SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="eed9c-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eed9c-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eed9c-172">Next steps</span></span>

* <span data-ttu-id="eed9c-173">Per un approfondimento, vedere [Panoramica delle query elastiche](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eed9c-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="eed9c-174">Per un'esercitazione sul partizionamento verticale, vedere [Introduzione alle query tra database (partizionamento verticale)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="eed9c-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="eed9c-175">Per le query di esempio e sintassi per i dati con partizionamento verticale, vedere [Eseguire query su dati con partizionamento verticale](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="eed9c-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="eed9c-176">Per le query di esempio e sintassi per i dati con partizionamento orizzontale, vedere [Eseguire query su dati con partizionamento orizzontale](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="eed9c-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="eed9c-177">Vedere [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) per una stored procedure che esegue un'istruzione Transact-SQL su un singolo database SQL di Azure remoto o un set di database che fungono da partizioni in uno schema di partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="eed9c-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
