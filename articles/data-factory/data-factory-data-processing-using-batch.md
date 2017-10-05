---
title: Elaborare set di dati su larga scala con Data Factory e Batch | Microsoft Docs
description: "Descrive come elaborare elevate quantità di dati in una pipeline di Data factory di Azure usando la funzionalità di elaborazione parallela di Azure Batch."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 9defbf7a6a515740fa3b3cb1c67a2f5f9d9baa01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="c5d03-103">Elaborazione di fogli dati su larga scala con Data Factory e Batch</span><span class="sxs-lookup"><span data-stu-id="c5d03-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="c5d03-104">Questo articolo descrive l'architettura di una soluzione di esempio che sposta ed elabora set di dati su larga scala in modo automatico e pianificato.</span><span class="sxs-lookup"><span data-stu-id="c5d03-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="c5d03-105">Fornisce inoltre una procedura dettagliata end-to-end per implementare la soluzione mediante Azure Data Factory e Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-105">It also provides an end-to-end walkthrough to implement the solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="c5d03-106">Questo articolo è più lungo dei nostri articoli tipici perché contiene la procedura dettagliata per un'intera soluzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="c5d03-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="c5d03-107">Se non si ha familiarità con Batch e Data Factory, sarà possibile conoscere questi servizi e come interagiscono.</span><span class="sxs-lookup"><span data-stu-id="c5d03-107">If you are new to Batch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="c5d03-108">Se si conoscono i servizi parzialmente e si intende progettare un'architettura o una soluzione, è possibile concentrarsi solo sulla [sezione dell'articolo relativa all'architettura](#architecture-of-sample-solution), se invece si intende sviluppare una soluzione o un prototipo, è possibile provare anche le istruzioni della [procedura dettagliata](#implementation-of-sample-solution).</span><span class="sxs-lookup"><span data-stu-id="c5d03-108">If you know something about the services and are designing/architecting a solution, you may focus just on the [architecture section](#architecture-of-sample-solution) of the article and if you are developing a prototype or a solution, you may also want to try out step-by-step instructions in the [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="c5d03-109">Microsoft invita gli utenti a inviare i loro commenti su questo contenuto e sulle relative modalità di impiego.</span><span class="sxs-lookup"><span data-stu-id="c5d03-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="c5d03-110">In primo luogo si vedrà in che modo i servizi Data Factory e Batch possono essere utili per l'elaborazione di grandi set di dati nel cloud.</span><span class="sxs-lookup"><span data-stu-id="c5d03-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in the cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="c5d03-111">Perché Azure Batch?</span><span class="sxs-lookup"><span data-stu-id="c5d03-111">Why Azure Batch?</span></span>
<span data-ttu-id="c5d03-112">Azure Batch consente di eseguire in modo efficiente applicazioni parallele e HPC (High Performance Computing) su larga scala nel cloud.</span><span class="sxs-lookup"><span data-stu-id="c5d03-112">Azure Batch enables you to run large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="c5d03-113">È un servizio di piattaforma che pianifica l'esecuzione del lavoro a elevato utilizzo di calcolo su una raccolta gestita di macchine virtuali e che può ridimensionare automaticamente le risorse di calcolo in base alle esigenze dei processi.</span><span class="sxs-lookup"><span data-stu-id="c5d03-113">It's a platform service that schedules compute-intensive work to run on a managed collection of virtual machines, and can automatically scale compute resources to meet the needs of your jobs.</span></span>

<span data-ttu-id="c5d03-114">Il servizio Batch consente di definire le risorse di calcolo di Azure per eseguire le applicazioni in parallelo e su larga scala.</span><span class="sxs-lookup"><span data-stu-id="c5d03-114">With the Batch service, you define Azure compute resources to execute your applications in parallel, and at scale.</span></span> <span data-ttu-id="c5d03-115">È possibile eseguire processi su richiesta o pianificati e non è necessario creare, configurare e gestire manualmente un cluster HPC, singole macchine virtuali, reti virtuali o un'infrastruttura complessa di pianificazione di processi e attività.</span><span class="sxs-lookup"><span data-stu-id="c5d03-115">You can run on-demand or scheduled jobs, and you don't need to manually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="c5d03-116">Se non si ha familiarità con Azure Batch, vedere gli articoli seguenti che aiutano a comprendere l'architettura e l'implementazione della soluzione descritta in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c5d03-116">See the following articles if you are not familiar with Azure Batch as it helps with understanding the architecture/implementation of the solution described in this article.</span></span>   

* [<span data-ttu-id="c5d03-117">Nozioni di base su Azure Batch</span><span class="sxs-lookup"><span data-stu-id="c5d03-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="c5d03-118">Panoramica delle funzionalità Batch</span><span class="sxs-lookup"><span data-stu-id="c5d03-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="c5d03-119">(facoltativo) Per altre informazioni su Azure Batch, vedere il [percorso di apprendimento per Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span><span class="sxs-lookup"><span data-stu-id="c5d03-119">(optional) To learn more about Azure Batch, see the [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="c5d03-120">Perché Azure Data Factory?</span><span class="sxs-lookup"><span data-stu-id="c5d03-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="c5d03-121">Data factory è un servizio di integrazione delle informazioni basato sul cloud che permette di automatizzare lo spostamento e la trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="c5d03-121">Data Factory is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="c5d03-122">Con il servizio Data Factory è possibile creare pipeline di dati gestiti per spostare i dati da archivi locali e su cloud a un archivio dati centralizzato (come l'archiviazione BLOB di Azure) ed elaborarli o trasformarli tramite servizi come HDInsight di Azure e Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c5d03-122">Using the Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores to a centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="c5d03-123">È inoltre possibile pianificare le pipeline di dati affinché si eseguano in un modo programmato (ogni ora, una volta al giorno, una volta alla settimana e così via) e monitorarle e gestirle a colpo d'occhio per identificare i problemi ed eseguire azioni.</span><span class="sxs-lookup"><span data-stu-id="c5d03-123">You can also schedule data pipelines to run in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance to identify issues and take action.</span></span>

<span data-ttu-id="c5d03-124">Se non si ha familiarità con Azure Data Factory, vedere gli articoli seguenti che aiutano a comprendere l'architettura e l'implementazione della soluzione descritta in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="c5d03-124">See the following articles if you are not familiar with Azure Data Factory as it helps with understanding the architecture/implementation of the solution described in this article.</span></span>  

* [<span data-ttu-id="c5d03-125">Introduzione ad Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c5d03-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="c5d03-126">Creare la prima pipeline di dati</span><span class="sxs-lookup"><span data-stu-id="c5d03-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="c5d03-127">(facoltativo) Per altre informazioni su Azure Data Factory, vedere il [percorso di apprendimento per Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="c5d03-127">(optional) To learn more about Azure Data Factory, see the [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="c5d03-128">Data Factory e Batch insieme</span><span class="sxs-lookup"><span data-stu-id="c5d03-128">Data Factory and Batch together</span></span>
<span data-ttu-id="c5d03-129">Data Factory include attività predefinite, ad esempio l'attività di copia per copiare o spostare dati da un archivio dati di origine a un archivio dati di destinazione e l'attività hive per elaborare i dati usando i cluster Hadoop (HDInsight) in Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d03-129">Data Factory includes built-in activities such as Copy Activity to copy/move data from a source data store to a destination data store and Hive Activity to process data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="c5d03-130">Per un elenco delle attività di trasformazione supportate, vedere le informazioni sulle [attività di trasformazione dati](data-factory-data-transformation-activities.md) .</span><span class="sxs-lookup"><span data-stu-id="c5d03-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="c5d03-131">Consente inoltre di creare attività .NET personalizzate per spostare o elaborare i dati con la propria logica ed eseguire queste attività in un cluster HDInsight di Azure o in un pool di VM di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-131">It also allows you to create custom .NET activities to move or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="c5d03-132">Quando si usa Azure Batch, è possibile configurare il pool per la scalabilità automatica (aggiungere o rimuovere VM in base al carico di lavoro) secondo la formula che si fornisce.</span><span class="sxs-lookup"><span data-stu-id="c5d03-132">When you use Azure Batch, you can configure the pool to auto-scale (add or remove VMs based on the workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="c5d03-133">Architettura della soluzione di esempio</span><span class="sxs-lookup"><span data-stu-id="c5d03-133">Architecture of sample solution</span></span>
<span data-ttu-id="c5d03-134">L'architettura descritta in questo articolo riguarda una soluzione semplice ma è adatta anche per scenari complessi come la modellazione dei rischi per le organizzazioni di servizi finanziari, l'elaborazione e il rendering di immagini e l'analisi genomica.</span><span class="sxs-lookup"><span data-stu-id="c5d03-134">Even though the architecture described in this article is for a simple solution, it is relevant to complex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="c5d03-135">Il diagramma illustra 1) in che modo Data Factory orchestra l'elaborazione e lo spostamento dei dati e 2) in che modo Azure Batch elabora i dati in modalità parallela.</span><span class="sxs-lookup"><span data-stu-id="c5d03-135">The diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes the data in a parallel manner.</span></span> <span data-ttu-id="c5d03-136">Scaricare e stampare il diagramma per riferimento (28 x 43 cm</span><span class="sxs-lookup"><span data-stu-id="c5d03-136">Download and print the diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="c5d03-137">o formato A3): [Orchestrazione di HPC e dati con Azure Batch e Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span><span class="sxs-lookup"><span data-stu-id="c5d03-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="c5d03-138">[![Diagramma di elaborazione dei dati su larga scala](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="c5d03-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="c5d03-139">Nell'elenco seguente vengono presentati i passaggi di base del processo.</span><span class="sxs-lookup"><span data-stu-id="c5d03-139">The following list provides the basic steps of the process.</span></span> <span data-ttu-id="c5d03-140">La soluzione include il codice e le spiegazioni per compilare la soluzione end-to-end.</span><span class="sxs-lookup"><span data-stu-id="c5d03-140">The solution includes code and explanations to build the end-to-end solution.</span></span>

1. <span data-ttu-id="c5d03-141">**Configurare Azure Batch con un pool di nodi di calcolo (VM)**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="c5d03-142">È possibile specificare il numero di nodi e le dimensioni di ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="c5d03-142">You can specify the number of nodes and size of each node.</span></span>
2. <span data-ttu-id="c5d03-143">**Creare un'istanza di Azure Data Factory** configurata con le entità che rappresentano l'archiviazione BLOB di Azure, il servizio di calcolo di Azure Batch, i dati di input/output e una pipeline o un flusso di lavoro con attività per lo spostamento e la trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="c5d03-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="c5d03-144">**Creare un'attività personalizzata**da usare in una pipeline di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c5d03-144">**Create a custom .NET activity in the Data Factory pipeline**.</span></span> <span data-ttu-id="c5d03-145">L'attività è il codice utente che viene eseguito nel pool di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-145">The activity is your user code that runs on the Azure Batch pool.</span></span>
4. <span data-ttu-id="c5d03-146">**Archiviare grandi quantità di dati di input come BLOB nell'archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="c5d03-147">I dati vengono divisi in sezioni logiche, in genere in base al tempo.</span><span class="sxs-lookup"><span data-stu-id="c5d03-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="c5d03-148">**Data Factory copia i dati che vengono elaborati in parallelo** nel percorso secondario.</span><span class="sxs-lookup"><span data-stu-id="c5d03-148">**Data Factory copies data that is processed in parallel** to the secondary location.</span></span>
6. <span data-ttu-id="c5d03-149">**Data Factory esegue l'attività personalizzata usando il pool allocato da Batch**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-149">**Data Factory runs the custom activity using the pool allocated by Batch**.</span></span> <span data-ttu-id="c5d03-150">Data Factory può eseguire attività contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="c5d03-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="c5d03-151">Ogni attività elabora una sezione dei dati.</span><span class="sxs-lookup"><span data-stu-id="c5d03-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="c5d03-152">I risultati vengono archiviati nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d03-152">The results are stored in Azure storage.</span></span>
7. <span data-ttu-id="c5d03-153">**Data Factory sposta i risultati finali in un terzo percorso**per la distribuzione tramite un'app o per un'ulteriore elaborazione con altri strumenti.</span><span class="sxs-lookup"><span data-stu-id="c5d03-153">**Data Factory moves the final results to a third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="c5d03-154">Implementazione della soluzione di esempio</span><span class="sxs-lookup"><span data-stu-id="c5d03-154">Implementation of sample solution</span></span>
<span data-ttu-id="c5d03-155">La soluzione di esempio è intenzionalmente semplice e ha lo scopo di mostrare come usare Data Factory e Batch insieme per elaborare i set di dati.</span><span class="sxs-lookup"><span data-stu-id="c5d03-155">The sample solution is intentionally simple and is to show you how to use Data Factory and Batch together to process datasets.</span></span> <span data-ttu-id="c5d03-156">La soluzione conta semplicemente il numero di occorrenze del termine di ricerca ("Microsoft") nei file di input organizzati in una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="c5d03-156">The solution simply counts the number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="c5d03-157">Restituisce il numero in file di output.</span><span class="sxs-lookup"><span data-stu-id="c5d03-157">It outputs the count to output files.</span></span>

<span data-ttu-id="c5d03-158">**Tempo**: se si ha familiarità con le nozioni di base di Azure Data Factory e Batch e sono stati completati i prerequisiti elencati di seguito, si stima che il completamento di questa soluzione richieda 1-2 ore.</span><span class="sxs-lookup"><span data-stu-id="c5d03-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed the prerequisites listed below, we estimate this solution takes 1-2 hours to complete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c5d03-159">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c5d03-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="c5d03-160">Sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="c5d03-160">Azure subscription</span></span>
<span data-ttu-id="c5d03-161">Se non si ha una sottoscrizione di Azure, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="c5d03-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c5d03-162">Vedere [Versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5d03-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="c5d03-163">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c5d03-163">Azure storage account</span></span>
<span data-ttu-id="c5d03-164">In questa esercitazione si userà un account di archiviazione di Azure per archiviare i dati.</span><span class="sxs-lookup"><span data-stu-id="c5d03-164">You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="c5d03-165">Se non si ha un account di archiviazione di Azure, vedere [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="c5d03-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="c5d03-166">La soluzione di esempio usa l'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="c5d03-166">The sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="c5d03-167">Account Azure Batch</span><span class="sxs-lookup"><span data-stu-id="c5d03-167">Azure Batch account</span></span>
<span data-ttu-id="c5d03-168">Creare un account di Azure Batch tramite il [portale di Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="c5d03-168">Create an Azure Batch account using the [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="c5d03-169">Vedere [Creare e gestire un account Azure Batch nel portale di Azure](../batch/batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c5d03-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="c5d03-170">Annotare il nome e la chiave dell'account Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-170">Note the Azure Batch account name and account key.</span></span> <span data-ttu-id="c5d03-171">È anche possibile usare il cmdlet [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) per creare un account Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet to create an Azure Batch account.</span></span> <span data-ttu-id="c5d03-172">Per istruzioni dettagliate sull'uso del cmdlet, vedere [Guida introduttiva ai cmdlet PowerShell di Azure Batch](../batch/batch-powershell-cmdlets-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="c5d03-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="c5d03-173">Per elaborare i dati in modalità parallela in un pool di nodi di calcolo, ovvero una raccolta gestita di macchine virtuali, la soluzione di esempio usa Azure Batch indirettamente tramite una pipeline di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c5d03-173">The sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) to process data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="c5d03-174">Pool Azure Batch di macchine virtuali (VM)</span><span class="sxs-lookup"><span data-stu-id="c5d03-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="c5d03-175">Creare un **pool di Azure Batch** con almeno 2 nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="c5d03-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="c5d03-176">Nel menu a sinistra del [portale di Azure](https://portal.azure.com) fare clic su **Esplora** e quindi su **Account Batch**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-176">In the [Azure portal](https://portal.azure.com), click **Browse** in the left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="c5d03-177">Selezionare il proprio account Azure Batch per aprire il pannello **Account Batch** .</span><span class="sxs-lookup"><span data-stu-id="c5d03-177">Select your Azure Batch account to open the **Batch Account** blade.</span></span>
3. <span data-ttu-id="c5d03-178">Fare clic sul riquadro **Pool** .</span><span class="sxs-lookup"><span data-stu-id="c5d03-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="c5d03-179">Nel riquadro **pool** fare clic sul pulsante Aggiungi nella barra degli strumenti per aggiungere un pool.</span><span class="sxs-lookup"><span data-stu-id="c5d03-179">In the **Pools** blade, click Add button on the toolbar to add a pool.</span></span>
   1. <span data-ttu-id="c5d03-180">Immettere un ID per il pool (**ID pool**).</span><span class="sxs-lookup"><span data-stu-id="c5d03-180">Enter an ID for the pool (**Pool ID**).</span></span> <span data-ttu-id="c5d03-181">Prendere nota dell' **ID del pool**perché sarà necessario durante la creazione della soluzione Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c5d03-181">Note the **ID of the pool**; you need it when creating the Data Factory solution.</span></span>
   2. <span data-ttu-id="c5d03-182">Specificare **Windows Server 2012 R2** per l'impostazione Famiglia di sistemi operativi.</span><span class="sxs-lookup"><span data-stu-id="c5d03-182">Specify **Windows Server 2012 R2** for the Operating System Family setting.</span></span>
   3. <span data-ttu-id="c5d03-183">Selezionare un **piano tariffario per il nodo**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="c5d03-184">Immettere **2** come valore per l'impostazione **Pool dedicati di destinazione**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-184">Enter **2** as value for the **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="c5d03-185">Immettere **2** come valore per l'impostazione **Numero massimo attività per nodo**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-185">Enter **2** as value for the **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="c5d03-186">Fare clic su **OK** per creare il pool.</span><span class="sxs-lookup"><span data-stu-id="c5d03-186">Click **OK** to create the pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="c5d03-187">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="c5d03-187">Azure Storage Explorer</span></span>
<span data-ttu-id="c5d03-188">[Azure Storage Explorer 6 (strumento)](https://azurestorageexplorer.codeplex.com/) o [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (di ClumsyLeaf Software).</span><span class="sxs-lookup"><span data-stu-id="c5d03-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="c5d03-189">Tali strumenti sono usati per esaminare e modificare i dati nei progetti di Archiviazione di Azure, inclusi i log delle applicazioni ospitate nel cloud.</span><span class="sxs-lookup"><span data-stu-id="c5d03-189">You use these tools for inspecting and altering the data in your Azure Storage projects including the logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="c5d03-190">Creare un contenitore denominato **mycontainer** con accesso privato (Nessun accesso anonimo)</span><span class="sxs-lookup"><span data-stu-id="c5d03-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="c5d03-191">Se si usa **CloudXplorer**, creare cartelle e sottocartelle con la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="c5d03-191">If you are using **CloudXplorer**, create folders and subfolders with the following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="c5d03-192">`Inputfolder`e `outputfolder` sono le cartelle di livello superiore in `mycontainer`.</span><span class="sxs-lookup"><span data-stu-id="c5d03-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="c5d03-193">`inputfolder` contiene sottocartelle con indicatori data e ora (AAAA-MM-GG-HH).</span><span class="sxs-lookup"><span data-stu-id="c5d03-193">The `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="c5d03-194">Se si usa **Azure Storage Explorer**, nel passaggio successivo si dovranno caricare file denominati`inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` e così via.</span><span class="sxs-lookup"><span data-stu-id="c5d03-194">If you are using **Azure Storage Explorer**, in the next step, you need to upload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="c5d03-195">Le cartelle verranno create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c5d03-195">This step automatically creates the folders.</span></span>
3. <span data-ttu-id="c5d03-196">Creare un file di testo **file.txt** nel computer con contenuto che include la parola chiave **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-196">Create a text file **file.txt** on your machine with content that has the keyword **Microsoft**.</span></span> <span data-ttu-id="c5d03-197">Ad esempio: "test attività personalizzata Microsoft testare l'attività personalizzata Microsoft".</span><span class="sxs-lookup"><span data-stu-id="c5d03-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="c5d03-198">Caricare il file nelle cartelle di input seguenti nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d03-198">Upload the file to the following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="c5d03-199">Se si usa **Azure Storage Explorer**, caricare il file **file.txt** in **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-199">If you are using **Azure Storage Explorer**, upload the file **file.txt** to **mycontainer**.</span></span> <span data-ttu-id="c5d03-200">Fare clic su **Copia** sulla barra degli strumenti per creare una copia del BLOB.</span><span class="sxs-lookup"><span data-stu-id="c5d03-200">Click **Copy** on the toolbar to create a copy of the blob.</span></span> <span data-ttu-id="c5d03-201">Nella finestra di dialogo **Copia BLOB** modificare il **nome del BLOB di destinazione** in `inputfolder/2015-11-16-00/file.txt`.</span><span class="sxs-lookup"><span data-stu-id="c5d03-201">In the **Copy Blob** dialog box, change the **destination blob name** to `inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="c5d03-202">Ripetere questo passaggio per creare `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` e così via.</span><span class="sxs-lookup"><span data-stu-id="c5d03-202">Repeat this step to create `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="c5d03-203">Le cartelle verranno create automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c5d03-203">This action automatically creates the folders.</span></span>
5. <span data-ttu-id="c5d03-204">Creare un altro contenitore denominato `customactivitycontainer`.</span><span class="sxs-lookup"><span data-stu-id="c5d03-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="c5d03-205">Si carica il file ZIP dell'attività personalizzata in questo contenitore.</span><span class="sxs-lookup"><span data-stu-id="c5d03-205">You upload the custom activity zip file to this container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="c5d03-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c5d03-206">Visual Studio</span></span>
<span data-ttu-id="c5d03-207">Installare Microsoft Visual Studio 2012 o versione successiva per creare l'attività Batch personalizzata da usare nella soluzione Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c5d03-207">Install Microsoft Visual Studio 2012 or later to create the custom Batch activity to be used in the Data Factory solution.</span></span>

### <a name="high-level-steps-to-create-the-solution"></a><span data-ttu-id="c5d03-208">Passaggi generali per creare la soluzione</span><span class="sxs-lookup"><span data-stu-id="c5d03-208">High-level steps to create the solution</span></span>
1. <span data-ttu-id="c5d03-209">Creare un'attività personalizzata che contenga la logica di elaborazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="c5d03-209">Create a custom activity that contains the data processing logic.</span></span>
2. <span data-ttu-id="c5d03-210">Creare una data factory di Azure che usa l'attività personalizzata:</span><span class="sxs-lookup"><span data-stu-id="c5d03-210">Create an Azure data factory that uses the custom activity:</span></span>

### <a name="create-the-custom-activity"></a><span data-ttu-id="c5d03-211">Creare l'attività personalizzata</span><span class="sxs-lookup"><span data-stu-id="c5d03-211">Create the custom activity</span></span>
<span data-ttu-id="c5d03-212">L'attività personalizzata di Data Factory è il fulcro della soluzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="c5d03-212">The Data Factory custom activity is the heart of this sample solution.</span></span> <span data-ttu-id="c5d03-213">La soluzione di esempio usa Azure Batch per eseguire l'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c5d03-213">The sample solution uses Azure Batch to run the custom activity.</span></span> <span data-ttu-id="c5d03-214">Per informazioni di base su come sviluppare attività personalizzate e usarle in una pipeline di Data factory di Azure, vedere [Usare attività personalizzate in una pipeline di Data factory di Azure](data-factory-use-custom-activities.md) .</span><span class="sxs-lookup"><span data-stu-id="c5d03-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for the basic information to develop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="c5d03-215">Per creare un'attività personalizzata .NET da usare in una pipeline di Data Factory di Azure, è necessario creare un progetto della **libreria di classi .NET** con una classe che implementa l'interfaccia **IDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-215">To create a .NET custom activity that you can use in an Azure Data Factory pipeline, you need to create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="c5d03-216">Questa interfaccia ha un solo metodo, **Execute**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="c5d03-217">Questa è la firma del metodo:</span><span class="sxs-lookup"><span data-stu-id="c5d03-217">Here is the signature of the method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="c5d03-218">È necessario conoscere alcuni dei componenti chiave del metodo.</span><span class="sxs-lookup"><span data-stu-id="c5d03-218">The method has a few key components that you need to understand.</span></span>

* <span data-ttu-id="c5d03-219">Il metodo accetta quattro parametri:</span><span class="sxs-lookup"><span data-stu-id="c5d03-219">The method takes four parameters:</span></span>

  1. <span data-ttu-id="c5d03-220">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-220">**linkedServices**.</span></span> <span data-ttu-id="c5d03-221">Un elenco enumerabile di servizi collegati che collegano origini dati di input/output (ad esempio, Archiviazione BLOB di Azure) alla data factory.</span><span class="sxs-lookup"><span data-stu-id="c5d03-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) to the data factory.</span></span> <span data-ttu-id="c5d03-222">In questo esempio c'è un solo servizio collegato di tipo Archiviazione di Azure usato sia per l'input che per l'output.</span><span class="sxs-lookup"><span data-stu-id="c5d03-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="c5d03-223">**datasets**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-223">**datasets**.</span></span> <span data-ttu-id="c5d03-224">Un elenco enumerabile di set di dati.</span><span class="sxs-lookup"><span data-stu-id="c5d03-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="c5d03-225">È possibile usare questo parametro per ottenere le posizioni e gli schemi definiti da set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="c5d03-225">You can use this parameter to get the locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="c5d03-226">**activity**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-226">**activity**.</span></span> <span data-ttu-id="c5d03-227">Questo parametro rappresenta l'entità di calcolo corrente, in questo caso un servizio Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-227">This parameter represents the current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="c5d03-228">**logger**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-228">**logger**.</span></span> <span data-ttu-id="c5d03-229">Il logger consente di scrivere commenti di debug che verranno visualizzati come log dell'utente per la pipeline.</span><span class="sxs-lookup"><span data-stu-id="c5d03-229">The logger lets you write debug comments that surface as the “User” log for the pipeline.</span></span>
* <span data-ttu-id="c5d03-230">Il metodo restituisce un dizionario che può essere usato per concatenare le attività personalizzate in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="c5d03-230">The method returns a dictionary that can be used to chain custom activities together in the future.</span></span> <span data-ttu-id="c5d03-231">Questa funzionalità non è ancora implementata, quindi il metodo restituisce un dizionario vuoto.</span><span class="sxs-lookup"><span data-stu-id="c5d03-231">This feature is not implemented yet, so return an empty dictionary from the method.</span></span>

#### <a name="procedure-create-the-custom-activity"></a><span data-ttu-id="c5d03-232">Procedura: Creare l'attività personalizzata</span><span class="sxs-lookup"><span data-stu-id="c5d03-232">Procedure: Create the custom activity</span></span>
1. <span data-ttu-id="c5d03-233">Creare un progetto Libreria di classi .NET in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c5d03-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="c5d03-234">Avviare **Visual Studio 2012**/**2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="c5d03-235">Fare clic su **File**, scegliere **Nuovo** e quindi fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-235">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="c5d03-236">Espandere **Modelli** e quindi selezionare **Visual C\#**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="c5d03-237">In questa procedura dettagliata viene usato C\#, ma è possibile usare qualsiasi linguaggio .NET per sviluppare l'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c5d03-237">In this walkthrough, you use C\#, but you can use any .NET language to develop the custom activity.</span></span>
   4. <span data-ttu-id="c5d03-238">Selezionare la **libreria di classi** dall'elenco relativo ai tipi di progetto visualizzato a destra.</span><span class="sxs-lookup"><span data-stu-id="c5d03-238">Select **Class Library** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="c5d03-239">Immettere **MyDotNetActivity** for the **Nome**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-239">Enter **MyDotNetActivity** for the **Name**.</span></span>
   6. <span data-ttu-id="c5d03-240">Selezionare **C:\\ADF** per **Percorso**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-240">Select **C:\\ADF** for the **Location**.</span></span> <span data-ttu-id="c5d03-241">Creare la cartella **ADF** se non esiste.</span><span class="sxs-lookup"><span data-stu-id="c5d03-241">Create the folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="c5d03-242">Fare clic su **OK** per creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="c5d03-242">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="c5d03-243">Fare clic su **Strumenti**, scegliere **Gestione pacchetti NuGet** e quindi fare clic su **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-243">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="c5d03-244">Nella **console di gestione pacchetti**, eseguire il seguente comando per importare **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-244">In the **Package Manager Console**, execute the following command to import **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="c5d03-245">Importare nel progetto il pacchetto NuGet **Azure Storage** .</span><span class="sxs-lookup"><span data-stu-id="c5d03-245">Import the **Azure Storage** NuGet package in to the project.</span></span> <span data-ttu-id="c5d03-246">Questo pacchetto è necessario perché in questo esempio si usa l'API di archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="c5d03-246">You need this package because you use the Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="c5d03-247">Aggiungere le direttive **using** seguenti al file di origine nel progetto.</span><span class="sxs-lookup"><span data-stu-id="c5d03-247">Add the following **using** directives to the source file in the project.</span></span>

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="c5d03-248">Modificare il nome dello **spazio dei nomi** in **MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-248">Change the name of the **namespace** to **MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="c5d03-249">Modificare il nome della classe in **MyDotNetActivity** e derivarlo dall'interfaccia **IDotNetActivity** come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c5d03-249">Change the name of the class to **MyDotNetActivity** and derive it from the **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="c5d03-250">Implementare (aggiungere) il metodo **Execute** dell'interfaccia **IDotNetActivity** nella classe **MyDotNetActivity** e copiare il seguente codice di esempio nel metodo.</span><span class="sxs-lookup"><span data-stu-id="c5d03-250">Implement (Add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class and copy the following sample code to the method.</span></span> <span data-ttu-id="c5d03-251">Per una descrizione della logica usata in questo metodo, vedere la sezione [Metodo Execute](#execute-method) .</span><span class="sxs-lookup"><span data-stu-id="c5d03-251">See the [Execute Method](#execute-method) section for explanation for the logic used in this method.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is the only method of IDotNetActivity interface you must implement.
    /// In this sample, the method invokes the Calculate method to perform the core logic.  
    /// </summary>
    public IDictionary<string, string> Execute(
       IEnumerable<LinkedService> linkedServices,
       IEnumerable<Dataset> datasets,
       Activity activity,
       IActivityLogger logger)
    {
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using the same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // To create an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass the connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize the continuation token before using it in the do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get the list of input blobs from the input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns the number of occurrences of
           // the search term (“Microsoft”) in each blob associated
           // with the data slice.
           //
           // definition of the method is shown in the next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get the output dataset using the name of the dataset matched to a name in the Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob to the folder: {0}", folderPath);
    
       // create a storage object for the output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write the name of the file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload the output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} to the output blob", output);
       outputBlob.UploadText(output);
    
       // The dictionary can be used to chain custom activities together in the future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="c5d03-252">Aggiungere alla classe i metodi helper riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="c5d03-252">Add the following helper methods to the class.</span></span> <span data-ttu-id="c5d03-253">Questi metodi vengono richiamati dal metodo **Execute** .</span><span class="sxs-lookup"><span data-stu-id="c5d03-253">These methods are invoked by the **Execute** method.</span></span> <span data-ttu-id="c5d03-254">In particolare, il metodo **Calculate** isola il codice che esegue l'iterazione di ogni BLOB.</span><span class="sxs-lookup"><span data-stu-id="c5d03-254">Most importantly, the **Calculate** method isolates the code that iterates through each blob.</span></span>

    ```csharp
    /// <summary>
    /// Gets the folderPath value from the input/output dataset.
    /// </summary>
    private static string GetFolderPath(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets the fileName value from the input/output dataset.
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in the folder, counts the number of instances of search term in the file,
    /// and prepares the output text that is written to the output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
       string output = string.Empty;
       logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
       foreach (IListBlobItem listBlobItem in Bresult.Results)
       {
           CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
           if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
           {
               string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
               logger.Write("input blob text: {0}", blobText);
               string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
               var matchQuery = from word in source
                                where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                select word;
               int wordCount = matchQuery.Count();
               output += string.Format("{0} occurrences(s) of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    <span data-ttu-id="c5d03-255">Il metodo **GetFolderPath** restituisce il percorso della cartella a cui punta il set di dati e il metodo **GetFileName** restituisce il nome del BLOB o del file a cui punta il set di dati.</span><span class="sxs-lookup"><span data-stu-id="c5d03-255">The **GetFolderPath** method returns the path to the folder that the dataset points to and the **GetFileName** method returns the name of the blob/file that the dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="c5d03-256">Il metodo **Calculate** calcola il numero di istanze della parola chiave **Microsoft** nei file di input (BLOB nella cartella).</span><span class="sxs-lookup"><span data-stu-id="c5d03-256">The **Calculate** method calculates the number of instances of keyword **Microsoft** in the input files (blobs in the folder).</span></span> <span data-ttu-id="c5d03-257">Il termine di ricerca ("Microsoft") è hardcoded nel codice.</span><span class="sxs-lookup"><span data-stu-id="c5d03-257">The search term (“Microsoft”) is hard-coded in the code.</span></span>

1. <span data-ttu-id="c5d03-258">Compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="c5d03-258">Compile the project.</span></span> <span data-ttu-id="c5d03-259">Fare clic su **Compila** dal menu e scegliere **Compila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-259">Click **Build** from the menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="c5d03-260">Avviare **Esplora risorse** e passare alla cartella **bin\\debug** o **bin\\release**, a seconda del tipo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-260">Launch **Windows Explorer**, and navigate to **bin\\debug** or **bin\\release** folder depending on the type of build.</span></span>
3. <span data-ttu-id="c5d03-261">Creare un file ZIP **MyDotNetActivity.zip** che contiene tutti i file binari disponibili nella cartella **\\bin\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-261">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the **\\bin\\Debug** folder.</span></span> <span data-ttu-id="c5d03-262">È possibile includere il file **MyDotNetActivity.pdb** per ottenere altri dettagli, ad esempio il numero della riga nel codice sorgente che ha causato il problema in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="c5d03-262">You may want to include the MyDotNetActivity.**pdb** file so that you get additional details such as line number in the source code that caused the issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="c5d03-263">Caricare **MyDotNetActivity.zip** come BLOB nel contenitore BLOB `customactivitycontainer` nell'archiviazione BLOB di Azure usata dal servizio collegato **StorageLinkedService** in **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-263">Upload **MyDotNetActivity.zip** as a blob to the blob container: `customactivitycontainer` in the Azure blob storage that the **StorageLinkedService** linked service in the **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="c5d03-264">Se non esiste ancora, creare il contenitore BLOB `customactivitycontainer`.</span><span class="sxs-lookup"><span data-stu-id="c5d03-264">Create the blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="c5d03-265">Metodo Execute</span><span class="sxs-lookup"><span data-stu-id="c5d03-265">Execute method</span></span>
<span data-ttu-id="c5d03-266">Questa sezione fornisce informazioni dettagliate e note sul codice nel metodo Execute.</span><span class="sxs-lookup"><span data-stu-id="c5d03-266">This section provides more details and notes about the code in the Execute method.</span></span>

1. <span data-ttu-id="c5d03-267">I membri per l'iterazione della raccolta di input si trovano nello spazio dei nomi [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c5d03-267">The members for iterating through the input collection are found in the [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="c5d03-268">L'iterazione della raccolta di BLOB richiede l'uso della classe **BlobContinuationToken** .</span><span class="sxs-lookup"><span data-stu-id="c5d03-268">Iterating through the blob collection requires using the **BlobContinuationToken** class.</span></span> <span data-ttu-id="c5d03-269">In sostanza, è necessario usare un ciclo do-while con il token come meccanismo di uscita dal ciclo.</span><span class="sxs-lookup"><span data-stu-id="c5d03-269">In essence, you must use a do-while loop with the token as the mechanism for exiting the loop.</span></span> <span data-ttu-id="c5d03-270">Per altre informazioni, vedere [Come usare l'archivio BLOB da .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="c5d03-270">For more information, see [How to use Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="c5d03-271">Di seguito è illustrato un ciclo di base:</span><span class="sxs-lookup"><span data-stu-id="c5d03-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize the continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get the list of input blobs from the input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   <span data-ttu-id="c5d03-272">Per informazioni dettagliate, vedere la documentazione relativa al metodo [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c5d03-272">See the documentation for the [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="c5d03-273">Il codice per l'uso in modo logico del set di BLOB viene inserito all'interno del ciclo do-while.</span><span class="sxs-lookup"><span data-stu-id="c5d03-273">The code for working through the set of blobs logically goes within the do-while loop.</span></span> <span data-ttu-id="c5d03-274">Nel metodo **Execute** il ciclo do-while passa l'elenco di BLOB a un metodo denominato **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-274">In the **Execute** method, the do-while loop passes the list of blobs to a method named **Calculate**.</span></span> <span data-ttu-id="c5d03-275">Il metodo restituisce una variabile stringa denominata **output** che rappresenta il risultato dell'iterazione di tutti i BLOB nel segmento.</span><span class="sxs-lookup"><span data-stu-id="c5d03-275">The method returns a string variable named **output** that is the result of having iterated through all the blobs in the segment.</span></span>

   <span data-ttu-id="c5d03-276">Restituisce il numero di occorrenze del termine di ricerca, **Microsoft**, nel BLOB passato al metodo **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-276">It returns the number of occurrences of the search term (**Microsoft**) in the blob passed to the **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="c5d03-277">Una volta completato, il metodo **Calculate** deve essere scritto in un nuovo BLOB.</span><span class="sxs-lookup"><span data-stu-id="c5d03-277">Once the **Calculate** method has done the work, it must be written to a new blob.</span></span> <span data-ttu-id="c5d03-278">Quindi, per ogni set di BLOB elaborati è possibile scrivere un nuovo BLOB con i risultati.</span><span class="sxs-lookup"><span data-stu-id="c5d03-278">So for every set of blobs processed, a new blob can be written with the results.</span></span> <span data-ttu-id="c5d03-279">Per scrivere in un nuovo BLOB, trovare prima di tutto il set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="c5d03-279">To write to a new blob, first find the output dataset.</span></span>

    ```csharp
    // Get the output dataset using the name of the dataset matched to a name in the Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="c5d03-280">Il codice chiama anche un metodo helper, **GetFolderPath** , per recuperare il percorso della cartella, ovvero il nome del contenitore di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-280">The code also calls a helper method: **GetFolderPath** to retrieve the folder path (the storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="c5d03-281">**GetFolderPath** esegue il cast dell'oggetto DataSet a un oggetto AzureBlobDataSet, che include una proprietà denominata FolderPath.</span><span class="sxs-lookup"><span data-stu-id="c5d03-281">The **GetFolderPath** casts the DataSet object to an AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="c5d03-282">Il codice chiama il metodo **GetFileName** per recuperare il nome del file (nome del BLOB).</span><span class="sxs-lookup"><span data-stu-id="c5d03-282">The code calls the **GetFileName** method to retrieve the file name (blob name).</span></span> <span data-ttu-id="c5d03-283">Il codice è simile a quello visto in precedenza per ottenere il percorso della cartella.</span><span class="sxs-lookup"><span data-stu-id="c5d03-283">The code is similar to the above code to get the folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="c5d03-284">Il nome del file viene scritto creando un oggetto URI.</span><span class="sxs-lookup"><span data-stu-id="c5d03-284">The name of the file is written by creating a URI object.</span></span> <span data-ttu-id="c5d03-285">Il costruttore URI usa la proprietà **BlobEndpoint** per restituire il nome del contenitore.</span><span class="sxs-lookup"><span data-stu-id="c5d03-285">The URI constructor uses the **BlobEndpoint** property to return the container name.</span></span> <span data-ttu-id="c5d03-286">Il nome del file e il percorso della cartella vengono aggiunti per creare l'URI del BLOB di output.</span><span class="sxs-lookup"><span data-stu-id="c5d03-286">The folder path and file name are added to construct the output blob URI.</span></span>  

    ```csharp
    // Write the name of the file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="c5d03-287">Il nome del file è stato scritto e ora è possibile scrivere la stringa di output del metodo **Calculate** in un nuovo BLOB:</span><span class="sxs-lookup"><span data-stu-id="c5d03-287">The name of the file has been written and now you can write the output string from the **Calculate** method to a new blob:</span></span>

    ```csharp
    // Create a blob and upload the output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} to the output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-the-data-factory"></a><span data-ttu-id="c5d03-288">Creare la data factory</span><span class="sxs-lookup"><span data-stu-id="c5d03-288">Create the data factory</span></span>
<span data-ttu-id="c5d03-289">La sezione [Creare l'attività personalizzata](#create-the-custom-activity) ha illustrato come creare un'attività personalizzata e caricare il file ZIP con i file binari e il file PDB in un contenitore BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d03-289">In the [Create the custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded the zip file with binaries and the PDB file to an Azure blob container.</span></span> <span data-ttu-id="c5d03-290">Questa sezione illustra come creare una **data factory** di Azure con una **pipeline** che usa l'**attività personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-290">In this section, you create an Azure **data factory** with a **pipeline** that uses the **custom activity**.</span></span>

<span data-ttu-id="c5d03-291">Il set di dati di input per l'attività personalizzata rappresenta i BLOB (file) nella cartella di input (`mycontainer\\inputfolder`) nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="c5d03-291">The input dataset for the custom activity represents the blobs (files) in the input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="c5d03-292">Il set di dati di output per l'attività rappresenta i BLOB di output nella cartella di output (`mycontainer\\outputfolder`) nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="c5d03-292">The output dataset for the activity represents the output blobs in the output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="c5d03-293">Lasciare uno o più file nelle cartelle di input:</span><span class="sxs-lookup"><span data-stu-id="c5d03-293">Drop one or more files in the input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="c5d03-294">Ad esempio, rilasciare un file, file.txt, con il contenuto seguente in ognuna delle cartelle.</span><span class="sxs-lookup"><span data-stu-id="c5d03-294">For example, drop one file (file.txt) with the following content into each of the folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="c5d03-295">Ogni cartella di input corrisponde a una sezione in Azure Data Factory, anche se la cartella contiene 2 o più file.</span><span class="sxs-lookup"><span data-stu-id="c5d03-295">Each input folder corresponds to a slice in Azure Data Factory even if the folder has 2 or more files.</span></span> <span data-ttu-id="c5d03-296">Quando ogni sezione viene elaborata dalla pipeline, l'attività personalizzata esegue l'iterazione di tutti i BLOB nella cartella di input per tale sezione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-296">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span></span>

<span data-ttu-id="c5d03-297">Verranno visualizzati cinque file di output con lo stesso contenuto.</span><span class="sxs-lookup"><span data-stu-id="c5d03-297">You see five output files with the same content.</span></span> <span data-ttu-id="c5d03-298">Ad esempio, il file di output generato dall'elaborazione del file nella cartella 2015-11-16-00 ha il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="c5d03-298">For example, the output file from processing the file in the 2015-11-16-00 folder has the following content:</span></span>

```
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="c5d03-299">Se si rilasciano più file, ovvero file.txt, file2.txt, file3.txt, con lo stesso contenuto nella cartella di input, nel file di output viene visualizzato il contenuto seguente.</span><span class="sxs-lookup"><span data-stu-id="c5d03-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with the same content to the input folder, you see the following content in the output file.</span></span> <span data-ttu-id="c5d03-300">Ogni cartella (2015-11-16-00 e così via) corrisponde a una sezione in questo esempio, anche se la cartella contiene più file di input.</span><span class="sxs-lookup"><span data-stu-id="c5d03-300">Each folder (2015-11-16-00, etc.) corresponds to a slice in this sample even though the folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="c5d03-301">Il file di output include tre righe, una per ogni file di input (BLOB) presente nella cartella associata alla sezione (2015-11-16-00).</span><span class="sxs-lookup"><span data-stu-id="c5d03-301">The output file has three lines now, one for each input file (blob) in the folder associated with the slice (2015-11-16-00).</span></span>

<span data-ttu-id="c5d03-302">Per ogni esecuzione di attività viene creata un'attività.</span><span class="sxs-lookup"><span data-stu-id="c5d03-302">A task is created for each activity run.</span></span> <span data-ttu-id="c5d03-303">In questo esempio è presente una sola attività nella pipeline.</span><span class="sxs-lookup"><span data-stu-id="c5d03-303">In this sample, there is only one activity in the pipeline.</span></span> <span data-ttu-id="c5d03-304">Quando una sezione viene elaborata dalla pipeline, l'attività personalizzata viene eseguita in Azure Batch per elaborare la sezione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-304">When a slice is processed by the pipeline, the custom activity runs on Azure Batch to process the slice.</span></span> <span data-ttu-id="c5d03-305">Poiché ci sono cinque sezioni, e ogni sezione può contenere più BLOB o file, in Azure Batch vengono create cinque attività.</span><span class="sxs-lookup"><span data-stu-id="c5d03-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="c5d03-306">Quando un'attività viene eseguita in Batch, si tratta in effetti dell'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c5d03-306">When a task runs on Batch, it is actually the custom activity that is running.</span></span>

<span data-ttu-id="c5d03-307">La procedura dettagliata seguente fornisce dettagli aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="c5d03-307">The following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-the-data-factory"></a><span data-ttu-id="c5d03-308">Passaggio 1: Creare la data factory</span><span class="sxs-lookup"><span data-stu-id="c5d03-308">Step 1: Create the data factory</span></span>
1. <span data-ttu-id="c5d03-309">Dopo l'accesso al [portale di Azure](https://portal.azure.com/), seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c5d03-309">After logging in to the [Azure portal](https://portal.azure.com/), do the following steps:</span></span>

   1. <span data-ttu-id="c5d03-310">Fare clic su **Nuovo** nel menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="c5d03-310">Click **NEW** on the left menu.</span></span>
   2. <span data-ttu-id="c5d03-311">Fare clic su **Dati e analisi** nel pannello **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-311">Click **Data + Analytics** in the **New** blade.</span></span>
   3. <span data-ttu-id="c5d03-312">Fare clic su **Data factory** nel pannello **Analisi dei dati**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-312">Click **Data Factory** on the **Data analytics** blade.</span></span>
2. <span data-ttu-id="c5d03-313">Nel pannello **Nuova data factory** immettere **CustomActivityFactory** come Nome.</span><span class="sxs-lookup"><span data-stu-id="c5d03-313">In the **New data factory** blade, enter **CustomActivityFactory** for the Name.</span></span> <span data-ttu-id="c5d03-314">È necessario specificare un nome univoco globale per l'istanza di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c5d03-314">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="c5d03-315">Se viene visualizzato l'errore **Il nome "CustomActivityFactory" per la data factory non è disponibile**, cambiare il nome della data factory, ad esempio, **nomeutenteCustomActivityFactory**, e provare di nuovo a crearla.</span><span class="sxs-lookup"><span data-stu-id="c5d03-315">If you receive the error: **Data factory name “CustomActivityFactory” is not available**, change the name of the data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="c5d03-316">Fare clic su **NOME DEL GRUPPO DI RISORSE**e selezionare un gruppo di risorse esistente o crearne uno.</span><span class="sxs-lookup"><span data-stu-id="c5d03-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="c5d03-317">Verificare se la sottoscrizione e l'area in cui si vuole creare la data factory sono quelle corrette.</span><span class="sxs-lookup"><span data-stu-id="c5d03-317">Verify that you are using the correct subscription and region where you want the data factory to be created.</span></span>
5. <span data-ttu-id="c5d03-318">Fare clic su **Crea** nel pannello **Nuova data factory**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-318">Click **Create** on the **New data factory** blade.</span></span>
6. <span data-ttu-id="c5d03-319">Nel **Dashboard** del portale di Azure verrà visualizzata la data factory in fase di creazione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-319">You see the data factory being created in the **Dashboard** of the Azure portal.</span></span>
7. <span data-ttu-id="c5d03-320">Dopo la creazione della data factory, viene visualizzata la pagina corrispondente con elencato il contenuto della data factory.</span><span class="sxs-lookup"><span data-stu-id="c5d03-320">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="c5d03-321">Passaggio 2: Creare servizi collegati</span><span class="sxs-lookup"><span data-stu-id="c5d03-321">Step 2: Create linked services</span></span>
<span data-ttu-id="c5d03-322">I servizi collegati collegano archivi dati o servizi di calcolo a una data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d03-322">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="c5d03-323">In questo passaggio si collegheranno l'account di **Archiviazione di Azure** e l'account **Azure Batch** alla data factory.</span><span class="sxs-lookup"><span data-stu-id="c5d03-323">In this step, you link your **Azure Storage** account and **Azure Batch** account to your data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="c5d03-324">Creare il servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c5d03-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="c5d03-325">Fare clic sul riquadro **Creare e distribuire** nel pannello **DATA FACTORY** per **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-325">Click the **Author and deploy** tile on the **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="c5d03-326">Viene visualizzato l'editor di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c5d03-326">You see the Data Factory Editor.</span></span>
2. <span data-ttu-id="c5d03-327">Fare clic su **Nuovo archivio dati** sulla barra dei comandi e scegliere **Archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-327">Click **New data store** on the command bar and choose **Azure storage.**</span></span> <span data-ttu-id="c5d03-328">Nell'editor verrà visualizzato lo script JSON per la creazione di un servizio collegato Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d03-328">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="c5d03-329">Sostituire **account name** con il nome dell'account di archiviazione di Azure e **account key** con la chiave di accesso dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d03-329">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="c5d03-330">Per informazioni su come ottenere la chiave di accesso alle risorse di archiviazione, vedere la sezione [Visualizzare, copiare e rigenerare le chiavi di accesso nelle risorse di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="c5d03-330">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="c5d03-331">Fare clic su **Distribuisci** sulla barra dei comandi per distribuire il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="c5d03-331">Click **Deploy** on the command bar to deploy the linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="c5d03-332">Creare il servizio collegato Azure Batch</span><span class="sxs-lookup"><span data-stu-id="c5d03-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="c5d03-333">In questo passaggio si crea un servizio collegato per l'account **Azure Batch** che verrà usato per eseguire l'attività personalizzata di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c5d03-333">In this step, you create a linked service for your **Azure Batch** account that is used to run the Data Factory custom activity.</span></span>

1. <span data-ttu-id="c5d03-334">Fare clic su **Nuovo calcolo** sulla barra dei comandi e scegliere **Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-334">Click **New compute** on the command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="c5d03-335">Nell'editor verrà visualizzato lo script JSON per la creazione di un servizio collegato Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-335">You should see the JSON script for creating an Azure Batch linked service in the editor.</span></span>
2. <span data-ttu-id="c5d03-336">Nello script JSON:</span><span class="sxs-lookup"><span data-stu-id="c5d03-336">In the JSON script:</span></span>

   1. <span data-ttu-id="c5d03-337">Sostituire **account name** con il nome dell'account Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-337">Replace **account name** with the name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="c5d03-338">Sostituire **access key** con la chiave di accesso dell'account Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-338">Replace **access key** with the access key of the Azure Batch account.</span></span>
   3. <span data-ttu-id="c5d03-339">Immettere l'ID del pool per la proprietà **poolName****.**</span><span class="sxs-lookup"><span data-stu-id="c5d03-339">Enter the ID of the pool for the **poolName** property**.**</span></span> <span data-ttu-id="c5d03-340">Per questa proprietà è possibile specificare il nome del pool o del pool di ID.</span><span class="sxs-lookup"><span data-stu-id="c5d03-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="c5d03-341">Immettere l'URI del batch per la proprietà JSON **batchUri** .</span><span class="sxs-lookup"><span data-stu-id="c5d03-341">Enter the batch URI for the **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="c5d03-342">L'**URL** nel **pannello dell'account Azure Batch** è nel formato seguente: \<nomeaccount\>.\<area\>.batch.azure.com. Per la proprietà **batchUri** nello script JSON è necessario **rimuovere "accountname."**</span><span class="sxs-lookup"><span data-stu-id="c5d03-342">The **URL** from the **Azure Batch account blade** is in the following format: \<accountname\>.\<region\>.batch.azure.com. For the **batchUri** property in the JSON, you need to **remove "accountname."**</span></span> <span data-ttu-id="c5d03-343">dall'URL.</span><span class="sxs-lookup"><span data-stu-id="c5d03-343">from the URL.</span></span> <span data-ttu-id="c5d03-344">Esempio: `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="c5d03-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="c5d03-345">Per la proprietà **poolName** è anche possibile specificare l'ID del pool anziché il nome del pool.</span><span class="sxs-lookup"><span data-stu-id="c5d03-345">For the **poolName** property, you can also specify the ID of the pool instead of the name of the pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c5d03-346">Il servizio Data Factory non supporta un'opzione su richiesta per il Batch di Azure come accade per HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c5d03-346">The Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="c5d03-347">È possibile utilizzare solo il proprio pool di Batch di Azure in una data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d03-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="c5d03-348">Specificare **StorageLinkedService** for the **StorageLinkedService** .</span><span class="sxs-lookup"><span data-stu-id="c5d03-348">Specify **StorageLinkedService** for the **linkedServiceName** property.</span></span> <span data-ttu-id="c5d03-349">Questo servizio collegato è stato creato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="c5d03-349">You created this linked service in the previous step.</span></span> <span data-ttu-id="c5d03-350">Questo servizio di archiviazione viene usato come area di staging per file e log.</span><span class="sxs-lookup"><span data-stu-id="c5d03-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="c5d03-351">Fare clic su **Distribuisci** sulla barra dei comandi per distribuire il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="c5d03-351">Click **Deploy** on the command bar to deploy the linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="c5d03-352">Passaggio 3: Creare set di dati</span><span class="sxs-lookup"><span data-stu-id="c5d03-352">Step 3: Create datasets</span></span>
<span data-ttu-id="c5d03-353">In questo passaggio vengono creati set di dati per rappresentare i dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="c5d03-353">In this step, you create datasets to represent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="c5d03-354">Creare set di dati di input</span><span class="sxs-lookup"><span data-stu-id="c5d03-354">Create input dataset</span></span>
1. <span data-ttu-id="c5d03-355">Nell'**Editor** per l'istanza di Data factory fare clic sul pulsante **Nuovo set di dati** sulla barra degli strumenti, quindi scegliere **Archiviazione BLOB di Azure** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="c5d03-355">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="c5d03-356">Sostituire il codice JSON nel riquadro a destra con il frammento JSON seguente.</span><span class="sxs-lookup"><span data-stu-id="c5d03-356">Replace the JSON in the right pane with the following JSON snippet:</span></span>

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           },
           "external": true,
           "policy": {}
       }
    }
    ```

    <span data-ttu-id="c5d03-357">Più avanti in questa procedura dettagliata viene creata una pipeline con ora di inizio: 2015-11-16T00:00:00Z e ora di fine: 2015-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="c5d03-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="c5d03-358">Viene pianificata per produrre dati **ogni ora**, in modo da ottenere 5 sezioni di input/output tra **00**:00:00 -\> **05**:00:00.</span><span class="sxs-lookup"><span data-stu-id="c5d03-358">It is scheduled to produce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="c5d03-359">La **frequenza** e l'**intervallo** per il set di dati di input sono impostati su **Ora** e **1**. Ciò significa che la sezione di input è disponibile ogni ora.</span><span class="sxs-lookup"><span data-stu-id="c5d03-359">The **frequency** and **interval** for the input dataset is set to **Hour** and **1**, which means that the input slice is available hourly.</span></span>

    <span data-ttu-id="c5d03-360">Qui sono indicate le ore di inizio per ogni sezione, rappresentate dalla variabile di sistema **SliceStart** nel precedente frammento di codice JSON.</span><span class="sxs-lookup"><span data-stu-id="c5d03-360">Here are the start times for each slice, which is represented by **SliceStart** system variable in the above JSON snippet.</span></span>

    | <span data-ttu-id="c5d03-361">**Sezione**</span><span class="sxs-lookup"><span data-stu-id="c5d03-361">**Slice**</span></span> | <span data-ttu-id="c5d03-362">**Ora di inizio**</span><span class="sxs-lookup"><span data-stu-id="c5d03-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="c5d03-363">1</span><span class="sxs-lookup"><span data-stu-id="c5d03-363">1</span></span>         | <span data-ttu-id="c5d03-364">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="c5d03-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="c5d03-365">2</span><span class="sxs-lookup"><span data-stu-id="c5d03-365">2</span></span>         | <span data-ttu-id="c5d03-366">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="c5d03-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="c5d03-367">3</span><span class="sxs-lookup"><span data-stu-id="c5d03-367">3</span></span>         | <span data-ttu-id="c5d03-368">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="c5d03-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="c5d03-369">4</span><span class="sxs-lookup"><span data-stu-id="c5d03-369">4</span></span>         | <span data-ttu-id="c5d03-370">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="c5d03-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="c5d03-371">5</span><span class="sxs-lookup"><span data-stu-id="c5d03-371">5</span></span>         | <span data-ttu-id="c5d03-372">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="c5d03-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="c5d03-373">La proprietà **folderPath** viene calcolata usando la parte di anno, mese, giorno e ora dell'ora di inizio sezione (**SliceStart**).</span><span class="sxs-lookup"><span data-stu-id="c5d03-373">The **folderPath** is calculated by using the year, month, day, and hour part of the slice start time (**SliceStart**).</span></span> <span data-ttu-id="c5d03-374">Ecco quindi come viene eseguito il mapping di una cartella di input a una sezione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-374">Therefore, here is how an input folder is mapped to a slice.</span></span>

    | <span data-ttu-id="c5d03-375">**Sezione**</span><span class="sxs-lookup"><span data-stu-id="c5d03-375">**Slice**</span></span> | <span data-ttu-id="c5d03-376">**Ora di inizio**</span><span class="sxs-lookup"><span data-stu-id="c5d03-376">**Start time**</span></span>          | <span data-ttu-id="c5d03-377">**Cartella di input**</span><span class="sxs-lookup"><span data-stu-id="c5d03-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="c5d03-378">1</span><span class="sxs-lookup"><span data-stu-id="c5d03-378">1</span></span>         | <span data-ttu-id="c5d03-379">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="c5d03-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="c5d03-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="c5d03-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="c5d03-381">2</span><span class="sxs-lookup"><span data-stu-id="c5d03-381">2</span></span>         | <span data-ttu-id="c5d03-382">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="c5d03-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="c5d03-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="c5d03-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="c5d03-384">3</span><span class="sxs-lookup"><span data-stu-id="c5d03-384">3</span></span>         | <span data-ttu-id="c5d03-385">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="c5d03-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="c5d03-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="c5d03-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="c5d03-387">4</span><span class="sxs-lookup"><span data-stu-id="c5d03-387">4</span></span>         | <span data-ttu-id="c5d03-388">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="c5d03-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="c5d03-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="c5d03-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="c5d03-390">5</span><span class="sxs-lookup"><span data-stu-id="c5d03-390">5</span></span>         | <span data-ttu-id="c5d03-391">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="c5d03-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="c5d03-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="c5d03-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="c5d03-393">Fare clic su **Distribuisci** sulla barra degli strumenti per creare e distribuire la tabella **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-393">Click **Deploy** on the toolbar to create and deploy the **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="c5d03-394">Creare il set di dati di output</span><span class="sxs-lookup"><span data-stu-id="c5d03-394">Create output dataset</span></span>
<span data-ttu-id="c5d03-395">In questo passaggio si crea un altro set di dati di tipo AzureBlob per rappresentare i dati di output.</span><span class="sxs-lookup"><span data-stu-id="c5d03-395">In this step, you create another dataset of type AzureBlob to represent the output data.</span></span>

1. <span data-ttu-id="c5d03-396">Nell'**Editor** per l'istanza di Data Factory fare clic sul pulsante **Nuovo set di dati** sulla barra degli strumenti, quindi scegliere **Archiviazione BLOB di Azure** dal menu a discesa.</span><span class="sxs-lookup"><span data-stu-id="c5d03-396">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="c5d03-397">Sostituire il codice JSON nel riquadro a destra con il frammento JSON seguente.</span><span class="sxs-lookup"><span data-stu-id="c5d03-397">Replace the JSON in the right pane with the following JSON snippet:</span></span>

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
               "partitionedBy": [
                   {
                       "name": "slice",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy-MM-dd-HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           }
       }
    }
    ```

    <span data-ttu-id="c5d03-398">Un BLOB o file di output viene generato per ogni sezione di input.</span><span class="sxs-lookup"><span data-stu-id="c5d03-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="c5d03-399">Ecco come viene denominato il file di output per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="c5d03-400">Tutti i file di output vengono generati in una cartella di output: `mycontainer\\outputfolder`.</span><span class="sxs-lookup"><span data-stu-id="c5d03-400">All the output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="c5d03-401">**Sezione**</span><span class="sxs-lookup"><span data-stu-id="c5d03-401">**Slice**</span></span> | <span data-ttu-id="c5d03-402">**Ora di inizio**</span><span class="sxs-lookup"><span data-stu-id="c5d03-402">**Start time**</span></span>          | <span data-ttu-id="c5d03-403">**File di output**</span><span class="sxs-lookup"><span data-stu-id="c5d03-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="c5d03-404">1</span><span class="sxs-lookup"><span data-stu-id="c5d03-404">1</span></span>         | <span data-ttu-id="c5d03-405">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="c5d03-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="c5d03-406">2015-11-16-**00.txt**</span><span class="sxs-lookup"><span data-stu-id="c5d03-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="c5d03-407">2</span><span class="sxs-lookup"><span data-stu-id="c5d03-407">2</span></span>         | <span data-ttu-id="c5d03-408">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="c5d03-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="c5d03-409">2015-11-16-**01.txt**</span><span class="sxs-lookup"><span data-stu-id="c5d03-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="c5d03-410">3</span><span class="sxs-lookup"><span data-stu-id="c5d03-410">3</span></span>         | <span data-ttu-id="c5d03-411">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="c5d03-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="c5d03-412">2015-11-16-**02.txt**</span><span class="sxs-lookup"><span data-stu-id="c5d03-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="c5d03-413">4</span><span class="sxs-lookup"><span data-stu-id="c5d03-413">4</span></span>         | <span data-ttu-id="c5d03-414">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="c5d03-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="c5d03-415">2015-11-16-**03.txt**</span><span class="sxs-lookup"><span data-stu-id="c5d03-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="c5d03-416">5</span><span class="sxs-lookup"><span data-stu-id="c5d03-416">5</span></span>         | <span data-ttu-id="c5d03-417">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="c5d03-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="c5d03-418">2015-11-16-**04.txt**</span><span class="sxs-lookup"><span data-stu-id="c5d03-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="c5d03-419">Tenere presente che tutti i file in una cartella di input, ad esempio 2015-11-16-00, fanno parte di una sezione con l'ora di inizio 2015-11-16-00.</span><span class="sxs-lookup"><span data-stu-id="c5d03-419">Remember that all the files in an input folder (for example: 2015-11-16-00) are part of a slice with the start time: 2015-11-16-00.</span></span> <span data-ttu-id="c5d03-420">Quando la sezione viene elaborata, l'attività personalizzata esamina ogni file e produce una riga nel file di output con il numero di occorrenze del termine di ricerca ("Microsoft").</span><span class="sxs-lookup"><span data-stu-id="c5d03-420">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="c5d03-421">Se nella cartella 2015-11-16-00 sono presenti tre file, ci saranno tre righe nel file di output 2015-11-16-00.txt.</span><span class="sxs-lookup"><span data-stu-id="c5d03-421">If there are three files in the folder 2015-11-16-00, there are three lines in the output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="c5d03-422">Fare clic su **Distribuisci** sulla barra degli strumenti per creare e distribuire **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-422">Click **Deploy** on the toolbar to create and deploy the **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-the-pipeline-with-custom-activity"></a><span data-ttu-id="c5d03-423">Passaggio 4: Creare ed eseguire la pipeline con l'attività personalizzata</span><span class="sxs-lookup"><span data-stu-id="c5d03-423">Step 4: Create and run the pipeline with custom activity</span></span>
<span data-ttu-id="c5d03-424">In questo passaggio si crea una pipeline con un'attività, ovvero l'attività personalizzata creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c5d03-424">In this step, you create a pipeline with one activity, the custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5d03-425">Prima di creare la pipeline, caricare il **file.txt** nelle cartelle di input nel contenitore BLOB, se ancora non è stato fatto.</span><span class="sxs-lookup"><span data-stu-id="c5d03-425">If you haven't uploaded the **file.txt** to input folders in the blob container, do so before creating the pipeline.</span></span> <span data-ttu-id="c5d03-426">La proprietà **isPaused** è impostata su false nello script JSON della pipeline, quindi la pipeline verrà eseguita immediatamente non appena sarà trascorsa la data di **inizio**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-426">The **isPaused** property is set to false in the pipeline JSON, so the pipeline runs immediately as the **start** date is in the past.</span></span>
>
>

1. <span data-ttu-id="c5d03-427">Nell'Editor di Data factory fare clic su **Nuova pipeline** sulla barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="c5d03-427">In the Data Factory Editor, click **New pipeline** on the command bar.</span></span> <span data-ttu-id="c5d03-428">Se non viene visualizzato il comando, fare clic su **... (puntini di sospensione)** per visualizzarlo.</span><span class="sxs-lookup"><span data-stu-id="c5d03-428">If you do not see the command, click **... (Ellipsis)** to see it.</span></span>
2. <span data-ttu-id="c5d03-429">Sostituire lo script JSON nel riquadro a destra con lo script JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="c5d03-429">Replace the JSON in the right pane with the following JSON script:</span></span>

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   <span data-ttu-id="c5d03-430">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="c5d03-430">Note the following points:</span></span>

   * <span data-ttu-id="c5d03-431">Nella pipeline esiste una sola attività ed è di tipo **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-431">There is only one activity in the pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="c5d03-432">**AssemblyName** è impostato sul nome della DLL **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-432">**AssemblyName** is set to the name of the DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="c5d03-433">**EntryPoint** è impostato su **MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-433">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="c5d03-434">Si tratta in sostanza di \<spazio dei nomi\>.\<nome classe\> nel codice.</span><span class="sxs-lookup"><span data-stu-id="c5d03-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="c5d03-435">**PackageLinkedService** è impostato su **StorageLinkedService** che punta all'archivio BLOB contenente il file ZIP dell'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c5d03-435">**PackageLinkedService** is set to **StorageLinkedService** that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="c5d03-436">Se vengono usati account di archiviazione di Azure diversi per i file di input/output e per il file ZIP dell'attività personalizzata, è necessario creare un altro servizio collegato Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d03-436">If you are using different Azure Storage accounts for input/output files and the custom activity zip file, you have to create another Azure Storage linked service.</span></span> <span data-ttu-id="c5d03-437">Questo articolo presuppone che venga usato lo stesso account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d03-437">This article assumes that you are using the same Azure Storage account.</span></span>
   * <span data-ttu-id="c5d03-438">**PackageFile** è impostato su **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-438">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="c5d03-439">Ha il formato: \<contenitoreperlozip\>/\<nomedellozip.zip\>.</span><span class="sxs-lookup"><span data-stu-id="c5d03-439">It is in the format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="c5d03-440">L'attività personalizzata accetta **InputDataset** come input e **OutputDataset** come output.</span><span class="sxs-lookup"><span data-stu-id="c5d03-440">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="c5d03-441">La proprietà **linkedServiceName** dell'attività personalizzata punta ad **AzureBatchLinkedService** per indicare a Data Factory di Azure che l'attività personalizzata deve essere eseguita in Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-441">The **linkedServiceName** property of the custom activity points to the **AzureBatchLinkedService**, which tells Azure Data Factory that the custom activity needs to run on Azure Batch.</span></span>
   * <span data-ttu-id="c5d03-442">L'impostazione **concurrency** è importante.</span><span class="sxs-lookup"><span data-stu-id="c5d03-442">The **concurrency** setting is important.</span></span> <span data-ttu-id="c5d03-443">Se si usa il valore predefinito 1, le sezioni vengono elaborate una dopo l'altra, anche se sono disponibili 2 o più nodi di calcolo nel pool di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-443">If you use the default value, which is 1, even if you have 2 or more compute nodes in the Azure Batch pool, the slices are processed one after another.</span></span> <span data-ttu-id="c5d03-444">In questo modo non si sfrutterà la funzionalità di elaborazione parallela di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-444">Therefore, you are not taking advantage of the parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="c5d03-445">Se si imposta **concurrency** su un valore superiore, ad esempio 2, potranno essere elaborate contemporaneamente due sezioni (corrispondenti a due attività in Azure Batch), usando in questo caso entrambe le VM nel pool di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-445">If you set **concurrency** to a higher value, say 2, it means that two slices (corresponds to two tasks in Azure Batch) can be processed at the same time, in which case, both the VMs in the Azure Batch pool are utilized.</span></span> <span data-ttu-id="c5d03-446">Impostare quindi correttamente la proprietà concurrency.</span><span class="sxs-lookup"><span data-stu-id="c5d03-446">Therefore, set the concurrency property appropriately.</span></span>
   * <span data-ttu-id="c5d03-447">Per impostazione predefinita, viene eseguita solo un'attività (sezione) in una VM in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="c5d03-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="c5d03-448">Questo avviene perché, per impostazione predefinita, il **numero massimo di attività per ogni VM** è impostato su 1 per un pool di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-448">The reason is that, by default, the **Maximum tasks per VM** is set to 1 for an Azure Batch pool.</span></span> <span data-ttu-id="c5d03-449">Come parte dei prerequisiti è stato creato un pool con questa proprietà impostata su 2, per poter eseguire contemporaneamente due sezioni di Data Factory in una VM.</span><span class="sxs-lookup"><span data-stu-id="c5d03-449">As part of prerequisites, you created a pool with this property set to 2, so two Data Factory slices can be running on a VM at the same time.</span></span>

    -   <span data-ttu-id="c5d03-450">**isPaused** è impostata su false per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="c5d03-450">**isPaused** property is set to false by default.</span></span> <span data-ttu-id="c5d03-451">In questo esempio la pipeline viene eseguita immediatamente perché le sezioni hanno inizio nel passato.</span><span class="sxs-lookup"><span data-stu-id="c5d03-451">The pipeline runs immediately in this example because the slices start in the past.</span></span> <span data-ttu-id="c5d03-452">È possibile impostare questa proprietà su true per sospendere la pipeline e reimpostarla su false per riavviare la pipeline.</span><span class="sxs-lookup"><span data-stu-id="c5d03-452">You can set this property to true to pause the pipeline and set it back to false to restart.</span></span>

    -   <span data-ttu-id="c5d03-453">L'ora di **inizio** e l'ora di **fine** hanno cinque ore di differenza e le sezioni vengono prodotte ogni ora, quindi la pipeline genera cinque sezioni.</span><span class="sxs-lookup"><span data-stu-id="c5d03-453">The **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by the pipeline.</span></span>

1. <span data-ttu-id="c5d03-454">Fare clic su **Distribuisci** sulla barra dei comandi per distribuire la pipeline.</span><span class="sxs-lookup"><span data-stu-id="c5d03-454">Click **Deploy** on the command bar to deploy the pipeline.</span></span>

#### <a name="step-5-test-the-pipeline"></a><span data-ttu-id="c5d03-455">Passaggio 5: Testare la pipeline</span><span class="sxs-lookup"><span data-stu-id="c5d03-455">Step 5: Test the pipeline</span></span>
<span data-ttu-id="c5d03-456">In questo passaggio si testerà la pipeline rilasciando i file nelle cartelle di input.</span><span class="sxs-lookup"><span data-stu-id="c5d03-456">In this step, you test the pipeline by dropping files into the input folders.</span></span> <span data-ttu-id="c5d03-457">Iniziare testando la pipeline con un file per una cartella di input.</span><span class="sxs-lookup"><span data-stu-id="c5d03-457">Let’s start with testing the pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="c5d03-458">Nel pannello Data factory del portale di Azure fare clic su **Diagramma**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-458">In the Data Factory blade in the Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="c5d03-459">Nella vista diagramma fare doppio clic sul set di dati di input **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-459">In the diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="c5d03-460">Verrà visualizzato il pannello **InputDataset** con tutte e cinque le sezioni pronte.</span><span class="sxs-lookup"><span data-stu-id="c5d03-460">You should see the **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="c5d03-461">Notare i valori di **ORA DI INIZIO SEZIONE** e **ORA DI FINE SEZIONE** per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-461">Notice the **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="c5d03-462">Nella vista **Diagramma** fare clic su **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-462">In the **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="c5d03-463">Le cinque sezioni di output si trovano nello stato Ready se sono già state generate.</span><span class="sxs-lookup"><span data-stu-id="c5d03-463">You should see that the five output slices are in the Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="c5d03-464">Usare il portale di Azure per visualizzare le **attività** associate alle **sezioni** e vedere in quale VM viene eseguita ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-464">Use Azure portal to view the **tasks** associated with the **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="c5d03-465">Per altre informazioni, vedere la sezione [Integrazione di Data Factory e Batch](#data-factory-and-batch-integration) .</span><span class="sxs-lookup"><span data-stu-id="c5d03-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="c5d03-466">I file di output verranno visualizzati nella cartella `outputfolder` di `mycontainer` nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d03-466">You should see the output files in the `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="c5d03-467">Saranno presenti cinque file di output, uno per ogni sezione di input.</span><span class="sxs-lookup"><span data-stu-id="c5d03-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="c5d03-468">Il contenuto di ogni file di output sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="c5d03-468">Each of the output file should have content similar to the following output:</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="c5d03-469">Il diagramma seguente illustra il mapping tra le sezioni di Data Factory e le attività in Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-469">The following diagram illustrates how the Data Factory slices map to tasks in Azure Batch.</span></span> <span data-ttu-id="c5d03-470">In questo esempio a una sezione è associata una sola esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="c5d03-471">Si proverà ora con più file in una cartella.</span><span class="sxs-lookup"><span data-stu-id="c5d03-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="c5d03-472">Creare i file **file2.txt**, **file3.txt**, **file4.txt****file5.txt** con lo stesso contenuto del file.txt nella cartella: **2015-11-06-01**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with the same content as in file.txt in the folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="c5d03-473">Nella cartella di output **eliminare** il file di output **2015-11-16-01.txt**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-473">In the output folder, **delete** the output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="c5d03-474">A questo punto, nel pannello **OutputDataset** fare clic con il pulsante destro del mouse sulla sezione con **ORA DI INIZIO SEZIONE** impostata su **11/16/2015 01:00:00 AM** e scegliere **Esegui** per rieseguire/rielaborare la sezione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-474">Now, in the **OutputDataset** blade, right-click the slice with **SLICE START TIME** set to **11/16/2015 01:00:00 AM**, and click **Run** to rerun/re-process the slice.</span></span> <span data-ttu-id="c5d03-475">A questo punto, la sezione ha cinque file anziché un file.</span><span class="sxs-lookup"><span data-stu-id="c5d03-475">Now, the slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="c5d03-476">Dopo che la sezione è stata eseguita e lo stato è diventato **Pronto**, verificare il contenuto nel file di output per questa sezione (**2015-11-16-01.txt**) nella cartella `outputfolder` di `mycontainer` nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="c5d03-476">After the slice runs and its status is **Ready**, verify the content in the output file for this slice (**2015-11-16-01.txt**) in the `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="c5d03-477">Deve essere presente una riga per ogni file della sezione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-477">There should be a line for each file of the slice.</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="c5d03-478">Se il file di output 2015-11-16-01.txt non è stato eliminato prima di provare con cinque file di input, si vedrà una riga della precedente esecuzione della sezione e cinque righe dell'esecuzione attuale della sezione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-478">If you did not delete the output file 2015-11-16-01.txt before trying with five input files, you see one line from the previous slice run and five lines from the current slice run.</span></span> <span data-ttu-id="c5d03-479">Per impostazione predefinita, il contenuto viene aggiunto ai file di output, se esiste già.</span><span class="sxs-lookup"><span data-stu-id="c5d03-479">By default, the content is appended to output file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="c5d03-480">Integrazione di Data Factory e Batch</span><span class="sxs-lookup"><span data-stu-id="c5d03-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="c5d03-481">Il servizio Data Factory crea un processo in Azure Batch denominato `adf-poolname:job-xxx`.</span><span class="sxs-lookup"><span data-stu-id="c5d03-481">The Data Factory service creates a job in Azure Batch with the name: `adf-poolname:job-xxx`.</span></span>

![Azure Data Factory: processi di Batch](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="c5d03-483">Per ogni esecuzione attività di una sezione viene creata un'attività nel processo.</span><span class="sxs-lookup"><span data-stu-id="c5d03-483">A task in the job is created for each activity run of a slice.</span></span> <span data-ttu-id="c5d03-484">Se sono presenti 10 sezioni pronte per l'elaborazione, nel processo vengono create 10 attività.</span><span class="sxs-lookup"><span data-stu-id="c5d03-484">If there are 10 slices ready to be processed, 10 tasks are created in the job.</span></span> <span data-ttu-id="c5d03-485">È possibile eseguire più sezioni in parallelo se sono disponibili più nodi di calcolo nel pool.</span><span class="sxs-lookup"><span data-stu-id="c5d03-485">You can have more than one slice running in parallel if you have multiple compute nodes in the pool.</span></span> <span data-ttu-id="c5d03-486">È anche possibile eseguire più sezioni nello stesso nodo di calcolo se l'impostazione per il numero massimo di attività per nodo di calcolo è > 1.</span><span class="sxs-lookup"><span data-stu-id="c5d03-486">If the maximum tasks per compute node is set to > 1, there can be more than one slice running on the same compute.</span></span>

<span data-ttu-id="c5d03-487">In questo esempio ci sono cinque sezioni, quindi cinque attività in Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="c5d03-488">Con la proprietà **concurrency** impostata su **5** nello script JSON della pipeline in Azure Data Factory e il **numero massimo di attività per ogni VM** impostato su **2** nel pool di Azure Batch con **2** VM, le attività vengono eseguite molto velocemente. Controllare l'ora di inizio e fine delle attività.</span><span class="sxs-lookup"><span data-stu-id="c5d03-488">With the **concurrency** set to **5** in the pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set to **2** in Azure Batch pool with **2** VMs, the tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="c5d03-489">Usare il portale per visualizzare il processo Batch e le relative attività associate alle **sezioni** e vedere in quale VM viene eseguita ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-489">Use the portal to view the Batch job and its tasks that are associated with the **slices** and see what VM each slice ran on.</span></span>

![Azure Data Factory: attività processi di Batch](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-the-pipeline"></a><span data-ttu-id="c5d03-491">Eseguire il debug della pipeline</span><span class="sxs-lookup"><span data-stu-id="c5d03-491">Debug the pipeline</span></span>
<span data-ttu-id="c5d03-492">Il debug è costituito da alcune tecniche di base:</span><span class="sxs-lookup"><span data-stu-id="c5d03-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="c5d03-493">Se la sezione di input non è impostata su **Ready**, verificare che la struttura di cartelle di input sia corretta e che file.txt sia presente nelle cartelle di input.</span><span class="sxs-lookup"><span data-stu-id="c5d03-493">If the input slice is not set to **Ready**, confirm that the input folder structure is correct and file.txt exists in the input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="c5d03-494">Nel metodo **Execute** dell'attività personalizzata usare l'oggetto **IActivityLogger** per registrare informazioni utili per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="c5d03-494">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span></span> <span data-ttu-id="c5d03-495">I messaggi registrati verranno visualizzati nel file user\_0.log.</span><span class="sxs-lookup"><span data-stu-id="c5d03-495">The logged messages show up in the user\_0.log file.</span></span>

   <span data-ttu-id="c5d03-496">Nel pannello **OutputDataset** fare clic sulla sezione per visualizzare il relativo pannello **SEZIONE DATI**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-496">In the **OutputDataset** blade, click the slice to see the **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="c5d03-497">Verranno visualizzate le **esecuzioni di attività** per quella sezione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="c5d03-498">Dovrebbe essere visualizzata una esecuzione attività per questa sezione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-498">You should see one activity run for the slice.</span></span> <span data-ttu-id="c5d03-499">Facendo clic su **Esegui** sulla barra dei comandi è possibile avviare un'altra esecuzione di attività per la stessa sezione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-499">If you click **Run** in the command bar, you can start another activity run for the same slice.</span></span>

   <span data-ttu-id="c5d03-500">Quando si fa clic sull'esecuzione attività viene visualizzato il pannello **DETTAGLI ESECUZIONE ATTIVITÀ** con un elenco di file di log.</span><span class="sxs-lookup"><span data-stu-id="c5d03-500">When you click the activity run, you see the **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="c5d03-501">I messaggi registrati verranno visualizzati nel file **user\_0.log**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-501">You see logged messages in the **user\_0.log** file.</span></span> <span data-ttu-id="c5d03-502">Quando si verifica un errore vengono visualizzate tre esecuzioni attività perché il numero di tentativi è impostato su 3 nel codice JSON della pipeline/attività.</span><span class="sxs-lookup"><span data-stu-id="c5d03-502">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span></span> <span data-ttu-id="c5d03-503">Quando si fa clic sull'esecuzione attività vengono visualizzati i file di log che è possibile esaminare per risolvere l'errore.</span><span class="sxs-lookup"><span data-stu-id="c5d03-503">When you click the activity run, you see the log files that you can review to troubleshoot the error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="c5d03-504">Nell'elenco dei file di log fare clic su **user-0.log**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-504">In the list of log files, click the **user-0.log**.</span></span> <span data-ttu-id="c5d03-505">Nel riquadro destro sono riportati i risultati dell'uso del metodo **IActivityLogger.Write** .</span><span class="sxs-lookup"><span data-stu-id="c5d03-505">In the right panel are the results of using the **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="c5d03-506">È consigliabile cercare anche nel file system-0.log eventuali messaggi di errore di sistema ed eccezioni.</span><span class="sxs-lookup"><span data-stu-id="c5d03-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="c5d03-507">Includere il file **PDB** nel file ZIP in modo che i dettagli dell'errore contengano informazioni come lo **stack di chiamate** quando si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="c5d03-507">Include the **PDB** file in the zip file so that the error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="c5d03-508">Tutti i file nel file ZIP dell'attività personalizzata devono trovarsi nel **primo livello** , senza sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="c5d03-508">All the files in the zip file for the custom activity must be at the **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="c5d03-509">Assicurarsi che **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip) e **packageLinkedService** (deve fare riferimento all'archivio BLOB di Azure che contiene il file ZIP) siano impostati su valori corretti.</span><span class="sxs-lookup"><span data-stu-id="c5d03-509">Ensure that the **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the Azure blob storage that contains the zip file) are set to correct values.</span></span>
6. <span data-ttu-id="c5d03-510">Se è stato risolto un errore e si vuole rielaborare la sezione, fare clic con il pulsante destro del mouse sulla sezione nel pannello **OutputDataset**, quindi scegliere **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-510">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="c5d03-511">Nell'archiviazione BLOB di Azure verrà visualizzato un **contenitore** denominato `adfjobs`.</span><span class="sxs-lookup"><span data-stu-id="c5d03-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="c5d03-512">Questo contenitore non viene eliminato automaticamente, ma è possibile farlo senza problemi dopo aver completato il test della soluzione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-512">This container is not automatically deleted, but you can safely delete it after you are done testing the solution.</span></span> <span data-ttu-id="c5d03-513">Analogamente, la soluzione Data Factory crea un **processo** di Azure Batch denominato `adf-\<pool ID/name\>:job-0000000001`.</span><span class="sxs-lookup"><span data-stu-id="c5d03-513">Similarly, the Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="c5d03-514">Dopo aver eseguito il test della soluzione, è possibile eliminare questo processo se necessario.</span><span class="sxs-lookup"><span data-stu-id="c5d03-514">You can delete this job after you test the solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="c5d03-515">L'attività personalizzata non usa il file **app** dal pacchetto.</span><span class="sxs-lookup"><span data-stu-id="c5d03-515">The custom activity does not use the **app.config** file from your package.</span></span> <span data-ttu-id="c5d03-516">Pertanto, se il codice legge tutte le stringhe di connessione dal file di configurazione, l'attività non funzionerà in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-516">Therefore, if your code reads any connection strings from the configuration file, it does not work at runtime.</span></span> <span data-ttu-id="c5d03-517">La procedura consigliata quando si usa Azure Batch consiste nell'inserire tutti i segreti in un **insieme di credenziali delle chiavi di Azure**, usare un'entità servizio basata su certificato per proteggere l'insieme di credenziali e distribuire il certificato nel pool di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-517">The best practice when using Azure Batch is to hold any secrets in an **Azure KeyVault**, use a certificate-based service principal to protect the keyvault, and distribute the certificate to Azure Batch pool.</span></span> <span data-ttu-id="c5d03-518">L'attività personalizzata .NET può quindi accedere ai segreti dall'insieme di credenziali delle chiavi in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-518">The .NET custom activity then can access secrets from the KeyVault at runtime.</span></span> <span data-ttu-id="c5d03-519">Questa è una soluzione generica e può essere ridimensionata per qualsiasi tipo di segreto, non solo per una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-519">This solution is a generic one and can scale to any type of secret, not just connection string.</span></span>

    <span data-ttu-id="c5d03-520">Esiste una soluzione più semplice, ma non consigliata: è possibile creare un **servizio collegato di Azure SQL** con le impostazioni della stringa di connessione, creare un set di dati che usa il servizio collegato e concatenare tale set di dati come set di dati di input fittizio all'attività .NET personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c5d03-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses the linked service, and chain the dataset as a dummy input dataset to the custom .NET activity.</span></span> <span data-ttu-id="c5d03-521">È quindi possibile accedere alla stringa di connessione del servizio collegato nel codice dell'attività personalizzata, che dovrebbe funzionare correttamente in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-521">You can then access the linked service's connection string in the custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-the-sample"></a><span data-ttu-id="c5d03-522">Estendere l'esempio</span><span class="sxs-lookup"><span data-stu-id="c5d03-522">Extend the sample</span></span>
<span data-ttu-id="c5d03-523">È possibile estendere questo esempio per ottenere altre informazioni sulle funzionalità di Azure Data Factory e Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-523">You can extend this sample to learn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="c5d03-524">Ad esempio, per elaborare le sezioni in un intervallo di tempo diverso, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c5d03-524">For example, to process slices in a different time range, do the following steps:</span></span>

1. <span data-ttu-id="c5d03-525">Aggiungere le sottocartelle seguenti nella cartella `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09. Inserire i file di input in queste cartelle.</span><span class="sxs-lookup"><span data-stu-id="c5d03-525">Add the following subfolders in the `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="c5d03-526">Modificare l'ora di fine per la pipeline da `2015-11-16T05:00:00Z` a `2015-11-16T10:00:00Z`.</span><span class="sxs-lookup"><span data-stu-id="c5d03-526">Change the end time for the pipeline from `2015-11-16T05:00:00Z` to `2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="c5d03-527">In **Vista diagramma** fare doppio clic su **InputDataset** e verificare che le sezioni di input siano pronte.</span><span class="sxs-lookup"><span data-stu-id="c5d03-527">In the **Diagram View**, double-click the **InputDataset**, and confirm that the input slices are ready.</span></span> <span data-ttu-id="c5d03-528">Fare doppio clic su **OuptutDataset** per visualizzare lo stato delle sezioni di output.</span><span class="sxs-lookup"><span data-stu-id="c5d03-528">Double-click **OuptutDataset** to see the state of output slices.</span></span> <span data-ttu-id="c5d03-529">Se lo stato è Pronto, controllare i file di output nella cartella di output.</span><span class="sxs-lookup"><span data-stu-id="c5d03-529">If they are in Ready state, check the output folder for the output files.</span></span>
2. <span data-ttu-id="c5d03-530">Aumentare o diminuire l'impostazione **concurrency** per comprenderne gli effetti sulle prestazioni della soluzione, in particolare l'elaborazione che si verifica in Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="c5d03-530">Increase or decrease the **concurrency** setting to understand how it affects the performance of your solution, especially the processing that occurs on Azure Batch.</span></span> <span data-ttu-id="c5d03-531">Per altre informazioni sull'impostazione **concurrency** , vedere Passaggio 4: Creare ed eseguire la pipeline.</span><span class="sxs-lookup"><span data-stu-id="c5d03-531">(See Step 4: Create and run the pipeline for more on the **concurrency** setting.)</span></span>
3. <span data-ttu-id="c5d03-532">Creare un pool con un **numero massimo di attività per ogni VM**più alto o più basso.</span><span class="sxs-lookup"><span data-stu-id="c5d03-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="c5d03-533">Aggiornare il servizio collegato Azure Batch nella soluzione Data Factory per usare il nuovo pool creato.</span><span class="sxs-lookup"><span data-stu-id="c5d03-533">To use the new pool you created, update the Azure Batch linked service in the Data Factory solution.</span></span> <span data-ttu-id="c5d03-534">Per altre informazioni sull'impostazione del **numero massimo di attività per ogni VM** , vedere Passaggio 4: Creare ed eseguire la pipeline.</span><span class="sxs-lookup"><span data-stu-id="c5d03-534">(See Step 4: Create and run the pipeline for more on the **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="c5d03-535">Creare un pool di Azure Batch con la funzionalità **Scalabilità automatica** .</span><span class="sxs-lookup"><span data-stu-id="c5d03-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="c5d03-536">Il ridimensionamento automatico dei nodi di calcolo in un pool di Azure Batch è una regolazione dinamica della potenza di elaborazione usata dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c5d03-536">Automatically scaling compute nodes in an Azure Batch pool is the dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="c5d03-537">Di seguito la formula di esempio consente di ottenere il comportamento seguente: quando il pool viene creato inizialmente, inizia con 1 macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c5d03-537">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="c5d03-538">La metrica $PendingTasks definisce il numero di attività in esecuzione e quelle in coda.</span><span class="sxs-lookup"><span data-stu-id="c5d03-538">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="c5d03-539">La formula trova il numero medio di attività in sospeso negli ultimi 180 secondi e imposta TargetDedicated di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="c5d03-539">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="c5d03-540">Assicura che TargetDedicated non vada mai oltre 25 macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="c5d03-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="c5d03-541">Pertanto, quando vengono inviate nuove attività, il pool si espande automaticamente e al completamento delle attività le macchine virtuali diventano disponibili una alla volta e la scalabilità automatica le riduce.</span><span class="sxs-lookup"><span data-stu-id="c5d03-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span></span> <span data-ttu-id="c5d03-542">È possibile regolare startingNumberOfVMs e maxNumberofVMs in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="c5d03-542">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span></span>
 
    <span data-ttu-id="c5d03-543">Formula di scalabilità automatica:</span><span class="sxs-lookup"><span data-stu-id="c5d03-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="c5d03-544">Per i dettagli, vedere [Ridimensionare automaticamente i nodi di calcolo in un pool di Azure Batch](../batch/batch-automatic-scaling.md) .</span><span class="sxs-lookup"><span data-stu-id="c5d03-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="c5d03-545">Se il pool usa il valore predefinito [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), possono essere necessari 15-30 minuti perché il servizio Batch prepari la VM prima di eseguire l'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c5d03-545">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span></span>  <span data-ttu-id="c5d03-546">Se il pool usa un valore autoScaleEvaluationInterval diverso, il servizio Batch può richiedere un valore autoScaleEvaluationInterval + 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="c5d03-546">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="c5d03-547">Nella soluzione di esempio il metodo**Execute** richiama il metodo **Calculate** che elabora una sezione di dati di input per generare una sezione di dati di output.</span><span class="sxs-lookup"><span data-stu-id="c5d03-547">In the sample solution, the **Execute** method invokes the **Calculate** method that processes an input data slice to produce an output data slice.</span></span> <span data-ttu-id="c5d03-548">È possibile scrivere un metodo personalizzato per elaborare i dati di input e sostituire la chiamata al metodo Calculate nel metodo Execute con una chiamata al metodo personalizzato.</span><span class="sxs-lookup"><span data-stu-id="c5d03-548">You can write your own method to process input data and replace the Calculate method call in the Execute method with a call to your method.</span></span>

### <a name="next-steps-consume-the-data"></a><span data-ttu-id="c5d03-549">Passaggi successivi: Utilizzare i dati</span><span class="sxs-lookup"><span data-stu-id="c5d03-549">Next steps: Consume the data</span></span>
<span data-ttu-id="c5d03-550">Dopo l'elaborazione dei dati, è possibile usarli con strumenti online come **Microsoft Power BI**.</span><span class="sxs-lookup"><span data-stu-id="c5d03-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="c5d03-551">Ecco alcuni collegamenti che illustrano Power BI e come è possibile usarlo in Azure:</span><span class="sxs-lookup"><span data-stu-id="c5d03-551">Here are links to help you understand Power BI and how to use it in Azure:</span></span>

* [<span data-ttu-id="c5d03-552">Esplorare un set di dati in Power BI</span><span class="sxs-lookup"><span data-stu-id="c5d03-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="c5d03-553">Introduzione a Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="c5d03-553">Getting started with the Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="c5d03-554">Aggiornamento dei dati in Power BI</span><span class="sxs-lookup"><span data-stu-id="c5d03-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="c5d03-555">Azure e Power BI - Panoramica di base</span><span class="sxs-lookup"><span data-stu-id="c5d03-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="c5d03-556">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="c5d03-556">References</span></span>
* [<span data-ttu-id="c5d03-557">Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="c5d03-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="c5d03-558">Introduzione al servizio Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="c5d03-558">Introduction to Azure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="c5d03-559">Introduzione a Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="c5d03-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="c5d03-560">Usare attività personalizzate in una pipeline di Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="c5d03-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="c5d03-561">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="c5d03-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="c5d03-562">Nozioni di base su Azure Batch</span><span class="sxs-lookup"><span data-stu-id="c5d03-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="c5d03-563">Cenni preliminari sulle funzionalità di Azure Batch</span><span class="sxs-lookup"><span data-stu-id="c5d03-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="c5d03-564">Creare e gestire un account Azure Batch nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c5d03-564">Create and manage Azure Batch account in the Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="c5d03-565">Introduzione alla libreria di Azure Batch per .NET</span><span class="sxs-lookup"><span data-stu-id="c5d03-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
