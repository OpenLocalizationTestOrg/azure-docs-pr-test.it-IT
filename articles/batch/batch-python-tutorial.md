---
title: aaaTutorial - hello usare Azure Batch SDK per Python | Documenti Microsoft
description: Informazioni su concetti di base di Azure Batch hello e compilare una soluzione semplice usando Python.
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: 42cae157-d43d-47f8-88f5-486ccfd334f4
ms.service: batch
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c4d5152aeef31848c50a7f2aae5e7a7e0e1e9535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-sdk-for-python"></a>Introduzione a hello Batch SDK per Python

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.js](batch-nodejs-get-started.md)
>
>

Nozioni di base hello di [Azure Batch] [ azure_batch] hello e [Python Batch] [ py_azure_sdk] client come illustrato una piccola applicazione Batch scritta in Python. Vengono analizzati come due esempio script utilizzare hello Batch servizio tooprocess un carico di lavoro parallelo in macchine virtuali Linux in cloud hello e la loro interazione [di archiviazione di Azure](../storage/common/storage-introduction.md) per gestione temporanea di file e il recupero. Si illustra Batch applicazione flusso di lavoro comune e acquisire una comprensione di base dei componenti principali hello del Batch, ad esempio i processi, attività, i pool e nodi di calcolo.

![Flusso di lavoro della soluzione Batch (di base)][11]<br/>

## <a name="prerequisites"></a>Prerequisiti
Questo articolo presuppone che l'utente sappia usare Python e Linux Si presuppone inoltre che si è in grado di toosatisfy hello creazione requisiti dell'account specificate di seguito per Azure e hello Batch e servizi di archiviazione.

### <a name="accounts"></a>Account
* **Account Azure**: se non si ha già una sottoscrizione di Azure, [creare un account Azure gratuito][azure_free_account].
* **Account Batch**: dopo aver creato una sottoscrizione di Azure, [creare un account Azure Batch](batch-account-create-portal.md).
* **Account di archiviazione**: vedere [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).

### <a name="code-sample"></a>Esempio di codice
esercitazione di Python Hello [nell'esempio di codice] [ github_article_samples] è uno dei molti esempi di codice di Batch, vedere hello hello [esempi di azure batch] [ github_samples] repository in GitHub. È possibile scaricare tutti gli esempi di hello facendo **Clone o download > Download ZIP** nella home page del repository hello o facendo clic su hello [azure-batch-esempi-master.zip] [ github_samples_zip]collegamento diretto. Dopo aver estratto il contenuto di hello del file ZIP hello, script hello due per questa esercitazione si trovano in hello `article_samples` directory:

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a>Ambiente Python
hello toorun *python_tutorial_client.py* script di esempio nella workstation locale, è necessario un **interprete Python** compatibile con la versione **2.7** o **3.3 +**. script Hello è stato testato su Linux e Windows.

### <a name="cryptography-dependencies"></a>Dipendenze di cryptography
È necessario installare le dipendenze di hello per hello [crittografia] [ crypto] libreria, richiesta da hello `azure-batch` e `azure-storage` pacchetti Python. Eseguire una delle seguente operazioni appropriate per la piattaforma hello o fare riferimento toohello [installazione crittografia] [ crypto_install] dettagli per ulteriori informazioni:

* Ubuntu

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* CentOS

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* SLES/OpenSUSE

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* Windows

    `pip install cryptography`

> [!NOTE]
> Se l'installazione di Python 3.3 + su Linux, utilizzare equivalenti python3 hello per le dipendenze di Python hello. Ad esempio, in Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`
>
>

### <a name="azure-packages"></a>Pacchetti di Azure
Installare quindi hello **Azure Batch** e **di archiviazione di Azure** pacchetti Python. È possibile installare entrambi i pacchetti utilizzando **pip** hello e *requirements.txt* disponibili qui:

`/azure-batch-samples/Python/Batch/requirements.txt`

Il seguente problema **pip** pacchetti di Batch e l'archiviazione hello tooinstall di comando:

`pip install -r requirements.txt`

In alternativa, è possibile installare hello [azure batch] [ pypi_batch] e [archiviazione di azure] [ pypi_storage] Python pacchetti manualmente:

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> Se si utilizza un account senza privilegi, potrebbe essere necessario tooprefix i comandi con `sudo`. ad esempio `sudo pip install -r requirements.txt`. Per altre informazioni sull'installazione dei pacchetti Python, vedere [Installing Packages][pypi_install] (Installazione di pacchetti) in python.org.
>
>

## <a name="batch-python-tutorial-code-sample"></a>Esempio di codice per l'esercitazione di Batch Python
Nell'esempio di codice dell'esercitazione Batch Python Hello è costituito da due script Python e alcuni file di dati.

* **python_tutorial_client.py**: interagisce con tooexecute di servizi di archiviazione e Batch hello un carico di lavoro parallelo in nodi di calcolo (macchine virtuali). Hello *python_tutorial_client.py* script viene eseguito nella workstation locale.
* **python_tutorial_task.py**: hello dello script eseguito in nodi di calcolo in Azure tooperform il lavoro effettivo hello. Nell'esempio hello *python_tutorial_task.py* analizza hello testo in un file scaricato dall'archiviazione di Azure (file di input di hello). Quindi, produce un file di testo (file di output di hello) che contiene un elenco di hello prime tre parole che vengono visualizzati nel file di input hello. Dopo la creazione di file di output di hello, *python_tutorial_task.py* caricamenti hello tooAzure file archiviazione. Questo rende disponibili per lo script client di toohello download esecuzione sulla workstation. Hello *python_tutorial_task.py* script viene eseguito in parallelo su più nodi di calcolo nel servizio Batch hello.
* **./Data/taskdata\*. txt**: questi file di tre testo forniscono input hello per le attività di hello eseguite sul hello nodi di calcolo.

Hello seguente diagramma illustra hello primaria le operazioni eseguite dagli script di hello client e attività. Questo flusso di lavoro di base è tipico di molte soluzioni di calcolo create con Batch. Mentre non vengono visualizzati tutte le funzionalità disponibili nel servizio Batch hello, quasi ogni scenario di Batch include parti del flusso di lavoro.

![Flusso di lavoro dell'esempio di Batch][8]<br/>

[**Passaggio 1.**](#step-1-create-storage-containers) Creare **contenitori** nell'archivio BLOB di Azure.<br/>
[**Passaggio 2.**](#step-2-upload-task-script-and-data-files) Caricare toocontainers di file di script e l'input dell'attività.<br/>
[**Passaggio 3.**](#step-3-create-batch-pool) Creare un **pool** di Batch.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Hello pool **StartTask** download hello attività script (python_tutorial_task.py) toonodes che si connettono pool hello.<br/>
[**Passaggio 4.**](#step-4-create-batch-job) Creare un **processo** di Batch.<br/>
[**Passaggio 5.**](#step-5-add-tasks-to-job) Aggiungere **attività** toohello processo.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** attività di Hello sono tooexecute pianificati sui nodi.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** Ogni attività scarica i rispettivi dati di input da Archiviazione di Azure e quindi avvia l'esecuzione.<br/>
[**Passaggio 6.**](#step-6-monitor-tasks) Monitorare le attività.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** Come vengono completate, caricamento del loro tooAzure di dati di output archiviazione.<br/>
[**Passaggio 7.**](#step-7-download-task-output) Scaricare l'output delle attività dal servizio di archiviazione.

Come indicato, non tutte le soluzioni Batch eseguono esattamente questi passaggi e potrebbero includerne molti altri, ma l'esempio illustra i processi comuni presenti in una soluzione Batch.

## <a name="prepare-client-script"></a>Preparare lo script client
Prima di eseguire l'esempio hello, aggiungere le credenziali dell'account di archiviazione e Batch troppo*python_tutorial_client.py*. Se non è già stato fatto, aprire il file hello i Preferiti hello editor e l'aggiornamento dopo le righe con le credenziali.

```python
# Update hello Batch and Storage account credential strings below with hello values
# unique tooyour accounts. These are used when constructing connection strings
# for hello Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

È possibile trovare le credenziali dell'account Batch e l'archiviazione all'interno di blade account hello di ogni servizio in hello [portale di Azure][azure_portal]:

![Batch credenziali nel portale di hello][9]
![le credenziali di archiviazione nel portale di hello][10]<br/>

Nelle seguenti sezioni di hello, consente di analizzare i passi hello utilizzati dal hello script tooprocess un carico di lavoro in hello servizio Batch. Si consiglia di toorefer regolarmente toohello script nell'editor mentre si percorrere rest hello dell'articolo hello.

Passare toohello seguente riga **python_tutorial_client.py** toostart con il passaggio 1:

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a>Passaggio 1: Creare contenitori di archiviazione
![Creare contenitori in Archiviazione di Azure][1]
<br/>

Batch include il supporto predefinito per l'interazione con Archiviazione di Azure. I contenitori nell'account di archiviazione offrono file hello necessari per le attività di hello eseguite nell'account di Batch. i contenitori di Hello offrono anche un posizionamento toostore hello output di dati che producono attività hello. in primo luogo Hello hello *python_tutorial_client.py* script consente di creare tre contenitori in [archiviazione Blob di Azure](../storage/common/storage-introduction.md#blob-storage):

* **applicazione**: questo contenitore verranno archiviati hello Python script eseguiti dalle attività hello, *python_tutorial_task.py*.
* **input**: attività scaricherà tooprocess i file di dati hello dal hello *input* contenitore.
* **output**: al termine dell'elaborazione del file di input di attività, verrà caricato hello risultati toohello *output* contenitore.

In ordine toointeract con uno spazio di archiviazione account e creare contenitori, utilizziamo hello [archiviazione di azure] [ pypi_storage] pacchetto toocreate un [BlockBlobService] [ py_blockblobservice] oggetto--hello ""blob client. È quindi possibile creare tre contenitori nell'account di archiviazione di hello utilizzando client hello del blob.

```python
import azure.storage.blob as azureblob

# Create hello blob client, for use in obtaining references to
# blob storage containers and uploading files toocontainers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use hello blob client toocreate hello containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

Dopo avere creati i contenitori di hello, un'applicazione hello ora possibile caricare file hello che verranno utilizzati dalle attività hello.

> [!TIP]
> [Come toouse archiviazione Blob di Azure da Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) fornisce una buona panoramica dell'utilizzo di BLOB e contenitori di archiviazione di Azure. Quando si inizia a batch deve essere superiore hello dell'elenco di lettura.
>
>

## <a name="step-2-upload-task-script-and-data-files"></a>Passaggio 2: Caricare lo script attività e i file di dati
![Attività di caricamento dell'applicazione e di input (dati) file toocontainers][2]
<br/>

Nel file hello caricare operazione *python_tutorial_client.py* prima definisce le raccolte di **applicazione** e **input** percorsi di file in cui si trovano sul computer locale hello. Carica quindi questi contenitori toohello file creato nel passaggio precedente hello.

```python
# Paths toohello task script. This script will be executed by hello tasks that
# run on hello compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# hello collection of data files that are toobe processed by hello tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload hello application script tooAzure Storage. This is hello script that
# will process hello data files, and is executed by each of hello tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload hello data files. This is hello data that will be processed by each of
# hello tasks executed on hello compute nodes in hello pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

Mediante la comprensione di elenco, hello `upload_file_to_container` funzione viene chiamata per ogni file nelle raccolte di hello e due [ResourceFile] [ py_resource_file] raccolte vengono popolate. Hello `upload_file_to_container` funzione viene visualizzata di seguito:

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file tooan Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: hello name of hello Azure Blob storage container.
    :param str file_path: hello local path toohello file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} toocontainer [{}]...'.format(path,
                                                          container_name))

    block_blob_client.create_blob_from_path(container_name,
                                            blob_name,
                                            file_path)

    sas_token = block_blob_client.generate_blob_shared_access_signature(
        container_name,
        blob_name,
        permission=azureblob.BlobPermissions.READ,
        expiry=datetime.datetime.utcnow() + datetime.timedelta(hours=2))

    sas_url = block_blob_client.make_blob_url(container_name,
                                              blob_name,
                                              sas_token=sas_token)

    return batchmodels.ResourceFile(file_path=blob_name,
                                    blob_source=sas_url)
```

### <a name="resourcefiles"></a>ResourceFiles
Oggetto [ResourceFile] [ py_resource_file] fornisce operazioni in Batch con file di tooa URL hello in archiviazione di Azure che viene scaricato tooa nodo di calcolo prima di tale attività è in esecuzione. Hello [ResourceFile][py_resource_file]. **blob_source** proprietà specifica hello URL completo del file hello presenti in archiviazione di Azure. Hello URL può includere una firma di accesso condiviso (SAS) che fornisce l'accesso sicuro toohello file. La maggior parte dei tipi di attività in Batch include una proprietà *ResourceFiles*, ad esempio:

* [CloudTask][py_task]
* [StartTask][py_starttask]
* [JobPreparationTask][py_jobpreptask]
* [JobReleaseTask][py_jobreltask]

In questo esempio non utilizza hello JobPreparationTask o JobReleaseTask tipi di attività, ma è possibile leggere informazioni su di essi in [attività Esegui processo di preparazione e completamento del Batch di Azure i nodi di calcolo](batch-job-prep-release.md).

### <a name="shared-access-signature-sas"></a>Firma di accesso condiviso
Firme di accesso condiviso sono stringhe che forniscono l'accesso sicuro toocontainers e BLOB in archiviazione di Azure. Hello *python_tutorial_client.py* script vengono utilizzati entrambi i blob e contenitore firme di accesso condiviso, viene illustrato come accedere stringhe firma tooobtain questi condiviso dal servizio di archiviazione hello.

* **Firme di accesso condiviso di BLOB**: utilizza StartTask hello pool blob firme di accesso condiviso durante il download di hello attività script e input i file di dati dall'archivio (vedere [passaggio #3](#step-3-create-batch-pool) sotto). Hello `upload_file_to_container` funzionare in *python_tutorial_client.py* contiene codice hello che ottiene la firma di accesso condiviso del blob ogni. Esegue l'operazione chiamando [BlockBlobService.make_blob_url] [ py_make_blob_url] nel modulo di archiviazione hello.
* **Firma di accesso condiviso del contenitore**: come le operazioni sul nodo di calcolo hello al termine di ogni attività, viene caricato il toohello di file di output *output* contenitore di archiviazione di Azure. toodo, *python_tutorial_task.py* utilizza una firma di accesso condiviso di contenitore che fornisce l'accesso in scrittura toohello contenitore. Hello `get_container_sas_token` funzionare in *python_tutorial_client.py* Ottiene firma di accesso condiviso del contenitore di hello, che viene quindi passata come attività di toohello un argomento della riga di comando. Passaggio &#5;, [processo di aggiunta attività tooa](#step-5-add-tasks-to-job), viene descritto l'utilizzo di hello del contenitore hello SAS.

> [!TIP]
> Check-out di serie in due parti hello sulle firme di accesso condiviso, [parte 1: modello di firma di accesso condiviso hello comprensione](../storage/common/storage-dotnet-shared-access-signature-part-1.md) e [parte 2: creare e usare una firma di accesso condiviso con il servizio Blob hello](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn ulteriori informazioni su come fornire accesso sicuro toodata nell'account di archiviazione.
>
>

## <a name="step-3-create-batch-pool"></a>Passaggio 3: Creare un pool di Batch
![Creare un pool di Batch][3]
<br/>

Un **pool** di Batch è una raccolta di nodi di calcolo (macchine virtuali) in cui Batch esegue le attività di un processo.

Dopo che viene caricato hello attività script e i dati file toohello account di archiviazione, *python_tutorial_client.py* avvia l'interazione con il servizio Batch hello mediante il modulo di Python Batch hello. toodo, un [BatchServiceClient] [ py_batchserviceclient] viene creato:

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

Successivamente, viene creato un pool di nodi di calcolo in hello account Batch con una chiamata troppo`create_pool`.

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with hello specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for hello new pool.
    :param list resource_files: A collection of resource files for hello pool's
    start task.
    :param str publisher: Marketplace image publisher
    :param str offer: Marketplace image offer
    :param str sku: Marketplace image sku
    """
    print('Creating pool [{}]...'.format(pool_id))

    # Create a new pool of Linux compute nodes using an Azure Virtual Machines
    # Marketplace image. For more information about creating pools of Linux
    # nodes, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/

    # Specify hello commands for hello pool's start task. hello start task is run
    # on each node as it joins hello pool, and when it's rebooted or re-imaged.
    # We use hello start task tooprep hello node for running our task script.
    task_commands = [
        # Copy hello python_tutorial_task.py script toohello "shared" directory
        # that all tasks that run on hello node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and hello dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install hello azure-storage module so that hello task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get hello node agent SKU and image reference for hello virtual machine
    # configuration.
    # For more information about hello virtual machine configuration, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/
    sku_to_use, image_ref_to_use = \
        common.helpers.select_latest_verified_vm_image_with_node_agent_sku(
            batch_service_client, publisher, offer, sku)

    new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            node_agent_sku_id=sku_to_use),
        vm_size=_POOL_VM_SIZE,
        target_dedicated=_POOL_NODE_COUNT,
        start_task=batch.models.StartTask(
            command_line=
            common.helpers.wrap_commands_in_shell('linux', task_commands),
            run_elevated=True,
            wait_for_success=True,
            resource_files=resource_files),
        )

    try:
        batch_service_client.pool.add(new_pool)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

Quando si crea un pool, si definisce un [PoolAddParameter] [ py_pooladdparam] che consente di specificare diverse proprietà per il pool di hello:

* **ID** del pool di hello (*id* - obbligatorio)<p/>Così come la maggior parte delle entità in Batch, il nuovo pool deve avere un ID univoco all'interno dell'account Batch. Il codice fa riferimento utilizzando l'ID del pool di toothis ed è identificare pool hello in hello Azure [portale][azure_portal].
* **Numero di nodi di calcolo** (*target_dedicated*: obbligatorio)<p/>Questa proprietà specifica il numero di macchine virtuali devono essere distribuite nel pool di hello. È importante toonote dispongano di tutti gli account Batch predefinito **quota** che limiti hello numero di **core** (e di conseguenza, i nodi di calcolo) in un account Batch. È possibile trovare le quote predefinite hello e istruzioni su come troppo[aumentare la quota](batch-quota-limit.md#increase-a-quota) (come il numero massimo di hello di core nell'account di Batch) in [quote e limiti per il servizio Azure Batch hello](batch-quota-limit.md). Se il pool non raggiunge più di X nodi, ad esempio, Questa quota core può essere causa hello.
* **Sistema operativo** per i nodi (*virtual_machine_configuration***o***cloud_service_configuration*: obbligatorio)<p/>In *python_tutorial_client.py* viene creato un pool di nodi Linux tramite [VirtualMachineConfiguration][py_vm_config]. Hello `select_latest_verified_vm_image_with_node_agent_sku` funzionare in `common.helpers` semplifica l'utilizzo di [macchine virtuali di Azure Marketplace] [ vm_marketplace] immagini. Per altre informazioni sull'uso delle immagini del Marketplace, vedere [Effettuare il provisioning di nodi di calcolo Linux nei pool di Azure Batch](batch-linux-nodes.md) .
* **Dimensione dei nodi di calcolo** (*vm_size*: obbligatorio)<p/>Dato che vengono specificati nodi Linux per [VirtualMachineConfiguration][py_vm_config], viene specificata una dimensione di VM, in questo esempio `STANDARD_A1`, in base a quanto descritto in [Dimensioni delle macchine virtuali in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Per altre informazioni, vedere [Effettuare il provisioning di nodi di calcolo Linux nei pool di Azure Batch](batch-linux-nodes.md) .
* **Attività di avvio** (*start_task*: non obbligatorio)<p/>Insieme a hello sopra le proprietà del nodo fisico, è inoltre possibile specificare un [StartTask] [ py_starttask] per pool hello (non è obbligatorio). Hello StartTask viene eseguito in ogni nodo come nodo aggiunto pool hello e ogni volta che un nodo viene riavviato. Hello StartTask è particolarmente utile per la preparazione dei nodi di calcolo per l'esecuzione di attività, ad esempio l'installazione di applicazioni di hello che vengono eseguite le attività hello.<p/>In questa applicazione di esempio, hello StartTask copia i file hello scaricati dall'archiviazione (che vengono specificati usando del StartTask hello **resource_files** proprietà) da hello StartTask *directorydilavoro* toohello *condivisa* directory che possono accedere a tutte le attività in esecuzione nel nodo hello. In pratica, questa copia `python_tutorial_task.py` toohello directory condivise su ciascun nodo come nodo hello join pool hello, in modo che qualsiasi attività che vengono eseguite sul nodo hello può accedervi.

È possibile riscontrare hello chiamata toohello `wrap_commands_in_shell` funzione di supporto. Questa funzione acquisisce una raccolta di comandi separati e crea una singola riga di comando appropriata per la proprietà della riga di comando dell'attività.

Inoltre rilevanti nel frammento di codice hello sopra sono utilizzare hello due variabili di ambiente nell'hello **riga di comando** proprietà di hello StartTask: `AZ_BATCH_TASK_WORKING_DIR` e `AZ_BATCH_NODE_SHARED_DIR`. Ogni nodo di calcolo all'interno di un Batch viene configurato automaticamente con alcune variabili di ambiente sono tooBatch specifico. Qualsiasi processo che viene eseguita da un'attività con le variabili di ambiente toothese di accesso.

> [!TIP]
> toofind ulteriori informazioni sulle variabili di ambiente hello sono disponibili nei nodi di calcolo in un pool di Batch, nonché informazioni sulla directory di lavoro attività, vedere **impostazioni di ambiente per l'attività** e **file e directory**  in hello [panoramica delle funzionalità di Azure Batch](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a>Passaggio 4: Creare un processo di Batch
![Creare un processo di Batch][4]<br/>

Un **processo** di Batch è una raccolta di attività ed è associato a un pool di nodi di calcolo. attività Hello in un processo eseguito sui nodi di calcolo del pool di hello associata.

È possibile utilizzare un processo non solo per l'organizzazione e il rilevamento di attività nei carichi di lavoro correlati, ma anche per l'imposizione di determinati vincoli, ad esempio hello di esecuzione massimo per il processo di hello (e, di conseguenza, le relative attività) e la priorità del processo nei processi tooother relazione in hello account Batch. In questo esempio, tuttavia, viene associato solo a pool hello creato nel passaggio &#3; processo hello. Non vengono configurate proprietà aggiuntive.

Tutti i processi di Batch sono associati a un pool specifico. Questa associazione indica quali nodi del processo di hello eseguite ai. Per specificare il pool di hello, utilizzare hello [PoolInformation] [ py_poolinfo] proprietà, come illustrato nel frammento di codice hello riportato di seguito.

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with hello specified ID, associated with hello specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID for hello job.
    :param str pool_id: hello ID for hello pool.
    """
    print('Creating job [{}]...'.format(job_id))

    job = batch.models.JobAddParameter(
        job_id,
        batch.models.PoolInformation(pool_id=pool_id))

    try:
        batch_service_client.job.add(job)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

Ora che è stato creato un processo, le attività vengono aggiunti lavoro hello tooperform.

## <a name="step-5-add-tasks-toojob"></a>Passaggio 5: Aggiungere attività toojob
![Aggiungere attività toojob][5]<br/>
*(1) processo toohello sono state aggiunte le attività, le attività di hello (2) sono pianificati toorun nei nodi e attività hello (3) scaricare tooprocess i file di dati hello*

Batch **attività** sono nodi di calcolo hello singole unità di lavoro che vengono eseguite sullo hello. Un'attività dispone di una riga di comando ed esegue gli script hello o file eseguibili specificati in questa riga di comando.

tooactually eseguire lavoro, è necessario aggiungere attività tooa processo. Ogni [CloudTask] [ py_task] è configurato con una proprietà della riga di comando e [ResourceFiles] [ py_resource_file] (come StartTask del pool di hello) che hello attività Scarica il nodo toohello prima che la riga di comando viene eseguita automaticamente. Nell'esempio hello, ogni attività vengono elaborati solo un file. Di conseguenza, la rispettiva raccolta ResourceFiles contiene un singolo elemento.

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in hello collection toohello specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID of hello job toowhich tooadd hello tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: hello ID of an Azure Blob storage container to
    which hello tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    hello specified Azure Blob storage container.
    """

    print('Adding {} tasks toojob [{}]...'.format(len(input_files), job_id))

    tasks = list()

    for input_file in input_files:

        command = ['python $AZ_BATCH_NODE_SHARED_DIR/python_tutorial_task.py '
                   '--filepath {} --numwords {} --storageaccount {} '
                   '--storagecontainer {} --sastoken "{}"'.format(
                    input_file.file_path,
                    '3',
                    _STORAGE_ACCOUNT_NAME,
                    output_container_name,
                    output_container_sas_token)]

        tasks.append(batch.models.TaskAddParameter(
                'topNtask{}'.format(input_files.index(input_file)),
                wrap_commands_in_shell('linux', command),
                resource_files=[input_file]
                )
        )

    batch_service_client.task.add_collection(job_id, tasks)
```

> [!IMPORTANT]
> Quando accedono a variabili di ambiente, ad esempio `$AZ_BATCH_NODE_SHARED_DIR` o eseguire un'applicazione non trovata nel nodo di hello `PATH`, righe di comando dell'attività deve richiamare hello shell in modo esplicito, ad esempio con `/bin/sh -c MyTaskApplication $MY_ENV_VAR`. Questo requisito non è necessario se un'applicazione di esecuzione delle attività nel nodo di hello `PATH` e non fanno riferimento a tutte le variabili di ambiente.
>
>

All'interno di hello `for` ciclo nel frammento di codice hello precedente, è possibile vedere che la riga di comando hello per attività hello è costruita con cinque argomenti della riga di comando che vengono passati troppo*python_tutorial_task.py*:

1. **FilePath**: si tratta di file toohello di hello percorso locale nello stato attuale per il nodo hello. Quando hello oggetto ResourceFile `upload_file_to_container` è stato creato nel passaggio 2, nome del file hello è stato utilizzato per questa proprietà (hello `file_path` parametro nel costruttore ResourceFile hello). Ciò indica che file hello è reperibile in hello stesso nodo hello come directory *python_tutorial_task.py*.
2. **NUMWORDS**: inizio hello *N* parole devono essere scritti i file di output toohello.
3. **storageaccount**: nome hello di hello account di archiviazione che possiede l'output dell'attività hello toowhich hello contenitore deve essere caricato.
4. **storagecontainer**: nome hello di hello toowhich di hello archiviazione contenitore output file devono essere caricati.
5. **sastoken**: firma di accesso condiviso hello (SAS) che fornisce l'accesso in scrittura toohello **output** contenitore di archiviazione di Azure. Hello *python_tutorial_task.py* script utilizza la firma di accesso condiviso quando si crea il relativo riferimento BlockBlobService. Questo fornisce l'accesso in scrittura toohello contenitore senza richiedere una chiave di accesso per account di archiviazione hello.

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a>Passaggio 6: Monitorare le attività
![Monitorare le attività][6]<br/>
*Hello hello (1) Monitor attività per lo stato di completamento e caricare il risultato dati tooAzure archiviazione attività hello (2)*

Quando le attività vengono aggiunte tooa processo, vengono automaticamente in coda e pianificate per l'esecuzione nei nodi di calcolo nel pool di hello associata al processo hello. In base alle impostazioni di hello specificate, Batch gestisce tutte le attività di accodamento, la pianificazione, nuovo tentativo in corso e altre funzioni di amministrazione di attività per l'utente.

Esistono molti approcci toomonitoring l'esecuzione dell'attività. Hello `wait_for_tasks_to_complete` funzionare in *python_tutorial_client.py* fornisce un semplice esempio di attività di monitoraggio per un determinato stato, in questo caso, hello [completato] [ py_taskstate] stato.

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in hello specified job reach hello Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello id of hello job whose tasks should be toomonitored.
    :param timedelta timeout: hello duration toowait for task completion. If all
    tasks in hello specified job do not reach Completed state within this time
    period, an exception will be raised.
    """
    timeout_expiration = datetime.datetime.now() + timeout

    print("Monitoring all tasks for 'Completed' state, timeout in {}..."
          .format(timeout), end='')

    while datetime.datetime.now() < timeout_expiration:
        print('.', end='')
        sys.stdout.flush()
        tasks = batch_service_client.task.list(job_id)

        incomplete_tasks = [task for task in tasks if
                            task.state != batchmodels.TaskState.completed]
        if not incomplete_tasks:
            print()
            return True
        else:
            time.sleep(1)

    print()
    raise RuntimeError("ERROR: Tasks did not reach 'Completed' state within "
                       "timeout period of " + str(timeout))
```

## <a name="step-7-download-task-output"></a>Passaggio 7: Scaricare l'output dell'attività
![Scaricare l'output delle attività dal servizio di archiviazione][7]<br/>

Hello processo una volta completato, l'output di hello di hello attività può essere scaricato dall'archiviazione di Azure. Questa operazione viene eseguita con una chiamata troppo`download_blobs_from_container` in *python_tutorial_client.py*:

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from hello specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: hello Azure Blob storage container from which to
     download files.
    :param directory_path: hello local directory toowhich toodownload hello files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] too{}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> Hello chiamata troppo`download_blobs_from_container` in *python_tutorial_client.py* specifica che il file hello devono essere scaricato tooyour home directory. Ritiene toomodify disponibile in questo percorso di output.
>
>

## <a name="step-8-delete-containers"></a>Passaggio 8: Eliminare i contenitori
Poiché vengono addebitati i dati che si trovano in archiviazione di Azure, è sempre tooremove una buona idea tutti i blob che non sono più necessari per i processi Batch. In *python_tutorial_client.py*, questa operazione viene eseguita con le tre chiamate troppo[BlockBlobService.delete_container][py_delete_container]:

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a>Passaggio 9: Eliminare il processo di hello e pool hello
Nel passaggio finale hello, si è richiesta toodelete hello processo e hello del pool che sono state create da hello *python_tutorial_client.py* script. Anche se non vengono addebitati costi per i processi e le attività in sé, *vengono* addebiti costi per i nodi di calcolo. È quindi consigliabile allocare i nodi solo in base alla necessità. L'eliminazione dei pool inutilizzati può fare parte del processo di manutenzione.

BatchServiceClient Hello [JobOperations] [ py_job] e [PoolOperations] [ py_pool] dispongono di metodi di eliminazione corrispondente, ovvero chiamato se si conferma l'eliminazione:

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> Occorre ricordare che vengono effettuati addebiti per le risorse di calcolo e che l'eliminazione di pool inutilizzati consente di ridurre al minimo i costi. Inoltre, tenere presente che l'eliminazione di un pool Elimina tutti i nodi di calcolo all'interno di tale pool e che tutti i dati nei nodi hello sarà irreversibili dopo l'eliminazione di pool hello.
>
>

## <a name="run-hello-sample-script"></a>Eseguire uno script di esempio hello
Quando si esegue hello *python_tutorial_client.py* script dall'esercitazione hello [nell'esempio di codice][github_article_samples], output della console hello è simile toohello seguente. Vi sarà una pausa in `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` mentre vengono creati i nodi di calcolo del pool di hello, avviato, e vengono eseguiti i comandi di hello in attività di avvio del pool di hello. Hello utilizzare [portale di Azure] [ azure_portal] toomonitor il pool, nodi di calcolo, processi e attività durante e dopo l'esecuzione. Hello utilizzare [portale di Azure] [ azure_portal] o hello [Microsoft Azure Storage Explorer] [ storage_explorer] tooview le risorse di archiviazione hello (contenitori e BLOB) che vengono creati da un'applicazione hello.

> [!TIP]
> Eseguire hello *python_tutorial_client.py* generare uno script da all'interno di hello `azure-batch-samples/Python/Batch/article_samples` directory. Usa un percorso relativo per hello `common.helpers` importazione del modulo, pertanto si potrebbe osservare `ImportError: No module named 'common'` se non viene eseguito uno script di hello all'interno di questa directory.
>
>

Tempo di esecuzione tipico è **minuti circa 5-7** quando si esegue l'esempio hello nella configurazione predefinita.

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py toocontainer [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt toocontainer [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks toojob [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached hello 'Completed' state within hello specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] too/home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] too/home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] too/home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER tooexit...
```

## <a name="next-steps"></a>Passaggi successivi
È gratuita toomake modifiche troppo*python_tutorial_client.py* e *python_tutorial_task.py* tooexperiment con diversi scenari di calcolo. Ad esempio, provare ad aggiungere un ritardo di esecuzione troppo*python_tutorial_task.py* toosimulate lunga le attività e monitorarli nel portale di hello. Provare aggiungendo più attività o modificando il numero di hello di nodi di calcolo. Aggiungere logica toocheck per e consentire l'utilizzo di hello di un tempo di esecuzione toospeed pool esistenti.

Ora che si ha familiarità con hello base del flusso di lavoro di una soluzione di Batch, è ora toodig in toohello funzionalità aggiuntive di hello servizio Batch.

* Hello revisione [funzionalità Panoramica di Azure Batch](batch-api-basics.md) articolo, è consigliabile se si è nuovo servizio toohello.
* Inizio nel hello altri articoli di sviluppo di Batch in **sviluppo approfondito** in hello [il percorso di apprendimento Batch][batch_learning_path].
* Estrarre un'implementazione diversa di elaborazione hello "top N parole" del carico di lavoro con Batch in hello [TopNWords] [ github_topnwords] esempio.

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[blog_linux]: http://blogs.technet.com/b/windowshpc/archive/2016/03/30/introducing-linux-support-on-azure-batch.aspx
[crypto]: https://cryptography.io/en/latest/
[crypto_install]: https://cryptography.io/en/latest/installation/
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[github_article_samples]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/article_samples

[nuget_packagemgr]: https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build

[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_batchserviceclient]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html#azure.batch.BatchServiceClient
[py_blockblobservice]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.blockblobservice.html#azure.storage.blob.blockblobservice.BlockBlobService
[py_cloudtask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_cs_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudServiceConfiguration
[py_delete_container]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.delete_container
[py_gen_blob_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_blob_shared_access_signature
[py_gen_container_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_container_shared_access_signature
[py_image_ref]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_job]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.JobOperations
[py_jobpreptask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobPreparationTask
[py_jobreltask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobReleaseTask
[py_list_skus]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[py_make_blob_url]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.make_blob_url
[py_pool]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.PoolOperations
[py_pooladdparam]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolAddParameter
[py_poolinfo]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolInformation
[py_resource_file]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ResourceFile
[py_samples_github]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_task]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_taskstate]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.TaskState
[py_vm_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.VirtualMachineConfiguration
[pypi_batch]: https://pypi.python.org/pypi/azure-batch
[pypi_storage]: https://pypi.python.org/pypi/azure-storage
[pypi_install]: https://packaging.python.org/installing/
[storage_explorer]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/products/vs-2015-product-editions
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-python-tutorial/batch_workflow_01_sm.png "Creare contenitori in Archiviazione di Azure"
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "Attività di caricamento dell'applicazione e di input (dati) file toocontainers"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Creare un pool di Batch"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Creare un processo di Batch"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "Aggiungere attività toojob"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "Monitorare le attività"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Scaricare l'output delle attività dal servizio di archiviazione"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Flusso di lavoro della soluzione Batch (diagramma completo)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "Credenziali di Batch nel portale"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "Credenziali del servizio di archiviazione nel portale"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Flusso di lavoro della soluzione Batch (diagramma minimo)"
