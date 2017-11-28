---
title: una rete virtuale - Azure PowerShell aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate un virtuale di rete con PowerShell.
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
ms.openlocfilehash: 8d6e395a77f71de9f94b6304b05450e46b47544f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-powershell"></a><span data-ttu-id="27e67-103">Creare una rete virtuale usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="27e67-103">Create a virtual network using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="27e67-104">Azure offre due modelli di distribuzione, ovvero Azure Resource Manager e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="27e67-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="27e67-105">Si consiglia di creare risorse modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="27e67-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="27e67-106">altre informazioni sulle toolearn hello le differenze tra hello due modelli, leggere hello [modelli di distribuzione Azure comprendere](../azure-resource-manager/resource-manager-deployment-model.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="27e67-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="27e67-107">In questo articolo viene illustrato come una rete virtuale tramite la distribuzione di gestione risorse di hello toocreate modello tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27e67-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="27e67-108">È anche possibile creare una rete virtuale tramite Gestione risorse di usare altri strumenti o creare una rete virtuale tramite il modello di distribuzione classica hello selezionando un'opzione diversa da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="27e67-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="27e67-109">Portale</span><span class="sxs-lookup"><span data-stu-id="27e67-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="27e67-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="27e67-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="27e67-111">CLI</span><span class="sxs-lookup"><span data-stu-id="27e67-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="27e67-112">Modello</span><span class="sxs-lookup"><span data-stu-id="27e67-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="27e67-113">Portale (versione classica)</span><span class="sxs-lookup"><span data-stu-id="27e67-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="27e67-114">PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="27e67-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="27e67-115">Interfaccia della riga di comando (versione classica)</span><span class="sxs-lookup"><span data-stu-id="27e67-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="27e67-116">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="27e67-116">Create a virtual network</span></span>

<span data-ttu-id="27e67-117">toocreate i passaggi da una rete virtuale usando PowerShell, hello completo seguente:</span><span class="sxs-lookup"><span data-stu-id="27e67-117">toocreate a virtual network using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="27e67-118">Installare e configurare Azure PowerShell, seguendo i passaggi hello hello [come tooInstall e configurare Azure PowerShell](/powershell/azure/overview) articolo.</span><span class="sxs-lookup"><span data-stu-id="27e67-118">Install and configure Azure PowerShell, by following hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>

2. <span data-ttu-id="27e67-119">Se necessario, creare un nuovo gruppo di risorse, come mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="27e67-119">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="27e67-120">Per questo scenario, creare un gruppo di risorse denominato *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="27e67-120">For this scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="27e67-121">Per altre informazioni sui gruppi di risorse, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="27e67-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="27e67-122">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="27e67-122">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. <span data-ttu-id="27e67-123">Creare una nuova rete virtuale denominata *TestVNet*:</span><span class="sxs-lookup"><span data-stu-id="27e67-123">Create a new VNet named *TestVNet*:</span></span>

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    <span data-ttu-id="27e67-124">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="27e67-124">Expected output:</span></span>

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
4. <span data-ttu-id="27e67-125">Oggetto di rete virtuale archivio hello in una variabile:</span><span class="sxs-lookup"><span data-stu-id="27e67-125">Store hello virtual network object in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > <span data-ttu-id="27e67-126">È possibile combinare i passaggi 3 e 4 eseguendo `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span><span class="sxs-lookup"><span data-stu-id="27e67-126">You can combine steps 3 and 4 by running `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span></span>
   > 

5. <span data-ttu-id="27e67-127">Aggiungere una subnet toohello nuova variabile di rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="27e67-127">Add a subnet toohello new VNet variable:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    <span data-ttu-id="27e67-128">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="27e67-128">Expected output:</span></span>
   
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

6. <span data-ttu-id="27e67-129">Ripetere il passaggio 5 riportato sopra per ogni subnet desiderate toocreate.</span><span class="sxs-lookup"><span data-stu-id="27e67-129">Repeat step 5 above for each subnet you want toocreate.</span></span> <span data-ttu-id="27e67-130">il comando seguente Hello crea hello *back-end* subnet per uno scenario di hello:</span><span class="sxs-lookup"><span data-stu-id="27e67-130">hello following command creates hello *BackEnd* subnet for hello scenario:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. <span data-ttu-id="27e67-131">Anche se si crea una subnet, sono attualmente presenti in hello tooretrieve di utilizzata variabile locale hello rete virtuale creato nel passaggio 4 riportato sopra.</span><span class="sxs-lookup"><span data-stu-id="27e67-131">Although you create subnets, they currently only exist in hello local variable used tooretrieve hello VNet you create in step 4 above.</span></span> <span data-ttu-id="27e67-132">toosave hello modifiche tooAzure, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="27e67-132">toosave hello changes tooAzure, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    <span data-ttu-id="27e67-133">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="27e67-133">Expected output:</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="27e67-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="27e67-134">Next steps</span></span>

<span data-ttu-id="27e67-135">Informazioni su come tooconnect:</span><span class="sxs-lookup"><span data-stu-id="27e67-135">Learn how tooconnect:</span></span>

- <span data-ttu-id="27e67-136">Una rete virtuale tooa di macchina virtuale (VM) leggendo hello [creare una macchina virtuale Windows](../virtual-machines/virtual-machines-windows-ps-create.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="27e67-136">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span></span> <span data-ttu-id="27e67-137">Anziché creare una rete virtuale e subnet nei passaggi hello degli articoli hello, è possibile selezionare una rete virtuale esistente e subnet tooconnect una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="27e67-137">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="27e67-138">Hello reti virtuali di rete virtuale tooother leggendo hello [connettere reti virtuali](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="27e67-138">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="27e67-139">rete locale tooan rete virtuale Hello utilizza una rete privata virtuale (VPN) da sito a sito o un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="27e67-139">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="27e67-140">Ulteriori informazioni, leggere hello [connettere una rete locale tooan di rete virtuale tramite una VPN site-to-site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [collegare un circuito ExpressRoute di tooan rete virtuale](../expressroute/expressroute-howto-linkvnet-arm.md) articoli.</span><span class="sxs-lookup"><span data-stu-id="27e67-140">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
