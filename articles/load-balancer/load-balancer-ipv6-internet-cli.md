---
title: 'Creare un servizio di bilanciamento del carico con connessione Internet con IPv6: interfaccia della riga di comando di Azure | Documentazione Microsoft'
description: Informazioni sulla creazione di un servizio di bilanciamento del carico con connessione Internet con IPv6 in Azure Resource Manager usando l'interfaccia della riga di comando di Azure
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
ms.openlocfilehash: efb4771800c42df544c3cc37d1d164045fdcaf3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-the-azure-cli"></a><span data-ttu-id="937bd-104">Creare un servizio di bilanciamento del carico con connessione Internet con IPv6 in Azure Resource Manager usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="937bd-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="937bd-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="937bd-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="937bd-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="937bd-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="937bd-107">Modello</span><span class="sxs-lookup"><span data-stu-id="937bd-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="937bd-108">Azure Load Balancer è un servizio di bilanciamento del carico di livello 4 (TCP, UDP).</span><span class="sxs-lookup"><span data-stu-id="937bd-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="937bd-109">Il servizio di bilanciamento del carico offre disponibilità elevata distribuendo il traffico in ingresso tra istanze del servizio integre in servizi cloud o macchine virtuali in un set di bilanciamento del carico .</span><span class="sxs-lookup"><span data-stu-id="937bd-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="937bd-110">Azure Load Balancer può anche presentare tali servizi su più porte, più indirizzi IP o entrambi.</span><span class="sxs-lookup"><span data-stu-id="937bd-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="937bd-111">Scenario di distribuzione di esempio</span><span class="sxs-lookup"><span data-stu-id="937bd-111">Example deployment scenario</span></span>

<span data-ttu-id="937bd-112">Il diagramma seguente illustra la soluzione di bilanciamento del carico distribuita usando il modello di esempio descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="937bd-112">The following diagram illustrates the load balancing solution being deployed using the example template described in this article.</span></span>

![Scenario del bilanciamento del carico](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="937bd-114">In questo scenario si creeranno le seguenti risorse di Azure:</span><span class="sxs-lookup"><span data-stu-id="937bd-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="937bd-115">due macchine virtuali (VM)</span><span class="sxs-lookup"><span data-stu-id="937bd-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="937bd-116">un'interfaccia di rete virtuale per ogni VM con l'assegnazione degli indirizzi IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="937bd-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="937bd-117">un servizio di bilanciamento del carico con connessione Internet con un indirizzo IP pubblico IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="937bd-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="937bd-118">un set di disponibilità contenente le due macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="937bd-118">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="937bd-119">due regole di bilanciamento del carico per eseguire il mapping degli indirizzi VIP pubblici agli endpoint privati</span><span class="sxs-lookup"><span data-stu-id="937bd-119">two load balancing rules to map the public VIPs to the private endpoints</span></span>

## <a name="deploying-the-solution-using-the-azure-cli"></a><span data-ttu-id="937bd-120">Distribuzione della soluzione tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="937bd-120">Deploying the solution using the Azure CLI</span></span>

<span data-ttu-id="937bd-121">La procedura seguente illustra come creare un servizio di bilanciamento del carico Internet usando Azure Resource Manager con l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="937bd-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="937bd-122">Con Azure Resource Manager ogni risorsa viene creata e configurata singolarmente e quindi integrata per creare una risorsa.</span><span class="sxs-lookup"><span data-stu-id="937bd-122">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="937bd-123">Per distribuire un servizio di bilanciamento del carico è necessario creare e configurare gli oggetti seguenti:</span><span class="sxs-lookup"><span data-stu-id="937bd-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="937bd-124">Configurazione di IP front-end: contiene gli indirizzi IP pubblici per il traffico di rete in ingresso.</span><span class="sxs-lookup"><span data-stu-id="937bd-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="937bd-125">Pool di indirizzi back-end: contiene interfacce di rete (NIC) per le macchine virtuali per la ricezione di traffico di rete dal servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="937bd-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="937bd-126">Regole di bilanciamento del carico: contengono regole per il mapping di una porta pubblica nel servizio di bilanciamento del carico alle porte nel pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="937bd-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="937bd-127">Regole NAT in ingresso: contengono regole per il mapping di una porta pubblica nel servizio di bilanciamento del carico a una porta per una macchina virtuale specifica nel pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="937bd-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="937bd-128">Probe: contengono probe di integrità usati per verificare la disponibilità di istanze di macchine virtuali nel pool di indirizzi back-end.</span><span class="sxs-lookup"><span data-stu-id="937bd-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="937bd-129">Per altre informazioni, vedere [Supporto di Azure Resource Manager per Load Balancer](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="937bd-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-to-use-azure-resource-manager"></a><span data-ttu-id="937bd-130">Configurare l'ambiente dell'interfaccia della riga di comando per l'uso di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="937bd-130">Set up your CLI environment to use Azure Resource Manager</span></span>

<span data-ttu-id="937bd-131">Per questo esempio verranno eseguiti gli strumenti dell'interfaccia della riga di comando in una finestra di comando di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="937bd-131">For this example, we are running the CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="937bd-132">Non verranno usati i cmdlet di Azure PowerShell, ma le funzionalità di script di PowerShell per migliorare la leggibilità e il riutilizzo.</span><span class="sxs-lookup"><span data-stu-id="937bd-132">We are not using the Azure PowerShell cmdlets but we use PowerShell's scripting capabilities to improve readability and reuse.</span></span>

1. <span data-ttu-id="937bd-133">Se l'interfaccia della riga di comando di Azure non è mai stata usata, vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md) e seguire le istruzioni fino al punto in cui si selezionano l'account e la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="937bd-133">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="937bd-134">Eseguire il comando **azure config mode** per passare alla modalità Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="937bd-134">Run the **azure config mode** command to switch to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="937bd-135">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="937bd-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="937bd-136">Accedere ad Azure e ottenere un elenco delle sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="937bd-136">Sign in to Azure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="937bd-137">Immettere le credenziali di Azure quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="937bd-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="937bd-138">Selezionare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="937bd-138">Pick the subscription you want to use.</span></span> <span data-ttu-id="937bd-139">Prendere nota dell'ID sottoscrizione per il passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="937bd-139">Make note of the subscription Id for the next step.</span></span>

4. <span data-ttu-id="937bd-140">Impostare le variabili di PowerShell per l'uso con i comandi dell'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="937bd-140">Set up PowerShell variables for use with the CLI commands.</span></span>

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

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="937bd-141">Creare un gruppo di risorse, un servizio di bilanciamento del carico, una rete virtuale e subnet</span><span class="sxs-lookup"><span data-stu-id="937bd-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="937bd-142">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="937bd-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="937bd-143">Creare un servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="937bd-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="937bd-144">Creare una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="937bd-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="937bd-145">Creare due subnet nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="937bd-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-the-front-end-pool"></a><span data-ttu-id="937bd-146">Creare indirizzi IP pubblici per il pool front-end</span><span class="sxs-lookup"><span data-stu-id="937bd-146">Create public IP addresses for the front-end pool</span></span>

1. <span data-ttu-id="937bd-147">Configurare le variabili di PowerShell</span><span class="sxs-lookup"><span data-stu-id="937bd-147">Set up the PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="937bd-148">Creare un indirizzo IP pubblico per il pool IP front-end.</span><span class="sxs-lookup"><span data-stu-id="937bd-148">Create a public IP address the front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="937bd-149">Il servizio di bilanciamento del carico usa l'etichetta di dominio dell'indirizzo IP pubblico come nome di dominio completo.</span><span class="sxs-lookup"><span data-stu-id="937bd-149">The load balancer uses the domain label of the public IP as its FQDN.</span></span> <span data-ttu-id="937bd-150">Si tratta di una differenza rispetto alla distribuzione classica, che usa il nome del servizio cloud come nome di dominio completo del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="937bd-150">This a change from classic deployment, which uses the cloud service name as the load balancer FQDN.</span></span>
    > <span data-ttu-id="937bd-151">In questo esempio, il nome di dominio completo è *contoso09152016.southcentralus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="937bd-151">In this example, the FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="937bd-152">Creare pool front-end e back-end</span><span class="sxs-lookup"><span data-stu-id="937bd-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="937bd-153">Questo esempio crea il pool di indirizzi IP front-end che riceve il traffico in ingresso per il servizio di bilanciamento del carico e il pool di indirizzi IP back-end a cui il pool front-end invia il traffico di rete con bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="937bd-153">This example creates the front-end IP pool that receives the incoming network traffic on the load balancer and the back-end IP pool where the front-end pool sends the load balanced network traffic.</span></span>

1. <span data-ttu-id="937bd-154">Configurare le variabili di PowerShell</span><span class="sxs-lookup"><span data-stu-id="937bd-154">Set up the PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="937bd-155">Creare un pool di indirizzi IP front-end che associa l'indirizzo IP pubblico creato nel passaggio precedente e il servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="937bd-155">Create a front-end IP pool associating the public IP created in the previous step and the load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-the-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="937bd-156">Creare il probe, le regole NAT e le regole di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="937bd-156">Create the probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="937bd-157">Questo esempio crea gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="937bd-157">This example creates the following items:</span></span>

* <span data-ttu-id="937bd-158">una regola probe per verificare la connettività alla porta TCP 80</span><span class="sxs-lookup"><span data-stu-id="937bd-158">a probe rule to check for connectivity to TCP port 80</span></span>
* <span data-ttu-id="937bd-159">una regola NAT per la conversione di tutto il traffico in ingresso nella porta 3389 alla porta 3389 per RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="937bd-159">a NAT rule to translate all incoming traffic on port 3389 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="937bd-160">una regola NAT per la conversione di tutto il traffico in ingresso nella porta 3391 alla porta 3389 per RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="937bd-160">a NAT rule to translate all incoming traffic on port 3391 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="937bd-161">Regola del servizio di bilanciamento del carico per il bilanciamento di tutto il traffico in ingresso sulla porta 80 verso la porta 80 negli indirizzi nel pool back-end.</span><span class="sxs-lookup"><span data-stu-id="937bd-161">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>

<span data-ttu-id="937bd-162"><sup>1</sup> Le regole NAT vengono associate a un'istanza di macchina virtuale specifica dietro al servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="937bd-162"><sup>1</sup> NAT rules are associated to a specific virtual machine instance behind the load balancer.</span></span> <span data-ttu-id="937bd-163">Il traffico di rete in arrivo sulla porta 3389 viene inviato alla specifica macchina virtuale e alla porta associata alla regola NAT.</span><span class="sxs-lookup"><span data-stu-id="937bd-163">The network traffic arriving on port 3389 is sent to the specific virtual machine and port associated with the NAT rule.</span></span> <span data-ttu-id="937bd-164">È necessario specificare un protocollo (UDP o TCP) per una regola NAT.</span><span class="sxs-lookup"><span data-stu-id="937bd-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="937bd-165">Entrambi i protocolli non possono essere assegnati alla stessa porta.</span><span class="sxs-lookup"><span data-stu-id="937bd-165">Both protocols can't be assigned to the same port.</span></span>

1. <span data-ttu-id="937bd-166">Configurare le variabili di PowerShell</span><span class="sxs-lookup"><span data-stu-id="937bd-166">Set up the PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="937bd-167">Creare il probe</span><span class="sxs-lookup"><span data-stu-id="937bd-167">Create the probe</span></span>

    <span data-ttu-id="937bd-168">L'esempio seguente crea un probe TCP che verifica la connettività alla porta TCP di back-end 80 ogni 15 secondi.</span><span class="sxs-lookup"><span data-stu-id="937bd-168">The following example creates a TCP probe that checks for connectivity to back-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="937bd-169">Contrassegna la risorsa back-end come non disponibile dopo due tentativi consecutivi non riusciti.</span><span class="sxs-lookup"><span data-stu-id="937bd-169">It will mark the back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="937bd-170">Creare regole NAT in ingresso che consentano connessioni RDP alle risorse back-end</span><span class="sxs-lookup"><span data-stu-id="937bd-170">Create inbound NAT rules that allow RDP connections to the back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="937bd-171">Creare regole del servizio di bilanciamento del carico che inviano il traffico a porte back-end diverse a seconda del front-end che ha ricevuto la richiesta</span><span class="sxs-lookup"><span data-stu-id="937bd-171">Create a load balancer rules that send traffic to different back-end ports depending on which front end received the request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="937bd-172">Verificare le impostazioni</span><span class="sxs-lookup"><span data-stu-id="937bd-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="937bd-173">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="937bd-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up the load balancer "myIPv4IPv6Lb"
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

## <a name="create-nics"></a><span data-ttu-id="937bd-174">Creare NIC</span><span class="sxs-lookup"><span data-stu-id="937bd-174">Create NICs</span></span>

<span data-ttu-id="937bd-175">Creare schede di interfaccia di rete e associarle a regole NAT, regole del servizio di bilanciamento del carico e probe.</span><span class="sxs-lookup"><span data-stu-id="937bd-175">Create NICs and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="937bd-176">Configurare le variabili di PowerShell</span><span class="sxs-lookup"><span data-stu-id="937bd-176">Set up the PowerShell variables</span></span>

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

2. <span data-ttu-id="937bd-177">Creare una scheda di interfaccia di rete per ogni back-end e aggiungere una configurazione di IPv6.</span><span class="sxs-lookup"><span data-stu-id="937bd-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-the-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="937bd-178">Creare le risorse delle macchine virtuali back-end e collegare ogni scheda di interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="937bd-178">Create the back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="937bd-179">Per creare le macchine virtuali è necessario un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="937bd-179">To create VMs, you must have a storage account.</span></span> <span data-ttu-id="937bd-180">Per il bilanciamento del carico, le macchine virtuali devono essere membri di un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="937bd-180">For load balancing, the VMs need to be members of an availability set.</span></span> <span data-ttu-id="937bd-181">Per altre informazioni sulla creazione di VM, vedere [Creare una VM di Azure con PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="937bd-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="937bd-182">Configurare le variabili di PowerShell</span><span class="sxs-lookup"><span data-stu-id="937bd-182">Set up the PowerShell variables</span></span>

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
    > <span data-ttu-id="937bd-183">Questo esempio usa il nome utente e la password per le macchine virtuali in testo non crittografato.</span><span class="sxs-lookup"><span data-stu-id="937bd-183">This example uses the username and password for the VMs in clear text.</span></span> <span data-ttu-id="937bd-184">È necessario prestare attenzione quando si usano credenziali non crittografate.</span><span class="sxs-lookup"><span data-stu-id="937bd-184">Appropriate care must be taken when using credentials in the clear.</span></span> <span data-ttu-id="937bd-185">Per un metodo più sicuro per la gestione delle credenziali in PowerShell, vedere il cmdlet [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) .</span><span class="sxs-lookup"><span data-stu-id="937bd-185">For a more secure method of handling credentials in PowerShell, see the [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="937bd-186">Creare l'account di archiviazione e il set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="937bd-186">Create the storage account and availability set</span></span>

    <span data-ttu-id="937bd-187">È possibile usare un account di archiviazione esistente quando si creano le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="937bd-187">You may use an existing storage account when you create the VMs.</span></span> <span data-ttu-id="937bd-188">Il comando seguente consente di creare un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="937bd-188">The following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="937bd-189">Creare quindi il set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="937bd-189">Next, create the availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="937bd-190">Creare le macchine virtuali con le schede di interfaccia di rete associate</span><span class="sxs-lookup"><span data-stu-id="937bd-190">Create the virtual machines with the associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="937bd-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="937bd-191">Next steps</span></span>

[<span data-ttu-id="937bd-192">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="937bd-192">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="937bd-193">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="937bd-193">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="937bd-194">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="937bd-194">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
