---
title: architettura del motore (Lucene) ricerca testo aaaFull in ricerca di Azure | Documenti Microsoft
description: Spiegazione di Lucene documento e l'elaborazione il recupero dei concetti relativi alle query per la ricerca full-text, come tooAzure correlati ricerca.
services: search
manager: jhubbard
author: yahnoosh
documentationcenter: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/06/2017
ms.author: jlembicz
ms.openlocfilehash: c6d1bea8d40154fd9237b9e44584cdfcd193cbd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-full-text-search-works-in-azure-search"></a>Funzionamento della ricerca full-text in Ricerca di Azure

Questo articolo si rivolge agli sviluppatori che hanno bisogno di una conoscenza più approfondita circa il funzionamento della ricerca full-text di Lucene in Ricerca di Azure. Per le query di testo, Ricerca di Azure fornirà i risultati previsti nella maggior parte degli scenari, ma in alcuni casi è possibile ottenere un risultato che sembrerà in qualche modo "strano". In queste situazioni, con uno sfondo hello quattro fasi di esecuzione di query Lucene (analisi lessicale, analisi di query, documento corrispondente, il punteggio) consentono di identificare le modifiche specifiche tooquery parametri o un indice di configurazione che apporterà hello risultato desiderato. 

> [!Note] 
> Ricerca di Azure usa Lucene per la ricerca full-text, ma l'integrazione con Lucene non è completa. È in modo selettivo espongono ed estendere Lucene funzionalità tooenable hello scenari importanti tooAzure ricerca. 

## <a name="architecture-overview-and-diagram"></a>Panoramica e diagramma dell'architettura

Elaborazione di una query di ricerca full-text inizia con i termini di ricerca tooextract testo hello query di analisi. il motore di ricerca Hello Usa un tooretrieve indicizzare i documenti con termini corrispondenti. I termini di query singole sono suddivisi in alcuni casi e ricostituita nel nuovo form toocast una rete più ampia su ciò che può essere considerato come corrispondenza potenziale. Un set di risultati viene quindi ordinato per un pertinenza punteggio tooeach assegnato corrispondente documento singolo. Quelli nella parte superiore di hello di hello classificata elenco vengono restituiti l'applicazione chiamante toohello.

L'esecuzione di query riproposte presenta quattro fasi: 

1. Analisi della query 
2. Analisi lessicale 
3. Recupero dei documenti 
4. Assegnazione dei punteggi 

diagramma di Hello seguente illustra hello componenti utilizzati tooprocess una richiesta di ricerca. 

 ![Diagramma dell'architettura della query di Lucene in Ricerca di Azure][1]


| Componenti chiave | Descrizione funzionale | 
|----------------|------------------------|
|**Parser della query** | Separare i termini di query dagli operatori di query e creare il motore di ricerca toohello hello query struttura (albero di query) toobe inviato. |
|**Analizzatori** | Eseguire l'analisi lessicale sui termini della query. Questo processo può implicare la trasformazione, la rimozione o l'espansione dei termini della query. |
|**Index** | Una struttura di dati efficiente utilizzato toostore e organizzare ricerca termini estratti da documenti indicizzati. |
|**Motore di ricerca** | Recupera e punteggi di corrispondenza in base al contenuto hello di hello documenti indice invertito. |

## <a name="anatomy-of-a-search-request"></a>Anatomia di una richiesta di ricerca

Una richiesta di ricerca è una specifica completa di ciò che deve essere restituito in un set di risultati. Nella forma più semplice, è una query vuota senza alcun tipo di criterio. Un esempio più realistico include parametri, diversi termini, i campi toocertain probabilmente con ambito, con probabilmente un'espressione di filtro e ordinamento delle regole di query.  

esempio Hello è una richiesta di ricerca è possibile inviare tooAzure ricerca utilizzando hello [API REST](https://docs.microsoft.com/rest/api/searchservice/search-documents).  

~~~~
POST /indexes/hotels/docs/search?api-version=2016-09-01 
{  
    "search": "Spacious, air-condition* +\"Ocean view\"",  
    "searchFields": "description, title",  
    "searchMode": "any",
    "filter": "price ge 60 and price lt 300",  
    "orderby": "geo.distance(location, geography'POINT(-159.476235 22.227659)')", 
    "queryType": "full" 
 } 
~~~~

Per questa richiesta, il motore di ricerca hello hello seguenti:

1. Filtra i documenti in cui il prezzo di hello almeno $60 e inferiore a $300.
2. Esegue query hello. In questo esempio, la query di ricerca hello costituito frasi e termini: `"Spacious, air-condition* +\"Ocean view\""` (gli utenti in genere non immettono segni di punteggiatura, ma incluso nell'esempio hello consente tooexplain come gli analizzatori di gestirlo). Per questa query, il motore di ricerca hello analizza descrizione hello e i campi titolo specificati `searchFields` per documenti che contengono "Vista sull'Oceano" e inoltre termine hello "spazioso" o su termini che iniziano con il prefisso hello "air-condition". Hello `searchMode` parametro è utilizzato toomatch su qualsiasi termine (impostazione predefinita) o tutti, per i casi in cui non è richiesto in modo esplicito un termine (`+`).
3. Gli ordini hello set risultante di hotel da prossimità tooa geography percorso specificato e quindi restituiti toohello di applicazione chiamante. 

Hello maggior parte di questo articolo riguarda l'elaborazione di hello *query di ricerca*: `"Spacious, air-condition* +\"Ocean view\""`. Il filtro e l'ordinamento non appartengono all'ambito. Per ulteriori informazioni, vedere hello [la documentazione di riferimento API di ricerca](https://docs.microsoft.com/rest/api/searchservice/search-documents).

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a>Fase 1: Analisi della query 

Come accennato, la stringa di query hello è hello prima riga della richiesta di hello: 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

il parser separa gli operatori di query di Hello (ad esempio `*` e `+` nell'esempio hello) da ricerca di termini e annullamento della costruzione delle query di ricerca hello in *sottoquery* di un tipo supportato: 

+ *query del termine* per i termini singoli (ad esempio spazioso)
+ *query della frase* per i termini tra virgolette (ad esempio vista oceano)
+ *query del prefisso* per i termini seguiti da un operatore prefisso `*` (ad esempio, aria condizionata)

Per un elenco completo dei tipi di query supportati vedere [Sintassi di query Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

Operatori associati a una sottoquery determinano se la query hello "deve essere" o "deve essere" soddisfatti in ordine per un documento toobe considerata una corrispondenza. Ad esempio, `+"Ocean view"` "deve" toohello scadenza `+` operatore. 

parser di query Hello Ristruttura sottoquery hello in un *della struttura della query* (una struttura interna che rappresenta la query hello) passa nel motore di ricerca toohello. Nella prima fase hello di query di analisi, la struttura della query hello è simile al seguente.  

 ![Boolean query searchmode any][2]

### <a name="supported-parsers-simple-and-full-lucene"></a>Parser supportati: Lucene semplice e completa 

 La Ricerca di Azure espone due diversi linguaggi di query, `simple` (impostazione predefinita) e `full`. Per impostazione hello `queryType` parametro con la richiesta di ricerca, comunicare hello query parser del linguaggio di query si sceglie in modo che rilevi come toointerpret hello operatori e sintassi. Hello [lingua query semplice](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) è intuitiva e potente, l'input dell'utente toointerpret spesso adatto come-senza elaborazione sul lato client. Supporta operatori di query familiari dai motori di ricerca Web. Hello [il linguaggio di query completo Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), che si ottiene impostando `queryType=full`, estende il linguaggio di query semplice hello predefinito aggiungendo supporto per più operatori e tipi di query come carattere jolly, fuzzy regex e le query con ambito di campo. Ad esempio, un'espressione regolare inviata nella sintassi di query semplice verrebbe interpretata come una stringa di query e non come un'espressione. richiesta di esempio Hello in questo articolo viene utilizzato il linguaggio di query completo Lucene hello.

### <a name="impact-of-searchmode-on-hello-parser"></a>Impatto di searchMode nel parser hello 

Un altro parametro di richiesta di ricerca che interessa l'analisi è hello `searchMode` parametro. Controlla l'operatore predefinito hello per le query booleane: qualsiasi (impostazione predefinita) o tutti.  

Quando `searchMode=any`, ovvero hello spazio delimitatore spazioso predefinita hello e air-condition è o (`||`), rendendo equivalente al testo di query di esempio hello: 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

Gli operatori espliciti, ad esempio `+` in `+"Ocean view"`, non sono ambigui nella costruzione delle query booleano (termine hello *deve* corrispondono). È meno ovvio come condizioni di hello toointerpret rimanenti: spazioso e air-condition. Dovrebbe motore di ricerca hello trovare corrispondenze nella vista sull'Oceano *e* spazioso *e* air-condition? O deve trovare vista sull'Oceano più *uno* di hello rimanenti condizioni? 

Per impostazione predefinita (`searchMode=any`), il motore di ricerca hello presuppone l'interpretazione di più ampia di hello. Uno dei campi *dovrebbe* essere associato, riflettendo la semantica di "or". struttura ad albero di query iniziale Hello illustrato in precedenza, con hello due operazioni "deve", Mostra hello predefinito.  

Si supponga che abbiamo ora impostato `searchMode=all`. In questo caso, lo spazio di hello viene interpretato come un'operazione "e". Ognuna delle condizioni rimanenti hello devono essere entrambi presente in hello documento tooqualify come una corrispondenza. query di esempio risultante Hello verrebbe interpretato come segue: 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

Una struttura ad albero di query modificata per la query sarà come segue, in cui un documento corrispondente è l'intersezione di hello di tutti e tre le sottoquery: 

 ![Boolean query searchmode all][3]

> [!Note] 
> La scelta `searchMode=any` rispetto a `searchMode=all` è una scelta migliore a cui si arriva eseguendo le query rappresentative. Gli utenti che sono probabilmente tooinclude operatori (comune quando si archivia il documento di ricerca) può risultare risultati più intuitiva se `searchMode=all` informa i costrutti delle query booleano. Per ulteriori informazioni sull'interazione di hello tra `searchMode` e operatori, vedere [semplice sintassi di query](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a>Fase 2: Analisi lessicale 

Processo analizzatori lessicali *termini query* e *una frase query* dopo hello query albero. Un analizzatore accetta hello tooit dato di input di testo dal parser hello processi hello testo e quindi invia di nuovo in formato token termini toobe incorporato in hello della struttura della query. 

Hello form più comuni di analisi lessicale è *l'analisi linguistica* che consente di trasformare i termini di query in base a tooa specifico di regole specificato linguaggio: 

* La riduzione di un modulo di query termine toohello radice di una parola 
* Rimozione di parole non essenziali (parole non significative, ad esempio "the" o "and" in inglese) 
* Suddivisione di una parola composta nelle parti che la compongono 
* Trasformazione in lettere minuscole di una parola in lettere maiuscole 

Tutte queste operazioni tendono tooerase differenze tra l'input di testo hello fornito dai termini hello hello e utente, archiviati nell'indice hello. Tali operazioni superano l'elaborazione del testo e richiedono una conoscenza approfondita del linguaggio hello. tooadd questo livello di compatibilità linguistico, ricerca di Azure supporta un lungo elenco di [gli analizzatori del linguaggio](https://docs.microsoft.com/rest/api/searchservice/language-support) da Lucene e Microsoft.

> [!Note]
> Requisiti per l'analisi può variare da tooelaborate minimo a seconda dello scenario. È possibile controllare la complessità dell'analisi lessicale hello selezionando una delle analizzatori hello predefinita o creando un proprio [analizzatore personalizzato](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search). Gli analizzatori sono campi toosearchable con ambito e vengono specificati come parte di una definizione di campo. In questo modo si analisi lessicale toovary in base al campo. Non viene specificato, hello *standard* analizzatore Lucene viene utilizzato.

Nell'esempio precedente tooanalysis, una virgola che hello parser di query vengono interpretati come parte del termine della query hello (una virgola non viene considerata un operatore di query language) dell'albero di query iniziale hello ha termine hello "Spacious", con una "S" maiuscola.  

Quando l'analizzatore predefinito hello elabora termine hello, verrà minuscolo "Vista sull'Oceano" e "spazioso" e rimuovere carattere virgola hello. Struttura query modificata Hello apparirà come segue: 

 ![Query booleana con termini analizzati][4]

### <a name="testing-analyzer-behaviors"></a>Comportamenti dell'analizzatore del test 

comportamento di Hello di un analizzatore può essere testato usando hello [analizzare API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer). Fornire testo hello da tooanalyze toosee genererà i termini dato analyzer. Ad esempio, toosee elabora come analizzatore standard hello hello testo "air-condition", è possibile emettere hello seguito richiesta:

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

analizzatore standard Hello suddivide il testo di input hello in hello due token, li annotazione con attributi quali iniziale e offset finale (utilizzato per l'evidenziazione dei riscontri), nonché la loro posizione (utilizzato per la corrispondenza di una frase) seguenti:

~~~~
{  
  "tokens": [
    {
      "token": "air",
      "startOffset": 0,
      "endOffset": 3,
      "position": 0
    },
    {
      "token": "condition",
      "startOffset": 4,
      "endOffset": 13,
      "position": 1
    }
  ]
}
~~~~

### <a name="exceptions-toolexical-analysis"></a>Analisi toolexical eccezioni 

Analisi lessicale applicano tooquery solo i tipi che richiedono i termini, una query di termine o una query di una frase. Tipi di tooquery con termini incompleti: query di prefisso, la query con caratteri jolly, query regex – o tooa fuzzy query non è applicabile. Tali tipi, tra cui query prefisso hello con termini di query *air-condition\**  in questo esempio, vengono aggiunti direttamente sui toohello albero della query, ignorando fase di analisi hello. Hello solo trasformazione eseguita in base alle esigenze di questi tipi di query è minuscola.

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a>Fase 3: Recupero dei documenti 

Il recupero di documento fa riferimento toofinding documenti con i termini corrispondenti nell'indice hello. Questa fase viene spiegata meglio attraverso un esempio. Iniziamo con un indice gli alberghi con hello segue uno schema semplice: 

~~~~
{   
    "name": "hotels",     
    "fields": [     
        { "name": "id", "type": "Edm.String", "key": true, "searchable": false },     
        { "name": "title", "type": "Edm.String", "searchable": true },     
        { "name": "description", "type": "Edm.String", "searchable": true }
    ] 
} 
~~~~

Si supponga inoltre che l'indice contiene hello quattro documenti seguenti: 

~~~~
{ 
    "value": [
        {         
            "id": "1",         
            "title": "Hotel Atman",         
            "description": "Spacious rooms, ocean view, walking distance toohello beach."   
        },       
        {         
            "id": "2",         
            "title": "Beach Resort",        
            "description": "Located on hello north shore of hello island of Kauaʻi. Ocean view."     
        },       
        {         
            "id": "3",         
            "title": "Playa Hotel",         
            "description": "Comfortable, air-conditioned rooms with ocean view."
        },       
        {         
            "id": "4",         
            "title": "Ocean Retreat",         
            "description": "Quiet and secluded"
        }    
    ]
}
~~~~

**Come vengono indicizzati termini**

recupero di toounderstand, è utile tooknow alcune nozioni fondamentali per l'indicizzazione. unità di Hello di archiviazione è un indice invertito, uno per ogni campo di ricerca. In un indice invertito è presente un elenco ordinato di tutti i termini derivanti da tutti i documenti. Esegue il mapping di ogni termine toohello elenco di documenti in cui si verifica, come è evidente nel seguente esempio hello.

condizioni di hello tooproduce in un indice invertito, il motore di ricerca di hello esegue analisi lessicale sul contenuto dei documenti, hello toowhat simile si verifica durante l'elaborazione delle query. Input di testo vengono passati tooan analyzer in minuscolo, prive di punteggiatura e così via, a seconda della configurazione dell'analizzatore hello. È comune, ma non obbligatorio, toouse hello stesso analizzatori per la ricerca e le operazioni di indicizzazione in modo che i termini di query somigliare più ad termini all'interno dell'indice hello.

> [!Note]
> Ricerca di Azure consente di specificare diversi analizzatori per l'indicizzazione e la ricerca tramite parametri di campo aggiuntivi `indexAnalyzer` e `searchAnalyzer`. Se non viene specificato, hello analyzer impostata con hello `analyzer` proprietà viene utilizzata per l'indicizzazione e ricerca.  

**Indice invertito per i documenti di esempio**

Restituzione tooour, ad esempio, hello **titolo** campo indice invertito hello è simile al seguente:

| Termine | Elenco di documenti |
|------|---------------|
| atman | 1 |
| spiaggia | 2 |
| hotel | 1, 3 |
| oceano | 4  |
| playa | 3 |
| resort | 3 |
| rifugio | 4 |

Nel campo titolo hello, solo *hotel* viene visualizzato in due documenti: 1, 3.

Per hello **descrizione** campo indice hello è come segue:

| Termine | Elenco di documenti |
|------|---------------|
| aria | 3
| e | 4
| spiaggia | 1
| condizionata | 3
| comodo | 3
| distance | 1
| isola | 2
| kauaʻi | 2
| posizionato | 2
| nord | 2
| oceano | 1, 2, 3
| di | 2
| in |2
| tranquillo | 4
| camere  | 1, 3
| appartato | 4
| costa | 2
| spazioso | 1
| Hello | 1, 2
| Anche| 1
| view | 1, 2, 3
| passeggiata | 1
| con | 3


**Corrispondenza dei termini di query con i termini indicizzati**

Indici invertito hello precedenti, verrà restituito nella query di esempio toohello provvisto di vedere documenti corrispondenti come vengono rilevati per la query di esempio. Richiamare che tale struttura ad albero di query finale hello è simile al seguente: 

 ![Query booleana con termini analizzati][4]

Durante l'esecuzione di query, le singole query vengono eseguite in campi ricercabili hello in modo indipendente. 

+ Hello TermQuery "spazioso", corrisponde a 1 (Hotel Atman) di documento. 

+ Hello PrefixQuery, "air-condition *", non corrisponde a tutti i documenti. 

  Si tratta di un comportamento che a volte confonde gli sviluppatori. Sebbene hello air-conditioned esiste nel documento hello, viene suddivisa in due termini dall'analizzatore di hello predefinito. È importante ricordare che le query di prefisso, che contengono termini parziali, non vengono analizzate. Pertanto i termini con prefisso "air-condition" vengono ricercati in hello indice invertito e non trovato.

+ Hello PhraseQuery "Vista sull'Oceano," Cerca termini hello "Oceano" e "visualizzazione" e verifica di prossimità hello delle condizioni nel documento originale hello. Documenti 1, 2 e 3 corrispondano alla query nel campo Descrizione hello. Il documento di avviso 4 è Oceano termine hello nel titolo hello ma non è considerato una corrispondenza, come, stiamo cercando la frase "Vista sull'Oceano" hello, anziché a singole parole. 

> [!Note]
> Una query di ricerca viene eseguita in modo indipendente rispetto a tutti i campi ricercabili nell'indice di ricerca di Azure a meno che non si limita i campi di hello impostato con hello hello `searchFields` parametro, come illustrato nella richiesta di ricerca di esempio hello. Vengono restituiti i documenti che corrispondono in uno dei campi hello selezionato. 

In hello intero, per query hello in questione, documenti hello corrispondenti sono 1, 2, 3. 

## <a name="stage-4-scoring"></a>Fase 4: Assegnazione dei punteggi  

Ad ogni documento in un set di risultati di ricerca viene assegnato un punteggio di pertinenza. funzione Hello del punteggio di pertinenza hello è maggiore di tali documenti che meglio risposta a un utente di domanda espresse dalla query di ricerca hello toorank. Hello punteggio viene calcolato in base alle proprietà statistiche dei termini corrispondenti. Componenti di base di hello punteggio formula hello è [TF/IDF (frequenza di termini documento frequenza inverso)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf). Nelle query che contiene termini comuni e rari, TF/IDF Alza di livello risultati contenenti termini rari hello. Ad esempio in un indice ipotetico con tutti gli articoli di Wikipedia, documenti query hello corrispondente da *presidente hello*, documenti corrispondenza *presidente* sono considerati più pertinenti di ricerca in documenti *il*.


### <a name="scoring-example"></a>Esempio di assegnazione dei punteggi

Richiamo hello tre documenti che soddisfano la query di esempio:
~~~~
search=Spacious, air-condition* +"Ocean view"  
~~~~
~~~~
{  
  "value": [
    {
      "@search.score": 0.25610128,
      "id": "1",
      "title": "Hotel Atman",
      "description": "Spacious rooms, ocean view, walking distance toohello beach."
    },
    {
      "@search.score": 0.08951007,
      "id": "3",
      "title": "Playa Hotel",
      "description": "Comfortable, air-conditioned rooms with ocean view."
    },
    {
      "@search.score": 0.05967338,
      "id": "2",
      "title": "Ocean Resort",
      "description": "Located on a cliff on hello north shore of hello island of Kauai. Ocean view."
    }
  ]
}
~~~~

Documentare meglio 1 query hello corrispondente perché entrambi hello termine *spazioso* e frase obbligatorio hello *vista sull'Oceano* si verificano nel campo Descrizione hello. Hello due documenti che corrispondono solo la frase hello *vista sull'Oceano*. Potrebbe sorprendere il punteggio di pertinenza hello per documento 2 e 3 è diversa, anche se di corrispondenza con query hello in hello allo stesso modo. Infatti hello punteggio formula include più componenti appena TF/IDF. In questo caso al documento 3 è stato assegnato un punteggio leggermente maggiore perché la sua descrizione è più breve. Informazioni su [Lucene pratiche di punteggio Formula](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) toounderstand come lunghezza del campo e altri fattori possono incidere sui hello punteggio di pertinenza.

Per alcune query di tipo (carattere jolly, prefisso, regex) contribuiscono sempre un costante punteggio complessivo toohello punteggio dei documenti. In questo modo corrispondenze trovate tramite query espansione toobe inclusi nei risultati di hello, ma senza influire sul calcolo della pertinenza hello. 

Un esempio illustra il motivo per cui questo risulta importante. Ricerche con caratteri jolly, tra cui ricerche con prefisso, sono ambigue per definizione perché hello input è una stringa parziale con le eventuali corrispondenze in un numero molto elevato di termini diversi (prendere in considerazione un input di "Panoramica *", con corrispondenze trovate in "demo", "tourettes", e " tourmaline"). Data la natura hello di questi risultati, non è possibile dedurre tooreasonably quali termini sono più utili rispetto ad altri. Per questo motivo, verranno ignorate le frequenze di termini durante l'assegnazione dei punteggi dei risultati nelle query di tipo con caratteri jolly, prefisso e regex. In una richiesta di ricerca più parti che contiene i termini parziali e completi, i risultati da un input parziale hello vengono incorporati con una costante punteggio distorsione tooavoid verso risultati imprevisti.

### <a name="score-tuning"></a>Ottimizzazione del punteggio

Esistono due modi i punteggi di pertinenza tootune in ricerca di Azure:

1. **I profili di punteggio** promuovere i documenti nell'elenco di hello classificata dei risultati in base a un set di regole. In questo esempio, è possibile prendere in considerazione documenti corrispondenti nel campo titolo hello più pertinente di documenti corrispondenti nel campo Descrizione hello. In aggiunta, se l'indice dispone di un campo prezzo per ogni albergo, è possibile promuovere i documenti con prezzo inferiore. Altre informazioni come troppo[aggiungere l'indice di ricerca tooa i profili di punteggio.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)
2. **Al termine boosting** (disponibile solo nella sintassi della query completa Lucene hello) fornisce un operatore boosting `^` che può essere applicato tooany parte dell'albero di query hello. In questo esempio, anziché dover cercare prefisso hello *air-condition*\*, una possibile cercare un termine esatto hello *air-condition* o prefisso hello, ma i documenti che corrispondono in hello esatta termine di un livello superiore tramite l'applicazione di query di termine toohello boost: *aria condizione ^ 2 | | AIR-Condition**. Altre informazioni sull'[aumento della priorità dei termini](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).


### <a name="scoring-in-a-distributed-index"></a>Assegnazione dei punteggi in un indice distribuito

Tutti gli indici in ricerca di Azure vengono automaticamente suddiviso in più partizioni, consentendo a noi tooquickly distribuire indice hello tra più nodi durante il ridimensionamento di un servizio di backup o scalare verso il basso. Quando viene eseguita una richiesta di ricerca, viene generata in ogni partizione in modo indipendente. Hello risultati di ogni partizione vengono quindi uniti e ordinati in base al punteggio (se è definito alcun altro ordine). È importante tooknow che hello punteggio funzione pesi termine frequenza delle query con la frequenza di documento inverso in tutti i documenti all'interno di partizioni hello, non tra tutte le partizioni.

Ciò significa che un punteggio di pertinenza *potrebbe* essere diverso per documenti identici se si trovano in partizioni diverse. Fortunatamente, tali differenze tendono toodisappear man mano che aumenta il numero di hello di documenti nell'indice hello a causa di distribuzione di termini anche toomore. Non è possibile tooassume su quale partizione verrà inserito un documento specifico. Tuttavia, se una chiave di documento non viene modificato, sarà sempre assegnato toohello stesso partizione.

In generale, il punteggio di documento non attributo migliore hello ordinare documenti se stabilità di ordine è importante. Ad esempio, ha due documento con un punteggio identico, non è garantito quale compare per primo nelle esecuzioni successive dell'hello stessa query. Punteggio di documento deve solo un'idea generale di pertinenza documento documenti tooother relativo nel set di risultati hello.

## <a name="conclusion"></a>Conclusioni

esito positivo Hello dei motori di ricerca internet ha generato le aspettative dei clienti per la ricerca full-text su dati privati. Per quasi tutti i tipi di esperienza di ricerca, è ora previsto hello motore toounderstand finalità, anche quando i termini di errori di ortografia o incompleta. Si possono anche prevedere delle corrispondenze basate su termini quasi equivalenti o sinonimi che non abbiamo mai specificato.

Dal punto di vista tecnico, ricerca full-text è estremamente complessa, che richiedono l'analisi linguistica sofisticata e tooprocessing un approccio sistematico in modo da filtrare, espanderla e la trasformazione query termini toodeliver un risultato pertinente. Dato complessità intrinseca hello, esistono molti fattori che possono influire sul risultato di hello di una query. Per questo motivo, investire hello ora toounderstand hello meccanismi che consentono di ricerca full-text offre vantaggi tangibili durante il tentativo di toowork tramite risultati imprevisti.  

In questo articolo sono stati illustrati la ricerca full-text nel contesto di hello di ricerca di Azure. Ci auguriamo che offre sufficiente background toorecognize le possibili cause e soluzioni per risolvere problemi comuni di query. 

## <a name="next-steps"></a>Passaggi successivi

+ Compilare l'indice degli esempi di hello, provare a query diverse e rivedere i risultati. Per istruzioni, vedere [compilare ed eseguire query di un indice nel portale di hello](search-get-started-portal.md#query-index).

+ Provare la sintassi di query aggiuntive di hello [ricerca documenti](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) sezione esempio o da [semplice sintassi di query](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) in Esplora ricerche nel portale di hello.

+ Revisione [i profili di punteggio](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) se si desidera tootune classificazione nell'applicazione di ricerca.

+ Informazioni su come tooapply [analizzatori lessicali specifiche della lingua](https://docs.microsoft.com/rest/api/searchservice/language-support).

+ [Configurare gli analizzatori personalizzati](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) per un'elaborazione minima o specializzati per settori specifici.

+ [Fare un confronto affiancato degli analizzatori standard e in lingua inglese](http://alice.unearth.ai/) in questo sito Web demo. 

## <a name="see-also"></a>Vedere anche

[Search Documents REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents) (API REST di Ricerca di documenti)

[Sintassi di query semplice](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

[Full Lucene query syntax](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) (Sintassi di query completa Lucene)

[Gestire i risultati della ricerca](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: ./media/search-lucene-query-architecture/architecture-diagram2.png
[2]: ./media/search-lucene-query-architecture/azSearch-queryparsing-should2.png
[3]: ./media/search-lucene-query-architecture/azSearch-queryparsing-must2.png
[4]: ./media/search-lucene-query-architecture/azSearch-queryparsing-spacious2.png
