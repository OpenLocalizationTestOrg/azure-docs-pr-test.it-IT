---
title: Avvio rapido - aaaAzure creare VM PowerShell | Documenti Microsoft
description: Apprendere toocreate una macchine virtuali Linux con PowerShell
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: f05ea7fedafe4fda660dc6084ae57ebf9dced473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a><span data-ttu-id="bf544-103">Creare una macchina virtuale Linux con PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf544-103">Create a Linux virtual machine with PowerShell</span></span>

<span data-ttu-id="bf544-104">modulo di Azure PowerShell Hello è toocreate utilizzato e gestire risorse di Azure dalla riga di comando di PowerShell hello o negli script.</span><span class="sxs-lookup"><span data-stu-id="bf544-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="bf544-105">Questa guida descrive l'utilizzo di una macchina virtuale in esecuzione il server Ubuntu toodeploy modulo di Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="bf544-105">This guide details using hello Azure PowerShell module toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="bf544-106">Dopo aver distribuito il server di hello, viene creata una connessione SSH e viene installato un server Web NGINX.</span><span class="sxs-lookup"><span data-stu-id="bf544-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="bf544-107">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="bf544-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="bf544-108">Questa Guida introduttiva richiede hello Azure PowerShell versione 3.6 o versioni successive del modulo.</span><span class="sxs-lookup"><span data-stu-id="bf544-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="bf544-109">Eseguire ` Get-Module -ListAvailable AzureRM` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="bf544-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="bf544-110">Se è necessario tooinstall o l'aggiornamento, vedere [modulo installare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="bf544-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="bf544-111">Infine, una chiave SSH pubblica con nome hello *id_rsa.pub* deve toobe archiviati in hello *.ssh* directory del profilo utente Windows.</span><span class="sxs-lookup"><span data-stu-id="bf544-111">Finally, a public SSH key with hello name *id_rsa.pub* needs toobe stored in hello *.ssh* directory of your Windows user profile.</span></span> <span data-ttu-id="bf544-112">Per informazioni dettagliate sulla creazione delle chiavi SSH per Azure, vedere [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Creare chiavi SSH per Azure).</span><span class="sxs-lookup"><span data-stu-id="bf544-112">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="bf544-113">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="bf544-113">Log in tooAzure</span></span>

<span data-ttu-id="bf544-114">Accedere alla sottoscrizione di Azure con hello tooyour `Login-AzureRmAccount` comando e seguire hello le direzioni.</span><span class="sxs-lookup"><span data-stu-id="bf544-114">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="bf544-115">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="bf544-115">Create resource group</span></span>

<span data-ttu-id="bf544-116">Creare un gruppo di risorse di Azure con [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="bf544-116">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="bf544-117">Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="bf544-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a><span data-ttu-id="bf544-118">Creare risorse di rete</span><span class="sxs-lookup"><span data-stu-id="bf544-118">Create networking resources</span></span>

<span data-ttu-id="bf544-119">Creare una rete virtuale, una subnet e un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="bf544-119">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="bf544-120">Queste risorse sono la macchina virtuale utilizzati tooprovide rete connettività toohello e connetterla toohello internet.</span><span class="sxs-lookup"><span data-stu-id="bf544-120">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location eastus `
-Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location eastus `
-AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

<span data-ttu-id="bf544-121">Creare un gruppo di sicurezza di rete e una regola del gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="bf544-121">Create a network security group and a network security group rule.</span></span> <span data-ttu-id="bf544-122">gruppo di sicurezza di rete Hello protegge una macchina virtuale hello utilizzando le regole in entrata e in uscita.</span><span class="sxs-lookup"><span data-stu-id="bf544-122">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="bf544-123">In questo caso viene creata una regola in entrata per la porta 22 che consente le connessioni SSH in ingresso.</span><span class="sxs-lookup"><span data-stu-id="bf544-123">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span></span> <span data-ttu-id="bf544-124">È anche necessario toocreate una regola in entrata per la porta 80, che consente il traffico web in ingresso.</span><span class="sxs-lookup"><span data-stu-id="bf544-124">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleSSH  -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location eastus `
-Name myNetworkSecurityGroup -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

<span data-ttu-id="bf544-125">Creare una scheda di rete con [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="bf544-125">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="bf544-126">scheda di rete Hello connette hello macchina virtuale tooa subnet, il gruppo di sicurezza di rete e indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="bf544-126">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="bf544-127">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="bf544-127">Create virtual machine</span></span>

<span data-ttu-id="bf544-128">Creare una configurazione di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="bf544-128">Create a virtual machine configuration.</span></span> <span data-ttu-id="bf544-129">Questa configurazione include le impostazioni di hello utilizzate quando si distribuisce una macchina virtuale hello, ad esempio un'immagine, dimensioni e l'autenticazione di configurazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="bf544-129">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span>

```powershell
# Define a credential object
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("azureuser", $securePassword)

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Linux -ComputerName myVM -Credential $cred -DisablePasswordAuthentication | `
Set-AzureRmVMSourceImage -PublisherName Canonical -Offer UbuntuServer -Skus 14.04.2-LTS -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmconfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"
```

<span data-ttu-id="bf544-130">Creare una macchina virtuale hello con [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="bf544-130">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="bf544-131">Connettere la macchina toovirtual</span><span class="sxs-lookup"><span data-stu-id="bf544-131">Connect toovirtual machine</span></span>

<span data-ttu-id="bf544-132">Una volta completata la distribuzione di hello, creare una connessione SSH con la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="bf544-132">After hello deployment has completed, create an SSH connection with hello virtual machine.</span></span>

<span data-ttu-id="bf544-133">Hello utilizzare [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) comando tooreturn hello indirizzo IP pubblico della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="bf544-133">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="bf544-134">Da un sistema con SSH installato, macchina virtuale di tooconnect toohello comando che segue di hello utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bf544-134">From a system with SSH installed, used hello following command tooconnect toohello virtual machine.</span></span> <span data-ttu-id="bf544-135">Se l'utilizzo in Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) può essere utilizzato toocreate hello connessione.</span><span class="sxs-lookup"><span data-stu-id="bf544-135">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used toocreate hello connection.</span></span> 

```bash 
ssh <Public IP Address>
```

<span data-ttu-id="bf544-136">Quando richiesto, nome utente di accesso hello è *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="bf544-136">When prompted, hello login user name is *azureuser*.</span></span> <span data-ttu-id="bf544-137">Se durante la creazione di chiavi SSH è stata immessa una passphrase, è necessario anche questo tooenter.</span><span class="sxs-lookup"><span data-stu-id="bf544-137">If a passphrase was entered when creating SSH keys, you need tooenter this as well.</span></span>


## <a name="install-nginx"></a><span data-ttu-id="bf544-138">Installare NGINX</span><span class="sxs-lookup"><span data-stu-id="bf544-138">Install NGINX</span></span>

<span data-ttu-id="bf544-139">Seguente hello utilizzare origini dei pacchetti tooupdate script bash e installare il pacchetto NGINX più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="bf544-139">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a><span data-ttu-id="bf544-140">Pagina iniziale di visualizzazione hello NGIX</span><span class="sxs-lookup"><span data-stu-id="bf544-140">View hello NGIX welcome page</span></span>

<span data-ttu-id="bf544-141">Con NGINX installato e la porta 80 è aperta nella VM da hello Internet, è possibile utilizzare un browser web la scelta tooview hello NGINX pagina iniziale predefinita.</span><span class="sxs-lookup"><span data-stu-id="bf544-141">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="bf544-142">Impossibile verificare toouse hello indirizzo IP pubblico che descritto in precedenza pagina predefinita di toovisit hello.</span><span class="sxs-lookup"><span data-stu-id="bf544-142">Be sure toouse hello public IP address you documented above toovisit hello default page.</span></span> 

![Sito NGINX predefinito](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="bf544-144">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="bf544-144">Clean up resources</span></span>

<span data-ttu-id="bf544-145">Quando non è più necessario, è possibile utilizzare hello [Remove AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) comando gruppo di risorse tooremove hello, macchina virtuale e tutte le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="bf544-145">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="bf544-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bf544-146">Next steps</span></span>

<span data-ttu-id="bf544-147">In questa guida introduttiva è stata distribuita una macchina virtuale semplice, è stata creata una regola del gruppo di sicurezza di rete ed è stato installato un server Web.</span><span class="sxs-lookup"><span data-stu-id="bf544-147">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="bf544-148">toolearn informazioni sulle macchine virtuali di Azure, continuare l'esercitazione toohello per le macchine virtuali Linux.</span><span class="sxs-lookup"><span data-stu-id="bf544-148">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bf544-149">Esercitazioni per le macchine virtuali di Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="bf544-149">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
