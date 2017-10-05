---
title: Controllare il routing in una rete virtuale di Azure - PowerShell - Modello di distribuzione classica | Documentazione Microsoft
description: Informazioni su come controllare il routing in reti virtuali usando PowerShell | Classico
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: e9564d223cb85529f1fa97bc398d35c6debcedae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a><span data-ttu-id="227c4-103">Controllare il routing e usare dispositivi virtuali di rete (distribuzione classica) mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="227c4-103">Control routing and use virtual appliances (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="227c4-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="227c4-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="227c4-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="227c4-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="227c4-106">Modello</span><span class="sxs-lookup"><span data-stu-id="227c4-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="227c4-107">PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="227c4-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="227c4-108">Interfaccia della riga di comando (versione classica)</span><span class="sxs-lookup"><span data-stu-id="227c4-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="227c4-109">Prima di iniziare a usare le risorse di Azure, è importante comprendere che Azure al momento offre due modelli di distribuzione, la distribuzione classica e Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="227c4-109">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="227c4-110">È importante comprendere i [modelli e strumenti di distribuzione](../azure-resource-manager/resource-manager-deployment-model.md) prima di lavorare con le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="227c4-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="227c4-111">È possibile visualizzare la documentazione relativa ai diversi strumenti selezionando un'opzione nella parte superiore di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="227c4-111">You can view the documentation for different tools by selecting an option at the top of this article.</span></span> <span data-ttu-id="227c4-112">In questo articolo viene illustrato il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="227c4-112">This article covers the classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="227c4-113">I comandi di esempio di Azure PowerShell riportati di seguito prevedono un ambiente semplice già creato in base allo scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="227c4-113">The sample Azure PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="227c4-114">Se si desidera eseguire i comandi illustrati in questo documento, creare l'ambiente descritto nella pagina relativa alla [creazione di una rete virtuale (classica) mediante PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="227c4-114">If you want to run the commands as they are displayed in this document, create the environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="227c4-115">Creare la route definita dall'utente per la subnet front-end</span><span class="sxs-lookup"><span data-stu-id="227c4-115">Create the UDR for the front end subnet</span></span>
<span data-ttu-id="227c4-116">Per creare la tabella di route e la route necessarie per la subnet front-end in base allo scenario precedente, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="227c4-116">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="227c4-117">Eseguire il comando seguente per creare una tabella di route per la subnet front-end:</span><span class="sxs-lookup"><span data-stu-id="227c4-117">Run the following command to create a route table for the front-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. <span data-ttu-id="227c4-118">Eseguire il comando seguente per creare una route nella tabella della route creata in precedenza per inviare tutto il traffico destinato alla subnet back-end (192.168.2.0/24) alla VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="227c4-118">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="227c4-119">Eseguire il comando seguente per associare la tabella di route creata in precedenza alla subnet **FrontEnd**:</span><span class="sxs-lookup"><span data-stu-id="227c4-119">Run the following command to associate the route table with the **FrontEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="227c4-120">Creare la route definita dall'utente per la subnet back-end</span><span class="sxs-lookup"><span data-stu-id="227c4-120">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="227c4-121">Per creare la tabella di route e la route necessarie per la subnet back-end in base allo scenario precedente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="227c4-121">To create the route table and route needed for the back end subnet based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="227c4-122">Per creare una tabella di route per la subnet back-end, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="227c4-122">Run the following command to create a route table for the back-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. <span data-ttu-id="227c4-123">Eseguire il comando seguente per creare una route nella tabella della route creata in precedenza per inviare tutto il traffico destinato alla subnet front-end (192.168.1.0/24) alla VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="227c4-123">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="227c4-124">Eseguire il comando seguente per associare la tabella di route creata in precedenza alla subnet **BackEnd**:</span><span class="sxs-lookup"><span data-stu-id="227c4-124">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-the-fw1-vm"></a><span data-ttu-id="227c4-125">Abilitare l'inoltro dell'indirizzo IP sulla VM FW1</span><span class="sxs-lookup"><span data-stu-id="227c4-125">Enable IP forwarding on the FW1 VM</span></span>

<span data-ttu-id="227c4-126">Per abilitare l'inoltro dell'indirizzo IP nella macchina virtuale FW1, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="227c4-126">To enable IP forwarding in the FW1 VM, complete the following steps:</span></span>

1. <span data-ttu-id="227c4-127">Per verificare lo stato dell'inoltro dell'indirizzo IP, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="227c4-127">Run the following command to check the status of IP forwarding:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. <span data-ttu-id="227c4-128">Per abilitare l'inoltro dell'indirizzo IP per la macchina virtuale *FW1*, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="227c4-128">Run the following command to enable IP forwarding for the *FW1* VM:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
