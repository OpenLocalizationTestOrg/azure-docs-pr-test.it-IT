---
title: routing aaaControl classica una rete virtuale di Azure - CLI - | Documenti Microsoft
description: Informazioni su come toocontrol routing in reti virtuali mediante hello CLI di Azure nel modello di distribuzione classica hello
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
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a><span data-ttu-id="e8d14-103">Routing di controllo e l'utilizzo di dispositivi virtuali (classici) utilizzare hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="e8d14-103">Control routing and use virtual appliances (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e8d14-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8d14-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="e8d14-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e8d14-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="e8d14-106">Modello</span><span class="sxs-lookup"><span data-stu-id="e8d14-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="e8d14-107">PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="e8d14-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="e8d14-108">Interfaccia della riga di comando (versione classica)</span><span class="sxs-lookup"><span data-stu-id="e8d14-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="e8d14-109">Questo articolo descrive il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="e8d14-109">This article covers hello classic deployment model.</span></span> <span data-ttu-id="e8d14-110">È anche possibile [controllare il routing e utilizzare i dispositivi di rete nel modello di distribuzione di gestione risorse di hello](virtual-network-create-udr-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e8d14-110">You can also [control routing and use virtual appliances in hello Resource Manager deployment model](virtual-network-create-udr-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="e8d14-111">Hello esempio CLI di Azure comandi riportati di seguito prevedono un ambiente semplice già creato in base a uno scenario di hello precedente.</span><span class="sxs-lookup"><span data-stu-id="e8d14-111">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="e8d14-112">Se si desidera comandi hello toorun così come sono visualizzati in questo documento, creare nell'ambiente di hello [creare una rete virtuale (classico) mediante Azure CLI hello](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e8d14-112">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using hello Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="e8d14-113">Creare hello UDR per subnet front-end hello</span><span class="sxs-lookup"><span data-stu-id="e8d14-113">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="e8d14-114">tabella di route toocreate hello e route necessarie per la subnet front-end hello a seconda dello scenario hello precedente, seguire i passaggi di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="e8d14-114">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="e8d14-115">Eseguire hello modalità tooclassic tooswitch dei comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e8d14-115">Run hello following command tooswitch tooclassic mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="e8d14-116">Output:</span><span class="sxs-lookup"><span data-stu-id="e8d14-116">Output:</span></span>

        info:    New mode is asm

2. <span data-ttu-id="e8d14-117">Eseguire hello successivo comando toocreate una tabella di route per la subnet front-end hello:</span><span class="sxs-lookup"><span data-stu-id="e8d14-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="e8d14-118">Output:</span><span class="sxs-lookup"><span data-stu-id="e8d14-118">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    <span data-ttu-id="e8d14-119">Parametri</span><span class="sxs-lookup"><span data-stu-id="e8d14-119">Parameters:</span></span>
   
   * <span data-ttu-id="e8d14-120">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="e8d14-120">**-l (or --location)**.</span></span> <span data-ttu-id="e8d14-121">Area di Azure in cui hello nuovo gruppo verrà creato.</span><span class="sxs-lookup"><span data-stu-id="e8d14-121">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="e8d14-122">Per questo scenario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="e8d14-122">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="e8d14-123">**-n (o --nome)**.</span><span class="sxs-lookup"><span data-stu-id="e8d14-123">**-n (or --name)**.</span></span> <span data-ttu-id="e8d14-124">Nome per hello nuovo gruppo.</span><span class="sxs-lookup"><span data-stu-id="e8d14-124">Name for hello new NSG.</span></span> <span data-ttu-id="e8d14-125">Per questo scenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="e8d14-125">For our scenario, *NSG-FrontEnd*.</span></span>
3. <span data-ttu-id="e8d14-126">Eseguire hello successivo comando toocreate una route in toosend tabella di route hello tutto il traffico destinato toohello subnet back-end (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="e8d14-126">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    <span data-ttu-id="e8d14-127">Output:</span><span class="sxs-lookup"><span data-stu-id="e8d14-127">Output:</span></span>
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    <span data-ttu-id="e8d14-128">Parametri</span><span class="sxs-lookup"><span data-stu-id="e8d14-128">Parameters:</span></span>
   
   * <span data-ttu-id="e8d14-129">**-r (o --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="e8d14-129">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="e8d14-130">Nome della tabella di routing hello in cui verrà aggiunti route hello.</span><span class="sxs-lookup"><span data-stu-id="e8d14-130">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="e8d14-131">Per questo scenario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="e8d14-131">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="e8d14-132">**-a (o --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="e8d14-132">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="e8d14-133">Prefisso dell'indirizzo per subnet hello in cui i pacchetti sono destinati a.</span><span class="sxs-lookup"><span data-stu-id="e8d14-133">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="e8d14-134">Per questo scenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="e8d14-134">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="e8d14-135">**-t (o --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="e8d14-135">**-t (or --next-hop-type)**.</span></span> <span data-ttu-id="e8d14-136">Tipo di oggetto al quale verrà inviato il traffico.</span><span class="sxs-lookup"><span data-stu-id="e8d14-136">Type of object traffic will be sent to.</span></span> <span data-ttu-id="e8d14-137">I valori possibili sono *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* o *None*.</span><span class="sxs-lookup"><span data-stu-id="e8d14-137">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="e8d14-138">**-p (o --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="e8d14-138">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="e8d14-139">Indirizzo IP per l'hop successivo.</span><span class="sxs-lookup"><span data-stu-id="e8d14-139">IP address for next hop.</span></span> <span data-ttu-id="e8d14-140">Per questo scenario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="e8d14-140">For our scenario, *192.168.0.4*.</span></span>
4. <span data-ttu-id="e8d14-141">Comando che segue hello esecuzione tabella di route hello tooassociate creata con hello **front-end** subnet:</span><span class="sxs-lookup"><span data-stu-id="e8d14-141">Run hello following command tooassociate hello route table created with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="e8d14-142">Output:</span><span class="sxs-lookup"><span data-stu-id="e8d14-142">Output:</span></span>
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    <span data-ttu-id="e8d14-143">Parametri</span><span class="sxs-lookup"><span data-stu-id="e8d14-143">Parameters:</span></span>
   
   * <span data-ttu-id="e8d14-144">**-t (o --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="e8d14-144">**-t (or --vnet-name)**.</span></span> <span data-ttu-id="e8d14-145">Nome della rete virtuale in cui si trova subnet hello hello.</span><span class="sxs-lookup"><span data-stu-id="e8d14-145">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="e8d14-146">Per questo scenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="e8d14-146">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="e8d14-147">**-n (o --subnet-name**.</span><span class="sxs-lookup"><span data-stu-id="e8d14-147">**-n (or --subnet-name**.</span></span> <span data-ttu-id="e8d14-148">Verrà aggiunto al nome della tabella di routing hello subnet hello.</span><span class="sxs-lookup"><span data-stu-id="e8d14-148">Name of hello subnet hello route table will be added to.</span></span> <span data-ttu-id="e8d14-149">Per questo scenario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="e8d14-149">For our scenario, *FrontEnd*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="e8d14-150">Creare hello UDR per subnet back-end hello</span><span class="sxs-lookup"><span data-stu-id="e8d14-150">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="e8d14-151">tabella di route toocreate hello e route necessarie per la subnet di back-end hello a seconda dello scenario hello, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e8d14-151">toocreate hello route table and route needed for hello back-end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="e8d14-152">Eseguire hello successivo comando toocreate una tabella di route per la subnet di back-end hello:</span><span class="sxs-lookup"><span data-stu-id="e8d14-152">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. <span data-ttu-id="e8d14-153">Eseguire hello successivo comando toocreate una route in toosend tabella di route hello tutto il traffico destinato toohello subnet front-end (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="e8d14-153">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="e8d14-154">Esecuzione hello seguenti tabella di routing di comandi tooassociate hello con hello **back-end** subnet:</span><span class="sxs-lookup"><span data-stu-id="e8d14-154">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

