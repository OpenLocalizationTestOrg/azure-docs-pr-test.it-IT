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
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a>Connettersi a un circuito ExpressRoute tooan di rete virtuale utilizzando l'interfaccia CLI

In questo articolo consente di collegare i circuiti ExpressRoute di reti virtuali (Vnet) tooAzure utilizzando CLI. toolink mediante Azure CLI, le reti virtuali hello devono essere create usando il modello di distribuzione del hello Gestione risorse. Può essere in hello stessa sottoscrizione o parte di un'altra sottoscrizione. Se si desidera toouse tooconnect un metodo diverso del circuito ExpressRoute di tooan di rete virtuale, è possibile selezionare un articolo da hello seguente elenco:

> [!div class="op_single_selector"]
> * [Portale di Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Interfaccia della riga di comando di Azure](howto-linkvnet-cli.md)
> * [Video - Portale di Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (classico)](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a>Prerequisiti di configurazione

* È necessario l'ultima versione di hello dell'interfaccia della riga di comando hello (CLI). Per altre informazioni, vedere [Installare l'interfaccia della riga di comando di Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
* È necessario hello tooreview [prerequisiti](expressroute-prerequisites.md), [requisiti di routing](expressroute-routing.md), e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.
* È necessario avere un circuito ExpressRoute attivo. 
  * Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](howto-circuit-cli.md) e includere circuito hello abilitato dal provider di connettività. 
  * Assicurarsi di disporre del peering privato di Azure configurato per il circuito. Vedere hello [configurare il routing](howto-routing-cli.md) articolo per le istruzioni di routing. 
  * Verificare che il peering privato di Azure sia configurato. il peering BGP Hello tra la rete e Microsoft deve essere backup in modo che è possibile abilitare la connettività end-to-end.
  * Assicurarsi di disporre di una rete virtuale e di un gateway di rete virtuale creati e con provisioning completo. Seguire le istruzioni di hello troppo[configurare un gateway di rete virtuale per ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli). Toouse assicurarsi di essere `--gateway-type ExpressRoute`.

* È possibile collegare il circuito ExpressRoute standard di too10 reti virtuali tooa. Tutte le reti virtuali devono essere in hello stessa regione di natura geopolitica quando si utilizza un circuito ExpressRoute standard. 

* Se si abilita il componente aggiuntivo di hello ExpressRoute premium, è possibile collegare una rete virtuale all'esterno di hello geopolitici paese hello circuito ExpressRoute o connettersi a un numero maggiore di reti virtuali tooyour circuito ExpressRoute. Per ulteriori informazioni sul componente aggiuntivo di hello premium, vedere hello [domande frequenti su](expressroute-faqs.md).

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Connettere una rete virtuale in hello circuito tooa sottoscrizione

È possibile connettersi a un circuito ExpressRoute tooan di rete virtuale gateway utilizzando l'esempio hello. Verificare che tale gateway di rete virtuale hello viene creato ed è pronto per il collegamento prima di eseguire il comando hello.

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Connettere una rete virtuale in un circuito tooa sottoscrizione diversa

È possibile condividere un circuito ExpressRoute tra più sottoscrizioni. Figura Hello seguente illustra un semplice schematica del funzionamento della condivisione di circuiti ExpressRoute tra più sottoscrizioni.

Ogni cloud più piccoli hello all'interno di cloud di grandi dimensioni hello è toorepresent utilizzate sottoscrizioni appartenenti a reparti toodifferent all'interno dell'organizzazione. Ognuno dei reparti hello hello organizzazione può usare la propria sottoscrizione per la distribuzione i propri servizi, ma possono condividere ExpressRoute circuito tooconnect tooyour indietro locale reti. Un singolo reparto (in questo esempio: IT) può possedere il circuito ExpressRoute hello. Altre sottoscrizioni all'interno dell'organizzazione hello è possono usare il circuito ExpressRoute hello.

> [!NOTE]
> Le spese di connettività e larghezza di banda per il circuito dedicato hello verranno applicato toohello proprietario del circuito ExpressRoute. Tutte le reti virtuali condividono hello stessa larghezza di banda.
> 
> 

![Connettività tra sottoscrizioni](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a>Amministrazione: proprietari e utenti del circuito

Hello 'Proprietario del circuito' è un utente autorizzato di alimentazione di hello risorse circuito ExpressRoute. Proprietario del circuito Hello è possibile creare le autorizzazioni che possono essere riscattate da 'Circuito Users'. Gli utenti del circuito sono proprietari della rete virtuale gateway che non sono in hello stessa sottoscrizione come hello circuito ExpressRoute. Gli utenti del circuito possono riscattare le autorizzazioni, una per ogni rete virtuale.

Proprietario del circuito Hello è hello power toomodify e revocare le autorizzazioni per in qualsiasi momento. Quando l'autorizzazione viene revocata, tutte le connessioni di collegamento vengono eliminate dalla sottoscrizione hello il cui accesso è stato revocato.

### <a name="circuit-owner-operations"></a>Operazioni del proprietario del circuito

**toocreate un'autorizzazione**

Proprietario del circuito Hello crea un'autorizzazione, che consente di creare una chiave di autorizzazione che può essere utilizzato da un utente del circuito di tooconnect loro toohello di gateway di rete virtuale circuito ExpressRoute. Un'autorizzazione è valida per una sola connessione.

Hello seguente esempio viene illustrato come toocreate un'autorizzazione:

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

risposta Hello contiene lo stato e la chiave di autorizzazione hello:

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

**autorizzazioni tooreview**

Hello proprietario del circuito può esaminare tutte le autorizzazioni che vengono eseguite su un particolare circuito eseguendo hello di esempio seguente:

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

**autorizzazioni tooadd**

Proprietario del circuito Hello è possibile aggiungere le autorizzazioni utilizzando hello di esempio seguente:

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

**autorizzazioni toodelete**

Hello proprietario del circuito può revocare/eliminazione utente toohello autorizzazioni eseguendo hello di esempio seguente:

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a>Operazioni dell'utente del circuito

Utente del circuito Hello deve ID peer hello e una chiave di autorizzazione dal proprietario del circuito hello. chiave di autorizzazione Hello è un GUID.

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem un'autorizzazione di connessione**

Hello utente del circuito è possibile eseguire il seguente esempio tooredeem hello un'autorizzazione del collegamento:

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease un'autorizzazione di connessione**

È possibile rilasciare un'autorizzazione per l'eliminazione hello connessione che si collega una rete virtuale toohello circuito ExpressRoute hello.

## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).
