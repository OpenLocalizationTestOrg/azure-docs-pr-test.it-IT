---
title: Requisiti QoS per ExpressRoute | Documentazione Microsoft
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
ms.openlocfilehash: c097a9ccba91f59b323215d42d37e6d85e0981ce
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="9eed4-103">Requisiti ExpressRoute QoS</span><span class="sxs-lookup"><span data-stu-id="9eed4-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="9eed4-104">Skype per aziende dispone di diversi carichi di lavoro che richiedono la gestione QoS differenziata.</span><span class="sxs-lookup"><span data-stu-id="9eed4-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="9eed4-105">Se si prevede di utilizzare i servizi vocali tramite ExpressRoute, è necessario rispettare i requisiti descritti di seguito.</span><span class="sxs-lookup"><span data-stu-id="9eed4-105">If you plan to consume voice services through ExpressRoute, you should adhere to the requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="9eed4-106">I requisiti QoS si applicano solo ai peer Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9eed4-106">QoS requirements apply to the Microsoft peering only.</span></span> <span data-ttu-id="9eed4-107">I valori DSCP del traffico di rete ricevuti nel peer pubblico e nel peer privato di Azure saranno reimpostati su 0.</span><span class="sxs-lookup"><span data-stu-id="9eed4-107">The DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset to 0.</span></span> 
> 
> 

<span data-ttu-id="9eed4-108">La tabella seguente fornisce un elenco di contrassegni DSCP utilizzati da Skype per aziende.</span><span class="sxs-lookup"><span data-stu-id="9eed4-108">The following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="9eed4-109">Fare riferimento a [Gestione QoS per Skype per aziende](https://technet.microsoft.com/library/gg405409.aspx) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="9eed4-109">Refer to [Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="9eed4-110">**Classe di traffico**</span><span class="sxs-lookup"><span data-stu-id="9eed4-110">**Traffic Class**</span></span> | <span data-ttu-id="9eed4-111">**Modalità di gestione (contrassegno DSCP)**</span><span class="sxs-lookup"><span data-stu-id="9eed4-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="9eed4-112">**Carichi di lavoro di Skype per aziende**</span><span class="sxs-lookup"><span data-stu-id="9eed4-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9eed4-113">**Voice**</span><span class="sxs-lookup"><span data-stu-id="9eed4-113">**Voice**</span></span> |<span data-ttu-id="9eed4-114">ENTITY FRAMEWORK (46)</span><span class="sxs-lookup"><span data-stu-id="9eed4-114">EF (46)</span></span> |<span data-ttu-id="9eed4-115">Skype / voice di Lync</span><span class="sxs-lookup"><span data-stu-id="9eed4-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="9eed4-116">**Interattivo**</span><span class="sxs-lookup"><span data-stu-id="9eed4-116">**Interactive**</span></span> |<span data-ttu-id="9eed4-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="9eed4-117">AF41 (34)</span></span> |<span data-ttu-id="9eed4-118">Video, VBSS</span><span class="sxs-lookup"><span data-stu-id="9eed4-118">Video, VBSS</span></span> |
| <span data-ttu-id="9eed4-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="9eed4-119">AF21 (18)</span></span> |<span data-ttu-id="9eed4-120">Condivisione delle app</span><span class="sxs-lookup"><span data-stu-id="9eed4-120">App sharing</span></span> | |
| <span data-ttu-id="9eed4-121">**Default**</span><span class="sxs-lookup"><span data-stu-id="9eed4-121">**Default**</span></span> |<span data-ttu-id="9eed4-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="9eed4-122">AF11 (10)</span></span> |<span data-ttu-id="9eed4-123">Trasferimento di file</span><span class="sxs-lookup"><span data-stu-id="9eed4-123">File transfer</span></span> |
| <span data-ttu-id="9eed4-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="9eed4-124">CS0 (0)</span></span> |<span data-ttu-id="9eed4-125">Altro</span><span class="sxs-lookup"><span data-stu-id="9eed4-125">Anything else</span></span> | |

* <span data-ttu-id="9eed4-126">È necessario classificare i carichi di lavoro e contrassegnare i valori DSCP corretti.</span><span class="sxs-lookup"><span data-stu-id="9eed4-126">You should classify the workloads and mark the right DSCP values.</span></span> <span data-ttu-id="9eed4-127">Seguire le indicazioni fornite [qui](https://technet.microsoft.com/library/gg405409.aspx) su come impostare i contrassegni DSCP nella rete.</span><span class="sxs-lookup"><span data-stu-id="9eed4-127">Follow the guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how to set DSCP markings in your network.</span></span>
* <span data-ttu-id="9eed4-128">È necessario configurare e supportare più code di QoS nella rete.</span><span class="sxs-lookup"><span data-stu-id="9eed4-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="9eed4-129">La Voce deve essere una classe autonoma e ricevere il trattamento di Entity Framework specificato in RFC 3246.</span><span class="sxs-lookup"><span data-stu-id="9eed4-129">Voice must be a standalone class and receive the EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="9eed4-130">È possibile decidere il meccanismo di accodamento, i criteri di rilevamento della congestione e l’allocazione della larghezza di banda per ogni classe di traffico.</span><span class="sxs-lookup"><span data-stu-id="9eed4-130">You can decide the queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="9eed4-131">Tuttavia, è necessario mantenere il contrassegno DSCP per i carichi di lavoro di Skype per aziende.</span><span class="sxs-lookup"><span data-stu-id="9eed4-131">But, the DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="9eed4-132">Se si utilizzano i contrassegni DSCP non elencati sopra, ad esempio AF31 (26), è necessario riscrivere il valore DSCP su 0 prima di inviare il pacchetto a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9eed4-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value to 0 before sending the packet to Microsoft.</span></span> <span data-ttu-id="9eed4-133">Microsoft invia solo i pacchetti contrassegnati con il valore di DSCP illustrato nella tabella precedente.</span><span class="sxs-lookup"><span data-stu-id="9eed4-133">Microsoft only sends packets marked with the DSCP value shown in the above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9eed4-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9eed4-134">Next steps</span></span>
* <span data-ttu-id="9eed4-135">Fare riferimento ai requisiti per [Routing](expressroute-routing.md) e [NAT](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="9eed4-135">Refer to the requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="9eed4-136">Vedere i collegamenti seguenti per configurare la connessione ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="9eed4-136">See the following links to configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="9eed4-137">Creare un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9eed4-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="9eed4-138">Configurare il routing</span><span class="sxs-lookup"><span data-stu-id="9eed4-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="9eed4-139">Collegare una rete virtuale a un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="9eed4-139">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

