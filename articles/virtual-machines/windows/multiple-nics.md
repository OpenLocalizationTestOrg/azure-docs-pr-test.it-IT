---
title: "aaaCreate e gestire macchine virtuali di Windows Azure che utilizzano più schede di rete | Documenti Microsoft"
description: "Informazioni su come toocreate e gestire macchine Virtuali di Windows che dispone di più tooit collegato a schede di rete tramite modelli di Azure PowerShell o Gestione risorse."
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
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="6e6a3-103">Creare e gestire una macchina virtuale Windows che ha più schede di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="6e6a3-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="6e6a3-104">Macchine virtuali (VM) in Azure può avere più toothem schede (NIC) collegato interfaccia di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached toothem.</span></span> <span data-ttu-id="6e6a3-105">Uno scenario comune è toohave subnet diverse per la connettività front-end e back-end, o una rete dedicata tooa monitoraggio o una soluzione di backup.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="6e6a3-106">In questo articolo illustra in dettaglio come toocreate una macchina virtuale che dispone di più schede di rete associata tooit.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-106">This article details how toocreate a VM that has multiple NICs attached tooit.</span></span> <span data-ttu-id="6e6a3-107">Verrà inoltre descritto come le schede NIC tooadd o rimuovere da una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-107">You also learn how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="6e6a3-108">Le differenti [dimensioni della macchina virtuale](sizes.md) supportano un numero variabile di schede di rete, pertanto scegliere le dimensioni della macchina virtuale di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="6e6a3-109">Per informazioni dettagliate, tra cui toocreate vedere più schede di rete all'interno di script PowerShell [distribuzione di macchine virtuali di più schede di rete](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="6e6a3-109">For detailed information, including how toocreate multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e6a3-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6e6a3-110">Prerequisites</span></span>
<span data-ttu-id="6e6a3-111">Assicurarsi di avere hello [versione più recente di Azure PowerShell installato e configurato](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6e6a3-111">Make sure that you have hello [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="6e6a3-112">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="6e6a3-113">I nomi dei parametri di esempio includono *myResourceGroup*, *myVnet* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="6e6a3-114">Creare una macchina virtuale con più NIC</span><span class="sxs-lookup"><span data-stu-id="6e6a3-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="6e6a3-115">Creare prima un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-115">First, create a resource group.</span></span> <span data-ttu-id="6e6a3-116">esempio Hello crea un gruppo di risorse denominato *myResourceGroup* in hello *EastUs* percorso:</span><span class="sxs-lookup"><span data-stu-id="6e6a3-116">hello following example creates a resource group named *myResourceGroup* in hello *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="6e6a3-117">Creare la rete virtuale e le subnet</span><span class="sxs-lookup"><span data-stu-id="6e6a3-117">Create virtual network and subnets</span></span>
<span data-ttu-id="6e6a3-118">Uno scenario comune è per una rete virtuale di toohave due o più subnet.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-118">A common scenario is for a virtual network toohave two or more subnets.</span></span> <span data-ttu-id="6e6a3-119">Una subnet sia per il traffico front-end, hello altri per il traffico di back-end.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-119">One subnet may be for front-end traffic, hello other for back-end traffic.</span></span> <span data-ttu-id="6e6a3-120">tooconnect tooboth subnet, quindi utilizzare più schede di rete nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-120">tooconnect tooboth subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="6e6a3-121">Definire due subnet della rete virtuale con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="6e6a3-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="6e6a3-122">esempio Hello definisce subnet hello per *mySubnetFrontEnd* e *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="6e6a3-122">hello following example defines hello subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="6e6a3-123">Creare la rete virtuale e le subnet con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="6e6a3-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="6e6a3-124">esempio Hello crea una rete virtuale denominata *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="6e6a3-124">hello following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="6e6a3-125">Creare più schede di rete</span><span class="sxs-lookup"><span data-stu-id="6e6a3-125">Create multiple NICs</span></span>
<span data-ttu-id="6e6a3-126">Creare due schede di interfaccia di rete con [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="6e6a3-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="6e6a3-127">Collegare una scheda di rete toohello front-end subnet e una scheda di rete toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-127">Attach one NIC toohello front-end subnet and one NIC toohello back-end subnet.</span></span> <span data-ttu-id="6e6a3-128">esempio Hello crea NIC denominata *myNic1* e *myNic2*:</span><span class="sxs-lookup"><span data-stu-id="6e6a3-128">hello following example creates NICs named *myNic1* and *myNic2*:</span></span>

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

<span data-ttu-id="6e6a3-129">In genere si crea anche un [il gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md) o [bilanciamento del carico](../../load-balancer/load-balancer-overview.md) toohelp gestire e distribuire il traffico tra le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="6e6a3-130">Hello [dettagliate più schede di rete VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) articolo illustra la creazione di un gruppo di sicurezza di rete e l'assegnazione delle schede di rete.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-130">hello [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="6e6a3-131">Creare una macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="6e6a3-131">Create hello virtual machine</span></span>
<span data-ttu-id="6e6a3-132">Ora avviare toobuild configurazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-132">Now start toobuild your VM configuration.</span></span> <span data-ttu-id="6e6a3-133">Ogni dimensione della macchina virtuale ha un limite per il numero totale di schede di rete che è possibile aggiungere VM tooa hello.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-133">Each VM size has a limit for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="6e6a3-134">Per altre informazioni, vedere [Dimensioni delle macchine virtuali in Azure](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="6e6a3-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="6e6a3-135">Impostare il toohello credenziali VM `$cred` variabile come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6e6a3-135">Set your VM credentials toohello `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="6e6a3-136">Definire la VM con [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span><span class="sxs-lookup"><span data-stu-id="6e6a3-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="6e6a3-137">esempio Hello definisce una macchina virtuale denominata *myVM* e si utilizza una dimensione di macchina virtuale che supporta più di due schede di rete (*Standard_DS3_v2*):</span><span class="sxs-lookup"><span data-stu-id="6e6a3-137">hello following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="6e6a3-138">Creare il resto di hello della configurazione della macchina virtuale con [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) e [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span><span class="sxs-lookup"><span data-stu-id="6e6a3-138">Create hello rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="6e6a3-139">Hello di esempio seguente crea una macchina virtuale di Windows Server 2016:</span><span class="sxs-lookup"><span data-stu-id="6e6a3-139">hello following example creates a Windows Server 2016 VM:</span></span>

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

4. <span data-ttu-id="6e6a3-140">Collegare hello due schede di rete creato in precedenza con [Aggiungi AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="6e6a3-140">Attach hello two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="6e6a3-141">Creare infine la VM con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="6e6a3-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a><span data-ttu-id="6e6a3-142">Aggiungere un tooan NIC VM esistente</span><span class="sxs-lookup"><span data-stu-id="6e6a3-142">Add a NIC tooan existing VM</span></span>
<span data-ttu-id="6e6a3-143">aggiungere un tooan NIC virtuale macchina virtuale esistente, si dealloca hello VM, tooadd hello NIC virtuale, quindi avviare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-143">tooadd a virtual NIC tooan existing VM, you deallocate hello VM, add hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="6e6a3-144">Deallocare hello macchina virtuale con [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="6e6a3-144">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="6e6a3-145">esempio Hello dealloca hello macchina virtuale denominata *myVM* in *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="6e6a3-145">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="6e6a3-146">Ottenere la configurazione esistente di hello di hello VM con [Get AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="6e6a3-146">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="6e6a3-147">Hello seguente esempio mostra come ottenere informazioni per la macchina virtuale denominata hello *myVM* in *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="6e6a3-147">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="6e6a3-148">esempio Hello crea una scheda di rete virtuale con [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) denominato *myNic3* collegato troppo*mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-148">hello following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached too*mySubnetBackEnd*.</span></span> <span data-ttu-id="6e6a3-149">Hello NIC virtuale viene quindi collegato toohello macchina virtuale denominata *myVM* in *myResourceGroup* con [Aggiungi AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="6e6a3-149">hello virtual NIC is then attached toohello VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="6e6a3-150">Schede di interfaccia di rete virtuale primarie</span><span class="sxs-lookup"><span data-stu-id="6e6a3-150">Primary virtual NICs</span></span>
    <span data-ttu-id="6e6a3-151">Una delle schede di rete in una macchina virtuale multi-NIC hello deve toobe primario.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-151">One of hello NICs on a multi-NIC VM needs toobe primary.</span></span> <span data-ttu-id="6e6a3-152">Se una delle schede di rete virtuale esistente di hello in hello VM è già impostato come primario, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-152">If one of hello existing virtual NICs on hello VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="6e6a3-153">Hello seguente si presuppone che due schede di rete virtuale sono ora presenti in una macchina virtuale e si desidera tooadd hello prima NIC (`[0]`) come hello primario:</span><span class="sxs-lookup"><span data-stu-id="6e6a3-153">hello following example assumes that two virtual NICs are now present on a VM and you wish tooadd hello first NIC (`[0]`) as hello primary:</span></span>
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="6e6a3-154">Avvia macchina virtuale con hello [inizio AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="6e6a3-154">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="6e6a3-155">Rimuovere una scheda di interfaccia di rete da una VM esistente</span><span class="sxs-lookup"><span data-stu-id="6e6a3-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="6e6a3-156">tooremove una scheda di rete virtuale da una macchina virtuale esistente, deallocare hello macchina virtuale, rimuovere hello NIC virtuale, quindi avviare hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-156">tooremove a virtual NIC from an existing VM, you deallocate hello VM, remove hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="6e6a3-157">Deallocare hello macchina virtuale con [Stop AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="6e6a3-157">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="6e6a3-158">esempio Hello dealloca hello macchina virtuale denominata *myVM* in *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="6e6a3-158">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="6e6a3-159">Ottenere la configurazione esistente di hello di hello VM con [Get AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="6e6a3-159">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="6e6a3-160">Hello seguente esempio mostra come ottenere informazioni per la macchina virtuale denominata hello *myVM* in *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="6e6a3-160">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="6e6a3-161">Ottenere informazioni su hello NIC rimuovere con [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="6e6a3-161">Get information about hello NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="6e6a3-162">Hello seguente esempio ottiene informazioni sul *myNic3*:</span><span class="sxs-lookup"><span data-stu-id="6e6a3-162">hello following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="6e6a3-163">Rimuovere hello NIC con [Remove AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) , quindi aggiornare hello macchina virtuale con [aggiornamento AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="6e6a3-163">Remove hello NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update hello VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="6e6a3-164">Hello esempio seguente viene rimosso *myNic3* ottenuta da `$nicId` nel precedente passaggio hello:</span><span class="sxs-lookup"><span data-stu-id="6e6a3-164">hello following example removes *myNic3* as obtained by `$nicId` in hello preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="6e6a3-165">Avvia macchina virtuale con hello [inizio AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="6e6a3-165">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="6e6a3-166">Creare più schede di interfaccia di rete con i modelli</span><span class="sxs-lookup"><span data-stu-id="6e6a3-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="6e6a3-167">Modelli di gestione risorse di Azure forniscono un modo toocreate più istanze di una risorsa durante la distribuzione, ad esempio la creazione di più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-167">Azure Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="6e6a3-168">Modelli di gestione risorse utilizzano dichiarativa JSON file toodefine l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-168">Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="6e6a3-169">Per altre informazioni, vedere [Panoramica di Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6e6a3-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="6e6a3-170">È possibile utilizzare *copia* numero hello toospecify di toocreate istanze:</span><span class="sxs-lookup"><span data-stu-id="6e6a3-170">You can use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="6e6a3-171">Per altre informazioni, vedere [Creazione di più istanze con *copy*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="6e6a3-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="6e6a3-172">È inoltre possibile utilizzare `copyIndex()` tooappend un nome di risorsa tooa numero.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-172">You can also use `copyIndex()` tooappend a number tooa resource name.</span></span> <span data-ttu-id="6e6a3-173">È quindi possibile creare *myNic1*, *MyNic2* e così via.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="6e6a3-174">Hello codice riportato di seguito viene illustrato un esempio di aggiunta di valore di indice hello:</span><span class="sxs-lookup"><span data-stu-id="6e6a3-174">hello following code shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="6e6a3-175">È possibile consultare un esempio completo di [creazione di più schede di interfaccia di rete tramite i modelli di Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="6e6a3-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e6a3-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6e6a3-176">Next steps</span></span>
<span data-ttu-id="6e6a3-177">Revisione [dimensioni delle macchine Virtuali di Windows](sizes.md) quando si cerca toocreate una macchina virtuale che dispone di più schede di rete.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-177">Review [Windows VM sizes](sizes.md) when you're trying toocreate a VM that has multiple NICs.</span></span> <span data-ttu-id="6e6a3-178">Prestare attenzione toohello massimo schede di rete che supporta ogni dimensione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6e6a3-178">Pay attention toohello maximum number of NICs that each VM size supports.</span></span> 


