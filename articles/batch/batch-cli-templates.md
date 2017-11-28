---
title: Azure Batch aaaRun processi end-to-end senza scrivere codice (anteprima) | Documenti Microsoft
description: "Creare il file di modello per hello Azure CLI toocreate Batch pool, processi e attività."
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="2f4dd-103">Usare il trasferimento di file e i modelli dell'interfaccia della riga di comando di Azure Batch (anteprima)</span><span class="sxs-lookup"><span data-stu-id="2f4dd-103">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="2f4dd-104">Utilizzando hello CLI di Azure, è possibile toorun i processi Batch senza scrivere codice.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-104">Using hello Azure CLI it is possible toorun Batch jobs without writing code.</span></span>

<span data-ttu-id="2f4dd-105">File di modello possono essere creati e usati con hello CLI di Azure che consentono di pool di Batch, i processi e attività toobe creato.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-105">Template files can be created and used with hello Azure CLI that allow Batch pools, jobs, and tasks toobe created.</span></span> <span data-ttu-id="2f4dd-106">File di input del processo possono essere caricati facilmente all'account di archiviazione hello associato hello Batch account e processo di output file scaricati.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-106">Job input files can be easily uploaded to hello storage account associated with hello Batch account and job output files downloaded.</span></span>

## <a name="overview"></a><span data-ttu-id="2f4dd-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2f4dd-107">Overview</span></span>

<span data-ttu-id="2f4dd-108">Consente a un toohello estensione CLI di Azure Batch toobe utilizzato end-to-end dagli utenti che non sono sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-108">An extension toohello Azure CLI enables Batch toobe used end-to-end by users who are not developers.</span></span> <span data-ttu-id="2f4dd-109">È possibile creare un pool, caricato i dati di input, processi e attività associate creata, e hello risultante output dati scaricati: nessun codice necessario, hello CLI viene utilizzato direttamente o viene integrato negli script.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-109">A pool can be created, input data uploaded, jobs and associated tasks created, and hello resulting output data downloaded – no code required, hello CLI being used directly or being integrated into scripts.</span></span>

<span data-ttu-id="2f4dd-110">Compilazione di modelli di batch in hello [le funzionalità di supporto Batch hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) file JSON che consente i valori delle proprietà toospecify per la creazione di hello di pool di processi, attività e altri elementi.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-110">Batch templates build on hello [existing Batch support in hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) that allows JSON files toospecify property values for hello creation of pools, jobs, tasks, and other items.</span></span> <span data-ttu-id="2f4dd-111">Con i modelli di Batch, hello seguenti funzionalità sono state aggiunte su ciò che è possibile con i file JSON hello:</span><span class="sxs-lookup"><span data-stu-id="2f4dd-111">With Batch templates, hello following capabilities are added over what is possible with hello JSON files:</span></span>

-   <span data-ttu-id="2f4dd-112">È possibile definire parametri.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-112">Parameters can be defined.</span></span> <span data-ttu-id="2f4dd-113">Quando si utilizza il modello di hello, solo i valori di parametro hello sono elemento hello toocreate specificato, con altri valori di proprietà di elemento specificato nel corpo del modello hello.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-113">When hello template is used, only hello parameter values are specified toocreate hello item, with other item property values being specified in hello template body.</span></span> <span data-ttu-id="2f4dd-114">Gli utenti in grado di riconoscere che batch e il toobe applicazioni eseguiti dal Batch è possono creare modelli, specificare i pool di processi e i valori delle proprietà di attività.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-114">A user who understands Batch and the applications toobe run by Batch can create templates, specifying pool, job, and task property values.</span></span> <span data-ttu-id="2f4dd-115">Un utente minori che hanno familiarità con le applicazioni e/o di Batch deve solo i valori hello toospecify per i parametri di hello definito.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-115">A user less familiar with Batch and/or the applications only needs toospecify hello values for hello defined parameters.</span></span>

-   <span data-ttu-id="2f4dd-116">Factory delle attività processo creare uno o più attività associata a un processo, evitando hello necessario per molti toobe le definizioni di attività creata e allo scopo di semplificare notevolmente l'invio di processi.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-116">Job task factories create one or more tasks associated with a job, avoiding hello need for many task definitions toobe created and significantly simplifying job submission.</span></span>


<span data-ttu-id="2f4dd-117">File di dati di input devono toobe forniti per i processi e i file di dati di output vengono spesso generati.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-117">Input data files need toobe supplied for jobs and output data files are often produced.</span></span> <span data-ttu-id="2f4dd-118">È associato un account di archiviazione, per impostazione predefinita, con ogni Batch account e i file possono essere trasferiti facilmente tooand da questo account di archiviazione usando l'interfaccia CLI, senza scrivere codice e credenziali di archiviazione non necessaria.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-118">A storage account is associated, by default, with each Batch account and files can be easily transferred tooand from this storage account using the CLI, with no coding and no storage credentials required.</span></span>

<span data-ttu-id="2f4dd-119">Ad esempio, [ffmpeg](http://ffmpeg.org/) è una diffusa applicazione che elabora i file audio e video.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-119">For example, [ffmpeg](http://ffmpeg.org/) is a popular application that processes audio and video files.</span></span> <span data-ttu-id="2f4dd-120">Hello CLI di Azure Batch può essere utilizzato tooinvoke ffmpeg tootranscode origine file video toodifferent risoluzioni.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-120">hello Azure Batch CLI can be used tooinvoke ffmpeg tootranscode source video files toodifferent resolutions.</span></span>

-   <span data-ttu-id="2f4dd-121">Viene creato un modello di pool.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-121">A pool template is created.</span></span> <span data-ttu-id="2f4dd-122">utente Hello creazione modello hello sa come toocall hello ffmpeg applicazione e i relativi requisiti; specifichino hello OS appropriato, VM dimensioni, come ffmpeg sia installato (da un pacchetto di applicazione o tramite Gestione pacchetti, ad esempio) e altri valori di proprietà del pool.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-122">hello user creating hello template knows how toocall hello ffmpeg application and its requirements; they specify hello appropriate OS, VM size, how ffmpeg is installed (from an application package or using a package manager, for example), and other pool property values.</span></span> <span data-ttu-id="2f4dd-123">I parametri vengono creati quando si utilizza il modello di hello, solo l'id del pool hello e numero di macchine virtuali necessario toobe specificato.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-123">Parameters are created so when hello template is used, only hello pool id and number of VMs need toobe specified.</span></span>

-   <span data-ttu-id="2f4dd-124">Viene creato un modello di processo.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-124">A job template is created.</span></span> <span data-ttu-id="2f4dd-125">modello di Hello utente Creazione hello sa come ffmpeg esigenze toobe richiamato una risoluzione diversa tootranscode origine video tooa e specifica riga di comando attività hello; Inoltre, che sappiano che vi sia una cartella contenente file video di origine hello, con un'attività necessaria per ogni file di input.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-125">hello user creating hello template knows how ffmpeg needs toobe invoked tootranscode source video tooa different resolution and specifies hello task command line; they also know that there is a folder containing hello source video files, with a task required per input file.</span></span>

-   <span data-ttu-id="2f4dd-126">Un utente finale con un set di file video tootranscode crea innanzitutto un pool usando il modello di pool di hello, specificare solo l'id del pool hello e numero di macchine virtuali necessarie.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-126">An end user with a set of video files tootranscode first creates a pool using hello pool template, specifying only hello pool id and number of VMs required.</span></span> <span data-ttu-id="2f4dd-127">È quindi possibile caricare tootranscode i file di origine hello.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-127">They can then upload hello source files tootranscode.</span></span> <span data-ttu-id="2f4dd-128">Un processo potrà quindi essere inviato utilizzando il modello di processo hello, specificare solo l'id del pool hello e percorso dei file di origine hello caricato.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-128">A job can then be submitted using hello job template, specifying only hello pool id and location of hello source files uploaded.</span></span> <span data-ttu-id="2f4dd-129">processo Batch Hello viene creato con un'attività per ciascun file di input in corso la generazione.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-129">hello Batch job is created, with one task per input file being generated.</span></span> <span data-ttu-id="2f4dd-130">Infine, i file di output di hello transcodificato possono essere il download.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-130">Finally, hello transcoded output files can be download.</span></span>

## <a name="installation"></a><span data-ttu-id="2f4dd-131">Installazione</span><span class="sxs-lookup"><span data-stu-id="2f4dd-131">Installation</span></span>

<span data-ttu-id="2f4dd-132">funzionalità di trasferimento di modello e un file Hello richiedono toobe un'estensione installata.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-132">hello template and file transfer capabilities require an extension toobe installed.</span></span>

<span data-ttu-id="2f4dd-133">Per istruzioni su come tooinstall hello CLI di Azure vedere [installare Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2f4dd-133">For instructions on how tooinstall hello Azure CLI see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="2f4dd-134">Una volta hello che CLI di Azure è stato installato, hello Batch estensione può essere installata usando il comando CLI seguente:</span><span class="sxs-lookup"><span data-stu-id="2f4dd-134">Once hello Azure CLI has been installed, hello Batch extension can be installed using the following CLI command:</span></span>

```azurecli
az component update --add batch-extensions --allow-third-party
```

<span data-ttu-id="2f4dd-135">Per ulteriori informazioni su hello estensione Batch, vedere [Microsoft Azure Batch CLI Extensions per Windows, Mac e Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span><span class="sxs-lookup"><span data-stu-id="2f4dd-135">For more information about hello Batch extension, see [Microsoft Azure Batch CLI Extensions for Windows, Mac and Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span></span>

## <a name="templates"></a><span data-ttu-id="2f4dd-136">Modelli</span><span class="sxs-lookup"><span data-stu-id="2f4dd-136">Templates</span></span>

<span data-ttu-id="2f4dd-137">Hello CLI di Azure Batch consente di elementi, ad esempio pool di processi e attività toobe creato specificando un file JSON che contengono valori e nomi di proprietà.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-137">hello Azure Batch CLI allows items such as pools, jobs, and tasks toobe created by specifying a JSON file containing property names and values.</span></span> <span data-ttu-id="2f4dd-138">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2f4dd-138">For example:</span></span>

```azurecli
az batch pool create –-json-file AppPool.json
```

<span data-ttu-id="2f4dd-139">Modelli di Azure Batch sono modelli di gestione risorse tooAzure simile, funzionalità e di sintassi.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-139">Azure Batch templates are similar tooAzure Resource Manager templates, in functionality and syntax.</span></span> <span data-ttu-id="2f4dd-140">File JSON che contengono valori e nomi di proprietà di elementi, ma aggiungere hello seguendo i concetti principali sono:</span><span class="sxs-lookup"><span data-stu-id="2f4dd-140">They are JSON files that contain item property names and values, but add hello following main concepts:</span></span>

-   <span data-ttu-id="2f4dd-141">**Parametri**</span><span class="sxs-lookup"><span data-stu-id="2f4dd-141">**Parameters**</span></span>

    -   <span data-ttu-id="2f4dd-142">Consenti toobe di valori di proprietà specificato in una sezione del corpo, con la necessità di toobe fornito quando si utilizza il modello di hello solo valori di parametro.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-142">Allow property values toobe specified in a body section, with only parameter values needing toobe supplied when hello template is used.</span></span> <span data-ttu-id="2f4dd-143">Ad esempio, è stato possibile collocare definizione completa di hello per un pool nel corpo di hello e un solo parametro definito per l'id del pool. solo una stringa id pool deve pertanto toocreate toobe fornito un pool.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-143">For example, hello complete definition for a pool could be placed in hello body and only one parameter defined for pool id; only a pool id string therefore needs toobe supplied toocreate a pool.</span></span>
        
    -   <span data-ttu-id="2f4dd-144">corpo del modello Hello può essere creato da un utente con le informazioni di Batch e hello applicazioni toobe eseguito dal Batch. Quando si utilizza il modello di hello, è necessario specificare solo i valori per parametri definiti dall'autore hello.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-144">hello template body can be authored by someone with knowledge of Batch and hello applications toobe run by Batch; only values for hello author-defined parameters must be supplied when hello template is used.</span></span> <span data-ttu-id="2f4dd-145">Un utente senza hello Batch approfondite e/o informazioni sulle applicazioni è pertanto possono utilizzare i modelli.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-145">A user without hello in-depth Batch and/or application knowledge can therefore use the templates.</span></span>

-   <span data-ttu-id="2f4dd-146">**Variabili**</span><span class="sxs-lookup"><span data-stu-id="2f4dd-146">**Variables**</span></span>

    -   <span data-ttu-id="2f4dd-147">Consenti toobe valori di parametro semplici o complesse specificato in un'unica posizione e utilizzata in uno o più posizioni nel corpo del modello hello.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-147">Allow simple or complex parameter values toobe specified in one place and used in one or more places in hello template body.</span></span> <span data-ttu-id="2f4dd-148">Le variabili possono semplificare e ridurre le dimensioni di hello del modello di hello, così come renderla più gestibile con una proprietà toochange percorso il cui valore può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-148">Variables can simplify and reduce hello size of hello template, as well as make it more maintainable by having one location toochange properties whose value may change.</span></span>

-   <span data-ttu-id="2f4dd-149">**Costrutti di livello superiore**</span><span class="sxs-lookup"><span data-stu-id="2f4dd-149">**Higher-level constructs**</span></span>

    -   <span data-ttu-id="2f4dd-150">Alcuni costrutti di livello superiore sono disponibili nel modello di hello che non sono ancora disponibili in hello API Batch.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-150">Some higher-level constructs are available in hello template that are not yet available in hello Batch APIs.</span></span> <span data-ttu-id="2f4dd-151">Ad esempio, una factory delle attività può essere definita in un modello di processo che crea più attività per il processo di hello utilizzando una definizione di attività comuni.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-151">For example, a task factory can be defined in a job template that creates multiple tasks for hello job using a common task definition.</span></span> <span data-ttu-id="2f4dd-152">Questi costrutti evitare hello necessario toocode per dinamicamente creare più file JSON, ad esempio un file per ogni attività, nonché per creare script applicazioni tooinstall file tramite Gestione pacchetti, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-152">These constructs avoid hello need toocode to dynamically create multiple JSON files, such as one file per task, as well as create script files tooinstall applications via a package manager, for example.</span></span>

    -   <span data-ttu-id="2f4dd-153">In alcuni punti, dove applicabile, che questi costrutti possono essere aggiunto toothe Batch al servizio e disponibile in hello API Batch, le interfacce utente e così via.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-153">At some point, where applicable, these constructs may be added toothe Batch service and available in hello Batch APIs, UIs, etc.</span></span>

### <a name="pool-templates"></a><span data-ttu-id="2f4dd-154">Modelli di pool</span><span class="sxs-lookup"><span data-stu-id="2f4dd-154">Pool templates</span></span>

<span data-ttu-id="2f4dd-155">Il modello di pool di hello sono inoltre supportate le funzionalità di modelli standard toohello di parametri e variabili, hello seguenti costrutti di livello superiore:</span><span class="sxs-lookup"><span data-stu-id="2f4dd-155">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello pool template:</span></span>

-   <span data-ttu-id="2f4dd-156">**Riferimenti ai pacchetti**</span><span class="sxs-lookup"><span data-stu-id="2f4dd-156">**Package references**</span></span>

    -   <span data-ttu-id="2f4dd-157">Consente facoltativamente nodi toopool di software toobe copiati tramite pacchetti di gestori.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-157">Optionally allows software toobe copied toopool nodes by using package managers.</span></span> <span data-ttu-id="2f4dd-158">gestione di pacchetti Hello e id del pacchetto vengono specificati.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-158">hello package manager and package id are specified.</span></span> <span data-ttu-id="2f4dd-159">Viene toodeclare in grado di uno o più pacchetti evita hello necessità toocreate uno script che recupera i pacchetti hello necessario, installare script hello ed eseguire script hello in ogni nodo del pool.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-159">Being able toodeclare one or more packages avoids hello need toocreate a script that gets hello required packages, install hello script, and run hello script on each pool node.</span></span>

<span data-ttu-id="2f4dd-160">Hello di seguito è riportato un esempio di un modello che crea un pool di macchine virtuali Linux con ffmpeg installato e solo richiede un pool id stringa e hello numero di macchine virtuali toobe fornito toouse:</span><span class="sxs-lookup"><span data-stu-id="2f4dd-160">hello following is an example of a template that creates a pool of Linux VMs with ffmpeg installed and only requires a pool id string and hello number of VMs toobe supplied toouse:</span></span>

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

<span data-ttu-id="2f4dd-161">Se è stato denominato file del modello di hello _pool ffmpeg.json_, quindi il modello di hello viene richiamato come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="2f4dd-161">If hello template file was named _pool-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a><span data-ttu-id="2f4dd-162">Modelli di processo</span><span class="sxs-lookup"><span data-stu-id="2f4dd-162">Job templates</span></span>

<span data-ttu-id="2f4dd-163">Funzionalità di modelli standard toohello di parametri e variabili, hello seguenti costrutti di livello superiore sono inoltre supportate dal modello di processo hello:</span><span class="sxs-lookup"><span data-stu-id="2f4dd-163">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello job template:</span></span>

-   <span data-ttu-id="2f4dd-164">**Factory di attività**</span><span class="sxs-lookup"><span data-stu-id="2f4dd-164">**Task factory**</span></span>

    -   <span data-ttu-id="2f4dd-165">Vengono create più attività per un processo da una definizione di attività.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-165">Creates multiple tasks for a job from one task definition.</span></span> <span data-ttu-id="2f4dd-166">Sono supportati tre tipi di factory di attività: processo parametrico di organizzazione, attività per file e raccolta di attività.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-166">Three types of task factory are supported – parametric sweep, task per file, and task collection.</span></span>

<span data-ttu-id="2f4dd-167">Hello Ecco un esempio di un modello che crea un processo che utilizza ffmpeg per eseguire la transcodifica MP4 file video tooone di due risoluzioni inferiori, con un'attività creata per ogni file video di origine:</span><span class="sxs-lookup"><span data-stu-id="2f4dd-167">hello following is an example of a template that creates a job that uses ffmpeg to transcode MP4 video files tooone of two lower resolutions, with one task created per source video file:</span></span>

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

<span data-ttu-id="2f4dd-168">Se è stato denominato file del modello di hello _processo ffmpeg.json_, quindi il modello di hello viene richiamato come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="2f4dd-168">If hello template file was named _job-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a><span data-ttu-id="2f4dd-169">Gruppi e trasferimenti di file</span><span class="sxs-lookup"><span data-stu-id="2f4dd-169">File groups and file transfer</span></span>

<span data-ttu-id="2f4dd-170">La maggior parte dei processi e delle attività richiede file di input e produce file di output.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-170">Most jobs and tasks require input files and produce output files.</span></span> <span data-ttu-id="2f4dd-171">Entrambi i file di input e i file di output è in genere necessario toobe trasferiti, dal nodo di toohello hello client o dal client di toohello nodo hello.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-171">Both input files and output files typically need toobe transferred, either from hello client toohello node, or from hello node toohello client.</span></span> <span data-ttu-id="2f4dd-172">Hello estensione CLI di Azure Batch estrae il trasferimento di file di stoccaggio e utilizza l'account di archiviazione hello viene creato per impostazione predefinita per ogni account Batch.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-172">hello Azure Batch CLI extension abstracts away file transfer and utilizes hello storage account that is created by default for each Batch account.</span></span>

<span data-ttu-id="2f4dd-173">Un gruppo di file equivale contenitore tooa creati in hello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-173">A file group equates tooa container that is created in hello Azure storage account.</span></span> <span data-ttu-id="2f4dd-174">gruppo di file Hello abbia le sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-174">hello file group may have subfolders.</span></span>

<span data-ttu-id="2f4dd-175">Hello estensione CLI Batch sono disponibili comandi per il caricamento di file dal gruppo di file specificato tooa client e il download dei file dal client tooa gruppo di file specificato hello.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-175">hello Batch CLI extension provides commands for uploading files from client tooa specified file group and downloading files from hello specified file group tooa client.</span></span>

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

<span data-ttu-id="2f4dd-176">Modelli di processo e di pool consentono i file archiviati nel file gruppi toobe specificata per la copia sui nodi pool o off pool nodi, eseguire il gruppo di file tooa.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-176">Pool and job templates allow files stored in file groups toobe specified for copy onto pool nodes or off pool nodes back tooa file group.</span></span> <span data-ttu-id="2f4dd-177">Ad esempio, nel modello di processo specificato in precedenza, hello file gruppo "ffmpeg-input" è specificato per la factory delle attività hello come percorso di hello hello video di file di origine copiato nodo hello per la transcodifica; file gruppo "ffmpeg-output di Hello" viene utilizzato come percorso in cui i file di output di hello transcodificato hello copiati nodo hello toofrom in esecuzione di ogni attività.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-177">For example, in the job template specified previously, hello file group “ffmpeg-input” is specified for hello task factory as hello location of hello source video files copied down onto hello node for transcoding; hello file group “ffmpeg-output” is used as hello location where hello transcoded output files are copied toofrom hello node running each task.</span></span>

## <a name="summary"></a><span data-ttu-id="2f4dd-178">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="2f4dd-178">Summary</span></span>

<span data-ttu-id="2f4dd-179">Supporto per il trasferimento di modello e un file attualmente sono stati aggiunti solo toohello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-179">Template and file transfer support have currently been added only toohello Azure CLI.</span></span> <span data-ttu-id="2f4dd-180">obiettivo di Hello è pubblico hello tooexpand utilizzabile toousers Batch che non richiedono codice toodevelop utilizzando hello API Batch, ad esempio i ricercatori, gli utenti IT e così via.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-180">hello goal is tooexpand hello audience that can use Batch toousers who do not need toodevelop code using hello Batch APIs, such as researchers, IT users, and so on.</span></span> <span data-ttu-id="2f4dd-181">Senza la generazione di codice, gli utenti esperti di Azure, Batch e hello applicazioni toobe eseguire dal Batch possono creare modelli per la creazione di pool e processo.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-181">Without coding, users with knowledge of Azure, Batch, and hello applications toobe run by Batch can create templates for pool and job creation.</span></span> <span data-ttu-id="2f4dd-182">Con parametri di modello, gli utenti senza una conoscenza approfondita di Batch e hello applicazioni possono utilizzare i modelli di hello.</span><span class="sxs-lookup"><span data-stu-id="2f4dd-182">With template parameters, users without detailed knowledge of Batch and hello applications can use hello templates.</span></span>

<span data-ttu-id="2f4dd-183">Provare a hello estensione Batch per hello CLI di Azure e fornire commenti o suggerimenti, entrambi hello in commenti per l'articolo o tramite hello [forum di Azure Batch](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span><span class="sxs-lookup"><span data-stu-id="2f4dd-183">Try out hello Batch extension for hello Azure CLI and provide us with any feedback or suggestions, either in hello comments for this article or via hello [Azure Batch forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f4dd-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f4dd-184">Next steps</span></span>

- <span data-ttu-id="2f4dd-185">Vedere post sul blog di modelli di hello Batch: [i processi in esecuzione Batch di Azure mediante hello CLI di Azure: è richiesto alcun codice](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span><span class="sxs-lookup"><span data-stu-id="2f4dd-185">See hello Batch templates blog post: [Running Azure Batch jobs using hello Azure CLI – no code required](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span></span>
- <span data-ttu-id="2f4dd-186">Installazione e utilizzo della documentazione, esempi e codice sorgente sono disponibili in hello [repository GitHub Azure](https://github.com/Azure/azure-batch-cli-extensions).</span><span class="sxs-lookup"><span data-stu-id="2f4dd-186">Detailed installation and usage documentation, samples, and source code are available in hello [Azure GitHub repository](https://github.com/Azure/azure-batch-cli-extensions).</span></span>
