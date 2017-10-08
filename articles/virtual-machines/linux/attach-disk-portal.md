---
title: aaaAttach un tooa disco dati VM Linux | Documenti Microsoft
description: Tooattach dati nuovi o esistenti disco tooa VM Linux in Azure mediante portale hello hello come modello di distribuzione di gestione risorse.
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
ms.openlocfilehash: 069c3c6f5e71a8c495342e6d0c6f3d92c4ed5053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-vm-in-hello-azure-portal"></a><span data-ttu-id="8f025-103">Funzionamento dei dischi tooa VM Linux nel portale di Azure hello tooattach un tipo di dati</span><span class="sxs-lookup"><span data-stu-id="8f025-103">How tooattach a data disk tooa Linux VM in hello Azure portal</span></span>
<span data-ttu-id="8f025-104">Questo articolo illustra come tooattach sia nuovi che esistenti dischi di macchina virtuale di Linux tooa tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f025-104">This article shows you how tooattach both new and existing disks tooa Linux virtual machine through hello Azure portal.</span></span> <span data-ttu-id="8f025-105">È anche possibile [collegare un tooa di disco dati macchina virtuale di Windows nel portale di Azure hello](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f025-105">You can also [attach a data disk tooa Windows VM in hello Azure portal](../windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="8f025-106">È possibile scegliere toouse entrambi i dischi di Azure gestiti o non gestito di dischi.</span><span class="sxs-lookup"><span data-stu-id="8f025-106">You can choose toouse either Azure Managed Disks or unmanaged disks.</span></span> <span data-ttu-id="8f025-107">Dischi gestiti vengono gestiti dal hello piattaforma Azure e non richiedono alcun toostore preparazione o percorso li.</span><span class="sxs-lookup"><span data-stu-id="8f025-107">Managed disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="8f025-108">I dischi non gestiti richiedono un account di archiviazione e presentano alcune [quote e limiti applicati](../../azure-subscription-service-limits.md#storage-limits).</span><span class="sxs-lookup"><span data-stu-id="8f025-108">Unmanaged disks require a storage account and have some [quotas and limits that apply](../../azure-subscription-service-limits.md#storage-limits).</span></span> <span data-ttu-id="8f025-109">Per altre informazioni su Azure Managed Disks, vedere [Azure Managed Disks overview](../windows/managed-disks-overview.md) (Panoramica di Azure Managed Disks).</span><span class="sxs-lookup"><span data-stu-id="8f025-109">For more information about Azure Managed Disks, see [Azure Managed Disks overview](../windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="8f025-110">Prima di collegare i dischi tooyour VM, esaminare i seguenti suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="8f025-110">Before you attach disks tooyour VM, review these tips:</span></span>

* <span data-ttu-id="8f025-111">dimensioni di Hello della macchina virtuale hello controlla il numero di dischi dati è possibile collegare.</span><span class="sxs-lookup"><span data-stu-id="8f025-111">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="8f025-112">Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f025-112">For details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="8f025-113">toouse archiviazione Premium, è necessario una macchina virtuale serie DS o GS-series.</span><span class="sxs-lookup"><span data-stu-id="8f025-113">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="8f025-114">Con queste macchine virtuali, è possibile usare dischi Premium e Standard.</span><span class="sxs-lookup"><span data-stu-id="8f025-114">You can use both Premium and Standard disks with these virtual machines.</span></span> <span data-ttu-id="8f025-115">L’archiviazione Premium è disponibile solo in determinate aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="8f025-115">Premium storage is available in certain regions.</span></span> <span data-ttu-id="8f025-116">Per ulteriori informazioni, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f025-116">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="8f025-117">I dischi collegati toovirtual macchine sono effettivamente i file con estensione vhd archiviati in Azure.</span><span class="sxs-lookup"><span data-stu-id="8f025-117">Disks attached toovirtual machines are actually .vhd files stored in Azure.</span></span> <span data-ttu-id="8f025-118">Per informazioni dettagliate, vedere [Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f025-118">For details, see [About disks and VHDs for virtual machines](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="8f025-119">Trovare la macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="8f025-119">Find hello virtual machine</span></span>
1. <span data-ttu-id="8f025-120">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8f025-120">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8f025-121">Nel menu Hub hello, fare clic su **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="8f025-121">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="8f025-122">Selezionare macchina virtuale hello hello elenco.</span><span class="sxs-lookup"><span data-stu-id="8f025-122">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="8f025-123">toohello virtuale macchine pannello **Essentials**, fare clic su **dischi**.</span><span class="sxs-lookup"><span data-stu-id="8f025-123">toohello Virtual machines blade, in **Essentials**, click **Disks**.</span></span>
   
    ![Aprire le impostazioni del disco](./media/attach-disk-portal/find-disk-settings.png)

<span data-ttu-id="8f025-125">Continuare seguendo le istruzioni per il collegamento di un [disco gestito](#use-azure-managed-disks) o di un [disco non gestito](#use-unmanaged-disks).</span><span class="sxs-lookup"><span data-stu-id="8f025-125">Continue by following instructions for attaching either a [managed disk](#use-azure-managed-disks) or [unmanaged disk](#use-unmanaged-disks).</span></span>

## <a name="use-azure-managed-disks"></a><span data-ttu-id="8f025-126">Usare Azure Managed Disks</span><span class="sxs-lookup"><span data-stu-id="8f025-126">Use Azure Managed Disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="8f025-127">Collegare un nuovo disco</span><span class="sxs-lookup"><span data-stu-id="8f025-127">Attach a new disk</span></span>

1. <span data-ttu-id="8f025-128">In hello **dischi** pannello, fare clic su **+ Aggiungi disco di dati**.</span><span class="sxs-lookup"><span data-stu-id="8f025-128">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="8f025-129">Fare clic sul menu a discesa hello **nome** e selezionare **Crea disco**:</span><span class="sxs-lookup"><span data-stu-id="8f025-129">Click hello drop-down menu for **Name** and select **Create disk**:</span></span>

    ![Creare un disco gestito Azure](./media/attach-disk-portal/create-new-md.png)

3. <span data-ttu-id="8f025-131">Immettere un nome per il disco gestito.</span><span class="sxs-lookup"><span data-stu-id="8f025-131">Enter a name for your managed disk.</span></span> <span data-ttu-id="8f025-132">Esaminare le impostazioni predefinite di hello, aggiornare, se necessario e quindi fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="8f025-132">Review hello default settings, update as necessary, and then click **Create**.</span></span>
   
   ![Esaminare le impostazioni del disco](./media/attach-disk-portal/create-new-md-settings.png)

4. <span data-ttu-id="8f025-134">Fare clic su **salvare** toocreate hello gestiti disco e aggiornamento configurazione della macchina virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="8f025-134">Click **Save** toocreate hello managed disk and update hello VM configuration:</span></span>

   ![Salvare il nuovo disco gestito Azure](./media/attach-disk-portal/confirm-create-new-md.png)

5. <span data-ttu-id="8f025-136">Dopo che Azure crea un disco hello e lo collega macchina virtuale toohello, nuovo disco hello è elencato nelle impostazioni del disco della macchina virtuale hello in **dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="8f025-136">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span> <span data-ttu-id="8f025-137">I dischi gestiti sono una risorsa di primo livello e disco hello viene visualizzato nella radice di hello hello del gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="8f025-137">As managed disks are a top-level resource, hello disk appears at hello root of hello resource group:</span></span>

   ![Disco gestito Azure nel gruppo di risorse](./media/attach-disk-portal/view-md-resource-group.png)

### <a name="attach-an-existing-disk"></a><span data-ttu-id="8f025-139">Collegare un disco esistente</span><span class="sxs-lookup"><span data-stu-id="8f025-139">Attach an existing disk</span></span>
1. <span data-ttu-id="8f025-140">In hello **dischi** pannello, fare clic su **+ Aggiungi disco di dati**.</span><span class="sxs-lookup"><span data-stu-id="8f025-140">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="8f025-141">Fare clic sul menu a discesa hello **nome** tooview un elenco esistente gestito dischi accessibili tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8f025-141">Click hello drop-down menu for **Name** tooview a list of existing managed disks accessible tooyour Azure subscription.</span></span> <span data-ttu-id="8f025-142">Seleziona hello gestito tooattach disco:</span><span class="sxs-lookup"><span data-stu-id="8f025-142">Select hello managed disk tooattach:</span></span>

   ![Collegare il disco gestito di Azure](./media/attach-disk-portal/select-existing-md.png)

3. <span data-ttu-id="8f025-144">Fare clic su **salvare** tooattach hello esistenti gestiti disco e aggiornamento configurazione della macchina virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="8f025-144">Click **Save** tooattach hello existing managed disk and update hello VM configuration:</span></span>
   
   ![Salvare gli aggiornamenti del disco gestito Azure](./media/attach-disk-portal/confirm-attach-existing-md.png)

4. <span data-ttu-id="8f025-146">Dopo il collega Azure hello macchina virtuale di toohello disco, viene elencata per le impostazioni del disco della macchina virtuale hello in **dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="8f025-146">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-unmanaged-disks"></a><span data-ttu-id="8f025-147">Usare i dischi non gestiti</span><span class="sxs-lookup"><span data-stu-id="8f025-147">Use unmanaged disks</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="8f025-148">Collegare un nuovo disco</span><span class="sxs-lookup"><span data-stu-id="8f025-148">Attach a new disk</span></span>

1. <span data-ttu-id="8f025-149">In hello **dischi** pannello, fare clic su **+ Aggiungi disco di dati**.</span><span class="sxs-lookup"><span data-stu-id="8f025-149">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="8f025-150">Esaminare le impostazioni predefinite di hello, aggiornare, se necessario e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f025-150">Review hello default settings, update as necessary, and then click **OK**.</span></span>
   
   ![Esaminare le impostazioni del disco](./media/attach-disk-portal/attach-new.png)
3. <span data-ttu-id="8f025-152">Dopo che Azure crea un disco hello e lo collega macchina virtuale toohello, nuovo disco hello è elencato nelle impostazioni del disco della macchina virtuale hello in **dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="8f025-152">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="8f025-153">Collegare un disco esistente</span><span class="sxs-lookup"><span data-stu-id="8f025-153">Attach an existing disk</span></span>
1. <span data-ttu-id="8f025-154">In hello **dischi** pannello, fare clic su **+ Aggiungi disco di dati**.</span><span class="sxs-lookup"><span data-stu-id="8f025-154">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="8f025-155">In **Collega un disco esistente** fare clic su **File VHD**.</span><span class="sxs-lookup"><span data-stu-id="8f025-155">Under **Attach existing disk**, click **VHD File**.</span></span>
   
   ![Collegare un disco esistente](./media/attach-disk-portal/attach-existing.png)
3. <span data-ttu-id="8f025-157">In **gli account di archiviazione**, selezionare account hello e contenitore che include i file con estensione vhd hello.</span><span class="sxs-lookup"><span data-stu-id="8f025-157">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>
   
   ![Individuare il percorso di un VHD](./media/attach-disk-portal/find-storage-container.png)
4. <span data-ttu-id="8f025-159">Selezionare i file con estensione vhd hello.</span><span class="sxs-lookup"><span data-stu-id="8f025-159">Select hello .vhd file.</span></span>
5. <span data-ttu-id="8f025-160">In **collegare un disco esistente**, file hello appena selezionata è elencato in **File VHD**.</span><span class="sxs-lookup"><span data-stu-id="8f025-160">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="8f025-161">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f025-161">Click **OK**.</span></span>
6. <span data-ttu-id="8f025-162">Dopo il collega Azure hello macchina virtuale di toohello disco, viene elencata per le impostazioni del disco della macchina virtuale hello in **dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="8f025-162">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8f025-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8f025-163">Next steps</span></span>
<span data-ttu-id="8f025-164">Dopo aver aggiunto il disco di hello, è necessario tooprepare l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="8f025-164">After hello disk is added, you need tooprepare it for use.</span></span> <span data-ttu-id="8f025-165">Per ulteriori informazioni, vedere [Procedura: inizializzare un nuovo disco dati in Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="8f025-165">For more information, see [How to: Initialize a new data disk in Linux](add-disk.md).</span></span>
