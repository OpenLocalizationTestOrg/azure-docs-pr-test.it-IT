---
title: Configurare un web application firewall - Gateway applicazione di Azure | Microsoft Docs
description: Questo articolo fornisce indicazioni su come iniziare a usare il firewall applicazione Web in un gateway applicazione nuovo o esistente.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: gwallace
ms.openlocfilehash: dab489a1c9fb7d4a51b9ccbce543b209bec23575
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="25d95-103">Configurare un web application firewall su un gateway applicazione nuovo o esistente</span><span class="sxs-lookup"><span data-stu-id="25d95-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="25d95-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="25d95-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="25d95-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="25d95-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="25d95-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="25d95-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="25d95-107">Informazioni su come creare un gateway applicazione abilitato per un firewall applicazione Web o su come aggiungere un firewall applicazione Web a un gateway applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="25d95-107">Learn how to create a web application firewall enabled Application Gateway or add web application firewall to an existing Application Gateway.</span></span>

<span data-ttu-id="25d95-108">Il firewall applicazione Web (WAF) nel gateway applicazione di Azure protegge le applicazioni Web dai comuni attacchi basati sul Web, come ad esempio gli attacchi SQL injection, gli attacchi di scripting intersito e il controllo delle sessioni.</span><span class="sxs-lookup"><span data-stu-id="25d95-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="25d95-109">Il gateway applicazione di Azure è un dispositivo di bilanciamento del carico di livello 7.</span><span class="sxs-lookup"><span data-stu-id="25d95-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="25d95-110">Fornisce richieste HTTP con routing delle prestazioni e failover tra server diversi, sia nel cloud che in locale.</span><span class="sxs-lookup"><span data-stu-id="25d95-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="25d95-111">Il gateway applicazione offre numerose funzionalità di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller), tra cui bilanciamento del carico HTTP, affinità di sessione basata su cookie, offload SSL (Secure Sockets Layer), probe di integrità personalizzati, supporto per più siti e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="25d95-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="25d95-112">Per un elenco completo delle funzionalità supportate, vedere la [panoramica del gateway applicazione](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="25d95-112">To find a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="25d95-113">L'articolo seguente illustra come [aggiungere il firewall applicazione Web a un gateway applicazione esistente](#add-web-application-firewall-to-an-existing-application-gateway) e [creare un gateway applicazione che usa il firewall applicazione Web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="25d95-113">The following article shows how to [add web application firewall to an existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![immagine dello scenario][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="25d95-115">Differenze di configurazione dei WAF</span><span class="sxs-lookup"><span data-stu-id="25d95-115">WAF configuration differences</span></span>

<span data-ttu-id="25d95-116">Se è stato letto l'argomento relativo alla [creazione di un gateway applicazione con PowerShell](application-gateway-create-gateway-arm.md), si conoscono le impostazioni dello SKU da configurare quando si crea un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="25d95-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand the SKU settings to configure when creating an Application Gateway.</span></span> <span data-ttu-id="25d95-117">WAF fornisce impostazioni aggiuntive da definire quando si configura lo SKU in un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="25d95-117">WAF provides additional settings to define when configuring the SKU on an Application Gateway.</span></span> <span data-ttu-id="25d95-118">Sul gateway applicazione non è invece necessario apportare altre modifiche.</span><span class="sxs-lookup"><span data-stu-id="25d95-118">There are no additional changes that you make on the Application Gateway itself.</span></span>

| <span data-ttu-id="25d95-119">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="25d95-119">**Setting**</span></span> | <span data-ttu-id="25d95-120">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="25d95-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="25d95-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="25d95-121">**SKU**</span></span> |<span data-ttu-id="25d95-122">Un gateway applicazione normale senza WAF supporta le dimensioni **Standard\_Small**, **Standard\_Medium** e **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="25d95-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="25d95-123">Con l'introduzione di WAF sono disponibili due SKU aggiuntive, **WAF\_Medium** e **WAF\_Large**.</span><span class="sxs-lookup"><span data-stu-id="25d95-123">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="25d95-124">WAF non è supportato sui gateway applicazione Small.</span><span class="sxs-lookup"><span data-stu-id="25d95-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="25d95-125">**Livello**</span><span class="sxs-lookup"><span data-stu-id="25d95-125">**Tier**</span></span> | <span data-ttu-id="25d95-126">I valori disponibili sono **Standard** o **WAF**.</span><span class="sxs-lookup"><span data-stu-id="25d95-126">The available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="25d95-127">Quando si usa un web application firewall, è necessario scegliere **WAF** .</span><span class="sxs-lookup"><span data-stu-id="25d95-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="25d95-128">**Modalità**</span><span class="sxs-lookup"><span data-stu-id="25d95-128">**Mode**</span></span> | <span data-ttu-id="25d95-129">Questa impostazione è la modalità di WAF.</span><span class="sxs-lookup"><span data-stu-id="25d95-129">This setting is the mode of WAF.</span></span> <span data-ttu-id="25d95-130">I valori consentiti sono **Rilevamento** e **Prevenzione**.</span><span class="sxs-lookup"><span data-stu-id="25d95-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="25d95-131">Quando il firewall WAF è configurato in modalità di rilevamento, tutte le minacce vengono archiviate in un file di log.</span><span class="sxs-lookup"><span data-stu-id="25d95-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="25d95-132">In modalità di prevenzione, gli eventi vengono comunque registrati, ma l'autore dell'attacco riceve una risposta di mancata autorizzazione 403 dal gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="25d95-132">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the Application Gateway.</span></span>|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a><span data-ttu-id="25d95-133">Aggiungere un firewall applicazione Web a un gateway applicazione esistente</span><span class="sxs-lookup"><span data-stu-id="25d95-133">Add web application firewall to an existing Application Gateway</span></span>

<span data-ttu-id="25d95-134">Assicurarsi di usare la versione più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25d95-134">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="25d95-135">Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="25d95-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="25d95-136">Accedere all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="25d95-136">Log in to your Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="25d95-137">Selezionare la sottoscrizione da usare per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="25d95-137">Select the subscription to use for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="25d95-138">Recuperare il gateway a cui si sta aggiungendo il web application firewall.</span><span class="sxs-lookup"><span data-stu-id="25d95-138">Retrieve the gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="25d95-139">Configurare la SKU del firewall applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="25d95-139">Configure the web application firewall sku.</span></span> <span data-ttu-id="25d95-140">Le dimensioni disponibili sono **WAF\_Large** e **WAF\_Medium**.</span><span class="sxs-lookup"><span data-stu-id="25d95-140">The available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="25d95-141">Quando viene usato Web application firewall, il livello deve essere **WAF** e la capacità deve essere confermata quando si imposta lo SKU.</span><span class="sxs-lookup"><span data-stu-id="25d95-141">When web application firewall is used the tier must be **WAF**, the capacity must be confirmed when setting the sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="25d95-142">Configurare le impostazioni WAF nel modo definito nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="25d95-142">Configure the WAF settings as defined in the following example:</span></span>

   <span data-ttu-id="25d95-143">Per**FirewallMode** , i valori disponibili sono rilevamento e prevenzione.</span><span class="sxs-lookup"><span data-stu-id="25d95-143">For **FirewallMode**, the available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="25d95-144">Aggiornare il gateway applicazione con le impostazioni definite nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="25d95-144">Update the Application Gateway with the settings defined in the preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="25d95-145">Questo comando aggiorna il gateway applicazione con il firewall applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="25d95-145">This command updates the Application Gateway with web application firewall.</span></span> <span data-ttu-id="25d95-146">Per informazioni su come visualizzare i log per il gateway applicazione, vedere l'argomento relativo alla [diagnostica del gateway applicazione](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="25d95-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your Application Gateway.</span></span> <span data-ttu-id="25d95-147">Per le implicazioni di sicurezza del WAF, i log devono essere esaminati a intervalli regolari per essere aggiornati sulle condizioni di sicurezza delle applicazioni web.</span><span class="sxs-lookup"><span data-stu-id="25d95-147">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="25d95-148">Creare un gateway applicazione con il web application firewall</span><span class="sxs-lookup"><span data-stu-id="25d95-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="25d95-149">I passaggi seguenti illustrano l'intero processo di creazione di un gateway applicazione con il web application firewall.</span><span class="sxs-lookup"><span data-stu-id="25d95-149">The following steps take you through the entire process from beginning to end for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="25d95-150">Assicurarsi di usare la versione più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25d95-150">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="25d95-151">Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="25d95-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="25d95-152">Accedere ad Azure eseguendo `Login-AzureRmAccount`; verrà richiesto di eseguire l'autenticazione con le proprie credenziali.</span><span class="sxs-lookup"><span data-stu-id="25d95-152">Log in to Azure by running `Login-AzureRmAccount`, you are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="25d95-153">Controllare le sottoscrizioni per l'account eseguendo `Get-AzureRmSubscription`</span><span class="sxs-lookup"><span data-stu-id="25d95-153">Check the subscriptions for the account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="25d95-154">Scegliere le sottoscrizioni ad Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="25d95-154">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="25d95-155">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="25d95-155">Create a resource group</span></span>

<span data-ttu-id="25d95-156">Creare un gruppo di risorse per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="25d95-156">Create a resource group for the Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="25d95-157">Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso</span><span class="sxs-lookup"><span data-stu-id="25d95-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="25d95-158">che viene usato come percorso predefinito per le risorse presenti in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="25d95-158">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="25d95-159">Assicurarsi che tutti i comandi per creare un gateway applicazione usino lo stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="25d95-159">Make sure that all commands to create an Application Gateway uses the same resource group.</span></span>

<span data-ttu-id="25d95-160">Nell'esempio precedente è stato creato un gruppo di risorse denominato "appgw-RG" e la località "Stati Uniti occidentali".</span><span class="sxs-lookup"><span data-stu-id="25d95-160">In the preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="25d95-161">Se è necessario configurare un probe personalizzato per il gateway applicazione, vedere [Creare un probe personalizzato per il gateway applicazione con PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="25d95-161">If you need to configure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="25d95-162">Per altre informazioni, vedere l'articolo relativo a [probe personalizzati e monitoraggio dell'integrità](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="25d95-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="25d95-163">Configurare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="25d95-163">Configure virtual network</span></span>

<span data-ttu-id="25d95-164">Il gateway applicazione richiede una propria subnet.</span><span class="sxs-lookup"><span data-stu-id="25d95-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="25d95-165">In questo passaggio si crea una rete virtuale con uno spazio degli indirizzi di 10.0.0.0/16 e due subnet, una per il gateway applicazione e una per i membri del pool di back-end.</span><span class="sxs-lookup"><span data-stu-id="25d95-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for the Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for the Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your Application Gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="25d95-166">Configurare l'indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="25d95-166">Configure public IP address</span></span>

<span data-ttu-id="25d95-167">Per gestire le richieste esterne, il gateway applicazione richiede un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="25d95-167">In order to handle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="25d95-168">Questo indirizzo IP pubblico non deve avere un `DomainNameLabel` definito per essere usato dal gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="25d95-168">This public IP address must not have a `DomainNameLabel` defined to be used by the Application Gateway.</span></span>

```powershell
# Create a public IP address for use with the Application Gateway. Defining the domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-the-application-gateway"></a><span data-ttu-id="25d95-169">Configurare il gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="25d95-169">Configure the Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool to hold the addresses or NICs for the application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload the authenication certificate that will be used to communicate with the backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path to .cer file>

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration to associate the public IP address with the Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure the certificate for the Application Gateway. This certificate is used to decrypt and re-encrypt the traffic on the Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>

# Create the HTTP listener for the Application Gateway. Assign the front-end ip configuration, port, and ssl certificate to use.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure the SKU of the Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define the SSL policy to use
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure the waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create the Application Gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="25d95-170">I gateway applicazione creati con la configurazione di base del firewall applicazione Web sono configurati con CRS 3.0 per la protezione.</span><span class="sxs-lookup"><span data-stu-id="25d95-170">Application Gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="25d95-171">Ottenere il nome DNS del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="25d95-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="25d95-172">Dopo avere creato il gateway, il passaggio successivo prevede la configurazione del front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="25d95-172">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="25d95-173">Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo.</span><span class="sxs-lookup"><span data-stu-id="25d95-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="25d95-174">Per assicurarsi che gli utenti finali possano raggiungere il gateway applicazione, è possibile usare un record CNAME che faccia riferimento all'endpoint pubblico del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="25d95-174">To ensure end users can hit the Application Gateway, a CNAME record can be used to point to the public endpoint of the Application Gateway.</span></span> <span data-ttu-id="25d95-175">[Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="25d95-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="25d95-176">Per configurare un alias, recuperare i dettagli del gateway applicazione e il relativo nome DNS/indirizzo IP usando l'elemento PublicIPAddress collegato al gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="25d95-176">To configure an alias, retrieve details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element attached to the Application Gateway.</span></span> <span data-ttu-id="25d95-177">Il nome DNS del gateway applicazione dovrà essere usato per creare un record CNAME che associ le due applicazioni Web a questo nome DNS.</span><span class="sxs-lookup"><span data-stu-id="25d95-177">The Application Gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="25d95-178">Non è consigliabile usare record A perché l'indirizzo VIP può cambiare al riavvio del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="25d95-178">The use of A-records is not recommended since the VIP may change on restart of Application Gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="25d95-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25d95-179">Next steps</span></span>

<span data-ttu-id="25d95-180">Per informazioni su come configurare la registrazione diagnostica, per registrare gli eventi che vengono rilevati o bloccati con il web application firewall, visitare [Registrazione diagnostica per il gateway applicazione](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="25d95-180">Learn how to configure diagnostic logging, to log the events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
