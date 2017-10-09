---
title: tipi di contenuto aaaHandle - App Azure per la logica | Documenti Microsoft
description: 'Procedura: come App per la logica di Azure gestisce i tipi di contenuto in fase di progettazione e di runtime'
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: cd1f08fd-8cde-4afc-86ff-2e5738cc8288
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: a823249c5388b15ae0aae450b40499b420ea005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="handle-content-types-in-logic-apps"></a>Gestire i tipi di contenuto di app per la logica

Molti tipi diversi di contenuto possono attraversare un'app per la logica, tra cui JSON, XML, file flat e dati binari. Mentre la logica App motore hello supporta tutti i tipi di contenuto, alcune in modo nativo vengono riconosciuti da hello logica App motore. Altri potrebbero richiedere cast o conversioni in base alle esigenze. In questo articolo viene descritto come motore hello gestisce diversi tipi di contenuto e come toocorrectly gestire questi tipi quando necessario.

## <a name="content-type-header"></a>Intestazione Content-Type

toostart in pratica, si esaminerà hello due `Content-Types` che non richiedono una conversione o cast che è possibile utilizzare in un'app di logica: `application/json` e `text/plain`.

## <a name="applicationjson"></a>Application/JSON

motore del flusso di lavoro di Hello si basa su hello `Content-Type` intestazione HTTP chiama la corretta gestione toodetermine hello. Qualsiasi richiesta con tipo di contenuto hello `application/json` viene archiviato e gestito come un oggetto JSON. Per impostazione predefinita, il contenuto JSON può anche essere analizzato senza che sia necessario alcun cast. 

Ad esempio, è stato possibile analizzare una richiesta con l'intestazione del tipo di contenuto hello `application/json ` in un flusso di lavoro utilizzando un'espressione come `@body('myAction')['foo'][0]` valore hello tooget `bar` in questo caso:

```
{
    "data": "a",
    "foo": [
        "bar"
    ]
}
```

Non è necessario alcun cast aggiuntivo. Se si lavora con i dati JSON, ma non contiene un'intestazione specificata, è possibile manualmente eseguirne il cast tooJSON utilizzando hello `@json()` funzione, ad esempio: `@json(triggerBody())['foo']`.

### <a name="schema-and-schema-generator"></a>Schema e generatore di schemi

Hello trigger richiesta consente di tooenter uno schema JSON per il payload di hello tooreceive previsto. Questo schema consente di progettazione hello generare i token, pertanto è possibile utilizzare hello contenuto della richiesta di hello. Se non si dispone di uno schema pronto, selezionare **schema toogenerate payload di esempio utilizzare**, pertanto è possibile generare uno schema JSON da un payload di esempio.

![Schema](./media/logic-apps-http-endpoint/manualtrigger.png)

### <a name="parse-json-action"></a>Azione di "analisi JSON"

Hello `Parse JSON` azione consente di analizzare il contenuto JSON in token descrittivo per l'utilizzo di logica dell'applicazione. Trigger di richiesta toohello simile, questa azione consente di immettere o generare uno schema JSON per contenuto desiderato tooparse hello. Questo strumento rende molto più semplice l'uso di dati da Bus di servizio, Cosmos DB e così via.

![Analizzare JSON](./media/logic-apps-content-type/ParseJSON.png)

## <a name="textplain"></a>Text/plain

Simile troppo`application/json`, i messaggi HTTP ricevuti con hello `Content-Type` intestazione `text/plain` vengono archiviati in formato non elaborato. Inoltre, se questi messaggi sono inclusi in azioni successive senza eseguire il cast, queste richieste passano con l'intestazione `Content-Type`: `text/plain`. Ad esempio, quando si usa un file flat, è possibile che venga visualizzato questo contenuto HTTP come `text/plain`:

```
Date,Name,Address
Oct-1,Frank,123 Ave.
```

Se nell'azione successiva hello, si invia richiesta hello come corpo hello di un'altra richiesta (`@body('flatfile')`), richiesta hello avrebbe un `text/plain` intestazione Content-Type. Se si lavora con i dati che sono testo normale, ma non hanno un'intestazione specificata, è possibile impostare manualmente tootext dati hello utilizzando hello `@string()` funzione, ad esempio: `@string(triggerBody())`.

## <a name="applicationxml-and-applicationoctet-stream-and-converter-functions"></a>Application/xml, Application/octet-stream e funzioni del convertitore

Hello logica App motore mantiene sempre hello `Content-Type` che è stato ricevuto nel hello HTTP richiesta o risposta. Pertanto, se il motore di hello riceve il contenuto con hello `Content-Type` di `application/octet-stream`, e si includono che è contenuto in un'azione successiva senza eseguire il cast, la richiesta in uscita hello è `Content-Type`: `application/octet-stream`. In questo modo, il motore di hello in grado di garantire dati non vada perduti durante lo spostamento tramite flusso di lavoro hello. Tuttavia, lo stato di azione hello (input e output) verrà archiviato in un oggetto JSON come hello sposta lo stato tramite flusso di lavoro hello. Pertanto toopreserve alcuni tipi di dati, il motore di hello converte hello stringa con codifica base64 binaria tooa contenuto con i metadati appropriati che mantiene sia `$content` e `$content-type`, che vengono automaticamente convertiti. 

* `@json()`-esegue il cast di dati troppo`application/json`
* `@xml()`-esegue il cast di dati troppo`application/xml`
* `@binary()`-esegue il cast di dati troppo`application/octet-stream`
* `@string()`-esegue il cast di dati troppo`text/plain`
* `@base64()`-Converte una stringa base64 tooa contenuto
* `@base64toString()`-Converte una stringa con codificata base64 troppo`text/plain`
* `@base64toBinary()`-Converte una stringa con codificata base64 troppo`application/octet-stream`
* `@encodeDataUri()` : codifica una stringa come matrice di byte dataUri
* `@decodeDataUri()` : decodifica un dataUri in una matrice di byte

Ad esempio, se si riceve una richiesta HTTP con `Content-Type`: `application/xml`:

```
<?xml version="1.0" encoding="UTF-8" ?>
<CustomerName>Frank</CustomerName>
```

Si potrebbe eseguire il cast e usarlo in un secondo tempo con un elemento simile a `@xml(triggerBody())` o all'interno di una funzione come `@xpath(xml(triggerBody()), '/CustomerName')`.

## <a name="other-content-types"></a>Altri tipi di contenuto

Altri tipi di contenuto sono supportati e funziona con le app di logica, ma potrebbe essere necessario recuperare manualmente il corpo del messaggio hello dalla decodifica di hello `$content`. Si supponga ad esempio si attiva un `application/x-www-url-formencoded` richiesta where `$content` payload hello codificata come un toopreserve stringa base64 tutti i dati:

```
CustomerName=Frank&Address=123+Avenue
```

Poiché non è richiesta hello in testo normale o JSON, richiesta hello viene archiviato in azione hello come indicato di seguito:

```
...
"body": {
    "$content-type": "application/x-www-url-formencoded",
    "$content": "AAB1241BACDFA=="
}
```

Attualmente, non è una funzione nativa per i dati del form, pertanto è possibile utilizzare questi dati in un flusso di lavoro manualmente l'accesso a dati hello con una funzione come `@string(body('formdataAction'))`. Se si desidera hello richiesta in uscita tooalso hanno hello `application/x-www-url-formencoded` intestazione di tipo di contenuto, è possibile aggiungere il corpo di hello richiesta toohello azione senza casting come `@body('formdataAction')`. Tuttavia, questo metodo funziona solo se il corpo di hello hello solo parametro hello `body` input. Se si tenta di toouse `@body('formdataAction')` in un `application/json` richiesta, verrà generato un errore di runtime perché il corpo codificato hello viene inviato.

