---
title: "Caricare un disco rigido virtuale generalizzato per creare più macchine virtuali in Azure | Microsoft Docs"
description: Caricare un disco rigido virtuale generalizzato in un account di archiviazione di Azure per creare una macchina virtuale Windows da usare con il modello di distribuzione di Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: e6fc49855b449a7723a7f8a0c1c41516b3a44ee5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="upload-a-generalized-vhd-to-azure-to-create-a-new-vm"></a><span data-ttu-id="3ad23-103">Caricare un disco rigido virtuale generalizzato in Azure e creare una nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3ad23-103">Upload a generalized VHD to Azure to create a new VM</span></span>

<span data-ttu-id="3ad23-104">In questo argomento viene illustrato il caricamento di un disco non gestito in un account di archiviazione e quindi la creazione di una nuova macchina virtuale tramite il disco caricato.</span><span class="sxs-lookup"><span data-stu-id="3ad23-104">This topic covers uploading a generalized unmanaged disk to a storage account and then creating a new VM using the uploaded disk.</span></span> <span data-ttu-id="3ad23-105">Tutte le informazioni sull'account personale sono state rimosse da un'immagine di disco rigido virtuale generalizzato mediante Sysprep.</span><span class="sxs-lookup"><span data-stu-id="3ad23-105">A generalized VHD image has had all of your personal account information removed using Sysprep.</span></span> 

<span data-ttu-id="3ad23-106">Se si vuole creare una VM da un disco rigido virtuale specializzato in un account di archiviazione, vedere [Creare una macchina virtuale da un disco specializzato](sa-create-vm-specialized.md).</span><span class="sxs-lookup"><span data-stu-id="3ad23-106">If you want to create a VM from a specialized VHD in a storage account, see [Create a VM from a specialized VHD](sa-create-vm-specialized.md).</span></span>

<span data-ttu-id="3ad23-107">In questo argomento viene illustrato l'uso degli account di archiviazione, ma si consiglia di passare all'uso di dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="3ad23-107">This topic covers using storage accounts, but we recommend customers move to using Managed Disks instead.</span></span> <span data-ttu-id="3ad23-108">Per una procedura dettagliata completa su come preparare, caricare e creare una nuova macchina virtuale mediante dischi gestiti, vedere [Creare una nuova macchina virtuale da un disco rigido virtuale generalizzato e caricato in Azure usando Managed Disks](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="3ad23-108">For a complete walk-through of how to prepare, upload and create a new VM using managed disks, see [Create a new VM from a generalized VHD uploaded to Azure using Managed Disks](upload-generalized-managed.md).</span></span>



## <a name="prepare-the-vm"></a><span data-ttu-id="3ad23-109">Preparare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3ad23-109">Prepare the VM</span></span>

<span data-ttu-id="3ad23-110">Tutte le informazioni sull'account personale sono state rimosse da un'immagine del disco rigido virtuale generalizzata tramite Sysprep.</span><span class="sxs-lookup"><span data-stu-id="3ad23-110">A generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="3ad23-111">Se si vuole usare il disco rigido virtuale come immagine dalla quale creare nuove macchine virtuali, è necessario:</span><span class="sxs-lookup"><span data-stu-id="3ad23-111">If you intend to use the VHD as an image to create new VMs from, you should:</span></span>
  
  * <span data-ttu-id="3ad23-112">[Preparare un disco rigido virtuale (VHD) di Windows per il caricamento in Azure](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="3ad23-112">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md).</span></span> 
  * <span data-ttu-id="3ad23-113">Generalizzare la macchina virtuale con Sysprep</span><span class="sxs-lookup"><span data-stu-id="3ad23-113">Generalize the virtual machine using Sysprep</span></span>

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a><span data-ttu-id="3ad23-114">Generalizzare una macchina virtuale Windows mediante Sysprep</span><span class="sxs-lookup"><span data-stu-id="3ad23-114">Generalize a Windows virtual machine using Sysprep</span></span>
<span data-ttu-id="3ad23-115">Questa sezione illustra come generalizzare la macchina virtuale di Windows da usare come immagine.</span><span class="sxs-lookup"><span data-stu-id="3ad23-115">This section shows you how to generalize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="3ad23-116">Sysprep rimuove anche tutte le informazioni sull'account personale e prepara la VM da usare come immagine.</span><span class="sxs-lookup"><span data-stu-id="3ad23-116">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="3ad23-117">Per altre informazioni su Sysprep, vedere [Come usare Sysprep: Introduzione](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ad23-117">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="3ad23-118">Assicurarsi che i ruoli server in esecuzione sulla macchina siano supportati da Sysprep.</span><span class="sxs-lookup"><span data-stu-id="3ad23-118">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="3ad23-119">Per ulteriori informazioni, vedere [Supporto Sysprep per i ruoli server](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="3ad23-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3ad23-120">Se si esegue Sysprep prima di caricare il disco rigido virtuale in Azure per la prima volta, verificare di aver [preparato la VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) prima di eseguire Sysprep.</span><span class="sxs-lookup"><span data-stu-id="3ad23-120">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="3ad23-121">Accedere alla macchina virtuale Windows.</span><span class="sxs-lookup"><span data-stu-id="3ad23-121">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="3ad23-122">Aprire la finestra del prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="3ad23-122">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="3ad23-123">Impostare la directory su **%windir%\system32\sysprep**, quindi eseguire `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="3ad23-123">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="3ad23-124">Nella finestra di dialogo **Utilità preparazione sistema** selezionare **Passare alla Configurazione guidata** e verificare che la casella di controllo **Generalizza** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="3ad23-124">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="3ad23-125">In **Opzioni di arresto del sistema** selezionare **Arresta il sistema**.</span><span class="sxs-lookup"><span data-stu-id="3ad23-125">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="3ad23-126">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ad23-126">Click **OK**.</span></span>
   
    ![Avvio di Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="3ad23-128">Al termine, Sysprep arresta la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3ad23-128">When Sysprep completes, it shuts down the virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3ad23-129">Non riavviare la macchina virtuale fino a quando non viene completato il caricamento del disco rigido virtuale in Azure o la creazione dell'immagine dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3ad23-129">Do not restart the VM until you are done uploading the VHD to Azure or creating an image from the VM.</span></span> <span data-ttu-id="3ad23-130">Se la macchina virtuale viene riavviata accidentalmente, eseguire Sysprep per generalizzarla nuovamente.</span><span class="sxs-lookup"><span data-stu-id="3ad23-130">If the VM accidentally gets restarted, run Sysprep to generalize it again.</span></span>
> 
> 


## <a name="upload-the-vhd"></a><span data-ttu-id="3ad23-131">Caricare il disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="3ad23-131">Upload the VHD</span></span>

<span data-ttu-id="3ad23-132">Caricare il disco rigido virtuale in un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad23-132">Upload the VHD to an Azure storage account.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="3ad23-133">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="3ad23-133">Log in to Azure</span></span>
<span data-ttu-id="3ad23-134">Se PowerShell versione 1.4 o successiva non è già stato installato, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3ad23-134">If you don't already have PowerShell version 1.4 or above installed, read [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="3ad23-135">Aprire Azure PowerShell e accedere al proprio account di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad23-135">Open Azure PowerShell and sign in to your Azure account.</span></span> <span data-ttu-id="3ad23-136">Verrà visualizzata una finestra popup in cui immettere le credenziali dell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad23-136">A pop-up window opens for you to enter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="3ad23-137">Ottenere l'ID di sottoscrizione per le sottoscrizioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="3ad23-137">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="3ad23-138">Impostare la sottoscrizione corretta utilizzandone l'ID.</span><span class="sxs-lookup"><span data-stu-id="3ad23-138">Set the correct subscription using the subscription ID.</span></span> <span data-ttu-id="3ad23-139">Sostituire `<subscriptionID>` con l'ID della sottoscrizione corretta.</span><span class="sxs-lookup"><span data-stu-id="3ad23-139">Replace `<subscriptionID>` with the ID of the correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-the-storage-account"></a><span data-ttu-id="3ad23-140">Ottenere l'account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="3ad23-140">Get the storage account</span></span>
<span data-ttu-id="3ad23-141">Per archiviare l'immagine della VM caricata, è necessario un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3ad23-141">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="3ad23-142">È possibile usare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="3ad23-142">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="3ad23-143">Per mostrare gli account di archiviazione disponibili, digitare:</span><span class="sxs-lookup"><span data-stu-id="3ad23-143">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="3ad23-144">Se si vuole usare un account di archiviazione esistente, passare alla sezione [Caricare l'immagine della VM](#upload-the-vm-vhd-to-your-storage-account) .</span><span class="sxs-lookup"><span data-stu-id="3ad23-144">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="3ad23-145">Per creare un account di archiviazione, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="3ad23-145">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="3ad23-146">È necessario il nome del gruppo di risorse in cui deve essere creato l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3ad23-146">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="3ad23-147">Per trovare tutti i gruppi di risorse inclusi nella sottoscrizione digitare:</span><span class="sxs-lookup"><span data-stu-id="3ad23-147">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="3ad23-148">Per creare un gruppo di risorse denominato **MyResourceGroup** nell'area **Stati Uniti occidentali**, digitare:</span><span class="sxs-lookup"><span data-stu-id="3ad23-148">To create a resource group named **myResourceGroup** in the **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="3ad23-149">Creare un account di archiviazione denominato **mystorageaccount** in questo gruppo di risorse con il cmdlet [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount).</span><span class="sxs-lookup"><span data-stu-id="3ad23-149">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-the-upload"></a><span data-ttu-id="3ad23-150">Avviare il caricamento</span><span class="sxs-lookup"><span data-stu-id="3ad23-150">Start the upload</span></span> 

<span data-ttu-id="3ad23-151">Usare il cmdlet [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) per caricare l'immagine in un contenitore nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3ad23-151">Use the [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet to upload the image to a container in your storage account.</span></span> <span data-ttu-id="3ad23-152">In questo esempio, il file **myVHD.vhd** viene caricato da `"C:\Users\Public\Documents\Virtual hard disks\"` a un account di archiviazione denominato **mystorageaccount** nel gruppo di risorse **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="3ad23-152">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span></span> <span data-ttu-id="3ad23-153">Il file viene inserito nel contenitore denominato **mycontainer** e il nuovo nome del file sarà **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="3ad23-153">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="3ad23-154">Se l'operazione riesce, si ottiene una risposta simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="3ad23-154">If successful, you get a response that looks similar to this:</span></span>

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

<span data-ttu-id="3ad23-155">L'esecuzione del comando potrebbe richiedere del tempo, a seconda della connessione di rete e delle dimensioni del file VHD.</span><span class="sxs-lookup"><span data-stu-id="3ad23-155">Depending on your network connection and the size of your VHD file, this command may take a while to complete.</span></span>


## <a name="create-a-new-vm"></a><span data-ttu-id="3ad23-156">Creare una nuova VM</span><span class="sxs-lookup"><span data-stu-id="3ad23-156">Create a new VM</span></span> 

<span data-ttu-id="3ad23-157">È ora possibile usare il disco rigido virtuale caricato per creare una nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3ad23-157">You can now use the uploaded VHD to create a new VM.</span></span> 

### <a name="set-the-uri-of-the-vhd"></a><span data-ttu-id="3ad23-158">Impostare l'URI del disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="3ad23-158">Set the URI of the VHD</span></span>

<span data-ttu-id="3ad23-159">L'URI del disco rigido virtuale da usare è nel formato seguente: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span><span class="sxs-lookup"><span data-stu-id="3ad23-159">The URI for the VHD to use is in the format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="3ad23-160">In questo esempio il disco rigido virtuale denominato **myVHD** si trova nell'account di archiviazione **mystorageaccount** del contenitore **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="3ad23-160">In this example the VHD named **myVHD** is in the storage account **mystorageaccount** in the container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="3ad23-161">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="3ad23-161">Create a virtual network</span></span>
<span data-ttu-id="3ad23-162">Creare la rete virtuale e la subnet della [rete virtuale](../../virtual-network/virtual-networks-overview.md) stessa.</span><span class="sxs-lookup"><span data-stu-id="3ad23-162">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="3ad23-163">Creare la subnet.</span><span class="sxs-lookup"><span data-stu-id="3ad23-163">Create the subnet.</span></span> <span data-ttu-id="3ad23-164">Nell'esempio seguente viene creata una subnet denominata **mySubnet** nel gruppo di risorse **myResourceGroup** con il prefisso di indirizzo **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="3ad23-164">The following sample creates a subnet named **mySubnet** in the resource group **myResourceGroup** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="3ad23-165">Creare la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3ad23-165">Create the virtual network.</span></span> <span data-ttu-id="3ad23-166">Nell'esempio seguente viene creata una rete virtuale denominata **myVnet** nell'ubicazione **West US** con il prefisso di indirizzo **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="3ad23-166">The following sample creates a virtual network named **myVnet** in the **West US** location with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="3ad23-167">Creare un indirizzo IP pubblico e un'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="3ad23-167">Create a public IP address and network interface</span></span>
<span data-ttu-id="3ad23-168">Per abilitare la comunicazione con la macchina virtuale nella rete virtuale, sono necessari un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="3ad23-168">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="3ad23-169">Creare un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="3ad23-169">Create a public IP address.</span></span> <span data-ttu-id="3ad23-170">In questo esempio viene creato un indirizzo IP pubblico denominato **myPip**.</span><span class="sxs-lookup"><span data-stu-id="3ad23-170">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="3ad23-171">Creare la scheda NIC.</span><span class="sxs-lookup"><span data-stu-id="3ad23-171">Create the NIC.</span></span> <span data-ttu-id="3ad23-172">In questo esempio viene creata una scheda NIC denominata **myNic**.</span><span class="sxs-lookup"><span data-stu-id="3ad23-172">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="3ad23-173">Creare il gruppo di sicurezza di rete e una regola RDP</span><span class="sxs-lookup"><span data-stu-id="3ad23-173">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="3ad23-174">Per essere in grado di accedere alla VM tramite RDP, è necessario disporre di una regola di sicurezza che consenta l'accesso RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="3ad23-174">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="3ad23-175">In questo esempio viene creato un gruppo di sicurezza di rete denominato **myNsg** contenente una regola denominata **myRdpRule** che consente il traffico RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="3ad23-175">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="3ad23-176">Per altre informazioni sui gruppi di sicurezza di rete, vedere [Apertura di porte a una VM tramite PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3ad23-176">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="3ad23-177">Creare una variabile per la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="3ad23-177">Create a variable for the virtual network</span></span>
<span data-ttu-id="3ad23-178">Creare una variabile per la rete virtuale realizzata.</span><span class="sxs-lookup"><span data-stu-id="3ad23-178">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-the-vm"></a><span data-ttu-id="3ad23-179">Creare la VM</span><span class="sxs-lookup"><span data-stu-id="3ad23-179">Create the VM</span></span>
<span data-ttu-id="3ad23-180">Lo script di PowerShell seguente illustra come impostare le configurazioni della macchina virtuale e usare l'immagine della VM caricata come origine per la nuova installazione.</span><span class="sxs-lookup"><span data-stu-id="3ad23-180">The following PowerShell script shows how to set up the virtual machine configurations and use the uploaded VM image as the source for the new installation.</span></span>



```powershell
# Enter a new user name and password to use as the local administrator account 
    # for remotely accessing the VM.
    $cred = Get-Credential

    # Name of the storage account where the VHD is located. This example sets the 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of the virtual machine. This example sets the VM name as "myVM".
    $vmName = "myVM"

    # Size of the virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See the VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for the VM. This examples sets the computer name as "myComputer".
    $computerName = "myComputer"

    # Name of the disk that holds the OS. This example sets the 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets the SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get the storage account where the uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set the VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set the Windows operating system configuration and add the NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create the OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure the OS disk to be created from the existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create the new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="3ad23-181">Verificare che la VM sia stata creata</span><span class="sxs-lookup"><span data-stu-id="3ad23-181">Verify that the VM was created</span></span>
<span data-ttu-id="3ad23-182">Al termine, la VM appena creata dovrebbe essere visualizzata nel [portale di Azure](https://portal.azure.com) in **Browse** (Sfoglia)  > **Macchine virtuali**. In alternativa, è possibile usare i comandi PowerShell seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ad23-182">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="3ad23-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3ad23-183">Next steps</span></span>
<span data-ttu-id="3ad23-184">Per gestire la nuova macchina virtuale con Azure PowerShell, vedere [Gestire macchine virtuali di Azure con Azure Resource Manager e PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3ad23-184">To manage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


