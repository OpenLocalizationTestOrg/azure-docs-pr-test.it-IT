---
title: 'Esercitazione: Usare Azure Batch SDK per Python | Documentazione Microsoft'
description: Apprendere i concetti di base di Azure Batch e creare una soluzione semplice mediante Python.
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
ms.openlocfilehash: bd5a977c10d3955639beb893cd7a37581b14f7c0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-batch-sdk-for-python"></a><span data-ttu-id="50fb2-103">Introduzione all'SDK di Batch per Python</span><span class="sxs-lookup"><span data-stu-id="50fb2-103">Get started with the Batch SDK for Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="50fb2-104">.NET</span><span class="sxs-lookup"><span data-stu-id="50fb2-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="50fb2-105">Python</span><span class="sxs-lookup"><span data-stu-id="50fb2-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="50fb2-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="50fb2-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="50fb2-107">Questo articolo illustra i concetti di base relativi ad [Azure Batch][azure_batch] e al client [Python di Batch][py_azure_sdk] esaminando una piccola applicazione Batch scritta in Python.</span><span class="sxs-lookup"><span data-stu-id="50fb2-107">Learn the basics of [Azure Batch][azure_batch] and the [Batch Python][py_azure_sdk] client as we discuss a small Batch application written in Python.</span></span> <span data-ttu-id="50fb2-108">Verrà illustrato il modo in cui due script di esempio usano il servizio Batch per elaborare un carico di lavoro parallelo in macchine virtuali Linux nel cloud e come interagiscono con [Archiviazione di Azure](../storage/common/storage-introduction.md) per lo staging e il recupero di file.</span><span class="sxs-lookup"><span data-stu-id="50fb2-108">We look at how two sample scripts use the Batch service to process a parallel workload on Linux virtual machines in the cloud, and how they interact with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="50fb2-109">Saranno disponibili informazioni su un flusso di lavoro comune dell'applicazione Batch e sui principali componenti di Batch, ad esempio processi, attività, pool e nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="50fb2-109">You'll learn a common Batch application workflow and gain a base understanding of the major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="50fb2-110">![Flusso di lavoro della soluzione Batch (di base)][11]</span><span class="sxs-lookup"><span data-stu-id="50fb2-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="50fb2-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="50fb2-111">Prerequisites</span></span>
<span data-ttu-id="50fb2-112">Questo articolo presuppone che l'utente sappia usare Python e Linux</span><span class="sxs-lookup"><span data-stu-id="50fb2-112">This article assumes that you have a working knowledge of Python and familiarity with Linux.</span></span> <span data-ttu-id="50fb2-113">e possa soddisfare i requisiti di creazione dell'account specificati di seguito per Azure e per i servizi Batch e di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="50fb2-113">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="50fb2-114">Account</span><span class="sxs-lookup"><span data-stu-id="50fb2-114">Accounts</span></span>
* <span data-ttu-id="50fb2-115">**Account Azure**: se non si ha già una sottoscrizione di Azure, [creare un account Azure gratuito][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="50fb2-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="50fb2-116">**Account Batch**: dopo aver creato una sottoscrizione di Azure, [creare un account Azure Batch](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="50fb2-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="50fb2-117">**Account di archiviazione**: vedere [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="50fb2-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

### <a name="code-sample"></a><span data-ttu-id="50fb2-118">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="50fb2-118">Code sample</span></span>
<span data-ttu-id="50fb2-119">L'[esempio di codice][github_article_samples] Python usato nell'esercitazione è uno dei molti esempi di codice Batch disponibili nel repository [azure-batch-samples][github_samples] in GitHub.</span><span class="sxs-lookup"><span data-stu-id="50fb2-119">The Python tutorial [code sample][github_article_samples] is one of the many Batch code samples found in the [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="50fb2-120">È possibile scaricare tutti gli esempi facendo clic su **Clone or download > Download ZIP** (Clona o scarica > Scarica ZIP) nella home page del repository oppure facendo clic sul collegamento di download diretto [azure-batch-samples-master.zip][github_samples_zip].</span><span class="sxs-lookup"><span data-stu-id="50fb2-120">You can download all the samples by clicking **Clone or download > Download ZIP** on the repository home page, or by clicking the [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="50fb2-121">Dopo aver estratto il contenuto del file ZIP, i due script per questa esercitazione sono disponibili nella directory `article_samples` :</span><span class="sxs-lookup"><span data-stu-id="50fb2-121">Once you've extracted the contents of the ZIP file, the two scripts for this tutorial are found in the `article_samples` directory:</span></span>

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a><span data-ttu-id="50fb2-122">Ambiente Python</span><span class="sxs-lookup"><span data-stu-id="50fb2-122">Python environment</span></span>
<span data-ttu-id="50fb2-123">Per eseguire lo script di esempio *python_tutorial_client.py* nella workstation locale è necessario un **interprete Python** compatibile con la versione **2.7** o **3.3+**.</span><span class="sxs-lookup"><span data-stu-id="50fb2-123">To run the *python_tutorial_client.py* sample script on your local workstation, you need a **Python interpreter** compatible with version **2.7** or **3.3+**.</span></span> <span data-ttu-id="50fb2-124">Lo script è stato verificato in ambiente Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="50fb2-124">The script has been tested on both Linux and Windows.</span></span>

### <a name="cryptography-dependencies"></a><span data-ttu-id="50fb2-125">Dipendenze di cryptography</span><span class="sxs-lookup"><span data-stu-id="50fb2-125">cryptography dependencies</span></span>
<span data-ttu-id="50fb2-126">È necessario installare le dipendenze per la libreria [cryptography][crypto], richieste dai pacchetti Python `azure-batch` e `azure-storage`.</span><span class="sxs-lookup"><span data-stu-id="50fb2-126">You must install the dependencies for the [cryptography][crypto] library, required by the `azure-batch` and `azure-storage` Python packages.</span></span> <span data-ttu-id="50fb2-127">Eseguire una di queste operazioni appropriate per la piattaforma o vedere i dettagli dell'[installazione di cryptography][crypto_install] per altre informazioni:</span><span class="sxs-lookup"><span data-stu-id="50fb2-127">Perform one of the following operations appropriate for your platform, or refer to the [cryptography installation][crypto_install] details for more information:</span></span>

* <span data-ttu-id="50fb2-128">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="50fb2-128">Ubuntu</span></span>

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* <span data-ttu-id="50fb2-129">CentOS</span><span class="sxs-lookup"><span data-stu-id="50fb2-129">CentOS</span></span>

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* <span data-ttu-id="50fb2-130">SLES/OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="50fb2-130">SLES/OpenSUSE</span></span>

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* <span data-ttu-id="50fb2-131">Windows</span><span class="sxs-lookup"><span data-stu-id="50fb2-131">Windows</span></span>

    `pip install cryptography`

> [!NOTE]
> <span data-ttu-id="50fb2-132">Se si esegue l'installazione per Python 3.3+ in Linux, usare gli equivalenti di python3 per le dipendenze di Python.</span><span class="sxs-lookup"><span data-stu-id="50fb2-132">If installing for Python 3.3+ on Linux, use the python3 equivalents for the Python dependencies.</span></span> <span data-ttu-id="50fb2-133">Ad esempio, in Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span><span class="sxs-lookup"><span data-stu-id="50fb2-133">For example, on Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span></span>
>
>

### <a name="azure-packages"></a><span data-ttu-id="50fb2-134">Pacchetti di Azure</span><span class="sxs-lookup"><span data-stu-id="50fb2-134">Azure packages</span></span>
<span data-ttu-id="50fb2-135">Installare poi i pacchetti Python per **Azure Batch** e **Archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="50fb2-135">Next, install the **Azure Batch** and **Azure Storage** Python packages.</span></span> <span data-ttu-id="50fb2-136">È possibile installare entrambi i pacchetti usando **pip** e *requirements.txt* disponibili qui:</span><span class="sxs-lookup"><span data-stu-id="50fb2-136">You can install both packages by using **pip** and the *requirements.txt* found here:</span></span>

`/azure-batch-samples/Python/Batch/requirements.txt`

<span data-ttu-id="50fb2-137">Per installare i pacchetti per Batch e Archiviazione, eseguire il comando **pip** seguente:</span><span class="sxs-lookup"><span data-stu-id="50fb2-137">Issue following **pip** command to install the Batch and Storage packages:</span></span>

`pip install -r requirements.txt`

<span data-ttu-id="50fb2-138">In alternativa, è possibile installare i pacchetti Python [azure-batch][pypi_batch] e [azure-storage][pypi_storage] manualmente:</span><span class="sxs-lookup"><span data-stu-id="50fb2-138">Or, you can install the [azure-batch][pypi_batch] and [azure-storage][pypi_storage] Python packages manually:</span></span>

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> <span data-ttu-id="50fb2-139">Se si una un account senza privilegi, può essere necessario anteporre `sudo` ai comandi.</span><span class="sxs-lookup"><span data-stu-id="50fb2-139">If you are using an unprivileged account, you may need to prefix your commands with `sudo`.</span></span> <span data-ttu-id="50fb2-140">Ad esempio: `sudo pip install -r requirements.txt`.</span><span class="sxs-lookup"><span data-stu-id="50fb2-140">For example, `sudo pip install -r requirements.txt`.</span></span> <span data-ttu-id="50fb2-141">Per altre informazioni sull'installazione dei pacchetti Python, vedere [Installing Packages][pypi_install] (Installazione di pacchetti) in python.org.</span><span class="sxs-lookup"><span data-stu-id="50fb2-141">For more information on installing Python packages, see [Installing Packages][pypi_install] on python.org.</span></span>
>
>

## <a name="batch-python-tutorial-code-sample"></a><span data-ttu-id="50fb2-142">Esempio di codice per l'esercitazione di Batch Python</span><span class="sxs-lookup"><span data-stu-id="50fb2-142">Batch Python tutorial code sample</span></span>
<span data-ttu-id="50fb2-143">L'esempio di codice per l'esercitazione di Batch Python è costituito da due script Python e alcuni file di dati.</span><span class="sxs-lookup"><span data-stu-id="50fb2-143">The Batch Python tutorial code sample consists of two Python scripts and a few data files.</span></span>

* <span data-ttu-id="50fb2-144">**python_tutorial_client.py**: interagisce con i servizi Batch e Archiviazione per eseguire un carico di lavoro parallelo nei nodi di calcolo (macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="50fb2-144">**python_tutorial_client.py**: Interacts with the Batch and Storage services to execute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="50fb2-145">Lo script *python_tutorial_client.py* viene eseguito nella workstation locale.</span><span class="sxs-lookup"><span data-stu-id="50fb2-145">The *python_tutorial_client.py* script runs on your local workstation.</span></span>
* <span data-ttu-id="50fb2-146">**python_tutorial_task.py**: script eseguito nei nodi di calcolo in Azure per completare le operazioni effettive.</span><span class="sxs-lookup"><span data-stu-id="50fb2-146">**python_tutorial_task.py**: The script that runs on compute nodes in Azure to perform the actual work.</span></span> <span data-ttu-id="50fb2-147">Nell'esempio *python_tutorial_task.py* analizza il testo in un file scaricato da Archiviazione di Azure (file di input).</span><span class="sxs-lookup"><span data-stu-id="50fb2-147">In the sample, *python_tutorial_task.py* parses the text in a file downloaded from Azure Storage (the input file).</span></span> <span data-ttu-id="50fb2-148">Produce quindi un file di testo (file di output) che contiene un elenco delle prime tre parole visualizzate nel file di input.</span><span class="sxs-lookup"><span data-stu-id="50fb2-148">Then it produces a text file (the output file) that contains a list of the top three words that appear in the input file.</span></span> <span data-ttu-id="50fb2-149">Dopo aver creato il file di output, *python_tutorial_task.py* carica il file in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="50fb2-149">After it creates the output file, *python_tutorial_task.py* uploads the file to Azure Storage.</span></span> <span data-ttu-id="50fb2-150">Questo lo rende disponibile per il download nello script client in esecuzione nella workstation.</span><span class="sxs-lookup"><span data-stu-id="50fb2-150">This makes it available for download to the client script running on your workstation.</span></span> <span data-ttu-id="50fb2-151">Lo script *python_tutorial_task.py* viene eseguito in parallelo in più nodi di calcolo nel servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="50fb2-151">The *python_tutorial_task.py* script runs in parallel on multiple compute nodes in the Batch service.</span></span>
* <span data-ttu-id="50fb2-152">**./data/taskdata\*.txt**: questi tre file di testo forniscono l'input per le attività eseguite nei nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="50fb2-152">**./data/taskdata\*.txt**: These three text files provide the input for the tasks that run on the compute nodes.</span></span>

<span data-ttu-id="50fb2-153">Il diagramma seguente illustra le operazioni principali eseguite dagli script client e attività.</span><span class="sxs-lookup"><span data-stu-id="50fb2-153">The following diagram illustrates the primary operations that are performed by the client and task scripts.</span></span> <span data-ttu-id="50fb2-154">Questo flusso di lavoro di base è tipico di molte soluzioni di calcolo create con Batch.</span><span class="sxs-lookup"><span data-stu-id="50fb2-154">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="50fb2-155">Anche se non illustra ogni funzionalità disponibile nel servizio Batch, quasi tutti gli scenari di Batch includono parti di questo flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="50fb2-155">While it does not demonstrate every feature available in the Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="50fb2-156">![Flusso di lavoro dell'esempio di Batch][8]</span><span class="sxs-lookup"><span data-stu-id="50fb2-156">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="50fb2-157">**Passaggio 1.**</span><span class="sxs-lookup"><span data-stu-id="50fb2-157">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="50fb2-158">Creare **contenitori** nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="50fb2-158">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="50fb2-159">
[**Passaggio 2.**](#step-2-upload-task-script-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="50fb2-159">
[**Step 2.**](#step-2-upload-task-script-and-data-files)</span></span> <span data-ttu-id="50fb2-160">Caricare lo script attività e i file di input nei contenitori.</span><span class="sxs-lookup"><span data-stu-id="50fb2-160">Upload task script and input files to containers.</span></span><br/><span data-ttu-id="50fb2-161">
[**Passaggio 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="50fb2-161">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="50fb2-162">Creare un **pool** di Batch.</span><span class="sxs-lookup"><span data-stu-id="50fb2-162">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="50fb2-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="50fb2-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="50fb2-164">L'attività **StartTask** del pool scarica lo script attività (python_tutorial_task.py) nei nodi quando questi vengono aggiunti al pool.</span><span class="sxs-lookup"><span data-stu-id="50fb2-164">The pool **StartTask** downloads the task script (python_tutorial_task.py) to nodes as they join the pool.</span></span><br/><span data-ttu-id="50fb2-165">
[**Passaggio 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="50fb2-165">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="50fb2-166">Creare un **processo** di Batch.</span><span class="sxs-lookup"><span data-stu-id="50fb2-166">Create a Batch **job**.</span></span><br/><span data-ttu-id="50fb2-167">
[**Passaggio 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="50fb2-167">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="50fb2-168">Aggiungere **attività** al processo.</span><span class="sxs-lookup"><span data-stu-id="50fb2-168">Add **tasks** to the job.</span></span><br/>
  <span data-ttu-id="50fb2-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="50fb2-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="50fb2-170">Viene pianificata l'esecuzione delle attività nei nodi.</span><span class="sxs-lookup"><span data-stu-id="50fb2-170">The tasks are scheduled to execute on nodes.</span></span><br/>
    <span data-ttu-id="50fb2-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="50fb2-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="50fb2-172">Ogni attività scarica i rispettivi dati di input da Archiviazione di Azure e quindi avvia l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="50fb2-172">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="50fb2-173">
[**Passaggio 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="50fb2-173">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="50fb2-174">Monitorare le attività.</span><span class="sxs-lookup"><span data-stu-id="50fb2-174">Monitor tasks.</span></span><br/>
  <span data-ttu-id="50fb2-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="50fb2-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="50fb2-176">Dopo il completamento, le attività caricano i rispettivi dati di output in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="50fb2-176">As tasks are completed, they upload their output data to Azure Storage.</span></span><br/><span data-ttu-id="50fb2-177">
[**Passaggio 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="50fb2-177">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="50fb2-178">Scaricare l'output delle attività dal servizio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="50fb2-178">Download task output from Storage.</span></span>

<span data-ttu-id="50fb2-179">Come indicato, non tutte le soluzioni Batch eseguono esattamente questi passaggi e potrebbero includerne molti altri, ma l'esempio illustra i processi comuni presenti in una soluzione Batch.</span><span class="sxs-lookup"><span data-stu-id="50fb2-179">As mentioned, not every Batch solution performs these exact steps, and may include many more, but this sample demonstrates common processes found in a Batch solution.</span></span>

## <a name="prepare-client-script"></a><span data-ttu-id="50fb2-180">Preparare lo script client</span><span class="sxs-lookup"><span data-stu-id="50fb2-180">Prepare client script</span></span>
<span data-ttu-id="50fb2-181">Prima di eseguire l'esempio, aggiungere le credenziali dell'account Batch e dell'account di archiviazione a *python_tutorial_client.py*.</span><span class="sxs-lookup"><span data-stu-id="50fb2-181">Before you run the sample, add your Batch and Storage account credentials to *python_tutorial_client.py*.</span></span> <span data-ttu-id="50fb2-182">Se non è già stato fatto, aprire il file in un editor qualsiasi e aggiornare le righe seguenti con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="50fb2-182">If you have not done so already, open the file in your favorite editor and update the following lines with your credentials.</span></span>

```python
# Update the Batch and Storage account credential strings below with the values
# unique to your accounts. These are used when constructing connection strings
# for the Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

<span data-ttu-id="50fb2-183">Le credenziali dell'account Batch e dell'account di archiviazione sono disponibili nel pannello dell'account di ogni servizio nel [portale di Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="50fb2-183">You can find your Batch and Storage account credentials within the account blade of each service in the [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="50fb2-184">![Credenziali di Batch nel portale][9]
![Credenziali di archiviazione nel portale][10]</span><span class="sxs-lookup"><span data-stu-id="50fb2-184">![Batch credentials in the portal][9]
![Storage credentials in the portal][10]</span></span><br/>

<span data-ttu-id="50fb2-185">Nelle sezioni seguenti verranno analizzati i passaggi usati dagli script per elaborare un carico di lavoro nel servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="50fb2-185">In the following sections, we analyze the steps used by the scripts to process a workload in the Batch service.</span></span> <span data-ttu-id="50fb2-186">È consigliabile fare sempre riferimento agli script nell'editor durante la lettura dell'articolo.</span><span class="sxs-lookup"><span data-stu-id="50fb2-186">We encourage you to refer regularly to the scripts in your editor while you work your way through the rest of the article.</span></span>

<span data-ttu-id="50fb2-187">Passare alla riga seguente in **python_tutorial_client.py** per iniziare con il passaggio 1:</span><span class="sxs-lookup"><span data-stu-id="50fb2-187">Navigate to the following line in **python_tutorial_client.py** to start with Step 1:</span></span>

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="50fb2-188">Passaggio 1: Creare contenitori di archiviazione</span><span class="sxs-lookup"><span data-stu-id="50fb2-188">Step 1: Create Storage containers</span></span>
<span data-ttu-id="50fb2-189">![Creare contenitori in Archiviazione di Azure][1]
</span><span class="sxs-lookup"><span data-stu-id="50fb2-189">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="50fb2-190">Batch include il supporto predefinito per l'interazione con Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="50fb2-190">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="50fb2-191">I contenitori nell'account di archiviazione forniranno i file necessari per le attività eseguite nell'account Batch,</span><span class="sxs-lookup"><span data-stu-id="50fb2-191">Containers in your Storage account will provide the files needed by the tasks that run in your Batch account.</span></span> <span data-ttu-id="50fb2-192">oltre a una posizione in cui archiviare i dati di output prodotti.</span><span class="sxs-lookup"><span data-stu-id="50fb2-192">The containers also provide a place to store the output data that the tasks produce.</span></span> <span data-ttu-id="50fb2-193">La prima operazione eseguita dallo script *python_tutorial_client.py* consiste nel creare tre contenitori nell'[archivio BLOB di Azure](../storage/common/storage-introduction.md#blob-storage):</span><span class="sxs-lookup"><span data-stu-id="50fb2-193">The first thing the *python_tutorial_client.py* script does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage):</span></span>

* <span data-ttu-id="50fb2-194">**application**: in questo contenitore verrà archiviato lo script Python eseguito dalle attività, *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="50fb2-194">**application**: This container will store the Python script run by the tasks, *python_tutorial_task.py*.</span></span>
* <span data-ttu-id="50fb2-195">**input**: le attività scaricheranno i file di dati da elaborare dal contenitore *input* .</span><span class="sxs-lookup"><span data-stu-id="50fb2-195">**input**: Tasks will download the data files to process from the *input* container.</span></span>
* <span data-ttu-id="50fb2-196">**output**: dopo aver completato l'elaborazione dei file di input, le attività caricheranno i risultati nel contenitore *output* .</span><span class="sxs-lookup"><span data-stu-id="50fb2-196">**output**: When tasks complete input file processing, they will upload the results to the *output* container.</span></span>

<span data-ttu-id="50fb2-197">Per interagire con un account di archiviazione e creare contenitori, viene usato il pacchetto [azure-storage][pypi_storage] per creare un oggetto [BlockBlobService][py_blockblobservice], ovvero il "client BLOB".</span><span class="sxs-lookup"><span data-stu-id="50fb2-197">In order to interact with a Storage account and create containers, we use the [azure-storage][pypi_storage] package to create a [BlockBlobService][py_blockblobservice] object--the "blob client."</span></span> <span data-ttu-id="50fb2-198">Verranno quindi creati tre contenitori nell'account di archiviazione usando il client BLOB.</span><span class="sxs-lookup"><span data-stu-id="50fb2-198">We then create three containers in the Storage account using the blob client.</span></span>

```python
import azure.storage.blob as azureblob

# Create the blob client, for use in obtaining references to
# blob storage containers and uploading files to containers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use the blob client to create the containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

<span data-ttu-id="50fb2-199">Dopo la creazione dei contenitori, l'applicazione può caricare i file che verranno usati dalle attività.</span><span class="sxs-lookup"><span data-stu-id="50fb2-199">Once the containers have been created, the application can now upload the files that will be used by the tasks.</span></span>

> [!TIP]
> <span data-ttu-id="50fb2-200">[Come usare l'archiviazione BLOB di Azure da Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) offre utili informazioni generali sull'uso dei contenitori e dei BLOB di Archiviazione di Azure,</span><span class="sxs-lookup"><span data-stu-id="50fb2-200">[How to use Azure Blob storage from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="50fb2-201">quindi è consigliabile prenderne visione quando si inizia a usare Batch.</span><span class="sxs-lookup"><span data-stu-id="50fb2-201">It should be near the top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-script-and-data-files"></a><span data-ttu-id="50fb2-202">Passaggio 2: Caricare lo script attività e i file di dati</span><span class="sxs-lookup"><span data-stu-id="50fb2-202">Step 2: Upload task script and data files</span></span>
<span data-ttu-id="50fb2-203">![Caricare l'applicazione dell'attività e i file di input (dati) nei contenitori][2]
</span><span class="sxs-lookup"><span data-stu-id="50fb2-203">![Upload task application and input (data) files to containers][2]
</span></span><br/>

<span data-ttu-id="50fb2-204">Nell'operazione di caricamento dei file *python_tutorial_client.py* definisce prima di tutto le raccolte dei percorsi di file di **application** e **input** esistenti nel computer locale,</span><span class="sxs-lookup"><span data-stu-id="50fb2-204">In the file upload operation, *python_tutorial_client.py* first defines collections of **application** and **input** file paths as they exist on the local machine.</span></span> <span data-ttu-id="50fb2-205">quindi carica i file nei contenitori creati nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="50fb2-205">Then it uploads these files to the containers that you created in the previous step.</span></span>

```python
# Paths to the task script. This script will be executed by the tasks that
# run on the compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# The collection of data files that are to be processed by the tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload the application script to Azure Storage. This is the script that
# will process the data files, and is executed by each of the tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload the data files. This is the data that will be processed by each of
# the tasks executed on the compute nodes in the pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

<span data-ttu-id="50fb2-206">Con la comprensione di lista, la funzione `upload_file_to_container` viene chiamata per ogni file presente nelle raccolte e vengono popolate due raccolte [ResourceFile][py_resource_file].</span><span class="sxs-lookup"><span data-stu-id="50fb2-206">Using list comprehension, the `upload_file_to_container` function is called for each file in the collections, and two [ResourceFile][py_resource_file] collections are populated.</span></span> <span data-ttu-id="50fb2-207">La funzione `upload_file_to_container` è riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="50fb2-207">The `upload_file_to_container` function appears below:</span></span>

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file to an Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: The name of the Azure Blob storage container.
    :param str file_path: The local path to the file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} to container [{}]...'.format(path,
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

### <a name="resourcefiles"></a><span data-ttu-id="50fb2-208">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="50fb2-208">ResourceFiles</span></span>
<span data-ttu-id="50fb2-209">Un oggetto [ResourceFile][py_resource_file] fornisce alle attività in Batch l'URL di un file in Archiviazione di Azure che verrà scaricato in un nodo di calcolo prima dell'esecuzione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="50fb2-209">A [ResourceFile][py_resource_file] provides tasks in Batch with the URL to a file in Azure Storage that is downloaded to a compute node before that task is run.</span></span> <span data-ttu-id="50fb2-210">La proprietà [ResourceFile][py_resource_file].**blob_source** specifica l'URL completo del file esistente in Archiviazione di Azure,</span><span class="sxs-lookup"><span data-stu-id="50fb2-210">The [ResourceFile][py_resource_file].**blob_source** property specifies the full URL of the file as it exists in Azure Storage.</span></span> <span data-ttu-id="50fb2-211">che può includere anche una firma di accesso condiviso che fornisce l'accesso sicuro al file.</span><span class="sxs-lookup"><span data-stu-id="50fb2-211">The URL may also include a shared access signature (SAS) that provides secure access to the file.</span></span> <span data-ttu-id="50fb2-212">La maggior parte dei tipi di attività in Batch include una proprietà *ResourceFiles*, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="50fb2-212">Most task types in Batch include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="50fb2-213">[CloudTask][py_task]</span><span class="sxs-lookup"><span data-stu-id="50fb2-213">[CloudTask][py_task]</span></span>
* <span data-ttu-id="50fb2-214">[StartTask][py_starttask]</span><span class="sxs-lookup"><span data-stu-id="50fb2-214">[StartTask][py_starttask]</span></span>
* <span data-ttu-id="50fb2-215">[JobPreparationTask][py_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="50fb2-215">[JobPreparationTask][py_jobpreptask]</span></span>
* <span data-ttu-id="50fb2-216">[JobReleaseTask][py_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="50fb2-216">[JobReleaseTask][py_jobreltask]</span></span>

<span data-ttu-id="50fb2-217">Questo esempio non usa i tipi di attività JobPreparationTask o JobReleaseTask, ma altre informazioni in merito sono disponibili in [Eseguire attività di preparazione e completamento di processi in nodi di calcolo di Azure Batch](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="50fb2-217">This sample does not use the JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="50fb2-218">Firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="50fb2-218">Shared access signature (SAS)</span></span>
<span data-ttu-id="50fb2-219">Le firme di accesso condiviso sono stringhe che consentono l'accesso sicuro a contenitori e BLOB in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="50fb2-219">Shared access signatures are strings that provide secure access to containers and blobs in Azure Storage.</span></span> <span data-ttu-id="50fb2-220">Lo script *python_tutorial_client.py* usa firme di accesso condiviso per BLOB e contenitori e illustra come ottenere queste stringhe di firma di accesso condiviso dal servizio Archiviazione.</span><span class="sxs-lookup"><span data-stu-id="50fb2-220">The *python_tutorial_client.py* script uses both blob and container shared access signatures, and demonstrates how to obtain these shared access signature strings from the Storage service.</span></span>

* <span data-ttu-id="50fb2-221">**Firme di accesso condiviso per BLOB**: l'attività StartTask del pool usa le firme di accesso condiviso dei BLOB durante il download dello script attività e dei file di dati di input da Archiviazione, come illustrato più avanti nel [passaggio 3](#step-3-create-batch-pool) .</span><span class="sxs-lookup"><span data-stu-id="50fb2-221">**Blob shared access signatures**: The pool's StartTask uses blob shared access signatures when it downloads the task script and input data files from Storage (see [Step #3](#step-3-create-batch-pool) below).</span></span> <span data-ttu-id="50fb2-222">La funzione `upload_file_to_container` in *python_tutorial_client.py* contiene il codice che ottiene la firma di accesso condiviso di ogni BLOB.</span><span class="sxs-lookup"><span data-stu-id="50fb2-222">The `upload_file_to_container` function in *python_tutorial_client.py* contains the code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="50fb2-223">L'operazione viene eseguita chiamando [BlockBlobService.make_blob_url][py_make_blob_url] nel modulo di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="50fb2-223">It does so by calling [BlockBlobService.make_blob_url][py_make_blob_url] in the Storage module.</span></span>
* <span data-ttu-id="50fb2-224">**Firma di accesso condiviso per contenitori**: quando completa le operazioni sul nodo di calcolo, ogni attività carica il rispettivo file di output nel contenitore *output* in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="50fb2-224">**Container shared access signature**: As each task finishes its work on the compute node, it uploads its output file to the *output* container in Azure Storage.</span></span> <span data-ttu-id="50fb2-225">A tale scopo, *python_tutorial_task.py* usa una firma di accesso condiviso del contenitore che fornisce l'accesso in scrittura al contenitore stesso.</span><span class="sxs-lookup"><span data-stu-id="50fb2-225">To do so, *python_tutorial_task.py* uses a container shared access signature that provides write access to the container.</span></span> <span data-ttu-id="50fb2-226">La funzione `get_container_sas_token` in *python_tutorial_client.py* ottiene la firma di accesso condiviso del contenitore, che viene quindi passata alle attività come argomento della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="50fb2-226">The `get_container_sas_token` function in *python_tutorial_client.py* obtains the container's shared access signature, which is then passed as a command-line argument to the tasks.</span></span> <span data-ttu-id="50fb2-227">Il passaggio 5, [Aggiungere attività a un processo](#step-5-add-tasks-to-job), illustra l'utilizzo della firma di accesso condiviso del contenitore.</span><span class="sxs-lookup"><span data-stu-id="50fb2-227">Step #5, [Add tasks to a job](#step-5-add-tasks-to-job), discusses the usage of the container SAS.</span></span>

> [!TIP]
> <span data-ttu-id="50fb2-228">Per altre informazioni su come fornire un accesso sicuro ai dati nell'account di archiviazione, vedere la serie in due parti sulle firme di accesso condiviso, [Parte 1: Informazioni sul modello di firma di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md) e [Parte 2: Creare e usare una firma di accesso condiviso con il servizio BLOB](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="50fb2-228">Check out the two-part series on shared access signatures, [Part 1: Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a SAS with the Blob service](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), to learn more about providing secure access to data in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="50fb2-229">Passaggio 3: Creare un pool di Batch</span><span class="sxs-lookup"><span data-stu-id="50fb2-229">Step 3: Create Batch pool</span></span>
<span data-ttu-id="50fb2-230">![Creare un pool di Batch][3]
</span><span class="sxs-lookup"><span data-stu-id="50fb2-230">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="50fb2-231">Un **pool** di Batch è una raccolta di nodi di calcolo (macchine virtuali) in cui Batch esegue le attività di un processo.</span><span class="sxs-lookup"><span data-stu-id="50fb2-231">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="50fb2-232">Dopo il caricamento dello script attività e dei file di dati nell'account di archiviazione, *python_tutorial_client.py* avvia l'interazione con il servizio Batch usando il modulo Batch Python.</span><span class="sxs-lookup"><span data-stu-id="50fb2-232">After it uploads the task script and data files to the Storage account, *python_tutorial_client.py* starts its interaction with the Batch service by using the Batch Python module.</span></span> <span data-ttu-id="50fb2-233">A tale scopo viene creato un oggetto [BatchServiceClient][py_batchserviceclient]:</span><span class="sxs-lookup"><span data-stu-id="50fb2-233">To do so, a [BatchServiceClient][py_batchserviceclient] is created:</span></span>

```python
# Create a Batch service client. We'll now be interacting with the Batch
# service in addition to Storage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

<span data-ttu-id="50fb2-234">Viene quindi creato un pool di nodi di calcolo nell'account Batch con una chiamata a `create_pool`.</span><span class="sxs-lookup"><span data-stu-id="50fb2-234">Next, a pool of compute nodes is created in the Batch account with a call to `create_pool`.</span></span>

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with the specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for the new pool.
    :param list resource_files: A collection of resource files for the pool's
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

    # Specify the commands for the pool's start task. The start task is run
    # on each node as it joins the pool, and when it's rebooted or re-imaged.
    # We use the start task to prep the node for running our task script.
    task_commands = [
        # Copy the python_tutorial_task.py script to the "shared" directory
        # that all tasks that run on the node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and the dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install the azure-storage module so that the task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get the node agent SKU and image reference for the virtual machine
    # configuration.
    # For more information about the virtual machine configuration, see:
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

<span data-ttu-id="50fb2-235">Quando si crea un pool, si definisce un elemento [PoolAddParameter][py_pooladdparam] che specifica diverse proprietà per il pool:</span><span class="sxs-lookup"><span data-stu-id="50fb2-235">When you create a pool, you define a [PoolAddParameter][py_pooladdparam] that specifies several properties for the pool:</span></span>

* <span data-ttu-id="50fb2-236">**ID** del pool (*id*: obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="50fb2-236">**ID** of the pool (*id* - required)</span></span><p/><span data-ttu-id="50fb2-237">Così come la maggior parte delle entità in Batch, il nuovo pool deve avere un ID univoco all'interno dell'account Batch.</span><span class="sxs-lookup"><span data-stu-id="50fb2-237">As with most entities in Batch, your new pool must have a unique ID within your Batch account.</span></span> <span data-ttu-id="50fb2-238">Il codice fa riferimento a questo pool usando il relativo ID, che costituisce anche il modo con cui si identifica il pool nel [portale][azure_portal] di Azure.</span><span class="sxs-lookup"><span data-stu-id="50fb2-238">Your code refers to this pool using its ID, and it's how you identify the pool in the Azure [portal][azure_portal].</span></span>
* <span data-ttu-id="50fb2-239">**Numero di nodi di calcolo** (*target_dedicated*: obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="50fb2-239">**Number of compute nodes** (*target_dedicated* - required)</span></span><p/><span data-ttu-id="50fb2-240">Questa proprietà specifica il numero di macchine virtuali da distribuire nel pool.</span><span class="sxs-lookup"><span data-stu-id="50fb2-240">This property specifies how many VMs should be deployed in the pool.</span></span> <span data-ttu-id="50fb2-241">È importante notare che tutti gli account Batch hanno una **quota** predefinita che limita il numero di **core** e di conseguenza di nodi di calcolo in un account Batch.</span><span class="sxs-lookup"><span data-stu-id="50fb2-241">It is important to note that all Batch accounts have a default **quota** that limits the number of **cores** (and thus, compute nodes) in a Batch account.</span></span> <span data-ttu-id="50fb2-242">Le quote predefinite e le istruzioni su come [aumentare una quota](batch-quota-limit.md#increase-a-quota), ad esempio il numero massimo di core nell'account Batch, sono riportate in [Quote e limiti per il servizio Azure Batch](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="50fb2-242">You can find the default quotas and instructions on how to [increase a quota](batch-quota-limit.md#increase-a-quota) (such as the maximum number of cores in your Batch account) in [Quotas and limits for the Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="50fb2-243">Se il pool non raggiunge più di X nodi, ad esempio,</span><span class="sxs-lookup"><span data-stu-id="50fb2-243">If you find yourself asking "Why won't my pool reach more than X nodes?"</span></span> <span data-ttu-id="50fb2-244">questa quota di core può essere la causa.</span><span class="sxs-lookup"><span data-stu-id="50fb2-244">this core quota may be the cause.</span></span>
* <span data-ttu-id="50fb2-245">**Sistema operativo** per i nodi (*virtual_machine_configuration* **o** *cloud_service_configuration*: obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="50fb2-245">**Operating system** for nodes (*virtual_machine_configuration* **or** *cloud_service_configuration* - required)</span></span><p/><span data-ttu-id="50fb2-246">In *python_tutorial_client.py* viene creato un pool di nodi Linux tramite [VirtualMachineConfiguration][py_vm_config].</span><span class="sxs-lookup"><span data-stu-id="50fb2-246">In *python_tutorial_client.py*, we create a pool of Linux nodes using a [VirtualMachineConfiguration][py_vm_config].</span></span> <span data-ttu-id="50fb2-247">La funzione `select_latest_verified_vm_image_with_node_agent_sku` in `common.helpers` semplifica l'uso delle immagini di [Marketplace per Macchine virtuali di Azure][vm_marketplace].</span><span class="sxs-lookup"><span data-stu-id="50fb2-247">The `select_latest_verified_vm_image_with_node_agent_sku` function in `common.helpers` simplifies working with [Azure Virtual Machines Marketplace][vm_marketplace] images.</span></span> <span data-ttu-id="50fb2-248">Per altre informazioni sull'uso delle immagini del Marketplace, vedere [Effettuare il provisioning di nodi di calcolo Linux nei pool di Azure Batch](batch-linux-nodes.md) .</span><span class="sxs-lookup"><span data-stu-id="50fb2-248">See [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information about using Marketplace images.</span></span>
* <span data-ttu-id="50fb2-249">**Dimensione dei nodi di calcolo** (*vm_size*: obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="50fb2-249">**Size of compute nodes** (*vm_size* - required)</span></span><p/><span data-ttu-id="50fb2-250">Dato che vengono specificati nodi Linux per [VirtualMachineConfiguration][py_vm_config], viene specificata una dimensione di VM, in questo esempio `STANDARD_A1`, in base a quanto descritto in [Dimensioni delle macchine virtuali in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="50fb2-250">Since we're specifying Linux nodes for our [VirtualMachineConfiguration][py_vm_config], we specify a VM size (`STANDARD_A1` in this sample) from [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="50fb2-251">Per altre informazioni, vedere [Effettuare il provisioning di nodi di calcolo Linux nei pool di Azure Batch](batch-linux-nodes.md) .</span><span class="sxs-lookup"><span data-stu-id="50fb2-251">Again, see [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information.</span></span>
* <span data-ttu-id="50fb2-252">**Attività di avvio** (*start_task*: non obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="50fb2-252">**Start task** (*start_task* - not required)</span></span><p/><span data-ttu-id="50fb2-253">Oltre alle proprietà relative ai nodi fisici sopra descritte, è possibile specificare anche un elemento [StartTask][py_starttask] per il pool, ma non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="50fb2-253">Along with the above physical node properties, you may also specify a [StartTask][py_starttask] for the pool (it is not required).</span></span> <span data-ttu-id="50fb2-254">L'attività StartTask viene eseguita in ogni nodo quando questo viene aggiunto al pool e ogni volta che viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="50fb2-254">The StartTask executes on each node as that node joins the pool, and each time a node is restarted.</span></span> <span data-ttu-id="50fb2-255">StartTask è particolarmente utile per preparare i nodi di calcolo per l'esecuzione di attività, ad esempio per installare le applicazioni che vengono eseguite dalle attività.</span><span class="sxs-lookup"><span data-stu-id="50fb2-255">The StartTask is especially useful for preparing compute nodes for the execution of tasks, such as installing the applications that your tasks run.</span></span><p/><span data-ttu-id="50fb2-256">In questa applicazione di esempio StartTask copia i file scaricati dal servizio di archiviazione, specificati usando la proprietà **resource_files** di StartTask, dalla *directory di lavoro* di StartTask alla directory *condivisa* a cui possono accedere tutte le attività in esecuzione sul nodo.</span><span class="sxs-lookup"><span data-stu-id="50fb2-256">In this sample application, the StartTask copies the files that it downloads from Storage (which are specified by using the StartTask's **resource_files** property) from the StartTask *working directory* to the *shared* directory that all tasks running on the node can access.</span></span> <span data-ttu-id="50fb2-257">Sostanzialmente, viene copiato `python_tutorial_task.py` nella directory condivisa in ogni nodo quando questo viene aggiunto al pool, in modo che qualsiasi attività in esecuzione nel nodo possa accedervi.</span><span class="sxs-lookup"><span data-stu-id="50fb2-257">Essentially, this copies `python_tutorial_task.py` to the shared directory on each node as the node joins the pool, so that any tasks that run on the node can access it.</span></span>

<span data-ttu-id="50fb2-258">Si noti la chiamata alla funzione helper `wrap_commands_in_shell` .</span><span class="sxs-lookup"><span data-stu-id="50fb2-258">You may notice the call to the `wrap_commands_in_shell` helper function.</span></span> <span data-ttu-id="50fb2-259">Questa funzione acquisisce una raccolta di comandi separati e crea una singola riga di comando appropriata per la proprietà della riga di comando dell'attività.</span><span class="sxs-lookup"><span data-stu-id="50fb2-259">This function takes a collection of separate commands and creates a single command line appropriate for a task's command-line property.</span></span>

<span data-ttu-id="50fb2-260">Nel frammento di codice precedente si può notare anche l'uso di due variabili di ambiente nella proprietà **command_line** di StartTask: `AZ_BATCH_TASK_WORKING_DIR` e `AZ_BATCH_NODE_SHARED_DIR`.</span><span class="sxs-lookup"><span data-stu-id="50fb2-260">Also notable in the code snippet above is the use of two environment variables in the **command_line** property of the StartTask: `AZ_BATCH_TASK_WORKING_DIR` and `AZ_BATCH_NODE_SHARED_DIR`.</span></span> <span data-ttu-id="50fb2-261">Ogni nodo di calcolo in un pool di Batch viene configurato automaticamente con diverse variabili di ambiente specifiche per Batch.</span><span class="sxs-lookup"><span data-stu-id="50fb2-261">Each compute node within a Batch pool is automatically configured with several environment variables that are specific to Batch.</span></span> <span data-ttu-id="50fb2-262">Tutti processi eseguiti da un'attività possono accedere a queste variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="50fb2-262">Any process that is executed by a task has access to these environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="50fb2-263">Per altre informazioni sulle variabili di ambiente disponibili nei nodi di calcolo di un pool di Batch, oltre a informazioni sulle directory di lavoro delle attività, vedere **Impostazioni di ambiente per le attività** e **File e directory** in [Panoramica delle funzionalità di Batch per sviluppatori](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="50fb2-263">To find out more about the environment variables that are available on compute nodes in a Batch pool, as well as information on task working directories, see **Environment settings for tasks** and **Files and directories** in the [overview of Azure Batch features](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="50fb2-264">Passaggio 4: Creare un processo di Batch</span><span class="sxs-lookup"><span data-stu-id="50fb2-264">Step 4: Create Batch job</span></span>
<span data-ttu-id="50fb2-265">![Creare un processo di Batch][4]</span><span class="sxs-lookup"><span data-stu-id="50fb2-265">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="50fb2-266">Un **processo** di Batch è una raccolta di attività ed è associato a un pool di nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="50fb2-266">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="50fb2-267">Le attività in un processo vengono eseguite nei nodi di calcolo del pool associato.</span><span class="sxs-lookup"><span data-stu-id="50fb2-267">The tasks in a job execute on the associated pool's compute nodes.</span></span>

<span data-ttu-id="50fb2-268">È possibile usare un processo non solo per organizzare le attività nei carichi di lavoro correlati e tenerne traccia, ma anche per imporre determinati vincoli, ad esempio il tempo di esecuzione massimo per il processo e, per estensione, per le rispettive attività, nonché per imporre la priorità dei processi rispetto ad altri nell'account Batch.</span><span class="sxs-lookup"><span data-stu-id="50fb2-268">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as the maximum runtime for the job (and by extension, its tasks) and job priority in relation to other jobs in the Batch account.</span></span> <span data-ttu-id="50fb2-269">In questo esempio, tuttavia, il processo viene associato solo al pool creato nel Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="50fb2-269">In this example, however, the job is associated only with the pool that was created in step #3.</span></span> <span data-ttu-id="50fb2-270">Non vengono configurate proprietà aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="50fb2-270">No additional properties are configured.</span></span>

<span data-ttu-id="50fb2-271">Tutti i processi di Batch sono associati a un pool specifico.</span><span class="sxs-lookup"><span data-stu-id="50fb2-271">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="50fb2-272">Questa associazione indica i nodi in cui verranno eseguite le attività del processo.</span><span class="sxs-lookup"><span data-stu-id="50fb2-272">This association indicates which nodes the job's tasks execute on.</span></span> <span data-ttu-id="50fb2-273">Il pool viene specificato con la proprietà [PoolInformation][py_poolinfo], come illustrato nel frammento di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="50fb2-273">You specify the pool by using the [PoolInformation][py_poolinfo] property, as shown in the code snippet below.</span></span>

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with the specified ID, associated with the specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The ID for the job.
    :param str pool_id: The ID for the pool.
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

<span data-ttu-id="50fb2-274">Dopo la creazione di un processo, vengono aggiunte attività per l'esecuzione delle operazioni.</span><span class="sxs-lookup"><span data-stu-id="50fb2-274">Now that a job has been created, tasks are added to perform the work.</span></span>

## <a name="step-5-add-tasks-to-job"></a><span data-ttu-id="50fb2-275">Passaggio 5: Aggiungere attività a un processo</span><span class="sxs-lookup"><span data-stu-id="50fb2-275">Step 5: Add tasks to job</span></span>
<span data-ttu-id="50fb2-276">![Aggiungere attività a un processo][5]</span><span class="sxs-lookup"><span data-stu-id="50fb2-276">![Add tasks to job][5]</span></span><br/><span data-ttu-id="50fb2-277">
*(1) Le attività vengono aggiunte al processo, (2) viene pianificata l'esecuzione delle attività nei nodi e (3) le attività scaricano i file di dati da elaborare*</span><span class="sxs-lookup"><span data-stu-id="50fb2-277">
*(1) Tasks are added to the job, (2) the tasks are scheduled to run on nodes, and (3) the tasks download the data files to process*</span></span>

<span data-ttu-id="50fb2-278">Le **attività** di Batch sono le singole unità di lavoro eseguite nei nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="50fb2-278">Batch **tasks** are the individual units of work that execute on the compute nodes.</span></span> <span data-ttu-id="50fb2-279">Un'attività ha una riga di comando ed esegue gli script o i file eseguibili specificati in questa riga di comando.</span><span class="sxs-lookup"><span data-stu-id="50fb2-279">A task has a command line and runs the scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="50fb2-280">Per eseguire effettivamente le operazioni, è necessario aggiungere attività a un processo.</span><span class="sxs-lookup"><span data-stu-id="50fb2-280">To actually perform work, tasks must be added to a job.</span></span> <span data-ttu-id="50fb2-281">Ogni elemento [CloudTask][py_task] viene configurato con una proprietà della riga di comando e, analogamente all'attività StartTask del pool, con oggetti [ResourceFiles][py_resource_file] scaricati dall'attività nel nodo prima dell'esecuzione automatica della rispettiva riga di comando.</span><span class="sxs-lookup"><span data-stu-id="50fb2-281">Each [CloudTask][py_task] is configured with a command-line property and [ResourceFiles][py_resource_file] (as with the pool's StartTask) that the task downloads to the node before its command line is automatically executed.</span></span> <span data-ttu-id="50fb2-282">Nell'esempio, ogni attività elabora un solo file.</span><span class="sxs-lookup"><span data-stu-id="50fb2-282">In the sample, each task processes only one file.</span></span> <span data-ttu-id="50fb2-283">Di conseguenza, la rispettiva raccolta ResourceFiles contiene un singolo elemento.</span><span class="sxs-lookup"><span data-stu-id="50fb2-283">Thus, its ResourceFiles collection contains a single element.</span></span>

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in the collection to the specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The ID of the job to which to add the tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: The ID of an Azure Blob storage container to
    which the tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    the specified Azure Blob storage container.
    """

    print('Adding {} tasks to job [{}]...'.format(len(input_files), job_id))

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
> <span data-ttu-id="50fb2-284">Quando accedono a variabili di ambiente come `$AZ_BATCH_NODE_SHARED_DIR` o eseguono un'applicazione non presente nell'elemento `PATH` del nodo, le righe di comando delle attività devono richiamare la shell in modo esplicito, ad esempio con `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span><span class="sxs-lookup"><span data-stu-id="50fb2-284">When they access environment variables such as `$AZ_BATCH_NODE_SHARED_DIR` or execute an application not found in the node's `PATH`, task command lines must invoke the shell explicitly, such as with `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span></span> <span data-ttu-id="50fb2-285">Questo requisito è superfluo se le attività eseguono un'applicazione nell'elemento `PATH` del nodo e non fanno riferimento a variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="50fb2-285">This requirement is unnecessary if your tasks execute an application in the node's `PATH` and do not reference any environment variables.</span></span>
>
>

<span data-ttu-id="50fb2-286">Nel ciclo `for` del frammento di codice precedente, la riga di comando per l'attività è costruita con cinque argomenti della riga di comando che vengono passati a *python_tutorial_task.py*:</span><span class="sxs-lookup"><span data-stu-id="50fb2-286">Within the `for` loop in the code snippet above, you can see that the command line for the task is constructed with five command-line arguments that are passed to *python_tutorial_task.py*:</span></span>

1. <span data-ttu-id="50fb2-287">**filepath**: percorso locale del file esistente nel nodo.</span><span class="sxs-lookup"><span data-stu-id="50fb2-287">**filepath**: This is the local path to the file as it exists on the node.</span></span> <span data-ttu-id="50fb2-288">Durante la creazione dell'oggetto ResourceFile in `upload_file_to_container` nel precedente passaggio 2, per questa proprietà (parametro `file_path` nel costruttore ResourceFile) è stato usato il nome file.</span><span class="sxs-lookup"><span data-stu-id="50fb2-288">When the ResourceFile object in `upload_file_to_container` was created in Step 2 above, the file name was used for this property (the `file_path` parameter in the ResourceFile constructor).</span></span> <span data-ttu-id="50fb2-289">Ciò indica che il file si trova nella stessa directory di *python_tutorial_task.py* nel nodo.</span><span class="sxs-lookup"><span data-stu-id="50fb2-289">This indicates that the file can be found in the same directory on the node as *python_tutorial_task.py*.</span></span>
2. <span data-ttu-id="50fb2-290">**numwords**: le prime *N* parole devono essere scritte nel file di output.</span><span class="sxs-lookup"><span data-stu-id="50fb2-290">**numwords**: The top *N* words should be written to the output file.</span></span>
3. <span data-ttu-id="50fb2-291">**storageaccount**: nome dell'account di archiviazione proprietario del contenitore in cui dovrà essere caricato l'output dell'attività.</span><span class="sxs-lookup"><span data-stu-id="50fb2-291">**storageaccount**: The name of the Storage account that owns the container to which the task output should be uploaded.</span></span>
4. <span data-ttu-id="50fb2-292">**storagecontainer**: nome del contenitore di archiviazione in cui dovranno essere caricati i file di output.</span><span class="sxs-lookup"><span data-stu-id="50fb2-292">**storagecontainer**: The name of the Storage container to which the output files should be uploaded.</span></span>
5. <span data-ttu-id="50fb2-293">**sastoken**: firma di accesso condiviso che consente l'accesso in scrittura al contenitore **output** in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="50fb2-293">**sastoken**: The shared access signature (SAS) that provides write access to the **output** container in Azure Storage.</span></span> <span data-ttu-id="50fb2-294">Lo script *python_tutorial_task.py* usa questa firma di accesso condiviso quando crea il riferimento BlockBlobService.</span><span class="sxs-lookup"><span data-stu-id="50fb2-294">The *python_tutorial_task.py* script uses this shared access signature when creates its BlockBlobService reference.</span></span> <span data-ttu-id="50fb2-295">È così possibile accedere al contenitore in scrittura senza una chiave di accesso dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="50fb2-295">This provides write access to the container without requiring an access key for the storage account.</span></span>

```python
# NOTE: Taken from python_tutorial_task.py

# Create the blob client using the container's SAS token.
# This allows us to create a client that provides write
# access only to the container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="50fb2-296">Passaggio 6: Monitorare le attività</span><span class="sxs-lookup"><span data-stu-id="50fb2-296">Step 6: Monitor tasks</span></span>
<span data-ttu-id="50fb2-297">![Monitorare le attività][6]</span><span class="sxs-lookup"><span data-stu-id="50fb2-297">![Monitor tasks][6]</span></span><br/><span data-ttu-id="50fb2-298">
*(1) Lo script monitora le attività per verificare lo stato di completamento e (2) le attività caricano i dati dei risultati in Archiviazione di Azure*</span><span class="sxs-lookup"><span data-stu-id="50fb2-298">
*The script (1) monitors the tasks for completion status, and (2) the tasks upload result data to Azure Storage*</span></span>

<span data-ttu-id="50fb2-299">Quando le attività vengono aggiunte a un processo, vengono accodate automaticamente e ne viene pianificata l'esecuzione nei nodi di calcolo entro il pool associato al progetto.</span><span class="sxs-lookup"><span data-stu-id="50fb2-299">When tasks are added to a job, they are automatically queued and scheduled for execution on compute nodes within the pool associated with the job.</span></span> <span data-ttu-id="50fb2-300">In base alle impostazioni specificate, Batch gestisce tutte le operazioni di accodamento, pianificazione, ripetizione di tentativi dell'attività e tutte le altre operazioni amministrative relative all'attività.</span><span class="sxs-lookup"><span data-stu-id="50fb2-300">Based on the settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="50fb2-301">Sono disponibili molti approcci al monitoraggio dell'esecuzione delle attività.</span><span class="sxs-lookup"><span data-stu-id="50fb2-301">There are many approaches to monitoring task execution.</span></span> <span data-ttu-id="50fb2-302">La funzione `wait_for_tasks_to_complete` in *python_tutorial_client.py* offre un esempio semplice di monitoraggio delle attività per un determinato stato, in questo caso lo stato [Completed][py_taskstate].</span><span class="sxs-lookup"><span data-stu-id="50fb2-302">The `wait_for_tasks_to_complete` function in *python_tutorial_client.py* provides a simple example of monitoring tasks for a certain state, in this case, the [completed][py_taskstate] state.</span></span>

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in the specified job reach the Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: The id of the job whose tasks should be to monitored.
    :param timedelta timeout: The duration to wait for task completion. If all
    tasks in the specified job do not reach Completed state within this time
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

## <a name="step-7-download-task-output"></a><span data-ttu-id="50fb2-303">Passaggio 7: Scaricare l'output dell'attività</span><span class="sxs-lookup"><span data-stu-id="50fb2-303">Step 7: Download task output</span></span>
<span data-ttu-id="50fb2-304">![Scaricare l'output delle attività dal servizio di archiviazione][7]</span><span class="sxs-lookup"><span data-stu-id="50fb2-304">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="50fb2-305">Dopo il completamento del processo, l'output delle attività può essere scaricato da Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="50fb2-305">Now that the job is completed, the output from the tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="50fb2-306">con una chiamata a `download_blobs_from_container` in *python_tutorial_client.py*:</span><span class="sxs-lookup"><span data-stu-id="50fb2-306">This is done with a call to `download_blobs_from_container` in *python_tutorial_client.py*:</span></span>

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from the specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: The Azure Blob storage container from which to
     download files.
    :param directory_path: The local directory to which to download the files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] to {}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> <span data-ttu-id="50fb2-307">La chiamata a `download_blobs_from_container` in *python_tutorial_client.py* specifica che i file devono essere scaricati nella home directory dell'utente.</span><span class="sxs-lookup"><span data-stu-id="50fb2-307">The call to `download_blobs_from_container` in *python_tutorial_client.py* specifies that the files should be downloaded to your home directory.</span></span> <span data-ttu-id="50fb2-308">È possibile modificare questo percorso di output.</span><span class="sxs-lookup"><span data-stu-id="50fb2-308">Feel free to modify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="50fb2-309">Passaggio 8: Eliminare i contenitori</span><span class="sxs-lookup"><span data-stu-id="50fb2-309">Step 8: Delete containers</span></span>
<span data-ttu-id="50fb2-310">Poiché vengono effettuati addebiti per i dati che risiedono in Archiviazione di Azure, è consigliabile rimuovere eventuali BLOB non più necessari per i processi di Batch.</span><span class="sxs-lookup"><span data-stu-id="50fb2-310">Because you are charged for data that resides in Azure Storage, it is always a good idea to remove any blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="50fb2-311">In *python_tutorial_client.py*, questa operazione viene eseguita con tre chiamate a [BlockBlobService.delete_container][py_delete_container]:</span><span class="sxs-lookup"><span data-stu-id="50fb2-311">In *python_tutorial_client.py*, this is done with three calls to [BlockBlobService.delete_container][py_delete_container]:</span></span>

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-the-job-and-the-pool"></a><span data-ttu-id="50fb2-312">Passaggio 9: Eliminare il processo e il pool</span><span class="sxs-lookup"><span data-stu-id="50fb2-312">Step 9: Delete the job and the pool</span></span>
<span data-ttu-id="50fb2-313">Nel passaggio finale viene richiesto all'utente di eliminare il processo e il pool creati dallo script *python_tutorial_client.py*.</span><span class="sxs-lookup"><span data-stu-id="50fb2-313">In the final step, you are prompted to delete the job and the pool that were created by the *python_tutorial_client.py* script.</span></span> <span data-ttu-id="50fb2-314">Anche se non vengono addebitati costi per i processi e le attività in sé, *vengono* addebiti costi per i nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="50fb2-314">Although you are not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="50fb2-315">È quindi consigliabile allocare i nodi solo in base alla necessità.</span><span class="sxs-lookup"><span data-stu-id="50fb2-315">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="50fb2-316">L'eliminazione dei pool inutilizzati può fare parte del processo di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="50fb2-316">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="50fb2-317">Gli elementi [JobOperations][py_job] e [PoolOperations][py_pool] di BatchServiceClient includono metodi di eliminazione corrispondenti, che vengono chiamati se l'utente conferma l'eliminazione:</span><span class="sxs-lookup"><span data-stu-id="50fb2-317">The BatchServiceClient's [JobOperations][py_job] and [PoolOperations][py_pool] both have corresponding deletion methods, which are called if you confirm deletion:</span></span>

```python
# Clean up Batch resources (if the user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> <span data-ttu-id="50fb2-318">Occorre ricordare che vengono effettuati addebiti per le risorse di calcolo e che l'eliminazione di pool inutilizzati consente di ridurre al minimo i costi.</span><span class="sxs-lookup"><span data-stu-id="50fb2-318">Keep in mind that you are charged for compute resources--deleting unused pools will minimize cost.</span></span> <span data-ttu-id="50fb2-319">Si noti anche che l'eliminazione di un pool comporta l'eliminazione di tutti i nodi di calcolo in quel pool e che eventuali dati disponibili nei nodi non potranno essere più recuperati dopo l'eliminazione del pool.</span><span class="sxs-lookup"><span data-stu-id="50fb2-319">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on the nodes will be unrecoverable after the pool is deleted.</span></span>
>
>

## <a name="run-the-sample-script"></a><span data-ttu-id="50fb2-320">Eseguire lo script di esempio</span><span class="sxs-lookup"><span data-stu-id="50fb2-320">Run the sample script</span></span>
<span data-ttu-id="50fb2-321">Quando si esegue lo script *python_tutorial_client.py* dal [codice di esempio][github_article_samples] dell'esercitazione, l'output della console sarà simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="50fb2-321">When you run the *python_tutorial_client.py* script from the tutorial [code sample][github_article_samples], the console output is similar to the following.</span></span> <span data-ttu-id="50fb2-322">Si riscontra una pausa in corrispondenza di `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` mentre vengono creati e avviati i nodi di calcolo del pool e vengono eseguiti i comandi nell'attività iniziale del pool.</span><span class="sxs-lookup"><span data-stu-id="50fb2-322">There is a pause at `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` while the pool's compute nodes are created, started, and the commands in the pool's start task are executed.</span></span> <span data-ttu-id="50fb2-323">Usare il [portale di Azure][azure_portal] per monitorare il pool, i nodi di calcolo, il processo e le attività durante e dopo l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="50fb2-323">Use the [Azure portal][azure_portal] to monitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="50fb2-324">Usare il [portale di Azure][azure_portal] o [Microsoft Azure Storage Explorer][storage_explorer] per visualizzare le risorse di archiviazione (contenitori e BLOB) create dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="50fb2-324">Use the [Azure portal][azure_portal] or the [Microsoft Azure Storage Explorer][storage_explorer] to view the Storage resources (containers and blobs) that are created by the application.</span></span>

> [!TIP]
> <span data-ttu-id="50fb2-325">Eseguire lo script *python_tutorial_client.py* dalla directory `azure-batch-samples/Python/Batch/article_samples`.</span><span class="sxs-lookup"><span data-stu-id="50fb2-325">Run the *python_tutorial_client.py* script from within the `azure-batch-samples/Python/Batch/article_samples` directory.</span></span> <span data-ttu-id="50fb2-326">che usa un percorso relativo per l'importazione del modulo `common.helpers`. Perciò se non si esegue lo script da questa directory, è possibile che venga visualizzato il messaggio `ImportError: No module named 'common'`.</span><span class="sxs-lookup"><span data-stu-id="50fb2-326">It uses a relative path for the `common.helpers` module import, so you might see `ImportError: No module named 'common'` if you don't run the script from within this directory.</span></span>
>
>

<span data-ttu-id="50fb2-327">Se si esegue l'esempio con la configurazione predefinita, il tempo di esecuzione tipico è di **circa 5-7 minuti** .</span><span class="sxs-lookup"><span data-stu-id="50fb2-327">Typical execution time is **approximately 5-7 minutes** when you run the sample in its default configuration.</span></span>

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py to container [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt to container [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt to container [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt to container [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks to job [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached the 'Completed' state within the specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] to /home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] to /home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] to /home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="50fb2-328">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="50fb2-328">Next steps</span></span>
<span data-ttu-id="50fb2-329">È possibile modificare *python_tutorial_client.py* e *python_tutorial_task.py* per sperimentare scenari di calcolo diversi.</span><span class="sxs-lookup"><span data-stu-id="50fb2-329">Feel free to make changes to *python_tutorial_client.py* and *python_tutorial_task.py* to experiment with different compute scenarios.</span></span> <span data-ttu-id="50fb2-330">Si può ad esempio provare ad aggiungere un ritardo di esecuzione in *python_tutorial_task.py* per simulare attività con esecuzione prolungata e monitorarle nel portale.</span><span class="sxs-lookup"><span data-stu-id="50fb2-330">For example, try adding an execution delay to *python_tutorial_task.py* to simulate long-running tasks and monitor them in the portal.</span></span> <span data-ttu-id="50fb2-331">Provare ad aggiungere altre attività o a modificare il numero di nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="50fb2-331">Try adding more tasks or adjusting the number of compute nodes.</span></span> <span data-ttu-id="50fb2-332">Aggiungere la logica per la ricerca e l'uso di un pool esistente per ridurre il tempo di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="50fb2-332">Add logic to check for and allow the use of an existing pool to speed execution time.</span></span>

<span data-ttu-id="50fb2-333">Dopo avere acquisito familiarità con il flusso di lavoro di base di una soluzione Batch, è possibile esaminare in dettaglio le funzionalità aggiuntive del servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="50fb2-333">Now that you're familiar with the basic workflow of a Batch solution, it's time to dig in to the additional features of the Batch service.</span></span>

* <span data-ttu-id="50fb2-334">Se non si ha familiarità con il servizio, è consigliabile vedere [Panoramica delle funzionalità di Batch per sviluppatori](batch-api-basics.md) .</span><span class="sxs-lookup"><span data-stu-id="50fb2-334">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
* <span data-ttu-id="50fb2-335">Per altri articoli sullo sviluppo in Batch, vedere **Approfondimenti sullo sviluppo** nel [percorso di apprendimento per Batch][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="50fb2-335">Start on the other Batch development articles under **Development in-depth** in the [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="50fb2-336">Una diversa implementazione dell'elaborazione del carico di lavoro di tipo "prime N parole" con Batch è disponibile nell'esempio [TopNWords][github_topnwords].</span><span class="sxs-lookup"><span data-stu-id="50fb2-336">Check out a different implementation of processing the "top N words" workload with Batch in the [TopNWords][github_topnwords] sample.</span></span>

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
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "Caricare l'applicazione dell'attività e i file di input (dati) nei contenitori"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Creare un pool di Batch"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Creare un processo di Batch"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "Aggiungere attività a un processo"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "Monitorare le attività"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Scaricare l'output delle attività dal servizio di archiviazione"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Flusso di lavoro della soluzione Batch (diagramma completo)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "Credenziali di Batch nel portale"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "Credenziali del servizio di archiviazione nel portale"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Flusso di lavoro della soluzione Batch (diagramma minimo)"
