---
title: 'Creare e modificare un circuito ExpressRoute: PowerShell: Azure Resource Manager| Microsoft Docs'
description: In questo articolo viene descritto come toocreate, eseguire il provisioning, verificare, aggiornare, eliminare e il deprovisioning di un circuito ExpressRoute.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="d54e3-103">Creare e modificare un circuito ExpressRoute mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="d54e3-103">Create and modify an ExpressRoute circuit using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d54e3-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d54e3-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="d54e3-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d54e3-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="d54e3-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="d54e3-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="d54e3-107">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d54e3-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="d54e3-108">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="d54e3-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="d54e3-109">In questo articolo viene descritto come toocreate Azure ExpressRoute circuito mediante PowerShell cmdlet e hello Azure Resource Manager modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d54e3-109">This article describes how toocreate an Azure ExpressRoute circuit by using PowerShell cmdlets and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="d54e3-110">Mostra anche come lo stato di hello toocheck del circuito di hello, aggiornare o eliminare e deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="d54e3-110">This article also shows you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d54e3-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="d54e3-111">Before you begin</span></span>
* <span data-ttu-id="d54e3-112">Installare hello l'ultima versione di hello cmdlet PowerShell di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d54e3-112">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="d54e3-113">Per altre informazioni, vedere la [panoramica di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d54e3-113">For more information, see [Overview of Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="d54e3-114">Hello revisione [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="d54e3-114">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>


## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="d54e3-115">Creare un circuito ExpressRoute ed eseguirne il provisioning</span><span class="sxs-lookup"><span data-stu-id="d54e3-115">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a><span data-ttu-id="d54e3-116">1. Accedi tooyour account Azure e selezionare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="d54e3-116">1. Sign in tooyour Azure account and select your subscription</span></span>
<span data-ttu-id="d54e3-117">toobegin della configurazione, accedi tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="d54e3-117">toobegin your configuration, sign in tooyour Azure account.</span></span> <span data-ttu-id="d54e3-118">Hello seguenti esempi toohelp che ci si connette, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="d54e3-118">Use hello following examples toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="d54e3-119">Controllare le sottoscrizioni di hello per hello account:</span><span class="sxs-lookup"><span data-stu-id="d54e3-119">Check hello subscriptions for hello account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="d54e3-120">Selezionare hello sottoscrizione che si desidera toocreate circuiti ExpressRoute per:</span><span class="sxs-lookup"><span data-stu-id="d54e3-120">Select hello subscription that you want toocreate an ExpressRoute circuit for:</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="d54e3-121">2. Ottenere l'elenco di hello di provider supportati, posizioni e delle larghezze di banda</span><span class="sxs-lookup"><span data-stu-id="d54e3-121">2. Get hello list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="d54e3-122">Prima di creare un circuito ExpressRoute, è necessario l'elenco di hello del provider di connettività supportate, località e le opzioni di larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="d54e3-122">Before you create an ExpressRoute circuit, you need hello list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="d54e3-123">cmdlet di PowerShell Hello **Get AzureRmExpressRouteServiceProvider** restituisce queste informazioni, che verranno usati nei passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="d54e3-123">hello PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** returns this information, which you’ll use in later steps:</span></span>

```powershell
Get-AzureRmExpressRouteServiceProvider
```

<span data-ttu-id="d54e3-124">Controllare toosee se viene elencato il provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="d54e3-124">Check toosee if your connectivity provider is listed there.</span></span> <span data-ttu-id="d54e3-125">Prendere nota di hello le seguenti informazioni.</span><span class="sxs-lookup"><span data-stu-id="d54e3-125">Make a note of hello following information.</span></span> <span data-ttu-id="d54e3-126">che saranno necessarie durante la creazione del circuito.</span><span class="sxs-lookup"><span data-stu-id="d54e3-126">You'll need it later when you create a circuit.</span></span>

* <span data-ttu-id="d54e3-127">Nome</span><span class="sxs-lookup"><span data-stu-id="d54e3-127">Name</span></span>
* <span data-ttu-id="d54e3-128">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="d54e3-128">PeeringLocations</span></span>
* <span data-ttu-id="d54e3-129">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="d54e3-129">BandwidthsOffered</span></span>

<span data-ttu-id="d54e3-130">Si è ora pronto toocreate un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d54e3-130">You're now ready toocreate an ExpressRoute circuit.</span></span>   

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="d54e3-131">3. Creare un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="d54e3-131">3. Create an ExpressRoute circuit</span></span>
<span data-ttu-id="d54e3-132">Se non si ha già un gruppo di risorse, è necessario crearne uno prima di creare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d54e3-132">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="d54e3-133">È possibile farlo eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d54e3-133">You can do so by running hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


<span data-ttu-id="d54e3-134">Hello di esempio seguente viene illustrato come un ExpressRoute a 200 Mbps toocreate circuit tramite Equinix Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="d54e3-134">hello following example shows how toocreate a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="d54e3-135">Se si usa un altro provider e impostazioni diverse, sostituire tali informazioni al momento della richiesta.</span><span class="sxs-lookup"><span data-stu-id="d54e3-135">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> <span data-ttu-id="d54e3-136">di seguito Hello è un esempio di richiesta per una nuova chiave di servizio:</span><span class="sxs-lookup"><span data-stu-id="d54e3-136">hello following is an example request for a new service key:</span></span>

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

<span data-ttu-id="d54e3-137">Assicurarsi di specificare hello corretto dello SKU e famiglia di SKU:</span><span class="sxs-lookup"><span data-stu-id="d54e3-137">Make sure that you specify hello correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="d54e3-138">Il livello SKU determina se deve essere abilitato il componente aggiuntivo ExpressRoute Standard o Premium.</span><span class="sxs-lookup"><span data-stu-id="d54e3-138">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="d54e3-139">È possibile specificare *Standard* tooget hello SKU standard o *Premium* per il componente aggiuntivo di hello premium.</span><span class="sxs-lookup"><span data-stu-id="d54e3-139">You can specify *Standard* tooget hello standard SKU or *Premium* for hello premium add-on.</span></span>
* <span data-ttu-id="d54e3-140">Famiglia di SKU determina tipo fatturazione hello.</span><span class="sxs-lookup"><span data-stu-id="d54e3-140">SKU family determines hello billing type.</span></span> <span data-ttu-id="d54e3-141">Specificare *Metereddata* per un piano dati a consumo e *Unlimiteddata* per un piano dati senza limiti.</span><span class="sxs-lookup"><span data-stu-id="d54e3-141">You can specify *Metereddata* for a metered data plan and *Unlimiteddata* for an unlimited data plan.</span></span> <span data-ttu-id="d54e3-142">È possibile modificare il tipo fatturazione di hello da *Metereddata* troppo*Unlimiteddata*, ma è possibile modificare il tipo di hello da *Unlimiteddata* troppo*Metereddata* .</span><span class="sxs-lookup"><span data-stu-id="d54e3-142">You can change hello billing type from *Metereddata* too*Unlimiteddata*, but you can't change hello type from *Unlimiteddata* too*Metereddata*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d54e3-143">Dal momento hello che viene eseguita una chiave del servizio verrà addebitato il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d54e3-143">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="d54e3-144">Assicurarsi di eseguire questa operazione quando il provider di connettività hello è circuito hello tooprovision pronto.</span><span class="sxs-lookup"><span data-stu-id="d54e3-144">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

<span data-ttu-id="d54e3-145">risposta Hello contiene una chiave del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d54e3-145">hello response contains hello service key.</span></span> <span data-ttu-id="d54e3-146">È possibile ottenere una descrizione dettagliata di tutti i parametri di hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d54e3-146">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="d54e3-147">4. Elencare tutti i circuiti ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="d54e3-147">4. List all ExpressRoute circuits</span></span>
<span data-ttu-id="d54e3-148">tooget hello di un elenco di tutti i circuiti ExpressRoute creato, eseguire hello **Get AzureRmExpressRouteCircuit** comando:</span><span class="sxs-lookup"><span data-stu-id="d54e3-148">tooget a list of all hello ExpressRoute circuits that you created, run hello **Get-AzureRmExpressRouteCircuit** command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

<span data-ttu-id="d54e3-149">risposta Hello avrà un aspetto simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d54e3-149">hello response will look similar toohello following example:</span></span>

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
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

<span data-ttu-id="d54e3-150">È possibile recuperare queste informazioni in qualsiasi momento utilizzando hello `Get-AzureRmExpressRouteCircuit` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d54e3-150">You can retrieve this information at any time by using hello `Get-AzureRmExpressRouteCircuit` cmdlet.</span></span> <span data-ttu-id="d54e3-151">Chiamata hello senza parametri, vengono elencati tutti i circuiti hello.</span><span class="sxs-lookup"><span data-stu-id="d54e3-151">Making hello call with no parameters lists all hello circuits.</span></span> <span data-ttu-id="d54e3-152">La chiave del servizio sarà elencata nel hello *ServiceKey* campo:</span><span class="sxs-lookup"><span data-stu-id="d54e3-152">Your service key will be listed in hello *ServiceKey* field:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="d54e3-153">risposta Hello avrà un aspetto simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d54e3-153">hello response will look similar toohello following example:</span></span>

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
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


<span data-ttu-id="d54e3-154">È possibile ottenere una descrizione dettagliata di tutti i parametri di hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d54e3-154">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="d54e3-155">5. Inviare i provider di connettività di hello servizio tooyour chiave per il provisioning</span><span class="sxs-lookup"><span data-stu-id="d54e3-155">5. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="d54e3-156">*ServiceProviderProvisioningState* fornisce informazioni sullo stato corrente di hello di provisioning sul lato di provider di servizi di hello.</span><span class="sxs-lookup"><span data-stu-id="d54e3-156">*ServiceProviderProvisioningState* provides information about hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="d54e3-157">Stato fornisce lo stato di hello in hello lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d54e3-157">Status provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="d54e3-158">Per ulteriori informazioni sul provisioning stati circuito, vedere hello [flussi di lavoro](expressroute-workflows.md#expressroute-circuit-provisioning-states) articolo.</span><span class="sxs-lookup"><span data-stu-id="d54e3-158">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="d54e3-159">Quando si crea un nuovo circuito ExpressRoute, circuito hello sarà nel seguente stato hello:</span><span class="sxs-lookup"><span data-stu-id="d54e3-159">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



<span data-ttu-id="d54e3-160">circuito Hello cambierà toohello seguente lo stato quando il provider di connettività hello è in corso di hello di abilitarlo per l'utente:</span><span class="sxs-lookup"><span data-stu-id="d54e3-160">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="d54e3-161">Per è toobe in grado di toouse un circuito ExpressRoute, deve essere nel seguente stato hello:</span><span class="sxs-lookup"><span data-stu-id="d54e3-161">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="d54e3-162">6. Controllare periodicamente hello stato della chiave circuito hello e hello</span><span class="sxs-lookup"><span data-stu-id="d54e3-162">6. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="d54e3-163">Controllo stato hello della chiave circuito hello e hello consente di sapere quando il circuito viene abilitato il provider.</span><span class="sxs-lookup"><span data-stu-id="d54e3-163">Checking hello status and hello state of hello circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="d54e3-164">Dopo aver configurato il circuito hello, *ServiceProviderProvisioningState* viene visualizzato come *provisioning eseguito*, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="d54e3-164">After hello circuit has been configured, *ServiceProviderProvisioningState* appears as *Provisioned*, as shown in hello following example:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="d54e3-165">risposta Hello avrà un aspetto simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d54e3-165">hello response will look similar toohello following example:</span></span>

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

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="d54e3-166">7. Creare la configurazione di routing</span><span class="sxs-lookup"><span data-stu-id="d54e3-166">7. Create your routing configuration</span></span>
<span data-ttu-id="d54e3-167">Per istruzioni dettagliate, vedere hello [configurazione del routing circuito ExpressRoute](expressroute-howto-routing-arm.md) toocreate dell'articolo e modificare peering di circuito.</span><span class="sxs-lookup"><span data-stu-id="d54e3-167">For step-by-step instructions, see hello [ExpressRoute circuit routing configuration](expressroute-howto-routing-arm.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d54e3-168">Queste istruzioni si applicano solo toocircuits creati con i provider di servizi che offrono servizi di livello 2 di connettività.</span><span class="sxs-lookup"><span data-stu-id="d54e3-168">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="d54e3-169">Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito un IP VPN, come MPLS), il provider di connettività configurerà e gestirà il routing per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d54e3-169">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="d54e3-170">8. Collegare un circuito ExpressRoute di tooan rete virtuale</span><span class="sxs-lookup"><span data-stu-id="d54e3-170">8. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="d54e3-171">Successivamente, collegare un circuito ExpressRoute di tooyour rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="d54e3-171">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="d54e3-172">Hello utilizzare [collegamento virtuale reti circuiti tooExpressRoute](expressroute-howto-linkvnet-arm.md) articolo quando si lavora con modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="d54e3-172">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="d54e3-173">Ottenere lo stato di hello di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="d54e3-173">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="d54e3-174">È possibile recuperare queste informazioni in qualsiasi momento utilizzando hello **Get AzureRmExpressRouteCircuit** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d54e3-174">You can retrieve this information at any time by using hello **Get-AzureRmExpressRouteCircuit** cmdlet.</span></span> <span data-ttu-id="d54e3-175">Chiamata hello senza parametri, vengono elencati tutti i circuiti hello.</span><span class="sxs-lookup"><span data-stu-id="d54e3-175">Making hello call with no parameters lists all hello circuits.</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="d54e3-176">risposta di Hello sarà simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d54e3-176">hello response will be similar toohello following example:</span></span>

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


<span data-ttu-id="d54e3-177">È possibile ottenere informazioni su un circuito ExpressRoute specifico passando nome gruppo di risorse hello e il nome del circuito come una chiamata di toohello parametro:</span><span class="sxs-lookup"><span data-stu-id="d54e3-177">You can get information on a specific ExpressRoute circuit by passing hello resource group name and circuit name as a parameter toohello call:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="d54e3-178">risposta Hello avrà un aspetto simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="d54e3-178">hello response will look similar toohello following example:</span></span>

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


<span data-ttu-id="d54e3-179">È possibile ottenere una descrizione dettagliata di tutti i parametri di hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d54e3-179">You can get detailed descriptions of all hello parameters by running hello following command:</span></span>

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <span data-ttu-id="d54e3-180"><a name="modify"></a>Modifica di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="d54e3-180"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="d54e3-181">È possibile modificare determinate proprietà di un circuito ExpressRoute senza conseguenze per la connettività.</span><span class="sxs-lookup"><span data-stu-id="d54e3-181">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="d54e3-182">È possibile eseguire hello seguenti senza tempi di inattività:</span><span class="sxs-lookup"><span data-stu-id="d54e3-182">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="d54e3-183">Abilitare o disabilitare un componente aggiuntivo ExpressRoute Premium per il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d54e3-183">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="d54e3-184">Aumento della larghezza di banda hello del circuito ExpressRoute fornito è la capacità disponibile sulla porta hello.</span><span class="sxs-lookup"><span data-stu-id="d54e3-184">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="d54e3-185">Il downgrade della larghezza di banda hello di un circuito non è supportato.</span><span class="sxs-lookup"><span data-stu-id="d54e3-185">Downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="d54e3-186">Modificare hello piano dati a consumo tooUnlimited dati di controllo.</span><span class="sxs-lookup"><span data-stu-id="d54e3-186">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="d54e3-187">Modifica hello misurazione piano da dati senza limiti tooMetered che dati non è supportata.</span><span class="sxs-lookup"><span data-stu-id="d54e3-187">Changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="d54e3-188">È possibile abilitare e disabilitare l'opzione *Allow Classic Operations*(Consenti operazioni classiche).</span><span class="sxs-lookup"><span data-stu-id="d54e3-188">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="d54e3-189">Per ulteriori informazioni su limiti e limitazioni, vedere toohello [domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="d54e3-189">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="tooenable-hello-expressroute-premium-add-on"></a><span data-ttu-id="d54e3-190">componente aggiuntivo di tooenable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="d54e3-190">tooenable hello ExpressRoute premium add-on</span></span>
<span data-ttu-id="d54e3-191">È possibile abilitare il componente aggiuntivo di hello ExpressRoute premium per il circuito esistente utilizzando hello seguente frammento di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d54e3-191">You can enable hello ExpressRoute premium add-on for your existing circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

<span data-ttu-id="d54e3-192">circuito Hello avranno ora le funzionalità dei componenti aggiuntivi di hello ExpressRoute premium abilitata.</span><span class="sxs-lookup"><span data-stu-id="d54e3-192">hello circuit will now have hello ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="d54e3-193">Verrà avviato fatturazione è per la funzionalità di componente aggiuntivo di hello premium come comando hello è stata eseguita correttamente.</span><span class="sxs-lookup"><span data-stu-id="d54e3-193">We will begin billing you for hello premium add-on capability as soon as hello command has successfully run.</span></span>

### <a name="toodisable-hello-expressroute-premium-add-on"></a><span data-ttu-id="d54e3-194">componente aggiuntivo di toodisable hello ExpressRoute premium</span><span class="sxs-lookup"><span data-stu-id="d54e3-194">toodisable hello ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d54e3-195">Questa operazione può non riuscire se si utilizza le risorse che sono maggiori di ciò che è consentito per il circuito standard hello.</span><span class="sxs-lookup"><span data-stu-id="d54e3-195">This operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

<span data-ttu-id="d54e3-196">Si noti hello segue:</span><span class="sxs-lookup"><span data-stu-id="d54e3-196">Note hello following:</span></span>

* <span data-ttu-id="d54e3-197">Prima effettuare il downgrade da premium toostandard, è necessario verificare tale numero hello di reti virtuali collegate circuito toohello è inferiore a 10.</span><span class="sxs-lookup"><span data-stu-id="d54e3-197">Before you downgrade from premium toostandard, you must ensure that hello number of virtual networks that are linked toohello circuit is less than 10.</span></span> <span data-ttu-id="d54e3-198">In caso contrario, la richiesta di aggiornamento avrà esito negativo e verranno fatturate le tariffe Premium.</span><span class="sxs-lookup"><span data-stu-id="d54e3-198">If you don't do this, your update request fails, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="d54e3-199">È necessario scollegare tutte le reti virtuali in altre aree geopolitiche.</span><span class="sxs-lookup"><span data-stu-id="d54e3-199">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="d54e3-200">In caso contrario, la richiesta di aggiornamento avrà esito negativo e verranno fatturate le tariffe Premium.</span><span class="sxs-lookup"><span data-stu-id="d54e3-200">If you don't do this, your update request will fail, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="d54e3-201">La tabella di route deve includere meno di 4.000 route per il peering privato.</span><span class="sxs-lookup"><span data-stu-id="d54e3-201">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="d54e3-202">Se le dimensioni di tabella di route sono maggiore di 4.000 route, sessione BGP hello Elimina e non verrà riabilitata fino a quando il numero di hello di prefissi annunciati scende sotto 4.000.</span><span class="sxs-lookup"><span data-stu-id="d54e3-202">If your route table size is greater than 4,000 routes, hello BGP session drops and won't be reenabled until hello number of advertised prefixes goes below 4,000.</span></span>

<span data-ttu-id="d54e3-203">È possibile disabilitare componente aggiuntivo di hello ExpressRoute premium per il circuito esistente hello utilizzando hello cmdlet di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="d54e3-203">You can disable hello ExpressRoute premium add-on for hello existing circuit by using hello following PowerShell cmdlet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a><span data-ttu-id="d54e3-204">larghezza di banda circuito ExpressRoute hello tooupdate</span><span class="sxs-lookup"><span data-stu-id="d54e3-204">tooupdate hello ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="d54e3-205">Per le larghezze di banda supportate per il provider, controllare hello [domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="d54e3-205">For supported bandwidth options for your provider, check hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="d54e3-206">È possibile scegliere qualsiasi dimensione maggiore della dimensione hello del circuito esistente.</span><span class="sxs-lookup"><span data-stu-id="d54e3-206">You can pick any size greater than hello size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d54e3-207">Potrebbe essere circuito ExpressRoute di hello toorecreate se ha capacità insufficiente sulla porta esistente hello.</span><span class="sxs-lookup"><span data-stu-id="d54e3-207">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="d54e3-208">Se non è presente capacità aggiuntive disponibili in tale posizione non è possibile aggiornare il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="d54e3-208">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="d54e3-209">È possibile ridurre la larghezza di banda hello di un circuito ExpressRoute senza interruzioni.</span><span class="sxs-lookup"><span data-stu-id="d54e3-209">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="d54e3-210">Il downgrade della larghezza di banda è necessario il circuito ExpressRoute toodeprovision hello e quindi ripetere il provisioning di un nuovo circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d54e3-210">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 

<span data-ttu-id="d54e3-211">Dopo aver stabilito quali dimensioni, è necessario, usare il circuito hello tooresize di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d54e3-211">After you decide what size you need, use hello following command tooresize your circuit:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


<span data-ttu-id="d54e3-212">Il circuito verrà ridimensionato sul lato Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="d54e3-212">Your circuit will be sized up on hello Microsoft side.</span></span> <span data-ttu-id="d54e3-213">È quindi necessario contattare le configurazioni di tooupdate provider di connettività nella loro toomatch lato questa modifica.</span><span class="sxs-lookup"><span data-stu-id="d54e3-213">Then you must contact your connectivity provider tooupdate configurations on their side toomatch this change.</span></span> <span data-ttu-id="d54e3-214">Dopo aver apportato questa notifica, verrà avviato è fatturazione per l'opzione di hello aggiornato della larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="d54e3-214">After you make this notification, we will begin billing you for hello updated bandwidth option.</span></span>

### <a name="toomove-hello-sku-from-metered-toounlimited"></a><span data-ttu-id="d54e3-215">toomove hello SKU da toounlimited a consumo</span><span class="sxs-lookup"><span data-stu-id="d54e3-215">toomove hello SKU from metered toounlimited</span></span>
<span data-ttu-id="d54e3-216">È possibile modificare hello SKU di un circuito ExpressRoute tramite hello seguente frammento di PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d54e3-216">You can change hello SKU of an ExpressRoute circuit by using hello following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a><span data-ttu-id="d54e3-217">classica di toohello toocontrol accesso e gli ambienti di gestione risorse</span><span class="sxs-lookup"><span data-stu-id="d54e3-217">toocontrol access toohello classic and Resource Manager environments</span></span>
<span data-ttu-id="d54e3-218">Rivedere le istruzioni di hello in [circuiti ExpressRoute spostare dal modello di distribuzione di gestione risorse toohello classico hello](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="d54e3-218">Review hello instructions in [Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="d54e3-219">Deprovisioning ed eliminazione di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="d54e3-219">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="d54e3-220">Si noti hello segue:</span><span class="sxs-lookup"><span data-stu-id="d54e3-220">Note hello following:</span></span>

* <span data-ttu-id="d54e3-221">È necessario scollegare tutte le reti virtuali da hello circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="d54e3-221">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="d54e3-222">Se questa operazione non riesce, controllare toosee se sono configurate reti virtuali collegate toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="d54e3-222">If this operation fails, check toosee if any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="d54e3-223">Se il provider del servizio di circuito ExpressRoute di hello lo stato di provisioning **Provisioning** o **provisioning eseguito** è necessario collaborare con il circuito di hello toodeprovision provider del servizio sul relativo lato.</span><span class="sxs-lookup"><span data-stu-id="d54e3-223">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="d54e3-224">Si continuerà tooreserve risorse e a pagamento fino a quando il provider di servizi di hello completa deprovisioning circuito hello e invia una notifica di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d54e3-224">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="d54e3-225">Se il provider di servizi di hello è deprovisioning circuito hello (provider di servizi di hello lo stato di provisioning è stato impostato troppo**non è stato eseguito il provisioning**) è possibile eliminare il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="d54e3-225">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="d54e3-226">Questa operazione arresterà la fatturazione per il circuito hello</span><span class="sxs-lookup"><span data-stu-id="d54e3-226">This will stop billing for hello circuit</span></span>

<span data-ttu-id="d54e3-227">È possibile eliminare il circuito ExpressRoute eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d54e3-227">You can delete your ExpressRoute circuit by running hello following command:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a><span data-ttu-id="d54e3-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d54e3-228">Next steps</span></span>

<span data-ttu-id="d54e3-229">Dopo aver creato il circuito, verificare che hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="d54e3-229">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="d54e3-230">Creare e modificare il routing per un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="d54e3-230">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="d54e3-231">Collegamento del circuito ExpressRoute di tooyour di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="d54e3-231">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
