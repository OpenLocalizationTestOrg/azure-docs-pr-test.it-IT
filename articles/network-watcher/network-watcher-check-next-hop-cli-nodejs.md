---
title: Individuare l'hop successivo con Azure Network Watcher - Interfaccia della riga di comando di Azure 1.0 | Microsoft Docs
description: "Questo articolo descrive come individuare il tipo di hop successivo e l'indirizzo IP tramite la funzionalità Hop successivo dell'interfaccia della riga di comando di Azure."
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
ms.openlocfilehash: ff88e945060ae033717ceb29db1352e112f05a3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="d35e1-103">Individuare il tipo di hop successivo tramite la funzionalità Hop successivo di Azure Network Watcher usando l'interfaccia della riga di comando di Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="d35e1-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d35e1-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d35e1-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="d35e1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d35e1-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="d35e1-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="d35e1-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="d35e1-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="d35e1-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="d35e1-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="d35e1-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="d35e1-109">Hop successivo è una funzionalità di Network Watcher che consente di recuperare il tipo di hop successivo e l'indirizzo IP in base a una macchina virtuale specificata.</span><span class="sxs-lookup"><span data-stu-id="d35e1-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="d35e1-110">La funzionalità è utile per determinare se il traffico in uscita da una macchina virtuale attraversa gateway, Internet o reti virtuali per arrivare alla propria destinazione.</span><span class="sxs-lookup"><span data-stu-id="d35e1-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

<span data-ttu-id="d35e1-111">Questo articolo usa l'interfaccia della riga di comando di Azure 1.0 multipiattaforma, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="d35e1-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d35e1-112">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="d35e1-112">Before you begin</span></span>

<span data-ttu-id="d35e1-113">In questo scenario viene usata l'interfaccia della riga di comando di Azure per trovare il tipo di hop successivo e l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="d35e1-113">In this scenario, you will use the Azure CLI to find the next hop type and IP address.</span></span>

<span data-ttu-id="d35e1-114">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="d35e1-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="d35e1-115">Lo scenario presuppone inoltre che esista e possa essere usato un gruppo di risorse con una macchina virtuale valida.</span><span class="sxs-lookup"><span data-stu-id="d35e1-115">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="d35e1-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="d35e1-116">Scenario</span></span>

<span data-ttu-id="d35e1-117">Lo scenario illustrato in questo articolo usa la funzionalità Hop successivo di Network Watcher che rileva il tipo di hop successivo e l'indirizzo IP di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="d35e1-117">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="d35e1-118">Per altre informazioni sulla funzionalità di individuazione dell'hop successivo, consultare la [panoramica su Hop successivo](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d35e1-118">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="d35e1-119">Ottenere l'hop successivo</span><span class="sxs-lookup"><span data-stu-id="d35e1-119">Get Next Hop</span></span>

<span data-ttu-id="d35e1-120">Per ottenere l'hop successivo viene usato il cmdlet `azure netowrk watcher next-hop`.</span><span class="sxs-lookup"><span data-stu-id="d35e1-120">To get the next hop we call the `azure netowrk watcher next-hop` cmdlet.</span></span> <span data-ttu-id="d35e1-121">Al cmdlet vengono passati il gruppo di risorse di Network Watcher, l'ID della macchina virtuale, l'indirizzo IP di origine e l'indirizzo IP di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d35e1-121">We pass the cmdlet the Network Watcher resource group, the NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="d35e1-122">Nell'esempio seguente, l'indirizzo IP di destinazione corrisponde a una macchina virtuale in un'altra rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d35e1-122">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="d35e1-123">Tra le due reti virtuali esiste un gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d35e1-123">There is a virtual network gateway between the two virtual networks.</span></span> 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
<span data-ttu-id="d35e1-124">Se la macchina virtuale è dotata di più schede NIC e su una qualsiasi delle schede NIC è abilitato l'inoltro dell'IP, è necessario specificare il parametro NIC (-i nic-id).</span><span class="sxs-lookup"><span data-stu-id="d35e1-124">If the VM has multiple NICs and IP forwarding is enabled on any of the NICs, then the NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="d35e1-125">In caso contrario, è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="d35e1-125">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="d35e1-126">Esaminare i risultati</span><span class="sxs-lookup"><span data-stu-id="d35e1-126">Review results</span></span>

<span data-ttu-id="d35e1-127">Al termine vengono forniti i risultati.</span><span class="sxs-lookup"><span data-stu-id="d35e1-127">When complete, the results are provided.</span></span> <span data-ttu-id="d35e1-128">Viene inoltre restituito l'indirizzo IP dell'hop successivo e il tipo di risorsa corrispondente.</span><span class="sxs-lookup"><span data-stu-id="d35e1-128">The next hop IP address is returned as well as the type of resource it is.</span></span>

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

<span data-ttu-id="d35e1-129">L'elenco seguente mostra i valori NextHopType attualmente disponibili:</span><span class="sxs-lookup"><span data-stu-id="d35e1-129">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="d35e1-130">**Tipo di hop successivo**</span><span class="sxs-lookup"><span data-stu-id="d35e1-130">**Next Hop Type**</span></span>

* <span data-ttu-id="d35e1-131">Internet</span><span class="sxs-lookup"><span data-stu-id="d35e1-131">Internet</span></span>
* <span data-ttu-id="d35e1-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="d35e1-132">VirtualAppliance</span></span>
* <span data-ttu-id="d35e1-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="d35e1-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="d35e1-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="d35e1-134">VnetLocal</span></span>
* <span data-ttu-id="d35e1-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="d35e1-135">HyperNetGateway</span></span>
* <span data-ttu-id="d35e1-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="d35e1-136">VnetPeering</span></span>
* <span data-ttu-id="d35e1-137">None</span><span class="sxs-lookup"><span data-stu-id="d35e1-137">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="d35e1-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d35e1-138">Next steps</span></span>

<span data-ttu-id="d35e1-139">Per altre informazioni su come verificare le impostazioni del gruppo di sicurezza di rete a livello di codice, consultare l'articolo su come [verificare i gruppi di sicurezza di rete con Network Watcher](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="d35e1-139">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
