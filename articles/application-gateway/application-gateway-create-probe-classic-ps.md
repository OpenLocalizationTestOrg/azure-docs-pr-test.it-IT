---
title: un classico PowerShell probe personalizzato - Gateway applicazione Azure - aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate personalizzato probe per il Gateway applicazione usando PowerShell in modello di distribuzione classica hello
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a>Creare un probe personalizzato per il gateway applicazione di Azure (classico) con PowerShell

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-create-probe-portal.md)
> * [PowerShell per Azure Resource Manager](application-gateway-create-probe-ps.md)
> * [PowerShell per Azure classico](application-gateway-create-probe-classic-ps.md)

In questo articolo aggiungere un gateway di applicazione esistente probe personalizzato tooan con PowerShell. Probe personalizzati sono utili per le applicazioni che dispone di una pagina di controllo di integrità specifico o per le applicazioni che non forniscono una risposta corretta in un'applicazione web predefinita hello.

> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Informazioni su come troppo[eseguire questi passaggi tramite il modello di gestione risorse di hello](application-gateway-create-probe-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a>Creare un gateway applicazione

toocreate un gateway applicazione:

1. Creare una risorsa del gateway applicazione.
2. Creare un file XML di configurazione o un oggetto di configurazione.
3. Eseguire il commit toohello configurazione hello appena creati risorsa per il gateway applicazione.

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a>Creare una risorsa del gateway applicazione con un probe personalizzato

gateway hello toocreate, utilizzare hello `New-AzureApplicationGateway` cmdlet, sostituendo i valori hello con valori personalizzati. La fatturazione per il gateway hello non inizia a questo punto. La fatturazione inizia in un passaggio successivo, quando il gateway hello sia stato avviato correttamente.

Hello seguente viene creato un gateway applicazione tramite una rete virtuale denominata "testvnet1" e una subnet denominata "subnet-1".

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

toovalidate che hello gateway è stato creato, è possibile usare hello `Get-AzureApplicationGateway` cmdlet.

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> il valore predefinito per Hello *InstanceCount* è 2, con un valore massimo di 10. il valore predefinito per Hello *GatewaySize* è Medium. È possibile scegliere tra Small, Medium e Large.
> 
> 

*Gli IP virtuali* e *DnsName* vengono visualizzati come vuoto perché non è ancora iniziata gateway hello. Questi valori vengono creati una volta hello gateway si trova in stato di esecuzione hello.

### <a name="configure-an-application-gateway-by-using-xml"></a>Configurare un gateway applicazione usando XML

Nell'esempio seguente di hello, un tooconfigure file XML tutte le impostazioni di gateway applicazione e di eseguirne il commit toohello risorsa per il gateway applicazione.  

Copiare hello tooNotepad testo seguente.

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

Modificare i valori hello tra parentesi hello hello degli elementi di configurazione. Salvare hello file con estensione XML.

Hello seguente viene illustrato come un tooset di file di configurazione di tooload di gateway applicazione hello toouse bilanciare il traffico HTTP sulla porta pubblica 80 e inviare il traffico di rete porta tooback fine 80 tra due indirizzi IP utilizzando un probe personalizzato.

> [!IMPORTANT]
> Hello protocollo Http o Https è tra maiuscole e minuscole.

Un nuovo elemento di configurazione \<Probe\> viene aggiunto probe personalizzato tooconfigure.

parametri di configurazione di Hello sono:

|.|Descrizione|
|---|---|
|**Nome** |Nome di riferimento del probe personalizzato. |
* **Protocol** | Protocollo usato. I valori possibili sono HTTP o HTTPS.|
| **Host** e **Path** | Percorso URL completo che viene richiamato dall'integrità hello applicazione gateway toodetermine hello dell'istanza di hello. Ad esempio, se si dispone di http://contoso.com/ un sito Web, quindi probe personalizzato hello può essere configurate per "http://contoso.com/path/custompath.htm" per il probe controlla toohave una risposta HTTP ha esito positivo.|
| **Interval** | Consente di configurare i controlli di intervallo di probe hello in secondi.|
| **Timeout** | Definisce il periodo di timeout di hello probe per un controllo della risposta HTTP.|
| **UnhealthyThreshold** | Hello numero di risposte HTTP non riuscite necessari tooflag hello back-end dell'istanza come *integro*.|

nome di probe Hello viene fatto riferimento in hello \<BackendHttpSettings\> tooassign configurazione quale pool back-end Usa le impostazioni di tipo probe personalizzato.

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a>Aggiungere un gateway di applicazione esistente tooan probe personalizzato

La modifica della configurazione corrente hello di un gateway applicazione sono necessari tre passaggi: ottenere i file di configurazione XML corrente hello, modificare toohave un probe personalizzato e configurare gateway applicazione hello con le nuove impostazioni XML hello.

1. Ottenere i file XML di hello utilizzando `Get-AzureApplicationGatewayConfig`. Questo toobe XML di configurazione di cmdlet esportazioni hello modificato tooadd un'impostazione probe.

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. Aprire il file XML di hello in un editor di testo. Aggiungere una sezione `<probe>` dopo `<frontendport>`.

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  Nella sezione di backendHttpSettings hello di hello XML, aggiungere il nome di probe hello come illustrato nell'esempio seguente hello:

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  Salvare il file XML di hello.

1. Configurazione di gateway applicazione hello aggiornamento con nuovo file XML hello utilizzando `Set-AzureApplicationGatewayConfig`. Questo cmdlet aggiorna il gateway applicazione con una nuova configurazione hello.

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a>Passaggi successivi

Se si desidera tooconfigure offload Secure Sockets Layer (SSL), vedere [configurare un gateway applicazione per l'offload SSL](application-gateway-ssl.md).

Se si desidera tooconfigure un toouse di gateway applicazione con un servizio di bilanciamento del carico interno, vedere [creare un gateway applicazione con un servizio di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).

