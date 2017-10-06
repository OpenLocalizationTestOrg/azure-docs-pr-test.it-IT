---
title: aaaHow toouse gestione API di Azure nella rete virtuale con Gateway applicazione | Documenti Microsoft
description: Informazioni su come toosetup e configurare Gestione API di Azure in rete virtuale interna con applicazioni Gateway (WAF) come front-end
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a>Integrare Gestione API in una rete virtuale interna con un gateway applicazione 

##<a name="overview"></a> Panoramica
 
Hello servizio Gestione API può essere configurato in una rete virtuale in modalità interna che rende accessibile solo dall'interno hello rete virtuale. Il gateway applicazione di Azure è un servizio PAAS con bilanciamento del carico di livello 7. Funge da servizio proxy inverso e offre anche un Web application firewall (WAF).

La combinazione di gestione API, il provisioning in una rete virtuale interna con front-end di Gateway applicazione hello consente hello seguenti scenari:

* Utilizzare hello stessa risorsa di gestione API per l'utilizzo dal consumer interno sia utenti esterni.
* Uso di una singola risorsa di Gestione API e disponibilità di un sottoinsieme di API definite in Gestione API per gli utenti esterni.
* Fornire un tooAPI di accesso di tooswitch Gestione chiavi in modo da hello rete Internet pubblica e disattivare. 

##<a name="scenario"> </a> Scenario
In questo articolo verrà coprire come toouse un singolo Management API del servizio per i consumer interni ed esterni e consentono di agire come un singolo server front-end per entrambi locale e le API del cloud. Verrà visualizzato anche come tooexpose solo un subset delle API (nell'esempio hello vengono evidenziati in verde) per l'utilizzo esterno utilizzando hello PathBasedRouting funzionalità disponibili in Gateway applicazione.

Nel primo esempio il programma di installazione di hello tutte le API vengono gestite solo dall'interno della rete virtuale. Gli utenti interni (evidenziati in arancione) possono accedere a tutte le API interne ed esterne. Il traffico non viene mai salvato tooInternet che viene recapitato un ad alte prestazioni tramite circuiti Expressroute.

![route dell'URL](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <a name="before-you-begin"></a> Prima di iniziare

1. Installare più recente dei cmdlet di Azure PowerShell hello hello utilizzando hello installazione guidata piattaforma Web. È possibile scaricare e installare la versione più recente di hello da hello **Windows PowerShell** sezione di hello [pagina di download](https://azure.microsoft.com/downloads/).
2. Creare una rete virtuale e subnet separate per Gestione API e il gateway applicazione. 
3. Se si prevede un server DNS personalizzato per la rete virtuale hello toocreate, è possibile farlo prima di avviare la distribuzione hello. Verificare che funziona garantendo una macchina virtuale creata in una nuova subnet nella rete virtuale hello può risolvere e accedere a tutti gli endpoint di servizio di Azure.

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a>Che cos'è obbligatorio toocreate un'integrazione tra gestione API e di Gateway applicazione?

* **Pool di server back-end:** tratta hello interno indirizzo IP virtuale del servizio Gestione API hello.
* **Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie. Queste impostazioni sono applicate tooall server hello pool.
* **Porta front-end:** porta pubblica di hello che viene aperta su gateway applicazione hello. Traffico raggiungimento di si ottiene tooone reindirizzato di hello server back-end.
* **Listener:** listener hello dispone di una porta front-end, un protocollo (Http o Https, questi valori sono distinzione maiuscole/minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload).
* **Regola:** regola hello associa un pool di server back-end tooa listener.
* **Probe di integrità personalizzato:** Gateway applicazione, per impostazione predefinita, utilizza IP indirizzo basato su probe toofigure out server hello BackendAddressPool sono attivi. Servizio gestione API Hello risponde solo toorequests che presenta l'intestazione host corretto hello, pertanto probe predefiniti hello avere esito negativo. Un probe di integrità personalizzato deve toobe definito gateway applicazione toohelp determinare che il servizio hello è attivo e inoltra le richieste.
* **Certificato di dominio personalizzato:** tooaccess gestione API da hello internet è necessario toocreate un mapping CNAME del nome host toohello Gateway applicazione front-end nome DNS. Questo assicura che hello hostname intestazione e il certificato inviato tooApplication Gateway inoltrati tooAPI gestione sia uno in grado di riconoscere ruoli come valido.

## <a name="overview-steps"> </a> Passaggi necessari per l'integrazione di Gestione API e il gateway applicazione 

1. Creare un gruppo di risorse per Gestione risorse.
2. Creare una rete virtuale, subnet e l'indirizzo IP pubblico per hello Gateway applicazione. Creare un'altra subnet per Gestione API.
3. Creare un servizio di gestione API in subnet di rete virtuale hello creato in precedenza e accertarsi di utilizzare la modalità interna hello.
4. Nome di dominio personalizzato hello in hello servizio Gestione API del programma di installazione.
5. Creare un oggetto di configurazione del gateway applicazione.
6. Creare una risorsa gateway applicazione.
7. Creare un record CNAME dal nome DNS pubblico hello nomehost hello Gateway applicazione toohello gestione API proxy.

## <a name="create-a-resource-group-for-resource-manager"></a>Creare un gruppo di risorse per Gestione risorse

Assicurarsi che si utilizza hello la versione più recente di Azure PowerShell. Altre informazioni sono disponibili in [Uso di Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Passaggio 1

Accedi tooAzure

```powershell
Login-AzureRmAccount
```

Eseguire l'autenticazione con le proprie credenziali.<BR>

### <a name="step-2"></a>Passaggio 2

Controllare le sottoscrizioni di hello per account hello e selezionarlo.

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a>Passaggio 3

Creare un gruppo di risorse. Ignorare questo passaggio se si usa un gruppo di risorse esistente.

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso Viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse. Assicurarsi che tutti i comandi toocreate un hello di uso di gateway applicazione stesso gruppo di risorse.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Creare una rete virtuale e una subnet per il gateway applicazione hello

Hello di esempio seguente viene illustrato come una rete virtuale utilizzando toocreate hello Gestione risorse.

### <a name="step-1"></a>Passaggio 1

Assegnare hello indirizzo intervallo 10.0.0.0/24 toohello subnet variabile toobe utilizzato per il Gateway applicazione durante la creazione di una rete virtuale.

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a>Passaggio 2

Assegnare hello indirizzo intervallo 10.0.1.0/24 toohello subnet variabile toobe utilizzato per l'API di gestione durante la creazione di una rete virtuale.

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a>Passaggio 3

Creare una rete virtuale denominata **appgwvnet** nel gruppo di risorse **ruoli-appGw-RG** per area Stati Uniti occidentali hello utilizzando hello prefisso 10.0.0.0/16 con subnet 10.0.0.0/24 e 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a>Passaggio 4

Assegnare una variabile di subnet per i passaggi successivi hello

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a>Creare un servizio Gestione API in una rete virtuale configurata in modalità interna

Hello esempio seguente viene illustrato come toocreate un servizio di gestione API in una rete virtuale configurato per il solo accesso interno.

### <a name="step-1"></a>Passaggio 1
Creare un oggetto di rete virtuale di gestione API mediante subnet hello $apimsubnetdata creato in precedenza.

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a>Passaggio 2
Creare un servizio di gestione API all'interno di hello rete virtuale.

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
Dopo hello sopra comando ha esito positivo, consultare troppo[necessaria una configurazione DNS del servizio Gestione API di rete virtuale interno tooaccess](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess è.

## <a name="set-up-a-custom-domain-name-in-api-management"></a>Configurare un nome di dominio personalizzato in Gestione API

### <a name="step-1"></a>Passaggio 1
Caricare il certificato di hello con la chiave privata per il dominio hello. Per questo esempio sarà `*.contoso.net`. 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a>Passaggio 2
Una volta caricato il certificato di hello, creare un oggetto di configurazione di nome host per il proxy di hello con un nome host di `api.contoso.net`, come certificato di esempio hello fornisce autorità per hello `*.contoso.net` dominio. 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Creare un indirizzo IP pubblico per la configurazione front-end hello

Creare una risorsa IP pubblica **publicIP01** nel gruppo di risorse **ruoli-appGw-RG** per area Stati Uniti occidentali hello.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

Viene assegnato a un indirizzo IP gateway applicazione toohello all'avvio del servizio hello.

## <a name="create-application-gateway-configuration"></a>Creare la configurazione del gateway applicazione

Tutti gli elementi di configurazione necessario impostare prima di creare i gateway applicazione hello. Hello seguenti passaggi necessari per creare hello gli elementi di configurazione necessari per una risorsa di gateway applicazione.

### <a name="step-1"></a>Passaggio 1

Creare una configurazione IP del gateway applicazione denominata **gatewayIP01**. Avvio di Gateway applicazione preleva un indirizzo IP dalla subnet hello configurato e instradare gli indirizzi IP di toohello il traffico di rete nel pool IP back-end hello. Tenere presente che ogni istanza ha un indirizzo IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a>Passaggio 2

Configurare una porta IP front-end di hello per endpoint IP pubblico hello. Questa porta è porta hello in grado di connettersi agli utenti finali.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a>Passaggio 3

Configurazione IP front-end hello con endpoint IP pubblico.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a>Passaggio 4

Configurare il certificato di hello per Gateway di applicazione, hello utilizzato toodecrypt e crittografa nuovamente traffico hello passano attraverso.

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a>Passaggio 5

Creare il listener HTTP hello per hello Gateway applicazione. Assegnare una configurazione IP front-end hello, porta e tooit certificato ssl.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a>Passaggio 6

Creare un servizio di gestione API di toohello probe personalizzato `ContosoApi` endpoint proxy per dominio. percorso Hello `/status-0123456789abcdef` è ospitato in tutti i servizi di gestione API hello un endpoint di integrità predefinito. Impostare `api.contoso.net` come un toosecure nome host di tipo probe personalizzato con certificato SSL.

> [!NOTE]
> Hello hostname `contosoapi.azure-api.net` nome host di proxy predefinito hello configurato quando un servizio denominato `contosoapi` creato in Azure pubblica. 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a>Passaggio 7

Caricare il certificato di hello toobe utilizzato per le risorse di pool di hello SSL abilitato back-end. Si tratta di hello stesso certificato che è fornito nel passaggio 4 precedente.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a>Passaggio 8

Configurare le impostazioni HTTP back-end hello Gateway applicazione. Questo passaggio include l'impostazione di un limite di timeout per la richiesta del back-end, raggiunto il quale verrà annullata. Questo valore è diverso dal timeout probe hello.

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a>Passaggio 9:

Configurare un pool di indirizzi IP back-end denominato **apimbackend** con indirizzo IP virtuale interno hello indirizzo del servizio Gestione API hello creato in precedenza.

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a>Passaggio 10

Creare le impostazioni per un back-end fittizio (inesistente). I percorsi di tooAPI di richieste che non si desidera tooexpose da Gestione API tramite il Gateway applicazione verranno raggiunto questo back-end e restituire l'errore 404.

Configurare le impostazioni HTTP back-end fittizio di hello.

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

Configurare un back-end fittizio **dummyBackendPool**, vale a dire indirizzo FQDN tooa **dummybackend.com**. Questo indirizzo FQDN non esiste nella rete virtuale hello.

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

Creare una regola di impostazione che hello Gateway applicazione utilizzerà per impostazione predefinita che punta back-end inesistente toohello **dummybackend.com** in hello rete virtuale.

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a>Passaggio 11

Configurare i percorsi di regola di URL per il pool di back-end hello. In questo modo selezionando solo alcune delle hello le API di gestione API per essere esposte toohello pubblico. Ad esempio, se esistono `Echo API` (/echo/), `Calculator API` (/calc/) e così via, è possibile rendere accessibile da Internet solo `Echo API`. 

Hello esempio seguente viene creata una semplice regola per hello "echo /" percorso routing del traffico toohello back-end "apimProxyBackendPool".

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

Se non corrisponde a percorso hello percorso hello regole desideriamo tooenable dalla gestione API, regola hello configurazione mappa percorso consente di configurare anche un pool di indirizzi back-end di predefinito denominato **dummyBackendPool**. Ad esempio, http://api.contoso.net/calc/ * diventa troppo**dummyBackendPool** con cui è definito come il pool predefinito hello per il traffico senza corrispondenza.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

Hello sopra passaggio garantisce che solo le richieste per il percorso di hello "/ echo" siano consentiti attraverso il Gateway applicazione hello. Tooother richieste che API configurate in Gestione API genererà 404 errori dal Gateway applicazione quando si accede da hello Internet. 

### <a name="step-12"></a>Passaggio 12

Creare un'impostazione di regole per hello Gateway applicazione toouse basato sul percorso routing degli URL.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a>Passaggio 13

Configurare hello numero di istanze e le dimensioni per hello Gateway applicazione. Qui utilizziamo hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) per aumentare la protezione di hello risorse di gestione API.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a>Passaggio 14

Configurare WAF toobe in modalità "Programmi".
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a>Creare il gateway applicazione

Creare un Gateway applicazione con tutti gli oggetti di configurazione hello da hello passaggi precedenti.

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a>CNAME hello gestione API proxy hostname toohello nome DNS pubblico del hello risorse Gateway applicazione

Una volta creato il gateway hello passaggio successivo hello è tooconfigure hello front-end per la comunicazione. Quando si utilizza un indirizzo IP pubblico, Gateway applicazione richiede un nome DNS assegnato dinamicamente, che potrebbe non essere toouse semplice. 

Hello nome DNS del Gateway applicazione deve essere utilizzato toocreate un record CNAME che punta nome host di hello ruoli proxy (ad esempio `api.contoso.net` negli esempi di hello sopra) toothis il nome DNS. front-end hello tooconfigure record CNAME IP, recuperare i dettagli di hello di Gateway applicazione hello e il relativo nome IP/DNS associato utilizzando l'elemento PublicIPAddress hello. utilizzo di Hello del record non è consigliato poiché hello VIP potrebbe cambiare al riavvio del gateway.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<a name="summary"></a> Riepilogo
Gestione API di Azure configurato in una rete virtuale fornisce un'interfaccia di gateway singolo per tutte le API configurate, se sono ospitati in locale o nel cloud hello. L'integrazione di Gateway applicazione con l'API di gestione offre la flessibilità di hello di attivazione selettiva particolare toobe di API accessibile su Internet hello, nonché di fornire un Firewall applicazione Web come un'istanza di gestione API tooyour front-end.

##<a name="next-steps"></a> Passaggi successivi
* Altre informazioni sul gateway applicazione di Azure
  * [Panoramica del gateway applicazione](../application-gateway/application-gateway-introduction.md)
  * [Web application firewall del gateway applicazione](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [Creare un gateway applicazione con il routing basato sul percorso](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* Altre informazioni su Gestione API e reti virtuali
  * [Utilizzo di gestione API disponibile solo all'interno di hello rete virtuale](api-management-using-with-internal-vnet.md)
  * [Usare Gestione API in una rete virtuale](api-management-using-with-vnet.md)
