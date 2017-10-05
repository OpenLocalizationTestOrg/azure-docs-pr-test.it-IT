---
title: Flussi di lavoro per la configurazione di un circuito ExpressRoute | Documentazione Microsoft
description: Questa pagina illustra i flussi di lavoro per la configurazione di un circuito ExpressRoute e dei peering
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
ms.openlocfilehash: cba1b2cfee379e7d2b079bcb3089981ef1044d66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a><span data-ttu-id="f9289-103">Flussi di lavoro ExpressRoute per provisioning di un circuito e stati di circuito</span><span class="sxs-lookup"><span data-stu-id="f9289-103">ExpressRoute workflows for circuit provisioning and circuit states</span></span>
<span data-ttu-id="f9289-104">Questa pagina illustra i flussi di lavoro di provisioning del servizio e configurazione del routing a livello generale.</span><span class="sxs-lookup"><span data-stu-id="f9289-104">This page walks you through the service provisioning and routing configuration workflows at a high level.</span></span>

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

<span data-ttu-id="f9289-105">La figura e i passaggi corrispondenti riportati di seguito descrivono le attività per il provisioning end-to-end di un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f9289-105">The following figure and corresponding steps show the tasks you must follow in order to have an ExpressRoute circuit provisioned end-to-end.</span></span> 

1. <span data-ttu-id="f9289-106">Usare PowerShell per configurare un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f9289-106">Use PowerShell to configure an ExpressRoute circuit.</span></span> <span data-ttu-id="f9289-107">Per altre informazioni, seguire le istruzioni contenute nell'articolo relativo alla [creazione di circuiti ExpressRoute](expressroute-howto-circuit-classic.md) .</span><span class="sxs-lookup"><span data-stu-id="f9289-107">Follow the instructions in the [Create ExpressRoute circuits](expressroute-howto-circuit-classic.md) article for more details.</span></span>
2. <span data-ttu-id="f9289-108">Ordinare la connettività dal provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="f9289-108">Order connectivity from the service provider.</span></span> <span data-ttu-id="f9289-109">Questo processo varia.</span><span class="sxs-lookup"><span data-stu-id="f9289-109">This process varies.</span></span> <span data-ttu-id="f9289-110">Per altre informazioni su come ordinare la connettività, contattare il provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="f9289-110">Contact your connectivity provider for more details about how to order connectivity.</span></span>
3. <span data-ttu-id="f9289-111">Assicurarsi che il provisioning del circuito sia stato eseguito correttamente verificando lo stato di provisioning del circuito ExpressRoute tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f9289-111">Ensure that the circuit has been provisioned successfully by verifying the ExpressRoute circuit provisioning state through PowerShell.</span></span> 
4. <span data-ttu-id="f9289-112">Configurare i domini di routing.</span><span class="sxs-lookup"><span data-stu-id="f9289-112">Configure routing domains.</span></span> <span data-ttu-id="f9289-113">Se il provider di connettività gestisce il livello 3, configurerà il routing per il circuito.</span><span class="sxs-lookup"><span data-stu-id="f9289-113">If your connectivity provider manages Layer 3 for you, they will configure routing for your circuit.</span></span> <span data-ttu-id="f9289-114">Se invece il provider di connettività offre solo servizi di livello 2, sarà necessario configurare il routing secondo le linee guida descritte nelle pagine relative ai [requisiti di routing](expressroute-routing.md) e alla [configurazione del routing](expressroute-howto-routing-classic.md).</span><span class="sxs-lookup"><span data-stu-id="f9289-114">If your connectivity provider only offers Layer 2 services, you must configure routing per guidelines described in the [routing requirements](expressroute-routing.md) and [routing configuration](expressroute-howto-routing-classic.md) pages.</span></span>
   
   * <span data-ttu-id="f9289-115">Abilitare il peering privato di Azure: è necessario abilitare questo peering per la connessione alle macchine virtuali e ai servizi cloud distribuiti nelle reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="f9289-115">Enable Azure private peering - You must enable this peering to connect to VMs / cloud services deployed within virtual networks.</span></span>
   * <span data-ttu-id="f9289-116">Abilitare il peering pubblico di Azure: è necessario abilitare questo peering se si desidera connettersi ai servizi di Azure ospitati in indirizzi IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="f9289-116">Enable Azure public peering - You must enable Azure public peering if you wish to connect to Azure services hosted on public IP addresses.</span></span> <span data-ttu-id="f9289-117">Questo è un requisito per accedere alle risorse di Azure se si è scelto di abilitare il routing predefinito per il peering privato di Azure.</span><span class="sxs-lookup"><span data-stu-id="f9289-117">This is a requirement to access Azure resources if you have chosen to enable default routing for Azure private peering.</span></span>
   * <span data-ttu-id="f9289-118">Abilitare il peering Microsoft: è necessario abilitare questo peering per accedere ai servizi Office 365 e Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="f9289-118">Enable Microsoft peering - You must enable this to access Office 365 and Dynamics 365.</span></span> 
     
     > [!IMPORTANT]
     > <span data-ttu-id="f9289-119">Per la connessione a Microsoft è necessario usare un server proxy/perimetrale separato rispetto a quello usato per Internet.</span><span class="sxs-lookup"><span data-stu-id="f9289-119">You must ensure that you use a separate proxy / edge to connect to Microsoft than the one you use for the Internet.</span></span> <span data-ttu-id="f9289-120">Se si usa lo stesso server perimetrale per ExpressRoute e Internet, si verificherà un routing asimmetrico con interruzioni della connettività di rete.</span><span class="sxs-lookup"><span data-stu-id="f9289-120">Using the same edge for both ExpressRoute and the Internet will cause asymmetric routing and cause connectivity outages for your network.</span></span>
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. <span data-ttu-id="f9289-121">Collegamento di reti virtuali a circuiti ExpressRoute: è possibile collegare reti virtuali al circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f9289-121">Linking virtual networks to ExpressRoute circuits - You can link virtual networks to your ExpressRoute circuit.</span></span> <span data-ttu-id="f9289-122">Seguire le istruzioni [per collegare reti virtuali](expressroute-howto-linkvnet-arm.md) a un circuito.</span><span class="sxs-lookup"><span data-stu-id="f9289-122">Follow instructions [to link VNets](expressroute-howto-linkvnet-arm.md) to your circuit.</span></span> <span data-ttu-id="f9289-123">Queste reti virtuali possono trovarsi nella stessa sottoscrizione di Azure del circuito ExpressRoute oppure in una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="f9289-123">These VNets can either be in the same Azure subscription as the ExpressRoute circuit, or can be in a different subscription.</span></span>

## <a name="expressroute-circuit-provisioning-states"></a><span data-ttu-id="f9289-124">Stati di provisioning del circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f9289-124">ExpressRoute circuit provisioning states</span></span>
<span data-ttu-id="f9289-125">Ogni circuito ExpressRoute prevede due stati:</span><span class="sxs-lookup"><span data-stu-id="f9289-125">Each ExpressRoute circuit has two states:</span></span>

* <span data-ttu-id="f9289-126">Stato di provisioning del provider di servizi</span><span class="sxs-lookup"><span data-stu-id="f9289-126">Service provider provisioning state</span></span>
* <span data-ttu-id="f9289-127">Stato</span><span class="sxs-lookup"><span data-stu-id="f9289-127">Status</span></span>

<span data-ttu-id="f9289-128">Status rappresenta lo stato di provisioning di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f9289-128">Status represents Microsoft's provisioning state.</span></span> <span data-ttu-id="f9289-129">Questa proprietà è impostata su Enabled quando si crea un circuito Expressroute</span><span class="sxs-lookup"><span data-stu-id="f9289-129">This property is set to Enabled when you create an Expressroute circuit</span></span>

<span data-ttu-id="f9289-130">Lo stato di provisioning del provider di connettività rappresenta lo stato sul lato del provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="f9289-130">The connectivity provider provisioning state represents the state on the connectivity provider's side.</span></span> <span data-ttu-id="f9289-131">Può essere impostato su *NotProvisioned*, *Provisioning* o *Provisioned*.</span><span class="sxs-lookup"><span data-stu-id="f9289-131">It can either be *NotProvisioned*, *Provisioning*, or *Provisioned*.</span></span> <span data-ttu-id="f9289-132">Il circuito ExpressRoute può essere usato solo se è impostato sullo stato Provisioned.</span><span class="sxs-lookup"><span data-stu-id="f9289-132">The ExpressRoute circuit must be in Provisioned state for you to be able to use it.</span></span>

### <a name="possible-states-of-an-expressroute-circuit"></a><span data-ttu-id="f9289-133">Stati possibili di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f9289-133">Possible states of an ExpressRoute circuit</span></span>
<span data-ttu-id="f9289-134">Questa sezione elenca gli stati possibili di un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f9289-134">This section lists out the possible states for an ExpressRoute circuit.</span></span>

<span data-ttu-id="f9289-135">**Al momento della creazione**</span><span class="sxs-lookup"><span data-stu-id="f9289-135">**At creation time**</span></span>

<span data-ttu-id="f9289-136">Lo stato del circuito ExpressRoute sarà il seguente nel momento in cui si esegue il cmdlet di PowerShell per creare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f9289-136">You will see the ExpressRoute circuit in the following state as soon as you run the PowerShell cmdlet to create the ExpressRoute circuit.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="f9289-137">**Quando il provider di connettività è in fase di provisioning del circuito**</span><span class="sxs-lookup"><span data-stu-id="f9289-137">**When connectivity provider is in the process of provisioning the circuit**</span></span>

<span data-ttu-id="f9289-138">Lo stato del circuito ExpressRoute sarà il seguente quando si passa la chiave di servizio al provider di connettività ed è stato avviato il processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="f9289-138">You will see the ExpressRoute circuit in the following state as soon as you pass the service key to the connectivity provider and they have started the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


<span data-ttu-id="f9289-139">**Quando il provider di connettività ha completato il processo di provisioning**</span><span class="sxs-lookup"><span data-stu-id="f9289-139">**When connectivity provider has completed the provisioning process**</span></span>

<span data-ttu-id="f9289-140">Lo stato del circuito ExpressRoute sarà il seguente quando il provider di connettività ha completato il processo di provisioning.</span><span class="sxs-lookup"><span data-stu-id="f9289-140">You will see the ExpressRoute circuit in the following state as soon as the connectivity provider has completed the provisioning process.</span></span>

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

<span data-ttu-id="f9289-141">Provisioned ed Enabled sono gli unici stati che consentono di usare il circuito.</span><span class="sxs-lookup"><span data-stu-id="f9289-141">Provisioned and Enabled is the only state the circuit can be in for you to be able to use it.</span></span> <span data-ttu-id="f9289-142">Se si usa un provider di livello 2, è possibile configurare il routing per il circuito solo quando è attivo questo stato.</span><span class="sxs-lookup"><span data-stu-id="f9289-142">If you are using a Layer 2 provider, you can configure routing for your circuit only when it is in this state.</span></span>

<span data-ttu-id="f9289-143">**Quando il provider di connettività sta eseguendo il deprovisioning del circuito**</span><span class="sxs-lookup"><span data-stu-id="f9289-143">**When connectivity provider is deprovisioning the circuit**</span></span>

<span data-ttu-id="f9289-144">Se si è richiesto al provider di servizi di eseguire il deprovisioning del circuito ExpressRoute, al termine del processo di deprovisioning eseguito dal provider di servizi lo stato del circuito sarà il seguente.</span><span class="sxs-lookup"><span data-stu-id="f9289-144">If you requested the service provider to deprovision the ExpressRoute circuit, you will see the circuit set to the following state after the service provider has completed the deprovisioning process.</span></span>

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


<span data-ttu-id="f9289-145">È possibile scegliere di abilitarlo nuovamente, se necessario, o eseguire i cmdlet di PowerShell per eliminare il circuito.</span><span class="sxs-lookup"><span data-stu-id="f9289-145">You can choose to re-enable it if needed, or run PowerShell cmdlets to delete the circuit.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="f9289-146">Se si esegue il cmdlet PowerShell per eliminare il circuito quando lo stato di ServiceProviderProvisioningState è Provisioning in corso o Provisioning eseguito, l'operazione avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="f9289-146">If you run the PowerShell cmdlet to delete the circuit when the ServiceProviderProvisioningState is Provisioning or Provisioned the operation will fail.</span></span> <span data-ttu-id="f9289-147">Collaborare con il provider di connettività per eseguire il deprovisioning del circuito ExpressRoute e quindi eliminare il circuito.</span><span class="sxs-lookup"><span data-stu-id="f9289-147">Please work with your connectivity provider to deprovision the ExpressRoute circuit first and then delete the circuit.</span></span> <span data-ttu-id="f9289-148">Microsoft continuerà ad applicare l'addebito per il circuito finché non si esegue il cmdlet di PowerShell per eliminare il circuito.</span><span class="sxs-lookup"><span data-stu-id="f9289-148">Microsoft will continue to bill the circuit until you run the PowerShell cmdlet to delete the circuit.</span></span>
> 
> 

## <a name="routing-session-configuration-state"></a><span data-ttu-id="f9289-149">Stato di configurazione della sessione di routing</span><span class="sxs-lookup"><span data-stu-id="f9289-149">Routing session configuration state</span></span>
<span data-ttu-id="f9289-150">Lo stato di provisioning BGP indica se la sessione BGP è stata abilitata sul lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f9289-150">The BGP provisioning state lets you know if the BGP session has been enabled on the Microsoft edge.</span></span> <span data-ttu-id="f9289-151">Per usare il peering è necessario che lo stato sia abilitato.</span><span class="sxs-lookup"><span data-stu-id="f9289-151">The state must be enabled for you to be able to use the peering.</span></span>

<span data-ttu-id="f9289-152">È importante controllare lo stato della sessione BGP soprattutto per il peering Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f9289-152">It is important to check the BGP session state especially for Microsoft peering.</span></span> <span data-ttu-id="f9289-153">Oltre allo stato di provisioning BGP, esiste un altro stato denominato *prefissi pubblici annunciati*.</span><span class="sxs-lookup"><span data-stu-id="f9289-153">In addition to the BGP provisioning state, there is another state called *advertised public prefixes state*.</span></span> <span data-ttu-id="f9289-154">Per i prefissi pubblici annunciati deve essere impostato lo stato *configured* perché la sessione BGP sia attiva e perché il routing funzioni in modalità end-to-end.</span><span class="sxs-lookup"><span data-stu-id="f9289-154">The advertised public prefixes state must be in *configured* state, both for the BGP session to be up and for your routing to work end-to-end.</span></span> 

<span data-ttu-id="f9289-155">Se invece è impostato lo stato *validation needed* , la sessione BGP non è abilitata, poiché i prefissi annunciati non corrispondono al numero AS nei registri di routing.</span><span class="sxs-lookup"><span data-stu-id="f9289-155">If the advertised public prefix state is set to a *validation needed* state, the BGP session is not enabled, as the advertised prefixes did not match the AS number in any of the routing registries.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f9289-156">Se i prefissi pubblici annunciati sono impostati sullo stato *manual validation* , è necessario aprire un ticket di supporto con il [supporto tecnico Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) e fornire la prova di essere proprietari degli indirizzi IP annunciati insieme con il numero di sistema autonomo (AS) associato.</span><span class="sxs-lookup"><span data-stu-id="f9289-156">If the advertised public prefixes state is in *manual validation* state, you must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and provide evidence that you own the IP addresses advertised along with the associated Autonomous System number.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f9289-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f9289-157">Next steps</span></span>
* <span data-ttu-id="f9289-158">Configurare la connessione ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f9289-158">Configure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="f9289-159">Creare un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f9289-159">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-arm.md)
  * [<span data-ttu-id="f9289-160">Configurare il routing</span><span class="sxs-lookup"><span data-stu-id="f9289-160">Configure routing</span></span>](expressroute-howto-routing-arm.md)
  * [<span data-ttu-id="f9289-161">Collegare una rete virtuale a un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="f9289-161">Link a VNet to an ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

