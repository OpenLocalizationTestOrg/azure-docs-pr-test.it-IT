---
title: "aaaUpload un toocreate VHD generalize più macchine virtuali in Azure | Documenti Microsoft"
description: Caricare un generalizzato VHD tooan Azure storage account toocreate toouse una macchina virtuale di Windows con modello di distribuzione di gestione risorse di hello.
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
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a><span data-ttu-id="91eaa-103">Caricare un toocreate di tooAzure di disco rigido virtuale generalizzato una nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="91eaa-103">Upload a generalized VHD tooAzure toocreate a new VM</span></span>

<span data-ttu-id="91eaa-104">Questo argomento viene illustrato il caricamento di un account di archiviazione tooa generalizzato disco non gestito e quindi creare una nuova macchina virtuale utilizzando il disco caricato hello.</span><span class="sxs-lookup"><span data-stu-id="91eaa-104">This topic covers uploading a generalized unmanaged disk tooa storage account and then creating a new VM using hello uploaded disk.</span></span> <span data-ttu-id="91eaa-105">Tutte le informazioni sull'account personale sono state rimosse da un'immagine di disco rigido virtuale generalizzato mediante Sysprep.</span><span class="sxs-lookup"><span data-stu-id="91eaa-105">A generalized VHD image has had all of your personal account information removed using Sysprep.</span></span> 

<span data-ttu-id="91eaa-106">Se si desidera toocreate una macchina virtuale da un disco rigido virtuale specializzato in un account di archiviazione, vedere [creare una macchina virtuale da un disco rigido virtuale specializzato](sa-create-vm-specialized.md).</span><span class="sxs-lookup"><span data-stu-id="91eaa-106">If you want toocreate a VM from a specialized VHD in a storage account, see [Create a VM from a specialized VHD](sa-create-vm-specialized.md).</span></span>

<span data-ttu-id="91eaa-107">In questo argomento viene illustrato l'utilizzo di account di archiviazione, è consigliabile che i clienti spostano i dischi gestiti toousing invece.</span><span class="sxs-lookup"><span data-stu-id="91eaa-107">This topic covers using storage accounts, but we recommend customers move toousing Managed Disks instead.</span></span> <span data-ttu-id="91eaa-108">Per una procedura completa di come tooprepare, caricare e creare una nuova macchina virtuale tramite dischi gestiti, vedere [crea una nuova macchina virtuale da un tooAzure generalizzato di disco rigido virtuale caricato utilizzando dischi gestiti](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="91eaa-108">For a complete walk-through of how tooprepare, upload and create a new VM using managed disks, see [Create a new VM from a generalized VHD uploaded tooAzure using Managed Disks](upload-generalized-managed.md).</span></span>



## <a name="prepare-hello-vm"></a><span data-ttu-id="91eaa-109">Preparare hello VM</span><span class="sxs-lookup"><span data-stu-id="91eaa-109">Prepare hello VM</span></span>

<span data-ttu-id="91eaa-110">Tutte le informazioni sull'account personale sono state rimosse da un'immagine del disco rigido virtuale generalizzata tramite Sysprep.</span><span class="sxs-lookup"><span data-stu-id="91eaa-110">A generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="91eaa-111">Se si prevede di hello toouse toocreate un'immagine disco rigido virtuale nuove macchine virtuali da, è necessario:</span><span class="sxs-lookup"><span data-stu-id="91eaa-111">If you intend toouse hello VHD as an image toocreate new VMs from, you should:</span></span>
  
  * <span data-ttu-id="91eaa-112">[Preparare un tooAzure tooupload disco rigido virtuale di Windows](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="91eaa-112">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md).</span></span> 
  * <span data-ttu-id="91eaa-113">Generalizzare una macchina virtuale hello tramite Sysprep</span><span class="sxs-lookup"><span data-stu-id="91eaa-113">Generalize hello virtual machine using Sysprep</span></span>

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a><span data-ttu-id="91eaa-114">Generalizzare una macchina virtuale Windows mediante Sysprep</span><span class="sxs-lookup"><span data-stu-id="91eaa-114">Generalize a Windows virtual machine using Sysprep</span></span>
<span data-ttu-id="91eaa-115">In questa sezione illustra come toogeneralize la macchina virtuale di Windows per l'utilizzo come immagine.</span><span class="sxs-lookup"><span data-stu-id="91eaa-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="91eaa-116">Sysprep consente di rimuovere tutte le informazioni sull'account personale, tra le altre cose e lo prepara hello macchina toobe utilizzato come immagine.</span><span class="sxs-lookup"><span data-stu-id="91eaa-116">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="91eaa-117">Per ulteriori informazioni su Sysprep, vedere [come tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="91eaa-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="91eaa-118">Assicurarsi che i ruoli del server hello in esecuzione sul computer hello sono supportati da Sysprep.</span><span class="sxs-lookup"><span data-stu-id="91eaa-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="91eaa-119">Per ulteriori informazioni, vedere [Supporto Sysprep per i ruoli server](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="91eaa-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91eaa-120">Se si esegue Sysprep prima di caricare il disco rigido virtuale tooAzure per hello prima volta, assicurarsi di avere [preparato la macchina virtuale](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) prima di eseguire Sysprep.</span><span class="sxs-lookup"><span data-stu-id="91eaa-120">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="91eaa-121">Accedi toohello macchina virtuale di Windows.</span><span class="sxs-lookup"><span data-stu-id="91eaa-121">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="91eaa-122">Aprire una finestra del prompt dei comandi hello come amministratore.</span><span class="sxs-lookup"><span data-stu-id="91eaa-122">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="91eaa-123">Modificare anche le directory hello**%windir%\system32\sysprep**, quindi eseguire `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="91eaa-123">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="91eaa-124">In hello **System Preparation Tool** nella finestra di dialogo **immettere sistema Out-of-Box guidata**e assicurarsi che tale hello **Generalize** casella di controllo è selezionata.</span><span class="sxs-lookup"><span data-stu-id="91eaa-124">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="91eaa-125">In **Opzioni di arresto del sistema** selezionare **Arresta il sistema**.</span><span class="sxs-lookup"><span data-stu-id="91eaa-125">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="91eaa-126">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="91eaa-126">Click **OK**.</span></span>
   
    ![Avvio di Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="91eaa-128">Al termine di Sysprep, arresta macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="91eaa-128">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="91eaa-129">Non riavviare hello VM finché non si è fatto tooAzure di disco rigido virtuale hello caricamento o la creazione di un'immagine da hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="91eaa-129">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="91eaa-130">Se accidentalmente hello VM Ottiene riavviato, eseguire Sysprep toogeneralize nuovamente.</span><span class="sxs-lookup"><span data-stu-id="91eaa-130">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 


## <a name="upload-hello-vhd"></a><span data-ttu-id="91eaa-131">Caricare hello disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="91eaa-131">Upload hello VHD</span></span>

<span data-ttu-id="91eaa-132">Caricare hello VHD tooan account di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="91eaa-132">Upload hello VHD tooan Azure storage account.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="91eaa-133">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="91eaa-133">Log in tooAzure</span></span>
<span data-ttu-id="91eaa-134">Se si dispone già di PowerShell versione 1.4 o versione successiva installato, leggere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="91eaa-134">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="91eaa-135">Aprire Azure PowerShell e accedere tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="91eaa-135">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="91eaa-136">Una finestra popup viene aperto per si tooenter le credenziali dell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="91eaa-136">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="91eaa-137">Ottenere l'ID sottoscrizione hello per le sottoscrizioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="91eaa-137">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="91eaa-138">Set hello sottoscrizione corretta utilizzando l'ID di sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="91eaa-138">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="91eaa-139">Sostituire `<subscriptionID>` con ID hello hello correggere sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="91eaa-139">Replace `<subscriptionID>` with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a><span data-ttu-id="91eaa-140">Ottenere l'account di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="91eaa-140">Get hello storage account</span></span>
<span data-ttu-id="91eaa-141">È necessario un account di archiviazione nell'immagine di macchina virtuale di Azure toostore hello caricato.</span><span class="sxs-lookup"><span data-stu-id="91eaa-141">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="91eaa-142">È possibile usare un account di archiviazione esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="91eaa-142">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="91eaa-143">account di archiviazione disponibili hello tooshow, digitare:</span><span class="sxs-lookup"><span data-stu-id="91eaa-143">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="91eaa-144">Se si desidera toouse un account di archiviazione esistente, procedere toohello [immagine di macchina virtuale di caricamento hello](#upload-the-vm-vhd-to-your-storage-account) sezione.</span><span class="sxs-lookup"><span data-stu-id="91eaa-144">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="91eaa-145">Se è necessario un account di archiviazione toocreate, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="91eaa-145">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="91eaa-146">È necessario il nome di hello hello del gruppo di risorse in cui deve essere creato l'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="91eaa-146">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="91eaa-147">toofind out tutti i gruppi di risorse hello nella sottoscrizione di tipo sono:</span><span class="sxs-lookup"><span data-stu-id="91eaa-147">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="91eaa-148">un gruppo di risorse denominato toocreate **myResourceGroup** in hello **Stati Uniti occidentali** area, digitare:</span><span class="sxs-lookup"><span data-stu-id="91eaa-148">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="91eaa-149">Creare un account di archiviazione denominato **mystorageaccount** in questo gruppo di risorse utilizzando hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="91eaa-149">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a><span data-ttu-id="91eaa-150">Avviare il caricamento di hello</span><span class="sxs-lookup"><span data-stu-id="91eaa-150">Start hello upload</span></span> 

<span data-ttu-id="91eaa-151">Hello utilizzare [Aggiungi AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello tooa il contenitore di immagini nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="91eaa-151">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="91eaa-152">In questo esempio caricamenti hello file **myVHD.vhd** da `"C:\Users\Public\Documents\Virtual hard disks\"` tooa account di archiviazione denominato **mystorageaccount** in hello **myResourceGroup** gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="91eaa-152">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="91eaa-153">sarà inseriti file Hello contenitore hello denominato **mycontainer** e sarà il nuovo nome di file hello **myUploadedVHD.vhd**.</span><span class="sxs-lookup"><span data-stu-id="91eaa-153">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="91eaa-154">Se ha esito positivo, si otterrà una risposta simile toothis simile:</span><span class="sxs-lookup"><span data-stu-id="91eaa-154">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="91eaa-155">La connessione di rete e delle dimensioni di hello del file di disco rigido virtuale, questo comando potrebbe richiedere qualche minuto toocomplete.</span><span class="sxs-lookup"><span data-stu-id="91eaa-155">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="create-a-new-vm"></a><span data-ttu-id="91eaa-156">Creare una nuova VM</span><span class="sxs-lookup"><span data-stu-id="91eaa-156">Create a new VM</span></span> 

<span data-ttu-id="91eaa-157">È possibile utilizzare hello caricato VHD toocreate una nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="91eaa-157">You can now use hello uploaded VHD toocreate a new VM.</span></span> 

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="91eaa-158">Impostare l'URI del disco rigido virtuale hello hello</span><span class="sxs-lookup"><span data-stu-id="91eaa-158">Set hello URI of hello VHD</span></span>

<span data-ttu-id="91eaa-159">Hello URI per hello toouse di disco rigido virtuale è in formato hello: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**con estensione vhd.</span><span class="sxs-lookup"><span data-stu-id="91eaa-159">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="91eaa-160">In questo esempio hello disco rigido virtuale denominato **myVHD** viene nell'account di archiviazione hello **mystorageaccount** nel contenitore hello **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="91eaa-160">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="91eaa-161">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="91eaa-161">Create a virtual network</span></span>
<span data-ttu-id="91eaa-162">Creare reti virtuali hello e la subnet di hello [rete virtuale](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="91eaa-162">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="91eaa-163">Creare subnet hello.</span><span class="sxs-lookup"><span data-stu-id="91eaa-163">Create hello subnet.</span></span> <span data-ttu-id="91eaa-164">Hello esempio seguente viene creata una subnet denominata **mySubnet** nel gruppo di risorse hello **myResourceGroup** con prefisso di indirizzo hello **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="91eaa-164">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="91eaa-165">Creare la rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="91eaa-165">Create hello virtual network.</span></span> <span data-ttu-id="91eaa-166">Hello seguente esempio viene creata una rete virtuale denominata **myVnet** in hello **Stati Uniti occidentali** posizione con prefisso di indirizzo hello **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="91eaa-166">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="91eaa-167">Creare un indirizzo IP pubblico e un'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="91eaa-167">Create a public IP address and network interface</span></span>
<span data-ttu-id="91eaa-168">comunicazione tooenable con hello di macchina virtuale nella rete virtuale hello, è necessario un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="91eaa-168">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="91eaa-169">Creare un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="91eaa-169">Create a public IP address.</span></span> <span data-ttu-id="91eaa-170">In questo esempio viene creato un indirizzo IP pubblico denominato **myPip**.</span><span class="sxs-lookup"><span data-stu-id="91eaa-170">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="91eaa-171">Creare una scheda di rete hello.</span><span class="sxs-lookup"><span data-stu-id="91eaa-171">Create hello NIC.</span></span> <span data-ttu-id="91eaa-172">In questo esempio viene creata una scheda NIC denominata **myNic**.</span><span class="sxs-lookup"><span data-stu-id="91eaa-172">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="91eaa-173">Creare gruppi di sicurezza di rete hello e una regola di RDP</span><span class="sxs-lookup"><span data-stu-id="91eaa-173">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="91eaa-174">toobe toolog in grado di tooyour macchina virtuale tramite RDP, è necessario toohave una regola di sicurezza che consente l'accesso RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="91eaa-174">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="91eaa-175">In questo esempio viene creato un gruppo di sicurezza di rete denominato **myNsg** contenente una regola denominata **myRdpRule** che consente il traffico RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="91eaa-175">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="91eaa-176">Per ulteriori informazioni su NSGs, vedere [apertura di porte tooa VM in Azure utilizzando PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="91eaa-176">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="91eaa-177">Creare una variabile per la rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="91eaa-177">Create a variable for hello virtual network</span></span>
<span data-ttu-id="91eaa-178">Creare una variabile per la rete virtuale hello completata.</span><span class="sxs-lookup"><span data-stu-id="91eaa-178">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="91eaa-179">Creare VM hello</span><span class="sxs-lookup"><span data-stu-id="91eaa-179">Create hello VM</span></span>
<span data-ttu-id="91eaa-180">Hello script PowerShell riportato di seguito viene illustrato come tooset di configurazioni di macchina virtuale hello e utilizzare hello caricato l'immagine di macchina virtuale come origine di hello per una nuova installazione hello.</span><span class="sxs-lookup"><span data-stu-id="91eaa-180">hello following PowerShell script shows how tooset up hello virtual machine configurations and use hello uploaded VM image as hello source for hello new installation.</span></span>



```powershell
# Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="91eaa-181">Verificare che hello che è stata creata una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="91eaa-181">Verify that hello VM was created</span></span>
<span data-ttu-id="91eaa-182">Al termine, si dovrebbe essere hello macchina virtuale appena creata in hello [portale di Azure](https://portal.azure.com) in **Sfoglia** > **macchine virtuali**, o tramite hello seguenti Comandi di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="91eaa-182">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="91eaa-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="91eaa-183">Next steps</span></span>
<span data-ttu-id="91eaa-184">vedere la nuova macchina virtuale con Azure PowerShell, toomanage [gestire macchine virtuali tramite Gestione risorse di Azure e PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="91eaa-184">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


