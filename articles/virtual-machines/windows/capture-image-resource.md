---
title: aaaCreate un'immagine gestita in Azure | Documenti Microsoft
description: "Creare un'immagine gestita di un disco rigido virtuale o una macchina virtuale generalizzati in Azure. Le immagini può essere utilizzati toocreate più macchine virtuali che usano dischi gestiti."
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
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="70deb-104">Creare un'immagine gestita di una macchina virtuale generalizzata in Azure</span><span class="sxs-lookup"><span data-stu-id="70deb-104">Create a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="70deb-105">È possibile creare una risorsa immagine gestita da una macchina virtuale generalizzata archiviata come disco gestito o come disco non gestito in un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="70deb-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disk in a storage account.</span></span> <span data-ttu-id="70deb-106">Hello immagine può quindi essere utilizzato toocreate più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="70deb-106">hello image can then be used toocreate multiple VMs.</span></span> 


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="70deb-107">Generalizzare hello macchina virtuale di Windows tramite Sysprep</span><span class="sxs-lookup"><span data-stu-id="70deb-107">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="70deb-108">Sysprep consente di rimuovere tutte le informazioni sull'account personale, tra le altre cose e lo prepara hello macchina toobe utilizzato come immagine.</span><span class="sxs-lookup"><span data-stu-id="70deb-108">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="70deb-109">Per ulteriori informazioni su Sysprep, vedere [come tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="70deb-109">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="70deb-110">Assicurarsi che i ruoli del server hello in esecuzione sul computer hello sono supportati da Sysprep.</span><span class="sxs-lookup"><span data-stu-id="70deb-110">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="70deb-111">Per ulteriori informazioni, vedere [Supporto Sysprep per i ruoli server](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="70deb-111">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="70deb-112">Se si esegue Sysprep prima di caricare il disco rigido virtuale tooAzure per hello prima volta, assicurarsi di avere [preparato la macchina virtuale](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) prima di eseguire Sysprep.</span><span class="sxs-lookup"><span data-stu-id="70deb-112">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="70deb-113">Accedi toohello macchina virtuale di Windows.</span><span class="sxs-lookup"><span data-stu-id="70deb-113">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="70deb-114">Aprire una finestra del prompt dei comandi hello come amministratore.</span><span class="sxs-lookup"><span data-stu-id="70deb-114">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="70deb-115">Modificare anche le directory hello**%windir%\system32\sysprep**, quindi eseguire `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="70deb-115">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="70deb-116">In hello **System Preparation Tool** nella finestra di dialogo **immettere sistema Out-of-Box guidata**e assicurarsi che tale hello **Generalize** casella di controllo è selezionata.</span><span class="sxs-lookup"><span data-stu-id="70deb-116">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="70deb-117">In **Opzioni di arresto del sistema** selezionare **Arresta il sistema**.</span><span class="sxs-lookup"><span data-stu-id="70deb-117">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="70deb-118">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="70deb-118">Click **OK**.</span></span>
   
    ![Avvio di Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="70deb-120">Al termine di Sysprep, arresta macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="70deb-120">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="70deb-121">Non riavviare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="70deb-121">Do not restart hello VM.</span></span>


## <a name="create-a-managed-image-in-hello-portal"></a><span data-ttu-id="70deb-122">Creare un'immagine gestita nel portale di hello</span><span class="sxs-lookup"><span data-stu-id="70deb-122">Create a managed image in hello portal</span></span> 

1. <span data-ttu-id="70deb-123">Aprire hello [portale](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="70deb-123">Open hello [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="70deb-124">Fare clic su hello toocreate sul segno più di una nuova risorsa.</span><span class="sxs-lookup"><span data-stu-id="70deb-124">Click hello plus sign toocreate a new resource.</span></span>
3. <span data-ttu-id="70deb-125">Nella ricerca di filtro hello, digitare **immagine**.</span><span class="sxs-lookup"><span data-stu-id="70deb-125">In hello filter search, type **Image**.</span></span>
4. <span data-ttu-id="70deb-126">Selezionare **immagine** dai risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="70deb-126">Select **Image** from hello results.</span></span>
5. <span data-ttu-id="70deb-127">In hello **immagine** pannello, fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="70deb-127">In hello **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="70deb-128">In **nome**, digitare un nome per l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="70deb-128">In **Name**, type a name for hello image.</span></span>
7. <span data-ttu-id="70deb-129">Se si dispone di più di una sottoscrizione, selezionare hello corretta in da hello **sottoscrizione** elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="70deb-129">If you have more than one subscription, select hello correct one from hello **Subscription** drop-down.</span></span>
7. <span data-ttu-id="70deb-130">In **gruppo di risorse** selezionare **Crea nuovo** e digitare un nome o selezionare **da esistente** e selezionare un toouse gruppo di risorse dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="70deb-130">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group toouse from hello drop-down list.</span></span>
8. <span data-ttu-id="70deb-131">In **percorso**, scegliere il percorso di hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="70deb-131">In **Location**, choose hello location of your resource group.</span></span>
9. <span data-ttu-id="70deb-132">In **tipo di sistema operativo** selezionare il tipo di hello del sistema operativo Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="70deb-132">In **OS type** select hello type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="70deb-133">In **blob di archiviazione**, fare clic su **Sfoglia** toolook per hello VHD nell'archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="70deb-133">In **Storage blob**, click **Browse** toolook for hello VHD in your Azure storage.</span></span>
12. <span data-ttu-id="70deb-134">In **Tipo di account** scegliere Standard_LRS o Premium_LRS.</span><span class="sxs-lookup"><span data-stu-id="70deb-134">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="70deb-135">Il tipo Standard usa unità disco rigido, mente l'account Premium usa unità SSD.</span><span class="sxs-lookup"><span data-stu-id="70deb-135">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="70deb-136">Entrambi usano l'archiviazione con ridondanza locale.</span><span class="sxs-lookup"><span data-stu-id="70deb-136">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="70deb-137">In **la cache del disco** selezionare hello disco appropriato, opzione di memorizzazione nella cache.</span><span class="sxs-lookup"><span data-stu-id="70deb-137">In **Disk caching** select hello appropriate disk caching option.</span></span> <span data-ttu-id="70deb-138">opzioni di Hello sono **Nessuno**, **Read-only** e **lettura/scrittura**.</span><span class="sxs-lookup"><span data-stu-id="70deb-138">hello options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="70deb-139">Facoltativo: È possibile anche aggiungere un'immagine di toohello disco dati esistente, fare clic su **+ Aggiungi disco di dati**.</span><span class="sxs-lookup"><span data-stu-id="70deb-139">Optional: You can also add an existing data disk toohello image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="70deb-140">Dopo aver completato le selezioni, fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="70deb-140">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="70deb-141">Dopo aver creato l'immagine di hello, verrà visualizzato come un **immagine** risorsa nell'elenco di hello delle risorse nel gruppo di risorse hello scelto.</span><span class="sxs-lookup"><span data-stu-id="70deb-141">After hello image is created, you will see it as an **Image** resource in hello list of resources in hello resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="70deb-142">Creare un'immagine gestita di una macchina virtuale tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="70deb-142">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="70deb-143">Creazione di un'immagine direttamente da hello che VM assicura che l'immagine hello include tutti i dischi di hello associati hello macchina virtuale, compresi hello disco del sistema operativo e qualsiasi disco dati.</span><span class="sxs-lookup"><span data-stu-id="70deb-143">Creating an image directly from hello VM ensures that hello image includes all of hello disks associated with hello VM, including hello OS Disk and any data disks.</span></span>


<span data-ttu-id="70deb-144">Prima di iniziare, assicurarsi di aver hello la versione più recente del modulo AzureRM.Compute PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="70deb-144">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="70deb-145">Eseguire hello seguenti comando tooinstall.</span><span class="sxs-lookup"><span data-stu-id="70deb-145">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="70deb-146">Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="70deb-146">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


1. <span data-ttu-id="70deb-147">Creare alcune variabili.</span><span class="sxs-lookup"><span data-stu-id="70deb-147">Create some variables.</span></span>

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="70deb-148">Verificare che hello che VM è stato deallocato.</span><span class="sxs-lookup"><span data-stu-id="70deb-148">Make sure hello VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="70deb-149">Impostare lo stato di hello della macchina virtuale hello troppo**generalizzato**.</span><span class="sxs-lookup"><span data-stu-id="70deb-149">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="70deb-150">Ottenere una macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="70deb-150">Get hello virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="70deb-151">Creare una configurazione immagine hello.</span><span class="sxs-lookup"><span data-stu-id="70deb-151">Create hello image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="70deb-152">Creare l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="70deb-152">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="70deb-153">Creare un'immagine gestita di un disco rigido virtuale tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="70deb-153">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="70deb-154">Creare un'immagine gestita tramite il disco rigido virtuale del sistema operativo generalizzato.</span><span class="sxs-lookup"><span data-stu-id="70deb-154">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="70deb-155">Innanzitutto, impostare i parametri comuni di hello:</span><span class="sxs-lookup"><span data-stu-id="70deb-155">First, set hello common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="70deb-156">Hello Step\deallocate macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="70deb-156">Step\deallocate hello VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="70deb-157">Contrassegnare hello VM come generalizzato.</span><span class="sxs-lookup"><span data-stu-id="70deb-157">Mark hello VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="70deb-158">Creare l'immagine di hello utilizzando il disco rigido virtuale generalizzato di sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="70deb-158">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="70deb-159">Creare un'immagine gestita da uno snapshot tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="70deb-159">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="70deb-160">È anche possibile creare un'immagine gestita da uno snapshot del disco rigido virtuale da una macchina virtuale generalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="70deb-160">You can also create a managed image from a snapshot of hello VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="70deb-161">Creare alcune variabili.</span><span class="sxs-lookup"><span data-stu-id="70deb-161">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="70deb-162">Ottenere snapshot di hello.</span><span class="sxs-lookup"><span data-stu-id="70deb-162">Get hello snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="70deb-163">Creare una configurazione immagine hello.</span><span class="sxs-lookup"><span data-stu-id="70deb-163">Create hello image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="70deb-164">Creare l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="70deb-164">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="70deb-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="70deb-165">Next steps</span></span>
- <span data-ttu-id="70deb-166">È ora possibile [creare una macchina virtuale dall'immagine gestito hello generalizzato](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="70deb-166">Now you can [create a VM from hello generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>    

