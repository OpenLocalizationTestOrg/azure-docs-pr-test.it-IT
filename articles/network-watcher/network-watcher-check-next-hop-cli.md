---
title: Individuare l'hop successivo con Azure Network Watcher - Interfaccia della riga di comando di Azure 2.0 | Microsoft Docs
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
ms.openlocfilehash: d1ee6870ba0188ff2c473e4cca12a5bdc1f97d3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="476a7-103">Individuare il tipo di hop successivo tramite la funzionalità Hop successivo di Azure Network Watcher usando l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="476a7-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="476a7-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="476a7-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="476a7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="476a7-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="476a7-106">Interfaccia della riga di comando 1.0</span><span class="sxs-lookup"><span data-stu-id="476a7-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="476a7-107">Interfaccia della riga di comando 2.0</span><span class="sxs-lookup"><span data-stu-id="476a7-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="476a7-108">API REST di Azure</span><span class="sxs-lookup"><span data-stu-id="476a7-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="476a7-109">Hop successivo è una funzionalità di Network Watcher che consente di recuperare il tipo di hop successivo e l'indirizzo IP in base a una macchina virtuale specificata.</span><span class="sxs-lookup"><span data-stu-id="476a7-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="476a7-110">La funzionalità è utile per determinare se il traffico in uscita da una macchina virtuale attraversa gateway, Internet o reti virtuali per arrivare alla propria destinazione.</span><span class="sxs-lookup"><span data-stu-id="476a7-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

<span data-ttu-id="476a7-111">Questo articolo usa l'interfaccia della riga di comando di nuova generazione per il modello di distribuzione di gestione delle risorse, ovvero l'interfaccia della riga di comando di Azure 2.0, disponibile per Windows, Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="476a7-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="476a7-112">Per eseguire i passaggi indicati in questo articolo è necessario [installare l'interfaccia della riga di comando di Azure per Mac, Linux e Windows (interfaccia della riga di comando di Azure)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="476a7-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="476a7-113">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="476a7-113">Before you begin</span></span>

<span data-ttu-id="476a7-114">In questo scenario viene usata l'interfaccia della riga di comando di Azure per trovare il tipo di hop successivo e l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="476a7-114">In this scenario, you will use the Azure CLI to find the next hop type and IP address.</span></span>

<span data-ttu-id="476a7-115">Questo scenario presuppone il completamento dei passaggi descritti in [Creare un servizio Network Watcher](network-watcher-create.md) per creare un servizio Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="476a7-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="476a7-116">Lo scenario presuppone inoltre che esista e possa essere usato un gruppo di risorse con una macchina virtuale valida.</span><span class="sxs-lookup"><span data-stu-id="476a7-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="476a7-117">Scenario</span><span class="sxs-lookup"><span data-stu-id="476a7-117">Scenario</span></span>

<span data-ttu-id="476a7-118">Lo scenario illustrato in questo articolo usa la funzionalità Hop successivo di Network Watcher che rileva il tipo di hop successivo e l'indirizzo IP di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="476a7-118">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="476a7-119">Per altre informazioni sulla funzionalità di individuazione dell'hop successivo, consultare la [panoramica su Hop successivo](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="476a7-119">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="476a7-120">Ottenere l'hop successivo</span><span class="sxs-lookup"><span data-stu-id="476a7-120">Get Next Hop</span></span>

<span data-ttu-id="476a7-121">Per ottenere l'hop successivo viene usato il cmdlet `az network watcher show-next-hop`.</span><span class="sxs-lookup"><span data-stu-id="476a7-121">To get the next hop we call the `az network watcher show-next-hop` cmdlet.</span></span> <span data-ttu-id="476a7-122">Al cmdlet vengono passati il gruppo di risorse di Network Watcher, l'ID della macchina virtuale, l'indirizzo IP di origine e l'indirizzo IP di destinazione.</span><span class="sxs-lookup"><span data-stu-id="476a7-122">We pass the cmdlet the Network Watcher resource group, the NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="476a7-123">Nell'esempio seguente, l'indirizzo IP di destinazione corrisponde a una macchina virtuale in un'altra rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="476a7-123">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="476a7-124">Tra le due reti virtuali esiste un gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="476a7-124">There is a virtual network gateway between the two virtual networks.</span></span>

<span data-ttu-id="476a7-125">Se questa operazione non è stata ancora eseguita, installare e configurare l'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2) e accedere a un account Azure usando il comando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="476a7-125">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="476a7-126">Quindi, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="476a7-126">Then run the following command:</span></span>

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
<span data-ttu-id="476a7-127">Se la macchina virtuale è dotata di più schede NIC e su una qualsiasi delle schede NIC è abilitato l'inoltro dell'IP, è necessario specificare il parametro NIC (-i nic-id).</span><span class="sxs-lookup"><span data-stu-id="476a7-127">If the VM has multiple NICs and IP forwarding is enabled on any of the NICs, then the NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="476a7-128">In caso contrario, è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="476a7-128">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="476a7-129">Esaminare i risultati</span><span class="sxs-lookup"><span data-stu-id="476a7-129">Review results</span></span>

<span data-ttu-id="476a7-130">Al termine vengono forniti i risultati.</span><span class="sxs-lookup"><span data-stu-id="476a7-130">When complete, the results are provided.</span></span> <span data-ttu-id="476a7-131">Viene inoltre restituito l'indirizzo IP dell'hop successivo e il tipo di risorsa corrispondente.</span><span class="sxs-lookup"><span data-stu-id="476a7-131">The next hop IP address is returned as well as the type of resource it is.</span></span>

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

<span data-ttu-id="476a7-132">L'elenco seguente mostra i valori NextHopType attualmente disponibili:</span><span class="sxs-lookup"><span data-stu-id="476a7-132">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="476a7-133">**Tipo di hop successivo**</span><span class="sxs-lookup"><span data-stu-id="476a7-133">**Next Hop Type**</span></span>

* <span data-ttu-id="476a7-134">Internet</span><span class="sxs-lookup"><span data-stu-id="476a7-134">Internet</span></span>
* <span data-ttu-id="476a7-135">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="476a7-135">VirtualAppliance</span></span>
* <span data-ttu-id="476a7-136">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="476a7-136">VirtualNetworkGateway</span></span>
* <span data-ttu-id="476a7-137">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="476a7-137">VnetLocal</span></span>
* <span data-ttu-id="476a7-138">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="476a7-138">HyperNetGateway</span></span>
* <span data-ttu-id="476a7-139">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="476a7-139">VnetPeering</span></span>
* <span data-ttu-id="476a7-140">None</span><span class="sxs-lookup"><span data-stu-id="476a7-140">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="476a7-141">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="476a7-141">Next steps</span></span>

<span data-ttu-id="476a7-142">Per altre informazioni su come verificare le impostazioni del gruppo di sicurezza di rete a livello di codice, consultare l'articolo su come [verificare i gruppi di sicurezza di rete con Network Watcher](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="476a7-142">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
