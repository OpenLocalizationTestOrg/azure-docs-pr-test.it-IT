---
title: aaaAzure reti virtuali e macchine virtuali di Windows | Documenti Microsoft
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
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="1fd32-103">Gestire reti virtuali di Azure e macchine virtuali Windows con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1fd32-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="1fd32-104">Le macchine virtuali di Azure usano la rete di Azure per la comunicazione di rete interna ed esterna.</span><span class="sxs-lookup"><span data-stu-id="1fd32-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="1fd32-105">In questa esercitazione vengono create più macchine virtuali (VM) in una rete virtuale e viene configurata la connettività di rete tra di esse.</span><span class="sxs-lookup"><span data-stu-id="1fd32-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="1fd32-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="1fd32-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1fd32-107">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="1fd32-107">Create a virtual network</span></span>
> * <span data-ttu-id="1fd32-108">Creare subnet di reti virtuali</span><span class="sxs-lookup"><span data-stu-id="1fd32-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="1fd32-109">Controllare il traffico di rete con gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="1fd32-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="1fd32-110">Visualizzare le regole del traffico applicate</span><span class="sxs-lookup"><span data-stu-id="1fd32-110">View traffic rules in action</span></span>

<span data-ttu-id="1fd32-111">Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo.</span><span class="sxs-lookup"><span data-stu-id="1fd32-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="1fd32-112">Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="1fd32-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="1fd32-113">Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="1fd32-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="1fd32-114">Creare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="1fd32-114">Create VNet</span></span>

<span data-ttu-id="1fd32-115">Una rete virtuale è una rappresentazione della rete nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="1fd32-115">A VNet is a representation of your own network in hello cloud.</span></span> <span data-ttu-id="1fd32-116">Una rete virtuale è un isolamento logico di hello sottoscrizione tooyour cloud di Azure dedicato.</span><span class="sxs-lookup"><span data-stu-id="1fd32-116">A VNet is a logical isolation of hello Azure cloud dedicated tooyour subscription.</span></span> <span data-ttu-id="1fd32-117">All'interno di una rete virtuale, si trova subnet, le regole per la connettività toothose subnet e connessioni da subnet toohello di hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="1fd32-117">Within a VNet, you find subnets, rules for connectivity toothose subnets, and connections from hello VMs toohello subnets.</span></span>

<span data-ttu-id="1fd32-118">Prima di poter creare altre risorse di Azure, è necessario toocreate un gruppo di risorse con [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="1fd32-118">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="1fd32-119">esempio Hello crea un gruppo di risorse denominato *myRGNetwork* in hello *EastUS* percorso:</span><span class="sxs-lookup"><span data-stu-id="1fd32-119">hello following example creates a resource group named *myRGNetwork* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="1fd32-120">Una subnet è una risorsa figlio di una rete virtuale e consente di definire i segmenti degli spazi di indirizzi all'interno di un blocco CIDR, usando i prefissi degli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="1fd32-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="1fd32-121">Schede di rete possono essere aggiunte toosubnets e tooVMs connesso, fornisce la connettività per diversi carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="1fd32-121">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="1fd32-122">Creare una subnet con [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="1fd32-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="1fd32-123">Creare una rete virtuale denominata *myVNet* che usa *myFrontendSubnet* con [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="1fd32-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="1fd32-124">Creare la VM front-end</span><span class="sxs-lookup"><span data-stu-id="1fd32-124">Create front-end VM</span></span>

<span data-ttu-id="1fd32-125">Per una macchina virtuale toocommunicate in una rete virtuale, è necessaria un'interfaccia di rete virtuale (NIC).</span><span class="sxs-lookup"><span data-stu-id="1fd32-125">For a VM toocommunicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="1fd32-126">Hello *myFrontendVM* è accessibile da hello internet, pertanto è necessario disporre anche di un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="1fd32-126">hello *myFrontendVM* is accessed from hello internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="1fd32-127">Creare un indirizzo IP pubblico con [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="1fd32-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="1fd32-128">Creare un'interfaccia di rete con [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="1fd32-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="1fd32-129">Impostare username hello e una password per account di amministratore hello su hello VM con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="1fd32-129">Set hello username and password needed for hello administrator account on hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="1fd32-130">Creare le macchine virtuali hello con [New AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [AzureRmVMNetworkInterface aggiungere](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), e [nuova AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="1fd32-130">Create hello VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

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

## <a name="install-web-server"></a><span data-ttu-id="1fd32-131">Installare il server Web</span><span class="sxs-lookup"><span data-stu-id="1fd32-131">Install web server</span></span>

<span data-ttu-id="1fd32-132">È possibile installare IIS in *myFrontendVM* usando una sessione Desktop remoto.</span><span class="sxs-lookup"><span data-stu-id="1fd32-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="1fd32-133">È necessario tooget hello indirizzo IP pubblico del hello tooaccess VM è.</span><span class="sxs-lookup"><span data-stu-id="1fd32-133">You need tooget hello public IP address of hello VM tooaccess it.</span></span>

<span data-ttu-id="1fd32-134">È possibile ottenere l'indirizzo IP pubblico hello del *myFrontendVM* con [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="1fd32-134">You can get hello public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="1fd32-135">esempio Hello Ottiene hello di indirizzo IP per *myPublicIPAddress* creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="1fd32-135">hello following example obtains hello IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="1fd32-136">Prendere nota di questo indirizzo IP per poterlo usare nei passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="1fd32-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="1fd32-137">Comando che segue di hello utilizzare toocreate una sessione desktop remota con *myFrontendVM*.</span><span class="sxs-lookup"><span data-stu-id="1fd32-137">Use hello following command toocreate a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="1fd32-138">Sostituire  *<publicIPAddress>*  con indirizzo hello annotato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1fd32-138">Replace *<publicIPAddress>* with hello address that you previously recorded.</span></span> <span data-ttu-id="1fd32-139">Quando richiesto, immettere le credenziali di hello utilizzate durante la creazione di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1fd32-139">When prompted, enter hello credentials used when you created hello VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="1fd32-140">Ora che sono registrati nel troppo*myFrontendVM*, è possibile utilizzare una singola riga di PowerShell tooinstall IIS e abilitare il traffico web tooallow di hello firewall locale regola.</span><span class="sxs-lookup"><span data-stu-id="1fd32-140">Now that you have logged in too*myFrontendVM*, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="1fd32-141">Aprire un prompt dei comandi di PowerShell ed eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1fd32-141">Open a PowerShell prompt and run hello following command:</span></span>

<span data-ttu-id="1fd32-142">Utilizzare [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello un'estensione personalizzata per l'installazione di server Web IIS hello:</span><span class="sxs-lookup"><span data-stu-id="1fd32-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello custom script extension that installs hello IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="1fd32-143">Ora è possibile utilizzare hello pubblica IP indirizzo toobrowse toohello VM toosee hello sito IIS.</span><span class="sxs-lookup"><span data-stu-id="1fd32-143">Now you can use hello public IP address toobrowse toohello VM toosee hello IIS site.</span></span>

![Sito IIS predefinito](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="1fd32-145">Gestire il traffico interno</span><span class="sxs-lookup"><span data-stu-id="1fd32-145">Manage internal traffic</span></span>

<span data-ttu-id="1fd32-146">Un rete gruppo di sicurezza () contiene un elenco di regole di sicurezza che consentono o negano tooa tooresources connessi di rete del traffico tra reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="1fd32-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooa VNet.</span></span> <span data-ttu-id="1fd32-147">NSGs può essere associato toosubnets o singole schede di rete associata tooVMs.</span><span class="sxs-lookup"><span data-stu-id="1fd32-147">NSGs can be associated toosubnets or individual NICs attached tooVMs.</span></span> <span data-ttu-id="1fd32-148">Viene eseguita l'apertura o chiusura di accesso tooVMs tramite porte utilizzando regole di gruppo.</span><span class="sxs-lookup"><span data-stu-id="1fd32-148">Opening or closing access tooVMs through ports is done using NSG rules.</span></span> <span data-ttu-id="1fd32-149">Alla creazione di *myFrontendVM*, la porta in ingresso 3389 è stata aperta automaticamente per la connettività RDP.</span><span class="sxs-lookup"><span data-stu-id="1fd32-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="1fd32-150">La comunicazione interna delle VM può essere configurata usando un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="1fd32-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="1fd32-151">In questa sezione viene illustrato come una subnet aggiuntiva in hello toocreate di rete e assegnare un tooallow tooit NSG una connessione da *myFrontendVM* troppo*myBackendVM* sulla porta 1433.</span><span class="sxs-lookup"><span data-stu-id="1fd32-151">In this section, you learn how toocreate an additional subnet in hello network and assign an NSG tooit tooallow a connection from *myFrontendVM* too*myBackendVM* on port 1433.</span></span> <span data-ttu-id="1fd32-152">subnet Hello viene quindi assegnato toohello VM al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="1fd32-152">hello subnet is then assigned toohello VM when it is created.</span></span>

<span data-ttu-id="1fd32-153">È possibile limitare il traffico interno troppo*myBackendVM* solo da *myFrontendVM* mediante la creazione di un gruppo per la subnet di back-end hello.</span><span class="sxs-lookup"><span data-stu-id="1fd32-153">You can limit internal traffic too*myBackendVM* from only *myFrontendVM* by creating an NSG for hello back-end subnet.</span></span> <span data-ttu-id="1fd32-154">esempio Hello crea una regola di gruppo denominata *myBackendNSGRule* con [New AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span><span class="sxs-lookup"><span data-stu-id="1fd32-154">hello following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

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

<span data-ttu-id="1fd32-155">Aggiungere un gruppo di sicurezza di rete denominato *myBackendNSG* con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="1fd32-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="1fd32-156">Aggiungere la subnet back-end</span><span class="sxs-lookup"><span data-stu-id="1fd32-156">Add back-end subnet</span></span>

<span data-ttu-id="1fd32-157">Aggiungi *myBackEndSubnet* troppo*myVNet* con [Aggiungi AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="1fd32-157">Add *myBackEndSubnet* too*myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

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

## <a name="create-back-end-vm"></a><span data-ttu-id="1fd32-158">Creare la VM back-end</span><span class="sxs-lookup"><span data-stu-id="1fd32-158">Create back-end VM</span></span>

<span data-ttu-id="1fd32-159">hello toocreate modo più semplice di Hello VM back-end è tramite un'immagine di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1fd32-159">hello easiest way toocreate hello back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="1fd32-160">Solo in questa esercitazione crea hello VM al server di database hello, ma non fornisce informazioni sull'accesso a database hello.</span><span class="sxs-lookup"><span data-stu-id="1fd32-160">This tutorial only creates hello VM with hello database server, but doesn't provide information about accessing hello database.</span></span>

<span data-ttu-id="1fd32-161">Creare *myBackendNic*:</span><span class="sxs-lookup"><span data-stu-id="1fd32-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="1fd32-162">Impostare username hello e una password per account di amministratore hello nella macchina virtuale con Get-Credential hello:</span><span class="sxs-lookup"><span data-stu-id="1fd32-162">Set hello username and password needed for hello administrator account on hello VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="1fd32-163">Creare *myBackendVM*:</span><span class="sxs-lookup"><span data-stu-id="1fd32-163">Create *myBackendVM*:</span></span>

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

<span data-ttu-id="1fd32-164">immagine di Hello utilizzata è installato SQL Server, ma non viene utilizzato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="1fd32-164">hello image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="1fd32-165">È incluso tooshow è illustrato come configurare il traffico web toohandle una macchina virtuale e la gestione di database toohandle una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1fd32-165">It is included tooshow you how you can configure a VM toohandle web traffic and a VM toohandle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fd32-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1fd32-166">Next steps</span></span>

<span data-ttu-id="1fd32-167">In questa esercitazione è creato e protetto reti di Azure come macchine toovirtual correlati.</span><span class="sxs-lookup"><span data-stu-id="1fd32-167">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="1fd32-168">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="1fd32-168">Create a virtual network</span></span>
> * <span data-ttu-id="1fd32-169">Creare subnet di reti virtuali</span><span class="sxs-lookup"><span data-stu-id="1fd32-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="1fd32-170">Controllare il traffico di rete con gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="1fd32-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="1fd32-171">Visualizzare le regole del traffico applicate</span><span class="sxs-lookup"><span data-stu-id="1fd32-171">View traffic rules in action</span></span>

<span data-ttu-id="1fd32-172">Spostare toohello toolearn esercitazione successiva sul monitoraggio di protezione dati su macchine virtuali tramite backup di Azure.</span><span class="sxs-lookup"><span data-stu-id="1fd32-172">Advance toohello next tutorial toolearn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="1fd32-173">.</span><span class="sxs-lookup"><span data-stu-id="1fd32-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1fd32-174">Eseguire il backup di macchine virtuali Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="1fd32-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
