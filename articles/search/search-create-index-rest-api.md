---
title: 'Creare un indice: API REST e Ricerca di Azure | Microsoft Docs'
description: Creare un indice nel codice tramite l'API REST HTTP di Ricerca di Azure.
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
ms.openlocfilehash: 9a64d1436471e406b7d9b700257d3dd96b5edcde
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-search-index-using-the-rest-api"></a>Creare un indice di Ricerca di Azure con l'API REST
> [!div class="op_single_selector"]
>
> * [Panoramica](search-what-is-an-index.md)
> * [Portale](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
>
>

Questo articolo illustra il processo di creazione di un [indice](https://docs.microsoft.com/rest/api/searchservice/Create-Index) di Ricerca di Azure mediante l'API REST di Ricerca di Azure.

Prima di seguire le indicazioni di questa guida e creare un indice, è necessario [creare un servizio Ricerca di Azure](search-create-service-portal.md).

Per creare un indice di Ricerca di Azure usando l'API REST, verrà inviata una singola richiesta HTTP POST all'endpoint dell'URL del servizio Ricerca di Azure. La definizione dell'indice verrà inclusa nel corpo della richiesta come contenuto JSON ben formato.

## <a name="identify-your-azure-search-services-admin-api-key"></a>Identificare la chiave API amministratore del servizio Ricerca di Azure
Dopo avere effettuato il provisioning di un servizio Ricerca di Azure, è possibile inviare richieste HTTP rispetto all'endpoint dell'URL del servizio usando l'API REST. *Tutte* le richieste API devono includere la chiave API generata per il servizio di ricerca di cui è stato effettuato il provisioning. La presenza di una chiave valida stabilisce una relazione di trust, in base alle singole richieste, tra l'applicazione che invia la richiesta e il servizio che la gestisce.

1. Per trovare le chiavi API del servizio, è necessario accedere al [portale di Azure](https://portal.azure.com/)
2. Passare al pannello del servizio Ricerca di Azure.
3. Fare clic sull'icona "Chiavi".

Il servizio avrà *chiavi amministratore* e *chiavi di query*.

* Le *chiavi amministratore* primarie e secondarie concedono diritti completi a tutte le operazioni, inclusa la possibilità di gestire il servizio, creare ed eliminare indici, indicizzatori e origini dati. Sono disponibili due chiavi, quindi è possibile continuare a usare la chiave secondaria se si decide di rigenerare la chiave primaria e viceversa.
* Le *chiavi di query* concedono l'accesso in sola lettura agli indici e ai documenti e vengono in genere distribuite alle applicazioni client che inviano richieste di ricerca.

Per la creazione di un indice è possibile usare la chiave primaria o secondaria.

## <a name="define-your-azure-search-index-using-well-formed-json"></a>Definire l'indice di Ricerca di Azure usando JSON ben formato
Una singola richiesta HTTP POST al servizio creerà l'indice. Il corpo della richiesta HTTP POST conterrà un singolo oggetto JSON che definisce l'indice di Ricerca di Azure.

1. La prima proprietà di questo oggetto JSON è il nome dell'indice.
2. La seconda proprietà di questo oggetto JSON è una matrice JSON denominata `fields` che contiene un oggetto JSON separato per ogni campo dell'indice. Ogni oggetto JSON contiene più coppie nome/valore per ogni attributo dei campi che include "name", "type" e così via.

È importante tenere in considerazione l'esperienza di ricerca dell'utente e le esigenze aziendali quando si progetta l'indice, perché a ogni campo devono essere assegnati gli [attributi appropriati](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Questi attributi controllano le funzionalità di ricerca (filtro, facet, ordinamento, ricerca full-text e così via) che vengono applicate ai campi. Per eventuali attributi non specificati, per impostazione predefinita verrà abilitata la funzionalità di ricerca corrispondente, a meno che non si specifichi che deve essere disabilitata.

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

Gli attributi dell'indice per ogni campo sono stati scelti con attenzione in base al modo in cui si pensa che verranno usati nell'applicazione. Ad esempio, `hotelId` è una chiave univoca che probabilmente le persone che cercano hotel non conosceranno, quindi si disabilita la ricerca full-text per quel campo impostando `searchable` su `false`, in modo da risparmiare spazio nell'indice.

Si noti che esattamente un campo di tipo `Edm.String` nell'indice deve essere il campo designato come 'key'.

La definizione di indice precedente usa un analizzatore della lingua per il campo `description_fr` perché quest'ultimo viene usato per archiviare testo in francese. Per altre informazioni sugli analizzatori di lingue, vedere l'[articolo sul supporto per le lingue](https://docs.microsoft.com/rest/api/searchservice/Language-support) e il [post di blog](https://azure.microsoft.com/blog/language-support-in-azure-search/) corrispondente.

## <a name="issue-the-http-request"></a>Inviare la richiesta HTTP
1. Usando la definizione di indice come corpo della richiesta, inviare una richiesta HTTP POST all'URL dell'endpoint di servizio Ricerca di Azure. Assicurarsi di usare nell'URL il nome del servizio come nome host e specificare il valore `api-version` appropriato come parametro della stringa di query. La versione API corrente è `2016-09-01` al momento della pubblicazione di questo documento.
2. Nelle intestazioni della richiesta specificare `Content-Type` come `application/json`. Sarà anche necessario specificare la chiave amministratore del servizio identificata nel Passaggio I nell'intestazione `api-key` .

È necessario fornire il nome servizio e la chiave API per inviare la richiesta seguente:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [api-key]


Per una richiesta riuscita, verrà visualizzato il codice di stato 201 (Creato). Per altre informazioni sulla creazione di un indice tramite l'API REST, vedere [qui le informazioni di riferimento sulle API](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Per altre informazioni su altri codici di stato HTTP che possono essere restituiti in caso di errore, vedere [Codici di stato HTTP (Ricerca di Azure)](https://docs.microsoft.com/rest/api/searchservice/HTTP-status-codes).

Dopo avere usato un indice, se si vuole eliminarlo è sufficiente inviare una richiesta HTTP DELETE. Ad esempio, per eliminare l'indice "hotels":

    DELETE https://[service name].search.windows.net/indexes/hotels?api-version=2016-09-01
    api-key: [api-key]


## <a name="next-steps"></a>Passaggi successivi
Dopo avere creato un indice di Ricerca di Azure, sarà possibile [caricare il contenuto nell'indice](search-what-is-data-import.md) , in modo che si possa iniziare a eseguire ricerche nei dati.
