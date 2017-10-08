---
title: aaaCreate macchina virtuale da un'immagine di macchina virtuale gestita in Azure | Documenti Microsoft
description: Creare una macchina virtuale Windows da un'immagine di macchina virtuale gestita generalizzata usando Azure PowerShell, nel modello di distribuzione di gestione risorse di hello.
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
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a><span data-ttu-id="3e335-103">Creare una macchina virtuale da un'immagine gestita</span><span class="sxs-lookup"><span data-stu-id="3e335-103">Create a VM from a managed image</span></span>

<span data-ttu-id="3e335-104">È possibile creare più macchine virtuali da un'immagine di macchina virtuale gestita in Azure.</span><span class="sxs-lookup"><span data-stu-id="3e335-104">You can create multiple VMs from a managed VM image in Azure.</span></span> <span data-ttu-id="3e335-105">Un'immagine di macchina virtuale gestita contiene hello informazioni necessarie toocreate una macchina virtuale, inclusi i dischi del sistema operativo e dati hello.</span><span class="sxs-lookup"><span data-stu-id="3e335-105">A managed VM image contains hello information necessary toocreate a VM, including hello OS and data disks.</span></span> <span data-ttu-id="3e335-106">Hello dischi rigidi virtuali che costituiscono l'immagine di hello, inclusi i dischi di hello del sistema operativo sia eventuali dischi dati, vengono archiviati come dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="3e335-106">hello VHDs that make up hello image, including both hello OS disks and any data disks, are stored as managed disks.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="3e335-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3e335-107">Prerequisites</span></span>

<span data-ttu-id="3e335-108">È necessario già toohave [creata un'immagine di macchina virtuale gestita](capture-image-resource.md) toouse per la creazione di hello nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3e335-108">You need toohave already [created a managed VM image](capture-image-resource.md) toouse for creating hello new VM.</span></span> 

<span data-ttu-id="3e335-109">Assicurarsi di disporre di hello versioni più recenti dei moduli di AzureRM.Compute e AzureRM.Network PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="3e335-109">Make sure that you have hello latest versions of hello AzureRM.Compute and AzureRM.Network PowerShell modules.</span></span> <span data-ttu-id="3e335-110">Aprire un prompt dei comandi di PowerShell come amministratore ed eseguire hello successivo comando tooinstall li.</span><span class="sxs-lookup"><span data-stu-id="3e335-110">Open a PowerShell prompt as an Administrator and run hello following command tooinstall them.</span></span>

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
<span data-ttu-id="3e335-111">Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3e335-111">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>



## <a name="collect-information-about-hello-image"></a><span data-ttu-id="3e335-112">Raccogliere informazioni sull'immagine di hello</span><span class="sxs-lookup"><span data-stu-id="3e335-112">Collect information about hello image</span></span>

<span data-ttu-id="3e335-113">È innanzitutto necessario toogather le informazioni di base sull'immagine di hello e creare una variabile per l'immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="3e335-113">First we need toogather basic information about hello image and create a variable for hello image.</span></span> <span data-ttu-id="3e335-114">In questo esempio Usa un'immagine di macchina virtuale gestita denominata **myImage** ovvero hello in **myResourceGroup** gruppo di risorse in hello **occidentale Stati Uniti centro** percorso.</span><span class="sxs-lookup"><span data-stu-id="3e335-114">This example uses a managed VM image named **myImage** that is in hello **myResourceGroup** resource group in hello **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="3e335-115">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="3e335-115">Create a virtual network</span></span>
<span data-ttu-id="3e335-116">Creare reti virtuali hello e la subnet di hello [rete virtuale](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3e335-116">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="3e335-117">Creare subnet hello.</span><span class="sxs-lookup"><span data-stu-id="3e335-117">Create hello subnet.</span></span> <span data-ttu-id="3e335-118">Questo esempio viene creata una subnet denominata **mySubnet** con prefisso di indirizzo hello **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="3e335-118">This example creates a subnet named **mySubnet** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="3e335-119">Creare la rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="3e335-119">Create hello virtual network.</span></span> <span data-ttu-id="3e335-120">Questo esempio viene creata una rete virtuale denominata **myVnet** con prefisso di indirizzo hello **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="3e335-120">This example creates a virtual network named **myVnet** with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="3e335-121">Creare un indirizzo IP pubblico e un'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="3e335-121">Create a public IP address and network interface</span></span>

<span data-ttu-id="3e335-122">comunicazione tooenable con hello di macchina virtuale nella rete virtuale hello, è necessario un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="3e335-122">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="3e335-123">Creare un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="3e335-123">Create a public IP address.</span></span> <span data-ttu-id="3e335-124">In questo esempio viene creato un indirizzo IP pubblico denominato **myPip**.</span><span class="sxs-lookup"><span data-stu-id="3e335-124">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="3e335-125">Creare una scheda di rete hello.</span><span class="sxs-lookup"><span data-stu-id="3e335-125">Create hello NIC.</span></span> <span data-ttu-id="3e335-126">In questo esempio viene creata una scheda NIC denominata **myNic**.</span><span class="sxs-lookup"><span data-stu-id="3e335-126">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="3e335-127">Creare gruppi di sicurezza di rete hello e una regola di RDP</span><span class="sxs-lookup"><span data-stu-id="3e335-127">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="3e335-128">toobe toolog in grado di tooyour macchina virtuale tramite RDP, è necessario toohave una regola di sicurezza di rete (gruppo) che consente l'accesso RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="3e335-128">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="3e335-129">In questo esempio viene creato un gruppo di sicurezza di rete denominato **myNsg** contenente una regola denominata **myRdpRule** che consente il traffico RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="3e335-129">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="3e335-130">Per ulteriori informazioni su NSGs, vedere [apertura di porte tooa VM in Azure utilizzando PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3e335-130">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

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


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="3e335-131">Creare una variabile per la rete virtuale hello</span><span class="sxs-lookup"><span data-stu-id="3e335-131">Create a variable for hello virtual network</span></span>

<span data-ttu-id="3e335-132">Creare una variabile per la rete virtuale hello completata.</span><span class="sxs-lookup"><span data-stu-id="3e335-132">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="3e335-133">Ottenere le credenziali di hello per hello VM</span><span class="sxs-lookup"><span data-stu-id="3e335-133">Get hello credentials for hello VM</span></span>

<span data-ttu-id="3e335-134">Hello cmdlet riportato di seguito verrà aperta una finestra in cui è necessario specificare un nuovo toouse di nome e una password utente come account amministratore locale hello per accedere in remoto alle macchine Virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="3e335-134">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a><span data-ttu-id="3e335-135">Variabili impostate per hello VM name, nome di computer e hello dimensioni di hello VM</span><span class="sxs-lookup"><span data-stu-id="3e335-135">Set variables for hello VM name, computer name and hello size of hello VM</span></span>

1. <span data-ttu-id="3e335-136">Creare variabili per il nome di macchina virtuale hello e nome del computer.</span><span class="sxs-lookup"><span data-stu-id="3e335-136">Create variables for hello VM name and computer name.</span></span> <span data-ttu-id="3e335-137">In questo esempio imposta come nome della macchina virtuale hello **myVM** e nome del computer hello come **myComputer**.</span><span class="sxs-lookup"><span data-stu-id="3e335-137">This example sets hello VM name as **myVM** and hello computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="3e335-138">Impostare dimensioni hello della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="3e335-138">Set hello size of hello virtual machine.</span></span> <span data-ttu-id="3e335-139">Questo esempio crea una macchina virtuale con dimensione **Standard_DS1_v2**.</span><span class="sxs-lookup"><span data-stu-id="3e335-139">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="3e335-140">Vedere hello [dimensioni delle macchine Virtuali](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentazione per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="3e335-140">See hello [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="3e335-141">Aggiungere hello nome della macchina virtuale e configurazione della macchina virtuale toohello dimensioni.</span><span class="sxs-lookup"><span data-stu-id="3e335-141">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="3e335-142">Immagine di macchina virtuale hello set come immagine di origine per hello nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3e335-142">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="3e335-143">Impostare l'immagine di origine hello usando un ID di hello dell'immagine di macchina virtuale hello gestito.</span><span class="sxs-lookup"><span data-stu-id="3e335-143">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="3e335-144">Impostare la configurazione del sistema operativo hello e aggiungere una scheda di rete hello.</span><span class="sxs-lookup"><span data-stu-id="3e335-144">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="3e335-145">Immettere un tipo di archiviazione hello (PremiumLRS o StandardLRS) e dimensioni hello del disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="3e335-145">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="3e335-146">In questo esempio imposta il tipo di account hello troppo**PremiumLRS**, hello dimensioni disco troppo**128 GB** e memorizzazione nella cache del disco troppo**ReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="3e335-146">This example sets hello account type too**PremiumLRS**, hello disk size too**128 GB** and disk caching too**ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="3e335-147">Creare VM hello</span><span class="sxs-lookup"><span data-stu-id="3e335-147">Create hello VM</span></span>

<span data-ttu-id="3e335-148">Crea nuova macchina virtuale utilizzando la configurazione di hello che abbiamo creato e archiviato in hello hello **$vm** variabile.</span><span class="sxs-lookup"><span data-stu-id="3e335-148">Create hello new Vm using hello configuration that we have built and stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="3e335-149">Verificare che hello che è stata creata una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="3e335-149">Verify that hello VM was created</span></span>
<span data-ttu-id="3e335-150">Al termine, si dovrebbe essere hello macchina virtuale appena creata in hello [portale di Azure](https://portal.azure.com) in **Sfoglia** > **macchine virtuali**, o tramite hello seguenti Comandi di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3e335-150">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="3e335-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3e335-151">Next steps</span></span>
<span data-ttu-id="3e335-152">vedere la nuova macchina virtuale con Azure PowerShell, toomanage [creare e gestire macchine virtuali di Windows con il modulo di Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3e335-152">toomanage your new virtual machine with Azure PowerShell, see [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

