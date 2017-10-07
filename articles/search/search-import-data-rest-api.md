---
title: aaa "caricamento di dati (API REST - ricerca di Azure) | Documenti di Microsoft"
description: Informazioni su come indice di tooan tooupload dati in ricerca di Azure tramite hello API REST.
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: 8d0749fb-6e08-4a17-8cd3-1a215138abc6
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 6ba1336012d1f0f6d6d6c933e16aa879afb9b824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-rest-api"></a>Caricamento dati tooAzure ricerca tramite hello API REST
> [!div class="op_single_selector"]
>
> * [Panoramica](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
>
>

In questo articolo viene illustrato come hello toouse [API REST di ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/) tooimport dati in un indice di ricerca di Azure.

Prima di iniziare questa procedura dettagliata, è necessario avere [creato un indice di Ricerca di Azure](search-what-is-an-index.md).

Nei documenti di ordine toopush nell'indice utilizzando l'API REST di hello, vengono emessi endpoint dell'URL del tooyour indice richiesta HTTP POST. corpo Hello di hello richiesta HTTP corpo è un oggetto JSON che contengono i documenti hello toobe aggiunte, modificate o eliminate.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Identificare la chiave API amministratore del servizio Ricerca di Azure
Quando si inviano richieste HTTP per il servizio utilizzando l'API REST di hello *ogni* richiesta API deve includere hello chiave api che è stato generato per hello è effettuato il provisioning del servizio di ricerca. Disporre di una chiave valida stabilisce relazioni di trust, un singolo per ogni richiesta, tra hello invio hello richiesta e il servizio di hello che la gestisce.

1. toofind le chiavi del servizio api, è possibile accedere in toohello [portale di Azure](https://portal.azure.com/)
2. Pannello del servizio di ricerca di Azure andare tooyour
3. Fare clic su hello icona "Chiavi"

Il servizio avrà *chiavi amministratore* e *chiavi di query*.

* Il database primario e secondario *chiavi amministratore* concedere diritti completi tooall operazioni, incluso hello possibilità toomanage hello servizio, creare ed eliminare origini di dati, gli indicizzatori e gli indici. Esistono due chiavi in modo che sia possibile continuare chiave secondaria di hello toouse se si decide di tooregenerate hello primary key e viceversa.
* Il *query chiavi* concedere l'accesso in sola lettura tooindexes e documenti e sono in genere distribuite tooclient applicazioni che inviano richieste di ricerca.

Ai fini di hello di importazione di dati in un indice, è possibile utilizzare la chiave amministratore primaria o secondaria.

## <a name="decide-which-indexing-action-toouse"></a>Decidere quali indicizzazione toouse azione
Quando si utilizza l'API REST di hello, vengono emessi richieste HTTP POST con l'URL dell'endpoint JSON richiesta corpi tooyour ricerca di Azure dell'indice. oggetto JSON Hello nel corpo della richiesta HTTP contiene una matrice JSON denominato "value", che contiene oggetti JSON che rappresenta i documenti di cui si desidera tooadd tooyour indice, aggiornare o eliminare.

Ogni oggetto JSON nella matrice di "value" hello rappresenta un toobe documento indicizzato. Ognuno di questi oggetti contiene la chiave del documento hello e si specifica l'azione di indicizzazione hello desiderato (caricamento, unione, eliminazione e così via). A seconda di quale dei hello si sceglie di azioni riportate di seguito, solo alcuni campi devono essere inclusi per ogni documento:

| @search.action | Descrizione | Campi necessari per ogni documento | Note |
| --- | --- | --- | --- |
| `upload` |Un `upload` tooan simile "upsert" in cui verrà inserito se è nuovo e aggiornato/sostituito se esiste il documento hello è intervento dell'utente. |chiave, oltre a tutti gli altri campi che si desidera toodefine |Durante l'aggiornamento o la sostituzione di un documento esistente, qualsiasi campo che non è specificato nella richiesta di hello avrà il campo impostato troppo`null`. Questo errore si verifica anche quando il campo hello è stato impostato precedentemente valore non null tooa. |
| `merge` |Gli aggiornamenti del documento esistente con hello specificati campi. Se non esiste alcun documento hello nell'indice hello, merge hello avrà esito negativo. |chiave, oltre a tutti gli altri campi che si desidera toodefine |Qualsiasi campo specificato in un'unione sostituirà campo esistente di hello nel documento hello. Sono inclusi anche i campi di tipo `Collection(Edm.String)`. Ad esempio, se hello documento contiene un campo `tags` con valore `["budget"]` e si esegue un'unione con valore `["economy", "pool"]` per `tags`, il valore finale di hello hello `tags` campo sarà `["economy", "pool"]`. e non `["budget", "economy", "pool"]`. |
| `mergeOrUpload` |Questa azione è analoga `merge` se esiste un documento con hello data già chiave nell'indice hello. Se il documento hello non esiste, si comporta come `upload` con un nuovo documento. |chiave, oltre a tutti gli altri campi che si desidera toodefine |- |
| `delete` |Rimozione di documento specificato hello dall'indice di hello. |solo campo chiave |Tutti i campi specificare diverso hello chiave campo verrà ignorato. Se si desidera tooremove un singolo campo da un documento, utilizzare `merge` invece e impostare semplicemente il campo hello in modo esplicito toonull. |

## <a name="construct-your-http-request-and-request-body"></a>Creare la richiesta HTTP e il corpo della richiesta
Ora che i valori dei campi necessari hello raccolti per le operazioni di indice, la richiesta HTTP effettiva di tooconstruct pronto hello e tooimport corpo della richiesta JSON i dati.

#### <a name="request-and-request-headers"></a>Richiesta e intestazioni della richiesta
Nell'URL hello, è necessario tooprovide il nome del servizio, il nome di indice ("Hotel" in questo caso), nonché la versione API appropriata hello (versione API corrente hello `2016-09-01` in fase di hello della pubblicazione di questo documento). Sarà necessario hello toodefine `Content-Type` e `api-key` intestazioni della richiesta. Per quest'ultimo hello, usare una delle chiavi di amministratore del servizio.

    POST https://[search service].search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

#### <a name="request-body"></a>Request Body
```JSON
{
    "value": [
        {
            "@search.action": "upload",
            "hotelId": "1",
            "baseRate": 199.0,
            "description": "Best hotel in town",
            "description_fr": "Meilleur hôtel en ville",
            "hotelName": "Fancy Stay",
            "category": "Luxury",
            "tags": ["pool", "view", "wifi", "concierge"],
            "parkingIncluded": false,
            "smokingAllowed": false,
            "lastRenovationDate": "2010-06-27T00:00:00Z",
            "rating": 5,
            "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
            "@search.action": "upload",
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags": ["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
            "@search.action": "mergeOrUpload",
            "hotelId": "3",
            "baseRate": 129.99,
            "description": "Close tootown hall and hello river"
        },
        {
            "@search.action": "delete",
            "hotelId": "6"
        }
    ]
}
```

In questo caso, si useranno `upload`, `mergeOrUpload` e `delete` come azioni di ricerca.

Si supponga che l'indice "hotels" di esempio sia già popolato con alcuni documenti. Si noti come non è toospecify tutti i campi del documento possibili hello quando si utilizza `mergeOrUpload` e come viene specificata solo la chiave di documento hello (`hotelId`) quando si utilizza `delete`.

Inoltre, si noti che è possibile includere solo i documenti too1000 (o 16 MB) in una singola richiesta di indicizzazione.

## <a name="understand-your-http-response-code"></a>Informazioni sul codice di risposta HTTP
#### <a name="200"></a>200
Dopo l'invio di una richiesta di indicizzazione riuscita, si riceverà una risposta HTTP con codice di stato `200 OK`. il corpo JSON di risposta HTTP hello Hello verrà modificato come segue:

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": true,
            "errorMessage": null
        },
        ...
    ]
}
```

#### <a name="207"></a>207
Quando almeno un elemento non è stato indicizzato correttamente, viene restituito il codice di stato `207` . Hello corpo JSON di risposta HTTP hello conterrà informazioni sui documenti di hello non riuscito.

```JSON
{
    "value": [
        {
            "key": "unique_key_of_document",
            "status": false,
            "errorMessage": "hello search service is too busy tooprocess this document. Please try again later."
        },
        ...
    ]
}
```

> [!NOTE]
> Spesso questo significa che il hello nella ricerca servizio sta raggiungendo un punto in cui le richieste di indicizzazione avranno inizio tooreturn `503` le risposte. In questo caso, è consigliabile interrompere l'invio del codice client e attendere prima di riprovare. Questa query fornirà sistema hello alcuni toorecover tempo, aumentare le opportunità hello che avrà esito positivo richieste future. Ripetizione rapida delle richieste prolungherà semplicemente situazione hello.
>
>

#### <a name="429"></a>429
Il codice di stato `429` saranno restituite quando è stata superata la quota per il numero di hello di documenti per indice.

#### <a name="503"></a>503
Il codice di stato `503` verrà restituito se nessuno degli elementi di hello in hello richiesta sono state indicizzate correttamente. Questo errore indica che sistema hello è sovraccarico e non può elaborare la richiesta in questo momento.

> [!NOTE]
> In questo caso, è consigliabile interrompere l'invio del codice client e attendere prima di riprovare. Questa query fornirà sistema hello alcuni toorecover tempo, aumentare le opportunità hello che avrà esito positivo richieste future. Ripetizione rapida delle richieste prolungherà semplicemente situazione hello.
>
>

Per altre informazioni su azioni sui documenti e risposte di esito positivo/errore, vedere [Aggiungere, aggiornare o eliminare documenti](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents). Per altre informazioni su altri codici di stato HTTP che possono essere restituiti in caso di errore, vedere [Codici di stato HTTP (Ricerca di Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).

## <a name="next-steps"></a>Passaggi successivi
Dopo avere popolato l'indice di ricerca di Azure, sarà pronto toostart emittente toosearch query per i documenti. Per informazioni dettagliate, vedere [Eseguire query su un indice di Ricerca di Azure](search-query-overview.md) .
