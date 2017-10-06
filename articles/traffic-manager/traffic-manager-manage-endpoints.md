---
title: gli endpoint aaaManage Traffic Manager di Azure | Documenti Microsoft
description: "Questo articolo aiuterà ad aggiungere, rimuovere, abilitare e disabilitare gli endpoint da Gestione traffico di Azure."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: ade2bbc2-35a7-43c5-8001-4698f7254526
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kumud
ms.openlocfilehash: fc65874ae2eaeb6fca5d8c4f33403c258307bdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-disable-enable-or-delete-endpoints"></a>Aggiungere, disabilitare, abilitare o eliminare gli endpoint

funzionalità di App Web Hello in Azure App Service fornisce già funzionalità di routing del traffico round robin per siti Web all'interno di un Data Center, indipendentemente dalla modalità sito Web hello e di failover. Gestione traffico di Azure consente toospecify failover e il routing del traffico round robin per siti Web e i servizi cloud in Data Center diversi. Hello primo passaggio necessario tooprovide che la funzionalità è tooadd hello cloud del sito Web o del servizio endpoint tooTraffic Manager.

È anche possibile disabilitare singoli endpoint che appartengono a un profilo di Gestione traffico. Disabilitazione di un endpoint lascia come parte del profilo di hello, ma il profilo di hello si comporta come se l'endpoint di hello non è incluso in essa contenuti. Questa azione è utile per rimuovere temporaneamente un endpoint che si trova in modalità di manutenzione o è in corso di ridistribuzione. Una volta endpoint hello nuovamente attivo e in esecuzione, può essere attivata.

> [!NOTE]
> Disabilitazione di un endpoint non ha nulla toodo con lo stato di distribuzione in Azure. Un endpoint integro rimane attivo e in grado di tooreceive traffico anche se è disabilitato in Traffic Manager. La disabilitazione di un endpoint in un profilo non influisce sul relativo stato in un altro profilo.

## <a name="tooadd-a-cloud-service-or-an-app-service-endpoint-tooa-traffic-manager-profile"></a>tooadd un servizio cloud o un tooa di endpoint di servizio App profilo di gestione traffico

1. Da un browser, accedi toohello [portale di Azure](http://portal.azure.com).
2. Nella barra di ricerca del portale hello, cercare hello **profilo di gestione traffico** nome che si desidera toomodify e quindi scegliere il profilo di gestione traffico hello in hello risultati che hello visualizzato.
3. In hello **profilo di gestione traffico** pannello in hello **impostazioni** fare clic su **endpoint**.
4. In hello **endpoint** pannello in cui è visualizzato, fare clic su **Aggiungi**.
5. In hello **aggiungere endpoint** pannello completo come segue:
    1. In **Tipo** fare clic su **Endpoint di Azure**.
    2. Fornire un **nome** mediante il quale si desidera toorecognize questo endpoint.
    3. Per **tipo di risorsa di destinazione**, da hello elenco a discesa, scegliere il tipo di risorsa appropriata hello.
    4. Per **risorsa di destinazione**, da hello elenco a discesa, scegliere una risorsa di destinazione appropriata hello tooshow hello elenco risorse hello stessa sottoscrizione in hello **pannello risorse**. In hello **risorse** pannello viene visualizzato, selezione hello servizio che si desidera tooadd come primo endpoint hello.
    5. In **Priorità** selezionare **1**. In questo modo tutto il traffico verso endpoint toothis se è integro.
    6. Mantenere deselezionata l'opzione **Aggiungi come disabilitato**.
    7. Fare clic su **OK**
6.  Ripetere i passaggi 4 e 5 tooadd hello successivo endpoint di Azure. Verificare che tooadd con il relativo **priorità** valore impostato in **2**.
7.  Una volta completata l'aggiunta di hello di entrambi gli endpoint, vengono visualizzati in hello **profilo di gestione traffico** pannello con lo stato di monitoraggio **Online**.

> [!NOTE]
> Dopo l'aggiunta o rimozione di un endpoint da un profilo utilizzando hello *Failover* metodo di routing del traffico, non può essere ordinato l'elenco delle priorità failover hello sono desiderato. È possibile modificare l'ordine di hello di hello elenco priorità Failover nella pagina Configurazione hello. Per ulteriori informazioni, vedere [Configurare il routing del traffico failover](traffic-manager-configure-failover-routing-method.md).

## <a name="toodisable-an-endpoint"></a>toodisable un endpoint

1. Da un browser, accedi toohello [portale di Azure](http://portal.azure.com).
2. Nella barra di ricerca del portale hello, cercare hello **profilo di gestione traffico** nome che si desidera toomodify e quindi scegliere il profilo di gestione traffico hello in hello che i risultati visualizzati.
3. In hello **profilo di gestione traffico** pannello in hello **impostazioni** fare clic su **endpoint**. 
4. Fare clic sull'endpoint che si desidera toodisable, hello e quindi su hello **Endpoint** pannello in cui è visualizzato, fare clic su **modifica**.
5. In hello **Endpoint** pannello, modificare lo stato di endpoint hello troppo**disabilitato**, quindi fare clic su **salvare**.
6. I client continuano endpoint toohello di traffico toosend per durata hello di Time-to-Live (TTL). È possibile modificare hello durata (TTL) nella pagina di configurazione hello di hello profilo di gestione traffico.

## <a name="tooenable-an-endpoint"></a>tooenable un endpoint

1. Da un browser, accedi toohello [portale di Azure](http://portal.azure.com).
2. Nella barra di ricerca del portale hello, cercare hello **profilo di gestione traffico** nome che si desidera toomodify e quindi scegliere il profilo di gestione traffico hello in hello che i risultati visualizzati.
3. In hello **profilo di gestione traffico** pannello in hello **impostazioni** fare clic su **endpoint**. 
4. Fare clic sull'endpoint che si desidera toodisable, hello e quindi su hello **Endpoint** pannello in cui è visualizzato, fare clic su **modifica**.
5. In hello **Endpoint** pannello, modificare lo stato di endpoint hello troppo**abilitato**, quindi fare clic su **salvare**.
6. I client continuano endpoint toohello di traffico toosend per durata hello di Time-to-Live (TTL). È possibile modificare hello durata (TTL) nella pagina di configurazione hello di hello profilo di gestione traffico.

## <a name="toodelete-an-endpoint"></a>toodelete un endpoint

1. Da un browser, accedi toohello [portale di Azure](http://portal.azure.com).
2. Nella barra di ricerca del portale hello, cercare hello **profilo di gestione traffico** nome che si desidera toomodify e quindi scegliere il profilo di gestione traffico hello in hello che i risultati visualizzati.
3. In hello **profilo di gestione traffico** pannello in hello **impostazioni** fare clic su **endpoint**. 
4. Fare clic sull'endpoint che si desidera toodisable, hello e quindi su hello **Endpoint** pannello in cui è visualizzato, fare clic su **modifica**.
5. In hello **Endpoint** pannello, modificare lo stato di endpoint hello troppo**abilitato**, quindi fare clic su **salvare**.


## <a name="next-steps"></a>Passaggi successivi

* [Gestire un profilo di Gestione traffico](traffic-manager-manage-profiles.md)
* [Configure routing methods](traffic-manager-configure-routing-method.md) (Configurare metodi di routing)
* [Risoluzione dei problemi relativi allo stato Danneggiato di Gestione traffico](traffic-manager-troubleshooting-degraded.md)
* [Considerazioni sulle prestazioni di gestione traffico](traffic-manager-performance-considerations.md)
* [Operazioni per Gestione traffico (informazioni di riferimento API REST)](http://go.microsoft.com/fwlink/p/?LinkID=313584)

