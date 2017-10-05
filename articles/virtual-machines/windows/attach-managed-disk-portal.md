---
title: Collegare un disco dati gestito a una macchina virtuale Windows - Azure | Microsoft Docs
description: Come collegare un disco dati gestito nuovo a una macchina virtuale Windows nel portale di Azure tramite il modello di distribuzione di Resource Manager.
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
ms.openlocfilehash: f0cf88a06c5470ef173b22e7213419a6c8760723
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-a-managed-data-disk-to-a-windows-vm-in-the-azure-portal"></a><span data-ttu-id="9b8dd-103">Collegare un disco dati gestito a una macchina virtuale Windows nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9b8dd-103">How to attach a managed data disk to a Windows VM in the Azure portal</span></span>

<span data-ttu-id="9b8dd-104">Questo articolo illustra come collegare dischi gestiti nuovi a una macchina virtuale Windows tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-104">This article shows you how to attach a new managed data disk to Windows virtual machines through the Azure portal.</span></span> <span data-ttu-id="9b8dd-105">Prima di procedere, rivedere i suggerimenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9b8dd-105">Before you do this, review these tips:</span></span>

* <span data-ttu-id="9b8dd-106">La dimensione della macchina virtuale controlla il numero di dischi dati che è possibile collegare.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-106">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="9b8dd-107">Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="9b8dd-107">For details, see [Sizes for virtual machines](sizes.md).</span></span>
* <span data-ttu-id="9b8dd-108">Per un nuovo disco, non è necessario crearlo prima perché Azure lo crea quando lo si collega.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-108">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="9b8dd-109">È anche possibile [collegare un disco dati usando Powershell](attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9b8dd-109">You can also [attach a data disk using Powershell](attach-disk-ps.md).</span></span>



## <a name="add-a-data-disk"></a><span data-ttu-id="9b8dd-110">Aggiungere un disco dati</span><span class="sxs-lookup"><span data-stu-id="9b8dd-110">Add a data disk</span></span>
1. <span data-ttu-id="9b8dd-111">Nel menu a sinistra fare clic su **Macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-111">In the menu on the left, click **Virtual Machines**.</span></span>
2. <span data-ttu-id="9b8dd-112">Selezionare la macchina virtuale dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-112">Select the virtual machine from the list.</span></span>
3. <span data-ttu-id="9b8dd-113">Nel pannello Macchine virtuali, fare clic su **Dischi**.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-113">On the virtual machine blade, click **Disks**.</span></span>
   4. <span data-ttu-id="9b8dd-114">Nel pannello **Dischi** fare clic su **+ Add data disk** (+ Aggiungi disco dati).</span><span class="sxs-lookup"><span data-stu-id="9b8dd-114">On the **Disks** blade, click **+ Add data disk**.</span></span>
5. <span data-ttu-id="9b8dd-115">Nell'elenco a discesa per il nuovo disco, selezionare **Crea vuoto...**.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-115">In the drop-down for the new disk, select **Create empty**.</span></span>
6. <span data-ttu-id="9b8dd-116">Nel pannello **Crea disco gestito**, digitare un nome per il disco e regolare le altre impostazioni in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-116">In the **Create managed disk** blade, type in a name for the disk and adjust the other settings as necessary.</span></span> <span data-ttu-id="9b8dd-117">Al termine dell'operazione fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-117">When you are done, click **Create**.</span></span>
7. <span data-ttu-id="9b8dd-118">Nel pannello **Dischi**, fare clic Salva per salvare la configurazione del nuovo disco della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-118">In the **Disks** blade, click save to save the new disk configuration for the VM.</span></span>
6. <span data-ttu-id="9b8dd-119">Dopo che Azure crea il disco e lo collega alla macchina virtuale, il nuovo disco viene elencato nella sezione Impostazioni disco della macchina virtuale in **Dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-119">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>


## <a name="initialize-a-new-data-disk"></a><span data-ttu-id="9b8dd-120">Inizializzare un nuovo disco dati</span><span class="sxs-lookup"><span data-stu-id="9b8dd-120">Initialize a new data disk</span></span>

1. <span data-ttu-id="9b8dd-121">Connettersi alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-121">Connect to the VM.</span></span>
1. <span data-ttu-id="9b8dd-122">Fare clic sul menu Start della macchina virtuale, digitare **diskmgmt.msc** e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-122">Click the start menu inside the VM and type **diskmgmt.msc** and hit **Enter**.</span></span> <span data-ttu-id="9b8dd-123">Verrà avviato lo snap-in Gestione disco.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-123">This will start the Disk Management snap-in.</span></span>
2. <span data-ttu-id="9b8dd-124">Gestione disco rileva la disponibilità di un nuovo disco non inizializzato e viene visualizzata la finestra Inizializza disco.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-124">Disk Management will recognize that you have a new, un-initialized disk and the Initialize Disk window will pop up.</span></span>
3. <span data-ttu-id="9b8dd-125">Assicurarsi di selezionare il nuovo disco e fare clic su **OK** per l'inizializzazione.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-125">Make sure the new disk is selected and click **OK** to initialize it.</span></span>
4. <span data-ttu-id="9b8dd-126">Il nuovo disco verrà visualizzato come **Non allocato**.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-126">The new disk will now appear as **unallocated**.</span></span> <span data-ttu-id="9b8dd-127">Fare clic sul disco e scegliere **Nuovo volume semplice...**.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-127">Right-click anywhere on the disk and select **New simple volume**.</span></span> <span data-ttu-id="9b8dd-128">Si avvia così la **Creazione guidata nuovo volume semplice**.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-128">The **New Simple Volume Wizard** will start.</span></span>
5. <span data-ttu-id="9b8dd-129">Esaminare la procedura guidata mantenendo tutti i valori predefiniti e al termine scegliere **Fine**.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-129">Go through the wizard, keeping all of the defaults, when you are done select **Finish**.</span></span>
6. <span data-ttu-id="9b8dd-130">Chiudere Gestione disco.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-130">Close Disk Management.</span></span>
7. <span data-ttu-id="9b8dd-131">Verrà visualizzata una finestra popup che indica la necessità di formattare il nuovo disco prima di poterlo usare.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-131">You will get a pop-up that you need to format the new disk before you can use it.</span></span> <span data-ttu-id="9b8dd-132">Fare clic su **Formatta disco**.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-132">Click **Format disk**.</span></span>
8. <span data-ttu-id="9b8dd-133">Nella finestra di dialogo **Formatta il nuovo disco**, controllare le impostazioni, quindi fare clic su **Start**.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-133">In the **Format new disk** dialog, check the settings and then click **Start**.</span></span>
9. <span data-ttu-id="9b8dd-134">Verrà visualizzato un avviso che la formattazione dei dischi cancella tutti i dati. Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-134">You will get a warning that formatting the disks will erase all of the data, click **OK**.</span></span>
10. <span data-ttu-id="9b8dd-135">Dopo avere completato la formattazione, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-135">When the format is complete, click **OK**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="9b8dd-136">Usare TRIM con l'archiviazione Standard</span><span class="sxs-lookup"><span data-stu-id="9b8dd-136">Use TRIM with standard storage</span></span>

<span data-ttu-id="9b8dd-137">Se si usa l'archiviazione Standard (HDD), è consigliabile abilitare TRIM.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-137">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="9b8dd-138">TRIM ignora i blocchi inutilizzati nel disco facendo in modo che venga addebitato solo lo spazio di archiviazione usato effettivamente.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-138">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="9b8dd-139">In questo modo è possibile risparmiare sui costi quando si creano file di grandi dimensioni per poi eliminarli.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-139">This can save on costs if you create large files and then delete them.</span></span> 

<span data-ttu-id="9b8dd-140">Per verificare l'impostazione TRIM, è possibile eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-140">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="9b8dd-141">Aprire un prompt dei comandi nella macchina virtuale Windows e digitare:</span><span class="sxs-lookup"><span data-stu-id="9b8dd-141">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="9b8dd-142">Se il comando restituisce 0, l'impostazione TRIM è abilitata correttamente.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-142">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="9b8dd-143">Se restituisce 1, eseguire questo comando per abilitare TRIM:</span><span class="sxs-lookup"><span data-stu-id="9b8dd-143">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

<span data-ttu-id="9b8dd-144">Dopo l'eliminazione di dati dal disco è possibile verificare che le operazioni TRIM avvengano correttamente eseguendo la deframmentazione con TRIM:</span><span class="sxs-lookup"><span data-stu-id="9b8dd-144">After deleting data from your disk, you can ensure the TRIM operations flush properly by running defrag with TRIM:</span></span>

```
defrag.exe <volume:> -l
```

<span data-ttu-id="9b8dd-145">È possibile garantire anche che l'intero volume sia tagliato formattandolo.</span><span class="sxs-lookup"><span data-stu-id="9b8dd-145">You can also ensure the entire volume is trimmed by formatting the volume.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b8dd-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9b8dd-146">Next steps</span></span>
<span data-ttu-id="9b8dd-147">Se l'applicazione deve usare l'unità D: per archiviare i dati, è possibile [modificare la lettera di unità del disco temporaneo di Windows](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9b8dd-147">If you application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
