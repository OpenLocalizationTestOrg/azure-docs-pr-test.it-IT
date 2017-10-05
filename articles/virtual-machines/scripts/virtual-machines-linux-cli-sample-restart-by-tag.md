---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Riavviare macchine virtuali | Microsoft Docs
description: Esempio di script dell'interfaccia della riga di comando di Azure - Riavviare macchine virtuali in base al tag e all'ID
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: 4d0fe95287c91a4b656904f9007ceaaf866e155f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="restart-vms"></a><span data-ttu-id="afd99-103">Riavviare le VM</span><span class="sxs-lookup"><span data-stu-id="afd99-103">Restart VMs</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="afd99-104">Questo esempio illustra un paio di modi per ottenere alcune VM e riavviarle.</span><span class="sxs-lookup"><span data-stu-id="afd99-104">This sample shows a couple of ways to get some VMs and restart them.</span></span>

<span data-ttu-id="afd99-105">Il primo riavvia tutte le VM nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="afd99-105">The first restarts all the VMs in the resource group.</span></span>

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

<span data-ttu-id="afd99-106">Il secondo ottiene le VM con tag tramite `az resouce list` e filtra le risorse che sono VM quindi riavvia queste VM.</span><span class="sxs-lookup"><span data-stu-id="afd99-106">The second gets the tagged VMs using `az resouce list` and filters to the resources that are VMs, and restarts those VMs.</span></span>

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

<span data-ttu-id="afd99-107">Questo esempio funziona in una shell Bash.</span><span class="sxs-lookup"><span data-stu-id="afd99-107">This sample works in a Bash shell.</span></span> <span data-ttu-id="afd99-108">Per le opzioni sull'esecuzione di script dell'interfaccia della riga di comando di Azure nel client Windows, vedere [Running the Azure CLI in Windows](../windows/cli-options.md) (Esecuzione dell'interfaccia della riga di comando di Azure in Windows).</span><span class="sxs-lookup"><span data-stu-id="afd99-108">For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../windows/cli-options.md).</span></span>


## <a name="sample-script"></a><span data-ttu-id="afd99-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="afd99-109">Sample script</span></span>

<span data-ttu-id="afd99-110">L'esempio prevede tre script.</span><span class="sxs-lookup"><span data-stu-id="afd99-110">The sample has three scripts.</span></span>
<span data-ttu-id="afd99-111">Il primo esegue il provisioning delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="afd99-111">The first one provisions the virtual machines.</span></span>
<span data-ttu-id="afd99-112">Usa l'opzione senza attesa in modo che il comando ritorni senza attendere per ogni VM di cui eseguire il provisioning.</span><span class="sxs-lookup"><span data-stu-id="afd99-112">It uses the no-wait option so the command returns without waiting on each VM to be provisioned.</span></span>
<span data-ttu-id="afd99-113">Il secondo attende il provisioning completo delle VM.</span><span class="sxs-lookup"><span data-stu-id="afd99-113">The second waits for the VMs to be fully provisioned.</span></span>
<span data-ttu-id="afd99-114">Il terzo script riavvia tutte le VM di cui è stato eseguito il provisioning e quindi solo le VM con tag.</span><span class="sxs-lookup"><span data-stu-id="afd99-114">The third script restarts all the VMs that were provisioned, and then just the tagged VMs.</span></span>

### <a name="provision-the-vms"></a><span data-ttu-id="afd99-115">Eseguire il provisioning delle VM</span><span class="sxs-lookup"><span data-stu-id="afd99-115">Provision the VMs</span></span>

<span data-ttu-id="afd99-116">Questo script crea un gruppo di risorse e quindi crea tre VM da riavviare.</span><span class="sxs-lookup"><span data-stu-id="afd99-116">This script creates a resource group and then it creates three VMs to restart.</span></span>
<span data-ttu-id="afd99-117">Due di queste vengono contrassegnate con tag.</span><span class="sxs-lookup"><span data-stu-id="afd99-117">Two of them are tagged.</span></span>

<span data-ttu-id="afd99-118">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Eseguire il provisioning delle VM")]</span><span class="sxs-lookup"><span data-stu-id="afd99-118">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision the VMs")]</span></span>

### <a name="wait"></a><span data-ttu-id="afd99-119">Attesa</span><span class="sxs-lookup"><span data-stu-id="afd99-119">Wait</span></span>

<span data-ttu-id="afd99-120">Questo script verifica lo stato del provisioning ogni 20 secondi, fino a quando viene completato il provisioning di tutte e tre le VM oppure il provisioning di una delle VM fallisce.</span><span class="sxs-lookup"><span data-stu-id="afd99-120">This script checks on the provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails to provision.</span></span>

<span data-ttu-id="afd99-121">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Attendere che venga completato il provisioning della VM")]</span><span class="sxs-lookup"><span data-stu-id="afd99-121">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for the VMs to be provisioned")]</span></span>

### <a name="restart-the-vms"></a><span data-ttu-id="afd99-122">Riavviare le VM</span><span class="sxs-lookup"><span data-stu-id="afd99-122">Restart the VMs</span></span>

<span data-ttu-id="afd99-123">Questo script riavvia tutte le VM nel gruppo di risorse e quindi riavvia solo le VM con tag.</span><span class="sxs-lookup"><span data-stu-id="afd99-123">This script restarts all the VMs in the resource group, and then it restarts just the tagged VMs.</span></span>

<span data-ttu-id="afd99-124">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Riavviare le macchine virtuali in base al tag")]</span><span class="sxs-lookup"><span data-stu-id="afd99-124">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="afd99-125">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="afd99-125">Clean up deployment</span></span> 

<span data-ttu-id="afd99-126">Dopo l'esecuzione dello script di esempio, eseguire il comando seguente per rimuovere i gruppi di risorse, le macchine virtuali e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="afd99-126">After the script sample has been run, the following command can be used to remove the resource groups, VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a><span data-ttu-id="afd99-127">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="afd99-127">Script explanation</span></span>

<span data-ttu-id="afd99-128">Questo script usa i comandi seguenti per creare un gruppo di risorse, la macchina virtuale, il set di disponibilità, il bilanciamento del carico e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="afd99-128">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="afd99-129">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="afd99-129">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="afd99-130">Comando</span><span class="sxs-lookup"><span data-stu-id="afd99-130">Command</span></span> | <span data-ttu-id="afd99-131">Note</span><span class="sxs-lookup"><span data-stu-id="afd99-131">Notes</span></span> |
|---|---|
| [<span data-ttu-id="afd99-132">az group create</span><span class="sxs-lookup"><span data-stu-id="afd99-132">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="afd99-133">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="afd99-133">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="afd99-134">az vm create</span><span class="sxs-lookup"><span data-stu-id="afd99-134">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="afd99-135">Crea le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="afd99-135">Creates the virtual machines.</span></span>  |
| [<span data-ttu-id="afd99-136">az vm list</span><span class="sxs-lookup"><span data-stu-id="afd99-136">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="afd99-137">Si usa con `--query` per assicurare che venga eseguito il provisionign delle VM prima del loro riavvio e poi per ottenere gli ID delle VM e riavviarle.</span><span class="sxs-lookup"><span data-stu-id="afd99-137">Used with `--query` to ensure the VMs are provisioned before restarting them, and then to get the IDs of the VMs to restart them.</span></span> |
| [<span data-ttu-id="afd99-138">az resource list</span><span class="sxs-lookup"><span data-stu-id="afd99-138">az resource list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="afd99-139">Si usa con `--query` per ottenere gli ID delle VM con il tag.</span><span class="sxs-lookup"><span data-stu-id="afd99-139">Used with `--query` to get the IDs of the VMs using the tag.</span></span> |
| [<span data-ttu-id="afd99-140">az vm restart</span><span class="sxs-lookup"><span data-stu-id="afd99-140">az vm restart</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="afd99-141">Riavvia le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="afd99-141">Restarts the VMs.</span></span> |
| [<span data-ttu-id="afd99-142">az group delete</span><span class="sxs-lookup"><span data-stu-id="afd99-142">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="afd99-143">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="afd99-143">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="afd99-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="afd99-144">Next steps</span></span>

<span data-ttu-id="afd99-145">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="afd99-145">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="afd99-146">Altri esempi di script dell'interfaccia della riga di comando della macchina virtuale sono reperibili nella [documentazione della VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="afd99-146">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
