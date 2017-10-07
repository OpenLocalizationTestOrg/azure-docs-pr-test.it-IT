---
title: 'Collegare un circuito ExpressRoute di tooan rete virtuale: CLI: Azure | Documenti Microsoft'
description: Questo documento viene fornita una panoramica del modo virtuale toolink reti circuiti tooExpressRoute (Vnet) con modello di distribuzione di gestione risorse di hello e CLI.
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a><span data-ttu-id="a93df-103">Connettersi a un circuito ExpressRoute tooan di rete virtuale utilizzando l'interfaccia CLI</span><span class="sxs-lookup"><span data-stu-id="a93df-103">Connect a virtual network tooan ExpressRoute circuit using CLI</span></span>

<span data-ttu-id="a93df-104">In questo articolo consente di collegare i circuiti ExpressRoute di reti virtuali (Vnet) tooAzure utilizzando CLI.</span><span class="sxs-lookup"><span data-stu-id="a93df-104">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits using CLI.</span></span> <span data-ttu-id="a93df-105">toolink mediante Azure CLI, le reti virtuali hello devono essere create usando il modello di distribuzione del hello Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="a93df-105">toolink using Azure CLI, hello virtual networks must be created using hello Resource Manager deployment model.</span></span> <span data-ttu-id="a93df-106">Può essere in hello stessa sottoscrizione o parte di un'altra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="a93df-106">They can either be in hello same subscription, or part of another subscription.</span></span> <span data-ttu-id="a93df-107">Se si desidera toouse tooconnect un metodo diverso del circuito ExpressRoute di tooan di rete virtuale, è possibile selezionare un articolo da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="a93df-107">If you want toouse a different method tooconnect your VNet tooan ExpressRoute circuit, you can select an article from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a93df-108">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a93df-108">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="a93df-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a93df-109">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="a93df-110">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a93df-110">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="a93df-111">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a93df-111">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="a93df-112">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="a93df-112">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a><span data-ttu-id="a93df-113">Prerequisiti di configurazione</span><span class="sxs-lookup"><span data-stu-id="a93df-113">Configuration prerequisites</span></span>

* <span data-ttu-id="a93df-114">È necessario l'ultima versione di hello dell'interfaccia della riga di comando hello (CLI).</span><span class="sxs-lookup"><span data-stu-id="a93df-114">You need hello latest version of hello command-line interface (CLI).</span></span> <span data-ttu-id="a93df-115">Per altre informazioni, vedere [Installare l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a93df-115">For more information, see [Install Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="a93df-116">È necessario hello tooreview [prerequisiti](expressroute-prerequisites.md), [requisiti di routing](expressroute-routing.md), e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="a93df-116">You need tooreview hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="a93df-117">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="a93df-117">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="a93df-118">Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](howto-circuit-cli.md) e includere circuito hello abilitato dal provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="a93df-118">Follow hello instructions too[create an ExpressRoute circuit](howto-circuit-cli.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="a93df-119">Assicurarsi di disporre del peering privato di Azure configurato per il circuito.</span><span class="sxs-lookup"><span data-stu-id="a93df-119">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="a93df-120">Vedere hello [configurare il routing](howto-routing-cli.md) articolo per le istruzioni di routing.</span><span class="sxs-lookup"><span data-stu-id="a93df-120">See hello [configure routing](howto-routing-cli.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="a93df-121">Verificare che il peering privato di Azure sia configurato.</span><span class="sxs-lookup"><span data-stu-id="a93df-121">Ensure that Azure private peering is configured.</span></span> <span data-ttu-id="a93df-122">il peering BGP Hello tra la rete e Microsoft deve essere backup in modo che è possibile abilitare la connettività end-to-end.</span><span class="sxs-lookup"><span data-stu-id="a93df-122">hello BGP peering between your network and Microsoft must be up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="a93df-123">Assicurarsi di disporre di una rete virtuale e di un gateway di rete virtuale creati e con provisioning completo.</span><span class="sxs-lookup"><span data-stu-id="a93df-123">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="a93df-124">Seguire le istruzioni di hello troppo[configurare un gateway di rete virtuale per ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span><span class="sxs-lookup"><span data-stu-id="a93df-124">Follow hello instructions too[Configure a virtual network gateway for ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli).</span></span> <span data-ttu-id="a93df-125">Toouse assicurarsi di essere `--gateway-type ExpressRoute`.</span><span class="sxs-lookup"><span data-stu-id="a93df-125">Be sure toouse `--gateway-type ExpressRoute`.</span></span>

* <span data-ttu-id="a93df-126">È possibile collegare il circuito ExpressRoute standard di too10 reti virtuali tooa.</span><span class="sxs-lookup"><span data-stu-id="a93df-126">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="a93df-127">Tutte le reti virtuali devono essere in hello stessa regione di natura geopolitica quando si utilizza un circuito ExpressRoute standard.</span><span class="sxs-lookup"><span data-stu-id="a93df-127">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="a93df-128">Se si abilita il componente aggiuntivo di hello ExpressRoute premium, è possibile collegare una rete virtuale all'esterno di hello geopolitici paese hello circuito ExpressRoute o connettersi a un numero maggiore di reti virtuali tooyour circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a93df-128">If you enable hello ExpressRoute premium add-on, you can link a virtual network outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit.</span></span> <span data-ttu-id="a93df-129">Per ulteriori informazioni sul componente aggiuntivo di hello premium, vedere hello [domande frequenti su](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="a93df-129">For more information about hello premium add-on, see hello [FAQ](expressroute-faqs.md).</span></span>

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="a93df-130">Connettere una rete virtuale in hello circuito tooa sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="a93df-130">Connect a virtual network in hello same subscription tooa circuit</span></span>

<span data-ttu-id="a93df-131">È possibile connettersi a un circuito ExpressRoute tooan di rete virtuale gateway utilizzando l'esempio hello.</span><span class="sxs-lookup"><span data-stu-id="a93df-131">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello example.</span></span> <span data-ttu-id="a93df-132">Verificare che tale gateway di rete virtuale hello viene creato ed è pronto per il collegamento prima di eseguire il comando hello.</span><span class="sxs-lookup"><span data-stu-id="a93df-132">Make sure that hello virtual network gateway is created and is ready for linking before you run hello command.</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="a93df-133">Connettere una rete virtuale in un circuito tooa sottoscrizione diversa</span><span class="sxs-lookup"><span data-stu-id="a93df-133">Connect a virtual network in a different subscription tooa circuit</span></span>

<span data-ttu-id="a93df-134">È possibile condividere un circuito ExpressRoute tra più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="a93df-134">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="a93df-135">Figura Hello seguente illustra un semplice schematica del funzionamento della condivisione di circuiti ExpressRoute tra più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="a93df-135">hello figure below shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="a93df-136">Ogni cloud più piccoli hello all'interno di cloud di grandi dimensioni hello è toorepresent utilizzate sottoscrizioni appartenenti a reparti toodifferent all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="a93df-136">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="a93df-137">Ognuno dei reparti hello hello organizzazione può usare la propria sottoscrizione per la distribuzione i propri servizi, ma possono condividere ExpressRoute circuito tooconnect tooyour indietro locale reti.</span><span class="sxs-lookup"><span data-stu-id="a93df-137">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="a93df-138">Un singolo reparto (in questo esempio: IT) può possedere il circuito ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="a93df-138">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="a93df-139">Altre sottoscrizioni all'interno dell'organizzazione hello è possono usare il circuito ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="a93df-139">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="a93df-140">Le spese di connettività e larghezza di banda per il circuito dedicato hello verranno applicato toohello proprietario del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a93df-140">Connectivity and bandwidth charges for hello dedicated circuit will be applied toohello ExpressRoute Circuit Owner.</span></span> <span data-ttu-id="a93df-141">Tutte le reti virtuali condividono hello stessa larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="a93df-141">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Connettività tra sottoscrizioni](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="a93df-143">Amministrazione: proprietari e utenti del circuito</span><span class="sxs-lookup"><span data-stu-id="a93df-143">Administration - Circuit Owners and Circuit Users</span></span>

<span data-ttu-id="a93df-144">Hello 'Proprietario del circuito' è un utente autorizzato di alimentazione di hello risorse circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a93df-144">hello 'Circuit Owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="a93df-145">Proprietario del circuito Hello è possibile creare le autorizzazioni che possono essere riscattate da 'Circuito Users'.</span><span class="sxs-lookup"><span data-stu-id="a93df-145">hello Circuit Owner can create authorizations that can be redeemed by 'Circuit Users'.</span></span> <span data-ttu-id="a93df-146">Gli utenti del circuito sono proprietari della rete virtuale gateway che non sono in hello stessa sottoscrizione come hello circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a93df-146">Circuit Users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="a93df-147">Gli utenti del circuito possono riscattare le autorizzazioni, una per ogni rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="a93df-147">Circuit Users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="a93df-148">Proprietario del circuito Hello è hello power toomodify e revocare le autorizzazioni per in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="a93df-148">hello Circuit Owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="a93df-149">Quando l'autorizzazione viene revocata, tutte le connessioni di collegamento vengono eliminate dalla sottoscrizione hello il cui accesso è stato revocato.</span><span class="sxs-lookup"><span data-stu-id="a93df-149">When an authorization is revoked, all link connections are deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="a93df-150">Operazioni del proprietario del circuito</span><span class="sxs-lookup"><span data-stu-id="a93df-150">Circuit Owner operations</span></span>

<span data-ttu-id="a93df-151">**toocreate un'autorizzazione**</span><span class="sxs-lookup"><span data-stu-id="a93df-151">**toocreate an authorization**</span></span>

<span data-ttu-id="a93df-152">Proprietario del circuito Hello crea un'autorizzazione, che consente di creare una chiave di autorizzazione che può essere utilizzato da un utente del circuito di tooconnect loro toohello di gateway di rete virtuale circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="a93df-152">hello Circuit Owner creates an authorization, which creates an authorization key that can be used by a Circuit User tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="a93df-153">Un'autorizzazione è valida per una sola connessione.</span><span class="sxs-lookup"><span data-stu-id="a93df-153">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="a93df-154">Hello seguente esempio viene illustrato come toocreate un'autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="a93df-154">hello following example shows how toocreate an authorization:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

<span data-ttu-id="a93df-155">risposta Hello contiene lo stato e la chiave di autorizzazione hello:</span><span class="sxs-lookup"><span data-stu-id="a93df-155">hello response contains hello authorization key and status:</span></span>

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

<span data-ttu-id="a93df-156">**autorizzazioni tooreview**</span><span class="sxs-lookup"><span data-stu-id="a93df-156">**tooreview authorizations**</span></span>

<span data-ttu-id="a93df-157">Hello proprietario del circuito può esaminare tutte le autorizzazioni che vengono eseguite su un particolare circuito eseguendo hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="a93df-157">hello Circuit Owner can review all authorizations that are issued on a particular circuit by running hello following example:</span></span>

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

<span data-ttu-id="a93df-158">**autorizzazioni tooadd**</span><span class="sxs-lookup"><span data-stu-id="a93df-158">**tooadd authorizations**</span></span>

<span data-ttu-id="a93df-159">Proprietario del circuito Hello è possibile aggiungere le autorizzazioni utilizzando hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="a93df-159">hello Circuit Owner can add authorizations by using hello following example:</span></span>

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

<span data-ttu-id="a93df-160">**autorizzazioni toodelete**</span><span class="sxs-lookup"><span data-stu-id="a93df-160">**toodelete authorizations**</span></span>

<span data-ttu-id="a93df-161">Hello proprietario del circuito può revocare/eliminazione utente toohello autorizzazioni eseguendo hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="a93df-161">hello Circuit Owner can revoke/delete authorizations toohello user by running hello following example:</span></span>

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a><span data-ttu-id="a93df-162">Operazioni dell'utente del circuito</span><span class="sxs-lookup"><span data-stu-id="a93df-162">Circuit User operations</span></span>

<span data-ttu-id="a93df-163">Utente del circuito Hello deve ID peer hello e una chiave di autorizzazione dal proprietario del circuito hello.</span><span class="sxs-lookup"><span data-stu-id="a93df-163">hello Circuit User needs hello peer ID and an authorization key from hello Circuit Owner.</span></span> <span data-ttu-id="a93df-164">chiave di autorizzazione Hello è un GUID.</span><span class="sxs-lookup"><span data-stu-id="a93df-164">hello authorization key is a GUID.</span></span>

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="a93df-165">**tooredeem un'autorizzazione di connessione**</span><span class="sxs-lookup"><span data-stu-id="a93df-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="a93df-166">Hello utente del circuito è possibile eseguire il seguente esempio tooredeem hello un'autorizzazione del collegamento:</span><span class="sxs-lookup"><span data-stu-id="a93df-166">hello Circuit User can run hello following example tooredeem a link authorization:</span></span>

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="a93df-167">**toorelease un'autorizzazione di connessione**</span><span class="sxs-lookup"><span data-stu-id="a93df-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="a93df-168">È possibile rilasciare un'autorizzazione per l'eliminazione hello connessione che si collega una rete virtuale toohello circuito ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="a93df-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a93df-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a93df-169">Next steps</span></span>

<span data-ttu-id="a93df-170">Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="a93df-170">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
