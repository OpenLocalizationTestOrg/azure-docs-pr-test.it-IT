---
title: pacchetti di applicazioni aaaInstall sui nodi di calcolo - Azure Batch | Documenti Microsoft
description: "Funzionalità di pacchetti dell'applicazione hello uso di Azure Batch tooeasily gestire più applicazioni e nodi di calcolo di versioni per l'installazione nel Batch."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a><span data-ttu-id="5b7d4-103">Distribuire i nodi toocompute di applicazioni con pacchetti di applicazione di Batch</span><span class="sxs-lookup"><span data-stu-id="5b7d4-103">Deploy applications toocompute nodes with Batch application packages</span></span>

<span data-ttu-id="5b7d4-104">funzionalità di pacchetti di applicazione Hello del Batch di Azure consente una gestione semplificata delle applicazioni di attività e i relativi toohello distribuzione nodi di calcolo nel pool di.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-104">hello application packages feature of Azure Batch provides easy management of task applications and their deployment toohello compute nodes in your pool.</span></span> <span data-ttu-id="5b7d4-105">Con i pacchetti di applicazioni, è possibile caricare e gestire più versioni di applicazioni hello che eseguire le attività, inclusi i relativi file di supporto.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-105">With application packages, you can upload and manage multiple versions of hello applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="5b7d4-106">È possibile quindi distribuire automaticamente uno o più di queste applicazioni toohello nodi di calcolo nel pool di.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-106">You can then automatically deploy one or more of these applications toohello compute nodes in your pool.</span></span>

<span data-ttu-id="5b7d4-107">In questo articolo si apprenderà come tooupload e gestire i pacchetti di applicazione nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-107">In this article, you will learn how tooupload and manage application packages in hello Azure portal.</span></span> <span data-ttu-id="5b7d4-108">Si apprenderà quindi come tooinstall in un pool nodi di calcolo con hello [.NET per Batch] [ api_net] libreria.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-108">You will then learn how tooinstall them on a pool's compute nodes with hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="5b7d4-109">I pacchetti dell'applicazione sono supportati in tutti i pool di Batch creati dopo il 5 luglio 2017.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="5b7d4-110">Sono supportate nei pool di Batch creato tra 10 marzo 2016 e 5 luglio 2017 solo se il pool di hello è stato creato utilizzando una configurazione del servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="5b7d4-111">Pool di batch creati too10 precedente marzo 2016 non supportano pacchetti di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-111">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="5b7d4-112">API per la creazione e gestione dei pacchetti di applicazione Hello fanno parte di hello [gestione .NET per Batch] [[api_net_mgmt]] libreria.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-112">hello APIs for creating and managing application packages are part of hello [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="5b7d4-113">API per l'installazione di pacchetti di applicazioni in un nodo di calcolo Hello fanno parte di hello [.NET per Batch] [ api_net] libreria.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-113">hello APIs for installing application packages on a compute node are part of hello [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="5b7d4-114">funzionalità di pacchetti di applicazione Hello descritti di seguito sostituisce funzionalità delle App Batch hello disponibili nelle versioni precedenti del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-114">hello application packages feature described here supersedes hello Batch Apps feature available in previous versions of hello service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="5b7d4-115">Requisiti dei pacchetti dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="5b7d4-115">Application package requirements</span></span>
<span data-ttu-id="5b7d4-116">pacchetti di applicazioni toouse, è necessario troppo[collegare un account di archiviazione di Azure](#link-a-storage-account) tooyour account Batch.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-116">toouse application packages, you need too[link an Azure Storage account](#link-a-storage-account) tooyour Batch account.</span></span>

<span data-ttu-id="5b7d4-117">Questa funzionalità è stata introdotta in [API REST di Batch] [ api_rest] versione 2015-12-01.2.2 e hello corrispondente [.NET per Batch] [ api_net] versione della libreria 3.1.0.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and hello corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="5b7d4-118">È consigliabile utilizzare sempre versione API più recente di hello quando si utilizzano Batch.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-118">We recommend that you always use hello latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="5b7d4-119">I pacchetti dell'applicazione sono supportati in tutti i pool di Batch creati dopo il 5 luglio 2017.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="5b7d4-120">Sono supportate nei pool di Batch creato tra 10 marzo 2016 e 5 luglio 2017 solo se il pool di hello è stato creato utilizzando una configurazione del servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="5b7d4-121">Pool di batch creati too10 precedente marzo 2016 non supportano pacchetti di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-121">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="5b7d4-122">Informazioni sulle applicazioni e sui pacchetti dell’applicazione</span><span class="sxs-lookup"><span data-stu-id="5b7d4-122">About applications and application packages</span></span>
<span data-ttu-id="5b7d4-123">All'interno di Batch di Azure, un *applicazione* fa riferimento il set di tooa dei file binari con controllo delle versioni che possono essere nodi di calcolo toohello automaticamente scaricato nel pool di.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-123">Within Azure Batch, an *application* refers tooa set of versioned binaries that can be automatically downloaded toohello compute nodes in your pool.</span></span> <span data-ttu-id="5b7d4-124">Un *pacchetto di applicazione* fa riferimento tooa *set specifico* di tali file binari e rappresenta un determinato *versione* dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-124">An *application package* refers tooa *specific set* of those binaries and represents a given *version* of hello application.</span></span>

<span data-ttu-id="5b7d4-125">![Diagramma di alto livello di applicazioni e pacchetti applicazione][1]</span><span class="sxs-lookup"><span data-stu-id="5b7d4-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="5b7d4-126">Applicazioni</span><span class="sxs-lookup"><span data-stu-id="5b7d4-126">Applications</span></span>
<span data-ttu-id="5b7d4-127">Un'applicazione in Batch contiene uno o più applicazioni, pacchetti e specifica le opzioni di configurazione per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-127">An application in Batch contains one or more application packages and specifies configuration options for hello application.</span></span> <span data-ttu-id="5b7d4-128">Ad esempio, un'applicazione può specificare hello predefinito applicazione pacchetto versione tooinstall in nodi di calcolo e se i pacchetti possono essere aggiornati o eliminati.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-128">For example, an application can specify hello default application package version tooinstall on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="5b7d4-129">Pacchetti dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="5b7d4-129">Application packages</span></span>
<span data-ttu-id="5b7d4-130">Un pacchetto di applicazione è un file con estensione zip che contiene i file binari dell'applicazione hello e i file di supporto necessari per l'applicazione hello toorun di attività.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-130">An application package is a .zip file that contains hello application binaries and supporting files that are required for your tasks toorun hello application.</span></span> <span data-ttu-id="5b7d4-131">Ogni pacchetto di applicazione rappresenta una versione specifica di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-131">Each application package represents a specific version of hello application.</span></span>

<span data-ttu-id="5b7d4-132">È possibile specificare i pacchetti di applicazioni a livello di pool e attività hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-132">You can specify application packages at hello pool and task levels.</span></span> <span data-ttu-id="5b7d4-133">È possibile specificare uno o più di questi pacchetti ed eventualmente una versione quando si crea un pool o un'attività.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="5b7d4-134">**Pacchetti di applicazioni del pool** vengono distribuiti troppo*ogni* nodo nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-134">**Pool application packages** are deployed too*every* node in hello pool.</span></span> <span data-ttu-id="5b7d4-135">Le applicazioni vengono distribuite quando un nodo viene aggiunto a un pool e quando viene riavviato o oppure la sua immagine viene ricreata.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="5b7d4-136">I pacchetti dell'applicazione del pool possono essere usati quando tutti i nodi in un pool eseguono le attività di un processo.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="5b7d4-137">È possibile specificare uno o più pacchetti dell'applicazione quando si crea un pool e aggiungere o aggiornare i pacchetti di un pool esistente.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="5b7d4-138">Se si aggiornano pacchetti di applicazioni del pool esistenti, è necessario riavviare il nuovo pacchetto hello tooinstall nodi.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-138">If you update an existing pool's application packages, you must restart its nodes tooinstall hello new package.</span></span>
* <span data-ttu-id="5b7d4-139">**Attività di pacchetti di applicazioni** vengono distribuiti solo tooa del nodo di calcolo toorun un'attività pianificata, appena prima di eseguire la riga di comando dell'attività hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-139">**Task application packages** are deployed only tooa compute node scheduled toorun a task, just before running hello task's command line.</span></span> <span data-ttu-id="5b7d4-140">Se specificato hello versione e pacchetto dell'applicazione è già presente nel nodo hello, non viene ridistribuito e viene utilizzato un pacchetto esistente hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-140">If hello specified application package and version is already on hello node, it is not redeployed and hello existing package is used.</span></span>
  
    <span data-ttu-id="5b7d4-141">Pacchetti di applicazioni di attività sono utili in ambienti pool condiviso, in cui diversi processi vengono eseguiti in un pool e pool hello non viene eliminato quando un processo viene completato.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and hello pool is not deleted when a job is completed.</span></span> <span data-ttu-id="5b7d4-142">Se il processo è l'attività più o meno di nodi nel pool di hello, pacchetti di applicazioni di attività possono ridurre al minimo il trasferimento dei dati poiché l'applicazione viene distribuita toohello solo i nodi che eseguono attività.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-142">If your job has fewer tasks than nodes in hello pool, task application packages can minimize data transfer since your application is deployed only toohello nodes that run tasks.</span></span>
  
    <span data-ttu-id="5b7d4-143">Altri scenari che possono trarre vantaggio dai pacchetti dell'applicazione per le attività sono i processi che usano un'applicazione di dimensioni elevate, ma solo per poche attività.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="5b7d4-144">Ad esempio, una fase di pre-elaborazione o un'attività di tipo merge, in cui un'applicazione hello pre-elaborazione o di tipo merge è pesante, potrebbe trarre vantaggio dall'utilizzo di pacchetti di applicazioni di attività.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-144">For example, a pre-processing stage or a merge task, where hello pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5b7d4-145">Esistono limitazioni alle dimensioni di pacchetto di applicazione massimo hello e numero hello di applicazioni e pacchetti di applicazioni all'interno di un account Batch.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-145">There are restrictions on hello number of applications and application packages within a Batch account and on hello maximum application package size.</span></span> <span data-ttu-id="5b7d4-146">Vedere [quote e limiti per il servizio Azure Batch hello](batch-quota-limit.md) per informazioni dettagliate su questi limiti.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-146">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="5b7d4-147">Vantaggi dei pacchetti dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="5b7d4-147">Benefits of application packages</span></span>
<span data-ttu-id="5b7d4-148">Pacchetti di applicazioni possono semplificare il codice di hello in Batch soluzione e inferiore hello overhead toomanage obbligatorio hello le applicazioni che eseguono le attività.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-148">Application packages can simplify hello code in your Batch solution and lower hello overhead required toomanage hello applications that your tasks run.</span></span>

<span data-ttu-id="5b7d4-149">Con i pacchetti di applicazioni, attività di avvio del pool non ha toospecify un lungo elenco di risorse singoli file tooinstall nei nodi hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-149">With application packages, your pool's start task doesn't have toospecify a long list of individual resource files tooinstall on hello nodes.</span></span> <span data-ttu-id="5b7d4-150">Non è necessario toomanually gestire più versioni dei file dell'applicazione nell'archiviazione di Azure o sui nodi di.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-150">You don't have toomanually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="5b7d4-151">E non è necessario tooworry sulla generazione di [URL SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide accedere ai file di toohello nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-151">And, you don't need tooworry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide access toohello files in your Storage account.</span></span> <span data-ttu-id="5b7d4-152">Batch funziona in background hello con pacchetti di applicazioni di servizio di archiviazione Azure toostore e distribuirli toocompute nodi.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-152">Batch works in hello background with Azure Storage toostore application packages and deploy them toocompute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="5b7d4-153">Hello dimensione totale di un'attività di avvio deve essere minore o uguale too32768 caratteri, inclusi i file di risorse e le variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-153">hello total size of a start task must be less than or equal too32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="5b7d4-154">Se l'attività di avvio supera questo limite, l'uso di pacchetti dell'applicazione è un'altra opzione.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="5b7d4-155">Si può anche creare un archivio compresso contenente i file di risorse, caricare il file come tooAzure un blob Storage e decomprimere dalla riga di comando hello dell'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-155">You can also create a zipped archive containing your resource files, upload it as a blob tooAzure Storage, and then unzip it from hello command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="5b7d4-156">Caricare e gestire le applicazioni</span><span class="sxs-lookup"><span data-stu-id="5b7d4-156">Upload and manage applications</span></span>
<span data-ttu-id="5b7d4-157">È possibile utilizzare hello [portale di Azure] [ portal] o hello [gestione .NET per Batch](batch-management-dotnet.md) pacchetti di applicazioni di libreria toomanage hello nell'account di Batch.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-157">You can use hello [Azure portal][portal] or hello [Batch Management .NET](batch-management-dotnet.md) library toomanage hello application packages in your Batch account.</span></span> <span data-ttu-id="5b7d4-158">Hello successivamente in sezioni, è innanzitutto illustrano toolink un account di archiviazione, quindi illustrati aggiungendo applicazioni e pacchetti e gestirli con hello portale.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-158">In hello next few sections, we first show how toolink a Storage account, then discuss adding applications and packages and managing them with hello portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="5b7d4-159">Collegare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="5b7d4-159">Link a Storage account</span></span>
<span data-ttu-id="5b7d4-160">pacchetti di applicazioni toouse, è innanzitutto necessario collegare un tooyour di account di archiviazione di Azure account Batch.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-160">toouse application packages, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="5b7d4-161">Se non è ancora stato configurato un account di archiviazione, hello portale di Azure consente di visualizzare hello un avviso prima volta che si fa clic su hello **applicazioni** riquadro in hello **account Batch** blade.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-161">If you have not yet configured a Storage account, hello Azure portal displays a warning hello first time you click hello **Applications** tile in hello **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5b7d4-162">Batch attualmente supporta *solo* hello **generica** tipo di account di archiviazione come descritto nel passaggio 5, [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account)nella [su Azure gli account di archiviazione](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="5b7d4-162">Batch currently supports *only* hello **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="5b7d4-163">Quando si collega un tooyour di account di archiviazione di Azure account Batch, collegare *solo* un **generica** account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-163">When you link an Azure Storage account tooyour Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="5b7d4-164">!['Nessun account di archiviazione configurato' nel portale di Azure][9]</span><span class="sxs-lookup"><span data-stu-id="5b7d4-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="5b7d4-165">Hello Batch servizio utilizza hello associati toostore account di archiviazione i pacchetti di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-165">hello Batch service uses hello associated Storage account toostore your application packages.</span></span> <span data-ttu-id="5b7d4-166">Dopo avere collegato due account hello, Batch possibile distribuire automaticamente i pacchetti hello archiviati in nodi di calcolo tooyour account archiviazione hello collegato.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-166">After you've linked hello two accounts, Batch can automatically deploy hello packages stored in hello linked Storage account tooyour compute nodes.</span></span> <span data-ttu-id="5b7d4-167">toolink un tooyour di account di archiviazione account Batch, fare clic su **impostazioni dell'account di archiviazione** su hello **avviso** blade e quindi fare clic su **Account di archiviazione** su hello **Account di archiviazione** blade.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-167">toolink a Storage account tooyour Batch account, click **Storage account settings** on hello **Warning** blade, and then click **Storage Account** on hello **Storage Account** blade.</span></span>

<span data-ttu-id="5b7d4-168">![Selezionare il pannello Account di archiviazione nel portale di Azure][10]</span><span class="sxs-lookup"><span data-stu-id="5b7d4-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="5b7d4-169">È consigliabile creare un account di archiviazione da usare *specificamente* con l'account Batch e selezionarlo qui.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="5b7d4-170">Per informazioni dettagliate su come toocreate un account di archiviazione, vedere "Creazione di un account di archiviazione" nella [gli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="5b7d4-170">For details about how toocreate a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="5b7d4-171">Dopo aver creato un account di archiviazione, è possibile quindi collegarlo account Batch tooyour utilizzando hello **Account di archiviazione** blade.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-171">After you've created a Storage account, you can then link it tooyour Batch account by using hello **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="5b7d4-172">Hello servizio Batch utilizza i pacchetti di applicazioni toostore di archiviazione di Azure come BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-172">hello Batch service uses Azure Storage toostore your application packages as block blobs.</span></span> <span data-ttu-id="5b7d4-173">Si è [addebitato come normale] [ storage_pricing] per i dati blob blocco hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-173">You are [charged as normal][storage_pricing] for hello block blob data.</span></span> <span data-ttu-id="5b7d4-174">Dimensioni di hello che tooconsider e il numero dei pacchetti di applicazione, quindi periodicamente rimuovere pacchetti deprecati toominimize costi.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-174">Be sure tooconsider hello size and number of your application packages, and periodically remove deprecated packages toominimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="5b7d4-175">Visualizzare le applicazioni correnti</span><span class="sxs-lookup"><span data-stu-id="5b7d4-175">View current applications</span></span>
<span data-ttu-id="5b7d4-176">applicazioni di hello tooview nell'account di Batch, fare clic su hello **applicazioni** voce di menu nel menu a sinistra di hello durante la visualizzazione hello **account Batch** blade.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-176">tooview hello applications in your Batch account, click hello **Applications** menu item in hello left menu while viewing hello **Batch account** blade.</span></span>

<span data-ttu-id="5b7d4-177">![Riquadro Applicazioni][2]</span><span class="sxs-lookup"><span data-stu-id="5b7d4-177">![Applications tile][2]</span></span>

<span data-ttu-id="5b7d4-178">Selezionare questa opzione di menu per aprire hello **applicazioni** pannello:</span><span class="sxs-lookup"><span data-stu-id="5b7d4-178">Selecting this menu option opens hello **Applications** blade:</span></span>

<span data-ttu-id="5b7d4-179">![Elenco applicazioni][3]</span><span class="sxs-lookup"><span data-stu-id="5b7d4-179">![List applications][3]</span></span>

<span data-ttu-id="5b7d4-180">Hello **applicazioni** pannello Visualizza hello ID di ogni applicazione nel proprio account e hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="5b7d4-180">hello **Applications** blade displays hello ID of each application in your account and hello following properties:</span></span>

* <span data-ttu-id="5b7d4-181">**Pacchetti**: hello numero di versioni associate a questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-181">**Packages**: hello number of versions associated with this application.</span></span>
* <span data-ttu-id="5b7d4-182">**Versione predefinita**: versione dell'applicazione hello installato se non è necessario indicare una versione quando si specifica un'applicazione hello per un pool.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-182">**Default version**: hello application version installed if you do not indicate a version when you specify hello application for a pool.</span></span> <span data-ttu-id="5b7d4-183">Questa impostazione è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-183">This setting is optional.</span></span>
* <span data-ttu-id="5b7d4-184">**Consenti aggiornamenti**: valore hello che specifica se pacchetto aggiornamenti, eliminazioni e aggiunte sono consentiti.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-184">**Allow updates**: hello value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="5b7d4-185">Se viene impostato troppo**n**, eliminazioni e aggiornamenti pacchetto sono disabilitate per l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-185">If this is set too**No**, package updates and deletions are disabled for hello application.</span></span> <span data-ttu-id="5b7d4-186">È possibile aggiungere solo nuove versioni del pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-186">Only new application package versions can be added.</span></span> <span data-ttu-id="5b7d4-187">valore predefinito di Hello è **Sì**.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-187">hello default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="5b7d4-188">Visualizzare i dettagli dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="5b7d4-188">View application details</span></span>
<span data-ttu-id="5b7d4-189">Pannello hello tooopen che include i dettagli di hello per un'applicazione hello dell'applicazione, selezionare in hello **applicazioni** blade.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-189">tooopen hello blade that includes hello details for an application, select hello application in hello **Applications** blade.</span></span>

<span data-ttu-id="5b7d4-190">![Dettagli applicazione][4]</span><span class="sxs-lookup"><span data-stu-id="5b7d4-190">![Application details][4]</span></span>

<span data-ttu-id="5b7d4-191">Nel Pannello di dettagli applicazione hello, è possibile configurare hello seguenti impostazioni per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-191">In hello application details blade, you can configure hello following settings for your application.</span></span>

* <span data-ttu-id="5b7d4-192">**Consenti aggiornamenti**: specificare se i pacchetti dell'applicazione possono essere aggiornati o eliminati.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="5b7d4-193">Vedere "Aggiornare o eliminare un pacchetto dell'applicazione" più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="5b7d4-194">**Versione predefinita**: specificare un pacchetto di predefinito applicazione toodeploy toocompute nodi.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-194">**Default version**: Specify a default application package toodeploy toocompute nodes.</span></span>
* <span data-ttu-id="5b7d4-195">**Nome visualizzato**: specificare un nome descrittivo del Batch soluzione può impiegare quando vengono visualizzate informazioni sull'applicazione hello, ad esempio, nell'interfaccia utente di un servizio fornito ai clienti tooyour tramite Batch hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about hello application, for example, in hello UI of a service that you provide tooyour customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="5b7d4-196">Aggiungere un’applicazione nuova</span><span class="sxs-lookup"><span data-stu-id="5b7d4-196">Add a new application</span></span>
<span data-ttu-id="5b7d4-197">toocreate una nuova applicazione, aggiungere un pacchetto di applicazione e specificare un ID applicazione di nuovi e univoci.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-197">toocreate a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="5b7d4-198">Inoltre, Hello primo pacchetto di applicazione si aggiunge con un nuovo ID applicazione di hello Crea nuova applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-198">hello first application package that you add with hello new application ID also creates hello new application.</span></span>

<span data-ttu-id="5b7d4-199">Fare clic su **Aggiungi** su hello **applicazioni** hello tooopen pannello **nuova applicazione** blade.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-199">Click **Add** on hello **Applications** blade tooopen hello **New application** blade.</span></span>

<span data-ttu-id="5b7d4-200">![Pannello Nuova applicazione nel portale di Azure][5]</span><span class="sxs-lookup"><span data-stu-id="5b7d4-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="5b7d4-201">Hello **nuova applicazione** pannello fornisce seguente hello campi impostazioni hello toospecify della nuova applicazione e il pacchetto di applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-201">hello **New application** blade provides hello following fields toospecify hello settings of your new application and application package.</span></span>

<span data-ttu-id="5b7d4-202">**ID applicazione**</span><span class="sxs-lookup"><span data-stu-id="5b7d4-202">**Application id**</span></span>

<span data-ttu-id="5b7d4-203">Questo campo specifica hello ID della nuova applicazione, che è soggetto toohello standard ID Batch di Azure le regole di convalida.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-203">This field specifies hello ID of your new application, which is subject toohello standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="5b7d4-204">le regole per fornire un ID applicazione Hello sono come segue:</span><span class="sxs-lookup"><span data-stu-id="5b7d4-204">hello rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="5b7d4-205">I nodi Windows hello ID può contenere qualsiasi combinazione di caratteri alfanumerici, trattini e caratteri di sottolineatura.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-205">On Windows nodes, hello ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="5b7d4-206">Nei nodi di Linux, sono consentiti solo caratteri alfanumerici e caratteri di sottolineatura.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="5b7d4-207">Non può contenere più di 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="5b7d4-208">Deve essere univoco all'interno di hello account Batch.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-208">Must be unique within hello Batch account.</span></span>
* <span data-ttu-id="5b7d4-209">Mantiene le maiuscole/minuscole e non fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="5b7d4-210">**Versione**</span><span class="sxs-lookup"><span data-stu-id="5b7d4-210">**Version**</span></span>

<span data-ttu-id="5b7d4-211">Questo campo specifica versione di hello hello del pacchetto di applicazione che si sta caricando.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-211">This field specifies hello version of hello application package you are uploading.</span></span> <span data-ttu-id="5b7d4-212">Le stringhe di versione sono toohello soggetto alle regole di convalida:</span><span class="sxs-lookup"><span data-stu-id="5b7d4-212">Version strings are subject toohello following validation rules:</span></span>

* <span data-ttu-id="5b7d4-213">Nei nodi di Windows, la stringa di versione hello può contenere qualsiasi combinazione di caratteri alfanumerici, trattini, caratteri di sottolineatura e punti.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-213">On Windows nodes, hello version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="5b7d4-214">Nei nodi di Linux, stringa di versione di hello può contenere solo caratteri alfanumerici e caratteri di sottolineatura.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-214">On Linux nodes, hello version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="5b7d4-215">Non può contenere più di 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="5b7d4-216">Deve essere univoco all'interno di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-216">Must be unique within hello application.</span></span>
* <span data-ttu-id="5b7d4-217">Mantengono le maiuscole/minuscole e non fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="5b7d4-218">**Pacchetto dell'applicazione**</span><span class="sxs-lookup"><span data-stu-id="5b7d4-218">**Application package**</span></span>

<span data-ttu-id="5b7d4-219">Questo campo specifica hello con estensione zip che contiene i file binari dell'applicazione hello e i file di supporto dell'applicazione hello tooexecute obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-219">This field specifies hello .zip file that contains hello application binaries and supporting files that are required tooexecute hello application.</span></span> <span data-ttu-id="5b7d4-220">Fare clic su hello **selezionare un file** casella o hello tooand toobrowse icona di cartella selezionare un file con estensione zip che contiene i file dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-220">Click hello **Select a file** box or hello folder icon toobrowse tooand select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="5b7d4-221">Dopo aver selezionato un file, fare clic su **OK** toobegin hello caricamento tooAzure archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-221">After you've selected a file, click **OK** toobegin hello upload tooAzure Storage.</span></span> <span data-ttu-id="5b7d4-222">Quando l'operazione di caricamento hello è stata completata, portale hello Visualizza una notifica e chiude il pannello hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-222">When hello upload operation is complete, hello portal displays a notification and closes hello blade.</span></span> <span data-ttu-id="5b7d4-223">A seconda delle dimensioni di hello del file hello che si sta caricando e hello velocità della connessione di rete, questa operazione potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-223">Depending on hello size of hello file that you are uploading and hello speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="5b7d4-224">Non chiudere hello **nuova applicazione** pannello prima operazione di caricamento hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-224">Do not close hello **New application** blade before hello upload operation is complete.</span></span> <span data-ttu-id="5b7d4-225">In questo modo, il processo di caricamento hello verrà interrotta.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-225">Doing so will stop hello upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="5b7d4-226">Aggiungere un nuovo pacchetto dell’applicazione</span><span class="sxs-lookup"><span data-stu-id="5b7d4-226">Add a new application package</span></span>
<span data-ttu-id="5b7d4-227">tooadd una nuova versione del pacchetto dell'applicazione per un'applicazione esistente, selezionare un'applicazione hello **applicazioni** pannello, fare clic su **pacchetti**, quindi fare clic su **Aggiungi** tooopen Hello **Aggiungi pacchetto** blade.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-227">tooadd a new application package version for an existing application, select an application in hello **Applications** blade, click **Packages**, then click **Add** tooopen hello **Add package** blade.</span></span>

<span data-ttu-id="5b7d4-228">![Pannello per aggiungere un pacchetto dell'applicazione nel portale di Azure][8]</span><span class="sxs-lookup"><span data-stu-id="5b7d4-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="5b7d4-229">Come si può notare, i campi di hello corrispondono a quelle di hello **nuova applicazione** pannello ma hello **id applicazione** casella è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-229">As you can see, hello fields match those of hello **New application** blade, but hello **Application id** box is disabled.</span></span> <span data-ttu-id="5b7d4-230">Come per la nuova applicazione hello, specificare hello **versione** per il nuovo pacchetto, visitare tooyour **pacchetto di applicazione** ZIP file, quindi fare clic su **OK** hello tooupload pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-230">As you did for hello new application, specify hello **Version** for your new package, browse tooyour **Application package** .zip file, then click **OK** tooupload hello package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="5b7d4-231">Aggiornare o eliminare un pacchetto dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="5b7d4-231">Update or delete an application package</span></span>
<span data-ttu-id="5b7d4-232">tooupdate o eliminare un pacchetto di applicazione esistente, il pannello dettagli hello open per un'applicazione hello, fare clic su **pacchetti** tooopen hello **pacchetti** pannello, fare clic su hello **i puntini di sospensione**nella riga hello hello del pacchetto di applicazione che si desidera toomodify e selezionare hello azione che si desidera tooperform.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-232">tooupdate or delete an existing application package, open hello details blade for hello application, click **Packages** tooopen hello **Packages** blade, click hello **ellipsis** in hello row of hello application package that you want toomodify, and select hello action that you want tooperform.</span></span>

<span data-ttu-id="5b7d4-233">![Aggiornare o eliminare un pacchetto nel portale di Azure][7]</span><span class="sxs-lookup"><span data-stu-id="5b7d4-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="5b7d4-234">**Aggiornare**</span><span class="sxs-lookup"><span data-stu-id="5b7d4-234">**Update**</span></span>

<span data-ttu-id="5b7d4-235">Quando fa clic su **aggiornamento**, hello *pacchetto di aggiornamento* pannello viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-235">When you click **Update**, hello *Update package* blade is displayed.</span></span> <span data-ttu-id="5b7d4-236">Questo pannello è simile toohello *nuovo pacchetto di applicazione* pannello, tuttavia, solo il campo selezione pacchetto hello è abilitato, consente toospecify un nuovo tooupload file ZIP.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-236">This blade is similar toohello *New application package* blade, however only hello package selection field is enabled, allowing you toospecify a new ZIP file tooupload.</span></span>

<span data-ttu-id="5b7d4-237">![Pannello per aggiornare un pacchetto nel portale di Azure][11]</span><span class="sxs-lookup"><span data-stu-id="5b7d4-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="5b7d4-238">**Eliminazione**</span><span class="sxs-lookup"><span data-stu-id="5b7d4-238">**Delete**</span></span>

<span data-ttu-id="5b7d4-239">Quando fa clic su **eliminare**, viene richiesto l'eliminazione di hello tooconfirm della versione del pacchetto hello e Batch Elimina pacchetto di hello da archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-239">When you click **Delete**, you are asked tooconfirm hello deletion of hello package version, and Batch deletes hello package from Azure Storage.</span></span> <span data-ttu-id="5b7d4-240">Se si elimina una versione di hello predefinita di un'applicazione, hello **versione predefinita** impostazione è stata rimossa per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-240">If you delete hello default version of an application, hello **Default version** setting is removed for hello application.</span></span>

<span data-ttu-id="5b7d4-241">![Eliminare un'applicazione ][12]</span><span class="sxs-lookup"><span data-stu-id="5b7d4-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="5b7d4-242">Installare le applicazioni su nodi di calcolo</span><span class="sxs-lookup"><span data-stu-id="5b7d4-242">Install applications on compute nodes</span></span>
<span data-ttu-id="5b7d4-243">Ora che si è appreso come applicazione toomanage dei pacchetti con hello portale di Azure, è possibile illustrare come toodeploy tali nodi toocompute ed eseguirli con le attività Batch.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-243">Now that you've learned how toomanage application packages with hello Azure portal, we can discuss how toodeploy them toocompute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="5b7d4-244">Installare pacchetti dell'applicazione nel pool</span><span class="sxs-lookup"><span data-stu-id="5b7d4-244">Install pool application packages</span></span>
<span data-ttu-id="5b7d4-245">tooinstall un pacchetto dell'applicazione in tutti i nodi di calcolo in un pool, specificare uno o più pacchetti di applicazione *riferimenti* per pool hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-245">tooinstall an application package on all compute nodes in a pool, specify one or more application package *references* for hello pool.</span></span> <span data-ttu-id="5b7d4-246">pacchetti di applicazione Hello specificato per un pool vengono installati in ogni nodo di calcolo quando viene aggiunto a tale nodo pool hello e quando il nodo hello viene riavviato o ricreata l'immagine.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-246">hello application packages that you specify for a pool are installed on each compute node when that node joins hello pool, and when hello node is rebooted or reimaged.</span></span>

<span data-ttu-id="5b7d4-247">In Batch .NET specificare uno o più [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] quando si crea un nuovo pool oppure aggiungerli al pool esistente.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="5b7d4-248">Hello [ApplicationPackageReference] [ net_pkgref] classe specifica un ID applicazione e la versione tooinstall in un pool di nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-248">hello [ApplicationPackageReference][net_pkgref] class specifies an application ID and version tooinstall on a pool's compute nodes.</span></span>

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="5b7d4-249">Se una distribuzione del pacchetto di applicazione non riesce per qualsiasi motivo, i segni di servizio Batch hello hello nodo [inutilizzabile][net_nodestate], e nessuna attività viene pianificata per l'esecuzione in tale nodo.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-249">If an application package deployment fails for any reason, hello Batch service marks hello node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="5b7d4-250">In questo caso, è necessario **riavviare** hello distribuzione dei pacchetti hello tooreinitiate nodo.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-250">In this case, you should **restart** hello node tooreinitiate hello package deployment.</span></span> <span data-ttu-id="5b7d4-251">Nodo hello riavviare consente inoltre di pianificazione delle attività nuovamente nel nodo hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-251">Restarting hello node also enables task scheduling again on hello node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="5b7d4-252">Installare pacchetti dell'applicazione per le attività</span><span class="sxs-lookup"><span data-stu-id="5b7d4-252">Install task application packages</span></span>
<span data-ttu-id="5b7d4-253">Pool tooa simile, specificare il pacchetto di applicazione *riferimenti* per un'attività.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-253">Similar tooa pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="5b7d4-254">Quando un'attività è pianificata toorun in un nodo, il pacchetto di hello viene scaricato ed estratto prima riga di comando dell'attività hello venga eseguito.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-254">When a task is scheduled toorun on a node, hello package is downloaded and extracted just before hello task's command line is executed.</span></span> <span data-ttu-id="5b7d4-255">Se un pacchetto specificato e la versione è già installato nel nodo hello, non viene scaricato il pacchetto di hello e viene utilizzato un pacchetto esistente hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-255">If a specified package and version is already installed on hello node, hello package is not downloaded and hello existing package is used.</span></span>

<span data-ttu-id="5b7d4-256">tooinstall un pacchetto di applicazione di attività, configurare dell'attività hello [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] proprietà:</span><span class="sxs-lookup"><span data-stu-id="5b7d4-256">tooinstall a task application package, configure hello task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-hello-installed-applications"></a><span data-ttu-id="5b7d4-257">Eseguire le applicazioni hello installato</span><span class="sxs-lookup"><span data-stu-id="5b7d4-257">Execute hello installed applications</span></span>
<span data-ttu-id="5b7d4-258">vengono scaricati Hello pacchetti specificati per un pool o un'attività ed estratti tooa denominato directory all'interno di hello `AZ_BATCH_ROOT_DIR` del nodo hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-258">hello packages that you've specified for a pool or task are downloaded and extracted tooa named directory within hello `AZ_BATCH_ROOT_DIR` of hello node.</span></span> <span data-ttu-id="5b7d4-259">Batch Crea inoltre una variabile di ambiente contenente toohello percorso hello denominato directory.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-259">Batch also creates an environment variable that contains hello path toohello named directory.</span></span> <span data-ttu-id="5b7d4-260">Le righe di comando attività usare questa variabile di ambiente quando si fa riferimento a un'applicazione hello nel nodo hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-260">Your task command lines use this environment variable when referencing hello application on hello node.</span></span> 

<span data-ttu-id="5b7d4-261">Variabile hello è nodi Windows in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="5b7d4-261">On Windows nodes, hello variable is in hello following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="5b7d4-262">In nodi di Linux, il formato di hello è leggermente diverso.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-262">On Linux nodes, hello format is slightly different.</span></span> <span data-ttu-id="5b7d4-263">Punti (.), trattini (-) e simboli di cancelletto (#) sono bidimensionali toounderscores nella variabile di ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-263">Periods (.), hypens (-) and number signs (#) are flattened toounderscores in hello environment variable.</span></span> <span data-ttu-id="5b7d4-264">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="5b7d4-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="5b7d4-265">`APPLICATIONID`e `version` sono valori che corrispondono toohello applicazione e versione del pacchetto è stato specificato per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-265">`APPLICATIONID` and `version` are values that correspond toohello application and package version you've specified for deployment.</span></span> <span data-ttu-id="5b7d4-266">Ad esempio, se è stata specificata la versione 2.7 di applicazione *blender* deve essere installata nei nodi di Windows, le righe di comando attività utilizzerà questo tooaccess variabile di ambiente relativi file:</span><span class="sxs-lookup"><span data-stu-id="5b7d4-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable tooaccess its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="5b7d4-267">Nei nodi di Linux, specificare la variabile di ambiente hello nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="5b7d4-267">On Linux nodes, specify hello environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="5b7d4-268">Quando si carica un pacchetto di applicazione, è possibile specificare un tooyour toodeploy di versione predefinito nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-268">When you upload an application package, you can specify a default version toodeploy tooyour compute nodes.</span></span> <span data-ttu-id="5b7d4-269">Se è stata specificata una versione predefinita per un'applicazione, è possibile omettere il suffisso di versione di hello quando si fa riferimento a un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-269">If you have specified a default version for an application, you can omit hello version suffix when you reference hello application.</span></span> <span data-ttu-id="5b7d4-270">È possibile specificare una versione di hello predefinito dell'applicazione nel portale di Azure, nel Pannello di applicazioni hello, hello come illustrato nella [caricare e gestire applicazioni](#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="5b7d4-270">You can specify hello default application version in hello Azure portal, on hello Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="5b7d4-271">Ad esempio, se si imposta come versione di hello predefinita per l'applicazione "2.7" *blender*, le attività di riferimento hello seguente variabile di ambiente, quindi i nodi Windows eseguirà versione 2.7:</span><span class="sxs-lookup"><span data-stu-id="5b7d4-271">For example, if you set "2.7" as hello default version for application *blender*, and your tasks reference hello following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="5b7d4-272">Hello frammento di codice seguente viene illustrata una riga di comando di attività di esempio che avvia versione di hello predefinita di hello *blender* applicazione:</span><span class="sxs-lookup"><span data-stu-id="5b7d4-272">hello following code snippet shows an example task command line that launches hello default version of hello *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="5b7d4-273">Vedere [impostazioni di ambiente per l'attività](batch-api-basics.md#environment-settings-for-tasks) in hello [Cenni preliminari sulle funzionalità di Batch](batch-api-basics.md) per ulteriori informazioni sulle impostazioni di ambiente nodo di calcolo.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in hello [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="5b7d4-274">Aggiornare i pacchetti dell’applicazione di un pool</span><span class="sxs-lookup"><span data-stu-id="5b7d4-274">Update a pool's application packages</span></span>
<span data-ttu-id="5b7d4-275">Se un pool esistente è già stato configurato con un pacchetto di applicazione, è possibile specificare un nuovo pacchetto per il pool di hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-275">If an existing pool has already been configured with an application package, you can specify a new package for hello pool.</span></span> <span data-ttu-id="5b7d4-276">Se si specifica un nuovo riferimento pacchetto per un pool, si applicano i seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="5b7d4-276">If you specify a new package reference for a pool, hello following apply:</span></span>

* <span data-ttu-id="5b7d4-277">Hello servizio Batch installa hello appena specificato per il pacchetto in tutti i nuovi nodi che uniscono in join pool hello e su qualsiasi nodo esistente che è stato riavviato oppure ricreata l'immagine.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-277">hello Batch service installs hello newly specified package on all new nodes that join hello pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="5b7d4-278">Consente di calcolare i nodi già presenti nel pool di hello quando si aggiorna hello pacchetto fa riferimento non installano automaticamente il nuovo pacchetto di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-278">Compute nodes that are already in hello pool when you update hello package references do not automatically install hello new application package.</span></span> <span data-ttu-id="5b7d4-279">Questi nodi è necessario riavviare o calcolo tooreceive nuove immagini hello nuovo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-279">These compute nodes must be rebooted or reimaged tooreceive hello new package.</span></span>
* <span data-ttu-id="5b7d4-280">Quando viene distribuito un nuovo pacchetto, creata variabili di ambiente hello riflettono hello nuova applicazione pacchetto fa riferimento.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-280">When a new package is deployed, hello created environment variables reflect hello new application package references.</span></span>

<span data-ttu-id="5b7d4-281">In questo esempio, un pool esistente hello è versione 2.7 di hello *blender* applicazione configurata come uno dei relativi [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref].</span><span class="sxs-lookup"><span data-stu-id="5b7d4-281">In this example, hello existing pool has version 2.7 of hello *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="5b7d4-282">i nodi del pool di hello tooupdate con versione 2.76b, specificare un nuovo [ApplicationPackageReference] [ net_pkgref] con una nuova versione di hello e commit hello modifica.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-282">tooupdate hello pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with hello new version, and commit hello change.</span></span>

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

<span data-ttu-id="5b7d4-283">Ora che hello nuova versione è stata configurata, hello servizio Batch installa versione 2.76b tooany *nuova* nodi aggiunti al pool di hello.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-283">Now that hello new version has been configured, hello Batch service installs version 2.76b tooany *new* node that joins hello pool.</span></span> <span data-ttu-id="5b7d4-284">tooinstall 2.76b in hello i nodi *già* nel pool di hello, riavviare o ricreare l'immagine di essi.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-284">tooinstall 2.76b on hello nodes that are *already* in hello pool, reboot or reimage them.</span></span> <span data-ttu-id="5b7d4-285">Si noti che i nodi riavviati mantengono file hello da distribuzioni di pacchetto precedente.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-285">Note that rebooted nodes retain hello files from previous package deployments.</span></span>

## <a name="list-hello-applications-in-a-batch-account"></a><span data-ttu-id="5b7d4-286">Elenco di applicazioni hello in un account Batch</span><span class="sxs-lookup"><span data-stu-id="5b7d4-286">List hello applications in a Batch account</span></span>
<span data-ttu-id="5b7d4-287">È possibile elencare i pacchetti in un account di Batch e applicazioni hello utilizzando hello [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] metodo.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-287">You can list hello applications and their packages in a Batch account by using hello [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List hello applications and their application packages in hello Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a><span data-ttu-id="5b7d4-288">Eseguire il wrapping</span><span class="sxs-lookup"><span data-stu-id="5b7d4-288">Wrap up</span></span>
<span data-ttu-id="5b7d4-289">Con pacchetti di applicazioni, è possibile aiutare i clienti selezionare applicazioni hello per svolgere il lavoro e specificare hello versione esatta toouse durante l'elaborazione di processi con il servizio Batch abilitata.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-289">With application packages, you can help your customers select hello applications for their jobs and specify hello exact version toouse when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="5b7d4-290">Potrebbe inoltre offrono possibilità di hello per tooupload i clienti e tenere traccia delle proprie applicazioni del servizio.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-290">You might also provide hello ability for your customers tooupload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b7d4-291">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5b7d4-291">Next steps</span></span>
* <span data-ttu-id="5b7d4-292">Hello [API REST di Batch] [ api_rest] fornisce inoltre supporto toowork con pacchetti di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-292">hello [Batch REST API][api_rest] also provides support toowork with application packages.</span></span> <span data-ttu-id="5b7d4-293">Ad esempio, vedere hello [applicationPackageReferences] [ rest_add_pool_with_packages] elemento [aggiungere un account del pool di tooan] [ rest_add_pool] per informazioni su come toospecify tooinstall di pacchetti tramite hello API REST.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-293">For example, see hello [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool tooan account][rest_add_pool] for information about how toospecify packages tooinstall by using hello REST API.</span></span> <span data-ttu-id="5b7d4-294">Vedere [applicazioni] [ rest_applications] per informazioni dettagliate su come le informazioni sull'applicazione tooobtain utilizzando hello API REST di Batch.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-294">See [Applications][rest_applications] for details about how tooobtain application information by using hello Batch REST API.</span></span>
* <span data-ttu-id="5b7d4-295">Informazioni su come tooprogrammatically [gestire gli account Azure Batch e le quote con gestione .NET per Batch](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5b7d4-295">Learn how tooprogrammatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="5b7d4-296">Hello [gestione .NET per Batch][api_net_mgmt] libreria è possibile abilitare funzionalità di creazione e l'eliminazione di account per l'applicazione di Batch o di un servizio.</span><span class="sxs-lookup"><span data-stu-id="5b7d4-296">hello [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "Diagramma di alto livello di pacchetti applicazione"
[2]: ./media/batch-application-packages/app_pkg_02.png "Riquadro Applicazioni nel portale di Azure"
[3]: ./media/batch-application-packages/app_pkg_03.png "Pannello Applicazioni nel portale di Azure"
[4]: ./media/batch-application-packages/app_pkg_04.png "Pannello Dettagli applicazione nel portale di Azure"
[5]: ./media/batch-application-packages/app_pkg_05.png "Pannello Nuova applicazione nel portale di Azure"
[7]: ./media/batch-application-packages/app_pkg_07.png "Elenco a discesa per aggiornamento o eliminazione pacchetto nel portale di Azure"
[8]: ./media/batch-application-packages/app_pkg_08.png "Pannello per nuovo pacchetto dell'applicazione nel portale di Azure"
[9]: ./media/batch-application-packages/app_pkg_09.png " Nessun account di archiviazione collegato"
[10]: ./media/batch-application-packages/app_pkg_10.png "Selezionare il pannello Account di archiviazione nel portale di Azure"
[11]: ./media/batch-application-packages/app_pkg_11.png "Pannello Aggiorna pacchetto nel portale di Azure"
[12]: ./media/batch-application-packages/app_pkg_12.png "Finestra di conferma eliminazione pacchetto nel portale di Azure"
