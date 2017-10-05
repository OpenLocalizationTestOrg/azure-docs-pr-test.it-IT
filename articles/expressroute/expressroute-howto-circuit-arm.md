---
title: 'Creare e modificare un circuito ExpressRoute: PowerShell: Azure Resource Manager| Microsoft Docs'
description: Questo articolo descrive le procedure di creazione, provisioning, verifica, aggiornamento, eliminazione e deprovisioning di un circuito ExpressRoute.
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
ms.openlocfilehash: 8bfae39d84aaac3b9527084df9dcfbd51f591dfe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a><span data-ttu-id="2e1c8-103">Creare e modificare un circuito ExpressRoute mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e1c8-103">Create and modify an ExpressRoute circuit using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e1c8-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2e1c8-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="2e1c8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e1c8-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="2e1c8-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="2e1c8-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="2e1c8-107">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2e1c8-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="2e1c8-108">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="2e1c8-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="2e1c8-109">Questo articolo illustra i passaggi per creare un circuito ExpressRoute di Azure tramite i cmdlet di PowerShell e il modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-109">This article describes how to create an Azure ExpressRoute circuit by using PowerShell cmdlets and the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="2e1c8-110">L'articolo descrive anche le procedure di controllo di stato, aggiornamento, eliminazione e deprovisioning del circuito.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-110">This article also shows you how to check the status of the circuit, update it, or delete and deprovision it.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2e1c8-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="2e1c8-111">Before you begin</span></span>
* <span data-ttu-id="2e1c8-112">Installare la versione più recente dei cmdlet di PowerShell per Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-112">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="2e1c8-113">Per altre informazioni, vedere la [panoramica di Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2e1c8-113">For more information, see [Overview of Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="2e1c8-114">Prima di iniziare la configurazione, verificare i [prerequisiti](expressroute-prerequisites.md) e i [flussi di lavoro](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="2e1c8-114">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>


## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="2e1c8-115">Creare un circuito ExpressRoute ed eseguirne il provisioning</span><span class="sxs-lookup"><span data-stu-id="2e1c8-115">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-to-your-azure-account-and-select-your-subscription"></a><span data-ttu-id="2e1c8-116">1. Accedere al proprio account Azure e selezionare la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="2e1c8-116">1. Sign in to your Azure account and select your subscription</span></span>
<span data-ttu-id="2e1c8-117">Per iniziare la configurazione, accedere al proprio account Azure.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-117">To begin your configuration, sign in to your Azure account.</span></span> <span data-ttu-id="2e1c8-118">Per eseguire la connessione, usare gli esempi che seguono:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-118">Use the following examples to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="2e1c8-119">Controllare le sottoscrizioni per l'account:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-119">Check the subscriptions for the account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="2e1c8-120">Selezionare la sottoscrizione per la quale si vuole creare un circuito ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-120">Select the subscription that you want to create an ExpressRoute circuit for:</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-the-list-of-supported-providers-locations-and-bandwidths"></a><span data-ttu-id="2e1c8-121">2. Ottenere l'elenco dei provider, delle località e delle larghezze di banda supportate</span><span class="sxs-lookup"><span data-stu-id="2e1c8-121">2. Get the list of supported providers, locations, and bandwidths</span></span>
<span data-ttu-id="2e1c8-122">Prima di creare un circuito ExpressRoute, è necessario avere l'elenco delle località, delle opzioni di larghezza di banda e dei provider di connettività supportati.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-122">Before you create an ExpressRoute circuit, you need the list of supported connectivity providers, locations, and bandwidth options.</span></span>

<span data-ttu-id="2e1c8-123">Il cmdlet **Get-AzureRmExpressRouteServiceProvider** di PowerShell restituisce queste informazioni, che verranno usate nei passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-123">The PowerShell cmdlet **Get-AzureRmExpressRouteServiceProvider** returns this information, which you’ll use in later steps:</span></span>

```powershell
Get-AzureRmExpressRouteServiceProvider
```

<span data-ttu-id="2e1c8-124">Verificare se sia presente anche il proprio provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-124">Check to see if your connectivity provider is listed there.</span></span> <span data-ttu-id="2e1c8-125">Annotare le informazioni seguenti,</span><span class="sxs-lookup"><span data-stu-id="2e1c8-125">Make a note of the following information.</span></span> <span data-ttu-id="2e1c8-126">che saranno necessarie durante la creazione del circuito.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-126">You'll need it later when you create a circuit.</span></span>

* <span data-ttu-id="2e1c8-127">Nome</span><span class="sxs-lookup"><span data-stu-id="2e1c8-127">Name</span></span>
* <span data-ttu-id="2e1c8-128">PeeringLocations</span><span class="sxs-lookup"><span data-stu-id="2e1c8-128">PeeringLocations</span></span>
* <span data-ttu-id="2e1c8-129">BandwidthsOffered</span><span class="sxs-lookup"><span data-stu-id="2e1c8-129">BandwidthsOffered</span></span>

<span data-ttu-id="2e1c8-130">È ora possibile creare un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-130">You're now ready to create an ExpressRoute circuit.</span></span>   

### <a name="3-create-an-expressroute-circuit"></a><span data-ttu-id="2e1c8-131">3. Creare un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="2e1c8-131">3. Create an ExpressRoute circuit</span></span>
<span data-ttu-id="2e1c8-132">Se non si ha già un gruppo di risorse, è necessario crearne uno prima di creare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-132">If you don't already have a resource group, you must create one before you create your ExpressRoute circuit.</span></span> <span data-ttu-id="2e1c8-133">A questo scopo, eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-133">You can do so by running the following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


<span data-ttu-id="2e1c8-134">L'esempio seguente illustra come creare un circuito ExpressRoute a 200 Mbps tramite Equinix nella Silicon Valley.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-134">The following example shows how to create a 200-Mbps ExpressRoute circuit through Equinix in Silicon Valley.</span></span> <span data-ttu-id="2e1c8-135">Se si usa un altro provider e impostazioni diverse, sostituire tali informazioni al momento della richiesta.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-135">If you're using a different provider and different settings, substitute that information when you make your request.</span></span> <span data-ttu-id="2e1c8-136">Di seguito è riportato un esempio di richiesta di una nuova chiave di servizio:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-136">The following is an example request for a new service key:</span></span>

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

<span data-ttu-id="2e1c8-137">Verificare di aver specificato il livello e la famiglia SKU corretti:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-137">Make sure that you specify the correct SKU tier and SKU family:</span></span>

* <span data-ttu-id="2e1c8-138">Il livello SKU determina se deve essere abilitato il componente aggiuntivo ExpressRoute Standard o Premium.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-138">SKU tier determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="2e1c8-139">È possibile specificare *Standard* per ottenere lo SKU Standard o *Premium* per il componente aggiuntivo Premium.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-139">You can specify *Standard* to get the standard SKU or *Premium* for the premium add-on.</span></span>
* <span data-ttu-id="2e1c8-140">La famiglia SKU determina il tipo di fatturazione.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-140">SKU family determines the billing type.</span></span> <span data-ttu-id="2e1c8-141">Specificare *Metereddata* per un piano dati a consumo e *Unlimiteddata* per un piano dati senza limiti.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-141">You can specify *Metereddata* for a metered data plan and *Unlimiteddata* for an unlimited data plan.</span></span> <span data-ttu-id="2e1c8-142">È possibile modificare il tipo di fatturazione da *Metereddata* a *Unlimiteddata*, ma *non* è possibile eseguire il passaggio *inverso*.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-142">You can change the billing type from *Metereddata* to *Unlimiteddata*, but you can't change the type from *Unlimiteddata* to *Metereddata*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e1c8-143">Il circuito ExpressRoute viene addebitato dal momento in cui emessa una chiave di servizio.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-143">Your ExpressRoute circuit will be billed from the moment a service key is issued.</span></span> <span data-ttu-id="2e1c8-144">Verificare che l'operazione venga eseguita quando il provider di connettività è pronto a effettuare il provisioning del circuito.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-144">Ensure that you perform this operation when the connectivity provider is ready to provision the circuit.</span></span>
> 
> 

<span data-ttu-id="2e1c8-145">La risposta contiene la chiave di servizio.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-145">The response contains the service key.</span></span> <span data-ttu-id="2e1c8-146">È possibile ottenere descrizioni dettagliate di tutti i parametri eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-146">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a><span data-ttu-id="2e1c8-147">4. Elencare tutti i circuiti ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="2e1c8-147">4. List all ExpressRoute circuits</span></span>
<span data-ttu-id="2e1c8-148">Per ottenere un elenco di tutti i circuiti ExpressRoute creati, eseguire il comando **Get-AzureRmExpressRouteCircuit**:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-148">To get a list of all the ExpressRoute circuits that you created, run the **Get-AzureRmExpressRouteCircuit** command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

<span data-ttu-id="2e1c8-149">La risposta ha un aspetto simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-149">The response will look similar to the following example:</span></span>

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

<span data-ttu-id="2e1c8-150">È possibile recuperare queste informazioni in qualsiasi momento usando il cmdlet `Get-AzureRmExpressRouteCircuit` .</span><span class="sxs-lookup"><span data-stu-id="2e1c8-150">You can retrieve this information at any time by using the `Get-AzureRmExpressRouteCircuit` cmdlet.</span></span> <span data-ttu-id="2e1c8-151">Se si effettua la chiamata senza parametri, verranno elencati tutti i circuiti.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-151">Making the call with no parameters lists all the circuits.</span></span> <span data-ttu-id="2e1c8-152">La chiave di servizio verrà elencata nel campo *ServiceKey* :</span><span class="sxs-lookup"><span data-stu-id="2e1c8-152">Your service key will be listed in the *ServiceKey* field:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="2e1c8-153">La risposta ha un aspetto simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-153">The response will look similar to the following example:</span></span>

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


<span data-ttu-id="2e1c8-154">È possibile ottenere descrizioni dettagliate di tutti i parametri eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-154">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a><span data-ttu-id="2e1c8-155">5. Inviare la chiave di servizio al provider di connettività per il provisioning</span><span class="sxs-lookup"><span data-stu-id="2e1c8-155">5. Send the service key to your connectivity provider for provisioning</span></span>
<span data-ttu-id="2e1c8-156">*ServiceProviderProvisioningState* offre informazioni sullo stato di provisioning corrente sul lato provider del servizio.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-156">*ServiceProviderProvisioningState* provides information about the current state of provisioning on the service-provider side.</span></span> <span data-ttu-id="2e1c8-157">Status indica lo stato sul lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-157">Status provides the state on the Microsoft side.</span></span> <span data-ttu-id="2e1c8-158">Per altre informazioni sullo stato di provisioning dei circuiti, vedere l'articolo relativo ai [flussi di lavoro](expressroute-workflows.md#expressroute-circuit-provisioning-states) .</span><span class="sxs-lookup"><span data-stu-id="2e1c8-158">For more information about circuit provisioning states, see the [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="2e1c8-159">Quando si crea un nuovo circuito ExpressRoute, il circuito ha lo stato seguente:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-159">When you create a new ExpressRoute circuit, the circuit will be in the following state:</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



<span data-ttu-id="2e1c8-160">Il circuito passa allo stato seguente quando è in corso l'abilitazione da parte del provider di connettività:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-160">The circuit will change to the following state when the connectivity provider is in the process of enabling it for you:</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

<span data-ttu-id="2e1c8-161">Per poterlo usare, un circuito ExpressRoute deve avere lo stato seguente:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-161">For you to be able to use an ExpressRoute circuit, it must be in the following state:</span></span>

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a><span data-ttu-id="2e1c8-162">6. Controllare periodicamente lo stato e la condizione della chiave del circuito</span><span class="sxs-lookup"><span data-stu-id="2e1c8-162">6. Periodically check the status and the state of the circuit key</span></span>
<span data-ttu-id="2e1c8-163">La verifica dello stato e della condizione della chiave del circuito comunicano all'utente quando il provider ha abilitato il circuito.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-163">Checking the status and the state of the circuit key lets you know when your provider has enabled your circuit.</span></span> <span data-ttu-id="2e1c8-164">Dopo la configurazione del circuito, lo stato di *ServiceProviderProvisioningState* visualizzato è *Provisioned*, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-164">After the circuit has been configured, *ServiceProviderProvisioningState* appears as *Provisioned*, as shown in the following example:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="2e1c8-165">La risposta ha un aspetto simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-165">The response will look similar to the following example:</span></span>

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

### <a name="7-create-your-routing-configuration"></a><span data-ttu-id="2e1c8-166">7. Creare la configurazione di routing</span><span class="sxs-lookup"><span data-stu-id="2e1c8-166">7. Create your routing configuration</span></span>
<span data-ttu-id="2e1c8-167">Per istruzioni dettagliate, vedere l'articolo relativo alla [configurazione del routing per un circuito ExpressRoute](expressroute-howto-routing-arm.md) per creare e modificare i peering del circuito.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-167">For step-by-step instructions, see the [ExpressRoute circuit routing configuration](expressroute-howto-routing-arm.md) article to create and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e1c8-168">Queste istruzioni si applicano solo ai circuiti creati con provider di servizi che offrono servizi di connettività di livello 2.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-168">These instructions only apply to circuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="2e1c8-169">Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito un IP VPN, come MPLS), il provider di connettività configurerà e gestirà il routing per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-169">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="8-link-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="2e1c8-170">8. Collegare una rete virtuale a un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="2e1c8-170">8. Link a virtual network to an ExpressRoute circuit</span></span>
<span data-ttu-id="2e1c8-171">Collegare quindi una rete virtuale al circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-171">Next, link a virtual network to your ExpressRoute circuit.</span></span> <span data-ttu-id="2e1c8-172">Fare riferimento all'articolo [Collegare una rete virtuale a un circuito ExpressRoute](expressroute-howto-linkvnet-arm.md) quando si usa il modello di distribuzione di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-172">Use the [Linking virtual networks to ExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with the Resource Manager deployment model.</span></span>

## <a name="getting-the-status-of-an-expressroute-circuit"></a><span data-ttu-id="2e1c8-173">Ottenere lo stato di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="2e1c8-173">Getting the status of an ExpressRoute circuit</span></span>
<span data-ttu-id="2e1c8-174">È possibile recuperare queste informazioni in qualsiasi momento usando il cmdlet **Get-AzureRmExpressRouteCircuit**.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-174">You can retrieve this information at any time by using the **Get-AzureRmExpressRouteCircuit** cmdlet.</span></span> <span data-ttu-id="2e1c8-175">Se si effettua la chiamata senza parametri, verranno elencati tutti i circuiti.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-175">Making the call with no parameters lists all the circuits.</span></span>

```powershell
Get-AzureRmExpressRouteCircuit
```


<span data-ttu-id="2e1c8-176">La risposta sarà simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-176">The response will be similar to the following example:</span></span>

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


<span data-ttu-id="2e1c8-177">È possibile ottenere informazioni su un circuito ExpressRoute specifico passando il nome del gruppo di risorse e il nome del circuito come parametri alla chiamata:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-177">You can get information on a specific ExpressRoute circuit by passing the resource group name and circuit name as a parameter to the call:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


<span data-ttu-id="2e1c8-178">La risposta ha un aspetto simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-178">The response will look similar to the following example:</span></span>

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


<span data-ttu-id="2e1c8-179">È possibile ottenere descrizioni dettagliate di tutti i parametri eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-179">You can get detailed descriptions of all the parameters by running the following command:</span></span>

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <span data-ttu-id="2e1c8-180"><a name="modify"></a>Modifica di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="2e1c8-180"><a name="modify"></a>Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="2e1c8-181">È possibile modificare determinate proprietà di un circuito ExpressRoute senza conseguenze per la connettività.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-181">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="2e1c8-182">È possibile eseguire le operazioni seguenti senza tempi di inattività:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-182">You can do the following with no downtime:</span></span>

* <span data-ttu-id="2e1c8-183">Abilitare o disabilitare un componente aggiuntivo ExpressRoute Premium per il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-183">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="2e1c8-184">Aumentare la larghezza di banda del circuito ExpressRoute, a condizione che sulla porta sia disponibile capacità.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-184">Increase the bandwidth of your ExpressRoute circuit provided there is capacity available on the port.</span></span> <span data-ttu-id="2e1c8-185">Il downgrade della larghezza di banda di un circuito non è supportato.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-185">Downgrading the bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="2e1c8-186">Modificare il piano di misurazione da Dati a consumo a Dati senza limiti.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-186">Change the metering plan from Metered Data to Unlimited Data.</span></span> <span data-ttu-id="2e1c8-187">La modifica del piano di misurazione da Dati senza limiti a Dati a consumo non è supportata.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-187">Changing the metering plan from Unlimited Data to Metered Data is not supported.</span></span>
* <span data-ttu-id="2e1c8-188">È possibile abilitare e disabilitare l'opzione *Allow Classic Operations*(Consenti operazioni classiche).</span><span class="sxs-lookup"><span data-stu-id="2e1c8-188">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="2e1c8-189">Per altre informazioni su limiti e limitazioni, vedere [Domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="2e1c8-189">For more information on limits and limitations, refer to the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

### <a name="to-enable-the-expressroute-premium-add-on"></a><span data-ttu-id="2e1c8-190">Per abilitare il componente aggiuntivo ExpressRoute Premium</span><span class="sxs-lookup"><span data-stu-id="2e1c8-190">To enable the ExpressRoute premium add-on</span></span>
<span data-ttu-id="2e1c8-191">È possibile abilitare il componente aggiuntivo ExpressRoute Premium per il circuito esistente usando il frammento di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-191">You can enable the ExpressRoute premium add-on for your existing circuit by using the following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

<span data-ttu-id="2e1c8-192">Le funzionalità del componente aggiuntivo ExpressRoute Premium sono così abilitate nel circuito.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-192">The circuit will now have the ExpressRoute premium add-on features enabled.</span></span> <span data-ttu-id="2e1c8-193">La fatturazione della funzionalità del componente aggiuntivo Premium inizierà non appena il comando verrà eseguito correttamente.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-193">We will begin billing you for the premium add-on capability as soon as the command has successfully run.</span></span>

### <a name="to-disable-the-expressroute-premium-add-on"></a><span data-ttu-id="2e1c8-194">Per disabilitare il componente aggiuntivo ExpressRoute Premium</span><span class="sxs-lookup"><span data-stu-id="2e1c8-194">To disable the ExpressRoute premium add-on</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2e1c8-195">Questa operazione può avere esito negativo se si usano più risorse di quelle consentite per il circuito standard.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-195">This operation can fail if you're using resources that are greater than what is permitted for the standard circuit.</span></span>
> 
> 

<span data-ttu-id="2e1c8-196">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-196">Note the following:</span></span>

* <span data-ttu-id="2e1c8-197">Prima di effettuare il downgrade da Premium a Standard, è necessario assicurarsi che il numero di reti virtuali collegate al circuito sia minore di 10.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-197">Before you downgrade from premium to standard, you must ensure that the number of virtual networks that are linked to the circuit is less than 10.</span></span> <span data-ttu-id="2e1c8-198">In caso contrario, la richiesta di aggiornamento avrà esito negativo e verranno fatturate le tariffe Premium.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-198">If you don't do this, your update request fails, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="2e1c8-199">È necessario scollegare tutte le reti virtuali in altre aree geopolitiche.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-199">You must unlink all virtual networks in other geopolitical regions.</span></span> <span data-ttu-id="2e1c8-200">In caso contrario, la richiesta di aggiornamento avrà esito negativo e verranno fatturate le tariffe Premium.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-200">If you don't do this, your update request will fail, and we will bill you at premium rates.</span></span>
* <span data-ttu-id="2e1c8-201">La tabella di route deve includere meno di 4.000 route per il peering privato.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-201">Your route table must be less than 4,000 routes for private peering.</span></span> <span data-ttu-id="2e1c8-202">Se la tabella di route include più di 4.000 route, la sessione BGP viene eliminata e non sarà riabilitata finché il numero di prefissi pubblicati non scenderà al di sotto di 4.000.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-202">If your route table size is greater than 4,000 routes, the BGP session drops and won't be reenabled until the number of advertised prefixes goes below 4,000.</span></span>

<span data-ttu-id="2e1c8-203">È possibile disabilitare il componente aggiuntivo ExpressRoute Premium per il circuito esistente usando il cmdlet di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-203">You can disable the ExpressRoute premium add-on for the existing circuit by using the following PowerShell cmdlet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-update-the-expressroute-circuit-bandwidth"></a><span data-ttu-id="2e1c8-204">Per aggiornare la larghezza di banda del circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="2e1c8-204">To update the ExpressRoute circuit bandwidth</span></span>
<span data-ttu-id="2e1c8-205">Per le opzioni relative alla larghezza di banda supportate per il provider, vedere [Domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="2e1c8-205">For supported bandwidth options for your provider, check the [ExpressRoute FAQ](expressroute-faqs.md).</span></span> <span data-ttu-id="2e1c8-206">È possibile scegliere qualsiasi dimensione maggiore della dimensione del circuito esistente.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-206">You can pick any size greater than the size of your existing circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2e1c8-207">Se la capacità sulla porta esistente non è sufficiente, potrebbe essere necessario ricreare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-207">You may have to recreate the ExpressRoute circuit if there is inadequate capacity on the existing port.</span></span> <span data-ttu-id="2e1c8-208">Il circuito non può essere aggiornato se in tale posizione non è disponibile capacità aggiuntiva.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-208">You cannot upgrade the circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="2e1c8-209">Non è possibile ridurre la larghezza di banda di un circuito ExpressRoute senza interruzioni.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-209">You cannot reduce the bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="2e1c8-210">Il downgrade della larghezza di banda richiede il deprovisioning del circuito ExpressRoute e quindi il provisioning di un nuovo circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-210">Downgrading bandwidth requires you to deprovision the ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 

<span data-ttu-id="2e1c8-211">Una volta stabilite le dimensioni necessarie, usare il comando seguente per ridimensionare il circuito:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-211">After you decide what size you need, use the following command to resize your circuit:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


<span data-ttu-id="2e1c8-212">Il circuito verrà ridimensionato su lato di competenza di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-212">Your circuit will be sized up on the Microsoft side.</span></span> <span data-ttu-id="2e1c8-213">Sarà quindi necessario contattare il provider di connettività perché aggiorni le configurazioni corrispondenti in base a questa modifica.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-213">Then you must contact your connectivity provider to update configurations on their side to match this change.</span></span> <span data-ttu-id="2e1c8-214">In seguito alla notifica, Microsoft inizierà la fatturazione in base all'opzione relativa alla larghezza di banda aggiornata.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-214">After you make this notification, we will begin billing you for the updated bandwidth option.</span></span>

### <a name="to-move-the-sku-from-metered-to-unlimited"></a><span data-ttu-id="2e1c8-215">Per passare lo SKU dal piano a consumo al piano senza limiti</span><span class="sxs-lookup"><span data-stu-id="2e1c8-215">To move the SKU from metered to unlimited</span></span>
<span data-ttu-id="2e1c8-216">È possibile modificare lo SKU di un circuito ExpressRoute usando il frammento di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-216">You can change the SKU of an ExpressRoute circuit by using the following PowerShell snippet:</span></span>

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-control-access-to-the-classic-and-resource-manager-environments"></a><span data-ttu-id="2e1c8-217">Per controllare l'accesso all'ambiente classico e all'ambiente Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2e1c8-217">To control access to the classic and Resource Manager environments</span></span>
<span data-ttu-id="2e1c8-218">Vedere le istruzioni contenute in [Spostare i circuiti ExpressRoute dal modello di distribuzione classica a quello Resource Manager](expressroute-howto-move-arm.md).</span><span class="sxs-lookup"><span data-stu-id="2e1c8-218">Review the instructions in [Move ExpressRoute circuits from the classic to the Resource Manager deployment model](expressroute-howto-move-arm.md).</span></span>  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="2e1c8-219">Deprovisioning ed eliminazione di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="2e1c8-219">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="2e1c8-220">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-220">Note the following:</span></span>

* <span data-ttu-id="2e1c8-221">È necessario scollegare tutte le reti virtuali dal circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-221">You must unlink all virtual networks from the ExpressRoute circuit.</span></span> <span data-ttu-id="2e1c8-222">Se l'operazione non riesce, controllare se sono presenti reti virtuali collegate al circuito.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-222">If this operation fails, check to see if any virtual networks are linked to the circuit.</span></span>
* <span data-ttu-id="2e1c8-223">Se lo stato di provisioning del provider del servizio del circuito ExpressRoute è **Provisioning in corso** o **Provisioning eseguito**, è necessario collaborare con il provider di servizi per eseguire il deprovisioning del circuito sul lato del provider.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-223">If the ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider to deprovision the circuit on their side.</span></span> <span data-ttu-id="2e1c8-224">Le risorse continueranno a essere riservate e la fatturazione continuerà a essere applicata finché il provider di servizi non avrà completato il deprovisioning del circuito e inviato una notifica a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-224">We will continue to reserve resources and bill you until the service provider completes deprovisioning the circuit and notifies us.</span></span>
* <span data-ttu-id="2e1c8-225">Se il provider di servizi ha eseguito il deprovisioning del circuito, ovvero lo stato di provisioning del provider di servizi è impostato su **Senza provisioning**, è possibile eliminare il circuito.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-225">If the service provider has deprovisioned the circuit (the service provider provisioning state is set to **Not provisioned**) you can then delete the circuit.</span></span> <span data-ttu-id="2e1c8-226">Non verrà più applicata la fatturazione corrispondente.</span><span class="sxs-lookup"><span data-stu-id="2e1c8-226">This will stop billing for the circuit</span></span>

<span data-ttu-id="2e1c8-227">È possibile eliminare un circuito ExpressRoute eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-227">You can delete your ExpressRoute circuit by running the following command:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a><span data-ttu-id="2e1c8-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2e1c8-228">Next steps</span></span>

<span data-ttu-id="2e1c8-229">Dopo aver creato il circuito, verificare di eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2e1c8-229">After you create your circuit, make sure that you do the following:</span></span>

* [<span data-ttu-id="2e1c8-230">Creare e modificare il routing per un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="2e1c8-230">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="2e1c8-231">Collegare la rete virtuale al circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="2e1c8-231">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
