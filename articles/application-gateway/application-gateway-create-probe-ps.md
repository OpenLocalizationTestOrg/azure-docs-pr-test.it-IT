---
title: aaaCreate personalizzato probe - Gateway applicazione Azure - PowerShell | Documenti Microsoft
description: Informazioni su come toocreate personalizzato probe per il Gateway applicazione tramite PowerShell in Gestione risorse
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68feb660-7fa4-4f69-a7e4-bdd7bdc474db
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 44c9ffa75401d6d0db023e66fa82c701fb0cf8bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="c773e-103">Creare un probe personalizzato per il gateway applicazione di Azure con PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c773e-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c773e-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="c773e-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="c773e-105">PowerShell per Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c773e-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="c773e-106">PowerShell per Azure classico</span><span class="sxs-lookup"><span data-stu-id="c773e-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="c773e-107">In questo articolo aggiungere un gateway di applicazione esistente probe personalizzato tooan con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c773e-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="c773e-108">Probe personalizzati sono utili per le applicazioni che dispone di una pagina di controllo di integrità specifico o per le applicazioni che non forniscono una risposta corretta in un'applicazione web predefinita hello.</span><span class="sxs-lookup"><span data-stu-id="c773e-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!NOTE]
> <span data-ttu-id="c773e-109">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c773e-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="c773e-110">In questo articolo viene illustrato l'utilizzo modello di distribuzione di gestione delle risorse hello, si consiglia di per la maggior parte delle nuove distribuzioni anziché hello [modello di distribuzione classica](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c773e-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](application-gateway-create-probe-classic-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway-with-a-custom-probe"></a><span data-ttu-id="c773e-111">Creare un gateway applicazione con un probe personalizzato</span><span class="sxs-lookup"><span data-stu-id="c773e-111">Create an application gateway with a custom probe</span></span>

### <a name="sign-in-and-create-resource-group"></a><span data-ttu-id="c773e-112">Eseguire l'accesso e creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="c773e-112">Sign in and create resource group</span></span>

1. <span data-ttu-id="c773e-113">Utilizzare `Login-AzureRmAccount` tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="c773e-113">Use `Login-AzureRmAccount` tooauthenticate.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

1. <span data-ttu-id="c773e-114">Recupera le sottoscrizioni di hello per conto di hello.</span><span class="sxs-lookup"><span data-stu-id="c773e-114">Get hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

1. <span data-ttu-id="c773e-115">Scegliere quali di toouse le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="c773e-115">Choose which of your Azure subscriptions toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -Subscriptionid '{subscriptionGuid}'
  ```

1. <span data-ttu-id="c773e-116">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c773e-116">Create a resource group.</span></span> <span data-ttu-id="c773e-117">Se si dispone di un gruppo di risorse, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="c773e-117">You can skip this step if you have an existing resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name appgw-rg -Location 'West US'
  ```

<span data-ttu-id="c773e-118">Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso</span><span class="sxs-lookup"><span data-stu-id="c773e-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="c773e-119">Questo percorso viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c773e-119">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="c773e-120">Assicurarsi che tutti i comandi toocreate un hello di uso di gateway applicazione stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c773e-120">Make sure that all commands toocreate an application gateway use hello same resource group.</span></span>

<span data-ttu-id="c773e-121">In hello sopra riportato, è stato creato un gruppo di risorse denominato **appgw-RG** nel percorso **Stati Uniti occidentali**.</span><span class="sxs-lookup"><span data-stu-id="c773e-121">In hello preceding example, we created a resource group called **appgw-RG** in location **West US**.</span></span>

### <a name="create-a-virtual-network-and-a-subnet"></a><span data-ttu-id="c773e-122">Creare una rete virtuale e una subnet</span><span class="sxs-lookup"><span data-stu-id="c773e-122">Create a virtual network and a subnet</span></span>

<span data-ttu-id="c773e-123">Hello seguente viene creata una rete virtuale e una subnet per il gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c773e-123">hello following example creates a virtual network and a subnet for hello application gateway.</span></span> <span data-ttu-id="c773e-124">Per il gateway applicazione è necessaria una propria subnet.</span><span class="sxs-lookup"><span data-stu-id="c773e-124">Application gateway requires its own subnet for use.</span></span> <span data-ttu-id="c773e-125">Per questo motivo, subnet hello creata per il gateway applicazione hello deve essere minore di spazio di indirizzo hello hello tooallow di rete virtuale per altri toobe subnet creati e utilizzati.</span><span class="sxs-lookup"><span data-stu-id="c773e-125">For this reason, hello subnet created for hello application gateway should be smaller than hello address space of hello VNET tooallow for other subnets toobe created and used.</span></span>

```powershell
# Assign hello address range 10.0.0.0/24 tooa subnet variable toobe used toocreate a virtual network.
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network named appgwvnet in resource group appgw-rg for hello West US region using hello prefix 10.0.0.0/16 with subnet 10.0.0.0/24.
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Assign a subnet variable for hello next steps, which create an application gateway.
$subnet = $vnet.Subnets[0]
```

### <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a><span data-ttu-id="c773e-126">Creare un indirizzo IP pubblico per la configurazione front-end hello</span><span class="sxs-lookup"><span data-stu-id="c773e-126">Create a public IP address for hello front-end configuration</span></span>

<span data-ttu-id="c773e-127">Creare una risorsa IP pubblica **publicIP01** nel gruppo di risorse **appgw-rg** per area Stati Uniti occidentali hello.</span><span class="sxs-lookup"><span data-stu-id="c773e-127">Create a public IP resource **publicIP01** in resource group **appgw-rg** for hello West US region.</span></span> <span data-ttu-id="c773e-128">Questo esempio Usa un indirizzo IP pubblico per indirizzo IP front-end di hello del gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c773e-128">This example uses a public IP address for hello front-end IP address of hello application gateway.</span></span>  <span data-ttu-id="c773e-129">Gateway applicazione richiede hello pubblica IP indirizzo toohave hello pertanto un nome DNS creato dinamicamente `-DomainNameLabel` non può essere specificato durante la creazione dell'indirizzo IP pubblico hello hello.</span><span class="sxs-lookup"><span data-stu-id="c773e-129">Application gateway requires hello public IP address toohave a dynamically created DNS name therefore hello `-DomainNameLabel` cannot be specified during hello creation of hello public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location 'West US' -AllocationMethod Dynamic
```

### <a name="create-an-application-gateway"></a><span data-ttu-id="c773e-130">Creare un gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="c773e-130">Create an application gateway</span></span>

<span data-ttu-id="c773e-131">Impostare tutti gli elementi di configurazione prima di creare i gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c773e-131">You set up all configuration items before creating hello application gateway.</span></span> <span data-ttu-id="c773e-132">Hello seguente viene creato hello gli elementi di configurazione necessari per una risorsa di gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c773e-132">hello following example creates hello configuration items that are needed for an application gateway resource.</span></span>

| <span data-ttu-id="c773e-133">**Componente**</span><span class="sxs-lookup"><span data-stu-id="c773e-133">**Component**</span></span> | <span data-ttu-id="c773e-134">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="c773e-134">**Description**</span></span> |
|---|---|
| <span data-ttu-id="c773e-135">**Configurazione IP del gateway**</span><span class="sxs-lookup"><span data-stu-id="c773e-135">**Gateway IP configuration**</span></span> | <span data-ttu-id="c773e-136">Configurazione IP per un gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c773e-136">An IP configuration for an application gateway.</span></span>|
| <span data-ttu-id="c773e-137">**Pool back-end**</span><span class="sxs-lookup"><span data-stu-id="c773e-137">**Backend pool**</span></span> | <span data-ttu-id="c773e-138">Un pool di indirizzi IP, nomi FQDN o schede di rete che sono toohello applicazione server che ospitano un'applicazione web hello</span><span class="sxs-lookup"><span data-stu-id="c773e-138">A pool of IP addresses, FQDN's, or NICs that are toohello application servers that host hello web application</span></span>|
| <span data-ttu-id="c773e-139">**Probe di integrità**</span><span class="sxs-lookup"><span data-stu-id="c773e-139">**Health probe**</span></span> | <span data-ttu-id="c773e-140">Un probe personalizzato utilizzato integrità hello toomonitor di membri del pool back-end hello</span><span class="sxs-lookup"><span data-stu-id="c773e-140">A custom probe used toomonitor hello health of hello backend pool members</span></span>|
| <span data-ttu-id="c773e-141">**Impostazioni HTTP**</span><span class="sxs-lookup"><span data-stu-id="c773e-141">**HTTP settings**</span></span> | <span data-ttu-id="c773e-142">Raccolta di impostazioni quali porta, protocollo, affinità basata sui cookie, probe e timeout.</span><span class="sxs-lookup"><span data-stu-id="c773e-142">A collection of settings including, port, protocol, cookie-based affinity, probe, and timeout.</span></span>  <span data-ttu-id="c773e-143">Queste impostazioni determinano la modalità il traffico viene indirizzato toohello i membri del pool back-end</span><span class="sxs-lookup"><span data-stu-id="c773e-143">These settings determine how traffic is routed toohello backend pool members</span></span>|
| <span data-ttu-id="c773e-144">**Porta front-end**</span><span class="sxs-lookup"><span data-stu-id="c773e-144">**Frontend port**</span></span> | <span data-ttu-id="c773e-145">porta Hello hello gateway applicazione in ascolto del traffico su</span><span class="sxs-lookup"><span data-stu-id="c773e-145">hello port that hello application gateway listens for traffic on</span></span>|
| <span data-ttu-id="c773e-146">**Listener**</span><span class="sxs-lookup"><span data-stu-id="c773e-146">**Listener**</span></span> | <span data-ttu-id="c773e-147">Combinazione di protocollo, configurazione IP front-end e porta front-end</span><span class="sxs-lookup"><span data-stu-id="c773e-147">A combination of a protocol, frontend IP configuration, and frontend port.</span></span> <span data-ttu-id="c773e-148">che consente di ascoltare le richieste in ingresso.</span><span class="sxs-lookup"><span data-stu-id="c773e-148">This is what listens for incoming requests.</span></span>
|<span data-ttu-id="c773e-149">**Regola**</span><span class="sxs-lookup"><span data-stu-id="c773e-149">**Rule**</span></span>| <span data-ttu-id="c773e-150">Le route hello traffico toohello back-end appropriati in base alle impostazioni HTTP.</span><span class="sxs-lookup"><span data-stu-id="c773e-150">Routes hello traffic toohello appropriate backend based on HTTP settings.</span></span>|

```powershell
# Creates a application gateway Frontend IP configuration named gatewayIP01
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

#Creates a back-end IP address pool named pool01 with IP addresses 134.170.185.46, 134.170.188.221, 134.170.185.50.
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

# Creates a probe that will check health at http://contoso.com/path/path.htm
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/path.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Creates hello backend http settings toobe used. This component references hello $probe created in hello previous command.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80

# Creates a frontend port for hello application gateway toolisten on port 80 that will be used by hello listener.
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80

# Creates a frontend IP configuration. This associates hello $publicip variable defined previously with hello front-end IP that will be used by hello listener.
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Creates hello listener. hello listener is a combination of protocol and hello frontend IP configuration $fipconfig and frontend port $fp created in previous steps.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp

# Creates hello rule that routes traffic toohello backend pools.  In this example we create a basic rule that uses hello previous defined http settings and backend address pool.  It also associates hello listener toohello rule
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Sets hello SKU of hello application gateway, in this example we create a small standard application gateway with 2 instances.
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# hello final step creates hello application gateway with all hello previously defined components.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location 'West US' -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-tooan-existing-application-gateway"></a><span data-ttu-id="c773e-151">Aggiungere un gateway di applicazione esistente tooan probe</span><span class="sxs-lookup"><span data-stu-id="c773e-151">Add a probe tooan existing application gateway</span></span>

<span data-ttu-id="c773e-152">Hello frammento di codice seguente aggiunge un gateway applicazione esistente tooan probe.</span><span class="sxs-lookup"><span data-stu-id="c773e-152">hello following code snippet adds a probe tooan existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Create hello probe object that will check health at http://contoso.com/path/path.htm
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName 'contoso.com' -Path '/path/custompath.htm' -Interval 30 -Timeout 120 -UnhealthyThreshold 8

# Set hello backend HTTP settings toouse hello new probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="c773e-153">Rimuovere un probe da un gateway applicazione esistente</span><span class="sxs-lookup"><span data-stu-id="c773e-153">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="c773e-154">Hello seguente frammento di codice rimuove un probe da un gateway applicazione esistente.</span><span class="sxs-lookup"><span data-stu-id="c773e-154">hello following code snippet removes a probe from an existing application gateway.</span></span>

```powershell
# Load hello application gateway resource into a PowerShell variable by using Get-AzureRmApplicationGateway.
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg

# Remove hello probe from hello application gateway configuration object
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name

# Set hello backend HTTP settings tooremove hello reference toohello probe. hello backend http settings now use hello default probe
$getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled

# Save hello application gateway with hello configuration changes
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="c773e-155">Ottenere il nome DNS del gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="c773e-155">Get application gateway DNS name</span></span>

<span data-ttu-id="c773e-156">Una volta creato il gateway hello passaggio successivo hello è tooconfigure hello front-end per la comunicazione.</span><span class="sxs-lookup"><span data-stu-id="c773e-156">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="c773e-157">Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo.</span><span class="sxs-lookup"><span data-stu-id="c773e-157">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="c773e-158">gli utenti finali tooensure possibile raggiungere il gateway di applicazione hello può essere utilizzato un record CNAME toopoint toohello endpoint pubblico del gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c773e-158">tooensure end users can hit hello application gateway a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="c773e-159">[Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c773e-159">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="c773e-160">toodo, dettagli recuperare di gateway applicazione hello e il relativo nome IP/DNS associato usando hello PublicIPAddress elemento collegato toohello applicazioni gateway.</span><span class="sxs-lookup"><span data-stu-id="c773e-160">toodo this, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="c773e-161">nome DNS del gateway applicazione Hello deve essere utilizzato toocreate un record CNAME, il nome DNS punti hello due web applicazioni toothis.</span><span class="sxs-lookup"><span data-stu-id="c773e-161">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="c773e-162">utilizzo di Hello del record non è consigliato poiché hello VIP potrebbe cambiare al riavvio del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="c773e-162">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c773e-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c773e-163">Next steps</span></span>

<span data-ttu-id="c773e-164">Informazioni su tooconfigure offload SSL, visitare il sito: [configurare Offload SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="c773e-164">Learn tooconfigure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

