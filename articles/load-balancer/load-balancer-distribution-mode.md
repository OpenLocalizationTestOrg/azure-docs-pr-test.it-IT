---
title: "modalità di distribuzione del bilanciamento del carico aaaConfigure | Documenti Microsoft"
description: "Le modalità di caricamento di affinità dell'indirizzo IP di origine toosupport di bilanciamento del carico distribuzione modalità tooconfigure Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 7df27a4d-67a8-47d6-b73e-32c0c6206e6e
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: e745240b733ffc07928d8ed0ae097785ad4f412e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-distribution-mode-for-load-balancer"></a>Configurare la modalità di distribuzione hello di bilanciamento del carico

## <a name="hash-based-distribution-mode"></a>Modalità di distribuzione basata su hash

algoritmo di distribuzione predefinito di Hello è una tupla con 5 (origine IP, porta di origine, IP di destinazione, la porta di destinazione, tipo di protocollo) Server tooavailable di traffico toomap hash. La persistenza viene mantenuta solo all'interno di una sessione di trasporto. I pacchetti hello stessa sessione saranno indirizzate toohello istanza stesso Data Center IP (DIP) dietro l'endpoint con carico bilanciato hello. Quando hello client avvia una nuova sessione da hello stesso indirizzo IP di origine, la porta di origine hello viene modificata e provoca hello traffico toogo tooa DIP endpoint diversi.

![bilanciamento del carico basato su hash](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

Figura 1. Distribuzione a 5 tuple

## <a name="source-ip-affinity-mode"></a>Modalità di affinità IP di origine

Esiste un'altra modalità di distribuzione definita affinità IP di origine (anche nota come affinità di sessione o affinità del client IP). Bilanciamento del carico di Azure può essere configurato toouse una tupla con 2 (indirizzo IP di origine, IP di destinazione) o server disponibili toohello il traffico toomap tupla con 3 elementi (indirizzo IP di origine, IP di destinazione, Protocol). Utilizzando l'affinità IP di origine, le connessioni avviate da hello stessi computer client passa toohello stesso endpoint DIP.

Hello seguente diagramma viene illustrata una tupla con 2 elementi configurazione. Si noti la modalità di esecuzione tramite hello carico bilanciamento toovirtual macchina 1 (VM1) che viene quindi eseguito il backup VM2 e VM3 hello tupla con 2 elementi.

![affinità di sessione](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

Figura 2. Distribuzione a 2 tuple

Affinità dell'indirizzo IP di origine è stato risolto un problema di incompatibilità tra hello bilanciamento del carico di Azure e Gateway Desktop remoto (desktop remoto). Ora è possibile creare una farm di gateway Desktop remoto in un singolo servizio cloud.

Un altro scenario di caso di utilizzo è il caricamento di supporti in cui il caricamento di dati hello avviene tramite UDP, ma il piano di controllo hello viene ottenuto tramite TCP:

* Un client avvia una sessione TCP indirizzo pubblico con bilanciamento del carico toohello prima di tutto, ottiene tooa diretto DIP specifico, questo canale è stato della connessione hello toomonitor attivo a sinistra
* Una nuova sessione UDP da hello stessi computer client viene avviato toohello endpoint pubblico con bilanciamento del carico stesso, previsione hello qui è che la connessione è anche toohello diretto stesso endpoint DIP connessione TCP precedente hello in modo che supporti caricare può essere viene eseguito a velocità effettiva elevata pur mantenendo un canale di controllo tramite TCP.

> [!NOTE]
> Quando un set con carico bilanciato viene modificato (rimozione o aggiunta di una macchina virtuale), viene ricalcolata distribuzione hello di richieste client. Non è possibile basarsi su nuove connessioni da client esistenti terminando hello stesso server. Inoltre, l'uso della modalità di distribuzione dell'affinità IP di origine può comportare una distribuzione diversa del traffico. I client in esecuzione dietro i proxy possono essere visto come una applicazione client univoca.

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a>Configurazione delle impostazioni di affinità IP di origine per il bilanciamento del carico

Per le macchine virtuali, è possibile utilizzare le impostazioni di timeout toochange PowerShell:

Aggiungere una macchina virtuale di tooa l'endpoint di Azure e impostare modalità di distribuzione del servizio di bilanciamento del carico

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

È possibile impostare LoadBalancerDistribution toosourceIP per 2 tuple (IP di origine, IP di destinazione) bilanciamento del carico, sourceIPProtocol per il bilanciamento del carico di tupla con 3 elementi (protocollo IP di origine, IP di destinazione,) o nessuno se si desidera il comportamento predefinito di hello del bilanciamento del carico di 5 tuple.

Utilizzare hello tooretrieve una configurazione di modalità endpoint distribuzione di bilanciamento del carico seguenti:

    PS C:\> Get-AzureVM –ServiceName MyService –Name MyVM | Get-AzureEndpoint

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
    LoadBalancerDistribution : sourceIP

Se l'elemento LoadBalancerDistribution hello non è presente hello Azure bilanciamento del carico utilizza l'algoritmo predefinito 5 tuple hello.

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a>Impostare la modalità di distribuzione hello in un set di endpoint con carico bilanciato

Se gli endpoint sono parte di un set di endpoint con carico bilanciato, è necessario impostare la modalità di distribuzione hello nel set di endpoint con carico bilanciato hello:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a>Modalità di distribuzione toochange configurazione del servizio cloud

È possibile sfruttare hello Azure SDK per .NET 2.5 (toobe rilasciato nel mese di novembre) tooupdate il servizio Cloud. Le impostazioni di endpoint per servizi Cloud vengono eseguite in hello. csdef. In ordine tooupdate hello carico bilanciamento modalità di distribuzione per una distribuzione di servizi Cloud, è necessario un aggiornamento di distribuzione.
Di seguito è riportato un esempio di modifiche del file con estensione csdef alle impostazioni degli endpoint:

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancerDistribution="sourceIP" />
    </Endpoints>
</WorkerRole>
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

## <a name="api-example"></a>Esempio di API

È possibile configurare una distribuzione del servizio di bilanciamento del carico hello utilizzando l'API di Gestione servizio hello. Verificare che hello tooadd `x-ms-version` intestazione è impostata tooversion `2014-09-01` o versione successiva.

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a>Aggiorna il set di configurazione di hello specificato con bilanciata del carico hello in una distribuzione

#### <a name="request-example"></a>Esempio di richiesta

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>?comp=UpdateLbSet   x-ms-version: 2014-09-01
    Content-Type: application/xml

    <LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
      <InputEndpoint>
        <LoadBalancedEndpointSetName> endpoint-set-name </LoadBalancedEndpointSetName>
        <LocalPort> local-port-number </LocalPort>
        <Port> external-port-number </Port>
        <LoadBalancerProbe>
          <Port> port-assigned-to-probe </Port>
          <Protocol> probe-protocol </Protocol>
          <IntervalInSeconds> interval-of-probe </IntervalInSeconds>
          <TimeoutInSeconds> timeout-for-probe </TimeoutInSeconds>
        </LoadBalancerProbe>
        <Protocol> endpoint-protocol </Protocol>
        <EnableDirectServerReturn> enable-direct-server-return </EnableDirectServerReturn>
        <IdleTimeoutInMinutes>idle-time-out</IdleTimeoutInMinutes>
        <LoadBalancerDistribution>sourceIP</LoadBalancerDistribution>
      </InputEndpoint>
    </LoadBalancedEndpointList>

il valore di Hello di LoadBalancerDistribution può essere sourceIP affinità tupla con 2 elementi, sourceIPProtocol affinità tupla con 3 elementi o Nessuno (per alcuna affinità. ad esempio 5 tuple).

#### <a name="response"></a>Response

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a>Passaggi successivi

[Panoramica del bilanciamento del carico interno](load-balancer-internal-overview.md)

[Introduzione alla configurazione del bilanciamento del carico Internet](load-balancer-get-started-internet-arm-ps.md)

[Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md)
