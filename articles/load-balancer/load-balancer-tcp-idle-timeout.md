---
title: "timeout di inattività TCP del servizio di bilanciamento carico di aaaConfigure | Documenti Microsoft"
description: "Configurazione del timeout di inattività TCP di Load Balancer"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 4625c6a8-5725-47ce-81db-4fa3bd055891
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2bf0704b891f708e0a5bd7aa827441930f51cfaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a>Configurazione del timeout di inattività TCP di Azure Load Balancer

La configurazione predefinita di Azure Load Balancer prevede che il timeout di inattività sia impostato su 4 minuti. Se un periodo di inattività supera il valore di timeout di hello, non c'è garanzia che hello TCP o HTTP sessione viene mantenuta tra client hello e il servizio cloud.

Chiusura della connessione hello, l'applicazione client può ricevere hello seguente messaggio di errore: "hello connessione sottostante chiusa: una connessione che doveva toobe mantenuta attiva è stata chiusa dal server hello."

Una pratica comune è toouse un keep-alive TCP. Questa procedura mantiene connessione hello attivo per un periodo più lungo. Per altre informazioni, vedere questi [esempi .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx). Keep-alive abilitata, i pacchetti vengono inviati durante i periodi di inattività della connessione hello. Questi pacchetti keep-alive assicurarsi che il valore di timeout di inattività hello non viene mai raggiunto e connessione hello viene mantenuta per un lungo periodo.

Questa impostazione funziona solo per le connessioni in entrata. tooavoid perdita della connessione hello, è necessario configurare hello keep-alive TCP con un intervallo minore di hello timeout di inattività impostazione o aumentare hello valore timeout di inattività. toosupport tali scenari, è stato aggiunto il supporto per un timeout di inattività. È ora possibile impostare per una durata pari a 4 minuti too30.

La connessione TCP keep-alive è particolarmente adatta per gli scenari non vincolati alla durata della batteria, mentre non è consigliabile per le applicazioni mobili. Con un TCP keep-alive in un'applicazione per dispositivi mobili possono svuotare batteria dispositivo hello più velocemente.

![Timeout TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

Hello le sezioni seguenti descrivono come toochange nelle macchine virtuali, le impostazioni di timeout di inattività e i servizi cloud.

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a>Configurare timeout TCP hello per i minuti di too15 IP pubblici a livello di istanza

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

`IdleTimeoutInMinutes` è facoltativo. Se non è impostata, il timeout predefinito hello è 4 minuti. intervallo di timeout accettabile Hello è 4 too30 minuti.

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a>Impostare i timeout di inattività hello durante la creazione di un endpoint di Azure in una macchina virtuale

toochange hello timeout impostazione per un endpoint, utilizzare hello seguente:

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

tooretrieve la configurazione di timeout di inattività, utilizzare hello comando seguente:

    PS C:\> Get-AzureVM -ServiceName "MyService" -Name "MyVM" | Get-AzureEndpoint
    VERBOSE: 6:43:50 PM - Completed Operation: Get Deployment
    LBSetName : MyLoadBalancedSet
    LocalPort : 80
    Name : HTTP
    Port : 80
    Protocol : tcp
    Vip : 65.52.xxx.xxx
    ProbePath :
    ProbePort : 80
    ProbeProtocol : tcp
    ProbeIntervalInSeconds : 15
    ProbeTimeoutInSeconds : 31
    EnableDirectServerReturn : False
    Acl : {}
    InternalLoadBalancerName :
    IdleTimeoutInMinutes : 15

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a>Impostare i timeout TCP hello in un set di endpoint con bilanciamento del carico

Se gli endpoint sono parte di un set di endpoint con bilanciamento del carico, è necessario impostare timeout TCP hello in set di endpoint con carico bilanciato hello. ad esempio:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a>Modifica delle impostazioni di timeout per i servizi cloud

È possibile utilizzare hello Azure SDK tooupdate il servizio cloud. File con estensione csdef hello è effettuare le impostazioni di endpoint per i servizi cloud. L'aggiornamento di hello timeout TCP per la distribuzione di un servizio cloud richiede un aggiornamento della distribuzione. Un'eccezione è se hello TCP timeout viene specificato solo per un indirizzo IP pubblico. Impostazioni dell'IP pubbliche sono nel file con estensione cscfg hello e aggiornarle tramite l'aggiornamento e aggiornamento della distribuzione.

modifiche di csdef Hello per le impostazioni di endpoint sono:

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

le modifiche apportate al file con estensione cscfg Hello per l'impostazione di timeout hello su indirizzi IP pubblici sono:

```xml
<NetworkConfiguration>
    <VirtualNetworkSite name="VNet"/>
    <AddressAssignments>
    <InstanceAddress roleName="VMRolePersisted">
    <PublicIPs>
        <PublicIP name="public-ip-name" idleTimeoutInMinutes="timeout-in-minutes"/>
    </PublicIPs>
    </InstanceAddress>
    </AddressAssignments>
</NetworkConfiguration>
```

## <a name="rest-api-example"></a>Esempio di API REST

È possibile configurare i timeout di inattività TCP hello mediante API di Gestione servizio hello. Verificare che tale hello `x-ms-version` intestazione è impostata tooversion `2014-06-01` o versione successiva. Aggiorna configurazione hello di hello specifica gli endpoint di input con bilanciamento del carico in tutte le macchine virtuali in una distribuzione.

### <a name="request"></a>Richiesta

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a>Response

```xml
<LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <InputEndpoint>
    <LoadBalancedEndpointSetName>endpoint-set-name</LoadBalancedEndpointSetName>
    <LocalPort>local-port-number</LocalPort>
    <Port>external-port-number</Port>
    <LoadBalancerProbe>
        <Path>path-of-probe</Path>
        <Port>port-assigned-to-probe</Port>
        <Protocol>probe-protocol</Protocol>
        <IntervalInSeconds>interval-of-probe</IntervalInSeconds>
        <TimeoutInSeconds>timeout-for-probe</TimeoutInSeconds>
    </LoadBalancerProbe>
    <LoadBalancerName>name-of-internal-loadbalancer</LoadBalancerName>
    <Protocol>endpoint-protocol</Protocol>
    <IdleTimeoutInMinutes>15</IdleTimeoutInMinutes>
    <EnableDirectServerReturn>enable-direct-server-return</EnableDirectServerReturn>
    <EndpointACL>
        <Rules>
        <Rule>
            <Order>priority-of-the-rule</Order>
            <Action>permit-rule</Action>
            <RemoteSubnet>subnet-of-the-rule</RemoteSubnet>
            <Description>description-of-the-rule</Description>
        </Rule>
        </Rules>
    </EndpointACL>
    </InputEndpoint>
</LoadBalancedEndpointList>
```

## <a name="next-steps"></a>Passaggi successivi

[Panoramica del bilanciamento del carico interno](load-balancer-internal-overview.md)

[Introduzione alla configurazione del bilanciamento del carico Internet](load-balancer-get-started-internet-arm-ps.md)

[Configurare una modalità di distribuzione del servizio di bilanciamento del carico](load-balancer-distribution-mode.md)
