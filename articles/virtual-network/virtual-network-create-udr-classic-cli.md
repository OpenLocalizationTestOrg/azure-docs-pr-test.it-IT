---
title: Controllare il routing in una rete virtuale di Azure - Interfaccia della riga di comando - Modello di distribuzione classica | Documentazione Microsoft
description: Informazioni su come controllare il routing in reti virtuali mediante l'interfaccia della riga di comando di Azure nel modello di distribuzione classica
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 8fcb98723e7e872c932908e3456dc8680deb0901
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-the-azure-cli"></a><span data-ttu-id="48d6e-103">Controllare il routing e usare dispositivi virtuali di rete (distribuzione classica) mediante l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="48d6e-103">Control routing and use virtual appliances (classic) using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="48d6e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="48d6e-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="48d6e-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="48d6e-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="48d6e-106">Modello</span><span class="sxs-lookup"><span data-stu-id="48d6e-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="48d6e-107">PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="48d6e-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="48d6e-108">Interfaccia della riga di comando (versione classica)</span><span class="sxs-lookup"><span data-stu-id="48d6e-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="48d6e-109">In questo articolo viene illustrato il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="48d6e-109">This article covers the classic deployment model.</span></span> <span data-ttu-id="48d6e-110">È possibile anche [controllare il routing e usare dispositivi virtuali di rete nel modello di distribuzione di Gestione risorse](virtual-network-create-udr-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="48d6e-110">You can also [control routing and use virtual appliances in the Resource Manager deployment model](virtual-network-create-udr-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="48d6e-111">I comandi di esempio dell'interfaccia della riga di comando di Azure riportati di seguito prevedono un ambiente semplice già creato in base allo scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="48d6e-111">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="48d6e-112">Se si desidera eseguire i comandi illustrati in questo documento, creare l'ambiente descritto nella pagina relativa alla [creazione di una rete virtuale (classica) mediante l'interfaccia della riga di comando di Azure](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="48d6e-112">If you want to run the commands as they are displayed in this document, create the environment shown in [create a VNet (classic) using the Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="48d6e-113">Creare la route definita dall'utente per la subnet front-end</span><span class="sxs-lookup"><span data-stu-id="48d6e-113">Create the UDR for the front end subnet</span></span>
<span data-ttu-id="48d6e-114">Per creare la tabella di route e la route necessarie per la subnet front-end in base allo scenario precedente, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="48d6e-114">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="48d6e-115">Usare il comando seguente per passare alla modalità classica:</span><span class="sxs-lookup"><span data-stu-id="48d6e-115">Run the following command to switch to classic mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="48d6e-116">Output:</span><span class="sxs-lookup"><span data-stu-id="48d6e-116">Output:</span></span>

        info:    New mode is asm

2. <span data-ttu-id="48d6e-117">Eseguire il comando seguente per creare una tabella di route per la subnet front-end:</span><span class="sxs-lookup"><span data-stu-id="48d6e-117">Run the following command to create a route table for the front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="48d6e-118">Output:</span><span class="sxs-lookup"><span data-stu-id="48d6e-118">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    <span data-ttu-id="48d6e-119">Parametri</span><span class="sxs-lookup"><span data-stu-id="48d6e-119">Parameters:</span></span>
   
   * <span data-ttu-id="48d6e-120">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="48d6e-120">**-l (or --location)**.</span></span> <span data-ttu-id="48d6e-121">Area di Azure in cui verrà creato il nuovo gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="48d6e-121">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="48d6e-122">Per questo scenario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="48d6e-122">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="48d6e-123">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="48d6e-123">**-n (or --name)**.</span></span> <span data-ttu-id="48d6e-124">Nome per il nuovo gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="48d6e-124">Name for the new NSG.</span></span> <span data-ttu-id="48d6e-125">Per questo scenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="48d6e-125">For our scenario, *NSG-FrontEnd*.</span></span>
3. <span data-ttu-id="48d6e-126">Eseguire il comando seguente per creare una route nella tabella della route creata in precedenza per inviare tutto il traffico destinato alla subnet back-end (192.168.2.0/24) alla VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="48d6e-126">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    <span data-ttu-id="48d6e-127">Output:</span><span class="sxs-lookup"><span data-stu-id="48d6e-127">Output:</span></span>
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    <span data-ttu-id="48d6e-128">Parametri</span><span class="sxs-lookup"><span data-stu-id="48d6e-128">Parameters:</span></span>
   
   * <span data-ttu-id="48d6e-129">**-r (o --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="48d6e-129">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="48d6e-130">Nome della tabella di route in cui verrà aggiunta la route.</span><span class="sxs-lookup"><span data-stu-id="48d6e-130">Name of the route table where the route will be added.</span></span> <span data-ttu-id="48d6e-131">Per questo scenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="48d6e-131">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="48d6e-132">**-a (o --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="48d6e-132">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="48d6e-133">Prefisso di indirizzo della subnet alla quale sono destinati i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="48d6e-133">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="48d6e-134">Per questo scenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="48d6e-134">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="48d6e-135">**-t (o --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="48d6e-135">**-t (or --next-hop-type)**.</span></span> <span data-ttu-id="48d6e-136">Tipo di oggetto al quale verrà inviato il traffico.</span><span class="sxs-lookup"><span data-stu-id="48d6e-136">Type of object traffic will be sent to.</span></span> <span data-ttu-id="48d6e-137">I valori possibili sono *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* o *None*.</span><span class="sxs-lookup"><span data-stu-id="48d6e-137">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="48d6e-138">**-p (o --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="48d6e-138">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="48d6e-139">Indirizzo IP per l'hop successivo.</span><span class="sxs-lookup"><span data-stu-id="48d6e-139">IP address for next hop.</span></span> <span data-ttu-id="48d6e-140">Per questo scenario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="48d6e-140">For our scenario, *192.168.0.4*.</span></span>
4. <span data-ttu-id="48d6e-141">Eseguire il comando seguente per associare la tabella di route creata con la subnet **FrontEnd**:</span><span class="sxs-lookup"><span data-stu-id="48d6e-141">Run the following command to associate the route table created with the **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="48d6e-142">Output:</span><span class="sxs-lookup"><span data-stu-id="48d6e-142">Output:</span></span>
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    <span data-ttu-id="48d6e-143">Parametri</span><span class="sxs-lookup"><span data-stu-id="48d6e-143">Parameters:</span></span>
   
   * <span data-ttu-id="48d6e-144">**-t (o --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="48d6e-144">**-t (or --vnet-name)**.</span></span> <span data-ttu-id="48d6e-145">Nome della rete virtuale in cui si trova la subnet.</span><span class="sxs-lookup"><span data-stu-id="48d6e-145">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="48d6e-146">Per questo scenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="48d6e-146">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="48d6e-147">**-n (o --subnet-name**.</span><span class="sxs-lookup"><span data-stu-id="48d6e-147">**-n (or --subnet-name**.</span></span> <span data-ttu-id="48d6e-148">Nome della subnet in cui verrà aggiunta la tabella di route.</span><span class="sxs-lookup"><span data-stu-id="48d6e-148">Name of the subnet the route table will be added to.</span></span> <span data-ttu-id="48d6e-149">Per questo scenario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="48d6e-149">For our scenario, *FrontEnd*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="48d6e-150">Creare la route definita dall'utente per la subnet back-end</span><span class="sxs-lookup"><span data-stu-id="48d6e-150">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="48d6e-151">Per creare la tabella di route e la route necessarie per la subnet back-end in base allo scenario precedente, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="48d6e-151">To create the route table and route needed for the back-end subnet based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="48d6e-152">Eseguire il comando seguente per creare una tabella di route per la subnet back-end:</span><span class="sxs-lookup"><span data-stu-id="48d6e-152">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. <span data-ttu-id="48d6e-153">Eseguire il comando seguente per creare una route nella tabella della route creata in precedenza per inviare tutto il traffico destinato alla subnet front-end (192.168.1.0/24) alla VM **FW1** (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="48d6e-153">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="48d6e-154">Eseguire il comando seguente per associare la tabella di route creata in precedenza alla subnet **BackEnd**:</span><span class="sxs-lookup"><span data-stu-id="48d6e-154">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

