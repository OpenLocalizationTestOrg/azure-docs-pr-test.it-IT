---
title: Creare un servizio di bilanciamento del carico interno per Servizi cloud di Azure | Documentazione Microsoft
description: Informazioni su come creare un servizio di bilanciamento del carico interno usando PowerShell nel modello di distribuzione classica
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
ms.openlocfilehash: 8dbc951416d577fa7f534c2eab1605c6bee61fce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a><span data-ttu-id="95a0d-103">Introduzione alla creazione di un servizio di bilanciamento del carico interno (classico) per i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="95a0d-103">Get started creating an internal load balancer (classic) for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="95a0d-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="95a0d-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="95a0d-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="95a0d-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="95a0d-106">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="95a0d-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> <span data-ttu-id="95a0d-107">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="95a0d-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="95a0d-108">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="95a0d-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="95a0d-109">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="95a0d-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="95a0d-110">Informazioni su come [eseguire questa procedura con il modello di Resource Manager](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="95a0d-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

## <a name="configure-internal-load-balancer-for-cloud-services"></a><span data-ttu-id="95a0d-111">Configurare il servizio di bilanciamento del carico interno per i servizi cloud</span><span class="sxs-lookup"><span data-stu-id="95a0d-111">Configure internal load balancer for cloud services</span></span>

<span data-ttu-id="95a0d-112">Il servizio di bilanciamento del carico interno è supportato sia per le macchine virtuali che per i servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="95a0d-112">Internal load balancer is supported for both virtual machines and cloud services.</span></span> <span data-ttu-id="95a0d-113">Un endpoint del servizio di bilanciamento del carico interno creato in un servizio cloud esterno a una rete virtuale dell'area sarà accessibile solo nel servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="95a0d-113">An internal load balancer endpoint created in a cloud service that is outside a regional virtual network will be accessible only within the cloud service.</span></span>

<span data-ttu-id="95a0d-114">La configurazione del servizio di bilanciamento del carico interno deve essere impostata durante la creazione della prima distribuzione nel servizio cloud, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="95a0d-114">The internal load balancer configuration has to be set during the creation of the first deployment in the cloud service, as shown in the sample below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="95a0d-115">Come prerequisito per eseguire i passaggi seguenti, è necessario avere già creato una rete virtuale per la distribuzione cloud.</span><span class="sxs-lookup"><span data-stu-id="95a0d-115">A prerequisite to run the steps below is to have a virtual network already created for the cloud deployment.</span></span> <span data-ttu-id="95a0d-116">Per creare il bilanciamento del carico interno, saranno necessari il nome della rete virtuale e il nome della subnet.</span><span class="sxs-lookup"><span data-stu-id="95a0d-116">You will need the virtual network name and subnet name to create the Internal Load Balancing.</span></span>

### <a name="step-1"></a><span data-ttu-id="95a0d-117">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="95a0d-117">Step 1</span></span>

<span data-ttu-id="95a0d-118">Aprire il file di configurazione del servizio (.cscfg) per la distribuzione cloud in Visual Studio e aggiungere la sezione seguente per creare il bilanciamento del carico interno sotto l'ultimo elemento "`</Role>`" per la configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="95a0d-118">Open the service configuration file (.cscfg) for your cloud deployment in Visual Studio and add the following section to create the Internal Load Balancing under the last "`</Role>`" item for the network configuration.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of the load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="95a0d-119">Vengono aggiunti i valori per il file di configurazione di rete per mostrare come apparirà.</span><span class="sxs-lookup"><span data-stu-id="95a0d-119">Let's add the values for the network configuration file to show how it will look.</span></span> <span data-ttu-id="95a0d-120">Nell'esempio, si supponga di aver creato una rete virtuale denominata "test_vnet" con una subnet 10.0.0.0/24 denominata test_subnet e un indirizzo IP statico 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="95a0d-120">In the example, assume you created a VNet called "test_vnet" with a subnet 10.0.0.0/24 called test_subnet and a static IP 10.0.0.4.</span></span> <span data-ttu-id="95a0d-121">Il servizio di bilanciamento del carico si chiamerà testLB.</span><span class="sxs-lookup"><span data-stu-id="95a0d-121">The load balancer will be named testLB.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="95a0d-122">Per altre informazioni sullo schema di bilanciamento del carico, vedere [Aggiungere il servizio di bilanciamento del carico](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span><span class="sxs-lookup"><span data-stu-id="95a0d-122">For more information about the load balancer schema, see [Add load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span></span>

### <a name="step-2"></a><span data-ttu-id="95a0d-123">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="95a0d-123">Step 2</span></span>

<span data-ttu-id="95a0d-124">Modificare il file di definizione del servizio (.csdef) per aggiungere endpoint al bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="95a0d-124">Change the service definition (.csdef) file to add endpoints to the Internal Load Balancing.</span></span> <span data-ttu-id="95a0d-125">Non appena viene creata un'istanza del ruolo, il file di definizione del servizio aggiunge le istanze del ruolo al bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="95a0d-125">The moment a role instance is created, the service definition file will add the role instances to the Internal Load Balancing.</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="95a0d-126">Usando gli stessi valori dell'esempio precedente, vengono aggiunti i valori al file di definizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="95a0d-126">Following the same values from the example above, let's add the values to the service definition file.</span></span>

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="95a0d-127">Il traffico di rete verrà configurato per il bilanciamento del carico tramite il servizio di bilanciamento del carico testLB, usando la porta 80 per le richieste in ingresso e anche per l'invio alle istanze del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="95a0d-127">The network traffic will be load balanced using the testLB load balancer using port 80 for incoming requests, sending to worker role instances also on port 80.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95a0d-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="95a0d-128">Next steps</span></span>

[<span data-ttu-id="95a0d-129">Configurare una modalità di distribuzione del servizio di bilanciamento del carico utilizzando l’affinità dell’IP di origine</span><span class="sxs-lookup"><span data-stu-id="95a0d-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="95a0d-130">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="95a0d-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

