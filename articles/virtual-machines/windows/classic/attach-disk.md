---
title: Collegare un disco a una macchina virtuale di Azure classica | Documentazione Microsoft
description: Collegare un disco dati da una macchina virtuale Windows creata con il modello di distribuzione classico e inizializzarla.
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
ms.openlocfilehash: 087d5cda354f6e1780bddd3725859444177abd16
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="attach-a-data-disk-to-a-windows-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="9564d-103">Collegare un disco dati da una macchina virtuale di Windows creata con il modello di distribuzione classico.</span><span class="sxs-lookup"><span data-stu-id="9564d-103">Attach a data disk to a Windows virtual machine created with the classic deployment model</span></span>
<!--
Refernce article:
    If you want to use the new portal, see [How to attach a data disk to a Windows VM in the Azure portal](../../virtual-machines-windows-attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

<span data-ttu-id="9564d-104">Questo articolo illustra come collegare dischi nuovi o esistenti creati con il modello di distribuzione classica a una macchina virtuale Windows usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9564d-104">This article shows you how to attach new and existing disks created with the Classic deployment model to a Windows virtual machine using the Azure portal.</span></span>

<span data-ttu-id="9564d-105">È possibile anche [collegare un disco dati a una macchina virtuale Linux nel portale di Azure](../../linux/attach-disk-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9564d-105">You can also [attach a data disk to a Linux VM in the Azure portal](../../linux/attach-disk-portal.md).</span></span>

<span data-ttu-id="9564d-106">Prima di collegare un disco, esaminare i seguenti suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="9564d-106">Before you attach a disk, review these tips:</span></span>

* <span data-ttu-id="9564d-107">La dimensione della macchina virtuale controlla il numero di dischi dati che è possibile collegare.</span><span class="sxs-lookup"><span data-stu-id="9564d-107">The size of the virtual machine controls how many data disks you can attach.</span></span> <span data-ttu-id="9564d-108">Per informazioni dettagliate, vedere [Dimensioni delle macchine virtuali](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9564d-108">For details, see [Sizes for virtual machines](../../virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="9564d-109">Per usare l'archiviazione Premium, è necessaria una macchina virtuale della serie DS o GS.</span><span class="sxs-lookup"><span data-stu-id="9564d-109">To use Premium storage, you need a DS-series or GS-series virtual machine.</span></span> <span data-ttu-id="9564d-110">È possibile utilizzare dischi dagli account di archiviazione sia Premium che Standard con queste macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="9564d-110">You can use disks from both Premium and Standard storage accounts with these virtual machines.</span></span> <span data-ttu-id="9564d-111">L’archiviazione Premium è disponibile solo in determinate aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="9564d-111">Premium storage is available in certain regions.</span></span> <span data-ttu-id="9564d-112">Per ulteriori informazioni, vedere [Archiviazione Premium: archiviazione ad alte prestazioni per carichi di lavoro delle macchine virtuali di Azure](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9564d-112">For details, see [Premium Storage: High-Performance Storage for Azure Virtual Machine Workloads](../../../storage/common/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

* <span data-ttu-id="9564d-113">Per un nuovo disco, non è necessario crearlo prima perché Azure lo crea quando lo si collega.</span><span class="sxs-lookup"><span data-stu-id="9564d-113">For a new disk, you don't need to create it first because Azure creates it when you attach it.</span></span>

<span data-ttu-id="9564d-114">È anche possibile [collegare un disco dati usando Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9564d-114">You can also [attach a data disk using Powershell](../../virtual-machines-windows-attach-disk-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9564d-115">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9564d-115">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>

## <a name="find-the-virtual-machine"></a><span data-ttu-id="9564d-116">Trovare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="9564d-116">Find the virtual machine</span></span>
1. <span data-ttu-id="9564d-117">Accedere al [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9564d-117">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9564d-118">Selezionare la macchina virtuale dalla risorsa visualizzata nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="9564d-118">Select the virtual machine from the resource listed on the dashboard.</span></span>
3. <span data-ttu-id="9564d-119">Nella sezione **Impostazioni** presente nel riquadro sinistro fare clic su **Dischi**.</span><span class="sxs-lookup"><span data-stu-id="9564d-119">In the left pane under **Settings**, click **Disks**.</span></span>

    ![Aprire le impostazioni del disco](./media/attach-disk/virtualmachinedisks.png)

<span data-ttu-id="9564d-121">Continuare seguendo le istruzioni per il collegamento di un [nuovo disco](#option-1-attach-a-new-disk) o un [disco esistente](#option-2-attach-an-existing-disk).</span><span class="sxs-lookup"><span data-stu-id="9564d-121">Continue by following instructions for attaching either a [new disk](#option-1-attach-a-new-disk) or an [existing disk](#option-2-attach-an-existing-disk).</span></span>

## <a name="option-1-attach-and-initialize-a-new-disk"></a><span data-ttu-id="9564d-122">Opzione 1: Connettere e inizializzare un nuovo disco</span><span class="sxs-lookup"><span data-stu-id="9564d-122">Option 1: Attach and initialize a new disk</span></span>

1. <span data-ttu-id="9564d-123">Nel pannello **Dischi** fare clic su **Collega nuovo**.</span><span class="sxs-lookup"><span data-stu-id="9564d-123">On the **Disks** blade, click **Attach new**.</span></span>
2. <span data-ttu-id="9564d-124">Esaminare le impostazioni predefinite, aggiornare se necessario e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9564d-124">Review the default settings, update as necessary, and then click **OK**.</span></span>

   ![Esaminare le impostazioni del disco](./media/attach-disk/attach-new.png)

3. <span data-ttu-id="9564d-126">Dopo che Azure crea il disco e lo collega alla macchina virtuale, il nuovo disco viene elencato nella sezione Impostazioni disco della macchina virtuale in **Dischi dati**.</span><span class="sxs-lookup"><span data-stu-id="9564d-126">After Azure creates the disk and attaches it to the virtual machine, the new disk is listed in the virtual machine's disk settings under **Data Disks**.</span></span>

### <a name="initialize-a-new-data-disk"></a><span data-ttu-id="9564d-127">Inizializzare un nuovo disco dati</span><span class="sxs-lookup"><span data-stu-id="9564d-127">Initialize a new data disk</span></span>

1. <span data-ttu-id="9564d-128">Connettersi alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9564d-128">Connect to the virtual machine.</span></span> <span data-ttu-id="9564d-129">Per istruzioni, vedere [Come connettersi e accedere a una macchina virtuale di Azure che esegue Windows Server](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9564d-129">For instructions, see [How to connect and log on to an Azure virtual machine running Windows](../../virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="9564d-130">Dopo aver eseguito l'accesso alla macchina virtuale, aprire **Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="9564d-130">After you log on to the virtual machine, open **Server Manager**.</span></span> <span data-ttu-id="9564d-131">Nel riquadro sinistro fare clic su **Servizi file e archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="9564d-131">In the left pane, select **File and Storage Services**.</span></span>

    ![Avviare Server Manager](../media/attach-disk-portal/fileandstorageservices.png)

3. <span data-ttu-id="9564d-133">Selezionare **Dischi**.</span><span class="sxs-lookup"><span data-stu-id="9564d-133">Select **Disks**.</span></span>
4. <span data-ttu-id="9564d-134">La sezione **dischi** contiene un elenco dei dischi.</span><span class="sxs-lookup"><span data-stu-id="9564d-134">The **Disks** section lists the disks.</span></span> <span data-ttu-id="9564d-135">Nella maggior parte dei casi, avrà disco 0, disco 1 e disco 2.</span><span class="sxs-lookup"><span data-stu-id="9564d-135">Most often, a virtual machine has disk 0, disk 1, and disk 2.</span></span> <span data-ttu-id="9564d-136">Il disco 0 è il disco del sistema operativo, il disco 1 è il disco temporaneo e il disco 2 è il disco dati appena connesso alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9564d-136">Disk 0 is the operating system disk, disk 1 is the temporary disk, and disk 2 is the data disk newly attached to the virtual machine.</span></span> <span data-ttu-id="9564d-137">Il disco dati visualizza la partizione come **Unknown** (Sconosciuta).</span><span class="sxs-lookup"><span data-stu-id="9564d-137">The data disk lists the Partition as **Unknown**.</span></span>

 <span data-ttu-id="9564d-138">Fare clic con il pulsante destro del mouse sul disco e scegliere **Inizializza**.</span><span class="sxs-lookup"><span data-stu-id="9564d-138">Right-click the disk and select **Initialize**.</span></span>

5. <span data-ttu-id="9564d-139">Si riceverà una notifica che tutti i dati verranno cancellati quando viene inizializzato il disco.</span><span class="sxs-lookup"><span data-stu-id="9564d-139">You're notified that all data will be erased when the disk is initialized.</span></span> <span data-ttu-id="9564d-140">Fare clic su **Sì** per accettare il messaggio di avviso e inizializzare il disco.</span><span class="sxs-lookup"><span data-stu-id="9564d-140">Click **Yes** to acknowledge the warning and initialize the disk.</span></span> <span data-ttu-id="9564d-141">Una volta completata l'operazione, la partizione verrà elencata come **GPT**.</span><span class="sxs-lookup"><span data-stu-id="9564d-141">Once complete, the partition will be listed as **GPT**.</span></span> <span data-ttu-id="9564d-142">Fare di nuovo clic con il pulsante destro del mouse sul disco e scegliere **Nuovo volume**.</span><span class="sxs-lookup"><span data-stu-id="9564d-142">Right-click the disk again and select **New Volume**.</span></span>

6. <span data-ttu-id="9564d-143">Completare la procedura guidata usando i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="9564d-143">Complete the wizard using the default values.</span></span> <span data-ttu-id="9564d-144">Al termine della procedura guidata, nella sezione **Volumi** verrà visualizzato il nuovo volume.</span><span class="sxs-lookup"><span data-stu-id="9564d-144">When the wizard is done, the **Volumes** section lists the new volume.</span></span> <span data-ttu-id="9564d-145">Il disco sarà ora online e pronto per l'archiviazione di dati.</span><span class="sxs-lookup"><span data-stu-id="9564d-145">The disk is now online and ready to store data.</span></span>

    ![Inizializzazione del volume completata](./media/attach-disk/newdiskafterinitialization.png)

## <a name="option-2-attach-an-existing-disk"></a><span data-ttu-id="9564d-147">Opzione 2: Collegare un disco esistente</span><span class="sxs-lookup"><span data-stu-id="9564d-147">Option 2: Attach an existing disk</span></span>
1. <span data-ttu-id="9564d-148">Nel pannello **Dischi** fare clic su **Collega esistente**.</span><span class="sxs-lookup"><span data-stu-id="9564d-148">On the **Disks** blade, click **Attach existing**.</span></span>
2. <span data-ttu-id="9564d-149">In **Collega un disco esistente** fare clic su **Posizione**.</span><span class="sxs-lookup"><span data-stu-id="9564d-149">Under **Attach existing disk**, click **Location**.</span></span>

   ![Collegare un disco esistente](./media/attach-disk/attachexistingdisksettings.png)
3. <span data-ttu-id="9564d-151">In **Account di archiviazione**, selezionare l'account e un contenitore che contiene il file con estensione vhd.</span><span class="sxs-lookup"><span data-stu-id="9564d-151">Under **Storage accounts**, select the account and container that holds the .vhd file.</span></span>

   ![Individuare il percorso di un VHD](./media/attach-disk/existdiskstorageaccountandcontainer.png)

4. <span data-ttu-id="9564d-153">Selezionare il file con estensione vhd.</span><span class="sxs-lookup"><span data-stu-id="9564d-153">Select the .vhd file.</span></span>
5. <span data-ttu-id="9564d-154">In **Collega un disco esistente** il file appena selezionato è elencato in **File VHD**.</span><span class="sxs-lookup"><span data-stu-id="9564d-154">Under **Attach existing disk**, the file you just selected is listed under **VHD File**.</span></span> <span data-ttu-id="9564d-155">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9564d-155">Click **OK**.</span></span>
6. <span data-ttu-id="9564d-156">Dopo che Azure collega il disco alla macchina virtuale, esso viene elencato nella sezione Impostazioni disco della macchina virtuale in **Dischi dei dati**.</span><span class="sxs-lookup"><span data-stu-id="9564d-156">After Azure attaches the disk to the virtual machine, it's listed in the virtual machine's disk settings under **Data Disks**.</span></span>

## <a name="use-trim-with-standard-storage"></a><span data-ttu-id="9564d-157">Usare TRIM con l'archiviazione Standard</span><span class="sxs-lookup"><span data-stu-id="9564d-157">Use TRIM with standard storage</span></span>

<span data-ttu-id="9564d-158">Se si usa l'archiviazione Standard (HDD), è consigliabile abilitare TRIM.</span><span class="sxs-lookup"><span data-stu-id="9564d-158">If you use standard storage (HDD), you should enable TRIM.</span></span> <span data-ttu-id="9564d-159">TRIM ignora i blocchi inutilizzati nel disco facendo in modo che venga addebitato solo lo spazio di archiviazione usato effettivamente.</span><span class="sxs-lookup"><span data-stu-id="9564d-159">TRIM discards unused blocks on the disk so you are only billed for storage that you are actually using.</span></span> <span data-ttu-id="9564d-160">L'uso di TRIM consente di risparmiare sui costi, inclusi i blocchi inutilizzati risultanti dall'eliminazione di file di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="9564d-160">Using TRIM can save costs, including unused blocks that result from deleting large files.</span></span>

<span data-ttu-id="9564d-161">Per verificare l'impostazione TRIM, è possibile eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="9564d-161">You can run this command to check the TRIM setting.</span></span> <span data-ttu-id="9564d-162">Aprire un prompt dei comandi nella macchina virtuale Windows e digitare:</span><span class="sxs-lookup"><span data-stu-id="9564d-162">Open a command prompt on your Windows VM and type:</span></span>

```
fsutil behavior query DisableDeleteNotify
```

<span data-ttu-id="9564d-163">Se il comando restituisce 0, l'impostazione TRIM è abilitata correttamente.</span><span class="sxs-lookup"><span data-stu-id="9564d-163">If the command returns 0, TRIM is enabled correctly.</span></span> <span data-ttu-id="9564d-164">Se restituisce 1, eseguire questo comando per abilitare TRIM:</span><span class="sxs-lookup"><span data-stu-id="9564d-164">If it returns 1, run the following command to enable TRIM:</span></span>
```
fsutil behavior set DisableDeleteNotify 0
```

## <a name="next-steps"></a><span data-ttu-id="9564d-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9564d-165">Next steps</span></span>
<span data-ttu-id="9564d-166">Se l'applicazione deve usare l'unità D: per archiviare i dati, è possibile [modificare la lettera di unità del disco temporaneo di Windows](../../virtual-machines-windows-change-drive-letter.md).</span><span class="sxs-lookup"><span data-stu-id="9564d-166">If your application needs to use the D: drive to store data, you can [change the drive letter of the Windows temporary disk](../../virtual-machines-windows-change-drive-letter.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9564d-167">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="9564d-167">Additional resources</span></span>
[<span data-ttu-id="9564d-168">Informazioni sui dischi e sui dischi rigidi virtuali per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="9564d-168">About disks and VHDs for virtual machines</span></span>](../../virtual-machines-linux-about-disks-vhds.md)
