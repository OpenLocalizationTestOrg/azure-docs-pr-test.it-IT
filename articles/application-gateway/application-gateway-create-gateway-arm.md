---
title: aaaCreate e gestire un Gateway di applicazione di Azure - PowerShell | Documenti Microsoft
description: Questa pagina vengono fornite istruzioni toocreate, configurare, avviare ed eliminare un gateway applicazione Azure con Gestione risorse di Azure
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: ab98d5f9aa0dc309f8353b7f72591359e1121849
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a><span data-ttu-id="b6ee6-103">Creare, avviare o eliminare un gateway applicazione tramite Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="b6ee6-103">Create, start, or delete an application gateway by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b6ee6-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b6ee6-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="b6ee6-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b6ee6-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="b6ee6-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="b6ee6-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="b6ee6-107">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b6ee6-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="b6ee6-108">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b6ee6-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="b6ee6-109">Il gateway applicazione di Azure è un dispositivo di bilanciamento del carico di livello 7.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="b6ee6-110">Fornisce il failover e il routing delle prestazioni delle richieste HTTP tra server diversi, che si trovino in locale o cloud hello.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="b6ee6-111">Il gateway applicazione offre numerose funzionalità di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller), tra cui bilanciamento del carico HTTP, affinità di sessione basata su cookie, offload SSL (Secure Sockets Layer), probe di integrità personalizzati, supporto per più siti e molte altre.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="b6ee6-112">toofind un elenco completo delle funzionalità supportate, visitare [Panoramica di Gateway applicazione](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b6ee6-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md).</span></span>

<span data-ttu-id="b6ee6-113">Questo articolo vengono illustrati toocreate passaggi hello, configurare, avviare ed eliminare un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b6ee6-114">Prima di lavorare con le risorse di Azure, è importante toounderstand che Azure ha due modelli di distribuzione: gestione delle risorse e classica.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-114">Before you work with Azure resources, it is important toounderstand that Azure currently has two deployment models: Resource Manager and classic.</span></span> <span data-ttu-id="b6ee6-115">È importante conoscere i [modelli e gli strumenti di distribuzione](../azure-classic-rm.md) prima di usare le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-115">Make sure that you understand [deployment models and tools](../azure-classic-rm.md) before working with any Azure resource.</span></span> <span data-ttu-id="b6ee6-116">È possibile visualizzare la documentazione di hello per diversi strumenti facendo clic sulle schede hello nella parte superiore di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-116">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="b6ee6-117">Questo documento illustra la creazione di un gateway applicazione con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-117">This document covers creating an application gateway by using Azure Resource Manager.</span></span> <span data-ttu-id="b6ee6-118">versione classica hello toouse, andare troppo[creare una distribuzione di applicazioni gateway classico mediante PowerShell](application-gateway-create-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="b6ee6-118">toouse hello classic version, go too[Create an application gateway classic deployment by using PowerShell](application-gateway-create-gateway.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b6ee6-119">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="b6ee6-119">Before you begin</span></span>

1. <span data-ttu-id="b6ee6-120">Installare più recente dei cmdlet di Azure PowerShell hello hello utilizzando hello installazione guidata piattaforma Web.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-120">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="b6ee6-121">È possibile scaricare e installare la versione più recente di hello da hello **Windows PowerShell** sezione di hello [pagina di download](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b6ee6-121">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
1. <span data-ttu-id="b6ee6-122">Se si dispone di una rete virtuale esistente, selezionare una subnet vuota esistente o creare una subnet nella rete virtuale esistente esclusivamente per l'utilizzo dal gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-122">If you have an existing virtual network, either select an existing empty subnet or create a subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="b6ee6-123">Non è possibile distribuire hello applicazione gateway tooa rete virtuale diverso rispetto alle risorse di hello intendi toodeploy dietro gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-123">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway.</span></span>
1. <span data-ttu-id="b6ee6-124">deve esistere server Hello configurare gateway di applicazione hello toouse o disporre i relativi endpoint creato nella rete virtuale hello o con un indirizzo IP/VIP pubblico.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-124">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="b6ee6-125">Che cos'è toocreate necessario un gateway applicazione?</span><span class="sxs-lookup"><span data-stu-id="b6ee6-125">What is required toocreate an application gateway?</span></span>

* <span data-ttu-id="b6ee6-126">**Pool di server back-end:** elenco hello di schede di rete del server back-end hello, FQDN o indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-126">**Backend server pool:** hello list of IP addresses, FQDNs, or NICs of hello backend servers.</span></span> <span data-ttu-id="b6ee6-127">Se vengono utilizzati indirizzi IP, essi devono appartenere toohello subnet della rete virtuale o deve essere un indirizzo IP/VIP pubblico.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-127">If IP addresses are used, they should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="b6ee6-128">**Impostazioni del pool di server back-end:** ogni pool ha impostazioni come porta, protocollo e affinità basata sui cookie.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-128">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="b6ee6-129">Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-129">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="b6ee6-130">**porta front-end:** questa porta è una porta pubblica hello aperta sul gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-130">**frontend port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="b6ee6-131">Traffico raggiunge questa porta e quindi ottiene reindirizzato tooone dei server back-end hello.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-131">Traffic hits this port, and then gets redirected tooone of hello backend servers.</span></span>
* <span data-ttu-id="b6ee6-132">**Listener:** listener hello dispone di una porta di front-end, un protocollo (Http o Https, questi valori sono distinzione maiuscole/minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload).</span><span class="sxs-lookup"><span data-stu-id="b6ee6-132">**Listener:** hello listener has a frontend port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="b6ee6-133">**Regola:** regola hello associa listener hello, pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-133">**Rule:** hello rule binds hello listener, hello backend server pool and defines which backend server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="b6ee6-134">Creare un gruppo di risorse per Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="b6ee6-134">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="b6ee6-135">Assicurarsi che si utilizza hello la versione più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-135">Make sure that you are using hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="b6ee6-136">Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b6ee6-136">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

1. <span data-ttu-id="b6ee6-137">Accedi tooAzure e immettere le credenziali.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-137">Log in tooAzure and enter your credentials.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="b6ee6-138">Controllare le sottoscrizioni di hello per account hello.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-138">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="b6ee6-139">Scegliere quali di toouse le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-139">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
  ```

4. <span data-ttu-id="b6ee6-140">Creare un gruppo di risorse. Ignorare questo passaggio se si usa un gruppo di risorse esistente.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-140">Create a resource group (skip this step if you're using an existing resource group).</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name ContosoRG -Location "West US"
  ```

<span data-ttu-id="b6ee6-141">Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso</span><span class="sxs-lookup"><span data-stu-id="b6ee6-141">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="b6ee6-142">Questo percorso viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-142">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="b6ee6-143">Assicurarsi che tutti i comandi toocreate utilizza un gateway applicazione hello stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-143">Make sure that all commands toocreate an application gateway uses hello same resource group.</span></span>

<span data-ttu-id="b6ee6-144">Nell'esempio hello sopra, è stato creato un gruppo di risorse denominato **ContosoRG** e il percorso **Stati Uniti orientali**.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-144">In hello example above, we created a resource group called **ContosoRG** and location **East US**.</span></span>

> [!NOTE]
> <span data-ttu-id="b6ee6-145">Se è necessario tooconfigure un probe personalizzato per il gateway applicazione, visitare: [creare un gateway applicazione con probe personalizzati usando PowerShell](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b6ee6-145">If you need tooconfigure a custom probe for your application gateway, visit: [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md).</span></span> <span data-ttu-id="b6ee6-146">Per altre informazioni, vedere l'articolo relativo a [probe personalizzati e monitoraggio dell'integrità](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="b6ee6-146">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>


## <a name="create-hello-application-gateway-configuration-objects"></a><span data-ttu-id="b6ee6-147">Creare gli oggetti di configurazione di gateway applicazione hello</span><span class="sxs-lookup"><span data-stu-id="b6ee6-147">Create hello application gateway configuration objects</span></span>

<span data-ttu-id="b6ee6-148">Tutti gli elementi di configurazione necessario impostare prima di creare i gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-148">All configuration items must be set up before creating hello application gateway.</span></span> <span data-ttu-id="b6ee6-149">Hello seguenti passaggi necessari per creare hello gli elementi di configurazione necessari per una risorsa di gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-149">hello following steps create hello configuration items that are needed for an application gateway resource.</span></span>

```powershell
# Create a subnet and assign hello address space of 10.0.0.0/24
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with hello address space of 10.0.0.0/16 and add hello subnet
$vnet = New-AzureRmVirtualNetwork -Name ContosoVNET -ResourceGroupName ContosoRG -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve hello newly created subnet
$subnet=$vnet.Subnets[0]

# Create a public IP address that is used tooconnect toohello application gateway. Application Gateway does not support custom DNS names on public IP addresses.  If a custom name is required for hello public endpoint, a CNAME record should be created toopoint toohello automatically generated DNS name for hello public IP address.
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a gateway IP configuration. hello gateway picks up an IP addressfrom hello configured subnet and routes network traffic toohello IP addresses in hello backend IP pool. Keep in mind that each instance takes one IP address.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Configure a backend pool with hello addresses of your web servers. These backend pool members are all validated toobe healthy by probes, whether they are basic probes or custom probes.  Traffic is then routed toothem when requests come into hello application gateway. Backend pools can be used by multiple rules within hello application gateway, which means one backend pool could be used for multiple web applications that reside on hello same host.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Configure backend http settings toodetermine hello protocol and port that is used when sending traffic toohello backend servers. Cookie-based sessions are also determined by hello backend HTTP settings.  If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

# Configure a frontend port that is used tooconnect toohello application gateway through hello public IP address
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80

# Configure hello frontend IP configuration with hello public IP address created earlier.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Configure hello listener.  hello listener is a combination of hello front end IP configuration, protocol, and port and is used tooreceive incoming network traffic. 
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Configure a basic rule that is used tooroute traffic toohello backend servers. hello backend pool settings, listener, and backend pool created in hello previous steps make up hello rule. Based on hello criteria defined traffic is routed toohello appropriate backend.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Configure hello SKU for hello application gateway, this determines hello size and whether or not WAF is used.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Create hello application gateway
$appgw = New-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="b6ee6-150">Al termine, è possibile recuperare i dettagli DNS e l'indirizzo VIP del gateway applicazione hello dal gateway di hello pubblica IP risorsa allegato toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-150">When complete, retrieve DNS and VIP details of hello application gateway from hello public IP resource attached toohello application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName ContosoRG
```

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="b6ee6-151">Eliminare il gateway applicazione hello</span><span class="sxs-lookup"><span data-stu-id="b6ee6-151">Delete hello application gateway</span></span>

<span data-ttu-id="b6ee6-152">Hello esempio elimina gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-152">hello following example deletes hello application gateway.</span></span>

```powershell
# Retrieve hello application gateway
$gw = Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG

# Stops hello application gateway
Stop-AzureRmApplicationGateway -ApplicationGateway $gw

# Once hello application gateway is in a stopped state, use hello `Remove-AzureRmApplicationGateway` cmdlet tooremove hello service.
Remove-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG -Force
```

> [!NOTE]
> <span data-ttu-id="b6ee6-153">Hello **-force** switch possono essere messaggio di conferma rimozione hello toosuppress utilizzato.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-153">hello **-force** switch can be used toosuppress hello remove confirmation message.</span></span>

<span data-ttu-id="b6ee6-154">tooverify che hello servizio è stato rimosso, è possibile usare hello `Get-AzureRmApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-154">tooverify that hello service has been removed, you can use hello `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="b6ee6-155">Questo passaggio non è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-155">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name ContosoAppGateway -ResourceGroupName ContosoRG
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="b6ee6-156">Ottenere il nome DNS del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="b6ee6-156">Get application gateway DNS name</span></span>

<span data-ttu-id="b6ee6-157">Una volta creato il gateway hello passaggio successivo hello è tooconfigure hello front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-157">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="b6ee6-158">Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-158">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="b6ee6-159">gli utenti finali tooensure possibile raggiungere il gateway di applicazione hello, un record CNAME può essere utilizzati toopoint endpoint pubblico di toohello di gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-159">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="b6ee6-160">toodo, dettagli recuperare di gateway applicazione hello e il relativo nome IP/DNS associato usando hello PublicIPAddress elemento collegato toohello applicazioni gateway.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="b6ee6-161">A tale scopo con DNS di Azure o di altri provider DNS per la creazione di un record CNAME che punta toohello [indirizzo IP pubblico](../dns/dns-custom-domain.md#public-ip-address).</span><span class="sxs-lookup"><span data-stu-id="b6ee6-161">This can be done with Azure DNS or other DNS providers, by creating a CNAME record that points toohello [public IP address](../dns/dns-custom-domain.md#public-ip-address).</span></span> <span data-ttu-id="b6ee6-162">utilizzo di Hello del record non è consigliato poiché hello VIP potrebbe cambiare al riavvio del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="b6ee6-163">Viene assegnato a un indirizzo IP gateway applicazione toohello all'avvio del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="b6ee6-163">An IP address is assigned toohello application gateway when hello service starts.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName ContosoRG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : ContosoRG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/ContosoRG/providers/Microsoft.Network/applicationGateways/ContosoAppGateway/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="delete-all-resources"></a><span data-ttu-id="b6ee6-164">Eliminare tutte le risorse</span><span class="sxs-lookup"><span data-stu-id="b6ee6-164">Delete all resources</span></span>

<span data-ttu-id="b6ee6-165">toodelete tutte le risorse create in questo articolo, hello completo seguente passaggio:</span><span class="sxs-lookup"><span data-stu-id="b6ee6-165">toodelete all resources created in this article, complete hello following step:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name ContosoRG
```

## <a name="next-steps"></a><span data-ttu-id="b6ee6-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b6ee6-166">Next steps</span></span>

<span data-ttu-id="b6ee6-167">Se si desidera tooconfigure offload SSL, visitare: [configurare un gateway applicazione per l'offload SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="b6ee6-167">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="b6ee6-168">Se si desidera tooconfigure un toouse di gateway applicazione con un servizio di bilanciamento del carico interno, visitare: [creare un gateway applicazione con un servizio di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="b6ee6-168">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="b6ee6-169">Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:</span><span class="sxs-lookup"><span data-stu-id="b6ee6-169">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="b6ee6-170">Servizio di bilanciamento del carico di Azure</span><span class="sxs-lookup"><span data-stu-id="b6ee6-170">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="b6ee6-171">Gestione traffico di Azure</span><span class="sxs-lookup"><span data-stu-id="b6ee6-171">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
