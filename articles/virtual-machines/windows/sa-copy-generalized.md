---
title: aaaCreate un'immagine non gestita di una macchina virtuale generalizzata in Azure | Documenti Microsoft
description: "Creare un'immagine di unmanged di un generalizzato toocreate toouse macchina virtuale di Windows più copie di una macchina virtuale in Azure."
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
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a><span data-ttu-id="c219a-103">Come immagine di toocreate una macchina virtuale di non gestita da una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="c219a-103">How toocreate an unmanaged VM image from an Azure VM</span></span>

<span data-ttu-id="c219a-104">In questo articolo illustra l'uso degli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c219a-104">This article covers using storage accounts.</span></span> <span data-ttu-id="c219a-105">È consigliabile usare dischi e immagini anziché un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c219a-105">We recommend that you use managed disks and managed images instead of a storage account.</span></span> <span data-ttu-id="c219a-106">Per altre informazioni, vedere [Acquisire un'immagine gestita di una macchina virtuale generalizzata in Azure](capture-image-resource.md).</span><span class="sxs-lookup"><span data-stu-id="c219a-106">For more information, see [Capture a managed image of a generalized VM in Azure](capture-image-resource.md).</span></span>

<span data-ttu-id="c219a-107">In questo articolo illustra come toouse Azure PowerShell toocreate un'immagine di una macchina virtuale generalizzata di Azure utilizzando un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c219a-107">This article shows you how toouse Azure PowerShell toocreate an image of a generalized Azure VM using a storage account.</span></span> <span data-ttu-id="c219a-108">È quindi possibile utilizzare hello immagine toocreate un'altra macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c219a-108">You can then use hello image toocreate another VM.</span></span> <span data-ttu-id="c219a-109">immagine di Hello include disco del sistema operativo hello e i dischi dati hello sono macchina virtuale toohello associata.</span><span class="sxs-lookup"><span data-stu-id="c219a-109">hello image includes hello OS disk and hello data disks that are attached toohello virtual machine.</span></span> <span data-ttu-id="c219a-110">immagine di Hello non include le risorse di rete virtuale hello, pertanto è necessario tooset tali risorse quando si crea hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c219a-110">hello image doesn't include hello virtual network resources, so you need tooset up those resources when you create hello new VM.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c219a-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c219a-111">Prerequisites</span></span>
<span data-ttu-id="c219a-112">È necessario toohave Azure PowerShell versione 1.0 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="c219a-112">You need toohave Azure PowerShell version 1.0.x or newer installed.</span></span> <span data-ttu-id="c219a-113">Se non è ancora installato PowerShell, leggere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per i passaggi di installazione.</span><span class="sxs-lookup"><span data-stu-id="c219a-113">If you haven't already installed PowerShell, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for installation steps.</span></span>

## <a name="generalize-hello-vm"></a><span data-ttu-id="c219a-114">Generalizzare hello VM</span><span class="sxs-lookup"><span data-stu-id="c219a-114">Generalize hello VM</span></span> 
<span data-ttu-id="c219a-115">In questa sezione illustra come toogeneralize la macchina virtuale di Windows per l'utilizzo come immagine.</span><span class="sxs-lookup"><span data-stu-id="c219a-115">This section shows you how toogeneralize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="c219a-116">Generalizzazione di una macchina virtuale rimuove tutte le informazioni sull'account personale, tra le altre cose e prepara hello macchina toobe utilizzato come immagine.</span><span class="sxs-lookup"><span data-stu-id="c219a-116">Generalizing a VM removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="c219a-117">Per ulteriori informazioni su Sysprep, vedere [come tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="c219a-117">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="c219a-118">Assicurarsi che i ruoli del server hello in esecuzione sul computer hello sono supportati da Sysprep.</span><span class="sxs-lookup"><span data-stu-id="c219a-118">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="c219a-119">Per ulteriori informazioni, vedere [Supporto Sysprep per i ruoli server](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="c219a-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c219a-120">Se si sta caricando tooAzure il disco rigido virtuale per hello prima volta, assicurarsi di avere [preparato la macchina virtuale](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) prima di eseguire Sysprep.</span><span class="sxs-lookup"><span data-stu-id="c219a-120">If you are uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

<span data-ttu-id="c219a-121">È anche possibile generalizzare una VM Linux utilizzando `sudo waagent -deprovision+user` e quindi usare PowerShell toocapture hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c219a-121">You can also generalize a Linux VM using `sudo waagent -deprovision+user` and then use PowerShell toocapture hello VM.</span></span> <span data-ttu-id="c219a-122">Per informazioni sull'utilizzo di hello CLI toocapture una macchina virtuale, vedere [come toogeneralize e acquisire una macchina virtuale Linux utilizzando hello Azure CLI ](../linux/capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="c219a-122">For information about using hello CLI toocapture a VM, see [How toogeneralize and capture a Linux virtual machine using hello Azure CLI ](../linux/capture-image.md).</span></span>


1. <span data-ttu-id="c219a-123">Accedi toohello macchina virtuale di Windows.</span><span class="sxs-lookup"><span data-stu-id="c219a-123">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="c219a-124">Aprire una finestra del prompt dei comandi hello come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c219a-124">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="c219a-125">Modificare anche le directory hello**%windir%\system32\sysprep**, quindi eseguire `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="c219a-125">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="c219a-126">In hello **System Preparation Tool** nella finestra di dialogo **immettere sistema Out-of-Box guidata**e assicurarsi che tale hello **Generalize** casella di controllo è selezionata.</span><span class="sxs-lookup"><span data-stu-id="c219a-126">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="c219a-127">In **Opzioni di arresto del sistema** selezionare **Arresta il sistema**.</span><span class="sxs-lookup"><span data-stu-id="c219a-127">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="c219a-128">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="c219a-128">Click **OK**.</span></span>
   
    ![Avvio di Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="c219a-130">Al termine di Sysprep, arresta macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="c219a-130">When Sysprep completes, it shuts down hello virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c219a-131">Non riavviare hello VM finché non si è fatto tooAzure di disco rigido virtuale hello caricamento o la creazione di un'immagine da hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c219a-131">Do not restart hello VM until you are done uploading hello VHD tooAzure or creating an image from hello VM.</span></span> <span data-ttu-id="c219a-132">Se accidentalmente hello VM Ottiene riavviato, eseguire Sysprep toogeneralize nuovamente.</span><span class="sxs-lookup"><span data-stu-id="c219a-132">If hello VM accidentally gets restarted, run Sysprep toogeneralize it again.</span></span>
> 
> 

## <a name="log-in-tooazure-powershell"></a><span data-ttu-id="c219a-133">Accedi tooAzure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c219a-133">Log in tooAzure PowerShell</span></span>
1. <span data-ttu-id="c219a-134">Aprire Azure PowerShell e accedere tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="c219a-134">Open Azure PowerShell and sign in tooyour Azure account.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    <span data-ttu-id="c219a-135">Una finestra popup viene aperto per si tooenter le credenziali dell'account Azure.</span><span class="sxs-lookup"><span data-stu-id="c219a-135">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
2. <span data-ttu-id="c219a-136">Ottenere l'ID sottoscrizione hello per le sottoscrizioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="c219a-136">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="c219a-137">Set hello sottoscrizione corretta utilizzando l'ID di sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="c219a-137">Set hello correct subscription using hello subscription ID.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a><span data-ttu-id="c219a-138">Deallocare hello macchina virtuale e impostare hello stato toogeneralized</span><span class="sxs-lookup"><span data-stu-id="c219a-138">Deallocate hello VM and set hello state toogeneralized</span></span>
1. <span data-ttu-id="c219a-139">Deallocare risorse VM hello.</span><span class="sxs-lookup"><span data-stu-id="c219a-139">Deallocate hello VM resources.</span></span>
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    <span data-ttu-id="c219a-140">Hello *stato* per Ciao VM hello Azure portal cambia da **arrestato** troppo**arrestato (deallocato)**.</span><span class="sxs-lookup"><span data-stu-id="c219a-140">hello *Status* for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>
2. <span data-ttu-id="c219a-141">Impostare lo stato di hello della macchina virtuale hello troppo**generalizzato**.</span><span class="sxs-lookup"><span data-stu-id="c219a-141">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. <span data-ttu-id="c219a-142">Controllare lo stato di hello di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c219a-142">Check hello status of hello VM.</span></span> <span data-ttu-id="c219a-143">Hello **OSState/generalizzate** sezione per hello macchina virtuale deve disporre di hello **DisplayStatus** impostare troppo**macchina virtuale generalizzata**.</span><span class="sxs-lookup"><span data-stu-id="c219a-143">hello **OSState/generalized** section for hello VM should have hello **DisplayStatus** set too**VM generalized**.</span></span>  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a><span data-ttu-id="c219a-144">Creare l'immagine di hello</span><span class="sxs-lookup"><span data-stu-id="c219a-144">Create hello image</span></span>

<span data-ttu-id="c219a-145">Creare un'immagine di macchina virtuale non gestita nel contenitore di archiviazione di destinazione hello tramite questo comando.</span><span class="sxs-lookup"><span data-stu-id="c219a-145">Create an unmanaged virtual machine image in hello destination storage container using this command.</span></span> <span data-ttu-id="c219a-146">Hello immagine è creata in hello stesso account di archiviazione come hello macchina virtuale originale.</span><span class="sxs-lookup"><span data-stu-id="c219a-146">hello image is created in hello same storage account as hello original virtual machine.</span></span> <span data-ttu-id="c219a-147">Hello `-Path` parametro consente di salvare una copia del modello di hello JSON per il computer locale tooyour hello origine macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c219a-147">hello `-Path` parameter saves a copy of hello JSON template for hello source VM tooyour local computer.</span></span> <span data-ttu-id="c219a-148">Hello `-DestinationContainerName` parametro è il nome di hello del contenitore di hello che si desidera toohold le immagini.</span><span class="sxs-lookup"><span data-stu-id="c219a-148">hello `-DestinationContainerName` parameter is hello name of hello container that you want toohold your images.</span></span> <span data-ttu-id="c219a-149">Se il contenitore di hello non esiste, viene creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c219a-149">If hello container doesn't exist, it is created for you.</span></span>
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
<span data-ttu-id="c219a-150">È possibile ottenere hello URL dell'immagine dal modello di file JSON hello.</span><span class="sxs-lookup"><span data-stu-id="c219a-150">You can get hello URL of your image from hello JSON file template.</span></span> <span data-ttu-id="c219a-151">Passare toohello **risorse** > **storageProfile** > **osDisk** > **immagine**  >  **uri** sezione per il percorso completo di hello dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="c219a-151">Go toohello **resources** > **storageProfile** > **osDisk** > **image** > **uri** section for hello complete path of your image.</span></span> <span data-ttu-id="c219a-152">Hello URL dell'immagine di hello è simile: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span><span class="sxs-lookup"><span data-stu-id="c219a-152">hello URL of hello image looks like: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.</span></span>
   
<span data-ttu-id="c219a-153">È inoltre possibile verificare hello URI nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="c219a-153">You can also verify hello URI in hello portal.</span></span> <span data-ttu-id="c219a-154">immagine di Hello è copiato tooa contenitore denominato **sistema** nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c219a-154">hello image is copied tooa container named **system** in your storage account.</span></span> 

## <a name="create-a-vm-from-hello-image"></a><span data-ttu-id="c219a-155">Creare una macchina virtuale dall'immagine hello</span><span class="sxs-lookup"><span data-stu-id="c219a-155">Create a VM from hello image</span></span>

<span data-ttu-id="c219a-156">Ora è possibile creare uno o più macchine virtuali dall'immagine di hello non gestito.</span><span class="sxs-lookup"><span data-stu-id="c219a-156">Now you can create one or more VMs from hello unmanaged image.</span></span>

### <a name="set-hello-uri-of-hello-vhd"></a><span data-ttu-id="c219a-157">Impostare l'URI del disco rigido virtuale hello hello</span><span class="sxs-lookup"><span data-stu-id="c219a-157">Set hello URI of hello VHD</span></span>

<span data-ttu-id="c219a-158">Hello URI per hello toouse di disco rigido virtuale è in formato hello: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**con estensione vhd.</span><span class="sxs-lookup"><span data-stu-id="c219a-158">hello URI for hello VHD toouse is in hello format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="c219a-159">In questo esempio hello disco rigido virtuale denominato **myVHD** viene nell'account di archiviazione hello **mystorageaccount** nel contenitore hello **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="c219a-159">In this example hello VHD named **myVHD** is in hello storage account **mystorageaccount** in hello container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="c219a-160">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="c219a-160">Create a virtual network</span></span>
<span data-ttu-id="c219a-161">Creare reti virtuali hello e la subnet di hello [rete virtuale](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c219a-161">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="c219a-162">Creare subnet hello.</span><span class="sxs-lookup"><span data-stu-id="c219a-162">Create hello subnet.</span></span> <span data-ttu-id="c219a-163">Hello esempio seguente viene creata una subnet denominata **mySubnet** nel gruppo di risorse hello **myResourceGroup** con prefisso di indirizzo hello **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="c219a-163">hello following sample creates a subnet named **mySubnet** in hello resource group **myResourceGroup** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="c219a-164">Creare la rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="c219a-164">Create hello virtual network.</span></span> <span data-ttu-id="c219a-165">Hello seguente esempio viene creata una rete virtuale denominata **myVnet** in hello **Stati Uniti occidentali** posizione con prefisso di indirizzo hello **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="c219a-165">hello following sample creates a virtual network named **myVnet** in hello **West US** location with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="c219a-166">Creare un indirizzo IP pubblico e un'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="c219a-166">Create a public IP address and network interface</span></span>
<span data-ttu-id="c219a-167">comunicazione tooenable con hello di macchina virtuale nella rete virtuale hello, è necessario un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="c219a-167">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="c219a-168">Creare un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="c219a-168">Create a public IP address.</span></span> <span data-ttu-id="c219a-169">In questo esempio viene creato un indirizzo IP pubblico denominato **myPip**.</span><span class="sxs-lookup"><span data-stu-id="c219a-169">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="c219a-170">Creare una scheda di rete hello.</span><span class="sxs-lookup"><span data-stu-id="c219a-170">Create hello NIC.</span></span> <span data-ttu-id="c219a-171">In questo esempio viene creata una scheda NIC denominata **myNic**.</span><span class="sxs-lookup"><span data-stu-id="c219a-171">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="c219a-172">Creare gruppi di sicurezza di rete hello e una regola di RDP</span><span class="sxs-lookup"><span data-stu-id="c219a-172">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="c219a-173">toobe toolog in grado di tooyour macchina virtuale tramite RDP, è necessario toohave una regola di sicurezza che consente l'accesso RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="c219a-173">toobe able toolog in tooyour VM using RDP, you need toohave a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="c219a-174">In questo esempio viene creato un gruppo di sicurezza di rete denominato **myNsg** contenente una regola denominata **myRdpRule** che consente il traffico RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="c219a-174">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="c219a-175">Per ulteriori informazioni su NSGs, vedere [apertura di porte tooa VM in Azure utilizzando PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c219a-175">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="c219a-176">Creare una variabile per la rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="c219a-176">Create a variable for hello virtual network</span></span>
<span data-ttu-id="c219a-177">Creare una variabile per la rete virtuale hello completata.</span><span class="sxs-lookup"><span data-stu-id="c219a-177">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a><span data-ttu-id="c219a-178">Creare VM hello</span><span class="sxs-lookup"><span data-stu-id="c219a-178">Create hello VM</span></span>
<span data-ttu-id="c219a-179">Hello PowerShell seguente completa le configurazioni di macchina virtuale hello e utilizza l'immagine non gestito come origine di hello per una nuova installazione hello.</span><span class="sxs-lookup"><span data-stu-id="c219a-179">hello following PowerShell completes hello virtual machine configurations and uses unmanaged image as hello source for hello new installation.</span></span>

</br>

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

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="c219a-180">Verificare che hello che è stata creata una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c219a-180">Verify that hello VM was created</span></span>
<span data-ttu-id="c219a-181">Al termine, si dovrebbe essere hello macchina virtuale appena creata in hello [portale di Azure](https://portal.azure.com) in **Sfoglia** > **macchine virtuali**, o tramite hello seguenti Comandi di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c219a-181">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="c219a-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c219a-182">Next steps</span></span>
<span data-ttu-id="c219a-183">vedere la nuova macchina virtuale con Azure PowerShell, toomanage [gestire macchine virtuali tramite Gestione risorse di Azure e PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c219a-183">toomanage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


