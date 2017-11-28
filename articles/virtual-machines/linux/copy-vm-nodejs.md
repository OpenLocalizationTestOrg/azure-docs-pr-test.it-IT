---
title: Creare una copia della macchina virtuale Linux con l'interfaccia della riga di comando di Azure 1.0 | Documentazione Microsoft
description: Informazioni su come creare una copia della macchina virtuale Linux di Azure con l'interfaccia della riga di comando di Azure 1.0 nel modello di distribuzione Resource Manager
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 62ae54f3596c9383cbf3b401fcfdb42ecfdee63c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-the-azure-cli-10"></a><span data-ttu-id="cabed-103">Creare la copia di una macchina virtuale Linux eseguita in Azure con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="cabed-103">Create a copy of a Linux virtual machine running on Azure with the Azure CLI 1.0</span></span>
<span data-ttu-id="cabed-104">Questo articolo descrive come creare una copia di una macchina virtuale (VM) di Azure che esegue Linux nel modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cabed-104">This article shows you how to create a copy of your Azure virtual machine (VM) running Linux using the Resource Manager deployment model.</span></span> <span data-ttu-id="cabed-105">Per prima cosa si esegue la copia dei dischi dati e del sistema operativo in un nuovo contenitore, quindi si configurano le risorse di rete e si crea la nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="cabed-105">First you copy over the operating system and data disks to a new container, then set up the network resources and create the new virtual machine.</span></span>

<span data-ttu-id="cabed-106">È anche possibile [caricare e creare una VM da un'immagine disco personalizzata](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cabed-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="cabed-107">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="cabed-107">CLI versions to complete the task</span></span>
<span data-ttu-id="cabed-108">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="cabed-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="cabed-109">Interfaccia della riga di comando di Azure 1.0: interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="cabed-109">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="cabed-110">[Interfaccia della riga di comando di Azure 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="cabed-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cabed-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="cabed-111">Before you begin</span></span>
<span data-ttu-id="cabed-112">Accertarsi che prima di iniziare la procedura siano soddisfatti i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="cabed-112">Ensure that you meet the following prerequisites before you start the steps:</span></span>

* <span data-ttu-id="cabed-113">Nel computer è stata scaricata e installata l' [interfaccia della riga di comando di Azure](../../cli-install-nodejs.md) .</span><span class="sxs-lookup"><span data-stu-id="cabed-113">You have the [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="cabed-114">Sono anche necessarie alcune informazioni sulla VM Linux di Azure esistente:</span><span class="sxs-lookup"><span data-stu-id="cabed-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="cabed-115">Informazioni sulla VM di origine</span><span class="sxs-lookup"><span data-stu-id="cabed-115">Source VM information</span></span> | <span data-ttu-id="cabed-116">Informazioni sulla collocazione</span><span class="sxs-lookup"><span data-stu-id="cabed-116">Where to get it</span></span> |
| --- | --- |
| <span data-ttu-id="cabed-117">Nome della VM</span><span class="sxs-lookup"><span data-stu-id="cabed-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="cabed-118">Nome del gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="cabed-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="cabed-119">Location</span><span class="sxs-lookup"><span data-stu-id="cabed-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="cabed-120">Nome dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="cabed-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="cabed-121">Nome del contenitore</span><span class="sxs-lookup"><span data-stu-id="cabed-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="cabed-122">Nome del file VHD della VM di origine</span><span class="sxs-lookup"><span data-stu-id="cabed-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="cabed-123">Sarà necessario scegliere alcune informazioni sulla nuova VM:    </span><span class="sxs-lookup"><span data-stu-id="cabed-123">You will need to make some choices about your new VM:    </span></span><br> <span data-ttu-id="cabed-124">-Nome contenitore    </span><span class="sxs-lookup"><span data-stu-id="cabed-124">-Container name    </span></span><br> <span data-ttu-id="cabed-125">-Nome della VM    </span><span class="sxs-lookup"><span data-stu-id="cabed-125">-VM name    </span></span><br> <span data-ttu-id="cabed-126">-Dimensioni della VM    </span><span class="sxs-lookup"><span data-stu-id="cabed-126">-VM size    </span></span><br> <span data-ttu-id="cabed-127">-Nome della vNet    </span><span class="sxs-lookup"><span data-stu-id="cabed-127">-vNet name    </span></span><br> <span data-ttu-id="cabed-128">-Nome della SubNet    </span><span class="sxs-lookup"><span data-stu-id="cabed-128">-SubNet name    </span></span><br> <span data-ttu-id="cabed-129">-Nome dell'IP    </span><span class="sxs-lookup"><span data-stu-id="cabed-129">-IP Name    </span></span><br> <span data-ttu-id="cabed-130">-Nome NIC</span><span class="sxs-lookup"><span data-stu-id="cabed-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="cabed-131">Effettuare l'accesso e impostare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="cabed-131">Login and set your subscription</span></span>
1. <span data-ttu-id="cabed-132">Effettuare l'accesso all'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="cabed-132">Login to the CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="cabed-133">Verificare di essere in modalità Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cabed-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="cabed-134">Impostare la sottoscrizione corretta.</span><span class="sxs-lookup"><span data-stu-id="cabed-134">Set the correct subscription.</span></span> <span data-ttu-id="cabed-135">Per un elenco di tutte le sottoscrizioni, consultare l'elenco degli account Azure.</span><span class="sxs-lookup"><span data-stu-id="cabed-135">You can use 'azure account list' to see all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-the-vm"></a><span data-ttu-id="cabed-136">Arrestare la VM</span><span class="sxs-lookup"><span data-stu-id="cabed-136">Stop the VM</span></span>
<span data-ttu-id="cabed-137">Arrestare e deallocare la VM di origine.</span><span class="sxs-lookup"><span data-stu-id="cabed-137">Stop and deallocate the source VM.</span></span> <span data-ttu-id="cabed-138">Per un elenco di tutte le VM presenti nella sottoscrizione e dei nomi dei relativi gruppi di risorse, consultare l'elenco delle VM Azure.</span><span class="sxs-lookup"><span data-stu-id="cabed-138">You can use 'azure vm list' to get a list of all of the VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-the-vhd"></a><span data-ttu-id="cabed-139">Copiare il file VHD</span><span class="sxs-lookup"><span data-stu-id="cabed-139">Copy the VHD</span></span>
<span data-ttu-id="cabed-140">Per copiare il file VHD dall'archiviazione di origine a quella di destinazione, è possibile usare `azure storage blob copy start`.</span><span class="sxs-lookup"><span data-stu-id="cabed-140">You can copy the VHD from the source storage to the destination using the `azure storage blob copy start`.</span></span> <span data-ttu-id="cabed-141">In questo esempio il file VHD viene copiato nello stesso account di archiviazione, ma in un contenitore diverso.</span><span class="sxs-lookup"><span data-stu-id="cabed-141">In this example, we are going to copy the VHD to the same storage account, but a different container.</span></span>

<span data-ttu-id="cabed-142">Per copiare il file VHD in un altro contenitore dello stesso account di archiviazione, digitare:</span><span class="sxs-lookup"><span data-stu-id="cabed-142">To copy the VHD to another container in the same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-the-virtual-network-for-your-new-vm"></a><span data-ttu-id="cabed-143">Configurare la rete virtuale per la nuova VM</span><span class="sxs-lookup"><span data-stu-id="cabed-143">Set up the virtual network for your new VM</span></span>
<span data-ttu-id="cabed-144">Configurare una rete virtuale e una scheda NIC per la nuova VM.</span><span class="sxs-lookup"><span data-stu-id="cabed-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-the-new-vm"></a><span data-ttu-id="cabed-145">Creare la nuova VM</span><span class="sxs-lookup"><span data-stu-id="cabed-145">Create the new VM</span></span>
<span data-ttu-id="cabed-146">A questo punto è possibile creare una VM dal disco rigido virtuale caricato [usando un modello di Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) oppure tramite l'interfaccia della riga di comando, specificando l'URI del disco copiato come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="cabed-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through the CLI by specifying the URI to your copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="cabed-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cabed-147">Next steps</span></span>
<span data-ttu-id="cabed-148">Per altre informazioni su come usare l'interfaccia della riga di comando di Azure per gestire la nuova macchina virtuale, vedere [Comandi dell'interfaccia della riga di comando Azure per Azure Resource Manager](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="cabed-148">To learn how to use Azure CLI to manage your new virtual machine, see [Azure CLI commands for the Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

