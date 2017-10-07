---
title: "metodo di routing tramite Azure Traffic Manager il traffico priorità aaaConfigure | Documenti Microsoft"
description: "Questo articolo viene illustrato come metodo di routing in Traffic Manager il traffico priorità hello tooconfigure"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: dd3e3bb2a727e5ea087cee35962c8e6f7c357282
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-priority-traffic-routing-method-in-traffic-manager"></a>Configurare il metodo di routing del traffico Priorità di Gestione traffico

Indipendentemente dalla modalità sito Web di hello, siti Web di Azure forniscono già funzionalità di failover per siti Web all'interno di un Data Center (noto anche come area). Gestione traffico fornisce failover per i siti Web in diversi data center.

Un modello comune per il failover del servizio è servizio primario di toosend traffico tooa e forniscono un set identico di servizi di backup per il failover. Hello passaggi seguenti illustrano come tooconfigure questa priorità failover con servizi cloud di Azure e siti Web:

## <a name="tooconfigure-hello-priority-traffic-routing-method"></a>metodo routing del traffico tooconfigure hello priorità

1. Da un browser, accedi toohello [portale di Azure](http://portal.azure.com). Se non si ha già di un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita della durata di un mese](https://azure.microsoft.com/free/). 
2. Nella barra di ricerca del portale hello, cercare hello **profili di gestione traffico** e quindi fare clic su nome del profilo hello desiderati come metodo di routing hello tooconfigure per.
3. In hello **profilo di gestione traffico** pannello, verificare che sia hello servizi cloud e siti Web che si desidera tooinclude nella configurazione sono presenti.
4. In hello **impostazioni** fare clic su **configurazione**e in hello **configurazione** pannello completo come segue:
    1. Per **impostazioni del metodo di routing del traffico**, verificare che sia di metodo di routing del traffico hello **priorità**. In caso contrario, fare clic su **priorità** dall'elenco a discesa hello.
    2. Set hello **le impostazioni di monitoraggio Endpoint** identici per tutti i ogni endpoint in questo profilo come indicato di seguito:
        1. Seleziona hello appropriato **protocollo**e specificare hello **porta** numero. 
        2. In **Percorso** immettere una barra */*. toomonitor endpoint, è necessario specificare un percorso e nome file. Barra "/" è una voce valida per il percorso relativo hello e implica che il file hello trovi nella directory radice di hello (impostazione predefinita).
        3. Nella parte superiore di hello della pagina hello, fare clic su **salvare**.
5. In hello **impostazioni** fare clic su **endpoint**.
6. In hello **endpoint** pannello revisione hello di ordine di priorità per gli endpoint. Quando si seleziona hello **priorità** metodo di routing del traffico, hello ordine degli endpoint hello selezionato è rilevante. Verificare l'ordine di priorità hello degli endpoint.  endpoint primario Hello è in primo piano. Fare doppio clic sull'ordine di hello che viene visualizzato. tutte le richieste verranno indirizzati toohello primo endpoint e se Gestione traffico rileva in non integro, il traffico hello automaticamente eseguito il failover toohello successivo endpoint. 
7. toochange hello ordine di priorità dell'endpoint, fare clic sull'endpoint, hello e hello **Endpoint** pannello in cui è visualizzato, fare clic su **modifica** e modificare hello **priorità** valore in base alle esigenze . 
8. Fare clic su **salvare** toosave modificare le impostazioni di endpoint hello.
9. Dopo aver completato le modifiche di configurazione, fare clic su **salvare** nella parte inferiore di hello della pagina hello.
10. Testare le modifiche di hello nella configurazione, come indicato di seguito:
    1.  Nella barra di ricerca del portale hello, cercare il nome del profilo di Traffic Manager hello e scegliere il profilo di gestione traffico hello nei risultati di hello che hello visualizzato.
    2.  In hello **Traffic Manager** profilo pannello, fare clic su **Panoramica**.
    3.  Hello **profilo di gestione traffico** pannello viene visualizzato il nome DNS hello del profilo di Traffic Manager appena creato. È utilizzabile da qualsiasi endpoint destra di toohello tooget instradati ai client (ad esempio, passando tooit tramite un browser web) come determinato dal tipo di routing hello. In questo caso tutte le richieste vengono indirizzato toohello primo endpoint e se Gestione traffico rileva in non integro, il traffico hello automaticamente eseguito il failover toohello successivo endpoint.
11. Dopo avere utilizza profilo di Traffic Manager, modificare il record DNS hello nel toopoint di server DNS autorevole il nome di dominio della società dominio nome toohello Traffic Manager.

![Configurare il metodo di routing del traffico Priorità in Gestione traffico][1]

## <a name="next-steps"></a>Passaggi successivi


- Informazioni sul [metodo di routing del traffico Ponderato](traffic-manager-configure-weighted-routing-method.md).
- Informazioni sul [metodo di routing Prestazioni](traffic-manager-configure-performance-routing-method.md).
- Informazioni sul [metodo di routing Geografico](traffic-manager-configure-geographic-routing-method.md).
- Informazioni su come troppo[verificare le impostazioni di gestione traffico](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-priority-routing-method/traffic-manager-priority-routing-method.png