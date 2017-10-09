---
title: Esempio di Script CLI - esecuzione di un processo batch aaaAzure | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Eseguire un processo con Batch
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="98bfc-103">Eseguire processi in Azure Batch con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="98bfc-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="98bfc-104">Questo script crea un processo Batch e aggiunge una serie di processi toohello di attività.</span><span class="sxs-lookup"><span data-stu-id="98bfc-104">This script creates a Batch job and adds a series of tasks toohello job.</span></span> <span data-ttu-id="98bfc-105">Viene inoltre illustrato come toomonitor un processo e le relative attività.</span><span class="sxs-lookup"><span data-stu-id="98bfc-105">It also demonstrates how toomonitor a job and its tasks.</span></span> <span data-ttu-id="98bfc-106">Infine, Mostra come tooquery hello servizio Batch in modo efficiente per informazioni sulle attività del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="98bfc-106">Finally, it shows how tooquery hello Batch service efficiently for information about hello job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98bfc-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="98bfc-107">Prerequisites</span></span>

- <span data-ttu-id="98bfc-108">Installazione hello CLI di Azure utilizzando istruzioni hello fornite nella hello [Guida all'installazione di Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), se non è già stato fatto.</span><span class="sxs-lookup"><span data-stu-id="98bfc-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="98bfc-109">Creare un account Batch, se non è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="98bfc-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="98bfc-110">Vedere [creare un account Batch con hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) per uno script di esempio che crea un account.</span><span class="sxs-lookup"><span data-stu-id="98bfc-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="98bfc-111">Se non è ancora fatto, configurare un'applicazione toorun da un'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="98bfc-111">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="98bfc-112">Vedere [aggiunta applicazioni tooAzure Batch con Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) per uno script di esempio che crea un'applicazione e carica un tooAzure pacchetto di applicazione.</span><span class="sxs-lookup"><span data-stu-id="98bfc-112">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>
- <span data-ttu-id="98bfc-113">Configurare un pool in cui hello processo verrà eseguito.</span><span class="sxs-lookup"><span data-stu-id="98bfc-113">Configure a pool on which hello job will run.</span></span> <span data-ttu-id="98bfc-114">Vedere [Gestione dei pool di Azure Batch con l'interfaccia della riga di comando di Azure](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) per uno script di esempio che crea un pool con una configurazione del servizio cloud o della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="98bfc-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="98bfc-115">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="98bfc-115">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a><span data-ttu-id="98bfc-116">Pulire un processo</span><span class="sxs-lookup"><span data-stu-id="98bfc-116">Clean up job</span></span>

<span data-ttu-id="98bfc-117">Dopo aver eseguito hello di sopra di script di esempio, eseguire hello tooremove comando seguendo il processo e tutte le attività.</span><span class="sxs-lookup"><span data-stu-id="98bfc-117">After you run hello above sample script, run hello following command tooremove the job and all of its tasks.</span></span> <span data-ttu-id="98bfc-118">Si noti che il pool di hello sarà necessario toobe eliminata separatamente.</span><span class="sxs-lookup"><span data-stu-id="98bfc-118">Note that hello pool will need toobe deleted separately.</span></span> <span data-ttu-id="98bfc-119">Vedere [Gestione dei pool di Azure Batch con l'interfaccia della riga di comando di Azure](./batch-cli-sample-manage-pool.md) per altre informazioni sulla creazione e l'eliminazione di pool.</span><span class="sxs-lookup"><span data-stu-id="98bfc-119">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="98bfc-120">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="98bfc-120">Script explanation</span></span>

<span data-ttu-id="98bfc-121">Questo script utilizza hello toocreate i comandi seguenti, attività e un processo Batch.</span><span class="sxs-lookup"><span data-stu-id="98bfc-121">This script uses hello following commands toocreate a Batch job and tasks.</span></span> <span data-ttu-id="98bfc-122">Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.</span><span class="sxs-lookup"><span data-stu-id="98bfc-122">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="98bfc-123">Comando</span><span class="sxs-lookup"><span data-stu-id="98bfc-123">Command</span></span> | <span data-ttu-id="98bfc-124">Note</span><span class="sxs-lookup"><span data-stu-id="98bfc-124">Notes</span></span> |
|---|---|
| [<span data-ttu-id="98bfc-125">az batch account login</span><span class="sxs-lookup"><span data-stu-id="98bfc-125">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="98bfc-126">Eseguire l'autenticazione con un account Batch.</span><span class="sxs-lookup"><span data-stu-id="98bfc-126">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="98bfc-127">az batch job create</span><span class="sxs-lookup"><span data-stu-id="98bfc-127">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="98bfc-128">Crea un processo Batch.</span><span class="sxs-lookup"><span data-stu-id="98bfc-128">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="98bfc-129">az batch job set</span><span class="sxs-lookup"><span data-stu-id="98bfc-129">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="98bfc-130">Aggiorna le proprietà di un processo Batch.</span><span class="sxs-lookup"><span data-stu-id="98bfc-130">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="98bfc-131">az batch job show</span><span class="sxs-lookup"><span data-stu-id="98bfc-131">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="98bfc-132">Recupera i dettagli di un processo Batch specificato.</span><span class="sxs-lookup"><span data-stu-id="98bfc-132">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="98bfc-133">az batch task create</span><span class="sxs-lookup"><span data-stu-id="98bfc-133">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="98bfc-134">Aggiunge che un toohello di attività specificato processo Batch.</span><span class="sxs-lookup"><span data-stu-id="98bfc-134">Adds a task toohello specified Batch job.</span></span>  |
| [<span data-ttu-id="98bfc-135">az batch task show</span><span class="sxs-lookup"><span data-stu-id="98bfc-135">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="98bfc-136">Recupera i dettagli di hello di un'attività da hello specificato processo Batch.</span><span class="sxs-lookup"><span data-stu-id="98bfc-136">Retrieves hello details of a task from hello specified Batch job.</span></span>  |
| [<span data-ttu-id="98bfc-137">az batch task list</span><span class="sxs-lookup"><span data-stu-id="98bfc-137">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="98bfc-138">Vengono elencate le attività di hello associate al processo specificato hello.</span><span class="sxs-lookup"><span data-stu-id="98bfc-138">Lists hello tasks associated with hello specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="98bfc-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="98bfc-139">Next steps</span></span>

<span data-ttu-id="98bfc-140">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="98bfc-140">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="98bfc-141">Ulteriori esempi di script Batch CLI sono reperibile in hello [documentazione CLI di Azure Batch](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="98bfc-141">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
