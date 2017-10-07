---
title: aaaTutorial - libreria client di utilizzare hello Azure Batch per .NET | Documenti Microsoft
description: Informazioni su concetti di base di Azure Batch hello e compilare una soluzione semplice usando .NET.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a><span data-ttu-id="1e321-103">Iniziare a creare soluzioni alla libreria client di hello Batch per .NET</span><span class="sxs-lookup"><span data-stu-id="1e321-103">Get started building solutions with hello Batch client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1e321-104">.NET</span><span class="sxs-lookup"><span data-stu-id="1e321-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="1e321-105">Python</span><span class="sxs-lookup"><span data-stu-id="1e321-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="1e321-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="1e321-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="1e321-107">Nozioni di base hello di [Azure Batch] [ azure_batch] hello e [.NET per Batch] [ net_api] libreria in questo articolo come illustrato un passaggio dell'applicazione di esempio in c# da passaggio.</span><span class="sxs-lookup"><span data-stu-id="1e321-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span></span> <span data-ttu-id="1e321-108">Si esamina come applicazione di esempio hello sfrutta hello Batch servizio tooprocess un carico di lavoro parallelo in cloud hello e come essa interagisce con [di archiviazione di Azure](../storage/common/storage-introduction.md) per gestione temporanea di file e il recupero.</span><span class="sxs-lookup"><span data-stu-id="1e321-108">We look at how hello sample application leverages hello Batch service tooprocess a parallel workload in hello cloud, and how it interacts with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="1e321-109">Si illustra Batch applicazione flusso di lavoro comune e acquisire una comprensione di base dei componenti principali hello del Batch, ad esempio i processi, attività, i pool e nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="1e321-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="1e321-110">![Flusso di lavoro della soluzione Batch (di base)][11]</span><span class="sxs-lookup"><span data-stu-id="1e321-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="1e321-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1e321-111">Prerequisites</span></span>
<span data-ttu-id="1e321-112">Questo articolo presuppone che si sia in grado di usare C# e Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1e321-112">This article assumes that you have a working knowledge of C# and Visual Studio.</span></span> <span data-ttu-id="1e321-113">Si presuppone inoltre che si è in grado di toosatisfy hello creazione requisiti dell'account specificate di seguito per Azure e hello Batch e servizi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1e321-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="1e321-114">Account</span><span class="sxs-lookup"><span data-stu-id="1e321-114">Accounts</span></span>
* <span data-ttu-id="1e321-115">**Account Azure**: se non si ha già una sottoscrizione di Azure, [creare un account Azure gratuito][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="1e321-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="1e321-116">**Account Batch**: dopo aver creato una sottoscrizione di Azure, [creare un account Azure Batch](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1e321-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="1e321-117">**Account di archiviazione**: vedere [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="1e321-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1e321-118">Batch attualmente supporta *solo* hello **generica** tipo di account di archiviazione, come descritto nel passaggio &#5; [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [su Azure gli account di archiviazione](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="1e321-118">Batch currently supports *only* hello **general-purpose** storage account type, as described in step #5 [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

### <a name="visual-studio"></a><span data-ttu-id="1e321-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1e321-119">Visual Studio</span></span>
<span data-ttu-id="1e321-120">È necessario disporre di **Visual Studio 2015 o versione successiva** toobuild progetto di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-120">You must have **Visual Studio 2015 or newer** toobuild hello sample project.</span></span> <span data-ttu-id="1e321-121">È possibile trovare versioni gratuite e di valutazione di Visual Studio in hello [panoramica dei prodotti Visual Studio][visual_studio].</span><span class="sxs-lookup"><span data-stu-id="1e321-121">You can find free and trial versions of Visual Studio in hello [overview of Visual Studio products][visual_studio].</span></span>

### <a name="dotnettutorial-code-sample"></a><span data-ttu-id="1e321-122">*DotNetTutorial*</span><span class="sxs-lookup"><span data-stu-id="1e321-122">*DotNetTutorial* code sample</span></span>
<span data-ttu-id="1e321-123">Hello [DotNetTutorial] [ github_dotnettutorial] esempio è uno dei molti esempi di codice di Batch, vedere hello hello [esempi di azure batch] [ github_samples] repository in GitHub.</span><span class="sxs-lookup"><span data-stu-id="1e321-123">hello [DotNetTutorial][github_dotnettutorial] sample is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="1e321-124">È possibile scaricare tutti gli esempi di hello facendo **Clone o download > Download ZIP** nella home page del repository hello o facendo clic su hello [azure-batch-esempi-master.zip] [ github_samples_zip]collegamento diretto.</span><span class="sxs-lookup"><span data-stu-id="1e321-124">You can download all hello samples by clicking  **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="1e321-125">Dopo aver estratto il contenuto di hello del file ZIP hello, è possibile trovare la soluzione hello in hello seguente cartella:</span><span class="sxs-lookup"><span data-stu-id="1e321-125">Once you've extracted hello contents of hello ZIP file, you can find hello solution in hello following folder:</span></span>

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a><span data-ttu-id="1e321-126">Azure Batch Explorer (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="1e321-126">Azure Batch Explorer (optional)</span></span>
<span data-ttu-id="1e321-127">Hello [Azure Batch Explorer] [ github_batchexplorer] è un'utilità gratuita che è incluso in hello [esempi di azure batch] [ github_samples] repository in GitHub.</span><span class="sxs-lookup"><span data-stu-id="1e321-127">hello [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="1e321-128">Mentre toocomplete non necessari in questa esercitazione, può essere utile durante lo sviluppo e debug delle soluzioni di Batch.</span><span class="sxs-lookup"><span data-stu-id="1e321-128">While not required toocomplete this tutorial, it can be useful while developing and debugging your Batch solutions.</span></span>

## <a name="dotnettutorial-sample-project-overview"></a><span data-ttu-id="1e321-129">Panoramica del progetto di esempio DotNetTutorial</span><span class="sxs-lookup"><span data-stu-id="1e321-129">DotNetTutorial sample project overview</span></span>
<span data-ttu-id="1e321-130">Hello *DotNetTutorial* nell'esempio di codice è una soluzione di Visual Studio che è costituito da due progetti: **DotNetTutorial** e **TaskApplication**.</span><span class="sxs-lookup"><span data-stu-id="1e321-130">hello *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span></span>

* <span data-ttu-id="1e321-131">**DotNetTutorial** è un'applicazione hello client che interagisce con tooexecute di servizi di archiviazione e Batch hello un carico di lavoro parallelo in nodi di calcolo (macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="1e321-131">**DotNetTutorial** is hello client application that interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="1e321-132">L'esempio DotNetTutorial viene eseguito nella workstation locale.</span><span class="sxs-lookup"><span data-stu-id="1e321-132">DotNetTutorial runs on your local workstation.</span></span>
* <span data-ttu-id="1e321-133">**TaskApplication** programma hello che viene eseguito in nodi di calcolo di Azure tooperform il lavoro effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-133">**TaskApplication** is hello program that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="1e321-134">Nell'esempio hello `TaskApplication.exe` analizza hello testo in un file scaricato dall'archiviazione di Azure (file di input di hello).</span><span class="sxs-lookup"><span data-stu-id="1e321-134">In hello sample, `TaskApplication.exe` parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="1e321-135">Quindi, produce un file di testo (file di output di hello) che contiene un elenco di hello prime tre parole che vengono visualizzati nel file di input hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-135">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="1e321-136">Dopo la creazione di file di output di hello TaskApplication carica tooAzure file hello archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1e321-136">After it creates hello output file, TaskApplication uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="1e321-137">Questo rende l'applicazione client toohello disponibili per il download.</span><span class="sxs-lookup"><span data-stu-id="1e321-137">This makes it available toohello client application for download.</span></span> <span data-ttu-id="1e321-138">TaskApplication viene eseguito in parallelo in più nodi di calcolo di hello servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="1e321-138">TaskApplication runs in parallel on multiple compute nodes in hello Batch service.</span></span>

<span data-ttu-id="1e321-139">Hello diagramma seguente è illustrata hello primaria le operazioni eseguite dall'applicazione client hello, *DotNetTutorial*, un'applicazione che viene eseguita dalle attività hello, hello e *TaskApplication*.</span><span class="sxs-lookup"><span data-stu-id="1e321-139">hello following diagram illustrates hello primary operations that are performed by hello client application, *DotNetTutorial*, and hello application that is executed by hello tasks, *TaskApplication*.</span></span> <span data-ttu-id="1e321-140">Questo flusso di lavoro di base è tipico di molte soluzioni di calcolo create con Batch.</span><span class="sxs-lookup"><span data-stu-id="1e321-140">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="1e321-141">Mentre non vengono visualizzati tutte le funzionalità disponibili nel servizio Batch hello, quasi ogni scenario di Batch include parti del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="1e321-141">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="1e321-142">![Flusso di lavoro dell'esempio di Batch][8]</span><span class="sxs-lookup"><span data-stu-id="1e321-142">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="1e321-143">**Passaggio 1.**</span><span class="sxs-lookup"><span data-stu-id="1e321-143">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="1e321-144">Creare **contenitori** nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e321-144">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="1e321-145">
[**Passaggio 2.**](#step-2-upload-task-application-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="1e321-145">
[**Step 2.**](#step-2-upload-task-application-and-data-files)</span></span> <span data-ttu-id="1e321-146">Caricare i file dell'applicazione di attività e i file di input toocontainers.</span><span class="sxs-lookup"><span data-stu-id="1e321-146">Upload task application files and input files toocontainers.</span></span><br/><span data-ttu-id="1e321-147">
[**Passaggio 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="1e321-147">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="1e321-148">Creare un **pool** di Batch.</span><span class="sxs-lookup"><span data-stu-id="1e321-148">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="1e321-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="1e321-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="1e321-150">Hello pool **StartTask** download hello toonodes (TaskApplication) i file binari di attività che si connettono pool hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-150">hello pool **StartTask** downloads hello task binary files (TaskApplication) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="1e321-151">
[**Passaggio 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="1e321-151">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="1e321-152">Creare un **processo** di Batch.</span><span class="sxs-lookup"><span data-stu-id="1e321-152">Create a Batch **job**.</span></span><br/><span data-ttu-id="1e321-153">
[**Passaggio 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="1e321-153">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="1e321-154">Aggiungere **attività** toohello processo.</span><span class="sxs-lookup"><span data-stu-id="1e321-154">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="1e321-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="1e321-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="1e321-156">attività di Hello sono tooexecute pianificati sui nodi.</span><span class="sxs-lookup"><span data-stu-id="1e321-156">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="1e321-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="1e321-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="1e321-158">Ogni attività scarica i rispettivi dati di input da Archiviazione di Azure e quindi avvia l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1e321-158">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="1e321-159">
[**Passaggio 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="1e321-159">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="1e321-160">Monitorare le attività.</span><span class="sxs-lookup"><span data-stu-id="1e321-160">Monitor tasks.</span></span><br/>
  <span data-ttu-id="1e321-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="1e321-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="1e321-162">Come vengono completate, caricamento del loro tooAzure di dati di output archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1e321-162">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="1e321-163">
[**Passaggio 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="1e321-163">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="1e321-164">Scaricare l'output delle attività dal servizio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1e321-164">Download task output from Storage.</span></span>

<span data-ttu-id="1e321-165">Come indicato, non tutte le soluzioni di Batch consente di eseguire questi passaggi esatti e possono includere molte altre ancora, ma hello *DotNetTutorial* applicazione di esempio illustra i processi comuni in una soluzione di Batch.</span><span class="sxs-lookup"><span data-stu-id="1e321-165">As mentioned, not every Batch solution performs these exact steps, and may include many more, but hello *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span></span>

## <a name="build-hello-dotnettutorial-sample-project"></a><span data-ttu-id="1e321-166">Compilare hello *DotNetTutorial* progetto di esempio</span><span class="sxs-lookup"><span data-stu-id="1e321-166">Build hello *DotNetTutorial* sample project</span></span>
<span data-ttu-id="1e321-167">Prima di eseguire correttamente l'esempio hello, è necessario specificare le credenziali dell'account Batch e l'archiviazione sia in hello *DotNetTutorial* del progetto `Program.cs` file.</span><span class="sxs-lookup"><span data-stu-id="1e321-167">Before you can successfully run hello sample, you must specify both Batch and Storage account credentials in hello *DotNetTutorial* project's `Program.cs` file.</span></span> <span data-ttu-id="1e321-168">Se non è già stato fatto, aprire la soluzione hello in Visual Studio facendo doppio clic su hello `DotNetTutorial.sln` file della soluzione.</span><span class="sxs-lookup"><span data-stu-id="1e321-168">If you have not done so already, open hello solution in Visual Studio by double-clicking hello `DotNetTutorial.sln` solution file.</span></span> <span data-ttu-id="1e321-169">O aprirlo da Visual Studio utilizzando hello **File > Apri > progetto/soluzione** menu.</span><span class="sxs-lookup"><span data-stu-id="1e321-169">Or open it from within Visual Studio by using hello **File > Open > Project/Solution** menu.</span></span>

<span data-ttu-id="1e321-170">Aprire `Program.cs` all'interno di hello *DotNetTutorial* progetto.</span><span class="sxs-lookup"><span data-stu-id="1e321-170">Open `Program.cs` within hello *DotNetTutorial* project.</span></span> <span data-ttu-id="1e321-171">Quindi aggiungere le credenziali specificate superiore hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="1e321-171">Then add your credentials as specified near hello top of hello file:</span></span>

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> <span data-ttu-id="1e321-172">Come indicato in precedenza, attualmente non è necessario specificare le credenziali di hello per un **generica** account di archiviazione in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e321-172">As mentioned above, you must currently specify hello credentials for a **general-purpose** storage account in Azure Storage.</span></span> <span data-ttu-id="1e321-173">Le applicazioni di Batch utilizzano spazio di archiviazione blob hello **generica** account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1e321-173">Your Batch applications use blob storage within hello **general-purpose** storage account.</span></span> <span data-ttu-id="1e321-174">Non specificare le credenziali di hello per un account di archiviazione che è stata creata tramite la selezione hello *nell'archiviazione Blob* tipo di account.</span><span class="sxs-lookup"><span data-stu-id="1e321-174">Do not specify hello credentials for a Storage account that was created by selecting hello *Blob storage* account type.</span></span>
>
>

<span data-ttu-id="1e321-175">È possibile trovare le credenziali dell'account Batch e l'archiviazione all'interno di blade account hello di ogni servizio in hello [portale di Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="1e321-175">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="1e321-176">![Batch credenziali nel portale di hello][9]
![le credenziali di archiviazione nel portale di hello][10]</span><span class="sxs-lookup"><span data-stu-id="1e321-176">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="1e321-177">Ora che è stato aggiornato il progetto di hello con le credenziali, fare doppio clic hello soluzione in Esplora soluzioni e fare clic su **Compila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="1e321-177">Now that you've updated hello project with your credentials, right-click hello solution in Solution Explorer and click **Build Solution**.</span></span> <span data-ttu-id="1e321-178">Confermare l'operazione di ripristino di hello di tutti i pacchetti NuGet, se richiesto.</span><span class="sxs-lookup"><span data-stu-id="1e321-178">Confirm hello restoration of any NuGet packages, if you're prompted.</span></span>

> [!TIP]
> <span data-ttu-id="1e321-179">Se non vengono ripristinati automaticamente i pacchetti di NuGet hello o se vengono visualizzati errori sui pacchetti di hello toorestore errore, assicurarsi di aver hello [Gestione pacchetti NuGet] [ nuget_packagemgr] installato.</span><span class="sxs-lookup"><span data-stu-id="1e321-179">If hello NuGet packages are not automatically restored, or if you see errors about a failure toorestore hello packages, ensure that you have hello [NuGet Package Manager][nuget_packagemgr] installed.</span></span> <span data-ttu-id="1e321-180">Quindi, abilitare il download di hello di pacchetti mancanti.</span><span class="sxs-lookup"><span data-stu-id="1e321-180">Then enable hello download of missing packages.</span></span> <span data-ttu-id="1e321-181">Vedere [abilitazione pacchetto ripristinare durante la compilazione] [ nuget_restore] tooenable download del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1e321-181">See [Enabling Package Restore During Build][nuget_restore] tooenable package download.</span></span>
>
>

<span data-ttu-id="1e321-182">Hello le sezioni seguenti, è suddividere l'applicazione di esempio hello in passaggi hello tooprocess viene eseguito un carico di lavoro nel servizio Batch hello e discutere i passaggi descritti in dettaglio.</span><span class="sxs-lookup"><span data-stu-id="1e321-182">In hello following sections, we break down hello sample application into hello steps that it performs tooprocess a workload in hello Batch service, and discuss those steps in detail.</span></span> <span data-ttu-id="1e321-183">Si consiglia di toorefer toohello Apri soluzione in Visual Studio mentre si lavora in modo tramite rest hello di questo articolo, poiché non ogni riga di codice nell'esempio hello è descritto.</span><span class="sxs-lookup"><span data-stu-id="1e321-183">We encourage you toorefer toohello open solution in Visual Studio while you work your way through hello rest of this article, since not every line of code in hello sample is discussed.</span></span>

<span data-ttu-id="1e321-184">Passare toohello cima hello `MainAsync` metodo hello *DotNetTutorial* del progetto `Program.cs` file toostart con il passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="1e321-184">Navigate toohello top of hello `MainAsync` method in hello *DotNetTutorial* project's `Program.cs` file toostart with Step 1.</span></span> <span data-ttu-id="1e321-185">Ogni passaggio seguito quindi approssimativamente segue hello progressione del metodo viene chiamato `MainAsync`.</span><span class="sxs-lookup"><span data-stu-id="1e321-185">Each step below then roughly follows hello progression of method calls in `MainAsync`.</span></span>

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="1e321-186">Passaggio 1: Creare contenitori di archiviazione</span><span class="sxs-lookup"><span data-stu-id="1e321-186">Step 1: Create Storage containers</span></span>
<span data-ttu-id="1e321-187">![Creare contenitori in Archiviazione di Azure][1]
</span><span class="sxs-lookup"><span data-stu-id="1e321-187">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="1e321-188">Batch include il supporto predefinito per l'interazione con Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e321-188">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="1e321-189">I contenitori nell'account di archiviazione offrono file hello necessari per le attività di hello eseguite nell'account di Batch.</span><span class="sxs-lookup"><span data-stu-id="1e321-189">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="1e321-190">i contenitori di Hello offrono anche un posizionamento toostore hello output di dati che producono attività hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-190">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="1e321-191">in primo luogo Hello hello *DotNetTutorial* applicazione client è creare tre contenitori in [archiviazione Blob di Azure](../storage/common/storage-introduction.md):</span><span class="sxs-lookup"><span data-stu-id="1e321-191">hello first thing hello *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md):</span></span>

* <span data-ttu-id="1e321-192">**applicazione**: questo contenitore verranno archiviati applicazione hello eseguita dall'attività hello, nonché le relative dipendenze, ad esempio le DLL.</span><span class="sxs-lookup"><span data-stu-id="1e321-192">**application**: This container will store hello application run by hello tasks, as well as any of its dependencies, such as DLLs.</span></span>
* <span data-ttu-id="1e321-193">**input**: attività scaricherà tooprocess i file di dati hello dal hello *input* contenitore.</span><span class="sxs-lookup"><span data-stu-id="1e321-193">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="1e321-194">**output**: al termine dell'elaborazione del file di input di attività, verrà caricato hello risultati toohello *output* contenitore.</span><span class="sxs-lookup"><span data-stu-id="1e321-194">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="1e321-195">In ordine toointeract con uno spazio di archiviazione account e creare contenitori, utilizziamo hello [Azure Storage Client Library per .NET][net_api_storage].</span><span class="sxs-lookup"><span data-stu-id="1e321-195">In order toointeract with a Storage account and create containers, we use hello [Azure Storage Client Library for .NET][net_api_storage].</span></span> <span data-ttu-id="1e321-196">Si crea un account toohello di riferimento con [CloudStorageAccount][net_cloudstorageaccount]e da cui creare un [CloudBlobClient][net_cloudblobclient]:</span><span class="sxs-lookup"><span data-stu-id="1e321-196">We create a reference toohello account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span></span>

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="1e321-197">Utilizziamo hello `blobClient` fare riferimento in un'applicazione hello e passarlo come parametro tooseveral metodi.</span><span class="sxs-lookup"><span data-stu-id="1e321-197">We use hello `blobClient` reference throughout hello application and pass it as a parameter tooseveral methods.</span></span> <span data-ttu-id="1e321-198">Un esempio è nel blocco di codice hello che segue immediatamente hello precedente, in cui è stato chiamato `CreateContainerIfNotExistAsync` tooactually creare contenitori di hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-198">An example of this is in hello code block that immediately follows hello above, where we call `CreateContainerIfNotExistAsync` tooactually create hello containers.</span></span>

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

<span data-ttu-id="1e321-199">Dopo avere creati i contenitori di hello, un'applicazione hello ora possibile caricare file hello che verranno utilizzati dalle attività hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="1e321-200">[Come archiviazione di Blob da .NET toouse](../storage/blobs/storage-dotnet-how-to-use-blobs.md) fornisce una buona panoramica dell'utilizzo di BLOB e contenitori di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e321-200">[How toouse Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="1e321-201">Quando si inizia a batch deve essere superiore hello dell'elenco di lettura.</span><span class="sxs-lookup"><span data-stu-id="1e321-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-application-and-data-files"></a><span data-ttu-id="1e321-202">Passaggio 2: Caricare l'applicazione dell'attività e i file di dati</span><span class="sxs-lookup"><span data-stu-id="1e321-202">Step 2: Upload task application and data files</span></span>
<span data-ttu-id="1e321-203">![Attività di caricamento dell'applicazione e di input (dati) file toocontainers][2]
</span><span class="sxs-lookup"><span data-stu-id="1e321-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="1e321-204">Nel file hello caricare operazione *DotNetTutorial* prima definisce le raccolte di **applicazione** e **input** percorsi di file in cui si trovano sul computer locale hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-204">In hello file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="1e321-205">Carica quindi questi contenitori toohello file creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

<span data-ttu-id="1e321-206">Esistono due metodi in `Program.cs` che sono coinvolti nel processo di caricamento hello:</span><span class="sxs-lookup"><span data-stu-id="1e321-206">There are two methods in `Program.cs` that are involved in hello upload process:</span></span>

* <span data-ttu-id="1e321-207">`UploadFilesToContainerAsync`: Questo metodo restituisce una raccolta di [ResourceFile] [ net_resourcefile] oggetti (come descritti di seguito) e internamente chiamate `UploadFileToContainerAsync` tooupload ogni file che è passato in hello *filePaths* parametro.</span><span class="sxs-lookup"><span data-stu-id="1e321-207">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` tooupload each file that is passed in hello *filePaths* parameter.</span></span>
* <span data-ttu-id="1e321-208">`UploadFileToContainerAsync`: Questo è il metodo hello che effettivamente esegue il caricamento di file hello e crea hello [ResourceFile] [ net_resourcefile] oggetti.</span><span class="sxs-lookup"><span data-stu-id="1e321-208">`UploadFileToContainerAsync`: This is hello method that actually performs hello file upload and creates hello [ResourceFile][net_resourcefile] objects.</span></span> <span data-ttu-id="1e321-209">Dopo aver caricato il file hello, ottiene una firma di accesso condiviso (SAS) per il file hello e restituisce un oggetto ResourceFile che lo rappresenta.</span><span class="sxs-lookup"><span data-stu-id="1e321-209">After uploading hello file, it obtains a shared access signature (SAS) for hello file and returns a ResourceFile object that represents it.</span></span> <span data-ttu-id="1e321-210">Più avanti vengono illustrate anche le firme di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="1e321-210">Shared access signatures are also discussed below.</span></span>

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a><span data-ttu-id="1e321-211">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="1e321-211">ResourceFiles</span></span>
<span data-ttu-id="1e321-212">Oggetto [ResourceFile] [ net_resourcefile] fornisce operazioni in Batch con file di tooa URL hello in archiviazione di Azure che viene scaricato tooa nodo di calcolo prima di tale attività è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1e321-212">A [ResourceFile][net_resourcefile] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="1e321-213">Hello [ResourceFile.BlobSource] [ net_resourcefile_blobsource] proprietà specifica hello URL completo del file hello presenti in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e321-213">hello [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="1e321-214">Hello URL può includere una firma di accesso condiviso (SAS) che fornisce l'accesso sicuro toohello file.</span><span class="sxs-lookup"><span data-stu-id="1e321-214">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="1e321-215">Una proprietà *ResourceFiles* è inclusa nella maggior parte dei tipi di attività in Batch .NET, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1e321-215">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="1e321-216">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="1e321-216">[CloudTask][net_task]</span></span>
* <span data-ttu-id="1e321-217">[StartTask][net_pool_starttask]</span><span class="sxs-lookup"><span data-stu-id="1e321-217">[StartTask][net_pool_starttask]</span></span>
* <span data-ttu-id="1e321-218">[JobPreparationTask][net_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="1e321-218">[JobPreparationTask][net_jobpreptask]</span></span>
* <span data-ttu-id="1e321-219">[JobReleaseTask][net_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="1e321-219">[JobReleaseTask][net_jobreltask]</span></span>

<span data-ttu-id="1e321-220">Hello DotNetTutorial l'applicazione di esempio non utilizza hello JobPreparationTask o JobReleaseTask tipi di attività, ma è possibile leggere informazioni su di essi in [attività Esegui processo di preparazione e completamento del Batch di Azure i nodi di calcolo](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="1e321-220">hello DotNetTutorial sample application does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="1e321-221">Firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="1e321-221">Shared access signature (SAS)</span></span>
<span data-ttu-id="1e321-222">Accesso condiviso, le firme sono stringhe che, quando incluse come parte di un URL, fornire accesso sicuro toocontainers e BLOB in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e321-222">Shared access signatures are strings which—when included as part of a URL—provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="1e321-223">Hello DotNetTutorial applicazione vengono utilizzati entrambi blob e contenitore gli URL di firma di accesso condiviso, viene illustrato come accedere stringhe firma tooobtain questi condiviso dal servizio di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-223">hello DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="1e321-224">**Firme di accesso condiviso di BLOB**: StartTask del pool di hello in DotNetTutorial utilizza le firme di accesso condiviso di blob durante il download dei file binari dell'applicazione hello e i file di dati di input dall'archivio (vedere il # passaggio 3 riportato di seguito).</span><span class="sxs-lookup"><span data-stu-id="1e321-224">**Blob shared access signatures**: hello pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads hello application binaries and input data files from Storage (see Step #3 below).</span></span> <span data-ttu-id="1e321-225">Hello `UploadFileToContainerAsync` del DotNetTutorial metodo `Program.cs` contiene codice hello che ottiene la firma di accesso condiviso del blob ogni.</span><span class="sxs-lookup"><span data-stu-id="1e321-225">hello `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="1e321-226">L'operazione viene eseguita chiamando [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span><span class="sxs-lookup"><span data-stu-id="1e321-226">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span></span>
* <span data-ttu-id="1e321-227">**Firme di accesso condiviso contenitore**: come le operazioni sul nodo di calcolo hello al termine di ogni attività, viene caricato il toohello di file di output *output* contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e321-227">**Container shared access signatures**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="1e321-228">toodo in tal caso, TaskApplication utilizza una firma di accesso condiviso di contenitore che fornisce l'accesso in scrittura toohello contenitore come parte del percorso di hello quando viene caricato il file hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-228">toodo so, TaskApplication uses a container shared access signature that provides write access toohello container as part of hello path when it uploads hello file.</span></span> <span data-ttu-id="1e321-229">Firma di accesso condiviso di ottenere hello contenitore viene eseguita in modo simile come quando i blob hello ottenere firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="1e321-229">Obtaining hello container shared access signature is done in a similar fashion as when obtaining hello blob shared access signature.</span></span> <span data-ttu-id="1e321-230">DotNetTutorial, si noterà che hello `GetContainerSasUrl` chiamate al metodo helper [Cloudblobcontainer] [ net_sas_container] toodo in modo.</span><span class="sxs-lookup"><span data-stu-id="1e321-230">In DotNetTutorial, you will find that hello `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] toodo so.</span></span> <span data-ttu-id="1e321-231">È possibile leggere informazioni sull'utilizzo di contenitore hello TaskApplication condiviso di firma di accesso in "passaggio 6: attività di monitoraggio."</span><span class="sxs-lookup"><span data-stu-id="1e321-231">You'll read more about how TaskApplication uses hello container shared access signature in "Step 6: Monitor Tasks."</span></span>

> [!TIP]
> <span data-ttu-id="1e321-232">Check-out di serie in due parti hello sulle firme di accesso condiviso, [parte 1: hello comprensione condiviso il modello di firma di accesso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) e [parte 2: creare e usare una firma di accesso condiviso (SAS) con archiviazione Blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn ulteriori informazioni su come fornire accesso sicuro toodata nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1e321-232">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="1e321-233">Passaggio 3: Creare un pool di Batch</span><span class="sxs-lookup"><span data-stu-id="1e321-233">Step 3: Create Batch pool</span></span>
<span data-ttu-id="1e321-234">![Creare un pool di Batch][3]
</span><span class="sxs-lookup"><span data-stu-id="1e321-234">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="1e321-235">Un **pool** di Batch è una raccolta di nodi di calcolo (macchine virtuali) in cui Batch esegue le attività di un processo.</span><span class="sxs-lookup"><span data-stu-id="1e321-235">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="1e321-236">Dopo il caricamento di un'applicazione hello e i file di dati toohello account di archiviazione con le API di archiviazione di Azure, *DotNetTutorial* inizia effettua chiamate toohello Batch servizio con le API fornite dalla libreria .NET di Batch hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-236">After uploading hello application and data files toohello Storage account with Azure Storage APIs, *DotNetTutorial* begins making calls toohello Batch service with APIs provided by hello Batch .NET library.</span></span> <span data-ttu-id="1e321-237">Hello codice crea prima una [BatchClient][net_batchclient]:</span><span class="sxs-lookup"><span data-stu-id="1e321-237">hello code first creates a [BatchClient][net_batchclient]:</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

<span data-ttu-id="1e321-238">Successivamente, esempio hello crea un pool di nodi di calcolo nell'account di Batch hello con una chiamata troppo`CreatePoolIfNotExistsAsync`.</span><span class="sxs-lookup"><span data-stu-id="1e321-238">Next, hello sample creates a pool of compute nodes in hello Batch account with a call too`CreatePoolIfNotExistsAsync`.</span></span> <span data-ttu-id="1e321-239">`CreatePoolIfNotExistsAsync`Usa hello [BatchClient.PoolOperations.CreatePool] [ net_pool_create] metodo toocreate un nuovo pool di hello servizio Batch:</span><span class="sxs-lookup"><span data-stu-id="1e321-239">`CreatePoolIfNotExistsAsync` uses hello [BatchClient.PoolOperations.CreatePool][net_pool_create] method toocreate a new pool in hello Batch service:</span></span>

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

<span data-ttu-id="1e321-240">Quando si crea un pool con [CreatePool][net_pool_create], specificare diversi parametri, ad esempio il numero di hello di nodi di calcolo, hello [dimensioni dei nodi hello](../cloud-services/cloud-services-sizes-specs.md), e hello operativo dei nodi System.</span><span class="sxs-lookup"><span data-stu-id="1e321-240">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as hello number of compute nodes, hello [size of hello nodes](../cloud-services/cloud-services-sizes-specs.md), and hello nodes' operating system.</span></span> <span data-ttu-id="1e321-241">In *DotNetTutorial*, utilizziamo [CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 da [servizi Cloud](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="1e321-241">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> 

<span data-ttu-id="1e321-242">È anche possibile creare pool di nodi di calcolo che sono macchine virtuali di Azure (VM) specificando hello [VirtualMachineConfiguration] [ net_virtualmachineconfiguration] per il pool.</span><span class="sxs-lookup"><span data-stu-id="1e321-242">You can also create pools of compute nodes that are Azure Virtual Machines (VMs) by specifying hello [VirtualMachineConfiguration][net_virtualmachineconfiguration] for your pool.</span></span> <span data-ttu-id="1e321-243">È possibile creare un pool di nodi di calcolo di tipo VM da immagini Windows o [Linux](batch-linux-nodes.md).</span><span class="sxs-lookup"><span data-stu-id="1e321-243">You can create a pool of VM compute nodes from either Windows or [Linux images](batch-linux-nodes.md).</span></span> <span data-ttu-id="1e321-244">origine Hello per le immagini di macchina virtuale possono essere:</span><span class="sxs-lookup"><span data-stu-id="1e321-244">hello source for your VM images can be either:</span></span>

- <span data-ttu-id="1e321-245">Hello [macchine virtuali di Azure Marketplace][vm_marketplace], che fornisce le immagini di Windows e Linux che sono pronti all'uso.</span><span class="sxs-lookup"><span data-stu-id="1e321-245">hello [Azure Virtual Machines Marketplace][vm_marketplace], which provides both Windows and Linux images that are ready-to-use.</span></span> 
- <span data-ttu-id="1e321-246">Un'immagine personalizzata preparata e fornita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="1e321-246">A custom image that you prepare and provide.</span></span> <span data-ttu-id="1e321-247">Per informazioni dettagliate sulle immagini personalizzate, vedere [Sviluppare soluzioni di calcolo parallele su larga scala con Batch](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="1e321-247">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1e321-248">Vengono effettuati addebiti per le risorse di calcolo in Batch.</span><span class="sxs-lookup"><span data-stu-id="1e321-248">You are charged for compute resources in Batch.</span></span> <span data-ttu-id="1e321-249">toominimize costi, è possibile abbassare `targetDedicatedComputeNodes` too1 prima di eseguire l'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-249">toominimize costs, you can lower `targetDedicatedComputeNodes` too1 before you run hello sample.</span></span>
>
>

<span data-ttu-id="1e321-250">Con queste proprietà del nodo fisico, è inoltre possibile specificare un [StartTask] [ net_pool_starttask] per pool hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-250">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for hello pool.</span></span> <span data-ttu-id="1e321-251">Hello StartTask viene eseguito in ogni nodo come nodo aggiunto pool hello e ogni volta che un nodo viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="1e321-251">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="1e321-252">Hello StartTask è particolarmente utile per l'installazione di applicazioni in esecuzione precedente toohello nodi di calcolo delle attività.</span><span class="sxs-lookup"><span data-stu-id="1e321-252">hello StartTask is especially useful for installing applications on compute nodes prior toohello execution of tasks.</span></span> <span data-ttu-id="1e321-253">Se, ad esempio, le attività di elaborano i dati utilizzando gli script Python, è possibile utilizzare un tooinstall StartTask Python sui nodi di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-253">For example, if your tasks process data by using Python scripts, you could use a StartTask tooinstall Python on hello compute nodes.</span></span>

<span data-ttu-id="1e321-254">In questa applicazione di esempio, hello StartTask copia i file hello scaricati dall'archiviazione (che vengono specificati usando hello [StartTask][net_starttask].[ ResourceFiles] [ net_starttask_resourcefiles] proprietà) dalla cartella condivisa di hello StartTask lavoro directory toohello che *tutti* accessibili alle attività in esecuzione nel nodo hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-254">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from hello StartTask working directory toohello shared directory that *all* tasks running on hello node can access.</span></span> <span data-ttu-id="1e321-255">In pratica, questa copia `TaskApplication.exe` e relativo toohello dipendenze directory condivise su ciascun nodo come nodo hello join pool hello, in modo che qualsiasi attività che vengono eseguite sul nodo hello può accedervi.</span><span class="sxs-lookup"><span data-stu-id="1e321-255">Essentially, this copies `TaskApplication.exe` and its dependencies toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

> [!TIP]
> <span data-ttu-id="1e321-256">Hello **pacchetti di applicazioni** funzionalità di Batch di Azure fornisce un altro modo tooget l'applicazione nei nodi di calcolo hello in un pool.</span><span class="sxs-lookup"><span data-stu-id="1e321-256">hello **application packages** feature of Azure Batch provides another way tooget your application onto hello compute nodes in a pool.</span></span> <span data-ttu-id="1e321-257">Vedere [distribuire applicazioni toocompute nodi con i pacchetti di applicazione di Batch](batch-application-packages.md) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="1e321-257">See [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md) for details.</span></span>
>
>

<span data-ttu-id="1e321-258">Inoltre rilevanti nel frammento di codice hello sopra sono utilizzare hello due variabili di ambiente nell'hello *CommandLine* proprietà di hello StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` e `%AZ_BATCH_NODE_SHARED_DIR%`.</span><span class="sxs-lookup"><span data-stu-id="1e321-258">Also notable in hello code snippet above is hello use of two environment variables in hello *CommandLine* property of hello StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span></span> <span data-ttu-id="1e321-259">Ogni nodo di calcolo all'interno di un Batch viene configurato automaticamente con alcune variabili di ambiente sono tooBatch specifico.</span><span class="sxs-lookup"><span data-stu-id="1e321-259">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="1e321-260">Qualsiasi processo che viene eseguita da un'attività con le variabili di ambiente toothese di accesso.</span><span class="sxs-lookup"><span data-stu-id="1e321-260">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="1e321-261">toofind ulteriori informazioni sulle variabili di ambiente hello sono disponibili nei nodi di calcolo in un pool di Batch e informazioni sulla directory di lavoro attività, vedere hello [impostazioni di ambiente per l'attività](batch-api-basics.md#environment-settings-for-tasks) e [file e directory ](batch-api-basics.md#files-and-directories) sezioni hello [Cenni preliminari sulla funzionalità di Batch per gli sviluppatori](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="1e321-261">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, and information on task working directories, see hello [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) and [Files and directories](batch-api-basics.md#files-and-directories) sections in hello [Batch feature overview for developers](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="1e321-262">Passaggio 4: Creare un processo di Batch</span><span class="sxs-lookup"><span data-stu-id="1e321-262">Step 4: Create Batch job</span></span>
<span data-ttu-id="1e321-263">![Creare un processo di Batch][4]</span><span class="sxs-lookup"><span data-stu-id="1e321-263">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="1e321-264">Un **processo** di Batch è una raccolta di attività ed è associato a un pool di nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="1e321-264">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="1e321-265">attività Hello in un processo eseguito sui nodi di calcolo del pool di hello associata.</span><span class="sxs-lookup"><span data-stu-id="1e321-265">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="1e321-266">È possibile utilizzare un processo non solo per l'organizzazione e il rilevamento di attività nei carichi di lavoro correlati, ma anche per l'imposizione di determinati vincoli, ad esempio hello di esecuzione massimo per il processo di hello (e, di conseguenza, le relative attività) nonché la priorità del processo nei processi tooother relazione in hello Batch account.</span><span class="sxs-lookup"><span data-stu-id="1e321-266">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) as well as job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="1e321-267">In questo esempio, tuttavia, viene associato solo a pool hello creato nel passaggio &#3; processo hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-267">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="1e321-268">Non vengono configurate proprietà aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="1e321-268">No additional properties are configured.</span></span>

<span data-ttu-id="1e321-269">Tutti i processi di Batch sono associati a un pool specifico.</span><span class="sxs-lookup"><span data-stu-id="1e321-269">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="1e321-270">Questa associazione indica i nodi che eseguirà l'attività del processo di hello in.</span><span class="sxs-lookup"><span data-stu-id="1e321-270">This association indicates which nodes hello job's tasks will execute on.</span></span> <span data-ttu-id="1e321-271">Specificare tramite hello [CloudJob.PoolInformation] [ net_job_poolinfo] proprietà, come illustrato nel frammento di codice hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="1e321-271">You specify this by using hello [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in hello code snippet below.</span></span>

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

<span data-ttu-id="1e321-272">Ora che è stato creato un processo, le attività vengono aggiunti lavoro hello tooperform.</span><span class="sxs-lookup"><span data-stu-id="1e321-272">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="1e321-273">Passaggio 5: Aggiungere attività toojob</span><span class="sxs-lookup"><span data-stu-id="1e321-273">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="1e321-274">![Aggiungere attività toojob][5]</span><span class="sxs-lookup"><span data-stu-id="1e321-274">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="1e321-275">
*(1) processo toohello sono state aggiunte le attività, le attività di hello (2) sono pianificati toorun nei nodi e attività hello (3) scaricare tooprocess i file di dati hello*</span><span class="sxs-lookup"><span data-stu-id="1e321-275">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="1e321-276">Batch **attività** sono nodi di calcolo hello singole unità di lavoro che vengono eseguite sullo hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-276">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="1e321-277">Un'attività dispone di una riga di comando ed esegue gli script hello o file eseguibili specificati in questa riga di comando.</span><span class="sxs-lookup"><span data-stu-id="1e321-277">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="1e321-278">tooactually eseguire lavoro, è necessario aggiungere attività tooa processo.</span><span class="sxs-lookup"><span data-stu-id="1e321-278">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="1e321-279">Ogni [CloudTask] [ net_task] viene configurata con una proprietà della riga di comando e [ResourceFiles] [ net_task_resourcefiles] (come StartTask del pool di hello) che attività Hello Scarica nodo toohello prima che la riga di comando viene eseguita automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1e321-279">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="1e321-280">In hello *DotNetTutorial* progetto di esempio, ogni attività elabora un solo file.</span><span class="sxs-lookup"><span data-stu-id="1e321-280">In hello *DotNetTutorial* sample project, each task processes only one file.</span></span> <span data-ttu-id="1e321-281">Di conseguenza, la rispettiva raccolta ResourceFiles contiene un singolo elemento.</span><span class="sxs-lookup"><span data-stu-id="1e321-281">Thus, its ResourceFiles collection contains a single element.</span></span>

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> <span data-ttu-id="1e321-282">Quando accedono a variabili di ambiente, ad esempio `%AZ_BATCH_NODE_SHARED_DIR%` o eseguire un'applicazione non trovata nel nodo di hello `PATH`, righe di comando dell'attività devono essere precedute dai `cmd /c`.</span><span class="sxs-lookup"><span data-stu-id="1e321-282">When they access environment variables such as `%AZ_BATCH_NODE_SHARED_DIR%` or execute an application not found in hello node's `PATH`, task command lines must be prefixed with `cmd /c`.</span></span> <span data-ttu-id="1e321-283">In modo esplicito verrà eseguire interprete dei comandi hello e fare in modo che tooterminate dopo aver eseguito il comando.</span><span class="sxs-lookup"><span data-stu-id="1e321-283">This will explicitly execute hello command interpreter and instruct it tooterminate after carrying out your command.</span></span> <span data-ttu-id="1e321-284">Questo requisito non è necessario se un'applicazione di esecuzione delle attività nel nodo di hello `PATH` (ad esempio *robocopy.exe* o *powershell.exe*) e non le variabili di ambiente vengono utilizzate.</span><span class="sxs-lookup"><span data-stu-id="1e321-284">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` (such as *robocopy.exe* or *powershell.exe*) and no environment variables are used.</span></span>
>
>

<span data-ttu-id="1e321-285">All'interno di hello `foreach` ciclo nel frammento di codice hello precedente, è possibile vedere che la riga di comando hello per attività hello viene costruita in modo che i tre argomenti della riga di comando vengono passati troppo*TaskApplication.exe*:</span><span class="sxs-lookup"><span data-stu-id="1e321-285">Within hello `foreach` loop in hello code snippet above, you can see that hello command line for hello task is constructed such that three command-line arguments are passed too*TaskApplication.exe*:</span></span>

1. <span data-ttu-id="1e321-286">Hello **primo argomento** percorso hello di tooprocess file hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-286">hello **first argument** is hello path of hello file tooprocess.</span></span> <span data-ttu-id="1e321-287">Si tratta di file toohello percorso locale di hello quanto sia presente nel nodo hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-287">This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="1e321-288">Quando hello oggetto ResourceFile `UploadFileToContainerAsync` creazione sopra, nome del file hello è stato utilizzato per questa proprietà (come costruttore ResourceFile toohello parametro).</span><span class="sxs-lookup"><span data-stu-id="1e321-288">When hello ResourceFile object in `UploadFileToContainerAsync` was first created above, hello file name was used for this property (as a parameter toohello ResourceFile constructor).</span></span> <span data-ttu-id="1e321-289">Ciò indica che file hello è reperibile in hello stessa directory come *TaskApplication.exe*.</span><span class="sxs-lookup"><span data-stu-id="1e321-289">This indicates that hello file can be found in hello same directory as *TaskApplication.exe*.</span></span>
2. <span data-ttu-id="1e321-290">Hello **secondo argomento** specifica che la parte superiore di hello *N* parole devono essere scritti i file di output toohello.</span><span class="sxs-lookup"><span data-stu-id="1e321-290">hello **second argument** specifies that hello top *N* words should be written toohello output file.</span></span> <span data-ttu-id="1e321-291">Nell'esempio hello, questo livello di codice in modo che i tre parole hello superiore vengono scritti i file di output toohello.</span><span class="sxs-lookup"><span data-stu-id="1e321-291">In hello sample, this is hard-coded so that hello top three words are written toohello output file.</span></span>
3. <span data-ttu-id="1e321-292">Hello **terzo argomento** firma di accesso condiviso hello (SAS) che fornisce l'accesso in scrittura toohello **output** contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e321-292">hello **third argument** is hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="1e321-293">*TaskApplication.exe* vengono usati il condiviso accesso URL della firma quando carica hello output file tooAzure archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1e321-293">*TaskApplication.exe* uses this shared access signature URL when it uploads hello output file tooAzure Storage.</span></span> <span data-ttu-id="1e321-294">È disponibile codice hello per questo hello `UploadFileToContainer` metodo nel hello TaskApplication progetto `Program.cs` file:</span><span class="sxs-lookup"><span data-stu-id="1e321-294">You can find hello code for this in hello `UploadFileToContainer` method in hello TaskApplication project's `Program.cs` file:</span></span>

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="1e321-295">Passaggio 6: Monitorare le attività</span><span class="sxs-lookup"><span data-stu-id="1e321-295">Step 6: Monitor tasks</span></span>
<span data-ttu-id="1e321-296">![Monitorare le attività][6]</span><span class="sxs-lookup"><span data-stu-id="1e321-296">![Monitor tasks][6]</span></span><br/><span data-ttu-id="1e321-297">
*applicazione client di Hello (1) monitoraggi hello attività per il completamento e lo stato di esito positivo e (2) hello attività caricamento risultati dati tooAzure archiviazione*</span><span class="sxs-lookup"><span data-stu-id="1e321-297">
*hello client application (1) monitors hello tasks for completion and success status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="1e321-298">Quando le attività vengono aggiunte tooa processo, vengono automaticamente in coda e pianificate per l'esecuzione nei nodi di calcolo nel pool di hello associata al processo hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-298">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="1e321-299">In base alle impostazioni di hello specificate, Batch gestisce tutte le attività di accodamento, la pianificazione, nuovo tentativo in corso e altre funzioni di amministrazione di attività per l'utente.</span><span class="sxs-lookup"><span data-stu-id="1e321-299">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="1e321-300">Esistono molti approcci toomonitoring l'esecuzione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="1e321-300">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="1e321-301">DotNetTutorial illustra un semplice esempio che segnala solo gli stati di completamento ed esito positivo o negativo dell'attività.</span><span class="sxs-lookup"><span data-stu-id="1e321-301">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span></span> <span data-ttu-id="1e321-302">All'interno di hello `MonitorTasks` del DotNetTutorial metodo `Program.cs`, sono disponibili tre concetti .NET per Batch che garantisca la discussione.</span><span class="sxs-lookup"><span data-stu-id="1e321-302">Within hello `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span></span> <span data-ttu-id="1e321-303">I concetti sono elencati di seguito nell'ordine in cui appaiono:</span><span class="sxs-lookup"><span data-stu-id="1e321-303">They are listed below in their order of appearance:</span></span>

1. <span data-ttu-id="1e321-304">**ODATADetailLevel**: specificare [ODATADetailLevel][net_odatadetaillevel] nelle operazioni di tipo elenco, come ad esempio il recupero di un elenco delle attività di un processo, è essenziale per assicurare prestazioni ottimali per l'applicazione Batch.</span><span class="sxs-lookup"><span data-stu-id="1e321-304">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span></span> <span data-ttu-id="1e321-305">Aggiungere [Query in modo efficiente il servizio di Azure Batch hello](batch-efficient-list-queries.md) tooyour lettura dell'elenco se prevede di eseguire una sorta di monitoraggio dello stato all'interno delle applicazioni di Batch.</span><span class="sxs-lookup"><span data-stu-id="1e321-305">Add [Query hello Azure Batch service efficiently](batch-efficient-list-queries.md) tooyour reading list if you plan on doing any sort of status monitoring within your Batch applications.</span></span>
2. <span data-ttu-id="1e321-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] fornisce alle applicazioni Batch .NET le utilità helper per monitorare gli stati delle attività.</span><span class="sxs-lookup"><span data-stu-id="1e321-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span></span> <span data-ttu-id="1e321-307">In `MonitorTasks`, *DotNetTutorial* è in attesa di tutte le attività tooreach [TaskState.Completed] [ net_taskstate] entro un limite di tempo.</span><span class="sxs-lookup"><span data-stu-id="1e321-307">In `MonitorTasks`, *DotNetTutorial* waits for all tasks tooreach [TaskState.Completed][net_taskstate] within a time limit.</span></span> <span data-ttu-id="1e321-308">Quindi termina il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-308">Then it terminates hello job.</span></span>
3. <span data-ttu-id="1e321-309">**TerminateJobAsync**: terminare un processo con [JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] (o hello blocco JobOperations.TerminateJob) contrassegna tale processo come completato.</span><span class="sxs-lookup"><span data-stu-id="1e321-309">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or hello blocking JobOperations.TerminateJob) marks that job as completed.</span></span> <span data-ttu-id="1e321-310">È essenziale toodo pertanto se la soluzione Batch utilizza un [JobReleaseTask][net_jobreltask].</span><span class="sxs-lookup"><span data-stu-id="1e321-310">It is essential toodo so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span></span> <span data-ttu-id="1e321-311">un tipo speciale di attività descritto in [Attività di preparazione e completamento di processi](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="1e321-311">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span></span>

<span data-ttu-id="1e321-312">Hello `MonitorTasks` metodo *DotNetTutorial*del `Program.cs` viene visualizzato sotto:</span><span class="sxs-lookup"><span data-stu-id="1e321-312">hello `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span></span>

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="1e321-313">Passaggio 7: Scaricare l'output dell'attività</span><span class="sxs-lookup"><span data-stu-id="1e321-313">Step 7: Download task output</span></span>
<span data-ttu-id="1e321-314">![Scaricare l'output delle attività dal servizio di archiviazione][7]</span><span class="sxs-lookup"><span data-stu-id="1e321-314">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="1e321-315">Hello processo una volta completato, l'output di hello di hello attività può essere scaricato dall'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1e321-315">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="1e321-316">Questa operazione viene eseguita con una chiamata troppo`DownloadBlobsFromContainerAsync` in *DotNetTutorial*del `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="1e321-316">This is done with a call too`DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span></span>

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> <span data-ttu-id="1e321-317">Hello chiamata troppo`DownloadBlobsFromContainerAsync` in hello *DotNetTutorial* applicazione specifica che il file hello devono essere scaricato tooyour `%TEMP%` cartella.</span><span class="sxs-lookup"><span data-stu-id="1e321-317">hello call too`DownloadBlobsFromContainerAsync` in hello *DotNetTutorial* application specifies that hello files should be downloaded tooyour `%TEMP%` folder.</span></span> <span data-ttu-id="1e321-318">Ritiene toomodify disponibile in questo percorso di output.</span><span class="sxs-lookup"><span data-stu-id="1e321-318">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="1e321-319">Passaggio 8: Eliminare i contenitori</span><span class="sxs-lookup"><span data-stu-id="1e321-319">Step 8: Delete containers</span></span>
<span data-ttu-id="1e321-320">Poiché vengono addebitati i dati che si trovano in archiviazione di Azure, è sempre un BLOB tooremove buona norma che non sono più necessari per i processi Batch.</span><span class="sxs-lookup"><span data-stu-id="1e321-320">Because you are charged for data that resides in Azure Storage, it's always a good idea tooremove blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="1e321-321">In DotNetTutorial `Program.cs`, questa operazione viene eseguita con metodo di supporto toohello tre chiamate `DeleteContainerAsync`:</span><span class="sxs-lookup"><span data-stu-id="1e321-321">In DotNetTutorial's `Program.cs`, this is done with three calls toohello helper method `DeleteContainerAsync`:</span></span>

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

<span data-ttu-id="1e321-322">metodo Hello stesso Ottiene semplicemente un contenitore di toohello di riferimento e quindi chiama [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span><span class="sxs-lookup"><span data-stu-id="1e321-322">hello method itself merely obtains a reference toohello container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span></span>

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="1e321-323">Passaggio 9: Eliminare il processo di hello e pool hello</span><span class="sxs-lookup"><span data-stu-id="1e321-323">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="1e321-324">Nel passaggio finale hello, puoi toodelete richiesta hello hello e processo del pool creati dall'applicazione DotNetTutorial hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-324">In hello final step, you're prompted toodelete hello job and hello pool that were created by hello DotNetTutorial application.</span></span> <span data-ttu-id="1e321-325">Anche se non vengono addebitati costi per i processi e per le attività, *vengono* invece addebiti costi per i nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="1e321-325">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="1e321-326">È quindi consigliabile allocare i nodi solo in base alla necessità.</span><span class="sxs-lookup"><span data-stu-id="1e321-326">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="1e321-327">L'eliminazione dei pool inutilizzati può fare parte del processo di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="1e321-327">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="1e321-328">BatchClient Hello [JobOperations] [ net_joboperations] e [PoolOperations] [ net_pooloperations] dispongono di metodi di eliminazione corrispondente, ovvero se utente Hello conferma eliminazione:</span><span class="sxs-lookup"><span data-stu-id="1e321-328">hello BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if hello user confirms deletion:</span></span>

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> <span data-ttu-id="1e321-329">Occorre ricordare che vengono effettuati addebiti per le risorse di calcolo e che l'eliminazione di pool non usati consente di ridurre al minimo i costi.</span><span class="sxs-lookup"><span data-stu-id="1e321-329">Keep in mind that you are charged for compute resources—deleting unused pools will minimize cost.</span></span> <span data-ttu-id="1e321-330">Inoltre, tenere presente che l'eliminazione di un pool Elimina tutti i nodi di calcolo all'interno di tale pool e che tutti i dati nei nodi hello sarà irreversibili dopo l'eliminazione di pool hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-330">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-dotnettutorial-sample"></a><span data-ttu-id="1e321-331">Eseguire hello *DotNetTutorial* esempio</span><span class="sxs-lookup"><span data-stu-id="1e321-331">Run hello *DotNetTutorial* sample</span></span>
<span data-ttu-id="1e321-332">Quando si esegue l'applicazione di esempio hello, l'output di console hello sarà simile toohello seguente.</span><span class="sxs-lookup"><span data-stu-id="1e321-332">When you run hello sample application, hello console output will be similar toohello following.</span></span> <span data-ttu-id="1e321-333">Durante l'esecuzione, si verificherà una pausa in `Awaiting task completion, timeout in 00:30:00...` mentre vengono avviati i nodi di calcolo del pool di hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-333">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while hello pool's compute nodes are started.</span></span> <span data-ttu-id="1e321-334">Hello utilizzare [portale di Azure] [ azure_portal] toomonitor il pool, nodi di calcolo, processi e attività durante e dopo l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1e321-334">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="1e321-335">Hello utilizzare [portale di Azure] [ azure_portal] o hello [Azure Storage Explorer] [ storage_explorers] tooview hello le risorse di archiviazione (contenitori e BLOB) che sono creato da un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-335">Use hello [Azure portal][azure_portal] or hello [Azure Storage Explorer][storage_explorers] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

<span data-ttu-id="1e321-336">Tempo di esecuzione tipico è **circa 5 minuti** quando si esegue un'applicazione hello nella configurazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1e321-336">Typical execution time is **approximately 5 minutes** when you run hello application in its default configuration.</span></span>

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="1e321-337">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1e321-337">Next steps</span></span>
<span data-ttu-id="1e321-338">È gratuita toomake modifiche troppo*DotNetTutorial* e *TaskApplication* tooexperiment con diversi scenari di calcolo.</span><span class="sxs-lookup"><span data-stu-id="1e321-338">Feel free toomake changes too*DotNetTutorial* and *TaskApplication* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="1e321-339">Ad esempio, provare ad aggiungere un ritardo di esecuzione troppo*TaskApplication*, ad esempio come con [Sleep][net_thread_sleep], le attività e monitorarli nel portale di hello toosimulate con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="1e321-339">For example, try adding an execution delay too*TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="1e321-340">Provare aggiungendo più attività o modificando il numero di hello di nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="1e321-340">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="1e321-341">Aggiungere logica toocheck per e consentire l'utilizzo di hello di un tempo di esecuzione toospeed pool esistenti (*hint*: estrarre `ArticleHelpers.cs` in hello [Microsoft.Azure.Batch.Samples.Common] [ github_samples_common] nel progetto [esempi di azure batch][github_samples]).</span><span class="sxs-lookup"><span data-stu-id="1e321-341">Add logic toocheck for and allow hello use of an existing pool toospeed execution time (*hint*: check out `ArticleHelpers.cs` in hello [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span></span>

<span data-ttu-id="1e321-342">Ora che si ha familiarità con hello base del flusso di lavoro di una soluzione di Batch, è ora toodig in toohello funzionalità aggiuntive di hello servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="1e321-342">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="1e321-343">Hello revisione [funzionalità Panoramica di Azure Batch](batch-api-basics.md) articolo, è consigliabile se si è nuovo servizio toohello.</span><span class="sxs-lookup"><span data-stu-id="1e321-343">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="1e321-344">Inizio nel hello altri articoli di sviluppo di Batch in **sviluppo approfondito** in hello [il percorso di apprendimento Batch][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="1e321-344">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="1e321-345">Estrarre un'implementazione diversa di elaborazione del carico di lavoro hello "top N parole" tramite Batch in hello [TopNWords] [ github_topnwords] esempio.</span><span class="sxs-lookup"><span data-stu-id="1e321-345">Check out a different implementation of processing hello "top N words" workload by using Batch in hello [TopNWords][github_topnwords] sample.</span></span>
* <span data-ttu-id="1e321-346">Hello revisione .NET per Batch [note sulla versione](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) per le modifiche più recenti di hello nella libreria hello.</span><span class="sxs-lookup"><span data-stu-id="1e321-346">Review hello Batch .NET [release notes](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) for hello latest changes in hello library.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "Creare contenitori in Archiviazione di Azure"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Attività di caricamento dell'applicazione e di input (dati) file toocontainers"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Creare un pool di Batch"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Creare un processo di Batch"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Aggiungere attività toojob"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Monitorare le attività"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Scaricare l'output delle attività dal servizio di archiviazione"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Flusso di lavoro della soluzione Batch (diagramma completo)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Credenziali di Batch nel portale"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Credenziali del servizio di archiviazione nel portale"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Flusso di lavoro della soluzione Batch (diagramma minimo)"
