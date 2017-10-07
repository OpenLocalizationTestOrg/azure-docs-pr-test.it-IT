---
title: 'Schema progettuale di Azure Cosmos DB: app di social media | Microsoft Docs'
description: "Informazioni su un modello di progettazione per Social Network sfruttando la flessibilità di hello archiviazione di Azure Cosmos DB e altri servizi di Azure."
keywords: app di social media
services: cosmos-db
author: ealsur
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 2dbf83a7-512a-4993-bf1b-ea7d72e095d9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: mimig
ms.openlocfilehash: 47a22f2c5762d62b176921c8052e7bd75d8cf6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="going-social-with-azure-cosmos-db"></a>Integrazione con i social con Azure Cosmos DB
Vivere in una società profondamente interconnessa porta, prima o poi, ad avere a che fare con i **social network**. Utilizziamo tookeep social network in contatto con amici, colleghi, familiari e talvolta tooshare intento con le persone con interessi comuni.

Come tecnici o gli sviluppatori, è possibile spiega come queste reti archiviazione e i dati sono collegati o potrebbe avere anche stato toocreate assegnati compiti o architect una nuova rete sociale per una specifica nicchia mercato personalmente. Ovvero quando si verifica domanda big hello: modalità di tutti i dati di archiviazione?

Si supponga di voler creare un nuovo social network, in cui gli utenti possano pubblicare articoli con elementi multimediali correlati, ad esempio immagini, video o musica, La pagina di destinazione principale del sito Web includerà un feed di post che gli utenti possono visualizzare e con cui possono interagire. Sarà presente un feed di post che gli utenti vedono e in grado di toointeract con nella pagina di destinazione del sito Web principale hello. Questo non sembrare molto complesso (inizialmente), ma per i migliori risultati hello di semplicità, si esaurisce (è possibile approfondire feed personalizzati utente influenzato dalle relazioni, ma quest'ultimo supera l'obiettivo di hello di questo articolo).

Come e dove archiviare i dati?

Molti di voi potrebbe avere esperienza nei database SQL oppure disporre almeno nozione di [modellazione dei dati relazionali](https://en.wikipedia.org/wiki/Relational_model) e potrebbe essere tentati toostart disegno simile al seguente:

![Diagramma che illustra un modello relazionale relativo](./media/social-media-apps/social-media-apps-sql.png) 

Una struttura di dati perfettamente normalizzata... che non supporta la scalabilità. 

I database SQL sono certamente molto utili, ma come ogni modello, procedura e piattaforma software non sono perfetti per tutti gli scenari.

Non è ottimale hello SQL in questo scenario. Si esaminerà la struttura hello di un messaggio, se desidera tooshow che registra in un sito Web o un'applicazione, è necessario toodo una query con... tabella 8 join (!) tooshow solo una singola post, ora, immagine, un flusso di messaggi che vengono caricate in modo dinamico e visualizzato nella schermata di hello e si potrebbe essere visualizzato in cui verrà.

È possibile, ovviamente, usare un'istanza di SQL humongous con sufficiente toosolve power migliaia di query con questi tooserve join molti contenuti, ma davvero, motivo per cui si è quando una soluzione più semplice esiste?

## <a name="hello-nosql-road"></a>strada NoSQL Hello
Questo articolo verranno illustrati nella modellazione dei dati con database NoSQL di Azure della piattaforma di social [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) in modo economico, sfruttando al contempo altre funzionalità di database di Azure Cosmos come hello [API Graph Gremlin ](../cosmos-db/graph-introduction.md). Con un approccio [NoSQL](https://en.wikipedia.org/wiki/NoSQL), che prevede l'archiviazione dei dati in formato JSON e l'applicazione della [denormalizzazione](https://en.wikipedia.org/wiki/Denormalization), il post che prima risultava complesso può essere trasformato in un singolo [documento](https://en.wikipedia.org/wiki/Document-oriented_database):


    {
        "id":"ew12-res2-234e-544f",
        "title":"post title",
        "date":"2016-01-01",
        "body":"this is an awesome post stored on NoSQL",
        "createdBy":User,
        "images":["http://myfirstimage.png","http://mysecondimage.png"],
        "videos":[
            {"url":"http://myfirstvideo.mp4", "title":"hello first video"},
            {"url":"http://mysecondvideo.mp4", "title":"hello second video"}
        ],
        "audios":[
            {"url":"http://myfirstaudio.mp3", "title":"hello first audio"},
            {"url":"http://mysecondaudio.mp3", "title":"hello second audio"}
        ]
    }

E può essere ottenuto con una singola query, senza l'uso di join. Questo è molto più semplice e lineare e, budget-wise, richiede meno risorse tooachieve risultati migliori.

DB Cosmos Azure garantisce che tutte le proprietà di hello vengono indicizzate con il relativo l'indicizzazione automatica, che può anche essere [personalizzato](indexing-policies.md). Hello privi di schema approccio consente di archiviare documenti con diversi e strutture dinamiche, forse domani che desideriamo toohave post consente di gestire un elenco di categorie o hashtag associate, Cosmos DB hello nuovi documenti con hello aggiunti gli attributi con senza aggiuntivi lavoro richiesto da Microsoft.

I commenti a un post possono essere considerati come altri post con una proprietà padre e questo semplifica il mapping degli oggetti. 

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":User2,
        "parent":"ew12-res2-234e-544f"
    }

    {
        "id":"asd2-fee4-23gc-jh67",
        "title":"Ditto!",
        "date":"2016-01-03",
        "createdBy":User3,
        "parent":"ew12-res2-234e-544f"
    }

Tutte le interazioni social possono essere archiviate in un oggetto separato come contatori:

    {
        "id":"dfe3-thf5-232s-dse4",
        "post":"ew12-res2-234e-544f",
        "comments":2,
        "likes":10,
        "points":200
    }

Per la creazione di feed è sufficiente creare documenti che possano contenere un elenco di ID post con un ordine di pertinenza specifico:

    [
        {"relevance":9, "post":"ew12-res2-234e-544f"},
        {"relevance":8, "post":"fer7-mnb6-fgh9-2344"},
        {"relevance":7, "post":"w34r-qeg6-ref6-8565"}
    ]

Con i post ordinati in base alla data di creazione di un flusso "più recente", "interessanti" flusso con quelli post con altre simili in hello ultime 24 ore, è anche possibile implementare un flusso personalizzato per ogni utente in base alla logica come anelli e interessi e sarebbe comunque un elenco di  post. Si tratta della modalità toobuild questi elenchi, ma le prestazioni di lettura hello rimangono senza problemi. Una volta che si acquisisce uno di questi elenchi, inviare tooCosmos una singola query DB utilizzando hello [nell'operatore](documentdb-sql-query.md#WhereClause) tooobtain pagine di invio alla volta.

Hello feed flussi può essere creata utilizzando [servizi App di Azure](https://azure.microsoft.com/services/app-service/) processi in background: [processi Web](../app-service-web/web-sites-create-web-jobs.md). Dopo aver creato un post, l'elaborazione in background può essere attivato utilizzando [di archiviazione di Azure](https://azure.microsoft.com/services/storage/) [code](../storage/queues/storage-dotnet-how-to-use-queues.md) e processi Web generati mediante hello [Azure Webjobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md), implementazione Hello post propagazione all'interno di flussi in base alle proprie logica personalizzata. 

Punti e così via in un post può essere elaborate in modo posticipato utilizzando questo stesso toocreate tecnica un ambiente alla fine coerente.

I follower sono più complessi. DB COSMOS ha un limite di dimensione massima del documento e lettura/scrittura di documenti di grandi dimensioni può influire sulla scalabilità hello dell'applicazione. È quindi consigliabile archiviare i follower come documento con questa struttura:

    {
        "id":"234d-sd23-rrf2-552d",
        "followersOf": "dse4-qwe2-ert4-aad2",
        "followers":[
            "ewr5-232d-tyrg-iuo2",
            "qejh-2345-sdf1-ytg5",
            //...
            "uie0-4tyg-3456-rwjh"
        ]
    }

Questa soluzione potrebbe funzionare per un utente con alcune migliaia anelli, ma se alcuni famoso unisce i ranghi, questo approccio comporta tooa dimensioni del documento di grandi dimensioni e potrebbe limitare la dimensione del documento hello infine hit.

toosolve, è possibile usare un approccio misto. Come parte del documento di hello statistiche relative agli utenti che è possibile archiviare il numero di hello di bisogno di seguenti:

    {
        "id":"234d-sd23-rrf2-552d",
        "user": "dse4-qwe2-ert4-aad2",
        "followers":55230,
        "totalPosts":452,
        "totalPoints":11342
    }

E può essere archiviato grafico effettivo di hello degli anelli tramite Azure Cosmos DB [API Graph Gremlin](../cosmos-db/graph-introduction.md), toocreate [vertici](http://mathworld.wolfram.com/GraphVertex.html) per ogni utente e [bordi](http://mathworld.wolfram.com/GraphEdge.html) che gestiscono hello " Relazioni segue-A-B". Hello API Graph consente non solo è ottenere anelli hello di un determinato utente ma creare query più complesse tooeven suggerire agli utenti in comune. Se si aggiunta hello grafico toohello categorie di contenuto che agli utenti come o usufruisci, è possibile avviare tessitura esperienze che includono smart individuazione dei contenuti, suggerendo contenuto rispetto a quelle si seguirà come o ricerca di persone con cui potremmo avere gran parte in comune.

documento di statistiche relative agli utenti di Hello può comunque essere utilizzati toocreate schede hello dell'interfaccia utente o le anteprime di profilo rapido.

## <a name="hello-ladder-pattern-and-data-duplication"></a>la duplicazione di modello e dati "Scala" Hello
Come si può notare nel documento JSON hello che fa riferimento a un post, sono presenti più occorrenze di un utente. E si sarebbe immaginare destra, che ciò significa che le informazioni di hello che rappresenta un utente, la denormalizzazione, potrebbero essere presenti in più di un'unica posizione.

In ordine tooallow per le query più veloce, si comportano la duplicazione dei dati. problema di Hello con questo effetto collaterale è che se per un'azione, le modifiche ai dati dell'utente, è necessario toofind tutte le attività di hello mai ha e aggiornarli tutti. Questo è un aspetto che va risolto.

È in corso toosolve, identificando hello gli attributi di chiave di un utente che illustrare nell'applicazione per ogni attività. Se si visivamente Mostra un post nell'applicazione e Mostra del solo hello creatore nome e immagine, motivo per cui archiviare tutti i dati dell'utente hello nell'attributo createdBy"hello"? Se per ogni commento è Mostra hello immagine utente, abbiamo bisogno rest hello le informazioni di. Che è in un elemento che chiamare hello "scala"modello entra in gioco.

Si prendano ad esempio le informazioni relative a un utente:

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "address":"742 Evergreen Terrace",
        "birthday":"1983-05-07",
        "email":"john@doe.com",
        "twitterHandle":"@john",
        "username":"johndoe",
        "password":"some_encrypted_phrase",
        "totalPoints":100,
        "totalPosts":24
    }

Esaminando queste informazioni è possibile distinguere rapidamente quelle più o meno critiche, creando così dei "gradini":

![Diagramma di un modello a gradini](./media/social-media-apps/social-media-apps-ladder.png)

passaggio più piccolo di Hello è definito un UserChunk, hello minimo informazione che identifica un utente e viene utilizzato per la duplicazione dei dati. Riducendo la dimensione hello delle informazioni sui hello tooonly dati hello duplicato è sarà "Mostra", si riduce il possibilità di hello degli aggiornamenti massicci.

passaggio intermedio Hello viene chiamato utente hello, è hello completa di dati che verrà usata nella maggior parte delle query basate sulle prestazioni su DB Cosmos, hello più critica e a cui si accede. Sono incluse informazioni hello rappresentate da un UserChunk.

Hello più grande è hello utente estesa. Include tutte le informazioni utente critici hello e altri dati che non richiedono rapidamente effettivamente toobe lettura o di utilizzo è finale (ad esempio, il processo di accesso di hello). Questi dati possono essere archiviati al di fuori di Cosmos DB, nel database SQL di Azure o nelle tabelle di archiviazione di Azure.

Perché si è suddiviso utente hello e anche archiviare queste informazioni in diverse posizioni? Poiché dal punto di vista delle prestazioni, hello documenti hello più grandi, hello costlier query hello. Mantenere i documenti sottile, con hello destra informazioni toodo tutte le prestazioni dipendente di una query per un social network e archivio hello altri informazioni aggiuntive per gli scenari di eventuali ad esempio, modifiche profilo completo, gli account di accesso, anche il data mining per analitica di utilizzo e Big Iniziative di dati. È davvero indifferente se hello la raccolta dati per il data mining sono più lenti, perché è in esecuzione nel Database SQL Azure, si hanno riguardano tuttavia che gli utenti abbiano un'esperienza veloce e sottile. Un utente archiviato in Cosmos DB si presenta come segue:

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "username":"johndoe"
        "email":"john@doe.com",
        "twitterHandle":"@john"
    }

Un post invece si presenta come segue:

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":{
            "id":"dse4-qwe2-ert4-aad2",
            "username":"johndoe"
        }
    }

E quando una modifica si verifica uno degli attributi di hello del blocco hello in cui è interessato, documenti hello interessato toofind semplice utilizzando le query che fanno riferimento gli attributi toohello indicizzata (selezionare * FROM post p WHERE p.createdBy.id = = "edited_user_id") e l'aggiornamento blocchi di Hello.

## <a name="hello-search-box"></a>casella di ricerca Hello
Gli utenti generano molti contenuti Si dovrebbe essere in grado di tooprovide hello possibilità toosearch e cercare il contenuto che potrebbe non essere direttamente nella loro flussi di contenuti, forse perché è non seguono gli autori di hello e forse si sta solo tentando toofind tale post precedente che abbiamo 6 mesi.

Fortunatamente, e poiché si sta usando Azure Cosmos DB, è possibile implementare facilmente un motore di ricerca mediante [ricerca di Azure](https://azure.microsoft.com/services/search/) in un paio di minuti e senza digitare una singola riga di codice (diverso da hello ovviamente, cercare processo e dell'interfaccia utente).

Perché è così semplice?

Ricerca di Azure implementa che chiamano [indicizzatori](https://msdn.microsoft.com/library/azure/dn946891.aspx), sfondo elabora tale hook nei repository dei dati e operazioni di aggiungere, aggiornare o rimuovere gli oggetti negli indici hello. Supportano gli [indicizzatori di database SQL di Azure](https://blogs.msdn.microsoft.com/kaevans/2015/03/06/indexing-azure-sql-database-with-azure-search/), gli [indicizzatori di BLOB di Azure](../search/search-howto-indexing-azure-blob-storage.md) e, soprattutto, gli [indicizzatori di Azure Cosmos DB](../search/search-howto-index-documentdb.md). Hello transizione di informazioni dal database Cosmos tooAzure ricerca è semplice, come entrambi archivia le informazioni in formato JSON, è sufficiente troppo[creare l'indice](../search/search-create-index-portal.md) ed eseguire il mapping di attributi quali i documenti si desideri indicizzare e questo è tutto, in pochi minuti (dipende dimensioni hello dei dati), tutti i contenuti saranno toobe disponibile al momento, la ricerca migliore soluzione ricerca-as-a-Service hello nell'infrastruttura cloud. 

Per ulteriori informazioni sulla ricerca di Azure, è possibile visitare hello [tooSearch Guida alla pagina Web contenente](https://blogs.msdn.microsoft.com/mvpawardprogram/2016/02/02/a-hitchhikers-guide-to-search/).

## <a name="hello-underlying-knowledge"></a>knowledge sottostante Hello
Dopo aver archiviato tutti questi contenuti che continuano ad aumentare, come è possibile mettere tutto questo flusso di informazioni al servizio degli utenti?

risposte Hello sono semplice: inserirlo toowork e imparare da esso.

Ad esempio, Alcuni esempi semplici includono [analisi del sentiment](https://en.wikipedia.org/wiki/Sentiment_analysis)contenuto indicazioni in base alle preferenze dell'utente o persino un automatizzati contenuto moderatore che assicura che tutti hello contenuto pubblicato per la rete social è sicuro per hello famiglia di caratteri.

Ora che è stato visualizzato è associato, è probabilmente proprio come se è necessario alcuni PhD in matematica scienza tooextract i modelli e informazioni dal database semplici e file, ma è errato.

[Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/), ma fa parte di hello [Cortana Intelligence Suite](https://www.microsoft.com/en/server-cloud/cortana-analytics-suite/overview.aspx), è un servizio cloud completamente gestito che consente di creare flussi di lavoro utilizzando gli algoritmi in una semplice interfaccia di trascinamento e rilascio, codice di algoritmi personalizzati di hello in [R](https://en.wikipedia.org/wiki/R_\(programming_language\)) o utilizzare alcune delle hello già creato e pronto toouse API, ad esempio: [testo Analitica](https://gallery.cortanaanalytics.com/MachineLearningAPI/Text-Analytics-2), [contenuto moderatore](https://www.microsoft.com/moderator) o [indicazioni](https://gallery.cortanaanalytics.com/MachineLearningAPI/Recommendations-2).

tooachieve qualsiasi di questi scenari di Machine Learning, è possibile utilizzare [Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) tooingest hello informazioni provenienti da origini diverse e utilizzare [U-SQL](https://azure.microsoft.com/documentation/videos/data-lake-u-sql-query-execution/) tooprocess hello informazioni e generare un output che possono essere elaborati da Azure Machine Learning.

Un'altra opzione disponibile è toouse [servizi cognitivi Microsoft](https://www.microsoft.com/cognitive-services) tooanalyze nostri utenti contenuti; non solo è possibile comprenderne meglio (tramite l'analisi con la scrittura [testo Analitica API](https://www.microsoft.com/cognitive-services/en-us/text-analytics-api)), ma è inoltre possibile rilevare il contenuto indesiderato o consolidato e agire di conseguenza con [Computer Vision API](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api). Servizi cognitivi includono molte soluzioni di casella che non richiedono alcun tipo di Machine Learning knowledge toouse.

## <a name="a-planet-scale-social-experience"></a>Un'esperienza social su scala globale
C'è un ultimo, ma non meno importante, argomento da affrontare: la **scalabilità**. Quando si progetta un'architettura che è molto importante che ogni componente adattabile autonomamente, sia perché sono necessari maggiori dati tooprocess o dal momento che toohave una copertura geografica più grande (o entrambe). Per fortuna, il raggiungimento di questo obiettivo così complesso si rivela un'**esperienza chiavi in mano** con Cosmos DB.

Supporta COSMOS DB [partizionamento dinamico](https://azure.microsoft.com/blog/10-things-to-know-about-documentdb-partitioned-collections/) out-of-the-box creando automaticamente partizioni in base a un determinato **chiave di partizione** (definito come uno degli attributi hello nei documenti). Definizione di hello corretto la chiave di partizione deve essere eseguita in fase di progettazione e mantenendo in hello presente [procedure consigliate](../cosmos-db/partition-data.md#designing-for-partitioning) disponibile; in caso di hello di un'esperienza sociale, la strategia di partizionamento deve essere allineata con la modalità di hello è eseguire una query (letture all'interno di hello stessa partizione sono auspicabile) e la scrittura (evitare "sensibili" distribuendo scritture in più partizioni). Alcune opzioni sono: partizioni in base a una chiave temporale (mese/giorno/settimana), in base alla categoria del contenuto, per area geografica, dall'utente. Tutto dipende effettivamente come eseguire query sui dati hello e visualizzarlo nella tua esperienza sociale. 

Uno spunto interessante la pena sottolineare è che DB Cosmos eseguirà le query (inclusi [aggregazioni](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)) in tutte le partizioni in modo trasparente, non è necessario tooadd qualsiasi logica alla crescita dei dati.

Con il tempo, aumenterà il traffico e di conseguenza aumenterà il consumo di risorse (misurato in [UR](request-units.md) o unità richiesta). Leggerà e scriverà più frequentemente come il userbase aumenta e avvierà la creazione e lettura del contenuto più; possibilità di Hello **la velocità effettiva di ridimensionamento** è essenziale. Aumentando il russo è molto semplice, è possibile farlo con pochi clic nel portale di Azure hello o [eseguono i comandi tramite hello API](https://docs.microsoft.com/rest/api/documentdb/replace-an-offer).

![Aumento delle prestazioni e definizione di una chiave di partizione](./media/social-media-apps/social-media-apps-scaling.png)

Poi le cose migliorano e gli utenti di un'altra area, paese o continente, notano la piattaforma e iniziano a usarla. Che magnifica sorpresa!

Attendere..., ma si appena nota alla propria esperienza con la piattaforma non ottimale; sono finora dalla propria area operativa latenza hello terribile, che sia ovviamente non si desidera tooquit. Ci vorrebbe un modo semplice per **estendere la portata globale** e infatti il modo esiste.

COSMOS DB consente di [replicare i dati a livello globale](../cosmos-db/tutorial-global-distribution-documentdb.md) e con un paio di clic e automaticamente in modo trasparente selezionare tra aree geografiche disponibili hello dal [codice client](../cosmos-db/tutorial-global-distribution-documentdb.md). Questo significa anche che è possibile avere [più aree di failover](regional-failover.md). 

Quando si replicano i dati a livello globale, è necessario assicurarsi che i client possono sfruttare il toomake. Se si utilizza un front-end web o le API di accesso da client mobili, è possibile distribuire [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) e clonare il servizio App di Azure su tutte le aree di hello desiderato, utilizzando un [configurazione prestazioni](../app-service-web/web-sites-traffic-manager.md)toosupport la copertura globale estesa. Quando i client di accedono al server front-end o all'API, sarà indirizzato toohello più vicino servizio App, che a sua volta, si connetterà toohello locale Cosmos DB replica.

![Aggiunta della piattaforma social tooyour copertura globale](./media/social-media-apps/social-media-apps-global-replicate.png)

## <a name="conclusion"></a>Conclusioni
In questo articolo tenta tooshed alcuni chiaro in alternative hello della creazione di social network completamente in Azure con i servizi di basso costo e fornendo risultati eccezionali usando incoraggianti hello una distribuzione di soluzioni e i dati a più livelli di archiviazione denominata "Scala".

![Diagramma di interazione tra servizi di Azure per il social networking](./media/social-media-apps/social-media-apps-azure-solution.png)

verità Hello è che non esiste alcun alcuni limiti specifici per questo tipo di scenari, ha hello sinergia creata da una combinazione di hello di grandi servizi che consentono di esperienze all'avanguardia toobuild: hello velocità e la libertà di Azure Cosmos DB tooprovide un'applicazione di social networking ottima, intelligence Hello dietro una soluzione di prima classe ricerca come ricerca di Azure, la flessibilità di hello di servizi di App di Azure toohost non anche le applicazioni indipendenti dal linguaggio ma i processi in background potenti e hello espandibile archiviazione di Azure e Database SQL di Azure per l'archiviazione di grandi quantità di dati e hello potenza analitica di Azure Machine Learning toocreate conoscenze e business intelligence che è possibile fornire commenti e suggerimenti tooour processi e contribuire a garantire hello toohello destra contenuto destra agli utenti.

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni sui casi di utilizzo per Cosmos DB, vedere [casi d'uso comuni Cosmos DB](use-cases.md).
