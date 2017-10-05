---
title: Reti virtuali di Azure e macchine virtuali Windows | Microsoft Docs
description: 'Esercitazione: gestire reti virtuali di Azure e macchine virtuali Windows con Azure PowerShell'
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: c71c07f8ecd123a7e27848ba5043d46e315fcf03
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="269c4-103">Gestire reti virtuali di Azure e macchine virtuali Windows con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="269c4-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="269c4-104">Le macchine virtuali di Azure usano la rete di Azure per la comunicazione di rete interna ed esterna.</span><span class="sxs-lookup"><span data-stu-id="269c4-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="269c4-105">In questa esercitazione vengono create più macchine virtuali (VM) in una rete virtuale e viene configurata la connettività di rete tra di esse.</span><span class="sxs-lookup"><span data-stu-id="269c4-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="269c4-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="269c4-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="269c4-107">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="269c4-107">Create a virtual network</span></span>
> * <span data-ttu-id="269c4-108">Creare subnet di reti virtuali</span><span class="sxs-lookup"><span data-stu-id="269c4-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="269c4-109">Controllare il traffico di rete con gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="269c4-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="269c4-110">Visualizzare le regole del traffico applicate</span><span class="sxs-lookup"><span data-stu-id="269c4-110">View traffic rules in action</span></span>

<span data-ttu-id="269c4-111">Questa esercitazione richiede il modulo Azure PowerShell 3.6 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="269c4-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="269c4-112">Eseguire ` Get-Module -ListAvailable AzureRM` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="269c4-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="269c4-113">Se è necessario eseguire l'aggiornamento, vedere [Installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="269c4-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="269c4-114">Creare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="269c4-114">Create VNet</span></span>

<span data-ttu-id="269c4-115">Una rete virtuale è una rappresentazione della propria rete nel cloud.</span><span class="sxs-lookup"><span data-stu-id="269c4-115">A VNet is a representation of your own network in the cloud.</span></span> <span data-ttu-id="269c4-116">È un isolamento logico del cloud di Azure dedicato alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="269c4-116">A VNet is a logical isolation of the Azure cloud dedicated to your subscription.</span></span> <span data-ttu-id="269c4-117">All'interno di una rete virtuale si trovano subnet, regole per la connettività a tali subnet e connessioni dalle VM alle subnet.</span><span class="sxs-lookup"><span data-stu-id="269c4-117">Within a VNet, you find subnets, rules for connectivity to those subnets, and connections from the VMs to the subnets.</span></span>

<span data-ttu-id="269c4-118">Per poter creare qualsiasi altra risorsa di Azure, è necessario prima creare un gruppo di risorse con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="269c4-118">Before you can create any other Azure resources, you need to create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="269c4-119">L'esempio seguente crea un gruppo di risorse denominato *myRGNetwork* nella posizione *EastUS*:</span><span class="sxs-lookup"><span data-stu-id="269c4-119">The following example creates a resource group named *myRGNetwork* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="269c4-120">Una subnet è una risorsa figlio di una rete virtuale e consente di definire i segmenti degli spazi di indirizzi all'interno di un blocco CIDR, usando i prefissi degli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="269c4-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="269c4-121">Le NIC possono essere aggiunte alle subnet e connesse alle macchine virtuali, fornendo connettività per diversi carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="269c4-121">NICs can be added to subnets, and connected to VMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="269c4-122">Creare una subnet con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="269c4-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="269c4-123">Creare una rete virtuale denominata *myVNet* che usa *myFrontendSubnet* con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="269c4-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="269c4-124">Creare la VM front-end</span><span class="sxs-lookup"><span data-stu-id="269c4-124">Create front-end VM</span></span>

<span data-ttu-id="269c4-125">Per comunicare in una rete virtuale, una VM deve avere un'interfaccia di rete (NIC) virtuale.</span><span class="sxs-lookup"><span data-stu-id="269c4-125">For a VM to communicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="269c4-126">*myFrontendVM* deve essere accessibile da Internet e deve quindi avere anche un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="269c4-126">The *myFrontendVM* is accessed from the internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="269c4-127">Creare un indirizzo IP pubblico con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="269c4-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="269c4-128">Creare un'interfaccia di rete con [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="269c4-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="269c4-129">Impostare il nome utente e la password necessari per l'account amministratore della VM con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="269c4-129">Set the username and password needed for the administrator account on the VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="269c4-130">Creare le VM con [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) e [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="269c4-130">Create the VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a><span data-ttu-id="269c4-131">Installare il server Web</span><span class="sxs-lookup"><span data-stu-id="269c4-131">Install web server</span></span>

<span data-ttu-id="269c4-132">È possibile installare IIS in *myFrontendVM* usando una sessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="269c4-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="269c4-133">Per accedere alla VM è necessario ottenerne l'indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="269c4-133">You need to get the public IP address of the VM to access it.</span></span>

<span data-ttu-id="269c4-134">È possibile ottenere l'indirizzo IP pubblico di *myFrontendVM* con [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="269c4-134">You can get the public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="269c4-135">L'esempio seguente ottiene l'indirizzo IP per *myPublicIPAddress* creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="269c4-135">The following example obtains the IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="269c4-136">Prendere nota di questo indirizzo IP per poterlo usare nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="269c4-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="269c4-137">Usare il comando seguente per creare una sessione Desktop remoto con *myFrontendVM*.</span><span class="sxs-lookup"><span data-stu-id="269c4-137">Use the following command to create a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="269c4-138">Sostituire *<publicIPAddress>* con l'indirizzo registrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="269c4-138">Replace *<publicIPAddress>* with the address that you previously recorded.</span></span> <span data-ttu-id="269c4-139">Quando richiesto, immettere le credenziali usate durante la creazione della VM.</span><span class="sxs-lookup"><span data-stu-id="269c4-139">When prompted, enter the credentials used when you created the VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="269c4-140">Dopo avere eseguito l'accesso a *myFrontendVM*, è possibile usare una singola riga di codice di PowerShell per installare IIS e abilitare la regola del firewall locale per consentire il traffico Web.</span><span class="sxs-lookup"><span data-stu-id="269c4-140">Now that you have logged in to *myFrontendVM*, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="269c4-141">Aprire un prompt di PowerShell ed eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="269c4-141">Open a PowerShell prompt and run the following command:</span></span>

<span data-ttu-id="269c4-142">Usare [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) per eseguire l'estensione di script personalizzata che installa il server Web IIS:</span><span class="sxs-lookup"><span data-stu-id="269c4-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) to run the custom script extension that installs the IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="269c4-143">È ora possibile usare l'indirizzo IP pubblico per passare alla VM e visualizzare il sito IIS.</span><span class="sxs-lookup"><span data-stu-id="269c4-143">Now you can use the public IP address to browse to the VM to see the IIS site.</span></span>

![Sito IIS predefinito](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="269c4-145">Gestire il traffico interno</span><span class="sxs-lookup"><span data-stu-id="269c4-145">Manage internal traffic</span></span>

<span data-ttu-id="269c4-146">Un gruppo di sicurezza di rete (NSG) contiene un elenco di regole di sicurezza che consentono o rifiutano il traffico di rete verso le risorse connesse a una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="269c4-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic to resources connected to a VNet.</span></span> <span data-ttu-id="269c4-147">I gruppi di sicurezza di rete possono essere associati a subnet o singole interfacce di rete collegate a VM.</span><span class="sxs-lookup"><span data-stu-id="269c4-147">NSGs can be associated to subnets or individual NICs attached to VMs.</span></span> <span data-ttu-id="269c4-148">Per aprire o chiudere l'accesso alle VM tramite le porte vengono usate le regole dei gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="269c4-148">Opening or closing access to VMs through ports is done using NSG rules.</span></span> <span data-ttu-id="269c4-149">Alla creazione di *myFrontendVM*, la porta in ingresso 3389 è stata aperta automaticamente per la connettività RDP.</span><span class="sxs-lookup"><span data-stu-id="269c4-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="269c4-150">La comunicazione interna delle VM può essere configurata usando un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="269c4-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="269c4-151">Questa sezione illustra come creare una subnet aggiuntiva nella rete e assegnare un gruppo di sicurezza di rete a tale subnet per consentire una connessione da *myFrontendVM* a *myBackendVM* sulla porta 1433.</span><span class="sxs-lookup"><span data-stu-id="269c4-151">In this section, you learn how to create an additional subnet in the network and assign an NSG to it to allow a connection from *myFrontendVM* to *myBackendVM* on port 1433.</span></span> <span data-ttu-id="269c4-152">La subnet viene quindi assegnata alla VM al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="269c4-152">The subnet is then assigned to the VM when it is created.</span></span>

<span data-ttu-id="269c4-153">È possibile limitare il traffico interno verso *myBackendVM* solo da *myFrontendVM* creando un gruppo di sicurezza di rete per la subnet back-end.</span><span class="sxs-lookup"><span data-stu-id="269c4-153">You can limit internal traffic to *myBackendVM* from only *myFrontendVM* by creating an NSG for the back-end subnet.</span></span> <span data-ttu-id="269c4-154">L'esempio seguente crea una regola del gruppo di sicurezza di rete denominata *myBackendNSGRule* con [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span><span class="sxs-lookup"><span data-stu-id="269c4-154">The following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

<span data-ttu-id="269c4-155">Aggiungere un gruppo di sicurezza di rete denominato *myBackendNSG* con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="269c4-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="269c4-156">Aggiungere la subnet back-end</span><span class="sxs-lookup"><span data-stu-id="269c4-156">Add back-end subnet</span></span>

<span data-ttu-id="269c4-157">Aggiungere *myBackEndSubnet* a *myVNet* con [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="269c4-157">Add *myBackEndSubnet* to *myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a><span data-ttu-id="269c4-158">Creare la VM back-end</span><span class="sxs-lookup"><span data-stu-id="269c4-158">Create back-end VM</span></span>

<span data-ttu-id="269c4-159">Il modo più semplice per creare la VM back-end consiste nell'usare un'immagine di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="269c4-159">The easiest way to create the back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="269c4-160">Questa esercitazione si limita a creare la VM con il server di database e non include informazioni sull'accesso al database.</span><span class="sxs-lookup"><span data-stu-id="269c4-160">This tutorial only creates the VM with the database server, but doesn't provide information about accessing the database.</span></span>

<span data-ttu-id="269c4-161">Creare *myBackendNic*:</span><span class="sxs-lookup"><span data-stu-id="269c4-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="269c4-162">Impostare il nome utente e la password necessari per l'account amministratore della VM con Get-Credential:</span><span class="sxs-lookup"><span data-stu-id="269c4-162">Set the username and password needed for the administrator account on the VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="269c4-163">Creare *myBackendVM*:</span><span class="sxs-lookup"><span data-stu-id="269c4-163">Create *myBackendVM*:</span></span>

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

<span data-ttu-id="269c4-164">L'immagine, in cui è installato SQL Server, non viene usata in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="269c4-164">The image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="269c4-165">È inclusa per illustrare come è possibile configurare una VM per il traffico Web e una VM per la gestione di database.</span><span class="sxs-lookup"><span data-stu-id="269c4-165">It is included to show you how you can configure a VM to handle web traffic and a VM to handle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="269c4-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="269c4-166">Next steps</span></span>

<span data-ttu-id="269c4-167">In questa esercitazione sono state create e protette reti di Azure in relazione a macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="269c4-167">In this tutorial, you created and secured Azure networks as related to virtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="269c4-168">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="269c4-168">Create a virtual network</span></span>
> * <span data-ttu-id="269c4-169">Creare subnet di reti virtuali</span><span class="sxs-lookup"><span data-stu-id="269c4-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="269c4-170">Controllare il traffico di rete con gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="269c4-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="269c4-171">Visualizzare le regole del traffico applicate</span><span class="sxs-lookup"><span data-stu-id="269c4-171">View traffic rules in action</span></span>

<span data-ttu-id="269c4-172">Passare all'esercitazione successiva per informazioni sul monitoraggio della protezione dei dati nelle macchine virtuali con Backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="269c4-172">Advance to the next tutorial to learn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="269c4-173">.</span><span class="sxs-lookup"><span data-stu-id="269c4-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="269c4-174">Eseguire il backup di macchine virtuali Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="269c4-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
