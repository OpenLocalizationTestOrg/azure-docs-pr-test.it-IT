---
title: Avvio rapido in Azure - Creare VM Windows con PowerShell | Documentazione Microsoft
description: Informazioni veloci su come creare una macchina virtuale Windows con PowerShell
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 8516cfa2272694496eb353a83eca77c13a516750
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a><span data-ttu-id="89d81-103">Creare una macchina virtuale Windows con PowerShell</span><span class="sxs-lookup"><span data-stu-id="89d81-103">Create a Windows virtual machine with PowerShell</span></span>

<span data-ttu-id="89d81-104">Il modulo Azure PowerShell viene usato per creare e gestire le risorse di Azure dalla riga di comando di PowerShell o negli script.</span><span class="sxs-lookup"><span data-stu-id="89d81-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span></span> <span data-ttu-id="89d81-105">Questa guida descrive dettagliatamente l'uso di PowerShell per creare una macchina virtuale di Azure che esegue Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="89d81-105">This guide details using PowerShell to create and Azure virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="89d81-106">Al termine della distribuzione, viene eseguita la connessione al server e viene installato IIS.</span><span class="sxs-lookup"><span data-stu-id="89d81-106">Once deployment is complete, we connect to the server and install IIS.</span></span>  

<span data-ttu-id="89d81-107">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="89d81-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="89d81-108">Questa guida introduttiva richiede il modulo Azure PowerShell 3.6 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="89d81-108">This quick start requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="89d81-109">Eseguire ` Get-Module -ListAvailable AzureRM` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="89d81-109">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="89d81-110">Se è necessario eseguire l'installazione o l'aggiornamento, vedere come [installare il modulo Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="89d81-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="89d81-111">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="89d81-111">Log in to Azure</span></span>

<span data-ttu-id="89d81-112">Accedere alla sottoscrizione di Azure con il comando `Login-AzureRmAccount` e seguire le istruzioni visualizzate.</span><span class="sxs-lookup"><span data-stu-id="89d81-112">Log in to your Azure subscription with the `Login-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="89d81-113">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="89d81-113">Create resource group</span></span>

<span data-ttu-id="89d81-114">Creare un gruppo di risorse di Azure con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="89d81-114">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="89d81-115">Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="89d81-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a><span data-ttu-id="89d81-116">Creare risorse di rete</span><span class="sxs-lookup"><span data-stu-id="89d81-116">Create networking resources</span></span>

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a><span data-ttu-id="89d81-117">Creare una rete virtuale, una subnet e un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="89d81-117">Create a virtual network, subnet, and a public IP address.</span></span> 
<span data-ttu-id="89d81-118">Queste risorse vengono usate per fornire la connettività di rete alla macchina virtuale e connetterla a Internet.</span><span class="sxs-lookup"><span data-stu-id="89d81-118">These resources are used to provide network connectivity to the virtual machine and connect it to the internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location EastUS `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location EastUS `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="89d81-119">Creare un gruppo di sicurezza di rete e una regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="89d81-119">Create a network security group and a network security group rule.</span></span> 
<span data-ttu-id="89d81-120">Il gruppo di sicurezza di rete protegge la macchina virtuale usando le regole in entrata e in uscita.</span><span class="sxs-lookup"><span data-stu-id="89d81-120">The network security group secures the virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="89d81-121">In questo caso viene creata una regola in entrata per la porta 3389 che consente connessioni desktop remoto in ingresso.</span><span class="sxs-lookup"><span data-stu-id="89d81-121">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span> <span data-ttu-id="89d81-122">È necessario anche creare una regola in ingresso per la porta 80, che consente il traffico Web in ingresso.</span><span class="sxs-lookup"><span data-stu-id="89d81-122">We also want to create an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-the-virtual-machine"></a><span data-ttu-id="89d81-123">Creare una scheda di rete per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="89d81-123">Create a network card for the virtual machine.</span></span> 
<span data-ttu-id="89d81-124">Creare una scheda di rete con [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="89d81-124">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for the virtual machine.</span></span> <span data-ttu-id="89d81-125">La scheda di rete connette la macchina virtuale a una subnet, a un gruppo di sicurezza di rete e a un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="89d81-125">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="89d81-126">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="89d81-126">Create virtual machine</span></span>

<span data-ttu-id="89d81-127">Creare una configurazione di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="89d81-127">Create a virtual machine configuration.</span></span> <span data-ttu-id="89d81-128">Questa configurazione include le impostazioni utilizzate quando si distribuisce la macchina virtuale, ad esempio l'immagine della macchina virtuale, la dimensione e la configurazione di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="89d81-128">This configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, and authentication configuration.</span></span> <span data-ttu-id="89d81-129">Quando si esegue questo passaggio vengono chieste le credenziali.</span><span class="sxs-lookup"><span data-stu-id="89d81-129">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="89d81-130">I valori immessi sono configurati come nome utente e password per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="89d81-130">The values that you enter are configured as the user name and password for the virtual machine.</span></span>

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

<span data-ttu-id="89d81-131">Creare la macchina virtuale con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="89d81-131">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-to-virtual-machine"></a><span data-ttu-id="89d81-132">Connettersi alla macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="89d81-132">Connect to virtual machine</span></span>

<span data-ttu-id="89d81-133">Dopo aver completato la distribuzione, creare una connessione desktop remoto con la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="89d81-133">After the deployment has completed, create a remote desktop connection with the virtual machine.</span></span>

<span data-ttu-id="89d81-134">Usare il comando [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) per ottenere l'indirizzo IP pubblico della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="89d81-134">Use the [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command to return the public IP address of the virtual machine.</span></span> <span data-ttu-id="89d81-135">Annotare questo indirizzo IP, in modo da potersi connettere ad esso con il browser per testare la connettività Web in un passaggio futuro.</span><span class="sxs-lookup"><span data-stu-id="89d81-135">Take note of this IP Address so you can connect to it with your browser to test web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="89d81-136">Usare il comando seguente per creare una sessione desktop remoto con la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="89d81-136">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="89d81-137">Sostituire l'indirizzo IP con l'indirizzo *publicIPAddress* della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="89d81-137">Replace the IP address with the *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="89d81-138">Quando richiesto, immettere le credenziali utilizzate durante la creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="89d81-138">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a><span data-ttu-id="89d81-139">Installare IIS tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="89d81-139">Install IIS via PowerShell</span></span>

<span data-ttu-id="89d81-140">Dopo avere eseguito l'accesso alla macchina virtuale di Azure, è possibile usare una singola riga di codice di PowerShell per installare IIS e abilitare la regola del firewall locale per consentire il traffico Web.</span><span class="sxs-lookup"><span data-stu-id="89d81-140">Now that you have logged in to the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="89d81-141">Aprire un prompt di PowerShell ed eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="89d81-141">Open a PowerShell prompt and run the following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="89d81-142">Visualizzare la pagina iniziale di IIS</span><span class="sxs-lookup"><span data-stu-id="89d81-142">View the IIS welcome page</span></span>

<span data-ttu-id="89d81-143">Dopo l'installazione di IIS e l'apertura della porta 80 nella macchina virtuale da Internet, è possibile usare il Web browser preferito per visualizzare la pagina iniziale predefinita di IIS.</span><span class="sxs-lookup"><span data-stu-id="89d81-143">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span></span> <span data-ttu-id="89d81-144">Assicurarsi di usare l'indirizzo *publicIpAddress* descritto in precedenza per passare alla pagina predefinita.</span><span class="sxs-lookup"><span data-stu-id="89d81-144">Be sure to use the *publicIpAddress* you documented above to visit the default page.</span></span> 

![Sito IIS predefinito](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="89d81-146">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="89d81-146">Clean up resources</span></span>

<span data-ttu-id="89d81-147">Quando non servono più, è possibile usare il comando [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) per rimuovere il gruppo di risorse, la macchina virtuale e tutte le risorse correlate.</span><span class="sxs-lookup"><span data-stu-id="89d81-147">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="89d81-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="89d81-148">Next steps</span></span>

<span data-ttu-id="89d81-149">In questa guida introduttiva è stata distribuita una macchina virtuale semplice, è stata creata una regola del gruppo di sicurezza di rete ed è stato installato un server Web.</span><span class="sxs-lookup"><span data-stu-id="89d81-149">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="89d81-150">Per altre informazioni sulle macchine virtuali di Azure, passare all'esercitazione per le VM di Windows.</span><span class="sxs-lookup"><span data-stu-id="89d81-150">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="89d81-151">Esercitazioni per le macchine virtuali di Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="89d81-151">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
