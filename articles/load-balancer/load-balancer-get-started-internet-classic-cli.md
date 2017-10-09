---
title: con una connessione Internet aaaCreate bilanciamento del carico - CLI di Azure classico | Documenti Microsoft
description: Informazioni su come toocreate un Internet rivolto al bilanciamento del carico in modello di distribuzione classica utilizzando hello CLI di Azure
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
ms.openlocfilehash: e6070cbc574f74bca0cccb960ff192847d6511bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-cli"></a><span data-ttu-id="4dba5-103">Introduzione alla creazione di un bilanciamento del carico (classico) in hello CLI di Azure per Internet</span><span class="sxs-lookup"><span data-stu-id="4dba5-103">Get started creating an Internet facing load balancer (classic) in hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4dba5-104">portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="4dba5-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="4dba5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dba5-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="4dba5-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="4dba5-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="4dba5-107">Servizi cloud di Azure</span><span class="sxs-lookup"><span data-stu-id="4dba5-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="4dba5-108">Prima di lavorare con le risorse di Azure, è importante toounderstand che Azure ha due modelli di distribuzione: Gestione risorse di Azure e classica.</span><span class="sxs-lookup"><span data-stu-id="4dba5-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="4dba5-109">È importante comprendere i [modelli e strumenti di distribuzione](../azure-classic-rm.md) prima di lavorare con le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="4dba5-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="4dba5-110">È possibile visualizzare la documentazione di hello per diversi strumenti facendo clic sulle schede hello nella parte superiore di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="4dba5-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="4dba5-111">Questo articolo descrive il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="4dba5-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="4dba5-112">È anche possibile [informazioni su come una connessione Internet toocreate bilanciamento del carico con Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4dba5-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a><span data-ttu-id="4dba5-113">Procedura dettagliata sulla creazione di un servizio di bilanciamento del carico Internet tramite CLI</span><span class="sxs-lookup"><span data-stu-id="4dba5-113">Step by step creating an Internet facing load balancer using CLI</span></span>

<span data-ttu-id="4dba5-114">Questa guida viene spiegato come toocreate un bilanciamento del carico Internet in base a hello scenario precedente.</span><span class="sxs-lookup"><span data-stu-id="4dba5-114">This guide shows how toocreate an Internet load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="4dba5-115">Se non si è mai usato CLI di Azure, vedere [installare e configurare hello Azure CLI](../cli-install-nodejs.md) e seguire le istruzioni di hello toohello un punto in cui si seleziona l'account di Azure e la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="4dba5-115">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="4dba5-116">Eseguire hello **modalità di configurazione azure** comando tooswitch tooclassic modalità come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="4dba5-116">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="4dba5-117">Output previsto:</span><span class="sxs-lookup"><span data-stu-id="4dba5-117">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="4dba5-118">Creazione dell’endpoint e del set del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="4dba5-118">Create endpoint and load balancer set</span></span>

<span data-ttu-id="4dba5-119">scenario di Hello si presuppone che le macchine virtuali hello "web1" e "web2" sono stati creati.</span><span class="sxs-lookup"><span data-stu-id="4dba5-119">hello scenario assumes hello virtual machines "web1" and "web2" were created.</span></span>
<span data-ttu-id="4dba5-120">In questa guida verrà creato un set del servizio di bilanciamento del carico utilizzando la porta 80 come porta pubblica e la porta 80 come porta locale.</span><span class="sxs-lookup"><span data-stu-id="4dba5-120">This guide will create a load balancer set using port 80 as public port and port 80 as local port.</span></span> <span data-ttu-id="4dba5-121">Una porta probe viene configurata anche sulla porta 80 e bilanciamento del carico denominato hello imposta "set con carico bilanciato".</span><span class="sxs-lookup"><span data-stu-id="4dba5-121">A probe port is also configured on port 80 and named hello load balancer set "lbset".</span></span>

### <a name="step-1"></a><span data-ttu-id="4dba5-122">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="4dba5-122">Step 1</span></span>

<span data-ttu-id="4dba5-123">Creare endpoint prima di hello e bilanciamento del carico impostato utilizzando `azure network vm endpoint create` per la macchina virtuale "web1".</span><span class="sxs-lookup"><span data-stu-id="4dba5-123">Create hello first endpoint and load balancer set using `azure network vm endpoint create` for virtual machine "web1".</span></span>

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a><span data-ttu-id="4dba5-124">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="4dba5-124">Step 2</span></span>

<span data-ttu-id="4dba5-125">Aggiungere un secondo set di bilanciamento carico toohello macchina virtuale "web2".</span><span class="sxs-lookup"><span data-stu-id="4dba5-125">Add a second virtual machine "web2" toohello load balancer set.</span></span>

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a><span data-ttu-id="4dba5-126">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="4dba5-126">Step 3</span></span>

<span data-ttu-id="4dba5-127">Verificare tramite configurazione del servizio di bilanciamento carico di hello `azure vm show` .</span><span class="sxs-lookup"><span data-stu-id="4dba5-127">Verify hello load balancer configuration using `azure vm show` .</span></span>

```azurecli
azure vm show web1
```

<span data-ttu-id="4dba5-128">output di Hello sarà:</span><span class="sxs-lookup"><span data-stu-id="4dba5-128">hello output will be:</span></span>

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

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="4dba5-129">Creare un endpoint di desktop remoto per una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="4dba5-129">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="4dba5-130">È possibile creare un traffico di rete tooforward endpoint desktop remoto da una porta locale tooa di porta pubblica per l'utilizzo di una macchina virtuale specifica `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="4dba5-130">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="4dba5-131">Rimuovere la macchina virtuale dal servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="4dba5-131">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="4dba5-132">È necessario caricare il set di bilanciamento del carico dalla macchina virtuale hello toodelete hello endpoint associato toohello.</span><span class="sxs-lookup"><span data-stu-id="4dba5-132">You have toodelete hello endpoint associated toohello load balancer set from hello virtual machine.</span></span> <span data-ttu-id="4dba5-133">Dopo la rimozione di endpoint hello, macchina virtuale hello non appartiene a bilanciamento del carico toohello imposta più.</span><span class="sxs-lookup"><span data-stu-id="4dba5-133">Once hello endpoint is removed, hello virtual machine doesn't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="4dba5-134">Utilizzando l'esempio hello precedente, è possibile rimuovere endpoint hello creato per la macchina virtuale "web1" dal servizio di bilanciamento del carico "set con carico bilanciato" utilizzando il comando hello `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="4dba5-134">Using hello example above, you can remove hello endpoint created for virtual machine "web1" from load balancer "lbset" using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> <span data-ttu-id="4dba5-135">È possibile esplorare più endpoint di toomanage opzioni comando hello`azure vm endpoint --help`</span><span class="sxs-lookup"><span data-stu-id="4dba5-135">You can explore more options toomanage endpoints using hello command `azure vm endpoint --help`</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dba5-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4dba5-136">Next steps</span></span>

[<span data-ttu-id="4dba5-137">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="4dba5-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="4dba5-138">Configurare una modalità di distribuzione del servizio di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="4dba5-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="4dba5-139">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="4dba5-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
