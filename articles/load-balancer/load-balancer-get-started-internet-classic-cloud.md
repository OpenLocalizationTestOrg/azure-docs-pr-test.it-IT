---
title: bilanciamento del carico aaaCreate con una connessione Internet per i servizi cloud di Azure | Documenti Microsoft
description: Informazioni su come una connessione Internet toocreate bilanciamento del carico in modello di distribuzione classica per i servizi cloud
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
ms.openlocfilehash: d93cf76d417cbfc744cf07ba48c43a63cc14df69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a><span data-ttu-id="3b7b0-103">Introduzione alla creazione del servizio di bilanciamento del carico Internet per i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="3b7b0-103">Get started creating an Internet facing load balancer for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3b7b0-104">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="3b7b0-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="3b7b0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b7b0-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="3b7b0-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="3b7b0-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="3b7b0-107">Servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="3b7b0-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="3b7b0-108">Prima di lavorare con le risorse di Azure, è importante toounderstand che Azure ha due modelli di distribuzione: Gestione risorse di Azure e classica.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="3b7b0-109">È importante comprendere i [modelli e strumenti di distribuzione](../azure-classic-rm.md) prima di lavorare con le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="3b7b0-110">È possibile visualizzare la documentazione di hello per diversi strumenti facendo clic sulle schede hello nella parte superiore di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="3b7b0-111">Questo articolo descrive il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="3b7b0-112">È anche possibile [informazioni su come una connessione Internet toocreate bilanciamento del carico con Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3b7b0-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

<span data-ttu-id="3b7b0-113">Servizi cloud vengono configurati automaticamente con un bilanciamento del carico e possono essere personalizzati tramite il modello di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-113">Cloud services are automatically configured with a load balancer and can be customized via hello service model.</span></span>

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a><span data-ttu-id="3b7b0-114">Creare un bilanciamento del carico utilizzando file di definizione del servizio hello</span><span class="sxs-lookup"><span data-stu-id="3b7b0-114">Create a load balancer using hello service definition file</span></span>

<span data-ttu-id="3b7b0-115">È possibile sfruttare hello Azure SDK per .NET 2.5 tooupdate il servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-115">You can leverage hello Azure SDK for .NET 2.5 tooupdate your cloud service.</span></span> <span data-ttu-id="3b7b0-116">Le impostazioni di endpoint per servizi cloud vengono eseguite in hello [definizione servizio](https://msdn.microsoft.com/library/azure/gg557553.aspx) file con estensione csdef.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-116">Endpoint settings for cloud services are made in hello [service definition](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef file.</span></span>

<span data-ttu-id="3b7b0-117">Hello esempio seguente viene illustrato come un file servicedefinition. csdef per una distribuzione cloud configurato:</span><span class="sxs-lookup"><span data-stu-id="3b7b0-117">hello following example shows how a servicedefinition.csdef file for a cloud deployment is configured:</span></span>

<span data-ttu-id="3b7b0-118">Controllo di frammento hello per file con estensione csdef hello generato da una distribuzione cloud, è possibile visualizzare hello endpoint esterno configurato toouse porte HTTP sulla porta 10000 e 10001 10002.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-118">Checking hello snippet for hello .csdef file generated by a cloud deployment, you can see hello external endpoint configured toouse ports HTTP on port 10000, 10001, and 10002.</span></span>

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

## <a name="check-load-balancer-health-status-for-cloud-services"></a><span data-ttu-id="3b7b0-119">Controllo dello stato di integrità del servizio di bilanciamento del carico per i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="3b7b0-119">Check load balancer health status for cloud services</span></span>

<span data-ttu-id="3b7b0-120">Hello Ecco un esempio di un probe di integrità:</span><span class="sxs-lookup"><span data-stu-id="3b7b0-120">hello following is an example of a health probe:</span></span>

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

<span data-ttu-id="3b7b0-121">Hello bilanciamento del carico combina hello informazioni dell'endpoint hello e hello di hello probe toocreate un URL nel formato hello `http://{DIP of VM}:80/Probe.aspx` che può essere utilizzato tooquery hello integrità del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-121">hello load balancer combines hello information of hello endpoint and hello information of hello probe toocreate a URL in hello form of `http://{DIP of VM}:80/Probe.aspx` that can be used tooquery hello health of hello service.</span></span>

<span data-ttu-id="3b7b0-122">servizio Hello rileva probe periodiche da hello stesso indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-122">hello service detects periodic probes from hello same IP address.</span></span> <span data-ttu-id="3b7b0-123">Si tratta di richiesta di probe di integrità hello provenienti dall'host di hello del nodo hello in cui è in esecuzione macchine virtuali di hello.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-123">This is hello health probe request coming from hello host of hello node where hello virtual machine is running.</span></span> <span data-ttu-id="3b7b0-124">servizio Hello è toorespond con codice di stato HTTP 200 per tooassume del servizio di bilanciamento carico di hello che servizio hello è integro.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-124">hello service has toorespond with a HTTP 200 status code for hello load balancer tooassume that hello service is healthy.</span></span> <span data-ttu-id="3b7b0-125">Qualsiasi altro tipo di stato HTTP (ad esempio 503) il codice direttamente accetta hello macchina virtuale dalla rotazione.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-125">Any other HTTP status code (for example 503) directly takes hello virtual machine out of rotation.</span></span>

<span data-ttu-id="3b7b0-126">definizione di tipo probe Hello controlla anche la frequenza di hello del probe hello.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-126">hello probe definition also controls hello frequency of hello probe.</span></span> <span data-ttu-id="3b7b0-127">In questo caso precedente, bilanciamento del carico hello è probing endpoint hello ogni 5 secondi.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-127">In our case above, hello load balancer is probing hello endpoint every 5 secs.</span></span> <span data-ttu-id="3b7b0-128">Se nessuna risposta positiva viene ricevuta per 10 secondi (due intervalli di probe), si presuppone che il probe hello verso il basso e macchina virtuale hello viene escluso dalla rotazione.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-128">If no positive answer is received for 10 secs (two probe intervals), hello probe is assumed down, and hello virtual machine is taken out of rotation.</span></span> <span data-ttu-id="3b7b0-129">Analogamente, se il servizio di hello è dalla rotazione e viene ricevuta una risposta positiva, servizio hello viene reinserita toorotation immediatamente.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-129">Similarly, if hello service is out of rotation and a positive answer is received, hello service is put back toorotation right away.</span></span> <span data-ttu-id="3b7b0-130">Se il servizio hello sta fluttuando. potete tra integro e non corretti, bilanciamento del carico hello può decidere reintroduzione hello toodelay di hello servizio back-toorotation fino a quando non è stato integro per un numero di probe.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-130">If hello service is fluctuating between healthy and unhealthy, hello load balancer can decide toodelay hello re-introduction of hello service back toorotation until it has been healthy for a number of probes.</span></span>

<span data-ttu-id="3b7b0-131">Verifica dello schema di definizione del servizio di hello per hello [probe di integrità](https://msdn.microsoft.com/library/azure/jj151530.aspx) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="3b7b0-131">Check hello service definition schema for hello [health probe](https://msdn.microsoft.com/library/azure/jj151530.aspx) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b7b0-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3b7b0-132">Next steps</span></span>

[<span data-ttu-id="3b7b0-133">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="3b7b0-133">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="3b7b0-134">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="3b7b0-134">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="3b7b0-135">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="3b7b0-135">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

