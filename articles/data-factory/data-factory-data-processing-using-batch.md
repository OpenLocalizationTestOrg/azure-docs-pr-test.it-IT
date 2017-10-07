---
title: aaaProcess set di dati su larga scala con Data Factory e Batch | Documenti Microsoft
description: "Viene descritto come pipeline di tooprocess enormi quantità di dati in una Data Factory di Azure con funzionalità di elaborazione parallela di Batch di Azure."
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
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="45bde-103">Elaborazione di fogli dati su larga scala con Data Factory e Batch</span><span class="sxs-lookup"><span data-stu-id="45bde-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="45bde-104">Questo articolo descrive l'architettura di una soluzione di esempio che sposta ed elabora set di dati su larga scala in modo automatico e pianificato.</span><span class="sxs-lookup"><span data-stu-id="45bde-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="45bde-105">Fornisce inoltre una soluzione di hello tooimplement procedura dettagliata end-to-end con Azure Data Factory e i Batch di Azure.</span><span class="sxs-lookup"><span data-stu-id="45bde-105">It also provides an end-to-end walkthrough tooimplement hello solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="45bde-106">Questo articolo è più lungo dei nostri articoli tipici perché contiene la procedura dettagliata per un'intera soluzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="45bde-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="45bde-107">Se si sta tooBatch nuovo e Data Factory, è possibile acquisire informazioni questi servizi e come interagiscono tra loro.</span><span class="sxs-lookup"><span data-stu-id="45bde-107">If you are new tooBatch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="45bde-108">Se si conosca servizi hello e è progettazione/creazione di una soluzione, può concentrare su hello [sezione architettura](#architecture-of-sample-solution) di articolo hello e se si sviluppa una soluzione o un prototipo, è inoltre possibile tootry out istruzioni dettagliate sull'hello [procedura dettagliata](#implementation-of-sample-solution).</span><span class="sxs-lookup"><span data-stu-id="45bde-108">If you know something about hello services and are designing/architecting a solution, you may focus just on hello [architecture section](#architecture-of-sample-solution) of hello article and if you are developing a prototype or a solution, you may also want tootry out step-by-step instructions in hello [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="45bde-109">Microsoft invita gli utenti a inviare i loro commenti su questo contenuto e sulle relative modalità di impiego.</span><span class="sxs-lookup"><span data-stu-id="45bde-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="45bde-110">In primo luogo, si esaminerà come servizi Data Factory e Batch agevola l'elaborazione di grandi set di dati nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in hello cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="45bde-111">Perché Azure Batch?</span><span class="sxs-lookup"><span data-stu-id="45bde-111">Why Azure Batch?</span></span>
<span data-ttu-id="45bde-112">Azure Batch consente applicazioni su larga scala parallele e ad alte prestazioni (HPC) computing toorun in modo efficiente nel cloud di hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-112">Azure Batch enables you toorun large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="45bde-113">È un servizio di piattaforma che pianifica toorun di lavoro a utilizzo intensivo di calcolo su una raccolta di macchine virtuali gestita e possa automaticamente la scala di calcolo esigenze hello toomeet di risorse dei processi.</span><span class="sxs-lookup"><span data-stu-id="45bde-113">It's a platform service that schedules compute-intensive work toorun on a managed collection of virtual machines, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span>

<span data-ttu-id="45bde-114">Con il servizio Batch hello, definire tooexecute risorse di calcolo di Azure le applicazioni in parallelo e su larga scala.</span><span class="sxs-lookup"><span data-stu-id="45bde-114">With hello Batch service, you define Azure compute resources tooexecute your applications in parallel, and at scale.</span></span> <span data-ttu-id="45bde-115">È possibile eseguire su richiesta o pianificati processi ed è necessario toomanually creare, configurare e gestire un cluster HPC, singole macchine virtuali, reti virtuali o un processo complesso e infrastruttura di pianificazione di attività.</span><span class="sxs-lookup"><span data-stu-id="45bde-115">You can run on-demand or scheduled jobs, and you don't need toomanually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="45bde-116">Vedere i seguenti articoli se non si ha familiarità con Azure Batch modo di conoscere l'architettura di implementazione della soluzione hello descritto in questo articolo hello hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-116">See hello following articles if you are not familiar with Azure Batch as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>   

* [<span data-ttu-id="45bde-117">Nozioni di base su Azure Batch</span><span class="sxs-lookup"><span data-stu-id="45bde-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="45bde-118">Panoramica delle funzionalità Batch</span><span class="sxs-lookup"><span data-stu-id="45bde-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="45bde-119">(facoltativo) toolearn ulteriori informazioni su Azure Batch, vedere hello [il percorso di apprendimento per Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span><span class="sxs-lookup"><span data-stu-id="45bde-119">(optional) toolearn more about Azure Batch, see hello [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="45bde-120">Perché Azure Data Factory?</span><span class="sxs-lookup"><span data-stu-id="45bde-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="45bde-121">Data Factory è un servizio di integrazione di dati basato su cloud che Orchestra e automatizza lo spostamento di hello e trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="45bde-121">Data Factory is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="45bde-122">Con il servizio di Data Factory hello, è possibile creare pipeline di dati gestiti spostano i dati locali e cloud archivio dati centralizzata tooa archivi di dati (ad esempio: archiviazione Blob di Azure) e processo/trasformare dati tramite i servizi, ad esempio HDInsight di Azure e Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="45bde-122">Using hello Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores tooa centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="45bde-123">È inoltre possibile pianificare toorun pipeline di dati in un modo pianificato (oraria, giornaliera, settimanale, ecc.) e il monitoraggio e gestirli in problemi di tooidentify un riepilogo e intraprendere azioni.</span><span class="sxs-lookup"><span data-stu-id="45bde-123">You can also schedule data pipelines toorun in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance tooidentify issues and take action.</span></span>

<span data-ttu-id="45bde-124">Vedere i seguenti articoli se non si ha familiarità con Azure Data Factory modo di conoscere l'architettura di implementazione della soluzione hello descritto in questo articolo hello hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-124">See hello following articles if you are not familiar with Azure Data Factory as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>  

* [<span data-ttu-id="45bde-125">Introduzione ad Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="45bde-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="45bde-126">Creare la prima pipeline di dati</span><span class="sxs-lookup"><span data-stu-id="45bde-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="45bde-127">(facoltativo) toolearn ulteriori informazioni su Data Factory di Azure, vedere hello [il percorso di apprendimento per Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="45bde-127">(optional) toolearn more about Azure Data Factory, see hello [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="45bde-128">Data Factory e Batch insieme</span><span class="sxs-lookup"><span data-stu-id="45bde-128">Data Factory and Batch together</span></span>
<span data-ttu-id="45bde-129">Data Factory include attività predefinite, ad esempio attività di copia toocopy o spostare i dati dai dati di origine archiviano tooa archivio dati di destinazione e dati tooprocess attività Hive con i cluster Hadoop (HDInsight) in Azure.</span><span class="sxs-lookup"><span data-stu-id="45bde-129">Data Factory includes built-in activities such as Copy Activity toocopy/move data from a source data store tooa destination data store and Hive Activity tooprocess data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="45bde-130">Per un elenco delle attività di trasformazione supportate, vedere le informazioni sulle [attività di trasformazione dati](data-factory-data-transformation-activities.md) .</span><span class="sxs-lookup"><span data-stu-id="45bde-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="45bde-131">Inoltre consente si toocreate .NET attività personalizzate dati toomove o un processo con la logica personalizzata ed eseguire queste attività in un cluster HDInsight di Azure o in un pool di Batch di Azure di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="45bde-131">It also allows you toocreate custom .NET activities toomove or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="45bde-132">Quando si usa Azure Batch, è possibile configurare tooauto pool hello della scala (aggiungere o rimuovere le macchine virtuali in base al carico di lavoro hello) in base a una formula è fornire.</span><span class="sxs-lookup"><span data-stu-id="45bde-132">When you use Azure Batch, you can configure hello pool tooauto-scale (add or remove VMs based on hello workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="45bde-133">Architettura della soluzione di esempio</span><span class="sxs-lookup"><span data-stu-id="45bde-133">Architecture of sample solution</span></span>
<span data-ttu-id="45bde-134">Anche se l'architettura di hello descritto in questo articolo è per una semplice soluzione, è toocomplex rilevanti scenari di rischio per la modellazione servizi finanziari, l'elaborazione di immagini e il rendering e genomica analysis.</span><span class="sxs-lookup"><span data-stu-id="45bde-134">Even though hello architecture described in this article is for a simple solution, it is relevant toocomplex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="45bde-135">Hello illustrata 1) come Data Factory gestisce lo spostamento dei dati e l'elaborazione e 2) le modalità di elaborazione di Batch di Azure hello dati in modo parallelo.</span><span class="sxs-lookup"><span data-stu-id="45bde-135">hello diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes hello data in a parallel manner.</span></span> <span data-ttu-id="45bde-136">Download e il diagramma di stampa hello per semplificarne (11 x 17.</span><span class="sxs-lookup"><span data-stu-id="45bde-136">Download and print hello diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="45bde-137">o formato A3): [Orchestrazione di HPC e dati con Azure Batch e Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span><span class="sxs-lookup"><span data-stu-id="45bde-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="45bde-138">[![Diagramma di elaborazione dei dati su larga scala](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="45bde-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="45bde-139">Hello elenco seguente vengono illustrate operazioni di base hello del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-139">hello following list provides hello basic steps of hello process.</span></span> <span data-ttu-id="45bde-140">soluzione Hello include codice e le spiegazioni soluzione end-to-end di hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="45bde-140">hello solution includes code and explanations toobuild hello end-to-end solution.</span></span>

1. <span data-ttu-id="45bde-141">**Configurare Azure Batch con un pool di nodi di calcolo (VM)**.</span><span class="sxs-lookup"><span data-stu-id="45bde-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="45bde-142">È possibile specificare il numero di hello dei nodi e le dimensioni di ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="45bde-142">You can specify hello number of nodes and size of each node.</span></span>
2. <span data-ttu-id="45bde-143">**Creare un'istanza di Azure Data Factory** configurata con le entità che rappresentano l'archiviazione BLOB di Azure, il servizio di calcolo di Azure Batch, i dati di input/output e una pipeline o un flusso di lavoro con attività per lo spostamento e la trasformazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="45bde-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="45bde-144">**Creare un'attività personalizzata di .NET in pipeline di Data Factory hello**.</span><span class="sxs-lookup"><span data-stu-id="45bde-144">**Create a custom .NET activity in hello Data Factory pipeline**.</span></span> <span data-ttu-id="45bde-145">attività Hello è codice utente in esecuzione su hello pool Batch di Azure.</span><span class="sxs-lookup"><span data-stu-id="45bde-145">hello activity is your user code that runs on hello Azure Batch pool.</span></span>
4. <span data-ttu-id="45bde-146">**Archiviare grandi quantità di dati di input come BLOB nell'archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="45bde-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="45bde-147">I dati vengono divisi in sezioni logiche, in genere in base al tempo.</span><span class="sxs-lookup"><span data-stu-id="45bde-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="45bde-148">**Data Factory copia i dati elaborati in parallelo** posizione secondaria toohello.</span><span class="sxs-lookup"><span data-stu-id="45bde-148">**Data Factory copies data that is processed in parallel** toohello secondary location.</span></span>
6. <span data-ttu-id="45bde-149">**Data Factory viene eseguita l'attività personalizzata hello utilizzando hello pool allocato dal Batch**.</span><span class="sxs-lookup"><span data-stu-id="45bde-149">**Data Factory runs hello custom activity using hello pool allocated by Batch**.</span></span> <span data-ttu-id="45bde-150">Data Factory può eseguire attività contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="45bde-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="45bde-151">Ogni attività elabora una sezione dei dati.</span><span class="sxs-lookup"><span data-stu-id="45bde-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="45bde-152">Hello risultati vengono archiviati in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="45bde-152">hello results are stored in Azure storage.</span></span>
7. <span data-ttu-id="45bde-153">**Data Factory Sposta terza posizione hello risultati finali tooa**, per la distribuzione tramite un'app o per un'ulteriore elaborazione da altri strumenti.</span><span class="sxs-lookup"><span data-stu-id="45bde-153">**Data Factory moves hello final results tooa third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="45bde-154">Implementazione della soluzione di esempio</span><span class="sxs-lookup"><span data-stu-id="45bde-154">Implementation of sample solution</span></span>
<span data-ttu-id="45bde-155">soluzione di esempio Hello è intenzionalmente semplice ed è tooshow è come toouse DataSet tooprocess insieme Data Factory e Batch.</span><span class="sxs-lookup"><span data-stu-id="45bde-155">hello sample solution is intentionally simple and is tooshow you how toouse Data Factory and Batch together tooprocess datasets.</span></span> <span data-ttu-id="45bde-156">soluzione Hello semplicemente hello delle conta le occorrenze di un termine di ricerca ("Microsoft") nei file di input organizzati in una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="45bde-156">hello solution simply counts hello number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="45bde-157">Restituisce i file toooutput conteggio hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-157">It outputs hello count toooutput files.</span></span>

<span data-ttu-id="45bde-158">**Tempo**: se si ha familiarità con concetti di base di Azure Data Factory e Batch e dispongano dei prerequisiti completato hello elencati di seguito, si stima la soluzione accetta toocomplete 1-2 ore.</span><span class="sxs-lookup"><span data-stu-id="45bde-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed hello prerequisites listed below, we estimate this solution takes 1-2 hours toocomplete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="45bde-159">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="45bde-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="45bde-160">Sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="45bde-160">Azure subscription</span></span>
<span data-ttu-id="45bde-161">Se non si ha una sottoscrizione di Azure, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="45bde-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="45bde-162">Vedere [Versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="45bde-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="45bde-163">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="45bde-163">Azure storage account</span></span>
<span data-ttu-id="45bde-164">Utilizzare un account di archiviazione di Azure per archiviare i dati di hello in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="45bde-164">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="45bde-165">Se non si ha un account di archiviazione di Azure, vedere [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="45bde-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="45bde-166">soluzione di esempio Hello utilizza l'archiviazione di blob.</span><span class="sxs-lookup"><span data-stu-id="45bde-166">hello sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="45bde-167">Account Azure Batch</span><span class="sxs-lookup"><span data-stu-id="45bde-167">Azure Batch account</span></span>
<span data-ttu-id="45bde-168">Creare un account Azure Batch utilizzando hello [portale di Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="45bde-168">Create an Azure Batch account using hello [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="45bde-169">Vedere [Creare e gestire un account Azure Batch nel portale di Azure](../batch/batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="45bde-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="45bde-170">Si noti hello Azure nome account e la chiave dell'account Batch.</span><span class="sxs-lookup"><span data-stu-id="45bde-170">Note hello Azure Batch account name and account key.</span></span> <span data-ttu-id="45bde-171">È inoltre possibile utilizzare [New AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) toocreate cmdlet un account Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="45bde-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate an Azure Batch account.</span></span> <span data-ttu-id="45bde-172">Per istruzioni dettagliate sull'uso del cmdlet, vedere [Guida introduttiva ai cmdlet PowerShell di Azure Batch](../batch/batch-powershell-cmdlets-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="45bde-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="45bde-173">soluzione di esempio Hello utilizza dati tooprocess Batch di Azure (indirettamente tramite una pipeline di Data Factory di Azure) in modo parallelo in un pool di nodi di calcolo (una raccolta di macchine virtuali gestito).</span><span class="sxs-lookup"><span data-stu-id="45bde-173">hello sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) tooprocess data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="45bde-174">Pool Azure Batch di macchine virtuali (VM)</span><span class="sxs-lookup"><span data-stu-id="45bde-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="45bde-175">Creare un **pool di Azure Batch** con almeno 2 nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="45bde-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="45bde-176">In hello [portale di Azure](https://portal.azure.com), fare clic su **Sfoglia** in hello menu a sinistra, quindi fare clic su **account Batch**.</span><span class="sxs-lookup"><span data-stu-id="45bde-176">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="45bde-177">Selezionare il hello tooopen di account Azure Batch **Account Batch** blade.</span><span class="sxs-lookup"><span data-stu-id="45bde-177">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
3. <span data-ttu-id="45bde-178">Fare clic sul riquadro **Pool** .</span><span class="sxs-lookup"><span data-stu-id="45bde-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="45bde-179">In hello **pool** pannello, fare clic su Aggiungi pulsante nella barra degli strumenti di hello tooadd un pool.</span><span class="sxs-lookup"><span data-stu-id="45bde-179">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
   1. <span data-ttu-id="45bde-180">Immettere un ID per il pool di hello (**ID pool di applicazioni**).</span><span class="sxs-lookup"><span data-stu-id="45bde-180">Enter an ID for hello pool (**Pool ID**).</span></span> <span data-ttu-id="45bde-181">Hello nota **ID del pool di hello**; è necessario durante la creazione di soluzioni di Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-181">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
   2. <span data-ttu-id="45bde-182">Specificare **Windows Server 2012 R2** per l'impostazione di hello famiglia di sistemi operativi.</span><span class="sxs-lookup"><span data-stu-id="45bde-182">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
   3. <span data-ttu-id="45bde-183">Selezionare un **piano tariffario per il nodo**.</span><span class="sxs-lookup"><span data-stu-id="45bde-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="45bde-184">Immettere **2** come valore per hello **destinazione dedicato** impostazione.</span><span class="sxs-lookup"><span data-stu-id="45bde-184">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="45bde-185">Immettere **2** come valore per hello **Max attività per ogni nodo** impostazione.</span><span class="sxs-lookup"><span data-stu-id="45bde-185">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="45bde-186">Fare clic su **OK** pool hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="45bde-186">Click **OK** toocreate hello pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="45bde-187">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="45bde-187">Azure Storage Explorer</span></span>
<span data-ttu-id="45bde-188">[Azure Storage Explorer 6 (strumento)](https://azurestorageexplorer.codeplex.com/) o [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (di ClumsyLeaf Software).</span><span class="sxs-lookup"><span data-stu-id="45bde-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="45bde-189">Utilizzare questi strumenti per analizzare e modificare i dati di hello nei progetti di archiviazione di Azure, inclusi i log di hello delle applicazioni cloud ospitato.</span><span class="sxs-lookup"><span data-stu-id="45bde-189">You use these tools for inspecting and altering hello data in your Azure Storage projects including hello logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="45bde-190">Creare un contenitore denominato **mycontainer** con accesso privato (Nessun accesso anonimo)</span><span class="sxs-lookup"><span data-stu-id="45bde-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="45bde-191">Se si utilizza **CloudXplorer**, creare cartelle e sottocartelle con hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="45bde-191">If you are using **CloudXplorer**, create folders and subfolders with hello following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="45bde-192">`Inputfolder`e `outputfolder` sono le cartelle di livello superiore in `mycontainer`.</span><span class="sxs-lookup"><span data-stu-id="45bde-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="45bde-193">Hello `inputfolder` contiene sottocartelle con data e ora (AAAA-MM-GG-HH).</span><span class="sxs-lookup"><span data-stu-id="45bde-193">hello `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="45bde-194">Se si utilizza **Azure Storage Explorer**, nel passaggio successivo hello, è necessario per i file con nomi tooupload: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` e così via.</span><span class="sxs-lookup"><span data-stu-id="45bde-194">If you are using **Azure Storage Explorer**, in hello next step, you need tooupload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="45bde-195">Questo passaggio Crea automaticamente cartelle hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-195">This step automatically creates hello folders.</span></span>
3. <span data-ttu-id="45bde-196">Creare un file di testo **file.txt** nel computer con il contenuto che contiene la parola chiave hello **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="45bde-196">Create a text file **file.txt** on your machine with content that has hello keyword **Microsoft**.</span></span> <span data-ttu-id="45bde-197">Ad esempio: "test attività personalizzata Microsoft testare l'attività personalizzata Microsoft".</span><span class="sxs-lookup"><span data-stu-id="45bde-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="45bde-198">Caricare toohello file hello seguenti cartelle di input nell'archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="45bde-198">Upload hello file toohello following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="45bde-199">Se si utilizza **Azure Storage Explorer**, caricare il file hello **file.txt** troppo**mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="45bde-199">If you are using **Azure Storage Explorer**, upload hello file **file.txt** too**mycontainer**.</span></span> <span data-ttu-id="45bde-200">Fare clic su **copia** nella barra degli strumenti di hello toocreate una copia di blob hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-200">Click **Copy** on hello toolbar toocreate a copy of hello blob.</span></span> <span data-ttu-id="45bde-201">In hello **Copy Blob** della finestra di dialogo Modifica hello **nome blob di destinazione** troppo`inputfolder/2015-11-16-00/file.txt`.</span><span class="sxs-lookup"><span data-stu-id="45bde-201">In hello **Copy Blob** dialog box, change hello **destination blob name** too`inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="45bde-202">Ripetere questo passaggio toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` e così via.</span><span class="sxs-lookup"><span data-stu-id="45bde-202">Repeat this step toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="45bde-203">Questa azione crea automaticamente cartelle hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-203">This action automatically creates hello folders.</span></span>
5. <span data-ttu-id="45bde-204">Creare un altro contenitore denominato `customactivitycontainer`.</span><span class="sxs-lookup"><span data-stu-id="45bde-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="45bde-205">Contenitore di toothis file zip attività personalizzata hello caricare.</span><span class="sxs-lookup"><span data-stu-id="45bde-205">You upload hello custom activity zip file toothis container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="45bde-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="45bde-206">Visual Studio</span></span>
<span data-ttu-id="45bde-207">Installare Microsoft Visual Studio 2012 o versioni successive toocreate hello personalizzato Batch attività toobe utilizzati in soluzioni di Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-207">Install Microsoft Visual Studio 2012 or later toocreate hello custom Batch activity toobe used in hello Data Factory solution.</span></span>

### <a name="high-level-steps-toocreate-hello-solution"></a><span data-ttu-id="45bde-208">Soluzione hello toocreate di passaggi di alto livello</span><span class="sxs-lookup"><span data-stu-id="45bde-208">High-level steps toocreate hello solution</span></span>
1. <span data-ttu-id="45bde-209">Creare un'attività personalizzata che contiene la logica di elaborazione dei dati hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-209">Create a custom activity that contains hello data processing logic.</span></span>
2. <span data-ttu-id="45bde-210">Creare una data factory di Azure che utilizza l'attività personalizzata hello:</span><span class="sxs-lookup"><span data-stu-id="45bde-210">Create an Azure data factory that uses hello custom activity:</span></span>

### <a name="create-hello-custom-activity"></a><span data-ttu-id="45bde-211">Creazione di attività personalizzata hello</span><span class="sxs-lookup"><span data-stu-id="45bde-211">Create hello custom activity</span></span>
<span data-ttu-id="45bde-212">attività di Data Factory personalizzata Hello è il cuore hello della soluzione di esempio.</span><span class="sxs-lookup"><span data-stu-id="45bde-212">hello Data Factory custom activity is hello heart of this sample solution.</span></span> <span data-ttu-id="45bde-213">soluzione di esempio Hello Usa l'attività personalizzata hello toorun di Batch di Azure.</span><span class="sxs-lookup"><span data-stu-id="45bde-213">hello sample solution uses Azure Batch toorun hello custom activity.</span></span> <span data-ttu-id="45bde-214">Vedere [utilizzare attività personalizzate in una pipeline di Data Factory di Azure](data-factory-use-custom-activities.md) per attività personalizzate toodevelop informazioni di base di hello e l'utilizzo in Data Factory di Azure delle pipeline.</span><span class="sxs-lookup"><span data-stu-id="45bde-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for hello basic information toodevelop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="45bde-215">toocreate un'attività personalizzata .NET che è possibile utilizzare in una pipeline di Data Factory di Azure, è necessario toocreate un **libreria di classi .NET** progetto con una classe che implementa che **IDotNetActivity** interfaccia.</span><span class="sxs-lookup"><span data-stu-id="45bde-215">toocreate a .NET custom activity that you can use in an Azure Data Factory pipeline, you need toocreate a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="45bde-216">Questa interfaccia ha un solo metodo, **Execute**.</span><span class="sxs-lookup"><span data-stu-id="45bde-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="45bde-217">Questa è hello firma del metodo hello:</span><span class="sxs-lookup"><span data-stu-id="45bde-217">Here is hello signature of hello method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="45bde-218">metodo Hello ha alcuni componenti chiave che è necessario toounderstand.</span><span class="sxs-lookup"><span data-stu-id="45bde-218">hello method has a few key components that you need toounderstand.</span></span>

* <span data-ttu-id="45bde-219">metodo Hello accetta quattro parametri:</span><span class="sxs-lookup"><span data-stu-id="45bde-219">hello method takes four parameters:</span></span>

  1. <span data-ttu-id="45bde-220">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="45bde-220">**linkedServices**.</span></span> <span data-ttu-id="45bde-221">Elenco enumerabile di servizi collegati che collegano le origini dati di input/output (ad esempio: archiviazione Blob di Azure) data factory di toohello.</span><span class="sxs-lookup"><span data-stu-id="45bde-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) toohello data factory.</span></span> <span data-ttu-id="45bde-222">In questo esempio c'è un solo servizio collegato di tipo Archiviazione di Azure usato sia per l'input che per l'output.</span><span class="sxs-lookup"><span data-stu-id="45bde-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="45bde-223">**datasets**.</span><span class="sxs-lookup"><span data-stu-id="45bde-223">**datasets**.</span></span> <span data-ttu-id="45bde-224">Un elenco enumerabile di set di dati.</span><span class="sxs-lookup"><span data-stu-id="45bde-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="45bde-225">È possibile utilizzare questo percorsi hello tooget di parametro e gli schemi definiti dal set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="45bde-225">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="45bde-226">**activity**.</span><span class="sxs-lookup"><span data-stu-id="45bde-226">**activity**.</span></span> <span data-ttu-id="45bde-227">Questo parametro rappresenta hello calcolo entità corrente, in questo caso, un servizio Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="45bde-227">This parameter represents hello current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="45bde-228">**logger**.</span><span class="sxs-lookup"><span data-stu-id="45bde-228">**logger**.</span></span> <span data-ttu-id="45bde-229">Consente di logger Hello di scrivere commenti debug tale area come "Utente" accesso per hello hello pipeline.</span><span class="sxs-lookup"><span data-stu-id="45bde-229">hello logger lets you write debug comments that surface as hello “User” log for hello pipeline.</span></span>
* <span data-ttu-id="45bde-230">metodo Hello restituisce un dizionario che può essere attività personalizzate toochain utilizzati insieme in futuro hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-230">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="45bde-231">Questa funzionalità non ancora implementata, pertanto restituire un dizionario vuoto da metodo hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-231">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>

#### <a name="procedure-create-hello-custom-activity"></a><span data-ttu-id="45bde-232">Procedura: Creare attività personalizzata hello</span><span class="sxs-lookup"><span data-stu-id="45bde-232">Procedure: Create hello custom activity</span></span>
1. <span data-ttu-id="45bde-233">Creare un progetto Libreria di classi .NET in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="45bde-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="45bde-234">Avviare **Visual Studio 2012**/**2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="45bde-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="45bde-235">Fare clic su **File**, punto troppo**New**, fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="45bde-235">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="45bde-236">Espandere **Modelli** e quindi selezionare **Visual C\#**.</span><span class="sxs-lookup"><span data-stu-id="45bde-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="45bde-237">In questa procedura dettagliata, si utilizza C\#, ma è possibile utilizzare qualsiasi attività personalizzate .NET language toodevelop hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-237">In this walkthrough, you use C\#, but you can use any .NET language toodevelop hello custom activity.</span></span>
   4. <span data-ttu-id="45bde-238">Selezionare **libreria di classi** dall'elenco di hello dei tipi di progetto su hello destra.</span><span class="sxs-lookup"><span data-stu-id="45bde-238">Select **Class Library** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="45bde-239">Immettere **MyDotNetActivity** per hello **nome**.</span><span class="sxs-lookup"><span data-stu-id="45bde-239">Enter **MyDotNetActivity** for hello **Name**.</span></span>
   6. <span data-ttu-id="45bde-240">Selezionare **c:\\ADF** per hello **percorso**.</span><span class="sxs-lookup"><span data-stu-id="45bde-240">Select **C:\\ADF** for hello **Location**.</span></span> <span data-ttu-id="45bde-241">Creare la cartella hello **ADF** se non esiste.</span><span class="sxs-lookup"><span data-stu-id="45bde-241">Create hello folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="45bde-242">Fare clic su **OK** progetto hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="45bde-242">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="45bde-243">Fare clic su **strumenti**, punto troppo**Gestione pacchetti NuGet**, fare clic su **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="45bde-243">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="45bde-244">In hello **Package Manager Console**, eseguire hello successivo comando tooimport **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="45bde-244">In hello **Package Manager Console**, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="45bde-245">Hello importazione **di archiviazione di Azure** pacchetto NuGet nel progetto toohello.</span><span class="sxs-lookup"><span data-stu-id="45bde-245">Import hello **Azure Storage** NuGet package in toohello project.</span></span> <span data-ttu-id="45bde-246">Poiché si utilizza l'API di archiviazione Blob di hello in questo esempio, è necessario il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="45bde-246">You need this package because you use hello Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="45bde-247">Aggiungere il seguente hello **utilizzando** direttive toohello file sorgente hello progetto.</span><span class="sxs-lookup"><span data-stu-id="45bde-247">Add hello following **using** directives toohello source file in hello project.</span></span>

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
6. <span data-ttu-id="45bde-248">Modifica nome hello di hello **dello spazio dei nomi** troppo**MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="45bde-248">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="45bde-249">Modificare il nome di hello della classe hello troppo**MyDotNetActivity** ed eseguirne la derivazione da hello **IDotNetActivity** interfaccia come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="45bde-249">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="45bde-250">Hello implementare (Aggiungi) **Execute** metodo hello **IDotNetActivity** interfaccia toohello **MyDotNetActivity** classe e copia hello metodo toohello codice di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="45bde-250">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span> <span data-ttu-id="45bde-251">Vedere hello [metodo Execute](#execute-method) sezione per una descrizione per la logica di hello utilizzata in questo metodo.</span><span class="sxs-lookup"><span data-stu-id="45bde-251">See hello [Execute Method](#execute-method) section for explanation for hello logic used in this method.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
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
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass hello connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize hello continuation token before using it in hello do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get hello list of input blobs from hello input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns hello number of occurrences of
           // hello search term (“Microsoft”) in each blob associated
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload hello output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} toohello output blob", output);
       outputBlob.UploadText(output);
    
       // hello dictionary can be used toochain custom activities together in hello future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="45bde-252">Aggiungere hello seguente classe toohello metodi di supporto.</span><span class="sxs-lookup"><span data-stu-id="45bde-252">Add hello following helper methods toohello class.</span></span> <span data-ttu-id="45bde-253">Questi metodi vengono richiamati dal hello **Execute** metodo.</span><span class="sxs-lookup"><span data-stu-id="45bde-253">These methods are invoked by hello **Execute** method.</span></span> <span data-ttu-id="45bde-254">In particolare, hello **Calculate** metodo isola codice hello che scorre ogni oggetto blob.</span><span class="sxs-lookup"><span data-stu-id="45bde-254">Most importantly, hello **Calculate** method isolates hello code that iterates through each blob.</span></span>

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
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
    /// Gets hello fileName value from hello input/output dataset.
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
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
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
               output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    <span data-ttu-id="45bde-255">Hello **GetFolderPath** restituisce cartella toohello hello tale set di dati di prova punti tooand prova **GetFileName** metodo restituisce il nome di hello di hello/file blob che hello per i punti di set di dati.</span><span class="sxs-lookup"><span data-stu-id="45bde-255">hello **GetFolderPath** method returns hello path toohello folder that hello dataset points tooand hello **GetFileName** method returns hello name of hello blob/file that hello dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="45bde-256">Hello **Calculate** metodo calcola il numero di hello di istanze della parola chiave **Microsoft** nei file di input hello (BLOB nella cartella hello).</span><span class="sxs-lookup"><span data-stu-id="45bde-256">hello **Calculate** method calculates hello number of instances of keyword **Microsoft** in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="45bde-257">il termine di ricerca Hello ("Microsoft") è hardcoded nel codice hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-257">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>

1. <span data-ttu-id="45bde-258">Compilare il progetto hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-258">Compile hello project.</span></span> <span data-ttu-id="45bde-259">Fare clic su **compilare** menu hello e fare clic su **Compila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="45bde-259">Click **Build** from hello menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="45bde-260">Avviare **Esplora**e passare troppo**bin\\debug** o **bin\\versione** cartella in base al tipo di hello di compilazione.</span><span class="sxs-lookup"><span data-stu-id="45bde-260">Launch **Windows Explorer**, and navigate too**bin\\debug** or **bin\\release** folder depending on hello type of build.</span></span>
3. <span data-ttu-id="45bde-261">Creare un file zip **MyDotNetActivity.zip** che contiene tutti i file binari hello in hello  **\\bin\\Debug** cartella.</span><span class="sxs-lookup"><span data-stu-id="45bde-261">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello **\\bin\\Debug** folder.</span></span> <span data-ttu-id="45bde-262">È opportuno hello tooinclude MyDotNetActivity. **pdb** file in modo che sia possibile ottenere ulteriori dettagli, ad esempio il numero di riga nel codice sorgente hello che ha causato il problema di hello quando si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="45bde-262">You may want tooinclude hello MyDotNetActivity.**pdb** file so that you get additional details such as line number in hello source code that caused hello issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="45bde-263">Caricare **MyDotNetActivity.zip** come un contenitore di blob toohello blob: `customactivitycontainer` in hello Azure nell'archiviazione blob che hello **StorageLinkedService** servizio in hello collegato  **ADFTutorialDataFactory** utilizza.</span><span class="sxs-lookup"><span data-stu-id="45bde-263">Upload **MyDotNetActivity.zip** as a blob toohello blob container: `customactivitycontainer` in hello Azure blob storage that hello **StorageLinkedService** linked service in hello **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="45bde-264">Creare il contenitore di blob hello `customactivitycontainer` se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="45bde-264">Create hello blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="45bde-265">Metodo Execute</span><span class="sxs-lookup"><span data-stu-id="45bde-265">Execute method</span></span>
<span data-ttu-id="45bde-266">Questa sezione vengono fornite altre informazioni e note sul codice hello in hello metodo Execute.</span><span class="sxs-lookup"><span data-stu-id="45bde-266">This section provides more details and notes about hello code in hello Execute method.</span></span>

1. <span data-ttu-id="45bde-267">i membri di Hello per scorrere la raccolta di hello input presenti nei hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="45bde-267">hello members for iterating through hello input collection are found in hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="45bde-268">Scorrere la raccolta di blob hello richiede l'utilizzo di hello **BlobContinuationToken** classe.</span><span class="sxs-lookup"><span data-stu-id="45bde-268">Iterating through hello blob collection requires using hello **BlobContinuationToken** class.</span></span> <span data-ttu-id="45bde-269">In pratica, è necessario utilizzare un do-durante il ciclo con token hello come meccanismo di hello di uscita ciclo hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-269">In essence, you must use a do-while loop with hello token as hello mechanism for exiting hello loop.</span></span> <span data-ttu-id="45bde-270">Per ulteriori informazioni, vedere [come archiviazione di Blob da .NET toouse](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="45bde-270">For more information, see [How toouse Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="45bde-271">Di seguito è illustrato un ciclo di base:</span><span class="sxs-lookup"><span data-stu-id="45bde-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
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
   <span data-ttu-id="45bde-272">Vedere la documentazione di hello per hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) metodo per i dettagli.</span><span class="sxs-lookup"><span data-stu-id="45bde-272">See hello documentation for hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="45bde-273">Hello codice per l'utilizzo tramite set hello di BLOB logicamente passa all'interno di hello eseguire-il ciclo while.</span><span class="sxs-lookup"><span data-stu-id="45bde-273">hello code for working through hello set of blobs logically goes within hello do-while loop.</span></span> <span data-ttu-id="45bde-274">In hello **Execute** (metodo), eseguire hello-durante il ciclo passa elenco hello di BLOB metodo tooa denominato **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="45bde-274">In hello **Execute** method, hello do-while loop passes hello list of blobs tooa method named **Calculate**.</span></span> <span data-ttu-id="45bde-275">metodo Hello restituisce una variabile di stringa denominata **output** ovvero hello risultato con scorrere tutti i BLOB hello nel segmento hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-275">hello method returns a string variable named **output** that is hello result of having iterated through all hello blobs in hello segment.</span></span>

   <span data-ttu-id="45bde-276">Restituisce il numero di hello di occorrenze del termine di ricerca hello (**Microsoft**) in blob hello passato toohello **Calculate** metodo.</span><span class="sxs-lookup"><span data-stu-id="45bde-276">It returns hello number of occurrences of hello search term (**Microsoft**) in hello blob passed toohello **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="45bde-277">Una volta hello **Calculate** metodo ha eseguito operazioni di hello, deve essere scritta tooa nuovo blob.</span><span class="sxs-lookup"><span data-stu-id="45bde-277">Once hello **Calculate** method has done hello work, it must be written tooa new blob.</span></span> <span data-ttu-id="45bde-278">Pertanto, per ogni set di BLOB elaborato, un nuovo blob possono essere scritti con risultati hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-278">So for every set of blobs processed, a new blob can be written with hello results.</span></span> <span data-ttu-id="45bde-279">primo set di output di hello trova toowrite tooa nuovo blob.</span><span class="sxs-lookup"><span data-stu-id="45bde-279">toowrite tooa new blob, first find hello output dataset.</span></span>

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="45bde-280">codice di Hello viene inoltre chiamato un metodo di supporto: **GetFolderPath** percorso della cartella hello tooretrieve (nome del contenitore di archiviazione a hello).</span><span class="sxs-lookup"><span data-stu-id="45bde-280">hello code also calls a helper method: **GetFolderPath** tooretrieve hello folder path (hello storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="45bde-281">Hello **GetFolderPath** cast hello set di dati oggetto tooan AzureBlobDataSet, che include una proprietà denominata FolderPath.</span><span class="sxs-lookup"><span data-stu-id="45bde-281">hello **GetFolderPath** casts hello DataSet object tooan AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="45bde-282">hello chiamate di codice Hello **GetFileName** metodo tooretrieve hello file nome (blob).</span><span class="sxs-lookup"><span data-stu-id="45bde-282">hello code calls hello **GetFileName** method tooretrieve hello file name (blob name).</span></span> <span data-ttu-id="45bde-283">codice Hello è simile toohello sopra percorso cartella hello tooget del codice.</span><span class="sxs-lookup"><span data-stu-id="45bde-283">hello code is similar toohello above code tooget hello folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="45bde-284">nome di Hello del file hello viene scritta tramite la creazione di un oggetto URI.</span><span class="sxs-lookup"><span data-stu-id="45bde-284">hello name of hello file is written by creating a URI object.</span></span> <span data-ttu-id="45bde-285">costruttore URI Hello utilizza hello **BlobEndpoint** nome del contenitore di proprietà tooreturn hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-285">hello URI constructor uses hello **BlobEndpoint** property tooreturn hello container name.</span></span> <span data-ttu-id="45bde-286">nome file e percorso della cartella Hello vengono aggiunti tooconstruct hello output URI del blob.</span><span class="sxs-lookup"><span data-stu-id="45bde-286">hello folder path and file name are added tooconstruct hello output blob URI.</span></span>  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="45bde-287">nome di Hello del file hello è stato scritto e ora è possibile scrivere una stringa di output di hello da hello **Calculate** nuovo blob di metodo tooa:</span><span class="sxs-lookup"><span data-stu-id="45bde-287">hello name of hello file has been written and now you can write hello output string from hello **Calculate** method tooa new blob:</span></span>

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a><span data-ttu-id="45bde-288">Creare hello data factory</span><span class="sxs-lookup"><span data-stu-id="45bde-288">Create hello data factory</span></span>
<span data-ttu-id="45bde-289">In hello [creare attività personalizzata hello](#create-the-custom-activity) sezione creata un'attività personalizzata e il file zip hello caricato con i file binari e hello PDB file tooan contenitore blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="45bde-289">In hello [Create hello custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded hello zip file with binaries and hello PDB file tooan Azure blob container.</span></span> <span data-ttu-id="45bde-290">In questa sezione si crea un Azure **data factory di** con un **pipeline** che utilizza hello **attività personalizzata**.</span><span class="sxs-lookup"><span data-stu-id="45bde-290">In this section, you create an Azure **data factory** with a **pipeline** that uses hello **custom activity**.</span></span>

<span data-ttu-id="45bde-291">Hello input set di dati per l'attività personalizzata hello rappresenta BLOB hello (file) nella cartella input hello (`mycontainer\\inputfolder`) nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="45bde-291">hello input dataset for hello custom activity represents hello blobs (files) in hello input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="45bde-292">Hello set di dati di output per attività hello rappresenta BLOB di output di hello nella cartella di output di hello (`mycontainer\\outputfolder`) nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="45bde-292">hello output dataset for hello activity represents hello output blobs in hello output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="45bde-293">Eliminare uno o più file nelle cartelle di input hello:</span><span class="sxs-lookup"><span data-stu-id="45bde-293">Drop one or more files in hello input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="45bde-294">Ad esempio, è possibile eliminare un file (file. txt) con hello dopo contenuto in ciascuna delle cartelle hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-294">For example, drop one file (file.txt) with hello following content into each of hello folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="45bde-295">Ogni cartella di input corrisponde sezione tooa nella Data Factory di Azure, anche se la cartella hello è 2 o più file.</span><span class="sxs-lookup"><span data-stu-id="45bde-295">Each input folder corresponds tooa slice in Azure Data Factory even if hello folder has 2 or more files.</span></span> <span data-ttu-id="45bde-296">Quando ogni sezione venga elaborato dalla pipeline di hello, attività personalizzata hello scorre tutti i BLOB hello nella cartella di input hello per tale sezione.</span><span class="sxs-lookup"><span data-stu-id="45bde-296">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="45bde-297">Vedrai cinque dei file di output con hello stesso contenuto.</span><span class="sxs-lookup"><span data-stu-id="45bde-297">You see five output files with hello same content.</span></span> <span data-ttu-id="45bde-298">Ad esempio, file di output di hello di elaborazione del file nella cartella hello 2015-11-16-00 hello è hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="45bde-298">For example, hello output file from processing hello file in hello 2015-11-16-00 folder has hello following content:</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="45bde-299">Se si elimina più file (file. txt, file2.txt, file3.txt) con hello stesso contenuto toohello cartella di input, viene visualizzato dopo contenuto nel file di output di hello hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with hello same content toohello input folder, you see hello following content in hello output file.</span></span> <span data-ttu-id="45bde-300">Ogni cartella (2015-11-16-00, e così via) corrispondente sezione tooa in questo esempio, anche se la cartella hello dispone di più file di input.</span><span class="sxs-lookup"><span data-stu-id="45bde-300">Each folder (2015-11-16-00, etc.) corresponds tooa slice in this sample even though hello folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="45bde-301">file di output di Hello con tre righe a questo punto, uno per ogni file di input (blob) nella cartella hello associata a una sezione hello (2015-11-16-00).</span><span class="sxs-lookup"><span data-stu-id="45bde-301">hello output file has three lines now, one for each input file (blob) in hello folder associated with hello slice (2015-11-16-00).</span></span>

<span data-ttu-id="45bde-302">Per ogni esecuzione di attività viene creata un'attività.</span><span class="sxs-lookup"><span data-stu-id="45bde-302">A task is created for each activity run.</span></span> <span data-ttu-id="45bde-303">In questo esempio, è presente una sola attività nella pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-303">In this sample, there is only one activity in hello pipeline.</span></span> <span data-ttu-id="45bde-304">Quando una sezione venga elaborata dalla pipeline di hello, nella sezione di Azure Batch tooprocess hello viene eseguita l'attività personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-304">When a slice is processed by hello pipeline, hello custom activity runs on Azure Batch tooprocess hello slice.</span></span> <span data-ttu-id="45bde-305">Poiché ci sono cinque sezioni, e ogni sezione può contenere più BLOB o file, in Azure Batch vengono create cinque attività.</span><span class="sxs-lookup"><span data-stu-id="45bde-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="45bde-306">Quando un'attività viene eseguita in Batch, è effettivamente hello attività personalizzata che è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="45bde-306">When a task runs on Batch, it is actually hello custom activity that is running.</span></span>

<span data-ttu-id="45bde-307">Hello seguendo questa procedura dettagliata fornisce dettagli aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="45bde-307">hello following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="45bde-308">Passaggio 1: Creare hello data factory</span><span class="sxs-lookup"><span data-stu-id="45bde-308">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="45bde-309">Dopo l'accesso toohello [portale di Azure](https://portal.azure.com/), hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="45bde-309">After logging in toohello [Azure portal](https://portal.azure.com/), do hello following steps:</span></span>

   1. <span data-ttu-id="45bde-310">Fare clic su **NEW** nel menu di sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-310">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="45bde-311">Fare clic su **dati + Analitica** in hello **New** blade.</span><span class="sxs-lookup"><span data-stu-id="45bde-311">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="45bde-312">Fare clic su **Data Factory** su hello **analitica dati** blade.</span><span class="sxs-lookup"><span data-stu-id="45bde-312">Click **Data Factory** on hello **Data analytics** blade.</span></span>
2. <span data-ttu-id="45bde-313">In hello **nuova data factory** pannello immettere **CustomActivityFactory** per hello Name.</span><span class="sxs-lookup"><span data-stu-id="45bde-313">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="45bde-314">nome Hello di hello Azure data factory deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="45bde-314">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="45bde-315">Se viene visualizzato l'errore hello: **"CustomActivityFactory" nome della Data factory non è disponibile**, modificare il nome di hello della data factory di hello (ad esempio, **yournameCustomActivityFactory**) e provare a creare nuovo.</span><span class="sxs-lookup"><span data-stu-id="45bde-315">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="45bde-316">Fare clic su **NOME DEL GRUPPO DI RISORSE**e selezionare un gruppo di risorse esistente o crearne uno.</span><span class="sxs-lookup"><span data-stu-id="45bde-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="45bde-317">Verificare che la sottoscrizione corretta hello e regione in cui si desidera hello data factory toobe creato in uso.</span><span class="sxs-lookup"><span data-stu-id="45bde-317">Verify that you are using hello correct subscription and region where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="45bde-318">Fare clic su **crea** su hello **nuova data factory** blade.</span><span class="sxs-lookup"><span data-stu-id="45bde-318">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="45bde-319">Vedrai data factory di hello viene creato nel hello **Dashboard** di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="45bde-319">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="45bde-320">Dopo aver hello data factory è stata creata correttamente, vedrai hello data factory pagina nella quale viene hello contenuto di data factory di hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-320">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="45bde-321">Passaggio 2: Creare servizi collegati</span><span class="sxs-lookup"><span data-stu-id="45bde-321">Step 2: Create linked services</span></span>
<span data-ttu-id="45bde-322">Servizi collegati collegano archivi dati o servizi tooan data factory di Azure di calcolo.</span><span class="sxs-lookup"><span data-stu-id="45bde-322">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="45bde-323">In questo passaggio si collega il **di archiviazione di Azure** account e **Azure Batch** tooyour data factory di account.</span><span class="sxs-lookup"><span data-stu-id="45bde-323">In this step, you link your **Azure Storage** account and **Azure Batch** account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="45bde-324">Creare il servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="45bde-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="45bde-325">Fare clic su hello **autore e distribuire** riquadro hello **DATA FACTORY** pannello **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="45bde-325">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="45bde-326">Vedrai hello Editor delle Data Factory.</span><span class="sxs-lookup"><span data-stu-id="45bde-326">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="45bde-327">Fare clic su **nuovo archivio dati** hello barra dei comandi e scegliere **archiviazione di Azure.**</span><span class="sxs-lookup"><span data-stu-id="45bde-327">Click **New data store** on hello command bar and choose **Azure storage.**</span></span> <span data-ttu-id="45bde-328">Dovrebbe essere hello script JSON per la creazione di una risorsa di archiviazione di Azure il servizio nell'editor di hello collegato.</span><span class="sxs-lookup"><span data-stu-id="45bde-328">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="45bde-329">Sostituire **nome account** con nome hello dell'account di archiviazione di Azure e **chiave dell'account** con la chiave di accesso hello di hello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="45bde-329">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="45bde-330">toolearn modalità di accesso di archiviazione di tooget chiave, vedere [visualizzazione, copia e l'archiviazione di rigenerare le chiavi di accesso](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="45bde-330">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="45bde-331">Fare clic su **Distribuisci** sul comando hello barra toodeploy hello collegato servizio.</span><span class="sxs-lookup"><span data-stu-id="45bde-331">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="45bde-332">Creare il servizio collegato Azure Batch</span><span class="sxs-lookup"><span data-stu-id="45bde-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="45bde-333">In questo passaggio si crea un servizio collegato per il **Azure Batch** account attività personalizzata utilizzata toorun hello Data Factory.</span><span class="sxs-lookup"><span data-stu-id="45bde-333">In this step, you create a linked service for your **Azure Batch** account that is used toorun hello Data Factory custom activity.</span></span>

1. <span data-ttu-id="45bde-334">Fare clic su **nuovo calcolo** hello barra dei comandi e scegliere **Azure Batch.**</span><span class="sxs-lookup"><span data-stu-id="45bde-334">Click **New compute** on hello command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="45bde-335">Dovrebbe essere hello script JSON per la creazione di un Batch di Azure il servizio nell'editor di hello collegato.</span><span class="sxs-lookup"><span data-stu-id="45bde-335">You should see hello JSON script for creating an Azure Batch linked service in hello editor.</span></span>
2. <span data-ttu-id="45bde-336">In hello script JSON:</span><span class="sxs-lookup"><span data-stu-id="45bde-336">In hello JSON script:</span></span>

   1. <span data-ttu-id="45bde-337">Sostituire **nome account** con nome hello dell'account di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="45bde-337">Replace **account name** with hello name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="45bde-338">Sostituire **chiave di accesso** con la chiave di accesso hello di hello account Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="45bde-338">Replace **access key** with hello access key of hello Azure Batch account.</span></span>
   3. <span data-ttu-id="45bde-339">Immettere l'ID di hello del pool di hello per hello **poolName** proprietà**.**</span><span class="sxs-lookup"><span data-stu-id="45bde-339">Enter hello ID of hello pool for hello **poolName** property**.**</span></span> <span data-ttu-id="45bde-340">Per questa proprietà è possibile specificare il nome del pool o del pool di ID.</span><span class="sxs-lookup"><span data-stu-id="45bde-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="45bde-341">Immettere il batch di hello URI per hello **batchUri** proprietà JSON.</span><span class="sxs-lookup"><span data-stu-id="45bde-341">Enter hello batch URI for hello **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="45bde-342">Hello **URL** da hello **pannello account Azure Batch** in hello seguente formato: \<accountname\>.\< area\>. batch.azure.com. Per hello **batchUri** proprietà hello JSON, è necessario troppo**rimuovere "accountname".**</span><span class="sxs-lookup"><span data-stu-id="45bde-342">hello **URL** from hello **Azure Batch account blade** is in hello following format: \<accountname\>.\<region\>.batch.azure.com. For hello **batchUri** property in hello JSON, you need too**remove "accountname."**</span></span> <span data-ttu-id="45bde-343">dall'URL hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-343">from hello URL.</span></span> <span data-ttu-id="45bde-344">Esempio: `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="45bde-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="45bde-345">Per hello **poolName** proprietà, è inoltre possibile specificare l'ID di hello del pool di hello anziché il nome di hello del pool di hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-345">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="45bde-346">Hello servizio Data Factory non supporta un'opzione su richiesta per il Batch di Azure a quanto accade per HDInsight.</span><span class="sxs-lookup"><span data-stu-id="45bde-346">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="45bde-347">È possibile usare solo il proprio pool di Batch di Azure in una data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="45bde-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="45bde-348">Specificare **StorageLinkedService** per hello **linkedServiceName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="45bde-348">Specify **StorageLinkedService** for hello **linkedServiceName** property.</span></span> <span data-ttu-id="45bde-349">Il servizio collegato creato nel passaggio precedente di hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-349">You created this linked service in hello previous step.</span></span> <span data-ttu-id="45bde-350">Questo servizio di archiviazione viene usato come area di staging per file e log.</span><span class="sxs-lookup"><span data-stu-id="45bde-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="45bde-351">Fare clic su **Distribuisci** sul comando hello barra toodeploy hello collegato servizio.</span><span class="sxs-lookup"><span data-stu-id="45bde-351">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="45bde-352">Passaggio 3: Creare set di dati</span><span class="sxs-lookup"><span data-stu-id="45bde-352">Step 3: Create datasets</span></span>
<span data-ttu-id="45bde-353">In questo passaggio, creare set di dati toorepresent input e i dati di output.</span><span class="sxs-lookup"><span data-stu-id="45bde-353">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="45bde-354">Creare set di dati di input</span><span class="sxs-lookup"><span data-stu-id="45bde-354">Create input dataset</span></span>
1. <span data-ttu-id="45bde-355">In hello **Editor** per hello Data Factory, fare clic su **nuovo set di dati** pulsante sulla barra degli strumenti hello e fare clic su **archiviazione Blob di Azure** dal menu a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-355">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="45bde-356">Sostituire hello JSON nel riquadro di destra hello con hello frammento di codice JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="45bde-356">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

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

    <span data-ttu-id="45bde-357">Più avanti in questa procedura dettagliata viene creata una pipeline con ora di inizio: 2015-11-16T00:00:00Z e ora di fine: 2015-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="45bde-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="45bde-358">Si tratta di dati pianificati tooproduce **oraria**, pertanto vi sono 5 sezioni di input/output (tra **00**: 00:00 -\> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="45bde-358">It is scheduled tooproduce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="45bde-359">Hello **frequenza** e **intervallo** per hello di un set di dati dell'input è troppo**ora** e **1**, il che significa che hello input sezione è disponibile ogni ora.</span><span class="sxs-lookup"><span data-stu-id="45bde-359">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span>

    <span data-ttu-id="45bde-360">Di seguito sono ora di inizio di hello per ogni sezione, rappresentato da **SliceStart** variabile di sistema in hello sopra il frammento JSON.</span><span class="sxs-lookup"><span data-stu-id="45bde-360">Here are hello start times for each slice, which is represented by **SliceStart** system variable in hello above JSON snippet.</span></span>

    | <span data-ttu-id="45bde-361">**Sezione**</span><span class="sxs-lookup"><span data-stu-id="45bde-361">**Slice**</span></span> | <span data-ttu-id="45bde-362">**Ora di inizio**</span><span class="sxs-lookup"><span data-stu-id="45bde-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="45bde-363">1</span><span class="sxs-lookup"><span data-stu-id="45bde-363">1</span></span>         | <span data-ttu-id="45bde-364">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="45bde-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="45bde-365">2</span><span class="sxs-lookup"><span data-stu-id="45bde-365">2</span></span>         | <span data-ttu-id="45bde-366">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="45bde-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="45bde-367">3</span><span class="sxs-lookup"><span data-stu-id="45bde-367">3</span></span>         | <span data-ttu-id="45bde-368">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="45bde-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="45bde-369">4</span><span class="sxs-lookup"><span data-stu-id="45bde-369">4</span></span>         | <span data-ttu-id="45bde-370">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="45bde-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="45bde-371">5</span><span class="sxs-lookup"><span data-stu-id="45bde-371">5</span></span>         | <span data-ttu-id="45bde-372">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="45bde-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="45bde-373">Hello **folderPath** viene calcolato utilizzando hello di anno, mese, giorno e ora parte dell'ora di inizio sezione hello (**SliceStart**).</span><span class="sxs-lookup"><span data-stu-id="45bde-373">hello **folderPath** is calculated by using hello year, month, day, and hour part of hello slice start time (**SliceStart**).</span></span> <span data-ttu-id="45bde-374">Di conseguenza, ecco come una cartella di input è l'intervallo di tooa mappato.</span><span class="sxs-lookup"><span data-stu-id="45bde-374">Therefore, here is how an input folder is mapped tooa slice.</span></span>

    | <span data-ttu-id="45bde-375">**Sezione**</span><span class="sxs-lookup"><span data-stu-id="45bde-375">**Slice**</span></span> | <span data-ttu-id="45bde-376">**Ora di inizio**</span><span class="sxs-lookup"><span data-stu-id="45bde-376">**Start time**</span></span>          | <span data-ttu-id="45bde-377">**Cartella di input**</span><span class="sxs-lookup"><span data-stu-id="45bde-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="45bde-378">1</span><span class="sxs-lookup"><span data-stu-id="45bde-378">1</span></span>         | <span data-ttu-id="45bde-379">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="45bde-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="45bde-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="45bde-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="45bde-381">2</span><span class="sxs-lookup"><span data-stu-id="45bde-381">2</span></span>         | <span data-ttu-id="45bde-382">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="45bde-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="45bde-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="45bde-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="45bde-384">3</span><span class="sxs-lookup"><span data-stu-id="45bde-384">3</span></span>         | <span data-ttu-id="45bde-385">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="45bde-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="45bde-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="45bde-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="45bde-387">4</span><span class="sxs-lookup"><span data-stu-id="45bde-387">4</span></span>         | <span data-ttu-id="45bde-388">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="45bde-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="45bde-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="45bde-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="45bde-390">5</span><span class="sxs-lookup"><span data-stu-id="45bde-390">5</span></span>         | <span data-ttu-id="45bde-391">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="45bde-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="45bde-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="45bde-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="45bde-393">Fare clic su **Distribuisci** hello toocreate barra degli strumenti e distribuire hello **InputDataset** tabella.</span><span class="sxs-lookup"><span data-stu-id="45bde-393">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="45bde-394">Creare il set di dati di output</span><span class="sxs-lookup"><span data-stu-id="45bde-394">Create output dataset</span></span>
<span data-ttu-id="45bde-395">In questo passaggio si crea un altro set di dati di tipo di dati di output di hello toorepresent AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="45bde-395">In this step, you create another dataset of type AzureBlob toorepresent hello output data.</span></span>

1. <span data-ttu-id="45bde-396">In hello **Editor** per hello Data Factory, fare clic su **nuovo set di dati** pulsante sulla barra degli strumenti hello e fare clic su **archiviazione Blob di Azure** dal menu a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-396">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="45bde-397">Sostituire hello JSON nel riquadro di destra hello con hello frammento di codice JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="45bde-397">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

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

    <span data-ttu-id="45bde-398">Un BLOB o file di output viene generato per ogni sezione di input.</span><span class="sxs-lookup"><span data-stu-id="45bde-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="45bde-399">Ecco come viene denominato il file di output per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="45bde-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="45bde-400">Tutti i file di output di hello vengono generati in una cartella di output: `mycontainer\\outputfolder`.</span><span class="sxs-lookup"><span data-stu-id="45bde-400">All hello output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="45bde-401">**Sezione**</span><span class="sxs-lookup"><span data-stu-id="45bde-401">**Slice**</span></span> | <span data-ttu-id="45bde-402">**Ora di inizio**</span><span class="sxs-lookup"><span data-stu-id="45bde-402">**Start time**</span></span>          | <span data-ttu-id="45bde-403">**File di output**</span><span class="sxs-lookup"><span data-stu-id="45bde-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="45bde-404">1</span><span class="sxs-lookup"><span data-stu-id="45bde-404">1</span></span>         | <span data-ttu-id="45bde-405">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="45bde-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="45bde-406">2015-11-16-**00.txt**</span><span class="sxs-lookup"><span data-stu-id="45bde-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="45bde-407">2</span><span class="sxs-lookup"><span data-stu-id="45bde-407">2</span></span>         | <span data-ttu-id="45bde-408">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="45bde-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="45bde-409">2015-11-16-**01.txt**</span><span class="sxs-lookup"><span data-stu-id="45bde-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="45bde-410">3</span><span class="sxs-lookup"><span data-stu-id="45bde-410">3</span></span>         | <span data-ttu-id="45bde-411">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="45bde-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="45bde-412">2015-11-16-**02.txt**</span><span class="sxs-lookup"><span data-stu-id="45bde-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="45bde-413">4</span><span class="sxs-lookup"><span data-stu-id="45bde-413">4</span></span>         | <span data-ttu-id="45bde-414">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="45bde-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="45bde-415">2015-11-16-**03.txt**</span><span class="sxs-lookup"><span data-stu-id="45bde-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="45bde-416">5</span><span class="sxs-lookup"><span data-stu-id="45bde-416">5</span></span>         | <span data-ttu-id="45bde-417">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="45bde-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="45bde-418">2015-11-16-**04.txt**</span><span class="sxs-lookup"><span data-stu-id="45bde-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="45bde-419">Tenere presente che tutti i file in una cartella di input di hello (ad esempio: 2015-11-16-00) fanno parte di una sezione con ora di inizio hello: 2015-11-16-00.</span><span class="sxs-lookup"><span data-stu-id="45bde-419">Remember that all hello files in an input folder (for example: 2015-11-16-00) are part of a slice with hello start time: 2015-11-16-00.</span></span> <span data-ttu-id="45bde-420">Durante l'elaborazione di questa sezione, attività personalizzata hello esamina ogni file e produce una riga nel file di output di hello con numero di hello di occorrenze del termine di ricerca ("Microsoft").</span><span class="sxs-lookup"><span data-stu-id="45bde-420">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="45bde-421">Se sono presenti tre file nella cartella hello 2015-11-16-00, sono presenti tre righe nel file di output di hello: 2015-11-16-00.txt.</span><span class="sxs-lookup"><span data-stu-id="45bde-421">If there are three files in hello folder 2015-11-16-00, there are three lines in hello output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="45bde-422">Fare clic su **Distribuisci** hello toocreate barra degli strumenti e distribuire hello **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="45bde-422">Click **Deploy** on hello toolbar toocreate and deploy hello **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a><span data-ttu-id="45bde-423">Passaggio 4: Creare ed eseguire pipeline hello con attività personalizzata</span><span class="sxs-lookup"><span data-stu-id="45bde-423">Step 4: Create and run hello pipeline with custom activity</span></span>
<span data-ttu-id="45bde-424">In questo passaggio creare una pipeline con un'attività, attività personalizzata hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="45bde-424">In this step, you create a pipeline with one activity, hello custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45bde-425">Se si non sono stati caricati hello **file.txt** tooinput cartelle nel contenitore blob hello, eseguire questa operazione prima di creare pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-425">If you haven't uploaded hello **file.txt** tooinput folders in hello blob container, do so before creating hello pipeline.</span></span> <span data-ttu-id="45bde-426">Hello **isPaused** proprietà è impostata toofalse nella pipeline hello JSON, pertanto viene eseguita immediatamente pipeline hello come hello **avviare** la data è hello precedente.</span><span class="sxs-lookup"><span data-stu-id="45bde-426">hello **isPaused** property is set toofalse in hello pipeline JSON, so hello pipeline runs immediately as hello **start** date is in hello past.</span></span>
>
>

1. <span data-ttu-id="45bde-427">Nell'Editor delle Data Factory hello, fare clic su **nuova pipeline** hello barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="45bde-427">In hello Data Factory Editor, click **New pipeline** on hello command bar.</span></span> <span data-ttu-id="45bde-428">Se il comando hello non viene visualizzata, fare clic su **... (Puntini di sospensione)**  toosee è.</span><span class="sxs-lookup"><span data-stu-id="45bde-428">If you do not see hello command, click **... (Ellipsis)** toosee it.</span></span>
2. <span data-ttu-id="45bde-429">Sostituire hello JSON nel riquadro di destra hello con hello lo script JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="45bde-429">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

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
   <span data-ttu-id="45bde-430">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="45bde-430">Note hello following points:</span></span>

   * <span data-ttu-id="45bde-431">È presente una sola attività nella pipeline hello e che è di tipo: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="45bde-431">There is only one activity in hello pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="45bde-432">**AssemblyName** è impostato il nome toohello di hello DLL: **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="45bde-432">**AssemblyName** is set toohello name of hello DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="45bde-433">**Punto di ingresso** è troppo**MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="45bde-433">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="45bde-434">Si tratta in sostanza di \<spazio dei nomi\>.\<nome classe\> nel codice.</span><span class="sxs-lookup"><span data-stu-id="45bde-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="45bde-435">**PackageLinkedService** è troppo**StorageLinkedService** che punta toohello archiviazione di blob che contiene i file zip di attività personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-435">**PackageLinkedService** is set too**StorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="45bde-436">Se si utilizza diversi account di archiviazione di Azure per i file di input/output e i file zip di attività personalizzata hello, è necessario toocreate un altro servizio di archiviazione Azure il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="45bde-436">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you have toocreate another Azure Storage linked service.</span></span> <span data-ttu-id="45bde-437">Questo articolo si presuppone che si sta utilizzando hello stesso account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="45bde-437">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="45bde-438">**PackageFile** è troppo**customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="45bde-438">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="45bde-439">È in formato hello: \<containerforthezip\>/\<nameofthezip.zip\>.</span><span class="sxs-lookup"><span data-stu-id="45bde-439">It is in hello format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="45bde-440">attività personalizzata Hello accetta **InputDataset** come input e **OutputDataset** come output.</span><span class="sxs-lookup"><span data-stu-id="45bde-440">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="45bde-441">Hello **linkedServiceName** proprietà dell'attività personalizzata hello punta toohello **AzureBatchLinkedService**, che indica Data Factory di Azure, tale attività personalizzata hello deve toorun nel Batch di Azure.</span><span class="sxs-lookup"><span data-stu-id="45bde-441">hello **linkedServiceName** property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch.</span></span>
   * <span data-ttu-id="45bde-442">Hello **concorrenza** impostazione è importante.</span><span class="sxs-lookup"><span data-stu-id="45bde-442">hello **concurrency** setting is important.</span></span> <span data-ttu-id="45bde-443">Se si utilizza il valore predefinito hello, ovvero 1, anche se si dispone di 2 o più nodi di calcolo nel pool di Azure Batch hello, sezioni hello vengono elaborate una dopo l'altra.</span><span class="sxs-lookup"><span data-stu-id="45bde-443">If you use hello default value, which is 1, even if you have 2 or more compute nodes in hello Azure Batch pool, hello slices are processed one after another.</span></span> <span data-ttu-id="45bde-444">Pertanto, non si potrà usufruire della funzionalità di elaborazione parallela hello di Batch di Azure.</span><span class="sxs-lookup"><span data-stu-id="45bde-444">Therefore, you are not taking advantage of hello parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="45bde-445">Se si imposta **concorrenza** tooa più alto valore, ad esempio 2, significa che due sezioni (corrisponde tootwo operazioni in Batch di Azure) possono essere elaborate in hello stesso tempo, in questo caso, entrambe le macchine virtuali di hello in hello Azure Batch vengono utilizzati pool.</span><span class="sxs-lookup"><span data-stu-id="45bde-445">If you set **concurrency** tooa higher value, say 2, it means that two slices (corresponds tootwo tasks in Azure Batch) can be processed at hello same time, in which case, both hello VMs in hello Azure Batch pool are utilized.</span></span> <span data-ttu-id="45bde-446">Pertanto, impostare proprietà di concorrenza hello in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="45bde-446">Therefore, set hello concurrency property appropriately.</span></span>
   * <span data-ttu-id="45bde-447">Per impostazione predefinita, viene eseguita solo un'attività (sezione) in una VM in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="45bde-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="45bde-448">Hello motivo è che, per impostazione predefinita, hello **massimo attività per ogni macchina virtuale** è impostato too1 per un pool di Batch di Azure.</span><span class="sxs-lookup"><span data-stu-id="45bde-448">hello reason is that, by default, hello **Maximum tasks per VM** is set too1 for an Azure Batch pool.</span></span> <span data-ttu-id="45bde-449">Come parte dei prerequisiti, è stato creato un pool con too2 questo set di proprietà, in modo da due intervalli di Data Factory possono essere eseguito su una macchina virtuale in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="45bde-449">As part of prerequisites, you created a pool with this property set too2, so two Data Factory slices can be running on a VM at hello same time.</span></span>

    -   <span data-ttu-id="45bde-450">**isPaused** proprietà è impostata toofalse per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="45bde-450">**isPaused** property is set toofalse by default.</span></span> <span data-ttu-id="45bde-451">pipeline Hello verrà eseguito immediatamente in questo esempio perché l'inizio delle sezioni hello in hello precedente.</span><span class="sxs-lookup"><span data-stu-id="45bde-451">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="45bde-452">È possibile impostare la pipeline di hello toopause tootrue proprietà e impostarla toorestart toofalse indietro.</span><span class="sxs-lookup"><span data-stu-id="45bde-452">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>

    -   <span data-ttu-id="45bde-453">Hello **avviare** tempo e **fine** tempi sono distanza di cinque ore e le sezioni vengono generate ogni ora, in modo da cinque sezioni vengono generate dalla pipeline di hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-453">hello **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>

1. <span data-ttu-id="45bde-454">Fare clic su **Distribuisci** sul comando hello barra pipeline hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="45bde-454">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span>

#### <a name="step-5-test-hello-pipeline"></a><span data-ttu-id="45bde-455">Passaggio 5: Testare la pipeline hello</span><span class="sxs-lookup"><span data-stu-id="45bde-455">Step 5: Test hello pipeline</span></span>
<span data-ttu-id="45bde-456">In questo passaggio si verifica pipeline hello eliminazione file nelle cartelle di input hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-456">In this step, you test hello pipeline by dropping files into hello input folders.</span></span> <span data-ttu-id="45bde-457">Iniziamo con pipeline hello test con un file per una cartella di input.</span><span class="sxs-lookup"><span data-stu-id="45bde-457">Let’s start with testing hello pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="45bde-458">Nel Pannello di Data Factory hello in hello portale di Azure, fare clic su **diagramma**.</span><span class="sxs-lookup"><span data-stu-id="45bde-458">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="45bde-459">Nella vista diagramma hello, fare doppio clic sul set di dati input: **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="45bde-459">In hello diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="45bde-460">Dovrebbe essere hello **InputDataset** pannello con tutti e cinque sezioni pronto.</span><span class="sxs-lookup"><span data-stu-id="45bde-460">You should see hello **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="45bde-461">Hello preavviso **ora di inizio sezione** e **ora di fine sezione** per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="45bde-461">Notice hello **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="45bde-462">In hello **vista diagramma**, fare clic su **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="45bde-462">In hello **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="45bde-463">Dovrebbe essere che le sezioni di output cinque hello sono nello stato Ready hello se sono già stati elaborati.</span><span class="sxs-lookup"><span data-stu-id="45bde-463">You should see that hello five output slices are in hello Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="45bde-464">Hello tooview portale Azure usare **attività** associato hello **sezioni** e vedere quali macchine Virtuali di ogni sezione è stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="45bde-464">Use Azure portal tooview hello **tasks** associated with hello **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="45bde-465">Per altre informazioni, vedere la sezione [Integrazione di Data Factory e Batch](#data-factory-and-batch-integration) .</span><span class="sxs-lookup"><span data-stu-id="45bde-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="45bde-466">Si noterà che i file di output di hello in hello `outputfolder` di `mycontainer` nell'archiviazione di Azure blob.</span><span class="sxs-lookup"><span data-stu-id="45bde-466">You should see hello output files in hello `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="45bde-467">Saranno presenti cinque file di output, uno per ogni sezione di input.</span><span class="sxs-lookup"><span data-stu-id="45bde-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="45bde-468">Ognuno di hello l'output del file deve essere contenuto toohello simile seguente output:</span><span class="sxs-lookup"><span data-stu-id="45bde-468">Each of hello output file should have content similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="45bde-469">Hello diagramma seguente illustra il mapping tra sezioni Data Factory hello tootasks in Batch di Azure.</span><span class="sxs-lookup"><span data-stu-id="45bde-469">hello following diagram illustrates how hello Data Factory slices map tootasks in Azure Batch.</span></span> <span data-ttu-id="45bde-470">In questo esempio a una sezione è associata una sola esecuzione.</span><span class="sxs-lookup"><span data-stu-id="45bde-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="45bde-471">Si proverà ora con più file in una cartella.</span><span class="sxs-lookup"><span data-stu-id="45bde-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="45bde-472">Creazione di file: **file2.txt**, **file3.txt**, **file4.txt**, e **file5.txt** con hello stesso contenuto come file. txt nella cartella hello: **2015-11-06-01**.</span><span class="sxs-lookup"><span data-stu-id="45bde-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with hello same content as in file.txt in hello folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="45bde-473">Nella cartella di output di hello, **eliminare** file di output di hello: **2015-11-16-01.txt**.</span><span class="sxs-lookup"><span data-stu-id="45bde-473">In hello output folder, **delete** hello output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="45bde-474">A questo punto, in hello **OutputDataset** blade, sezione hello pulsante destro del mouse con **ora di inizio sezione** impostare troppo**16/11/2015 01:00:00 AM**, fare clic su **eseguire**sezione hello toorerun/rinviati-process.</span><span class="sxs-lookup"><span data-stu-id="45bde-474">Now, in hello **OutputDataset** blade, right-click hello slice with **SLICE START TIME** set too**11/16/2015 01:00:00 AM**, and click **Run** toorerun/re-process hello slice.</span></span> <span data-ttu-id="45bde-475">A questo punto, sezione hello ha cinque file anziché un file.</span><span class="sxs-lookup"><span data-stu-id="45bde-475">Now, hello slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="45bde-476">Dopo l'esecuzione di sezione hello e il suo stato sia **pronto**, verificare il contenuto di hello nel file di output di hello per questa sezione (**2015-11-16-01.txt**) in hello `outputfolder` di `mycontainer` nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="45bde-476">After hello slice runs and its status is **Ready**, verify hello content in hello output file for this slice (**2015-11-16-01.txt**) in hello `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="45bde-477">Deve essere presente una riga per ogni file della sezione hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-477">There should be a line for each file of hello slice.</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="45bde-478">Se non è stato eliminato hello output file 2015-11-16-01.txt prima di tentare con cinque file di input, viene visualizzata una riga da eseguire la sezione precedente hello e cinque righe dall'intervallo corrente di hello eseguire.</span><span class="sxs-lookup"><span data-stu-id="45bde-478">If you did not delete hello output file 2015-11-16-01.txt before trying with five input files, you see one line from hello previous slice run and five lines from hello current slice run.</span></span> <span data-ttu-id="45bde-479">Per impostazione predefinita, il contenuto di hello è accodato toooutput file se esiste già.</span><span class="sxs-lookup"><span data-stu-id="45bde-479">By default, hello content is appended toooutput file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="45bde-480">Integrazione di Data Factory e Batch</span><span class="sxs-lookup"><span data-stu-id="45bde-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="45bde-481">Hello servizio Data Factory crea un processo in Batch di Azure con nome hello: `adf-poolname:job-xxx`.</span><span class="sxs-lookup"><span data-stu-id="45bde-481">hello Data Factory service creates a job in Azure Batch with hello name: `adf-poolname:job-xxx`.</span></span>

![Azure Data Factory: processi di Batch](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="45bde-483">Per ogni esecuzione di attività di una sezione viene creata un'attività nel processo di hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-483">A task in hello job is created for each activity run of a slice.</span></span> <span data-ttu-id="45bde-484">Se sono presenti toobe pronto 10 sezioni elaborate, vengono create 10 attività nel processo di hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-484">If there are 10 slices ready toobe processed, 10 tasks are created in hello job.</span></span> <span data-ttu-id="45bde-485">È possibile avere più di una sezione in esecuzione in parallelo, se si dispone di più nodi di calcolo nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-485">You can have more than one slice running in parallel if you have multiple compute nodes in hello pool.</span></span> <span data-ttu-id="45bde-486">Se del numero massimo di attività hello per calcola i set di nodi sono troppo > 1, possono essere presenti più di una sezione in esecuzione su hello calcolo stesso.</span><span class="sxs-lookup"><span data-stu-id="45bde-486">If hello maximum tasks per compute node is set too> 1, there can be more than one slice running on hello same compute.</span></span>

<span data-ttu-id="45bde-487">In questo esempio ci sono cinque sezioni, quindi cinque attività in Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="45bde-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="45bde-488">Con hello **concorrenza** impostare troppo**5** in hello pipeline JSON in Azure Data Factory e **massimo attività per ogni macchina virtuale** impostare troppo**2** in Batch di Azure pool di applicazioni con **2** le macchine virtuali, hello attività esecuzione veloce (ora di inizio e fine per le attività di controllo).</span><span class="sxs-lookup"><span data-stu-id="45bde-488">With hello **concurrency** set too**5** in hello pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set too**2** in Azure Batch pool with **2** VMs, hello tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="45bde-489">Utilizzare procedura batch hello tooview portale hello e le relative attività associate a hello **sezioni** e vedere quali macchine Virtuali di ogni sezione è stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="45bde-489">Use hello portal tooview hello Batch job and its tasks that are associated with hello **slices** and see what VM each slice ran on.</span></span>

![Azure Data Factory: attività processi di Batch](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a><span data-ttu-id="45bde-491">Eseguire il debug di pipeline hello</span><span class="sxs-lookup"><span data-stu-id="45bde-491">Debug hello pipeline</span></span>
<span data-ttu-id="45bde-492">Il debug è costituito da alcune tecniche di base:</span><span class="sxs-lookup"><span data-stu-id="45bde-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="45bde-493">Se non è troppo impostata sezione input hello**pronto**, verificare che hello struttura di cartella di input sia corretto e file. txt presente nelle cartelle di input hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-493">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and file.txt exists in hello input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="45bde-494">In hello **Execute** metodo dell'attività personalizzata, utilizzare hello **IActivityLogger** informazioni toolog oggetto che consente di risolvere i problemi.</span><span class="sxs-lookup"><span data-stu-id="45bde-494">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="45bde-495">messaggi Hello registrato visualizzata all'utente di hello\_file di log di 0.</span><span class="sxs-lookup"><span data-stu-id="45bde-495">hello logged messages show up in hello user\_0.log file.</span></span>

   <span data-ttu-id="45bde-496">In hello **OutputDataset** pannello, fare clic su hello toosee di sezione hello **sezione dati** pannello per tale sezione.</span><span class="sxs-lookup"><span data-stu-id="45bde-496">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="45bde-497">Verranno visualizzate le **esecuzioni di attività** per quella sezione.</span><span class="sxs-lookup"><span data-stu-id="45bde-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="45bde-498">Verrà visualizzata un'attività eseguire per sezione hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-498">You should see one activity run for hello slice.</span></span> <span data-ttu-id="45bde-499">Se si fa clic **eseguire** nella barra dei comandi di hello, è possibile avviare un'altra attività eseguita per hello stessa sezione.</span><span class="sxs-lookup"><span data-stu-id="45bde-499">If you click **Run** in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="45bde-500">Quando si sceglie di eseguire attività di hello, vedrai hello **Dettagli esecuzione attività** pannello con un elenco di file di log.</span><span class="sxs-lookup"><span data-stu-id="45bde-500">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="45bde-501">Vedere i messaggi registrati in hello **utente\_0 log** file.</span><span class="sxs-lookup"><span data-stu-id="45bde-501">You see logged messages in hello **user\_0.log** file.</span></span> <span data-ttu-id="45bde-502">Quando si verifica un errore, vengono visualizzati tre esecuzioni di attività perché il numero di tentativi di hello è too3 nella pipeline/attività hello JSON.</span><span class="sxs-lookup"><span data-stu-id="45bde-502">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="45bde-503">Quando si sceglie di eseguire attività di hello, vedrai che è possibile esaminare l'errore hello tootroubleshoot i file di log hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-503">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="45bde-504">Nell'elenco di hello dei file di log, fare clic su hello **utente 0.log**.</span><span class="sxs-lookup"><span data-stu-id="45bde-504">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="45bde-505">Nel riquadro di destra hello sono risultati hello dell'utilizzo di hello **IActivityLogger.Write** metodo.</span><span class="sxs-lookup"><span data-stu-id="45bde-505">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="45bde-506">È consigliabile cercare anche nel file system-0.log eventuali messaggi di errore di sistema ed eccezioni.</span><span class="sxs-lookup"><span data-stu-id="45bde-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="45bde-507">Includere hello **PDB** file nel file zip hello in modo che i dettagli dell'errore hello presentano informazioni ad esempio **stack di chiamate** quando si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="45bde-507">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="45bde-508">Tutti hello file nel file zip hello per attività personalizzata hello deve essere in hello **livello principale** senza sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="45bde-508">All hello files in hello zip file for hello custom activity must be at hello **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="45bde-509">Verificare che hello **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip) e **packageLinkedService** (deve toohello punto Azure nell'archiviazione blob che contiene i file zip hello) sono impostate toocorrect valori.</span><span class="sxs-lookup"><span data-stu-id="45bde-509">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
6. <span data-ttu-id="45bde-510">Se è stata corretta una sezione di hello tooreprocess errore e si desidera, fare doppio clic su sezione hello hello **OutputDataset** pannello e fare clic su **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="45bde-510">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="45bde-511">Nell'archiviazione BLOB di Azure verrà visualizzato un **contenitore** denominato `adfjobs`.</span><span class="sxs-lookup"><span data-stu-id="45bde-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="45bde-512">Questo contenitore non viene eliminato automaticamente, ma è possibile eliminare senza problemi dopo aver completato la soluzione di hello test.</span><span class="sxs-lookup"><span data-stu-id="45bde-512">This container is not automatically deleted, but you can safely delete it after you are done testing hello solution.</span></span> <span data-ttu-id="45bde-513">Analogamente, hello soluzioni di Data Factory crea un Batch di Azure **processo** denominato: `adf-\<pool ID/name\>:job-0000000001`.</span><span class="sxs-lookup"><span data-stu-id="45bde-513">Similarly, hello Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="45bde-514">Dopo avere testato soluzione hello se lo si desidera, è possibile eliminare il processo.</span><span class="sxs-lookup"><span data-stu-id="45bde-514">You can delete this job after you test hello solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="45bde-515">attività personalizzata Hello non utilizza hello **app** file dal pacchetto.</span><span class="sxs-lookup"><span data-stu-id="45bde-515">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="45bde-516">Pertanto, se il codice legge tutte le stringhe di connessione dal file di configurazione di hello, non funziona in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="45bde-516">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="45bde-517">Hello consigliata quando si utilizza Azure Batch è toohold tutti i segreti in un **KeyVault Azure**, utilizzare un keyvault hello tooprotect principale di servizio basato sul certificato e la distribuzione di pool di hello certificato tooAzure Batch.</span><span class="sxs-lookup"><span data-stu-id="45bde-517">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello keyvault, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="45bde-518">attività personalizzate .NET Hello quindi possono accedere i segreti in hello KeyVault in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="45bde-518">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="45bde-519">Questa soluzione è generica e può essere ridimensionato tooany tipo di chiave privata, non solo stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="45bde-519">This solution is a generic one and can scale tooany type of secret, not just connection string.</span></span>

    <span data-ttu-id="45bde-520">È una soluzione più semplice (ma non consigliata): è possibile creare un **servizio collegato SQL Azure** con le impostazioni della stringa di connessione, creare un set di dati che utilizza hello servizio collegato e catena hello dataset come un set di dati di input fittizio attività di .NET toohello personalizzata.</span><span class="sxs-lookup"><span data-stu-id="45bde-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="45bde-521">È possibile quindi hello accesso collegato stringa di connessione del servizio nel codice di attività personalizzata hello e dovrebbe funzionare correttamente in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="45bde-521">You can then access hello linked service's connection string in hello custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-hello-sample"></a><span data-ttu-id="45bde-522">Estendere l'esempio hello</span><span class="sxs-lookup"><span data-stu-id="45bde-522">Extend hello sample</span></span>
<span data-ttu-id="45bde-523">È possibile estendere questo esempio toolearn ulteriori informazioni sulle funzionalità di Data Factory di Azure e Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="45bde-523">You can extend this sample toolearn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="45bde-524">Tooprocess sezioni in un intervallo di tempo diversi, ad esempio, hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="45bde-524">For example, tooprocess slices in a different time range, do hello following steps:</span></span>

1. <span data-ttu-id="45bde-525">Aggiungere hello seguendo le sottocartelle in hello `inputfolder`: 2015-11-16-05, 2015-11-16-06 201-11-16-07, 2011-11-16-08, 09 2015-11-16 e inserire file di input in tali cartelle.</span><span class="sxs-lookup"><span data-stu-id="45bde-525">Add hello following subfolders in hello `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="45bde-526">Modificare l'ora di fine hello pipeline hello `2015-11-16T05:00:00Z` troppo`2015-11-16T10:00:00Z`.</span><span class="sxs-lookup"><span data-stu-id="45bde-526">Change hello end time for hello pipeline from `2015-11-16T05:00:00Z` too`2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="45bde-527">In hello **vista diagramma**, fare doppio clic su hello **InputDataset**e verificare che le sezioni di input hello sono pronte.</span><span class="sxs-lookup"><span data-stu-id="45bde-527">In hello **Diagram View**, double-click hello **InputDataset**, and confirm that hello input slices are ready.</span></span> <span data-ttu-id="45bde-528">Fare doppio clic su **OuptutDataset** stato hello toosee delle sezioni di output.</span><span class="sxs-lookup"><span data-stu-id="45bde-528">Double-click **OuptutDataset** toosee hello state of output slices.</span></span> <span data-ttu-id="45bde-529">Se sono in stato pronto, controllare la cartella di output hello per i file di output di hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-529">If they are in Ready state, check hello output folder for hello output files.</span></span>
2. <span data-ttu-id="45bde-530">Aumentare o diminuire hello **concorrenza** toounderstand impostazione come influisce sulle prestazioni di hello della soluzione, in particolare hello elaborazione che si verifica nel Batch di Azure.</span><span class="sxs-lookup"><span data-stu-id="45bde-530">Increase or decrease hello **concurrency** setting toounderstand how it affects hello performance of your solution, especially hello processing that occurs on Azure Batch.</span></span> <span data-ttu-id="45bde-531">(Vedere il passaggio 4: creare ed eseguire pipeline hello per ulteriori informazioni su hello **concorrenza** impostazione.)</span><span class="sxs-lookup"><span data-stu-id="45bde-531">(See Step 4: Create and run hello pipeline for more on hello **concurrency** setting.)</span></span>
3. <span data-ttu-id="45bde-532">Creare un pool con un **numero massimo di attività per ogni VM**più alto o più basso.</span><span class="sxs-lookup"><span data-stu-id="45bde-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="45bde-533">toouse hello nuovo pool è stato creato, hello aggiornamento servizio collegato Azure Batch nella soluzione di Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-533">toouse hello new pool you created, update hello Azure Batch linked service in hello Data Factory solution.</span></span> <span data-ttu-id="45bde-534">(Vedere il passaggio 4: creare ed eseguire pipeline hello per ulteriori informazioni su hello **massimo attività per ogni macchina virtuale** impostazione.)</span><span class="sxs-lookup"><span data-stu-id="45bde-534">(See Step 4: Create and run hello pipeline for more on hello **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="45bde-535">Creare un pool di Azure Batch con la funzionalità **Scalabilità automatica** .</span><span class="sxs-lookup"><span data-stu-id="45bde-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="45bde-536">Nodi di calcolo in un pool di Azure Batch di scalabilità automatica è regolazione dinamica dei hello della potenza utilizzata dall'applicazione di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="45bde-536">Automatically scaling compute nodes in an Azure Batch pool is hello dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="45bde-537">formula di esempio Hello qui si ottiene hello seguente comportamento: quando viene creato inizialmente pool hello, inizia con 1 macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="45bde-537">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="45bde-538">Metrica $PendingTasks definisce il numero di hello di attività in esecuzione + attivo (in coda) dello stato.</span><span class="sxs-lookup"><span data-stu-id="45bde-538">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="45bde-539">formula Hello trova numero medio di hello attività in sospeso in hello ultimi 180 secondi e imposta TargetDedicated di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="45bde-539">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="45bde-540">Assicura che TargetDedicated non vada mai oltre 25 macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="45bde-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="45bde-541">In tal caso, come vengono inviate nuove attività, pool aumentano automaticamente e come attività di completamento, le macchine virtuali diventano disponibile uno alla volta e la scalabilità automatica hello compatta tali macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="45bde-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="45bde-542">startingNumberOfVMs e maxNumberofVMs può essere adattato tooyour esigenze.</span><span class="sxs-lookup"><span data-stu-id="45bde-542">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>
 
    <span data-ttu-id="45bde-543">Formula di scalabilità automatica:</span><span class="sxs-lookup"><span data-stu-id="45bde-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="45bde-544">Per i dettagli, vedere [Ridimensionare automaticamente i nodi di calcolo in un pool di Azure Batch](../batch/batch-automatic-scaling.md) .</span><span class="sxs-lookup"><span data-stu-id="45bde-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="45bde-545">Se il pool di hello utilizza predefinito hello [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello servizio Batch può richiedere 15-30 minuti tooprepare hello VM prima di eseguire l'attività personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="45bde-545">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="45bde-546">Se il pool di hello sta utilizzando un diverso autoScaleEvaluationInterval, hello servizio Batch può assumere autoScaleEvaluationInterval + 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="45bde-546">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="45bde-547">Nella soluzione di esempio hello hello **Execute** metodo richiama hello **Calculate** metodo che elabora un tooproduce porzioni di dati di input una sezione di dati di output.</span><span class="sxs-lookup"><span data-stu-id="45bde-547">In hello sample solution, hello **Execute** method invokes hello **Calculate** method that processes an input data slice tooproduce an output data slice.</span></span> <span data-ttu-id="45bde-548">È possibile scrivere la propria tooprocess metodo dati di input e sostituire chiamata al metodo hello Calculate nel metodo Execute hello con un metodo di chiamata tooyour.</span><span class="sxs-lookup"><span data-stu-id="45bde-548">You can write your own method tooprocess input data and replace hello Calculate method call in hello Execute method with a call tooyour method.</span></span>

### <a name="next-steps-consume-hello-data"></a><span data-ttu-id="45bde-549">Passaggi successivi: utilizzare i dati di hello</span><span class="sxs-lookup"><span data-stu-id="45bde-549">Next steps: Consume hello data</span></span>
<span data-ttu-id="45bde-550">Dopo l'elaborazione dei dati, è possibile usarli con strumenti online come **Microsoft Power BI**.</span><span class="sxs-lookup"><span data-stu-id="45bde-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="45bde-551">Di seguito sono collegamenti toohelp comprendere Power BI e come toouse in Azure:</span><span class="sxs-lookup"><span data-stu-id="45bde-551">Here are links toohelp you understand Power BI and how toouse it in Azure:</span></span>

* [<span data-ttu-id="45bde-552">Esplorare un set di dati in Power BI</span><span class="sxs-lookup"><span data-stu-id="45bde-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="45bde-553">Introduzione a Power BI Desktop hello</span><span class="sxs-lookup"><span data-stu-id="45bde-553">Getting started with hello Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="45bde-554">Aggiornamento dei dati in Power BI</span><span class="sxs-lookup"><span data-stu-id="45bde-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="45bde-555">Azure e Power BI - Panoramica di base</span><span class="sxs-lookup"><span data-stu-id="45bde-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="45bde-556">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="45bde-556">References</span></span>
* [<span data-ttu-id="45bde-557">Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="45bde-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="45bde-558">Introduzione tooAzure servizio Data Factory</span><span class="sxs-lookup"><span data-stu-id="45bde-558">Introduction tooAzure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="45bde-559">Introduzione a Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="45bde-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="45bde-560">Usare attività personalizzate in una pipeline di Data factory di Azure</span><span class="sxs-lookup"><span data-stu-id="45bde-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="45bde-561">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="45bde-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="45bde-562">Nozioni di base su Azure Batch</span><span class="sxs-lookup"><span data-stu-id="45bde-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="45bde-563">Cenni preliminari sulle funzionalità di Azure Batch</span><span class="sxs-lookup"><span data-stu-id="45bde-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="45bde-564">Creare e gestire account Azure Batch nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="45bde-564">Create and manage Azure Batch account in hello Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="45bde-565">Introduzione alla libreria di Azure Batch per .NET</span><span class="sxs-lookup"><span data-stu-id="45bde-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
