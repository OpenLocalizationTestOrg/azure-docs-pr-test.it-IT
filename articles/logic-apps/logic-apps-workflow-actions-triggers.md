---
title: aaaWorkflow azioni e trigger - App Azure per la logica | Documenti Microsoft
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a>Azioni e trigger del flusso di lavoro per App per la logica di Azure

Le app per la logica sono costituite da trigger e da azioni. Sono disponibili sei tipi di trigger. Ogni tipo ha un'interfaccia e un comportamento diversi. È inoltre possibile apprendere altri dettagli, esaminando i dettagli di hello di hello [il linguaggio di definizione del flusso di lavoro](logic-apps-workflow-definition-language.md).  
  
Continuare a leggere toolearn ulteriori informazioni sui trigger e le azioni e come è possibile usarli toobuild logica App tooimprove i processi di business e flussi di lavoro.  
  
### <a name="triggers"></a>Trigger  

Un trigger specifica chiamate hello in grado di avviare un'esecuzione del flusso di lavoro logica app. Di seguito sono due modi diversi di hello tooinitiate un'esecuzione del flusso di lavoro:  
  
-   Un trigger di poll  

-   Un trigger di push - dal chiamante hello [API REST del servizio del flusso di lavoro](https://docs.microsoft.com/rest/api/logic/workflows)  
  
Tutti i trigger contengono questi elementi di livello superiore:  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a>Tipi e input dei trigger  

È possibile usare questi tipi di trigger:
  
-   **Richiesta** \- rende hello logica app un endpoint per è toocall  
  
-   **Recurrence** \- Esegue l'attivazione in base a una pianificazione definita  
  
-   **HTTP**\- Esegue il polling di un endpoint Web HTTP. endpoint HTTP Hello devono essere conformi a contratto di attivazione specifica tooa \- utilizzando un codice 202\-un modello asincrono, oppure tramite la restituzione di una matrice  
  
-   **ApiConnection** \- trigger viene eseguito il polling come hello HTTP, tuttavia, consente di usufruire di hello [API gestita da Microsoft](https://docs.microsoft.com/azure/connectors/apis-list)  
  
-   **HTTPWebhook** \- viene aperto un endpoint, simile toohello manuale trigger, tuttavia, viene inoltre chiamato out tooa tooregister URL specificato e annullare la registrazione  
  
-   **ApiConnectionWebhook** \- opera come hello trigger HTTPWebhook sfruttando hello API gestita da Microsoft       
    Ogni tipo di trigger ha un diverso set di **input** che ne definisce il comportamento.  
  
## <a name="request-trigger"></a>Trigger di richiesta  

Questo trigger opera come un endpoint che si chiamano tramite tooinvoke una richiesta HTTP app logica. Un trigger request è simile a questo esempio:  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

Esiste anche una proprietà facoltativa denominata **schema**:  
  
|Nome dell'elemento|Obbligatorio|Descrizione|  
|----------------|------------|---------------|  
|schema|No|Schema JSON che convalida la richiesta in ingresso hello. È utile per aiutare i passaggi successivi del flusso di lavoro sapere quali tooreference di proprietà.|

tooinvoke questo endpoint, è necessario hello toocall *listCallbackUrl* API. Vedere [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows) (API REST del servizio di flusso di lavoro).  
  
## <a name="recurrence-trigger"></a>Trigger Recurrence  

Un trigger Recurrence viene eseguito in base a una pianificazione definita. Tale trigger può essere simile a questo esempio:  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

Come si può notare, è toorun un modo semplice un flusso di lavoro.  
  
|Nome dell'elemento|Obbligatorio|Descrizione|  
|----------------|------------|---------------|  
|frequency|Sì|La frequenza con cui hello trigger viene eseguito. Usare solo uno di questi possibili valori: second, minute, hour, day, week, month o year|  
|interval|Sì|Intervallo di hello dato frequenza ricorrenza hello|  
|startTime|No|Se viene fornito un valore startTime senza una differenza dall'ora UTC, viene usato tale valore timeZone.|  
|timeZone|no|Se viene fornito un valore startTime senza una differenza dall'ora UTC, viene usato tale valore timeZone.|  
  
È inoltre possibile pianificare un trigger toostart in esecuzione in un determinato hello future. Ad esempio, se si desidera un riepilogo settimanale report ogni lunedì toostart è possibile pianificare hello logica app toostart come ogni lunedì, creando hello seguenti trigger:  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a>Trigger HTTP  

I trigger HTTP il polling di un endpoint specificato e controllare hello risposta toodetermine se il flusso di lavoro hello deve essere eseguito. oggetto di input Hello prende il set di hello di parametri necessari tooconstruct una chiamata HTTP:  
  
|Nome dell'elemento|Obbligatorio|Descrizione|Tipo|  
|----------------|------------|---------------|--------|  
|statico|sì|Può essere uno dei seguenti metodi HTTP hello: GET, POST, PUT, DELETE, PATCH o HEAD|String|  
|Uri|sì|Hello endpoint http o https che viene chiamato. Il valore massimo è di 2 kilobyte.|String|  
|query|No|Oggetto che rappresenta hello query parametri tooadd toohello URL. Ad esempio, `"queries" : { "api-version": "2015-02-01" }` aggiunge `?api-version=2015-02-01` toohello URL.|Oggetto|  
|headers|No|Oggetto che rappresenta ciascuna delle intestazioni di hello inviato toohello richiesta. Ad esempio, tooset hello lingua e il tipo in una richiesta:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|Oggetto|  
|body|No|Oggetto che rappresenta il payload hello inviato toohello endpoint.|Oggetto|  
|retryPolicy|No|Oggetto che consente di personalizzare il comportamento di ripetizione hello 4xx o 5xx errori.|Oggetto|  
|authentication|No|Metodo hello rappresenta hello richiesta deve essere autenticata. Per informazioni dettagliate su questo oggetto, vedere [Autenticazione in uscita dell'Utilità di pianificazione](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Oltre all'utilità di pianificazione, esiste un'altra proprietà supportata: `authority`. Per impostazione predefinita, questo valore è `https://login.windows.net` quando non viene specificato, ma è possibile usare un gruppo di destinatari diverso, ad esempio `https://login.windows\-ppe.net`|Oggetto|  
  
trigger di Hello HTTP richiede hello API HTTP tooconform con toowork un modello specifico e con l'app logica. Richiede hello seguenti campi:  
  
|Response|Descrizione|  
|------------|---------------|  
|Codice di stato|Codice di stato 200 \(OK\) toocause un'esecuzione. Nessun altro codice di stato attiva un'esecuzione.|  
|Intestazione Retry\-after|Numero di secondi fino a quando non esegue il polling nuovamente hello logica app endpoint hello.|  
|Intestazione Location|intervallo di polling successivo hello, Hello toocall URL. Se non specificato, viene utilizzato l'URL originale hello.|  
  
Di seguito sono riportati alcuni esempi di comportamenti diversi a seconda del tipo di richiesta:  
  
|Codice della risposta|Retry\-After|Comportamento|  
|-----------------|----------------|------------|  
|200|\(nessuna\)|Un trigger non valido, nuovo tentativo\-dopo il motore hello necessarie, altrimenti non esegue il polling per la richiesta successiva hello.|  
|202|60|Flusso di lavoro hello non attivano. viene eseguito il tentativo successivo di Hello in un minuto.|  
|200|10|Esecuzione del flusso di lavoro hello e controllare di nuovo per il contenuto di più di 10 secondi.|  
|400|\(nessuna\)|Richiesta non valida, non eseguire il flusso di lavoro hello. Se è presente alcun **criteri di ripetizione** definito, il criterio predefinito hello viene utilizzato. Una volta raggiunto il numero di hello tentativi, il trigger di hello non è più valido.|  
|500|\(nessuna\)|Errore del server, non sono in esecuzione del flusso di lavoro di hello.  Se è presente alcun **criteri di ripetizione** definito, il criterio predefinito hello viene utilizzato. Una volta raggiunto il numero di hello tentativi, il trigger di hello non è più valido.|  
  
output di Hello di un trigger HTTP aspetto simile al seguente:  
  
|Nome dell'elemento|Descrizione|Tipo|  
|----------------|---------------|--------|  
|headers|intestazioni Hello di risposta http hello.|Oggetto|  
|body|corpo Hello di risposta http hello.|Oggetto|  
  
## <a name="api-connection-trigger"></a>Trigger ApiConnection  

Hello API connessione tratta simile toohello HTTP trigger nella funzionalità di base. Tuttavia, i parametri di hello per identificare l'azione di hello sono diversi. Di seguito è fornito un esempio:  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|Nome dell'elemento|Obbligatoria|Tipo|Descrizione|  
|----------------|------------|--------|---------------|  
|host|Sì||Hello ApiApp host gateway e id.|  
|statico|Sì|String|Può essere uno dei seguenti metodi HTTP hello: **ottenere**, **POST**, **inserire**, **eliminare**, **PATCH**, o  **HEAD**|  
|query|No|Oggetto|Rappresenta hello query parametri toobe aggiunto toohello URL. Ad esempio, `"queries" : { "api-version": "2015-02-01" }` aggiunge `?api-version=2015-02-01` toohello URL.|  
|headers|No|Oggetto|Rappresenta singole intestazioni hello che viene inviata una richiesta di toohello di. Ad esempio, tooset hello lingua e il tipo in una richiesta:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|No|Oggetto|Rappresenta il payload hello inviato toohello endpoint.|  
|retryPolicy|No|Oggetto|Consente di comportamento del nuovo tentativo hello toocustomize 4xx o 5xx errori.|  
|authentication|No|Oggetto|Metodo hello rappresenta hello richiesta deve essere autenticata. Per informazioni dettagliate su questo oggetto, vedere [Autenticazione in uscita dell'Utilità di pianificazione](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)|  
  
proprietà Hello per host sono:  
  
|Nome dell'elemento|Obbligatorio|Descrizione|  
|----------------|------------|---------------|  
|api runtimeUrl|Sì|endpoint Hello di hello API gestita.|  
|connection name||Deve essere un parametro di riferimento tooa chiamato `$connection` ed è il nome di hello della connessione di API gestita hello che hello del flusso di lavoro viene utilizzato.|
  
output di Hello di un trigger di connessione API sono:
  
|Nome dell'elemento|Tipo|Descrizione|  
|----------------|--------|---------------|  
|headers|Oggetto|intestazioni Hello di risposta http hello.|  
|body|Oggetto|corpo Hello di risposta http hello.|  
  
## <a name="httpwebhook-trigger"></a>Trigger HTTPWebhook  

verrà visualizzata la trigger HTTPWebhook Hello un endpoint, i trigger manuale di toohello simile, ma hello trigger HTTPWebhook anche effettua una chiamata tooa tooregister URL specificato e annullare la registrazione. Ecco un esempio di come si presenta un trigger HTTPWebhook:  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

Molte di queste sezioni sono facoltativi e il comportamento di hello di hello Webhook dipende da quali sezioni sono fornite o omesso.  
proprietà Hello di un Webhook sono i seguenti:  
  
|Nome dell'elemento|Obbligatorio|Descrizione|  
|----------------|------------|---------------|  
|subscribe|No|Hello in uscita richiesta che viene chiamato quando il trigger di hello viene creato ed esegue la registrazione iniziale hello.|  
|unsubscribe|No|Hello in uscita richiesta quando viene eliminato il trigger di hello.|  
  
-   **La sottoscrizione** è hello chiamata che ha apportato tooevents ascolto toostart in uscita. Questa chiamata inizia con hello si stesso set di parametri che hello azioni HTTP normale. Questa chiamata in uscita viene eseguita qualsiasi hello ora le modifiche del flusso di lavoro in qualsiasi modo, ad esempio, ogni volta che le credenziali di hello vengono eseguito il rollback o modifica i parametri di input del trigger hello.
  
    toosupport questa chiamata è una nuova funzione: `@listCallbackUrl()`. Questa funzione restituisce un URL univoco per il trigger specifico nel flusso di lavoro. Rappresenta l'identificatore univoco di hello per gli endpoint di hello che utilizzano hello servizio REST.  
  
-   **Unsubscribe** viene chiamata quando un'operazione rende questo trigger non valido, tra cui:  
  
    -   L'eliminazione o la disabilitazione di trigger hello  
  
    -   L'eliminazione o la disabilitazione del flusso di lavoro hello  
  
    -   L'eliminazione o la disabilitazione di sottoscrizione hello  
  
    app per la logica Hello chiama automaticamente hello annullare l'azione. Hello parametri di funzione toothis hello stesso come trigger HTTP hello.  
  
    Hello output di trigger HTTPWebhook hello sono hello contenuto della richiesta in ingresso hello:  
  
|Nome dell'elemento|Tipo|Descrizione|  
|-----------------|--------|---------------|  
|headers|Oggetto|intestazioni Hello della richiesta http hello.|  
|body|Oggetto|corpo Hello della richiesta http hello.|  

È possibile specificare i limiti per un'azione di webhook in hello esattamente come [HTTP asincroni limiti](#asynchronous-limits).
  

## <a name="conditions"></a>Condizioni  

Per qualsiasi trigger, è possibile utilizzare uno o più toodetermine condizioni se il flusso di lavoro hello deve essere eseguito o non. ad esempio:  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

In questo caso, hello solo i trigger report durante il flusso di lavoro hello `sendReports` parametro è impostato tootrue. Infine, le condizioni possono fare riferimento a codice di stato hello del trigger hello. È possibile, ad esempio, avviare un flusso di lavoro solo quando il sito Web restituisce un codice di stato 500, come indicato di seguito:
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> Quando un'espressione fa riferimento a codice di stato hello del trigger hello \(in alcun modo\), hello comportamento predefinito \(trigger solo su 200 \(OK\) \) viene sostituito. Ad esempio, se si desidera tootrigger sul codice di stato 200 sia il codice di stato 201, avere tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` come condizione.  
  
## <a name="start-multiple-runs-for-a-request"></a>Avviare più esecuzioni per una richiesta

tookick esterno viene eseguito più volte per una singola richiesta, `splitOn` è utile, ad esempio, quando si desidera toopoll un endpoint che può avere più nuovi elementi tra gli intervalli di polling.
  
Con `splitOn`, si specifica la proprietà hello interno hello payload di risposta che contiene la matrice hello degli elementi, ognuno dei quali si vuole toouse toostart un'esecuzione di trigger hello. Si supponga, ad esempio, che è disponibile un'API che restituisce hello seguente risposta:  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
L'app di logica deve solo contenuto righe hello, pertanto è possibile creare il trigger come in questo esempio:  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
Quindi, nella definizione di flusso di lavoro, hello `@triggerBody().name` restituisce `mycoolrow` per la prima esecuzione, hello e `another row` per la seconda esecuzione hello. Hello trigger output aspetto simile al seguente:  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

Pertanto, se si utilizza `SplitOn`, non è possibile ottenere le proprietà di hello che non rientrano hello matrice, in questo caso, hello `Status` campo.  
  
> [!NOTE]  
> In questo esempio, si usa hello `?` tooavoid in grado di operatore toobe un errore se hello `Rows` proprietà non è presente. 
  
## <a name="single-run-instance"></a>Istanza di esecuzione singola

È possibile configurare i trigger che hanno un incendio tooonly di proprietà ricorrenza se sono state completate tutte le esecuzioni attive. Se una ricorrenza pianificata si verifica mentre è presente un'esecuzione in corso, trigger hello Ignora e attende fino a quando hello successivo pianificato ricorrenza intervallo toocheck nuovamente.

È possibile configurare questa impostazione tramite le opzioni di operazione hello:

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a>Tipi e input  

Esistono molti tipi di azioni, ognuna con un comportamento univoco. Le azioni di raccolta possono contenere diverse altre azioni.

### <a name="standard-actions"></a>Azioni standard  

-   **HTTP** Questa azione chiama un endpoint Web HTTP.  
  
-   **ApiConnection** \- questa azione si comporta come hello azione HTTP, ma utilizza hello API gestita da Microsoft.  
  
-   **ApiConnectionWebhook** \- HTTPWebhook simile, ma utilizza hello API gestita da Microsoft.  
  
-   **Response** \- Questa azione definisce una risposta per una chiamata in ingresso.  
  
-   **Wait** \- Questa semplice azione attende per un intervallo di tempo fisso o fino a un'ora specifica.  
  
-   **Workflow**\- Questa azione rappresenta un flusso di lavoro annidato.  

-   **Function**\- Questa azione rappresenta una funzione di Azure.

### <a name="collection-actions"></a>Azioni di raccolta

-   **Scope** \- Questa azione è un raggruppamento logico di altre azioni.

-   **Condizione** \- questa azione viene valutata un'espressione ed esegue il ramo risultato corrispondente di hello.

-   **ForEach** \- Questa azione di riproduzione a ciclo continuo scorre una matrice ed esegue azioni interne per ogni elemento.

-   **Fino a quando non** \- ciclo verrà eseguito azioni interne fino a quando una condizione risultati tootrue.
  
Ogni tipo di azione ha un set diverso di **input** che definiscono il comportamento di un'azione.  
  
## <a name="http-action"></a>Azione HTTP  

Azioni HTTP chiamano un endpoint specificato e verificare hello risposta toodetermine se hello flusso di lavoro. Hello **input** oggetto prende il set di hello di parametri necessari tooconstruct hello HTTP chiamata:  
  
|Nome dell'elemento|Obbligatoria|Tipo|Descrizione|  
|----------------|------------|--------|---------------|  
|statico|Sì|String|Può essere uno dei seguenti metodi HTTP hello: **ottenere**, **POST**, **inserire**, **eliminare**, **PATCH**, o  **HEAD**|  
|Uri|Sì|String|Hello endpoint http o https che viene chiamato. La lunghezza massima è 2 kilobyte.|  
|query|No|Oggetto|Rappresenta l'URL toohello tooadd i parametri della query hello. Ad esempio, `"queries" : { "api-version": "2015-02-01" }` aggiunge `?api-version=2015-02-01` toohello URL.|  
|headers|No|Oggetto|Rappresenta singole intestazioni hello che viene inviata una richiesta di toohello di. Ad esempio, tooset hello lingua e il tipo in una richiesta:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|No|Oggetto|Rappresenta il payload hello inviato toohello endpoint.|  
|retryPolicy|No|Oggetto|Consente di personalizzare il comportamento di ripetizione hello 4xx o 5xx errori.|  
|operationsOptions|No|String|Definisce il set di hello di toooverride comportamenti speciali.|  
|authentication|No|Oggetto|Metodo hello rappresenta hello richiesta deve essere autenticata. Per informazioni dettagliate su questo oggetto, vedere [Autenticazione in uscita dell'Utilità di pianificazione](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication). Oltre all'utilità di pianificazione, esiste un'altra proprietà supportata, `authority`, che, per impostazione predefinita, è `https://login.windows.net` quando non è specificata, ma è possibile usare un gruppo di destinatari diverso, ad esempio `https://login.windows\-ppe.net`|  
  
Le azioni HTTP \(e di connessione API\) supportano i criteri per i tentativi. Un criterio di ripetizione applica toointermittent errori caratterizzati allo stato HTTP 408 429 e 5xx, eccezioni di connettività tooany inoltre i codici. Questo criterio è descritto l'utilizzo di hello *retryPolicy* oggetto definito come illustrato di seguito:
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
intervallo tra tentativi Hello è specificato in formato ISO 8601 hello. Questo intervallo ha un valore predefinito e il valore minimo di 20 secondi, mentre il valore massimo hello è un'ora. numero di tentativi predefinito e massimo Hello corrisponde a quattro ore. Se non viene specificata definizione dei criteri di ripetizione hello, un `fixed` strategia viene utilizzata con valori di conteggio e l'intervallo di tentativi predefiniti. criteri di ripetizione hello toodisable, impostare il relativo tipo troppo`None`.  
  
Ad esempio, hello azione seguente Ritenta recupero hello ultime notizie su due volte, se si sono verificati errori intermittenti, per un totale di tre esecuzioni, con un ritardo di 30 secondi tra ogni tentativo di:  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a>Modelli asincroni

Per impostazione predefinita, tutte le azioni basate su HTTP supportano il pattern di operazione asincrona standard hello. Pertanto se il server remoto hello indica che la richiesta hello è accettato per l'elaborazione con un codice 202 \(accettato\) risposta, il motore di App per la logica hello mantiene polling specificato nell'intestazione location della risposta hello fino a raggiungere un terminale dell'URL di hello stato \(non\-risposta 202\).  
  
comportamento asincrono di toodisable hello precedentemente descritto, imposta un `DisableAsyncPattern` opzione nell'input azione hello. In questo caso, output di hello dell'azione hello dipende hello iniziale 202 risposta hello server.  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a>Limiti asincroni

Un modello asincrono può essere limitato nel relativo intervallo di tempo specifico tooa durata.  Allo scadere dell'intervallo di tempo hello non abbia raggiunto uno stato terminale, lo stato di hello dell'azione hello verrà contrassegnato `Cancelled` con codice `ActionTimedOut`.  timeout di limite Hello è specificato in formato ISO 8601.  È possibile specificare limiti con hello la seguente sintassi:

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a>Connessione API  

La connessione API è un'azione che fa riferimento a un connettore gestito da Microsoft.
Questa azione richiede una connessione valida tooa di riferimento e per informazioni sull'API hello e i parametri richiesti.

|Nome dell'elemento|Obbligatoria|Tipo|Descrizione|  
|----------------|------------|--------|---------------|  
|host|Sì|Oggetto|Rappresenta informazioni sul connettore hello, ad esempio hello runtimeUrl e riferimento toohello oggetto di connessione|
|statico|Sì|String|Può essere uno dei seguenti metodi HTTP hello: **ottenere**, **POST**, **inserire**, **eliminare**, **PATCH**, o  **HEAD**|  
|path|Sì|String|percorso di Hello dell'operazione hello API.|  
|query|No|Oggetto|Rappresenta l'URL toohello tooadd i parametri della query hello. Ad esempio, `"queries" : { "api-version": "2015-02-01" }` aggiunge `?api-version=2015-02-01` toohello URL.|  
|headers|No|Oggetto|Rappresenta singole intestazioni hello che viene inviata una richiesta di toohello di. Ad esempio, tooset hello lingua e il tipo in una richiesta:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|No|Oggetto|Rappresenta il payload hello inviato toohello endpoint.|  
|retryPolicy|No|Oggetto|Consente di personalizzare il comportamento di ripetizione hello 4xx o 5xx errori.|  
|operationsOptions|No|String|Definisce il set di hello di toooverride comportamenti speciali.|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a>Azione webhook di connessione API

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

È possibile specificare i limiti per un'azione di webhook in hello esattamente come [HTTP asincroni limiti](#asynchronous-limits).
  
## <a name="response-action"></a>Azione di risposta  

Questo tipo di azione contiene il payload della risposta hello da una richiesta HTTP e include un codice di stato, corpo e intestazioni:  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
azione di risposta Hello presenta restrizioni speciali che non si applicano tooother azioni. In particolare:  
  
-   Azioni di risposta non possono essere parallele in una definizione perché è necessaria una richiesta in ingresso toohello di risposta deterministica.  
  
-   Se un'azione di risposta viene raggiunto dopo la richiesta in ingresso hello ha ricevuto una risposta, azione hello viene considerato non riuscito \(conflitto\), e di conseguenza, hello eseguire `Failed`.  
  
-   Un flusso di lavoro con azioni response non può avere `splitOn` nel trigger perché una chiamata genera più esecuzioni. Di conseguenza, si devono essere convalidato quando il flusso di hello è PUT e causa una richiesta non valida.  
  
## <a name="wait-action"></a>Azione wait  

Hello `wait` azione sospende l'esecuzione del flusso di lavoro per l'intervallo specificato "hello". Ad esempio, toowait 15 minuti, è possibile utilizzare questo frammento di codice:  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
In alternativa, toowait fino a un momento specifico, è possibile usare questo esempio:  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> durata dell'attesa Hello può essere specificata sia utilizzando hello **intervallo** oggetto o hello **fino a quando non** oggetto, ma non entrambi.  
  
|Nome|Obbligatoria|Tipo|Descrizione|  
|--------|------------|--------|---------------|  
|interval|No|Oggetto|Hello in base alle quantità di tempo di durata dell'attesa.|  
|interval unit|Sì|String|Uno di questi intervalli: second, minute, hour, day, week, month, year.|  
|interval count|Sì|String|Durata in base alle unità di misura interno determinata hello.|  
|until|No|Oggetto|Hello basata su un punto nel tempo di durata dell'attesa.|  
|until timestamp|Sì|String|Stringa &#124; hello punto nel tempo in formato UTC quando hello attesa scade.|  

## <a name="query-action"></a>Azione di query

Hello `query` azione consente di filtrare una matrice in base a una condizione. Ad esempio, tooselect numeri maggiori di 2, è possibile utilizzare:

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

output di hello Hello `query` azione è una matrice contenente gli elementi dalla matrice di input hello che soddisfano la condizione hello.

> [!NOTE]
> Se nessun valore soddisfano hello `where` condizione, risultato hello è una matrice vuota.

|Nome|Obbligatoria|Tipo|Descrizione|
|--------|------------|--------|---------------|
|from|Sì|Array|Matrice di origine Hello.|
|dove|Sì|String|Hello tooapply tooeach elemento di condizione della matrice di origine hello.|

## <a name="select-action"></a>Seleziona azione

Hello `select` azione consente di ogni elemento della matrice di progetto in un nuovo valore.
Ad esempio, tooconvert una matrice di numeri in una matrice di oggetti, è possibile utilizzare:

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

output di hello Hello `select` azione è una matrice con hello cardinalità stesso come hello matrice di input, con ogni elemento trasformato come definita da hello `select` proprietà. Se l'input di hello è una matrice vuota, hello anche l'output è una matrice vuota.

|Nome|Obbligatoria|Tipo|Descrizione|
|--------|------------|--------|---------------|
|from|Sì|Array|Matrice di origine Hello.|
|seleziona|Sì|Qualsiasi|Hello proiezione tooapply tooeach elemento di matrice di origine hello.|

## <a name="terminate-action"></a>Azione terminate

azione di terminazione Hello interrompe l'esecuzione del hello del flusso di lavoro eseguito, l'interruzione di tutte le azioni in transito e ignorare tutte le azioni rimanenti. Ad esempio, un'esecuzione con lo stato di tooterminate **non riuscito**, è possibile utilizzare hello frammento di codice seguente:

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> Già completate le azioni non sono interessate da hello terminare l'operazione.

|Nome|Obbligatoria|Tipo|Descrizione|
|--------|------------|--------|---------------|
|runStatus|Sì|String|destinazione Hello stato di esecuzione. **Failed** o **Cancelled**.|
|runError|No|Oggetto|dettagli dell'errore Hello. Supportato quando solo **runStatus** è troppo**Failed**.|
|runError code|No|String|Hello eseguire codice di errore.|
|runError message|No|String|Hello eseguire messaggio di errore.|

## <a name="compose-action"></a>Azione compose

Hello Scrivi azione consente di costruire un oggetto arbitrario. output di Hello di hello comporre azione hello risultato della valutazione relativi input. Ad esempio, è possibile utilizzare hello comporre output toomerge azione di più azioni:

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> Hello **comporre** azione può essere utilizzato tooconstruct alcun output, inclusi gli oggetti, matrici e qualsiasi altro tipo supportato da app logica come XML e binario.

## <a name="table-action"></a>azione Tabella

Hello `table` consente tooconvert una matrice di elementi in un **CSV** o **HTML** tabella.

Presumere che @triggerBody() sia

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

E consente di definire come azione hello

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

produrrebbe Hello precedente

<table><thead><tr><th>id</th><th>name</th></tr></thead><tbody><tr><td>0</td><td>mele</td></tr><tr><td>1</td><td>arance</td></tr></tbody></table>"

Nella tabella di hello toocustomize ordine, è possibile specificare colonne hello in modo esplicito. ad esempio:

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

produrrebbe Hello precedente

<table><thead><tr><th>ottenere ID</th><th>Descrizione</th></tr></thead><tbody><tr><td>0</td><td>mele fresche</td></tr><tr><td>1</td><td>arance fresche</td></tr></tbody></table>"

Se hello `from` valore della proprietà è una matrice vuota, l'output di hello è una tabella vuota.

|Nome|Obbligatoria|Tipo|Descrizione|
|--------|------------|--------|---------------|
|from|Sì|Array|Matrice di origine Hello.|
|format|Sì|String|Hello formato, ovvero **CSV** o **HTML**.|
|columns|No|Array|colonne di Hello. Consente a forma di toooverride hello predefinita della tabella hello.|
|intestazione di colonna|No|String|intestazione Hello della colonna hello.|
|valore colonna|Sì|String|valore di Hello della colonna hello.|

## <a name="workflow-action"></a>Azione workflow   

|Nome|Obbligatoria|Tipo|Descrizione|  
|--------|------------|--------|---------------|  
|host id|Sì|String|ID di risorsa Hello del flusso di lavoro hello che si desidera toocall.|  
|host triggerName|Sì|String|nome di Hello del trigger hello che si desidera tooinvoke.|  
|query|No|Oggetto|Rappresenta l'URL toohello tooadd i parametri della query hello. Ad esempio, `"queries" : { "api-version": "2015-02-01" }` aggiunge `?api-version=2015-02-01` toohello URL.|  
|headers|No|Oggetto|Rappresenta singole intestazioni hello che viene inviata una richiesta di toohello di. Ad esempio, tooset hello lingua e il tipo in una richiesta:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`|  
|body|No|Oggetto|Rappresenta il payload di hello inviato toohello endpoint.|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
Viene eseguita una verifica di accesso nel flusso di lavoro hello \(in particolare, i trigger di hello\), ciò significa che è necessario accedere toohello del flusso di lavoro.  
  
Hello di output di hello `workflow` azione si basano su quelle definite nella hello `response` azione nel flusso di lavoro figlio hello. Se non è stato definito uno `response` azione, quindi l'output di hello sono vuoti.  

## <a name="function-action"></a>Azione delle funzioni   

|Nome|Obbligatoria|Tipo|Descrizione|  
|--------|------------|--------|---------------|  
|function id|Sì|String|ID della funzione hello che si desidera tooinvoke risorsa Hello.|  
|statico|No|String|Hello metodo HTTP utilizzato funzione hello tooinvoke. Per impostazione predefinita, è `POST` quando non è specificato.|  
|query|No|Oggetto|Rappresenta l'URL toohello tooadd i parametri della query hello. Ad esempio, `"queries" : { "api-version": "2015-02-01" }` aggiunge `?api-version=2015-02-01` toohello URL.|  
|headers|No|Oggetto|Rappresenta singole intestazioni hello che viene inviata una richiesta di toohello di. Ad esempio, tooset hello lingua e il tipo in una richiesta: `"headers" : { "Accept-Language": "en-us" }`.|  
|body|No|Oggetto|Rappresenta il payload di hello inviato toohello endpoint.|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

Quando si salva hello logica app, si esegue alcuni controlli nella funzione hello a cui fa riferimento:
-   È necessario toohave access toohello (funzione).
-   È consentito solo il trigger HTTP standard o il trigger webhook JSON generico.
-   Non deve essere presente alcuna route definita.
-   Sono consentiti solo i livelli di autorizzazione "funzione" e "anonimo".

URL trigger Hello viene recuperato, memorizzato nella cache e utilizzato in fase di esecuzione. Pertanto, se qualsiasi operazione invalida URL memorizzati nella cache di hello, hello azione ha esito negativo in fase di esecuzione. toowork il problema, salvare la logica app hello nuovamente, che causerà la logica app tooretrieve e memorizzare nella cache di hello trigger URL nuovamente.

## <a name="collection-actions-scopes-and-loops"></a>Azioni di raccolta (ambiti e cicli)

Alcuni tipi di azioni possono contenere azioni. Azioni di riferimento all'interno di una raccolta è possibile fare riferimento direttamente all'esterno di raccolta hello. Se si è definito `http` in un ambito, `@body('http')` è ancora valido in qualsiasi punto del flusso di lavoro. Le azioni all'interno di una raccolta possono `runAfter` solo altre azioni all'interno di hello stessa raccolta.

## <a name="scope-action"></a>Azione scope

Hello `scope` azione consente di raggruppare azioni in un flusso di lavoro in modo logico.

|Nome|Obbligatoria|Tipo|Descrizione|  
|--------|------------|--------|---------------|  
|Azioni|Sì|Oggetto|Azioni interna tooexecute ambito hello|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a>Azione ForEach

Questa azione di riproduzione a ciclo continuo scorre una matrice ed esegue azioni interne per ogni elemento. Per impostazione predefinita, ciclo foreach hello esegue in parallelo (20 le esecuzioni in parallelo alla volta). È possibile impostare regole di esecuzione utilizzando hello `operationOptions` parametro.

|Nome|Obbligatoria|Tipo|Descrizione|  
|--------|------------|--------|---------------|  
|Azioni|Sì|Oggetto|Tooexecute interna azioni all'interno di ciclo hello|
|foreach|Sì|string|Hello matrice tooiterate su|
|operationOptions|no|string|Qualsiasi opzione di operazione per il comportamento. Attualmente supporta solo `sequential` tooexecute iterazioni in modo sequenziale (comportamento predefinito è parallelo)|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a>Azione Until

Questa azione ciclo esegue azioni interne fino a quando una condizione risultati tootrue.

|Nome|Obbligatoria|Tipo|Descrizione|  
|--------|------------|--------|---------------|  
|Azioni|Sì|Oggetto|Tooexecute interna azioni all'interno di ciclo hello|
|expression|Sì|string|Hello espressione tooevaluate dopo ogni iterazione|
|limit|sì|Oggetto|i limiti di Hello per ciclo hello - almeno un limite devono essere definiti|
|count|no|int|Hello limitazione toohello del numero di iterazioni che possono essere eseguite|
|timeout|no|string|timeout di Hello per quanto tempo deve ciclo.  Formato ISO 8601|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a>Condizioni: azione If

Hello `If` azione consente di valutare una condizione ed eseguire un ramo in base che hello espressione troppo`true`.

|Nome|Obbligatoria|Tipo|Descrizione|  
|--------|------------|--------|---------------|  
|Azioni|Sì|Oggetto|Azioni interna tooexecute quando l'espressione restituisce troppo`true`|
|expression|Sì|string|Hello espressione tooevaluate|
|else|no|Oggetto|Azioni interna tooexecute quando l'espressione restituisce troppo`false`|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
Hello nella tabella seguente vengono illustrati esempi di condizioni di utilizzo espressioni in un'azione:  
  
|Valore JSON|Risultato|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|Qualsiasi valore valuterà tootrue provoca toopass questa condizione. Sono supportate solo le espressioni booleane. tooconvert altri tipi tooBoolean, utilizzare le funzioni `empty`, `equals`.|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|Sono supportate le funzioni di confronto. Per questo esempio hello, l'azione di hello viene eseguita solo quando l'output di hello di act1 è maggiore del valore soglia hello.|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|Funzioni delle regole sono inoltre supportati toocreate nidificati espressioni booleane. In questo caso, hello verrà eseguito quando l'output di hello del act1 è superiore alla soglia hello o inferiore a 100.|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|Se una matrice con tutti gli elementi, è possibile utilizzare toocheck funzioni di matrice. In questo caso, hello verrà eseguito quando hello errori matrice è vuota.| 
|`"expression": "parameters('hasSpecialAction')"`|Errore: condizione non valida perché @ è obbligatorio per le condizioni.|  
  
Se una condizione viene valutata correttamente, condizione hello è contrassegnato come `Succeeded`. Le azioni all'interno di uno hello `actions` o `else` oggetti valutare troppo`Succeeded` quando eseguita e ha avuto esito positivo, `Failed` quando eseguita e non è riuscita o `Skipped` quando non viene eseguita tale branch.

## <a name="next-steps"></a>Passaggi successivi

[API REST del servizio flusso di lavoro](https://docs.microsoft.com/rest/api/logic/workflows)
