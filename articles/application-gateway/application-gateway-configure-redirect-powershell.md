---
title: Configurare il reindirizzamento per il gateway applicazione di Azure - PowerShell | Microsoft Docs
description: Questa pagina contiene scenari di configurazione del reindirizzamento per il gateway applicazione tramite PowerShell
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/18/2017
ms.author: gwallace
ms.openlocfilehash: 84a25e572a27df2fe46e07c4ab0a4aab5969d68e
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="configure-redirection-on-application-gateway-with-powershell"></a><span data-ttu-id="379f2-103">Configurare il reindirizzamento nel gateway applicazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="379f2-103">Configure redirection on Application Gateway with PowerShell</span></span>

<span data-ttu-id="379f2-104">Il gateway applicazione supporta il reindirizzamento del traffico in base a una configurazione definita.</span><span class="sxs-lookup"><span data-stu-id="379f2-104">Application gateway supports the ability to redirect traffic based on a defined configuration.</span></span> <span data-ttu-id="379f2-105">Per altre informazioni sul reindirizzamento in generale, vedere la [panoramica del reindirizzamento del gateway applicazione](application-gateway-redirect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="379f2-105">To learn more about redirection in general visit, [Application Gateway redirect overview](application-gateway-redirect-overview.md).</span></span> <span data-ttu-id="379f2-106">Questo articolo contiene esempi di reindirizzamento da HTTP a HTTPS e di reindirizzamenti basati sul percorso, multisito e a siti esterni.</span><span class="sxs-lookup"><span data-stu-id="379f2-106">This article provides examples of HTTP to HTTPS redirection, path based redirects, multi-site redirects, and redirects to external sites.</span></span>

## <a name="http-to-https-redirect-on-an-existing-application-gateway"></a><span data-ttu-id="379f2-107">Reindirizzamento da HTTP a HTTPS in un gateway applicazione esistente</span><span class="sxs-lookup"><span data-stu-id="379f2-107">HTTP to HTTPS redirect on an existing application gateway</span></span>

<span data-ttu-id="379f2-108">L'esempio seguente crea un nuovo listener HTTP sulla porta 80 per reindirizzare le richieste per il listener esistente alla porta 443.</span><span class="sxs-lookup"><span data-stu-id="379f2-108">The following example creates a new HTTP listener on port 80 to redirect requests to the existing listener on port 443.</span></span>

```powershell
# Get the application gateway
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG

# Get the existing HTTPS listener
$httpslistener = Get-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener -ApplicationGateway $gw

# Get the existing front end IP configuration
$fipconfig = Get-AzureRmApplicationGatewayFrontendIPConfig -Name appgatewayfrontendip -ApplicationGateway $gw

# Add a new front end port to support HTTP traffic
Add-AzureRmApplicationGatewayFrontendPort -Name appGatewayFrontendPort2  -Port 80 -ApplicationGateway $gw

# Get the recently created port
$fp = Get-AzureRmApplicationGatewayFrontendPort -Name appGatewayFrontendPort2 -ApplicationGateway $gw

# Create a new HTTP listener using the port created earlier
Add-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener2  -Protocol Http -FrontendPort $fp -FrontendIPConfiguration $fipconfig -ApplicationGateway $gw 

# Get the new listener
$listener = Get-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener2 -ApplicationGateway $gw

# Add a redirection configuration using a permanent redirect and targeting the existing listener
Add-AzureRmApplicationGatewayRedirectConfiguration -Name redirectHttptoHttps -RedirectType Permanent -TargetListener $httpslistener -IncludePath $true -IncludeQueryString $true -ApplicationGateway $gw

# Get the redirect configuration
$redirectconfig = Get-AzureRmApplicationGatewayRedirectConfiguration -Name redirectHttptoHttps -ApplicationGateway $gw


# Add a new rule to handle the redirect and use the new listener
Add-AzureRmApplicationGatewayRequestRoutingRule -Name rule02 -RuleType Basic -HttpListener $listener -RedirectConfiguration $redirectconfig -ApplicationGateway $gw

# Update the application gateway
Set-AzureRmApplicationGateway -ApplicationGateway $gw 
```

<span data-ttu-id="379f2-109">Dopo aver aggiornato il gateway applicazione, testare il nuovo listener sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="379f2-109">Once the application gateway is updated, test the new listener on port 80.</span></span>  <span data-ttu-id="379f2-110">L'esempio seguente illustra l'uso di `curl` per il test del reindirizzamento.</span><span class="sxs-lookup"><span data-stu-id="379f2-110">The following example shows using `curl` test the redirection.</span></span>

```
curl http://40.69.161.221 -i
HTTP/1.1 301 Moved Permanently
Content-Type: text/html; charset=UTF-8
Location: https://40.69.161.221/
Server: Microsoft-IIS/10.0
Date: Tue, 11 Jul 2017 20:54:00 GMT
Content-Length: 145

<head><title>Document Moved</title></head>
<body><h1>Object Moved</h1>This document may be found <a HREF="https://40.69.161.221/">here</a></body>
```

## <a name="path-based-redirect"></a><span data-ttu-id="379f2-111">Reindirizzamento basato sul percorso</span><span class="sxs-lookup"><span data-stu-id="379f2-111">Path based redirect</span></span>

<span data-ttu-id="379f2-112">L'esempio seguente crea un nuovo listener e una regola basata sul percorso in un gateway applicazione esistente, che reindirizza solo il traffico che soddisfa il percorso dell'URL specifico.</span><span class="sxs-lookup"><span data-stu-id="379f2-112">The following example creates a new listener and a path based rule on an existing application gateway that redirects only traffic meeting the specific url path.</span></span>

```powershell
# Get the application gateway
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG

# Get the existing HTTPS listener
$httpslistener = Get-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener -ApplicationGateway $gw

# Get the existing front end IP configuration
$fipconfig = Get-AzureRmApplicationGatewayFrontendIPConfig -Name appgatewayfrontendip -ApplicationGateway $gw

# Add a new front end port to support HTTP traffic
Add-AzureRmApplicationGatewayFrontendPort -Name appGatewayFrontendPort2  -Port 80 -ApplicationGateway $gw

# Get the recently created port
$fp = Get-AzureRmApplicationGatewayFrontendPort -Name appGatewayFrontendPort2 -ApplicationGateway $gw

# Create a new HTTP listener using the port created earlier
Add-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener2  -Protocol Http -FrontendPort $fp -FrontendIPConfiguration $fipconfig -ApplicationGateway $gw 

# Get the new listener
$listener = Get-AzureRmApplicationGatewayHttpListener -Name appgatewayhttplistener2 -ApplicationGateway $gw

# Add a redirection configuration using a permanent redirect and targeting the existing listener
$redirectconfig = Get-AzureRmApplicationGatewayRedirectConfiguration -Name redirectpath6 -ApplicationGateway $gw

# Retrieve the existing backend http settings to be used
$poolSetting = Get-AzureRmApplicationGatewayBackendHttpSettings -Name "appGatewayBackendHttpSettings" -ApplicationGateway $gw

# Retrieve an existing backend pool
$pool = Get-AzureRmApplicationGatewayBackendAddressPool -Name appGatewayBackendPool -ApplicationGateway $gw

# Create a new path based rule
$pathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule6" -Paths "/image/*" -BackendAddressPool $pool -BackendHttpSettings $poolSetting

# Create a path map to add to the rule
Add-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $pathRule -DefaultBackendAddressPool $pool -DefaultBackendHttpSettings $poolSetting -ApplicationGateway $gw

# Retrieve the url path map created
$urlPathMap = Get-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -ApplicationGateway $gw

# Add a new rule to handle the redirect and use the new listener
Add-AzureRmApplicationGatewayRequestRoutingRule -Name "rule6" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap -RedirectConfiguration $redirectconfig -ApplicationGateway $gw

# Update the application gateway
Set-AzureRmApplicationGateway -ApplicationGateway $gw 
```

## <a name="multi-site-redirect"></a><span data-ttu-id="379f2-113">Reindirizzamento multisito</span><span class="sxs-lookup"><span data-stu-id="379f2-113">Multi-site redirect</span></span>

<span data-ttu-id="379f2-114">L'esempio seguente crea un nuovo gateway applicazione con due listener multisito sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="379f2-114">The following example creates a new application gateway with 2 multi-site listeners on port 80.</span></span> <span data-ttu-id="379f2-115">I listener sono per adatum.com e adatum.org.</span><span class="sxs-lookup"><span data-stu-id="379f2-115">The listeners are for adatum.com and adatum.org.</span></span> <span data-ttu-id="379f2-116">Viene creata una regola di reindirizzamento per reindirizzare il traffico da adatum.org ad adatum.com.</span><span class="sxs-lookup"><span data-stu-id="379f2-116">A redirect rule is created to redirect traffic from adatum.org to adatum.com.</span></span> <span data-ttu-id="379f2-117">È necessaria una configurazione aggiuntiva per configurare gli alias CNAME con gli indirizzi IP pubblici del gateway applicazione. Per altre informazioni sulla delega del dominio al servizio DNS di Azure e la creazione di record CNAME per il dominio, vedere [Delegare un dominio al servizio DNS di Azure](../dns/dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="379f2-117">Additional configuration is required for configuring CNAME aliases to the application gateway public IP address, for more information on delegating your domain to Azure DNS and creating CNAME records for your domain visit, [Delegate a domain to Azure DNS](../dns/dns-delegate-domain-azure-dns.md).</span></span>

```powershell
# Create a new resource group for the application gateway
New-AzureRmResourceGroup -Name appgw-rg -Location "East US"

# Create a subnet configuration object for the application gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your application gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet

# Create a public IP address for use with the application gateway. Defining the domainnamelabel during creation is not supported for use with application gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "East US" -AllocationMethod Dynamic

# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $vnet.Subnets[0]

# Create a backend pool to hold the addresses or NICs for the application that application gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 80

# Create a frontend IP configuration to associate the public IP address with the application gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Create the HTTP listener for the application gateway for adatum.com. Assign the front-end ip configuration, and port.
$listener1 = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp -HostName adatum.com

# Create the HTTP listener for the application gateway for adatum.org this listener will redirect to the abc.com listener. Assign the front-end ip configuration, and port.
$listener2 = New-AzureRmApplicationGatewayHttpListener -Name listener02 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp -HostName adatum.org

# Create the redirect configuration that will point traffic to the 
$redirectconfig = New-AzureRmApplicationGatewayRedirectConfiguration -Name redirectOrgtoCom -RedirectType Found -TargetListener $listener1 -IncludePath $true -IncludeQueryString $true

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule1 = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -HttpListener $listener1 -BackendHttpSettings $poolSetting -BackendAddressPool $pool

#Create a load balancer routing rule that redirects traffic to the adatum.com listener
$rule2 = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule02 -RuleType Basic -HttpListener $listener2 -RedirectConfiguration $redirectconfig

# Configure the SKU of the application gateway
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Medium -Tier Standard -Capacity 2

# Create the application gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener,$listener2 -RequestRoutingRules $rule1,$rule2 -RedirectConfigurations $redirectconfig -Sku $sku
```

## <a name="redirect-to-an-external-site"></a><span data-ttu-id="379f2-118">Reindirizzamento a un sito esterno</span><span class="sxs-lookup"><span data-stu-id="379f2-118">Redirect to an external site</span></span>

<span data-ttu-id="379f2-119">L'esempio seguente reindirizza il traffico in ingresso nel gateway applicazione a un sito Web esterno (bing.com).</span><span class="sxs-lookup"><span data-stu-id="379f2-119">The following example redirects traffic coming into the application gateway to an external website (bing.com).</span></span> <span data-ttu-id="379f2-120">Quando si usa l'opzione `TargetUrl`, le opzioni `IncludePath` e `IncludeQuery` opzioni non sono consentite.</span><span class="sxs-lookup"><span data-stu-id="379f2-120">When using the `TargetUrl` switch the `IncludePath` and `IncludeQuery` switches are not allowed.</span></span>

```powershell
# Create a new resource group for the application gateway
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"

# Create a subnet configuration object for the application gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your application gateway in the future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for the backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create the virtual network with the previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet

# Create a public IP address for use with the application gateway. Defining the domainnamelabel during creation is not supported for use with application gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic

# Create a IP configuration. This configures what subnet the Application Gateway uses. When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $vnet.Subnets[0]

# Create a backend pool to hold the addresses or NICs for the application that application gateway is protecting.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3

# Conifugre the backend HTTP settings to be used to define how traffic is routed to the backend pool. The authenication certificate used in the previous step is added to the backend http settings.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled

# Create a frontend port to be used by the listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 80

# Create a frontend IP configuration to associate the public IP address with the application gateway
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip

# Create the HTTP listener for the application gateway. Assign the front-end ip configuration, and port.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp 

# Create the redirect configuration that will point traffic to the 
$redirectconfig = New-AzureRmApplicationGatewayRedirectConfiguration -Name myredirect -RedirectType Temporary -TargetUrl "http://bing.com" -IncludePath $true -IncludeQueryString $true

#Create a load balancer routing rule that configures the load balancer behavior. In this example, a basic round robin rule is created.
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -HttpListener $listener -RedirectConfiguration $redirectconfig 

# Configure the SKU of the application gateway
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2

# Create the application gateway utilizing all the previously created configuration objects
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -RedirectConfigurations $redirectconfig -Sku $sku
```

## <a name="next-steps"></a><span data-ttu-id="379f2-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="379f2-121">Next steps</span></span>

<span data-ttu-id="379f2-122">Vedere [Configurare SSL end-to-end e i criteri SSL con il gateway applicazione tramite PowerShell](application-gateway-end-to-end-ssl-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="379f2-122">Visit [configure end to end SSL with application gateway using PowerShell](application-gateway-end-to-end-ssl-powershell.md)</span></span>