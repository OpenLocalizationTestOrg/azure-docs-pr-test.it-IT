---
title: "Capacità dedicata per i processi del servizio di esecuzione Batch di Machine Learning | Documentazione Microsoft"
description: Panoramica dei servizi di Azure Batch per i processi di Machine Learning.
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 3879eb3d0c6fa9d74fff01b07f5c07d3991dfbbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="45de6-103">Servizio Azure Batch per i processi di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="45de6-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="45de6-104">L'elaborazione di pool di Batch in Machine Learning fornisce la scalabilità gestita dal cliente per il servizio di esecuzione Batch di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="45de6-104">Machine Learning Batch Pool processing provides customer-managed scale for the Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="45de6-105">L'elaborazione batch classica per l'apprendimento automatico avviene in un ambiente multi-tenant, limitando il numero di processi simultanei che è possibile inviare, e i processi vengono accodati in base alla modalità First-In-First-Out.</span><span class="sxs-lookup"><span data-stu-id="45de6-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits the number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="45de6-106">Non è quindi possibile prevedere con precisione quando verrà eseguito il processo.</span><span class="sxs-lookup"><span data-stu-id="45de6-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="45de6-107">L'elaborazione di pool di Batch consente di creare pool a cui è possibile inviare i processi batch.</span><span class="sxs-lookup"><span data-stu-id="45de6-107">Batch Pool processing allows you to create pools on which you can submit batch jobs.</span></span> <span data-ttu-id="45de6-108">Vengono controllati le dimensioni del pool e il pool specifico a cui viene inviato il processo.</span><span class="sxs-lookup"><span data-stu-id="45de6-108">You control the size of the pool, and to which pool the job is submitted.</span></span> <span data-ttu-id="45de6-109">Il processo BES viene eseguito nel proprio spazio di elaborazione, assicurando prestazioni di elaborazione prevedibili e la possibilità di creare pool di risorse corrispondenti al carico di elaborazione inviato.</span><span class="sxs-lookup"><span data-stu-id="45de6-109">Your BES job runs in its own processing space providing predictable processing performance and the ability to create resource pools that correspond to the processing load that you submit.</span></span>

## <a name="how-to-use-batch-pool-processing"></a><span data-ttu-id="45de6-110">Procedura: Usare l'elaborazione di pool Batch</span><span class="sxs-lookup"><span data-stu-id="45de6-110">How to use Batch Pool processing</span></span>

<span data-ttu-id="45de6-111">La configurazione dell'elaborazione di pool di Batch non è attualmente disponibile tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="45de6-111">Configuration of Batch Pool Processing is not currently available through the Azure portal.</span></span> <span data-ttu-id="45de6-112">Per usare l'elaborazione di pool di Batch, è necessario:</span><span class="sxs-lookup"><span data-stu-id="45de6-112">To use Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="45de6-113">Chiamare CSS per creare un account di pool di Batch e ottenere un URL del servizio pool e una chiave di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="45de6-113">Call CSS to create a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="45de6-114">Creare un nuovo servizio Web e un nuovo piano di fatturazione basati su Resource Manager</span><span class="sxs-lookup"><span data-stu-id="45de6-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="45de6-115">Per creare il proprio account, contattare il Supporto tecnico Microsoft e fornire l'ID di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="45de6-115">To create your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="45de6-116">Il personale è a disposizione per aiutare a determinare la capacità necessaria per lo scenario in uso.</span><span class="sxs-lookup"><span data-stu-id="45de6-116">CSS will work with you to determine the appropriate capacity for your scenario.</span></span> <span data-ttu-id="45de6-117">Configurerà quindi l'account con il numero massimo di pool che è possibile creare e il numero massimo di macchine virtuali (VM) che è possibile inserire in ogni pool.</span><span class="sxs-lookup"><span data-stu-id="45de6-117">CSS then configures your account with the maximum number of pools you can create and the maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="45de6-118">Al termine della configurazione dell'account viene fornito l'URL del servizio pool e una chiave di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="45de6-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="45de6-119">Dopo avere creato l'account, usare l'URL del servizio pool e la chiave di autorizzazione per eseguire le operazioni di gestione del pool sul pool Batch.</span><span class="sxs-lookup"><span data-stu-id="45de6-119">After your account is created, you use the Pool Service URL and authorization key to perform pool management operations on your Batch Pool.</span></span>

![Architettura del servizio pool Batch.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="45de6-121">Creare i pool chiamando l'operazione di creazione dei pool per l'URL del servizio pool fornito dal Supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="45de6-121">You create pools by calling the Create Pool operation on the pool service URL that CSS provided to you.</span></span> <span data-ttu-id="45de6-122">Quando si crea un pool, specificare il numero di VM e l'URL del file swagger.json di un nuovo servizio Web di Machine Learning basato su Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="45de6-122">When you create a pool, specify the number of VMs and the URL of the swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="45de6-123">Questo servizio Web viene fornito per definire l'associazione al piano di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="45de6-123">This web service is provided to establish the billing association.</span></span> <span data-ttu-id="45de6-124">ll servizio pool Batch usa il file swagger.json per associare il pool a un piano di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="45de6-124">The Batch Pool service uses the swagger.json to associate the pool with a billing plan.</span></span> <span data-ttu-id="45de6-125">È possibile eseguire qualsiasi servizio Web BES scelto per il pool: quello nuovo basato su Resource Manager o quello classico.</span><span class="sxs-lookup"><span data-stu-id="45de6-125">You can run any BES web service, both New Resource Manager based and classic, you choose on the pool.</span></span>

<span data-ttu-id="45de6-126">È possibile usare qualsiasi nuovo servizio Web basato su Resource Manager, ma tenere presente che la fatturazione per i processi viene addebitata in base al piano di fatturazione associato al servizio scelto.</span><span class="sxs-lookup"><span data-stu-id="45de6-126">You can use any New Resource Manager based web service, but be aware that the billing for the jobs are charged against the billing plan associated with that service.</span></span> <span data-ttu-id="45de6-127">È consigliabile creare un servizio Web e un nuovo piano di fatturazione specifici per l'esecuzione dei processi di pool Batch.</span><span class="sxs-lookup"><span data-stu-id="45de6-127">You may want to create a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="45de6-128">Per altre informazioni sulla creazione di servizi Web, vedere [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="45de6-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="45de6-129">Dopo avere creato un pool, si invia un processo BES usando l'URL delle richieste Batch per il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="45de6-129">Once you have created a pool, you submit the BES job using the Batch Requests URL for the web service.</span></span> <span data-ttu-id="45de6-130">È possibile scegliere di inviarlo a un pool o usare l'elaborazione batch classica.</span><span class="sxs-lookup"><span data-stu-id="45de6-130">You can choose to submit it to a pool or to classic batch processing.</span></span> <span data-ttu-id="45de6-131">Per inviare un processo a un pool Batch, aggiungere al corpo della richiesta di invio del processo il parametro seguente:</span><span class="sxs-lookup"><span data-stu-id="45de6-131">To submit a job to Batch Pool processing, you add the following parameter to the job submission request body:</span></span>

<span data-ttu-id="45de6-132">"AzureBatchPoolId":"&lt;ID pool&gt;"</span><span class="sxs-lookup"><span data-stu-id="45de6-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="45de6-133">Se non si aggiunge il parametro, il processo viene eseguito nell'ambiente di elaborazione classico.</span><span class="sxs-lookup"><span data-stu-id="45de6-133">If you do not add the parameter, the job is run in the classic batch process environment.</span></span> <span data-ttu-id="45de6-134">Se sono disponibili risorse per il pool, il processo viene avviato immediatamente.</span><span class="sxs-lookup"><span data-stu-id="45de6-134">If the pool has available resources, the job starts running immediately.</span></span> <span data-ttu-id="45de6-135">Se non sono disponibili risorse per il pool, il processo viene accodato fino a quando non diventa disponibile una risorsa.</span><span class="sxs-lookup"><span data-stu-id="45de6-135">If the pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="45de6-136">Se è necessario aumentare la capacità perché si raggiunge spesso la capacità massima dei pool, contattare il Supporto tecnico Microsoft e concordare un aumento delle quote.</span><span class="sxs-lookup"><span data-stu-id="45de6-136">If you find that you regularly reach the capacity of your pools, and you need increased capacity, you can call CSS and work with a representative to increase your quotas.</span></span>

<span data-ttu-id="45de6-137">Richiesta di esempio:</span><span class="sxs-lookup"><span data-stu-id="45de6-137">Example Request:</span></span>

<span data-ttu-id="45de6-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span><span class="sxs-lookup"><span data-stu-id="45de6-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span></span>

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="45de6-139">Considerazioni sull'elaborazione di pool Batch</span><span class="sxs-lookup"><span data-stu-id="45de6-139">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="45de6-140">L'elaborazione di pool Batch è un servizio fatturabile sempre attivo che deve essere associato a un piano di fatturazione basato su Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="45de6-140">Batch Pool Processing is an always-on billable service and that requires you to associate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="45de6-141">Verrà addebitato solo il numero di ore di calcolo in esecuzione nel pool, indipendentemente dal numero di processi eseguiti in questo periodo.</span><span class="sxs-lookup"><span data-stu-id="45de6-141">You are only billed for the number of compute hours the pool is running; regardless of the number of jobs run during that time pool.</span></span> <span data-ttu-id="45de6-142">Se si crea un pool, vengono addebitate le ore di calcolo di ogni macchina virtuale in essa contenuto fino all'eliminazione del pool, anche se non sono in esecuzione processi batch.</span><span class="sxs-lookup"><span data-stu-id="45de6-142">If you create a pool, you are billed for the compute hours of each virtual machine in the pool until the pool is deleted, even if no batch jobs are running in the pool.</span></span> <span data-ttu-id="45de6-143">La fatturazione per le macchine virtuali inizia con il completamento del provisioning e termina con l'eliminazione del batch.</span><span class="sxs-lookup"><span data-stu-id="45de6-143">Billing for the virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="45de6-144">È possibile usare uno dei piani disponibili nella [pagina relativa ai prezzi di Machine Learning](https://azure.microsoft.com/pricing/details/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="45de6-144">You can use any of the plans found on the [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="45de6-145">Esempio di fatturazione:</span><span class="sxs-lookup"><span data-stu-id="45de6-145">Billing example:</span></span>

<span data-ttu-id="45de6-146">Se si crea un pool Batch con 2 macchine virtuali e lo si elimina dopo 24 ore, al piano di fatturazione verranno addebitate 48 ore di calcolo, indipendentemente dal numero di processi eseguiti in questo periodo.</span><span class="sxs-lookup"><span data-stu-id="45de6-146">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="45de6-147">Se si crea un pool Batch con 4 macchine virtuali e lo si elimina dopo 12 ore, al piano di fatturazione verranno addebitate 48 ore di calcolo.</span><span class="sxs-lookup"><span data-stu-id="45de6-147">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="45de6-148">È consigliabile eseguire il polling dello stato del processo per determinare quando i processi sono stati completati.</span><span class="sxs-lookup"><span data-stu-id="45de6-148">We recommend that you poll the job status to determine when jobs complete.</span></span> <span data-ttu-id="45de6-149">Al termine dell'esecuzione di tutti i processi, chiamare l'operazione di ridimensionamento del pool per impostare il numero di macchine virtuali del pool a zero.</span><span class="sxs-lookup"><span data-stu-id="45de6-149">When all your jobs have finished running, call the Resize Pool operation to set the number of virtual machines in the pool to zero.</span></span> <span data-ttu-id="45de6-150">Se le risorse nel pool non sono sufficienti ed è necessario creare un nuovo pool, ad esempio per la fatturazione in base a un piano di fatturazione diverso, è possibile invece eliminare il pool al termine dell'elaborazione di tutti i processi.</span><span class="sxs-lookup"><span data-stu-id="45de6-150">If you are short on pool resources and you need to create a new pool, for example to bill against a different billing plan, you can delete the pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="45de6-151">**Usare l'elaborazione di pool Batch quando**</span><span class="sxs-lookup"><span data-stu-id="45de6-151">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="45de6-152">**Usare l'elaborazione di batch classica quando**</span><span class="sxs-lookup"><span data-stu-id="45de6-152">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="45de6-153">È necessario eseguire un numero elevato di processi</span><span class="sxs-lookup"><span data-stu-id="45de6-153">You need to run a large number of jobs</span></span><br><span data-ttu-id="45de6-154">Or</span><span class="sxs-lookup"><span data-stu-id="45de6-154">Or</span></span><br/><span data-ttu-id="45de6-155">È necessario che i processi vengano eseguiti immediatamente</span><span class="sxs-lookup"><span data-stu-id="45de6-155">You need to know that your jobs will run immediately</span></span><br/><span data-ttu-id="45de6-156">Or</span><span class="sxs-lookup"><span data-stu-id="45de6-156">Or</span></span><br/><span data-ttu-id="45de6-157">È necessario garantire la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="45de6-157">You need guaranteed throughput.</span></span> <span data-ttu-id="45de6-158">Ad esempio, è necessario eseguire alcuni processi in un determinato intervallo temporale e aumentare le risorse di calcolo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="45de6-158">For example, you need to run a number of jobs in a given time frame, and want to scale out your compute resources to meet your needs.</span></span>    | <span data-ttu-id="45de6-159">Si sta eseguendo un numero limitato di processi</span><span class="sxs-lookup"><span data-stu-id="45de6-159">You are running just a few jobs</span></span><br/><span data-ttu-id="45de6-160">e</span><span class="sxs-lookup"><span data-stu-id="45de6-160">And</span></span><br/> <span data-ttu-id="45de6-161">non è necessario che i processi vengano eseguiti immediatamente</span><span class="sxs-lookup"><span data-stu-id="45de6-161">You don’t need the jobs to run immediately</span></span> |
