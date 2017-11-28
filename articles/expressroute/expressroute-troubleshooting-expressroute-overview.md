---
title: "Verifica della connettività: guida alla risoluzione dei problemi di Azure ExpressRoute | Microsoft Docs"
description: "Questa pagina fornisce istruzioni sulla risoluzione dei problemi e convalida della connettività end-to-end di un circuito ExpressRoute."
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
ms.openlocfilehash: 5a6360b56963d219ab576fb3e2636b6c51dd72ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="verifying-expressroute-connectivity"></a><span data-ttu-id="12f20-103">Verifica della connettività di ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="12f20-103">Verifying ExpressRoute connectivity</span></span>
<span data-ttu-id="12f20-104">ExpressRoute, che consente di estendere una rete locale nel cloud Microsoft tramite una connessione privata fornita da un provider di connettività, coinvolge le tre diverse aree di rete seguenti:</span><span class="sxs-lookup"><span data-stu-id="12f20-104">ExpressRoute, which extends an on-premises network into the Microsoft cloud over a private connection that is facilitated by a connectivity provider, involves the following three distinct network zones:</span></span>

-   <span data-ttu-id="12f20-105">Rete del cliente</span><span class="sxs-lookup"><span data-stu-id="12f20-105">Customer Network</span></span>
-   <span data-ttu-id="12f20-106">Rete del provider</span><span class="sxs-lookup"><span data-stu-id="12f20-106">Provider Network</span></span>
-   <span data-ttu-id="12f20-107">Datacenter Microsoft</span><span class="sxs-lookup"><span data-stu-id="12f20-107">Microsoft Datacenter</span></span>

<span data-ttu-id="12f20-108">Lo scopo di questo documento è di aiutare l'utente a identificare dove (o anche se) esiste un problema di connettività e all'interno di quale area, in modo tale da richiedere assistenza al team appropriato per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="12f20-108">The purpose of this document is to help user to identify where (or even if) a connectivity issue exists and within which zone, thereby to seek help from appropriate team to resolve the issue.</span></span> <span data-ttu-id="12f20-109">Se per risolvere un problema è necessaria l'assistenza tecnica di Microsoft, aprire un ticket di supporto al [supporto tecnico Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="12f20-109">If Microsoft support is needed to resolve an issue, open a support ticket with [Microsoft Support][Support].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12f20-110">Questo documento è pensato per aiutare l'utente a rilevare e risolvere problemi semplici.</span><span class="sxs-lookup"><span data-stu-id="12f20-110">This document is intended to help diagnosing and fixing simple issues.</span></span> <span data-ttu-id="12f20-111">Non sostituisce tuttavia il supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="12f20-111">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="12f20-112">Se non si riesce a risolvere il problema tramite la procedura descritta, è necessario aprire un ticket di supporto al [supporto tecnico Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="12f20-112">Open a support ticket with [Microsoft Support][Support] if you are unable to solve the problem using the guidance provided.</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="12f20-113">Panoramica</span><span class="sxs-lookup"><span data-stu-id="12f20-113">Overview</span></span>
<span data-ttu-id="12f20-114">Il diagramma seguente illustra la connettività logica della rete di un cliente alla rete Microsoft usando ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12f20-114">The following diagram shows the logical connectivity of a customer network to Microsoft network using ExpressRoute.</span></span>
<span data-ttu-id="12f20-115">[![1]][1]</span><span class="sxs-lookup"><span data-stu-id="12f20-115">[![1]][1]</span></span>

<span data-ttu-id="12f20-116">Nel diagramma precedente i numeri indicano i punti principali delle reti.</span><span class="sxs-lookup"><span data-stu-id="12f20-116">In the preceding diagram, the numbers indicate key network points.</span></span> <span data-ttu-id="12f20-117">Tali punti sono spesso citati in questo articolo tramite il numero associato.</span><span class="sxs-lookup"><span data-stu-id="12f20-117">The network points are referenced often through this article by their associated number.</span></span>

<span data-ttu-id="12f20-118">A seconda del modello di connettività ExpressRoute (condivisione percorso per Cloud Exchange, connessione Ethernet punto a punto o any-to-any (IPVPN)), i punti 3 e 4 della rete potrebbero essere switch (dispositivi di livello 2).</span><span class="sxs-lookup"><span data-stu-id="12f20-118">Depending on the ExpressRoute connectivity model (Cloud Exchange Co-location, Point-to-Point Ethernet Connection, or Any-to-any (IPVPN)) the network points 3 and 4 may be switches (Layer 2 devices).</span></span> <span data-ttu-id="12f20-119">I punti principali delle reti illustrati sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="12f20-119">The key network points illustrated are as follows:</span></span>

1.  <span data-ttu-id="12f20-120">Dispositivo di calcolo del cliente (ad esempio, un server o un PC)</span><span class="sxs-lookup"><span data-stu-id="12f20-120">Customer compute device (for example, a server or PC)</span></span>
2.  <span data-ttu-id="12f20-121">CE: router perimetrali del cliente</span><span class="sxs-lookup"><span data-stu-id="12f20-121">CEs: Customer edge routers</span></span> 
3.  <span data-ttu-id="12f20-122">PE (rivolti verso i CE): router/switch perimetrali del provider rivolti verso i router perimetrali del cliente.</span><span class="sxs-lookup"><span data-stu-id="12f20-122">PEs (CE facing): Provider edge routers/switches that are facing customer edge routers.</span></span> <span data-ttu-id="12f20-123">Indicata con il nome di PE-CE nel presente documento.</span><span class="sxs-lookup"><span data-stu-id="12f20-123">Referred to as PE-CEs in this document.</span></span>
4.  <span data-ttu-id="12f20-124">PE (rivolti verso gli MSEE): router/switch perimetrali del provider rivolti verso gli MSEE.</span><span class="sxs-lookup"><span data-stu-id="12f20-124">PEs (MSEE facing): Provider edge routers/switches that are facing MSEEs.</span></span> <span data-ttu-id="12f20-125">Indicata con il nome di PE-MSEE nel presente documento.</span><span class="sxs-lookup"><span data-stu-id="12f20-125">Referred to as PE-MSEEs in this document.</span></span>
5.  <span data-ttu-id="12f20-126">MSEE: router ExpressRoute Microsoft Enterprise Edge (MSEE)</span><span class="sxs-lookup"><span data-stu-id="12f20-126">MSEEs: Microsoft Enterprise Edge (MSEE) ExpressRoute routers</span></span>
6.  <span data-ttu-id="12f20-127">Gateway di rete virtuale (VNet)</span><span class="sxs-lookup"><span data-stu-id="12f20-127">Virtual Network (VNet) Gateway</span></span>
7.  <span data-ttu-id="12f20-128">Dispositivo di calcolo sulla rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="12f20-128">Compute device on the Azure VNet</span></span>

<span data-ttu-id="12f20-129">Se vengono usati modelli di connettività di condivisione percorso per Cloud Exchange o connessione Ethernet punto a punto, il router perimetrale del cliente (2) stabilisce il peering BGP con gli MSEE (5).</span><span class="sxs-lookup"><span data-stu-id="12f20-129">If the Cloud Exchange Co-location or Point-to-Point Ethernet Connection connectivity models are used, the customer edge router (2) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="12f20-130">I punti 3 e 4 sono ancora presenti, ma in forma trasparente, come dispositivi di livello 2.</span><span class="sxs-lookup"><span data-stu-id="12f20-130">Network points 3 and 4 would still exist but be somewhat transparent as Layer 2 devices.</span></span>

<span data-ttu-id="12f20-131">Se si usa il modello di connettività any-to-any (IPVPN), i PE (rivolti verso gli MSEE) (4) stabiliscono il peering BGP con gli MSEE (5).</span><span class="sxs-lookup"><span data-stu-id="12f20-131">If the Any-to-any (IPVPN) connectivity model is used, the PEs (MSEE facing) (4) would establish BGP peering with MSEEs (5).</span></span> <span data-ttu-id="12f20-132">Le route si propagano quindi nuovamente alla rete del cliente attraverso la rete del provider di servizi IPVPN.</span><span class="sxs-lookup"><span data-stu-id="12f20-132">Routes would then propagate back to the customer network via the IPVPN service provider network.</span></span>

>[!NOTE]
><span data-ttu-id="12f20-133">Per la disponibilità elevata di ExpressRoute, Microsoft richiede una coppia ridondante di sessioni BGP tra MSEE (5) e PE-MSEE (4).</span><span class="sxs-lookup"><span data-stu-id="12f20-133">For ExpressRoute high availability, Microsoft requires a redundant pair of BGP sessions between MSEEs (5) and PE-MSEEs (4).</span></span> <span data-ttu-id="12f20-134">Si consiglia anche una coppia ridondante di percorsi di rete tra rete del cliente e PE-CE.</span><span class="sxs-lookup"><span data-stu-id="12f20-134">A redundant pair of network paths is also encouraged between customer network and PE-CEs.</span></span> <span data-ttu-id="12f20-135">Tuttavia, nel modello di connessione any-to-any (IPVPN), un singolo dispositivo CE (2) può essere collegato a uno o più PE (3).</span><span class="sxs-lookup"><span data-stu-id="12f20-135">However, in Any-to-any (IPVPN) connection model, a single CE device (2) may be connected to one or more PEs (3).</span></span>
>
>

<span data-ttu-id="12f20-136">Per convalidare un circuito ExpressRoute, vengono seguiti i seguenti passaggi, con il punto di rete indicato dal numero associato:</span><span class="sxs-lookup"><span data-stu-id="12f20-136">To validate an ExpressRoute circuit, the following steps are covered (with the network point indicated by the associated number):</span></span>
1. [<span data-ttu-id="12f20-137">Convalidare il provisioning del circuito e lo stato (5)</span><span class="sxs-lookup"><span data-stu-id="12f20-137">Validate circuit provisioning and state (5)</span></span>](#validate-circuit-provisioning-and-state)
2. [<span data-ttu-id="12f20-138">Convalidare la configurazione di almeno un peering di ExpressRoute (5)</span><span class="sxs-lookup"><span data-stu-id="12f20-138">Validate at least one ExpressRoute peering is configured (5)</span></span>](#validate-peering-configuration)
3. [<span data-ttu-id="12f20-139">Convalidare ARP tra Microsoft e il provider di servizi (collegamento tra 4 e 5)</span><span class="sxs-lookup"><span data-stu-id="12f20-139">Validate ARP between Microsoft and the service provider (link between 4 and 5)</span></span>](#validate-arp-between-microsoft-and-the-service-provider)
4. [<span data-ttu-id="12f20-140">Convalidare BGP e route sul MSEE (BGP tra 4 e 5 e 5 e 6 se una rete virtuale è connessa)</span><span class="sxs-lookup"><span data-stu-id="12f20-140">Validate BGP and routes on the MSEE (BGP between 4 to 5, and 5 to 6 if a VNet is connected)</span></span>](#validate-bgp-and-routes-on-the-msee)
5. [<span data-ttu-id="12f20-141">Verificare le statistiche del traffico (traffico che attraversa 5)</span><span class="sxs-lookup"><span data-stu-id="12f20-141">Check the Traffic Statistics (Traffic passing through 5)</span></span>](#check-the-traffic-statistics)

<span data-ttu-id="12f20-142">In futuro verranno aggiunti altri controlli e maggiori convalide. Si consiglia quindi di verificare mensilmente.</span><span class="sxs-lookup"><span data-stu-id="12f20-142">More validations and checks will be added in the future, check back monthly!</span></span>

##<a name="validate-circuit-provisioning-and-state"></a><span data-ttu-id="12f20-143">Convalidare il provisioning del circuito e lo stato</span><span class="sxs-lookup"><span data-stu-id="12f20-143">Validate circuit provisioning and state</span></span>
<span data-ttu-id="12f20-144">Indipendentemente dal modello di connettività, è necessario creare un circuito ExpressRoute e, pertanto, generare una chiave del servizio per il provisioning del circuito.</span><span class="sxs-lookup"><span data-stu-id="12f20-144">Regardless of the connectivity model, an ExpressRoute circuit has to be created and thus a service key generated for circuit provisioning.</span></span> <span data-ttu-id="12f20-145">Il provisioning di un circuito ExpressRoute stabilisce connessioni ridondanti di livello 2 tra PE-MSEE (4) e MSEE (5).</span><span class="sxs-lookup"><span data-stu-id="12f20-145">Provisioning an ExpressRoute circuit establishes a redundant Layer 2 connections between PE-MSEEs (4) and MSEEs (5).</span></span> <span data-ttu-id="12f20-146">Per altre informazioni su come creare, modificare, eseguire il provisioning e verificare un circuito ExpressRoute, vedere l'articolo [Creare e modificare un circuito ExpressRoute][CreateCircuit].</span><span class="sxs-lookup"><span data-stu-id="12f20-146">For more information on how to create, modify, provision, and verify an ExpressRoute circuit, see the article [Create and modify an ExpressRoute circuit][CreateCircuit].</span></span>

>[!TIP]
><span data-ttu-id="12f20-147">Una chiave del servizio identifica in modo univoco un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12f20-147">A service key uniquely identifies an ExpressRoute circuit.</span></span> <span data-ttu-id="12f20-148">Questa chiave è necessaria per la maggior parte dei comandi di Powershell indicati in questo documento.</span><span class="sxs-lookup"><span data-stu-id="12f20-148">This key is required for most of the powershell commands mentioned in this document.</span></span> <span data-ttu-id="12f20-149">Se fosse necessario richiedere l'assistenza di Microsoft o di un partner ExpressRoute per risolvere un problema di ExpressRoute, fornire la chiave del servizio per identificare facilmente il circuito.</span><span class="sxs-lookup"><span data-stu-id="12f20-149">Also, should you need assistance from Microsoft or from an ExpressRoute partner to troubleshoot an ExpressRoute issue, provide the service key to readily identify the circuit.</span></span>
>
>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="12f20-150">Verifica tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="12f20-150">Verification via the Azure portal</span></span>
<span data-ttu-id="12f20-151">Nel portale di Azure lo stato di un circuito ExpressRoute può essere controllato selezionando ![2][2] nel menu sulla barra laterale sinistra e quindi selezionando il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12f20-151">In the Azure portal, the status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="12f20-152">La selezione di un circuito ExpressRoute elencato in "All resources" (Tutte le risorse) determina l'apertura del pannello del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12f20-152">Selecting an ExpressRoute circuit listed under "All resources" opens the ExpressRoute circuit blade.</span></span> <span data-ttu-id="12f20-153">Nella sezione ![3][3] del pannello sono elencate le informazioni di base di ExpressRoute come illustrato nella schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="12f20-153">In the ![3][3] section of the blade, the ExpressRoute essentials are listed as shown in the following screen shot:</span></span>

<span data-ttu-id="12f20-154">![4][4]</span><span class="sxs-lookup"><span data-stu-id="12f20-154">![4][4]</span></span>    

<span data-ttu-id="12f20-155">Nelle informazioni di base di ExpressRoute *Stato circuito* indica lo stato del circuito sul lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="12f20-155">In the ExpressRoute Essentials, *Circuit status* indicates the status of the circuit on the Microsoft side.</span></span> <span data-ttu-id="12f20-156">*Stato provider* indica se si tratta di un circuito con *Provisioning eseguito/Senza provisioning* sul lato del provider dei servizi.</span><span class="sxs-lookup"><span data-stu-id="12f20-156">*Provider status* indicates if the circuit has been *Provisioned/Not provisioned* on the service-provider side.</span></span> 

<span data-ttu-id="12f20-157">Per consentire il funzionamento di un circuito ExpressRoute, *Stato circuito* deve essere impostato su *Abilitato* e *Stato provider* su *Provisioning eseguito*.</span><span class="sxs-lookup"><span data-stu-id="12f20-157">For an ExpressRoute circuit to be operational, the *Circuit status* must be *Enabled* and the *Provider status* must be *Provisioned*.</span></span>

>[!NOTE]
><span data-ttu-id="12f20-158">Se *Stato circuito* non è impostato su Abilitato, contattare il [supporto tecnico Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="12f20-158">If the *Circuit status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="12f20-159">Se *Stato provider* è impostato su Senza provisioning, contattare il provider dei servizi.</span><span class="sxs-lookup"><span data-stu-id="12f20-159">If the *Provider status* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="12f20-160">Verifica tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="12f20-160">Verification via PowerShell</span></span>
<span data-ttu-id="12f20-161">Per elencare tutti i circuiti ExpressRoute in un gruppo di risorse, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="12f20-161">To list all the ExpressRoute circuits in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
><span data-ttu-id="12f20-162">È possibile ottenere il nome del gruppo di risorse tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="12f20-162">You can get your resource group name through the Azure portal.</span></span> <span data-ttu-id="12f20-163">Vedere la sezione precedente di questo documento e notare che il nome del gruppo di risorse è elencato nella schermata di esempio.</span><span class="sxs-lookup"><span data-stu-id="12f20-163">See the previous subsection of this document and note that the resource group name is listed in the example screen shot.</span></span>
>
>

<span data-ttu-id="12f20-164">Per selezionare uno specifico circuito ExpressRoute in un gruppo di risorse, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="12f20-164">To select a particular ExpressRoute circuit in a Resource Group, use the following command:</span></span>

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

<span data-ttu-id="12f20-165">Una risposta di esempio:</span><span class="sxs-lookup"><span data-stu-id="12f20-165">A sample response is:</span></span>

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

<span data-ttu-id="12f20-166">Per verificare se un circuito ExpressRoute è operativo, prestare particolare attenzione ai campi seguenti:</span><span class="sxs-lookup"><span data-stu-id="12f20-166">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields:</span></span>

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
><span data-ttu-id="12f20-167">Se *CircuitProvisioningState* non è abilitato, contattare il [supporto tecnico Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="12f20-167">If the *CircuitProvisioningState* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="12f20-168">Se *ServiceProviderProvisioningState* è senza provisioning, contattare il provider di servizi.</span><span class="sxs-lookup"><span data-stu-id="12f20-168">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

###<a name="verification-via-powershell-classic"></a><span data-ttu-id="12f20-169">Verifica tramite PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="12f20-169">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="12f20-170">Per elencare tutti i circuiti ExpressRoute in una sottoscrizione, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="12f20-170">To list all the ExpressRoute circuits under a subscription, use the following command:</span></span>

    Get-AzureDedicatedCircuit

<span data-ttu-id="12f20-171">Per selezionare uno specifico circuito ExpressRoute, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="12f20-171">To select a particular ExpressRoute circuit, use the following command:</span></span>

    Get-AzureDedicatedCircuit -ServiceKey **************************************

<span data-ttu-id="12f20-172">Una risposta di esempio:</span><span class="sxs-lookup"><span data-stu-id="12f20-172">A sample response is:</span></span>

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

<span data-ttu-id="12f20-173">Per verificare se un circuito ExpressRoute è operativo, prestare particolare attenzione ai campi seguenti: ServiceProviderProvisioningState: Provisioned Status: Enabled</span><span class="sxs-lookup"><span data-stu-id="12f20-173">To confirm if an ExpressRoute circuit is operational, pay particular attention to the following fields: ServiceProviderProvisioningState : Provisioned Status                           : Enabled</span></span>

>[!NOTE]
><span data-ttu-id="12f20-174">Se *Status* non è abilitato, contattare il [supporto tecnico Microsoft][Support].</span><span class="sxs-lookup"><span data-stu-id="12f20-174">If the *Status* is not enabled, contact [Microsoft Support][Support].</span></span> <span data-ttu-id="12f20-175">Se *ServiceProviderProvisioningState* è senza provisioning, contattare il provider di servizi.</span><span class="sxs-lookup"><span data-stu-id="12f20-175">If the *ServiceProviderProvisioningState* is not provisioned, contact your service provider.</span></span>
>
>

##<a name="validate-peering-configuration"></a><span data-ttu-id="12f20-176">Convalidare la configurazione del peering</span><span class="sxs-lookup"><span data-stu-id="12f20-176">Validate Peering Configuration</span></span>
<span data-ttu-id="12f20-177">Dopo che il provider di servizi ha completato il provisioning del circuito ExpressRoute, è possibile creare una configurazione di routing sul circuito ExpressRoute tra MSEE-PR (4) e MSEE (5).</span><span class="sxs-lookup"><span data-stu-id="12f20-177">After the service provider has completed the provisioning the ExpressRoute circuit, a routing configuration can be created over the ExpressRoute circuit between MSEE-PRs (4) and MSEEs (5).</span></span> <span data-ttu-id="12f20-178">Ogni circuito ExpressRoute può avere uno, due o tre contesti di routing abilitati: peering privato di Azure, ovvero il traffico verso reti virtuali private in Azure, peering pubblico di Azure, ovvero il traffico verso indirizzi IP pubblici in Azure e peering Microsoft, ovvero il traffico verso Office 365 e Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="12f20-178">Each ExpressRoute circuit can have one, two, or three routing contexts enabled: Azure private peering (traffic to private virtual networks in Azure), Azure public peering (traffic to public IP addresses in Azure), and Microsoft peering (traffic to Office 365 and Dynamics 365).</span></span> <span data-ttu-id="12f20-179">Per altre informazioni su come creare e modificare la configurazione di routing, vedere l'articolo [Creare e modificare il routing per un circuito ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="12f20-179">For more information on how to create and modify routing configuration, see the article [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>

###<a name="verification-via-the-azure-portal"></a><span data-ttu-id="12f20-180">Verifica tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="12f20-180">Verification via the Azure portal</span></span>
>[!IMPORTANT]
><span data-ttu-id="12f20-181">Esiste un bug noto nel portale di Azure in cui i peering di ExpressRoute *NON* sono mostrati nel portale se configurati dal provider di servizi.</span><span class="sxs-lookup"><span data-stu-id="12f20-181">There is a known bug in the Azure portal wherein ExpressRoute peerings are *NOT* shown in the portal if configured by the service provider.</span></span> <span data-ttu-id="12f20-182">Aggiungendo peering di ExpressRoute tramite il portale o PowerShell *si sovrascrivono le impostazioni del provider di servizi*.</span><span class="sxs-lookup"><span data-stu-id="12f20-182">Adding ExpressRoute peerings via the portal or PowerShell *overwrites the service provider settings*.</span></span> <span data-ttu-id="12f20-183">Questa operazione interrompe il routing del circuito ExpressRoute ed è richiesto il supporto del provider di servizi per ripristinare le impostazioni e ristabilire il routing normale.</span><span class="sxs-lookup"><span data-stu-id="12f20-183">This action breaks the routing on the ExpressRoute circuit and requires the support of the service provider to restore the settings and reestablish normal routing.</span></span> <span data-ttu-id="12f20-184">Modificare i peering di ExpressRoute solo se si è certi che il provider di servizi offre esclusivamente servizi di livello 2.</span><span class="sxs-lookup"><span data-stu-id="12f20-184">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="12f20-185">Se il provider offre servizi di livello 3 e i peering non sono mostrati nel portale, è possibile usare PowerShell per visualizzare le impostazioni configurate del provider di servizi.</span><span class="sxs-lookup"><span data-stu-id="12f20-185">If layer 3 is provided by the service provider and the peerings are blank in the portal, PowerShell can be used to see the service provider configured settings.</span></span>
>
>

<span data-ttu-id="12f20-186">Nel portale di Azure lo stato di un circuito ExpressRoute può essere controllato selezionando ![2][2] nel menu sulla barra laterale sinistra e quindi selezionando il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12f20-186">In the Azure portal, status of an ExpressRoute circuit can be checked by selecting ![2][2] on the left-side-bar menu and then selecting the ExpressRoute circuit.</span></span> <span data-ttu-id="12f20-187">La selezione di un circuito ExpressRoute elencato in "All resources" (Tutte le risorse) determina l'apertura del pannello del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="12f20-187">Selecting an ExpressRoute circuit listed under "All resources" would open the ExpressRoute circuit blade.</span></span> <span data-ttu-id="12f20-188">Nella sezione ![3][3] del pannello saranno elencate le informazioni di base di ExpressRoute come illustrato nella schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="12f20-188">In the ![3][3] section of the blade, the ExpressRoute essentials would be listed as shown in the following screen shot:</span></span>

<span data-ttu-id="12f20-189">![5][5]</span><span class="sxs-lookup"><span data-stu-id="12f20-189">![5][5]</span></span>

<span data-ttu-id="12f20-190">Nell'esempio precedente, come indicato, il contesto di routing di peering privato di Azure è abilitato, mentre i contesti di routing di peering pubblico e Microsoft non sono abilitati.</span><span class="sxs-lookup"><span data-stu-id="12f20-190">In the preceding example, as noted Azure private peering routing context is enabled, whereas Azure public and Microsoft peering routing contexts are not enabled.</span></span> <span data-ttu-id="12f20-191">Per un contesto di peering abilitato correttamente vengono anche elencate le subnet punto a punto primarie e secondarie (per il protocollo BGP).</span><span class="sxs-lookup"><span data-stu-id="12f20-191">A successfully enabled peering context would also have the primary and secondary point-to-point (required for BGP) subnets listed.</span></span> <span data-ttu-id="12f20-192">Le /30 subnet vengono usate per l'indirizzo IP dell'interfaccia degli MSEE e PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="12f20-192">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span> 

>[!NOTE]
><span data-ttu-id="12f20-193">Se non è abilitato alcun peering, verificare se le subnet primarie e secondarie assegnate corrispondono alla configurazione su PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="12f20-193">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on PE-MSEEs.</span></span> <span data-ttu-id="12f20-194">In caso contrario, per modificare la configurazione sui router MSEE, fare riferimento a [Creare e modificare il routing per un circuito ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="12f20-194">If not, to change the configuration on MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>
>
>

###<a name="verification-via-powershell"></a><span data-ttu-id="12f20-195">Verifica tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="12f20-195">Verification via PowerShell</span></span>
<span data-ttu-id="12f20-196">Per ottenere i dettagli di configurazione del peering privato di Azure, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="12f20-196">To get the Azure private peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

<span data-ttu-id="12f20-197">Una risposta di esempio, per un peering privato configurato correttamente:</span><span class="sxs-lookup"><span data-stu-id="12f20-197">A sample response, for a successfully configured private peering, is:</span></span>

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

 <span data-ttu-id="12f20-198">In un contesto di peering abilitato correttamente vengono elencati i prefissi di indirizzi primari e secondari.</span><span class="sxs-lookup"><span data-stu-id="12f20-198">A successfully enabled peering context would have the primary and secondary address prefixes listed.</span></span> <span data-ttu-id="12f20-199">Le /30 subnet vengono usate per l'indirizzo IP dell'interfaccia degli MSEE e PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="12f20-199">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="12f20-200">Per ottenere i dettagli di configurazione del peering pubblico di Azure, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="12f20-200">To get the Azure public peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

<span data-ttu-id="12f20-201">Per ottenere i dettagli di configurazione del peering Microsoft, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="12f20-201">To get the Microsoft peering configuration details, use the following commands:</span></span>

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

<span data-ttu-id="12f20-202">Se non è configurato alcun peering, viene visualizzato un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="12f20-202">If a peering is not configured, there would be an error message.</span></span> <span data-ttu-id="12f20-203">Una risposta di esempio, quando il peering indicato (peering pubblico di Azure in questo esempio) non è configurato all'interno del circuito:</span><span class="sxs-lookup"><span data-stu-id="12f20-203">A sample response, when the stated peering (Azure Public peering in this example) is not configured within the circuit:</span></span>

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
><span data-ttu-id="12f20-204">Se non è abilitato alcun peering, verificare se le subnet primarie e secondarie assegnate corrispondono alla configurazione sul PE-MSEE collegato.</span><span class="sxs-lookup"><span data-stu-id="12f20-204">If a peering is not enabled, check if the primary and secondary subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="12f20-205">Controllare anche che siano usati i valori corretti *VlanId*, *AzureASN* e *PeerASN* sugli MSEE e che tali valori corrispondano a quelli usati sul PE-MSEE collegato.</span><span class="sxs-lookup"><span data-stu-id="12f20-205">Also check if the correct *VlanId*, *AzureASN*, and *PeerASN* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="12f20-206">Se si sceglie l'hash MD5, la chiave condivisa deve essere identica nella coppia MSEE e PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="12f20-206">If MD5 hashing is chosen, the shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="12f20-207">Per modificare la configurazione sui router MSEE, fare riferimento a [Creare e modificare il routing per un circuito ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="12f20-207">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>  
>
>

### <a name="verification-via-powershell-classic"></a><span data-ttu-id="12f20-208">Verifica tramite PowerShell (versione classica)</span><span class="sxs-lookup"><span data-stu-id="12f20-208">Verification via PowerShell (Classic)</span></span>
<span data-ttu-id="12f20-209">Per ottenere i dettagli di configurazione del peering privato di Azure, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="12f20-209">To get the Azure private peering configuration details, use the following command:</span></span>

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

<span data-ttu-id="12f20-210">Una risposta di esempio, per un peering privato configurato correttamente:</span><span class="sxs-lookup"><span data-stu-id="12f20-210">A sample response, for a successfully configured private peering is:</span></span>

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

<span data-ttu-id="12f20-211">In un contesto di peering abilitato correttamente vengono elencate le subnet peer primarie e secondarie.</span><span class="sxs-lookup"><span data-stu-id="12f20-211">A successfully, enabled peering context would have the primary and secondary peer subnets listed.</span></span> <span data-ttu-id="12f20-212">Le /30 subnet vengono usate per l'indirizzo IP dell'interfaccia degli MSEE e PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="12f20-212">The /30 subnets are used for the interface IP address of the MSEEs and PE-MSEEs.</span></span>

<span data-ttu-id="12f20-213">Per ottenere i dettagli di configurazione del peering pubblico di Azure, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="12f20-213">To get the Azure public peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

<span data-ttu-id="12f20-214">Per ottenere i dettagli di configurazione del peering Microsoft, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="12f20-214">To get the Microsoft peering configuration details, use the following commands:</span></span>

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
><span data-ttu-id="12f20-215">Se il provider di servizi ha impostato peering di livello 3, l'impostazione dei peering di ExpressRoute tramite il portale o PowerShell sovrascrive le impostazioni del provider di servizi.</span><span class="sxs-lookup"><span data-stu-id="12f20-215">If layer 3 peerings were set by the service provider, setting the ExpressRoute peerings via the portal or PowerShell overwrites the service provider settings.</span></span> <span data-ttu-id="12f20-216">La riconfigurazione delle impostazioni di peering lato provider richiede il supporto del provider di servizi.</span><span class="sxs-lookup"><span data-stu-id="12f20-216">Resetting the provider side peering settings requires the support of the service provider.</span></span> <span data-ttu-id="12f20-217">Modificare i peering di ExpressRoute solo se si è certi che il provider di servizi offre esclusivamente servizi di livello 2.</span><span class="sxs-lookup"><span data-stu-id="12f20-217">Only modify the ExpressRoute peerings if it is certain that the service provider is providing layer 2 services only!</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="12f20-218">Se non è abilitato alcun peering, verificare se le subnet peer primarie e secondarie assegnate corrispondono alla configurazione sul PE-MSEE collegato.</span><span class="sxs-lookup"><span data-stu-id="12f20-218">If a peering is not enabled, check if the primary and secondary peer subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="12f20-219">Controllare anche che siano usati i valori corretti *VlanId*, *AzureASN* e *PeerASN* sugli MSEE e che tali valori corrispondano a quelli usati sul PE-MSEE collegato.</span><span class="sxs-lookup"><span data-stu-id="12f20-219">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="12f20-220">Per modificare la configurazione sui router MSEE, fare riferimento a [Creare e modificare il routing per un circuito ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="12f20-220">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

## <a name="validate-arp-between-microsoft-and-the-service-provider"></a><span data-ttu-id="12f20-221">Convalidare ARP tra Microsoft e il provider di servizi</span><span class="sxs-lookup"><span data-stu-id="12f20-221">Validate ARP between Microsoft and the service provider</span></span>
<span data-ttu-id="12f20-222">In questa sezione vengono usati i comandi di PowerShell (versione classica).</span><span class="sxs-lookup"><span data-stu-id="12f20-222">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="12f20-223">Se si usano i comandi di PowerShell basati su Azure Resource Manager, assicurarsi di disporre dell'accesso di amministratore/coamministratore alla sottoscrizione tramite il [portale di Azure classico][OldPortal].</span><span class="sxs-lookup"><span data-stu-id="12f20-223">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal].</span></span> <span data-ttu-id="12f20-224">Per la risoluzione dei problemi tramite i comandi di Azure Resource Manager, vedere il documento [Recupero di tabelle ARP nel modello di distribuzione Resource Manager][ARP].</span><span class="sxs-lookup"><span data-stu-id="12f20-224">For troubleshooting using Azure Resource Manager commands please refer to the [Getting ARP tables in the Resource Manager deployment model][ARP] document.</span></span>

>[!NOTE]
><span data-ttu-id="12f20-225">Per ottenere ARP, è possibile usare sia il portale di Azure sia i comandi di PowerShell basati su Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="12f20-225">To get ARP, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="12f20-226">In caso di errori con i comandi di PowerShell basati su Azure Resource Manager, i comandi classici di PowerShell dovrebbero essere operativi in quanto tali comandi funzionano anche con circuiti ExpressRoute in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="12f20-226">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as Classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="12f20-227">Per ottenere la tabella ARP dal router MSEE primario per il peering privato, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="12f20-227">To get the ARP table from the primary MSEE router for the private peering, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="12f20-228">Un esempio di risposta per il comando, nello scenario di esito positivo:</span><span class="sxs-lookup"><span data-stu-id="12f20-228">An example response for the command, in the successful scenario:</span></span>

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

<span data-ttu-id="12f20-229">Allo stesso modo è possibile controllare la tabella ARP dal MSEE nel percorso *Primary*/*Secondary* per peering *Private*/*Public*/*Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="12f20-229">Similarly, you can check the ARP table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* peerings.</span></span>

<span data-ttu-id="12f20-230">L'esempio seguente mostra la risposta del comando per un peering inesistente.</span><span class="sxs-lookup"><span data-stu-id="12f20-230">The following example shows the response of the command for a peering does not exist.</span></span>

    ARP Info:
       
>[!NOTE]
><span data-ttu-id="12f20-231">Se la tabella ARP non dispone di indirizzi IP delle interfacce associate agli indirizzi MAC, esaminare le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="12f20-231">If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:</span></span>
>1. <span data-ttu-id="12f20-232">Se il primo indirizzo IP delle /30 subnet assegnate per il collegamento tra il MSEE-PR e il MSEE viene usato nell'interfaccia di MSEE-PR.</span><span class="sxs-lookup"><span data-stu-id="12f20-232">If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR.</span></span> <span data-ttu-id="12f20-233">Azure usa sempre il secondo indirizzo IP per MSEE.</span><span class="sxs-lookup"><span data-stu-id="12f20-233">Azure always uses the second IP address for MSEEs.</span></span>
>2. <span data-ttu-id="12f20-234">Verificare se i tag VLAN del cliente (C-Tag) e del servizio (S-Tag) corrispondono nella coppia MSEE-PR e MSEE.</span><span class="sxs-lookup"><span data-stu-id="12f20-234">Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
>
>

## <a name="validate-bgp-and-routes-on-the-msee"></a><span data-ttu-id="12f20-235">Convalidare BGP e route sul MSEE</span><span class="sxs-lookup"><span data-stu-id="12f20-235">Validate BGP and routes on the MSEE</span></span>
<span data-ttu-id="12f20-236">In questa sezione vengono usati i comandi di PowerShell (versione classica).</span><span class="sxs-lookup"><span data-stu-id="12f20-236">This section uses PowerShell (Classic) commands.</span></span> <span data-ttu-id="12f20-237">Se si usano i comandi di PowerShell basati su Azure Resource Manager, assicurarsi di disporre dell'accesso di amministratore/coamministratore alla sottoscrizione tramite il [portale di Azure classico][OldPortal]</span><span class="sxs-lookup"><span data-stu-id="12f20-237">If you have been using PowerShell Azure Resource Manager commands, ensure that you have admin/co-admin access to the subscription via [Azure classic portal][OldPortal]</span></span>

>[!NOTE]
><span data-ttu-id="12f20-238">Per ottenere informazioni BGP, è possibile usare sia il portale di Azure sia i comandi di PowerShell basati su Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="12f20-238">To get BGP information, both the Azure portal and Azure Resource Manager PowerShell commands can be used.</span></span> <span data-ttu-id="12f20-239">In caso di errori con i comandi di PowerShell basati su Azure Resource Manager, i comandi classici di PowerShell dovrebbero essere operativi in quanto tali comandi funzionano anche con circuiti ExpressRoute in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="12f20-239">If errors are encountered with the Azure Resource Manager PowerShell commands, classic PowerShell commands should work as classic PowerShell commands also work with Azure Resource Manager ExpressRoute circuits.</span></span>
>
>

<span data-ttu-id="12f20-240">Per ottenere il riepilogo della tabella di routing (BGP adiacente) per un particolare contesto di routing, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="12f20-240">To get the routing table (BGP neighbor) summary for a particular routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="12f20-241">Una risposta di esempio:</span><span class="sxs-lookup"><span data-stu-id="12f20-241">An example response is:</span></span>

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

<span data-ttu-id="12f20-242">Come illustrato nell'esempio precedente, il comando è utile per determinare da quanto tempo è stato stabilito il contesto di routing.</span><span class="sxs-lookup"><span data-stu-id="12f20-242">As shown in the preceding example, the command is useful to determine for how long the routing context has been established.</span></span> <span data-ttu-id="12f20-243">Indica inoltre il numero di prefissi di route annunciati dal router di peering.</span><span class="sxs-lookup"><span data-stu-id="12f20-243">It also indicates number of route prefixes advertised by the peering router.</span></span>

>[!NOTE]
><span data-ttu-id="12f20-244">Se lo stato è attivo o inattivo, verificare se le subnet peer primarie e secondarie assegnate corrispondono alla configurazione sul PE-MSEE collegato.</span><span class="sxs-lookup"><span data-stu-id="12f20-244">If the state is in Active or Idle, check if the primary and secondary peer subnets assigned match the configuration on the linked PE-MSEE.</span></span> <span data-ttu-id="12f20-245">Controllare anche che siano usati i valori corretti *VlanId*, *AzureASN* e *PeerASN* sugli MSEE e che tali valori corrispondano a quelli usati sul PE-MSEE collegato.</span><span class="sxs-lookup"><span data-stu-id="12f20-245">Also check if the correct *VlanId*, *AzureAsn*, and *PeerAsn* are used on MSEEs and if these values maps to the ones used on the linked PE-MSEE.</span></span> <span data-ttu-id="12f20-246">Se si sceglie l'hash MD5, la chiave condivisa deve essere identica nella coppia MSEE e PE-MSEE.</span><span class="sxs-lookup"><span data-stu-id="12f20-246">If MD5 hashing is chosen, the shared key should be same on MSEE and PE-MSEE pair.</span></span> <span data-ttu-id="12f20-247">Per modificare la configurazione sui router MSEE, fare riferimento a [Creare e modificare il routing per un circuito ExpressRoute][CreatePeering].</span><span class="sxs-lookup"><span data-stu-id="12f20-247">To change the configuration on the MSEE routers, refer to [Create and modify routing for an ExpressRoute circuit][CreatePeering].</span></span>
>
>

<p/>
>[!NOTE]
><span data-ttu-id="12f20-248">Se alcune destinazioni non sono raggiungibili tramite un particolare peering, controllare la tabella di route dei MSEE appartenente al contesto di peering specifico.</span><span class="sxs-lookup"><span data-stu-id="12f20-248">If certain destinations are not reachable over a particular peering, check the route table of the MSEEs belonging to the particular peering context.</span></span> <span data-ttu-id="12f20-249">Se un prefisso corrispondente, ad esempio un IP su cui è stato eseguito il NAT, questo è presente nella tabella di routing, controllare che ci siano firewalls/NSG/ACLs nel percorso e che questi consentano il traffico.</span><span class="sxs-lookup"><span data-stu-id="12f20-249">If a matching prefix (could be NATed IP) is present in the routing table, then check if there are firewalls/NSG/ACLs on the path and if they permit the traffic.</span></span>
>
>

<span data-ttu-id="12f20-250">Per ottenere la tabella di routing completa da MSEE sul percorso *Primary* per il contesto di routing *Private* specifico, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="12f20-250">To get the full routing table from MSEE on the *Primary* path for the particular *Private* routing context, use the following command:</span></span>

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

<span data-ttu-id="12f20-251">Un risultato positivo di esempio per il comando:</span><span class="sxs-lookup"><span data-stu-id="12f20-251">An example successful outcome for the command is:</span></span>

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

<span data-ttu-id="12f20-252">Allo stesso modo è possibile controllare la tabella di routing dal MSEE nel percorso *Primary*/*Secondary*, per un contesto di peering *Private*/*Public*/*Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="12f20-252">Similarly, you can check the routing table from the MSEE in the *Primary*/*Secondary* path, for *Private*/*Public*/*Microsoft* a peering context.</span></span>

<span data-ttu-id="12f20-253">L'esempio seguente mostra la risposta del comando per un peering inesistente:</span><span class="sxs-lookup"><span data-stu-id="12f20-253">The following example shows the response of the command for a peering does not exist:</span></span>

    Route Table Info:

##<a name="check-the-traffic-statistics"></a><span data-ttu-id="12f20-254">Controllare le statistiche sul traffico</span><span class="sxs-lookup"><span data-stu-id="12f20-254">Check the Traffic Statistics</span></span>
<span data-ttu-id="12f20-255">Per ottenere le statistiche sul traffico del percorso primario e secondario combinato, byte in entrata e in uscita, di un contesto di peering, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="12f20-255">To get the combined primary and secondary path traffic statistics--bytes in and out--of a peering context, use the following command:</span></span>

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

<span data-ttu-id="12f20-256">Output di esempio del comando:</span><span class="sxs-lookup"><span data-stu-id="12f20-256">A sample output of the command is:</span></span>

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

<span data-ttu-id="12f20-257">Output di esempio del comando per un peering inesistente:</span><span class="sxs-lookup"><span data-stu-id="12f20-257">A sample output of the command for a non-existent peering is:</span></span>

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a><span data-ttu-id="12f20-258">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="12f20-258">Next Steps</span></span>
<span data-ttu-id="12f20-259">Per maggiori informazioni o assistenza, consultare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="12f20-259">For more information or help, check out the following links:</span></span>

- <span data-ttu-id="12f20-260">[Supporto tecnico Microsoft][Support]</span><span class="sxs-lookup"><span data-stu-id="12f20-260">[Microsoft Support][Support]</span></span>
- <span data-ttu-id="12f20-261">[Creare e modificare un circuito ExpressRoute][CreateCircuit]</span><span class="sxs-lookup"><span data-stu-id="12f20-261">[Create and modify an ExpressRoute circuit][CreateCircuit]</span></span>
- <span data-ttu-id="12f20-262">[Creare e modificare il routing per un circuito ExpressRoute][CreatePeering]</span><span class="sxs-lookup"><span data-stu-id="12f20-262">[Create and modify routing for an ExpressRoute circuit][CreatePeering]</span></span>

<!--Image References-->
<span data-ttu-id="12f20-263">[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Connettività logica ExpressRoute"</span><span class="sxs-lookup"><span data-stu-id="12f20-263">[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Logical Express Route Connectivity"</span></span>
<span data-ttu-id="12f20-264">[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Icona All resources"</span><span class="sxs-lookup"><span data-stu-id="12f20-264">[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "All resources icon"</span></span>
<span data-ttu-id="12f20-265">[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Icona Overview"</span><span class="sxs-lookup"><span data-stu-id="12f20-265">[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Overview icon"</span></span>
<span data-ttu-id="12f20-266">[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Schermata di esempio delle informazioni di base di ExpressRoute"</span><span class="sxs-lookup"><span data-stu-id="12f20-266">[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute Essentials sample screenshot"</span></span>
<span data-ttu-id="12f20-267">[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Schermata di esempio delle informazioni di base di ExpressRoute"</span><span class="sxs-lookup"><span data-stu-id="12f20-267">[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute Essentials sample screenshot"</span></span>

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






