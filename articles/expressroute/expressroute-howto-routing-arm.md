---
title: 'Come tooconfigure routing (peering) per un circuito ExpressRoute: Gestione risorse: PowerShell: Azure | Documenti Microsoft'
description: In questo articolo vengono illustrati i passaggi hello per la creazione e il provisioning di hello privato, pubblico e peering Microsoft di un circuito ExpressRoute. Mostra anche come stato hello toocheck, aggiornamento o eliminazione di peering per il circuito.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="6cb2a-104">Creare e modificare il peering per un circuito ExpressRoute usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="6cb2a-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="6cb2a-105">In questo articolo consente di creare e gestire la configurazione di routing per un circuito ExpressRoute nel modello di distribuzione di gestione risorse hello tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="6cb2a-106">È anche possibile controllare lo stato di hello, update o delete e deprovisioning peering per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-106">You can also check hello status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="6cb2a-107">Se si desidera toouse toowork un metodo diverso con il circuito, selezionare un articolo da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-107">If you want toouse a different method toowork with your circuit, select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6cb2a-108">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6cb2a-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="6cb2a-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6cb2a-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="6cb2a-110">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="6cb2a-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="6cb2a-111">Video - Peering privato</span><span class="sxs-lookup"><span data-stu-id="6cb2a-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="6cb2a-112">Video - Peering pubblico</span><span class="sxs-lookup"><span data-stu-id="6cb2a-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="6cb2a-113">Video - Peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="6cb2a-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="6cb2a-114">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="6cb2a-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="6cb2a-115">Prerequisiti di configurazione</span><span class="sxs-lookup"><span data-stu-id="6cb2a-115">Configuration prerequisites</span></span>

* <span data-ttu-id="6cb2a-116">Sarà necessario hello versione hello cmdlet PowerShell di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-116">You will need hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="6cb2a-117">Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6cb2a-117">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="6cb2a-118">Assicurarsi di aver esaminato hello [prerequisiti](expressroute-prerequisites.md) pagina hello [requisiti di routing](expressroute-routing.md) pagina e hello [flussi di lavoro](expressroute-workflows.md) pagina prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-118">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md) page, hello [routing requirements](expressroute-routing.md) page, and hello [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="6cb2a-119">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="6cb2a-120">Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md) e circuito hello abilitato dal provider di connettività prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-120">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="6cb2a-121">Hello circuito ExpressRoute deve essere in uno stato di provisioning e abilitato per l'utente toobe toorun in grado di hello cmdlet in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-121">hello ExpressRoute circuit must be in a provisioned and enabled state for you toobe able toorun hello cmdlets in this article.</span></span>

<span data-ttu-id="6cb2a-122">Queste istruzioni si applicano solo toocircuits creato con il provider di servizi che offre servizi di connettività di livello 2.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-122">These instructions only apply toocircuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="6cb2a-123">Se si usa un provider di servizi che offre servizi gestiti di livello 3 (in genere una VPN IP, come MPLS), il provider di connettività configurerà e gestirà il routing per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6cb2a-124">È attualmente non inviano annunci peering configurato dai provider di servizi tramite il portale di Gestione servizi hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-124">We currently do not advertise peerings configured by service providers through hello service management portal.</span></span> <span data-ttu-id="6cb2a-125">L'abilitazione di questa funzionalità sarà presto disponibile.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="6cb2a-126">Rivolgersi al provider di servizi prima di configurare peering BGP.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="6cb2a-127">Per un circuito ExpressRoute è possibile configurare uno, due o tutti e tre i peering (peering privato di Azure, peering pubblico di Azure e peering Microsoft).</span><span class="sxs-lookup"><span data-stu-id="6cb2a-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="6cb2a-128">È possibile configurare i peering nell'ordine desiderato.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="6cb2a-129">Tuttavia, è necessario assicurarsi completare hello configurazione di ogni peer uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-129">However, you must make sure that you complete hello configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="6cb2a-130">Peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="6cb2a-130">Azure private peering</span></span>

<span data-ttu-id="6cb2a-131">In questa sezione consente di creare, ottenere, aggiornare ed eliminare hello Azure configurazione peering privata per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-131">This section helps you create, get, update, and delete hello Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-private-peering"></a><span data-ttu-id="6cb2a-132">toocreate peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="6cb2a-132">toocreate Azure private peering</span></span>

1. <span data-ttu-id="6cb2a-133">Importare il modulo di PowerShell hello per ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-133">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="6cb2a-134">È necessario installare una versione più recente installer PowerShell hello da [PowerShell Gallery](http://www.powershellgallery.com/) e importare i moduli di gestione risorse di Azure hello nella sessione di PowerShell hello in toostart ordine utilizzando i cmdlet di ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-134">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="6cb2a-135">È necessario toorun PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-135">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="6cb2a-136">Importare tutti i moduli AzureRM.* hello all'interno di hello noto l'intervallo di versioni semantico.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-136">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="6cb2a-137">È anche possibile importare un modulo select all'interno di hello noto intervallo versione semantica.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-137">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="6cb2a-138">Eseguire l'accesso tooyour account.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-138">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="6cb2a-139">Selezionare una sottoscrizione hello da circuito ExpressRoute toocreate.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-139">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="6cb2a-140">Creare un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="6cb2a-141">Seguire hello istruzioni toocreate un [circuito ExpressRoute](expressroute-howto-circuit-arm.md) e fare in modo fornito dal provider di connettività hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-141">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="6cb2a-142">Se il provider di connettività offre servizi di livello 3 gestiti, è possibile richiedere il tooenable provider di connettività privata peering per l'utente di Azure.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="6cb2a-143">In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-143">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="6cb2a-144">Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, continuare la configurazione utilizzando i passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="6cb2a-145">Controllare toomake di circuito ExpressRoute hello assicurarsi che sia stato eseguito il provisioning e inoltre abilitato.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-145">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="6cb2a-146">Utilizzare hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-146">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="6cb2a-147">risposta Hello è simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-147">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="6cb2a-148">Configurare peering privato di Azure per il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-148">Configure Azure private peering for hello circuit.</span></span> <span data-ttu-id="6cb2a-149">Assicurarsi di disporre delle seguenti prima di procedere con passaggi successivi hello hello:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-149">Make sure that you have hello following items before you proceed with hello next steps:</span></span>

  * <span data-ttu-id="6cb2a-150">/ 30 subnet per collegamento primario hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-150">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="6cb2a-151">subnet Hello non deve essere parte di qualsiasi spazio degli indirizzi riservato per le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-151">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="6cb2a-152">/ 30 subnet per collegamento secondario hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-152">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="6cb2a-153">subnet Hello non deve essere parte di qualsiasi spazio degli indirizzi riservato per le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-153">hello subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="6cb2a-154">Un esempio di ID VLAN valido tooestablish il peer.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-154">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="6cb2a-155">Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-155">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="6cb2a-156">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-156">AS number for peering.</span></span> <span data-ttu-id="6cb2a-157">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="6cb2a-158">È possibile usare il numero AS privato per questo peering.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="6cb2a-159">Assicurarsi di non usare il numero 65515.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="6cb2a-160">**Facoltativo:** un hash MD5 se si sceglie toouse uno.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-160">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="6cb2a-161">Utilizzare hello seguente esempio tooconfigure privata peering per il circuito di Azure:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-161">Use hello following example tooconfigure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="6cb2a-162">Se si sceglie toouse un hash MD5, usare hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-162">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="6cb2a-163">Assicurarsi di specificare il numero AS come ASN di peering e non come ASN cliente.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-private-peering-details"></a><span data-ttu-id="6cb2a-164">tooview dettagli di peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="6cb2a-164">tooview Azure private peering details</span></span>

<span data-ttu-id="6cb2a-165">È possibile ottenere i dettagli di configurazione utilizzando hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-165">You can get configuration details by using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a><span data-ttu-id="6cb2a-166">configurazione di peering privato Azure tooupdate</span><span class="sxs-lookup"><span data-stu-id="6cb2a-166">tooupdate Azure private peering configuration</span></span>

<span data-ttu-id="6cb2a-167">È possibile aggiornare qualsiasi parte della configurazione di hello utilizzando hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-167">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="6cb2a-168">In questo esempio hello ID VLAN del circuito hello viene aggiornato da too500 100.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-168">In this example, hello VLAN ID of hello circuit is being updated from 100 too500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a><span data-ttu-id="6cb2a-169">toodelete peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="6cb2a-169">toodelete Azure private peering</span></span>

<span data-ttu-id="6cb2a-170">È possibile rimuovere la configurazione di peering eseguendo hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-170">You can remove your peering configuration by running hello following example:</span></span>

> [!WARNING]
> <span data-ttu-id="6cb2a-171">È necessario assicurarsi che tutte le reti virtuali vengono scollegate dal hello circuito ExpressRoute prima di eseguire questo esempio.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-171">You must ensure that all virtual networks are unlinked from hello ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="6cb2a-172">Peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="6cb2a-172">Azure public peering</span></span>

<span data-ttu-id="6cb2a-173">In questa sezione consente di creare, ottenere, aggiornare ed eliminare hello Azure configurazione di peering pubblico per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-173">This section helps you create, get, update, and delete hello Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="toocreate-azure-public-peering"></a><span data-ttu-id="6cb2a-174">toocreate peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="6cb2a-174">toocreate Azure public peering</span></span>

1. <span data-ttu-id="6cb2a-175">Importare il modulo di PowerShell hello per ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-175">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="6cb2a-176">È necessario installare una versione più recente installer PowerShell hello da [PowerShell Gallery](http://www.powershellgallery.com/) e importare i moduli di gestione risorse di Azure hello nella sessione di PowerShell hello in toostart ordine utilizzando i cmdlet di ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-176">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="6cb2a-177">È necessario toorun PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-177">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="6cb2a-178">Importare tutti i moduli AzureRM.* hello all'interno di hello noto l'intervallo di versioni semantico.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-178">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="6cb2a-179">È anche possibile importare un modulo select all'interno di hello noto intervallo versione semantica.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-179">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="6cb2a-180">Eseguire l'accesso tooyour account.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-180">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="6cb2a-181">Selezionare una sottoscrizione hello da circuito ExpressRoute toocreate.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-181">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="6cb2a-182">Creare un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="6cb2a-183">Seguire hello istruzioni toocreate un [circuito ExpressRoute](expressroute-howto-circuit-arm.md) e fare in modo fornito dal provider di connettività hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-183">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="6cb2a-184">Se il provider di connettività offre servizi di livello 3 gestiti, è possibile richiedere il tooenable provider di connettività privata peering per l'utente di Azure.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="6cb2a-185">In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-185">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="6cb2a-186">Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, continuare la configurazione utilizzando i passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="6cb2a-187">Controllare hello ExpressRoute circuito tooensure che sia stato eseguito il provisioning e inoltre abilitato.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-187">Check hello ExpressRoute circuit tooensure it is provisioned and also enabled.</span></span> <span data-ttu-id="6cb2a-188">Utilizzare hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-188">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="6cb2a-189">risposta Hello è simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-189">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                      "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="6cb2a-190">Configurare peering pubblico di Azure per il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-190">Configure Azure public peering for hello circuit.</span></span> <span data-ttu-id="6cb2a-191">Assicurarsi di avere le seguenti informazioni prima di continuare ulteriormente hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-191">Make sure that you have hello following information before you proceed further.</span></span>

  * <span data-ttu-id="6cb2a-192">/ 30 subnet per collegamento primario hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-192">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="6cb2a-193">Deve essere un prefisso IPv4 pubblico valido.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="6cb2a-194">/ 30 subnet per collegamento secondario hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-194">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="6cb2a-195">Deve essere un prefisso IPv4 pubblico valido.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="6cb2a-196">Un esempio di ID VLAN valido tooestablish il peer.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-196">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="6cb2a-197">Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-197">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="6cb2a-198">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-198">AS number for peering.</span></span> <span data-ttu-id="6cb2a-199">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="6cb2a-200">**Facoltativo:** un hash MD5 se si sceglie toouse uno.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-200">**Optional -** An MD5 hash if you choose toouse one.</span></span>

  <span data-ttu-id="6cb2a-201">Eseguire hello seguente esempio tooconfigure pubblici di peering per il circuito di Azure</span><span class="sxs-lookup"><span data-stu-id="6cb2a-201">Run hello following example tooconfigure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="6cb2a-202">Se si sceglie toouse un hash MD5, usare hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-202">If you choose toouse an MD5 hash, use hello following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="6cb2a-203">Assicurarsi di specificare il numero AS come ASN di peering e non come ASN cliente.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="tooview-azure-public-peering-details"></a><span data-ttu-id="6cb2a-204">tooview dettagli di peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="6cb2a-204">tooview Azure public peering details</span></span>

<span data-ttu-id="6cb2a-205">È possibile ottenere i dettagli di configurazione mediante hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-205">You can get configuration details using hello following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a><span data-ttu-id="6cb2a-206">configurazione di peering pubblico Azure tooupdate</span><span class="sxs-lookup"><span data-stu-id="6cb2a-206">tooupdate Azure public peering configuration</span></span>

<span data-ttu-id="6cb2a-207">È possibile aggiornare qualsiasi parte della configurazione di hello utilizzando hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-207">You can update any part of hello configuration using hello following example.</span></span> <span data-ttu-id="6cb2a-208">In questo esempio hello ID VLAN del circuito hello viene aggiornato da too600 200.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-208">In this example, hello VLAN ID of hello circuit is being updated from 200 too600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a><span data-ttu-id="6cb2a-209">toodelete peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="6cb2a-209">toodelete Azure public peering</span></span>

<span data-ttu-id="6cb2a-210">È possibile rimuovere la configurazione di peering eseguendo hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-210">You can remove your peering configuration by running hello following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="6cb2a-211">Peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="6cb2a-211">Microsoft peering</span></span>

<span data-ttu-id="6cb2a-212">In questa sezione consente di creare, ottenere, aggiornare ed eliminare le configurazioni di peering Microsoft hello per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-212">This section helps you create, get, update, and delete hello Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6cb2a-213">Microsoft peering di circuiti ExpressRoute che sono stati configurati precedente tooAugust 1, 2017 disporrà di tutti i prefissi di servizio pubblicati tramite hello peering Microsoft, anche se non sono definiti i filtri di route.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-213">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through hello Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="6cb2a-214">Microsoft peering di circuiti ExpressRoute configurati o dopo il 1 agosto 2017 non avrà alcun prefisso annunciato fino a quando non è associato un filtro di route toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span> <span data-ttu-id="6cb2a-215">Per altre informazioni, vedere [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md) (Configurare un filtro di route per il peering Microsoft).</span><span class="sxs-lookup"><span data-stu-id="6cb2a-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="toocreate-microsoft-peering"></a><span data-ttu-id="6cb2a-216">toocreate peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="6cb2a-216">toocreate Microsoft peering</span></span>

1. <span data-ttu-id="6cb2a-217">Importare il modulo di PowerShell hello per ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-217">Import hello PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="6cb2a-218">È necessario installare una versione più recente installer PowerShell hello da [PowerShell Gallery](http://www.powershellgallery.com/) e importare i moduli di gestione risorse di Azure hello nella sessione di PowerShell hello in toostart ordine utilizzando i cmdlet di ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-218">You must install hello latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import hello Azure Resource Manager modules into hello PowerShell session in order toostart using hello ExpressRoute cmdlets.</span></span> <span data-ttu-id="6cb2a-219">È necessario toorun PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-219">You will need toorun PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="6cb2a-220">Importare tutti i moduli AzureRM.* hello all'interno di hello noto l'intervallo di versioni semantico.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-220">Import all of hello AzureRM.* modules within hello known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="6cb2a-221">È anche possibile importare un modulo select all'interno di hello noto intervallo versione semantica.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-221">You can also just import a select module within hello known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="6cb2a-222">Eseguire l'accesso tooyour account.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-222">Sign in tooyour account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="6cb2a-223">Selezionare una sottoscrizione hello da circuito ExpressRoute toocreate.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-223">Select hello subscription you want toocreate ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="6cb2a-224">Creare un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="6cb2a-225">Seguire hello istruzioni toocreate un [circuito ExpressRoute](expressroute-howto-circuit-arm.md) e fare in modo fornito dal provider di connettività hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-225">Follow hello instructions toocreate an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by hello connectivity provider.</span></span>

  <span data-ttu-id="6cb2a-226">Se il provider di connettività offre servizi di livello 3 gestiti, è possibile richiedere il tooenable provider di connettività privata peering per l'utente di Azure.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider tooenable Azure private peering for you.</span></span> <span data-ttu-id="6cb2a-227">In tal caso, non sarà necessario istruzioni toofollow riportate nelle sezioni successive di hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-227">In that case, you won't need toofollow instructions listed in hello next sections.</span></span> <span data-ttu-id="6cb2a-228">Tuttavia, se il provider di connettività non gestisce il routing, dopo la creazione del circuito, continuare la configurazione utilizzando i passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using hello next steps.</span></span>
3. <span data-ttu-id="6cb2a-229">Controllare toomake di circuito ExpressRoute hello assicurarsi che sia stato eseguito il provisioning e inoltre abilitato.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-229">Check hello ExpressRoute circuit toomake sure it is provisioned and also enabled.</span></span> <span data-ttu-id="6cb2a-230">Utilizzare hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-230">Use hello following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="6cb2a-231">risposta Hello è simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-231">hello response is similar toohello following example:</span></span>

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. <span data-ttu-id="6cb2a-232">Configurare Microsoft peering per il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-232">Configure Microsoft peering for hello circuit.</span></span> <span data-ttu-id="6cb2a-233">Assicurarsi di aver hello le seguenti informazioni prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-233">Make sure that you have hello following information before you proceed.</span></span>

  * <span data-ttu-id="6cb2a-234">/ 30 subnet per collegamento primario hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-234">A /30 subnet for hello primary link.</span></span> <span data-ttu-id="6cb2a-235">Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="6cb2a-236">/ 30 subnet per collegamento secondario hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-236">A /30 subnet for hello secondary link.</span></span> <span data-ttu-id="6cb2a-237">Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="6cb2a-238">Un esempio di ID VLAN valido tooestablish il peer.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-238">A valid VLAN ID tooestablish this peering on.</span></span> <span data-ttu-id="6cb2a-239">Non verificare che nessun altro peering nel circuito hello utilizza hello stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-239">Ensure that no other peering in hello circuit uses hello same VLAN ID.</span></span>
  * <span data-ttu-id="6cb2a-240">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-240">AS number for peering.</span></span> <span data-ttu-id="6cb2a-241">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="6cb2a-242">I prefissi annunciati: È necessario fornire un elenco di tutti i prefissi Prevedi tooadvertise sessione BGP hello.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-242">Advertised prefixes: You must provide a list of all prefixes you plan tooadvertise over hello BGP session.</span></span> <span data-ttu-id="6cb2a-243">Sono accettati solo prefissi di indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="6cb2a-244">Se si prevede un set di prefissi toosend, è possibile inviare un elenco delimitato da virgole.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-244">If you plan toosend a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="6cb2a-245">I prefissi devono essere registrati tooyou in un RIR / IRR.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-245">These prefixes must be registered tooyou in an RIR / IRR.</span></span>
  * <span data-ttu-id="6cb2a-246">**Facoltativo:** cliente ASN: nel caso di annunci con prefissi non registrato toohello peering sotto forma di numero, è possibile specificare hello come numero toowhich sono registrati.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered toohello peering AS number, you can specify hello AS number toowhich they are registered.</span></span>
  * <span data-ttu-id="6cb2a-247">Nome del Registro di sistema di routing: È possibile specificare hello RIR / IRR contro cui hello come numero e i prefissi sono registrati.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-247">Routing Registry Name: You can specify hello RIR / IRR against which hello AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="6cb2a-248">**Facoltativo:** un hash MD5 se si sceglie toouse uno.</span><span class="sxs-lookup"><span data-stu-id="6cb2a-248">**Optional -** An MD5 hash if you choose toouse one.</span></span>

   <span data-ttu-id="6cb2a-249">Utilizzare hello seguendo l'esempio tooconfigure peering Microsoft per il circuito:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-249">Use hello following example tooconfigure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a><span data-ttu-id="6cb2a-250">dettagli di peering Microsoft tooget</span><span class="sxs-lookup"><span data-stu-id="6cb2a-250">tooget Microsoft peering details</span></span>

<span data-ttu-id="6cb2a-251">È possibile ottenere i dettagli di configurazione mediante hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-251">You can get configuration details using hello following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a><span data-ttu-id="6cb2a-252">configurazione di peering Microsoft tooupdate</span><span class="sxs-lookup"><span data-stu-id="6cb2a-252">tooupdate Microsoft peering configuration</span></span>

<span data-ttu-id="6cb2a-253">È possibile aggiornare qualsiasi parte della configurazione di hello utilizzando hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-253">You can update any part of hello configuration using hello following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a><span data-ttu-id="6cb2a-254">toodelete peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="6cb2a-254">toodelete Microsoft peering</span></span>

<span data-ttu-id="6cb2a-255">È possibile rimuovere la configurazione di peering eseguendo hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6cb2a-255">You can remove your peering configuration by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="6cb2a-256">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6cb2a-256">Next steps</span></span>

<span data-ttu-id="6cb2a-257">Passaggio successivo, [collegare un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="6cb2a-257">Next step, [Link a VNet tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="6cb2a-258">Per ulteriori informazioni sui flussi di lavoro ExpressRoute, vedere [Flussi di lavoro ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="6cb2a-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="6cb2a-259">Per altre informazioni sul peering del circuito, vedere l'articolo relativo ai [circuiti ExpressRoute e domini di routing](expressroute-circuit-peerings.md)</span><span class="sxs-lookup"><span data-stu-id="6cb2a-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="6cb2a-260">Per ulteriori informazioni sull’uso delle reti virtuali, vedere [Panoramica sulla rete virtuale](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6cb2a-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
