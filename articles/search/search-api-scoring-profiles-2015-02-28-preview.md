---
title: profili aaaScoring (ricerca REST API versione 2015-02-28-Anteprima di Azure) | Documenti Microsoft
description: "Ricerca di Azure è un servizio di ricerca ospitato sul cloud  che supporta l'ottimizzazione dei risultati in base ai profili di punteggio definiti dall'utente."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: bfd62649-13d7-40b3-a8fa-85521a15084d
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.author: heidist
ms.date: 10/27/2016
ms.openlocfilehash: 17f83fdf6818dc6ffcc3e04f5d0185c6f646b63d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scoring-profiles-azure-search-rest-api-version-2015-02-28-preview"></a>Profili di punteggio (API REST di Ricerca di Azure versione 2015-02-28-Preview)
> [!NOTE]
> Questo articolo descrive i profili di punteggio hello [2015-02-28-Preview](search-api-2015-02-28-preview.md). Attualmente non vi è alcuna differenza tra hello `2016-09-01` versione documentati nella [MSDN](http://msdn.microsoft.com/library/azure/mt183328.aspx) e hello `2015-02-28-Preview` versione descritti qui, ma in questo documento è offrire comunque nel code coverage di documento di ordine tooprovide in hello intera API.
>
>

## <a name="overview"></a>Panoramica
Punteggio fa riferimento toohello calcolo del punteggio di ricerca per ogni elemento restituito nei risultati della ricerca. Punteggio di Hello è un indicatore di pertinenza di un elemento nel contesto di hello dell'operazione di ricerca corrente hello. Hello hello punteggio, più rilevante hello hello elemento. Nei risultati della ricerca, gli elementi vengono classificati da elevata toolow, basato sul punteggio di ricerca hello calcolati per ogni elemento.

Ricerca di Azure Usa punteggio toocompute un punteggio iniziale predefinito, ma è possibile personalizzare il calcolo di hello tramite un profilo di punteggio. I profili di punteggio offrono maggiore controllo sulla classificazione hello di elementi nei risultati della ricerca. Ad esempio, si potrebbe tooboost elementi in base alle loro potenziale di ricavi, alzare di livello elementi più recenti o evidenziare elementi che sono stati in inventario troppo lungo.

Un profilo di punteggio fa parte della definizione di indice hello, composto da campi, funzioni e parametri.

toogive è un'idea di cosa un profilo di punteggio sembra, hello esempio seguente viene illustrato un semplice profilo denominato 'geo'. Questo incrementa gli elementi con il termine di ricerca hello in hello `hotelName` campo. Utilizza inoltre hello `distance` funzione toofavor elementi che si trovano entro dieci chilometri della posizione corrente di hello. Se un utente cerca hello termine 'inn' e 'inn' risulta toobe parte del nome di hotel hello, documenti che includono gli hotel con 'inn' verranno visualizzato nei risultati della ricerca hello superiori.

    "scoringProfiles": [
      {
        "name": "geo",
        "text": {
          "weights": { "hotelName": 5 }
        },
        "functions": [
          {
            "type": "distance",
            "boost": 5,
            "fieldName": "location",
            "interpolation": "logarithmic",
            "distance": {
              "referencePointParameter": "currentLocation",
              "boostingDistance": 10
            }
          }
        ]
      }
    ]

toouse che il profilo di punteggio, la query viene formulata profilo hello toospecify nella stringa di query hello. Nella query hello seguente, si noti il parametro di query hello, `scoringProfile=geo` nella richiesta di hello.

    GET /indexes/hotels/docs?search=inn&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&api-version=2015-02-28-Preview

Questa query cerca hello termine 'inn' e passa la posizione corrente di hello. Si noti che questa query include altri parametri, ad esempio `scoringParameter`. I parametri della query sono illustrati in [Cercare documenti (API di Ricerca di Azure)](search-api-2015-02-28-preview.md#SearchDocs).

Fare clic su [esempio](#example) tooreview un esempio più dettagliato di un profilo di punteggio.

## <a name="what-is-default-scoring"></a>Informazioni sull'assegnazione predefinita di punteggio
L'assegnazione di punteggio calcola un punteggio di ricerca per ogni elemento in un set di risultati ordinato in base a una classificazione. Ogni elemento in un set di risultati di ricerca viene assegnato un punteggio di ricerca, quindi classificata toolowest più alto. Applicazione toohello vengono restituiti gli elementi con punteggi maggiori hello. Per impostazione predefinita, hello primi 50 vengono restituiti, ma è possibile utilizzare hello `$top` parametro tooreturn un numero minore o maggiore di voci (backup too1000 in un'unica risposta).

Per impostazione predefinita, un punteggio di ricerca viene calcolato in base alle proprietà statistiche dei dati hello e query hello. Ricerca di Azure trova documenti che includono i termini di ricerca hello nella stringa di query hello (alcuni o tutti, a seconda `searchMode`), preferendo i documenti che includono più istanze del termine di ricerca hello. Hello punteggio di ricerca aumenta ancora maggiore se hello termine risulta raro nell'insieme di dati hello, ma comune all'interno di documenti hello. base Hello la pertinenza di toocomputing questo approccio è noto come TF-IDF o (frequenza di termini documento frequenza inverso).

Presupponendo che non vi sia alcun ordinamento personalizzato, risultati vengono quindi classificati dal punteggio di ricerca prima che vengano restituite toohello di applicazione chiamante. Se `$top` viene omesso, 50 elementi con punteggio viene restituito la ricerca più alta hello.

I valori dei punteggi di ricerca possono essere ripetuti in un set di risultati. Ad esempio, possono essere presenti 10 elementi con punteggio pari a 1,2, 20 elementi con punteggio pari a 1,0 e 20 elementi con punteggio pari a 0,5. Quando più riscontri hanno hello stesso punteggio di ricerca, hello ordinamento degli stessi elementi con punteggio non è definito e non è stabile. Eseguire nuovamente la query hello ed è possibile rilevare gli elementi di cambio di posizione. Se due elementi hanno punteggio identico, non vi è alcuna garanzia su quale elemento verrà visualizzato per primo.

## <a name="when-toouse-custom-scoring"></a>Quando toouse assegnazione personalizzata di punteggio
È consigliabile creare uno o più profili di punteggio quando comportamento di classificazione predefinito hello non passare sufficientemente grande in soddisfare gli obiettivi aziendali. È ad esempio possibile che si voglia assegnare una rilevanza di ricerca maggiore agli elementi aggiunti di recente. Analogamente, è possibile che sia presente un campo che include i margini di profitto o un altro campo che indica il potenziale di ricavi. L'aumento della priorità riscontri utili tooyour business può essere un fattore importante nella decisione toouse i profili di punteggio.

che permettono anche di implementare l'ordinamento basato sulla rilevanza. Prendere in considerazione i risultati della ricerca pagine usate in hello precedente che consentono di ordinare in base a prezzo, data, classificazione o rilevanza. In ricerca di Azure, i profili di punteggio unità opzione 'pertinenza' hello. definizione di Hello della rilevanza è controllata dall'utente, base agli obiettivi aziendali e il tipo di hello di un'esperienza di ricerca desiderato toodeliver.

<a name="example"></a>

## <a name="example"></a>Esempio
Come indicato in precedenza, l'assegnazione personalizzata di punteggio viene implementata tramite profili di punteggio definiti in uno schema di indice.

In questo esempio mostra hello dello schema di un indice con due profili di punteggio (`boostGenre`, `newAndHighlyRated`). Qualsiasi query eseguita in questo indice che include dei profili come un parametro di query utilizzeranno i set di risultati di hello profilo tooscore hello.

    {
      "name": "musicstoreindex",
      "fields": [
        { "name": "key", "type": "Edm.String", "key": true },
        { "name": "albumTitle", "type": "Edm.String" },
        { "name": "albumUrl", "type": "Edm.String", "filterable": false },
        { "name": "genre", "type": "Edm.String" },
        { "name": "genreDescription", "type": "Edm.String", "filterable": false },
        { "name": "artistName", "type": "Edm.String" },
        { "name": "orderableOnline", "type": "Edm.Boolean" },
        { "name": "rating", "type": "Edm.Int32" },
        { "name": "tags", "type": "Collection(Edm.String)" },
        { "name": "price", "type": "Edm.Double", "filterable": false },
        { "name": "margin", "type": "Edm.Int32", "retrievable": false },
        { "name": "inventory", "type": "Edm.Int32" },
        { "name": "lastUpdated", "type": "Edm.DateTimeOffset" }
      ],
      "scoringProfiles": [
        {
          "name": "boostGenre",
          "text": {
            "weights": {
              "albumTitle": 1.5,
              "genre": 5,
              "artistName": 2
            }
          }
        },
        {
          "name": "newAndHighlyRated",
          "functions": [
            {
              "type": "freshness",
              "fieldName": "lastUpdated",
              "boost": 10,
              "interpolation": "quadratic",
              "freshness": {
                "boostingDuration": "P365D"
              }
            },
            {
              "type": "magnitude",
              "fieldName": "rating",
              "boost": 10,
              "interpolation": "linear",
              "magnitude": {
                "boostingRangeStart": 1,
                "boostingRangeEnd": 5,
                "constantBoostBeyondRange": false
              }
            }
          ]
        }
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["albumTitle", "artistName"]
        }
      ]
    }


## <a name="workflow"></a>Flusso di lavoro
tooimplement personalizzata di punteggio comportamento, aggiungere uno schema toohello profilo punteggio definisce l'indice di hello. È possibile avere fino a profili di punteggio too16 all'interno di un indice (vedere [limiti dei servizi](search-limits-quotas-capacity.md)), ma è possibile specificare solo un profilo in fase di una determinata query.

Iniziare con hello [modello](#bkmk_template) fornite in questo argomento.

Specificare un nome. I profili di punteggio sono facoltativi, ma se si aggiunge uno, il nome di hello è obbligatorio. Essere toofollow che le convenzioni di denominazione hello per i campi (inizia con una lettera, evita caratteri speciali e parole riservate). Per altre informazioni, vedere [Regole di denominazione](http://msdn.microsoft.com/library/azure/dn857353.aspx) .

il corpo di Hello del profilo di punteggio hello viene costruito da campi ponderati e funzioni.

### <a name="weights"></a>Weights
Hello `weights` proprietà di un profilo di punteggio specifica le coppie nome-valore che assegnano un campo tooa peso relativo. In hello [esempio](#example), i campi albumTitle, genre e artistName hello sono con Boosting 1.5, 5 e 2, rispettivamente. Genre viene molto più alta rispetto ad altri utenti hello? Se la ricerca su dati abbastanza omogenei (come accade hello di 'genre' in hello `musicstoreindex`), potrebbe essere necessario una varianza maggiore nei pesi relativi hello. Ad esempio, in hello `musicstoreindex`, 'rock' viene visualizzato sia come genere e nelle descrizioni di genere che in modo identico. Se si desidera una descrizione di genere toooutweigh genre, campo genre hello sarà necessario un peso relativo decisamente maggiore.

### <a name="functions"></a>Funzioni
Le funzioni vengono usate quando sono necessari calcoli aggiuntivi per contesti specifici. I tipi di funzione validi sono `freshness`, `magnitude`, `distance` e `tag`. Ogni funzione dispone di parametri che sono tooit univoco.

* `freshness`deve essere utilizzato quando si desidera è tooboost come nuovo o quello precedente elemento. Questa funzione può essere usata solo con campi datetime (`Edm.DataTimeOffset`). Hello nota `boostingDuration` attributo viene utilizzato solo con funzione di aggiornamento hello.
* `magnitude`deve essere utilizzato quando si desidera tooboost in base a come alto o basso un valore numerico è. Gli scenari che richiedono questa funzione includono l'aumento della priorità in base a margine di profitto, prezzo massimo, prezzo minimo o conteggio di download. È possibile invertire l'intervallo di hello toolow elevata, se si desidera che il modello inverso hello (ad esempio, tooboost con un prezzo inferiore elementi più alta elementi). Specificato un intervallo di prezzi da $100 troppo$ 1, è necessario impostare `boostingRangeStart` 100 e `boostingRangeEnd` gli elementi con un prezzo inferiore di hello 1 tooboost. Questa funzione può essere usata solo con i campi di tipo Integer e Double.
* `distance`deve essere utilizzato quando si desidera tooboost prossimità o area geografica. Questa funzione può essere usata solo con campi `Edm.GeographyPoint` .
* `tag`deve essere utilizzato quando si desidera tooboost tag in comune tra documenti e query di ricerca. Questa funzione può essere usata solo con campi `Edm.String` e `Collection(Edm.String)`.

#### <a name="rules-for-using-functions"></a>Regole per l'uso delle funzioni
* Il tipo di funzione (freshness, magnitude, distance, tag) deve essere scritto in lettere minuscole.
* Le funzioni non possono includere valori Null o vuoti. In particolare, se si include il nome campo, è necessario tooset è toosomething.
* Le funzioni possono essere solo campi toofilterable applicato. Per altre informazioni sui campi filtrabili, vedere [Creare un indice](search-api-2015-02-28-preview.md#CreateIndex).
* Funzioni possono essere applicati toofields definiti nella raccolta di campi hello di un indice.

Dopo aver definito l'indice di hello, compilare l'indice hello caricando schema dell'indice hello, seguito dai documenti. Per istruzioni relative a queste operazioni, vedere [Creare un indice](search-api-2015-02-28-preview.md#CreateIndex) e [Aggiungere o aggiornare documenti](search-api-2015-02-28-preview.md#AddOrUpdateDocuments). Una volta creato l'indice di hello, è necessario un profilo di punteggio funzionale utilizzabile con i dati di ricerca.

<a name="bkmk_template"></a>

## <a name="template"></a>Modello
Questa sezione illustra la sintassi di hello e modello per i profili di punteggio. Fare riferimento troppo[l'indice di riferimento all'attributo](#bkmk_indexref) nella sezione successiva di hello per le descrizioni degli attributi hello.

    ...
    "scoringProfiles": [
      {
        "name": "name of scoring profile",
        "text": (optional, only applies toosearchable fields) {
          "weights": {
            "searchable_field_name": relative_weight_value (positive #'s),
            ...
          }
        },
        "functions": (optional) [
          {
            "type": "magnitude | freshness | distance | tag",
            "boost": # (positive number used as multiplier for raw score != 1),
            "fieldName": "...",
            "interpolation": "constant | linear (default) | quadratic | logarithmic",

            "magnitude": {
              "boostingRangeStart": #,
              "boostingRangeEnd": #,
              "constantBoostBeyondRange": true | false (default)
            }

            // (- or -)

            "freshness": {
              "boostingDuration": "..." (value representing timespan over which boosting occurs)
            }

            // (- or -)

            "distance": {
              "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location)
              "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
            }

            // (- or -)

            "tag": {
              "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field)
            }
          }
        ],
        "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
      }
    ],
    "defaultScoringProfile": (optional) "...",
    ...

<a name="bkmk_indexref"></a>

## <a name="scoring-profile-property-reference"></a>Riferimento alle proprietà dei profili di punteggio
> [!NOTE]
> Una funzione di assegnazione dei punteggi può essere applicati toofields filtrabili.
>
>

| Proprietà | Descrizione |
| --- | --- |
| `name` |Obbligatorio. Questo è il nome di hello del profilo di punteggio hello. Viene indicato di seguito hello stesse convenzioni di denominazione di un campo. Deve iniziare con una lettera, non può contenere punti, due punti o simboli @ e non può iniziare con la frase hello "azureSearch" (maiuscole/minuscole). |
| `text` |Contiene proprietà Weights hello. |
| `weights` |Facoltativo. Coppia nome-valore che specifica un nome campo e il peso relativo. Il peso relativo deve essere un numero intero o a virgola mobile positivo. È possibile specificare il nome di campo hello senza un peso corrispondente. I pesi sono utilizzati tooindicate hello importanza di un campo relativo tooanother. |
| `functions` |Facoltativo. Si noti che una funzione di punteggio può essere solo toofields applicato filtrabili. |
| `type` |Obbligatorio per le funzioni di assegnazione di punteggio. Indica il tipo di hello di funzione toouse. I valori validi includono `magnitude`, `freshness`, `distance` e `tag`. È possibile includere più funzioni in ogni profilo di punteggio. nome della funzione Hello deve essere in minuscolo. |
| `boost` |Obbligatorio per le funzioni di assegnazione di punteggio. Numero positivo usato come moltiplicatore per un punteggio non elaborato. Non può essere uguale too1. |
| `fieldName` |Obbligatorio per le funzioni di assegnazione di punteggio. Una funzione di assegnazione dei punteggi può essere applicati toofields che fanno parte della raccolta di campi hello dell'indice hello e che sono filtrabili. Ogni tipo di funzione introduce inoltre restrizioni aggiuntive (il valore freshness viene usato con campi datetime, il valore magnitude con campi di tipo Integer o Double, il valore distance con campi location e il valore tag con campi string o string collection). È possibile specificare solo un campo per ogni definizione di funzione. Per esempio, toouse magnitude due volte in hello stesso profilo, sarà necessario tooinclude due definizioni di magnitude, uno per ogni campo. |
| `interpolation` |Obbligatorio per le funzioni di assegnazione di punteggio. Definisce l'inclinazione hello per cui hello Aumenta priorità del punteggio dall'inizio di hello di hello intervallo toohello fine hello intervallo. I valori validi includono `linear` (impostazione predefinita), `constant`, `quadratic` e `logarithmic`. Per informazioni dettagliate, vedere [Impostare le interpolazioni](#bkmk_interpolation) . |
| `magnitude` |grandezza Hello funzione di classificazione è utilizzato tooalter classificazioni in base hello intervallo di valori per un campo numerico. Alcuni degli esempi di utilizzo di questo genere hello sono:<ul><li>Classificazioni a stelle: Alter hello punteggio in base al valore di hello nel campo "Star Rating" hello. Quando due elementi sono rilevanti, elemento hello con classificazione superiore hello verrà visualizzato per primo.</li><li>Margine: Quando due documenti sono rilevanti, un rivenditore può essere utile documenti tooboost con margini più elevati prima.</li><li>Fare clic su conteggi: per fare clic su applicazioni che tengono traccia delle pagine o tooproducts azioni, è possibile utilizzare gli elementi tooboost grandezza che tendono a hello tooget maggior parte del traffico.</li><li>Conteggio di download: per le applicazioni che tengono traccia dei download, hello funzione magnitude permette di aumentare la priorità gli elementi che hanno la maggior parte dei download di hello.</li></ul> |
| `magnitude:boostingRangeStart` |Hello Imposta valore iniziale dell'intervallo di hello in cui viene calcolato il punteggio di grandezza. il valore di Hello deve essere un numero intero o un numero a virgola mobile. Per le classificazioni a stelle da 1 a 4, corrisponde a 1. Per i margini superiori al 50%, corrisponde a 50. |
| `magnitude:boostingRangeEnd` |Imposta il valore finale hello dell'intervallo di hello in cui viene calcolato il punteggio di grandezza. il valore di Hello deve essere un numero intero o un numero a virgola mobile. Per le classificazioni a stelle da 1 a 4, corrisponde a 4. |
| `magnitude:constantBoostBeyondRange` |I valori validi sono true o false (predefinito). Se impostato, tootrue aumento priorità completo hello continuerà toodocuments tooapply che hanno un valore di campo di destinazione hello è superiore al limite superiore dell'intervallo di hello hello. Se false, boost hello di questa funzione non saranno applicate toodocuments con un valore per il campo di destinazione hello esterna all'intervallo di hello. |
| `freshness` |validità minima Hello funzione di classificazione è utilizzato tooalter classificazione punteggi per gli elementi in base ai valori nei campi DateTimeOffset. Ad esempio, un elemento con una data più recente può essere classificato con una priorità maggiore rispetto agli elementi meno recenti. (Si noti che è anche possibile toorank elementi come eventi del calendario con date future in modo che è possibile classificare superiore rispetto a elementi ulteriormente toohello più vicino a elementi presentano in hello future) Nella versione di servizio corrente hello, un'estremità dell'intervallo di hello verrà risolto toohello ora corrente. estremità Hello è un'ora in hello precedente in base a hello `boostingDuration`. un intervallo di tempo in futuro hello tooboost utilizzare un valore negativo `boostingDuration`. frequenza di Hello in cui hello boosting modifiche da un intervallo minimo e massimo è determinato dal hello interpolazione applicata toohello profilo di punteggio (vedere Figura hello seguente). tooreverse hello fattore di aumento priorità applicato, scegliere un fattore di aumento di priorità minore di 1. |
| `freshness:boostingDuration` |Imposta un periodo di scadenza, dopo il quale l'aumento di priorità non verrà più applicato a un determinato documento. Vedere [impostare boostingDuration](#bkmk_boostdur) nella seguente sezione per la sintassi ed esempi di hello. |
| `distance` |distanza Hello funzione di classificazione è hello tooaffect utilizzati punteggio dei documenti in base a come chiusura o distanza sono tooa relativa area geografica di riferimento. percorso di riferimento Hello viene fornito come parte della query hello in un parametro (utilizzando hello `scoringParameter` parametro di query) come un argomento lon, lat. |
| `distance:referencePointParameter` |Toobe un parametro passato query toouse come percorso di riferimento. scoringParameter è un parametro di query. Per descrizioni dei parametri di query, vedere [Eseguire ricerche nei documenti](search-api-2015-02-28-preview.md#SearchDocs) . |
| `distance:boostingDistance` |Numero che indica hello distanza in chilometri dalla posizione di riferimento hello in cui hello boosting intervallo termina. |
| `tag` |Hello funzione di punteggio viene utilizzato il tag punteggio hello tooaffect dei documenti in base a tag nei documenti e query di ricerca. Documenti con tag in comune con query di ricerca hello verranno essere incrementati. Hello tag per la query di ricerca hello è fornita come parametro di assegnazione dei punteggi in ciascuna richiesta di ricerca (tramite hello `scoringParameter` parametro di query). |
| `tag:tagsParameter` |Toobe un parametro passato nelle query toospecify tag per una particolare richiesta. `scoringParameter` è un parametro di query. Per descrizioni dei parametri di query, vedere [Eseguire ricerche nei documenti](search-api-2015-02-28-preview.md#SearchDocs) . |
| `functionAggregation` |facoltativo. Applicabile solo se vengono specificate funzioni. I valori validi includono `sum` (impostazione predefinita), `average`, `minimum`, `maximum` e `firstMatching`. Un punteggio di ricerca è un singolo valore calcolato da più variabili, con funzioni multiple. Questo attributo indica il modo in cui vengono combinati degli incrementi hello di tutte le funzioni hello in un singolo incremento di aggregazione che viene quindi applicato toohello punteggio di documento di base. Punteggio di base Hello è basato sul valore di tf-idf hello calcolato dal documento hello e query di ricerca hello. |
| `defaultScoringProfile` |Quando si esegue una richiesta di ricerca, se non viene specificato alcun profilo di punteggio, verrà usato il punteggio predefinito (solo tf-idf). Valore predefinito è il nome del profilo di punteggio può essere impostato in questo caso, causando tale profilo toouse di ricerca di Azure quando viene fornito alcun profilo specifico nella richiesta di ricerca hello. |

<a name="bkmk_interpolation"></a>

## <a name="set-interpolations"></a>Impostare le interpolazioni
Le interpolazioni permettono inclinazione hello toodefine per cui hello Aumenta priorità del punteggio dall'inizio di hello di hello intervallo toohello fine hello intervallo. è possibile utilizzare Hello le interpolazioni seguenti:

* `Linear`: Per gli elementi all'interno di hello max e min intervallo, hello aumento di priorità applicato toohello elemento verrà eseguito in un importo costantemente decrescente. Interpolazione predefinita hello per un profilo di punteggio è lineare.
* `Constant`: Per gli elementi all'interno di hello inizio e di intervallo finale, un aumento costante sarà applicato toohello classificare i risultati.
* `Quadratic`: In confronto tooa interpolazione lineare che presenta un aumento di priorità costantemente decrescente, quadratica presenterà una diminuzione iniziale a un ritmo più piccolo e quindi come si avvicina hello fine intervallo diminuzione con un intervallo molto più elevato. Questa opzione di interpolazione non è consentita nelle funzioni di assegnazione di punteggio in base a tag.
* `Logarithmic`: In confronto tooa interpolazione lineare che presenta un aumento di priorità costantemente decrescente, logaritmica diminuirà inizialmente a un ritmo più elevato e quindi come si avvicina hello fine intervallo diminuisce con un intervallo molto più piccolo. Questa opzione di interpolazione non è consentita nelle funzioni di assegnazione di punteggio in base a tag.

<a name="Figure1"></a> ![][1]

<a name="bkmk_boostdur"></a>

## <a name="set-boostingduration"></a>Impostare boostingDuration
`boostingDuration`è un attributo della funzione freshness hello. Utilizzarla tooset smetterà di un periodo di scadenza dopo il quale l'aumento della priorità per un determinato documento. Ad esempio, tooboost una linea di prodotti o una marca per un periodo promozionale di 10 giorni, specificare hello 10 giorni come "P10D" per tali documenti. O tooboost eventi futuri in hello settimana successiva specificano "-P7D".

`boostingDuration` deve essere formattato come valore XSD "dayTimeDuration" (un subset limitato di un valore di durata ISO 8601). modello Hello è: `[-]P[nD][T[nH][nM][nS]]`.

Hello nella tabella seguente fornisce alcuni esempi.

| Duration | boostingDuration |
| --- | --- |
| 1 giorno |"P1D" |
| 2 giorni e 12 ore |"P2DT12H" |
| 15 minuti |"PT15M" |
| 30 giorni, 5 ore, 10 minuti e 6334 secondi |"P30DT5H10M6.334S" |

Per altri esempi, vedere il sito Web relativo ai [tipi di dati dello schema XML (W3.org)](http://www.w3.org/TR/xmlschema11-2/).

**Vedere anche**
[API REST per il servizio Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn798935.aspx) su MSDN <br/>
[Create Index (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798941.aspx) (Creare un indice (API di Ricerca di Azure))su MSDN<br/>
[Aggiungere un indice di ricerca tooa profilo punteggio](http://msdn.microsoft.com/library/azure/dn798928.aspx) su MSDN<br/>

<!--Image references-->
[1]: ./media/search-api-scoring-profiles-2015-02-28-Preview/scoring_interpolations.png
