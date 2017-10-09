---
title: aaaAzure CLI Script di esempio - creare una macchina virtuale con un disco rigido virtuale | Documenti Microsoft
description: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una macchina virtuale Linux usando un disco rigido virtuale.
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
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="6df46-103">Creare una macchina virtuale con un disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="6df46-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="6df46-104">In questo esempio viene creata una macchina virtuale usando un disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="6df46-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="6df46-105">Crea un gruppo di risorse, un account di archiviazione e un contenitore, quindi crea una macchina virtuale caricando contenitore toohello di hello disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="6df46-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading hello VHD toohello container.</span></span>
<span data-ttu-id="6df46-106">Sostituisce hello ssh pubblica della chiave con la chiave pubblica in modo da disporre di accesso toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6df46-106">It replaces hello ssh public key with your public key so that you have access toohello VM.</span></span>

<span data-ttu-id="6df46-107">È necessario un disco rigido virtuale di avvio.</span><span class="sxs-lookup"><span data-stu-id="6df46-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="6df46-108">È possibile scaricare hello disco rigido virtuale che è stato usato da https://azclisamples.blob.core.windows.net/vhds/sample.vhd o utilizzare un disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="6df46-108">You can download hello VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="6df46-109">Cerca script Hello `~/sample.vhd`.</span><span class="sxs-lookup"><span data-stu-id="6df46-109">hello script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6df46-110">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="6df46-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6df46-111">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="6df46-111">Clean up deployment</span></span> 

<span data-ttu-id="6df46-112">Comando che segue hello esecuzione gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="6df46-112">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="6df46-113">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="6df46-113">Script explanation</span></span>

<span data-ttu-id="6df46-114">Questo script utilizza hello seguenti comandi toocreate un gruppo di risorse, macchina virtuale, set di disponibilità, bilanciamento del carico e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="6df46-114">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="6df46-115">Ogni comando in documentazione specifica toocommand hello tabella collegamenti.</span><span class="sxs-lookup"><span data-stu-id="6df46-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6df46-116">Comando</span><span class="sxs-lookup"><span data-stu-id="6df46-116">Command</span></span> | <span data-ttu-id="6df46-117">Note</span><span class="sxs-lookup"><span data-stu-id="6df46-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6df46-118">az group create</span><span class="sxs-lookup"><span data-stu-id="6df46-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6df46-119">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="6df46-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6df46-120">az storage account list</span><span class="sxs-lookup"><span data-stu-id="6df46-120">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="6df46-121">Elenca gli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="6df46-121">Lists storage accounts</span></span> |
| [<span data-ttu-id="6df46-122">az storage account check-name</span><span class="sxs-lookup"><span data-stu-id="6df46-122">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="6df46-123">Verifica che un nome di account di archiviazione sia valido e che non esista già</span><span class="sxs-lookup"><span data-stu-id="6df46-123">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="6df46-124">az storage account keys list</span><span class="sxs-lookup"><span data-stu-id="6df46-124">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="6df46-125">Elenca le chiavi per gli account di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="6df46-125">Lists keys for hello storage accounts</span></span> |
| [<span data-ttu-id="6df46-126">az storage blob exists</span><span class="sxs-lookup"><span data-stu-id="6df46-126">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="6df46-127">Verifica l'esistenza di blob hello</span><span class="sxs-lookup"><span data-stu-id="6df46-127">Checks whether hello blob exists</span></span> |
| [<span data-ttu-id="6df46-128">az storage container create</span><span class="sxs-lookup"><span data-stu-id="6df46-128">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="6df46-129">Crea un contenitore in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6df46-129">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="6df46-130">az storage blob upload</span><span class="sxs-lookup"><span data-stu-id="6df46-130">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="6df46-131">Crea un blob nel contenitore hello hello il caricamento del disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="6df46-131">Creates a blob in hello container by uploading hello VHD.</span></span> |
| [<span data-ttu-id="6df46-132">az vm list</span><span class="sxs-lookup"><span data-stu-id="6df46-132">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="6df46-133">Utilizzato con `--query` controllare se il nome di macchina virtuale hello è in uso.</span><span class="sxs-lookup"><span data-stu-id="6df46-133">Used with `--query` check whether hello VM name is in use.</span></span> | 
| [<span data-ttu-id="6df46-134">az vm create</span><span class="sxs-lookup"><span data-stu-id="6df46-134">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="6df46-135">Crea le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="6df46-135">Creates hello virtual machines.</span></span> |
| [<span data-ttu-id="6df46-136">az vm access set-linux-user</span><span class="sxs-lookup"><span data-stu-id="6df46-136">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="6df46-137">Reimposta hello SSH toogive chiave hello corrente utente accesso toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6df46-137">Resets hello SSH key toogive hello current user access toohello VM.</span></span> |
| [<span data-ttu-id="6df46-138">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="6df46-138">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="6df46-139">Ottiene l'indirizzo IP hello di hello macchina virtuale che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="6df46-139">Gets hello IP address of hello VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6df46-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6df46-140">Next steps</span></span>

<span data-ttu-id="6df46-141">Per ulteriori informazioni su hello CLI di Azure, vedere [documentazione CLI di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6df46-141">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6df46-142">Esempi di script di macchina virtuale aggiuntiva CLI sono reperibile in hello [documentazione VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6df46-142">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
