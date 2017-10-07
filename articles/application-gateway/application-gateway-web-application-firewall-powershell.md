---
title: firewall di applicazione web aaaConfigure - Gateway applicazione Azure | Documenti Microsoft
description: In questo articolo vengono fornite indicazioni su come toostart tramite web firewall applicazione su un Gateway applicazione nuova o esistente.
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
ms.openlocfilehash: bd2a69901f0ec0d6551d633e2588b74c3ab59a71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="31dcb-103">Configurare un web application firewall su un gateway applicazione nuovo o esistente</span><span class="sxs-lookup"><span data-stu-id="31dcb-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="31dcb-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="31dcb-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="31dcb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="31dcb-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="31dcb-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="31dcb-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="31dcb-107">Informazioni su come toocreate un firewall applicazione web abilitata Gateway applicazione oppure aggiungere tooan di firewall applicazione web esistente di Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="31dcb-107">Learn how toocreate a web application firewall enabled Application Gateway or add web application firewall tooan existing Application Gateway.</span></span>

<span data-ttu-id="31dcb-108">firewall applicazione web di Hello (WAF) nel Gateway di applicazione di Azure consente di proteggere le applicazioni web da attacchi basati sul web comuni quali attacchi SQL injection, attacchi di script e assume il controllo di sessione.</span><span class="sxs-lookup"><span data-stu-id="31dcb-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="31dcb-109">Il gateway applicazione di Azure è un dispositivo di bilanciamento del carico di livello 7.</span><span class="sxs-lookup"><span data-stu-id="31dcb-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="31dcb-110">Fornisce il failover, le prestazioni di routing di richieste HTTP tra server diversi, che si trovino in locale o cloud hello.</span><span class="sxs-lookup"><span data-stu-id="31dcb-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="31dcb-111">Il gateway applicazione offre numerose funzionalità di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller), tra cui bilanciamento del carico HTTP, affinità di sessione basata su cookie, offload SSL (Secure Sockets Layer), probe di integrità personalizzati, supporto per più siti e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="31dcb-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="31dcb-112">toofind un elenco completo delle funzionalità supportate, visitare: [Panoramica del Gateway applicazione](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="31dcb-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="31dcb-113">Hello articolo seguente viene illustrato come troppo[aggiungere tooan di firewall applicazione web esistente di Gateway applicazione](#add-web-application-firewall-to-an-existing-application-gateway) e [creare un Gateway di applicazione che utilizza firewall applicazione web](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="31dcb-113">hello following article shows how too[add web application firewall tooan existing Application Gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an Application Gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![immagine dello scenario][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="31dcb-115">Differenze di configurazione dei WAF</span><span class="sxs-lookup"><span data-stu-id="31dcb-115">WAF configuration differences</span></span>

<span data-ttu-id="31dcb-116">Se si è letto [creare un Gateway applicazione con PowerShell](application-gateway-create-gateway-arm.md), comprendere hello SKU impostazioni tooconfigure durante la creazione di un Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="31dcb-116">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand hello SKU settings tooconfigure when creating an Application Gateway.</span></span> <span data-ttu-id="31dcb-117">WAF fornisce toodefine impostazioni aggiuntive quando si configurano hello SKU di Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="31dcb-117">WAF provides additional settings toodefine when configuring hello SKU on an Application Gateway.</span></span> <span data-ttu-id="31dcb-118">Non sono presenti modifiche aggiuntive che verranno apportate hello Gateway applicazione stessa.</span><span class="sxs-lookup"><span data-stu-id="31dcb-118">There are no additional changes that you make on hello Application Gateway itself.</span></span>

| <span data-ttu-id="31dcb-119">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="31dcb-119">**Setting**</span></span> | <span data-ttu-id="31dcb-120">**Dettagli**</span><span class="sxs-lookup"><span data-stu-id="31dcb-120">**Details**</span></span>
|---|---|
|<span data-ttu-id="31dcb-121">**SKU**</span><span class="sxs-lookup"><span data-stu-id="31dcb-121">**SKU**</span></span> |<span data-ttu-id="31dcb-122">Un gateway applicazione normale senza WAF supporta le dimensioni **Standard\_Small**, **Standard\_Medium** e **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="31dcb-122">A normal Application Gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="31dcb-123">Introduzione di hello di WAF, non vi sono due SKU aggiuntive, **WAF\_Media** e **WAF\_grande**.</span><span class="sxs-lookup"><span data-stu-id="31dcb-123">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="31dcb-124">WAF non è supportato sui gateway applicazione Small.</span><span class="sxs-lookup"><span data-stu-id="31dcb-124">WAF is not supported on small Application Gateways.</span></span>|
|<span data-ttu-id="31dcb-125">**Livello**</span><span class="sxs-lookup"><span data-stu-id="31dcb-125">**Tier**</span></span> | <span data-ttu-id="31dcb-126">i valori disponibili Hello sono **Standard** o **WAF**.</span><span class="sxs-lookup"><span data-stu-id="31dcb-126">hello available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="31dcb-127">Quando si usa un web application firewall, è necessario scegliere **WAF** .</span><span class="sxs-lookup"><span data-stu-id="31dcb-127">When using web application firewall, **WAF** must be chosen.</span></span>|
|<span data-ttu-id="31dcb-128">**Modalità**</span><span class="sxs-lookup"><span data-stu-id="31dcb-128">**Mode**</span></span> | <span data-ttu-id="31dcb-129">Questa impostazione è la modalità di WAF hello.</span><span class="sxs-lookup"><span data-stu-id="31dcb-129">This setting is hello mode of WAF.</span></span> <span data-ttu-id="31dcb-130">I valori consentiti sono **Rilevamento** e **Prevenzione**.</span><span class="sxs-lookup"><span data-stu-id="31dcb-130">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="31dcb-131">Quando il firewall WAF è configurato in modalità di rilevamento, tutte le minacce vengono archiviate in un file di log.</span><span class="sxs-lookup"><span data-stu-id="31dcb-131">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="31dcb-132">In modalità di prevenzione, gli eventi vengono comunque registrati ma autore dell'attacco hello riceve una risposta di non autorizzato 403 dal Gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="31dcb-132">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello Application Gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="31dcb-133">Aggiungere tooan di firewall applicazione web esistente di Gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="31dcb-133">Add web application firewall tooan existing Application Gateway</span></span>

<span data-ttu-id="31dcb-134">Assicurarsi che si utilizza hello la versione più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31dcb-134">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="31dcb-135">Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="31dcb-135">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="31dcb-136">Accedi tooyour Account Azure.</span><span class="sxs-lookup"><span data-stu-id="31dcb-136">Log in tooyour Azure Account.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

2. <span data-ttu-id="31dcb-137">Selezionare hello toouse di sottoscrizione per questo scenario.</span><span class="sxs-lookup"><span data-stu-id="31dcb-137">Select hello subscription toouse for this scenario.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. <span data-ttu-id="31dcb-138">Recuperare gateway hello che si sta aggiungendo firewall applicazione web per.</span><span class="sxs-lookup"><span data-stu-id="31dcb-138">Retrieve hello gateway that you are adding web application firewall to.</span></span>

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. <span data-ttu-id="31dcb-139">Configurare hello web application firewall sku.</span><span class="sxs-lookup"><span data-stu-id="31dcb-139">Configure hello web application firewall sku.</span></span> <span data-ttu-id="31dcb-140">sono di dimensioni disponibili Hello **WAF\_grande** e **WAF\_Media**.</span><span class="sxs-lookup"><span data-stu-id="31dcb-140">hello available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="31dcb-141">Quando si utilizza firewall applicazione web deve essere livello hello **WAF**, capacità hello devono essere confermate durante l'impostazione sku hello.</span><span class="sxs-lookup"><span data-stu-id="31dcb-141">When web application firewall is used hello tier must be **WAF**, hello capacity must be confirmed when setting hello sku.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. <span data-ttu-id="31dcb-142">Configurare le impostazioni di hello WAF come definito nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="31dcb-142">Configure hello WAF settings as defined in hello following example:</span></span>

   <span data-ttu-id="31dcb-143">Per **FirewallMode**, i valori hello disponibili sono il rilevamento e prevenzione.</span><span class="sxs-lookup"><span data-stu-id="31dcb-143">For **FirewallMode**, hello available values are Prevention and Detection.</span></span>

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. <span data-ttu-id="31dcb-144">Aggiorna Gateway applicazione hello con impostazioni hello definite nel precedente passaggio hello.</span><span class="sxs-lookup"><span data-stu-id="31dcb-144">Update hello Application Gateway with hello settings defined in hello preceding step.</span></span>

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

<span data-ttu-id="31dcb-145">Questo comando Aggiorna Gateway applicazione hello con firewall applicazione web.</span><span class="sxs-lookup"><span data-stu-id="31dcb-145">This command updates hello Application Gateway with web application firewall.</span></span> <span data-ttu-id="31dcb-146">Visitare [diagnostica del Gateway applicazione](application-gateway-diagnostics.md) toounderstand come tooview Registra per il Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="31dcb-146">Visit [Application Gateway diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your Application Gateway.</span></span> <span data-ttu-id="31dcb-147">A causa di toohello sicurezza natura WAF, registri necessità toobe rivisto regolarmente condizioni di sicurezza hello toounderstand delle applicazioni web.</span><span class="sxs-lookup"><span data-stu-id="31dcb-147">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="31dcb-148">Creare un gateway applicazione con il web application firewall</span><span class="sxs-lookup"><span data-stu-id="31dcb-148">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="31dcb-149">Hello passaggi seguenti consentono hello intero processo da tooend di inizio per la creazione di un Gateway applicazione con firewall applicazione web.</span><span class="sxs-lookup"><span data-stu-id="31dcb-149">hello following steps take you through hello entire process from beginning tooend for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="31dcb-150">Assicurarsi che si utilizza hello la versione più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31dcb-150">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="31dcb-151">Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="31dcb-151">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="31dcb-152">Accedi tooAzure eseguendo `Login-AzureRmAccount`, si è tooauthenticate richiesta con le credenziali.</span><span class="sxs-lookup"><span data-stu-id="31dcb-152">Log in tooAzure by running `Login-AzureRmAccount`, you are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="31dcb-153">Controllare le sottoscrizioni di hello per account hello eseguendo`Get-AzureRmSubscription`</span><span class="sxs-lookup"><span data-stu-id="31dcb-153">Check hello subscriptions for hello account by running `Get-AzureRmSubscription`</span></span>

1. <span data-ttu-id="31dcb-154">Scegliere quali di toouse le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="31dcb-154">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a><span data-ttu-id="31dcb-155">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="31dcb-155">Create a resource group</span></span>

<span data-ttu-id="31dcb-156">Creare un gruppo di risorse per hello Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="31dcb-156">Create a resource group for hello Application Gateway.</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="31dcb-157">Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso</span><span class="sxs-lookup"><span data-stu-id="31dcb-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="31dcb-158">Questo percorso viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="31dcb-158">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="31dcb-159">Assicurarsi che tutti i comandi Usa toocreate un Gateway applicazione hello stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="31dcb-159">Make sure that all commands toocreate an Application Gateway uses hello same resource group.</span></span>

<span data-ttu-id="31dcb-160">In hello sopra riportato, è stato creato un gruppo di risorse denominato "Appgw-RG" e il percorso "Stati Uniti occidentali."</span><span class="sxs-lookup"><span data-stu-id="31dcb-160">In hello preceding example, we created a resource group called "appgw-RG" and location "West US."</span></span>

> [!NOTE]
> <span data-ttu-id="31dcb-161">Se è necessario tooconfigure un probe personalizzato per il Gateway applicazione, vedere [creare un Gateway applicazione con probe personalizzati usando PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="31dcb-161">If you need tooconfigure a custom probe for your Application Gateway, see [Create an Application Gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="31dcb-162">Per altre informazioni, vedere l'articolo relativo a [probe personalizzati e monitoraggio dell'integrità](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="31dcb-162">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

### <a name="configure-virtual-network"></a><span data-ttu-id="31dcb-163">Configurare la rete virtuale</span><span class="sxs-lookup"><span data-stu-id="31dcb-163">Configure virtual network</span></span>

<span data-ttu-id="31dcb-164">Il gateway applicazione richiede una propria subnet.</span><span class="sxs-lookup"><span data-stu-id="31dcb-164">Application Gateway requires a subnet of its own.</span></span> <span data-ttu-id="31dcb-165">In questo passaggio creare una rete virtuale con uno spazio degli indirizzi di 10.0.0.0/16 e due subnet, uno per il Gateway applicazione hello e uno per i membri del pool back-end.</span><span class="sxs-lookup"><span data-stu-id="31dcb-165">In this step, you create a virtual network with an address space of 10.0.0.0/16 and two subnets, one for hello Application Gateway and one for backend pool members.</span></span>

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a><span data-ttu-id="31dcb-166">Configurare l'indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="31dcb-166">Configure public IP address</span></span>

<span data-ttu-id="31dcb-167">In ordine toohandle le richieste esterne, i Gateway applicazione richiede un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="31dcb-167">In order toohandle external requests, Application Gateway requires a public IP address.</span></span> <span data-ttu-id="31dcb-168">Questo indirizzo IP pubblico non deve avere un `DomainNameLabel` definito toobe utilizzato da hello Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="31dcb-168">This public IP address must not have a `DomainNameLabel` defined toobe used by hello Application Gateway.</span></span>

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a><span data-ttu-id="31dcb-169">Configurare hello Gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="31dcb-169">Configure hello Application Gateway</span></span>

```powershell
# Create a IP configuration. This configures what subnet hello Application Gateway uses. When Application Gateway starts, it picks up an IP address from hello subnet configured and routes network traffic toohello IP addresses in hello back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet

# Create a backend pool toohold hello addresses or NICs for hello application that Application Gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Upload hello authenication certificate that will be used toocommunicate with hello backend servers
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path too.cer file>

# Conifugre hello backend HTTP settings toobe used toodefine how traffic is routed toohello backend pool. hello authenication certificate used in hello previous step is added toohello backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert

# Create a frontend port toobe used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443

# Create a frontend IP configuration tooassociate hello public IP address with hello Application Gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Configure hello certificate for hello Application Gateway. This certificate is used toodecrypt and re-encrypt hello traffic on hello Application Gateway.
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>

# Create hello HTTP listener for hello Application Gateway. Assign hello front-end ip configuration, port, and ssl certificate toouse.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

#Create a load balancer routing rule that configures hello load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU of hello Application Gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Define hello SSL policy toouse
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

#Configure hello waf configuration settings.
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"

# Create hello Application Gateway utilizing all hello previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> <span data-ttu-id="31dcb-170">Gateway applicazione creati con configurazione del firewall applicazione web di base hello sono configurati con CRS 3.0 per la protezione.</span><span class="sxs-lookup"><span data-stu-id="31dcb-170">Application Gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="31dcb-171">Ottenere il nome DNS del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="31dcb-171">Get Application Gateway DNS name</span></span>

<span data-ttu-id="31dcb-172">Una volta creato il gateway hello passaggio successivo hello è tooconfigure hello front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="31dcb-172">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="31dcb-173">Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo.</span><span class="sxs-lookup"><span data-stu-id="31dcb-173">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="31dcb-174">gli utenti finali tooensure possibile raggiungere il Gateway applicazione hello, un record CNAME può essere utilizzati toopoint endpoint pubblico di toohello di Gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="31dcb-174">tooensure end users can hit hello Application Gateway, a CNAME record can be used toopoint toohello public endpoint of hello Application Gateway.</span></span> <span data-ttu-id="31dcb-175">[Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="31dcb-175">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="31dcb-176">tooconfigure un alias, recuperare i dettagli del Gateway applicazione hello e il relativo nome IP/DNS associato utilizzando hello PublicIPAddress elemento collegata toohello Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="31dcb-176">tooconfigure an alias, retrieve details of hello Application Gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello Application Gateway.</span></span> <span data-ttu-id="31dcb-177">nome DNS del Gateway applicazione Hello deve essere utilizzato toocreate un record CNAME, il nome DNS punti hello due web applicazioni toothis.</span><span class="sxs-lookup"><span data-stu-id="31dcb-177">hello Application Gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="31dcb-178">utilizzo di Hello del record non è consigliato poiché hello VIP potrebbe cambiare al riavvio del Gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="31dcb-178">hello use of A-records is not recommended since hello VIP may change on restart of Application Gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="31dcb-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31dcb-179">Next steps</span></span>

<span data-ttu-id="31dcb-180">Informazioni su come la registrazione diagnostica tooconfigure, toolog hello gli eventi rilevati o prevenire firewall applicazione web, visitare il sito [diagnostica del Gateway applicazione](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="31dcb-180">Learn how tooconfigure diagnostic logging, toolog hello events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
