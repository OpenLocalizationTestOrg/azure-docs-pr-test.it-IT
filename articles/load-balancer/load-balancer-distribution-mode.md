---
title: "Configurare la modalità di distribuzione del bilanciamento del carico |Documentazione Microsoft"
description: "Come configurare la modalità di distribuzione del bilanciamento del carico di Azure per supportare l'affinità IP di origine"
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
ms.openlocfilehash: 4cb000c8ee1bb2e267dc0813dab23a77a46080ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-distribution-mode-for-load-balancer"></a><span data-ttu-id="0a223-103">Configurare la modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="0a223-103">Configure the distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="0a223-104">Modalità di distribuzione basata su hash</span><span class="sxs-lookup"><span data-stu-id="0a223-104">Hash-based distribution mode</span></span>

<span data-ttu-id="0a223-105">L'algoritmo di distribuzione predefinito è un hash a 5 tuple (IP di origine, porta di origine, IP di destinazione, porta di destinazione, tipo di protocollo) per eseguire il mapping del traffico ai server disponibili.</span><span class="sxs-lookup"><span data-stu-id="0a223-105">The default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash to map traffic to available servers.</span></span> <span data-ttu-id="0a223-106">La persistenza viene mantenuta solo all'interno di una sessione di trasporto.</span><span class="sxs-lookup"><span data-stu-id="0a223-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="0a223-107">I pacchetti nella stessa sessione verranno indirizzati alla stessa istanza di IP di data center (DIP) nell'endpoint con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="0a223-107">Packets in the same session will be directed to the same datacenter IP (DIP) instance behind the load balanced endpoint.</span></span> <span data-ttu-id="0a223-108">Quando il client avvia una nuova sessione dallo stesso IP di origine, la porta di origine cambia e il traffico quindi viene indirizzato a un endpoint DIP diverso.</span><span class="sxs-lookup"><span data-stu-id="0a223-108">When the client starts a new session from the same source IP, the source port changes and causes the traffic to go to a different DIP endpoint.</span></span>

![bilanciamento del carico basato su hash](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="0a223-110">Figura 1. Distribuzione a 5 tuple</span><span class="sxs-lookup"><span data-stu-id="0a223-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="0a223-111">Modalità di affinità IP di origine</span><span class="sxs-lookup"><span data-stu-id="0a223-111">Source IP affinity mode</span></span>

<span data-ttu-id="0a223-112">Esiste un'altra modalità di distribuzione definita affinità IP di origine (anche nota come affinità di sessione o affinità del client IP).</span><span class="sxs-lookup"><span data-stu-id="0a223-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="0a223-113">Il bilanciamento del carico di Azure può essere configurato in modo che usi 2 tuple (IP di origine, IP di destinazione) o 3 tuple (IP di origine, IP di destinazione, protocollo) per eseguire il mapping del traffico ai server disponibili.</span><span class="sxs-lookup"><span data-stu-id="0a223-113">Azure Load Balancer can be configured to use a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) to map traffic to the available servers.</span></span> <span data-ttu-id="0a223-114">Usando l'affinità IP di origine, le connessioni avviate dallo stesso computer client passano allo stesso endpoint DIP.</span><span class="sxs-lookup"><span data-stu-id="0a223-114">By using Source IP affinity, connections initiated from the same client computer goes to the same DIP endpoint.</span></span>

<span data-ttu-id="0a223-115">Il diagramma seguente illustra una configurazione a 2 tuple.</span><span class="sxs-lookup"><span data-stu-id="0a223-115">The following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="0a223-116">Si noti come la configurazione a 2 tuple viene eseguita tramite il bilanciamento del carico nella macchina virtuale 1 (VM1) e quindi sottoposta a backup nelle VM2 e VM3.</span><span class="sxs-lookup"><span data-stu-id="0a223-116">Notice how the 2-tuple runs through the load balancer to virtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![affinità di sessione](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="0a223-118">Figura 2. Distribuzione a 2 tuple</span><span class="sxs-lookup"><span data-stu-id="0a223-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="0a223-119">L'affinità IP di origine risolve un'incompatibilità tra il Gateway Desktop remoto e Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="0a223-119">Source IP affinity solves an incompatibility between the Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="0a223-120">Ora è possibile creare una farm di gateway Desktop remoto in un singolo servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="0a223-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="0a223-121">Un altro scenario d'uso è il caricamento di contenuti multimediali dove il caricamento dei dati avviene tramite UDP, ma il piano di controllo viene raggiunto tramite TCP:</span><span class="sxs-lookup"><span data-stu-id="0a223-121">Another use case scenario is media upload where the data upload happens through UDP but the control plane is achieved through TCP:</span></span>

* <span data-ttu-id="0a223-122">Prima un client avvia una sessione TCP all'indirizzo pubblico con carico bilanciato e viene diretto a un DIP specifico. Questo canale viene lasciato attivo per monitorare lo stato della connessione</span><span class="sxs-lookup"><span data-stu-id="0a223-122">A client first initiates a TCP session to the load balanced public address, gets directed to a specific DIP, this channel is left active to monitor the connection health</span></span>
* <span data-ttu-id="0a223-123">Viene avviata una nuova sessione UDP dallo stesso computer client allo stesso endpoint pubblico con carico bilanciato. Qui ci si aspetta che anche questa connessione venga indirizzata allo stesso endpoint DIP della precedente connessione TCP in modo che il caricamento di contenuti multimediali possa essere eseguito a una velocità effettiva elevata, mantenendo allo stesso tempo un canale di controllo tramite TCP.</span><span class="sxs-lookup"><span data-stu-id="0a223-123">A new UDP session from the same client computer is initiated to the same load balanced public endpoint, the expectation here is that this connection is also directed to the same DIP endpoint as the previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="0a223-124">Quando il set con carico bilanciato viene modificato (rimozione o aggiunta di una macchina virtuale), la distribuzione delle richieste client viene ricalcolata.</span><span class="sxs-lookup"><span data-stu-id="0a223-124">When a load-balanced set changes (removing or adding a virtual machine), the distribution of client requests is recomputed.</span></span> <span data-ttu-id="0a223-125">Non è possibile dipendere da nuove connessioni da client esistenti che terminano nello stesso server.</span><span class="sxs-lookup"><span data-stu-id="0a223-125">You cannot depend on new connections from existing clients ending up at the same server.</span></span> <span data-ttu-id="0a223-126">Inoltre, l'uso della modalità di distribuzione dell'affinità IP di origine può comportare una distribuzione diversa del traffico.</span><span class="sxs-lookup"><span data-stu-id="0a223-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="0a223-127">I client in esecuzione dietro i proxy possono essere visto come una applicazione client univoca.</span><span class="sxs-lookup"><span data-stu-id="0a223-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="0a223-128">Configurazione delle impostazioni di affinità IP di origine per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="0a223-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="0a223-129">Per le macchine virtuali, è possibile usare PowerShell per modificare le impostazioni di timeout:</span><span class="sxs-lookup"><span data-stu-id="0a223-129">For virtual machines, you can use PowerShell to change timeout settings:</span></span>

<span data-ttu-id="0a223-130">Aggiungere un endpoint di Azure a una macchina virtuale e impostare la modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="0a223-130">Add an Azure endpoint to a Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="0a223-131">LoadBalancerDistribution può essere impostato su sourceIP per il bilanciamento del carico a 2 tuple (IP di origine, IP di destinazione), su sourceIPProtocol per il bilanciamento del carico a 3 tuple (IP di origine, IP di destinazione, protocollo) o su Nessuno per il comportamento predefinito con bilanciamento del carico a 5 tuple.</span><span class="sxs-lookup"><span data-stu-id="0a223-131">LoadBalancerDistribution can be set to sourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want the default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="0a223-132">Usare il codice seguente per recuperare una configurazione con modalità di distribuzione del bilanciamento del carico con endpoint:</span><span class="sxs-lookup"><span data-stu-id="0a223-132">Use the following to retrieve an endpoint load balancer distribution mode configuration:</span></span>

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

<span data-ttu-id="0a223-133">Se l'elemento LoadBalancerDistribution non viene specificato, il bilanciamento del carico di Azure utilizza l'algoritmo di 5 tuple predefinito</span><span class="sxs-lookup"><span data-stu-id="0a223-133">If the LoadBalancerDistribution element is not present then the Azure Load balancer uses the default 5-tuple algorithm.</span></span>

### <a name="set-the-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="0a223-134">Impostare la modalità di distribuzione su un set di endpoint con carico bilanciato</span><span class="sxs-lookup"><span data-stu-id="0a223-134">Set the Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="0a223-135">Se gli endpoint fanno parte di un set di endpoint con carico bilanciato, è necessario impostare la modalità di distribuzione sul set di endpoint con carico bilanciato:</span><span class="sxs-lookup"><span data-stu-id="0a223-135">If endpoints are part of a load balanced endpoint set, the distribution mode must be set on the load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-to-change-distribution-mode"></a><span data-ttu-id="0a223-136">Configurazione del servizio cloud per modificare la modalità di distribuzione</span><span class="sxs-lookup"><span data-stu-id="0a223-136">Cloud Service configuration to change distribution mode</span></span>

<span data-ttu-id="0a223-137">È possibile usare Azure SDK per .NET 2.5 (in arrivo a novembre) per aggiornare il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="0a223-137">You can leverage the Azure SDK for .NET 2.5 (to be released in November) to update your Cloud Service.</span></span> <span data-ttu-id="0a223-138">Le impostazioni degli endpoint per i servizi cloud vengono effettuate nel file con estensione csdef.</span><span class="sxs-lookup"><span data-stu-id="0a223-138">Endpoint settings for Cloud Services are made in the .csdef.</span></span> <span data-ttu-id="0a223-139">Per aggiornare la modalità di distribuzione del servizio di bilanciamento del carico per una distribuzione di servizi cloud, è necessario un aggiornamento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0a223-139">In order to update the load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="0a223-140">Di seguito è riportato un esempio di modifiche del file con estensione csdef alle impostazioni degli endpoint:</span><span class="sxs-lookup"><span data-stu-id="0a223-140">Here is an example of .csdef changes for endpoint settings:</span></span>

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

## <a name="api-example"></a><span data-ttu-id="0a223-141">Esempio di API</span><span class="sxs-lookup"><span data-stu-id="0a223-141">API example</span></span>

<span data-ttu-id="0a223-142">È possibile configurare la distribuzione del servizio di bilanciamento del carico tramite l'API di gestione dei servizi.</span><span class="sxs-lookup"><span data-stu-id="0a223-142">You can configure the load balancer distribution using the service management API.</span></span> <span data-ttu-id="0a223-143">Assicurarsi di aggiungere l'intestazione `x-ms-version` impostata sulla versione `2014-09-01` o successiva.</span><span class="sxs-lookup"><span data-stu-id="0a223-143">Make sure to add the `x-ms-version` header is set to version `2014-09-01` or higher.</span></span>

### <a name="update-the-configuration-of-the-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="0a223-144">Aggiornare la configurazione del set con carico bilanciato specificato in una distribuzione</span><span class="sxs-lookup"><span data-stu-id="0a223-144">Update the configuration of the specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="0a223-145">Esempio di richiesta</span><span class="sxs-lookup"><span data-stu-id="0a223-145">Request example</span></span>

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

<span data-ttu-id="0a223-146">Il valore di LoadBalancerDistribution può essere sourceIP per l'affinità a 2 tuple, sourceIPProtocol per l'affinità a 3 tuple o Nessuno (per nessuna affinità,</span><span class="sxs-lookup"><span data-stu-id="0a223-146">The value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="0a223-147">ad esempio 5 tuple).</span><span class="sxs-lookup"><span data-stu-id="0a223-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="0a223-148">Response</span><span class="sxs-lookup"><span data-stu-id="0a223-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="0a223-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0a223-149">Next Steps</span></span>

[<span data-ttu-id="0a223-150">Panoramica del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="0a223-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="0a223-151">Introduzione alla configurazione del bilanciamento del carico Internet</span><span class="sxs-lookup"><span data-stu-id="0a223-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="0a223-152">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="0a223-152">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
