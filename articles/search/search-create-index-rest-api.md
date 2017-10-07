---
title: aaa "creare un indice (API REST - ricerca di Azure) | Documenti di Microsoft"
description: Creare un indice nel codice utilizzando hello API REST HTTP ricerca di Azure.
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: ac6c5fba-ad59-492d-b715-d25a7a7ae051
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: 117ab64a9874a443351a8a02a9b959b8f7beb7c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-rest-api"></a>Creare un indice di ricerca di Azure mediante l'API REST hello
> [!div class="op_single_selector"]
>
> * [Panoramica](search-what-is-an-index.md)
> * [Portale](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
>
>

In questo articolo verrà illustrati il processo di hello di creazione di una ricerca di Azure [indice](https://docs.microsoft.com/rest/api/searchservice/Create-Index) utilizzando hello API REST di ricerca di Azure.

Prima di seguire le indicazioni di questa guida e creare un indice, è necessario [creare un servizio Ricerca di Azure](search-create-service-portal.md).

toocreate un indice di ricerca di Azure mediante hello API REST, si rilascia un singolo POST HTTP richiesta tooyour ricerca di Azure URL dell'endpoint del servizio. Definizione dell'indice sarà contenuta nel corpo della richiesta hello come contenuto JSON in formato corretto.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Identificare la chiave API amministratore del servizio Ricerca di Azure
Ora che è stato effettuato il provisioning di un servizio di ricerca di Azure, è possibile eseguire le richieste HTTP con endpoint dell'URL del servizio utilizzando l'API REST hello. *Tutti* le richieste API devono includere hello chiave api che è stato generato per hello è effettuato il provisioning del servizio di ricerca. Disporre di una chiave valida stabilisce relazioni di trust, un singolo per ogni richiesta, tra hello invio hello richiesta e il servizio di hello che la gestisce.

1. toofind chiavi di api del servizio è necessario accedere a hello [portale di Azure](https://portal.azure.com/)
2. Pannello del servizio di ricerca di Azure andare tooyour
3. Fare clic su hello icona "Chiavi"

Il servizio avrà *chiavi amministratore* e *chiavi di query*.

* Il database primario e secondario *chiavi amministratore* concedere diritti completi tooall operazioni, incluso hello possibilità toomanage hello servizio, creare ed eliminare origini di dati, gli indicizzatori e gli indici. Esistono due chiavi in modo che sia possibile continuare chiave secondaria di hello toouse se si decide di tooregenerate hello primary key e viceversa.
* Il *query chiavi* concedere l'accesso in sola lettura tooindexes e documenti e sono in genere distribuite tooclient applicazioni che inviano richieste di ricerca.

Ai fini di hello di creazione di un indice, è possibile utilizzare la chiave amministratore primaria o secondaria.

## <a name="define-your-azure-search-index-using-well-formed-json"></a>Definire l'indice di Ricerca di Azure usando JSON ben formato
Un singolo servizio tooyour di richiesta HTTP POST verrà creato l'indice. Hello corpo della richiesta POST HTTP contiene un singolo oggetto JSON che definisce l'indice di ricerca di Azure.

1. Hello prima proprietà dell'oggetto JSON è il nome di hello dell'indice.
2. Hello seconda proprietà dell'oggetto JSON è una matrice JSON denominata `fields` che contiene un oggetto JSON separato per ogni campo nell'indice. Ognuno di questi oggetti JSON contengono più coppie nome/valore per ogni hello degli attributi del campo incluso "name", "tipo" e così via.

È importante tenere le esigenze di business e di esperienza utente ricerca presenti quando si progetta l'indice di ogni campo deve essere assegnato hello [agli attributi](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Questi attributi controllano la cui funzionalità (applicazione di filtri, facet, ordinamento, ricerca full-text e così via) di ricerca si applicano toowhich campi. Per un attributo che non viene specificato, predefinito hello sarà funzionalità di ricerca tooenable hello corrispondente a meno che non si disabilitare in modo specifico.

All'indice di esempio è stato assegnato il nome "hotels" e i campi sono stati definiti come segue:

```JSON
{
    "name": "hotels",  
    "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false, "sortable": false, "facetable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String", "facetable": false},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean", "sortable": false},
        {"name": "smokingAllowed", "type": "Edm.Boolean", "sortable": false},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
    ]
}
```

Con attenzione, abbiamo scelto hello indicizzare gli attributi per ogni campo in base a come si ritiene che verranno utilizzati in un'applicazione. Ad esempio, `hotelId` è una chiave univoca che agli utenti di eseguire la ricerca non sapranno hotel probabile, in modo verrà disabilitata la ricerca full-text per il campo impostando `searchable` troppo`false`, che consente di risparmiare spazio nell'indice hello.

Si noti che un solo campo nell'indice di tipo `Edm.String` deve essere hello designata come campo di hello 'key'.

definizione dell'indice Hello precedente Usa un analizzatore di lingua per hello `description_fr` campo perché è testo francese toostore desiderato. Vedere [argomento supporto lingua di hello](https://docs.microsoft.com/rest/api/searchservice/Language-support) nonché hello corrispondente [post di blog](https://azure.microsoft.com/blog/language-support-in-azure-search/) per ulteriori informazioni sugli analizzatori di linguaggio.

## <a name="issue-hello-http-request"></a>Richiesta di rilascio hello HTTP
1. Usando la definizione dell'indice come corpo della richiesta hello, emettere un URL di endpoint servizio di ricerca di Azure POST HTTP richiesta tooyour. Nell'URL hello, essere toouse che il nome del servizio come nome host hello e inserire hello corretto `api-version` come parametro di stringa di query (versione API corrente hello `2016-09-01` in fase di hello della pubblicazione di questo documento).
2. Nelle intestazioni di richiesta hello, specificare hello `Content-Type` come `application/json`. È necessario anche tooprovide chiave di amministrazione del servizio identificati nel passaggio I hello `api-key` intestazione.

Sarà necessario tooprovide proprio nome e l'api tooissue chiave hello richiesta di servizio seguente:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [api-key]


Per una richiesta riuscita, verrà visualizzato il codice di stato 201 (Creato). Per ulteriori informazioni sulla creazione di un indice tramite l'API REST di hello, visitare hello [qui riferimento all'API](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Per altre informazioni su altri codici di stato HTTP che possono essere restituiti in caso di errore, vedere [Codici di stato HTTP (Ricerca di Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).

Una volta terminato con un toodelete indice e si desidera, eseguire solo una richiesta HTTP DELETE. Ad esempio, ecco come si sarebbe eliminare l'indice "Hotel" hello:

    DELETE https://[service name].search.windows.net/indexes/hotels?api-version=2016-09-01
    api-key: [api-key]


## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato un indice di ricerca di Azure, sarà possibile troppo[caricare i contenuti in indice hello](search-what-is-data-import.md) in modo è possibile avviare la ricerca dei dati.
