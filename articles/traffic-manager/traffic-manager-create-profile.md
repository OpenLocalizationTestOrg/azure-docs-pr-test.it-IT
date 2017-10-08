---
title: un profilo di Traffic Manager in Azure aaaCreate | Documenti Microsoft
description: Questo articolo viene descritto come toocreate un profilo di Traffic Manager
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: kumud
ms.openlocfilehash: 5cd3d2903552c9a0427da41a73f6f38f6b0afc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-traffic-manager-profile"></a>Creare un profilo di Gestione traffico

In questo articolo viene descritto come un profilo con **priorità** il tipo di routing è possibile creare gli endpoint di tooroute utenti tootwo App Web di Azure. Utilizzando hello **priorità** routing tipo, tutto il traffico sia indirizzato toohello primo endpoint mentre hello in secondo luogo viene mantenuta come backup. Di conseguenza, gli utenti possono essere indirizzati toohello secondo endpoint, se il primo endpoint hello diventa non integro.

In questo articolo, due endpoint di App Web di Azure creato in precedenza sono il profilo di gestione traffico associato toothis appena creato. altre informazioni su come toolearn toocreate gli endpoint di App Web di Azure, visitare hello [pagina della documentazione di App Web di Azure](https://docs.microsoft.com/azure/app-service-web/). È possibile aggiungere qualsiasi endpoint che dispone di un nome DNS ed è raggiungibile tramite hello internet pubblico e che si sta usando l'endpoint di App Web di Azure come esempio.

### <a name="create-a-traffic-manager-profile"></a>Creare un profilo di Gestione traffico
1. Da un browser, accedi toohello [portale di Azure](http://portal.azure.com). Se non si ha già di un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita della durata di un mese](https://azure.microsoft.com/free/). 
2. In hello **Hub** menu, fare clic su **New** > **rete** > **vedere tutti**, fare clic su **traffico Gestione** hello tooopen profilo **profilo di Traffic Manager creare** pannello, quindi fare clic su **crea**.
3. In hello **profilo di Traffic Manager creare** pannello completo come segue:
    1. In **Nome** specificare un nome per il profilo. Questo nome deve toobe univoco all'interno di zona trafficmanager.net hello e restituisce il nome DNS hello <name>, trafficmanager.net che è usato tooaccess profilo di Traffic Manager.
    2. In **il metodo di Routing**selezionare hello **priorità** metodo di routing.
    3. In **sottoscrizione**, selezionare la sottoscrizione di hello desiderato toocreate questo profilo
    4. In **gruppo di risorse**, creare un nuovo tooplace gruppo di risorse di questo profilo.
    5. In **percorso del gruppo di risorse**, selezionare il percorso di hello hello del gruppo di risorse. Questa impostazione fa riferimento il percorso toohello hello del gruppo di risorse e non ha alcun impatto su hello profilo di Traffic Manager che verrà distribuito a livello globale.
    6. Fare clic su **Crea**.
    7. Una volta completata la distribuzione globale di hello del profilo di Traffic Manager, è elencato nel gruppo di risorse corrispondente come una delle risorse di hello.

    ![Creare un profilo di Gestione traffico](./media/traffic-manager-create-profile/Create-traffic-manager-profile.png)

## <a name="add-traffic-manager-endpoints"></a>Aggiungere endpoint di Gestione traffico

1. Nella barra di ricerca del portale hello, cercare hello **profilo di gestione traffico** nome creato nella precedente sezione e fare clic su profilo di gestione traffico di hello in hello hello risultati che hello visualizzato.
2. In hello **profilo di gestione traffico** pannello in hello **impostazioni** fare clic su **endpoint**.
3. In hello **endpoint** pannello in cui è visualizzato, fare clic su **Aggiungi**.
4. In hello **aggiungere endpoint** pannello completo come segue:
    1. In **Tipo** fare clic su **Endpoint di Azure**.
    2. Fornire un **nome** mediante il quale si desidera toorecognize questo endpoint.
    3. In **Tipo di risorsa di destinazione** fare clic su **Servizio app**.
    4. Per **risorsa di destinazione**, fare clic su **scegliere un servizio app** elenco hello tooshow di hello App Web in hello stessa sottoscrizione. In hello **risorse** pannello viene visualizzato, hello di prelievo del servizio App che si desidera tooadd come primo endpoint hello.
    5. In **Priorità** selezionare **1**. In questo modo tutto il traffico verso endpoint toothis se è integro.
    6. Mantenere deselezionata l'opzione **Aggiungi come disabilitato**.
    7. Fare clic su **OK**
5.  Ripetere i passaggi 3 e 4 per endpoint di hello successivo App Web di Azure. Verificare che tooadd con il relativo **priorità** valore impostato in **2**.
6.  Una volta completata l'aggiunta di hello di entrambi gli endpoint, vengono visualizzati in hello **profilo di gestione traffico** pannello con lo stato di monitoraggio **Online**.

    ![Aggiungere un endpoint di Gestione traffico](./media/traffic-manager-create-profile/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Utilizzare il profilo di gestione traffico hello
1.  Nella barra di ricerca del portale hello, cercare hello **profilo di gestione traffico** nome creato nella precedente sezione hello. Nei risultati di hello che vengono visualizzati, fare clic sul profilo di gestione traffico hello.
2. In hello **profilo di gestione traffico** pannello, fare clic su **Panoramica**.
3. Hello **profilo di gestione traffico** pannello viene visualizzato il nome DNS hello del profilo di Traffic Manager appena creato. È utilizzabile da qualsiasi endpoint destra di toohello tooget instradati ai client (ad esempio, passando tooit tramite un browser web) come determinato dal tipo di routing hello. In questo caso, tutte le richieste vengono indirizzato toohello primo endpoint e se Gestione traffico rileva non integro, il traffico hello automaticamente eseguito il failover toohello successivo endpoint.

## <a name="delete-hello-traffic-manager-profile"></a>Eliminare il profilo di Traffic Manager hello
Quando non è più necessario, eliminare il gruppo di risorse hello e profilo di gestione traffico hello creato. toodo in tal caso, selezionare il gruppo di risorse hello hello **profilo di gestione traffico** pannello e fare clic su **eliminare**.

## <a name="next-steps"></a>Passaggi successivi

- Altre informazioni sui [tipi di routing](traffic-manager-routing-methods.md).
- Altre informazioni sui [tipi di endpoint](traffic-manager-endpoint-types.md).
- Altre informazioni sul [monitoraggio degli endpoint](traffic-manager-monitoring.md).



