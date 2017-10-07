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
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>Connettersi a un circuito ExpressRoute di tooan rete virtuale
> [!div class="op_single_selector"]
> * [Portale di Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Interfaccia della riga di comando di Azure](howto-linkvnet-cli.md)
> * [Video - Portale di Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (classico)](expressroute-howto-linkvnet-classic.md)
>

In questo articolo consente di collegare i circuiti ExpressRoute di reti virtuali (Vnet) tooAzure con modello di distribuzione di gestione risorse di hello e PowerShell. Reti virtuali possono essere in hello stessa sottoscrizione o parte di un'altra sottoscrizione. In questo articolo mostra anche la modalità di collegamento tooupdate una rete virtuale. 

## <a name="before-you-begin"></a>Prima di iniziare
* Installare più recente dei moduli di Azure PowerShell hello hello. Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).
* Hello revisione [prerequisiti](expressroute-prerequisites.md), [requisiti di routing](expressroute-routing.md), e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.
* È necessario avere un circuito ExpressRoute attivo. 
  * Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md) e includere circuito hello abilitato dal provider di connettività. 
  * Assicurarsi di disporre del peering privato di Azure configurato per il circuito. Vedere hello [configurare il routing](expressroute-howto-routing-arm.md) articolo per le istruzioni di routing. 
  * Verificare di peering privato di Azure è configurato hello peering BGP tra la rete e Microsoft sia attivo in modo che è possibile abilitare la connettività end-to-end.
  * Assicurarsi di disporre di una rete virtuale e di un gateway di rete virtuale creati e con provisioning completo. Seguire le istruzioni di hello troppo[creare un gateway di rete virtuale per ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Un gateway di rete virtuale per ExpressRoute utilizza hello 'ExpressRoute', il tipo di gateway non VPN.

* È possibile collegare il circuito ExpressRoute standard di too10 reti virtuali tooa. Tutte le reti virtuali devono essere in hello stessa regione di natura geopolitica quando si utilizza un circuito ExpressRoute standard. 

* È possibile collegare una rete virtuale all'esterno di hello geopolitici paese hello circuito ExpressRoute o connettersi a un numero maggiore di reti virtuali tooyour circuito ExpressRoute se è stato abilitato il componente aggiuntivo di hello ExpressRoute premium. Controllare hello [domande frequenti su](expressroute-faqs.md) per ulteriori informazioni sul componente aggiuntivo di hello premium.


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Connettere una rete virtuale in hello circuito tooa sottoscrizione
È possibile connettersi a un tooan di gateway di rete virtuale circuito ExpressRoute tramite hello cmdlet seguenti. Verificare che tale gateway di rete virtuale hello viene creato ed è pronto per il collegamento prima di eseguire il cmdlet hello:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Connettere una rete virtuale in un circuito tooa sottoscrizione diversa
È possibile condividere un circuito ExpressRoute tra più sottoscrizioni. Hello nella figura seguente illustra un semplice schema di funzionamento della condivisione di circuiti ExpressRoute tra più sottoscrizioni.

Ogni cloud più piccoli hello all'interno di cloud di grandi dimensioni hello è toorepresent utilizzate sottoscrizioni appartenenti a reparti toodifferent all'interno dell'organizzazione. Ognuno dei reparti hello hello organizzazione può usare la propria sottoscrizione per la distribuzione i propri servizi, ma possono condividere ExpressRoute circuito tooconnect tooyour indietro locale reti. Un singolo reparto (in questo esempio: IT) può possedere il circuito ExpressRoute hello. Altre sottoscrizioni all'interno dell'organizzazione hello è possono usare il circuito ExpressRoute hello.

> [!NOTE]
> Gli addebiti di connettività e larghezza di banda per hello circuito ExpressRoute sarà proprietario della sottoscrizione toohello applicato. Tutte le reti virtuali condividono hello stessa larghezza di banda.
> 
> 

![Connettività tra sottoscrizioni](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a>Amministrazione - Proprietari e utenti del circuito

Hello 'proprietario del circuito' è un utente autorizzato di alimentazione di hello risorse circuito ExpressRoute. proprietario del circuito Hello è possibile creare le autorizzazioni che possono essere riscattate 'utenti circuito'. Gli utenti del circuito sono proprietari della rete virtuale gateway che non sono in hello stessa sottoscrizione come hello circuito ExpressRoute. Gli utenti del circuito possono riscattare le autorizzazioni (un'autorizzazione per ogni rete virtuale).

proprietario del circuito Hello ha hello power toomodify e revocare le autorizzazioni per in qualsiasi momento. Revoca un risultati di autorizzazione in tutte le connessioni di collegamento viene eliminate dalla sottoscrizione hello il cui accesso è stato revocato.

### <a name="circuit-owner-operations"></a>Operazioni del proprietario del circuito

**toocreate un'autorizzazione**

proprietario del circuito Hello crea un'autorizzazione. Questo comporta hello creazione di una chiave di autorizzazione che può essere utilizzato da un tooconnect utente circuito loro toohello di gateway di rete virtuale circuito ExpressRoute. Un'autorizzazione è valida per una sola connessione.

Hello seguente mostra cmdlet come toocreate un'autorizzazione:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


Hello risposta toothis conterrà lo stato e la chiave di autorizzazione hello:

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



**autorizzazioni tooreview**

proprietario del circuito Hello è possibile esaminare tutte le autorizzazioni che vengono eseguite su un particolare circuito eseguendo hello seguente cmdlet:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**autorizzazioni tooadd**

proprietario del circuito Hello è possibile aggiungere le autorizzazioni utilizzando hello seguente cmdlet:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**autorizzazioni toodelete**

proprietario del circuito Hello può revocare/eliminazione utente toohello autorizzazioni eseguendo hello seguente cmdlet:

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a>Operazioni dell'utente del circuito

utente del circuito Hello deve ID peer hello e una chiave di autorizzazione dal proprietario del circuito hello. chiave di autorizzazione Hello è un GUID.

ID peer può essere controllato da hello comando seguente:

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem un'autorizzazione di connessione**

utente del circuito Hello è possibile eseguire il seguente cmdlet tooredeem hello un'autorizzazione del collegamento:

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease un'autorizzazione di connessione**

È possibile rilasciare un'autorizzazione per l'eliminazione hello connessione che si collega una rete virtuale toohello circuito ExpressRoute hello.

## <a name="modify-a-virtual-network-connection"></a>Modificare una connessione di rete virtuale
È possibile aggiornare alcune proprietà di una connessione di rete virtuale. 

**peso di connessione hello tooupdate**

La rete virtuale può essere connesso toomultiple circuiti di ExpressRoute. Hello stesso prefisso, si potrebbe ricevere da più di un circuito ExpressRoute. toochoose destinati a quale tipo di traffico toosend connessione per il prefisso, è possibile modificare *peso di routing* di una connessione. Il traffico verrà inviato in connessione hello con hello massimo *peso di routing*.

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

intervallo di Hello *peso di routing* è too32000 0. valore predefinito di Hello è 0.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).
