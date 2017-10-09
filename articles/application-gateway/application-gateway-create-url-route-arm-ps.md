---
title: un gateway applicazione utilizzando l'URL di routing regole aaaCreate | Documenti Microsoft
description: Questa pagina fornisce istruzioni toocreate, configurare un gateway applicazione Azure utilizzando le regole di routing di URL
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a>Creare un gateway applicazione con il routing basato sul percorso

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-create-url-route-portal.md)
> * [PowerShell per Azure Resource Manager](application-gateway-create-url-route-arm-ps.md)
> * [Interfaccia della riga di comando di Azure 2.0](application-gateway-create-url-route-cli.md)

Il routing basato sul percorso URL consente di tooassociate route in base al percorso URL hello di una richiesta Http. Verifica la presenza di un pool di back-end tooa route configurati per l'URL di hello presentati in hello Gateway applicazione. Invia quindi toohello il traffico di rete hello è definito il pool back-end. Un utilizzo comune per il routing basato su URL è tooload bilanciamento delle richieste per i pool di server back-end toodifferent diversi tipi di contenuto.

Routing basato su URL introduce un nuovo gateway tooapplication tipo di regola. Per il gateway applicazione sono disponibili due tipi di regole: basic e PathBasedRouting. Tipo di regola di base fornisce servizio round robin per hello back-end pool inoltre PathBasedRouting durante la distribuzione round robin tooround, accetta inoltre il modello del percorso dell'URL di richiesta hello in considerazione durante la scelta di pool back-end hello.

## <a name="scenario"></a>Scenario

Nell'esempio seguente di hello, Gateway applicazione gestisce il traffico per contoso.com con due pool di server back-end: pool di server video e immagine pool dei server.

Le richieste di http://contoso.com/image * vengono indirizzati vengono indirizzati i pool di server tooimage (pool1) e http://contoso.com/video * toovideo pool di server (pool2). Se nessuno dei modelli di percorso hello corrisponde, viene selezionato un pool di server predefinito (pool1).

![route dell'URL](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a>Prima di iniziare

1. Installare più recente dei cmdlet di Azure PowerShell hello hello utilizzando hello installazione guidata piattaforma Web. È possibile scaricare e installare la versione più recente di hello da hello **Windows PowerShell** sezione di hello [pagina di download](https://azure.microsoft.com/downloads/).
2. Creare una rete virtuale e una subnet per il gateway applicazione. Assicurarsi che nessun macchine virtuali o le distribuzioni di cloud utilizza subnet hello. gateway applicazione Hello deve essere da solo in una subnet di rete virtuale.
3. server Hello aggiunto deve essere presente il gateway applicazione hello di toohello pool back-end toouse o i relativi endpoint creato nella rete virtuale hello o con un indirizzo IP/VIP pubblico assegnato.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Che cos'è toocreate necessario un gateway applicazione?

* **Pool di server back-end:** elenco hello di indirizzi IP dei server back-end hello. gli indirizzi IP Hello elencati devono appartenere toohello subnet della rete virtuale o devono essere un indirizzo IP/VIP pubblico.
* **Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie. Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.
* **Porta front-end:** questa porta è una porta pubblica hello aperta sul gateway applicazione hello. Traffico riscontri questa porta, e quindi ottiene reindirizzato tooone dei server back-end hello.
* **Listener:** listener hello dispone di una porta front-end, un protocollo (Http o Https, questi valori sono distinzione maiuscole/minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload).
* **Regola:** regola hello associa listener hello, pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener.

## <a name="create-an-application-gateway"></a>Creare un gateway applicazione

differenza Hello tra l'utilizzo di Azure classico e Gestione risorse di Azure è ordine hello in cui è stato creato il gateway di applicazione hello e gli elementi hello necessario toobe configurato.

Gestione risorse di tutti gli elementi che costituiscono un gateway applicazione vengono configurati singolarmente e riunire risorsa per il gateway applicazione toocreate hello.

Ecco i passaggi hello toocreate necessario un gateway applicazione:

1. Creare un gruppo di risorse per Gestione risorse.
2. Creare una rete virtuale, subnet e l'indirizzo IP pubblico per il gateway applicazione hello.
3. Creare un oggetto di configurazione del gateway applicazione.
4. Creare una risorsa del gateway applicazione.

## <a name="create-a-resource-group-for-resource-manager"></a>Creare un gruppo di risorse per Gestione risorse

Assicurarsi che si utilizza hello la versione più recente di Azure PowerShell. Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Passaggio 1

Accedi tooAzure

```powershell
Login-AzureRmAccount
```

Si è tooauthenticate richiesta con le credenziali.<BR>

### <a name="step-2"></a>Passaggio 2

Controllare le sottoscrizioni di hello per account hello.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>Passaggio 3

Scegliere quali di toouse le sottoscrizioni di Azure. <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Passaggio 4

Creare un gruppo di risorse. Ignorare questo passaggio se si usa un gruppo di risorse esistente.

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

In alternativa, è anche possibile creare tag del gruppo di risorse per il gateway applicazione:

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso Questo gruppo di risorse viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse. Assicurarsi che tutti i comandi toocreate un hello di uso di gateway applicazione stesso gruppo di risorse.

Nell'esempio hello sopra, viene creato un gruppo di risorse denominato "appgw-RG" e il percorso "Stati Uniti occidentali".

> [!NOTE]
> Se è necessario tooconfigure un probe personalizzato per il gateway applicazione, vedere [creare un gateway applicazione con probe personalizzati usando PowerShell](application-gateway-create-probe-ps.md). Per altre informazioni, vedere l'articolo relativo a [probe personalizzati e monitoraggio dell'integrità](application-gateway-probe-overview.md) .
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Creare una rete virtuale e una subnet per il gateway applicazione hello

Hello seguente esempio viene illustrato come toocreate una rete virtuale usando Gestione risorse. Questo esempio viene creata una rete virtuale per hello Gateway applicazione. Gateway applicazione richiede il proprio subnet, per questo motivo subnet hello creata per il Gateway applicazione hello è minore di hello spazio degli indirizzi di rete virtuale. Altre risorse, incluse in questo modo, ma non limitata tooweb server toobe configurati in hello stesso rete virtuale.

### <a name="step-1"></a>Passaggio 1

Assegnare hello indirizzo intervallo 10.0.0.0/24 toohello subnet toobe variabile utilizzata toocreate una rete virtuale.  Questo crea l'oggetto di configurazione di subnet di hello per Gateway di applicazione, che viene utilizzato nell'esempio riportato di seguito hello hello.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a>Passaggio 2

Creare una rete virtuale denominata **appgwvnet** nel gruppo di risorse **appgw-rg** per area Stati Uniti occidentali hello con hello prefisso 10.0.0.0/16 10.0.0.0/24 subnet. Configurazione di hello di hello rete virtuale con una singola subnet per tooreside di Gateway applicazione hello è stata completata.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a>Passaggio 3

Assegnare variabile subnet hello per hello passaggi successivi, viene passato toohello `New-AzureRMApplicationGateway` cmdlet in un passaggio successivo.

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Creare un indirizzo IP pubblico per la configurazione front-end hello

Creare una risorsa IP pubblica **publicIP01** nel gruppo di risorse **appgw-rg** per area Stati Uniti occidentali hello. Gateway applicazione può utilizzare un indirizzo IP pubblico, l'indirizzo IP interno o entrambe le richieste tooreceive per il bilanciamento del carico.  Per questo esempio è stato usato solo un indirizzo IP pubblico. Nell'esempio seguente di hello, nessun nome DNS è configurato per la creazione di indirizzo IP pubblico hello.  Il gateway applicazione non supporta i nomi DNS personalizzati negli indirizzi IP pubblici.  Se un nome personalizzato è necessario per l'endpoint pubblico hello, un record CNAME deve essere creato nome DNS del toopoint toohello generato automaticamente per l'indirizzo IP pubblico hello.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Viene assegnato a un indirizzo IP gateway applicazione toohello all'avvio del servizio hello.

## <a name="create-application-gateway-configuration"></a>Creare la configurazione del gateway applicazione

Tutti gli elementi di configurazione necessario impostare prima di creare i gateway applicazione hello. Hello seguenti passaggi necessari per creare hello gli elementi di configurazione necessari per una risorsa di gateway applicazione.

### <a name="step-1"></a>Passaggio 1

Creare una configurazione IP del gateway applicazione denominata **gatewayIP01**. Avvio di Gateway applicazione preleva un indirizzo IP dalla subnet hello configurato e instradare gli indirizzi IP di toohello il traffico di rete nel pool IP back-end hello. Tenere presente che ogni istanza ha un indirizzo IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a>Passaggio 2

Configurare hello pool di indirizzi IP back-end denominato **pool01** e **pool2** con indirizzi IP per **pool1** e **pool2**. Questi indirizzi IP sono gli indirizzi IP hello delle risorse di hello che ospitano toobe di applicazione web hello protetti da gateway applicazione hello. Questi membri di pool back-end sono tutti toobe convalidato integro tramite probe base probe o probe personalizzati.  Il traffico viene indirizzato toothem quando le richieste provengano in gateway applicazione hello. Pool back-end può essere utilizzato da più regole all'interno di gateway applicazione hello, ovvero un pool back-end possono essere utilizzate per più applicazioni web che si trovano su hello stesso host.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

In questo esempio, sono disponibili due pool back-end tooroute il traffico di rete in base al percorso URL hello. Un pool riceve il traffico dal percorso dell'URL "/video" e l'altro riceve il traffico dal percorso "/image". Sostituire hello precedente tooadd gli indirizzi IP endpoint dell'indirizzo IP la propria applicazione. 

### <a name="step-3"></a>Passaggio 3

Configurare impostazioni del gateway applicazione **poolsetting01** e **poolsetting02** hello con bilanciamento del carico del traffico di rete nel pool back-end hello. In questo esempio, configurare le impostazioni del pool back-end diverso per il pool di back-end hello. Ogni pool back-end può avere un'impostazione del pool back-end dedicata.  Le impostazioni HTTP back-end vengono utilizzate per i membri del pool back-end corretto toohello traffico tooroute regole. Questo parametro determina il protocollo di hello e la porta utilizzata durante l'invio di traffico toohello i membri del pool back-end. Sessioni basate su cookie sono determinate anche dalle impostazioni HTTP back-end di hello.  Se abilitata, l'affinità di sessione basato su cookie invia traffico toohello stesso back-end come richieste precedenti per ogni pacchetto.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>Passaggio 4

Configurazione IP front-end hello con endpoint IP pubblico. oggetto di configurazione IP front-end Hello viene utilizzato un hello toorelate listener rivolti verso l'indirizzo IP con listener hello verso l'esterno.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>Passaggio 5

Configurare hello porta front-end per un gateway applicazione. oggetto di configurazione di Hello porta front-end viene utilizzato un toodefine listener cosa porta hello Gateway applicazione è in attesa del traffico listener hello.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a>Passaggio 6

Configurare il listener di hello. Questo passaggio consente di configurare il listener hello per l'indirizzo IP pubblico hello e la porta utilizzata tooreceive il traffico di rete in ingresso. Hello di esempio seguente accetta la configurazione IP front-end hello configurato in precedenza, la configurazione della porta front-end e un protocollo (http o https) e configura il listener hello. In questo esempio, il listener hello è in attesa di traffico tooHTTP sulla porta 80 all'indirizzo IP pubblico hello è stato creato in precedenza.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a>Passaggio 7

Configurare i percorsi di regola di URL per il pool di back-end hello. Questo passaggio consente di configurare un percorso di hello usato dal gateway di applicazione e definisce il mapping di hello tra il percorso di URL hello e un pool back-end hello viene assegnato il traffico in ingresso di toohandle hello.

> [!IMPORTANT]
> Ogni percorso deve iniziare con / e hello solo un "\*" è consentita, al fine di hello. Alcuni esempi validi sono /xyz, /xyz* o /xyz/*. Hello stringa inserito toohello matcher di percorso non include alcun testo dopo hello innanzitutto "?" o "#" e tali caratteri non consentiti. 

esempio Hello crea due regole: uno per il percorso "immagine /" routing del traffico "pool1" tooback-end e un'altra per "video /" percorso di routing del traffico tooback-end "pool2". Queste regole assicurano che il traffico per ogni set di URL di back-end toohello indirizzato. Ad esempio, http://contoso.com/image/figure1.jpg passa toopool1 e http://contoso.com/video/example.mp4 diventa toopool2.

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

Se il percorso di hello non corrisponde a una delle regole di percorso predefinito di hello, configurazione della mappa di hello regola percorso consente di configurare anche un pool di indirizzi back-end di predefinito. Ad esempio, http://contoso.com/shoppingcart/test.html passa toopool1 con cui è definito come il pool predefinito hello per il traffico non corrispondente.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a>Passaggio 8

Creare un'impostazione della regola. Questo passaggio Configura hello applicazione gateway toouse basato sul percorso routing degli URL. Hello `$urlPathMap` variabile definita in hello passaggio precedente è la regola adesso toocreate utilizzati hello basata sul percorso. In questo passaggio, Associamo regola hello con un listener e il mapping del percorso url hello creato in precedenza.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a>Passaggio 9:

Configurare hello numero di istanze e le dimensioni per il gateway applicazione hello.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Creare il gateway applicazione

Creare un gateway applicazione con tutti gli oggetti di configurazione da hello passaggi precedenti.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a>Ottenere il nome DNS del gateway applicazione

Una volta creato il gateway hello passaggio successivo hello è tooconfigure hello front-end per la comunicazione. Quando si usa un IP pubblico, il gateway applicazione richiede un nome DNS assegnato in modo dinamico, non descrittivo. gli utenti finali tooensure possibile raggiungere il gateway di applicazione hello, un record CNAME può essere utilizzati toopoint endpoint pubblico di toohello di gateway applicazione hello. [Configurazione di un nome di dominio personalizzato in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). front-end hello tooconfigure record CNAME IP, recuperare i dettagli del gateway applicazione hello e il relativo nome IP/DNS associato usando hello PublicIPAddress elemento collegato toohello applicazioni gateway. nome DNS del gateway applicazione Hello deve essere utilizzato toocreate un record CNAME. utilizzo di Hello del record non è consigliato poiché hello VIP potrebbe cambiare al riavvio del gateway applicazione.

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

Se si desidera toolearn offload Secure Sockets Layer (SSL), vedere [configurare un gateway applicazione per l'offload SSL](application-gateway-ssl-arm.md).

