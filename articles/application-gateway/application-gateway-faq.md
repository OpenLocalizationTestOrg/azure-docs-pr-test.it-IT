---
title: Domande frequenti sul gateway applicazione di Azure | Microsoft Docs
description: Questa pagina offre risposte alle domande frequenti sul gateway applicazione di Azure
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 4e6244d92f41e0aa5c8a70db0db2881036984247
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a><span data-ttu-id="3946f-103">Domande frequenti sul gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="3946f-103">Frequently asked questions for Application Gateway</span></span>

## <a name="general"></a><span data-ttu-id="3946f-104">Generale</span><span class="sxs-lookup"><span data-stu-id="3946f-104">General</span></span>

<span data-ttu-id="3946f-105">**D. Che cos'è il gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="3946f-105">**Q. What is Application Gateway?**</span></span>

<span data-ttu-id="3946f-106">Il gateway applicazione di Azure è un servizio di controller per la distribuzione di applicazioni (ADC) con numerose funzionalità di bilanciamento del carico di livello 7.</span><span class="sxs-lookup"><span data-stu-id="3946f-106">Azure Application Gateway is an Application Delivery Controller (ADC) as a service, offering various layer 7 load balancing capabilities for your applications.</span></span> <span data-ttu-id="3946f-107">Offre un servizio altamente disponibile e scalabile completamente gestito da Azure.</span><span class="sxs-lookup"><span data-stu-id="3946f-107">It offers highly available and scalable service, which is fully managed by Azure.</span></span>

<span data-ttu-id="3946f-108">**D. Quali funzionalità supporta il gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="3946f-108">**Q. What features does Application Gateway support?**</span></span>

<span data-ttu-id="3946f-109">Application Gateway supporta l'offload SSL e SSL end-to-end, web application firewall, affinità della sessione basata su cookie, routing basato su percorso url, hosting multisito e altro.</span><span class="sxs-lookup"><span data-stu-id="3946f-109">Application Gateway supports SSL offloading and end to end SSL, Web Application Firewall, cookie-based session affinity, url path-based routing, multi site hosting, and others.</span></span> <span data-ttu-id="3946f-110">Per un elenco completo delle funzionalità supportate, vedere l'[introduzione al gateway applicazione](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="3946f-110">For a full list of supported features, visit [Introduction to Application Gateway](application-gateway-introduction.md)</span></span>

<span data-ttu-id="3946f-111">**D. Qual è la differenza tra gateway applicazione e Azure Load Balancer?**</span><span class="sxs-lookup"><span data-stu-id="3946f-111">**Q. What is the difference between Application Gateway and Azure Load Balancer?**</span></span>

<span data-ttu-id="3946f-112">Il gateway applicazione è un servizio di bilanciamento del carico di livello 7 e funziona quindi solo con il traffico Web (HTTP/HTTPS/WebSocket).</span><span class="sxs-lookup"><span data-stu-id="3946f-112">Application Gateway is a layer 7 load balancer, which means it works with web traffic only (HTTP/HTTPS/WebSocket).</span></span> <span data-ttu-id="3946f-113">Supporta funzionalità come terminazione SSL, affinità di sessione basata su cookie e round robin per il bilanciamento del carico del traffico.</span><span class="sxs-lookup"><span data-stu-id="3946f-113">It supports capabilities such as SSL termination, cookie-based session affinity, and round robin for load balancing traffic.</span></span> <span data-ttu-id="3946f-114">Load Balancer esegue il bilanciamento del carico del traffico al livello 4 (TCP/UDP).</span><span class="sxs-lookup"><span data-stu-id="3946f-114">Load Balancer, load balances traffic at layer 4 (TCP/UDP).</span></span>

<span data-ttu-id="3946f-115">**D. Quali protocolli supporta il gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="3946f-115">**Q. What protocols does Application Gateway support?**</span></span>

<span data-ttu-id="3946f-116">Il gateway applicazione supporta HTTP, HTTPS e WebSocket.</span><span class="sxs-lookup"><span data-stu-id="3946f-116">Application Gateway supports HTTP, HTTPS, and WebSocket.</span></span>

<span data-ttu-id="3946f-117">**D. Quali risorse sono supportate oggi nell'ambito del pool back-end?**</span><span class="sxs-lookup"><span data-stu-id="3946f-117">**Q. What resources are supported today as part of backend pool?**</span></span>

<span data-ttu-id="3946f-118">I pool back-end possono essere costituiti da schede di interfaccia di rete, set di scalabilità di macchine virtuali, indirizzi IP pubblici, indirizzi IP interni, nomi di dominio completi (FQDN) e back-end multi-tenant come App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="3946f-118">Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, fully qualified domain names (FQDN), and multi-tenant back-ends like Azure Web Apps.</span></span> <span data-ttu-id="3946f-119">I membri del pool back-end del gateway applicazione non sono associati a un set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="3946f-119">Application Gateway backend pool members are not tied to an availability set.</span></span> <span data-ttu-id="3946f-120">I membri del pool back-end possono trovarsi tra cluster, data center o all'esterno di Azure, purché abbiano connettività IP.</span><span class="sxs-lookup"><span data-stu-id="3946f-120">Members of backend pools can be across clusters, data centers, or outside of Azure as long as they have IP connectivity.</span></span>

<span data-ttu-id="3946f-121">**D. In quale aree è disponibile il servizio?**</span><span class="sxs-lookup"><span data-stu-id="3946f-121">**Q. What regions is the service available in?**</span></span>

<span data-ttu-id="3946f-122">Il gateway applicazione è disponibile in tutte le aree di Azure globale.</span><span class="sxs-lookup"><span data-stu-id="3946f-122">Application Gateway is available in all regions of global Azure.</span></span> <span data-ttu-id="3946f-123">È anche disponibile in [Azure Cina](https://www.azure.cn/) e [Azure per enti pubblici](https://azure.microsoft.com/en-us/overview/clouds/government/)</span><span class="sxs-lookup"><span data-stu-id="3946f-123">It is also available in [Azure China](https://www.azure.cn/) and [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span></span>

<span data-ttu-id="3946f-124">**D. Si tratta di una distribuzione dedicata per la sottoscrizione o è condivisa tra clienti?**</span><span class="sxs-lookup"><span data-stu-id="3946f-124">**Q. Is this a dedicated deployment for my subscription or is it shared across customers?**</span></span>

<span data-ttu-id="3946f-125">Il gateway applicazione è una distribuzione dedicata nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3946f-125">Application Gateway is a dedicated deployment in your virtual network.</span></span>

<span data-ttu-id="3946f-126">**D. È supportato il reindirizzamento HTTP->HTTPS?**</span><span class="sxs-lookup"><span data-stu-id="3946f-126">**Q. Is HTTP->HTTPS redirection supported?**</span></span>

<span data-ttu-id="3946f-127">Il reindirizzamento è supportato.</span><span class="sxs-lookup"><span data-stu-id="3946f-127">Redirection is supported.</span></span> <span data-ttu-id="3946f-128">Per altre informazioni, vedere la [panoramica del reindirizzamento del gateway applicazione](application-gateway-redirect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3946f-128">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) to learn more.</span></span>

<span data-ttu-id="3946f-129">**D. In quale ordine vengono elaborati i listener?**</span><span class="sxs-lookup"><span data-stu-id="3946f-129">**Q. In what order are listeners processed?**</span></span>

<span data-ttu-id="3946f-130">I listener vengono elaborati nell'ordine in cui sono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="3946f-130">Listeners are processed in the order they are shown.</span></span> <span data-ttu-id="3946f-131">Per tale motivo, se un listener di base corrisponde a una richiesta in ingresso, questa viene elaborata per prima.</span><span class="sxs-lookup"><span data-stu-id="3946f-131">For that reason if a basic listener matches an incoming request it processes it first.</span></span>  <span data-ttu-id="3946f-132">I listener multisito devono essere configurati prima di un listener di base per garantire che il traffico sia indirizzato al back-end corretto.</span><span class="sxs-lookup"><span data-stu-id="3946f-132">Multi-site listeners should be configured before a basic listener to ensure traffic is routed to the correct back-end.</span></span>

<span data-ttu-id="3946f-133">**D. Dove è possibile trovare IP e DNS del gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="3946f-133">**Q. Where do I find Application Gateway’s IP and DNS?**</span></span>

<span data-ttu-id="3946f-134">Quando si usa un indirizzo IP pubblico come endpoint, queste informazioni sono reperibili nella risorsa dell'indirizzo IP pubblico o nella pagina Panoramica del gateway applicazione nel portale.</span><span class="sxs-lookup"><span data-stu-id="3946f-134">When using a public IP address as an endpoint, this information can be found on the public IP address resource or on the Overview page for the Application Gateway in the portal.</span></span> <span data-ttu-id="3946f-135">Per gli indirizzi IP interni, queste informazioni si trovano nella pagina Panoramica.</span><span class="sxs-lookup"><span data-stu-id="3946f-135">For internal IP addresses, this can be found on the Overview page.</span></span>

<span data-ttu-id="3946f-136">**D. L'IP o il DNS cambia durante il ciclo di vita del gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="3946f-136">**Q. Does the IP or DNS change over the lifetime of the Application Gateway?**</span></span>

<span data-ttu-id="3946f-137">L'indirizzo VIP può cambiare se il gateway viene arrestato e avviato dal cliente.</span><span class="sxs-lookup"><span data-stu-id="3946f-137">The VIP can change if the gateway is stopped and started by the customer.</span></span> <span data-ttu-id="3946f-138">Il DNS associato al gateway applicazione non cambia durante il ciclo di vita del gateway.</span><span class="sxs-lookup"><span data-stu-id="3946f-138">The DNS associated with Application Gateway does not change over the lifecycle of the gateway.</span></span> <span data-ttu-id="3946f-139">Per questo motivo è consigliabile usare un alias CNAME che punti all'indirizzo DNS del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3946f-139">For this reason, it is recommended to use a CNAME alias and point it to the DNS address of the Application Gateway.</span></span>

<span data-ttu-id="3946f-140">**D. Il gateway applicazione supporta l'IP statico?**</span><span class="sxs-lookup"><span data-stu-id="3946f-140">**Q. Does Application Gateway support static IP?**</span></span>

<span data-ttu-id="3946f-141">No, il gateway applicazione non supporta indirizzi IP pubblici statici, ma supporta indirizzi IP interni statici.</span><span class="sxs-lookup"><span data-stu-id="3946f-141">No, Application Gateway does not support static public IP addresses, but it does support static internal IPs.</span></span>

<span data-ttu-id="3946f-142">**D. Il gateway applicazione supporta più indirizzi IP pubblici nel gateway?**</span><span class="sxs-lookup"><span data-stu-id="3946f-142">**Q. Does Application Gateway support multiple public IPs on the gateway?**</span></span>

<span data-ttu-id="3946f-143">Il gateway applicazione supporta un solo indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="3946f-143">Only one public IP address is supported on an Application Gateway.</span></span>

<span data-ttu-id="3946f-144">**D. Il gateway applicazione supporta le intestazioni x-forwarded-for?**</span><span class="sxs-lookup"><span data-stu-id="3946f-144">**Q. Does Application Gateway support x-forwarded-for headers?**</span></span>

<span data-ttu-id="3946f-145">Sì, il gateway applicazione inserisce le intestazioni x-forwarded-for, x-forwarded-proto e x-forwarded-port nella richiesta inoltrata al back-end.</span><span class="sxs-lookup"><span data-stu-id="3946f-145">Yes, Application Gateway inserts x-forwarded-for, x-forwarded-proto, and x-forwarded-port headers into the request forwarded to the backend.</span></span> <span data-ttu-id="3946f-146">Il formato dell'intestazione x-forwarded-for è un elenco di IP:Porta separato da virgole.</span><span class="sxs-lookup"><span data-stu-id="3946f-146">The format for x-forwarded-for header is a comma-separated list of IP:Port.</span></span> <span data-ttu-id="3946f-147">I valori validi per x-forwarded-proto sono http o https.</span><span class="sxs-lookup"><span data-stu-id="3946f-147">The valid values for x-forwarded-proto are http or https.</span></span> <span data-ttu-id="3946f-148">X-forwarded-port specifica la porta raggiunta dalla richiesta nel gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3946f-148">X-forwarded-port specifies the port at which the request reached at the Application Gateway.</span></span>

<span data-ttu-id="3946f-149">**D. Quanto tempo occorre per distribuire un gateway applicazione? Il gateway applicazione funziona durante l'aggiornamento?**</span><span class="sxs-lookup"><span data-stu-id="3946f-149">**Q. How long does it take to deploy an Application Gateway? Does my Application Gateway still work when being updated?**</span></span>

<span data-ttu-id="3946f-150">Nuove distribuzioni di gateway applicazione possono richiedere fino a 20 minuti per effettuare il provisioning.</span><span class="sxs-lookup"><span data-stu-id="3946f-150">New Application Gateway deployments can take up to 20 minutes to provision.</span></span> <span data-ttu-id="3946f-151">Le modifiche all'istanza di conteggio/dimensioni non causano problemi e il gateway rimane attivo durante questo periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="3946f-151">Changes to instance size/count are not disruptive, and the gateway remains active during this time.</span></span>

## <a name="configuration"></a><span data-ttu-id="3946f-152">Configurazione</span><span class="sxs-lookup"><span data-stu-id="3946f-152">Configuration</span></span>

<span data-ttu-id="3946f-153">**D. Il gateway applicazione viene sempre distribuito in una rete virtuale?**</span><span class="sxs-lookup"><span data-stu-id="3946f-153">**Q. Is Application Gateway always deployed in a virtual network?**</span></span>

<span data-ttu-id="3946f-154">Sì, il gateway applicazione viene sempre distribuito in una subnet di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3946f-154">Yes, Application Gateway is always deployed in a virtual network subnet.</span></span> <span data-ttu-id="3946f-155">Questa subnet può contenere solo gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3946f-155">This subnet can only contain Application Gateways.</span></span>

<span data-ttu-id="3946f-156">**D. Il gateway applicazione può comunicare con istanze all'esterno della rete virtuale?**</span><span class="sxs-lookup"><span data-stu-id="3946f-156">**Q. Can Application Gateway talk to instances outside its virtual network?**</span></span>

<span data-ttu-id="3946f-157">Il gateway applicazione può comunicare con le istanze all'esterno della rete virtuale nella quale si trova se è disponibile la connettività IP.</span><span class="sxs-lookup"><span data-stu-id="3946f-157">Application Gateway can talk to instances outside of the virtual network that it is in as long as there is IP connectivity.</span></span> <span data-ttu-id="3946f-158">Se si prevede di usare indirizzi IP interni come membri del pool back-end, è necessario il [peering reti virtuali](../virtual-network/virtual-network-peering-overview.md) o il [gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="3946f-158">If you plan to use internal IPs as backend pool members, then it requires [VNET Peering](../virtual-network/virtual-network-peering-overview.md) or [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>

<span data-ttu-id="3946f-159">**D. È possibile distribuire altri elementi nella subnet del gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="3946f-159">**Q. Can I deploy anything else in the Application Gateway subnet?**</span></span>

<span data-ttu-id="3946f-160">No, ma è possibile distribuire altri gateway applicazione nella subnet.</span><span class="sxs-lookup"><span data-stu-id="3946f-160">No, but you can deploy other application gateways in the subnet.</span></span>

<span data-ttu-id="3946f-161">**D. I gruppi di sicurezza di rete sono supportati nella subnet del gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="3946f-161">**Q. Are Network Security Groups supported on the Application Gateway subnet?**</span></span>

<span data-ttu-id="3946f-162">I gruppi di sicurezza di rete sono supportati nella subnet del gateway applicazione con le restrizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3946f-162">Network Security Groups are supported on the Application Gateway subnet with the following restrictions:</span></span>

* <span data-ttu-id="3946f-163">Le eccezioni devono essere inserite per il traffico in entrata sulle porte 65503-65534 affinché l'integrità del back-end funzioni correttamente.</span><span class="sxs-lookup"><span data-stu-id="3946f-163">Exceptions must be put in for incoming traffic on ports 65503-65534 for backend health to work correctly.</span></span>

* <span data-ttu-id="3946f-164">La connettività Internet in uscita non può essere bloccata.</span><span class="sxs-lookup"><span data-stu-id="3946f-164">Outbound internet connectivity can not be blocked.</span></span>

* <span data-ttu-id="3946f-165">È necessario consentire il traffico dal tag AzureLoadBalancer.</span><span class="sxs-lookup"><span data-stu-id="3946f-165">Traffic from the AzureLoadBalancer tag must be allowed.</span></span>

<span data-ttu-id="3946f-166">**D. Quali sono i limiti del gateway applicazione? È possibile aumentare questi limiti?**</span><span class="sxs-lookup"><span data-stu-id="3946f-166">**Q. What are the limits on Application Gateway? Can I increase these limits?**</span></span>

<span data-ttu-id="3946f-167">Vedere [Limiti del gateway applicazione](../azure-subscription-service-limits.md#application-gateway-limits) per informazioni sui limiti.</span><span class="sxs-lookup"><span data-stu-id="3946f-167">Visit [Application Gateway Limits](../azure-subscription-service-limits.md#application-gateway-limits) to view the limits.</span></span>

<span data-ttu-id="3946f-168">**D. È possibile usare il gateway applicazione per il traffico interno ed esterno contemporaneamente?**</span><span class="sxs-lookup"><span data-stu-id="3946f-168">**Q. Can I use Application Gateway for both external and internal traffic simultaneously?**</span></span>

<span data-ttu-id="3946f-169">Sì, il gateway applicazione supporta un indirizzo IP interno e un indirizzo IP esterno.</span><span class="sxs-lookup"><span data-stu-id="3946f-169">Yes, Application Gateway supports having one internal IP and one external IP per Application Gateway.</span></span>

<span data-ttu-id="3946f-170">**D. Il peering reti virtuali è supportato?**</span><span class="sxs-lookup"><span data-stu-id="3946f-170">**Q. Is VNet peering supported?**</span></span>

<span data-ttu-id="3946f-171">Sì, il peering reti virtuali è supportato ed è utile per il bilanciamento del carico del traffico in altre reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="3946f-171">Yes, VNet peering is supported and is beneficial for load balancing traffic in other virtual networks.</span></span>

<span data-ttu-id="3946f-172">**D. È possibile comunicare con server locali se connessi da tunnel VPN o ExpressRoute?**</span><span class="sxs-lookup"><span data-stu-id="3946f-172">**Q. Can I talk to on-premises servers when they are connected by ExpressRoute or VPN tunnels?**</span></span>

<span data-ttu-id="3946f-173">Sì, se il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="3946f-173">Yes, as long as traffic is allowed.</span></span>

<span data-ttu-id="3946f-174">**D. È possibile avere un pool back-end che serve molte applicazioni su porte diverse?**</span><span class="sxs-lookup"><span data-stu-id="3946f-174">**Q. Can I have one backend pool serving many applications on different ports?**</span></span>

<span data-ttu-id="3946f-175">L'architettura di microservizi è supportata.</span><span class="sxs-lookup"><span data-stu-id="3946f-175">Micro service architecture is supported.</span></span> <span data-ttu-id="3946f-176">È necessario configurare più impostazioni HTTP per il probe su porte diverse.</span><span class="sxs-lookup"><span data-stu-id="3946f-176">You would need multiple http settings configured to probe on different ports.</span></span>

<span data-ttu-id="3946f-177">**D. I probe personalizzati supportano caratteri jolly o regex nei dati di risposta?**</span><span class="sxs-lookup"><span data-stu-id="3946f-177">**Q. Do custom probes support wildcards/regex on response data?**</span></span>

<span data-ttu-id="3946f-178">I probe personalizzati non supportano caratteri jolly o regex nei dati di risposta.</span><span class="sxs-lookup"><span data-stu-id="3946f-178">Custom probes do not support wildcard or regex on response data.</span></span> 

<span data-ttu-id="3946f-179">**D. Come vengono elaborate le regole?**</span><span class="sxs-lookup"><span data-stu-id="3946f-179">**Q. How are rules processed?**</span></span>

<span data-ttu-id="3946f-180">Le regole vengono elaborate nell'ordine in cui sono configurate.</span><span class="sxs-lookup"><span data-stu-id="3946f-180">Rules are processed in the order they are configured.</span></span> <span data-ttu-id="3946f-181">È consigliabile che le regole multisito siano configurate prima delle regole di base per ridurre le probabilità che il traffico sia indirizzato a un back-end inappropriato, in quanto la regola di base selezionarebbe il traffico in base alla porta prima che venga valutata la regola multisito.</span><span class="sxs-lookup"><span data-stu-id="3946f-181">It is recommended that multi-site rules are configured before basic rules to reduce the chance that traffic is routed to the inappropriate backend as the basic rule would match traffic based on port prior to the multi-site rule being evaluated.</span></span>

<span data-ttu-id="3946f-182">**D. Come vengono elaborate le regole?**</span><span class="sxs-lookup"><span data-stu-id="3946f-182">**Q. How are rules processed?**</span></span>

<span data-ttu-id="3946f-183">Le regole vengono elaborate nell'ordine in cui sono create.</span><span class="sxs-lookup"><span data-stu-id="3946f-183">Rules are processed in the order they are created.</span></span> <span data-ttu-id="3946f-184">È consigliabile configurare le regole multisito prima delle regole di base.</span><span class="sxs-lookup"><span data-stu-id="3946f-184">It is recommended that multi-site rules are configured before basic rules.</span></span> <span data-ttu-id="3946f-185">Configurando prima i listener multisito, la configurazione riduce le probabilità che il traffico venga instradato al back-end non appropriato.</span><span class="sxs-lookup"><span data-stu-id="3946f-185">By configuring multi-site listeners first, this configuration reduces the chance that traffic is routed to the inappropriate backend.</span></span> <span data-ttu-id="3946f-186">Questo problema di routing può verificarsi se la regola di base corrisponde al traffico in base alla porta prima che venga valutata la regola multisito.</span><span class="sxs-lookup"><span data-stu-id="3946f-186">This routing issue can occur as the basic rule would match traffic based on port prior to the multi-site rule being evaluated.</span></span>

<span data-ttu-id="3946f-187">**D. Cosa indica il campo Host per i probe personalizzati?**</span><span class="sxs-lookup"><span data-stu-id="3946f-187">**Q. What does the Host field for custom probes signify?**</span></span>

<span data-ttu-id="3946f-188">Il campo Host specifica il nome a cui inviare il probe.</span><span class="sxs-lookup"><span data-stu-id="3946f-188">Host field specifies the name to send the probe to.</span></span> <span data-ttu-id="3946f-189">Applicabile solo quando vengono configurati più siti nel gateway applicazione. In caso contrario, usare "127.0.0.1".</span><span class="sxs-lookup"><span data-stu-id="3946f-189">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="3946f-190">Questo valore è diverso dal nome host della VM ed è nel formato \<protocollo\>://\<host\>:\<porta\>\<percorso\>.</span><span class="sxs-lookup"><span data-stu-id="3946f-190">This value is different from VM host name and is in format \<protocol\>://\<host\>:\<port\>\<path\>.</span></span>

<span data-ttu-id="3946f-191">**D. È possibile consentire l'accesso al gateway applicazione ad alcuni IP di origine?**</span><span class="sxs-lookup"><span data-stu-id="3946f-191">**Q. Can I whitelist Application Gateway access to a few source IPs?**</span></span>

<span data-ttu-id="3946f-192">Questo scenario è possibile usando gruppi di sicurezza di rete nella subnet del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3946f-192">This scenario can be done using NSGs on Application Gateway subnet.</span></span> <span data-ttu-id="3946f-193">Nella subnet nell'ordine di priorità elencato, è necessario inserire le restrizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3946f-193">The following restrictions should be put on the subnet in the listed order of priority:</span></span>

* <span data-ttu-id="3946f-194">Consentire il traffico in ingresso dall'intervallo di IP/IP di origine.</span><span class="sxs-lookup"><span data-stu-id="3946f-194">Allow incoming traffic from source IP/IP range.</span></span>

* <span data-ttu-id="3946f-195">Consentire le richieste in ingresso da tutte le origini alle porte 65503-65534 per la [comunicazione integrità back-end](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="3946f-195">Allow incoming requests from all sources to ports 65503-65534 for [backend health communication](application-gateway-diagnostics.md).</span></span>

* <span data-ttu-id="3946f-196">Consentire probe di bilanciamento del carico di Azure in ingresso (tag AzureLoadBalancer) e il traffico di rete virtuale in ingresso (tag VirtualNetwork) nei [gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="3946f-196">Allow incoming Azure Load Balancer probes (AzureLoadBalancer tag) and inbound virtual network traffic (VirtualNetwork tag) on the [NSG](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="3946f-197">Bloccare tutto il traffico in ingresso con una regola Nega tutto.</span><span class="sxs-lookup"><span data-stu-id="3946f-197">Block all other incoming traffic with a Deny all rule.</span></span>

* <span data-ttu-id="3946f-198">Consentire il traffico in uscita a Internet per tutte le destinazioni.</span><span class="sxs-lookup"><span data-stu-id="3946f-198">Allow outbound traffic to the internet for all destinations.</span></span>

## <a name="performance"></a><span data-ttu-id="3946f-199">Prestazioni</span><span class="sxs-lookup"><span data-stu-id="3946f-199">Performance</span></span>

<span data-ttu-id="3946f-200">**D. In che modo il gateway applicazione supporta la disponibilità elevata e la scalabilità?**</span><span class="sxs-lookup"><span data-stu-id="3946f-200">**Q. How does Application Gateway support high availability and scalability?**</span></span>

<span data-ttu-id="3946f-201">Il gateway applicazione supporta scenari di disponibilità elevata se sono presenti due o più istanze distribuite.</span><span class="sxs-lookup"><span data-stu-id="3946f-201">Application Gateway supports high availability scenarios when you have two or more instances deployed.</span></span> <span data-ttu-id="3946f-202">Azure distribuisce queste istanze nei domini di errore e di aggiornamento per impedire l'arresto simultaneo di tutte le istanze.</span><span class="sxs-lookup"><span data-stu-id="3946f-202">Azure distributes these instances across update and fault domains to ensure that all instances do not fail at the same time.</span></span> <span data-ttu-id="3946f-203">Il gateway applicazione supporta la scalabilità tramite l'aggiunta di più istanze dello stesso gateway per ripartire il carico.</span><span class="sxs-lookup"><span data-stu-id="3946f-203">Application Gateway supports scalability by adding multiple instances of the same gateway to share the load.</span></span>

<span data-ttu-id="3946f-204">**D. Come si ottiene uno scenario di ripristino di emergenza tra data center con un gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="3946f-204">**Q. How do I achieve DR scenario across data centers with Application Gateway?**</span></span>

<span data-ttu-id="3946f-205">I clienti possono usare Gestione traffico per distribuire il traffico tra più gateway applicazione in data center diversi.</span><span class="sxs-lookup"><span data-stu-id="3946f-205">Customers can use Traffic Manager to distribute traffic across multiple Application Gateways in different datacenters.</span></span>

<span data-ttu-id="3946f-206">**D. La scalabilità automatica è supportata?**</span><span class="sxs-lookup"><span data-stu-id="3946f-206">**Q. Is auto scaling supported?**</span></span>

<span data-ttu-id="3946f-207">No, ma il gateway applicazione offre una metrica della velocità effettiva che può essere usata per ricevere un avviso quando viene raggiunta una soglia.</span><span class="sxs-lookup"><span data-stu-id="3946f-207">No, but Application Gateway has a throughput metric that can be used to alert you when a threshold is reached.</span></span> <span data-ttu-id="3946f-208">L'operazione manuale di aggiunta di istanze o ridimensionamento non provoca il riavvio del gateway e non ha alcun impatto sul traffico esistente.</span><span class="sxs-lookup"><span data-stu-id="3946f-208">Manually adding instances or changing size does not restart the gateway and does not impact existing traffic.</span></span>

<span data-ttu-id="3946f-209">**D. Il ridimensionamento manuale causa tempi di inattività?**</span><span class="sxs-lookup"><span data-stu-id="3946f-209">**Q. Does manual scale up/down cause downtime?**</span></span>

<span data-ttu-id="3946f-210">Non si verificano tempi di inattività, le istanze vengono distribuite tra domini di aggiornamento e domini di errore.</span><span class="sxs-lookup"><span data-stu-id="3946f-210">There is no downtime, instances are distributed across upgrade domains and fault domains.</span></span>

<span data-ttu-id="3946f-211">**D. È possibile modificare le dimensioni di un'istanza da medie a grandi senza interruzioni?**</span><span class="sxs-lookup"><span data-stu-id="3946f-211">**Q. Can I change instance size from medium to large without disruption?**</span></span>

<span data-ttu-id="3946f-212">Sì, Azure distribuisce le istanze nei domini di errore e di aggiornamento per impedire l'arresto simultaneo di tutte le istanze.</span><span class="sxs-lookup"><span data-stu-id="3946f-212">Yes, Azure distributes instances across update and fault domains to ensure that all instances do not fail at the same time.</span></span> <span data-ttu-id="3946f-213">Il gateway applicazione supporta la scalabilità con l'aggiunta di più istanze dello stesso gateway per la condivisione del carico.</span><span class="sxs-lookup"><span data-stu-id="3946f-213">Application Gateway supports scaling by adding multiple instances of the same gateway to share the load.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="3946f-214">Configurazione SSL</span><span class="sxs-lookup"><span data-stu-id="3946f-214">SSL Configuration</span></span>

<span data-ttu-id="3946f-215">**D. Quali certificati sono supportati dal gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="3946f-215">**Q. What certificates are supported on Application Gateway?**</span></span>

<span data-ttu-id="3946f-216">Sono supportati certificati autofirmati, certificati della CA e certificati con caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="3946f-216">Self signed certs, CA certs, and wild-card certs are supported.</span></span> <span data-ttu-id="3946f-217">I certificati di convalida estesa non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="3946f-217">EV certs are not supported.</span></span>

<span data-ttu-id="3946f-218">**D. Quali sono i pacchetti di crittografia attualmente supportati dal gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="3946f-218">**Q. What are the current cipher suites supported by Application Gateway?**</span></span>

<span data-ttu-id="3946f-219">Di seguito sono elencati i pacchetti di crittografia attualmente supportati dal gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3946f-219">The following are the current cipher suites supported by application gateway.</span></span> <span data-ttu-id="3946f-220">Per informazioni su come configurare le opzioni SSL, vedere l'articolo [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) (Configurare versioni di criteri SSL e pacchetti di crittografia nel gateway applicazione).</span><span class="sxs-lookup"><span data-stu-id="3946f-220">Visit: [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) to learn how to customize SSL options.</span></span>

- <span data-ttu-id="3946f-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="3946f-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="3946f-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3946f-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="3946f-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3946f-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="3946f-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3946f-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="3946f-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="3946f-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="3946f-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="3946f-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="3946f-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3946f-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="3946f-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3946f-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="3946f-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="3946f-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="3946f-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="3946f-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="3946f-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3946f-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="3946f-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3946f-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="3946f-233">TLS_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3946f-233">TLS_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="3946f-234">TLS_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3946f-234">TLS_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="3946f-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="3946f-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="3946f-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="3946f-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="3946f-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="3946f-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="3946f-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3946f-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="3946f-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3946f-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="3946f-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3946f-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="3946f-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3946f-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="3946f-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3946f-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="3946f-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3946f-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="3946f-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3946f-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="3946f-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3946f-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span></span>
- <span data-ttu-id="3946f-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="3946f-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span></span>

<span data-ttu-id="3946f-247">**D. Il gateway applicazione supporta anche la ripetizione della crittografia del traffico nel back-end?**</span><span class="sxs-lookup"><span data-stu-id="3946f-247">**Q. Does Application Gateway also support re-encryption of traffic to the backend?**</span></span>

<span data-ttu-id="3946f-248">Sì, il gateway applicazione supporta l'offload SSL e l'SSL end-to-end, che consente di crittografare nuovamente il traffico nel back-end.</span><span class="sxs-lookup"><span data-stu-id="3946f-248">Yes, Application Gateway supports SSL offload, and end to end SSL, which re-encrypts the traffic to the backend.</span></span>

<span data-ttu-id="3946f-249">**D. È possibile configurare i criteri SSL per gestire le versioni del protocollo SSL?**</span><span class="sxs-lookup"><span data-stu-id="3946f-249">**Q. Can I configure SSL policy to control SSL Protocol versions?**</span></span>

<span data-ttu-id="3946f-250">Sì, è possibile configurare il gateway applicazione per rifiutare TLS1.0, TLS1.1 e TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="3946f-250">Yes, you can configure Application Gateway to deny TLS1.0, TLS1.1, and TLS1.2.</span></span> <span data-ttu-id="3946f-251">SSL 2.0 e 3.0 sono già disabilitati per impostazione predefinita e non sono configurabili.</span><span class="sxs-lookup"><span data-stu-id="3946f-251">SSL 2.0 and 3.0 are already disabled by default and are not configurable.</span></span>

<span data-ttu-id="3946f-252">**D. È possibile configurare l'ordine dei pacchetti di crittografia e dei criteri?**</span><span class="sxs-lookup"><span data-stu-id="3946f-252">**Q. Can I configure cipher suites and policy order?**</span></span>

<span data-ttu-id="3946f-253">Sì, la [configurazione dei pacchetti di crittografia](application-gateway-ssl-policy-overview.md) è supportata.</span><span class="sxs-lookup"><span data-stu-id="3946f-253">Yes, [configuration of cipher suites](application-gateway-ssl-policy-overview.md) is supported.</span></span> <span data-ttu-id="3946f-254">Quando si definiscono criteri personalizzati, deve essere abilitato almeno uno dei pacchetti di crittografia seguenti.</span><span class="sxs-lookup"><span data-stu-id="3946f-254">When defining a custom policy, at least one of the following cipher suites must be enabled.</span></span> <span data-ttu-id="3946f-255">Il gateway applicazione usa SHA256 per la gestione del back-end.</span><span class="sxs-lookup"><span data-stu-id="3946f-255">Application gateway uses SHA256 to for backend management.</span></span>

* <span data-ttu-id="3946f-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="3946f-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
* <span data-ttu-id="3946f-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3946f-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
* <span data-ttu-id="3946f-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="3946f-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="3946f-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="3946f-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="3946f-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3946f-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
* <span data-ttu-id="3946f-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3946f-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

<span data-ttu-id="3946f-262">**D. Quanti certificati SSL sono supportati?**</span><span class="sxs-lookup"><span data-stu-id="3946f-262">**Q. How many SSL certificates are supported?**</span></span>

<span data-ttu-id="3946f-263">Sono supportati fino a 20 certificati SSL.</span><span class="sxs-lookup"><span data-stu-id="3946f-263">Up to 20 SSL certificates are supported.</span></span>

<span data-ttu-id="3946f-264">**D. Quanti certificati di autenticazione sono supportati per la ripetizione della crittografia nel back-end?**</span><span class="sxs-lookup"><span data-stu-id="3946f-264">**Q. How many authentication certificates for backend re-encryption are supported?**</span></span>

<span data-ttu-id="3946f-265">Sono supportati fino a 10 certificati di autenticazione con un valore predefinito di 5.</span><span class="sxs-lookup"><span data-stu-id="3946f-265">Up to 10 authentication certificates are supported with a default of 5.</span></span>

<span data-ttu-id="3946f-266">**D. Il gateway applicazione si integra con Azure Key Vault in modo nativo?**</span><span class="sxs-lookup"><span data-stu-id="3946f-266">**Q. Does Application Gateway integrate with Azure Key Vault natively?**</span></span>

<span data-ttu-id="3946f-267">No, non è integrato con Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3946f-267">No, it is not integrated with Azure Key Vault.</span></span>

## <a name="web-application-firewall-waf-configuration"></a><span data-ttu-id="3946f-268">Configurazione del Web application firewall (WAF)</span><span class="sxs-lookup"><span data-stu-id="3946f-268">Web Application Firewall (WAF) Configuration</span></span>

<span data-ttu-id="3946f-269">**D. Lo SKU del WAF offre tutte le funzionalità disponibili con lo SKU Standard?**</span><span class="sxs-lookup"><span data-stu-id="3946f-269">**Q. Does the WAF SKU offer all the features available with the Standard SKU?**</span></span>

<span data-ttu-id="3946f-270">Sì, il WAF offre tutte le funzionalità disponibili nello SKU Standard.</span><span class="sxs-lookup"><span data-stu-id="3946f-270">Yes, WAF supports all the features in the Standard SKU.</span></span>

<span data-ttu-id="3946f-271">**D. Qual è la versione di CRS supportata dal gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="3946f-271">**Q. What is the CRS version Application Gateway supports?**</span></span>

<span data-ttu-id="3946f-272">Il gateway applicazione supporta CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) e CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span><span class="sxs-lookup"><span data-stu-id="3946f-272">Application Gateway supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span></span>

<span data-ttu-id="3946f-273">**D. Come si monitora il Web application firewall?**</span><span class="sxs-lookup"><span data-stu-id="3946f-273">**Q. How do I monitor WAF?**</span></span>

<span data-ttu-id="3946f-274">Il Web application firewall viene monitorato tramite la registrazione diagnostica. Per altre informazioni sulla registrazione diagnostica, vedere [Integrità back-end, registrazione diagnostica e metriche per il gateway applicazione](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="3946f-274">WAF is monitored through diagnostic logging, more information on diagnostic logging can be found at [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="3946f-275">**D. La modalità di rilevamento blocca il traffico?**</span><span class="sxs-lookup"><span data-stu-id="3946f-275">**Q. Does detection mode block traffic?**</span></span>

<span data-ttu-id="3946f-276">No, la modalità di rilevamento registra solo il traffico che ha attivato una regola del Web application firewall.</span><span class="sxs-lookup"><span data-stu-id="3946f-276">No, detection mode only logs traffic, which triggered a WAF rule.</span></span>

<span data-ttu-id="3946f-277">**D. Come si personalizzano le regole del Web application firewall?**</span><span class="sxs-lookup"><span data-stu-id="3946f-277">**Q. How do I customize WAF rules?**</span></span>

<span data-ttu-id="3946f-278">Sì, le regole WAF sono personalizzabili. Per altre informazioni sulla relativa personalizzazione, vedere [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md) (Personalizzare le regole e i gruppi di regole di WAF)</span><span class="sxs-lookup"><span data-stu-id="3946f-278">Yes, WAF rules are customizable, for more information on how to customize them visit [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md)</span></span>

<span data-ttu-id="3946f-279">**D. Quali regole sono attualmente disponibili?**</span><span class="sxs-lookup"><span data-stu-id="3946f-279">**Q. What rules are currently available?**</span></span>

<span data-ttu-id="3946f-280">Il Web application firewall supporta attualmente CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) e [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), che offre la protezione di base per la maggior parte delle prime 10 vulnerabilità identificate dall'Open Web Application Security Project (OWASP) disponibili in [Prime 10 vulnerabilità OWASP](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span><span class="sxs-lookup"><span data-stu-id="3946f-280">WAF currently supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), which provide baseline security against most of the top 10 vulnerabilities identified by the Open Web Application Security Project (OWASP) found here [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span></span>

* <span data-ttu-id="3946f-281">Protezione dagli attacchi SQL injection</span><span class="sxs-lookup"><span data-stu-id="3946f-281">SQL injection protection</span></span>

* <span data-ttu-id="3946f-282">Protezione dagli attacchi di scripting intersito</span><span class="sxs-lookup"><span data-stu-id="3946f-282">Cross site scripting protection</span></span>

* <span data-ttu-id="3946f-283">Protezione dai comuni attacchi Web, ad esempio attacchi di iniezione di comandi, richieste HTTP non valide, attacchi HTTP Response Splitting e Remote File Inclusion</span><span class="sxs-lookup"><span data-stu-id="3946f-283">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

* <span data-ttu-id="3946f-284">Protezione dalle violazioni del protocollo HTTP</span><span class="sxs-lookup"><span data-stu-id="3946f-284">Protection against HTTP protocol violations</span></span>

* <span data-ttu-id="3946f-285">Protezione contro eventuali anomalie del protocollo HTTP, ad esempio user agent host mancante e accept header</span><span class="sxs-lookup"><span data-stu-id="3946f-285">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

* <span data-ttu-id="3946f-286">Prevenzione contro robot, crawler e scanner</span><span class="sxs-lookup"><span data-stu-id="3946f-286">Prevention against bots, crawlers, and scanners</span></span>

* <span data-ttu-id="3946f-287">Rilevamento di errori di configurazione dell'applicazione comuni (ad esempio, Apache, IIS e così via)</span><span class="sxs-lookup"><span data-stu-id="3946f-287">Detection of common application misconfigurations (that is, Apache, IIS, etc.)</span></span>

<span data-ttu-id="3946f-288">**D. Il WAF supporta anche la prevenzione DDoS?**</span><span class="sxs-lookup"><span data-stu-id="3946f-288">**Q. Does WAF also support DDoS prevention?**</span></span>

<span data-ttu-id="3946f-289">No, non fornisce la prevenzione DDoS.</span><span class="sxs-lookup"><span data-stu-id="3946f-289">No, WAF does not provide DDoS prevention.</span></span>

## <a name="diagnostics-and-logging"></a><span data-ttu-id="3946f-290">Diagnostica e registrazione</span><span class="sxs-lookup"><span data-stu-id="3946f-290">Diagnostics and Logging</span></span>

<span data-ttu-id="3946f-291">**D. Quali tipi di log sono disponibili con il gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="3946f-291">**Q. What types of logs are available with Application Gateway?**</span></span>

<span data-ttu-id="3946f-292">Sono disponibili tre log con il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3946f-292">There are three logs available for Application Gateway.</span></span> <span data-ttu-id="3946f-293">Per altre informazioni su questi log e altre funzionalità di diagnostica, vedere [Integrità back-end, log di diagnostica e metriche per il gateway applicazione](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="3946f-293">For more information on these logs and other diagnostic capabilities, visit [Backend health, diagnostics logs, and metrics for Application Gateway](application-gateway-diagnostics.md).</span></span>

- <span data-ttu-id="3946f-294">**ApplicationGatewayAccessLog**: il log di accesso contiene ogni richiesta inviata al front-end del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3946f-294">**ApplicationGatewayAccessLog** - The access log contains each request submitted to the Application Gateway frontend.</span></span> <span data-ttu-id="3946f-295">I dati includono indirizzo IP del chiamante, URL richiesto, latenza della risposta, codice restituito, byte in ingresso e in uscita. Il log di accesso viene raccolto ogni 300 secondi.</span><span class="sxs-lookup"><span data-stu-id="3946f-295">The data includes the caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span></span> <span data-ttu-id="3946f-296">Il log contiene un record per ogni istanza del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3946f-296">This log contains one record per instance of Application Gateway.</span></span>
- <span data-ttu-id="3946f-297">**ApplicationGatewayPerformanceLog**: il log delle prestazioni acquisisce le informazioni sulle prestazioni di ogni singola istanza, come il totale delle richieste servite, la velocità effettiva in byte, il numero delle richieste non riuscite e il numero delle istanze back-end integre e non integre.</span><span class="sxs-lookup"><span data-stu-id="3946f-297">**ApplicationGatewayPerformanceLog** - The performance log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span></span>
- <span data-ttu-id="3946f-298">**ApplicationGatewayFirewallLog**: il log del firewall contiene le richieste registrate tramite la modalità di rilevamento o prevenzione di un gateway applicazione configurato con il Web application firewall.</span><span class="sxs-lookup"><span data-stu-id="3946f-298">**ApplicationGatewayFirewallLog** - The firewall log contains requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span></span>

<span data-ttu-id="3946f-299">**D. Come è possibile sapere se i membri del pool back-end sono integri?**</span><span class="sxs-lookup"><span data-stu-id="3946f-299">**Q. How do I know if my backend pool members are healthy?**</span></span>

<span data-ttu-id="3946f-300">È possibile usare il cmdlet `Get-AzureRmApplicationGatewayBackendHealth` di PowerShell o verificare l'integrità tramite il portale. Vedere la [diagnostica del gateway applicazione](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="3946f-300">You can use the PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth` or verify health through the portal by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="3946f-301">**D. Che cos'è il criterio di conservazione per i log di diagnostica?**</span><span class="sxs-lookup"><span data-stu-id="3946f-301">**Q. What is the retention policy on the diagnostics logs?**</span></span>

<span data-ttu-id="3946f-302">I log di diagnostica vengono inseriti nell'account di archiviazione dei clienti, i quali possono impostare i criteri di conservazione in base alle preferenze.</span><span class="sxs-lookup"><span data-stu-id="3946f-302">Diagnostic logs flow to the customers storage account and customers can set the retention policy based on their preference.</span></span> <span data-ttu-id="3946f-303">I log di diagnostica possono anche essere inviati a un hub eventi o a Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3946f-303">Diagnostic logs can also be sent to an Event Hub or Log Analytics.</span></span> <span data-ttu-id="3946f-304">Vedere [Diagnostica del gateway applicazione](application-gateway-diagnostics.md) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="3946f-304">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) for more details.</span></span>

<span data-ttu-id="3946f-305">**D. Come si ottengono i log di controllo per il gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="3946f-305">**Q. How do I get audit logs for Application Gateway?**</span></span>

<span data-ttu-id="3946f-306">Sono disponibili log di controllo per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="3946f-306">Audit logs are available for Application Gateway.</span></span> <span data-ttu-id="3946f-307">Nel portale fare clic su **Log attività** nel pannello del menu di un gateway applicazione per accedere al log di controllo.</span><span class="sxs-lookup"><span data-stu-id="3946f-307">In the portal, click **Activity Log** in the menu blade of an Application Gateway to access the audit log.</span></span> 

<span data-ttu-id="3946f-308">**D. È possibile impostare avvisi con il gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="3946f-308">**Q. Can I set alerts with Application Gateway?**</span></span>

<span data-ttu-id="3946f-309">Sì, il gateway applicazione supporta gli avvisi, che vengono configurati in base alle metriche.</span><span class="sxs-lookup"><span data-stu-id="3946f-309">Yes, Application Gateway does support alerts, alerts are configured off metrics.</span></span>  <span data-ttu-id="3946f-310">Il gateway applicazione ha attualmente una metrica di "velocità effettiva" che può essere configurata per l'invio di avvisi.</span><span class="sxs-lookup"><span data-stu-id="3946f-310">Application Gateway currently has a metric of "throughput", which can be configured to alert.</span></span> <span data-ttu-id="3946f-311">Per altre informazioni sugli avvisi, vedere [Ricevere notifiche di avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="3946f-311">To learn more about alerts, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="3946f-312">**D. L'integrità back-end restituisce uno stato sconosciuto. Quale potrebbe essere la causa?**</span><span class="sxs-lookup"><span data-stu-id="3946f-312">**Q. Backend health returns unknown status, what could be causing this status?**</span></span>

<span data-ttu-id="3946f-313">Nella maggior parte dei casi, l'accesso al back-end è bloccato da un gruppo di sicurezza di rete o un DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="3946f-313">The most common reason is access to the backend is being blocked by an NSG or custom DNS.</span></span> <span data-ttu-id="3946f-314">Vedere [Integrità back-end, registrazione diagnostica e metriche per il gateway applicazione](application-gateway-diagnostics.md) per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="3946f-314">Visit [Backend health, diagnostics logging, and metrics for Application Gateway](application-gateway-diagnostics.md) to learn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3946f-315">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3946f-315">Next Steps</span></span>

<span data-ttu-id="3946f-316">Per altre informazioni sul gateway applicazione, vedere la [panoramica del gateway applicazione](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3946f-316">To learn more about Application Gateway visit [Introduction to Application Gateway](application-gateway-introduction.md).</span></span>
