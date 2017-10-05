---
title: "Configurare il timeout di inattività TCP di Load Balancer | Microsoft Docs"
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
ms.openlocfilehash: d040fe6580b8ae777aecc9dd385ed33861530c38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="ae9ec-103">Configurazione del timeout di inattività TCP di Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="ae9ec-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="ae9ec-104">La configurazione predefinita di Azure Load Balancer prevede che il timeout di inattività sia impostato su 4 minuti.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="ae9ec-105">Se un periodo di inattività è più lungo del valore di timeout, non ci sono garanzie che venga mantenuta la sessione TCP o HTTP tra il client e il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-105">If a period of inactivity is longer than the timeout value, there's no guarantee that the TCP or HTTP session is maintained between the client and your cloud service.</span></span>

<span data-ttu-id="ae9ec-106">Quando la connessione viene chiusa, l'applicazione client potrebbe ricevere il messaggio di errore seguente: "Connessione sottostante chiusa: una connessione che doveva restare attiva è stata chiusa dal server in modo imprevisto".</span><span class="sxs-lookup"><span data-stu-id="ae9ec-106">When the connection is closed, your client application may receive the following error message: "The underlying connection was closed: A connection that was expected to be kept alive was closed by the server."</span></span>

<span data-ttu-id="ae9ec-107">Una prassi comune consiste nell'usare una connessione TCP keep-alive</span><span class="sxs-lookup"><span data-stu-id="ae9ec-107">A common practice is to use a TCP keep-alive.</span></span> <span data-ttu-id="ae9ec-108">per mantenere la connessione attiva per un periodo più lungo.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-108">This practice keeps the connection active for a longer period.</span></span> <span data-ttu-id="ae9ec-109">Per altre informazioni, vedere questi [esempi .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span><span class="sxs-lookup"><span data-stu-id="ae9ec-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="ae9ec-110">Con la connessione keep-alive abilitata, i pacchetti vengono inviati durante i periodi di inattività della connessione.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-110">With keep-alive enabled, packets are sent during periods of inactivity on the connection.</span></span> <span data-ttu-id="ae9ec-111">Questi pacchetti keep-alive garantiscono che il valore del timeout di inattività non venga mai raggiunto e che la connessione sia mantenuta per un lungo periodo.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-111">These keep-alive packets ensure that the idle timeout value is never reached and the connection is maintained for a long period.</span></span>

<span data-ttu-id="ae9ec-112">Questa impostazione funziona solo per le connessioni in entrata.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="ae9ec-113">Per evitare di perdere la connessione, è necessario configurare l'impostazione keep-alive TCP con un intervallo minore rispetto all'impostazione di timeout di inattività o aumentare il valore del timeout di inattività.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-113">To avoid losing the connection, you must configure the TCP keep-alive with an interval less than the idle timeout setting or increase the idle timeout value.</span></span> <span data-ttu-id="ae9ec-114">Per supportare tali scenari, è stato aggiunto il supporto per un timeout di inattività configurabile.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-114">To support such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="ae9ec-115">È ora possibile impostare questo valore su una durata compresa tra 4 e 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-115">You can now set it for a duration of 4 to 30 minutes.</span></span>

<span data-ttu-id="ae9ec-116">La connessione TCP keep-alive è particolarmente adatta per gli scenari non vincolati alla durata della batteria,</span><span class="sxs-lookup"><span data-stu-id="ae9ec-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="ae9ec-117">mentre non è consigliabile per le applicazioni mobili.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="ae9ec-118">L'uso di un'impostazione keep-alive TCP in un'applicazione per dispositivi mobili può far scaricare più velocemente la batteria del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-118">Using a TCP keep-alive in a mobile application can drain the device battery faster.</span></span>

![Timeout TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="ae9ec-120">Nella sezione seguente è descritto come modificare le impostazioni del timeout di inattività in macchine virtuali e servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-120">The following sections describe how to change idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-the-tcp-timeout-for-your-instance-level-public-ip-to-15-minutes"></a><span data-ttu-id="ae9ec-121">Configurazione del timeout TCP per l'IP pubblico a livello di istanza su 15 minuti</span><span class="sxs-lookup"><span data-stu-id="ae9ec-121">Configure the TCP timeout for your instance-level public IP to 15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="ae9ec-122">`IdleTimeoutInMinutes` è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="ae9ec-123">Se non impostato, il timeout predefinito è 4 minuti.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-123">If it is not set, the default timeout is 4 minutes.</span></span> <span data-ttu-id="ae9ec-124">L'intervallo di timeout accettabile è compreso tra 4 e 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-124">The acceptable timeout range is 4 to 30 minutes.</span></span>

## <a name="set-the-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="ae9ec-125">Impostazione del timeout di inattività durante la creazione di un endpoint di Azure in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="ae9ec-125">Set the idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="ae9ec-126">Per modificare l'impostazione di timeout per un endpoint, usare il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="ae9ec-126">To change the timeout setting for an endpoint, use the following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="ae9ec-127">Per recuperare la configurazione del timeout di inattività, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ae9ec-127">To retrieve your idle timeout configuration, use the following command:</span></span>

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

## <a name="set-the-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="ae9ec-128">Impostazione del timeout TCP su un set di endpoint con carico bilanciato</span><span class="sxs-lookup"><span data-stu-id="ae9ec-128">Set the TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="ae9ec-129">Se gli endpoint fanno parte di un set di endpoint con carico bilanciato, è necessario impostare il timeout TCP sul set di endpoint con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-129">If endpoints are part of a load-balanced endpoint set, the TCP timeout must be set on the load-balanced endpoint set.</span></span> <span data-ttu-id="ae9ec-130">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ae9ec-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="ae9ec-131">Modifica delle impostazioni di timeout per i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="ae9ec-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="ae9ec-132">È possibile usare Azure SDK per aggiornare il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-132">You can use the Azure SDK to update your cloud service.</span></span> <span data-ttu-id="ae9ec-133">Le impostazioni degli endpoint per i servizi cloud vengono effettuate nel file .csdef.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-133">You make endpoint settings for cloud services in the .csdef file.</span></span> <span data-ttu-id="ae9ec-134">L'aggiornamento il timeout TCP per la distribuzione di un servizio cloud richiede un aggiornamento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-134">Updating the TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="ae9ec-135">Fa eccezione il caso in cui il timeout TCP sia specificato solo per un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-135">An exception is if the TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="ae9ec-136">Le impostazioni degli indirizzi IP pubblici si trovano nel file .cscfg e possono essere aggiornate tramite l'aggiornamento della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-136">Public IP settings are in the .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="ae9ec-137">Le modifiche del file con estensione csdef per le impostazioni di endpoint sono:</span><span class="sxs-lookup"><span data-stu-id="ae9ec-137">The .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="ae9ec-138">Le modifiche al file .cscfg per l'impostazione di timeout negli indirizzi IP pubblici sono le seguenti:</span><span class="sxs-lookup"><span data-stu-id="ae9ec-138">The .cscfg changes for the timeout setting on public IPs are:</span></span>

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

## <a name="rest-api-example"></a><span data-ttu-id="ae9ec-139">Esempio di API REST</span><span class="sxs-lookup"><span data-stu-id="ae9ec-139">REST API example</span></span>

<span data-ttu-id="ae9ec-140">È possibile configurare il timeout di inattività TCP l'API Gestione dei servizi.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-140">You can configure the TCP idle timeout by using the service management API.</span></span> <span data-ttu-id="ae9ec-141">Controllare che l'intestazione `x-ms-version` sia impostata sulla versione `2014-06-01` o successiva.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-141">Make sure that the `x-ms-version` header is set to version `2014-06-01` or later.</span></span> <span data-ttu-id="ae9ec-142">Aggiornare la configurazione degli endpoint di input specificati con carico bilanciato in tutte le macchine virtuali di una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ae9ec-142">Update the configuration of the specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="ae9ec-143">Richiesta</span><span class="sxs-lookup"><span data-stu-id="ae9ec-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="ae9ec-144">Response</span><span class="sxs-lookup"><span data-stu-id="ae9ec-144">Response</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ae9ec-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ae9ec-145">Next steps</span></span>

[<span data-ttu-id="ae9ec-146">Panoramica del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="ae9ec-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="ae9ec-147">Introduzione alla configurazione del bilanciamento del carico Internet</span><span class="sxs-lookup"><span data-stu-id="ae9ec-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="ae9ec-148">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="ae9ec-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
