---
title: aaaFind hop successivo con rete Azure Watcher Hop successivo - portale di Azure | Documenti Microsoft
description: "In questo articolo descrive come è possibile trovare quale hello tipo dell'hop successivo è e indirizzo ip utilizzando di Hop successivo hello portale di Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="95ae7-103">Individuare il tipo dell'hop successivo hello sta utilizzando funzionalità Hop successivo hello in Watcher di rete di Azure tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="95ae7-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="95ae7-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="95ae7-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="95ae7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="95ae7-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="95ae7-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="95ae7-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="95ae7-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="95ae7-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="95ae7-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="95ae7-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="95ae7-109">Hop successivo è una funzionalità di controllo di rete che consente di hello ottenere il tipo dell'hop successivo di hello e l'indirizzo IP in base a una macchina virtuale specificata.</span><span class="sxs-lookup"><span data-stu-id="95ae7-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="95ae7-110">Questa funzionalità è utile per determinare se il traffico da una macchina virtuale consente di scorrere un gateway, internet o reti virtuali tooget tooits destinazione.</span><span class="sxs-lookup"><span data-stu-id="95ae7-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="95ae7-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="95ae7-111">Before you begin</span></span>

<span data-ttu-id="95ae7-112">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="95ae7-112">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="95ae7-113">scenario di Hello si suppone inoltre che un gruppo di risorse con una macchina virtuale valida toobe utilizzato.</span><span class="sxs-lookup"><span data-stu-id="95ae7-113">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="95ae7-114">Scenario</span><span class="sxs-lookup"><span data-stu-id="95ae7-114">Scenario</span></span>

<span data-ttu-id="95ae7-115">scenario di Hello illustrato in questo articolo Usa toofind hop successivo tipo dell'hop successivo hello e indirizzo IP per una risorsa.</span><span class="sxs-lookup"><span data-stu-id="95ae7-115">hello scenario covered in this article uses Next hop toofind out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="95ae7-116">toolearn su più Hop successivo, visitare [panoramica dell'Hop successivo](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="95ae7-116">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="95ae7-117">In questo scenario si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="95ae7-117">In this scenario, you will:</span></span>

* <span data-ttu-id="95ae7-118">Recuperare l'hop successivo hello da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="95ae7-118">Retrieve hello next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="95ae7-119">Ottenere l'hop successivo</span><span class="sxs-lookup"><span data-stu-id="95ae7-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="95ae7-120">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="95ae7-120">Step 1</span></span>

<span data-ttu-id="95ae7-121">Passare risorsa Watcher di rete tooyour hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="95ae7-121">Navigate tooyour Network Watcher resource in hello Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="95ae7-122">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="95ae7-122">Step 2</span></span>

<span data-ttu-id="95ae7-123">Fare clic su **hop successivo** nel riquadro di spostamento hello, macchina virtuale selezionare hello e interfaccia di rete, compilare hello IP di origine e di destinazione e fare clic su hello **hop successivo** pulsante.</span><span class="sxs-lookup"><span data-stu-id="95ae7-123">Click **Next hop** in hello navigation pane, select hello virtual machine and network interface, fill out hello source and destination IP, and click hello **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="95ae7-124">Hop successivo è necessario che risorsa macchina virtuale hello è allocato toorun.</span><span class="sxs-lookup"><span data-stu-id="95ae7-124">Next hop requires that hello VM resource is allocated toorun.</span></span>

![Panoramica di come ottenere l'hop successivo][1]

### <a name="step-3"></a><span data-ttu-id="95ae7-126">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="95ae7-126">Step 3</span></span>

<span data-ttu-id="95ae7-127">Una volta completata l'attività hello, vengono forniti i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="95ae7-127">Once hello task is complete, hello results are provided.</span></span> <span data-ttu-id="95ae7-128">Hello indirizzo IP e il tipo dell'hop successivo hello di dispositivo, viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="95ae7-128">hello IP address and type of device hello next hop is, is displayed.</span></span> <span data-ttu-id="95ae7-129">Hello nella tabella seguente mostra i valori restituiti di hello disponibili nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="95ae7-129">hello following table shows hello available returned values in hello portal.</span></span>

<span data-ttu-id="95ae7-130">**Tipo di hop successivo**</span><span class="sxs-lookup"><span data-stu-id="95ae7-130">**Next Hop Type**</span></span>

* <span data-ttu-id="95ae7-131">Internet</span><span class="sxs-lookup"><span data-stu-id="95ae7-131">Internet</span></span>
* <span data-ttu-id="95ae7-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="95ae7-132">VirtualAppliance</span></span>
* <span data-ttu-id="95ae7-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="95ae7-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="95ae7-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="95ae7-134">VnetLocal</span></span>
* <span data-ttu-id="95ae7-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="95ae7-135">HyperNetGateway</span></span>
* <span data-ttu-id="95ae7-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="95ae7-136">VnetPeering</span></span>
* <span data-ttu-id="95ae7-137">Nessuno</span><span class="sxs-lookup"><span data-stu-id="95ae7-137">None</span></span>

<span data-ttu-id="95ae7-138">Se una route personalizzata è stata utilizzata tooroute il traffico, route definite dall'utente hello (UDR) viene visualizzato anche con risultati hello.</span><span class="sxs-lookup"><span data-stu-id="95ae7-138">If a custom route was used tooroute this traffic, hello User-defined route (UDR) is shown as well with hello results.</span></span>

![Risultati dell'ottenimento dell'hop successivo][2]

## <a name="next-steps"></a><span data-ttu-id="95ae7-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="95ae7-140">Next steps</span></span>

<span data-ttu-id="95ae7-141">Informazioni su come tooreview le impostazioni di gruppo di sicurezza di rete a livello di codice, visitare il sito [NSG il controllo con Watcher di rete](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="95ae7-141">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














