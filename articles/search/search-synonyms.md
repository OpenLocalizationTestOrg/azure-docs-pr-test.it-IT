---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Documentazione preliminare per funzionalità di sinonimi (anteprima) hello, esposte in hello API REST di ricerca di Azure."
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a>Sinonimi in Ricerca di Azure (anteprima)

Sinonimi nei motori di ricerca associano equivalente termini che si espandono in modo implicito ambito hello di una query, senza utente hello con tooactually fornire termine hello. Ad esempio, il termine specificato hello "dog" e le associazioni di sinonimi di "canino" e "Cucciolo", tutti i documenti contenenti "dog", "canino" o "Cucciolo" saranno compreso ambito hello di query di hello.

In Ricerca di Azure l'espansione sinonimica viene eseguita in fase di query. È possibile aggiungere sinonimo mappe tooa servizio senza operazioni tooexisting interruzioni. È possibile aggiungere un **synonymMaps** definizione di campo di proprietà tooa senza indice hello toorebuild. Per altre informazioni, vedere [Aggiornare un indice](https://docs.microsoft.com/rest/api/searchservice/update-index) .

## <a name="feature-availability"></a>Disponibilità delle funzionalità

sinonimi Hello funzionalità è attualmente in anteprima e solo supportati in hello api-versione di anteprima più recente (api-version = 2016-09-01-Preview). Non è attualmente disponibile alcun supporto nel portale di Azure. Poiché viene specificata una versione di hello API richiesta hello, è possibile toocombine disponibile a livello generale (GA) e le API in anteprima in hello stessa app. Le API disponibili in anteprima non rientrano nel Contratto di servizio e le funzionalità disponibili in anteprima possono subire modifiche, quindi non è consigliabile usarle nelle applicazioni di produzione.

## <a name="how-toouse-synonyms-in-azure-search"></a>La modalità di ricerca di sinonimi toouse in Azure

In ricerca di Azure, supporto di sinonimi è basato sulle mappe sinonimo di definire e caricare il servizio tooyour. Queste mappe costituiscono una risorsa indipendente (ad esempio indici o origini dati) e possono essere utilizzate da qualsiasi campo ricercabile in qualsiasi indice nel servizio di ricerca.

Le mappe sinonimiche e gli indici vengono mantenuti in modo indipendente. Dopo aver definito una mappa di sinonimo e caricarlo tooyour servizio, è possibile abilitare funzionalità di sinonimo hello su un campo tramite l'aggiunta di una nuova proprietà denominata **synonymMaps** nella definizione di campo hello. Creazione, aggiornamento ed eliminazione di che una mappa di sinonimo è sempre un'operazione dell'intero documento, vale a dire che è possibile creare, aggiornare o eliminare le parti della mappa sinonimo hello in modo incrementale. Se si aggiorna anche una singola voce è necessario ripetere il caricamento.

L'aggiunta di sinonimi in un'applicazione di ricerca è una procedura in due passaggi:

1.  Aggiungere un servizio di ricerca sinonimo mappa tooyour tramite hello API riportato di seguito.  

2.  Nella definizione dell'indice hello, configurare una mappa di sinonimo hello toouse campo ricercabile.

### <a name="synonymmaps-resource-apis"></a>API di risorsa SynonymMaps

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a>Aggiungere o aggiornare una mappa sinonimica nel servizio tramite POST o PUT.

Vengono caricate sinonimo mappe servizio toohello tramite POST o PUT. Ogni regola deve essere delimitato da hello carattere di nuova riga ('\n'). È possibile definire too5, 000 regole per ogni sinonimo mappa in un servizio gratuito e 10.000 regole in tutti gli altri SKU. Ogni regola può essere composto too20 espansioni.

In questa versione di anteprima mappe sinonimo devono essere nel formato Solr Apache hello viene spiegato di seguito. Se si dispone di un dizionario di sinonimo esistente in un formato diverso e si desidera toouse direttamente, Saremmo lieti di sapere su [UserVoice](https://feedback.azure.com/forums/263029-azure-search).

È possibile creare una nuova mappa sinonimo utilizzando POST HTTP, come in hello di esempio seguente:

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

In alternativa, è possibile usare PUT e specificare nome della mappa sinonimo hello in hello URI. Se hello sinonimo mappa non esiste, verrà creato.

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a>Formato dei sinonimi Apache Solr

formato Solr Hello supporta i mapping di sinonimo equivalente ed esplicite. Specifica del filtro toohello Apri origine sinonimo di Solr Apache, descritte in questo documento di rispettare le regole di mapping: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter). Di seguito è riportata una regola di esempio per sinonimi equivalenti.
```
              USA, United States, United States of America
```

Con la regola di hello è precedente, una query di ricerca 'USA' espanderà troppo "USA" o "United States" o "Stati Uniti d'America".

Il mapping esplicito è indicato da una freccia "=>". Quando specificato, una sequenza di termine di una query di ricerca che corrisponde a hello lato sinistro di "= >" verrà sostituito con alternative hello sul lato destro hello. Dato regola hello, "Washington", "Washington" query di ricerca o "WA" verrà tutti riscritto troppo "WA". Mapping esplicito applica in direzione hello specificata e non riscrivere la query di hello "WA" troppo "Washington" in questo caso.
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a>Elencare le mappe sinonimiche del proprio servizio.

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a>Aggiungere una mappa sinonimica al proprio servizio.

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a>Eliminare una mappa sinonimica dal proprio servizio.

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a>Nella definizione dell'indice hello, configurare una mappa di sinonimo hello toouse campo ricercabile.

Una nuova proprietà di campo **synonymMaps** può essere utilizzato toospecify toouse di mappa un sinonimo per un campo ricercabile. Le mappe di sinonimo sono risorse a livello di servizio e a cui fa riferimento da qualsiasi campo di un indice nel servizio hello.

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

**synonymMaps** può essere specificato per i campi ricercabili hello tipo di 'Edm. String' o 'Collection'.

> [!NOTE]
> In questa versione di anteprima è possibile avere solo una mappa sinonimica per campo. Se si desidera toouse più mappe sinonimo, Saremmo lieti di sapere su [UserVoice](https://feedback.azure.com/forums/263029-azure-search).

## <a name="impact-of-synonyms-on-other-search-features"></a>Impatto dei sinonimi sulle altre funzionalità di ricerca

funzionalità di sinonimi Hello riscrive query originale di hello con sinonimi con hello operatore OR. Per questo motivo, hit evidenziazione e i profili di punteggio considerano termine originale hello e sinonimi come equivalenti.

Funzionalità di sinonimo applica toosearch query e non si applica toofilters o i facet. Analogamente, i suggerimenti sono basati solo sul termine originale hello; sinonimo corrispondenze non vengono visualizzati in risposta hello.

Non sono applicabili toowildcard i termini di ricerca; espansioni sinonimo prefisso, fuzzy e i termini di regex non sono espansi.

## <a name="tips-for-building-a-synonym-map"></a>Suggerimenti per la creazione di una mappa sinonimica

- Una mappa sinonimica concisa e ben progettata è più efficiente rispetto a un elenco completo delle possibili corrispondenze. Dizionari eccessivamente grandi dimensioni o complessi richiedere più tempo tooparse e influiscono sulla latenza delle query hello se query hello espande toomany sinonimi. Invece di stima in cui potrebbero essere utilizzati i termini, è possibile ottenere termini hello tramite un [report di analisi del traffico di ricerca](search-traffic-analytics.md).

- Come esercizio preliminary sia una convalida, abilitare e quindi verrà trarre vantaggio da una corrispondenza di sinonimo, questo tooprecisely report determinare quali condizioni di utilizzo e quindi continuare toouse come convalida che la mappa di sinonimo produce un risultato migliore. Nel report hello predefinito, hello riquadri "query di ricerca più comuni" e "query di ricerca Zero risultati" fornirà hello le informazioni necessarie.

- È possibile creare più mappe sinonimiche per l'applicazione di ricerca (ad esempio in base alla lingua se l'applicazione supporta clienti multilingue). Attualmente un campo può usarne una sola. È possibile aggiornare la proprietà synonymMaps di un campo in qualsiasi momento.

## <a name="next-steps"></a>Passaggi successivi

- Se si dispone di un indice esistente in un ambiente di sviluppo (non di produzione), provare a utilizzare toosee un dizionario di piccole dimensioni come aggiunta hello di sinonimi cambia hello un'esperienza di ricerca, compreso l'impatto sui profili di punteggio, hit evidenziazione e suggerimenti.

- [Abilita ricerca traffico analitica](search-traffic-analytics.md) e utilizzare hello predefinite di report di Power BI toolearn le parole usate hello la maggior parte e quali quelli restituito zero documenti. Grazie a queste informazioni, rivedere i sinonimi tooinclude dizionario hello per le query produttivo che devono essere risoluzione toodocuments nell'indice.
