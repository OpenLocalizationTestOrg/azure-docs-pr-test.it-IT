---
title: aaaSet di monitoraggio di eventi agli hub di eventi di Azure per le app di logica di Azure | Documenti Microsoft
description: Monitorare gli eventi tooreceive flussi di dati e inviare eventi per le app di logica di Azure con hub eventi di Azure
services: logic-apps
keywords: flusso di dati, monitoraggio eventi, hub eventi
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a>Monitorare, ricevere e inviare eventi con il connettore di hub eventi hello

tooset di un monitoraggio di eventi in modo che l'app logica può rilevare gli eventi, ricevere eventi e inviare eventi, connettersi tooan [Hub di eventi di Azure](https://azure.microsoft.com/services/event-hubs) dall'app logica. Altre informazioni su [Hub eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md).

## <a name="requirements"></a>Requisiti

* Si dispone di toohave un [gli hub di eventi dello spazio dei nomi e Hub eventi](../event-hubs/event-hubs-create.md) in Azure. Informazioni su [come toocreate un hub eventi dello spazio dei nomi e Hub eventi](../event-hubs/event-hubs-create.md). 

* toouse [i connettori](https://docs.microsoft.com/azure/connectors/apis-list) in app logica, è necessario toocreate un'app logica prima. Informazioni su [come un'app di logica toocreate](../logic-apps/logic-apps-create-a-logic-app.md).

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a>Controllare le autorizzazioni dello spazio dei nomi di hub eventi e trovare la stringa di connessione hello

Per i tooaccess app logica qualsiasi servizio, si dispone di toocreate un [ *connessione* ](./connectors-overview.md) tra il logica app hello servizio e, se hai già fatto. Questa connessione, si autorizza i dati di tooaccess logica app.
Per i tooaccess app logica dell'Hub eventi, è necessario toohave **Gestisci** autorizzazioni e la stringa di connessione hello per lo spazio dei nomi dell'hub eventi.

toocheck le autorizzazioni e la stringa di connessione hello get, seguire questi passaggi.

1.  Accedi toohello [portale di Azure](https://portal.azure.com "portale di Azure"). 

2.  Passare gli hub di eventi tooyour *dello spazio dei nomi*, non hello Hub eventi specifico. Nel Pannello di hello dello spazio dei nomi, in **impostazioni**, scegliere **criteri di accesso condiviso**. In **Attestazioni** controllare di avere le autorizzazioni di **gestione** per lo spazio dei nomi.

    ![Gestire le autorizzazioni per lo spazio dei nomi di Hub eventi](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  stringa di connessione di hello toocopy per hello dello spazio dei nomi di hub eventi, scegliere **RootManageSharedAccessKey**. Avanti tooyour primario chiave di stringa di connessione, scegliere il pulsante di copia hello.

    ![Copiare la stringa di connessione dello spazio dei nomi di Hub eventi](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > tooconfirm se la stringa di connessione è associato a uno spazio dei nomi di hub eventi o a un Hub di eventi specifici, verificare la stringa di connessione hello per hello `EntityPath` parametro. Se questo parametro, la stringa di connessione hello è per un Hub eventi specifico "entità" e non è hello stringa corretta toouse con l'app logica.

4.  Ora quando viene chiesto di credenziali dopo l'aggiunta di un'app hub di eventi trigger o azione tooyour logica, è possibile connettersi dello spazio dei nomi di tooyour hub eventi. Assegnare un nome di connessione, immettere stringa di connessione hello copiato e scegliere **crea**.

    ![Immettere la stringa di connessione per lo spazio dei nomi di Hub eventi](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    Dopo aver creato la connessione, nome connessione hello compariranno in hello gli hub di eventi trigger o un'azione. 
    È quindi possibile continuare con gli altri passaggi di logica app hello.

    ![Connessione allo spazio dei nomi di Hub eventi creata](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a>Avviare il flusso di lavoro quando l'hub eventi riceve nuovi eventi

Un [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) è un evento che avvia un flusso di lavoro nell'app per la logica. Per avviare un flusso di lavoro quando i nuovi eventi vengono inviati tooyour Hub eventi, seguire questi passaggi per l'aggiunta di trigger hello in grado di rilevare questo evento.

1.  In hello [portale di Azure](https://portal.azure.com "portale di Azure"), passare tooyour app per la logica esistente o creare un'app logica vuoto.

2.  Nella casella di ricerca hello per hello progettazione applicazione logica, immettere `event hubs` per il filtro. Selezionare il trigger: **Quando sono disponibili eventi nell'hub eventi**

    ![Selezionare il trigger per quando l'hub eventi riceve nuovi eventi](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    Se si dispone già di uno spazio dei nomi di connessione tooyour hub eventi, viene chiesto toocreate ora questa connessione. Assegnare un nome di connessione e immettere la stringa di connessione hello per lo spazio dei nomi dell'hub eventi. 
    Se necessario, informazioni su [come toofind la stringa di connessione](#permissions-connection-string).

    ![Immettere la stringa di connessione per lo spazio dei nomi di Hub eventi](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    Dopo aver creato una connessione di hello, hello le impostazioni per hello **quando un evento in disponibile in un Hub eventi** trigger vengono visualizzati.

    ![Impostazioni del trigger per quando l'hub eventi riceve nuovi eventi](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  Immettere o selezionare il nome di hello per Hub di eventi che si desidera toomonitor hello. Selezionare la frequenza di hello e intervallo per la frequenza con cui toocheck hello Hub eventi.

    > [!TIP]
    > Selezionare un gruppo di consumer per la lettura degli eventi, scegliere di toooptionally **Visualizza le opzioni avanzate**. 

    ![Specificare l'hub eventi o il gruppo di consumer](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    Ora impostati un toostart trigger un flusso di lavoro per l'app logica. 
    Logica app controlla hello specificato Hub eventi in base a una pianificazione hello è impostata. 
    Se l'app consente di individuare nuovi eventi hello Hub eventi, nell'app logica trigger hello esegue altre azioni e trigger.

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a>Inviare gli eventi tooyour Hub eventi dalla tua app di logica

Un'[*azione*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) è un'attività eseguita dal flusso di lavoro dell'app per la logica. Dopo avere aggiunto un'app di logica tooyour trigger, è possibile aggiungere un tooperform operazioni con i dati generati dal trigger. toosend tooyour un evento Hub eventi dalla logica app, seguire questi passaggi.

1.  Nella finestra di progettazione dell'app per la logica scegliere **Nuovo passaggio** > **Aggiungi un'azione** sotto il trigger dell'app per la logica.

    ![Scegliere "Nuovo passaggio" e quindi "Aggiungi un'azione"](./media/connectors-create-api-azure-event-hubs/add-action.png)

    Ora è possibile trovare e selezionare tooperform un'azione. 
    Sebbene sia possibile selezionare qualsiasi azione, per questo esempio, si desidera hello hub eventi azione toosend eventi.

2.  Nella casella di ricerca hello, immettere `event hubs` per il filtro.
Selezionare questa azione: **Invia evento**

    ![Selezionare l'azione "Hub eventi - Invia evento"](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  Immettere i dettagli di hello necessario per l'evento hello, ad esempio nome hello per Hub eventi in cui si desidera evento hello toosend hello. Immettere gli altri dettagli sull'evento hello, ad esempio il contenuto per tale evento facoltativi.

    > [!TIP]
    > toooptionally specificare partizione dell'Hub eventi hello dove toosend hello evento, scegliere **Visualizza le opzioni avanzate**. 

    ![Immettere il nome dell'hub eventi e i dettagli facoltativi dell'evento](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  Salvare le modifiche.

    ![Salvare l'app per la logica](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    A questo punto sono stati impostati gli eventi di toosend un'azione dall'app logica. 

## <a name="connector-specific-details"></a>Dettagli specifici del connettore

Visualizzare tutti i trigger e azioni definite in swagger hello e anche eventuali limiti di hello [dettagli connettore](/connectors/eventhubs/). 

## <a name="get-help"></a>Ottenere aiuto

in caso di altri utenti le app di logica di Azure, vedere tooask domande e rispondere alle domande visitare hello [forum di Azure logica app](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp migliorare App per la logica e i connettori, votare o inviare idee in hello [sito di commenti e suggerimenti dell'utente di App per la logica](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Passaggi successivi

*  [Trovare altri connettori per App per la logica di Azure](./apis-list.md)