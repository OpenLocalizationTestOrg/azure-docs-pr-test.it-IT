---
title: aaa "Query di un indice (API REST - ricerca di Azure) | Documenti di Microsoft"
description: Compilare una query di ricerca in ricerca di Azure e usare i parametri toofilter e ordinamento ricerca risultati della ricerca.
services: search
documentationcenter: 
manager: jhubbard
author: ashmaka
ms.assetid: 8b3ca890-2f5f-44b6-a140-6cb676fc2c9c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/12/2017
ms.author: ashmaka
ms.openlocfilehash: 2f12238b8f4b045f536489cfc8766fb68307bbe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-rest-api"></a>Query sull'indice utilizzando hello API REST di ricerca di Azure
> [!div class="op_single_selector"]
>
> * [Panoramica](search-query-overview.md)
> * [Portale](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

Questo articolo viene illustrato come un indice utilizzando tooquery hello [API REST di ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/).

Prima di iniziare questa procedura dettagliata, è necessario avere [creato un indice di Ricerca di Azure](search-what-is-an-index.md) e [averlo popolato con dati](search-what-is-data-import.md). Per informazioni generali, vedere [Funzionamento della ricerca full-text in Ricerca di Azure](search-lucene-query-architecture.md).

## <a name="identify-your-azure-search-services-query-api-key"></a>Identificare la chiave API di query del servizio Ricerca di Azure
Un componente chiave di ogni operazione di ricerca su hello API REST di ricerca di Azure è hello *chiave api* che è stato generato per il servizio di hello è effettuato il provisioning. Disporre di una chiave valida stabilisce relazioni di trust, un singolo per ogni richiesta, tra hello invio hello richiesta e il servizio di hello che la gestisce.

1. toofind le chiavi del servizio api, è possibile accedere in toohello [portale di Azure](https://portal.azure.com/)
2. Pannello del servizio di ricerca di Azure andare tooyour
3. Fare clic sull'icona "Chiavi" hello

Il servizio ha *chiavi amministratore* e *chiavi di query*.

* Il database primario e secondario *chiavi amministratore* concedere diritti completi tooall operazioni, incluso hello possibilità toomanage hello servizio, creare ed eliminare origini di dati, gli indicizzatori e gli indici. Esistono due chiavi in modo che sia possibile continuare chiave secondaria di hello toouse se si decide di tooregenerate hello primary key e viceversa.
* Il *query chiavi* concedere l'accesso in sola lettura tooindexes e documenti e sono in genere distribuite tooclient applicazioni che inviano richieste di ricerca.

Ai fini di hello di query nell'indice, è possibile utilizzare una delle chiavi di query. Le chiavi amministratore utilizzabile anche per le query, ma è necessario usare una chiave di query nel codice dell'applicazione, come segue meglio hello [principio di privilegio minimo](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## <a name="formulate-your-query"></a>Formulare la query
Esistono due modi troppo[l'indice utilizzando hello API REST di ricerca](https://docs.microsoft.com/rest/api/searchservice/Search-Documents). È una richiesta HTTP POST tooissue in cui i parametri di query sono definiti in un oggetto JSON nel corpo della richiesta hello. Hello viceversa è tooissue una richiesta HTTP GET in cui i parametri di query vengono definiti all'interno di hello URL della richiesta. POST contiene più [assoluta limiti](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) sulle dimensioni hello di parametri di query da GET. Per questo motivo, è consigliabile usare POST, a meno di non avere circostanze particolari in cui l'uso di GET potrebbe essere più conveniente.

Per POST e GET, è necessario tooprovide il *nome servizio*, *nome indice*, hello appropriato e *versione API* (versione API corrente hello `2016-09-01` in fase di hello della pubblicazione di questo documento) in hello URL della richiesta. Per ottenere, hello *stringa di query* in hello fine dell'URL hello è possibile fornire parametri di query hello. Per il formato di URL hello, vedere di seguito:

    https://[service name].search.windows.net/indexes/[index name]/docs?[query string]&api-version=2016-09-01

Hello formato per POST è hello stesso, ma con solo api-version nei parametri di stringa di query hello.

#### <a name="example-queries"></a>Query di esempio
Ecco alcuni esempi di query su un indice denominato "hotels". Queste query vengono visualizzate in formato GET e POST.

Eseguire una ricerca hello intero indice per il termine hello "budget" e restituire solo hello `hotelName` campo:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=budget&$select=hotelName&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "budget",
    "select": "hotelName"
}
```

Applicare un filtro toohello indice toofind gli hotel più economica rispetto alla 150 dollari notte e restituire hello `hotelId` e `description`:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$filter=baseRate lt 150&$select=hotelId,description&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "filter": "baseRate lt 150",
    "select": "hotelId,description"
}
```

Cerca nell'intero indice hello, ordine per un campo specifico (`lastRenovationDate`) in ordine decrescente, eseguire i primi due risultati di hello e Mostra solo `hotelName` e `lastRenovationDate`:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=*&$top=2&$orderby=lastRenovationDate desc&$select=hotelName,lastRenovationDate&api-version=2016-09-01

POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
{
    "search": "*",
    "orderby": "lastRenovationDate desc",
    "select": "hotelName,lastRenovationDate",
    "top": 2
}
```

## <a name="submit-your-http-request"></a>Inviare la richiesta HTTP
Dopo aver formulato la query come parte dell'URL della richiesta HTTP (per GET) o del corpo (per POST), è possibile definire le intestazioni delle richieste e inviare la query.

#### <a name="request-and-request-headers"></a>Richiesta e intestazioni della richiesta
È necessario definire due intestazioni della richiesta per GET o tre per POST:

1. Hello `api-key` intestazione deve essere impostata come chiave di query toohello trovato nel passaggio si precedente. È inoltre possibile utilizzare una chiave amministratore come hello `api-key` intestazione, ma è consigliabile utilizzare una chiave di query come esclusivamente garantisce l'accesso in sola lettura tooindexes e documenti.
2. Hello `Accept` intestazione deve essere impostata troppo`application/json`.
3. Per i POST, hello `Content-Type` intestazione deve essere impostata troppo`application/json`.

Per un HTTP GET richiesta toosearch hello "Hotel" indice utilizzando l'API REST ricerca di Azure, utilizzando una query semplice che cerca il termine hello "motel" hello, vedere di seguito:

```
GET https://[service name].search.windows.net/indexes/hotels/docs?search=motel&api-version=2016-09-01
Accept: application/json
api-key: [query key]
```

Ecco hello stessa query di esempio, questa volta utilizzando HTTP POST:

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2016-09-01
Content-Type: application/json
Accept: application/json
api-key: [query key]

{
    "search": "motel"
}
```

Una richiesta di query ha esito positivo comporterà un codice di stato `200 OK` e vengono restituiti i risultati della ricerca hello come JSON nel corpo della risposta hello. Ecco i risultati dei quali hello per hello di sopra di query è simile, presupponendo che l'indice di hotel"hello" viene popolato con i dati di esempio hello in [importazione dei dati in ricerca di Azure tramite API REST di hello](search-import-data-rest-api.md) (si noti che hello JSON è stato formattato per maggiore chiarezza).

```JSON
{
    "value": [
        {
            "@search.score": 0.59600675,
            "hotelId": "2",
            "baseRate": 79.99,
            "description": "Cheapest hotel in town",
            "description_fr": "Hôtel le moins cher en ville",
            "hotelName": "Roach Motel",
            "category": "Budget",
            "tags":["motel", "budget"],
            "parkingIncluded": true,
            "smokingAllowed": true,
            "lastRenovationDate": "1982-04-28T00:00:00Z",
            "rating": 1,
            "location": {
                "type": "Point",
                "coordinates": [-122.131577, 49.678581],
                "crs": {
                    "type":"name",
                    "properties": {
                        "name": "EPSG:4326"
                    }
                }
            }
        }
    ]
}
```

toolearn, visitare sezione "Risposta" hello [ricerca documenti](https://docs.microsoft.com/rest/api/searchservice/Search-Documents). Per altre informazioni su altri codici di stato HTTP che possono essere restituiti in caso di errore, vedere [Codici di stato HTTP (Ricerca di Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).
