---
title: Individuare l'hop successivo con Network Watcher di Azure - Portale di Azure | Documentazione Microsoft
description: "Questo articolo descrive come individuare il tipo di hop successivo e l'indirizzo IP mediante la funzionalità Hop successivo del portale di Azure"
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
ms.openlocfilehash: 5434b7972346821985c459fc4620805adb88676b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-the-portal"></a><span data-ttu-id="22907-103">Individuare il tipo di hop successivo tramite la funzionalità Hop successivo di Network Watcher di Azure mediante il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="22907-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using the portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="22907-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="22907-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="22907-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="22907-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="22907-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="22907-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="22907-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="22907-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="22907-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="22907-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="22907-109">Hop successivo è una funzionalità di Network Watcher che consente di recuperare il tipo di hop successivo e l'indirizzo IP in base a una macchina virtuale specificata.</span><span class="sxs-lookup"><span data-stu-id="22907-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="22907-110">La funzionalità è utile per determinare se il traffico in uscita da una macchina virtuale attraversa gateway, Internet o reti virtuali per arrivare alla propria destinazione.</span><span class="sxs-lookup"><span data-stu-id="22907-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="22907-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="22907-111">Before you begin</span></span>

<span data-ttu-id="22907-112">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="22907-112">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="22907-113">Lo scenario presuppone inoltre che esista e possa essere usato un gruppo di risorse con una macchina virtuale valida.</span><span class="sxs-lookup"><span data-stu-id="22907-113">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="22907-114">Scenario</span><span class="sxs-lookup"><span data-stu-id="22907-114">Scenario</span></span>

<span data-ttu-id="22907-115">Lo scenario illustrato in questo articolo usa la funzionalità Hop successivo per rilevare il tipo di hop successivo e l'indirizzo IP per una risorsa.</span><span class="sxs-lookup"><span data-stu-id="22907-115">The scenario covered in this article uses Next hop to find out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="22907-116">Per altre informazioni sulla funzionalità di individuazione dell'hop successivo, consultare la [panoramica sulla funzionalità Hop successivo](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="22907-116">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="22907-117">In questo scenario si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="22907-117">In this scenario, you will:</span></span>

* <span data-ttu-id="22907-118">Recuperare l'hop successivo da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="22907-118">Retrieve the next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="22907-119">Ottenere l'hop successivo</span><span class="sxs-lookup"><span data-stu-id="22907-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="22907-120">Passaggio 1</span><span class="sxs-lookup"><span data-stu-id="22907-120">Step 1</span></span>

<span data-ttu-id="22907-121">Nel portale di Azure passare alla risorsa Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="22907-121">Navigate to your Network Watcher resource in the Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="22907-122">Passaggio 2</span><span class="sxs-lookup"><span data-stu-id="22907-122">Step 2</span></span>

<span data-ttu-id="22907-123">Fare clic su **Hop successivo** nel riquadro di spostamento, selezionare la macchina virtuale e l'interfaccia di rete, compilare l'indirizzo IP di origine e di destinazione e fare clic sul pulsante **Hop successivo**.</span><span class="sxs-lookup"><span data-stu-id="22907-123">Click **Next hop** in the navigation pane, select the virtual machine and network interface, fill out the source and destination IP, and click the **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="22907-124">La funzionalità Hop successivo richiede che la risorsa VM sia allocata.</span><span class="sxs-lookup"><span data-stu-id="22907-124">Next hop requires that the VM resource is allocated to run.</span></span>

![Panoramica di come ottenere l'hop successivo][1]

### <a name="step-3"></a><span data-ttu-id="22907-126">Passaggio 3</span><span class="sxs-lookup"><span data-stu-id="22907-126">Step 3</span></span>

<span data-ttu-id="22907-127">Al termine dell'attività vengono forniti i risultati.</span><span class="sxs-lookup"><span data-stu-id="22907-127">Once the task is complete, the results are provided.</span></span> <span data-ttu-id="22907-128">Vengono visualizzati l'indirizzo IP e il tipo di dispositivo dell'hop successivo.</span><span class="sxs-lookup"><span data-stu-id="22907-128">The IP address and type of device the next hop is, is displayed.</span></span> <span data-ttu-id="22907-129">La tabella seguente illustra i valori restituiti disponibili nel portale.</span><span class="sxs-lookup"><span data-stu-id="22907-129">The following table shows the available returned values in the portal.</span></span>

<span data-ttu-id="22907-130">**Tipo di hop successivo**</span><span class="sxs-lookup"><span data-stu-id="22907-130">**Next Hop Type**</span></span>

* <span data-ttu-id="22907-131">Internet</span><span class="sxs-lookup"><span data-stu-id="22907-131">Internet</span></span>
* <span data-ttu-id="22907-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="22907-132">VirtualAppliance</span></span>
* <span data-ttu-id="22907-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="22907-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="22907-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="22907-134">VnetLocal</span></span>
* <span data-ttu-id="22907-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="22907-135">HyperNetGateway</span></span>
* <span data-ttu-id="22907-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="22907-136">VnetPeering</span></span>
* <span data-ttu-id="22907-137">None</span><span class="sxs-lookup"><span data-stu-id="22907-137">None</span></span>

<span data-ttu-id="22907-138">Se è stata usata una route personalizzata per indirizzare il traffico, insieme ai risultati viene visualizzata la route definita dall'utente (UDR).</span><span class="sxs-lookup"><span data-stu-id="22907-138">If a custom route was used to route this traffic, the User-defined route (UDR) is shown as well with the results.</span></span>

![Risultati dell'ottenimento dell'hop successivo][2]

## <a name="next-steps"></a><span data-ttu-id="22907-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="22907-140">Next steps</span></span>

<span data-ttu-id="22907-141">Per altre informazioni su come verificare le impostazioni del gruppo di sicurezza di rete a livello di codice, consultare l'articolo su come [verificare i gruppi di sicurezza di rete con Network Watcher](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="22907-141">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














