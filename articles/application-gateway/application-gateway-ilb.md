---
title: Gateway applicazione Azure con bilanciamento del carico interno aaaUsing | Documenti Microsoft
description: Questa pagina fornisce istruzioni tooconfigure un Gateway applicazione Azure con un endpoint con bilanciamento del carico interno
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a>Creare un gateway applicazione con un dispositivo di bilanciamento del carico interno (ILB)

> [!div class="op_single_selector"]
> * [PowerShell per Azure classico](application-gateway-ilb.md)
> * [PowerShell per Azure Resource Manager](application-gateway-ilb-arm.md)

Gateway applicazione può essere configurato con un indirizzo IP virtuale è connessa a internet o con toohello un endpoint interno non è esposta internet, noto anche come endpoint di servizio di bilanciamento di carico interno (ILB). Configurazione di gateway hello con un bilanciamento del carico interno è utile per applicazioni line-of-business interne non esposte toointernet. È inoltre utile per i servizi o livelli all'interno di un'applicazione multilivello, che si trova in un toointernet limite non esposti di sicurezza, ma ancora richiede la distribuzione del carico round robin, aderenza sessione o la terminazione SSL. In questo articolo illustra i passaggi di hello tooconfigure un gateway applicazione con un bilanciamento del carico interno.

## <a name="before-you-begin"></a>Prima di iniziare

1. Installare la versione più recente dei cmdlet di Azure PowerShell hello utilizzando hello installazione guidata piattaforma Web. È possibile scaricare e installare la versione più recente di hello da hello **Windows PowerShell** sezione di hello [pagina di Download](https://azure.microsoft.com/downloads/).
2. Assicurarsi di avere una rete virtuale funzionante con una subnet valida.
3. Verificare di disporre di server back-end nella rete virtuale hello o con un indirizzo IP/VIP pubblico assegnato.

toocreate un gateway di applicazione, eseguire hello seguendo i passaggi nell'ordine di hello elencati. 

1. [Creare un gateway applicazione](#create-a-new-application-gateway)
2. [Configurare il gateway hello](#configure-the-gateway)
3. [Configurazione del gateway hello set](#set-the-gateway-configuration)
4. [Avviare il gateway hello](#start-the-gateway)
5. [Verificare i gateway hello](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Creare un gateway applicazione:

**gateway hello toocreate**, utilizzare hello `New-AzureApplicationGateway` cmdlet, sostituendo i valori hello con valori personalizzati. Si noti che la fatturazione per il gateway hello non viene avviato a questo punto. La fatturazione inizia in un passaggio successivo, quando il gateway hello sia stato avviato correttamente.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

**toovalidate** che gateway hello è stato creato, è possibile usare hello `Get-AzureApplicationGateway` cmdlet. 

Nell'esempio hello *descrizione*, *InstanceCount*, e *GatewaySize* sono parametri facoltativi. il valore predefinito per Hello *InstanceCount* è 2, con un valore massimo di 10. il valore predefinito per Hello *GatewaySize* è Medium. Small e Large sono altri valori disponibili. *VIP* e *DnsName* vengono visualizzati come vuoto perché non è ancora iniziata gateway hello. Vengono creati una volta hello gateway si trova in stato di esecuzione hello. 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-hello-gateway"></a>Configurare il gateway hello
La configurazione di un gateway applicazione è costituita da più valori. possono essere associati i valori Hello configurazione hello tooconstruct insieme.

i valori Hello sono:

* **Pool di server back-end:** elenco hello di indirizzi IP dei server back-end hello. gli indirizzi IP Hello elencati devono appartenere toohello subnet di rete virtuale oppure devono essere un indirizzo IP/VIP pubblico. 
* **Impostazioni del pool di server back-end:** ogni pool ha impostazioni come porta, protocollo e affinità basata sui cookie. Queste impostazioni sono legato tooa pool e vengono applicati tooall server hello pool.
* **Porta front-end:** questa porta è aperta nel gateway applicazione hello la porta pubblica hello. Traffico raggiunge questa porta e quindi ottiene reindirizzato tooone dei server back-end hello.
* **Listener:** listener hello dispone di una porta di front-end, un protocollo (Http o Https, si tratta tra maiuscole e minuscole) e il nome certificato SSL hello (se la configurazione di SSL di offload). 
* **Regola:** regola hello associa listener hello e pool di server back-end hello e definisce il traffico di hello pool di server back-end deve essere diretto toowhen raggiunge un determinato listener. Attualmente, solo hello *base* regola supportata. Hello *base* regola è una distribuzione del carico round robin.

È possibile definire la configurazione creando un oggetto di configurazione oppure usando un file XML di configurazione. tooconstruct la configurazione utilizzando un file XML di configurazione, utilizzare hello di esempio seguente.

Si noti hello segue:

* Hello *Frontendipconfiguration* elemento descrive i dettagli di bilanciamento del carico interno hello rilevanti per la configurazione di Gateway applicazione con un bilanciamento del carico interno. 
* IP di front-end Hello *tipo* deve essere impostato too'Private'
* Hello *StaticIPAddress* deve essere impostato su quale hello gateway riceve il traffico di indirizzo IP interno toohello desiderato. Si noti che hello *StaticIPAddress* elemento è facoltativo. Se non impostato, viene scelto un indirizzo IP interno disponibili dalla subnet hello distribuito. 
* valore di hello Hello *nome* specificato nell'elemento *FrontendIPConfiguration* deve essere utilizzato in HTTPListener hello *FrontendIP* toohello toorefer elemento FrontendIPConfiguration.
  
  **Esempio di file XML di configurazione**
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
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
            <FrontendIP>fip1</FrontendIP>
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


## <a name="set-hello-gateway-configuration"></a>Configurazione del gateway hello set
Successivamente, impostare gateway applicazione hello. È possibile utilizzare hello `Set-AzureApplicationGatewayConfig` cmdlet con un oggetto di configurazione o con un file XML di configurazione. 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-hello-gateway"></a>Avviare il gateway hello

Una volta configurato il gateway di hello, utilizzare hello `Start-AzureApplicationGateway` gateway hello toostart di cmdlet. La fatturazione per un gateway applicazione inizia dopo il gateway hello è stata avviata. 

> [!NOTE]
> Hello `Start-AzureApplicationGateway` cmdlet può richiedere toocomplete too15-20 minuti. 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-hello-gateway-status"></a>Verificare lo stato del gateway hello

Hello utilizzare `Get-AzureApplicationGateway` stato hello toocheck di cmdlet del gateway. Se `Start-AzureApplicationGateway` ha avuto esito positivo nel passaggio precedente hello, deve essere stato hello *esecuzione*, hello Vip e DnsName dovrebbe avere voci valide. In questo esempio viene illustrato il cmdlet hello hello della prima riga, seguito dall'output di hello. In questo esempio, hello gateway è in esecuzione e di traffico tootake pronto. 

> [!NOTE]
> gateway applicazione Hello è configurato il traffico tooaccept hello configurato l'endpoint di bilanciamento del carico interno 10.0.0.10 in questo esempio.

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
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni generali sulle opzioni di bilanciamento del carico, vedere:

* [Servizio di bilanciamento del carico di Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Gestione traffico di Azure](https://azure.microsoft.com/documentation/services/traffic-manager/)

