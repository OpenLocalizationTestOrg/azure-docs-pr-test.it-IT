---
title: Introduzione alla topologia di Azure Network Watcher | Documentazione Microsoft
description: "Questa pagina fornisce una panoramica delle funzionalità di topologia di Network Watcher"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 42443f614b76b8180ac163b9889163021adbf048
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-topology-in-azure-network-watcher"></a><span data-ttu-id="49442-103">Introduzione alla topologia di Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="49442-103">Introduction to topology in Azure Network Watcher</span></span>

<span data-ttu-id="49442-104">La topologia restituisce un grafico delle risorse di rete in una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="49442-104">Topology returns a graph of network resources in a virtual network.</span></span> <span data-ttu-id="49442-105">Il grafico illustra l'interconnessione tra le risorse per rappresentare in modo completo la connettività di rete.</span><span class="sxs-lookup"><span data-stu-id="49442-105">The graph depicts the interconnection between the resources to represent the end to end network connectivity.</span></span>

![Panoramica della topologia][1]

<span data-ttu-id="49442-107">Nel portale la topologia restituisce gli oggetti risorsa per ogni singola rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="49442-107">In the portal, Topology returns the resource objects on a per virtual network basis.</span></span> <span data-ttu-id="49442-108">Le relazioni sono rappresentate dalle linee tra le risorse all'esterno dell'area di Network Watcher, anche se non vengono visualizzate nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="49442-108">The relationships are depicted by lines between the resources Resources outside of the Network Watcher region, even if in the resource group will not be displayed.</span></span> <span data-ttu-id="49442-109">Le risorse restituite nella vista del portale sono un sottoinsieme di componenti di rete rappresentati in un grafico.</span><span class="sxs-lookup"><span data-stu-id="49442-109">The resources returned in the portal view are a subset of the networking components that are graphed.</span></span> <span data-ttu-id="49442-110">Per visualizzare l'elenco completo delle risorse di rete è possibile usare [PowerShell](network-watcher-topology-powershell.md) o [REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="49442-110">To see the full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span></span>

> [!NOTE]
> <span data-ttu-id="49442-111">È necessaria un'istanza di Network Watcher in ogni area in cui si desidera eseguire la topologia.</span><span class="sxs-lookup"><span data-stu-id="49442-111">An instance of Network Watcher is required in each region that you want to run Topology on.</span></span>

<span data-ttu-id="49442-112">Quando le risorse vengono restituite, la connessione tra di esse viene modellati in due relazioni.</span><span class="sxs-lookup"><span data-stu-id="49442-112">As resources are returned the connection between them are modeled under two relationships.</span></span>

- <span data-ttu-id="49442-113">**Contenimento** - Esempio: la rete virtuale contiene una subnet che contiene una scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="49442-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span></span>
- <span data-ttu-id="49442-114">**Associazione** - Esempio: una scheda NIC è associata a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="49442-114">**Associated** - Example: A NIC is associated with a VM</span></span>

### <a name="next-steps"></a><span data-ttu-id="49442-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="49442-115">Next steps</span></span>

<span data-ttu-id="49442-116">Le informazioni su come usare PowerShell per recuperare la vista della topologia sono disponibili in [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md) (Topologia di Network Watcher con PowerShell)</span><span class="sxs-lookup"><span data-stu-id="49442-116">Learn how to use PowerShell to retrieve the Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span></span>

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
