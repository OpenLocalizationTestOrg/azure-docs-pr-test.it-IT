---
title: "Creare un set di scalabilità di macchine virtuali di Azure | Microsoft Docs"
description: "Creare e distribuire un set di scalabilità di macchine virtuali Linux o Windows Azure con l'interfaccia della riga di comando di Azure, PowerShell, un modello o Visual Studio."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 07/21/2017
ms.author: adegeo
ms.openlocfilehash: 32af01aa545c541688128a7ae6bbb82a0e046f2d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a><span data-ttu-id="420b0-103">Creare e distribuire un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="420b0-103">Create and deploy a virtual machine scale set</span></span>
<span data-ttu-id="420b0-104">I set di scalabilità di macchine virtuali semplificano la distribuzione e la gestione di macchine virtuali identiche come un set.</span><span class="sxs-lookup"><span data-stu-id="420b0-104">Virtual machine scale sets make it easy for you to deploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="420b0-105">I set di scalabilità offrono un livello di calcolo scalabile e personalizzabile per applicazioni con iperscalabilità e supportano le immagini della piattaforma Windows, le immagini della piattaforma Linux, le immagini personalizzate e le estensioni.</span><span class="sxs-lookup"><span data-stu-id="420b0-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="420b0-106">Per altre informazioni sui set di scalabilità, vedere [Set di scalabilità di macchine virtuali](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="420b0-106">For more information about scale sets, see [Virtual machine scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="420b0-107">Questa esercitazione mostra come creare un set di scalabilità di macchine virtuali **senza** usare il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="420b0-107">This tutorial shows you how to create a virtual machine scale set **without** using the Azure portal.</span></span> <span data-ttu-id="420b0-108">Per informazioni su come usare il portale di Azure, vedere [Come creare un set di scalabilità di macchine virtuali tramite il portale di Azure](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="420b0-108">For information about how to use the Azure portal, see [How to create a virtual machine scale set with the Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

>[!NOTE]
><span data-ttu-id="420b0-109">Per altre informazioni sulle risorse di Azure Resource Manager, vedere [Confronto tra distribuzione di Azure Resource Manager e classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="420b0-109">For more information about Azure Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="420b0-110">Accedere ad Azure</span><span class="sxs-lookup"><span data-stu-id="420b0-110">Sign in to Azure</span></span>

<span data-ttu-id="420b0-111">Se si usa l'interfaccia della riga di comando di Azure 2.0 o Azure PowerShell per creare un set di scalabilità, per prima cosa è necessario accedere alla propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="420b0-111">If you're using Azure CLI 2.0 or Azure PowerShell to create a scale set, you first need to sign in to your subscription.</span></span>

<span data-ttu-id="420b0-112">Per altre informazioni su come installare, configurare e accedere ad Azure con l'interfaccia della riga di comando di Azure o con PowerShell, vedere [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) (Introduzione all'interfaccia della riga di comando di Azure 2.0) o [Get started with Azure PowerShell cmdlets](/powershell/azure/overview) (Introduzione ai cmdlet di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="420b0-112">For more information about how to install, set up, and sign in to Azure with Azure CLI or PowerShell, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) or [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="420b0-113">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="420b0-113">Create a resource group</span></span>

<span data-ttu-id="420b0-114">Per prima cosa è necessario creare un gruppo di risorse a cui sia associato il set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="420b0-114">You first need to create a resource group that the virtual machine scale set is associated with.</span></span>

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a><span data-ttu-id="420b0-115">Creare un set di scalabilità dall'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="420b0-115">Create from Azure CLI</span></span>

<span data-ttu-id="420b0-116">Con l'interfaccia della riga di comando di Azure, è possibile creare facilmente un set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="420b0-116">With Azure CLI, you can create a virtual machine scale set with minimal effort.</span></span> <span data-ttu-id="420b0-117">Se omessi, i valori predefiniti vengono forniti automaticamente.</span><span class="sxs-lookup"><span data-stu-id="420b0-117">If you omit default values, they are provided for you.</span></span> <span data-ttu-id="420b0-118">Ad esempio, se non si specificano le informazioni relative alla rete virtuale, ne verrà creata una automaticamente.</span><span class="sxs-lookup"><span data-stu-id="420b0-118">For example, if you don't specify any virtual network information, a virtual network is created for you.</span></span> <span data-ttu-id="420b0-119">Se si omettono le parti seguenti, queste verranno create:</span><span class="sxs-lookup"><span data-stu-id="420b0-119">If you omit the following parts, they are created for you:</span></span> 
- <span data-ttu-id="420b0-120">Un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="420b0-120">A load balancer</span></span>
- <span data-ttu-id="420b0-121">Una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="420b0-121">A virtual network</span></span>
- <span data-ttu-id="420b0-122">Un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="420b0-122">A public IP address</span></span>

<span data-ttu-id="420b0-123">Quando si sceglie l'immagine della macchina virtuale da usare nel set di scalabilità di macchine virtuali, sono disponibili alcune opzioni:</span><span class="sxs-lookup"><span data-stu-id="420b0-123">When choosing the virtual machine image that you want to use on the virtual machine scale set, you have a few choices:</span></span>

- <span data-ttu-id="420b0-124">URN</span><span class="sxs-lookup"><span data-stu-id="420b0-124">URN</span></span>  
<span data-ttu-id="420b0-125">L'identificatore di una risorsa:</span><span class="sxs-lookup"><span data-stu-id="420b0-125">The identifier of a resource:</span></span>  
<span data-ttu-id="420b0-126">**Win2012R2Datacenter**</span><span class="sxs-lookup"><span data-stu-id="420b0-126">**Win2012R2Datacenter**</span></span>

- <span data-ttu-id="420b0-127">Alias URN</span><span class="sxs-lookup"><span data-stu-id="420b0-127">URN alias</span></span>  
<span data-ttu-id="420b0-128">Il nome descrittivo di un URN:</span><span class="sxs-lookup"><span data-stu-id="420b0-128">The friendly name of a URN:</span></span>  
<span data-ttu-id="420b0-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span><span class="sxs-lookup"><span data-stu-id="420b0-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span></span>

- <span data-ttu-id="420b0-130">ID risorsa personalizzata</span><span class="sxs-lookup"><span data-stu-id="420b0-130">Custom resource id</span></span>  
<span data-ttu-id="420b0-131">Il percorso di una risorsa di Azure:</span><span class="sxs-lookup"><span data-stu-id="420b0-131">The path to an Azure resource:</span></span>  
<span data-ttu-id="420b0-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span><span class="sxs-lookup"><span data-stu-id="420b0-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span></span>

- <span data-ttu-id="420b0-133">Risorsa Web</span><span class="sxs-lookup"><span data-stu-id="420b0-133">Web resource</span></span>  
<span data-ttu-id="420b0-134">Il percorso di un URI HTTP:</span><span class="sxs-lookup"><span data-stu-id="420b0-134">The path to an HTTP URI:</span></span>  
<span data-ttu-id="420b0-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span><span class="sxs-lookup"><span data-stu-id="420b0-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span></span>

>[!TIP]
><span data-ttu-id="420b0-136">È possibile ottenere un elenco di immagini disponibili con `az vm image list`.</span><span class="sxs-lookup"><span data-stu-id="420b0-136">You can get a list of available images with `az vm image list`.</span></span>

<span data-ttu-id="420b0-137">Per creare un set di scalabilità di macchine virtuali, è necessario specificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="420b0-137">To create a virtual machine scale set, you must specify the following:</span></span>

- <span data-ttu-id="420b0-138">Resource group</span><span class="sxs-lookup"><span data-stu-id="420b0-138">Resource group</span></span> 
- <span data-ttu-id="420b0-139">Nome</span><span class="sxs-lookup"><span data-stu-id="420b0-139">Name</span></span>
- <span data-ttu-id="420b0-140">Immagine del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="420b0-140">Operating system image</span></span>
- <span data-ttu-id="420b0-141">Informazioni di autenticazione</span><span class="sxs-lookup"><span data-stu-id="420b0-141">Authentication information</span></span> 
 
<span data-ttu-id="420b0-142">L'esempio seguente crea un set di scalabilità di macchine virtuali di base (questo passaggio può richiedere alcuni minuti).</span><span class="sxs-lookup"><span data-stu-id="420b0-142">The following example creates a basic virtual machine scale set (this step might take a few minutes).</span></span>

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

<span data-ttu-id="420b0-143">Dopo il completamento del comando il set di scalabilità di macchine virtuali è stato creato.</span><span class="sxs-lookup"><span data-stu-id="420b0-143">Once the command finishes you will now have your virtual machine scale set created.</span></span> <span data-ttu-id="420b0-144">Potrebbe essere necessario ottenere l'indirizzo IP della macchina virtuale per stabilire la connessione.</span><span class="sxs-lookup"><span data-stu-id="420b0-144">You may need to get the IP address of the virtual machine so that you can connect to it.</span></span> <span data-ttu-id="420b0-145">È possibile ottenere varie informazioni relative alla macchina virtuale (incluso l'indirizzo IP) con il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="420b0-145">You can get a lot of different information about the virtual machine (including the IP address) with the following command.</span></span> 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a><span data-ttu-id="420b0-146">Creare un set di scalabilità da PowerShell</span><span class="sxs-lookup"><span data-stu-id="420b0-146">Create from PowerShell</span></span>

<span data-ttu-id="420b0-147">PowerShell è più complicato da usare rispetto all'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="420b0-147">PowerShell is more complicated to use than Azure CLI.</span></span> <span data-ttu-id="420b0-148">Mentre l'interfaccia della riga di comando di Azure fornisce automaticamente le opzioni predefinite per le risorse di rete (bilanciamenti del carico, indirizzi IP, reti virtuali), questo non avviene in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="420b0-148">While Azure CLI provides defaults for networking-related resources (such as load balancers, IP addresses, and virtual networks), PowerShell does not.</span></span> <span data-ttu-id="420b0-149">Anche fare riferimento a un'immagine con PowerShell è leggermente più complicato.</span><span class="sxs-lookup"><span data-stu-id="420b0-149">Referencing an image with PowerShell is a slightly more complicated too.</span></span> <span data-ttu-id="420b0-150">È possibile ottenere immagini con i cmdlet seguenti:</span><span class="sxs-lookup"><span data-stu-id="420b0-150">You can get images with the following cmdlets:</span></span>

1. <span data-ttu-id="420b0-151">Get-AzureRMVMImagePublisher</span><span class="sxs-lookup"><span data-stu-id="420b0-151">Get-AzureRMVMImagePublisher</span></span>
2. <span data-ttu-id="420b0-152">Get-AzureRMVMImageOffer</span><span class="sxs-lookup"><span data-stu-id="420b0-152">Get-AzureRMVMImageOffer</span></span>
3. <span data-ttu-id="420b0-153">Get-AzureRmVMImageSku</span><span class="sxs-lookup"><span data-stu-id="420b0-153">Get-AzureRmVMImageSku</span></span>

<span data-ttu-id="420b0-154">Il lavoro dei cmdlet può essere reindirizzato in sequenza.</span><span class="sxs-lookup"><span data-stu-id="420b0-154">The cmdlets work can be piped in sequence.</span></span> <span data-ttu-id="420b0-155">Di seguito è riportato un esempio di come ottenere tutte le immagini per l'area **West US 2** (Stati Uniti occidentali 2) il cui nome dell'editore contiene **microsoft**.</span><span class="sxs-lookup"><span data-stu-id="420b0-155">Here is an example of how to get all images for the **West US 2** region with a publisher that has the name **microsoft** in it.</span></span>

```powershell
Get-AzureRMVMImagePublisher -Location WestUS2 | Where-Object PublisherName -Like *microsoft* | Get-AzureRMVMImageOffer | Get-AzureRmVMImageSku | Select-Object PublisherName, Offer, Skus
```

```
PublisherName              Offer                    Skus
-------------              -----                    ----
microsoft-ads              linux-data-science-vm    linuxdsvm
microsoft-ads              standard-data-science-vm standard-data-science-vm
MicrosoftAzureSiteRecovery Process-Server           Windows-2012-R2-Datacenter
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Enterprise
MicrosoftBizTalkServer     BizTalk-Server           2013-R2-Standard
MicrosoftBizTalkServer     BizTalk-Server           2016-Developer
MicrosoftBizTalkServer     BizTalk-Server           2016-Enterprise
...
```

<span data-ttu-id="420b0-156">Il flusso di lavoro per la creazione di un set di scalabilità di macchine virtuali è il seguente:</span><span class="sxs-lookup"><span data-stu-id="420b0-156">The workflow for creating a virtual machine scale set is as follows:</span></span>

1. <span data-ttu-id="420b0-157">Creare un oggetto di configurazione contenente informazioni sul set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="420b0-157">Create a config object that holds information about the scale set.</span></span>
2. <span data-ttu-id="420b0-158">Fare riferimento all'immagine del sistema operativo di base.</span><span class="sxs-lookup"><span data-stu-id="420b0-158">Reference the base OS image.</span></span>
3. <span data-ttu-id="420b0-159">Configurare le impostazioni del sistema operativo: autenticazione, prefisso del nome della VM e utente/password.</span><span class="sxs-lookup"><span data-stu-id="420b0-159">Configure the operating system settings: authentication, VM name prefix, and user/pass.</span></span>
4. <span data-ttu-id="420b0-160">Configurare le impostazioni di rete.</span><span class="sxs-lookup"><span data-stu-id="420b0-160">Configure networking.</span></span>
5. <span data-ttu-id="420b0-161">Creare il set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="420b0-161">Create the scale set.</span></span>

<span data-ttu-id="420b0-162">Questo esempio consente di creare un set di scalabilità di base a due istanze per un computer con installato Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="420b0-162">This example creates a basic two-instance scale set for a computer that has Windows Server 2016 installed.</span></span>

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from the gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with the virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create the virtual network resources

## Basics
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name "my-subnet" -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name "my-network" -ResourceGroupName $rg -Location $location -AddressPrefix 10.0.0.0/16 -Subnet $subnet

## Load balancer
$publicIP = New-AzureRmPublicIpAddress -Name "PublicIP" -ResourceGroupName $rg -Location $location -AllocationMethod Static -DomainNameLabel "myuniquedomain"
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontend" -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "LB-backend"
$probe = New-AzureRmLoadBalancerProbeConfig -Name "HealthProbe" -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
$inboundNATRule1= New-AzureRmLoadBalancerRuleConfig -Name "webserver" -FrontendIpConfiguration $frontendIP -Protocol Tcp -FrontendPort 80 -BackendPort 80 -IdleTimeoutInMinutes 15 -Probe $probe -BackendAddressPool $backendPool
$inboundNATPool1 = New-AzureRmLoadBalancerInboundNatPoolConfig -Name "RDP" -FrontendIpConfigurationId $frontendIP.Id -Protocol TCP -FrontendPortRangeStart 53380 -FrontendPortRangeEnd 53390 -BackendPort 3389

New-AzureRmLoadBalancer -ResourceGroupName $rg -Name "LB1" -Location $location -FrontendIpConfiguration $frontendIP -LoadBalancingRule $inboundNATRule1 -InboundNatPool $inboundNATPool1 -BackendAddressPool $backendPool -Probe $probe

## IP address config
$ipConfig = New-AzureRmVmssIpConfig -Name "my-ipaddress" -LoadBalancerBackendAddressPoolsId $backendPool.Id -SubnetId $vnet.Subnets[0].Id -LoadBalancerInboundNatPoolsId $inboundNATPool1.Id

# Attach the virtual network to the IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create the scale set with the config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a><span data-ttu-id="420b0-163">Usare un'immagine di macchina virtuale personalizzata</span><span class="sxs-lookup"><span data-stu-id="420b0-163">Using a custom virtual machine image</span></span>
<span data-ttu-id="420b0-164">Se si sta creando un set di scalabilità da un'immagine personalizzata anziché fare riferimento a un'immagine di macchina virtuale dalla raccolta, il comando _Set AzureRmVmssStorageProfile_ avrà l'aspetto seguente:</span><span class="sxs-lookup"><span data-stu-id="420b0-164">If you are creating a scale set from your own custom image, instead of referencing a virtual machine image from the gallery, the _Set-AzureRmVmssStorageProfile_ command would look like this:</span></span>
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a><span data-ttu-id="420b0-165">Creare un set di scalabilità da un modello</span><span class="sxs-lookup"><span data-stu-id="420b0-165">Create from a template</span></span>

<span data-ttu-id="420b0-166">È possibile distribuire un set di scalabilità di macchine virtuali usando un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="420b0-166">You can deploy a virtual machine scale set by using an Azure Resource Manager template.</span></span> <span data-ttu-id="420b0-167">È possibile creare un modello personalizzato o usarne uno del [repository di modelli](https://azure.microsoft.com/resources/templates/?term=vmss).</span><span class="sxs-lookup"><span data-stu-id="420b0-167">You can create your own template or use one from the [template repository](https://azure.microsoft.com/resources/templates/?term=vmss).</span></span> <span data-ttu-id="420b0-168">Questi modelli possono essere distribuiti direttamente alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="420b0-168">These templates can be deployed directly to your Azure subscription.</span></span>

>[!NOTE]
><span data-ttu-id="420b0-169">Per creare un modello personalizzato, si crea un file di testo JSON.</span><span class="sxs-lookup"><span data-stu-id="420b0-169">To create your own template, you create a JSON text file.</span></span> <span data-ttu-id="420b0-170">Per informazioni generali su come creare e personalizzare un modello, vedere [Modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="420b0-170">For general information about how to create and customize a template, see [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="420b0-171">Un modello di esempio è disponibile [in GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span><span class="sxs-lookup"><span data-stu-id="420b0-171">A sample template is available [on GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span></span> <span data-ttu-id="420b0-172">Per altre informazioni su come creare e usare tale esempio, vedere [Un set di scalabilità a validità minima](.\virtual-machine-scale-sets-mvss-start.md).</span><span class="sxs-lookup"><span data-stu-id="420b0-172">For more information about how to create and use that sample, see [Minimum viable scale set](.\virtual-machine-scale-sets-mvss-start.md).</span></span>

## <a name="create-from-visual-studio"></a><span data-ttu-id="420b0-173">Creare un set di scalabilità da Visual Studio</span><span class="sxs-lookup"><span data-stu-id="420b0-173">Create from Visual Studio</span></span>

<span data-ttu-id="420b0-174">Con Visual Studio, è possibile creare un progetto del gruppo di risorse di Azure e aggiungervi un modello di set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="420b0-174">With Visual Studio, you can create an Azure resource group project and add a virtual machine scale set template to it.</span></span> <span data-ttu-id="420b0-175">È possibile scegliere se si desidera eseguire l'importazione da GitHub o dalla raccolta di applicazioni Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="420b0-175">You can choose whether you want to import it from GitHub or the Azure Web Application Gallery.</span></span> <span data-ttu-id="420b0-176">Viene inoltre generato automaticamente uno script di PowerShell per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="420b0-176">A deployment PowerShell script is also generated for you.</span></span> <span data-ttu-id="420b0-177">Per altre informazioni, vedere [Come creare un set di scalabilità di macchine virtuali con Visual Studio](virtual-machine-scale-sets-vs-create.md).</span><span class="sxs-lookup"><span data-stu-id="420b0-177">For more information, see [How to create a virtual machine scale set with Visual Studio](virtual-machine-scale-sets-vs-create.md).</span></span>

## <a name="create-from-the-azure-portal"></a><span data-ttu-id="420b0-178">Creare un set di scalabilità dal portale di Azure</span><span class="sxs-lookup"><span data-stu-id="420b0-178">Create from the Azure portal</span></span>

<span data-ttu-id="420b0-179">Il portale di Azure costituisce un modo semplice per creare rapidamente un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="420b0-179">The Azure portal provides a convenient way to quickly create a scale set.</span></span> <span data-ttu-id="420b0-180">Per altre informazioni, vedere [Come creare un set di scalabilità di macchine virtuali tramite il portale di Azure](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="420b0-180">For more information, see [How to create a virtual machine scale set with the Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="420b0-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="420b0-181">Next steps</span></span>

<span data-ttu-id="420b0-182">Altre informazioni su [dischi dati](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="420b0-182">Learn more about [data disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="420b0-183">Informazioni su come [gestire le app](virtual-machine-scale-sets-deploy-app.md).</span><span class="sxs-lookup"><span data-stu-id="420b0-183">Learn how to [manage your apps](virtual-machine-scale-sets-deploy-app.md).</span></span>
