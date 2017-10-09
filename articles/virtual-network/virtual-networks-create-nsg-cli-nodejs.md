---
title: -i gruppi di sicurezza di rete aaaCreate 1.0 CLI di Azure | Documenti Microsoft
description: Informazioni su come toocreate e distribuire i gruppi di sicurezza di rete utilizzando hello Azure CLI 1.0.
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
ms.openlocfilehash: eeb7feedab959d92659e03c5c46d93fdfc08faea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="32a99-103">Creare gruppi di protezione utilizzando hello Azure CLI 1.0 di rete</span><span class="sxs-lookup"><span data-stu-id="32a99-103">Create network security groups using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="32a99-104">Attività hello toocomplete versioni CLI</span><span class="sxs-lookup"><span data-stu-id="32a99-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="32a99-105">È possibile completare l'attività hello utilizzando una delle seguenti versioni CLI hello:</span><span class="sxs-lookup"><span data-stu-id="32a99-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="32a99-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) : l'interfaccia CLI per hello classic risorse Gestione modelli di distribuzione e (in questo articolo)</span><span class="sxs-lookup"><span data-stu-id="32a99-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="32a99-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) -CLI la prossima generazione per modello di distribuzione di gestione risorse hello</span><span class="sxs-lookup"><span data-stu-id="32a99-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="32a99-108">Questo articolo descrive il modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="32a99-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="32a99-109">È anche possibile [creare NSGs nel modello di distribuzione classica hello](virtual-networks-create-nsg-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="32a99-109">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="32a99-110">Hello esempio CLI di Azure comandi riportati di seguito prevedono un ambiente semplice già creato in base a uno scenario di hello precedente.</span><span class="sxs-lookup"><span data-stu-id="32a99-110">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> 

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="32a99-111">Come toocreate hello NSG per hello subnet front-end</span><span class="sxs-lookup"><span data-stu-id="32a99-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="32a99-112">toocreate denominato di un gruppo denominato *front-end di NSG* a seconda dello scenario hello precedente, procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="32a99-112">toocreate an NSG named named *NSG-FrontEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="32a99-113">Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="32a99-113">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="32a99-114">Eseguire hello **modalità di configurazione azure** tooswitch tooResource Manager modalità comando, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="32a99-114">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="32a99-115">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="32a99-115">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="32a99-116">Eseguire hello **rete azure creare** comando toocreate un gruppo.</span><span class="sxs-lookup"><span data-stu-id="32a99-116">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    <span data-ttu-id="32a99-117">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="32a99-117">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="32a99-118">Parametri</span><span class="sxs-lookup"><span data-stu-id="32a99-118">Parameters:</span></span>
   
   * <span data-ttu-id="32a99-119">**-g (o --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="32a99-119">**-g (or --resource-group)**.</span></span> <span data-ttu-id="32a99-120">Nome del gruppo di risorse hello in cui verrà creato hello gruppo.</span><span class="sxs-lookup"><span data-stu-id="32a99-120">Name of hello resource group where hello NSG will be created.</span></span> <span data-ttu-id="32a99-121">Per questo scenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="32a99-121">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="32a99-122">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="32a99-122">**-l (or --location)**.</span></span> <span data-ttu-id="32a99-123">Area di Azure in cui hello nuovo gruppo verrà creato.</span><span class="sxs-lookup"><span data-stu-id="32a99-123">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="32a99-124">Per questo scenario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="32a99-124">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="32a99-125">**-n (o --nome)**.</span><span class="sxs-lookup"><span data-stu-id="32a99-125">**-n (or --name)**.</span></span> <span data-ttu-id="32a99-126">Nome per hello nuovo gruppo.</span><span class="sxs-lookup"><span data-stu-id="32a99-126">Name for hello new NSG.</span></span> <span data-ttu-id="32a99-127">Per questo scenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="32a99-127">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="32a99-128">Eseguire hello **regola gruppo di rete di azure creare** toocreate comando una regola che consenta l'accesso tooport 3389 (RDP) da hello Internet.</span><span class="sxs-lookup"><span data-stu-id="32a99-128">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="32a99-129">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="32a99-129">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up hello network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="32a99-130">Parametri</span><span class="sxs-lookup"><span data-stu-id="32a99-130">Parameters:</span></span>
   
   * <span data-ttu-id="32a99-131">**-a (o --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="32a99-131">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="32a99-132">Nome del gruppo hello in cui hello regola verrà creata.</span><span class="sxs-lookup"><span data-stu-id="32a99-132">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="32a99-133">Per questo scenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="32a99-133">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="32a99-134">**-n (o --nome)**.</span><span class="sxs-lookup"><span data-stu-id="32a99-134">**-n (or --name)**.</span></span> <span data-ttu-id="32a99-135">Nome nuova regola hello.</span><span class="sxs-lookup"><span data-stu-id="32a99-135">Name for hello new rule.</span></span> <span data-ttu-id="32a99-136">Per questo scenario, *rdp-rule*.</span><span class="sxs-lookup"><span data-stu-id="32a99-136">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="32a99-137">**-c (o --access)**.</span><span class="sxs-lookup"><span data-stu-id="32a99-137">**-c (or --access)**.</span></span> <span data-ttu-id="32a99-138">Livello di accesso per la regola di hello (Deny o Consenti).</span><span class="sxs-lookup"><span data-stu-id="32a99-138">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="32a99-139">**-p (o --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="32a99-139">**-p (or --protocol)**.</span></span> <span data-ttu-id="32a99-140">Protocollo (Tcp, Udp o *) per la regola di hello.</span><span class="sxs-lookup"><span data-stu-id="32a99-140">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="32a99-141">**-r (o--direction)**.</span><span class="sxs-lookup"><span data-stu-id="32a99-141">**-r (or --direction)**.</span></span> <span data-ttu-id="32a99-142">Direzione di connessione (Inbound o Outbound).</span><span class="sxs-lookup"><span data-stu-id="32a99-142">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="32a99-143">**-y (o --priority)**.</span><span class="sxs-lookup"><span data-stu-id="32a99-143">**-y (or --priority)**.</span></span> <span data-ttu-id="32a99-144">Priorità per la regola di hello.</span><span class="sxs-lookup"><span data-stu-id="32a99-144">Priority for hello rule.</span></span>
   * <span data-ttu-id="32a99-145">**-f (o --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="32a99-145">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="32a99-146">Prefisso dell'indirizzo di origine in CIDR o con tag predefiniti.</span><span class="sxs-lookup"><span data-stu-id="32a99-146">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="32a99-147">**-o (o --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="32a99-147">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="32a99-148">Porta o intervallo di porte di origine.</span><span class="sxs-lookup"><span data-stu-id="32a99-148">Source port, or port range.</span></span>
   * <span data-ttu-id="32a99-149">**-e (o --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="32a99-149">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="32a99-150">Prefisso dell'indirizzo di destinazione in CIDR o con tag predefiniti.</span><span class="sxs-lookup"><span data-stu-id="32a99-150">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="32a99-151">**-u (o --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="32a99-151">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="32a99-152">Porta o intervallo di porte di destinazione.</span><span class="sxs-lookup"><span data-stu-id="32a99-152">Destination port, or port range.</span></span>    
5. <span data-ttu-id="32a99-153">Eseguire hello **regola gruppo di rete di azure creare** toocreate comando una regola che consenta l'accesso tooport 80 (HTTP) da hello Internet.</span><span class="sxs-lookup"><span data-stu-id="32a99-153">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="32a99-154">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="32a99-154">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
6. <span data-ttu-id="32a99-155">Eseguire hello **set di subnet della rete virtuale azure rete** subnet front-end di comando toolink hello NSG toohello.</span><span class="sxs-lookup"><span data-stu-id="32a99-155">Run hello **azure network vnet subnet set** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    <span data-ttu-id="32a99-156">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="32a99-156">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
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

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="32a99-157">Come toocreate hello NSG per hello nuovamente terminare subnet</span><span class="sxs-lookup"><span data-stu-id="32a99-157">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="32a99-158">toocreate denominato di un gruppo denominato *back-end di NSG* a seconda dello scenario hello precedente, procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="32a99-158">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="32a99-159">Eseguire hello **rete azure creare** comando toocreate un gruppo.</span><span class="sxs-lookup"><span data-stu-id="32a99-159">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    <span data-ttu-id="32a99-160">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="32a99-160">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
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
2. <span data-ttu-id="32a99-161">Eseguire hello **regola gruppo di rete di azure creare** toocreate comando una regola che consenta l'accesso tooport 1433 (SQL) dalla subnet front-end hello.</span><span class="sxs-lookup"><span data-stu-id="32a99-161">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="32a99-162">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="32a99-162">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
3. <span data-ttu-id="32a99-163">Eseguire hello **regola gruppo di rete di azure creare** toocreate comando una regola che nega l'accesso toohello Internet da.</span><span class="sxs-lookup"><span data-stu-id="32a99-163">Run hello **azure network nsg rule create** command toocreate a rule that denies access toohello Internet from.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    <span data-ttu-id="32a99-164">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="32a99-164">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
4. <span data-ttu-id="32a99-165">Eseguire hello **set di subnet della rete virtuale azure rete** comando toolink hello NSG toohello nuovamente terminare subnet.</span><span class="sxs-lookup"><span data-stu-id="32a99-165">Run hello **azure network vnet subnet set** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    <span data-ttu-id="32a99-166">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="32a99-166">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up hello subnet "BackEnd"
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

