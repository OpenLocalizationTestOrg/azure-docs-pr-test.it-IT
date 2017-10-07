---
title: esempi di query aaaLucene per ricerca di Azure | Documenti Microsoft
description: "Sintassi di query Lucene per ricerca fuzzy, ricerca per prossimità, l'aumento della priorità dei termini, ricerca con espressioni regolari e ricerca con caratteri jolly."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: Lucene query analyzer syntax
ms.assetid: 147f360d-a5ce-4d7b-a909-c8b65bfb748c
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: liamca
ms.openlocfilehash: d859cf697ef9485a49e9e0591b68e812ffa55f1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="lucene-query-syntax-examples-for-building-queries-in-azure-search"></a>Esempi di sintassi di query Lucene per la creazione di query in Ricerca di Azure
Quando si creano query di ricerca di Azure, è possibile utilizzare l'impostazione predefinita hello [semplice sintassi di query](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) o un'alternativa hello [Lucene Parser di Query in ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search). Hello Lucene Parser di Query supporta i costrutti delle query più complessi, ad esempio le query con ambito di campo, ricerca fuzzy, ricerca per prossimità, termine boosting e ricerca di espressione regolare.

In questo articolo, è possibile eseguire operazioni di query disponibili esempi quando si utilizza la sintassi completa di hello.

## <a name="viewing-hello-examples-in-jsfiddle"></a>La visualizzazione degli esempi di hello in JSFiddle

Tutti gli esempi di hello in questo articolo sono query eseguibile in esecuzione su un indice di ricerca di pre-caricato nella [JSFiddle](https://jsfiddle.net), un editor di codice in linea per il testing di script e HTML. 

toorun, fare clic su hello query esempio URL tooopen JSFiddle in una finestra distinta del browser.

> [!NOTE]
> Negli esempi seguenti Hello sfruttano un indice di ricerca composta da processi disponibili in base a un set di dati forniti da hello [città di New York parte](https://nycopendata.socrata.com/) initiative. Questi dati non devono essere considerati attuali o completi. indice di Hello è definito in un sandbox di servizio fornito da Microsoft. Non è necessaria una sottoscrizione di Azure o tootry di ricerca di Azure queste query.
>


## <a name="how-tooinvoke-full-lucene-parsing"></a>Come tooinvoke completo Lucene analisi

Tutti gli esempi di hello in questo articolo specificare hello **queryType = full** parametro, che indica la sintassi completa, hello gestita dal Parser di Query Lucene hello di ricerca. 

**Esempio 1** - hello rapida tooopen frammento di query in un browser nuova pagina che segue carica JSFiddle e viene eseguito hello query:

* [&queryType=full&search=*](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*)

In nuova finestra del browser di hello, hello JavaScript origine e output HTML sono presentate side-by-side. script Hello fa riferimento a una query completa (non solo hello frammento di codice, come illustrato nel collegamento hello). query completa Hello viene visualizzato negli URL hello per ogni esempio. 

Questa query restituisce documenti dall'indice delle offerte di lavoro della città di New York, ovvero nycjobs caricato in un servizio sandbox. Per ragioni di brevità, query hello specifica vengono restituiti solo i titoli di business. la query sottostante completa di Hello è come segue:

    http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26searchFields=business_title%26$select=business_title%26queryType=full%26search=*

Hello **searchFields** parametro limita campo titolo di hello ricerca toojust hello business. Hello **queryType** è troppo**completo**, che indica hello toouse di ricerca di Azure Lucene Parser di Query per questa query.

> [!NOTE]
> Per informazioni di base sull'elaborazione di query, vedere [Funzionamento della ricerca full-text in Ricerca di Azure](search-lucene-query-architecture.md). Per altre informazioni sui parametri di ricerca, vedere [Search Documents (Azure Search Service REST API)](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) (Documenti di ricerca: API REST del servizio Ricerca di Azure).
>

### <a name="fielded-query-operation"></a>Operazione di query con campo
È possibile modificare gli esempi di hello in questo articolo, specificando un **fieldname:searchterm** toodefine costruzione un'operazione di query già distribuito sul campo, in cui campo hello è una singola parola e hello termine di ricerca è anche una singola parola o frase, facoltativamente con gli operatori booleani. Alcuni esempi seguenti hello:

* business_title:(senior NOT junior)
* state:("New York" AND "New Jersey")

Essere tooput che più stringhe racchiuse tra virgolette se si desidera che entrambe le stringhe di toobe valutata come una singola entità, come in questo caso la ricerca di due distinte città nel campo percorso hello. Assicurarsi, inoltre, viene convertita in maiuscolo con NOT come operatore hello e and.

specificato nel campo Hello **fieldname:searchterm** deve essere un campo ricercabile. Per informazioni dettagliate sull'uso di attributi dell'indice nelle definizioni campo, vedere [Creare l'indice (API REST del servizio Ricerca di Azure)](https://docs.microsoft.com/rest/api/searchservice/create-index) .

**Esempio 2** -frammento di query seguente hello rapida questa query cerca i titoli di business con hello termini senior in essi contenuti, ma non junior:

* [&amp;queryType=full&amp;search= business_title:senior NOT junior](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:senior+NOT+junior)

## <a name="fuzzy-search-example"></a>Esempio di ricerca fuzzy
Una ricerca fuzzy trova le corrispondenze in termini che hanno una costruzione simile. Secondo la [documentazione di Lucene](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html), le ricerche fuzzy si basano sulla [distanza di Damerau-Levenshtein](https://en.wikipedia.org/wiki/Damerau%e2%80%93Levenshtein_distance).

toodo una ricerca fuzzy, accodare tilde hello "~" simbolo alla fine di hello di una singola parola con un parametro facoltativo, un valore compreso tra 0 e 2, che specifica la distanza di modifica hello. Ad esempio, "blue~" or "blue~1" restituirà blue, blues e glue.

**Esempio 3** -frammento di query seguente hello pulsante destro del mouse. Questa query cerca i processi con associate termine hello (in cui si è digitato):

* [&amp;queryType=full&amp;search= business_title:asosiate~](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:asosiate~)

> [!Note]
> Le query fuzzy non vengono [analizzate](https://docs.microsoft.com/azure/search/search-lucene-query-architecture#stage-2-lexical-analysis), il che può sorprendere se si prevede lo stemming o la lemmatizzazione. L'analisi lessicale viene eseguita solo su termini completi, la query di un termine o di una locuzione. Tipi di query con termini incompleti (query prefisso, la query con caratteri jolly, regex query, query fuzzy) vengono aggiunti direttamente toohello albero della query, ignorando fase di analisi hello. Hello solo trasformazione eseguita in base alle esigenze della query incompleta è minuscola.
>

## <a name="proximity-search-example"></a>Esempio di ricerca per prossimità
Ricerche per prossimità sono toofind utilizzati i termini vicini in un documento. Inserire una tilde "~" simbolo alla fine di hello di una frase seguita dal numero di hello di parole che compongono il limite di prossimità hello. Ad esempio, "aeroporto hotel" ~ 5 troveranno hotel termini hello e aeroporto entro 5 parole in un documento.

**Esempio 4** -query hello pulsante destro del mouse. Ricerca di processi con il termine hello "senior analista" in cui è separato da non più di una parola:

* [&amp;queryType=full&amp;search=business_title:"senior analyst"~1](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~1)

**Esempio 5** -provare nuovamente la rimozione di parole hello tra termini hello "senior analista".

* [&amp;queryType=full&amp;search=business_title:"senior analyst"~0](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:%22senior%20analyst%22~0)

## <a name="term-boosting-examples"></a>Esempi di aumento della priorità dei termini
Termine boosting fa riferimento un documento superiore se contiene hello con Boosting termine toodocuments relativo che non contengono il termine hello tooranking. Questo comportamento è diverso dall'assegnazione di punteggi ai profili, perché questo metodo assegna priorità ad alcuni campi, invece che a termini specifici. Hello esempio seguente consente di illustrare le differenze di hello.

Si consideri un profilo di punteggio che incrementa corrisponde a un determinato campo, ad esempio **genre** nell'esempio di musicstoreindex hello. Termine boosting può essere utilizzato toofurther boost determinate condizioni di ricerca maggiore rispetto ad altri. Ad esempio, "rock ^ 2 electronic" si migliorerà documenti che contengono i termini di ricerca hello in hello **genre** campo superiore altri campi di ricerca nell'indice hello. Inoltre, i documenti che contengono il termine di ricerca hello "rock" verranno classificati superiore rispetto a hello altro termine di ricerca "electronic" in seguito a valore di incremento termine hello (2).

tooboost un termine, l'utilizzo del punto di inserimento hello, "^", simbolo con un fattore di aumento di priorità (number) alla fine di hello del termine hello si esegue la ricerca. Hello fattore di aumento di priorità maggiore hello, hello termine hello più rilevante sarà relativo tooother i termini di ricerca. Per impostazione predefinita, il fattore di aumento di priorità hello è 1. Anche se il fattore di aumento di priorità hello deve essere positivo, può essere minore di 1 (ad esempio, 0,2).

**Esempio 6** -query hello pulsante destro del mouse. Ricerca di processi con il termine hello "analista di computer" in cui si vedere non sono presenti risultati con computer parole e analista ancora nella parte superiore dei risultati di hello hello sono processi analista.

* [&amp;queryType=full&amp;search=business_title:computer analyst](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

**Esempio 7** -tentare nuovamente, questo tempo boosting risultati con computer termine hello su analista termine hello, se non sono presenti entrambe le parole.

* [&queryType=full&search=business_title:computer^2 analyst](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26$select=business_title%26queryType=full%26search=business_title:computer%5e2%20analyst)

## <a name="regular-expression-example"></a>Esempio di espressione regolare
Una ricerca di espressioni regolari trova una corrispondenza in base al contenuto hello tra le barre "/", come documentato in hello [classe RegExp](http://lucene.apache.org/core/4_10_2/core/org/apache/lucene/util/automaton/RegExp.html).

**Esempio 8** -query hello pulsante destro del mouse. Ricerca di processi con il termine hello Senior o Junior.

* `&queryType=full&$select=business_title&search=business_title:/(Sen|Jun)ior/`

Nella pagina hello Hello URL per questo esempio non restituirà correttamente. In alternativa, copiare l'URL di hello seguente e incollarlo in indirizzo URL del browser hello:`http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:/(Sen|Jun)ior/)`

## <a name="wildcard-search-example"></a>Esempio di ricerca con caratteri jolly
È possibile usare una sintassi generalmente riconosciuta per ricerche con caratteri jolly per trovare più caratteri (\*) o un singolo carattere (?). Si noti query Lucene hello parser supporta l'utilizzo di hello di questi simboli con un termine singolo e non una frase.

**Esempio 9** -query hello pulsante destro del mouse. Cercare i processi che contengono hello prefisso 'prog' che include i titoli di business con i termini di hello di programmazione e programmatore in essa contenuti.

* [&queryType=full&$select=business_title&search=business_title:prog*](http://fiddle.jshell.net/liamca/gkvfLe6s/1/?index=nycjobs&apikey=252044BE3886FE4A8E3BAA4F595114BB&query=api-version=2016-09-01%26queryType=full%26$select=business_title%26search=business_title:prog*)

Non è possibile usare un carattere * o ? simbolo come primo carattere di hello di una ricerca.

## <a name="next-steps"></a>Passaggi successivi
Provare a specificare hello Lucene Parser di Query nel codice. Hello seguenti collegamenti viene illustrato come viene eseguita una query tooset la ricerca per hello API REST e .NET. collegamenti Hello utilizzano sintassi semplice di hello predefinita pertanto sarà necessario tooapply è stato descritto da questa hello toospecify articolo **queryType**.

* [Indice di ricerca di Azure utilizzando hello SDK .NET di query](search-query-dotnet.md)
* [Indice di ricerca di Azure utilizzando hello API REST di query](search-query-rest-api.md)

## <a name="see-also"></a>Vedere anche

 [Funzionamento della ricerca full-text in Ricerca di Azure](search-lucene-query-architecture.md)