---
title: Collegare un disco dati a una macchina virtuale Linux | Microsoft Docs
description: Come collegare un disco dati nuovo o esistente a una macchina virtuale Linux nel portale di Azure tramite il modello di distribuzione di Resource Manager.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5e1c6212-976c-4962-a297-177942f90907
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: cynthn
ms.openlocfilehash: 1599ee241c3d9fb3623ebd89ae30f2795cae1930
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-attach-a-data-disk-to-a-linux-vm-in-the-azure-portal"></a><span data-ttu-id="59c2f-103">Come collegare un disco dati a una macchina virtuale Linux nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="59c2f-103">How to attach a data disk to a Linux VM in the Azure portal</span></span>
<span data-ttu-id="59c2f-104">In questo articolo viene illustrato come collegare dischi nuovi o esistenti a una macchina virtuale Linux tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="59c2f-104">This article shows you how to attach both new and existing disks to a Linux virtual machine through the Azure portal.</span></span> <span data-ttu-id="59c2f-105">È possibile anche [collegare un disco dati a una macchina virtuale Windows nel portale di Azure](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="59c2f-105">You can also [attach a data disk to a Windows VM in the Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="59c2f-106">È possibile scegliere di usare Azure Managed Disks o dischi non gestiti.</span><span class="sxs-lookup"><span data-stu-id="59c2f-106">You can choose to use either Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="59c2f-107">La funzionalità Managed Disks viene gestita dalla piattaforma Azure e non richiede alcuna pianificazione o alcuna posizione per l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="59c2f-107">Managed disks are handled by the Azure platform and do not require any preparation or location to store them.</span></span> <span data-ttu-id="59c2f-108">I dischi non gestiti richiedono un account di archiviazione e presentano alcune [quote e limiti applicati](../../azure-subscription-service-limits.md#storage-limits).</span><span class="sxs-lookup"><span data-stu-id="59c2f-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="59c2f-109">Per altre informazioni su Azure Managed Disks, vedere [Azure Managed Disks overview](../windows/managed-disks-overview.md) (Panoramica di Azure Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="59c2f-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="59c2f-110">Prima di collegare i dischi alla macchina virtuale, leggere i seguenti suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="59c2f-110">Before you attach disks to your VM, review these tips:</span></span>

* <span data-ttu-id="59c2f-111">La dimensione della macchina virtuale controlla il numero di dischi dati che è possibile collegare.</span><span class="sxs-lookup"><span data-stu-id="59c2f-111">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="59c2f-112">Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="59c2f-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="59c2f-113">Per usare l'archiviazione Premium, è necessaria una macchina virtuale della serie DS o GS.</span><span class="sxs-lookup"><span data-stu-id="59c2f-113">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="59c2f-114">Con queste macchine virtuali, è possibile usare dischi Premium e Standard.</span><span class="sxs-lookup"><span data-stu-id="59c2f-114">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="59c2f-115">L’archiviazione Premium è disponibile solo in determinate aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="59c2f-115">Premium storage is available in certain regions.</span></span> <span data-ttu-id="59c2f-116">Per ulteriori informazioni, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="59c2f-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="59c2f-117">I dischi collegati a macchine virtuali sono effettivamente file con estensione VHD archiviati in Azure.</span><span class="sxs-lookup"><span data-stu-id="59c2f-117">Disks attached to virtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="59c2f-118">Per informazioni dettagliate, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="59c2f-118">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="find-the-virtual-machine"></a><span data-ttu-id="59c2f-119">Trovare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="59c2f-119">Find the virtual machine</span></span>
1. <span data-ttu-id="59c2f-120">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="59c2f-120">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="59c2f-121">Scegliere **Macchine virtuali**dal menu Hub.</span><span class="sxs-lookup"><span data-stu-id="59c2f-121">On the Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="59c2f-122">Selezionare la macchina virtuale dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="59c2f-122">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="59c2f-123">Nel pannello Macchine virtuali di **Essentials** fare clic su **Dischi**.</span><span class="sxs-lookup"><span data-stu-id="59c2f-123">To the Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![Aprire le impostazioni del disco](./media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="59c2f-125">Continuare seguendo le istruzioni per il collegamento di un [disco gestito](#use-azure-managed-disks) o di un [disco non gestito](#use-unmanaged-disks).</span><span class="sxs-lookup"><span data-stu-id="59c2f-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span></span>

## <a name="use-azure-managed-disks"></a><span data-ttu-id="59c2f-126">Usare Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="59c2f-126">Use Azure Managed Disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="59c2f-127">Collegare un nuovo disco</span><span class="sxs-lookup"><span data-stu-id="59c2f-127">Attach a new disk</span></span>

1. <span data-ttu-id="59c2f-128">Nel pannello **Dischi** fare clic su **+ Add data disk** (+ Aggiungi disco dati).</span><span class="sxs-lookup"><span data-stu-id="59c2f-128">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="59c2f-129">Fare clic sul menu a discesa **Nome** e selezionare **Crea disco**:</span><span class="sxs-lookup"><span data-stu-id="59c2f-129">Click the drop-down menu for **Name** and select **Create disk**:</span></span>

    ![Creare un disco gestito Azure](./media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="59c2f-131">Immettere un nome per il disco gestito.</span><span class="sxs-lookup"><span data-stu-id="59c2f-131">Enter a name for your managed disk.</span></span> <span data-ttu-id="59c2f-132">Esaminare le impostazioni predefinite, aggiornare se necessario e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="59c2f-132">Review the default settings, update as necessary, and then click **Create**.</span></span>
   
   ![Esaminare le impostazioni del disco](./media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="59c2f-134">Fare clic su **Salva** per creare il disco gestito e aggiornare la configurazione della macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="59c2f-134">Click **Save** to create the managed disk and update the VM configuration:</span></span>

   ![Salvare il nuovo disco gestito Azure](./media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="59c2f-136">Dopo che Azure crea il disco e lo collega alla macchina virtuale, il nuovo disco viene elencato nella sezione Impostazioni disco della macchina virtuale in **Dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="59c2f-136">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="59c2f-137">Dal momento che i dischi gestiti sono una risorsa di livello superiore, il disco viene visualizzato nella directory principale del gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="59c2f-137">As managed disks are a top-level resource, the disk appears at the root of the resource group:</span></span>

   ![Disco gestito Azure nel gruppo di risorse](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a><span data-ttu-id="59c2f-139">Collegare un disco esistente</span><span class="sxs-lookup"><span data-stu-id="59c2f-139">Attach an existing disk</span></span>
1. <span data-ttu-id="59c2f-140">Nel pannello **Dischi** fare clic su **+ Add data disk** (+ Aggiungi disco dati).</span><span class="sxs-lookup"><span data-stu-id="59c2f-140">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="59c2f-141">Fare clic sul menu a discesa **Nome** per visualizzare un elenco di dischi gestiti esistenti a cui è possibile accedere con la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="59c2f-141">Click the drop-down menu for **Name** to view a list of existing managed disks accessible to your Azure subscription.</span></span> <span data-ttu-id="59c2f-142">Selezionare il disco gestito da collegare:</span><span class="sxs-lookup"><span data-stu-id="59c2f-142">Select the managed disk to attach:</span></span>

   ![Collegare il disco gestito di Azure](./media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="59c2f-144">Fare clic su **Salva** per collegare il disco gestito esistente e aggiornare la configurazione della macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="59c2f-144">Click **Save** to attach the existing managed disk and update the VM configuration:</span></span>
   
   ![Salvare gli aggiornamenti del disco gestito Azure](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="59c2f-146">Dopo che Azure collega il disco alla macchina virtuale, esso viene elencato nella sezione Impostazioni disco della macchina virtuale in **Dischi dei dati**.</span><span class="sxs-lookup"><span data-stu-id="59c2f-146">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-unmanaged-disks"></a><span data-ttu-id="59c2f-147">Usare i dischi non gestiti</span><span class="sxs-lookup"><span data-stu-id="59c2f-147">Use unmanaged disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="59c2f-148">Collegare un nuovo disco</span><span class="sxs-lookup"><span data-stu-id="59c2f-148">Attach a new disk</span></span>

1. <span data-ttu-id="59c2f-149">Nel pannello **Dischi** fare clic su **+ Add data disk** (+ Aggiungi disco dati).</span><span class="sxs-lookup"><span data-stu-id="59c2f-149">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="59c2f-150">Esaminare le impostazioni predefinite, aggiornare se necessario e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="59c2f-150">Review the default settings, update as necessary, and then click **OK**.</span></span>
   
   ![Esaminare le impostazioni del disco](./media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="59c2f-152">Dopo che Azure crea il disco e lo collega alla macchina virtuale, il nuovo disco viene elencato nella sezione Impostazioni disco della macchina virtuale in **Dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="59c2f-152">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="59c2f-153">Collegare un disco esistente</span><span class="sxs-lookup"><span data-stu-id="59c2f-153">Attach an existing disk</span></span>
1. <span data-ttu-id="59c2f-154">Nel pannello **Dischi** fare clic su **+ Add data disk** (+ Aggiungi disco dati).</span><span class="sxs-lookup"><span data-stu-id="59c2f-154">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="59c2f-155">In **Collega un disco esistente** fare clic su **File VHD**.</span><span class="sxs-lookup"><span data-stu-id="59c2f-155">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![Collegare un disco esistente](./media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="59c2f-157">In **Account di archiviazione**, selezionare l'account e un contenitore che contiene il file con estensione vhd.</span><span class="sxs-lookup"><span data-stu-id="59c2f-157">Under **Storage accounts**, select the account and container that holds the .vhd file.</span></span>
   
   ![Individuare il percorso di un VHD](./media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="59c2f-159">Selezionare il file con estensione vhd.</span><span class="sxs-lookup"><span data-stu-id="59c2f-159">Select the .vhd file.</span></span>
5. <span data-ttu-id="59c2f-160">In **Collega un disco esistente** il file appena selezionato è elencato in **File VHD**.</span><span class="sxs-lookup"><span data-stu-id="59c2f-160">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="59c2f-161">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="59c2f-161">Click **OK**.</span></span>
6. <span data-ttu-id="59c2f-162">Dopo che Azure collega il disco alla macchina virtuale, esso viene elencato nella sezione Impostazioni disco della macchina virtuale in **Dischi dei dati**.</span><span class="sxs-lookup"><span data-stu-id="59c2f-162">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="59c2f-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="59c2f-163">Next steps</span></span>
<span data-ttu-id="59c2f-164">Dopo aver aggiunto il disco, è necessario prepararlo per l'uso.</span><span class="sxs-lookup"><span data-stu-id="59c2f-164">After the disk is added, you need to prepare it for use.</span></span> <span data-ttu-id="59c2f-165">Per ulteriori informazioni, vedere [Procedura: inizializzare un nuovo disco dati in Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="59c2f-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span></span>
