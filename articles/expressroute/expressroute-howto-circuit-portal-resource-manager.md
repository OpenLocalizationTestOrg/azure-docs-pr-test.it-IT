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
# <a name="create-and-modify-an-expressroute-circuit"></a>Creare e modificare un circuito ExpressRoute
> [!div class="op_single_selector"]
> * [Portale di Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Interfaccia della riga di comando di Azure](howto-circuit-cli.md)
> * [Video - Portale di Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (classico)](expressroute-howto-circuit-classic.md)
>

In questo articolo viene descritto come toocreate un circuito ExpressRoute di Azure tramite hello Azure portal e hello Azure Resource Manager modello di distribuzione. Hello anche passaggi Mostra come lo stato di hello toocheck del circuito di hello, aggiornarla, o eliminare e deprovisioning.


## <a name="before-you-begin"></a>Prima di iniziare
* Hello revisione [prerequisiti](expressroute-prerequisites.md) e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.
* Assicurarsi di disporre di accesso toohello [portale di Azure](https://portal.azure.com).
* Assicurarsi di disporre delle autorizzazioni toocreate nuova le risorse di rete. Se non si dispone delle autorizzazioni appropriate di hello, contattare l'amministratore dell'account.
* È possibile [visualizzare un video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) prima di iniziare, in ordine toobetter comprendere i passaggi di hello.

## <a name="create-and-provision-an-expressroute-circuit"></a>Creare un circuito ExpressRoute ed eseguirne il provisioning
### <a name="1-sign-in-toohello-azure-portal"></a>1. Accedi toohello portale di Azure
Da un browser, passare toohello [portale di Azure](http://portal.azure.com) e accedere con l'account di Azure.

### <a name="2-create-a-new-expressroute-circuit"></a>2. Creare un nuovo circuito ExpressRoute
> [!IMPORTANT]
> Dal momento hello che viene eseguita una chiave del servizio verrà addebitato il circuito ExpressRoute. Assicurarsi di eseguire questa operazione quando il provider di connettività hello è circuito hello tooprovision pronto.
> 
> 

1. È possibile creare un circuito ExpressRoute selezionando hello opzione toocreate una nuova risorsa. Fare clic su **New** > **rete** > **ExpressRoute**, come illustrato nella seguente immagine hello:
   
    ![Creare un circuito ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. Dopo aver fatto clic **ExpressRoute**, si noterà hello **circuito ExpressRoute creare** blade. Quando sta inserimento dei valori hello in questo pannello, assicurarsi di specificare hello corretto dello SKU e misurazione dei dati.
   
   * **livello** determina se è abilitato un componente aggiuntivo ExpressRoute Standard o ExpressRoute Premium. È possibile specificare **Standard** tooget hello SKU standard o **Premium** per il componente aggiuntivo di hello premium.
   * **Misurazione dei dati** determina tipo fatturazione hello. È possibile specificare **A consumo** per un piano dati a consumo e **Senza limiti** per un piano dati illimitato. Si noti che è possibile modificare il tipo fatturazione di hello da **Metered** troppo**Unlimited**, ma è possibile modificare il tipo di hello da **Unlimited** troppo**Metered**.
     
     ![Configurare il livello SKU hello e misurazione dei dati](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> Tenere presente che il percorso di Peering hello indica hello [posizione fisica](expressroute-locations.md) in cui sono peering con Microsoft. Si tratta di **non** collegato troppo proprietà "Location", che fa riferimento geography toohello hello Provider di risorse di rete di Azure in cui si trova. Non sono correlate, ma è toochoose una buona norma un toohello geograficamente chiudere il percorso di Peering del circuito hello di Provider di risorse di rete. 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a>3. Visualizzazione hello circuiti e proprietà
**Consente di visualizzare tutti i circuiti hello**

È possibile visualizzare tutti i circuiti hello creato selezionando **tutte le risorse** dal menu a sinistra di hello.

![Visualizzazione dei circuiti](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

**Visualizzare le proprietà di hello**

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Visualizza proprietà](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>4. Inviare i provider di connettività di hello servizio tooyour chiave per il provisioning
In questo pannello, **stato Provider** fornisce informazioni sullo stato corrente di hello di provisioning sul lato di provider di servizi di hello. **Stato circuit** fornisce lo stato di hello in hello lato Microsoft. Per ulteriori informazioni sul provisioning stati circuito, vedere hello [flussi di lavoro](expressroute-workflows.md#expressroute-circuit-provisioning-states) articolo.

Quando si crea un nuovo circuito ExpressRoute, circuito hello sarà nel seguente stato hello:

Stato provider: Senza provisioning<BR>
 Stato circuito: Abilitato

![Avvio del processo di provisioning](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

circuito Hello cambierà toohello seguente lo stato quando il provider di connettività hello è in corso di hello di abilitarlo per l'utente:

Stato provider: Provisioning in corso<BR>
 Stato circuito: Abilitato

Per è toobe in grado di toouse un circuito ExpressRoute, deve essere nel seguente stato hello:

Stato provider: Provisioning eseguito<BR>
 Stato circuito: Abilitato

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>5. Controllare periodicamente hello stato della chiave circuito hello e hello
È possibile visualizzare le proprietà di hello del circuito hello che è interessati a selezionandolo. Controllare hello **stato Provider** e assicurarsi che siano spostati troppo**provisioning eseguito** prima di continuare.

![Stato del circuito e del provider](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a>6. Creare la configurazione di routing
Per istruzioni dettagliate, vedere toohello [configurazione del routing circuito ExpressRoute](expressroute-howto-routing-portal-resource-manager.md) toocreate dell'articolo e modificare peering di circuito.

> [!IMPORTANT]
> Queste istruzioni si applicano solo toocircuits creati con i provider di servizi che offrono servizi di livello 2 di connettività. Se si usa un provider di servizi che offre servizi gestiti di livello 3 (di solito un IP VPN, come MPLS), il provider di connettività configurerà e gestirà il routing per conto dell'utente.
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a>7. Collegare un circuito ExpressRoute di tooan rete virtuale
Successivamente, collegare un circuito ExpressRoute di tooyour rete virtuale. Hello utilizzare [collegamento virtuale reti circuiti tooExpressRoute](expressroute-howto-linkvnet-arm.md) articolo quando si lavora con modello di distribuzione di gestione risorse di hello.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Ottenere lo stato di hello di un circuito ExpressRoute
È possibile visualizzare lo stato di hello di un circuito, selezionarlo. 

![Stato di un circuito ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a>Modifica di un circuito ExpressRoute
È possibile modificare determinate proprietà di un circuito ExpressRoute senza conseguenze per la connettività.

È possibile eseguire hello seguenti senza tempi di inattività:

* Abilitare o disabilitare un componente aggiuntivo ExpressRoute Premium per il circuito ExpressRoute.
* Aumento della larghezza di banda hello del circuito ExpressRoute fornito è la capacità disponibile sulla porta hello. Si noti che il downgrade della larghezza di banda hello di un circuito non è supportato. 
* Modificare hello piano dati a consumo tooUnlimited dati di controllo. Si noti tale piano del controllo modifica hello da dati senza limiti tooMetered che dati non è supportata.
* È possibile abilitare e disabilitare l'opzione *Allow Classic Operations*(Consenti operazioni classiche).

Per ulteriori informazioni su limiti e limitazioni, vedere toohello [domande frequenti su ExpressRoute](expressroute-faqs.md).

toomodify un circuito ExpressRoute, fare clic su hello **configurazione** come illustrato nella figura che segue hello.

![Modificare il circuito](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

È possibile modificare la larghezza di banda hello, SKU, modello di fatturazione e consentire operazioni classiche in Pannello di configurazione hello.

> [!IMPORTANT]
> Potrebbe essere circuito ExpressRoute di hello toorecreate se ha capacità insufficiente sulla porta esistente hello. Se non è presente capacità aggiuntive disponibili in tale posizione non è possibile aggiornare il circuito hello.
>
> È possibile ridurre la larghezza di banda hello di un circuito ExpressRoute senza interruzioni. Il downgrade della larghezza di banda è necessario il circuito ExpressRoute toodeprovision hello e quindi ripetere il provisioning di un nuovo circuito ExpressRoute.
> 
> Disabilitare il componente aggiuntivo premium operazione può non riuscire se si utilizza le risorse che sono maggiori di ciò che è consentito per il circuito standard hello.
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Deprovisioning ed eliminazione di un circuito ExpressRoute
È possibile eliminare il circuito ExpressRoute selezionando hello **eliminare** icona. Si noti hello segue:

* È necessario scollegare tutte le reti virtuali da hello circuito ExpressRoute. Se questa operazione non riesce, controllare se le reti virtuali sono collegate toohello circuito.
* Se il provider del servizio di circuito ExpressRoute di hello lo stato di provisioning **Provisioning** o **provisioning eseguito** è necessario collaborare con il circuito di hello toodeprovision provider del servizio sul relativo lato. Si continuerà tooreserve risorse e a pagamento fino a quando il provider di servizi di hello completa deprovisioning circuito hello e invia una notifica di Microsoft.
* Se il provider di servizi di hello è deprovisioning circuito hello (provider di servizi di hello lo stato di provisioning è stato impostato troppo**non è stato eseguito il provisioning**) è possibile eliminare il circuito hello. Questa operazione arresterà la fatturazione per il circuito hello

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato il circuito, verificare che hello seguenti:

* [Creare e modificare il routing per un circuito ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)
* [Collegamento del circuito ExpressRoute di tooyour di rete virtuale](expressroute-howto-linkvnet-arm.md)

