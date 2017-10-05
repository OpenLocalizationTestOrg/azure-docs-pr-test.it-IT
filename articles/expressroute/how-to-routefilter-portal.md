---
title: 'Configurare i filtri di route per il peering Microsoft Azure ExpressRoute: Portale | Microsoft Docs'
description: Questo articolo descrive come configurare i filtri di route per il peering Microsoft con il portale di Azure.
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
ms.openlocfilehash: f17bf3e475a33cfc617e8a026e9606b3792101f3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="ea94b-103">Configurare i filtri di route per il peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="ea94b-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="ea94b-104">I filtri di route rappresentano un modo per usare un subset di servizi supportati tramite il peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ea94b-104">Route filters are a way to consume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="ea94b-105">I passaggi descritti in questo articolo consentono di configurare e gestire i filtri di route per i circuiti ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ea94b-105">The steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="ea94b-106">I servizi Dynamics 365 e i servizi Office 365, come Exchange Online, SharePoint Online e Skype for Business sono accessibili tramite il peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ea94b-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through the Microsoft peering.</span></span> <span data-ttu-id="ea94b-107">Quando si configura il peering Microsoft in un circuito ExpressRoute, tutti i prefissi relativi a questi servizi vengono annunciati tramite le sessioni BGP stabilite.</span><span class="sxs-lookup"><span data-stu-id="ea94b-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related to these services are advertised through the BGP sessions that are established.</span></span> <span data-ttu-id="ea94b-108">A ogni prefisso viene associato un valore di community BGP per identificare il servizio offerto tramite il prefisso.</span><span class="sxs-lookup"><span data-stu-id="ea94b-108">A BGP community value is attached to every prefix to identify the service that is offered through the prefix.</span></span> <span data-ttu-id="ea94b-109">Per un elenco dei valori di community BGP e i servizi a cui sono associati, vedere [community BGP](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="ea94b-109">For a list of the BGP community values and the services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="ea94b-110">Se è necessaria la connettività a tutti i servizi, tramite BGP viene annunciato un numero elevato di prefissi.</span><span class="sxs-lookup"><span data-stu-id="ea94b-110">If you require connectivity to all services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="ea94b-111">Ciò aumenta notevolmente le dimensioni delle tabelle di route gestite dai router all'interno della rete.</span><span class="sxs-lookup"><span data-stu-id="ea94b-111">This significantly increases the size of the route tables maintained by routers within your network.</span></span> <span data-ttu-id="ea94b-112">Se si prevede di usare solo un subset dei servizi offerti tramite il peering Microsoft, è possibile ridurre le dimensioni delle tabelle di route in due modi.</span><span class="sxs-lookup"><span data-stu-id="ea94b-112">If you plan to consume only a subset of services offered through Microsoft peering, you can reduce the size of your route tables in two ways.</span></span> <span data-ttu-id="ea94b-113">È possibile:</span><span class="sxs-lookup"><span data-stu-id="ea94b-113">You can:</span></span>

- <span data-ttu-id="ea94b-114">Escludere i prefissi indesiderati applicando filtri di route alle community BGP.</span><span class="sxs-lookup"><span data-stu-id="ea94b-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="ea94b-115">Si tratta di una procedura di rete standard usata comunemente in molte reti.</span><span class="sxs-lookup"><span data-stu-id="ea94b-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="ea94b-116">Definire i filtri di route e applicarli al circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ea94b-116">Define route filters and apply them to your ExpressRoute circuit.</span></span> <span data-ttu-id="ea94b-117">Un filtro di route è una nuova risorsa che consente di selezionare l'elenco dei servizi che si prevede di usare tramite il peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ea94b-117">A route filter is a new resource that lets you select the list of services you plan to consume through Microsoft peering.</span></span> <span data-ttu-id="ea94b-118">I router ExpressRoute inviano solo l'elenco dei prefissi che appartengono ai servizi identificati nel filtro di route.</span><span class="sxs-lookup"><span data-stu-id="ea94b-118">ExpressRoute routers only send the list of prefixes that belong to the services identified in the route filter.</span></span>

### <span data-ttu-id="ea94b-119"><a name="about"></a>Informazioni sui filtri di route</span><span class="sxs-lookup"><span data-stu-id="ea94b-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="ea94b-120">Quando il peering Microsoft è configurato nel circuito ExpressRoute, i router perimetrali Microsoft stabiliscono una coppia di sessioni BGP con i router perimetrali (dell'utente o del provider di connettività).</span><span class="sxs-lookup"><span data-stu-id="ea94b-120">When Microsoft peering is configured on your ExpressRoute circuit, the Microsoft edge routers establish a pair of BGP sessions with the edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="ea94b-121">Non viene annunciata alcuna route per la rete.</span><span class="sxs-lookup"><span data-stu-id="ea94b-121">No routes are advertised to your network.</span></span> <span data-ttu-id="ea94b-122">Per abilitare gli annunci delle ruote per la rete, è necessario associare un filtro di route.</span><span class="sxs-lookup"><span data-stu-id="ea94b-122">To enable route advertisements to your network, you must associate a route filter.</span></span>

<span data-ttu-id="ea94b-123">Un filtro di route consente di identificare i servizi da usare tramite il peering Microsoft del circuito di ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ea94b-123">A route filter lets you identify services you want to consume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="ea94b-124">Si tratta fondamentalmente di un elenco di tutti i valori di community BGP consentiti.</span><span class="sxs-lookup"><span data-stu-id="ea94b-124">It is essentially a white list of all the BGP community values.</span></span> <span data-ttu-id="ea94b-125">Dopo aver definito una risorsa filtro di route e averla associata a un circuito ExpressRoute, tutti i prefissi corrispondenti ai valori di community BGP vengono annunciati per la rete.</span><span class="sxs-lookup"><span data-stu-id="ea94b-125">Once a route filter resource is defined and attached to an ExpressRoute circuit, all prefixes that map to the BGP community values are advertised to your network.</span></span>

<span data-ttu-id="ea94b-126">Per poter associare i filtri di route ai servizi Office 365, è necessario essere autorizzati all'uso dei servizi Office 365 tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ea94b-126">To be able to attach route filters with Office 365 services on them, you must have authorization to consume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="ea94b-127">Se non si è autorizzati a usare i servizi Office 365 tramite ExpressRoute, l'operazione di associazione dei filtri di route non riesce.</span><span class="sxs-lookup"><span data-stu-id="ea94b-127">If you are not authorized to consume Office 365 services through ExpressRoute, the operation to attach route filters fails.</span></span> <span data-ttu-id="ea94b-128">Per altre informazioni sul processo di autorizzazione, vedere [Azure ExpressRoute per Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="ea94b-128">For more information about the authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="ea94b-129">Per la connettività ai servizi Dynamics 365 NON sono richieste autorizzazioni preliminari.</span><span class="sxs-lookup"><span data-stu-id="ea94b-129">Connectivity to Dynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea94b-130">Per i circuiti ExpressRoute configurati prima del 1 agosto 2017, tutti i prefissi dei servizi verranno annunciati tramite il peering Microsoft, anche in mancanza di filtri di route definiti.</span><span class="sxs-lookup"><span data-stu-id="ea94b-130">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="ea94b-131">Per il peering Microsoft dei circuiti ExpressRoute configurati dopo il 1 agosto 2017 non verrà annunciato alcun prefisso fino a quando non viene associato un filtro di route al circuito.</span><span class="sxs-lookup"><span data-stu-id="ea94b-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span>
> 
> 

### <span data-ttu-id="ea94b-132"><a name="workflow"></a>Flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="ea94b-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="ea94b-133">Per riuscire a connettersi correttamente ai servizi tramite il peering Microsoft, è necessario completare i passaggi di configurazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="ea94b-133">To be able to successfully connect to services through Microsoft peering, you must complete the following configuration steps:</span></span>

- <span data-ttu-id="ea94b-134">È necessario avere un circuito ExpressRoute attivo, per cui è stato effettuato il provisioning del peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ea94b-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="ea94b-135">È possibile usare le istruzioni seguenti per eseguire queste attività:</span><span class="sxs-lookup"><span data-stu-id="ea94b-135">You can use the following instructions to accomplish these tasks:</span></span>
  - <span data-ttu-id="ea94b-136">[Creare un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e fare in modo che venga abilitato dal provider di connettività prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="ea94b-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="ea94b-137">È necessario che sia stato effettuato il provisioning del circuito ExpressRoute e che il circuito sia in stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="ea94b-137">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="ea94b-138">[Creare il peering Microsoft](expressroute-howto-routing-portal-resource-manager.md) se si gestisce direttamente la sessione BGP.</span><span class="sxs-lookup"><span data-stu-id="ea94b-138">[Create Microsoft peering](expressroute-howto-routing-portal-resource-manager.md) if you manage the BGP session directly.</span></span> <span data-ttu-id="ea94b-139">In caso contrario, richiedere al provider della connettività di effettuare il provisioning del peering Microsoft per il circuito.</span><span class="sxs-lookup"><span data-stu-id="ea94b-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="ea94b-140">È necessario creare e configurare un filtro di route.</span><span class="sxs-lookup"><span data-stu-id="ea94b-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="ea94b-141">Identificare i servizi da usare tramite il peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="ea94b-141">Identify the services you with to consume through Microsoft peering</span></span>
    - <span data-ttu-id="ea94b-142">Identificare l'elenco dei valori di community BGP associati ai servizi</span><span class="sxs-lookup"><span data-stu-id="ea94b-142">Identify the list of BGP community values associated with the services</span></span>
    - <span data-ttu-id="ea94b-143">Creare una regola per consentire l'elenco di prefissi corrispondenti ai valori di community BGP</span><span class="sxs-lookup"><span data-stu-id="ea94b-143">Create a rule to allow the prefix list matching the BGP community values</span></span>

-  <span data-ttu-id="ea94b-144">È necessario associare il filtro di route al circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ea94b-144">You must attach the route filter to the ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ea94b-145">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="ea94b-145">Before you begin</span></span>

<span data-ttu-id="ea94b-146">Prima di iniziare la configurazione, assicurarsi che siano soddisfatti i criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="ea94b-146">Before you begin configuration, make sure you meet the following criteria:</span></span>

 - <span data-ttu-id="ea94b-147">Prima di iniziare la configurazione, verificare i [prerequisiti](expressroute-prerequisites.md) e i [flussi di lavoro](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="ea94b-147">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="ea94b-148">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="ea94b-148">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="ea94b-149">Seguire le istruzioni per [creare un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e fare in modo che venga abilitato dal provider di connettività prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="ea94b-149">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="ea94b-150">È necessario che sia stato effettuato il provisioning del circuito ExpressRoute e che il circuito sia in stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="ea94b-150">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="ea94b-151">È necessario disporre di un peering Microsoft attivo.</span><span class="sxs-lookup"><span data-stu-id="ea94b-151">You must have an active Microsoft peering.</span></span> <span data-ttu-id="ea94b-152">Seguire le istruzioni per [creare e modificare la configurazione del peering](expressroute-howto-routing-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ea94b-152">Follow instructions at [Create and modifying peering configuration](expressroute-howto-routing-portal-resource-manager.md)</span></span>


## <span data-ttu-id="ea94b-153"><a name="prefixes"></a>Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="ea94b-153"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="ea94b-154">Ottenere un elenco di prefissi e di valori di community BGP</span><span class="sxs-lookup"><span data-stu-id="ea94b-154">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="ea94b-155">1. Ottenere un elenco dei valori di community BGP</span><span class="sxs-lookup"><span data-stu-id="ea94b-155">1. Get a list of BGP community values</span></span>

<span data-ttu-id="ea94b-156">I valori di community BGP associati ai servizi accessibili tramite il peering Microsoft sono disponibili nella pagina [Requisiti per il routing di ExpressRoute](expressroute-routing.md).</span><span class="sxs-lookup"><span data-stu-id="ea94b-156">BGP community values associated with services accessible through Microsoft peering is available in the [ExpressRoute routing requirements](expressroute-routing.md) page.</span></span>

### <a name="2-make-a-list-of-the-values-that-you-want-to-use"></a><span data-ttu-id="ea94b-157">2. Creare un elenco dei valori che si vuole usare</span><span class="sxs-lookup"><span data-stu-id="ea94b-157">2. Make a list of the values that you want to use</span></span>

<span data-ttu-id="ea94b-158">Creare un elenco dei valori di community BGP che si vuole usare nel filtro di route.</span><span class="sxs-lookup"><span data-stu-id="ea94b-158">Make a list of BGP community values you want to use in the route filter.</span></span> <span data-ttu-id="ea94b-159">Ad esempio, il valore di community BGP per i servizi Dynamics 365 è 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="ea94b-159">As an example, the BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="ea94b-160"><a name="filter"></a>Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="ea94b-160"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="ea94b-161">Creare un filtro di route e una regola di filtro</span><span class="sxs-lookup"><span data-stu-id="ea94b-161">Create a route filter and a filter rule</span></span>

<span data-ttu-id="ea94b-162">Un filtro di route può includere una sola regola di tipo 'Consenti'.</span><span class="sxs-lookup"><span data-stu-id="ea94b-162">A route filter can have only one rule, and the rule must be of type 'Allow'.</span></span> <span data-ttu-id="ea94b-163">A questa regola può essere associato un elenco di valori di community BGP.</span><span class="sxs-lookup"><span data-stu-id="ea94b-163">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="ea94b-164">1. Creare un filtro di route</span><span class="sxs-lookup"><span data-stu-id="ea94b-164">1. Create a route filter</span></span>
<span data-ttu-id="ea94b-165">È possibile creare un filtro di route selezionando l'opzione che consente di creare una nuova risorsa.</span><span class="sxs-lookup"><span data-stu-id="ea94b-165">You can create a route filter by selecting the option to create a new resource.</span></span> <span data-ttu-id="ea94b-166">Fare clic su **Nuovo** > **Rete** > **Filtro della route**, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="ea94b-166">Click **New** > **Networking** > **RouteFilter**, as shown in the following image:</span></span>

![Creare un filtro di route](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

<span data-ttu-id="ea94b-168">Il filtro di route deve essere inserito in un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ea94b-168">You must place the route filter in a resource group.</span></span> 

![Creare un filtro di route](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="ea94b-170">2. Creare una regola di filtro</span><span class="sxs-lookup"><span data-stu-id="ea94b-170">2. Create a filter rule</span></span>

<span data-ttu-id="ea94b-171">È possibile aggiungere e aggiornare regole selezionando la scheda di gestione delle regole per il filtro di route.</span><span class="sxs-lookup"><span data-stu-id="ea94b-171">You can add and update rules by selecting the manage rule tab for your route filter.</span></span>

![Creare un filtro di route](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


<span data-ttu-id="ea94b-173">Nell'elenco a discesa è possibile selezionare i servizi a cui si intende connettersi e, al termine, salvare la regola.</span><span class="sxs-lookup"><span data-stu-id="ea94b-173">You can select the services you want to connect to from the drop down list and save the rule when done.</span></span>

![Creare un filtro di route](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <span data-ttu-id="ea94b-175"><a name="attach"></a>Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="ea94b-175"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="ea94b-176">Associare il filtro di route a un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="ea94b-176">Attach the route filter to an ExpressRoute circuit</span></span>

<span data-ttu-id="ea94b-177">È possibile associare il filtro di route a un circuito facendo clic sul pulsante "Aggiungi circuito" e selezionando il circuito ExpressRoute nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="ea94b-177">You can attach the route filter to a circuit by selecting the "add Circuit" button and selecting the ExpressRoute circuit from the drop down list.</span></span>

![Creare un filtro di route](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <span data-ttu-id="ea94b-179"><a name="getproperties"></a>Per ottenere le proprietà di un filtro di route</span><span class="sxs-lookup"><span data-stu-id="ea94b-179"><a name="getproperties"></a>To get the properties of a route filter</span></span>

<span data-ttu-id="ea94b-180">È possibile visualizzare le proprietà di un filtro di route quando si apre la risorsa nel portale.</span><span class="sxs-lookup"><span data-stu-id="ea94b-180">You can view properties of a route filter when you open the resource in the portal.</span></span>

![Creare un filtro di route](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <span data-ttu-id="ea94b-182"><a name="updateproperties"></a>Per aggiornare le proprietà di un filtro di route</span><span class="sxs-lookup"><span data-stu-id="ea94b-182"><a name="updateproperties"></a>To update the properties of a route filter</span></span>

<span data-ttu-id="ea94b-183">È possibile aggiornare l'elenco dei valori di community BGP associato a un circuito facendo clic sul pulsante "Gestisci regola".</span><span class="sxs-lookup"><span data-stu-id="ea94b-183">You can update the list of BGP community values attached to a circuit by selecting the "Manage rule" button.</span></span>


![Creare un filtro di route](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Creare un filtro di route](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <span data-ttu-id="ea94b-186"><a name="detach"></a>Per rimuovere l'associazione di un filtro di route da un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="ea94b-186"><a name="detach"></a>To detach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="ea94b-187">Per disconnettere un circuito dal filtro di route, fare clic con il pulsante destro del mouse sul circuito e fare clic su "annulla associazione".</span><span class="sxs-lookup"><span data-stu-id="ea94b-187">To detach a circuit from the route filter, right click on the circuit and click on "disassociate".</span></span>

![Creare un filtro di route](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <span data-ttu-id="ea94b-189"><a name="delete"></a>Per eliminare un filtro di route</span><span class="sxs-lookup"><span data-stu-id="ea94b-189"><a name="delete"></a>To delete a route filter</span></span>

<span data-ttu-id="ea94b-190">È possibile eliminare un filtro di route selezionando il pulsante di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="ea94b-190">You can delete a route filter by selecting the delete button.</span></span> 

![Creare un filtro di route](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a><span data-ttu-id="ea94b-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ea94b-192">Next steps</span></span>

<span data-ttu-id="ea94b-193">Per altre informazioni su ExpressRoute, vedere le [Domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="ea94b-193">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>