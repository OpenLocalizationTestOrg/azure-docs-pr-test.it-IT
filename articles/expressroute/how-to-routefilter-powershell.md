---
title: 'Configurare i filtri di route per il peering Microsoft Azure ExpressRoute: PowerShell | Microsoft Docs'
description: Questo articolo descrive come configurare i filtri di route per il peering Microsoft con PowerShell.
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
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: de3550c20439fa809869d98b8a57ea3be9c03e7c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="52e67-103">Configurare i filtri di route per il peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="52e67-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="52e67-104">I filtri di route rappresentano un modo per usare un subset di servizi supportati tramite il peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="52e67-104">Route filters are a way to consume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="52e67-105">I passaggi descritti in questo articolo consentono di configurare e gestire i filtri di route per i circuiti ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="52e67-105">The steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="52e67-106">I servizi Dynamics 365 e i servizi Office 365, come Exchange Online, SharePoint Online e Skype for Business sono accessibili tramite il peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="52e67-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through the Microsoft peering.</span></span> <span data-ttu-id="52e67-107">Quando si configura il peering Microsoft in un circuito ExpressRoute, tutti i prefissi relativi a questi servizi vengono annunciati tramite le sessioni BGP stabilite.</span><span class="sxs-lookup"><span data-stu-id="52e67-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related to these services are advertised through the BGP sessions that are established.</span></span> <span data-ttu-id="52e67-108">A ogni prefisso viene associato un valore di community BGP per identificare il servizio offerto tramite il prefisso.</span><span class="sxs-lookup"><span data-stu-id="52e67-108">A BGP community value is attached to every prefix to identify the service that is offered through the prefix.</span></span> <span data-ttu-id="52e67-109">Per un elenco dei valori di community BGP e i servizi a cui sono associati, vedere [community BGP](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="52e67-109">For a list of the BGP community values and the services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="52e67-110">Se è necessaria la connettività a tutti i servizi, tramite BGP viene annunciato un numero elevato di prefissi.</span><span class="sxs-lookup"><span data-stu-id="52e67-110">If you require connectivity to all services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="52e67-111">Ciò aumenta notevolmente le dimensioni delle tabelle di route gestite dai router all'interno della rete.</span><span class="sxs-lookup"><span data-stu-id="52e67-111">This significantly increases the size of the route tables maintained by routers within your network.</span></span> <span data-ttu-id="52e67-112">Se si prevede di usare solo un subset dei servizi offerti tramite il peering Microsoft, è possibile ridurre le dimensioni delle tabelle di route in due modi.</span><span class="sxs-lookup"><span data-stu-id="52e67-112">If you plan to consume only a subset of services offered through Microsoft peering, you can reduce the size of your route tables in two ways.</span></span> <span data-ttu-id="52e67-113">È possibile:</span><span class="sxs-lookup"><span data-stu-id="52e67-113">You can:</span></span>

- <span data-ttu-id="52e67-114">Escludere i prefissi indesiderati applicando filtri di route alle community BGP.</span><span class="sxs-lookup"><span data-stu-id="52e67-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="52e67-115">Si tratta di una procedura di rete standard usata comunemente in molte reti.</span><span class="sxs-lookup"><span data-stu-id="52e67-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="52e67-116">Definire i filtri di route e applicarli al circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="52e67-116">Define route filters and apply them to your ExpressRoute circuit.</span></span> <span data-ttu-id="52e67-117">Un filtro di route è una nuova risorsa che consente di selezionare l'elenco dei servizi che si prevede di usare tramite il peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="52e67-117">A route filter is a new resource that lets you select the list of services you plan to consume through Microsoft peering.</span></span> <span data-ttu-id="52e67-118">I router ExpressRoute inviano solo l'elenco dei prefissi che appartengono ai servizi identificati nel filtro di route.</span><span class="sxs-lookup"><span data-stu-id="52e67-118">ExpressRoute routers only send the list of prefixes that belong to the services identified in the route filter.</span></span>

### <span data-ttu-id="52e67-119"><a name="about"></a>Informazioni sui filtri di route</span><span class="sxs-lookup"><span data-stu-id="52e67-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="52e67-120">Quando il peering Microsoft è configurato nel circuito ExpressRoute, i router perimetrali Microsoft stabiliscono una coppia di sessioni BGP con i router perimetrali (dell'utente o del provider di connettività).</span><span class="sxs-lookup"><span data-stu-id="52e67-120">When Microsoft peering is configured on your ExpressRoute circuit, the Microsoft edge routers establish a pair of BGP sessions with the edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="52e67-121">Non viene annunciata alcuna route per la rete.</span><span class="sxs-lookup"><span data-stu-id="52e67-121">No routes are advertised to your network.</span></span> <span data-ttu-id="52e67-122">Per abilitare gli annunci delle ruote per la rete, è necessario associare un filtro di route.</span><span class="sxs-lookup"><span data-stu-id="52e67-122">To enable route advertisements to your network, you must associate a route filter.</span></span>

<span data-ttu-id="52e67-123">Un filtro di route consente di identificare i servizi da usare tramite il peering Microsoft del circuito di ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="52e67-123">A route filter lets you identify services you want to consume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="52e67-124">Si tratta fondamentalmente di un elenco di tutti i valori di community BGP consentiti.</span><span class="sxs-lookup"><span data-stu-id="52e67-124">It is essentially a white list of all the BGP community values.</span></span> <span data-ttu-id="52e67-125">Dopo aver definito una risorsa filtro di route e averla associata a un circuito ExpressRoute, tutti i prefissi corrispondenti ai valori di community BGP vengono annunciati per la rete.</span><span class="sxs-lookup"><span data-stu-id="52e67-125">Once a route filter resource is defined and attached to an ExpressRoute circuit, all prefixes that map to the BGP community values are advertised to your network.</span></span>

<span data-ttu-id="52e67-126">Per poter associare i filtri di route ai servizi Office 365, è necessario essere autorizzati all'uso dei servizi Office 365 tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="52e67-126">To be able to attach route filters with Office 365 services on them, you must have authorization to consume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="52e67-127">Se non si è autorizzati a usare i servizi Office 365 tramite ExpressRoute, l'operazione di associazione dei filtri di route non riesce.</span><span class="sxs-lookup"><span data-stu-id="52e67-127">If you are not authorized to consume Office 365 services through ExpressRoute, the operation to attach route filters fails.</span></span> <span data-ttu-id="52e67-128">Per altre informazioni sul processo di autorizzazione, vedere [Azure ExpressRoute per Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="52e67-128">For more information about the authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="52e67-129">Per la connettività ai servizi Dynamics 365 NON sono richieste autorizzazioni preliminari.</span><span class="sxs-lookup"><span data-stu-id="52e67-129">Connectivity to Dynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52e67-130">Per i circuiti ExpressRoute configurati prima del 1 agosto 2017, tutti i prefissi dei servizi verranno annunciati tramite il peering Microsoft, anche in mancanza di filtri di route definiti.</span><span class="sxs-lookup"><span data-stu-id="52e67-130">Microsoft peering of ExpressRoute circuits that were configured prior to August 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="52e67-131">Per il peering Microsoft dei circuiti ExpressRoute configurati dopo il 1 agosto 2017 non verrà annunciato alcun prefisso fino a quando non viene associato un filtro di route al circuito.</span><span class="sxs-lookup"><span data-stu-id="52e67-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached to the circuit.</span></span>
> 
> 

### <span data-ttu-id="52e67-132"><a name="workflow"></a>Flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="52e67-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="52e67-133">Per riuscire a connettersi correttamente ai servizi tramite il peering Microsoft, è necessario completare i passaggi di configurazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="52e67-133">To be able to successfully connect to services through Microsoft peering, you must complete the following configuration steps:</span></span>

- <span data-ttu-id="52e67-134">È necessario avere un circuito ExpressRoute attivo, per cui è stato effettuato il provisioning del peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="52e67-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="52e67-135">È possibile usare le istruzioni seguenti per eseguire queste attività:</span><span class="sxs-lookup"><span data-stu-id="52e67-135">You can use the following instructions to accomplish these tasks:</span></span>
  - <span data-ttu-id="52e67-136">[Creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md) e fare in modo che venga abilitato dal provider di connettività prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="52e67-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="52e67-137">È necessario che sia stato effettuato il provisioning del circuito ExpressRoute e che il circuito sia in stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="52e67-137">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="52e67-138">[Creare il peering Microsoft](expressroute-circuit-peerings.md) se si gestisce direttamente la sessione BGP.</span><span class="sxs-lookup"><span data-stu-id="52e67-138">[Create Microsoft peering](expressroute-circuit-peerings.md) if you manage the BGP session directly.</span></span> <span data-ttu-id="52e67-139">In caso contrario, richiedere al provider della connettività di effettuare il provisioning del peering Microsoft per il circuito.</span><span class="sxs-lookup"><span data-stu-id="52e67-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="52e67-140">È necessario creare e configurare un filtro di route.</span><span class="sxs-lookup"><span data-stu-id="52e67-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="52e67-141">Identificare i servizi da usare tramite il peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="52e67-141">Identify the services you with to consume through Microsoft peering</span></span>
    - <span data-ttu-id="52e67-142">Identificare l'elenco dei valori di community BGP associati ai servizi</span><span class="sxs-lookup"><span data-stu-id="52e67-142">Identify the list of BGP community values associated with the services</span></span>
    - <span data-ttu-id="52e67-143">Creare una regola per consentire l'elenco di prefissi corrispondenti ai valori di community BGP</span><span class="sxs-lookup"><span data-stu-id="52e67-143">Create a rule to allow the prefix list matching the BGP community values</span></span>

-  <span data-ttu-id="52e67-144">È necessario associare il filtro di route al circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="52e67-144">You must attach the route filter to the ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="52e67-145">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="52e67-145">Before you begin</span></span>

<span data-ttu-id="52e67-146">Prima di iniziare la configurazione, assicurarsi che siano soddisfatti i criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="52e67-146">Before you begin configuration, make sure you meet the following criteria:</span></span>

 - <span data-ttu-id="52e67-147">Installare la versione più recente dei cmdlet di PowerShell per Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="52e67-147">Install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="52e67-148">Per altre informazioni, vedere [Installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="52e67-148">For more information, see [Install and configure Azure PowerShelll](/powershell/azure/install-azurerm-ps).</span></span>

  > [!NOTE]
  > <span data-ttu-id="52e67-149">Scaricare la versione più recente da PowerShell Gallery, invece di usare il programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="52e67-149">Download the latest version from the PowerShell Gallery, rather than using the Installer.</span></span> <span data-ttu-id="52e67-150">Il programma di installazione non supporta attualmente i cmdlet richiesti.</span><span class="sxs-lookup"><span data-stu-id="52e67-150">The Installer currently does not support the required cmdlets.</span></span>
  > 

 - <span data-ttu-id="52e67-151">Prima di iniziare la configurazione, verificare i [prerequisiti](expressroute-prerequisites.md) e i [flussi di lavoro](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="52e67-151">Review the [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="52e67-152">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="52e67-152">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="52e67-153">Seguire le istruzioni per [creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md) e fare in modo che venga abilitato dal provider di connettività prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="52e67-153">Follow the instructions to [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="52e67-154">È necessario che sia stato effettuato il provisioning del circuito ExpressRoute e che il circuito sia in stato abilitato.</span><span class="sxs-lookup"><span data-stu-id="52e67-154">The ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="52e67-155">È necessario disporre di un peering Microsoft attivo.</span><span class="sxs-lookup"><span data-stu-id="52e67-155">You must have an active Microsoft peering.</span></span> <span data-ttu-id="52e67-156">Seguire le istruzioni per [creare e modificare la configurazione del peering](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="52e67-156">Follow instructions at [Create and modifying peering configuration](expressroute-circuit-peerings.md)</span></span>

### <a name="log-in-to-your-azure-account"></a><span data-ttu-id="52e67-157">Accedere all'account Azure</span><span class="sxs-lookup"><span data-stu-id="52e67-157">Log in to your Azure account</span></span>

<span data-ttu-id="52e67-158">Prima di iniziare questa configurazione, è necessario accedere all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="52e67-158">Before beginning this configuration, you must log in to your Azure account.</span></span> <span data-ttu-id="52e67-159">Il cmdlet richiede le credenziali di accesso per l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="52e67-159">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="52e67-160">Dopo l'accesso, vengono scaricate le impostazioni dell'account in modo che siano disponibili per Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52e67-160">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span>

<span data-ttu-id="52e67-161">Aprire la console di PowerShell con privilegi elevati e connettersi al proprio account.</span><span class="sxs-lookup"><span data-stu-id="52e67-161">Open your PowerShell console with elevated privileges, and connect to your account.</span></span> <span data-ttu-id="52e67-162">Per eseguire la connessione, usare gli esempi che seguono:</span><span class="sxs-lookup"><span data-stu-id="52e67-162">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="52e67-163">Se si hanno più sottoscrizioni di Azure, selezionare le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="52e67-163">If you have multiple Azure subscriptions, check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="52e67-164">Specificare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="52e67-164">Specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="52e67-165"><a name="prefixes"></a>Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="52e67-165"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="52e67-166">Ottenere un elenco di prefissi e di valori di community BGP</span><span class="sxs-lookup"><span data-stu-id="52e67-166">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="52e67-167">1. Ottenere un elenco dei valori di community BGP</span><span class="sxs-lookup"><span data-stu-id="52e67-167">1. Get a list of BGP community values</span></span>

<span data-ttu-id="52e67-168">Usare il cmdlet seguente per ottenere l'elenco dei valori di community BGP associati ai servizi accessibili tramite il peering Microsoft e l'elenco dei prefissi associati:</span><span class="sxs-lookup"><span data-stu-id="52e67-168">Use the following cmdlet to get the list of BGP community values associated with services accessible through Microsoft peering, and the list of prefixes associated with them:</span></span>

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-the-values-that-you-want-to-use"></a><span data-ttu-id="52e67-169">2. Creare un elenco dei valori che si vuole usare</span><span class="sxs-lookup"><span data-stu-id="52e67-169">2. Make a list of the values that you want to use</span></span>

<span data-ttu-id="52e67-170">Creare un elenco dei valori di community BGP che si vuole usare nel filtro di route.</span><span class="sxs-lookup"><span data-stu-id="52e67-170">Make a list of BGP community values you want to use in the route filter.</span></span> <span data-ttu-id="52e67-171">Ad esempio, il valore di community BGP per i servizi Dynamics 365 è 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="52e67-171">As an example, the BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="52e67-172"><a name="filter"></a>Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="52e67-172"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="52e67-173">Creare un filtro di route e una regola di filtro</span><span class="sxs-lookup"><span data-stu-id="52e67-173">Create a route filter and a filter rule</span></span>

<span data-ttu-id="52e67-174">Un filtro di route può includere una sola regola di tipo 'Consenti'.</span><span class="sxs-lookup"><span data-stu-id="52e67-174">A route filter can have only one rule, and the rule must be of type 'Allow'.</span></span> <span data-ttu-id="52e67-175">A questa regola può essere associato un elenco di valori di community BGP.</span><span class="sxs-lookup"><span data-stu-id="52e67-175">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="52e67-176">1. Creare un filtro di route</span><span class="sxs-lookup"><span data-stu-id="52e67-176">1. Create a route filter</span></span>

<span data-ttu-id="52e67-177">Creare prima di tutto il filtro di route.</span><span class="sxs-lookup"><span data-stu-id="52e67-177">First, create the route filter.</span></span> <span data-ttu-id="52e67-178">Il comando 'New-AzureRmRouteFilter' crea solo una risorsa filtro di route.</span><span class="sxs-lookup"><span data-stu-id="52e67-178">The command 'New-AzureRmRouteFilter' only creates a route filter resource.</span></span> <span data-ttu-id="52e67-179">Dopo aver creato la risorsa, è necessario creare una regola e associarla all'oggetto filtro di route.</span><span class="sxs-lookup"><span data-stu-id="52e67-179">After you create the resource, you must then create a rule and attach it to the route filter object.</span></span> <span data-ttu-id="52e67-180">Eseguire il comando seguente per creare una risorsa filtro di route:</span><span class="sxs-lookup"><span data-stu-id="52e67-180">Run the following command to create a route filter resource:</span></span>

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="52e67-181">2. Creare una regola di filtro</span><span class="sxs-lookup"><span data-stu-id="52e67-181">2. Create a filter rule</span></span>

<span data-ttu-id="52e67-182">È possibile specificare un set di community BGP come elenco delimitato da virgole, come illustrato nell'esempio.</span><span class="sxs-lookup"><span data-stu-id="52e67-182">You can specify a set of BGP communities as a comma-separated list, as shown in the example.</span></span> <span data-ttu-id="52e67-183">Eseguire il comando seguente per creare una nuova regola:</span><span class="sxs-lookup"><span data-stu-id="52e67-183">Run the following command to create a new rule:</span></span>
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-the-rule-to-the-route-filter"></a><span data-ttu-id="52e67-184">3. Aggiungere la regola al filtro di route</span><span class="sxs-lookup"><span data-stu-id="52e67-184">3. Add the rule to the route filter</span></span>

<span data-ttu-id="52e67-185">Eseguire il comando seguente per aggiungere la regola di filtro al filtro di route:</span><span class="sxs-lookup"><span data-stu-id="52e67-185">Run the following command to add the filter rule to the route filter:</span></span>
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="52e67-186"><a name="attach"></a>Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="52e67-186"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="52e67-187">Associare il filtro di route a un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="52e67-187">Attach the route filter to an ExpressRoute circuit</span></span>

<span data-ttu-id="52e67-188">Se si usano solo peer Microsoft, eseguire questo comando per associare il filtro route al circuito ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="52e67-188">Run the following command to attach the route filter to the ExpressRoute circuit, assuming you have only Microsoft peering:</span></span>

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="52e67-189"><a name="getproperties"></a>Per ottenere le proprietà di un filtro di route</span><span class="sxs-lookup"><span data-stu-id="52e67-189"><a name="getproperties"></a>To get the properties of a route filter</span></span>

<span data-ttu-id="52e67-190">Per ottenere le proprietà di un filtro di route, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="52e67-190">To get the properties of a route filter, use the following steps:</span></span>

1. <span data-ttu-id="52e67-191">Eseguire il comando seguente per ottenere una risorsa filtro di route:</span><span class="sxs-lookup"><span data-stu-id="52e67-191">Run the following command to get the route filter resource:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. <span data-ttu-id="52e67-192">Eseguire il comando seguente per ottenere le regole di filtro di route per la risorsa filtro di route:</span><span class="sxs-lookup"><span data-stu-id="52e67-192">Get the route filter rules for the route-filter resource by running the following command:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <span data-ttu-id="52e67-193"><a name="updateproperties"></a>Per aggiornare le proprietà di un filtro di route</span><span class="sxs-lookup"><span data-stu-id="52e67-193"><a name="updateproperties"></a>To update the properties of a route filter</span></span>

<span data-ttu-id="52e67-194">Se il filtro di route è già associato a un circuito, gli aggiornamenti all'elenco di community BGP includono la propagazione automatica delle modifiche per gli annunci dei prefissi tramite le sessioni BGP stabilite.</span><span class="sxs-lookup"><span data-stu-id="52e67-194">If the route filter is already attached to a circuit, updates to the BGP community list automatically propagates appropriate prefix advertisement changes through the established BGP sessions.</span></span> <span data-ttu-id="52e67-195">È possibile aggiornare l'elenco di community BGP del filtro di route con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="52e67-195">You can update the BGP community list of your route filter using the following command:</span></span>

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="52e67-196"><a name="detach"></a>Per rimuovere l'associazione di un filtro di route da un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="52e67-196"><a name="detach"></a>To detach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="52e67-197">Dopo aver rimosso l'associazione di un filtro di route dal circuito ExpressRoute, nessun prefisso viene annunciato tramite la sessione BGP.</span><span class="sxs-lookup"><span data-stu-id="52e67-197">Once a route filter is detached from the ExpressRoute circuit, no prefixes are advertised through the BGP session.</span></span> <span data-ttu-id="52e67-198">Usare il comando seguente per rimuovere l'associazione di un filtro di route da un circuito ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="52e67-198">You can detach a route filter from an ExpressRoute circuit using the following command:</span></span>
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="52e67-199"><a name="delete"></a>Per eliminare un filtro di route</span><span class="sxs-lookup"><span data-stu-id="52e67-199"><a name="delete"></a>To delete a route filter</span></span>

<span data-ttu-id="52e67-200">È possibile eliminare un filtro di route solo se non è associato a un circuito.</span><span class="sxs-lookup"><span data-stu-id="52e67-200">You can only delete a route filter if it is not attached to any circuit.</span></span> <span data-ttu-id="52e67-201">Assicurarsi che il filtro di route non sia associato a un circuito prima di tentare di eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="52e67-201">Ensure that the route filter is not attached to any circuit before attempting to delete it.</span></span> <span data-ttu-id="52e67-202">È possibile eliminare un filtro di route con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="52e67-202">You can delete a route filter using the following command:</span></span>

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="52e67-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="52e67-203">Next steps</span></span>

<span data-ttu-id="52e67-204">Per altre informazioni su ExpressRoute, vedere le [Domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="52e67-204">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>