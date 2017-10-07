---
title: aaaMigrate il tooSQL di dati Data Warehouse | Documenti Microsoft
description: Suggerimenti per la migrazione del tooAzure di dati SQL Data Warehouse per lo sviluppo di soluzioni.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="635fe-103">Eseguire la migrazione dei dati</span><span class="sxs-lookup"><span data-stu-id="635fe-103">Migrate Your Data</span></span>
<span data-ttu-id="635fe-104">È possibile spostare dati da differenti origini a SQL Data Warehouse con diversi strumenti,</span><span class="sxs-lookup"><span data-stu-id="635fe-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="635fe-105">Copia file ADF SSIS e bcp può tutti tooachieve usato questo obiettivo.</span><span class="sxs-lookup"><span data-stu-id="635fe-105">ADF Copy, SSIS, and bcp can all be used tooachieve this goal.</span></span> <span data-ttu-id="635fe-106">Tuttavia, man mano che aumenta la quantità hello di dati è necessario considerare suddivisione migrazione dei dati hello in passaggi.</span><span class="sxs-lookup"><span data-stu-id="635fe-106">However, as hello amount of data increases you should think about breaking down hello data migration process into steps.</span></span> <span data-ttu-id="635fe-107">Ciò consente hello opportunità toooptimize ogni passaggio sia per le prestazioni e per la resilienza tooensure una migrazione dei dati uniforme.</span><span class="sxs-lookup"><span data-stu-id="635fe-107">This affords you hello opportunity toooptimize each step both for performance and for resilience tooensure a smooth data migration.</span></span>

<span data-ttu-id="635fe-108">In questo articolo viene innanzitutto gli scenari di migrazione semplice hello di copia file ADF SSIS e bcp.</span><span class="sxs-lookup"><span data-stu-id="635fe-108">This article first discusses hello simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="635fe-109">Quindi approfondire in modalità migrazione hello può essere ottimizzata.</span><span class="sxs-lookup"><span data-stu-id="635fe-109">It then look a little deeper into how hello migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="635fe-110">ADF Copy</span><span class="sxs-lookup"><span data-stu-id="635fe-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="635fe-111">[ADF Copy][ADF Copy] fa parte di [Azure Data Factory][Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="635fe-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="635fe-112">È possibile utilizzare Copia ADF tooexport tooflat dei file di dati che risiedono nell'archiviazione locale, file flat tooremote contenute nell'archiviazione blob di Azure o direttamente in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="635fe-112">You can use ADF Copy tooexport your data tooflat files residing on local storage, tooremote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="635fe-113">Se i dati viene avviato in file flat, quindi è necessario innanzitutto tootransfer il blob di archiviazione tooAzure prima dell'avvio di un carico in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="635fe-113">If your data starts in flat files, then you will first need tootransfer it tooAzure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="635fe-114">Una volta hello dati vengono trasferiti nell'archiviazione blob di Azure è possibile scegliere toouse [copia ADF] [ ADF Copy] nuovamente i dati hello toopush in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="635fe-114">Once hello data is transferred into Azure blob storage you can choose toouse [ADF Copy][ADF Copy] again toopush hello data into SQL Data Warehouse.</span></span>

<span data-ttu-id="635fe-115">PolyBase offre inoltre un'opzione di ad alte prestazioni per il caricamento dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="635fe-115">PolyBase also provides a high-performance option for loading hello data.</span></span> <span data-ttu-id="635fe-116">Questo non significa però che debbano essere usati due strumenti anziché uno.</span><span class="sxs-lookup"><span data-stu-id="635fe-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="635fe-117">Se è necessario ottenere prestazioni ottimali hello, usare PolyBase.</span><span class="sxs-lookup"><span data-stu-id="635fe-117">If you need hello best performance then use PolyBase.</span></span> <span data-ttu-id="635fe-118">Se si desidera un'esperienza singolo strumento (e i dati di hello non sono larga) ADF è la risposta.</span><span class="sxs-lookup"><span data-stu-id="635fe-118">If you want a single tool experience (and hello data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="635fe-119">Head su toohello articolo per alcuni elevate seguente [esempi ADF][ADF samples].</span><span class="sxs-lookup"><span data-stu-id="635fe-119">Head over toohello following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="635fe-120">Integration Services</span><span class="sxs-lookup"><span data-stu-id="635fe-120">Integration Services</span></span>
<span data-ttu-id="635fe-121">Integration Services (SSIS) è uno strumento sofisticato e flessibile di Extract Transform and Load (ETL) che supporta flussi di lavoro complessi, la trasformazione dei dati e diverse opzioni di caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="635fe-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="635fe-122">Utilizzare SSIS toosimply trasferimento dati tooAzure o come parte di una migrazione più ampia.</span><span class="sxs-lookup"><span data-stu-id="635fe-122">Use SSIS toosimply transfer data tooAzure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="635fe-123">SSIS è possibile esportare tooUTF-8 senza hello ordine dei byte nel file hello.</span><span class="sxs-lookup"><span data-stu-id="635fe-123">SSIS can export tooUTF-8 without hello byte order mark in hello file.</span></span> <span data-ttu-id="635fe-124">Ciò è necessario utilizzare hello derivato colonna componente tooconvert hello dati di tipo carattere tooconfigure hello flusso toouse hello 65001 UTF-8 codice pagina di dati.</span><span class="sxs-lookup"><span data-stu-id="635fe-124">tooconfigure this you must first use hello derived column component tooconvert hello character data in hello data flow toouse hello 65001 UTF-8 code page.</span></span> <span data-ttu-id="635fe-125">Una volta colonne hello sono state convertite, scrivere hello dati toohello file flat destinazione adapter assicurandosi che 65001 è stata selezionata anche come pagina di codice hello per file hello.</span><span class="sxs-lookup"><span data-stu-id="635fe-125">Once hello columns have been converted, write hello data toohello flat file destination adapter ensuring that 65001 has also been selected as hello code page for hello file.</span></span>
> 
> 

<span data-ttu-id="635fe-126">SSIS si connette tooSQL Data Warehouse come connessione tooa distribuzione di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="635fe-126">SSIS connects tooSQL Data Warehouse just as it would connect tooa SQL Server deployment.</span></span> <span data-ttu-id="635fe-127">Tuttavia, le connessioni saranno necessario toobe utilizzando una gestione connessione ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="635fe-127">However, your connections will need toobe using an ADO.NET connection manager.</span></span> <span data-ttu-id="635fe-128">Inoltre è necessario tooconfigure hello "Utilizzare inserimento bulk quando disponibili" velocità effettiva toomaximize impostazione.</span><span class="sxs-lookup"><span data-stu-id="635fe-128">You should also take care tooconfigure hello "Use bulk insert when available" setting toomaximize throughput.</span></span> <span data-ttu-id="635fe-129">Consultare toohello [adattatore di destinazione ADO.NET] [ ADO.NET destination adapter] toolearn articolo informazioni su questa proprietà</span><span class="sxs-lookup"><span data-stu-id="635fe-129">Please refer toohello [ADO.NET destination adapter][ADO.NET destination adapter] article toolearn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="635fe-130">Connessione tooAzure SQL Data Warehouse mediante OLEDB non è supportata.</span><span class="sxs-lookup"><span data-stu-id="635fe-130">Connecting tooAzure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="635fe-131">Inoltre, vi è sempre hello possibilità che un pacchetto potrebbe non riuscire a causa di problemi di rete o toothrottling.</span><span class="sxs-lookup"><span data-stu-id="635fe-131">In addition, there is always hello possibility that a package might fail due toothrottling or network issues.</span></span> <span data-ttu-id="635fe-132">Progettazione pacchetti in modo possano essere ripresi nel punto di hello di errore, senza il rollforward di lavoro completate prima errore hello.</span><span class="sxs-lookup"><span data-stu-id="635fe-132">Design packages so they can be resumed at hello point of failure, without redoing work that completed before hello failure.</span></span>

<span data-ttu-id="635fe-133">Per ulteriori informazioni consultare hello [documentazione SSIS][SSIS documentation].</span><span class="sxs-lookup"><span data-stu-id="635fe-133">For more information consult hello [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="635fe-134">bcp</span><span class="sxs-lookup"><span data-stu-id="635fe-134">bcp</span></span>
<span data-ttu-id="635fe-135">L'utilità della riga di comando bcp è progettata per l'importazione e l'esportazione di dati di file flat.</span><span class="sxs-lookup"><span data-stu-id="635fe-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="635fe-136">Durante l'esportazione di dati possono essere eseguite trasformazioni.</span><span class="sxs-lookup"><span data-stu-id="635fe-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="635fe-137">trasformazioni semplice tooperform utilizzano tooselect una query e trasformare i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="635fe-137">tooperform simple transformations use a query tooselect and transform hello data.</span></span> <span data-ttu-id="635fe-138">Una volta esportato, file flat hello possono quindi essere caricati direttamente nel database di SQL Data Warehouse di hello destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="635fe-138">Once exported, hello flat files can then be loaded directly into hello target hello SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="635fe-139">È spesso un hello tooencapsulate consigliabile esportano le trasformazioni utilizzate durante i dati in una vista nel sistema di origine hello.</span><span class="sxs-lookup"><span data-stu-id="635fe-139">It is often a good idea tooencapsulate hello transformations used during data export in a view on hello source system.</span></span> <span data-ttu-id="635fe-140">Ciò garantisce che la logica di hello viene mantenuta e processo hello è ripetibile.</span><span class="sxs-lookup"><span data-stu-id="635fe-140">This ensures that hello logic is retained and hello process is repeatable.</span></span>
> 
> 

<span data-ttu-id="635fe-141">I vantaggi derivanti dall'uso dell'utilità bcp sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="635fe-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="635fe-142">Semplicità.</span><span class="sxs-lookup"><span data-stu-id="635fe-142">Simplicity.</span></span> <span data-ttu-id="635fe-143">i comandi bcp sono toobuild semplice ed eseguire</span><span class="sxs-lookup"><span data-stu-id="635fe-143">bcp commands are simple toobuild and execute</span></span>
* <span data-ttu-id="635fe-144">Possibilità di riavviare il processo di caricamento.</span><span class="sxs-lookup"><span data-stu-id="635fe-144">Re-startable load process.</span></span> <span data-ttu-id="635fe-145">Una volta esportato hello carico può essere eseguita qualsiasi numero di volte</span><span class="sxs-lookup"><span data-stu-id="635fe-145">Once exported hello load can be executed any number of times</span></span>

<span data-ttu-id="635fe-146">Le limitazioni dell'utilità bcp sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="635fe-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="635fe-147">Funziona solo con file flat tabulari.</span><span class="sxs-lookup"><span data-stu-id="635fe-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="635fe-148">Non funziona ad esempio con file XML o JSON.</span><span class="sxs-lookup"><span data-stu-id="635fe-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="635fe-149">Funzionalità di trasformazione dei dati sono toohello limitato solo fase di esportazione e semplici</span><span class="sxs-lookup"><span data-stu-id="635fe-149">Data transformation capabilities are limited toohello export stage only and are simple in nature</span></span>
* <span data-ttu-id="635fe-150">bcp non è stato adattato toobe affidabili durante il caricamento dei dati su hello internet.</span><span class="sxs-lookup"><span data-stu-id="635fe-150">bcp has not been adapted toobe robust when loading data over hello internet.</span></span> <span data-ttu-id="635fe-151">Qualsiasi instabilità della rete può causare un errore di caricamento.</span><span class="sxs-lookup"><span data-stu-id="635fe-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="635fe-152">utilità bcp si basa sullo schema di hello presente carico toohello precedente del database di destinazione hello</span><span class="sxs-lookup"><span data-stu-id="635fe-152">bcp relies on hello schema being present in hello target database prior toohello load</span></span>

<span data-ttu-id="635fe-153">Per ulteriori informazioni, vedere [utilizzare dati tooload bcp in SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="635fe-153">For more information, see [Use bcp tooload data into SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="635fe-154">Ottimizzazione della migrazione dei dati</span><span class="sxs-lookup"><span data-stu-id="635fe-154">Optimizing data migration</span></span>
<span data-ttu-id="635fe-155">Un processo di migrazione di dati SQLDW può essere suddiviso in modo efficace in tre passaggi discreti:</span><span class="sxs-lookup"><span data-stu-id="635fe-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="635fe-156">Esportazione dei dati di origine</span><span class="sxs-lookup"><span data-stu-id="635fe-156">Export of source data</span></span>
2. <span data-ttu-id="635fe-157">Trasferimento di dati tooAzure</span><span class="sxs-lookup"><span data-stu-id="635fe-157">Transfer of data tooAzure</span></span>
3. <span data-ttu-id="635fe-158">Caricare nel database di hello destinazione SQLDW</span><span class="sxs-lookup"><span data-stu-id="635fe-158">Load into hello target SQLDW database</span></span>

<span data-ttu-id="635fe-159">Ogni passaggio può essere ottimizzato singolarmente toocreate un processo di migrazione affidabile, nuovamente avviato e resiliente che ottimizza le prestazioni a ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="635fe-159">Each step can be individually optimized toocreate a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="635fe-160">Ottimizzazione del caricamento dei dati</span><span class="sxs-lookup"><span data-stu-id="635fe-160">Optimizing data load</span></span>
<span data-ttu-id="635fe-161">Esaminando questi elementi in ordine inverso per un momento; dati tooload modo più veloci di Hello sono tramite PolyBase.</span><span class="sxs-lookup"><span data-stu-id="635fe-161">Looking at these in reverse order for a moment; hello fastest way tooload data is via PolyBase.</span></span> <span data-ttu-id="635fe-162">Ottimizzazione di un processo di caricamento PolyBase posizionato prerequisiti hello passaggi precedenti, pertanto è migliore toounderstand questo iniziale.</span><span class="sxs-lookup"><span data-stu-id="635fe-162">Optimizing for a PolyBase load process places prerequisites on hello preceding steps so it's best toounderstand this upfront.</span></span> <span data-ttu-id="635fe-163">Sono:</span><span class="sxs-lookup"><span data-stu-id="635fe-163">They are:</span></span>

1. <span data-ttu-id="635fe-164">Codifica dei file di dati</span><span class="sxs-lookup"><span data-stu-id="635fe-164">Encoding of data files</span></span>
2. <span data-ttu-id="635fe-165">Formato dei file di dati</span><span class="sxs-lookup"><span data-stu-id="635fe-165">Format of data files</span></span>
3. <span data-ttu-id="635fe-166">Percorso dei file di dati</span><span class="sxs-lookup"><span data-stu-id="635fe-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="635fe-167">Codifica</span><span class="sxs-lookup"><span data-stu-id="635fe-167">Encoding</span></span>
<span data-ttu-id="635fe-168">PolyBase richiede toobe i file di dati UTF-8 o UTF-16FE.</span><span class="sxs-lookup"><span data-stu-id="635fe-168">PolyBase requires data files toobe UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="635fe-169">Formato dei file di dati</span><span class="sxs-lookup"><span data-stu-id="635fe-169">Format of data files</span></span>
<span data-ttu-id="635fe-170">PolyBase impone un carattere di terminazione di riga fisso \n o una nuova riga.</span><span class="sxs-lookup"><span data-stu-id="635fe-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="635fe-171">I file di dati devono essere conforme toothis standard.</span><span class="sxs-lookup"><span data-stu-id="635fe-171">Your data files must conform toothis standard.</span></span> <span data-ttu-id="635fe-172">Non esistono restrizioni per i caratteri di terminazione di colonna o stringa.</span><span class="sxs-lookup"><span data-stu-id="635fe-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="635fe-173">Sarà necessario toodefine ogni colonna nel file hello come parte della tabella esterna in PolyBase.</span><span class="sxs-lookup"><span data-stu-id="635fe-173">You will have toodefine every column in hello file as part of your external table in PolyBase.</span></span> <span data-ttu-id="635fe-174">Assicurarsi che tutte le colonne esportate sono obbligatori e che i tipi di hello conforme standard toohello richiesto.</span><span class="sxs-lookup"><span data-stu-id="635fe-174">Make sure that all exported columns are required and that hello types conform toohello required standards.</span></span>

<span data-ttu-id="635fe-175">Fare riferimento toohello [eseguire la migrazione dello schema] articolo per informazioni dettagliate sui tipi di dati supportati.</span><span class="sxs-lookup"><span data-stu-id="635fe-175">Please refer back toohello [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="635fe-176">Percorso dei file di dati</span><span class="sxs-lookup"><span data-stu-id="635fe-176">Location of data files</span></span>
<span data-ttu-id="635fe-177">SQL Data Warehouse usa esclusivamente dati di PolyBase tooload dall'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="635fe-177">SQL Data Warehouse uses PolyBase tooload data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="635fe-178">Di conseguenza, i dati di hello devono innanzitutto trasferiti nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="635fe-178">Consequently, hello data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="635fe-179">Ottimizzazione del trasferimento dei dati</span><span class="sxs-lookup"><span data-stu-id="635fe-179">Optimizing data transfer</span></span>
<span data-ttu-id="635fe-180">Una delle parti di più lente hello della migrazione dei dati è il trasferimento di hello di hello tooAzure di dati.</span><span class="sxs-lookup"><span data-stu-id="635fe-180">One of hello slowest parts of data migration is hello transfer of hello data tooAzure.</span></span> <span data-ttu-id="635fe-181">Non solo la larghezza di banda di rete può costituire un problema, ma anche l'affidabilità della rete può gravemente compromettere lo stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="635fe-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="635fe-182">Per impostazione predefinita la migrazione dei dati tooAzure è su internet hello così probabilità di errori di trasferimento che si verificano ragionevolmente probabilmente hello.</span><span class="sxs-lookup"><span data-stu-id="635fe-182">By default migrating data tooAzure is over hello internet so hello chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="635fe-183">Tuttavia, questi errori possono richiedere toobe dati inviati di nuovo in tutto o in parte.</span><span class="sxs-lookup"><span data-stu-id="635fe-183">However, these errors may require data toobe re-sent either in whole or in part.</span></span>

<span data-ttu-id="635fe-184">Per fortuna sono diverse velocità di opzioni tooimprove hello e resilienza di questo processo:</span><span class="sxs-lookup"><span data-stu-id="635fe-184">Fortunately you have several options tooimprove hello speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="635fe-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="635fe-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="635fe-186">È possibile utilizzare tooconsider [ExpressRoute] [ ExpressRoute] toospeed di trasferimento hello.</span><span class="sxs-lookup"><span data-stu-id="635fe-186">You may want tooconsider using [ExpressRoute][ExpressRoute] toospeed up hello transfer.</span></span> <span data-ttu-id="635fe-187">[ExpressRoute] [ ExpressRoute] fornisce con un tooAzure di stabilire una connessione privata in modo da non superare connessione hello hello rete internet pubblica.</span><span class="sxs-lookup"><span data-stu-id="635fe-187">[ExpressRoute][ExpressRoute] provides you with an established private connection tooAzure so hello connection does not go over hello public internet.</span></span> <span data-ttu-id="635fe-188">Non si tratta di un passaggio obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="635fe-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="635fe-189">Tuttavia, determina un miglioramento della velocità effettiva quando si tooAzure dati da un locale o funzionalità di condivisione percorso.</span><span class="sxs-lookup"><span data-stu-id="635fe-189">However, it will improve throughput when pushing data tooAzure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="635fe-190">vantaggi dell'utilizzo di Hello [ExpressRoute] [ ExpressRoute] sono:</span><span class="sxs-lookup"><span data-stu-id="635fe-190">hello benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="635fe-191">Maggiore affidabilità</span><span class="sxs-lookup"><span data-stu-id="635fe-191">Increased reliability</span></span>
2. <span data-ttu-id="635fe-192">Maggiore velocità di rete</span><span class="sxs-lookup"><span data-stu-id="635fe-192">Faster network speed</span></span>
3. <span data-ttu-id="635fe-193">Minore latenza di rete</span><span class="sxs-lookup"><span data-stu-id="635fe-193">Lower network latency</span></span>
4. <span data-ttu-id="635fe-194">Maggiore sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="635fe-194">higher network security</span></span>

<span data-ttu-id="635fe-195">[ExpressRoute] [ ExpressRoute] è utile per il numero di scenari; hello non appena la migrazione.</span><span class="sxs-lookup"><span data-stu-id="635fe-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just hello migration.</span></span>

<span data-ttu-id="635fe-196">Per altre informazioni</span><span class="sxs-lookup"><span data-stu-id="635fe-196">Interested?</span></span> <span data-ttu-id="635fe-197">Per ulteriori informazioni e i prezzi, visitare hello [documentazione di ExpressRoute][ExpressRoute documentation].</span><span class="sxs-lookup"><span data-stu-id="635fe-197">For more information and pricing please visit hello [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="635fe-198">Servizio Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="635fe-198">Azure Import and Export Service</span></span>
<span data-ttu-id="635fe-199">Hello servizio di esportazione e importazione di Azure è un processo di trasferimento di dati progettato per trasferimenti grandi dimensioni (GB + +) toomassive (TB + +) dei dati in Azure.</span><span class="sxs-lookup"><span data-stu-id="635fe-199">hello Azure Import and Export Service is a data transfer process designed for large (GB++) toomassive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="635fe-200">Comporta la scrittura di toodisks i dati e il loro trasferimento tooan data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="635fe-200">It involves writing your data toodisks and shipping them tooan Azure data center.</span></span> <span data-ttu-id="635fe-201">contenuto del disco Hello verrà quindi caricato nel BLOB di archiviazione di Azure per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="635fe-201">hello disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="635fe-202">Una panoramica del processo di esportazione importazione hello è come segue:</span><span class="sxs-lookup"><span data-stu-id="635fe-202">A high-level view of hello import export process is as follows:</span></span>

1. <span data-ttu-id="635fe-203">Configurare una data di archiviazione Blob di Azure contenitore tooreceive hello</span><span class="sxs-lookup"><span data-stu-id="635fe-203">Configure an Azure Blob Storage container tooreceive hello data</span></span>
2. <span data-ttu-id="635fe-204">Esportare l'archiviazione dei dati toolocal</span><span class="sxs-lookup"><span data-stu-id="635fe-204">Export your data toolocal storage</span></span>
3. <span data-ttu-id="635fe-205">Copiare hello dati too3.5 pollice SATA II/III unità disco rigido utilizzando hello [strumento di importazione/esportazione di Azure]</span><span class="sxs-lookup"><span data-stu-id="635fe-205">Copy hello data too3.5 inch SATA II/III hard disk drives using hello [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="635fe-206">Creare un processo di importazione utilizzando hello importazione di Azure e il servizio di esportazione che fornisce file journal hello prodotti da hello [strumento di importazione/esportazione di Azure]</span><span class="sxs-lookup"><span data-stu-id="635fe-206">Create an Import Job using hello Azure Import and Export Service providing hello journal files produced by hello [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="635fe-207">Spedire i dischi di hello del nominato data center di Azure</span><span class="sxs-lookup"><span data-stu-id="635fe-207">Ship hello disks your nominated Azure data center</span></span>
6. <span data-ttu-id="635fe-208">I dati vengono trasferiti tooyour contenitore di archiviazione Blob di Azure</span><span class="sxs-lookup"><span data-stu-id="635fe-208">Your data is transferred tooyour Azure Blob Storage container</span></span>
7. <span data-ttu-id="635fe-209">Caricare i dati di hello in SQLDW con PolyBase</span><span class="sxs-lookup"><span data-stu-id="635fe-209">Load hello data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="635fe-210">Utilità [AZCopy][AZCopy]</span><span class="sxs-lookup"><span data-stu-id="635fe-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="635fe-211">Hello [AZCopy][AZCopy] utilità è un ottimo strumento per ottenere i dati trasferiti nel BLOB di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="635fe-211">hello [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="635fe-212">È progettato per piccole (MB + +) toovery grandi dimensioni (GB + +) trasferimenti di dati.</span><span class="sxs-lookup"><span data-stu-id="635fe-212">It is designed for small (MB++) toovery large (GB++) data transfers.</span></span> <span data-ttu-id="635fe-213">[AZCopy] è stato progettato tooprovide resilienti una velocità effettiva ottimale quando il trasferimento di dati tooAzure e pertanto è la scelta ideale per la fase di trasferimento dei dati hello.</span><span class="sxs-lookup"><span data-stu-id="635fe-213">[AZCopy] has also been designed tooprovide good resilient throughput when transferring data tooAzure and so is a great choice for hello data transfer step.</span></span> <span data-ttu-id="635fe-214">Una volta trasferiti, è possibile caricare i dati di hello usando PolyBase in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="635fe-214">Once transferred you can load hello data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="635fe-215">È anche possibile incorporare AZCopy nei pacchetti SSIS usando un'attività "Execute Process".</span><span class="sxs-lookup"><span data-stu-id="635fe-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="635fe-216">toouse AZCopy sarà anche necessario toodownload e installarlo prima.</span><span class="sxs-lookup"><span data-stu-id="635fe-216">toouse AZCopy you will first need toodownload and install it.</span></span> <span data-ttu-id="635fe-217">Sono disponibili una [versione di produzione][production version] e una [versione di anteprima][preview version].</span><span class="sxs-lookup"><span data-stu-id="635fe-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="635fe-218">tooupload un file dal file system che è necessario un comando simile hello uno di seguito:</span><span class="sxs-lookup"><span data-stu-id="635fe-218">tooupload a file from your file system you will need a command like hello one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="635fe-219">Segue un riepilogo generale del processo:</span><span class="sxs-lookup"><span data-stu-id="635fe-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="635fe-220">Configurare un dati di hello tooreceive del contenitore di blob di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="635fe-220">Configure an Azure storage blob container tooreceive hello data</span></span>
2. <span data-ttu-id="635fe-221">Esportare l'archiviazione dei dati toolocal</span><span class="sxs-lookup"><span data-stu-id="635fe-221">Export your data toolocal storage</span></span>
3. <span data-ttu-id="635fe-222">I dati nel contenitore di archiviazione Blob di Azure hello AZCopy</span><span class="sxs-lookup"><span data-stu-id="635fe-222">AZCopy your data in hello Azure Blob Storage container</span></span>
4. <span data-ttu-id="635fe-223">Caricare i dati di hello in SQL Data Warehouse tramite PolyBase</span><span class="sxs-lookup"><span data-stu-id="635fe-223">Load hello data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="635fe-224">Documentazione completa disponibile: [AZCopy][AZCopy].</span><span class="sxs-lookup"><span data-stu-id="635fe-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="635fe-225">Ottimizzazione dell'esportazione dei dati</span><span class="sxs-lookup"><span data-stu-id="635fe-225">Optimizing data export</span></span>
<span data-ttu-id="635fe-226">Inoltre tooensuring che esportazione hello conforme requisiti toohello disposti da PolyBase è anche possibile cercare esportazione hello toooptimize hello processo di data tooimprove hello ulteriormente.</span><span class="sxs-lookup"><span data-stu-id="635fe-226">In addition tooensuring that hello export conforms toohello requirements laid out by PolyBase you can also seek toooptimize hello export of hello data tooimprove hello process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="635fe-227">Compressione dei dati</span><span class="sxs-lookup"><span data-stu-id="635fe-227">Data compression</span></span>
<span data-ttu-id="635fe-228">PolyBase è in grado di leggere i dati compressi in file gzip.</span><span class="sxs-lookup"><span data-stu-id="635fe-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="635fe-229">Se si è in grado di toocompress toogzip dei file di dati, quindi si verrà ridurre hello dati caduti rete hello.</span><span class="sxs-lookup"><span data-stu-id="635fe-229">If you are able toocompress your data toogzip files then you will minimize hello amount of data being pushed over hello network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="635fe-230">File multipli</span><span class="sxs-lookup"><span data-stu-id="635fe-230">Multiple files</span></span>
<span data-ttu-id="635fe-231">Suddividere le tabelle di grandi dimensioni in più file non solo consente di tooimprove esportare velocità, consente inoltre con trasferimento re-startability e la gestibilità complessiva dei dati di hello una volta nell'archiviazione blob di Azure di hello hello.</span><span class="sxs-lookup"><span data-stu-id="635fe-231">Breaking up large tables into several files not only helps tooimprove export speed, it also helps with transfer re-startability, and hello overall manageability of hello data once in hello Azure blob storage.</span></span> <span data-ttu-id="635fe-232">Una delle numerose funzionalità interessante di PolyBase è che verrà letto tutti hello hello file all'interno di una cartella e considerarla come una tabella.</span><span class="sxs-lookup"><span data-stu-id="635fe-232">One of hello many nice features of PolyBase is that it will read all hello files inside a folder and treat it as one table.</span></span> <span data-ttu-id="635fe-233">È pertanto un file di hello buona tooisolate per ogni tabella nella relativa cartella.</span><span class="sxs-lookup"><span data-stu-id="635fe-233">It is therefore a good idea tooisolate hello files for each table into its own folder.</span></span>

<span data-ttu-id="635fe-234">PolyBase supporta anche una funzionalità nota come "attraversamento di cartelle ricorsivo".</span><span class="sxs-lookup"><span data-stu-id="635fe-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="635fe-235">È possibile utilizzare questa funzionalità toofurther migliorare organizzazione hello di tooimprove i dati esportati la gestione dei dati.</span><span class="sxs-lookup"><span data-stu-id="635fe-235">You can use this feature toofurther enhance hello organization of your exported data tooimprove your data management.</span></span>

<span data-ttu-id="635fe-236">toolearn più sul caricamento dei dati con PolyBase, vedere [dati tooload usare PolyBase in SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="635fe-236">toolearn more about loading data with PolyBase, see [Use PolyBase tooload data into SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="635fe-237">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="635fe-237">Next steps</span></span>
<span data-ttu-id="635fe-238">Per ulteriori informazioni sulla migrazione, vedere [eseguire la migrazione del Data Warehouse di tooSQL soluzione][Migrate your solution tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="635fe-238">For more about migration, see [Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse].</span></span>
<span data-ttu-id="635fe-239">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="635fe-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
