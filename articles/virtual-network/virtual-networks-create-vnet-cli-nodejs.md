---
title: una rete virtuale utilizzando aaaCreate hello Azure CLI 1.0 | Documenti Microsoft
description: Informazioni su come una rete virtuale utilizzando toocreate hello Azure CLI 1.0 | Gestore delle risorse.
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a><span data-ttu-id="3e601-103">Creare una rete virtuale usando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="3e601-103">Create a virtual network using hello Azure CLI</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="3e601-104">Azure offre due modelli di distribuzione, ovvero Azure Resource Manager e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="3e601-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="3e601-105">Si consiglia di creare risorse modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="3e601-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="3e601-106">altre informazioni sulle toolearn hello le differenze tra hello due modelli, leggere hello [modelli di distribuzione Azure comprendere](../azure-resource-manager/resource-manager-deployment-model.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="3e601-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="3e601-107">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="3e601-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="3e601-108">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="3e601-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="3e601-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) -la prossima generazione CLI per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="3e601-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span>
- <span data-ttu-id="3e601-110">[Azure CLI 1.0](#create-a-virtual-network) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="3e601-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for hello classic and resource management deployment models (this article)</span></span>

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="3e601-111">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="3e601-111">Create a virtual network</span></span>

<span data-ttu-id="3e601-112">una rete virtuale utilizzando toocreate hello CLI di Azure, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="3e601-112">toocreate a virtual network using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="3e601-113">Installare e configurare Azure CLI da hello seguente passaggi hello in hello [installare e configurare hello Azure CLI](../cli-install-nodejs.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="3e601-113">Install and configure hello Azure CLI by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article.</span></span>

2. <span data-ttu-id="3e601-114">Creare una rete virtuale e subnet:</span><span class="sxs-lookup"><span data-stu-id="3e601-114">Create a VNet and a subnet:</span></span>

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    <span data-ttu-id="3e601-115">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="3e601-115">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    <span data-ttu-id="3e601-116">Parametri utilizzati:</span><span class="sxs-lookup"><span data-stu-id="3e601-116">Parameters used:</span></span>

   * <span data-ttu-id="3e601-117">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="3e601-117">**--vnet**.</span></span> <span data-ttu-id="3e601-118">Nome di hello toobe di rete virtuale creata.</span><span class="sxs-lookup"><span data-stu-id="3e601-118">Name of hello VNet toobe created.</span></span> <span data-ttu-id="3e601-119">Per questo scenario, *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="3e601-119">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="3e601-120">**-e (o --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="3e601-120">**-e (or --address-space)**.</span></span> <span data-ttu-id="3e601-121">Spazio degli indirizzi della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3e601-121">VNet address space.</span></span> <span data-ttu-id="3e601-122">Per questo scenario, *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="3e601-122">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="3e601-123">**-i (o -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="3e601-123">**-i (or -cidr)**.</span></span> <span data-ttu-id="3e601-124">Maschera di rete nel formato CIDR.</span><span class="sxs-lookup"><span data-stu-id="3e601-124">Network mask in CIDR format.</span></span> <span data-ttu-id="3e601-125">Per questo scenario, *16*</span><span class="sxs-lookup"><span data-stu-id="3e601-125">For our scenario, *16*.</span></span>
   * <span data-ttu-id="3e601-126">**- n (o --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="3e601-126">**-n (or --subnet-name**).</span></span> <span data-ttu-id="3e601-127">Nome della subnet prima hello.</span><span class="sxs-lookup"><span data-stu-id="3e601-127">Name of hello first subnet.</span></span> <span data-ttu-id="3e601-128">Per questo scenario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="3e601-128">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="3e601-129">**-p (or --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="3e601-129">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="3e601-130">Indirizzo IP iniziale per la subnet o spazio di indirizzi della subnet.</span><span class="sxs-lookup"><span data-stu-id="3e601-130">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="3e601-131">Per questo scenario, *192.168.1.0*</span><span class="sxs-lookup"><span data-stu-id="3e601-131">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="3e601-132">**-r (o --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="3e601-132">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="3e601-133">Maschera di rete nel formato CIDR per la subnet.</span><span class="sxs-lookup"><span data-stu-id="3e601-133">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="3e601-134">Per questo scenario, *24*</span><span class="sxs-lookup"><span data-stu-id="3e601-134">For our scenario, *24*.</span></span>
   * <span data-ttu-id="3e601-135">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="3e601-135">**-l (or --location)**.</span></span> <span data-ttu-id="3e601-136">Area di Azure in cui è stato creato hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3e601-136">Azure region where hello VNet is created.</span></span> <span data-ttu-id="3e601-137">Per questo scenario, *Central US*.</span><span class="sxs-lookup"><span data-stu-id="3e601-137">For our scenario, *Central US*.</span></span>

3. <span data-ttu-id="3e601-138">Creare una subnet:</span><span class="sxs-lookup"><span data-stu-id="3e601-138">Create a subnet:</span></span>

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    <span data-ttu-id="3e601-139">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="3e601-139">Expected output:</span></span>

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    <span data-ttu-id="3e601-140">Parametri utilizzati:</span><span class="sxs-lookup"><span data-stu-id="3e601-140">Parameters used:</span></span>

   * <span data-ttu-id="3e601-141">**-t (o --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="3e601-141">**-t (or --vnet-name**.</span></span> <span data-ttu-id="3e601-142">Nome della rete virtuale in cui verrà creata la subnet hello hello.</span><span class="sxs-lookup"><span data-stu-id="3e601-142">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="3e601-143">Per questo scenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="3e601-143">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="3e601-144">**-n (o --nome)**.</span><span class="sxs-lookup"><span data-stu-id="3e601-144">**-n (or --name)**.</span></span> <span data-ttu-id="3e601-145">Nome della nuova subnet hello.</span><span class="sxs-lookup"><span data-stu-id="3e601-145">Name of hello new subnet.</span></span> <span data-ttu-id="3e601-146">Per questo scenario, *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="3e601-146">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="3e601-147">**-a (o --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="3e601-147">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="3e601-148">Blocco CIDR della subnet.</span><span class="sxs-lookup"><span data-stu-id="3e601-148">Subnet CIDR block.</span></span> <span data-ttu-id="3e601-149">Per questo scenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="3e601-149">Four our scenario, *192.168.2.0/24*.</span></span>
   
4. <span data-ttu-id="3e601-150">proprietà hello tooview di hello nuova rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="3e601-150">tooview hello properties of hello new VNet:</span></span>

    ```azurecli
    azure network vnet show
    ```
   
    <span data-ttu-id="3e601-151">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="3e601-151">Expected output:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a><span data-ttu-id="3e601-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3e601-152">Next steps</span></span>

<span data-ttu-id="3e601-153">Informazioni su come tooconnect:</span><span class="sxs-lookup"><span data-stu-id="3e601-153">Learn how tooconnect:</span></span>

- <span data-ttu-id="3e601-154">Una rete virtuale tooa di macchina virtuale (VM) leggendo hello [creare una VM Linux](../virtual-machines/linux/quick-create-cli.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="3e601-154">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="3e601-155">Anziché creare una rete virtuale e subnet nei passaggi hello degli articoli hello, è possibile selezionare una rete virtuale esistente e subnet tooconnect una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="3e601-155">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="3e601-156">Hello reti virtuali di rete virtuale tooother leggendo hello [connettere reti virtuali](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="3e601-156">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="3e601-157">rete locale tooan rete virtuale Hello utilizza una rete privata virtuale (VPN) da sito a sito o un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3e601-157">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="3e601-158">Ulteriori informazioni, leggere hello [connettere una rete locale tooan di rete virtuale tramite una VPN site-to-site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [collegare un circuito ExpressRoute di tooan rete virtuale](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="3e601-158">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
