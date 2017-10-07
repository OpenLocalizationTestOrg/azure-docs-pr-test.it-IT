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
# <a name="get-started-with-batch-sdk-for-nodejs"></a>Introduzione all'SDK di Batch per Node.js

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Nozioni di base hello di compilazione di un client di Batch con Node.js [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/). Verrà adottato un approccio graduale che prevede la definizione di uno scenario per un'applicazione batch e quindi la relativa configurazione con un client Node.js.  

## <a name="prerequisites"></a>Prerequisiti
Questo articolo presuppone che l'utente sappia usare Node.js e abbia familiarità con Linux. Inoltre, si presuppone di aver impostato un account Azure con accesso diritti toocreate Batch e servizi di archiviazione.

È consigliabile leggere [Panoramica tecnica di Azure Batch](batch-technical-overview.md) prima di passare a passaggi hello descritte in questo articolo.

## <a name="hello-tutorial-scenario"></a>scenario dell'esercitazione Hello
Verrà ora analizzata uno scenario di hello batch del flusso di lavoro. Abbiamo un semplice script scritto in Python che scarica csv tutti i file da un contenitore di archiviazione Blob di Azure e li converte tooJSON. account di archiviazione più tooprocess contenitori in parallelo, è possibile distribuire script hello come un processo Batch di Azure.

## <a name="azure-batch-architecture"></a>Architettura di Azure Batch
Hello diagramma seguente illustra come è possibile ridimensionare hello Python script usando Azure Batch e un client di Node.js.

![Scenario di Azure Batch](./media/batch-nodejs-get-started/BatchScenario.png)

il client di node.js Hello consente di distribuire un processo batch con un'attività di preparazione (illustrato in dettaglio più avanti) e un set di attività, in base al numero di hello di contenitori nell'account di archiviazione hello. È possibile scaricare gli script hello dal repository github hello.

* [Client Node.js](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [Script della shell per l'attività di preparazione](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [Processore tooJSON csv di Python](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> client di Node.js Hello in hello collegamento specificato non contiene codice specifico toobe distribuiti come un'app di Azure (funzione). È possibile fare riferimento toohello seguenti collegamenti per le istruzioni toocreate uno.
> - [Creare un'app per le funzioni](../azure-functions/functions-create-first-azure-function.md)
> - [Creare una funzione trigger timer](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-hello-application"></a>Compilare un'applicazione hello

A questo punto, segnalare il problema attenersi alla hello passaggi del processo in compilazione client Node.js hello:

### <a name="step-1-install-azure-batch-sdk"></a>Passaggio 1: Installare l'SDK di Azure Batch

È possibile installare i Batch di Azure SDK per Node.js usando il comando install npm hello.

`npm install azure-batch`

Questo comando installa una versione più recente di hello del nodo di batch di azure SDK.

>[!Tip]
> In un'app di Azure (funzione), è possibile passare troppo comandi dell'istallazione "Kudu Console" nella funzione Azure hello impostazioni scheda toorun hello npm. In questo caso tooinstall Azure Batch SDK per Node.js.
>
>

### <a name="step-2-create-an-azure-batch-account"></a>Passaggio 2: Creare un account Azure Batch

È possibile crearlo da hello [portale di Azure](batch-account-create-portal.md) o dalla riga di comando ([Powershell](batch-powershell-cmdlets-get-started.md) /[cli di Azure](https://docs.microsoft.com/cli/azure/overview)).

Di seguito sono hello comandi toocreate uno tramite l'interfaccia CLI di Azure.

Creare un gruppo di risorse, ignorare questo passaggio se già presente in cui si desidera toocreate hello Account Batch:

`az group create -n "<resource-group-name>" -l "<location>"`

Creare quindi un account Azure Batch.

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

Ogni account Batch ha chiavi di accesso corrispondenti, Queste chiavi sono necessari toocreate ulteriori risorse nell'account Azure batch. Una buona norma per l'ambiente di produzione è toouse insieme credenziali chiavi Azure toostore queste chiavi. È quindi possibile creare un servizio principale per un'applicazione hello. Con questa applicazione hello dell'entità servizio è possibile creare un chiavi tooaccess token OAuth dall'insieme di credenziali chiave hello.

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

Copiare e archiviare toobe di hello chiave utilizzato nei passaggi successivi hello.

### <a name="step-3-create-an-azure-batch-service-client"></a>Passaggio 3: Creare un client del servizio Azure Batch
Frammento di codice seguente prima Importa modulo Node.js di azure batch hello e quindi crea un client del servizio Batch. È necessario toofirst creare un oggetto SharedKeyCredentials con chiave dell'account Batch hello copiato dal passaggio precedente hello.

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

Hello URI del Batch di Azure sono disponibili nella scheda Panoramica hello di hello portale di Azure. È del formato hello:

`https://accountname.location.batch.azure.com`

Fare riferimento toohello schermata:

![URI di Azure Batch](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a>Passaggio 4: Creare un pool di Azure Batch
Un pool di Azure Batch è costituito da più VM, dette anche nodi Batch. Servizio di Azure Batch distribuisce attività hello in tali nodi e li gestisce. È possibile definire i seguenti parametri di configurazione per il pool di hello.

* Tipo di immagine di macchina virtuale
* Dimensioni dei nodi macchina virtuale
* Numero di nodi macchina virtuale

> [!Tip]
> dimensioni Hello e numero di nodi di macchina virtuale dipendono in gran parte hello numero di attività si toorun in parallelo e anche attività hello stessa. Si consiglia di test toodetermine numero ideale di hello e dimensioni.
>
>

Hello frammento di codice seguente crea hello oggetti parametro di configurazione.

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
> Per hello l'elenco delle immagini VM Linux disponibili per il Batch di Azure e i relativi ID SKU, vedere [elenco di immagini di macchina virtuale](batch-linux-nodes.md#list-of-virtual-machine-images).
>
>

Dopo la configurazione del pool di hello è definita, è possibile creare pool di hello Azure Batch. Hello comando pool Batch crea nodi di macchina virtuale di Azure e li Prepara toobe tooreceive pronto attività tooexecute. Ogni pool dovrà avere un ID univoco a cui fare riferimento nei passaggi successivi.

Hello frammento di codice seguente crea un pool di Batch di Azure.

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

È possibile controllare lo stato di hello del pool di hello creato e verificare che lo stato di hello "attivo" prima di procedere con l'invio di un pool di processi toothat.

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

Di seguito è un oggetto di esempio risultato restituito dalla funzione pool.get hello.

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


### <a name="step-4-submit-an-azure-batch-job"></a>Passaggio 5: Inviare un processo di Azure Batch
Un processo di Azure Batch è un gruppo logico di attività simili. In questo scenario, è "Processo csv tooJSON." Ogni attività potrà elaborare i file CSV presenti in ogni contenitore di archiviazione di Azure.

Queste attività verranno eseguite in parallelo e distribuiti su più nodi, orchestrati dal servizio Azure Batch hello.

> [!Tip]
> È possibile utilizzare hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) numero massimo di proprietà toospecify di attività che possono essere eseguiti contemporaneamente in un singolo nodo.
>
>

#### <a name="preparation-task"></a>Attività di preparazione

nodi VM Hello creati sono vuote Ubuntu. Spesso, è necessario un gruppo di programmi tooinstall come prerequisiti.
In genere, per i nodi di Linux è disponibile uno script della shell che installa i prerequisiti di hello prima di eseguire le attività effettivo hello. Può tuttavia trattarsi di qualsiasi eseguibile programmabile.
Hello [script della shell](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in questo esempio installa pip di Python e hello Azure Storage SDK per Python.

È possibile caricare script hello in un Account di archiviazione di Azure e generare uno script di hello tooaccess URI SAS. Questo processo può anche essere automatizzato tramite hello Node.js di Azure Storage SDK.

> [!Tip]
> Un'attività di preparazione per un processo viene eseguito solo su nodi VM hello in hello specifiche esigenze dell'utente toorun. Se si desidera toobe prerequisiti installati in tutti i nodi, indipendentemente dalle attività hello che vengono eseguite su di esso, è possibile utilizzare hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) proprietà durante l'aggiunta di un pool. È possibile utilizzare hello seguente definizione di attività di preparazione per riferimento.
>
>

Un'attività di preparazione è specificata durante l'invio di hello del processo Batch di Azure. Seguenti sono hello parametri di configurazione dell'attività di preparazione:

* **ID**: un identificatore univoco per l'attività di preparazione hello
* **riga di comando**: riga di comando tooexecute hello eseguibile dell'attività
* **resourceFiles**: matrice di oggetti che forniscono i dettagli dei file necessari toobe scaricato per toorun questa attività.  Di seguito sono riportate le opzioni.
    - blobSource: hello URI SAS del file hello
    - filePath: toodownload percorso locale e salvare il file hello
    - fileMode: applicabile solo per nodi Linux, in formato ottale con valore predefinito 0770
* **impostazione di waitForSuccess**: se set tootrue, attività hello non viene eseguito per gli errori attività di preparazione
* **runElevated**: impostare tootrue se attività hello toorun necessari privilegi elevati.

Frammento di codice seguente viene illustrato l'esempio di configurazione di hello preparazione attività script:

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

Se sono non presenti alcun toobe prerequisiti installati per toorun le attività, è possibile ignorare l'attività di preparazione hello. Il codice seguente crea un processo con il nome visualizzato "process csv files".

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


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a>Passaggio 6: Inviare le attività di Azure Batch per un processo

Dopo aver creato il processo per l'elaborazione dei file CSV, si creeranno le attività per tale processo. Se che si dispone di quattro contenitori, abbiamo toocreate quattro attività, uno per ogni contenitore.

Se si esamina hello [script Python](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), accetta due parametri:

* nome del contenitore: hello file toodownload contenitore di archiviazione da
* pattern: parametro facoltativo del modello di nome file

Se che si dispone di quattro contenitori "con1", "con2", "con3", "con4" codice seguente viene illustrato l'invio per attività toohello Azure batch processo "processo csv" creata in precedenza.

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

codice Hello aggiunge più pool toohello di attività. E ognuna delle attività hello viene eseguito in un nodo nel pool di hello di macchine virtuali create. Se il numero di hello di attività supera numero hello di macchine virtuali in una proprietà maxTasksPerNode hello o pool, attività hello attendere fino a quando non viene fornito un nodo. Questa orchestrazione viene gestita automaticamente da Azure Batch.

portale Hello contiene dettagliate visualizzazioni attività hello e stati dei processi. È possibile anche usare elenco hello e ottenere le funzioni hello nodo di Azure SDK. Vengono forniti dettagli nella documentazione di hello [collegamento](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).

## <a name="next-steps"></a>Passaggi successivi

- Hello revisione [funzionalità Panoramica di Azure Batch](batch-api-basics.md) articolo, è consigliabile se si è nuovo servizio toohello.
- Vedere hello [riferimento Batch Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello API Batch.

