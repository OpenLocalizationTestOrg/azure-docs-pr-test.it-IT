---
title: routing aaaControl classica una rete virtuale di Azure - PowerShell - | Documenti Microsoft
description: Informazioni su come toocontrol routing in reti virtuali mediante PowerShell | Classica
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
ms.openlocfilehash: 36edf263fb434d5fb13310d4324da20e57f016a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a><span data-ttu-id="2fcc8-103">Controllare il routing e usare dispositivi virtuali di rete (distribuzione classica) mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fcc8-103">Control routing and use virtual appliances (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2fcc8-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fcc8-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="2fcc8-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="2fcc8-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="2fcc8-106">Modello</span><span class="sxs-lookup"><span data-stu-id="2fcc8-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="2fcc8-107">PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="2fcc8-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="2fcc8-108">Interfaccia della riga di comando (versione classica)</span><span class="sxs-lookup"><span data-stu-id="2fcc8-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="2fcc8-109">Prima di lavorare con le risorse di Azure, è importante toounderstand che Azure ha due modelli di distribuzione: Gestione risorse di Azure e classica.</span><span class="sxs-lookup"><span data-stu-id="2fcc8-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="2fcc8-110">È importante comprendere i [modelli e strumenti di distribuzione](../azure-resource-manager/resource-manager-deployment-model.md) prima di lavorare con le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2fcc8-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="2fcc8-111">È possibile visualizzare la documentazione di hello per diversi strumenti selezionando un'opzione nella parte superiore di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="2fcc8-111">You can view hello documentation for different tools by selecting an option at hello top of this article.</span></span> <span data-ttu-id="2fcc8-112">Questo articolo descrive il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="2fcc8-112">This article covers hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="2fcc8-113">esempio Hello Azure PowerShell comandi riportati di seguito prevedono un ambiente semplice già creato in base hello scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="2fcc8-113">hello sample Azure PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="2fcc8-114">Se si desidera comandi hello toorun così come sono visualizzati in questo documento, creare nell'ambiente di hello [creare una rete virtuale (versione classica) con PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2fcc8-114">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="2fcc8-115">Creare hello UDR per subnet front-end hello</span><span class="sxs-lookup"><span data-stu-id="2fcc8-115">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="2fcc8-116">tabella di route toocreate hello e route necessarie per la subnet front-end hello a seconda dello scenario hello precedente, seguire i passaggi di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="2fcc8-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="2fcc8-117">Eseguire hello successivo comando toocreate una tabella di route per la subnet front-end hello:</span><span class="sxs-lookup"><span data-stu-id="2fcc8-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. <span data-ttu-id="2fcc8-118">Eseguire hello successivo comando toocreate una route in toosend tabella di route hello tutto il traffico destinato toohello subnet back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="2fcc8-118">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="2fcc8-119">Esecuzione hello seguenti tabella di routing di comandi tooassociate hello con hello **front-end** subnet:</span><span class="sxs-lookup"><span data-stu-id="2fcc8-119">Run hello following command tooassociate hello route table with hello **FrontEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="2fcc8-120">Creare hello UDR per subnet back-end hello</span><span class="sxs-lookup"><span data-stu-id="2fcc8-120">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="2fcc8-121">tabella di route toocreate hello e route necessarie per il backup di hello terminare subnet in base a uno scenario di hello, completare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2fcc8-121">toocreate hello route table and route needed for hello back end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="2fcc8-122">Eseguire hello successivo comando toocreate una tabella di route per la subnet di back-end hello:</span><span class="sxs-lookup"><span data-stu-id="2fcc8-122">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. <span data-ttu-id="2fcc8-123">Eseguire hello successivo comando toocreate una route in toosend tabella di route hello tutto il traffico destinato toohello subnet front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="2fcc8-123">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="2fcc8-124">Esecuzione hello seguenti tabella di routing di comandi tooassociate hello con hello **back-end** subnet:</span><span class="sxs-lookup"><span data-stu-id="2fcc8-124">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a><span data-ttu-id="2fcc8-125">Attivare l'inoltro IP in hello FW1 VM</span><span class="sxs-lookup"><span data-stu-id="2fcc8-125">Enable IP forwarding on hello FW1 VM</span></span>

<span data-ttu-id="2fcc8-126">inoltro dell'indirizzo IP tooenable in hello FW1 VM, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2fcc8-126">tooenable IP forwarding in hello FW1 VM, complete hello following steps:</span></span>

1. <span data-ttu-id="2fcc8-127">Eseguire hello seguente lo stato del comando toocheck hello dell'inoltro IP:</span><span class="sxs-lookup"><span data-stu-id="2fcc8-127">Run hello following command toocheck hello status of IP forwarding:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. <span data-ttu-id="2fcc8-128">Comando che segue hello esecuzione tooenable inoltro dell'indirizzo IP per hello *FW1* VM:</span><span class="sxs-lookup"><span data-stu-id="2fcc8-128">Run hello following command tooenable IP forwarding for hello *FW1* VM:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
