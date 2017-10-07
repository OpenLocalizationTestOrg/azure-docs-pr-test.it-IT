---
title: aaaCreate, avviare o eliminare un gateway applicazione | Documenti Microsoft
description: Questa pagina vengono fornite istruzioni toocreate, configurare, avviare ed eliminare un gateway applicazione Azure
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a>Creare, avviare o eliminare un gateway applicazione con PowerShell 

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-create-gateway-portal.md)
> * [PowerShell per Azure Resource Manager](application-gateway-create-gateway-arm.md)
> * [PowerShell per Azure classico](application-gateway-create-gateway.md)
> * [Modello di Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [Interfaccia della riga di comando di Azure](application-gateway-create-gateway-cli.md)

Il gateway applicazione di Azure è un dispositivo di bilanciamento del carico di livello 7. Fornisce il failover, le prestazioni di routing di richieste HTTP tra server diversi, che si trovino in locale o cloud hello. Il gateway applicazione offre numerose funzionalità di controller per la distribuzione di applicazioni (ADC, Application Delivery Controller), tra cui bilanciamento del carico HTTP, affinità di sessione basata su cookie, offload SSL (Secure Sockets Layer), probe di integrità personalizzati, supporto per più siti e molte altre. toofind un elenco completo delle funzionalità supportate, visitare [Panoramica di Gateway applicazione](application-gateway-introduction.md)

Questo articolo vengono illustrati toocreate passaggi hello, configurare, avviare ed eliminare un gateway applicazione.

## <a name="before-you-begin"></a>Prima di iniziare

1. Installare più recente dei cmdlet di Azure PowerShell hello hello utilizzando hello installazione guidata piattaforma Web. È possibile scaricare e installare la versione più recente di hello da hello **Windows PowerShell** sezione di hello [pagina di download](https://azure.microsoft.com/downloads/).
2. Se si dispone di una rete virtuale esistente, selezionare una subnet vuota esistente o creare una nuova subnet nella rete virtuale esistente esclusivamente per l'utilizzo dal gateway applicazione hello. Non è possibile distribuire hello applicazione gateway tooa rete virtuale diverso rispetto alle risorse di hello intendi toodeploy dietro gateway applicazione hello a meno che non peering reti virtuali viene utilizzato. visitare più toolearn [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md)
3. Assicurarsi di avere una rete virtuale funzionante con una subnet valida. Assicurarsi che nessun macchine virtuali o le distribuzioni di cloud utilizza subnet hello. gateway applicazione Hello deve essere da solo in una subnet di rete virtuale.
4. deve esistere server Hello configurare gateway di applicazione hello toouse o disporre i relativi endpoint creato nella rete virtuale hello o con un indirizzo IP/VIP pubblico.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Che cos'è toocreate necessario un gateway applicazione?

Quando si utilizza hello `New-AzureApplicationGateway` gateway di applicazione hello toocreate comando, non è impostata una configurazione a questo punto e risorse hello appena creato sono configurati utilizzando XML o un oggetto di configurazione.

i valori Hello sono:

* **Pool di server back-end:** elenco hello di indirizzi IP dei server back-end hello. gli indirizzi IP Hello elencati devono appartenere toohello subnet della rete virtuale o devono essere un indirizzo IP/VIP pubblico.
* **Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie. Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.
* **Porta front-end:** questa porta è una porta pubblica hello aperta sul gateway applicazione hello. Traffico riscontri questa porta, e quindi ottiene reindirizzato tooone dei server back-end hello.
* **Listener:** listener hello dispone di una porta front-end, un protocollo (Http o Https, questi valori sono distinzione maiuscole/minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload).
* **Regola:** regola hello associa listener hello e pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener.

## <a name="create-an-application-gateway"></a>Creare un gateway applicazione

toocreate un gateway applicazione:

1. Creare una risorsa del gateway applicazione.
2. Creare un file XML di configurazione o un oggetto di configurazione.
3. Eseguire il commit toohello configurazione hello appena creati risorsa per il gateway applicazione.

> [!NOTE]
> Se è necessario tooconfigure un probe personalizzato per il gateway applicazione, vedere [creare un gateway applicazione con probe personalizzati usando PowerShell](application-gateway-create-probe-classic-ps.md). Per altre informazioni, vedere l'articolo relativo a [probe personalizzati e monitoraggio dell'integrità](application-gateway-probe-overview.md) .

![Esempio dello scenario][scenario]

### <a name="create-an-application-gateway-resource"></a>Creare una risorsa del gateway applicazione

gateway hello toocreate, utilizzare hello `New-AzureApplicationGateway` cmdlet, sostituendo i valori hello con valori personalizzati. La fatturazione per il gateway hello non inizia a questo punto. La fatturazione inizia in un passaggio successivo, quando il gateway hello sia stato avviato correttamente.

Hello esempio seguente viene creato un gateway applicazione tramite una rete virtuale denominata "testvnet1" e una subnet denominata "subnet-1":

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

*Description*, *InstanceCount* e *GatewaySize* sono parametri facoltativi.

toovalidate che hello gateway è stato creato, è possibile usare hello `Get-AzureApplicationGateway` cmdlet.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> il valore predefinito per Hello *InstanceCount* è 2, con un valore massimo di 10. il valore predefinito per Hello *GatewaySize* è Medium. È possibile scegliere tra Small, Medium e Large.

*Gli IP virtuali* e *DnsName* vengono visualizzati come vuoto perché non è ancora iniziata gateway hello. Vengono creati una volta hello gateway si trova in stato di esecuzione hello.

## <a name="configure-hello-application-gateway"></a>Configurare gateway applicazione hello

È possibile configurare gateway applicazione hello utilizzando XML o un oggetto di configurazione.

### <a name="configure-hello-application-gateway-by-using-xml"></a>Configurazione di gateway applicazione hello tramite XML

Nell'esempio seguente di hello, un tooconfigure file XML tutte le impostazioni di gateway applicazione e di eseguirne il commit toohello risorsa per il gateway applicazione.  

#### <a name="step-1"></a>Passaggio 1

Copiare hello tooNotepad testo seguente.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

Modificare i valori hello tra parentesi hello hello degli elementi di configurazione. Salvare hello file con estensione XML.

> [!IMPORTANT]
> Hello protocollo Http o Https è tra maiuscole e minuscole.

Hello di esempio seguente viene illustrato come una configurazione toouse file tooset di gateway applicazione hello. il caricamento di esempio Hello bilancia il traffico HTTP sulla porta pubblica 80 e invia il traffico di rete porta tooback fine 80 tra due indirizzi IP.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

#### <a name="step-2"></a>Passaggio 2

Quindi, impostare gateway applicazione hello. Hello utilizzare `Set-AzureApplicationGatewayConfig` cmdlet con un file XML di configurazione.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a>Configurazione di gateway applicazione hello utilizzando un oggetto di configurazione

Hello di esempio seguente viene illustrato come tooconfigure hello gateway applicazione tramite gli oggetti di configurazione. Tutti gli elementi di configurazione devono essere configurati singolarmente e quindi aggiunta oggetto di configurazione di gateway applicazione tooan. Dopo aver creato l'oggetto di configurazione di hello, utilizzare hello `Set-AzureApplicationGateway` comando toocommit hello configurazione toohello creato in precedenza di risorsa per il gateway applicazione.

> [!NOTE]
> Prima di assegnare un oggetto di configurazione tooeach valore, è necessario toodeclare il tipo di oggetto PowerShell utilizza per l'archiviazione. Hello prima toocreate hello singole voci definisce le azioni `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` vengono utilizzati.

#### <a name="step-1"></a>Passaggio 1

Creare tutti i singoli elementi di configurazione.

Creare l'indirizzo IP front-end hello come illustrato nell'esempio seguente hello.

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

Creare la porta front-end di hello come illustrato nell'esempio seguente hello.

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

Creare il pool di server back-end hello.

Definire gli indirizzi IP hello aggiunti toohello pool di server back-end come mostrato nell'esempio riportato di seguito hello.

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

Utilizzare hello $server tooadd hello valori toohello pool back-end dell'oggetto ($pool).

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

Creare l'impostazione del pool di server back-end hello.

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

Creare listener hello.

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

Creare una regola di hello.

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a>Passaggio 2

Assegnare tutti i singoli elementi tooan applicazione gateway configurazione oggetto di configurazione ($appgwconfig).

Aggiungere la configurazione front-end IP toohello hello.

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

Aggiunta una configurazione toohello hello porta front-end.

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
Aggiungi configurazione toohello del pool di server back-end hello.

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

Aggiungere toohello di configurazione di hello pool back-end.

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

Aggiungere una configurazione di toohello hello del listener.

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

Aggiungere hello regola toohello configurazione.

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a>Passaggio 3
Eseguire il commit utilizzando risorse di gateway applicazione hello configurazione oggetto toohello `Set-AzureApplicationGatewayConfig`.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a>Avviare il gateway hello

Una volta configurato il gateway di hello, utilizzare hello `Start-AzureApplicationGateway` gateway hello toostart di cmdlet. La fatturazione per un gateway applicazione inizia dopo il gateway hello è stata avviata.

> [!NOTE]
> Hello `Start-AzureApplicationGateway` cmdlet può richiedere toofinish too15-20 minuti.

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Verificare lo stato del gateway hello

Hello utilizzare `Get-AzureApplicationGateway` cmdlet toocheck hello stato gateway hello. Se `Start-AzureApplicationGateway` ha avuto esito positivo nel passaggio precedente hello *stato* deve essere in esecuzione, e *Vip* e *DnsName* dovrebbero avere voci valide.

Hello esempio seguente viene illustrato un gateway di applicazione che è in esecuzione e pronto tootake il traffico destinato `http://<generated-dns-name>.cloudapp.net`.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-hello-application-gateway"></a>Eliminare il gateway applicazione hello

gateway applicazione hello di toodelete:

1. Hello utilizzare `Stop-AzureApplicationGateway` gateway hello toostop di cmdlet.
2. Hello utilizzare `Remove-AzureApplicationGateway` gateway hello tooremove di cmdlet.
3. Verificare che gateway hello è stato rimosso utilizzando hello `Get-AzureApplicationGateway` cmdlet.

Hello riportato di seguito hello `Stop-AzureApplicationGateway` cmdlet hello della prima riga, seguito dall'output di hello.

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

Una volta gateway applicazione hello in stato di interruzione, utilizzare hello `Remove-AzureApplicationGateway` servizio hello tooremove di cmdlet.

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

tooverify che hello servizio è stato rimosso, è possibile usare hello `Get-AzureApplicationGateway` cmdlet. Questo passaggio non è obbligatorio.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a>Passaggi successivi

Se si desidera tooconfigure offload SSL, vedere [configurare un gateway applicazione per l'offload SSL](application-gateway-ssl.md).

Se si desidera tooconfigure un toouse di gateway applicazione con un servizio di bilanciamento del carico interno, vedere [creare un gateway applicazione con un servizio di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).

Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:

* [Servizio di bilanciamento del carico di Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Gestione traffico di Azure](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
