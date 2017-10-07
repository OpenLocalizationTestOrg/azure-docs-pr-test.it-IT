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
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a>Configurare un web application firewall su un gateway applicazione nuovo o esistente

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Interfaccia della riga di comando di Azure](application-gateway-web-application-firewall-cli.md)

Informazioni su come toocreate un firewall applicazione web abilitata Gateway applicazione oppure aggiungere tooan di firewall applicazione web esistente di Gateway applicazione.

firewall applicazione web di Hello (WAF) nel Gateway di applicazione di Azure consente di proteggere le applicazioni web da attacchi basati sul web comuni quali attacchi SQL injection, attacchi di script e assume il controllo di sessione.

Il gateway applicazione di Azure è un dispositivo di bilanciamento del carico di livello 7. Fornisce il failover, le prestazioni di routing di richieste HTTP tra server diversi, che si trovino in locale o cloud hello. Il gateway applicazione offre numerose funzionalità di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller), tra cui bilanciamento del carico HTTP, affinità di sessione basata su cookie, offload SSL (Secure Sockets Layer), probe di integrità personalizzati, supporto per più siti e altro ancora. toofind un elenco completo delle funzionalità supportate, visitare: [Panoramica del Gateway applicazione](application-gateway-introduction.md).

Hello articolo seguente viene illustrato come troppo[aggiungere tooan di firewall applicazione web esistente di Gateway applicazione](#add-web-application-firewall-to-an-existing-application-gateway) e [creare un Gateway di applicazione che utilizza firewall applicazione web](#create-an-application-gateway-with-web-application-firewall).

![immagine dello scenario][scenario]

## <a name="waf-configuration-differences"></a>Differenze di configurazione dei WAF

Se si è letto [creare un Gateway applicazione con PowerShell](application-gateway-create-gateway-arm.md), comprendere hello SKU impostazioni tooconfigure durante la creazione di un Gateway applicazione. WAF fornisce toodefine impostazioni aggiuntive quando si configurano hello SKU di Gateway applicazione. Non sono presenti modifiche aggiuntive che verranno apportate hello Gateway applicazione stessa.

| **Impostazione** | **Dettagli**
|---|---|
|**SKU** |Un gateway applicazione normale senza WAF supporta le dimensioni **Standard\_Small**, **Standard\_Medium** e **Standard\_Large**. Introduzione di hello di WAF, non vi sono due SKU aggiuntive, **WAF\_Media** e **WAF\_grande**. WAF non è supportato sui gateway applicazione Small.|
|**Livello** | i valori disponibili Hello sono **Standard** o **WAF**. Quando si usa un web application firewall, è necessario scegliere **WAF** .|
|**Modalità** | Questa impostazione è la modalità di WAF hello. I valori consentiti sono **Rilevamento** e **Prevenzione**. Quando il firewall WAF è configurato in modalità di rilevamento, tutte le minacce vengono archiviate in un file di log. In modalità di prevenzione, gli eventi vengono comunque registrati ma autore dell'attacco hello riceve una risposta di non autorizzato 403 dal Gateway applicazione hello.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>Aggiungere tooan di firewall applicazione web esistente di Gateway applicazione

Assicurarsi che si utilizza hello la versione più recente di Azure PowerShell. Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).

1. Accedi tooyour Account Azure.

    ```powershell
    Login-AzureRmAccount
    ```

2. Selezionare hello toouse di sottoscrizione per questo scenario.

    ```powershell
    Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
    ```

3. Recuperare gateway hello che si sta aggiungendo firewall applicazione web per.

    ```powershell
    $gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
    ```

1. Configurare hello web application firewall sku. sono di dimensioni disponibili Hello **WAF\_grande** e **WAF\_Media**. Quando si utilizza firewall applicazione web deve essere livello hello **WAF**, capacità hello devono essere confermate durante l'impostazione sku hello.

    ```powershell
    $gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
    ```

1. Configurare le impostazioni di hello WAF come definito nell'esempio seguente hello:

   Per **FirewallMode**, i valori hello disponibili sono il rilevamento e prevenzione.

    ```powershell
    $gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
    ```

1. Aggiorna Gateway applicazione hello con impostazioni hello definite nel precedente passaggio hello.

    ```powershell
    Set-AzureRmApplicationGateway -ApplicationGateway $gw
    ```

Questo comando Aggiorna Gateway applicazione hello con firewall applicazione web. Visitare [diagnostica del Gateway applicazione](application-gateway-diagnostics.md) toounderstand come tooview Registra per il Gateway applicazione. A causa di toohello sicurezza natura WAF, registri necessità toobe rivisto regolarmente condizioni di sicurezza hello toounderstand delle applicazioni web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Creare un gateway applicazione con il web application firewall

Hello passaggi seguenti consentono hello intero processo da tooend di inizio per la creazione di un Gateway applicazione con firewall applicazione web.

Assicurarsi che si utilizza hello la versione più recente di Azure PowerShell. Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).

1. Accedi tooAzure eseguendo `Login-AzureRmAccount`, si è tooauthenticate richiesta con le credenziali.

1. Controllare le sottoscrizioni di hello per account hello eseguendo`Get-AzureRmSubscription`

1. Scegliere quali di toouse le sottoscrizioni di Azure.

    ```powershell
    Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
    ```

### <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un gruppo di risorse per hello Gateway applicazione.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso Questo percorso viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse. Assicurarsi che tutti i comandi Usa toocreate un Gateway applicazione hello stesso gruppo di risorse.

In hello sopra riportato, è stato creato un gruppo di risorse denominato "Appgw-RG" e il percorso "Stati Uniti occidentali."

> [!NOTE]
> Se è necessario tooconfigure un probe personalizzato per il Gateway applicazione, vedere [creare un Gateway applicazione con probe personalizzati usando PowerShell](application-gateway-create-probe-ps.md). Per altre informazioni, vedere l'articolo relativo a [probe personalizzati e monitoraggio dell'integrità](application-gateway-probe-overview.md) .

### <a name="configure-virtual-network"></a>Configurare la rete virtuale

Il gateway applicazione richiede una propria subnet. In questo passaggio creare una rete virtuale con uno spazio degli indirizzi di 10.0.0.0/16 e due subnet, uno per il Gateway applicazione hello e uno per i membri del pool back-end.

```powershell
# Create a subnet configuration object for hello Application Gateway subnet. A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in hello subnet for Application Gateway instances. With a smaller subnet, you may not be able tooadd more instance of your Application Gateway in hello future.
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24

# Create a subnet configuration object for hello backend pool members subnet
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24

# Create hello virtual network with hello previous created subnets
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="configure-public-ip-address"></a>Configurare l'indirizzo IP pubblico

In ordine toohandle le richieste esterne, i Gateway applicazione richiede un indirizzo IP pubblico. Questo indirizzo IP pubblico non deve avere un `DomainNameLabel` definito toobe utilizzato da hello Gateway applicazione.

```powershell
# Create a public IP address for use with hello Application Gateway. Defining hello domainnamelabel during creation is not supported for use with Application Gateway
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

### <a name="configure-hello-application-gateway"></a>Configurare hello Gateway applicazione

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
> Gateway applicazione creati con configurazione del firewall applicazione web di base hello sono configurati con CRS 3.0 per la protezione.

## <a name="get-application-gateway-dns-name"></a>Ottenere il nome DNS del gateway applicazione

Una volta creato il gateway hello passaggio successivo hello è tooconfigure hello front-end per la comunicazione. Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo. gli utenti finali tooensure possibile raggiungere il Gateway applicazione hello, un record CNAME può essere utilizzati toopoint endpoint pubblico di toohello di Gateway applicazione hello. [Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure un alias, recuperare i dettagli del Gateway applicazione hello e il relativo nome IP/DNS associato utilizzando hello PublicIPAddress elemento collegata toohello Gateway applicazione. nome DNS del Gateway applicazione Hello deve essere utilizzato toocreate un record CNAME, il nome DNS punti hello due web applicazioni toothis. utilizzo di Hello del record non è consigliato poiché hello VIP potrebbe cambiare al riavvio del Gateway applicazione.

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

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come la registrazione diagnostica tooconfigure, toolog hello gli eventi rilevati o prevenire firewall applicazione web, visitare il sito [diagnostica del Gateway applicazione](application-gateway-diagnostics.md)

[scenario]: ./media/application-gateway-web-application-firewall-powershell/scenario.png
