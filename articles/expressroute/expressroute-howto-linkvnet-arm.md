---
title: 'Collegamento di una rete virtuale a un circuito ExpressRoute: PowerShell: Azure | Microsoft Docs'
description: Questo documento offre una panoramica sulle procedure di collegamento delle reti virtuali ai circuiti ExpressRoute usando il modello di distribuzione di Resource Manager e PowerShell.
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
ms.openlocfilehash: 8c2f3036f754a98090ab860f95900416690ebf83
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="connect-a-virtual-network-to-an-expressroute-circuit"></a><span data-ttu-id="e0bfb-103">Connettere una rete virtuale a un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="e0bfb-103">Connect a virtual network to an ExpressRoute circuit</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0bfb-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e0bfb-104">Azure portal</span></span>](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [<span data-ttu-id="e0bfb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0bfb-105">PowerShell</span></span>](expressroute-howto-linkvnet-arm.md)
> * [<span data-ttu-id="e0bfb-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="e0bfb-106">Azure CLI</span></span>](howto-linkvnet-cli.md)
> * [<span data-ttu-id="e0bfb-107">Video - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e0bfb-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [<span data-ttu-id="e0bfb-108">PowerShell (classico)</span><span class="sxs-lookup"><span data-stu-id="e0bfb-108">PowerShell (classic)</span></span>](expressroute-howto-linkvnet-classic.md)
>

<span data-ttu-id="e0bfb-109">Questo articolo spiega come collegare le reti virtuali ai circuiti di Azure ExpressRoute usando il modello di distribuzione di Resource Manager e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-109">This article helps you link virtual networks (VNets) to Azure ExpressRoute circuits by using the Resource Manager deployment model and PowerShell.</span></span> <span data-ttu-id="e0bfb-110">Le reti virtuali possono essere nella stessa sottoscrizione o appartenere a un'altra sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-110">Virtual networks can either be in the same subscription or part of another subscription.</span></span> <span data-ttu-id="e0bfb-111">Questo articolo illustra inoltre come aggiornare un collegamento alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-111">This article also shows you how to update a virtual network link.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="e0bfb-112">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="e0bfb-112">Before you begin</span></span>
* <span data-ttu-id="e0bfb-113">Installare la versione più recente dei moduli di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-113">Install the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="e0bfb-114">Per altre informazioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e0bfb-114">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="e0bfb-115">Verificare i [prerequisiti](expressroute-prerequisites.md), i [requisiti di routing](expressroute-routing.md) e i [flussi di lavoro](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="e0bfb-115">Review the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="e0bfb-116">È necessario avere un circuito ExpressRoute attivo.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-116">You must have an active ExpressRoute circuit.</span></span> 
  * <span data-ttu-id="e0bfb-117">Seguire le istruzioni per [creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md) e fare in modo che venga abilitato dal provider di connettività.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-117">Follow the instructions to [create an ExpressRoute circuit](expressroute-howto-circuit-arm.md) and have the circuit enabled by your connectivity provider.</span></span> 
  * <span data-ttu-id="e0bfb-118">Assicurarsi di disporre del peering privato di Azure configurato per il circuito.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-118">Ensure that you have Azure private peering configured for your circuit.</span></span> <span data-ttu-id="e0bfb-119">Vedere l'articolo relativo alla [configurazione del routing](expressroute-howto-routing-arm.md) per istruzioni relative al routing.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-119">See the [configure routing](expressroute-howto-routing-arm.md) article for routing instructions.</span></span> 
  * <span data-ttu-id="e0bfb-120">Per abilitare la connettività end-to-end è necessario assicurarsi che sia configurato il peering privato di Azure e sia attivo il peering BGP tra la rete e Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-120">Ensure that Azure private peering is configured and the BGP peering between your network and Microsoft is up so that you can enable end-to-end connectivity.</span></span>
  * <span data-ttu-id="e0bfb-121">Assicurarsi di disporre di una rete virtuale e di un gateway di rete virtuale creati e con provisioning completo.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-121">Ensure that you have a virtual network and a virtual network gateway created and fully provisioned.</span></span> <span data-ttu-id="e0bfb-122">Seguire le istruzioni per [creare un gateway di rete virtuale per ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e0bfb-122">Follow the instructions to [create a virtual network gateway for ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).</span></span> <span data-ttu-id="e0bfb-123">Un gateway di rete virtuale per ExpressRoute usa 'ExpressRoute' come GatewayType, non VPN.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-123">A virtual network gateway for ExpressRoute uses the GatewayType 'ExpressRoute', not VPN.</span></span>

* <span data-ttu-id="e0bfb-124">È possibile collegare fino a 10 reti virtuali a un circuito ExpressRoute standard.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-124">You can link up to 10 virtual networks to a standard ExpressRoute circuit.</span></span> <span data-ttu-id="e0bfb-125">Tutte le reti virtuali devono essere nella stessa area geopolitica quando si usa un circuito ExpressRoute standard.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-125">All virtual networks must be in the same geopolitical region when using a standard ExpressRoute circuit.</span></span> 

* <span data-ttu-id="e0bfb-126">È possibile collegare reti virtuali esterne all'area geopolitica del circuito ExpressRoute o connettere un numero maggiore di reti virtuali al circuito ExpressRoute se è stato abilitato il componente aggiuntivo ExpressRoute Premium.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-126">You can link a virtual networks outside of the geopolitical region of the ExpressRoute circuit, or connect a larger number of virtual networks to your ExpressRoute circuit if you enabled the ExpressRoute premium add-on.</span></span> <span data-ttu-id="e0bfb-127">Per altre informazioni sul componente aggiuntivo Premium, vedere le [domande frequenti](expressroute-faqs.md) .</span><span class="sxs-lookup"><span data-stu-id="e0bfb-127">Check the [FAQ](expressroute-faqs.md) for more details on the premium add-on.</span></span>


## <a name="connect-a-virtual-network-in-the-same-subscription-to-a-circuit"></a><span data-ttu-id="e0bfb-128">Collegare una rete virtuale della stessa sottoscrizione a un circuito</span><span class="sxs-lookup"><span data-stu-id="e0bfb-128">Connect a virtual network in the same subscription to a circuit</span></span>
<span data-ttu-id="e0bfb-129">È possibile collegare un gateway di rete virtuale a un circuito ExpressRoute usando il cmdlet seguente.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-129">You can connect a virtual network gateway to an ExpressRoute circuit by using the following cmdlet.</span></span> <span data-ttu-id="e0bfb-130">Prima di eseguire il cmdlet, assicurarsi che il gateway di rete virtuale sia stato creato e sia pronto per il collegamento.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-130">Make sure that the virtual network gateway is created and is ready for linking before you run the cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-to-a-circuit"></a><span data-ttu-id="e0bfb-131">Collegare una rete virtuale di un'altra sottoscrizione a un circuito</span><span class="sxs-lookup"><span data-stu-id="e0bfb-131">Connect a virtual network in a different subscription to a circuit</span></span>
<span data-ttu-id="e0bfb-132">È possibile condividere un circuito ExpressRoute tra più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-132">You can share an ExpressRoute circuit across multiple subscriptions.</span></span> <span data-ttu-id="e0bfb-133">La figura seguente mostra un semplice schema del funzionamento della condivisione di circuiti ExpressRoute tra più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-133">The following figure shows a simple schematic of how sharing works for ExpressRoute circuits across multiple subscriptions.</span></span>

<span data-ttu-id="e0bfb-134">Ciascuno dei cloud più piccoli nel cloud di grandi dimensioni viene usato per rappresentare le sottoscrizioni appartenenti a reparti diversi di un'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-134">Each of the smaller clouds within the large cloud is used to represent subscriptions that belong to different departments within an organization.</span></span> <span data-ttu-id="e0bfb-135">Ciascun reparto dell'organizzazione può usare la propria sottoscrizione per distribuire i servizi, ma i reparti possono condividere un singolo circuito ExpressRoute per la connessione alla rete locale.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-135">Each of the departments within the organization can use their own subscription for deploying their services--but they can share a single ExpressRoute circuit to connect back to your on-premises network.</span></span> <span data-ttu-id="e0bfb-136">Un singolo reparto (in questo esempio, IT) può possedere il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-136">A single department (in this example: IT) can own the ExpressRoute circuit.</span></span> <span data-ttu-id="e0bfb-137">Altre sottoscrizioni all'interno dell'organizzazione possono usare il circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-137">Other subscriptions within the organization can use the ExpressRoute circuit.</span></span>

> [!NOTE]
> <span data-ttu-id="e0bfb-138">I costi relativi a connettività e larghezza di banda per il circuito ExpressRoute saranno addebitati al proprietario della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-138">Connectivity and bandwidth charges for the ExpressRoute circuit will be applied to the subscription owner.</span></span> <span data-ttu-id="e0bfb-139">Tutte le reti virtuali condividono la stessa larghezza di banda.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-139">All virtual networks share the same bandwidth.</span></span>
> 
> 

![Connettività tra sottoscrizioni](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a><span data-ttu-id="e0bfb-141">Amministrazione - Proprietari e utenti del circuito</span><span class="sxs-lookup"><span data-stu-id="e0bfb-141">Administration - circuit owners and circuit users</span></span>

<span data-ttu-id="e0bfb-142">Il proprietario del circuito è l'utente esperto autorizzato della risorsa circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-142">The 'circuit owner' is an authorized Power User of the ExpressRoute circuit resource.</span></span> <span data-ttu-id="e0bfb-143">Il proprietario del circuito può creare le autorizzazioni che possono essere riscattate dagli "utenti del circuito".</span><span class="sxs-lookup"><span data-stu-id="e0bfb-143">The circuit owner can create authorizations that can be redeemed by 'circuit users'.</span></span> <span data-ttu-id="e0bfb-144">Gli utenti del circuito sono i proprietari dei gateway di rete virtuale, che non sono nella stessa sottoscrizione del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-144">Circuit users are owners of virtual network gateways that are not within the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="e0bfb-145">Gli utenti del circuito possono riscattare le autorizzazioni (un'autorizzazione per ogni rete virtuale).</span><span class="sxs-lookup"><span data-stu-id="e0bfb-145">Circuit users can redeem authorizations (one authorization per virtual network).</span></span>

<span data-ttu-id="e0bfb-146">Il proprietario del circuito ha la facoltà di modificare e revocare le autorizzazioni in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-146">The circuit owner has the power to modify and revoke authorizations at any time.</span></span> <span data-ttu-id="e0bfb-147">La revoca dell'autorizzazione comporterà l'eliminazione di tutti i collegamenti dalla sottoscrizione di cui è stato revocato l'accesso.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-147">Revoking an authorization results in all link connections being deleted from the subscription whose access was revoked.</span></span>

### <a name="circuit-owner-operations"></a><span data-ttu-id="e0bfb-148">Operazioni del proprietario del circuito</span><span class="sxs-lookup"><span data-stu-id="e0bfb-148">Circuit owner operations</span></span>

<span data-ttu-id="e0bfb-149">**Per creare un'autorizzazione**</span><span class="sxs-lookup"><span data-stu-id="e0bfb-149">**To create an authorization**</span></span>

<span data-ttu-id="e0bfb-150">Il proprietario del circuito crea un'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-150">The circuit owner creates an authorization.</span></span> <span data-ttu-id="e0bfb-151">Questo comporta la creazione di una chiave di autorizzazione che può essere utilizzata da un utente del circuito per connettere i gateway di rete virtuale al circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-151">This results in the creation of an authorization key that can be used by a circuit user to connect their virtual network gateways to the ExpressRoute circuit.</span></span> <span data-ttu-id="e0bfb-152">Un'autorizzazione è valida per una sola connessione.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-152">An authorization is valid for only one connection.</span></span>

<span data-ttu-id="e0bfb-153">Il frammento di cmdlet seguente mostra come creare un'autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="e0bfb-153">The following cmdlet snippet shows how to create an authorization:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


<span data-ttu-id="e0bfb-154">La risposta conterrà la chiave di autorizzazione e lo stato:</span><span class="sxs-lookup"><span data-stu-id="e0bfb-154">The response to this will contain the authorization key and status:</span></span>

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



<span data-ttu-id="e0bfb-155">**Per verificare le autorizzazioni**</span><span class="sxs-lookup"><span data-stu-id="e0bfb-155">**To review authorizations**</span></span>

<span data-ttu-id="e0bfb-156">Il proprietario del circuito può esaminare tutte le autorizzazioni rilasciate in un particolare circuito eseguendo il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="e0bfb-156">The circuit owner can review all authorizations that are issued on a particular circuit by running the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="e0bfb-157">**Per aggiungere le autorizzazioni**</span><span class="sxs-lookup"><span data-stu-id="e0bfb-157">**To add authorizations**</span></span>

<span data-ttu-id="e0bfb-158">Il proprietario del circuito può aggiungere le autorizzazioni usando il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="e0bfb-158">The circuit owner can add authorizations by using the following cmdlet:</span></span>

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

<span data-ttu-id="e0bfb-159">**Per eliminare le autorizzazioni**</span><span class="sxs-lookup"><span data-stu-id="e0bfb-159">**To delete authorizations**</span></span>

<span data-ttu-id="e0bfb-160">Il proprietario del circuito può revocare o eliminare le autorizzazioni dell'utente eseguendo il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="e0bfb-160">The circuit owner can revoke/delete authorizations to the user by running the following cmdlet:</span></span>

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a><span data-ttu-id="e0bfb-161">Operazioni dell'utente del circuito</span><span class="sxs-lookup"><span data-stu-id="e0bfb-161">Circuit user operations</span></span>

<span data-ttu-id="e0bfb-162">L’utente del circuito deve richiedere l’ID peer e una chiave di autorizzazione al proprietario del circuito.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-162">The circuit user needs the peer ID and an authorization key from the circuit owner.</span></span> <span data-ttu-id="e0bfb-163">La chiave di autorizzazione è un GUID.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-163">The authorization key is a GUID.</span></span>

<span data-ttu-id="e0bfb-164">L'ID peer può essere controllato con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="e0bfb-164">Peer ID can be checked from the following command:</span></span>

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

<span data-ttu-id="e0bfb-165">**Per riscattare un'autorizzazione di connessione**</span><span class="sxs-lookup"><span data-stu-id="e0bfb-165">**To redeem a connection authorization**</span></span>

<span data-ttu-id="e0bfb-166">L'utente del circuito può eseguire il cmdlet seguente per riscattare un'autorizzazione di collegamento:</span><span class="sxs-lookup"><span data-stu-id="e0bfb-166">The circuit user can run the following cmdlet to redeem a link authorization:</span></span>

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

<span data-ttu-id="e0bfb-167">**Per rilasciare un'autorizzazione di connessione**</span><span class="sxs-lookup"><span data-stu-id="e0bfb-167">**To release a connection authorization**</span></span>

<span data-ttu-id="e0bfb-168">È possibile rilasciare un'autorizzazione eliminando il collegamento del circuito ExpressRoute alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-168">You can release an authorization by deleting the connection that links the ExpressRoute circuit to the virtual network.</span></span>

## <a name="modify-a-virtual-network-connection"></a><span data-ttu-id="e0bfb-169">Modificare una connessione di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="e0bfb-169">Modify a virtual network connection</span></span>
<span data-ttu-id="e0bfb-170">È possibile aggiornare alcune proprietà di una connessione di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-170">You can update certain properties of a virtual network connection.</span></span> 

<span data-ttu-id="e0bfb-171">**Per aggiornare il peso della connessione**</span><span class="sxs-lookup"><span data-stu-id="e0bfb-171">**To update the connection weight**</span></span>

<span data-ttu-id="e0bfb-172">La rete virtuale può essere connessa a più circuiti ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-172">Your virtual network can be connected to multiple ExpressRoute circuits.</span></span> <span data-ttu-id="e0bfb-173">È possibile ricevere lo stesso prefisso da più di un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-173">You may receive the same prefix from more than one ExpressRoute circuit.</span></span> <span data-ttu-id="e0bfb-174">Per scegliere la connessione per l'invio di traffico destinato per questo prefisso, è possibile modificare il valore *RoutingWeight* di una connessione.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-174">To choose which connection to send traffic destined for this prefix, you can change *RoutingWeight* of a connection.</span></span> <span data-ttu-id="e0bfb-175">Il traffico verrà inviato sulla connessione con il valore massimo di *RoutingWeight*.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-175">Traffic will be sent on the connection with the highest *RoutingWeight*.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

<span data-ttu-id="e0bfb-176">L'intervallo di *RoutingWeight* va da 0 a 32.000.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-176">The range of *RoutingWeight* is 0 to 32000.</span></span> <span data-ttu-id="e0bfb-177">Il valore predefinito è 0.</span><span class="sxs-lookup"><span data-stu-id="e0bfb-177">The default value is 0.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0bfb-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e0bfb-178">Next steps</span></span>
<span data-ttu-id="e0bfb-179">Per altre informazioni su ExpressRoute, vedere le [Domande frequenti su ExpressRoute](expressroute-faqs.md).</span><span class="sxs-lookup"><span data-stu-id="e0bfb-179">For more information about ExpressRoute, see the [ExpressRoute FAQ](expressroute-faqs.md).</span></span>
