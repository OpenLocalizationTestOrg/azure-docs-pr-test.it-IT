---
title: Installare pacchetti dell'applicazione nei nodi di calcolo - Azure Batch | Microsoft Docs
description: "Usare la funzionalità dei pacchetti dell’applicazione di Azure Batch per gestire facilmente più applicazioni e versioni ed eseguire l'installazione su nodi di calcolo in Batch."
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
ms.openlocfilehash: afcc04c80ec15872a22de5d5969a7ef6a583562f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-applications-to-compute-nodes-with-batch-application-packages"></a><span data-ttu-id="4ceba-103">Distribuire le applicazioni nei nodi di calcolo con i pacchetti dell'applicazione Batch</span><span class="sxs-lookup"><span data-stu-id="4ceba-103">Deploy applications to compute nodes with Batch application packages</span></span>

<span data-ttu-id="4ceba-104">I pacchetti dell'applicazione sono una funzionalità di Azure Batch che consente di gestire e distribuire facilmente le applicazioni per le attività nei nodi di calcolo del pool.</span><span class="sxs-lookup"><span data-stu-id="4ceba-104">The application packages feature of Azure Batch provides easy management of task applications and their deployment to the compute nodes in your pool.</span></span> <span data-ttu-id="4ceba-105">I pacchetti dell'applicazione consentono di caricare e gestire più versioni delle applicazioni eseguite dalle attività, inclusi i file di supporto.</span><span class="sxs-lookup"><span data-stu-id="4ceba-105">With application packages, you can upload and manage multiple versions of the applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="4ceba-106">È quindi possibile di distribuire automaticamente una o più applicazioni nei nodi di calcolo del pool.</span><span class="sxs-lookup"><span data-stu-id="4ceba-106">You can then automatically deploy one or more of these applications to the compute nodes in your pool.</span></span>

<span data-ttu-id="4ceba-107">In questo articolo si apprenderà come caricare e gestire pacchetti dell'applicazione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ceba-107">In this article, you will learn how to upload and manage application packages in the Azure portal.</span></span> <span data-ttu-id="4ceba-108">Si apprenderà quindi come installarli nei nodi di calcolo di un pool usando la libreria [Batch .NET][api_net].</span><span class="sxs-lookup"><span data-stu-id="4ceba-108">You will then learn how to install them on a pool's compute nodes with the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="4ceba-109">I pacchetti dell'applicazione sono supportati in tutti i pool di Batch creati dopo il 5 luglio 2017.</span><span class="sxs-lookup"><span data-stu-id="4ceba-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="4ceba-110">Sono supportati nei pool di Batch creati tra il 10 marzo 2016 e il 5 luglio 2017 solo se il pool è stato creato usando una configurazione del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="4ceba-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="4ceba-111">I pool di Batch creati prima del 10 marzo 2016 non supportano i pacchetti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-111">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="4ceba-112">Le API per la creazione e la gestione dei pacchetti dell'applicazione fanno parte della raccolta [Batch Management .NET] [[api_net_mgmt]].</span><span class="sxs-lookup"><span data-stu-id="4ceba-112">The APIs for creating and managing application packages are part of the [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="4ceba-113">Le API per l'installazione dei pacchetti dell'applicazione in un nodo di calcolo sono parte della raccolta [Batch .NET][api_net].</span><span class="sxs-lookup"><span data-stu-id="4ceba-113">The APIs for installing application packages on a compute node are part of the [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="4ceba-114">La funzionalità dei pacchetti dell’applicazione descritta di seguito sostituisce la funzionalità App Batch disponibile nelle versioni precedenti del servizio.</span><span class="sxs-lookup"><span data-stu-id="4ceba-114">The application packages feature described here supersedes the Batch Apps feature available in previous versions of the service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="4ceba-115">Requisiti dei pacchetti dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="4ceba-115">Application package requirements</span></span>
<span data-ttu-id="4ceba-116">Per usare i pacchetti dell'applicazione, è necessario [collegare un account di archiviazione di Azure](#link-a-storage-account) all'account Batch.</span><span class="sxs-lookup"><span data-stu-id="4ceba-116">To use application packages, you need to [link an Azure Storage account](#link-a-storage-account) to your Batch account.</span></span>

<span data-ttu-id="4ceba-117">Questa funzionalità è stata introdotta nella versione 2015-12-01.2.2 dell'[API REST Batch][api_rest] e nella versione 3.1.0 della libreria [Batch .NET][api_net] corrispondente.</span><span class="sxs-lookup"><span data-stu-id="4ceba-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and the corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="4ceba-118">È consigliabile usare sempre la versione API più recente quando si usa Batch.</span><span class="sxs-lookup"><span data-stu-id="4ceba-118">We recommend that you always use the latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="4ceba-119">I pacchetti dell'applicazione sono supportati in tutti i pool di Batch creati dopo il 5 luglio 2017.</span><span class="sxs-lookup"><span data-stu-id="4ceba-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="4ceba-120">Sono supportati nei pool di Batch creati tra il 10 marzo 2016 e il 5 luglio 2017 solo se il pool è stato creato usando una configurazione del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="4ceba-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="4ceba-121">I pool di batch creati prima del 10 marzo 2016 non supportano i pacchetti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-121">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="4ceba-122">Informazioni sulle applicazioni e sui pacchetti dell’applicazione</span><span class="sxs-lookup"><span data-stu-id="4ceba-122">About applications and application packages</span></span>
<span data-ttu-id="4ceba-123">Per *applicazione* in Azure Batch si intende un set di file binari con versione che possono essere scaricati automaticamente nei nodi di calcolo del pool.</span><span class="sxs-lookup"><span data-stu-id="4ceba-123">Within Azure Batch, an *application* refers to a set of versioned binaries that can be automatically downloaded to the compute nodes in your pool.</span></span> <span data-ttu-id="4ceba-124">Un *pacchetto dell'applicazione* è invece un *set specifico* di tali file binari e rappresenta una *versione* specifica dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-124">An *application package* refers to a *specific set* of those binaries and represents a given *version* of the application.</span></span>

<span data-ttu-id="4ceba-125">![Diagramma di alto livello di applicazioni e pacchetti applicazione][1]</span><span class="sxs-lookup"><span data-stu-id="4ceba-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="4ceba-126">Applicazioni</span><span class="sxs-lookup"><span data-stu-id="4ceba-126">Applications</span></span>
<span data-ttu-id="4ceba-127">Un'applicazione in Batch contiene uno o più pacchetti dell'applicazione e specifica le opzioni di configurazione per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-127">An application in Batch contains one or more application packages and specifies configuration options for the application.</span></span> <span data-ttu-id="4ceba-128">Un'applicazione può ad esempio specificare la versione predefinita del pacchetto dell'applicazione da installare nei nodi di calcolo e se i pacchetti possono essere aggiornati o eliminati.</span><span class="sxs-lookup"><span data-stu-id="4ceba-128">For example, an application can specify the default application package version to install on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="4ceba-129">Pacchetti dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="4ceba-129">Application packages</span></span>
<span data-ttu-id="4ceba-130">Un pacchetto dell'applicazione è un file zip contenente i file binari e i file di supporto dell'applicazione necessari per le attività di esecuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-130">An application package is a .zip file that contains the application binaries and supporting files that are required for your tasks to run the application.</span></span> <span data-ttu-id="4ceba-131">Ogni pacchetto dell’applicazione rappresenta una versione specifica dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-131">Each application package represents a specific version of the application.</span></span>

<span data-ttu-id="4ceba-132">È possibile specificare i pacchetti dell'applicazione a livello di pool e di attività.</span><span class="sxs-lookup"><span data-stu-id="4ceba-132">You can specify application packages at the pool and task levels.</span></span> <span data-ttu-id="4ceba-133">È possibile specificare uno o più di questi pacchetti ed eventualmente una versione quando si crea un pool o un'attività.</span><span class="sxs-lookup"><span data-stu-id="4ceba-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="4ceba-134">**pacchetti dell'applicazione del pool** vengono distribuiti in *ogni* nodo del pool.</span><span class="sxs-lookup"><span data-stu-id="4ceba-134">**Pool application packages** are deployed to *every* node in the pool.</span></span> <span data-ttu-id="4ceba-135">Le applicazioni vengono distribuite quando un nodo viene aggiunto a un pool e quando viene riavviato o oppure la sua immagine viene ricreata.</span><span class="sxs-lookup"><span data-stu-id="4ceba-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="4ceba-136">I pacchetti dell'applicazione del pool possono essere usati quando tutti i nodi in un pool eseguono le attività di un processo.</span><span class="sxs-lookup"><span data-stu-id="4ceba-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="4ceba-137">È possibile specificare uno o più pacchetti dell'applicazione quando si crea un pool e aggiungere o aggiornare i pacchetti di un pool esistente.</span><span class="sxs-lookup"><span data-stu-id="4ceba-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="4ceba-138">Se si aggiornano i pacchetti dell'applicazione di un pool esistente, è necessario riavviare i nodi per installare il nuovo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4ceba-138">If you update an existing pool's application packages, you must restart its nodes to install the new package.</span></span>
* <span data-ttu-id="4ceba-139">**pacchetti dell'applicazione per le attività** vengono distribuiti solo in un nodo di calcolo che dovrà eseguire un'attività, appena prima di eseguire la riga di comando dell'attività.</span><span class="sxs-lookup"><span data-stu-id="4ceba-139">**Task application packages** are deployed only to a compute node scheduled to run a task, just before running the task's command line.</span></span> <span data-ttu-id="4ceba-140">Se il pacchetto dell'applicazione specificato con la versione corrispondente si trova già nel nodo, non verrà ridistribuito e verrà usato il pacchetto esistente.</span><span class="sxs-lookup"><span data-stu-id="4ceba-140">If the specified application package and version is already on the node, it is not redeployed and the existing package is used.</span></span>
  
    <span data-ttu-id="4ceba-141">I pacchetti dell'applicazione per le attività sono utili in ambienti di pool condivisi, in cui diversi processi vengono eseguiti in un pool e il pool non viene eliminato quando viene completato un processo.</span><span class="sxs-lookup"><span data-stu-id="4ceba-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and the pool is not deleted when a job is completed.</span></span> <span data-ttu-id="4ceba-142">Se il processo ha meno attività che nodi nel pool, i pacchetti dell'applicazione di attività possono ridurre il trasferimento dei dati, perché l'applicazione viene distribuita solo nei nodi che eseguono le attività.</span><span class="sxs-lookup"><span data-stu-id="4ceba-142">If your job has fewer tasks than nodes in the pool, task application packages can minimize data transfer since your application is deployed only to the nodes that run tasks.</span></span>
  
    <span data-ttu-id="4ceba-143">Altri scenari che possono trarre vantaggio dai pacchetti dell'applicazione per le attività sono i processi che usano un'applicazione di dimensioni elevate, ma solo per poche attività.</span><span class="sxs-lookup"><span data-stu-id="4ceba-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="4ceba-144">Una fase di pre-elaborazione o un'attività di unione in cui l'applicazione di pre-elaborazione o di unione è pesante possono ad esempio beneficiare dell'uso di pacchetti dell'applicazione per le attività.</span><span class="sxs-lookup"><span data-stu-id="4ceba-144">For example, a pre-processing stage or a merge task, where the pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ceba-145">Sono previste restrizioni al numero di applicazioni e di pacchetti dell'applicazione in un account Batch e alle dimensioni massime del pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-145">There are restrictions on the number of applications and application packages within a Batch account and on the maximum application package size.</span></span> <span data-ttu-id="4ceba-146">Per informazioni dettagliate su questi limiti, vedere [Quote e limiti per il servizio Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="4ceba-146">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="4ceba-147">Vantaggi dei pacchetti dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="4ceba-147">Benefits of application packages</span></span>
<span data-ttu-id="4ceba-148">Con i pacchetti dell'applicazione è possibile semplificare il codice nella soluzione Batch e ridurre il sovraccarico richiesto in termini di gestione delle applicazioni eseguite delle attività.</span><span class="sxs-lookup"><span data-stu-id="4ceba-148">Application packages can simplify the code in your Batch solution and lower the overhead required to manage the applications that your tasks run.</span></span>

<span data-ttu-id="4ceba-149">Con i pacchetti dell'applicazione non è necessario che l'attività di avvio del pool specifichi un lungo elenco di singoli file di risorse da installare nei nodi.</span><span class="sxs-lookup"><span data-stu-id="4ceba-149">With application packages, your pool's start task doesn't have to specify a long list of individual resource files to install on the nodes.</span></span> <span data-ttu-id="4ceba-150">Non è necessario gestire manualmente più versioni dei file dell'applicazione in Archiviazione di Azure o nei nodi.</span><span class="sxs-lookup"><span data-stu-id="4ceba-150">You don't have to manually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="4ceba-151">Per accedere ai file nell'account di archiviazione non è necessario generare un [URL di firma di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) .</span><span class="sxs-lookup"><span data-stu-id="4ceba-151">And, you don't need to worry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to provide access to the files in your Storage account.</span></span> <span data-ttu-id="4ceba-152">Batch interagisce in background con Archiviazione di Azure per archiviare e distribuire i pacchetti dell'applicazione nei nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="4ceba-152">Batch works in the background with Azure Storage to store application packages and deploy them to compute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="4ceba-153">La dimensione totale di un'attività di avvio deve essere inferiore o uguale a 32768 caratteri, inclusi i file di risorse e le variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="4ceba-153">The total size of a start task must be less than or equal to 32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="4ceba-154">Se l'attività di avvio supera questo limite, l'uso di pacchetti dell'applicazione è un'altra opzione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="4ceba-155">Si può inoltre creare un archivio compresso contenente i file di risorse, caricarlo come un BLOB in Archiviazione di Azure e quindi decomprimerlo dalla riga di comando dell'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="4ceba-155">You can also create a zipped archive containing your resource files, upload it as a blob to Azure Storage, and then unzip it from the command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="4ceba-156">Caricare e gestire le applicazioni</span><span class="sxs-lookup"><span data-stu-id="4ceba-156">Upload and manage applications</span></span>
<span data-ttu-id="4ceba-157">È possibile usare il [portale di Azure][portal] o la libreria [di gestione .NET per Batch](batch-management-dotnet.md) per gestire i pacchetti dell'applicazione nell'account Batch.</span><span class="sxs-lookup"><span data-stu-id="4ceba-157">You can use the [Azure portal][portal] or the [Batch Management .NET](batch-management-dotnet.md) library to manage the application packages in your Batch account.</span></span> <span data-ttu-id="4ceba-158">Nelle sezioni successive verrà prima di tutto mostrato come collegare un account di archiviazione, quindi verrà descritta l'aggiunta di applicazioni e di pacchetti e la loro gestione con il portale.</span><span class="sxs-lookup"><span data-stu-id="4ceba-158">In the next few sections, we first show how to link a Storage account, then discuss adding applications and packages and managing them with the portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="4ceba-159">Collegare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4ceba-159">Link a Storage account</span></span>
<span data-ttu-id="4ceba-160">Per usare i pacchetti dell'applicazione, è prima necessario collegare un account di archiviazione di Azure all'account Batch.</span><span class="sxs-lookup"><span data-stu-id="4ceba-160">To use application packages, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="4ceba-161">Se non è stato ancora configurato un account di archiviazione, il portale di Azure visualizza un avviso nel momento in cui si seleziona per la prima volta il riquadro **Applicazioni** nel pannello **account Batch**.</span><span class="sxs-lookup"><span data-stu-id="4ceba-161">If you have not yet configured a Storage account, the Azure portal displays a warning the first time you click the **Applications** tile in the **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ceba-162">Batch supporta attualmente *solo* account di archiviazione **per uso generico**, come descritto nel passaggio 5, [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account), dell'articolo [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="4ceba-162">Batch currently supports *only* the **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="4ceba-163">Quando si collega un account di archiviazione di Azure all'account Batch, collegare *solo* un account di archiviazione **per uso generico**.</span><span class="sxs-lookup"><span data-stu-id="4ceba-163">When you link an Azure Storage account to your Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="4ceba-164">!['Nessun account di archiviazione configurato' nel portale di Azure][9]</span><span class="sxs-lookup"><span data-stu-id="4ceba-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="4ceba-165">Il servizio Batch usa l'account di archiviazione associato per archiviare i pacchetti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-165">The Batch service uses the associated Storage account to store your application packages.</span></span> <span data-ttu-id="4ceba-166">Dopo aver collegato i due account, Batch può distribuire automaticamente i pacchetti archiviati nell'account di archiviazione collegato nei nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="4ceba-166">After you've linked the two accounts, Batch can automatically deploy the packages stored in the linked Storage account to your compute nodes.</span></span> <span data-ttu-id="4ceba-167">Per collegare un account di archiviazione a un account Batch selezionare **Impostazioni account di archiviazione** nel pannello **Avviso** e quindi fare clic su **Account di archiviazione** nel pannello **Account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="4ceba-167">To link a Storage account to your Batch account, click **Storage account settings** on the **Warning** blade, and then click **Storage Account** on the **Storage Account** blade.</span></span>

<span data-ttu-id="4ceba-168">![Selezionare il pannello Account di archiviazione nel portale di Azure][10]</span><span class="sxs-lookup"><span data-stu-id="4ceba-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="4ceba-169">È consigliabile creare un account di archiviazione da usare *specificamente* con l'account Batch e selezionarlo qui.</span><span class="sxs-lookup"><span data-stu-id="4ceba-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="4ceba-170">Per informazioni dettagliate sulla creazione di un account di archiviazione, vedere "Creare un account di archiviazione" in [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="4ceba-170">For details about how to create a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="4ceba-171">Dopo aver creato un account di archiviazione, è possibile collegarlo all'account Batch tramite il pannello **Account di archiviazione** .</span><span class="sxs-lookup"><span data-stu-id="4ceba-171">After you've created a Storage account, you can then link it to your Batch account by using the **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="4ceba-172">Il servizio Batch usa Archiviazione di Azure per archiviare i pacchetti dell'applicazione come BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="4ceba-172">The Batch service uses Azure Storage to store your application packages as block blobs.</span></span> <span data-ttu-id="4ceba-173">L'[importo addebitato] [ storage_pricing] sarà lo stesso calcolato per i dati BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="4ceba-173">You are [charged as normal][storage_pricing] for the block blob data.</span></span> <span data-ttu-id="4ceba-174">Controllare la dimensione e il numero dei pacchetti dell'applicazione e rimuovere periodicamente i pacchetti obsoleti per ridurre al minimo il costo.</span><span class="sxs-lookup"><span data-stu-id="4ceba-174">Be sure to consider the size and number of your application packages, and periodically remove deprecated packages to minimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="4ceba-175">Visualizzare le applicazioni correnti</span><span class="sxs-lookup"><span data-stu-id="4ceba-175">View current applications</span></span>
<span data-ttu-id="4ceba-176">Per visualizzare le applicazioni nell'account Batch, fare clic sulla voce **Applicazioni** nel menu di sinistra mentre il pannello **Account Batch** è aperto.</span><span class="sxs-lookup"><span data-stu-id="4ceba-176">To view the applications in your Batch account, click the **Applications** menu item in the left menu while viewing the **Batch account** blade.</span></span>

<span data-ttu-id="4ceba-177">![Riquadro Applicazioni][2]</span><span class="sxs-lookup"><span data-stu-id="4ceba-177">![Applications tile][2]</span></span>

<span data-ttu-id="4ceba-178">Selezionando questa opzione di menu viene visualizzato il pannello **Applicazioni**:</span><span class="sxs-lookup"><span data-stu-id="4ceba-178">Selecting this menu option opens the **Applications** blade:</span></span>

<span data-ttu-id="4ceba-179">![Elenco applicazioni][3]</span><span class="sxs-lookup"><span data-stu-id="4ceba-179">![List applications][3]</span></span>

<span data-ttu-id="4ceba-180">Nel pannello **Applicazioni** vengono visualizzati l'ID di ogni applicazione nell'account e le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ceba-180">The **Applications** blade displays the ID of each application in your account and the following properties:</span></span>

* <span data-ttu-id="4ceba-181">**Pacchetti**: il numero delle versioni associate a questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-181">**Packages**: The number of versions associated with this application.</span></span>
* <span data-ttu-id="4ceba-182">**Versione predefinita**: la versione dell'applicazione che verrà installata se non si indica una versione quando si specifica l'applicazione per un pool.</span><span class="sxs-lookup"><span data-stu-id="4ceba-182">**Default version**: The application version installed if you do not indicate a version when you specify the application for a pool.</span></span> <span data-ttu-id="4ceba-183">Questa impostazione è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="4ceba-183">This setting is optional.</span></span>
* <span data-ttu-id="4ceba-184">**Consenti aggiornamenti**: il valore che specifica se sono consentiti aggiornamenti, eliminazioni e aggiunte per il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4ceba-184">**Allow updates**: The value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="4ceba-185">Se l'opzione è impostata su **No**, gli aggiornamenti del pacchetto e le eliminazioni sono disabilitate per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-185">If this is set to **No**, package updates and deletions are disabled for the application.</span></span> <span data-ttu-id="4ceba-186">È possibile aggiungere solo nuove versioni del pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-186">Only new application package versions can be added.</span></span> <span data-ttu-id="4ceba-187">Il valore predefinito è **Sì**.</span><span class="sxs-lookup"><span data-stu-id="4ceba-187">The default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="4ceba-188">Visualizzare i dettagli dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="4ceba-188">View application details</span></span>
<span data-ttu-id="4ceba-189">Per aprire il pannello che include i dettagli dell'applicazione, selezionare l'applicazione nel pannello **Applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="4ceba-189">To open the blade that includes the details for an application, select the application in the **Applications** blade.</span></span>

<span data-ttu-id="4ceba-190">![Dettagli applicazione][4]</span><span class="sxs-lookup"><span data-stu-id="4ceba-190">![Application details][4]</span></span>

<span data-ttu-id="4ceba-191">Nel pannello dei dettagli dell'applicazione, è possibile configurare le impostazioni seguenti per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-191">In the application details blade, you can configure the following settings for your application.</span></span>

* <span data-ttu-id="4ceba-192">**Consenti aggiornamenti**: specificare se i pacchetti dell'applicazione possono essere aggiornati o eliminati.</span><span class="sxs-lookup"><span data-stu-id="4ceba-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="4ceba-193">Vedere "Aggiornare o eliminare un pacchetto dell'applicazione" più avanti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="4ceba-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="4ceba-194">**Versione predefinita**: specificare un pacchetto dell'applicazione predefinito da distribuire nei nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="4ceba-194">**Default version**: Specify a default application package to deploy to compute nodes.</span></span>
* <span data-ttu-id="4ceba-195">**Nome visualizzato**: si tratta di un nome descrittivo che la soluzione Batch può usare per visualizzare informazioni sull'applicazione, ad esempio nell'interfaccia utente di un servizio offerto ai clienti tramite Batch.</span><span class="sxs-lookup"><span data-stu-id="4ceba-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about the application, for example, in the UI of a service that you provide to your customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="4ceba-196">Aggiungere un’applicazione nuova</span><span class="sxs-lookup"><span data-stu-id="4ceba-196">Add a new application</span></span>
<span data-ttu-id="4ceba-197">Per creare un'applicazione nuova, aggiungere un pacchetto dell'applicazione usando un ID applicazione nuovo e univoco.</span><span class="sxs-lookup"><span data-stu-id="4ceba-197">To create a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="4ceba-198">Il primo pacchetto dell'applicazione aggiunto usando il nuovo ID applicazione crea anche la nuova applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-198">The first application package that you add with the new application ID also creates the new application.</span></span>

<span data-ttu-id="4ceba-199">Fare clic su **Aggiungi** nel pannello **Applicazioni** per aprire il pannello **Nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="4ceba-199">Click **Add** on the **Applications** blade to open the **New application** blade.</span></span>

<span data-ttu-id="4ceba-200">![Pannello Nuova applicazione nel portale di Azure][5]</span><span class="sxs-lookup"><span data-stu-id="4ceba-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="4ceba-201">Il pannello **Nuova applicazione** contiene i campi seguenti per specificare le impostazioni della nuova applicazione e del pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-201">The **New application** blade provides the following fields to specify the settings of your new application and application package.</span></span>

<span data-ttu-id="4ceba-202">**ID applicazione**</span><span class="sxs-lookup"><span data-stu-id="4ceba-202">**Application id**</span></span>

<span data-ttu-id="4ceba-203">Questo campo specifica l'ID della nuova applicazione, che è soggetto alle regole standard di convalida dell'ID di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="4ceba-203">This field specifies the ID of your new application, which is subject to the standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="4ceba-204">Di seguito sono riportate le regole per fornire un ID applicazione:</span><span class="sxs-lookup"><span data-stu-id="4ceba-204">The rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="4ceba-205">Nei nodi di Windows, l'ID può contenere qualsiasi combinazione di caratteri alfanumerici, trattini e caratteri di sottolineatura.</span><span class="sxs-lookup"><span data-stu-id="4ceba-205">On Windows nodes, the ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="4ceba-206">Nei nodi di Linux, sono consentiti solo caratteri alfanumerici e caratteri di sottolineatura.</span><span class="sxs-lookup"><span data-stu-id="4ceba-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="4ceba-207">Non può contenere più di 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="4ceba-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="4ceba-208">Deve essere univoco nell’account Batch.</span><span class="sxs-lookup"><span data-stu-id="4ceba-208">Must be unique within the Batch account.</span></span>
* <span data-ttu-id="4ceba-209">Mantiene le maiuscole/minuscole e non fa distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="4ceba-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="4ceba-210">**Versione**</span><span class="sxs-lookup"><span data-stu-id="4ceba-210">**Version**</span></span>

<span data-ttu-id="4ceba-211">Questo campo specifica la versione del pacchetto dell'applicazione che si sta caricando.</span><span class="sxs-lookup"><span data-stu-id="4ceba-211">This field specifies the version of the application package you are uploading.</span></span> <span data-ttu-id="4ceba-212">Le stringhe della versione sono soggette alle regole di convalida seguenti:</span><span class="sxs-lookup"><span data-stu-id="4ceba-212">Version strings are subject to the following validation rules:</span></span>

* <span data-ttu-id="4ceba-213">Nei nodi di Windows la stringa di versione può contenere qualsiasi combinazione di caratteri alfanumerici, trattini, caratteri di sottolineatura e punti.</span><span class="sxs-lookup"><span data-stu-id="4ceba-213">On Windows nodes, the version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="4ceba-214">Nei nodi di Linux, la stringa di versione può contenere solo caratteri alfanumerici e caratteri di sottolineatura.</span><span class="sxs-lookup"><span data-stu-id="4ceba-214">On Linux nodes, the version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="4ceba-215">Non può contenere più di 64 caratteri.</span><span class="sxs-lookup"><span data-stu-id="4ceba-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="4ceba-216">Devono essere univoche nell’applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-216">Must be unique within the application.</span></span>
* <span data-ttu-id="4ceba-217">Mantengono le maiuscole/minuscole e non fanno distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="4ceba-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="4ceba-218">**Pacchetto dell'applicazione**</span><span class="sxs-lookup"><span data-stu-id="4ceba-218">**Application package**</span></span>

<span data-ttu-id="4ceba-219">Questo campo specifica il file ZIP contenente i file binari e i file di supporto dell'applicazione necessari per l'esecuzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-219">This field specifies the .zip file that contains the application binaries and supporting files that are required to execute the application.</span></span> <span data-ttu-id="4ceba-220">Fare clic sulla casella **Selezionare un file** oppure sull'icona della cartella per cercare e selezionare un file ZIP contenente i file dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-220">Click the **Select a file** box or the folder icon to browse to and select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="4ceba-221">Dopo aver selezionato un file, fare clic su **OK** per avviare il caricamento in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ceba-221">After you've selected a file, click **OK** to begin the upload to Azure Storage.</span></span> <span data-ttu-id="4ceba-222">Una volta completata l'operazione di caricamento, il portale visualizza una notifica e chiude il pannello.</span><span class="sxs-lookup"><span data-stu-id="4ceba-222">When the upload operation is complete, the portal displays a notification and closes the blade.</span></span> <span data-ttu-id="4ceba-223">A seconda delle dimensioni del file che si sta caricando e della velocità della connessione di rete, l'operazione potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="4ceba-223">Depending on the size of the file that you are uploading and the speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="4ceba-224">Non chiudere il pannello **Nuova applicazione** prima che l'operazione di caricamento sia terminata,</span><span class="sxs-lookup"><span data-stu-id="4ceba-224">Do not close the **New application** blade before the upload operation is complete.</span></span> <span data-ttu-id="4ceba-225">altrimenti il processo di caricamento sarà interrotto.</span><span class="sxs-lookup"><span data-stu-id="4ceba-225">Doing so will stop the upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="4ceba-226">Aggiungere un nuovo pacchetto dell’applicazione</span><span class="sxs-lookup"><span data-stu-id="4ceba-226">Add a new application package</span></span>
<span data-ttu-id="4ceba-227">Per aggiungere una nuova versione del pacchetto dell'applicazione per un'applicazione esistente, selezionare un'applicazione nel pannello **Applicazioni**, fare clic su **Pacchetti** e quindi su **Aggiungi** per visualizzare il pannello **Aggiungi pacchetto**.</span><span class="sxs-lookup"><span data-stu-id="4ceba-227">To add a new application package version for an existing application, select an application in the **Applications** blade, click **Packages**, then click **Add** to open the **Add package** blade.</span></span>

<span data-ttu-id="4ceba-228">![Pannello per aggiungere un pacchetto dell'applicazione nel portale di Azure][8]</span><span class="sxs-lookup"><span data-stu-id="4ceba-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="4ceba-229">Come si può notare, i campi corrispondono a quelli del pannello **Nuova applicazione**, ad eccezione della casella **ID applicazione** che è disabilitata.</span><span class="sxs-lookup"><span data-stu-id="4ceba-229">As you can see, the fields match those of the **New application** blade, but the **Application id** box is disabled.</span></span> <span data-ttu-id="4ceba-230">Come è stato fatto per la nuova applicazione, specificare la **versione** del nuovo pacchetto, scegliere il file ZIP del **pacchetto dell'applicazione** e quindi fare clic su **OK** per caricare il pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4ceba-230">As you did for the new application, specify the **Version** for your new package, browse to your **Application package** .zip file, then click **OK** to upload the package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="4ceba-231">Aggiornare o eliminare un pacchetto dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="4ceba-231">Update or delete an application package</span></span>
<span data-ttu-id="4ceba-232">Per aggiornare o eliminare un pacchetto dell'applicazione esistente, aprire il pannello dei dettagli relativo all'applicazione, fare clic su **Pacchetti** per visualizzare il pannello **Pacchetti**, fare clic sui **puntini di sospensione** nella riga del pacchetto dell'applicazione che si vuole modificare e quindi selezionare l'azione da eseguire.</span><span class="sxs-lookup"><span data-stu-id="4ceba-232">To update or delete an existing application package, open the details blade for the application, click **Packages** to open the **Packages** blade, click the **ellipsis** in the row of the application package that you want to modify, and select the action that you want to perform.</span></span>

<span data-ttu-id="4ceba-233">![Aggiornare o eliminare un pacchetto nel portale di Azure][7]</span><span class="sxs-lookup"><span data-stu-id="4ceba-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="4ceba-234">**Aggiornare**</span><span class="sxs-lookup"><span data-stu-id="4ceba-234">**Update**</span></span>

<span data-ttu-id="4ceba-235">Se si seleziona **Aggiorna**, verrà visualizzato il pannello *Aggiorna pacchetto*.</span><span class="sxs-lookup"><span data-stu-id="4ceba-235">When you click **Update**, the *Update package* blade is displayed.</span></span> <span data-ttu-id="4ceba-236">Questo pannello è simile al pannello usato per creare un *nuovo pacchetto dell'applicazione*. In questo caso, però, è abilitato solo il campo di selezione del pacchetto, in cui è possibile specificare un nuovo file ZIP da caricare.</span><span class="sxs-lookup"><span data-stu-id="4ceba-236">This blade is similar to the *New application package* blade, however only the package selection field is enabled, allowing you to specify a new ZIP file to upload.</span></span>

<span data-ttu-id="4ceba-237">![Pannello per aggiornare un pacchetto nel portale di Azure][11]</span><span class="sxs-lookup"><span data-stu-id="4ceba-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="4ceba-238">**Eliminazione**</span><span class="sxs-lookup"><span data-stu-id="4ceba-238">**Delete**</span></span>

<span data-ttu-id="4ceba-239">Se si seleziona **Elimina**, verrà chiesto di confermare l'eliminazione della versione del pacchetto e Batch eliminerà il pacchetto da Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4ceba-239">When you click **Delete**, you are asked to confirm the deletion of the package version, and Batch deletes the package from Azure Storage.</span></span> <span data-ttu-id="4ceba-240">Se si elimina la versione predefinita di un'applicazione, verrà rimossa l'impostazione **Versione predefinita** per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-240">If you delete the default version of an application, the **Default version** setting is removed for the application.</span></span>

<span data-ttu-id="4ceba-241">![Eliminare un'applicazione ][12]</span><span class="sxs-lookup"><span data-stu-id="4ceba-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="4ceba-242">Installare le applicazioni su nodi di calcolo</span><span class="sxs-lookup"><span data-stu-id="4ceba-242">Install applications on compute nodes</span></span>
<span data-ttu-id="4ceba-243">Dopo aver appreso come gestire i pacchetti dell'applicazione con il portale di Azure, verrà ora descritta la distribuzione dei pacchetti nei nodi di calcolo e la relativa esecuzione con attività di Batch.</span><span class="sxs-lookup"><span data-stu-id="4ceba-243">Now that you've learned how to manage application packages with the Azure portal, we can discuss how to deploy them to compute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="4ceba-244">Installare pacchetti dell'applicazione nel pool</span><span class="sxs-lookup"><span data-stu-id="4ceba-244">Install pool application packages</span></span>
<span data-ttu-id="4ceba-245">Per installare un pacchetto dell'applicazione in tutti i nodi di calcolo di un pool, specificare uno o più *riferimenti* al pacchetto dell'applicazione per il pool.</span><span class="sxs-lookup"><span data-stu-id="4ceba-245">To install an application package on all compute nodes in a pool, specify one or more application package *references* for the pool.</span></span> <span data-ttu-id="4ceba-246">I pacchetti dell'applicazione specificati per un pool vengono installati su ciascun nodo di calcolo quando tale nodo viene aggiunto al pool e quando il nodo viene riavviato o ne viene ricreata l'immagine.</span><span class="sxs-lookup"><span data-stu-id="4ceba-246">The application packages that you specify for a pool are installed on each compute node when that node joins the pool, and when the node is rebooted or reimaged.</span></span>

<span data-ttu-id="4ceba-247">In Batch .NET specificare uno o più [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] quando si crea un nuovo pool oppure aggiungerli al pool esistente.</span><span class="sxs-lookup"><span data-stu-id="4ceba-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="4ceba-248">La classe [ApplicationPackageReference][net_pkgref] specifica un ID applicazione e la versione da installare nei nodi di calcolo di un pool.</span><span class="sxs-lookup"><span data-stu-id="4ceba-248">The [ApplicationPackageReference][net_pkgref] class specifies an application ID and version to install on a pool's compute nodes.</span></span>

```csharp
// Create the unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify the application and version to install on the compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit the pool so that it's created in the Batch service. As the nodes join
// the pool, the specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="4ceba-249">Se una distribuzione del pacchetto dell'applicazione non riesce, il servizio Batch contrassegna il nodo come [inutilizzabile][net_nodestate] e non vengono pianificate attività per l'esecuzione in tale nodo.</span><span class="sxs-lookup"><span data-stu-id="4ceba-249">If an application package deployment fails for any reason, the Batch service marks the node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="4ceba-250">In questo caso è necessario **riavviare** il nodo per reinizializzare la distribuzione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4ceba-250">In this case, you should **restart** the node to reinitiate the package deployment.</span></span> <span data-ttu-id="4ceba-251">Il riavvio del nodo consente anche di pianificarne di nuovo le attività.</span><span class="sxs-lookup"><span data-stu-id="4ceba-251">Restarting the node also enables task scheduling again on the node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="4ceba-252">Installare pacchetti dell'applicazione per le attività</span><span class="sxs-lookup"><span data-stu-id="4ceba-252">Install task application packages</span></span>
<span data-ttu-id="4ceba-253">Come per un pool, specificare i *riferimenti* del pacchetto dell'applicazione per un'attività.</span><span class="sxs-lookup"><span data-stu-id="4ceba-253">Similar to a pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="4ceba-254">Quando un'attività è pianificata per l'esecuzione su un nodo, il pacchetto viene scaricato ed estratto appena prima dell'esecuzione della riga di comando dell'attività.</span><span class="sxs-lookup"><span data-stu-id="4ceba-254">When a task is scheduled to run on a node, the package is downloaded and extracted just before the task's command line is executed.</span></span> <span data-ttu-id="4ceba-255">Se un pacchetto specificato con la versione corrispondente è già installato nel nodo, non verrà scaricato e verrà usato il pacchetto esistente.</span><span class="sxs-lookup"><span data-stu-id="4ceba-255">If a specified package and version is already installed on the node, the package is not downloaded and the existing package is used.</span></span>

<span data-ttu-id="4ceba-256">Per installare un pacchetto dell'applicazione per le attività, configurare la proprietà [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] dell'attività:</span><span class="sxs-lookup"><span data-stu-id="4ceba-256">To install a task application package, configure the task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

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

## <a name="execute-the-installed-applications"></a><span data-ttu-id="4ceba-257">Eseguire le applicazioni installate</span><span class="sxs-lookup"><span data-stu-id="4ceba-257">Execute the installed applications</span></span>
<span data-ttu-id="4ceba-258">I pacchetti specificati per un pool o un'attività vengono scaricati ed estratti in una directory denominata all'interno del nodo `AZ_BATCH_ROOT_DIR` .</span><span class="sxs-lookup"><span data-stu-id="4ceba-258">The packages that you've specified for a pool or task are downloaded and extracted to a named directory within the `AZ_BATCH_ROOT_DIR` of the node.</span></span> <span data-ttu-id="4ceba-259">Batch crea anche una variabile di ambiente che contiene il percorso della directory denominata.</span><span class="sxs-lookup"><span data-stu-id="4ceba-259">Batch also creates an environment variable that contains the path to the named directory.</span></span> <span data-ttu-id="4ceba-260">Le righe di comando dell'attività usano questa variabile di ambiente quando fanno riferimento all'applicazione nel nodo.</span><span class="sxs-lookup"><span data-stu-id="4ceba-260">Your task command lines use this environment variable when referencing the application on the node.</span></span> 

<span data-ttu-id="4ceba-261">Nei nodi di Windows la variabile è nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="4ceba-261">On Windows nodes, the variable is in the following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="4ceba-262">Nei nodi di Linux, il formato è leggermente diverso.</span><span class="sxs-lookup"><span data-stu-id="4ceba-262">On Linux nodes, the format is slightly different.</span></span> <span data-ttu-id="4ceba-263">Punti (.), trattini (-) e simboli di cancelletto (#) vengono convertiti in caratteri di sottolineatura nella variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="4ceba-263">Periods (.), hypens (-) and number signs (#) are flattened to underscores in the environment variable.</span></span> <span data-ttu-id="4ceba-264">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4ceba-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="4ceba-265">`APPLICATIONID` e `version` sono valori che corrispondono all'applicazione e alla versione del pacchetto specificati per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-265">`APPLICATIONID` and `version` are values that correspond to the application and package version you've specified for deployment.</span></span> <span data-ttu-id="4ceba-266">Se ad esempio si specifica l'installazione della versione 2.7 dell'applicazione *blender* nei nodi di Windows, le righe di comando dell'attività useranno questa variabile di ambiente per accedere ai file corrispondenti:</span><span class="sxs-lookup"><span data-stu-id="4ceba-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable to access its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="4ceba-267">Nei nodi di Linux, specificare la variabile di ambiente nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="4ceba-267">On Linux nodes, specify the environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="4ceba-268">Quando si carica un pacchetto dell'applicazione, è possibile specificare una versione predefinita da distribuire ai nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="4ceba-268">When you upload an application package, you can specify a default version to deploy to your compute nodes.</span></span> <span data-ttu-id="4ceba-269">Se è stata specificata una versione predefinita per un'applicazione, è possibile omettere il suffisso della versione quando si fa riferimento l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-269">If you have specified a default version for an application, you can omit the version suffix when you reference the application.</span></span> <span data-ttu-id="4ceba-270">È possibile specificare la versione predefinita dell'applicazione nel pannello Applicazioni del portale di Azure, come illustrato in [Caricare e gestire le applicazioni](#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="4ceba-270">You can specify the default application version in the Azure portal, on the Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="4ceba-271">Se ad esempio è stata specificata la versione predefinita "2.7" per l'applicazione *blender* e le attività fanno riferimento alla variabile di ambiente seguente, i nodi di Windows eseguiranno la versione 2.7:</span><span class="sxs-lookup"><span data-stu-id="4ceba-271">For example, if you set "2.7" as the default version for application *blender*, and your tasks reference the following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="4ceba-272">Il frammento di codice seguente mostra una riga di comando dell'attività di esempio che consente di avviare la versione predefinita dell'applicazione *blender* :</span><span class="sxs-lookup"><span data-stu-id="4ceba-272">The following code snippet shows an example task command line that launches the default version of the *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="4ceba-273">Per altre informazioni sulle impostazioni dell'ambiente dei nodi di calcolo, vedere [Impostazioni di ambiente per le attività](batch-api-basics.md#environment-settings-for-tasks) in [Panoramica delle funzionalità di Batch per sviluppatori](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="4ceba-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in the [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="4ceba-274">Aggiornare i pacchetti dell’applicazione di un pool</span><span class="sxs-lookup"><span data-stu-id="4ceba-274">Update a pool's application packages</span></span>
<span data-ttu-id="4ceba-275">Se un pool esistente è già stato configurato con un pacchetto dell’applicazione, è possibile specificare un nuovo pacchetto per il pool.</span><span class="sxs-lookup"><span data-stu-id="4ceba-275">If an existing pool has already been configured with an application package, you can specify a new package for the pool.</span></span> <span data-ttu-id="4ceba-276">Se si specifica un nuovo riferimento al pacchetto per un pool, si applica quanto segue:</span><span class="sxs-lookup"><span data-stu-id="4ceba-276">If you specify a new package reference for a pool, the following apply:</span></span>

* <span data-ttu-id="4ceba-277">Il servizio Batch installa il pacchetto appena specificato su tutti i nuovi nodi aggiunti al pool e su tutti i nodi esistenti riavviati o per i quali viene ricreata l'immagine.</span><span class="sxs-lookup"><span data-stu-id="4ceba-277">The Batch service installs the newly specified package on all new nodes that join the pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="4ceba-278">I nodi di calcolo che si trovano già nel pool quando si aggiornano i riferimenti al pacchetto non installano automaticamente il nuovo pacchetto dell’applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-278">Compute nodes that are already in the pool when you update the package references do not automatically install the new application package.</span></span> <span data-ttu-id="4ceba-279">Questi nodi di calcolo devono essere riavviati o ne deve essere ricreata l'immagine per ricevere il nuovo pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4ceba-279">These compute nodes must be rebooted or reimaged to receive the new package.</span></span>
* <span data-ttu-id="4ceba-280">Quando viene distribuito un nuovo pacchetto, le variabili di ambiente create riflettono i riferimenti al nuovo pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-280">When a new package is deployed, the created environment variables reflect the new application package references.</span></span>

<span data-ttu-id="4ceba-281">In questo esempio il pool esistente ha la versione 2.7 dell'applicazione *blender* configurata come uno dei relativi [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span><span class="sxs-lookup"><span data-stu-id="4ceba-281">In this example, the existing pool has version 2.7 of the *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="4ceba-282">Per aggiornare i nodi del pool alla versione 2.76b, specificare un nuovo [ApplicationPackageReference][net_pkgref] con la nuova versione ed eseguire il commit della modifica.</span><span class="sxs-lookup"><span data-stu-id="4ceba-282">To update the pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with the new version, and commit the change.</span></span>

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

<span data-ttu-id="4ceba-283">Ora che è stata configurata la nuova versione, il servizio Batch installa la versione 2.76b su qualsiasi *nuovo* nodo aggiunto al pool.</span><span class="sxs-lookup"><span data-stu-id="4ceba-283">Now that the new version has been configured, the Batch service installs version 2.76b to any *new* node that joins the pool.</span></span> <span data-ttu-id="4ceba-284">Per installare la versione 2.76b nei nodi *già* presenti nel pool, riavviarli o ricrearne l'immagine.</span><span class="sxs-lookup"><span data-stu-id="4ceba-284">To install 2.76b on the nodes that are *already* in the pool, reboot or reimage them.</span></span> <span data-ttu-id="4ceba-285">Notare che i nodi riavviati mantengono i file delle distribuzioni precedenti del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4ceba-285">Note that rebooted nodes retain the files from previous package deployments.</span></span>

## <a name="list-the-applications-in-a-batch-account"></a><span data-ttu-id="4ceba-286">Elencare le applicazioni in un account Batch</span><span class="sxs-lookup"><span data-stu-id="4ceba-286">List the applications in a Batch account</span></span>
<span data-ttu-id="4ceba-287">È possibile elencare le applicazioni e i relativi pacchetti in un account Batch con il metodo [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries].</span><span class="sxs-lookup"><span data-stu-id="4ceba-287">You can list the applications and their packages in a Batch account by using the [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List the applications and their application packages in the Batch account.
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

## <a name="wrap-up"></a><span data-ttu-id="4ceba-288">Eseguire il wrapping</span><span class="sxs-lookup"><span data-stu-id="4ceba-288">Wrap up</span></span>
<span data-ttu-id="4ceba-289">Con i pacchetti dell'applicazione è possibile assistere i clienti nella scelta delle applicazioni per i loro processi e specificare la versione corretta da usare durante l'elaborazione dei processi con il servizio abilitato per Batch.</span><span class="sxs-lookup"><span data-stu-id="4ceba-289">With application packages, you can help your customers select the applications for their jobs and specify the exact version to use when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="4ceba-290">I clienti possono inoltre caricare e monitorare le applicazioni usate nel servizio.</span><span class="sxs-lookup"><span data-stu-id="4ceba-290">You might also provide the ability for your customers to upload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ceba-291">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4ceba-291">Next steps</span></span>
* <span data-ttu-id="4ceba-292">L'[API REST Batch][api_rest] consente anche di usare i pacchetti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4ceba-292">The [Batch REST API][api_rest] also provides support to work with application packages.</span></span> <span data-ttu-id="4ceba-293">Per informazioni su come specificare i pacchetti da installare con l'API REST, vedere ad esempio l'elemento [applicationPackageReferences][rest_add_pool_with_packages] in [Aggiungere un pool a un account][rest_add_pool].</span><span class="sxs-lookup"><span data-stu-id="4ceba-293">For example, see the [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool to an account][rest_add_pool] for information about how to specify packages to install by using the REST API.</span></span> <span data-ttu-id="4ceba-294">Per dettagli su come ottenere informazioni sull'applicazione con l'API REST Batch, vedere [Applicazioni][rest_applications].</span><span class="sxs-lookup"><span data-stu-id="4ceba-294">See [Applications][rest_applications] for details about how to obtain application information by using the Batch REST API.</span></span>
* <span data-ttu-id="4ceba-295">È possibile scoprire come [gestire quote e account Azure Batch con la gestione .NET per Batch](batch-management-dotnet.md)a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="4ceba-295">Learn how to programmatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="4ceba-296">Con la libreria di [gestione .NET per Batch][api_net_mgmt] è possibile abilitare funzionalità di creazione ed eliminazione di account per l'applicazione o il servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="4ceba-296">The [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

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
