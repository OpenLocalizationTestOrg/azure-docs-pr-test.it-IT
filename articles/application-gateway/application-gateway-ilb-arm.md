---
title: Gateway applicazione Azure con bilanciamento del carico interno - PowerShell aaaUsing | Documenti Microsoft
description: Questa pagina vengono fornite istruzioni toocreate, configurare, avviare ed eliminare un gateway applicazione Azure con bilanciamento del carico interno (ILB) per Gestione risorse di Azure
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: dd0d7e954b1fa219ae6ebe42cb4b479dbcf08653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a>Creare un gateway applicazione con un dispositivo di bilanciamento del carico interno (ILB) tramite Gestione risorse di Azure

> [!div class="op_single_selector"]
> * [PowerShell per Azure classico](application-gateway-ilb.md)
> * [PowerShell per Azure Resource Manager](application-gateway-ilb-arm.md)

Gateway applicazione Azure può essere configurato con un indirizzo VIP rivolto a Internet o con un endpoint interno non è esposto toohello Internet, noto anche come un endpoint di (ILB) del servizio di bilanciamento del carico interno. Configurazione di gateway hello con un bilanciamento del carico interno è utile per applicazioni line-of-business interne che non sono esposto toohello Internet. È inoltre utile per i servizi e i livelli all'interno di un'applicazione multilivello che si trovano in un limite di sicurezza che non è esposto toohello Internet, ma richiedono comunque round-robin caricano distribuzione, l'aderenza sessione o terminazione Secure Sockets Layer (SSL).

In questo articolo illustra i passaggi di hello tooconfigure un gateway applicazione con un bilanciamento del carico interno.

## <a name="before-you-begin"></a>Prima di iniziare

1. Installare più recente dei cmdlet di Azure PowerShell hello hello utilizzando hello installazione guidata piattaforma Web. È possibile scaricare e installare la versione più recente di hello da hello **Windows PowerShell** sezione di hello [pagina di download](https://azure.microsoft.com/downloads/).
2. Creare una rete virtuale e una subnet per il gateway applicazione. Assicurarsi che nessun macchine virtuali o le distribuzioni di cloud utilizza subnet hello. Il gateway applicazione deve essere da solo in una subnet di rete virtuale.
3. deve esistere server Hello configurare gateway di applicazione hello toouse o disporre i relativi endpoint creato nella rete virtuale hello o con un indirizzo IP/VIP pubblico.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Che cos'è toocreate necessario un gateway applicazione?

* **Pool di server back-end:** elenco hello di indirizzi IP dei server back-end hello. Hello indirizzi IP elencati devono appartenere toohello di rete virtuale, ma in un'altra subnet per il gateway applicazione hello o deve essere un indirizzo IP/VIP pubblico.
* **Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie. Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.
* **Porta front-end:** questa porta è una porta pubblica hello aperta sul gateway applicazione hello. Traffico riscontri questa porta, e quindi ottiene reindirizzato tooone dei server back-end hello.
* **Listener:** listener hello dispone di una porta front-end, un protocollo (Http o Https, si tratta tra maiuscole e minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload).
* **Regola:** regola hello associa listener hello e pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener. Attualmente, solo hello *base* regola supportata. Hello *base* regola è una distribuzione del carico round robin.

## <a name="create-an-application-gateway"></a>Creare un gateway applicazione

differenza Hello tra l'utilizzo di Azure classico e Gestione risorse di Azure è ordine hello in cui è stato creato il gateway di applicazione hello e gli elementi hello necessario toobe configurato.
Gestione risorse di tutti gli elementi che costituiscono un gateway applicazione viene configurata singolarmente e riunire risorsa per il gateway applicazione toocreate hello.

Ecco i passaggi hello toocreate necessario un gateway applicazione:

1. Creare un gruppo di risorse per Gestione risorse
2. Creare una rete virtuale e una subnet per il gateway applicazione hello
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

Creare un nuovo gruppo di risorse. Ignorare questo passaggio se si sta usando un gruppo di risorse esistente.

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

Gestione risorse di Azure richiede che tutti i gruppi di risorse specifichino un percorso Viene utilizzato come percorso predefinito di hello per le risorse in tale gruppo di risorse. Assicurarsi che tutti i comandi toocreate utilizza un gateway applicazione hello stesso gruppo di risorse.

In hello sopra riportato, è stato creato un gruppo di risorse denominato "Appgw-rg" e il percorso "Stati Uniti occidentali".

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Creare una rete virtuale e una subnet per il gateway applicazione hello

Hello seguente esempio viene illustrato come toocreate una rete virtuale usando Gestione risorse:

### <a name="step-1"></a>Passaggio 1

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

Questo passaggio assegna hello indirizzo intervallo 10.0.0.0/24 tooa subnet toobe variabile utilizzata toocreate una rete virtuale.

### <a name="step-2"></a>Passaggio 2

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

Questo passaggio viene creata una rete virtuale denominata "appgwvnet" nella risorsa gruppo "appgw-rg" per area Stati Uniti occidentali hello con hello prefisso 10.0.0.0/16 10.0.0.0/24 subnet.

### <a name="step-3"></a>Passaggio 3

```powershell
$subnet = $vnet.subnets[0]
```

Questo passaggio assegna hello subnet oggetto toovariable $subnet per i passaggi successivi hello.

## <a name="create-an-application-gateway-configuration-object"></a>Creare un oggetto di configurazione gateway applicazione

### <a name="step-1"></a>Passaggio 1

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

Questo passaggio crea una configurazione IP del gateway applicazione denominata "gatewayIP01". Avvio di Gateway applicazione preleva un indirizzo IP dalla subnet hello configurato e instradare gli indirizzi IP di toohello il traffico di rete nel pool IP back-end hello. Tenere presente che ogni istanza ha un indirizzo IP.

### <a name="step-2"></a>Passaggio 2

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.1.1.8,10.1.1.9,10.1.1.10
```

Questo passaggio consente di configurare pool indirizzi IP back-end di hello denominato "pool01" con IP indirizzi "10.1.1.8, 10.1.1.9, 10.1.1.10". Questi sono gli indirizzi IP hello che ricevono il traffico di rete hello proveniente dall'endpoint IP front-end hello. Sostituire hello precedente tooadd gli indirizzi IP endpoint dell'indirizzo IP la propria applicazione.

### <a name="step-3"></a>Passaggio 3

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

Questo passaggio consente di configurare applicazioni gateway impostazione "poolsetting01" per il carico hello con bilanciati del traffico di rete nel pool back-end hello.

### <a name="step-4"></a>Passaggio 4

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

Questo passaggio Configura porta IP front-end hello denominata "frontendport01" per hello bilanciamento del carico interno.

### <a name="step-5"></a>Passaggio 5

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

Questo passaggio Crea una configurazione IP front-end hello chiamata "fipconfig01" e lo associa a un indirizzo IP dalla subnet di rete virtuale corrente hello privato.

### <a name="step-6"></a>Passaggio 6

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

Questo passaggio consente di creare listener hello chiamato "listener01" e associa una configurazione IP front-end di hello porta front-end toohello.

### <a name="step-7"></a>Passaggio 7

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

Questo passaggio Crea hello regola bilanciamento del carico routing chiamato "rule01" che configura il comportamento del servizio di bilanciamento carico di hello.

### <a name="step-8"></a>Passaggio 8

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

Questo passaggio consente di configurare dimensioni di istanza hello del gateway applicazione hello.

> [!NOTE]
> il valore predefinito per Hello *InstanceCount* è 2, con un valore massimo di 10. il valore predefinito per Hello *GatewaySize* è Medium. È possibile scegliere tra Standard_Small, Standard_Medium e Standard_Large.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a>Creare un gateway applicazione usando New-AzureApplicationGateway

Crea un gateway applicazione con tutti gli elementi di configurazione da hello passaggi precedenti. In questo esempio, i gateway applicazione hello viene chiamato "appgwtest".

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

Questo passaggio Crea un gateway applicazione con tutti gli elementi di configurazione da hello passaggi precedenti. Nell'esempio hello gateway applicazione hello viene chiamato "appgwtest".

## <a name="delete-an-application-gateway"></a>Eliminare un gateway applicazione

toodelete un gateway applicazione, è necessario hello toodo procedura nell'ordine seguente:

1. Hello utilizzare `Stop-AzureRmApplicationGateway` gateway hello toostop di cmdlet.
2. Hello utilizzare `Remove-AzureRmApplicationGateway` gateway hello tooremove di cmdlet.
3. Verificare che gateway hello è stato rimosso utilizzando hello `Get-AzureApplicationGateway` cmdlet.

### <a name="step-1"></a>Passaggio 1

Ottenere l'oggetto di gateway applicazione hello e associarlo variabile tooa "$getgw".

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a>Passaggio 2

Utilizzare `Stop-AzureRmApplicationGateway` toostop gateway di applicazione hello. In questo esempio viene hello `Stop-AzureRmApplicationGateway` cmdlet hello della prima riga, seguito dall'output di hello.

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

Una volta gateway applicazione hello in stato di interruzione, utilizzare hello `Remove-AzureRmApplicationGateway` servizio hello tooremove di cmdlet.

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> Hello **-force** switch possono essere messaggio di conferma rimozione hello toosuppress utilizzato.

tooverify che hello servizio è stato rimosso, è possibile usare hello `Get-AzureRmApplicationGateway` cmdlet. Questo passaggio non è obbligatorio.

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
```

## <a name="next-steps"></a>Passaggi successivi

Se si desidera tooconfigure offload SSL, vedere [configurare un gateway applicazione per l'offload SSL](application-gateway-ssl.md).

Se si desidera tooconfigure un toouse di gateway applicazione con un bilanciamento del carico interno, vedere [creare un gateway applicazione con un servizio di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).

Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:

* [Servizio di bilanciamento del carico di Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Gestione traffico di Azure](https://azure.microsoft.com/documentation/services/traffic-manager/)

