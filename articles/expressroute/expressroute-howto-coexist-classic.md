---
title: 'Configurare connessioni coesistenti ExpressRoute e VPN da sito a sito - Versione classica: Azure| Microsoft Docs'
description: Questo articolo illustra come configurare connessioni ExpressRoute e VPN da sito a sito ai fini della coesistenza per il modello di distribuzione classica.
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
ms.openlocfilehash: 09d1649f0ca0cf4ca464d95b29461cad3fe51788
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a><span data-ttu-id="e80be-103">Configurare connessioni coesistenti ExpressRoute e da sito a sito (versione classica)</span><span class="sxs-lookup"><span data-stu-id="e80be-103">Configure ExpressRoute and Site-to-Site coexisting connections (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e80be-104">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="e80be-104">PowerShell - Resource Manager</span></span>](expressroute-howto-coexist-resource-manager.md)
> * [<span data-ttu-id="e80be-105">PowerShell - Classico</span><span class="sxs-lookup"><span data-stu-id="e80be-105">PowerShell - Classic</span></span>](expressroute-howto-coexist-classic.md)
> 
> 

<span data-ttu-id="e80be-106">La possibilità di configurare una VPN da sito a sito ed ExpressRoute offre diversi vantaggi.</span><span class="sxs-lookup"><span data-stu-id="e80be-106">Having the ability to configure Site-to-Site VPN and ExpressRoute has several advantages.</span></span> <span data-ttu-id="e80be-107">È possibile configurare una VPN da sito a sito come percorso di failover sicuro per ExressRoute oppure usare VPN da sito a sito per connettersi a siti che non sono connessi tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e80be-107">You can configure Site-to-Site VPN as a secure failover path for ExressRoute, or use Site-to-Site VPNs to connect to sites that are not connected through ExpressRoute.</span></span> <span data-ttu-id="e80be-108">In questo articolo verranno illustrati i passaggi per configurare entrambi questi scenari.</span><span class="sxs-lookup"><span data-stu-id="e80be-108">We will cover the steps to configure both scenarios in this article.</span></span> <span data-ttu-id="e80be-109">Questo articolo si applica al modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="e80be-109">This article applies to the classic deployment model.</span></span> <span data-ttu-id="e80be-110">Questa configurazione non è disponibile nel portale.</span><span class="sxs-lookup"><span data-stu-id="e80be-110">This configuration is not available in the portal.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="e80be-111">**Informazioni sui modelli di distribuzione di Azure**</span><span class="sxs-lookup"><span data-stu-id="e80be-111">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="e80be-112">Per eseguire le istruzioni riportate di seguito devono essere presenti circuiti ExpressRoute preconfigurati.</span><span class="sxs-lookup"><span data-stu-id="e80be-112">ExpressRoute circuits must be pre-configured before you follow the instructions below.</span></span> <span data-ttu-id="e80be-113">Verificare di aver seguito le guide per la [creazione di un circuito ExpressRoute](expressroute-howto-circuit-classic.md) e per la [configurazione del routing](expressroute-howto-routing-classic.md) prima di eseguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="e80be-113">Make sure that you have followed the guides to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and [configure routing](expressroute-howto-routing-classic.md) before you follow the steps below.</span></span>
> 
> 

## <a name="limits-and-limitations"></a><span data-ttu-id="e80be-114">Limiti e limitazioni</span><span class="sxs-lookup"><span data-stu-id="e80be-114">Limits and limitations</span></span>
* <span data-ttu-id="e80be-115">**L'instradamento del transito non è supportato.**</span><span class="sxs-lookup"><span data-stu-id="e80be-115">**Transit routing is not supported.**</span></span> <span data-ttu-id="e80be-116">Con Azure non è possibile attivare il routing tra la rete locale connessa tramite la VPN da sito a sito e la rete locale connessa tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e80be-116">You cannot route (via Azure) between your local network connected via Site-to-Site VPN and your local network connected via ExpressRoute.</span></span>
* <span data-ttu-id="e80be-117">**La connessione da punto a sito non è supportata.**</span><span class="sxs-lookup"><span data-stu-id="e80be-117">**Point-to-site is not supported.**</span></span> <span data-ttu-id="e80be-118">Non è possibile abilitare connessioni VPN da punto a sito dalla stessa rete virtuale connessa a ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e80be-118">You can't enable point-to-site VPN connections to the same VNet that is connected to ExpressRoute.</span></span> <span data-ttu-id="e80be-119">Non possono coesistere connessioni VPN da punto a sito ed ExpressRoute per la stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e80be-119">Point-to-site VPN and ExpressRoute cannot coexist for the same VNet.</span></span>
* <span data-ttu-id="e80be-120">**Il tunneling forzato non può essere abilitato nel gateway VPN da sito a sito.**</span><span class="sxs-lookup"><span data-stu-id="e80be-120">**Forced tunneling cannot be enabled on the Site-to-Site VPN gateway.**</span></span> <span data-ttu-id="e80be-121">È soltanto possibile "forzare" tutto il traffico associato a Internet verso la rete locale tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e80be-121">You can only "force" all Internet-bound traffic back to your on-premises network via ExpressRoute.</span></span>
* <span data-ttu-id="e80be-122">**Il gateway SKU Basic non è supportato.**</span><span class="sxs-lookup"><span data-stu-id="e80be-122">**Basic SKU gateway is not supported.**</span></span> <span data-ttu-id="e80be-123">È necessario usare un gateway SKU non Basic sia per il [gateway ExpressRoute](expressroute-about-virtual-network-gateways.md) che per il [gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="e80be-123">You must use a non-Basic SKU gateway for both the [ExpressRoute gateway](expressroute-about-virtual-network-gateways.md) and the [VPN gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="e80be-124">**È supportato solo il gateway VPN basato su route.**</span><span class="sxs-lookup"><span data-stu-id="e80be-124">**Only route-based VPN gateway is supported.**</span></span> <span data-ttu-id="e80be-125">È necessario usare un [gateway VPN basato su route](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="e80be-125">You must use a route-based [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="e80be-126">**Deve essere configurata una route statica per il gateway VPN.**</span><span class="sxs-lookup"><span data-stu-id="e80be-126">**Static route should be configured for your VPN gateway.**</span></span> <span data-ttu-id="e80be-127">Se la rete locale è connessa sia a ExpressRoute che a una VPN da sito a sito, per il routing della connessione VPN da sito a sito alla rete Internet pubblica è necessario che nella rete locale sia configurata una route statica.</span><span class="sxs-lookup"><span data-stu-id="e80be-127">If your local network is connected to both ExpressRoute and a Site-to-Site VPN, you must have a static route configured in your local network to route the Site-to-Site VPN connection to the public Internet.</span></span>
* <span data-ttu-id="e80be-128">**Il gateway ExpressRoute deve essere configurato prima.**</span><span class="sxs-lookup"><span data-stu-id="e80be-128">**ExpressRoute gateway must be configured first.**</span></span> <span data-ttu-id="e80be-129">È necessario creare il gateway ExpressRoute prima di aggiungere il gateway VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="e80be-129">You must create the ExpressRoute gateway first before you add the Site-to-Site VPN gateway.</span></span>

## <a name="configuration-designs"></a><span data-ttu-id="e80be-130">Progetti di configurazione</span><span class="sxs-lookup"><span data-stu-id="e80be-130">Configuration designs</span></span>
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a><span data-ttu-id="e80be-131">Configurare una VPN da sito a sito come percorso di failover per ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e80be-131">Configure a Site-to-Site VPN as a failover path for ExpressRoute</span></span>
<span data-ttu-id="e80be-132">È possibile configurare una connessione VPN da sito a sito come backup per ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e80be-132">You can configure a Site-to-Site VPN connection as a backup for ExpressRoute.</span></span> <span data-ttu-id="e80be-133">Questo si applica solo alle reti virtuali collegate al percorso di peering privato di Azure.</span><span class="sxs-lookup"><span data-stu-id="e80be-133">This applies only to virtual networks linked to the Azure private peering path.</span></span> <span data-ttu-id="e80be-134">Non esiste alcuna soluzione di failover basato su VPN per i servizi accessibili tramite i peering pubblico di Azure e Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e80be-134">There is no VPN-based failover solution for services accessible through Azure public and Microsoft peerings.</span></span> <span data-ttu-id="e80be-135">Il circuito ExpressRoute è sempre il collegamento principale.</span><span class="sxs-lookup"><span data-stu-id="e80be-135">The ExpressRoute circuit is always the primary link.</span></span> <span data-ttu-id="e80be-136">Il flusso dei dati attraverserà il percorso VPN da sito a sito solo se il circuito ExpressRoute ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="e80be-136">Data will flow through the Site-to-Site VPN path only if the ExpressRoute circuit fails.</span></span> 

> [!NOTE]
> <span data-ttu-id="e80be-137">Mentre il circuito ExpressRoute viene preferito sulla VPN da sito a sito quando entrambe le route sono uguali, Azure userà la corrispondenza di prefisso più lunga per scegliere la route verso la destinazione del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="e80be-137">While ExpressRoute circuit is preferred over Site-to-Site VPN when both routes are the same, Azure will use the longest prefix match to choose the route towards the packet's destination.</span></span>
> 
> 

![Coesistenza](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-to-connect-to-sites-not-connected-through-expressroute"></a><span data-ttu-id="e80be-139">Configurare una VPN da sito a sito per la connessione a siti non connessi tramite ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e80be-139">Configure a Site-to-Site VPN to connect to sites not connected through ExpressRoute</span></span>
<span data-ttu-id="e80be-140">È possibile configurare una rete in cui alcuni siti si connettono direttamente ad Azure tramite VPN da sito a sito e altri si connettono tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e80be-140">You can configure your network where some sites connect directly to Azure over Site-to-Site VPN, and some sites connect through ExpressRoute.</span></span> 

![Coesistenza](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> <span data-ttu-id="e80be-142">Non è possibile configurare una rete virtuale come router di transito.</span><span class="sxs-lookup"><span data-stu-id="e80be-142">You cannot a configure a virtual network as a transit router.</span></span>
> 
> 

## <a name="selecting-the-steps-to-use"></a><span data-ttu-id="e80be-143">Selezione dei passaggi da usare</span><span class="sxs-lookup"><span data-stu-id="e80be-143">Selecting the steps to use</span></span>
<span data-ttu-id="e80be-144">Esistono due diverse serie di procedure disponibili per configurare le connessioni che possono coesistere.</span><span class="sxs-lookup"><span data-stu-id="e80be-144">There are two different sets of procedures to choose from in order to configure connections that can coexist.</span></span> <span data-ttu-id="e80be-145">La procedura di configurazione scelta dipende dalla disponibilità o meno di una rete virtuale esistente a cui stabilire la connessione oppure dall'esigenza di creare una nuova rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e80be-145">The configuration procedure that you select will depend on whether you have an existing virtual network that you want to connect to, or you want to create a new virtual network.</span></span>

* <span data-ttu-id="e80be-146">Non è disponibile una rete virtuale ed è necessario crearne una.</span><span class="sxs-lookup"><span data-stu-id="e80be-146">I don't have a VNet and need to create one.</span></span>
  
    <span data-ttu-id="e80be-147">Se non si ha ancora una rete virtuale, questa procedura consentirà la creazione di una nuova rete virtuale e di nuove connessioni ExpressRoute e VPN da sito a sito usando il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="e80be-147">If you don’t already have a virtual network, this procedure will walk you through creating a new virtual network using the classic deployment model and creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="e80be-148">Per la configurazione, eseguire i passaggi nella sezione [Per creare una nuova rete virtuale con connessioni coesistenti](#new).</span><span class="sxs-lookup"><span data-stu-id="e80be-148">To configure, follow the steps in the article section [To create a new virtual network and coexisting connections](#new).</span></span>
* <span data-ttu-id="e80be-149">È già disponibile una rete virtuale con modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="e80be-149">I already have a classic deployment model VNet.</span></span>
  
    <span data-ttu-id="e80be-150">E’ possibile che esista già una rete virtuale con una connessione VPN da sito a sito o una connessione ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e80be-150">You may already have a virtual network in place with an existing Site-to-Site VPN connection or ExpressRoute connection.</span></span> <span data-ttu-id="e80be-151">La sezione [Per configurare connessioni coesistenti per una rete virtuale esistente](#add) illustra come eliminare il gateway e quindi come creare nuove connessioni ExpressRoute e VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="e80be-151">The article section [To configure coexsiting connections for an already existing VNet](#add) will walk you through deleting the gateway, and then creating new ExpressRoute and Site-to-Site VPN connections.</span></span> <span data-ttu-id="e80be-152">Durante la creazione di nuove connessioni, è necessario completare i passaggi in un ordine molto specifico.</span><span class="sxs-lookup"><span data-stu-id="e80be-152">Note that when creating the new connections, the steps must be completed in a very specific order.</span></span> <span data-ttu-id="e80be-153">Non usare le istruzioni in altri articoli per creare gateway e connessioni.</span><span class="sxs-lookup"><span data-stu-id="e80be-153">Don't use the instructions in other articles to create your gateways and connections.</span></span>
  
    <span data-ttu-id="e80be-154">In questa procedura, la creazione di connessioni che possono coesistere richiederà l’eliminazione del gateway e la configurazione di nuovi gateway.</span><span class="sxs-lookup"><span data-stu-id="e80be-154">In this procedure, creating connections that can coexist will require you to delete your gateway, and then configure new gateways.</span></span> <span data-ttu-id="e80be-155">Mentre si elimina e si ricrea il gateway e le connessioni, si avrà un tempo di inattività per le connessioni cross-premise, ma non sarà necessario eseguire la migrazione delle macchine virtuali o dei servizi a una nuova rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e80be-155">This means you will have downtime for your cross-premises connections while you delete and recreate your gateway and connections, but you will not need to migrate any of your VMs or services to a new virtual network.</span></span> <span data-ttu-id="e80be-156">Le macchine virtuali e i servizi saranno comunque in grado di comunicare tramite il servizio di bilanciamento del carico mentre si configura il gateway, se sono configurati in questo senso.</span><span class="sxs-lookup"><span data-stu-id="e80be-156">Your VMs and services will still be able to communicate out through the load balancer while you configure your gateway if they are configured to do so.</span></span>

## <span data-ttu-id="e80be-157"><a name="new"></a>Per creare una nuova rete virtuale con connessioni coesistenti</span><span class="sxs-lookup"><span data-stu-id="e80be-157"><a name="new"></a>To create a new virtual network and coexisting connections</span></span>
<span data-ttu-id="e80be-158">Questa procedura illustra come creare una rete virtuale e connessioni da sito a sito ed ExpressRoute coesistenti.</span><span class="sxs-lookup"><span data-stu-id="e80be-158">This procedure will walk you through creating a VNet and create Site-to-Site and ExpressRoute connections that will coexist.</span></span>

1. <span data-ttu-id="e80be-159">È necessario installare l'ultima versione dei cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e80be-159">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="e80be-160">Per altre informazioni sull'installazione dei cmdlet di PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="e80be-160">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span> <span data-ttu-id="e80be-161">Si noti che i cmdlet usati per questa configurazione possono essere leggermente diversi da quelli con cui si ha familiarità.</span><span class="sxs-lookup"><span data-stu-id="e80be-161">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="e80be-162">Assicurarsi di usare i cmdlet specificati in queste istruzioni.</span><span class="sxs-lookup"><span data-stu-id="e80be-162">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="e80be-163">Creare uno schema per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e80be-163">Create a schema for your virtual network.</span></span> <span data-ttu-id="e80be-164">Per altre informazioni sullo schema di configurazione, vedere [Schema di configurazione della rete virtuale di Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="e80be-164">For more information about the configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   
    <span data-ttu-id="e80be-165">Quando si crea lo schema, assicurarsi di usare i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="e80be-165">When you create your schema, make sure you use the following values:</span></span>
   
   * <span data-ttu-id="e80be-166">La subnet del gateway per la rete virtuale deve essere /27 o un prefisso più breve (ad esempio /26 o /25).</span><span class="sxs-lookup"><span data-stu-id="e80be-166">The gateway subnet for the virtual network must be /27 or a shorter prefix (such as /26 or /25).</span></span>
   * <span data-ttu-id="e80be-167">Il tipo di connessione del gateway è "Dedicato".</span><span class="sxs-lookup"><span data-stu-id="e80be-167">The gateway connection type is "Dedicated".</span></span>
     
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
3. <span data-ttu-id="e80be-168">Dopo la creazione e configurazione del file di schema xml, caricare il file.</span><span class="sxs-lookup"><span data-stu-id="e80be-168">After creating and configuring your xml schema file, upload the file.</span></span> <span data-ttu-id="e80be-169">Verrà creata la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e80be-169">This will create your virtual network.</span></span>
   
    <span data-ttu-id="e80be-170">Usare il cmdlet seguente per caricare il file, sostituendo il valore con uno personalizzato.</span><span class="sxs-lookup"><span data-stu-id="e80be-170">Use the following cmdlet to upload your file, replacing the value with your own.</span></span>
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <span data-ttu-id="e80be-171"><a name="gw"></a>Creare un gateway ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e80be-171"><a name="gw"></a>Create an ExpressRoute gateway.</span></span> <span data-ttu-id="e80be-172">Specificare *Standard*, *HighPerformance* o *UltraPerformance* per GatewaySKU e *DynamicRouting* per GatewayType.</span><span class="sxs-lookup"><span data-stu-id="e80be-172">Be sure to specify the GatewaySKU as *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType as *DynamicRouting*.</span></span>
   
    <span data-ttu-id="e80be-173">Usare l'esempio di seguito, sostituendo i valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="e80be-173">Use the following sample, substituting the values for your own.</span></span>
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. <span data-ttu-id="e80be-174">Collegare il gateway ExpressRoute al circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e80be-174">Link the ExpressRoute gateway to the ExpressRoute circuit.</span></span> <span data-ttu-id="e80be-175">Dopo aver completato questo passaggio, viene stabilita la connessione tra la rete locale e Azure tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e80be-175">After this step has been completed, the connection between your on-premises network and Azure, through ExpressRoute, is established.</span></span>
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <span data-ttu-id="e80be-176"><a name="vpngw"></a>Creare quindi il gateway VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="e80be-176"><a name="vpngw"></a>Next, create your Site-to-Site VPN gateway.</span></span> <span data-ttu-id="e80be-177">GatewaySKU deve essere *Standard*, *HighPerformance* o *UltraPerformance* e GatewayType deve essere *DynamicRouting*.</span><span class="sxs-lookup"><span data-stu-id="e80be-177">The GatewaySKU must be *Standard*, *HighPerformance*, or *UltraPerformance* and the GatewayType must be *DynamicRouting*.</span></span>
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    <span data-ttu-id="e80be-178">Per recuperare le impostazioni del gateway di rete virtuale, inclusi l'ID del gateway e l'indirizzo IP pubblico, usare il cmdlet `Get-AzureVirtualNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="e80be-178">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span>
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for the following virtual network: GNSDesMoines
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
7. <span data-ttu-id="e80be-179">Creare un'entità gateway VPN del sito locale.</span><span class="sxs-lookup"><span data-stu-id="e80be-179">Create a local site VPN gateway entity.</span></span> <span data-ttu-id="e80be-180">Questo comando non configura il gateway VPN locale.</span><span class="sxs-lookup"><span data-stu-id="e80be-180">This command doesn’t configure your on-premises VPN gateway.</span></span> <span data-ttu-id="e80be-181">Consente invece di fornire le impostazioni del gateway locale, ad esempio l'indirizzo IP pubblico e lo spazio indirizzi locale, in modo che il gateway VPN di Azure possa connettersi.</span><span class="sxs-lookup"><span data-stu-id="e80be-181">Rather, it allows you to provide the local gateway settings, such as the public IP and the on-premises address space, so that the Azure VPN gateway can connect to it.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="e80be-182">Il sito locale per la connessione VPN da sito a sito non è definito nel file netcfg.</span><span class="sxs-lookup"><span data-stu-id="e80be-182">The local site for the Site-to-Site VPN is not defined in the netcfg.</span></span> <span data-ttu-id="e80be-183">È invece necessario usare questo cmdlet per specificare i parametri del sito locale.</span><span class="sxs-lookup"><span data-stu-id="e80be-183">Instead, you must use this cmdlet to specify the local site parameters.</span></span> <span data-ttu-id="e80be-184">Non è possibile definirlo tramite il portale o il file netcfg.</span><span class="sxs-lookup"><span data-stu-id="e80be-184">You cannot define it using either portal, or the netcfg file.</span></span>
   > 
   > 
   
    <span data-ttu-id="e80be-185">Usare l'esempio seguente, sostituendo i valori con quelli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="e80be-185">Use the following sample, replacing the values with your own.</span></span>
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > <span data-ttu-id="e80be-186">Se la rete locale include più route, è possibile passarle tutte come una matrice.</span><span class="sxs-lookup"><span data-stu-id="e80be-186">If your local network has multiple routes, you can pass them all in as an array.</span></span>  <span data-ttu-id="e80be-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span><span class="sxs-lookup"><span data-stu-id="e80be-187">$MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")</span></span>  
   > 
   > 

    <span data-ttu-id="e80be-188">Per recuperare le impostazioni del gateway di rete virtuale, inclusi l'ID del gateway e l'indirizzo IP pubblico, usare il cmdlet `Get-AzureVirtualNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="e80be-188">To retrieve the virtual network gateway settings, including the gateway ID and the public IP, use the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="e80be-189">Vedere l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="e80be-189">See the following example.</span></span>

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. <span data-ttu-id="e80be-190">Configurare il dispositivo VPN locale per la connessione al nuovo gateway.</span><span class="sxs-lookup"><span data-stu-id="e80be-190">Configure your local VPN device to connect to the new gateway.</span></span> <span data-ttu-id="e80be-191">Quando si configura il dispositivo VPN, usare le informazioni recuperate nel passaggio 6.</span><span class="sxs-lookup"><span data-stu-id="e80be-191">Use the information that you retrieved in step 6 when configuring your VPN device.</span></span> <span data-ttu-id="e80be-192">Per altre informazioni sulla configurazione del dispositivo VPN, vedere la pagina relativa alla [configurazione del dispositivo VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="e80be-192">For more information about VPN device configuration, see [VPN Device Configuration](../vpn-gateway/vpn-gateway-about-vpn-devices.md).</span></span>
2. <span data-ttu-id="e80be-193">Collegare il gateway VPN da sito a sito in Azure al gateway locale.</span><span class="sxs-lookup"><span data-stu-id="e80be-193">Link the Site-to-Site VPN gateway on Azure to the local gateway.</span></span>
   
    <span data-ttu-id="e80be-194">In questo esempio connectedEntityId è l'ID del gateway locale, che è possibile trovare eseguendo `Get-AzureLocalNetworkGateway`.</span><span class="sxs-lookup"><span data-stu-id="e80be-194">In this example, connectedEntityId is the local gateway ID, which you can find by running `Get-AzureLocalNetworkGateway`.</span></span> <span data-ttu-id="e80be-195">È possibile trovare virtualNetworkGatewayId usando il cmdlet `Get-AzureVirtualNetworkGateway` .</span><span class="sxs-lookup"><span data-stu-id="e80be-195">You can find virtualNetworkGatewayId by using the `Get-AzureVirtualNetworkGateway` cmdlet.</span></span> <span data-ttu-id="e80be-196">Dopo questo passaggio, viene stabilita la connessione tra la rete locale e Azure tramite la connessione VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="e80be-196">After this step, the connection between your local network and Azure via the Site-to-Site VPN connection is established.</span></span>

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <span data-ttu-id="e80be-197"><a name="add"></a>Per configurare connessioni coesistenti per una rete virtuale esistente</span><span class="sxs-lookup"><span data-stu-id="e80be-197"><a name="add"></a>To configure coexsiting connections for an already existing VNet</span></span>
<span data-ttu-id="e80be-198">Se esiste già una rete virtuale, controllare le dimensioni della subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="e80be-198">If you have an existing virtual network, check the gateway subnet size.</span></span> <span data-ttu-id="e80be-199">Se la subnet del gateway è pari a/29 o /28, è necessario eliminare prima di tutto il gateway di rete virtuale e aumentare le dimensioni della subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="e80be-199">If the gateway subnet is /28 or /29, you must first delete the virtual network gateway and increase the gateway subnet size.</span></span> <span data-ttu-id="e80be-200">I passaggi descritti in questa sezione illustrano come eseguire questa operazione.</span><span class="sxs-lookup"><span data-stu-id="e80be-200">The steps in this section will show you how to do that.</span></span>

<span data-ttu-id="e80be-201">Se la subnet del gateway è /27 o superiore e la rete virtuale è connessa tramite ExpressRoute, è possibile ignorare i passaggi seguenti e andare al ["Passaggio 6: Creare un gateway VPN da sito a sito"](#vpngw) nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="e80be-201">If the gateway subnet is /27 or larger and the virtual network is connected via ExpressRoute, you can skip the steps below and proceed to ["Step 6 - Create a Site-to-Site VPN gateway"](#vpngw) in the previous section.</span></span>

> [!NOTE]
> <span data-ttu-id="e80be-202">Quando si elimina il gateway esistente, gli ambienti locali perderanno la connessione alla rete virtuale mentre si lavora a questa configurazione.</span><span class="sxs-lookup"><span data-stu-id="e80be-202">When you delete the existing gateway, your local premises will lose the connection to your virtual network while you are working on this configuration.</span></span>
> 
> 

1. <span data-ttu-id="e80be-203">È necessario installare la versione più recente dei cmdlet di PowerShell per Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="e80be-203">You'll need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="e80be-204">Per altre informazioni sull'installazione dei cmdlet di PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="e80be-204">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span> <span data-ttu-id="e80be-205">Si noti che i cmdlet usati per questa configurazione possono essere leggermente diversi da quelli con cui si ha familiarità.</span><span class="sxs-lookup"><span data-stu-id="e80be-205">Note that the cmdlets that you'll use for this configuration may be slightly different than what you might be familiar with.</span></span> <span data-ttu-id="e80be-206">Assicurarsi di usare i cmdlet specificati in queste istruzioni.</span><span class="sxs-lookup"><span data-stu-id="e80be-206">Be sure to use the cmdlets specified in these instructions.</span></span> 
2. <span data-ttu-id="e80be-207">Eliminare il gateway ExpressRoute o VPN da sito a sito esistente.</span><span class="sxs-lookup"><span data-stu-id="e80be-207">Delete the existing ExpressRoute or Site-to-Site VPN gateway.</span></span> <span data-ttu-id="e80be-208">Usare il cmdlet seguente, sostituendo i valori con quelli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="e80be-208">Use the following cmdlet, replacing the values with your own.</span></span>
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. <span data-ttu-id="e80be-209">Esportare lo schema della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e80be-209">Export the virtual network schema.</span></span> <span data-ttu-id="e80be-210">Usare il cmdlet PowerShell seguente, sostituendo i valori con quelli personalizzati.</span><span class="sxs-lookup"><span data-stu-id="e80be-210">Use the following PowerShell cmdlet, replacing the values with your own.</span></span>
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. <span data-ttu-id="e80be-211">Modificare lo schema del file di configurazione di rete in modo che la subnet del gateway sia /27 o un prefisso più breve (ad esempio /26 o /25).</span><span class="sxs-lookup"><span data-stu-id="e80be-211">Edit the network configuration file schema so that the gateway subnet is /27 or a shorter prefix (such as /26 or /25).</span></span> <span data-ttu-id="e80be-212">Vedere l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="e80be-212">See the following example.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e80be-213">Se non sono rimasti indirizzi IP sufficienti nella rete virtuale per aumentare le dimensioni della subnet del gateway, è necessario aggiungere altro spazio di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="e80be-213">If you don't have enough IP addresses left in your virtual network to increase the gateway subnet size, you need to add more IP address space.</span></span> <span data-ttu-id="e80be-214">Per altre informazioni sullo schema di configurazione, vedere [Schema di configurazione della rete virtuale di Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="e80be-214">For more information about the configuration schema, see [Azure Virtual Network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. <span data-ttu-id="e80be-215">Se il gateway precedente era una VPN da sito a sito, è necessario modificare anche il tipo di connessione su **Dedicato**.</span><span class="sxs-lookup"><span data-stu-id="e80be-215">If your previous gateway was a Site-to-Site VPN, you must also change the connection type to **Dedicated**.</span></span>
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. <span data-ttu-id="e80be-216">A questo punto, si avrà una rete virtuale senza gateway.</span><span class="sxs-lookup"><span data-stu-id="e80be-216">At this point, you'll have a VNet with no gateways.</span></span> <span data-ttu-id="e80be-217">Per creare nuovi gateway e completare le connessioni, è possibile procedere con il [Passaggio 4: Creare un gateway ExpressRoute](#gw), disponibile nel set di passaggi precedente.</span><span class="sxs-lookup"><span data-stu-id="e80be-217">To create new gateways and complete your connections, you can proceed with [Step 4 - Create an ExpressRoute gateway](#gw), found in the preceding set of steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e80be-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e80be-218">Next steps</span></span>
<span data-ttu-id="e80be-219">Per altre informazioni su ExpressRoute, vedere le [Domande frequenti su ExpressRoute](expressroute-faqs.md)</span><span class="sxs-lookup"><span data-stu-id="e80be-219">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md)</span></span>

