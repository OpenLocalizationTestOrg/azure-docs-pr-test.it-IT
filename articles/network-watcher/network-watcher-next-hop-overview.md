---
title: aaaIntroduction toonext hop Watcher di rete di Azure | Documenti Microsoft
description: "Questa pagina viene fornita una panoramica di hello Watcher di rete dalla capacità dell'hop successiva"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a><span data-ttu-id="fd66f-103">Hop toonext introduzione Watcher di rete di Azure</span><span class="sxs-lookup"><span data-stu-id="fd66f-103">Introduction toonext hop in Azure Network Watcher</span></span>

<span data-ttu-id="fd66f-104">Il traffico proveniente da una macchina virtuale viene inviato a destinazione tooa in base a route valide di hello associate a una scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="fd66f-104">Traffic from a VM is sent tooa destination based on hello effective routes associated with a NIC.</span></span> <span data-ttu-id="fd66f-105">Hop successivo Ottiene il tipo dell'hop successivo di hello e l'indirizzo IP di un pacchetto da una macchina virtuale specifica e una scheda di rete.</span><span class="sxs-lookup"><span data-stu-id="fd66f-105">Next hop gets hello next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="fd66f-106">In questo modo toodetermine se hello pacchetto è in corso destinazione toohello diretti o è holed traffico hello in nero.</span><span class="sxs-lookup"><span data-stu-id="fd66f-106">This helps toodetermine if hello packet is being directed toohello destination or is hello traffic being black holed.</span></span> <span data-ttu-id="fd66f-107">Una configurazione non corretta di route da hello utente, in cui il traffico di un percorso locale tooan diretti o da un dispositivo virtuale, può causare problemi di tooconnectivity.</span><span class="sxs-lookup"><span data-stu-id="fd66f-107">An improper configuration of routes by hello user, where a traffic is directed tooan on-premises location or a virtual appliance, can lead tooconnectivity issues.</span></span> <span data-ttu-id="fd66f-108">Hop successivo restituisce anche tabella di route hello associata all'hop successivo hello.</span><span class="sxs-lookup"><span data-stu-id="fd66f-108">Next hop also returns hello route table associated with hello next hop.</span></span> <span data-ttu-id="fd66f-109">Quando si eseguono query hop successivo itinerario hello è definito come una route definita dall'utente, verrà restituito tale route.</span><span class="sxs-lookup"><span data-stu-id="fd66f-109">When querying a next hop if hello route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="fd66f-110">In caso contrario l'hop successivo restituisce la route di sistema.</span><span class="sxs-lookup"><span data-stu-id="fd66f-110">Otherwise Next hop returns "System Route".</span></span>

![Panoramica dell'hop successivo][1]

<span data-ttu-id="fd66f-112">Hello seguito è riportato un elenco di tipi di hop successivi hello che possono essere restituiti quando si eseguono query hop successivo.</span><span class="sxs-lookup"><span data-stu-id="fd66f-112">hello following is a list of hello next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="fd66f-113">Internet</span><span class="sxs-lookup"><span data-stu-id="fd66f-113">Internet</span></span>
* <span data-ttu-id="fd66f-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="fd66f-114">VirtualAppliance</span></span>
* <span data-ttu-id="fd66f-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="fd66f-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="fd66f-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="fd66f-116">VnetLocal</span></span>
* <span data-ttu-id="fd66f-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="fd66f-117">HyperNetGateway</span></span>
* <span data-ttu-id="fd66f-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="fd66f-118">VnetPeering</span></span>
* <span data-ttu-id="fd66f-119">None</span><span class="sxs-lookup"><span data-stu-id="fd66f-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="fd66f-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fd66f-120">Next steps</span></span>

<span data-ttu-id="fd66f-121">Informazioni su come toofind hop successivo toouse problemi con la connettività di rete, visitare il sito [controllo hello dell'hop successivo in una macchina virtuale](network-watcher-check-next-hop-portal.md)</span><span class="sxs-lookup"><span data-stu-id="fd66f-121">Learn how toouse next hop toofind issues with network connectivity by visiting [Check hello next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













