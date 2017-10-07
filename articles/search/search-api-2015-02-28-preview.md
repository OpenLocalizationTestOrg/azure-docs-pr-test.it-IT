---
title: Ricerca servizio REST API versione 2015-02-28-Preview aaaAzure | Documenti Microsoft
description: "L'API REST di Ricerca di Azure versione 2015-02-28-Preview include funzionalità sperimentali come gli analizzatori del linguaggio naturale e le ricerche moreLikeThis."
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a>API REST del servizio Ricerca di Azure: versione 2015-02-28-Preview
Questo articolo è la documentazione di riferimento hello per `api-version=2015-02-28-Preview`. Questa versione di anteprima estende hello in genere versione disponibile, [versione api = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), fornendo hello funzionalità sperimentali di seguito:

* `moreLikeThis`parametro di hello query [ricerca documenti](#SearchDocs) API. Trova altri documenti che sono rilevanti tooanother documento specifico.

Alcune parti aggiuntive hello `2015-02-28-Preview` API REST sono documentate separatamente. incluse le seguenti:

* [Profili di punteggio](search-api-scoring-profiles-2015-02-28-preview.md)
* [Indicizzatori](search-api-indexers-2015-02-28-preview.md)

Ricerca di Azure è disponibile in più versioni. Consultare troppo[controllo delle versioni del servizio di ricerca](http://msdn.microsoft.com/library/azure/dn864560.aspx) per informazioni dettagliate.

## <a name="apis-in-this-document"></a>API in questo documento
L'API del servizio Ricerca di Azure supporta due sintassi di URL per le operazioni dell'API, ovvero semplice e OData. Per informazioni dettagliate, vedere [Supporto per OData (Ricerca di Azure)](http://msdn.microsoft.com/library/azure/dn798932.aspx). Hello elenco seguente mostra la sintassi semplice hello.

[Creare un indice](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[Aggiornare un indice](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[Ottenere un indice](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[Elencare gli indici](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[Ottenere le statistiche di un indice](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[Analizzatore di test](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[Eliminare un indice](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[Aggiungere, aggiornare o eliminare documenti](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[Eseguire ricerche nei documenti](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[Cercare un documento](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[Contare i documenti](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[Suggerimenti](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a>Operazioni sugli indici
È possibile creare e gestire gli indici in Ricerca di Azure tramite semplici richieste HTTP (POST, GET, PUT, DELETE) su una risorsa indice specifica. toocreate un indice, è innanzitutto registrare un documento JSON che descrive hello schema di indice. schema di Hello definisce i campi di hello di indice hello, i tipi di dati e come possono essere utilizzati (ad esempio, nelle ricerche full-text, filtri, ordinamento o facet). Definisce inoltre i profili di punteggio, suggerimento e altri comportamenti di hello tooconfigure gli attributi dell'indice hello.

Hello esempio seguente viene illustrato uno schema utilizzato per la ricerca di informazioni sugli alberghi con il campo di descrizione hello definito in due lingue. Si noti come gli attributi controllino come campo hello è utilizzato. Ad esempio hello `hotelId` viene utilizzata come chiave di documento hello (`"key": true`) e viene escluso dalla ricerca full-text (`"searchable": false`).

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

Dopo aver creato l'indice di hello, caricare documenti che popolano indice hello. Per questo passaggio successivo, vedere [Aggiungere, aggiornare o eliminare documenti](#AddOrUpdateDocuments) .

Per un video di introduzione tooindexing in ricerca di Azure, vedere hello [Channel 9 Cloud Cover, episodio in ricerca di Azure](http://go.microsoft.com/fwlink/p/?LinkId=511509).

<a name="CreateIndex"></a>

## <a name="create-index"></a>Creare un indice
Un indice è hello mezzo principale per organizzare e cercare documenti in ricerca di Azure, simile toohow una tabella organizza i record in un database. Ogni indice sono una raccolta di documenti tutti conformi toohello schema di indice (nomi di campo, i tipi di dati e proprietà) che gli indici specificano anche costrutti aggiuntivi (suggerimento, profili di punteggio e le opzioni CORS) che definiscono altri comportamenti di ricerca.

È possibile creare un nuovo indice in Ricerca di Azure mediante una richiesta HTTP POST o PUT. il corpo di Hello della richiesta di hello è uno schema JSON che specifica le informazioni di indice e la configurazione di hello.

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

In alternativa, è possibile usare PUT e specificare il nome di indice hello in hello URI. Se non esiste alcun indice hello, verrà creato.

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

Creazione di un indice determina la struttura di hello di hello documenti archiviati e utilizzati nelle operazioni di ricerca. Il popolamento dell'indice hello è un'operazione separata. Per questo passaggio, è possibile usare un [indicizzatore](https://msdn.microsoft.com/library/azure/mt183328.aspx) (disponibile per le origini dati supportate) o un'[operazione di aggiunta, aggiornamento o eliminazione di documenti](https://msdn.microsoft.com/library/azure/dn798930.aspx). indice invertito Hello viene generato quando i documenti hello vengono registrati.

**Nota**: numero massimo di hello di indici consentito varia in base al livello di prezzo. servizio gratuito Hello consente backup too3 indici. Nel servizio standard sono consentiti 50 indici per servizio di ricerca. Per dettagli, vedere [Limitazioni e vincoli](http://msdn.microsoft.com/library/azure/dn798934.aspx) .

**Richiesta**

Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS. Hello **Create Index** richiesta può essere costruita utilizzando un metodo POST o PUT. Quando si usa POST, è necessario fornire un nome di indice nel corpo di richiesta hello insieme definizione dello schema di indice hello. Con PUT, il nome dell'indice hello fa parte dell'URL hello. Se l'indice di hello non esiste, viene creato. Se esiste già, è aggiornato toohello nuova definizione.

Nome indice Hello deve essere minuscola, iniziare con una lettera o un numero, avere senza barre o punti e minore di 128 caratteri. Dopo avere avviato il nome dell'indice hello con una lettera o un numero, il resto di hello del nome hello può includere qualsiasi lettera, numero e trattino, purché hello trattini non siano consecutivi.

Hello `api-version` è obbligatorio. Per un elenco delle versioni disponibili, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**Intestazioni della richiesta**

Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.

* `Content-Type`: elemento obbligatorio. Impostare questa proprietà troppo`application/json`
* `api-key`: elemento obbligatorio. Hello `api-key` viene utilizzato per
* eseguire l'autenticazione del servizio di ricerca di hello richiesta tooyour. È un valore stringa, il servizio tooyour univoco. Hello **Create Index** richiesta deve includere un `api-key` tooyour chiave di amministrazione (come chiave di query anziché tooa) impostare l'intestazione.

È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello. È possibile ottenere nome servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello. Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.

<a name="RequestData"></a>
**Sintassi del corpo della richiesta**

Hello corpo della richiesta di hello contiene una definizione di schema, che include l'elenco di hello dei campi di dati all'interno di documenti che verranno inseriti nell'indice, gli attributi, tipi di dati, nonché un elenco facoltativo di profili di punteggio è utilizzati tooscore documenti in corrispondenza ora di query.

Si noti che per una richiesta POST, è necessario specificare il nome dell'indice hello nel corpo della richiesta hello.

Può esistere solo un campo chiave nell'indice hello. Toobe presenta un campo stringa. Questo campo rappresenta l'identificatore univoco di hello per ogni documento archiviato all'interno dell'indice hello.

le parti principali di un indice Hello includono hello informazioni seguenti:

* `name`
* `fields` : elementi che verranno inseriti nell'indice, tra cui il nome, il tipo di dati e le proprietà che definiscono le azioni consentite.
* `suggesters` : elementi usati per le query con completamento automatico.
* `scoringProfiles` :elementi usati per la classificazione personalizzata dei punteggi di ricerca. Per informazioni dettagliate, vedere [Aggiungere profili di punteggio a un indice di ricerca](https://msdn.microsoft.com/library/azure/dn798928.aspx) .
* `analyzers`, `charFilters`, `tokenizers`, `tokenFilters` utilizzato toodefine come documenti/query sono suddivisi in token indicizzabile o disponibile per la ricerca. Per i dettagli, vedere la pagina relativa all' [analisi in Ricerca di Azure](https://aka.ms//azsanalysis) .
* `defaultScoringProfile`Utilizzare i comportamenti di punteggio predefinito di toooverwrite hello.
* `corsOptions`tooallow le query sull'indice.

sintassi di Hello per la struttura di payload della richiesta hello è come indicato di seguito. Più avanti in questo argomento è riportata una richiesta di esempio.

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
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
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

**Attributi dell'indice**

Hello attributi seguenti possono essere impostati durante la creazione di un indice. Per informazioni dettagliate sull'assegnazione dei punteggi e sui profili di punteggio, vedere [Aggiungere profili di punteggio a un indice di ricerca](https://msdn.microsoft.com/library/azure/dn798928.aspx).

`name`-Set hello nome del campo hello.

`type`-Set hello il tipo di dati per il campo hello.

`searchable`-Hello campo viene contrassegnato come full-text in grado di ricerca. Ciò significa che verrà sottoposto ad analisi, ad esempio la suddivisione in parole durante l'indicizzazione. Se si imposta un `searchable` tooa valore del campo come "sunny day", internamente verrà suddiviso in singoli token hello "sunny" e "giorno". È così possibile eseguire ricerche full-text di questi termini. I campi di tipo `Edm.String` o `Collection(Edm.String)` sono `searchable` per impostazione predefinita. I campi di altri tipi non possono essere `searchable`.

* **Nota**: `searchable` campi utilizzano spazio aggiuntivo nell'indice poiché ricerca di Azure memorizzerà una versione in formato token aggiuntiva di valore del campo hello per le ricerche full-text. Se si desidera che lo spazio toosave l'indice e non devono essere toobe un campo inclusi nella ricerca, impostare `searchable` troppo`false`.

`filterable`-Consente di hello toobe di campo a cui fa riferimento `$filter` query. `filterable` è diverso da `searchable` nella modalità di gestione delle stringhe. I campi di tipo `Edm.String` o `Collection(Edm.String)` che sono `filterable` non sono sottoposti a suddivisione delle parole e quindi i confronti riguardano solo le corrispondenze esatte. Ad esempio, se si imposta tale campo `f` troppo "sunny day" `$filter=f eq 'sunny'` troverà alcuna corrispondenza, ma `$filter=f eq 'sunny day'` verrà. Tutti i campi sono `filterable` per impostazione predefinita.

`sortable`-Per impostazione predefinita sistema hello Ordina risultati in base al punteggio, ma in molti casi gli utenti verranno toosort dai campi nei documenti di hello. I campi di tipo `Collection(Edm.String)` non possono essere `sortable`. Tutti gli altri campi sono `sortable` per impostazione predefinita.

`facetable`: usato generalmente in una presentazione dei risultati di ricerca che include il numero di risultati per categoria (ad esempio, per cercare fotocamere digitali e visualizzare i risultati in base alla marca, ai megapixel, al prezzo e così via). Questa opzione non può essere usata con i campi di tipo `Edm.GeographyPoint`. Tutti gli altri campi sono `facetable` per impostazione predefinita.

* **Nota**: i campi di tipo `Edm.String` che sono `filterable`, `sortable` o `facetable` possono avere al massimo una lunghezza di 32 KB. In questo modo tali campi sono considerati un unico termine di ricerca e lunghezza massima di hello di un termine in ricerca di Azure è 32KB. Se è necessario toostore più testo in un campo stringa singola, sarà necessario tooexplicitly impostare `filterable`, `sortable`, e `facetable` troppo`false` nella definizione dell'indice.
* **Nota**: se un campo include nessuno dei precedente hello gli attributi impostati troppo`true` (`searchable`, `filterable`, `sortable`, o`facetable`) campo hello viene effettivamente isolato dall'indice invertito hello. Questa opzione è utile per i campi che non vengono usati nelle query, ma che sono necessari nei risultati della ricerca. Esclusione di tali campi dall'indice hello migliora le prestazioni.

`key`-Contrassegni hello campo come contenente identificatori univoci per i documenti all'interno dell'indice hello. Un solo campo deve essere scelto come hello `key` campo e deve essere di tipo `Edm.String`. I campi chiavi possono essere utilizzati toolook i documenti direttamente tramite hello [API di ricerca](#LookupAPI).

`retrievable`-Imposta se il campo hello può essere restituito nei risultati di ricerca.  Ciò è utile quando si vuole toouse un campo (ad esempio margine) come un filtro, ordinamento o punteggio meccanismo, ma non si desidera l'utente finale di hello campo toobe toohello visibile. L'attributo deve essere `true` for `key` .

`analyzer`-Set hello Nome hello analyzer toouse per il campo hello in fase di indicizzazione e ricerca. Per set di valori consentito hello vedere [analizzatori](https://msdn.microsoft.com/library/mt605304.aspx). Questa opzione può essere usata solo con campi `searchable` e non può essere impostata con `searchAnalyzer` o `indexAnalyzer`.  Una volta hello scelto, non può essere modificato per il campo hello.

`searchAnalyzer`-Set hello nome dell'analizzatore di hello utilizzato in fase di ricerca per il campo hello. Per set di valori consentito hello vedere [analizzatori](https://msdn.microsoft.com/library/mt605304.aspx). Questa opzione può essere usata solo con i campi `searchable` . Deve essere impostato insieme a `indexAnalyzer` e non può essere impostato insieme a hello `analyzer` opzione. Questo analizzatore può essere aggiornato per un campo esistente.

`indexAnalyzer`-Set hello nome dell'analizzatore di hello utilizzato in fase di indicizzazione per il campo hello. Per set di valori consentito hello vedere [analizzatori](https://msdn.microsoft.com/library/mt605304.aspx). Questa opzione può essere usata solo con i campi `searchable` . Deve essere impostato insieme a `searchAnalyzer` e non può essere impostato insieme a hello `analyzer` opzione. Una volta hello scelto, non può essere modificato per il campo hello.

`suggesters`-Set hello in modalità di ricerca e campi che sono hello origine di contenuto hello per i suggerimenti. Per informazioni dettagliate, vedere [Componenti per il suggerimento](#Suggesters) .

`scoringProfiles` : definisce i comportamenti di punteggio personalizzati che consentono di determinare quali elementi verranno visualizzati più in alto nei risultati della ricerca. I profili di punteggio sono costituiti da funzioni e campi ponderati. Vedere [aggiungere i profili di punteggio](https://msdn.microsoft.com/library/azure/dn798928.aspx) per ulteriori informazioni sugli attributi hello utilizzato in un profilo di punteggio.

<!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Supporto per le lingue**

I campi disponibili per la ricerca vengono sottoposti a un processo di analisi, che spesso comporta la suddivisione in parole, la normalizzazione del testo e l'esclusione di termini tramite filtro. Per impostazione predefinita, i campi ricercabili in ricerca di Azure vengono analizzati con hello [analizzatore Apache Lucene Standard](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) che suddivide il testo in elementi di["Segmentazione di testo Unicode"](http://unicode.org/reports/tr29/) regole. Inoltre, analizzatore standard hello converte tutti i form di lettere minuscole tootheir caratteri. I documenti indicizzati e i termini di ricerca passano tramite l'analisi di hello durante l'indicizzazione e l'elaborazione delle query.

Ricerca di Azure supporta una varietà di linguaggi. Ogni lingua richiede un analizzatore di testo non standard che tenga conto delle caratteristiche specifiche della lingua. Ricerca di Azure offre due tipi di analizzatori:

* 35 sono basati sulla tecnologia Lucene.
* 50 sono basati sulla tecnologia proprietaria di Microsoft per l'elaborazione del linguaggio naturale usata in Office e Bing.

Alcuni sviluppatori preferiscono hello Lucene soluzione open source, semplice e più familiare. Gli analizzatori Lucene sono più veloci, ma gli analizzatori Microsoft hello dispone di funzionalità avanzate, ad esempio lemmatizzazione, decompounding (in linguaggi come il tedesco, danese, olandese, svedese, norvegese, estone, fine, ungherese, slovacco) e il riconoscimento di entità (URL di word messaggi di posta elettronica, date, numeri). Se possibile, è necessario eseguire i confronti di entrambi hello Microsoft e Lucene analizzatori toodecide cui uno è una soluzione migliore.

***Analizzatori a confronto***

analizzatore Lucene Hello per la lingua inglese estende l'analizzatore standard hello. Rimuove il genitivo sassone (la 's finale) dalle parole, applica lo stemming in base all'[algoritmo Porter Stemming](http://tartarus.org/~martin/PorterStemmer/) e rimuove le parole [non significative](http://en.wikipedia.org/wiki/Stop_words) per la lingua inglese.

In confronto, analizzatore Microsoft hello esegue lemmatizzazione anziché lo stemming. Significa che è possibile gestire le forme lessicali flesse e irregolari in modo decisamente migliore, producendo risultati di ricerca più rilevanti. Guardare il modulo 7 della [presentazione di Ricerca di Azure MVA](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) per altri dettagli.

L'indicizzazione con gli analizzatori Microsoft Media è due volte toothree inferiore equivalenti Lucene, a seconda del linguaggio hello. Le prestazioni della ricerca non devono essere influenzate in modo significativo per le query di dimensioni medie.

***Configurazione***

Per ogni campo nella definizione dell'indice hello, è possibile impostare hello `analyzer` nome analizzatore tooan della proprietà che specifica la lingua e fornitore. Hello analyzer stesso verranno applicate quando l'indicizzazione e ricerca per tale campo.
Ad esempio, è possibile avere campi separati per inglese, francese e spagnola descrizioni di hotel side-by-side in hello stesso indice. Hello utilizzare [parametro query 'searchFields'](#SearchQueryParameters) toospecify toosearch quale campo specifico della lingua base nelle query. È possibile esaminare gli esempi di query che includono hello `analyzer` proprietà [ricerca documenti](#SearchDocs). 

***Elenco di analizzatori***

Di seguito è elenco hello delle lingue supportate con i nomi di Analizzatore Lucene e Microsoft.

<table style="font-size:12">
    <tr>
        <th>Lingua</th>
        <th>Nome analizzatore Microsoft</th>
        <th>Nome analizzatore Lucene</th>
    </tr>
    <tr>
        <td>Arabo</td>
        <td>ar.microsoft</td>
        <td>ar.lucene</td>        
    </tr>
    <tr>
        <td>Armeno</td>
        <td></td>
        <td>hy.lucene</td>
      </tr>
    <tr>
        <td>Bengalese</td>
        <td>bn.microsoft</td>
        <td></td>
    </tr>
      <tr>
        <td>Basco</td>
        <td></td>
        <td>eu.lucene</td>
    </tr>
      <tr>
         <td>Bulgaro</td>
        <td>bg.microsoft</td>
        <td>bg.lucene</td>
      </tr>
      <tr>
        <td>Catalano</td>
        <td>ca.microsoft</td>
        <td>ca.lucene</td>          
      </tr>
    <tr>
        <td>Cinese semplificato</td>
        <td>zh-Hans.microsoft</td>
        <td>zh-Hans.lucene</td>        
    </tr>
    <tr>
        <td>Cinese tradizionale</td>
        <td>zh-Hant.microsoft</td>
        <td>zh-Hant.lucene</td>        
    <tr>
    <tr>
        <td>Croato</td>
        <td>hr.microsoft</td>
        <td/></td>
    </tr>
    <tr>
        <td>Ceco</td>
        <td>cs.microsoft</td>
        <td>cs.lucene</td>        
    </tr>    
    <tr>
        <td>Danese</td>
        <td>da.microsoft</td>
        <td>da.lucene</td>        
    </tr>    
    <tr>
        <td>Olandese</td>
        <td>nl.microsoft</td>
        <td>nl.lucene</td>    
    </tr>    
    <tr>
        <td>Inglese</td>        
        <td>en.microsoft</td>
        <td>en.lucene</td>        
    </tr>
    <tr>
        <td>Estone</td>
        <td>et.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Finlandese</td>
        <td>fi.microsoft</td>
        <td>fi.lucene</td>        
    </tr>    
    <tr>
        <td>Francese</td>
        <td>fr.microsoft</td>
        <td>fr.lucene</td>        
    </tr>
    <tr>
        <td>Gallego</td>
        <td></td>
        <td>gl.lucene</td>        
      </tr>
    <tr>
        <td>Tedesco</td>
        <td>de.microsoft</td>
        <td>de.lucene</td>        
    </tr>
    <tr>
        <td>Greco</td>
        <td>el.microsoft</td>
        <td>el.lucene</td>        
    </tr>
    <tr>
        <td>Gujarati</td>
        <td>gu.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Ebraico</td>
        <td>he.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Hindi</td>
        <td>hi.microsoft</td>
        <td>hi.lucene</td>        
    </tr>
    <tr>
        <td>Ungherese</td>        
        <td>hu.microsoft</td>
        <td>hu.lucene</td>
    </tr>
    <tr>
        <td>Islandese</td>
        <td>is.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Indonesiano (Bahasa)</td>
        <td>id.microsoft</td>
        <td>id.lucene</td>        
    </tr>
    <tr>
        <td>Irlandese</td>
        <td></td>
          <td>ga.lucene</td>
    </tr>
    <tr>
        <td>Italiano</td>
        <td>it.microsoft</td>
        <td>it.lucene</td>        
    </tr>
    <tr>
        <td>Giapponese</td>
        <td>ja.microsoft</td>
        <td>ja.lucene</td>

    </tr>
    <tr>
        <td>Kannada</td>
        <td>ka.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Coreano</td>
        <td>ko.Microsoft</td>
        <td>ko.lucene</td>
    </tr>
    <tr>
        <td>Lettone</td>        
        <td>lv.microsoft</td>
        <td>lv.lucene</td>    
    </tr>
    <tr>
        <td>Lituano</td>
        <td>lt.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Malayalam</td>
        <td>ml.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Malese (alfabeto latino)</td>
        <td>ms.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Marathi</td>
        <td>mr.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Norvegese</td>
        <td>nb.microsoft</td>
        <td>no.lucene</td>        
    </tr>
      <tr>
        <td>Persiano</td>
        <td></td>
        <td>fa.lucene</td>        
      </tr>
    <tr>
        <td>Polacco</td>
        <td>pl.microsoft</td>
        <td>pl.lucene</td>        
    </tr>
    <tr>
        <td>Portoghese (Brasile)</td>
        <td>pt-Br.microsoft</td>
        <td>pt-Br.lucene</td>        
    </tr>
    <tr>
        <td>Portoghese (Portogallo)</td>
        <td>pt-Pt.microsoft</td>        
        <td>pt-Pt.lucene</td>
    </tr>
    <tr>
        <td>Punjabi</td>
        <td>pa.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Romeno</td>
        <td>ro.microsoft</td>
        <td>ro.lucene</td>
    </tr>
    <tr>
        <td>Russo</td>
        <td>ru.microsoft</td>
        <td>ru.lucene</td>    
    </tr>
    <tr>
        <td>Serbo (alfabeto cirillico)</td>
        <td>sr-cyrillic.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Serbo (alfabeto latino)</td>
        <td>sr-latin.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Slovacco</td>
        <td>sk.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Sloveno</td>
        <td>sl.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Spagnolo</td>
        <td>es.microsoft</td>
        <td>es.lucene</td>
    </tr>
    <tr>
        <td>Svedese</td>
        <td>sv.microsoft</td>
        <td>sv.lucene</td>
    </tr>

    <tr>
        <td>Tamil</td>
        <td>ta.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Telugu</td>
        <td>te.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Thai</td>
        <td>th.microsoft</td>
        <td>th.lucene</td>
    </tr>
    <tr>
        <td>Turco</td>
        <td>tr.microsoft</td>
        <td>tr.lucene</td>        
    </tr>
    <tr>
        <td>Ucraino</td>
        <td>uk.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Urdu</td>
        <td>ur.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Vietnamita</td>
        <td>vi.microsoft</td>
        <td></td>
    </tr>
    <td colspan="3">Ricerca di Azure fornisce inoltre configurazioni dell'analizzatore indipendenti dalla lingua</td>
    <tr>
        <td>Riduzione ASCII standard</td>
        <td>standardasciifolding.lucene</td>
        <td>
        <ul>
            <li>Segmentazione di testo Unicode (tokenizer standard)</li>
            <li>Filtro di riduzione ASCII - converte i caratteri Unicode che non appartengono al set di toohello dei primi 127 caratteri ASCII nei rispettivi equivalenti ASCII. Questo filtro è utile per la rimozione dei segni diacritici.</li>
        </ul>
        </td>
    </tr>
</table>

Tutti gli analizzatori con nomi contenenti la parola <i>lucene</i> sono basati sugli [analizzatori di lingua Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html). Sono disponibili ulteriori informazioni sul filtro di riduzione ASCII di hello [qui](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).

**Componenti per il suggerimento**

Oggetto `suggester` definisce i campi in un indice vengono utilizzati toosupport completamento automatico nelle ricerche. In genere stringhe di ricerca parziali vengono inviate toohello [API suggerimenti](#Suggestions) hello utente digita una query di ricerca, mentre hello API restituisce un set di frasi suggerite. Un strumento suggerimenti definite nell'indice hello determina quali campi sono termini di ricerca della digitazione di hello toobuild utilizzato. Per visualizzare i dettagli sulla configurazione, consultare [Componenti per il suggerimento](#Suggesters) .

**Profili di punteggio**

Oggetto `scoringProfile` definisce i comportamenti di punteggio personalizzati che consentono di determinare quali elementi verranno visualizzati nei risultati della ricerca hello superiore. I profili di punteggio sono costituiti da funzioni e campi ponderati. toouse loro, si specifica un profilo in base al nome nella stringa di query hello.

Un profilo di punteggio predefinito agisce dietro hello scene toocompute un punteggio di ricerca per ogni elemento in un set di risultati. È possibile utilizzare hello interne e senza nome, il profilo di punteggio. In alternativa, impostare `defaultScoringProfile` toouse un profilo personalizzato come valore predefinito di hello, viene richiamato ogni qualvolta un profilo personalizzato non è specificato nella stringa di query hello.

Vedere [tooa indice di ricerca (ricerca di Azure del servizio API REST) i profili di punteggio Aggiungi](search-api-scoring-profiles-2015-02-28-preview.md) per informazioni dettagliate.

**Opzioni CORS**

Javascript sul lato client non è possibile chiamare le API per impostazione predefinita poiché browser hello impedirà tutte le richieste cross-origin. Per abilitare CORS (Cross-Origin Resource Sharing) impostando hello `corsOptions` indice tooyour query multiorigine tooallow di attributo. Si noti che, per motivi di sicurezza, solo le API di query supportano CORS. è possibile impostare per CORS Hello le opzioni seguenti:

* `allowedOrigins`(obbligatorio): si tratta di un elenco di origini che verrà concesso l'indice tooyour di accesso. Ciò significa che il codice Javascript servito da queste origini sarà consentito tooquery indice (presupponendo che venga fornita la chiave API corretta hello). Ogni origine è in genere formato hello `protocol://fully-qualified-domain-name:port` Sebbene hello porta viene spesso omessa. Per altri dettagli, vedere [questo articolo](http://go.microsoft.com/fwlink/?LinkId=330822) .
  * Se si desidera tooallow le entità Origin tooall di accesso, includere `*` come un singolo elemento hello `allowedOrigins` matrice. Tenere presente che **questa non è la procedura consigliata per i servizi di ricerca di produzione.** Può comunque essere utile per finalità di sviluppo o debug.
* `maxAgeInSeconds`(facoltativo): i browser usano questo valore toodetermine hello durata (in secondi) toocache delle risposte preliminari CORS. Questo valore deve essere un intero non negativo. Questo valore è, prestazioni migliori hello Hello più grande, ma hello più tempo che richiederà per effetto di tootake modifiche dei criteri CORS. Se questo valore non è impostato, viene usata una durata predefinita di 5 minuti.

<a name="CreateUpdateIndexExample"></a>
**Esempio di corpo della richiesta**

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

**Risposta**

Per una richiesta con esito positivo: "201 Creato".

Per impostazione predefinita il corpo della risposta hello conterrà hello JSON per la definizione dell'indice hello che è stato creato. Se hello `Prefer` intestazione della richiesta è troppo`return=minimal`, hello corpo della risposta sarà vuoto e codice di stato hello esito positivo sarà "204 Nessun contenuto" invece di "201 creato". Questo vale indipendentemente dal fatto se PUT o POST è indice di hello toocreate utilizzato.

**Osservazioni**

Attualmente è previsto un supporto limitato per gli aggiornamenti dello schema di indice. Gli aggiornamenti dello schema che richiedono la reindicizzazione, ad esempio la modifica dei tipi di campo, non sono attualmente supportati. Sebbene i campi esistenti non possono essere modificati o eliminati, è possano aggiungere nuovi campi tooan di indice esistente in qualsiasi momento. Quando viene aggiunto un nuovo campo, tutti i documenti esistenti nell'indice hello avranno automaticamente un valore null per tale campo. Nessun ulteriore spazio di archiviazione verrà utilizzato fino a quando non verranno aggiunti toohello indice nuovi documenti.

<a name="Suggesters"></a>

## <a name="suggesters"></a>Componenti per il suggerimento
funzionalità dei suggerimenti Hello in ricerca di Azure è una funzionalità di query di digitazione o di completamento automatico, che fornisce un elenco di potenziali termini di ricerca nella risposta toopartial input di stringa in una casella di ricerca. I suggerimenti di query sono quelli visualizzati quando si usano i motori di ricerca commerciali: se si digita ".NET" in Bing, viene visualizzato un elenco di termini quali ".NET 4.5", ".NET Framework 3.5" e così via. Quando si utilizza l'API REST del servizio ricerca hello, l'implementazione di suggerimenti in un'applicazione di ricerca di Azure personalizzata richiede seguente hello:

* Abilitare i suggerimenti aggiungendo un **dello strumento suggerimenti** costruzione nell'indice, offrendo digitazione nome hello, modalità di ricerca e un elenco di campi per il quale viene richiamata. Ad esempio, se si specifica "NomeCittà" come un campo di origine, digitare una stringa di ricerca parziale del "Mare" comporterà "Seattle", "Milazzo" e "Militello" (tutti e tre sono nomi di città effettive) offerto come utente toohello suggerimenti di query.
* Richiamare i suggerimenti mediante chiamata hello [API suggerimenti](#Suggestions) nel codice dell'applicazione. In genere stringhe di ricerca parziali vengono inviate toohello servizio hello utente digita una query di ricerca, mentre l'API restituisce un set di frasi suggerite.

Questo articolo viene illustrato come tooconfigure un **dello strumento suggerimenti**. È inoltre consigliabile esaminare hello [API suggerimenti](#Suggestions) per informazioni dettagliate sull'utilizzo di un strumento suggerimenti.

**Utilizzo**

`Suggesters`vengono creati nell'indice hello e adatti per documenti specifici toosuggest invece che termini o frasi. campi di Hello migliori candidate sono titoli, nomi e altre frasi relativamente brevi che consentono di identificare un elemento. I campi meno efficaci sono quelli ripetitivi, come le categorie e i tag, o quelli molto lunghi, come le descrizioni o i commenti.

Come parte della definizione di indice hello, è possibile aggiungere un singolo strumento suggerimenti toohello `suggesters` insieme. Le proprietà che definiscono un strumento suggerimenti includono hello informazioni seguenti:

* `name`: nome hello di strumento suggerimenti hello. Utilizza il nome di hello di strumento suggerimenti hello quando si chiama hello `suggest` API.
* `searchMode`: hello toosearch strategia utilizzata per ottenere frasi candidate. Hello unica modalità attualmente supportata è `analyzingInfixMatching`, che esegue una corrispondenza flessibile di frasi all'inizio di hello o all'interno delle proposizioni hello.
* `sourceFields`: Un elenco di uno o più campi che sono hello origine di contenuto hello per i suggerimenti. Solo i campi di tipo `Edm.String` e `Collection(Edm.String)` possono essere origini per i suggerimenti. È possibile usare solo campi per i quali non è impostato un analizzatore di lingua personalizzato.

**Esempio di componente di suggerimento**

Un strumento suggerimenti è parte dell'indice hello. Può esistere un solo strumento suggerimenti in hello `suggesters` insieme fields raccolta nella versione corrente di hello, insieme a hello e `scoringProfiles`.

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> Se è stata utilizzata la versione di anteprima pubblica hello di ricerca di Azure, `suggesters` sostituisce una proprietà booleana precedente (`"suggestions": false`) che supporta solo i suggerimenti di prefisso per stringhe brevi (da 3 a 25 caratteri). Il relativo sostituto, `suggesters`, supporta infisso che trovano termini corrispondenti all'inizio di hello o centro hello del contenuto del campo, con una migliore tolleranza per gli errori nelle stringhe di ricerca di corrispondenza. Si è a partire dalla versione di hello in genere disponibili, ora hello unica implementazione di suggerimenti hello API. Hello precedente `suggestions` proprietà che è stata introdotta in `api-version=2014-07-31-Preview` continua toowork in tale versione, ma non è operativa nella hello `2015-02-28` o versioni successive di ricerca di Azure.
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a>Aggiornare un indice
È possibile aggiornare un indice esistente in Ricerca di Azure usando una richiesta HTTP PUT. Gli aggiornamenti possono includere l'aggiunta di nuovi campi toohello schema esistente, la modifica delle opzioni CORS e la modifica di profili di punteggio. Per altre informazioni, vedere [Aggiungere profili di punteggio a un indice di ricerca](https://msdn.microsoft.com/library/azure/dn798928.aspx) . Specificare il nome di hello di hello indice tooupdate nell'URI richiesta hello:

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Importante:** il supporto per gli aggiornamenti dello schema di indice è toooperations limitato che non richiedono la ricompilazione di indice di ricerca hello. Gli aggiornamenti dello schema che richiedono la reindicizzazione, ad esempio la modifica dei tipi di campo, non sono attualmente supportati. È possibile aggiungere nuovi campi in qualsiasi momento, anche se i campi esistenti non possono essere modificati o eliminati. Hello vale troppo`suggesters`. Possono aggiungere nuovi campi vengono aggiunti dello strumento suggerimenti tooa in campi di hello hello ora, ma non è possibile rimuovere campi da `suggesters` e non è possibile aggiungere campi esistenti troppo`suggesters`.

Quando si aggiunge un nuovo indice tooan campo, tutti i documenti esistenti nell'indice hello avranno automaticamente un valore null per tale campo. Nessun ulteriore spazio di archiviazione verrà utilizzato fino a quando non verranno aggiunti toohello indice nuovi documenti.

**Richiesta**

Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS. Hello **indice ad aggiornamento in** richiesta viene costruita utilizzando HTTP PUT. Con PUT, il nome dell'indice hello fa parte dell'URL hello. Se l'indice di hello non esiste, viene creato. Se l'indice hello esiste già, è aggiornato toohello nuova definizione.

Nome indice Hello deve essere minuscola, iniziare con una lettera o un numero, avere senza barre o punti e minore di 128 caratteri. Dopo avere avviato il nome dell'indice hello con una lettera o un numero, il resto di hello del nome hello può includere qualsiasi lettera, numero e trattino, purché hello trattini non siano consecutivi.

`api-version=[string]` (elemento obbligatorio). versione di anteprima Hello è `api-version=2015-02-28-Preview`. Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**Intestazioni della richiesta**

Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.

* `Content-Type`: elemento obbligatorio. Impostare questa proprietà troppo`application/json`
* `api-key`: elemento obbligatorio. Hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca. È un valore stringa, il servizio tooyour univoco. Hello **indice ad aggiornamento in** richiesta deve includere un `api-key` tooyour chiave di amministrazione (come chiave di query anziché tooa) impostare l'intestazione.

È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello. È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello. Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.

**Sintassi del corpo della richiesta**

Quando si aggiorna un indice esistente, il corpo di hello deve includere definizione dello schema originale hello, nonché i nuovi campi hello che si aggiunge, nonché hello modificato i profili di punteggio, suggerimento e le opzioni CORS, se presente. Se non si modificano i profili di punteggio hello e le opzioni CORS, è necessario includere originali hello dalla creazione dell'indice hello. In genere hello migliore modello toouse per gli aggiornamenti è definizione dell'indice hello tooretrieve con un'operazione GET, modificarla, quindi aggiornarla mediante PUT.

sintassi dello schema Hello utilizzato toocreate che un indice viene riprodotto di seguito per praticità. Per altri dettagli, vedere [Creare un indice](#CreateIndex) .

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
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
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


**Risposta**

Per una richiesta con esito positivo: "204 Nessun contenuto".

Per impostazione predefinita hello corpo della risposta sarà vuoto. Tuttavia, se hello `Prefer` intestazione della richiesta è troppo`return=representation`, corpo della risposta hello conterrà hello JSON per la definizione dell'indice hello che è stata aggiornata. In questo caso, cui codice di stato di hello esito positivo sarà "200 OK".

**Aggiornamento della definizione dell'indice con analizzatori personalizzati**

Dopo che un analizzatore, un tokenizer, un filtro di token o un filtro di carattere è stato definito non può essere modificato. Nuovi possono essere aggiunto indice esistente tooan solo se hello `allowIndexDowntime` flag è impostato tootrue nella richiesta di aggiornamento di hello indice: 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

Si noti che questa operazione passerà l'indice offline per almeno alcuni secondi, causando l'indicizzazione e query richiede toofail. Disponibilità delle prestazioni e di scrittura dell'indice hello può essere compromesso per alcuni minuti dopo aver aggiornato l'indice di hello, o più per gli indici di dimensioni molto grandi.

<a name="ListIndexes"></a>

## <a name="list-indexes"></a>Elencare gli indici
Hello **indici dell'elenco** operazione restituisce un elenco di indici hello attualmente nel servizio di ricerca di Azure.

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

**Richiesta**

Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS. Hello **indici dell'elenco** richiesta può essere costruita utilizzando il metodo GET hello.

`api-version=[string]` (elemento obbligatorio). versione di anteprima Hello è `api-version=2015-02-28-Preview`. Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**Intestazioni della richiesta**

Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.

* `api-key`: elemento obbligatorio. Hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca. È un valore stringa, il servizio tooyour univoco. Hello **indici dell'elenco** richiesta deve includere un `api-key` set tooan di chiave di amministrazione (come chiave di query anziché tooa).

È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello. È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello. Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.

**Corpo della richiesta**

Nessuno.

**Risposta**

Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.

Di seguito è riportato il corpo di una risposta di esempio:

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

Si noti che è possibile filtrare la risposta hello delle proprietà hello toojust che si è interessati. Ad esempio, se si desidera solo un elenco di nomi di indice, utilizzare hello OData `$select` opzione di query:

    GET /indexes?api-version=2015-02-28-Preview&$select=name

In questo caso, la risposta hello hello sopra riportato sarebbe simile al seguente:

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

Si tratta di una larghezza di banda toosave tecnica utile se si dispone di un numero eccessivo di indici in servizio di ricerca.

<a name="GetIndex"></a>

## <a name="get-index"></a>Ottenere un indice
Hello **ottenere indice** operazione Ottiene la definizione di indice hello da ricerca di Azure.

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**Richiesta**

Per le richieste del servizio, è necessario usare il protocollo HTTPS. Hello **ottenere indice** richiesta può essere costruita utilizzando il metodo GET hello.

Hello [nome indice] nell'URI della richiesta hello specifica quali tooreturn indice dalla raccolta di indici hello.

`api-version=[string]` (elemento obbligatorio). versione di anteprima Hello è `api-version=2015-02-28-Preview`. Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**Intestazioni della richiesta**

Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.

* `api-key`: hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca. È un valore stringa, il servizio tooyour univoco. Hello **ottenere indice** richiesta deve includere un `api-key` set tooan di chiave di amministrazione (come chiave di query anziché tooa).

È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello. È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello. Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.

**Corpo della richiesta**

Nessuno.

**Risposta**

Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.

Vedere l'esempio hello JSON in [la creazione e aggiornamento di un indice](#CreateUpdateIndexExample) per un esempio di payload di risposta hello.

<a name="DeleteIndex"></a>

## <a name="delete-index"></a>Eliminare un indice
Hello **Elimina indice** operazione rimuove un indice e i documenti associati al servizio di ricerca di Azure. È possibile ottenere il nome dell'indice hello dal dashboard del servizio nel portale di Azure hello hello o da hello API. Per informazioni dettagliate, vedere [Elencare gli indici](#ListIndexes) .

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**Richiesta**

Per le richieste del servizio, è necessario usare il protocollo HTTPS. Hello **Elimina indice** richiesta può essere costruita utilizzando il metodo DELETE hello.

Hello [nome indice] nell'URI della richiesta hello specifica quali toodelete indice dalla raccolta di indici hello.

`api-version=[string]` (elemento obbligatorio). versione di anteprima Hello è `api-version=2015-02-28-Preview`. Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**Intestazioni della richiesta**

Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.

* `api-key`: elemento obbligatorio. Hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca. È un valore di stringa, univoco tooyour URL del servizio. Hello **Elimina indice** richiesta deve includere un `api-key` tooyour chiave di amministrazione (come chiave di query anziché tooa) impostare l'intestazione.

È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello. È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello. Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.

**Corpo della richiesta**

Nessuno.

**Risposta**

Se la risposta ha esito positivo, viene restituito il codice di stato 204 Nessun contenuto.

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a>Ottenere le statistiche di un indice
Hello **ottenere statistiche dell'indice** operazione restituisce da ricerca di Azure con un numero di documenti per indice corrente hello, nonché l'utilizzo di archiviazione.

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> Le statistiche sul numero di documenti e le dimensioni vengono raccolte ad intervalli di pochi minuti, non in tempo reale. Pertanto, statistiche hello restituite da questa API potrebbero non riflettere le modifiche è causato da operazioni di indicizzazione di recente.
> 
> 

**Richiesta**

Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS. Hello **ottenere statistiche dell'indice** richiesta può essere costruita utilizzando il metodo GET hello.

Hello [nome indice] nell'URI della richiesta hello indica hello servizio tooreturn indice le statistiche per hello specificato indice.

`api-version=[string]` (elemento obbligatorio). versione di anteprima Hello è `api-version=2015-02-28-Preview`. Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**Intestazioni della richiesta**

Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.

* `api-key`: hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca. È un valore stringa, il servizio tooyour univoco. Hello **ottenere statistiche dell'indice** richiesta deve includere un `api-key` set tooan di chiave di amministrazione (come chiave di query anziché tooa).

È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello. È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello. Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.

**Corpo della richiesta**

Nessuno.

**Risposta**

Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.

corpo della risposta Hello è nel seguente formato hello:

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a>Analizzatore di test
Hello **analizzare API** viene illustrato come un analizzatore suddivide il testo in token.

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Richiesta**

Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS. Hello **analizzare API** richiesta può essere costruita utilizzando il metodo POST hello.

`api-version=[string]` (elemento obbligatorio). versione di anteprima Hello è `api-version=2015-02-28-Preview`. Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**Intestazioni della richiesta**

Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.

* `api-key`: hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca. È un valore stringa, il servizio tooyour univoco. Hello **analizzare API** richiesta deve includere un `api-key` set tooan di chiave di amministrazione (come chiave di query anziché tooa).

È necessario anche il nome dell'indice hello e URL della richiesta hello tooconstruct nome servizio hello. È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello. Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.

**Corpo della richiesta**

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

oppure

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

Hello `analyzer_name`, `tokenizer_name`, `token_filter_name` e `char_filter_name` necessario toobe nomi validi di analizzatori predefiniti o personalizzati, tokenizer, filtri di token e char per indice hello. altre informazioni sul processo di hello dell'analisi lessicale vedere toolearn [Analysis in ricerca di Azure](https://aka.ms/azsanalysis).

**Risposta**

Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.

corpo della risposta Hello è nel seguente formato hello:

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

**Esempio dell'API di analisi**

**Richiesta**

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

**Risposta**

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a>Operazioni sui documenti
In ricerca di Azure, un indice viene archiviato nel cloud hello e popolato con i documenti JSON caricare toohello servizio. Tutti i documenti hello caricati costituiscono insieme hello dei dati di ricerca. I documenti includono campi, alcuni dei quali sono stati suddivisi in token corrispondenti a termini di ricerca durante il caricamento. Hello `/docs` segmento di URL in hello API di ricerca di Azure rappresenta l'insieme di hello di documenti in un indice. Tutte le operazioni eseguite nella raccolta di hello, ad esempio caricamento, unione, eliminazione o l'esecuzione di query su documenti avvengono nel contesto di hello di un singolo indice, in tal caso hello URL per queste operazioni inizieranno sempre con `/indexes/[index name]/docs` per un nome dell'indice specificato.

Il codice dell'applicazione deve generare JSON documenti tooupload tooAzure ricerca o è possibile utilizzare un [indicizzatore](https://msdn.microsoft.com/library/dn946891.aspx) tooload documenti di origine di dati di hello è il Database di SQL Azure o Azure Cosmos DB. In genere, gli indici vengono popolati da un singolo set di dati specificato dall'utente.

È consigliabile pianificare sulla disponibilità di un documento per ogni elemento che si desidera toosearch. Un'applicazione per il noleggio di film può avere un documento per ogni film, un'applicazione di tipo vetrina può avere un documento per ogni SKU, un'applicazione per corsi online può avere un documento per ogni corso oppure una società di ricerche può avere un documento per ogni articolo accademico disponibile nel proprio archivio e così via.

I documenti sono costituiti da uno o più campi. I campi possono contenere testo suddiviso da Ricerca di Azure in token corrispondenti a termini di ricerca, oltre a valori senza token o non di testo che possono essere usati nei filtri o nei profili di punteggio. Hello nomi, tipi di dati e le funzionalità di ricerca supportate per ogni campo sono determinate dallo schema di indice hello. Uno dei campi di hello in ogni schema di indice deve essere designato come un ID e ogni documento deve avere un valore per il campo ID hello che identifica in modo univoco tale documento nell'indice hello. Tutti gli altri campi di documento sono facoltativi e verranno tooa null il valore predefinito se non specificato. Si noti che i valori null non occupano spazio nell'indice di ricerca hello.

Prima di poter caricare documenti, è necessario avere già creato indice hello sul servizio hello. Per informazioni dettagliate su questo primo passaggio, vedere [Creare un indice](#CreateIndex) .

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a>aggiunta, aggiornamento o eliminazione di documenti
È possibile caricare, unire o eliminare documenti da un indice specificato usando HTTP POST. Per un numero elevato di aggiornamenti, è consigliabile l'invio in batch di documenti, documenti too1000 per ogni batch, o circa 16 MB per batch.

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Richiesta**

Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS. È possibile caricare, unire o eliminare documenti da un indice specificato usando HTTP POST.

Hello URI della richiesta include [nome indice], che specifica quali toopost indicizzare i documenti. È possibile registrare solo indice tooone documenti alla volta.

`api-version=[string]` (elemento obbligatorio). versione di anteprima Hello è `api-version=2015-02-28-Preview`. Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**Intestazioni della richiesta**

Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.

* `Content-Type`: elemento obbligatorio. Impostare questa proprietà troppo`application/json`
* `api-key`: elemento obbligatorio. Hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca. È un valore stringa, il servizio tooyour univoco. Hello **aggiungere documenti** richiesta deve includere un `api-key` tooyour chiave di amministrazione (come chiave di query anziché tooa) impostare l'intestazione.

È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello. È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello. Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.

**Corpo della richiesta**

corpo Hello della richiesta di hello contiene uno o più documenti toobe indicizzata. I documenti sono identificati da una chiave univoca. Ogni documento è associato a un'azione: upload, merge, mergeOrUpload o delete. Le richieste di caricamento deve includere i dati del documento hello come un set di coppie chiave/valore.

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> Le chiavi di documenti possono contenere solo lettere, numeri, trattini ("-"), caratteri di sottolineatura ("_") e segni di uguale ("="). Per altre informazioni, vedere la pagina relativa alle [regole di denominazione](https://msdn.microsoft.com/library/azure/dn857353.aspx).
> 
> 

**Azioni sui documenti**

* `upload`: Un'azione upload è simile tooan "upsert" in cui verrà inserito se è nuovo e aggiornato/sostituito se esiste il documento hello. Si noti che tutti i campi vengono sostituiti in caso di aggiornamento hello.
* `merge`: Merge aggiorna un'esistente il documento con hello specificati campi. Se il documento hello non esiste, l'unione di hello avrà esito negativo. Qualsiasi campo specificato in un'unione sostituirà campo esistente di hello nel documento hello. Sono inclusi anche i campi di tipo `Collection(Edm.String)`. Ad esempio, se hello documento contiene un campo "tags" con valore `["budget"]` e si esegue un'unione con valore `["economy", "pool"]` per "tags", valore finale di hello del campo hello "tags" sarà `["economy", "pool"]`. e **non** sarà `["budget", "economy", "pool"]`.
* `mergeOrUpload`: si comporta come `merge` se esiste un documento con hello data già chiave nell'indice hello. Se il documento hello non esiste, si comporta come `upload` con un nuovo documento.
* `delete`: Delete Elimina documento specificato hello indice hello. Si noti che tutti i campi specificare un `delete` operazione diversa da quella campo chiave hello verrà ignorati. Se si desidera tooremove un singolo campo da un documento, utilizzare `merge` invece e impostare semplicemente il campo hello in modo esplicito troppo`null`.

**Risposta**

Il codice di stato 200 (OK) viene restituito per una risposta con esito positivo, a indicare che tutti gli elementi sono stati indicizzati correttamente. In questo caso viene hello `status` proprietà impostata tootrue per tutti gli elementi, nonché hello `statusCode` proprietà impostata tooeither 201 (per i documenti appena caricati) o 200 (per i documenti uniti o eliminati):

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

Il codice di stato 207 (Multi-Status) viene restituito quando almeno un elemento non è stato indicizzato correttamente. Gli elementi che non sono stati indicizzati hanno hello `status` toofalse set di campi. Hello `errorMessage` e `statusCode` proprietà indicherà il motivo di hello dell'errore di indicizzazione hello:

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

Hello nella tabella seguente illustra vari documento i codici di stato che possono essere restituiti nella risposta hello hello. Si noti che alcune indica problemi relativi alla richiesta di hello stesso, mentre altri indicare le condizioni di errore temporaneo. Hello quest'ultimo che si consiglia di riprovare dopo un ritardo.

<table style="font-size:12">
    <tr>
        <th>Codice di stato</th>
        <th>Significato</th>
        <th>Non irreversibile</th>
        <th>Note</th>
    </tr>
    <tr>
        <td>200</td>
        <td>Il documento è stato modificato o eliminato correttamente.</td>
        <td>n/d</td>
        <td>Le operazioni di eliminazione sono <a href="https://en.wikipedia.org/wiki/Idempotence">idempotenti</a>. Vale a dire, anche se non esiste una chiave di documento nell'indice hello, il tentativo di un'operazione di eliminazione con tale chiave comporterà un codice di 200 stato.</td>
    </tr>
    <tr>
        <td>201</td>
        <td>Il documento è stato creato correttamente.</td>
        <td>n/d</td>
        <td></td>
    </tr>
    <tr>
        <td>400</td>
        <td>Si è verificato un errore nel documento hello che ne ha impedito da indicizzare.</td>
        <td>No</td>
        <td>messaggio di errore Hello in risposta hello indicherà qual è il documento hello.</td>
    </tr>
    <tr>
        <td>404</td>
        <td>Impossibile unire il documento Hello perché hello data chiave non esiste nell'indice hello.</td>
        <td>No</td>
        <td>Questo errore non si verifica per i caricamenti perché questi creano nuovi documenti e non si verifica per le eliminazioni perché queste sono <a href="https://en.wikipedia.org/wiki/Idempotence">idempotenti</a>.</td>
    </tr>
    <tr>
        <td>409</td>
        <td>Quando si tenta di tooindex un documento, è stato rilevato un conflitto di versione.</td>
        <td>Sì</td>
        <td>Ciò può verificarsi quando si cerca di hello tooindex stesso documento più di una volta contemporaneamente.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>indice di Hello è temporaneamente non disponibile perché è stato aggiornato con too'true set di flag hello 'allowIndexDowntime' '.</td>
        <td>Sì</td>
        <td></td>
    </tr>
    <tr>
        <td>503</td>
        <td>Il servizio di ricerca è temporaneamente non disponibile, probabilmente a causa di tooheavy carico.</td>
        <td>Sì</td>
        <td>Il codice deve attendere prima di ritentare in questo caso, o si rischia di prolungamento indisponibilità del servizio hello.</td>
    </tr>
</table> 

**Nota**: se il codice client riceve spesso una risposta 207, è possibile che il sistema di hello è sotto carico. È possibile verificarlo controllando hello `statusCode` proprietà 503. Se questo è il caso di hello, è consigliabile ***la limitazione delle richieste di indicizzazione***. In caso contrario, se non si riduce il traffico di indicizzazione, hello sistema inizi a rifiutare tutte le richieste con 503 errori.

Il codice di stato 429 indica che è stata superata la quota per il numero di hello di documenti per indice. È necessario creare un nuovo indice o effettuare l'aggiornamento per ottenere limiti di capacità più elevati.

**Esempio:**

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
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a>ricerca documenti
Oggetto **ricerca** operazione viene eseguita come una richiesta GET o POST e specifica i parametri che consentono di criteri di hello per la selezione di documenti corrispondenti.

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**Quando toouse registra anziché GET**

Quando si utilizza HTTP GET hello toocall **ricerca** API, è necessario tenere presente che la lunghezza hello dell'URL di richiesta di hello non può superare 8 KB toobe. Di solito è sufficiente per la maggior parte delle applicazioni. Alcune applicazioni, tuttavia, generano query di dimensioni molto grandi o espressioni di filtro OData. Per queste applicazioni è preferibile usare HTTP POST perché consente filtri e query di maggiori dimensioni rispetto a GET. Con POST, il numero di hello di condizioni o le clausole in una query hello limitano fattore, non pari a hello query non elaborati di hello poiché il limite di dimensione richiesta di hello per POST è circa 16 MB.

> [!NOTE]
> Anche se limite delle dimensioni richiesta POST hello è molto grande, le query di ricerca e filtro espressioni non possono essere arbitrariamente complesse. Per altre informazioni sulle limitazioni della complessità dei filtri e delle query di ricerca, vedere [Sintassi delle query Lucene](https://msdn.microsoft.com/library/mt589323.aspx) e [Sintassi delle espressioni di OData](https://msdn.microsoft.com/library/dn798921.aspx).
> 
> 

**Richiesta**

Per le richieste del servizio, è necessario usare il protocollo HTTPS. Hello **ricerca** richiesta può essere costruita usando i metodi POST o GET hello.

URI della richiesta Hello specifica quali tooquery di indice, per tutti i documenti corrispondenti ai parametri hello. I parametri vengono specificati nella stringa di query hello in caso di hello di richieste GET, e nella richiesta di hello richiede il corpo nel caso di hello di POST.

Come procedura consigliata quando si creano le richieste GET, ricordare troppo[codifica URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) query specifica i parametri quando si chiama hello API REST direttamente. Per le operazioni **Search** sono inclusi i parametri seguenti:

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

La codifica URL è consigliata solo nei hello sopra i parametri di query. Se si codifica URL inavvertitamente hello intera stringa di query (tutti gli elementi dopo hello?), le richieste si interromperanno.

Inoltre, la codifica URL è necessaria solo quando si chiama direttamente tramite API REST di ottenere hello. Non è necessaria alcuna codifica URL quando si chiama **ricerca** utilizzando POST, o quando si utilizza hello [libreria client .NET](https://msdn.microsoft.com/library/dn951165.aspx), che gestisce la codifica URL per l'utente.

<a name="SearchQueryParameters"></a>
**Parametri della query**

**Search** accetta diversi parametri che forniscono i criteri di query e specificano anche il comportamento di ricerca. Specificare questi parametri nell'URL hello stringa di query quando si chiama **ricerca** tramite GET e come proprietà JSON nel corpo della richiesta hello quando si chiama **ricerca** tramite POST. la sintassi di Hello per alcuni parametri è leggermente diversa tra GET e POST. Queste differenze sono riportate di seguito:

`search=[string]`(facoltativo): hello toosearch di testo per. Per impostazione predefinita, la ricerca viene eseguita in tutti i campi `searchable` a meno che non sia specificato `searchFields`. Durante la ricerca `searchable` campi, testo di ricerca hello stesso vengono assegnati token, in modo più termini possono essere separati da spazi (ad esempio: `search=hello world`). utilizzare qualsiasi termine, toomatch `*` (può essere utile per query di filtro booleane). Se si omette questo parametro ha lo stesso effetto dell'impostazione troppo hello`*`. Vedere [semplice sintassi di Query](https://msdn.microsoft.com/library/dn798920.aspx) per informazioni specifiche sulla sintassi di ricerca hello.

* **Nota**: risultati hello in alcuni casi possono essere sorprendenti quando si eseguono query su `searchable` campi. tokenizer Hello include logica toohandle casi comuni tooEnglish testo, ad esempio apostrofi, virgole in numeri, e così via. Ad esempio, `search=123,456` corrisponderà a un singolo termine 123,456 invece hello singoli termini 123 e 456, poiché le virgole vengono utilizzate come separatore delle migliaia per i numeri di grandi dimensioni in inglese. Per questo motivo, è consigliabile utilizzare lo spazio vuoto anziché termini tooseparate punteggiatura hello `search` parametro.

`searchMode=any|all`(facoltativo, valore predefinito è troppo`any`) - indica se uno o tutti i termini di ricerca hello devono corrispondere nel documento di ordine toocount hello come una corrispondenza.

`searchFields=[string]`(facoltativo): elenco di hello di toosearch di nomi di campo delimitati da virgole per hello il testo specificato. I campi di destinazione devono essere contrassegnati come `searchable`.

`queryType=simple|full`(facoltativo, valore predefinito è troppo`simple`): quando il testo di ricerca troppo "semplice" set viene interpretato utilizzando un linguaggio di query semplice che consente di simboli, ad esempio +, * e "". Per impostazione predefinita, le query vengono valutate in tutti i campi disponibili per la ricerca o nei campi indicati in `searchFields`in ogni documento. Quando il tipo di query hello è impostato troppo`full` testo di ricerca viene interpretato utilizzando linguaggio di query Lucene hello, che consente di cercare specifici di campo e ponderate. Vedere [semplice sintassi di Query](https://msdn.microsoft.com/library/dn798920.aspx) e [sintassi delle Query Lucene](https://msdn.microsoft.com/library/mt589323.aspx) per informazioni specifiche sulla sintassi di ricerca hello. 

> [!NOTE]
> Intervallo di ricerca in hello Lucene linguaggio di query non è supportato a favore $filter che offre funzionalità simili.
> 
> 

`moreLikeThis=[key]` (facoltativo) **Importante:** questa funzionalità è disponibile solo in `2015-02-28-Preview`. Questa opzione non può essere utilizzata in una query contenente parametri di ricerca di testo hello, `search=[string]`. Hello `moreLikeThis` parametro consente di trovare documenti simili documento toohello specificato dalla chiave di documento hello. Quando viene effettuata una richiesta di ricerca con `moreLikeThis`, viene generato un elenco di termini di ricerca in base a frequenza hello e delle condizioni nel documento di origine hello. Questi termini vengono quindi utilizzati toomake hello richiesta. Per impostazione predefinita, hello contenuto di tutti i `searchable` campi sono considerati a meno che non `searchFields` è usato toorestrict campi a cui vengono eseguita la ricerca.  

`$skip=#`(facoltativo): numero di hello della ricerca risultati tooskip; Non può essere maggiore di 100.000. Se necessario tooscan documenti in sequenza, ma non è possibile utilizzare `$skip` scadenza toothis limitazione, è consigliabile utilizzare `$orderby` su una chiave totalmente ordinata e `$filter` con un intervallo di query alternativa.

> [!NOTE]
> Quando si chiama **Search** con POST, questo parametro è denominato `skip` invece di `$skip`.
> 
> 

`$top=#`(facoltativo): numero di hello della ricerca risultati tooretrieve. Può essere utilizzato in combinazione con `$skip` tooimplement il paging sul lato client dei risultati della ricerca.

> [!NOTE]
> Quando si chiama **Search** con POST, questo parametro è denominato `top` invece di `$top`.
> 
> 

`$count=true|false`(facoltativo, valore predefinito è troppo`false`)-specifica se toofetch hello conteggio totale dei risultati. Si tratta di hello conteggio di tutti i documenti corrispondenti hello `search` e `$filter` parametri, ignorando `$top` e `$skip`. Impostazione del valore troppo`true` può avere un impatto sulle prestazioni. Si noti che il conteggio di hello restituito sono un'approssimazione.

> [!NOTE]
> Quando si chiama **Search** con POST, questo parametro è denominato `count` invece di `$count`.
> 
> 

`$orderby=[string]`(facoltativo): un elenco di espressioni delimitato da virgole toosort hello risultati da. Ogni espressione può essere un nome di campo o una chiamata toohello `geo.distance()` (funzione). Ogni espressione può essere seguito da `asc` tooindicated crescente, e `desc` tooindicate decrescente. valore predefinito di Hello è l'ordine crescente. Valori equivalenti verranno suddivise di punteggi di corrispondenza hello dei documenti. Se non `$orderby` viene specificato, l'ordinamento predefinito hello sarà decrescente in base al punteggio di corrispondenza documento. È previsto un limite di 32 clausole per `$orderby`.

> [!NOTE]
> Quando si chiama **Search** con POST, questo parametro è denominato `orderby` invece di `$orderby`.
> 
> 

`$select=[string]`(facoltativo): un elenco di campi separati da virgola tooretrieve. Se non viene specificato, sono inclusi tutti i campi contrassegnati come recuperabili nello schema di hello. È anche possibile richiedere esplicitamente tutti i campi impostando questo parametro troppo`*`.

> [!NOTE]
> Quando si chiama **Search** con POST, questo parametro è denominato `select` invece di `$select`.
> 
> 

`facet=[string]`(zero o più) - toofacet un campo da. Facoltativamente è possibile che la stringa hello contenga facet di hello toocustomize parametri espresso come delimitato da virgole `name:value` coppie. I parametri validi sono:

* `count`: numero massimo di termini facet. Il valore predefinito è 10. Non vi è alcun valore massimo, ma i valori più alti comportano una riduzione delle prestazioni corrispondenti, soprattutto se campo con facet hello contiene un numero elevato di termini univoci.
  * Ad esempio: `facet=category,count:5` Ottiene hello prime cinque categorie nei risultati di facet.  
  * **Nota**: se hello `count` parametro è minore di hello di termini univoci, risultati hello potrebbero non essere accurati. Questo è dovuto modo toohello query facet vengono distribuite tra partizioni. Aumento `count` in genere aumenta hello precisione dei conteggi di termini hello, ma un calo delle prestazioni.
* `sort`(uno dei `count` toosort *decrescente* dal conteggio, `-count` toosort *crescente* dal conteggio, `value` toosort *crescente* per valore, o `-value` toosort *decrescente* dal valore)
  * Ad esempio: `facet=category,count:3,sort:count` Ottiene hello prime tre categorie nei risultati di facet in ordine decrescente per il numero di hello di documenti con ogni nome di città. Ad esempio, se hello prime tre categorie sono Budget, Motel e Luxury e 5 riscontri dispone di Budget, Motel ha 6 e lusso è 4, quindi hello bucket sarà nell'ordine di hello Motel, Budget, Luxury.
  * Esempio: `facet=rating,sort:-value` genera bucket per tutte le classificazioni possibili, in ordine decrescente in base al valore. Ad esempio, se le classificazioni di hello sono da 1 too5, hello bucket avranno l'ordine 5, 4, 3, 2, 1, indipendentemente dal numero di documenti corrispondenti a ogni classificazione.
* `values` (valori numerici delimitati da pipe o valori `Edm.DateTimeOffset` che specificano un set dinamico di valori di immissione di facet)
  * Ad esempio: `facet=baseRate,values:10|20` produce tre bucket: uno per la tariffa di base 0 backup toobut 10 escluso, uno da 10 backup toobut non tra 20 e uno per 20 o superiore.
  * Esempio: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` genera due bucket, uno per hotel rinnovati prima del febbraio 2010 e uno per hotel rinnovati a partire dal 1° febbraio 2010.
* `interval` (intervallo di tipo Integer maggiore di 0 per i numeri o `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` per i valori di tipo data/ora)
  * Esempio: `facet=baseRate,interval:100` genera bucket in base agli intervalli di tariffe di base con dimensioni pari a 100. Se le tariffe di base sono tutte comprese tra € 60 e € 600, saranno presenti bucket per 0-100, 100-200, 200-300, 300-400, 400-500 e 500-600.
  * Esempio: `facet=lastRenovationDate,interval:year` genera un bucket per ogni anno in cui gli hotel sono stati rinnovati.
* `timeoffset` ([+-]hh:mm, [+-]hhmm o [+-]hh) `timeoffset` è facoltativo. Possono essere combinata solo con hello `interval` opzione e solo quando applicata tooa campo di tipo `Edm.DateTimeOffset`. il valore di Hello specifica tooaccount offset UTC di hello di tempo per l'impostazione di limiti di tempo.
  * Ad esempio: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` utilizza hello limiti di giorno che inizia in corrispondenza UTC 01:00:00 (mezzanotte nel fuso orario di destinazione hello)
* **Nota**: `count` e `sort` possono essere combinati in hello stessa specifica di facet, ma non può essere combinato con `interval` o `values`, e `interval` e `values` non possono essere combinati tra loro.
* **Nota**: se `timeoffset` non è specificato, i facet di intervallo per data e ora vengono calcolati in base all'ora UTC. Ad esempio: per `facet=lastRenovationDate,interval:day`, limiti di giorno di hello inizia alle 00:00:00 UTC. 

> [!NOTE]
> Quando si chiama **Search** con POST, questo parametro è denominato `facets` invece di `facet`. Viene specificato anche come matrice di stringhe JSON, dove ogni stringa è un'espressione facet distinta.
> 
> 

`$filter=[string]` (facoltativo): specifica un'espressione di ricerca strutturata nella sintassi standard di OData.

> [!NOTE]
> Quando si chiama **Search** con POST, questo parametro è denominato `filter` invece di `$filter`.
> 
> 

`highlight=[string]` (facoltativo): specifica un set di nomi di campo delimitati da virgole usati per evidenziare i risultati. Per l'evidenziazione dei risultati è possibile usare solo i campi `searchable` .

`highlightPreTag=[string]`(facoltativo, valore predefinito è troppo`<em>`): un tag che consente di anteporre evidenzia toohit di stringa. Deve essere impostato con `highlightPostTag`.

> [!NOTE]
> Quando si chiama **ricerca** utilizza GET, i caratteri riservati nell'URL hello devono essere codificati in percentuale (ad esempio, % 23 invece di #).
> 
> 

`highlightPostTag=[string]`(facoltativo, valore predefinito è troppo`</em>`)-un tag di stringa che aggiunge toohit evidenzia. Deve essere impostato con `highlightPreTag`.

> [!NOTE]
> Quando si chiama **ricerca** utilizza GET, i caratteri riservati nell'URL hello devono essere codificati in percentuale (ad esempio, % 23 invece di #).
> 
> 

`scoringProfile=[string]`(facoltativo): nome hello di un punteggio di profilo tooevaluate punteggi di corrispondenza per i documenti corrispondenti nei risultati di hello toosort ordine.

`scoringParameter=[string]`(zero o più) - indica i valori hello per ogni parametro definito in una funzione di punteggio (ad esempio, `referencePointParameter`) utilizzando il formato di hello `name-value1,value2,...`.

* Ad esempio, se hello profilo di punteggio definisce una funzione con un parametro denominato "mylocation" opzione stringa della query hello sarebbe `&scoringParameter=mylocation--122.2,44.8`. trattino prima Hello separa nome hello da elenco di valori hello, mentre il secondo trattino hello fa parte del valore del primo hello (longitudine in questo esempio).
* Per i parametri di punteggio, ad esempio per tag boosting che può contenere virgole, fare in modo che tutti i valori nell'elenco di hello utilizzando le virgolette singole. Se i valori di hello contengono virgolette singole, è possibile utilizzare caratteri di escape raddoppiando.
  * Ad esempio, se si dispone di un parametro denominato "mytag" aumento della priorità di tag e si desidera tooboost nel tag hello i valori "Hello, o ' Brien" e "Smith" query hello opzione stringa sarà `&scoringParameter=mytag-'Hello, O''Brien',Smith`. Si noti che le virgolette sono necessarie solo per i valori che contengono virgole.

> [!NOTE]
> Quando si chiama **Search** con POST, questo parametro è denominato `scoringParameters` invece di `scoringParameter`. Viene specificato come matrice di stringhe JSON, dove ogni stringa è una coppia `name-values` separata.
> 
> 

`minimumCoverage`(facoltativo, per impostazione predefinita too100) - un numero compreso tra 0 e 100 che indica la percentuale hello dell'indice hello che deve essere analizzata da una query di ricerca affinché hello query toobe segnalati come completati. Per impostazione predefinita, un indice hello deve essere disponibile o `Search` restituirà il codice di stato HTTP 503. Se si imposta `minimumCoverage` e `Search` ha esito positivo, verrà restituito HTTP 200 e includere un `@search.coverage` valore nella risposta hello indicando la percentuale hello dell'indice hello che è stato incluso nella query hello.

> [!NOTE]
> Se il valore di tooa di parametro è minore di 100 può risultare utile per garantire la disponibilità di ricerca neanche per i servizi con una sola replica. Tuttavia, non tutti i documenti corrispondenti vengono garantiti toobe presenti nei risultati della ricerca hello. Se il richiamo di ricerca più importanti dell'applicazione tooyour di disponibilità, allora è migliore tooleave `minimumCoverage` sul valore predefinito pari a 100.
> 
> 

`api-version=[string]` (elemento obbligatorio). versione di anteprima Hello è `api-version=2015-02-28-Preview`. Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

Nota: Per questa operazione, hello `api-version` è specificato come un parametro di query nell'URL hello indipendentemente dal fatto se si chiama **ricerca** con GET o POST.

**Intestazioni della richiesta**

Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.

* `api-key`: hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca. È un valore di stringa, univoco tooyour URL del servizio. Hello **ricerca** richiesta può specificare una chiave amministratore o una chiave di query per `api-key`.

È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello. È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello. Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.

**Corpo della richiesta**

Per GET: nessuno.

Per POST:

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

**Continuazione di risposte di ricerca parziali**

In alcuni casi ricerca di Azure non può restituire che tutti hello risultati richiesti in un'unica risposta di ricerca. Questa situazione può verificarsi per diversi motivi, ad esempio quando la query hello richiede molti documenti non specificando `$top` o specificando un valore per `$top` troppo grande. In questi casi, ricerca di Azure includerà hello `@odata.nextLink` annotazione nel corpo della risposta hello, nonché `@search.nextPageParameters` se si trattasse di una richiesta POST. È possibile utilizzare i valori hello di tooformulate queste annotazioni un'altra ricerca richiesta tooget hello parte successiva della risposta di ricerca hello. Si tratta di un ***continuazione*** di richiesta di ricerca originale hello e hello annotazioni vengono in genere chiamate ***i token di continuazione***. Vedere [esempio hello seguente](#SearchResponse) per informazioni dettagliate sulla sintassi di hello di queste annotazioni e in cui appaiono nel corpo della risposta hello. 

motivi Hello perché ricerca di Azure potrebbe restituire i token di continuazione sono specifiche dell'implementazione e soggette toochange. I client affidabili devono essere sempre pronti toohandle casi in cui vengono restituiti documenti meno del previsto e un token di continuazione è incluso toocontinue recupero di documenti. Inoltre è necessario utilizzare hello stesso metodo HTTP della richiesta originale di hello in ordine toocontinue. Se ad esempio si invia una richiesta GET, anche le richieste di continuazione inviate devono usare il metodo GET e lo stesso vale per il metodo POST.

<a name="SearchResponse"></a>
**Risposta**

Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

**Esempi:**

È possibile trovare esempi aggiuntivi nella hello [sintassi dell'espressione OData per ricerca di Azure](https://msdn.microsoft.com/library/azure/dn798921.aspx) pagina.

1)    Hello ricerca dell'indice in ordine decrescente per Data.

    GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }

2)    In una ricerca con facet, eseguire ricerche nell'indice hello e recuperare i facet per categorie, classificazioni, tag, nonché gli elementi con baseRate in intervalli specifici:

    GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }

3)    Utilizzando un filtro, restringere i risultati di query con facet precedenti hello dopo hello utente fa clic sulla classificazione 3 e della categoria "Motel":

    GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }

4) In una ricerca con facet, impostare un limite massimo per i termini univoci restituiti in una query. valore predefinito di Hello è 10, ma è possibile aumentare o ridurre questo valore utilizzando hello `count` parametro hello `facet` attributo:

    GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }

5)    Ricerca hello indice entro campi specifici; Ad esempio, un campo specifico del linguaggio:

    GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }

6) Indice di hello in più campi di ricerca. Ad esempio, è possibile archiviare e hello di eseguire query su campi ricercabili in più lingue, tutti all'interno dello stesso indice.  Se la lingua inglese e francese coesistono descrizioni in hello stesso documento, è possibile restituire hello in uno o tutti i risultati della query:

    GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }

Si noti che è possibile eseguire query su un solo indice alla volta. Non creare più indici per ogni lingua, a meno che non si prevede di tooquery uno alla volta.

7)    Paging - pagina 1 ° di hello Get di elementi (dimensioni di pagina sono 10):

    GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }

8)    Paging - pagina 2a di hello Get di elementi (dimensioni di pagina sono 10):

    GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }

9)    Recuperare un set specifico di campi:

    GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }

10)  Recuperare i documenti corrispondenti a un'espressione di filtro specifica:

    GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }

11) Eseguire ricerche nell'indice hello e restituire frammenti con evidenziazioni di riscontri

    GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }

12) Eseguire ricerche nell'indice hello e restituire documenti ordinati dal più vicino toofarther lontano da una posizione di riferimento

    GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }

13) Ricerca hello indice presupponendo che non vi è un profilo di punteggio denominato "geo" con due funzioni di assegnazione dei punteggi di distanza, che definisce un parametro denominato "currentLocation" e una definizione di un parametro denominato "lastLocation"

    GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }

14) Trovare documenti nell'indice hello utilizzando [semplice sintassi di query](https://msdn.microsoft.com/library/dn798920.aspx). Questa query restituisce gli hotel i cui campi ricercabili contengono hello termini "comfort" e "location" ma non "motel":

    GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }

Si noti hello utilizzo di `searchMode=all` sopra. Inclusione di questo parametro esegue l'override predefinito hello `searchMode=any`e si assicura che `-motel` significa "AND NOT" invece di "OR NOT". Senza `searchMode=all`, si ottiene "OR NOT" che vengono espansi anziché limitati i risultati della ricerca e può essere poco plausibile toosome utenti.

15) Trovare documenti nell'indice hello utilizzando [sintassi delle query lucene](https://msdn.microsoft.com/library/mt589323.aspx). Questa query restituisce gli hotel in cui il campo categoria hello contiene termini hello "budget" e i campi ricercabili tutti contenente la frase hello "rinnovata recente". Documenti che contengono la frase hello "recentemente rinnovata" rango più elevato in seguito a valore incremento del termine hello (3)

    GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full

    POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }

<a name="LookupAPI"></a>

## <a name="lookup-document"></a>Cercare un documento
Hello **Lookup Document** operazione recupera un documento da ricerca di Azure. Ciò è utile quando un utente fa clic su un risultato di ricerca specifico e si desidera toolook i dettagli specifici su tale documento.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

**Richiesta**

Per le richieste del servizio, è necessario usare il protocollo HTTPS. Hello **Lookup Document** richiesta può essere costruita come indicato di seguito.

    GET /indexes/[index name]/docs/key?[query parameters]

In alternativa, è possibile utilizzare sintassi di OData hello tradizionali per la ricerca della chiave:

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

Hello URI della richiesta include [nome di un indice] e [key], che specifica quali tooretrieve documento da quale indice. È possibile recuperare un solo documento alla volta. Utilizzare **ricerca** tooget più documenti in una singola richiesta.

**Parametri della query**

`$select=[string]`(facoltativo): un elenco di campi separati da virgola tooretrieve. Se non specificato o impostato troppo`*`, tutti i campi contrassegnati come recuperabili nello schema hello sono inclusi nella proiezione hello.

`api-version=[string]` (elemento obbligatorio). versione di anteprima Hello è `api-version=2015-02-28-Preview`. Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

Nota: Per questa operazione, hello `api-version` viene specificato come un parametro di query.

**Intestazioni della richiesta**

Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.

* `api-key`: hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca. È un valore di stringa, univoco tooyour URL del servizio. Hello **Lookup Document** richiesta può specificare una chiave amministratore o una chiave di query per `api-key`.

È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello. È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello. Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.

**Corpo della richiesta**

Nessuno.

**Risposta**

Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

**Esempio**

Documento hello ricerca con chiave '2'

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

Documento hello ricerca con chiave '3' utilizzando la sintassi di OData:

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a>Contare i documenti
Hello **Count Documents** operazione recupera un conteggio del numero di hello di documenti in un indice di ricerca. Hello `$count` sintassi fa parte di hello protocollo OData.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

**Richiesta**

Per le richieste del servizio, è necessario usare il protocollo HTTPS. Hello **Count Documents** richiesta può essere costruita utilizzando il metodo GET hello.

Hello [nome indice] nell'URI della richiesta hello hello servizio tooreturn indica un conteggio di tutti gli elementi nella raccolta documenti di hello dell'indice specificato di hello.

`api-version=[string]` (elemento obbligatorio). versione di anteprima Hello è `api-version=2015-02-28-Preview`. Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

**Intestazioni della richiesta**

Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo.

* `Accept`: Questo valore deve essere impostato troppo`text/plain`.
* `api-key`: hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca. È un valore di stringa, univoco tooyour URL del servizio. Hello **Count Documents** richiesta può specificare una chiave amministratore o una chiave di query per `api-key`.

È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello. È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello. Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.

**Corpo della richiesta**

Nessuno.

**Risposta**

Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.

corpo della risposta Hello contiene il valore di count hello come un valore integer formattato in testo normale.

<a name="Suggestions"></a>

## <a name="suggestions"></a>Suggerimenti
Hello **suggerimenti** operazione recupera i suggerimenti in base a input di ricerca parziale. Viene in genere usato in suggerimenti di ricerca finestre tooprovide durante la digitazione, come gli utenti immettono i termini di ricerca.

Le richieste di suggerimenti hanno lo scopo di suggerire documenti di destinazione, in modo hello suggerito testo può essere ripetuto se corrispondano a più documenti hello stesso input di ricerca. È possibile utilizzare `$select` tooretrieve altri campi (inclusa chiave documento hello) del documento in modo che è possibile stabilire quale documento è origine hello per ogni suggerimento.

Un'operazione **Suggestions** viene generata come richiesta GET.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**Quando toouse registra anziché GET**

Quando si utilizza HTTP GET hello toocall **suggerimenti** API, è necessario tenere presente che la lunghezza hello dell'URL di richiesta di hello non può superare 8 KB toobe. Di solito è sufficiente per la maggior parte delle applicazioni. Alcune applicazioni generano tuttavia query di dimensioni molto grandi, specialmente le espressioni di filtro OData. Per queste applicazioni è preferibile usare HTTP POST perché consente filtri di maggiori dimensioni rispetto a GET. Con POST, un numero di clausole in un filtro hello fattore limitante hello, hello non dimensioni della stringa di filtro non elaborato hello poiché il limite di dimensione richiesta di hello per POST è circa 16 MB.

> [!NOTE]
> Anche se limite delle dimensioni richiesta POST hello è molto grande, le espressioni di filtro non possono essere arbitrariamente complesse. Per altre informazioni sulle limitazioni della complessità dei filtri vedere [Sintassi delle espressioni di OData](https://msdn.microsoft.com/library/dn798921.aspx) .
> 
> 

**Richiesta**

Per le richieste del servizio, è necessario usare il protocollo HTTPS. Hello **suggerimenti** richiesta può essere costruita usando i metodi POST o GET hello.

URI della richiesta Hello Specifica nome hello di hello tooquery di indice. Parametri, ad esempio al termine di ricerca immesso parzialmente hello, vengono specificati nella stringa di query hello in caso di hello di richieste GET, e nella richiesta di hello richiede il corpo nel caso di hello di POST.

Come procedura consigliata quando si creano le richieste GET, ricordare troppo[codifica URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) query specifica i parametri quando si chiama hello API REST direttamente. Per le operazioni **Suggestions** sono inclusi i parametri seguenti:

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

La codifica URL è consigliata solo nei hello sopra i parametri di query. Se si codifica URL inavvertitamente hello intera stringa di query (tutti gli elementi dopo hello?), le richieste si interromperanno.

Inoltre, la codifica URL è necessaria solo quando si chiama direttamente tramite API REST di ottenere hello. Non è necessaria alcuna codifica URL quando si chiama **suggerimenti** utilizzando POST, o quando si utilizza hello [libreria client .NET](https://msdn.microsoft.com/library/dn951165.aspx), che gestisce la codifica URL per l'utente.

**Parametri della query**

**Suggestions** accetta diversi parametri che forniscono i criteri di query e specificano anche il comportamento di ricerca. Specificare questi parametri nell'URL hello stringa di query quando si chiama **suggerimenti** tramite GET e come proprietà JSON nel corpo della richiesta hello quando si chiama **suggerimenti** tramite POST. la sintassi di Hello per alcuni parametri è leggermente diversa tra GET e POST. Queste differenze sono riportate di seguito:

`search=[string]`-hello toosuggest toouse di testo di ricerca. Deve essere composto da un minimo di 1 carattere e da un massimo di 100 caratteri.

`highlightPreTag=[string]`(facoltativo): un tag di stringa che viene aggiunto toosearch riscontri. Deve essere impostato con `highlightPostTag`.

> [!NOTE]
> Quando si chiama **suggerimenti** utilizza GET, i caratteri riservati nell'URL hello devono essere codificati in percentuale (ad esempio, % 23 invece di #).
> 
> 

`highlightPostTag=[string]`(facoltativo): un tag di stringa che aggiunge toosearch riscontri. Deve essere impostato con `highlightPreTag`.

> [!NOTE]
> Quando si chiama **suggerimenti** utilizza GET, i caratteri riservati nell'URL hello devono essere codificati in percentuale (ad esempio, % 23 invece di #).
> 
> 

`suggesterName=[string]`-nome hello di strumento suggerimenti hello come specificato in hello `suggesters` raccolta che fa parte della definizione di indice hello. Un elemento `suggester` determina i campi analizzati per i termini di query suggeriti. Per informazioni dettagliate, vedere [Componenti per il suggerimento](#Suggesters) .

`fuzzy=[boolean]`(facoltativo, il valore predefinito = false), quando questa opzione impostata tootrue API trova i suggerimenti anche se è presente un carattere sostituto o manca nel testo di ricerca hello. Anche se offre un'esperienza migliore in alcuni scenari, influisce negativamente sulle prestazioni poiché le ricerche con suggerimenti fuzzy sono più lente e utilizzano più risorse.

`searchFields=[string]`(facoltativo): elenco hello di toosearch di nomi di campo delimitati da virgole per hello il testo di ricerca specificato. I campi di destinazione devono essere abilitati per suggerimenti.

`$top=#`(facoltativo, il valore predefinito = 5)-numero di suggerimenti tooretrieve hello. Deve essere un numero compreso tra 1 e 100.

> [!NOTE]
> Quando si chiama **Suggestions** con POST, questo parametro è denominato `top` invece di `$top`.
> 
> 

`$filter=[string]`(facoltativo): un'espressione che filtra i documenti hello considerati per i suggerimenti.

> [!NOTE]
> Quando si chiama **Suggestions** con POST, questo parametro è denominato `filter` invece di `$filter`.
> 
> 

`$orderby=[string]`(facoltativo): un elenco di espressioni delimitato da virgole toosort hello risultati da. Ogni espressione può essere un nome di campo o una chiamata toohello `geo.distance()` (funzione). Ogni espressione può essere seguito da `asc` tooindicated crescente, e `desc` tooindicate decrescente. valore predefinito di Hello è l'ordine crescente. È previsto un limite di 32 clausole per `$orderby`.

> [!NOTE]
> Quando si chiama **Suggestions** con POST, questo parametro è denominato `orderby` invece di `$orderby`.
> 
> 

`$select=[string]`(facoltativo): un elenco di campi separati da virgola tooretrieve. Se non viene specificato, solo hello chiave di documento e viene restituito il testo di suggerimento. È possibile richiedere in modo esplicito tutti i campi impostando questo parametro troppo`*`.

> [!NOTE]
> Quando si chiama **Suggestions** con POST, questo parametro è denominato `select` invece di `$select`.
> 
> 

`minimumCoverage`(facoltativo, per impostazione predefinita too80) - un numero compreso tra 0 e 100 che indica la percentuale hello dell'indice hello che deve essere analizzata da una query di suggerimenti affinché hello query toobe segnalati come completati. Per impostazione predefinita, deve essere disponibile almeno l'80% di indice hello o `Suggest` restituirà il codice di stato HTTP 503. Se si imposta `minimumCoverage` e `Suggest` ha esito positivo, verrà restituito HTTP 200 e includere un `@search.coverage` valore nella risposta hello indicando la percentuale hello dell'indice hello che è stato incluso nella query hello.

> [!NOTE]
> Se il valore di tooa di parametro è minore di 100 può risultare utile per garantire la disponibilità di ricerca neanche per i servizi con una sola replica. Tuttavia, non tutti i suggerimenti corrispondenti vengono garantiti toobe presenti nei risultati di hello. Tenere presente è più importante tooyour di disponibilità, quindi di procedure non toolower `minimumCoverage` sotto il relativo valore predefinito 80.
> 
> 

`api-version=[string]` (elemento obbligatorio). versione di anteprima Hello è `api-version=2015-02-28-Preview`. Per informazioni dettagliate sulle altre versioni, vedere [Controllo delle versioni di Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn864560.aspx) .

Nota: Per questa operazione, hello `api-version` è specificato come un parametro di query nell'URL hello indipendentemente dal fatto se si chiama **suggerimenti** con GET o POST.

**Intestazioni della richiesta**

Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo

* `api-key`: hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca. È un valore di stringa, univoco tooyour URL del servizio. Hello **suggerimenti** richiesta può specificare una chiave amministratore o una chiave di query come hello `api-key`.

È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello. È possibile ottenere il nome di servizio hello e `api-key` dal dashboard servizi nel portale di Azure hello. Vedere [creare un servizio di ricerca di Azure nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.

**Corpo della richiesta**

Per GET: nessuno.

Per POST:

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

**Risposta**

Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

Se l'opzione di proiezione di hello tooretrieve utilizzato i campi che sono inclusi in ogni elemento della matrice hello:

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

**Esempio**

Recuperare 5 suggerimenti, in cui hello input di ricerca parziale è "lux"

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
