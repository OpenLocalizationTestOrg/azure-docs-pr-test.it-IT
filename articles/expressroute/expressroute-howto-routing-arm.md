---
title: 'Come configurare il routing (peering) per un circuito ExpressRoute: Resource Manager: PowerShell: Azure | Documentazione Microsoft'
description: Questo articolo descrive come creare ed eseguire il provisioning di un circuito ExpressRoute per il peering privato, il peering pubblico e il peering Microsoft. Questo articolo mostra anche come controllare lo stato e aggiornare o eliminare i peering per un circuito.
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
ms.openlocfilehash: af68955b78239832e413e1b59e033d7d3da8d599
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="e25c4-104">Creare e modificare il peering per un circuito ExpressRoute usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="e25c4-104">Create and modify peering for an ExpressRoute circuit using PowerShell</span></span>

<span data-ttu-id="e25c4-105">Questo articolo consente di creare e gestire la configurazione di routing per un circuito ExpressRoute nel modello di distribuzione Resource Manager tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e25c4-105">This article helps you create and manage routing configuration for an ExpressRoute circuit in the Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="e25c4-106">La procedura seguente mostra anche come controllare lo stato e aggiornare, eliminare o eseguire il deprovisioning dei peering per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e25c4-106">You can also check the status, update, or delete and deprovision peerings for an ExpressRoute circuit.</span></span> <span data-ttu-id="e25c4-107">Se si vuole usare un metodo diverso per eseguire operazioni nel circuito, selezionare l'articolo appropriato nell'elenco seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-107">If you want to use a different method to work with your circuit, select an article from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e25c4-108">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e25c4-108">Azure portal</span></span>](expressroute-howto-routing-portal-resource-manager.md)
> * [<span data-ttu-id="e25c4-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e25c4-109">PowerShell</span></span>](expressroute-howto-routing-arm.md)
> * [<span data-ttu-id="e25c4-110">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e25c4-110">Azure CLI</span></span>](howto-routing-cli.md)
> * [<span data-ttu-id="e25c4-111">Video - Peering privato</span><span class="sxs-lookup"><span data-stu-id="e25c4-111">Video - Private peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="e25c4-112">Video - Peering pubblico</span><span class="sxs-lookup"><span data-stu-id="e25c4-112">Video - Public peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="e25c4-113">Video - Peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="e25c4-113">Video - Microsoft peering</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [<span data-ttu-id="e25c4-114">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="e25c4-114">PowerShell (classic)</span></span>](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="e25c4-115">Prerequisiti di configurazione</span><span class="sxs-lookup"><span data-stu-id="e25c4-115">Configuration prerequisites</span></span>

* <span data-ttu-id="e25c4-116">È necessaria la versione più recente dei cmdlet di PowerShell per Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e25c4-116">You will need the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="e25c4-117">Per altre informazioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e25c4-117">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 
* <span data-ttu-id="e25c4-118">Prima di iniziare la configurazione, assicurarsi di aver letto le pagine relative ai [prerequisiti](expressroute-prerequisites.md), ai [requisiti per il routing](expressroute-routing.md) e ai [flussi di lavoro](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="e25c4-118">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md) page, the [routing requirements](expressroute-routing.md) page, and the [workflows](expressroute-workflows.md) page before you begin configuration.</span></span>
* <span data-ttu-id="e25c4-119">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="e25c4-119">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="e25c4-120">Seguire le istruzioni per [creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md) e fare in modo che venga abilitato dal provider di connettività prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="e25c4-120">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="e25c4-121">Per poter eseguire i cmdlet descritti in questo articolo deve essere stato effettuato il provisioning del circuito ExpressRoute e lo stato del circuito deve essere abilitato.</span><span class="sxs-lookup"><span data-stu-id="e25c4-121">The ExpressRoute circuit must be in a provisioned and enabled state for you to be able to run the cmdlets in this article.</span></span>

<span data-ttu-id="e25c4-122">Queste istruzioni si applicano solo ai circuiti creati con provider di servizi che offrono servizi di connettività di livello 2.</span><span class="sxs-lookup"><span data-stu-id="e25c4-122">These instructions only apply to circuits created with service providers offering Layer 2 connectivity services.</span></span> <span data-ttu-id="e25c4-123">Se si usa un provider di servizi che offre servizi gestiti di livello 3 (in genere una VPN IP, come MPLS), il provider di connettività configurerà e gestirà il routing per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="e25c4-123">If you are using a service provider that offers managed Layer 3 services (typically an IPVPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e25c4-124">Attualmente non vengono annunciati peering configurati da provider di servizi tramite il portale di gestione del servizio.</span><span class="sxs-lookup"><span data-stu-id="e25c4-124">We currently do not advertise peerings configured by service providers through the service management portal.</span></span> <span data-ttu-id="e25c4-125">L'abilitazione di questa funzionalità sarà presto disponibile.</span><span class="sxs-lookup"><span data-stu-id="e25c4-125">We are working on enabling this capability soon.</span></span> <span data-ttu-id="e25c4-126">Rivolgersi al provider di servizi prima di configurare peering BGP.</span><span class="sxs-lookup"><span data-stu-id="e25c4-126">Check with your service provider before configuring BGP peerings.</span></span>
> 
> 

<span data-ttu-id="e25c4-127">Per un circuito ExpressRoute è possibile configurare uno, due o tutti e tre i peering (peering privato di Azure, peering pubblico di Azure e peering Microsoft).</span><span class="sxs-lookup"><span data-stu-id="e25c4-127">You can configure one, two, or all three peerings (Azure private, Azure public and Microsoft) for an ExpressRoute circuit.</span></span> <span data-ttu-id="e25c4-128">È possibile configurare i peering nell'ordine desiderato.</span><span class="sxs-lookup"><span data-stu-id="e25c4-128">You can configure peerings in any order you choose.</span></span> <span data-ttu-id="e25c4-129">assicurandosi, tuttavia, di completare la configurazione di un peering per volta.</span><span class="sxs-lookup"><span data-stu-id="e25c4-129">However, you must make sure that you complete the configuration of each peering one at a time.</span></span> 

## <a name="azure-private-peering"></a><span data-ttu-id="e25c4-130">Peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="e25c4-130">Azure private peering</span></span>

<span data-ttu-id="e25c4-131">Questa sezione fornisce le istruzioni per creare, ottenere, aggiornare ed eliminare la configurazione del peering privato di Azure per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e25c4-131">This section helps you create, get, update, and delete the Azure private peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-private-peering"></a><span data-ttu-id="e25c4-132">Per creare un peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="e25c4-132">To create Azure private peering</span></span>

1. <span data-ttu-id="e25c4-133">Importare il modulo PowerShell per ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e25c4-133">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="e25c4-134">È necessario installare da [PowerShell Gallery](http://www.powershellgallery.com/) il programma di installazione di PowerShell più recente e importare i moduli di Gestione risorse di Azure nella sessione di PowerShell per iniziare a usare i cmdlet di ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e25c4-134">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="e25c4-135">È necessario eseguire PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e25c4-135">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  <span data-ttu-id="e25c4-136">Importare tutti i moduli AzureRM.* nell'intervallo noto delle versioni semantiche.</span><span class="sxs-lookup"><span data-stu-id="e25c4-136">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="e25c4-137">È possibile anche importare un solo modulo nell'intervallo noto delle versioni semantiche.</span><span class="sxs-lookup"><span data-stu-id="e25c4-137">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network 
  ```

  <span data-ttu-id="e25c4-138">Accedere al proprio account.</span><span class="sxs-lookup"><span data-stu-id="e25c4-138">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="e25c4-139">Selezionare la sottoscrizione desiderata per creare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e25c4-139">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="e25c4-140">Creare un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e25c4-140">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="e25c4-141">Seguire le istruzioni per creare un [circuito ExpressRoute](expressroute-howto-circuit-arm.md) e chiedere al provider di connettività di effettuarne il provisioning.</span><span class="sxs-lookup"><span data-stu-id="e25c4-141">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="e25c4-142">Se il provider di connettività offre servizi gestiti di livello 3, è possibile chiedere al provider di connettività di abilitare il peering privato di Azure.</span><span class="sxs-lookup"><span data-stu-id="e25c4-142">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="e25c4-143">In questo caso, non sarà necessario seguire le istruzioni riportate nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="e25c4-143">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="e25c4-144">Se invece il provider di connettività non gestisce il routing per conto dell'utente, dopo aver creato il circuito, proseguire la configurazione seguendo questa procedura.</span><span class="sxs-lookup"><span data-stu-id="e25c4-144">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="e25c4-145">Controllare che sia stato effettuato il provisioning del circuito ExpressRoute e che il circuito sia abilitato.</span><span class="sxs-lookup"><span data-stu-id="e25c4-145">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="e25c4-146">Usare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-146">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="e25c4-147">La risposta restituita è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-147">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="e25c4-148">Configurare il peering privato di Azure per il circuito.</span><span class="sxs-lookup"><span data-stu-id="e25c4-148">Configure Azure private peering for the circuit.</span></span> <span data-ttu-id="e25c4-149">Prima di procedere con i passaggi successivi, verificare che siano presenti gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e25c4-149">Make sure that you have the following items before you proceed with the next steps:</span></span>

  * <span data-ttu-id="e25c4-150">Una subnet /30 per il collegamento primario.</span><span class="sxs-lookup"><span data-stu-id="e25c4-150">A /30 subnet for the primary link.</span></span> <span data-ttu-id="e25c4-151">La subnet non deve far parte di alcuno spazio indirizzi riservato per le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="e25c4-151">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="e25c4-152">Una subnet /30 per il collegamento secondario.</span><span class="sxs-lookup"><span data-stu-id="e25c4-152">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="e25c4-153">La subnet non deve far parte di alcuno spazio indirizzi riservato per le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="e25c4-153">The subnet must not be part of any address space reserved for virtual networks.</span></span>
  * <span data-ttu-id="e25c4-154">Un ID VLAN valido su cui stabilire questo peering.</span><span class="sxs-lookup"><span data-stu-id="e25c4-154">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="e25c4-155">Assicurarsi che nessun altro peering nel circuito usi lo stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="e25c4-155">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="e25c4-156">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="e25c4-156">AS number for peering.</span></span> <span data-ttu-id="e25c4-157">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="e25c4-157">You can use both 2-byte and 4-byte AS numbers.</span></span> <span data-ttu-id="e25c4-158">È possibile usare il numero AS privato per questo peering.</span><span class="sxs-lookup"><span data-stu-id="e25c4-158">You can use a private AS number for this peering.</span></span> <span data-ttu-id="e25c4-159">Assicurarsi di non usare il numero 65515.</span><span class="sxs-lookup"><span data-stu-id="e25c4-159">Ensure that you are not using 65515.</span></span>
  * <span data-ttu-id="e25c4-160">**Facoltativo:** un hash MD5, se si sceglie di usarne uno.</span><span class="sxs-lookup"><span data-stu-id="e25c4-160">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="e25c4-161">Per configurare il peering privato di Azure per il circuito, usare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-161">Use the following example to configure Azure private peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="e25c4-162">Se si sceglie di usare un hash MD5, usare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-162">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="e25c4-163">Assicurarsi di specificare il numero AS come ASN di peering e non come ASN cliente.</span><span class="sxs-lookup"><span data-stu-id="e25c4-163">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="to-view-azure-private-peering-details"></a><span data-ttu-id="e25c4-164">Per visualizzare i dettagli relativi al peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="e25c4-164">To view Azure private peering details</span></span>

<span data-ttu-id="e25c4-165">Per ottenere i dettagli di configurazione, usare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-165">You can get configuration details by using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="to-update-azure-private-peering-configuration"></a><span data-ttu-id="e25c4-166">Per aggiornare la configurazione del peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="e25c4-166">To update Azure private peering configuration</span></span>

<span data-ttu-id="e25c4-167">Per aggiornare qualsiasi parte della configurazione, usare l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="e25c4-167">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="e25c4-168">In questo esempio il valore dell'ID VLAN del circuito viene aggiornato da 100 a 500.</span><span class="sxs-lookup"><span data-stu-id="e25c4-168">In this example, the VLAN ID of the circuit is being updated from 100 to 500.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-azure-private-peering"></a><span data-ttu-id="e25c4-169">Per eliminare un peering privato di Azure</span><span class="sxs-lookup"><span data-stu-id="e25c4-169">To delete Azure private peering</span></span>

<span data-ttu-id="e25c4-170">Per rimuovere la configurazione di peering, eseguire l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-170">You can remove your peering configuration by running the following example:</span></span>

> [!WARNING]
> <span data-ttu-id="e25c4-171">Assicurarsi che tutte le reti virtuali siano scollegate dal circuito ExpressRoute prima di eseguire questo esempio.</span><span class="sxs-lookup"><span data-stu-id="e25c4-171">You must ensure that all virtual networks are unlinked from the ExpressRoute circuit before running this example.</span></span> 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a><span data-ttu-id="e25c4-172">Peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="e25c4-172">Azure public peering</span></span>

<span data-ttu-id="e25c4-173">Questa sezione consente di creare, ottenere, aggiornare ed eliminare la configurazione del peering pubblico di Azure per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e25c4-173">This section helps you create, get, update, and delete the Azure public peering configuration for an ExpressRoute circuit.</span></span>

### <a name="to-create-azure-public-peering"></a><span data-ttu-id="e25c4-174">Per creare un peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="e25c4-174">To create Azure public peering</span></span>

1. <span data-ttu-id="e25c4-175">Importare il modulo PowerShell per ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e25c4-175">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="e25c4-176">È necessario installare da [PowerShell Gallery](http://www.powershellgallery.com/) il programma di installazione di PowerShell più recente e importare i moduli di Gestione risorse di Azure nella sessione di PowerShell per iniziare a usare i cmdlet di ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e25c4-176">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="e25c4-177">È necessario eseguire PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e25c4-177">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  <span data-ttu-id="e25c4-178">Importare tutti i moduli AzureRM.* nell'intervallo noto delle versioni semantiche.</span><span class="sxs-lookup"><span data-stu-id="e25c4-178">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="e25c4-179">È possibile anche importare un solo modulo nell'intervallo noto delle versioni semantiche.</span><span class="sxs-lookup"><span data-stu-id="e25c4-179">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
```

  <span data-ttu-id="e25c4-180">Accedere al proprio account.</span><span class="sxs-lookup"><span data-stu-id="e25c4-180">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="e25c4-181">Selezionare la sottoscrizione desiderata per creare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e25c4-181">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="e25c4-182">Creare un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e25c4-182">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="e25c4-183">Seguire le istruzioni per creare un [circuito ExpressRoute](expressroute-howto-circuit-arm.md) e chiedere al provider di connettività di effettuarne il provisioning.</span><span class="sxs-lookup"><span data-stu-id="e25c4-183">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="e25c4-184">Se il provider di connettività offre servizi gestiti di livello 3, è possibile chiedere al provider di connettività di abilitare il peering privato di Azure.</span><span class="sxs-lookup"><span data-stu-id="e25c4-184">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="e25c4-185">In questo caso, non sarà necessario seguire le istruzioni riportate nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="e25c4-185">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="e25c4-186">Se invece il provider di connettività non gestisce il routing per conto dell'utente, dopo aver creato il circuito, proseguire la configurazione seguendo questa procedura.</span><span class="sxs-lookup"><span data-stu-id="e25c4-186">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="e25c4-187">Controllare che sia stato effettuato il provisioning del circuito ExpressRoute e che il circuito sia abilitato.</span><span class="sxs-lookup"><span data-stu-id="e25c4-187">Check the ExpressRoute circuit to ensure it is provisioned and also enabled.</span></span> <span data-ttu-id="e25c4-188">Usare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-188">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="e25c4-189">La risposta restituita è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-189">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="e25c4-190">Configurare il peering pubblico di Azure per il circuito.</span><span class="sxs-lookup"><span data-stu-id="e25c4-190">Configure Azure public peering for the circuit.</span></span> <span data-ttu-id="e25c4-191">Prima di continuare, verificare di avere a disposizione le informazioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="e25c4-191">Make sure that you have the following information before you proceed further.</span></span>

  * <span data-ttu-id="e25c4-192">Una subnet /30 per il collegamento primario.</span><span class="sxs-lookup"><span data-stu-id="e25c4-192">A /30 subnet for the primary link.</span></span> <span data-ttu-id="e25c4-193">Deve essere un prefisso IPv4 pubblico valido.</span><span class="sxs-lookup"><span data-stu-id="e25c4-193">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="e25c4-194">Una subnet /30 per il collegamento secondario.</span><span class="sxs-lookup"><span data-stu-id="e25c4-194">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="e25c4-195">Deve essere un prefisso IPv4 pubblico valido.</span><span class="sxs-lookup"><span data-stu-id="e25c4-195">This must be a valid public IPv4 prefix.</span></span>
  * <span data-ttu-id="e25c4-196">Un ID VLAN valido su cui stabilire questo peering.</span><span class="sxs-lookup"><span data-stu-id="e25c4-196">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="e25c4-197">Assicurarsi che nessun altro peering nel circuito usi lo stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="e25c4-197">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="e25c4-198">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="e25c4-198">AS number for peering.</span></span> <span data-ttu-id="e25c4-199">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="e25c4-199">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="e25c4-200">**Facoltativo:** un hash MD5, se si sceglie di usarne uno.</span><span class="sxs-lookup"><span data-stu-id="e25c4-200">**Optional -** An MD5 hash if you choose to use one.</span></span>

  <span data-ttu-id="e25c4-201">Per configurare il peering pubblico di Azure per il circuito, applicare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-201">Run the following example to configure Azure public peering for your circuit</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  <span data-ttu-id="e25c4-202">Se si sceglie di usare un hash MD5, usare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-202">If you choose to use an MD5 hash, use the following example:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > <span data-ttu-id="e25c4-203">Assicurarsi di specificare il numero AS come ASN di peering e non come ASN cliente.</span><span class="sxs-lookup"><span data-stu-id="e25c4-203">Ensure that you specify your AS number as peering ASN, not customer ASN.</span></span>
  > 
  >

### <a name="to-view-azure-public-peering-details"></a><span data-ttu-id="e25c4-204">Per visualizzare i dettagli relativi al peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="e25c4-204">To view Azure public peering details</span></span>

<span data-ttu-id="e25c4-205">Per ottenere i dettagli di configurazione, usare il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-205">You can get configuration details using the following cmdlet:</span></span>

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="to-update-azure-public-peering-configuration"></a><span data-ttu-id="e25c4-206">Per aggiornare la configurazione del peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="e25c4-206">To update Azure public peering configuration</span></span>

<span data-ttu-id="e25c4-207">Per aggiornare qualsiasi parte della configurazione, usare l'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="e25c4-207">You can update any part of the configuration using the following example.</span></span> <span data-ttu-id="e25c4-208">In questo esempio il valore dell'ID VLAN del circuito viene aggiornato da 200 a 600.</span><span class="sxs-lookup"><span data-stu-id="e25c4-208">In this example, the VLAN ID of the circuit is being updated from 200 to 600.</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-azure-public-peering"></a><span data-ttu-id="e25c4-209">Per eliminare un peering pubblico di Azure</span><span class="sxs-lookup"><span data-stu-id="e25c4-209">To delete Azure public peering</span></span>

<span data-ttu-id="e25c4-210">Per rimuovere la configurazione di peering, eseguire l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-210">You can remove your peering configuration by running the following example:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a><span data-ttu-id="e25c4-211">Peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="e25c4-211">Microsoft peering</span></span>

<span data-ttu-id="e25c4-212">Questa sezione consente di creare, ottenere, aggiornare ed eliminare la configurazione del peering Microsoft per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e25c4-212">This section helps you create, get, update, and delete the Microsoft peering configuration for an ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e25c4-213">Per i circuiti ExpressRoute configurati prima del 1 agosto 2017 tutti i prefissi di servizio saranno annunciati tramite il peering Microsoft, anche se non sono definiti i filtri di route.</span><span class="sxs-lookup"><span data-stu-id="e25c4-213">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through the Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="e25c4-214">Per il peering Microsoft dei circuiti ExpressRoute configurati dopo il 1 agosto 2017 non verrà annunciato alcun prefisso fino a quando non viene associato un filtro di route al circuito.</span><span class="sxs-lookup"><span data-stu-id="e25c4-214">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span> <span data-ttu-id="e25c4-215">Per altre informazioni, vedere [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md) (Configurare un filtro di route per il peering Microsoft).</span><span class="sxs-lookup"><span data-stu-id="e25c4-215">For more information, see [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md).</span></span>
> 
> 

### <a name="to-create-microsoft-peering"></a><span data-ttu-id="e25c4-216">Per creare il peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="e25c4-216">To create Microsoft peering</span></span>

1. <span data-ttu-id="e25c4-217">Importare il modulo PowerShell per ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e25c4-217">Import the PowerShell module for ExpressRoute.</span></span>

  <span data-ttu-id="e25c4-218">È necessario installare da [PowerShell Gallery](http://www.powershellgallery.com/) il programma di installazione di PowerShell più recente e importare i moduli di Gestione risorse di Azure nella sessione di PowerShell per iniziare a usare i cmdlet di ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e25c4-218">You must install the latest PowerShell installer from [PowerShell Gallery](http://www.powershellgallery.com/) and import the Azure Resource Manager modules into the PowerShell session in order to start using the ExpressRoute cmdlets.</span></span> <span data-ttu-id="e25c4-219">È necessario eseguire PowerShell come amministratore.</span><span class="sxs-lookup"><span data-stu-id="e25c4-219">You will need to run PowerShell as an Administrator.</span></span>

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  <span data-ttu-id="e25c4-220">Importare tutti i moduli AzureRM.* nell'intervallo noto delle versioni semantiche.</span><span class="sxs-lookup"><span data-stu-id="e25c4-220">Import all of the AzureRM.* modules within the known semantic version range.</span></span>

  ```powershell
  Import-AzureRM
  ```

  <span data-ttu-id="e25c4-221">È possibile anche importare un solo modulo nell'intervallo noto delle versioni semantiche.</span><span class="sxs-lookup"><span data-stu-id="e25c4-221">You can also just import a select module within the known semantic version range.</span></span>

  ```powershell
  Import-Module AzureRM.Network
  ```

  <span data-ttu-id="e25c4-222">Accedere al proprio account.</span><span class="sxs-lookup"><span data-stu-id="e25c4-222">Sign in to your account.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="e25c4-223">Selezionare la sottoscrizione desiderata per creare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e25c4-223">Select the subscription you want to create ExpressRoute circuit.</span></span>

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. <span data-ttu-id="e25c4-224">Creare un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e25c4-224">Create an ExpressRoute circuit.</span></span>

  <span data-ttu-id="e25c4-225">Seguire le istruzioni per creare un [circuito ExpressRoute](expressroute-howto-circuit-arm.md) e chiedere al provider di connettività di effettuarne il provisioning.</span><span class="sxs-lookup"><span data-stu-id="e25c4-225">Follow the instructions to create an [ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have it provisioned by the connectivity provider.</span></span>

  <span data-ttu-id="e25c4-226">Se il provider di connettività offre servizi gestiti di livello 3, è possibile chiedere al provider di connettività di abilitare il peering privato di Azure.</span><span class="sxs-lookup"><span data-stu-id="e25c4-226">If your connectivity provider offers managed Layer 3 services, you can request your connectivity provider to enable Azure private peering for you.</span></span> <span data-ttu-id="e25c4-227">In questo caso, non sarà necessario seguire le istruzioni riportate nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="e25c4-227">In that case, you won't need to follow instructions listed in the next sections.</span></span> <span data-ttu-id="e25c4-228">Se invece il provider di connettività non gestisce il routing per conto dell'utente, dopo aver creato il circuito, proseguire la configurazione seguendo questa procedura.</span><span class="sxs-lookup"><span data-stu-id="e25c4-228">However, if your connectivity provider does not manage routing for you, after creating your circuit, continue your configuration using the next steps.</span></span>
3. <span data-ttu-id="e25c4-229">Controllare che sia stato effettuato il provisioning del circuito ExpressRoute e che il circuito sia abilitato.</span><span class="sxs-lookup"><span data-stu-id="e25c4-229">Check the ExpressRoute circuit to make sure it is provisioned and also enabled.</span></span> <span data-ttu-id="e25c4-230">Usare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-230">Use the following example:</span></span>

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  <span data-ttu-id="e25c4-231">La risposta restituita è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-231">The response is similar to the following example:</span></span>

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
4. <span data-ttu-id="e25c4-232">Configurare il peering Microsoft per il circuito.</span><span class="sxs-lookup"><span data-stu-id="e25c4-232">Configure Microsoft peering for the circuit.</span></span> <span data-ttu-id="e25c4-233">Prima di procedere, verificare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="e25c4-233">Make sure that you have the following information before you proceed.</span></span>

  * <span data-ttu-id="e25c4-234">Una subnet /30 per il collegamento primario.</span><span class="sxs-lookup"><span data-stu-id="e25c4-234">A /30 subnet for the primary link.</span></span> <span data-ttu-id="e25c4-235">Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.</span><span class="sxs-lookup"><span data-stu-id="e25c4-235">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="e25c4-236">Una subnet /30 per il collegamento secondario.</span><span class="sxs-lookup"><span data-stu-id="e25c4-236">A /30 subnet for the secondary link.</span></span> <span data-ttu-id="e25c4-237">Deve essere un prefisso IPv4 pubblico valido di proprietà dell'utente e registrato presso un registro RIR o IRR.</span><span class="sxs-lookup"><span data-stu-id="e25c4-237">This must be a valid public IPv4 prefix owned by you and registered in an RIR / IRR.</span></span>
  * <span data-ttu-id="e25c4-238">Un ID VLAN valido su cui stabilire questo peering.</span><span class="sxs-lookup"><span data-stu-id="e25c4-238">A valid VLAN ID to establish this peering on.</span></span> <span data-ttu-id="e25c4-239">Assicurarsi che nessun altro peering nel circuito usi lo stesso ID VLAN.</span><span class="sxs-lookup"><span data-stu-id="e25c4-239">Ensure that no other peering in the circuit uses the same VLAN ID.</span></span>
  * <span data-ttu-id="e25c4-240">Numero AS per il peering.</span><span class="sxs-lookup"><span data-stu-id="e25c4-240">AS number for peering.</span></span> <span data-ttu-id="e25c4-241">È possibile usare numeri AS a 2 e a 4 byte.</span><span class="sxs-lookup"><span data-stu-id="e25c4-241">You can use both 2-byte and 4-byte AS numbers.</span></span>
  * <span data-ttu-id="e25c4-242">Advertised prefixes: è necessario fornire un elenco di tutti i prefissi che si intende pubblicizzare nella sessione BGP.</span><span class="sxs-lookup"><span data-stu-id="e25c4-242">Advertised prefixes: You must provide a list of all prefixes you plan to advertise over the BGP session.</span></span> <span data-ttu-id="e25c4-243">Sono accettati solo prefissi di indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="e25c4-243">Only public IP address prefixes are accepted.</span></span> <span data-ttu-id="e25c4-244">Se si intende inviare un set di prefissi, è possibile creare un elenco delimitato da virgole.</span><span class="sxs-lookup"><span data-stu-id="e25c4-244">If you plan to send a set of prefixes, you can send a comma-separated list.</span></span> <span data-ttu-id="e25c4-245">Questi prefissi devono essere intestati all'utente in un registro RIR o IRR.</span><span class="sxs-lookup"><span data-stu-id="e25c4-245">These prefixes must be registered to you in an RIR / IRR.</span></span>
  * <span data-ttu-id="e25c4-246">**Facoltativo -** ASN cliente: se si annunciano prefissi non registrati nel numero AS di peering, è possibile specificare il numero AS in cui sono registrati.</span><span class="sxs-lookup"><span data-stu-id="e25c4-246">**Optional -** Customer ASN: If you are advertising prefixes that are not registered to the peering AS number, you can specify the AS number to which they are registered.</span></span>
  * <span data-ttu-id="e25c4-247">Routing Registry Name: è possibile specificare il registro RIR/IRR in cui sono registrati il numero AS e i prefissi.</span><span class="sxs-lookup"><span data-stu-id="e25c4-247">Routing Registry Name: You can specify the RIR / IRR against which the AS number and prefixes are registered.</span></span>
  * <span data-ttu-id="e25c4-248">**Facoltativo:** un hash MD5, se si sceglie di usarne uno.</span><span class="sxs-lookup"><span data-stu-id="e25c4-248">**Optional -** An MD5 hash if you choose to use one.</span></span>

   <span data-ttu-id="e25c4-249">Per configurare il peering Microsoft per il circuito, applicare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-249">Use the following example to configure Microsoft peering for your circuit:</span></span>

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="to-get-microsoft-peering-details"></a><span data-ttu-id="e25c4-250">Ottenere i dettagli del peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="e25c4-250">To get Microsoft peering details</span></span>

<span data-ttu-id="e25c4-251">Per ottenere i dettagli di configurazione, usare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-251">You can get configuration details using the following example:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="to-update-microsoft-peering-configuration"></a><span data-ttu-id="e25c4-252">Per aggiornare la configurazione del peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="e25c4-252">To update Microsoft peering configuration</span></span>

<span data-ttu-id="e25c4-253">Per aggiornare qualsiasi parte della configurazione, applicare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-253">You can update any part of the configuration using the following example:</span></span>

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-delete-microsoft-peering"></a><span data-ttu-id="e25c4-254">Per eliminare il peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="e25c4-254">To delete Microsoft peering</span></span>

<span data-ttu-id="e25c4-255">Per rimuovere la configurazione di peering, eseguire il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="e25c4-255">You can remove your peering configuration by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a><span data-ttu-id="e25c4-256">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e25c4-256">Next steps</span></span>

<span data-ttu-id="e25c4-257">Successivamente, [collegare una rete virtuale a un circuito ExpressRoute](expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="e25c4-257">Next step, [Link a VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

* <span data-ttu-id="e25c4-258">Per ulteriori informazioni sui flussi di lavoro ExpressRoute, vedere [Flussi di lavoro ExpressRoute](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="e25c4-258">For more information about ExpressRoute workflows, see [ExpressRoute workflows](expressroute-workflows.md).</span></span>
* <span data-ttu-id="e25c4-259">Per altre informazioni sul peering del circuito, vedere l'articolo relativo ai [circuiti ExpressRoute e domini di routing](expressroute-circuit-peerings.md)</span><span class="sxs-lookup"><span data-stu-id="e25c4-259">For more information about circuit peering, see [ExpressRoute circuits and routing domains](expressroute-circuit-peerings.md).</span></span>
* <span data-ttu-id="e25c4-260">Per ulteriori informazioni sull’uso delle reti virtuali, vedere [Panoramica sulla rete virtuale](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e25c4-260">For more information about working with virtual networks, see [Virtual network overview](../virtual-network/virtual-networks-overview.md).</span></span>
