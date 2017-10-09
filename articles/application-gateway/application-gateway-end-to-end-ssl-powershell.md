---
title: aaaConfigure fine tooend SSL con Gateway applicazione Azure | Documenti Microsoft
description: In questo articolo viene descritto come tooconfigure terminare tooend SSL con il Gateway applicazione usando Gestione risorse di Azure PowerShell
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a>Configurare tooend fine SSL con il Gateway applicazione con PowerShell

## <a name="overview"></a>Panoramica

Supporta Gateway applicazione finale tooend la crittografia del traffico. Gateway applicazione esegue questa operazione terminerà hello di connessione SSL al gateway applicazione hello. gateway Hello Applica regole di routing hello traffico toohello, crittografare nuovamente i pacchetti hello e inoltra hello pacchetto toohello back-end appropriati in base alle regole di routing hello definite. Le risposte dal server web hello attraversa hello stessa procedura adottata toohello back-end utente.

Un'altra funzionalità supportata dal gateway applicazione è la definizione delle opzioni SSL personalizzate. Gateway applicazione supporta hello disabilitando la seguente versione di protocollo. **TLSv1.0**, **TLSv1.1**, e **TLSv1.2** anche la definizione di hello che codifica ordine toouse e hello di gruppi di preferenza.  toolearn più sulle opzioni configurabili SSL, visitare [Panoramica criteri SSL](application-gateway-SSL-policy-overview.md).

> [!NOTE]
> SSL 2.0 e SSL 3.0 sono disabilitati per impostazione predefinita e non possono essere abilitati. Questi sono considerati non sicuri e non sono in grado di toobe utilizzato con Gateway applicazione.

![immagine dello scenario][scenario]

## <a name="scenario"></a>Scenario

In questo scenario viene illustrato come toocreate gateway un'applicazione che utilizza end tooend SSL tramite PowerShell.

Questo scenario illustrerà come:

* Creare un gruppo di risorse denominato **appgw-rg**
* Creare una rete virtuale denominata **appgwvnet** con uno spazio indirizzi 10.0.0.0/16.
* Creare due subnet denominate **appgwsubnet** e **appsubnet**.
* Creare una piccola applicazione gateway supporto end tooend la crittografia SSL che limiti versioni di protocolli SSL e i pacchetti di crittografia.

## <a name="before-you-begin"></a>Prima di iniziare

fine tooconfigure tooend SSL con un gateway applicazione, è necessario per il gateway hello un certificato e i certificati sono necessari per i server back-end hello. certificato di gateway Hello è utilizzato tooencrypt e decrittografia hello il traffico inviato tooit mediante SSL. certificato di gateway Hello deve toobe nel formato di scambio di informazioni personali (pfx). Questo formato di file consente di hello privata toobe chiave esportato richiesto dal hello applicazione gateway tooperform hello crittografia e decrittografia del traffico.

Per end tooend SSL crittografia hello back-end deve essere abilitata con gateway applicazione. Questa operazione viene eseguita dal caricamento hello certificato pubblico del gateway applicazione toohello di hello back-end. In questo modo si garantisce che il gateway applicazione hello comunica solo con istanze di back-end noti. Questo protegge ulteriormente la comunicazione di tooend end hello.

Questo processo è descritto in hello alla procedura seguente:

## <a name="create-hello-resource-group"></a>Creare hello gruppo di risorse

Questa sezione viene illustrata la creazione di un gruppo di risorse, che contiene i gateway applicazione hello.

### <a name="step-1"></a>Passaggio 1

Accedi tooyour Account Azure.

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Passaggio 2

Selezionare hello toouse di sottoscrizione per questo scenario.

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a>Passaggio 3

Creare un gruppo di risorse. Ignorare questo passaggio se si usa un gruppo di risorse esistente.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Creare una rete virtuale e una subnet per il gateway applicazione hello

Hello seguente viene creata una rete virtuale e due subnet. Gateway applicazione hello di toohold usato è una subnet. le altre subnet Hello viene utilizzato per hello back-end web hosting hello applicazione.

### <a name="step-1"></a>Passaggio 1

Assegnare un intervallo di indirizzi per subnet hello da utilizzare per hello Gateway applicazione stessa.

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> Le subnet configurate per il gateway applicazione devono essere ridimensionate in modo corretto. Un gateway applicazione può essere configurato per le istanze di too10. Ogni istanza richiede un indirizzo IP dalla subnet hello. Le dimensioni eccessivamente piccole di una subnet possono influire negativamente sull'aumento del numero di istanze di un gateway applicazione.
> 
> 

### <a name="step-2"></a>Passaggio 2

Assegnare un toobe intervallo di indirizzi utilizzato per il pool di indirizzi back-end hello.

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a>Passaggio 3

Creare una rete virtuale con subnet hello definita in hello passaggi precedenti.

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a>Passaggio 4

Recuperare hello rete virtuale risorse e la subnet risorse toobe utilizzato in hello alla procedura seguente:

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Creare un indirizzo IP pubblico per la configurazione front-end hello

Creare un toobe di risorsa IP pubblica utilizzata per il gateway applicazione hello. Questo indirizzo IP pubblico viene usato in uno dei prossimi passaggi.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> Gateway applicazione non supporta l'utilizzo di hello di un indirizzo IP pubblico creato con un'etichetta di dominio definita. È supportato solo un indirizzo IP pubblico con etichetta di dominio creata in modo dinamico. Se è necessario un nome descrittivo di dns per il gateway applicazione hello, si consiglia di registrare un record CNAME toouse come alias.

## <a name="create-an-application-gateway-configuration-object"></a>Creare un oggetto di configurazione gateway applicazione

Tutti gli elementi di configurazione vengono impostati prima di creare i gateway applicazione hello. Hello seguenti passaggi necessari per creare hello gli elementi di configurazione necessari per una risorsa di gateway applicazione.

### <a name="step-1"></a>Passaggio 1

Creare una configurazione IP del gateway applicazione, questa impostazione configura utilizzi gateway applicazione hello subnet. Avvio di gateway applicazione preleva un indirizzo IP dalla subnet hello configurato e lo indirizza gli indirizzi IP di toohello il traffico di rete nel pool IP back-end hello. Tenere presente che ogni istanza ha un indirizzo IP.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a>Passaggio 2

Creare una configurazione IP front-end, questa impostazione esegue il mapping di un ip pubblico o privato indirizzo toohello front-end del gateway applicazione hello. Hello riportata dopo il passaggio Associa indirizzo IP pubblico hello nel precedente passaggio con configurazione IP front-end hello hello.

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a>Passaggio 3

Configurare i pool di indirizzi IP di hello back-end con indirizzi IP hello del server web back-end di hello. Questi indirizzi IP sono gli indirizzi IP hello che ricevono il traffico di rete hello proveniente dall'endpoint IP front-end hello. Sostituire hello seguente tooadd gli indirizzi IP endpoint dell'indirizzo IP la propria applicazione.

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> Un nome di dominio completo (FQDN) è un valore valido al posto di un indirizzo ip per i server back-end hello tramite commutatore - BackendFqdns hello. 

### <a name="step-4"></a>Passaggio 4

Configurare una porta IP front-end di hello per endpoint IP pubblico hello. Questa porta è porta hello in grado di connettersi agli utenti finali.

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a>Passaggio 5

Configurare hello certificato per il gateway applicazione hello. Questo certificato viene utilizzato toodecrypt e crittografa nuovamente traffico hello gateway applicazione hello.

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> Questo esempio Configura certificato hello utilizzato per la connessione SSL. certificato Hello deve toobe in formato PFX e password hello deve essere compresa tra 4 too12 caratteri.

### <a name="step-6"></a>Passaggio 6

Creare il listener HTTP hello per il gateway applicazione hello. Assegnare una configurazione ip front-end di hello, porta e toouse certificato SSL.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a>Passaggio 7

Caricare il certificato di hello toobe utilizzato su hello SSL abilitato risorse del pool back-end.

> [!NOTE]
> probe predefinito Hello Ottiene la chiave pubblica di hello da hello **predefinito** associazione SSL per l'indirizzo IP hello back-end e confronta hello valore della chiave pubblica riceve toohello valore della chiave pubblica qui. Hello recuperata la chiave pubblica potrebbe non essere necessariamente flussi di traffico hello destinato sito toowhich **se** si utilizzano intestazioni host e SNI hello back-end. In caso di dubbio, visitare https://127.0.0.1/ tooconfirm back-end hello quale certificato viene utilizzato per hello **predefinito** binding SSL. Utilizzare una chiave pubblica di hello dalla richiesta in questa sezione. Se si utilizzano intestazioni host e SNI associazioni HTTPS e non si riceve una risposta e il certificato da un toohttps://127.0.0.1/ richiesta browser manuale in hello back-end, è necessario configurare un binding SSL predefinito in hello back-end. Se non, probe esito negativo e hello back-end non è abilitata.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> certificato Hello fornito in questo passaggio deve essere una chiave pubblica di hello del certificato pfx hello presente nel back-end hello. Esportare il certificato di hello (non certificato radice hello) installato nel server back-end hello in. CER formattare e utilizzarlo in questo passaggio. Delle whitelist passaggio hello back-end con gateway applicazione hello.

### <a name="step-8"></a>Passaggio 8

Configurare le impostazioni http back-end di gateway applicazione hello. Assegnare il certificato di hello caricato nel precedente passaggio toohello http impostazioni hello.

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a>Passaggio 9:

Creare una regola di routing bilanciamento del carico che configura il comportamento del servizio di bilanciamento carico di hello. In questo esempio viene creata una regola round robin di base.

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a>Passaggio 10

Configurare le dimensioni di istanza hello del gateway applicazione hello.  sono di dimensioni disponibili Hello **Standard\_Small**, **Standard\_Media**, e **Standard\_grande**.  Per la capacità, i valori disponibili hello sono 1 e 10.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> A scopo di test si può scegliere 1 come numero di istanze. È importante che tutte le istanze in due istanze di contare tooknow non coperto da hello contratto di servizio e pertanto non sono consigliati. Gateway di piccole dimensioni sono toobe utilizzato per il test di sviluppo e non per scopi di produzione.

### <a name="step-11"></a>Passaggio 11

Configurare hello SSL criteri toobe utilizzato su hello Gateway applicazione. Gateway applicazione supporta hello possibilità tooset una versione minima per le versioni protocollo SSL.

Hello i valori seguenti sono un elenco delle versioni del protocollo che possono essere definiti.

* **TLSv1_0**
* **TLSv1_1**
* **TLSv1_2**

Set di hello versione del protocollo minimo troppo**TLSv1_2** ed **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_ SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**e **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** solo.

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a>Creare hello Gateway applicazione

Utilizzando hello tutti i passaggi precedenti, creare hello Gateway applicazione. creazione di Hello del gateway hello è un processo a esecuzione prolungata.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a>Limitare le versioni del protocollo SSL in un gateway applicazione esistente

Hello passaggi precedenti consentono di creazione di un'applicazione con tooend fine SSL e la disabilitazione di alcune versioni del protocollo SSL. Hello seguente disabilita determinati criteri SSL un gateway applicazione esistente.

### <a name="step-1"></a>Passaggio 1

Recuperare tooupdate di gateway applicazione hello.

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a>Passaggio 2

Definire un criterio SSL. Nell'esempio seguente di hello, TLSv1.0 e TLSv1.1 sono disattivati e hello pacchetti di crittografia **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, e  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** è hello soli quelli consentiti.

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a>Passaggio 3

Infine, aggiornare il gateway hello. È importante toonote che quest'ultimo passaggio è un'attività a esecuzione prolungata. Al termine, terminare tooend che SSL configurato nel gateway applicazione hello.

```powershell
$gw | Set-AzureRmApplicationGateway
```

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

Informazioni sulla protezione avanzata di sicurezza hello delle applicazioni web con Web Application Firewall tramite il Gateway applicazione visitando [Panoramica del Firewall applicazione Web](application-gateway-webapplicationfirewall-overview.md)

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
