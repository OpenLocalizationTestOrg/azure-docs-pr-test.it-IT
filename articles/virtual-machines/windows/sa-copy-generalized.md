---
title: Creare un'immagine non gestita di una macchina virtuale generalizzata in Azure | Microsoft Docs
description: "Creare un'immagine non gestita di una macchina virtuale Windows generalizzata da usare per creare più copie di una macchina virtuale in Azure."
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: d7f4a9558175835eba9096e6845726f21c7459d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-create-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="2646e-103">Come creare un'immagine di macchina virtuale non gestita da una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="2646e-103">How to create an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="2646e-104">In questo articolo illustra l'uso degli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2646e-104">This article covers using storage accounts.</span></span> <span data-ttu-id="2646e-105">È consigliabile usare dischi e immagini anziché un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2646e-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="2646e-106">Per altre informazioni, vedere [Acquisire un'immagine gestita di una macchina virtuale generalizzata in Azure](capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="2646e-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="2646e-107">Questo articolo illustra come usare Azure PowerShell per creare un'immagine di una macchina virtuale generalizzata di Azure con un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2646e-107">This article shows you how to use Azure PowerShell to create an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="2646e-108">È quindi possibile usare l'immagine per creare un'altra VM.</span><span class="sxs-lookup"><span data-stu-id="2646e-108">You can then use the image to create another VM.</span></span> <span data-ttu-id="2646e-109">Questa immagine include il disco del sistema operativo e i dischi dati collegati alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2646e-109">The image includes the OS disk and the data disks that are attached to the virtual machine.</span></span> <span data-ttu-id="2646e-110">L'immagine non include le risorse della rete virtuale, quindi è necessario configurare queste risorse quando si crea la nuova VM.</span><span class="sxs-lookup"><span data-stu-id="2646e-110">The image doesn't include the virtual network resources, so you need to set up those resources when you create the new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2646e-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2646e-111">Prerequisites</span></span>
<span data-ttu-id="2646e-112">È necessario che sia installato Azure PowerShell 1.0.x o una versione più recente.</span><span class="sxs-lookup"><span data-stu-id="2646e-112">You need to have Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="2646e-113">Se non è già stato installato PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview) per la procedura di installazione.</span><span class="sxs-lookup"><span data-stu-id="2646e-113">If you haven't already installed PowerShell, read [How to install and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-the-vm"></a><span data-ttu-id="2646e-114">Generalizzare la VM</span><span class="sxs-lookup"><span data-stu-id="2646e-114">Generalize the VM</span></span> 
<span data-ttu-id="2646e-115">Questa sezione illustra come generalizzare la macchina virtuale di Windows da usare come immagine.</span><span class="sxs-lookup"><span data-stu-id="2646e-115">This section shows you how to generalize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="2646e-116">Generalizzando una VM si rimuovono anche tutte le informazioni personali sull'account e si prepara la macchina da usare come immagine.</span><span class="sxs-lookup"><span data-stu-id="2646e-116">Generalizing a VM removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="2646e-117">Per altre informazioni su Sysprep, vedere [Come usare Sysprep: Introduzione](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="2646e-117">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="2646e-118">Assicurarsi che i ruoli server in esecuzione sulla macchina siano supportati da Sysprep.</span><span class="sxs-lookup"><span data-stu-id="2646e-118">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="2646e-119">Per ulteriori informazioni, vedere [Supporto Sysprep per i ruoli server](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="2646e-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2646e-120">Se si carica il disco rigido virtuale in Azure per la prima volta, verificare di aver [preparato la macchina virtuale](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) prima di eseguire Sysprep.</span><span class="sxs-lookup"><span data-stu-id="2646e-120">If you are uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="2646e-121">È possibile anche generalizzare una VM Linux tramite `sudo waagent -deprovision+user` e quindi usare PowerShell per acquisire la VM.</span><span class="sxs-lookup"><span data-stu-id="2646e-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell to capture the VM.</span></span> <span data-ttu-id="2646e-122">Per informazioni sull'uso dell'interfaccia della riga di comando per acquisire una macchina virtuale, vedere [Come generalizzare e acquisire una macchina virtuale Linux con l'interfaccia della riga di comando di Azure](../linux/capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="2646e-122">For information about using the CLI to capture a VM, see [How to generalize and capture a Linux virtual machine using the Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="2646e-123">Accedere alla macchina virtuale Windows.</span><span class="sxs-lookup"><span data-stu-id="2646e-123">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="2646e-124">Aprire la finestra del prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="2646e-124">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="2646e-125">Impostare la directory su **%windir%\system32\sysprep**, quindi eseguire `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="2646e-125">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="2646e-126">Nella finestra di dialogo **Utilità preparazione sistema** selezionare **Passare alla Configurazione guidata** e verificare che la casella di controllo **Generalizza** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="2646e-126">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="2646e-127">In **Opzioni di arresto del sistema** selezionare **Arresta il sistema**.</span><span class="sxs-lookup"><span data-stu-id="2646e-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="2646e-128">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2646e-128">Click **OK**.</span></span>
   
    ![Avvio di Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="2646e-130">Al termine, Sysprep arresta la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2646e-130">When Sysprep completes, it shuts down the virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2646e-131">Non riavviare la macchina virtuale fino a quando non viene completato il caricamento del disco rigido virtuale in Azure o la creazione dell'immagine dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2646e-131">Do not restart the VM until you are done uploading the VHD to Azure or creating an image from the VM.</span></span> <span data-ttu-id="2646e-132">Se la macchina virtuale viene riavviata accidentalmente, eseguire Sysprep per generalizzarla nuovamente.</span><span class="sxs-lookup"><span data-stu-id="2646e-132">If the VM accidentally gets restarted, run Sysprep to generalize it again.</span></span>
> 
> 

## <a name="log-in-to-azure-powershell"></a><span data-ttu-id="2646e-133">Accedere ad Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2646e-133">Log in to Azure PowerShell</span></span>
1. <span data-ttu-id="2646e-134">Aprire Azure PowerShell e accedere al proprio account di Azure.</span><span class="sxs-lookup"><span data-stu-id="2646e-134">Open Azure PowerShell and sign in to your Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="2646e-135">Verrà visualizzata una finestra popup in cui immettere le credenziali dell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="2646e-135">A pop-up window opens for you to enter your Azure account credentials.</span></span>
2. <span data-ttu-id="2646e-136">Ottenere l'ID di sottoscrizione per le sottoscrizioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="2646e-136">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="2646e-137">Impostare la sottoscrizione corretta utilizzandone l'ID.</span><span class="sxs-lookup"><span data-stu-id="2646e-137">Set the correct subscription using the subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-the-vm-and-set-the-state-to-generalized"></a><span data-ttu-id="2646e-138">Deallocare la VM e impostare lo stato generalizzato</span><span class="sxs-lookup"><span data-stu-id="2646e-138">Deallocate the VM and set the state to generalized</span></span>
1. <span data-ttu-id="2646e-139">Deallocare le risorse della VM.</span><span class="sxs-lookup"><span data-stu-id="2646e-139">Deallocate the VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="2646e-140">Nel portale di Azure lo *stato* della VM passa da **Arrestato** ad **Arrestato (deallocato)**.</span><span class="sxs-lookup"><span data-stu-id="2646e-140">The *Status* for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="2646e-141">Impostare lo stato della macchina virtuale su **Generalizzato**.</span><span class="sxs-lookup"><span data-stu-id="2646e-141">Set the status of the virtual machine to **Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="2646e-142">Controllare lo stato della VM.</span><span class="sxs-lookup"><span data-stu-id="2646e-142">Check the status of the VM.</span></span> <span data-ttu-id="2646e-143">Nella sezione **OSState/generalized** per la VM, il valore **DisplayStatus** dovrebbe essere impostato su **Macchina virtuale generalizzata**.</span><span class="sxs-lookup"><span data-stu-id="2646e-143">The **OSState/generalized** section for the VM should have the **DisplayStatus** set to **VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-the-image"></a><span data-ttu-id="2646e-144">Creare l'immagine</span><span class="sxs-lookup"><span data-stu-id="2646e-144">Create the image</span></span>

<span data-ttu-id="2646e-145">Creare l'immagine della macchina virtuale non gestita nel contenitore di archiviazione di destinazione usando questo comando.</span><span class="sxs-lookup"><span data-stu-id="2646e-145">Create an unmanaged virtual machine image in the destination storage container using this command.</span></span> <span data-ttu-id="2646e-146">L'immagine viene creata nello stesso account di archiviazione della macchina virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="2646e-146">The image is created in the same storage account as the original virtual machine.</span></span> <span data-ttu-id="2646e-147">Il parametro `-Path` salva una copia del modello JSON per la macchina virtuale di origine nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="2646e-147">The `-Path` parameter saves a copy of the JSON template for the source VM to your local computer.</span></span> <span data-ttu-id="2646e-148">Il parametro `-DestinationContainerName` è il nome del contenitore in cui si vuole salvare le immagini.</span><span class="sxs-lookup"><span data-stu-id="2646e-148">The `-DestinationContainerName` parameter is the name of the container that you want to hold your images.</span></span> <span data-ttu-id="2646e-149">Se il contenitore non esiste, verrà creato.</span><span class="sxs-lookup"><span data-stu-id="2646e-149">If the container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="2646e-150">È possibile ottenere l'URL dell'immagine dal modello del file JSON.</span><span class="sxs-lookup"><span data-stu-id="2646e-150">You can get the URL of your image from the JSON file template.</span></span> <span data-ttu-id="2646e-151">Passare alla sezione **resources** > **storageProfile** > **osDisk** > **image** > **uri** per il percorso completo dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="2646e-151">Go to the **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for the complete path of your image.</span></span> <span data-ttu-id="2646e-152">L'URL dell'immagine è simile a questo: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="2646e-152">The URL of the image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="2646e-153">È anche possibile verificare l'URI nel portale.</span><span class="sxs-lookup"><span data-stu-id="2646e-153">You can also verify the URI in the portal.</span></span> <span data-ttu-id="2646e-154">L'immagine viene copiata in un contenitore denominato **system** nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2646e-154">The image is copied to a container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-the-image"></a><span data-ttu-id="2646e-155">Creare una macchina virtuale dall'immagine</span><span class="sxs-lookup"><span data-stu-id="2646e-155">Create a VM from the image</span></span>

<span data-ttu-id="2646e-156">A questo punto è possibile creare una o più macchine virtuali dall'immagine non gestita.</span><span class="sxs-lookup"><span data-stu-id="2646e-156">Now you can create one or more VMs from the unmanaged image.</span></span>

### <a name="set-the-uri-of-the-vhd"></a><span data-ttu-id="2646e-157">Impostare l'URI del disco rigido virtuale</span><span class="sxs-lookup"><span data-stu-id="2646e-157">Set the URI of the VHD</span></span>

<span data-ttu-id="2646e-158">L'URI del disco rigido virtuale da usare è nel formato seguente: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span><span class="sxs-lookup"><span data-stu-id="2646e-158">The URI for the VHD to use is in the format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="2646e-159">In questo esempio il disco rigido virtuale denominato **myVHD** si trova nell'account di archiviazione **mystorageaccount** del contenitore **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="2646e-159">In this example the VHD named **myVHD** is in the storage account **mystorageaccount** in the container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="2646e-160">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="2646e-160">Create a virtual network</span></span>
<span data-ttu-id="2646e-161">Creare la rete virtuale e la subnet della [rete virtuale](../../virtual-network/virtual-networks-overview.md) stessa.</span><span class="sxs-lookup"><span data-stu-id="2646e-161">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="2646e-162">Creare la subnet.</span><span class="sxs-lookup"><span data-stu-id="2646e-162">Create the subnet.</span></span> <span data-ttu-id="2646e-163">Nell'esempio seguente viene creata una subnet denominata **mySubnet** nel gruppo di risorse **myResourceGroup** con il prefisso di indirizzo **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="2646e-163">The following sample creates a subnet named **mySubnet** in the resource group **myResourceGroup** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="2646e-164">Creare la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="2646e-164">Create the virtual network.</span></span> <span data-ttu-id="2646e-165">Nell'esempio seguente viene creata una rete virtuale denominata **myVnet** nell'ubicazione **West US** con il prefisso di indirizzo **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="2646e-165">The following sample creates a virtual network named **myVnet** in the **West US** location with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="2646e-166">Creare un indirizzo IP pubblico e un'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="2646e-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="2646e-167">Per abilitare la comunicazione con la macchina virtuale nella rete virtuale, sono necessari un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="2646e-167">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="2646e-168">Creare un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="2646e-168">Create a public IP address.</span></span> <span data-ttu-id="2646e-169">In questo esempio viene creato un indirizzo IP pubblico denominato **myPip**.</span><span class="sxs-lookup"><span data-stu-id="2646e-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="2646e-170">Creare la scheda NIC.</span><span class="sxs-lookup"><span data-stu-id="2646e-170">Create the NIC.</span></span> <span data-ttu-id="2646e-171">In questo esempio viene creata una scheda NIC denominata **myNic**.</span><span class="sxs-lookup"><span data-stu-id="2646e-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="2646e-172">Creare il gruppo di sicurezza di rete e una regola RDP</span><span class="sxs-lookup"><span data-stu-id="2646e-172">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="2646e-173">Per essere in grado di accedere alla VM tramite RDP, è necessario disporre di una regola di sicurezza che consenta l'accesso RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="2646e-173">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="2646e-174">In questo esempio viene creato un gruppo di sicurezza di rete denominato **myNsg** contenente una regola denominata **myRdpRule** che consente il traffico RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="2646e-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="2646e-175">Per altre informazioni sui gruppi di sicurezza di rete, vedere [Apertura di porte a una VM tramite PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2646e-175">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="2646e-176">Creare una variabile per la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="2646e-176">Create a variable for the virtual network</span></span>
<span data-ttu-id="2646e-177">Creare una variabile per la rete virtuale realizzata.</span><span class="sxs-lookup"><span data-stu-id="2646e-177">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-the-vm"></a><span data-ttu-id="2646e-178">Creare la VM</span><span class="sxs-lookup"><span data-stu-id="2646e-178">Create the VM</span></span>
<span data-ttu-id="2646e-179">PowerShell riportato di seguito completa le configurazioni della macchina virtuale e usa l'immagine della non gestita come origine per la nuova installazione.</span><span class="sxs-lookup"><span data-stu-id="2646e-179">The following PowerShell completes the virtual machine configurations and uses unmanaged image as the source for the new installation.</span></span>

</br>

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

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="2646e-180">Verificare che la VM sia stata creata</span><span class="sxs-lookup"><span data-stu-id="2646e-180">Verify that the VM was created</span></span>
<span data-ttu-id="2646e-181">Al termine, la VM appena creata dovrebbe essere visualizzata nel [portale di Azure](https://portal.azure.com) in **Browse** (Sfoglia)  > **Macchine virtuali**. In alternativa, è possibile usare i comandi PowerShell seguenti:</span><span class="sxs-lookup"><span data-stu-id="2646e-181">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="2646e-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2646e-182">Next steps</span></span>
<span data-ttu-id="2646e-183">Per gestire la nuova macchina virtuale con Azure PowerShell, vedere [Gestire macchine virtuali di Azure con Azure Resource Manager e PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2646e-183">To manage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


