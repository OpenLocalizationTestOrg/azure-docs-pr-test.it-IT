---
title: Espandere i dischi rigidi virtuali in una macchina virtuale Linux in Azure | Microsoft Docs
description: Informazioni su come espandere i dischi rigidi virtuali in una macchina virtuale Linux con l'interfaccia della riga di comando 2.0 di Azure
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: b82cc0473c003da767ee230ab485c69b233977d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-expand-virtual-hard-disks-on-a-linux-vm-with-the-azure-cli"></a><span data-ttu-id="268b9-103">Procedura per espandere i dischi rigidi virtuali in una macchina virtuale Linux con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="268b9-103">How to expand virtual hard disks on a Linux VM with the Azure CLI</span></span>
<span data-ttu-id="268b9-104">Le dimensioni predefinite del disco rigido virtuale per il sistema operativo sono in genere di 30 GB in una VM Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="268b9-104">The default virtual hard disk size for the operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="268b9-105">È possibile [aggiungere dischi dati](add-disk.md) per aumentare lo spazio di archiviazione, ma è anche possibile espandere un disco dati esistente.</span><span class="sxs-lookup"><span data-stu-id="268b9-105">You can [add data disks](add-disk.md) to provide for additional storage space, but you may also wish to expand an existing data disk.</span></span> <span data-ttu-id="268b9-106">Questo articolo illustra come espandere i dischi gestiti di una macchina virtuale Linux tramite l'interfaccia della riga di comando 2.0 di Azure.</span><span class="sxs-lookup"><span data-stu-id="268b9-106">This article details how to expand managed disks for a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="268b9-107">È anche possibile espandere il disco del sistema operativo non gestito con l'[interfaccia della riga di comando 1.0 di Azure](expand-disks-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="268b9-107">You can also expand the unmanaged OS disk with the [Azure CLI 1.0](expand-disks-nodejs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="268b9-108">Assicurarsi sempre di eseguire il backup dei dati prima di eseguire operazioni di ridimensionamento dei dischi.</span><span class="sxs-lookup"><span data-stu-id="268b9-108">Always make sure that you back up your data before you perform disk resize operations.</span></span> <span data-ttu-id="268b9-109">Per altre informazioni, vedere [Eseguire il backup di macchine virtuali Linux in Azure](tutorial-backup-vms.md).</span><span class="sxs-lookup"><span data-stu-id="268b9-109">For more information, see [Back up Linux VMs in Azure](tutorial-backup-vms.md).</span></span>

## <a name="expand-disk"></a><span data-ttu-id="268b9-110">Espandere il disco</span><span class="sxs-lookup"><span data-stu-id="268b9-110">Expand disk</span></span>
<span data-ttu-id="268b9-111">Assicurarsi di avere installato la versione più recente dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e di aver eseguito l'accesso a un account Azure tramite il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="268b9-111">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="268b9-112">Questo articolo richiede una VM esistente in Azure con almeno un disco dati collegato e preparato.</span><span class="sxs-lookup"><span data-stu-id="268b9-112">This article requires an existing VM in Azure with at least one data disk attached and prepared.</span></span> <span data-ttu-id="268b9-113">Se non si ha già una VM da usare, vedere [Creare e preparare una VM con dischi dati](tutorial-manage-disks.md#create-and-attach-disks).</span><span class="sxs-lookup"><span data-stu-id="268b9-113">If you do not already have a VM that you can use, see [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks).</span></span>

<span data-ttu-id="268b9-114">Negli esempi seguenti sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="268b9-114">In the following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="268b9-115">I nomi dei parametri di esempio includono *myResourceGroup* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="268b9-115">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

1. <span data-ttu-id="268b9-116">Non è possibile eseguire operazioni sui dischi rigidi virtuali quando la macchina virtuale è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="268b9-116">Operations on virtual hard disks cannot be performed with the VM running.</span></span> <span data-ttu-id="268b9-117">Deallocare la macchina virtuale con [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="268b9-117">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="268b9-118">L'esempio seguente dealloca la VM denominata *myVM* nel gruppo di risorse *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="268b9-118">The following example deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="268b9-119">`az vm stop` non rilascia le risorse di calcolo.</span><span class="sxs-lookup"><span data-stu-id="268b9-119">`az vm stop` does not release the compute resources.</span></span> <span data-ttu-id="268b9-120">Per rilasciare le risorse di calcolo, usare `az vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="268b9-120">To release compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="268b9-121">Per espandere il disco rigido virtuale è necessario deallocare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="268b9-121">The VM must be deallocated to expand the virtual hard disk.</span></span>

2. <span data-ttu-id="268b9-122">Vedere un elenco di dischi gestiti presenti nel gruppo di risorse con [az disk list](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="268b9-122">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="268b9-123">L'esempio seguente mostra un elenco di dischi gestiti nel gruppo di risorse denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="268b9-123">The following example displays a list of managed disks in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="268b9-124">Espandere il disco richiesto con [az disk update](/cli/azure/disk#update).</span><span class="sxs-lookup"><span data-stu-id="268b9-124">Expand the required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="268b9-125">L'esempio seguente espande il disco gestito denominato *myDataDisk* per portarlo a *200*Gb:</span><span class="sxs-lookup"><span data-stu-id="268b9-125">The following example expands the managed disk named *myDataDisk* to be *200*Gb in size:</span></span>

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="268b9-126">Quando si espande un disco gestito, si esegue il mapping delle dimensioni aggiornate per le dimensioni del disco gestito più vicino.</span><span class="sxs-lookup"><span data-stu-id="268b9-126">When you expand a managed disk, the updated size is mapped to the nearest managed disk size.</span></span> <span data-ttu-id="268b9-127">Per consultare una tabella delle dimensioni e dei livelli dei dischi disponibili, vedere [Panoramica di Azure Managed Disks - Prezzi e fatturazione](../windows/managed-disks-overview.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="268b9-127">For a table of the available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../windows/managed-disks-overview.md#pricing-and-billing).</span></span>

3. <span data-ttu-id="268b9-128">Avviare la macchina virtuale con [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="268b9-128">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="268b9-129">L'esempio seguente avvia la VM denominata *myVM* nel gruppo di risorse *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="268b9-129">The following example starts the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="268b9-130">Eseguire SSH nella macchina virtuale con le credenziali appropriate.</span><span class="sxs-lookup"><span data-stu-id="268b9-130">SSH to your VM with the appropriate credentials.</span></span> <span data-ttu-id="268b9-131">È possibile ottenere l'indirizzo IP pubblico della VM con [az vm show](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="268b9-131">You can obtain the public IP address of your VM with [az vm show](/cli/azure/vm#show):</span></span>

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. <span data-ttu-id="268b9-132">Per usare il disco espanso, è necessario espandere la partizione e il file system sottostanti.</span><span class="sxs-lookup"><span data-stu-id="268b9-132">To use the expanded disk, you need to expand the underlying partition and filesystem.</span></span>

    <span data-ttu-id="268b9-133">a.</span><span class="sxs-lookup"><span data-stu-id="268b9-133">a.</span></span> <span data-ttu-id="268b9-134">Se il disco è già montato, smontarlo:</span><span class="sxs-lookup"><span data-stu-id="268b9-134">If already mounted, unmount the disk:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

    <span data-ttu-id="268b9-135">b.</span><span class="sxs-lookup"><span data-stu-id="268b9-135">b.</span></span> <span data-ttu-id="268b9-136">Usare `parted` per visualizzare informazioni sul disco e ridimensionare la partizione:</span><span class="sxs-lookup"><span data-stu-id="268b9-136">Use `parted` to view disk information and resize the partition:</span></span>

    ```bash
    sudo parted /dev/sdc
    ```

    <span data-ttu-id="268b9-137">Visualizzare le informazioni sul layout di partizione esistente con `print`.</span><span class="sxs-lookup"><span data-stu-id="268b9-137">View information about the existing partition layout with `print`.</span></span> <span data-ttu-id="268b9-138">L'output è simile all'esempio seguente, che mostra che il disco sottostante ha dimensioni di 215 GB:</span><span class="sxs-lookup"><span data-stu-id="268b9-138">The output is similar to the following example, which shows the underlying disk is 215Gb in size:</span></span>

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome to GNU Parted! Type 'help' to view a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    <span data-ttu-id="268b9-139">c.</span><span class="sxs-lookup"><span data-stu-id="268b9-139">c.</span></span> <span data-ttu-id="268b9-140">Espandere la partizione con `resizepart`.</span><span class="sxs-lookup"><span data-stu-id="268b9-140">Expand the partition with `resizepart`.</span></span> <span data-ttu-id="268b9-141">Immettere il numero di partizione, *1*, e le dimensioni per la nuova partizione:</span><span class="sxs-lookup"><span data-stu-id="268b9-141">Enter the partition number, *1*, and a size for the new partition:</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    <span data-ttu-id="268b9-142">d.</span><span class="sxs-lookup"><span data-stu-id="268b9-142">d.</span></span> <span data-ttu-id="268b9-143">Per uscire, immettere `quit`</span><span class="sxs-lookup"><span data-stu-id="268b9-143">To exit, enter `quit`</span></span>

5. <span data-ttu-id="268b9-144">Dopo aver ridimensionato la partizione, verificarne la coerenza con `e2fsck`:</span><span class="sxs-lookup"><span data-stu-id="268b9-144">With the partition resized, verify the partition consistency with `e2fsck`:</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. <span data-ttu-id="268b9-145">Ridimensionare quindi il file system con `resize2fs`:</span><span class="sxs-lookup"><span data-stu-id="268b9-145">Now resize the filesystem with `resize2fs`:</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. <span data-ttu-id="268b9-146">Montare la partizione nella posizione desiderata, ad esempio `/datadrive`:</span><span class="sxs-lookup"><span data-stu-id="268b9-146">Mount the partition to the desired location, such as `/datadrive`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. <span data-ttu-id="268b9-147">Per verificare che il disco del sistema operativo sia stato ridimensionato, usare `df -h`.</span><span class="sxs-lookup"><span data-stu-id="268b9-147">To verify the OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="268b9-148">L'output di esempio seguente mostra che il disco dati */dev/sdc1* ha ora dimensioni di 200 GB:</span><span class="sxs-lookup"><span data-stu-id="268b9-148">The following example output shows the data drive, */dev/sdc1*, is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="268b9-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="268b9-149">Next steps</span></span>
<span data-ttu-id="268b9-150">Se è necessario altro spazio di archiviazione, è possibile [aggiungere dischi dati a una VM Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="268b9-150">If you need additional storage, you also [add data disks to a Linux VM](add-disk.md).</span></span> <span data-ttu-id="268b9-151">Per altre informazioni sulla crittografia del disco, vedere [Crittografare i dischi di una VM Linux usando l'interfaccia della riga di comando di Azure](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="268b9-151">For more information about disk encryption, see [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md).</span></span>
