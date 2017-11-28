---
title: 'Configurare i filtri di route per il peering Microsoft Azure ExpressRoute: PowerShell | Microsoft Docs'
description: In questo articolo viene descritto come i filtri di route tooconfigure per il Peering Microsoft tramite PowerShell
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
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a><span data-ttu-id="ad0cb-103">Configurare i filtri di route per il peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="ad0cb-103">Configure route filters for Microsoft peering</span></span>

<span data-ttu-id="ad0cb-104">I filtri di route sono tooconsume un modo un sottoinsieme di servizi supportati tramite il peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-104">Route filters are a way tooconsume a subset of supported services through Microsoft peering.</span></span> <span data-ttu-id="ad0cb-105">Hello passaggi in questo articolo consentono configurare e gestire i filtri di route per i circuiti ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-105">hello steps in this article help you configure and manage route filters for ExpressRoute circuits.</span></span>

<span data-ttu-id="ad0cb-106">Dynamics 365 servizi e i servizi di Office 365, ad esempio Exchange Online, SharePoint Online e Skype for Business, sono accessibili tramite il peering Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-106">Dynamics 365 services, and Office 365 services such as Exchange Online, SharePoint Online, and Skype for Business, are accessible through hello Microsoft peering.</span></span> <span data-ttu-id="ad0cb-107">Quando Microsoft peering è configurato in un circuito ExpressRoute, tutti i servizi correlati toothese prefissi sono annunciati tramite sessioni BGP hello stabilite.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-107">When Microsoft peering is configured in an ExpressRoute circuit, all prefixes related toothese services are advertised through hello BGP sessions that are established.</span></span> <span data-ttu-id="ad0cb-108">Un valore di community BGP è collegato tooevery prefisso tooidentify hello servizio verrà offerti attraverso prefisso hello.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-108">A BGP community value is attached tooevery prefix tooidentify hello service that is offered through hello prefix.</span></span> <span data-ttu-id="ad0cb-109">Per un elenco di valori di community hello BGP e i servizi di hello viene eseguito il mapping, vedere [community BGP](expressroute-routing.md#bgp).</span><span class="sxs-lookup"><span data-stu-id="ad0cb-109">For a list of hello BGP community values and hello services they  map to, see [BGP communities](expressroute-routing.md#bgp).</span></span>

<span data-ttu-id="ad0cb-110">Se si richiedono servizi di integrazione applicativa tooall, un numero elevato di prefissi venga pubblicato tramite BGP.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-110">If you require connectivity tooall services, a large number of prefixes are advertised through BGP.</span></span> <span data-ttu-id="ad0cb-111">Ciò aumenta significativamente il dimensioni hello hello di tabelle di route gestita da router all'interno della rete.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-111">This significantly increases hello size of hello route tables maintained by routers within your network.</span></span> <span data-ttu-id="ad0cb-112">Se si prevede solo un sottoinsieme di servizi offerti tramite il peering Microsoft tooconsume, è possibile ridurre le dimensioni di hello delle tabelle di route in due modi.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-112">If you plan tooconsume only a subset of services offered through Microsoft peering, you can reduce hello size of your route tables in two ways.</span></span> <span data-ttu-id="ad0cb-113">È possibile:</span><span class="sxs-lookup"><span data-stu-id="ad0cb-113">You can:</span></span>

- <span data-ttu-id="ad0cb-114">Escludere i prefissi indesiderati applicando filtri di route alle community BGP.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-114">Filter out unwanted prefixes by applying route filters on BGP communities.</span></span> <span data-ttu-id="ad0cb-115">Si tratta di una procedura di rete standard usata comunemente in molte reti.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-115">This is a standard networking practice and is used commonly within many networks.</span></span>

- <span data-ttu-id="ad0cb-116">Definire i filtri di route e applicarli circuito ExpressRoute tooyour.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-116">Define route filters and apply them tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="ad0cb-117">Un filtro di route è una nuova risorsa, che consente di selezionare l'elenco di hello dei servizi è pianificare tooconsume tramite il peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-117">A route filter is a new resource that lets you select hello list of services you plan tooconsume through Microsoft peering.</span></span> <span data-ttu-id="ad0cb-118">Router di ExpressRoute inviare solo elenco hello di prefissi che appartengono a servizi toohello individuati nel filtro di route hello.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-118">ExpressRoute routers only send hello list of prefixes that belong toohello services identified in hello route filter.</span></span>

### <span data-ttu-id="ad0cb-119"><a name="about"></a>Informazioni sui filtri di route</span><span class="sxs-lookup"><span data-stu-id="ad0cb-119"><a name="about"></a>About route filters</span></span>

<span data-ttu-id="ad0cb-120">Quando Microsoft peering è configurato il circuito ExpressRoute, router perimetrali dei Microsoft hello stabilisce una coppia di sessioni BGP con il router perimetrali hello (il proprio o il provider di connettività).</span><span class="sxs-lookup"><span data-stu-id="ad0cb-120">When Microsoft peering is configured on your ExpressRoute circuit, hello Microsoft edge routers establish a pair of BGP sessions with hello edge routers (yours or your connectivity provider's).</span></span> <span data-ttu-id="ad0cb-121">Nessuna route sono rete tooyour annunciato.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-121">No routes are advertised tooyour network.</span></span> <span data-ttu-id="ad0cb-122">rete di tooyour gli annunci di route tooenable, è necessario associare un filtro di route.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-122">tooenable route advertisements tooyour network, you must associate a route filter.</span></span>

<span data-ttu-id="ad0cb-123">Un filtro di route consente di identificare i servizi desiderati tooconsume tramite il peering Microsoft del circuito di ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-123">A route filter lets you identify services you want tooconsume through your ExpressRoute circuit's Microsoft peering.</span></span> <span data-ttu-id="ad0cb-124">È essenzialmente un elenco vuoto di tutti i valori della community di hello BGP.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-124">It is essentially a white list of all hello BGP community values.</span></span> <span data-ttu-id="ad0cb-125">Una volta una risorsa di filtro di route è definita e collegata tooan circuito ExpressRoute, tutti i prefissi che mappa i valori della community BGP toohello sono rete tooyour annunciato.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-125">Once a route filter resource is defined and attached tooan ExpressRoute circuit, all prefixes that map toohello BGP community values are advertised tooyour network.</span></span>

<span data-ttu-id="ad0cb-126">filtri di route in grado di tooattach toobe con servizi di Office 365 su di essi, è necessario disporre di servizi di Office 365 tooconsume autorizzazione tramite ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-126">toobe able tooattach route filters with Office 365 services on them, you must have authorization tooconsume Office 365 services through ExpressRoute.</span></span> <span data-ttu-id="ad0cb-127">Se non si è autorizzati tooconsume Office 365 services tramite ExpressRoute, filtri di route tooattach hello operazione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-127">If you are not authorized tooconsume Office 365 services through ExpressRoute, hello operation tooattach route filters fails.</span></span> <span data-ttu-id="ad0cb-128">Per ulteriori informazioni sul processo di autorizzazione hello, vedere [Azure ExpressRoute per Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span><span class="sxs-lookup"><span data-stu-id="ad0cb-128">For more information about hello authorization process, see [Azure ExpressRoute for Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd).</span></span> <span data-ttu-id="ad0cb-129">Servizi di integrazione applicativa tooDynamics 365 non richiede alcuna autorizzazione precedente.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-129">Connectivity tooDynamics 365 services does NOT require any prior authorization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad0cb-130">Microsoft peering di circuiti ExpressRoute che sono stati configurati precedente tooAugust 1, 2017 disporrà di tutti i prefissi di servizio pubblicati tramite Microsoft peering, anche se non sono definiti i filtri di route.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-130">Microsoft peering of ExpressRoute circuits that were configured prior tooAugust 1, 2017 will have all service prefixes advertised through Microsoft peering, even if route filters are not defined.</span></span> <span data-ttu-id="ad0cb-131">Microsoft peering di circuiti ExpressRoute configurati o dopo il 1 agosto 2017 non avrà alcun prefisso annunciato fino a quando non è associato un filtro di route toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-131">Microsoft peering of ExpressRoute circuits that are configured on or after August 1, 2017 will not have any prefixes advertised until a route filter is attached toohello circuit.</span></span>
> 
> 

### <span data-ttu-id="ad0cb-132"><a name="workflow"></a>Flusso di lavoro</span><span class="sxs-lookup"><span data-stu-id="ad0cb-132"><a name="workflow"></a>Workflow</span></span>

<span data-ttu-id="ad0cb-133">toobe toosuccessfully in grado di connettersi tooservices tramite il peering Microsoft, è necessario completare hello seguendo i passaggi di configurazione:</span><span class="sxs-lookup"><span data-stu-id="ad0cb-133">toobe able toosuccessfully connect tooservices through Microsoft peering, you must complete hello following configuration steps:</span></span>

- <span data-ttu-id="ad0cb-134">È necessario avere un circuito ExpressRoute attivo, per cui è stato effettuato il provisioning del peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-134">You must have an active ExpressRoute circuit that has Microsoft peering provisioned.</span></span> <span data-ttu-id="ad0cb-135">È possibile utilizzare hello seguendo le istruzioni tooaccomplish queste attività:</span><span class="sxs-lookup"><span data-stu-id="ad0cb-135">You can use hello following instructions tooaccomplish these tasks:</span></span>
  - <span data-ttu-id="ad0cb-136">[Creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md) e circuito hello abilitato dal provider di connettività prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-136">[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="ad0cb-137">Hello circuito ExpressRoute deve essere in uno stato di provisioning e abilitato.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-137">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>
  - <span data-ttu-id="ad0cb-138">[Creare il peering Microsoft](expressroute-circuit-peerings.md) se si Gestione sessione BGP di hello direttamente.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-138">[Create Microsoft peering](expressroute-circuit-peerings.md) if you manage hello BGP session directly.</span></span> <span data-ttu-id="ad0cb-139">In caso contrario, richiedere al provider della connettività di effettuare il provisioning del peering Microsoft per il circuito.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-139">Or, have your connectivity provider provision Microsoft peering for your circuit.</span></span>

-  <span data-ttu-id="ad0cb-140">È necessario creare e configurare un filtro di route.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-140">You must create and configure a route filter.</span></span>
    - <span data-ttu-id="ad0cb-141">Identificare hello è servizi con tooconsume tramite il peering Microsoft</span><span class="sxs-lookup"><span data-stu-id="ad0cb-141">Identify hello services you with tooconsume through Microsoft peering</span></span>
    - <span data-ttu-id="ad0cb-142">Identificare hello elenco di valori di community BGP associati ai servizi hello</span><span class="sxs-lookup"><span data-stu-id="ad0cb-142">Identify hello list of BGP community values associated with hello services</span></span>
    - <span data-ttu-id="ad0cb-143">Creare un regola tooallow hello prefisso elenco corrispondente hello valori community BGP</span><span class="sxs-lookup"><span data-stu-id="ad0cb-143">Create a rule tooallow hello prefix list matching hello BGP community values</span></span>

-  <span data-ttu-id="ad0cb-144">È necessario collegare il circuito ExpressRoute toohello di hello route filtro.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-144">You must attach hello route filter toohello ExpressRoute circuit.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ad0cb-145">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="ad0cb-145">Before you begin</span></span>

<span data-ttu-id="ad0cb-146">Prima di iniziare la configurazione, assicurarsi che siano soddisfatti hello seguenti criteri:</span><span class="sxs-lookup"><span data-stu-id="ad0cb-146">Before you begin configuration, make sure you meet hello following criteria:</span></span>

 - <span data-ttu-id="ad0cb-147">Installare hello l'ultima versione di hello cmdlet PowerShell di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-147">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="ad0cb-148">Per altre informazioni, vedere [Installare e configurare Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="ad0cb-148">For more information, see [Install and configure Azure PowerShelll](/powershell/azure/install-azurerm-ps).</span></span>

  > [!NOTE]
  > <span data-ttu-id="ad0cb-149">Scaricare la versione più recente di hello da hello PowerShell Gallery, anziché utilizzare hello programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-149">Download hello latest version from hello PowerShell Gallery, rather than using hello Installer.</span></span> <span data-ttu-id="ad0cb-150">Hello Installer attualmente non supporta i cmdlet di hello necessario.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-150">hello Installer currently does not support hello required cmdlets.</span></span>
  > 

 - <span data-ttu-id="ad0cb-151">Hello revisione [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-151">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>

 - <span data-ttu-id="ad0cb-152">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-152">You must have an active ExpressRoute circuit.</span></span> <span data-ttu-id="ad0cb-153">Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md) e circuito hello abilitato dal provider di connettività prima di procedere.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-153">Follow hello instructions too[Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider before you proceed.</span></span> <span data-ttu-id="ad0cb-154">Hello circuito ExpressRoute deve essere in uno stato di provisioning e abilitato.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-154">hello ExpressRoute circuit must be in a provisioned and enabled state.</span></span>

 - <span data-ttu-id="ad0cb-155">È necessario disporre di un peering Microsoft attivo.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-155">You must have an active Microsoft peering.</span></span> <span data-ttu-id="ad0cb-156">Seguire le istruzioni per [creare e modificare la configurazione del peering](expressroute-circuit-peerings.md).</span><span class="sxs-lookup"><span data-stu-id="ad0cb-156">Follow instructions at [Create and modifying peering configuration](expressroute-circuit-peerings.md)</span></span>

### <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="ad0cb-157">Accedi tooyour account Azure</span><span class="sxs-lookup"><span data-stu-id="ad0cb-157">Log in tooyour Azure account</span></span>

<span data-ttu-id="ad0cb-158">Prima di iniziare questa configurazione, è necessario accedere tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-158">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="ad0cb-159">cmdlet di Hello richiede le credenziali di accesso hello per l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-159">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="ad0cb-160">Dopo l'accesso, scarica le impostazioni dell'account in modo che siano disponibili tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-160">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="ad0cb-161">Aprire la console di PowerShell con privilegi elevati e tooyour account di connessione.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-161">Open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="ad0cb-162">Utilizzare hello toohelp esempio che ci si connette seguenti:</span><span class="sxs-lookup"><span data-stu-id="ad0cb-162">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="ad0cb-163">Se si dispone di più sottoscrizioni di Azure, controllare le sottoscrizioni di hello per account hello.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-163">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="ad0cb-164">Specificare una sottoscrizione di hello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-164">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="ad0cb-165"><a name="prefixes"></a>Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-165"><a name="prefixes"></a>Step 1.</span></span> <span data-ttu-id="ad0cb-166">Ottenere un elenco di prefissi e di valori di community BGP</span><span class="sxs-lookup"><span data-stu-id="ad0cb-166">Get a list of prefixes and BGP community values</span></span>

### <a name="1-get-a-list-of-bgp-community-values"></a><span data-ttu-id="ad0cb-167">1. Ottenere un elenco dei valori di community BGP</span><span class="sxs-lookup"><span data-stu-id="ad0cb-167">1. Get a list of BGP community values</span></span>

<span data-ttu-id="ad0cb-168">Utilizzare hello dopo cmdlet tooget hello elenco dei valori di community BGP associati servizi accessibili tramite il peering Microsoft e hello elenco di prefissi associati:</span><span class="sxs-lookup"><span data-stu-id="ad0cb-168">Use hello following cmdlet tooget hello list of BGP community values associated with services accessible through Microsoft peering, and hello list of prefixes associated with them:</span></span>

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a><span data-ttu-id="ad0cb-169">2. Creare un elenco di valori hello che si desidera toouse</span><span class="sxs-lookup"><span data-stu-id="ad0cb-169">2. Make a list of hello values that you want toouse</span></span>

<span data-ttu-id="ad0cb-170">Creare un elenco dei valori di community BGP da toouse nel filtro di route hello.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-170">Make a list of BGP community values you want toouse in hello route filter.</span></span> <span data-ttu-id="ad0cb-171">Ad esempio, il valore di community BGP per servizi di Dynamics 365 hello è 12076:5040.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-171">As an example, hello BGP community value for Dynamics 365 services is 12076:5040.</span></span>

## <span data-ttu-id="ad0cb-172"><a name="filter"></a>Passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-172"><a name="filter"></a>Step 2.</span></span> <span data-ttu-id="ad0cb-173">Creare un filtro di route e una regola di filtro</span><span class="sxs-lookup"><span data-stu-id="ad0cb-173">Create a route filter and a filter rule</span></span>

<span data-ttu-id="ad0cb-174">Un filtro di route può avere solo una regola e hello regola deve essere di tipo 'Consenti'.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-174">A route filter can have only one rule, and hello rule must be of type 'Allow'.</span></span> <span data-ttu-id="ad0cb-175">A questa regola può essere associato un elenco di valori di community BGP.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-175">This rule can have a list of BGP community values associated with it.</span></span>

### <a name="1-create-a-route-filter"></a><span data-ttu-id="ad0cb-176">1. Creare un filtro di route</span><span class="sxs-lookup"><span data-stu-id="ad0cb-176">1. Create a route filter</span></span>

<span data-ttu-id="ad0cb-177">Creare innanzitutto il filtro di route hello.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-177">First, create hello route filter.</span></span> <span data-ttu-id="ad0cb-178">comando Hello 'New-AzureRmRouteFilter' Crea solo una risorsa di filtro di route.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-178">hello command 'New-AzureRmRouteFilter' only creates a route filter resource.</span></span> <span data-ttu-id="ad0cb-179">Dopo aver creato la risorsa hello, è necessario creare una regola e collegarlo oggetto filtro di route toohello.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-179">After you create hello resource, you must then create a rule and attach it toohello route filter object.</span></span> <span data-ttu-id="ad0cb-180">Eseguire hello successivo comando toocreate una risorsa di filtro delle route:</span><span class="sxs-lookup"><span data-stu-id="ad0cb-180">Run hello following command toocreate a route filter resource:</span></span>

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a><span data-ttu-id="ad0cb-181">2. Creare una regola di filtro</span><span class="sxs-lookup"><span data-stu-id="ad0cb-181">2. Create a filter rule</span></span>

<span data-ttu-id="ad0cb-182">È possibile specificare un insieme di Comunità BGP come un elenco delimitato da virgole, come illustrato nell'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-182">You can specify a set of BGP communities as a comma-separated list, as shown in hello example.</span></span> <span data-ttu-id="ad0cb-183">Eseguire una nuova regola di hello successivo comando toocreate:</span><span class="sxs-lookup"><span data-stu-id="ad0cb-183">Run hello following command toocreate a new rule:</span></span>
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a><span data-ttu-id="ad0cb-184">3. Aggiungere filtri di route hello regola toohello</span><span class="sxs-lookup"><span data-stu-id="ad0cb-184">3. Add hello rule toohello route filter</span></span>

<span data-ttu-id="ad0cb-185">Eseguire hello comando tooadd hello regola toohello route filtro seguente:</span><span class="sxs-lookup"><span data-stu-id="ad0cb-185">Run hello following command tooadd hello filter rule toohello route filter:</span></span>
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="ad0cb-186"><a name="attach"></a>Passaggio 3.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-186"><a name="attach"></a>Step 3.</span></span> <span data-ttu-id="ad0cb-187">Collegare il circuito ExpressRoute hello route filtro tooan</span><span class="sxs-lookup"><span data-stu-id="ad0cb-187">Attach hello route filter tooan ExpressRoute circuit</span></span>

<span data-ttu-id="ad0cb-188">Eseguire hello comando tooattach hello route filtro toohello circuito ExpressRoute, presupponendo che si dispone solo di peering Microsoft seguenti:</span><span class="sxs-lookup"><span data-stu-id="ad0cb-188">Run hello following command tooattach hello route filter toohello ExpressRoute circuit, assuming you have only Microsoft peering:</span></span>

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="ad0cb-189"><a name="getproperties"></a>proprietà hello tooget di un filtro di route</span><span class="sxs-lookup"><span data-stu-id="ad0cb-189"><a name="getproperties"></a>tooget hello properties of a route filter</span></span>

<span data-ttu-id="ad0cb-190">proprietà hello tooget di un filtro di route, usare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="ad0cb-190">tooget hello properties of a route filter, use hello following steps:</span></span>

1. <span data-ttu-id="ad0cb-191">Risorsa di filtro route hello tooget comando che segue di hello esecuzione:</span><span class="sxs-lookup"><span data-stu-id="ad0cb-191">Run hello following command tooget hello route filter resource:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. <span data-ttu-id="ad0cb-192">Ottenere le regole di filtro di hello route per la risorsa di filtro di route hello eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ad0cb-192">Get hello route filter rules for hello route-filter resource by running hello following command:</span></span>

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <span data-ttu-id="ad0cb-193"><a name="updateproperties"></a>proprietà hello tooupdate di un filtro di route</span><span class="sxs-lookup"><span data-stu-id="ad0cb-193"><a name="updateproperties"></a>tooupdate hello properties of a route filter</span></span>

<span data-ttu-id="ad0cb-194">Se è già collegato il filtro di route hello tooa circuito, elenco di aggiornamenti toohello BGP community propaga automaticamente le modifiche di annuncio prefisso appropriato tramite sessioni BGP hello stabilita.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-194">If hello route filter is already attached tooa circuit, updates toohello BGP community list automatically propagates appropriate prefix advertisement changes through hello established BGP sessions.</span></span> <span data-ttu-id="ad0cb-195">È possibile aggiornare l'elenco di community hello BGP del filtro route utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ad0cb-195">You can update hello BGP community list of your route filter using hello following command:</span></span>

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <span data-ttu-id="ad0cb-196"><a name="detach"></a>toodetach un filtro di route da un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="ad0cb-196"><a name="detach"></a>toodetach a route filter from an ExpressRoute circuit</span></span>

<span data-ttu-id="ad0cb-197">Dopo essere stato disconnesso da hello circuito ExpressRoute, un filtro di route non prefissi sono annunciati tramite sessione BGP hello.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-197">Once a route filter is detached from hello ExpressRoute circuit, no prefixes are advertised through hello BGP session.</span></span> <span data-ttu-id="ad0cb-198">È possibile scollegare un filtro di route da un circuito ExpressRoute tramite hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ad0cb-198">You can detach a route filter from an ExpressRoute circuit using hello following command:</span></span>
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <span data-ttu-id="ad0cb-199"><a name="delete"></a>toodelete un filtro di route</span><span class="sxs-lookup"><span data-stu-id="ad0cb-199"><a name="delete"></a>toodelete a route filter</span></span>

<span data-ttu-id="ad0cb-200">È possibile solo eliminare un filtro di route, se non è collegato tooany circuito.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-200">You can only delete a route filter if it is not attached tooany circuit.</span></span> <span data-ttu-id="ad0cb-201">Verificare che il filtro route hello non è collegato il circuito tooany prima di tentare di toodelete è.</span><span class="sxs-lookup"><span data-stu-id="ad0cb-201">Ensure that hello route filter is not attached tooany circuit before attempting toodelete it.</span></span> <span data-ttu-id="ad0cb-202">È possibile eliminare un filtro di route utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ad0cb-202">You can delete a route filter using hello following command:</span></span>

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="ad0cb-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ad0cb-203">Next steps</span></span>

<span data-ttu-id="ad0cb-204">Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="ad0cb-204">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
