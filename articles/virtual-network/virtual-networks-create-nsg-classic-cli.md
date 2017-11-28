---
title: "aaaHow toocreate NSGs in modalità classica con hello CLI di Azure | Documenti Microsoft"
description: "Informazioni su come toocreate e distribuire NSGs in modalità classica utilizzando hello CLI di Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a><span data-ttu-id="b28de-103">Come NSGs toocreate (classico) nell'hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="b28de-103">How toocreate NSGs (classic) in hello Azure CLI</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="b28de-104">Questo articolo descrive il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="b28de-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="b28de-105">È anche possibile [creare NSGs nel modello di distribuzione di gestione risorse di hello](virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b28de-105">You can also [create NSGs in hello Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="b28de-106">Hello esempio CLI di Azure comandi riportati di seguito prevedono un ambiente semplice già creato in base a uno scenario di hello precedente.</span><span class="sxs-lookup"><span data-stu-id="b28de-106">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="b28de-107">Se si desidera comandi hello toorun così come sono visualizzati in questo documento, è innanzitutto necessario generare ambiente di test hello da [la creazione di una rete virtuale](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b28de-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="b28de-108">Come toocreate hello NSG per hello subnet front-end</span><span class="sxs-lookup"><span data-stu-id="b28de-108">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="b28de-109">toocreate denominato di un gruppo denominato **front-end di NSG** a seconda dello scenario hello precedente, procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="b28de-109">toocreate an NSG named named **NSG-FrontEnd** based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="b28de-110">Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="b28de-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="b28de-111">Eseguire hello  **`azure config mode`**  comando tooswitch tooclassic modalità come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b28de-111">Run hello **`azure config mode`** command tooswitch tooclassic mode, as shown below.</span></span>
   
        azure config mode asm
   
    <span data-ttu-id="b28de-112">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="b28de-112">Expected output:</span></span>
   
        info:    New mode is asm
3. <span data-ttu-id="b28de-113">Eseguire hello  **`azure network nsg create`**  comando toocreate un gruppo.</span><span class="sxs-lookup"><span data-stu-id="b28de-113">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    <span data-ttu-id="b28de-114">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="b28de-114">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="b28de-115">Parametri</span><span class="sxs-lookup"><span data-stu-id="b28de-115">Parameters:</span></span>
   
   * <span data-ttu-id="b28de-116">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="b28de-116">**-l (or --location)**.</span></span> <span data-ttu-id="b28de-117">Area di Azure in cui hello nuovo gruppo verrà creato.</span><span class="sxs-lookup"><span data-stu-id="b28de-117">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="b28de-118">Per questo scenario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="b28de-118">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="b28de-119">**-n (o --nome)**.</span><span class="sxs-lookup"><span data-stu-id="b28de-119">**-n (or --name)**.</span></span> <span data-ttu-id="b28de-120">Nome per hello nuovo gruppo.</span><span class="sxs-lookup"><span data-stu-id="b28de-120">Name for hello new NSG.</span></span> <span data-ttu-id="b28de-121">Per questo scenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="b28de-121">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="b28de-122">Eseguire hello  **`azure network nsg rule create`**  toocreate comando una regola che consenta l'accesso tooport 3389 (RDP) da hello Internet.</span><span class="sxs-lookup"><span data-stu-id="b28de-122">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="b28de-123">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="b28de-123">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="b28de-124">Parametri</span><span class="sxs-lookup"><span data-stu-id="b28de-124">Parameters:</span></span>
   
   * <span data-ttu-id="b28de-125">**-a (o --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="b28de-125">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="b28de-126">Nome del gruppo hello in cui hello regola verrà creata.</span><span class="sxs-lookup"><span data-stu-id="b28de-126">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="b28de-127">Per questo scenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="b28de-127">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="b28de-128">**-n (o --nome)**.</span><span class="sxs-lookup"><span data-stu-id="b28de-128">**-n (or --name)**.</span></span> <span data-ttu-id="b28de-129">Nome nuova regola hello.</span><span class="sxs-lookup"><span data-stu-id="b28de-129">Name for hello new rule.</span></span> <span data-ttu-id="b28de-130">Per questo scenario, *rdp-rule*.</span><span class="sxs-lookup"><span data-stu-id="b28de-130">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="b28de-131">**-c (o --action)**.</span><span class="sxs-lookup"><span data-stu-id="b28de-131">**-c (or --action)**.</span></span> <span data-ttu-id="b28de-132">Livello di accesso per la regola di hello (Deny o Consenti).</span><span class="sxs-lookup"><span data-stu-id="b28de-132">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="b28de-133">**-p (o --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="b28de-133">**-p (or --protocol)**.</span></span> <span data-ttu-id="b28de-134">Protocollo (Tcp, Udp o *) per la regola di hello.</span><span class="sxs-lookup"><span data-stu-id="b28de-134">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="b28de-135">**-r (o --type)**.</span><span class="sxs-lookup"><span data-stu-id="b28de-135">**-r (or --type)**.</span></span> <span data-ttu-id="b28de-136">Direzione di connessione (Inbound o Outbound).</span><span class="sxs-lookup"><span data-stu-id="b28de-136">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="b28de-137">**-y (o --priority)**.</span><span class="sxs-lookup"><span data-stu-id="b28de-137">**-y (or --priority)**.</span></span> <span data-ttu-id="b28de-138">Priorità per la regola di hello.</span><span class="sxs-lookup"><span data-stu-id="b28de-138">Priority for hello rule.</span></span>
   * <span data-ttu-id="b28de-139">**-f (o --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="b28de-139">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="b28de-140">Prefisso dell'indirizzo di origine in CIDR o con tag predefiniti.</span><span class="sxs-lookup"><span data-stu-id="b28de-140">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="b28de-141">**-o (o --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="b28de-141">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="b28de-142">Porta o intervallo di porte di origine.</span><span class="sxs-lookup"><span data-stu-id="b28de-142">Source port, or port range.</span></span>
   * <span data-ttu-id="b28de-143">**-e (o --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="b28de-143">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="b28de-144">Prefisso dell'indirizzo di destinazione in CIDR o con tag predefiniti.</span><span class="sxs-lookup"><span data-stu-id="b28de-144">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="b28de-145">**-u (o --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="b28de-145">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="b28de-146">Porta o intervallo di porte di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b28de-146">Destination port, or port range.</span></span>
5. <span data-ttu-id="b28de-147">Eseguire hello  **`azure network nsg rule create`**  toocreate comando una regola che consenta l'accesso tooport 80 (HTTP) da hello Internet.</span><span class="sxs-lookup"><span data-stu-id="b28de-147">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="b28de-148">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="b28de-148">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="b28de-149">Eseguire hello  **`azure network nsg subnet add`**  subnet front-end di comando toolink hello NSG toohello.</span><span class="sxs-lookup"><span data-stu-id="b28de-149">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    <span data-ttu-id="b28de-150">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="b28de-150">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="b28de-151">Come toocreate hello NSG per hello nuovamente terminare subnet</span><span class="sxs-lookup"><span data-stu-id="b28de-151">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="b28de-152">toocreate denominato di un gruppo denominato *back-end di NSG* a seconda dello scenario hello precedente, procedura hello riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="b28de-152">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="b28de-153">Eseguire hello  **`azure network nsg create`**  comando toocreate un gruppo.</span><span class="sxs-lookup"><span data-stu-id="b28de-153">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    <span data-ttu-id="b28de-154">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="b28de-154">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="b28de-155">Parametri</span><span class="sxs-lookup"><span data-stu-id="b28de-155">Parameters:</span></span>
   
   * <span data-ttu-id="b28de-156">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="b28de-156">**-l (or --location)**.</span></span> <span data-ttu-id="b28de-157">Area di Azure in cui hello nuovo gruppo verrà creato.</span><span class="sxs-lookup"><span data-stu-id="b28de-157">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="b28de-158">Per questo scenario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="b28de-158">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="b28de-159">**-n (o --nome)**.</span><span class="sxs-lookup"><span data-stu-id="b28de-159">**-n (or --name)**.</span></span> <span data-ttu-id="b28de-160">Nome per hello nuovo gruppo.</span><span class="sxs-lookup"><span data-stu-id="b28de-160">Name for hello new NSG.</span></span> <span data-ttu-id="b28de-161">Per questo scenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="b28de-161">For our scenario, *NSG-FrontEnd*.</span></span>
2. <span data-ttu-id="b28de-162">Eseguire hello  **`azure network nsg rule create`**  toocreate comando una regola che consenta l'accesso tooport 1433 (SQL) dalla subnet front-end hello.</span><span class="sxs-lookup"><span data-stu-id="b28de-162">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="b28de-163">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="b28de-163">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="b28de-164">Eseguire hello  **`azure network nsg rule create`**  toocreate comando una regola che nega l'accesso toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="b28de-164">Run hello **`azure network nsg rule create`** command toocreate a rule that denies access toohello Internet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    <span data-ttu-id="b28de-165">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="b28de-165">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="b28de-166">Eseguire hello  **`azure network nsg subnet add`**  comando toolink hello NSG toohello nuovamente terminare subnet.</span><span class="sxs-lookup"><span data-stu-id="b28de-166">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    <span data-ttu-id="b28de-167">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="b28de-167">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

