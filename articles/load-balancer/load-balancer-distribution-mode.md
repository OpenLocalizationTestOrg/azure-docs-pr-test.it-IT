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
# <a name="configure-hello-distribution-mode-for-load-balancer"></a><span data-ttu-id="885d9-103">Configurare la modalità di distribuzione hello di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="885d9-103">Configure hello distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="885d9-104">Modalità di distribuzione basata su hash</span><span class="sxs-lookup"><span data-stu-id="885d9-104">Hash-based distribution mode</span></span>

<span data-ttu-id="885d9-105">algoritmo di distribuzione predefinito di Hello è una tupla con 5 (origine IP, porta di origine, IP di destinazione, la porta di destinazione, tipo di protocollo) Server tooavailable di traffico toomap hash.</span><span class="sxs-lookup"><span data-stu-id="885d9-105">hello default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash toomap traffic tooavailable servers.</span></span> <span data-ttu-id="885d9-106">La persistenza viene mantenuta solo all'interno di una sessione di trasporto.</span><span class="sxs-lookup"><span data-stu-id="885d9-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="885d9-107">I pacchetti hello stessa sessione saranno indirizzate toohello istanza stesso Data Center IP (DIP) dietro l'endpoint con carico bilanciato hello.</span><span class="sxs-lookup"><span data-stu-id="885d9-107">Packets in hello same session will be directed toohello same datacenter IP (DIP) instance behind hello load balanced endpoint.</span></span> <span data-ttu-id="885d9-108">Quando hello client avvia una nuova sessione da hello stesso indirizzo IP di origine, la porta di origine hello viene modificata e provoca hello traffico toogo tooa DIP endpoint diversi.</span><span class="sxs-lookup"><span data-stu-id="885d9-108">When hello client starts a new session from hello same source IP, hello source port changes and causes hello traffic toogo tooa different DIP endpoint.</span></span>

![bilanciamento del carico basato su hash](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="885d9-110">Figura 1. Distribuzione a 5 tuple</span><span class="sxs-lookup"><span data-stu-id="885d9-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="885d9-111">Modalità di affinità IP di origine</span><span class="sxs-lookup"><span data-stu-id="885d9-111">Source IP affinity mode</span></span>

<span data-ttu-id="885d9-112">Esiste un'altra modalità di distribuzione definita affinità IP di origine (anche nota come affinità di sessione o affinità del client IP).</span><span class="sxs-lookup"><span data-stu-id="885d9-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="885d9-113">Bilanciamento del carico di Azure può essere configurato toouse una tupla con 2 (indirizzo IP di origine, IP di destinazione) o server disponibili toohello il traffico toomap tupla con 3 elementi (indirizzo IP di origine, IP di destinazione, Protocol).</span><span class="sxs-lookup"><span data-stu-id="885d9-113">Azure Load Balancer can be configured toouse a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) toomap traffic toohello available servers.</span></span> <span data-ttu-id="885d9-114">Utilizzando l'affinità IP di origine, le connessioni avviate da hello stessi computer client passa toohello stesso endpoint DIP.</span><span class="sxs-lookup"><span data-stu-id="885d9-114">By using Source IP affinity, connections initiated from hello same client computer goes toohello same DIP endpoint.</span></span>

<span data-ttu-id="885d9-115">Hello seguente diagramma viene illustrata una tupla con 2 elementi configurazione.</span><span class="sxs-lookup"><span data-stu-id="885d9-115">hello following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="885d9-116">Si noti la modalità di esecuzione tramite hello carico bilanciamento toovirtual macchina 1 (VM1) che viene quindi eseguito il backup VM2 e VM3 hello tupla con 2 elementi.</span><span class="sxs-lookup"><span data-stu-id="885d9-116">Notice how hello 2-tuple runs through hello load balancer toovirtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![affinità di sessione](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="885d9-118">Figura 2. Distribuzione a 2 tuple</span><span class="sxs-lookup"><span data-stu-id="885d9-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="885d9-119">Affinità dell'indirizzo IP di origine è stato risolto un problema di incompatibilità tra hello bilanciamento del carico di Azure e Gateway Desktop remoto (desktop remoto).</span><span class="sxs-lookup"><span data-stu-id="885d9-119">Source IP affinity solves an incompatibility between hello Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="885d9-120">Ora è possibile creare una farm di gateway Desktop remoto in un singolo servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="885d9-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="885d9-121">Un altro scenario di caso di utilizzo è il caricamento di supporti in cui il caricamento di dati hello avviene tramite UDP, ma il piano di controllo hello viene ottenuto tramite TCP:</span><span class="sxs-lookup"><span data-stu-id="885d9-121">Another use case scenario is media upload where hello data upload happens through UDP but hello control plane is achieved through TCP:</span></span>

* <span data-ttu-id="885d9-122">Un client avvia una sessione TCP indirizzo pubblico con bilanciamento del carico toohello prima di tutto, ottiene tooa diretto DIP specifico, questo canale è stato della connessione hello toomonitor attivo a sinistra</span><span class="sxs-lookup"><span data-stu-id="885d9-122">A client first initiates a TCP session toohello load balanced public address, gets directed tooa specific DIP, this channel is left active toomonitor hello connection health</span></span>
* <span data-ttu-id="885d9-123">Una nuova sessione UDP da hello stessi computer client viene avviato toohello endpoint pubblico con bilanciamento del carico stesso, previsione hello qui è che la connessione è anche toohello diretto stesso endpoint DIP connessione TCP precedente hello in modo che supporti caricare può essere viene eseguito a velocità effettiva elevata pur mantenendo un canale di controllo tramite TCP.</span><span class="sxs-lookup"><span data-stu-id="885d9-123">A new UDP session from hello same client computer is initiated toohello same load balanced public endpoint, hello expectation here is that this connection is also directed toohello same DIP endpoint as hello previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="885d9-124">Quando un set con carico bilanciato viene modificato (rimozione o aggiunta di una macchina virtuale), viene ricalcolata distribuzione hello di richieste client.</span><span class="sxs-lookup"><span data-stu-id="885d9-124">When a load-balanced set changes (removing or adding a virtual machine), hello distribution of client requests is recomputed.</span></span> <span data-ttu-id="885d9-125">Non è possibile basarsi su nuove connessioni da client esistenti terminando hello stesso server.</span><span class="sxs-lookup"><span data-stu-id="885d9-125">You cannot depend on new connections from existing clients ending up at hello same server.</span></span> <span data-ttu-id="885d9-126">Inoltre, l'uso della modalità di distribuzione dell'affinità IP di origine può comportare una distribuzione diversa del traffico.</span><span class="sxs-lookup"><span data-stu-id="885d9-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="885d9-127">I client in esecuzione dietro i proxy possono essere visto come una applicazione client univoca.</span><span class="sxs-lookup"><span data-stu-id="885d9-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="885d9-128">Configurazione delle impostazioni di affinità IP di origine per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="885d9-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="885d9-129">Per le macchine virtuali, è possibile utilizzare le impostazioni di timeout toochange PowerShell:</span><span class="sxs-lookup"><span data-stu-id="885d9-129">For virtual machines, you can use PowerShell toochange timeout settings:</span></span>

<span data-ttu-id="885d9-130">Aggiungere una macchina virtuale di tooa l'endpoint di Azure e impostare modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="885d9-130">Add an Azure endpoint tooa Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="885d9-131">È possibile impostare LoadBalancerDistribution toosourceIP per 2 tuple (IP di origine, IP di destinazione) bilanciamento del carico, sourceIPProtocol per il bilanciamento del carico di tupla con 3 elementi (protocollo IP di origine, IP di destinazione,) o nessuno se si desidera il comportamento predefinito di hello del bilanciamento del carico di 5 tuple.</span><span class="sxs-lookup"><span data-stu-id="885d9-131">LoadBalancerDistribution can be set toosourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want hello default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="885d9-132">Utilizzare hello tooretrieve una configurazione di modalità endpoint distribuzione di bilanciamento del carico seguenti:</span><span class="sxs-lookup"><span data-stu-id="885d9-132">Use hello following tooretrieve an endpoint load balancer distribution mode configuration:</span></span>

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

<span data-ttu-id="885d9-133">Se l'elemento LoadBalancerDistribution hello non è presente hello Azure bilanciamento del carico utilizza l'algoritmo predefinito 5 tuple hello.</span><span class="sxs-lookup"><span data-stu-id="885d9-133">If hello LoadBalancerDistribution element is not present then hello Azure Load balancer uses hello default 5-tuple algorithm.</span></span>

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="885d9-134">Impostare la modalità di distribuzione hello in un set di endpoint con carico bilanciato</span><span class="sxs-lookup"><span data-stu-id="885d9-134">Set hello Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="885d9-135">Se gli endpoint sono parte di un set di endpoint con carico bilanciato, è necessario impostare la modalità di distribuzione hello nel set di endpoint con carico bilanciato hello:</span><span class="sxs-lookup"><span data-stu-id="885d9-135">If endpoints are part of a load balanced endpoint set, hello distribution mode must be set on hello load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a><span data-ttu-id="885d9-136">Modalità di distribuzione toochange configurazione del servizio cloud</span><span class="sxs-lookup"><span data-stu-id="885d9-136">Cloud Service configuration toochange distribution mode</span></span>

<span data-ttu-id="885d9-137">È possibile sfruttare hello Azure SDK per .NET 2.5 (toobe rilasciato nel mese di novembre) tooupdate il servizio Cloud.</span><span class="sxs-lookup"><span data-stu-id="885d9-137">You can leverage hello Azure SDK for .NET 2.5 (toobe released in November) tooupdate your Cloud Service.</span></span> <span data-ttu-id="885d9-138">Le impostazioni di endpoint per servizi Cloud vengono eseguite in hello. csdef.</span><span class="sxs-lookup"><span data-stu-id="885d9-138">Endpoint settings for Cloud Services are made in hello .csdef.</span></span> <span data-ttu-id="885d9-139">In ordine tooupdate hello carico bilanciamento modalità di distribuzione per una distribuzione di servizi Cloud, è necessario un aggiornamento di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="885d9-139">In order tooupdate hello load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="885d9-140">Di seguito è riportato un esempio di modifiche del file con estensione csdef alle impostazioni degli endpoint:</span><span class="sxs-lookup"><span data-stu-id="885d9-140">Here is an example of .csdef changes for endpoint settings:</span></span>

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

## <a name="api-example"></a><span data-ttu-id="885d9-141">Esempio di API</span><span class="sxs-lookup"><span data-stu-id="885d9-141">API example</span></span>

<span data-ttu-id="885d9-142">È possibile configurare una distribuzione del servizio di bilanciamento del carico hello utilizzando l'API di Gestione servizio hello.</span><span class="sxs-lookup"><span data-stu-id="885d9-142">You can configure hello load balancer distribution using hello service management API.</span></span> <span data-ttu-id="885d9-143">Verificare che hello tooadd `x-ms-version` intestazione è impostata tooversion `2014-09-01` o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="885d9-143">Make sure tooadd hello `x-ms-version` header is set tooversion `2014-09-01` or higher.</span></span>

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="885d9-144">Aggiorna il set di configurazione di hello specificato con bilanciata del carico hello in una distribuzione</span><span class="sxs-lookup"><span data-stu-id="885d9-144">Update hello configuration of hello specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="885d9-145">Esempio di richiesta</span><span class="sxs-lookup"><span data-stu-id="885d9-145">Request example</span></span>

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

<span data-ttu-id="885d9-146">il valore di Hello di LoadBalancerDistribution può essere sourceIP affinità tupla con 2 elementi, sourceIPProtocol affinità tupla con 3 elementi o Nessuno (per alcuna affinità.</span><span class="sxs-lookup"><span data-stu-id="885d9-146">hello value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="885d9-147">ad esempio 5 tuple).</span><span class="sxs-lookup"><span data-stu-id="885d9-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="885d9-148">Response</span><span class="sxs-lookup"><span data-stu-id="885d9-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="885d9-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="885d9-149">Next Steps</span></span>

[<span data-ttu-id="885d9-150">Panoramica del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="885d9-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="885d9-151">Introduzione alla configurazione del bilanciamento del carico Internet</span><span class="sxs-lookup"><span data-stu-id="885d9-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="885d9-152">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="885d9-152">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
