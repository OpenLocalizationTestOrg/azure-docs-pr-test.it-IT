---
title: Risolvere i problemi eliminando account di archiviazione di Azure, contenitori o dischi rigidi virtuali in una distribuzione classica | Microsoft Docs
description: Risolvere i problemi eliminando account di archiviazione di Azure, contenitori o dischi rigidi virtuali in una distribuzione classica
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 9f3e824414ad6c1a0aba98a3d549ee63ddc7272f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a><span data-ttu-id="1cbdf-103">Risolvere i problemi eliminando account di archiviazione di Azure, contenitori o dischi rigidi virtuali in una distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="1cbdf-103">Troubleshoot deleting Azure storage accounts, containers, or VHDs in a classic deployment</span></span>
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

<span data-ttu-id="1cbdf-104">Durante il tentativo di eliminazione di account di Archiviazione di Azure, contenitori o VHD nel [Portale di Azure](https://portal.azure.com/) o nel [portale di Azure classico](https://manage.windowsazure.com/) è possibile che vengano visualizzati errori.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-104">You might receive errors when you try to delete the Azure storage account, container, or VHD in the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](https://manage.windowsazure.com/).</span></span> <span data-ttu-id="1cbdf-105">I problemi possono essere causati dalle circostanze seguenti:</span><span class="sxs-lookup"><span data-stu-id="1cbdf-105">The issues can be caused by the following circumstances:</span></span>

* <span data-ttu-id="1cbdf-106">Quando si elimina una VM, il disco e il VHD non vengono automaticamente eliminati.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-106">When you delete a VM, the disk and VHD are not automatically deleted.</span></span> <span data-ttu-id="1cbdf-107">Questo potrebbe essere il motivo dell'errore di eliminazione dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-107">That might be the reason for failure on storage account deletion.</span></span> <span data-ttu-id="1cbdf-108">Il disco non viene eliminato perché sia possibile usarlo per montare un'altra VM.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-108">We don't delete the disk so that you can use the disk to mount another VM.</span></span>
* <span data-ttu-id="1cbdf-109">Sul disco o sul BLOB associato al disco è ancora attivo un lease.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-109">There is still a lease on a disk or the blob that's associated with the disk.</span></span>
* <span data-ttu-id="1cbdf-110">È ancora presente un'immagine di VM che usa un BLOB, un contenitore o un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-110">There is still a VM image that is using a blob, container, or storage account.</span></span>

<span data-ttu-id="1cbdf-111">Se il problema riguardante Azure non è trattato in questo articolo, visitare i forum di Azure su [MSDN e Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="1cbdf-111">If your Azure issue is not addressed in this article, visit the Azure forums on [MSDN and the Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="1cbdf-112">È possibile pubblicare il problema in questi forum o in @AzureSupport su Twitter.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-112">You can post your issue on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="1cbdf-113">È anche possibile inviare una richiesta di supporto tecnico di Azure selezionando **Ottieni supporto** nel sito del [supporto tecnico di Azure](https://azure.microsoft.com/support/options/) .</span><span class="sxs-lookup"><span data-stu-id="1cbdf-113">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="1cbdf-114">Sintomi</span><span class="sxs-lookup"><span data-stu-id="1cbdf-114">Symptoms</span></span>
<span data-ttu-id="1cbdf-115">La sezione seguente elenca alcuni errori comuni che potrebbero essere visualizzati quando si tenta di eliminare gli account di Archiviazione di Azure, contenitori o VHD.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-115">The following section lists common errors that you might receive when you try to delete the Azure storage accounts, containers, or VHDs.</span></span>

### <a name="scenario-1-unable-to-delete-a-storage-account"></a><span data-ttu-id="1cbdf-116">Scenario 1: Impossibile eliminare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="1cbdf-116">Scenario 1: Unable to delete a storage account</span></span>
<span data-ttu-id="1cbdf-117">Quando si passa all'account di archiviazione classico del [portale Azure](https://portal.azure.com/) e si seleziona **Elimina**, è possibile che venga visualizzato un elenco di oggetti che impediscono l'eliminazione dell'account di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="1cbdf-117">When you navigate to the classic storage account in the [Azure portal](https://portal.azure.com/) and select **Delete**, you may be presented with a list of objects that are preventing deletion of the storage account:</span></span>

  ![Immagine dell'errore in fase di eliminazione dell'account di archiviazione](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

<span data-ttu-id="1cbdf-119">Quando si passa all'account di archiviazione nel [portale di Azure classico](https://manage.windowsazure.com/) e si seleziona **Delete**, potrebbe essere visualizzato uno dei messaggi di errore seguenti:</span><span class="sxs-lookup"><span data-stu-id="1cbdf-119">When you navigate to the storage account in the [Azure classic portal](https://manage.windowsazure.com/) and select **Delete**, you might see one of the following errors:</span></span>

- <span data-ttu-id="1cbdf-120">*L'account di archiviazione StorageAccountName contiene immagini di VM. Assicurarsi di rimuovere queste immagini prima di eliminare questo account di archiviazione.*</span><span class="sxs-lookup"><span data-stu-id="1cbdf-120">*Storage account StorageAccountName contains VM Images. Ensure these VM Images are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="1cbdf-121">*Non è stato possibile eliminare l'account di archiviazione <nome-account-archiviazione-vm>. Impossibile eliminare l'account di archiviazione <nome-account-archiviazione-vm>: "<nome-account-archiviazione-vm> presenta alcune immagini e/o dischi attivi. Assicurarsi di rimuovere tali immagini e/o dischi prima di eliminare l'account di archiviazione.*</span><span class="sxs-lookup"><span data-stu-id="1cbdf-121">*Failed to delete storage account <vm-storage-account-name>. Unable to delete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.*</span></span>

- <span data-ttu-id="1cbdf-122">*L'account di archiviazione<nome-account-archiviazione-vm> presenta alcune immagini e/o dischi attivi, ad esempio xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Assicurarsi di rimuovere tali immagini e/o dischi prima di eliminare l'account di archiviazione.*</span><span class="sxs-lookup"><span data-stu-id="1cbdf-122">*Storage account <vm-storage-account-name> has some active image(s) and/or disk(s), e.g. xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Ensure these image(s) and/or disk(s) are removed before deleting this storage account.*</span></span>

- <span data-ttu-id="1cbdf-123">*L'account di archiviazione <nome-account-archiviazione-vm> presenta 1 contenitore con un'immagine attiva e/o elementi di disco. Assicurarsi che gli elementi locali siano rimossi dall'archivio immagini prima di eliminare l'account di archiviazione*.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-123">*Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account*.</span></span>

- <span data-ttu-id="1cbdf-124">*Invio non riuscito L'account di archiviazione <nome-account-archiviazione-vm> presenta 1 contenitore con un'immagine attiva e/o elementi di disco. Assicurarsi che gli elementi locali siano rimossi dall'archivio immagini prima di eliminare l'account di archiviazione. Quando si tenta di eliminare un account di archiviazione con dischi associati ancora attivi, viene visualizzato un messaggio in cui si chiede di eliminare i dischi attivi*.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-124">*Submit Failed Storage account <vm-storage-account-name> has 1 container(s) which have an active image and/or disk artifacts. Ensure those artifacts are removed from the image repository before deleting this storage account. When you attempt to delete a storage account and there are still active disks associated with it, you will see a message telling you there are active disks that need to be deleted*.</span></span>

### <a name="scenario-2-unable-to-delete-a-container"></a><span data-ttu-id="1cbdf-125">Scenario 2. Impossibile eliminare un contenitore</span><span class="sxs-lookup"><span data-stu-id="1cbdf-125">Scenario 2: Unable to delete a container</span></span>
<span data-ttu-id="1cbdf-126">Quando si tenta di eliminare il contenitore di archiviazione, potrebbe essere visualizzato l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="1cbdf-126">When you try to delete the storage container, you might see the following error:</span></span>

<span data-ttu-id="1cbdf-127">*Non è stato possibile eliminare il contenitore di archiviazione<container name>. Errore: sul contenitore è ancora attivo un lease. Nessun ID lease è stato specificato nella richiesta*.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-127">*Failed to delete storage container <container name>. Error: 'There is currently a lease on the container and no lease ID was specified in the request*.</span></span>

<span data-ttu-id="1cbdf-128">Oppure</span><span class="sxs-lookup"><span data-stu-id="1cbdf-128">Or</span></span>

<span data-ttu-id="1cbdf-129">*I dischi di macchina virtuale seguenti usano BLOB in questo contenitore, pertanto il contenitore non può essere eliminato: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span><span class="sxs-lookup"><span data-stu-id="1cbdf-129">*The following virtual machine disks use blobs in this container, so the container cannot be deleted: VirtualMachineDiskName1, VirtualMachineDiskName2, ...*</span></span>

### <a name="scenario-3-unable-to-delete-a-vhd"></a><span data-ttu-id="1cbdf-130">Scenario 3. Impossibile eliminare un VHD</span><span class="sxs-lookup"><span data-stu-id="1cbdf-130">Scenario 3: Unable to delete a VHD</span></span>
<span data-ttu-id="1cbdf-131">Dopo l'eliminazione di una VM, se si tenta di eliminare i BLOB relativi ai VHD associati, potrebbe essere visualizzato il messaggio seguente:</span><span class="sxs-lookup"><span data-stu-id="1cbdf-131">After you delete a VM and then try to delete the blobs for the associated VHDs, you might receive the following message:</span></span>

<span data-ttu-id="1cbdf-132">*Non è stato possibile eliminare il BLOB ''percorso/XXXXXX-XXXXXX-os-1447379084699.vhd''. Errore: sul BLOB è ancora attivo un lease. Nessun ID lease è stato specificato nella richiesta.*</span><span class="sxs-lookup"><span data-stu-id="1cbdf-132">*Failed to delete blob 'path/XXXXXX-XXXXXX-os-1447379084699.vhd'. Error: 'There is currently a lease on the blob and no lease ID was specified in the request.*</span></span>

<span data-ttu-id="1cbdf-133">Or</span><span class="sxs-lookup"><span data-stu-id="1cbdf-133">Or</span></span>

<span data-ttu-id="1cbdf-134">*Il BLOB 'BlobName.vhd' è in uso come disco di macchina virtuale 'VirtualMachineDiskName', pertanto non può essere eliminato.*</span><span class="sxs-lookup"><span data-stu-id="1cbdf-134">*Blob 'BlobName.vhd' is in use as virtual machine disk 'VirtualMachineDiskName', so the blob cannot be deleted.*</span></span>

## <a name="solution"></a><span data-ttu-id="1cbdf-135">Soluzione</span><span class="sxs-lookup"><span data-stu-id="1cbdf-135">Solution</span></span>
<span data-ttu-id="1cbdf-136">Per risolvere i problemi più comuni, provare una delle procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="1cbdf-136">To resolve the most common issues, try the following method:</span></span>

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-the-storage-account-container-or-vhd"></a><span data-ttu-id="1cbdf-137">Passaggio 1: eliminare eventuali dischi che impediscono l'eliminazione dell'account di archiviazione, del contenitore o del disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="1cbdf-137">Step 1: Delete any disks that are preventing deletion of the storage account, container, or VHD</span></span>
1. <span data-ttu-id="1cbdf-138">Accedere al [portale di Azure classico](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="1cbdf-138">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="1cbdf-139">Selezionare **MACCHINA VIRTUALE** > **DISCHI**.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-139">Select **VIRTUAL MACHINE** > **DISKS**.</span></span>

    ![Immagine di dischi all'interno di macchine virtuali nel Portale di Azure classico.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. <span data-ttu-id="1cbdf-141">Individuare i dischi associati all'account di archiviazione, al contenitore o al VHD che si vuole eliminare.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-141">Locate the disks that are associated with the storage account, container, or VHD that you want to delete.</span></span> <span data-ttu-id="1cbdf-142">Controllando la posizione del disco, è possibile trovare l'account di archiviazione, il contenitore e il VHD associati.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-142">When you check the location of the disk, you will find the associated storage account, container, or VHD.</span></span>

    ![Immagine che mostra le informazioni sulla posizione per i dischi nel Portale di Azure classico](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. <span data-ttu-id="1cbdf-144">Eliminare i dischi usando uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1cbdf-144">Delete the disks by using one of the following methods:</span></span>

  - <span data-ttu-id="1cbdf-145">Se nel campo **Collegato a** del disco non sono elencate VM, è possibile eliminare il disco direttamente.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-145">If  there is no VM listed on the **Attached To** field of the disk, you can delete the disk directly.</span></span>

  - <span data-ttu-id="1cbdf-146">Nel caso di un disco dati, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="1cbdf-146">If the disk is a data disk, follow these steps:</span></span>

    1. <span data-ttu-id="1cbdf-147">Controllare il nome della VM a cui è collegato il disco.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-147">Check the name of the VM that the disk is attached to.</span></span>
    2. <span data-ttu-id="1cbdf-148">Passare a **Macchine virtuali** > **Istanze** e individuare la VM.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-148">Go to **Virtual Machines** > **Instances**, and then locate the VM.</span></span>
    3. <span data-ttu-id="1cbdf-149">Assicurarsi che nessuno stia usando il disco.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-149">Make sure that nothing is actively using the disk.</span></span>
    4. <span data-ttu-id="1cbdf-150">Selezionare **Scollega disco** nella parte inferiore del portale per scollegare il disco.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-150">Select **Detach Disk** at the bottom of the portal to detach the disk.</span></span>
    5. <span data-ttu-id="1cbdf-151">Passare a **Macchine virtuali** > **Dischi** e attendere che il campo **Collegato a** diventi vuoto.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-151">Go to **Virtual Machines** > **Disks**, and wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="1cbdf-152">Ciò indica che il disco è stato scollegato correttamente dalla VM.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-152">This indicates the disk has successfully detached from the VM.</span></span>
    6. <span data-ttu-id="1cbdf-153">Selezionare **Elimina** in basso in **Macchine virtuali** > **Dischi** per eliminare il disco.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-153">Select **Delete** at the bottom of **Virtual Machines** > **Disks** to delete the disk.</span></span>

  - <span data-ttu-id="1cbdf-154">Se il disco è un disco del sistema operativo (il valore del campo **Contiene sistema operativo** è Windows o simile) ed è collegato a una VM, seguire questa procedura per eliminare la VM.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-154">If the disk is an OS disk (the **Contains OS** field has a value like Windows) and attached to a VM, follow these steps to delete the VM.</span></span> <span data-ttu-id="1cbdf-155">Il disco del sistema operativo non può essere scollegato, quindi è necessario eliminare la VM per rilasciare il lease.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-155">The OS disk cannot be detached, so we have to delete the VM to release the lease.</span></span>

    1. <span data-ttu-id="1cbdf-156">Controllare il nome della macchina virtuale a cui è collegato il disco dati.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-156">Check the name of the Virtual Machine the Data Disk is attached to.</span></span>  
    2. <span data-ttu-id="1cbdf-157">Passare a **Macchine virtuali** > **Istanze** e quindi selezionare la VM a cui è collegato il disco.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-157">Go to **Virtual Machines** > **Instances**, and then select the VM that the disk is attached to.</span></span>
    3. <span data-ttu-id="1cbdf-158">Assicurarsi che la macchina virtuale non sia in uso e che non sia più necessaria.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-158">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
    4. <span data-ttu-id="1cbdf-159">Selezionare la VM a cui è collegato il disco e quindi selezionare **Elimina** > **Elimina dischi collegati**.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-159">Select the VM the disk is attached to, then select **Delete** > **Delete the attached disks**.</span></span>
    5. <span data-ttu-id="1cbdf-160">Passare a **Macchine virtuali** > **Dischi** e attendere che il disco scompaia.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-160">Go to **Virtual Machines** > **Disks**, and wait for the disk to disappear.</span></span>  <span data-ttu-id="1cbdf-161">L'operazione potrebbe impiegare qualche minuto e potrebbe essere necessario aggiornare la pagina.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-161">It may take a few minutes for this to occur, and you may need to refresh the page.</span></span>
    6. <span data-ttu-id="1cbdf-162">Se il disco non scompare, attendere che il campo **Collegato a** diventi vuoto.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-162">If the disk does not disappear, wait for the **Attached To** field to turn blank.</span></span> <span data-ttu-id="1cbdf-163">Ciò indica che il disco è stato scollegato completamente dalla VM.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-163">This indicates the disk has fully detached from the VM.</span></span>  <span data-ttu-id="1cbdf-164">Selezionare quindi il disco e poi **Elimina** nella parte inferiore della pagina per eliminare il disco.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-164">Then, select the disk, and select **Delete** at the bottom of the page to delete the disk.</span></span>


   > [!NOTE]
   > <span data-ttu-id="1cbdf-165">Se un disco è collegato a una VM, non sarà possibile eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-165">If a disk is attached to a VM, you will not be able to delete it.</span></span> <span data-ttu-id="1cbdf-166">I dischi vengono scollegati da una VM eliminata in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-166">Disks are detached from a deleted VM asynchronously.</span></span> <span data-ttu-id="1cbdf-167">Dopo l'eliminazione della VM la cancellazione di questo campo potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-167">It might take a few minutes after the VM is deleted for this field to clear up.</span></span>
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-the-storage-account-or-container"></a><span data-ttu-id="1cbdf-168">Passaggio 2: Eliminare eventuali immagini di VM che impediscono l'eliminazione dell'account di archiviazione o del contenitore</span><span class="sxs-lookup"><span data-stu-id="1cbdf-168">Step 2: Delete any VM Images that are preventing deletion of the storage account or container</span></span>
1. <span data-ttu-id="1cbdf-169">Accedere al [portale di Azure classico](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="1cbdf-169">Switch to the [Azure classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="1cbdf-170">Selezionare **MACCHINA VIRTUALE** > **IMMAGINI** e quindi eliminare le immagini associate all'account di archiviazione, al contenitore o al disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-170">Select **VIRTUAL MACHINE** > **IMAGES**, and then delete the images that are associated with the storage account, container, or VHD.</span></span>

    <span data-ttu-id="1cbdf-171">Provare quindi di nuovo a eliminare l'account di archiviazione, il contenitore o il VHD.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-171">After that, try to delete the storage account, container, or VHD again.</span></span>

> [!WARNING]
> <span data-ttu-id="1cbdf-172">Assicurarsi di eseguire il backup di tutti gli elementi da salvare prima di eliminare l'account.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-172">Be sure to back up anything you want to save before you delete the account.</span></span> <span data-ttu-id="1cbdf-173">Quando si elimina un disco rigido virtuale, un BLOB, una tabella, una coda o un file, l'elemento viene eliminato definitivamente.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-173">Once you delete a VHD, blob, table, queue, or file, it is permanently deleted.</span></span> <span data-ttu-id="1cbdf-174">Assicurarsi che la risorsa non sia in uso.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-174">Ensure that the resource is not in use.</span></span>
>
>

## <a name="about-the-stopped-deallocated-status"></a><span data-ttu-id="1cbdf-175">Informazioni sullo stato Arrestato (deallocato)</span><span class="sxs-lookup"><span data-stu-id="1cbdf-175">About the Stopped (deallocated) status</span></span>
<span data-ttu-id="1cbdf-176">Le VM che sono state create nel modello di distribuzione classico e che sono state mantenute avranno lo stato **Arrestato (deallocato)** nel [Portale di Azure](https://portal.azure.com/) o nel [portale di Azure classico](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="1cbdf-176">VMs that were created in the classic deployment model and that have been retained will have the **Stopped (deallocated)** status on either the [Azure portal](https://portal.azure.com/) or [Azure classic portal](https://manage.windowsazure.com/).</span></span>

<span data-ttu-id="1cbdf-177">**Portale di Azure classico**:</span><span class="sxs-lookup"><span data-stu-id="1cbdf-177">**Azure classic portal**:</span></span>

![Stato Arrestato (deallocato) per VM nel Portale di Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

<span data-ttu-id="1cbdf-179">**Portale di Azure**:</span><span class="sxs-lookup"><span data-stu-id="1cbdf-179">**Azure portal**:</span></span>

![Stato Arrestato (deallocato) per VM nel Portale di Azure classico.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

<span data-ttu-id="1cbdf-181">Lo stato "Arrestato (deallocato)" rilascia le risorse del computer, ad esempio CPU, memoria e rete.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-181">A "Stopped (deallocated)" status releases the computer resources, such as the CPU, memory, and network.</span></span> <span data-ttu-id="1cbdf-182">I dischi, tuttavia, vengono mantenuti, in modo che si possa rapidamente ricreare la VM se necessario.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-182">The disks, however, are still retained so that you can quickly re-create the VM if necessary.</span></span> <span data-ttu-id="1cbdf-183">Questi dischi vengono creati all'interno di VHD, che sono supportati da Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-183">These disks are created on top of VHDs, which are backed by Azure storage.</span></span> <span data-ttu-id="1cbdf-184">L'account di archiviazione possiede questi VHD e i dischi hanno un lease su di essi.</span><span class="sxs-lookup"><span data-stu-id="1cbdf-184">The storage account has these VHDs, and the disks have leases on those VHDs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cbdf-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1cbdf-185">Next steps</span></span>
* [<span data-ttu-id="1cbdf-186">Eliminare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="1cbdf-186">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
