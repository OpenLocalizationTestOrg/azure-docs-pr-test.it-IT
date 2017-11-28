---
title: "Capacità per i processi del servizio esecuzione Batch Machine Learning aaaDedicated | Documenti Microsoft"
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
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="0998a-103">Servizio Azure Batch per i processi di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0998a-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="0998a-104">L'elaborazione di Machine Learning Batch Pool fornisce scalabilità gestita dal cliente per hello servizio esecuzione Batch di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0998a-104">Machine Learning Batch Pool processing provides customer-managed scale for hello Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="0998a-105">Elaborazione per machine learning classico batch viene eseguito in un ambiente multi-tenant, il numero di hello limiti di processi simultanei, è possibile inviare e i processi viene messe in coda con cadenza first-in-first-out.</span><span class="sxs-lookup"><span data-stu-id="0998a-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits hello number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="0998a-106">Non è quindi possibile prevedere con precisione quando verrà eseguito il processo.</span><span class="sxs-lookup"><span data-stu-id="0998a-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="0998a-107">L'elaborazione di batch Pool consente toocreate pool in cui è possibile inviare i processi batch.</span><span class="sxs-lookup"><span data-stu-id="0998a-107">Batch Pool processing allows you toocreate pools on which you can submit batch jobs.</span></span> <span data-ttu-id="0998a-108">È possibile controllare le dimensioni di hello del pool di hello e toowhich pool hello processo viene inviato.</span><span class="sxs-lookup"><span data-stu-id="0998a-108">You control hello size of hello pool, and toowhich pool hello job is submitted.</span></span> <span data-ttu-id="0998a-109">Il processo di BES viene eseguito in proprio fornire spazio di elaborazione delle prestazioni di elaborazione stimabile e hello possibilità toocreate i pool di risorse che corrispondono a carico di elaborazione toohello inviati.</span><span class="sxs-lookup"><span data-stu-id="0998a-109">Your BES job runs in its own processing space providing predictable processing performance and hello ability toocreate resource pools that correspond toohello processing load that you submit.</span></span>

## <a name="how-toouse-batch-pool-processing"></a><span data-ttu-id="0998a-110">Come l'elaborazione Batch Pool toouse</span><span class="sxs-lookup"><span data-stu-id="0998a-110">How toouse Batch Pool processing</span></span>

<span data-ttu-id="0998a-111">Configurazione del Pool di elaborazione Batch non è attualmente disponibile tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0998a-111">Configuration of Batch Pool Processing is not currently available through hello Azure portal.</span></span> <span data-ttu-id="0998a-112">toouse Pool Batch l'elaborazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="0998a-112">toouse Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="0998a-113">Chiamare CSS toocreate un Account del Pool di Batch e ottenere un URL del servizio del Pool e una chiave di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="0998a-113">Call CSS toocreate a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="0998a-114">Creare un nuovo servizio Web e un nuovo piano di fatturazione basati su Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0998a-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="0998a-115">toocreate il tuo account, chiamare il servizio clienti e supporto tecnico e fornire l'ID sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="0998a-115">toocreate your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="0998a-116">CSS funziona con si toodetermine hello capacità per il proprio scenario.</span><span class="sxs-lookup"><span data-stu-id="0998a-116">CSS will work with you toodetermine hello appropriate capacity for your scenario.</span></span> <span data-ttu-id="0998a-117">CSS configura quindi l'account con numero massimo di hello di pool, è possibile creare e hello numero massimo di macchine virtuali (VM) che è possibile inserire in ciascun pool.</span><span class="sxs-lookup"><span data-stu-id="0998a-117">CSS then configures your account with hello maximum number of pools you can create and hello maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="0998a-118">Al termine della configurazione dell'account viene fornito l'URL del servizio pool e una chiave di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="0998a-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="0998a-119">Dopo aver creato l'account, utilizzare hello URL del servizio del Pool e l'autorizzazione tooperform chiave pool operazioni di gestione nel Pool di Batch.</span><span class="sxs-lookup"><span data-stu-id="0998a-119">After your account is created, you use hello Pool Service URL and authorization key tooperform pool management operations on your Batch Pool.</span></span>

![Architettura del servizio pool Batch.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="0998a-121">Creare pool chiamando l'operazione di creazione del Pool di hello all'URL di servizio del pool di hello che tooyou CSS fornito.</span><span class="sxs-lookup"><span data-stu-id="0998a-121">You create pools by calling hello Create Pool operation on hello pool service URL that CSS provided tooyou.</span></span> <span data-ttu-id="0998a-122">Quando si crea un pool, specificare il numero di hello di macchine virtuali e l'URL di hello di hello swagger di un nuovo gestore di risorse basato su servizio web Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0998a-122">When you create a pool, specify hello number of VMs and hello URL of hello swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="0998a-123">Questo servizio web viene fornito l'associazione di fatturazione hello tooestablish.</span><span class="sxs-lookup"><span data-stu-id="0998a-123">This web service is provided tooestablish hello billing association.</span></span> <span data-ttu-id="0998a-124">servizio del Pool di Batch di Hello utilizza hello swagger tooassociate hello pool con un piano di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="0998a-124">hello Batch Pool service uses hello swagger.json tooassociate hello pool with a billing plan.</span></span> <span data-ttu-id="0998a-125">È possibile eseguire qualsiasi BES entrambi nuovo gestore di risorse basato su servizio web e classico, si sceglie nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="0998a-125">You can run any BES web service, both New Resource Manager based and classic, you choose on hello pool.</span></span>

<span data-ttu-id="0998a-126">È possibile utilizzare qualsiasi servizio web basato su nuovo gestore di risorse, ma tenere presente che la fatturazione per i processi di hello hello vengano addebitati rispetto al piano di fatturazione hello associato al servizio.</span><span class="sxs-lookup"><span data-stu-id="0998a-126">You can use any New Resource Manager based web service, but be aware that hello billing for hello jobs are charged against hello billing plan associated with that service.</span></span> <span data-ttu-id="0998a-127">È progettato per l'esecuzione di processi Batch Pool toocreate un servizio web e fatturazione nuovo piano.</span><span class="sxs-lookup"><span data-stu-id="0998a-127">You may want toocreate a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="0998a-128">Per altre informazioni sulla creazione di servizi Web, vedere [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="0998a-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="0998a-129">Dopo aver creato un pool, si invia hello BES processo tramite hello Batch le richieste di URL per il servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="0998a-129">Once you have created a pool, you submit hello BES job using hello Batch Requests URL for hello web service.</span></span> <span data-ttu-id="0998a-130">È possibile scegliere toosubmit è tooa tooclassic o del pool di elaborazione di batch.</span><span class="sxs-lookup"><span data-stu-id="0998a-130">You can choose toosubmit it tooa pool or tooclassic batch processing.</span></span> <span data-ttu-id="0998a-131">toosubmit un'elaborazione Pool tooBatch, aggiungere hello seguendo il corpo della richiesta parametro toohello processo invio:</span><span class="sxs-lookup"><span data-stu-id="0998a-131">toosubmit a job tooBatch Pool processing, you add hello following parameter toohello job submission request body:</span></span>

<span data-ttu-id="0998a-132">"AzureBatchPoolId":"&lt;ID pool&gt;"</span><span class="sxs-lookup"><span data-stu-id="0998a-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="0998a-133">Se non si aggiunge il parametro hello, processo di hello viene eseguito nell'ambiente di elaborazione batch classico hello.</span><span class="sxs-lookup"><span data-stu-id="0998a-133">If you do not add hello parameter, hello job is run in hello classic batch process environment.</span></span> <span data-ttu-id="0998a-134">Se il pool di hello ha risorse disponibili, il processo di hello avvia immediatamente l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0998a-134">If hello pool has available resources, hello job starts running immediately.</span></span> <span data-ttu-id="0998a-135">Se il pool di hello non dispone di liberare le risorse, il processo viene accodato fino a quando non è disponibile una risorsa.</span><span class="sxs-lookup"><span data-stu-id="0998a-135">If hello pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="0998a-136">Se si ritiene che si raggiunge regolarmente i pool di capacità hello ed è necessario maggiore capacità, è possibile chiamare CSS e lavorare con un rappresentante tooincrease le quote.</span><span class="sxs-lookup"><span data-stu-id="0998a-136">If you find that you regularly reach hello capacity of your pools, and you need increased capacity, you can call CSS and work with a representative tooincrease your quotas.</span></span>

<span data-ttu-id="0998a-137">Richiesta di esempio:</span><span class="sxs-lookup"><span data-stu-id="0998a-137">Example Request:</span></span>

<span data-ttu-id="0998a-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span><span class="sxs-lookup"><span data-stu-id="0998a-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span></span>

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

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="0998a-139">Considerazioni sull'elaborazione di pool Batch</span><span class="sxs-lookup"><span data-stu-id="0998a-139">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="0998a-140">Pool di elaborazione batch è un servizio di fatturabile always-on e che richiede tooassociate è un gestore di risorse basato su piano di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="0998a-140">Batch Pool Processing is an always-on billable service and that requires you tooassociate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="0998a-141">Verrà addebitato solo per il numero di ore di calcolo è in esecuzione il pool di hello; hello indipendentemente dal numero di hello dei processi eseguiti durante tale pool di tempo.</span><span class="sxs-lookup"><span data-stu-id="0998a-141">You are only billed for hello number of compute hours hello pool is running; regardless of hello number of jobs run during that time pool.</span></span> <span data-ttu-id="0998a-142">Se si crea un pool, verrà addebitato per ore di calcolo hello di ogni macchina virtuale nel pool di hello fino a quando non viene eliminato il pool di hello, anche se nessun processo batch è in esecuzione nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="0998a-142">If you create a pool, you are billed for hello compute hours of each virtual machine in hello pool until hello pool is deleted, even if no batch jobs are running in hello pool.</span></span> <span data-ttu-id="0998a-143">La fatturazione per le macchine virtuali hello inizia quando hanno finito di provisioning e si arresta quando sono state eliminate.</span><span class="sxs-lookup"><span data-stu-id="0998a-143">Billing for hello virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="0998a-144">È possibile utilizzare uno dei piani di hello trovati in hello [dettagli prezzi di Machine Learning](https://azure.microsoft.com/pricing/details/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="0998a-144">You can use any of hello plans found on hello [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="0998a-145">Esempio di fatturazione:</span><span class="sxs-lookup"><span data-stu-id="0998a-145">Billing example:</span></span>

<span data-ttu-id="0998a-146">Se si crea un pool Batch con 2 macchine virtuali e lo si elimina dopo 24 ore, al piano di fatturazione verranno addebitate 48 ore di calcolo, indipendentemente dal numero di processi eseguiti in questo periodo.</span><span class="sxs-lookup"><span data-stu-id="0998a-146">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="0998a-147">Se si crea un pool Batch con 4 macchine virtuali e lo si elimina dopo 12 ore, al piano di fatturazione verranno addebitate 48 ore di calcolo.</span><span class="sxs-lookup"><span data-stu-id="0998a-147">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="0998a-148">È consigliabile eseguire il polling hello processo stato toodetermine quando completamento dei processi.</span><span class="sxs-lookup"><span data-stu-id="0998a-148">We recommend that you poll hello job status toodetermine when jobs complete.</span></span> <span data-ttu-id="0998a-149">Quando tutti i processi hanno terminato l'esecuzione, chiamata hello ridimensionamento Pool tooset hello numero delle operazioni delle macchine virtuali in hello pool toozero.</span><span class="sxs-lookup"><span data-stu-id="0998a-149">When all your jobs have finished running, call hello Resize Pool operation tooset hello number of virtual machines in hello pool toozero.</span></span> <span data-ttu-id="0998a-150">Se sono brevi su risorse del pool ed è necessario toocreate un nuovo pool, ad esempio toobill rispetto a un piano di fatturazione diverso, è possibile eliminare pool hello invece al termine del tutti i processi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0998a-150">If you are short on pool resources and you need toocreate a new pool, for example toobill against a different billing plan, you can delete hello pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="0998a-151">**Usare l'elaborazione di pool Batch quando**</span><span class="sxs-lookup"><span data-stu-id="0998a-151">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="0998a-152">**Usare l'elaborazione di batch classica quando**</span><span class="sxs-lookup"><span data-stu-id="0998a-152">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="0998a-153">È necessario un numero elevato di processi toorun</span><span class="sxs-lookup"><span data-stu-id="0998a-153">You need toorun a large number of jobs</span></span><br><span data-ttu-id="0998a-154">Or</span><span class="sxs-lookup"><span data-stu-id="0998a-154">Or</span></span><br/><span data-ttu-id="0998a-155">È necessario tooknow che i processi verranno eseguiti immediatamente</span><span class="sxs-lookup"><span data-stu-id="0998a-155">You need tooknow that your jobs will run immediately</span></span><br/><span data-ttu-id="0998a-156">Or</span><span class="sxs-lookup"><span data-stu-id="0998a-156">Or</span></span><br/><span data-ttu-id="0998a-157">È necessario garantire la velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="0998a-157">You need guaranteed throughput.</span></span> <span data-ttu-id="0998a-158">Ad esempio necessario toorun un numero di processi in un determinato intervallo di tempo e desidera tooscale out del toomeet risorse di calcolo le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="0998a-158">For example, you need toorun a number of jobs in a given time frame, and want tooscale out your compute resources toomeet your needs.</span></span>    | <span data-ttu-id="0998a-159">Si sta eseguendo un numero limitato di processi</span><span class="sxs-lookup"><span data-stu-id="0998a-159">You are running just a few jobs</span></span><br/><span data-ttu-id="0998a-160">e</span><span class="sxs-lookup"><span data-stu-id="0998a-160">And</span></span><br/> <span data-ttu-id="0998a-161">Non è necessario hello processi toorun immediatamente</span><span class="sxs-lookup"><span data-stu-id="0998a-161">You don’t need hello jobs toorun immediately</span></span> |
