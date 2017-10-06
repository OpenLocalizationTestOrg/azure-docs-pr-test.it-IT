---
title: bilanciamento del carico aaaCreate con una connessione Internet con IPv6 - CLI di Azure | Documenti Microsoft
description: Informazioni su come toocreate un Internet rivolto al bilanciamento del carico con IPv6 in Gestione risorse di Azure utilizzando hello CLI di Azure
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: ipv6, azure load balancer, dual stack, ip pubblico, ipv6 nativo, mobili, iot
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a><span data-ttu-id="d7873-104">Creare un servizio di bilanciamento del carico con IPv6 in Gestione di risorse di Azure mediante Azure CLI hello per Internet</span><span class="sxs-lookup"><span data-stu-id="d7873-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d7873-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d7873-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="d7873-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="d7873-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="d7873-107">Modello</span><span class="sxs-lookup"><span data-stu-id="d7873-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="d7873-108">Azure Load Balancer è un servizio di bilanciamento del carico di livello 4 (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="d7873-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="d7873-109">servizio di bilanciamento del carico Hello garantisce disponibilità elevata mediante la distribuzione del traffico in entrata tra le istanze del servizio di integrità in servizi cloud o macchine virtuali in un set di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="d7873-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="d7873-110">Azure Load Balancer può anche presentare tali servizi su più porte, più indirizzi IP o entrambi.</span><span class="sxs-lookup"><span data-stu-id="d7873-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="d7873-111">Scenario di distribuzione di esempio</span><span class="sxs-lookup"><span data-stu-id="d7873-111">Example deployment scenario</span></span>

<span data-ttu-id="d7873-112">Hello diagramma seguente vengono illustrate soluzioni di bilanciamento del carico di hello distribuito utilizzando il modello di esempio hello descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d7873-112">hello following diagram illustrates hello load balancing solution being deployed using hello example template described in this article.</span></span>

![Scenario del bilanciamento del carico](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="d7873-114">In questo scenario creerai hello seguendo le risorse di Azure:</span><span class="sxs-lookup"><span data-stu-id="d7873-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="d7873-115">due macchine virtuali (VM)</span><span class="sxs-lookup"><span data-stu-id="d7873-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="d7873-116">un'interfaccia di rete virtuale per ogni VM con l'assegnazione degli indirizzi IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="d7873-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="d7873-117">un servizio di bilanciamento del carico con connessione Internet con un indirizzo IP pubblico IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="d7873-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="d7873-118">un Set di disponibilità toothat contiene macchine virtuali hello due</span><span class="sxs-lookup"><span data-stu-id="d7873-118">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="d7873-119">due bilanciamento regole toomap hello VIP toohello privato endpoint pubblici di carico</span><span class="sxs-lookup"><span data-stu-id="d7873-119">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="d7873-120">La distribuzione di soluzioni hello utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="d7873-120">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="d7873-121">Hello alla procedura seguente viene illustrato come una connessione Internet toocreate bilanciamento del carico con Gestione risorse di Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d7873-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="d7873-122">Con Gestione risorse di Azure, ogni risorsa viene creata e configurata individualmente e riunire toocreate una risorsa.</span><span class="sxs-lookup"><span data-stu-id="d7873-122">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="d7873-123">toodeploy un bilanciamento del carico, per creare e configurare hello seguenti oggetti:</span><span class="sxs-lookup"><span data-stu-id="d7873-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="d7873-124">Configurazione di IP front-end: contiene gli indirizzi IP pubblici per il traffico di rete in ingresso.</span><span class="sxs-lookup"><span data-stu-id="d7873-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="d7873-125">Pool di indirizzi di back-end - contiene le interfacce di rete (NIC) per tooreceive il traffico di rete dal servizio di bilanciamento del carico hello hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="d7873-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="d7873-126">Regole di bilanciamento del carico - contiene le regole di mapping di una porta pubblica su tooport del servizio di bilanciamento carico di hello nel pool di indirizzi back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="d7873-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="d7873-127">Regole NAT in ingresso - contiene le regole di mapping di una porta pubblica nella porta di tooa del bilanciamento del carico hello per una macchina virtuale specifica nel pool di indirizzi back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="d7873-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="d7873-128">Probe - contiene integrità probe usati toocheck disponibilità delle istanze di macchine virtuali nel pool di indirizzi back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="d7873-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="d7873-129">Per altre informazioni, vedere [Supporto di Azure Resource Manager per Load Balancer](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="d7873-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a><span data-ttu-id="d7873-130">Impostare il toouse ambiente CLI Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="d7873-130">Set up your CLI environment toouse Azure Resource Manager</span></span>

<span data-ttu-id="d7873-131">Per questo esempio, gli strumenti CLI hello in esecuzione in una finestra di comando di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7873-131">For this example, we are running hello CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="d7873-132">Non si sono utilizzando i cmdlet di Azure PowerShell hello ma si utilizza la leggibilità tooimprove funzionalità script di PowerShell e il riutilizzo.</span><span class="sxs-lookup"><span data-stu-id="d7873-132">We are not using hello Azure PowerShell cmdlets but we use PowerShell's scripting capabilities tooimprove readability and reuse.</span></span>

1. <span data-ttu-id="d7873-133">Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d7873-133">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="d7873-134">Eseguire hello **azure configurazione modalità** modalità Manager tooResource tooswitch di comando.</span><span class="sxs-lookup"><span data-stu-id="d7873-134">Run hello **azure config mode** command tooswitch tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="d7873-135">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="d7873-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="d7873-136">Accedi tooAzure e ottenere un elenco di sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="d7873-136">Sign in tooAzure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="d7873-137">Immettere le credenziali di Azure quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="d7873-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="d7873-138">Selezionare la sottoscrizione di hello da toouse.</span><span class="sxs-lookup"><span data-stu-id="d7873-138">Pick hello subscription you want toouse.</span></span> <span data-ttu-id="d7873-139">Prendere nota dell'Id sottoscrizione hello per successiva hello.</span><span class="sxs-lookup"><span data-stu-id="d7873-139">Make note of hello subscription Id for hello next step.</span></span>

4. <span data-ttu-id="d7873-140">Impostare le variabili di PowerShell per l'utilizzo con i comandi CLI hello.</span><span class="sxs-lookup"><span data-stu-id="d7873-140">Set up PowerShell variables for use with hello CLI commands.</span></span>

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="d7873-141">Creare un gruppo di risorse, un servizio di bilanciamento del carico, una rete virtuale e subnet</span><span class="sxs-lookup"><span data-stu-id="d7873-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="d7873-142">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="d7873-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="d7873-143">Creare un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="d7873-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="d7873-144">Creare una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d7873-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="d7873-145">Creare due subnet nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d7873-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a><span data-ttu-id="d7873-146">Creare gli indirizzi IP pubblici per il pool di server front-end hello</span><span class="sxs-lookup"><span data-stu-id="d7873-146">Create public IP addresses for hello front-end pool</span></span>

1. <span data-ttu-id="d7873-147">Impostare le variabili PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="d7873-147">Set up hello PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="d7873-148">Creare un pubblico hello front-end IP pool di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="d7873-148">Create a public IP address hello front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="d7873-149">bilanciamento del carico di Hello Usa etichetta hello del dominio dell'indirizzo IP pubblico hello come il nome di dominio completo.</span><span class="sxs-lookup"><span data-stu-id="d7873-149">hello load balancer uses hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="d7873-150">Questa distribuzione classica, che utilizza nome del servizio cloud hello come servizio di bilanciamento del carico FQDN hello una modifica.</span><span class="sxs-lookup"><span data-stu-id="d7873-150">This a change from classic deployment, which uses hello cloud service name as hello load balancer FQDN.</span></span>
    > <span data-ttu-id="d7873-151">In questo esempio, hello FQDN è *contoso09152016.southcentralus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="d7873-151">In this example, hello FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="d7873-152">Creare pool front-end e back-end</span><span class="sxs-lookup"><span data-stu-id="d7873-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="d7873-153">Questo esempio crea pool IP front-end hello che riceve il traffico di rete in ingresso di hello nel servizio di bilanciamento del carico hello e pool IP back-end di hello in pool front-end hello invia il traffico di rete con carico bilanciato hello.</span><span class="sxs-lookup"><span data-stu-id="d7873-153">This example creates hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello back-end IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="d7873-154">Impostare le variabili PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="d7873-154">Set up hello PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="d7873-155">Creare un pool IP front-end associazione hello creato nel passaggio precedente hello e bilanciamento del carico hello indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="d7873-155">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="d7873-156">Creare regole LB probe hello e le regole NAT</span><span class="sxs-lookup"><span data-stu-id="d7873-156">Create hello probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="d7873-157">In questo esempio crea hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="d7873-157">This example creates hello following items:</span></span>

* <span data-ttu-id="d7873-158">un toocheck regola probe per la porta 80 tooTCP di connettività</span><span class="sxs-lookup"><span data-stu-id="d7873-158">a probe rule toocheck for connectivity tooTCP port 80</span></span>
* <span data-ttu-id="d7873-159">un dispositivo NAT regola tootranslate tutto il traffico in ingresso sulla porta 3389 tooport 3389 per RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="d7873-159">a NAT rule tootranslate all incoming traffic on port 3389 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="d7873-160">un dispositivo NAT regola tootranslate tutto il traffico in ingresso sulla porta 3391 tooport 3389 per RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="d7873-160">a NAT rule tootranslate all incoming traffic on port 3391 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="d7873-161">un toobalance regola di bilanciamento carico di tutto il traffico in ingresso sulla porta 80 tooport 80 su hello indirizzi nel pool back-end hello.</span><span class="sxs-lookup"><span data-stu-id="d7873-161">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>

<span data-ttu-id="d7873-162"><sup>1</sup> le regole NAT sono associati tooa macchina virtuale specifica istanza bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="d7873-162"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="d7873-163">macchina virtuale specifica toohello e la porta associata alla regola NAT hello, viene inviato il traffico di rete Hello in arrivo sulla porta 3389.</span><span class="sxs-lookup"><span data-stu-id="d7873-163">hello network traffic arriving on port 3389 is sent toohello specific virtual machine and port associated with hello NAT rule.</span></span> <span data-ttu-id="d7873-164">È necessario specificare un protocollo (UDP o TCP) per una regola NAT.</span><span class="sxs-lookup"><span data-stu-id="d7873-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="d7873-165">Entrambi i protocolli non possono essere assegnato toohello stessa porta.</span><span class="sxs-lookup"><span data-stu-id="d7873-165">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="d7873-166">Impostare le variabili PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="d7873-166">Set up hello PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="d7873-167">Creare il probe hello</span><span class="sxs-lookup"><span data-stu-id="d7873-167">Create hello probe</span></span>

    <span data-ttu-id="d7873-168">Hello seguente viene creato un probe TCP verifica per la porta TCP tooback-end di connettività 80 ogni 15 secondi.</span><span class="sxs-lookup"><span data-stu-id="d7873-168">hello following example creates a TCP probe that checks for connectivity tooback-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="d7873-169">Contrassegna risorsa back-end hello disponibile dopo due tentativi consecutivi non riusciti.</span><span class="sxs-lookup"><span data-stu-id="d7873-169">It will mark hello back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="d7873-170">Creare le regole NAT in ingresso che consentono le connessioni RDP risorse back-end toohello</span><span class="sxs-lookup"><span data-stu-id="d7873-170">Create inbound NAT rules that allow RDP connections toohello back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="d7873-171">Creazione di regole che il traffico toodifferent back-end le porte di trasmissione a seconda di quale richiesta hello front-end ha ricevuto un bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="d7873-171">Create a load balancer rules that send traffic toodifferent back-end ports depending on which front end received hello request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="d7873-172">Verificare le impostazioni</span><span class="sxs-lookup"><span data-stu-id="d7873-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="d7873-173">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="d7873-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a><span data-ttu-id="d7873-174">Creare NIC</span><span class="sxs-lookup"><span data-stu-id="d7873-174">Create NICs</span></span>

<span data-ttu-id="d7873-175">Creare schede di rete e associarli tooNAT regole, regole di bilanciamento del carico e probe.</span><span class="sxs-lookup"><span data-stu-id="d7873-175">Create NICs and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="d7873-176">Impostare le variabili PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="d7873-176">Set up hello PowerShell variables</span></span>

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. <span data-ttu-id="d7873-177">Creare una scheda di interfaccia di rete per ogni back-end e aggiungere una configurazione di IPv6.</span><span class="sxs-lookup"><span data-stu-id="d7873-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="d7873-178">Creare risorse macchina virtuale back-end di hello e associare ogni scheda di rete</span><span class="sxs-lookup"><span data-stu-id="d7873-178">Create hello back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="d7873-179">toocreate macchine virtuali, è necessario disporre di un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d7873-179">toocreate VMs, you must have a storage account.</span></span> <span data-ttu-id="d7873-180">Per il bilanciamento del carico, le macchine virtuali hello necessario toobe membri di un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="d7873-180">For load balancing, hello VMs need toobe members of an availability set.</span></span> <span data-ttu-id="d7873-181">Per altre informazioni sulla creazione di VM, vedere [Creare una VM di Azure con PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="d7873-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="d7873-182">Impostare le variabili PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="d7873-182">Set up hello PowerShell variables</span></span>

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > <span data-ttu-id="d7873-183">Questo esempio Usa hello username e password per le macchine virtuali hello in testo non crittografato.</span><span class="sxs-lookup"><span data-stu-id="d7873-183">This example uses hello username and password for hello VMs in clear text.</span></span> <span data-ttu-id="d7873-184">Appropriato prestare attenzione quando utilizzando le credenziali in hello deselezionare.</span><span class="sxs-lookup"><span data-stu-id="d7873-184">Appropriate care must be taken when using credentials in hello clear.</span></span> <span data-ttu-id="d7873-185">Per un metodo più sicuro per la gestione delle credenziali in PowerShell, vedere hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d7873-185">For a more secure method of handling credentials in PowerShell, see hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="d7873-186">Creare set di account e la disponibilità di archiviazione hello</span><span class="sxs-lookup"><span data-stu-id="d7873-186">Create hello storage account and availability set</span></span>

    <span data-ttu-id="d7873-187">Quando si crea hello macchine virtuali, è possibile utilizzare un account di archiviazione esistente.</span><span class="sxs-lookup"><span data-stu-id="d7873-187">You may use an existing storage account when you create hello VMs.</span></span> <span data-ttu-id="d7873-188">Hello comando seguente crea un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d7873-188">hello following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="d7873-189">Successivamente, creare set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="d7873-189">Next, create hello availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="d7873-190">Creare macchine virtuali hello con schede di rete hello associata</span><span class="sxs-lookup"><span data-stu-id="d7873-190">Create hello virtual machines with hello associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="d7873-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d7873-191">Next steps</span></span>

[<span data-ttu-id="d7873-192">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="d7873-192">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="d7873-193">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="d7873-193">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="d7873-194">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="d7873-194">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
