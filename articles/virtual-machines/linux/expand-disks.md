---
title: aaaExpand i dischi rigidi virtuali in una VM Linux di Azure | Documenti Microsoft
description: Informazioni su come tooexpand i dischi rigidi virtuali in una VM Linux con hello Azure CLI 2.0
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
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="9baf9-103">Come tooexpand i dischi rigidi virtuali in una VM Linux con hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="9baf9-103">How tooexpand virtual hard disks on a Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="9baf9-104">dimensioni di disco rigido virtuale Hello predefinite per il sistema operativo hello (sistema operativo) sono in genere 30 GB in una macchina virtuale Linux (VM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="9baf9-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="9baf9-105">È possibile [aggiungere dischi dati](add-disk.md) tooprovide per ulteriore spazio di archiviazione, ma è inoltre possibile tooexpand un disco dati esistente.</span><span class="sxs-lookup"><span data-stu-id="9baf9-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand an existing data disk.</span></span> <span data-ttu-id="9baf9-106">In questo articolo illustra in dettaglio come dischi tooexpand gestiti per una VM Linux con hello CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="9baf9-106">This article details how tooexpand managed disks for a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="9baf9-107">È anche possibile espandere il disco del sistema operativo hello non gestita con hello [CLI di Azure 1.0](expand-disks-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9baf9-107">You can also expand hello unmanaged OS disk with hello [Azure CLI 1.0](expand-disks-nodejs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="9baf9-108">Assicurarsi sempre di eseguire il backup dei dati prima di eseguire operazioni di ridimensionamento dei dischi.</span><span class="sxs-lookup"><span data-stu-id="9baf9-108">Always make sure that you back up your data before you perform disk resize operations.</span></span> <span data-ttu-id="9baf9-109">Per altre informazioni, vedere [Eseguire il backup di macchine virtuali Linux in Azure](tutorial-backup-vms.md).</span><span class="sxs-lookup"><span data-stu-id="9baf9-109">For more information, see [Back up Linux VMs in Azure](tutorial-backup-vms.md).</span></span>

## <a name="expand-disk"></a><span data-ttu-id="9baf9-110">Espandere il disco</span><span class="sxs-lookup"><span data-stu-id="9baf9-110">Expand disk</span></span>
<span data-ttu-id="9baf9-111">Assicurarsi di aver hello più recente [CLI di Azure 2.0](/cli/azure/install-az-cli2) installato e registrato con un account Azure tooan [accesso az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="9baf9-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="9baf9-112">Questo articolo richiede una VM esistente in Azure con almeno un disco dati collegato e preparato.</span><span class="sxs-lookup"><span data-stu-id="9baf9-112">This article requires an existing VM in Azure with at least one data disk attached and prepared.</span></span> <span data-ttu-id="9baf9-113">Se non si ha già una VM da usare, vedere [Creare e preparare una VM con dischi dati](tutorial-manage-disks.md#create-and-attach-disks).</span><span class="sxs-lookup"><span data-stu-id="9baf9-113">If you do not already have a VM that you can use, see [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks).</span></span>

<span data-ttu-id="9baf9-114">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="9baf9-114">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="9baf9-115">I nomi dei parametri di esempio includono *myResourceGroup* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="9baf9-115">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

1. <span data-ttu-id="9baf9-116">Impossibile eseguire operazioni su dischi rigidi virtuali con hello macchina virtuale in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9baf9-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="9baf9-117">Deallocare la macchina virtuale con [az vm deallocate](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="9baf9-117">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="9baf9-118">esempio Hello dealloca hello macchina virtuale denominata *myVM* nel gruppo di risorse hello denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="9baf9-118">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="9baf9-119">`az vm stop`non rilasciare le risorse di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="9baf9-119">`az vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="9baf9-120">toorelease le risorse di calcolo, utilizzare `az vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="9baf9-120">toorelease compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="9baf9-121">Hello VM deve essere deallocata il disco rigido virtuale di tooexpand hello.</span><span class="sxs-lookup"><span data-stu-id="9baf9-121">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="9baf9-122">Vedere un elenco di dischi gestiti presenti nel gruppo di risorse con [az disk list](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="9baf9-122">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="9baf9-123">Hello esempio seguente visualizza un elenco di dischi gestiti nel gruppo di risorse hello denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="9baf9-123">hello following example displays a list of managed disks in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="9baf9-124">Espandere hello disco necessarie con [aggiornamento disco az](/cli/azure/disk#update).</span><span class="sxs-lookup"><span data-stu-id="9baf9-124">Expand hello required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="9baf9-125">esempio Hello espande disco di hello gestito denominato *myDataDisk* toobe *200*dimensioni Gb:</span><span class="sxs-lookup"><span data-stu-id="9baf9-125">hello following example expands hello managed disk named *myDataDisk* toobe *200*Gb in size:</span></span>

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="9baf9-126">Quando si espande un disco gestito, dimensioni hello aggiornato sono mappato toohello più vicino delle dimensioni del disco gestito.</span><span class="sxs-lookup"><span data-stu-id="9baf9-126">When you expand a managed disk, hello updated size is mapped toohello nearest managed disk size.</span></span> <span data-ttu-id="9baf9-127">Per una tabella di dimensioni disco gestito disponibili hello e livelli, vedere [gestiti dischi Panoramica di Azure - prezzi e fatturazione](../windows/managed-disks-overview.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="9baf9-127">For a table of hello available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../windows/managed-disks-overview.md#pricing-and-billing).</span></span>

3. <span data-ttu-id="9baf9-128">Avviare la macchina virtuale con [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="9baf9-128">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="9baf9-129">Dopo l'avvio di esempio Hello hello macchina virtuale denominata *myVM* nel gruppo di risorse hello denominato *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="9baf9-129">hello following example starts hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="9baf9-130">SSH tooyour VM con le credenziali appropriate hello.</span><span class="sxs-lookup"><span data-stu-id="9baf9-130">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="9baf9-131">È possibile ottenere l'indirizzo IP pubblico hello della macchina virtuale con [Mostra vm az](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="9baf9-131">You can obtain hello public IP address of your VM with [az vm show](/cli/azure/vm#show):</span></span>

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. <span data-ttu-id="9baf9-132">hello toouse espansa del disco, è necessario filesystem e partizione di tooexpand hello sottostante.</span><span class="sxs-lookup"><span data-stu-id="9baf9-132">toouse hello expanded disk, you need tooexpand hello underlying partition and filesystem.</span></span>

    <span data-ttu-id="9baf9-133">a.</span><span class="sxs-lookup"><span data-stu-id="9baf9-133">a.</span></span> <span data-ttu-id="9baf9-134">Se è già montato, smontare il disco hello:</span><span class="sxs-lookup"><span data-stu-id="9baf9-134">If already mounted, unmount hello disk:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

    <span data-ttu-id="9baf9-135">b.</span><span class="sxs-lookup"><span data-stu-id="9baf9-135">b.</span></span> <span data-ttu-id="9baf9-136">Utilizzare `parted` tooview informazioni sul disco e ridimensionare partizione hello:</span><span class="sxs-lookup"><span data-stu-id="9baf9-136">Use `parted` tooview disk information and resize hello partition:</span></span>

    ```bash
    sudo parted /dev/sdc
    ```

    <span data-ttu-id="9baf9-137">Consente di visualizzare informazioni sul layout di partizione esistente di hello con `print`.</span><span class="sxs-lookup"><span data-stu-id="9baf9-137">View information about hello existing partition layout with `print`.</span></span> <span data-ttu-id="9baf9-138">l'output è simile toohello seguente esempio, disco sottostante hello è Gb 215 dimensioni Hello:</span><span class="sxs-lookup"><span data-stu-id="9baf9-138">hello output is similar toohello following example, which shows hello underlying disk is 215Gb in size:</span></span>

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    <span data-ttu-id="9baf9-139">c.</span><span class="sxs-lookup"><span data-stu-id="9baf9-139">c.</span></span> <span data-ttu-id="9baf9-140">Espandere la partizione hello con `resizepart`.</span><span class="sxs-lookup"><span data-stu-id="9baf9-140">Expand hello partition with `resizepart`.</span></span> <span data-ttu-id="9baf9-141">Immettere il numero di partizione hello, *1*e una dimensione per la nuova partizione hello:</span><span class="sxs-lookup"><span data-stu-id="9baf9-141">Enter hello partition number, *1*, and a size for hello new partition:</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    <span data-ttu-id="9baf9-142">d.</span><span class="sxs-lookup"><span data-stu-id="9baf9-142">d.</span></span> <span data-ttu-id="9baf9-143">tooexit, immettere`quit`</span><span class="sxs-lookup"><span data-stu-id="9baf9-143">tooexit, enter `quit`</span></span>

5. <span data-ttu-id="9baf9-144">Con partizione hello ridimensionato, verificare la coerenza di partizione hello con `e2fsck`:</span><span class="sxs-lookup"><span data-stu-id="9baf9-144">With hello partition resized, verify hello partition consistency with `e2fsck`:</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. <span data-ttu-id="9baf9-145">Ora ridimensionare filesystem hello con `resize2fs`:</span><span class="sxs-lookup"><span data-stu-id="9baf9-145">Now resize hello filesystem with `resize2fs`:</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. <span data-ttu-id="9baf9-146">Montaggio hello partizione toohello desiderati percorso, ad esempio `/datadrive`:</span><span class="sxs-lookup"><span data-stu-id="9baf9-146">Mount hello partition toohello desired location, such as `/datadrive`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. <span data-ttu-id="9baf9-147">disco del sistema operativo hello tooverify è stato ridimensionato, utilizzare `df -h`.</span><span class="sxs-lookup"><span data-stu-id="9baf9-147">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="9baf9-148">Hello output di esempio seguente viene illustrato l'unità dati hello, *dev/sdc1*, ora pari a 200 GB:</span><span class="sxs-lookup"><span data-stu-id="9baf9-148">hello following example output shows hello data drive, */dev/sdc1*, is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="9baf9-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9baf9-149">Next steps</span></span>
<span data-ttu-id="9baf9-150">Se è necessario ulteriore spazio di archiviazione, è anche [aggiungere tooa dischi dati VM Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="9baf9-150">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="9baf9-151">Per ulteriori informazioni sulla crittografia del disco, vedere [Encrypt dischi in una VM Linux utilizzando hello Azure CLI](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="9baf9-151">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
