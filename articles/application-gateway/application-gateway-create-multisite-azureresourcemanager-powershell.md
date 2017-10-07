---
title: "un gateway applicazione per ospitare più siti aaaCreate | Documenti Microsoft"
description: "Questa pagina fornisce istruzioni toocreate, configurare un gateway applicazione Azure per ospitare più applicazioni web su hello stesso gateway."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a>Creare un gateway applicazione per l'hosting di più applicazioni Web

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-create-multisite-portal.md)
> * [PowerShell per Azure Resource Manager](application-gateway-create-multisite-azureresourcemanager-powershell.md)

Hosting di più siti consente toodeploy più di una sola applicazione web su hello stesso gateway applicazione. Si basa su presenza dell'intestazione host nella richiesta HTTP in ingresso hello, toodetermine quali listener riceve traffico. listener di Hello indirizza quindi il pool back-end tooappropriate traffico come configurato nella definizione delle regole hello del gateway hello. Nelle applicazioni web SSL abilitato, i gateway applicazione si basa su hello indicazione nome Server (SNI) estensione toochoose hello corretto del listener per il traffico web hello. Viene in genere utilizzata per l'hosting del sito più tooload bilanciamento delle richieste per i pool di server back-end web diversi domini toodifferent. Analogamente, più sottodomini del dominio radice della stessa può essere ospitato su hello hello stesso gateway applicazione.

## <a name="scenario"></a>Scenario

Nell'esempio seguente di hello, gateway applicazione gestisce il traffico per contoso.com e fabrikam.com con due pool di server back-end: contoso pool di server e il pool di server di fabrikam. Il programma di installazione simile potrebbe essere sottodomini toohost usato come app.contoso.com e blog.contoso.com.

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a>Prima di iniziare

1. Installare più recente dei cmdlet di Azure PowerShell hello hello utilizzando hello installazione guidata piattaforma Web. È possibile scaricare e installare la versione più recente di hello da hello **Windows PowerShell** sezione di hello [pagina di download](https://azure.microsoft.com/downloads/).
2. server Hello aggiunto deve essere presente il gateway applicazione hello di toohello pool back-end toouse o i relativi endpoint creato in una rete virtuale di hello in una subnet distinta o con un indirizzo IP/VIP pubblico assegnato.

## <a name="requirements"></a>Requisiti

* **Pool di server back-end:** elenco hello di indirizzi IP dei server back-end hello. gli indirizzi IP Hello elencati devono appartenere toohello subnet della rete virtuale o devono essere un indirizzo IP/VIP pubblico. È possibile usare anche FQDN.
* **Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie. Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.
* **Porta front-end:** questa porta è una porta pubblica hello aperta sul gateway applicazione hello. Traffico riscontri questa porta, e quindi ottiene reindirizzato tooone dei server back-end hello.
* **Listener:** listener hello dispone di una porta front-end, un protocollo (Http o Https, questi valori sono distinzione maiuscole/minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload). Per i gateway applicazione abilitati per più siti vengono aggiunti anche indicatori SNI e nome host.
* **Regola:** regola hello associa listener hello, pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener. Le regole vengono elaborate in ordine di hello che sono elencati e il traffico verrà indirizzato tramite hello prima regola che corrisponde indipendentemente dal fatto di specificità. Ad esempio, se si dispone di una regola di utilizzo di un listener di base e una regola di utilizzo di un listener multisito entrambi nella stessa regola di porta, hello con hello listener multisito hello deve essere elencato prima regola hello con listener di base hello affinché hello multisito regola toofunction come previsto.

## <a name="create-an-application-gateway"></a>Creare un gateway applicazione

di seguito Hello sono passaggi hello necessari toocreate un gateway applicazione.

1. Creare un gruppo di risorse per Gestione risorse.
2. Creare una rete virtuale, subnet e indirizzo IP pubblico per il gateway applicazione hello.
3. Creare un oggetto di configurazione del gateway applicazione.
4. Creare una risorsa del gateway applicazione.

## <a name="create-a-resource-group-for-resource-manager"></a>Creare un gruppo di risorse per Gestione risorse

Assicurarsi che si utilizza hello la versione più recente di Azure PowerShell. Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Passaggio 1

Accedi tooAzure

```powershell
Login-AzureRmAccount
```
Si è tooauthenticate richiesta con le credenziali.

### <a name="step-2"></a>Passaggio 2

Controllare le sottoscrizioni di hello per account hello.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>Passaggio 3

Scegliere quali di toouse le sottoscrizioni di Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Passaggio 4

Creare un gruppo di risorse. Ignorare questo passaggio se si usa un gruppo di risorse esistente.

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

In alternativa, è anche possibile creare tag del gruppo di risorse per il gateway applicazione:

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso Questo percorso viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse. Assicurarsi che tutti i comandi toocreate un hello di uso di gateway applicazione stesso gruppo di risorse.

Nell'esempio hello sopra, è stato creato un gruppo di risorse denominato **appgw-RG** con un percorso di **Stati Uniti occidentali**.

> [!NOTE]
> Se è necessario tooconfigure un probe personalizzato per il gateway applicazione, vedere [creare un gateway applicazione con probe personalizzati usando PowerShell](application-gateway-create-probe-ps.md). Per altre informazioni, vedere l'articolo relativo a [probe personalizzati e monitoraggio dell'integrità](application-gateway-probe-overview.md) .

## <a name="create-a-virtual-network-and-subnets"></a>Creare una rete virtuale e le subnet

Hello seguente esempio viene illustrato come toocreate una rete virtuale usando Gestione risorse. In questo passaggio vengono create due subnet. prima di subnet Hello è per il gateway applicazione hello stesso. Gateway applicazione richiede il proprio toohold subnet delle istanze. In tale subnet possono essere distribuiti solo altri gateway applicazione. subnet secondo Hello è server back-end di applicazione hello toohold utilizzato.

### <a name="step-1"></a>Passaggio 1

Assegnare hello indirizzo intervallo 10.0.0.0/24 toohello subnet toobe variabile toohold utilizzati hello gateway applicazione.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a>Passaggio 2

Assegnare hello indirizzo intervallo 10.0.1.0/24 toohello subnet2 variabile toobe utilizzato per il pool di back-end hello.

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a>Passaggio 3

Creare una rete virtuale denominata **appgwvnet** nel gruppo di risorse **appgw-rg** per area Stati Uniti occidentali hello con hello prefisso 10.0.0.0/16 10.0.0.0/24 subnet e 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a>Passaggio 4

Assegnare una variabile di subnet per i passaggi successivi hello, che consente di creare un gateway applicazione.

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Creare un indirizzo IP pubblico per la configurazione front-end hello

Creare una risorsa IP pubblica **publicIP01** nel gruppo di risorse **appgw-rg** per area Stati Uniti occidentali hello.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Viene assegnato a un indirizzo IP gateway applicazione toohello all'avvio del servizio hello.

## <a name="create-application-gateway-configuration"></a>Creare la configurazione del gateway applicazione

Hai tooset backup di tutti gli elementi di configurazione prima di creare i gateway applicazione hello. Hello seguenti passaggi necessari per creare hello gli elementi di configurazione necessari per una risorsa di gateway applicazione.

### <a name="step-1"></a>Passaggio 1

Creare una configurazione IP del gateway applicazione denominata **gatewayIP01**. Avvio di gateway applicazione preleva un indirizzo IP dalla subnet hello configurato e instradare gli indirizzi IP di toohello il traffico di rete nel pool IP back-end hello. Tenere presente che ogni istanza ha un indirizzo IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a>Passaggio 2

Configurare hello pool di indirizzi IP back-end denominato **pool01** e **pool2** con indirizzi IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** per **pool1** e **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  per **pool2**.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

In questo esempio, sono disponibili due pool back-end tooroute il traffico di rete basato su sito richiesto hello. Un pool riceve il traffico dal sito "contoso.com" e l'altro riceve il traffico dal sito "fabrikam.com". È necessario hello tooreplace precedente tooadd gli indirizzi IP endpoint dell'indirizzo IP la propria applicazione. Al posto di indirizzi IP interni si potrebbero usare per le istanze back-end anche indirizzi IP pubblici, FQDN o la scheda di interfaccia di rete di una VM. toospecify FQDN anziché gli indirizzi IP in uso di PowerShell "-BackendFQDNs" parametro.

### <a name="step-3"></a>Passaggio 3

Configurare impostazioni del gateway applicazione **poolsetting01** e **poolsetting02** hello con bilanciamento del carico del traffico di rete nel pool back-end hello. In questo esempio, configurare le impostazioni del pool back-end diverso per il pool di back-end hello. Ogni pool back-end può avere un'impostazione del pool back-end dedicata.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>Passaggio 4

Configurazione IP front-end hello con endpoint IP pubblico.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>Passaggio 5

Configurare hello porta front-end per un gateway applicazione.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a>Passaggio 6

Configurare due i certificati SSL per i siti Web hello due verrà toosupport in questo esempio. È un certificato per il traffico di contoso.com e altri hello è per il traffico fabrikam.com. Questi certificati per i siti Web devono essere rilasciati da un'autorità di certificazione. I certificati autofirmati sono supportati, ma non sono consigliati per il traffico di produzione.

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a>Passaggio 7

In questo esempio, configurare due listener per hello due siti web. Questo passaggio consente di configurare i listener di hello per host, porta e indirizzo IP pubblico usato tooreceive il traffico in entrata. Parametro HostName è obbligatorio per il supporto del sito e deve essere toohello appropriato siti Web per cui hello ricezione del traffico. Parametro RequireServerNameIndication deve essere impostato tootrue per i siti Web che necessitano di supporto per SSL in uno scenario con più host. Se è richiesto il supporto SSL, è necessario anche toospecify hello SSL certificato traffico toosecure utilizzato per l'applicazione web. combinazione di Hello di FrontendIPConfiguration front-end e il nome host deve essere univoco tooa listener. Ogni listener può supportare un certificato.

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a>Passaggio 8

Creare due regola impostazione per hello due applicazioni web in questo esempio. Una regola collega listener, pool back-end e impostazioni HTTP. Questo passaggio Configura hello applicazione gateway toouse base regola di routing, uno per ogni sito Web. Sito Web tooeach il traffico viene ricevuto dal relativo listener configurato e viene quindi indirizzato tooits configurato pool back-end, utilizzando le proprietà di hello specificate in hello BackendHttpSettings.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a>Passaggio 9:

Configurare hello numero di istanze e le dimensioni per il gateway applicazione hello.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Creare il gateway applicazione

Creare un gateway applicazione con tutti gli oggetti di configurazione da hello passaggi precedenti.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> Provisioning di Gateway applicazione è un'operazione a esecuzione prolungata e potrebbe richiedere alcuni toocomplete ora.
> 
> 

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

Informazioni su come tooprotect i siti Web con [Gateway applicazione - Firewall applicazione Web](application-gateway-webapplicationfirewall-overview.md)

