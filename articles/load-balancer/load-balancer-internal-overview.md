---
title: servizio di bilanciamento del carico aaaInternal Panoramica | Documenti Microsoft
description: "Panoramica di bilanciamento del carico interno e delle relative funzionalità. Funzionamento di un servizio di bilanciamento del carico per gli endpoint interni di Azure e possibili scenari tooconfigure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="81c1d-103">Panoramica del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="81c1d-103">Internal load balancer overview</span></span>

<span data-ttu-id="81c1d-104">A differenza di hello Internet rivolto al bilanciamento del carico, bilanciamento del carico interno hello (ILB) indirizza il traffico tooresources solo all'interno del servizio cloud hello o tramite VPN tooaccess hello dell'infrastruttura di Azure.</span><span class="sxs-lookup"><span data-stu-id="81c1d-104">Unlike hello Internet facing load balancer, hello internal load balancer (ILB) directs traffic only tooresources inside hello cloud service or using VPN tooaccess hello Azure infrastructure.</span></span> <span data-ttu-id="81c1d-105">infrastruttura Hello limita accesso toohello con carico bilanciato indirizzi IP virtuali (VIP) di un servizio Cloud o una rete virtuale in modo che non siano mai esposto direttamente tooan Internet endpoint.</span><span class="sxs-lookup"><span data-stu-id="81c1d-105">hello infrastructure restricts access toohello load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed tooan Internet endpoint.</span></span> <span data-ttu-id="81c1d-106">Questo consente interno line-of-business (LOB) toorun di applicazioni in Azure e accesso dal cloud hello o da risorse locali.</span><span class="sxs-lookup"><span data-stu-id="81c1d-106">This enables internal line of business (LOB) applications toorun in Azure and be accessed from within hello cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="81c1d-107">Perché potrebbe servire il bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="81c1d-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="81c1d-108">Il bilanciamento del carico interno di Azure consente di bilanciare il carico tra macchine virtuali che si trovano in un servizio cloud o una rete virtuale nell'ambito di un'area.</span><span class="sxs-lookup"><span data-stu-id="81c1d-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="81c1d-109">Per informazioni sull'uso di hello e la configurazione di reti virtuali con un ambito regionale, vedere [reti virtuali regionali](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in hello blog di Azure.</span><span class="sxs-lookup"><span data-stu-id="81c1d-109">For information about hello use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in hello Azure blog.</span></span> <span data-ttu-id="81c1d-110">Le reti virtuali esistenti che sono state configurate per un gruppo di affinità non possono usare il bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="81c1d-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="81c1d-111">ILB consente hello seguenti tipi di bilanciamento del carico:</span><span class="sxs-lookup"><span data-stu-id="81c1d-111">ILB enables hello following types of load balancing:</span></span>

* <span data-ttu-id="81c1d-112">All'interno di un servizio cloud, macchine virtuali tooa set di macchine virtuali che risiedono all'interno di hello stesso servizio cloud (vedere la figura 1).</span><span class="sxs-lookup"><span data-stu-id="81c1d-112">Within a cloud service, from virtual machines tooa set of virtual machines that reside within hello same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="81c1d-113">All'interno di una rete virtuale, da macchine virtuali nel set di tooa hello rete virtuale di macchine virtuali che risiedono all'interno di hello stesso servizio cloud di hello virtuale di rete (vedere la figura 2).</span><span class="sxs-lookup"><span data-stu-id="81c1d-113">Within a virtual network, from virtual machines in hello virtual network tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 2).</span></span>
* <span data-ttu-id="81c1d-114">Per una rete virtuale cross-premise, dal set di tooa computer locale di macchine virtuali che risiedono all'interno di hello stesso servizio cloud di hello virtuale di rete (vedere la figura 3).</span><span class="sxs-lookup"><span data-stu-id="81c1d-114">For a cross-premises virtual network, from on-premises computers tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 3).</span></span>
* <span data-ttu-id="81c1d-115">Con connessione Internet applicazioni multilivello in cui i livelli di back-end hello non sono esposti a Internet, ma richiedono il bilanciamento del carico per il traffico dal livello di hello con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="81c1d-115">Internet-facing, multi-tier applications in which hello back-end tiers are not Internet-facing but require load balancing for traffic from hello Internet-facing tier.</span></span>
* <span data-ttu-id="81c1d-116">Bilanciamento del carico per applicazioni LOB ospitate in Azure senza la necessità di applicazioni software o componenti hardware aggiuntivi per il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="81c1d-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="81c1d-117">Tra i server locali nel set di hello di computer il cui traffico è a carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="81c1d-117">Including on-premises servers in hello set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="81c1d-118">Applicazioni multilivello con connessione Internet</span><span class="sxs-lookup"><span data-stu-id="81c1d-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="81c1d-119">livello web Hello ha endpoint con connessione Internet per client Internet e fa parte di un set con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="81c1d-119">hello web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="81c1d-120">servizio di bilanciamento del carico Hello distribuisce il traffico in ingresso dai client web per TCP porta 443 (HTTPS) toohello i server web.</span><span class="sxs-lookup"><span data-stu-id="81c1d-120">hello load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) toohello web servers.</span></span>

<span data-ttu-id="81c1d-121">server di database Hello sono protetti da un endpoint di bilanciamento del carico interno che i server web hello utilizzano per l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="81c1d-121">hello database servers are behind an ILB endpoint which hello web servers use for storage.</span></span> <span data-ttu-id="81c1d-122">Endpoint, il tipo di traffico con carico bilanciato tra i server di database hello nel set di bilanciamento del carico interno hello con bilanciamento del carico di servizio in questo database.</span><span class="sxs-lookup"><span data-stu-id="81c1d-122">This database service load balanced endpoint, which traffic is load balanced across hello database servers in hello ILB set.</span></span>

<span data-ttu-id="81c1d-123">Hello seguente immagine Mostra hello applicazione multilivello per Internet all'interno di hello stesso servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="81c1d-123">hello following image shows hello Internet facing multi-tier application within hello same cloud service.</span></span>

![Bilanciamento del carico interno di un singolo servizio cloud](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="81c1d-125">Figura 1. Applicazione multilivello con connessione Internet</span><span class="sxs-lookup"><span data-stu-id="81c1d-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="81c1d-126">È possibile inoltre utilizzare un'applicazione multilivello è quando hello ILB distribuito tooa un servizio cloud differente rispetto a un servizio consumer di hello per hello ILB hello.</span><span class="sxs-lookup"><span data-stu-id="81c1d-126">Another possible use for a multi-tier application is when hello ILB deployed tooa different cloud service than hello one consuming hello service for hello ILB.</span></span>

<span data-ttu-id="81c1d-127">Cloud services utilizzando hello stessa rete virtuale avranno accesso endpoint ILB toohello.</span><span class="sxs-lookup"><span data-stu-id="81c1d-127">Cloud services using hello same virtual network will have access toohello ILB endpoint.</span></span> <span data-ttu-id="81c1d-128">Hello seguente immagine vengono visualizzati i server web front-end in un servizio cloud diverso da hello database back-end e l'utilizzo di hello endpoint ILB all'interno di hello stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="81c1d-128">hello following image shows front-end web servers are in a different cloud service from hello database back-end and using hello ILB endpoint within hello same virtual network.</span></span>

![Bilanciamento del carico interno tra servizi cloud](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="81c1d-130">Figura 2. Server front-end in un altro servizio cloud</span><span class="sxs-lookup"><span data-stu-id="81c1d-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="81c1d-131">Applicazioni Intranet line-of-business</span><span class="sxs-lookup"><span data-stu-id="81c1d-131">Intranet line of business applications</span></span>

<span data-ttu-id="81c1d-132">Il traffico dai client nella rete locale hello viene bilanciato tra set hello del server LOB tramite rete tooAzure di connessione VPN.</span><span class="sxs-lookup"><span data-stu-id="81c1d-132">Traffic from clients on hello on-premises network get load-balanced across hello set of LOB servers using VPN connection tooAzure network.</span></span>

<span data-ttu-id="81c1d-133">computer client Hello avrà indirizzo IP tooan di accesso dal servizio VPN di Azure tramite VPN toosite punto.</span><span class="sxs-lookup"><span data-stu-id="81c1d-133">hello client machine will have access tooan IP address from Azure VPN service using point toosite VPN.</span></span> <span data-ttu-id="81c1d-134">Consente di hello utilizzare hello applicazione LOB ospitata dietro endpoint ILB hello.</span><span class="sxs-lookup"><span data-stu-id="81c1d-134">It allows hello use hello LOB application hosted behind hello ILB endpoint.</span></span>

![Interno il bilanciamento del carico tramite VPN toosite punto](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="81c1d-136">Figura 3 - applicazioni LOB ospitate dietro endpoint LB hello</span><span class="sxs-lookup"><span data-stu-id="81c1d-136">Figure 3 - LOB applications hosted behind hello LB endpoint</span></span>

<span data-ttu-id="81c1d-137">Un altro scenario hello LOB è una sito toosite VPN toohello rete virtuale in cui viene configurato l'endpoint di bilanciamento del carico interno hello toohave.</span><span class="sxs-lookup"><span data-stu-id="81c1d-137">Another scenario for hello LOB is toohave a site toosite VPN toohello virtual network where hello ILB endpoint is configured.</span></span> <span data-ttu-id="81c1d-138">In questo modo l'endpoint di rete traffico toobe indirizzato toohello ILB locale.</span><span class="sxs-lookup"><span data-stu-id="81c1d-138">This allows on-premises network traffic toobe routed toohello ILB endpoint.</span></span>

![Interno il bilanciamento del carico utilizzando toosite sito VPN](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="81c1d-140">Figura 4 - il traffico di rete locale indirizzata toohello ILB endpoint</span><span class="sxs-lookup"><span data-stu-id="81c1d-140">Figure 4 - On-premises network traffic routed toohello ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="81c1d-141">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="81c1d-141">Limitations</span></span>

<span data-ttu-id="81c1d-142">SNAT non è supportato dalle configurazioni del servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="81c1d-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="81c1d-143">Nel contesto di hello di questo documento, SNAT fa riferimento tooport simulazione origine NAT.</span><span class="sxs-lookup"><span data-stu-id="81c1d-143">In hello context of this document, SNAT refers tooport masquerading source  network address translation.</span></span>  <span data-ttu-id="81c1d-144">Si applica tooscenarios in una macchina virtuale in un pool di bilanciamento del carico richiede l'indirizzo IP del tooreach hello rispettivi interno bilanciamento del carico front-end.</span><span class="sxs-lookup"><span data-stu-id="81c1d-144">This applies tooscenarios where a VM in a load balancer pool needs tooreach hello respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="81c1d-145">Questo scenario non è supportato per il servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="81c1d-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="81c1d-146">Quando il flusso di hello è toohello con carico bilanciato macchina virtuale che ha avviato il flusso di hello, si verificheranno errori di connessione.</span><span class="sxs-lookup"><span data-stu-id="81c1d-146">Connection failures will occur when hello flow is load balanced toohello VM which originated hello flow.</span></span> <span data-ttu-id="81c1d-147">È necessario usare un servizio di bilanciamento del carico di tipo proxy per questi scenari.</span><span class="sxs-lookup"><span data-stu-id="81c1d-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81c1d-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="81c1d-148">Next Steps</span></span>

[<span data-ttu-id="81c1d-149">Supporto di Azure Resource Manager per Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="81c1d-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="81c1d-150">Introduzione alla configurazione del bilanciamento del carico Internet</span><span class="sxs-lookup"><span data-stu-id="81c1d-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="81c1d-151">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="81c1d-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="81c1d-152">Configurare una modalità di distribuzione del bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="81c1d-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="81c1d-153">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="81c1d-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
