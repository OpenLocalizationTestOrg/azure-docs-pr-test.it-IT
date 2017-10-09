---
title: un uso interno aaaCreate bilanciamento del carico - CLI di Azure classico | Documenti Microsoft
description: Informazioni su come un servizio di bilanciamento carico interno utilizzando toocreate hello CLI di Azure nel modello di distribuzione classica hello
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: becbbbde-a118-4269-9444-d3153f00bf34
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: ef29dfda5f7a75a411bbabe8b688a31c6bf81113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a><span data-ttu-id="68c03-103">Introduzione alla creazione di un bilanciamento del carico interno (classico) utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="68c03-103">Get started creating an internal load balancer (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="68c03-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68c03-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="68c03-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="68c03-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="68c03-106">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="68c03-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="68c03-107">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="68c03-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="68c03-108">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="68c03-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="68c03-109">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="68c03-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="68c03-110">Informazioni su come troppo[eseguire questi passaggi tramite il modello di gestione risorse di hello](load-balancer-get-started-ilb-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="68c03-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="68c03-111">toocreate un bilanciamento del carico interno è impostato per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="68c03-111">toocreate an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="68c03-112">toocreate un bilanciamento del carico interno impostato e hello server che invierà i tooit di traffico, è necessario eseguire il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="68c03-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you must do hello following:</span></span>

1. <span data-ttu-id="68c03-113">Creare un'istanza interna il bilanciamento del carico che fungerà da endpoint hello in arrivo traffico toobe con bilanciato del carico tra i server hello di un set con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="68c03-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="68c03-114">Aggiungere gli endpoint corrispondenti toohello le macchine virtuali che riceveranno il traffico in ingresso hello.</span><span class="sxs-lookup"><span data-stu-id="68c03-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="68c03-115">Configurare i server hello che invieranno hello traffico toobe con bilanciamento del carico toosend loro traffico toohello indirizzo IP virtuale (VIP) dell'istanza di hello interno il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="68c03-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a><span data-ttu-id="68c03-116">Procedura dettagliata sulla creazione di un servizio di bilanciamento del carico interno tramite CLI</span><span class="sxs-lookup"><span data-stu-id="68c03-116">Step by step creating an internal load balancer using CLI</span></span>

<span data-ttu-id="68c03-117">Questa guida viene spiegato come toocreate un bilanciamento del carico interno in base a hello scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="68c03-117">This guide shows how toocreate an internal load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="68c03-118">Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="68c03-118">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="68c03-119">Eseguire hello **modalità di configurazione azure** comando tooswitch tooclassic modalità come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="68c03-119">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="68c03-120">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="68c03-120">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="68c03-121">Creazione dell’endpoint e del set del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="68c03-121">Create endpoint and load balancer set</span></span>

<span data-ttu-id="68c03-122">scenario di Hello presuppone hello macchine "DB1" e "DB2" in un servizio cloud denominato "mytestcloud".</span><span class="sxs-lookup"><span data-stu-id="68c03-122">hello scenario assumes hello virtual machines "DB1" and "DB2" in a cloud service called "mytestcloud".</span></span> <span data-ttu-id="68c03-123">Entrambe le macchine virtuali utilizzano una rete virtuale denominata "my testvnet" con subnet "subnet-1".</span><span class="sxs-lookup"><span data-stu-id="68c03-123">Both virtual machines are using a virtual network called my "testvnet" with subnet "subnet-1".</span></span>

<span data-ttu-id="68c03-124">In questa guida verrà creato un set del servizio di bilanciamento del carico interno utilizzando la porta 1433 come porta privata e la porta 1433 come porta locale.</span><span class="sxs-lookup"><span data-stu-id="68c03-124">This guide will create an internal load balancer set using port 1433 as private port and 1433 as local port.</span></span>

<span data-ttu-id="68c03-125">Si tratta di uno scenario comune in cui si dispone di macchine virtuali SQL hello back-end utilizzando che un server di database hello tooguarantee bilanciamento di carico interno non verrà esposto direttamente tramite un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="68c03-125">This is a common scenario where you have SQL virtual machines on hello back end using an internal load balancer tooguarantee hello database servers won't be exposed directly using a public IP address.</span></span>

### <a name="step-1"></a><span data-ttu-id="68c03-126">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="68c03-126">Step 1</span></span>

<span data-ttu-id="68c03-127">Creare un set di bilanciamento del carico interno utilizzando `azure network service internal-load-balancer add`.</span><span class="sxs-lookup"><span data-stu-id="68c03-127">Create an internal load balancer set using `azure network service internal-load-balancer add`.</span></span>

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

<span data-ttu-id="68c03-128">Per ulteriori informazioni, vedere `azure service internal-load-balancer --help` .</span><span class="sxs-lookup"><span data-stu-id="68c03-128">Check out `azure service internal-load-balancer --help` for more information.</span></span>

<span data-ttu-id="68c03-129">È possibile controllare le proprietà del servizio di bilanciamento di carico interno hello comando hello `azure service internal-load-balancer list` *nome del servizio cloud*.</span><span class="sxs-lookup"><span data-stu-id="68c03-129">You can check hello internal load balancer properties using hello command `azure service internal-load-balancer list` *cloud service name*.</span></span>

<span data-ttu-id="68c03-130">Di seguito segue un esempio di output di hello:</span><span class="sxs-lookup"><span data-stu-id="68c03-130">Here follows an example of hello output:</span></span>

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a><span data-ttu-id="68c03-131">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="68c03-131">Step 2</span></span>

<span data-ttu-id="68c03-132">Configurare un bilanciamento del carico interno hello impostata quando si aggiungono endpoint prima di hello.</span><span class="sxs-lookup"><span data-stu-id="68c03-132">You configure hello internal load balancer set when you add hello first endpoint.</span></span> <span data-ttu-id="68c03-133">Associare hello endpoint, macchina virtuale e un probe porta toohello bilanciamento del carico interno impostato in questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="68c03-133">You will associate hello endpoint, virtual machine and probe port toohello internal load balancer set in this step.</span></span>

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a><span data-ttu-id="68c03-134">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="68c03-134">Step 3</span></span>

<span data-ttu-id="68c03-135">Verificare tramite configurazione del servizio di bilanciamento carico di hello `azure vm show` *nome della macchina virtuale*</span><span class="sxs-lookup"><span data-stu-id="68c03-135">Verify hello load balancer configuration using `azure vm show` *virtual machine name*</span></span>

```azurecli
azure vm show DB1
```

<span data-ttu-id="68c03-136">output di Hello sarà:</span><span class="sxs-lookup"><span data-stu-id="68c03-136">hello output will be:</span></span>

    azure vm show DB1
    info:    Executing command vm show
    + Getting virtual machines
    data:    DNSName "mytestcloud.cloudapp.net"
    data:    Location "East US 2"
    data:    VMName "DB1"
    data:    IPAddress "192.168.2.4"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "db1-DB1-0-201511120457370846"
    data:    OSDisk mediaLink "https://XXXX.blob.core.windows.net/vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "137.116.64.107"
    data:    VirtualIPAddresses 0 name "db1ContractContract"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    VirtualIPAddresses 1 address "192.168.2.7"
    data:    VirtualIPAddresses 1 name "ilbset"
    data:    Network Endpoints 0 localPort 5986
    data:    Network Endpoints 0 name "PowerShell"
    data:    Network Endpoints 0 port 5986
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 3389
    data:    Network Endpoints 1 name "Remote Desktop"
    data:    Network Endpoints 1 port 60173
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 1433
    data:    Network Endpoints 2 name "tcp-1433-1433"
    data:    Network Endpoints 2 port 1433
    data:    Network Endpoints 2 loadBalancerProbe port 1433
    data:    Network Endpoints 2 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 2 loadBalancerProbe intervalInSeconds 300
    data:    Network Endpoints 2 loadBalancerProbe timeoutInSeconds 600
    data:    Network Endpoints 2 protocol "tcp"
    data:    Network Endpoints 2 virtualIPAddress "192.168.2.7"
    data:    Network Endpoints 2 enableDirectServerReturn false
    data:    Network Endpoints 2 loadBalancerName "ilbset"
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="68c03-137">Creare un endpoint di desktop remoto per una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="68c03-137">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="68c03-138">È possibile creare un traffico di rete tooforward endpoint desktop remoto da una porta locale tooa di porta pubblica per l'utilizzo di una macchina virtuale specifica `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="68c03-138">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="68c03-139">Rimuovere la macchina virtuale dal servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="68c03-139">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="68c03-140">È possibile rimuovere una macchina virtuale da un bilanciamento del carico interno impostato tramite l'eliminazione di endpoint hello associata.</span><span class="sxs-lookup"><span data-stu-id="68c03-140">You can remove a virtual machine from an internal load balancer set by deleting hello associated endpoint.</span></span> <span data-ttu-id="68c03-141">Dopo la rimozione di endpoint hello, macchina virtuale hello non appartengono a bilanciamento del carico toohello imposta più.</span><span class="sxs-lookup"><span data-stu-id="68c03-141">Once hello endpoint is removed, hello virtual machine won't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="68c03-142">Utilizzando l'esempio hello precedente, è possibile rimuovere endpoint hello creato per la macchina virtuale "DB1" dal servizio di bilanciamento del carico interno "ilbset" utilizzando il comando hello `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="68c03-142">Using hello example above, you can remove hello endpoint created for virtual machine "DB1" from internal load balancer "ilbset" by using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

<span data-ttu-id="68c03-143">Per ulteriori informazioni, vedere `azure vm endpoint --help` .</span><span class="sxs-lookup"><span data-stu-id="68c03-143">Check out `azure vm endpoint --help` for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68c03-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="68c03-144">Next steps</span></span>

[<span data-ttu-id="68c03-145">Configurare una modalità di distribuzione del servizio di bilanciamento del carico utilizzando l’affinità dell’IP di origine</span><span class="sxs-lookup"><span data-stu-id="68c03-145">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="68c03-146">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="68c03-146">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
