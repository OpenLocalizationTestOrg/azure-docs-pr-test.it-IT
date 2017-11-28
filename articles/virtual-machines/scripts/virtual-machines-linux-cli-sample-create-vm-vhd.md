---
title: Esempio di script dell'interfaccia della riga di comando di Azure - Creare una macchina virtuale con un disco rigido virtuale | Microsoft Docs
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
ms.openlocfilehash: fab65296a552c1839522c5254a868a3dc96227f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="d38f6-103">Creare una macchina virtuale con un disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="d38f6-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="d38f6-104">In questo esempio viene creata una macchina virtuale usando un disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="d38f6-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="d38f6-105">Vengono prima creati un gruppo di risorse, un account di archiviazione e un contenitore e quindi viene creata una macchina virtuale caricando il disco rigido virtuale nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="d38f6-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading the VHD to the container.</span></span>
<span data-ttu-id="d38f6-106">Viene infine sostituita la chiave pubblica SSH con la chiave pubblica personale per poter accedere alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d38f6-106">It replaces the ssh public key with your public key so that you have access to the VM.</span></span>

<span data-ttu-id="d38f6-107">È necessario un disco rigido virtuale di avvio.</span><span class="sxs-lookup"><span data-stu-id="d38f6-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="d38f6-108">È possibile scaricare il disco rigido virtuale usato nell'esempio da https://azclisamples.blob.core.windows.net/vhds/sample.vhd oppure usare il proprio disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="d38f6-108">You can download the VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="d38f6-109">Lo script cerca `~/sample.vhd`.</span><span class="sxs-lookup"><span data-stu-id="d38f6-109">The script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d38f6-110">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="d38f6-110">Sample script</span></span>

<span data-ttu-id="d38f6-111">[!code-azurecli-interactive[principale](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Creare una macchina virtuale usando un disco rigido virtuale")]</span><span class="sxs-lookup"><span data-stu-id="d38f6-111">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d38f6-112">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="d38f6-112">Clean up deployment</span></span> 

<span data-ttu-id="d38f6-113">Eseguire questo comando per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="d38f6-113">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="d38f6-114">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="d38f6-114">Script explanation</span></span>

<span data-ttu-id="d38f6-115">Questo script usa i comandi seguenti per creare un gruppo di risorse, la macchina virtuale, il set di disponibilità, il bilanciamento del carico e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="d38f6-115">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="d38f6-116">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="d38f6-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d38f6-117">Comando</span><span class="sxs-lookup"><span data-stu-id="d38f6-117">Command</span></span> | <span data-ttu-id="d38f6-118">Note</span><span class="sxs-lookup"><span data-stu-id="d38f6-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d38f6-119">az group create</span><span class="sxs-lookup"><span data-stu-id="d38f6-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d38f6-120">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="d38f6-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d38f6-121">az storage account list</span><span class="sxs-lookup"><span data-stu-id="d38f6-121">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="d38f6-122">Elenca gli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d38f6-122">Lists storage accounts</span></span> |
| [<span data-ttu-id="d38f6-123">az storage account check-name</span><span class="sxs-lookup"><span data-stu-id="d38f6-123">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="d38f6-124">Verifica che un nome di account di archiviazione sia valido e che non esista già</span><span class="sxs-lookup"><span data-stu-id="d38f6-124">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="d38f6-125">az storage account keys list</span><span class="sxs-lookup"><span data-stu-id="d38f6-125">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="d38f6-126">Elenca le chiavi per gli account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d38f6-126">Lists keys for the storage accounts</span></span> |
| [<span data-ttu-id="d38f6-127">az storage blob exists</span><span class="sxs-lookup"><span data-stu-id="d38f6-127">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="d38f6-128">Controlla se il BLOB esiste</span><span class="sxs-lookup"><span data-stu-id="d38f6-128">Checks whether the blob exists</span></span> |
| [<span data-ttu-id="d38f6-129">az storage container create</span><span class="sxs-lookup"><span data-stu-id="d38f6-129">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="d38f6-130">Crea un contenitore in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d38f6-130">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="d38f6-131">az storage blob upload</span><span class="sxs-lookup"><span data-stu-id="d38f6-131">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="d38f6-132">Crea un BLOB nel contenitore caricando il disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="d38f6-132">Creates a blob in the container by uploading the VHD.</span></span> |
| [<span data-ttu-id="d38f6-133">az vm list</span><span class="sxs-lookup"><span data-stu-id="d38f6-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="d38f6-134">Usato con `--query`, controlla se il nome della macchina virtuale è in uso.</span><span class="sxs-lookup"><span data-stu-id="d38f6-134">Used with `--query` check whether the VM name is in use.</span></span> | 
| [<span data-ttu-id="d38f6-135">az vm create</span><span class="sxs-lookup"><span data-stu-id="d38f6-135">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="d38f6-136">Crea le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="d38f6-136">Creates the virtual machines.</span></span> |
| [<span data-ttu-id="d38f6-137">az vm access set-linux-user</span><span class="sxs-lookup"><span data-stu-id="d38f6-137">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="d38f6-138">Reimposta la chiave SSH per consentire all'utente corrente di accedere alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d38f6-138">Resets the SSH key to give the current user access to the VM.</span></span> |
| [<span data-ttu-id="d38f6-139">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="d38f6-139">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="d38f6-140">Ottiene l'indirizzo IP della macchina virtuale creata.</span><span class="sxs-lookup"><span data-stu-id="d38f6-140">Gets the IP address of the VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d38f6-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d38f6-141">Next steps</span></span>

<span data-ttu-id="d38f6-142">Per altre informazioni sull'interfaccia della riga di comando di Azure, vedere la [documentazione sull'interfaccia della riga di comando di Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d38f6-142">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d38f6-143">Altri esempi di script dell'interfaccia della riga di comando della macchina virtuale sono reperibili nella [documentazione della VM Linux di Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d38f6-143">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
