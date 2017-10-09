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
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a><span data-ttu-id="e3f92-103">Pianificazione e progettazione per il gateway VPN</span><span class="sxs-lookup"><span data-stu-id="e3f92-103">Planning and design for VPN Gateway</span></span>

<span data-ttu-id="e3f92-104">Le operazioni di pianificazione e progettazione di connessioni cross-premise e da rete virtuale a rete virtuale possono essere molto semplici o piuttosto complicate, a seconda delle esigenze di rete.</span><span class="sxs-lookup"><span data-stu-id="e3f92-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span></span> <span data-ttu-id="e3f92-105">Questo articolo illustra in dettaglio alcune considerazioni di base sulla progettazione e sulla pianificazione.</span><span class="sxs-lookup"><span data-stu-id="e3f92-105">This article walks you through basic planning and design considerations.</span></span>

## <span data-ttu-id="e3f92-106"><a name="planning"></a>Pianificazione</span><span class="sxs-lookup"><span data-stu-id="e3f92-106"><a name="planning"></a>Planning</span></span>

### <span data-ttu-id="e3f92-107"><a name="compare"></a>Opzioni di connettività di più sedi locali</span><span class="sxs-lookup"><span data-stu-id="e3f92-107"><a name="compare"></a>Cross-premises connectivity options</span></span>

<span data-ttu-id="e3f92-108">Se si desidera tooconnect locale siti in modo sicuro la rete virtuale tooa, è pertanto toodo di tre modi diversi: da sito a sito, Point-to-Site ed ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e3f92-108">If you want tooconnect your on-premises sites securely tooa virtual network, you have three different ways toodo so: Site-to-Site, Point-to-Site, and ExpressRoute.</span></span> <span data-ttu-id="e3f92-109">Confrontare le connessioni cross-premise diversi hello disponibili.</span><span class="sxs-lookup"><span data-stu-id="e3f92-109">Compare hello different cross-premises connections that are available.</span></span> <span data-ttu-id="e3f92-110">opzione che tu scelga determina Hello può dipendere da diverse considerazioni, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="e3f92-110">hello option you choose can depend on various considerations, such as:</span></span>

* <span data-ttu-id="e3f92-111">Che tipo di velocità effettiva richiede la soluzione?</span><span class="sxs-lookup"><span data-stu-id="e3f92-111">What kind of throughput does your solution require?</span></span>
* <span data-ttu-id="e3f92-112">Si desidera toocommunicate su hello rete Internet pubblica tramite VPN sicura o tramite una connessione privata?</span><span class="sxs-lookup"><span data-stu-id="e3f92-112">Do you want toocommunicate over hello public Internet via secure VPN, or over a private connection?</span></span>
* <span data-ttu-id="e3f92-113">Si dispone di un toouse disponibili di indirizzi IP pubblici?</span><span class="sxs-lookup"><span data-stu-id="e3f92-113">Do you have a public IP address available toouse?</span></span>
* <span data-ttu-id="e3f92-114">Se si sta pianificando toouse un dispositivo VPN?</span><span class="sxs-lookup"><span data-stu-id="e3f92-114">Are you planning toouse a VPN device?</span></span> <span data-ttu-id="e3f92-115">In tal caso, è compatibile?</span><span class="sxs-lookup"><span data-stu-id="e3f92-115">If so, is it compatible?</span></span>
* <span data-ttu-id="e3f92-116">Si connette un numero limitato di computer o si desidera una connessione permanente per il sito?</span><span class="sxs-lookup"><span data-stu-id="e3f92-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span></span>
* <span data-ttu-id="e3f92-117">Il tipo di gateway VPN è necessario per la soluzione hello desiderato toocreate?</span><span class="sxs-lookup"><span data-stu-id="e3f92-117">What type of VPN gateway is required for hello solution you want toocreate?</span></span>
* <span data-ttu-id="e3f92-118">Quale SKU del gateway è opportuno usare?</span><span class="sxs-lookup"><span data-stu-id="e3f92-118">Which gateway SKU should you use?</span></span>

### <span data-ttu-id="e3f92-119"><a name="planningtable"></a>Tabella di pianificazione</span><span class="sxs-lookup"><span data-stu-id="e3f92-119"><a name="planningtable"></a>Planning table</span></span>

<span data-ttu-id="e3f92-120">Hello nella tabella seguente consente di decidere hello connettività migliore per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="e3f92-120">hello following table can help you decide hello best connectivity option for your solution.</span></span>

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <span data-ttu-id="e3f92-121"><a name="gwsku"></a>SKU del gateway</span><span class="sxs-lookup"><span data-stu-id="e3f92-121"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <span data-ttu-id="e3f92-122"><a name="wf"></a>Flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="e3f92-122"><a name="wf"></a>Workflow</span></span>

<span data-ttu-id="e3f92-123">Hello seguito sono riportati i hello comune del flusso di lavoro per la connettività di cloud:</span><span class="sxs-lookup"><span data-stu-id="e3f92-123">hello following list outlines hello common workflow for cloud connectivity:</span></span>

1. <span data-ttu-id="e3f92-124">Progettazione e pianificare che il connettività della topologia ed elenco hello gli spazi di indirizzi per tutte le reti si desidera tooconnect.</span><span class="sxs-lookup"><span data-stu-id="e3f92-124">Design and plan your connectivity topology and list hello address spaces for all networks you want tooconnect.</span></span>
2. <span data-ttu-id="e3f92-125">Creare una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="e3f92-125">Create an Azure virtual network.</span></span> 
3. <span data-ttu-id="e3f92-126">Creare un gateway VPN per rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="e3f92-126">Create a VPN gateway for hello virtual network.</span></span>
4. <span data-ttu-id="e3f92-127">Creare e configurare le reti locali tooon di connessioni o altre reti virtuali (se necessario).</span><span class="sxs-lookup"><span data-stu-id="e3f92-127">Create and configure connections tooon-premises networks or other virtual networks (as needed).</span></span>
5. <span data-ttu-id="e3f92-128">Creare e configurare una connessione Da punto a sito per il gateway VPN di Azure, se necessario.</span><span class="sxs-lookup"><span data-stu-id="e3f92-128">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span></span>

## <span data-ttu-id="e3f92-129"><a name="design"></a>Progettazione</span><span class="sxs-lookup"><span data-stu-id="e3f92-129"><a name="design"></a>Design</span></span>
### <span data-ttu-id="e3f92-130"><a name="topologies"></a>Topologie di connessione</span><span class="sxs-lookup"><span data-stu-id="e3f92-130"><a name="topologies"></a>Connection topologies</span></span>

<span data-ttu-id="e3f92-131">Iniziare esaminando i diagrammi di hello in hello [sul Gateway VPN](vpn-gateway-about-vpngateways.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="e3f92-131">Start by looking at hello diagrams in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span> <span data-ttu-id="e3f92-132">articolo Hello contiene diagrammi di base, i modelli di distribuzione hello per ogni topologia e strumenti di distribuzione disponibili hello è possibile utilizzare la configurazione toodeploy.</span><span class="sxs-lookup"><span data-stu-id="e3f92-132">hello article contains basic diagrams, hello deployment models for each topology, and hello available deployment tools you can use toodeploy your configuration.</span></span>

### <span data-ttu-id="e3f92-133"><a name="designbasics"></a>Nozioni di base sulla progettazione</span><span class="sxs-lookup"><span data-stu-id="e3f92-133"><a name="designbasics"></a>Design basics</span></span>

<span data-ttu-id="e3f92-134">Hello le sezioni seguenti illustrano nozioni di base di hello VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="e3f92-134">hello following sections discuss hello VPN gateway basics.</span></span> 

#### <span data-ttu-id="e3f92-135"><a name="servicelimits"></a>Limiti dei servizi di rete</span><span class="sxs-lookup"><span data-stu-id="e3f92-135"><a name="servicelimits"></a>Networking services limits</span></span>

<span data-ttu-id="e3f92-136">Scorrere hello tabelle tooview [networking servizi limiti](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="e3f92-136">Scroll through hello tables tooview [networking services limits](../azure-subscription-service-limits.md#networking-limits).</span></span> <span data-ttu-id="e3f92-137">limiti di Hello elencati potrebbero compromettere la progettazione.</span><span class="sxs-lookup"><span data-stu-id="e3f92-137">hello limits listed may impact your design.</span></span>

#### <span data-ttu-id="e3f92-138"><a name="subnets"></a>Informazioni sulle subnet</span><span class="sxs-lookup"><span data-stu-id="e3f92-138"><a name="subnets"></a>About subnets</span></span>

<span data-ttu-id="e3f92-139">Quando si creano le connessioni, è necessario considerare gli intervalli di indirizzi della subnet.</span><span class="sxs-lookup"><span data-stu-id="e3f92-139">When you are creating connections, you must consider your subnet ranges.</span></span> <span data-ttu-id="e3f92-140">Gli intervalli di indirizzi della subnet non possono sovrapporsi.</span><span class="sxs-lookup"><span data-stu-id="e3f92-140">You cannot have overlapping subnet address ranges.</span></span> <span data-ttu-id="e3f92-141">Una subnet sovrapposta è quando un percorso locale o di rete virtuale contiene hello contiene stesso spazio di indirizzi che hello altra posizione.</span><span class="sxs-lookup"><span data-stu-id="e3f92-141">An overlapping subnet is when one virtual network or on-premises location contains hello same address space that hello other location contains.</span></span> <span data-ttu-id="e3f92-142">Questo significa che è necessario ai tecnici di rete per il toocarve reti locale out toouse è un intervallo per l'IP di Azure/subnet spazio di indirizzamento.</span><span class="sxs-lookup"><span data-stu-id="e3f92-142">This means that you need your network engineers for your local on-premises networks toocarve out a range for you toouse for your Azure IP addressing space/subnets.</span></span> <span data-ttu-id="e3f92-143">È necessario spazio di indirizzi che non è in uso nella rete locale hello.</span><span class="sxs-lookup"><span data-stu-id="e3f92-143">You need address space that is not being used on hello local on-premises network.</span></span>

<span data-ttu-id="e3f92-144">È importante evitare che le subnet si sovrappongano anche quando si utilizzano connessioni Da rete virtuale a rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e3f92-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span></span> <span data-ttu-id="e3f92-145">Se si sovrappongono le subnet e un indirizzo IP presente in hello l'invio e la destinazione di reti virtuali, le connessioni di rete virtuale a non riuscire.</span><span class="sxs-lookup"><span data-stu-id="e3f92-145">If your subnets overlap and an IP address exists in both hello sending and destination VNets, VNet-to-VNet connections fail.</span></span> <span data-ttu-id="e3f92-146">Azure non è possibile indirizzare hello dati toohello altra rete virtuale perché l'indirizzo di destinazione hello fa parte di hello l'invio di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e3f92-146">Azure can't route hello data toohello other VNet because hello destination address is part of hello sending VNet.</span></span>

<span data-ttu-id="e3f92-147">I gateway VPN richiedono una subnet specifica chiamata subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="e3f92-147">VPN Gateways require a specific subnet called a gateway subnet.</span></span> <span data-ttu-id="e3f92-148">Tutte le subnet gateway devono essere denominate GatewaySubnet toowork correttamente.</span><span class="sxs-lookup"><span data-stu-id="e3f92-148">All gateway subnets must be named GatewaySubnet toowork properly.</span></span> <span data-ttu-id="e3f92-149">Verificare che non tooname la subnet gateway con un altro nome e non distribuire macchine virtuali o qualsiasi altra subnet del gateway toohello.</span><span class="sxs-lookup"><span data-stu-id="e3f92-149">Be sure not tooname your gateway subnet a different name, and don't deploy VMs or anything else toohello gateway subnet.</span></span> <span data-ttu-id="e3f92-150">Vedere [Subnet del gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span><span class="sxs-lookup"><span data-stu-id="e3f92-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span></span>

#### <span data-ttu-id="e3f92-151"><a name="local"></a>Informazioni sui gateway di rete locali</span><span class="sxs-lookup"><span data-stu-id="e3f92-151"><a name="local"></a>About local network gateways</span></span>

<span data-ttu-id="e3f92-152">gateway di rete locale Hello si riferisce solitamente percorso locale tooyour.</span><span class="sxs-lookup"><span data-stu-id="e3f92-152">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="e3f92-153">Nel modello di distribuzione classica hello, gateway di rete locale hello è tooas di cui si fa riferimento un sito di rete locale.</span><span class="sxs-lookup"><span data-stu-id="e3f92-153">In hello classic deployment model, hello local network gateway is referred tooas a Local Network Site.</span></span> <span data-ttu-id="e3f92-154">Quando si configura un gateway di rete locale, si assegnargli un nome, specifica l'indirizzo IP pubblico hello del dispositivo VPN locale di hello e specificare i prefissi di indirizzo hello presenti nel percorso locale hello.</span><span class="sxs-lookup"><span data-stu-id="e3f92-154">When you configure a local network gateway, you give it a name, specify hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are in hello on-premises location.</span></span> <span data-ttu-id="e3f92-155">Azure esamina i prefissi di indirizzo di destinazione hello il traffico di rete, consulta configurazione hello che è stato specificato per il gateway di rete locale hello e instrada i pacchetti di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="e3f92-155">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for hello local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="e3f92-156">È possibile modificare i prefissi di indirizzo hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="e3f92-156">You can modify hello address prefixes as needed.</span></span> <span data-ttu-id="e3f92-157">Per altre informazioni, vedere [Gateway di rete locali](vpn-gateway-about-vpn-gateway-settings.md#lng).</span><span class="sxs-lookup"><span data-stu-id="e3f92-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span></span>

#### <span data-ttu-id="e3f92-158"><a name="gwtype"></a>Informazioni sui tipi di gateway</span><span class="sxs-lookup"><span data-stu-id="e3f92-158"><a name="gwtype"></a>About gateway types</span></span>

<span data-ttu-id="e3f92-159">Selezione tipo di gateway corretto hello per la topologia è fondamentale.</span><span class="sxs-lookup"><span data-stu-id="e3f92-159">Selecting hello correct gateway type for your topology is critical.</span></span> <span data-ttu-id="e3f92-160">Se si seleziona un tipo non corretto hello, il gateway non funzionerà correttamente.</span><span class="sxs-lookup"><span data-stu-id="e3f92-160">If you select hello wrong type, your gateway won't work properly.</span></span> <span data-ttu-id="e3f92-161">tipo di gateway Hello specifica la modalità gateway hello stesso si connette e un'impostazione di configurazione necessarie per il modello di distribuzione di gestione risorse hello.</span><span class="sxs-lookup"><span data-stu-id="e3f92-161">hello gateway type specifies how hello gateway itself connects and is a required configuration setting for hello Resource Manager deployment model.</span></span>

<span data-ttu-id="e3f92-162">i tipi di gateway Hello sono:</span><span class="sxs-lookup"><span data-stu-id="e3f92-162">hello gateway types are:</span></span>

* <span data-ttu-id="e3f92-163">VPN</span><span class="sxs-lookup"><span data-stu-id="e3f92-163">Vpn</span></span>
* <span data-ttu-id="e3f92-164">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e3f92-164">ExpressRoute</span></span>

#### <span data-ttu-id="e3f92-165"><a name="connectiontype"></a>Informazioni sui tipi di connessione</span><span class="sxs-lookup"><span data-stu-id="e3f92-165"><a name="connectiontype"></a>About connection types</span></span>

<span data-ttu-id="e3f92-166">Ogni configurazione richiede un tipo di connessione specifico.</span><span class="sxs-lookup"><span data-stu-id="e3f92-166">Each configuration requires a specific connection type.</span></span> <span data-ttu-id="e3f92-167">tipi di connessione Hello sono:</span><span class="sxs-lookup"><span data-stu-id="e3f92-167">hello connection types are:</span></span>

* <span data-ttu-id="e3f92-168">IPsec</span><span class="sxs-lookup"><span data-stu-id="e3f92-168">IPsec</span></span>
* <span data-ttu-id="e3f92-169">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="e3f92-169">Vnet2Vnet</span></span>
* <span data-ttu-id="e3f92-170">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e3f92-170">ExpressRoute</span></span>
* <span data-ttu-id="e3f92-171">VPNClient</span><span class="sxs-lookup"><span data-stu-id="e3f92-171">VPNClient</span></span>

#### <span data-ttu-id="e3f92-172"><a name="vpntype"></a>Informazioni sui tipi di VPN</span><span class="sxs-lookup"><span data-stu-id="e3f92-172"><a name="vpntype"></a>About VPN types</span></span>

<span data-ttu-id="e3f92-173">Ogni configurazione richiede un tipo di VPN specifico.</span><span class="sxs-lookup"><span data-stu-id="e3f92-173">Each configuration requires a specific VPN type.</span></span> <span data-ttu-id="e3f92-174">Se si combinano due configurazioni, ad esempio la creazione di una connessione Site-to-Site e un toohello connessione Point-to-Site stessa rete virtuale, è necessario utilizzare un tipo VPN che soddisfa entrambi i requisiti di connessione.</span><span class="sxs-lookup"><span data-stu-id="e3f92-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection toohello same VNet, you must use a VPN type that satisfies both connection requirements.</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="e3f92-175">Hello tabelle seguenti illustrano il tipo di VPN hello come viene eseguito il mapping tooeach configurazione della connessione.</span><span class="sxs-lookup"><span data-stu-id="e3f92-175">hello following tables show hello VPN type as it maps tooeach connection configuration.</span></span> <span data-ttu-id="e3f92-176">Verificare che hello tipo VPN per la configurazione di hello corrispondenze gateway che si desidera toocreate.</span><span class="sxs-lookup"><span data-stu-id="e3f92-176">Make sure hello VPN type for your gateway matches hello configuration that you want toocreate.</span></span> 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <span data-ttu-id="e3f92-177"><a name="devices"></a>Dispositivi VPN per connessioni da sito a sito</span><span class="sxs-lookup"><span data-stu-id="e3f92-177"><a name="devices"></a>VPN devices for Site-to-Site connections</span></span>

<span data-ttu-id="e3f92-178">connessione di un sito a sito tooconfigure, indipendentemente dal modello di distribuzione, è necessario hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="e3f92-178">tooconfigure a Site-to-Site connection, regardless of deployment model, you need hello following items:</span></span>

* <span data-ttu-id="e3f92-179">Un dispositivo VPN compatibile con i gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="e3f92-179">A VPN device that is compatible with Azure VPN gateways</span></span>
* <span data-ttu-id="e3f92-180">Un indirizzo IP IPv4 pubblico che non si trovi dietro un NAT</span><span class="sxs-lookup"><span data-stu-id="e3f92-180">A public-facing IPv4 IP address that is not behind a NAT</span></span>

<span data-ttu-id="e3f92-181">È necessario toohave esperienza di configurazione del dispositivo VPN oppure è necessario che un utente che possono configurare il dispositivo di hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e3f92-181">You need toohave experience configuring your VPN device, or have someone that can configure hello device for you.</span></span>

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <span data-ttu-id="e3f92-182"><a name="forcedtunnel"></a>Prendere in considerazione il routing con tunneling forzato</span><span class="sxs-lookup"><span data-stu-id="e3f92-182"><a name="forcedtunnel"></a>Consider forced tunnel routing</span></span>

<span data-ttu-id="e3f92-183">Per la maggior parte delle configurazioni è possibile impostare il tunneling forzato.</span><span class="sxs-lookup"><span data-stu-id="e3f92-183">For most configurations, you can configure forced tunneling.</span></span> <span data-ttu-id="e3f92-184">Il tunneling consente di reindirizzare o "forzare" tutto associato a Internet traffico tooyour indietro percorso locale tramite un tunnel VPN da sito a sito per l'ispezione e controllo forzato.</span><span class="sxs-lookup"><span data-stu-id="e3f92-184">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="e3f92-185">Si tratta di un requisito di sicurezza critico per la maggior parte dei criteri IT aziendali.</span><span class="sxs-lookup"><span data-stu-id="e3f92-185">This is a critical security requirement for most enterprise IT policies.</span></span> 

<span data-ttu-id="e3f92-186">Senza il tunneling forzato, il traffico Internet dalle macchine virtuali in Azure passerà sempre dall'infrastruttura di rete di Azure direttamente out toohello Internet, senza tooallow opzione hello è traffico hello tooinspect o audit.</span><span class="sxs-lookup"><span data-stu-id="e3f92-186">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="e3f92-187">Accesso a Internet non autorizzato potrebbe provocare la diffusione di tooinformation o altri tipi di violazioni di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="e3f92-187">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

<span data-ttu-id="e3f92-188">È possibile configurare una connessione di tunneling forzato in entrambi i modelli di distribuzione e tramite strumenti diversi.</span><span class="sxs-lookup"><span data-stu-id="e3f92-188">A forced tunneling connection can be configured in both deployment models and by using different tools.</span></span> <span data-ttu-id="e3f92-189">Per altre informazioni, vedere [Configurare il tunneling forzato](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="e3f92-189">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>

<span data-ttu-id="e3f92-190">**Diagramma tunneling forzato**</span><span class="sxs-lookup"><span data-stu-id="e3f92-190">**Forced tunneling diagram**</span></span>

![Diagramma di tunneling forzato di Gateway VPN di Azure](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a><span data-ttu-id="e3f92-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e3f92-192">Next steps</span></span>

<span data-ttu-id="e3f92-193">Vedere hello [domande frequenti su Gateway VPN](vpn-gateway-vpn-faq.md) e [sul Gateway VPN](vpn-gateway-about-vpngateways.md) sugli articoli per ulteriori informazioni toohelp si con la progettazione.</span><span class="sxs-lookup"><span data-stu-id="e3f92-193">See hello [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information toohelp you with your design.</span></span>

<span data-ttu-id="e3f92-194">Per altre informazioni sulle impostazioni specifiche del gateway, vedere [Informazioni sulle impostazioni del gateway VPN](vpn-gateway-about-vpn-gateway-settings.md).</span><span class="sxs-lookup"><span data-stu-id="e3f92-194">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>