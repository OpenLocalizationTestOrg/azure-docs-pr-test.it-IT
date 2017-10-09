---
title: Esempi di PowerShell aaaAzure | Documenti Microsoft
description: Esempi di Azure PowerShell
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/24/2017
ms.author: georgewallace
ms.openlocfilehash: 130a6e755691b46a9549cad5acaa5bde4fe38e95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-networking"></a><span data-ttu-id="709fc-103">Esempi di Azure PowerShell per la rete</span><span class="sxs-lookup"><span data-stu-id="709fc-103">Azure PowerShell Samples for networking</span></span>

<span data-ttu-id="709fc-104">Hello nella tabella seguente include collegamenti tooscripts compilate tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="709fc-104">hello following table includes links tooscripts built using Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="709fc-105">**Connettività tra risorse di Azure**</span><span class="sxs-lookup"><span data-stu-id="709fc-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="709fc-106">Creare una rete virtuale per le applicazioni multilivello</span><span class="sxs-lookup"><span data-stu-id="709fc-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="709fc-107">Crea una rete virtuale con subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="709fc-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="709fc-108">Subnet con traffico toohello front-end è tooHTTP limitata, mentre il traffico toohello subnet back-end è tooSQL limitata, la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="709fc-108">Traffic toohello front-end subnet is limited tooHTTP, while traffic toohello back-end subnet is limited tooSQL, port 1433.</span></span> |
| [<span data-ttu-id="709fc-109">Eseguire il peering di due reti virtuali</span><span class="sxs-lookup"><span data-stu-id="709fc-109">Peer two virtual networks</span></span>](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="709fc-110">Crea e si connette due reti virtuali in hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="709fc-110">Creates and connects two virtual networks in hello same region.</span></span> |
| [<span data-ttu-id="709fc-111">Instradare il traffico attraverso un'appliance virtuale di rete</span><span class="sxs-lookup"><span data-stu-id="709fc-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="709fc-112">Crea una rete virtuale e una macchina virtuale che è in grado di tooroute traffico tra subnet hello due subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="709fc-112">Creates a virtual network with front-end and back-end subnets and a VM that is able tooroute traffic between hello two subnets.</span></span> |
| [<span data-ttu-id="709fc-113">Filtrare il traffico della VM in ingresso e in uscita</span><span class="sxs-lookup"><span data-stu-id="709fc-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="709fc-114">Crea una rete virtuale con subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="709fc-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="709fc-115">Il traffico di rete in ingresso subnet front-end toohello è limitato tooHTTP e HTTPS...</span><span class="sxs-lookup"><span data-stu-id="709fc-115">Inbound network traffic toohello front-end subnet is limited tooHTTP and HTTPS..</span></span> <span data-ttu-id="709fc-116">Non è consentito il traffico in uscita toohello Internet dalla subnet di back-end hello.</span><span class="sxs-lookup"><span data-stu-id="709fc-116">Outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="709fc-117">**Bilanciamento del carico e direzione del traffico**</span><span class="sxs-lookup"><span data-stu-id="709fc-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="709fc-118">Caricare tooVMs di bilanciare il traffico per la disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="709fc-118">Load balance traffic tooVMs for high availability</span></span>](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="709fc-119">Consente di creare più macchine virtuali in una configurazione a disponibilità elevata e con bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="709fc-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="709fc-120">Eseguire il bilanciamento del carico per più siti Web sulle VM</span><span class="sxs-lookup"><span data-stu-id="709fc-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="709fc-121">Crea due macchine virtuali con più configurazioni IP, tooan aggiunti a un Set di disponibilità, accessibile tramite un servizio di bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="709fc-121">Creates two VMs with multiple IP configurations, joined tooan Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="709fc-122">Dirigere il traffico su più aree per la disponibilità elevata delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="709fc-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="709fc-123">Crea due piani di servizio app, due app Web, un profilo di gestione traffico e due endpoint di gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="709fc-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
