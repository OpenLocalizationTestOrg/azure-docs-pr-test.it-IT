---
title: una macchina virtuale Windows in Azure aaaCustomize | Documenti Microsoft
description: Informazioni su come toouse hello estensione script personalizzata e l'insieme di credenziali chiave toocustomize macchine virtuali di Windows in Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c03b2bb6d70875134c63ea2fe4c2e2c1777c2188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="f3e20-103">Come toocustomize una macchina virtuale Windows Azure</span><span class="sxs-lookup"><span data-stu-id="f3e20-103">How toocustomize a Windows virtual machine in Azure</span></span>
<span data-ttu-id="f3e20-104">in genere desiderata tooconfigure virtuali (VM) in modo rapido e coerenza, qualche forma di automazione.</span><span class="sxs-lookup"><span data-stu-id="f3e20-104">tooconfigure virtual machines (VMs) in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="f3e20-105">Un comune toocustomize approccio una macchina virtuale di Windows è toouse [Custom Script di estensione per Windows](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="f3e20-105">A common approach toocustomize a Windows VM is toouse [Custom Script Extension for Windows](extensions-customscript.md).</span></span> <span data-ttu-id="f3e20-106">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="f3e20-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f3e20-107">Utilizzare tooinstall estensione Script personalizzata hello IIS</span><span class="sxs-lookup"><span data-stu-id="f3e20-107">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="f3e20-108">Creare una macchina virtuale che utilizza l'estensione dello Script personalizzata hello</span><span class="sxs-lookup"><span data-stu-id="f3e20-108">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="f3e20-109">Consente di visualizzare un sito IIS in esecuzione dopo l'applicazione di estensione hello</span><span class="sxs-lookup"><span data-stu-id="f3e20-109">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="f3e20-110">Questa esercitazione richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo.</span><span class="sxs-lookup"><span data-stu-id="f3e20-110">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="f3e20-111">Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="f3e20-111">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="f3e20-112">Se è necessario tooupgrade, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="f3e20-112">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="custom-script-extension-overview"></a><span data-ttu-id="f3e20-113">Panoramica dell'estensione script personalizzata</span><span class="sxs-lookup"><span data-stu-id="f3e20-113">Custom script extension overview</span></span>
<span data-ttu-id="f3e20-114">Estensione dello Script personalizzata Hello Scarica ed esegue gli script nelle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3e20-114">hello Custom Script Extension downloads and executes scripts on Azure VMs.</span></span> <span data-ttu-id="f3e20-115">Questa estensione è utile per la configurazione post-distribuzione, l'installazione di software o qualsiasi altra attività di configurazione o gestione.</span><span class="sxs-lookup"><span data-stu-id="f3e20-115">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="f3e20-116">Gli script possono essere scaricati da GitHub o di archiviazione di Azure o forniti toohello portale di Azure in fase di esecuzione di estensione.</span><span class="sxs-lookup"><span data-stu-id="f3e20-116">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span>

<span data-ttu-id="f3e20-117">estensione Script personalizzata Hello si integra con i modelli di gestione risorse di Azure e può essere eseguito anche tramite hello Azure CLI, PowerShell, il portale di Azure o hello API REST di macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f3e20-117">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="f3e20-118">È possibile utilizzare l'estensione dello Script personalizzata hello con le macchine virtuali Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="f3e20-118">You can use hello Custom Script Extension with both Windows and Linux VMs.</span></span>


## <a name="create-virtual-machine"></a><span data-ttu-id="f3e20-119">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f3e20-119">Create virtual machine</span></span>
<span data-ttu-id="f3e20-120">Per poter creare una macchina virtuale è prima necessario creare un gruppo di risorse con il comando [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="f3e20-120">Before you can create a VM, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="f3e20-121">esempio Hello crea un gruppo di risorse denominato *myResourceGroupAutomate* in hello *EastUS* percorso:</span><span class="sxs-lookup"><span data-stu-id="f3e20-121">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

<span data-ttu-id="f3e20-122">Impostare un amministratore di nome utente e password per le macchine virtuali hello con [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="f3e20-122">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="f3e20-123">Ora è possibile creare hello macchina virtuale con [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f3e20-123">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="f3e20-124">Crea componenti di rete virtuale hello necessario, la configurazione del sistema operativo hello, Hello seguente e quindi crea una macchina virtuale denominata *myVM*:</span><span class="sxs-lookup"><span data-stu-id="f3e20-124">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleWWW  `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName myResourceGroupAutomate -Location EastUS -VM $vmConfig
```

<span data-ttu-id="f3e20-125">Richiede alcuni minuti per le risorse di hello e toobe macchina virtuale creata.</span><span class="sxs-lookup"><span data-stu-id="f3e20-125">It takes a few minutes for hello resources and VM toobe created.</span></span>


## <a name="automate-iis-install"></a><span data-ttu-id="f3e20-126">Automatizzare l'installazione IIS</span><span class="sxs-lookup"><span data-stu-id="f3e20-126">Automate IIS install</span></span>
<span data-ttu-id="f3e20-127">Utilizzare [Set AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello estensione Script personalizzata.</span><span class="sxs-lookup"><span data-stu-id="f3e20-127">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="f3e20-128">Hello estensione esecuzioni `powershell Add-WindowsFeature Web-Server` tooinstall hello server Web IIS e quindi hello aggiornamenti *Default.htm* pagina tooshow hello hostname di hello VM:</span><span class="sxs-lookup"><span data-stu-id="f3e20-128">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName myResourceGroupAutomate `
    -ExtensionName IIS `
    -VMName myVM `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
    -Location EastUS
```


## <a name="test-web-site"></a><span data-ttu-id="f3e20-129">Testare il sito Web</span><span class="sxs-lookup"><span data-stu-id="f3e20-129">Test web site</span></span>
<span data-ttu-id="f3e20-130">Ottenere l'indirizzo IP pubblico di hello del servizio di bilanciamento del carico con [Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="f3e20-130">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="f3e20-131">esempio Hello Ottiene hello di indirizzo IP per *myPublicIP* creato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="f3e20-131">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

<span data-ttu-id="f3e20-132">È quindi possibile immettere l'indirizzo IP pubblico hello nel browser web tooa.</span><span class="sxs-lookup"><span data-stu-id="f3e20-132">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="f3e20-133">sito Hello viene visualizzato, inclusi hello nome host della macchina virtuale hello tale bilanciamento del carico hello distribuite tooas traffico nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="f3e20-133">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Esecuzione del sito Web IIS](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a><span data-ttu-id="f3e20-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f3e20-135">Next steps</span></span>

<span data-ttu-id="f3e20-136">In questa esercitazione è stato automatizzato hello IIS è installato in una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f3e20-136">In this tutorial, you automated hello IIS install on a VM.</span></span> <span data-ttu-id="f3e20-137">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="f3e20-137">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f3e20-138">Utilizzare tooinstall estensione Script personalizzata hello IIS</span><span class="sxs-lookup"><span data-stu-id="f3e20-138">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="f3e20-139">Creare una macchina virtuale che utilizza l'estensione dello Script personalizzata hello</span><span class="sxs-lookup"><span data-stu-id="f3e20-139">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="f3e20-140">Consente di visualizzare un sito IIS in esecuzione dopo l'applicazione di estensione hello</span><span class="sxs-lookup"><span data-stu-id="f3e20-140">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="f3e20-141">Spostare toolearn esercitazione successiva toohello come toocreate immagini di macchina virtuale personalizzate.</span><span class="sxs-lookup"><span data-stu-id="f3e20-141">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f3e20-142">Creare un'immagine di VM personalizzata</span><span class="sxs-lookup"><span data-stu-id="f3e20-142">Create custom VM images</span></span>](./tutorial-custom-images.md)
