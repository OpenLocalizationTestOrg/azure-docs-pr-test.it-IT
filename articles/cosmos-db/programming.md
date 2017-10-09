---
title: programmazione JavaScript sul lato aaaServer per Azure Cosmos DB | Documenti Microsoft
description: Informazioni su come toouse Azure Cosmos DB toowrite stored procedure, trigger di database e funzioni definite dall'utente (UDF) in JavaScript. Ottenere suggerimenti sulla programmazione di database e altro ancora.
keywords: Trigger di database, stored procedure, programma di database, sproc, documentdb, azure, Microsoft Azure
services: cosmos-db
documentationcenter: 
author: aliuy
manager: jhubbard
editor: mimig
ms.assetid: 0fba7ebd-a4fc-4253-a786-97f1354fbf17
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: andrl
ms.openlocfilehash: 5a011d1c4b0b5908d5de73607a1bc328ed1711d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a>Programmazione lato server per Azure Cosmos DB: stored procedure, trigger del database e funzioni definite dall'utente
L'esecuzione integrata e transazionale di JavaScript con il linguaggio di Azure Cosmos DB permette agli sviluppatori di scrivere **stored procedure**, **trigger** e **funzioni definite dall'utente** in modo nativo in [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript. In questo modo toowrite database programma logica dell'applicazione che può essere inviata e può essere eseguita direttamente sulle partizioni di archiviazione di database hello. 

È consigliabile ottenere avviata da hello guardando seguente video, in cui Andrew Liu fornisce tooCosmos una breve introduzione del database modello di programmazione sul lato server database. 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

Tornare quindi toothis articolo, in cui si apprenderà toohello risposte hello seguenti domande:  

* Come è possibile scrivere una stored procedure, un trigger o una funzione definita dall'utente usando JavaScript?
* In che modo Cosmos DB garantisce proprietà ACID?
* Come funzionano le transazioni in Cosmos DB?
* Cosa sono i pre-trigger e i post-trigger e come si scrivono?
* Come si registra e si esegue una stored procedure, un trigger o una funzione definita dall'utente in modalità RESTful usando HTTP?
* Quali sono disponibili toocreate Cosmos DB SDK ed eseguire stored procedure, trigger e funzioni definite dall'utente?

## <a name="introduction-toostored-procedure-and-udf-programming"></a>Introduzione tooStored Procedure e funzioni definite dall'utente per la programmazione
Questo approccio di *"JavaScript come una moderna T-SQL"* consente agli sviluppatori di applicazioni di complessità hello di sistema di tipi non corrispondenti e le tecnologie di mapping relazionale a oggetti. Include inoltre una serie di vantaggi intrinseci che possono essere utilizzati toobuild applicazioni:  

* **Logica procedurale:** JavaScript come un linguaggio di programmazione di alto livello, fornisce un tooexpress un'interfaccia familiare e rich logica di business. È possibile eseguire complesse sequenze più vicino toohello dei dati delle operazioni.
* **Transazioni atomiche:** Cosmos DB garantisce che le operazioni di database all'interno di una singola stored procedure o un trigger siano atomiche. Di conseguenza, un'applicazione potrà combinare le operazioni correlate in un unico batch, in modo che o tutte o nessuna di esse avranno esito positivo. 
* **Prestazioni:** fatti hello che JSON è intrinsecamente mappato toohello Javascript language tipo sistema ed è anche unità di archiviazione nel database Cosmos base hello consente un numero di ottimizzazioni come lazy materializzazione di JSON documenti nel buffer hello pool e renderli disponibili su richiesta toohello, l'esecuzione del codice. Sono disponibili ulteriori vantaggi di prestazioni associati shipping database toohello logica di business:
  
  * Invio in batch: gli sviluppatori possono raggruppare le operazioni, come gli inserimenti, e inviarle in blocco. costo di latenza di traffico di rete Hello e transazioni separate di hello archivio toocreate overhead vengono ridotti in modo significativo. 
  * Pre-compilazione: consente di precompilare Cosmos DB stored procedure, trigger e definiti dall'utente le funzioni definite dal tooavoid JavaScript costo di compilazione per ogni chiamata. Hello overhead per la generazione di codice a un byte hello per logica procedurale hello è ammortizzato tooa di valore minimo.
  * Sequenziazione: molte operazioni necessitano di un effetto collaterale ("trigger") che implica potenzialmente l'esecuzione di una o più operazioni di archiviazione secondarie. A parte l'atomicità, questo è più efficiente quando spostato toohello server. 
* **Incapsulamento:** Stored procedure possono essere utilizzato toogroup logica di business in un'unica posizione. Ciò comporta due vantaggi:
  * Aggiunge un livello di astrazione su dati non elaborati hello, che consente di applicazioni in modo indipendente da dati hello tooevolve architetti di dati. Ciò è particolarmente utile quando i dati di hello sono senza schema, a causa di ipotesi fragile toohello che potrebbe essere necessario toobe baked in un'applicazione hello se hanno toodeal con i dati direttamente.  
  * Questa astrazione consente alle aziende di proteggere i propri dati grazie alla semplificazione di accesso di hello dagli script hello.  

Hello creazione ed esecuzione di trigger di database, stored procedure e gli operatori di query personalizzata è supportata tramite hello [API REST](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), e [client SDK](documentdb-sdk-dotnet.md) in molte piattaforme, tra cui .NET, Node.js e JavaScript.

Questa esercitazione viene utilizzato hello [Node.js SDK con domande e](http://azure.github.io/azure-documentdb-node-q/) tooillustrate sintassi e l'utilizzo di stored procedure, trigger e funzioni definite dall'utente.   

## <a name="stored-procedures"></a>Stored procedure
### <a name="example-write-a-simple-stored-procedure"></a>Esempio: scrivere una stored procedure semplice
Per cominciare, si analizzerà una semplice stored procedure che restituisce una risposta "Hello World".

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


Le stored procedure vengono registrate per ogni raccolta e funzionano in qualsiasi documento e allegato presente nella raccolta. Hello frammento di codice seguente viene illustrato come tooregister hello helloWorld stored procedure con una raccolta. 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


Una volta registrata procedure hello archiviato, è possibile eseguirla insieme hello e leggere i risultati al client hello hello. 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


oggetto di contesto Hello fornisce l'accesso tooall operazioni che possono essere eseguite su archiviazione Cosmos DB, nonché accedere agli oggetti di richiesta e risposta toohello. In questo caso, abbiamo utilizzato hello oggetto tooset hello corpo della risposta di risposta hello client toohello indietro è stato inviato. Per ulteriori informazioni, vedere toohello [server Azure Cosmos DB JavaScript documentazione SDK](http://azure.github.io/azure-documentdb-js-server/).  

Espandere questo esempio segnalare il problema e aggiungere altre funzionalità correlate del database toohello stored procedure. Stored procedure possono creare, aggiornare, leggere, eseguire una query ed eliminare documenti e gli allegati all'interno di hello.    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a>Esempio: Scrivere una stored procedure toocreate un documento
frammento di codice Hello successivo mostra come toouse hello toointeract oggetto di contesto con risorse DB Cosmos.

    var createDocumentStoredProc = {
        id: "createMyDocument",
        serverScript: function createMyDocument(documentToCreate) {
            var context = getContext();
            var collection = context.getCollection();

            var accepted = collection.createDocument(collection.getSelfLink(),
                  documentToCreate,
                  function (err, documentCreated) {
                      if (err) throw new Error('Error' + err.message);
                      context.getResponse().setBody(documentCreated.id)
                  });
            if (!accepted) return;
        }
    }


Questa stored procedure accetta come input documentToCreate, corpo hello di toobe un documento creato nella raccolta corrente hello. Tutte queste operazioni sono asincrone e dipendono dai callback della funzione JavaScript. funzione di callback Hello ha due parametri, uno per l'oggetto errore hello nel caso in cui hello operazione ha esito negativo e uno per hello creato l'oggetto. All'interno di callback hello, gli utenti possono gestire hello eccezione o viene generato un errore. Nel caso in cui non è stato specificato un callback e si verifica un errore, hello Azure Cosmos DB runtime genera un errore.   

Nell'esempio hello sopra, il callback di hello genera un errore se hello operazione non riuscita. In caso contrario, imposta id hello di hello creato documento come corpo hello del client di toohello risposta hello. Ecco come viene eseguita questa stored procedure con i parametri di input.

    // register hello stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure toocreate a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "hello Hitchhiker’s Guide toohello Galaxy",
                author: "Douglas Adams"
            };

            return client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/createMyDocument',
                  docToCreate);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response); // "DocFromSproc"
    }, function (error) {
        console.log("Error", error);
    });


Si noti che questa stored procedure possono essere modificato tootake una matrice di corpi di documento come input e crearli in hello stesso archiviato esecuzione della procedura anziché una rete più richieste toocreate di essi singolarmente. Può essere utilizzato tooimplement un'unità di importazione bulk sia efficiente per DB Cosmos (descritto più avanti in questa esercitazione).   

esempio Hello descritto dimostrato come toouse stored procedure. I trigger e funzioni definite dall'utente (UDF) verranno illustrate più avanti nell'esercitazione di hello.

## <a name="database-program-transactions"></a>Transazioni del programma del database
Una transazione in un tipico database può essere definita come una sequenza di operazioni eseguite come singola unità di lavoro logica. Ogni transazione offre **garanzie ACID**. ACID è un acronimo noto che riassume quattro proprietà: Atomicità, Coerenza, Isolamento e Durabilità.  

In breve, l'atomicità assicura che tutto il lavoro hello eseguito all'interno di una transazione viene considerato come una singola unità in cui entrambi tutti i relativi viene eseguito il commit o nessuno. Coerenza assicura che i dati di hello sono sempre in buono stato interno tra le transazioni. Isolamento in modo che le due transazioni non interferiscono tra loro, in genere, la maggior parte dei sistemi forniscono più livelli di isolamento che possono essere utilizzati in base ai requisiti dell'applicazione hello. Durabilità assicura che qualsiasi modifica che viene eseguito il commit nel database di hello sarà sempre presenta.   

In DB Cosmos, JavaScript è ospitato in hello database hello stesso spazio di memoria. Di conseguenza, le richieste effettuate all'interno di stored procedure e trigger è eseguite in hello stesso ambito di una sessione di database. In questo modo Cosmos DB tooguarantee ACID per tutte le operazioni che fanno parte di un singolo stored procedure o trigger. Si consideri il seguente hello archiviati definizione della stored procedure:

    // JavaScript source code
    var exchangeItemsSproc = {
        id: "exchangeItems",
        serverScript: function (playerId1, playerId2) {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            var player1Document, player2Document;

            // query for players
            var filterQuery = 'SELECT * FROM Players p where p.id  = "' + playerId1 + '"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery, {},
                function (err, documents, responseOptions) {
                    if (err) throw new Error("Error" + err.message);

                    if (documents.length != 1) throw "Unable toofind both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable toofind both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable tooread player details, abort ";
                });

            if (!accept) throw "Unable tooread player details, abort ";

            // swap hello two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable tooupdate player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable tooupdate player 2, abort"
                            });

                        if (!accept2) throw "Unable tooupdate player 2, abort";
                    });

                if (!accept) throw "Unable tooupdate player 1, abort";
            }
        }
    }

    // register hello stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

Questa stored procedure utilizza transazioni all'interno di elementi di tootrade app un gioco tra due giocatori in un'unica operazione. Hello stored procedure tentativi tooread due documenti che ogni player toohello corrispondente di ID passato come argomento. Se vengono trovati entrambi i documenti Windows Media player, quindi hello stored procedura consente di aggiornare documenti hello scambiando gli elementi. Se vengono rilevati errori durante il processo di hello, verrà generata un'eccezione JavaScript che la transazione hello si interrompe in modo implicito.

Se hello procedure hello archiviato insieme è registrata in è una raccolta unica partizione, sarà hello transazione documenti hello tooall con ambito raccolta hello. Se la raccolta hello è partizionata, stored procedure vengono eseguite nell'ambito di transazione hello di una chiave singola partizione. Ogni stored esecuzione di stored procedure deve quindi includere un valore di chiave di partizione della transazione hello ambito toohello corrispondente deve essere eseguito con. Per altri dettagli, vedere l'articolo relativo al [partizionamento di Azure Cosmos DB](partition-data.md).

### <a name="commit-and-rollback"></a>Commit e rollback
Le transazioni sono integrate in maniera approfondita e nativa nel modello di programmazione JavaScript di Cosmos DB. All'interno di una funzione JavaScript, viene eseguito il wrapping di tutte le operazioni in un'unica transazione. Se hello JavaScript viene completata senza alcuna eccezione, il database toohello operations Manager hello viene eseguito il commit. In effetti, le istruzioni "BEGIN TRANSACTION" e "Eseguire il COMMIT della transazione" hello nei database relazionali sono implicite nel DB Cosmos.  

Se è presente qualsiasi eccezione che viene propagato da script hello, il runtime di JavaScript Cosmos DB eseguirà il rollback dell'intera transazione hello. Come illustrato in precedenza in hello esempio, generare un'eccezione è tooa equivale "ROLLBACK TRANSACTION" DB Cosmos.

### <a name="data-consistency"></a>Coerenza dei dati
Stored procedure e trigger vengono sempre eseguiti sulla replica primaria di hello del contenitore di Azure Cosmos DB hello. In tal modo si garantisce la coerenza assoluta delle letture all'interno delle stored procedure. Le query che utilizzano funzioni definite dall'utente possono essere eseguite su hello primaria o una qualsiasi replica secondaria, ma è garantire toomeet hello richiesto livello di coerenza scegliendo replica appropriata hello.

## <a name="bounded-execution"></a>Esecuzione vincolata
Tutte le operazioni DB Cosmos devono essere completata entro server hello specificato richiesta la durata del timeout. Questo vincolo si applica anche funzioni tooJavaScript (stored procedure, trigger e funzioni definite dall'utente). Se un'operazione non viene completato con tale limite, viene eseguito il rollback delle transazioni hello. Le funzioni JavaScript devono terminare entro il limite di tempo hello o implementare una continuazione in base modellare toobatch o ripresa l'esecuzione.  

In ordine toosimplify lo sviluppo di stored procedure e trigger toohandle termini, tutte le funzioni nell'oggetto raccolta hello (per creare, leggere, sostituire e l'eliminazione di documenti e allegati) restituiscono un valore booleano che rappresenta se che verrà completata l'operazione. Se questo valore è false, è un'indicazione che il limite di tempo hello sta tooexpire e tale procedura hello deve eseguire il wrapping di esecuzione.  Operazioni in coda toohello precedente prima archivio non accettato operazione sono consentite toocomplete se procedure hello archiviato viene completato in tempo e non mette in coda a tutte le altre richieste.  

Anche le funzioni JavaScript sono vincolate al consumo di risorse. COSMOS DB riserva velocità effettiva per ogni raccolta in base alle dimensioni di hello il provisioning di un account di database. La velocità effettiva viene espressa in termini di un'unità normalizzata di consumo CPU, memoria e IO, denominata unità di richiesta, o RU. Le funzioni JavaScript possono comportare l'utilizzo di un numero elevato di unità riservate all'interno di un breve periodo di tempo e potrebbero ottenere frequenza limitata se viene raggiunto il limite dell'insieme di hello. Stored procedure con utilizzo intensivo risorsa potrebbero inoltre essere messi in quarantena tooensure disponibilità delle operazioni di database primitivo.  

### <a name="example-bulk-importing-data-into-a-database-program"></a>Esempio: importazione in blocco dei dati in un programma di database
Di seguito è riportato un esempio di una stored procedure che viene scritto toobulk-importazione di documenti in una raccolta. Si noti come hello esecuzione di stored procedure handle delimitati controllando hello Boolean restituito da createDocument e quindi utilizza hello conteggio dei documenti inseriti in ogni chiamata di hello stored procedure tootrack e riprendere lo stato di avanzamento in batch.

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // hello count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("hello array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call hello create API toocreate a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) hello createDocument request was not accepted. 
        //    In this case hello callback will not be called, we just call setBody and we are done.
        // 2) hello callback was called docs.length times.
        //    In this case all documents were created and we don’t need toocall tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If hello request was accepted, callback will be called.
            // Otherwise report current count back toohello client, 
            // which will call hello script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order tooprocess hello result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment hello count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set hello response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <a id="trigger"></a> Trigger del database
### <a name="database-pre-triggers"></a>Pre-trigger del database
Cosmos DB include trigger che vengono eseguiti o attivati da un'operazione su un documento. Ad esempio, è possibile specificare un pre-trigger quando si crea un documento, pre-trigger verrà eseguito prima che venga creato il documento hello. Hello Ecco un esempio di come pre-trigger può essere utilizzato toovalidate hello proprietà di un documento che viene creato:

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document toobe created in hello current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update hello document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


E hello corrispondente codice di registrazione client-side Node.js per trigger hello:

    // register pre-trigger
    client.createTriggerAsync(collection.self, validateDocumentContentsTrigger)
        .then(function (response) {
            console.log("Created", response.resource);
            var docToCreate = {
                id: "DocWithTrigger",
                event: "Error",
                source: "Network outage"
            };

            // run trigger while creating above document 
            var options = { preTriggerInclude: "validateDocumentContents" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response.resource); // document with timestamp property added
    }, function (error) {
        console.log("Error", error);
    });


I pre-trigger non possono avere parametri di input. oggetto richiesta Hello può essere utilizzato toomanipulate messaggio di richiesta di hello associato all'operazione hello. In questo caso, pre-trigger di hello è in esecuzione con creazione hello di un documento e corpo del messaggio di richiesta di hello contiene toobe documento hello creato in formato JSON.   

Quando i trigger vengono registrati, gli utenti possono specificare le operazioni eseguibili con hello. Questo trigger è stato creato con TriggerOperation.Create, ovvero seguente hello non è consentito.

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a>Post-trigger del database
I post-trigger, come i pre-trigger, sono associati a un'operazione su un documento e non accettano parametri di input. Vengono eseguiti **dopo** hello operazione è stata completata e hanno accesso toohello risposta messaggio che viene inviato toohello client.   

Hello di esempio seguente mostra i post-trigger in azione:

    var updateMetadataTrigger = {
        id: "updateMetadata",
        serverScript: function updateMetadata() {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            // document that was created
            var createdDocument = response.getBody();

            // query for metadata document
            var filterQuery = 'SELECT * FROM root r WHERE r.id = "_metadata"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery,
                updateMetadataCallback);
            if(!accept) throw "Unable tooupdate metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable toofind metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable tooupdate metadata, abort";
                               });
                         if(!accept) throw "Unable tooupdate metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


trigger Hello possono essere registrati come illustrato nel seguente esempio hello.

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "hello Band",
                albums: ["Hellujah", "Rotators", "Spinning Top"]
            };

            // run trigger while creating above document 
            var options = { postTriggerInclude: "updateMetadata" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });


Trigger di una query per il documento di metadati hello e viene aggiornato con i dettagli sul documento hello appena creato.  

Un aspetto importante toonote hello **transazionale** esecuzione dei trigger nel database Cosmos. Questo post-trigger viene eseguito come parte di hello creazione hello del documento originale hello stessa transazione. Pertanto, se viene generata un'eccezione da un post-trigger di hello (ad esempio se il canale è documento di metadati non è possibile tooupdate hello), dell'intera transazione hello avrà esito negativo e il rollback. Non verrà creato alcun documento e verrà restituita un'eccezione.  

## <a id="udf"></a>Funzioni definite dall'utente
Funzioni definite dall'utente (UDF) sono grammatica del linguaggio query SQL API DocumentDB hello tooextend utilizzata e implementano la logica di business personalizzata. Possono essere richiamate solo dall'interno delle query. Non dispongono di oggetto di contesto di accesso toohello ma sono concepite toobe utilizzato come JavaScript di solo calcolo. Pertanto, è possibile eseguire funzioni definite dall'utente nelle repliche secondarie di hello servizio DB Cosmos.  

Hello esempio seguente viene creata una funzione definita dall'utente toocalculate reddito in base alle tariffe per parentesi quadre reddito diversi e viene utilizzata all'interno di una query toofind tutti gli utenti a pagamento di più di 20.000 $ imposte.

    var taxUdf = {
        id: "tax",
        serverScript: function tax(income) {

            if(income == undefined) 
                throw 'no input';

            if (income < 1000) 
                return income * 0.1;
            else if (income < 10000) 
                return income * 0.2;
            else
                return income * 0.4;
        }
    }


Hello funzione definita dall'utente può essere usato in seguito nelle query, come nel seguente esempio hello:

    // register UDF
    client.createUserDefinedFunctionAsync('dbs/testdb/colls/testColl', taxUdf)
        .then(function(response) { 
            console.log("Created", response.resource);

            var query = 'SELECT * FROM TaxPayers t WHERE udf.tax(t.income) > 20000'; 
            return client.queryDocuments('dbs/testdb/colls/testColl',
                   query).toArrayAsync();
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        var documents = response.feed;
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });

## <a name="javascript-language-integrated-query-api"></a>API della Language-Integrated Query di JavaScript
Query tooissuing utilizzando la grammatica SQL di DocumentDB, hello SDK lato server consente inoltre tooperform con ottimizzazione per la query utilizzando un'interfaccia intuitiva di JavaScript senza la conoscenza di SQL. query di JavaScript Hello che API consente query compilazione tooprogrammatically passando le funzioni di predicato in funzione concatenabile chiama, con un tooECMAScript5 familiare sintassi incorporati di matrice e librerie JavaScript più diffuse come lodash. Le query vengono analizzate dal hello JavaScript runtime toobe eseguiti in modo efficiente con gli indici del database di Azure Cosmos.

> [!NOTE]
> `__`(doppio carattere di sottolineatura) è un alias troppo`getContext().getCollection()`.
> <br/>
> In altre parole, è possibile utilizzare `__` o `getContext().getCollection()` tooaccess hello API query JavaScript.
> 
> 

Tra le funzioni supportate:

<ul>
<li>
<b>chain() ... .value([callback] [, options])</b>
<ul>
<li>
Avvia una chiamata concatenata che deve terminare con value().
</li>
</ul>
</li>
<li>
<b>filter(predicateFunction [, options] [, callback])</b>
<ul>
<li>
I filtri di input utilizzando una funzione di predicato restituisce true o false in ordine toofilter documenti di input in/out nel set risultante hello hello. Questo comportamento è simile tooa clausola WHERE in SQL.
</li>
</ul>
</li>
<li>
<b>map(transformationFunction [, options] [, callback])</b>
<ul>
<li>
Si applica una proiezione di una funzione di trasformazione che esegue il mapping di ogni oggetto JavaScript tooa di elemento di input o il valore specificata. Questo comportamento è simile tooa di clausola SELECT in SQL.
</li>
</ul>
</li>
<li>
<b>pluck([propertyName] [, options] [, callback])</b>
<ul>
<li>
Si tratta di un collegamento per una mappa che estrae il valore di hello di una singola proprietà di ogni elemento di input.
</li>
</ul>
</li>
<li>
<b>flatten([isShallow] [, options] [, callback])</b>
<ul>
<li>
Combina e appiattisce matrici da ogni elemento di input in tooa singola matrice. Questo comportamento tooSelectMany simili nelle query LINQ.
</li>
</ul>
</li>
<li>
<b>sortBy([predicate] [, options] [, callback])</b>
<ul>
<li>
Generare un nuovo set di documenti quando si ordinano i documenti hello nel flusso di input documento hello in ordine crescente utilizzando hello predicato specificato. Questo comportamento è simile tooa clausola ORDER BY in SQL.
</li>
</ul>
</li>
<li>
<b>sortByDescending([predicate] [, options] [, callback])</b>
<ul>
<li>
Generare un nuovo set di documenti quando si ordinano i documenti hello nel flusso di input documento hello in ordine decrescente utilizzando hello predicato specificato. Il funzionamento è simile clausola ORDER BY x DESC tooa SQL.
</li>
</ul>
</li>
</ul>


Quando incluso all'interno delle funzioni di predicato e/o selettore, hello seguenti costrutti JavaScript ottengono automaticamente ottimizzato toorun direttamente nel database di Azure Cosmos indici:

* Operatori semplici: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;! ~
* Valori letterali, inclusi valore letterale di oggetto hello: {}
* var, return

Hello JavaScript seguente costruisce non ottenere ottimizzata per gli indici di database Cosmos Azure:

* Flusso di controllo (ad esempio, se, per, mentre)
* Chiamate di funzione

Per ulteriori informazioni, vedere [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a>Esempio: Scrivere una stored procedure utilizzando l'API di query hello JavaScript
Hello nell'esempio di codice seguente è riportato un esempio di come utilizzare JavaScript Query API hello nel contesto di hello di una stored procedure. Inserisce un documento, fornito dal parametro di input, Hello stored procedure e aggiorna un documento di metadati utilizzando hello `__.filter()` metodo, con minSize, maxSize e totalSize in base alla proprietà di dimensioni del documento input hello.

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent tooour callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check hello doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get hello meta document. We keep it in hello same collection. it's hello only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed toofind hello metadata document.");

            // hello metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all hello rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace hello metadata document in hello store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read hello meta again 
              //       and update again because due tooSnapshot isolation we will read same exact version (we are in same transaction).
              //       We have tootake care of that on hello client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-toojavascript-cheat-sheet"></a>Foglio informativo tooJavascript SQL
Hello tabella seguente vengono illustrate diverse query JavaScript corrispondente hello e query SQL.

Come le query SQL, le chiavi di proprietà del documento (ad esempio `doc.id`) fanno distinzione tra maiuscole e minuscole.

|SQL| API di query JavaScript|Descrizione sotto|
|---|---|---|
|SELECT *<br>FROM docs| __.map(function(doc) { <br>&nbsp;&nbsp;&nbsp;&nbsp;return doc;<br>});|1|
|SELECT docs.id, docs.message AS msg, docs.actions <br>FROM docs|__.map(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;id: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;msg: doc.message,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;actions:doc.actions<br>&nbsp;&nbsp;&nbsp;&nbsp;};<br>});|2|
|SELECT *<br>FROM docs<br>WHERE docs.id="X998_Y998"|__.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";<br>});|3|
|SELECT *<br>FROM docs<br>WHERE ARRAY_CONTAINS(docs.Tags, 123)|__.filter(function(x) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;<br>});|4|
|SELECT docs.id, docs.message AS msg<br>FROM docs<br>WHERE docs.id="X998_Y998"|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;id: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;msg: doc.message<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>.value();|5|
|SELECT VALUE tag<br>FROM docs<br>JOIN tag IN docs.Tags<br>ORDER BY docs._ts|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return doc.Tags &amp;&amp; Array.isArray(doc.Tags);<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")<br>&nbsp;&nbsp;&nbsp;&nbsp;.flatten()<br>&nbsp;&nbsp;&nbsp;&nbsp;.value()|6|

Hello descrizioni riportate di seguito viene illustrato ogni query della tabella hello precedente.
1. Viene restituita così com'è in tutti i documenti, impaginati con token di continuazione.
2. Progetti hello id, il messaggio (alias toomsg) e azione da tutti i documenti.
3. Le query per i documenti con un predicato hello: id = "X998_Y998".
4. Le query per i documenti che presentano una proprietà di tag e tag è una matrice che contiene il valore di hello 123.
5. Le query per i documenti con un predicato, id = "X998_Y998" e id di hello quindi progetti e dei messaggi (toomsg alias).
6. I filtri per i documenti che hanno una proprietà di matrice, tag, e documenti risultanti hello vengono ordinati in proprietà sistema del timestamp hello TS e quindi proiettato + appiattisce la matrice di tag hello.


## <a name="runtime-support"></a>Supporto di runtime
[API sul lato server di DocumentDB JavaScript](http://azure.github.io/azure-documentdb-js-server/) fornisce il supporto per hello la maggior parte delle hello mainstream funzionalità del linguaggio JavaScript come standard da [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).

### <a name="security"></a>Sicurezza
JavaScript stored procedure e trigger vengono create mediante sandbox in modo che gli effetti di hello di uno script non modificati non perdono toohello altri senza passare attraverso l'isolamento delle transazioni snapshot di hello a livello di database hello. gli ambienti di runtime Hello sono in pool ma puliti del contesto di hello dopo ogni esecuzione. Sono pertanto sono sicuramente toobe provvisoria di tutti gli effetti collaterali non intenzionali tra loro.

### <a name="pre-compilation"></a>Precompilazione
Stored procedure, trigger e funzioni definite dall'utente sono formato di codice in modo implicito precompilata toohello byte nel costo di compilazione tooavoid ordine in fase di hello di ogni chiamata dello script. Questo garantisce la velocità elevata e il footprint ridotto delle chiamate delle stored procedure.

## <a name="client-sdk-support"></a>Supporto di client SDK
In aggiunta toohello API DocumentDB per [Node.js](documentdb-sdk-node.md) dispone di client, Azure Cosmos DB [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), e [Python SDK](documentdb-sdk-python.md) per hello API DocumentDB. È possibile creare ed eseguire stored procedure, trigger e UDFs usando anche uno qualsiasi di questi SDK. Hello seguente esempio viene illustrato come toocreate ed eseguire una stored procedure utilizzando client .NET hello. Si noti come tipi .NET hello vengono passati in hello stored procedure come JSON e leggere nuovamente.

    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    

                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }

                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };

    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;

    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "sproc"), document, 1920);


Questo esempio viene illustrato come hello toouse [API .NET di DocumentDB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate pre-trigger e creare un documento con trigger hello abilitato. 

    Trigger preTrigger = new Trigger()
    {
        Id = "CapitalizeName",
        Body = @"function() {
            var item = getContext().getRequest().getBody();
            item.id = item.id.toUpperCase();
            getContext().getRequest().setBody(item);
        }",
        TriggerOperation = TriggerOperation.Create,
        TriggerType = TriggerType.Pre
    };

    Document createdItem = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), new Document { Id = "documentdb" },
        new RequestOptions
        {
            PreTriggerInclude = new List<string> { "CapitalizeName" },
        });


E hello di esempio seguente viene illustrato come toocreate un utente definito (dall'utente UDF) (funzione) e utilizzarla in un [query SQL API DocumentDB](documentdb-sql-query.md).

    UserDefinedFunction function = new UserDefinedFunction()
    {
        Id = "LOWER",
        Body = @"function(input) 
        {
            return input.toLowerCase();
        }"
    };

    foreach (Book book in client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        "SELECT * FROM Books b WHERE udf.LOWER(b.Title) = 'war and peace'"))
    {
        Console.WriteLine("Read {0} from query", book);
    }

## <a name="rest-api"></a>API REST
Tutte le operazioni di Azure Cosmos DB possono essere eseguite in modalità RESTful. È possibile registrare stored procedure, trigger e funzioni definite dall'utente in una raccolta usando il verbo HTTP POST. Hello seguito è riportato un esempio di come tooregister una stored procedure:

    POST https://<url>/sprocs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT


    var x = {
      "name": "createAndAddProperty",
      "body": function (docToCreate, addedPropertyName, addedPropertyValue) {
                var collectionManager = getContext().getCollection();
                collectionManager.createDocument(
                    collectionManager.getSelfLink(),
                    docToCreate,
                    function(err, docCreated) {
                      if(err) throw new Error('Error:  ' + err.message);
                      docCreated[addedPropertyName] = addedPropertyValue;
                      getContext().getResponse().setBody(docCreated);
                    });
            }
    }


Hello stored procedure è registrata tramite l'esecuzione di una richiesta POST hello URI dbs/testdb/colls/testColl/stored procedure con hello corpo contenente hello toocreate stored procedure. Trigger e funzioni definite dall'utente possono essere registrati in modo analogo eseguendo una richiesta POST rispettivamente su /triggers e /udfs.
Questa stored procedure può quindi essere eseguita tramite una richiesta POST sul relativo collegamento alle risorse:

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


In questo caso, procedure toohello input archiviato hello viene passata nel corpo della richiesta hello. Si noti che hello input viene passato come matrice JSON dei parametri di input. Hello stored procedure accetta hello primo input di un documento che è un corpo della risposta. è stata ricevuta risposta di Hello è indicato di seguito:

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of hello Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


A differenza delle stored procedure, non è possibile eseguire direttamente i trigger, che vengono però eseguiti come parte di un'operazione o di un documento. È possibile specificare hello trigger toorun con una richiesta utilizzando le intestazioni HTTP. di seguito Hello è richiesta toocreate un documento.

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “hello Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


Qui toobe pre-trigger hello eseguire con richiesta di hello viene specificato nell'intestazione x-ms-documentdb-pre-trigger-include hello. Di conseguenza, qualsiasi post-trigger figurano nell'intestazione x-ms-documentdb-post-trigger-include hello. Notare che è possibile specificare sia pre-trigger sia post-trigger per una determinata richiesta.

## <a name="sample-code"></a>Codice di esempio
Per trovare altri esempi di codice sul lato server, inclusi esempi relativi all'[eliminazione in blocco](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) e all'[aggiornamento](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js), vedere l'[archivio GitHub](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).

Desidera tooshare straordinaria stored procedure? Inviare una richiesta di pull! 

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato uno o più stored procedure, trigger e funzioni definite dall'utente create, è possibile caricarli e visualizzarli nel portale di Azure utilizzando Esplora dati hello.

È inoltre possibile trovare il seguente hello riferimenti e risorse utili per il percorso toolearn ulteriori informazioni sulla programmazione sul lato server dB Cosmos Azure:

* [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md)
* [DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases)
* [JSON](http://www.json.org/) 
* [JavaScript ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [Estensibilità di Database protette e portatile](http://dl.acm.org/citation.cfm?id=276339) 
* [Database architettura orientata ai servizi](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [Hosting hello .NET Runtime in Microsoft SQL server](http://dl.acm.org/citation.cfm?id=1007669)

