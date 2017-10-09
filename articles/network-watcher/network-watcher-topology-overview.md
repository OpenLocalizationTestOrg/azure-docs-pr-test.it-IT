---
title: tootopology aaaIntroduction in Watcher di rete di Azure | Documenti Microsoft
description: "Questa pagina fornisce una panoramica delle funzionalità di topologia hello Watcher di rete"
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
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a><span data-ttu-id="51854-103">Introduzione tootopology in Watcher di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="51854-103">Introduction tootopology in Azure Network Watcher</span></span>

<span data-ttu-id="51854-104">La topologia restituisce un grafico delle risorse di rete in una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="51854-104">Topology returns a graph of network resources in a virtual network.</span></span> <span data-ttu-id="51854-105">grafico di Hello illustra l'interconnessione hello tra hello risorse toorepresent hello fine tooend la connettività di rete.</span><span class="sxs-lookup"><span data-stu-id="51854-105">hello graph depicts hello interconnection between hello resources toorepresent hello end tooend network connectivity.</span></span>

![Panoramica della topologia][1]

<span data-ttu-id="51854-107">Nel portale di hello topologia restituisce oggetti risorsa hello in una base di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="51854-107">In hello portal, Topology returns hello resource objects on a per virtual network basis.</span></span> <span data-ttu-id="51854-108">relazioni Hello sono rappresentate dalle linee tra risorse hello risorse all'esterno di area di hello Watcher di rete, anche se nella risorsa hello gruppo non verrà visualizzato.</span><span class="sxs-lookup"><span data-stu-id="51854-108">hello relationships are depicted by lines between hello resources Resources outside of hello Network Watcher region, even if in hello resource group will not be displayed.</span></span> <span data-ttu-id="51854-109">risorse di Hello restituite nella visualizzazione portale hello sono un subset di componenti che sono rappresentate hello.</span><span class="sxs-lookup"><span data-stu-id="51854-109">hello resources returned in hello portal view are a subset of hello networking components that are graphed.</span></span> <span data-ttu-id="51854-110">elenco completo di hello toosee delle risorse di rete è possibile utilizzare [PowerShell](network-watcher-topology-powershell.md) o [REST](network-watcher-topology-rest.md)</span><span class="sxs-lookup"><span data-stu-id="51854-110">toosee hello full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span></span>

> [!NOTE]
> <span data-ttu-id="51854-111">È necessaria un'istanza del controllo di rete in ogni area che si desidera includere toorun topologia.</span><span class="sxs-lookup"><span data-stu-id="51854-111">An instance of Network Watcher is required in each region that you want toorun Topology on.</span></span>

<span data-ttu-id="51854-112">Poiché le risorse vengono restituite connessione hello tra di essi vengono modellati in due relazioni.</span><span class="sxs-lookup"><span data-stu-id="51854-112">As resources are returned hello connection between them are modeled under two relationships.</span></span>

- <span data-ttu-id="51854-113">**Contenimento** - Esempio: la rete virtuale contiene una subnet che contiene una scheda di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="51854-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span></span>
- <span data-ttu-id="51854-114">**Associazione** - Esempio: una scheda NIC è associata a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="51854-114">**Associated** - Example: A NIC is associated with a VM</span></span>

### <a name="next-steps"></a><span data-ttu-id="51854-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="51854-115">Next steps</span></span>

<span data-ttu-id="51854-116">Informazioni su come toouse PowerShell tooretrieve hello topologia visualizzare visitando [topologia Watcher di rete con PowerShell](network-watcher-topology-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="51854-116">Learn how toouse PowerShell tooretrieve hello Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span></span>

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
