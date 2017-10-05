---
title: Eseguire la migrazione dei dati in SQL Data Warehouse | Microsoft Docs
description: Suggerimenti per la migrazione dei dati in Azure SQL Data Warehouse per lo sviluppo di soluzioni.
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
ms.openlocfilehash: dbdf1696cd169aa7e5e23f116027a1170347f4ea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="624a9-103">Eseguire la migrazione dei dati</span><span class="sxs-lookup"><span data-stu-id="624a9-103">Migrate Your Data</span></span>
<span data-ttu-id="624a9-104">È possibile spostare dati da differenti origini a SQL Data Warehouse con diversi strumenti,</span><span class="sxs-lookup"><span data-stu-id="624a9-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="624a9-105">ad esempio usando ADF Copy, SSIS e bcp.</span><span class="sxs-lookup"><span data-stu-id="624a9-105">ADF Copy, SSIS, and bcp can all be used to achieve this goal.</span></span> <span data-ttu-id="624a9-106">Tuttavia, con l'aumento della quantità di dati, prendere in considerazione la possibilità di suddividere il processo di migrazione in passaggi.</span><span class="sxs-lookup"><span data-stu-id="624a9-106">However, as the amount of data increases you should think about breaking down the data migration process into steps.</span></span> <span data-ttu-id="624a9-107">Ciò consente di ottimizzare ogni passaggio sia per le prestazioni che per la resilienza in modo da garantire una migrazione uniforme dei dati.</span><span class="sxs-lookup"><span data-stu-id="624a9-107">This affords you the opportunity to optimize each step both for performance and for resilience to ensure a smooth data migration.</span></span>

<span data-ttu-id="624a9-108">Questo articolo descrive in primo luogo i semplici scenari di migrazione di ADF Copy, SSIS e bcp,</span><span class="sxs-lookup"><span data-stu-id="624a9-108">This article first discusses the simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="624a9-109">per poi analizzare come ottimizzare la migrazione.</span><span class="sxs-lookup"><span data-stu-id="624a9-109">It then look a little deeper into how the migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="624a9-110">ADF Copy</span><span class="sxs-lookup"><span data-stu-id="624a9-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="624a9-111">[ADF Copy][ADF Copy] fa parte di [Azure Data Factory][Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="624a9-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="624a9-112">È possibile usare ADF Copy per esportare i dati in file flat che si trovano in un'archiviazione locale, in file flat remoti contenuti nell'archiviazione BLOB di Azure o direttamente in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="624a9-112">You can use ADF Copy to export your data to flat files residing on local storage, to remote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="624a9-113">Se i dati sono contenuti in file flat, è necessario trasferirli nel BLOB di archiviazione di Azure prima di avviare un caricamento in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="624a9-113">If your data starts in flat files, then you will first need to transfer it to Azure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="624a9-114">Dopo il trasferimento dei dati nell'archiviazione BLOB di Azure, è possibile scegliere di usare nuovamente [ADF Copy][ADF Copy] per effettuare il push dei dati in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="624a9-114">Once the data is transferred into Azure blob storage you can choose to use [ADF Copy][ADF Copy] again to push the data into SQL Data Warehouse.</span></span>

<span data-ttu-id="624a9-115">Anche PolyBase rappresenta un'opzione a prestazioni elevate per il caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="624a9-115">PolyBase also provides a high-performance option for loading the data.</span></span> <span data-ttu-id="624a9-116">Questo non significa però che debbano essere usati due strumenti anziché uno.</span><span class="sxs-lookup"><span data-stu-id="624a9-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="624a9-117">Se si vuole ottenere prestazioni ottimali, usare PolyBase.</span><span class="sxs-lookup"><span data-stu-id="624a9-117">If you need the best performance then use PolyBase.</span></span> <span data-ttu-id="624a9-118">Se invece si vuole usare un unico strumento (e il volume di dati non è elevato), ADF è la soluzione ideale.</span><span class="sxs-lookup"><span data-stu-id="624a9-118">If you want a single tool experience (and the data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="624a9-119">Leggere l'articolo seguente per alcuni [esempi di ADF][ADF samples].</span><span class="sxs-lookup"><span data-stu-id="624a9-119">Head over to the following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="624a9-120">Integration Services</span><span class="sxs-lookup"><span data-stu-id="624a9-120">Integration Services</span></span>
<span data-ttu-id="624a9-121">Integration Services (SSIS) è uno strumento sofisticato e flessibile di Extract Transform and Load (ETL) che supporta flussi di lavoro complessi, la trasformazione dei dati e diverse opzioni di caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="624a9-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="624a9-122">Usare SSIS per trasferire semplicemente dati in Azure o come parte di una migrazione più ampia.</span><span class="sxs-lookup"><span data-stu-id="624a9-122">Use SSIS to simply transfer data to Azure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="624a9-123">SSIS può esportare in UTF-8 senza byte order mark nel file.</span><span class="sxs-lookup"><span data-stu-id="624a9-123">SSIS can export to UTF-8 without the byte order mark in the file.</span></span> <span data-ttu-id="624a9-124">Per configurare questa funzionalità, è necessario prima usare il componente colonna derivata per convertire i dati di tipo carattere nel flusso di dati per usare la tabella codici 65001 UTF-8.</span><span class="sxs-lookup"><span data-stu-id="624a9-124">To configure this you must first use the derived column component to convert the character data in the data flow to use the 65001 UTF-8 code page.</span></span> <span data-ttu-id="624a9-125">Dopo la conversione delle colonne, scrivere i dati nell'adattatore di destinazione di file flat verificando che sia stata selezionata la tabella codici 65001 per il file.</span><span class="sxs-lookup"><span data-stu-id="624a9-125">Once the columns have been converted, write the data to the flat file destination adapter ensuring that 65001 has also been selected as the code page for the file.</span></span>
> 
> 

<span data-ttu-id="624a9-126">SSIS si connette a SQL Data Warehouse nello stesso modo in cui si connetterebbe a una distribuzione di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="624a9-126">SSIS connects to SQL Data Warehouse just as it would connect to a SQL Server deployment.</span></span> <span data-ttu-id="624a9-127">La connessione tuttavia dovrà usare una gestione connessioni ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="624a9-127">However, your connections will need to be using an ADO.NET connection manager.</span></span> <span data-ttu-id="624a9-128">È anche necessario configurare l'impostazione per "utilizzare l'inserimento di massa quando disponibile" per ottimizzare la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="624a9-128">You should also take care to configure the "Use bulk insert when available" setting to maximize throughput.</span></span> <span data-ttu-id="624a9-129">Fare riferimento all'articolo relativo all'[adattatore di destinazione ADO.NET][ADO.NET destination adapter] per altre informazioni su questa proprietà</span><span class="sxs-lookup"><span data-stu-id="624a9-129">Please refer to the [ADO.NET destination adapter][ADO.NET destination adapter] article to learn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="624a9-130">La connessione ad Azure SQL Data Warehouse mediante OLEDB non è supportata.</span><span class="sxs-lookup"><span data-stu-id="624a9-130">Connecting to Azure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="624a9-131">Esiste inoltre sempre la possibilità che si verifichi l'errore di un pacchetto per problemi di rete o limitazione delle richieste.</span><span class="sxs-lookup"><span data-stu-id="624a9-131">In addition, there is always the possibility that a package might fail due to throttling or network issues.</span></span> <span data-ttu-id="624a9-132">Progettare i pacchetti in modo che sia possibile ripartire dal punto in cui si è verificato l'errore, senza dover ripetere il lavoro completato prima dell'errore.</span><span class="sxs-lookup"><span data-stu-id="624a9-132">Design packages so they can be resumed at the point of failure, without redoing work that completed before the failure.</span></span>

<span data-ttu-id="624a9-133">Per altre informazioni, vedere la [documentazione relativa a SSIS][SSIS documentation].</span><span class="sxs-lookup"><span data-stu-id="624a9-133">For more information consult the [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="624a9-134">bcp</span><span class="sxs-lookup"><span data-stu-id="624a9-134">bcp</span></span>
<span data-ttu-id="624a9-135">L'utilità della riga di comando bcp è progettata per l'importazione e l'esportazione di dati di file flat.</span><span class="sxs-lookup"><span data-stu-id="624a9-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="624a9-136">Durante l'esportazione di dati possono essere eseguite trasformazioni.</span><span class="sxs-lookup"><span data-stu-id="624a9-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="624a9-137">Per eseguire trasformazioni semplici, usare una query per selezionare e trasformare i dati.</span><span class="sxs-lookup"><span data-stu-id="624a9-137">To perform simple transformations use a query to select and transform the data.</span></span> <span data-ttu-id="624a9-138">Dopo l'esportazione, i file flat possono quindi essere caricati direttamente nel database di SQL Data Warehouse di destinazione.</span><span class="sxs-lookup"><span data-stu-id="624a9-138">Once exported, the flat files can then be loaded directly into the target the SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="624a9-139">Spesso è una buona idea incapsulare le trasformazioni usate durante l'esportazione di dati in una vista nel sistema di origine.</span><span class="sxs-lookup"><span data-stu-id="624a9-139">It is often a good idea to encapsulate the transformations used during data export in a view on the source system.</span></span> <span data-ttu-id="624a9-140">In questo modo viene mantenuta la logica e il processo è ripetibile.</span><span class="sxs-lookup"><span data-stu-id="624a9-140">This ensures that the logic is retained and the process is repeatable.</span></span>
> 
> 

<span data-ttu-id="624a9-141">I vantaggi derivanti dall'uso dell'utilità bcp sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="624a9-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="624a9-142">Semplicità.</span><span class="sxs-lookup"><span data-stu-id="624a9-142">Simplicity.</span></span> <span data-ttu-id="624a9-143">I comandi di bcp sono semplici da creare ed eseguire.</span><span class="sxs-lookup"><span data-stu-id="624a9-143">bcp commands are simple to build and execute</span></span>
* <span data-ttu-id="624a9-144">Possibilità di riavviare il processo di caricamento.</span><span class="sxs-lookup"><span data-stu-id="624a9-144">Re-startable load process.</span></span> <span data-ttu-id="624a9-145">Dopo l'esportazione, il caricamento può essere eseguito un numero illimitato di volte.</span><span class="sxs-lookup"><span data-stu-id="624a9-145">Once exported the load can be executed any number of times</span></span>

<span data-ttu-id="624a9-146">Le limitazioni dell'utilità bcp sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="624a9-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="624a9-147">Funziona solo con file flat tabulari.</span><span class="sxs-lookup"><span data-stu-id="624a9-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="624a9-148">Non funziona ad esempio con file XML o JSON.</span><span class="sxs-lookup"><span data-stu-id="624a9-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="624a9-149">Le funzionalità di trasformazione dei dati sono limitate alla sola fase di esportazione e sono semplici per natura.</span><span class="sxs-lookup"><span data-stu-id="624a9-149">Data transformation capabilities are limited to the export stage only and are simple in nature</span></span>
* <span data-ttu-id="624a9-150">L'utilità bcp non è stata adattata per essere efficace durante il caricamento di dati su Internet.</span><span class="sxs-lookup"><span data-stu-id="624a9-150">bcp has not been adapted to be robust when loading data over the internet.</span></span> <span data-ttu-id="624a9-151">Qualsiasi instabilità della rete può causare un errore di caricamento.</span><span class="sxs-lookup"><span data-stu-id="624a9-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="624a9-152">L'utilità bcp si basa sullo schema presente nel database di destinazione prima del caricamento.</span><span class="sxs-lookup"><span data-stu-id="624a9-152">bcp relies on the schema being present in the target database prior to the load</span></span>

<span data-ttu-id="624a9-153">Per altre informazioni, vedere l'articolo relativo all'[uso di bcp per caricare dati in SQL Data Warehouse][Use bcp to load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="624a9-153">For more information, see [Use bcp to load data into SQL Data Warehouse][Use bcp to load data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="624a9-154">Ottimizzazione della migrazione dei dati</span><span class="sxs-lookup"><span data-stu-id="624a9-154">Optimizing data migration</span></span>
<span data-ttu-id="624a9-155">Un processo di migrazione di dati SQLDW può essere suddiviso in modo efficace in tre passaggi discreti:</span><span class="sxs-lookup"><span data-stu-id="624a9-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="624a9-156">Esportazione dei dati di origine</span><span class="sxs-lookup"><span data-stu-id="624a9-156">Export of source data</span></span>
2. <span data-ttu-id="624a9-157">Trasferimento dei dati in Azure</span><span class="sxs-lookup"><span data-stu-id="624a9-157">Transfer of data to Azure</span></span>
3. <span data-ttu-id="624a9-158">Caricamento nel database SQLDW di destinazione</span><span class="sxs-lookup"><span data-stu-id="624a9-158">Load into the target SQLDW database</span></span>

<span data-ttu-id="624a9-159">È possibile ottimizzare singolarmente ogni passaggio per creare un processo di migrazione solido, nuovamente avviabile e resiliente che ottimizza le prestazioni a ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="624a9-159">Each step can be individually optimized to create a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="624a9-160">Ottimizzazione del caricamento dei dati</span><span class="sxs-lookup"><span data-stu-id="624a9-160">Optimizing data load</span></span>
<span data-ttu-id="624a9-161">Esaminando per un momento queste operazioni in ordine inverso, il modo più rapido per caricare i dati è tramite PolyBase.</span><span class="sxs-lookup"><span data-stu-id="624a9-161">Looking at these in reverse order for a moment; the fastest way to load data is via PolyBase.</span></span> <span data-ttu-id="624a9-162">L'ottimizzazione per un processo di caricamento PolyBase prevede prerequisiti per i passaggi precedenti, pertanto è consigliabile capire questo aspetto dall'inizio.</span><span class="sxs-lookup"><span data-stu-id="624a9-162">Optimizing for a PolyBase load process places prerequisites on the preceding steps so it's best to understand this upfront.</span></span> <span data-ttu-id="624a9-163">Vale a dire:</span><span class="sxs-lookup"><span data-stu-id="624a9-163">They are:</span></span>

1. <span data-ttu-id="624a9-164">Codifica dei file di dati</span><span class="sxs-lookup"><span data-stu-id="624a9-164">Encoding of data files</span></span>
2. <span data-ttu-id="624a9-165">Formato dei file di dati</span><span class="sxs-lookup"><span data-stu-id="624a9-165">Format of data files</span></span>
3. <span data-ttu-id="624a9-166">Percorso dei file di dati</span><span class="sxs-lookup"><span data-stu-id="624a9-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="624a9-167">Codifica</span><span class="sxs-lookup"><span data-stu-id="624a9-167">Encoding</span></span>
<span data-ttu-id="624a9-168">PolyBase richiede file di dati con codifica UTF-8 o UTF-16FE.</span><span class="sxs-lookup"><span data-stu-id="624a9-168">PolyBase requires data files to be UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="624a9-169">Formato dei file di dati</span><span class="sxs-lookup"><span data-stu-id="624a9-169">Format of data files</span></span>
<span data-ttu-id="624a9-170">PolyBase impone un carattere di terminazione di riga fisso \n o una nuova riga.</span><span class="sxs-lookup"><span data-stu-id="624a9-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="624a9-171">I file di dati devono essere conformi a questo standard.</span><span class="sxs-lookup"><span data-stu-id="624a9-171">Your data files must conform to this standard.</span></span> <span data-ttu-id="624a9-172">Non esistono restrizioni per i caratteri di terminazione di colonna o stringa.</span><span class="sxs-lookup"><span data-stu-id="624a9-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="624a9-173">Sarà necessario definire ogni colonna nel file come parte della tabella esterna in PolyBase.</span><span class="sxs-lookup"><span data-stu-id="624a9-173">You will have to define every column in the file as part of your external table in PolyBase.</span></span> <span data-ttu-id="624a9-174">Assicurarsi che tutte le colonne esportate siano necessarie e che i tipi siano conformi agli standard richiesti.</span><span class="sxs-lookup"><span data-stu-id="624a9-174">Make sure that all exported columns are required and that the types conform to the required standards.</span></span>

<span data-ttu-id="624a9-175">Vedere l'articolo sulla [migrazione di uno schema] per informazioni su tipi di dati supportati.</span><span class="sxs-lookup"><span data-stu-id="624a9-175">Please refer back to the [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="624a9-176">Percorso dei file di dati</span><span class="sxs-lookup"><span data-stu-id="624a9-176">Location of data files</span></span>
<span data-ttu-id="624a9-177">SQL Data Warehouse usa PolyBase per caricare i dati esclusivamente dall'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="624a9-177">SQL Data Warehouse uses PolyBase to load data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="624a9-178">I dati pertanto devono essere stati prima trasferiti nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="624a9-178">Consequently, the data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="624a9-179">Ottimizzazione del trasferimento dei dati</span><span class="sxs-lookup"><span data-stu-id="624a9-179">Optimizing data transfer</span></span>
<span data-ttu-id="624a9-180">Una delle fasi più lente della migrazione dei dati è costituita dal trasferimento dei dati in Azure.</span><span class="sxs-lookup"><span data-stu-id="624a9-180">One of the slowest parts of data migration is the transfer of the data to Azure.</span></span> <span data-ttu-id="624a9-181">Non solo la larghezza di banda di rete può costituire un problema, ma anche l'affidabilità della rete può gravemente compromettere lo stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="624a9-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="624a9-182">Per impostazione predefinita, la migrazione dei dati in Azure viene eseguita tramite Internet ed è pertanto probabile che si verifichino errori di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="624a9-182">By default migrating data to Azure is over the internet so the chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="624a9-183">Questi errori tuttavia possono richiedere che i dati vengano inviati di nuovo completamente o in parte.</span><span class="sxs-lookup"><span data-stu-id="624a9-183">However, these errors may require data to be re-sent either in whole or in part.</span></span>

<span data-ttu-id="624a9-184">Fortunatamente sono disponibili diverse opzioni per migliorare la velocità e la resilienza di questo processo:</span><span class="sxs-lookup"><span data-stu-id="624a9-184">Fortunately you have several options to improve the speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="624a9-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="624a9-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="624a9-186">È possibile provare a usare [ExpressRoute][ExpressRoute] per velocizzare il trasferimento.</span><span class="sxs-lookup"><span data-stu-id="624a9-186">You may want to consider using [ExpressRoute][ExpressRoute] to speed up the transfer.</span></span> <span data-ttu-id="624a9-187">[ExpressRoute][ExpressRoute] consente di stabilire una connessione privata ad Azure in modo che la connessione non passi attraverso la rete Internet pubblica.</span><span class="sxs-lookup"><span data-stu-id="624a9-187">[ExpressRoute][ExpressRoute] provides you with an established private connection to Azure so the connection does not go over the public internet.</span></span> <span data-ttu-id="624a9-188">Non si tratta di un passaggio obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="624a9-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="624a9-189">Determina tuttavia un miglioramento della velocità effettiva quando si effettua il push dei dati in Azure da una struttura locale o da una condivisione di percorso.</span><span class="sxs-lookup"><span data-stu-id="624a9-189">However, it will improve throughput when pushing data to Azure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="624a9-190">I vantaggi derivanti dall'uso di [ExpressRoute][ExpressRoute] sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="624a9-190">The benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="624a9-191">Maggiore affidabilità</span><span class="sxs-lookup"><span data-stu-id="624a9-191">Increased reliability</span></span>
2. <span data-ttu-id="624a9-192">Maggiore velocità di rete</span><span class="sxs-lookup"><span data-stu-id="624a9-192">Faster network speed</span></span>
3. <span data-ttu-id="624a9-193">Minore latenza di rete</span><span class="sxs-lookup"><span data-stu-id="624a9-193">Lower network latency</span></span>
4. <span data-ttu-id="624a9-194">Maggiore sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="624a9-194">higher network security</span></span>

<span data-ttu-id="624a9-195">[ExpressRoute][ExpressRoute] è utile per numerosi scenari e non solo per la migrazione.</span><span class="sxs-lookup"><span data-stu-id="624a9-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just the migration.</span></span>

<span data-ttu-id="624a9-196">Per altre informazioni</span><span class="sxs-lookup"><span data-stu-id="624a9-196">Interested?</span></span> <span data-ttu-id="624a9-197">e i dati relativi ai prezzi, vedere la [documentazione relativa a ExpressRoute][ExpressRoute documentation].</span><span class="sxs-lookup"><span data-stu-id="624a9-197">For more information and pricing please visit the [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="624a9-198">Servizio Importazione/Esportazione di Azure</span><span class="sxs-lookup"><span data-stu-id="624a9-198">Azure Import and Export Service</span></span>
<span data-ttu-id="624a9-199">Il servizio Importazione/Esportazione di Azure è un processo di trasferimento dati progettato per trasferimenti di un numero elevato (GB++) o ingente (TB++) di dati in Azure.</span><span class="sxs-lookup"><span data-stu-id="624a9-199">The Azure Import and Export Service is a data transfer process designed for large (GB++) to massive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="624a9-200">Comporta la scrittura dei dati su dischi e l'invio in un data center di Azure.</span><span class="sxs-lookup"><span data-stu-id="624a9-200">It involves writing your data to disks and shipping them to an Azure data center.</span></span> <span data-ttu-id="624a9-201">Il contenuto dei dischi verrà quindi caricato nei BLOB di archiviazione di Azure per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="624a9-201">The disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="624a9-202">Segue una panoramica del processo di importazione/esportazione:</span><span class="sxs-lookup"><span data-stu-id="624a9-202">A high-level view of the import export process is as follows:</span></span>

1. <span data-ttu-id="624a9-203">Configurare un contenitore dell'archiviazione BLOB di Azure per ricevere i dati.</span><span class="sxs-lookup"><span data-stu-id="624a9-203">Configure an Azure Blob Storage container to receive the data</span></span>
2. <span data-ttu-id="624a9-204">Esportare i dati nell'archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="624a9-204">Export your data to local storage</span></span>
3. <span data-ttu-id="624a9-205">Copiare i dati su unità disco rigido SATA II/III da 3,5 pollici usando lo [strumento Importazione/Esportazione di Azure].</span><span class="sxs-lookup"><span data-stu-id="624a9-205">Copy the data to 3.5 inch SATA II/III hard disk drives using the [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="624a9-206">Creare un processo di importazione usando il servizio Importazione/Esportazione di Azure fornendo i file journal generati dallo [strumento Importazione/Esportazione di Azure].</span><span class="sxs-lookup"><span data-stu-id="624a9-206">Create an Import Job using the Azure Import and Export Service providing the journal files produced by the [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="624a9-207">Inviare i dischi al data center di Azure prescelto.</span><span class="sxs-lookup"><span data-stu-id="624a9-207">Ship the disks your nominated Azure data center</span></span>
6. <span data-ttu-id="624a9-208">I dati vengono trasferiti nel contenitore dell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="624a9-208">Your data is transferred to your Azure Blob Storage container</span></span>
7. <span data-ttu-id="624a9-209">Caricare i dati in SQLDW usando PolyBase.</span><span class="sxs-lookup"><span data-stu-id="624a9-209">Load the data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="624a9-210">Utilità [AZCopy][AZCopy]</span><span class="sxs-lookup"><span data-stu-id="624a9-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="624a9-211">L'utilità [AZCopy][AZCopy] è uno strumento ideale per il trasferimento dei dati nei BLOB di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="624a9-211">The [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="624a9-212">È progettato per il trasferimento di dati di piccole (MB++) e grandi dimensioni (GB+ +).</span><span class="sxs-lookup"><span data-stu-id="624a9-212">It is designed for small (MB++) to very large (GB++) data transfers.</span></span> <span data-ttu-id="624a9-213">[AZCopy] è stato progettato anche per garantire una velocità effettiva resiliente durante il trasferimento dei dati in Azure e pertanto rappresenta un'ottima scelta per il passaggio relativo al trasferimento dei dati.</span><span class="sxs-lookup"><span data-stu-id="624a9-213">[AZCopy] has also been designed to provide good resilient throughput when transferring data to Azure and so is a great choice for the data transfer step.</span></span> <span data-ttu-id="624a9-214">Dopo il trasferimento, è possibile caricare i dati con PolyBase in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="624a9-214">Once transferred you can load the data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="624a9-215">È anche possibile incorporare AZCopy nei pacchetti SSIS usando un'attività "Execute Process".</span><span class="sxs-lookup"><span data-stu-id="624a9-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="624a9-216">Per usare AZCopy, sarà necessario prima scaricarlo e installarlo.</span><span class="sxs-lookup"><span data-stu-id="624a9-216">To use AZCopy you will first need to download and install it.</span></span> <span data-ttu-id="624a9-217">Sono disponibili una [versione di produzione][production version] e una [versione di anteprima][preview version].</span><span class="sxs-lookup"><span data-stu-id="624a9-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="624a9-218">Per caricare un file dal file system, è necessario un comando simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="624a9-218">To upload a file from your file system you will need a command like the one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="624a9-219">Segue un riepilogo generale del processo:</span><span class="sxs-lookup"><span data-stu-id="624a9-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="624a9-220">Configurare un contenitore di BLOB di archiviazione di Azure per ricevere i dati.</span><span class="sxs-lookup"><span data-stu-id="624a9-220">Configure an Azure storage blob container to receive the data</span></span>
2. <span data-ttu-id="624a9-221">Esportare i dati nell'archiviazione locale.</span><span class="sxs-lookup"><span data-stu-id="624a9-221">Export your data to local storage</span></span>
3. <span data-ttu-id="624a9-222">Copiare tramite AZCopy i dati nel contenitore dell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="624a9-222">AZCopy your data in the Azure Blob Storage container</span></span>
4. <span data-ttu-id="624a9-223">Caricare i dati in SQL Data Warehouse usando PolyBase.</span><span class="sxs-lookup"><span data-stu-id="624a9-223">Load the data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="624a9-224">Documentazione completa disponibile: [AZCopy][AZCopy].</span><span class="sxs-lookup"><span data-stu-id="624a9-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="624a9-225">Ottimizzazione dell'esportazione dei dati</span><span class="sxs-lookup"><span data-stu-id="624a9-225">Optimizing data export</span></span>
<span data-ttu-id="624a9-226">Oltre a garantire che l'esportazione sia conforme ai requisiti previsti da PolyBase, è anche possibile cercare di ottimizzare l'esportazione dei dati per migliorare ulteriormente il processo.</span><span class="sxs-lookup"><span data-stu-id="624a9-226">In addition to ensuring that the export conforms to the requirements laid out by PolyBase you can also seek to optimize the export of the data to improve the process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="624a9-227">Compressione dei dati</span><span class="sxs-lookup"><span data-stu-id="624a9-227">Data compression</span></span>
<span data-ttu-id="624a9-228">PolyBase è in grado di leggere i dati compressi in file gzip.</span><span class="sxs-lookup"><span data-stu-id="624a9-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="624a9-229">Se è possibile comprimere i dati in file gzip, verrà ridotta la quantità di dati di cui viene effettuato il push in rete.</span><span class="sxs-lookup"><span data-stu-id="624a9-229">If you are able to compress your data to gzip files then you will minimize the amount of data being pushed over the network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="624a9-230">File multipli</span><span class="sxs-lookup"><span data-stu-id="624a9-230">Multiple files</span></span>
<span data-ttu-id="624a9-231">La suddivisione di tabelle di grandi dimensioni in più file non solo consente di migliorare la velocità di esportazione, ma favorisce anche la possibilità di riavviare i trasferimenti e semplifica la gestibilità complessiva dei dati dopo che sono stati trasferiti nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="624a9-231">Breaking up large tables into several files not only helps to improve export speed, it also helps with transfer re-startability, and the overall manageability of the data once in the Azure blob storage.</span></span> <span data-ttu-id="624a9-232">Una delle numerose funzionalità interessanti di PolyBase è costituita dalla possibilità di leggere tutti i file all'interno di una cartella considerandola come una tabella.</span><span class="sxs-lookup"><span data-stu-id="624a9-232">One of the many nice features of PolyBase is that it will read all the files inside a folder and treat it as one table.</span></span> <span data-ttu-id="624a9-233">È pertanto opportuno isolare i file per ogni tabella nella relativa cartella.</span><span class="sxs-lookup"><span data-stu-id="624a9-233">It is therefore a good idea to isolate the files for each table into its own folder.</span></span>

<span data-ttu-id="624a9-234">PolyBase supporta anche una funzionalità nota come "attraversamento di cartelle ricorsivo".</span><span class="sxs-lookup"><span data-stu-id="624a9-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="624a9-235">È possibile usare questa funzionalità per migliorare ulteriormente l'organizzazione dei dati esportati e ottimizzare la gestione dei dati.</span><span class="sxs-lookup"><span data-stu-id="624a9-235">You can use this feature to further enhance the organization of your exported data to improve your data management.</span></span>

<span data-ttu-id="624a9-236">Per altre informazioni sul caricamento dei dati con PolyBase, vedere [Caricare dati con PolyBase in SQL Data Warehouse][Use PolyBase to load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="624a9-236">To learn more about loading data with PolyBase, see [Use PolyBase to load data into SQL Data Warehouse][Use PolyBase to load data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="624a9-237">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="624a9-237">Next steps</span></span>
<span data-ttu-id="624a9-238">Per altre informazioni sulla migrazione, vedere [Eseguire la migrazione della soluzione in SQL Data Warehouse][Migrate your solution to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="624a9-238">For more about migration, see [Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse].</span></span>
<span data-ttu-id="624a9-239">Per altri suggerimenti sullo sviluppo, vedere la [panoramica dello sviluppo][development overview].</span><span class="sxs-lookup"><span data-stu-id="624a9-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution to SQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp to load data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase to load data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
