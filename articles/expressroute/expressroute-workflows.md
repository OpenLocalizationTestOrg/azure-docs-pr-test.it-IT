---
title: aaaWorkflows per la configurazione di un circuito ExpressRoute | Documenti Microsoft
description: Questa pagina vengono illustrati i flussi di lavoro hello per la configurazione di peering e il circuito ExpressRoute
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a>Flussi di lavoro ExpressRoute per provisioning di un circuito e stati di circuito
Questa pagina viene illustrato il provisioning del servizio di hello e routing configurazione dei flussi di lavoro a un livello elevato.

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

Hello figura riportata di seguito e i passaggi corrispondenti mostrano attività hello che è necessario eseguire in ordine toohave un ExpressRoute circuito provisioning end-to-end. 

1. Utilizzare PowerShell tooconfigure un circuito ExpressRoute. Seguire le istruzioni hello hello [circuiti ExpressRoute creare](expressroute-howto-circuit-classic.md) per ulteriori dettagli.
2. Connettività ordine dal provider di servizi di hello. Questo processo varia. Per ulteriori dettagli su come contattare il provider di connettività tooorder connettività.
3. Verificare che il circuito hello sia stato preparato correttamente verificando il circuito ExpressRoute hello provisioning dello stato tramite PowerShell. 
4. Configurare i domini di routing. Se il provider di connettività gestisce il livello 3, configurerà il routing per il circuito. Se il provider di connettività offre solo servizi di livello 2, è necessario configurare il routing per linee guida descritte in hello [requisiti di routing](expressroute-routing.md) e [configurazione del routing](expressroute-howto-routing-classic.md) pagine.
   
   * Abilitare peering privato di Azure, è necessario abilitare questo peer di tooconnect tooVMs / cloud servizi distribuiti nelle reti virtuali.
   * Abilitare peering pubblico di Azure, è necessario abilitare peering pubblico di Azure se si desiderano tooconnect tooAzure servizi ospitati su indirizzi IP pubblici. Si tratta di un tooaccess requisito risorse di Azure se si è scelto di tooenable routing predefinito per il peering privato di Azure.
   * Abilitare Microsoft peering - è necessario abilitare questo tooaccess Office 365 e Dynamics 365. 
     
     > [!IMPORTANT]
     > È necessario assicurarsi che si usa un proxy separato o edge tooconnect tooMicrosoft rispetto a quello che viene utilizzato per hello hello Internet. Utilizzo di hello stesso bordo per ExpressRoute e hello Internet causerà routing asimmetrica e causare interruzioni della connettività di rete.
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. Il collegamento virtuale reti circuiti tooExpressRoute: È possibile collegare il circuito ExpressRoute tooyour reti virtuali. Seguire le istruzioni [toolink reti virtuali](expressroute-howto-linkvnet-arm.md) tooyour circuito. Queste reti virtuali possono essere nella stessa sottoscrizione Azure circuito ExpressRoute hello hello, oppure può essere in una sottoscrizione diversa.

## <a name="expressroute-circuit-provisioning-states"></a>Stati di provisioning del circuito ExpressRoute
Ogni circuito ExpressRoute prevede due stati:

* Stato di provisioning del provider di servizi
* Stato

Status rappresenta lo stato di provisioning di Microsoft. Questa proprietà è impostata tooEnabled quando si crea un circuito Expressroute

stato di provisioning provider di connettività Hello rappresenta lo stato di hello sul lato del provider di connettività hello. Può essere impostato su *NotProvisioned*, *Provisioning* o *Provisioned*. Hello circuito ExpressRoute deve essere in stato di provisioning eseguito per si toobe in grado di toouse è.

### <a name="possible-states-of-an-expressroute-circuit"></a>Stati possibili di un circuito ExpressRoute
In questa sezione elenca gli stati possibili di hello per un circuito ExpressRoute.

**Al momento della creazione**

Verrà visualizzato il circuito ExpressRoute hello in hello seguente non appena è stato eseguito circuito ExpressRoute di hello PowerShell cmdlet toocreate hello.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


**Quando i provider di connettività è nel processo di hello del provisioning del circuito hello**

Verrà visualizzato il circuito ExpressRoute hello in hello seguente non appena è stato passare i provider di connettività toohello chiave servizio hello e avvio hello processo di provisioning.

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


**Quando il provider di connettività è stata completata hello processo di provisioning**

Verrà visualizzato hello in seguito lo stato come provider di connettività hello ha completato il processo di provisioning hello hello il circuito ExpressRoute.

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

Il provisioning e abilitato è hello circuito hello lo stato è possibile solo per si toobe in grado di toouse è. Se si usa un provider di livello 2, è possibile configurare il routing per il circuito solo quando è attivo questo stato.

**Quando il provider di connettività è deprovisioning circuito hello**

Se è stato richiesto il circuito ExpressRoute hello toodeprovision di hello service provider, verrà visualizzato il circuito hello imposta toohello seguente stato dopo che il provider di servizi di hello ha completato hello processo di deprovisioning.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


È possibile scegliere di abilitare toore, se necessario, o eseguire i cmdlet PowerShell circuito hello toodelete.  

> [!IMPORTANT]
> Se si esegue PowerShell cmdlet toodelete hello circuito quando hello ServiceProviderProvisioningState Provisioning o provisioning eseguito operazione hello hello avrà esito negativo. . Prima di lavoro con il circuito ExpressRoute di hello toodeprovision di provider di connettività, quindi eliminare il circuito hello. Microsoft continuerà circuito hello toobill fino a quando non si esegue hello circuito hello toodelete cmdlet di PowerShell.
> 
> 

## <a name="routing-session-configuration-state"></a>Stato di configurazione della sessione di routing
stato di provisioning BGP Hello consente di sapere se sessione BGP hello è stata abilitata in hello Microsoft edge. Hello stato deve essere abilitato per l'utente toobe toouse in grado di hello peering.

È stato della sessione BGP hello toocheck importante soprattutto per il peering Microsoft. In aggiunta toohello BGP stato di provisioning, è un altro stato denominato *stato prefissi pubblici annunciati*. Hello annunciati prefissi pubblici stato deve essere *configurato* dello stato, sia per hello BGP sessione toobe backup e per il routing toowork end-to-end. 

Se hello annunciati stato pubblica prefisso è impostato tooa *convalida necessita* stato sessione BGP hello non è abilitata, come hello annunciati prefissi non corrispondeva hello come numero in uno dei registri di routing hello. 

> [!IMPORTANT]
> Se hello annunciati stato prefissi pubblici *convalida manuale* stato, è necessario aprire un ticket di supporto con [supporto tecnico Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) e dimostrare che si è proprietari di indirizzi IP hello annunciati lungo hello associata numero sistema autonomo.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* Configurare la connessione ExpressRoute.
  
  * [Creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md)
  * [Configurare il routing](expressroute-howto-routing-arm.md)
  * [Collegare un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-arm.md)

