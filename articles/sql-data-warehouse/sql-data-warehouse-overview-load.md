---
title: Caricare i dati in Azure SQL Data Warehouse | Microsoft Docs
description: "Informazioni sugli scenari comuni per il caricamento dei dati in SQL Data Warehouse. Questi includono l'uso di PolyBase, dell’archiviazione BLOB di Azure, di file flat e l’invio dei dischi. È anche possibile usare strumenti di terze parti."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: c4199a387f5cdbd477a5e348e48ba8e8b5900075
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="9d49a-105">Caricare i dati in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="9d49a-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="9d49a-106">Riepilogo delle opzioni di scenario e consigli per il caricamento dei dati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d49a-106">A summary of the scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="9d49a-107">La parte più difficile del caricamento dei dati è in genere la preparazione dei dati per il caricamento.</span><span class="sxs-lookup"><span data-stu-id="9d49a-107">The hardest part of loading data is usually preparing the data for the load.</span></span> <span data-ttu-id="9d49a-108">Azure semplifica il caricamento usando l’archiviazione BLOB come archivio dati comune per molti servizi e Azure Data Factory per orchestrare la comunicazione e lo spostamento dei dati tra i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="9d49a-108">Azure simplifies loading by using Azure blob storage as a common data store for many of the services, and using Azure Data Factory to orchestrate communication and data movement between the Azure services.</span></span> <span data-ttu-id="9d49a-109">Questi processi sono integrati con la tecnologia PolyBase che usa l'elaborazione parallela massiva (MPP) per caricare i dati in parallelo dall’archiviazione BLOB di Azure in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d49a-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) to load data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="9d49a-110">Per esercitazioni in cui vengono caricati database di esempio, vedere [Caricare i dati di esempio in SQL Data Warehouse][Load sample databases].</span><span class="sxs-lookup"><span data-stu-id="9d49a-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="9d49a-111">Caricare i dati dall’archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="9d49a-111">Load from Azure blob storage</span></span>
<span data-ttu-id="9d49a-112">Il modo più rapido per importare dati in SQL Data Warehouse consiste nell'usare PolyBase per caricare i dati dall'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="9d49a-112">The fastest way to import data into SQL Data Warehouse is to use PolyBase to load data from Azure blob storage.</span></span> <span data-ttu-id="9d49a-113">PolyBase usa la progettazione di elaborazione parallela massiva (MPP) di SQL Data Warehouse per caricare dati in parallelo dall’archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="9d49a-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design to load data in parallel from Azure blob storage.</span></span> <span data-ttu-id="9d49a-114">Per usare PolyBase, è possibile usare i comandi T-SQL o una pipeline di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9d49a-114">To use PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="9d49a-115">1. Usare PolyBase e T-SQL</span><span class="sxs-lookup"><span data-stu-id="9d49a-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="9d49a-116">Riepilogo del processo di caricamento:</span><span class="sxs-lookup"><span data-stu-id="9d49a-116">Summary of loading process:</span></span>

1. <span data-ttu-id="9d49a-117">Spostare i dati in Archiviazione BLOB di Azure o Azure Data Lake Store e archiviarli in file di testo.</span><span class="sxs-lookup"><span data-stu-id="9d49a-117">Move your data to Azure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="9d49a-118">Configurare gli oggetti esterni in SQL Data Warehouse per definire il percorso e il formato dei dati.</span><span class="sxs-lookup"><span data-stu-id="9d49a-118">Configure external objects in SQL Data Warehouse to define the location and format of the data</span></span>
3. <span data-ttu-id="9d49a-119">Eseguire un comando T-SQL per caricare i dati in parallelo in una nuova tabella di database.</span><span class="sxs-lookup"><span data-stu-id="9d49a-119">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="9d49a-120">Per un'esercitazione, vedere [Caricare dati dall'archivio BLOB di Azure in SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="9d49a-120">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="9d49a-121">2. Usare Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9d49a-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="9d49a-122">Per usare PolyBase in modo più semplice, è possibile creare una pipeline di Azure Data Factory che usa PolyBase per caricare i dati dall'archiviazione BLOB di Azure in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d49a-122">For a simpler way to use PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase to load data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="9d49a-123">Si tratta di un’operazione rapida da configurare poiché non è necessario definire gli oggetti T-SQL.</span><span class="sxs-lookup"><span data-stu-id="9d49a-123">This is fast to configure since you don't need to define the T-SQL objects.</span></span> <span data-ttu-id="9d49a-124">Se è necessario eseguire query sui dati esterni senza importarli, usare T-SQL.</span><span class="sxs-lookup"><span data-stu-id="9d49a-124">If you need to query the external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="9d49a-125">Riepilogo del processo di caricamento:</span><span class="sxs-lookup"><span data-stu-id="9d49a-125">Summary of loading process:</span></span>

1. <span data-ttu-id="9d49a-126">Spostare i dati nell’archiviazione BLOB di Azure e archiviarli in file di testo.</span><span class="sxs-lookup"><span data-stu-id="9d49a-126">Move your data to Azure blob storage and store it in text files.</span></span> <span data-ttu-id="9d49a-127">Azure Data Factory attualmente non supporta la connettività ADLS con PolyBase.</span><span class="sxs-lookup"><span data-stu-id="9d49a-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="9d49a-128">Creare una pipeline di Azure Data Factory per l'inserimento dei dati.</span><span class="sxs-lookup"><span data-stu-id="9d49a-128">Create an Azure Data Factory pipeline to ingest the data.</span></span> <span data-ttu-id="9d49a-129">Usare l'opzione PolyBase.</span><span class="sxs-lookup"><span data-stu-id="9d49a-129">Use the PolyBase option.</span></span>
4. <span data-ttu-id="9d49a-130">Pianificare ed eseguire la pipeline.</span><span class="sxs-lookup"><span data-stu-id="9d49a-130">Schedule and run the pipeline.</span></span>

<span data-ttu-id="9d49a-131">Per un'esercitazione, vedere [Caricare i dati dall'archivio BLOB di Azure in Azure SQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span><span class="sxs-lookup"><span data-stu-id="9d49a-131">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="9d49a-132">Caricare i dati da SQL Server</span><span class="sxs-lookup"><span data-stu-id="9d49a-132">Load from SQL Server</span></span>
<span data-ttu-id="9d49a-133">Per caricare i dati da SQL Server in SQL Data Warehouse, è possibile usare SQL Server Integration Services (SSIS), trasferire file flat o inviare i dischi a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9d49a-133">To load data from SQL Server to SQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks to Microsoft.</span></span> <span data-ttu-id="9d49a-134">Continuare a leggere per un riepilogo dei diversi processi di caricamento e i collegamenti alle relative esercitazioni.</span><span class="sxs-lookup"><span data-stu-id="9d49a-134">Read on to see a summary of the different loading processes and links to tutorials.</span></span>

<span data-ttu-id="9d49a-135">Per pianificare una migrazione completa dei dati da SQL Server a SQL Data Warehouse, vedere [Eseguire la migrazione della soluzione in SQL Data Warehouse][Migration overview].</span><span class="sxs-lookup"><span data-stu-id="9d49a-135">To plan a full data migration from SQL Server to SQL Data Warehouse, see the [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="9d49a-136">Usare SQL Server Integration Services (SSIS)</span><span class="sxs-lookup"><span data-stu-id="9d49a-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="9d49a-137">Se già si usano pacchetti di SQL Server Integration Services (SSIS) per il caricamento in SQL Server, è possibile aggiornare i pacchetti in modo da usare SQL Server come origine e SQL Data Warehouse come destinazione.</span><span class="sxs-lookup"><span data-stu-id="9d49a-137">If you are already using Integration Services (SSIS) packages to load into SQL Server, you can update your packages to use SQL Server as the source and SQL Data Warehouse as the destination.</span></span> <span data-ttu-id="9d49a-138">Si tratta di un’operazione semplice e veloce ed è un'ottima scelta se non si sta tentando di eseguire la migrazione del processo di caricamento per usare dati già presenti nel cloud.</span><span class="sxs-lookup"><span data-stu-id="9d49a-138">This is quick and easy to do, and is a good choice if you are not trying to migrate your loading process to use data already in the cloud.</span></span> <span data-ttu-id="9d49a-139">Il caricamento sarà tuttavia più lento rispetto all'uso di PolyBase poiché SSIS non esegue il caricamento in parallelo.</span><span class="sxs-lookup"><span data-stu-id="9d49a-139">The tradeoff is the load will be slower than using PolyBase because this SSIS does not perform the load in parallel.</span></span>

<span data-ttu-id="9d49a-140">Riepilogo del processo di caricamento:</span><span class="sxs-lookup"><span data-stu-id="9d49a-140">Summary of loading process:</span></span>

1. <span data-ttu-id="9d49a-141">Modificare il pacchetto SSIS in modo da puntare all'istanza di SQL Server per l'origine e al database di SQL Data Warehouse per la destinazione.</span><span class="sxs-lookup"><span data-stu-id="9d49a-141">Revise your Integration Services package to point to the SQL Server instance for the source and the SQL Data Warehouse database for the destination.</span></span>
2. <span data-ttu-id="9d49a-142">Eseguire la migrazione dello schema in SQL Data Warehouse se non è già presente.</span><span class="sxs-lookup"><span data-stu-id="9d49a-142">Migrate your schema to SQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="9d49a-143">Modificare il mapping nei pacchetti usando solo i tipi di dati supportati da SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d49a-143">Change the mapping in your packages use only the data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="9d49a-144">Pianificare ed eseguire il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9d49a-144">Schedule and run the package.</span></span>

<span data-ttu-id="9d49a-145">Per un'esercitazione, vedere [Caricare dati da SQL Server in Azure SQL Data Warehouse (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span><span class="sxs-lookup"><span data-stu-id="9d49a-145">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="9d49a-146">Usare AZCopy (scelta consigliata per i dati < 10 TB)</span><span class="sxs-lookup"><span data-stu-id="9d49a-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="9d49a-147">Se la dimensione dei dati è < 10 TB, è possibile esportarli da SQL Server in file flat, copiare i file nell’archiviazione BLOB di Azure e quindi usare PolyBase per caricare i dati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d49a-147">If your data size is < 10 TB, you can export the data from SQL Server to flat files, copy the files to Azure blob storage, and then use PolyBase to load the data into SQL Data Warehouse</span></span>

<span data-ttu-id="9d49a-148">Riepilogo del processo di caricamento:</span><span class="sxs-lookup"><span data-stu-id="9d49a-148">Summary of loading process:</span></span>

1. <span data-ttu-id="9d49a-149">Usare l'utilità della riga di comando bcp per esportare i dati da SQL Server in file flat.</span><span class="sxs-lookup"><span data-stu-id="9d49a-149">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="9d49a-150">Usare l'utilità della riga di comando AZCopy per copiare i dati dai file flat nell’archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="9d49a-150">Use the AZCopy command-line utility to copy data from flat files to Azure blob storage.</span></span>
3. <span data-ttu-id="9d49a-151">Usare PolyBase per caricare i dati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d49a-151">Use PolyBase to load into SQL Data Warehouse.</span></span>

<span data-ttu-id="9d49a-152">Per un'esercitazione, vedere [Caricare dati dall'archivio BLOB di Azure in SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="9d49a-152">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="9d49a-153">Usare bcp</span><span class="sxs-lookup"><span data-stu-id="9d49a-153">Use bcp</span></span>
<span data-ttu-id="9d49a-154">Se si dispone di una piccola quantità di dati, è possibile usare bcp per caricarli direttamente in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d49a-154">If you have a small amount of data you can use bcp to load directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="9d49a-155">Riepilogo del processo di caricamento:</span><span class="sxs-lookup"><span data-stu-id="9d49a-155">Summary of loading process:</span></span>

1. <span data-ttu-id="9d49a-156">Usare l'utilità della riga di comando bcp per esportare i dati da SQL Server in file flat.</span><span class="sxs-lookup"><span data-stu-id="9d49a-156">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="9d49a-157">Usare bcp per caricare i dati dai file flat direttamente in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d49a-157">Use bcp to load data from flat files directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="9d49a-158">Per un'esercitazione, vedere [Caricare dati da SQL Server in Azure SQL Data Warehouse (file flat)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span><span class="sxs-lookup"><span data-stu-id="9d49a-158">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (bcp)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="9d49a-159">Usare il servizio Importazione/Esportazione (scelta consigliata per i dati > 10 TB)</span><span class="sxs-lookup"><span data-stu-id="9d49a-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="9d49a-160">Se la dimensione dei dati è maggioire di 10 TB e si intende spostarli in Azure, è consigliabile usare il servizio di invio di dischi [Importazione/Esportazione][Import/Export].</span><span class="sxs-lookup"><span data-stu-id="9d49a-160">If your data size is > 10 TB and you want to move it to Azure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="9d49a-161">Riepilogo del processo di caricamento</span><span class="sxs-lookup"><span data-stu-id="9d49a-161">Summary of loading process</span></span>

1. <span data-ttu-id="9d49a-162">Usare l'utilità della riga di comando bcp per esportare i dati da SQL Server in file flat su dischi trasferibili.</span><span class="sxs-lookup"><span data-stu-id="9d49a-162">Use the bcp command-line utility to export data from SQL Server to flat files on transferrable disks.</span></span>
2. <span data-ttu-id="9d49a-163">Inviare i dischi a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9d49a-163">Ship the disks to Microsoft.</span></span>
3. <span data-ttu-id="9d49a-164">Microsoft carica i dati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d49a-164">Microsoft loads the data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="9d49a-165">Caricare da HDInsight</span><span class="sxs-lookup"><span data-stu-id="9d49a-165">Load from HDInsight</span></span>
<span data-ttu-id="9d49a-166">SQL Data Warehouse supporta il caricamento di dati da HDInsight tramite PolyBase.</span><span class="sxs-lookup"><span data-stu-id="9d49a-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="9d49a-167">Il processo è lo stesso usato per il caricamento dei dati dall'archivio BLOB di Azure, usando PolyBase per connettersi a HDInsight per caricare i dati.</span><span class="sxs-lookup"><span data-stu-id="9d49a-167">The process is the same as loading data from Azure Blob Storage - using PolyBase to connect to HDInsight to load data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="9d49a-168">1. Usare PolyBase e T-SQL</span><span class="sxs-lookup"><span data-stu-id="9d49a-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="9d49a-169">Riepilogo del processo di caricamento:</span><span class="sxs-lookup"><span data-stu-id="9d49a-169">Summary of loading process:</span></span>

1. <span data-ttu-id="9d49a-170">Spostare i dati in HDInsight e archiviarli nel file di testo, in formato ORC o Parquet.</span><span class="sxs-lookup"><span data-stu-id="9d49a-170">Move your data to HDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="9d49a-171">Configurare gli oggetti esterni in SQL Data Warehouse per definire il percorso e il formato dei dati.</span><span class="sxs-lookup"><span data-stu-id="9d49a-171">Configure external objects in SQL Data Warehouse to define the location and format of the data.</span></span>
3. <span data-ttu-id="9d49a-172">Eseguire un comando T-SQL per caricare i dati in parallelo in una nuova tabella di database.</span><span class="sxs-lookup"><span data-stu-id="9d49a-172">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<span data-ttu-id="9d49a-173">Per un'esercitazione, vedere [Caricare dati dall'archivio BLOB di Azure in SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="9d49a-173">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="9d49a-174">Raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="9d49a-174">Recommendations</span></span>
<span data-ttu-id="9d49a-175">Molti partner Microsoft dispongono di soluzioni di caricamento.</span><span class="sxs-lookup"><span data-stu-id="9d49a-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="9d49a-176">Per altre informazioni, vedere l'elenco dei [partner di soluzioni][solution partners].</span><span class="sxs-lookup"><span data-stu-id="9d49a-176">To find out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="9d49a-177">Se i dati provengono da un'origine non relazionale e si intende caricarli in SQL Data Warehouse, è necessario trasformarli in righe e colonne prima di caricarli.</span><span class="sxs-lookup"><span data-stu-id="9d49a-177">If your data is coming from a non-relational source and you want to load it into SQL Data Warehouse you will need to transform it into rows and columns before you load it.</span></span> <span data-ttu-id="9d49a-178">I dati trasformati non devono essere archiviati in un database e possono essere archiviati in file di testo.</span><span class="sxs-lookup"><span data-stu-id="9d49a-178">The transformed data doesn't need to be stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="9d49a-179">Creare statistiche sui dati appena caricati.</span><span class="sxs-lookup"><span data-stu-id="9d49a-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="9d49a-180">SQL Data Warehouse di Azure non supporta ancora le statistiche di creazione automatica o aggiornamento automatico.</span><span class="sxs-lookup"><span data-stu-id="9d49a-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="9d49a-181">Per ottenere le migliori prestazioni dalle query, è importante creare statistiche per tutte le colonne di tutte le tabelle dopo il primo caricamento o dopo eventuali modifiche sostanziali dei dati.</span><span class="sxs-lookup"><span data-stu-id="9d49a-181">In order to get the best performance from your queries, it's important to create statistics on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="9d49a-182">Per informazioni dettagliate, vedere [Managing statistics on tables in SQL Data Warehouse][Statistics](Gestione delle statistiche nelle tabelle in SQL Data Warehouse).</span><span class="sxs-lookup"><span data-stu-id="9d49a-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d49a-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9d49a-183">Next steps</span></span>
<span data-ttu-id="9d49a-184">Per altri suggerimenti relativi allo sviluppo, vedere la [panoramica sullo sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="9d49a-184">For more development tips, see the [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage to SQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server to Azure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server to Azure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server to Azure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
