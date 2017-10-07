---
title: dati aaaLoad in Azure SQL Data Warehouse | Documenti Microsoft
description: "Informazioni su scenari comuni di hello per i dati durante il caricamento in SQL Data Warehouse. Questi includono l'uso di PolyBase, dell’archiviazione BLOB di Azure, di file flat e l’invio dei dischi. È anche possibile usare strumenti di terze parti."
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
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="c8a7e-105">Caricare i dati in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c8a7e-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="c8a7e-106">Un riepilogo delle opzioni di scenario hello e consigli per il caricamento dei dati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-106">A summary of hello scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="c8a7e-107">parte di più difficile Hello di caricamento dei dati è in genere preparazione dei dati hello carico hello.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-107">hello hardest part of loading data is usually preparing hello data for hello load.</span></span> <span data-ttu-id="c8a7e-108">Azure semplifica il caricamento con l'archiviazione blob di Azure come archivio dati comuni per la maggior parte dei servizi di hello e usando Azure Data Factory tooorchestrate lo spostamento di dati e la comunicazione tra hello servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-108">Azure simplifies loading by using Azure blob storage as a common data store for many of hello services, and using Azure Data Factory tooorchestrate communication and data movement between hello Azure services.</span></span> <span data-ttu-id="c8a7e-109">Questi processi sono integrati con la tecnologia PolyBase che utilizza l'elaborazione parallela massiva dati tooload (. MPP) in parallelo dall'archiviazione blob di Azure in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) tooload data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="c8a7e-110">Per esercitazioni in cui vengono caricati database di esempio, vedere [Caricare i dati di esempio in SQL Data Warehouse][Load sample databases].</span><span class="sxs-lookup"><span data-stu-id="c8a7e-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="c8a7e-111">Caricare i dati dall’archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="c8a7e-111">Load from Azure blob storage</span></span>
<span data-ttu-id="c8a7e-112">Hello più veloce modo tooimport dati in SQL Data Warehouse sono toouse dati tooload PolyBase dall'archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-112">hello fastest way tooimport data into SQL Data Warehouse is toouse PolyBase tooload data from Azure blob storage.</span></span> <span data-ttu-id="c8a7e-113">PolyBase utilizza SQL Data Warehouse elaborazione parallela massiva dati tooload della progettazione (. MPP) in parallelo dall'archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design tooload data in parallel from Azure blob storage.</span></span> <span data-ttu-id="c8a7e-114">toouse PolyBase, è possibile utilizzare i comandi T-SQL o una pipeline di Data Factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-114">toouse PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="c8a7e-115">1. Usare PolyBase e T-SQL</span><span class="sxs-lookup"><span data-stu-id="c8a7e-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="c8a7e-116">Riepilogo del processo di caricamento:</span><span class="sxs-lookup"><span data-stu-id="c8a7e-116">Summary of loading process:</span></span>

1. <span data-ttu-id="c8a7e-117">Spostare l'archiviazione blob di dati tooAzure o archivio Azure Data Lake e archiviarlo nel file di testo.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-117">Move your data tooAzure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="c8a7e-118">Configurare gli oggetti esterni nel percorso di hello toodefine SQL Data Warehouse e il formato dei dati hello</span><span class="sxs-lookup"><span data-stu-id="c8a7e-118">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data</span></span>
3. <span data-ttu-id="c8a7e-119">Eseguire una data di hello tooload comando T-SQL in parallelo in una nuova tabella di database.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-119">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="c8a7e-120">Per un'esercitazione, vedere [caricare dati da tooSQL di archiviazione blob di Azure Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="c8a7e-120">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="c8a7e-121">2. Usare Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c8a7e-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="c8a7e-122">Per un toouse modo più semplice PolyBase, è possibile creare una pipeline di Data Factory di Azure che utilizza dati di PolyBase tooload dall'archiviazione blob di Azure in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-122">For a simpler way toouse PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase tooload data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="c8a7e-123">Si tratta di tooconfigure veloce, poiché non è necessario oggetti T-SQL di toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-123">This is fast tooconfigure since you don't need toodefine hello T-SQL objects.</span></span> <span data-ttu-id="c8a7e-124">Se è necessario dati esterni di hello tooquery senza eseguirne l'importazione, è possibile utilizzare T-SQL.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-124">If you need tooquery hello external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="c8a7e-125">Riepilogo del processo di caricamento:</span><span class="sxs-lookup"><span data-stu-id="c8a7e-125">Summary of loading process:</span></span>

1. <span data-ttu-id="c8a7e-126">Spostare l'archiviazione blob di dati tooAzure e archiviarlo nel file di testo.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-126">Move your data tooAzure blob storage and store it in text files.</span></span> <span data-ttu-id="c8a7e-127">Azure Data Factory attualmente non supporta la connettività ADLS con PolyBase.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="c8a7e-128">Creare una pipeline di Data Factory di Azure tooingest hello dati.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-128">Create an Azure Data Factory pipeline tooingest hello data.</span></span> <span data-ttu-id="c8a7e-129">Utilizzare l'opzione PolyBase hello.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-129">Use hello PolyBase option.</span></span>
4. <span data-ttu-id="c8a7e-130">Pianificare ed eseguire pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-130">Schedule and run hello pipeline.</span></span>

<span data-ttu-id="c8a7e-131">Per un'esercitazione, vedere [caricare dati da tooSQL di archiviazione blob di Azure Data Warehouse (Data Factory di Azure)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span><span class="sxs-lookup"><span data-stu-id="c8a7e-131">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="c8a7e-132">Caricare i dati da SQL Server</span><span class="sxs-lookup"><span data-stu-id="c8a7e-132">Load from SQL Server</span></span>
<span data-ttu-id="c8a7e-133">tooload tooSQL di SQL Server Data Warehouse è possibile utilizzare Integration Services (SSIS), trasferimento di file flat o spedire i dischi tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-133">tooload data from SQL Server tooSQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks tooMicrosoft.</span></span> <span data-ttu-id="c8a7e-134">Continuare a leggere toosee un riepilogo dei diverso durante il caricamento dei processi e i collegamenti tootutorials hello.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-134">Read on toosee a summary of hello different loading processes and links tootutorials.</span></span>

<span data-ttu-id="c8a7e-135">tooplan una migrazione completa di dati da tooSQL di SQL Server Data Warehouse, vedere hello [Cenni preliminari sulla migrazione][Migration overview].</span><span class="sxs-lookup"><span data-stu-id="c8a7e-135">tooplan a full data migration from SQL Server tooSQL Data Warehouse, see hello [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="c8a7e-136">Usare SQL Server Integration Services (SSIS)</span><span class="sxs-lookup"><span data-stu-id="c8a7e-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="c8a7e-137">Se si usa già tooload di pacchetti di Integration Services (SSIS) in SQL Server, è possibile aggiornare il toouse pacchetti SQL Server come origine di hello e SQL Data Warehouse come destinazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-137">If you are already using Integration Services (SSIS) packages tooload into SQL Server, you can update your packages toouse SQL Server as hello source and SQL Data Warehouse as hello destination.</span></span> <span data-ttu-id="c8a7e-138">Questa è un'operazione rapida e semplice toodo, ed è una buona scelta se non si stia tentando toomigrate il caricamento elaborare dati toouse già presenti nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-138">This is quick and easy toodo, and is a good choice if you are not trying toomigrate your loading process toouse data already in hello cloud.</span></span> <span data-ttu-id="c8a7e-139">compromesso di Hello è carico hello risulterà più lenta rispetto all'utilizzo di PolyBase poiché questo SSIS non esegue il carico hello in parallelo.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-139">hello tradeoff is hello load will be slower than using PolyBase because this SSIS does not perform hello load in parallel.</span></span>

<span data-ttu-id="c8a7e-140">Riepilogo del processo di caricamento:</span><span class="sxs-lookup"><span data-stu-id="c8a7e-140">Summary of loading process:</span></span>

1. <span data-ttu-id="c8a7e-141">Modificare l'istanza di SQL Server Integration Services pacchetto toopoint toohello per origine hello e database di SQL Data Warehouse hello per destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-141">Revise your Integration Services package toopoint toohello SQL Server instance for hello source and hello SQL Data Warehouse database for hello destination.</span></span>
2. <span data-ttu-id="c8a7e-142">Eseguire la migrazione del tooSQL dello schema del Data Warehouse, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-142">Migrate your schema tooSQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="c8a7e-143">Modifica associazione hello nei pacchetti di utilizzare solo i tipi di dati di hello sono supportati da SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-143">Change hello mapping in your packages use only hello data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="c8a7e-144">Pianificare ed eseguire il pacchetto di hello.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-144">Schedule and run hello package.</span></span>

<span data-ttu-id="c8a7e-145">Per un'esercitazione, vedere [caricare dati da SQL Server tooAzure SQL Data Warehouse (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span><span class="sxs-lookup"><span data-stu-id="c8a7e-145">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="c8a7e-146">Usare AZCopy (scelta consigliata per i dati < 10 TB)</span><span class="sxs-lookup"><span data-stu-id="c8a7e-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="c8a7e-147">Se la dimensione dei dati è < 10 TB, è possibile esportare dati hello dai file tooflat di SQL Server, copiare l'archiviazione di blob tooAzure file hello e quindi utilizzare i dati di PolyBase tooload hello in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c8a7e-147">If your data size is < 10 TB, you can export hello data from SQL Server tooflat files, copy hello files tooAzure blob storage, and then use PolyBase tooload hello data into SQL Data Warehouse</span></span>

<span data-ttu-id="c8a7e-148">Riepilogo del processo di caricamento:</span><span class="sxs-lookup"><span data-stu-id="c8a7e-148">Summary of loading process:</span></span>

1. <span data-ttu-id="c8a7e-149">Usare hello bcp utilità della riga di comando tooexport dati da file tooflat di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-149">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="c8a7e-150">Utilizzare i dati di hello AZCopy utilità della riga di comando toocopy dall'archiviazione blob tooAzure di file flat.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-150">Use hello AZCopy command-line utility toocopy data from flat files tooAzure blob storage.</span></span>
3. <span data-ttu-id="c8a7e-151">Utilizzare tooload PolyBase in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-151">Use PolyBase tooload into SQL Data Warehouse.</span></span>

<span data-ttu-id="c8a7e-152">Per un'esercitazione, vedere [caricare dati da tooSQL di archiviazione blob di Azure Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="c8a7e-152">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="c8a7e-153">Usare bcp</span><span class="sxs-lookup"><span data-stu-id="c8a7e-153">Use bcp</span></span>
<span data-ttu-id="c8a7e-154">Se si dispone di una piccola quantità di dati è possibile utilizzare bcp tooload direttamente in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-154">If you have a small amount of data you can use bcp tooload directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="c8a7e-155">Riepilogo del processo di caricamento:</span><span class="sxs-lookup"><span data-stu-id="c8a7e-155">Summary of loading process:</span></span>

1. <span data-ttu-id="c8a7e-156">Usare hello bcp utilità della riga di comando tooexport dati da file tooflat di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-156">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="c8a7e-157">Utilizzare bcp tooload da flat i file di dati direttamente tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-157">Use bcp tooload data from flat files directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="c8a7e-158">Per un'esercitazione, vedere [caricare dati da SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span><span class="sxs-lookup"><span data-stu-id="c8a7e-158">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="c8a7e-159">Usare il servizio Importazione/Esportazione (scelta consigliata per i dati > 10 TB)</span><span class="sxs-lookup"><span data-stu-id="c8a7e-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="c8a7e-160">Se la dimensione dei dati è > 10 TB e si desidera toomove è tooAzure, si consiglia di utilizzare il disco di servizio di spedizione [importazione/esportazione][Import/Export].</span><span class="sxs-lookup"><span data-stu-id="c8a7e-160">If your data size is > 10 TB and you want toomove it tooAzure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="c8a7e-161">Riepilogo del processo di caricamento</span><span class="sxs-lookup"><span data-stu-id="c8a7e-161">Summary of loading process</span></span>

1. <span data-ttu-id="c8a7e-162">Utilizzare hello bcp utilità della riga di comando tooexport dati dai file di SQL Server tooflat su dischi trasferibili.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-162">Use hello bcp command-line utility tooexport data from SQL Server tooflat files on transferrable disks.</span></span>
2. <span data-ttu-id="c8a7e-163">Hello spedire i dischi tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-163">Ship hello disks tooMicrosoft.</span></span>
3. <span data-ttu-id="c8a7e-164">Microsoft carica i dati di hello in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c8a7e-164">Microsoft loads hello data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="c8a7e-165">Caricare da HDInsight</span><span class="sxs-lookup"><span data-stu-id="c8a7e-165">Load from HDInsight</span></span>
<span data-ttu-id="c8a7e-166">SQL Data Warehouse supporta il caricamento di dati da HDInsight tramite PolyBase.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="c8a7e-167">il processo di Hello è hello stesso come il caricamento dei dati dall'archiviazione Blob di Azure - utilizzo dati di PolyBase tooconnect tooHDInsight tooload.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-167">hello process is hello same as loading data from Azure Blob Storage - using PolyBase tooconnect tooHDInsight tooload data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="c8a7e-168">1. Usare PolyBase e T-SQL</span><span class="sxs-lookup"><span data-stu-id="c8a7e-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="c8a7e-169">Riepilogo del processo di caricamento:</span><span class="sxs-lookup"><span data-stu-id="c8a7e-169">Summary of loading process:</span></span>

1. <span data-ttu-id="c8a7e-170">Spostare i dati tooHDInsight e archiviarlo nel file di testo, ORC o Parquet formato.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-170">Move your data tooHDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="c8a7e-171">In SQL Data Warehouse toodefine hello percorso e il formato dei dati di hello, configurare gli oggetti esterni.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-171">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data.</span></span>
3. <span data-ttu-id="c8a7e-172">Eseguire una data di hello tooload comando T-SQL in parallelo in una nuova tabella di database.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-172">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<span data-ttu-id="c8a7e-173">Per un'esercitazione, vedere [caricare dati da tooSQL di archiviazione blob di Azure Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="c8a7e-173">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="c8a7e-174">Raccomandazioni</span><span class="sxs-lookup"><span data-stu-id="c8a7e-174">Recommendations</span></span>
<span data-ttu-id="c8a7e-175">Molti partner Microsoft dispongono di soluzioni di caricamento.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="c8a7e-176">toofind altre informazioni, vedere un elenco dei nostri [partner delle soluzioni][solution partners].</span><span class="sxs-lookup"><span data-stu-id="c8a7e-176">toofind out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="c8a7e-177">Se i dati provenienti da un'origine non relazionali e si desidera tooload in SQL Data Warehouse è necessario tootransform in righe e colonne prima di caricarli.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-177">If your data is coming from a non-relational source and you want tooload it into SQL Data Warehouse you will need tootransform it into rows and columns before you load it.</span></span> <span data-ttu-id="c8a7e-178">i dati di Hello trasformato non devono toobe archiviati in un database, possono essere archiviato nei file di testo.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-178">hello transformed data doesn't need toobe stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="c8a7e-179">Creare statistiche sui dati appena caricati.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="c8a7e-180">SQL Data Warehouse di Azure non supporta ancora le statistiche di creazione automatica o aggiornamento automatico.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="c8a7e-181">Ordine tooget hello prestazioni migliori dalle query, è importante innanzitutto caricano toocreate statistiche per tutte le colonne di tutte le tabelle dopo hello o si verificano modifiche sostanziali in dati hello.</span><span class="sxs-lookup"><span data-stu-id="c8a7e-181">In order tooget hello best performance from your queries, it's important toocreate statistics on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="c8a7e-182">Per informazioni dettagliate, vedere [Managing statistics on tables in SQL Data Warehouse][Statistics](Gestione delle statistiche nelle tabelle in SQL Data Warehouse).</span><span class="sxs-lookup"><span data-stu-id="c8a7e-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8a7e-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c8a7e-183">Next steps</span></span>
<span data-ttu-id="c8a7e-184">Per ulteriori suggerimenti per lo sviluppo, vedere hello [Cenni preliminari sullo sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="c8a7e-184">For more development tips, see hello [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
