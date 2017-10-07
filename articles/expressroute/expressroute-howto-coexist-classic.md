---
title: 'Configurare connessioni coesistenti ExpressRoute e VPN da sito a sito - Versione classica: Azure| Microsoft Docs'
description: "In questo articolo illustra la configurazione di una connessione VPN da sito a sito che può coesistere per il modello di distribuzione classica hello ed ExpressRoute."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="37a3e-103">Configurare connessioni coesistenti ExpressRoute e da sito a sito (versione classica)</span><span class="sxs-lookup"><span data-stu-id="37a3e-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="37a3e-104">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="37a3e-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="37a3e-105">PowerShell - Classico</span><span class="sxs-lookup"><span data-stu-id="37a3e-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="37a3e-106">Con possibilità di hello tooconfigure VPN Site-to-Site ed ExpressRoute presenta diversi vantaggi.</span><span class="sxs-lookup"><span data-stu-id="37a3e-106">Having hello ability tooconfigure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="37a3e-107">È possibile configurare la VPN da sito a sito come un percorso sicuro failover per ExressRoute o usare VPN da sito a sito tooconnect toosites che non sono connessi tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="37a3e-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs tooconnect toosites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="37a3e-108">Verranno illustrate hello passaggi tooconfigure entrambi gli scenari in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="37a3e-108">We will cover hello steps tooconfigure both scenarios in this article.</span></span> <span data-ttu-id="37a3e-109">In questo articolo si applica il modello di distribuzione classica toohello.</span><span class="sxs-lookup"><span data-stu-id="37a3e-109">This article applies toohello classic deployment model.</span></span> <span data-ttu-id="37a3e-110">Questa configurazione non è disponibile nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="37a3e-110">This configuration is not available in hello portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="37a3e-111">**Informazioni sui modelli di distribuzione di Azure**</span><span class="sxs-lookup"><span data-stu-id="37a3e-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="37a3e-112">Circuiti ExpressRoute devono essere pre-configurati prima di seguire le istruzioni di hello seguenti.</span><span class="sxs-lookup"><span data-stu-id="37a3e-112">ExpressRoute circuits must be pre-configured before you follow hello instructions below.</span></span> <span data-ttu-id="37a3e-113">Assicurarsi di aver seguito le guide di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-classic.md) e [configurare il routing](expressroute-howto-routing-classic.md) prima di seguire i passaggi di hello riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="37a3e-113">Make sure that you have followed hello guides too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow hello steps below.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="37a3e-114">Limiti e limitazioni</span><span class="sxs-lookup"><span data-stu-id="37a3e-114">Limits and limitations</span></span>
* <span data-ttu-id="37a3e-115">**L'instradamento del transito non è supportato.**</span><span class="sxs-lookup"><span data-stu-id="37a3e-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="37a3e-116">Con Azure non è possibile attivare il routing tra la rete locale connessa tramite la VPN da sito a sito e la rete locale connessa tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="37a3e-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="37a3e-117">**La connessione da punto a sito non è supportata.**</span><span class="sxs-lookup"><span data-stu-id="37a3e-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="37a3e-118">Non è possibile abilitare toohello di connessioni VPN point-to-site stessa rete virtuale che è connesso tooExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="37a3e-118">You can't enable point-to-site VPN connections toohello same VNet that is connected tooExpressRoute.</span></span> <span data-ttu-id="37a3e-119">VPN Point-to-site ed ExpressRoute non può coesistere per hello stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="37a3e-119">Point-to-site VPN and ExpressRoute cannot coexist for hello same VNet.</span></span>
* <span data-ttu-id="37a3e-120">**Impossibile abilitare il tunneling forzato su gateway VPN da sito a sito hello.**</span><span class="sxs-lookup"><span data-stu-id="37a3e-120">**Forced tunneling cannot be enabled on hello Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="37a3e-121">È possibile solo "forzare" tutto associato a Internet traffico tooyour indietro rete locale tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="37a3e-121">You can only "force" all Internet-bound traffic back tooyour on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="37a3e-122">**Il gateway SKU Basic non è supportato.**</span><span class="sxs-lookup"><span data-stu-id="37a3e-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="37a3e-123">È necessario utilizzare un gateway non base SKU per entrambi hello [gateway ExpressRoute](expressroute-about-virtual-network-gateways.md) hello e [gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="37a3e-123">You must use a non-Basic SKU gateway for both hello [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and hello [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="37a3e-124">**È supportato solo il gateway VPN basato su route.**</span><span class="sxs-lookup"><span data-stu-id="37a3e-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="37a3e-125">È necessario usare un [gateway VPN basato su route](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="37a3e-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="37a3e-126">**Deve essere configurata una route statica per il gateway VPN.**</span><span class="sxs-lookup"><span data-stu-id="37a3e-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="37a3e-127">Se la rete locale è connesso tooboth ExpressRoute e una Site-to-Site VPN, è necessario disporre una route statica configurata nel toohello di connessione di rete locale tooroute hello Site-to-Site VPN rete Internet pubblica.</span><span class="sxs-lookup"><span data-stu-id="37a3e-127">If your local network is connected tooboth ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network tooroute hello Site-to-Site VPN connection toohello public Internet.</span></span>
* <span data-ttu-id="37a3e-128">**Il gateway ExpressRoute deve essere configurato prima.**</span><span class="sxs-lookup"><span data-stu-id="37a3e-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="37a3e-129">È necessario creare innanzitutto gateway ExpressRoute hello prima di aggiungere gateway VPN da sito a sito hello.</span><span class="sxs-lookup"><span data-stu-id="37a3e-129">You must create hello ExpressRoute gateway first before you add hello Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="37a3e-130">Progetti di configurazione</span><span class="sxs-lookup"><span data-stu-id="37a3e-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="37a3e-131">Configurare una VPN da sito a sito come percorso di failover per ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="37a3e-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="37a3e-132">È possibile configurare una connessione VPN da sito a sito come backup per ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="37a3e-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="37a3e-133">Si applica solo toovirtual reti collegate toohello Azure percorso di peering privato.</span><span class="sxs-lookup"><span data-stu-id="37a3e-133">This applies only toovirtual networks linked toohello Azure private peering path.</span></span> <span data-ttu-id="37a3e-134">Non esiste alcuna soluzione di failover basato su VPN per i servizi accessibili tramite i peering pubblico di Azure e Microsoft.</span><span class="sxs-lookup"><span data-stu-id="37a3e-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="37a3e-135">Hello circuito ExpressRoute è sempre collegamento primario hello.</span><span class="sxs-lookup"><span data-stu-id="37a3e-135">hello ExpressRoute circuit is always hello primary link.</span></span> <span data-ttu-id="37a3e-136">Flusso dei dati tramite il percorso VPN Site-to-Site hello solo se hello circuito ExpressRoute ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="37a3e-136">Data will flow through hello Site-to-Site VPN path only if hello ExpressRoute circuit fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="37a3e-137">Mentre il circuito ExpressRoute è preferito tramite VPN Site-to-Site quando entrambe le route sono hello stesso, Azure utilizzerà hello più lunga prefisso corrispondenza toochoose hello route verso la destinazione del pacchetto di hello.</span><span class="sxs-lookup"><span data-stu-id="37a3e-137">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are hello same, Azure will use hello longest prefix match toochoose hello route towards hello packet's destination.</span></span>
> 
> 

![Coesistenza](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a><span data-ttu-id="37a3e-139">Configurare un toosites tooconnect VPN da sito a sito non è connesso tramite ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="37a3e-139">Configure a Site-to-Site VPN tooconnect toosites not connected through ExpressRoute</span></span>
<span data-ttu-id="37a3e-140">È possibile configurare la rete in cui alcuni siti si connettono direttamente tooAzure tramite VPN Site-to-Site e alcuni siti si connettono tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="37a3e-140">You can configure your network where some sites connect directly tooAzure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Coesistenza](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="37a3e-142">Non è possibile configurare una rete virtuale come router di transito.</span><span class="sxs-lookup"><span data-stu-id="37a3e-142">You cannot a configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-hello-steps-toouse"></a><span data-ttu-id="37a3e-143">Selezione di hello passaggi toouse</span><span class="sxs-lookup"><span data-stu-id="37a3e-143">Selecting hello steps toouse</span></span>
<span data-ttu-id="37a3e-144">Esistono due diversi set di procedure toochoose dall'ordine tooconfigure nelle connessioni in cui possono coesistere.</span><span class="sxs-lookup"><span data-stu-id="37a3e-144">There are two different sets of procedures toochoose from in order tooconfigure connections that can coexist.</span></span> <span data-ttu-id="37a3e-145">procedura di configurazione di Hello selezionato dipenderà se si dispone di una rete virtuale esistente che si desidera tooconnect a o si desidera toocreate una nuova rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="37a3e-145">hello configuration procedure that you select will depend on whether you have an existing virtual network that you want tooconnect to, or you want toocreate a new virtual network.</span></span>

* <span data-ttu-id="37a3e-146">Non dispone di una rete virtuale e necessario toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="37a3e-146">I don't have a VNet and need toocreate one.</span></span>
  
    <span data-ttu-id="37a3e-147">Se si dispone già di una rete virtuale, questa procedura assiste l'utente la creazione di una nuova rete virtuale utilizzando il modello di distribuzione classica hello e creazione di nuove connessioni di VPN Site-to-Site ed ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="37a3e-147">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using hello classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="37a3e-148">tooconfigure, eseguire i passaggi nella sezione articolo hello hello [toocreate una nuova rete virtuale e le connessioni coesistenti](#new).</span><span class="sxs-lookup"><span data-stu-id="37a3e-148">tooconfigure, follow hello steps in hello article section [toocreate a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="37a3e-149">È già disponibile una rete virtuale con modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="37a3e-149">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="37a3e-150">E’ possibile che esista già una rete virtuale con una connessione VPN da sito a sito o una connessione ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="37a3e-150">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="37a3e-151">Hello articolo sezione [tooconfigure coexsiting connessioni per una rete virtuale di già esistente](#add) consentirà di eliminazione del gateway hello e quindi la creazione di nuove connessioni VPN Site-to-Site ed ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="37a3e-151">hello article section [tooconfigure coexsiting connections for an already existing VNet](#add) will walk you through deleting hello gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="37a3e-152">Si noti che, quando si creano hello nuove connessioni, è necessario completare i passaggi di hello in un ordine specifico.</span><span class="sxs-lookup"><span data-stu-id="37a3e-152">Note that when creating hello new connections, hello steps must be completed in a very specific order.</span></span> <span data-ttu-id="37a3e-153">Non utilizzare istruzioni hello toocreate altri articoli del gateway e connessioni.</span><span class="sxs-lookup"><span data-stu-id="37a3e-153">Don't use hello instructions in other articles toocreate your gateways and connections.</span></span>
  
    <span data-ttu-id="37a3e-154">In questa procedura, la creazione di connessioni che possono coesistere verrà richiedono toodelete è il gateway e quindi configurare nuovi gateway.</span><span class="sxs-lookup"><span data-stu-id="37a3e-154">In this procedure, creating connections that can coexist will require you toodelete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="37a3e-155">Ciò significa che si disporrà di tempo di inattività per le connessioni cross-premise mentre eliminare e ricreare il gateway e connessioni, ma non è necessario toomigrate le macchine virtuali o servizi tooa nuova rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="37a3e-155">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need toomigrate any of your VMs or services tooa new virtual network.</span></span> <span data-ttu-id="37a3e-156">Le macchine virtuali e servizi sarà comunque in grado di toocommunicate out tramite bilanciamento del carico hello durante la configurazione del gateway se sono pertanto toodo configurato.</span><span class="sxs-lookup"><span data-stu-id="37a3e-156">Your VMs and services will still be able toocommunicate out through hello load balancer while you configure your gateway if they are configured toodo so.</span></span>

## <span data-ttu-id="37a3e-157"><a name="new"></a>connessioni coesistenti e toocreate una nuova rete virtuale</span><span class="sxs-lookup"><span data-stu-id="37a3e-157"><a name="new"></a>toocreate a new virtual network and coexisting connections</span></span>
<span data-ttu-id="37a3e-158">Questa procedura illustra come creare una rete virtuale e connessioni da sito a sito ed ExpressRoute coesistenti.</span><span class="sxs-lookup"><span data-stu-id="37a3e-158">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="37a3e-159">È necessario tooinstall hello più recente di hello cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37a3e-159">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="37a3e-160">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="37a3e-160">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="37a3e-161">Si noti che i cmdlet di hello che verrà utilizzato per questa configurazione potrebbero essere leggermente diversi rispetto a ciò che potrebbe acquisire familiarità con.</span><span class="sxs-lookup"><span data-stu-id="37a3e-161">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="37a3e-162">I cmdlet di hello toouse che è possibile specificare in queste istruzioni.</span><span class="sxs-lookup"><span data-stu-id="37a3e-162">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="37a3e-163">Creare uno schema per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="37a3e-163">Create a schema for your virtual network.</span></span> <span data-ttu-id="37a3e-164">Per ulteriori informazioni sullo schema di configurazione di hello, vedere [dello schema di configurazione di rete virtuale di Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="37a3e-164">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="37a3e-165">Quando si crea lo schema, assicurarsi di che usare hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="37a3e-165">When you create your schema, make sure you use hello following values:</span></span>
   
   * <span data-ttu-id="37a3e-166">subnet del gateway per la rete virtuale hello Hello deve essere /27 o un prefisso (ad esempio /26 o /25) più breve.</span><span class="sxs-lookup"><span data-stu-id="37a3e-166">hello gateway subnet for hello virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="37a3e-167">tipo di connessione gateway Hello "dedicato".</span><span class="sxs-lookup"><span data-stu-id="37a3e-167">hello gateway connection type is "Dedicated".</span></span>
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. <span data-ttu-id="37a3e-168">Dopo la creazione e configurazione dei file di schema xml, caricare il file hello.</span><span class="sxs-lookup"><span data-stu-id="37a3e-168">After creating and configuring your xml schema file, upload hello file.</span></span> <span data-ttu-id="37a3e-169">Verrà creata la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="37a3e-169">This will create your virtual network.</span></span>
   
    <span data-ttu-id="37a3e-170">Utilizzare hello tooupload cmdlet seguenti il file, sostituendo il valore di hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="37a3e-170">Use hello following cmdlet tooupload your file, replacing hello value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <span data-ttu-id="37a3e-171"><a name="gw"></a>Creare un gateway ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="37a3e-171"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="37a3e-172">Toospecify assicurarsi di essere hello GatewaySKU come *Standard*, *ad alte prestazioni*, o *UltraPerformance* e il tipo di gateway come hello *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="37a3e-172">Be sure toospecify hello GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="37a3e-173">Utilizzare hello di esempio seguente, sostituendo i valori hello per uso personale.</span><span class="sxs-lookup"><span data-stu-id="37a3e-173">Use hello following sample, substituting hello values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="37a3e-174">Collegare il circuito ExpressRoute toohello di hello ExpressRoute gateway.</span><span class="sxs-lookup"><span data-stu-id="37a3e-174">Link hello ExpressRoute gateway toohello ExpressRoute circuit.</span></span> <span data-ttu-id="37a3e-175">Dopo questo passaggio è stato completato, viene stabilita connessione hello tra la rete locale e Azure tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="37a3e-175">After this step has been completed, hello connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <span data-ttu-id="37a3e-176"><a name="vpngw"></a>Creare quindi il gateway VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="37a3e-176"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="37a3e-177">Hello GatewaySKU deve essere *Standard*, *ad alte prestazioni*, o *UltraPerformance* e hello il tipo di gateway deve essere *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="37a3e-177">hello GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and hello GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="37a3e-178">tooretrieve hello virtuale gateway le impostazioni di rete, inclusi ID gateway hello e indirizzo IP pubblico hello, utilizzano hello `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="37a3e-178">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. <span data-ttu-id="37a3e-179">Creare un'entità gateway VPN del sito locale.</span><span class="sxs-lookup"><span data-stu-id="37a3e-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="37a3e-180">Questo comando non configura il gateway VPN locale.</span><span class="sxs-lookup"><span data-stu-id="37a3e-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="37a3e-181">Invece, consente di impostazioni del gateway locale hello tooprovide, ad esempio indirizzo IP pubblico hello e hello locale lo spazio degli indirizzi, in modo che hello gateway VPN di Azure può connettersi tooit.</span><span class="sxs-lookup"><span data-stu-id="37a3e-181">Rather, it allows you tooprovide hello local gateway settings, such as hello public IP and hello on-premises address space, so that hello Azure VPN gateway can connect tooit.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="37a3e-182">sito locale di Hello per hello VPN da sito a sito non è definito in netcfg hello.</span><span class="sxs-lookup"><span data-stu-id="37a3e-182">hello local site for hello Site-to-Site VPN is not defined in hello netcfg.</span></span> <span data-ttu-id="37a3e-183">In alternativa, è necessario utilizzare i parametri del sito locale hello toospecify questo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="37a3e-183">Instead, you must use this cmdlet toospecify hello local site parameters.</span></span> <span data-ttu-id="37a3e-184">È possibile definire tramite portale o file netcfg hello.</span><span class="sxs-lookup"><span data-stu-id="37a3e-184">You cannot define it using either portal, or hello netcfg file.</span></span>
   > 
   > 
   
    <span data-ttu-id="37a3e-185">Utilizzare hello di esempio seguente, sostituendo i valori hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="37a3e-185">Use hello following sample, replacing hello values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > <span data-ttu-id="37a3e-186">Se la rete locale include più route, è possibile passarle tutte come una matrice.</span><span class="sxs-lookup"><span data-stu-id="37a3e-186">If your local network has multiple routes, you can pass them all in as an array.</span></span>  <span data-ttu-id="37a3e-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span><span class="sxs-lookup"><span data-stu-id="37a3e-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span></span>  
   > 
   > 

    <span data-ttu-id="37a3e-188">tooretrieve hello virtuale gateway le impostazioni di rete, inclusi ID gateway hello e indirizzo IP pubblico hello, utilizzano hello `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="37a3e-188">tooretrieve hello virtual network gateway settings, including hello gateway ID and hello public IP, use hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="37a3e-189">Vedere hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="37a3e-189">See hello following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="37a3e-190">Configurare il gateway VPN locale dispositivo tooconnect toohello nuovo.</span><span class="sxs-lookup"><span data-stu-id="37a3e-190">Configure your local VPN device tooconnect toohello new gateway.</span></span> <span data-ttu-id="37a3e-191">Utilizzare le informazioni di hello recuperato nel passaggio 6 quando si configura il dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="37a3e-191">Use hello information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="37a3e-192">Per altre informazioni sulla configurazione del dispositivo VPN, vedere l'articolo relativo alla [configurazione del dispositivo VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="37a3e-192">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="37a3e-193">Collegamento hello Site-to-Site VPN gateway in gateway locale toohello Azure.</span><span class="sxs-lookup"><span data-stu-id="37a3e-193">Link hello Site-to-Site VPN gateway on Azure toohello local gateway.</span></span>
   
    <span data-ttu-id="37a3e-194">In questo esempio, connectedEntityId è l'ID del gateway locale hello, che è possibile trovare eseguendo `Get-AzureLocalNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="37a3e-194">In this example, connectedEntityId is hello local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="37a3e-195">È possibile trovare virtualNetworkGatewayId utilizzando hello `Get-AzureVirtualNetworkGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="37a3e-195">You can find virtualNetworkGatewayId by using hello `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="37a3e-196">Dopo questo passaggio, viene stabilita la connessione di hello tra la rete locale e Azure tramite hello connessione VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="37a3e-196">After this step, hello connection between your local network and Azure via hello Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <span data-ttu-id="37a3e-197"><a name="add"></a>tooconfigure coexsiting connessioni per una rete virtuale di già esistente</span><span class="sxs-lookup"><span data-stu-id="37a3e-197"><a name="add"></a>tooconfigure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="37a3e-198">Se si dispone di una rete virtuale esistente, è possibile controllare la dimensione della subnet gateway hello.</span><span class="sxs-lookup"><span data-stu-id="37a3e-198">If you have an existing virtual network, check hello gateway subnet size.</span></span> <span data-ttu-id="37a3e-199">Se subnet del gateway hello /28 o /29, è necessario eliminare il gateway di rete virtuale hello e aumentare la dimensione della subnet gateway hello.</span><span class="sxs-lookup"><span data-stu-id="37a3e-199">If hello gateway subnet is /28 or /29, you must first delete hello virtual network gateway and increase hello gateway subnet size.</span></span> <span data-ttu-id="37a3e-200">Hello passaggi in questa sezione verranno illustrato come toodo che.</span><span class="sxs-lookup"><span data-stu-id="37a3e-200">hello steps in this section will show you how toodo that.</span></span>

<span data-ttu-id="37a3e-201">Se subnet del gateway hello è /27 o superiore e la rete virtuale hello è connesso tramite ExpressRoute, è possibile ignorare i passaggi di hello riportati di seguito e andare troppo["Passaggio 6: creare un gateway VPN da sito a sito"](#vpngw) nella sezione precedente hello.</span><span class="sxs-lookup"><span data-stu-id="37a3e-201">If hello gateway subnet is /27 or larger and hello virtual network is connected via ExpressRoute, you can skip hello steps below and proceed too["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in hello previous section.</span></span>

> [!NOTE]
> <span data-ttu-id="37a3e-202">Quando si elimina gateway esistente hello, sedi locali perderà rete virtuale tooyour hello mentre si lavora in questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="37a3e-202">When you delete hello existing gateway, your local premises will lose hello connection tooyour virtual network while you are working on this configuration.</span></span>
> 
> 

1. <span data-ttu-id="37a3e-203">È necessario tooinstall hello più recente di hello cmdlet PowerShell di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="37a3e-203">You'll need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="37a3e-204">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="37a3e-204">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span> <span data-ttu-id="37a3e-205">Si noti che i cmdlet di hello che verrà utilizzato per questa configurazione potrebbero essere leggermente diversi rispetto a ciò che potrebbe acquisire familiarità con.</span><span class="sxs-lookup"><span data-stu-id="37a3e-205">Note that hello cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="37a3e-206">I cmdlet di hello toouse che è possibile specificare in queste istruzioni.</span><span class="sxs-lookup"><span data-stu-id="37a3e-206">Be sure toouse hello cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="37a3e-207">Eliminare il gateway ExpressRoute o VPN da sito a sito esistente hello.</span><span class="sxs-lookup"><span data-stu-id="37a3e-207">Delete hello existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="37a3e-208">Utilizzare hello cmdlet seguenti, sostituendo i valori hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="37a3e-208">Use hello following cmdlet, replacing hello values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="37a3e-209">Esportare lo schema di rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="37a3e-209">Export hello virtual network schema.</span></span> <span data-ttu-id="37a3e-210">Utilizzare hello cmdlet di PowerShell seguente, sostituendo i valori hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="37a3e-210">Use hello following PowerShell cmdlet, replacing hello values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="37a3e-211">Modifica schema di file di configurazione di rete hello in modo che sia di subnet del gateway hello /27 o un prefisso (ad esempio /26 o /25) più breve.</span><span class="sxs-lookup"><span data-stu-id="37a3e-211">Edit hello network configuration file schema so that hello gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="37a3e-212">Vedere hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="37a3e-212">See hello following example.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="37a3e-213">Se non si dispone di indirizzi IP sufficiente la dimensione di subnet gateway di rete virtuale tooincrease hello a sinistra, è necessario tooadd più spazio di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="37a3e-213">If you don't have enough IP addresses left in your virtual network tooincrease hello gateway subnet size, you need tooadd more IP address space.</span></span> <span data-ttu-id="37a3e-214">Per ulteriori informazioni sullo schema di configurazione di hello, vedere [dello schema di configurazione di rete virtuale di Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="37a3e-214">For more information about hello configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="37a3e-215">Se il gateway precedente era una VPN Site-to-Site, è necessario modificare anche il tipo di connessione hello troppo**dedicato**.</span><span class="sxs-lookup"><span data-stu-id="37a3e-215">If your previous gateway was a Site-to-Site VPN, you must also change hello connection type too**Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="37a3e-216">A questo punto, si avrà una rete virtuale senza gateway.</span><span class="sxs-lookup"><span data-stu-id="37a3e-216">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="37a3e-217">toocreate nuovi gateway e completare le connessioni, è possibile procedere con [passaggio 4: creare un gateway ExpressRoute](#gw), trovato in hello precedente set di passaggi.</span><span class="sxs-lookup"><span data-stu-id="37a3e-217">toocreate new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in hello preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37a3e-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="37a3e-218">Next steps</span></span>
<span data-ttu-id="37a3e-219">Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md)</span><span class="sxs-lookup"><span data-stu-id="37a3e-219">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md)</span></span>

