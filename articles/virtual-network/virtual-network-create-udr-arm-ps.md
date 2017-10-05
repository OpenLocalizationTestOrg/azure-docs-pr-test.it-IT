---
title: Controllare il routing e le appliance virtuali in Azure PowerShell | Microsoft Docs
description: Informazioni su come controllare il routing e i dispositivi virtuali usando PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 9582fdaa-249c-4c98-9618-8c30d496940f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: 3ab24f193c74449ae7414b4ea0675c0aae0211f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-user-defined-routes-udr-using-powershell"></a><span data-ttu-id="2404d-103">Creare route definite dall'utente (UDR) usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="2404d-103">Create User-Defined Routes (UDR) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2404d-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2404d-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="2404d-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="2404d-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="2404d-106">Modello</span><span class="sxs-lookup"><span data-stu-id="2404d-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="2404d-107">PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="2404d-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="2404d-108">Interfaccia della riga di comando (versione classica)</span><span class="sxs-lookup"><span data-stu-id="2404d-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="2404d-109">Prima di iniziare a usare le risorse di Azure, è importante comprendere che Azure al momento offre due modelli di distribuzione, la distribuzione classica e Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2404d-109">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="2404d-110">È importante comprendere i [modelli e strumenti di distribuzione](../azure-resource-manager/resource-manager-deployment-model.md) prima di lavorare con le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2404d-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="2404d-111">È possibile visualizzare la documentazione relativa a diversi strumenti facendo clic sulle schede nella parte superiore di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="2404d-111">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span>
>

<span data-ttu-id="2404d-112">Questo articolo illustra il modello di distribuzione Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="2404d-112">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="2404d-113">È possibile anche [creare route definite dall'utente nel modello di distribuzione classica](virtual-network-create-udr-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2404d-113">You can also [create UDRs in the classic deployment model](virtual-network-create-udr-classic-ps.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="2404d-114">I comandi di esempio PowerShell riportati di seguito prevedono un ambiente semplice già creato in base allo scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="2404d-114">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="2404d-115">Se si desidera eseguire i comandi così come sono visualizzati in questo documento, creare innanzitutto l'ambiente di test distribuendo [questo modello](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), fare clic su **Distribuisci in Azure**, sostituire i valori di parametro predefiniti, se necessario e seguire le istruzioni nel portale.</span><span class="sxs-lookup"><span data-stu-id="2404d-115">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="2404d-116">Creare la route definita dall'utente per la subnet front-end</span><span class="sxs-lookup"><span data-stu-id="2404d-116">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="2404d-117">Per creare la tabella di route e la route necessarie per la subnet front-end in base allo scenario precedente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2404d-117">To create the route table and route needed for the front-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="2404d-118">Creare una route usata per inviare tutto il traffico destinato alla subnet front-end (192.168.2.0/24) da instradare al dispositivo virtuale di rete **FW1** (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="2404d-118">Create a route used to send all traffic destined to the back-end subnet (192.168.2.0/24) to be routed to the **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToBackEnd `
    -AddressPrefix 192.168.2.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="2404d-119">Creare una tabella di route denominata **UDR-FrontEnd** nell'area **westus** contenente la route.</span><span class="sxs-lookup"><span data-stu-id="2404d-119">Create a route table named **UDR-FrontEnd** in the **westus** region that contains the route.</span></span>

    ```powershell
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-FrontEnd -Route $route
    ```

3. <span data-ttu-id="2404d-120">Creare una variabile contenente la rete virtuale in cui si trova la subnet.</span><span class="sxs-lookup"><span data-stu-id="2404d-120">Create a variable that contains the VNet where the subnet is.</span></span> <span data-ttu-id="2404d-121">In questo scenario, la rete virtuale è denominata **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="2404d-121">In our scenario, the VNet is named **TestVNet**.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

4. <span data-ttu-id="2404d-122">Associare la tabella di route creata in precedenza alla subnet **FrontEnd** .</span><span class="sxs-lookup"><span data-stu-id="2404d-122">Associate the route table created above to the **FrontEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -RouteTable $routeTable
    ```

    > [!WARNING]
    > <span data-ttu-id="2404d-123">L'output per il comando precedente mostra il contenuto per l'oggetto di configurazione della rete virtuale, che esiste solo nei computer in cui si esegue PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2404d-123">The output for the command above shows the content for the virtual network configuration object, which only exists on the computer where you are running PowerShell.</span></span> <span data-ttu-id="2404d-124">È necessario eseguire il cmdlet **Set-AzureVirtualNetwork** ,per salvare queste impostazioni in Azure.</span><span class="sxs-lookup"><span data-stu-id="2404d-124">You need to run the **Set-AzureVirtualNetwork** cmdlet to save these settings to Azure.</span></span>
    > 

5. <span data-ttu-id="2404d-125">Salvare la nuova configurazione di subnet in Azure.</span><span class="sxs-lookup"><span data-stu-id="2404d-125">Save the new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="2404d-126">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="2404d-126">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                                ...,
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              },
                                ...
                            ]    

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="2404d-127">Creare la route definita dall'utente per la subnet back-end</span><span class="sxs-lookup"><span data-stu-id="2404d-127">Create the UDR for the back-end subnet</span></span>

<span data-ttu-id="2404d-128">Per creare la tabella di route e la route necessarie per la subnet back-end in base allo scenario precedente, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="2404d-128">To create the route table and route needed for the back-end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="2404d-129">Creare una route usata per inviare tutto il traffico destinato alla subnet front-end (192.168.1.0/24) da instradare al dispositivo virtuale di rete **FW1** (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="2404d-129">Create a route used to send all traffic destined to the front-end subnet (192.168.1.0/24) to be routed to the **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="2404d-130">Creare una tabella di route denominata **UDR-BackEnd** nell'area **uswest** contenente la route creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2404d-130">Create a route table named **UDR-BackEnd** in the **uswest** region that contains the route created above.</span></span>

    ```
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-BackEnd -Route $route
    ```

3. <span data-ttu-id="2404d-131">Associare la tabella di route creata in precedenza alla subnet **BackEnd** .</span><span class="sxs-lookup"><span data-stu-id="2404d-131">Associate the route table created above to the **BackEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd `
    -AddressPrefix 192.168.2.0/24 -RouteTable $routeTable
    ```

4. <span data-ttu-id="2404d-132">Salvare la nuova configurazione di subnet in Azure.</span><span class="sxs-lookup"><span data-stu-id="2404d-132">Save the new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="2404d-133">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="2404d-133">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              ...,
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BacEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="2404d-134">Abilitare l'inoltro dell'indirizzo IP su FW1</span><span class="sxs-lookup"><span data-stu-id="2404d-134">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="2404d-135">Per abilitare l'inoltro dell'indirizzo IP nella scheda di interfaccia di rete usata da **FW1**, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="2404d-135">To enable IP forwarding in the NIC used by **FW1**, follow the steps below.</span></span>

1. <span data-ttu-id="2404d-136">Creare una variabile contenente le impostazioni per la scheda di interfaccia di rete usata da FW1.</span><span class="sxs-lookup"><span data-stu-id="2404d-136">Create a variable that contains the settings for the NIC used by FW1.</span></span> <span data-ttu-id="2404d-137">In questo scenario, la scheda di interfaccia di rete è denominata **NICFW1**.</span><span class="sxs-lookup"><span data-stu-id="2404d-137">In our scenario, the NIC is named **NICFW1**.</span></span>

    ```powershell
    $nicfw1 = Get-AzureRmNetworkInterface -ResourceGroupName TestRG -Name NICFW1
    ```

2. <span data-ttu-id="2404d-138">Attivare l'inoltro dell'indirizzo IP e salvare le impostazioni della scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="2404d-138">Enable IP forwarding, and save the NIC settings.</span></span>

    ```powershell
    $nicfw1.EnableIPForwarding = 1
    Set-AzureRmNetworkInterface -NetworkInterface $nicfw1
    ```
   
    <span data-ttu-id="2404d-139">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="2404d-139">Expected output:</span></span>
   
        Name                 : NICFW1
        ResourceGroupName    : TestRG
        Location             : westus
        Id                   : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1
        Etag                 : W/"[Id]"
        ProvisioningState    : Succeeded
        Tags                 : 
                               Name         Value                  
                               ===========  =======================
                               displayName  NetworkInterfaces - DMZ
   
        VirtualMachine       : {
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/FW1"
                               }
        IpConfigurations     : [
                                 {
                                   "Name": "ipconfig1",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1/ipConfigurations/ipconfig1",
                                   "PrivateIpAddress": "192.168.0.4",
                                   "PrivateIpAllocationMethod": "Static",
                                   "Subnet": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/DMZ"
                                   },
                                   "PublicIpAddress": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPFW1"
                                   },
                                   "LoadBalancerBackendAddressPools": [],
                                   "LoadBalancerInboundNatRules": [],
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
        DnsSettings          : {
                                 "DnsServers": [],
                                 "AppliedDnsServers": [],
                                 "InternalDnsNameLabel": null,
                                 "InternalFqdn": null
                               }
        EnableIPForwarding   : True
        NetworkSecurityGroup : null
        Primary              : True

