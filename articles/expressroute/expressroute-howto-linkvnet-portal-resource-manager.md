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
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>Connettersi a un circuito ExpressRoute di tooan rete virtuale
> [!div class="op_single_selector"]
> * [Portale di Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Interfaccia della riga di comando di Azure](howto-linkvnet-cli.md)
> * [Video - Portale di Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (classico)](expressroute-howto-linkvnet-classic.md)
> 

In questo articolo consente di collegare i circuiti ExpressRoute di reti virtuali (Vnet) tooAzure con modello di distribuzione di gestione risorse di hello e hello portale di Azure. Reti virtuali possono essere in hello stessa sottoscrizione oppure può essere parte di un'altra sottoscrizione.

## <a name="before-you-begin"></a>Prima di iniziare
* Hello revisione [prerequisiti](expressroute-prerequisites.md), [requisiti di routing](expressroute-routing.md), e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.
* È necessario avere un circuito ExpressRoute attivo.
  
  * Seguire le istruzioni di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e includere circuito hello abilitato dal provider di connettività.
  * Assicurarsi di disporre del peering privato di Azure configurato per il circuito. Vedere hello [Configura routing](expressroute-howto-routing-portal-resource-manager.md) articolo per le istruzioni di routing.
  * Verificare di peering privato di Azure è configurato hello peering BGP tra la rete e Microsoft sia attivo in modo che è possibile abilitare la connettività end-to-end.
  * Assicurarsi di disporre di una rete virtuale e di un gateway di rete virtuale creati e con provisioning completo. Seguire le istruzioni di hello troppo[creare un gateway di rete virtuale per ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Un gateway di rete virtuale per ExpressRoute utilizza hello 'ExpressRoute', il tipo di gateway non VPN.

* È possibile collegare il circuito ExpressRoute standard di too10 reti virtuali tooa. Tutte le reti virtuali devono essere in hello stessa regione di natura geopolitica quando si utilizza un circuito ExpressRoute standard. 
* È possibile collegare una rete virtuale all'esterno di hello geopolitici paese hello circuito ExpressRoute o connettersi a un numero maggiore di reti virtuali tooyour circuito ExpressRoute se è stato abilitato il componente aggiuntivo di hello ExpressRoute premium. Controllare hello [domande frequenti su](expressroute-faqs.md) per ulteriori informazioni sul componente aggiuntivo di hello premium.
* È possibile [visualizzare un video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) prima toobetter inizio comprendere i passaggi di hello.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Connettere una rete virtuale in hello circuito tooa sottoscrizione

### <a name="toocreate-a-connection"></a>toocreate una connessione

> [!NOTE]
> Informazioni di configurazione BGP non apparirà se il provider di livello 3 hello configurato il peering. Se il circuito si trova in uno stato di provisioning, dovrebbe essere in grado di toocreate connessioni.
>

1. Verificare che il circuito ExpressRoute e il peering privato di Azure siano configurati correttamente. Seguire le istruzioni hello [creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md) e [Configura routing](expressroute-howto-routing-arm.md). Il circuito ExpressRoute dovrebbe essere simile hello seguente immagine:

    ![Schermata del circuito ExpressRoute](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. È ora possibile avviare il provisioning del tooyour di gateway di rete virtuale circuito ExpressRoute toolink una connessione. Fare clic su **connessione** > **Aggiungi** tooopen hello **Aggiungi connessione** pannello e quindi configurare i valori hello.

    ![Aggiungere la schermata della connessione](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. Dopo la connessione è stata configurata, l'oggetto di connessione verrà visualizzate informazioni di hello per connessione hello.

     ![Schermata dell'oggetto connessione](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a>toodelete una connessione
È possibile eliminare una connessione selezionando hello **eliminare** icona nel Pannello di hello per la connessione.

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Connettere una rete virtuale in un circuito tooa sottoscrizione diversa
È possibile condividere un circuito ExpressRoute tra più sottoscrizioni. Figura Hello seguente illustra un semplice schematica del funzionamento della condivisione di circuiti ExpressRoute tra più sottoscrizioni.

![Connettività tra sottoscrizioni](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- Ogni cloud più piccoli hello all'interno di cloud di grandi dimensioni hello è toorepresent utilizzate sottoscrizioni appartenenti a reparti toodifferent all'interno dell'organizzazione.
- Ognuno dei reparti hello hello organizzazione può usare la propria sottoscrizione per distribuire i propri servizi, ma queste possono condividere una singola ExpressRoute circuito tooconnect tooyour indietro locale rete.
- Un singolo reparto (in questo esempio: IT) può possedere il circuito ExpressRoute hello. Altre sottoscrizioni all'interno dell'organizzazione hello è possono usare il circuito ExpressRoute hello.

    > [!NOTE]
    > Gli addebiti di connettività e larghezza di banda per il circuito dedicato hello sarà proprietario del circuito ExpressRoute toohello applicato. Tutte le reti virtuali condividono hello stessa larghezza di banda.
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a>Amministrazione - Proprietari e utenti del circuito

Hello 'proprietario del circuito' è un utente autorizzato di alimentazione di hello risorse circuito ExpressRoute. proprietario del circuito Hello è possibile creare le autorizzazioni che possono essere riscattate 'utenti circuito'. Gli utenti del circuito sono proprietari della rete virtuale gateway che non sono in hello stessa sottoscrizione come hello circuito ExpressRoute. Gli utenti del circuito possono riscattare le autorizzazioni (un'autorizzazione per ogni rete virtuale).

proprietario del circuito Hello ha hello power toomodify e revocare le autorizzazioni per in qualsiasi momento. Revoca un risultati di autorizzazione in tutte le connessioni di collegamento viene eliminate dalla sottoscrizione hello il cui accesso è stato revocato.

### <a name="circuit-owner-operations"></a>Operazioni del proprietario del circuito

**toocreate un'autorizzazione di connessione**

proprietario del circuito Hello crea un'autorizzazione. Questo comporta hello creazione di una chiave di autorizzazione che può essere utilizzato da un tooconnect utente circuito loro toohello di gateway di rete virtuale circuito ExpressRoute. Un'autorizzazione è valida per una sola connessione.

1. Nel Pannello di ExpressRoute hello, fare clic su **autorizzazioni** e quindi digitare un **nome** autorizzazione hello e fare clic su **salvare**.

    ![Authorizations](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. Dopo aver salvata la configurazione hello, copiare hello **ID risorsa** hello e **chiave di autorizzazione**.

    ![Chiave di autorizzazione](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

**toodelete un'autorizzazione di connessione**

È possibile eliminare una connessione selezionando hello **eliminare** icona nel Pannello di hello per la connessione.

### <a name="circuit-user-operations"></a>Operazioni dell'utente del circuito

utente del circuito Hello necessita di ID di risorsa hello e una chiave di autorizzazione dal proprietario del circuito hello. 

**tooredeem un'autorizzazione di connessione**

1.  Fare clic su hello **+ nuovo** pulsante.

    ![Click New](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  Cercare **"Connessione"** hello Marketplace, selezionarla e fare clic su **crea**.

    ![Cercare Connection (Connessione)](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  Verificare che hello **tipo di connessione** è troppo "ExpressRoute".


4.  Specificare i dettagli di hello, quindi fare clic su **OK** nel Pannello di hello nozioni di base.

    ![Pannello Nozioni di base](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  In hello **impostazioni** blade, seleziona hello **gateway di rete virtuale** e controllare hello **riscattare autorizzazione** casella di controllo.

6.  Immettere hello **chiave di autorizzazione** hello e **Peer circuito URI** e assegnare un nome di connessione hello. Fare clic su **OK**.

    ![Pannello Impostazioni](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. Esaminare le informazioni di hello in hello **riepilogo** pannello e fare clic su **OK**.


**toorelease un'autorizzazione di connessione**

È possibile rilasciare un'autorizzazione per l'eliminazione hello connessione che si collega una rete virtuale toohello circuito ExpressRoute hello.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).
