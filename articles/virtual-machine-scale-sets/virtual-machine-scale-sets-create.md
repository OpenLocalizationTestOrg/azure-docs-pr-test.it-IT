---
title: imposta una scala di macchina virtuale di Azure aaaCreate | Documenti Microsoft
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
ms.openlocfilehash: 73de25c1dd2424e64655b3accfea848926e72f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-a-virtual-machine-scale-set"></a><span data-ttu-id="daa85-103">Creare e distribuire un set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="daa85-103">Create and deploy a virtual machine scale set</span></span>
<span data-ttu-id="daa85-104">Set di scalabilità di macchine virtuali semplificano automaticamente toodeploy e gestire macchine virtuali identiche come un set.</span><span class="sxs-lookup"><span data-stu-id="daa85-104">Virtual machine scale sets make it easy for you toodeploy and manage identical virtual machines as a set.</span></span> <span data-ttu-id="daa85-105">I set di scalabilità offrono un livello di calcolo scalabile e personalizzabile per applicazioni con iperscalabilità e supportano le immagini della piattaforma Windows, le immagini della piattaforma Linux, le immagini personalizzate e le estensioni.</span><span class="sxs-lookup"><span data-stu-id="daa85-105">Scale sets provide a highly scalable and customizable compute layer for hyperscale applications, and they support Windows platform images, Linux platform images, custom images, and extensions.</span></span> <span data-ttu-id="daa85-106">Per altre informazioni sui set di scalabilità, vedere [Set di scalabilità di macchine virtuali](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="daa85-106">For more information about scale sets, see [Virtual machine scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="daa85-107">Questa esercitazione viene illustrato come toocreate un scalabilità della macchina virtuale impostare **senza** utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="daa85-107">This tutorial shows you how toocreate a virtual machine scale set **without** using hello Azure portal.</span></span> <span data-ttu-id="daa85-108">Per informazioni su come toouse hello portale di Azure, vedere [come toocreate impostato di scalabilità di macchine virtuali con hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="daa85-108">For information about how toouse hello Azure portal, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

>[!NOTE]
><span data-ttu-id="daa85-109">Per altre informazioni sulle risorse di Azure Resource Manager, vedere [Confronto tra distribuzione di Azure Resource Manager e classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="daa85-109">For more information about Azure Resource Manager resources, see [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="daa85-110">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="daa85-110">Sign in tooAzure</span></span>

<span data-ttu-id="daa85-111">Se si utilizza l'interfaccia CLI di Azure 2.0 o Azure PowerShell toocreate una scala impostata, è innanzitutto necessario toosign nella sottoscrizione tooyour.</span><span class="sxs-lookup"><span data-stu-id="daa85-111">If you're using Azure CLI 2.0 or Azure PowerShell toocreate a scale set, you first need toosign in tooyour subscription.</span></span>

<span data-ttu-id="daa85-112">Per ulteriori informazioni su come tooinstall, configurare e accesso tooAzure con CLI di Azure o PowerShell, vedere [Introduzione a Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) o [Introduzione ai cmdlet di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="daa85-112">For more information about how tooinstall, set up, and sign in tooAzure with Azure CLI or PowerShell, see [Getting Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md) or [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

```azurecli
az login
```

```powershell
Login-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="daa85-113">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="daa85-113">Create a resource group</span></span>

<span data-ttu-id="daa85-114">È necessario innanzitutto toocreate è associato un gruppo di risorse che il set di scalabilità della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="daa85-114">You first need toocreate a resource group that hello virtual machine scale set is associated with.</span></span>

```azurecli
az group create --location westus2 --name MyResourceGroup1
```

```powershell
New-AzureRmResourceGroup -Location westus2 -Name MyResourceGroup1
```

## <a name="create-from-azure-cli"></a><span data-ttu-id="daa85-115">Creare un set di scalabilità dall'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="daa85-115">Create from Azure CLI</span></span>

<span data-ttu-id="daa85-116">Con l'interfaccia della riga di comando di Azure, è possibile creare facilmente un set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="daa85-116">With Azure CLI, you can create a virtual machine scale set with minimal effort.</span></span> <span data-ttu-id="daa85-117">Se omessi, i valori predefiniti vengono forniti automaticamente.</span><span class="sxs-lookup"><span data-stu-id="daa85-117">If you omit default values, they are provided for you.</span></span> <span data-ttu-id="daa85-118">Ad esempio, se non si specificano le informazioni relative alla rete virtuale, ne verrà creata una automaticamente.</span><span class="sxs-lookup"><span data-stu-id="daa85-118">For example, if you don't specify any virtual network information, a virtual network is created for you.</span></span> <span data-ttu-id="daa85-119">Se si omette le seguenti parti hello, essi vengono creati automaticamente:</span><span class="sxs-lookup"><span data-stu-id="daa85-119">If you omit hello following parts, they are created for you:</span></span> 
- <span data-ttu-id="daa85-120">Un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="daa85-120">A load balancer</span></span>
- <span data-ttu-id="daa85-121">Una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="daa85-121">A virtual network</span></span>
- <span data-ttu-id="daa85-122">Un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="daa85-122">A public IP address</span></span>

<span data-ttu-id="daa85-123">Quando scelta hello immagine di macchina virtuale che si desidera toouse nel set di scalabilità della macchina virtuale hello, sono disponibili alcune opzioni:</span><span class="sxs-lookup"><span data-stu-id="daa85-123">When choosing hello virtual machine image that you want toouse on hello virtual machine scale set, you have a few choices:</span></span>

- <span data-ttu-id="daa85-124">URN</span><span class="sxs-lookup"><span data-stu-id="daa85-124">URN</span></span>  
<span data-ttu-id="daa85-125">Identificatore Hello di una risorsa:</span><span class="sxs-lookup"><span data-stu-id="daa85-125">hello identifier of a resource:</span></span>  
<span data-ttu-id="daa85-126">**Win2012R2Datacenter**</span><span class="sxs-lookup"><span data-stu-id="daa85-126">**Win2012R2Datacenter**</span></span>

- <span data-ttu-id="daa85-127">Alias URN</span><span class="sxs-lookup"><span data-stu-id="daa85-127">URN alias</span></span>  
<span data-ttu-id="daa85-128">nome descrittivo di Hello di un URN:</span><span class="sxs-lookup"><span data-stu-id="daa85-128">hello friendly name of a URN:</span></span>  
<span data-ttu-id="daa85-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span><span class="sxs-lookup"><span data-stu-id="daa85-129">**MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest**</span></span>

- <span data-ttu-id="daa85-130">ID risorsa personalizzata</span><span class="sxs-lookup"><span data-stu-id="daa85-130">Custom resource id</span></span>  
<span data-ttu-id="daa85-131">Hello percorso tooan risorse di Azure:</span><span class="sxs-lookup"><span data-stu-id="daa85-131">hello path tooan Azure resource:</span></span>  
<span data-ttu-id="daa85-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span><span class="sxs-lookup"><span data-stu-id="daa85-132">**/subscriptions/subscription-guid/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/images/MyImage**</span></span>

- <span data-ttu-id="daa85-133">Risorsa Web</span><span class="sxs-lookup"><span data-stu-id="daa85-133">Web resource</span></span>  
<span data-ttu-id="daa85-134">Hello percorso tooan URI HTTP:</span><span class="sxs-lookup"><span data-stu-id="daa85-134">hello path tooan HTTP URI:</span></span>  
<span data-ttu-id="daa85-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span><span class="sxs-lookup"><span data-stu-id="daa85-135">**http://contoso.blob.core.windows.net/vhds/osdiskimage.vhd**</span></span>

>[!TIP]
><span data-ttu-id="daa85-136">È possibile ottenere un elenco di immagini disponibili con `az vm image list`.</span><span class="sxs-lookup"><span data-stu-id="daa85-136">You can get a list of available images with `az vm image list`.</span></span>

<span data-ttu-id="daa85-137">toocreate set di scalabilità di macchine virtuali, è necessario specificare i seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="daa85-137">toocreate a virtual machine scale set, you must specify hello following:</span></span>

- <span data-ttu-id="daa85-138">Gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="daa85-138">Resource group</span></span> 
- <span data-ttu-id="daa85-139">Nome</span><span class="sxs-lookup"><span data-stu-id="daa85-139">Name</span></span>
- <span data-ttu-id="daa85-140">Immagine del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="daa85-140">Operating system image</span></span>
- <span data-ttu-id="daa85-141">Informazioni di autenticazione</span><span class="sxs-lookup"><span data-stu-id="daa85-141">Authentication information</span></span> 
 
<span data-ttu-id="daa85-142">Hello di esempio seguente crea un set di scalabilità della macchina virtuale di base (questa operazione potrebbe richiedere alcuni minuti).</span><span class="sxs-lookup"><span data-stu-id="daa85-142">hello following example creates a basic virtual machine scale set (this step might take a few minutes).</span></span>

```azurecli
az vmss create --resource-group MyResourceGroup1 --name MyScaleSet --image UbuntuLTS --authentication-type password --admin-username azureuser --admin-password P@ssw0rd!
```

<span data-ttu-id="daa85-143">Una volta terminato il comando hello si avranno ora la scalabilità della macchina virtuale creato.</span><span class="sxs-lookup"><span data-stu-id="daa85-143">Once hello command finishes you will now have your virtual machine scale set created.</span></span> <span data-ttu-id="daa85-144">Potrebbe essere necessario l'indirizzo IP di hello tooget della macchina virtuale hello in modo che sia possibile connettersi tooit.</span><span class="sxs-lookup"><span data-stu-id="daa85-144">You may need tooget hello IP address of hello virtual machine so that you can connect tooit.</span></span> <span data-ttu-id="daa85-145">È possibile ottenere numerose informazioni sui diversi sulla macchina virtuale hello (incluso l'indirizzo IP hello) con hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="daa85-145">You can get a lot of different information about hello virtual machine (including hello IP address) with hello following command.</span></span> 

```azurecli
az vmss list-instance-connection-info --resource-group MyResourceGroup1 --name MyScaleSet
```

## <a name="create-from-powershell"></a><span data-ttu-id="daa85-146">Creare un set di scalabilità da PowerShell</span><span class="sxs-lookup"><span data-stu-id="daa85-146">Create from PowerShell</span></span>

<span data-ttu-id="daa85-147">PowerShell è più complicato toouse di CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="daa85-147">PowerShell is more complicated toouse than Azure CLI.</span></span> <span data-ttu-id="daa85-148">Mentre l'interfaccia della riga di comando di Azure fornisce automaticamente le opzioni predefinite per le risorse di rete (bilanciamenti del carico, indirizzi IP, reti virtuali), questo non avviene in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="daa85-148">While Azure CLI provides defaults for networking-related resources (such as load balancers, IP addresses, and virtual networks), PowerShell does not.</span></span> <span data-ttu-id="daa85-149">Anche fare riferimento a un'immagine con PowerShell è leggermente più complicato.</span><span class="sxs-lookup"><span data-stu-id="daa85-149">Referencing an image with PowerShell is a slightly more complicated too.</span></span> <span data-ttu-id="daa85-150">È possibile ottenere le immagini con hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="daa85-150">You can get images with hello following cmdlets:</span></span>

1. <span data-ttu-id="daa85-151">Get-AzureRMVMImagePublisher</span><span class="sxs-lookup"><span data-stu-id="daa85-151">Get-AzureRMVMImagePublisher</span></span>
2. <span data-ttu-id="daa85-152">Get-AzureRMVMImageOffer</span><span class="sxs-lookup"><span data-stu-id="daa85-152">Get-AzureRMVMImageOffer</span></span>
3. <span data-ttu-id="daa85-153">Get-AzureRmVMImageSku</span><span class="sxs-lookup"><span data-stu-id="daa85-153">Get-AzureRmVMImageSku</span></span>

<span data-ttu-id="daa85-154">può essere inoltrato tramite pipe Hello cmdlet funzionano in sequenza.</span><span class="sxs-lookup"><span data-stu-id="daa85-154">hello cmdlets work can be piped in sequence.</span></span> <span data-ttu-id="daa85-155">Di seguito è riportato un esempio di come tooget tutte le immagini per hello **Stati Uniti occidentali 2** area con un server di pubblicazione con nome hello **microsoft** in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="daa85-155">Here is an example of how tooget all images for hello **West US 2** region with a publisher that has hello name **microsoft** in it.</span></span>

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

<span data-ttu-id="daa85-156">flusso di lavoro di Hello per la creazione di un set di scalabilità della macchina virtuale è indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="daa85-156">hello workflow for creating a virtual machine scale set is as follows:</span></span>

1. <span data-ttu-id="daa85-157">Creare un oggetto di configurazione che contiene informazioni sui set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="daa85-157">Create a config object that holds information about hello scale set.</span></span>
2. <span data-ttu-id="daa85-158">Riferimento hello del sistema operativo immagine di base.</span><span class="sxs-lookup"><span data-stu-id="daa85-158">Reference hello base OS image.</span></span>
3. <span data-ttu-id="daa85-159">Configurare le impostazioni del sistema operativo hello: autenticazione, il prefisso del nome di macchina virtuale e utente/passaggio.</span><span class="sxs-lookup"><span data-stu-id="daa85-159">Configure hello operating system settings: authentication, VM name prefix, and user/pass.</span></span>
4. <span data-ttu-id="daa85-160">Configurare le impostazioni di rete.</span><span class="sxs-lookup"><span data-stu-id="daa85-160">Configure networking.</span></span>
5. <span data-ttu-id="daa85-161">Creare set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="daa85-161">Create hello scale set.</span></span>

<span data-ttu-id="daa85-162">Questo esempio consente di creare un set di scalabilità di base a due istanze per un computer con installato Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="daa85-162">This example creates a basic two-instance scale set for a computer that has Windows Server 2016 installed.</span></span>

```powershell
# Resource group name from above
$rg = "MyResourceGroup1"
$location = "WestUS2"

# Create a config object
$vmssConfig = New-AzureRmVmssConfig -Location $location -SkuCapacity 2 -SkuName Standard_A0  -UpgradePolicyMode Automatic

# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig -ImageReferencePublisher MicrosoftWindowsServer -ImageReferenceOffer WindowsServer -ImageReferenceSku 2016-Datacenter -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig -AdminUsername azureuser -AdminPassword P@ssw0rd! -ComputerNamePrefix myvmssvm

# Create hello virtual network resources

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

# Attach hello virtual network toohello IP object
Add-AzureRmVmssNetworkInterfaceConfiguration -VirtualMachineScaleSet $vmssConfig -Name "network-config" -Primary $true -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss -ResourceGroupName $rg -Name "MyScaleSet1" -VirtualMachineScaleSet $vmssConfig
```

### <a name="using-a-custom-virtual-machine-image"></a><span data-ttu-id="daa85-163">Usare un'immagine di macchina virtuale personalizzata</span><span class="sxs-lookup"><span data-stu-id="daa85-163">Using a custom virtual machine image</span></span>
<span data-ttu-id="daa85-164">Se si sta creando una scala impostato da un'immagine personalizzata, anziché fare riferimento a un'immagine di macchina virtuale da raccolta hello, hello _Set AzureRmVmssStorageProfile_ comando è analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="daa85-164">If you are creating a scale set from your own custom image, instead of referencing a virtual machine image from hello gallery, hello _Set-AzureRmVmssStorageProfile_ command would look like this:</span></span>
```PowerShell
Set-AzureRmVmssStorageProfile -OsDiskCreateOption FromImage -ManagedDisk PremiumLRS -OsDiskCaching "None" -OsDiskOsType Linux -ImageReferenceId (Get-AzureRmImage -ImageName $VMImage -ResourceGroupName $rg).id
```

## <a name="create-from-a-template"></a><span data-ttu-id="daa85-165">Creare un set di scalabilità da un modello</span><span class="sxs-lookup"><span data-stu-id="daa85-165">Create from a template</span></span>

<span data-ttu-id="daa85-166">È possibile distribuire un set di scalabilità di macchine virtuali usando un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="daa85-166">You can deploy a virtual machine scale set by using an Azure Resource Manager template.</span></span> <span data-ttu-id="daa85-167">È possibile creare un modello personalizzato o usarne uno dal hello [repository modello](https://azure.microsoft.com/resources/templates/?term=vmss).</span><span class="sxs-lookup"><span data-stu-id="daa85-167">You can create your own template or use one from hello [template repository](https://azure.microsoft.com/resources/templates/?term=vmss).</span></span> <span data-ttu-id="daa85-168">Questi modelli possono essere distribuiti direttamente tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="daa85-168">These templates can be deployed directly tooyour Azure subscription.</span></span>

>[!NOTE]
><span data-ttu-id="daa85-169">toocreate un modello personalizzato, si crea un file di testo JSON.</span><span class="sxs-lookup"><span data-stu-id="daa85-169">toocreate your own template, you create a JSON text file.</span></span> <span data-ttu-id="daa85-170">Per informazioni generali su come toocreate e personalizzare un modello, vedere [modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="daa85-170">For general information about how toocreate and customize a template, see [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="daa85-171">Un modello di esempio è disponibile [in GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span><span class="sxs-lookup"><span data-stu-id="daa85-171">A sample template is available [on GitHub](https://github.com/gatneil/mvss/tree/minimum-viable-scale-set).</span></span> <span data-ttu-id="daa85-172">Per ulteriori informazioni su come toocreate e usare tale esempio, vedere [set vitali di scala minimo](.\virtual-machine-scale-sets-mvss-start.md).</span><span class="sxs-lookup"><span data-stu-id="daa85-172">For more information about how toocreate and use that sample, see [Minimum viable scale set](.\virtual-machine-scale-sets-mvss-start.md).</span></span>

## <a name="create-from-visual-studio"></a><span data-ttu-id="daa85-173">Creare un set di scalabilità da Visual Studio</span><span class="sxs-lookup"><span data-stu-id="daa85-173">Create from Visual Studio</span></span>

<span data-ttu-id="daa85-174">Con Visual Studio, è possibile creare un progetto di gruppo di risorse di Azure e aggiungere che un scalabilità della macchina virtuale impostata tooit modello.</span><span class="sxs-lookup"><span data-stu-id="daa85-174">With Visual Studio, you can create an Azure resource group project and add a virtual machine scale set template tooit.</span></span> <span data-ttu-id="daa85-175">È possibile scegliere se si desidera tooimport da GitHub o hello raccolta applicazioni Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="daa85-175">You can choose whether you want tooimport it from GitHub or hello Azure Web Application Gallery.</span></span> <span data-ttu-id="daa85-176">Viene inoltre generato automaticamente uno script di PowerShell per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="daa85-176">A deployment PowerShell script is also generated for you.</span></span> <span data-ttu-id="daa85-177">Per ulteriori informazioni, vedere [come toocreate set di scalabilità di macchine virtuali con Visual Studio](virtual-machine-scale-sets-vs-create.md).</span><span class="sxs-lookup"><span data-stu-id="daa85-177">For more information, see [How toocreate a virtual machine scale set with Visual Studio](virtual-machine-scale-sets-vs-create.md).</span></span>

## <a name="create-from-hello-azure-portal"></a><span data-ttu-id="daa85-178">Il nome di hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="daa85-178">Create from hello Azure portal</span></span>

<span data-ttu-id="daa85-179">Hello portale di Azure fornisce un modo pratico tooquickly creare un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="daa85-179">hello Azure portal provides a convenient way tooquickly create a scale set.</span></span> <span data-ttu-id="daa85-180">Per ulteriori informazioni, vedere [come toocreate impostato di scalabilità di macchine virtuali con hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span><span class="sxs-lookup"><span data-stu-id="daa85-180">For more information, see [How toocreate a virtual machine scale set with hello Azure portal](virtual-machine-scale-sets-portal-create.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="daa85-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="daa85-181">Next steps</span></span>

<span data-ttu-id="daa85-182">Altre informazioni su [dischi dati](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="daa85-182">Learn more about [data disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

<span data-ttu-id="daa85-183">Informazioni su come troppo[gestire le app](virtual-machine-scale-sets-deploy-app.md).</span><span class="sxs-lookup"><span data-stu-id="daa85-183">Learn how too[manage your apps](virtual-machine-scale-sets-deploy-app.md).</span></span>
