---
title: 'Come configurare il routing (peering) per un circuito ExpressRoute: Azure: versione classica | Documentazione Microsoft'
description: Questo articolo descrive come creare ed eseguire il provisioning di un circuito ExpressRoute per il peering privato, il peering pubblico e il peering Microsoft. Questo articolo mostra anche come controllare lo stato e aggiornare o eliminare i peering per un circuito.
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
ms.openlocfilehash: 37713db70f3ae837edafc997b78b16b121d0a885
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a><span data-ttu-id="3205a-104">Creare e modificare il peering per un circuito ExpressRoute (versione classica)</span><span class="sxs-lookup"><span data-stu-id="3205a-104">Create and modify peering for an ExpressRoute circuit (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3205a-105">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3205a-105">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="3205a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3205a-106">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="3205a-107">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="3205a-107">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="3205a-108">Video - Peering privato</span><span class="sxs-lookup"><span data-stu-id="3205a-108">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="3205a-109">Video - Peering pubblico</span><span class="sxs-lookup"><span data-stu-id="3205a-109">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="3205a-110">Video - Peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="3205a-110">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="3205a-111">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="3205a-111">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

<span data-ttu-id="3205a-112">Questo articolo descrive le procedure per creare e gestire la configurazione di routing per un circuito ExpressRoute usando PowerShell e il modello di distribuzione classico.</span><span class="sxs-lookup"><span data-stu-id="3205a-112">This article walks you through the steps to create and manage routing configuration for an ExpressRoute circuit using PowerShell and the classic deployment model.</span></span> <span data-ttu-id="3205a-113">La procedura seguente mostra anche come controllare lo stato e aggiornare, eliminare o effettuare il deprovisioning dei peering per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3205a-113">The steps below will also show you how to check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span>

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="3205a-114">**Informazioni sui modelli di distribuzione di Azure**</span><span class="sxs-lookup"><span data-stu-id="3205a-114">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a><span data-ttu-id="3205a-115">Prerequisiti di configurazione</span><span class="sxs-lookup"><span data-stu-id="3205a-115">Configuration prerequisites</span></span>
* <span data-ttu-id="3205a-116">È necessaria la versione più recente dei cmdlet di PowerShell per Gestione dei servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="3205a-116">You will need the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="3205a-117">Per altre informazioni, vedere [Introduzione ai cmdlet di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3205a-117">For more information, see [Getting started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="3205a-118">Prima di iniziare la configurazione, assicurarsi di aver letto le pagine relative ai [prerequisiti](expressroute-prerequisites.md), ai [requisiti per il routing](expressroute-routing.md) e ai [flussi di lavoro](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="3205a-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="3205a-119">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="3205a-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="3205a-120">Seguire le istruzioni per [creare un circuito ExpressRoute](expressroute-howto-circuit-classic.md) e fare in modo che venga abilitato dal provider di connettività prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="3205a-120">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="3205a-121">Per poter eseguire i cmdlet descritti di seguito deve essere stato effettuato il provisioning del circuito ExpressRoute e lo stato del circuito deve essere abilitato.</span><span class="sxs-lookup"><span data-stu-id="3205a-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets described below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3205a-122">Queste istruzioni si applicano solo ai circuiti creati con provider di servizi che offrono servizi di connettività di livello 2.</span><span class="sxs-lookup"><span data-stu-id="3205a-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="3205a-123">Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito un IPVPN, come MPLS), il provider di connettività configurerà e gestirà il routing per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="3205a-123">If you are using a service provider offering managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

<span data-ttu-id="3205a-124">Per un circuito ExpressRoute è possibile configurare uno, due o tutti e tre i peering (peering privato di Azure, peering pubblico di Azure e peering Microsoft).</span><span class="sxs-lookup"><span data-stu-id="3205a-124">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="3205a-125">È possibile configurare i peering nell'ordine desiderato.</span><span class="sxs-lookup"><span data-stu-id="3205a-125">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="3205a-126">assicurandosi, tuttavia, di completare la configurazione di un peering per volta.</span><span class="sxs-lookup"><span data-stu-id="3205a-126">However, you must make sure that you complete the configuration of each peering one at a time.</span></span>


### <a name="log-in-to-your-azure-account-and-select-a-subscription"></a><span data-ttu-id="3205a-127">Accedere all'account Azure e selezionare una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="3205a-127">Log in to your Azure account and select a subscription</span></span>
1. <span data-ttu-id="3205a-128">Aprire la console di PowerShell con diritti elevati e connettersi all'account.</span><span class="sxs-lookup"><span data-stu-id="3205a-128">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="3205a-129">Per eseguire la connessione, usare gli esempi che seguono:</span><span class="sxs-lookup"><span data-stu-id="3205a-129">Use the following example to help you connect:</span></span>

        Login-AzureRmAccount

2. <span data-ttu-id="3205a-130">Controllare le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="3205a-130">Check the subscriptions for the account.</span></span>

        Get-AzureRmSubscription

3. <span data-ttu-id="3205a-131">Se sono disponibili più sottoscrizioni, selezionare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="3205a-131">If you have more than one subscription, select the subscription that you want to use.</span></span>

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. <span data-ttu-id="3205a-132">Successivamente, utilizzare il cmdlet seguente per aggiungere la sottoscrizione di Azure a PowerShell per il modello di distribuzione classico.</span><span class="sxs-lookup"><span data-stu-id="3205a-132">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

        Add-AzureAccount


## <a name="azure-private-peering"></a><span data-ttu-id="3205a-133">Peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="3205a-133">Azure private peering</span></span>
<span data-ttu-id="3205a-134">Questa sezione fornisce le istruzioni per creare, ottenere, aggiornare ed eliminare la configurazione del peering privato di Azure per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3205a-134">This section provides instructions on how to create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="3205a-135">Per creare un peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="3205a-135">To create Azure private peering</span></span>
1. <span data-ttu-id="3205a-136">**Importare il modulo PowerShell per ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="3205a-136">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="3205a-137">Per iniziare a usare i cmdlet per ExpressRoute, è necessario importare i moduli di Azure ed ExpressRoute nella sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3205a-137">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="3205a-138">Per importare i moduli di Azure ed ExpressRoute nella sessione di PowerShell, eseguire i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="3205a-138">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="3205a-139">**Creare un circuito ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="3205a-139">**Create an ExpressRoute circuit.**</span></span>
   
    <span data-ttu-id="3205a-140">Seguire le istruzioni per creare un [circuito ExpressRoute](expressroute-howto-circuit-classic.md) e chiedere al provider di connettività di effettuarne il provisioning.</span><span class="sxs-lookup"><span data-stu-id="3205a-140">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="3205a-141">Se il provider di connettività offre servizi gestiti di livello 3, è possibile chiedere al provider di connettività di abilitare il peering privato di Azure.</span><span class="sxs-lookup"><span data-stu-id="3205a-141">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="3205a-142">In questo caso, non sarà necessario seguire le istruzioni riportate nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="3205a-142">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="3205a-143">Se invece il provider di connettività non gestisce il routing per conto dell'utente, dopo aver creato il circuito, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="3205a-143">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span> 
3. <span data-ttu-id="3205a-144">**Verificare che sia stato effettuato il provisioning del circuito ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="3205a-144">**Check the ExpressRoute circuit to ensure it is provisioned.**</span></span>
   
    <span data-ttu-id="3205a-145">In primo luogo, è necessario verificare se è stato effettuato il provisioning del circuito ExpressRoute e se il circuito è abilitato.</span><span class="sxs-lookup"><span data-stu-id="3205a-145">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="3205a-146">Vedere l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="3205a-146">See the example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="3205a-147">Assicurarsi che lo stato visualizzato per il circuito sia Provisioning eseguito e Abilitato.</span><span class="sxs-lookup"><span data-stu-id="3205a-147">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="3205a-148">In caso contrario, rivolgersi al provider di connettività affinché imposti gli stati necessari per il circuito.</span><span class="sxs-lookup"><span data-stu-id="3205a-148">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="3205a-149">**Configurare il peering privato di Azure per il circuito.**</span><span class="sxs-lookup"><span data-stu-id="3205a-149">**Configure Azure private peering for the circuit.**</span></span>
   
    <span data-ttu-id="3205a-150">Prima di procedere con i passaggi successivi, verificare che siano presenti gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3205a-150">Make sure that you have the following items before you proceed with the next steps:</span></span>
   
   * <span data-ttu-id="3205a-151">Una subnet /30 per il collegamento primario.</span><span class="sxs-lookup"><span data-stu-id="3205a-151">A /30 subnet for the primary link.</span></span> <span data-ttu-id="3205a-152">Non deve far parte di alcuno spazio indirizzi riservato per le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="3205a-152">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="3205a-153">Una subnet /30 per il collegamento secondario.</span><span class="sxs-lookup"><span data-stu-id="3205a-153">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="3205a-154">Non deve far parte di alcuno spazio indirizzi riservato per le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="3205a-154">This must not be part of any address space reserved for virtual networks.</span></span>
   * <span data-ttu-id="3205a-155">Un ID VLAN valido su cui stabilire questo peering.</span><span class="sxs-lookup"><span data-stu-id="3205a-155">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="3205a-156">Assicurarsi che nessun altro peering nel circuito usi lo stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="3205a-156">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="3205a-157">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="3205a-157">AS number for peering.</span></span> <span data-ttu-id="3205a-158">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="3205a-158">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="3205a-159">È possibile usare il numero AS privato per questo peering.</span><span class="sxs-lookup"><span data-stu-id="3205a-159">You can use a private AS number for this peering.</span></span> <span data-ttu-id="3205a-160">Assicurarsi di non usare il numero 65515.</span><span class="sxs-lookup"><span data-stu-id="3205a-160">Ensure that you are not using 65515.</span></span>
   * <span data-ttu-id="3205a-161">Un hash MD5, se si sceglie di usarne uno.</span><span class="sxs-lookup"><span data-stu-id="3205a-161">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="3205a-162">**Facoltativo**.</span><span class="sxs-lookup"><span data-stu-id="3205a-162">**This is optional**.</span></span>
     
    <span data-ttu-id="3205a-163">Per configurare il peering privato di Azure per il circuito, eseguire il cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="3205a-163">You can run the following cmdlet to configure Azure private peering for your circuit.</span></span>
     
        <span data-ttu-id="3205a-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span><span class="sxs-lookup"><span data-stu-id="3205a-164">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100</span></span>
     
    <span data-ttu-id="3205a-165">Se si sceglie di usare un hash MD5, eseguire il cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="3205a-165">You can use the cmdlet below if you choose to use an MD5 hash.</span></span>
     
        <span data-ttu-id="3205a-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="3205a-166">New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="3205a-167">Assicurarsi di specificare il numero AS come ASN di peering e non come ASN cliente.</span><span class="sxs-lookup"><span data-stu-id="3205a-167">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
     > 
     > 

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="3205a-168">Per visualizzare i dettagli relativi al peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="3205a-168">To view Azure private peering details</span></span>
<span data-ttu-id="3205a-169">Per ottenere i dettagli di configurazione, usare il cmdlet seguente</span><span class="sxs-lookup"><span data-stu-id="3205a-169">You can get configuration details using the following cmdlet</span></span>

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


### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="3205a-170">Per aggiornare la configurazione del peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="3205a-170">To update Azure private peering configuration</span></span>
<span data-ttu-id="3205a-171">Per aggiornare qualsiasi parte della configurazione, usare il cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="3205a-171">You can update any part of the configuration using the following cmdlet.</span></span> <span data-ttu-id="3205a-172">Nell'esempio seguente il valore dell'ID VLAN del circuito viene aggiornato da 100 a 500.</span><span class="sxs-lookup"><span data-stu-id="3205a-172">In the example below, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="3205a-173">Per eliminare un peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="3205a-173">To delete Azure private peering</span></span>
<span data-ttu-id="3205a-174">Per rimuovere la configurazione di peering, eseguire il cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="3205a-174">You can remove your peering configuration by running the following cmdlet.</span></span>

> [!WARNING]
> <span data-ttu-id="3205a-175">Assicurarsi che tutte le reti virtuali siano scollegate dal circuito ExpressRoute prima di eseguire questo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3205a-175">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this cmdlet.</span></span> 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a><span data-ttu-id="3205a-176">Peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="3205a-176">Azure public peering</span></span>
<span data-ttu-id="3205a-177">Questa sezione fornisce le istruzioni per creare, ottenere, aggiornare ed eliminare la configurazione del peering pubblico di Azure per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3205a-177">This section provides instructions on how to create, get, update and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="3205a-178">Per creare un peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="3205a-178">To create Azure public peering</span></span>
1. <span data-ttu-id="3205a-179">**Importare il modulo PowerShell per ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="3205a-179">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="3205a-180">Per iniziare a usare i cmdlet per ExpressRoute, è necessario importare i moduli di Azure ed ExpressRoute nella sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3205a-180">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="3205a-181">Per importare i moduli di Azure ed ExpressRoute nella sessione di PowerShell, eseguire i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="3205a-181">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span> 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="3205a-182">**Creare un circuito ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="3205a-182">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="3205a-183">Seguire le istruzioni per creare un [circuito ExpressRoute](expressroute-howto-circuit-classic.md) e chiedere al provider di connettività di effettuarne il provisioning.</span><span class="sxs-lookup"><span data-stu-id="3205a-183">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="3205a-184">Se il provider di connettività offre servizi gestiti di livello 3, è possibile chiedere al provider di abilitare il peering privato di Azure.</span><span class="sxs-lookup"><span data-stu-id="3205a-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure public peering for you.</span></span> <span data-ttu-id="3205a-185">In questo caso, non sarà necessario seguire le istruzioni riportate nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="3205a-185">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="3205a-186">Se invece il provider di connettività non gestisce il routing per conto dell'utente, dopo aver creato il circuito, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="3205a-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
3. <span data-ttu-id="3205a-187">**Verificare che sia stato eseguito il provisioning del circuito ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="3205a-187">**Check ExpressRoute circuit to ensure it is provisioned**</span></span>
   
    <span data-ttu-id="3205a-188">In primo luogo, è necessario verificare se è stato effettuato il provisioning del circuito ExpressRoute e se il circuito è abilitato.</span><span class="sxs-lookup"><span data-stu-id="3205a-188">You must first check to see if the ExpressRoute circuit is Provisioned and also Enabled.</span></span> <span data-ttu-id="3205a-189">Vedere l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="3205a-189">See the example below.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="3205a-190">Assicurarsi che lo stato visualizzato per il circuito sia Provisioning eseguito e Abilitato.</span><span class="sxs-lookup"><span data-stu-id="3205a-190">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="3205a-191">In caso contrario, rivolgersi al provider di connettività affinché imposti gli stati necessari per il circuito.</span><span class="sxs-lookup"><span data-stu-id="3205a-191">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="3205a-192">**Configurare il peering pubblico di Azure per il circuito**</span><span class="sxs-lookup"><span data-stu-id="3205a-192">**Configure Azure public peering for the circuit**</span></span>
   
    <span data-ttu-id="3205a-193">Prima di procedere, verificare che siano presenti gli elementi seguenti.</span><span class="sxs-lookup"><span data-stu-id="3205a-193">Ensure that you have the following information before you proceed further.</span></span>
   
   * <span data-ttu-id="3205a-194">Una subnet /30 per il collegamento primario.</span><span class="sxs-lookup"><span data-stu-id="3205a-194">A /30 subnet for the primary link.</span></span> <span data-ttu-id="3205a-195">Deve essere un prefisso IPv4 pubblico valido.</span><span class="sxs-lookup"><span data-stu-id="3205a-195">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="3205a-196">Una subnet /30 per il collegamento secondario.</span><span class="sxs-lookup"><span data-stu-id="3205a-196">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="3205a-197">Deve essere un prefisso IPv4 pubblico valido.</span><span class="sxs-lookup"><span data-stu-id="3205a-197">This must be a valid public IPv4 prefix.</span></span>
   * <span data-ttu-id="3205a-198">Un ID VLAN valido su cui stabilire questo peering.</span><span class="sxs-lookup"><span data-stu-id="3205a-198">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="3205a-199">Assicurarsi che nessun altro peering nel circuito usi lo stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="3205a-199">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="3205a-200">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="3205a-200">AS number for peering.</span></span> <span data-ttu-id="3205a-201">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="3205a-201">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="3205a-202">Un hash MD5, se si sceglie di usarne uno.</span><span class="sxs-lookup"><span data-stu-id="3205a-202">An MD5 hash if you choose to use one.</span></span> <span data-ttu-id="3205a-203">**Facoltativo**.</span><span class="sxs-lookup"><span data-stu-id="3205a-203">**This is optional**.</span></span>
     
    <span data-ttu-id="3205a-204">Per configurare il peering pubblico di Azure per il circuito, è possibile eseguire il cmdlet seguente</span><span class="sxs-lookup"><span data-stu-id="3205a-204">You can run the following cmdlet to configure Azure public peering for your circuit</span></span>
     
        <span data-ttu-id="3205a-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span><span class="sxs-lookup"><span data-stu-id="3205a-205">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200</span></span>
     
    <span data-ttu-id="3205a-206">Se si sceglie di usare un hash MD5, eseguire il cmdlet seguente</span><span class="sxs-lookup"><span data-stu-id="3205a-206">You can use the cmdlet below if you choose to use an MD5 hash</span></span>
     
        <span data-ttu-id="3205a-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="3205a-207">New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="3205a-208">Assicurarsi di specificare il numero AS come ASN di peering e non come ASN cliente.</span><span class="sxs-lookup"><span data-stu-id="3205a-208">Ensure that you specify your AS number as peering ASN and not customer ASN.</span></span>
     > 
     > 

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="3205a-209">Per visualizzare i dettagli relativi al peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="3205a-209">To view Azure public peering details</span></span>
<span data-ttu-id="3205a-210">Per ottenere i dettagli di configurazione, usare il cmdlet seguente</span><span class="sxs-lookup"><span data-stu-id="3205a-210">You can get configuration details using the following cmdlet</span></span>

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


### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="3205a-211">Per aggiornare la configurazione del peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="3205a-211">To update Azure public peering configuration</span></span>
<span data-ttu-id="3205a-212">Per aggiornare qualsiasi parte della configurazione, usare il cmdlet seguente</span><span class="sxs-lookup"><span data-stu-id="3205a-212">You can update any part of the configuration using the following cmdlet</span></span>

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

<span data-ttu-id="3205a-213">Nell'esempio precedente il valore dell'ID VLAN è stato aggiornato da 200 a 600.</span><span class="sxs-lookup"><span data-stu-id="3205a-213">The VLAN ID of the circuit is being updated from 200 to 600 in the above example.</span></span>

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="3205a-214">Per eliminare un peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="3205a-214">To delete Azure public peering</span></span>
<span data-ttu-id="3205a-215">Per rimuovere la configurazione di peering, eseguire il cmdlet seguente</span><span class="sxs-lookup"><span data-stu-id="3205a-215">You can remove your peering configuration by running the following cmdlet</span></span>

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a><span data-ttu-id="3205a-216">Peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="3205a-216">Microsoft peering</span></span>
<span data-ttu-id="3205a-217">Questa sezione fornisce le istruzioni per creare, ottenere, aggiornare ed eliminare la configurazione del peering Microsoft per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3205a-217">This section provides instructions on how to create, get, update and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="3205a-218">Per creare il peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="3205a-218">To create Microsoft peering</span></span>
1. <span data-ttu-id="3205a-219">**Importare il modulo PowerShell per ExpressRoute.**</span><span class="sxs-lookup"><span data-stu-id="3205a-219">**Import the PowerShell module for ExpressRoute.**</span></span>
   
    <span data-ttu-id="3205a-220">Per iniziare a usare i cmdlet per ExpressRoute, è necessario importare i moduli di Azure ed ExpressRoute nella sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3205a-220">You must import the Azure and ExpressRoute modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="3205a-221">Per importare i moduli di Azure ed ExpressRoute nella sessione di PowerShell, eseguire i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="3205a-221">Run the following commands to import the Azure and ExpressRoute modules into the PowerShell session.</span></span>  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. <span data-ttu-id="3205a-222">**Creare un circuito ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="3205a-222">**Create an ExpressRoute circuit**</span></span>
   
    <span data-ttu-id="3205a-223">Seguire le istruzioni per creare un [circuito ExpressRoute](expressroute-howto-circuit-classic.md) e chiedere al provider di connettività di effettuarne il provisioning.</span><span class="sxs-lookup"><span data-stu-id="3205a-223">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-classic.md) and have it provisioned by the connectivity provider.</span></span> <span data-ttu-id="3205a-224">Se il provider di connettività offre servizi gestiti di livello 3, è possibile chiedere al provider di connettività di abilitare il peering privato di Azure.</span><span class="sxs-lookup"><span data-stu-id="3205a-224">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="3205a-225">In questo caso, non sarà necessario seguire le istruzioni riportate nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="3205a-225">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="3205a-226">Se invece il provider di connettività non gestisce il routing per conto dell'utente, dopo aver creato il circuito, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="3205a-226">However, if your connectivity provider does not manage routing for you, after creating your circuit, follow the instructions below.</span></span>
3. <span data-ttu-id="3205a-227">**Verificare che sia stato eseguito il provisioning del circuito ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="3205a-227">**Check ExpressRoute circuit to ensure it is provisioned**</span></span>
   
    <span data-ttu-id="3205a-228">In primo luogo, è necessario verificare se è stato eseguito il provisioning del circuito ExpressRoute e se il circuito è abilitato.</span><span class="sxs-lookup"><span data-stu-id="3205a-228">You must first check to see if the ExpressRoute circuit is in Provisioned and Enabled state.</span></span>
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    <span data-ttu-id="3205a-229">Assicurarsi che lo stato visualizzato per il circuito sia Provisioning eseguito e Abilitato.</span><span class="sxs-lookup"><span data-stu-id="3205a-229">Make sure that the circuit shows as Provisioned and Enabled.</span></span> <span data-ttu-id="3205a-230">In caso contrario, rivolgersi al provider di connettività affinché imposti gli stati necessari per il circuito.</span><span class="sxs-lookup"><span data-stu-id="3205a-230">If it doesn't, work with your connectivity provider to get your circuit to the required state and status.</span></span>
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. <span data-ttu-id="3205a-231">**Configurare il peering Microsoft per il circuito**</span><span class="sxs-lookup"><span data-stu-id="3205a-231">**Configure Microsoft peering for the circuit**</span></span>
   
    <span data-ttu-id="3205a-232">Prima di procedere, verificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="3205a-232">Make sure that you have the following information before you proceed.</span></span>
   
   * <span data-ttu-id="3205a-233">Una subnet /30 per il collegamento primario.</span><span class="sxs-lookup"><span data-stu-id="3205a-233">A /30 subnet for the primary link.</span></span> <span data-ttu-id="3205a-234">Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.</span><span class="sxs-lookup"><span data-stu-id="3205a-234">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="3205a-235">Una subnet /30 per il collegamento secondario.</span><span class="sxs-lookup"><span data-stu-id="3205a-235">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="3205a-236">Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.</span><span class="sxs-lookup"><span data-stu-id="3205a-236">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
   * <span data-ttu-id="3205a-237">Un ID VLAN valido su cui stabilire questo peering.</span><span class="sxs-lookup"><span data-stu-id="3205a-237">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="3205a-238">Assicurarsi che nessun altro peering nel circuito usi lo stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="3205a-238">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
   * <span data-ttu-id="3205a-239">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="3205a-239">AS number for peering.</span></span> <span data-ttu-id="3205a-240">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="3205a-240">You can use both 2-byte and 4-byte AS numbers.</span></span>
   * <span data-ttu-id="3205a-241">Advertised prefixes: è necessario fornire un elenco di tutti i prefissi che si intende pubblicizzare nella sessione BGP.</span><span class="sxs-lookup"><span data-stu-id="3205a-241">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="3205a-242">Sono accettati solo prefissi di indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="3205a-242">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="3205a-243">Per inviare un set di prefissi, è possibile creare un elenco con valori delimitati da virgole.</span><span class="sxs-lookup"><span data-stu-id="3205a-243">You can send a comma separated list if you plan to send a set of prefixes.</span></span> <span data-ttu-id="3205a-244">Questi prefissi devono essere intestati all'utente in un registro RIR o IRR.</span><span class="sxs-lookup"><span data-stu-id="3205a-244">These prefixes must be registered to you in an RIR / IRR.</span></span>
   * <span data-ttu-id="3205a-245">Customer ASN: se si annunciano prefissi registrati al numero AS di peering, è possibile specificare il numero AS a cui sono registrati.</span><span class="sxs-lookup"><span data-stu-id="3205a-245">Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span> <span data-ttu-id="3205a-246">**Facoltativo**.</span><span class="sxs-lookup"><span data-stu-id="3205a-246">**This is optional**.</span></span>
   * <span data-ttu-id="3205a-247">Routing Registry Name: è possibile specificare il registro RIR/IRR in cui sono registrati il numero AS e i prefissi.</span><span class="sxs-lookup"><span data-stu-id="3205a-247">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
   * <span data-ttu-id="3205a-248">Un hash MD5, se si sceglie di usarne uno.</span><span class="sxs-lookup"><span data-stu-id="3205a-248">An MD5 hash, if you choose to use one.</span></span> <span data-ttu-id="3205a-249">**Facoltativo.**</span><span class="sxs-lookup"><span data-stu-id="3205a-249">**This is optional.**</span></span>
     
    <span data-ttu-id="3205a-250">Per configurare il peering Microsoft per il circuito, eseguire il cmdlet seguente</span><span class="sxs-lookup"><span data-stu-id="3205a-250">You can run the following cmdlet to configure Microsoft pering for your circuit</span></span>
     
        <span data-ttu-id="3205a-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span><span class="sxs-lookup"><span data-stu-id="3205a-251">New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"</span></span>

### <a name="to-view-microsoft-peering-details"></a><span data-ttu-id="3205a-252">Per visualizzare i dettagli del peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="3205a-252">To view Microsoft peering details</span></span>
<span data-ttu-id="3205a-253">Per ottenere i dettagli di configurazione, usare il cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="3205a-253">You can get configuration details using the following cmdlet.</span></span>

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


### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="3205a-254">Per aggiornare la configurazione del peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="3205a-254">To update Microsoft peering configuration</span></span>
<span data-ttu-id="3205a-255">Per aggiornare qualsiasi parte della configurazione, usare il cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="3205a-255">You can update any part of the configuration using the following cmdlet.</span></span>

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="3205a-256">Per eliminare il peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="3205a-256">To delete Microsoft peering</span></span>
<span data-ttu-id="3205a-257">Per rimuovere la configurazione di peering, eseguire il cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="3205a-257">You can remove your peering configuration by running the following cmdlet.</span></span>

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a><span data-ttu-id="3205a-258">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3205a-258">Next steps</span></span>
<span data-ttu-id="3205a-259">Successivamente, [Collegare una rete virtuale a un circuito ExpressRoute](expressroute-howto-linkvnet-classic.md)</span><span class="sxs-lookup"><span data-stu-id="3205a-259">Next, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

* <span data-ttu-id="3205a-260">Per ulteriori informazioni sui flussi di lavoro, vedere [Flussi di lavoro ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="3205a-260">For more information about workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="3205a-261">Per altre informazioni sul peering del circuito, vedere l'articolo relativo ai [circuiti ExpressRoute e domini di routing](expressroute-circuit-peerings.md)</span><span class="sxs-lookup"><span data-stu-id="3205a-261">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>

