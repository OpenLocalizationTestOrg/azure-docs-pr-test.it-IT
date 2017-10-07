---
title: aaaConfigure SSL offload classica - Gateway applicazione Azure - PowerShell | Documenti Microsoft
description: In questo articolo vengono fornite istruzioni toocreate eseguire l'offload usando un gateway applicazione con SSL hello modello di distribuzione classico di Azure.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a>Configurare un gateway applicazione per l'offload SSL utilizzando il modello di distribuzione classica hello

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-ssl-portal.md)
> * [PowerShell per Azure Resource Manager](application-gateway-ssl-arm.md)
> * [PowerShell per Azure classico](application-gateway-ssl.md)
> * [Interfaccia della riga di comando di Azure 2.0](application-gateway-ssl-cli.md)

Gateway applicazione Azure può essere configurato tooterminate hello Secure Sockets Layer (SSL) sessione hello gateway tooavoid costosi SSL decrittografia attività toohappen alla farm web hello. Offload SSL semplifica anche l'installazione di server front-end di hello e gestione di un'applicazione web hello.

## <a name="before-you-begin"></a>Prima di iniziare

1. Installare più recente dei cmdlet di Azure PowerShell hello hello utilizzando hello installazione guidata piattaforma Web. È possibile scaricare e installare la versione più recente di hello da hello **Windows PowerShell** sezione di hello [pagina di download](https://azure.microsoft.com/downloads/).
2. Assicurarsi di avere una rete virtuale funzionante con una subnet valida. Assicurarsi che nessun macchine virtuali o le distribuzioni di cloud utilizza subnet hello. gateway applicazione Hello deve essere da solo in una subnet di rete virtuale.
3. deve esistere server Hello configurare gateway di applicazione hello toouse o disporre i relativi endpoint creato nella rete virtuale hello o con un indirizzo IP/VIP pubblico.

tooconfigure SSL offload su un gateway applicazione, hello in ordine di hello elencati come segue:

1. [Creare un gateway applicazione](#create-an-application-gateway)
2. [Caricare i certificati SSL](#upload-ssl-certificates)
3. [Configurare il gateway hello](#configure-the-gateway)
4. [Configurazione del gateway hello set](#set-the-gateway-configuration)
5. [Avviare il gateway hello](#start-the-gateway)
6. [Verificare lo stato del gateway hello](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Creare un gateway applicazione

gateway hello toocreate, utilizzare hello `New-AzureApplicationGateway` cmdlet, sostituendo i valori hello con valori personalizzati. La fatturazione per il gateway hello non inizia a questo punto. La fatturazione inizia in un passaggio successivo, quando il gateway hello sia stato avviato correttamente.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

toovalidate che hello gateway è stato creato, è possibile usare hello `Get-AzureApplicationGateway` cmdlet.

Nell'esempio hello *descrizione*, *InstanceCount*, e *GatewaySize* sono parametri facoltativi. il valore predefinito per Hello *InstanceCount* è 2, con un valore massimo di 10. il valore predefinito per Hello *GatewaySize* è Medium. Small e Large sono altri valori disponibili. *Gli IP virtuali* e *DnsName* vengono visualizzati come vuoto perché non è ancora iniziata gateway hello. Questi valori vengono creati una volta hello gateway si trova in stato di esecuzione hello.

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a>Caricare i certificati SSL

Utilizzare `Add-AzureApplicationGatewaySslCertificate` tooupload hello certificato del server *pfx* gateway applicazione toohello di formato. nome del certificato Hello è un nome scelti dall'utente e deve essere univoco all'interno di gateway applicazione hello. Questo certificato è tooby di cui si fa riferimento questo nome in tutte le operazioni di gestione di certificati su gateway applicazione hello.

L'esempio seguente mostra i cmdlet di hello, sostituire i valori di hello nell'esempio hello con valori personalizzati.

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

Successivamente, convalidare il caricamento di certificati hello. Hello utilizzare `Get-AzureApplicationGatewayCertificate` cmdlet.

In questo esempio viene illustrato il cmdlet hello hello della prima riga, seguito dall'output di hello.

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> password del certificato Hello è toobe tra 4 too12 caratteri, lettere o numeri. Non sono ammessi caratteri speciali.

## <a name="configure-hello-gateway"></a>Configurare il gateway hello

La configurazione di un gateway applicazione è costituita da più valori. possono essere associati i valori Hello configurazione hello tooconstruct insieme.

i valori Hello sono:

* **Pool di server back-end:** elenco hello di indirizzi IP dei server back-end hello. gli indirizzi IP Hello elencati devono appartenere toohello subnet della rete virtuale o devono essere un indirizzo IP/VIP pubblico.
* **Impostazioni del pool di server back-end:** ogni pool ha impostazioni quali porta, protocollo e affinità basata sui cookie. Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.
* **Porta front-end:** questa porta è una porta pubblica hello aperta sul gateway applicazione hello. Traffico riscontri questa porta, e quindi ottiene reindirizzato tooone dei server back-end hello.
* **Listener:** listener hello dispone di una porta front-end, un protocollo (Http o Https, questi valori sono distinzione maiuscole/minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload).
* **Regola:** regola hello associa listener hello e pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener. Attualmente, solo hello *base* regola supportata. Hello *base* regola è una distribuzione del carico round robin.

**Note aggiuntive sulla configurazione**

Per la configurazione di certificati SSL, hello protocollo **HttpListener** deve modificare troppo*Https* (maiuscole / minuscole). Hello **SslCert** elemento viene aggiunto troppo**HttpListener** con hello impostato toohello stesso nome utilizzato per il caricamento di hello della precedente sezione relativa ai certificati SSL. porta front-end di Hello deve essere aggiornato too443.

**affinità basato su cookie tooenable**: un gateway applicazione può essere configurato tooensure che una richiesta da una sessione client è sempre toohello diretto stessa macchina virtuale nella farm web hello. Questo scenario viene eseguito dall'inserimento di un cookie di sessione che consenta il traffico di toodirect di hello gateway in modo appropriato. impostata l'affinità basato su cookie tooenable, **CookieBasedAffinity** troppo*abilitato* in hello **BackendHttpSettings** elemento.

È possibile definire la configurazione creando un oggetto di configurazione oppure usando un file XML di configurazione.
Utilizzare la configurazione utilizzando una file XML di configurazione tooconstruct hello seguente esempio:

**Esempio di file XML di configurazione**

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

## <a name="set-hello-gateway-configuration"></a>Configurazione del gateway hello set

È quindi possibile impostare gateway applicazione hello. È possibile utilizzare hello `Set-AzureApplicationGatewayConfig` cmdlet con un oggetto di configurazione o con un file XML di configurazione.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a>Avviare il gateway hello

Una volta configurato il gateway di hello, utilizzare hello `Start-AzureApplicationGateway` gateway hello toostart di cmdlet. La fatturazione per un gateway applicazione inizia dopo il gateway hello è stata avviata.

> [!NOTE]
> Hello `Start-AzureApplicationGateway` cmdlet può richiedere toofinish too15-20 minuti.
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Verificare lo stato del gateway hello

Hello utilizzare `Get-AzureApplicationGateway` cmdlet toocheck hello stato gateway hello. Se `Start-AzureApplicationGateway` ha avuto esito positivo nel passaggio precedente hello *stato* deve essere in esecuzione, e *gli IP virtuali* e *DnsName* dovrebbero avere voci valide.

Questo esempio viene illustrato un gateway di applicazione, in esecuzione, ed è pronto tootake traffico.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:

* [Servizio di bilanciamento del carico di Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Gestione traffico di Azure](https://azure.microsoft.com/documentation/services/traffic-manager/)

