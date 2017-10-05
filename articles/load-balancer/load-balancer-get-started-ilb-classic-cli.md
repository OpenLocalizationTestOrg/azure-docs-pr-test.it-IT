---
title: Creare un servizio di bilanciamento del carico interno - Interfaccia della riga di comando di Azure (versione classica) | Documentazione Microsoft
description: "Informazioni su come creare un servizio di bilanciamento del carico interno usando l’interfaccia della riga di comando di Azure nel modello di distribuzione classica"
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
ms.openlocfilehash: d24b95f75b5ffd1116b07cf9f8bac33767a9c835
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-the-azure-cli"></a><span data-ttu-id="32552-103">Introduzione alla creazione di un servizio di bilanciamento del carico interno (classico) tramite l’interfaccia di riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="32552-103">Get started creating an internal load balancer (classic) using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="32552-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="32552-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="32552-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="32552-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="32552-106">Servizi cloud</span><span class="sxs-lookup"><span data-stu-id="32552-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="32552-107">Azure offre due modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="32552-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="32552-108">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="32552-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="32552-109">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="32552-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="32552-110">Informazioni su come [eseguire questa procedura con il modello di Resource Manager](load-balancer-get-started-ilb-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="32552-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="to-create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="32552-111">Per creare un set con servizio di bilanciamento del carico interno per le macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="32552-111">To create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="32552-112">Per creare un set con servizio di bilanciamento del carico e i server che invieranno il traffico a esso, è necessario eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="32552-112">To create an internal load balancer set and the servers that will send their traffic to it, you must do the following:</span></span>

1. <span data-ttu-id="32552-113">Creare un'istanza della funzionalità di bilanciamento del carico interno che sarà l'endpoint del traffico in ingresso da configurare con carico bilanciato tra i server di un set con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="32552-113">Create an instance of Internal Load Balancing that will be the endpoint of incoming traffic to be load balanced across the servers of a load-balanced set.</span></span>
2. <span data-ttu-id="32552-114">Aggiungere gli endpoint corrispondenti alle macchine virtuali che riceveranno il traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="32552-114">Add endpoints corresponding to the virtual machines that will be receiving the incoming traffic.</span></span>
3. <span data-ttu-id="32552-115">Configurare i server che invieranno il traffico con carico bilanciato all'indirizzo IP virtuale (indirizzo VIP) dell'istanza del bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="32552-115">Configure the servers that will be sending the traffic to be load balanced to send their traffic to the virtual IP (VIP) address of the Internal Load Balancing instance.</span></span>

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a><span data-ttu-id="32552-116">Procedura dettagliata sulla creazione di un servizio di bilanciamento del carico interno tramite CLI</span><span class="sxs-lookup"><span data-stu-id="32552-116">Step by step creating an internal load balancer using CLI</span></span>

<span data-ttu-id="32552-117">In questa guida viene illustrato come creare un servizio di bilanciamento del carico interno in base allo scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="32552-117">This guide shows how to create an internal load balancer based on the scenario above.</span></span>

1. <span data-ttu-id="32552-118">Se l'interfaccia della riga di comando di Azure non è mai stata usata, vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md) e seguire le istruzioni fino al punto in cui si selezionano l'account e la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="32552-118">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="32552-119">Eseguire il comando **azure config mode** per passare alla modalità classica, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="32552-119">Run the **azure config mode** command to switch to classic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="32552-120">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="32552-120">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="32552-121">Creazione dell’endpoint e del set del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="32552-121">Create endpoint and load balancer set</span></span>

<span data-ttu-id="32552-122">Lo scenario presuppone le macchine virtuali "DB1" e "DB2" in un servizio cloud denominato "mytestcloud".</span><span class="sxs-lookup"><span data-stu-id="32552-122">The scenario assumes the virtual machines "DB1" and "DB2" in a cloud service called "mytestcloud".</span></span> <span data-ttu-id="32552-123">Entrambe le macchine virtuali utilizzano una rete virtuale denominata "my testvnet" con subnet "subnet-1".</span><span class="sxs-lookup"><span data-stu-id="32552-123">Both virtual machines are using a virtual network called my "testvnet" with subnet "subnet-1".</span></span>

<span data-ttu-id="32552-124">In questa guida verrà creato un set del servizio di bilanciamento del carico interno utilizzando la porta 1433 come porta privata e la porta 1433 come porta locale.</span><span class="sxs-lookup"><span data-stu-id="32552-124">This guide will create an internal load balancer set using port 1433 as private port and 1433 as local port.</span></span>

<span data-ttu-id="32552-125">Si tratta di uno scenario comune in cui si dispone di macchine virtuali di SQL nel back-end che utilizzano un servizio di bilanciamento del carico interno per garantire che i server di database non siano esposti direttamente tramite un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="32552-125">This is a common scenario where you have SQL virtual machines on the back end using an internal load balancer to guarantee the database servers won't be exposed directly using a public IP address.</span></span>

### <a name="step-1"></a><span data-ttu-id="32552-126">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="32552-126">Step 1</span></span>

<span data-ttu-id="32552-127">Creare un set di bilanciamento del carico interno utilizzando `azure network service internal-load-balancer add`.</span><span class="sxs-lookup"><span data-stu-id="32552-127">Create an internal load balancer set using `azure network service internal-load-balancer add`.</span></span>

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

<span data-ttu-id="32552-128">Per ulteriori informazioni, vedere `azure service internal-load-balancer --help` .</span><span class="sxs-lookup"><span data-stu-id="32552-128">Check out `azure service internal-load-balancer --help` for more information.</span></span>

<span data-ttu-id="32552-129">È possibile controllare le proprietà del servizio di bilanciamento del carico interno utilizzando il comando `azure service internal-load-balancer list` *nome del servizio cloud*.</span><span class="sxs-lookup"><span data-stu-id="32552-129">You can check the internal load balancer properties using the command `azure service internal-load-balancer list` *cloud service name*.</span></span>

<span data-ttu-id="32552-130">Qui di seguito un esempio di output:</span><span class="sxs-lookup"><span data-stu-id="32552-130">Here follows an example of the output:</span></span>

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a><span data-ttu-id="32552-131">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="32552-131">Step 2</span></span>

<span data-ttu-id="32552-132">Configurare il set di bilanciamento del carico interno quando si aggiunge il primo endpoint.</span><span class="sxs-lookup"><span data-stu-id="32552-132">You configure the internal load balancer set when you add the first endpoint.</span></span> <span data-ttu-id="32552-133">Associare l'endpoint, la macchina virtuale e la porta probe per il set di bilanciamento del carico interno in questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="32552-133">You will associate the endpoint, virtual machine and probe port to the internal load balancer set in this step.</span></span>

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a><span data-ttu-id="32552-134">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="32552-134">Step 3</span></span>

<span data-ttu-id="32552-135">Verificare la configurazione del servizio di bilanciamento del carico utilizzando `azure vm show` *nome macchina virtuale*</span><span class="sxs-lookup"><span data-stu-id="32552-135">Verify the load balancer configuration using `azure vm show` *virtual machine name*</span></span>

```azurecli
azure vm show DB1
```

<span data-ttu-id="32552-136">L'output sarà:</span><span class="sxs-lookup"><span data-stu-id="32552-136">The output will be:</span></span>

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

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="32552-137">Creare un endpoint di desktop remoto per una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="32552-137">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="32552-138">È possibile creare un endpoint di desktop remoto per inoltrare il traffico di rete da una porta pubblica a una porta locale per una macchina virtuale specifica utilizzando `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="32552-138">You can create a remote desktop endpoint to forward network traffic from a public port to a local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="32552-139">Rimuovere la macchina virtuale dal servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="32552-139">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="32552-140">È possibile rimuovere una macchina virtuale da un set di bilanciamento del carico interno impostato eliminando l'endpoint associato.</span><span class="sxs-lookup"><span data-stu-id="32552-140">You can remove a virtual machine from an internal load balancer set by deleting the associated endpoint.</span></span> <span data-ttu-id="32552-141">Una volta rimosso l'endpoint, la macchina virtuale non appartiene più al set del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="32552-141">Once the endpoint is removed, the virtual machine won't belong to the load balancer set anymore.</span></span>

<span data-ttu-id="32552-142">Utilizzando l'esempio precedente, è possibile rimuovere l'endpoint creato per la macchina virtuale "DB1" dal servizio di bilanciamento del carico interno "ilbset" utilizzando il comando `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="32552-142">Using the example above, you can remove the endpoint created for virtual machine "DB1" from internal load balancer "ilbset" by using the command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

<span data-ttu-id="32552-143">Per ulteriori informazioni, vedere `azure vm endpoint --help` .</span><span class="sxs-lookup"><span data-stu-id="32552-143">Check out `azure vm endpoint --help` for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32552-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="32552-144">Next steps</span></span>

[<span data-ttu-id="32552-145">Configurare una modalità di distribuzione del servizio di bilanciamento del carico utilizzando l’affinità dell’IP di origine</span><span class="sxs-lookup"><span data-stu-id="32552-145">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="32552-146">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="32552-146">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
