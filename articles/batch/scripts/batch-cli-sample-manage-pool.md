---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Gestione dei pool in Batch | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Gestione dei pool in Batch
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
ms.openlocfilehash: 2556b02459886390b803407c5cb828687229a44e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="06eb8-103">Gestione dei pool di Azure Batch con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="06eb8-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="06eb8-104">Questi script illustrano alcuni degli strumenti disponibili nell'interfaccia della riga di comando di Azure per creare e gestire pool di nodi di calcolo nel servizio Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="06eb8-104">These script demonstrates some of the tools available in the Azure CLI to create and manage pools of compute nodes in the Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="06eb8-105">I comandi in questo esempio creano macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="06eb8-105">The commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="06eb8-106">L'esecuzione di macchine virtuali comporterà addebiti all'account.</span><span class="sxs-lookup"><span data-stu-id="06eb8-106">Running VMs will accrue charges to your account.</span></span> <span data-ttu-id="06eb8-107">Per ridurre al minimo tali addebiti, eliminare le macchine virtuali dopo aver eseguito l'esempio.</span><span class="sxs-lookup"><span data-stu-id="06eb8-107">To minimize these charges, delete the VMs once you're done running the sample.</span></span> <span data-ttu-id="06eb8-108">Vedere [Eseguire la pulizia dei pool](#clean-up-pools).</span><span class="sxs-lookup"><span data-stu-id="06eb8-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="06eb8-109">È possibile configurare i pool di Batch in due modi: con una configurazione Servizi cloud (solo Windows) o con una configurazoine Macchina virtuale (Windows e Linux).</span><span class="sxs-lookup"><span data-stu-id="06eb8-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="06eb8-110">Gli script di esempio seguenti mostrano come creare pool con entrambe le configurazioni.</span><span class="sxs-lookup"><span data-stu-id="06eb8-110">The sample scripts below show how to create pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06eb8-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="06eb8-111">Prerequisites</span></span>

- <span data-ttu-id="06eb8-112">Installare l'interfaccia della riga di comando di Azure usando le istruzioni presenti nella [Guida all'installazione dell'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), se questa operazione non è stata ancora eseguita.</span><span class="sxs-lookup"><span data-stu-id="06eb8-112">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="06eb8-113">Creare un account Batch, se non è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="06eb8-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="06eb8-114">Vedere [Creare un account Batch con l'interfaccia della riga di comando di Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) per uno script di esempio che crea un account.</span><span class="sxs-lookup"><span data-stu-id="06eb8-114">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="06eb8-115">Se questa operazione non è stata già eseguita, configurare un'applicazione in modo che venga eseguita da un'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="06eb8-115">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="06eb8-116">Vedere [Aggiunta di applicazioni ad Azure Batch con l'interfaccia della riga di comando di Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) per uno script di esempio che crea un'applicazione e carica un pacchetto dell'applicazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="06eb8-116">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="06eb8-117">Script di esempio per un pool con configurazione Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="06eb8-117">Pool with cloud service configuration sample script</span></span>

<span data-ttu-id="06eb8-118">[!code-azurecli[principale](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Gestire pool con Servizi cloud")]</span><span class="sxs-lookup"><span data-stu-id="06eb8-118">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]</span></span>

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="06eb8-119">Script di esempio per un pool con configurazione Macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="06eb8-119">Pool with virtual machine configuration sample script</span></span>

<span data-ttu-id="06eb8-120">[!code-azurecli[principale](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Gestire pool con Macchina virtuale")]</span><span class="sxs-lookup"><span data-stu-id="06eb8-120">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]</span></span>

## <a name="clean-up-pools"></a><span data-ttu-id="06eb8-121">Eseguire la pulizia dei pool</span><span class="sxs-lookup"><span data-stu-id="06eb8-121">Clean up pools</span></span>

<span data-ttu-id="06eb8-122">Dopo aver eseguito lo script di esempio precedente, eseguire il comando seguente per eliminare i pool.</span><span class="sxs-lookup"><span data-stu-id="06eb8-122">After you run the above sample script, run the following command to delete the pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="06eb8-123">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="06eb8-123">Script explanation</span></span>

<span data-ttu-id="06eb8-124">Questo script usa i comandi seguenti per creare e manipolare pool Batch.</span><span class="sxs-lookup"><span data-stu-id="06eb8-124">This script uses the following commands to create and manipulate Batch pools.</span></span>
<span data-ttu-id="06eb8-125">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="06eb8-125">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="06eb8-126">Comando</span><span class="sxs-lookup"><span data-stu-id="06eb8-126">Command</span></span> | <span data-ttu-id="06eb8-127">Note</span><span class="sxs-lookup"><span data-stu-id="06eb8-127">Notes</span></span> |
|---|---|
| [<span data-ttu-id="06eb8-128">az batch account login</span><span class="sxs-lookup"><span data-stu-id="06eb8-128">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="06eb8-129">Eseguire l'autenticazione con un account Batch.</span><span class="sxs-lookup"><span data-stu-id="06eb8-129">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="06eb8-130">az batch application summary list</span><span class="sxs-lookup"><span data-stu-id="06eb8-130">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="06eb8-131">Elencare le applicazioni disponibili nell'account Batch.</span><span class="sxs-lookup"><span data-stu-id="06eb8-131">List the available applications in the Batch account.</span></span>  |
| [<span data-ttu-id="06eb8-132">az batch pool create</span><span class="sxs-lookup"><span data-stu-id="06eb8-132">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="06eb8-133">Creare un pool di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="06eb8-133">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="06eb8-134">az batch pool set</span><span class="sxs-lookup"><span data-stu-id="06eb8-134">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="06eb8-135">Aggiornare le proprietà di un pool.</span><span class="sxs-lookup"><span data-stu-id="06eb8-135">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="06eb8-136">az batch pool node-agent-skus list</span><span class="sxs-lookup"><span data-stu-id="06eb8-136">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="06eb8-137">Elencare gli SKU agente nodo disponibili e le informazioni dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="06eb8-137">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="06eb8-138">az batch pool resize</span><span class="sxs-lookup"><span data-stu-id="06eb8-138">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="06eb8-139">Ridimensionare il numero di macchine virtuali in esecuzione nel pool specificato.</span><span class="sxs-lookup"><span data-stu-id="06eb8-139">Resize the number of running VMs in the specified pool.</span></span>  |
| [<span data-ttu-id="06eb8-140">az batch pool show</span><span class="sxs-lookup"><span data-stu-id="06eb8-140">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="06eb8-141">Visualizzare le proprietà di un pool.</span><span class="sxs-lookup"><span data-stu-id="06eb8-141">Display the properties of a pool.</span></span>  |
| [<span data-ttu-id="06eb8-142">az batch pool delete</span><span class="sxs-lookup"><span data-stu-id="06eb8-142">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="06eb8-143">Eliminare il pool specificato.</span><span class="sxs-lookup"><span data-stu-id="06eb8-143">Delete the specified pool.</span></span>  |
| [<span data-ttu-id="06eb8-144">az batch pool autoscale enable</span><span class="sxs-lookup"><span data-stu-id="06eb8-144">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="06eb8-145">Abilitare la scalabilità automatica in un pool e applicare una formula.</span><span class="sxs-lookup"><span data-stu-id="06eb8-145">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="06eb8-146">az batch pool autoscale disable</span><span class="sxs-lookup"><span data-stu-id="06eb8-146">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="06eb8-147">Disabilitare la scalabilità automatica in un pool.</span><span class="sxs-lookup"><span data-stu-id="06eb8-147">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="06eb8-148">az batch node list</span><span class="sxs-lookup"><span data-stu-id="06eb8-148">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="06eb8-149">Elencare tutti i nodi di calcolo nel pool specificato.</span><span class="sxs-lookup"><span data-stu-id="06eb8-149">List all the compute node in the specified pool.</span></span>  |
| [<span data-ttu-id="06eb8-150">az batch node reboot</span><span class="sxs-lookup"><span data-stu-id="06eb8-150">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="06eb8-151">Riavviare il nodo di calcolo specificato.</span><span class="sxs-lookup"><span data-stu-id="06eb8-151">Reboot the specified compute node.</span></span>  |
| [<span data-ttu-id="06eb8-152">az batch node delete</span><span class="sxs-lookup"><span data-stu-id="06eb8-152">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="06eb8-153">Eliminare i nodi elencati dal pool specificato.</span><span class="sxs-lookup"><span data-stu-id="06eb8-153">Delete the listed nodes from the specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="06eb8-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="06eb8-154">Next steps</span></span>

<span data-ttu-id="06eb8-155">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="06eb8-155">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="06eb8-156">Altri esempi di script dell'interfaccia della riga di comando di Batch sono disponibili nella [documentazione dell'interfaccia della riga di comando di Azure Batch](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="06eb8-156">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

