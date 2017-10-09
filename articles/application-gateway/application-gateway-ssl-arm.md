---
title: -Gateway applicazione Azure - PowerShell di offload SSL aaaConfigure | Documenti Microsoft
description: Questa pagina fornisce istruzioni toocreate un gateway applicazione con SSL offload usando Gestione risorse di Azure
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c2855d8d3caaa97ec05475c67ff0f8dce72ef2a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a>Configurare un gateway applicazione per l'offload SSL con Azure Resource Manager

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-ssl-portal.md)
> * [PowerShell per Azure Resource Manager](application-gateway-ssl-arm.md)
> * [PowerShell per Azure classico](application-gateway-ssl.md)
> * [Interfaccia della riga di comando di Azure 2.0](application-gateway-ssl-cli.md)

Gateway applicazione Azure può essere configurato tooterminate hello Secure Sockets Layer (SSL) sessione hello gateway tooavoid costosi SSL decrittografia attività toohappen alla farm web hello. Offload SSL semplifica anche l'installazione di server front-end di hello e gestione di un'applicazione web hello.

## <a name="before-you-begin"></a>Prima di iniziare

1. Installare più recente dei cmdlet di Azure PowerShell hello hello utilizzando hello installazione guidata piattaforma Web. È possibile scaricare e installare la versione più recente di hello da hello **Windows PowerShell** sezione di hello [pagina di download](https://azure.microsoft.com/downloads/).
2. Creare una rete virtuale e una subnet per il gateway applicazione hello. Assicurarsi che nessun macchine virtuali o le distribuzioni di cloud utilizza subnet hello. Il gateway applicazione deve essere da solo in una subnet di rete virtuale.
3. server di Hello è configurare gateway di applicazione hello toouse deve essere presente o i relativi endpoint creato nella rete virtuale hello o con un indirizzo IP/VIP pubblico assegnato.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Che cos'è toocreate necessario un gateway applicazione?

* **Pool di server back-end:** elenco hello di indirizzi IP dei server back-end hello. gli indirizzi IP Hello elencati devono appartenere toohello subnet della rete virtuale o devono essere un indirizzo IP/VIP pubblico.
* **Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie. Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.
* **Porta front-end:** questa porta è una porta pubblica hello aperta sul gateway applicazione hello. Traffico riscontri questa porta, e quindi ottiene reindirizzato tooone dei server back-end hello.
* **Listener:** listener hello dispone di una porta front-end, un protocollo (Http o Https, queste impostazioni sono distinzione maiuscole/minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload).
* **Regola:** regola hello associa listener hello e pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener. Attualmente, solo hello *base* regola supportata. Hello *base* regola è una distribuzione del carico round robin.

**Note aggiuntive sulla configurazione**

Per la configurazione di certificati SSL, hello protocollo **HttpListener** deve modificare troppo*Https* (maiuscole / minuscole). Hello **SslCertificate** elemento viene aggiunto troppo**HttpListener** con valore della variabile hello configurato per il certificato SSL hello. porta front-end di Hello deve essere aggiornato too443.

**affinità basato su cookie tooenable**: un gateway applicazione può essere configurato tooensure che una richiesta da una sessione client è sempre toohello diretto stessa macchina virtuale nella farm web hello. Questo scenario viene eseguito dall'inserimento di un cookie di sessione che consenta il traffico di toodirect di hello gateway in modo appropriato. impostata l'affinità basato su cookie tooenable, **CookieBasedAffinity** troppo*abilitato* in hello **BackendHttpSettings** elemento.

## <a name="create-an-application-gateway"></a>Creare un gateway applicazione

differenza Hello tra il modello di distribuzione di Azure classico hello e Gestione risorse di Azure è ordine hello che si crea un'applicazione gateway e hello gli elementi che devono toobe configurato.

Gestione risorse di tutti i componenti di gateway applicazione sono configurati singolarmente e quindi inserire toocreate insieme una risorsa di gateway applicazione.

Di seguito è hello passaggi necessari toocreate un gateway applicazione:

1. Creare un gruppo di risorse per Gestione risorse
2. Creare una rete virtuale, subnet e indirizzo IP pubblico per il gateway applicazione hello
3. Creare un oggetto di configurazione gateway applicazione
4. Creare una risorsa del gateway applicazione

## <a name="create-a-resource-group-for-resource-manager"></a>Creare un gruppo di risorse per Gestione risorse

Assicurarsi che si passa in modalità toouse hello Azure Resource Manager cmdlet. Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Passaggio 1

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Passaggio 2

Controllare le sottoscrizioni di hello per account hello.

```powershell
Get-AzureRmSubscription
```

Si è tooauthenticate richiesta con le credenziali.

### <a name="step-3"></a>Passaggio 3

Scegliere quali di toouse le sottoscrizioni di Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Passaggio 4

Creare un gruppo di risorse. Ignorare questo passaggio se si usa un gruppo di risorse esistente.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso Questa impostazione viene utilizzata come posizione predefinita hello per le risorse in tale gruppo di risorse. Assicurarsi che tutti i comandi toocreate utilizza un gateway applicazione hello stesso gruppo di risorse.

Nell'esempio hello sopra, è stato creato un gruppo di risorse denominato **appgw-RG** e il percorso **Stati Uniti occidentali**.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Creare una rete virtuale e una subnet per il gateway applicazione hello

Hello seguente esempio viene illustrato come toocreate una rete virtuale usando Gestione risorse:

### <a name="step-1"></a>Passaggio 1

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

In questo esempio assegna hello indirizzo intervallo 10.0.0.0/24 tooa subnet toobe variabile utilizzata toocreate una rete virtuale.

### <a name="step-2"></a>Passaggio 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

In questo esempio crea una rete virtuale denominata **appgwvnet** nel gruppo di risorse **appgw-rg** per area Stati Uniti occidentali hello con hello prefisso 10.0.0.0/16 10.0.0.0/24 subnet.

### <a name="step-3"></a>Passaggio 3

```powershell
$subnet = $vnet.Subnets[0]
```

In questo esempio assegna hello subnet oggetto toovariable $subnet per i passaggi successivi hello.

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Creare un indirizzo IP pubblico per la configurazione front-end hello

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

In questo esempio crea una risorsa IP pubblica **publicIP01** nel gruppo di risorse **appgw-rg** per area Stati Uniti occidentali hello.

## <a name="create-an-application-gateway-configuration-object"></a>Creare un oggetto di configurazione gateway applicazione

### <a name="step-1"></a>Passaggio 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

Questo esempio crea una configurazione IP del gateway applicazione denominata **gatewayIP01**. Avvio di Gateway applicazione preleva un indirizzo IP dalla subnet hello configurato e instradare gli indirizzi IP di toohello il traffico di rete nel pool IP back-end hello. Tenere presente che ogni istanza ha un indirizzo IP.

### <a name="step-2"></a>Passaggio 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

Questo esempio Configura pool indirizzi IP back-end di hello denominato **pool01** con indirizzi IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** . Tali valori sono gli indirizzi IP hello che ricevono il traffico di rete hello proveniente dall'endpoint IP front-end hello. Sostituire gli indirizzi IP hello hello sopra riportato con indirizzi IP hello degli endpoint dell'applicazione web.

### <a name="step-3"></a>Passaggio 3

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

In questo esempio consente di configurare impostazioni del gateway applicazione **poolsetting01** il traffico di rete bilanciato tooload nel pool back-end hello.

### <a name="step-4"></a>Passaggio 4

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

Questo esempio Configura porta IP front-end hello denominata **frontendport01** per endpoint IP pubblico hello.

### <a name="step-5"></a>Passaggio 5

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

Questo esempio Configura certificato hello utilizzato per la connessione SSL. certificato Hello deve toobe in formato PFX e password hello deve essere compresa tra 4 too12 caratteri.

### <a name="step-6"></a>Passaggio 6

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

In questo esempio Crea configurazione IP front-end di hello denominata **fipconfig01** e lo associa hello indirizzo IP pubblico con configurazione IP front-end hello.

### <a name="step-7"></a>Passaggio 7

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

Questo esempio viene creato il nome del listener hello **listener01** e lo associa hello configurazione IP front-end di porte front-end toohello e il certificato.

### <a name="step-8"></a>Passaggio 8

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

In questo esempio crea hello regola bilanciamento del carico routing denominata **rule01** che configura il comportamento del servizio di bilanciamento carico di hello.

### <a name="step-9"></a>Passaggio 9:

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

In questo esempio consente di configurare dimensioni di istanza hello del gateway applicazione hello.

> [!NOTE]
> il valore predefinito per Hello *InstanceCount* è 2, con un valore massimo di 10. il valore predefinito per Hello *GatewaySize* è Medium. È possibile scegliere tra Standard_Small, Standard_Medium e Standard_Large.

### <a name="step-10"></a>Passaggio 10

```powershell
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S
```

Questo passaggio definisce hello SSL criteri toouse gateway applicazione hello. Visitare [le versioni dei criteri configurare SSL e pacchetti di crittografia nel Gateway applicazione](application-gateway-configure-ssl-policy-powershell.md) toolearn altre.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>Creare un gateway applicazione usando New-AzureApplicationGateway

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

Questo esempio viene creato un gateway applicazione con tutti gli elementi di configurazione da hello passaggi precedenti. Nell'esempio hello, viene chiamato gateway applicazione hello **appgwtest**.

## <a name="get-application-gateway-dns-name"></a>Ottenere il nome DNS del gateway applicazione

Una volta creato il gateway hello passaggio successivo hello è tooconfigure hello front-end per la comunicazione. Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo. gli utenti finali tooensure possibile raggiungere il gateway di applicazione hello, un record CNAME può essere utilizzati toopoint endpoint pubblico di toohello di gateway applicazione hello. [Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). toodo, dettagli recuperare di gateway applicazione hello e il relativo nome IP/DNS associato usando hello PublicIPAddress elemento collegato toohello applicazioni gateway. nome DNS del gateway applicazione Hello deve essere utilizzato toocreate un record CNAME, il nome DNS punti hello due web applicazioni toothis. utilizzo di Hello del record non è consigliato poiché hello VIP potrebbe cambiare al riavvio del gateway applicazione.


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

Se si desidera tooconfigure un toouse di gateway applicazione con un servizio di bilanciamento del carico interno (ILB), vedere [creare un gateway applicazione con un servizio di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).

Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:

* [Servizio di bilanciamento del carico di Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Gestione traffico di Azure](https://azure.microsoft.com/documentation/services/traffic-manager/)

