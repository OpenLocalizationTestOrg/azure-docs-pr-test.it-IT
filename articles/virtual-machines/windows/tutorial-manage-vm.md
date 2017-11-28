---
title: aaaCreate e gestire macchine virtuali di Windows con hello modulo Azure PowerShell | Documenti Microsoft
description: 'Esercitazione: creare e gestire le macchine virtuali Windows con hello modulo Azure PowerShell'
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a><span data-ttu-id="c70df-103">Creare e gestire le macchine virtuali Windows con hello modulo Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c70df-103">Create and Manage Windows VMs with hello Azure PowerShell module</span></span>

<span data-ttu-id="c70df-104">Le macchine virtuali di Azure offrono un ambiente di elaborazione completamente configurabile e flessibile.</span><span class="sxs-lookup"><span data-stu-id="c70df-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="c70df-105">Questa esercitazione illustra gli elementi di base della distribuzione di una macchina virtuale di Azure, ad esempio la selezione delle dimensioni di una VM, la selezione dell'immagine di una VM e la distribuzione di una VM.</span><span class="sxs-lookup"><span data-stu-id="c70df-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="c70df-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="c70df-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c70df-107">Creare e connettersi tooa VM</span><span class="sxs-lookup"><span data-stu-id="c70df-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="c70df-108">Selezionare e usare le immagini di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c70df-108">Select and use VM images</span></span>
> * <span data-ttu-id="c70df-109">Visualizzare e usare macchine virtuali di dimensioni specifiche</span><span class="sxs-lookup"><span data-stu-id="c70df-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="c70df-110">Ridimensionare una VM</span><span class="sxs-lookup"><span data-stu-id="c70df-110">Resize a VM</span></span>
> * <span data-ttu-id="c70df-111">Visualizzare e comprendere lo stato di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c70df-111">View and understand VM state</span></span>

<span data-ttu-id="c70df-112">Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo.</span><span class="sxs-lookup"><span data-stu-id="c70df-112">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="c70df-113">Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="c70df-113">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="c70df-114">Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="c70df-114">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="c70df-115">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="c70df-115">Create resource group</span></span>

<span data-ttu-id="c70df-116">Creare un gruppo di risorse con hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) comando.</span><span class="sxs-lookup"><span data-stu-id="c70df-116">Create a resource group with hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> 

<span data-ttu-id="c70df-117">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="c70df-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="c70df-118">Il gruppo di risorse deve essere creato prima della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c70df-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="c70df-119">In questo esempio, un gruppo di risorse denominato *myResourceGroupVM* viene creato in hello *EastUS* area.</span><span class="sxs-lookup"><span data-stu-id="c70df-119">In this example, a resource group named *myResourceGroupVM* is created in hello *EastUS* region.</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

<span data-ttu-id="c70df-120">gruppo di risorse Hello viene specificato durante la creazione o modifica di una macchina virtuale, che può essere visualizzata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c70df-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="c70df-121">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c70df-121">Create virtual machine</span></span>

<span data-ttu-id="c70df-122">Una macchina virtuale deve essere connesso tooa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c70df-122">A virtual machine must be connected tooa virtual network.</span></span> <span data-ttu-id="c70df-123">Comunicare con la macchina virtuale hello tramite un indirizzo IP pubblico a una scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="c70df-123">You communicate with hello virtual machine using a public IP address through a network interface card.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="c70df-124">Creare una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="c70df-124">Create virtual network</span></span>

<span data-ttu-id="c70df-125">Creare una subnet con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="c70df-125">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="c70df-126">Creare una rete virtuale con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="c70df-126">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a><span data-ttu-id="c70df-127">Creare un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="c70df-127">Create public IP address</span></span>

<span data-ttu-id="c70df-128">Creare un indirizzo IP pubblico con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="c70df-128">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a><span data-ttu-id="c70df-129">Creare una scheda di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="c70df-129">Create network interface card</span></span>

<span data-ttu-id="c70df-130">Creare una scheda di interfaccia di rete con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="c70df-130">Create a network interface card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a><span data-ttu-id="c70df-131">Creare un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="c70df-131">Create network security group</span></span>

<span data-ttu-id="c70df-132">Un [gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md) di Azure consente di controllare il traffico in ingresso e in uscita per una o più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="c70df-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="c70df-133">Le regole di un gruppo di sicurezza di rete consentono o impediscono il traffico di rete su una porta specifica o un intervallo di porte.</span><span class="sxs-lookup"><span data-stu-id="c70df-133">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="c70df-134">Queste regole possono includere un prefisso dell'indirizzo di origine, in modo che solo il traffico proveniente da un'origine specificata possa comunicare con una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c70df-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span> <span data-ttu-id="c70df-135">server Web a IIS hello tooaccess che si sta installando, è necessario aggiungere una regola di gruppo in ingresso.</span><span class="sxs-lookup"><span data-stu-id="c70df-135">tooaccess hello IIS webserver that you are installing, you must add an inbound NSG rule.</span></span>

<span data-ttu-id="c70df-136">utilizzare una regola di gruppo in ingresso, toocreate [Aggiungi AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="c70df-136">toocreate an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="c70df-137">esempio Hello crea una regola di gruppo denominata *myNSGRule* che consente di aprire la porta *3389* per la macchina virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="c70df-137">hello following example creates an NSG rule named *myNSGRule* that opens port *3389* for hello virtual machine:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

<span data-ttu-id="c70df-138">Creare hello NSG utilizzando *myNSGRule* con [New AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="c70df-138">Create hello NSG using *myNSGRule* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

<span data-ttu-id="c70df-139">Aggiungi subnet toohello NSG hello nella rete virtuale di hello con [Set AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="c70df-139">Add hello NSG toohello subnet in hello virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="c70df-140">Rete virtuale hello di Update con [Set AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="c70df-140">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a><span data-ttu-id="c70df-141">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c70df-141">Create virtual machine</span></span>

<span data-ttu-id="c70df-142">Per la creazione di una macchina virtuale sono disponibili diverse opzioni, ad esempio l'immagine del sistema operativo, il ridimensionamento del disco e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="c70df-142">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="c70df-143">In questo esempio viene creata una macchina virtuale con un nome di *myVM* in esecuzione hello più recente di Windows Server 2016 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="c70df-143">In this example, a virtual machine is created with a name of *myVM* running hello latest version of Windows Server 2016 Datacenter.</span></span>

<span data-ttu-id="c70df-144">Impostare username hello e una password per account di amministratore hello nella macchina virtuale hello con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="c70df-144">Set hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="c70df-145">Creare la configurazione iniziale per la macchina virtuale hello con hello [New AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span><span class="sxs-lookup"><span data-stu-id="c70df-145">Create hello initial configuration for hello virtual machine with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="c70df-146">Aggiungi configurazione macchina virtuale con hello del sistema operativo informazioni toohello [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span><span class="sxs-lookup"><span data-stu-id="c70df-146">Add hello operating system information toohello virtual machine configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span></span>

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="c70df-147">Aggiungere hello immagine informazioni toohello configurazione della macchina virtuale con [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span><span class="sxs-lookup"><span data-stu-id="c70df-147">Add hello image information toohello virtual machine configuration with [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

<span data-ttu-id="c70df-148">Aggiungere hello del sistema operativo disco impostazioni toohello configurazione della macchina virtuale con [Set AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span><span class="sxs-lookup"><span data-stu-id="c70df-148">Add hello operating system disk settings toohello virtual machine configuration with [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

<span data-ttu-id="c70df-149">Aggiungi hello scheda di rete creato in precedenza toohello configurazione della macchina virtuale con [Aggiungi AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="c70df-149">Add hello network interface card that you previously created toohello virtual machine configuration with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="c70df-150">Creare una macchina virtuale hello con [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="c70df-150">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a><span data-ttu-id="c70df-151">Connettersi tooVM</span><span class="sxs-lookup"><span data-stu-id="c70df-151">Connect tooVM</span></span>

<span data-ttu-id="c70df-152">Una volta completata la distribuzione di hello, creare una connessione desktop remoto con la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="c70df-152">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="c70df-153">Eseguire i seguenti comandi tooreturn hello indirizzo IP pubblico della macchina virtuale hello hello.</span><span class="sxs-lookup"><span data-stu-id="c70df-153">Run hello following commands tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="c70df-154">Prendere nota dell'indirizzo IP per la connessione tooit con la connettività di web browser tootest in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="c70df-154">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

<span data-ttu-id="c70df-155">Comando che segue di hello utilizzare toocreate una sessione desktop remota con la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="c70df-155">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="c70df-156">Sostituire l'indirizzo IP hello con hello *publicIPAddress* della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c70df-156">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="c70df-157">Quando richiesto, immettere le credenziali di hello utilizzate durante la creazione di macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="c70df-157">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a><span data-ttu-id="c70df-158">Informazioni sulle immagini delle VM</span><span class="sxs-lookup"><span data-stu-id="c70df-158">Understand VM images</span></span>

<span data-ttu-id="c70df-159">Hello Azure marketplace include molte immagini di macchine virtuali che possono essere utilizzati toocreate una nuova macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c70df-159">hello Azure marketplace includes many virtual machine images that can be used toocreate a new virtual machine.</span></span> <span data-ttu-id="c70df-160">Nei passaggi precedenti hello, una macchina virtuale è stata creata utilizzando l'immagine di Windows Server 2016-Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="c70df-160">In hello previous steps, a virtual machine was created using hello Windows Server 2016-Datacenter image.</span></span> <span data-ttu-id="c70df-161">In questo passaggio, il modulo di PowerShell hello è marketplace hello toosearch usato per altre immagini di Windows, che può anche come base per nuove macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="c70df-161">In this step, hello PowerShell module is used toosearch hello marketplace for other Windows images, which can also as a base for new VMs.</span></span> <span data-ttu-id="c70df-162">Questo processo costituito da ricerca di server di pubblicazione hello, offerta e nome dell'immagine hello (Sku).</span><span class="sxs-lookup"><span data-stu-id="c70df-162">This process consists of finding hello publisher, offer, and hello image name (Sku).</span></span> 

<span data-ttu-id="c70df-163">Hello utilizzare [Get AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) comando tooreturn un elenco degli editori di immagine.</span><span class="sxs-lookup"><span data-stu-id="c70df-163">Use hello [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command tooreturn a list of image publishers.</span></span>  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

<span data-ttu-id="c70df-164">Hello utilizzare [Get AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn un elenco di offerte di immagine.</span><span class="sxs-lookup"><span data-stu-id="c70df-164">Use hello [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn a list of image offers.</span></span> <span data-ttu-id="c70df-165">Con questo comando, hello ha restituito l'elenco viene filtrato nel server di pubblicazione specificato hello.</span><span class="sxs-lookup"><span data-stu-id="c70df-165">With this command, hello returned list is filtered on hello specified publisher.</span></span> 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

<span data-ttu-id="c70df-166">Hello [Get AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) comando quindi filtrerà tooreturn di nome di server di pubblicazione e offerta hello un elenco di nomi di immagini.</span><span class="sxs-lookup"><span data-stu-id="c70df-166">hello [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) command will then filter on hello publisher and offer name tooreturn a list of image names.</span></span>

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

<span data-ttu-id="c70df-167">Queste informazioni possono essere utilizzati toodeploy una macchina virtuale con un'immagine specifica.</span><span class="sxs-lookup"><span data-stu-id="c70df-167">This information can be used toodeploy a VM with a specific image.</span></span> <span data-ttu-id="c70df-168">In questo esempio imposta il nome di immagine hello sull'oggetto VM hello.</span><span class="sxs-lookup"><span data-stu-id="c70df-168">This example sets hello image name on hello VM object.</span></span> <span data-ttu-id="c70df-169">Vedere esempi precedenti toohello in questa esercitazione per la procedura di distribuzione completa.</span><span class="sxs-lookup"><span data-stu-id="c70df-169">Refer toohello previous examples in this tutorial for complete deployment steps.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="c70df-170">Informazioni sulle dimensioni delle VM</span><span class="sxs-lookup"><span data-stu-id="c70df-170">Understand VM sizes</span></span>

<span data-ttu-id="c70df-171">Una dimensione di macchina virtuale determina la quantità hello delle risorse di calcolo, ad esempio memoria, CPU e GPU che vengono apportate una macchina virtuale disponibile toohello.</span><span class="sxs-lookup"><span data-stu-id="c70df-171">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="c70df-172">Macchine virtuali devono toobe creato con una dimensione appropriata per hello prevede che il carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c70df-172">Virtual machines need toobe created with a size appropriate for hello expect work load.</span></span> <span data-ttu-id="c70df-173">Se aumenta il carico di lavoro, è possibile ridimensionare una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="c70df-173">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="c70df-174">Dimensioni delle VM</span><span class="sxs-lookup"><span data-stu-id="c70df-174">VM Sizes</span></span>

<span data-ttu-id="c70df-175">Hello nella tabella seguente classifica le dimensioni in casi di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="c70df-175">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="c70df-176">Tipo</span><span class="sxs-lookup"><span data-stu-id="c70df-176">Type</span></span>                     | <span data-ttu-id="c70df-177">Dimensioni</span><span class="sxs-lookup"><span data-stu-id="c70df-177">Sizes</span></span>           |    <span data-ttu-id="c70df-178">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c70df-178">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c70df-179">Scopo generico</span><span class="sxs-lookup"><span data-stu-id="c70df-179">General purpose</span></span>         |<span data-ttu-id="c70df-180">DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="c70df-180">DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="c70df-181">Rapporto equilibrato tra CPU e memoria.</span><span class="sxs-lookup"><span data-stu-id="c70df-181">Balanced CPU-to-memory.</span></span> <span data-ttu-id="c70df-182">La soluzione ideale per sviluppo / test e le soluzioni di applicazioni e dati toomedium di piccole dimensioni.</span><span class="sxs-lookup"><span data-stu-id="c70df-182">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| <span data-ttu-id="c70df-183">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="c70df-183">Compute optimized</span></span>      | <span data-ttu-id="c70df-184">Fs, F</span><span class="sxs-lookup"><span data-stu-id="c70df-184">Fs, F</span></span>             | <span data-ttu-id="c70df-185">Rapporto elevato tra CPU e memoria.</span><span class="sxs-lookup"><span data-stu-id="c70df-185">High CPU-to-memory.</span></span> <span data-ttu-id="c70df-186">Soluzione idonea per applicazioni con livelli medi di traffico, dispositivi di rete e processi batch.</span><span class="sxs-lookup"><span data-stu-id="c70df-186">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| <span data-ttu-id="c70df-187">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="c70df-187">Memory optimized</span></span>       | <span data-ttu-id="c70df-188">GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="c70df-188">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="c70df-189">Rapporto elevato tra memoria e core.</span><span class="sxs-lookup"><span data-stu-id="c70df-189">High memory-to-core.</span></span> <span data-ttu-id="c70df-190">Ideale per i database relazionali, cache toolarge medium e analitica in memoria.</span><span class="sxs-lookup"><span data-stu-id="c70df-190">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| <span data-ttu-id="c70df-191">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="c70df-191">Storage optimized</span></span>       | <span data-ttu-id="c70df-192">Ls</span><span class="sxs-lookup"><span data-stu-id="c70df-192">Ls</span></span>                | <span data-ttu-id="c70df-193">I/O e velocità effettiva del disco elevati.</span><span class="sxs-lookup"><span data-stu-id="c70df-193">High disk throughput and IO.</span></span> <span data-ttu-id="c70df-194">Ideale per Big Data, database SQL e NoSQL.</span><span class="sxs-lookup"><span data-stu-id="c70df-194">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| <span data-ttu-id="c70df-195">GPU</span><span class="sxs-lookup"><span data-stu-id="c70df-195">GPU</span></span>           | <span data-ttu-id="c70df-196">NV, NC</span><span class="sxs-lookup"><span data-stu-id="c70df-196">NV, NC</span></span>            | <span data-ttu-id="c70df-197">VM specializzate ottimizzate per livelli intensivi di rendering della grafica ed editing di video.</span><span class="sxs-lookup"><span data-stu-id="c70df-197">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| <span data-ttu-id="c70df-198">Prestazioni elevate</span><span class="sxs-lookup"><span data-stu-id="c70df-198">High performance</span></span> | <span data-ttu-id="c70df-199">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="c70df-199">H, A8-11</span></span>          | <span data-ttu-id="c70df-200">Le VM con CPU più potenti, con interfacce di rete ad alta velocità effettiva opzionali (RDMA).</span><span class="sxs-lookup"><span data-stu-id="c70df-200">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="c70df-201">Trovare le dimensioni delle macchine virtuali disponibili</span><span class="sxs-lookup"><span data-stu-id="c70df-201">Find available VM sizes</span></span>

<span data-ttu-id="c70df-202">toosee un elenco di macchine Virtuali di dimensioni disponibili in una determinata area, usare hello [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) comando.</span><span class="sxs-lookup"><span data-stu-id="c70df-202">toosee a list of VM sizes available in a particular region, use hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command.</span></span>

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a><span data-ttu-id="c70df-203">Ridimensionare una VM</span><span class="sxs-lookup"><span data-stu-id="c70df-203">Resize a VM</span></span>

<span data-ttu-id="c70df-204">Dopo la distribuzione di una macchina virtuale, può essere ridimensionato tooincrease o ridurre l'allocazione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="c70df-204">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="c70df-205">Prima di ridimensionamento di una macchina virtuale, controllare se hello dimensione desiderata è disponibile in cluster della macchina virtuale corrente hello.</span><span class="sxs-lookup"><span data-stu-id="c70df-205">Before resizing a VM, check if hello desired size is available on hello current VM cluster.</span></span> <span data-ttu-id="c70df-206">Hello [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) comando restituisce un elenco di dimensioni.</span><span class="sxs-lookup"><span data-stu-id="c70df-206">hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command returns a list of sizes.</span></span> 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

<span data-ttu-id="c70df-207">Se lo si desidera hello dimensione è disponibile, hello VM può essere ridimensionata da uno stato acceso, ma che è stato riavviato durante l'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c70df-207">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

<span data-ttu-id="c70df-208">Se hello dimensioni desiderate non è in cluster corrente hello, hello VM esigenze toobe deallocato prima operazione di ridimensionamento hello può verificarsi.</span><span class="sxs-lookup"><span data-stu-id="c70df-208">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="c70df-209">Si noti che quando hello VM viene acceso nuovamente, vengono rimossi tutti i dati su disco temporaneo hello e indirizzo IP pubblico hello modificare a meno che non viene utilizzato un indirizzo IP statico.</span><span class="sxs-lookup"><span data-stu-id="c70df-209">Note, when hello VM is powered back on, any data on hello temp disk are removed, and hello public IP address change unless a static IP address is being used.</span></span> 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a><span data-ttu-id="c70df-210">Stati di alimentazione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c70df-210">VM power states</span></span>

<span data-ttu-id="c70df-211">Una macchina virtuale di Azure può avere uno dei diversi stati di alimentazione.</span><span class="sxs-lookup"><span data-stu-id="c70df-211">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="c70df-212">Questo stato rappresenta lo stato corrente di hello di hello VM dal punto di vista hello di hello hypervisor.</span><span class="sxs-lookup"><span data-stu-id="c70df-212">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="c70df-213">Stati di alimentazione</span><span class="sxs-lookup"><span data-stu-id="c70df-213">Power states</span></span>

| <span data-ttu-id="c70df-214">Stato di alimentazione</span><span class="sxs-lookup"><span data-stu-id="c70df-214">Power State</span></span> | <span data-ttu-id="c70df-215">Descrizione</span><span class="sxs-lookup"><span data-stu-id="c70df-215">Description</span></span>
|----|----|
| <span data-ttu-id="c70df-216">Avvio in corso</span><span class="sxs-lookup"><span data-stu-id="c70df-216">Starting</span></span> | <span data-ttu-id="c70df-217">Indica la macchina virtuale hello viene avviata.</span><span class="sxs-lookup"><span data-stu-id="c70df-217">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="c70df-218">In esecuzione</span><span class="sxs-lookup"><span data-stu-id="c70df-218">Running</span></span> | <span data-ttu-id="c70df-219">Indica che la macchina virtuale hello è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c70df-219">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="c70df-220">Arresto in corso</span><span class="sxs-lookup"><span data-stu-id="c70df-220">Stopping</span></span> | <span data-ttu-id="c70df-221">Indica che la macchina virtuale hello è stata arrestata.</span><span class="sxs-lookup"><span data-stu-id="c70df-221">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="c70df-222">Arrestato</span><span class="sxs-lookup"><span data-stu-id="c70df-222">Stopped</span></span> | <span data-ttu-id="c70df-223">Indica che la macchina virtuale hello è stata arrestata.</span><span class="sxs-lookup"><span data-stu-id="c70df-223">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="c70df-224">Si noti che le macchine virtuali in stato arrestato hello continuerà a essere addebitati.</span><span class="sxs-lookup"><span data-stu-id="c70df-224">Note that virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="c70df-225">Deallocazione</span><span class="sxs-lookup"><span data-stu-id="c70df-225">Deallocating</span></span> | <span data-ttu-id="c70df-226">Indica che la macchina virtuale hello è in corso deallocazione.</span><span class="sxs-lookup"><span data-stu-id="c70df-226">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="c70df-227">Deallocato</span><span class="sxs-lookup"><span data-stu-id="c70df-227">Deallocated</span></span> | <span data-ttu-id="c70df-228">Indica che la macchina virtuale hello è stata completamente rimossa dall'hypervisor hello ma è ancora disponibile nel piano di controllo hello.</span><span class="sxs-lookup"><span data-stu-id="c70df-228">Indicates that hello virtual machine is completely removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="c70df-229">Macchine virtuali in stato deallocato hello non essere addebitati.</span><span class="sxs-lookup"><span data-stu-id="c70df-229">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="c70df-230">Indica che lo stato di alimentazione hello della macchina virtuale hello è sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="c70df-230">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="c70df-231">Trovare lo stato di alimentazione</span><span class="sxs-lookup"><span data-stu-id="c70df-231">Find power state</span></span>

<span data-ttu-id="c70df-232">stato di hello tooretrieve di una determinata macchina virtuale, utilizzare hello [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) comando.</span><span class="sxs-lookup"><span data-stu-id="c70df-232">tooretrieve hello state of a particular VM, use hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span> <span data-ttu-id="c70df-233">Essere toospecify che un nome valido per una macchina virtuale e un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c70df-233">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

<span data-ttu-id="c70df-234">Output:</span><span class="sxs-lookup"><span data-stu-id="c70df-234">Output:</span></span>

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a><span data-ttu-id="c70df-235">Attività di gestione</span><span class="sxs-lookup"><span data-stu-id="c70df-235">Management tasks</span></span>

<span data-ttu-id="c70df-236">Durante il ciclo di vita hello di una macchina virtuale, è opportuno toorun attività di gestione, ad esempio avvio, arresto o l'eliminazione di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c70df-236">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="c70df-237">Inoltre, è consigliabile toocreate script tooautomate attività ripetitive o complesse.</span><span class="sxs-lookup"><span data-stu-id="c70df-237">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="c70df-238">Utilizzo di PowerShell di Azure, molte attività comuni di gestione può essere eseguita dalla riga di comando hello o negli script.</span><span class="sxs-lookup"><span data-stu-id="c70df-238">Using Azure PowerShell, many common management tasks can be run from hello command line or in scripts.</span></span>

### <a name="stop-virtual-machine"></a><span data-ttu-id="c70df-239">Arrestare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c70df-239">Stop virtual machine</span></span>

<span data-ttu-id="c70df-240">Arrestare e deallocare una macchina virtuale con [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="c70df-240">Stop and deallocate a virtual machine with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

<span data-ttu-id="c70df-241">Se si desidera una macchina virtuale di hello tookeep in uno stato di provisioning, utilizzare il parametro - StayProvisioned hello.</span><span class="sxs-lookup"><span data-stu-id="c70df-241">If you want tookeep hello virtual machine in a provisioned state, use hello -StayProvisioned parameter.</span></span>

### <a name="start-virtual-machine"></a><span data-ttu-id="c70df-242">Avviare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c70df-242">Start virtual machine</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="c70df-243">Eliminare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="c70df-243">Delete resource group</span></span>

<span data-ttu-id="c70df-244">Se si elimina un gruppo di risorse, vengono eliminate anche tutte le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="c70df-244">Deleting a resource group also deletes all resources contained within.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a><span data-ttu-id="c70df-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c70df-245">Next steps</span></span>

<span data-ttu-id="c70df-246">In questa esercitazione sono illustrate la creazione e la gestione di VM di base, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c70df-246">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c70df-247">Creare e connettersi tooa VM</span><span class="sxs-lookup"><span data-stu-id="c70df-247">Create and connect tooa VM</span></span>
> * <span data-ttu-id="c70df-248">Selezionare e usare le immagini di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c70df-248">Select and use VM images</span></span>
> * <span data-ttu-id="c70df-249">Visualizzare e usare macchine virtuali di dimensioni specifiche</span><span class="sxs-lookup"><span data-stu-id="c70df-249">View and use specific VM sizes</span></span>
> * <span data-ttu-id="c70df-250">Ridimensionare una VM</span><span class="sxs-lookup"><span data-stu-id="c70df-250">Resize a VM</span></span>
> * <span data-ttu-id="c70df-251">Visualizzare e comprendere lo stato di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="c70df-251">View and understand VM state</span></span>

<span data-ttu-id="c70df-252">Spostare toohello toolearn esercitazione successiva su dischi di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c70df-252">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="c70df-253">Creare e gestire dischi di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="c70df-253">Create and Manage VM disks</span></span>](./tutorial-manage-data-disk.md)
