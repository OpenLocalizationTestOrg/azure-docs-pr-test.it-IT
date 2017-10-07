---
title: aaaError & eccezioni - App Azure per la logica | Documenti Microsoft
description: Modelli per la gestione degli errori e delle eccezioni in App per la logica di Azure
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a>Gestire errori ed eccezioni in App per la logica di Azure

Le app di logica di Azure fornisce strumenti avanzati e toohelp modelli assicurarsi che le integrazioni sono affidabile e resiliente agli errori. Qualsiasi architettura di integrazione pone hello problema del tempo di inattività che tooappropriately handle o problemi da sistemi dipendenti. Gestione degli errori di logica App rende un'esperienza di prima classe, offrendo hello gli strumenti necessari tooact in eccezioni ed errori nei flussi di lavoro.

## <a name="retry-policies"></a>Criteri di ripetizione dei tentativi

Un criterio di ripetizione è di tipo di eccezione e la gestione degli errori di base hello. Se una richiesta iniziale è scaduto oppure non è riuscita (qualsiasi richiesta che comporta un 429 o risposta 5xx), questo criterio definisce se deve ritentare l'azione di hello. Per impostazione predefinita, tutte le azioni vengono ripetute altre 4 volte a intervalli di 20 secondi. Pertanto, se prima richiesta hello riceve un `500 Internal Server Error` risposta, il motore di flusso di lavoro hello sospende per 20 secondi, e tentativi hello richiesta nuovamente. Se dopo tutti i tentativi, risposta hello è ancora un errore o eccezione, il flusso di hello continua e segni di hello stato dell'azione come `Failed`.

È possibile configurare criteri di tentativi in hello **input** per una determinata azione. Ad esempio, è possibile configurare un tootry di criteri di tentativi fino a 4 volte per gli intervalli di 1 ora. Per altre informazioni sulle proprietà di input, vedere [Azioni e trigger del flusso di lavoro][retryPolicyMSDN].

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

Se si desidera il tooretry di azione HTTP 4 volte, attendere 10 minuti tra ogni tentativo di utilizzare hello seguente definizione:

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

Per ulteriori informazioni sulla sintassi supportata, vedere hello [sezione criteri di ripetizione di azioni del flusso di lavoro e i trigger][retryPolicyMSDN].

## <a name="catch-failures-with-hello-runafter-property"></a>Intercettare gli errori con hello RunAfter proprietà

Ogni azione di logica app dichiara le azioni che devono essere completata prima dell'inizio azione hello, ad esempio ordinamento passaggi hello nel flusso di lavoro. Nella definizione di azione hello, questo ordinamento è noto come hello `runAfter` proprietà. Questa proprietà è un oggetto che descrive le azioni e gli stati di azione eseguire l'azione di hello. Per impostazione predefinita, tutte le azioni aggiunte tramite Progettazione applicazione logica hello sono troppo`runAfter` hello precedenza se hello passaggio precedente `Succeeded`. Tuttavia, è possibile personalizzare le azioni toofire questo valore quando le azioni precedenti hanno `Failed`, `Skipped`, o un set di possibili valori sono i seguenti. Se si desiderava tooadd tooa un elemento designato come argomento del Bus di servizio dopo un'azione specifica `Insert_Row` ha esito negativo, è possibile utilizzare hello seguente `runAfter` configurazione:

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

Hello preavviso `runAfter` proprietà viene impostata toofire se hello `Insert_Row` azione `Failed`. azione di hello toorun se è stato dell'azione hello `Succeeded`, `Failed`, o `Skipped`, utilizzare la seguente sintassi:

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> Le azioni eseguite dopo l'esito negativo di un'azione precedente e completate correttamente vengono contrassegnate come `Succeeded`. Ciò significa che se si catch tutti correttamente gli errori in un flusso di lavoro hello eseguito è contrassegnato come `Succeeded`.

## <a name="scopes-and-results-tooevaluate-actions"></a>Azioni tooevaluate ambiti e risultati

Toohow simile è possibile eseguire dopo le singole azioni, è possibile anche raggruppare azioni all'interno di un [ambito](../logic-apps/logic-apps-loops-and-scopes.md), che fungono da un raggruppamento logico di azioni. Gli ambiti sono utili per organizzare le azioni di app logica e per l'esecuzione di valutazioni di aggregazione in stato di hello di un ambito. ambito Hello stesso riceve lo stato dopo aver completato tutte le azioni in un ambito. stato dell'ambito Hello è determinato con hello un'esecuzione agli stessi criteri. Se hello azione finale in un branch di esecuzione è `Failed` o `Aborted`, lo stato di hello è `Failed`.

toofire azioni specifiche per eventuali errori che si sono verificati nell'ambito di hello, è possibile utilizzare `runAfter` con un ambito che è contrassegnato come `Failed`. Se *qualsiasi* azioni nell'ambito di hello non riescono, in esecuzione dopo un ambito ha esito negativo consente di creare una singola azione toocatch errori.

### <a name="getting-hello-context-of-failures-with-results"></a>Ottenere il contesto di hello degli errori relativi a risultati

Sebbene intercettare gli errori di un ambito è utile, è possibile anche toohelp di contesto che è comprendere esattamente le azioni che non è riuscite, ed eventuali errori o codici di stato che sono stati restituiti. Hello `@result()` funzione del flusso di lavoro fornisce un contesto sul risultato di hello di tutte le azioni in un ambito.

`@result()`accetta un singolo parametro, il nome dell'ambito e restituisce una matrice di tutti i risultati dell'azione hello da tale ambito. Questi oggetti azione includono hello stesso gli attributi come hello `@actions()` Genera oggetto, inclusi l'ora di inizio azione, ora di fine di azione, lo stato di azione, input azione, ID di correlazione di azione e azione. contesto toosend di tutte le azioni che non è riuscita in un ambito, può facilmente associare un `@result()` funzione con un `runAfter`.

tooexecute un'azione *per ogni* azione in un ambito che `Failed`tooactions risultati matrice hello filtro che non è riuscita, è possibile associare `@result()` con un  **[filtro matrice](../connectors/connectors-native-query.md)**  azione e un  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  ciclo. È possibile richiedere la matrice dei risultati filtrati hello ed eseguire un'azione per ogni errore utilizzando hello **ForEach** ciclo. Di seguito è riportato un esempio, seguito da una spiegazione dettagliata, che invia una richiesta HTTP POST con il corpo di risposta hello di tutte le azioni che non è nell'ambito di hello `My_Scope`.

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

Di seguito è riportato un toodescribe dettagliata cosa accade:

1. tutte le azioni all'interno di risultato hello tooget `My_Scope`, hello **filtro matrice** filtri azione `@result('My_Scope')`.

2. Hello condizione per **filtro matrice** qualsiasi `@result()` elemento il cui stato uguale troppo`Failed`. Questa condizione filtri matrice hello con tutti i risultati dell'azione da `My_Scope` tooan matrice con solo non è stato possibile risultati dell'azione.

3. Eseguire un **per ogni** azione hello **matrice filtrata** output. Questo passaggio esegue un'azione *per ogni* risultato di azione non riuscita precedentemente filtrato.

    Se non è riuscita un'unica azione nell'ambito di hello, hello azioni in hello `foreach` eseguire una sola volta. 
    Molte azioni non riuscite determinano un'azione per errore.

4. Inviare una richiesta POST HTTP su hello `foreach` elemento corpo della risposta, o `@item()['outputs']['body']`. Hello `@result()` è hello stessa forma di elemento come hello `@actions()` forma e può essere analizzato hello stesso modo.

5. Includere due intestazioni personalizzate con il nome di azione non riuscita hello `@item()['name']` e hello non è stato possibile eseguire client ID rilevamento `@item()['clientTrackingId']`.

Per riferimento, di seguito è riportato un esempio di un singolo `@result()` elemento, che mostra hello `name`, `body`, e `clientTrackingId` le proprietà che vengono analizzate nell'esempio precedente hello. All'esterno di `foreach`, `@result()` restituisce una matrice di questi oggetti.

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

tooperform eccezioni diversi modelli, è possibile utilizzare espressioni di hello illustrate in precedenza. Si potrebbe scegliere tooexecute un'unica eccezione che gestisce l'azione di fuori ambito hello che accetta l'intera matrice filtrata di hello di errori e rimuovere hello `foreach`. È inoltre possibile includere altre proprietà utili da hello `@result()` risposta illustrato in precedenza.

## <a name="azure-diagnostics-and-telemetry"></a>Diagnostica e telemetria di Azure

Hello precedenti sono consigliato toohandle errori ed eccezioni all'interno di un'esecuzione, ma è anche possibile identificare e rispondere tooerrors indipendente di hello eseguito. 
[Diagnostica di Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) fornisce un modo semplice di toosend tutti account di archiviazione Azure tooan di eventi (inclusi tutti gli stati di esecuzione e l'azione) del flusso di lavoro o un Hub di eventi di Azure. tooevaluate gli stati di esecuzione, è possibile monitorare le metriche e i registri di hello o pubblicarli in qualsiasi strumento di monitoraggio che si preferisce. Potenziale è toostream tutti gli eventi di hello tramite Hub di eventi di Azure in [Analitica flusso](https://azure.microsoft.com/services/stream-analytics/). Nel flusso Analitica, è possibile scrivere query in tempo reale disattivare eventuali anomalie, medie o errori da hello i log di diagnostica. Flusso Analitica può facilmente output tooother di origini dati quali code, argomenti, SQL, database Cosmos di Azure e Power BI.

## <a name="next-steps"></a>Passaggi successivi

* [Informazioni su come un cliente ha implementato una solida gestione delle eccezioni con App per la logica di Azure](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [Altri esempi e scenari di app per la logica](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Informazioni su come toocreate automatizzare le distribuzioni per App per la logica](../logic-apps/logic-apps-create-deploy-template.md)
* [Compilare e distribuire app per la logica con Visual Studio](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
