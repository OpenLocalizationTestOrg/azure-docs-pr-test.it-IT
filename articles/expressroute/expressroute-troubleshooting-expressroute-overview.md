---
title: "Verifica della connettività: guida alla risoluzione dei problemi di Azure ExpressRoute | Microsoft Docs"
description: "Questa pagina vengono fornite istruzioni sulla risoluzione dei problemi e convalida della connettività tooend fine di un circuito ExpressRoute."
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="5a87e-103">Verifica della connettività di ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="5a87e-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="5a87e-104">ExpressRoute, che estende una rete locale nel cloud di Microsoft hello su una connessione privata mediante un provider di connettività, prevede hello seguenti tre aree di rete distinti:</span><span class="sxs-lookup"><span data-stu-id="5a87e-104">ExpressRoute, which extends an on-premises network into hello Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves hello following three distinct network zones:</span></span>

-   <span data-ttu-id="5a87e-105">Rete del cliente</span><span class="sxs-lookup"><span data-stu-id="5a87e-105">Customer Network</span></span>
-   <span data-ttu-id="5a87e-106">Rete del provider</span><span class="sxs-lookup"><span data-stu-id="5a87e-106">Provider Network</span></span>
-   <span data-ttu-id="5a87e-107">Datacenter Microsoft</span><span class="sxs-lookup"><span data-stu-id="5a87e-107">Microsoft Datacenter</span></span>

<span data-ttu-id="5a87e-108">scopo di Hello di questo documento è toohelp utente tooidentify dove (o anche se) esiste un problema di connettività e all'interno della zona, che in tal modo tooseek Guida dal problema di hello tooresolve team appropriato.</span><span class="sxs-lookup"><span data-stu-id="5a87e-108">hello purpose of this document is toohelp user tooidentify where (or even if) a connectivity issue exists and within which zone, thereby tooseek help from appropriate team tooresolve hello issue.</span></span> <span data-ttu-id="5a87e-109">Se il supporto tecnico Microsoft è necessario tooresolve un problema, aprire un ticket di supporto con [supporto Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="5a87e-109">If Microsoft support is needed tooresolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a87e-110">Questo documento è previsto toohelp la diagnosi e la risoluzione dei problemi di tipo semplici.</span><span class="sxs-lookup"><span data-stu-id="5a87e-110">This document is intended toohelp diagnosing and fixing simple issues.</span></span> <span data-ttu-id="5a87e-111">Non è previsto toobe una sostituzione per il supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5a87e-111">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="5a87e-112">Aprire un ticket di supporto con [supporto Microsoft] [ Support] in caso di problema hello toosolve Impossibile utilizzando istruzioni hello disponibili.</span><span class="sxs-lookup"><span data-stu-id="5a87e-112">Open a support ticket with [Microsoft Support][Support] if you are unable toosolve hello problem using hello guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="5a87e-113">Panoramica</span><span class="sxs-lookup"><span data-stu-id="5a87e-113">Overview</span></span>
<span data-ttu-id="5a87e-114">Hello diagramma seguente mostra la connettività logico hello di una rete di tooMicrosoft cliente tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5a87e-114">hello following diagram shows hello logical connectivity of a customer network tooMicrosoft network using ExpressRoute.</span></span>
<span data-ttu-id="5a87e-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="5a87e-115">[![1]][1]</span></span>

<span data-ttu-id="5a87e-116">Nel precedente diagramma di hello, hello numeri indicano i punti chiave di rete.</span><span class="sxs-lookup"><span data-stu-id="5a87e-116">In hello preceding diagram, hello numbers indicate key network points.</span></span> <span data-ttu-id="5a87e-117">punti di rete Hello fa riferimento spesso questo articolo il numero associato.</span><span class="sxs-lookup"><span data-stu-id="5a87e-117">hello network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="5a87e-118">A seconda della connettività di ExpressRoute hello modello (Cloud Exchange condivisione percorso, connessione Ethernet o Any per qualsiasi (IPVPN)) hello rete punti 3 e 4 potrebbero essere switch (dispositivi di livello 2).</span><span class="sxs-lookup"><span data-stu-id="5a87e-118">Depending on hello ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) hello network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="5a87e-119">di seguito sono riportati i punti chiave di rete Hello illustrati:</span><span class="sxs-lookup"><span data-stu-id="5a87e-119">hello key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="5a87e-120">Dispositivo di calcolo del cliente (ad esempio, un server o un PC)</span><span class="sxs-lookup"><span data-stu-id="5a87e-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="5a87e-121">CE: router perimetrali del cliente</span><span class="sxs-lookup"><span data-stu-id="5a87e-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="5a87e-122">PE (rivolti verso i CE): router/switch perimetrali del provider rivolti verso i router perimetrali del cliente.</span><span class="sxs-lookup"><span data-stu-id="5a87e-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="5a87e-123">Cui tooas PE CEs in questo documento.</span><span class="sxs-lookup"><span data-stu-id="5a87e-123">Referred tooas PE-CEs in this document.</span></span>
4.  <span data-ttu-id="5a87e-124">PE (rivolti verso gli MSEE): router/switch perimetrali del provider rivolti verso gli MSEE.</span><span class="sxs-lookup"><span data-stu-id="5a87e-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="5a87e-125">Cui tooas PE MSEEs in questo documento.</span><span class="sxs-lookup"><span data-stu-id="5a87e-125">Referred tooas PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="5a87e-126">MSEE: router ExpressRoute Microsoft Enterprise Edge (MSEE)</span><span class="sxs-lookup"><span data-stu-id="5a87e-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="5a87e-127">Gateway di rete virtuale (VNet)</span><span class="sxs-lookup"><span data-stu-id="5a87e-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="5a87e-128">Dispositivo di rete virtuale di Azure hello di calcolo</span><span class="sxs-lookup"><span data-stu-id="5a87e-128">Compute device on hello Azure VNet</span></span>

<span data-ttu-id="5a87e-129">Se si utilizzano i modelli di connettività Cloud Exchange condivisione percorso o connessione Ethernet hello, router perimetrale del cliente hello (2) si possa stabilire BGP peering con MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="5a87e-129">If hello Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, hello customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="5a87e-130">I punti 3 e 4 sono ancora presenti, ma in forma trasparente, come dispositivi di livello 2.</span><span class="sxs-lookup"><span data-stu-id="5a87e-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="5a87e-131">Se si utilizza modello di integrazione applicativa hello Any per qualsiasi (IPVPN), hello PEs (con connessione MSEE) (4) si possa stabilire BGP peering con MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="5a87e-131">If hello Any-to-any (IPVPN) connectivity model is used, hello PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="5a87e-132">Le route propagherebbe quindi rete cliente toohello indietro tramite una rete hello IPVPN service provider.</span><span class="sxs-lookup"><span data-stu-id="5a87e-132">Routes would then propagate back toohello customer network via hello IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="5a87e-133">Per la disponibilità elevata di ExpressRoute, Microsoft richiede una coppia ridondante di sessioni BGP tra MSEE (5) e PE-MSEE (4).</span><span class="sxs-lookup"><span data-stu-id="5a87e-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="5a87e-134">Si consiglia anche una coppia ridondante di percorsi di rete tra rete del cliente e PE-CE.</span><span class="sxs-lookup"><span data-stu-id="5a87e-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="5a87e-135">Nel modello (IPVPN) Any per qualsiasi connessione, tuttavia, un singolo dispositivo CE (2) può essere connesso tooone o più file PE (3).</span><span class="sxs-lookup"><span data-stu-id="5a87e-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected tooone or more PEs (3).</span></span>
>
>

<span data-ttu-id="5a87e-136">(con hello rete indicata dal numero di hello associata) vengono trattati i toovalidate un circuito ExpressRoute, hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="5a87e-136">toovalidate an ExpressRoute circuit, hello following steps are covered (with hello network point indicated by hello associated number):</span></span>
1. [<span data-ttu-id="5a87e-137">Convalidare il provisioning del circuito e lo stato (5)</span><span class="sxs-lookup"><span data-stu-id="5a87e-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="5a87e-138">Convalidare la configurazione di almeno un peering di ExpressRoute (5)</span><span class="sxs-lookup"><span data-stu-id="5a87e-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="5a87e-139">Convalidare ARP tra provider di servizi Microsoft e hello (collegamento tra 4 e 5)</span><span class="sxs-lookup"><span data-stu-id="5a87e-139">Validate ARP between Microsoft and hello service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="5a87e-140">Convalidare il protocollo BGP e route su hello MSEE (BGP tra too5 4 e 5 too6 se una rete virtuale è connesso)</span><span class="sxs-lookup"><span data-stu-id="5a87e-140">Validate BGP and routes on hello MSEE (BGP between 4 too5, and 5 too6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="5a87e-141">Controllo hello statistiche sul traffico (traffico che attraversa 5)</span><span class="sxs-lookup"><span data-stu-id="5a87e-141">Check hello Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="5a87e-142">Altre convalide e controlli verranno aggiunti in hello future, verificare mensile!</span><span class="sxs-lookup"><span data-stu-id="5a87e-142">More validations and checks will be added in hello future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="5a87e-143">Convalidare il provisioning del circuito e lo stato</span><span class="sxs-lookup"><span data-stu-id="5a87e-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="5a87e-144">Indipendentemente dal modello di integrazione applicativa hello, un circuito ExpressRoute ha toobe creato e quindi un servizio chiave generata per il provisioning del circuito.</span><span class="sxs-lookup"><span data-stu-id="5a87e-144">Regardless of hello connectivity model, an ExpressRoute circuit has toobe created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="5a87e-145">Il provisioning di un circuito ExpressRoute stabilisce connessioni ridondanti di livello 2 tra PE-MSEE (4) e MSEE (5).</span><span class="sxs-lookup"><span data-stu-id="5a87e-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="5a87e-146">Per ulteriori informazioni su come toocreate, modificare, eseguire il provisioning e verificare un circuito ExpressRoute, vedere l'articolo hello [creare e modificare un circuito ExpressRoute][CreateCircuit].</span><span class="sxs-lookup"><span data-stu-id="5a87e-146">For more information on how toocreate, modify, provision, and verify an ExpressRoute circuit, see hello article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="5a87e-147">Una chiave del servizio identifica in modo univoco un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5a87e-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="5a87e-148">Questa chiave è obbligatoria per la maggior parte dei comandi di powershell hello citate in questo documento.</span><span class="sxs-lookup"><span data-stu-id="5a87e-148">This key is required for most of hello powershell commands mentioned in this document.</span></span> <span data-ttu-id="5a87e-149">È inoltre necessario richiedere assistenza da Microsoft o da un tootroubleshoot partner ExpressRoute un problema di ExpressRoute, fornire il servizio di hello tooreadily chiave identifica il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="5a87e-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner tootroubleshoot an ExpressRoute issue, provide hello service key tooreadily identify hello circuit.</span></span>
>
>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="5a87e-150">Verifica tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5a87e-150">Verification via hello Azure portal</span></span>
<span data-ttu-id="5a87e-151">In hello portale di Azure, lo stato di hello di un circuito ExpressRoute può essere controllato selezionando ![2][2] su hello menu laterale a sinistra e quindi selezionando hello circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5a87e-151">In hello Azure portal, hello status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="5a87e-152">Selezione di ExpressRoute circuito sotto "Tutte le risorse" apre il pannello di circuito ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="5a87e-152">Selecting an ExpressRoute circuit listed under "All resources" opens hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="5a87e-153">In hello ![3][3] sezione del pannello hello, hello ExpressRoute essentials sono elencati come illustrato nella seguente cattura di schermata hello:</span><span class="sxs-lookup"><span data-stu-id="5a87e-153">In hello ![3][3] section of hello blade, hello ExpressRoute essentials are listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="5a87e-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="5a87e-154">![4][4]</span></span>    

<span data-ttu-id="5a87e-155">In Essentials ExpressRoute, hello *Circuit stato* indica lo stato di hello del circuito hello in hello lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5a87e-155">In hello ExpressRoute Essentials, *Circuit status* indicates hello status of hello circuit on hello Microsoft side.</span></span> <span data-ttu-id="5a87e-156">*Stato provider* indica se è stato circuito hello */non provisioning eseguito il provisioning* sul lato di provider di servizi di hello.</span><span class="sxs-lookup"><span data-stu-id="5a87e-156">*Provider status* indicates if hello circuit has been *Provisioned/Not provisioned* on hello service-provider side.</span></span> 

<span data-ttu-id="5a87e-157">Per un toobe di circuito ExpressRoute operativa, hello *Circuit stato* deve essere *abilitato* hello e *stato Provider* deve essere *provisioning eseguito*.</span><span class="sxs-lookup"><span data-stu-id="5a87e-157">For an ExpressRoute circuit toobe operational, hello *Circuit status* must be *Enabled* and hello *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="5a87e-158">Se hello *Circuit stato* non è abilitato, contattare [supporto Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="5a87e-158">If hello *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="5a87e-159">Se hello *stato Provider* non è disponibile, contattare il provider di servizi.</span><span class="sxs-lookup"><span data-stu-id="5a87e-159">If hello *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="5a87e-160">Verifica tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a87e-160">Verification via PowerShell</span></span>
<span data-ttu-id="5a87e-161">toolist tutti hello circuiti ExpressRoute in un gruppo di risorse, usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5a87e-161">toolist all hello ExpressRoute circuits in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="5a87e-162">È possibile ottenere il nome del gruppo di risorse tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a87e-162">You can get your resource group name through hello Azure portal.</span></span> <span data-ttu-id="5a87e-163">Vedere hello sottosezione precedente di questo documento e si noti che il nome del gruppo di risorse hello è elencato nella schermata dell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="5a87e-163">See hello previous subsection of this document and note that hello resource group name is listed in hello example screen shot.</span></span>
>
>

<span data-ttu-id="5a87e-164">tooselect un particolare circuito ExpressRoute in un gruppo di risorse, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5a87e-164">tooselect a particular ExpressRoute circuit in a Resource Group, use hello following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="5a87e-165">Una risposta di esempio:</span><span class="sxs-lookup"><span data-stu-id="5a87e-165">A sample response is:</span></span>

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

<span data-ttu-id="5a87e-166">tooconfirm se un circuito ExpressRoute è operativo, è necessario prestare particolare attenzione toohello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="5a87e-166">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="5a87e-167">Se hello *stato di provisioning* non è abilitato, contattare [supporto Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="5a87e-167">If hello *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="5a87e-168">Se hello *ServiceProviderProvisioningState* non è disponibile, contattare il provider di servizi.</span><span class="sxs-lookup"><span data-stu-id="5a87e-168">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="5a87e-169">Verifica tramite PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="5a87e-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="5a87e-170">toolist tutti hello circuiti ExpressRoute in una sottoscrizione, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5a87e-170">toolist all hello ExpressRoute circuits under a subscription, use hello following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="5a87e-171">tooselect un particolare circuito ExpressRoute, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5a87e-171">tooselect a particular ExpressRoute circuit, use hello following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="5a87e-172">Una risposta di esempio:</span><span class="sxs-lookup"><span data-stu-id="5a87e-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="5a87e-173">tooconfirm se un circuito ExpressRoute è operativo, prestare particolare attenzione toohello seguenti campi: ServiceProviderProvisioningState: lo stato di provisioning: abilitato</span><span class="sxs-lookup"><span data-stu-id="5a87e-173">tooconfirm if an ExpressRoute circuit is operational, pay particular attention toohello following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="5a87e-174">Se hello *stato* non è abilitato, contattare [supporto Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="5a87e-174">If hello *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="5a87e-175">Se hello *ServiceProviderProvisioningState* non è disponibile, contattare il provider di servizi.</span><span class="sxs-lookup"><span data-stu-id="5a87e-175">If hello *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="5a87e-176">Convalidare la configurazione del peering</span><span class="sxs-lookup"><span data-stu-id="5a87e-176">Validate Peering Configuration</span></span>
<span data-ttu-id="5a87e-177">Dopo il provider di servizi di hello ha completato hello provisioning del circuito ExpressRoute hello, è possibile creare una configurazione di routing su hello circuito ExpressRoute tra MSEE (4), le prenotazioni permanenti e MSEEs (5).</span><span class="sxs-lookup"><span data-stu-id="5a87e-177">After hello service provider has completed hello provisioning hello ExpressRoute circuit, a routing configuration can be created over hello ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="5a87e-178">Ogni circuito ExpressRoute può avere uno, due o tre contesti di routing abilitati: peering privato di Azure (traffico tooprivate reti virtuali in Azure), peering pubblico di Azure (traffico toopublic gli indirizzi IP in Azure) e (traffico tooOffice 365 peering Microsoft e Dynamics 365).</span><span class="sxs-lookup"><span data-stu-id="5a87e-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic tooprivate virtual networks in Azure), Azure public peering (traffic toopublic IP addresses in Azure), and Microsoft peering (traffic tooOffice 365 and Dynamics 365).</span></span> <span data-ttu-id="5a87e-179">Per ulteriori informazioni su come toocreate e modificare la configurazione di routing, vedere l'articolo hello [creare e modificare il routing per un circuito ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="5a87e-179">For more information on how toocreate and modify routing configuration, see hello article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-hello-azure-portal"></a><span data-ttu-id="5a87e-180">Verifica tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5a87e-180">Verification via hello Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="5a87e-181">È presente un bug noto nel portale di Azure in cui il peering ExpressRoute è hello *non* visualizzata nel portale di hello se configurato dal provider di servizi di hello.</span><span class="sxs-lookup"><span data-stu-id="5a87e-181">There is a known bug in hello Azure portal wherein ExpressRoute peerings are *NOT* shown in hello portal if configured by hello service provider.</span></span> <span data-ttu-id="5a87e-182">Aggiunta di peering ExpressRoute tramite il portale di hello o PowerShell *sovrascrive le impostazioni del provider servizio hello*.</span><span class="sxs-lookup"><span data-stu-id="5a87e-182">Adding ExpressRoute peerings via hello portal or PowerShell *overwrites hello service provider settings*.</span></span> <span data-ttu-id="5a87e-183">Questa azione interrompe hello routing sul circuito ExpressRoute hello e richiede il supporto di hello hello impostazioni del servizio provider toorestore hello e ristabilire la normale di routing.</span><span class="sxs-lookup"><span data-stu-id="5a87e-183">This action breaks hello routing on hello ExpressRoute circuit and requires hello support of hello service provider toorestore hello settings and reestablish normal routing.</span></span> <span data-ttu-id="5a87e-184">Modificare solo il peering ExpressRoute hello se si è certi che il provider di servizi di hello fornisce solo servizi di livello 2.</span><span class="sxs-lookup"><span data-stu-id="5a87e-184">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="5a87e-185">Se layer 3 viene fornito da hello peering hello e di provider di servizio sono vuote nel portale di hello, PowerShell può essere utilizzato toosee hello servizio provider configurato impostazioni.</span><span class="sxs-lookup"><span data-stu-id="5a87e-185">If layer 3 is provided by hello service provider and hello peerings are blank in hello portal, PowerShell can be used toosee hello service provider configured settings.</span></span>
>
>

<span data-ttu-id="5a87e-186">In hello portale di Azure, lo stato di un circuito ExpressRoute può essere controllato selezionando ![2][2] su hello menu laterale a sinistra e quindi selezionando hello circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="5a87e-186">In hello Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on hello left-side-bar menu and then selecting hello ExpressRoute circuit.</span></span> <span data-ttu-id="5a87e-187">Selezione di ExpressRoute circuito sotto "Tutte le risorse" aprire Pannello circuito ExpressRoute di hello.</span><span class="sxs-lookup"><span data-stu-id="5a87e-187">Selecting an ExpressRoute circuit listed under "All resources" would open hello ExpressRoute circuit blade.</span></span> <span data-ttu-id="5a87e-188">In hello ![3][3] sezione del pannello hello, hello ExpressRoute essentials sarà elencato come illustrato nella seguente cattura di schermata hello:</span><span class="sxs-lookup"><span data-stu-id="5a87e-188">In hello ![3][3] section of hello blade, hello ExpressRoute essentials would be listed as shown in hello following screen shot:</span></span>

<span data-ttu-id="5a87e-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="5a87e-189">![5][5]</span></span>

<span data-ttu-id="5a87e-190">In hello sopra riportato, come indicato Azure contesto di routing di peering privato è abilitata, mentre Azure pubblico e contesti di routing peering Microsoft non sono abilitati.</span><span class="sxs-lookup"><span data-stu-id="5a87e-190">In hello preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="5a87e-191">Un contesto di peering abilitato correttamente avrebbe subnet primario e secondario Point-to-(obbligatorio per il protocollo BGP) hello elencate.</span><span class="sxs-lookup"><span data-stu-id="5a87e-191">A successfully enabled peering context would also have hello primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="5a87e-192">subnet Hello /30 vengono utilizzate per l'indirizzo IP dell'interfaccia hello di hello MSEEs e PE MSEEs.</span><span class="sxs-lookup"><span data-stu-id="5a87e-192">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="5a87e-193">Se un peering non è abilitato, verificare se subnet primario e secondario hello assegnata corrisponde configurazione hello PE MSEEs.</span><span class="sxs-lookup"><span data-stu-id="5a87e-193">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on PE-MSEEs.</span></span> <span data-ttu-id="5a87e-194">Se non, toochange hello configurazione router MSEE, fare riferimento troppo[creare e modificare il routing per un circuito ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="5a87e-194">If not, toochange hello configuration on MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="5a87e-195">Verifica tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a87e-195">Verification via PowerShell</span></span>
<span data-ttu-id="5a87e-196">tooget hello Azure privata peering dettagli di configurazione, utilizzare hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="5a87e-196">tooget hello Azure private peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="5a87e-197">Una risposta di esempio, per un peering privato configurato correttamente:</span><span class="sxs-lookup"><span data-stu-id="5a87e-197">A sample response, for a successfully configured private peering, is:</span></span>

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 <span data-ttu-id="5a87e-198">Un contesto di peering abilitato correttamente avrebbe prefissi di indirizzo primario e secondario hello elencati.</span><span class="sxs-lookup"><span data-stu-id="5a87e-198">A successfully enabled peering context would have hello primary and secondary address prefixes listed.</span></span> <span data-ttu-id="5a87e-199">subnet Hello /30 vengono utilizzate per l'indirizzo IP dell'interfaccia hello di hello MSEEs e PE MSEEs.</span><span class="sxs-lookup"><span data-stu-id="5a87e-199">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="5a87e-200">tooget hello Azure pubblica peering dettagli di configurazione, utilizzare hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="5a87e-200">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="5a87e-201">tooget hello Microsoft peering dettagli di configurazione, utilizzare hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="5a87e-201">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="5a87e-202">Se non è configurato alcun peering, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="5a87e-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="5a87e-203">Una risposta di esempio, quando hello indicato peering (pubblico di Azure peering in questo esempio) non è configurata nel circuito hello:</span><span class="sxs-lookup"><span data-stu-id="5a87e-203">A sample response, when hello stated peering (Azure Public peering in this example) is not configured within hello circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="5a87e-204">Se un peering non è abilitato, verificare se hello corrispondenza hello primario e secondario subnet assegnate configurazione hello collegato PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="5a87e-204">If a peering is not enabled, check if hello primary and secondary subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="5a87e-205">Anche verificare se hello correggere *VlanId*, *AzureASN*, e *PeerASN* vengono utilizzati su MSEEs e se questi valori viene eseguito il mapping toohello quelli utilizzati in hello collegato PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="5a87e-205">Also check if hello correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="5a87e-206">Se si sceglie di hash MD5, la chiave condivisa hello deve corrispondere in coppia MSEE e PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="5a87e-206">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="5a87e-207">configurazione di hello toochange in router MSEE hello, fare riferimento troppo [creare e modificare il routing per un circuito ExpressRoute] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="5a87e-207">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="5a87e-208">Verifica tramite PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="5a87e-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="5a87e-209">tooget hello Azure privata peering dettagli di configurazione, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5a87e-209">tooget hello Azure private peering configuration details, use hello following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="5a87e-210">Una risposta di esempio, per un peering privato configurato correttamente:</span><span class="sxs-lookup"><span data-stu-id="5a87e-210">A sample response, for a successfully configured private peering is:</span></span>

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

<span data-ttu-id="5a87e-211">Abilitato correttamente, un contesto di peering avrebbe subnet peer primaria e secondaria hello elencate.</span><span class="sxs-lookup"><span data-stu-id="5a87e-211">A successfully, enabled peering context would have hello primary and secondary peer subnets listed.</span></span> <span data-ttu-id="5a87e-212">subnet Hello /30 vengono utilizzate per l'indirizzo IP dell'interfaccia hello di hello MSEEs e PE MSEEs.</span><span class="sxs-lookup"><span data-stu-id="5a87e-212">hello /30 subnets are used for hello interface IP address of hello MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="5a87e-213">tooget hello Azure pubblica peering dettagli di configurazione, utilizzare hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="5a87e-213">tooget hello Azure public peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="5a87e-214">tooget hello Microsoft peering dettagli di configurazione, utilizzare hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="5a87e-214">tooget hello Microsoft peering configuration details, use hello following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="5a87e-215">Se peering di livello 3 sono state impostate dal provider di servizi di hello, l'impostazione di peering ExpressRoute hello tramite il portale di hello o PowerShell sovrascrive le impostazioni del provider servizio hello.</span><span class="sxs-lookup"><span data-stu-id="5a87e-215">If layer 3 peerings were set by hello service provider, setting hello ExpressRoute peerings via hello portal or PowerShell overwrites hello service provider settings.</span></span> <span data-ttu-id="5a87e-216">Reimpostazione delle impostazioni peer hello provider lato richiede il supporto di hello hello del provider di servizi.</span><span class="sxs-lookup"><span data-stu-id="5a87e-216">Resetting hello provider side peering settings requires hello support of hello service provider.</span></span> <span data-ttu-id="5a87e-217">Modificare solo il peering ExpressRoute hello se si è certi che il provider di servizi di hello fornisce solo servizi di livello 2.</span><span class="sxs-lookup"><span data-stu-id="5a87e-217">Only modify hello ExpressRoute peerings if it is certain that hello service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="5a87e-218">Se un peering non è abilitato, verificare se hello peer primario e secondario subnet assegnate corrispondenza hello configurazione su hello collegato PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="5a87e-218">If a peering is not enabled, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="5a87e-219">Anche verificare se hello correggere *VlanId*, *AzureAsn*, e *PeerAsn* vengono utilizzati su MSEEs e se questi valori viene eseguito il mapping toohello quelli utilizzati in hello collegato PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="5a87e-219">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="5a87e-220">configurazione di hello toochange in router MSEE hello, fare riferimento troppo [creare e modificare il routing per un circuito ExpressRoute] [CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="5a87e-220">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a><span data-ttu-id="5a87e-221">Convalidare ARP tra Microsoft e hello provider del servizio</span><span class="sxs-lookup"><span data-stu-id="5a87e-221">Validate ARP between Microsoft and hello service provider</span></span>
<span data-ttu-id="5a87e-222">In questa sezione vengono usati i comandi di PowerShell (versione classica).</span><span class="sxs-lookup"><span data-stu-id="5a87e-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="5a87e-223">Se si utilizza i comandi di gestione risorse di Azure PowerShell, assicurarsi di avere accesso amministratore/coamministratore toohello sottoscrizione tramite [portale di Azure classico][OldPortal].</span><span class="sxs-lookup"><span data-stu-id="5a87e-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="5a87e-224">Per la risoluzione dei problemi mediante Gestione risorse di Azure i comandi, vedere toohello [tabelle recupero ARP nel modello di distribuzione di gestione risorse di hello] [ ARP] documento.</span><span class="sxs-lookup"><span data-stu-id="5a87e-224">For troubleshooting using Azure Resource Manager commands please refer toohello [Getting ARP tables in hello Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="5a87e-225">tooget ARP, sia hello portale di Azure e i comandi di PowerShell di gestione risorse di Azure può essere utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5a87e-225">tooget ARP, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="5a87e-226">Se si verificano errori con i comandi di PowerShell di gestione risorse di Azure hello, i comandi di PowerShell classici dovrebbero funzionare come PowerShell classico comandi funzionano anche con circuiti ExpressRoute di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a87e-226">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="5a87e-227">tooget hello tabella ARP hello MSEE del router principale per il peering privato hello, usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5a87e-227">tooget hello ARP table from hello primary MSEE router for hello private peering, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="5a87e-228">Una risposta di esempio per il comando di hello, in caso di esito positivo hello:</span><span class="sxs-lookup"><span data-stu-id="5a87e-228">An example response for hello command, in hello successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="5a87e-229">Analogamente, è possibile controllare la tabella ARP da Ciao MSEE hello hello *primario*/*secondario* percorso, per *privata* /  *Pubblica*/*Microsoft* peering.</span><span class="sxs-lookup"><span data-stu-id="5a87e-229">Similarly, you can check hello ARP table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="5a87e-230">Hello esempio seguente viene mostrato hello risposta del comando hello per un peering non esiste.</span><span class="sxs-lookup"><span data-stu-id="5a87e-230">hello following example shows hello response of hello command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="5a87e-231">Se la tabella ARP hello non dispone di indirizzi IP delle interfacce hello eseguire il mapping di indirizzi tooMAC, hello esaminare le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="5a87e-231">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
>1. <span data-ttu-id="5a87e-232">Se hello primo indirizzo IP del subnet hello /30 assegnato per il collegamento hello tra hello MSEE PR e MSEE viene utilizzato nell'interfaccia hello del MSEE PR</span><span class="sxs-lookup"><span data-stu-id="5a87e-232">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="5a87e-233">Azure Usa sempre l'indirizzo IP secondo hello per MSEEs.</span><span class="sxs-lookup"><span data-stu-id="5a87e-233">Azure always uses hello second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="5a87e-234">Verificare se cliente hello (C-Tag) e i tag VLAN servizio (S-Tag) corrispondano entrambi in coppia MSEE PR e MSEE.</span><span class="sxs-lookup"><span data-stu-id="5a87e-234">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a><span data-ttu-id="5a87e-235">Convalidare il protocollo BGP e route su hello MSEE</span><span class="sxs-lookup"><span data-stu-id="5a87e-235">Validate BGP and routes on hello MSEE</span></span>
<span data-ttu-id="5a87e-236">In questa sezione vengono usati i comandi di PowerShell (versione classica).</span><span class="sxs-lookup"><span data-stu-id="5a87e-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="5a87e-237">Se si utilizza i comandi di gestione risorse di Azure PowerShell, assicurarsi di avere accesso amministratore/coamministratore toohello sottoscrizione tramite [portale di Azure classico][OldPortal]</span><span class="sxs-lookup"><span data-stu-id="5a87e-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access toohello subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="5a87e-238">tooget BGP informazioni, entrambi hello è possibile utilizzare il portale di Azure e i comandi di PowerShell di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a87e-238">tooget BGP information, both hello Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="5a87e-239">Se si verificano errori con i comandi di PowerShell di gestione risorse di Azure hello, i comandi di PowerShell classici dovrebbero funzionare come PowerShell classico comandi funzionano anche con circuiti ExpressRoute di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a87e-239">If errors are encountered with hello Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="5a87e-240">tooget hello tabella di routing (adiacente BGP) riepilogo per un particolare contesto di routing, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5a87e-240">tooget hello routing table (BGP neighbor) summary for a particular routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="5a87e-241">Una risposta di esempio:</span><span class="sxs-lookup"><span data-stu-id="5a87e-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="5a87e-242">Come illustrato nell'esempio sopra riportato hello, hello è utile toodetermine per quanto tempo contesto routing hello è stata stabilita.</span><span class="sxs-lookup"><span data-stu-id="5a87e-242">As shown in hello preceding example, hello command is useful toodetermine for how long hello routing context has been established.</span></span> <span data-ttu-id="5a87e-243">Indica inoltre il numero di prefissi di route annunciate dal router di peering hello.</span><span class="sxs-lookup"><span data-stu-id="5a87e-243">It also indicates number of route prefixes advertised by hello peering router.</span></span>

>[!NOTE]
><span data-ttu-id="5a87e-244">Se lo stato di hello è attivo o inattivo, controllare se hello peer primario e secondario subnet assegnate corrispondenza hello configurazione su hello collegato PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="5a87e-244">If hello state is in Active or Idle, check if hello primary and secondary peer subnets assigned match hello configuration on hello linked PE-MSEE.</span></span> <span data-ttu-id="5a87e-245">Anche verificare se hello correggere *VlanId*, *AzureAsn*, e *PeerAsn* vengono utilizzati su MSEEs e se questi valori viene eseguito il mapping toohello quelli utilizzati in hello collegato PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="5a87e-245">Also check if hello correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps toohello ones used on hello linked PE-MSEE.</span></span> <span data-ttu-id="5a87e-246">Se si sceglie di hash MD5, la chiave condivisa hello deve corrispondere in coppia MSEE e PE MSEE.</span><span class="sxs-lookup"><span data-stu-id="5a87e-246">If MD5 hashing is chosen, hello shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="5a87e-247">configurazione di hello toochange in router MSEE hello, fare riferimento troppo[creare e modificare il routing per un circuito ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="5a87e-247">toochange hello configuration on hello MSEE routers, refer too[Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="5a87e-248">Se alcune destinazioni non sono raggiungibili su un particolare peering, controllare la tabella di route hello di hello MSEEs appartenenti toohello particolare contesto peer.</span><span class="sxs-lookup"><span data-stu-id="5a87e-248">If certain destinations are not reachable over a particular peering, check hello route table of hello MSEEs belonging toohello particular peering context.</span></span> <span data-ttu-id="5a87e-249">Se un prefisso corrispondente (potrebbe essere NATed IP) è presente nella tabella di routing hello, controllare se sono presenti firewall/gruppo/ACL nel percorso hello e consentono il traffico di hello.</span><span class="sxs-lookup"><span data-stu-id="5a87e-249">If a matching prefix (could be NATed IP) is present in hello routing table, then check if there are firewalls/NSG/ACLs on hello path and if they permit hello traffic.</span></span>
>
>

<span data-ttu-id="5a87e-250">tooget hello completa tabella di routing da MSEE su hello *primario* percorso per hello particolare *privata* contesto routing, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5a87e-250">tooget hello full routing table from MSEE on hello *Primary* path for hello particular *Private* routing context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="5a87e-251">È un risultato positivo di esempio per il comando hello:</span><span class="sxs-lookup"><span data-stu-id="5a87e-251">An example successful outcome for hello command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="5a87e-252">Analogamente, è possibile controllare tabella di routing hello da Ciao MSEE hello *primario*/*secondario* percorso, per *privata* / *Pubblica*/*Microsoft* un contesto di peer.</span><span class="sxs-lookup"><span data-stu-id="5a87e-252">Similarly, you can check hello routing table from hello MSEE in hello *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="5a87e-253">Hello esempio seguente viene mostrato hello risposta del comando hello per un peering non esiste:</span><span class="sxs-lookup"><span data-stu-id="5a87e-253">hello following example shows hello response of hello command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a><span data-ttu-id="5a87e-254">Controllare le statistiche sul traffico hello</span><span class="sxs-lookup"><span data-stu-id="5a87e-254">Check hello Traffic Statistics</span></span>
<span data-ttu-id="5a87e-255">hello tooget combinati e disconnettersi, statistiche sul traffico percorso primario e secondario - byte di un contesto di peering, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5a87e-255">tooget hello combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use hello following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="5a87e-256">Un esempio di output del comando hello è:</span><span class="sxs-lookup"><span data-stu-id="5a87e-256">A sample output of hello command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="5a87e-257">È un esempio di output del comando hello per un peering non esistente:</span><span class="sxs-lookup"><span data-stu-id="5a87e-257">A sample output of hello command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="5a87e-258">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5a87e-258">Next Steps</span></span>
<span data-ttu-id="5a87e-259">Per ulteriori informazioni o assistenza, vedere hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="5a87e-259">For more information or help, check out hello following links:</span></span>

- <span data-ttu-id="5a87e-260">[Supporto tecnico Microsoft][Support]</span><span class="sxs-lookup"><span data-stu-id="5a87e-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="5a87e-261">[Creare e modificare un circuito ExpressRoute][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="5a87e-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="5a87e-262">[Creare e modificare il routing per un circuito ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="5a87e-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Connettività logica ExpressRoute"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Icona All resources"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Icona Overview"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Schermata di esempio delle informazioni di base di ExpressRoute"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Schermata di esempio delle informazioni di base di ExpressRoute"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






