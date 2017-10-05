---
title: Creare una macchina virtuale da un'immagine di macchina virtuale gestita in Azure | Documentazione Microsoft
description: Creare una macchina virtuale Windows da un'immagine di macchina virtuale gestita generalizzata usando Azure PowerShell nel modello di distribuzione Resource Manager.
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
ms.openlocfilehash: 2bb2d66271178a64ec0f4642e46b23f5618a56d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-vm-from-a-managed-image"></a><span data-ttu-id="a6fff-103">Creare una macchina virtuale da un'immagine gestita</span><span class="sxs-lookup"><span data-stu-id="a6fff-103">Create a VM from a managed image</span></span>

<span data-ttu-id="a6fff-104">È possibile creare più macchine virtuali da un'immagine di macchina virtuale gestita in Azure.</span><span class="sxs-lookup"><span data-stu-id="a6fff-104">You can create multiple VMs from a managed VM image in Azure.</span></span> <span data-ttu-id="a6fff-105">Un'immagine di macchina virtuale gestita contiene le informazioni necessarie per creare una macchina virtuale, inclusi i dischi dati e del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="a6fff-105">A managed VM image contains the information necessary to create a VM, including the OS and data disks.</span></span> <span data-ttu-id="a6fff-106">I dischi rigidi virtuali che costituiscono l'immagine, inclusi i dischi del sistema operativo e qualsiasi disco dati, vengono archiviati come dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="a6fff-106">The VHDs that make up the image, including both the OS disks and any data disks, are stored as managed disks.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="a6fff-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a6fff-107">Prerequisites</span></span>

<span data-ttu-id="a6fff-108">È necessario aver già [creato un'immagine di macchina virtuale gestita](capture-image-resource.md) da usare per creare la nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a6fff-108">You need to have already [created a managed VM image](capture-image-resource.md) to use for creating the new VM.</span></span> 

<span data-ttu-id="a6fff-109">Verificare di disporre della versione più recente dei moduli di PowerShell AzureRM.Compute e AzureRM.Network.</span><span class="sxs-lookup"><span data-stu-id="a6fff-109">Make sure that you have the latest versions of the AzureRM.Compute and AzureRM.Network PowerShell modules.</span></span> <span data-ttu-id="a6fff-110">Aprire un prompt dei comandi di PowerShell come Amministratore ed eseguire il comando seguente per installarli.</span><span class="sxs-lookup"><span data-stu-id="a6fff-110">Open a PowerShell prompt as an Administrator and run the following command to install them.</span></span>

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
<span data-ttu-id="a6fff-111">Per altre informazioni, vedere [Controllo delle versioni di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a6fff-111">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>



## <a name="collect-information-about-the-image"></a><span data-ttu-id="a6fff-112">Raccogliere informazioni relative all'immagine</span><span class="sxs-lookup"><span data-stu-id="a6fff-112">Collect information about the image</span></span>

<span data-ttu-id="a6fff-113">Innanzitutto, è necessario raccogliere le informazioni di base dell'immagine e creare una variabile per l'immagine.</span><span class="sxs-lookup"><span data-stu-id="a6fff-113">First we need to gather basic information about the image and create a variable for the image.</span></span> <span data-ttu-id="a6fff-114">Questo esempio usa un'immagine di macchina virtuale gestita denominata **myImage** nel gruppo di risorse **myResourceGroup** nell'area **Stati Uniti centro-occidentali**.</span><span class="sxs-lookup"><span data-stu-id="a6fff-114">This example uses a managed VM image named **myImage** that is in the **myResourceGroup** resource group in the **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="a6fff-115">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="a6fff-115">Create a virtual network</span></span>
<span data-ttu-id="a6fff-116">Creare la rete virtuale e la subnet della [rete virtuale](../../virtual-network/virtual-networks-overview.md) stessa.</span><span class="sxs-lookup"><span data-stu-id="a6fff-116">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="a6fff-117">Creare la subnet.</span><span class="sxs-lookup"><span data-stu-id="a6fff-117">Create the subnet.</span></span> <span data-ttu-id="a6fff-118">Questo esempio crea una subnet denominata **mySubnet** con un prefisso di indirizzo di **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="a6fff-118">This example creates a subnet named **mySubnet** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="a6fff-119">Creare la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a6fff-119">Create the virtual network.</span></span> <span data-ttu-id="a6fff-120">Questo esempio crea una rete virtuale denominata **myVnet** con un prefisso di indirizzo di **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="a6fff-120">This example creates a virtual network named **myVnet** with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="a6fff-121">Creare un indirizzo IP pubblico e un'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="a6fff-121">Create a public IP address and network interface</span></span>

<span data-ttu-id="a6fff-122">Per abilitare la comunicazione con la macchina virtuale nella rete virtuale, sono necessari un [indirizzo IP pubblico](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) e un'interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="a6fff-122">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="a6fff-123">Creare un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="a6fff-123">Create a public IP address.</span></span> <span data-ttu-id="a6fff-124">In questo esempio viene creato un indirizzo IP pubblico denominato **myPip**.</span><span class="sxs-lookup"><span data-stu-id="a6fff-124">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="a6fff-125">Creare la scheda NIC.</span><span class="sxs-lookup"><span data-stu-id="a6fff-125">Create the NIC.</span></span> <span data-ttu-id="a6fff-126">In questo esempio viene creata una scheda NIC denominata **myNic**.</span><span class="sxs-lookup"><span data-stu-id="a6fff-126">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="a6fff-127">Creare il gruppo di sicurezza di rete e una regola RDP</span><span class="sxs-lookup"><span data-stu-id="a6fff-127">Create the network security group and an RDP rule</span></span>

<span data-ttu-id="a6fff-128">Per essere in grado di accedere alla VM tramite RDP, è necessario disporre di una regola di sicurezza della rete (NSG) che consenta l'accesso RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="a6fff-128">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="a6fff-129">In questo esempio viene creato un gruppo di sicurezza di rete denominato **myNsg** contenente una regola denominata **myRdpRule** che consente il traffico RDP sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="a6fff-129">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="a6fff-130">Per altre informazioni sui gruppi di sicurezza di rete, vedere [Apertura di porte a una VM tramite PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6fff-130">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

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


## <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="a6fff-131">Creare una variabile per la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="a6fff-131">Create a variable for the virtual network</span></span>

<span data-ttu-id="a6fff-132">Creare una variabile per la rete virtuale realizzata.</span><span class="sxs-lookup"><span data-stu-id="a6fff-132">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-the-credentials-for-the-vm"></a><span data-ttu-id="a6fff-133">Ottenere le credenziali per la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a6fff-133">Get the credentials for the VM</span></span>

<span data-ttu-id="a6fff-134">Il cmdlet seguente apre una finestra in cui verrà immesso un nuovo nome utente e una nuova password da usare come account dell'amministratore locale per accedere in da remoto alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a6fff-134">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-the-vm-name-computer-name-and-the-size-of-the-vm"></a><span data-ttu-id="a6fff-135">Impostare le variabili per il nome della macchina virtuale, per il nome del computer e per le dimensioni della macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a6fff-135">Set variables for the VM name, computer name and the size of the VM</span></span>

1. <span data-ttu-id="a6fff-136">Creare variabili per il nome della macchina virtuale e per il nome del computer.</span><span class="sxs-lookup"><span data-stu-id="a6fff-136">Create variables for the VM name and computer name.</span></span> <span data-ttu-id="a6fff-137">In questo il nome della macchina virtuale viene impostato su **myVM** e il nome del computer viene impostato su **myComputer**.</span><span class="sxs-lookup"><span data-stu-id="a6fff-137">This example sets the VM name as **myVM** and the computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="a6fff-138">Impostare le dimensioni della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a6fff-138">Set the size of the virtual machine.</span></span> <span data-ttu-id="a6fff-139">Questo esempio crea una macchina virtuale con dimensione **Standard_DS1_v2**.</span><span class="sxs-lookup"><span data-stu-id="a6fff-139">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="a6fff-140">Per altre informazioni, vedere la documentazione [Dimensioni per le macchine virtuali Windows in Azure](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/).</span><span class="sxs-lookup"><span data-stu-id="a6fff-140">See the [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="a6fff-141">Aggiungere il nome della macchina virtuale e le dimensioni per la configurazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a6fff-141">Add the VM name and size to the VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-the-vm-image-as-source-image-for-the-new-vm"></a><span data-ttu-id="a6fff-142">Impostare l'immagine della macchina virtuale come immagine di origine per la nuova macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a6fff-142">Set the VM image as source image for the new VM</span></span>

<span data-ttu-id="a6fff-143">Impostare l'immagine di origine usando l'ID dell'immagine di macchina virtuale gestita.</span><span class="sxs-lookup"><span data-stu-id="a6fff-143">Set the source image using the ID of the managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-the-os-configuration-and-add-the-nic"></a><span data-ttu-id="a6fff-144">Impostare la configurazione del sistema operativo e aggiungere la scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="a6fff-144">Set the OS configuration and add the NIC.</span></span>

<span data-ttu-id="a6fff-145">Immettere il tipo di archiviazione (PremiumLRS o StandardLRS) e le dimensioni del disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="a6fff-145">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span></span> <span data-ttu-id="a6fff-146">In questo esempio il tipo di account viene impostato su **PremiumLRS**, le dimensioni del disco su **128 GB** e il caching del disco su **ReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="a6fff-146">This example sets the account type to **PremiumLRS**, the disk size to **128 GB** and disk caching to **ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-the-vm"></a><span data-ttu-id="a6fff-147">Creare la VM</span><span class="sxs-lookup"><span data-stu-id="a6fff-147">Create the VM</span></span>

<span data-ttu-id="a6fff-148">Creare la nuova macchina virtuale usando la configurazione creata e archiviata nella variabile **$vm**.</span><span class="sxs-lookup"><span data-stu-id="a6fff-148">Create the new Vm using the configuration that we have built and stored in the **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="a6fff-149">Verificare che la VM sia stata creata</span><span class="sxs-lookup"><span data-stu-id="a6fff-149">Verify that the VM was created</span></span>
<span data-ttu-id="a6fff-150">Al termine, la VM appena creata dovrebbe essere visualizzata nel [portale di Azure](https://portal.azure.com) in **Browse** (Sfoglia)  > **Macchine virtuali**. In alternativa, è possibile usare i comandi PowerShell seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6fff-150">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="a6fff-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a6fff-151">Next steps</span></span>
<span data-ttu-id="a6fff-152">Per gestire la nuova macchina virtuale con Azure PowerShell, vedere [Creare e gestire VM di Windows con il modulo Azure PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a6fff-152">To manage your new virtual machine with Azure PowerShell, see [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

