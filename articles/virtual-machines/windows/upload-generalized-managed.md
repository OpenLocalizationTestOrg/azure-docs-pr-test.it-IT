---
title: Creare una macchina virtuale di Azure gestita da un disco rigido virtuale locale generalizzato | Microsoft Docs
description: Caricare un disco rigido virtuale generalizzato in Azure e usarlo per creare nuove macchine virtuali nel modello di distribuzione Azure Resource Manager.
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
ms.openlocfilehash: d802ba16ecb4e32e2adb7be3a8e99c72a1625841
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-to-create-new-vms-in-azure"></a><span data-ttu-id="b0b8a-103">Caricare un disco rigido virtuale generalizzato e usarlo per creare nuove macchine virtuali in Azure</span><span class="sxs-lookup"><span data-stu-id="b0b8a-103">Upload a generalized VHD and use it to create new VMs in Azure</span></span>

<span data-ttu-id="b0b8a-104">Questo argomento illustra come usare PowerShell per caricare un disco rigido virtuale di una macchina virtuale generalizzata in Azure, creare un'immagine dal disco rigido virtuale e quindi una nuova macchina virtuale da tale immagine.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-104">This topic walks you through using PowerShell to upload a VHD of a generalized VM to Azure, create an image from the VHD and create a new VM from that image.</span></span> <span data-ttu-id="b0b8a-105">È possibile caricare un disco rigido virtuale esportato da uno strumento di virtualizzazione locale o da un altro cloud.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-105">You can upload a VHD exported from an on-premises virtualization tool or from another cloud.</span></span> <span data-ttu-id="b0b8a-106">Usando [Managed Disks](managed-disks-overview.md) per la nuova macchina virtuale è possibile semplificarne la gestione e ottenere una maggiore disponibilità posizionando la macchina virtuale in un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-106">Using [Managed Disks](managed-disks-overview.md) for the new VM simplifies the VM managment and provides better availability when the VM is placed in an availability set.</span></span> 

<span data-ttu-id="b0b8a-107">Se si vuole usare uno script di esempio, vedere [Script di esempio per caricare un disco rigido virtuale in Azure e creare una nuova macchina virtuale](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span><span class="sxs-lookup"><span data-stu-id="b0b8a-107">If you want to use a sample script, see [Sample script to upload a VHD to Azure and create a new VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b0b8a-108">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="b0b8a-108">Before you begin</span></span>

- <span data-ttu-id="b0b8a-109">Prima di caricare dischi rigidi virtuali in Azure, è necessario seguire la procedura in [Preparare un disco rigido virtuale Windows o VHDX prima del caricamento in Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="b0b8a-109">Before uploading any VHD to Azure, you should follow [Prepare a Windows VHD or VHDX to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
- <span data-ttu-id="b0b8a-110">Rivedere l'articolo [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) (Piano per la migrazione a Managed Disks) prima di avviare la migrazione a [Managed Disks](managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b0b8a-110">Review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration to [Managed Disks](managed-disks-overview.md).</span></span>
- <span data-ttu-id="b0b8a-111">Verificare di avere la versione più recente del modulo di PowerShell AzureRM.Compute.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-111">Make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="b0b8a-112">Eseguire il comando seguente per installarlo.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-112">Run the following command to install it.</span></span>

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    <span data-ttu-id="b0b8a-113">Per altre informazioni, vedere [Azure PowerShell Versioning](/powershell/azure/overview) (Controllo delle versioni di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="b0b8a-113">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="b0b8a-114">Generalizzare la macchina virtuale Windows con Sysprep</span><span class="sxs-lookup"><span data-stu-id="b0b8a-114">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="b0b8a-115">Sysprep rimuove anche tutte le informazioni sull'account personale e prepara la VM da usare come immagine.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-115">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="b0b8a-116">Per altre informazioni su Sysprep, vedere [Come usare Sysprep: Introduzione](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0b8a-116">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="b0b8a-117">Assicurarsi che i ruoli server in esecuzione sulla macchina siano supportati da Sysprep.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-117">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="b0b8a-118">Per ulteriori informazioni, vedere [Supporto Sysprep per i ruoli server](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="b0b8a-118">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0b8a-119">Se si esegue Sysprep prima di caricare il disco rigido virtuale in Azure per la prima volta, verificare di aver [preparato la VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) prima di eseguire Sysprep.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-119">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="b0b8a-120">Accedere alla macchina virtuale Windows.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-120">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="b0b8a-121">Aprire la finestra del prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-121">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="b0b8a-122">Impostare la directory su **%windir%\system32\sysprep**, quindi eseguire `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-122">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="b0b8a-123">Nella finestra di dialogo **Utilità preparazione sistema** selezionare **Passare alla Configurazione guidata** e verificare che la casella di controllo **Generalizza** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-123">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="b0b8a-124">In **Opzioni di arresto del sistema** selezionare **Arresta il sistema**.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-124">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="b0b8a-125">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-125">Click **OK**.</span></span>
   
    ![Avvio di Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="b0b8a-127">Al termine, Sysprep arresta la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-127">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="b0b8a-128">Non riavviare la VM.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-128">Do not restart the VM.</span></span>



## <a name="log-in-to-azure"></a><span data-ttu-id="b0b8a-129">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="b0b8a-129">Log in to Azure</span></span>
<span data-ttu-id="b0b8a-130">Se PowerShell versione 1.4 o successiva non è già stato installato, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b0b8a-130">If you don't already have PowerShell version 1.4 or above installed, read [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="b0b8a-131">Aprire Azure PowerShell e accedere al proprio account di Azure.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-131">Open Azure PowerShell and sign in to your Azure account.</span></span> <span data-ttu-id="b0b8a-132">Verrà visualizzata una finestra popup in cui immettere le credenziali dell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-132">A pop-up window opens for you to enter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="b0b8a-133">Ottenere l'ID di sottoscrizione per le sottoscrizioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-133">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="b0b8a-134">Impostare la sottoscrizione corretta utilizzandone l'ID.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-134">Set the correct subscription using the subscription ID.</span></span> <span data-ttu-id="b0b8a-135">Sostituire *<subscriptionID>* con l'ID della sottoscrizione corretta.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-135">Replace *<subscriptionID>* with the ID of the correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-the-storage-account"></a><span data-ttu-id="b0b8a-136">Ottenere l'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="b0b8a-136">Get the storage account</span></span>
<span data-ttu-id="b0b8a-137">Per archiviare l'immagine della VM caricata, è necessario un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-137">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="b0b8a-138">È possibile usare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-138">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="b0b8a-139">Se il disco rigido virtuale verrà usato per creare un disco gestito per una macchina virtuale, la posizione dell'account di archiviazione deve corrispondere al percorso in cui verrà creata la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-139">If you will be using the VHD to create a managed disk for a VM, the storage account location must be same the location where you will be creating the VM.</span></span>

<span data-ttu-id="b0b8a-140">Per mostrare gli account di archiviazione disponibili, digitare:</span><span class="sxs-lookup"><span data-stu-id="b0b8a-140">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="b0b8a-141">Se si vuole usare un account di archiviazione esistente, passare alla sezione [Caricare l'immagine della VM](#upload-the-vm-vhd-to-your-storage-account) .</span><span class="sxs-lookup"><span data-stu-id="b0b8a-141">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="b0b8a-142">Per creare un account di archiviazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b0b8a-142">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="b0b8a-143">È necessario il nome del gruppo di risorse in cui deve essere creato l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-143">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="b0b8a-144">Per trovare tutti i gruppi di risorse inclusi nella sottoscrizione digitare:</span><span class="sxs-lookup"><span data-stu-id="b0b8a-144">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="b0b8a-145">Per creare un gruppo di risorse denominato **myResourceGroup** nell'area **Stati Uniti orientali**, digitare:</span><span class="sxs-lookup"><span data-stu-id="b0b8a-145">To create a resource group named **myResourceGroup** in the **East US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. <span data-ttu-id="b0b8a-146">Creare un account di archiviazione denominato **mystorageaccount** in questo gruppo di risorse con il cmdlet [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount).</span><span class="sxs-lookup"><span data-stu-id="b0b8a-146">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="b0b8a-147">I valori validi -SkuName validi sono:</span><span class="sxs-lookup"><span data-stu-id="b0b8a-147">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="b0b8a-148">**Standard_LRS**: archiviazione con ridondanza locale.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-148">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="b0b8a-149">**Standard_ZRS**: archiviazione con ridondanza della zona.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-149">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="b0b8a-150">**Standard_GRS**: archiviazione con ridondanza geografica.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-150">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="b0b8a-151">**Standard_RAGRS**: archiviazione con ridondanza geografica e accesso in lettura.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-151">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="b0b8a-152">**Premium_LRS**: archiviazione con ridondanza locale Premium.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-152">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="b0b8a-153">Caricare il disco rigido virtuale nell'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="b0b8a-153">Upload the VHD to your storage account</span></span>

<span data-ttu-id="b0b8a-154">Usare il cmdlet [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) per caricare il disco rigido virtuale in un contenitore nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-154">Use the [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet to upload the VHD to a container in your storage account.</span></span> <span data-ttu-id="b0b8a-155">In questo esempio, il file *myVHD.vhd* viene caricato da *"C:\Users\Public\Documents\Virtual hard disks\"* in un account di archiviazione denominato *mystorageaccount* nel gruppo di risorse *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-155">This example uploads the file *myVHD.vhd* from *"C:\Users\Public\Documents\Virtual hard disks\"* to a storage account named *mystorageaccount* in the *myResourceGroup* resource group.</span></span> <span data-ttu-id="b0b8a-156">Il file viene inserito nel contenitore denominato *mycontainer* e il nuovo nome del file sarà *myUploadedVHD.vhd*.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-156">The file will be placed into the container named *mycontainer* and the new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="b0b8a-157">Se l'operazione riesce, si ottiene una risposta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="b0b8a-157">If successful, you get a response that looks similar to this:</span></span>

```powershell
MD5 hash is being calculated for the file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for the operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="b0b8a-158">L'esecuzione del comando potrebbe richiedere del tempo, a seconda della connessione di rete e delle dimensioni del file VHD.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-158">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span></span>

<span data-ttu-id="b0b8a-159">Salvare il percorso dell'**URI di destinazione** da usare in seguito se si desidera creare un disco gestito o una nuova macchina virtuale con il disco rigido virtuale caricato.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-159">Save the **Destination URI** path to use later if you are going to create a managed disk or a new VM using the uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="b0b8a-160">Altre opzioni per il caricamento di un disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="b0b8a-160">Other options for uploading a VHD</span></span>
 
 
<span data-ttu-id="b0b8a-161">È anche possibile caricare un disco rigido virtuale nell'account di archiviazione tramite uno dei seguenti modi:</span><span class="sxs-lookup"><span data-stu-id="b0b8a-161">You can also upload a VHD to your storage account using one of the following:</span></span>

- [<span data-ttu-id="b0b8a-162">AzCopy</span><span class="sxs-lookup"><span data-stu-id="b0b8a-162">AzCopy</span></span>](http://aka.ms/downloadazcopy)
- [<span data-ttu-id="b0b8a-163">API Copy Blob di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b0b8a-163">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [<span data-ttu-id="b0b8a-164">Caricamento di BLOB in Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="b0b8a-164">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
- [<span data-ttu-id="b0b8a-165">Materiale di riferimento dell'API REST del servizio di importazione/esportazione dell'archiviazione</span><span class="sxs-lookup"><span data-stu-id="b0b8a-165">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)
-   <span data-ttu-id="b0b8a-166">È consigliabile usare il servizio di importazione/esportazione se il tempo di caricamento stimato è maggiore di 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-166">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="b0b8a-167">È possibile usare [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) per stimare il tempo in base alla dimensione dei dati e all'unità di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-167">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span> 
    <span data-ttu-id="b0b8a-168">Il servizio Importazione/esportazione può essere usato per eseguire la copia in un account di archiviazione standard.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-168">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="b0b8a-169">Sarà necessario copiare dall'archiviazione standard all’account di archiviazione premium mediante uno strumento come AzCopy.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-169">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>


## <a name="create-a-managed-image-from-the-uploaded-vhd"></a><span data-ttu-id="b0b8a-170">Creare un'immagine gestita dal disco rigido virtuale caricato</span><span class="sxs-lookup"><span data-stu-id="b0b8a-170">Create a managed image from the uploaded VHD</span></span> 

<span data-ttu-id="b0b8a-171">Creare un'immagine gestita tramite il disco rigido virtuale del sistema operativo generalizzato.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-171">Create a managed image using your generalized OS VHD.</span></span> <span data-ttu-id="b0b8a-172">Sostituire i valori con i propri.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-172">Replace the values with your own information.</span></span>


1.  <span data-ttu-id="b0b8a-173">Innanzitutto, impostare i parametri comuni:</span><span class="sxs-lookup"><span data-stu-id="b0b8a-173">First, set the common parameters:</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  <span data-ttu-id="b0b8a-174">Creare un'immagine tramite il disco rigido virtuale del sistema operativo generalizzato.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-174">Create the image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="b0b8a-175">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="b0b8a-175">Create a virtual network</span></span>
<span data-ttu-id="b0b8a-176">Creare la rete virtuale e la subnet della [rete virtuale](../../virtual-network/virtual-networks-overview.md) stessa.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-176">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="b0b8a-177">Creare la subnet.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-177">Create the subnet.</span></span> <span data-ttu-id="b0b8a-178">Questo esempio crea una subnet denominata *mySubnet* con un prefisso di indirizzo di *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-178">This example creates a subnet named *mySubnet* with the address prefix of *10.0.0.0/24*.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="b0b8a-179">Creare la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-179">Create the virtual network.</span></span> <span data-ttu-id="b0b8a-180">Questo esempio crea una rete virtuale denominata *myVnet* con un prefisso di indirizzo di *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-180">This example creates a virtual network named *myVnet* with the address prefix of *10.0.0.0/16*.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="b0b8a-181">Creare un indirizzo IP pubblico e un'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="b0b8a-181">Create a public IP address and network interface</span></span>

<span data-ttu-id="b0b8a-182">Per abilitare la comunicazione con la macchina virtuale nella rete virtuale, sono necessari un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-182">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="b0b8a-183">Creare un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-183">Create a public IP address.</span></span> <span data-ttu-id="b0b8a-184">In questo esempio viene creato un indirizzo IP pubblico denominato *myPip*.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-184">This example creates a public IP address named *myPip*.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="b0b8a-185">Creare la scheda NIC.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-185">Create the NIC.</span></span> <span data-ttu-id="b0b8a-186">In questo esempio viene creata una scheda NIC denominata **myNic**.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-186">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="b0b8a-187">Creare il gruppo di sicurezza di rete e una regola RDP</span><span class="sxs-lookup"><span data-stu-id="b0b8a-187">Create the network security group and an RDP rule</span></span>

<span data-ttu-id="b0b8a-188">Per essere in grado di accedere alla VM tramite RDP, è necessario disporre di una regola di sicurezza della rete (NSG) che consenta l'accesso RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-188">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="b0b8a-189">In questo esempio viene creato un gruppo di sicurezza di rete denominato *myNsg* contenente una regola denominata *myRdpRule* che consente il traffico RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-189">This example creates an NSG named *myNsg* that contains a rule called *myRdpRule* that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="b0b8a-190">Per altre informazioni sui gruppi di sicurezza di rete, vedere [Apertura di porte a una VM tramite PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b0b8a-190">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

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


## <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="b0b8a-191">Creare una variabile per la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="b0b8a-191">Create a variable for the virtual network</span></span>

<span data-ttu-id="b0b8a-192">Creare una variabile per la rete virtuale realizzata.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-192">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-the-credentials-for-the-vm"></a><span data-ttu-id="b0b8a-193">Ottenere le credenziali per la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b0b8a-193">Get the credentials for the VM</span></span>

<span data-ttu-id="b0b8a-194">Il cmdlet seguente apre una finestra in cui verrà immesso un nuovo nome utente e una nuova password da usare come account dell'amministratore locale per accedere in da remoto alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-194">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="add-the-vm-name-and-size-to-the-vm-configuration"></a><span data-ttu-id="b0b8a-195">Aggiungere il nome della macchina virtuale e le dimensioni per la configurazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-195">Add the VM name and size to the VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-the-vm-image-as-source-image-for-the-new-vm"></a><span data-ttu-id="b0b8a-196">Impostare l'immagine della macchina virtuale come immagine di origine per la nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="b0b8a-196">Set the VM image as source image for the new VM</span></span>

<span data-ttu-id="b0b8a-197">Impostare l'immagine di origine usando l'ID dell'immagine di macchina virtuale gestita.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-197">Set the source image using the ID of the managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-the-os-configuration-and-add-the-nic"></a><span data-ttu-id="b0b8a-198">Impostare la configurazione del sistema operativo e aggiungere la scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-198">Set the OS configuration and add the NIC.</span></span>

<span data-ttu-id="b0b8a-199">Immettere il tipo di archiviazione (PremiumLRS o StandardLRS) e le dimensioni del disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-199">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span></span> <span data-ttu-id="b0b8a-200">In questo esempio il tipo di account viene impostato su *PremiumLRS*, le dimensioni del disco su *128 GB* e il caching del disco su *ReadWrite*.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-200">This example sets the account type to *PremiumLRS*, the disk size to *128 GB* and disk caching to *ReadWrite*.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-the-vm"></a><span data-ttu-id="b0b8a-201">Creare la VM</span><span class="sxs-lookup"><span data-stu-id="b0b8a-201">Create the VM</span></span>

<span data-ttu-id="b0b8a-202">Creare la nuova VM usando la configurazione archiviata nella variabile **$vm**.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-202">Create the new VM using the configuration stored in the **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="b0b8a-203">Verificare che la VM sia stata creata</span><span class="sxs-lookup"><span data-stu-id="b0b8a-203">Verify that the VM was created</span></span>
<span data-ttu-id="b0b8a-204">Al termine, la VM appena creata dovrebbe essere visualizzata nel [portale di Azure](https://portal.azure.com) in **Browse** (Sfoglia)  > **Macchine virtuali**. In alternativa, è possibile usare i comandi PowerShell seguenti:</span><span class="sxs-lookup"><span data-stu-id="b0b8a-204">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="b0b8a-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b0b8a-205">Next steps</span></span>

<span data-ttu-id="b0b8a-206">Per accedere alla nuova macchina virtuale, passare alla VM nel [portale](https://portal.azure.com), fare clic su **Connetti**e aprire il file RDP di Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-206">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="b0b8a-207">Usare le credenziali dell'account della macchina virtuale originale per accedere alla nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="b0b8a-207">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="b0b8a-208">Per altre informazioni, vedere [Come connettersi e accedere a una macchina virtuale di Azure che esegue Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b0b8a-208">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

