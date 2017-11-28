---
title: aaaFind hop successivo con rete Azure Watcher Hop successivo - CLI di Azure 1.0 | Documenti Microsoft
description: "In questo articolo viene descritto come è possibile trovare quale hello tipo dell'hop successivo è e tramite indirizzo ip dell'Hop successivo utilizzando l'interfaccia CLI di Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 54124c051021413695d70ba93c370605abc6ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="a526c-103">Individuare il tipo dell'hop successivo hello sta utilizzando funzionalità Hop successivo hello in Watcher di rete di Azure mediante Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a526c-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a526c-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a526c-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="a526c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a526c-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="a526c-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="a526c-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="a526c-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="a526c-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="a526c-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="a526c-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="a526c-109">Hop successivo è una funzionalità di controllo di rete che consente di hello ottenere il tipo dell'hop successivo di hello e l'indirizzo IP in base a una macchina virtuale specificata.</span><span class="sxs-lookup"><span data-stu-id="a526c-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="a526c-110">Questa funzionalità è utile per determinare se il traffico da una macchina virtuale consente di scorrere un gateway, internet o reti virtuali tooget tooits destinazione.</span><span class="sxs-lookup"><span data-stu-id="a526c-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

<span data-ttu-id="a526c-111">Questo articolo usa l'interfaccia della riga di comando di Azure 1.0 multipiattaforma, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="a526c-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a526c-112">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="a526c-112">Before you begin</span></span>

<span data-ttu-id="a526c-113">In questo scenario, si utilizzerà il tipo dell'hop successivo di CLI di Azure toofind hello hello e l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="a526c-113">In this scenario, you will use hello Azure CLI toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="a526c-114">Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete.</span><span class="sxs-lookup"><span data-stu-id="a526c-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="a526c-115">scenario di Hello si suppone inoltre che un gruppo di risorse con una macchina virtuale valida toobe utilizzato.</span><span class="sxs-lookup"><span data-stu-id="a526c-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="a526c-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="a526c-116">Scenario</span></span>

<span data-ttu-id="a526c-117">scenario di Hello illustrato in questo articolo Usa Hop successivo, una funzionalità del controllo di rete che consente di trovare il tipo dell'hop successivo hello e indirizzo IP per una risorsa.</span><span class="sxs-lookup"><span data-stu-id="a526c-117">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="a526c-118">toolearn su più Hop successivo, visitare [panoramica dell'Hop successivo](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a526c-118">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="a526c-119">Ottenere l'hop successivo</span><span class="sxs-lookup"><span data-stu-id="a526c-119">Get Next Hop</span></span>

<span data-ttu-id="a526c-120">tooget hello dell'hop successivo è chiamare hello `azure netowrk watcher next-hop` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a526c-120">tooget hello next hop we call hello `azure netowrk watcher next-hop` cmdlet.</span></span> <span data-ttu-id="a526c-121">Passiamo hello NetworkWatcher, gruppo di risorse di hello cmdlet hello Watcher di rete, la macchina virtuale Id, indirizzo IP di origine e indirizzo IP di destinazione.</span><span class="sxs-lookup"><span data-stu-id="a526c-121">We pass hello cmdlet hello Network Watcher resource group, hello NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="a526c-122">In questo esempio, indirizzo IP di destinazione hello è tooa macchina virtuale in un'altra rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a526c-122">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="a526c-123">È un gateway di rete virtuale tra due reti virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="a526c-123">There is a virtual network gateway between hello two virtual networks.</span></span> 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
<span data-ttu-id="a526c-124">Se è abilitato l'inoltro IP in una delle schede di rete hello hello VM ha più schede di rete, quindi hello parametro NIC (-i nic-id) deve essere specificato.</span><span class="sxs-lookup"><span data-stu-id="a526c-124">If hello VM has multiple NICs and IP forwarding is enabled on any of hello NICs, then hello NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="a526c-125">In caso contrario, è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="a526c-125">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="a526c-126">Esaminare i risultati</span><span class="sxs-lookup"><span data-stu-id="a526c-126">Review results</span></span>

<span data-ttu-id="a526c-127">Al termine, vengono forniti i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="a526c-127">When complete, hello results are provided.</span></span> <span data-ttu-id="a526c-128">indirizzo IP dell'hop successivo Hello viene restituito nonché il tipo di hello della risorsa che è.</span><span class="sxs-lookup"><span data-stu-id="a526c-128">hello next hop IP address is returned as well as hello type of resource it is.</span></span>

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

<span data-ttu-id="a526c-129">Hello seguito sono elencati i valori NextHopType hello attualmente disponibili:</span><span class="sxs-lookup"><span data-stu-id="a526c-129">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="a526c-130">**Tipo di hop successivo**</span><span class="sxs-lookup"><span data-stu-id="a526c-130">**Next Hop Type**</span></span>

* <span data-ttu-id="a526c-131">Internet</span><span class="sxs-lookup"><span data-stu-id="a526c-131">Internet</span></span>
* <span data-ttu-id="a526c-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="a526c-132">VirtualAppliance</span></span>
* <span data-ttu-id="a526c-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="a526c-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="a526c-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="a526c-134">VnetLocal</span></span>
* <span data-ttu-id="a526c-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="a526c-135">HyperNetGateway</span></span>
* <span data-ttu-id="a526c-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="a526c-136">VnetPeering</span></span>
* <span data-ttu-id="a526c-137">None</span><span class="sxs-lookup"><span data-stu-id="a526c-137">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="a526c-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a526c-138">Next steps</span></span>

<span data-ttu-id="a526c-139">Informazioni su come tooreview le impostazioni di gruppo di sicurezza di rete a livello di codice, visitare il sito [NSG il controllo con Watcher di rete](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="a526c-139">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
