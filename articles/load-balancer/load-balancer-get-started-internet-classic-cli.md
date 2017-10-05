---
title: Creare un servizio di bilanciamento del carico con connessione Internet - Interfaccia della riga di comando di Azure classica | Documentazione Microsoft
description: Informazioni su come creare un servizio di bilanciamento del carico Internet nel modello di distribuzione classica mediante l'interfaccia della riga di comando di Azure
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: e433a824-4a8a-44d2-8765-a74f52d4e584
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: da3a908f17ff5c6d3923549a884ecc0a13cb8e9e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-the-azure-cli"></a><span data-ttu-id="fdae3-103">Introduzione alla creazione del servizio di bilanciamento del carico Internet (classico) nell’interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="fdae3-103">Get started creating an Internet facing load balancer (classic) in the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fdae3-104">Portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="fdae3-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="fdae3-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fdae3-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="fdae3-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="fdae3-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="fdae3-107">Servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="fdae3-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="fdae3-108">Prima di iniziare a usare le risorse di Azure, è importante comprendere che Azure al momento offre due modelli di distribuzione, la distribuzione classica e Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fdae3-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="fdae3-109">È importante comprendere i [modelli e strumenti di distribuzione](../azure-classic-rm.md) prima di lavorare con le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="fdae3-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="fdae3-110">È possibile visualizzare la documentazione relativa a diversi strumenti facendo clic sulle schede nella parte superiore di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="fdae3-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="fdae3-111">In questo articolo viene illustrato il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="fdae3-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="fdae3-112">Vedere [Informazioni su come creare un servizio di bilanciamento del carico Internet in Gestione risorse di Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="fdae3-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a><span data-ttu-id="fdae3-113">Procedura dettagliata sulla creazione di un servizio di bilanciamento del carico Internet tramite CLI</span><span class="sxs-lookup"><span data-stu-id="fdae3-113">Step by step creating an Internet facing load balancer using CLI</span></span>

<span data-ttu-id="fdae3-114">In questa guida viene illustrato come creare un servizio di bilanciamento del carico Internet in base allo scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="fdae3-114">This guide shows how to create an Internet load balancer based on the scenario above.</span></span>

1. <span data-ttu-id="fdae3-115">Se l'interfaccia della riga di comando di Azure non è mai stata usata, vedere [Installare e configurare l'interfaccia della riga di comando di Azure](../cli-install-nodejs.md) e seguire le istruzioni fino al punto in cui si selezionano l'account e la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fdae3-115">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="fdae3-116">Eseguire il comando **azure config mode** per passare alla modalità classica, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="fdae3-116">Run the **azure config mode** command to switch to classic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="fdae3-117">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="fdae3-117">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="fdae3-118">Creazione dell’endpoint e del set del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="fdae3-118">Create endpoint and load balancer set</span></span>

<span data-ttu-id="fdae3-119">Lo scenario presuppone che le macchine virtuali "web1" e "web2" sono state create.</span><span class="sxs-lookup"><span data-stu-id="fdae3-119">The scenario assumes the virtual machines "web1" and "web2" were created.</span></span>
<span data-ttu-id="fdae3-120">In questa guida verrà creato un set del servizio di bilanciamento del carico utilizzando la porta 80 come porta pubblica e la porta 80 come porta locale.</span><span class="sxs-lookup"><span data-stu-id="fdae3-120">This guide will create a load balancer set using port 80 as public port and port 80 as local port.</span></span> <span data-ttu-id="fdae3-121">Una porta probe è inoltre stata configurata sulla porta 80 e il set del servizio di bilanciamento del carico è stato chiamato "lbset".</span><span class="sxs-lookup"><span data-stu-id="fdae3-121">A probe port is also configured on port 80 and named the load balancer set "lbset".</span></span>

### <a name="step-1"></a><span data-ttu-id="fdae3-122">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="fdae3-122">Step 1</span></span>

<span data-ttu-id="fdae3-123">Creare il primo endpoint e il set del servizio di bilanciamento del carico utilizzando `azure network vm endpoint create` per la macchina virtuale "web1".</span><span class="sxs-lookup"><span data-stu-id="fdae3-123">Create the first endpoint and load balancer set using `azure network vm endpoint create` for virtual machine "web1".</span></span>

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a><span data-ttu-id="fdae3-124">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="fdae3-124">Step 2</span></span>

<span data-ttu-id="fdae3-125">Aggiungere una seconda macchina virtuale "web2" al set del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="fdae3-125">Add a second virtual machine "web2" to the load balancer set.</span></span>

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a><span data-ttu-id="fdae3-126">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="fdae3-126">Step 3</span></span>

<span data-ttu-id="fdae3-127">Verificare la configurazione del servizio di bilanciamento del carico utilizzando `azure vm show` .</span><span class="sxs-lookup"><span data-stu-id="fdae3-127">Verify the load balancer configuration using `azure vm show` .</span></span>

```azurecli
azure vm show web1
```

<span data-ttu-id="fdae3-128">L'output sarà:</span><span class="sxs-lookup"><span data-stu-id="fdae3-128">The output will be:</span></span>

    data:    DNSName "contoso.cloudapp.net"
    data:    Location "East US"
    data:    VMName "web1"
    data:    IPAddress "10.0.0.5"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-2015
    6-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "joaoma-1-web1-0-201509251804250879"
    data:    OSDisk mediaLink "https://XXXXXXXXXXXXXXX.blob.core.windows.
    /vhds/joaomatest-web1-2015-09-25.vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Se
    r-2012-R2-20150916-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "XXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 name "XXXXXXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    Network Endpoints 0 loadBalancedEndpointSetName "lbset"
    data:    Network Endpoints 0 localPort 80
    data:    Network Endpoints 0 name "tcp-80-80"
    data:    Network Endpoints 0 port 80
    data:    Network Endpoints 0 loadBalancerProbe port 80
    data:    Network Endpoints 0 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 0 loadBalancerProbe intervalInSeconds 15
    data:    Network Endpoints 0 loadBalancerProbe timeoutInSeconds 31
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 5986
    data:    Network Endpoints 1 name "PowerShell"
    data:    Network Endpoints 1 port 5986
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 3389
    data:    Network Endpoints 2 name "Remote Desktop"
    data:    Network Endpoints 2 port 58081
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="fdae3-129">Creare un endpoint di desktop remoto per una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fdae3-129">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="fdae3-130">È possibile creare un endpoint di desktop remoto per inoltrare il traffico di rete da una porta pubblica a una porta locale per una macchina virtuale specifica utilizzando `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="fdae3-130">You can create a remote desktop endpoint to forward network traffic from a public port to a local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="fdae3-131">Rimuovere la macchina virtuale dal servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="fdae3-131">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="fdae3-132">È necessario eliminare l'endpoint associato al set del servizio di bilanciamento del carico impostato dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fdae3-132">You have to delete the endpoint associated to the load balancer set from the virtual machine.</span></span> <span data-ttu-id="fdae3-133">Una volta rimosso l'endpoint, la macchina virtuale non appartiene più al set del servizio di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="fdae3-133">Once the endpoint is removed, the virtual machine doesn't belong to the load balancer set anymore.</span></span>

<span data-ttu-id="fdae3-134">Utilizzando l'esempio precedente, è possibile rimuovere l'endpoint creato per la macchina virtuale "web1" dal servizio di bilanciamento del carico "lbset" utilizzando il comando `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="fdae3-134">Using the example above, you can remove the endpoint created for virtual machine "web1" from load balancer "lbset" using the command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> <span data-ttu-id="fdae3-135">È possibile esplorare più opzioni per gestire gli endpoint utilizzando il comando `azure vm endpoint --help`</span><span class="sxs-lookup"><span data-stu-id="fdae3-135">You can explore more options to manage endpoints using the command `azure vm endpoint --help`</span></span>

## <a name="next-steps"></a><span data-ttu-id="fdae3-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fdae3-136">Next steps</span></span>

[<span data-ttu-id="fdae3-137">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="fdae3-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="fdae3-138">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="fdae3-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="fdae3-139">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="fdae3-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
