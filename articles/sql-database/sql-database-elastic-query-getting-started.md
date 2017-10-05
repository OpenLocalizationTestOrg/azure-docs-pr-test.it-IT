---
title: "Creare report in database cloud con scalabilità orizzontale (partizionamento orizzontale) | Documentazione Microsoft"
description: come utilizzare tra le query di database tra database
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
ms.openlocfilehash: 8eb56d44c3a261f6325d4fc91f169d09bf108160
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="d31b9-103">Creare report in database cloud con numero maggiore di istanze (anteprima)</span><span class="sxs-lookup"><span data-stu-id="d31b9-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="d31b9-104">È possibile creare report da più database SQL di Azure da un unico punto di connessione usando una [query elastica](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d31b9-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="d31b9-105">Il database deve essere con partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="d31b9-105">The databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="d31b9-106">Se si ha un database esistente, vedere [Migrazione dei database esistenti in database con un numero maggiore di istanze](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="d31b9-106">If you have an existing database, see [Migrating existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="d31b9-107">Per comprendere quali sono gli oggetti SQL necessari per eseguire una query, vedere [Eseguire query in database con partizionamento orizzontale](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="d31b9-107">To understand the SQL objects needed to query, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d31b9-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d31b9-108">Prerequisites</span></span>
<span data-ttu-id="d31b9-109">Scaricare ed eseguire [Introduzione allo strumento di esempio del Database elastico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d31b9-109">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="d31b9-110">Creare un gestore mappe partizione utilizzando l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="d31b9-110">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="d31b9-111">Di seguito si creerà un gestore mappe partizione con diverse partizioni, seguita dall'inserimento di dati nelle partizioni.</span><span class="sxs-lookup"><span data-stu-id="d31b9-111">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="d31b9-112">Se si dispone già di programma di installazione di partizioni con dati partizionati in essi, è possibile ignorare i passaggi seguenti e passare alla sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="d31b9-112">If you happen to already have shards setup with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="d31b9-113">Compilare ed eseguire l’applicazione di esempio **Introduzione agli strumenti del Database elastico** .</span><span class="sxs-lookup"><span data-stu-id="d31b9-113">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="d31b9-114">Seguire la procedura fino al passaggio 7 nella sezione [Scaricare ed eseguire l'app di esempio](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="d31b9-114">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="d31b9-115">Alla fine del passaggio 7, verrà visualizzato il seguente prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="d31b9-115">At the end of Step 7, you will see the following command prompt:</span></span>

    ![Aprire il prompt dei comandi.][1]
2. <span data-ttu-id="d31b9-117">Nella finestra di comando, digitare "1" e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="d31b9-117">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="d31b9-118">Viene creato il gestore delle mappe partizioni e aggiunge due partizioni al server.</span><span class="sxs-lookup"><span data-stu-id="d31b9-118">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="d31b9-119">Digitare "3" e premere **Invio**; ripetere l'azione quattro volte.</span><span class="sxs-lookup"><span data-stu-id="d31b9-119">Then type "3" and press **Enter**; repeat the action four times.</span></span> <span data-ttu-id="d31b9-120">Consente di inserire righe di dati di esempio nelle partizioni.</span><span class="sxs-lookup"><span data-stu-id="d31b9-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="d31b9-121">Il [portale di Azure](https://portal.azure.com) dovrebbe mostrare tre nuovi database nel server:</span><span class="sxs-lookup"><span data-stu-id="d31b9-121">The [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Conferma di Visual Studio][2]

   <span data-ttu-id="d31b9-123">A questo punto, le query tra database sono supportate tramite le risorse del client del Database elastico.</span><span class="sxs-lookup"><span data-stu-id="d31b9-123">At this point, cross-database queries are supported through the Elastic Database client libraries.</span></span> <span data-ttu-id="d31b9-124">Nella finestra di comando, ad esempio, utilizzare l'opzione 4.</span><span class="sxs-lookup"><span data-stu-id="d31b9-124">For example, use option 4 in the command window.</span></span> <span data-ttu-id="d31b9-125">I risultati di una query con più partizioni sono sempre un **UNION ALL** dei risultati di tutte le partizioni.</span><span class="sxs-lookup"><span data-stu-id="d31b9-125">The results from a multi-shard query are always a **UNION ALL** of the results from all shards.</span></span>

   <span data-ttu-id="d31b9-126">Nella sezione successiva, verrà creato un endpoint del database di esempio che supporta l'esecuzione più completa delle query dei dati tra partizioni.</span><span class="sxs-lookup"><span data-stu-id="d31b9-126">In the next section, we create a sample database endpoint that supports richer querying of the data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="d31b9-127">Creare un database di query elastico</span><span class="sxs-lookup"><span data-stu-id="d31b9-127">Create an elastic query database</span></span>
1. <span data-ttu-id="d31b9-128">Aprire il [portale di Azure](https://portal.azure.com) ed eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="d31b9-128">Open the [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="d31b9-129">Creare un nuovo database SQL Azure nello stesso server del programma di installazione del partizionamento.</span><span class="sxs-lookup"><span data-stu-id="d31b9-129">Create a new Azure SQL database in the same server as your shard setup.</span></span> <span data-ttu-id="d31b9-130">Denominare il database "ElasticDBQuery".</span><span class="sxs-lookup"><span data-stu-id="d31b9-130">Name the database "ElasticDBQuery."</span></span>

    ![Portale di Azure e il livello di prezzo][3]

    > [!NOTE]
    > <span data-ttu-id="d31b9-132">È possibile usare un database esistente.</span><span class="sxs-lookup"><span data-stu-id="d31b9-132">you can use an existing database.</span></span> <span data-ttu-id="d31b9-133">Se è possibile farlo, non deve essere una delle partizioni su cui si desidera eseguire la query.</span><span class="sxs-lookup"><span data-stu-id="d31b9-133">If you can do so, it must not be one of the shards that you would like to execute your queries on.</span></span> <span data-ttu-id="d31b9-134">Questo database verrà utilizzato per la creazione di oggetti di metadati per una query di database elastico.</span><span class="sxs-lookup"><span data-stu-id="d31b9-134">This database will be used for creating the metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="d31b9-135">Creare oggetti di database</span><span class="sxs-lookup"><span data-stu-id="d31b9-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="d31b9-136">Chiave master con ambito database e credenziali</span><span class="sxs-lookup"><span data-stu-id="d31b9-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="d31b9-137">Questi vengono utilizzati per la connessione per la gestione di gestore di mappe di partizioni e partizioni:</span><span class="sxs-lookup"><span data-stu-id="d31b9-137">These are used to connect to the shard map manager and the shards:</span></span>

1. <span data-ttu-id="d31b9-138">Apri SQL Server Management Studio e SQL Server Data Tools in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d31b9-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="d31b9-139">Connettersi al database ElasticDBQuery ed eseguire i comandi T-SQL seguenti:</span><span class="sxs-lookup"><span data-stu-id="d31b9-139">Connect to ElasticDBQuery database and execute the following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="d31b9-140">"nome utente" e "password" devono essere uguali alle informazioni di accesso usate nel passaggio 6 della sezione [Scaricare ed eseguire l'app di esempio](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Iniziare a utilizzare gli strumenti di database elastici](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d31b9-140">"username" and "password" should be the same as login information used in step 6 of [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="d31b9-141">DROP EXTERNAL DATA SOURCE</span><span class="sxs-lookup"><span data-stu-id="d31b9-141">External data sources</span></span>
<span data-ttu-id="d31b9-142">Per creare un'origine dati esterna, eseguire il comando seguente sul database ElasticDBQuery:</span><span class="sxs-lookup"><span data-stu-id="d31b9-142">To create an external data source, execute the following command on the ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="d31b9-143">"CustomerIDShardMap" è il nome della mappa del partizionamento, se è stato creato il mapping della partizione e la gestione di mapping di partizione utilizzando l'esempio di strumenti di database flessibile.</span><span class="sxs-lookup"><span data-stu-id="d31b9-143">"CustomerIDShardMap" is the name of the shard map, if you created the shard map and shard map manager using the elastic database tools sample.</span></span> <span data-ttu-id="d31b9-144">Tuttavia, se si utilizza il programma di installazione personalizzato per questo esempio, deve essere il nome di mappa partizionamento che scelto nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d31b9-144">However, if you used your custom setup for this sample, then it should be the shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="d31b9-145">Tabelle esterne</span><span class="sxs-lookup"><span data-stu-id="d31b9-145">External tables</span></span>
<span data-ttu-id="d31b9-146">Creare una tabella esterna corrispondente della tabella Customers nelle partizioni eseguendo il comando seguente sul database ElasticDBQuery:</span><span class="sxs-lookup"><span data-stu-id="d31b9-146">Create an external table that matches the Customers table on the shards by executing the following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="d31b9-147">Eseguire una query di esempio elastica database T-SQL</span><span class="sxs-lookup"><span data-stu-id="d31b9-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="d31b9-148">Dopo aver definito l'origine dati esterna e le tabelle esterne è ora possibile utilizzare T-SQL completa tramite le tabelle esterne.</span><span class="sxs-lookup"><span data-stu-id="d31b9-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="d31b9-149">Eseguire questa query sul database ElasticDBQuery:</span><span class="sxs-lookup"><span data-stu-id="d31b9-149">Execute this query on the ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="d31b9-150">Si noterà che la query di aggregare i risultati di tutte le partizioni e produce il seguente output:</span><span class="sxs-lookup"><span data-stu-id="d31b9-150">You will notice that the query aggregates results from all the shards and gives the following output:</span></span>

![Dettagli dell'output][4]

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="d31b9-152">Importare i risultati della query database elastica in Excel</span><span class="sxs-lookup"><span data-stu-id="d31b9-152">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="d31b9-153">È possibile importare i risultati da di una query a un file di Excel.</span><span class="sxs-lookup"><span data-stu-id="d31b9-153">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="d31b9-154">Avviare Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="d31b9-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="d31b9-155">Individuare il **dati** della barra multifunzione.</span><span class="sxs-lookup"><span data-stu-id="d31b9-155">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="d31b9-156">Fare clic su **Da altre origini** e quindi su **Da SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="d31b9-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importazione di Excel da altre origini][5]
4. <span data-ttu-id="d31b9-158">In **Connessione guidata dati** digitare le credenziali di accesso e il nome del server.</span><span class="sxs-lookup"><span data-stu-id="d31b9-158">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="d31b9-159">Quindi fare clic su **Next**.</span><span class="sxs-lookup"><span data-stu-id="d31b9-159">Then click **Next**.</span></span>
5. <span data-ttu-id="d31b9-160">Nella finestra di dialogo **Selezionare il database contenente i dati desiderati** selezionare il database **ElasticDBQuery**.</span><span class="sxs-lookup"><span data-stu-id="d31b9-160">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="d31b9-161">Selezionare la tabella **Customers** nella visualizzazione elenco e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d31b9-161">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="d31b9-162">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="d31b9-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="d31b9-163">Nel modulo **Importa dati** in **Specificare come visualizzare i dati nella cartella di lavoro** selezionare **Tabella** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d31b9-163">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="d31b9-164">Tutte le righe dalla tabella **Clienti** , archiviate in diverse partizioni sono riportate nel foglio Excel.</span><span class="sxs-lookup"><span data-stu-id="d31b9-164">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

<span data-ttu-id="d31b9-165">È ora possibile utilizzare funzioni di visualizzazione avanzata dei dati di Excel.</span><span class="sxs-lookup"><span data-stu-id="d31b9-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="d31b9-166">È possibile utilizzare la stringa di connessione con il nome del server, nome del database e credenziali per gli strumenti di integrazione di Business Intelligence e i dati di connettersi al database query elastica.</span><span class="sxs-lookup"><span data-stu-id="d31b9-166">You can use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="d31b9-167">Assicurarsi che SQL Server sia supportato come origine dati per lo strumento.</span><span class="sxs-lookup"><span data-stu-id="d31b9-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="d31b9-168">È possibile fare riferimento al database elastica query e tabelle esterne come qualsiasi altro database di SQL Server e tabelle di SQL Server è necessario connettersi allo strumento.</span><span class="sxs-lookup"><span data-stu-id="d31b9-168">You can refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="d31b9-169">Costi</span><span class="sxs-lookup"><span data-stu-id="d31b9-169">Cost</span></span>
<span data-ttu-id="d31b9-170">Non esiste senza alcun costo aggiuntivo per utilizzare la funzione elastica Query del Database.</span><span class="sxs-lookup"><span data-stu-id="d31b9-170">There is no additional charge for using the Elastic Database Query feature.</span></span>

<span data-ttu-id="d31b9-171">Per informazioni sui prezzi, vedere [Dettagli prezzi del database SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="d31b9-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d31b9-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d31b9-172">Next steps</span></span>

* <span data-ttu-id="d31b9-173">Per un approfondimento, vedere [Panoramica delle query elastiche](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d31b9-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="d31b9-174">Per un'esercitazione sul partizionamento verticale, vedere [Introduzione alle query tra database (partizionamento verticale)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="d31b9-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="d31b9-175">Per le query di esempio e sintassi per i dati con partizionamento verticale, vedere [Eseguire query su dati con partizionamento verticale](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="d31b9-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="d31b9-176">Per le query di esempio e sintassi per i dati con partizionamento orizzontale, vedere [Eseguire query su dati con partizionamento orizzontale](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="d31b9-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="d31b9-177">Vedere [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) per una stored procedure che esegue un'istruzione Transact-SQL su un singolo database SQL di Azure remoto o un set di database che fungono da partizioni in uno schema di partizionamento orizzontale.</span><span class="sxs-lookup"><span data-stu-id="d31b9-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
