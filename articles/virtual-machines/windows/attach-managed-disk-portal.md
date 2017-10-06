---
title: aaaAttach tooa un disco di dati gestiti - macchina virtuale di Windows Azure | Documenti Microsoft
description: Il modo tooattach nuovo gestiti tooa disco dati macchina virtuale Windows in Azure mediante portale hello hello il modello di distribuzione di gestione risorse.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: bacc0589ad2d93e4d3d055c8f837f8db27291ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-managed-data-disk-tooa-windows-vm-in-hello-azure-portal"></a><span data-ttu-id="47d0e-103">Funzionamento dei dischi tooa macchina virtuale di Windows nel portale di Azure hello tooattach dati gestiti</span><span class="sxs-lookup"><span data-stu-id="47d0e-103">How tooattach a managed data disk tooa Windows VM in hello Azure portal</span></span>

<span data-ttu-id="47d0e-104">Questo articolo illustra come i dati gestiti tooattach disco tooWindows le macchine virtuali tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="47d0e-104">This article shows you how tooattach a new managed data disk tooWindows virtual machines through hello Azure portal.</span></span> <span data-ttu-id="47d0e-105">Prima di procedere, rivedere i suggerimenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="47d0e-105">Before you do this, review these tips:</span></span>

* <span data-ttu-id="47d0e-106">dimensioni di Hello della macchina virtuale hello controlla il numero di dischi dati è possibile collegare.</span><span class="sxs-lookup"><span data-stu-id="47d0e-106">hello size of hello virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="47d0e-107">Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="47d0e-107">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="47d0e-108">Per un nuovo disco, non è necessario toocreate è primo poiché Azure crea momento del collegamento.</span><span class="sxs-lookup"><span data-stu-id="47d0e-108">For a new disk, you don't need toocreate it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="47d0e-109">È anche possibile [collegare un disco dati usando Powershell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="47d0e-109">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="add-a-data-disk"></a><span data-ttu-id="47d0e-110">Aggiungere un disco dati</span><span class="sxs-lookup"><span data-stu-id="47d0e-110">Add a data disk</span></span>
1. <span data-ttu-id="47d0e-111">Dal menu hello hello sinistra, fare clic su **macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="47d0e-111">In hello menu on hello left, click **Virtual Machines**.</span></span>
2. <span data-ttu-id="47d0e-112">Selezionare macchina virtuale hello hello elenco.</span><span class="sxs-lookup"><span data-stu-id="47d0e-112">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="47d0e-113">Nel Pannello di hello macchina virtuale, fare clic su **dischi**.</span><span class="sxs-lookup"><span data-stu-id="47d0e-113">On hello virtual machine blade, click **Disks**.</span></span>
   4. <span data-ttu-id="47d0e-114">In hello **dischi** pannello, fare clic su **+ Aggiungi disco di dati**.</span><span class="sxs-lookup"><span data-stu-id="47d0e-114">On hello **Disks** blade, click **+ Add data disk**.</span></span>
5. <span data-ttu-id="47d0e-115">Nell'elenco a discesa nuovo disco hello hello, selezionare **creare vuoto**.</span><span class="sxs-lookup"><span data-stu-id="47d0e-115">In hello drop-down for hello new disk, select **Create empty**.</span></span>
6. <span data-ttu-id="47d0e-116">In hello **disco gestito crea** pannello, digitare un nome per il disco hello e regolare hello altre impostazioni in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="47d0e-116">In hello **Create managed disk** blade, type in a name for hello disk and adjust hello other settings as necessary.</span></span> <span data-ttu-id="47d0e-117">Al termine dell'operazione fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="47d0e-117">When you are done, click **Create**.</span></span>
7. <span data-ttu-id="47d0e-118">In hello **dischi** pannello, fare clic su Salva toosave hello nuova configurazione del disco per hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="47d0e-118">In hello **Disks** blade, click save toosave hello new disk configuration for hello VM.</span></span>
6. <span data-ttu-id="47d0e-119">Dopo che Azure crea un disco hello e lo collega macchina virtuale toohello, nuovo disco hello è elencato nelle impostazioni del disco della macchina virtuale hello in **dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="47d0e-119">After Azure creates hello disk and attaches it toohello virtual machine, hello new disk is listed in hello virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="initialize-a-new-data-disk"></a><span data-ttu-id="47d0e-120">Inizializzare un nuovo disco dati</span><span class="sxs-lookup"><span data-stu-id="47d0e-120">Initialize a new data disk</span></span>

1. <span data-ttu-id="47d0e-121">Connettersi toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="47d0e-121">Connect toohello VM.</span></span>
1. <span data-ttu-id="47d0e-122">Fare clic su menu start hello all'interno di hello VM e tipo **diskmgmt.msc** e fare clic su **invio**.</span><span class="sxs-lookup"><span data-stu-id="47d0e-122">Click hello start menu inside hello VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="47d0e-123">Verrà avviata hello snap-in Gestione disco.</span><span class="sxs-lookup"><span data-stu-id="47d0e-123">This will start hello Disk Management snap-in.</span></span>
2. <span data-ttu-id="47d0e-124">Gestione disco riconoscerà che si disponga di un disco non inizializzato e si aprirà la finestra Inizializza disco hello.</span><span class="sxs-lookup"><span data-stu-id="47d0e-124">Disk Management will recognize that you have a new, un-initialized disk and hello Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="47d0e-125">Assicurarsi che sia selezionato il nuovo disco di hello e fare clic su **OK** tooinitialize è.</span><span class="sxs-lookup"><span data-stu-id="47d0e-125">Make sure hello new disk is selected and click **OK** tooinitialize it.</span></span>
4. <span data-ttu-id="47d0e-126">verrà visualizzato come nuovo disco Hello **non allocato**.</span><span class="sxs-lookup"><span data-stu-id="47d0e-126">hello new disk will now appear as **unallocated**.</span></span> <span data-ttu-id="47d0e-127">Fare clic sul disco hello e selezionare **nuovo volume semplice**.</span><span class="sxs-lookup"><span data-stu-id="47d0e-127">Right-click anywhere on hello disk and select **New simple volume**.</span></span> <span data-ttu-id="47d0e-128">Hello **semplice creazione guidata nuovo Volume** verrà avviato.</span><span class="sxs-lookup"><span data-stu-id="47d0e-128">hello **New Simple Volume Wizard** will start.</span></span>
5. <span data-ttu-id="47d0e-129">Seguire i passaggi guidata hello, mantenendo tutti i valori predefiniti di hello, al termine selezionare **fine**.</span><span class="sxs-lookup"><span data-stu-id="47d0e-129">Go through hello wizard, keeping all of hello defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="47d0e-130">Chiudere Gestione disco.</span><span class="sxs-lookup"><span data-stu-id="47d0e-130">Close Disk Management.</span></span>
7. <span data-ttu-id="47d0e-131">Verrà visualizzato un messaggio popup che è necessario nuovo disco di tooformat hello prima che sia possibile utilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="47d0e-131">You will get a pop-up that you need tooformat hello new disk before you can use it.</span></span> <span data-ttu-id="47d0e-132">Fare clic su **Formatta disco**.</span><span class="sxs-lookup"><span data-stu-id="47d0e-132">Click **Format disk**.</span></span>
8. <span data-ttu-id="47d0e-133">In hello **nuovo disco in formato** finestra di dialogo, controllare le impostazioni di hello e quindi fare clic su **avviare**.</span><span class="sxs-lookup"><span data-stu-id="47d0e-133">In hello **Format new disk** dialog, check hello settings and then click **Start**.</span></span>
9. <span data-ttu-id="47d0e-134">Verrà visualizzato un avviso che la formattazione dischi hello cancellerà tutti i dati di hello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="47d0e-134">You will get a warning that formatting hello disks will erase all of hello data, click **OK**.</span></span>
10. <span data-ttu-id="47d0e-135">Una volta completato il formato di hello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="47d0e-135">When hello format is complete, click **OK**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="47d0e-136">Usare TRIM con l'archiviazione Standard</span><span class="sxs-lookup"><span data-stu-id="47d0e-136">Use TRIM with standard storage</span></span>

<span data-ttu-id="47d0e-137">Se si usa l'archiviazione Standard (HDD), è consigliabile abilitare TRIM.</span><span class="sxs-lookup"><span data-stu-id="47d0e-137">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="47d0e-138">TRIM rimuove i blocchi inutilizzati nel disco hello in modo verrà addebitato solo per l'archiviazione che stiano effettivamente usando.</span><span class="sxs-lookup"><span data-stu-id="47d0e-138">TRIM discards unused blocks on hello disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="47d0e-139">In questo modo è possibile risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.</span><span class="sxs-lookup"><span data-stu-id="47d0e-139">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="47d0e-140">È possibile eseguire questo comando toocheck hello TRIM impostare.</span><span class="sxs-lookup"><span data-stu-id="47d0e-140">You can run this command toocheck hello TRIM setting.</span></span> <span data-ttu-id="47d0e-141">Aprire un prompt dei comandi nella macchina virtuale Windows e digitare:</span><span class="sxs-lookup"><span data-stu-id="47d0e-141">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="47d0e-142">Se il comando hello restituisce 0, l'ottimizzazione TRIM è abilitato correttamente.</span><span class="sxs-lookup"><span data-stu-id="47d0e-142">If hello command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="47d0e-143">Se viene restituito 1, eseguire hello tooenable comando TRIM seguenti:</span><span class="sxs-lookup"><span data-stu-id="47d0e-143">If it returns 1, run hello following command tooenable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="47d0e-144">Dopo l'eliminazione di dati dal disco, è possibile garantire scaricamento correttamente eseguendo le operazioni TRIM hello deframmentazione con TRIM:</span><span class="sxs-lookup"><span data-stu-id="47d0e-144">After deleting data from your disk, you can ensure hello TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="47d0e-145">È inoltre possibile garantire l'intero volume hello viene ritagliato formattando volume hello.</span><span class="sxs-lookup"><span data-stu-id="47d0e-145">You can also ensure hello entire volume is trimmed by formatting hello volume.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47d0e-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="47d0e-146">Next steps</span></span>
<span data-ttu-id="47d0e-147">Se l'applicazione necessita di dati di toostore unità d: hello toouse, è possibile [modificare hello lettera di unità del disco temporaneo di Windows hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="47d0e-147">If you application needs toouse hello D: drive toostore data, you can [change hello drive letter of hello Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
