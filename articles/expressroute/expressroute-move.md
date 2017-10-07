---
title: i circuiti ExpressRoute aaaMoving da tooResource classico Manager | Documenti Microsoft
description: "Questa pagina viene fornita una panoramica di ciò che è necessario tooknow sul bridging hello classic e modelli di distribuzione di gestione risorse di hello."
documentationcenter: na
services: expressroute
author: ganesr
manager: carmonm
editor: 
ms.assetid: bdf01217-1a98-4ec0-a08e-d84fd37f78af
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: ganesr
ms.openlocfilehash: c901d2cda01aec409b528d29fc937ac6afaea511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="moving-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model"></a>Lo spostamento di circuiti ExpressRoute da hello classic toohello il modello di distribuzione di gestione risorse
Questo articolo fornisce una panoramica del significato toomove un circuito ExpressRoute di Azure da hello classic toohello modello di distribuzione Azure Resource Manager.

È possibile usare un singola ExpressRoute circuito tooconnect toovirtual reti vengono distribuiti sia nei modelli di distribuzione di gestione risorse hello e hello classico. Un circuito ExpressRoute, indipendentemente dalla modalità di creazione, reti toovirtual ora è possibile collegare tra entrambi i modelli di distribuzione.

![Un circuito ExpressRoute che collega le reti toovirtual in entrambi i modelli di distribuzione](./media/expressroute-move/expressroute-move-1.png)

## <a name="expressroute-circuits-that-are-created-in-hello-classic-deployment-model"></a>Circuiti ExpressRoute che vengono creati nel modello di distribuzione classica hello
Circuiti ExpressRoute che vengono creati nel modello di distribuzione classica hello necessario toobe spostato toohello Gestione risorse distribuzione modello primo tooenable connettività tooboth hello classica e hello Gestione risorse modelli di distribuzione. Non si verificano perdite o interruzioni della connettività durante lo spostamento di una connessione. Tutti i collegamenti di rete circuito virtuale nel modello di distribuzione classica hello (hello nella stessa sottoscrizione e tra sottoscrizioni) vengono mantenuti.

Dopo lo spostamento hello è stata completata correttamente, hello circuito ExpressRoute Cerca, esegue e aspetto esattamente un circuito ExpressRoute creata nel modello di distribuzione di gestione risorse di hello. È ora possibile creare connessioni toovirtual reti nel modello di distribuzione di gestione risorse di hello.

Dopo un circuito ExpressRoute è stato spostato toohello modello di distribuzione di gestione delle risorse, è possibile gestire il ciclo di vita hello di hello circuito ExpressRoute solo utilizzando il modello di distribuzione di gestione risorse di hello. Ciò significa che è possibile eseguire operazioni come aggiunta/aggiornamento/eliminazione di peering, l'aggiornamento delle proprietà circuito (ad esempio la larghezza di banda, SKU e fatturazione di tipo) e l'eliminazione di circuiti solo nel modello di distribuzione di gestione risorse di hello. Sezione toohello seguito circuiti creati nel modello di distribuzione di gestione risorse di hello per ulteriori informazioni su come è possibile gestire i modelli di distribuzione di accesso tooboth, fare riferimento.

Non si dispone di tooinvolve spostare il hello tooperform provider di connettività.

## <a name="expressroute-circuits-that-are-created-in-hello-resource-manager-deployment-model"></a>Circuiti ExpressRoute che vengono creati nel modello di distribuzione di gestione risorse di hello
È possibile abilitare i circuiti ExpressRoute creati in hello Gestione risorse distribuzione modello toobe accessibili da entrambi i modelli di distribuzione. Qualsiasi circuito ExpressRoute nella sottoscrizione può essere abilitato toobe accessibile da entrambi i modelli di distribuzione.

* Circuiti ExpressRoute che sono stati creati nel modello di distribuzione di gestione risorse di hello non dispone del modello di distribuzione classica toohello di accesso per impostazione predefinita.
* Circuiti ExpressRoute che sono stati spostati dal modello di distribuzione di hello distribuzione classica modello toohello Resource manager sono accessibili da entrambi i modelli di distribuzione per impostazione predefinita.
* Un circuito ExpressRoute ha sempre accesso toohello Gestione risorse modello di distribuzione, indipendentemente dal fatto che siano state create in Gestione risorse di hello o un modello di distribuzione classica. Ciò significa che è possibile creare connessioni creare reti toovirtual in hello il modello di distribuzione di gestione risorse seguendo le istruzioni visualizzate in [come reti virtuali toolink](expressroute-howto-linkvnet-arm.md).
* Modello di distribuzione classica toohello di accesso è controllato da hello **allowClassicOperations** parametro hello circuito ExpressRoute.

> [!IMPORTANT]
> Tutte le quote sono documentate nella hello [i limiti del servizio](../azure-subscription-service-limits.md) pagina si applicano. Ad esempio, un circuito standard può avere al massimo 10 collegamenti/connessioni di rete virtuale sia hello classico di modelli di distribuzione di gestione risorse di hello.
> 
> 

## <a name="controlling-access-toohello-classic-deployment-model"></a>Modello di controllo dell'accesso toohello distribuzione classica
È possibile abilitare una singola rete toovirtual toolink di circuito ExpressRoute in entrambi i modelli di distribuzione per l'impostazione hello **allowClassicOperations** parametro di hello circuito ExpressRoute.

Impostazione **allowClassicOperations** tooTRUE consente le reti virtuali toolink entrambi toohello di modelli di distribuzione circuito ExpressRoute. È possibile collegare reti toovirtual nel modello di distribuzione classica hello da linee guida seguenti su [come toolink reti virtuali in hello modello di distribuzione classica](expressroute-howto-linkvnet-classic.md). È possibile collegare reti toovirtual nel modello di distribuzione di gestione risorse di hello da linee guida seguenti su [come toolink reti virtuali in hello il modello di distribuzione di gestione risorse](expressroute-howto-linkvnet-arm.md).

Impostazione **allowClassicOperations** tooFALSE blocchi accedono circuito toohello dal modello di distribuzione classica hello. Tuttavia, vengono conservati tutti i collegamenti di rete virtuale nel modello di distribuzione classica hello. In questo caso, hello circuito ExpressRoute non è visibile nel modello di distribuzione classica hello.

## <a name="supported-operations-in-hello-classic-deployment-model"></a>Operazioni supportate nel modello di distribuzione classica hello
Hello seguente classiche operazioni è supportata in ExpressRoute circuit quando **allowClassicOperations** è impostato tooTRUE:

* Ottenere informazioni sul circuito ExpressRoute.
* Collegamenti di rete virtuale di creazione/aggiornamento/get/eliminazione tooclassic le reti virtuali
* Creare, aggiornare, ottenere o eliminare autorizzazioni dei collegamenti alle reti virtuali per la connettività tra sottoscrizioni.

Non è possibile eseguire dopo operazioni classiche hello quando **allowClassicOperations** è impostato tooTRUE:

* Creare, aggiornare, ottenere o eliminare peering BGP (Border Gateway Protocol) per peering pubblici e privati di Azure e peering Microsoft.
* Eliminare circuiti ExpressRoute.

## <a name="communication-between-hello-classic-and-hello-resource-manager-deployment-models"></a>Comunicazione tra hello classic e modelli di distribuzione di gestione risorse di hello
funge da ponte tra hello classic e modelli di distribuzione di gestione risorse di hello Hello circuito ExpressRoute. Se entrambe le reti virtuali sono collegato toohello il traffico tra macchine virtuali in reti virtuali nel modello di distribuzione classica hello e quelli in reti virtuali in hello Gestione risorse distribuzione modello attraversa ExpressRoute stesso circuito ExpressRoute.

Velocità effettiva aggregata è limitata dalla capacità di velocità effettiva di hello del gateway di rete virtuale hello. Il traffico di immettere le reti del provider di connettività hello o le reti in tali casi. Il flusso del traffico tra reti virtuali hello è completamente indipendente all'interno di rete Microsoft hello.

## <a name="access-tooazure-public-and-microsoft-peering-resources"></a>Accesso tooAzure pubblico e risorse di peering Microsoft
È possibile continuare le risorse tooaccess che in genere sono accessibili tramite peering pubblico di Azure e Microsoft peering senza interruzioni.  

## <a name="whats-supported"></a>Attività supportate
Questa sezione descrive le attività supportate per i circuiti ExpressRoute:

* È possibile usare un singola ExpressRoute circuito tooaccess reti virtuali che vengono distribuiti in hello classic e modelli di distribuzione di gestione risorse di hello.
* È possibile spostare un circuito ExpressRoute da hello classic toohello il modello di distribuzione di gestione risorse. Dopo lo spostamento, hello circuito ExpressRoute Cerca abbia e opera come qualsiasi altro circuito ExpressRoute creata nel modello di distribuzione di gestione risorse di hello.
* È possibile spostare solo il circuito ExpressRoute hello. I gateway VPN, le reti virtuali e i collegamenti del circuito non possono essere spostati con questa operazione.
* Dopo un circuito ExpressRoute è stato spostato toohello modello di distribuzione di gestione delle risorse, è possibile gestire il ciclo di vita hello di hello circuito ExpressRoute solo utilizzando il modello di distribuzione di gestione risorse di hello. Ciò significa che è possibile eseguire operazioni come aggiunta/aggiornamento/eliminazione di peering, l'aggiornamento delle proprietà circuito (ad esempio la larghezza di banda, SKU e fatturazione di tipo) e l'eliminazione di circuiti solo nel modello di distribuzione di gestione risorse di hello.
* funge da ponte tra hello classic e modelli di distribuzione di gestione risorse di hello Hello circuito ExpressRoute. Se entrambe le reti virtuali sono collegato toohello il traffico tra macchine virtuali in reti virtuali nel modello di distribuzione classica hello e quelli in reti virtuali in hello Gestione risorse distribuzione modello attraversa ExpressRoute stesso circuito ExpressRoute.
* La connettività tra sottoscrizioni è supportata in hello classic sia modelli di distribuzione di gestione risorse di hello.
* Dopo aver spostato un circuito ExpressRoute dal modello di hello modello classico toohello Gestione risorse di Azure, è possibile [migrare hello reti virtuali collegate toohello circuito ExpressRoute](expressroute-migration-classic-resource-manager.md).

## <a name="whats-not-supported"></a>Attività non supportate
Questa sezione descrive le attività non supportate per i circuiti ExpressRoute:

* Gestione del ciclo di vita di hello di un circuito ExpressRoute dal modello di distribuzione classica hello.
* Supporto basata sui ruoli di controllo di accesso (RBAC) per il modello di distribuzione classica hello. È possibile eseguire il circuito tooa RBAC controlli nel modello di distribuzione classica hello. Qualsiasi amministratore/coadministrator di sottoscrizione hello possibile collegare o scollegare circuito toohello reti virtuali.

## <a name="configuration"></a>Configurazione
Seguire le istruzioni di hello descritti in [spostare un circuito ExpressRoute da modello di distribuzione di gestione risorse toohello classico hello](expressroute-howto-move-arm.md).

## <a name="next-steps"></a>Passaggi successivi
* [Eseguire la migrazione di hello reti virtuali collegate toohello circuito ExpressRoute da hello classico modello toohello Azure Resource Manager modello](expressroute-migration-classic-resource-manager.md)
* Per informazioni sul flusso di lavoro, vedere [Flussi di lavoro e stati di provisioning di un circuito ExpressRoute](expressroute-workflows.md).
* tooconfigure la connessione ExpressRoute:
  
  * [Creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md)
  * [Configurare il routing](expressroute-howto-routing-arm.md)
  * [Collegare un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-arm.md)

