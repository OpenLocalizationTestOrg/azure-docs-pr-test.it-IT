---
title: Requisiti di ExpressRoute aaaQoS | Documenti Microsoft
description: Questa pagina fornisce informazioni dettagliate sui requisiti per la configurazione e la gestione di QoS per circuiti ExpressRoute.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="8a6ef-103">Requisiti ExpressRoute QoS</span><span class="sxs-lookup"><span data-stu-id="8a6ef-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="8a6ef-104">Skype per aziende dispone di diversi carichi di lavoro che richiedono la gestione QoS differenziata.</span><span class="sxs-lookup"><span data-stu-id="8a6ef-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="8a6ef-105">Se si prevede di servizi di vocale tooconsume tramite ExpressRoute, è necessario rispettare i requisiti di toohello descritti di seguito.</span><span class="sxs-lookup"><span data-stu-id="8a6ef-105">If you plan tooconsume voice services through ExpressRoute, you should adhere toohello requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="8a6ef-106">Requisiti di qualità del applicare toohello peering solo Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8a6ef-106">QoS requirements apply toohello Microsoft peering only.</span></span> <span data-ttu-id="8a6ef-107">i valori DSCP Hello in traffico di rete ricevuti su peering pubblico di Azure e peering privato di Azure sarà too0 reimpostazione.</span><span class="sxs-lookup"><span data-stu-id="8a6ef-107">hello DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset too0.</span></span> 
> 
> 

<span data-ttu-id="8a6ef-108">Hello nella tabella seguente fornisce un elenco delle indicazioni DSCP utilizzato da Skype for Business.</span><span class="sxs-lookup"><span data-stu-id="8a6ef-108">hello following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="8a6ef-109">Fare riferimento troppo[gestione QoS per Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="8a6ef-109">Refer too[Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="8a6ef-110">**Classe di traffico**</span><span class="sxs-lookup"><span data-stu-id="8a6ef-110">**Traffic Class**</span></span> | <span data-ttu-id="8a6ef-111">**Modalità di gestione (contrassegno DSCP)**</span><span class="sxs-lookup"><span data-stu-id="8a6ef-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="8a6ef-112">**Carichi di lavoro di Skype per aziende**</span><span class="sxs-lookup"><span data-stu-id="8a6ef-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8a6ef-113">**Voice**</span><span class="sxs-lookup"><span data-stu-id="8a6ef-113">**Voice**</span></span> |<span data-ttu-id="8a6ef-114">ENTITY FRAMEWORK (46)</span><span class="sxs-lookup"><span data-stu-id="8a6ef-114">EF (46)</span></span> |<span data-ttu-id="8a6ef-115">Skype / voice di Lync</span><span class="sxs-lookup"><span data-stu-id="8a6ef-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="8a6ef-116">**Interattivo**</span><span class="sxs-lookup"><span data-stu-id="8a6ef-116">**Interactive**</span></span> |<span data-ttu-id="8a6ef-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="8a6ef-117">AF41 (34)</span></span> |<span data-ttu-id="8a6ef-118">Video, VBSS</span><span class="sxs-lookup"><span data-stu-id="8a6ef-118">Video, VBSS</span></span> |
| <span data-ttu-id="8a6ef-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="8a6ef-119">AF21 (18)</span></span> |<span data-ttu-id="8a6ef-120">Condivisione delle app</span><span class="sxs-lookup"><span data-stu-id="8a6ef-120">App sharing</span></span> | |
| <span data-ttu-id="8a6ef-121">**Default**</span><span class="sxs-lookup"><span data-stu-id="8a6ef-121">**Default**</span></span> |<span data-ttu-id="8a6ef-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="8a6ef-122">AF11 (10)</span></span> |<span data-ttu-id="8a6ef-123">Trasferimento di file</span><span class="sxs-lookup"><span data-stu-id="8a6ef-123">File transfer</span></span> |
| <span data-ttu-id="8a6ef-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="8a6ef-124">CS0 (0)</span></span> |<span data-ttu-id="8a6ef-125">Altro</span><span class="sxs-lookup"><span data-stu-id="8a6ef-125">Anything else</span></span> | |

* <span data-ttu-id="8a6ef-126">È consigliabile classificare i carichi di lavoro hello e contrassegnare i valori DSCP hello destra.</span><span class="sxs-lookup"><span data-stu-id="8a6ef-126">You should classify hello workloads and mark hello right DSCP values.</span></span> <span data-ttu-id="8a6ef-127">Seguire indicazioni hello fornite [qui](https://technet.microsoft.com/library/gg405409.aspx) su come contrassegni DSCP tooset nella rete.</span><span class="sxs-lookup"><span data-stu-id="8a6ef-127">Follow hello guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how tooset DSCP markings in your network.</span></span>
* <span data-ttu-id="8a6ef-128">È necessario configurare e supportare più code di QoS nella rete.</span><span class="sxs-lookup"><span data-stu-id="8a6ef-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="8a6ef-129">Voce deve essere una classe autonoma e ricevono un trattamento EF hello specificato nella RFC 3246.</span><span class="sxs-lookup"><span data-stu-id="8a6ef-129">Voice must be a standalone class and receive hello EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="8a6ef-130">È possibile decidere hello meccanismo, criteri di rilevamento di congestione e allocazione della larghezza di banda per ogni classe di traffico di Accodamento.</span><span class="sxs-lookup"><span data-stu-id="8a6ef-130">You can decide hello queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="8a6ef-131">Tuttavia, hello il contrassegno DSCP per Skype per carichi di lavoro di Business deve essere mantenuto.</span><span class="sxs-lookup"><span data-stu-id="8a6ef-131">But, hello DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="8a6ef-132">Se si usano i contrassegni DSCP non elencati in precedenza, ad esempio AF31 (26), è necessario riscrivere questa too0 valore DSCP prima dell'invio tooMicrosoft pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="8a6ef-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value too0 before sending hello packet tooMicrosoft.</span></span> <span data-ttu-id="8a6ef-133">Microsoft invia solo i pacchetti contrassegnati con hello valore DSCP mostrato in hello precedente tabella.</span><span class="sxs-lookup"><span data-stu-id="8a6ef-133">Microsoft only sends packets marked with hello DSCP value shown in hello above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8a6ef-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a6ef-134">Next steps</span></span>
* <span data-ttu-id="8a6ef-135">Consultare i requisiti di toohello per [Routing](expressroute-routing.md) e [NAT](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="8a6ef-135">Refer toohello requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="8a6ef-136">Vedere l'esempio hello collega tooconfigure la connessione ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="8a6ef-136">See hello following links tooconfigure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="8a6ef-137">Creare un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="8a6ef-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="8a6ef-138">Configurare il routing</span><span class="sxs-lookup"><span data-stu-id="8a6ef-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="8a6ef-139">Collegare un circuito ExpressRoute di tooan rete virtuale</span><span class="sxs-lookup"><span data-stu-id="8a6ef-139">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

