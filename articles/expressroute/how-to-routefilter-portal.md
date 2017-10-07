---
title: 'Configurare i filtri di route per il peering Microsoft Azure ExpressRoute: Portale | Microsoft Docs'
description: In questo articolo viene descritto come tooconfigure i filtri di route per l'utilizzo di Peering Microsoft hello portale di Azure
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="77ca5-103">Configurare i filtri di route per il peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="77ca5-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="77ca5-104">I filtri di route sono tooconsume un modo un sottoinsieme di servizi supportati tramite il peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="77ca5-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="77ca5-105">Hello passaggi in questo articolo consentono configurare e gestire i filtri di route per i circuiti ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="77ca5-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="77ca5-106">Dynamics 365 servizi e i servizi di Office 365, ad esempio Exchange Online, SharePoint Online e Skype for Business, sono accessibili tramite il peering Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="77ca5-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="77ca5-107">Quando Microsoft peering è configurato in un circuito ExpressRoute, tutti i servizi correlati toothese prefissi sono annunciati tramite sessioni BGP hello stabilite.</span><span class="sxs-lookup"><span data-stu-id="77ca5-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="77ca5-108">Un valore di community BGP è collegato tooevery prefisso tooidentify hello servizio verrà offerti attraverso prefisso hello.</span><span class="sxs-lookup"><span data-stu-id="77ca5-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="77ca5-109">Per un elenco di valori di community hello BGP e i servizi di hello viene eseguito il mapping, vedere [community BGP](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="77ca5-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="77ca5-110">Se si richiedono servizi di integrazione applicativa tooall, un numero elevato di prefissi venga pubblicato tramite BGP.</span><span class="sxs-lookup"><span data-stu-id="77ca5-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="77ca5-111">Ciò aumenta significativamente il dimensioni hello hello di tabelle di route gestita da router all'interno della rete.</span><span class="sxs-lookup"><span data-stu-id="77ca5-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="77ca5-112">Se si prevede solo un sottoinsieme di servizi offerti tramite il peering Microsoft tooconsume, è possibile ridurre le dimensioni di hello delle tabelle di route in due modi.</span><span class="sxs-lookup"><span data-stu-id="77ca5-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="77ca5-113">È possibile:</span><span class="sxs-lookup"><span data-stu-id="77ca5-113">You can:</span></span>

- <span data-ttu-id="77ca5-114">Escludere i prefissi indesiderati applicando filtri di route alle community BGP.</span><span class="sxs-lookup"><span data-stu-id="77ca5-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="77ca5-115">Si tratta di una procedura di rete standard usata comunemente in molte reti.</span><span class="sxs-lookup"><span data-stu-id="77ca5-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="77ca5-116">Definire i filtri di route e applicarli circuito ExpressRoute tooyour.</span><span class="sxs-lookup"><span data-stu-id="77ca5-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="77ca5-117">Un filtro di route è una nuova risorsa, che consente di selezionare l'elenco di hello dei servizi è pianificare tooconsume tramite il peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="77ca5-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="77ca5-118">Router di ExpressRoute inviare solo elenco hello di prefissi che appartengono a servizi toohello individuati nel filtro di route hello.</span><span class="sxs-lookup"><span data-stu-id="77ca5-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="77ca5-119"><a name="about"></a>Informazioni sui filtri di route</span><span class="sxs-lookup"><span data-stu-id="77ca5-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="77ca5-120">Quando Microsoft peering è configurato il circuito ExpressRoute, router perimetrali dei Microsoft hello stabilisce una coppia di sessioni BGP con il router perimetrali hello (il proprio o il provider di connettività).</span><span class="sxs-lookup"><span data-stu-id="77ca5-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="77ca5-121">Nessuna route sono rete tooyour annunciato.</span><span class="sxs-lookup"><span data-stu-id="77ca5-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="77ca5-122">rete di tooyour gli annunci di route tooenable, è necessario associare un filtro di route.</span><span class="sxs-lookup"><span data-stu-id="77ca5-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="77ca5-123">Un filtro di route consente di identificare i servizi desiderati tooconsume tramite il peering Microsoft del circuito di ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="77ca5-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="77ca5-124">È essenzialmente un elenco vuoto di tutti i valori della community di hello BGP.</span><span class="sxs-lookup"><span data-stu-id="77ca5-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="77ca5-125">Una volta una risorsa di filtro di route è definita e collegata tooan circuito ExpressRoute, tutti i prefissi che mappa i valori della community BGP toohello sono rete tooyour annunciato.</span><span class="sxs-lookup"><span data-stu-id="77ca5-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="77ca5-126">filtri di route in grado di tooattach toobe con servizi di Office 365 su di essi, è necessario disporre di servizi di Office 365 tooconsume autorizzazione tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="77ca5-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="77ca5-127">Se non si è autorizzati tooconsume Office 365 services tramite ExpressRoute, filtri di route tooattach hello operazione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="77ca5-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="77ca5-128">Per ulteriori informazioni sul processo di autorizzazione hello, vedere [Azure ExpressRoute per Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="77ca5-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="77ca5-129">Servizi di integrazione applicativa tooDynamics 365 non richiede alcuna autorizzazione precedente.</span><span class="sxs-lookup"><span data-stu-id="77ca5-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77ca5-130">Microsoft peering di circuiti ExpressRoute che sono stati configurati precedente tooAugust 1, 2017 disporrà di tutti i prefissi di servizio pubblicati tramite Microsoft peering, anche se non sono definiti i filtri di route.</span><span class="sxs-lookup"><span data-stu-id="77ca5-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="77ca5-131">Microsoft peering di circuiti ExpressRoute configurati o dopo il 1 agosto 2017 non avrà alcun prefisso annunciato fino a quando non è associato un filtro di route toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="77ca5-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="77ca5-132"><a name="workflow"></a>Flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="77ca5-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="77ca5-133">toobe toosuccessfully in grado di connettersi tooservices tramite il peering Microsoft, è necessario completare hello seguendo i passaggi di configurazione:</span><span class="sxs-lookup"><span data-stu-id="77ca5-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="77ca5-134">È necessario avere un circuito ExpressRoute attivo, per cui è stato effettuato il provisioning del peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="77ca5-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="77ca5-135">È possibile utilizzare hello seguendo le istruzioni tooaccomplish queste attività:</span><span class="sxs-lookup"><span data-stu-id="77ca5-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="77ca5-136">[Creare un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e circuito hello abilitato dal provider di connettività prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="77ca5-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="77ca5-137">Hello circuito ExpressRoute deve essere in uno stato di provisioning e abilitato.</span><span class="sxs-lookup"><span data-stu-id="77ca5-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="77ca5-138">[Creare il peering Microsoft](expressroute-howto-routing-portal-resource-manager.md) se si Gestione sessione BGP di hello direttamente.</span><span class="sxs-lookup"><span data-stu-id="77ca5-138">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="77ca5-139">In caso contrario, richiedere al provider della connettività di effettuare il provisioning del peering Microsoft per il circuito.</span><span class="sxs-lookup"><span data-stu-id="77ca5-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="77ca5-140">È necessario creare e configurare un filtro di route.</span><span class="sxs-lookup"><span data-stu-id="77ca5-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="77ca5-141">Identificare hello è servizi con tooconsume tramite il peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="77ca5-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="77ca5-142">Identificare hello elenco di valori di community BGP associati ai servizi hello</span><span class="sxs-lookup"><span data-stu-id="77ca5-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="77ca5-143">Creare un regola tooallow hello prefisso elenco corrispondente hello valori community BGP</span><span class="sxs-lookup"><span data-stu-id="77ca5-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="77ca5-144">È necessario collegare il circuito ExpressRoute toohello di hello route filtro.</span><span class="sxs-lookup"><span data-stu-id="77ca5-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="77ca5-145">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="77ca5-145">Before you begin</span></span>

<span data-ttu-id="77ca5-146">Prima di iniziare la configurazione, assicurarsi che siano soddisfatti hello seguenti criteri:</span><span class="sxs-lookup"><span data-stu-id="77ca5-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="77ca5-147">Hello revisione [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="77ca5-147">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="77ca5-148">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="77ca5-148">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="77ca5-149">Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e circuito hello abilitato dal provider di connettività prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="77ca5-149">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="77ca5-150">Hello circuito ExpressRoute deve essere in uno stato di provisioning e abilitato.</span><span class="sxs-lookup"><span data-stu-id="77ca5-150">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="77ca5-151">È necessario disporre di un peering Microsoft attivo.</span><span class="sxs-lookup"><span data-stu-id="77ca5-151">You must have an active Microsoft peering.</span></span> <span data-ttu-id="77ca5-152">Seguire le istruzioni per [creare e modificare la configurazione del peering](expressroute-howto-routing-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="77ca5-152">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span></span>


## <span data-ttu-id="77ca5-153"><a name="prefixes"></a>Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="77ca5-153"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="77ca5-154">Ottenere un elenco di prefissi e di valori di community BGP</span><span class="sxs-lookup"><span data-stu-id="77ca5-154">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="77ca5-155">1. Ottenere un elenco dei valori di community BGP</span><span class="sxs-lookup"><span data-stu-id="77ca5-155">1. Get a list of BGP community values</span></span>

<span data-ttu-id="77ca5-156">I valori della community BGP associati a servizi accessibili tramite il peering Microsoft è disponibile in hello [requisiti di routing ExpressRoute](expressroute-routing.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="77ca5-156">BGP community values associated with services accessible through Microsoft peering is available in hello [ExpressRoute routing requirements](expressroute-routing.md) page.</span></span>

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="77ca5-157">2. Creare un elenco di valori hello che si desidera toouse</span><span class="sxs-lookup"><span data-stu-id="77ca5-157">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="77ca5-158">Creare un elenco dei valori di community BGP da toouse nel filtro di route hello.</span><span class="sxs-lookup"><span data-stu-id="77ca5-158">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="77ca5-159">Ad esempio, il valore di community BGP per servizi di Dynamics 365 hello è 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="77ca5-159">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="77ca5-160"><a name="filter"></a>Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="77ca5-160"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="77ca5-161">Creare un filtro di route e una regola di filtro</span><span class="sxs-lookup"><span data-stu-id="77ca5-161">Create a route filter and a filter rule</span></span>

<span data-ttu-id="77ca5-162">Un filtro di route può avere solo una regola e hello regola deve essere di tipo 'Consenti'.</span><span class="sxs-lookup"><span data-stu-id="77ca5-162">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="77ca5-163">A questa regola può essere associato un elenco di valori di community BGP.</span><span class="sxs-lookup"><span data-stu-id="77ca5-163">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="77ca5-164">1. Creare un filtro di route</span><span class="sxs-lookup"><span data-stu-id="77ca5-164">1. Create a route filter</span></span>
<span data-ttu-id="77ca5-165">È possibile creare un filtro di route selezionando hello opzione toocreate una nuova risorsa.</span><span class="sxs-lookup"><span data-stu-id="77ca5-165">You can create a route filter by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="77ca5-166">Fare clic su **New** > **rete** > **RouteFilter**, come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="77ca5-166">Click **New** > **Networking** > **RouteFilter**, as shown in hello following image:</span></span>

![Creare un filtro di route](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

<span data-ttu-id="77ca5-168">È necessario inserire il filtro di route hello in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="77ca5-168">You must place hello route filter in a resource group.</span></span> 

![Creare un filtro di route](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="77ca5-170">2. Creare una regola di filtro</span><span class="sxs-lookup"><span data-stu-id="77ca5-170">2. Create a filter rule</span></span>

<span data-ttu-id="77ca5-171">È possibile aggiungere e gestire di regole di aggiornamento selezionando hello scheda regola per il filtro di route.</span><span class="sxs-lookup"><span data-stu-id="77ca5-171">You can add and update rules by selecting hello manage rule tab for your route filter.</span></span>

![Creare un filtro di route](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


<span data-ttu-id="77ca5-173">È possibile selezionare hello servizi desiderati tooconnect toofrom hello nell'elenco a discesa e salvare la regola di hello al termine.</span><span class="sxs-lookup"><span data-stu-id="77ca5-173">You can select hello services you want tooconnect toofrom hello drop down list and save hello rule when done.</span></span>

![Creare un filtro di route](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <span data-ttu-id="77ca5-175"><a name="attach"></a>Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="77ca5-175"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="77ca5-176">Collegare il circuito ExpressRoute hello route filtro tooan</span><span class="sxs-lookup"><span data-stu-id="77ca5-176">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="77ca5-177">È possibile collegare tooa circuito di hello route filtro selezionando pulsante "Aggiungi circuito" hello e selezionando il circuito ExpressRoute hello hello nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="77ca5-177">You can attach hello route filter tooa circuit by selecting hello "add Circuit" button and selecting hello ExpressRoute circuit from hello drop down list.</span></span>

![Creare un filtro di route](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <span data-ttu-id="77ca5-179"><a name="getproperties"></a>proprietà hello tooget di un filtro di route</span><span class="sxs-lookup"><span data-stu-id="77ca5-179"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="77ca5-180">Quando si apre risorse hello nel portale di hello, è possibile visualizzare le proprietà di un filtro di route.</span><span class="sxs-lookup"><span data-stu-id="77ca5-180">You can view properties of a route filter when you open hello resource in hello portal.</span></span>

![Creare un filtro di route](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <span data-ttu-id="77ca5-182"><a name="updateproperties"></a>proprietà hello tooupdate di un filtro di route</span><span class="sxs-lookup"><span data-stu-id="77ca5-182"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="77ca5-183">È possibile aggiornare l'elenco di hello del circuito BGP community valori collegati tooa selezionando pulsante hello "Gestisci"regola.</span><span class="sxs-lookup"><span data-stu-id="77ca5-183">You can update hello list of BGP community values attached tooa circuit by selecting hello "Manage rule" button.</span></span>


![Creare un filtro di route](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Creare un filtro di route](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <span data-ttu-id="77ca5-186"><a name="detach"></a>toodetach un filtro di route da un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="77ca5-186"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="77ca5-187">toodetach un circuito dal filtro di route hello, fare clic con il pulsante destro sul circuito hello e fare clic su "dissociare".</span><span class="sxs-lookup"><span data-stu-id="77ca5-187">toodetach a circuit from hello route filter, right click on hello circuit and click on "disassociate".</span></span>

![Creare un filtro di route](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <span data-ttu-id="77ca5-189"><a name="delete"></a>toodelete un filtro di route</span><span class="sxs-lookup"><span data-stu-id="77ca5-189"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="77ca5-190">È possibile eliminare un filtro di route selezionando pulsante Elimina hello.</span><span class="sxs-lookup"><span data-stu-id="77ca5-190">You can delete a route filter by selecting hello delete button.</span></span> 

![Creare un filtro di route](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a><span data-ttu-id="77ca5-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="77ca5-192">Next steps</span></span>

<span data-ttu-id="77ca5-193">Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="77ca5-193">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
