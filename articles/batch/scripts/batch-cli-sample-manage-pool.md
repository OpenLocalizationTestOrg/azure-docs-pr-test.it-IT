---
title: aaaAzure CLI Script di esempio - Gestione pool in Batch | Documenti Microsoft
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
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="7d6d6-103">Gestione dei pool di Azure Batch con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="7d6d6-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="7d6d6-104">Questi script vengono illustrate alcune delle strumenti hello disponibili in hello Azure CLI toocreate e gestire pool di nodi di calcolo nel servizio Azure Batch hello.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-104">These script demonstrates some of hello tools available in hello Azure CLI toocreate and manage pools of compute nodes in hello Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="7d6d6-105">i comandi di Hello in questo esempio creano macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-105">hello commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="7d6d6-106">Macchine virtuali in esecuzione trarrà account tooyour addebiti.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-106">Running VMs will accrue charges tooyour account.</span></span> <span data-ttu-id="7d6d6-107">toominimize questi addebiti, eliminare le macchine virtuali hello dopo averli: esempio hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-107">toominimize these charges, delete hello VMs once you're done running hello sample.</span></span> <span data-ttu-id="7d6d6-108">Vedere [Eseguire la pulizia dei pool](#clean-up-pools).</span><span class="sxs-lookup"><span data-stu-id="7d6d6-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="7d6d6-109">È possibile configurare i pool di Batch in due modi: con una configurazione Servizi cloud (solo Windows) o con una configurazoine Macchina virtuale (Windows e Linux).</span><span class="sxs-lookup"><span data-stu-id="7d6d6-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="7d6d6-110">script di esempio Hello seguenti mostrano come toocreate pool con entrambe le configurazioni.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-110">hello sample scripts below show how toocreate pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d6d6-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7d6d6-111">Prerequisites</span></span>

- <span data-ttu-id="7d6d6-112">Installazione hello CLI di Azure utilizzando istruzioni hello fornite nella hello [Guida all'installazione di Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), se non è già stato fatto.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-112">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="7d6d6-113">Creare un account Batch, se non è già disponibile.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="7d6d6-114">Vedere [creare un account Batch con hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) per uno script di esempio che crea un account.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-114">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="7d6d6-115">Se non è ancora fatto, configurare un'applicazione toorun da un'attività di avvio.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-115">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="7d6d6-116">Vedere [aggiunta applicazioni tooAzure Batch con Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) per uno script di esempio che crea un'applicazione e carica un tooAzure pacchetto di applicazione.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-116">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="7d6d6-117">Script di esempio per un pool con configurazione Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="7d6d6-117">Pool with cloud service configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="7d6d6-118">Script di esempio per un pool con configurazione Macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="7d6d6-118">Pool with virtual machine configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a><span data-ttu-id="7d6d6-119">Eseguire la pulizia dei pool</span><span class="sxs-lookup"><span data-stu-id="7d6d6-119">Clean up pools</span></span>

<span data-ttu-id="7d6d6-120">Dopo aver eseguito hello di sopra di script di esempio, eseguire hello seguente pool hello toodelete di comando.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-120">After you run hello above sample script, run hello following command toodelete hello pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="7d6d6-121">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="7d6d6-121">Script explanation</span></span>

<span data-ttu-id="7d6d6-122">Questo script utilizza i seguenti comandi toocreate hello e modificare i pool di Batch.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-122">This script uses hello following commands toocreate and manipulate Batch pools.</span></span>
<span data-ttu-id="7d6d6-123">Ogni comando nella documentazione di hello tabella collegamenti toocommand specifica.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-123">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="7d6d6-124">Comando</span><span class="sxs-lookup"><span data-stu-id="7d6d6-124">Command</span></span> | <span data-ttu-id="7d6d6-125">Note</span><span class="sxs-lookup"><span data-stu-id="7d6d6-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7d6d6-126">az batch account login</span><span class="sxs-lookup"><span data-stu-id="7d6d6-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="7d6d6-127">Eseguire l'autenticazione con un account Batch.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="7d6d6-128">az batch application summary list</span><span class="sxs-lookup"><span data-stu-id="7d6d6-128">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="7d6d6-129">Elencare le applicazioni disponibili hello in hello account Batch.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-129">List hello available applications in hello Batch account.</span></span>  |
| [<span data-ttu-id="7d6d6-130">az batch pool create</span><span class="sxs-lookup"><span data-stu-id="7d6d6-130">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="7d6d6-131">Creare un pool di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-131">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="7d6d6-132">az batch pool set</span><span class="sxs-lookup"><span data-stu-id="7d6d6-132">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="7d6d6-133">Aggiornare le proprietà di un pool.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-133">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="7d6d6-134">az batch pool node-agent-skus list</span><span class="sxs-lookup"><span data-stu-id="7d6d6-134">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="7d6d6-135">Elencare gli SKU agente nodo disponibili e le informazioni dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-135">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="7d6d6-136">az batch pool resize</span><span class="sxs-lookup"><span data-stu-id="7d6d6-136">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="7d6d6-137">Numero di hello di ridimensionamento di macchine virtuali in esecuzione in hello specificato pool.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-137">Resize hello number of running VMs in hello specified pool.</span></span>  |
| [<span data-ttu-id="7d6d6-138">az batch pool show</span><span class="sxs-lookup"><span data-stu-id="7d6d6-138">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="7d6d6-139">Visualizzare le proprietà di hello di un pool.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-139">Display hello properties of a pool.</span></span>  |
| [<span data-ttu-id="7d6d6-140">az batch pool delete</span><span class="sxs-lookup"><span data-stu-id="7d6d6-140">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="7d6d6-141">Eliminare hello specificato pool.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-141">Delete hello specified pool.</span></span>  |
| [<span data-ttu-id="7d6d6-142">az batch pool autoscale enable</span><span class="sxs-lookup"><span data-stu-id="7d6d6-142">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="7d6d6-143">Abilitare la scalabilità automatica in un pool e applicare una formula.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-143">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="7d6d6-144">az batch pool autoscale disable</span><span class="sxs-lookup"><span data-stu-id="7d6d6-144">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="7d6d6-145">Disabilitare la scalabilità automatica in un pool.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-145">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="7d6d6-146">az batch node list</span><span class="sxs-lookup"><span data-stu-id="7d6d6-146">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="7d6d6-147">Elencare tutti il nodo di calcolo hello in hello specificato pool.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-147">List all hello compute node in hello specified pool.</span></span>  |
| [<span data-ttu-id="7d6d6-148">az batch node reboot</span><span class="sxs-lookup"><span data-stu-id="7d6d6-148">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="7d6d6-149">Riavviare il nodo di calcolo specificata di hello.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-149">Reboot hello specified compute node.</span></span>  |
| [<span data-ttu-id="7d6d6-150">az batch node delete</span><span class="sxs-lookup"><span data-stu-id="7d6d6-150">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="7d6d6-151">I nodi di hello elencato Delete da hello specificati pool.</span><span class="sxs-lookup"><span data-stu-id="7d6d6-151">Delete hello listed nodes from hello specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="7d6d6-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7d6d6-152">Next steps</span></span>

<span data-ttu-id="7d6d6-153">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7d6d6-153">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7d6d6-154">Ulteriori esempi di script Batch CLI sono reperibile in hello [documentazione CLI di Azure Batch](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7d6d6-154">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

