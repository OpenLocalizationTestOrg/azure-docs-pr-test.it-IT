---
title: aaaWorkflows per la configurazione di un circuito ExpressRoute | Documenti Microsoft
description: Questa pagina vengono illustrati i flussi di lavoro hello per la configurazione di peering e il circuito ExpressRoute
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="6b7d2-103">Flussi di lavoro ExpressRoute per provisioning di un circuito e stati di circuito</span><span class="sxs-lookup"><span data-stu-id="6b7d2-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="6b7d2-104">Questa pagina viene illustrato il provisioning del servizio di hello e routing configurazione dei flussi di lavoro a un livello elevato.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-104">This page walks you through hello service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="6b7d2-105">Hello figura riportata di seguito e i passaggi corrispondenti mostrano attività hello che è necessario eseguire in ordine toohave un ExpressRoute circuito provisioning end-to-end.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-105">hello following figure and corresponding steps show hello tasks you must follow in order toohave an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="6b7d2-106">Utilizzare PowerShell tooconfigure un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-106">Use PowerShell tooconfigure an ExpressRoute circuit.</span></span> <span data-ttu-id="6b7d2-107">Seguire le istruzioni hello hello [circuiti ExpressRoute creare](expressroute-howto-circuit-classic.md) per ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-107">Follow hello instructions in hello [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="6b7d2-108">Connettività ordine dal provider di servizi di hello.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-108">Order connectivity from hello service provider.</span></span> <span data-ttu-id="6b7d2-109">Questo processo varia.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-109">This process varies.</span></span> <span data-ttu-id="6b7d2-110">Per ulteriori dettagli su come contattare il provider di connettività tooorder connettività.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-110">Contact your connectivity provider for more details about how tooorder connectivity.</span></span>
3. <span data-ttu-id="6b7d2-111">Verificare che il circuito hello sia stato preparato correttamente verificando il circuito ExpressRoute hello provisioning dello stato tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-111">Ensure that hello circuit has been provisioned successfully by verifying hello ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="6b7d2-112">Configurare i domini di routing.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-112">Configure routing domains.</span></span> <span data-ttu-id="6b7d2-113">Se il provider di connettività gestisce il livello 3, configurerà il routing per il circuito.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="6b7d2-114">Se il provider di connettività offre solo servizi di livello 2, è necessario configurare il routing per linee guida descritte in hello [requisiti di routing](expressroute-routing.md) e [configurazione del routing](expressroute-howto-routing-classic.md) pagine.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in hello [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="6b7d2-115">Abilitare peering privato di Azure, è necessario abilitare questo peer di tooconnect tooVMs / cloud servizi distribuiti nelle reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-115">Enable Azure private peering - You must enable this peering tooconnect tooVMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="6b7d2-116">Abilitare peering pubblico di Azure, è necessario abilitare peering pubblico di Azure se si desiderano tooconnect tooAzure servizi ospitati su indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-116">Enable Azure public peering - You must enable Azure public peering if you wish tooconnect tooAzure services hosted on public IP addresses.</span></span> <span data-ttu-id="6b7d2-117">Si tratta di un tooaccess requisito risorse di Azure se si è scelto di tooenable routing predefinito per il peering privato di Azure.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-117">This is a requirement tooaccess Azure resources if you have chosen tooenable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="6b7d2-118">Abilitare Microsoft peering - è necessario abilitare questo tooaccess Office 365 e Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-118">Enable Microsoft peering - You must enable this tooaccess Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="6b7d2-119">È necessario assicurarsi che si usa un proxy separato o edge tooconnect tooMicrosoft rispetto a quello che viene utilizzato per hello hello Internet.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-119">You must ensure that you use a separate proxy / edge tooconnect tooMicrosoft than hello one you use for hello Internet.</span></span> <span data-ttu-id="6b7d2-120">Utilizzo di hello stesso bordo per ExpressRoute e hello Internet causerà routing asimmetrica e causare interruzioni della connettività di rete.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-120">Using hello same edge for both ExpressRoute and hello Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="6b7d2-121">Il collegamento virtuale reti circuiti tooExpressRoute: È possibile collegare il circuito ExpressRoute tooyour reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-121">Linking virtual networks tooExpressRoute circuits - You can link virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="6b7d2-122">Seguire le istruzioni [toolink reti virtuali](expressroute-howto-linkvnet-arm.md) tooyour circuito.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-122">Follow instructions [toolink VNets](expressroute-howto-linkvnet-arm.md) tooyour circuit.</span></span> <span data-ttu-id="6b7d2-123">Queste reti virtuali possono essere nella stessa sottoscrizione Azure circuito ExpressRoute hello hello, oppure può essere in una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-123">These VNets can either be in hello same Azure subscription as hello ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="6b7d2-124">Stati di provisioning del circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6b7d2-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="6b7d2-125">Ogni circuito ExpressRoute prevede due stati:</span><span class="sxs-lookup"><span data-stu-id="6b7d2-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="6b7d2-126">Stato di provisioning del provider di servizi</span><span class="sxs-lookup"><span data-stu-id="6b7d2-126">Service provider provisioning state</span></span>
* <span data-ttu-id="6b7d2-127">Stato</span><span class="sxs-lookup"><span data-stu-id="6b7d2-127">Status</span></span>

<span data-ttu-id="6b7d2-128">Status rappresenta lo stato di provisioning di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="6b7d2-129">Questa proprietà è impostata tooEnabled quando si crea un circuito Expressroute</span><span class="sxs-lookup"><span data-stu-id="6b7d2-129">This property is set tooEnabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="6b7d2-130">stato di provisioning provider di connettività Hello rappresenta lo stato di hello sul lato del provider di connettività hello.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-130">hello connectivity provider provisioning state represents hello state on hello connectivity provider's side.</span></span> <span data-ttu-id="6b7d2-131">Può essere impostato su *NotProvisioned*, *Provisioning* o *Provisioned*.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="6b7d2-132">Hello circuito ExpressRoute deve essere in stato di provisioning eseguito per si toobe in grado di toouse è.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-132">hello ExpressRoute circuit must be in Provisioned state for you toobe able toouse it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="6b7d2-133">Stati possibili di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6b7d2-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="6b7d2-134">In questa sezione elenca gli stati possibili di hello per un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-134">This section lists out hello possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="6b7d2-135">**Al momento della creazione**</span><span class="sxs-lookup"><span data-stu-id="6b7d2-135">**At creation time**</span></span>

<span data-ttu-id="6b7d2-136">Verrà visualizzato il circuito ExpressRoute hello in hello seguente non appena è stato eseguito circuito ExpressRoute di hello PowerShell cmdlet toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-136">You will see hello ExpressRoute circuit in hello following state as soon as you run hello PowerShell cmdlet toocreate hello ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="6b7d2-137">**Quando i provider di connettività è nel processo di hello del provisioning del circuito hello**</span><span class="sxs-lookup"><span data-stu-id="6b7d2-137">**When connectivity provider is in hello process of provisioning hello circuit**</span></span>

<span data-ttu-id="6b7d2-138">Verrà visualizzato il circuito ExpressRoute hello in hello seguente non appena è stato passare i provider di connettività toohello chiave servizio hello e avvio hello processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-138">You will see hello ExpressRoute circuit in hello following state as soon as you pass hello service key toohello connectivity provider and they have started hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="6b7d2-139">**Quando il provider di connettività è stata completata hello processo di provisioning**</span><span class="sxs-lookup"><span data-stu-id="6b7d2-139">**When connectivity provider has completed hello provisioning process**</span></span>

<span data-ttu-id="6b7d2-140">Verrà visualizzato hello in seguito lo stato come provider di connettività hello ha completato il processo di provisioning hello hello il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-140">You will see hello ExpressRoute circuit in hello following state as soon as hello connectivity provider has completed hello provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="6b7d2-141">Il provisioning e abilitato è hello circuito hello lo stato è possibile solo per si toobe in grado di toouse è.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-141">Provisioned and Enabled is hello only state hello circuit can be in for you toobe able toouse it.</span></span> <span data-ttu-id="6b7d2-142">Se si usa un provider di livello 2, è possibile configurare il routing per il circuito solo quando è attivo questo stato.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="6b7d2-143">**Quando il provider di connettività è deprovisioning circuito hello**</span><span class="sxs-lookup"><span data-stu-id="6b7d2-143">**When connectivity provider is deprovisioning hello circuit**</span></span>

<span data-ttu-id="6b7d2-144">Se è stato richiesto il circuito ExpressRoute hello toodeprovision di hello service provider, verrà visualizzato il circuito hello imposta toohello seguente stato dopo che il provider di servizi di hello ha completato hello processo di deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-144">If you requested hello service provider toodeprovision hello ExpressRoute circuit, you will see hello circuit set toohello following state after hello service provider has completed hello deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="6b7d2-145">È possibile scegliere di abilitare toore, se necessario, o eseguire i cmdlet PowerShell circuito hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-145">You can choose toore-enable it if needed, or run PowerShell cmdlets toodelete hello circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="6b7d2-146">Se si esegue PowerShell cmdlet toodelete hello circuito quando hello ServiceProviderProvisioningState Provisioning o provisioning eseguito operazione hello hello avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-146">If you run hello PowerShell cmdlet toodelete hello circuit when hello ServiceProviderProvisioningState is Provisioning or Provisioned hello operation will fail.</span></span> <span data-ttu-id="6b7d2-147">. Prima di lavoro con il circuito ExpressRoute di hello toodeprovision di provider di connettività, quindi eliminare il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-147">Please work with your connectivity provider toodeprovision hello ExpressRoute circuit first and then delete hello circuit.</span></span> <span data-ttu-id="6b7d2-148">Microsoft continuerà circuito hello toobill fino a quando non si esegue hello circuito hello toodelete cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-148">Microsoft will continue toobill hello circuit until you run hello PowerShell cmdlet toodelete hello circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="6b7d2-149">Stato di configurazione della sessione di routing</span><span class="sxs-lookup"><span data-stu-id="6b7d2-149">Routing session configuration state</span></span>
<span data-ttu-id="6b7d2-150">stato di provisioning BGP Hello consente di sapere se sessione BGP hello è stata abilitata in hello Microsoft edge.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-150">hello BGP provisioning state lets you know if hello BGP session has been enabled on hello Microsoft edge.</span></span> <span data-ttu-id="6b7d2-151">Hello stato deve essere abilitato per l'utente toobe toouse in grado di hello peering.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-151">hello state must be enabled for you toobe able toouse hello peering.</span></span>

<span data-ttu-id="6b7d2-152">È stato della sessione BGP hello toocheck importante soprattutto per il peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-152">It is important toocheck hello BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="6b7d2-153">In aggiunta toohello BGP stato di provisioning, è un altro stato denominato *stato prefissi pubblici annunciati*.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-153">In addition toohello BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="6b7d2-154">Hello annunciati prefissi pubblici stato deve essere *configurato* dello stato, sia per hello BGP sessione toobe backup e per il routing toowork end-to-end.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-154">hello advertised public prefixes state must be in *configured* state, both for hello BGP session toobe up and for your routing toowork end-to-end.</span></span> 

<span data-ttu-id="6b7d2-155">Se hello annunciati stato pubblica prefisso è impostato tooa *convalida necessita* stato sessione BGP hello non è abilitata, come hello annunciati prefissi non corrispondeva hello come numero in uno dei registri di routing hello.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-155">If hello advertised public prefix state is set tooa *validation needed* state, hello BGP session is not enabled, as hello advertised prefixes did not match hello AS number in any of hello routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="6b7d2-156">Se hello annunciati stato prefissi pubblici *convalida manuale* stato, è necessario aprire un ticket di supporto con [supporto tecnico Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) e dimostrare che si è proprietari di indirizzi IP hello annunciati lungo hello associata numero sistema autonomo.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-156">If hello advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own hello IP addresses advertised along with hello associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6b7d2-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6b7d2-157">Next steps</span></span>
* <span data-ttu-id="6b7d2-158">Configurare la connessione ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6b7d2-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="6b7d2-159">Creare un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6b7d2-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="6b7d2-160">Configurare il routing</span><span class="sxs-lookup"><span data-stu-id="6b7d2-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="6b7d2-161">Collegare un circuito ExpressRoute di tooan rete virtuale</span><span class="sxs-lookup"><span data-stu-id="6b7d2-161">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

