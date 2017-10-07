---
titolo: aaa "Esercitazione: creare il primo indice di ricerca di Azure nel portale di hello | Descrizione di "Microsoft Docs: hello portale di Azure, utilizzare predefiniti toogenerate dati di esempio un indice. È possibile esplorare la ricerca full-text, i filtri, i facet, la ricerca fuzzy, la ricerca geografica e altro ancora.
servizi: ricerca documentationcenter: ' autore: manager HeidiSteen: jhubbard editor: ' tag: portale di azure

ms. AssetID: ms. Service 21adc351-69bb-4a39-bc59-598c60c8f958: ricerca ms. DevLang: Workload na: ricerca ms. topic: ms. tgt_pltfrm hero-article: ms. date na: author 26/06/2017: heidist

---
# <a name="tutorial-create-your-first-azure-search-index-in-hello-portal"></a>Esercitazione: Creare il primo indice di ricerca di Azure nel portale di hello

Nel portale di Azure hello, iniziare con un tooquickly di set di dati di esempio predefiniti generare un indice utilizzando hello **importare dati** procedura guidata. Con **Esplora ricerche** è possibile esplorare la ricerca full-text, i filtri, i facet, la ricerca fuzzy e la ricerca geografica.  

Questa introduzione senza codice permette di iniziare a usare i dati predefiniti per poter scrivere query interessanti fin da subito. Gli strumenti del portale non sostituiscono il codice, ma sono utili per eseguire queste attività:

+ Apprendere in modo pratico con una preparazione minima.
+ Creare il prototipo di un indice prima di scrivere codice in **Importa dati**.
+ Testare le query e la sintassi del parser in **Esplora ricerche**.
+ Visualizzare un oggetto esistente indice servizio pubblicato tooyour e cercare gli attributi

**Tempo stimato:** circa 15 minuti. Di più se è anche necessario eseguire l'iscrizione a un account o un servizio. 

In alternativa, salita utilizzando un [tooprogramming Introduzione basata su codice ricerca di Azure in .NET](search-howto-dotnet-sdk.md).

## <a name="prerequisites"></a>Prerequisiti

Questa esercitazione presuppone la disponibilità di una [sottoscrizione di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) e del [servizio Ricerca di Azure](search-create-service-portal.md). 

Se si desidera immediatamente tooprovision un servizio, è possibile controllare i passaggi da 6 minuti di hello in questa esercitazione, a partire da circa tre minuti in questa [video Cenni preliminari sulla ricerca di Azure](https://channel9.msdn.com/Events/Connect/2016/138).

## <a name="find-your-service"></a>Trovare il servizio
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Aprire il dashboard del servizio hello del servizio di ricerca di Azure. Se si non aggiungere hello servizio riquadro tooyour dashboard, è possibile trovare il servizio in questo modo: 
   
   * In hello Jumpbar, fare clic su **più servizi** nella parte inferiore di hello del riquadro di spostamento a sinistra di hello.
   * Nella casella di ricerca hello, digitare *ricerca* tooget un elenco di ricerca di servizi per la sottoscrizione. Il servizio verrà visualizzato nell'elenco di hello. 

## <a name="check-for-space"></a>Verificare lo spazio
Molti clienti che iniziano con servizio gratuito hello. Questa versione è limitato toothree indici, tre origini dati e tre gli indicizzatori. Assicurarsi di avere spazio per gli elementi aggiuntivi prima di iniziare, perché ne verrà creato uno per ogni oggetto. 

> [!TIP] 
> Riquadri nei dashboard del servizio hello mostrano il numero di indici, gli indicizzatori e origini dati si dispone già. riquadro indicizzatore Hello Mostra gli indicatori di esito positivo e negativo. Fare clic su hello riquadro tooview hello indicizzatore conteggio. 
>
> ![Riquadri degli indicizzatori e delle origini dati][1]
>

## <a name="create-index"></a> Creare un indice e caricare i dati
Le query di ricerca scorrono un *indice* contenente dati ricercabili, metadati e costrutti usati per l'ottimizzazione di determinati comportamenti di ricerca.

tookeep questa attività basate sul portale, utilizziamo un set di dati di esempio predefiniti che possono essere indicizzati mediante un indicizzatore tramite hello **importare dati** procedura guidata. 

#### <a name="step-1-start-hello-import-data-wizard"></a>Passaggio 1: Avviare hello importazione guidata dati
1. Nel dashboard del servizio ricerca di Azure, fare clic su **importare dati** in hello comando barra toostart una procedura guidata che crea e popola un indice.
   
    ![Comando Importa dati][2]

2. Nella procedura guidata hello, fare clic su **origine dati** > **esempi** > **realestate-us-esempio**. Questa origine dati è preconfigurata con un nome, un tipo e informazioni di connessione. Dopo la creazione, diventa una "origine dati esistente" che può essere riutilizzata in altre operazioni di importazione.

    ![Selezionare il set di dati di esempio][9]

3. Fare clic su **OK** toouse è.

#### <a name="step-2-define-hello-index"></a>Passaggio 2: Definire indice hello
Creazione di un indice è in genere manuale e basata su codice, ma la procedura guidata hello può generare un indice per qualsiasi origine dati che è possibile eseguire ricerche per indicizzazione. Come minimo, un indice richiede un nome e una raccolta di campi, con un campo contrassegnato come hello toouniquely chiave documento identificano ogni documento.

I campi hanno tipi di dati e attributi. caselle di controllo Hello in alto hello sono *indice attributi* controllo della modalità di utilizzo campo hello. 

* **Recuperabile** indica che viene visualizzato nell'elenco dei risultati della ricerca. Deselezionando questa casella di controllo è possibile contrassegnare i singoli campi perché siano esclusi dai risultati della ricerca, ad esempio quando vengono usati solo nelle espressioni di filtro. 
* **Filtrabile**, **Ordinabile** e **Con facet** determinano se un campo può essere usato in un filtro, un ordinamento o una struttura di esplorazione in base a facet. 
* **Ricercabile** indica che un campo è incluso nella ricerca full-text. Le stringhe sono ricercabili. I campi numerici e i campi booleani sono spesso contrassegnati come non ricercabili. 

Per impostazione predefinita, la procedura guidata hello analizza origine dati hello per gli identificatori univoci come base hello per il campo chiave hello. Le stringhe vengono attribuite come recuperabili e ricercabili. Gli Integer vengono attribuiti come recuperabili, filtrabili, ordinabili e con facet.

  ![Indice realestate generato][3]

Fare clic su **OK** indice hello toocreate.

#### <a name="step-3-define-hello-indexer"></a>Passaggio 3: Definire indicizzatore hello
Ancora in hello **importare dati** procedura guidata, fare clic su **indicizzatore** > **nome**e digitare un nome di un indicizzatore hello. 

Questo oggetto definisce un processo eseguibile. È possibile attivare su pianificazione ricorrente, ma per ora utilizzare hello opzione toorun hello indicizzatore una volta, immediatamente, quando fa clic su **OK**.  

  ![Indicizzatore realestate][8]

## <a name="check-progress"></a>Verificare l'avanzamento
dati toomonitor importare, tornare indietro toohello dashboard del servizio, scorrere verso il basso e fare doppio clic su hello **indicizzatori** elenco di icone tooopen hello gli indicizzatori. Dovrebbe essere indicizzatore hello appena creato nell'elenco di hello, che indica lo stato "in corso" o non riuscita, con numero di hello di documenti indicizzati.

   ![Messaggio di stato dell'indicizzatore][4]

## <a name="query-index"></a>Indice di query hello
È ora disponibile un indice di ricerca è tooquery pronto. **Esplora ricerche** è uno strumento di query incorporato nel portale di hello. Include una casella di ricerca che permette di verificare se i risultati della ricerca sono quelli previsti. 

> [!TIP]
> In hello [video Cenni preliminari sulla ricerca di Azure](https://channel9.msdn.com/Events/Connect/2016/138), hello alla procedura seguente viene illustrata in 6m08s video hello.
>

1. Fare clic su **Esplora ricerche** hello barra dei comandi.

   ![Comando di Esplora ricerche][5]

2. Fare clic su **indice modifica** su hello barra dei comandi tooswitch troppo*realestate-us-esempio*.

   ![Comandi dell'indice e dell'API][6]

3. Fare clic su **versione API impostare** su hello comando barra toosee che sono disponibili le API REST. Visualizzare in anteprima consentono l'API che accesso toonew funzionalità non è ancora in genere rilasciata. Per le query hello riportato di seguito, utilizzare la versione disponibile a livello generale hello (2016-09-01) solo se indicato. 

    > [!NOTE]
    > [API REST di ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/search-documents) hello e [libreria .NET](search-howto-dotnet-sdk.md#core-scenarios) completamente equivalenti, ma **Esplora ricerche** solo le chiamate REST toohandle completa. Accetta la sintassi sia per [semplice sintassi di query](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) e [completo parser di query Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), più tutte hello parametri di ricerca disponibili in [ricerca nel documento](https://docs.microsoft.com/rest/api/searchservice/search-documents) operazioni.
    > 

4. Nella barra di ricerca hello, immettere le stringhe di query hello riportato di seguito e fare clic su **ricerca**.

  ![Esempio di query di ricerca][7]

**`search=seattle`**

+ Hello `search` parametro è utilizzato tooinput una ricerca per parole chiave per la ricerca full-text, in questo caso, la restituzione di elenchi in stato di King County, Washington, contenente *Seattle* in qualsiasi campo disponibile per la ricerca nel documento hello. 

+ **Esplora ricerche** restituisce i risultati in JSON, ovvero tooread dettagliato e disco rigido se documenti hanno una struttura di tipo densa. A seconda dei documenti, potrebbe essere necessario codice toowrite che gli handle di ricerca di elementi importanti tooextract di risultati. 

+ I documenti sono costituiti da tutti i campi contrassegnati come recuperabili nello indice hello. Fare clic su attributi di indice tooview nel portale di hello *realestate-us-esempio* in hello **indici** riquadro.

**`search=seattle&$count=true&$top=100`**

+ Hello `&` simbolo è tooappend utilizzati parametri di ricerca, che possono essere specificati in qualsiasi ordine. 

+  Hello `$count=true` parametro restituisce un conteggio per la somma di tutti i documenti restituiti hello. È possibile verificare le query filtro monitorando le modifiche segnalate da `$count=true`. 

+ Hello `$top=100` hello restituisce più alto classificate 100 documenti fuori hello totale. Per impostazione predefinita, ricerca di Azure restituisce hello primi 50 corrispondenze migliori. È possibile aumentare o diminuire la quantità hello tramite `$top`.

**`search=*&facet=city&$top=2`**

+ `search=*` è una ricerca vuota. Le ricerche vuote permettono di eseguire la ricerca su tutti gli elementi. Uno dei motivi per l'invio di una query vuota è troppo filtrare o facet su set completo di hello dei documenti. Ad esempio, si desidera un tooconsist struttura di navigazione di facet di tutte le città indice hello.

+  `facet`Restituisce un oggetto di navigazione della struttura che è possibile passare un controllo dell'interfaccia utente tooa. Restituisce un conteggio e categorie. In questo caso, le categorie in base hello numero di città. Ricerca di Azure non prevede alcuna aggregazione, ma è possibile ottenere qualcosa di simile all'aggregazione usando `facet`, che restituisce un conteggio dei documenti in ogni categoria.

+ `$top=2`riporta i due documenti, che illustra che è possibile utilizzare `top` tooboth ridurre o aumentare i risultati.

**`search=seattle&facet=beds`**

+ Questa query consente l'esplorazione in base a facet e cerca "beds", ovvero "letti", in una ricerca di testo di *seattle*. `"beds"`può essere specificata come un facet perché hello campo viene contrassegnato come recuperabili, filtrabile e di valori, facetable indice hello e hello contiene (numerico, da 1 a 5), sono adatti per la categorizzazione di elenchi in gruppi (elenchi con 3 camere, 4 camere). 

+ Solo i campi filtrabili sono adatti all'esplorazione in base a facet. Solo i campi recuperabili possono essere restituiti nei risultati di hello.

**`search=seattle&$filter=beds gt 3`**

+ Hello `filter` parametro restituisce risultati corrispondenti ai criteri di hello fornito. In questo caso, un numero di camere da letto maggiore di 3. 

+ La sintassi del filtro è una costruzione OData. Per altre informazioni, vedere l'articolo relativo alla [sintassi OData per i filtri](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search).

**`search=granite countertops&highlight=description`**

+ Evidenziazione dei riscontri fa riferimento tooformatting sul testo corrispondente parola chiave hello specificato corrisponde presenti in un campo specifico. Se il termine di ricerca è eccessivamente inclusa in una descrizione, è possibile aggiungere passaggi toomake evidenziazione si toospot più semplice. In questo caso, hello formattato frase `"granite countertops"` è più facile toosee nel campo Descrizione hello.

**`search=mice&highlight=description`**

+ La ricerca full-text permette di trovare forme di termini con una semantica simile. In questo caso, i risultati della ricerca contengono testo evidenziato per "mouse", per i case che dispongono di grado del mouse, in risposta tooa ricerca per parole chiave in "mouse". Diverse forme della stessa parola può essere visualizzati nei risultati a causa di analisi linguistica hello. 

+ Ricerca di Azure supporta 56 analizzatori, sia Microsoft che Lucene. valore predefinito di Hello utilizzato dalla ricerca di Azure è analizzatore Lucene standard hello. 

**`search=samamish`**

+ Ortografia, ad esempio 'samamish' per la stabilizzazione Samammish hello nell'area di Seattle, hello non corrispondenze tooreturn in ricerca tipiche. errori di ortografia toohandle, è possibile utilizzare ricerca fuzzy, descritto nell'esempio riportato di seguito hello.

**`search=samamish~&queryType=full`**

+ La ricerca fuzzy è abilitata quando si specifica hello `~` dei simboli e utilizzare i parser di query completa hello, che vengono interpretati e analizza correttamente hello `~` sintassi. 

+ Ricerca fuzzy è disponibile quando si sceglie di partecipare per parser di query completa hello, che si verifica quando si imposta `queryType=full`. Per ulteriori informazioni sugli scenari di query abilitata dal parser di query completa hello, vedere [Lucene sintassi delle query in ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search).

+ Quando `queryType` è non specificato, hello predefinito simple query parser viene utilizzato. parser di query semplice Hello è più veloce, ma se è necessaria la ricerca fuzzy, le espressioni regolari, ricerca per prossimità o altri tipi di query avanzate, sarà necessario sintassi completa di hello. 

**`search=*&$count=true&$filter=geo.distance(location,geography'POINT(-122.121513 47.673988)') le 5`**

+ La ricerca geospaziale è supportata tramite hello [edm. Tipo di dati GeographyPoint](https://docs.microsoft.com/rest/api/searchservice/supported-data-types) su un campo che contiene le coordinate. La ricerca geografica è un tipo di filtro, illustrato nell'articolo relativo alla [sintassi OData per i filtri](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search). 

+ query di esempio Hello Filtra tutti i risultati per dati posizionali, in cui risultati sono meno di 5 miglia da un determinato punto (specificato come coordinate di latitudine e longitudine). Aggiungendo `$count`, è possibile visualizzare il numero di risultati viene restituito quando si modifica la distanza hello o hello coordinate. 

+ La ricerca geospaziale risulta utile se l'applicazione di ricerca include una funzionalità di "ricerca nelle vicinanze" o usa l'esplorazione mappa. Non si tratta, tuttavia, di una ricerca full-text. Se si dispone di requisiti per la ricerca in una città o il paese in base al nome dell'utente, aggiungere i campi contenenti i nomi di città o il paese, in aggiunta toocoordinates.

## <a name="next-steps"></a>Passaggi successivi

+ Modificare uno qualsiasi degli oggetti hello che appena creato. Dopo aver eseguito la procedura guidata hello una sola volta, è possibile tornare indietro e visualizzare o modificare i singoli componenti: origine dati, l'indicizzatore o indice. Alcune modifiche, ad esempio hello Modifica tipo di dati del campo hello, non sono consentiti su indice hello, ma la maggior parte delle proprietà e le impostazioni sono modificabili.

  tooview singoli componenti, fare clic su hello **indice**, **indicizzatore**, o **origini dati** riquadri di un elenco degli oggetti esistenti sul toodisplay dashboard. toolearn più informazioni sulle modifiche di indice che non richiedono una ricompilazione, vedere [Update Index (API REST di ricerca di Azure)](https://docs.microsoft.com/rest/api/searchservice/update-index).

+ Provare a hello strumenti e passaggi con altre origini dati. set di dati di esempio, Hello `realestate-us-sample`, provengono da un Database SQL di Azure che eseguire ricerche per indicizzazione di ricerca di Azure. Oltre che nel database SQL di Azure, Ricerca di Azure permette di effettuare ricerche per indicizzazione e dedurre un indice da strutture di dati flat nell'archivio tabelle di Azure, nell'archivio BLOB, in SQL Server in una macchina virtuale di Azure e in Azure Cosmos DB. Tutte le origini dati sono supportate nella procedura guidata hello. Nel codice è possibile popolare facilmente un indice tramite un *indicizzatore*.

+ Tutte le altre origini dati relative a indicizzatori non sono supportate tramite un modello push, in cui il codice inserisce nuovi e modificati i set di righe nell'indice tooyour JSON. Per altre informazioni, vedere [Add, update, or delete documents in Azure Search](https://docs.microsoft.com/rest/api/searchservice/addupdate-or-delete-documents) (Aggiungere, aggiornare o eliminare documenti da Ricerca di Azure).

Per informazioni sulle altre funzionalità descritte in questo articolo, visitare i collegamenti seguenti:

* [Panoramica degli indicizzatori](search-indexer-overview.md)
* [Creare l'indice (include una spiegazione dettagliata di attributi dell'indice hello)](https://docs.microsoft.com/rest/api/searchservice/create-index)
* [Esplora ricerche](search-explorer.md)
* [Eseguire ricerche nei documenti, include esempi di sintassi di query.](https://docs.microsoft.com/rest/api/searchservice/search-documents)


<!--Image references-->
[1]: ./media/search-get-started-portal/tiles-indexers-datasources2.png
[2]: ./media/search-get-started-portal/import-data-cmd2.png
[3]: ./media/search-get-started-portal/realestateindex2.png
[4]: ./media/search-get-started-portal/indexers-inprogress2.png
[5]: ./media/search-get-started-portal/search-explorer-cmd2.png
[6]: ./media/search-get-started-portal/search-explorer-changeindex-se2.png
[7]: ./media/search-get-started-portal/search-explorer-query2.png
[8]: ./media/search-get-started-portal/realestate-indexer2.png
[9]: ./media/search-get-started-portal/import-datasource-sample2.png