---
title: Indice di ricerca di Azure aaaQuery | Documenti Microsoft
description: Compilare una query di ricerca in ricerca di Azure e usare i parametri toofilter e ordinamento ricerca risultati della ricerca.
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 69205d7a-363f-4b92-a53f-6ca818a3d2c7
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: ashmaka
ms.openlocfilehash: 4a5ffffe179695fc09446760e21a738dd36c29b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index"></a>Eseguire query su un indice di Ricerca di Azure
> [!div class="op_single_selector"]
> * [Panoramica](search-query-overview.md)
> * [Portale](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Quando si inviano richieste di ricerca tooAzure ricerca, sono disponibili un numero di parametri che possono essere specificati insieme a parole effettivo hello digitato nella casella di ricerca hello dell'applicazione. Questi parametri di query consentono di tooachieve un controllo più approfondito di hello [un'esperienza di ricerca full-text](search-lucene-query-architecture.md).

Di seguito è riportato un elenco che illustra brevemente usi comuni dei parametri di query hello in ricerca di Azure. Per una copertura completa di parametri di query e il relativo comportamento, vedere hello dettagliate pagine per hello [API REST](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) e [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters#microsoft_azure_search_models_searchparameters#properties_summary).

## <a name="types-of-queries"></a>Tipi di query
Ricerca di Azure offre molte opzioni toocreate estremamente efficaci le query. Hello due tipi principali di query si utilizzerà sono `search` e `filter`. Oggetto `search` query esegue la ricerca per uno o più termini in tutti *ricercabili* campi nell'indice e funziona come hello che ci si aspetta un motore di ricerca come Bing o Google toowork. Una query `filter` valuta un'espressione booleana su tutti i campi *filtrabili* di un indice. A differenza di `search` query `filter` query corrispondono contenuto esatto di hello di un campo, ossia sono distinzione maiuscole/minuscole per i campi string.

È possibile usare le ricerche e i filtri insieme o separatamente. Se vengono usati insieme, hello filtro è applicato l'intero indice della prima toohello e quindi hello ricerca viene eseguita risultati hello hello filtro. I filtri possono pertanto le prestazioni delle query tooimprove una tecnica utile poiché riducono il set di hello di documenti hello tooprocess esigenze query di ricerca.

sintassi di Hello per le espressioni di filtro è un subset di hello [language filtro OData](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search). Per le query di ricerca è possibile utilizzare entrambi hello [la sintassi semplificata](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) o hello [sintassi delle query Lucene](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) che sono descritti di seguito.

### <a name="simple-query-syntax"></a>Sintassi di query semplice
Hello [semplice sintassi di query](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search) è linguaggio di query predefinito hello usata in ricerca di Azure. Hello semplice sintassi di query supporta un numero di operatori di ricerca comuni, inclusi hello AND, OR, NOT, una frase, suffisso e precedenza degli operatori.

### <a name="lucene-query-syntax"></a>sintassi di query Lucene
Hello [sintassi delle query Lucene](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search) consente hello toouse ampiamente adottato e linguaggio di query espressivo sviluppata come parte del [Apache Lucene](https://lucene.apache.org/core/4_10_2/queryparser/org/apache/lucene/queryparser/classic/package-summary.html).

Utilizzando questa sintassi di query consente tooeasily ottenere hello seguenti funzionalità: [query con ambito campo](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fields), [ricerca fuzzy](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_fuzzy), [ricerca per prossimità](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_proximity), [ al termine boosting](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_termboost), [ricerca di espressione regolare](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_regex), [ricerca con caratteri jolly](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_wildcard), [nozioni fondamentali sulla sintassi](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_syntax), e [utilizzando una query operatori booleani](https://docs.microsoft.com/rest/api/searchservice/Lucene-query-syntax-in-Azure-Search#bkmk_boolean).

## <a name="ordering-results"></a>Ordinamento dei risultati
Quando si ricevono risultati per una query di ricerca, è possibile richiedere che ricerca di Azure serve risultati hello ordinati in base ai valori di un campo specifico. Per impostazione predefinita, ricerca di Azure Ordina i risultati della ricerca hello in base a classifica hello del punteggio di ricerca di ciascun documento, che deriva da [TF-IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf).

Se si desidera i risultati ordinati in base a un valore diverso da punteggio di ricerca hello tooreturn di ricerca di Azure, è possibile utilizzare hello `orderby` parametro di ricerca. È possibile specificare il valore di hello di hello `orderby` nomi di campo tooinclude del parametro e chiama toohello [ `geo.distance()` funzione](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search) per i valori geospaziali. Ogni espressione può essere seguito da `asc` tooindicate che i risultati vengono richiesti in ordine crescente e `desc` tooindicate che i risultati vengono richiesti in ordine decrescente. classificazione predefinita di Hello ordine crescente.

## <a name="paging"></a>Paging
Ricerca di Azure rende facile tooimplement il paging dei risultati della ricerca. Utilizzando hello `top` e `skip` parametri, è possibile eseguire in modo uniforme le richieste di ricerca che consentono di set totale di hello tooreceive dei risultati della ricerca in subset gestibile, ordinato in grado di abilitare facilmente consigliate dell'interfaccia utente di ricerca valida. Quando si ricevono questi subset più piccolo di risultati, è inoltre possibile ottenere il conteggio di hello dei documenti nel set di totale hello dei risultati della ricerca.

È possibile approfondire il paging dei risultati di ricerca nell'articolo hello [come risultati della ricerca toopage in ricerca di Azure](search-pagination-page-layout.md).

## <a name="hit-highlighting"></a>Evidenziazione dei risultati
In ricerca di Azure, che mettono in evidenza hello esatta parte i risultati di ricerca che corrispondono a query di ricerca hello è semplice utilizzando hello `highlight`, `highlightPreTag`, e `highlightPostTag` parametri. È possibile specificare quali *ricercabili* campi devono avere il testo corrispondente evidenziato e specificando restituisce hello esatta stringa tag tooappend toohello inizio e fine di hello corrispondente testo di ricerca di Azure.

## <a name="try-out-query-syntax"></a>Prova della sintassi di query

differenze sintattiche toounderstand Hello migliore modo consiste nell'invio di query e revisione dei risultati.

+ Utilizzare [Esplora ricerche](search-explorer.md) in hello portale di Azure. Distribuendo [indice degli esempi di hello](search-get-started-portal.md), è possibile eseguire query indice hello in minuti di utilizzo degli strumenti nel portale di hello.

+ Utilizzare [Fiddler](search-fiddler.md) o Chrome Postman toosubmit query tooan indice che è stato caricato il servizio di ricerca tooyour. Entrambi gli strumenti supportano endpoint HTTP tooan di chiamate REST. 
