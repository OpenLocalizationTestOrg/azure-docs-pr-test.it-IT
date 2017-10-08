---
title: le route aaaTroubleshoot - PowerShell | Documenti Microsoft
description: Informazioni su come tootroubleshoot instrada nel modello di distribuzione Azure Resource Manager hello con Azure PowerShell.
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 7a07806df5c1d0caee921187e6ad29f6755ab535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a><span data-ttu-id="e685d-103">Risoluzione dei problemi di route con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e685d-103">Troubleshoot routes using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e685d-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e685d-104">Azure Portal</span></span>](virtual-network-routes-troubleshoot-portal.md)
> * [<span data-ttu-id="e685d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e685d-105">PowerShell</span></span>](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="e685d-106">Se si verificano tooor problemi connettività di rete dalla macchina virtuale di Azure (VM), le route possono influire dei flussi di traffico della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e685d-106">If you are experiencing network connectivity issues tooor from your Azure Virtual Machine (VM), routes may be impacting your VM traffic flows.</span></span> <span data-ttu-id="e685d-107">Questo articolo fornisce una panoramica delle funzionalità di diagnostica per le route toohelp risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="e685d-107">This article provides an overview of diagnostics capabilities for routes toohelp troubleshoot further.</span></span>

<span data-ttu-id="e685d-108">Le tabelle di route sono associate alle subnet e valgono per tutte le interfacce di rete della subnet.</span><span class="sxs-lookup"><span data-stu-id="e685d-108">Route tables are associated with subnets and are effective on all network interfaces (NIC) in that subnet.</span></span> <span data-ttu-id="e685d-109">Hello seguenti tipi di route può essere applicati tooeach interfaccia di rete:</span><span class="sxs-lookup"><span data-stu-id="e685d-109">hello following types of routes can be applied tooeach network interface:</span></span>

* <span data-ttu-id="e685d-110">**Route di sistema:** per impostazione predefinita, ogni subnet creata in una rete virtuale di Azure dispone di tabelle di route di sistema che consentono il traffico di rete virtuale locale, il traffico locale tramite gateway VPN e il traffico Internet.</span><span class="sxs-lookup"><span data-stu-id="e685d-110">**System routes:** By default, every subnet created in an Azure Virtual Network (VNet) has system route tables that allow local VNet traffic, on-premises traffic via VPN gateways, and Internet traffic.</span></span> <span data-ttu-id="e685d-111">Le route di sistema esistono anche per le reti virtuali con peering.</span><span class="sxs-lookup"><span data-stu-id="e685d-111">System routes also exist for peered VNets.</span></span>
* <span data-ttu-id="e685d-112">**Le route BGP:** propagate interfacce toonetwork attraverso ExpressRoute o le connessioni VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="e685d-112">**BGP routes:** Propagated toonetwork interfaces through ExpressRoute or site-to-site VPN connections.</span></span> <span data-ttu-id="e685d-113">Altre informazioni su routing BGP leggendo hello [BGP con gateway VPN](../vpn-gateway/vpn-gateway-bgp-overview.md) e [panoramica relativa a ExpressRoute](../expressroute/expressroute-introduction.md) articoli.</span><span class="sxs-lookup"><span data-stu-id="e685d-113">Learn more about BGP routing by reading hello [BGP with VPN gateways](../vpn-gateway/vpn-gateway-bgp-overview.md) and [ExpressRoute overview](../expressroute/expressroute-introduction.md) articles.</span></span>
* <span data-ttu-id="e685d-114">**Le route definite dall'utente (UDR):** se si usano dispositivi di rete virtuali o sono a tunneling forzato rete locale tooan del traffico tramite una VPN site-to-site, è possibile route definite dall'utente (UDRs) associate con la tabella di route della subnet.</span><span class="sxs-lookup"><span data-stu-id="e685d-114">**User-defined routes (UDR):** If you are using network virtual appliances or are forced-tunneling traffic tooan on-premises network via a site-to-site VPN, you may have user-defined routes (UDRs) associated with your subnet route table.</span></span> <span data-ttu-id="e685d-115">Se non si ha familiarità con UDRs, leggere hello [le route definite dall'utente](virtual-networks-udr-overview.md#user-defined-routes) articolo.</span><span class="sxs-lookup"><span data-stu-id="e685d-115">If you're not familiar with UDRs, read hello [user-defined routes](virtual-networks-udr-overview.md#user-defined-routes) article.</span></span>

<span data-ttu-id="e685d-116">Con hello route diverse che possono essere applicati tooa l'interfaccia di rete, può essere difficile toodetermine le route di aggregazione sono efficaci.</span><span class="sxs-lookup"><span data-stu-id="e685d-116">With hello various routes that can be applied tooa network interface, it can be difficult toodetermine which aggregate routes are effective.</span></span> <span data-ttu-id="e685d-117">toohelp risoluzione dei problemi di connettività di rete VM, è possibile visualizzare tutte le route efficaci hello per un'interfaccia di rete nel modello di distribuzione Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="e685d-117">toohelp troubleshoot VM network connectivity, you can view all hello effective routes for a network interface in hello Azure Resource Manager deployment model.</span></span>

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="e685d-118">Utilizzo di VM route valide tootroubleshoot il flusso del traffico</span><span class="sxs-lookup"><span data-stu-id="e685d-118">Using Effective Routes tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="e685d-119">In questo articolo Usa hello segue scenario come tooillustrate un esempio come tootroubleshoot hello effettiva instrada per un'interfaccia di rete:</span><span class="sxs-lookup"><span data-stu-id="e685d-119">This article uses hello following scenario as an example tooillustrate how tootroubleshoot hello effective routes for a network interface:</span></span>

<span data-ttu-id="e685d-120">Una macchina virtuale (*VM1*) connessi toohello rete virtuale (*VNet1*, prefisso: 10.9.0.0/16) ha esito negativo tooconnect tooa VM(VM3) in una rete virtuale appena peered (*VNet3*, prefisso 10.10.0.0/16).</span><span class="sxs-lookup"><span data-stu-id="e685d-120">A VM (*VM1*) connected toohello VNet (*VNet1*, prefix: 10.9.0.0/16) fails tooconnect tooa VM(VM3) in a newly peered VNet (*VNet3*, prefix 10.10.0.0/16).</span></span> <span data-ttu-id="e685d-121">Sono disponibili UDRs o BGP non instrada applicato tooVM1-NIC1 rete interfaccia connessa toohello macchina virtuale, vengono applicate solo le route di sistema.</span><span class="sxs-lookup"><span data-stu-id="e685d-121">There are no UDRs or BGP routes applied tooVM1-NIC1 network interface connected toohello VM, only system routes are applied.</span></span>

<span data-ttu-id="e685d-122">Questo articolo spiega come hello toodetermine causa dell'errore di connessione hello, utilizzando la funzionalità di route valide nel modello di distribuzione di gestione delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="e685d-122">This article explains how toodetermine hello cause of hello connection failure, using effective routes capability in Azure Resource Management deployment model.</span></span>
<span data-ttu-id="e685d-123">Mentre l'esempio hello Usa solo le route di sistema, hello stessi passaggi può essere utilizzati toodetermine errori di connessione in ingresso e in uscita su qualsiasi tipo di route.</span><span class="sxs-lookup"><span data-stu-id="e685d-123">While hello example uses only system routes, hello same steps can be used toodetermine inbound and outbound connection failures over any route type.</span></span>

> [!NOTE]
> <span data-ttu-id="e685d-124">Se la macchina virtuale è associata più di una scheda di rete, controllare route valide per ogni hello NIC tooand di problemi la connettività di rete toodiagnose da una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e685d-124">If your VM has more than one NIC attached, check effective routes for each of hello NICs toodiagnose network connectivity issues tooand from a VM.</span></span>
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a><span data-ttu-id="e685d-125">Visualizzare le route valide per una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="e685d-125">View effective routes for a virtual machine</span></span>
<span data-ttu-id="e685d-126">toosee hello aggregazione route che vengono applicato tooa macchina virtuale, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e685d-126">toosee hello aggregate routes that are applied tooa VM, complete hello following steps:</span></span>

### <a name="view-effective-routes-for-a-network-interface"></a><span data-ttu-id="e685d-127">Visualizzare le route valide per un'interfaccia di rete</span><span class="sxs-lookup"><span data-stu-id="e685d-127">View effective routes for a network interface</span></span>
<span data-ttu-id="e685d-128">toosee hello aggregazione route tooa applicata l'interfaccia di rete, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="e685d-128">toosee hello aggregate routes that are applied tooa network interface, complete hello following steps:</span></span>

1. <span data-ttu-id="e685d-129">Avviare un tooAzure di sessione e l'account di accesso di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e685d-129">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="e685d-130">Se non si ha familiarità con Azure PowerShell, leggere hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) articolo.</span><span class="sxs-lookup"><span data-stu-id="e685d-130">If you’re not familiar with Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="e685d-131">il comando seguente Hello restituisce tutte le route applicate tooa l'interfaccia di rete denominata *VM1 NIC1* nel gruppo di risorse hello *RG1*.</span><span class="sxs-lookup"><span data-stu-id="e685d-131">hello following command returns all routes applied tooa network interface named *VM1-NIC1* in hello resource group *RG1*.</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="e685d-132">Se non si conosce il nome di hello un'interfaccia di rete, digitare hello seguente i nomi di comando tooretrieve hello di tutte le interfacce di rete in un group.* risorse</span><span class="sxs-lookup"><span data-stu-id="e685d-132">If you don’t know hello name of a network interface, type hello following command tooretrieve hello names of all network interfaces in a resource group.*</span></span>
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   <span data-ttu-id="e685d-133">Hello output seguente cerca un output simile toohello hello di subnet toohello ogni route applicato a che connessa:</span><span class="sxs-lookup"><span data-stu-id="e685d-133">hello following output looks similar toohello output for each route applied toohello subnet hello NIC is connected to:</span></span>
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   <span data-ttu-id="e685d-134">Si noti seguenti hello nell'output di hello:</span><span class="sxs-lookup"><span data-stu-id="e685d-134">Notice hello following in hello output:</span></span>
   
   * <span data-ttu-id="e685d-135">**Nome**: nome della route valida hello può essere vuoto, a meno che non venga specificato esplicitamente, per le route definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="e685d-135">**Name**: Name of hello effective route may be empty, unless explicitly specified, for user-defined routes.</span></span> 
   * <span data-ttu-id="e685d-136">**Stato**: indica lo stato della route valida hello.</span><span class="sxs-lookup"><span data-stu-id="e685d-136">**State**: Indicates state of hello effective route.</span></span> <span data-ttu-id="e685d-137">Alcuni valori possibili sono "Active" o "Invalid"</span><span class="sxs-lookup"><span data-stu-id="e685d-137">Possible values are "Active" or "Invalid"</span></span>
   * <span data-ttu-id="e685d-138">**AddressPrefixes**: Specifica il prefisso di indirizzo hello della route valida hello in notazione CIDR.</span><span class="sxs-lookup"><span data-stu-id="e685d-138">**AddressPrefixes**: Specifies hello address prefix of hello effective route in CIDR notation.</span></span> 
   * <span data-ttu-id="e685d-139">**nextHopType**: indica l'hop successivo di hello per hello route specificato.</span><span class="sxs-lookup"><span data-stu-id="e685d-139">**nextHopType**: Indicates hello next hop for hello given route.</span></span> <span data-ttu-id="e685d-140">I valori possibili sono *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* e *Null*.</span><span class="sxs-lookup"><span data-stu-id="e685d-140">Possible values are *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering*, or *Null*.</span></span> <span data-ttu-id="e685d-141">Un valore *Null* per **nextHopType** in una route definita dall'utente potrebbe indicare una route non valida.</span><span class="sxs-lookup"><span data-stu-id="e685d-141">A value of *Null* for **nextHopType** in a UDR may indicate an invalid route.</span></span> <span data-ttu-id="e685d-142">Ad esempio, se **nextHopType** è *VirtualAppliance* e hello network appliance virtuale macchina virtuale non è in uno stato di provisioning/esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e685d-142">For example, if **nextHopType** is *VirtualAppliance* and hello network virtual appliance VM is not in a provisioned/running state.</span></span> <span data-ttu-id="e685d-143">Se **nextHopType** è *VPNGateway* e non è stato eseguito il provisioning/in esecuzione nella rete virtuale specificata hello alcun gateway, route hello potrebbe diventare non valide.</span><span class="sxs-lookup"><span data-stu-id="e685d-143">If **nextHopType** is *VPNGateway* and there is no gateway provisioned/running in hello given VNet, hello route may become invalid.</span></span>
   * <span data-ttu-id="e685d-144">**NextHopIpAddress**: specifica hello di indirizzo IP dell'hop successivo di hello della route valida hello.</span><span class="sxs-lookup"><span data-stu-id="e685d-144">**NextHopIpAddress**: Specifies hello IP address of hello next hop of hello effective route.</span></span>
   
   <span data-ttu-id="e685d-145">Hello seguente comando restituisce le route hello in una tabella tooview più semplice:</span><span class="sxs-lookup"><span data-stu-id="e685d-145">hello following command returns hello routes in an easier tooview table:</span></span>
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   <span data-ttu-id="e685d-146">Hello output riportato di seguito è parte dell'output di hello ricevuto per uno scenario di hello descritto in precedenza:</span><span class="sxs-lookup"><span data-stu-id="e685d-146">hello following output is some of hello output received for hello scenario described previously:</span></span>
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. <span data-ttu-id="e685d-147">Non vi è alcun toohello route elencate *WestUS VNet3* rete virtuale (prefisso 10.10.0.0/16)** da *WestUS VNet1* (prefisso 10.9.0.0/16) nell'output di hello dal passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="e685d-147">There is no route listed toohello *WestUS-VNet3* VNet (Prefix 10.10.0.0/16)** from *WestUS-VNet1* (Prefix 10.9.0.0/16) in hello output from hello previous step.</span></span> <span data-ttu-id="e685d-148">Come illustrato nella seguente immagine hello, hello collegamento di peering reti virtuali con hello *WestUS VNet3* rete virtuale è in hello *Disconnected* stato.</span><span class="sxs-lookup"><span data-stu-id="e685d-148">As shown in hello following picture, hello VNet peering link with hello *WestUS-VNet3* VNet is in hello *Disconnected* state.</span></span>
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    <span data-ttu-id="e685d-149">collegamento bidirezionale Hello di peering hello è interrotta, che spiega perché VM1 Impossibile connettersi tooVM3 in hello *WestUS VNet3* rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e685d-149">hello bi-directional link for hello peering is broken, which explains why VM1 could not connect tooVM3 in hello *WestUS-VNet3* VNet.</span></span> <span data-ttu-id="e685d-150">Configurare di nuovo un collegamento di peering di rete virtuale bidirezionale per le reti virtuali *WestUS VNet1* *WestUS VNet3*.</span><span class="sxs-lookup"><span data-stu-id="e685d-150">Setup a bi-directional VNet peering link again for *WestUS-VNet1* and *WestUS-VNet3* VNets.</span></span> <span data-ttu-id="e685d-151">output di Hello restituito dopo aver stabilito il collegamento di peering reti virtuali hello correttamente segue:</span><span class="sxs-lookup"><span data-stu-id="e685d-151">hello output returned after hello VNet peering link is correctly established follows:</span></span>
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    <span data-ttu-id="e685d-152">Dopo aver determinato problema hello, è possibile aggiungere, rimuovere, o modificare le route e tabelle di route.</span><span class="sxs-lookup"><span data-stu-id="e685d-152">Once you determine hello issue, you can add, remove, or change routes and route tables.</span></span> <span data-ttu-id="e685d-153">Digitare hello successivo comando toosee un elenco di hello comandi utilizzati toodo pertanto:</span><span class="sxs-lookup"><span data-stu-id="e685d-153">Type hello following command toosee a list of hello commands used toodo so:</span></span>
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a><span data-ttu-id="e685d-154">Considerazioni</span><span class="sxs-lookup"><span data-stu-id="e685d-154">Considerations</span></span>
<span data-ttu-id="e685d-155">Alcuni aspetti tookeep presente durante la revisione elenco hello di route restituito:</span><span class="sxs-lookup"><span data-stu-id="e685d-155">A few things tookeep in mind when reviewing hello list of routes returned:</span></span>

* <span data-ttu-id="e685d-156">Il routing è basato sulla corrispondenza del prefisso più lunga (LPM) tra le route definite dall'utente, BGP e di sistema.</span><span class="sxs-lookup"><span data-stu-id="e685d-156">Routing is based on Longest Prefix Match (LPM) among UDRs, BGP and system routes.</span></span> <span data-ttu-id="e685d-157">Se è presente più di una route con hello stesso LPM corrispondono, quindi una route viene selezionata in base origine hello seguente ordine:</span><span class="sxs-lookup"><span data-stu-id="e685d-157">If there is more than one route with hello same LPM match, then a route is selected based on its origin in hello following order:</span></span>
  
  * <span data-ttu-id="e685d-158">Route definita dall'utente</span><span class="sxs-lookup"><span data-stu-id="e685d-158">User-defined route</span></span>
  * <span data-ttu-id="e685d-159">Route BGP</span><span class="sxs-lookup"><span data-stu-id="e685d-159">BGP route</span></span>
  * <span data-ttu-id="e685d-160">Route di sistema (predefinita)</span><span class="sxs-lookup"><span data-stu-id="e685d-160">System (Default) route</span></span>
    
    <span data-ttu-id="e685d-161">Con route efficaci, è possibile visualizzare solo le route efficaci che corrispondono a LPM in base a tutte le route di hello disponibile.</span><span class="sxs-lookup"><span data-stu-id="e685d-161">With effective routes, you can only see effective routes that are LPM match based on all hello availble routes.</span></span> <span data-ttu-id="e685d-162">Mostrando come route hello vengono effettivamente valutate per una scheda di rete specificato, questo rende molto più semplice tootroubleshoot specifica le route che potrebbero influire negativamente sulla connettività da e verso la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="e685d-162">By showing how hello routes are actually evaluated for a given NIC, this makes it a lot easier tootroubleshoot specific routes that may be impacting connectivity to/from your VM.</span></span>
* <span data-ttu-id="e685d-163">Se si dispone di UDRs e inviano traffico tooa virtuale altri dispositivi di rete (NVA), con *VirtualAppliance* come **nextHopType**, verificare che l'inoltro IP sia abilitato sul traffico di hello NVA ricevente hello o i pacchetti vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="e685d-163">If you have UDRs and are sending traffic tooa network virtual appliance (NVA), with *VirtualAppliance* as **nextHopType**, ensure that IP forwarding is enabled on hello NVA receiving hello traffic or packets are dropped.</span></span> 
* <span data-ttu-id="e685d-164">Se è abilitato il tunneling forzato, tutto il traffico Internet in uscita sarà indirizzati tooon locale.</span><span class="sxs-lookup"><span data-stu-id="e685d-164">If Forced tunneling is enabled, all outbound Internet traffic will be routed tooon-premises.</span></span> <span data-ttu-id="e685d-165">RDP/SSH da Internet tooyour che macchina virtuale potrebbe non funzionare con questa impostazione, a seconda di come hello locale gestisce tale traffico.</span><span class="sxs-lookup"><span data-stu-id="e685d-165">RDP/SSH from Internet tooyour VM may not work with this setting, depending on how hello on-premises handles this traffic.</span></span> 
  <span data-ttu-id="e685d-166">Il tunneling forzato può essere abilitato:</span><span class="sxs-lookup"><span data-stu-id="e685d-166">Forced-tunneling can be enabled:</span></span>
  * <span data-ttu-id="e685d-167">Se si usa una VPN site-to-site, impostando una route definita dall'utente con nextHopType come Gateway VPN</span><span class="sxs-lookup"><span data-stu-id="e685d-167">If using site-to-site VPN, by setting a user-defined route (UDR) with nextHopType as VPN Gateway</span></span>
  * <span data-ttu-id="e685d-168">Se una route predefinita è pubblicizzata su BGP</span><span class="sxs-lookup"><span data-stu-id="e685d-168">If a default route is advertised over BGP</span></span>
* <span data-ttu-id="e685d-169">Per la rete virtuale peering correttamente, il traffico toowork una route di sistema **nextHopType** *VNetPeering* deve essere presente per il peering hello intervallo prefisso della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e685d-169">For VNet peering traffic toowork correctly, a system route with **nextHopType** *VNetPeering* must exist for hello peered VNet’s prefix range.</span></span> <span data-ttu-id="e685d-170">Se non esiste e hello peering reti virtuali, una route di tale collegamento ha un aspetto corretto:</span><span class="sxs-lookup"><span data-stu-id="e685d-170">If such a route doesn’t exist and hello VNet peering link looks OK:</span></span>
  * <span data-ttu-id="e685d-171">Attendere alcuni secondi e riprovare, se si tratta di un collegamento di peering appena stabilito.</span><span class="sxs-lookup"><span data-stu-id="e685d-171">Wait a few seconds and retry if it's a newly established peering link.</span></span> <span data-ttu-id="e685d-172">Occasionalmente Accetta route toopropagate più interfacce di rete tooall hello in una subnet.</span><span class="sxs-lookup"><span data-stu-id="e685d-172">It occasionally takes longer toopropagate routes tooall hello network interfaces in a subnet.</span></span>
  * <span data-ttu-id="e685d-173">Flussi di traffico hello potrebbero influire negativamente sulla regole Network Security Group (gruppo).</span><span class="sxs-lookup"><span data-stu-id="e685d-173">Network Security Group (NSG) rules may be impacting hello traffic flows.</span></span> <span data-ttu-id="e685d-174">Per ulteriori informazioni, vedere hello [risolvere i gruppi di sicurezza di rete](virtual-network-nsg-troubleshoot-powershell.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="e685d-174">For more information, see hello [Troubleshoot Network Security Groups](virtual-network-nsg-troubleshoot-powershell.md) article.</span></span>

