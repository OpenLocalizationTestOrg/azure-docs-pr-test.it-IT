---
title: aaa "creare un indice (portale - ricerca di Azure) | Documenti di Microsoft"
description: Creare un indice utilizzando hello portale di Azure.
services: search
manager: jhubbard
author: heidisteen
documentationcenter: 
ms.assetid: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/20/2017
ms.author: heidist
ms.openlocfilehash: 4c5d663499bf73a8883690aa9482b6ba59d1ddf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-azure-portal"></a>Creare un indice di ricerca di Azure utilizzando hello portale di Azure
> [!div class="op_single_selector"]
> * [Panoramica](search-what-is-an-index.md)
> * [Portale](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

Utilizzare Progettazione indice predefinito hello in tooprototype portale Azure oppure creare un [indice di ricerca](search-what-is-an-index.md) toorun nel servizio ricerca di Azure. 

## <a name="prerequisites"></a>Prerequisiti

Questo articolo presuppone la disponibilità di una [sottoscrizione di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) e del [servizio Ricerca di Azure](search-create-service-portal.md).  

## <a name="find-your-search-service"></a>Trovare il servizio di ricerca
1. Accedi alla pagina del portale Azure toohello ed esaminare hello [una ricerca in servizi per la sottoscrizione](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)
2. Selezionare il servizio Ricerca di Azure.

## <a name="name-hello-index"></a>Nome indice hello

1. Fare clic su hello **Aggiungi indice** pulsante nella barra dei comandi nella parte superiore di hello della pagina hello hello.
2. Assegnare un nome all'indice di Ricerca di Azure. 
   * Deve iniziare con una lettera.
   * Usare solo lettere minuscole, numeri o trattini ("-").
   * Limite di caratteri di too60 nome hello.

  nome dell'indice Hello diventa parte dell'URL dell'endpoint hello utilizzato su connessioni toohello indice e per l'invio di richieste HTTP in hello API REST di ricerca di Azure.

## <a name="define-hello-fields-of-your-index"></a>Definire i campi di hello dell'indice

Composizione di indice include un *insieme Fields* che definisce i dati ricercabili hello nell'indice. In particolare, specifica struttura di hello dei documenti caricati separatamente. raccolta di campi Hello include i campi obbligatori e facoltativi, denominato e tipizzata, con indice attributi toodetermine come campo di hello può essere utilizzato.

1. In hello **Add Index** pannello, fare clic su **campi >** tooslide aprire Pannello di definizione di campo hello. 

2. Accettare hello generato *chiave* campo di tipo EDM. Per impostazione predefinita, il campo di hello è denominato *id* ma è possibile rinominare, purché la stringa hello soddisfa [regole di denominazione](https://docs.microsoft.com/rest/api/searchservice/Naming-rules). Per ogni indice di Ricerca di Azure è obbligatorio un campo chiave che deve essere una stringa.

3. Aggiungere campi toofully specificare documenti hello verrà caricato. Se i documenti includono un *id*, *nome hotel*, *indirizzo*, *Città*, e *area*, creare un campo corrispondente per ciascuno di essi nell'indice hello. Hello revisione [progettare istruzioni nella sezione hello seguente](#design) per informazioni sull'impostazione degli attributi.

4. Facoltativamente, aggiungere tutti i campi che vengono usati internamente nelle espressioni di filtro. Impostare attributi di campo hello tooexclude campi dalle operazioni di ricerca.

5. Al termine, fare clic su **OK** toosave e creare l'indice di hello.

## <a name="tips-for-adding-fields"></a>Suggerimenti per l'aggiunta di campi

Creazione di un indice nel portale di hello è elevato utilizzo della tastiera. Abbreviare la procedura seguendo questo flusso di lavoro:

1. Creare innanzitutto l'elenco di campi di hello immettendo i nomi e l'impostazione di tipi di dati.

2. Quindi utilizza hello di caselle di controllo nella parte superiore di hello di toobulk ogni attributo Abilita hello impostazione per tutti i campi e quindi cancellare selettivamente le caselle per hello alcuni campi che non è richiesto. Ad esempio, nei i campi della stringa in genere è possibile eseguire ricerche. Di conseguenza, è possibile fare clic su **Retrievable** e **Searchable** tooboth hello restituiti valori di hello campo nei risultati della ricerca, nonché consentire la ricerca full-text nel campo hello. 

<a name="design"></a>
## <a name="design-guidance-for-setting-attributes"></a>Indicazioni di progettazione per impostare gli attributi

Sebbene sia possibile aggiungere nuovi campi in qualsiasi momento, le definizioni di campo esistente vengono bloccate in per la durata di hello dell'indice hello. Per questo motivo, gli sviluppatori in genere utilizzare portale hello per la creazione di indici semplici, test idee o utilizzando hello toolook di pagine del portale di un'impostazione. Frequenti iterazione su una struttura di indice è più efficiente se si segue un approccio basato sul codice in modo da poter ripristinare facilmente indice hello.

Gli analizzatori e suggerimento associati campi prima che venga salvato l'indice di hello. Impossibile verificare tooclick tramite ogni pagina a schede tooadd language analizzatori o suggerimento tooyour definizione dell'indice.

I campi della stringa spesso sono contrassegnati come **Ricercabile** e **Recuperabile**.

Includeranno risultati di ricerca di campi utilizzati toonarrow **Sortable**, **Filterable**, e **Facetable**.

Gli attributi del campo determinano le modalità in cui un campo viene usato, ad esempio se viene usato nella ricerca full-text, nella navigazione con facet, nelle operazioni di ordinamento e così via. Hello nella tabella seguente vengono descritti gli attributi.

|Attributo|Descrizione|  
|---------------|-----------------|  
|**searchable**|Full-text ricercabili, soggetto toolexical analisi, ad esempio word breaking durante l'indicizzazione. Se si imposta un valore di campo ricercabile tooa come "sunny day", internamente verrà suddiviso in hello token singoli "sunny" e "day". Per informazioni vedere [Funzionamento della ricerca full-text](search-lucene-query-architecture.md).|  
|**filterable**|A cui si fa riferimento nelle query **$filter**. I campi filtrabili di tipo `Edm.String` o `Collection(Edm.String)` non sono sottoposti a suddivisione delle parole e quindi i confronti riguardano solo le corrispondenze esatte. Ad esempio, se si imposta un campo f troppo "sunny day" `$filter=f eq 'sunny'` troverà alcuna corrispondenza, ma `$filter=f eq 'sunny day'` verrà. |  
|**sortable**|Per impostazione predefinita sistema hello Ordina risultati in base al punteggio, ma è possibile configurare l'ordinamento in base ai campi nei documenti di hello. I campi di tipo `Collection(Edm.String)` non possono essere **ordinabili**. |  
|**facetable**|In genere usato in una presentazione dei risultati della ricerca che include un numero di passaggi per categoria, ad esempio, gli hotel in una specifica città. Questa opzione non può essere usata con i campi di tipo `Edm.GeographyPoint`. I campi di tipo `Edm.String` che sono **filtrabili**, **ordinabili**, o **con facet** possono contenere al massimo 32 kilobyte di lunghezza. Per altri dettagli, vedere [Create Index (REST API)](https://docs.microsoft.com/rest/api/searchservice/create-index)(Creare un indice: API REST).|  
|**key**|Identificatore univoco per i documenti all'interno dell'indice hello. Deve essere scelti esattamente un campo come campo chiave hello e deve essere di tipo `Edm.String`.|  
|**retrievable**|Determina se il campo hello può essere restituito nei risultati di ricerca. Ciò è utile quando si desidera che un campo toouse (ad esempio *margine di profitto*) come filtro, ordinamento o punteggio meccanismo, ma non si desidera hello campo toobe toohello visibile finale. L'attributo deve essere `true` for `key` .|  

## <a name="create-hello-hotels-index-used-in-example-api-sections"></a>Creare hello hotel indice utilizzato nelle sezioni di API di esempio

La documentazione API di Ricerca di Azure include esempi di codice che presentano un semplice indice *hotel*. In hello schermate riportate di seguito, è possibile visualizzare una definizione di indice di hello, incluso l'analizzatore di lingua francese hello specificato durante la definizione dell'indice, che è possibile ricreare come un'esercitazione nel portale di hello.

![](./media/search-create-index-portal/field-definitions.png)

![](./media/search-create-index-portal/set-analyzer.png)

## <a name="next-steps"></a>Passaggi successivi

Dopo aver creato un indice di ricerca di Azure, è possibile spostare passaggio successivo toohello: [caricamento dati disponibile per la ricerca nell'indice hello](search-what-is-data-import.md).

In alternativa, è anche possibile analizzare in modo approfondito gli indici. Raccolta di campi toohello, un indice anche specifica inoltre gli analizzatori, suggerimento, profili e impostazioni di CORS di punteggio. Hello portale fornisce pagine a schede per definire gli elementi più comuni di hello: i campi e gli analizzatori di suggerimento. toocreate o modificare altri elementi, è possibile utilizzare hello API REST o .NET SDK.

## <a name="see-also"></a>Vedere anche

 [Funzionamento della ricerca full-text](search-lucene-query-architecture.md)  
 [API REST del servizio Ricerca](https://docs.microsoft.com/rest/api/searchservice/)[ .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/search?view=azure-dotnet)

