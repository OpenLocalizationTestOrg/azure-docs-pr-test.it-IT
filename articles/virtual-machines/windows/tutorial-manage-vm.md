---
title: Creare e gestire macchine virtuali di Windows con il modulo Azure PowerShell | Microsoft Docs
description: 'Esercitazione: creare e gestire macchine virtuali di Windows con il modulo Azure PowerShell'
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
ms.openlocfilehash: ec1bb7834beb66dc28dd5b1db764bd358243292c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-windows-vms-with-the-azure-powershell-module"></a><span data-ttu-id="99f24-103">Creare e gestire macchine virtuali di Windows con il modulo Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="99f24-103">Create and Manage Windows VMs with the Azure PowerShell module</span></span>

<span data-ttu-id="99f24-104">Le macchine virtuali di Azure offrono un ambiente di elaborazione completamente configurabile e flessibile.</span><span class="sxs-lookup"><span data-stu-id="99f24-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="99f24-105">Questa esercitazione illustra gli elementi di base della distribuzione di una macchina virtuale di Azure, ad esempio la selezione delle dimensioni di una VM, la selezione dell'immagine di una VM e la distribuzione di una VM.</span><span class="sxs-lookup"><span data-stu-id="99f24-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="99f24-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="99f24-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="99f24-107">Creare e connettersi a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="99f24-107">Create and connect to a VM</span></span>
> * <span data-ttu-id="99f24-108">Selezionare e usare le immagini di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="99f24-108">Select and use VM images</span></span>
> * <span data-ttu-id="99f24-109">Visualizzare e usare macchine virtuali di dimensioni specifiche</span><span class="sxs-lookup"><span data-stu-id="99f24-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="99f24-110">Ridimensionare una VM</span><span class="sxs-lookup"><span data-stu-id="99f24-110">Resize a VM</span></span>
> * <span data-ttu-id="99f24-111">Visualizzare e comprendere lo stato di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="99f24-111">View and understand VM state</span></span>

<span data-ttu-id="99f24-112">Questa esercitazione richiede il modulo Azure PowerShell 3.6 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="99f24-112">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="99f24-113">Eseguire ` Get-Module -ListAvailable AzureRM` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="99f24-113">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="99f24-114">Se è necessario eseguire l'aggiornamento, vedere [Installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="99f24-114">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="99f24-115">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="99f24-115">Create resource group</span></span>

<span data-ttu-id="99f24-116">Creare un gruppo di risorse con comando [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="99f24-116">Create a resource group with the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> 

<span data-ttu-id="99f24-117">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="99f24-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="99f24-118">Il gruppo di risorse deve essere creato prima della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="99f24-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="99f24-119">In questo esempio viene creato un gruppo di risorse denominato *myResourceGroupVM* nell'area *EastUS*.</span><span class="sxs-lookup"><span data-stu-id="99f24-119">In this example, a resource group named *myResourceGroupVM* is created in the *EastUS* region.</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

<span data-ttu-id="99f24-120">Il gruppo di risorse viene specificato quando si crea o si modifica una VM, come viene illustrato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="99f24-120">The resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="99f24-121">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="99f24-121">Create virtual machine</span></span>

<span data-ttu-id="99f24-122">Una macchina virtuale deve essere connessa a una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="99f24-122">A virtual machine must be connected to a virtual network.</span></span> <span data-ttu-id="99f24-123">Per comunicare con la macchina virtuale viene usato un indirizzo IP pubblico tramite una scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="99f24-123">You communicate with the virtual machine using a public IP address through a network interface card.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="99f24-124">Creare una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="99f24-124">Create virtual network</span></span>

<span data-ttu-id="99f24-125">Creare una subnet con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="99f24-125">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="99f24-126">Creare una rete virtuale con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="99f24-126">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a><span data-ttu-id="99f24-127">Creare un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="99f24-127">Create public IP address</span></span>

<span data-ttu-id="99f24-128">Creare un indirizzo IP pubblico con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="99f24-128">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a><span data-ttu-id="99f24-129">Creare una scheda di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="99f24-129">Create network interface card</span></span>

<span data-ttu-id="99f24-130">Creare una scheda di interfaccia di rete con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="99f24-130">Create a network interface card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a><span data-ttu-id="99f24-131">Creare un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="99f24-131">Create network security group</span></span>

<span data-ttu-id="99f24-132">Un [gruppo di sicurezza di rete](../../virtual-network/virtual-networks-nsg.md) di Azure consente di controllare il traffico in ingresso e in uscita per una o più macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="99f24-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="99f24-133">Le regole di un gruppo di sicurezza di rete consentono o impediscono il traffico di rete su una porta specifica o un intervallo di porte.</span><span class="sxs-lookup"><span data-stu-id="99f24-133">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="99f24-134">Queste regole possono includere un prefisso dell'indirizzo di origine, in modo che solo il traffico proveniente da un'origine specificata possa comunicare con una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="99f24-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span> <span data-ttu-id="99f24-135">Per accedere al server Web IIS che si sta installando, è necessario aggiungere una regola in ingresso per il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="99f24-135">To access the IIS webserver that you are installing, you must add an inbound NSG rule.</span></span>

<span data-ttu-id="99f24-136">Per creare una regola in ingresso per il gruppo di sicurezza di rete, usare [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="99f24-136">To create an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="99f24-137">L'esempio seguente crea una regola per il gruppo di sicurezza di rete denominata *myNSGRule* che apre la porta *3389* per la macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="99f24-137">The following example creates an NSG rule named *myNSGRule* that opens port *3389* for the virtual machine:</span></span>

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

<span data-ttu-id="99f24-138">Creare un gruppo di sicurezza di rete usando *myNSGRule* con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="99f24-138">Create the NSG using *myNSGRule* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

<span data-ttu-id="99f24-139">Aggiungere il gruppo di sicurezza di rete alla subnet della rete virtuale con [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="99f24-139">Add the NSG to the subnet in the virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="99f24-140">Aggiornare la rete virtuale con [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="99f24-140">Update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a><span data-ttu-id="99f24-141">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="99f24-141">Create virtual machine</span></span>

<span data-ttu-id="99f24-142">Per la creazione di una macchina virtuale sono disponibili diverse opzioni, ad esempio l'immagine del sistema operativo, il ridimensionamento del disco e le credenziali amministrative.</span><span class="sxs-lookup"><span data-stu-id="99f24-142">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="99f24-143">In questo esempio viene creata una macchina virtuale con un nome *myVM* che esegue la versione più recente di Windows Server 2016 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="99f24-143">In this example, a virtual machine is created with a name of *myVM* running the latest version of Windows Server 2016 Datacenter.</span></span>

<span data-ttu-id="99f24-144">Impostare il nome utente e la password necessari per l'account amministratore della macchina virtuale con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="99f24-144">Set the username and password needed for the administrator account on the virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="99f24-145">Creare la configurazione iniziale per la macchina virtuale con [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span><span class="sxs-lookup"><span data-stu-id="99f24-145">Create the initial configuration for the virtual machine with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="99f24-146">Aggiungere le informazioni sul sistema operativo nella configurazione della macchina virtuale con [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span><span class="sxs-lookup"><span data-stu-id="99f24-146">Add the operating system information to the virtual machine configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span></span>

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="99f24-147">Aggiungere le informazioni sull'immagine alla configurazione della macchina virtuale con [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span><span class="sxs-lookup"><span data-stu-id="99f24-147">Add the image information to the virtual machine configuration with [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

<span data-ttu-id="99f24-148">Aggiungere le impostazioni del disco del sistema operativo alla configurazione della macchina virtuale con [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span><span class="sxs-lookup"><span data-stu-id="99f24-148">Add the operating system disk settings to the virtual machine configuration with [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

<span data-ttu-id="99f24-149">Aggiungere la scheda di interfaccia di rete creata precedentemente alla configurazione della macchina virtuale con [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="99f24-149">Add the network interface card that you previously created to the virtual machine configuration with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="99f24-150">Creare la macchina virtuale con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="99f24-150">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-to-vm"></a><span data-ttu-id="99f24-151">Connettersi alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="99f24-151">Connect to VM</span></span>

<span data-ttu-id="99f24-152">Dopo aver completato la distribuzione, creare una connessione desktop remoto con la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="99f24-152">After the deployment has completed, create a remote desktop connection with the virtual machine.</span></span>

<span data-ttu-id="99f24-153">Eseguire i comandi seguenti per restituire l'indirizzo IP pubblico della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="99f24-153">Run the following commands to return the public IP address of the virtual machine.</span></span> <span data-ttu-id="99f24-154">Annotare questo indirizzo IP, in modo da potersi connettere ad esso con il browser per testare la connettività Web in un passaggio futuro.</span><span class="sxs-lookup"><span data-stu-id="99f24-154">Take note of this IP Address so you can connect to it with your browser to test web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

<span data-ttu-id="99f24-155">Usare il comando seguente per creare una sessione desktop remoto con la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="99f24-155">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="99f24-156">Sostituire l'indirizzo IP con l'indirizzo *publicIPAddress* della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="99f24-156">Replace the IP address with the *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="99f24-157">Quando richiesto, immettere le credenziali utilizzate durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="99f24-157">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a><span data-ttu-id="99f24-158">Informazioni sulle immagini delle VM</span><span class="sxs-lookup"><span data-stu-id="99f24-158">Understand VM images</span></span>

<span data-ttu-id="99f24-159">Azure Marketplace include diverse immagini di macchine virtuali che possono essere usate per creare nuove VM.</span><span class="sxs-lookup"><span data-stu-id="99f24-159">The Azure marketplace includes many virtual machine images that can be used to create a new virtual machine.</span></span> <span data-ttu-id="99f24-160">Nei passaggi precedenti è stata creata una macchina virtuale usando un'immagine Windows Server 2016-Datacenter.</span><span class="sxs-lookup"><span data-stu-id="99f24-160">In the previous steps, a virtual machine was created using the Windows Server 2016-Datacenter image.</span></span> <span data-ttu-id="99f24-161">In questo passaggio, viene usato il modulo PowerShell per cercare nel marketplace altre immagini di Windows da usare anche come base per le nuove macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="99f24-161">In this step, the PowerShell module is used to search the marketplace for other Windows images, which can also as a base for new VMs.</span></span> <span data-ttu-id="99f24-162">Questo processo consiste nell'individuazione del server di pubblicazione, dell'offerta e del nome dell'immagine (Sku).</span><span class="sxs-lookup"><span data-stu-id="99f24-162">This process consists of finding the publisher, offer, and the image name (Sku).</span></span> 

<span data-ttu-id="99f24-163">Usare il comando [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) per restituire un elenco di server di pubblicazione di immagini.</span><span class="sxs-lookup"><span data-stu-id="99f24-163">Use the [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command to return a list of image publishers.</span></span>  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

<span data-ttu-id="99f24-164">Usare [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) per restituire un elenco di offerte delle immagini.</span><span class="sxs-lookup"><span data-stu-id="99f24-164">Use the [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) to return a list of image offers.</span></span> <span data-ttu-id="99f24-165">Con questo comando, l'elenco restituito viene filtrato nel server di pubblicazione specificato.</span><span class="sxs-lookup"><span data-stu-id="99f24-165">With this command, the returned list is filtered on the specified publisher.</span></span> 

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

<span data-ttu-id="99f24-166">Il comando [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) verrà quindi filtrato in base al nome del server di pubblicazione e dell'offerta per restituire un elenco di nomi di immagini.</span><span class="sxs-lookup"><span data-stu-id="99f24-166">The [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) command will then filter on the publisher and offer name to return a list of image names.</span></span>

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

<span data-ttu-id="99f24-167">È possibile usare queste informazioni per distribuire una macchina virtuale con un'immagine specifica.</span><span class="sxs-lookup"><span data-stu-id="99f24-167">This information can be used to deploy a VM with a specific image.</span></span> <span data-ttu-id="99f24-168">In questo esempio viene impostato il nome dell'immagine per l'oggetto della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="99f24-168">This example sets the image name on the VM object.</span></span> <span data-ttu-id="99f24-169">Fare riferimento agli esempi precedenti in questa esercitazione per la procedura di distribuzione completa.</span><span class="sxs-lookup"><span data-stu-id="99f24-169">Refer to the previous examples in this tutorial for complete deployment steps.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="99f24-170">Informazioni sulle dimensioni delle VM</span><span class="sxs-lookup"><span data-stu-id="99f24-170">Understand VM sizes</span></span>

<span data-ttu-id="99f24-171">La dimensioni di una macchina virtuale determinano la quantità di risorse di calcolo, ad esempio CPU, GPU e memoria, disponibili per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="99f24-171">A virtual machine size determines the amount of compute resources such as CPU, GPU, and memory that are made available to the virtual machine.</span></span> <span data-ttu-id="99f24-172">Le macchine virtuali devono essere create con dimensioni adeguate al carico di lavoro previsto.</span><span class="sxs-lookup"><span data-stu-id="99f24-172">Virtual machines need to be created with a size appropriate for the expect work load.</span></span> <span data-ttu-id="99f24-173">Se aumenta il carico di lavoro, è possibile ridimensionare una macchina virtuale esistente.</span><span class="sxs-lookup"><span data-stu-id="99f24-173">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="99f24-174">Dimensioni delle VM</span><span class="sxs-lookup"><span data-stu-id="99f24-174">VM Sizes</span></span>

<span data-ttu-id="99f24-175">La tabella seguente classifica le dimensioni a seconda dei casi d'uso.</span><span class="sxs-lookup"><span data-stu-id="99f24-175">The following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="99f24-176">Tipo</span><span class="sxs-lookup"><span data-stu-id="99f24-176">Type</span></span>                     | <span data-ttu-id="99f24-177">Dimensioni</span><span class="sxs-lookup"><span data-stu-id="99f24-177">Sizes</span></span>           |    <span data-ttu-id="99f24-178">Descrizione</span><span class="sxs-lookup"><span data-stu-id="99f24-178">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="99f24-179">Scopo generico</span><span class="sxs-lookup"><span data-stu-id="99f24-179">General purpose</span></span>         |<span data-ttu-id="99f24-180">DSv2, Dv2, DS, D, Av2, A0-7</span><span class="sxs-lookup"><span data-stu-id="99f24-180">DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="99f24-181">Rapporto equilibrato tra CPU e memoria.</span><span class="sxs-lookup"><span data-stu-id="99f24-181">Balanced CPU-to-memory.</span></span> <span data-ttu-id="99f24-182">Soluzione ideale per sviluppo o test e soluzioni di dati e applicazioni medio-piccole.</span><span class="sxs-lookup"><span data-stu-id="99f24-182">Ideal for dev / test and small to medium applications and data solutions.</span></span>  |
| <span data-ttu-id="99f24-183">Ottimizzate per il calcolo</span><span class="sxs-lookup"><span data-stu-id="99f24-183">Compute optimized</span></span>      | <span data-ttu-id="99f24-184">Fs, F</span><span class="sxs-lookup"><span data-stu-id="99f24-184">Fs, F</span></span>             | <span data-ttu-id="99f24-185">Rapporto elevato tra CPU e memoria.</span><span class="sxs-lookup"><span data-stu-id="99f24-185">High CPU-to-memory.</span></span> <span data-ttu-id="99f24-186">Soluzione idonea per applicazioni con livelli medi di traffico, dispositivi di rete e processi batch.</span><span class="sxs-lookup"><span data-stu-id="99f24-186">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| <span data-ttu-id="99f24-187">Ottimizzate per la memoria</span><span class="sxs-lookup"><span data-stu-id="99f24-187">Memory optimized</span></span>       | <span data-ttu-id="99f24-188">GS, G, DSv2, DS, Dv2, D</span><span class="sxs-lookup"><span data-stu-id="99f24-188">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="99f24-189">Rapporto elevato tra memoria e core.</span><span class="sxs-lookup"><span data-stu-id="99f24-189">High memory-to-core.</span></span> <span data-ttu-id="99f24-190">Soluzione ideale per database relazionali, cache medio-grandi e analisi in memoria.</span><span class="sxs-lookup"><span data-stu-id="99f24-190">Great for relational databases, medium to large caches, and in-memory analytics.</span></span>                 |
| <span data-ttu-id="99f24-191">Ottimizzate per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="99f24-191">Storage optimized</span></span>       | <span data-ttu-id="99f24-192">Ls</span><span class="sxs-lookup"><span data-stu-id="99f24-192">Ls</span></span>                | <span data-ttu-id="99f24-193">I/O e velocità effettiva del disco elevati.</span><span class="sxs-lookup"><span data-stu-id="99f24-193">High disk throughput and IO.</span></span> <span data-ttu-id="99f24-194">Ideale per Big Data, database SQL e NoSQL.</span><span class="sxs-lookup"><span data-stu-id="99f24-194">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| <span data-ttu-id="99f24-195">GPU</span><span class="sxs-lookup"><span data-stu-id="99f24-195">GPU</span></span>           | <span data-ttu-id="99f24-196">NV, NC</span><span class="sxs-lookup"><span data-stu-id="99f24-196">NV, NC</span></span>            | <span data-ttu-id="99f24-197">VM specializzate ottimizzate per livelli intensivi di rendering della grafica ed editing di video.</span><span class="sxs-lookup"><span data-stu-id="99f24-197">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| <span data-ttu-id="99f24-198">Prestazioni elevate</span><span class="sxs-lookup"><span data-stu-id="99f24-198">High performance</span></span> | <span data-ttu-id="99f24-199">H, A8-11</span><span class="sxs-lookup"><span data-stu-id="99f24-199">H, A8-11</span></span>          | <span data-ttu-id="99f24-200">Le VM con CPU più potenti, con interfacce di rete ad alta velocità effettiva opzionali (RDMA).</span><span class="sxs-lookup"><span data-stu-id="99f24-200">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="99f24-201">Trovare le dimensioni delle macchine virtuali disponibili</span><span class="sxs-lookup"><span data-stu-id="99f24-201">Find available VM sizes</span></span>

<span data-ttu-id="99f24-202">Per visualizzare un elenco delle dimensioni delle VM disponibili in una determinata area, usare il comando [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize).</span><span class="sxs-lookup"><span data-stu-id="99f24-202">To see a list of VM sizes available in a particular region, use the [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command.</span></span>

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a><span data-ttu-id="99f24-203">Ridimensionare una VM</span><span class="sxs-lookup"><span data-stu-id="99f24-203">Resize a VM</span></span>

<span data-ttu-id="99f24-204">Dopo la distribuzione di una VM, è possibile ridimensionarla per aumentare o ridurre l'allocazione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="99f24-204">After a VM has been deployed, it can be resized to increase or decrease resource allocation.</span></span>

<span data-ttu-id="99f24-205">Prima di ridimensionare una macchina virtuale, verificare che le dimensioni desiderate siano disponibili nel cluster della VM corrente.</span><span class="sxs-lookup"><span data-stu-id="99f24-205">Before resizing a VM, check if the desired size is available on the current VM cluster.</span></span> <span data-ttu-id="99f24-206">Il comando [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) restituisce un elenco di dimensioni.</span><span class="sxs-lookup"><span data-stu-id="99f24-206">The [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command returns a list of sizes.</span></span> 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

<span data-ttu-id="99f24-207">Se le dimensioni desiderate sono disponibili, la VM può essere ridimensionata mentre è accesa, ma durante l'operazione viene riavviata.</span><span class="sxs-lookup"><span data-stu-id="99f24-207">If the desired size is available, the VM can be resized from a powered-on state, however it is rebooted during the operation.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

<span data-ttu-id="99f24-208">Se nel cluster corrente non sono disponibili le dimensioni desiderate, è necessario deallocare la VM prima di poter eseguire l'operazione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="99f24-208">If the desired size is not on the current cluster, the VM needs to be deallocated before the resize operation can occur.</span></span> <span data-ttu-id="99f24-209">Si noti che, quando la macchina virtuale viene riaccesa, vengono rimossi tutti i dati sul disco temporaneo, mentre l'indirizzo IP pubblico cambia a meno che non venga usato un indirizzo IP statico.</span><span class="sxs-lookup"><span data-stu-id="99f24-209">Note, when the VM is powered back on, any data on the temp disk are removed, and the public IP address change unless a static IP address is being used.</span></span> 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a><span data-ttu-id="99f24-210">Stati di alimentazione di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="99f24-210">VM power states</span></span>

<span data-ttu-id="99f24-211">Una macchina virtuale di Azure può avere uno dei diversi stati di alimentazione.</span><span class="sxs-lookup"><span data-stu-id="99f24-211">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="99f24-212">Questo stato rappresenta lo stato corrente della VM dal punto di vista dell'hypervisor.</span><span class="sxs-lookup"><span data-stu-id="99f24-212">This state represents the current state of the VM from the standpoint of the hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="99f24-213">Stati di alimentazione</span><span class="sxs-lookup"><span data-stu-id="99f24-213">Power states</span></span>

| <span data-ttu-id="99f24-214">Stato di alimentazione</span><span class="sxs-lookup"><span data-stu-id="99f24-214">Power State</span></span> | <span data-ttu-id="99f24-215">Descrizione</span><span class="sxs-lookup"><span data-stu-id="99f24-215">Description</span></span>
|----|----|
| <span data-ttu-id="99f24-216">Avvio in corso</span><span class="sxs-lookup"><span data-stu-id="99f24-216">Starting</span></span> | <span data-ttu-id="99f24-217">Indica che è in corso l'avvio della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="99f24-217">Indicates the virtual machine is being started.</span></span> |
| <span data-ttu-id="99f24-218">In esecuzione</span><span class="sxs-lookup"><span data-stu-id="99f24-218">Running</span></span> | <span data-ttu-id="99f24-219">Indica che la macchina virtuale è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="99f24-219">Indicates that the virtual machine is running.</span></span> |
| <span data-ttu-id="99f24-220">Arresto in corso</span><span class="sxs-lookup"><span data-stu-id="99f24-220">Stopping</span></span> | <span data-ttu-id="99f24-221">Indica che è in corso l'arresto della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="99f24-221">Indicates that the virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="99f24-222">Arrestato</span><span class="sxs-lookup"><span data-stu-id="99f24-222">Stopped</span></span> | <span data-ttu-id="99f24-223">Indica che la macchina virtuale è stata arrestata.</span><span class="sxs-lookup"><span data-stu-id="99f24-223">Indicates that the virtual machine is stopped.</span></span> <span data-ttu-id="99f24-224">Si noti che alle macchine virtuali con stato arrestato continuano a essere addebitati i costi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="99f24-224">Note that virtual machines in the stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="99f24-225">Deallocazione</span><span class="sxs-lookup"><span data-stu-id="99f24-225">Deallocating</span></span> | <span data-ttu-id="99f24-226">Indica che è in corso la deallocazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="99f24-226">Indicates that the virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="99f24-227">Deallocato</span><span class="sxs-lookup"><span data-stu-id="99f24-227">Deallocated</span></span> | <span data-ttu-id="99f24-228">Indica che la macchina virtuale è stata rimossa completamente dall'hypervisor, ma è ancora disponibile nel piano di controllo.</span><span class="sxs-lookup"><span data-stu-id="99f24-228">Indicates that the virtual machine is completely removed from the hypervisor but still available in the control plane.</span></span> <span data-ttu-id="99f24-229">Alle macchine virtuali con stato deallocato non vengono addebitati i costi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="99f24-229">Virtual machines in the Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="99f24-230">Indica che lo stato di alimentazione della macchina virtuale è sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="99f24-230">Indicates that the power state of the virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="99f24-231">Trovare lo stato di alimentazione</span><span class="sxs-lookup"><span data-stu-id="99f24-231">Find power state</span></span>

<span data-ttu-id="99f24-232">Per recuperare lo stato di una determinata VM, usare il comando [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="99f24-232">To retrieve the state of a particular VM, use the [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span> <span data-ttu-id="99f24-233">Assicurarsi di specificare un nome valido per una macchina virtuale e un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="99f24-233">Be sure to specify a valid name for a virtual machine and resource group.</span></span> 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

<span data-ttu-id="99f24-234">Output:</span><span class="sxs-lookup"><span data-stu-id="99f24-234">Output:</span></span>

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a><span data-ttu-id="99f24-235">Attività di gestione</span><span class="sxs-lookup"><span data-stu-id="99f24-235">Management tasks</span></span>

<span data-ttu-id="99f24-236">Durante il ciclo di vita di una macchina virtuale si eseguono attività di gestione come l'avvio, l'arresto o l'eliminazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="99f24-236">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="99f24-237">È consigliabile creare script per automatizzare le attività ripetitive o complesse.</span><span class="sxs-lookup"><span data-stu-id="99f24-237">Additionally, you may want to create scripts to automate repetitive or complex tasks.</span></span> <span data-ttu-id="99f24-238">Tramite Azure PowerShell è possibile eseguire molte attività di gestione comuni dalla riga di comando o con script.</span><span class="sxs-lookup"><span data-stu-id="99f24-238">Using Azure PowerShell, many common management tasks can be run from the command line or in scripts.</span></span>

### <a name="stop-virtual-machine"></a><span data-ttu-id="99f24-239">Arrestare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="99f24-239">Stop virtual machine</span></span>

<span data-ttu-id="99f24-240">Arrestare e deallocare una macchina virtuale con [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="99f24-240">Stop and deallocate a virtual machine with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

<span data-ttu-id="99f24-241">Se si vuole mantenere la macchina virtuale in uno stato di provisioning, usare il parametro -StayProvisioned.</span><span class="sxs-lookup"><span data-stu-id="99f24-241">If you want to keep the virtual machine in a provisioned state, use the -StayProvisioned parameter.</span></span>

### <a name="start-virtual-machine"></a><span data-ttu-id="99f24-242">Avviare la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="99f24-242">Start virtual machine</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="99f24-243">Eliminare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="99f24-243">Delete resource group</span></span>

<span data-ttu-id="99f24-244">Se si elimina un gruppo di risorse, vengono eliminate anche tutte le risorse in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="99f24-244">Deleting a resource group also deletes all resources contained within.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a><span data-ttu-id="99f24-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="99f24-245">Next steps</span></span>

<span data-ttu-id="99f24-246">In questa esercitazione sono illustrate la creazione e la gestione di VM di base, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="99f24-246">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="99f24-247">Creare e connettersi a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="99f24-247">Create and connect to a VM</span></span>
> * <span data-ttu-id="99f24-248">Selezionare e usare le immagini di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="99f24-248">Select and use VM images</span></span>
> * <span data-ttu-id="99f24-249">Visualizzare e usare macchine virtuali di dimensioni specifiche</span><span class="sxs-lookup"><span data-stu-id="99f24-249">View and use specific VM sizes</span></span>
> * <span data-ttu-id="99f24-250">Ridimensionare una VM</span><span class="sxs-lookup"><span data-stu-id="99f24-250">Resize a VM</span></span>
> * <span data-ttu-id="99f24-251">Visualizzare e comprendere lo stato di una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="99f24-251">View and understand VM state</span></span>

<span data-ttu-id="99f24-252">Passare all'esercitazione successiva per informazioni sui dischi di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="99f24-252">Advance to the next tutorial to learn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="99f24-253">Creare e gestire dischi di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="99f24-253">Create and Manage VM disks</span></span>](./tutorial-manage-data-disk.md)
