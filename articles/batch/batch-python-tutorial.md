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
# <a name="get-started-with-hello-batch-sdk-for-python"></a><span data-ttu-id="45cdb-103">Introduzione a hello Batch SDK per Python</span><span class="sxs-lookup"><span data-stu-id="45cdb-103">Get started with hello Batch SDK for Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="45cdb-104">.NET</span><span class="sxs-lookup"><span data-stu-id="45cdb-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="45cdb-105">Python</span><span class="sxs-lookup"><span data-stu-id="45cdb-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="45cdb-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="45cdb-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="45cdb-107">Nozioni di base hello di [Azure Batch] [ azure_batch] hello e [Python Batch] [ py_azure_sdk] client come illustrato una piccola applicazione Batch scritta in Python.</span><span class="sxs-lookup"><span data-stu-id="45cdb-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch Python][py_azure_sdk] client as we discuss a small Batch application written in Python.</span></span> <span data-ttu-id="45cdb-108">Vengono analizzati come due esempio script utilizzare hello Batch servizio tooprocess un carico di lavoro parallelo in macchine virtuali Linux in cloud hello e la loro interazione [di archiviazione di Azure](../storage/common/storage-introduction.md) per gestione temporanea di file e il recupero.</span><span class="sxs-lookup"><span data-stu-id="45cdb-108">We look at how two sample scripts use hello Batch service tooprocess a parallel workload on Linux virtual machines in hello cloud, and how they interact with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="45cdb-109">Si illustra Batch applicazione flusso di lavoro comune e acquisire una comprensione di base dei componenti principali hello del Batch, ad esempio i processi, attività, i pool e nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="45cdb-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="45cdb-110">![Flusso di lavoro della soluzione Batch (di base)][11]</span><span class="sxs-lookup"><span data-stu-id="45cdb-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="45cdb-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="45cdb-111">Prerequisites</span></span>
<span data-ttu-id="45cdb-112">Questo articolo presuppone che l'utente sappia usare Python e Linux</span><span class="sxs-lookup"><span data-stu-id="45cdb-112">This article assumes that you have a working knowledge of Python and familiarity with Linux.</span></span> <span data-ttu-id="45cdb-113">Si presuppone inoltre che si è in grado di toosatisfy hello creazione requisiti dell'account specificate di seguito per Azure e hello Batch e servizi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="45cdb-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="45cdb-114">Account</span><span class="sxs-lookup"><span data-stu-id="45cdb-114">Accounts</span></span>
* <span data-ttu-id="45cdb-115">**Account Azure**: se non si ha già una sottoscrizione di Azure, [creare un account Azure gratuito][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="45cdb-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="45cdb-116">**Account Batch**: dopo aver creato una sottoscrizione di Azure, [creare un account Azure Batch](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="45cdb-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="45cdb-117">**Account di archiviazione**: vedere [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="45cdb-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

### <a name="code-sample"></a><span data-ttu-id="45cdb-118">Esempio di codice</span><span class="sxs-lookup"><span data-stu-id="45cdb-118">Code sample</span></span>
<span data-ttu-id="45cdb-119">esercitazione di Python Hello [nell'esempio di codice] [ github_article_samples] è uno dei molti esempi di codice di Batch, vedere hello hello [esempi di azure batch] [ github_samples] repository in GitHub.</span><span class="sxs-lookup"><span data-stu-id="45cdb-119">hello Python tutorial [code sample][github_article_samples] is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="45cdb-120">È possibile scaricare tutti gli esempi di hello facendo **Clone o download > Download ZIP** nella home page del repository hello o facendo clic su hello [azure-batch-esempi-master.zip] [ github_samples_zip]collegamento diretto.</span><span class="sxs-lookup"><span data-stu-id="45cdb-120">You can download all hello samples by clicking **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="45cdb-121">Dopo aver estratto il contenuto di hello del file ZIP hello, script hello due per questa esercitazione si trovano in hello `article_samples` directory:</span><span class="sxs-lookup"><span data-stu-id="45cdb-121">Once you've extracted hello contents of hello ZIP file, hello two scripts for this tutorial are found in hello `article_samples` directory:</span></span>

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a><span data-ttu-id="45cdb-122">Ambiente Python</span><span class="sxs-lookup"><span data-stu-id="45cdb-122">Python environment</span></span>
<span data-ttu-id="45cdb-123">hello toorun *python_tutorial_client.py* script di esempio nella workstation locale, è necessario un **interprete Python** compatibile con la versione **2.7** o **3.3 +**.</span><span class="sxs-lookup"><span data-stu-id="45cdb-123">toorun hello *python_tutorial_client.py* sample script on your local workstation, you need a **Python interpreter** compatible with version **2.7** or **3.3+**.</span></span> <span data-ttu-id="45cdb-124">script Hello è stato testato su Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="45cdb-124">hello script has been tested on both Linux and Windows.</span></span>

### <a name="cryptography-dependencies"></a><span data-ttu-id="45cdb-125">Dipendenze di cryptography</span><span class="sxs-lookup"><span data-stu-id="45cdb-125">cryptography dependencies</span></span>
<span data-ttu-id="45cdb-126">È necessario installare le dipendenze di hello per hello [crittografia] [ crypto] libreria, richiesta da hello `azure-batch` e `azure-storage` pacchetti Python.</span><span class="sxs-lookup"><span data-stu-id="45cdb-126">You must install hello dependencies for hello [cryptography][crypto] library, required by hello `azure-batch` and `azure-storage` Python packages.</span></span> <span data-ttu-id="45cdb-127">Eseguire una delle seguente operazioni appropriate per la piattaforma hello o fare riferimento toohello [installazione crittografia] [ crypto_install] dettagli per ulteriori informazioni:</span><span class="sxs-lookup"><span data-stu-id="45cdb-127">Perform one of hello following operations appropriate for your platform, or refer toohello [cryptography installation][crypto_install] details for more information:</span></span>

* <span data-ttu-id="45cdb-128">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="45cdb-128">Ubuntu</span></span>

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* <span data-ttu-id="45cdb-129">CentOS</span><span class="sxs-lookup"><span data-stu-id="45cdb-129">CentOS</span></span>

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* <span data-ttu-id="45cdb-130">SLES/OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="45cdb-130">SLES/OpenSUSE</span></span>

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* <span data-ttu-id="45cdb-131">Windows</span><span class="sxs-lookup"><span data-stu-id="45cdb-131">Windows</span></span>

    `pip install cryptography`

> [!NOTE]
> <span data-ttu-id="45cdb-132">Se l'installazione di Python 3.3 + su Linux, utilizzare equivalenti python3 hello per le dipendenze di Python hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-132">If installing for Python 3.3+ on Linux, use hello python3 equivalents for hello Python dependencies.</span></span> <span data-ttu-id="45cdb-133">Ad esempio, in Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span><span class="sxs-lookup"><span data-stu-id="45cdb-133">For example, on Ubuntu: `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`</span></span>
>
>

### <a name="azure-packages"></a><span data-ttu-id="45cdb-134">Pacchetti di Azure</span><span class="sxs-lookup"><span data-stu-id="45cdb-134">Azure packages</span></span>
<span data-ttu-id="45cdb-135">Installare quindi hello **Azure Batch** e **di archiviazione di Azure** pacchetti Python.</span><span class="sxs-lookup"><span data-stu-id="45cdb-135">Next, install hello **Azure Batch** and **Azure Storage** Python packages.</span></span> <span data-ttu-id="45cdb-136">È possibile installare entrambi i pacchetti utilizzando **pip** hello e *requirements.txt* disponibili qui:</span><span class="sxs-lookup"><span data-stu-id="45cdb-136">You can install both packages by using **pip** and hello *requirements.txt* found here:</span></span>

`/azure-batch-samples/Python/Batch/requirements.txt`

<span data-ttu-id="45cdb-137">Il seguente problema **pip** pacchetti di Batch e l'archiviazione hello tooinstall di comando:</span><span class="sxs-lookup"><span data-stu-id="45cdb-137">Issue following **pip** command tooinstall hello Batch and Storage packages:</span></span>

`pip install -r requirements.txt`

<span data-ttu-id="45cdb-138">In alternativa, è possibile installare hello [azure batch] [ pypi_batch] e [archiviazione di azure] [ pypi_storage] Python pacchetti manualmente:</span><span class="sxs-lookup"><span data-stu-id="45cdb-138">Or, you can install hello [azure-batch][pypi_batch] and [azure-storage][pypi_storage] Python packages manually:</span></span>

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> <span data-ttu-id="45cdb-139">Se si utilizza un account senza privilegi, potrebbe essere necessario tooprefix i comandi con `sudo`.</span><span class="sxs-lookup"><span data-stu-id="45cdb-139">If you are using an unprivileged account, you may need tooprefix your commands with `sudo`.</span></span> <span data-ttu-id="45cdb-140">ad esempio `sudo pip install -r requirements.txt`.</span><span class="sxs-lookup"><span data-stu-id="45cdb-140">For example, `sudo pip install -r requirements.txt`.</span></span> <span data-ttu-id="45cdb-141">Per altre informazioni sull'installazione dei pacchetti Python, vedere [Installing Packages][pypi_install] (Installazione di pacchetti) in python.org.</span><span class="sxs-lookup"><span data-stu-id="45cdb-141">For more information on installing Python packages, see [Installing Packages][pypi_install] on python.org.</span></span>
>
>

## <a name="batch-python-tutorial-code-sample"></a><span data-ttu-id="45cdb-142">Esempio di codice per l'esercitazione di Batch Python</span><span class="sxs-lookup"><span data-stu-id="45cdb-142">Batch Python tutorial code sample</span></span>
<span data-ttu-id="45cdb-143">Nell'esempio di codice dell'esercitazione Batch Python Hello è costituito da due script Python e alcuni file di dati.</span><span class="sxs-lookup"><span data-stu-id="45cdb-143">hello Batch Python tutorial code sample consists of two Python scripts and a few data files.</span></span>

* <span data-ttu-id="45cdb-144">**python_tutorial_client.py**: interagisce con tooexecute di servizi di archiviazione e Batch hello un carico di lavoro parallelo in nodi di calcolo (macchine virtuali).</span><span class="sxs-lookup"><span data-stu-id="45cdb-144">**python_tutorial_client.py**: Interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="45cdb-145">Hello *python_tutorial_client.py* script viene eseguito nella workstation locale.</span><span class="sxs-lookup"><span data-stu-id="45cdb-145">hello *python_tutorial_client.py* script runs on your local workstation.</span></span>
* <span data-ttu-id="45cdb-146">**python_tutorial_task.py**: hello dello script eseguito in nodi di calcolo in Azure tooperform il lavoro effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-146">**python_tutorial_task.py**: hello script that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="45cdb-147">Nell'esempio hello *python_tutorial_task.py* analizza hello testo in un file scaricato dall'archiviazione di Azure (file di input di hello).</span><span class="sxs-lookup"><span data-stu-id="45cdb-147">In hello sample, *python_tutorial_task.py* parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="45cdb-148">Quindi, produce un file di testo (file di output di hello) che contiene un elenco di hello prime tre parole che vengono visualizzati nel file di input hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-148">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="45cdb-149">Dopo la creazione di file di output di hello, *python_tutorial_task.py* caricamenti hello tooAzure file archiviazione.</span><span class="sxs-lookup"><span data-stu-id="45cdb-149">After it creates hello output file, *python_tutorial_task.py* uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="45cdb-150">Questo rende disponibili per lo script client di toohello download esecuzione sulla workstation.</span><span class="sxs-lookup"><span data-stu-id="45cdb-150">This makes it available for download toohello client script running on your workstation.</span></span> <span data-ttu-id="45cdb-151">Hello *python_tutorial_task.py* script viene eseguito in parallelo su più nodi di calcolo nel servizio Batch hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-151">hello *python_tutorial_task.py* script runs in parallel on multiple compute nodes in hello Batch service.</span></span>
* <span data-ttu-id="45cdb-152">**./Data/taskdata\*. txt**: questi file di tre testo forniscono input hello per le attività di hello eseguite sul hello nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="45cdb-152">**./data/taskdata\*.txt**: These three text files provide hello input for hello tasks that run on hello compute nodes.</span></span>

<span data-ttu-id="45cdb-153">Hello seguente diagramma illustra hello primaria le operazioni eseguite dagli script di hello client e attività.</span><span class="sxs-lookup"><span data-stu-id="45cdb-153">hello following diagram illustrates hello primary operations that are performed by hello client and task scripts.</span></span> <span data-ttu-id="45cdb-154">Questo flusso di lavoro di base è tipico di molte soluzioni di calcolo create con Batch.</span><span class="sxs-lookup"><span data-stu-id="45cdb-154">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="45cdb-155">Mentre non vengono visualizzati tutte le funzionalità disponibili nel servizio Batch hello, quasi ogni scenario di Batch include parti del flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="45cdb-155">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="45cdb-156">![Flusso di lavoro dell'esempio di Batch][8]</span><span class="sxs-lookup"><span data-stu-id="45cdb-156">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="45cdb-157">**Passaggio 1.**</span><span class="sxs-lookup"><span data-stu-id="45cdb-157">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="45cdb-158">Creare **contenitori** nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="45cdb-158">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="45cdb-159">
[**Passaggio 2.**](#step-2-upload-task-script-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="45cdb-159">
[**Step 2.**](#step-2-upload-task-script-and-data-files)</span></span> <span data-ttu-id="45cdb-160">Caricare toocontainers di file di script e l'input dell'attività.</span><span class="sxs-lookup"><span data-stu-id="45cdb-160">Upload task script and input files toocontainers.</span></span><br/><span data-ttu-id="45cdb-161">
[**Passaggio 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="45cdb-161">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="45cdb-162">Creare un **pool** di Batch.</span><span class="sxs-lookup"><span data-stu-id="45cdb-162">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="45cdb-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="45cdb-163">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="45cdb-164">Hello pool **StartTask** download hello attività script (python_tutorial_task.py) toonodes che si connettono pool hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-164">hello pool **StartTask** downloads hello task script (python_tutorial_task.py) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="45cdb-165">
[**Passaggio 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="45cdb-165">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="45cdb-166">Creare un **processo** di Batch.</span><span class="sxs-lookup"><span data-stu-id="45cdb-166">Create a Batch **job**.</span></span><br/><span data-ttu-id="45cdb-167">
[**Passaggio 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="45cdb-167">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="45cdb-168">Aggiungere **attività** toohello processo.</span><span class="sxs-lookup"><span data-stu-id="45cdb-168">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="45cdb-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="45cdb-169">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="45cdb-170">attività di Hello sono tooexecute pianificati sui nodi.</span><span class="sxs-lookup"><span data-stu-id="45cdb-170">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="45cdb-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="45cdb-171">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="45cdb-172">Ogni attività scarica i rispettivi dati di input da Archiviazione di Azure e quindi avvia l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="45cdb-172">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="45cdb-173">
[**Passaggio 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="45cdb-173">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="45cdb-174">Monitorare le attività.</span><span class="sxs-lookup"><span data-stu-id="45cdb-174">Monitor tasks.</span></span><br/>
  <span data-ttu-id="45cdb-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="45cdb-175">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="45cdb-176">Come vengono completate, caricamento del loro tooAzure di dati di output archiviazione.</span><span class="sxs-lookup"><span data-stu-id="45cdb-176">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="45cdb-177">
[**Passaggio 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="45cdb-177">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="45cdb-178">Scaricare l'output delle attività dal servizio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="45cdb-178">Download task output from Storage.</span></span>

<span data-ttu-id="45cdb-179">Come indicato, non tutte le soluzioni Batch eseguono esattamente questi passaggi e potrebbero includerne molti altri, ma l'esempio illustra i processi comuni presenti in una soluzione Batch.</span><span class="sxs-lookup"><span data-stu-id="45cdb-179">As mentioned, not every Batch solution performs these exact steps, and may include many more, but this sample demonstrates common processes found in a Batch solution.</span></span>

## <a name="prepare-client-script"></a><span data-ttu-id="45cdb-180">Preparare lo script client</span><span class="sxs-lookup"><span data-stu-id="45cdb-180">Prepare client script</span></span>
<span data-ttu-id="45cdb-181">Prima di eseguire l'esempio hello, aggiungere le credenziali dell'account di archiviazione e Batch troppo*python_tutorial_client.py*.</span><span class="sxs-lookup"><span data-stu-id="45cdb-181">Before you run hello sample, add your Batch and Storage account credentials too*python_tutorial_client.py*.</span></span> <span data-ttu-id="45cdb-182">Se non è già stato fatto, aprire il file hello i Preferiti hello editor e l'aggiornamento dopo le righe con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="45cdb-182">If you have not done so already, open hello file in your favorite editor and update hello following lines with your credentials.</span></span>

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

<span data-ttu-id="45cdb-183">È possibile trovare le credenziali dell'account Batch e l'archiviazione all'interno di blade account hello di ogni servizio in hello [portale di Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="45cdb-183">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="45cdb-184">![Batch credenziali nel portale di hello][9]
![le credenziali di archiviazione nel portale di hello][10]</span><span class="sxs-lookup"><span data-stu-id="45cdb-184">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="45cdb-185">Nelle seguenti sezioni di hello, consente di analizzare i passi hello utilizzati dal hello script tooprocess un carico di lavoro in hello servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="45cdb-185">In hello following sections, we analyze hello steps used by hello scripts tooprocess a workload in hello Batch service.</span></span> <span data-ttu-id="45cdb-186">Si consiglia di toorefer regolarmente toohello script nell'editor mentre si percorrere rest hello dell'articolo hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-186">We encourage you toorefer regularly toohello scripts in your editor while you work your way through hello rest of hello article.</span></span>

<span data-ttu-id="45cdb-187">Passare toohello seguente riga **python_tutorial_client.py** toostart con il passaggio 1:</span><span class="sxs-lookup"><span data-stu-id="45cdb-187">Navigate toohello following line in **python_tutorial_client.py** toostart with Step 1:</span></span>

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="45cdb-188">Passaggio 1: Creare contenitori di archiviazione</span><span class="sxs-lookup"><span data-stu-id="45cdb-188">Step 1: Create Storage containers</span></span>
<span data-ttu-id="45cdb-189">![Creare contenitori in Archiviazione di Azure][1]
</span><span class="sxs-lookup"><span data-stu-id="45cdb-189">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="45cdb-190">Batch include il supporto predefinito per l'interazione con Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="45cdb-190">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="45cdb-191">I contenitori nell'account di archiviazione offrono file hello necessari per le attività di hello eseguite nell'account di Batch.</span><span class="sxs-lookup"><span data-stu-id="45cdb-191">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="45cdb-192">i contenitori di Hello offrono anche un posizionamento toostore hello output di dati che producono attività hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-192">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="45cdb-193">in primo luogo Hello hello *python_tutorial_client.py* script consente di creare tre contenitori in [archiviazione Blob di Azure](../storage/common/storage-introduction.md#blob-storage):</span><span class="sxs-lookup"><span data-stu-id="45cdb-193">hello first thing hello *python_tutorial_client.py* script does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md#blob-storage):</span></span>

* <span data-ttu-id="45cdb-194">**applicazione**: questo contenitore verranno archiviati hello Python script eseguiti dalle attività hello, *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="45cdb-194">**application**: This container will store hello Python script run by hello tasks, *python_tutorial_task.py*.</span></span>
* <span data-ttu-id="45cdb-195">**input**: attività scaricherà tooprocess i file di dati hello dal hello *input* contenitore.</span><span class="sxs-lookup"><span data-stu-id="45cdb-195">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="45cdb-196">**output**: al termine dell'elaborazione del file di input di attività, verrà caricato hello risultati toohello *output* contenitore.</span><span class="sxs-lookup"><span data-stu-id="45cdb-196">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="45cdb-197">In ordine toointeract con uno spazio di archiviazione account e creare contenitori, utilizziamo hello [archiviazione di azure] [ pypi_storage] pacchetto toocreate un [BlockBlobService] [ py_blockblobservice] oggetto--hello ""blob client.</span><span class="sxs-lookup"><span data-stu-id="45cdb-197">In order toointeract with a Storage account and create containers, we use hello [azure-storage][pypi_storage] package toocreate a [BlockBlobService][py_blockblobservice] object--hello "blob client."</span></span> <span data-ttu-id="45cdb-198">È quindi possibile creare tre contenitori nell'account di archiviazione di hello utilizzando client hello del blob.</span><span class="sxs-lookup"><span data-stu-id="45cdb-198">We then create three containers in hello Storage account using hello blob client.</span></span>

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

<span data-ttu-id="45cdb-199">Dopo avere creati i contenitori di hello, un'applicazione hello ora possibile caricare file hello che verranno utilizzati dalle attività hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="45cdb-200">[Come toouse archiviazione Blob di Azure da Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) fornisce una buona panoramica dell'utilizzo di BLOB e contenitori di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="45cdb-200">[How toouse Azure Blob storage from Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="45cdb-201">Quando si inizia a batch deve essere superiore hello dell'elenco di lettura.</span><span class="sxs-lookup"><span data-stu-id="45cdb-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-script-and-data-files"></a><span data-ttu-id="45cdb-202">Passaggio 2: Caricare lo script attività e i file di dati</span><span class="sxs-lookup"><span data-stu-id="45cdb-202">Step 2: Upload task script and data files</span></span>
<span data-ttu-id="45cdb-203">![Attività di caricamento dell'applicazione e di input (dati) file toocontainers][2]
</span><span class="sxs-lookup"><span data-stu-id="45cdb-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="45cdb-204">Nel file hello caricare operazione *python_tutorial_client.py* prima definisce le raccolte di **applicazione** e **input** percorsi di file in cui si trovano sul computer locale hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-204">In hello file upload operation, *python_tutorial_client.py* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="45cdb-205">Carica quindi questi contenitori toohello file creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

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

<span data-ttu-id="45cdb-206">Mediante la comprensione di elenco, hello `upload_file_to_container` funzione viene chiamata per ogni file nelle raccolte di hello e due [ResourceFile] [ py_resource_file] raccolte vengono popolate.</span><span class="sxs-lookup"><span data-stu-id="45cdb-206">Using list comprehension, hello `upload_file_to_container` function is called for each file in hello collections, and two [ResourceFile][py_resource_file] collections are populated.</span></span> <span data-ttu-id="45cdb-207">Hello `upload_file_to_container` funzione viene visualizzata di seguito:</span><span class="sxs-lookup"><span data-stu-id="45cdb-207">hello `upload_file_to_container` function appears below:</span></span>

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

### <a name="resourcefiles"></a><span data-ttu-id="45cdb-208">ResourceFiles</span><span class="sxs-lookup"><span data-stu-id="45cdb-208">ResourceFiles</span></span>
<span data-ttu-id="45cdb-209">Oggetto [ResourceFile] [ py_resource_file] fornisce operazioni in Batch con file di tooa URL hello in archiviazione di Azure che viene scaricato tooa nodo di calcolo prima di tale attività è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="45cdb-209">A [ResourceFile][py_resource_file] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="45cdb-210">Hello [ResourceFile][py_resource_file]. **blob_source** proprietà specifica hello URL completo del file hello presenti in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="45cdb-210">hello [ResourceFile][py_resource_file].**blob_source** property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="45cdb-211">Hello URL può includere una firma di accesso condiviso (SAS) che fornisce l'accesso sicuro toohello file.</span><span class="sxs-lookup"><span data-stu-id="45cdb-211">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="45cdb-212">La maggior parte dei tipi di attività in Batch include una proprietà *ResourceFiles*, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="45cdb-212">Most task types in Batch include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="45cdb-213">[CloudTask][py_task]</span><span class="sxs-lookup"><span data-stu-id="45cdb-213">[CloudTask][py_task]</span></span>
* <span data-ttu-id="45cdb-214">[StartTask][py_starttask]</span><span class="sxs-lookup"><span data-stu-id="45cdb-214">[StartTask][py_starttask]</span></span>
* <span data-ttu-id="45cdb-215">[JobPreparationTask][py_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="45cdb-215">[JobPreparationTask][py_jobpreptask]</span></span>
* <span data-ttu-id="45cdb-216">[JobReleaseTask][py_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="45cdb-216">[JobReleaseTask][py_jobreltask]</span></span>

<span data-ttu-id="45cdb-217">In questo esempio non utilizza hello JobPreparationTask o JobReleaseTask tipi di attività, ma è possibile leggere informazioni su di essi in [attività Esegui processo di preparazione e completamento del Batch di Azure i nodi di calcolo](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="45cdb-217">This sample does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="45cdb-218">Firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="45cdb-218">Shared access signature (SAS)</span></span>
<span data-ttu-id="45cdb-219">Firme di accesso condiviso sono stringhe che forniscono l'accesso sicuro toocontainers e BLOB in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="45cdb-219">Shared access signatures are strings that provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="45cdb-220">Hello *python_tutorial_client.py* script vengono utilizzati entrambi i blob e contenitore firme di accesso condiviso, viene illustrato come accedere stringhe firma tooobtain questi condiviso dal servizio di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-220">hello *python_tutorial_client.py* script uses both blob and container shared access signatures, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="45cdb-221">**Firme di accesso condiviso di BLOB**: utilizza StartTask hello pool blob firme di accesso condiviso durante il download di hello attività script e input i file di dati dall'archivio (vedere [passaggio #3](#step-3-create-batch-pool) sotto).</span><span class="sxs-lookup"><span data-stu-id="45cdb-221">**Blob shared access signatures**: hello pool's StartTask uses blob shared access signatures when it downloads hello task script and input data files from Storage (see [Step #3](#step-3-create-batch-pool) below).</span></span> <span data-ttu-id="45cdb-222">Hello `upload_file_to_container` funzionare in *python_tutorial_client.py* contiene codice hello che ottiene la firma di accesso condiviso del blob ogni.</span><span class="sxs-lookup"><span data-stu-id="45cdb-222">hello `upload_file_to_container` function in *python_tutorial_client.py* contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="45cdb-223">Esegue l'operazione chiamando [BlockBlobService.make_blob_url] [ py_make_blob_url] nel modulo di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-223">It does so by calling [BlockBlobService.make_blob_url][py_make_blob_url] in hello Storage module.</span></span>
* <span data-ttu-id="45cdb-224">**Firma di accesso condiviso del contenitore**: come le operazioni sul nodo di calcolo hello al termine di ogni attività, viene caricato il toohello di file di output *output* contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="45cdb-224">**Container shared access signature**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="45cdb-225">toodo, *python_tutorial_task.py* utilizza una firma di accesso condiviso di contenitore che fornisce l'accesso in scrittura toohello contenitore.</span><span class="sxs-lookup"><span data-stu-id="45cdb-225">toodo so, *python_tutorial_task.py* uses a container shared access signature that provides write access toohello container.</span></span> <span data-ttu-id="45cdb-226">Hello `get_container_sas_token` funzionare in *python_tutorial_client.py* Ottiene firma di accesso condiviso del contenitore di hello, che viene quindi passata come attività di toohello un argomento della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="45cdb-226">hello `get_container_sas_token` function in *python_tutorial_client.py* obtains hello container's shared access signature, which is then passed as a command-line argument toohello tasks.</span></span> <span data-ttu-id="45cdb-227">Passaggio &#5;, [processo di aggiunta attività tooa](#step-5-add-tasks-to-job), viene descritto l'utilizzo di hello del contenitore hello SAS.</span><span class="sxs-lookup"><span data-stu-id="45cdb-227">Step #5, [Add tasks tooa job](#step-5-add-tasks-to-job), discusses hello usage of hello container SAS.</span></span>

> [!TIP]
> <span data-ttu-id="45cdb-228">Check-out di serie in due parti hello sulle firme di accesso condiviso, [parte 1: modello di firma di accesso condiviso hello comprensione](../storage/common/storage-dotnet-shared-access-signature-part-1.md) e [parte 2: creare e usare una firma di accesso condiviso con il servizio Blob hello](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn ulteriori informazioni su come fornire accesso sicuro toodata nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="45cdb-228">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a SAS with hello Blob service](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="45cdb-229">Passaggio 3: Creare un pool di Batch</span><span class="sxs-lookup"><span data-stu-id="45cdb-229">Step 3: Create Batch pool</span></span>
<span data-ttu-id="45cdb-230">![Creare un pool di Batch][3]
</span><span class="sxs-lookup"><span data-stu-id="45cdb-230">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="45cdb-231">Un **pool** di Batch è una raccolta di nodi di calcolo (macchine virtuali) in cui Batch esegue le attività di un processo.</span><span class="sxs-lookup"><span data-stu-id="45cdb-231">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="45cdb-232">Dopo che viene caricato hello attività script e i dati file toohello account di archiviazione, *python_tutorial_client.py* avvia l'interazione con il servizio Batch hello mediante il modulo di Python Batch hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-232">After it uploads hello task script and data files toohello Storage account, *python_tutorial_client.py* starts its interaction with hello Batch service by using hello Batch Python module.</span></span> <span data-ttu-id="45cdb-233">toodo, un [BatchServiceClient] [ py_batchserviceclient] viene creato:</span><span class="sxs-lookup"><span data-stu-id="45cdb-233">toodo so, a [BatchServiceClient][py_batchserviceclient] is created:</span></span>

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

<span data-ttu-id="45cdb-234">Successivamente, viene creato un pool di nodi di calcolo in hello account Batch con una chiamata troppo`create_pool`.</span><span class="sxs-lookup"><span data-stu-id="45cdb-234">Next, a pool of compute nodes is created in hello Batch account with a call too`create_pool`.</span></span>

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

<span data-ttu-id="45cdb-235">Quando si crea un pool, si definisce un [PoolAddParameter] [ py_pooladdparam] che consente di specificare diverse proprietà per il pool di hello:</span><span class="sxs-lookup"><span data-stu-id="45cdb-235">When you create a pool, you define a [PoolAddParameter][py_pooladdparam] that specifies several properties for hello pool:</span></span>

* <span data-ttu-id="45cdb-236">**ID** del pool di hello (*id* - obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="45cdb-236">**ID** of hello pool (*id* - required)</span></span><p/><span data-ttu-id="45cdb-237">Così come la maggior parte delle entità in Batch, il nuovo pool deve avere un ID univoco all'interno dell'account Batch.</span><span class="sxs-lookup"><span data-stu-id="45cdb-237">As with most entities in Batch, your new pool must have a unique ID within your Batch account.</span></span> <span data-ttu-id="45cdb-238">Il codice fa riferimento utilizzando l'ID del pool di toothis ed è identificare pool hello in hello Azure [portale][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="45cdb-238">Your code refers toothis pool using its ID, and it's how you identify hello pool in hello Azure [portal][azure_portal].</span></span>
* <span data-ttu-id="45cdb-239">**Numero di nodi di calcolo** (*target_dedicated*: obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="45cdb-239">**Number of compute nodes** (*target_dedicated* - required)</span></span><p/><span data-ttu-id="45cdb-240">Questa proprietà specifica il numero di macchine virtuali devono essere distribuite nel pool di hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-240">This property specifies how many VMs should be deployed in hello pool.</span></span> <span data-ttu-id="45cdb-241">È importante toonote dispongano di tutti gli account Batch predefinito **quota** che limiti hello numero di **core** (e di conseguenza, i nodi di calcolo) in un account Batch.</span><span class="sxs-lookup"><span data-stu-id="45cdb-241">It is important toonote that all Batch accounts have a default **quota** that limits hello number of **cores** (and thus, compute nodes) in a Batch account.</span></span> <span data-ttu-id="45cdb-242">È possibile trovare le quote predefinite hello e istruzioni su come troppo[aumentare la quota](batch-quota-limit.md#increase-a-quota) (come il numero massimo di hello di core nell'account di Batch) in [quote e limiti per il servizio Azure Batch hello](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="45cdb-242">You can find hello default quotas and instructions on how too[increase a quota](batch-quota-limit.md#increase-a-quota) (such as hello maximum number of cores in your Batch account) in [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="45cdb-243">Se il pool non raggiunge più di X nodi, ad esempio,</span><span class="sxs-lookup"><span data-stu-id="45cdb-243">If you find yourself asking "Why won't my pool reach more than X nodes?"</span></span> <span data-ttu-id="45cdb-244">Questa quota core può essere causa hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-244">this core quota may be hello cause.</span></span>
* <span data-ttu-id="45cdb-245">**Sistema operativo** per i nodi (*virtual_machine_configuration***o***cloud_service_configuration*: obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="45cdb-245">**Operating system** for nodes (*virtual_machine_configuration* **or** *cloud_service_configuration* - required)</span></span><p/><span data-ttu-id="45cdb-246">In *python_tutorial_client.py* viene creato un pool di nodi Linux tramite [VirtualMachineConfiguration][py_vm_config].</span><span class="sxs-lookup"><span data-stu-id="45cdb-246">In *python_tutorial_client.py*, we create a pool of Linux nodes using a [VirtualMachineConfiguration][py_vm_config].</span></span> <span data-ttu-id="45cdb-247">Hello `select_latest_verified_vm_image_with_node_agent_sku` funzionare in `common.helpers` semplifica l'utilizzo di [macchine virtuali di Azure Marketplace] [ vm_marketplace] immagini.</span><span class="sxs-lookup"><span data-stu-id="45cdb-247">hello `select_latest_verified_vm_image_with_node_agent_sku` function in `common.helpers` simplifies working with [Azure Virtual Machines Marketplace][vm_marketplace] images.</span></span> <span data-ttu-id="45cdb-248">Per altre informazioni sull'uso delle immagini del Marketplace, vedere [Effettuare il provisioning di nodi di calcolo Linux nei pool di Azure Batch](batch-linux-nodes.md) .</span><span class="sxs-lookup"><span data-stu-id="45cdb-248">See [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information about using Marketplace images.</span></span>
* <span data-ttu-id="45cdb-249">**Dimensione dei nodi di calcolo** (*vm_size*: obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="45cdb-249">**Size of compute nodes** (*vm_size* - required)</span></span><p/><span data-ttu-id="45cdb-250">Dato che vengono specificati nodi Linux per [VirtualMachineConfiguration][py_vm_config], viene specificata una dimensione di VM, in questo esempio `STANDARD_A1`, in base a quanto descritto in [Dimensioni delle macchine virtuali in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="45cdb-250">Since we're specifying Linux nodes for our [VirtualMachineConfiguration][py_vm_config], we specify a VM size (`STANDARD_A1` in this sample) from [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="45cdb-251">Per altre informazioni, vedere [Effettuare il provisioning di nodi di calcolo Linux nei pool di Azure Batch](batch-linux-nodes.md) .</span><span class="sxs-lookup"><span data-stu-id="45cdb-251">Again, see [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information.</span></span>
* <span data-ttu-id="45cdb-252">**Attività di avvio** (*start_task*: non obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="45cdb-252">**Start task** (*start_task* - not required)</span></span><p/><span data-ttu-id="45cdb-253">Insieme a hello sopra le proprietà del nodo fisico, è inoltre possibile specificare un [StartTask] [ py_starttask] per pool hello (non è obbligatorio).</span><span class="sxs-lookup"><span data-stu-id="45cdb-253">Along with hello above physical node properties, you may also specify a [StartTask][py_starttask] for hello pool (it is not required).</span></span> <span data-ttu-id="45cdb-254">Hello StartTask viene eseguito in ogni nodo come nodo aggiunto pool hello e ogni volta che un nodo viene riavviato.</span><span class="sxs-lookup"><span data-stu-id="45cdb-254">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="45cdb-255">Hello StartTask è particolarmente utile per la preparazione dei nodi di calcolo per l'esecuzione di attività, ad esempio l'installazione di applicazioni di hello che vengono eseguite le attività hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-255">hello StartTask is especially useful for preparing compute nodes for hello execution of tasks, such as installing hello applications that your tasks run.</span></span><p/><span data-ttu-id="45cdb-256">In questa applicazione di esempio, hello StartTask copia i file hello scaricati dall'archiviazione (che vengono specificati usando del StartTask hello **resource_files** proprietà) da hello StartTask *directorydilavoro* toohello *condivisa* directory che possono accedere a tutte le attività in esecuzione nel nodo hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-256">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello StartTask's **resource_files** property) from hello StartTask *working directory* toohello *shared* directory that all tasks running on hello node can access.</span></span> <span data-ttu-id="45cdb-257">In pratica, questa copia `python_tutorial_task.py` toohello directory condivise su ciascun nodo come nodo hello join pool hello, in modo che qualsiasi attività che vengono eseguite sul nodo hello può accedervi.</span><span class="sxs-lookup"><span data-stu-id="45cdb-257">Essentially, this copies `python_tutorial_task.py` toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

<span data-ttu-id="45cdb-258">È possibile riscontrare hello chiamata toohello `wrap_commands_in_shell` funzione di supporto.</span><span class="sxs-lookup"><span data-stu-id="45cdb-258">You may notice hello call toohello `wrap_commands_in_shell` helper function.</span></span> <span data-ttu-id="45cdb-259">Questa funzione acquisisce una raccolta di comandi separati e crea una singola riga di comando appropriata per la proprietà della riga di comando dell'attività.</span><span class="sxs-lookup"><span data-stu-id="45cdb-259">This function takes a collection of separate commands and creates a single command line appropriate for a task's command-line property.</span></span>

<span data-ttu-id="45cdb-260">Inoltre rilevanti nel frammento di codice hello sopra sono utilizzare hello due variabili di ambiente nell'hello **riga di comando** proprietà di hello StartTask: `AZ_BATCH_TASK_WORKING_DIR` e `AZ_BATCH_NODE_SHARED_DIR`.</span><span class="sxs-lookup"><span data-stu-id="45cdb-260">Also notable in hello code snippet above is hello use of two environment variables in hello **command_line** property of hello StartTask: `AZ_BATCH_TASK_WORKING_DIR` and `AZ_BATCH_NODE_SHARED_DIR`.</span></span> <span data-ttu-id="45cdb-261">Ogni nodo di calcolo all'interno di un Batch viene configurato automaticamente con alcune variabili di ambiente sono tooBatch specifico.</span><span class="sxs-lookup"><span data-stu-id="45cdb-261">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="45cdb-262">Qualsiasi processo che viene eseguita da un'attività con le variabili di ambiente toothese di accesso.</span><span class="sxs-lookup"><span data-stu-id="45cdb-262">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="45cdb-263">toofind ulteriori informazioni sulle variabili di ambiente hello sono disponibili nei nodi di calcolo in un pool di Batch, nonché informazioni sulla directory di lavoro attività, vedere **impostazioni di ambiente per l'attività** e **file e directory**  in hello [panoramica delle funzionalità di Azure Batch](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="45cdb-263">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, as well as information on task working directories, see **Environment settings for tasks** and **Files and directories** in hello [overview of Azure Batch features](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="45cdb-264">Passaggio 4: Creare un processo di Batch</span><span class="sxs-lookup"><span data-stu-id="45cdb-264">Step 4: Create Batch job</span></span>
<span data-ttu-id="45cdb-265">![Creare un processo di Batch][4]</span><span class="sxs-lookup"><span data-stu-id="45cdb-265">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="45cdb-266">Un **processo** di Batch è una raccolta di attività ed è associato a un pool di nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="45cdb-266">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="45cdb-267">attività Hello in un processo eseguito sui nodi di calcolo del pool di hello associata.</span><span class="sxs-lookup"><span data-stu-id="45cdb-267">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="45cdb-268">È possibile utilizzare un processo non solo per l'organizzazione e il rilevamento di attività nei carichi di lavoro correlati, ma anche per l'imposizione di determinati vincoli, ad esempio hello di esecuzione massimo per il processo di hello (e, di conseguenza, le relative attività) e la priorità del processo nei processi tooother relazione in hello account Batch.</span><span class="sxs-lookup"><span data-stu-id="45cdb-268">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) and job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="45cdb-269">In questo esempio, tuttavia, viene associato solo a pool hello creato nel passaggio &#3; processo hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-269">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="45cdb-270">Non vengono configurate proprietà aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="45cdb-270">No additional properties are configured.</span></span>

<span data-ttu-id="45cdb-271">Tutti i processi di Batch sono associati a un pool specifico.</span><span class="sxs-lookup"><span data-stu-id="45cdb-271">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="45cdb-272">Questa associazione indica quali nodi del processo di hello eseguite ai.</span><span class="sxs-lookup"><span data-stu-id="45cdb-272">This association indicates which nodes hello job's tasks execute on.</span></span> <span data-ttu-id="45cdb-273">Per specificare il pool di hello, utilizzare hello [PoolInformation] [ py_poolinfo] proprietà, come illustrato nel frammento di codice hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="45cdb-273">You specify hello pool by using hello [PoolInformation][py_poolinfo] property, as shown in hello code snippet below.</span></span>

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

<span data-ttu-id="45cdb-274">Ora che è stato creato un processo, le attività vengono aggiunti lavoro hello tooperform.</span><span class="sxs-lookup"><span data-stu-id="45cdb-274">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="45cdb-275">Passaggio 5: Aggiungere attività toojob</span><span class="sxs-lookup"><span data-stu-id="45cdb-275">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="45cdb-276">![Aggiungere attività toojob][5]</span><span class="sxs-lookup"><span data-stu-id="45cdb-276">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="45cdb-277">
*(1) processo toohello sono state aggiunte le attività, le attività di hello (2) sono pianificati toorun nei nodi e attività hello (3) scaricare tooprocess i file di dati hello*</span><span class="sxs-lookup"><span data-stu-id="45cdb-277">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="45cdb-278">Batch **attività** sono nodi di calcolo hello singole unità di lavoro che vengono eseguite sullo hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-278">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="45cdb-279">Un'attività dispone di una riga di comando ed esegue gli script hello o file eseguibili specificati in questa riga di comando.</span><span class="sxs-lookup"><span data-stu-id="45cdb-279">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="45cdb-280">tooactually eseguire lavoro, è necessario aggiungere attività tooa processo.</span><span class="sxs-lookup"><span data-stu-id="45cdb-280">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="45cdb-281">Ogni [CloudTask] [ py_task] è configurato con una proprietà della riga di comando e [ResourceFiles] [ py_resource_file] (come StartTask del pool di hello) che hello attività Scarica il nodo toohello prima che la riga di comando viene eseguita automaticamente.</span><span class="sxs-lookup"><span data-stu-id="45cdb-281">Each [CloudTask][py_task] is configured with a command-line property and [ResourceFiles][py_resource_file] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="45cdb-282">Nell'esempio hello, ogni attività vengono elaborati solo un file.</span><span class="sxs-lookup"><span data-stu-id="45cdb-282">In hello sample, each task processes only one file.</span></span> <span data-ttu-id="45cdb-283">Di conseguenza, la rispettiva raccolta ResourceFiles contiene un singolo elemento.</span><span class="sxs-lookup"><span data-stu-id="45cdb-283">Thus, its ResourceFiles collection contains a single element.</span></span>

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
> <span data-ttu-id="45cdb-284">Quando accedono a variabili di ambiente, ad esempio `$AZ_BATCH_NODE_SHARED_DIR` o eseguire un'applicazione non trovata nel nodo di hello `PATH`, righe di comando dell'attività deve richiamare hello shell in modo esplicito, ad esempio con `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span><span class="sxs-lookup"><span data-stu-id="45cdb-284">When they access environment variables such as `$AZ_BATCH_NODE_SHARED_DIR` or execute an application not found in hello node's `PATH`, task command lines must invoke hello shell explicitly, such as with `/bin/sh -c MyTaskApplication $MY_ENV_VAR`.</span></span> <span data-ttu-id="45cdb-285">Questo requisito non è necessario se un'applicazione di esecuzione delle attività nel nodo di hello `PATH` e non fanno riferimento a tutte le variabili di ambiente.</span><span class="sxs-lookup"><span data-stu-id="45cdb-285">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` and do not reference any environment variables.</span></span>
>
>

<span data-ttu-id="45cdb-286">All'interno di hello `for` ciclo nel frammento di codice hello precedente, è possibile vedere che la riga di comando hello per attività hello è costruita con cinque argomenti della riga di comando che vengono passati troppo*python_tutorial_task.py*:</span><span class="sxs-lookup"><span data-stu-id="45cdb-286">Within hello `for` loop in hello code snippet above, you can see that hello command line for hello task is constructed with five command-line arguments that are passed too*python_tutorial_task.py*:</span></span>

1. <span data-ttu-id="45cdb-287">**FilePath**: si tratta di file toohello di hello percorso locale nello stato attuale per il nodo hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-287">**filepath**: This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="45cdb-288">Quando hello oggetto ResourceFile `upload_file_to_container` è stato creato nel passaggio 2, nome del file hello è stato utilizzato per questa proprietà (hello `file_path` parametro nel costruttore ResourceFile hello).</span><span class="sxs-lookup"><span data-stu-id="45cdb-288">When hello ResourceFile object in `upload_file_to_container` was created in Step 2 above, hello file name was used for this property (hello `file_path` parameter in hello ResourceFile constructor).</span></span> <span data-ttu-id="45cdb-289">Ciò indica che file hello è reperibile in hello stesso nodo hello come directory *python_tutorial_task.py*.</span><span class="sxs-lookup"><span data-stu-id="45cdb-289">This indicates that hello file can be found in hello same directory on hello node as *python_tutorial_task.py*.</span></span>
2. <span data-ttu-id="45cdb-290">**NUMWORDS**: inizio hello *N* parole devono essere scritti i file di output toohello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-290">**numwords**: hello top *N* words should be written toohello output file.</span></span>
3. <span data-ttu-id="45cdb-291">**storageaccount**: nome hello di hello account di archiviazione che possiede l'output dell'attività hello toowhich hello contenitore deve essere caricato.</span><span class="sxs-lookup"><span data-stu-id="45cdb-291">**storageaccount**: hello name of hello Storage account that owns hello container toowhich hello task output should be uploaded.</span></span>
4. <span data-ttu-id="45cdb-292">**storagecontainer**: nome hello di hello toowhich di hello archiviazione contenitore output file devono essere caricati.</span><span class="sxs-lookup"><span data-stu-id="45cdb-292">**storagecontainer**: hello name of hello Storage container toowhich hello output files should be uploaded.</span></span>
5. <span data-ttu-id="45cdb-293">**sastoken**: firma di accesso condiviso hello (SAS) che fornisce l'accesso in scrittura toohello **output** contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="45cdb-293">**sastoken**: hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="45cdb-294">Hello *python_tutorial_task.py* script utilizza la firma di accesso condiviso quando si crea il relativo riferimento BlockBlobService.</span><span class="sxs-lookup"><span data-stu-id="45cdb-294">hello *python_tutorial_task.py* script uses this shared access signature when creates its BlockBlobService reference.</span></span> <span data-ttu-id="45cdb-295">Questo fornisce l'accesso in scrittura toohello contenitore senza richiedere una chiave di accesso per account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-295">This provides write access toohello container without requiring an access key for hello storage account.</span></span>

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="45cdb-296">Passaggio 6: Monitorare le attività</span><span class="sxs-lookup"><span data-stu-id="45cdb-296">Step 6: Monitor tasks</span></span>
<span data-ttu-id="45cdb-297">![Monitorare le attività][6]</span><span class="sxs-lookup"><span data-stu-id="45cdb-297">![Monitor tasks][6]</span></span><br/><span data-ttu-id="45cdb-298">
*Hello hello (1) Monitor attività per lo stato di completamento e caricare il risultato dati tooAzure archiviazione attività hello (2)*</span><span class="sxs-lookup"><span data-stu-id="45cdb-298">
*hello script (1) monitors hello tasks for completion status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="45cdb-299">Quando le attività vengono aggiunte tooa processo, vengono automaticamente in coda e pianificate per l'esecuzione nei nodi di calcolo nel pool di hello associata al processo hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-299">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="45cdb-300">In base alle impostazioni di hello specificate, Batch gestisce tutte le attività di accodamento, la pianificazione, nuovo tentativo in corso e altre funzioni di amministrazione di attività per l'utente.</span><span class="sxs-lookup"><span data-stu-id="45cdb-300">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="45cdb-301">Esistono molti approcci toomonitoring l'esecuzione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="45cdb-301">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="45cdb-302">Hello `wait_for_tasks_to_complete` funzionare in *python_tutorial_client.py* fornisce un semplice esempio di attività di monitoraggio per un determinato stato, in questo caso, hello [completato] [ py_taskstate] stato.</span><span class="sxs-lookup"><span data-stu-id="45cdb-302">hello `wait_for_tasks_to_complete` function in *python_tutorial_client.py* provides a simple example of monitoring tasks for a certain state, in this case, hello [completed][py_taskstate] state.</span></span>

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

## <a name="step-7-download-task-output"></a><span data-ttu-id="45cdb-303">Passaggio 7: Scaricare l'output dell'attività</span><span class="sxs-lookup"><span data-stu-id="45cdb-303">Step 7: Download task output</span></span>
<span data-ttu-id="45cdb-304">![Scaricare l'output delle attività dal servizio di archiviazione][7]</span><span class="sxs-lookup"><span data-stu-id="45cdb-304">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="45cdb-305">Hello processo una volta completato, l'output di hello di hello attività può essere scaricato dall'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="45cdb-305">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="45cdb-306">Questa operazione viene eseguita con una chiamata troppo`download_blobs_from_container` in *python_tutorial_client.py*:</span><span class="sxs-lookup"><span data-stu-id="45cdb-306">This is done with a call too`download_blobs_from_container` in *python_tutorial_client.py*:</span></span>

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
> <span data-ttu-id="45cdb-307">Hello chiamata troppo`download_blobs_from_container` in *python_tutorial_client.py* specifica che il file hello devono essere scaricato tooyour home directory.</span><span class="sxs-lookup"><span data-stu-id="45cdb-307">hello call too`download_blobs_from_container` in *python_tutorial_client.py* specifies that hello files should be downloaded tooyour home directory.</span></span> <span data-ttu-id="45cdb-308">Ritiene toomodify disponibile in questo percorso di output.</span><span class="sxs-lookup"><span data-stu-id="45cdb-308">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="45cdb-309">Passaggio 8: Eliminare i contenitori</span><span class="sxs-lookup"><span data-stu-id="45cdb-309">Step 8: Delete containers</span></span>
<span data-ttu-id="45cdb-310">Poiché vengono addebitati i dati che si trovano in archiviazione di Azure, è sempre tooremove una buona idea tutti i blob che non sono più necessari per i processi Batch.</span><span class="sxs-lookup"><span data-stu-id="45cdb-310">Because you are charged for data that resides in Azure Storage, it is always a good idea tooremove any blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="45cdb-311">In *python_tutorial_client.py*, questa operazione viene eseguita con le tre chiamate troppo[BlockBlobService.delete_container][py_delete_container]:</span><span class="sxs-lookup"><span data-stu-id="45cdb-311">In *python_tutorial_client.py*, this is done with three calls too[BlockBlobService.delete_container][py_delete_container]:</span></span>

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="45cdb-312">Passaggio 9: Eliminare il processo di hello e pool hello</span><span class="sxs-lookup"><span data-stu-id="45cdb-312">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="45cdb-313">Nel passaggio finale hello, si è richiesta toodelete hello processo e hello del pool che sono state create da hello *python_tutorial_client.py* script.</span><span class="sxs-lookup"><span data-stu-id="45cdb-313">In hello final step, you are prompted toodelete hello job and hello pool that were created by hello *python_tutorial_client.py* script.</span></span> <span data-ttu-id="45cdb-314">Anche se non vengono addebitati costi per i processi e le attività in sé, *vengono* addebiti costi per i nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="45cdb-314">Although you are not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="45cdb-315">È quindi consigliabile allocare i nodi solo in base alla necessità.</span><span class="sxs-lookup"><span data-stu-id="45cdb-315">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="45cdb-316">L'eliminazione dei pool inutilizzati può fare parte del processo di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="45cdb-316">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="45cdb-317">BatchServiceClient Hello [JobOperations] [ py_job] e [PoolOperations] [ py_pool] dispongono di metodi di eliminazione corrispondente, ovvero chiamato se si conferma l'eliminazione:</span><span class="sxs-lookup"><span data-stu-id="45cdb-317">hello BatchServiceClient's [JobOperations][py_job] and [PoolOperations][py_pool] both have corresponding deletion methods, which are called if you confirm deletion:</span></span>

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> <span data-ttu-id="45cdb-318">Occorre ricordare che vengono effettuati addebiti per le risorse di calcolo e che l'eliminazione di pool inutilizzati consente di ridurre al minimo i costi.</span><span class="sxs-lookup"><span data-stu-id="45cdb-318">Keep in mind that you are charged for compute resources--deleting unused pools will minimize cost.</span></span> <span data-ttu-id="45cdb-319">Inoltre, tenere presente che l'eliminazione di un pool Elimina tutti i nodi di calcolo all'interno di tale pool e che tutti i dati nei nodi hello sarà irreversibili dopo l'eliminazione di pool hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-319">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-sample-script"></a><span data-ttu-id="45cdb-320">Eseguire uno script di esempio hello</span><span class="sxs-lookup"><span data-stu-id="45cdb-320">Run hello sample script</span></span>
<span data-ttu-id="45cdb-321">Quando si esegue hello *python_tutorial_client.py* script dall'esercitazione hello [nell'esempio di codice][github_article_samples], output della console hello è simile toohello seguente.</span><span class="sxs-lookup"><span data-stu-id="45cdb-321">When you run hello *python_tutorial_client.py* script from hello tutorial [code sample][github_article_samples], hello console output is similar toohello following.</span></span> <span data-ttu-id="45cdb-322">Vi sarà una pausa in `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` mentre vengono creati i nodi di calcolo del pool di hello, avviato, e vengono eseguiti i comandi di hello in attività di avvio del pool di hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-322">There is a pause at `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` while hello pool's compute nodes are created, started, and hello commands in hello pool's start task are executed.</span></span> <span data-ttu-id="45cdb-323">Hello utilizzare [portale di Azure] [ azure_portal] toomonitor il pool, nodi di calcolo, processi e attività durante e dopo l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="45cdb-323">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="45cdb-324">Hello utilizzare [portale di Azure] [ azure_portal] o hello [Microsoft Azure Storage Explorer] [ storage_explorer] tooview le risorse di archiviazione hello (contenitori e BLOB) che vengono creati da un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-324">Use hello [Azure portal][azure_portal] or hello [Microsoft Azure Storage Explorer][storage_explorer] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

> [!TIP]
> <span data-ttu-id="45cdb-325">Eseguire hello *python_tutorial_client.py* generare uno script da all'interno di hello `azure-batch-samples/Python/Batch/article_samples` directory.</span><span class="sxs-lookup"><span data-stu-id="45cdb-325">Run hello *python_tutorial_client.py* script from within hello `azure-batch-samples/Python/Batch/article_samples` directory.</span></span> <span data-ttu-id="45cdb-326">Usa un percorso relativo per hello `common.helpers` importazione del modulo, pertanto si potrebbe osservare `ImportError: No module named 'common'` se non viene eseguito uno script di hello all'interno di questa directory.</span><span class="sxs-lookup"><span data-stu-id="45cdb-326">It uses a relative path for hello `common.helpers` module import, so you might see `ImportError: No module named 'common'` if you don't run hello script from within this directory.</span></span>
>
>

<span data-ttu-id="45cdb-327">Tempo di esecuzione tipico è **minuti circa 5-7** quando si esegue l'esempio hello nella configurazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="45cdb-327">Typical execution time is **approximately 5-7 minutes** when you run hello sample in its default configuration.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="45cdb-328">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45cdb-328">Next steps</span></span>
<span data-ttu-id="45cdb-329">È gratuita toomake modifiche troppo*python_tutorial_client.py* e *python_tutorial_task.py* tooexperiment con diversi scenari di calcolo.</span><span class="sxs-lookup"><span data-stu-id="45cdb-329">Feel free toomake changes too*python_tutorial_client.py* and *python_tutorial_task.py* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="45cdb-330">Ad esempio, provare ad aggiungere un ritardo di esecuzione troppo*python_tutorial_task.py* toosimulate lunga le attività e monitorarli nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-330">For example, try adding an execution delay too*python_tutorial_task.py* toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="45cdb-331">Provare aggiungendo più attività o modificando il numero di hello di nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="45cdb-331">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="45cdb-332">Aggiungere logica toocheck per e consentire l'utilizzo di hello di un tempo di esecuzione toospeed pool esistenti.</span><span class="sxs-lookup"><span data-stu-id="45cdb-332">Add logic toocheck for and allow hello use of an existing pool toospeed execution time.</span></span>

<span data-ttu-id="45cdb-333">Ora che si ha familiarità con hello base del flusso di lavoro di una soluzione di Batch, è ora toodig in toohello funzionalità aggiuntive di hello servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="45cdb-333">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="45cdb-334">Hello revisione [funzionalità Panoramica di Azure Batch](batch-api-basics.md) articolo, è consigliabile se si è nuovo servizio toohello.</span><span class="sxs-lookup"><span data-stu-id="45cdb-334">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="45cdb-335">Inizio nel hello altri articoli di sviluppo di Batch in **sviluppo approfondito** in hello [il percorso di apprendimento Batch][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="45cdb-335">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="45cdb-336">Estrarre un'implementazione diversa di elaborazione hello "top N parole" del carico di lavoro con Batch in hello [TopNWords] [ github_topnwords] esempio.</span><span class="sxs-lookup"><span data-stu-id="45cdb-336">Check out a different implementation of processing hello "top N words" workload with Batch in hello [TopNWords][github_topnwords] sample.</span></span>

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
