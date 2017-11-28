---
title: Appliance virtuale e routing aaaControl utilizzando hello Azure CLI 2.0 | Documenti Microsoft
description: Informazioni su come Appliance virtuale e routing toocontrol utilizzando hello CLI di Azure 2.0.
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
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a><span data-ttu-id="b09fe-103">Creare le route definite dall'utente (UDR) utilizzando hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b09fe-103">Create User-Defined Routes (UDR) using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b09fe-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b09fe-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="b09fe-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b09fe-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="b09fe-106">Modello</span><span class="sxs-lookup"><span data-stu-id="b09fe-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="b09fe-107">PowerShell (distribuzione classica)</span><span class="sxs-lookup"><span data-stu-id="b09fe-107">PowerShell (Classic deployment)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="b09fe-108">Interfaccia della riga di comando (distribuzione classica)</span><span class="sxs-lookup"><span data-stu-id="b09fe-108">CLI (Classic deployment)</span></span>](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="b09fe-109">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="b09fe-109">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="b09fe-110">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="b09fe-110">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="b09fe-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – la CLI per hello classic e risorse Gestione modelli di distribuzione</span><span class="sxs-lookup"><span data-stu-id="b09fe-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="b09fe-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) -la prossima generazione CLI per modello di distribuzione Gestione risorse hello (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="b09fe-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="b09fe-113">Hello esempio CLI di Azure comandi riportati di seguito prevedono un ambiente semplice già creato in base a uno scenario di hello precedente.</span><span class="sxs-lookup"><span data-stu-id="b09fe-113">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="b09fe-114">Se si desidera comandi hello toorun così come sono visualizzati in questo documento, creare innanzitutto ambiente di test di hello distribuendo [questo modello](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), fare clic su **distribuire tooAzure**, sostituire i valori dei parametri predefiniti hello Se necessario e seguire le istruzioni di hello in hello portale.</span><span class="sxs-lookup"><span data-stu-id="b09fe-114">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="b09fe-115">Creare hello UDR per subnet front-end hello</span><span class="sxs-lookup"><span data-stu-id="b09fe-115">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="b09fe-116">tabella di route toocreate hello e route necessarie per la subnet front-end hello a seconda dello scenario hello precedente, seguire i passaggi di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="b09fe-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="b09fe-117">Creare una tabella di route per la subnet front-end hello con hello [-tabella di route az rete creare](/cli/azure/network/route-table#create) comando:</span><span class="sxs-lookup"><span data-stu-id="b09fe-117">Create a route table for hello front-end subnet with hello [az network route-table create](/cli/azure/network/route-table#create) command:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    <span data-ttu-id="b09fe-118">Output:</span><span class="sxs-lookup"><span data-stu-id="b09fe-118">Output:</span></span>

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

2. <span data-ttu-id="b09fe-119">Creare una route che invia tutto il traffico destinato toohello subnet back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) utilizzando hello [creare route della tabella di route di rete az](/cli/azure/network/route-table/route#create) comando:</span><span class="sxs-lookup"><span data-stu-id="b09fe-119">Create a route that sends all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) using hello [az network route-table route create](/cli/azure/network/route-table/route#create) command:</span></span>

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    <span data-ttu-id="b09fe-120">Output:</span><span class="sxs-lookup"><span data-stu-id="b09fe-120">Output:</span></span>

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
    <span data-ttu-id="b09fe-121">Parametri</span><span class="sxs-lookup"><span data-stu-id="b09fe-121">Parameters:</span></span>

    * <span data-ttu-id="b09fe-122">**--route-table-name**.</span><span class="sxs-lookup"><span data-stu-id="b09fe-122">**--route-table-name**.</span></span> <span data-ttu-id="b09fe-123">Nome della tabella di routing hello in cui verrà aggiunti route hello.</span><span class="sxs-lookup"><span data-stu-id="b09fe-123">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="b09fe-124">Per questo scenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="b09fe-124">For our scenario, *UDR-FrontEnd*.</span></span>
    * <span data-ttu-id="b09fe-125">**--address-prefix**.</span><span class="sxs-lookup"><span data-stu-id="b09fe-125">**--address-prefix**.</span></span> <span data-ttu-id="b09fe-126">Prefisso dell'indirizzo per subnet hello in cui i pacchetti sono destinati a.</span><span class="sxs-lookup"><span data-stu-id="b09fe-126">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="b09fe-127">Per questo scenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="b09fe-127">For our scenario, *192.168.2.0/24*.</span></span>
    * <span data-ttu-id="b09fe-128">**--next-hop-type**.</span><span class="sxs-lookup"><span data-stu-id="b09fe-128">**--next-hop-type**.</span></span> <span data-ttu-id="b09fe-129">Tipo di oggetto al quale verrà inviato il traffico.</span><span class="sxs-lookup"><span data-stu-id="b09fe-129">Type of object traffic will be sent to.</span></span> <span data-ttu-id="b09fe-130">I valori possibili sono *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* o *None*.</span><span class="sxs-lookup"><span data-stu-id="b09fe-130">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
    * <span data-ttu-id="b09fe-131">**--next-hop-ip-address**.</span><span class="sxs-lookup"><span data-stu-id="b09fe-131">**--next-hop-ip-address**.</span></span> <span data-ttu-id="b09fe-132">Indirizzo IP per l'hop successivo.</span><span class="sxs-lookup"><span data-stu-id="b09fe-132">IP address for next hop.</span></span> <span data-ttu-id="b09fe-133">Per questo scenario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="b09fe-133">For our scenario, *192.168.0.4*.</span></span>

3. <span data-ttu-id="b09fe-134">Eseguire hello [aggiornare subnet rete virtuale di rete az](/cli/azure/network/vnet/subnet#update) tabella di routing di comandi tooassociate hello creato in precedenza con hello **front-end** subnet:</span><span class="sxs-lookup"><span data-stu-id="b09fe-134">Run hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    <span data-ttu-id="b09fe-135">Output:</span><span class="sxs-lookup"><span data-stu-id="b09fe-135">Output:</span></span>

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

    <span data-ttu-id="b09fe-136">Parametri</span><span class="sxs-lookup"><span data-stu-id="b09fe-136">Parameters:</span></span>
    
    * <span data-ttu-id="b09fe-137">**--vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="b09fe-137">**--vnet-name**.</span></span> <span data-ttu-id="b09fe-138">Nome della rete virtuale in cui si trova subnet hello hello.</span><span class="sxs-lookup"><span data-stu-id="b09fe-138">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="b09fe-139">Per questo scenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="b09fe-139">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="b09fe-140">Creare hello UDR per subnet back-end hello</span><span class="sxs-lookup"><span data-stu-id="b09fe-140">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="b09fe-141">hello toocreate tabella di route e indirizzare necessari per la subnet di back-end hello a seconda dello scenario di hello sopra, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="b09fe-141">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="b09fe-142">Eseguire hello successivo comando toocreate una tabella di route per la subnet di back-end hello:</span><span class="sxs-lookup"><span data-stu-id="b09fe-142">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. <span data-ttu-id="b09fe-143">Eseguire hello successivo comando toocreate una route in toosend tabella di route hello tutto il traffico destinato toohello subnet front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="b09fe-143">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. <span data-ttu-id="b09fe-144">Esecuzione hello seguenti tabella di routing di comandi tooassociate hello con hello **back-end** subnet:</span><span class="sxs-lookup"><span data-stu-id="b09fe-144">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="b09fe-145">Abilitare l'inoltro dell'indirizzo IP su FW1</span><span class="sxs-lookup"><span data-stu-id="b09fe-145">Enable IP forwarding on FW1</span></span>

<span data-ttu-id="b09fe-146">inoltro dell'indirizzo IP nella scheda di rete utilizzata da hello tooenable **FW1**completa hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b09fe-146">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="b09fe-147">Eseguire hello [Mostra scheda di rete az](/cli/azure/network/nic#show) comando con un hello toodisplay filtro JMESPATH corrente **inoltro dell'indirizzo ip enable** valore per **inoltro IP abilitare**.</span><span class="sxs-lookup"><span data-stu-id="b09fe-147">Run hello [az network nic show](/cli/azure/network/nic#show) command with a JMESPATH filter toodisplay hello current **enable-ip-forwarding** value for **Enable IP forwarding**.</span></span> <span data-ttu-id="b09fe-148">Deve essere impostato troppo*false*.</span><span class="sxs-lookup"><span data-stu-id="b09fe-148">It should be set too*false*.</span></span>

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="b09fe-149">Output:</span><span class="sxs-lookup"><span data-stu-id="b09fe-149">Output:</span></span>

        false

2. <span data-ttu-id="b09fe-150">Eseguire hello inoltro dell'indirizzo IP tooenable comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b09fe-150">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    <span data-ttu-id="b09fe-151">È possibile esaminare console toohello con flusso di output hello, o semplicemente nuovamente per hello specifico **enableIpForwarding** valore:</span><span class="sxs-lookup"><span data-stu-id="b09fe-151">You can examine hello output streamed toohello console, or just retest for hello specific **enableIpForwarding** value:</span></span>

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="b09fe-152">Output:</span><span class="sxs-lookup"><span data-stu-id="b09fe-152">Output:</span></span>

        true

    <span data-ttu-id="b09fe-153">Parametri</span><span class="sxs-lookup"><span data-stu-id="b09fe-153">Parameters:</span></span>

    <span data-ttu-id="b09fe-154">**--ip-forwarding**: *true* o *false*.</span><span class="sxs-lookup"><span data-stu-id="b09fe-154">**--ip-forwarding**: *true* or *false*.</span></span>

