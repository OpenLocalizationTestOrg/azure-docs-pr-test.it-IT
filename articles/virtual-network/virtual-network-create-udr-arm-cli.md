---
title: Controllare il routing e i dispositivi virtuali usando l'interfaccia della riga di comando di Azure 2.0 | Microsoft Docs
description: Informazioni su come controllare il routing e i dispositivi virtuali mediante l'interfaccia della riga di comando di Azure 2.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: e5d9519998346619093f443b740c8904283f76e8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-user-defined-routes-udr-using-the-azure-cli-20"></a><span data-ttu-id="4f33a-103">Creare route definite dall'utente con l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4f33a-103">Create User-Defined Routes (UDR) using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4f33a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f33a-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="4f33a-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="4f33a-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="4f33a-106">Modello</span><span class="sxs-lookup"><span data-stu-id="4f33a-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="4f33a-107">PowerShell (distribuzione classica)</span><span class="sxs-lookup"><span data-stu-id="4f33a-107">PowerShell (Classic deployment)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="4f33a-108">Interfaccia della riga di comando (distribuzione classica)</span><span class="sxs-lookup"><span data-stu-id="4f33a-108">CLI (Classic deployment)</span></span>](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="4f33a-109">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="4f33a-109">CLI versions to complete the task</span></span> 

<span data-ttu-id="4f33a-110">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="4f33a-110">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="4f33a-111">[Interfaccia della riga di comando di Azure 1.0](virtual-network-create-udr-arm-cli-nodejs.md): l'interfaccia della riga di comando per i modelli di distribuzione classici e di gestione delle risorse</span><span class="sxs-lookup"><span data-stu-id="4f33a-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="4f33a-112">[Interfaccia della riga di comando di Azure 2.0](#Create-the-UDR-for-the-front-end-subnet): interfaccia avanzata per il modello di distribuzione di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="4f33a-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="4f33a-113">I comandi di esempio dell'interfaccia della riga di comando di Azure riportati di seguito prevedono un ambiente semplice già creato in base allo scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="4f33a-113">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="4f33a-114">Se si desidera eseguire i comandi così come sono visualizzati in questo documento, creare innanzitutto l'ambiente di test distribuendo [questo modello](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), fare clic su **Distribuisci in Azure**, sostituire i valori di parametro predefiniti, se necessario e seguire le istruzioni nel portale.</span><span class="sxs-lookup"><span data-stu-id="4f33a-114">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>


## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="4f33a-115">Creare la route definita dall'utente per la subnet front-end</span><span class="sxs-lookup"><span data-stu-id="4f33a-115">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="4f33a-116">Per creare la tabella di route e la route necessarie per la subnet front-end in base allo scenario precedente, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="4f33a-116">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="4f33a-117">Creare una tabella di route per la subnet front-end con il comando [az network route-table create](/cli/azure/network/route-table#create):</span><span class="sxs-lookup"><span data-stu-id="4f33a-117">Create a route table for the front-end subnet with the [az network route-table create](/cli/azure/network/route-table#create) command:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    <span data-ttu-id="4f33a-118">Output:</span><span class="sxs-lookup"><span data-stu-id="4f33a-118">Output:</span></span>

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. <span data-ttu-id="4f33a-119">Creare una route che invia tutto il traffico destinato alla subnet back-end (192.168.2.0/24) alla VM **FW1** (192.168.0.4) usando il comando [az network route-table route create](/cli/azure/network/route-table/route#create):</span><span class="sxs-lookup"><span data-stu-id="4f33a-119">Create a route that sends all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4) using the [az network route-table route create](/cli/azure/network/route-table/route#create) command:</span></span>

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    <span data-ttu-id="4f33a-120">Output:</span><span class="sxs-lookup"><span data-stu-id="4f33a-120">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    <span data-ttu-id="4f33a-121">Parametri</span><span class="sxs-lookup"><span data-stu-id="4f33a-121">Parameters:</span></span>

    * <span data-ttu-id="4f33a-122">**--route-table-name**.</span><span class="sxs-lookup"><span data-stu-id="4f33a-122">**--route-table-name**.</span></span> <span data-ttu-id="4f33a-123">Nome della tabella di route in cui verrà aggiunta la route.</span><span class="sxs-lookup"><span data-stu-id="4f33a-123">Name of the route table where the route will be added.</span></span> <span data-ttu-id="4f33a-124">Per questo scenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="4f33a-124">For our scenario, *UDR-FrontEnd*.</span></span>
    * <span data-ttu-id="4f33a-125">**--address-prefix**.</span><span class="sxs-lookup"><span data-stu-id="4f33a-125">**--address-prefix**.</span></span> <span data-ttu-id="4f33a-126">Prefisso di indirizzo della subnet alla quale sono destinati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="4f33a-126">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="4f33a-127">Per questo scenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="4f33a-127">For our scenario, *192.168.2.0/24*.</span></span>
    * <span data-ttu-id="4f33a-128">**--next-hop-type**.</span><span class="sxs-lookup"><span data-stu-id="4f33a-128">**--next-hop-type**.</span></span> <span data-ttu-id="4f33a-129">Tipo di oggetto al quale verrà inviato il traffico.</span><span class="sxs-lookup"><span data-stu-id="4f33a-129">Type of object traffic will be sent to.</span></span> <span data-ttu-id="4f33a-130">I valori possibili sono *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* o *None*.</span><span class="sxs-lookup"><span data-stu-id="4f33a-130">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
    * <span data-ttu-id="4f33a-131">**--next-hop-ip-address**.</span><span class="sxs-lookup"><span data-stu-id="4f33a-131">**--next-hop-ip-address**.</span></span> <span data-ttu-id="4f33a-132">Indirizzo IP per l'hop successivo.</span><span class="sxs-lookup"><span data-stu-id="4f33a-132">IP address for next hop.</span></span> <span data-ttu-id="4f33a-133">Per questo scenario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="4f33a-133">For our scenario, *192.168.0.4*.</span></span>

3. <span data-ttu-id="4f33a-134">Eseguire il comando [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) per associare la tabella di route creata in precedenza alla subnet **FrontEnd**:</span><span class="sxs-lookup"><span data-stu-id="4f33a-134">Run the [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command to associate the route table created above with the **FrontEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    <span data-ttu-id="4f33a-135">Output:</span><span class="sxs-lookup"><span data-stu-id="4f33a-135">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    <span data-ttu-id="4f33a-136">Parametri</span><span class="sxs-lookup"><span data-stu-id="4f33a-136">Parameters:</span></span>
    
    * <span data-ttu-id="4f33a-137">**--vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="4f33a-137">**--vnet-name**.</span></span> <span data-ttu-id="4f33a-138">Nome della rete virtuale in cui si trova la subnet.</span><span class="sxs-lookup"><span data-stu-id="4f33a-138">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="4f33a-139">Per questo scenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="4f33a-139">For our scenario, *TestVNet*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="4f33a-140">Creare la route definita dall'utente per la subnet back-end</span><span class="sxs-lookup"><span data-stu-id="4f33a-140">Create the UDR for the back-end subnet</span></span>

<span data-ttu-id="4f33a-141">Per creare la tabella di route e la route necessarie per la subnet back-end in base allo scenario precedente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4f33a-141">To create the route table and route needed for the back-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="4f33a-142">Per creare una tabella di route per la subnet back-end, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4f33a-142">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. <span data-ttu-id="4f33a-143">Eseguire il comando seguente per creare una route nella tabella della route creata in precedenza per inviare tutto il traffico destinato alla subnet front-end (192.168.1.0/24) alla VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="4f33a-143">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. <span data-ttu-id="4f33a-144">Eseguire il comando seguente per associare la tabella di route creata in precedenza alla subnet **BackEnd**:</span><span class="sxs-lookup"><span data-stu-id="4f33a-144">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="4f33a-145">Abilitare l'inoltro dell'indirizzo IP su FW1</span><span class="sxs-lookup"><span data-stu-id="4f33a-145">Enable IP forwarding on FW1</span></span>

<span data-ttu-id="4f33a-146">Per abilitare l'inoltro dell'indirizzo IP nella scheda di interfaccia di rete usata da **FW1**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4f33a-146">To enable IP forwarding in the NIC used by **FW1**, complete the following steps:</span></span>

1. <span data-ttu-id="4f33a-147">Eseguire il comando [az network nic show](/cli/azure/network/nic#show) con un filtro JMESPATH per visualizzare il valore **enable-ip-forwarding** corrente per **Enable IP forwarding** (Abilita inoltro IP).</span><span class="sxs-lookup"><span data-stu-id="4f33a-147">Run the [az network nic show](/cli/azure/network/nic#show) command with a JMESPATH filter to display the current **enable-ip-forwarding** value for **Enable IP forwarding**.</span></span> <span data-ttu-id="4f33a-148">Il valore deve essere impostato su *false*.</span><span class="sxs-lookup"><span data-stu-id="4f33a-148">It should be set to *false*.</span></span>

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="4f33a-149">Output:</span><span class="sxs-lookup"><span data-stu-id="4f33a-149">Output:</span></span>

        false

2. <span data-ttu-id="4f33a-150">Eseguire il comando seguente per abilitare l'inoltro dell'indirizzo IP:</span><span class="sxs-lookup"><span data-stu-id="4f33a-150">Run the following command to enable IP forwarding:</span></span>

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    <span data-ttu-id="4f33a-151">È possibile esaminare l'output trasferito alla console o semplicemente ripetere il test per lo specifico valore **enableIpForwarding**:</span><span class="sxs-lookup"><span data-stu-id="4f33a-151">You can examine the output streamed to the console, or just retest for the specific **enableIpForwarding** value:</span></span>

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="4f33a-152">Output:</span><span class="sxs-lookup"><span data-stu-id="4f33a-152">Output:</span></span>

        true

    <span data-ttu-id="4f33a-153">Parametri</span><span class="sxs-lookup"><span data-stu-id="4f33a-153">Parameters:</span></span>

    <span data-ttu-id="4f33a-154">**--ip-forwarding**: *true* o *false*.</span><span class="sxs-lookup"><span data-stu-id="4f33a-154">**--ip-forwarding**: *true* or *false*.</span></span>

