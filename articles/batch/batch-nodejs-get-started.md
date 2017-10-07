---
title: aaaTutorial - libreria client di utilizzare hello Batch di Azure per Node.js | Documenti Microsoft
description: Informazioni su concetti di base di Azure Batch hello e compilare una soluzione semplice utilizzando Node.js.
services: batch
author: shwetams
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: nodejs
ms.topic: hero-article
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: shwetams
ms.openlocfilehash: d2b0ecbe764e7100affd7b02839aef3077b073cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a><span data-ttu-id="670c8-103">Introduzione all'SDK di Batch per Node.js</span><span class="sxs-lookup"><span data-stu-id="670c8-103">Get started with Batch SDK for Node.js</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="670c8-104">.NET</span><span class="sxs-lookup"><span data-stu-id="670c8-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="670c8-105">Python</span><span class="sxs-lookup"><span data-stu-id="670c8-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="670c8-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="670c8-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="670c8-107">Nozioni di base hello di compilazione di un client di Batch con Node.js [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span><span class="sxs-lookup"><span data-stu-id="670c8-107">Learn hello basics of building a Batch client in Node.js using [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span></span> <span data-ttu-id="670c8-108">Verrà adottato un approccio graduale che prevede la definizione di uno scenario per un'applicazione batch e quindi la relativa configurazione con un client Node.js.</span><span class="sxs-lookup"><span data-stu-id="670c8-108">We take a step by step approach of understanding a scenario for a batch application and then setting it up using a Node.js client.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="670c8-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="670c8-109">Prerequisites</span></span>
<span data-ttu-id="670c8-110">Questo articolo presuppone che l'utente sappia usare Node.js e abbia familiarità con Linux.</span><span class="sxs-lookup"><span data-stu-id="670c8-110">This article assumes that you have a working knowledge of Node.js and familiarity with Linux.</span></span> <span data-ttu-id="670c8-111">Inoltre, si presuppone di aver impostato un account Azure con accesso diritti toocreate Batch e servizi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="670c8-111">It also assumes that you have an Azure account setup with access rights toocreate Batch and Storage services.</span></span>

<span data-ttu-id="670c8-112">È consigliabile leggere [Panoramica tecnica di Azure Batch](batch-technical-overview.md) prima di passare a passaggi hello descritte in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="670c8-112">We recommend reading [Azure Batch Technical Overview](batch-technical-overview.md) before you go through hello steps outlined this article.</span></span>

## <a name="hello-tutorial-scenario"></a><span data-ttu-id="670c8-113">scenario dell'esercitazione Hello</span><span class="sxs-lookup"><span data-stu-id="670c8-113">hello tutorial scenario</span></span>
<span data-ttu-id="670c8-114">Verrà ora analizzata uno scenario di hello batch del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="670c8-114">Let us understand hello batch workflow scenario.</span></span> <span data-ttu-id="670c8-115">Abbiamo un semplice script scritto in Python che scarica csv tutti i file da un contenitore di archiviazione Blob di Azure e li converte tooJSON.</span><span class="sxs-lookup"><span data-stu-id="670c8-115">We have a simple script written in Python that downloads all csv files from an Azure Blob storage container and converts them tooJSON.</span></span> <span data-ttu-id="670c8-116">account di archiviazione più tooprocess contenitori in parallelo, è possibile distribuire script hello come un processo Batch di Azure.</span><span class="sxs-lookup"><span data-stu-id="670c8-116">tooprocess multiple storage account containers in parallel, we can deploy hello script as an Azure Batch job.</span></span>

## <a name="azure-batch-architecture"></a><span data-ttu-id="670c8-117">Architettura di Azure Batch</span><span class="sxs-lookup"><span data-stu-id="670c8-117">Azure Batch Architecture</span></span>
<span data-ttu-id="670c8-118">Hello diagramma seguente illustra come è possibile ridimensionare hello Python script usando Azure Batch e un client di Node.js.</span><span class="sxs-lookup"><span data-stu-id="670c8-118">hello following diagram depicts how we can scale hello Python script using Azure Batch and a Node.js client.</span></span>

![Scenario di Azure Batch](./media/batch-nodejs-get-started/BatchScenario.png)

<span data-ttu-id="670c8-120">il client di node.js Hello consente di distribuire un processo batch con un'attività di preparazione (illustrato in dettaglio più avanti) e un set di attività, in base al numero di hello di contenitori nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="670c8-120">hello node.js client deploys a batch job with a preparation task (explained in detail later) and a set of tasks depending on hello number of containers in hello storage account.</span></span> <span data-ttu-id="670c8-121">È possibile scaricare gli script hello dal repository github hello.</span><span class="sxs-lookup"><span data-stu-id="670c8-121">You can download hello scripts from hello github repository.</span></span>

* [<span data-ttu-id="670c8-122">Client Node.js</span><span class="sxs-lookup"><span data-stu-id="670c8-122">Node.js client</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [<span data-ttu-id="670c8-123">Script della shell per l'attività di preparazione</span><span class="sxs-lookup"><span data-stu-id="670c8-123">Preparation task shell scripts</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [<span data-ttu-id="670c8-124">Processore tooJSON csv di Python</span><span class="sxs-lookup"><span data-stu-id="670c8-124">Python csv tooJSON processor</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> <span data-ttu-id="670c8-125">client di Node.js Hello in hello collegamento specificato non contiene codice specifico toobe distribuiti come un'app di Azure (funzione).</span><span class="sxs-lookup"><span data-stu-id="670c8-125">hello Node.js client in hello link specified does not contain specific code toobe deployed as an Azure function app.</span></span> <span data-ttu-id="670c8-126">È possibile fare riferimento toohello seguenti collegamenti per le istruzioni toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="670c8-126">You can refer toohello following links for instructions toocreate one.</span></span>
> - [<span data-ttu-id="670c8-127">Creare un'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="670c8-127">Create function app</span></span>](../azure-functions/functions-create-first-azure-function.md)
> - [<span data-ttu-id="670c8-128">Creare una funzione trigger timer</span><span class="sxs-lookup"><span data-stu-id="670c8-128">Create timer trigger function</span></span>](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-hello-application"></a><span data-ttu-id="670c8-129">Compilare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="670c8-129">Build hello application</span></span>

<span data-ttu-id="670c8-130">A questo punto, segnalare il problema attenersi alla hello passaggi del processo in compilazione client Node.js hello:</span><span class="sxs-lookup"><span data-stu-id="670c8-130">Now, let us follow hello process step by step into building hello Node.js client:</span></span>

### <a name="step-1-install-azure-batch-sdk"></a><span data-ttu-id="670c8-131">Passaggio 1: Installare l'SDK di Azure Batch</span><span class="sxs-lookup"><span data-stu-id="670c8-131">Step 1: Install Azure Batch SDK</span></span>

<span data-ttu-id="670c8-132">È possibile installare i Batch di Azure SDK per Node.js usando il comando install npm hello.</span><span class="sxs-lookup"><span data-stu-id="670c8-132">You can install Azure Batch SDK for Node.js using hello npm install command.</span></span>

`npm install azure-batch`

<span data-ttu-id="670c8-133">Questo comando installa una versione più recente di hello del nodo di batch di azure SDK.</span><span class="sxs-lookup"><span data-stu-id="670c8-133">This command installs hello latest version of azure-batch node SDK.</span></span>

>[!Tip]
> <span data-ttu-id="670c8-134">In un'app di Azure (funzione), è possibile passare troppo comandi dell'istallazione "Kudu Console" nella funzione Azure hello impostazioni scheda toorun hello npm.</span><span class="sxs-lookup"><span data-stu-id="670c8-134">In an Azure Function app, you can go too"Kudu Console" in hello Azure function's Settings tab toorun hello npm install commands.</span></span> <span data-ttu-id="670c8-135">In questo caso tooinstall Azure Batch SDK per Node.js.</span><span class="sxs-lookup"><span data-stu-id="670c8-135">In this case tooinstall Azure Batch SDK for Node.js.</span></span>
>
>

### <a name="step-2-create-an-azure-batch-account"></a><span data-ttu-id="670c8-136">Passaggio 2: Creare un account Azure Batch</span><span class="sxs-lookup"><span data-stu-id="670c8-136">Step 2: Create an Azure Batch account</span></span>

<span data-ttu-id="670c8-137">È possibile crearlo da hello [portale di Azure](batch-account-create-portal.md) o dalla riga di comando ([Powershell](batch-powershell-cmdlets-get-started.md) /[cli di Azure](https://docs.microsoft.com/cli/azure/overview)).</span><span class="sxs-lookup"><span data-stu-id="670c8-137">You can create it from hello [Azure portal](batch-account-create-portal.md) or from command line ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span></span>

<span data-ttu-id="670c8-138">Di seguito sono hello comandi toocreate uno tramite l'interfaccia CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="670c8-138">Following are hello commands toocreate one through Azure CLI.</span></span>

<span data-ttu-id="670c8-139">Creare un gruppo di risorse, ignorare questo passaggio se già presente in cui si desidera toocreate hello Account Batch:</span><span class="sxs-lookup"><span data-stu-id="670c8-139">Create a Resource Group, skip this step if you already have one where you want toocreate hello Batch Account:</span></span>

`az group create -n "<resource-group-name>" -l "<location>"`

<span data-ttu-id="670c8-140">Creare quindi un account Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="670c8-140">Next, create an Azure Batch account.</span></span>

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="670c8-141">Ogni account Batch ha chiavi di accesso corrispondenti,</span><span class="sxs-lookup"><span data-stu-id="670c8-141">Each Batch account has its corresponding access keys.</span></span> <span data-ttu-id="670c8-142">Queste chiavi sono necessari toocreate ulteriori risorse nell'account Azure batch.</span><span class="sxs-lookup"><span data-stu-id="670c8-142">These keys are needed toocreate further resources in Azure batch account.</span></span> <span data-ttu-id="670c8-143">Una buona norma per l'ambiente di produzione è toouse insieme credenziali chiavi Azure toostore queste chiavi.</span><span class="sxs-lookup"><span data-stu-id="670c8-143">A good practice for production environment is toouse Azure Key Vault toostore these keys.</span></span> <span data-ttu-id="670c8-144">È quindi possibile creare un servizio principale per un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="670c8-144">You can then create a Service principal for hello application.</span></span> <span data-ttu-id="670c8-145">Con questa applicazione hello dell'entità servizio è possibile creare un chiavi tooaccess token OAuth dall'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="670c8-145">Using this service principal hello application can create an OAuth token tooaccess keys from hello key vault.</span></span>

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="670c8-146">Copiare e archiviare toobe di hello chiave utilizzato nei passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="670c8-146">Copy and store hello key toobe used in hello subsequent steps.</span></span>

### <a name="step-3-create-an-azure-batch-service-client"></a><span data-ttu-id="670c8-147">Passaggio 3: Creare un client del servizio Azure Batch</span><span class="sxs-lookup"><span data-stu-id="670c8-147">Step 3: Create an Azure Batch service client</span></span>
<span data-ttu-id="670c8-148">Frammento di codice seguente prima Importa modulo Node.js di azure batch hello e quindi crea un client del servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="670c8-148">Following code snippet first imports hello azure-batch Node.js module and then creates a Batch Service client.</span></span> <span data-ttu-id="670c8-149">È necessario toofirst creare un oggetto SharedKeyCredentials con chiave dell'account Batch hello copiato dal passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="670c8-149">You need toofirst create a SharedKeyCredentials object with hello Batch account key copied from hello previous step.</span></span>

```nodejs
// Initializing Azure Batch variables

var batch = require('azure-batch');

var accountName = '<azure-batch-account-name>';

var accountKey = '<account-key-downloaded>';

var accountUrl = '<account-url>'

// Create Batch credentials object using account name and account key

var credentials = new batch.SharedKeyCredentials(accountName,accountKey);

// Create Batch service client

var batch_client = new batch.ServiceClient(credentials,accountUrl);

```

<span data-ttu-id="670c8-150">Hello URI del Batch di Azure sono disponibili nella scheda Panoramica hello di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="670c8-150">hello Azure Batch URI can be found in hello Overview tab of hello Azure portal.</span></span> <span data-ttu-id="670c8-151">È del formato hello:</span><span class="sxs-lookup"><span data-stu-id="670c8-151">It is of hello format:</span></span>

`https://accountname.location.batch.azure.com`

<span data-ttu-id="670c8-152">Fare riferimento toohello schermata:</span><span class="sxs-lookup"><span data-stu-id="670c8-152">Refer toohello screenshot:</span></span>

![URI di Azure Batch](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a><span data-ttu-id="670c8-154">Passaggio 4: Creare un pool di Azure Batch</span><span class="sxs-lookup"><span data-stu-id="670c8-154">Step 4: Create an Azure Batch pool</span></span>
<span data-ttu-id="670c8-155">Un pool di Azure Batch è costituito da più VM, dette anche nodi Batch.</span><span class="sxs-lookup"><span data-stu-id="670c8-155">An Azure Batch pool consists of multiple VMs (also known as Batch Nodes).</span></span> <span data-ttu-id="670c8-156">Servizio di Azure Batch distribuisce attività hello in tali nodi e li gestisce.</span><span class="sxs-lookup"><span data-stu-id="670c8-156">Azure Batch service deploys hello tasks on these nodes and manages them.</span></span> <span data-ttu-id="670c8-157">È possibile definire i seguenti parametri di configurazione per il pool di hello.</span><span class="sxs-lookup"><span data-stu-id="670c8-157">You can define hello following configuration parameters for your pool.</span></span>

* <span data-ttu-id="670c8-158">Tipo di immagine di macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="670c8-158">Type of Virtual Machine image</span></span>
* <span data-ttu-id="670c8-159">Dimensioni dei nodi macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="670c8-159">Size of Virtual Machine nodes</span></span>
* <span data-ttu-id="670c8-160">Numero di nodi macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="670c8-160">Number of Virtual Machine nodes</span></span>

> [!Tip]
> <span data-ttu-id="670c8-161">dimensioni Hello e numero di nodi di macchina virtuale dipendono in gran parte hello numero di attività si toorun in parallelo e anche attività hello stessa.</span><span class="sxs-lookup"><span data-stu-id="670c8-161">hello size and number of Virtual Machine nodes largely depend on hello number of tasks you want toorun in parallel and also hello task itself.</span></span> <span data-ttu-id="670c8-162">Si consiglia di test toodetermine numero ideale di hello e dimensioni.</span><span class="sxs-lookup"><span data-stu-id="670c8-162">We recommend testing toodetermine hello ideal number and size.</span></span>
>
>

<span data-ttu-id="670c8-163">Hello frammento di codice seguente crea hello oggetti parametro di configurazione.</span><span class="sxs-lookup"><span data-stu-id="670c8-163">hello following code snippet creates hello configuration parameter objects.</span></span>

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating hello VM configuration object with hello SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting hello VM size tooStandard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in hello pool too4
var numVMs = 4
```

> [!Tip]
> <span data-ttu-id="670c8-164">Per hello l'elenco delle immagini VM Linux disponibili per il Batch di Azure e i relativi ID SKU, vedere [elenco di immagini di macchina virtuale](batch-linux-nodes.md#list-of-virtual-machine-images).</span><span class="sxs-lookup"><span data-stu-id="670c8-164">For hello list of Linux VM images available for Azure Batch and their SKU IDs, see [List of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span></span>
>
>

<span data-ttu-id="670c8-165">Dopo la configurazione del pool di hello è definita, è possibile creare pool di hello Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="670c8-165">Once hello pool configuration is defined, you can create hello Azure Batch pool.</span></span> <span data-ttu-id="670c8-166">Hello comando pool Batch crea nodi di macchina virtuale di Azure e li Prepara toobe tooreceive pronto attività tooexecute.</span><span class="sxs-lookup"><span data-stu-id="670c8-166">hello Batch pool command creates Azure Virtual Machine nodes and prepares them toobe ready tooreceive tasks tooexecute.</span></span> <span data-ttu-id="670c8-167">Ogni pool dovrà avere un ID univoco a cui fare riferimento nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="670c8-167">Each pool should have a unique ID for reference in subsequent steps.</span></span>

<span data-ttu-id="670c8-168">Hello frammento di codice seguente crea un pool di Batch di Azure.</span><span class="sxs-lookup"><span data-stu-id="670c8-168">hello following code snippet creates an Azure Batch pool.</span></span>

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

<span data-ttu-id="670c8-169">È possibile controllare lo stato di hello del pool di hello creato e verificare che lo stato di hello "attivo" prima di procedere con l'invio di un pool di processi toothat.</span><span class="sxs-lookup"><span data-stu-id="670c8-169">You can check hello status of hello pool created and ensure that hello state is in "active" before going ahead with submission of a Job toothat pool.</span></span>

```nodejs
var cloudPool = batch_client.pool.get(poolid,function(error,result,request,response){
        if(error == null)
        {

            if(result.state == "active")
            {
                console.log("Pool is active");
            }
        }
        else
        {
            if(error.statusCode==404)
            {
                console.log("Pool not found yet returned 404...");    

            }
            else
            {
                console.log("Error occurred while retrieving pool data");
            }
        }
        });
```

<span data-ttu-id="670c8-170">Di seguito è un oggetto di esempio risultato restituito dalla funzione pool.get hello.</span><span class="sxs-lookup"><span data-stu-id="670c8-170">Following is a sample result object returned by hello pool.get function.</span></span>

```
{ id: 'processcsv_201721152',
  displayName: 'processcsv_201721152',
  url: 'https://<batch-account-name>.centralus.batch.azure.com/pools/processcsv_201721152',
  eTag: '<eTag>',
  lastModified: 2017-03-27T10:28:02.398Z,
  creationTime: 2017-03-27T10:28:02.398Z,
  state: 'active',
  stateTransitionTime: 2017-03-27T10:28:02.398Z,
  allocationState: 'resizing',
  allocationStateTransitionTime: 2017-03-27T10:28:02.398Z,
  vmSize: 'standard_a1',
  virtualMachineConfiguration:
   { imageReference:
      { publisher: 'Canonical',
        offer: 'UbuntuServer',
        sku: '14.04.2-LTS',
        version: 'latest' },
     nodeAgentSKUId: 'batch.node.ubuntu 14.04' },
  resizeTimeout:
   { [Number: 900000]
     _milliseconds: 900000,
     _days: 0,
     _months: 0,
     _data:
      { milliseconds: 0,
        seconds: 0,
        minutes: 15,
        hours: 0,
        days: 0,
        months: 0,
        years: 0 },
     _locale:
      Locale {
        _calendar: [Object],
        _longDateFormat: [Object],
        _invalidDate: 'Invalid date',
        ordinal: [Function: ordinal],
        _ordinalParse: /\d{1,2}(th|st|nd|rd)/,
        _relativeTime: [Object],
        _months: [Object],
        _monthsShort: [Object],
        _week: [Object],
        _weekdays: [Object],
        _weekdaysMin: [Object],
        _weekdaysShort: [Object],
        _meridiemParse: /[ap]\.?m?\.?/i,
        _abbr: 'en',
        _config: [Object],
        _ordinalParseLenient: /\d{1,2}(th|st|nd|rd)|\d{1,2}/ } },
  currentDedicated: 0,
  targetDedicated: 4,
  enableAutoScale: false,
  enableInterNodeCommunication: false,
  maxTasksPerNode: 1,
  taskSchedulingPolicy: { nodeFillType: 'Spread' } }
```


### <a name="step-4-submit-an-azure-batch-job"></a><span data-ttu-id="670c8-171">Passaggio 5: Inviare un processo di Azure Batch</span><span class="sxs-lookup"><span data-stu-id="670c8-171">Step 4: Submit an Azure Batch job</span></span>
<span data-ttu-id="670c8-172">Un processo di Azure Batch è un gruppo logico di attività simili.</span><span class="sxs-lookup"><span data-stu-id="670c8-172">An Azure Batch job is a logical group of similar tasks.</span></span> <span data-ttu-id="670c8-173">In questo scenario, è "Processo csv tooJSON."</span><span class="sxs-lookup"><span data-stu-id="670c8-173">In our scenario, it is "Process csv tooJSON."</span></span> <span data-ttu-id="670c8-174">Ogni attività potrà elaborare i file CSV presenti in ogni contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="670c8-174">Each task here could be processing csv files present in each Azure Storage container.</span></span>

<span data-ttu-id="670c8-175">Queste attività verranno eseguite in parallelo e distribuiti su più nodi, orchestrati dal servizio Azure Batch hello.</span><span class="sxs-lookup"><span data-stu-id="670c8-175">These tasks would run in parallel and deployed across multiple nodes, orchestrated by hello Azure Batch service.</span></span>

> [!Tip]
> <span data-ttu-id="670c8-176">È possibile utilizzare hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) numero massimo di proprietà toospecify di attività che possono essere eseguiti contemporaneamente in un singolo nodo.</span><span class="sxs-lookup"><span data-stu-id="670c8-176">You can use hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property toospecify maximum number of tasks that can run concurrently on a single node.</span></span>
>
>

#### <a name="preparation-task"></a><span data-ttu-id="670c8-177">Attività di preparazione</span><span class="sxs-lookup"><span data-stu-id="670c8-177">Preparation task</span></span>

<span data-ttu-id="670c8-178">nodi VM Hello creati sono vuote Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="670c8-178">hello VM nodes created are blank Ubuntu nodes.</span></span> <span data-ttu-id="670c8-179">Spesso, è necessario un gruppo di programmi tooinstall come prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="670c8-179">Often, you need tooinstall a set of programs as prerequisites.</span></span>
<span data-ttu-id="670c8-180">In genere, per i nodi di Linux è disponibile uno script della shell che installa i prerequisiti di hello prima di eseguire le attività effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="670c8-180">Typically, for Linux nodes you can have a shell script that installs hello prerequisites before hello actual tasks run.</span></span> <span data-ttu-id="670c8-181">Può tuttavia trattarsi di qualsiasi eseguibile programmabile.</span><span class="sxs-lookup"><span data-stu-id="670c8-181">However it could be any programmable executable.</span></span>
<span data-ttu-id="670c8-182">Hello [script della shell](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in questo esempio installa pip di Python e hello Azure Storage SDK per Python.</span><span class="sxs-lookup"><span data-stu-id="670c8-182">hello [shell script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in this example installs Python-pip and hello Azure Storage SDK for Python.</span></span>

<span data-ttu-id="670c8-183">È possibile caricare script hello in un Account di archiviazione di Azure e generare uno script di hello tooaccess URI SAS.</span><span class="sxs-lookup"><span data-stu-id="670c8-183">You can upload hello script on an Azure Storage Account and generate a SAS URI tooaccess hello script.</span></span> <span data-ttu-id="670c8-184">Questo processo può anche essere automatizzato tramite hello Node.js di Azure Storage SDK.</span><span class="sxs-lookup"><span data-stu-id="670c8-184">This process can also be automated using hello Azure Storage Node.js SDK.</span></span>

> [!Tip]
> <span data-ttu-id="670c8-185">Un'attività di preparazione per un processo viene eseguito solo su nodi VM hello in hello specifiche esigenze dell'utente toorun.</span><span class="sxs-lookup"><span data-stu-id="670c8-185">A preparation task for a job runs only on hello VM nodes where hello specific task needs toorun.</span></span> <span data-ttu-id="670c8-186">Se si desidera toobe prerequisiti installati in tutti i nodi, indipendentemente dalle attività hello che vengono eseguite su di esso, è possibile utilizzare hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) proprietà durante l'aggiunta di un pool.</span><span class="sxs-lookup"><span data-stu-id="670c8-186">If you want prerequisites toobe installed on all nodes irrespective of hello tasks that run on it, you can use hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property while adding a pool.</span></span> <span data-ttu-id="670c8-187">È possibile utilizzare hello seguente definizione di attività di preparazione per riferimento.</span><span class="sxs-lookup"><span data-stu-id="670c8-187">You can use hello following preparation task definition for reference.</span></span>
>
>

<span data-ttu-id="670c8-188">Un'attività di preparazione è specificata durante l'invio di hello del processo Batch di Azure.</span><span class="sxs-lookup"><span data-stu-id="670c8-188">A preparation task is specified during hello submission of Azure Batch job.</span></span> <span data-ttu-id="670c8-189">Seguenti sono hello parametri di configurazione dell'attività di preparazione:</span><span class="sxs-lookup"><span data-stu-id="670c8-189">Following are hello preparation task configuration parameters:</span></span>

* <span data-ttu-id="670c8-190">**ID**: un identificatore univoco per l'attività di preparazione hello</span><span class="sxs-lookup"><span data-stu-id="670c8-190">**ID**: A unique identifier for hello preparation task</span></span>
* <span data-ttu-id="670c8-191">**riga di comando**: riga di comando tooexecute hello eseguibile dell'attività</span><span class="sxs-lookup"><span data-stu-id="670c8-191">**commandLine**: Command line tooexecute hello task executable</span></span>
* <span data-ttu-id="670c8-192">**resourceFiles**: matrice di oggetti che forniscono i dettagli dei file necessari toobe scaricato per toorun questa attività.</span><span class="sxs-lookup"><span data-stu-id="670c8-192">**resourceFiles**: Array of objects that provide details of files needed toobe downloaded for this task toorun.</span></span>  <span data-ttu-id="670c8-193">Di seguito sono riportate le opzioni.</span><span class="sxs-lookup"><span data-stu-id="670c8-193">Following are its options</span></span>
    - <span data-ttu-id="670c8-194">blobSource: hello URI SAS del file hello</span><span class="sxs-lookup"><span data-stu-id="670c8-194">blobSource: hello SAS URI of hello file</span></span>
    - <span data-ttu-id="670c8-195">filePath: toodownload percorso locale e salvare il file hello</span><span class="sxs-lookup"><span data-stu-id="670c8-195">filePath: Local path toodownload and save hello file</span></span>
    - <span data-ttu-id="670c8-196">fileMode: applicabile solo per nodi Linux, in formato ottale con valore predefinito 0770</span><span class="sxs-lookup"><span data-stu-id="670c8-196">fileMode: Only applicable for Linux nodes, fileMode is in octal format with a default value of 0770</span></span>
* <span data-ttu-id="670c8-197">**impostazione di waitForSuccess**: se set tootrue, attività hello non viene eseguito per gli errori attività di preparazione</span><span class="sxs-lookup"><span data-stu-id="670c8-197">**waitForSuccess**: If set tootrue, hello task does not run on preparation task failures</span></span>
* <span data-ttu-id="670c8-198">**runElevated**: impostare tootrue se attività hello toorun necessari privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="670c8-198">**runElevated**: Set it tootrue if elevated privileges are needed toorun hello task.</span></span>

<span data-ttu-id="670c8-199">Frammento di codice seguente viene illustrato l'esempio di configurazione di hello preparazione attività script:</span><span class="sxs-lookup"><span data-stu-id="670c8-199">Following code snippet shows hello preparation task script configuration sample:</span></span>

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

<span data-ttu-id="670c8-200">Se sono non presenti alcun toobe prerequisiti installati per toorun le attività, è possibile ignorare l'attività di preparazione hello.</span><span class="sxs-lookup"><span data-stu-id="670c8-200">If there are no prerequisites toobe installed for your tasks toorun, you can skip hello preparation tasks.</span></span> <span data-ttu-id="670c8-201">Il codice seguente crea un processo con il nome visualizzato "process csv files".</span><span class="sxs-lookup"><span data-stu-id="670c8-201">Following code creates a job with display name "process csv files."</span></span>

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job toohello pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a><span data-ttu-id="670c8-202">Passaggio 6: Inviare le attività di Azure Batch per un processo</span><span class="sxs-lookup"><span data-stu-id="670c8-202">Step 5: Submit Azure Batch tasks for a job</span></span>

<span data-ttu-id="670c8-203">Dopo aver creato il processo per l'elaborazione dei file CSV, si creeranno le attività per tale processo.</span><span class="sxs-lookup"><span data-stu-id="670c8-203">Now that our process csv job is created, let us create tasks for that job.</span></span> <span data-ttu-id="670c8-204">Se che si dispone di quattro contenitori, abbiamo toocreate quattro attività, uno per ogni contenitore.</span><span class="sxs-lookup"><span data-stu-id="670c8-204">Assuming we have four containers, we have toocreate four tasks, one for each container.</span></span>

<span data-ttu-id="670c8-205">Se si esamina hello [script Python](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), accetta due parametri:</span><span class="sxs-lookup"><span data-stu-id="670c8-205">If we look at hello [Python script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), it accepts two parameters:</span></span>

* <span data-ttu-id="670c8-206">nome del contenitore: hello file toodownload contenitore di archiviazione da</span><span class="sxs-lookup"><span data-stu-id="670c8-206">container name: hello Storage container toodownload files from</span></span>
* <span data-ttu-id="670c8-207">pattern: parametro facoltativo del modello di nome file</span><span class="sxs-lookup"><span data-stu-id="670c8-207">pattern: An optional parameter of file name pattern</span></span>

<span data-ttu-id="670c8-208">Se che si dispone di quattro contenitori "con1", "con2", "con3", "con4" codice seguente viene illustrato l'invio per attività toohello Azure batch processo "processo csv" creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="670c8-208">Assuming we have four containers "con1", "con2", "con3","con4" following code shows submitting for tasks toohello Azure batch job "process csv" we created earlier.</span></span>

```nodejs
// storing container names in an array
var container_list = ["con1","con2","con3","con4"]
    container_list.forEach(function(val,index){           

           var container_name = val;
           var taskID = container_name + "_process";
           var task_config = {id:taskID,displayName:'process csv in ' + container_name,commandLine:'python processcsv.py --container ' + container_name,resourceFiles:[{'blobSource':'<blob SAS URI>','filePath':'processcsv.py'}]}
           var task = batch_client.task.add(poolid,task_config,function(error,result){
                if(error != null)
                {
                    console.log(error.response);     
                }
                else
                {
                    console.log("Task for container : " + container_name + "submitted successfully");
                }



           });

    });
```

<span data-ttu-id="670c8-209">codice Hello aggiunge più pool toohello di attività.</span><span class="sxs-lookup"><span data-stu-id="670c8-209">hello code adds multiple tasks toohello pool.</span></span> <span data-ttu-id="670c8-210">E ognuna delle attività hello viene eseguito in un nodo nel pool di hello di macchine virtuali create.</span><span class="sxs-lookup"><span data-stu-id="670c8-210">And each of hello tasks is executed on a node in hello pool of VMs created.</span></span> <span data-ttu-id="670c8-211">Se il numero di hello di attività supera numero hello di macchine virtuali in una proprietà maxTasksPerNode hello o pool, attività hello attendere fino a quando non viene fornito un nodo.</span><span class="sxs-lookup"><span data-stu-id="670c8-211">If hello number of tasks exceeds hello number of VMs in a pool or hello maxTasksPerNode property, hello tasks wait until a node is made available.</span></span> <span data-ttu-id="670c8-212">Questa orchestrazione viene gestita automaticamente da Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="670c8-212">This orchestration is handled by Azure Batch automatically.</span></span>

<span data-ttu-id="670c8-213">portale Hello contiene dettagliate visualizzazioni attività hello e stati dei processi.</span><span class="sxs-lookup"><span data-stu-id="670c8-213">hello portal has detailed views on hello tasks and job statuses.</span></span> <span data-ttu-id="670c8-214">È possibile anche usare elenco hello e ottenere le funzioni hello nodo di Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="670c8-214">You can also use hello list and get functions in hello Azure Node SDK.</span></span> <span data-ttu-id="670c8-215">Vengono forniti dettagli nella documentazione di hello [collegamento](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span><span class="sxs-lookup"><span data-stu-id="670c8-215">Details are provided in hello documentation [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="670c8-216">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="670c8-216">Next steps</span></span>

- <span data-ttu-id="670c8-217">Hello revisione [funzionalità Panoramica di Azure Batch](batch-api-basics.md) articolo, è consigliabile se si è nuovo servizio toohello.</span><span class="sxs-lookup"><span data-stu-id="670c8-217">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
- <span data-ttu-id="670c8-218">Vedere hello [riferimento Batch Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello API Batch.</span><span class="sxs-lookup"><span data-stu-id="670c8-218">See hello [Batch Node.js reference](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello Batch API.</span></span>

