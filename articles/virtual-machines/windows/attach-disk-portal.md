---
title: Collegare un disco dati non gestito a una macchina virtuale Windows - Azure | Microsoft Docs
description: Come collegare un disco dati non gestito nuovo o esistente a una macchina virtuale Windows nel portale di Azure tramite il modello di distribuzione di Resource Manager.
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
ms.openlocfilehash: c0886302c82641f8cc1a00d3972870d58ba8afb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-an-unmanaged-data-disk-to-a-windows-vm-in-the-azure-portal"></a><span data-ttu-id="95fc3-103">Collegare un disco dati non gestito a una macchina virtuale Windows nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="95fc3-103">How to attach an unmanaged data disk to a Windows VM in the Azure portal</span></span>

<span data-ttu-id="95fc3-104">Questo articolo illustra come collegare dischi non gestiti nuovi o esistenti a una macchina virtuale Windows tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="95fc3-104">This article shows you how to attach both new and existing unmanaged disks to Windows virtual machines through the Azure portal.</span></span> <span data-ttu-id="95fc3-105">È anche possibile [collegare un disco dati usando PowerShell](./attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="95fc3-105">You can also [attach a data disk using PowerShell](./attach-disk-ps.md).</span></span> <span data-ttu-id="95fc3-106">Prima di procedere, rivedere i suggerimenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="95fc3-106">Before you do this, review these tips:</span></span>

* <span data-ttu-id="95fc3-107">La dimensione della macchina virtuale controlla il numero di dischi dati che è possibile collegare.</span><span class="sxs-lookup"><span data-stu-id="95fc3-107">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="95fc3-108">Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="95fc3-108">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="95fc3-109">Per usare l'archiviazione Premium, è necessaria una macchina virtuale della serie DS o GS.</span><span class="sxs-lookup"><span data-stu-id="95fc3-109">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="95fc3-110">È possibile utilizzare dischi dagli account di archiviazione sia Premium che Standard con queste macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="95fc3-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="95fc3-111">L’archiviazione Premium è disponibile solo in determinate aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="95fc3-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="95fc3-112">Per ulteriori informazioni, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="95fc3-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="95fc3-113">Per un nuovo disco, non è necessario crearlo prima perché Azure lo crea quando lo si collega.</span><span class="sxs-lookup"><span data-stu-id="95fc3-113">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>


<span data-ttu-id="95fc3-114">È anche possibile [collegare un disco dati usando Powershell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="95fc3-114">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>


## <a name="find-the-virtual-machine"></a><span data-ttu-id="95fc3-115">Trovare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="95fc3-115">Find the virtual machine</span></span>
1. <span data-ttu-id="95fc3-116">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="95fc3-116">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="95fc3-117">Nel menu a sinistra fare clic su **Macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="95fc3-117">In the menu on the left, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="95fc3-118">Selezionare la macchina virtuale dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="95fc3-118">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="95fc3-119">Nel pannello Macchine virtuali, fare clic su **Dischi**.</span><span class="sxs-lookup"><span data-stu-id="95fc3-119">In the Virtual machines blade, click **Disks**.</span></span>
   
<span data-ttu-id="95fc3-120">Continuare seguendo le istruzioni per il collegamento di un [nuovo disco](#option-1-attach-a-new-disk) o un [disco esistente](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="95fc3-120">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="95fc3-121">Opzione 1: Connettere e inizializzare un nuovo disco</span><span class="sxs-lookup"><span data-stu-id="95fc3-121">Option 1: Attach and initialize a new disk</span></span>
1. <span data-ttu-id="95fc3-122">Nel pannello **Dischi** fare clic su **+ Add data disk** (+ Aggiungi disco dati).</span><span class="sxs-lookup"><span data-stu-id="95fc3-122">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="95fc3-123">Nel pannello **Attach managed disk** (Connetti disco gestito), digitare un nome per il disco in **Nome**, quindi selezionare  **Nuovo (disco vuoto)** in **Tipo di origine**.</span><span class="sxs-lookup"><span data-stu-id="95fc3-123">In the **Attach managed disk** blade, type a name for the disk in **Name** and then select **New (empty disk)** in **Source type**.</span></span>
3. <span data-ttu-id="95fc3-124">In **Contenitore di archiviazione**, fare clic sul pulsante **Sfoglia**, quindi passare all'account di archiviazione e al contenitore in cui si desidera che il nuovo disco rigido virtuale sia archiviato e fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="95fc3-124">Under **Storage container**, click the **Browse** button and browse to the storage account and container where you would like the new VHD to be stored and then click **Select**.</span></span> 
  
   ![Esaminare le impostazioni del disco](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. <span data-ttu-id="95fc3-126">Dopo aver completato le impostazioni per il disco dati, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="95fc3-126">When you are done with the settings for the data disk, click **OK**.</span></span>
4. <span data-ttu-id="95fc3-127">Nel pannello **Dischi**, fare clic su **Salva** per aggiungere il disco alla configurazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="95fc3-127">Back in the **Disks** blade, click **Save** to add the disk to the VM configuration.</span></span>


### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="95fc3-128">Inizializzare un nuovo disco dati</span><span class="sxs-lookup"><span data-stu-id="95fc3-128">Initialize a new data disk</span></span>

1. <span data-ttu-id="95fc3-129">Connettersi alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="95fc3-129">Connect to the virtual machine.</span></span> <span data-ttu-id="95fc3-130">Per istruzioni, vedere [Come connettersi e accedere a una macchina virtuale di Azure che esegue Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="95fc3-130">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
1. <span data-ttu-id="95fc3-131">Fare clic sul menu **Start**, digitare **diskmgmt.msc** e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="95fc3-131">Click the **Start** menu inside the VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="95fc3-132">Verrà avviato lo snap-in Gestione disco.</span><span class="sxs-lookup"><span data-stu-id="95fc3-132">This starts the Disk Management snap-in.</span></span>
2. <span data-ttu-id="95fc3-133">Gestione disco rileva la disponibilità di un nuovo disco non inizializzato e viene visualizzata la finestra Inizializza disco.</span><span class="sxs-lookup"><span data-stu-id="95fc3-133">Disk Management recognizes that you have a new, uninitialized disk and the Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="95fc3-134">Assicurarsi di selezionare il nuovo disco e fare clic su **OK** per l'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="95fc3-134">Make sure the new disk is selected and click **OK** to initialize it.</span></span>
4. <span data-ttu-id="95fc3-135">Il nuovo disco verrà visualizzato come **Non allocato**.</span><span class="sxs-lookup"><span data-stu-id="95fc3-135">The new disk now appears as **unallocated**.</span></span> <span data-ttu-id="95fc3-136">Fare clic sul disco e scegliere **Nuovo volume semplice...**.</span><span class="sxs-lookup"><span data-stu-id="95fc3-136">Right-click anywhere on the disk and select **New simple volume**.</span></span> <span data-ttu-id="95fc3-137">Si avvia così la **Creazione guidata nuovo volume semplice**.</span><span class="sxs-lookup"><span data-stu-id="95fc3-137">The **New Simple Volume Wizard** starts.</span></span>
5. <span data-ttu-id="95fc3-138">Esaminare la procedura guidata mantenendo tutti i valori predefiniti e al termine scegliere **Fine**.</span><span class="sxs-lookup"><span data-stu-id="95fc3-138">Go through the wizard, keeping all of the defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="95fc3-139">Chiudere Gestione disco.</span><span class="sxs-lookup"><span data-stu-id="95fc3-139">Close Disk Management.</span></span>
7. <span data-ttu-id="95fc3-140">Verrà visualizzata una finestra popup che indica la necessità di formattare il nuovo disco prima di poterlo usare.</span><span class="sxs-lookup"><span data-stu-id="95fc3-140">You get a pop-up that you need to format the new disk before you can use it.</span></span> <span data-ttu-id="95fc3-141">Fare clic su **Formatta disco**.</span><span class="sxs-lookup"><span data-stu-id="95fc3-141">Click **Format disk**.</span></span>
8. <span data-ttu-id="95fc3-142">Nella finestra di dialogo **Formatta il nuovo disco**, controllare le impostazioni, quindi fare clic su **Start**.</span><span class="sxs-lookup"><span data-stu-id="95fc3-142">In the **Format new disk** dialog, check the settings and then click **Start**.</span></span>
9. <span data-ttu-id="95fc3-143">Verrà visualizzato un avviso che la formattazione dei dischi cancella tutti i dati. Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="95fc3-143">You get a warning that formatting the disks erases all of the data, click **OK**.</span></span>
10. <span data-ttu-id="95fc3-144">Dopo avere completato la formattazione, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="95fc3-144">When the format is complete, click **OK**.</span></span>


## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="95fc3-145">Opzione 2: Collegare un disco esistente</span><span class="sxs-lookup"><span data-stu-id="95fc3-145">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="95fc3-146">Nel pannello **Dischi** fare clic su **+ Add data disk** (+ Aggiungi disco dati).</span><span class="sxs-lookup"><span data-stu-id="95fc3-146">On the **Disks** blade, click **+ Add data disk**.</span></span>
2. <span data-ttu-id="95fc3-147">Nel pannello**Connetti disco non gestito**, in **Tipo di origine** selezionare **BLOB esistente**.</span><span class="sxs-lookup"><span data-stu-id="95fc3-147">On the **Attach unmanaged disk** blade, in **Source type** select **Existing blob**.</span></span>

    ![Esaminare le impostazioni del disco](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. <span data-ttu-id="95fc3-149">Fare clic sul pulsante **Sfoglia** per passare all'account e al contenitore di archiviazione in cui si trova il disco rigido virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="95fc3-149">Click **Browse** to navigate to the storage account and container where the existing VHD is located.</span></span> <span data-ttu-id="95fc3-150">Fare sul disco rigido virtuale, quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="95fc3-150">Click and the VHD and then click **Select**.</span></span>
4. <span data-ttu-id="95fc3-151">Fare clic su **OK** nel pannello **Collega disco non gestito**.</span><span class="sxs-lookup"><span data-stu-id="95fc3-151">Click **OK** in the **Attach unmanaged disk** blade.</span></span>
5. <span data-ttu-id="95fc3-152">Nel pannello **Dischi**, fare clic **Salva** per aggiungere il disco alla configurazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="95fc3-152">In the **Disks** blade, click **Save** to add the disk to the configuration for the VM.</span></span>
   


## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="95fc3-153">Usare TRIM con l'archiviazione Standard</span><span class="sxs-lookup"><span data-stu-id="95fc3-153">Use TRIM with standard storage</span></span>

<span data-ttu-id="95fc3-154">Se si usa l'archiviazione Standard (HDD), è consigliabile abilitare TRIM.</span><span class="sxs-lookup"><span data-stu-id="95fc3-154">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="95fc3-155">TRIM ignora i blocchi inutilizzati nel disco facendo in modo che venga addebitato solo lo spazio di archiviazione usato effettivamente.</span><span class="sxs-lookup"><span data-stu-id="95fc3-155">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="95fc3-156">In questo modo è possibile risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.</span><span class="sxs-lookup"><span data-stu-id="95fc3-156">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="95fc3-157">Per verificare l'impostazione TRIM, è possibile eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="95fc3-157">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="95fc3-158">Aprire un prompt dei comandi nella macchina virtuale Windows e digitare:</span><span class="sxs-lookup"><span data-stu-id="95fc3-158">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="95fc3-159">Se il comando restituisce 0, l'impostazione TRIM è abilitata correttamente.</span><span class="sxs-lookup"><span data-stu-id="95fc3-159">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="95fc3-160">Se restituisce 1, eseguire questo comando per abilitare TRIM:</span><span class="sxs-lookup"><span data-stu-id="95fc3-160">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="95fc3-161">Dopo l'eliminazione di dati dal disco è possibile verificare che le operazioni TRIM avvengano correttamente eseguendo la deframmentazione con TRIM:</span><span class="sxs-lookup"><span data-stu-id="95fc3-161">After deleting data from your disk, you can ensure the TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="95fc3-162">È possibile garantire anche che l'intero volume sia tagliato formattandolo.</span><span class="sxs-lookup"><span data-stu-id="95fc3-162">You can also ensure the entire volume is trimmed by formatting the volume.</span></span>


## <a name="next-steps"></a><span data-ttu-id="95fc3-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="95fc3-163">Next steps</span></span>
<span data-ttu-id="95fc3-164">Se l'applicazione deve usare l'unità D: per archiviare i dati, è possibile [modificare la lettera di unità del disco temporaneo di Windows](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="95fc3-164">If you application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

