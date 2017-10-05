---
title: Eseguire processi di Azure Batch end-to-end senza scrivere codice (anteprima) | Microsoft Docs
description: "Creare file modello per l'interfaccia della riga di comando di Azure per creare pool, processi e attività di Batch."
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
ms.openlocfilehash: 6b91466da46d1f4ca9f25bf1718be783603efc58
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="6c3ae-103">Usare il trasferimento di file e i modelli dell'interfaccia della riga di comando di Azure Batch (anteprima)</span><span class="sxs-lookup"><span data-stu-id="6c3ae-103">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="6c3ae-104">Usando l'interfaccia della riga di comando di Azure è possibile eseguire processi di Batch senza scrittura del codice.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-104">Using the Azure CLI it is possible to run Batch jobs without writing code.</span></span>

<span data-ttu-id="6c3ae-105">È possibile creare e usare con l'interfaccia della riga di comando di Azure file modello che consentono la creazione di pool, processi e attività di Batch.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-105">Template files can be created and used with the Azure CLI that allow Batch pools, jobs, and tasks to be created.</span></span> <span data-ttu-id="6c3ae-106">I file di input dei processi possono essere caricati facilmente nell'account di archiviazione associato all'account Batch. È inoltre possibile scaricare i file di output dei processi.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-106">Job input files can be easily uploaded to the storage account associated with the Batch account and job output files downloaded.</span></span>

## <a name="overview"></a><span data-ttu-id="6c3ae-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6c3ae-107">Overview</span></span>

<span data-ttu-id="6c3ae-108">Un'estensione dell'interfaccia della riga di comando di Azure consente a utenti non sviluppatori di usare Batch end-to-end.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-108">An extension to the Azure CLI enables Batch to be used end-to-end by users who are not developers.</span></span> <span data-ttu-id="6c3ae-109">È possibile creare un pool, caricare i dati di input, creare processi e attività associate e scaricare i dati di output risultanti senza necessità di codice, usando direttamente l'interfaccia della riga di comando o integrandola in script.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-109">A pool can be created, input data uploaded, jobs and associated tasks created, and the resulting output data downloaded – no code required, the CLI being used directly or being integrated into scripts.</span></span>

<span data-ttu-id="6c3ae-110">I modelli di Batch sono basati sul [supporto di Batch esistente nell'interfaccia della riga di comando di Azure](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation), che consente ai file JSON di specificare i valori delle proprietà per la creazione di pool, processi, attività e altri elementi.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-110">Batch templates build on the [existing Batch support in the Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) that allows JSON files to specify property values for the creation of pools, jobs, tasks, and other items.</span></span> <span data-ttu-id="6c3ae-111">Con i modelli di Batch, vengono aggiunte le funzionalità seguenti a ciò che è possibile fare con i file JSON:</span><span class="sxs-lookup"><span data-stu-id="6c3ae-111">With Batch templates, the following capabilities are added over what is possible with the JSON files:</span></span>

-   <span data-ttu-id="6c3ae-112">È possibile definire parametri.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-112">Parameters can be defined.</span></span> <span data-ttu-id="6c3ae-113">Quando viene usato il modello, per creare l'elemento vengono specificati solo i valori dei parametri, mentre gli altri valori delle proprietà dell'elemento sono specificati nel corpo del modello.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-113">When the template is used, only the parameter values are specified to create the item, with other item property values being specified in the template body.</span></span> <span data-ttu-id="6c3ae-114">Un utente che conosce Batch e le applicazioni che devono essere eseguite da Batch può creare modelli, specificando i valori delle proprietà di pool, processi e attività.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-114">A user who understands Batch and the applications to be run by Batch can create templates, specifying pool, job, and task property values.</span></span> <span data-ttu-id="6c3ae-115">Un utente che ha meno familiarità con Batch e/o con le applicazioni può specificare solo i valori per i parametri definiti.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-115">A user less familiar with Batch and/or the applications only needs to specify the values for the defined parameters.</span></span>

-   <span data-ttu-id="6c3ae-116">Le factory delle attività di processo creano una o più attività associate a un processo, evitando di dover creare diverse definizioni di attività e semplificando così notevolmente l'invio di processi.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-116">Job task factories create one or more tasks associated with a job, avoiding the need for many task definitions to be created and significantly simplifying job submission.</span></span>


<span data-ttu-id="6c3ae-117">È necessario fornire file di dati di input per i processi e spesso vengono generati file di dati di output.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-117">Input data files need to be supplied for jobs and output data files are often produced.</span></span> <span data-ttu-id="6c3ae-118">Per impostazione predefinita, a ogni account Batch è associato un account di archiviazione e i file possono essere facilmente trasferiti da e verso questo account di archiviazione usando l'interfaccia della riga di comando, senza necessità di codici o credenziali di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-118">A storage account is associated, by default, with each Batch account and files can be easily transferred to and from this storage account using the CLI, with no coding and no storage credentials required.</span></span>

<span data-ttu-id="6c3ae-119">Ad esempio, [ffmpeg](http://ffmpeg.org/) è una diffusa applicazione che elabora i file audio e video.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-119">For example, [ffmpeg](http://ffmpeg.org/) is a popular application that processes audio and video files.</span></span> <span data-ttu-id="6c3ae-120">L'interfaccia della riga di comando di Azure Batch può essere usata per richiamare ffmpeg per la transcodifica di file video di origine in file con risoluzioni diverse.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-120">The Azure Batch CLI can be used to invoke ffmpeg to transcode source video files to different resolutions.</span></span>

-   <span data-ttu-id="6c3ae-121">Viene creato un modello di pool.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-121">A pool template is created.</span></span> <span data-ttu-id="6c3ae-122">L'utente che crea il modello sa come chiamare l'applicazione ffmpeg e conosce i relativi requisiti. Specifica i valori appropriati per sistema operativo, dimensioni VM, modalità di installazione di ffmpeg (ad esempio da un pacchetto dell'applicazione o usando uno strumento di gestione pacchetti) e altri valori delle proprietà del pool.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-122">The user creating the template knows how to call the ffmpeg application and its requirements; they specify the appropriate OS, VM size, how ffmpeg is installed (from an application package or using a package manager, for example), and other pool property values.</span></span> <span data-ttu-id="6c3ae-123">I parametri vengono creati in modo che quando il modello viene usato, è necessario specificare solo l'ID del pool e il numero di VM.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-123">Parameters are created so when the template is used, only the pool id and number of VMs need to be specified.</span></span>

-   <span data-ttu-id="6c3ae-124">Viene creato un modello di processo.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-124">A job template is created.</span></span> <span data-ttu-id="6c3ae-125">L'utente che crea il modello sa come si deve richiamare ffmpeg per eseguire la transcodifica di un video di origine in un file con una risoluzione diversa e specifica la riga di comando dell'attività. L'utente sa inoltre che è presente una cartella contenente i file video di origine, con un'attività necessaria per ogni file di input.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-125">The user creating the template knows how ffmpeg needs to be invoked to transcode source video to a different resolution and specifies the task command line; they also know that there is a folder containing the source video files, with a task required per input file.</span></span>

-   <span data-ttu-id="6c3ae-126">Un utente finale con un set di file video di cui eseguire la transcodifica deve prima di tutto creare un pool usando il modello di pool, specificando solo l'ID del pool e il numero di VM necessarie.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-126">An end user with a set of video files to transcode first creates a pool using the pool template, specifying only the pool id and number of VMs required.</span></span> <span data-ttu-id="6c3ae-127">Può quindi caricare i file di origine per la transcodifica.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-127">They can then upload the source files to transcode.</span></span> <span data-ttu-id="6c3ae-128">È quindi possibile inviare un processo usando il modello di processo, specificando solo l'ID del pool e il percorso dei file di origine caricati.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-128">A job can then be submitted using the job template, specifying only the pool id and location of the source files uploaded.</span></span> <span data-ttu-id="6c3ae-129">Viene creato il processo di batch con un'attività per ogni file di input generato.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-129">The Batch job is created, with one task per input file being generated.</span></span> <span data-ttu-id="6c3ae-130">Infine, i file di output transcodificati possono essere scaricati.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-130">Finally, the transcoded output files can be download.</span></span>

## <a name="installation"></a><span data-ttu-id="6c3ae-131">Installare</span><span class="sxs-lookup"><span data-stu-id="6c3ae-131">Installation</span></span>

<span data-ttu-id="6c3ae-132">Il modello e le funzionalità di trasferimento di file richiedono l'installazione di un'estensione.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-132">The template and file transfer capabilities require an extension to be installed.</span></span>

<span data-ttu-id="6c3ae-133">Per istruzioni su come installare l'interfaccia della riga di comando di Azure, vedere [Installare l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6c3ae-133">For instructions on how to install the Azure CLI see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="6c3ae-134">Una volta installata l'interfaccia della riga di comando di Azure, è possibile installare l'estensione di Batch utilizzando il seguente comando CLI:</span><span class="sxs-lookup"><span data-stu-id="6c3ae-134">Once the Azure CLI has been installed, the Batch extension can be installed using the following CLI command:</span></span>

```azurecli
az component update --add batch-extensions --allow-third-party
```

<span data-ttu-id="6c3ae-135">Per ulteriori informazioni sull'estensione del Batch, vedere [Estensioni per interfaccia della riga di comando Batch di Microsoft Azure per Windows, Mac e Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span><span class="sxs-lookup"><span data-stu-id="6c3ae-135">For more information about the Batch extension, see [Microsoft Azure Batch CLI Extensions for Windows, Mac and Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span></span>

## <a name="templates"></a><span data-ttu-id="6c3ae-136">Modelli</span><span class="sxs-lookup"><span data-stu-id="6c3ae-136">Templates</span></span>

<span data-ttu-id="6c3ae-137">L'interfaccia della riga di comando di Azure Batch consente la creazione di elementi, come pool, processi e attività, specificando un file JSON contenente valori e nomi di proprietà.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-137">The Azure Batch CLI allows items such as pools, jobs, and tasks to be created by specifying a JSON file containing property names and values.</span></span> <span data-ttu-id="6c3ae-138">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6c3ae-138">For example:</span></span>

```azurecli
az batch pool create –-json-file AppPool.json
```

<span data-ttu-id="6c3ae-139">I modelli di Azure Batch sono simili ai modelli di Azure Resource Manager per quanto riguarda funzionalità e sintassi.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-139">Azure Batch templates are similar to Azure Resource Manager templates, in functionality and syntax.</span></span> <span data-ttu-id="6c3ae-140">Si tratta di file JSON contenenti nomi e valori delle proprietà degli elementi, ma con i seguenti importanti concetti aggiuntivi:</span><span class="sxs-lookup"><span data-stu-id="6c3ae-140">They are JSON files that contain item property names and values, but add the following main concepts:</span></span>

-   <span data-ttu-id="6c3ae-141">**Parameters**</span><span class="sxs-lookup"><span data-stu-id="6c3ae-141">**Parameters**</span></span>

    -   <span data-ttu-id="6c3ae-142">I valori delle proprietà possono essere specificati in una sezione del corpo, in modo che quando il modello viene usato sia necessario fornire solo i valori dei parametri.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-142">Allow property values to be specified in a body section, with only parameter values needing to be supplied when the template is used.</span></span> <span data-ttu-id="6c3ae-143">È ad esempio possibile inserire la definizione completa di un pool nel corpo e definire un solo parametro come ID del pool. Per creare un pool deve quindi essere fornita solo una stringa di ID del pool.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-143">For example, the complete definition for a pool could be placed in the body and only one parameter defined for pool id; only a pool id string therefore needs to be supplied to create a pool.</span></span>
        
    -   <span data-ttu-id="6c3ae-144">Il corpo del modello può essere creato da un utente che conosce Batch e le applicazioni che devono essere eseguite da Batch. Quando il modello viene usato, è necessario fornire solo i valori per i parametri definiti dall'autore.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-144">The template body can be authored by someone with knowledge of Batch and the applications to be run by Batch; only values for the author-defined parameters must be supplied when the template is used.</span></span> <span data-ttu-id="6c3ae-145">Un utente senza conoscenza approfondita di Batch e/o delle applicazioni può quindi usare i modelli.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-145">A user without the in-depth Batch and/or application knowledge can therefore use the templates.</span></span>

-   <span data-ttu-id="6c3ae-146">**Variabili**</span><span class="sxs-lookup"><span data-stu-id="6c3ae-146">**Variables**</span></span>

    -   <span data-ttu-id="6c3ae-147">È possibile specificare valori dei parametri semplici o complessi in un'unica posizione e usarli in una o più posizioni nel corpo del modello.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-147">Allow simple or complex parameter values to be specified in one place and used in one or more places in the template body.</span></span> <span data-ttu-id="6c3ae-148">Le variabili possono semplificare il modello e ridurne le dimensioni, oltre che rendere più facile la sua gestione, grazie alla presenza di un'unica posizione per modificare le proprietà il cui valore può cambiare.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-148">Variables can simplify and reduce the size of the template, as well as make it more maintainable by having one location to change properties whose value may change.</span></span>

-   <span data-ttu-id="6c3ae-149">**Costrutti di livello superiore**</span><span class="sxs-lookup"><span data-stu-id="6c3ae-149">**Higher-level constructs**</span></span>

    -   <span data-ttu-id="6c3ae-150">Nel modello sono disponibili alcuni costrutti di livello superiore che non sono ancora disponibili nelle API di Batch.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-150">Some higher-level constructs are available in the template that are not yet available in the Batch APIs.</span></span> <span data-ttu-id="6c3ae-151">È ad esempio possibile definire una factory di attività in un modello di processo che crea più attività per il processo usando una definizione di attività comune.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-151">For example, a task factory can be defined in a job template that creates multiple tasks for the job using a common task definition.</span></span> <span data-ttu-id="6c3ae-152">Questi costrutti evitano la necessità di usare codice per creare dinamicamente più file JSON, ad esempio un file per ogni attività, oltre che creare file di script per installare le applicazioni tramite uno strumento di gestione pacchetti, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-152">These constructs avoid the need to code to dynamically create multiple JSON files, such as one file per task, as well as create script files to install applications via a package manager, for example.</span></span>

    -   <span data-ttu-id="6c3ae-153">A un certo punto, dove applicabile, questi costrutti possono essere aggiunti al servizio Batch e disponibili nelle API, nell'interfaccia utente e in altre posizioni di Batch.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-153">At some point, where applicable, these constructs may be added to the Batch service and available in the Batch APIs, UIs, etc.</span></span>

### <a name="pool-templates"></a><span data-ttu-id="6c3ae-154">Modelli di pool</span><span class="sxs-lookup"><span data-stu-id="6c3ae-154">Pool templates</span></span>

<span data-ttu-id="6c3ae-155">Oltre alle funzionalità standard di parametri e variabili dei modelli, il modello di pool supporta i costrutti di livello superiore seguenti:</span><span class="sxs-lookup"><span data-stu-id="6c3ae-155">In addition to the standard template capabilities of parameters and variables, the following higher-level constructs are supported by the pool template:</span></span>

-   <span data-ttu-id="6c3ae-156">**Riferimenti ai pacchetti**</span><span class="sxs-lookup"><span data-stu-id="6c3ae-156">**Package references**</span></span>

    -   <span data-ttu-id="6c3ae-157">Facoltativamente, è possibile copiare il software in nodi del pool usando strumenti di gestione dei pacchetti.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-157">Optionally allows software to be copied to pool nodes by using package managers.</span></span> <span data-ttu-id="6c3ae-158">Vengono specificati lo strumento di gestione dei pacchetti e l'ID del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-158">The package manager and package id are specified.</span></span> <span data-ttu-id="6c3ae-159">La possibilità di dichiarare uno o più pacchetti evita la necessità di creare uno script che ottiene i pacchetti necessari, installare lo script ed eseguire lo script in ogni nodo del pool.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-159">Being able to declare one or more packages avoids the need to create a script that gets the required packages, install the script, and run the script on each pool node.</span></span>

<span data-ttu-id="6c3ae-160">Di seguito è riportato un esempio di un modello che crea un pool di VM Linux con l'applicazione ffmpeg installata e richiede solo una stringa di ID del pool e il numero di VM da fornire:</span><span class="sxs-lookup"><span data-stu-id="6c3ae-160">The following is an example of a template that creates a pool of Linux VMs with ffmpeg installed and only requires a pool id string and the number of VMs to be supplied to use:</span></span>

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "The number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "The pool id "
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

<span data-ttu-id="6c3ae-161">Se il nome del file del modello fosse _pool-ffmpeg.json_, sarebbe possibile richiamare il modello nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="6c3ae-161">If the template file was named _pool-ffmpeg.json_, then the template would be invoked as follows:</span></span>

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a><span data-ttu-id="6c3ae-162">Modelli di processo</span><span class="sxs-lookup"><span data-stu-id="6c3ae-162">Job templates</span></span>

<span data-ttu-id="6c3ae-163">Oltre alle funzionalità standard di parametri e variabili dei modelli, il modello di processo supporta i costrutti di livello superiore seguenti:</span><span class="sxs-lookup"><span data-stu-id="6c3ae-163">In addition to the standard template capabilities of parameters and variables, the following higher-level constructs are supported by the job template:</span></span>

-   <span data-ttu-id="6c3ae-164">**Factory di attività**</span><span class="sxs-lookup"><span data-stu-id="6c3ae-164">**Task factory**</span></span>

    -   <span data-ttu-id="6c3ae-165">Vengono create più attività per un processo da una definizione di attività.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-165">Creates multiple tasks for a job from one task definition.</span></span> <span data-ttu-id="6c3ae-166">Sono supportati tre tipi di factory di attività: processo parametrico di organizzazione, attività per file e raccolta di attività.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-166">Three types of task factory are supported – parametric sweep, task per file, and task collection.</span></span>

<span data-ttu-id="6c3ae-167">Di seguito è riportato un esempio di un modello che crea un processo che usa ffmpeg per eseguire la transcodifica di file video MP4 in file con una di due risoluzioni inferiori, con un'attività creata per ogni file video di origine:</span><span class="sxs-lookup"><span data-stu-id="6c3ae-167">The following is an example of a template that creates a job that uses ffmpeg to transcode MP4 video files to one of two lower resolutions, with one task created per source video file:</span></span>

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "The name of Azure Batch pool which runs the job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "The name of Azure Batch job"
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

<span data-ttu-id="6c3ae-168">Se il nome del file del modello fosse _job-ffmpeg.json_, sarebbe possibile richiamare il modello nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="6c3ae-168">If the template file was named _job-ffmpeg.json_, then the template would be invoked as follows:</span></span>

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a><span data-ttu-id="6c3ae-169">Gruppi e trasferimenti di file</span><span class="sxs-lookup"><span data-stu-id="6c3ae-169">File groups and file transfer</span></span>

<span data-ttu-id="6c3ae-170">La maggior parte dei processi e delle attività richiede file di input e produce file di output.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-170">Most jobs and tasks require input files and produce output files.</span></span> <span data-ttu-id="6c3ae-171">Sia i file di input che i file di output in genere devono essere trasferiti dal client al nodo o dal nodo al client.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-171">Both input files and output files typically need to be transferred, either from the client to the node, or from the node to the client.</span></span> <span data-ttu-id="6c3ae-172">L'estensione dell'interfaccia della riga di comando di Azure Batch consente di evitare il trasferimento di file e usa l'account di archiviazione creato per impostazione predefinita per ogni account Batch.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-172">The Azure Batch CLI extension abstracts away file transfer and utilizes the storage account that is created by default for each Batch account.</span></span>

<span data-ttu-id="6c3ae-173">Un gruppo di file equivale a un contenitore creato nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-173">A file group equates to a container that is created in the Azure storage account.</span></span> <span data-ttu-id="6c3ae-174">Il gruppo di file può avere sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-174">The file group may have subfolders.</span></span>

<span data-ttu-id="6c3ae-175">L’estensione per interfaccia della riga di comando Batch fornisce comandi che consentono di caricare i file da un client a un gruppo di file specificato e di scaricare i file dal gruppo di file specificato a un client.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-175">The Batch CLI extension provides commands for uploading files from client to a specified file group and downloading files from the specified file group to a client.</span></span>

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

<span data-ttu-id="6c3ae-176">I modelli di processo e di pool consentono di specificare che i file archiviati in gruppi di file vengano copiati nei nodi del pool o dai nodi del pool a un gruppo di file.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-176">Pool and job templates allow files stored in file groups to be specified for copy onto pool nodes or off pool nodes back to a file group.</span></span> <span data-ttu-id="6c3ae-177">Nel modello di processo illustrato in precedenza, ad esempio, viene specificato il gruppo di file "ffmpeg-input" per la factory di attività come posizione dei file video di origine copiati nel nodo per la transcodifica. Il gruppo di file "ffmpeg-output" viene usato come posizione in cui vengono copiati i file di output transcodificati dal nodo che esegue ogni attività.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-177">For example, in the job template specified previously, the file group “ffmpeg-input” is specified for the task factory as the location of the source video files copied down onto the node for transcoding; the file group “ffmpeg-output” is used as the location where the transcoded output files are copied to from the node running each task.</span></span>

## <a name="summary"></a><span data-ttu-id="6c3ae-178">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="6c3ae-178">Summary</span></span>

<span data-ttu-id="6c3ae-179">Il supporto per i modelli e il trasferimento di file è stato attualmente aggiunto solo all'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-179">Template and file transfer support have currently been added only to the Azure CLI.</span></span> <span data-ttu-id="6c3ae-180">L'obiettivo è quello di allargare il numero di utenti che possono usare Batch, consentendone l'utilizzo anche a ricercatori, utenti IT e così via che non hanno la necessità di sviluppare codice usando le API di Batch.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-180">The goal is to expand the audience that can use Batch to users who do not need to develop code using the Batch APIs, such as researchers, IT users, and so on.</span></span> <span data-ttu-id="6c3ae-181">Senza dover scrivere il codice, gli utenti che conoscono Azure Batch e le applicazioni che devono essere eseguite da Batch possono creare modelli per la creazione di pool e processi.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-181">Without coding, users with knowledge of Azure, Batch, and the applications to be run by Batch can create templates for pool and job creation.</span></span> <span data-ttu-id="6c3ae-182">Con i parametri dei modelli, gli utenti che non hanno una conoscenza approfondita di Batch e delle applicazioni possono usare i modelli.</span><span class="sxs-lookup"><span data-stu-id="6c3ae-182">With template parameters, users without detailed knowledge of Batch and the applications can use the templates.</span></span>

<span data-ttu-id="6c3ae-183">Provare l'estensione Batch per l'interfaccia della riga di comando di Azure e fornire feedback o suggerimenti nella sezione Commenti dell'articolo o tramite il [forum di Azure Batch](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span><span class="sxs-lookup"><span data-stu-id="6c3ae-183">Try out the Batch extension for the Azure CLI and provide us with any feedback or suggestions, either in the comments for this article or via the [Azure Batch forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c3ae-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6c3ae-184">Next steps</span></span>

- <span data-ttu-id="6c3ae-185">Vedere il post del blog sui modelli di Batch: [Processi in esecuzione di Azure Batch che usano l'interfaccia della riga di comando di Azure: non è richiesto alcun codice](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span><span class="sxs-lookup"><span data-stu-id="6c3ae-185">See the Batch templates blog post: [Running Azure Batch jobs using the Azure CLI – no code required](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span></span>
- <span data-ttu-id="6c3ae-186">Documentazione dettagliata su installazione e utilizzo, esempi e codice sorgente sono disponibili nel [repository GitHub di Azure](https://github.com/Azure/azure-batch-cli-extensions).</span><span class="sxs-lookup"><span data-stu-id="6c3ae-186">Detailed installation and usage documentation, samples, and source code are available in the [Azure GitHub repository](https://github.com/Azure/azure-batch-cli-extensions).</span></span>
