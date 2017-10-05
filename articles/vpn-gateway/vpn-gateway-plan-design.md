---
title: Pianificazione e progettazione per connessioni cross-premise - Gateway VPN di Azure | Documentazione Microsoft
description: Informazioni sulla pianificazione e progettazione del gateway VPN per le connessioni Da rete virtuale a rete virtuale cross-premise e ibride
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 0ebc3ef4a64432e993dd6ed69766bb64544fe433
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a><span data-ttu-id="b0988-103">Pianificazione e progettazione per il gateway VPN</span><span class="sxs-lookup"><span data-stu-id="b0988-103">Planning and design for VPN Gateway</span></span>

<span data-ttu-id="b0988-104">Le operazioni di pianificazione e progettazione di connessioni cross-premise e da rete virtuale a rete virtuale possono essere molto semplici o piuttosto complicate, a seconda delle esigenze di rete.</span><span class="sxs-lookup"><span data-stu-id="b0988-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span></span> <span data-ttu-id="b0988-105">Questo articolo illustra in dettaglio alcune considerazioni di base sulla progettazione e sulla pianificazione.</span><span class="sxs-lookup"><span data-stu-id="b0988-105">This article walks you through basic planning and design considerations.</span></span>

## <span data-ttu-id="b0988-106"><a name="planning"></a>Pianificazione</span><span class="sxs-lookup"><span data-stu-id="b0988-106"><a name="planning"></a>Planning</span></span>

### <span data-ttu-id="b0988-107"><a name="compare"></a>Opzioni di connettività di più sedi locali</span><span class="sxs-lookup"><span data-stu-id="b0988-107"><a name="compare"></a>Cross-premises connectivity options</span></span>

<span data-ttu-id="b0988-108">Se si desidera connettere i siti locali in modo sicuro a una rete virtuale, sono disponibili tre modi diversi: Da sito a sito, Da punto a sito ed ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="b0988-108">If you want to connect your on-premises sites securely to a virtual network, you have three different ways to do so: Site-to-Site, Point-to-Site, and ExpressRoute.</span></span> <span data-ttu-id="b0988-109">Confrontare le diverse connessioni cross-premise disponibili.</span><span class="sxs-lookup"><span data-stu-id="b0988-109">Compare the different cross-premises connections that are available.</span></span> <span data-ttu-id="b0988-110">La scelta dell'opzione può dipendere da diversi fattori, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b0988-110">The option you choose can depend on various considerations, such as:</span></span>

* <span data-ttu-id="b0988-111">Che tipo di velocità effettiva richiede la soluzione?</span><span class="sxs-lookup"><span data-stu-id="b0988-111">What kind of throughput does your solution require?</span></span>
* <span data-ttu-id="b0988-112">Si desidera comunicare sulla rete Internet pubblica tramite VPN sicura o tramite una connessione privata?</span><span class="sxs-lookup"><span data-stu-id="b0988-112">Do you want to communicate over the public Internet via secure VPN, or over a private connection?</span></span>
* <span data-ttu-id="b0988-113">Si ha un indirizzo IP pubblico disponibile per l'utilizzo?</span><span class="sxs-lookup"><span data-stu-id="b0988-113">Do you have a public IP address available to use?</span></span>
* <span data-ttu-id="b0988-114">Si prevede di utilizzare un dispositivo VPN?</span><span class="sxs-lookup"><span data-stu-id="b0988-114">Are you planning to use a VPN device?</span></span> <span data-ttu-id="b0988-115">In tal caso, è compatibile?</span><span class="sxs-lookup"><span data-stu-id="b0988-115">If so, is it compatible?</span></span>
* <span data-ttu-id="b0988-116">Si connette un numero limitato di computer o si desidera una connessione permanente per il sito?</span><span class="sxs-lookup"><span data-stu-id="b0988-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span></span>
* <span data-ttu-id="b0988-117">Che tipo di gateway VPN è necessario per la soluzione che si desidera creare?</span><span class="sxs-lookup"><span data-stu-id="b0988-117">What type of VPN gateway is required for the solution you want to create?</span></span>
* <span data-ttu-id="b0988-118">Quale SKU del gateway è opportuno usare?</span><span class="sxs-lookup"><span data-stu-id="b0988-118">Which gateway SKU should you use?</span></span>

### <span data-ttu-id="b0988-119"><a name="planningtable"></a>Tabella di pianificazione</span><span class="sxs-lookup"><span data-stu-id="b0988-119"><a name="planningtable"></a>Planning table</span></span>

<span data-ttu-id="b0988-120">La tabella seguente può aiutare nella scelta della migliore opzione di connettività per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="b0988-120">The following table can help you decide the best connectivity option for your solution.</span></span>

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <span data-ttu-id="b0988-121"><a name="gwsku"></a>SKU del gateway</span><span class="sxs-lookup"><span data-stu-id="b0988-121"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <span data-ttu-id="b0988-122"><a name="wf"></a>Flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="b0988-122"><a name="wf"></a>Workflow</span></span>

<span data-ttu-id="b0988-123">L'elenco seguente descrive il flusso di lavoro comune per la connettività cloud:</span><span class="sxs-lookup"><span data-stu-id="b0988-123">The following list outlines the common workflow for cloud connectivity:</span></span>

1. <span data-ttu-id="b0988-124">Progettare e pianificare la topologia di connettività ed elencare gli spazi di indirizzi per tutte le reti a cui connettersi.</span><span class="sxs-lookup"><span data-stu-id="b0988-124">Design and plan your connectivity topology and list the address spaces for all networks you want to connect.</span></span>
2. <span data-ttu-id="b0988-125">Creare una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="b0988-125">Create an Azure virtual network.</span></span> 
3. <span data-ttu-id="b0988-126">Creare un gateway VPN per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="b0988-126">Create a VPN gateway for the virtual network.</span></span>
4. <span data-ttu-id="b0988-127">Creare e configurare le connessioni a reti locali o altre reti virtuali, se necessario.</span><span class="sxs-lookup"><span data-stu-id="b0988-127">Create and configure connections to on-premises networks or other virtual networks (as needed).</span></span>
5. <span data-ttu-id="b0988-128">Creare e configurare una connessione Da punto a sito per il gateway VPN di Azure, se necessario.</span><span class="sxs-lookup"><span data-stu-id="b0988-128">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span></span>

## <span data-ttu-id="b0988-129"><a name="design"></a>Progettazione</span><span class="sxs-lookup"><span data-stu-id="b0988-129"><a name="design"></a>Design</span></span>
### <span data-ttu-id="b0988-130"><a name="topologies"></a>Topologie di connessione</span><span class="sxs-lookup"><span data-stu-id="b0988-130"><a name="topologies"></a>Connection topologies</span></span>

<span data-ttu-id="b0988-131">Per prima cosa, consultare i diagrammi nell'articolo [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md) .</span><span class="sxs-lookup"><span data-stu-id="b0988-131">Start by looking at the diagrams in the [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span> <span data-ttu-id="b0988-132">Questo articolo contiene i diagrammi di base, i modelli di distribuzione per ogni topologia e gli strumenti di distribuzione che è possibile usare per distribuire la configurazione.</span><span class="sxs-lookup"><span data-stu-id="b0988-132">The article contains basic diagrams, the deployment models for each topology, and the available deployment tools you can use to deploy your configuration.</span></span>

### <span data-ttu-id="b0988-133"><a name="designbasics"></a>Nozioni di base sulla progettazione</span><span class="sxs-lookup"><span data-stu-id="b0988-133"><a name="designbasics"></a>Design basics</span></span>

<span data-ttu-id="b0988-134">Le sezioni seguenti illustrano le nozioni di base del gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="b0988-134">The following sections discuss the VPN gateway basics.</span></span> 

#### <span data-ttu-id="b0988-135"><a name="servicelimits"></a>Limiti dei servizi di rete</span><span class="sxs-lookup"><span data-stu-id="b0988-135"><a name="servicelimits"></a>Networking services limits</span></span>

<span data-ttu-id="b0988-136">Scorrere le tabelle per visualizzare i [limiti dei servizi di rete](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="b0988-136">Scroll through the tables to view [networking services limits](../azure-subscription-service-limits.md#networking-limits).</span></span> <span data-ttu-id="b0988-137">I limiti elencati potrebbero influire sulla progettazione.</span><span class="sxs-lookup"><span data-stu-id="b0988-137">The limits listed may impact your design.</span></span>

#### <span data-ttu-id="b0988-138"><a name="subnets"></a>Informazioni sulle subnet</span><span class="sxs-lookup"><span data-stu-id="b0988-138"><a name="subnets"></a>About subnets</span></span>

<span data-ttu-id="b0988-139">Quando si creano le connessioni, è necessario considerare gli intervalli di indirizzi della subnet.</span><span class="sxs-lookup"><span data-stu-id="b0988-139">When you are creating connections, you must consider your subnet ranges.</span></span> <span data-ttu-id="b0988-140">Gli intervalli di indirizzi della subnet non possono sovrapporsi.</span><span class="sxs-lookup"><span data-stu-id="b0988-140">You cannot have overlapping subnet address ranges.</span></span> <span data-ttu-id="b0988-141">Per subnet sovrapposta si intende una rete virtuale o una posizione locale che contiene lo stesso spazio di indirizzi dell'altra.</span><span class="sxs-lookup"><span data-stu-id="b0988-141">An overlapping subnet is when one virtual network or on-premises location contains the same address space that the other location contains.</span></span> <span data-ttu-id="b0988-142">È necessario che i tecnici di rete che si occupano delle reti locali definiscano un intervallo da usare per la subnet o lo spazio di indirizzi IP di Azure.</span><span class="sxs-lookup"><span data-stu-id="b0988-142">This means that you need your network engineers for your local on-premises networks to carve out a range for you to use for your Azure IP addressing space/subnets.</span></span> <span data-ttu-id="b0988-143">È necessario avere uno spazio di indirizzi che non viene usato nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="b0988-143">You need address space that is not being used on the local on-premises network.</span></span>

<span data-ttu-id="b0988-144">È importante evitare che le subnet si sovrappongano anche quando si utilizzano connessioni Da rete virtuale a rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="b0988-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span></span> <span data-ttu-id="b0988-145">La creazione di una connessione Da rete virtuale a rete virtuale non riuscirà se le subnet si sovrappongono e un indirizzo IP è presente sia nella rete virtuale di origine che in quella di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b0988-145">If your subnets overlap and an IP address exists in both the sending and destination VNets, VNet-to-VNet connections fail.</span></span> <span data-ttu-id="b0988-146">Azure non potrà instradare i dati all'altra rete virtuale, perché l'indirizzo di destinazione fa parte della rete virtuale di origine.</span><span class="sxs-lookup"><span data-stu-id="b0988-146">Azure can't route the data to the other VNet because the destination address is part of the sending VNet.</span></span>

<span data-ttu-id="b0988-147">I gateway VPN richiedono una subnet specifica chiamata subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="b0988-147">VPN Gateways require a specific subnet called a gateway subnet.</span></span> <span data-ttu-id="b0988-148">Per poter funzionare correttamente, tutte le subnet del gateway devono essere denominate GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="b0988-148">All gateway subnets must be named GatewaySubnet to work properly.</span></span> <span data-ttu-id="b0988-149">Assicurarsi di non assegnare alla subnet gateway un nome diverso e non distribuire VM o altri elementi alla subnet gateway.</span><span class="sxs-lookup"><span data-stu-id="b0988-149">Be sure not to name your gateway subnet a different name, and don't deploy VMs or anything else to the gateway subnet.</span></span> <span data-ttu-id="b0988-150">Vedere [Subnet del gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span><span class="sxs-lookup"><span data-stu-id="b0988-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span></span>

#### <span data-ttu-id="b0988-151"><a name="local"></a>Informazioni sui gateway di rete locali</span><span class="sxs-lookup"><span data-stu-id="b0988-151"><a name="local"></a>About local network gateways</span></span>

<span data-ttu-id="b0988-152">Il gateway di rete locale in genere fa riferimento al percorso locale.</span><span class="sxs-lookup"><span data-stu-id="b0988-152">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="b0988-153">Nel modello di distribuzione classica il gateway di rete locale è definito come sito di rete locale.</span><span class="sxs-lookup"><span data-stu-id="b0988-153">In the classic deployment model, the local network gateway is referred to as a Local Network Site.</span></span> <span data-ttu-id="b0988-154">Quando si configura un gateway di rete locale, si assegna un nome, si specifica l'indirizzo IP pubblico del dispositivo VPN locale e si indicano i prefissi di indirizzo che si trovano nel percorso locale.</span><span class="sxs-lookup"><span data-stu-id="b0988-154">When you configure a local network gateway, you give it a name, specify the public IP address of the on-premises VPN device, and specify the address prefixes that are in the on-premises location.</span></span> <span data-ttu-id="b0988-155">Azure esamina i prefissi di indirizzo di destinazione per il traffico di rete, consulta la configurazione specificata per il gateway di rete locale e indirizza i pacchetti di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="b0988-155">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for the local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="b0988-156">È possibile modificare i prefissi di indirizzo in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="b0988-156">You can modify the address prefixes as needed.</span></span> <span data-ttu-id="b0988-157">Per altre informazioni, vedere [Gateway di rete locali](vpn-gateway-about-vpn-gateway-settings.md#lng).</span><span class="sxs-lookup"><span data-stu-id="b0988-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span></span>

#### <span data-ttu-id="b0988-158"><a name="gwtype"></a>Informazioni sui tipi di gateway</span><span class="sxs-lookup"><span data-stu-id="b0988-158"><a name="gwtype"></a>About gateway types</span></span>

<span data-ttu-id="b0988-159">È importante selezione il tipo di gateway corretto per la topologia in uso.</span><span class="sxs-lookup"><span data-stu-id="b0988-159">Selecting the correct gateway type for your topology is critical.</span></span> <span data-ttu-id="b0988-160">Se si seleziona il tipo errato, il gateway non funzionerà correttamente.</span><span class="sxs-lookup"><span data-stu-id="b0988-160">If you select the wrong type, your gateway won't work properly.</span></span> <span data-ttu-id="b0988-161">Il tipo di gateway specifica il modo in cui il gateway stesso si connette ed è un'impostazione di configurazione necessaria per il modello di distribuzione di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b0988-161">The gateway type specifies how the gateway itself connects and is a required configuration setting for the Resource Manager deployment model.</span></span>

<span data-ttu-id="b0988-162">Ecco i tipi di gateway VPN:</span><span class="sxs-lookup"><span data-stu-id="b0988-162">The gateway types are:</span></span>

* <span data-ttu-id="b0988-163">VPN</span><span class="sxs-lookup"><span data-stu-id="b0988-163">Vpn</span></span>
* <span data-ttu-id="b0988-164">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="b0988-164">ExpressRoute</span></span>

#### <span data-ttu-id="b0988-165"><a name="connectiontype"></a>Informazioni sui tipi di connessione</span><span class="sxs-lookup"><span data-stu-id="b0988-165"><a name="connectiontype"></a>About connection types</span></span>

<span data-ttu-id="b0988-166">Ogni configurazione richiede un tipo di connessione specifico.</span><span class="sxs-lookup"><span data-stu-id="b0988-166">Each configuration requires a specific connection type.</span></span> <span data-ttu-id="b0988-167">Ecco i tipi di connessione:</span><span class="sxs-lookup"><span data-stu-id="b0988-167">The connection types are:</span></span>

* <span data-ttu-id="b0988-168">IPsec</span><span class="sxs-lookup"><span data-stu-id="b0988-168">IPsec</span></span>
* <span data-ttu-id="b0988-169">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="b0988-169">Vnet2Vnet</span></span>
* <span data-ttu-id="b0988-170">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="b0988-170">ExpressRoute</span></span>
* <span data-ttu-id="b0988-171">VPNClient</span><span class="sxs-lookup"><span data-stu-id="b0988-171">VPNClient</span></span>

#### <span data-ttu-id="b0988-172"><a name="vpntype"></a>Informazioni sui tipi di VPN</span><span class="sxs-lookup"><span data-stu-id="b0988-172"><a name="vpntype"></a>About VPN types</span></span>

<span data-ttu-id="b0988-173">Ogni configurazione richiede un tipo di VPN specifico.</span><span class="sxs-lookup"><span data-stu-id="b0988-173">Each configuration requires a specific VPN type.</span></span> <span data-ttu-id="b0988-174">Se si combinano due configurazioni, ad esempio creando una connessione da sito a sito e una connessione da punto a sito alla stessa rete virtuale, è necessario usare un tipo di VPN che soddisfi i requisiti di entrambe le connessioni.</span><span class="sxs-lookup"><span data-stu-id="b0988-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection to the same VNet, you must use a VPN type that satisfies both connection requirements.</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="b0988-175">Le tabelle seguenti mostrano il tipo di VPN e il relativo mapping a ogni configurazione di connessione.</span><span class="sxs-lookup"><span data-stu-id="b0988-175">The following tables show the VPN type as it maps to each connection configuration.</span></span> <span data-ttu-id="b0988-176">Assicurarsi che il tipo di VPN per il gateway corrisponda alla configurazione che si vuole creare.</span><span class="sxs-lookup"><span data-stu-id="b0988-176">Make sure the VPN type for your gateway matches the configuration that you want to create.</span></span> 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <span data-ttu-id="b0988-177"><a name="devices"></a>Dispositivi VPN per connessioni da sito a sito</span><span class="sxs-lookup"><span data-stu-id="b0988-177"><a name="devices"></a>VPN devices for Site-to-Site connections</span></span>

<span data-ttu-id="b0988-178">Per configurare una connessione da sito a sito, indipendentemente dal modello di distribuzione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b0988-178">To configure a Site-to-Site connection, regardless of deployment model, you need the following items:</span></span>

* <span data-ttu-id="b0988-179">Un dispositivo VPN compatibile con i gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="b0988-179">A VPN device that is compatible with Azure VPN gateways</span></span>
* <span data-ttu-id="b0988-180">Un indirizzo IP IPv4 pubblico che non si trovi dietro un NAT</span><span class="sxs-lookup"><span data-stu-id="b0988-180">A public-facing IPv4 IP address that is not behind a NAT</span></span>

<span data-ttu-id="b0988-181">È necessario avere esperienza nella configurazione del dispositivo VPN oppure chiedere a qualcuno di farlo al proprio posto.</span><span class="sxs-lookup"><span data-stu-id="b0988-181">You need to have experience configuring your VPN device, or have someone that can configure the device for you.</span></span>

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <span data-ttu-id="b0988-182"><a name="forcedtunnel"></a>Prendere in considerazione il routing con tunneling forzato</span><span class="sxs-lookup"><span data-stu-id="b0988-182"><a name="forcedtunnel"></a>Consider forced tunnel routing</span></span>

<span data-ttu-id="b0988-183">Per la maggior parte delle configurazioni è possibile impostare il tunneling forzato.</span><span class="sxs-lookup"><span data-stu-id="b0988-183">For most configurations, you can configure forced tunneling.</span></span> <span data-ttu-id="b0988-184">Il tunneling forzato consente di reindirizzare o "forzare" tutto il traffico associato a Internet verso la posizione locale tramite un tunnel VPN da sito a sito per l'ispezione e il controllo.</span><span class="sxs-lookup"><span data-stu-id="b0988-184">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="b0988-185">Si tratta di un requisito di sicurezza critico per la maggior parte dei criteri IT aziendali.</span><span class="sxs-lookup"><span data-stu-id="b0988-185">This is a critical security requirement for most enterprise IT policies.</span></span> 

<span data-ttu-id="b0988-186">Senza il tunneling forzato, il traffico associato a Internet dalle macchine virtuali in Azure raggiungerà direttamente Internet attraversando sempre l'infrastruttura di rete di Azure, senza l'opzione che consente di ispezionare o controllare il traffico.</span><span class="sxs-lookup"><span data-stu-id="b0988-186">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="b0988-187">L'accesso a Internet non autorizzato potrebbe provocare la divulgazione di informazioni o altri tipi di violazioni della sicurezza.</span><span class="sxs-lookup"><span data-stu-id="b0988-187">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span></span>

<span data-ttu-id="b0988-188">È possibile configurare una connessione di tunneling forzato in entrambi i modelli di distribuzione e tramite strumenti diversi.</span><span class="sxs-lookup"><span data-stu-id="b0988-188">A forced tunneling connection can be configured in both deployment models and by using different tools.</span></span> <span data-ttu-id="b0988-189">Per altre informazioni, vedere [Configurare il tunneling forzato](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="b0988-189">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>

<span data-ttu-id="b0988-190">**Diagramma tunneling forzato**</span><span class="sxs-lookup"><span data-stu-id="b0988-190">**Forced tunneling diagram**</span></span>

![Diagramma di tunneling forzato di Gateway VPN di Azure](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a><span data-ttu-id="b0988-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b0988-192">Next steps</span></span>

<span data-ttu-id="b0988-193">Per altre informazioni che aiutano a semplificare la progettazione, vedere gli articoli [Domande frequenti sul gateway VPN](vpn-gateway-vpn-faq.md) e [Informazioni sui gateway VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="b0988-193">See the [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information to help you with your design.</span></span>

<span data-ttu-id="b0988-194">Per altre informazioni sulle impostazioni specifiche del gateway, vedere [Informazioni sulle impostazioni del gateway VPN](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="b0988-194">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>