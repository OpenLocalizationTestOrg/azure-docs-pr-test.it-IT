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
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="43768-103">Configurazione del timeout di inattività TCP di Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="43768-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="43768-104">La configurazione predefinita di Azure Load Balancer prevede che il timeout di inattività sia impostato su 4 minuti.</span><span class="sxs-lookup"><span data-stu-id="43768-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="43768-105">Se un periodo di inattività supera il valore di timeout di hello, non c'è garanzia che hello TCP o HTTP sessione viene mantenuta tra client hello e il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="43768-105">If a period of inactivity is longer than hello timeout value, there's no guarantee that hello TCP or HTTP session is maintained between hello client and your cloud service.</span></span>

<span data-ttu-id="43768-106">Chiusura della connessione hello, l'applicazione client può ricevere hello seguente messaggio di errore: "hello connessione sottostante chiusa: una connessione che doveva toobe mantenuta attiva è stata chiusa dal server hello."</span><span class="sxs-lookup"><span data-stu-id="43768-106">When hello connection is closed, your client application may receive hello following error message: "hello underlying connection was closed: A connection that was expected toobe kept alive was closed by hello server."</span></span>

<span data-ttu-id="43768-107">Una pratica comune è toouse un keep-alive TCP.</span><span class="sxs-lookup"><span data-stu-id="43768-107">A common practice is toouse a TCP keep-alive.</span></span> <span data-ttu-id="43768-108">Questa procedura mantiene connessione hello attivo per un periodo più lungo.</span><span class="sxs-lookup"><span data-stu-id="43768-108">This practice keeps hello connection active for a longer period.</span></span> <span data-ttu-id="43768-109">Per altre informazioni, vedere questi [esempi .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span><span class="sxs-lookup"><span data-stu-id="43768-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="43768-110">Keep-alive abilitata, i pacchetti vengono inviati durante i periodi di inattività della connessione hello.</span><span class="sxs-lookup"><span data-stu-id="43768-110">With keep-alive enabled, packets are sent during periods of inactivity on hello connection.</span></span> <span data-ttu-id="43768-111">Questi pacchetti keep-alive assicurarsi che il valore di timeout di inattività hello non viene mai raggiunto e connessione hello viene mantenuta per un lungo periodo.</span><span class="sxs-lookup"><span data-stu-id="43768-111">These keep-alive packets ensure that hello idle timeout value is never reached and hello connection is maintained for a long period.</span></span>

<span data-ttu-id="43768-112">Questa impostazione funziona solo per le connessioni in entrata.</span><span class="sxs-lookup"><span data-stu-id="43768-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="43768-113">tooavoid perdita della connessione hello, è necessario configurare hello keep-alive TCP con un intervallo minore di hello timeout di inattività impostazione o aumentare hello valore timeout di inattività.</span><span class="sxs-lookup"><span data-stu-id="43768-113">tooavoid losing hello connection, you must configure hello TCP keep-alive with an interval less than hello idle timeout setting or increase hello idle timeout value.</span></span> <span data-ttu-id="43768-114">toosupport tali scenari, è stato aggiunto il supporto per un timeout di inattività.</span><span class="sxs-lookup"><span data-stu-id="43768-114">toosupport such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="43768-115">È ora possibile impostare per una durata pari a 4 minuti too30.</span><span class="sxs-lookup"><span data-stu-id="43768-115">You can now set it for a duration of 4 too30 minutes.</span></span>

<span data-ttu-id="43768-116">La connessione TCP keep-alive è particolarmente adatta per gli scenari non vincolati alla durata della batteria,</span><span class="sxs-lookup"><span data-stu-id="43768-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="43768-117">mentre non è consigliabile per le applicazioni mobili.</span><span class="sxs-lookup"><span data-stu-id="43768-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="43768-118">Con un TCP keep-alive in un'applicazione per dispositivi mobili possono svuotare batteria dispositivo hello più velocemente.</span><span class="sxs-lookup"><span data-stu-id="43768-118">Using a TCP keep-alive in a mobile application can drain hello device battery faster.</span></span>

![Timeout TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="43768-120">Hello le sezioni seguenti descrivono come toochange nelle macchine virtuali, le impostazioni di timeout di inattività e i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="43768-120">hello following sections describe how toochange idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a><span data-ttu-id="43768-121">Configurare timeout TCP hello per i minuti di too15 IP pubblici a livello di istanza</span><span class="sxs-lookup"><span data-stu-id="43768-121">Configure hello TCP timeout for your instance-level public IP too15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="43768-122">`IdleTimeoutInMinutes` è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="43768-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="43768-123">Se non è impostata, il timeout predefinito hello è 4 minuti.</span><span class="sxs-lookup"><span data-stu-id="43768-123">If it is not set, hello default timeout is 4 minutes.</span></span> <span data-ttu-id="43768-124">intervallo di timeout accettabile Hello è 4 too30 minuti.</span><span class="sxs-lookup"><span data-stu-id="43768-124">hello acceptable timeout range is 4 too30 minutes.</span></span>

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="43768-125">Impostare i timeout di inattività hello durante la creazione di un endpoint di Azure in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="43768-125">Set hello idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="43768-126">toochange hello timeout impostazione per un endpoint, utilizzare hello seguente:</span><span class="sxs-lookup"><span data-stu-id="43768-126">toochange hello timeout setting for an endpoint, use hello following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="43768-127">tooretrieve la configurazione di timeout di inattività, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="43768-127">tooretrieve your idle timeout configuration, use hello following command:</span></span>

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

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="43768-128">Impostare i timeout TCP hello in un set di endpoint con bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="43768-128">Set hello TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="43768-129">Se gli endpoint sono parte di un set di endpoint con bilanciamento del carico, è necessario impostare timeout TCP hello in set di endpoint con carico bilanciato hello.</span><span class="sxs-lookup"><span data-stu-id="43768-129">If endpoints are part of a load-balanced endpoint set, hello TCP timeout must be set on hello load-balanced endpoint set.</span></span> <span data-ttu-id="43768-130">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="43768-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="43768-131">Modifica delle impostazioni di timeout per i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="43768-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="43768-132">È possibile utilizzare hello Azure SDK tooupdate il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="43768-132">You can use hello Azure SDK tooupdate your cloud service.</span></span> <span data-ttu-id="43768-133">File con estensione csdef hello è effettuare le impostazioni di endpoint per i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="43768-133">You make endpoint settings for cloud services in hello .csdef file.</span></span> <span data-ttu-id="43768-134">L'aggiornamento di hello timeout TCP per la distribuzione di un servizio cloud richiede un aggiornamento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="43768-134">Updating hello TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="43768-135">Un'eccezione è se hello TCP timeout viene specificato solo per un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="43768-135">An exception is if hello TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="43768-136">Impostazioni dell'IP pubbliche sono nel file con estensione cscfg hello e aggiornarle tramite l'aggiornamento e aggiornamento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="43768-136">Public IP settings are in hello .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="43768-137">modifiche di csdef Hello per le impostazioni di endpoint sono:</span><span class="sxs-lookup"><span data-stu-id="43768-137">hello .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="43768-138">le modifiche apportate al file con estensione cscfg Hello per l'impostazione di timeout hello su indirizzi IP pubblici sono:</span><span class="sxs-lookup"><span data-stu-id="43768-138">hello .cscfg changes for hello timeout setting on public IPs are:</span></span>

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

## <a name="rest-api-example"></a><span data-ttu-id="43768-139">Esempio di API REST</span><span class="sxs-lookup"><span data-stu-id="43768-139">REST API example</span></span>

<span data-ttu-id="43768-140">È possibile configurare i timeout di inattività TCP hello mediante API di Gestione servizio hello.</span><span class="sxs-lookup"><span data-stu-id="43768-140">You can configure hello TCP idle timeout by using hello service management API.</span></span> <span data-ttu-id="43768-141">Verificare che tale hello `x-ms-version` intestazione è impostata tooversion `2014-06-01` o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="43768-141">Make sure that hello `x-ms-version` header is set tooversion `2014-06-01` or later.</span></span> <span data-ttu-id="43768-142">Aggiorna configurazione hello di hello specifica gli endpoint di input con bilanciamento del carico in tutte le macchine virtuali in una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="43768-142">Update hello configuration of hello specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="43768-143">Richiesta</span><span class="sxs-lookup"><span data-stu-id="43768-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="43768-144">Response</span><span class="sxs-lookup"><span data-stu-id="43768-144">Response</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="43768-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="43768-145">Next steps</span></span>

[<span data-ttu-id="43768-146">Panoramica del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="43768-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="43768-147">Introduzione alla configurazione del bilanciamento del carico Internet</span><span class="sxs-lookup"><span data-stu-id="43768-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="43768-148">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="43768-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
