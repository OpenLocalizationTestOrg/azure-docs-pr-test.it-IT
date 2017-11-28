---
title: aaaOverview di BGP con gateway VPN di Azure | Documenti Microsoft
description: Questo articolo fornisce una panoramica di BGP con i gateway VPN di Azure.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: f8c3985c-c128-4f34-835c-0e88742bf36e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/12/2017
ms.author: yushwang
ms.openlocfilehash: ced3f77ecd791c84fb72b96447e839be3bf94846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a><span data-ttu-id="5f6e9-103">Panoramica di BGP con i gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="5f6e9-103">Overview of BGP with Azure VPN Gateways</span></span>
<span data-ttu-id="5f6e9-104">Questo articolo fornisce una panoramica di BGP (Border Gateway Protocol) nei gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-104">This article provides an overview of BGP (Border Gateway Protocol) support in Azure VPN Gateways.</span></span>

<span data-ttu-id="5f6e9-105">BGP è hello protocollo di routing standard comunemente utilizzato nelle hello Internet tooexchange routing e raggiungibilità informazioni tra due o più reti.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-105">BGP is hello standard routing protocol commonly used in hello Internet tooexchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="5f6e9-106">Quando usata nel contesto di hello di reti virtuali di Azure, il protocollo BGP Abilita gateway VPN di Azure hello e i dispositivi VPN locali, chiamati peer BGP o elementi adiacenti, tooexchange "Invia" che indicherà entrambi i gateway su disponibilità hello e raggiungibilità per quelli i prefissi toogo tramite gateway hello o router coinvolti.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-106">When used in hello context of Azure Virtual Networks, BGP enables hello Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, tooexchange "routes" that will inform both gateways on hello availability and reachability for those prefixes toogo through hello gateways or routers involved.</span></span> <span data-ttu-id="5f6e9-107">BGP inoltre è possibile abilitare il routing di transito tra più reti mediante propagazione di route, un gateway BGP apprende da uno tooall peer BGP altri peer BGP.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-107">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer tooall other BGP peers.</span></span> 

## <a name="why-use-bgp"></a><span data-ttu-id="5f6e9-108">Perché usare BGP</span><span class="sxs-lookup"><span data-stu-id="5f6e9-108">Why use BGP?</span></span>
<span data-ttu-id="5f6e9-109">BGP è una funzionalità facoltativa che può essere usata con i gateway VPN di Azure basati su route.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-109">BGP is an optional feature you can use with Azure Route-Based VPN gateways.</span></span> <span data-ttu-id="5f6e9-110">Assicurarsi inoltre che il dispositivo VPN locale supporta BGP prima di abilitare funzionalità hello.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-110">You should also make sure your on-premises VPN devices support BGP before you enable hello feature.</span></span> <span data-ttu-id="5f6e9-111">È possibile continuare toouse i gateway VPN di Azure e i dispositivi VPN locali senza BGP.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-111">You can continue toouse Azure VPN gateways and your on-premises VPN devices without BGP.</span></span> <span data-ttu-id="5f6e9-112">È hello equivalente di utilizzo delle route statiche (senza BGP) *e* con routing dinamico con il protocollo BGP tra Azure e le reti.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-112">It is hello equivalent of using static routes (without BGP) *vs.* using dynamic routing with BGP between your networks and Azure.</span></span>

<span data-ttu-id="5f6e9-113">BGP offre nuove funzionalità e numerosi vantaggi, illustrati di seguito.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-113">There are several advantages and new capabilities with BGP:</span></span>

### <a name="support-automatic-and-flexible-prefix-updates"></a><span data-ttu-id="5f6e9-114">Supporto per l'aggiornamento automatico e flessibile dei prefissi</span><span class="sxs-lookup"><span data-stu-id="5f6e9-114">Support automatic and flexible prefix updates</span></span>
<span data-ttu-id="5f6e9-115">Con il protocollo BGP, è necessario solo un peer BGP minima prefisso specifico tooa toodeclare tramite tunnel VPN S2S IPsec hello.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-115">With BGP, you only need toodeclare a minimum prefix tooa specific BGP peer over hello IPsec S2S VPN tunnel.</span></span> <span data-ttu-id="5f6e9-116">Può essere più piccolo di un prefisso dell'host (/ 32) di hello indirizzo IP del peer BGP del dispositivo VPN locale.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-116">It can be as small as a host prefix (/32) of hello BGP peer IP address of your on-premises VPN device.</span></span> <span data-ttu-id="5f6e9-117">È possibile controllare quale locale i prefissi di rete desiderata tooadvertise tooAzure tooallow tooaccess la rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-117">You can control which on-premises network prefixes you want tooadvertise tooAzure tooallow your Azure Virtual Network tooaccess.</span></span>

<span data-ttu-id="5f6e9-118">È anche possibile segnalare prefissi più grandi, che possono includere alcuni dei prefissi di indirizzo della rete virtuale, come uno spazio di indirizzi IP privato di grandi dimensioni, ad esempio 10.0.0.0/8.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-118">You can also advertise larger prefixes that may include some of your VNet address prefixes, such as a large private IP address space (for example, 10.0.0.0/8).</span></span> <span data-ttu-id="5f6e9-119">Si noti anche se i prefissi di hello non possono essere identici con uno qualsiasi dei prefissi di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-119">Note though hello prefixes cannot be identical with any one of your VNet prefixes.</span></span> <span data-ttu-id="5f6e9-120">Tali prefissi di rete virtuale tooyour identiche delle route verranno rifiutate.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-120">Those routes identical tooyour VNet prefixes will be rejected.</span></span>

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a><span data-ttu-id="5f6e9-121">Supporto di più tunnel tra una rete virtuale e un sito locale con failover automatico basato su BGP</span><span class="sxs-lookup"><span data-stu-id="5f6e9-121">Support multiple tunnels between a VNet and an on-premises site with automatic failover based on BGP</span></span>
<span data-ttu-id="5f6e9-122">È possibile stabilire più connessioni tra i dispositivi VPN locali e di rete virtuale di Azure in hello nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-122">You can establish multiple connections between your Azure VNet and your on-premises VPN devices in hello same location.</span></span> <span data-ttu-id="5f6e9-123">Questa funzionalità fornisce più tunnel (percorsi) tra due reti di hello in una configurazione attivo-attivo.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-123">This capability provides multiple tunnels (paths) between hello two networks in an active-active configuration.</span></span> <span data-ttu-id="5f6e9-124">Se uno dei tunnel hello è disconnessa, verranno ritirate route corrispondente hello tramite il protocollo BGP e traffico hello viene spostato automaticamente toohello rimanenti tunnel.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-124">If one of hello tunnels is disconnected, hello corresponding routes will be withdrawn via BGP and hello traffic automatically shifts toohello remaining tunnels.</span></span>

<span data-ttu-id="5f6e9-125">Hello seguente diagramma illustra un semplice esempio di questo programma di installazione a disponibilità elevata:</span><span class="sxs-lookup"><span data-stu-id="5f6e9-125">hello following diagram shows a simple example of this highly available setup:</span></span>

![Più percorsi attivi](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a><span data-ttu-id="5f6e9-127">Supporto del routing di transito tra le reti locali e più reti virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="5f6e9-127">Support transit routing between your on-premises networks and multiple Azure VNets</span></span>
<span data-ttu-id="5f6e9-128">BGP consente a più gateway toolearn e propagare i prefissi da reti diverse, se sono direttamente o indirettamente collegati.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-128">BGP enables multiple gateways toolearn and propagate prefixes from different networks, whether they are directly or indirectly connected.</span></span> <span data-ttu-id="5f6e9-129">Questo consente il routing di transito con i gateway VPN di Azure tra i siti locali o tra più reti virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-129">This can enable transit routing with Azure VPN gateways between your on-premises sites or across multiple Azure Virtual Networks.</span></span>

<span data-ttu-id="5f6e9-130">Hello diagramma seguente viene illustrato un esempio di una topologia di multi-hop con percorsi multipli che possono transito del traffico tra reti locali due hello attraverso il gateway VPN di Azure all'interno di Networks Microsoft hello:</span><span class="sxs-lookup"><span data-stu-id="5f6e9-130">hello following diagram shows an example of a multi-hop topology with multiple paths that can transit traffic between hello two on-premises networks through Azure VPN gateways within hello Microsoft Networks:</span></span>

![Transito multihop](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a><span data-ttu-id="5f6e9-132">DOMANDE FREQUENTI SU BGP</span><span class="sxs-lookup"><span data-stu-id="5f6e9-132">BGP FAQ</span></span>
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="5f6e9-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5f6e9-133">Next steps</span></span>
<span data-ttu-id="5f6e9-134">Vedere [introduzione BGP nel gateway VPN di Azure](vpn-gateway-bgp-resource-manager-ps.md) per passaggi tooconfigure BGP per le connessioni di rete virtuale a cross-premise.</span><span class="sxs-lookup"><span data-stu-id="5f6e9-134">See [Getting started with BGP on Azure VPN gateways](vpn-gateway-bgp-resource-manager-ps.md) for steps tooconfigure BGP for your cross-premises and VNet-to-VNet connections.</span></span>

