---
title: aaaCreate web API e le API REST connettori - App Azure per la logica | Documenti Microsoft
description: Creare web API e le API REST toocall i sistemi, servizi o le API nei flussi di lavoro per le integrazioni di sistema con le app di logica di Azure
keywords: API Web, API REST, connettori, flussi di lavoro, integrazioni di sistema
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: bd229179-7199-4aab-bae0-1baf072c7659
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/26/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 2792204d1d298a6f810e75211c1789ee204c2fdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-apis-as-connectors-for-logic-apps"></a>Creare API personalizzate come connettori per app per la logica

Sebbene le app di logica di Azure offre [connettori incorporati 100 +](../connectors/apis-list.md) che è possibile utilizzare nei flussi di lavoro logica app, potrebbe essere necessario toocall API, sistemi e servizi che non sono disponibili come connettori. È possibile creare la propria API personalizzate che forniscono le azioni e trigger toouse in App per la logica. Ecco altri motivi per cui si decide toocreate proprio API troppo utilizzano come i connettori App per la logica:

* Estendere gli attuali flussi di lavoro di integrazione del sistema e integrazione dei dati.
* Consentono ai clienti di usare le attività del servizio toomanage personale o professionale.
* Espandere hello reach, individuazione e utilizzo per il servizio.

In pratica, i connettori sono API Web che usano REST per le interfacce collegabili, il [formato dei metadati Swagger](http://swagger.io/specification/) per la documentazione e JSON come formato di scambio di dati. Poiché i connettori sono API REST che comunicano attraverso endpoint HTTP, è possibile usare qualsiasi linguaggio, ad esempio .NET, Java o Node.js, per la creazione dei connettori. È anche possibile ospitare le API in [Azure App Service](../app-service/app-service-value-prop-what-is.md), un platform-as-a-service (PaaS) offerta che fornisce uno dei modi di hello migliori, più semplici e più scalabili per l'API di hosting. 

Per toowork API personalizzato con la logica App, è possibile fornire l'API [ *azioni* ](./logic-apps-what-are-logic-apps.md#logic-app-concepts) che eseguono attività specifiche nei flussi di lavoro logica app. L'API può anche agire come un [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) che avvia un flusso di lavoro di app per la logica quando nuovi dati o un evento soddisfano una condizione specificata. In questo argomento descrive i modelli comuni che è possibile seguire per la creazione di azioni e trigger dell'API, basato sul comportamento di hello che si desidera tooprovide l'API.

> [!TIP] 
> Sebbene sia possibile distribuire le API come [le app web](../app-service-web/app-service-web-overview.md), è consigliabile distribuire le API come [App per le API](../app-service-api/app-service-api-apps-why-best-platform.md), che può semplificare il lavoro quando si compila, host e utilizzare le API nel cloud hello e in locale. Non si dispone toochange qualsiasi codice nelle API--è sufficiente distribuire l'app per le API tooan di codice. Informazioni su come troppo [compilare App per le API creati con ASP.NET](../app-service-api/app-service-api-dotnet-get-started.md), [Java](../app-service-api/app-service-api-java-api-app.md), o [Node.js](../app-service-api/app-service-api-nodejs-api-app.md). 
>
> Per esempi di API App compilati per App per la logica, visitare hello [repository GitHub di App di Azure logica](http://github.com/logicappsio) o [blog](http://aka.ms/logicappsblog).

## <a name="helpful-tools"></a>Strumenti utili

Un'API personalizzata funziona meglio con logica App quando hello API ha anche un [Swagger documento](http://swagger.io/specification/) che descrive le operazioni e i parametri di hello dell'API.
Molte librerie, ad esempio [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle), può generare automaticamente il file Swagger hello automaticamente. file Swagger di hello tooannotate per i nomi visualizzati, i tipi di proprietà e così via, è inoltre possibile utilizzare [TRex](https://github.com/nihaue/TRex) in modo che il file Swagger funziona bene con applicazioni logica.

<a name="actions"></a>

## <a name="action-patterns"></a>Modelli di azione

Per le attività di tooperform logica App, l'API personalizzata deve fornire [ *azioni*](./logic-apps-what-are-logic-apps.md#logic-app-concepts). Azione tooan esegue il mapping di ogni operazione dell'API. Un'azione di base è un controller che accetta le richieste HTTP e restituisce risposte HTTP. Ad esempio, un'app logica invia un'app web tooyour di richiesta HTTP o app per le API. Restituisce una risposta HTTP dell'app, insieme ai contenuti hello logica app può elaborare.

Per un'azione standard, è possibile scrivere un metodo di richiesta HTTP nell'API e descrivere tale metodo in un file Swagger. È quindi possibile chiamare l'API direttamente con un'[azione HTTP](../connectors/connectors-native-http.md) o un'azione [HTTP + Swagger](../connectors/connectors-native-http-swagger.md). Per impostazione predefinita, le risposte devono essere restituite all'interno di hello [il limite di timeout della richiesta](./logic-apps-limits-and-config.md). 

![Modello di azione standard](./media/logic-apps-create-api-app/standard-action.png)

<a name="pattern-overview"></a>toomake un'app logica attendere l'API Termina attività in esecuzione più lungo, l'API può seguire hello [modello asincrono di polling](#async-pattern) o hello [webhook asincrona modello](#webhook-actions) descritte in questo argomento. Per un'analogia che consente di visualizzare i diversi comportamenti dei modelli, si supponga processo hello per l'ordinamento di una torta personalizzata da un'azienda. modello di polling Hello rispecchia il comportamento di hello in cui viene chiamato azienda hello toocheck ogni 20 minuti se torta hello è pronto. modello webhook Hello rispecchia il comportamento di hello in azienda hello viene richiesto per il numero di telefono in modo che si chiamano quando torta hello è pronto.

Per esempi, visitare hello [repository GitHub App logica](https://github.com/logicappsio). Vedere anche le informazioni sulla [misurazione dell'utilizzo per le azioni](logic-apps-pricing.md).

<a name="async-pattern"></a>

### <a name="perform-long-running-tasks-with-hello-polling-action-pattern"></a>Eseguire attività a esecuzione prolungata con hello polling modello azione

l'API di eseguire attività che è stato possibile eseguire più tempo rispetto a hello toohave [il limite di timeout della richiesta](./logic-apps-limits-and-config.md), è possibile utilizzare il modello di polling asincrona hello. Questo modello presenta l'API di lavoro in un thread separato, ma verrà mantenuto un motore di App per la logica toohello connessione attiva. In questo modo, hello logica app non è scaduta o continuare con il passaggio successivo hello nel flusso di lavoro hello prima che termina l'utilizzo dell'API.

Ecco modello generale hello:

1. Verificare che tale motore hello sa che l'API ha accettato la richiesta di hello e iniziare a lavorare.
2. Quando il motore di hello effettua le richieste successive per lo stato del processo, informare il motore di hello termine dell'attività hello dell'API.
3. Restituire motore toohello dati rilevanti in modo che sia possibile continuare a flusso di lavoro di hello logica app.

<a name="bakery-polling-action"></a>Ora applicare i criteri di polling di toohello azienda analogia precedente hello e si immagini di chiamare un'azienda e ordine di una torta personalizzata per il recapito. il processo di Hello per la torta hello richiede tempo e non si desidera toowait telefono hello mentre azienda hello funziona su torta hello. hosting Hello conferma dell'ordine e si ha una chiamata di ogni 20 minuti per lo stato della torta hello. Dopo 20 minuti, si chiama azienda hello, ma forniscono informazioni che non è prevista la torta e che è necessario chiamare in un'altra 20 minuti. Questo processo avanti e indietro continua fino a quando non si chiama e azienda hello indica che l'ordine è pronto e offre la torta. 

Questo scenario si può mappare al modello di polling. hosting Hello rappresenta API personalizzata, mentre si cliente torta hello, rappresentano il motore di App per la logica hello. Quando il motore di hello chiama l'API con una richiesta, l'API conferma la richiesta di hello e risponde con intervallo di tempo hello quando il motore di hello è possibile controllare lo stato del processo. motore Hello continua a controllare lo stato del processo fino a quando l'API di risposta che il processo di hello viene eseguito e restituisce dati tooyour logica app, che quindi continua del flusso di lavoro. 

![Modello di azione di polling](./media/logic-apps-create-api-app/custom-api-async-action-pattern.png)

Ecco i passaggi specifici hello per le toofollow API, descritto dal punto di vista dell'API di hello:

1. Quando l'API Ottiene lavoro toostart richiesta un HTTP, restituire immediatamente un HTTP `202 ACCEPTED` risposta con hello `location` intestazione descritto più avanti in questo passaggio. Questa risposta consente di hello logica App motore sapere che l'API ottenuto hello richiesta, il payload di richiesta accettata hello (dati di input) e sta elaborando. 
   
   Hello `202 ACCEPTED` risposta deve includere queste intestazioni:
   
   * *Richiesto*: A `location` intestazione che specifica l'URL di tooa hello percorso assoluto in cui il motore di App per la logica hello possibile controllare lo stato del processo dell'API

   * *Parametro facoltativo*: A `retry-after` intestazione che specifica il numero di hello di secondi che hello motore deve attendere prima di archiviare hello `location` URL per lo stato del processo. 

     Per impostazione predefinita, il motore di hello controlla ogni 20 secondi. un intervallo diverso, toospecify includono hello `retry-after` intestazione e hello il numero di secondi al polling successivo hello.

2. Dopo hello specificato passare del tempo, hello logica App motore hello polling `location` lo stato del processo toocheck URL. L'API deve eseguire questi controlli e restituire queste risposte:
   
   * Se il processo di hello viene eseguito, restituisce HTTP `200 OK` risposta, insieme al payload di risposta hello (input per il passaggio successivo hello).

   * Se sta ancora elaborando il processo di hello, restituire un'altra HTTP `202 ACCEPTED` risposta, ma con hello stesse intestazioni di risposta originale hello.

Quando l'API segue questo modello, non è necessario toodo qualsiasi elemento in toocontinue alla definizione del flusso di lavoro di hello logica app controllare lo stato del processo. Quando il motore di hello Ottiene HTTP `202 ACCEPTED` risposta e un valore valido `location` intestazione, hello motore rispetta hello asincrona criterio e controlli hello `location` intestazione fino a quando l'API restituisce una risposta non 202.

> [!TIP]
> Per un esempio di modello asincrono, esaminare questo [esempio di risposta del controller asincrono in GitHub](https://github.com/logicappsio/LogicAppsAsyncResponseSample).

<a name="webhook-actions"></a>

### <a name="perform-long-running-tasks-with-hello-webhook-action-pattern"></a>Eseguire attività a esecuzione prolungata con modello di azione hello webhook

In alternativa, è possibile utilizzare il modello di webhook hello per le attività di lunga durata e l'elaborazione asincrona. Questo modello è hello logica app sospendere e attendere un "callback" toofinish l'API di elaborazione prima di continuare del flusso di lavoro. Questo callback è un POST HTTP che invia un URL tooa messaggio quando si verifica un evento. 

<a name="bakery-webhook-action"></a>Ora applicare i criteri di hello precedente azienda analogia toohello webhook e si immagini di chiamare un'azienda e ordine di una torta personalizzata per il recapito. il processo di Hello per la torta hello richiede tempo e non si desidera toowait telefono hello mentre azienda hello funziona su torta hello. hosting Hello conferma dell'ordine, ma questa volta garantirvi il numero di telefono in modo che si chiamano quando viene eseguita la torta hello. Questa volta, azienda hello indica quando l'ordine è pronto e offre la torta.

Quando si esegue il mapping di questo modello webhook nuovamente, azienda hello rappresenta API personalizzata, mentre, cliente torta hello, rappresentano hello logica App motore. motore Hello chiama l'API con una richiesta e include un URL di "callback".
Quando il processo di hello viene eseguito, l'API utilizza hello URL toonotify hello motore e restituire dati tooyour logica app, che quindi continua del flusso di lavoro. 

Per questo modello, configurare due endpoint sul controller: `subscribe` e `unsubscribe`

*  `subscribe`endpoint: quando l'esecuzione raggiunge l'azione dell'API di flusso di lavoro hello, hello logica App motore hello chiamate `subscribe` endpoint. Questa operazione comporta hello logica app toocreate un URL di callback che l'API archivia e quindi attendere il callback dell'API hello lavoro è stato completato. L'API quindi richiamato con un URL toohello HTTP POST e passa le intestazioni e il contenuto restituito come input toohello logica app.

* `unsubscribe`endpoint: se l'applicazione logica hello in esecuzione viene annullata, hello logica App motore hello chiamate `unsubscribe` endpoint. L'API quindi annullare la registrazione URL callback hello e arrestare i processi in base alle esigenze.

![Modello di azione webhook](./media/logic-apps-create-api-app/custom-api-webhook-action-pattern.png)

> [!NOTE]
> Attualmente, hello logica App progettazione non supporta l'individuazione endpoint webhook tramite Swagger. Per questo motivo, è tooadd un [ **Webhook** azione](../connectors/connectors-native-webhook.md) e specificare l'URL di hello, intestazioni e corpo per la richiesta. Vedere anche [Azioni e trigger del flusso di lavoro](logic-apps-workflow-actions-triggers.md#api-connection-webhook-action). toopass nell'URL callback hello, è possibile utilizzare hello `@listCallbackUrl()` funzione del flusso di lavoro in uno dei campi precedenti hello in base alle esigenze.

> [!TIP]
> Per un esempio di modello webhook, esaminare questo [esempio di trigger webhook in GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs).

<a name="triggers"></a>

## <a name="trigger-patterns"></a>Modelli di trigger

L'API personalizzata può anche agire come un [*trigger*](./logic-apps-what-are-logic-apps.md#logic-app-concepts) che avvia un'app per la logica quando nuovi dati o un evento soddisfano una condizione specificata. Questo trigger può verificare regolarmente, o attendere e restare in ascolto, la presenza di nuovi dati o eventi presso l'endpoint servizio. Se soddisfa i nuovi dati o a un evento hello condizione specificata, in cui viene attivato il trigger di hello che avvia l'app logica hello, che è in ascolto toothat trigger. toostart logica App in questo modo, l'API può seguire hello [ *trigger polling* ](#polling-triggers) o hello [ *webhook trigger* ](#webhook-triggers) modello. Questi modelli sono simili controparti tootheir per [polling azioni](#async-pattern) e [azioni webhook](#webhook-actions). Vedere anche le informazioni sulla [misurazione dell'utilizzo per i trigger](logic-apps-pricing.md).

<a name="polling-triggers"></a>

### <a name="check-for-new-data-or-events-regularly-with-hello-polling-trigger-pattern"></a>Controllo per i nuovi dati o eventi regolarmente con hello polling motivo del trigger

Oggetto *trigger polling* opera analogamente a hello [polling azione](#async-pattern) descritto in precedenza in questo argomento. motore di App per la logica di Hello periodicamente chiama e controlla l'endpoint di trigger hello per nuovi dati o eventi. Se il motore di hello rileva nuovi dati o a un evento che soddisfa la condizione specificata, viene attivato il trigger di hello. Quindi, il motore di hello crea un'istanza di applicazione logica che elabora i dati di hello come input. 

![Modello di trigger di polling](./media/logic-apps-create-api-app/custom-api-polling-trigger-pattern.png)

> [!NOTE]
> Ogni richiesta di polling viene considerata un'esecuzione di azione, anche quando non viene creata alcuna istanza di app per la logica. elaborazione tooprevent hello stessi dati più volte, il trigger deve pulire i dati che è stato già letto e passati toohello logica app.

Ecco i passaggi specifici per un trigger di polling, descritto dal punto di vista dell'API hello:

| Sono stati rilevati nuovi dati o eventi?  | Risposta dell'API | 
| ------------------------- | ------------ |
| Trovato | Restituire un HTTP `200 OK` stato con payload di risposta hello (input per il passaggio successivo). <br/>Questa risposta crea un'istanza di applicazione logica e Avvia flusso di lavoro hello. |
| Non trovato | Restituire uno stato HTTP `202 ACCEPTED` con un'intestazione `location` e un'intestazione `retry-after`. <br/>Per i trigger, hello `location` intestazione deve contenere anche un `triggerState` parametro di query, in genere è "timestamp". L'API è possibile utilizzare questo hello tootrack identificatore ora dell'ultima hello logica app è stata attivata. |

Ad esempio, tooperiodically controllare il servizio per i nuovi file, che è possibile creare un trigger di polling con questi comportamenti:

| La richiesta include `triggerState`? | Risposta dell'API |
| -------------------------------- | -------------|
| No | Restituire un HTTP `202 ACCEPTED` stato oltre a una `location` intestazione con `triggerState` impostare toohello ora corrente e hello `retry-after` too15 intervallo (secondi). |
| Sì | Controllare il servizio per i file aggiunti dopo hello `DateTime` per `triggerState`. |

| Numero di file trovati | Risposta dell'API |
| --------------------- | -------------|
| Singolo file | Restituire un HTTP `200 OK` lo stato e hello payload del contenuto, aggiornare `triggerState` toohello `DateTime` per il file restituito hello e impostare `retry-after` too15 intervallo (secondi). |
| File multipli | Ripristinare un file contemporaneamente e un HTTP `200 OK` lo stato, l'aggiornamento `triggerState`e set hello `retry-after` too0 intervallo (secondi). </br>Questi passaggi informare il motore di hello che sono disponibili più dati e tale motore hello deve richiedere immediatamente dati hello dall'URL hello in hello `location` intestazione. |
| Nessun file | Restituire un HTTP `202 ACCEPTED` stato, non modificare `triggerState`e set hello `retry-after` too15 intervallo (secondi). |

> [!TIP]
> Per un esempio di modello di trigger di polling, vedere questo [esempio di controller di trigger di polling in GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/PollTriggerController.cs).

<a name="webhook-triggers"></a>

### <a name="wait-and-listen-for-new-data-or-events-with-hello-webhook-trigger-pattern"></a>Attendere e attendono gli eventi con modello di trigger webhook hello o nuovi dati

Un trigger webhook è un *trigger di push* che attende e resta in ascolto di nuovi dati o eventi in corrispondenza dell'endpoint servizio. Se i nuovi dati o a un evento soddisfa hello condizione, viene attivato trigger hello specificata e crea un'istanza di applicazione logica, che quindi elabora dati hello come input.
I trigger Webhook agiscono simile hello [azioni webhook](#webhook-actions) precedentemente descritto in questo argomento e sono impostati con `subscribe` e `unsubscribe` gli endpoint. 

* `subscribe`endpoint: quando si aggiungono e si salva un trigger webhook nell'app logica, hello logica App motore hello chiamate `subscribe` endpoint. Questa operazione comporta hello logica app toocreate un URL di callback che archivia l'API. Se non esistono nuovi dati o un evento che soddisfa hello condizione specificata, l'API chiama con un URL toohello HTTP POST. le intestazioni e payload contenuto hello passano come input toohello logica app.

* `unsubscribe`endpoint: se viene eliminato il trigger di webhook hello o tutta la logica app, App per la logica hello motore hello chiamate `unsubscribe` endpoint. L'API quindi annullare la registrazione URL callback hello e arrestare i processi in base alle esigenze.

![Modello di trigger webhook](./media/logic-apps-create-api-app/custom-api-webhook-trigger-pattern.png)

> [!NOTE]
> Attualmente, hello logica App progettazione non supporta l'individuazione endpoint webhook tramite Swagger. Per questo motivo, è tooadd un [ **Webhook** trigger](../connectors/connectors-native-webhook.md) e specificare l'URL di hello, intestazioni e corpo per la richiesta. Vedere anche [Trigger HTTPWebhook](logic-apps-workflow-actions-triggers.md#httpwebhook-trigger). toopass nell'URL callback hello, è possibile utilizzare hello `@listCallbackUrl()` funzione del flusso di lavoro in uno dei campi precedenti hello in base alle esigenze.
>
> elaborazione tooprevent hello stessi dati più volte, il trigger deve pulire i dati che è stato già letto e passati toohello logica app.

> [!TIP]
> Per un esempio di modello webhook, esaminare questo [esempio di controller di trigger webhook in GitHub](https://github.com/logicappsio/LogicAppTriggersExample/blob/master/LogicAppTriggers/Controllers/WebhookTriggerController.cs).

## <a name="deploy-call-and-secure-custom-apis"></a>Distribuire, chiamare e proteggere le API personalizzate

Dopo aver creato le API personalizzate, impostare le API per la distribuzione in modo da chiamarle in modo sicuro. Informazioni su come troppo[distribuire, chiamare e proteggere le API personalizzate per la logica app](./logic-apps-custom-hosted-api.md).

## <a name="publish-custom-apis-tooazure"></a>Pubblicare tooAzure API personalizzato

toomake le API personalizzate disponibili per l'uso pubblico in Azure, inviare il toohello le candidature [programma Microsoft Azure Certified](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/).

## <a name="get-help"></a>Ottenere aiuto

Per assistenza specifica per le API personalizzate, contattare [customapishelp@microsoft.com](mailto:customapishelp@microsoft.com).

in caso di altri utenti le app di logica di Azure, vedere tooask domande e rispondere alle domande visitare hello [forum di Azure logica app](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp migliorare App per la logica e i connettori, votare o inviare idee in hello [sito di commenti e suggerimenti dell'utente di App per la logica](http://aka.ms/logicapps-wish). 

## <a name="next-steps"></a>Passaggi successivi

* [Misurazione dell'utilizzo per azioni e trigger](logic-apps-pricing.md)
* [Gestire i tipi di contenuti](./logic-apps-content-type.md)
* [Gestire errori ed eccezioni](./logic-apps-exception-handling.md)
* [Proteggere l'accesso alle App per la logica tooyour](./logic-apps-securing-a-logic-app.md)
* [Chiamare, attivare o annidare le app per la logica con endpoint HTTP](./logic-apps-http-endpoint.md)