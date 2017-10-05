---
title: Panoramica del bilanciamento del carico interno | Documentazione Microsoft
description: "Panoramica del bilanciamento del carico interno e delle relative funzionalità. Modalità di funzionamento del bilanciamento del carico di Azure e possibili scenari per la configurazione di endpoint interni"
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
ms.openlocfilehash: d324aaf8ec2c8766d5cf11452158d14c19cba4d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="596fa-103">Panoramica del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="596fa-103">Internal load balancer overview</span></span>

<span data-ttu-id="596fa-104">A differenza del bilanciamento del carico Internet, il bilanciamento del carico interno indirizza il traffico solo alle risorse all'interno del servizio cloud o che accedono all'infrastruttura di Azure tramite una rete VPN.</span><span class="sxs-lookup"><span data-stu-id="596fa-104">Unlike the Internet facing load balancer, the internal load balancer (ILB) directs traffic only to resources inside the cloud service or using VPN to access the Azure infrastructure.</span></span> <span data-ttu-id="596fa-105">L'infrastruttura limita l'accesso agli indirizzi IP virtuali con carico bilanciato di un servizio cloud o una rete virtuale, senza esposizione diretta a un endpoint Internet.</span><span class="sxs-lookup"><span data-stu-id="596fa-105">The infrastructure restricts access to the load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed to an Internet endpoint.</span></span> <span data-ttu-id="596fa-106">Ciò consente di eseguire le applicazioni line-of-business (LOB) interne in Azure e di accedervi dal cloud o dalle risorse locali.</span><span class="sxs-lookup"><span data-stu-id="596fa-106">This enables internal line of business (LOB) applications to run in Azure and be accessed from within the cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="596fa-107">Perché potrebbe servire il bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="596fa-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="596fa-108">Il bilanciamento del carico interno di Azure consente di bilanciare il carico tra macchine virtuali che si trovano in un servizio cloud o una rete virtuale nell'ambito di un'area.</span><span class="sxs-lookup"><span data-stu-id="596fa-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="596fa-109">Per informazioni sull'uso e sulla configurazione di reti virtuali nell'ambito di un'area, vedere [Reti virtuali di area](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) nel blog di Azure.</span><span class="sxs-lookup"><span data-stu-id="596fa-109">For information about the use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in the Azure blog.</span></span> <span data-ttu-id="596fa-110">Le reti virtuali esistenti che sono state configurate per un gruppo di affinità non possono usare il bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="596fa-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="596fa-111">Il bilanciamento del carico interno permette di bilanciare i tipi di carico seguenti:</span><span class="sxs-lookup"><span data-stu-id="596fa-111">ILB enables the following types of load balancing:</span></span>

* <span data-ttu-id="596fa-112">In un servizio cloud, dalle macchine virtuali a un set di macchine virtuali che si trovano nello stesso servizio cloud (vedere la figura 1).</span><span class="sxs-lookup"><span data-stu-id="596fa-112">Within a cloud service, from virtual machines to a set of virtual machines that reside within the same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="596fa-113">In una rete virtuale, dalle macchine virtuali nella rete virtuale a un set di macchine virtuali che si trovano nello stesso servizio cloud della rete virtuale (vedere la figura 2).</span><span class="sxs-lookup"><span data-stu-id="596fa-113">Within a virtual network, from virtual machines in the virtual network to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 2).</span></span>
* <span data-ttu-id="596fa-114">Per una rete virtuale cross-premise, dai computer locali a un set di macchine virtuali che si trovano nello stesso servizio cloud della rete virtuale (vedere la figura 3).</span><span class="sxs-lookup"><span data-stu-id="596fa-114">For a cross-premises virtual network, from on-premises computers to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 3).</span></span>
* <span data-ttu-id="596fa-115">Applicazioni multilivello con connessione Internet in cui i livelli di back-end non sono connessi a Internet, ma che richiedono il bilanciamento del carico per il traffico dal livello con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="596fa-115">Internet-facing, multi-tier applications in which the back-end tiers are not Internet-facing but require load balancing for traffic from the Internet-facing tier.</span></span>
* <span data-ttu-id="596fa-116">Bilanciamento del carico per applicazioni LOB ospitate in Azure senza la necessità di applicazioni software o componenti hardware aggiuntivi per il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="596fa-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="596fa-117">Inserimento di server locali nel set di computer il cui traffico viene sottoposto a bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="596fa-117">Including on-premises servers in the set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="596fa-118">Applicazioni multilivello con connessione Internet</span><span class="sxs-lookup"><span data-stu-id="596fa-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="596fa-119">Il livello Web presenta endpoint con connessione Internet per i client Internet e fa parte di un set con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="596fa-119">The web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="596fa-120">Il bilanciamento del carico distribuisce il traffico in ingresso dai client Web per la porta TCP 443 (HTTPS) ai server Web.</span><span class="sxs-lookup"><span data-stu-id="596fa-120">The load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) to the web servers.</span></span>

<span data-ttu-id="596fa-121">I server di database si servono di un endpoint di bilanciamento del carico interno usato dai server Web per l'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="596fa-121">The database servers are behind an ILB endpoint which the web servers use for storage.</span></span> <span data-ttu-id="596fa-122">Questo database serve l'endpoint con carico bilanciato, il cui traffico viene sottoposto a bilanciamento del carico tra i server di database nel set di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="596fa-122">This database service load balanced endpoint, which traffic is load balanced across the database servers in the ILB set.</span></span>

<span data-ttu-id="596fa-123">L'immagine seguente illustra l'applicazione multilivello con connessione Internet all'interno dello stesso servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="596fa-123">The following image shows the Internet facing multi-tier application within the same cloud service.</span></span>

![Bilanciamento del carico interno di un singolo servizio cloud](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="596fa-125">Figura 1. Applicazione multilivello con connessione Internet</span><span class="sxs-lookup"><span data-stu-id="596fa-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="596fa-126">Un altro possibile uso per un'applicazione multilivello consiste nella distribuzione del bilanciamento del carico interno in un servizio cloud diverso rispetto a quello che utilizza il servizio per il bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="596fa-126">Another possible use for a multi-tier application is when the ILB deployed to a different cloud service than the one consuming the service for the ILB.</span></span>

<span data-ttu-id="596fa-127">I servizi cloud che usano la stessa rete virtuale avranno accesso all'endpoint di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="596fa-127">Cloud services using the same virtual network will have access to the ILB endpoint.</span></span> <span data-ttu-id="596fa-128">Nella figura seguente è possibile vedere che i server Web front-end si trovano in un servizio cloud diverso rispetto al back-end di database e usano l'endpoint di bilanciamento del carico interno nella stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="596fa-128">The following image shows front-end web servers are in a different cloud service from the database back-end and using the ILB endpoint within the same virtual network.</span></span>

![Bilanciamento del carico interno tra servizi cloud](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="596fa-130">Figura 2. Server front-end in un altro servizio cloud</span><span class="sxs-lookup"><span data-stu-id="596fa-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="596fa-131">Applicazioni Intranet line-of-business</span><span class="sxs-lookup"><span data-stu-id="596fa-131">Intranet line of business applications</span></span>

<span data-ttu-id="596fa-132">Il traffico dai client nella rete locale viene sottoposto a bilanciamento del carico nel set di server line-of-business usando la connessione VPN alla rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="596fa-132">Traffic from clients on the on-premises network get load-balanced across the set of LOB servers using VPN connection to Azure network.</span></span>

<span data-ttu-id="596fa-133">I client avranno accesso a un indirizzo IP dal servizio VPN di Azure tramite una connessione VPN da punto a sito.</span><span class="sxs-lookup"><span data-stu-id="596fa-133">The client machine will have access to an IP address from Azure VPN service using point to site VPN.</span></span> <span data-ttu-id="596fa-134">È quindi possibile usare l'applicazione LOB ospitata dietro l'endpoint di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="596fa-134">It allows the use the LOB application hosted behind the ILB endpoint.</span></span>

![Bilanciamento del carico interno tramite VPN da punto a sito](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="596fa-136">Figura 3. Applicazioni LOB ospitate dietro l'endpoint di bilanciamento carico</span><span class="sxs-lookup"><span data-stu-id="596fa-136">Figure 3 - LOB applications hosted behind the LB endpoint</span></span>

<span data-ttu-id="596fa-137">Un altro scenario di tipo line-of-business prevede l'uso di una rete VPN da sito a sito per la connessione alla rete virtuale in cui è stato configurato l'endpoint di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="596fa-137">Another scenario for the LOB is to have a site to site VPN to the virtual network where the ILB endpoint is configured.</span></span> <span data-ttu-id="596fa-138">In questo modo, il traffico di rete locale può essere instradato all'endpoint di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="596fa-138">This allows on-premises network traffic to be routed to the ILB endpoint.</span></span>

![Bilanciamento del carico interno tramite VPN da sito a sito](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="596fa-140">Figura 4. Il traffico di rete locale può essere instradato all'endpoint di bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="596fa-140">Figure 4 - On-premises network traffic routed to the ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="596fa-141">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="596fa-141">Limitations</span></span>

<span data-ttu-id="596fa-142">SNAT non è supportato dalle configurazioni del servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="596fa-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="596fa-143">Nel contesto di questo documento, SNAT fa riferimento alla traduzione dell'indirizzo di rete di origine mascherato della porta.</span><span class="sxs-lookup"><span data-stu-id="596fa-143">In the context of this document, SNAT refers to port masquerading source  network address translation.</span></span>  <span data-ttu-id="596fa-144">Questo vale per gli scenari in cui una macchina virtuale in un pool di bilanciamento del carico deve raggiungere l'indirizzo IP front-end del rispettivo servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="596fa-144">This applies to scenarios where a VM in a load balancer pool needs to reach the respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="596fa-145">Questo scenario non è supportato per il servizio di bilanciamento del carico interno.</span><span class="sxs-lookup"><span data-stu-id="596fa-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="596fa-146">Si verificheranno errori di connessione una volta eseguito il bilanciamento del carico del flusso sulla macchina virtuale che ha originato il flusso.</span><span class="sxs-lookup"><span data-stu-id="596fa-146">Connection failures will occur when the flow is load balanced to the VM which originated the flow.</span></span> <span data-ttu-id="596fa-147">È necessario usare un servizio di bilanciamento del carico di tipo proxy per questi scenari.</span><span class="sxs-lookup"><span data-stu-id="596fa-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="596fa-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="596fa-148">Next Steps</span></span>

[<span data-ttu-id="596fa-149">Supporto di Azure Resource Manager per Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="596fa-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="596fa-150">Introduzione alla configurazione del bilanciamento del carico Internet</span><span class="sxs-lookup"><span data-stu-id="596fa-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="596fa-151">Introduzione alla configurazione del bilanciamento del carico interno</span><span class="sxs-lookup"><span data-stu-id="596fa-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="596fa-152">Configurare una modalità di distribuzione del bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="596fa-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="596fa-153">Configurare le impostazioni del timeout di inattività TCP per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="596fa-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
