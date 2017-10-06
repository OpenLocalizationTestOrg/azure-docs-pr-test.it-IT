---
title: aaaAzure CLI Script di esempio - riavviare le macchine virtuali | Documenti Microsoft
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
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a><span data-ttu-id="8e98e-103">Riavviare le VM</span><span class="sxs-lookup"><span data-stu-id="8e98e-103">Restart VMs</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="8e98e-104">Questo esempio viene illustrato un paio di modi tooget alcune macchine virtuali e riavviarle.</span><span class="sxs-lookup"><span data-stu-id="8e98e-104">This sample shows a couple of ways tooget some VMs and restart them.</span></span>

<span data-ttu-id="8e98e-105">Hello riavvia innanzitutto tutte le macchine virtuali hello nel gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="8e98e-105">hello first restarts all hello VMs in hello resource group.</span></span>

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

<span data-ttu-id="8e98e-106">secondo ottiene hello Hello tag macchine virtuali con `az resouce list` Filtra le risorse toohello macchine virtuali e riavvia tali macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="8e98e-106">hello second gets hello tagged VMs using `az resouce list` and filters toohello resources that are VMs, and restarts those VMs.</span></span>

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

<span data-ttu-id="8e98e-107">Questo esempio funziona in una shell Bash.</span><span class="sxs-lookup"><span data-stu-id="8e98e-107">This sample works in a Bash shell.</span></span> <span data-ttu-id="8e98e-108">Per opzioni all'esecuzione di script CLI di Azure su client Windows, vedere [in esecuzione hello CLI di Azure in Windows](../windows/cli-options.md).</span><span class="sxs-lookup"><span data-stu-id="8e98e-108">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../windows/cli-options.md).</span></span>


## <a name="sample-script"></a><span data-ttu-id="8e98e-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="8e98e-109">Sample script</span></span>

<span data-ttu-id="8e98e-110">esempio Hello ha tre script.</span><span class="sxs-lookup"><span data-stu-id="8e98e-110">hello sample has three scripts.</span></span>
<span data-ttu-id="8e98e-111">Hello macchine virtuali di un primo disposizioni hello.</span><span class="sxs-lookup"><span data-stu-id="8e98e-111">hello first one provisions hello virtual machines.</span></span>
<span data-ttu-id="8e98e-112">Opzione no-wait hello viene utilizzato in modo comando hello viene restituita senza aspettare in ogni macchina virtuale toobe il provisioning.</span><span class="sxs-lookup"><span data-stu-id="8e98e-112">It uses hello no-wait option so hello command returns without waiting on each VM toobe provisioned.</span></span>
<span data-ttu-id="8e98e-113">Hello secondo rimane in attesa hello macchine virtuali toobe eseguito il provisioning completo.</span><span class="sxs-lookup"><span data-stu-id="8e98e-113">hello second waits for hello VMs toobe fully provisioned.</span></span>
<span data-ttu-id="8e98e-114">script terzo Hello riavvia tutte le macchine virtuali hello che ha effettuato il provisioning e quindi hello solo tag macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="8e98e-114">hello third script restarts all hello VMs that were provisioned, and then just hello tagged VMs.</span></span>

### <a name="provision-hello-vms"></a><span data-ttu-id="8e98e-115">Eseguire il provisioning di hello macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="8e98e-115">Provision hello VMs</span></span>

<span data-ttu-id="8e98e-116">Questo script crea un gruppo di risorse e quindi crea tre toorestart macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="8e98e-116">This script creates a resource group and then it creates three VMs toorestart.</span></span>
<span data-ttu-id="8e98e-117">Due di queste vengono contrassegnate con tag.</span><span class="sxs-lookup"><span data-stu-id="8e98e-117">Two of them are tagged.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a><span data-ttu-id="8e98e-118">Attesa</span><span class="sxs-lookup"><span data-stu-id="8e98e-118">Wait</span></span>

<span data-ttu-id="8e98e-119">Questo script verifica su hello ogni 20 secondi finché non vengono effettuato il provisioning di tutti e tre macchine virtuali, o uno di essi non tooprovision lo stato del provisioning.</span><span class="sxs-lookup"><span data-stu-id="8e98e-119">This script checks on hello provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails tooprovision.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a><span data-ttu-id="8e98e-120">Riavviare le macchine virtuali hello</span><span class="sxs-lookup"><span data-stu-id="8e98e-120">Restart hello VMs</span></span>

<span data-ttu-id="8e98e-121">Questo script viene riavviato hello tutte le macchine virtuali nel gruppo di risorse hello e riavvia solo le macchine virtuali hello tag.</span><span class="sxs-lookup"><span data-stu-id="8e98e-121">This script restarts all hello VMs in hello resource group, and then it restarts just hello tagged VMs.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8e98e-122">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="8e98e-122">Clean up deployment</span></span> 

<span data-ttu-id="8e98e-123">Dopo l'esecuzione di script di esempio hello, hello comando seguente può essere utilizzato tooremove hello gruppi di risorse, le macchine virtuali e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="8e98e-123">After hello script sample has been run, hello following command can be used tooremove hello resource groups, VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a><span data-ttu-id="8e98e-124">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="8e98e-124">Script explanation</span></span>

<span data-ttu-id="8e98e-125">Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, macchina virtuale, set di disponibilità, bilanciamento del carico e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="8e98e-125">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="8e98e-126">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="8e98e-126">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8e98e-127">Comando</span><span class="sxs-lookup"><span data-stu-id="8e98e-127">Command</span></span> | <span data-ttu-id="8e98e-128">Note</span><span class="sxs-lookup"><span data-stu-id="8e98e-128">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8e98e-129">az group create</span><span class="sxs-lookup"><span data-stu-id="8e98e-129">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="8e98e-130">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="8e98e-130">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8e98e-131">az vm create</span><span class="sxs-lookup"><span data-stu-id="8e98e-131">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="8e98e-132">Crea le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="8e98e-132">Creates hello virtual machines.</span></span>  |
| [<span data-ttu-id="8e98e-133">az vm list</span><span class="sxs-lookup"><span data-stu-id="8e98e-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="8e98e-134">Utilizzato con `--query` tooensure hello macchine virtuali viene effettuato il provisioning prima di riavviarli, e quindi tooget hello gli ID di hello toorestart di macchine virtuali di loro.</span><span class="sxs-lookup"><span data-stu-id="8e98e-134">Used with `--query` tooensure hello VMs are provisioned before restarting them, and then tooget hello IDs of hello VMs toorestart them.</span></span> |
| [<span data-ttu-id="8e98e-135">az resource list</span><span class="sxs-lookup"><span data-stu-id="8e98e-135">az resource list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="8e98e-136">Utilizzato con `--query` tooget hello gli ID delle macchine virtuali hello mediante tag hello.</span><span class="sxs-lookup"><span data-stu-id="8e98e-136">Used with `--query` tooget hello IDs of hello VMs using hello tag.</span></span> |
| [<span data-ttu-id="8e98e-137">az vm restart</span><span class="sxs-lookup"><span data-stu-id="8e98e-137">az vm restart</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="8e98e-138">Consente di riavviare le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="8e98e-138">Restarts hello VMs.</span></span> |
| [<span data-ttu-id="8e98e-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="8e98e-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="8e98e-140">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="8e98e-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8e98e-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8e98e-141">Next steps</span></span>

<span data-ttu-id="8e98e-142">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8e98e-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="8e98e-143">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8e98e-143">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
