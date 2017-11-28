---
title: domande frequenti per Azure applicazione Gateway aaaFrequently | Documenti Microsoft
description: Questa pagina vengono fornite le risposte toofrequently domande frequenti sul Gateway applicazione Azure
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
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a><span data-ttu-id="10aa3-103">Domande frequenti sul gateway applicazione</span><span class="sxs-lookup"><span data-stu-id="10aa3-103">Frequently asked questions for Application Gateway</span></span>

## <a name="general"></a><span data-ttu-id="10aa3-104">Generale</span><span class="sxs-lookup"><span data-stu-id="10aa3-104">General</span></span>

<span data-ttu-id="10aa3-105">**D. Che cos'è il gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-105">**Q. What is Application Gateway?**</span></span>

<span data-ttu-id="10aa3-106">Il gateway applicazione di Azure è un servizio di controller per la distribuzione di applicazioni (ADC) con numerose funzionalità di bilanciamento del carico di livello 7.</span><span class="sxs-lookup"><span data-stu-id="10aa3-106">Azure Application Gateway is an Application Delivery Controller (ADC) as a service, offering various layer 7 load balancing capabilities for your applications.</span></span> <span data-ttu-id="10aa3-107">Offre un servizio altamente disponibile e scalabile completamente gestito da Azure.</span><span class="sxs-lookup"><span data-stu-id="10aa3-107">It offers highly available and scalable service, which is fully managed by Azure.</span></span>

<span data-ttu-id="10aa3-108">**D. Quali funzionalità supporta il gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-108">**Q. What features does Application Gateway support?**</span></span>

<span data-ttu-id="10aa3-109">Gateway applicazione supporta SSL tooend end e di offload SSL, Web Application Firewall, affinità di sessione basato su cookie, url basato sul percorso routing, hosting di più siti e altri utenti.</span><span class="sxs-lookup"><span data-stu-id="10aa3-109">Application Gateway supports SSL offloading and end tooend SSL, Web Application Firewall, cookie-based session affinity, url path-based routing, multi site hosting, and others.</span></span> <span data-ttu-id="10aa3-110">Per un elenco completo delle funzionalità supportate, visitare [tooApplication introduzione Gateway](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="10aa3-110">For a full list of supported features, visit [Introduction tooApplication Gateway](application-gateway-introduction.md)</span></span>

<span data-ttu-id="10aa3-111">**D. Qual è la differenza hello tra il Gateway di applicazione e servizio di bilanciamento del carico di Azure?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-111">**Q. What is hello difference between Application Gateway and Azure Load Balancer?**</span></span>

<span data-ttu-id="10aa3-112">Il gateway applicazione è un servizio di bilanciamento del carico di livello 7 e funziona quindi solo con il traffico Web (HTTP/HTTPS/WebSocket).</span><span class="sxs-lookup"><span data-stu-id="10aa3-112">Application Gateway is a layer 7 load balancer, which means it works with web traffic only (HTTP/HTTPS/WebSocket).</span></span> <span data-ttu-id="10aa3-113">Supporta funzionalità come terminazione SSL, affinità di sessione basata su cookie e round robin per il bilanciamento del carico del traffico.</span><span class="sxs-lookup"><span data-stu-id="10aa3-113">It supports capabilities such as SSL termination, cookie-based session affinity, and round robin for load balancing traffic.</span></span> <span data-ttu-id="10aa3-114">Load Balancer esegue il bilanciamento del carico del traffico al livello 4 (TCP/UDP).</span><span class="sxs-lookup"><span data-stu-id="10aa3-114">Load Balancer, load balances traffic at layer 4 (TCP/UDP).</span></span>

<span data-ttu-id="10aa3-115">**D. Quali protocolli supporta il gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-115">**Q. What protocols does Application Gateway support?**</span></span>

<span data-ttu-id="10aa3-116">Il gateway applicazione supporta HTTP, HTTPS e WebSocket.</span><span class="sxs-lookup"><span data-stu-id="10aa3-116">Application Gateway supports HTTP, HTTPS, and WebSocket.</span></span>

<span data-ttu-id="10aa3-117">**D. Quali risorse sono supportate oggi nell'ambito del pool back-end?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-117">**Q. What resources are supported today as part of backend pool?**</span></span>

<span data-ttu-id="10aa3-118">I pool back-end possono essere costituiti da schede di interfaccia di rete, set di scalabilità di macchine virtuali, indirizzi IP pubblici, indirizzi IP interni, nomi di dominio completi (FQDN) e back-end multi-tenant come App Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="10aa3-118">Backend pools can be composed of NICs, virtual machine scale sets, public IPs, internal IPs, fully qualified domain names (FQDN), and multi-tenant back-ends like Azure Web Apps.</span></span> <span data-ttu-id="10aa3-119">Gateway applicazione non sono membri del pool back-end legati tooan set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="10aa3-119">Application Gateway backend pool members are not tied tooan availability set.</span></span> <span data-ttu-id="10aa3-120">I membri del pool back-end possono trovarsi tra cluster, data center o all'esterno di Azure, purché abbiano connettività IP.</span><span class="sxs-lookup"><span data-stu-id="10aa3-120">Members of backend pools can be across clusters, data centers, or outside of Azure as long as they have IP connectivity.</span></span>

<span data-ttu-id="10aa3-121">**D. Le aree è disponibile nel servizio di hello?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-121">**Q. What regions is hello service available in?**</span></span>

<span data-ttu-id="10aa3-122">Il gateway applicazione è disponibile in tutte le aree di Azure globale.</span><span class="sxs-lookup"><span data-stu-id="10aa3-122">Application Gateway is available in all regions of global Azure.</span></span> <span data-ttu-id="10aa3-123">È anche disponibile in [Azure Cina](https://www.azure.cn/) e [Azure per enti pubblici](https://azure.microsoft.com/en-us/overview/clouds/government/)</span><span class="sxs-lookup"><span data-stu-id="10aa3-123">It is also available in [Azure China](https://www.azure.cn/) and [Azure Government](https://azure.microsoft.com/en-us/overview/clouds/government/)</span></span>

<span data-ttu-id="10aa3-124">**D. Si tratta di una distribuzione dedicata per la sottoscrizione o è condivisa tra clienti?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-124">**Q. Is this a dedicated deployment for my subscription or is it shared across customers?**</span></span>

<span data-ttu-id="10aa3-125">Il gateway applicazione è una distribuzione dedicata nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="10aa3-125">Application Gateway is a dedicated deployment in your virtual network.</span></span>

<span data-ttu-id="10aa3-126">**D. È supportato il reindirizzamento HTTP->HTTPS?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-126">**Q. Is HTTP->HTTPS redirection supported?**</span></span>

<span data-ttu-id="10aa3-127">Il reindirizzamento è supportato.</span><span class="sxs-lookup"><span data-stu-id="10aa3-127">Redirection is supported.</span></span> <span data-ttu-id="10aa3-128">Visitare [Panoramica di reindirizzamento Gateway applicazione](application-gateway-redirect-overview.md) toolearn altre.</span><span class="sxs-lookup"><span data-stu-id="10aa3-128">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) toolearn more.</span></span>

<span data-ttu-id="10aa3-129">**D. In quale ordine vengono elaborati i listener?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-129">**Q. In what order are listeners processed?**</span></span>

<span data-ttu-id="10aa3-130">I listener vengono elaborati in ordine di hello che vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="10aa3-130">Listeners are processed in hello order they are shown.</span></span> <span data-ttu-id="10aa3-131">Per tale motivo, se un listener di base corrisponde a una richiesta in ingresso, questa viene elaborata per prima.</span><span class="sxs-lookup"><span data-stu-id="10aa3-131">For that reason if a basic listener matches an incoming request it processes it first.</span></span>  <span data-ttu-id="10aa3-132">Multisito listener devono essere configurate prima un traffico tooensure base listener è indirizzato toohello corretto back-end.</span><span class="sxs-lookup"><span data-stu-id="10aa3-132">Multi-site listeners should be configured before a basic listener tooensure traffic is routed toohello correct back-end.</span></span>

<span data-ttu-id="10aa3-133">**D. Dove è possibile trovare IP e DNS del gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-133">**Q. Where do I find Application Gateway’s IP and DNS?**</span></span>

<span data-ttu-id="10aa3-134">Quando si utilizza un indirizzo IP pubblico come un endpoint, queste informazioni sono reperibile nella risorsa di indirizzo IP pubblica hello o nella pagina di panoramica hello per hello Gateway applicazione nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="10aa3-134">When using a public IP address as an endpoint, this information can be found on hello public IP address resource or on hello Overview page for hello Application Gateway in hello portal.</span></span> <span data-ttu-id="10aa3-135">Per gli indirizzi IP interni, si trova nella pagina di panoramica hello.</span><span class="sxs-lookup"><span data-stu-id="10aa3-135">For internal IP addresses, this can be found on hello Overview page.</span></span>

<span data-ttu-id="10aa3-136">**D. Hello IP o DNS modifica nel corso della durata di Gateway applicazione hello hello?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-136">**Q. Does hello IP or DNS change over hello lifetime of hello Application Gateway?**</span></span>

<span data-ttu-id="10aa3-137">Hello VIP può cambiare se gateway hello viene arrestato e avviato dal cliente hello.</span><span class="sxs-lookup"><span data-stu-id="10aa3-137">hello VIP can change if hello gateway is stopped and started by hello customer.</span></span> <span data-ttu-id="10aa3-138">Hello DNS associato al Gateway applicazione non cambia nel ciclo di vita di hello del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="10aa3-138">hello DNS associated with Application Gateway does not change over hello lifecycle of hello gateway.</span></span> <span data-ttu-id="10aa3-139">Per questo motivo, è consigliabile toouse un alias CNAME e indirizzarlo toohello dell'indirizzo DNS del Gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="10aa3-139">For this reason, it is recommended toouse a CNAME alias and point it toohello DNS address of hello Application Gateway.</span></span>

<span data-ttu-id="10aa3-140">**D. Il gateway applicazione supporta l'IP statico?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-140">**Q. Does Application Gateway support static IP?**</span></span>

<span data-ttu-id="10aa3-141">No, il gateway applicazione non supporta indirizzi IP pubblici statici, ma supporta indirizzi IP interni statici.</span><span class="sxs-lookup"><span data-stu-id="10aa3-141">No, Application Gateway does not support static public IP addresses, but it does support static internal IPs.</span></span>

<span data-ttu-id="10aa3-142">**D. Gateway applicazione supporta più indirizzi IP pubblici nel gateway hello?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-142">**Q. Does Application Gateway support multiple public IPs on hello gateway?**</span></span>

<span data-ttu-id="10aa3-143">Il gateway applicazione supporta un solo indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="10aa3-143">Only one public IP address is supported on an Application Gateway.</span></span>

<span data-ttu-id="10aa3-144">**D. Il gateway applicazione supporta le intestazioni x-forwarded-for?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-144">**Q. Does Application Gateway support x-forwarded-for headers?**</span></span>

<span data-ttu-id="10aa3-145">Sì, Gateway applicazione inserisce x-inoltrati-per, proto inoltrati x e porta inoltrati x di intestazioni nella richiesta di hello inoltrati toohello di back-end.</span><span class="sxs-lookup"><span data-stu-id="10aa3-145">Yes, Application Gateway inserts x-forwarded-for, x-forwarded-proto, and x-forwarded-port headers into hello request forwarded toohello backend.</span></span> <span data-ttu-id="10aa3-146">formato di Hello per l'intestazione x-inoltrati-per è un elenco delimitato da virgole di creato.</span><span class="sxs-lookup"><span data-stu-id="10aa3-146">hello format for x-forwarded-for header is a comma-separated list of IP:Port.</span></span> <span data-ttu-id="10aa3-147">i valori validi di Hello per proto inoltrati x sono http o https.</span><span class="sxs-lookup"><span data-stu-id="10aa3-147">hello valid values for x-forwarded-proto are http or https.</span></span> <span data-ttu-id="10aa3-148">Porta inoltrati X specifica porta hello quali richiesta hello raggiunto al Gateway applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="10aa3-148">X-forwarded-port specifies hello port at which hello request reached at hello Application Gateway.</span></span>

<span data-ttu-id="10aa3-149">**D. Quanto tempo occorre toodeploy un Gateway applicazione? Il gateway applicazione funziona durante l'aggiornamento?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-149">**Q. How long does it take toodeploy an Application Gateway? Does my Application Gateway still work when being updated?**</span></span>

<span data-ttu-id="10aa3-150">Nuove distribuzioni di Gateway applicazione possono richiedere too20 minuti tooprovision.</span><span class="sxs-lookup"><span data-stu-id="10aa3-150">New Application Gateway deployments can take up too20 minutes tooprovision.</span></span> <span data-ttu-id="10aa3-151">Le modifiche tooinstance di conteggio/dimensioni non siano distruttive e gateway hello rimane attiva durante l'operazione.</span><span class="sxs-lookup"><span data-stu-id="10aa3-151">Changes tooinstance size/count are not disruptive, and hello gateway remains active during this time.</span></span>

## <a name="configuration"></a><span data-ttu-id="10aa3-152">Configurazione</span><span class="sxs-lookup"><span data-stu-id="10aa3-152">Configuration</span></span>

<span data-ttu-id="10aa3-153">**D. Il gateway applicazione viene sempre distribuito in una rete virtuale?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-153">**Q. Is Application Gateway always deployed in a virtual network?**</span></span>

<span data-ttu-id="10aa3-154">Sì, il gateway applicazione viene sempre distribuito in una subnet di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="10aa3-154">Yes, Application Gateway is always deployed in a virtual network subnet.</span></span> <span data-ttu-id="10aa3-155">Questa subnet può contenere solo gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="10aa3-155">This subnet can only contain Application Gateways.</span></span>

<span data-ttu-id="10aa3-156">**D. Gateway applicazione possono comunicare con tooinstances all'esterno della rete virtuale?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-156">**Q. Can Application Gateway talk tooinstances outside its virtual network?**</span></span>

<span data-ttu-id="10aa3-157">Gateway applicazione in grado di comunicare tooinstances all'esterno di rete virtuale hello in esso contenuto, purché vi sia connettività IP.</span><span class="sxs-lookup"><span data-stu-id="10aa3-157">Application Gateway can talk tooinstances outside of hello virtual network that it is in as long as there is IP connectivity.</span></span> <span data-ttu-id="10aa3-158">Se si prevede di toouse richiede indirizzi IP interni come membri del pool back-end, verrà [Peering reti VIRTUALI](../virtual-network/virtual-network-peering-overview.md) o [Gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="10aa3-158">If you plan toouse internal IPs as backend pool members, then it requires [VNET Peering](../virtual-network/virtual-network-peering-overview.md) or [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>

<span data-ttu-id="10aa3-159">**D. È possibile distribuire qualsiasi altro elemento nella subnet del Gateway applicazione hello?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-159">**Q. Can I deploy anything else in hello Application Gateway subnet?**</span></span>

<span data-ttu-id="10aa3-160">No, ma è possibile distribuire altri gateway applicazione nella subnet hello.</span><span class="sxs-lookup"><span data-stu-id="10aa3-160">No, but you can deploy other application gateways in hello subnet.</span></span>

<span data-ttu-id="10aa3-161">**D. Gruppi di sicurezza di rete sono supportati nella subnet del Gateway applicazione hello?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-161">**Q. Are Network Security Groups supported on hello Application Gateway subnet?**</span></span>

<span data-ttu-id="10aa3-162">Gruppi di sicurezza di rete sono supportati nella subnet del Gateway applicazione hello con hello seguenti restrizioni:</span><span class="sxs-lookup"><span data-stu-id="10aa3-162">Network Security Groups are supported on hello Application Gateway subnet with hello following restrictions:</span></span>

* <span data-ttu-id="10aa3-163">Le eccezioni devono essere inserite per il traffico in ingresso sulle porte 65503 65534 per toowork integrità back-end in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="10aa3-163">Exceptions must be put in for incoming traffic on ports 65503-65534 for backend health toowork correctly.</span></span>

* <span data-ttu-id="10aa3-164">La connettività Internet in uscita non può essere bloccata.</span><span class="sxs-lookup"><span data-stu-id="10aa3-164">Outbound internet connectivity can not be blocked.</span></span>

* <span data-ttu-id="10aa3-165">È necessario consentire il traffico proveniente da hello tag AzureLoadBalancer.</span><span class="sxs-lookup"><span data-stu-id="10aa3-165">Traffic from hello AzureLoadBalancer tag must be allowed.</span></span>

<span data-ttu-id="10aa3-166">**D. Quali sono i limiti di hello gateway applicazione? È possibile aumentare questi limiti?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-166">**Q. What are hello limits on Application Gateway? Can I increase these limits?**</span></span>

<span data-ttu-id="10aa3-167">Visitare [limiti di Gateway applicazione](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello limiti.</span><span class="sxs-lookup"><span data-stu-id="10aa3-167">Visit [Application Gateway Limits](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello limits.</span></span>

<span data-ttu-id="10aa3-168">**D. È possibile usare il gateway applicazione per il traffico interno ed esterno contemporaneamente?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-168">**Q. Can I use Application Gateway for both external and internal traffic simultaneously?**</span></span>

<span data-ttu-id="10aa3-169">Sì, il gateway applicazione supporta un indirizzo IP interno e un indirizzo IP esterno.</span><span class="sxs-lookup"><span data-stu-id="10aa3-169">Yes, Application Gateway supports having one internal IP and one external IP per Application Gateway.</span></span>

<span data-ttu-id="10aa3-170">**D. Il peering reti virtuali è supportato?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-170">**Q. Is VNet peering supported?**</span></span>

<span data-ttu-id="10aa3-171">Sì, il peering reti virtuali è supportato ed è utile per il bilanciamento del carico del traffico in altre reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="10aa3-171">Yes, VNet peering is supported and is beneficial for load balancing traffic in other virtual networks.</span></span>

<span data-ttu-id="10aa3-172">**D. È possibile contattare i server locali tooon quando sono connessi da tunnel VPN o ExpressRoute?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-172">**Q. Can I talk tooon-premises servers when they are connected by ExpressRoute or VPN tunnels?**</span></span>

<span data-ttu-id="10aa3-173">Sì, se il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="10aa3-173">Yes, as long as traffic is allowed.</span></span>

<span data-ttu-id="10aa3-174">**D. È possibile avere un pool back-end che serve molte applicazioni su porte diverse?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-174">**Q. Can I have one backend pool serving many applications on different ports?**</span></span>

<span data-ttu-id="10aa3-175">L'architettura di microservizi è supportata.</span><span class="sxs-lookup"><span data-stu-id="10aa3-175">Micro service architecture is supported.</span></span> <span data-ttu-id="10aa3-176">Occorre più tooprobe configurate impostazioni di http su porte diverse.</span><span class="sxs-lookup"><span data-stu-id="10aa3-176">You would need multiple http settings configured tooprobe on different ports.</span></span>

<span data-ttu-id="10aa3-177">**D. I probe personalizzati supportano caratteri jolly o regex nei dati di risposta?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-177">**Q. Do custom probes support wildcards/regex on response data?**</span></span>

<span data-ttu-id="10aa3-178">I probe personalizzati non supportano caratteri jolly o regex nei dati di risposta.</span><span class="sxs-lookup"><span data-stu-id="10aa3-178">Custom probes do not support wildcard or regex on response data.</span></span> 

<span data-ttu-id="10aa3-179">**D. Come vengono elaborate le regole?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-179">**Q. How are rules processed?**</span></span>

<span data-ttu-id="10aa3-180">Le regole vengono elaborate nell'ordine di hello che sono configurati.</span><span class="sxs-lookup"><span data-stu-id="10aa3-180">Rules are processed in hello order they are configured.</span></span> <span data-ttu-id="10aa3-181">È consigliabile che le regole di multi-sito siano configurate prima possibilità di hello tooreduce regole di base che il traffico viene instradato back-end inappropriato toohello come regola di base hello corrisponderebbe traffico in base alla regola di porta multisito toohello precedente viene valutato.</span><span class="sxs-lookup"><span data-stu-id="10aa3-181">It is recommended that multi-site rules are configured before basic rules tooreduce hello chance that traffic is routed toohello inappropriate backend as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="10aa3-182">**D. Come vengono elaborate le regole?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-182">**Q. How are rules processed?**</span></span>

<span data-ttu-id="10aa3-183">Le regole vengono elaborate in ordine di hello che sono stati creati.</span><span class="sxs-lookup"><span data-stu-id="10aa3-183">Rules are processed in hello order they are created.</span></span> <span data-ttu-id="10aa3-184">È consigliabile configurare le regole multisito prima delle regole di base.</span><span class="sxs-lookup"><span data-stu-id="10aa3-184">It is recommended that multi-site rules are configured before basic rules.</span></span> <span data-ttu-id="10aa3-185">Configurando innanzitutto listener multisito, questa configurazione riduce il possibilità hello che il traffico sia indirizzato toohello inappropriato backend.</span><span class="sxs-lookup"><span data-stu-id="10aa3-185">By configuring multi-site listeners first, this configuration reduces hello chance that traffic is routed toohello inappropriate backend.</span></span> <span data-ttu-id="10aa3-186">Come regola di base hello corrisponderebbe traffico in base alla regola di porta multisito toohello precedente viene valutata, può verificarsi questo problema di routing.</span><span class="sxs-lookup"><span data-stu-id="10aa3-186">This routing issue can occur as hello basic rule would match traffic based on port prior toohello multi-site rule being evaluated.</span></span>

<span data-ttu-id="10aa3-187">**D. Cosa indicano il campo Host hello per le ricerche personalizzate?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-187">**Q. What does hello Host field for custom probes signify?**</span></span>

<span data-ttu-id="10aa3-188">Il campo host specifica hello Nome toosend hello probe.</span><span class="sxs-lookup"><span data-stu-id="10aa3-188">Host field specifies hello name toosend hello probe to.</span></span> <span data-ttu-id="10aa3-189">Applicabile solo quando vengono configurati più siti nel gateway applicazione. In caso contrario, usare "127.0.0.1".</span><span class="sxs-lookup"><span data-stu-id="10aa3-189">Applicable only when multi-site is configured on Application Gateway, otherwise use '127.0.0.1'.</span></span> <span data-ttu-id="10aa3-190">Questo valore è diverso dal nome host della VM ed è nel formato \<protocollo\>://\<host\>:\<porta\>\<percorso\>.</span><span class="sxs-lookup"><span data-stu-id="10aa3-190">This value is different from VM host name and is in format \<protocol\>://\<host\>:\<port\>\<path\>.</span></span>

<span data-ttu-id="10aa3-191">**D. È possibile whitelist Gateway applicazione accesso tooa alcuni indirizzi IP di origine?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-191">**Q. Can I whitelist Application Gateway access tooa few source IPs?**</span></span>

<span data-ttu-id="10aa3-192">Questo scenario è possibile usando gruppi di sicurezza di rete nella subnet del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="10aa3-192">This scenario can be done using NSGs on Application Gateway subnet.</span></span> <span data-ttu-id="10aa3-193">nella subnet hello in hello all'ordine di priorità, è necessario inserire Hello seguenti restrizioni:</span><span class="sxs-lookup"><span data-stu-id="10aa3-193">hello following restrictions should be put on hello subnet in hello listed order of priority:</span></span>

* <span data-ttu-id="10aa3-194">Consentire il traffico in ingresso dall'intervallo di IP/IP di origine.</span><span class="sxs-lookup"><span data-stu-id="10aa3-194">Allow incoming traffic from source IP/IP range.</span></span>

* <span data-ttu-id="10aa3-195">Consentire le richieste in ingresso da tutte le origini tooports 65503 65534 per [comunicazione integrità back-end](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="10aa3-195">Allow incoming requests from all sources tooports 65503-65534 for [backend health communication](application-gateway-diagnostics.md).</span></span>

* <span data-ttu-id="10aa3-196">Consentire hello in arrivo probe di bilanciamento del carico di Azure (tag AzureLoadBalancer) e traffico di rete virtuale in ingresso (tag VirtualNetwork) [NSG](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="10aa3-196">Allow incoming Azure Load Balancer probes (AzureLoadBalancer tag) and inbound virtual network traffic (VirtualNetwork tag) on hello [NSG](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="10aa3-197">Bloccare tutto il traffico in ingresso con una regola Nega tutto.</span><span class="sxs-lookup"><span data-stu-id="10aa3-197">Block all other incoming traffic with a Deny all rule.</span></span>

* <span data-ttu-id="10aa3-198">Consentire il traffico in uscita toohello internet per tutte le destinazioni.</span><span class="sxs-lookup"><span data-stu-id="10aa3-198">Allow outbound traffic toohello internet for all destinations.</span></span>

## <a name="performance"></a><span data-ttu-id="10aa3-199">Prestazioni</span><span class="sxs-lookup"><span data-stu-id="10aa3-199">Performance</span></span>

<span data-ttu-id="10aa3-200">**D. In che modo il gateway applicazione supporta la disponibilità elevata e la scalabilità?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-200">**Q. How does Application Gateway support high availability and scalability?**</span></span>

<span data-ttu-id="10aa3-201">Il gateway applicazione supporta scenari di disponibilità elevata se sono presenti due o più istanze distribuite.</span><span class="sxs-lookup"><span data-stu-id="10aa3-201">Application Gateway supports high availability scenarios when you have two or more instances deployed.</span></span> <span data-ttu-id="10aa3-202">Azure distribuisce tali istanze tra tooensure di domini di aggiornamento e di errore che tutte le istanze non viene in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="10aa3-202">Azure distributes these instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="10aa3-203">Gateway applicazione supporta la scalabilità mediante l'aggiunta di più istanze di hello stesso carico di hello tooshare gateway.</span><span class="sxs-lookup"><span data-stu-id="10aa3-203">Application Gateway supports scalability by adding multiple instances of hello same gateway tooshare hello load.</span></span>

<span data-ttu-id="10aa3-204">**D. Come si ottiene uno scenario di ripristino di emergenza tra data center con un gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-204">**Q. How do I achieve DR scenario across data centers with Application Gateway?**</span></span>

<span data-ttu-id="10aa3-205">I clienti possono utilizzare toodistribute Traffic Manager il traffico tra più applicazioni gateway in diversi Data Center.</span><span class="sxs-lookup"><span data-stu-id="10aa3-205">Customers can use Traffic Manager toodistribute traffic across multiple Application Gateways in different datacenters.</span></span>

<span data-ttu-id="10aa3-206">**D. La scalabilità automatica è supportata?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-206">**Q. Is auto scaling supported?**</span></span>

<span data-ttu-id="10aa3-207">No, ma Gateway applicazione dispone di una metrica di velocità effettiva che può essere utilizzato tooalert quando viene raggiunta una soglia.</span><span class="sxs-lookup"><span data-stu-id="10aa3-207">No, but Application Gateway has a throughput metric that can be used tooalert you when a threshold is reached.</span></span> <span data-ttu-id="10aa3-208">Manualmente le istanze di aggiunta o modifica delle dimensioni non viene riavviato gateway hello e non influisce sulla traffico esistente.</span><span class="sxs-lookup"><span data-stu-id="10aa3-208">Manually adding instances or changing size does not restart hello gateway and does not impact existing traffic.</span></span>

<span data-ttu-id="10aa3-209">**D. Il ridimensionamento manuale causa tempi di inattività?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-209">**Q. Does manual scale up/down cause downtime?**</span></span>

<span data-ttu-id="10aa3-210">Non si verificano tempi di inattività, le istanze vengono distribuite tra domini di aggiornamento e domini di errore.</span><span class="sxs-lookup"><span data-stu-id="10aa3-210">There is no downtime, instances are distributed across upgrade domains and fault domains.</span></span>

<span data-ttu-id="10aa3-211">**D. È possibile modificare le dimensioni di istanza da medium toolarge senza interruzioni?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-211">**Q. Can I change instance size from medium toolarge without disruption?**</span></span>

<span data-ttu-id="10aa3-212">Sì, Azure distribuisce le istanze in tooensure di domini di aggiornamento e di errore che tutte le istanze non viene in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="10aa3-212">Yes, Azure distributes instances across update and fault domains tooensure that all instances do not fail at hello same time.</span></span> <span data-ttu-id="10aa3-213">Supporta il Gateway applicazione ridimensionamento aggiungendo più istanze di hello stesso carico di hello tooshare gateway.</span><span class="sxs-lookup"><span data-stu-id="10aa3-213">Application Gateway supports scaling by adding multiple instances of hello same gateway tooshare hello load.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="10aa3-214">Configurazione SSL</span><span class="sxs-lookup"><span data-stu-id="10aa3-214">SSL Configuration</span></span>

<span data-ttu-id="10aa3-215">**D. Quali certificati sono supportati dal gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-215">**Q. What certificates are supported on Application Gateway?**</span></span>

<span data-ttu-id="10aa3-216">Sono supportati certificati autofirmati, certificati della CA e certificati con caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="10aa3-216">Self signed certs, CA certs, and wild-card certs are supported.</span></span> <span data-ttu-id="10aa3-217">I certificati di convalida estesa non sono supportati.</span><span class="sxs-lookup"><span data-stu-id="10aa3-217">EV certs are not supported.</span></span>

<span data-ttu-id="10aa3-218">**D. Quali sono hello corrente pacchetti di crittografia supportati dal Gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-218">**Q. What are hello current cipher suites supported by Application Gateway?**</span></span>

<span data-ttu-id="10aa3-219">di seguito Hello sono hello corrente pacchetti di crittografia supportati dal gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="10aa3-219">hello following are hello current cipher suites supported by application gateway.</span></span> <span data-ttu-id="10aa3-220">Visita: [Configura SSL le versioni dei criteri e i pacchetti di crittografia nel Gateway applicazione](application-gateway-configure-ssl-policy-powershell.md) toolearn come opzioni SSL toocustomize.</span><span class="sxs-lookup"><span data-stu-id="10aa3-220">Visit: [Configure SSL policy versions and cipher suites on Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn how toocustomize SSL options.</span></span>

- <span data-ttu-id="10aa3-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="10aa3-221">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="10aa3-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="10aa3-222">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="10aa3-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="10aa3-223">TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="10aa3-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="10aa3-224">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="10aa3-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="10aa3-225">TLS_DHE_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="10aa3-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="10aa3-226">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="10aa3-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="10aa3-227">TLS_DHE_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="10aa3-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="10aa3-228">TLS_DHE_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="10aa3-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="10aa3-229">TLS_RSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="10aa3-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="10aa3-230">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="10aa3-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="10aa3-231">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="10aa3-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="10aa3-232">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="10aa3-233">TLS_RSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="10aa3-233">TLS_RSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="10aa3-234">TLS_RSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="10aa3-234">TLS_RSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="10aa3-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="10aa3-235">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
- <span data-ttu-id="10aa3-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="10aa3-236">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>
- <span data-ttu-id="10aa3-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span><span class="sxs-lookup"><span data-stu-id="10aa3-237">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384</span></span>
- <span data-ttu-id="10aa3-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="10aa3-238">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="10aa3-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="10aa3-239">TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="10aa3-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="10aa3-240">TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="10aa3-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="10aa3-241">TLS_DHE_DSS_WITH_AES_256_CBC_SHA256</span></span>
- <span data-ttu-id="10aa3-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="10aa3-242">TLS_DHE_DSS_WITH_AES_128_CBC_SHA256</span></span>
- <span data-ttu-id="10aa3-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="10aa3-243">TLS_DHE_DSS_WITH_AES_256_CBC_SHA</span></span>
- <span data-ttu-id="10aa3-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="10aa3-244">TLS_DHE_DSS_WITH_AES_128_CBC_SHA</span></span>
- <span data-ttu-id="10aa3-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="10aa3-245">TLS_RSA_WITH_3DES_EDE_CBC_SHA</span></span>
- <span data-ttu-id="10aa3-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span><span class="sxs-lookup"><span data-stu-id="10aa3-246">TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA</span></span>

<span data-ttu-id="10aa3-247">**D. Gateway applicazione supporta inoltre la riesecuzione della crittografia di back-end toohello traffico?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-247">**Q. Does Application Gateway also support re-encryption of traffic toohello backend?**</span></span>

<span data-ttu-id="10aa3-248">Sì, offload SSL di Gateway applicazione supporta e fine tooend SSL, che crittografa nuovamente hello back-end toohello di traffico.</span><span class="sxs-lookup"><span data-stu-id="10aa3-248">Yes, Application Gateway supports SSL offload, and end tooend SSL, which re-encrypts hello traffic toohello backend.</span></span>

<span data-ttu-id="10aa3-249">**D. È possibile configurare le versioni protocollo SSL toocontrol dei criteri SSL?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-249">**Q. Can I configure SSL policy toocontrol SSL Protocol versions?**</span></span>

<span data-ttu-id="10aa3-250">Sì, è possibile configurare il Gateway applicazione toodeny TLS 1.0, TLS 1.1 e TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="10aa3-250">Yes, you can configure Application Gateway toodeny TLS1.0, TLS1.1, and TLS1.2.</span></span> <span data-ttu-id="10aa3-251">SSL 2.0 e 3.0 sono già disabilitati per impostazione predefinita e non sono configurabili.</span><span class="sxs-lookup"><span data-stu-id="10aa3-251">SSL 2.0 and 3.0 are already disabled by default and are not configurable.</span></span>

<span data-ttu-id="10aa3-252">**D. È possibile configurare l'ordine dei pacchetti di crittografia e dei criteri?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-252">**Q. Can I configure cipher suites and policy order?**</span></span>

<span data-ttu-id="10aa3-253">Sì, la [configurazione dei pacchetti di crittografia](application-gateway-ssl-policy-overview.md) è supportata.</span><span class="sxs-lookup"><span data-stu-id="10aa3-253">Yes, [configuration of cipher suites](application-gateway-ssl-policy-overview.md) is supported.</span></span> <span data-ttu-id="10aa3-254">Quando si definisce un criterio personalizzato, almeno uno dei seguenti pacchetti di crittografia hello deve essere abilitato.</span><span class="sxs-lookup"><span data-stu-id="10aa3-254">When defining a custom policy, at least one of hello following cipher suites must be enabled.</span></span> <span data-ttu-id="10aa3-255">Gateway applicazione utilizza la gestione di back-end toofor SHA256.</span><span class="sxs-lookup"><span data-stu-id="10aa3-255">Application gateway uses SHA256 toofor backend management.</span></span>

* <span data-ttu-id="10aa3-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="10aa3-256">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
* <span data-ttu-id="10aa3-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="10aa3-257">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
* <span data-ttu-id="10aa3-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="10aa3-258">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="10aa3-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="10aa3-259">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
* <span data-ttu-id="10aa3-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="10aa3-260">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
* <span data-ttu-id="10aa3-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="10aa3-261">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

<span data-ttu-id="10aa3-262">**D. Quanti certificati SSL sono supportati?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-262">**Q. How many SSL certificates are supported?**</span></span>

<span data-ttu-id="10aa3-263">Configurazione SSL too20 sono supportati i certificati.</span><span class="sxs-lookup"><span data-stu-id="10aa3-263">Up too20 SSL certificates are supported.</span></span>

<span data-ttu-id="10aa3-264">**D. Quanti certificati di autenticazione sono supportati per la ripetizione della crittografia nel back-end?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-264">**Q. How many authentication certificates for backend re-encryption are supported?**</span></span>

<span data-ttu-id="10aa3-265">Backup too10 certificati di autenticazione sono supportati con un valore predefinito è 5.</span><span class="sxs-lookup"><span data-stu-id="10aa3-265">Up too10 authentication certificates are supported with a default of 5.</span></span>

<span data-ttu-id="10aa3-266">**D. Il gateway applicazione si integra con Azure Key Vault in modo nativo?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-266">**Q. Does Application Gateway integrate with Azure Key Vault natively?**</span></span>

<span data-ttu-id="10aa3-267">No, non è integrato con Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="10aa3-267">No, it is not integrated with Azure Key Vault.</span></span>

## <a name="web-application-firewall-waf-configuration"></a><span data-ttu-id="10aa3-268">Configurazione del Web application firewall (WAF)</span><span class="sxs-lookup"><span data-stu-id="10aa3-268">Web Application Firewall (WAF) Configuration</span></span>

<span data-ttu-id="10aa3-269">**D. Hello SKU WAF offre tutte le funzionalità di hello disponibili con hello SKU Standard?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-269">**Q. Does hello WAF SKU offer all hello features available with hello Standard SKU?**</span></span>

<span data-ttu-id="10aa3-270">Sì, WAF supporta tutte le funzionalità di hello hello SKU Standard.</span><span class="sxs-lookup"><span data-stu-id="10aa3-270">Yes, WAF supports all hello features in hello Standard SKU.</span></span>

<span data-ttu-id="10aa3-271">**D. Qual è la versione di hello CRS che supporta Gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-271">**Q. What is hello CRS version Application Gateway supports?**</span></span>

<span data-ttu-id="10aa3-272">Il gateway applicazione supporta CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) e CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span><span class="sxs-lookup"><span data-stu-id="10aa3-272">Application Gateway supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).</span></span>

<span data-ttu-id="10aa3-273">**D. Come si monitora il Web application firewall?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-273">**Q. How do I monitor WAF?**</span></span>

<span data-ttu-id="10aa3-274">Il Web application firewall viene monitorato tramite la registrazione diagnostica. Per altre informazioni sulla registrazione diagnostica, vedere [Integrità back-end, registrazione diagnostica e metriche per il gateway applicazione](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="10aa3-274">WAF is monitored through diagnostic logging, more information on diagnostic logging can be found at [Diagnostics Logging and Metrics for Application Gateway](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="10aa3-275">**D. La modalità di rilevamento blocca il traffico?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-275">**Q. Does detection mode block traffic?**</span></span>

<span data-ttu-id="10aa3-276">No, la modalità di rilevamento registra solo il traffico che ha attivato una regola del Web application firewall.</span><span class="sxs-lookup"><span data-stu-id="10aa3-276">No, detection mode only logs traffic, which triggered a WAF rule.</span></span>

<span data-ttu-id="10aa3-277">**D. Come si personalizzano le regole del Web application firewall?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-277">**Q. How do I customize WAF rules?**</span></span>

<span data-ttu-id="10aa3-278">Sì, le regole di WAF sono personalizzabili, per ulteriori informazioni su come essi toocustomize visitare [WAF personalizzare regole e gruppi di regole](application-gateway-customize-waf-rules-portal.md)</span><span class="sxs-lookup"><span data-stu-id="10aa3-278">Yes, WAF rules are customizable, for more information on how toocustomize them visit [Customize WAF rule groups and rules](application-gateway-customize-waf-rules-portal.md)</span></span>

<span data-ttu-id="10aa3-279">**D. Quali regole sono attualmente disponibili?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-279">**Q. What rules are currently available?**</span></span>

<span data-ttu-id="10aa3-280">WAF supporta attualmente CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) e [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), che forniscono la protezione di base con la maggior parte delle hello vulnerabilità primi 10 identificata da hello aprire Web applicazione sicurezza progetto (OWASP) fare clic qui [OWASP le prime 10 vulnerabilità](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span><span class="sxs-lookup"><span data-stu-id="10aa3-280">WAF currently supports CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) and [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), which provide baseline security against most of hello top 10 vulnerabilities identified by hello Open Web Application Security Project (OWASP) found here [OWASP top 10 Vulnerabilities](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)</span></span>

* <span data-ttu-id="10aa3-281">Protezione dagli attacchi SQL injection</span><span class="sxs-lookup"><span data-stu-id="10aa3-281">SQL injection protection</span></span>

* <span data-ttu-id="10aa3-282">Protezione dagli attacchi di scripting intersito</span><span class="sxs-lookup"><span data-stu-id="10aa3-282">Cross site scripting protection</span></span>

* <span data-ttu-id="10aa3-283">Protezione dai comuni attacchi Web, ad esempio attacchi di iniezione di comandi, richieste HTTP non valide, attacchi HTTP Response Splitting e Remote File Inclusion</span><span class="sxs-lookup"><span data-stu-id="10aa3-283">Common Web Attacks Protection such as command injection, HTTP request smuggling, HTTP response splitting, and remote file inclusion attack</span></span>

* <span data-ttu-id="10aa3-284">Protezione dalle violazioni del protocollo HTTP</span><span class="sxs-lookup"><span data-stu-id="10aa3-284">Protection against HTTP protocol violations</span></span>

* <span data-ttu-id="10aa3-285">Protezione contro eventuali anomalie del protocollo HTTP, ad esempio user agent host mancante e accept header</span><span class="sxs-lookup"><span data-stu-id="10aa3-285">Protection against HTTP protocol anomalies such as missing host user-agent and accept headers</span></span>

* <span data-ttu-id="10aa3-286">Prevenzione contro robot, crawler e scanner</span><span class="sxs-lookup"><span data-stu-id="10aa3-286">Prevention against bots, crawlers, and scanners</span></span>

* <span data-ttu-id="10aa3-287">Rilevamento di errori di configurazione dell'applicazione comuni (ad esempio, Apache, IIS e così via)</span><span class="sxs-lookup"><span data-stu-id="10aa3-287">Detection of common application misconfigurations (that is, Apache, IIS, etc.)</span></span>

<span data-ttu-id="10aa3-288">**D. Il WAF supporta anche la prevenzione DDoS?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-288">**Q. Does WAF also support DDoS prevention?**</span></span>

<span data-ttu-id="10aa3-289">No, non fornisce la prevenzione DDoS.</span><span class="sxs-lookup"><span data-stu-id="10aa3-289">No, WAF does not provide DDoS prevention.</span></span>

## <a name="diagnostics-and-logging"></a><span data-ttu-id="10aa3-290">Diagnostica e registrazione</span><span class="sxs-lookup"><span data-stu-id="10aa3-290">Diagnostics and Logging</span></span>

<span data-ttu-id="10aa3-291">**D. Quali tipi di log sono disponibili con il gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-291">**Q. What types of logs are available with Application Gateway?**</span></span>

<span data-ttu-id="10aa3-292">Sono disponibili tre log con il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="10aa3-292">There are three logs available for Application Gateway.</span></span> <span data-ttu-id="10aa3-293">Per altre informazioni su questi log e altre funzionalità di diagnostica, vedere [Integrità back-end, log di diagnostica e metriche per il gateway applicazione](application-gateway-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="10aa3-293">For more information on these logs and other diagnostic capabilities, visit [Backend health, diagnostics logs, and metrics for Application Gateway](application-gateway-diagnostics.md).</span></span>

- <span data-ttu-id="10aa3-294">**ApplicationGatewayAccessLog** -log di accesso hello contiene ogni richiesta inviata front-end di Gateway applicazione toohello.</span><span class="sxs-lookup"><span data-stu-id="10aa3-294">**ApplicationGatewayAccessLog** - hello access log contains each request submitted toohello Application Gateway frontend.</span></span> <span data-ttu-id="10aa3-295">dati Hello includono IP del chiamante hello, URL richiesto, latenza nella risposta, codice restituito, byte e la disconnessione. Il log di accesso viene raccolto ogni 300 secondi.</span><span class="sxs-lookup"><span data-stu-id="10aa3-295">hello data includes hello caller's IP, URL requested, response latency, return code, bytes in and out. Access log is collected every 300 seconds.</span></span> <span data-ttu-id="10aa3-296">Il log contiene un record per ogni istanza del gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="10aa3-296">This log contains one record per instance of Application Gateway.</span></span>
- <span data-ttu-id="10aa3-297">**ApplicationGatewayPerformanceLog** -log delle prestazioni hello acquisisce informazioni sulle prestazioni per ogni istanza incluso richiesta totale servita, velocità effettiva in byte, numero totale di richieste servite, numero di richieste non riuscite, corretti e non corretti numero di istanze di back-end.</span><span class="sxs-lookup"><span data-stu-id="10aa3-297">**ApplicationGatewayPerformanceLog** - hello performance log captures performance information on per instance basis including total request served, throughput in bytes, total requests served, failed request count, healthy and unhealthy back-end instance count.</span></span>
- <span data-ttu-id="10aa3-298">**ApplicationGatewayFirewallLog** -log firewall hello contiene le richieste che vengono registrate tramite la modalità di rilevamento o prevenzione di un gateway di applicazione che viene configurato con firewall applicazione web.</span><span class="sxs-lookup"><span data-stu-id="10aa3-298">**ApplicationGatewayFirewallLog** - hello firewall log contains requests that are logged through either detection or prevention mode of an application gateway that is configured with web application firewall.</span></span>

<span data-ttu-id="10aa3-299">**D. Come è possibile sapere se i membri del pool back-end sono integri?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-299">**Q. How do I know if my backend pool members are healthy?**</span></span>

<span data-ttu-id="10aa3-300">È possibile utilizzare i cmdlet di PowerShell hello `Get-AzureRmApplicationGatewayBackendHealth` o verificare l'integrità tramite il portale di hello visitando [diagnostica del Gateway applicazione](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="10aa3-300">You can use hello PowerShell cmdlet `Get-AzureRmApplicationGatewayBackendHealth` or verify health through hello portal by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

<span data-ttu-id="10aa3-301">**D. Che cos'è il criterio di conservazione hello nei log di diagnostica hello?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-301">**Q. What is hello retention policy on hello diagnostics logs?**</span></span>

<span data-ttu-id="10aa3-302">Account di archiviazione di flusso toohello clienti di log di diagnostica e se è possono impostare i criteri di conservazione hello in base alle loro specificate.</span><span class="sxs-lookup"><span data-stu-id="10aa3-302">Diagnostic logs flow toohello customers storage account and customers can set hello retention policy based on their preference.</span></span> <span data-ttu-id="10aa3-303">I log di diagnostica possono anche essere inviati tooan Hub eventi o Log Analitica.</span><span class="sxs-lookup"><span data-stu-id="10aa3-303">Diagnostic logs can also be sent tooan Event Hub or Log Analytics.</span></span> <span data-ttu-id="10aa3-304">Vedere [Diagnostica del gateway applicazione](application-gateway-diagnostics.md) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="10aa3-304">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) for more details.</span></span>

<span data-ttu-id="10aa3-305">**D. Come si ottengono i log di controllo per il gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-305">**Q. How do I get audit logs for Application Gateway?**</span></span>

<span data-ttu-id="10aa3-306">Sono disponibili log di controllo per il gateway applicazione.</span><span class="sxs-lookup"><span data-stu-id="10aa3-306">Audit logs are available for Application Gateway.</span></span> <span data-ttu-id="10aa3-307">Nel portale di hello, fare clic su **Log attività** nel pannello menu hello di un log di controllo di Gateway applicazione tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="10aa3-307">In hello portal, click **Activity Log** in hello menu blade of an Application Gateway tooaccess hello audit log.</span></span> 

<span data-ttu-id="10aa3-308">**D. È possibile impostare avvisi con il gateway applicazione?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-308">**Q. Can I set alerts with Application Gateway?**</span></span>

<span data-ttu-id="10aa3-309">Sì, il gateway applicazione supporta gli avvisi, che vengono configurati in base alle metriche.</span><span class="sxs-lookup"><span data-stu-id="10aa3-309">Yes, Application Gateway does support alerts, alerts are configured off metrics.</span></span>  <span data-ttu-id="10aa3-310">Gateway applicazione dispone attualmente di una metrica di "trasmissione", che può essere configurato tooalert.</span><span class="sxs-lookup"><span data-stu-id="10aa3-310">Application Gateway currently has a metric of "throughput", which can be configured tooalert.</span></span> <span data-ttu-id="10aa3-311">toolearn informazioni su avvisi, visitare [ricevere notifiche di avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="10aa3-311">toolearn more about alerts, visit [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>

<span data-ttu-id="10aa3-312">**D. L'integrità back-end restituisce uno stato sconosciuto. Quale potrebbe essere la causa?**</span><span class="sxs-lookup"><span data-stu-id="10aa3-312">**Q. Backend health returns unknown status, what could be causing this status?**</span></span>

<span data-ttu-id="10aa3-313">la causa più comune di Hello è back-end toohello di accesso è stato bloccato da un gruppo o un DNS personalizzato.</span><span class="sxs-lookup"><span data-stu-id="10aa3-313">hello most common reason is access toohello backend is being blocked by an NSG or custom DNS.</span></span> <span data-ttu-id="10aa3-314">Visitare [back-end integrità, la registrazione diagnostica e metriche per il Gateway applicazione](application-gateway-diagnostics.md) toolearn altre.</span><span class="sxs-lookup"><span data-stu-id="10aa3-314">Visit [Backend health, diagnostics logging, and metrics for Application Gateway](application-gateway-diagnostics.md) toolearn more.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10aa3-315">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="10aa3-315">Next Steps</span></span>

<span data-ttu-id="10aa3-316">informazioni sul Gateway applicazione visitare toolearn [tooApplication introduzione Gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="10aa3-316">toolearn more about Application Gateway visit [Introduction tooApplication Gateway](application-gateway-introduction.md).</span></span>
