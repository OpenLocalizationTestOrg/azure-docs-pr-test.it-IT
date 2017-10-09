<span data-ttu-id="3691e-101">domande frequenti per rete virtuale a Hello applica connessioni Gateway tooVPN.</span><span class="sxs-lookup"><span data-stu-id="3691e-101">hello VNet-to-VNet FAQ applies tooVPN Gateway connections.</span></span> <span data-ttu-id="3691e-102">Per informazioni sul peering reti virtuali, vedere [Peering di rete virtuale](../articles/virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3691e-102">If you are looking for VNet Peering, see [Virtual Network Peering](../articles/virtual-network/virtual-network-peering-overview.md)</span></span>

### <a name="does-azure-charge-for-traffic-between-vnets"></a><span data-ttu-id="3691e-103">È previsto un addebito per il traffico tra le reti virtuali?</span><span class="sxs-lookup"><span data-stu-id="3691e-103">Does Azure charge for traffic between VNets?</span></span>

<span data-ttu-id="3691e-104">Traffico di rete virtuale all'interno di hello stessa area geografica è gratuita per entrambe le direzioni quando si utilizza una connessione gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="3691e-104">VNet-to-VNet traffic within hello same region is free for both directions when using a VPN gateway connection.</span></span> <span data-ttu-id="3691e-105">Tra l'area di rete virtuale a uscita traffico viene addebitato con hello velocità di trasferimento dati in uscita tra reti virtuali in base alle aree di origine hello.</span><span class="sxs-lookup"><span data-stu-id="3691e-105">Cross region VNet-to-VNet egress traffic is charged with hello outbound inter-VNet data transfer rates based on hello source regions.</span></span> <span data-ttu-id="3691e-106">Fare riferimento toohello [Gateway VPN di pagina dei prezzi](https://azure.microsoft.com/pricing/details/vpn-gateway/) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="3691e-106">Refer toohello [VPN Gateway pricing page](https://azure.microsoft.com/pricing/details/vpn-gateway/) for details.</span></span> <span data-ttu-id="3691e-107">Se ci si connette le reti virtuali utilizzando Peering reti virtuali, anziché Gateway VPN, vedere hello [pagina dei prezzi di rete virtuale](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="3691e-107">If you are connecting your VNets using VNet Peering, rather than VPN Gateway, see hello [Virtual Network pricing page](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>

### <a name="does-vnet-to-vnet-traffic-travel-across-hello-internet"></a><span data-ttu-id="3691e-108">Il traffico di rete virtuale a attraversare Internet hello?</span><span class="sxs-lookup"><span data-stu-id="3691e-108">Does VNet-to-VNet traffic travel across hello Internet?</span></span>

<span data-ttu-id="3691e-109">No.</span><span class="sxs-lookup"><span data-stu-id="3691e-109">No.</span></span> <span data-ttu-id="3691e-110">Il traffico di rete virtuale a viaggia attraverso hello backbone di Microsoft Azure, non hello Internet.</span><span class="sxs-lookup"><span data-stu-id="3691e-110">VNet-to-VNet traffic travels across hello Microsoft Azure backbone, not hello Internet.</span></span>

### <a name="is-vnet-to-vnet-traffic-secure"></a><span data-ttu-id="3691e-111">Il traffico tra reti virtuali è sicuro?</span><span class="sxs-lookup"><span data-stu-id="3691e-111">Is VNet-to-VNet traffic secure?</span></span>

<span data-ttu-id="3691e-112">Sì, è protetto mediante la crittografia IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="3691e-112">Yes, it is protected by IPsec/IKE encryption.</span></span>

### <a name="do-i-need-a-vpn-device-tooconnect-vnets-together"></a><span data-ttu-id="3691e-113">È necessario un tooconnect dispositivo VPN reti virtuali insieme?</span><span class="sxs-lookup"><span data-stu-id="3691e-113">Do I need a VPN device tooconnect VNets together?</span></span>

<span data-ttu-id="3691e-114">No.</span><span class="sxs-lookup"><span data-stu-id="3691e-114">No.</span></span> <span data-ttu-id="3691e-115">Per il collegamento di più reti virtuali di Azure non è necessario un dispositivo VPN, a meno che non sia necessaria la connettività cross-premise.</span><span class="sxs-lookup"><span data-stu-id="3691e-115">Connecting multiple Azure virtual networks together doesn't require a VPN device unless cross-premises connectivity is required.</span></span>

### <a name="do-my-vnets-need-toobe-in-hello-same-region"></a><span data-ttu-id="3691e-116">La reti virtuali richiedono toobe in hello stessa regione?</span><span class="sxs-lookup"><span data-stu-id="3691e-116">Do my VNets need toobe in hello same region?</span></span>

<span data-ttu-id="3691e-117">No.</span><span class="sxs-lookup"><span data-stu-id="3691e-117">No.</span></span> <span data-ttu-id="3691e-118">reti virtuali di Hello possono trovarsi in hello uguali o diverse aree di Azure (posizioni).</span><span class="sxs-lookup"><span data-stu-id="3691e-118">hello virtual networks can be in hello same or different Azure regions (locations).</span></span>

### <a name="if-hello-vnets-are-not-in-hello-same-subscription-do-hello-subscriptions-need-toobe-associated-with-hello-same-ad-tenant"></a><span data-ttu-id="3691e-119">Se hello reti virtuali non è nello stesso hello necessario di sottoscrizione, le sottoscrizioni di hello toobe associato hello AD stesso tenant?</span><span class="sxs-lookup"><span data-stu-id="3691e-119">If hello VNets are not in hello same subscription, do hello subscriptions need toobe associated with hello same AD tenant?</span></span>

<span data-ttu-id="3691e-120">No.</span><span class="sxs-lookup"><span data-stu-id="3691e-120">No.</span></span>

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a><span data-ttu-id="3691e-121">È possibile usare la connessione da rete virtuale a rete virtuale insieme alle connessioni multisito?</span><span class="sxs-lookup"><span data-stu-id="3691e-121">Can I use VNet-to-VNet along with multi-site connections?</span></span>

<span data-ttu-id="3691e-122">Sì.</span><span class="sxs-lookup"><span data-stu-id="3691e-122">Yes.</span></span> <span data-ttu-id="3691e-123">La connettività di rete virtuale può essere usata contemporaneamente con VPN multisito,</span><span class="sxs-lookup"><span data-stu-id="3691e-123">Virtual network connectivity can be used simultaneously with multi-site VPNs.</span></span>

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a><span data-ttu-id="3691e-124">A quanti siti locali e reti virtuali può connettersi una rete virtuale?</span><span class="sxs-lookup"><span data-stu-id="3691e-124">How many on-premises sites and virtual networks can one virtual network connect to?</span></span>

<span data-ttu-id="3691e-125">Vedere la tabella [Requisiti del gateway](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="3691e-125">See [Gateway requirements](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements) table.</span></span>

### <a name="can-i-use-vnet-to-vnet-tooconnect-vms-or-cloud-services-outside-of-a-vnet"></a><span data-ttu-id="3691e-126">È possibile utilizzare tooconnect per rete virtuale a macchine virtuali o servizi all'esterno di una rete virtuale cloud?</span><span class="sxs-lookup"><span data-stu-id="3691e-126">Can I use VNet-to-VNet tooconnect VMs or cloud services outside of a VNet?</span></span>

<span data-ttu-id="3691e-127">No.</span><span class="sxs-lookup"><span data-stu-id="3691e-127">No.</span></span> <span data-ttu-id="3691e-128">La connettività da VNet a VNet supporta la connessione di reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="3691e-128">VNet-to-VNet supports connecting virtual networks.</span></span> <span data-ttu-id="3691e-129">Non supporta la connessione di macchine virtuali o servizi cloud non inclusi in una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3691e-129">It does not support connecting virtual machines or cloud services that are not in a virtual network.</span></span>

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a><span data-ttu-id="3691e-130">È possibile estendere un servizio cloud o un endpoint del servizio di bilanciamento del carico in più reti virtuali?</span><span class="sxs-lookup"><span data-stu-id="3691e-130">Can a cloud service or a load balancing endpoint span VNets?</span></span>

<span data-ttu-id="3691e-131">No.</span><span class="sxs-lookup"><span data-stu-id="3691e-131">No.</span></span> <span data-ttu-id="3691e-132">Un servizio cloud o un endpoint di bilanciamento del carico non può estendersi tra reti virtuali, anche se sono connesse tra loro.</span><span class="sxs-lookup"><span data-stu-id="3691e-132">A cloud service or a load balancing endpoint can't span across virtual networks, even if they are connected together.</span></span>

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a><span data-ttu-id="3691e-133">È possibile usare una VPN di tipo PolicyBased per connessioni da rete virtuale a rete virtuale o multisito?</span><span class="sxs-lookup"><span data-stu-id="3691e-133">Can I used a PolicyBased VPN type for VNet-to-VNet or Multi-Site connections?</span></span>

<span data-ttu-id="3691e-134">No.</span><span class="sxs-lookup"><span data-stu-id="3691e-134">No.</span></span> <span data-ttu-id="3691e-135">La connettività tra reti virtuali e multisito richiede la presenza di gateway VPN con tipi VPN RouteBased (in precedenza denominato routing dinamico).</span><span class="sxs-lookup"><span data-stu-id="3691e-135">VNet-to-VNet and Multi-Site connections require Azure VPN gateways with RouteBased (previously called Dynamic Routing) VPN types.</span></span>

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-tooanother-vnet-with-a-policybased-vpn-type"></a><span data-ttu-id="3691e-136">È possibile connettere una rete virtuale con un tooanother tipo VPN tipo RouteBased rete virtuale con un tipo di VPN PolicyBased?</span><span class="sxs-lookup"><span data-stu-id="3691e-136">Can I connect a VNet with a RouteBased VPN Type tooanother VNet with a PolicyBased VPN type?</span></span>

<span data-ttu-id="3691e-137">No, entrambe le reti virtuali DEVONO usare VPN basate su route (denominate in precedenza routing dinamico).</span><span class="sxs-lookup"><span data-stu-id="3691e-137">No, both virtual networks MUST be using route-based (previously called Dynamic Routing) VPNs.</span></span>

### <a name="do-vpn-tunnels-share-bandwidth"></a><span data-ttu-id="3691e-138">I tunnel VPN condividono la larghezza di banda?</span><span class="sxs-lookup"><span data-stu-id="3691e-138">Do VPN tunnels share bandwidth?</span></span>

<span data-ttu-id="3691e-139">Sì.</span><span class="sxs-lookup"><span data-stu-id="3691e-139">Yes.</span></span> <span data-ttu-id="3691e-140">Tutti i tunnel VPN della rete virtuale hello condividono larghezza di banda disponibile hello nel gateway VPN di Azure hello e hello stesso VPN gateway tempi di attività contratto di servizio in Azure.</span><span class="sxs-lookup"><span data-stu-id="3691e-140">All VPN tunnels of hello virtual network share hello available bandwidth on hello Azure VPN gateway and hello same VPN gateway uptime SLA in Azure.</span></span>

### <a name="are-redundant-tunnels-supported"></a><span data-ttu-id="3691e-141">Sono supportati i tunnel ridondanti?</span><span class="sxs-lookup"><span data-stu-id="3691e-141">Are redundant tunnels supported?</span></span>

<span data-ttu-id="3691e-142">I tunnel ridondanti tra una coppia di reti virtuali sono supportati quando un gateway di rete virtuale è configurato come attivo/attivo.</span><span class="sxs-lookup"><span data-stu-id="3691e-142">Redundant tunnels between a pair of virtual networks are supported when one virtual network gateway is configured as active-active.</span></span>

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a><span data-ttu-id="3691e-143">È consentita la sovrapposizione di spazi di indirizzi per configurazioni da rete virtuale a rete virtuale?</span><span class="sxs-lookup"><span data-stu-id="3691e-143">Can I have overlapping address spaces for VNet-to-VNet configurations?</span></span>

<span data-ttu-id="3691e-144">No.</span><span class="sxs-lookup"><span data-stu-id="3691e-144">No.</span></span> <span data-ttu-id="3691e-145">Gli intervalli di indirizzi IP non possono sovrapporsi.</span><span class="sxs-lookup"><span data-stu-id="3691e-145">You can't have overlapping IP address ranges.</span></span>

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a><span data-ttu-id="3691e-146">Possono esistere spazi di indirizzi sovrapposti tra le reti virtuali connesse e i siti locali?</span><span class="sxs-lookup"><span data-stu-id="3691e-146">Can there be overlapping address spaces among connected virtual networks and on-premises local sites?</span></span>

<span data-ttu-id="3691e-147">No.</span><span class="sxs-lookup"><span data-stu-id="3691e-147">No.</span></span> <span data-ttu-id="3691e-148">Gli intervalli di indirizzi IP non possono sovrapporsi.</span><span class="sxs-lookup"><span data-stu-id="3691e-148">You can't have overlapping IP address ranges.</span></span>



