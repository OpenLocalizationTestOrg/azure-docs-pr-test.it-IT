---
title: 'Creare e modificare un circuito ExpressRoute: Portale di Azure| Microsoft Docs'
description: In questo articolo viene descritto come toocreate, eseguire il provisioning, verificare, aggiornare, eliminare e il deprovisioning di un circuito ExpressRoute.
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a><span data-ttu-id="3955e-103">Creare e modificare un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3955e-103">Create and modify an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3955e-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3955e-104">Azure portal</span></span>](expressroute-howto-circuit-portal-resource-manager.md)
> * [<span data-ttu-id="3955e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3955e-105">PowerShell</span></span>](expressroute-howto-circuit-arm.md)
> * [<span data-ttu-id="3955e-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="3955e-106">Azure CLI</span></span>](howto-circuit-cli.md)
> * [<span data-ttu-id="3955e-107">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3955e-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [<span data-ttu-id="3955e-108">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="3955e-108">PowerShell (classic)</span></span>](expressroute-howto-circuit-classic.md)
>

<span data-ttu-id="3955e-109">In questo articolo viene descritto come toocreate un circuito ExpressRoute di Azure tramite hello Azure portal e hello Azure Resource Manager modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3955e-109">This article describes how toocreate an Azure ExpressRoute circuit by using hello Azure portal and hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="3955e-110">Hello anche passaggi Mostra come lo stato di hello toocheck del circuito di hello, aggiornarla, o eliminare e deprovisioning.</span><span class="sxs-lookup"><span data-stu-id="3955e-110">hello following steps also show you how toocheck hello status of hello circuit, update it, or delete and deprovision it.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="3955e-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="3955e-111">Before you begin</span></span>
* <span data-ttu-id="3955e-112">Hello revisione [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="3955e-112">Review hello [prerequisites](expressroute-prerequisites.md) and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="3955e-113">Assicurarsi di disporre di accesso toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3955e-113">Ensure that you have access toohello [Azure portal](https://portal.azure.com).</span></span>
* <span data-ttu-id="3955e-114">Assicurarsi di disporre delle autorizzazioni toocreate nuova le risorse di rete.</span><span class="sxs-lookup"><span data-stu-id="3955e-114">Ensure that you have permissions toocreate new networking resources.</span></span> <span data-ttu-id="3955e-115">Se non si dispone delle autorizzazioni appropriate di hello, contattare l'amministratore dell'account.</span><span class="sxs-lookup"><span data-stu-id="3955e-115">Contact your account administrator if you do not have hello right permissions.</span></span>
* <span data-ttu-id="3955e-116">È possibile [visualizzare un video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) prima di iniziare, in ordine toobetter comprendere i passaggi di hello.</span><span class="sxs-lookup"><span data-stu-id="3955e-116">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) before beginning in order toobetter understand hello steps.</span></span>

## <a name="create-and-provision-an-expressroute-circuit"></a><span data-ttu-id="3955e-117">Creare un circuito ExpressRoute ed eseguirne il provisioning</span><span class="sxs-lookup"><span data-stu-id="3955e-117">Create and provision an ExpressRoute circuit</span></span>
### <a name="1-sign-in-toohello-azure-portal"></a><span data-ttu-id="3955e-118">1. Accedi toohello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3955e-118">1. Sign in toohello Azure portal</span></span>
<span data-ttu-id="3955e-119">Da un browser, passare toohello [portale di Azure](http://portal.azure.com) e accedere con l'account di Azure.</span><span class="sxs-lookup"><span data-stu-id="3955e-119">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="2-create-a-new-expressroute-circuit"></a><span data-ttu-id="3955e-120">2. Creare un nuovo circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3955e-120">2. Create a new ExpressRoute circuit</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3955e-121">Dal momento hello che viene eseguita una chiave del servizio verrà addebitato il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3955e-121">Your ExpressRoute circuit will be billed from hello moment a service key is issued.</span></span> <span data-ttu-id="3955e-122">Assicurarsi di eseguire questa operazione quando il provider di connettività hello è circuito hello tooprovision pronto.</span><span class="sxs-lookup"><span data-stu-id="3955e-122">Ensure that you perform this operation when hello connectivity provider is ready tooprovision hello circuit.</span></span>
> 
> 

1. <span data-ttu-id="3955e-123">È possibile creare un circuito ExpressRoute selezionando hello opzione toocreate una nuova risorsa.</span><span class="sxs-lookup"><span data-stu-id="3955e-123">You can create an ExpressRoute circuit by selecting hello option toocreate a new resource.</span></span> <span data-ttu-id="3955e-124">Fare clic su **New** > **rete** > **ExpressRoute**, come illustrato nella seguente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="3955e-124">Click **New** > **Networking** > **ExpressRoute**, as shown in hello following image:</span></span>
   
    ![Creare un circuito ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. <span data-ttu-id="3955e-126">Dopo aver fatto clic **ExpressRoute**, si noterà hello **circuito ExpressRoute creare** blade.</span><span class="sxs-lookup"><span data-stu-id="3955e-126">After you click **ExpressRoute**, you'll see hello **Create ExpressRoute circuit** blade.</span></span> <span data-ttu-id="3955e-127">Quando sta inserimento dei valori hello in questo pannello, assicurarsi di specificare hello corretto dello SKU e misurazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="3955e-127">When you're filling in hello values on this blade, make sure that you specify hello correct SKU tier and data metering.</span></span>
   
   * <span data-ttu-id="3955e-128">**livello** determina se è abilitato un componente aggiuntivo ExpressRoute Standard o ExpressRoute Premium.</span><span class="sxs-lookup"><span data-stu-id="3955e-128">**Tier** determines whether an ExpressRoute standard or an ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="3955e-129">È possibile specificare **Standard** tooget hello SKU standard o **Premium** per il componente aggiuntivo di hello premium.</span><span class="sxs-lookup"><span data-stu-id="3955e-129">You can specify **Standard** tooget hello standard SKU or **Premium** for hello premium add-on.</span></span>
   * <span data-ttu-id="3955e-130">**Misurazione dei dati** determina tipo fatturazione hello.</span><span class="sxs-lookup"><span data-stu-id="3955e-130">**Data metering** determines hello billing type.</span></span> <span data-ttu-id="3955e-131">È possibile specificare **A consumo** per un piano dati a consumo e **Senza limiti** per un piano dati illimitato.</span><span class="sxs-lookup"><span data-stu-id="3955e-131">You can specify **Metered** for a metered data plan and **Unlimited** for an unlimited data plan.</span></span> <span data-ttu-id="3955e-132">Si noti che è possibile modificare il tipo fatturazione di hello da **Metered** troppo**Unlimited**, ma è possibile modificare il tipo di hello da **Unlimited** troppo**Metered**.</span><span class="sxs-lookup"><span data-stu-id="3955e-132">Note that you can change hello billing type from **Metered** too**Unlimited**, but you can't change hello type from **Unlimited** too**Metered**.</span></span>
     
     ![Configurare il livello SKU hello e misurazione dei dati](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> <span data-ttu-id="3955e-134">Tenere presente che il percorso di Peering hello indica hello [posizione fisica](expressroute-locations.md) in cui sono peering con Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3955e-134">Please be aware that hello Peering Location indicates hello [physical location](expressroute-locations.md) where you are peering with Microsoft.</span></span> <span data-ttu-id="3955e-135">Si tratta di **non** collegato troppo proprietà "Location", che fa riferimento geography toohello hello Provider di risorse di rete di Azure in cui si trova.</span><span class="sxs-lookup"><span data-stu-id="3955e-135">This is **not** linked too"Location" property, which refers toohello geography where hello Azure Network Resource Provider is located.</span></span> <span data-ttu-id="3955e-136">Non sono correlate, ma è toochoose una buona norma un toohello geograficamente chiudere il percorso di Peering del circuito hello di Provider di risorse di rete.</span><span class="sxs-lookup"><span data-stu-id="3955e-136">While they are not related, it is a good practice toochoose a Network Resource Provider geographically close toohello Peering Location of hello circuit.</span></span> 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a><span data-ttu-id="3955e-137">3. Visualizzazione hello circuiti e proprietà</span><span class="sxs-lookup"><span data-stu-id="3955e-137">3. View hello circuits and properties</span></span>
<span data-ttu-id="3955e-138">**Consente di visualizzare tutti i circuiti hello**</span><span class="sxs-lookup"><span data-stu-id="3955e-138">**View all hello circuits**</span></span>

<span data-ttu-id="3955e-139">È possibile visualizzare tutti i circuiti hello creato selezionando **tutte le risorse** dal menu a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="3955e-139">You can view all hello circuits that you created by selecting **All resources** on hello left-side menu.</span></span>

![Visualizzazione dei circuiti](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

<span data-ttu-id="3955e-141">**Visualizzare le proprietà di hello**</span><span class="sxs-lookup"><span data-stu-id="3955e-141">**View hello properties**</span></span>

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Visualizza proprietà](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a><span data-ttu-id="3955e-143">4. Inviare i provider di connettività di hello servizio tooyour chiave per il provisioning</span><span class="sxs-lookup"><span data-stu-id="3955e-143">4. Send hello service key tooyour connectivity provider for provisioning</span></span>
<span data-ttu-id="3955e-144">In questo pannello, **stato Provider** fornisce informazioni sullo stato corrente di hello di provisioning sul lato di provider di servizi di hello.</span><span class="sxs-lookup"><span data-stu-id="3955e-144">On this blade, **Provider status** provides information on hello current state of provisioning on hello service-provider side.</span></span> <span data-ttu-id="3955e-145">**Stato circuit** fornisce lo stato di hello in hello lato Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3955e-145">**Circuit status** provides hello state on hello Microsoft side.</span></span> <span data-ttu-id="3955e-146">Per ulteriori informazioni sul provisioning stati circuito, vedere hello [flussi di lavoro](expressroute-workflows.md#expressroute-circuit-provisioning-states) articolo.</span><span class="sxs-lookup"><span data-stu-id="3955e-146">For more information about circuit provisioning states, see hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) article.</span></span>

<span data-ttu-id="3955e-147">Quando si crea un nuovo circuito ExpressRoute, circuito hello sarà nel seguente stato hello:</span><span class="sxs-lookup"><span data-stu-id="3955e-147">When you create a new ExpressRoute circuit, hello circuit will be in hello following state:</span></span>

<span data-ttu-id="3955e-148">Stato provider: Senza provisioning</span><span class="sxs-lookup"><span data-stu-id="3955e-148">Provider status: Not provisioned</span></span><BR>
<span data-ttu-id="3955e-149"> Stato circuito: Abilitato</span><span class="sxs-lookup"><span data-stu-id="3955e-149">Circuit status: Enabled</span></span>

![Avvio del processo di provisioning](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

<span data-ttu-id="3955e-151">circuito Hello cambierà toohello seguente lo stato quando il provider di connettività hello è in corso di hello di abilitarlo per l'utente:</span><span class="sxs-lookup"><span data-stu-id="3955e-151">hello circuit will change toohello following state when hello connectivity provider is in hello process of enabling it for you:</span></span>

<span data-ttu-id="3955e-152">Stato provider: Provisioning in corso</span><span class="sxs-lookup"><span data-stu-id="3955e-152">Provider status: Provisioning</span></span><BR>
<span data-ttu-id="3955e-153"> Stato circuito: Abilitato</span><span class="sxs-lookup"><span data-stu-id="3955e-153">Circuit status: Enabled</span></span>

<span data-ttu-id="3955e-154">Per è toobe in grado di toouse un circuito ExpressRoute, deve essere nel seguente stato hello:</span><span class="sxs-lookup"><span data-stu-id="3955e-154">For you toobe able toouse an ExpressRoute circuit, it must be in hello following state:</span></span>

<span data-ttu-id="3955e-155">Stato provider: Provisioning eseguito</span><span class="sxs-lookup"><span data-stu-id="3955e-155">Provider status: Provisioned</span></span><BR>
<span data-ttu-id="3955e-156"> Stato circuito: Abilitato</span><span class="sxs-lookup"><span data-stu-id="3955e-156">Circuit status: Enabled</span></span>

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a><span data-ttu-id="3955e-157">5. Controllare periodicamente hello stato della chiave circuito hello e hello</span><span class="sxs-lookup"><span data-stu-id="3955e-157">5. Periodically check hello status and hello state of hello circuit key</span></span>
<span data-ttu-id="3955e-158">È possibile visualizzare le proprietà di hello del circuito hello che è interessati a selezionandolo.</span><span class="sxs-lookup"><span data-stu-id="3955e-158">You can view hello properties of hello circuit that you're interested in by selecting it.</span></span> <span data-ttu-id="3955e-159">Controllare hello **stato Provider** e assicurarsi che siano spostati troppo**provisioning eseguito** prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="3955e-159">Check hello **Provider status** and ensure that it has moved too**Provisioned** before you continue.</span></span>

![Stato del circuito e del provider](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a><span data-ttu-id="3955e-161">6. Creare la configurazione di routing</span><span class="sxs-lookup"><span data-stu-id="3955e-161">6. Create your routing configuration</span></span>
<span data-ttu-id="3955e-162">Per istruzioni dettagliate, vedere toohello [configurazione del routing circuito ExpressRoute](expressroute-howto-routing-portal-resource-manager.md) toocreate dell'articolo e modificare peering di circuito.</span><span class="sxs-lookup"><span data-stu-id="3955e-162">For step-by-step instructions, refer toohello [ExpressRoute circuit routing configuration](expressroute-howto-routing-portal-resource-manager.md) article toocreate and modify circuit peerings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3955e-163">Queste istruzioni si applicano solo toocircuits creati con i provider di servizi che offrono servizi di livello 2 di connettività.</span><span class="sxs-lookup"><span data-stu-id="3955e-163">These instructions only apply toocircuits that are created with service providers that offer layer 2 connectivity services.</span></span> <span data-ttu-id="3955e-164">Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito un IP VPN, come MPLS), il provider di connettività configurerà e gestirà il routing per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="3955e-164">If you're using a service provider that offers managed layer 3 services (typically an IP VPN, like MPLS), your connectivity provider will configure and manage routing for you.</span></span>
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="3955e-165">7. Collegare un circuito ExpressRoute di tooan rete virtuale</span><span class="sxs-lookup"><span data-stu-id="3955e-165">7. Link a virtual network tooan ExpressRoute circuit</span></span>
<span data-ttu-id="3955e-166">Successivamente, collegare un circuito ExpressRoute di tooyour rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="3955e-166">Next, link a virtual network tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="3955e-167">Hello utilizzare [collegamento virtuale reti circuiti tooExpressRoute](expressroute-howto-linkvnet-arm.md) articolo quando si lavora con modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="3955e-167">Use hello [Linking virtual networks tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article when you work with hello Resource Manager deployment model.</span></span>

## <a name="getting-hello-status-of-an-expressroute-circuit"></a><span data-ttu-id="3955e-168">Ottenere lo stato di hello di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3955e-168">Getting hello status of an ExpressRoute circuit</span></span>
<span data-ttu-id="3955e-169">È possibile visualizzare lo stato di hello di un circuito, selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="3955e-169">You can view hello status of a circuit by selecting it.</span></span> 

![Stato di un circuito ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a><span data-ttu-id="3955e-171">Modifica di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3955e-171">Modifying an ExpressRoute circuit</span></span>
<span data-ttu-id="3955e-172">È possibile modificare determinate proprietà di un circuito ExpressRoute senza conseguenze per la connettività.</span><span class="sxs-lookup"><span data-stu-id="3955e-172">You can modify certain properties of an ExpressRoute circuit without impacting connectivity.</span></span>

<span data-ttu-id="3955e-173">È possibile eseguire hello seguenti senza tempi di inattività:</span><span class="sxs-lookup"><span data-stu-id="3955e-173">You can do hello following with no downtime:</span></span>

* <span data-ttu-id="3955e-174">Abilitare o disabilitare un componente aggiuntivo ExpressRoute Premium per il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3955e-174">Enable or disable an ExpressRoute premium add-on for your ExpressRoute circuit.</span></span>
* <span data-ttu-id="3955e-175">Aumento della larghezza di banda hello del circuito ExpressRoute fornito è la capacità disponibile sulla porta hello.</span><span class="sxs-lookup"><span data-stu-id="3955e-175">Increase hello bandwidth of your ExpressRoute circuit provided there is capacity available on hello port.</span></span> <span data-ttu-id="3955e-176">Si noti che il downgrade della larghezza di banda hello di un circuito non è supportato.</span><span class="sxs-lookup"><span data-stu-id="3955e-176">Note that downgrading hello bandwidth of a circuit is not supported.</span></span> 
* <span data-ttu-id="3955e-177">Modificare hello piano dati a consumo tooUnlimited dati di controllo.</span><span class="sxs-lookup"><span data-stu-id="3955e-177">Change hello metering plan from Metered Data tooUnlimited Data.</span></span> <span data-ttu-id="3955e-178">Si noti tale piano del controllo modifica hello da dati senza limiti tooMetered che dati non è supportata.</span><span class="sxs-lookup"><span data-stu-id="3955e-178">Note that changing hello metering plan from Unlimited Data tooMetered Data is not supported.</span></span>
* <span data-ttu-id="3955e-179">È possibile abilitare e disabilitare l'opzione *Allow Classic Operations*(Consenti operazioni classiche).</span><span class="sxs-lookup"><span data-stu-id="3955e-179">You can enable and disable *Allow Classic Operations*.</span></span>

<span data-ttu-id="3955e-180">Per ulteriori informazioni su limiti e limitazioni, vedere toohello [domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="3955e-180">For more information on limits and limitations, refer toohello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>

<span data-ttu-id="3955e-181">toomodify un circuito ExpressRoute, fare clic su hello **configurazione** come illustrato nella figura che segue hello.</span><span class="sxs-lookup"><span data-stu-id="3955e-181">toomodify an ExpressRoute circuit, click on hello **Configuration** as shown in hello figure below.</span></span>

![Modificare il circuito](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

<span data-ttu-id="3955e-183">È possibile modificare la larghezza di banda hello, SKU, modello di fatturazione e consentire operazioni classiche in Pannello di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="3955e-183">You can modify hello bandwidth, SKU, billing model and allow classic operations within hello configuration blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3955e-184">Potrebbe essere circuito ExpressRoute di hello toorecreate se ha capacità insufficiente sulla porta esistente hello.</span><span class="sxs-lookup"><span data-stu-id="3955e-184">You may have toorecreate hello ExpressRoute circuit if there is inadequate capacity on hello existing port.</span></span> <span data-ttu-id="3955e-185">Se non è presente capacità aggiuntive disponibili in tale posizione non è possibile aggiornare il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="3955e-185">You cannot upgrade hello circuit if there is no additional capacity available at that location.</span></span>
>
> <span data-ttu-id="3955e-186">È possibile ridurre la larghezza di banda hello di un circuito ExpressRoute senza interruzioni.</span><span class="sxs-lookup"><span data-stu-id="3955e-186">You cannot reduce hello bandwidth of an ExpressRoute circuit without disruption.</span></span> <span data-ttu-id="3955e-187">Il downgrade della larghezza di banda è necessario il circuito ExpressRoute toodeprovision hello e quindi ripetere il provisioning di un nuovo circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3955e-187">Downgrading bandwidth requires you toodeprovision hello ExpressRoute circuit and then reprovision a new ExpressRoute circuit.</span></span>
> 
> <span data-ttu-id="3955e-188">Disabilitare il componente aggiuntivo premium operazione può non riuscire se si utilizza le risorse che sono maggiori di ciò che è consentito per il circuito standard hello.</span><span class="sxs-lookup"><span data-stu-id="3955e-188">Disable premium add-on operation can fail if you're using resources that are greater than what is permitted for hello standard circuit.</span></span>
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a><span data-ttu-id="3955e-189">Deprovisioning ed eliminazione di un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3955e-189">Deprovisioning and deleting an ExpressRoute circuit</span></span>
<span data-ttu-id="3955e-190">È possibile eliminare il circuito ExpressRoute selezionando hello **eliminare** icona.</span><span class="sxs-lookup"><span data-stu-id="3955e-190">You can delete your ExpressRoute circuit by selecting hello **delete** icon.</span></span> <span data-ttu-id="3955e-191">Si noti hello segue:</span><span class="sxs-lookup"><span data-stu-id="3955e-191">Note hello following:</span></span>

* <span data-ttu-id="3955e-192">È necessario scollegare tutte le reti virtuali da hello circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="3955e-192">You must unlink all virtual networks from hello ExpressRoute circuit.</span></span> <span data-ttu-id="3955e-193">Se questa operazione non riesce, controllare se le reti virtuali sono collegate toohello circuito.</span><span class="sxs-lookup"><span data-stu-id="3955e-193">If this operation fails, check whether any virtual networks are linked toohello circuit.</span></span>
* <span data-ttu-id="3955e-194">Se il provider del servizio di circuito ExpressRoute di hello lo stato di provisioning **Provisioning** o **provisioning eseguito** è necessario collaborare con il circuito di hello toodeprovision provider del servizio sul relativo lato.</span><span class="sxs-lookup"><span data-stu-id="3955e-194">If hello ExpressRoute circuit service provider provisioning state is **Provisioning** or **Provisioned** you must work with your service provider toodeprovision hello circuit on their side.</span></span> <span data-ttu-id="3955e-195">Si continuerà tooreserve risorse e a pagamento fino a quando il provider di servizi di hello completa deprovisioning circuito hello e invia una notifica di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3955e-195">We will continue tooreserve resources and bill you until hello service provider completes deprovisioning hello circuit and notifies us.</span></span>
* <span data-ttu-id="3955e-196">Se il provider di servizi di hello è deprovisioning circuito hello (provider di servizi di hello lo stato di provisioning è stato impostato troppo**non è stato eseguito il provisioning**) è possibile eliminare il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="3955e-196">If hello service provider has deprovisioned hello circuit (hello service provider provisioning state is set too**Not provisioned**) you can then delete hello circuit.</span></span> <span data-ttu-id="3955e-197">Questa operazione arresterà la fatturazione per il circuito hello</span><span class="sxs-lookup"><span data-stu-id="3955e-197">This will stop billing for hello circuit</span></span>

## <a name="next-steps"></a><span data-ttu-id="3955e-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3955e-198">Next steps</span></span>
<span data-ttu-id="3955e-199">Dopo aver creato il circuito, verificare che hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="3955e-199">After you create your circuit, make sure that you do hello following:</span></span>

* [<span data-ttu-id="3955e-200">Creare e modificare il routing per un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="3955e-200">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-portal-resource-manager.md)
* [<span data-ttu-id="3955e-201">Collegamento del circuito ExpressRoute di tooyour di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="3955e-201">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)

