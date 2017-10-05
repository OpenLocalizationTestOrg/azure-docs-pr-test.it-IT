---
title: Collegare una rete virtuale a un circuito ExpressRoute usando il portale di Azure | Documentazione Microsoft
description: Questo documento fornisce una panoramica delle operazioni per il collegamento di reti virtuali (VNet) a circuiti ExpressRoute.
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
ms.openlocfilehash: 595c30ab5d9adc6061ad753d952adf894ba80b2f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="e1e18-103">Connettere una rete virtuale a un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e1e18-103">Connect a virtual network to an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e1e18-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e1e18-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="e1e18-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e1e18-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="e1e18-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e1e18-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="e1e18-107">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e1e18-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="e1e18-108">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="e1e18-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

<span data-ttu-id="e1e18-109">Questo articolo spiega come collegare le reti virtuali ai circuiti ExpressRoute di Azure usando il modello di distribuzione di Resource Manager e il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e1e18-109">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and the Azure portal.</span></span> <span data-ttu-id="e1e18-110">Le reti virtuali possono trovarsi nella stessa sottoscrizione o appartenere a un'altra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="e1e18-110">Virtual networks can either be in the same subscription, or they can be part of another subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e1e18-111">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e1e18-111">Before you begin</span></span>
* <span data-ttu-id="e1e18-112">Verificare i [prerequisiti](expressroute-prerequisites.md), i [requisiti di routing](expressroute-routing.md) e i [flussi di lavoro](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="e1e18-112">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="e1e18-113">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="e1e18-113">You must have an active ExpressRoute circuit.</span></span>
  
  * <span data-ttu-id="e1e18-114">Seguire le istruzioni per [creare un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e fare in modo che venga abilitato dal provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="e1e18-114">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and have the circuit enabled by your connectivity provider.</span></span>
  * <span data-ttu-id="e1e18-115">Assicurarsi di disporre del peering privato di Azure configurato per il circuito.</span><span class="sxs-lookup"><span data-stu-id="e1e18-115">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="e1e18-116">Vedere l'articolo relativo alla [configurazione del routing](expressroute-howto-routing-portal-resource-manager.md) per istruzioni relative al routing.</span><span class="sxs-lookup"><span data-stu-id="e1e18-116">See the [Configure routing](expressroute-howto-routing-portal-resource-manager.md) article for routing instructions.</span></span>
  * <span data-ttu-id="e1e18-117">Per abilitare la connettività end-to-end è necessario assicurarsi che sia configurato il peering privato di Azure e sia attivo il peering BGP tra la rete e Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e1e18-117">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="e1e18-118">Assicurarsi di disporre di una rete virtuale e di un gateway di rete virtuale creati e con provisioning completo.</span><span class="sxs-lookup"><span data-stu-id="e1e18-118">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="e1e18-119">Seguire le istruzioni per [creare un gateway di rete virtuale per ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e1e18-119">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="e1e18-120">Un gateway di rete virtuale per ExpressRoute usa 'ExpressRoute' come GatewayType, non VPN.</span><span class="sxs-lookup"><span data-stu-id="e1e18-120">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="e1e18-121">È possibile collegare fino a 10 reti virtuali a un circuito ExpressRoute standard.</span><span class="sxs-lookup"><span data-stu-id="e1e18-121">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="e1e18-122">Tutte le reti virtuali devono essere nella stessa area geopolitica quando si usa un circuito ExpressRoute standard.</span><span class="sxs-lookup"><span data-stu-id="e1e18-122">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 
* <span data-ttu-id="e1e18-123">È possibile collegare una rete virtuale esterna all'area geopolitica del circuito ExpressRoute o connettere un numero maggiore di reti virtuali al circuito ExpressRoute se è stato abilitato il componente aggiuntivo ExpressRoute Premium.</span><span class="sxs-lookup"><span data-stu-id="e1e18-123">You can link a virtual network outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="e1e18-124">Per altre informazioni sul componente aggiuntivo Premium, vedere le [domande frequenti](expressroute-faqs.md) .</span><span class="sxs-lookup"><span data-stu-id="e1e18-124">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>
* <span data-ttu-id="e1e18-125">È possibile [visualizzare un video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) prima di iniziare, per comprendere meglio la procedura.</span><span class="sxs-lookup"><span data-stu-id="e1e18-125">You can [view a video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) before beginning to better understand the steps.</span></span>

## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="e1e18-126">Collegare una rete virtuale della stessa sottoscrizione a un circuito</span><span class="sxs-lookup"><span data-stu-id="e1e18-126">Connect a virtual network in the same subscription to a circuit</span></span>

### <a name="to-create-a-connection"></a><span data-ttu-id="e1e18-127">Per creare una connessione</span><span class="sxs-lookup"><span data-stu-id="e1e18-127">To create a connection</span></span>

> [!NOTE]
> <span data-ttu-id="e1e18-128">Le informazioni sulla configurazione BGP non verranno visualizzate se i peering sono stati configurati dal provider di livello 3.</span><span class="sxs-lookup"><span data-stu-id="e1e18-128">BGP configuration information will not show up if the layer 3 provider configured your peerings.</span></span> <span data-ttu-id="e1e18-129">Se è stato eseguito il provisioning del circuito, deve essere possibile creare le connessioni.</span><span class="sxs-lookup"><span data-stu-id="e1e18-129">If your circuit is in a provisioned state, you should be able to create connections.</span></span>
>

1. <span data-ttu-id="e1e18-130">Verificare che il circuito ExpressRoute e il peering privato di Azure siano configurati correttamente.</span><span class="sxs-lookup"><span data-stu-id="e1e18-130">Ensure that your ExpressRoute circuit and Azure private peering have been configured successfully.</span></span> <span data-ttu-id="e1e18-131">Seguire le istruzioni in [Creare e modificare un circuito ExpressRoute](expressroute-howto-circuit-arm.md) e [Creare e modificare il routing per un circuito ExpressRoute](expressroute-howto-routing-arm.md).</span><span class="sxs-lookup"><span data-stu-id="e1e18-131">Follow the instructions in [Create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and [Configure routing](expressroute-howto-routing-arm.md).</span></span> <span data-ttu-id="e1e18-132">Il circuito ExpressRoute deve essere simile a quello della figura seguente:</span><span class="sxs-lookup"><span data-stu-id="e1e18-132">Your ExpressRoute circuit should look like the following image:</span></span>

    ![Schermata del circuito ExpressRoute](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. <span data-ttu-id="e1e18-134">È ora possibile avviare il provisioning di una connessione per collegare il gateway della rete virtuale al circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e1e18-134">You can now start provisioning a connection to link your virtual network gateway to your ExpressRoute circuit.</span></span> <span data-ttu-id="e1e18-135">Fare clic su **Connessione** > **Aggiungi** per aprire il pannello **Aggiungi connessione** e configurare i valori.</span><span class="sxs-lookup"><span data-stu-id="e1e18-135">Click **Connection** > **Add** to open the **Add connection** blade, and then configure the values.</span></span>

    ![Aggiungere la schermata della connessione](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. <span data-ttu-id="e1e18-137">Al termine della configurazione, l'oggetto connessione visualizzerà le informazioni per la connessione.</span><span class="sxs-lookup"><span data-stu-id="e1e18-137">After your connection has been successfully configured, your connection object will show the information for the connection.</span></span>

     ![Schermata dell'oggetto connessione](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="to-delete-a-connection"></a><span data-ttu-id="e1e18-139">Per eliminare una connessione</span><span class="sxs-lookup"><span data-stu-id="e1e18-139">To delete a connection</span></span>
<span data-ttu-id="e1e18-140">È possibile eliminare una connessione selezionando l'icona **Elimina** nel pannello della connessione.</span><span class="sxs-lookup"><span data-stu-id="e1e18-140">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span></span>

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="e1e18-141">Collegare una rete virtuale di un'altra sottoscrizione a un circuito</span><span class="sxs-lookup"><span data-stu-id="e1e18-141">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="e1e18-142">È possibile condividere un circuito ExpressRoute tra più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="e1e18-142">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="e1e18-143">La figura seguente mostra un semplice schema del funzionamento della condivisione di circuiti ExpressRoute tra più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="e1e18-143">The figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

![Connettività tra sottoscrizioni](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- <span data-ttu-id="e1e18-145">Ciascuno dei cloud più piccoli nel cloud di grandi dimensioni viene usato per rappresentare le sottoscrizioni appartenenti a reparti diversi di un'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="e1e18-145">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span>
- <span data-ttu-id="e1e18-146">Ciascun reparto dell'organizzazione può usare la propria sottoscrizione per distribuire i servizi, ma i reparti possono condividere un singolo circuito ExpressRoute per la connessione alla rete locale.</span><span class="sxs-lookup"><span data-stu-id="e1e18-146">Each of the departments within the organization can use their own subscription for deploying their services, but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span>
- <span data-ttu-id="e1e18-147">Un singolo reparto (in questo esempio, IT) può possedere il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e1e18-147">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="e1e18-148">Altre sottoscrizioni all'interno dell'organizzazione possono usare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e1e18-148">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e1e18-149">I costi relativi a connettività e larghezza di banda per il circuito dedicato saranno addebitati al proprietario del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e1e18-149">Connectivity and bandwidth charges for the dedicated circuit will be applied to the ExpressRoute circuit owner.</span></span> <span data-ttu-id="e1e18-150">Tutte le reti virtuali condividono la stessa larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="e1e18-150">All virtual networks share the same bandwidth.</span></span>
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="e1e18-151">Amministrazione - Proprietari e utenti del circuito</span><span class="sxs-lookup"><span data-stu-id="e1e18-151">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="e1e18-152">Il proprietario del circuito è l'utente esperto autorizzato della risorsa circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e1e18-152">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="e1e18-153">Il proprietario del circuito può creare le autorizzazioni che possono essere riscattate dagli "utenti del circuito".</span><span class="sxs-lookup"><span data-stu-id="e1e18-153">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="e1e18-154">Gli utenti del circuito sono i proprietari dei gateway di rete virtuale, che non sono nella stessa sottoscrizione del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e1e18-154">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="e1e18-155">Gli utenti del circuito possono riscattare le autorizzazioni (un'autorizzazione per ogni rete virtuale).</span><span class="sxs-lookup"><span data-stu-id="e1e18-155">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="e1e18-156">Il proprietario del circuito ha la facoltà di modificare e revocare le autorizzazioni in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="e1e18-156">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="e1e18-157">La revoca dell'autorizzazione comporterà l'eliminazione di tutti i collegamenti dalla sottoscrizione di cui è stato revocato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="e1e18-157">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="e1e18-158">Operazioni del proprietario del circuito</span><span class="sxs-lookup"><span data-stu-id="e1e18-158">Circuit owner operations</span></span>

<span data-ttu-id="e1e18-159">**Per creare un'autorizzazione di connessione**</span><span class="sxs-lookup"><span data-stu-id="e1e18-159">**To create a connection authorization**</span></span>

<span data-ttu-id="e1e18-160">Il proprietario del circuito crea un'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="e1e18-160">The circuit owner creates an authorization.</span></span> <span data-ttu-id="e1e18-161">Questo comporta la creazione di una chiave di autorizzazione che può essere utilizzata da un utente del circuito per connettere i gateway di rete virtuale al circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e1e18-161">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="e1e18-162">Un'autorizzazione è valida per una sola connessione.</span><span class="sxs-lookup"><span data-stu-id="e1e18-162">An authorization is valid for only one connection.</span></span>

1. <span data-ttu-id="e1e18-163">Nel pannello di ExpressRoute fare clic su **Authorizations** (Autorizzazioni), digitare un **nome** per l'autorizzazione e fare clic su **Save** (Salva).</span><span class="sxs-lookup"><span data-stu-id="e1e18-163">In the ExpressRoute blade, Click **Authorizations** and then type a **name** for the authorization and click **Save**.</span></span>

    ![Authorizations](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. <span data-ttu-id="e1e18-165">Dopo che la configurazione è stata salvata, copiare l'**ID risorsa** e la **chiave di autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="e1e18-165">Once the configuration is saved, copy the **Resource ID** and the **Authorization Key**.</span></span>

    ![Chiave di autorizzazione](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

<span data-ttu-id="e1e18-167">**Per eliminare un'autorizzazione di connessione**</span><span class="sxs-lookup"><span data-stu-id="e1e18-167">**To delete a connection authorization**</span></span>

<span data-ttu-id="e1e18-168">È possibile eliminare una connessione selezionando l'icona **Elimina** nel pannello della connessione.</span><span class="sxs-lookup"><span data-stu-id="e1e18-168">You can delete a connection by selecting the **Delete** icon on the blade for your connection.</span></span>

### <a name="circuit-user-operations"></a><span data-ttu-id="e1e18-169">Operazioni dell'utente del circuito</span><span class="sxs-lookup"><span data-stu-id="e1e18-169">Circuit user operations</span></span>

<span data-ttu-id="e1e18-170">L'utente del circuito deve richiedere l'ID risorsa e una chiave di autorizzazione al proprietario del circuito.</span><span class="sxs-lookup"><span data-stu-id="e1e18-170">The circuit user needs the resource ID and an authorization key from the circuit owner.</span></span> 

<span data-ttu-id="e1e18-171">**Per riscattare un'autorizzazione di connessione**</span><span class="sxs-lookup"><span data-stu-id="e1e18-171">**To redeem a connection authorization**</span></span>

1.  <span data-ttu-id="e1e18-172">Fare clic sul pulsante **+ New** (Nuovo).</span><span class="sxs-lookup"><span data-stu-id="e1e18-172">Click the **+New** button.</span></span>

    ![Click New](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  <span data-ttu-id="e1e18-174">Cercare **"Connection"** (Connessione) in Marketplace, selezionare l'opzione e fare clic **Create** (Crea).</span><span class="sxs-lookup"><span data-stu-id="e1e18-174">Search for **"Connection"** in the Marketplace, select it, and click **Create**.</span></span>

    ![Cercare Connection (Connessione)](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  <span data-ttu-id="e1e18-176">Verificare che **Connection type** (Tipo di connessione) sia impostato su "ExpressRoute".</span><span class="sxs-lookup"><span data-stu-id="e1e18-176">Make sure the **Connection type** is set to "ExpressRoute".</span></span>


4.  <span data-ttu-id="e1e18-177">Inserire i dettagli e fare clic su **OK** nel pannello Basics (Nozioni di base).</span><span class="sxs-lookup"><span data-stu-id="e1e18-177">Fill in the details, then click **OK** in the Basics blade.</span></span>

    ![Pannello Nozioni di base](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  <span data-ttu-id="e1e18-179">Nel pannello **Settings** (Impostazioni) selezionare **Virtual network gateway** (Gateway di rete virtuale) e selezionare la casella di controllo **Redeem authorization** (Riscatta autorizzazione).</span><span class="sxs-lookup"><span data-stu-id="e1e18-179">In the **Settings** blade, Select the **Virtual network gateway** and check the **Redeem authorization** check box.</span></span>

6.  <span data-ttu-id="e1e18-180">Immettere i valori nei campi **Authorization key** (Chiave di autorizzazione) e **Peer circuit URI** (URI circuito peer) e assegnare un nome di connessione.</span><span class="sxs-lookup"><span data-stu-id="e1e18-180">Enter the **Authorization key** and the **Peer circuit URI** and give the connection a name.</span></span> <span data-ttu-id="e1e18-181">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1e18-181">Click **OK**.</span></span>

    ![Pannello Impostazioni](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. <span data-ttu-id="e1e18-183">Verificare le informazioni nel pannello **Summary** (Riepilogo) e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e1e18-183">Review the information in the **Summary** blade and click **OK**.</span></span>


<span data-ttu-id="e1e18-184">**Per rilasciare un'autorizzazione di connessione**</span><span class="sxs-lookup"><span data-stu-id="e1e18-184">**To release a connection authorization**</span></span>

<span data-ttu-id="e1e18-185">È possibile rilasciare un'autorizzazione eliminando il collegamento del circuito ExpressRoute alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e1e18-185">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1e18-186">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e1e18-186">Next steps</span></span>
<span data-ttu-id="e1e18-187">Per altre informazioni su ExpressRoute, vedere le [Domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="e1e18-187">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
