---
title: Creare i gruppi di sicurezza di rete - interfaccia della riga di comando 1.0 di Azure | Documentazione Microsoft
description: Informazioni su come creare e distribuire i gruppi di sicurezza di rete usando l'interfaccia della riga di comando di Azure 1.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ca8c182651e3c9f2f1f3a85b94361755d8e638d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-cli-10"></a><span data-ttu-id="412ad-103">Creare i gruppi di sicurezza di rete usando l'interfaccia della riga di comando 1.0 di Azure</span><span class="sxs-lookup"><span data-stu-id="412ad-103">Create network security groups using the Azure CLI 1.0</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="412ad-104">Versioni dell'interfaccia della riga di comando per completare l'attività</span><span class="sxs-lookup"><span data-stu-id="412ad-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="412ad-105">È possibile completare l'attività usando una delle versioni seguenti dell'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="412ad-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="412ad-106">[Interfaccia della riga di comando di Azure 1.0](#how-to-create-the-nsg-for-the-front-end-subnet): l'interfaccia della riga di comando per i modelli di distribuzione classica e di gestione delle risorse (questo articolo)</span><span class="sxs-lookup"><span data-stu-id="412ad-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="412ad-107">[Interfaccia della riga di comando di Azure 2.0](virtual-networks-create-nsg-arm-cli.md): interfaccia avanzata per il modello di distribuzione di gestione delle risorse</span><span class="sxs-lookup"><span data-stu-id="412ad-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - our next-generation CLI for the resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="412ad-108">Questo articolo illustra il modello di distribuzione Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="412ad-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="412ad-109">È anche possibile creare gruppi di sicurezza di rete con il [modello di distribuzione classica](virtual-networks-create-nsg-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="412ad-109">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="412ad-110">I comandi di esempio dell'interfaccia della riga di comando di Azure riportati di seguito prevedono un ambiente semplice già creato in base allo scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="412ad-110">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> 

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="412ad-111">Come creare il gruppo di sicurezza di rete per la subnet front-end</span><span class="sxs-lookup"><span data-stu-id="412ad-111">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="412ad-112">Per creare un gruppo di sicurezza di rete denominato *NSG-FrontEnd* in base allo scenario precedente, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="412ad-112">To create an NSG named named *NSG-FrontEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="412ad-113">Se l'interfaccia della riga di comando di Azure non è mai stata usata, vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md) e seguire le istruzioni fino al punto in cui si selezionano l'account e la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="412ad-113">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="412ad-114">Eseguire il comando **azure config mode** per passare alla modalità Gestione risorse, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="412ad-114">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="412ad-115">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="412ad-115">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="412ad-116">Eseguire il comando **azure network nsg create** per creare un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="412ad-116">Run the **azure network nsg create** command to create an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    <span data-ttu-id="412ad-117">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="412ad-117">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
        data:    Name                            : NSG-FrontEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
   
    <span data-ttu-id="412ad-118">Parametri</span><span class="sxs-lookup"><span data-stu-id="412ad-118">Parameters:</span></span>
   
   * <span data-ttu-id="412ad-119">**-g (o --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="412ad-119">**-g (or --resource-group)**.</span></span> <span data-ttu-id="412ad-120">Nome del gruppo di risorse in cui verrà creato il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="412ad-120">Name of the resource group where the NSG will be created.</span></span> <span data-ttu-id="412ad-121">Per questo scenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="412ad-121">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="412ad-122">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="412ad-122">**-l (or --location)**.</span></span> <span data-ttu-id="412ad-123">Area di Azure in cui verrà creato il nuovo gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="412ad-123">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="412ad-124">Per questo scenario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="412ad-124">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="412ad-125">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="412ad-125">**-n (or --name)**.</span></span> <span data-ttu-id="412ad-126">Nome per il nuovo gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="412ad-126">Name for the new NSG.</span></span> <span data-ttu-id="412ad-127">Per questo scenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="412ad-127">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="412ad-128">Eseguire il comando **azure network nsg rule create** per creare una regola che consenta l'accesso alla porta 3389 (RDP) da Internet.</span><span class="sxs-lookup"><span data-stu-id="412ad-128">Run the **azure network nsg rule create** command to create a rule that allows access to port 3389 (RDP) from the Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="412ad-129">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="412ad-129">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up the network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp
        -rule
        data:    Name                            : rdp-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 3389
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="412ad-130">Parametri</span><span class="sxs-lookup"><span data-stu-id="412ad-130">Parameters:</span></span>
   
   * <span data-ttu-id="412ad-131">**-a (o --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="412ad-131">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="412ad-132">Nome del gruppo di sicurezza di rete in cui verrà creata la regola.</span><span class="sxs-lookup"><span data-stu-id="412ad-132">Name of the NSG in which the rule will be created.</span></span> <span data-ttu-id="412ad-133">Per questo scenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="412ad-133">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="412ad-134">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="412ad-134">**-n (or --name)**.</span></span> <span data-ttu-id="412ad-135">Nome per la nuova regola.</span><span class="sxs-lookup"><span data-stu-id="412ad-135">Name for the new rule.</span></span> <span data-ttu-id="412ad-136">Per questo scenario, *rdp-rule*.</span><span class="sxs-lookup"><span data-stu-id="412ad-136">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="412ad-137">**-c (o --access)**.</span><span class="sxs-lookup"><span data-stu-id="412ad-137">**-c (or --access)**.</span></span> <span data-ttu-id="412ad-138">Livello di accesso per la regola (Deny o Allow).</span><span class="sxs-lookup"><span data-stu-id="412ad-138">Access level for the rule (Deny or Allow).</span></span>
   * <span data-ttu-id="412ad-139">**-p (o --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="412ad-139">**-p (or --protocol)**.</span></span> <span data-ttu-id="412ad-140">Protocollo (Tcp, Udp o *) per la regola.</span><span class="sxs-lookup"><span data-stu-id="412ad-140">Protocol (Tcp, Udp, or *) for the rule.</span></span>
   * <span data-ttu-id="412ad-141">**-r (o--direction)**.</span><span class="sxs-lookup"><span data-stu-id="412ad-141">**-r (or --direction)**.</span></span> <span data-ttu-id="412ad-142">Direzione di connessione (Inbound o Outbound).</span><span class="sxs-lookup"><span data-stu-id="412ad-142">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="412ad-143">**-y (o --priority)**.</span><span class="sxs-lookup"><span data-stu-id="412ad-143">**-y (or --priority)**.</span></span> <span data-ttu-id="412ad-144">Priorità per la regola.</span><span class="sxs-lookup"><span data-stu-id="412ad-144">Priority for the rule.</span></span>
   * <span data-ttu-id="412ad-145">**-f (o --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="412ad-145">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="412ad-146">Prefisso dell'indirizzo di origine in CIDR o con tag predefiniti.</span><span class="sxs-lookup"><span data-stu-id="412ad-146">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="412ad-147">**-o (o --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="412ad-147">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="412ad-148">Porta o intervallo di porte di origine.</span><span class="sxs-lookup"><span data-stu-id="412ad-148">Source port, or port range.</span></span>
   * <span data-ttu-id="412ad-149">**-e (o --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="412ad-149">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="412ad-150">Prefisso dell'indirizzo di destinazione in CIDR o con tag predefiniti.</span><span class="sxs-lookup"><span data-stu-id="412ad-150">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="412ad-151">**-u (o --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="412ad-151">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="412ad-152">Porta o intervallo di porte di destinazione.</span><span class="sxs-lookup"><span data-stu-id="412ad-152">Destination port, or port range.</span></span>    
5. <span data-ttu-id="412ad-153">Eseguire il comando **azure network nsg rule create** per creare una regola che consenta l'accesso alla porta 80 (HTTP) da Internet.</span><span class="sxs-lookup"><span data-stu-id="412ad-153">Run the **azure network nsg rule create** command to create a rule that allows access to port 80 (HTTP) from the Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="412ad-154">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="412ad-154">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 80
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="412ad-155">Eseguire il comando **azure network vnet subnet set** per collegare il gruppo di sicurezza di rete alla subnet front-end.</span><span class="sxs-lookup"><span data-stu-id="412ad-155">Run the **azure network vnet subnet set** command to link the NSG to the front end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    <span data-ttu-id="412ad-156">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="412ad-156">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up the subnet "FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="412ad-157">Come creare il gruppo di sicurezza di rete per la subnet back-end</span><span class="sxs-lookup"><span data-stu-id="412ad-157">How to create the NSG for the back end subnet</span></span>
<span data-ttu-id="412ad-158">Per creare un gruppo di sicurezza di rete denominato *NSG-BackEnd* in base allo scenario precedente, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="412ad-158">To create an NSG named named *NSG-BackEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="412ad-159">Eseguire il comando **azure network nsg create** per creare un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="412ad-159">Run the **azure network nsg create** command to create an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    <span data-ttu-id="412ad-160">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="412ad-160">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd
        data:    Name                            : NSG-BackEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
2. <span data-ttu-id="412ad-161">Eseguire il comando **azure network nsg rule create** per creare una regola che consenta l'accesso alla porta 1433 (SQL) dalla subnet front-end.</span><span class="sxs-lookup"><span data-stu-id="412ad-161">Run the **azure network nsg rule create** command to create a rule that allows access to port 1433 (SQL) from the front end subnet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="412ad-162">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="412ad-162">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule
        data:    Name                            : sql-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 1433
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="412ad-163">Eseguire il comando **azure network nsg rule create** per creare una regola che neghi l'accesso a Internet.</span><span class="sxs-lookup"><span data-stu-id="412ad-163">Run the **azure network nsg rule create** command to create a rule that denies access to the Internet from.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    <span data-ttu-id="412ad-164">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="412ad-164">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : *
        data:    Source Port                     : *
        data:    Destination IP                  : Internet
        data:    Destination Port                : *
        data:    Protocol                        : *
        data:    Direction                       : Outbound
        data:    Access                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="412ad-165">Eseguire il comando **azure network vnet subnet set** per collegare il gruppo di sicurezza di rete alla subnet back-end.</span><span class="sxs-lookup"><span data-stu-id="412ad-165">Run the **azure network vnet subnet set** command to link the NSG to the back end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    <span data-ttu-id="412ad-166">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="412ad-166">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up the subnet "BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/BackEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : BackEnd
        data:    Address prefix                  : 192.168.2.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL1/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL2/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

