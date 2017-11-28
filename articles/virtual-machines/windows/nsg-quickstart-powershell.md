---
title: aaaOpen porte tooa VM con Azure PowerShell | Documenti Microsoft
description: "Informazioni su come tooopen una porta / creare una macchina virtuale Windows di tooyour endpoint tramite la modalità di distribuzione di gestione risorse di Azure hello e PowerShell di Azure"
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
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a><span data-ttu-id="e5f00-103">Come tooopen tooa di porte e gli endpoint di macchina virtuale in Azure tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5f00-103">How tooopen ports and endpoints tooa VM in Azure using PowerShell</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="e5f00-104">Comandi rapidi</span><span class="sxs-lookup"><span data-stu-id="e5f00-104">Quick commands</span></span>
<span data-ttu-id="e5f00-105">Gruppo di sicurezza di rete toocreate e delle regole ACL è necessario [più recente di Azure PowerShell installata hello](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="e5f00-105">toocreate a Network Security Group and ACL rules you need [hello latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="e5f00-106">È anche possibile [eseguire questi passaggi tramite il portale di Azure hello](nsg-quickstart-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e5f00-106">You can also [perform these steps using hello Azure portal](nsg-quickstart-portal.md).</span></span>

<span data-ttu-id="e5f00-107">Accedi tooyour account di Azure:</span><span class="sxs-lookup"><span data-stu-id="e5f00-107">Log in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="e5f00-108">In hello negli esempi seguenti, sostituire i nomi dei parametri di esempio con i valori desiderati.</span><span class="sxs-lookup"><span data-stu-id="e5f00-108">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="e5f00-109">I nomi dei parametri di esempio includono *myResourceGroup*, *myNetworkSecurityGroup* e *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="e5f00-109">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="e5f00-110">Creare una regola con [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="e5f00-110">Create a rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="e5f00-111">esempio Hello crea una regola denominata *myNetworkSecurityGroupRule* tooallow *tcp* il traffico sulla porta *80*:</span><span class="sxs-lookup"><span data-stu-id="e5f00-111">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow *tcp* traffic on port *80*:</span></span>

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

<span data-ttu-id="e5f00-112">Successivamente, creare il gruppo di sicurezza di rete con [New AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) e assegnare hello HTTP regola appena creata come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="e5f00-112">Next, create your Network Security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) and assign hello HTTP rule you just created as follows.</span></span> <span data-ttu-id="e5f00-113">esempio Hello crea un gruppo di sicurezza di rete denominata *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="e5f00-113">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

<span data-ttu-id="e5f00-114">Ora si assegnare la subnet tooa il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="e5f00-114">Now let's assign your Network Security Group tooa subnet.</span></span> <span data-ttu-id="e5f00-115">esempio Hello assegna una rete virtuale esistente denominata *myVnet* toohello variabile *$vnet* con [Get AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="e5f00-115">hello following example assigns an existing virtual network named *myVnet* toohello variable *$vnet* with [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

<span data-ttu-id="e5f00-116">Associare il gruppo di sicurezza di rete alla subnet con [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="e5f00-116">Associate your Network Security Group with your subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="e5f00-117">esempio Hello associa subnet hello denominata *mySubnet* con il gruppo di sicurezza di rete:</span><span class="sxs-lookup"><span data-stu-id="e5f00-117">hello following example associates hello subnet named *mySubnet* with your Network Security Group:</span></span>

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="e5f00-118">Infine, aggiornare la rete virtuale con [Set AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) affinché l'effetto di tootake modifiche:</span><span class="sxs-lookup"><span data-stu-id="e5f00-118">Finally, update your virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) in order for your changes tootake effect:</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="e5f00-119">Altre informazioni sui gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="e5f00-119">More information on Network Security Groups</span></span>
<span data-ttu-id="e5f00-120">Hello rapido comandi consentono di tooget backup e in esecuzione con traffico propagazione tooyour macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e5f00-120">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="e5f00-121">Gruppi di sicurezza di rete forniscono numerose funzionalità eccellenti e granularità per il controllo tooyour di accedere alle risorse.</span><span class="sxs-lookup"><span data-stu-id="e5f00-121">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="e5f00-122">Per altre informazioni, leggere l'articolo sulla [creazione di un gruppo di sicurezza di rete e di regole dell'elenco di controllo di accesso qui](tutorial-virtual-network.md#manage-internal-traffic).</span><span class="sxs-lookup"><span data-stu-id="e5f00-122">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#manage-internal-traffic).</span></span>

<span data-ttu-id="e5f00-123">Per le applicazioni Web a disponibilità elevata, è consigliabile inserire le macchine virtuali dietro a un Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="e5f00-123">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="e5f00-124">bilanciamento del carico di Hello distribuisce il traffico tooVMs, con un gruppo di sicurezza di rete che consente di filtrare il traffico.</span><span class="sxs-lookup"><span data-stu-id="e5f00-124">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="e5f00-125">Per ulteriori informazioni, vedere [come macchine saldo tooload virtuali Linux in Azure toocreate applicazioni a disponibilità elevata](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="e5f00-125">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5f00-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e5f00-126">Next steps</span></span>
<span data-ttu-id="e5f00-127">In questo esempio è stato creato il traffico HTTP tooallow una semplice regola.</span><span class="sxs-lookup"><span data-stu-id="e5f00-127">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="e5f00-128">È possibile trovare informazioni sulla creazione di ambienti più dettagliati in hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="e5f00-128">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="e5f00-129">Panoramica di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e5f00-129">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="e5f00-130">Che cos'è un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="e5f00-130">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="e5f00-131">Panoramica di Azure Resource Manager per i servizi di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="e5f00-131">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

