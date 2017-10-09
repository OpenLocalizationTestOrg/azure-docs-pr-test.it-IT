---
title: aaaAttach tooa un disco macchina virtuale di Azure classico | Documenti Microsoft
description: Collegare una macchina virtuale di Windows di dati su disco tooa creata con il modello di distribuzione classica hello e inizializzarlo.
services: virtual-machines-windows, storage
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: be4e3e74-05bc-4527-969f-84f10a1d66a7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: cynthn
ms.openlocfilehash: bfe1b0fa066277d28d3862a18da4b1023cb4452d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="attach-a-data-disk-tooa-windows-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="8a2e2-103">Collegare una macchina virtuale di Windows di dati su disco tooa creata con il modello di distribuzione classica hello</span><span class="sxs-lookup"><span data-stu-id="8a2e2-103">Attach a data disk tooa Windows virtual machine created with hello classic deployment model</span></span>
<!--
Refernce article:
    If you want toouse hello new portal, see [How tooattach a data disk tooa Windows VM in hello Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="8a2e2-104">In questo articolo viene illustrato come creare i dischi nuovi ed esistenti tooattach con hello Classic distribuzione modello tooa macchina virtuale Windows usando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-104">This article shows you how tooattach new and existing disks created with hello Classic deployment model tooa Windows virtual machine using hello Azure portal.</span></span>

<span data-ttu-id="8a2e2-105">È anche possibile [collegare un tooa di disco dati VM Linux nel portale di Azure hello](../../linux/attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8a2e2-105">You can also [attach a data disk tooa Linux VM in hello Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="8a2e2-106">Prima di collegare un disco, esaminare i seguenti suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="8a2e2-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="8a2e2-107">dimensioni di Hello della macchina virtuale hello controlla il numero di dischi dati è possibile collegare.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="8a2e2-108">Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8a2e2-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="8a2e2-109">toouse archiviazione Premium, è necessario una macchina virtuale serie DS o GS-series.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="8a2e2-110">È possibile utilizzare dischi dagli account di archiviazione sia Premium che Standard con queste macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="8a2e2-111">L’archiviazione Premium è disponibile solo in determinate aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="8a2e2-112">Per ulteriori informazioni, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8a2e2-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="8a2e2-113">Per un nuovo disco, non è necessario toocreate è primo poiché Azure crea momento del collegamento.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="8a2e2-114">È anche possibile [collegare un disco dati usando Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8a2e2-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8a2e2-115">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8a2e2-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-hello-virtual-machine"></a><span data-ttu-id="8a2e2-116">Trovare la macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="8a2e2-116">Find hello virtual machine</span></span>
1. <span data-ttu-id="8a2e2-117">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8a2e2-117">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8a2e2-118">Macchina virtuale selezionare hello dalla risorsa hello elencato nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-118">Select hello virtual machine from hello resource listed on hello dashboard.</span></span>
3. <span data-ttu-id="8a2e2-119">Nel riquadro sinistro di hello in **impostazioni**, fare clic su **dischi**.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-119">In hello left pane under **Settings**, click **Disks**.</span></span>

    ![Aprire le impostazioni del disco](./media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="8a2e2-121">Continuare seguendo le istruzioni per il collegamento di un [nuovo disco](#option-1-attach-a-new-disk) o un [disco esistente](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="8a2e2-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="8a2e2-122">Opzione 1: Connettere e inizializzare un nuovo disco</span><span class="sxs-lookup"><span data-stu-id="8a2e2-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="8a2e2-123">In hello **dischi** pannello, fare clic su **nuovo collegamento**.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-123">On hello **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="8a2e2-124">Esaminare le impostazioni predefinite di hello, aggiornare, se necessario e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-124">Review hello default settings, update as necessary, and then click **OK**.</span></span>

   ![Esaminare le impostazioni del disco](./media/attach-disk/attach-new.png)

3. <span data-ttu-id="8a2e2-126">Dopo che Azure crea un disco hello e lo collega macchina virtuale toohello, nuovo disco hello è elencato nelle impostazioni del disco della macchina virtuale hello in **dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-126">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="8a2e2-127">Inizializzare un nuovo disco dati</span><span class="sxs-lookup"><span data-stu-id="8a2e2-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="8a2e2-128">Connessione macchina virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-128">Connect toohello virtual machine.</span></span> <span data-ttu-id="8a2e2-129">Per istruzioni, vedere [come tooconnect e tooan virtuali di Azure di accesso del computer che eseguono Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8a2e2-129">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="8a2e2-130">Dopo aver effettuato sulla macchina virtuale toohello, aprire **Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-130">After you log on toohello virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="8a2e2-131">Nel riquadro sinistro hello selezionare **servizi File e archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-131">In hello left pane, select **File and Storage Services**.</span></span>

    ![Avviare Server Manager](../media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="8a2e2-133">Selezionare **Dischi**.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-133">Select **Disks**.</span></span>
4. <span data-ttu-id="8a2e2-134">Hello **dischi** sezione sono elencati i dischi di hello.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-134">hello **Disks** section lists hello disks.</span></span> <span data-ttu-id="8a2e2-135">Nella maggior parte dei casi, avrà disco 0, disco 1 e disco 2.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="8a2e2-136">Disco 0 è il disco di sistema operativo hello, disco 1 è disco temporaneo hello e disco 2 è disco dati hello appena collegati macchina virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-136">Disk 0 is hello operating system disk, disk 1 is hello temporary disk, and disk 2 is hello data disk newly attached toohello virtual machine.</span></span> <span data-ttu-id="8a2e2-137">elenchi di disco dati Hello hello partizione come **sconosciuto**.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-137">hello data disk lists hello Partition as **Unknown**.</span></span>

 <span data-ttu-id="8a2e2-138">Fare doppio clic su disco hello e selezionare **inizializzare**.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-138">Right-click hello disk and select **Initialize**.</span></span>

5. <span data-ttu-id="8a2e2-139">Si è inviata una notifica che tutti i dati verranno cancellati quando viene inizializzato il disco di hello.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-139">You're notified that all data will be erased when hello disk is initialized.</span></span> <span data-ttu-id="8a2e2-140">Fare clic su **Sì** tooacknowledge hello avviso e inizializzare hello su disco.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-140">Click **Yes** tooacknowledge hello warning and initialize hello disk.</span></span> <span data-ttu-id="8a2e2-141">Al termine dell'operazione, verrà indicata come partizione hello **GPT**.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-141">Once complete, hello partition will be listed as **GPT**.</span></span> <span data-ttu-id="8a2e2-142">Fare nuovamente doppio clic su disco hello e selezionare **nuovo Volume**.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-142">Right-click hello disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="8a2e2-143">Completare Creazione guidata hello utilizzando i valori predefiniti di hello.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-143">Complete hello wizard using hello default values.</span></span> <span data-ttu-id="8a2e2-144">Quando viene eseguito la procedura guidata hello, hello **volumi** sezione sono elencati nuovo volume hello.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-144">When hello wizard is done, hello **Volumes** section lists hello new volume.</span></span> <span data-ttu-id="8a2e2-145">disco Hello è online e pronto toostore dati.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-145">hello disk is now online and ready toostore data.</span></span>

    ![Inizializzazione del volume completata](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="8a2e2-147">Opzione 2: Collegare un disco esistente</span><span class="sxs-lookup"><span data-stu-id="8a2e2-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="8a2e2-148">In hello **dischi** pannello, fare clic su **collegamento esistente**.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-148">On hello **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="8a2e2-149">In **Collega un disco esistente** fare clic su **Posizione**.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![Collegare un disco esistente](./media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="8a2e2-151">In **gli account di archiviazione**, selezionare account hello e contenitore che include i file con estensione vhd hello.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-151">Under **Storage accounts**, select hello account and container that holds hello .vhd file.</span></span>

   ![Individuare il percorso di un VHD](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="8a2e2-153">Selezionare i file con estensione vhd hello.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-153">Select hello .vhd file.</span></span>
5. <span data-ttu-id="8a2e2-154">In **collegare un disco esistente**, file hello appena selezionata è elencato in **File VHD**.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-154">Under **Attach existing disk**, hello file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="8a2e2-155">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-155">Click **OK**.</span></span>
6. <span data-ttu-id="8a2e2-156">Dopo il collega Azure hello macchina virtuale di toohello disco, viene elencata per le impostazioni del disco della macchina virtuale hello in **dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-156">After Azure attaches hello disk toohello virtual machine, it's listed in hello virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="8a2e2-157">Usare TRIM con l'archiviazione Standard</span><span class="sxs-lookup"><span data-stu-id="8a2e2-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="8a2e2-158">Se si usa l'archiviazione Standard (HDD), è consigliabile abilitare TRIM.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="8a2e2-159">TRIM rimuove i blocchi inutilizzati nel disco hello in modo verrà addebitato solo per l'archiviazione che stiano effettivamente usando.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-159">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="8a2e2-160">L'uso di TRIM consente di risparmiare sui costi, inclusi i blocchi inutilizzati risultanti dall'eliminazione di file di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="8a2e2-161">È possibile eseguire questo comando toocheck hello TRIM impostare.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-161">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="8a2e2-162">Aprire un prompt dei comandi nella macchina virtuale Windows e digitare:</span><span class="sxs-lookup"><span data-stu-id="8a2e2-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="8a2e2-163">Se il comando hello restituisce 0, l'ottimizzazione TRIM è abilitato correttamente.</span><span class="sxs-lookup"><span data-stu-id="8a2e2-163">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="8a2e2-164">Se viene restituito 1, eseguire hello tooenable comando TRIM seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a2e2-164">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="8a2e2-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a2e2-165">Next steps</span></span>
<span data-ttu-id="8a2e2-166">Se l'applicazione necessita di dati di toostore unità d: hello toouse, è possibile [modificare hello lettera di unità del disco temporaneo di Windows hello](../../virtual-machines-windows-change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="8a2e2-166">If your application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a2e2-167">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="8a2e2-167">Additional resources</span></span>
[<span data-ttu-id="8a2e2-168">Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="8a2e2-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)
