---
title: Aprire porte a una VM tramite Azure PowerShell | Documentazione Microsoft
description: Informazioni su come aprire una porta o creare un endpoint alla VM Windows tramite il modello di distribuzione di Azure Resource Manager e Azure PowerShell
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: e818e3b3c707e1471d6f580f8379a277d3575b89
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-open-ports-and-endpoints-to-a-vm-in-azure-using-powershell"></a><span data-ttu-id="8588f-103">Come aprire le porte e gli endpoint in una VM in Azure usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="8588f-103">How to open ports and endpoints to a VM in Azure using PowerShell</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="8588f-104">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="8588f-104">Quick commands</span></span>
<span data-ttu-id="8588f-105">Per creare un gruppo di sicurezza di rete e le regole del controllo di accesso, è necessario che [sia installata la versione più recente di Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="8588f-105">To create a Network Security Group and ACL rules you need [the latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="8588f-106">È possibile anche [eseguire questi passaggi tramite il portale di Azure](nsg-quickstart-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8588f-106">You can also [perform these steps using the Azure portal](nsg-quickstart-portal.md).</span></span>

<span data-ttu-id="8588f-107">Accedere all'account di Azure:</span><span class="sxs-lookup"><span data-stu-id="8588f-107">Log in to your Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="8588f-108">Nell'esempio seguente sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="8588f-108">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="8588f-109">I nomi dei parametri di esempio includono *myResourceGroup*, *myNetworkSecurityGroup* e *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="8588f-109">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="8588f-110">Creare una regola con [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="8588f-110">Create a rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="8588f-111">L'esempio seguente crea una regola denominata *myNetworkSecurityGroupRule* per consentire il traffico *tcp* sulla porta *80*:</span><span class="sxs-lookup"><span data-stu-id="8588f-111">The following example creates a rule named *myNetworkSecurityGroupRule* to allow *tcp* traffic on port *80*:</span></span>

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

<span data-ttu-id="8588f-112">Creare quindi il gruppo di sicurezza di rete con [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) e assegnare la regola HTTP appena creata come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="8588f-112">Next, create your Network Security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) and assign the HTTP rule you just created as follows.</span></span> <span data-ttu-id="8588f-113">L'esempio seguente crea un gruppo di sicurezza di rete denominato *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="8588f-113">The following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

<span data-ttu-id="8588f-114">Ora si assegnerà il gruppo di sicurezza di rete a una subnet.</span><span class="sxs-lookup"><span data-stu-id="8588f-114">Now let's assign your Network Security Group to a subnet.</span></span> <span data-ttu-id="8588f-115">L'esempio seguente assegna una rete virtuale esistente denominata *myVnet* alla variabile *$vnet* con [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="8588f-115">The following example assigns an existing virtual network named *myVnet* to the variable *$vnet* with [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

<span data-ttu-id="8588f-116">Associare il gruppo di sicurezza di rete alla subnet con [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="8588f-116">Associate your Network Security Group with your subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="8588f-117">L'esempio seguente associa la subnet denominata *mySubnet* al gruppo di sicurezza di rete:</span><span class="sxs-lookup"><span data-stu-id="8588f-117">The following example associates the subnet named *mySubnet* with your Network Security Group:</span></span>

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="8588f-118">Infine, aggiornare la rete virtuale con [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) affinché le modifiche abbiano effetto:</span><span class="sxs-lookup"><span data-stu-id="8588f-118">Finally, update your virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) in order for your changes to take effect:</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="8588f-119">Altre informazioni sui gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="8588f-119">More information on Network Security Groups</span></span>
<span data-ttu-id="8588f-120">I comandi rapidi seguenti consentono di rendere operativo il traffico verso la VM.</span><span class="sxs-lookup"><span data-stu-id="8588f-120">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="8588f-121">I gruppi di sicurezza di rete offrono numerose funzionalità efficienti e la necessaria granularità per controllare l'accesso alle risorse.</span><span class="sxs-lookup"><span data-stu-id="8588f-121">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="8588f-122">Per altre informazioni, leggere l'articolo sulla [creazione di un gruppo di sicurezza di rete e di regole dell'elenco di controllo di accesso qui](tutorial-virtual-network.md#manage-internal-traffic).</span><span class="sxs-lookup"><span data-stu-id="8588f-122">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#manage-internal-traffic).</span></span>

<span data-ttu-id="8588f-123">Per le applicazioni Web a disponibilità elevata, è consigliabile inserire le macchine virtuali dietro a un Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="8588f-123">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="8588f-124">Il bilanciamento del carico distribuisce il traffico alle macchine virtuali, con un gruppo di sicurezza di rete che consente di filtrare il traffico.</span><span class="sxs-lookup"><span data-stu-id="8588f-124">The load balancer distributes traffic to VMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="8588f-125">Per altre informazioni, vedere [Come bilanciare il carico per le macchine virtuali di Linux in Azure per creare un'applicazione a disponibilità elevata](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="8588f-125">For more information, see [How to load balance Linux virtual machines in Azure to create a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8588f-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8588f-126">Next steps</span></span>
<span data-ttu-id="8588f-127">In questo esempio viene creata una regola semplice per consentire il traffico HTTP.</span><span class="sxs-lookup"><span data-stu-id="8588f-127">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="8588f-128">È possibile trovare informazioni sulla creazione di ambienti più dettagliati negli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="8588f-128">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="8588f-129">Panoramica di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8588f-129">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="8588f-130">Che cos'è un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="8588f-130">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="8588f-131">Panoramica di Azure Resource Manager per i servizi di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="8588f-131">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

