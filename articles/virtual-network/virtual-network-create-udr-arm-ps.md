---
title: Accessori aaaControl di routing e virtuali in Azure - PowerShell | Documenti Microsoft
description: Informazioni su come Appliance virtuale e routing toocontrol tramite PowerShell.
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
ms.openlocfilehash: b7b8717529eb2cd8b1d28b8ab9c6e21159d14882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-powershell"></a><span data-ttu-id="3c856-103">Creare route definite dall'utente (UDR) usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c856-103">Create User-Defined Routes (UDR) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c856-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c856-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="3c856-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="3c856-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="3c856-106">Modello</span><span class="sxs-lookup"><span data-stu-id="3c856-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="3c856-107">PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="3c856-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="3c856-108">Interfaccia della riga di comando (versione classica)</span><span class="sxs-lookup"><span data-stu-id="3c856-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="3c856-109">Prima di lavorare con le risorse di Azure, è importante toounderstand che Azure ha due modelli di distribuzione: Gestione risorse di Azure e classica.</span><span class="sxs-lookup"><span data-stu-id="3c856-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="3c856-110">È importante comprendere i [modelli e strumenti di distribuzione](../azure-resource-manager/resource-manager-deployment-model.md) prima di lavorare con le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c856-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="3c856-111">È possibile visualizzare la documentazione di hello per diversi strumenti facendo clic sulle schede hello nella parte superiore di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="3c856-111">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span>
>

<span data-ttu-id="3c856-112">Questo articolo descrive il modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="3c856-112">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="3c856-113">È anche possibile [creare UDRs nel modello di distribuzione classica hello](virtual-network-create-udr-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3c856-113">You can also [create UDRs in hello classic deployment model](virtual-network-create-udr-classic-ps.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="3c856-114">esempio Hello PowerShell comandi riportati di seguito prevedono un ambiente semplice già creato in base hello scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="3c856-114">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="3c856-115">Se si desidera comandi hello toorun così come sono visualizzati in questo documento, creare innanzitutto ambiente di test di hello distribuendo [questo modello](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), fare clic su **distribuire tooAzure**, sostituire i valori dei parametri predefiniti hello Se necessario e seguire le istruzioni di hello in hello portale.</span><span class="sxs-lookup"><span data-stu-id="3c856-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="3c856-116">Creare hello UDR per subnet front-end hello</span><span class="sxs-lookup"><span data-stu-id="3c856-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="3c856-117">tabella di route toocreate hello e route necessarie per la subnet front-end hello a seconda dello scenario di hello sopra, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3c856-117">toocreate hello route table and route needed for hello front-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="3c856-118">Creare un toosend route utilizzato tutto il traffico destinato toohello subnet back-end (192.168.2.0/24) toobe indirizzato toohello **FW1** appliance virtuale (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="3c856-118">Create a route used toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToBackEnd `
    -AddressPrefix 192.168.2.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="3c856-119">Creare una tabella di route denominata **UDR-FrontEnd** in hello **westus** area che contiene la route hello.</span><span class="sxs-lookup"><span data-stu-id="3c856-119">Create a route table named **UDR-FrontEnd** in hello **westus** region that contains hello route.</span></span>

    ```powershell
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-FrontEnd -Route $route
    ```

3. <span data-ttu-id="3c856-120">Creare una variabile che contiene una rete virtuale in cui è subnet hello hello.</span><span class="sxs-lookup"><span data-stu-id="3c856-120">Create a variable that contains hello VNet where hello subnet is.</span></span> <span data-ttu-id="3c856-121">In questo scenario, hello tra reti virtuali sono denominato **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="3c856-121">In our scenario, hello VNet is named **TestVNet**.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

4. <span data-ttu-id="3c856-122">Tabella di route associano hello creata in precedenza toohello **front-end** subnet.</span><span class="sxs-lookup"><span data-stu-id="3c856-122">Associate hello route table created above toohello **FrontEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -RouteTable $routeTable
    ```

    > [!WARNING]
    > <span data-ttu-id="3c856-123">output di Hello per comando hello precedente mostra il contenuto di hello per l'oggetto configurazione di rete virtuale di hello che esiste solo nel computer di hello in cui si esegue PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c856-123">hello output for hello command above shows hello content for hello virtual network configuration object, which only exists on hello computer where you are running PowerShell.</span></span> <span data-ttu-id="3c856-124">È necessario hello toorun **Set AzureVirtualNetwork** toosave cmdlet tooAzure queste impostazioni.</span><span class="sxs-lookup"><span data-stu-id="3c856-124">You need toorun hello **Set-AzureVirtualNetwork** cmdlet toosave these settings tooAzure.</span></span>
    > 

5. <span data-ttu-id="3c856-125">Salvare la nuova configurazione subnet di hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="3c856-125">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="3c856-126">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="3c856-126">Expected output:</span></span>
   
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

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="3c856-127">Creare hello UDR per subnet back-end hello</span><span class="sxs-lookup"><span data-stu-id="3c856-127">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="3c856-128">tabella di route toocreate hello e route necessarie per la subnet di back-end hello a seconda dello scenario hello precedente, seguire i passaggi di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="3c856-128">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="3c856-129">Creare un toosend route utilizzato tutto il traffico destinato toohello subnet front-end (192.168.1.0/24) toobe indirizzato toohello **FW1** appliance virtuale (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="3c856-129">Create a route used toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="3c856-130">Creare una tabella di route denominata **back-end di UDR** in hello **uswest** area che contiene la route hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3c856-130">Create a route table named **UDR-BackEnd** in hello **uswest** region that contains hello route created above.</span></span>

    ```
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-BackEnd -Route $route
    ```

3. <span data-ttu-id="3c856-131">Tabella di route associano hello creata in precedenza toohello **back-end** subnet.</span><span class="sxs-lookup"><span data-stu-id="3c856-131">Associate hello route table created above toohello **BackEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd `
    -AddressPrefix 192.168.2.0/24 -RouteTable $routeTable
    ```

4. <span data-ttu-id="3c856-132">Salvare la nuova configurazione subnet di hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="3c856-132">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="3c856-133">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="3c856-133">Expected output:</span></span>
   
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

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="3c856-134">Abilitare l'inoltro dell'indirizzo IP su FW1</span><span class="sxs-lookup"><span data-stu-id="3c856-134">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="3c856-135">inoltro dell'indirizzo IP nella scheda di rete utilizzata da hello tooenable **FW1**, attenersi alla procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="3c856-135">tooenable IP forwarding in hello NIC used by **FW1**, follow hello steps below.</span></span>

1. <span data-ttu-id="3c856-136">Creare una variabile che contiene le impostazioni di hello per scheda di rete utilizzata da FW1 hello.</span><span class="sxs-lookup"><span data-stu-id="3c856-136">Create a variable that contains hello settings for hello NIC used by FW1.</span></span> <span data-ttu-id="3c856-137">In questo scenario, hello NIC denominato **NICFW1**.</span><span class="sxs-lookup"><span data-stu-id="3c856-137">In our scenario, hello NIC is named **NICFW1**.</span></span>

    ```powershell
    $nicfw1 = Get-AzureRmNetworkInterface -ResourceGroupName TestRG -Name NICFW1
    ```

2. <span data-ttu-id="3c856-138">Attivare l'inoltro IP e salvare le impostazioni di hello NIC.</span><span class="sxs-lookup"><span data-stu-id="3c856-138">Enable IP forwarding, and save hello NIC settings.</span></span>

    ```powershell
    $nicfw1.EnableIPForwarding = 1
    Set-AzureRmNetworkInterface -NetworkInterface $nicfw1
    ```
   
    <span data-ttu-id="3c856-139">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="3c856-139">Expected output:</span></span>
   
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

