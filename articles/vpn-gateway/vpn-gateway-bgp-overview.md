---
title: Panoramica di BGP con i gateway VPN di Azure | Microsoft Docs
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
ms.openlocfilehash: 60d8dd45ecbd4a075721c25acadb21d4e2fd5448
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a><span data-ttu-id="f7271-103">Panoramica di BGP con i gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="f7271-103">Overview of BGP with Azure VPN Gateways</span></span>
<span data-ttu-id="f7271-104">Questo articolo fornisce una panoramica di BGP (Border Gateway Protocol) nei gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="f7271-104">This article provides an overview of BGP (Border Gateway Protocol) support in Azure VPN Gateways.</span></span>

<span data-ttu-id="f7271-105">BGP è il protocollo di routing standard comunemente usato in Internet per lo scambio di informazioni di routing e raggiungibilità tra due o più reti.</span><span class="sxs-lookup"><span data-stu-id="f7271-105">BGP is the standard routing protocol commonly used in the Internet to exchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="f7271-106">Quando viene usato nel contesto di reti virtuali di Azure, BGP consente ai gateway VPN di Azure e ai dispositivi VPN locali, detti peer BGP o router adiacenti, lo scambio di "route" che indicano a entrambi i gateway la disponibilità e la raggiungibilità di tali prefissi per il passaggio attraverso i gateway o i router coinvolti.</span><span class="sxs-lookup"><span data-stu-id="f7271-106">When used in the context of Azure Virtual Networks, BGP enables the Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, to exchange "routes" that will inform both gateways on the availability and reachability for those prefixes to go through the gateways or routers involved.</span></span> <span data-ttu-id="f7271-107">BGP può anche abilitare il routing di transito tra più reti propagando a tutti gli altri peer BGP le route che un gateway BGP apprende da un peer BGP.</span><span class="sxs-lookup"><span data-stu-id="f7271-107">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer to all other BGP peers.</span></span> 

## <a name="why-use-bgp"></a><span data-ttu-id="f7271-108">Perché usare BGP</span><span class="sxs-lookup"><span data-stu-id="f7271-108">Why use BGP?</span></span>
<span data-ttu-id="f7271-109">BGP è una funzionalità facoltativa che può essere usata con i gateway VPN di Azure basati su route.</span><span class="sxs-lookup"><span data-stu-id="f7271-109">BGP is an optional feature you can use with Azure Route-Based VPN gateways.</span></span> <span data-ttu-id="f7271-110">Prima di abilitare tale funzionalità, assicurarsi che i dispositivi VPN locali supportino BGP.</span><span class="sxs-lookup"><span data-stu-id="f7271-110">You should also make sure your on-premises VPN devices support BGP before you enable the feature.</span></span> <span data-ttu-id="f7271-111">È possibile continuare a usare i gateway VPN di Azure e i dispositivi VPN locali senza BGP.</span><span class="sxs-lookup"><span data-stu-id="f7271-111">You can continue to use Azure VPN gateways and your on-premises VPN devices without BGP.</span></span> <span data-ttu-id="f7271-112">In altre parole occorre scegliere tra l'uso delle route statiche, senza BGP, *oppure* l'uso del routing dinamico con BGP tra le reti e Azure.</span><span class="sxs-lookup"><span data-stu-id="f7271-112">It is the equivalent of using static routes (without BGP) *vs.* using dynamic routing with BGP between your networks and Azure.</span></span>

<span data-ttu-id="f7271-113">BGP offre nuove funzionalità e numerosi vantaggi, illustrati di seguito.</span><span class="sxs-lookup"><span data-stu-id="f7271-113">There are several advantages and new capabilities with BGP:</span></span>

### <a name="support-automatic-and-flexible-prefix-updates"></a><span data-ttu-id="f7271-114">Supporto per l'aggiornamento automatico e flessibile dei prefissi</span><span class="sxs-lookup"><span data-stu-id="f7271-114">Support automatic and flexible prefix updates</span></span>
<span data-ttu-id="f7271-115">Con BGP, è sufficiente dichiarare un prefisso minimo a un peer BGP specifico attraverso il tunnel VPN S2S IPsec.</span><span class="sxs-lookup"><span data-stu-id="f7271-115">With BGP, you only need to declare a minimum prefix to a specific BGP peer over the IPsec S2S VPN tunnel.</span></span> <span data-ttu-id="f7271-116">La dimensione minima consentita è quella di un prefisso dell'host (/32) dell'indirizzo IP del peer BGP per il dispositivo VPN locale.</span><span class="sxs-lookup"><span data-stu-id="f7271-116">It can be as small as a host prefix (/32) of the BGP peer IP address of your on-premises VPN device.</span></span> <span data-ttu-id="f7271-117">È possibile controllare quali prefissi di rete locale segnalare in Azure per consentire alla rete virtuale di Azure di accedere.</span><span class="sxs-lookup"><span data-stu-id="f7271-117">You can control which on-premises network prefixes you want to advertise to Azure to allow your Azure Virtual Network to access.</span></span>

<span data-ttu-id="f7271-118">È anche possibile segnalare prefissi più grandi, che possono includere alcuni dei prefissi di indirizzo della rete virtuale, come uno spazio di indirizzi IP privato di grandi dimensioni, ad esempio 10.0.0.0/8.</span><span class="sxs-lookup"><span data-stu-id="f7271-118">You can also advertise larger prefixes that may include some of your VNet address prefixes, such as a large private IP address space (for example, 10.0.0.0/8).</span></span> <span data-ttu-id="f7271-119">Si noti che i prefissi non possono essere identici ad alcuno dei prefissi della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="f7271-119">Note though the prefixes cannot be identical with any one of your VNet prefixes.</span></span> <span data-ttu-id="f7271-120">Le route identiche ai prefissi della rete virtuale verranno rifiutate.</span><span class="sxs-lookup"><span data-stu-id="f7271-120">Those routes identical to your VNet prefixes will be rejected.</span></span>

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a><span data-ttu-id="f7271-121">Supporto di più tunnel tra una rete virtuale e un sito locale con failover automatico basato su BGP</span><span class="sxs-lookup"><span data-stu-id="f7271-121">Support multiple tunnels between a VNet and an on-premises site with automatic failover based on BGP</span></span>
<span data-ttu-id="f7271-122">È possibile stabilire più connessioni tra la rete virtuale di Azure e i dispositivi VPN locali nella stessa località.</span><span class="sxs-lookup"><span data-stu-id="f7271-122">You can establish multiple connections between your Azure VNet and your on-premises VPN devices in the same location.</span></span> <span data-ttu-id="f7271-123">Questa funzionalità fornisce più tunnel, o percorsi, tra le due reti in una configurazione di tipo attivo/attivo.</span><span class="sxs-lookup"><span data-stu-id="f7271-123">This capability provides multiple tunnels (paths) between the two networks in an active-active configuration.</span></span> <span data-ttu-id="f7271-124">Se uno dei tunnel viene disconnesso, le route corrispondenti vengono ritirate tramite BGP e il traffico si sposta automaticamente nei tunnel restanti.</span><span class="sxs-lookup"><span data-stu-id="f7271-124">If one of the tunnels is disconnected, the corresponding routes will be withdrawn via BGP and the traffic automatically shifts to the remaining tunnels.</span></span>

<span data-ttu-id="f7271-125">Il diagramma seguente mostra un esempio semplice di questa configurazione a disponibilità elevata:</span><span class="sxs-lookup"><span data-stu-id="f7271-125">The following diagram shows a simple example of this highly available setup:</span></span>

![Più percorsi attivi](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a><span data-ttu-id="f7271-127">Supporto del routing di transito tra le reti locali e più reti virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="f7271-127">Support transit routing between your on-premises networks and multiple Azure VNets</span></span>
<span data-ttu-id="f7271-128">BGP consente a più gateway di apprendere e propagare i prefissi da reti diverse, connesse sia direttamente che indirettamente.</span><span class="sxs-lookup"><span data-stu-id="f7271-128">BGP enables multiple gateways to learn and propagate prefixes from different networks, whether they are directly or indirectly connected.</span></span> <span data-ttu-id="f7271-129">Questo consente il routing di transito con i gateway VPN di Azure tra i siti locali o tra più reti virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="f7271-129">This can enable transit routing with Azure VPN gateways between your on-premises sites or across multiple Azure Virtual Networks.</span></span>

<span data-ttu-id="f7271-130">Il diagramma seguente illustra un esempio di una topologia multihop con più percorsi che possono far passare il traffico tra le due reti locali tramite i gateway VPN di Azure all'interno di reti Microsoft:</span><span class="sxs-lookup"><span data-stu-id="f7271-130">The following diagram shows an example of a multi-hop topology with multiple paths that can transit traffic between the two on-premises networks through Azure VPN gateways within the Microsoft Networks:</span></span>

![Transito multihop](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a><span data-ttu-id="f7271-132">DOMANDE FREQUENTI SU BGP</span><span class="sxs-lookup"><span data-stu-id="f7271-132">BGP FAQ</span></span>
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="f7271-133">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f7271-133">Next steps</span></span>
<span data-ttu-id="f7271-134">Per i passaggi di configurazione di BGP per le connessioni cross-premise e tra reti virtuali, vedere [Introduzione a BGP nei gateway VPN di Azure](vpn-gateway-bgp-resource-manager-ps.md) .</span><span class="sxs-lookup"><span data-stu-id="f7271-134">See [Getting started with BGP on Azure VPN gateways](vpn-gateway-bgp-resource-manager-ps.md) for steps to configure BGP for your cross-premises and VNet-to-VNet connections.</span></span>

