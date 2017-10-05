---
title: Controllare il routing e i dispositivi virtuali usando l'interfaccia della riga di comando di Azure 1.0 | Documentazione Microsoft
description: Informazioni su come controllare il routing e i dispositivi virtuali mediante l'interfaccia della riga di comando di Azure 1.0.
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
ms.openlocfilehash: 5f21bc7a4fcd9507ea9d6b2b752a2328a7b834f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-user-defined-routes-udr-using-the-azure-cli-10"></a><span data-ttu-id="8bd20-103">Creare route definite dall'utente con l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="8bd20-103">Create User-Defined Routes (UDR) using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8bd20-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8bd20-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="8bd20-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="8bd20-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="8bd20-106">Modello</span><span class="sxs-lookup"><span data-stu-id="8bd20-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="8bd20-107">PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="8bd20-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="8bd20-108">Interfaccia della riga di comando (versione classica)</span><span class="sxs-lookup"><span data-stu-id="8bd20-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="8bd20-109">Creare routing personalizzati e dispositivi virtuali mediante l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="8bd20-109">Create custom routing and virtual appliances using the Azure CLI.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="8bd20-110">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="8bd20-110">CLI versions to complete the task</span></span> 

<span data-ttu-id="8bd20-111">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="8bd20-111">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="8bd20-112">[Interfaccia della riga di comando di Azure 1.0](#Create-the-UDR-for-the-front-end-subnet): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="8bd20-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="8bd20-113">[Interfaccia della riga di comando di Azure 2.0](virtual-network-create-udr-arm-cli.md): interfaccia della riga di comando di prossima generazione per il modello di distribuzione di Gestione risorsa</span><span class="sxs-lookup"><span data-stu-id="8bd20-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for the resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="8bd20-114">I comandi di esempio dell'interfaccia della riga di comando di Azure riportati di seguito prevedono un ambiente semplice già creato in base allo scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="8bd20-114">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="8bd20-115">Se si desidera eseguire i comandi così come sono visualizzati in questo documento, creare innanzitutto l'ambiente di test distribuendo [questo modello](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), fare clic su **Distribuisci in Azure**, sostituire i valori di parametro predefiniti, se necessario e seguire le istruzioni nel portale.</span><span class="sxs-lookup"><span data-stu-id="8bd20-115">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>


## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="8bd20-116">Creare la route definita dall'utente per la subnet front-end</span><span class="sxs-lookup"><span data-stu-id="8bd20-116">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="8bd20-117">Per creare la tabella di route e la route necessarie per la subnet front-end in base allo scenario precedente, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="8bd20-117">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="8bd20-118">Eseguire il comando seguente per creare una tabella di route per la subnet front-end:</span><span class="sxs-lookup"><span data-stu-id="8bd20-118">Run the following command to create a route table for the front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="8bd20-119">Output:</span><span class="sxs-lookup"><span data-stu-id="8bd20-119">Output:</span></span>
   
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
   
    <span data-ttu-id="8bd20-120">Parametri</span><span class="sxs-lookup"><span data-stu-id="8bd20-120">Parameters:</span></span>
   
   * <span data-ttu-id="8bd20-121">**-g (o --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="8bd20-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="8bd20-122">Nome del gruppo di risorse in cui verrà creata la route definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="8bd20-122">Name of the resource group where the UDR will be created.</span></span> <span data-ttu-id="8bd20-123">Per questo scenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="8bd20-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="8bd20-124">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="8bd20-124">**-l (or --location)**.</span></span> <span data-ttu-id="8bd20-125">Area di Azure in cui verrà creata la route definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="8bd20-125">Azure region where the new UDR will be created.</span></span> <span data-ttu-id="8bd20-126">Per questo scenario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="8bd20-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="8bd20-127">**-n (o --nome)**.</span><span class="sxs-lookup"><span data-stu-id="8bd20-127">**-n (or --name)**.</span></span> <span data-ttu-id="8bd20-128">Nome della nuova route definita dall'utente.</span><span class="sxs-lookup"><span data-stu-id="8bd20-128">Name for the new UDR.</span></span> <span data-ttu-id="8bd20-129">Per questo scenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="8bd20-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="8bd20-130">Eseguire il comando seguente per creare una route nella tabella della route creata in precedenza per inviare tutto il traffico destinato alla subnet back-end (192.168.2.0/24) alla VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="8bd20-130">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="8bd20-131">Output:</span><span class="sxs-lookup"><span data-stu-id="8bd20-131">Output:</span></span>
   
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
   
    <span data-ttu-id="8bd20-132">Parametri</span><span class="sxs-lookup"><span data-stu-id="8bd20-132">Parameters:</span></span>
   
   * <span data-ttu-id="8bd20-133">**-r (o --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="8bd20-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="8bd20-134">Nome della tabella di route in cui verrà aggiunta la route.</span><span class="sxs-lookup"><span data-stu-id="8bd20-134">Name of the route table where the route will be added.</span></span> <span data-ttu-id="8bd20-135">Per questo scenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="8bd20-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="8bd20-136">**-a (o --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="8bd20-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="8bd20-137">Prefisso di indirizzo della subnet alla quale sono destinati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="8bd20-137">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="8bd20-138">Per questo scenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="8bd20-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="8bd20-139">**-y (o --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="8bd20-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="8bd20-140">Tipo di oggetto al quale verrà inviato il traffico.</span><span class="sxs-lookup"><span data-stu-id="8bd20-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="8bd20-141">I valori possibili sono *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* o *None*.</span><span class="sxs-lookup"><span data-stu-id="8bd20-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="8bd20-142">**-p (o --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="8bd20-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="8bd20-143">Indirizzo IP per l'hop successivo.</span><span class="sxs-lookup"><span data-stu-id="8bd20-143">IP address for next hop.</span></span> <span data-ttu-id="8bd20-144">Per questo scenario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="8bd20-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="8bd20-145">Eseguire il comando seguente per associare la tabella di route creata in precedenza alla subnet **FrontEnd**:</span><span class="sxs-lookup"><span data-stu-id="8bd20-145">Run the following command to associate the route table created above with the **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="8bd20-146">Output:</span><span class="sxs-lookup"><span data-stu-id="8bd20-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up the subnet "FrontEnd"
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
   
    <span data-ttu-id="8bd20-147">Parametri</span><span class="sxs-lookup"><span data-stu-id="8bd20-147">Parameters:</span></span>
   
   * <span data-ttu-id="8bd20-148">**-e (o --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="8bd20-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="8bd20-149">Nome della rete virtuale in cui si trova la subnet.</span><span class="sxs-lookup"><span data-stu-id="8bd20-149">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="8bd20-150">Per questo scenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="8bd20-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="8bd20-151">Creare la route definita dall'utente per la subnet back-end</span><span class="sxs-lookup"><span data-stu-id="8bd20-151">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="8bd20-152">Per creare la tabella di route e la route necessarie per la subnet back-end in base allo scenario precedente, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8bd20-152">To create the route table and route needed for the back-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="8bd20-153">Per creare una tabella di route per la subnet back-end, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8bd20-153">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="8bd20-154">Eseguire il comando seguente per creare una route nella tabella della route creata in precedenza per inviare tutto il traffico destinato alla subnet front-end (192.168.1.0/24) alla VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="8bd20-154">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="8bd20-155">Eseguire il comando seguente per associare la tabella di route creata in precedenza alla subnet **BackEnd**:</span><span class="sxs-lookup"><span data-stu-id="8bd20-155">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="8bd20-156">Abilitare l'inoltro dell'indirizzo IP su FW1</span><span class="sxs-lookup"><span data-stu-id="8bd20-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="8bd20-157">Per abilitare l'inoltro dell'indirizzo IP nella scheda di interfaccia di rete usata da **FW1**, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8bd20-157">To enable IP forwarding in the NIC used by **FW1**, complete the following steps:</span></span>

1. <span data-ttu-id="8bd20-158">Eseguire il comando seguente e notare il valore per **Abilita inoltro dell'indirizzo IP**.</span><span class="sxs-lookup"><span data-stu-id="8bd20-158">Run the command that follows and notice the value for **Enable IP forwarding**.</span></span> <span data-ttu-id="8bd20-159">Il valore deve essere impostato su *false*.</span><span class="sxs-lookup"><span data-stu-id="8bd20-159">It should be set to *false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="8bd20-160">Output:</span><span class="sxs-lookup"><span data-stu-id="8bd20-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up the network interface "NICFW1"
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
2. <span data-ttu-id="8bd20-161">Eseguire il comando seguente per abilitare l'inoltro dell'indirizzo IP:</span><span class="sxs-lookup"><span data-stu-id="8bd20-161">Run the following command to enable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="8bd20-162">Output:</span><span class="sxs-lookup"><span data-stu-id="8bd20-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up the network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up the network interface "NICFW1"
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
   
    <span data-ttu-id="8bd20-163">Parametri</span><span class="sxs-lookup"><span data-stu-id="8bd20-163">Parameters:</span></span>
   
   * <span data-ttu-id="8bd20-164">**-f (o --enable-ip-forwarding)**.</span><span class="sxs-lookup"><span data-stu-id="8bd20-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="8bd20-165">*true* o *false*.</span><span class="sxs-lookup"><span data-stu-id="8bd20-165">*true* or *false*.</span></span>

