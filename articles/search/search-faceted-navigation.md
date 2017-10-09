---
title: navigazione con facet di tooimplement aaaHow in ricerca di Azure | Documenti Microsoft
description: Aggiungere la navigazione con facet tooapplications che si integrano con ricerca di Azure, un servizio di ricerca cloud ospitato in Microsoft Azure.
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: cdf98fd4-63fd-4b50-b0b0-835cb08ad4d3
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 3/10/2017
ms.author: heidist
ms.openlocfilehash: c1e6bf9dc55d0044525db79e37d35a50ded5a736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-faceted-navigation-in-azure-search"></a>Come tooimplement navigazione con facet in ricerca di Azure
L'esplorazione in base a facet è un meccanismo di filtro che consente un'esplorazione drill-down mirata nelle applicazioni di ricerca. il termine Hello 'navigazione con facet' può essere poco note, ma probabilmente già utilizzato in precedenza. Come hello nel seguente esempio viene illustrato, navigazione con facet è teoricamente hello categorie usate toofilter risultati.

 ![Job Portal Demo di Ricerca di Azure][1]

Navigazione con facet è un toosearch di punto di ingresso alternativo. Offre un comodo tootyping alternativo espressioni complesse ricerca manualmente. I facet consentono di trovare ciò che si sta cercando con una percentuale di successo accertata. Gli sviluppatori di facet consentono di esporre i criteri di ricerca utili di hello per spostarsi tra l'insieme delle ricerche. Nelle applicazioni di vendita online, l'esplorazione in base a facet si basa spesso sulle marche, sui reparti (scarpe per bambini), sulla taglia, sul prezzo, sulla popolarità e sulle classificazioni. 

L'implementazione dell'esplorazione in base a facet si distingue tra le tecnologie di ricerca. Nella Ricerca di Azure, l'esplorazione in base a facet viene creata in fase di query, usando campi attribuiti precedenti nello schema.

-   Nelle query hello che l'applicazione viene compilata, è necessario che invii una query *i parametri di query facet* tooget hello disponibili filtro valori di facet per il documento di set di risultati.

-   tooactually trim hello set di risultati di documento, un'applicazione hello inoltre necessario applicare un `$filter` espressione.

Nell'ambiente di sviluppo di applicazioni, la scrittura di codice che crea query costituisce bulk hello del lavoro hello. Molti dei comportamenti dell'applicazione hello che ci si aspetta da una navigazione con facet vengono forniti dal servizio hello, incluso il supporto incorporato per la definizione di intervalli e il recupero di conteggi per i risultati di facet. servizio di Hello include inoltre impostazioni predefinite ragionevoli che consentono di evitare le strutture di navigazione difficile da gestire. 

## <a name="sample-code-and-demo"></a>Demo e codice di esempio
Questo articolo usa un portale di ricerca dei processi come esempio. esempio Hello viene implementato come un'applicazione MVC ASP.NET.

-   Visualizzare e testare hello lavoro demo online in [Demo portale processo di ricerca di Azure](http://azjobsdemo.azurewebsites.net/).

-   Scaricare codice hello da hello [repository di esempi di Azure su GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).

## <a name="get-started"></a>Attività iniziali
Se lo sviluppo di nuove toosearch, toothink modo migliore di hello di navigazione con facet è che consente di visualizzare il possibilità hello per la ricerca automatica diretto. Si tratta di un tipo di esperienza di ricerca drill-down, basata su filtri predefiniti usati per limitare rapidamente i risultati di ricerca tramite semplici azioni in un solo clic. 

### <a name="interaction-model"></a>Modello di interazione

Hello un'esperienza di ricerca per la navigazione con facet è possibile iniziare a comprendere, come una sequenza di query che si svolgano in azioni di risposta toouser iterativa.

punto di partenza Hello è una pagina dell'applicazione che fornisce funzioni di navigazione con facet, in genere nella periferia hello. L'esplorazione in base a facet è spesso una struttura ad albero, con caselle di controllo per ogni valore o testo selezionabile. 

1. Una query inviata tooAzure ricerca specifica struttura di navigazione con facet hello tramite uno o più parametri di query di facet. Ad esempio, in cui potrebbe includere query hello `facet=Rating`, ad esempio con un `:values` o `:sort` toofurther opzione perfezionare presentazione hello.
2. livello di presentazione Hello esegue il rendering di una pagina di ricerca che fornisce funzioni di navigazione con facet, tramite il facet hello specificato nella richiesta di hello.
3. Ha una struttura di navigazione con facet che include una valutazione, si fa clic su "4" tooindicate che devono essere visualizzati solo i prodotti con una classificazione 4 o versione successiva. 
4. In risposta, un'applicazione hello invia una query che include`$filter=Rating ge 4` 
5. Hello presentazione livello hello pagina aggiornamenti, che mostra un set di risultati ridotto, contenente solo gli elementi che soddisfano i criteri nuovi hello (in questo caso, i prodotti con classificazione 4 e successive).

Il facet è un parametro di query, da non confondere con l'input della query. Non viene mai usato come criterio di selezione in una query. Considerare invece facet parametri di query come input toohello struttura che viene restituita nella risposta hello. Per ogni parametro di query facet che è fornire, ricerca di Azure restituisce il numero di documenti presenti risultati parziali di hello per ogni valore del facet.

Hello preavviso `$filter` nel passaggio 4. filtro di Hello è un aspetto importante della navigazione con facet. Sebbene i facet e i filtri sono indipendenti in hello API, è necessario entrambi esperienza hello toodeliver desiderato. 

### <a name="app-design-pattern"></a>Schema progettuale di app

Nel codice dell'applicazione, il modello di hello è toouse facet parametri tooreturn hello navigazione con facet struttura delle query con risultati di facet, oltre a un'espressione $filter.  Hello filtro espressione handle hello click (evento) nel valore del facet hello. Si consideri hello `$filter` espressione come codice hello dietro la rimozione effettiva hello dei risultati della ricerca ha restituito il livello di presentazione toohello. Dato un facet di colori, fare clic su hello colore rosso viene implementata tramite un `$filter` espressione che seleziona solo gli elementi che hanno un colore di rosso. 

### <a name="query-basics"></a>Nozioni di base sulle query

In Ricerca di Azure una richiesta viene specificata tramite uno o più parametri di query (vedere [Eseguire ricerche nei documenti](http://msdn.microsoft.com/library/azure/dn798927.aspx) per una descrizione di ciascuno di essi). Nessuno dei parametri di query hello sono obbligatori, ma è necessario avere almeno un affinché toobe una query valida.

Precisione, compreso come hello toofilter possibilità out riscontri irrilevanti, è possibile ottenere tramite una o entrambe queste espressioni:

-   **ricerca =**  
    il valore di Hello di questo parametro costituisce l'espressione di ricerca hello. Potrebbe essere una singola parte di testo o un'espressione di ricerca complessa che include più termini e operatori. Un'espressione di ricerca viene utilizzata nel server di hello, per la ricerca full-text, l'esecuzione di query i campi ricercabili nell'indice hello per la corrispondenza di termini, restituendo i risultati in ordine di priorità. Se si imposta `search` toonull, esecuzione di query è hello intero indice (vale a dire `search=*`). In questo caso, gli altri elementi di hello di query, ad esempio un `$filter` o profilo di punteggio, è fattori principali che interessano i documenti vengono restituiti hello `($filter`) e in quale ordine (`scoringProfile` o `$orderby`).

-   **$filter=**  
    Un filtro è un meccanismo potente per la limitazione delle dimensioni di hello dei risultati della ricerca in base ai valori hello degli attributi di un documento specifico. Oggetto `$filter` viene valutata per prima, seguita da logica di facet che genera i valori disponibili hello e i conteggi corrispondenti per ogni valore

Espressioni di ricerca complesso ridurre le prestazioni di hello di query hello. Laddove possibile, utilizzare precisione tooincrease espressioni di filtro ben costruito e migliorare le prestazioni delle query.

toobetter comprendere come un filtro aggiunge maggiore precisione, confrontare un tooone di espressione di ricerca complessa che include un'espressione di filtro:

-   `GET /indexes/hotel/docs?search=lodging budget +Seattle –motel +parking`
-   `GET /indexes/hotel/docs?search=lodging&$filter=City eq ‘Seattle’ and Parking and Type ne ‘motel’`

Entrambe le query sono valide, ma hello in secondo luogo è superiore se si sta cercando non motel con parcheggio Seattle.
-   prima di query Hello si basa su tali parole specifiche non indicate nei campi stringa come nome, descrizione e qualsiasi altro campo contenente dati ricercabili o essere indicati.
-   query secondo Hello Cerca corrispondenze precise su dati strutturati ed è probabile che toobe molto più accurata.

Nelle applicazioni che includono l'esplorazione in base a facet, è necessario assicurarsi che ogni azione dell'utente su una struttura di esplorazione in base a facet sia accompagnata da una restrizione dei risultati della ricerca. toonarrow risultati, utilizzare un'espressione di filtro.

<a name="howtobuildit"></a>

## <a name="build-a-faceted-navigation-app"></a>Creare un'app di esplorazione in base a facet
Per implementare lo spostamento con facet con ricerca di Azure nel codice dell'applicazione che crea la richiesta di ricerca hello. navigazione con facet Hello si basa su elementi dello schema definito in precedenza.

Predefiniti nell'indice di ricerca è hello `Facetable [true|false]` indicizza attributo, impostare su tooenable campi selezionati o disabilitare l'uso in una struttura di navigazione con facet. Senza `"Facetable" = true`un campo non può essere usato nell'esplorazione in base a facet.

livello di presentazione Hello nel codice fornisce l'esperienza utente hello. È necessario elencare costituenti hello di navigazione con facet hello, ad esempio hello etichetta, i valori, le caselle di controllo e conteggio hello. Hello API REST di ricerca di Azure è indipendente dalla piattaforma, quindi utilizzare la lingua e la piattaforma desiderata. importante Hello è con stato dell'interfaccia utente aggiornato elementi dell'interfaccia utente tooinclude che supportano incrementale aggiornano ogni facet aggiuntivi selezionati. 

In fase di query, il codice dell'applicazione crea una richiesta che include `facet=[string]`, un parametro di richiesta che fornisce hello toofacet di campo da. Una query può avere più facet, ad esempio `&facet=color&facet=category&facet=rating`, ciascuno separato da un carattere e commerciale (&).

Il codice dell'applicazione è necessario creare anche un `$filter` hello toohandle espressione scegliere gli eventi di navigazione con facet. Oggetto `$filter` riduce i risultati della ricerca hello, utilizzando il valore di facet hello come criteri di filtro.

Ricerca di Azure restituisce i risultati della ricerca hello, in base a uno o più termini immessi dall'utente, insieme a struttura di navigazione con facet toohello di aggiornamenti. In Ricerca di Azure l'esplorazione in base a facet è una costruzione a livello singolo, con valori di facet, che calcola il numero di risultati trovati per ciascuno di essi.

In hello le sezioni seguenti, si accettano informazioni dettagliate su come toobuild ogni parte.

<a name="buildindex"></a>

## <a name="build-hello-index"></a>Compilare l'indice di hello
Facet è abilitato singolo campo per campo in indice hello, tramite l'attributo di indice: `"Facetable": true`.  
Tutti i tipi di campo che possono essere usati in esplorazione in base a facet sono `Facetable` per impostazione predefinita. Tali tipi di campi includono `Edm.String`, `Edm.DateTimeOffset`, e tutti i tipi di campi numerici di hello (in pratica, tutti i tipi di campo sono facetable tranne `Edm.GeographyPoint`, che non può essere usato nel riquadro di navigazione con facet). 

Quando si compila un indice, tooexplicitly facet di attivare una procedura consigliata per la navigazione con facet è disattivata per i campi che non devono mai essere utilizzati come facet.  In particolare, i campi di stringhe per i valori singleton, ad esempio un nome di prodotto o ID, devono essere impostati troppo`"Facetable": false` tooprevent loro accidentale e inefficaci utilizzano nel riquadro di navigazione con facet. Attivazione facet off in cui non è necessario mantenere ridotte le dimensioni di hello dell'indice hello e in genere migliora le prestazioni.

Di seguito è parte dello schema di hello per app di esempio hello processo portale Demo, tagliati delle dimensioni di hello tooreduce alcuni attributi:

```json
{
  ...
  "name": "nycjobs",
  "fields": [
    { “name”: "id",                 "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "job_id",             "type": "Edm.String",              "searchable": false, "filterable": false, ... "facetable": false, ... },
    { “name”: "agency",              "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "posting_type",        "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "num_of_positions",    "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "business_title",      "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "civil_service_title", "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "title_code_no",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "level",               "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_from",   "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_range_to",     "type": "Edm.Int32",              "searchable": false, "filterable": true, ...  "facetable": true, ...  },
    { “name”: "salary_frequency",    "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
    { “name”: "work_location",       "type": "Edm.String",             "searchable": true,  "filterable": true, ...  "facetable": true, ...  },
…
    { “name”: "geo_location",        "type": "Edm.GeographyPoint",     "searchable": false, "filterable": true, ...  "facetable": false, ... },
    { “name”: "tags",                "type": "Collection(Edm.String)", "searchable": true,  "filterable": true, ...  "facetable": true, ...  }
  ],
…
}
```

Come si può notare nello schema di esempio hello, `Facetable` è disattivata per i campi stringa non devono essere utilizzati come facet, ad esempio i valori di ID. Attivazione facet off in cui non è necessario mantenere ridotte le dimensioni di hello dell'indice hello e in genere migliora le prestazioni.

> [!TIP]
> Come procedura consigliata, includono il set completo di hello di attributi dell'indice per ogni campo. Anche se `Facetable` è per impostazione predefinita per quasi tutti i campi, impostazione intenzionalmente ogni attributo consentono di valutare le implicazioni di hello di ogni decisione di schema. 

<a name="checkdata"></a>

## <a name="check-hello-data"></a>Controllare i dati di hello
qualità Hello dei dati ha un effetto diretto sulla se struttura di navigazione con facet hello viene materializzato come previsto. Influisce anche sulla facilità hello di creazione di set di risultati di filtri tooreduce hello.

Se si desidera toofacet marchio o prezzo, ogni documento deve contenere i valori per *NomeMarchio* e *ProductPrice* che sono validi, coerenti e produttivi come opzione di filtro.

Ecco alcuni promemoria di quali tooscrub per:

* Per ogni campo che si desidera toofacet da, è necessario stabilire se contiene valori che sono adatti come filtri di ricerca attiva. i valori Hello devono essere sufficientemente distintive breve e descrittivo toooffer una scelta tra le opzioni di concorrenza non crittografata.
* Errori di ortografia o valori quasi corrispondenti. Se si facet sul colore e i valori dei campi includono arancione e Ornage (un errore di ortografia), un facet in base a campo di colori hello preleverebbe entrambi.
* Il testo con maiuscole e minuscole e può inoltre provocare danni all'esplorazione in base a facet con arancione e Arancione visualizzati come due valori diversi. 
* Versioni singole e plurale di hello stesso valore può comportare un facet separato per ogni.

Come è facile immaginare, molta attenzione nella preparazione dei dati hello è un aspetto essenziale di navigazione con facet effettivo.

<a name="presentationlayer"></a>

## <a name="build-hello-ui"></a>Compilare hello dell'interfaccia utente
Utilizzo dal livello di presentazione hello possibile scoprire i requisiti che potrebbero non riuscire in caso contrario e comprendere quali funzionalità sono essenziale toohello Guida esperienza di ricerca.

In termini di navigazione con facet, pagina web o l'applicazione visualizza la struttura di navigazione con facet hello rileva l'input dell'utente nella pagina hello e inserisce gli elementi modificato hello. 

Per le applicazioni web, in genere utilizzato AJAX nel livello di presentazione hello perché consente modifiche incrementali toorefresh. È anche possibile usare ASP.NET MVC o qualsiasi altra piattaforma di visualizzazione in grado di connettersi tramite HTTP tooan servizio di ricerca di Azure. applicazione di esempio Hello a cui fa riferimento in questo articolo: hello **Demo portale processo di ricerca di Azure** – avviene toobe un'applicazione MVC ASP.NET.

Nell'esempio hello, navigazione con facet viene compilata in hello pagina dei risultati di ricerca. Hello seguente esempio, tratto da hello `index.cshtml` file dell'applicazione di esempio hello, Mostra hello statica struttura HTML per visualizzare la navigazione con facet su ricerca hello pagina di risultati. elenco Hello di facet viene compilato o ricompilato in modo dinamico quando si invia un termine di ricerca, selezionare o deseleziona un facet.

```html
<div class="widget sidebar-widget jobs-filter-widget">
  <h5 class="widget-title">Filter Results</h5>
    <p id="filterReset"></p>
    <div class="widget-content">

      <h6 id="businessTitleFacetTitle">Business Title</h6>
      <ul class="filter-list" id="business_title_facets">
      </ul>

      <h6>Location</h6>
      <ul class="filter-list" id="posting_type_facets">
      </ul>

      <h6>Posting Type</h6>
      <ul class="filter-list" id="posting_type_facets"></ul>

      <h6>Minimum Salary</h6>
      <ul class="filter-list" id="salary_range_facets">
      </ul>

  </div>
</div>
```

Hello seguente frammento di codice hello `index.cshtml` pagina compila dinamicamente hello HTML toodisplay hello prima del facet, il titolo di Business. Funzioni simili compilare dinamicamente hello HTML per hello altri facet. Ogni facet ha un'etichetta e un conteggio, che visualizza il numero di hello di elementi trovati per il risultato del facet.

```js
function UpdateBusinessTitleFacets(data) {
  var facetResultsHTML = '';
  for (var i = 0; i < data.length; i++) {
    facetResultsHTML += '<li><a href="javascript:void(0)" onclick="ChooseBusinessTitleFacet(\'' + data[i].Value + '\');">' + data[i].Value + ' (' + data[i].Count + ')</span></a></li>';
  }

  $("#business_title_facets").html(facetResultsHTML);
}
```

> [!TIP]
> Quando si progetta una pagina di risultati di ricerca hello, tenere presente tooadd un meccanismo per la cancellazione di facet. Se si aggiungono le caselle di controllo, è possibile visualizzare facilmente come i filtri tooclear hello. Per altri layout potrebbe essere necessario un modello di navigazione o un altro approccio creativo. Ad esempio, nell'applicazione di esempio processo ricerca portale hello, è possibile fare clic su hello `[X]` dopo un facet di hello tooclear facet selezionato.

<a name="buildquery"></a>

## <a name="build-hello-query"></a>Compilare la query hello
il codice Hello scritto per la compilazione di query è necessario specificare tutte le parti di una query valida, incluse le espressioni di ricerca, facet, filtri, il punteggio profili – qualsiasi elemento utilizzato tooformulate una richiesta. In questa sezione vengono analizzate in facet rientrano in una query e come vengono utilizzati filtri con facet toodeliver ridotto set di risultati.

Si noti che i facet sono parte integrante di questa applicazione di esempio. esperienza di ricerca Hello in hello processo portale Demo viene progettata attorno a filtri e la navigazione con facet. la selezione host principali Hello di navigazione con facet nella pagina hello illustra l'importanza. 

Un esempio è spesso toobegin un buon punto. Hello seguente esempio, tratto da hello `JobsSearch.cs` file, le compilazioni in base una richiesta che crea la navigazione facet qualifica, posizione, tipo di registrazione e stipendio minimo. 

```cs
SearchParameters sp = new SearchParameters()
{
  ...
  // Add facets
  Facets = new List<String>() { "business_title", "posting_type", "level", "salary_range_from,interval:50000" },
};
```

Un parametro di query del facet è impostato il campo tooa e in base al tipo di dati hello, può essere parametrizzato ulteriormente dall'elenco delimitato da virgole che include `count:<integer>`, `sort:<>`, `interval:<integer>`, e `values:<list>`. Durante l'impostazione di intervalli è supportato un elenco di valori per i dati numerici. Per informazioni dettagliate, vedere [Eseguire ricerche nei documenti (API di Ricerca di Azure)](http://msdn.microsoft.com/library/azure/dn798927.aspx) .

Insieme a facet, richiesta hello formulata dall'applicazione deve essere basati anche filtri toonarrow verso il basso il set di hello di documenti in base alla selezione di un valore di facet. Per un archivio di biciclette, navigazione con facet include indicazioni tooquestions come *quali colori, i produttori e i tipi di biciclette sono disponibili?*. Il filtro risponde a domande come *Quali biciclette sono mountain bike rosse in questa fascia di prezzo?*. Quando si fa clic su "Red" tooindicate che devono essere visualizzati solo i prodotti di colore rossi, applicazione di hello query successiva hello invia include `$filter=Color eq ‘Red’`.

Hello seguente frammento di codice hello `JobsSearch.cs` pagina aggiunge hello selezionato qualifica toohello filtro se si seleziona un valore dal facet qualifica hello.

```cs
if (businessTitleFacet != "")
  filter = "business_title eq '" + businessTitleFacet + "'";
```

<a name="tips"></a> 

## <a name="tips-and-best-practices"></a>Suggerimenti e procedure consigliate

### <a name="indexing-tips"></a>Suggerimenti per l'indicizzazione
**Migliorare l'efficienza di un indice se non si usa una casella di ricerca**

Se l'applicazione utilizza esclusivamente di navigazione con facet (ovvero, nessuna casella di ricerca), è possibile contrassegnare il campo hello come `searchable=false`, `facetable=true` tooproduce un indice più compatto. Inoltre, l'indicizzazione viene eseguita solo su valori di facet intere, con nessuna interruzione di word o indicizzazione hello parti dei componenti di un valore più parole.

**Specificare quali campi possono essere usati come facet**

Tenere presente che hello dello schema di indice hello determina quali campi sono disponibili toouse come facet. Se che un campo è facetable, query hello specifica quali toofacet campi da. mediante il quale si è i facet di campo di Hello fornisce i valori hello vengono visualizzate sotto l'etichetta hello. 

i valori Hello visualizzati in ogni etichetta vengono recuperati dall'indice di hello. Ad esempio, se hello campo facet è *colore*, i valori hello disponibili per altre opzioni di filtro sono hello i valori del campo - rosso, bianco e così via.

Per valori numerici e data/ora solo, è possibile impostare in modo esplicito i valori nel campo facet hello (ad esempio, `facet=Rating,values:1|2|3|4|5`). Un elenco di valori è consentito per questi tipi toosimplify hello separazione campi dei risultati di facet in intervalli contigui (entrambi gli intervalli in base a valori numerici o periodi di tempo). 

**Per impostazione predefinita, è possibile avere un solo livello di esplorazione in base a facet** 

Come accennato, non esiste alcun supporto diretto per la nidificazione facet in una gerarchia. Per impostazione predefinita, l'esplorazione in base a facet in Ricerca di Azure supporta solo un livello di filtri. Tuttavia, esistono soluzioni alternative. È possibile codificare una struttura gerarchica facet in un `Collection(Edm.String)` con un punto di ingresso per singola gerarchia. Implementazione di questa soluzione esula dall'ambito di hello di questo articolo. 

### <a name="querying-tips"></a>Suggerimenti per le query
**Convalidare i campi**

Se si compila l'elenco di hello di facet in modo dinamico in base all'input utente non attendibile, convalidare che i nomi di hello di campi con facet hello sono validi. O, creazione di URL, utilizzando nomi hello di escape `Uri.EscapeDataString()` .NET o hello equivalente nella piattaforma a scelta.

### <a name="filtering-tips"></a>Suggerimenti per i filtri
**Aumentare la precisione della ricerca con i filtri**

Usare i filtri. Se si utilizzano solo espressioni di ricerca da solo, lo stemming potrebbe causare un toobe documento restituito che non dispone di valore del facet preciso hello in uno dei relativi campi.

**Aumentare le prestazioni della ricerca con i filtri**

I filtri restringono set hello di documenti di candidati per la ricerca ed escluderli dal calcolo della pertinenza. Se si dispone di un ampio set di documenti, l'uso di un drill-down di facet selettivo spesso consente un miglioramento significativo delle prestazioni.
  
**Filtrare solo i campi con facet hello**

In con facet drill-down, si vorrà probabilmente tooonly includono documenti che contengono il valore di facet hello in un campo specifico (con facet), non in un punto qualsiasi tra tutti i campi ricercabili. Aggiunta di un filtro ribadiscono il campo di destinazione hello indirizzando hello servizio toosearch solo nel campo con facet di hello per un valore corrispondente.

**Ridurre i risultati di facet con altri filtri**

Risultati di facet sono documenti trovati nei risultati di ricerca hello che corrispondono a un termine di facet. Nel seguente esempio, nei risultati della ricerca per hello *il cloud computing*, 254 elementi dispongono inoltre di *interno specifica* come tipo di contenuto. Gli elementi non si escludono necessariamente a vicenda. Se un elemento soddisfa i criteri di hello di entrambi i filtri, è espresso in ognuno di essi. È possibile quando la duplicazione facet su `Collection(Edm.String)` campi, che sono spesso utilizzati tooimplement documento tag.

        Search term: "cloud computing"
        Content type
           Internal specification (254)
           Video (10) 

In generale, se risulta che i risultati di facet in modo coerente le dimensioni sono eccessive, è consigliabile aggiungere più utenti vengono filtrati toogive ulteriori opzioni per limitare la ricerca hello.

### <a name="tips-about-result-count"></a>Suggerimenti sul conteggio dei risultati

**Limitazione del numero di elementi nel riquadro di navigazione facet hello hello**

Per ogni campo con facet nell'albero di navigazione hello, è previsto un limite predefinito di 10 valori. Questa impostazione predefinita è utile per le strutture di navigazione perché mantiene i valori hello dimensioni gestibili tooa dell'elenco. È possibile eseguire l'override di predefinito hello assegnando un valore toocount.

* `&facet=city,count:5`Specifica che solo hello primi cinque città trovata nell'espressione top hello classificati i risultati vengono restituite come risultato un facet. Si consideri una query di esempio con un termine di ricerca di "aeroporto" e 32 corrispondenze. Se la query hello specifica `&facet=city,count:5`, solo i primi cinque città univoche in hello con la maggior parte dei documenti nei risultati della ricerca hello sono inclusi in hello hello risultati facet.

Si noti hello distinzione tra i risultati di facet e i risultati della ricerca. Risultati della ricerca sono tutti i documenti che corrispondono a query hello hello. Risultati di facet sono hello corrispondente per ogni valore del facet. Nell'esempio hello, i risultati della ricerca includono i nomi di città che non sono presenti nell'elenco di classificazione facet hello (5 in questo esempio). I risultati che vengono filtrati tramite l'esplorazione in base a facet diventano visibili quando si cancellano i facet o si scelgono altri facet oltre a città. 

> [!NOTE]
> La discussione relativa a `count` quando ne esiste più di un tipo potrebbe portare a confusione. Hello nella tabella seguente offre un breve riepilogo dell'utilizzo di termini hello nell'API di ricerca di Azure, il codice di esempio e documentazione. 

* `@colorFacet.count`<br/>
  Nel codice di presentazione, dovrebbe essere un parametro del conteggio facet hello, toodisplay utilizzati hello numero dei risultati di facet. Nei risultati di facet, conteggio indica il numero di hello di documenti che corrispondono a termine facet hello o intervalli.
* `&facet=City,count:12`<br/>
  In una query con facet, è possibile impostare il valore di tooa count.  valore predefinito di Hello è 10, ma è possibile impostare una posizione superiore o inferiore. Impostazione `count:12` Ottiene hello prime 12 corrispondenze nei risultati di facet per il numero di documento.
* "`@odata.count`"<br/>
  In risposta alle query hello, questo valore indica il numero di hello di elementi corrispondenti nei risultati della ricerca hello. In Media, è maggiore di somma hello di tutti i facet risultati combinati, a causa di toohello presenza di elementi corrispondenti al termine di ricerca hello, ma senza corrispondenze di valore del facet.

**Ottenere i conteggi nei risultati di facet**

Quando si aggiunge una query con facet tooa di filtro, si consiglia di istruzione di facet hello tooretain (ad esempio, `facet=Rating&$filter=Rating ge 4`). Tecnicamente, i facet = classificazione non è necessaria, ma mantenendo restituisce conteggi hello dei valori di facet per le classificazioni, 4 e versioni successive. Ad esempio, se si sceglie "4" e hello query include un filtro per maggiore o uguale troppo "4", i conteggi vengono restituiti per ogni classificazione è 4 e versioni successive.  

**Verificare di ottenere conteggi di facet accurati**

In determinate circostanze, è possibile che i conteggi di facet non corrispondono a set di risultati hello (vedere [navigazione con facet in ricerca di Azure (post di forum)](https://social.msdn.microsoft.com/Forums/azure/06461173-ea26-4e6a-9545-fbbd7ee61c8f/faceting-on-azure-search?forum=azuresearch)).

I conteggi di facet possono essere corrette a causa di architettura di partizionamento orizzontale toohello. Ogni indice di ricerca include più partizioni, e ogni partizione segnala facet primi N hello dal numero di documenti, è quindi combinato in un singolo risultato. Se alcune partizioni hanno molti valori corrispondenti, mentre altri hanno meno, è possibile che alcuni valori di facet sono mancanti o in conteggiati in risultati hello.

Sebbene questo comportamento potrebbe cambiare in qualsiasi momento, se si verifica oggi questo comportamento, è possibile aggirare il problema artificialmente eccessi nella misurazione conteggio hello:<number> tooa grande numero tooenforce completo reporting da ogni partizione. Se hello valore del conteggio: è maggiore o uguale toohello numero di valori univoci nel campo hello, si sono certi risultati accurati. Tuttavia, quando i conteggi di documenti sono elevati, si verifica una riduzione delle prestazioni ed è quindi consigliabile usare questa opzione con cautela.

### <a name="user-interface-tips"></a>Suggerimenti per l'interfaccia utente
**Aggiungere etichette per ogni campo nella navigazione facet**

Le etichette vengono in genere definite nel modulo o hello HTML (`index.cshtml` nell'applicazione di esempio hello). Non esiste alcuna API in Ricerca di Azure per le etichette di navigazione facet o qualsiasi altro metadato.

<a name="rangefacets"></a>

## <a name="filter-based-on-a-range"></a>Filtro basato su un intervallo
L'esplorazione in base a facet su intervalli di valori è un requisito comune delle applicazioni di ricerca. Gli intervalli sono supportati per i dati numerici e i valori DateTime. Per ulteriori informazioni su ogni approccio in [Eseguire ricerche nei documenti (API di Ricerca di Azure)](http://msdn.microsoft.com/library/azure/dn798927.aspx).

Ricerca di Azure semplifica la creazione degli intervalli fornendo due approcci per l'elaborazione di un intervallo. Per entrambi gli approcci, ricerca di Azure crea hello gli intervalli appropriati, dati gli input hello che ci hai fornito. Ad esempio, se si specificano valori di intervallo di 10|20|30, vengono creati automaticamente gli intervalli 0-10, 10-20, 20-30. L'applicazione può facoltativamente rimuovere qualsiasi intervallo vuoto. 

**Approccio 1: Utilizzare il parametro di intervallo hello**  
facet di prezzo tooset in incrementi di 10, è necessario specificare:`&facet=price,interval:10`

**Approccio 2: utilizzare un elenco di valori**  
Per dati numerici, è possibile usare un elenco di valori.  Intervallo di facet hello per prendere in considerazione un `listPrice` campo, visualizzato come segue:

  ![Elenco di valori di esempio][5]

toospecify un intervallo del facet come hello in hello che precede la cattura di schermata, utilizzare un elenco di valori:

    facet=listPrice,values:10|25|100|500|1000|2500

Ogni intervallo viene compilato utilizzando 0 come punto di partenza, un valore dall'elenco di hello come un endpoint e quindi vengono tagliate hello precedente toocreate discreti intervalli. Ricerca di Azure esegue questa operazione nell'ambito dell'esplorazione in base facet. Non si dispone di codice toowrite per la struttura di ogni intervallo.

### <a name="build-a-filter-for-a-range"></a>Creare un filtro per un intervallo
documenti toofilter in base a un intervallo selezionato, è possibile utilizzare hello `"ge"` e `"lt"` operatori in un'espressione di due parti che definisce l'endpoint di hello dell'intervallo di hello di filtro. Ad esempio, se si sceglie hello intervallo 10 a 25 per un `listPrice` campo filtro hello sarebbe `$filter=listPrice ge 10 and listPrice lt 25`. Nell'esempio di codice hello, espressione di filtro hello utilizza **priceFrom** e **priceTo** endpoint hello tooset di parametri. 

  ![Query per un intervallo di valori][6]

<a name="geofacets"></a> 

## <a name="filter-based-on-distance"></a>Filtro basato sulla distanza
Toosee comuni di filtri che consentono scegliere un archivio, ristorante o destinazione in base alla relativa posizione corrente di prossimità tooyour. Questo tipo di filtro potrebbe somigliare all'esplorazione in base a facet, ma è semplicemente un filtro. Viene menzionato per coloro che cercano in particolare consigli di implementazione per tale problema particolare di progettazione.

Sono disponibili due funzioni geospaziali in Ricerca di Azure, **geo.distance** e **geo.intersects**.

* Hello **Distance** funzione restituisce la distanza hello in chilometri tra due punti. Un punto è un campo e altro è una costante passata come parte del filtro hello. 
* Hello **geo.intersects** funzione restituisce true se un punto specificato si trova all'interno di un dato poligono. punto Hello è un campo e hello poligono viene specificato come un elenco di coordinate passato come parte del filtro hello costante.

È possibile trovare alcuni esempi di filtri in [Sintassi dell'espressione di OData (Ricerca di Azure)](http://msdn.microsoft.com/library/azure/dn798921.aspx).

<a name="tryitout"></a>

## <a name="try-hello-demo"></a>Provare la demo hello
Hello Demo portale processo di ricerca di Azure è disponibili esempi di hello a cui fa riferimento in questo articolo.

-   Visualizzare e testare hello lavoro demo online in [Demo portale processo di ricerca di Azure](http://azjobsdemo.azurewebsites.net/).

-   Scaricare codice hello da hello [repository di esempi di Azure su GitHub](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs).

Mentre si lavora con i risultati della ricerca, guardare URL hello per le modifiche nella costruzione delle query. Questa applicazione si verifica tooappend facet toohello URI per la selezione di ciascuno di essi.

1. funzionalità di mapping hello toouse di app demo hello e ottenere una chiave Bing Maps da hello [Bing Maps Dev Center](https://www.bingmapsportal.com/). Incollare il codice su una chiave esistente hello hello `index.cshtml` pagina. Hello `BingApiKey` impostazione hello `Web.config` file non viene utilizzato. 

2. Eseguire un'applicazione hello. Presentazione di hello facoltativo o chiudere la finestra di dialogo hello.
   
3. Immettere un termine di ricerca, ad esempio "analista" e fare clic sull'icona di ricerca hello. query di Hello viene eseguita rapidamente.
   
   Una struttura di navigazione con facet viene restituita anche con i risultati della ricerca hello. Nella pagina di risultati di ricerca hello, struttura di navigazione con facet hello include i conteggi per ogni risultato del facet. Non sono stati selezionati facet e quindi vengono restituiti tutti i risultati corrispondenti.
   
   ![Risultati della ricerca prima della selezione di facet][11]

4. Fare clic su un valore per Business Title, Location o Minimum Salary. Facet sono null nella ricerca iniziale hello, ma come assumono i valori, i risultati della ricerca hello vengono rimossi elementi che non corrispondono.
   
   ![Risultati della ricerca dopo la selezione di facet][12]

5. query con facet di tooclear hello in modo che è possibile provare a comportamenti di query diverse, fare clic su hello `[X]` dopo hello selezionato facet hello tooclear di facet.
   
<a name="nextstep"></a>

## <a name="learn-more"></a>Altre informazioni
Guardare [Azure Search Deep Dive](http://channel9.msdn.com/Events/TechEd/Europe/2014/DBI-B410) (Approfondimenti su Ricerca di Azure). 45:25, vi è una dimostrazione su come tooimplement facet.

Per ulteriori informazioni dettagliate sui principi di progettazione per la navigazione con facet, è consigliabile hello seguenti collegamenti:

* [Progettazione per la ricerca con esplorazione in base a facet](http://www.uie.com/articles/faceted_search/)
* [Modelli di progettazione: esplorazione in base a facet](http://alistapart.com/article/design-patterns-faceted-navigation)


<!--Anchors-->
[How toobuild it]: #howtobuildit
[Build hello presentation layer]: #presentationlayer
[Build hello index]: #buildindex
[Check for data quality]: #checkdata
[Build hello query]: #buildquery
[Tips on how toocontrol faceted navigation]: #tips
[Faceted navigation based on range values]: #rangefacets
[Faceted navigation based on GeoPoints]: #geofacets
[Try it out]: #tryitout

<!--Image references-->
[1]: ./media/search-faceted-navigation/azure-search-faceting-example.PNG
[2]: ./media/search-faceted-navigation/Facet-2-CSHTML.PNG
[3]: ./media/search-faceted-navigation/Facet-3-schema.PNG
[4]: ./media/search-faceted-navigation/Facet-4-SearchMethod.PNG
[5]: ./media/search-faceted-navigation/Facet-5-Prices.PNG
[6]: ./media/search-faceted-navigation/Facet-6-buildfilter.PNG
[7]: ./media/search-faceted-navigation/Facet-7-appstart.png
[8]: ./media/search-faceted-navigation/Facet-8-appbike.png
[9]: ./media/search-faceted-navigation/Facet-9-appbikefaceted.png
[10]: ./media/search-faceted-navigation/Facet-10-appTitle.png
[11]: ./media/search-faceted-navigation/faceted-search-before-facets.png
[12]: ./media/search-faceted-navigation/faceted-search-after-facets.png

<!--Link references-->
[Designing for Faceted Search]: http://www.uie.com/articles/faceted_search/
[Design Patterns: Faceted Navigation]: http://alistapart.com/article/design-patterns-faceted-navigation
[Create your first application]: search-create-first-solution.md
[OData expression syntax (Azure Search)]: http://msdn.microsoft.com/library/azure/dn798921.aspx
[Azure Search Adventure Works Demo]: https://azuresearchadventureworksdemo.codeplex.com/
[http://www.odata.org/documentation/odata-version-2-0/overview/]: http://www.odata.org/documentation/odata-version-2-0/overview/ 
[Faceting on Azure Search forum post]: ../faceting-on-azure-search.md?forum=azuresearch
[Search Documents (Azure Search API)]: http://msdn.microsoft.com/library/azure/dn798927.aspx

