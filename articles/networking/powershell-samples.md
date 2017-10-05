---
title: Esempi di Azure PowerShell | Microsoft Docs
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
ms.openlocfilehash: 0bca4fb6874bd265f0ae9faeb4219abeb4ffb6d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-powershell-samples-for-networking"></a><span data-ttu-id="79f69-103">Esempi di Azure PowerShell per la rete</span><span class="sxs-lookup"><span data-stu-id="79f69-103">Azure PowerShell Samples for networking</span></span>

<span data-ttu-id="79f69-104">La tabella seguente include i collegamenti agli script creati usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="79f69-104">The following table includes links to scripts built using Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="79f69-105">**Connettività tra risorse di Azure**</span><span class="sxs-lookup"><span data-stu-id="79f69-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="79f69-106">Creare una rete virtuale per le applicazioni multilivello</span><span class="sxs-lookup"><span data-stu-id="79f69-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="79f69-107">Crea una rete virtuale con subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="79f69-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="79f69-108">Il traffico verso la subnet front-end è limitato a HTTP, mentre il traffico verso la subnet back-end è limitato a SQL sulla porta 1433.</span><span class="sxs-lookup"><span data-stu-id="79f69-108">Traffic to the front-end subnet is limited to HTTP, while traffic to the back-end subnet is limited to SQL, port 1433.</span></span> |
| [<span data-ttu-id="79f69-109">Eseguire il peering di due reti virtuali</span><span class="sxs-lookup"><span data-stu-id="79f69-109">Peer two virtual networks</span></span>](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="79f69-110">Crea e connette due reti virtuali nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="79f69-110">Creates and connects two virtual networks in the same region.</span></span> |
| [<span data-ttu-id="79f69-111">Instradare il traffico attraverso un'appliance virtuale di rete</span><span class="sxs-lookup"><span data-stu-id="79f69-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="79f69-112">Crea una rete virtuale con subnet front-end e back-end e una VM che è in grado di instradare il traffico tra le due subnet.</span><span class="sxs-lookup"><span data-stu-id="79f69-112">Creates a virtual network with front-end and back-end subnets and a VM that is able to route traffic between the two subnets.</span></span> |
| [<span data-ttu-id="79f69-113">Filtrare il traffico della VM in ingresso e in uscita</span><span class="sxs-lookup"><span data-stu-id="79f69-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="79f69-114">Crea una rete virtuale con subnet front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="79f69-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="79f69-115">Il traffico di rete in ingresso alla subnet front-end è limitato a HTTP e HTTPS.</span><span class="sxs-lookup"><span data-stu-id="79f69-115">Inbound network traffic to the front-end subnet is limited to HTTP and HTTPS..</span></span> <span data-ttu-id="79f69-116">Non è consentito il traffico in uscita verso Internet dalla subnet di back-end.</span><span class="sxs-lookup"><span data-stu-id="79f69-116">Outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="79f69-117">**Bilanciamento del carico e direzione del traffico**</span><span class="sxs-lookup"><span data-stu-id="79f69-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="79f69-118">Eseguire il bilanciamento del carico per il traffico verso le VM per la disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="79f69-118">Load balance traffic to VMs for high availability</span></span>](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="79f69-119">Consente di creare più macchine virtuali in una configurazione a disponibilità elevata e con bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="79f69-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="79f69-120">Eseguire il bilanciamento del carico per più siti Web sulle VM</span><span class="sxs-lookup"><span data-stu-id="79f69-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="79f69-121">Crea due VM con più configurazioni IP, unite a un set di disponibilità di Azure, accessibili tramite un servizio di bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="79f69-121">Creates two VMs with multiple IP configurations, joined to an Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="79f69-122">Dirigere il traffico su più aree per la disponibilità elevata delle applicazioni</span><span class="sxs-lookup"><span data-stu-id="79f69-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="79f69-123">Crea due piani di servizio app, due app Web, un profilo di gestione traffico e due endpoint di gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="79f69-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
