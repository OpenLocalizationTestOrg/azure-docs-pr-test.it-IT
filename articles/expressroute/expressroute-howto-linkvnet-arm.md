---
title: 'Collegare un circuito ExpressRoute di tooan rete virtuale: PowerShell: Azure | Documenti Microsoft'
description: Questo documento viene fornita una panoramica del modo virtuale toolink reti circuiti tooExpressRoute (Vnet) con modello di distribuzione di gestione risorse di hello e PowerShell.
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a><span data-ttu-id="97d0a-103">Connettersi a un circuito ExpressRoute di tooan rete virtuale</span><span class="sxs-lookup"><span data-stu-id="97d0a-103">Connect a virtual network tooan ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97d0a-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="97d0a-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="97d0a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="97d0a-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="97d0a-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="97d0a-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="97d0a-107">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="97d0a-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="97d0a-108">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="97d0a-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="97d0a-109">In questo articolo consente di collegare i circuiti ExpressRoute di reti virtuali (Vnet) tooAzure con modello di distribuzione di gestione risorse di hello e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="97d0a-109">This article helps you link virtual networks (VNets) tooAzure ExpressRoute circuits by using hello Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="97d0a-110">Reti virtuali possono essere in hello stessa sottoscrizione o parte di un'altra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="97d0a-110">Virtual networks can either be in hello same subscription or part of another subscription.</span></span> <span data-ttu-id="97d0a-111">In questo articolo mostra anche la modalità di collegamento tooupdate una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="97d0a-111">This article also shows you how tooupdate a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="97d0a-112">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="97d0a-112">Before you begin</span></span>
* <span data-ttu-id="97d0a-113">Installare più recente dei moduli di Azure PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="97d0a-113">Install hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="97d0a-114">Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="97d0a-114">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="97d0a-115">Hello revisione [prerequisiti](expressroute-prerequisites.md), [requisiti di routing](expressroute-routing.md), e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="97d0a-115">Review hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="97d0a-116">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="97d0a-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="97d0a-117">Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md) e includere circuito hello abilitato dal provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="97d0a-117">Follow hello instructions too[create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have hello circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="97d0a-118">Assicurarsi di disporre del peering privato di Azure configurato per il circuito.</span><span class="sxs-lookup"><span data-stu-id="97d0a-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="97d0a-119">Vedere hello [configurare il routing](expressroute-howto-routing-arm.md) articolo per le istruzioni di routing.</span><span class="sxs-lookup"><span data-stu-id="97d0a-119">See hello [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="97d0a-120">Verificare di peering privato di Azure è configurato hello peering BGP tra la rete e Microsoft sia attivo in modo che è possibile abilitare la connettività end-to-end.</span><span class="sxs-lookup"><span data-stu-id="97d0a-120">Ensure that Azure private peering is configured and hello BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="97d0a-121">Assicurarsi di disporre di una rete virtuale e di un gateway di rete virtuale creati e con provisioning completo.</span><span class="sxs-lookup"><span data-stu-id="97d0a-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="97d0a-122">Seguire le istruzioni di hello troppo[creare un gateway di rete virtuale per ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="97d0a-122">Follow hello instructions too[create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="97d0a-123">Un gateway di rete virtuale per ExpressRoute utilizza hello 'ExpressRoute', il tipo di gateway non VPN.</span><span class="sxs-lookup"><span data-stu-id="97d0a-123">A virtual network gateway for ExpressRoute uses hello GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="97d0a-124">È possibile collegare il circuito ExpressRoute standard di too10 reti virtuali tooa.</span><span class="sxs-lookup"><span data-stu-id="97d0a-124">You can link up too10 virtual networks tooa standard ExpressRoute circuit.</span></span> <span data-ttu-id="97d0a-125">Tutte le reti virtuali devono essere in hello stessa regione di natura geopolitica quando si utilizza un circuito ExpressRoute standard.</span><span class="sxs-lookup"><span data-stu-id="97d0a-125">All virtual networks must be in hello same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="97d0a-126">È possibile collegare una rete virtuale all'esterno di hello geopolitici paese hello circuito ExpressRoute o connettersi a un numero maggiore di reti virtuali tooyour circuito ExpressRoute se è stato abilitato il componente aggiuntivo di hello ExpressRoute premium.</span><span class="sxs-lookup"><span data-stu-id="97d0a-126">You can link a virtual networks outside of hello geopolitical region of hello ExpressRoute circuit, or connect a larger number of virtual networks tooyour ExpressRoute circuit if you enabled hello ExpressRoute premium add-on.</span></span> <span data-ttu-id="97d0a-127">Controllare hello [domande frequenti su](expressroute-faqs.md) per ulteriori informazioni sul componente aggiuntivo di hello premium.</span><span class="sxs-lookup"><span data-stu-id="97d0a-127">Check hello [FAQ](expressroute-faqs.md) for more details on hello premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a><span data-ttu-id="97d0a-128">Connettere una rete virtuale in hello circuito tooa sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="97d0a-128">Connect a virtual network in hello same subscription tooa circuit</span></span>
<span data-ttu-id="97d0a-129">È possibile connettersi a un tooan di gateway di rete virtuale circuito ExpressRoute tramite hello cmdlet seguenti.</span><span class="sxs-lookup"><span data-stu-id="97d0a-129">You can connect a virtual network gateway tooan ExpressRoute circuit by using hello following cmdlet.</span></span> <span data-ttu-id="97d0a-130">Verificare che tale gateway di rete virtuale hello viene creato ed è pronto per il collegamento prima di eseguire il cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="97d0a-130">Make sure that hello virtual network gateway is created and is ready for linking before you run hello cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a><span data-ttu-id="97d0a-131">Connettere una rete virtuale in un circuito tooa sottoscrizione diversa</span><span class="sxs-lookup"><span data-stu-id="97d0a-131">Connect a virtual network in a different subscription tooa circuit</span></span>
<span data-ttu-id="97d0a-132">È possibile condividere un circuito ExpressRoute tra più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="97d0a-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="97d0a-133">Hello nella figura seguente illustra un semplice schema di funzionamento della condivisione di circuiti ExpressRoute tra più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="97d0a-133">hello following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="97d0a-134">Ogni cloud più piccoli hello all'interno di cloud di grandi dimensioni hello è toorepresent utilizzate sottoscrizioni appartenenti a reparti toodifferent all'interno dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="97d0a-134">Each of hello smaller clouds within hello large cloud is used toorepresent subscriptions that belong toodifferent departments within an organization.</span></span> <span data-ttu-id="97d0a-135">Ognuno dei reparti hello hello organizzazione può usare la propria sottoscrizione per la distribuzione i propri servizi, ma possono condividere ExpressRoute circuito tooconnect tooyour indietro locale reti.</span><span class="sxs-lookup"><span data-stu-id="97d0a-135">Each of hello departments within hello organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit tooconnect back tooyour on-premises network.</span></span> <span data-ttu-id="97d0a-136">Un singolo reparto (in questo esempio: IT) può possedere il circuito ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="97d0a-136">A single department (in this example: IT) can own hello ExpressRoute circuit.</span></span> <span data-ttu-id="97d0a-137">Altre sottoscrizioni all'interno dell'organizzazione hello è possono usare il circuito ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="97d0a-137">Other subscriptions within hello organization can use hello ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="97d0a-138">Gli addebiti di connettività e larghezza di banda per hello circuito ExpressRoute sarà proprietario della sottoscrizione toohello applicato.</span><span class="sxs-lookup"><span data-stu-id="97d0a-138">Connectivity and bandwidth charges for hello ExpressRoute circuit will be applied toohello subscription owner.</span></span> <span data-ttu-id="97d0a-139">Tutte le reti virtuali condividono hello stessa larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="97d0a-139">All virtual networks share hello same bandwidth.</span></span>
> 
> 

![Connettività tra sottoscrizioni](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="97d0a-141">Amministrazione - Proprietari e utenti del circuito</span><span class="sxs-lookup"><span data-stu-id="97d0a-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="97d0a-142">Hello 'proprietario del circuito' è un utente autorizzato di alimentazione di hello risorse circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="97d0a-142">hello 'circuit owner' is an authorized Power User of hello ExpressRoute circuit resource.</span></span> <span data-ttu-id="97d0a-143">proprietario del circuito Hello è possibile creare le autorizzazioni che possono essere riscattate 'utenti circuito'.</span><span class="sxs-lookup"><span data-stu-id="97d0a-143">hello circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="97d0a-144">Gli utenti del circuito sono proprietari della rete virtuale gateway che non sono in hello stessa sottoscrizione come hello circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="97d0a-144">Circuit users are owners of virtual network gateways that are not within hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="97d0a-145">Gli utenti del circuito possono riscattare le autorizzazioni (un'autorizzazione per ogni rete virtuale).</span><span class="sxs-lookup"><span data-stu-id="97d0a-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="97d0a-146">proprietario del circuito Hello ha hello power toomodify e revocare le autorizzazioni per in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="97d0a-146">hello circuit owner has hello power toomodify and revoke authorizations at any time.</span></span> <span data-ttu-id="97d0a-147">Revoca un risultati di autorizzazione in tutte le connessioni di collegamento viene eliminate dalla sottoscrizione hello il cui accesso è stato revocato.</span><span class="sxs-lookup"><span data-stu-id="97d0a-147">Revoking an authorization results in all link connections being deleted from hello subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="97d0a-148">Operazioni del proprietario del circuito</span><span class="sxs-lookup"><span data-stu-id="97d0a-148">Circuit owner operations</span></span>

<span data-ttu-id="97d0a-149">**toocreate un'autorizzazione**</span><span class="sxs-lookup"><span data-stu-id="97d0a-149">**toocreate an authorization**</span></span>

<span data-ttu-id="97d0a-150">proprietario del circuito Hello crea un'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="97d0a-150">hello circuit owner creates an authorization.</span></span> <span data-ttu-id="97d0a-151">Questo comporta hello creazione di una chiave di autorizzazione che può essere utilizzato da un tooconnect utente circuito loro toohello di gateway di rete virtuale circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="97d0a-151">This results in hello creation of an authorization key that can be used by a circuit user tooconnect their virtual network gateways toohello ExpressRoute circuit.</span></span> <span data-ttu-id="97d0a-152">Un'autorizzazione è valida per una sola connessione.</span><span class="sxs-lookup"><span data-stu-id="97d0a-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="97d0a-153">Hello seguente mostra cmdlet come toocreate un'autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="97d0a-153">hello following cmdlet snippet shows how toocreate an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="97d0a-154">Hello risposta toothis conterrà lo stato e la chiave di autorizzazione hello:</span><span class="sxs-lookup"><span data-stu-id="97d0a-154">hello response toothis will contain hello authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="97d0a-155">**autorizzazioni tooreview**</span><span class="sxs-lookup"><span data-stu-id="97d0a-155">**tooreview authorizations**</span></span>

<span data-ttu-id="97d0a-156">proprietario del circuito Hello è possibile esaminare tutte le autorizzazioni che vengono eseguite su un particolare circuito eseguendo hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="97d0a-156">hello circuit owner can review all authorizations that are issued on a particular circuit by running hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="97d0a-157">**autorizzazioni tooadd**</span><span class="sxs-lookup"><span data-stu-id="97d0a-157">**tooadd authorizations**</span></span>

<span data-ttu-id="97d0a-158">proprietario del circuito Hello è possibile aggiungere le autorizzazioni utilizzando hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="97d0a-158">hello circuit owner can add authorizations by using hello following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="97d0a-159">**autorizzazioni toodelete**</span><span class="sxs-lookup"><span data-stu-id="97d0a-159">**toodelete authorizations**</span></span>

<span data-ttu-id="97d0a-160">proprietario del circuito Hello può revocare/eliminazione utente toohello autorizzazioni eseguendo hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="97d0a-160">hello circuit owner can revoke/delete authorizations toohello user by running hello following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="97d0a-161">Operazioni dell'utente del circuito</span><span class="sxs-lookup"><span data-stu-id="97d0a-161">Circuit user operations</span></span>

<span data-ttu-id="97d0a-162">utente del circuito Hello deve ID peer hello e una chiave di autorizzazione dal proprietario del circuito hello.</span><span class="sxs-lookup"><span data-stu-id="97d0a-162">hello circuit user needs hello peer ID and an authorization key from hello circuit owner.</span></span> <span data-ttu-id="97d0a-163">chiave di autorizzazione Hello è un GUID.</span><span class="sxs-lookup"><span data-stu-id="97d0a-163">hello authorization key is a GUID.</span></span>

<span data-ttu-id="97d0a-164">ID peer può essere controllato da hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="97d0a-164">Peer ID can be checked from hello following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="97d0a-165">**tooredeem un'autorizzazione di connessione**</span><span class="sxs-lookup"><span data-stu-id="97d0a-165">**tooredeem a connection authorization**</span></span>

<span data-ttu-id="97d0a-166">utente del circuito Hello è possibile eseguire il seguente cmdlet tooredeem hello un'autorizzazione del collegamento:</span><span class="sxs-lookup"><span data-stu-id="97d0a-166">hello circuit user can run hello following cmdlet tooredeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="97d0a-167">**toorelease un'autorizzazione di connessione**</span><span class="sxs-lookup"><span data-stu-id="97d0a-167">**toorelease a connection authorization**</span></span>

<span data-ttu-id="97d0a-168">È possibile rilasciare un'autorizzazione per l'eliminazione hello connessione che si collega una rete virtuale toohello circuito ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="97d0a-168">You can release an authorization by deleting hello connection that links hello ExpressRoute circuit toohello virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="97d0a-169">Modificare una connessione di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="97d0a-169">Modify a virtual network connection</span></span>
<span data-ttu-id="97d0a-170">È possibile aggiornare alcune proprietà di una connessione di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="97d0a-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="97d0a-171">**peso di connessione hello tooupdate**</span><span class="sxs-lookup"><span data-stu-id="97d0a-171">**tooupdate hello connection weight**</span></span>

<span data-ttu-id="97d0a-172">La rete virtuale può essere connesso toomultiple circuiti di ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="97d0a-172">Your virtual network can be connected toomultiple ExpressRoute circuits.</span></span> <span data-ttu-id="97d0a-173">Hello stesso prefisso, si potrebbe ricevere da più di un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="97d0a-173">You may receive hello same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="97d0a-174">toochoose destinati a quale tipo di traffico toosend connessione per il prefisso, è possibile modificare *peso di routing* di una connessione.</span><span class="sxs-lookup"><span data-stu-id="97d0a-174">toochoose which connection toosend traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="97d0a-175">Il traffico verrà inviato in connessione hello con hello massimo *peso di routing*.</span><span class="sxs-lookup"><span data-stu-id="97d0a-175">Traffic will be sent on hello connection with hello highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="97d0a-176">intervallo di Hello *peso di routing* è too32000 0.</span><span class="sxs-lookup"><span data-stu-id="97d0a-176">hello range of *RoutingWeight* is 0 too32000.</span></span> <span data-ttu-id="97d0a-177">valore predefinito di Hello è 0.</span><span class="sxs-lookup"><span data-stu-id="97d0a-177">hello default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97d0a-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="97d0a-178">Next steps</span></span>
<span data-ttu-id="97d0a-179">Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="97d0a-179">For more information about ExpressRoute, see hello [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
