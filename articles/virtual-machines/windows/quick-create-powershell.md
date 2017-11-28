---
title: Avvio rapido - aaaAzure creare PowerShell VM di Windows | Documenti Microsoft
description: Apprendere toocreate una macchina virtuale di Windows con PowerShell
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
ms.openlocfilehash: 5e92435bf7ee443a01c158fed91c356363e2f425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a><span data-ttu-id="1d6c6-103">Creare una macchina virtuale Windows con PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d6c6-103">Create a Windows virtual machine with PowerShell</span></span>

<span data-ttu-id="1d6c6-104">modulo di Azure PowerShell Hello è toocreate utilizzato e gestire risorse di Azure dalla riga di comando di PowerShell hello o negli script.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="1d6c6-105">Questa guida descrive l'utilizzo di PowerShell toocreate e macchina virtuale di Azure che esegue Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-105">This guide details using PowerShell toocreate and Azure virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="1d6c6-106">Una volta completata la distribuzione, è connettersi toohello server e installare IIS.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-106">Once deployment is complete, we connect toohello server and install IIS.</span></span>  

<span data-ttu-id="1d6c6-107">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="1d6c6-108">Questa Guida introduttiva richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="1d6c6-109">Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="1d6c6-110">Se è necessario tooinstall o l'aggiornamento, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="1d6c6-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="1d6c6-111">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="1d6c6-111">Log in tooAzure</span></span>

<span data-ttu-id="1d6c6-112">Accedere alla sottoscrizione di Azure con hello tooyour `Login-AzureRmAccount` comando e seguire hello le direzioni.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-112">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="1d6c6-113">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="1d6c6-113">Create resource group</span></span>

<span data-ttu-id="1d6c6-114">Creare un gruppo di risorse di Azure con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="1d6c6-114">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="1d6c6-115">Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a><span data-ttu-id="1d6c6-116">Creare risorse di rete</span><span class="sxs-lookup"><span data-stu-id="1d6c6-116">Create networking resources</span></span>

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a><span data-ttu-id="1d6c6-117">Creare una rete virtuale, una subnet e un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-117">Create a virtual network, subnet, and a public IP address.</span></span> 
<span data-ttu-id="1d6c6-118">Queste risorse sono la macchina virtuale utilizzati tooprovide rete connettività toohello e connetterla toohello internet.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-118">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

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

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="1d6c6-119">Creare un gruppo di sicurezza di rete e una regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-119">Create a network security group and a network security group rule.</span></span> 
<span data-ttu-id="1d6c6-120">gruppo di sicurezza di rete Hello protegge una macchina virtuale hello utilizzando le regole in entrata e in uscita.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-120">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="1d6c6-121">In questo caso viene creata una regola in entrata per la porta 3389 che consente connessioni desktop remoto in ingresso.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-121">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span> <span data-ttu-id="1d6c6-122">È anche necessario toocreate una regola in entrata per la porta 80, che consente il traffico web in ingresso.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-122">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

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

### <a name="create-a-network-card-for-hello-virtual-machine"></a><span data-ttu-id="1d6c6-123">Creare una scheda di rete per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-123">Create a network card for hello virtual machine.</span></span> 
<span data-ttu-id="1d6c6-124">Creare una scheda di rete con [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-124">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="1d6c6-125">scheda di rete Hello connette hello macchina virtuale tooa subnet, il gruppo di sicurezza di rete e indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-125">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="1d6c6-126">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="1d6c6-126">Create virtual machine</span></span>

<span data-ttu-id="1d6c6-127">Creare una configurazione di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-127">Create a virtual machine configuration.</span></span> <span data-ttu-id="1d6c6-128">Questa configurazione include le impostazioni di hello utilizzate quando si distribuisce una macchina virtuale hello, ad esempio un'immagine, dimensioni e l'autenticazione di configurazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-128">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span> <span data-ttu-id="1d6c6-129">Quando si esegue questo passaggio vengono chieste le credenziali.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-129">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="1d6c6-130">i valori Hello immesse siano configurati come nome utente hello e una password per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-130">hello values that you enter are configured as hello user name and password for hello virtual machine.</span></span>

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

<span data-ttu-id="1d6c6-131">Creare una macchina virtuale hello con [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="1d6c6-131">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="1d6c6-132">Connettere la macchina toovirtual</span><span class="sxs-lookup"><span data-stu-id="1d6c6-132">Connect toovirtual machine</span></span>

<span data-ttu-id="1d6c6-133">Una volta completata la distribuzione di hello, creare una connessione desktop remoto con la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-133">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="1d6c6-134">Hello utilizzare [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) comando tooreturn hello indirizzo IP pubblico della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-134">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="1d6c6-135">Prendere nota dell'indirizzo IP per la connessione tooit con la connettività di web browser tootest in un passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-135">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="1d6c6-136">Comando che segue di hello utilizzare toocreate una sessione desktop remota con la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-136">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="1d6c6-137">Sostituire l'indirizzo IP hello con hello *publicIPAddress* della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-137">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="1d6c6-138">Quando richiesto, immettere le credenziali di hello utilizzate durante la creazione di macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-138">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a><span data-ttu-id="1d6c6-139">Installare IIS tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d6c6-139">Install IIS via PowerShell</span></span>

<span data-ttu-id="1d6c6-140">Ora che è stato effettuato in toohello macchina virtuale di Azure, è possibile utilizzare una singola riga di PowerShell tooinstall IIS e abilitare il traffico web tooallow di hello firewall locale regola.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-140">Now that you have logged in toohello Azure VM, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="1d6c6-141">Aprire un prompt dei comandi di PowerShell ed eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1d6c6-141">Open a PowerShell prompt and run hello following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="1d6c6-142">Hello Visualizza la pagina iniziale di IIS</span><span class="sxs-lookup"><span data-stu-id="1d6c6-142">View hello IIS welcome page</span></span>

<span data-ttu-id="1d6c6-143">Con IIS installato e la porta 80 è aperta nella VM da hello Internet, è possibile utilizzare un browser web la pagina iniziale tooview scelte hello predefinita IIS.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-143">With IIS installed and port 80 now open on your VM from hello Internet, you can use a web browser of your choice tooview hello default IIS welcome page.</span></span> <span data-ttu-id="1d6c6-144">Essere certi hello toouse *publicIpAddress* descritto in precedenza pagina predefinita di toovisit hello.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-144">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![Sito IIS predefinito](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="1d6c6-146">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="1d6c6-146">Clean up resources</span></span>

<span data-ttu-id="1d6c6-147">Quando non è più necessario, è possibile utilizzare hello [Remove AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) comando gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-147">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="1d6c6-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1d6c6-148">Next steps</span></span>

<span data-ttu-id="1d6c6-149">In questa guida introduttiva è stata distribuita una macchina virtuale semplice, è stata creata una regola del gruppo di sicurezza di rete ed è stato installato un server Web.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-149">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="1d6c6-150">toolearn informazioni sulle macchine virtuali di Azure, continuare l'esercitazione toohello per le macchine virtuali di Windows.</span><span class="sxs-lookup"><span data-stu-id="1d6c6-150">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1d6c6-151">Esercitazioni per le macchine virtuali di Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="1d6c6-151">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
