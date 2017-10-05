---
title: Creare una rete virtuale - Azure PowerShell | Documentazione Microsoft
description: Informazioni su come creare una rete virtuale mediante PowerShell.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a31f4f12-54ee-4339-b968-1a8097ca77d3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e7072ddf51570d46578111e2e392e3cbea53f2aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-powershell"></a><span data-ttu-id="08d94-103">Creare una rete virtuale usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="08d94-103">Create a virtual network using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="08d94-104">Azure offre due modelli di distribuzione, ovvero Azure Resource Manager e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="08d94-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="08d94-105">Microsoft consiglia di creare le risorse tramite il modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="08d94-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="08d94-106">Per altre informazioni sulle differenze tra i due modelli, leggere l'articolo [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) (Informazioni sui modelli di distribuzione di Azure).</span><span class="sxs-lookup"><span data-stu-id="08d94-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="08d94-107">Questo articolo illustra come creare una rete virtuale tramite il modello di distribuzione Resource Manager usando PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08d94-107">This article explains how to create a VNet through the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="08d94-108">È anche possibile creare una rete virtuale tramite Resource Manager usando altri strumenti oppure tramite il modello di distribuzione classica selezionando un'opzione diversa dall'elenco seguente:</span><span class="sxs-lookup"><span data-stu-id="08d94-108">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="08d94-109">Portale</span><span class="sxs-lookup"><span data-stu-id="08d94-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="08d94-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="08d94-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="08d94-111">CLI</span><span class="sxs-lookup"><span data-stu-id="08d94-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="08d94-112">Modello</span><span class="sxs-lookup"><span data-stu-id="08d94-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="08d94-113">Portale (versione classica)</span><span class="sxs-lookup"><span data-stu-id="08d94-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="08d94-114">PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="08d94-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="08d94-115">Interfaccia della riga di comando (versione classica)</span><span class="sxs-lookup"><span data-stu-id="08d94-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="08d94-116">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="08d94-116">Create a virtual network</span></span>

<span data-ttu-id="08d94-117">Per creare una rete virtuale usando PowerShell, completare i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="08d94-117">To create a virtual network using PowerShell, complete the following steps:</span></span>

1. <span data-ttu-id="08d94-118">Installare e configurare Azure PowerShell seguendo i passaggi descritti nell'articolo [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="08d94-118">Install and configure Azure PowerShell, by following the steps in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>

2. <span data-ttu-id="08d94-119">Se necessario, creare un nuovo gruppo di risorse, come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="08d94-119">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="08d94-120">Per questo scenario, creare un gruppo di risorse denominato *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="08d94-120">For this scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="08d94-121">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="08d94-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="08d94-122">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="08d94-122">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. <span data-ttu-id="08d94-123">Creare una nuova rete virtuale denominata *TestVNet*:</span><span class="sxs-lookup"><span data-stu-id="08d94-123">Create a new VNet named *TestVNet*:</span></span>

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    <span data-ttu-id="08d94-124">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="08d94-124">Expected output:</span></span>

        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                   : W/"[Id]"
        ProvisioningState          : Succeeded
        Tags                       : 
        AddressSpace               : {
                                   "AddressPrefixes": [
                                     "192.168.0.0/16"
                                   ]
                                  }
        DhcpOptions                : {}
        Subnets                    : []
        VirtualNetworkPeerings     : []
4. <span data-ttu-id="08d94-125">Archiviare l'oggetto di rete virtuale in una variabile:</span><span class="sxs-lookup"><span data-stu-id="08d94-125">Store the virtual network object in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > <span data-ttu-id="08d94-126">È possibile combinare i passaggi 3 e 4 eseguendo `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span><span class="sxs-lookup"><span data-stu-id="08d94-126">You can combine steps 3 and 4 by running `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span></span>
   > 

5. <span data-ttu-id="08d94-127">Aggiungere una subnet alla nuova variabile di rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="08d94-127">Add a subnet to the new VNet variable:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    <span data-ttu-id="08d94-128">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="08d94-128">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {}
        Subnets             : [
                                  {
                                    "Name": "FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24"
                                  }
                                ]
        VirtualNetworkPeerings     : []

6. <span data-ttu-id="08d94-129">Ripetere il passaggio 5 riportato in precedenza per ogni subnet che si desidera creare.</span><span class="sxs-lookup"><span data-stu-id="08d94-129">Repeat step 5 above for each subnet you want to create.</span></span> <span data-ttu-id="08d94-130">Il comando seguente crea la subnet *BackEnd* per lo scenario:</span><span class="sxs-lookup"><span data-stu-id="08d94-130">The following command creates the *BackEnd* subnet for the scenario:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. <span data-ttu-id="08d94-131">Quando si crea una subnet, questa rimane solo nella variabile locale usata per recuperare la rete virtuale creata nel passaggio 4.</span><span class="sxs-lookup"><span data-stu-id="08d94-131">Although you create subnets, they currently only exist in the local variable used to retrieve the VNet you create in step 4 above.</span></span> <span data-ttu-id="08d94-132">Per salvare le modifiche in Azure, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="08d94-132">To save the changes to Azure, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    <span data-ttu-id="08d94-133">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="08d94-133">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {
                                  "DnsServers": []
                                }
        Subnets               : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  },
                                  {
                                    "Name": "BackEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                    "AddressPrefix": "192.168.2.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  }
                                ]
        VirtualNetworkPeerings : []

## <a name="next-steps"></a><span data-ttu-id="08d94-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="08d94-134">Next steps</span></span>

<span data-ttu-id="08d94-135">Leggere le informazioni su come connettere:</span><span class="sxs-lookup"><span data-stu-id="08d94-135">Learn how to connect:</span></span>

- <span data-ttu-id="08d94-136">Una macchina virtuale (VM) a una rete virtuale nell'articolo [Creare una VM Windows](../virtual-machines/virtual-machines-windows-ps-create.md).</span><span class="sxs-lookup"><span data-stu-id="08d94-136">A virtual machine (VM) to a virtual network by reading the [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span></span> <span data-ttu-id="08d94-137">Anziché creare una rete virtuale e una subnet, come illustrato nelle procedure degli articoli, è possibile selezionare una rete virtuale e una subnet esistenti a cui connettere una VM.</span><span class="sxs-lookup"><span data-stu-id="08d94-137">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="08d94-138">La rete virtuale ad altre reti virtuali nell'articolo [Connettere reti virtuali](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="08d94-138">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="08d94-139">La rete virtuale a una rete locale tramite una rete privata virtuale (VPN) da sito a sito o il circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="08d94-139">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="08d94-140">negli articoli [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) (Connettere una rete virtuale a una rete locale tramite una VPN da sito a sito) e [Collegare una rete virtuale a un circuito ExpressRoute](../expressroute/expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="08d94-140">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
