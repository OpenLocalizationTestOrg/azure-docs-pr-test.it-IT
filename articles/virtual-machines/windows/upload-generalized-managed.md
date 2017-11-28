---
title: una macchina virtuale Azure gestito da un disco rigido virtuale generalizzato locale aaaCreate | Documenti Microsoft
description: Caricare un tooAzure disco rigido virtuale generalizzato e usarlo toocreate nuove macchine virtuali, nel modello di distribuzione di gestione risorse di hello.
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
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a><span data-ttu-id="a5da2-103">Caricare un disco rigido virtuale generalizzato e usarlo toocreate nuove macchine virtuali in Azure</span><span class="sxs-lookup"><span data-stu-id="a5da2-103">Upload a generalized VHD and use it toocreate new VMs in Azure</span></span>

<span data-ttu-id="a5da2-104">In questo argomento illustra tooupload PowerShell utilizzando un disco rigido virtuale di un tooAzure macchina virtuale generalizzata, creare un'immagine da VHD hello e creare una nuova macchina virtuale da quell'immagine.</span><span class="sxs-lookup"><span data-stu-id="a5da2-104">This topic walks you through using PowerShell tooupload a VHD of a generalized VM tooAzure, create an image from hello VHD and create a new VM from that image.</span></span> <span data-ttu-id="a5da2-105">È possibile caricare un disco rigido virtuale esportato da uno strumento di virtualizzazione locale o da un altro cloud.</span><span class="sxs-lookup"><span data-stu-id="a5da2-105">You can upload a VHD exported from an on-premises virtualization tool or from another cloud.</span></span> <span data-ttu-id="a5da2-106">Utilizzando [dischi gestiti](managed-disks-overview.md) per hello semplifica la gestione delle macchine Virtuali hello nuova macchina virtuale e fornisce una migliore disponibilità quando hello VM viene inserito in un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="a5da2-106">Using [Managed Disks](managed-disks-overview.md) for hello new VM simplifies hello VM managment and provides better availability when hello VM is placed in an availability set.</span></span> 

<span data-ttu-id="a5da2-107">Se si desidera toouse uno script di esempio, vedere [tooupload script tooAzure un disco rigido virtuale di esempio e creare una nuova macchina virtuale](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span><span class="sxs-lookup"><span data-stu-id="a5da2-107">If you want toouse a sample script, see [Sample script tooupload a VHD tooAzure and create a new VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a5da2-108">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="a5da2-108">Before you begin</span></span>

- <span data-ttu-id="a5da2-109">Prima di caricare qualsiasi tooAzure disco rigido virtuale, è necessario seguire [preparare un tooAzure tooupload Windows VHD o VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a5da2-109">Before uploading any VHD tooAzure, you should follow [Prepare a Windows VHD or VHDX tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
- <span data-ttu-id="a5da2-110">Revisione [pianificare la migrazione di hello di dischi tooManaged](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) prima di avviare la migrazione troppo[dischi gestiti](managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a5da2-110">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration too[Managed Disks](managed-disks-overview.md).</span></span>
- <span data-ttu-id="a5da2-111">Assicurarsi di aver hello la versione più recente del modulo AzureRM.Compute PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="a5da2-111">Make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="a5da2-112">Eseguire hello seguenti comando tooinstall.</span><span class="sxs-lookup"><span data-stu-id="a5da2-112">Run hello following command tooinstall it.</span></span>

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    <span data-ttu-id="a5da2-113">Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a5da2-113">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="a5da2-114">Generalizzare hello macchina virtuale di Windows tramite Sysprep</span><span class="sxs-lookup"><span data-stu-id="a5da2-114">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="a5da2-115">Sysprep consente di rimuovere tutte le informazioni sull'account personale, tra le altre cose e lo prepara hello macchina toobe utilizzato come immagine.</span><span class="sxs-lookup"><span data-stu-id="a5da2-115">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="a5da2-116">Per ulteriori informazioni su Sysprep, vedere [come tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5da2-116">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="a5da2-117">Assicurarsi che i ruoli del server hello in esecuzione sul computer hello sono supportati da Sysprep.</span><span class="sxs-lookup"><span data-stu-id="a5da2-117">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="a5da2-118">Per ulteriori informazioni, vedere [Supporto Sysprep per i ruoli server](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="a5da2-118">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a5da2-119">Se si esegue Sysprep prima di caricare il disco rigido virtuale tooAzure per hello prima volta, assicurarsi di avere [preparato la macchina virtuale](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) prima di eseguire Sysprep.</span><span class="sxs-lookup"><span data-stu-id="a5da2-119">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="a5da2-120">Accedi toohello macchina virtuale di Windows.</span><span class="sxs-lookup"><span data-stu-id="a5da2-120">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="a5da2-121">Aprire una finestra del prompt dei comandi hello come amministratore.</span><span class="sxs-lookup"><span data-stu-id="a5da2-121">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="a5da2-122">Modificare anche le directory hello**%windir%\system32\sysprep**, quindi eseguire `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="a5da2-122">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="a5da2-123">In hello **System Preparation Tool** nella finestra di dialogo **immettere sistema Out-of-Box guidata**e assicurarsi che tale hello **Generalize** casella di controllo è selezionata.</span><span class="sxs-lookup"><span data-stu-id="a5da2-123">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="a5da2-124">In **Opzioni di arresto del sistema** selezionare **Arresta il sistema**.</span><span class="sxs-lookup"><span data-stu-id="a5da2-124">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="a5da2-125">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5da2-125">Click **OK**.</span></span>
   
    ![Avvio di Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="a5da2-127">Al termine di Sysprep, arresta macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="a5da2-127">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="a5da2-128">Non riavviare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a5da2-128">Do not restart hello VM.</span></span>



## <a name="log-in-tooazure"></a><span data-ttu-id="a5da2-129">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="a5da2-129">Log in tooAzure</span></span>
<span data-ttu-id="a5da2-130">Se si dispone già di PowerShell versione 1.4 o versione successiva installato, leggere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a5da2-130">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="a5da2-131">Aprire Azure PowerShell e accedere tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="a5da2-131">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="a5da2-132">Una finestra popup viene aperto per si tooenter le credenziali dell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="a5da2-132">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="a5da2-133">Ottenere l'ID sottoscrizione hello per le sottoscrizioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="a5da2-133">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="a5da2-134">Set hello sottoscrizione corretta utilizzando l'ID di sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="a5da2-134">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="a5da2-135">Sostituire  *<subscriptionID>*  con ID hello hello correggere sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a5da2-135">Replace *<subscriptionID>* with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a><span data-ttu-id="a5da2-136">Ottenere l'account di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="a5da2-136">Get hello storage account</span></span>
<span data-ttu-id="a5da2-137">È necessario un account di archiviazione nell'immagine di macchina virtuale di Azure toostore hello caricato.</span><span class="sxs-lookup"><span data-stu-id="a5da2-137">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="a5da2-138">È possibile usare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="a5da2-138">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="a5da2-139">Se si utilizzerà hello VHD toocreate un disco gestito per una macchina virtuale, posizione dell'account di archiviazione hello deve essere nello stesso percorso hello in cui si creano hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a5da2-139">If you will be using hello VHD toocreate a managed disk for a VM, hello storage account location must be same hello location where you will be creating hello VM.</span></span>

<span data-ttu-id="a5da2-140">account di archiviazione disponibili hello tooshow, digitare:</span><span class="sxs-lookup"><span data-stu-id="a5da2-140">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="a5da2-141">Se si desidera toouse un account di archiviazione esistente, procedere toohello [immagine di macchina virtuale di caricamento hello](#upload-the-vm-vhd-to-your-storage-account) sezione.</span><span class="sxs-lookup"><span data-stu-id="a5da2-141">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="a5da2-142">Se è necessario un account di archiviazione toocreate, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="a5da2-142">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="a5da2-143">È necessario il nome di hello hello del gruppo di risorse in cui deve essere creato l'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="a5da2-143">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="a5da2-144">toofind out tutti i gruppi di risorse hello nella sottoscrizione di tipo sono:</span><span class="sxs-lookup"><span data-stu-id="a5da2-144">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="a5da2-145">un gruppo di risorse denominato toocreate **myResourceGroup** in hello **Stati Uniti orientali** area, digitare:</span><span class="sxs-lookup"><span data-stu-id="a5da2-145">toocreate a resource group named **myResourceGroup** in hello **East US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. <span data-ttu-id="a5da2-146">Creare un account di archiviazione denominato **mystorageaccount** in questo gruppo di risorse utilizzando hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a5da2-146">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="a5da2-147">I valori validi -SkuName validi sono:</span><span class="sxs-lookup"><span data-stu-id="a5da2-147">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="a5da2-148">**Standard_LRS**: archiviazione con ridondanza locale.</span><span class="sxs-lookup"><span data-stu-id="a5da2-148">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="a5da2-149">**Standard_ZRS**: archiviazione con ridondanza della zona.</span><span class="sxs-lookup"><span data-stu-id="a5da2-149">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="a5da2-150">**Standard_GRS**: archiviazione con ridondanza geografica.</span><span class="sxs-lookup"><span data-stu-id="a5da2-150">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="a5da2-151">**Standard_RAGRS**: archiviazione con ridondanza geografica e accesso in lettura.</span><span class="sxs-lookup"><span data-stu-id="a5da2-151">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="a5da2-152">**Premium_LRS**: archiviazione con ridondanza locale Premium.</span><span class="sxs-lookup"><span data-stu-id="a5da2-152">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="a5da2-153">Caricare l'account di archiviazione tooyour hello disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="a5da2-153">Upload hello VHD tooyour storage account</span></span>

<span data-ttu-id="a5da2-154">Hello utilizzare [Aggiungi AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) contenitore cmdlet tooupload hello VHD tooa nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a5da2-154">Use hello [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="a5da2-155">In questo esempio caricamenti hello file *myVHD.vhd* da *"dischi rigidi C:\Users\Public\Documents\Virtual\"*  tooa account di archiviazione denominato *mystorageaccount*in hello *myResourceGroup* gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="a5da2-155">This example uploads hello file *myVHD.vhd* from *"C:\Users\Public\Documents\Virtual hard disks\"* tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="a5da2-156">sarà inseriti file Hello contenitore hello denominato *mycontainer* e sarà il nuovo nome di file hello *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="a5da2-156">hello file will be placed into hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="a5da2-157">Se ha esito positivo, si otterrà una risposta simile toothis simile:</span><span class="sxs-lookup"><span data-stu-id="a5da2-157">If successful, you get a response that looks similar toothis:</span></span>

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="a5da2-158">La connessione di rete e delle dimensioni di hello del file di disco rigido virtuale, questo comando potrebbe richiedere qualche minuto toocomplete</span><span class="sxs-lookup"><span data-stu-id="a5da2-158">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

<span data-ttu-id="a5da2-159">Salvare hello **URI di destinazione** percorso toouse in seguito se si prevede un disco gestito toocreate o una nuova macchina virtuale utilizzando hello caricati disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="a5da2-159">Save hello **Destination URI** path toouse later if you are going toocreate a managed disk or a new VM using hello uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="a5da2-160">Altre opzioni per il caricamento di un disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="a5da2-160">Other options for uploading a VHD</span></span>
 
 
<span data-ttu-id="a5da2-161">È inoltre possibile caricare un account di archiviazione tooyour disco rigido virtuale utilizzando uno dei seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="a5da2-161">You can also upload a VHD tooyour storage account using one of hello following:</span></span>

- [<span data-ttu-id="a5da2-162">AzCopy</span><span class="sxs-lookup"><span data-stu-id="a5da2-162">AzCopy</span></span>](http://aka.ms/downloadazcopy)
- [<span data-ttu-id="a5da2-163">API Copy Blob di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a5da2-163">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [<span data-ttu-id="a5da2-164">Caricamento di BLOB in Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="a5da2-164">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
- [<span data-ttu-id="a5da2-165">Materiale di riferimento dell'API REST del servizio di importazione/esportazione dell'archiviazione</span><span class="sxs-lookup"><span data-stu-id="a5da2-165">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)
-   <span data-ttu-id="a5da2-166">È consigliabile usare il servizio di importazione/esportazione se il tempo di caricamento stimato è maggiore di 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="a5da2-166">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="a5da2-167">È possibile utilizzare [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) ora hello tooestimate dall'unità di dimensioni e il trasferimento di dati.</span><span class="sxs-lookup"><span data-stu-id="a5da2-167">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span> 
    <span data-ttu-id="a5da2-168">Importazione/esportazione può essere utilizzato l'account di archiviazione standard tooa toocopy.</span><span class="sxs-lookup"><span data-stu-id="a5da2-168">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="a5da2-169">Sarà necessario toocopy dall'account di archiviazione toopremium archiviazione standard usando uno strumento come AzCopy.</span><span class="sxs-lookup"><span data-stu-id="a5da2-169">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a><span data-ttu-id="a5da2-170">Creare un'immagine da hello caricata disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="a5da2-170">Create a managed image from hello uploaded VHD</span></span> 

<span data-ttu-id="a5da2-171">Creare un'immagine gestita tramite il disco rigido virtuale del sistema operativo generalizzato.</span><span class="sxs-lookup"><span data-stu-id="a5da2-171">Create a managed image using your generalized OS VHD.</span></span> <span data-ttu-id="a5da2-172">Sostituire i valori hello con informazioni personali.</span><span class="sxs-lookup"><span data-stu-id="a5da2-172">Replace hello values with your own information.</span></span>


1.  <span data-ttu-id="a5da2-173">Innanzitutto, impostare i parametri comuni di hello:</span><span class="sxs-lookup"><span data-stu-id="a5da2-173">First, set hello common parameters:</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  <span data-ttu-id="a5da2-174">Creare l'immagine di hello utilizzando il disco rigido virtuale generalizzato di sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="a5da2-174">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="a5da2-175">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="a5da2-175">Create a virtual network</span></span>
<span data-ttu-id="a5da2-176">Creare reti virtuali hello e la subnet di hello [rete virtuale](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a5da2-176">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="a5da2-177">Creare subnet hello.</span><span class="sxs-lookup"><span data-stu-id="a5da2-177">Create hello subnet.</span></span> <span data-ttu-id="a5da2-178">Questo esempio viene creata una subnet denominata *mySubnet* con prefisso di indirizzo hello *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="a5da2-178">This example creates a subnet named *mySubnet* with hello address prefix of *10.0.0.0/24*.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="a5da2-179">Creare la rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="a5da2-179">Create hello virtual network.</span></span> <span data-ttu-id="a5da2-180">Questo esempio viene creata una rete virtuale denominata *myVnet* con prefisso di indirizzo hello *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="a5da2-180">This example creates a virtual network named *myVnet* with hello address prefix of *10.0.0.0/16*.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="a5da2-181">Creare un indirizzo IP pubblico e un'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="a5da2-181">Create a public IP address and network interface</span></span>

<span data-ttu-id="a5da2-182">comunicazione tooenable con hello di macchina virtuale nella rete virtuale hello, è necessario un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="a5da2-182">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="a5da2-183">Creare un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="a5da2-183">Create a public IP address.</span></span> <span data-ttu-id="a5da2-184">In questo esempio viene creato un indirizzo IP pubblico denominato *myPip*.</span><span class="sxs-lookup"><span data-stu-id="a5da2-184">This example creates a public IP address named *myPip*.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="a5da2-185">Creare una scheda di rete hello.</span><span class="sxs-lookup"><span data-stu-id="a5da2-185">Create hello NIC.</span></span> <span data-ttu-id="a5da2-186">In questo esempio viene creata una scheda NIC denominata **myNic**.</span><span class="sxs-lookup"><span data-stu-id="a5da2-186">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="a5da2-187">Creare gruppi di sicurezza di rete hello e una regola di RDP</span><span class="sxs-lookup"><span data-stu-id="a5da2-187">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="a5da2-188">toobe toolog in grado di tooyour macchina virtuale tramite RDP, è necessario toohave una regola di sicurezza di rete (gruppo) che consente l'accesso RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="a5da2-188">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="a5da2-189">In questo esempio viene creato un gruppo di sicurezza di rete denominato *myNsg* contenente una regola denominata *myRdpRule* che consente il traffico RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="a5da2-189">This example creates an NSG named *myNsg* that contains a rule called *myRdpRule* that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="a5da2-190">Per ulteriori informazioni su NSGs, vedere [apertura di porte tooa VM in Azure utilizzando PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a5da2-190">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="a5da2-191">Creare una variabile per la rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="a5da2-191">Create a variable for hello virtual network</span></span>

<span data-ttu-id="a5da2-192">Creare una variabile per la rete virtuale hello completata.</span><span class="sxs-lookup"><span data-stu-id="a5da2-192">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="a5da2-193">Ottenere le credenziali di hello per hello VM</span><span class="sxs-lookup"><span data-stu-id="a5da2-193">Get hello credentials for hello VM</span></span>

<span data-ttu-id="a5da2-194">Hello cmdlet riportato di seguito verrà aperta una finestra in cui è necessario specificare un nuovo toouse di nome e una password utente come account amministratore locale hello per accedere in remoto alle macchine Virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="a5da2-194">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a><span data-ttu-id="a5da2-195">Aggiungere hello nome della macchina virtuale e configurazione della macchina virtuale toohello dimensioni.</span><span class="sxs-lookup"><span data-stu-id="a5da2-195">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="a5da2-196">Immagine di macchina virtuale hello set come immagine di origine per hello nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a5da2-196">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="a5da2-197">Impostare l'immagine di origine hello usando un ID di hello dell'immagine di macchina virtuale hello gestito.</span><span class="sxs-lookup"><span data-stu-id="a5da2-197">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="a5da2-198">Impostare la configurazione del sistema operativo hello e aggiungere una scheda di rete hello.</span><span class="sxs-lookup"><span data-stu-id="a5da2-198">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="a5da2-199">Immettere un tipo di archiviazione hello (PremiumLRS o StandardLRS) e dimensioni hello del disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="a5da2-199">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="a5da2-200">In questo esempio imposta il tipo di account hello troppo*PremiumLRS*, hello dimensioni disco troppo*128 GB* e memorizzazione nella cache del disco troppo*ReadWrite*.</span><span class="sxs-lookup"><span data-stu-id="a5da2-200">This example sets hello account type too*PremiumLRS*, hello disk size too*128 GB* and disk caching too*ReadWrite*.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="a5da2-201">Creare VM hello</span><span class="sxs-lookup"><span data-stu-id="a5da2-201">Create hello VM</span></span>

<span data-ttu-id="a5da2-202">Creare una nuova macchina virtuale utilizzando la configurazione di hello archiviati in hello hello **$vm** variabile.</span><span class="sxs-lookup"><span data-stu-id="a5da2-202">Create hello new VM using hello configuration stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="a5da2-203">Verificare che hello che è stata creata una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a5da2-203">Verify that hello VM was created</span></span>
<span data-ttu-id="a5da2-204">Al termine, si dovrebbe essere hello macchina virtuale appena creata in hello [portale di Azure](https://portal.azure.com) in **Sfoglia** > **macchine virtuali**, o tramite hello seguenti Comandi di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a5da2-204">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="a5da2-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a5da2-205">Next steps</span></span>

<span data-ttu-id="a5da2-206">toosign tooyour nuova macchina virtuale, toohello Sfoglia VM in hello [portale](https://portal.azure.com), fare clic su **Connetti**e il file desktop remoto aprire hello.</span><span class="sxs-lookup"><span data-stu-id="a5da2-206">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="a5da2-207">Utilizzare le credenziali dell'account hello del toosign macchina virtuale originale tooyour nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a5da2-207">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="a5da2-208">Per ulteriori informazioni, vedere [come tooconnect e tooan virtuali di Azure di accesso del computer che eseguono Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a5da2-208">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

