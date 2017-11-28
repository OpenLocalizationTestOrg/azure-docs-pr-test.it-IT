---
title: Appliance virtuale e routing aaaControl utilizzando hello Azure CLI 1.0 | Documenti Microsoft
description: Informazioni su come Appliance virtuale e routing toocontrol utilizzando hello Azure CLI 1.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/18/2017
ms.author: jdial
ms.openlocfilehash: 1c8a552d949521fa554880c00405e65fa47a8162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-10"></a><span data-ttu-id="d14b1-103">Creare le route definite dall'utente (UDR) utilizzando hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d14b1-103">Create User-Defined Routes (UDR) using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d14b1-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d14b1-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="d14b1-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="d14b1-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="d14b1-106">Modello</span><span class="sxs-lookup"><span data-stu-id="d14b1-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="d14b1-107">PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="d14b1-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="d14b1-108">Interfaccia della riga di comando (versione classica)</span><span class="sxs-lookup"><span data-stu-id="d14b1-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="d14b1-109">Creare routing personalizzato e Appliance virtuali utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="d14b1-109">Create custom routing and virtual appliances using hello Azure CLI.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="d14b1-110">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="d14b1-110">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="d14b1-111">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="d14b1-111">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="d14b1-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="d14b1-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="d14b1-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="d14b1-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="d14b1-114">Hello esempio CLI di Azure comandi riportati di seguito prevedono un ambiente semplice già creato in base a uno scenario di hello precedente.</span><span class="sxs-lookup"><span data-stu-id="d14b1-114">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="d14b1-115">Se si desidera comandi hello toorun così come sono visualizzati in questo documento, creare innanzitutto ambiente di test di hello distribuendo [questo modello](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), fare clic su **distribuire tooAzure**, sostituire i valori dei parametri predefiniti hello Se necessario e seguire le istruzioni di hello in hello portale.</span><span class="sxs-lookup"><span data-stu-id="d14b1-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="d14b1-116">Creare hello UDR per subnet front-end hello</span><span class="sxs-lookup"><span data-stu-id="d14b1-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="d14b1-117">tabella di route toocreate hello e route necessarie per la subnet front-end hello a seconda dello scenario hello precedente, seguire i passaggi di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="d14b1-117">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="d14b1-118">Eseguire hello successivo comando toocreate una tabella di route per la subnet front-end hello:</span><span class="sxs-lookup"><span data-stu-id="d14b1-118">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="d14b1-119">Output:</span><span class="sxs-lookup"><span data-stu-id="d14b1-119">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Looking up route table "UDR-FrontEnd"
        info:    Creating route table "UDR-FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    Name                            : UDR-FrontEnd
        data:    Type                            : Microsoft.Network/routeTables
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        info:    network route-table create command OK
   
    <span data-ttu-id="d14b1-120">Parametri</span><span class="sxs-lookup"><span data-stu-id="d14b1-120">Parameters:</span></span>
   
   * <span data-ttu-id="d14b1-121">**-g (o --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="d14b1-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="d14b1-122">Nome del gruppo di risorse hello in cui verrà creato hello UDR.</span><span class="sxs-lookup"><span data-stu-id="d14b1-122">Name of hello resource group where hello UDR will be created.</span></span> <span data-ttu-id="d14b1-123">Per questo scenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="d14b1-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="d14b1-124">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="d14b1-124">**-l (or --location)**.</span></span> <span data-ttu-id="d14b1-125">Area di Azure in cui hello UDR nuovo verrà creato.</span><span class="sxs-lookup"><span data-stu-id="d14b1-125">Azure region where hello new UDR will be created.</span></span> <span data-ttu-id="d14b1-126">Per questo scenario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="d14b1-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="d14b1-127">**-n (o --nome)**.</span><span class="sxs-lookup"><span data-stu-id="d14b1-127">**-n (or --name)**.</span></span> <span data-ttu-id="d14b1-128">Nome per hello UDR nuovo.</span><span class="sxs-lookup"><span data-stu-id="d14b1-128">Name for hello new UDR.</span></span> <span data-ttu-id="d14b1-129">Per questo scenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="d14b1-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="d14b1-130">Eseguire hello successivo comando toocreate una route in toosend tabella di route hello tutto il traffico destinato toohello subnet back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="d14b1-130">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="d14b1-131">Output:</span><span class="sxs-lookup"><span data-stu-id="d14b1-131">Output:</span></span>
   
        info:    Executing command network route-table route create
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        info:    Creating route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd/routes/RouteToBackEnd
        data:    Name                            : RouteToBackEnd
        data:    Provisioning state              : Succeeded
        data:    Next hop type                   : VirtualAppliance
        data:    Next hop IP address             : 192.168.0.4
        data:    Address prefix                  : 192.168.2.0/24
        info:    network route-table route create command OK
   
    <span data-ttu-id="d14b1-132">Parametri</span><span class="sxs-lookup"><span data-stu-id="d14b1-132">Parameters:</span></span>
   
   * <span data-ttu-id="d14b1-133">**-r (o --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="d14b1-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="d14b1-134">Nome della tabella di routing hello in cui verrà aggiunti route hello.</span><span class="sxs-lookup"><span data-stu-id="d14b1-134">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="d14b1-135">Per questo scenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="d14b1-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="d14b1-136">**-a (o --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="d14b1-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="d14b1-137">Prefisso dell'indirizzo per subnet hello in cui i pacchetti sono destinati a.</span><span class="sxs-lookup"><span data-stu-id="d14b1-137">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="d14b1-138">Per questo scenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="d14b1-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="d14b1-139">**-y (o --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="d14b1-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="d14b1-140">Tipo di oggetto al quale verrà inviato il traffico.</span><span class="sxs-lookup"><span data-stu-id="d14b1-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="d14b1-141">I valori possibili sono *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* o *None*.</span><span class="sxs-lookup"><span data-stu-id="d14b1-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="d14b1-142">**-p (o --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="d14b1-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="d14b1-143">Indirizzo IP per l'hop successivo.</span><span class="sxs-lookup"><span data-stu-id="d14b1-143">IP address for next hop.</span></span> <span data-ttu-id="d14b1-144">Per questo scenario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="d14b1-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="d14b1-145">Comando che segue hello esecuzione tabella di route hello tooassociate creata in precedenza con hello **front-end** subnet:</span><span class="sxs-lookup"><span data-stu-id="d14b1-145">Run hello following command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="d14b1-146">Output:</span><span class="sxs-lookup"><span data-stu-id="d14b1-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    Route Table                     : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConf
        igurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConf
        igurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK
   
    <span data-ttu-id="d14b1-147">Parametri</span><span class="sxs-lookup"><span data-stu-id="d14b1-147">Parameters:</span></span>
   
   * <span data-ttu-id="d14b1-148">**-e (o --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="d14b1-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="d14b1-149">Nome della rete virtuale in cui si trova subnet hello hello.</span><span class="sxs-lookup"><span data-stu-id="d14b1-149">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="d14b1-150">Per questo scenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="d14b1-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="d14b1-151">Creare hello UDR per subnet back-end hello</span><span class="sxs-lookup"><span data-stu-id="d14b1-151">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="d14b1-152">hello toocreate tabella di route e indirizzare necessari per la subnet di back-end hello a seconda dello scenario di hello sopra, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d14b1-152">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="d14b1-153">Eseguire hello successivo comando toocreate una tabella di route per la subnet di back-end hello:</span><span class="sxs-lookup"><span data-stu-id="d14b1-153">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="d14b1-154">Eseguire hello successivo comando toocreate una route in toosend tabella di route hello tutto il traffico destinato toohello subnet front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="d14b1-154">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="d14b1-155">Esecuzione hello seguenti tabella di routing di comandi tooassociate hello con hello **back-end** subnet:</span><span class="sxs-lookup"><span data-stu-id="d14b1-155">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="d14b1-156">Abilitare l'inoltro dell'indirizzo IP su FW1</span><span class="sxs-lookup"><span data-stu-id="d14b1-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="d14b1-157">inoltro dell'indirizzo IP nella scheda di rete utilizzata da hello tooenable **FW1**completa hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d14b1-157">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="d14b1-158">Eseguire il comando hello che segue e Nota Il valore di hello per **inoltro IP abilitare**.</span><span class="sxs-lookup"><span data-stu-id="d14b1-158">Run hello command that follows and notice hello value for **Enable IP forwarding**.</span></span> <span data-ttu-id="d14b1-159">Deve essere impostato troppo*false*.</span><span class="sxs-lookup"><span data-stu-id="d14b1-159">It should be set too*false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="d14b1-160">Output:</span><span class="sxs-lookup"><span data-stu-id="d14b1-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : false
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic show command OK
2. <span data-ttu-id="d14b1-161">Eseguire hello inoltro dell'indirizzo IP tooenable comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d14b1-161">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="d14b1-162">Output:</span><span class="sxs-lookup"><span data-stu-id="d14b1-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up hello network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : true
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic set command OK
   
    <span data-ttu-id="d14b1-163">Parametri</span><span class="sxs-lookup"><span data-stu-id="d14b1-163">Parameters:</span></span>
   
   * <span data-ttu-id="d14b1-164">**-f (o --enable-ip-forwarding)**.</span><span class="sxs-lookup"><span data-stu-id="d14b1-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="d14b1-165">*true* o *false*.</span><span class="sxs-lookup"><span data-stu-id="d14b1-165">*true* or *false*.</span></span>

