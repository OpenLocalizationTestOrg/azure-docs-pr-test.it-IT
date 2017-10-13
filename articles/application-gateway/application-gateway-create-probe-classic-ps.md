---
title: Creare un probe personalizzato - Gateway applicazione di Azure - PowerShell versione classica | Microsoft Docs
description: Informazioni su come creare un probe personalizzato per il gateway applicazione usando PowerShell nel modello di distribuzione classica
services: application-gateway
documentationcenter: na
author: davidmu1
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
ms.author: davidmu
ms.openlocfilehash: b167a0584740a4e583a35bd6d44ec5d616ba04f7
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a>Creare un probe personalizzato per il gateway applicazione di Azure (classico) con PowerShell

> [!div class="op_single_selector"]
> * [Portale di Azure](application-gateway-create-probe-portal.md)
> * [PowerShell per Azure Resource Manager](application-gateway-create-probe-ps.md)
> * [PowerShell per Azure classico](application-gateway-create-probe-classic-ps.md)

Questo articolo illustra come aggiungere un probe personalizzato a un gateway applicazione esistente con PowerShell. I probe personalizzati sono utili per le applicazioni che dispongono di una pagina di controllo dell'integrità specifica o per quelle che non rispondono in modo corretto all'applicazione Web predefinita.

> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). Questo articolo illustra l'uso del modello di distribuzione classica. Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti. Informazioni su come [eseguire questa procedura con il modello di Resource Manager](application-gateway-create-probe-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a>Creare un gateway applicazione

Per creare un gateway applicazione:

1. Creare una risorsa del gateway applicazione.
2. Creare un file XML di configurazione o un oggetto di configurazione.
3. Eseguire il commit della configurazione nella risorsa del gateway applicazione appena creata.

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a>Creare una risorsa del gateway applicazione con un probe personalizzato

Per creare il gateway, usare il cmdlet `New-AzureApplicationGateway`, sostituendo i valori esistenti con quelli personalizzati. La fatturazione per il gateway non viene applicata a partire da questo punto. La fatturazione viene applicata a partire da un passaggio successivo, dopo l'avvio corretto del gateway.

L'esempio seguente mostra come creare un gateway applicazione usando una rete virtuale denominata "testvnet1" e una subnet denominata "subnet-1".

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

Per convalidare la creazione del gateway, è possibile usare il cmdlet `Get-AzureApplicationGateway`.

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> Il valore predefinito per *InstanceCount* è 2, con un valore massimo di 10. Il valore predefinito per *GatewaySize* è Medium. È possibile scegliere tra Small, Medium e Large.
> 
> 

*VirtualIPs* e *DnsName* vengono visualizzati vuoti perché il gateway non è stato ancora avviato. Questi valori vengono creati quando il gateway è in esecuzione.

### <a name="configure-an-application-gateway-by-using-xml"></a>Configurare un gateway applicazione usando XML

Nell'esempio seguente viene usato un file XML per configurare tutte le impostazioni del gateway applicazione ed eseguirne il commit nella risorsa del gateway applicazione.  

Copiare il testo seguente in Blocco note.

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

Modificare i valori tra parentesi per gli elementi di configurazione. Salvare il file con estensione XML.

L'esempio seguente mostra come usare un file di configurazione per impostare il gateway applicazione per il bilanciamento del carico del traffico HTTP sulla porta pubblica 80 e inviare il traffico di rete alla porta back-end 80 tra due indirizzi IP usando un probe personalizzato.

> [!IMPORTANT]
> L'elemento del protocollo HTTP o HTTPS deve rispettare la distinzione tra maiuscole e minuscole.

Viene aggiunto un nuovo elemento di configurazione \<Probe\> per configurare i probe personalizzati.

I parametri di configurazione sono:

|Parametro|Descrizione|
|---|---|
|**Nome** |Nome di riferimento del probe personalizzato. |
* **Protocol** | Protocollo usato. I valori possibili sono HTTP o HTTPS.|
| **Host** e **Path** | Percorso URL completo richiamato dal gateway applicazione per determinare l'integrità dell'istanza. Se si ha un sito Web http://contoso.com/, ad esempio, il probe personalizzato può essere configurato per "http://contoso.com/path/custompath.htm" in modo che i controlli del probe ottengano una risposta HTTP corretta.|
| **Interval** | Configura i controlli dell'intervallo di probe, in secondi.|
| **Timeout** | Definisce il timeout del probe per un controllo della risposta HTTP.|
| **UnhealthyThreshold** | Numero di risposte HTTP non riuscite necessario per contrassegnare l'istanza back-end come *non integra*.|

Nella configurazione \<BackendHttpSettings\> viene fatto riferimento al nome del probe per assegnare il pool back-end che userà le impostazioni del probe personalizzato.

## <a name="add-a-custom-probe-to-an-existing-application-gateway"></a>Aggiungere un probe personalizzato a un gateway applicazione esistente

Per modificare la configurazione corrente di un gateway applicazione sono necessari tre passaggi: ottenere il file di configurazione XML corrente, apportare modifiche per avere un probe personalizzato e configurare il gateway applicazione con le nuove impostazioni XML.

1. Ottenere il file XML usando `Get-AzureApplicationGatewayConfig`. Questo cmdlet esporta il file XML di configurazione, che potrà quindi essere modificato per aggiungere un'impostazione di probe.

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path to file>"
  ```

1. Aprire il file XML in un editor di testo. Aggiungere una sezione `<probe>` dopo `<frontendport>`.

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

  Nella sezione backendHttpSettings del file XML aggiungere il nome del probe, come nell'esempio seguente:

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

  Salvare il file XML.

1. Aggiornare la configurazione del gateway applicazione con il nuovo file XML usando `Set-AzureApplicationGatewayConfig`. Questo cmdlet aggiorna il gateway applicazione con la nuova configurazione.

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path to file>"
```

## <a name="next-steps"></a>Passaggi successivi

Per configurare l'offload SSL (Secure Sockets Layer), vedere [Configurare un gateway applicazione per l'offload SSL](application-gateway-ssl.md).

Per configurare un gateway applicazione da usare con un servizio di bilanciamento del carico interno, vedere [Creare un gateway applicazione con un servizio di bilanciamento del carico interno (ILB)](application-gateway-ilb.md).

