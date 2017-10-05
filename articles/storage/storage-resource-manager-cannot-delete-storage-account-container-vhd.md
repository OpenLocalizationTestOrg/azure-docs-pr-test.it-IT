---
title: Risolvere gli errori quando si eliminano account di archiviazione, contenitori o dischi rigidi virtuali di Azure in una distribuzione Resource Manager | Microsoft Docs
description: Risolvere gli errori quando si eliminano account di archiviazione, contenitori o dischi rigidi virtuali di Azure
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 318d7146ea53a806baf813ff7de2fe91f18becc8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a><span data-ttu-id="3d92e-103">Risolvere gli errori quando si eliminano account di archiviazione, contenitori o dischi rigidi virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="3d92e-103">Troubleshoot errors when you delete Azure storage accounts, containers, or VHDs</span></span>

<span data-ttu-id="3d92e-104">Durante il tentativo di eliminazione di account di archiviazione, contenitori o dischi rigidi virtuali di Azure nel [portale di Azure](https://portal.azure.com) è possibile ricevere errori.</span><span class="sxs-lookup"><span data-stu-id="3d92e-104">You might receive errors when you try to delete an Azure storage account, container, or virtual hard disk (VHD) in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="3d92e-105">Questo articolo fornisce indicazioni sulla risoluzione dei problemi in una distribuzione di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3d92e-105">This article provides troubleshooting guidance to help resolve the problem in an Azure Resource Manager deployment.</span></span>

<span data-ttu-id="3d92e-106">Se il problema di Azure non viene risolto in questo articolo, visitare i forum di Azure su [MSDN e Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="3d92e-106">If this article doesn't address your Azure problem, visit the Azure forums on [MSDN and Stack Overflow](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="3d92e-107">È possibile pubblicare il problema in questi forum o in @AzureSupport su Twitter.</span><span class="sxs-lookup"><span data-stu-id="3d92e-107">You can post your problem on these forums or to @AzureSupport on Twitter.</span></span> <span data-ttu-id="3d92e-108">È anche possibile inviare una richiesta di supporto tecnico di Azure selezionando **Ottieni supporto** nel sito del [supporto tecnico di Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="3d92e-108">Also, you can file an Azure support request by selecting **Get support** on the [Azure support](https://azure.microsoft.com/support/options/) site.</span></span>

## <a name="symptoms"></a><span data-ttu-id="3d92e-109">Sintomi</span><span class="sxs-lookup"><span data-stu-id="3d92e-109">Symptoms</span></span>
### <a name="scenario-1"></a><span data-ttu-id="3d92e-110">Scenario 1</span><span class="sxs-lookup"><span data-stu-id="3d92e-110">Scenario 1</span></span>
<span data-ttu-id="3d92e-111">Quando si tenta di eliminare un disco rigido virtuale in un account di archiviazione di una distribuzione di Resource Manager, viene visualizzato un messaggio di errore simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3d92e-111">When you try to delete a VHD in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="3d92e-112">**Non è stato possibile eliminare il BLOB 'vhds/BlobName.vhd'. Errore: sul BLOB è ancora attivo un lease. Nessun ID lease è stato specificato nella richiesta.**</span><span class="sxs-lookup"><span data-stu-id="3d92e-112">**Failed to delete blob 'vhds/BlobName.vhd'. Error: There is currently a lease on the blob and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="3d92e-113">Questo problema può verificarsi perché una macchina virtuale dispone di un lease sul disco rigido virtuale che si sta tentando di eliminare.</span><span class="sxs-lookup"><span data-stu-id="3d92e-113">This problem can occur because a virtual machine (VM) has a lease on the VHD that you are trying to delete.</span></span>

### <a name="scenario-2"></a><span data-ttu-id="3d92e-114">Scenario 2</span><span class="sxs-lookup"><span data-stu-id="3d92e-114">Scenario 2</span></span>
<span data-ttu-id="3d92e-115">Quando si tenta di eliminare un contenitore in un account di archiviazione di una distribuzione di Resource Manager, viene visualizzato un messaggio di errore simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3d92e-115">When you try to delete a container in a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="3d92e-116">**Non è stato possibile eliminare il contenitore di archiviazione 'vhds'. Errore: sul contenitore è ancora attivo un lease. Nessun ID lease è stato specificato nella richiesta.**</span><span class="sxs-lookup"><span data-stu-id="3d92e-116">**Failed to delete storage container 'vhds'. Error: There is currently a lease on the container and no lease ID was specified in the request.**</span></span>

<span data-ttu-id="3d92e-117">Questo problema può verificarsi perché il contenitore dispone di un disco rigido virtuale bloccato nello stato di lease.</span><span class="sxs-lookup"><span data-stu-id="3d92e-117">This problem can occur because the container has a VHD that is locked in the lease state.</span></span>

### <a name="scenario-3"></a><span data-ttu-id="3d92e-118">Scenario 3</span><span class="sxs-lookup"><span data-stu-id="3d92e-118">Scenario 3</span></span>
<span data-ttu-id="3d92e-119">Quando si tenta di eliminare un account di archiviazione di una distribuzione di Resource Manager, viene visualizzato un messaggio di errore simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="3d92e-119">When you try to delete a storage account in a Resource Manager deployment, you receive the following error message:</span></span>

<span data-ttu-id="3d92e-120">**Non è stato possibile eliminare l'account di archiviazione 'NomeAccountArchiviazione'. Errore: non è possibile eliminare l'account di archiviazione perché gli elementi sono in uso.**</span><span class="sxs-lookup"><span data-stu-id="3d92e-120">**Failed to delete storage account 'StorageAccountName'. Error: The storage account cannot be deleted due to its artifacts being in use.**</span></span>

<span data-ttu-id="3d92e-121">Questo problema può verificarsi perché l'account di archiviazione dispone di un disco rigido virtuale in stato di lease.</span><span class="sxs-lookup"><span data-stu-id="3d92e-121">This problem can occur because the storage account contains a VHD that is in the lease state.</span></span>

## <a name="solution"></a><span data-ttu-id="3d92e-122">Soluzione</span><span class="sxs-lookup"><span data-stu-id="3d92e-122">Solution</span></span> 
<span data-ttu-id="3d92e-123">Per risolvere questi problemi, è necessario identificare il disco rigido virtuale che sta causando l'errore e la macchina virtuale associata.</span><span class="sxs-lookup"><span data-stu-id="3d92e-123">To resolve these problems, you must identify the VHD that is causing the error and the associated VM.</span></span> <span data-ttu-id="3d92e-124">Quindi, scollegare il disco rigido virtuale dalla macchina virtuale (per i dischi dati) o eliminare la macchina virtuale che usa il disco rigido virtuale (per i dischi del sistema operativo).</span><span class="sxs-lookup"><span data-stu-id="3d92e-124">Then, detach the VHD from the VM (for data disks) or delete the VM that is using the VHD (for OS disks).</span></span> <span data-ttu-id="3d92e-125">In questo modo, viene rimosso il lease dal disco rigido virtuale e se ne consente l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="3d92e-125">This removes the lease from the VHD and allows it to be deleted.</span></span> 

<span data-ttu-id="3d92e-126">Per farlo, usare uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3d92e-126">To do this, use one of the following methods:</span></span>

### <a name="method-1---use-azure-storage-explorer"></a><span data-ttu-id="3d92e-127">Metodo 1: usare Esplora archivi di Azure</span><span class="sxs-lookup"><span data-stu-id="3d92e-127">Method 1 - Use Azure storage explorer</span></span>

### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="3d92e-128">Passaggio 1: identificare il disco rigido virtuale che impedisce l'eliminazione dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="3d92e-128">Step 1 Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="3d92e-129">Eliminando l'account di archiviazione, si riceverà una finestra di dialogo con messaggio come la seguente:</span><span class="sxs-lookup"><span data-stu-id="3d92e-129">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![Messaggio durante l'eliminazione dell'account di archiviazione](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="3d92e-131">Controllare l'**URL del disco** per identificare l'account di archiviazione e il disco rigido virtuale che impedisce di eliminare l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3d92e-131">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="3d92e-132">Nell'esempio seguente la stringa che precede ".blob.core.windows.net" è il nome dell'account di archiviazione, mentre "SCCM2012-2015-08-28.vhd" è il nome del disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="3d92e-132">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-the-vhd-by-using-azure-storage-explorer"></a><span data-ttu-id="3d92e-133">Passaggio 2: eliminare il disco rigido virtuale tramite Esplora archivi di Azure</span><span class="sxs-lookup"><span data-stu-id="3d92e-133">Step 2 Delete the VHD by using Azure Storage Explorer</span></span>

1. <span data-ttu-id="3d92e-134">Scaricare e installare la versione più recente di [Esplora archivi di Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="3d92e-134">Download and Install the latest version of [Azure Storage Explorer](http://storageexplorer.com/).</span></span> <span data-ttu-id="3d92e-135">Questo strumento è un'app autonoma di Microsoft che consente di gestire facilmente dati di Archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="3d92e-135">This tool is a standalone app from Microsoft that allows you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span>
2. <span data-ttu-id="3d92e-136">Aprire Esplora archivi di Azure, selezionare</span><span class="sxs-lookup"><span data-stu-id="3d92e-136">Open Azure Storage Explorer, select</span></span> ![icona account](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) <span data-ttu-id="3d92e-138">nella barra sinistra, selezionare l'ambiente di Azure e quindi eseguire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="3d92e-138">on the left bar, select your Azure environment, and then sign in.</span></span>

3. <span data-ttu-id="3d92e-139">Selezionare tutte le sottoscrizioni oppure quella contenente l'account di archiviazione da eliminare.</span><span class="sxs-lookup"><span data-stu-id="3d92e-139">Select all subscriptions or the subscription that contains the storage account you want to delete.</span></span>

    ![aggiungere sottoscrizione](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. <span data-ttu-id="3d92e-141">Passare all'account di archiviazione ottenuto in precedenza dall'URL del disco, selezionare i **contenitori BLOB** > **dischi rigidi virtuali** e cercare il disco rigido virtuale che impedisce di eliminare l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3d92e-141">Go to the storage account that we obtained from the disk URL earlier, select the **Blob Containers** > **vhds** and search for the VHD that prevents you delete the storage account.</span></span>
5. <span data-ttu-id="3d92e-142">Se viene trovato il disco rigido virtuale, controllare la colonna **Nome macchina virtuale** per trovare la macchina virtuale che sta usando tale disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="3d92e-142">If the VHD is found,  check the **VM Name** column to find the VM that is using this VHD.</span></span>

    ![Controllare la macchina virtuale](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. <span data-ttu-id="3d92e-144">Rimuovere il lease dal disco rigido virtuale tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3d92e-144">Remove the lease from the VHD by using Azure portal.</span></span> <span data-ttu-id="3d92e-145">Per ulteriori informazioni, vedere [Rimuovere il lease dal disco rigido virtuale](#remove-the-lease-from-the-vhd).</span><span class="sxs-lookup"><span data-stu-id="3d92e-145">For more information, see [Remove the lease from the VHD](#remove-the-lease-from-the-vhd).</span></span> 

7. <span data-ttu-id="3d92e-146">Passare a Esplora archivi di Azure, fare clic con il tasto destro del mouse sul disco rigido virtuale e quindi selezionare Elimina.</span><span class="sxs-lookup"><span data-stu-id="3d92e-146">Go to the Azure Storage Explorer, right-click the VHD and then select delete.</span></span>

8. <span data-ttu-id="3d92e-147">Elimina l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3d92e-147">Delete the storage account.</span></span>

### <a name="method-2---use-azure-portal"></a><span data-ttu-id="3d92e-148">Metodo 2: Usare il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3d92e-148">Method 2 - Use Azure portal</span></span> 

#### <a name="step-1-identify-the-vhd-that-prevent-deletion-of-the-storage-account"></a><span data-ttu-id="3d92e-149">Passaggio 1: identificare il disco rigido virtuale che impedisce l'eliminazione dell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="3d92e-149">Step 1: Identify the VHD that prevent deletion of the storage account</span></span>

1. <span data-ttu-id="3d92e-150">Eliminando l'account di archiviazione, si riceverà una finestra di dialogo con messaggio come la seguente:</span><span class="sxs-lookup"><span data-stu-id="3d92e-150">When you delete the storage account, you will receive a message dialog such as the following:</span></span> 

    ![Messaggio durante l'eliminazione dell'account di archiviazione](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. <span data-ttu-id="3d92e-152">Controllare l'**URL del disco** per identificare l'account di archiviazione e il disco rigido virtuale che impedisce di eliminare l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3d92e-152">Check the **Disk URL** to identify the storage account and the VHD that prevents you delete the storage account.</span></span> <span data-ttu-id="3d92e-153">Nell'esempio seguente la stringa che precede ".blob.core.windows.net" è il nome dell'account di archiviazione, mentre "SCCM2012-2015-08-28.vhd" è il nome del disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="3d92e-153">In the following example, the string before “.blob.core.windows.net “ is the storage account name, and "SCCM2012-2015-08-28.vhd" is the VHD name.</span></span>  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. <span data-ttu-id="3d92e-154">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3d92e-154">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
3. <span data-ttu-id="3d92e-155">Scegliere **Tutte le risorse** dal menu Hub.</span><span class="sxs-lookup"><span data-stu-id="3d92e-155">On the Hub menu, select **All resources**.</span></span> <span data-ttu-id="3d92e-156">Passare all'account di archiviazione e quindi selezionare **BLOB** > **dischi rigidi virtuali**.</span><span class="sxs-lookup"><span data-stu-id="3d92e-156">Go to the storage account, and then select **Blobs** > **vhds**.</span></span>

    ![Schermata del portale, con l'account di archiviazione e il contenitore "vhds" evidenziato](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. <span data-ttu-id="3d92e-158">Individuare il disco rigido virtuale ottenuto in precedenza dall'URL del disco.</span><span class="sxs-lookup"><span data-stu-id="3d92e-158">Locate the VHD that we obtained from the disk URL earlier.</span></span> <span data-ttu-id="3d92e-159">quindi determinare quale macchina virtuale sta usando il disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="3d92e-159">Then, determine which VM is using the VHD.</span></span> <span data-ttu-id="3d92e-160">In genere, è possibile determinare la macchina virtuale che contiene il disco rigido virtuale selezionando il nome di tale disco:</span><span class="sxs-lookup"><span data-stu-id="3d92e-160">Usually, you can determine which VM holds the VHD by checking name of the VHD:</span></span>

<span data-ttu-id="3d92e-161">Macchina virtuale nel modello di sviluppo di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3d92e-161">VM in Resource Manager development  model</span></span>

   * <span data-ttu-id="3d92e-162">I dischi sistema operativo in genere seguono questa convenzione di denominazione: VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="3d92e-162">OS disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="3d92e-163">I dischi dati in genere seguono questa convenzione di denominazione: VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="3d92e-163">Data disks generally follow this naming convention: VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

<span data-ttu-id="3d92e-164">Macchina virtuale nel modello di sviluppo classico</span><span class="sxs-lookup"><span data-stu-id="3d92e-164">VM in Classic development model</span></span>

   * <span data-ttu-id="3d92e-165">I dischi sistema operativo in genere seguono questa convenzione di denominazione: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="3d92e-165">OS disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>
   * <span data-ttu-id="3d92e-166">I dischi dati in genere seguono questa convenzione di denominazione: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span><span class="sxs-lookup"><span data-stu-id="3d92e-166">Data disks generally follow this naming convention: CloudServiceName-VMName-YYYY-MM-DD-HHMMSS.vhd</span></span>

#### <a name="step-2-remove-the-lease-from-the-vhd"></a><span data-ttu-id="3d92e-167">Passaggio 2: Rimuovere il lease dal disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="3d92e-167">Step 2: Remove the lease from the VHD</span></span>

<span data-ttu-id="3d92e-168">[Rimuovere il lease dal disco rigido virtuale](#remove-the-lease-from-the-vhd), quindi eliminare l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3d92e-168">[Remove the lease from the VHD](#remove-the-lease-from-the-vhd), and then delete the storage account.</span></span>

## <a name="what-is-a-lease"></a><span data-ttu-id="3d92e-169">Che cos'è un lease?</span><span class="sxs-lookup"><span data-stu-id="3d92e-169">What is a lease?</span></span>
<span data-ttu-id="3d92e-170">Un lease è un blocco che può essere usato per controllare l'accesso a un BLOB (ad esempio, un disco rigido virtuale).</span><span class="sxs-lookup"><span data-stu-id="3d92e-170">A lease is a lock that can be used to control access to a blob (for example, a VHD).</span></span> <span data-ttu-id="3d92e-171">Quando un BLOB è in stato di lease, solo i proprietari del lease possono accedere al BLOB.</span><span class="sxs-lookup"><span data-stu-id="3d92e-171">When a blob is leased, only the owners of the lease can access the blob.</span></span> <span data-ttu-id="3d92e-172">Un lease è importante per i motivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3d92e-172">A lease is important for the following reasons:</span></span>

* <span data-ttu-id="3d92e-173">Impedisce il danneggiamento dei dati se più proprietari tentano di scrivere nella stessa parte del BLOB nello stesso momento.</span><span class="sxs-lookup"><span data-stu-id="3d92e-173">It prevents data corruption if multiple owners try to write to the same portion of the blob at the same time.</span></span>
* <span data-ttu-id="3d92e-174">Impedisce l'eliminazione del BLOB se in uso (ad esempio, da parte di una macchina virtuale).</span><span class="sxs-lookup"><span data-stu-id="3d92e-174">It prevents the blob from being deleted if something is actively using it (for example, a VM).</span></span>
* <span data-ttu-id="3d92e-175">Impedisce l'eliminazione dell'account di archiviazione se in uso (ad esempio, da parte di una macchina virtuale).</span><span class="sxs-lookup"><span data-stu-id="3d92e-175">It prevents the storage account from being deleted if something is actively using it (for example, a VM).</span></span>

### <a name="remove-the-lease-from-the-vhd"></a><span data-ttu-id="3d92e-176">Rimuovere il lease dal disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="3d92e-176">Remove the lease from the VHD</span></span>
<span data-ttu-id="3d92e-177">Se il disco rigido virtuale è un disco sistema operativo, è necessario eliminare la macchina virtuale per rimuovere il lease:</span><span class="sxs-lookup"><span data-stu-id="3d92e-177">If the VHD is an OS disk, you must delete the VM to remove the lease:</span></span>

1. <span data-ttu-id="3d92e-178">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3d92e-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3d92e-179">Dal menu **Hub** scegliere **Macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="3d92e-179">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="3d92e-180">Selezionare la macchina virtuale che contiene un lease sul disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="3d92e-180">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="3d92e-181">Assicurarsi che la macchina virtuale non sia in uso e che non sia più necessaria.</span><span class="sxs-lookup"><span data-stu-id="3d92e-181">Make sure that nothing is actively using the virtual machine, and that you no longer need the virtual machine.</span></span>
5. <span data-ttu-id="3d92e-182">Nella parte superiore del pannello **VM details** (Dettagli macchina virtuale) selezionare **Elimina** e quindi fare clic su **Sì** per confermare.</span><span class="sxs-lookup"><span data-stu-id="3d92e-182">At the top of the **VM details** blade, select **Delete**, and then click **Yes** to confirm.</span></span>
6. <span data-ttu-id="3d92e-183">La macchina virtuale viene eliminata, ma il disco rigido virtuale può essere mantenuto.</span><span class="sxs-lookup"><span data-stu-id="3d92e-183">The VM should be deleted, but the VHD can be retained.</span></span> <span data-ttu-id="3d92e-184">Tuttavia, nel disco rigido virtuale non deve più essere presente un lease.</span><span class="sxs-lookup"><span data-stu-id="3d92e-184">However, the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="3d92e-185">Il rilascio del lease può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="3d92e-185">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="3d92e-186">Per verificare che il lease sia stato rilasciato, passare a **Tutte le risorse** > **nome account di archiviazione** > **BLOB** > **dischi rigidi virtuali**.</span><span class="sxs-lookup"><span data-stu-id="3d92e-186">To verify that the lease is released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="3d92e-187">Nel riquadro **Proprietà BLOB** il valore **Stato lease** deve essere **Sbloccato**.</span><span class="sxs-lookup"><span data-stu-id="3d92e-187">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

<span data-ttu-id="3d92e-188">Se il disco rigido virtuale è un disco dati, scollegarlo dalla macchina virtuale per rimuovere il lease:</span><span class="sxs-lookup"><span data-stu-id="3d92e-188">If the VHD is a data disk, detach the VHD from the VM to remove the lease:</span></span>

1. <span data-ttu-id="3d92e-189">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3d92e-189">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3d92e-190">Dal menu **Hub** scegliere **Macchine virtuali**.</span><span class="sxs-lookup"><span data-stu-id="3d92e-190">On the **Hub** menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="3d92e-191">Selezionare la macchina virtuale che contiene un lease sul disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="3d92e-191">Select the VM that holds a lease on the VHD.</span></span>
4. <span data-ttu-id="3d92e-192">Selezionare **Dischi** nel pannello **VM details** (Dettagli macchina virtuale).</span><span class="sxs-lookup"><span data-stu-id="3d92e-192">Select **Disks** on the **VM details** blade.</span></span>
5. <span data-ttu-id="3d92e-193">Selezionare il disco dati che contiene un lease sul disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="3d92e-193">Select the data disk that holds a lease on the VHD.</span></span> <span data-ttu-id="3d92e-194">È possibile determinare il disco rigido virtuale collegato al disco controllando l'URL del disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="3d92e-194">You can determine which VHD is attached in the disk by checking the URL of the VHD.</span></span>
6. <span data-ttu-id="3d92e-195">Stabilire con certezza che il disco dati non è in uso.</span><span class="sxs-lookup"><span data-stu-id="3d92e-195">Determine with certainty that nothing is actively using the data disk.</span></span>
7. <span data-ttu-id="3d92e-196">Fare clic su **Scollega** nel pannello **Dettagli disco**.</span><span class="sxs-lookup"><span data-stu-id="3d92e-196">Click **Detach** on the **Disk details** blade.</span></span>
8. <span data-ttu-id="3d92e-197">Il disco deve ora essere scollegato dalla macchina virtuale e nel disco rigido virtuale non deve più essere presente un lease.</span><span class="sxs-lookup"><span data-stu-id="3d92e-197">The disk should now be detached from the VM, and the VHD should no longer have a lease on it.</span></span> <span data-ttu-id="3d92e-198">Il rilascio del lease può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="3d92e-198">It may take a few minutes for the lease to be released.</span></span> <span data-ttu-id="3d92e-199">Per verificare che il lease sia stato rilasciato, passare a **Tutte le risorse** > **nome account di archiviazione** > **BLOB** > **dischi rigidi virtuali**.</span><span class="sxs-lookup"><span data-stu-id="3d92e-199">To verify that the lease has been released, go to **All resources** > **Storage Account Name** > **Blobs** > **vhds**.</span></span> <span data-ttu-id="3d92e-200">Nel riquadro **Proprietà BLOB** il valore **Stato lease** deve essere **Sbloccato**.</span><span class="sxs-lookup"><span data-stu-id="3d92e-200">In the **Blob properties** pane, the **Lease Status** value should be **Unlocked**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d92e-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3d92e-201">Next steps</span></span>
* [<span data-ttu-id="3d92e-202">Eliminare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="3d92e-202">Delete a storage account</span></span>](storage-create-storage-account.md#delete-a-storage-account)
* [<span data-ttu-id="3d92e-203">Procedura: Interrompere il lease bloccato di archiviazione BLOB in Microsoft Azure (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="3d92e-203">How to break the locked lease of blob storage in Microsoft Azure (PowerShell)</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
