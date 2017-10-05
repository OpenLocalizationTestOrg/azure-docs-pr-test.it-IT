---
title: Copiare una macchina virtuale Linux usando l'interfaccia della riga di comando di Azure 2.0 |Microsoft Docs
description: Informazioni su come creare una copia della VM Linux di Azure usando l'interfaccia della riga di comando di Azure 2.0 e i dischi gestiti.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: 7983061a933370803669480296d7625106e1360c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a><span data-ttu-id="6b078-103">Creare una copia di una VM Linux di Azure usando l'interfaccia della riga di comando di Azure 2.0 e i dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="6b078-103">Create a copy of a Linux VM by using Azure CLI 2.0 and Managed Disks</span></span>


<span data-ttu-id="6b078-104">Questo articolo descrive come creare una copia di una macchina virtuale (VM) di Azure che esegue Linux usando l'interfaccia della riga di comando di Azure 2.0 e il modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6b078-104">This article shows you how to create a copy of your Azure virtual machine (VM) running Linux using the Azure CLI 2.0 and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="6b078-105">È possibile anche eseguire questi passaggi tramite l'[interfaccia della riga di comando di Azure 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6b078-105">You can also perform these steps with the [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="6b078-106">È anche possibile [caricare e creare una VM da un disco rigido virtuale](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6b078-106">You can also [upload and create a VM from a VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b078-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6b078-107">Prerequisites</span></span>


-   <span data-ttu-id="6b078-108">Installare l'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="6b078-108">Install [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

-   <span data-ttu-id="6b078-109">Accedere a un account di Azure con [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="6b078-109">Sign in to an Azure account with [az login](/cli/azure/#login).</span></span>

-   <span data-ttu-id="6b078-110">Disporre di una VM di Azure da usare come origine per la copia.</span><span class="sxs-lookup"><span data-stu-id="6b078-110">Have an Azure VM to use as the source for your copy.</span></span>

## <a name="step-1-stop-the-source-vm"></a><span data-ttu-id="6b078-111">Passaggio 1: Arrestare la macchina virtuale di origine</span><span class="sxs-lookup"><span data-stu-id="6b078-111">Step 1: Stop the source VM</span></span>


<span data-ttu-id="6b078-112">Deallocare la macchina virtuale di origine usando il comando [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="6b078-112">Deallocate the source VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span>
<span data-ttu-id="6b078-113">L'esempio seguente dealloca la VM denominata **myVM** nel gruppo di risorse **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="6b078-113">The following example deallocates the VM named **myVM** in the resource group **myResourceGroup**:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-the-source-vm"></a><span data-ttu-id="6b078-114">Passaggio 2: Copiare la macchina virtuale di origine</span><span class="sxs-lookup"><span data-stu-id="6b078-114">Step 2: Copy the source VM</span></span>


<span data-ttu-id="6b078-115">Per copiare una macchina virtuale, si crea una copia del disco rigido virtuale sottostante.</span><span class="sxs-lookup"><span data-stu-id="6b078-115">To copy a VM, you create a copy of the underlying virtual hard disk.</span></span> <span data-ttu-id="6b078-116">Questo processo crea un disco rigido virtuale specializzato come disco gestito che contiene la stessa configurazione e le stesse impostazioni della VM di origine.</span><span class="sxs-lookup"><span data-stu-id="6b078-116">This process creates a specialized VHD as a Managed Disk that contains the same configuration and settings as the source VM.</span></span>

<span data-ttu-id="6b078-117">Per altre informazioni su Azure Managed Disks, vedere [Azure Managed Disks overview](../windows/managed-disks-overview.md) (Panoramica di Azure Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="6b078-117">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span> 

1.  <span data-ttu-id="6b078-118">Elencare ogni VM e il nome del relativo disco del sistema operativo con [az vm list](/cli/azure/vm#list).</span><span class="sxs-lookup"><span data-stu-id="6b078-118">List each VM and the name of its OS disk with [az vm list](/cli/azure/vm#list).</span></span> <span data-ttu-id="6b078-119">L'esempio seguente elenca tutte le VM del gruppo di risorse denominato **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="6b078-119">The following example lists all VMs in the resource group named **myResourceGroup**:</span></span>
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    <span data-ttu-id="6b078-120">L'output è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6b078-120">The output is similar to the following example:</span></span>

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  <span data-ttu-id="6b078-121">Copiare il disco creando un nuovo disco gestito con [az disk create](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="6b078-121">Copy the disk by creating a new managed disk using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="6b078-122">L'esempio seguente crea un disco denominato **myCopiedDisk** dal disco gestito denominato **myDisk**:</span><span class="sxs-lookup"><span data-stu-id="6b078-122">The following example creates a disk named **myCopiedDisk** from the managed disk named **myDisk**:</span></span>

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  <span data-ttu-id="6b078-123">Verificare i dischi gestiti ora presenti nel gruppo di risorse usando il comando [az disk list](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="6b078-123">Verify the managed disks now in your resource group by using [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="6b078-124">L'esempio seguente elenca i dischi gestiti nel gruppo di risorse denominato **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="6b078-124">The following example lists the managed disks in the resource group named **myResourceGroup**:</span></span>

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  <span data-ttu-id="6b078-125">Andare al [Passaggio 3: Configurare una rete virtuale](#step-3-set-up-a-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="6b078-125">Skip to ["Step 3: Set up a virtual network"](#step-3-set-up-a-virtual-network).</span></span>


## <a name="step-3-set-up-a-virtual-network"></a><span data-ttu-id="6b078-126">Passaggio 3: Configurare una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="6b078-126">Step 3: Set up a virtual network</span></span>


<span data-ttu-id="6b078-127">La procedura facoltativa seguente permette di creare una nuova rete virtuale, una subnet, un indirizzo IP pubblico e una scheda di interfaccia di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="6b078-127">The following optional steps create a new virtual network, subnet, public IP address, and virtual network interface card (NIC).</span></span>

<span data-ttu-id="6b078-128">Se si copia una macchina virtuale per la risoluzione di problemi o per distribuzioni aggiuntive, non è consigliabile usare una macchina virtuale in una rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="6b078-128">If you are copying a VM for troubleshooting purposes or additional deployments, you might not want to use a VM in an existing virtual network.</span></span>

<span data-ttu-id="6b078-129">Se si vuole creare un'infrastruttura di rete virtuale per le macchine virtuali copiate, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="6b078-129">If you want to create a virtual network infrastructure for your copied VMs, follow the next few steps.</span></span> <span data-ttu-id="6b078-130">Se non si vuole creare una rete virtuale, andare al [Passaggio 4: Creare una VM](#step-4-create-a-vm).</span><span class="sxs-lookup"><span data-stu-id="6b078-130">If you don't want to create a virtual network, skip to [Step 4: Create a VM](#step-4-create-a-vm).</span></span>

1.  <span data-ttu-id="6b078-131">Creare la rete virtuale usando il comando [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="6b078-131">Create the virtual network by using [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="6b078-132">L'esempio seguente crea una rete virtuale denominata **myVnet** e una subnet denominata **mySubnet**:</span><span class="sxs-lookup"><span data-stu-id="6b078-132">The following example creates a virtual network named **myVnet** and a subnet named **mySubnet**:</span></span>

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  <span data-ttu-id="6b078-133">Creare un indirizzo IP pubblico usando il comando [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="6b078-133">Create a public IP by using [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="6b078-134">L'esempio seguente crea un indirizzo IP pubblico chiamato **myPublicIP** con il nome DNS **mypublicdns**.</span><span class="sxs-lookup"><span data-stu-id="6b078-134">The following example creates a public IP named **myPublicIP** with the DNS name of **mypublicdns**.</span></span> <span data-ttu-id="6b078-135">È necessario specificare un nome DNS univoco.</span><span class="sxs-lookup"><span data-stu-id="6b078-135">(The DNS name must be unique, so provide a unique name.)</span></span>

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  <span data-ttu-id="6b078-136">Creare la scheda di interfaccia di rete usando [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="6b078-136">Create the NIC using [az network nic create](/cli/azure/network/nic#create).</span></span>
    <span data-ttu-id="6b078-137">L'esempio seguente crea una scheda di interfaccia di rete denominata **myNic** associata alla subnet **mySubnet**:</span><span class="sxs-lookup"><span data-stu-id="6b078-137">The following example creates a NIC named **myNic** that's attached to the **mySubnet** subnet:</span></span>

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a><span data-ttu-id="6b078-138">Passaggio 4: Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="6b078-138">Step 4: Create a VM</span></span>

<span data-ttu-id="6b078-139">Ora è possibile creare una macchina virtuale usando il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="6b078-139">You can now create a VM by using [az vm create](/cli/azure/vm#create).</span></span>

<span data-ttu-id="6b078-140">Specificare il disco gestito copiato da usare come disco del sistema operativo (--attach-os-disk). A tale scopo, procedere come segue:</span><span class="sxs-lookup"><span data-stu-id="6b078-140">Specify the copied managed disk to use as the OS disk (--attach-os-disk), as follows:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a><span data-ttu-id="6b078-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6b078-141">Next steps</span></span>

<span data-ttu-id="6b078-142">Per informazioni su come usare l'interfaccia della riga di comando di Azure per gestire la nuova VM, vedere [Comandi dell'interfaccia della riga di comando di Azure per Azure Resource Manager](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="6b078-142">To learn how to use Azure CLI to manage your new VM, see [Azure CLI commands for the Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>
