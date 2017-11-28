---
title: una VM Linux mediante Azure CLI 2.0 aaaCopy | Documenti Microsoft
description: Informazioni su come toocreate una copia della macchina virtuale Linux di Azure mediante Azure CLI 2.0 e i dischi gestiti.
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
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a><span data-ttu-id="abd89-103">Creare una copia di una VM Linux di Azure usando l'interfaccia della riga di comando di Azure 2.0 e i dischi gestiti</span><span class="sxs-lookup"><span data-stu-id="abd89-103">Create a copy of a Linux VM by using Azure CLI 2.0 and Managed Disks</span></span>


<span data-ttu-id="abd89-104">In questo articolo viene illustrato come una copia della macchina virtuale Azure (VM) in esecuzione Linux usando toocreate hello Azure CLI 2.0 e il modello di distribuzione Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="abd89-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Azure CLI 2.0 and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="abd89-105">È anche possibile eseguire questi passaggi con hello [CLI di Azure 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="abd89-105">You can also perform these steps with hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="abd89-106">È anche possibile [caricare e creare una VM da un disco rigido virtuale](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="abd89-106">You can also [upload and create a VM from a VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abd89-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="abd89-107">Prerequisites</span></span>


-   <span data-ttu-id="abd89-108">Installare l'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="abd89-108">Install [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

-   <span data-ttu-id="abd89-109">Accedi tooan account Azure con [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="abd89-109">Sign in tooan Azure account with [az login](/cli/azure/#login).</span></span>

-   <span data-ttu-id="abd89-110">Toouse una macchina virtuale di Azure per avere hello origine per la copia.</span><span class="sxs-lookup"><span data-stu-id="abd89-110">Have an Azure VM toouse as hello source for your copy.</span></span>

## <a name="step-1-stop-hello-source-vm"></a><span data-ttu-id="abd89-111">Passaggio 1: Arresta macchina virtuale di origine hello</span><span class="sxs-lookup"><span data-stu-id="abd89-111">Step 1: Stop hello source VM</span></span>


<span data-ttu-id="abd89-112">Deallocare una macchina virtuale di origine hello utilizzando [az vm deallocare](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="abd89-112">Deallocate hello source VM by using [az vm deallocate](/cli/azure/vm#deallocate).</span></span>
<span data-ttu-id="abd89-113">esempio Hello dealloca hello macchina virtuale denominata **myVM** nel gruppo di risorse hello **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="abd89-113">hello following example deallocates hello VM named **myVM** in hello resource group **myResourceGroup**:</span></span>

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a><span data-ttu-id="abd89-114">Passaggio 2: Copiare una macchina virtuale di origine hello</span><span class="sxs-lookup"><span data-stu-id="abd89-114">Step 2: Copy hello source VM</span></span>


<span data-ttu-id="abd89-115">toocopy una macchina virtuale, si crea una copia del disco rigido virtuale sottostante di hello.</span><span class="sxs-lookup"><span data-stu-id="abd89-115">toocopy a VM, you create a copy of hello underlying virtual hard disk.</span></span> <span data-ttu-id="abd89-116">Questo processo crea un disco rigido virtuale specifico come disco gestita che contiene hello impostazioni come hello e la stessa configurazione di macchina virtuale di origine.</span><span class="sxs-lookup"><span data-stu-id="abd89-116">This process creates a specialized VHD as a Managed Disk that contains hello same configuration and settings as hello source VM.</span></span>

<span data-ttu-id="abd89-117">Per altre informazioni su Azure Managed Disks, vedere [Azure Managed Disks overview](../windows/managed-disks-overview.md) (Panoramica di Azure Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="abd89-117">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span> 

1.  <span data-ttu-id="abd89-118">Elenco di ogni macchina virtuale e hello il nome del relativo disco del sistema operativo con [elenco vm az](/cli/azure/vm#list).</span><span class="sxs-lookup"><span data-stu-id="abd89-118">List each VM and hello name of its OS disk with [az vm list](/cli/azure/vm#list).</span></span> <span data-ttu-id="abd89-119">Hello esempio seguente vengono elencate tutte le macchine virtuali nel gruppo di risorse denominato **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="abd89-119">hello following example lists all VMs in the resource group named **myResourceGroup**:</span></span>
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    <span data-ttu-id="abd89-120">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="abd89-120">hello output is similar toohello following example:</span></span>

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  <span data-ttu-id="abd89-121">Disco di hello copia creando un nuovo gestito disco tramite [disco az creare](/cli/azure/disk#create).</span><span class="sxs-lookup"><span data-stu-id="abd89-121">Copy hello disk by creating a new managed disk using [az disk create](/cli/azure/disk#create).</span></span> <span data-ttu-id="abd89-122">esempio Hello crea un disco denominato **myCopiedDisk** da hello gestito disco denominato **myDisk**:</span><span class="sxs-lookup"><span data-stu-id="abd89-122">hello following example creates a disk named **myCopiedDisk** from hello managed disk named **myDisk**:</span></span>

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  <span data-ttu-id="abd89-123">Verificare i dischi di hello gestito ora nel gruppo di risorse utilizzando [elenco disco az](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="abd89-123">Verify hello managed disks now in your resource group by using [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="abd89-124">esempio Hello Elenca dischi hello gestito nel gruppo di risorse hello denominato **myResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="abd89-124">hello following example lists hello managed disks in hello resource group named **myResourceGroup**:</span></span>

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  <span data-ttu-id="abd89-125">Ignorare troppo["passaggio 3: configurare una rete virtuale"](#step-3-set-up-a-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="abd89-125">Skip too["Step 3: Set up a virtual network"](#step-3-set-up-a-virtual-network).</span></span>


## <a name="step-3-set-up-a-virtual-network"></a><span data-ttu-id="abd89-126">Passaggio 3: Configurare una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="abd89-126">Step 3: Set up a virtual network</span></span>


<span data-ttu-id="abd89-127">Hello passaggi facoltativi seguenti creare una nuova rete virtuale, subnet, l'indirizzo IP pubblico e scheda di interfaccia di rete virtuale (NIC).</span><span class="sxs-lookup"><span data-stu-id="abd89-127">hello following optional steps create a new virtual network, subnet, public IP address, and virtual network interface card (NIC).</span></span>

<span data-ttu-id="abd89-128">Se si copia una macchina virtuale per la risoluzione dei problemi relativi a scopo o altre distribuzioni, è consigliabile non toouse una macchina virtuale in una rete virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="abd89-128">If you are copying a VM for troubleshooting purposes or additional deployments, you might not want toouse a VM in an existing virtual network.</span></span>

<span data-ttu-id="abd89-129">Se si desidera toocreate un'infrastruttura di rete virtuale per le macchine virtuali di copiate, quindi seguire hello alcuni passaggi.</span><span class="sxs-lookup"><span data-stu-id="abd89-129">If you want toocreate a virtual network infrastructure for your copied VMs, follow hello next few steps.</span></span> <span data-ttu-id="abd89-130">Se non si desidera toocreate una rete virtuale, andare troppo[passaggio 4: creare una macchina virtuale](#step-4-create-a-vm).</span><span class="sxs-lookup"><span data-stu-id="abd89-130">If you don't want toocreate a virtual network, skip too[Step 4: Create a VM](#step-4-create-a-vm).</span></span>

1.  <span data-ttu-id="abd89-131">Creare una rete virtuale hello utilizzando [creazione della rete virtuale di rete az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="abd89-131">Create hello virtual network by using [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="abd89-132">esempio Hello crea una rete virtuale denominata **myVnet** e una subnet denominata **mySubnet**:</span><span class="sxs-lookup"><span data-stu-id="abd89-132">hello following example creates a virtual network named **myVnet** and a subnet named **mySubnet**:</span></span>

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  <span data-ttu-id="abd89-133">Creare un indirizzo IP pubblico usando il comando [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="abd89-133">Create a public IP by using [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="abd89-134">esempio Hello crea un indirizzo IP pubblico denominato **myPublicIP** con nome DNS hello **mypublicdns**.</span><span class="sxs-lookup"><span data-stu-id="abd89-134">hello following example creates a public IP named **myPublicIP** with hello DNS name of **mypublicdns**.</span></span> <span data-ttu-id="abd89-135">(nome DNS hello deve essere univoco, quindi specificare un nome univoco.)</span><span class="sxs-lookup"><span data-stu-id="abd89-135">(hello DNS name must be unique, so provide a unique name.)</span></span>

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  <span data-ttu-id="abd89-136">Creare una scheda NIC hello utilizzando [az rete nic creare](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="abd89-136">Create hello NIC using [az network nic create](/cli/azure/network/nic#create).</span></span>
    <span data-ttu-id="abd89-137">esempio Hello crea una scheda di rete denominata **myNic** toothe collegati che **mySubnet** subnet:</span><span class="sxs-lookup"><span data-stu-id="abd89-137">hello following example creates a NIC named **myNic** that's attached toothe **mySubnet** subnet:</span></span>

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a><span data-ttu-id="abd89-138">Passaggio 4: Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="abd89-138">Step 4: Create a VM</span></span>

<span data-ttu-id="abd89-139">Ora è possibile creare una macchina virtuale usando il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="abd89-139">You can now create a VM by using [az vm create](/cli/azure/vm#create).</span></span>

<span data-ttu-id="abd89-140">Specificare hello copiato toouse gestito disco come disco del sistema operativo hello (-disco del sistema operativo collegare), come segue:</span><span class="sxs-lookup"><span data-stu-id="abd89-140">Specify hello copied managed disk toouse as hello OS disk (--attach-os-disk), as follows:</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a><span data-ttu-id="abd89-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="abd89-141">Next steps</span></span>

<span data-ttu-id="abd89-142">toolearn come toouse CLI di Azure toomanage la nuova macchina virtuale, vedere [i comandi CLI di Azure per Gestione risorse di Azure hello](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="abd89-142">toolearn how toouse Azure CLI toomanage your new VM, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>
