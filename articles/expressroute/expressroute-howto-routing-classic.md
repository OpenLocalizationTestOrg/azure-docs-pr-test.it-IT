---
title: 'Come tooconfigure routing (peering) per un circuito ExpressRoute: Azure: classico | Documenti Microsoft'
description: In questo articolo vengono illustrati i passaggi hello per la creazione e il provisioning di hello privato, pubblico e peering Microsoft di un circuito ExpressRoute. Mostra anche come stato hello toocheck, aggiornamento o eliminazione di peering per il circuito.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="33dcf-104">Creare e modificare il peering per un circuito ExpressRoute (versione classica)</span><span class="sxs-lookup"><span data-stu-id="33dcf-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="33dcf-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="33dcf-105">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="33dcf-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="33dcf-106">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="33dcf-107">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="33dcf-107">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="33dcf-108">Video - Peering privato</span><span class="sxs-lookup"><span data-stu-id="33dcf-108">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="33dcf-109">Video - Peering pubblico</span><span class="sxs-lookup"><span data-stu-id="33dcf-109">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="33dcf-110">Video - Peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="33dcf-110">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="33dcf-111">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="33dcf-111">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="33dcf-112">In questo articolo illustra toocreate passaggi hello e gestire la configurazione di routing per un circuito ExpressRoute con PowerShell e hello modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="33dcf-112">This article walks you through hello steps toocreate and manage routing configuration for an ExpressRoute circuit using PowerShell and hello classic deployment model.</span></span> <span data-ttu-id="33dcf-113">passaggi di Hello riportati di seguito verranno inoltre Visualizza come stato hello toocheck, aggiornare, o eliminare e il deprovisioning di peering per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="33dcf-113">hello steps below will also show you how toocheck hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="33dcf-114">**Informazioni sui modelli di distribuzione di Azure**</span><span class="sxs-lookup"><span data-stu-id="33dcf-114">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a><span data-ttu-id="33dcf-115">Prerequisiti di configurazione</span><span class="sxs-lookup"><span data-stu-id="33dcf-115">Configuration prerequisites</span></span>
* <span data-ttu-id="33dcf-116">Sarà necessario hello versione hello cmdlet PowerShell di gestione del servizio di Azure (SM).</span><span class="sxs-lookup"><span data-stu-id="33dcf-116">You will need hello latest version of hello Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="33dcf-117">Per altre informazioni, vedere [Introduzione ai cmdlet di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="33dcf-117">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="33dcf-118">Assicurarsi di aver esaminato hello [prerequisiti](expressroute-prerequisites.md) pagina hello [requisiti di routing](expressroute-routing.md) pagina e hello [flussi di lavoro](expressroute-workflows.md) pagina prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="33dcf-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="33dcf-119">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="33dcf-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="33dcf-120">Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-classic.md) e circuito hello abilitato dal provider di connettività prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="33dcf-120">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="33dcf-121">Hello circuito ExpressRoute deve essere in uno stato di provisioning e abilitato per l'utente toobe toorun in grado di hello cmdlet descritti di seguito.</span><span class="sxs-lookup"><span data-stu-id="33dcf-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets described below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="33dcf-122">Queste istruzioni si applicano solo toocircuits creato con il provider di servizi che offre servizi di connettività di livello 2.</span><span class="sxs-lookup"><span data-stu-id="33dcf-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="33dcf-123">Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito un IPVPN, come MPLS), il provider di connettività configurerà e gestirà il routing per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="33dcf-123">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

<span data-ttu-id="33dcf-124">Per un circuito ExpressRoute è possibile configurare uno, due o tutti e tre i peering (peering privato di Azure, peering pubblico di Azure e peering Microsoft).</span><span class="sxs-lookup"><span data-stu-id="33dcf-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="33dcf-125">È possibile configurare i peering nell'ordine desiderato.</span><span class="sxs-lookup"><span data-stu-id="33dcf-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="33dcf-126">Tuttavia, è necessario assicurarsi completare hello configurazione di ogni peer uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="33dcf-126">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span>


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a><span data-ttu-id="33dcf-127">Accedi tooyour account Azure e selezionare una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="33dcf-127">Log in tooyour Azure account and select a subscription</span></span>
1. <span data-ttu-id="33dcf-128">Aprire la console di PowerShell con diritti elevati e tooyour account di connessione.</span><span class="sxs-lookup"><span data-stu-id="33dcf-128">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="33dcf-129">Utilizzare hello toohelp esempio che ci si connette seguenti:</span><span class="sxs-lookup"><span data-stu-id="33dcf-129">Use hello following example toohelp you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="33dcf-130">Controllare le sottoscrizioni di hello per account hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-130">Check hello subscriptions for hello account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="33dcf-131">Se si dispone di più di una sottoscrizione, selezionare una sottoscrizione di hello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="33dcf-131">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="33dcf-132">Successivamente, utilizzare hello seguente cmdlet tooadd tooPowerShell la sottoscrizione di Azure per il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-132">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="33dcf-133">Peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="33dcf-133">Azure private peering</span></span>
<span data-ttu-id="33dcf-134">In questa sezione vengono fornite istruzioni su come toocreate, ottenere, aggiornare ed eliminare hello Azure configurazione peering privata per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="33dcf-134">This section provides instructions on how toocreate, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="33dcf-135">toocreate peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="33dcf-135">toocreate Azure private peering</span></span>
1. <span data-ttu-id="33dcf-136">**Importare il modulo di PowerShell hello per ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="33dcf-136">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="33dcf-137">È necessario importare i moduli di Azure ed ExpressRoute hello nella sessione di PowerShell hello in toostart ordine utilizzando i cmdlet di ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-137">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="33dcf-138">I moduli di Azure ed ExpressRoute hello tooimport di comandi seguenti di hello esecuzione nella sessione di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-138">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="33dcf-139">**Creare un circuito ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="33dcf-139">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="33dcf-140">Seguire hello istruzioni toocreate un [circuito ExpressRoute](expressroute-howto-circuit-classic.md) e fare in modo fornito dal provider di connettività hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-140">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="33dcf-141">Se il provider di connettività offre servizi di livello 3 gestiti, è possibile richiedere il tooenable provider di connettività privata peering per l'utente di Azure.</span><span class="sxs-lookup"><span data-stu-id="33dcf-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="33dcf-142">In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-142">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="33dcf-143">Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, istruzioni hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="33dcf-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span> 
3. <span data-ttu-id="33dcf-144">**Controllare tooensure circuito ExpressRoute di hello che è disponibile.**</span><span class="sxs-lookup"><span data-stu-id="33dcf-144">**Check hello ExpressRoute circuit tooensure it is provisioned.**</span></span>
   
    <span data-ttu-id="33dcf-145">È innanzitutto necessario archiviare toosee se hello circuito ExpressRoute è stato eseguito il provisioning e inoltre abilitato.</span><span class="sxs-lookup"><span data-stu-id="33dcf-145">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="33dcf-146">Vedere l'esempio hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="33dcf-146">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="33dcf-147">Assicurarsi che il circuito hello viene illustrato come provisioning eseguito e abilitato.</span><span class="sxs-lookup"><span data-stu-id="33dcf-147">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="33dcf-148">In caso contrario, utilizzare il tooget di provider di connettività del circuito toohello necessarie sullo stato di e.</span><span class="sxs-lookup"><span data-stu-id="33dcf-148">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="33dcf-149">**Configurare peering privato di Azure per il circuito hello.**</span><span class="sxs-lookup"><span data-stu-id="33dcf-149">**Configure Azure private peering for hello circuit.**</span></span>
   
    <span data-ttu-id="33dcf-150">Assicurarsi di disporre delle seguenti prima di procedere con passaggi successivi hello hello:</span><span class="sxs-lookup"><span data-stu-id="33dcf-150">Make sure that you have hello following items before you proceed with hello next steps:</span></span>
   
   * <span data-ttu-id="33dcf-151">/ 30 subnet per collegamento primario hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-151">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="33dcf-152">Non deve far parte di alcuno spazio indirizzi riservato per le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="33dcf-152">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="33dcf-153">/ 30 subnet per collegamento secondario hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-153">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="33dcf-154">Non deve far parte di alcuno spazio indirizzi riservato per le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="33dcf-154">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="33dcf-155">Un esempio di ID VLAN valido tooestablish il peer.</span><span class="sxs-lookup"><span data-stu-id="33dcf-155">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="33dcf-156">Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="33dcf-156">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="33dcf-157">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="33dcf-157">AS number for peering.</span></span> <span data-ttu-id="33dcf-158">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="33dcf-158">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="33dcf-159">È possibile usare il numero AS privato per questo peering.</span><span class="sxs-lookup"><span data-stu-id="33dcf-159">You can use a private AS number for this peering.</span></span> <span data-ttu-id="33dcf-160">Assicurarsi di non usare il numero 65515.</span><span class="sxs-lookup"><span data-stu-id="33dcf-160">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="33dcf-161">Hash MD5 se si sceglie toouse uno.</span><span class="sxs-lookup"><span data-stu-id="33dcf-161">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="33dcf-162">**Facoltativo**.</span><span class="sxs-lookup"><span data-stu-id="33dcf-162">**This is optional**.</span></span>
     
    <span data-ttu-id="33dcf-163">È possibile eseguire hello seguente tooconfigure cmdlet peering privato di Azure per il circuito.</span><span class="sxs-lookup"><span data-stu-id="33dcf-163">You can run hello following cmdlet tooconfigure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="33dcf-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span><span class="sxs-lookup"><span data-stu-id="33dcf-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="33dcf-165">È possibile utilizzare i cmdlet di hello riportato di seguito se si sceglie toouse un hash MD5.</span><span class="sxs-lookup"><span data-stu-id="33dcf-165">You can use hello cmdlet below if you choose toouse an MD5 hash.</span></span>
     
        <span data-ttu-id="33dcf-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="33dcf-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="33dcf-167">Assicurarsi di specificare il numero AS come ASN di peering e non come ASN cliente.</span><span class="sxs-lookup"><span data-stu-id="33dcf-167">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="33dcf-168">tooview dettagli di peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="33dcf-168">tooview Azure private peering details</span></span>
<span data-ttu-id="33dcf-169">È possibile ottenere i dettagli di configurazione mediante hello seguenti cmdlet</span><span class="sxs-lookup"><span data-stu-id="33dcf-169">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="33dcf-170">configurazione di peering privato Azure tooupdate</span><span class="sxs-lookup"><span data-stu-id="33dcf-170">tooupdate Azure private peering configuration</span></span>
<span data-ttu-id="33dcf-171">È possibile aggiornare qualsiasi parte della configurazione di hello utilizzando hello cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="33dcf-171">You can update any part of hello configuration using hello following cmdlet.</span></span> <span data-ttu-id="33dcf-172">Nel seguente esempio hello hello ID VLAN del circuito hello viene aggiornato da too500 100.</span><span class="sxs-lookup"><span data-stu-id="33dcf-172">In hello example below, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="33dcf-173">toodelete peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="33dcf-173">toodelete Azure private peering</span></span>
<span data-ttu-id="33dcf-174">È possibile rimuovere la configurazione di peering eseguendo hello cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="33dcf-174">You can remove your peering configuration by running hello following cmdlet.</span></span>

> [!WARNING]
> <span data-ttu-id="33dcf-175">È necessario assicurarsi che tutte le reti virtuali vengono scollegate dal hello circuito ExpressRoute prima di eseguire questo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="33dcf-175">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this cmdlet.</span></span> 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="33dcf-176">Peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="33dcf-176">Azure public peering</span></span>
<span data-ttu-id="33dcf-177">In questa sezione vengono fornite istruzioni su come toocreate, ottenere, aggiornare ed eliminare hello Azure configurazione di peering pubblico per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="33dcf-177">This section provides instructions on how toocreate, get, update and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="33dcf-178">toocreate peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="33dcf-178">toocreate Azure public peering</span></span>
1. <span data-ttu-id="33dcf-179">**Importare il modulo di PowerShell hello per ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="33dcf-179">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="33dcf-180">È necessario importare i moduli di Azure ed ExpressRoute hello nella sessione di PowerShell hello in toostart ordine utilizzando i cmdlet di ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-180">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="33dcf-181">I moduli di Azure ed ExpressRoute hello tooimport di comandi seguenti di hello esecuzione nella sessione di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-181">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="33dcf-182">**Creare un circuito ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="33dcf-182">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="33dcf-183">Seguire hello istruzioni toocreate un [circuito ExpressRoute](expressroute-howto-circuit-classic.md) e fare in modo fornito dal provider di connettività hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="33dcf-184">Se il provider di connettività offre servizi di livello 3 gestiti, è possibile richiedere il tooenable provider di connettività pubblici di peering per l'utente di Azure.</span><span class="sxs-lookup"><span data-stu-id="33dcf-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure public peering for you.</span></span> <span data-ttu-id="33dcf-185">In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="33dcf-186">Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, istruzioni hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="33dcf-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="33dcf-187">**Tooensure circuito ExpressRoute di controllo che è disponibile**</span><span class="sxs-lookup"><span data-stu-id="33dcf-187">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="33dcf-188">È innanzitutto necessario archiviare toosee se hello circuito ExpressRoute è stato eseguito il provisioning e inoltre abilitato.</span><span class="sxs-lookup"><span data-stu-id="33dcf-188">You must first check toosee if hello ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="33dcf-189">Vedere l'esempio hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="33dcf-189">See hello example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="33dcf-190">Assicurarsi che il circuito hello viene illustrato come provisioning eseguito e abilitato.</span><span class="sxs-lookup"><span data-stu-id="33dcf-190">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="33dcf-191">In caso contrario, utilizzare il tooget di provider di connettività del circuito toohello necessarie sullo stato di e.</span><span class="sxs-lookup"><span data-stu-id="33dcf-191">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="33dcf-192">**Configurare peering pubblico di Azure per il circuito hello**</span><span class="sxs-lookup"><span data-stu-id="33dcf-192">**Configure Azure public peering for hello circuit**</span></span>
   
    <span data-ttu-id="33dcf-193">Verificare di disporre di hello le seguenti informazioni prima di procedere ulteriormente.</span><span class="sxs-lookup"><span data-stu-id="33dcf-193">Ensure that you have hello following information before you proceed further.</span></span>
   
   * <span data-ttu-id="33dcf-194">/ 30 subnet per collegamento primario hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-194">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="33dcf-195">Deve essere un prefisso IPv4 pubblico valido.</span><span class="sxs-lookup"><span data-stu-id="33dcf-195">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="33dcf-196">/ 30 subnet per collegamento secondario hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-196">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="33dcf-197">Deve essere un prefisso IPv4 pubblico valido.</span><span class="sxs-lookup"><span data-stu-id="33dcf-197">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="33dcf-198">Un esempio di ID VLAN valido tooestablish il peer.</span><span class="sxs-lookup"><span data-stu-id="33dcf-198">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="33dcf-199">Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="33dcf-199">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="33dcf-200">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="33dcf-200">AS number for peering.</span></span> <span data-ttu-id="33dcf-201">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="33dcf-201">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="33dcf-202">Hash MD5 se si sceglie toouse uno.</span><span class="sxs-lookup"><span data-stu-id="33dcf-202">An MD5 hash if you choose toouse one.</span></span> <span data-ttu-id="33dcf-203">**Facoltativo**.</span><span class="sxs-lookup"><span data-stu-id="33dcf-203">**This is optional**.</span></span>
     
    <span data-ttu-id="33dcf-204">È possibile eseguire i seguenti cmdlet tooconfigure peering pubblico di Azure per il circuito hello</span><span class="sxs-lookup"><span data-stu-id="33dcf-204">You can run hello following cmdlet tooconfigure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="33dcf-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span><span class="sxs-lookup"><span data-stu-id="33dcf-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="33dcf-206">È possibile utilizzare i cmdlet di hello riportato di seguito se si sceglie toouse un hash MD5</span><span class="sxs-lookup"><span data-stu-id="33dcf-206">You can use hello cmdlet below if you choose toouse an MD5 hash</span></span>
     
        <span data-ttu-id="33dcf-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="33dcf-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="33dcf-208">Assicurarsi di specificare il numero AS come ASN di peering e non come ASN cliente.</span><span class="sxs-lookup"><span data-stu-id="33dcf-208">Ensure that you specify your AS number as peering ASN and not customer ASN.</span></span>
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="33dcf-209">tooview dettagli di peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="33dcf-209">tooview Azure public peering details</span></span>
<span data-ttu-id="33dcf-210">È possibile ottenere i dettagli di configurazione mediante hello seguenti cmdlet</span><span class="sxs-lookup"><span data-stu-id="33dcf-210">You can get configuration details using hello following cmdlet</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="33dcf-211">configurazione di peering pubblico Azure tooupdate</span><span class="sxs-lookup"><span data-stu-id="33dcf-211">tooupdate Azure public peering configuration</span></span>
<span data-ttu-id="33dcf-212">È possibile aggiornare qualsiasi parte della configurazione di hello utilizzando hello seguenti cmdlet</span><span class="sxs-lookup"><span data-stu-id="33dcf-212">You can update any part of hello configuration using hello following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="33dcf-213">ID VLAN del circuito hello Hello viene aggiornato da 200 too600 in hello sopra riportato.</span><span class="sxs-lookup"><span data-stu-id="33dcf-213">hello VLAN ID of hello circuit is being updated from 200 too600 in hello above example.</span></span>

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="33dcf-214">toodelete peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="33dcf-214">toodelete Azure public peering</span></span>
<span data-ttu-id="33dcf-215">È possibile rimuovere la configurazione di peering eseguendo i seguenti cmdlet hello</span><span class="sxs-lookup"><span data-stu-id="33dcf-215">You can remove your peering configuration by running hello following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="33dcf-216">Peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="33dcf-216">Microsoft peering</span></span>
<span data-ttu-id="33dcf-217">In questa sezione vengono fornite istruzioni su come toocreate, ottenere, aggiornare ed eliminare le configurazioni di peering Microsoft hello per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="33dcf-217">This section provides instructions on how toocreate, get, update and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="33dcf-218">toocreate peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="33dcf-218">toocreate Microsoft peering</span></span>
1. <span data-ttu-id="33dcf-219">**Importare il modulo di PowerShell hello per ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="33dcf-219">**Import hello PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="33dcf-220">È necessario importare i moduli di Azure ed ExpressRoute hello nella sessione di PowerShell hello in toostart ordine utilizzando i cmdlet di ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-220">You must import hello Azure and ExpressRoute modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="33dcf-221">I moduli di Azure ed ExpressRoute hello tooimport di comandi seguenti di hello esecuzione nella sessione di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-221">Run hello following commands tooimport hello Azure and ExpressRoute modules into hello PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="33dcf-222">**Creare un circuito ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="33dcf-222">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="33dcf-223">Seguire hello istruzioni toocreate un [circuito ExpressRoute](expressroute-howto-circuit-classic.md) e fare in modo fornito dal provider di connettività hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-223">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by hello connectivity provider.</span></span> <span data-ttu-id="33dcf-224">Se il provider di connettività offre servizi di livello 3 gestiti, è possibile richiedere il tooenable provider di connettività privata peering per l'utente di Azure.</span><span class="sxs-lookup"><span data-stu-id="33dcf-224">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="33dcf-225">In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-225">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="33dcf-226">Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, istruzioni hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="33dcf-226">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow hello instructions below.</span></span>
3. <span data-ttu-id="33dcf-227">**Tooensure circuito ExpressRoute di controllo che è disponibile**</span><span class="sxs-lookup"><span data-stu-id="33dcf-227">**Check ExpressRoute circuit tooensure it is provisioned**</span></span>
   
    <span data-ttu-id="33dcf-228">È innanzitutto necessario archiviare toosee se hello circuito ExpressRoute è in stato di provisioning eseguito e abilitato.</span><span class="sxs-lookup"><span data-stu-id="33dcf-228">You must first check toosee if hello ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="33dcf-229">Assicurarsi che il circuito hello viene illustrato come provisioning eseguito e abilitato.</span><span class="sxs-lookup"><span data-stu-id="33dcf-229">Make sure that hello circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="33dcf-230">In caso contrario, utilizzare il tooget di provider di connettività del circuito toohello necessarie sullo stato di e.</span><span class="sxs-lookup"><span data-stu-id="33dcf-230">If it doesn't, work with your connectivity provider tooget your circuit toohello required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="33dcf-231">**Configurare Microsoft peering per il circuito hello**</span><span class="sxs-lookup"><span data-stu-id="33dcf-231">**Configure Microsoft peering for hello circuit**</span></span>
   
    <span data-ttu-id="33dcf-232">Assicurarsi di aver hello le seguenti informazioni prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="33dcf-232">Make sure that you have hello following information before you proceed.</span></span>
   
   * <span data-ttu-id="33dcf-233">/ 30 subnet per collegamento primario hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-233">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="33dcf-234">Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.</span><span class="sxs-lookup"><span data-stu-id="33dcf-234">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="33dcf-235">/ 30 subnet per collegamento secondario hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-235">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="33dcf-236">Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.</span><span class="sxs-lookup"><span data-stu-id="33dcf-236">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="33dcf-237">Un esempio di ID VLAN valido tooestablish il peer.</span><span class="sxs-lookup"><span data-stu-id="33dcf-237">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="33dcf-238">Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="33dcf-238">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
   * <span data-ttu-id="33dcf-239">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="33dcf-239">AS number for peering.</span></span> <span data-ttu-id="33dcf-240">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="33dcf-240">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="33dcf-241">I prefissi annunciati: È necessario fornire un elenco di tutti i prefissi Prevedi tooadvertise sessione BGP hello.</span><span class="sxs-lookup"><span data-stu-id="33dcf-241">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="33dcf-242">Sono accettati solo prefissi di indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="33dcf-242">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="33dcf-243">Se si prevede un set di prefissi toosend, è possibile inviare un elenco separato da virgole.</span><span class="sxs-lookup"><span data-stu-id="33dcf-243">You can send a comma separated list if you plan toosend a set of prefixes.</span></span> <span data-ttu-id="33dcf-244">I prefissi devono essere registrati tooyou in un RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="33dcf-244">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
   * <span data-ttu-id="33dcf-245">Cliente ASN: Se si desidera annunciare prefissi che non sono registrato toohello peering sotto forma di numero, è possibile specificare hello come numero toowhich che sono registrati.</span><span class="sxs-lookup"><span data-stu-id="33dcf-245">Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span> <span data-ttu-id="33dcf-246">**Facoltativo**.</span><span class="sxs-lookup"><span data-stu-id="33dcf-246">**This is optional**.</span></span>
   * <span data-ttu-id="33dcf-247">Nome del Registro di sistema di routing: È possibile specificare hello RIR / IRR contro cui hello come numero e i prefissi sono registrati.</span><span class="sxs-lookup"><span data-stu-id="33dcf-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="33dcf-248">Hash MD5, se si sceglie toouse uno.</span><span class="sxs-lookup"><span data-stu-id="33dcf-248">An MD5 hash, if you choose toouse one.</span></span> <span data-ttu-id="33dcf-249">**Facoltativo.**</span><span class="sxs-lookup"><span data-stu-id="33dcf-249">**This is optional.**</span></span>
     
    <span data-ttu-id="33dcf-250">È possibile eseguire hello seguente pering Microsoft tooconfigure di cmdlet per il circuito</span><span class="sxs-lookup"><span data-stu-id="33dcf-250">You can run hello following cmdlet tooconfigure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="33dcf-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="33dcf-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="tooview-microsoft-peering-details"></a><span data-ttu-id="33dcf-252">dettagli di peering Microsoft tooview</span><span class="sxs-lookup"><span data-stu-id="33dcf-252">tooview Microsoft peering details</span></span>
<span data-ttu-id="33dcf-253">È possibile ottenere i dettagli di configurazione mediante hello cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="33dcf-253">You can get configuration details using hello following cmdlet.</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="33dcf-254">configurazione di peering Microsoft tooupdate</span><span class="sxs-lookup"><span data-stu-id="33dcf-254">tooupdate Microsoft peering configuration</span></span>
<span data-ttu-id="33dcf-255">È possibile aggiornare qualsiasi parte della configurazione di hello utilizzando hello cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="33dcf-255">You can update any part of hello configuration using hello following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="33dcf-256">toodelete peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="33dcf-256">toodelete Microsoft peering</span></span>
<span data-ttu-id="33dcf-257">È possibile rimuovere la configurazione di peering eseguendo hello cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="33dcf-257">You can remove your peering configuration by running hello following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="33dcf-258">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33dcf-258">Next steps</span></span>
<span data-ttu-id="33dcf-259">Successivamente, [collegare un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-classic.md).</span><span class="sxs-lookup"><span data-stu-id="33dcf-259">Next, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="33dcf-260">Per ulteriori informazioni sui flussi di lavoro, vedere [Flussi di lavoro ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="33dcf-260">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="33dcf-261">Per altre informazioni sul peering del circuito, vedere l'articolo relativo ai [circuiti ExpressRoute e domini di routing](expressroute-circuit-peerings.md)</span><span class="sxs-lookup"><span data-stu-id="33dcf-261">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>

