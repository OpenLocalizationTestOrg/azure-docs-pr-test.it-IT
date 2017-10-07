---
title: 'Collegare un circuito ExpressRoute di tooan rete virtuale: portale di Azure | Documenti Microsoft'
description: Questo documento viene fornita una panoramica del modo virtuale toolink reti circuiti tooExpressRoute (Vnet).
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="067ec-103">Connettersi a un circuito ExpressRoute di tooan rete virtuale</span><span class="sxs-lookup"><span data-stu-id="067ec-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="067ec-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="067ec-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="067ec-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="067ec-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="067ec-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="067ec-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="067ec-107">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="067ec-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="067ec-108">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="067ec-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="067ec-109">In questo articolo consente di collegare i circuiti ExpressRoute di reti virtuali (Vnet) tooAzure con modello di distribuzione di gestione risorse di hello e hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="067ec-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and hello Azure portal.</span></span> <span data-ttu-id="067ec-110">Reti virtuali possono essere in hello stessa sottoscrizione oppure può essere parte di un'altra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="067ec-110">Virtual networks can either be in hello same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="067ec-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="067ec-111">Before you begin</span></span>
* <span data-ttu-id="067ec-112">Hello revisione [prerequisiti](expressroute-prerequisites.md), [requisiti di routing](expressroute-routing.md), e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="067ec-112">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="067ec-113">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="067ec-113">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="067ec-114">Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e includere circuito hello abilitato dal provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="067ec-114">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have hello circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="067ec-115">Assicurarsi di disporre del peering privato di Azure configurato per il circuito.</span><span class="sxs-lookup"><span data-stu-id="067ec-115">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="067ec-116">Vedere hello [Configura routing](expressroute-howto-routing-portal-resource-manager.md) articolo per le istruzioni di routing.</span><span class="sxs-lookup"><span data-stu-id="067ec-116">See hello [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="067ec-117">Verificare di peering privato di Azure è configurato hello peering BGP tra la rete e Microsoft sia attivo in modo che è possibile abilitare la connettività end-to-end.</span><span class="sxs-lookup"><span data-stu-id="067ec-117">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="067ec-118">Assicurarsi di disporre di una rete virtuale e di un gateway di rete virtuale creati e con provisioning completo.</span><span class="sxs-lookup"><span data-stu-id="067ec-118">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="067ec-119">Seguire le istruzioni di hello troppo[creare un gateway di rete virtuale per ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="067ec-119">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="067ec-120">Un gateway di rete virtuale per ExpressRoute utilizza hello 'ExpressRoute', il tipo di gateway non VPN.</span><span class="sxs-lookup"><span data-stu-id="067ec-120">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="067ec-121">È possibile collegare il circuito ExpressRoute standard di too10 reti virtuali tooa.</span><span class="sxs-lookup"><span data-stu-id="067ec-121">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="067ec-122">Tutte le reti virtuali devono essere in hello stessa regione di natura geopolitica quando si utilizza un circuito ExpressRoute standard.</span><span class="sxs-lookup"><span data-stu-id="067ec-122">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="067ec-123">È possibile collegare una rete virtuale all'esterno di hello geopolitici paese hello circuito ExpressRoute o connettersi a un numero maggiore di reti virtuali tooyour circuito ExpressRoute se è stato abilitato il componente aggiuntivo di hello ExpressRoute premium.</span><span class="sxs-lookup"><span data-stu-id="067ec-123">You can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="067ec-124">Controllare hello [domande frequenti su](expressroute-faqs.md) per ulteriori informazioni sul componente aggiuntivo di hello premium.</span><span class="sxs-lookup"><span data-stu-id="067ec-124">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>
* <span data-ttu-id="067ec-125">È possibile [visualizzare un video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) prima toobetter inizio comprendere i passaggi di hello.</span><span class="sxs-lookup"><span data-stu-id="067ec-125">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning toobetter understand hello steps.</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="067ec-126">Connettere una rete virtuale in hello circuito tooa sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="067ec-126">Connect a virtual network in hello same subscription tooa circuit</span></span>

### <a name="toocreate-a-connection"></a><span data-ttu-id="067ec-127">toocreate una connessione</span><span class="sxs-lookup"><span data-stu-id="067ec-127">toocreate a connection</span></span>

> [!NOTE]
> <span data-ttu-id="067ec-128">Informazioni di configurazione BGP non apparirà se il provider di livello 3 hello configurato il peering.</span><span class="sxs-lookup"><span data-stu-id="067ec-128">BGP configuration information will not show up if hello layer 3 provider configured your peerings.</span></span> <span data-ttu-id="067ec-129">Se il circuito si trova in uno stato di provisioning, dovrebbe essere in grado di toocreate connessioni.</span><span class="sxs-lookup"><span data-stu-id="067ec-129">If your circuit is in a provisioned state, you should be able toocreate connections.</span></span>
>

1. <span data-ttu-id="067ec-130">Verificare che il circuito ExpressRoute e il peering privato di Azure siano configurati correttamente.</span><span class="sxs-lookup"><span data-stu-id="067ec-130">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="067ec-131">Seguire le istruzioni hello [creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md) e [Configura routing](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="067ec-131">Follow hello instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="067ec-132">Il circuito ExpressRoute dovrebbe essere simile hello seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="067ec-132">Your ExpressRoute circuit should look like hello following image:</span></span>

    ![Schermata del circuito ExpressRoute](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="067ec-134">È ora possibile avviare il provisioning del tooyour di gateway di rete virtuale circuito ExpressRoute toolink una connessione.</span><span class="sxs-lookup"><span data-stu-id="067ec-134">You can now start provisioning a connection toolink your virtual network gateway tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="067ec-135">Fare clic su **connessione** > **Aggiungi** tooopen hello **Aggiungi connessione** pannello e quindi configurare i valori hello.</span><span class="sxs-lookup"><span data-stu-id="067ec-135">Click **Connection** > **Add** tooopen hello **Add connection** blade, and then configure hello values.</span></span>

    ![Aggiungere la schermata della connessione](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="067ec-137">Dopo la connessione è stata configurata, l'oggetto di connessione verrà visualizzate informazioni di hello per connessione hello.</span><span class="sxs-lookup"><span data-stu-id="067ec-137">After your connection has been successfully configured, your connection object will show hello information for hello connection.</span></span>

     ![Schermata dell'oggetto connessione](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a><span data-ttu-id="067ec-139">toodelete una connessione</span><span class="sxs-lookup"><span data-stu-id="067ec-139">toodelete a connection</span></span>
<span data-ttu-id="067ec-140">È possibile eliminare una connessione selezionando hello **eliminare** icona nel Pannello di hello per la connessione.</span><span class="sxs-lookup"><span data-stu-id="067ec-140">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="067ec-141">Connettere una rete virtuale in un circuito tooa sottoscrizione diversa</span><span class="sxs-lookup"><span data-stu-id="067ec-141">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="067ec-142">È possibile condividere un circuito ExpressRoute tra più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="067ec-142">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="067ec-143">Figura Hello seguente illustra un semplice schematica del funzionamento della condivisione di circuiti ExpressRoute tra più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="067ec-143">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![Connettività tra sottoscrizioni](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="067ec-145">Ogni cloud più piccoli hello all'interno di cloud di grandi dimensioni hello è toorepresent utilizzate sottoscrizioni appartenenti a reparti toodifferent all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="067ec-145">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span>
- <span data-ttu-id="067ec-146">Ognuno dei reparti hello hello organizzazione può usare la propria sottoscrizione per distribuire i propri servizi, ma queste possono condividere una singola ExpressRoute circuito tooconnect tooyour indietro locale rete.</span><span class="sxs-lookup"><span data-stu-id="067ec-146">Each of hello departments within hello organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span>
- <span data-ttu-id="067ec-147">Un singolo reparto (in questo esempio: IT) può possedere il circuito ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="067ec-147">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="067ec-148">Altre sottoscrizioni all'interno dell'organizzazione hello è possono usare il circuito ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="067ec-148">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="067ec-149">Gli addebiti di connettività e larghezza di banda per il circuito dedicato hello sarà proprietario del circuito ExpressRoute toohello applicato.</span><span class="sxs-lookup"><span data-stu-id="067ec-149">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute circuit owner.</span></span> <span data-ttu-id="067ec-150">Tutte le reti virtuali condividono hello stessa larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="067ec-150">All virtual networks share hello same bandwidth.</span></span>
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="067ec-151">Amministrazione - Proprietari e utenti del circuito</span><span class="sxs-lookup"><span data-stu-id="067ec-151">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="067ec-152">Hello 'proprietario del circuito' è un utente autorizzato di alimentazione di hello risorse circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="067ec-152">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="067ec-153">proprietario del circuito Hello è possibile creare le autorizzazioni che possono essere riscattate 'utenti circuito'.</span><span class="sxs-lookup"><span data-stu-id="067ec-153">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="067ec-154">Gli utenti del circuito sono proprietari della rete virtuale gateway che non sono in hello stessa sottoscrizione come hello circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="067ec-154">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="067ec-155">Gli utenti del circuito possono riscattare le autorizzazioni (un'autorizzazione per ogni rete virtuale).</span><span class="sxs-lookup"><span data-stu-id="067ec-155">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="067ec-156">proprietario del circuito Hello ha hello power toomodify e revocare le autorizzazioni per in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="067ec-156">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="067ec-157">Revoca un risultati di autorizzazione in tutte le connessioni di collegamento viene eliminate dalla sottoscrizione hello il cui accesso è stato revocato.</span><span class="sxs-lookup"><span data-stu-id="067ec-157">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="067ec-158">Operazioni del proprietario del circuito</span><span class="sxs-lookup"><span data-stu-id="067ec-158">Circuit owner operations</span></span>

<span data-ttu-id="067ec-159">**toocreate un'autorizzazione di connessione**</span><span class="sxs-lookup"><span data-stu-id="067ec-159">**toocreate a connection authorization**</span></span>

<span data-ttu-id="067ec-160">proprietario del circuito Hello crea un'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="067ec-160">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="067ec-161">Questo comporta hello creazione di una chiave di autorizzazione che può essere utilizzato da un tooconnect utente circuito loro toohello di gateway di rete virtuale circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="067ec-161">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="067ec-162">Un'autorizzazione è valida per una sola connessione.</span><span class="sxs-lookup"><span data-stu-id="067ec-162">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="067ec-163">Nel Pannello di ExpressRoute hello, fare clic su **autorizzazioni** e quindi digitare un **nome** autorizzazione hello e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="067ec-163">In hello ExpressRoute blade, Click **Authorizations** and then type a **name** for hello authorization and click **Save**.</span></span>

    ![Authorizations](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="067ec-165">Dopo aver salvata la configurazione hello, copiare hello **ID risorsa** hello e **chiave di autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="067ec-165">Once hello configuration is saved, copy hello **Resource ID** and hello **Authorization Key**.</span></span>

    ![Chiave di autorizzazione](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="067ec-167">**toodelete un'autorizzazione di connessione**</span><span class="sxs-lookup"><span data-stu-id="067ec-167">**toodelete a connection authorization**</span></span>

<span data-ttu-id="067ec-168">È possibile eliminare una connessione selezionando hello **eliminare** icona nel Pannello di hello per la connessione.</span><span class="sxs-lookup"><span data-stu-id="067ec-168">You can delete a connection by selecting hello **Delete** icon on hello blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="067ec-169">Operazioni dell'utente del circuito</span><span class="sxs-lookup"><span data-stu-id="067ec-169">Circuit user operations</span></span>

<span data-ttu-id="067ec-170">utente del circuito Hello necessita di ID di risorsa hello e una chiave di autorizzazione dal proprietario del circuito hello.</span><span class="sxs-lookup"><span data-stu-id="067ec-170">hello circuit user needs hello resource ID and an authorization key from hello circuit owner.</span></span> 

<span data-ttu-id="067ec-171">**tooredeem un'autorizzazione di connessione**</span><span class="sxs-lookup"><span data-stu-id="067ec-171">**tooredeem a connection authorization**</span></span>

1.  <span data-ttu-id="067ec-172">Fare clic su hello **+ nuovo** pulsante.</span><span class="sxs-lookup"><span data-stu-id="067ec-172">Click hello **+New** button.</span></span>

    ![Click New](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="067ec-174">Cercare **"Connessione"** hello Marketplace, selezionarla e fare clic su **crea**.</span><span class="sxs-lookup"><span data-stu-id="067ec-174">Search for **"Connection"** in hello Marketplace, select it, and click **Create**.</span></span>

    ![Cercare Connection (Connessione)](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="067ec-176">Verificare che hello **tipo di connessione** è troppo "ExpressRoute".</span><span class="sxs-lookup"><span data-stu-id="067ec-176">Make sure hello **Connection type** is set too"ExpressRoute".</span></span>


4.  <span data-ttu-id="067ec-177">Specificare i dettagli di hello, quindi fare clic su **OK** nel Pannello di hello nozioni di base.</span><span class="sxs-lookup"><span data-stu-id="067ec-177">Fill in hello details, then click **OK** in hello Basics blade.</span></span>

    ![Pannello Nozioni di base](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="067ec-179">In hello **impostazioni** blade, seleziona hello **gateway di rete virtuale** e controllare hello **riscattare autorizzazione** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="067ec-179">In hello **Settings** blade, Select hello **Virtual network gateway** and check hello **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="067ec-180">Immettere hello **chiave di autorizzazione** hello e **Peer circuito URI** e assegnare un nome di connessione hello.</span><span class="sxs-lookup"><span data-stu-id="067ec-180">Enter hello **Authorization key** and hello **Peer circuit URI** and give hello connection a name.</span></span> <span data-ttu-id="067ec-181">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="067ec-181">Click **OK**.</span></span>

    ![Pannello Impostazioni](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="067ec-183">Esaminare le informazioni di hello in hello **riepilogo** pannello e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="067ec-183">Review hello information in hello **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="067ec-184">**toorelease un'autorizzazione di connessione**</span><span class="sxs-lookup"><span data-stu-id="067ec-184">**toorelease a connection authorization**</span></span>

<span data-ttu-id="067ec-185">È possibile rilasciare un'autorizzazione per l'eliminazione hello connessione che si collega una rete virtuale toohello circuito ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="067ec-185">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="067ec-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="067ec-186">Next steps</span></span>
<span data-ttu-id="067ec-187">Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="067ec-187">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
