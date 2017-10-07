---
title: risultati della ricerca di toopage aaaHow in ricerca di Azure | Documenti Microsoft
description: "L’impaginazione in Ricerca di Azure, un servizio di ricerca ospitato sul cloud in Microsoft Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: e3abc1ca4d5994b0a77955379081a4fcfa5a7fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopage-search-results-in-azure-search"></a>La vista dei risultati ricerca toopage in ricerca di Azure
Questo articolo fornisce istruzioni su come toouse hello API REST di Azure ricerca tooimplement elementi standard di una ricerca di pagina dei risultati, ad esempio nei conteggi totali, il recupero di documenti, ordinamento e la navigazione.

In ogni caso riportato di seguito, le opzioni relative alla pagina che contribuiscono a dati o pagina di risultati di ricerca tooyour vengono specificate mediante hello [ricerca nel documento](http://msdn.microsoft.com/library/azure/dn798927.aspx) tooyour le richieste inviate il servizio di ricerca di Azure. Le richieste includono un comando GET, percorso e che servizio hello ciò che viene richiesto di indicare i parametri di query e come tooformulate hello risposta.

> [!NOTE]
> Una richiesta valida include diversi elementi, ad esempio URL e percorso del servizio, verbo HTTP, `api-version`, e così via. Per ragioni di brevità, ci tagliati hello esempi toohighlight hello solo la sintassi toopagination pertinente. Vedere hello [API REST di Azure ricerca](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentazione per informazioni dettagliate sulla sintassi della richiesta.
> 
> 

## <a name="total-hits-and-page-counts"></a>Corrispondenze totali e conteggi delle pagine
Visualizzazione hello totale numero di risultati restituiti da una query e quindi vengono restituiti i risultati in blocchi più piccoli, è fondamentale toovirtually tutte le pagine di ricerca.

![][1]

In ricerca di Azure, utilizzare hello `$count`, `$top`, e `$skip` tooreturn parametri questi valori. Hello esempio seguente viene illustrato un esempio di richiesta per Totale riscontri, restituito come `@OData.count`:

        GET /indexes/onlineCatalog/docs?$count=true

Recuperare i documenti in gruppi di 15 e visualizzare Totale riscontri hello, a partire dalla prima pagina hello:

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

L'impaginazione risultati richiede entrambi `$top` e `$skip`, dove `$top` specifica quanti elementi tooreturn in un batch, e `$skip` specifica quanti elementi tooskip. In hello seguente esempio, ogni pagina sono visualizzati hello elementi successivamente 15, indicato da salti incrementale di hello in hello `$skip` parametro.

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a>Layout
In una pagina di risultati di ricerca, è opportuno tooshow un'immagine di anteprima, un sottoinsieme dei campi e una pagina di collegamento tooa completa del prodotto.

 ![][2]

In ricerca di Azure, è consigliabile usare `$select` e una ricerca dei comandi tooimplement questa esperienza.

tooreturn un sottoinsieme dei campi per un layout affiancato:

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

Le immagini e file multimediali non sono direttamente ricercabili e devono essere archiviati in un'altra piattaforma di archiviazione, ad esempio l'archiviazione Blob di Azure, i costi tooreduce. Indice di hello e documenti, definire un campo che archivia l'indirizzo URL hello di contenuto esterno hello. È quindi possibile utilizzare il campo hello come riferimento a un'immagine. immagine di toohello Hello URL deve essere nel documento hello.

tooretrieve pagina una descrizione del prodotto per un **onClick** evento, utilizzare [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass nella chiave hello di hello documento tooretrieve. Hello è di tipo chiave hello `Edm.String`. In questo esempio è *246810*. 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a>Ordinare per pertinenza, classificazione o prezzo
Tipi di ordinamento spesso toorelevance predefinito, ma è comuni tipi di ordinamento alternativo toomake immediatamente disponibili in modo che i clienti possono riassegnare rapidamente risultati esistenti in un ordine di rango diverso.

 ![][3]

In ricerca di Azure, ordinamento si basa su hello `$orderby` per tutti i campi indicizzati come espressione`"Sortable": true.`

La pertinenza è fortemente associata ai profili di punteggio. È possibile utilizzare hello punteggio predefinito, che si basa sull'ordinamento di toorank statistiche e di analisi del testo, tutti i risultati con punteggi maggiori succedendo toodocuments con corrispondenze più o maggiore di un termine di ricerca.

Sono in genere associati tipi di ordinamento alternativo **onClick** gli eventi che chiamano il metodo tooa che compila ordinamento hello. Si consideri, ad esempio, questo elemento di pagina:

 ![][4]

Creare un metodo che accetta l'opzione di ordinamento hello selezionata come input e restituisce un elenco ordinato per i criteri di hello associata a tale opzione.

 ![][5]

> [!NOTE]
> Mentre il punteggio predefinito hello è sufficiente per molti scenari, è consigliabile basare pertinenza su un profilo di punteggio personalizzato invece. Un profilo di punteggio personalizzato offre un modo tooboost, gli elementi che sono più conveniente tooyour business. Vedere [Aggiungere un profilo di punteggio](http://msdn.microsoft.com/library/azure/dn798928.aspx) per ulteriori informazioni. 
> 
> 

## <a name="faceted-navigation"></a>Esplorazione in base a facet
Spostamento di ricerca è comune in una pagina di risultati, che spesso si trova nel lato hello o superiore di una pagina. In Ricerca di Azure, l’esplorazione basata su facet fornisce una ricerca autoindirizzata in base a filtri predefiniti. Per maggiori informazioni vendere [Esplorazione basata su facet in Ricerca di Azure](search-faceted-navigation.md) .

## <a name="filters-at-hello-page-level"></a>Filtri a livello di pagina hello
Se la progettazione della soluzione include pagine di ricerca dedicato per tipi specifici di contenuto (ad esempio, un'applicazione di vendita al dettaglio online con reparti elencati nella parte superiore di hello della pagina hello), è possibile inserire un'espressione di filtro insieme a un **onClick** evento tooopen una pagina in uno stato prefiltrato. 

È possibile inviare un filtro con o senza espressione di ricerca. Ad esempio, hello richiesta seguente filtrerà marca, restituendo solo i documenti corrispondenti.

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

Vedere [Ricerca nei documenti (API di Ricerca di Azure)](http://msdn.microsoft.com/library/azure/dn798927.aspx) per altre informazioni sulle espressioni `$filter`.

## <a name="see-also"></a>Vedere anche
* [API REST per il servizio Ricerca di Azure](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [Operazioni sugli indici](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [Operazioni sui documenti](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [Video ed esercitazioni su Ricerca di Azure](search-video-demo-tutorial-list.md)
* [Esplorazione in base a facet in Ricerca di Azure](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
