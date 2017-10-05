---
title: Creare una rete virtuale usando l'interfaccia della riga di comando 1.0 di Azure | Documentazione Microsoft
description: Informazioni su come creare una rete virtuale usando l'interfaccia della riga di comando 1.0 di Azure | Resource Manager.
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
ms.openlocfilehash: f0649c5c8c04dda72d2f147601efb37217f9bade
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-the-azure-cli"></a><span data-ttu-id="f459a-103">Creare una rete virtuale usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="f459a-103">Create a virtual network using the Azure CLI</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="f459a-104">Azure offre due modelli di distribuzione, ovvero Azure Resource Manager e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="f459a-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="f459a-105">Microsoft consiglia di creare le risorse tramite il modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f459a-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="f459a-106">Per altre informazioni sulle differenze tra i due modelli, leggere l'articolo [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) (Informazioni sui modelli di distribuzione di Azure).</span><span class="sxs-lookup"><span data-stu-id="f459a-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="f459a-107">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="f459a-107">CLI versions to complete the task</span></span>
<span data-ttu-id="f459a-108">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="f459a-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="f459a-109">[Interfaccia della riga di comando di Azure 2.0](virtual-networks-create-vnet-arm-cli.md): interfaccia avanzata per il modello di distribuzione di gestione delle risorse</span><span class="sxs-lookup"><span data-stu-id="f459a-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for the resource management deployment model</span></span>
- <span data-ttu-id="f459a-110">[Interfaccia della riga di comando di Azure 1.0](#create-a-virtual-network): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="f459a-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for the classic and resource management deployment models (this article)</span></span>

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="f459a-111">Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="f459a-111">Create a virtual network</span></span>

<span data-ttu-id="f459a-112">Per creare una rete virtuale usando l'interfaccia della riga di comando di Azure, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="f459a-112">To create a virtual network using the Azure CLI, complete the following steps:</span></span>

1. <span data-ttu-id="f459a-113">Per installare e configurare l'interfaccia della riga di comando di Azure, seguire la procedura riportata nell'articolo [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f459a-113">Install and configure the Azure CLI by following the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md) article.</span></span>

2. <span data-ttu-id="f459a-114">Creare una rete virtuale e subnet:</span><span class="sxs-lookup"><span data-stu-id="f459a-114">Create a VNet and a subnet:</span></span>

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    <span data-ttu-id="f459a-115">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="f459a-115">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    <span data-ttu-id="f459a-116">Parametri utilizzati:</span><span class="sxs-lookup"><span data-stu-id="f459a-116">Parameters used:</span></span>

   * <span data-ttu-id="f459a-117">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="f459a-117">**--vnet**.</span></span> <span data-ttu-id="f459a-118">Nome della rete virtuale da creare.</span><span class="sxs-lookup"><span data-stu-id="f459a-118">Name of the VNet to be created.</span></span> <span data-ttu-id="f459a-119">Per questo scenario, *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="f459a-119">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="f459a-120">**-e (o --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="f459a-120">**-e (or --address-space)**.</span></span> <span data-ttu-id="f459a-121">Spazio degli indirizzi della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="f459a-121">VNet address space.</span></span> <span data-ttu-id="f459a-122">Per questo scenario, *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="f459a-122">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="f459a-123">**-i (o -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="f459a-123">**-i (or -cidr)**.</span></span> <span data-ttu-id="f459a-124">Maschera di rete nel formato CIDR.</span><span class="sxs-lookup"><span data-stu-id="f459a-124">Network mask in CIDR format.</span></span> <span data-ttu-id="f459a-125">Per questo scenario, *16*</span><span class="sxs-lookup"><span data-stu-id="f459a-125">For our scenario, *16*.</span></span>
   * <span data-ttu-id="f459a-126">**- n (o --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="f459a-126">**-n (or --subnet-name**).</span></span> <span data-ttu-id="f459a-127">Nome della prima subnet.</span><span class="sxs-lookup"><span data-stu-id="f459a-127">Name of the first subnet.</span></span> <span data-ttu-id="f459a-128">Per questo scenario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="f459a-128">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="f459a-129">**-p (or --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="f459a-129">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="f459a-130">Indirizzo IP iniziale per la subnet o spazio di indirizzi della subnet.</span><span class="sxs-lookup"><span data-stu-id="f459a-130">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="f459a-131">Per questo scenario, *192.168.1.0*</span><span class="sxs-lookup"><span data-stu-id="f459a-131">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="f459a-132">**-r (o --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="f459a-132">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="f459a-133">Maschera di rete nel formato CIDR per la subnet.</span><span class="sxs-lookup"><span data-stu-id="f459a-133">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="f459a-134">Per questo scenario, *24*</span><span class="sxs-lookup"><span data-stu-id="f459a-134">For our scenario, *24*.</span></span>
   * <span data-ttu-id="f459a-135">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="f459a-135">**-l (or --location)**.</span></span> <span data-ttu-id="f459a-136">Area di Azure in cui verrà creata la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="f459a-136">Azure region where the VNet is created.</span></span> <span data-ttu-id="f459a-137">Per questo scenario, *Central US*.</span><span class="sxs-lookup"><span data-stu-id="f459a-137">For our scenario, *Central US*.</span></span>

3. <span data-ttu-id="f459a-138">Creare una subnet:</span><span class="sxs-lookup"><span data-stu-id="f459a-138">Create a subnet:</span></span>

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    <span data-ttu-id="f459a-139">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="f459a-139">Expected output:</span></span>

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up the subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    <span data-ttu-id="f459a-140">Parametri utilizzati:</span><span class="sxs-lookup"><span data-stu-id="f459a-140">Parameters used:</span></span>

   * <span data-ttu-id="f459a-141">**-t (o --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="f459a-141">**-t (or --vnet-name**.</span></span> <span data-ttu-id="f459a-142">Nome della rete virtuale in cui verrà creata la subnet.</span><span class="sxs-lookup"><span data-stu-id="f459a-142">Name of the VNet where the subnet will be created.</span></span> <span data-ttu-id="f459a-143">Per questo scenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="f459a-143">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="f459a-144">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="f459a-144">**-n (or --name)**.</span></span> <span data-ttu-id="f459a-145">Nome della nuova subnet.</span><span class="sxs-lookup"><span data-stu-id="f459a-145">Name of the new subnet.</span></span> <span data-ttu-id="f459a-146">Per questo scenario, *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="f459a-146">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="f459a-147">**-a (o --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="f459a-147">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="f459a-148">Blocco CIDR della subnet.</span><span class="sxs-lookup"><span data-stu-id="f459a-148">Subnet CIDR block.</span></span> <span data-ttu-id="f459a-149">Per questo scenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="f459a-149">Four our scenario, *192.168.2.0/24*.</span></span>
   
4. <span data-ttu-id="f459a-150">Per visualizzare le proprietà della nuova rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="f459a-150">To view the properties of the new VNet:</span></span>

    ```azurecli
    azure network vnet show
    ```
   
    <span data-ttu-id="f459a-151">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="f459a-151">Expected output:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up the virtual network sites
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

## <a name="next-steps"></a><span data-ttu-id="f459a-152">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f459a-152">Next steps</span></span>

<span data-ttu-id="f459a-153">Leggere le informazioni su come connettere:</span><span class="sxs-lookup"><span data-stu-id="f459a-153">Learn how to connect:</span></span>

- <span data-ttu-id="f459a-154">Una macchina virtuale (VM) a una rete virtuale nell'articolo [Creare una VM Linux](../virtual-machines/linux/quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f459a-154">A virtual machine (VM) to a virtual network by reading the [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="f459a-155">Anziché creare una rete virtuale e una subnet, come illustrato nelle procedure degli articoli, è possibile selezionare una rete virtuale e una subnet esistenti a cui connettere una VM.</span><span class="sxs-lookup"><span data-stu-id="f459a-155">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="f459a-156">La rete virtuale ad altre reti virtuali nell'articolo [Connettere reti virtuali](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f459a-156">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="f459a-157">La rete virtuale a una rete locale tramite una rete privata virtuale (VPN) da sito a sito o il circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f459a-157">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="f459a-158">Per le informazioni su come procedere, leggere [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) (Connettere una rete virtuale a una rete locale tramite una VPN da sito a sito) e [Collegare una rete virtuale a un circuito ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f459a-158">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>