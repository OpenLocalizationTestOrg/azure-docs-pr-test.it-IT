---
title: aaaCreate un bilanciamento del carico interno per servizi Cloud di Azure | Documenti Microsoft
description: Informazioni su come toocreate un interno bilanciamento del carico con PowerShell nel modello di distribuzione classica hello
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: fe7975bca7bec3248626b0ad0fad6823e278ade2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a><span data-ttu-id="48080-103">Introduzione alla creazione di un servizio di bilanciamento del carico interno (classico) per i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="48080-103">Get started creating an internal load balancer (classic) for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="48080-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="48080-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="48080-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="48080-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="48080-106">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="48080-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> <span data-ttu-id="48080-107">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="48080-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="48080-108">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="48080-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="48080-109">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="48080-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="48080-110">Informazioni su come troppo[eseguire questi passaggi tramite il modello di gestione risorse di hello](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="48080-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

## <a name="configure-internal-load-balancer-for-cloud-services"></a><span data-ttu-id="48080-111">Configurare il servizio di bilanciamento del carico interno per i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="48080-111">Configure internal load balancer for cloud services</span></span>

<span data-ttu-id="48080-112">Il servizio di bilanciamento del carico interno è supportato sia per le macchine virtuali che per i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="48080-112">Internal load balancer is supported for both virtual machines and cloud services.</span></span> <span data-ttu-id="48080-113">Un endpoint di servizio di bilanciamento carico interno creato in un servizio cloud di fuori di una rete virtuale regionale sarà accessibile solo all'interno del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="48080-113">An internal load balancer endpoint created in a cloud service that is outside a regional virtual network will be accessible only within hello cloud service.</span></span>

<span data-ttu-id="48080-114">configurazione di bilanciamento del carico interno Hello è toobe impostato durante la creazione di hello di distribuzione prima di hello nel servizio cloud hello, come illustrato nell'esempio hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="48080-114">hello internal load balancer configuration has toobe set during hello creation of hello first deployment in hello cloud service, as shown in hello sample below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48080-115">Una procedura di hello toorun prerequisiti riportata di seguito è una rete virtuale già creata per la distribuzione cloud hello toohave.</span><span class="sxs-lookup"><span data-stu-id="48080-115">A prerequisite toorun hello steps below is toohave a virtual network already created for hello cloud deployment.</span></span> <span data-ttu-id="48080-116">Sarà necessario hello rete virtuale nome e la subnet nome toocreate hello bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="48080-116">You will need hello virtual network name and subnet name toocreate hello Internal Load Balancing.</span></span>

### <a name="step-1"></a><span data-ttu-id="48080-117">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="48080-117">Step 1</span></span>

<span data-ttu-id="48080-118">Aprire file di configurazione servizio hello (. cscfg) per la distribuzione cloud in Visual Studio e aggiungere hello seguente ultima sezione toocreate hello bilanciamento del carico interno in hello "`</Role>`" elemento di configurazione di rete hello.</span><span class="sxs-lookup"><span data-stu-id="48080-118">Open hello service configuration file (.cscfg) for your cloud deployment in Visual Studio and add hello following section toocreate hello Internal Load Balancing under hello last "`</Role>`" item for hello network configuration.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="48080-119">Aggiungere i valori hello per hello rete configurazione file tooshow l'aspetto.</span><span class="sxs-lookup"><span data-stu-id="48080-119">Let's add hello values for hello network configuration file tooshow how it will look.</span></span> <span data-ttu-id="48080-120">Nell'esempio di hello si supponga che creare una rete virtuale denominata "test_vnet" con un 10.0.0.0/24 subnet denominata test_subnet e un indirizzo IP statico 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="48080-120">In hello example, assume you created a VNet called "test_vnet" with a subnet 10.0.0.0/24 called test_subnet and a static IP 10.0.0.4.</span></span> <span data-ttu-id="48080-121">servizio di bilanciamento del carico Hello verrà denominato testLB.</span><span class="sxs-lookup"><span data-stu-id="48080-121">hello load balancer will be named testLB.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="48080-122">Per ulteriori informazioni sullo schema di bilanciamento carico di hello, vedere [Aggiungi servizio di bilanciamento del carico](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span><span class="sxs-lookup"><span data-stu-id="48080-122">For more information about hello load balancer schema, see [Add load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span></span>

### <a name="step-2"></a><span data-ttu-id="48080-123">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="48080-123">Step 2</span></span>

<span data-ttu-id="48080-124">Modificare gli endpoint hello servizio definizione (con estensione csdef) file tooadd toohello con bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="48080-124">Change hello service definition (.csdef) file tooadd endpoints toohello Internal Load Balancing.</span></span> <span data-ttu-id="48080-125">momento di Hello viene creata un'istanza del ruolo, file di definizione del servizio hello aggiungerà hello toohello di istanze di ruolo bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="48080-125">hello moment a role instance is created, hello service definition file will add hello role instances toohello Internal Load Balancing.</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="48080-126">In seguito hello stesso valori nell'esempio hello precedente, aggiungere file di definizione del servizio toohello valori hello.</span><span class="sxs-lookup"><span data-stu-id="48080-126">Following hello same values from hello example above, let's add hello values toohello service definition file.</span></span>

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="48080-127">il traffico di rete Hello sarà con carico bilanciato con bilanciamento del carico di testLB hello utilizza la porta 80 per le richieste in ingresso, l'invio di tooworker le istanze del ruolo anche sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="48080-127">hello network traffic will be load balanced using hello testLB load balancer using port 80 for incoming requests, sending tooworker role instances also on port 80.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48080-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="48080-128">Next steps</span></span>

[<span data-ttu-id="48080-129">Configurare una modalità di distribuzione del servizio di bilanciamento del carico utilizzando l’affinità dell’IP di origine</span><span class="sxs-lookup"><span data-stu-id="48080-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="48080-130">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="48080-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

