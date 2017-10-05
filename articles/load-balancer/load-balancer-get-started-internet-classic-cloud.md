---
title: Creare un servizio di bilanciamento del carico con connessione Internet per Servizi cloud di Azure | Documentazione Microsoft
description: Informazioni su come creare un servizio di bilanciamento del carico Internet nel modello di distribuzione classica per i servizi cloud
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 0bb16f96-56a6-429f-88f5-0de2d0136756
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 1ceaafebcaebecb04314c7da62c69b2e9b5ba39a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a><span data-ttu-id="35272-103">Introduzione alla creazione del servizio di bilanciamento del carico Internet per i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="35272-103">Get started creating an Internet facing load balancer for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="35272-104">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="35272-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="35272-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="35272-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="35272-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="35272-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="35272-107">Servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="35272-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="35272-108">Prima di iniziare a usare le risorse di Azure, è importante comprendere che Azure al momento offre due modelli di distribuzione, la distribuzione classica e Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="35272-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="35272-109">È importante comprendere i [modelli e strumenti di distribuzione](../azure-classic-rm.md) prima di lavorare con le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="35272-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="35272-110">È possibile visualizzare la documentazione relativa a diversi strumenti facendo clic sulle schede nella parte superiore di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="35272-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="35272-111">In questo articolo viene illustrato il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="35272-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="35272-112">Vedere [Informazioni su come creare un servizio di bilanciamento del carico Internet in Gestione risorse di Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="35272-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

<span data-ttu-id="35272-113">I servizi cloud vengono configurati automaticamente con il servizio di bilanciamento del carico e possono essere personalizzati tramite il modello del servizio.</span><span class="sxs-lookup"><span data-stu-id="35272-113">Cloud services are automatically configured with a load balancer and can be customized via the service model.</span></span>

## <a name="create-a-load-balancer-using-the-service-definition-file"></a><span data-ttu-id="35272-114">Creare un bilanciamento del carico tramite il file di definizione del servizio</span><span class="sxs-lookup"><span data-stu-id="35272-114">Create a load balancer using the service definition file</span></span>

<span data-ttu-id="35272-115">È possibile usare Azure SDK per .NET 2.5 per aggiornare il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="35272-115">You can leverage the Azure SDK for .NET 2.5 to update your cloud service.</span></span> <span data-ttu-id="35272-116">Le impostazioni degli endpoint per i servizi cloud vengono configurate nel file di [definizione del servizio](https://msdn.microsoft.com/library/azure/gg557553.aspx), con estensione csdef.</span><span class="sxs-lookup"><span data-stu-id="35272-116">Endpoint settings for cloud services are made in the [service definition](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef file.</span></span>

<span data-ttu-id="35272-117">L'esempio seguente mostra la configurazione di un file servicedefinition.csdef per una distribuzione cloud:</span><span class="sxs-lookup"><span data-stu-id="35272-117">The following example shows how a servicedefinition.csdef file for a cloud deployment is configured:</span></span>

<span data-ttu-id="35272-118">Analizzando il frammento di codice per il file con estensione csdef generato da una distribuzione cloud, è possibile vedere l'endpoint esterno configurato per usare le porte HTTP sulle porte 10000, 10001 e 10002.</span><span class="sxs-lookup"><span data-stu-id="35272-118">Checking the snippet for the .csdef file generated by a cloud deployment, you can see the external endpoint configured to use ports HTTP on port 10000, 10001, and 10002.</span></span>

```xml
<ServiceDefinition name=“Tenant“>
    <WorkerRole name=“FERole” vmsize=“Small“>
<Endpoints>
    <InputEndpoint name=“FE_External_Http” protocol=“http” port=“10000“ />
    <InputEndpoint name=“FE_External_Tcp“  protocol=“tcp“  port=“10001“ />
    <InputEndpoint name=“FE_External_Udp“  protocol=“udp“  port=“10002“ />

    <InputEndpointname=“HTTP_Probe” protocol=“http” port=“80” loadBalancerProbe=“MyProbe“ />

    <InstanceInputEndpoint name=“InstanceEP” protocol=“tcp” localPort=“80“>
        <AllocatePublicPortFrom>
            <FixedPortRange min=“10110” max=“10120“  />
        </AllocatePublicPortFrom>
    </InstanceInputEndpoint>
    <InternalEndpoint name=“FE_InternalEP_Tcp” protocol=“tcp“ />
</Endpoints>
    </WorkerRole>
</ServiceDefinition>
```

## <a name="check-load-balancer-health-status-for-cloud-services"></a><span data-ttu-id="35272-119">Controllo dello stato di integrità del servizio di bilanciamento del carico per i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="35272-119">Check load balancer health status for cloud services</span></span>

<span data-ttu-id="35272-120">Di seguito è riportato un esempio di probe di integrità:</span><span class="sxs-lookup"><span data-stu-id="35272-120">The following is an example of a health probe:</span></span>

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

<span data-ttu-id="35272-121">Il servizio di bilanciamento del carico combina le informazioni dell'endpoint e le informazioni del probe per creare un URL nel formato `http://{DIP of VM}:80/Probe.aspx`, che verrà usato per eseguire una query sull'integrità del servizio.</span><span class="sxs-lookup"><span data-stu-id="35272-121">The load balancer combines the information of the endpoint and the information of the probe to create a URL in the form of `http://{DIP of VM}:80/Probe.aspx` that can be used to query the health of the service.</span></span>

<span data-ttu-id="35272-122">Il servizio rileva probe periodiche dallo stesso indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="35272-122">The service detects periodic probes from the same IP address.</span></span> <span data-ttu-id="35272-123">Si tratta della richiesta del probe di integrità proveniente dall'host del nodo in cui è in esecuzione la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="35272-123">This is the health probe request coming from the host of the node where the virtual machine is running.</span></span> <span data-ttu-id="35272-124">Il servizio deve rispondere con un codice di stato HTTP 200 per indicare l'integrità al bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="35272-124">The service has to respond with a HTTP 200 status code for the load balancer to assume that the service is healthy.</span></span> <span data-ttu-id="35272-125">Qualsiasi altro codice di stato HTTP (ad esempio 503) esclude direttamente la macchina virtuale dalla rotazione.</span><span class="sxs-lookup"><span data-stu-id="35272-125">Any other HTTP status code (for example 503) directly takes the virtual machine out of rotation.</span></span>

<span data-ttu-id="35272-126">La definizione del probe ne controlla anche la frequenza.</span><span class="sxs-lookup"><span data-stu-id="35272-126">The probe definition also controls the frequency of the probe.</span></span> <span data-ttu-id="35272-127">Nel caso precedente, il bilanciamento del carico controlla l'endpoint tramite probe ogni 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="35272-127">In our case above, the load balancer is probing the endpoint every 5 secs.</span></span> <span data-ttu-id="35272-128">Se non viene ricevuta alcuna risposta positiva per 10 secondi (due intervalli di probe), si presuppone che il probe abbia avuto esito negativo e la macchina virtuale viene esclusa dalla rotazione.</span><span class="sxs-lookup"><span data-stu-id="35272-128">If no positive answer is received for 10 secs (two probe intervals), the probe is assumed down, and the virtual machine is taken out of rotation.</span></span> <span data-ttu-id="35272-129">Analogamente, se il servizio è escluso dalla rotazione e viene ricevuta una risposta positiva, il servizio viene immediatamente inserito di nuovo nella rotazione.</span><span class="sxs-lookup"><span data-stu-id="35272-129">Similarly, if the service is out of rotation and a positive answer is received, the service is put back to rotation right away.</span></span> <span data-ttu-id="35272-130">Se il servizio passa continuamente da uno stato integro a uno non integro, il servizio di bilanciamento del carico può decidere di ritardare la reintroduzione del servizio nella rotazione fino a quando non risulta integro per un determinato numero di probe.</span><span class="sxs-lookup"><span data-stu-id="35272-130">If the service is fluctuating between healthy and unhealthy, the load balancer can decide to delay the re-introduction of the service back to rotation until it has been healthy for a number of probes.</span></span>

<span data-ttu-id="35272-131">Per altre informazioni, fare riferimento allo schema di definizione del servizio per il [probe di integrità](https://msdn.microsoft.com/library/azure/jj151530.aspx) .</span><span class="sxs-lookup"><span data-stu-id="35272-131">Check the service definition schema for the [health probe](https://msdn.microsoft.com/library/azure/jj151530.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35272-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="35272-132">Next steps</span></span>

[<span data-ttu-id="35272-133">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="35272-133">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="35272-134">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="35272-134">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="35272-135">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="35272-135">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

