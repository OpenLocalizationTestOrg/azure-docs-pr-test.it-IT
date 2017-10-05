---
title: "Creare e gestire VM Windows in Azure che usano più schede di interfaccia di rete | Microsoft Docs"
description: "Informazioni su come creare e gestire una VM Windows a cui sono collegate più schede di interfaccia di rete usando i modelli di Azure PowerShell o Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 3bd99a67dae41de3533d7f6e244eb7ee3ecc4049
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="fb2f6-103">Creare e gestire una macchina virtuale Windows che ha più schede di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="fb2f6-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="fb2f6-104">Alle macchine virtuali (VM) in Azure possono essere collegate più schede di interfaccia di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached to them.</span></span> <span data-ttu-id="fb2f6-105">Uno scenario comune è quello di avere subnet diverse per la connettività front-end e back-end oppure una rete dedicata a una soluzione di monitoraggio o backup.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="fb2f6-106">Questo articolo illustra come creare una macchina virtuale a cui sono collegate più schede di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="fb2f6-106">This article details how to create a VM that has multiple NICs attached to it.</span></span> <span data-ttu-id="fb2f6-107">e come aggiungere o rimuovere le schede di interfaccia di rete da una VM esistente.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-107">You also learn how to add or remove NICs from an existing VM.</span></span> <span data-ttu-id="fb2f6-108">Le differenti [dimensioni della macchina virtuale](sizes.md) supportano un numero variabile di schede di rete, pertanto scegliere le dimensioni della macchina virtuale di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="fb2f6-109">Per informazioni dettagliate, incluse quelle sulla creazione di più schede di interfaccia di rete negli script di PowerShell, vedere [Distribuzione di macchine virtuali con più schede di interfaccia di rete](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="fb2f6-109">For detailed information, including how to create multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb2f6-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fb2f6-110">Prerequisites</span></span>
<span data-ttu-id="fb2f6-111">Verificare di aver prima [installato e configurato la versione più recente di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fb2f6-111">Make sure that you have the [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="fb2f6-112">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-112">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="fb2f6-113">I nomi dei parametri di esempio includono *myResourceGroup*, *myVnet* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="fb2f6-114">Creare una macchina virtuale con più NIC</span><span class="sxs-lookup"><span data-stu-id="fb2f6-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="fb2f6-115">Creare prima un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-115">First, create a resource group.</span></span> <span data-ttu-id="fb2f6-116">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroup* nella località *EastUs*:</span><span class="sxs-lookup"><span data-stu-id="fb2f6-116">The following example creates a resource group named *myResourceGroup* in the *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="fb2f6-117">Creare la rete virtuale e le subnet</span><span class="sxs-lookup"><span data-stu-id="fb2f6-117">Create virtual network and subnets</span></span>
<span data-ttu-id="fb2f6-118">Negli scenari comuni una rete virtuale ha due o più subnet.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-118">A common scenario is for a virtual network to have two or more subnets.</span></span> <span data-ttu-id="fb2f6-119">Una subnet può essere dedicata al traffico front-end e l'altra al traffico back-end.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-119">One subnet may be for front-end traffic, the other for back-end traffic.</span></span> <span data-ttu-id="fb2f6-120">Per connettersi a entrambe le subnet, si usano quindi più schede di interfaccia di rete nella VM.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-120">To connect to both subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="fb2f6-121">Definire due subnet della rete virtuale con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="fb2f6-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="fb2f6-122">L'esempio seguente definisce le subnet per *mySubnetFrontEnd* e *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="fb2f6-122">The following example defines the subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="fb2f6-123">Creare la rete virtuale e le subnet con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="fb2f6-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="fb2f6-124">L'esempio seguente crea una rete virtuale denominata *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="fb2f6-124">The following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="fb2f6-125">Creare più schede di rete</span><span class="sxs-lookup"><span data-stu-id="fb2f6-125">Create multiple NICs</span></span>
<span data-ttu-id="fb2f6-126">Creare due schede di interfaccia di rete con [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="fb2f6-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="fb2f6-127">Collegare una scheda di interfaccia di rete alla subnet front-end e l'altra alla subnet back-end.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-127">Attach one NIC to the front-end subnet and one NIC to the back-end subnet.</span></span> <span data-ttu-id="fb2f6-128">L'esempio seguente crea le schede di interfaccia di rete denominate *myNic1* e *myNic2*:</span><span class="sxs-lookup"><span data-stu-id="fb2f6-128">The following example creates NICs named *myNic1* and *myNic2*:</span></span>

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

<span data-ttu-id="fb2f6-129">In genere è necessario creare anche un [gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md) o un [servizio di bilanciamento del carico](../../load-balancer/load-balancer-overview.md) per gestire e distribuire il traffico tra le VM.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="fb2f6-130">L'articolo dettagliato sulla [macchina virtuale con più schede di interfaccia di rete](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) offre una guida alla creazione di un gruppo di sicurezza di rete e all'assegnazione delle schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-130">The [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-the-virtual-machine"></a><span data-ttu-id="fb2f6-131">Creare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fb2f6-131">Create the virtual machine</span></span>
<span data-ttu-id="fb2f6-132">Ora è possibile iniziare con la configurazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-132">Now start to build your VM configuration.</span></span> <span data-ttu-id="fb2f6-133">Ad ogni dimensione della macchina virtuale corrisponde un limite del numero totale di schede di rete che è possibile aggiungere.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-133">Each VM size has a limit for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="fb2f6-134">Per altre informazioni, vedere [Dimensioni delle macchine virtuali in Azure](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="fb2f6-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="fb2f6-135">Impostare le credenziali della VM sulla variabile `$cred` come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="fb2f6-135">Set your VM credentials to the `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="fb2f6-136">Definire la VM con [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span><span class="sxs-lookup"><span data-stu-id="fb2f6-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="fb2f6-137">L'esempio seguente definisce una VM denominata *myVM* e usa una dimensione della VM che supporta fino a due schede di interfaccia di rete (*Standard_DS3_v2*):</span><span class="sxs-lookup"><span data-stu-id="fb2f6-137">The following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="fb2f6-138">Creare il resto della configurazione della VM con [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) e [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span><span class="sxs-lookup"><span data-stu-id="fb2f6-138">Create the rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="fb2f6-139">L'esempio seguente crea una VM Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="fb2f6-139">The following example creates a Windows Server 2016 VM:</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. <span data-ttu-id="fb2f6-140">Collegare le due schede di interfaccia di rete create prima con [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="fb2f6-140">Attach the two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="fb2f6-141">Creare infine la VM con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="fb2f6-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-to-an-existing-vm"></a><span data-ttu-id="fb2f6-142">Aggiungere una scheda di interfaccia di rete a una VM esistente</span><span class="sxs-lookup"><span data-stu-id="fb2f6-142">Add a NIC to an existing VM</span></span>
<span data-ttu-id="fb2f6-143">Per aggiungere una scheda di interfaccia di rete virtuale a una VM esistente, si dealloca la VM, si aggiunge la scheda di interfaccia di rete virtuale, quindi si avvia la VM.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-143">To add a virtual NIC to an existing VM, you deallocate the VM, add the virtual NIC, then start the VM.</span></span>

1. <span data-ttu-id="fb2f6-144">Deallocare la VM con [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="fb2f6-144">Deallocate the VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="fb2f6-145">L'esempio seguente dealloca la VM denominata *myVM* in *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="fb2f6-145">The following example deallocates the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="fb2f6-146">Ottenere la configurazione esistente della VM con [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="fb2f6-146">Get the existing configuration of the VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="fb2f6-147">L'esempio seguente ottiene le informazioni relative alla macchina virtuale denominata *myVM* in *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="fb2f6-147">The following example gets information for the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="fb2f6-148">L'esempio seguente crea una scheda di interfaccia di rete virtuale con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface), denominata *myNic3* e collegata *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-148">The following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached to *mySubnetBackEnd*.</span></span> <span data-ttu-id="fb2f6-149">La scheda di interfaccia di rete virtuale viene quindi collegata alla VM denominata *myVM* in *myResourceGroup* con [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="fb2f6-149">The virtual NIC is then attached to the VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for the back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get the ID of the new virtual NIC and add to VM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="fb2f6-150">Schede di interfaccia di rete virtuale primarie</span><span class="sxs-lookup"><span data-stu-id="fb2f6-150">Primary virtual NICs</span></span>
    <span data-ttu-id="fb2f6-151">Una delle schede di interfaccia di rete in una VM con più schede di interfaccia di rete deve essere primaria.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-151">One of the NICs on a multi-NIC VM needs to be primary.</span></span> <span data-ttu-id="fb2f6-152">Se una delle schede di interfaccia di rete virtuale esistenti nella VM è già impostata come primaria, è possibile saltare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-152">If one of the existing virtual NICs on the VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="fb2f6-153">L'esempio seguente presuppone che due schede di interfaccia di rete virtuale siano ora presenti in una VM e che si voglia aggiungere la prima scheda di interfaccia di rete (`[0]`) come primaria:</span><span class="sxs-lookup"><span data-stu-id="fb2f6-153">The following example assumes that two virtual NICs are now present on a VM and you wish to add the first NIC (`[0]`) as the primary:</span></span>
        
    ```powershell
    # List existing NICs on the VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 to be primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update the VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="fb2f6-154">Avviare la VM con [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="fb2f6-154">Start the VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="fb2f6-155">Rimuovere una scheda di interfaccia di rete da una VM esistente</span><span class="sxs-lookup"><span data-stu-id="fb2f6-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="fb2f6-156">Per rimuovere una scheda di interfaccia di rete virtuale da una VM esistente, si dealloca la VM, si rimuove la scheda di interfaccia di rete virtuale, quindi si avvia la VM.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-156">To remove a virtual NIC from an existing VM, you deallocate the VM, remove the virtual NIC, then start the VM.</span></span>

1. <span data-ttu-id="fb2f6-157">Deallocare la VM con [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="fb2f6-157">Deallocate the VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="fb2f6-158">L'esempio seguente dealloca la VM denominata *myVM* in *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="fb2f6-158">The following example deallocates the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="fb2f6-159">Ottenere la configurazione esistente della VM con [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="fb2f6-159">Get the existing configuration of the VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="fb2f6-160">L'esempio seguente ottiene le informazioni relative alla macchina virtuale denominata *myVM* in *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="fb2f6-160">The following example gets information for the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="fb2f6-161">Ottenere informazioni sulla rimozione della scheda di interfaccia di rete con [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="fb2f6-161">Get information about the NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="fb2f6-162">L'esempio seguente ottiene informazioni su *myNic3*:</span><span class="sxs-lookup"><span data-stu-id="fb2f6-162">The following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on the VM if you need to determine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="fb2f6-163">Rimuovere la scheda di interfaccia di rete con [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) e quindi aggiornare la VM con [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="fb2f6-163">Remove the NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update the VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="fb2f6-164">L'esempio seguente rimuove *myNic3* ottenuta da `$nicId` nel passaggio precedente:</span><span class="sxs-lookup"><span data-stu-id="fb2f6-164">The following example removes *myNic3* as obtained by `$nicId` in the preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="fb2f6-165">Avviare la VM con [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="fb2f6-165">Start the VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="fb2f6-166">Creare più schede di interfaccia di rete con i modelli</span><span class="sxs-lookup"><span data-stu-id="fb2f6-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="fb2f6-167">I modelli di Azure Resource Manager offrono un modo di creare più istanze di una risorsa durante la distribuzione, come ad esempio la creazione di più schede di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-167">Azure Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="fb2f6-168">I modelli di Resource Manager usano i file JSON dichiarativi per definire l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-168">Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="fb2f6-169">Per altre informazioni, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fb2f6-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="fb2f6-170">È possibile usare *copy* per specificare il numero di istanze da creare:</span><span class="sxs-lookup"><span data-stu-id="fb2f6-170">You can use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="fb2f6-171">Per altre informazioni, vedere [Creazione di più istanze con *copy*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="fb2f6-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="fb2f6-172">È anche possibile usare `copyIndex()` per aggiungere un numero a un nome di risorsa.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-172">You can also use `copyIndex()` to append a number to a resource name.</span></span> <span data-ttu-id="fb2f6-173">È quindi possibile creare *myNic1*, *MyNic2* e così via.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="fb2f6-174">Il codice seguente illustra un esempio di aggiunta del valore di indice:</span><span class="sxs-lookup"><span data-stu-id="fb2f6-174">The following code shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="fb2f6-175">È possibile consultare un esempio completo di [creazione di più schede di interfaccia di rete tramite i modelli di Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="fb2f6-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb2f6-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fb2f6-176">Next steps</span></span>
<span data-ttu-id="fb2f6-177">Vedere [Dimensioni per le macchine virtuali Windows](sizes.md) se si deve creare una VM con più schede di interfacce di rete.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-177">Review [Windows VM sizes](sizes.md) when you're trying to create a VM that has multiple NICs.</span></span> <span data-ttu-id="fb2f6-178">Prestare attenzione al numero massimo di schede di interfaccia di rete supportato per ogni dimensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fb2f6-178">Pay attention to the maximum number of NICs that each VM size supports.</span></span> 


