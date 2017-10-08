---
title: aaaAttach tooa un disco di dati non gestiti - macchina virtuale di Windows Azure | Documenti Microsoft
description: Tooattach nuovo o esistente dati non gestiti disco tooa macchina virtuale Windows in Azure mediante portale hello hello come modello di distribuzione di gestione risorse.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="58cd2-103">Funzionamento dei dischi tooa macchina virtuale di Windows nel portale di Azure hello tooattach un dati non gestiti</span><span class="sxs-lookup"><span data-stu-id="58cd2-103">How tooattach an unmanaged data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="58cd2-104">Questo articolo illustra come non gestito tooattach sia nuovi che esistenti dischi tooWindows le macchine virtuali tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="58cd2-104">This article shows you how tooattach both new and existing unmanaged disks tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="58cd2-105">È anche possibile [collegare un disco dati usando PowerShell](./attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="58cd2-105">You can also [attach a data disk using PowerShell](./attach-disk-ps.md).</span></span> <span data-ttu-id="58cd2-106">Prima di procedere, rivedere i suggerimenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="58cd2-106">Before you do this, review these tips:</span></span>

* <span data-ttu-id="58cd2-107">dimensioni di Hello della macchina virtuale hello controlla il numero di dischi dati è possibile collegare.</span><span class="sxs-lookup"><span data-stu-id="58cd2-107">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="58cd2-108">Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="58cd2-108">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="58cd2-109">toouse archiviazione Premium, è necessario una macchina virtuale serie DS o GS-series.</span><span class="sxs-lookup"><span data-stu-id="58cd2-109">toouse Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="58cd2-110">È possibile utilizzare dischi dagli account di archiviazione sia Premium che Standard con queste macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="58cd2-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="58cd2-111">L’archiviazione Premium è disponibile solo in determinate aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="58cd2-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="58cd2-112">Per ulteriori informazioni, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58cd2-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="58cd2-113">Per un nuovo disco, non è necessario toocreate è primo poiché Azure crea momento del collegamento.</span><span class="sxs-lookup"><span data-stu-id="58cd2-113">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>


<span data-ttu-id="58cd2-114">È anche possibile [collegare un disco dati usando Powershell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="58cd2-114">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>


## <a name="find-hello-virtual-machine"></a><span data-ttu-id="58cd2-115">Trovare la macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="58cd2-115">Find hello virtual machine</span></span>
1. <span data-ttu-id="58cd2-116">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="58cd2-116">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="58cd2-117">Dal menu hello hello sinistra, fare clic su **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="58cd2-117">In hello menu on hello left, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="58cd2-118">Selezionare macchina virtuale hello hello elenco.</span><span class="sxs-lookup"><span data-stu-id="58cd2-118">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="58cd2-119">Nel pannello macchine virtuali di hello, fare clic su **dischi**.</span><span class="sxs-lookup"><span data-stu-id="58cd2-119">In hello Virtual machines blade, click **Disks**.</span></span>
   
<span data-ttu-id="58cd2-120">Continuare seguendo le istruzioni per il collegamento di un [nuovo disco](#option-1-attach-a-new-disk) o un [disco esistente](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="58cd2-120">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="58cd2-121">Opzione 1: Connettere e inizializzare un nuovo disco</span><span class="sxs-lookup"><span data-stu-id="58cd2-121">Option 1: Attach and initialize a new disk</span></span>
1. <span data-ttu-id="58cd2-122">In hello **dischi** pannello, fare clic su **+ Aggiungi disco di dati**.</span><span class="sxs-lookup"><span data-stu-id="58cd2-122">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="58cd2-123">In hello **collega disco gestito** pannello, digitare un nome per il disco hello in **nome** e quindi selezionare **New (disco vuoto)** in **tipo di origine**.</span><span class="sxs-lookup"><span data-stu-id="58cd2-123">In hello **Attach managed disk** blade, type a name for hello disk in **Name** and then select **New (empty disk)** in **Source type**.</span></span>
3. <span data-ttu-id="58cd2-124">In **contenitore di archiviazione**, fare clic su hello **Sfoglia** pulsante ed esplorare toohello account di archiviazione e contenitore in cui desideri hello nuovo disco rigido virtuale toobe archiviati e quindi fare clic su **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="58cd2-124">Under **Storage container**, click hello **Browse** button and browse toohello storage account and container where you would like hello new VHD toobe stored and then click **Select**.</span></span> 
  
   ![Esaminare le impostazioni del disco](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. <span data-ttu-id="58cd2-126">Una volta con impostazioni hello per disco dati hello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="58cd2-126">When you are done with hello settings for hello data disk, click **OK**.</span></span>
4. <span data-ttu-id="58cd2-127">In hello **dischi** pannello, fare clic su **salvare** configurazione della macchina virtuale toohello tooadd hello disco.</span><span class="sxs-lookup"><span data-stu-id="58cd2-127">Back in hello **Disks** blade, click **Save** tooadd hello disk toohello VM configuration.</span></span>


### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="58cd2-128">Inizializzare un nuovo disco dati</span><span class="sxs-lookup"><span data-stu-id="58cd2-128">Initialize a new data disk</span></span>

1. <span data-ttu-id="58cd2-129">Connessione macchina virtuale toohello.</span><span class="sxs-lookup"><span data-stu-id="58cd2-129">Connect toohello virtual machine.</span></span> <span data-ttu-id="58cd2-130">Per istruzioni, vedere [come tooconnect e tooan virtuali di Azure di accesso del computer che eseguono Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58cd2-130">For instructions, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
1. <span data-ttu-id="58cd2-131">Fare clic su hello **avviare** menu all'interno di hello VM e tipo **diskmgmt.msc** e fare clic su **invio**.</span><span class="sxs-lookup"><span data-stu-id="58cd2-131">Click hello **Start** menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="58cd2-132">Verrà avviato lo snap-in Gestione disco hello.</span><span class="sxs-lookup"><span data-stu-id="58cd2-132">This starts hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="58cd2-133">Gestione disco riconosce che si disponga di un disco non inizializzato e si aprirà la finestra Inizializza disco hello.</span><span class="sxs-lookup"><span data-stu-id="58cd2-133">Disk Management recognizes that you have a new, uninitialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="58cd2-134">Assicurarsi che sia selezionato il nuovo disco di hello e fare clic su **OK** tooinitialize è.</span><span class="sxs-lookup"><span data-stu-id="58cd2-134">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="58cd2-135">Hello nuovo disco verrà visualizzato come **non allocato**.</span><span class="sxs-lookup"><span data-stu-id="58cd2-135">hello new disk now appears as **unallocated**.</span></span> <span data-ttu-id="58cd2-136">Fare clic sul disco hello e selezionare **nuovo volume semplice**.</span><span class="sxs-lookup"><span data-stu-id="58cd2-136">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="58cd2-137">Hello **semplice creazione guidata nuovo Volume** viene avviato.</span><span class="sxs-lookup"><span data-stu-id="58cd2-137">hello **New Simple Volume Wizard** starts.</span></span>
5. <span data-ttu-id="58cd2-138">Seguire i passaggi guidata hello, mantenendo tutti i valori predefiniti di hello, al termine selezionare **fine**.</span><span class="sxs-lookup"><span data-stu-id="58cd2-138">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="58cd2-139">Chiudere Gestione disco.</span><span class="sxs-lookup"><span data-stu-id="58cd2-139">Close Disk Management.</span></span>
7. <span data-ttu-id="58cd2-140">È possibile utilizzare una finestra popup che è necessario nuovo disco di tooformat hello prima che sia possibile utilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="58cd2-140">You get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="58cd2-141">Fare clic su **Formatta disco**.</span><span class="sxs-lookup"><span data-stu-id="58cd2-141">Click **Format disk**.</span></span>
8. <span data-ttu-id="58cd2-142">In hello **nuovo disco in formato** finestra di dialogo, controllare le impostazioni di hello e quindi fare clic su **avviare**.</span><span class="sxs-lookup"><span data-stu-id="58cd2-142">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="58cd2-143">Visualizzato un avviso che la formattazione di dischi hello Cancella tutti i dati di hello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="58cd2-143">You get a warning that formatting hello disks erases all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="58cd2-144">Una volta completato il formato di hello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="58cd2-144">When hello format is complete, click **OK**.</span></span>


## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="58cd2-145">Opzione 2: Collegare un disco esistente</span><span class="sxs-lookup"><span data-stu-id="58cd2-145">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="58cd2-146">In hello **dischi** pannello, fare clic su **+ Aggiungi disco di dati**.</span><span class="sxs-lookup"><span data-stu-id="58cd2-146">On hello **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="58cd2-147">In hello **collega disco non gestito** pannello, in **tipo di origine** selezionare **blob esistente**.</span><span class="sxs-lookup"><span data-stu-id="58cd2-147">On hello **Attach unmanaged disk** blade, in **Source type** select **Existing blob**.</span></span>

    ![Esaminare le impostazioni del disco](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. <span data-ttu-id="58cd2-149">Fare clic su **Sfoglia** toonavigate toohello account di archiviazione e contenitore hello disco rigido virtuale esistente in cui si trova.</span><span class="sxs-lookup"><span data-stu-id="58cd2-149">Click **Browse** toonavigate toohello storage account and container where hello existing VHD is located.</span></span> <span data-ttu-id="58cd2-150">Fare clic su hello disco rigido virtuale e quindi fare clic su **selezionare**.</span><span class="sxs-lookup"><span data-stu-id="58cd2-150">Click and hello VHD and then click **Select**.</span></span>
4. <span data-ttu-id="58cd2-151">Fare clic su **OK** in hello **collega disco non gestito** blade.</span><span class="sxs-lookup"><span data-stu-id="58cd2-151">Click **OK** in hello **Attach unmanaged disk** blade.</span></span>
5. <span data-ttu-id="58cd2-152">In hello **dischi** pannello, fare clic su **salvare** configurazione toohello del disco hello tooadd per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="58cd2-152">In hello **Disks** blade, click **Save** tooadd hello disk toohello configuration for hello VM.</span></span>
   


## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="58cd2-153">Usare TRIM con l'archiviazione Standard</span><span class="sxs-lookup"><span data-stu-id="58cd2-153">Use TRIM with standard storage</span></span>

<span data-ttu-id="58cd2-154">Se si usa l'archiviazione Standard (HDD), è consigliabile abilitare TRIM.</span><span class="sxs-lookup"><span data-stu-id="58cd2-154">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="58cd2-155">TRIM rimuove i blocchi inutilizzati nel disco hello in modo verrà addebitato solo per l'archiviazione che stiano effettivamente usando.</span><span class="sxs-lookup"><span data-stu-id="58cd2-155">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="58cd2-156">In questo modo è possibile risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.</span><span class="sxs-lookup"><span data-stu-id="58cd2-156">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="58cd2-157">È possibile eseguire questo comando toocheck hello TRIM impostare.</span><span class="sxs-lookup"><span data-stu-id="58cd2-157">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="58cd2-158">Aprire un prompt dei comandi nella macchina virtuale Windows e digitare:</span><span class="sxs-lookup"><span data-stu-id="58cd2-158">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="58cd2-159">Se il comando hello restituisce 0, l'ottimizzazione TRIM è abilitato correttamente.</span><span class="sxs-lookup"><span data-stu-id="58cd2-159">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="58cd2-160">Se viene restituito 1, eseguire hello tooenable comando TRIM seguenti:</span><span class="sxs-lookup"><span data-stu-id="58cd2-160">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="58cd2-161">Dopo l'eliminazione di dati dal disco, è possibile garantire scaricamento correttamente eseguendo le operazioni TRIM hello deframmentazione con TRIM:</span><span class="sxs-lookup"><span data-stu-id="58cd2-161">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="58cd2-162">È inoltre possibile garantire l'intero volume hello viene ritagliato formattando volume hello.</span><span class="sxs-lookup"><span data-stu-id="58cd2-162">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>


## <a name="next-steps"></a><span data-ttu-id="58cd2-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="58cd2-163">Next steps</span></span>
<span data-ttu-id="58cd2-164">Se l'applicazione necessita di dati di toostore unità d: hello toouse, è possibile [modificare hello lettera di unità del disco temporaneo di Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58cd2-164">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

