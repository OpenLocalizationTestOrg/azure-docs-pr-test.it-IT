---
title: aaaAzure DB Cosmos modello di risorse e concetti | Documenti Microsoft
description: "Informazioni sul modello gerarchico di Azure Cosmos DB del database, raccolte, la funzione definita dall'utente (UDF), documenti, le autorizzazioni toomanage risorse e più."
keywords: Modello gerarchico, Cosmos DB, Azure, Microsoft Azure
services: cosmos-db
documentationcenter: 
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: ef9d5c0c-0867-4317-bb1b-98e219799fd5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: anhoh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc3642232b86cc27901ebd97456c386829324632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-hierarchical-resource-model-and-core-concepts"></a>Modello di risorsa gerarchico e concetti di base relativi ad Azure Cosmos DB
le entità di database che consente di gestire Azure Cosmos DB Hello sono cui tooas **risorse**. Ogni risorsa viene identificata in modo univoco da un URI logico. È possibile interagire con risorse hello utilizzando i verbi HTTP standard, le intestazioni di richiesta/risposta e i codici di stato. 

Leggendo questo articolo, sarà in grado di tooanswer hello seguenti domande:

* Qual è il modello di risorsa di Cosmos DB?
* Quali sono system risorse definite come risorse anziché toouser definito?
* Come si indirizza una risorsa?
* Come si usano le raccolte?
* Come si usano le stored procedure, i trigger e le funzioni definite dall'utente

## <a name="hierarchical-resource-model"></a>Modello di risorse gerarchico
Come hello diagramma seguente viene illustrato, hello DB Cosmos gerarchica **modello di risorsa** costituiti da set di risorse con un account di database, ogni indirizzabile tramite URI logico e stabile. Un set di risorse sarà tooas di cui si fa riferimento un **feed** in questo articolo. 

> [!NOTE]
> DB Cosmos Azure offre un protocollo TCP altamente efficiente che è RESTful anche nel modello di comunicazione, disponibile tramite hello [API client .NET di DocumentDB](documentdb-sdk-dotnet.md).
> 
> 

![Modello di risorsa gerarchico di Azure Cosmos DB][1]  
**Modello di risorse gerarchico**   

toostart utilizzo delle risorse, è necessario [creare un account di database](create-documentdb-dotnet.md) tramite la sottoscrizione di Azure. Un account di database può essere costituito da un set di **database**, ognuno contenente più **raccolte**. Ogni raccolta include a propria volta **stored procedure, trigger, funzioni definite dall'utente, documenti** e **allegati** correlati. Un database è inoltre associate **utenti**, ognuno con un set di **autorizzazioni** tooaccess raccolte, stored procedure, trigger, funzioni definite dall'utente, documenti o gli allegati. Mentre i database, gli utenti, le autorizzazioni e le raccolte sono ricorse definite dal sistema con schemi noti, i documenti e gli allegati includono contenuto JSON arbitrario definito dagli utenti.  

| Risorsa | Descrizione |
| --- | --- |
| Account di database |Un account di database è associato a un set di database e a una quantità fissa di archivio BLOB per gli allegati. È possibile creare uno o più account di database usando la sottoscrizione di Azure. Per altre informazioni, visitare la [pagina dei prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/). |
| Database |Un database è un contenitore logico di archiviazione documenti partizionato nelle raccolte. Un database è anche un contenitore degli utenti |
| Utente |Hello spazio dei nomi logico per definire l'ambito delle autorizzazioni. |
| Autorizzazione |Un token di autorizzazione associato a un utente per la risorsa specifica tooa di accesso. |
| Raccolta |Una raccolta è un contenitore di documenti JSON e hello associati logica dell'applicazione JavaScript. Una raccolta è un'entità fatturabile, dove hello [costo](performance-levels.md) è determinato dal livello di prestazioni hello associato hello insieme. Le raccolte possono estendersi su uno o più partizioni/server e può essere ridimensionato toohandle praticamente illimitate di volumi di archiviazione o una velocità effettiva. |
| Stored Procedure |Logica dell'applicazione scritta in JavaScript che viene registrato in una raccolta e livello di transazione eseguita all'interno del motore di database hello. |
| Trigger |Logica dell'applicazione scritta in JavaScript ed eseguita prima o dopo un'operazione di inserimento, sostituzione o eliminazione. |
| UDF |Logica dell'applicazione scritta in JavaScript. Funzioni definite dall'utente abilitare si toomodel un operatore di query personalizzata e in tal modo estendere linguaggio di query API DocumentDB core hello. |
| Documento |Contenuto JSON definito dall'utente (arbitrario). Per impostazione predefinita, nessun schema deve essere toobe definito né che sia gli indici secondari toobe fornito per hello tutti i documenti aggiunti tooa insieme. |
| Attachment |Un allegato è un documento speciale contenente riferimenti e metadati associati per BLOB/file multimediali esterni. sviluppatore Hello scegliere toohave hello gestita blob tramite DB Cosmos o archiviarlo presso un provider di servizi blob esterno come OneDrive, Dropbox e così via. |

## <a name="system-vs-user-defined-resources"></a>Risorse definite dal sistema e risorse definite dall'utente
Tutte le risorse quali account di database, database, raccolte, utenti, autorizzazioni, stored procedure, trigger e funzioni UDF hanno uno schema fisso e sono definite risorse di sistema. Al contrario, le risorse, ad esempio documenti e gli allegati non presentano restrizioni schema hello e sono riportati esempi di risorse definiti dall'utente. In Cosmos DB le risorse definite sia dal sistema che dall'utente vengono rappresentate e gestite come risorse JSON conformi allo standard. Tutte le risorse del sistema o dall'utente, è necessario hello seguenti proprietà comuni.

> [!NOTE]
> Si noti che, nell'implementazione JSON, tutte le proprietà generate dal sistema in una risorsa hanno come prefisso un carattere di sottolineatura (_).
> 
> 

<table>
    <tbody>
        <tr>
            <td valign="top"><p><strong>Proprietà</strong></p></td>
            <td valign="top"><p><strong>Impostabile dall'utente o generata dal sistema</strong></p></td>
            <td valign="top"><p><strong>Scopo</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>_rid</p></td>
            <td valign="top"><p>Generata dal sistema</p></td>
            <td valign="top"><p>Generato dal sistema, un identificatore univoco e gerarchico della risorsa di hello</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_etag</p></td>
            <td valign="top"><p>Generata dal sistema</p></td>
            <td valign="top"><p>valore eTag della risorsa hello necessaria per il controllo della concorrenza ottimistica</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_ts</p></td>
            <td valign="top"><p>Generata dal sistema</p></td>
            <td valign="top"><p>Timestamp ultimo aggiornamento della risorsa hello</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_self</p></td>
            <td valign="top"><p>Generata dal sistema</p></td>
            <td valign="top"><p>URI indirizzabile univoco della risorsa hello</p></td>
        </tr>
        <tr>
            <td valign="top"><p>id</p></td>
            <td valign="top"><p>Generata dal sistema</p></td>
            <td valign="top"><p>Nome univoco della risorsa hello definito dall'utente (con hello stessa partizione di valore chiave). Se l'utente hello non specifica un id, un id sarà generata dal sistema</p></td>
        </tr>
    </tbody>
</table>

### <a name="wire-representation-of-resources"></a>Rappresentazione delle risorse
COSMOS DB non implica eventuali estensioni proprietarie toohello JSON standard o speciali codifiche; funziona con standard documenti compatibili con JSON.  

### <a name="addressing-a-resource"></a>Indirizzamento di una risorsa
Tutte le risorse sono indirizzabili mediante URI. valore di hello Hello **_self** proprietà di una risorsa rappresenta hello relativo URI della risorsa di hello. Hello formato dell'URI hello costituito hello /\<feed\>/ { RID} segmenti di percorso:  

| Valore di self hello | Descrizione |
| --- | --- |
| /dbs |Feed dei database in un account di database |
| /dbs/{dbName} |Database con id corrispondente valore hello {dbName} |
| /dbs/{dbName}/colls/ |Feed delle raccolte in un database |
| /dbs/{dbName}/colls/{collName} |Raccolta con id corrispondente valore hello {collName} |
| /dbs/{dbName}/colls/{collName}/docs |Feed dei documenti in una raccolta |
| /dbs/{dbName}/colls/{collName}/docs/{docId} |Il documento con un id corrispondente valore hello {doc} |
| /dbs/{dbName}/users/ |Feed degli utenti in un database |
| /dbs/{dbName}/users/{userId} |Utente con id corrispondente valore hello {user} |
| /dbs/{dbName}/users/{userId}/permissions |Feed delle autorizzazioni in un utente |
| /dbs/{dbName}/users/{userId}/permissions/{permissionId} |Autorizzazione con un id corrispondente valore hello {permission} |

Ogni risorsa ha un nome utente univoco definito esposto tramite proprietà id hello. Nota: per i documenti, se non è specificata, un id utente hello nostri supportato SDK genererà automaticamente un id univoco per il documento hello. id Hello è una stringa definita dall'utente, di backup too256 caratteri univoco all'interno di contesto hello di una risorsa padre specifico. 

Ogni risorsa ha anche un identificatore di risorsa gerarchica generata dal sistema (anche noto tooas un RID), che è disponibile tramite proprietà RID hello. Hello RID codifica hello la gerarchia di una determinata risorsa ed è che una rappresentazione interna pratica utilizzato tooenforce l'integrità referenziale in modalità distribuita. è utilizzato internamente da Cosmos DB per il routing efficiente senza le ricerche di partizione tra Hello RID è univoco all'interno di un account di database. i valori Hello self hello e le proprietà di RID hello sono rappresentazioni canoniche sia alternative di una risorsa. 

supporto API REST di Hello indirizzamento delle risorse e il routing delle richieste da id hello sia le proprietà di RID hello.

## <a name="database-accounts"></a>Account di database
È possibile effettuare il provisioning di uno o più account di database di Cosmos DB usando la sottoscrizione di Azure.

È possibile creare e gestire gli account di database Cosmos DB tramite il portale di Azure hello in [http://portal.azure.com/](https://portal.azure.com/). Per la creazione e la gestione di un account di database è necessario l'accesso amministrativo e queste operazioni possono essere eseguite solo con una sottoscrizione di Azure. 

### <a name="database-account-properties"></a>Proprietà degli account di database
Come parte di provisioning e la gestione di un account del database è possibile configurare e leggere hello le proprietà seguenti:  

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Nome proprietà</strong></p></td>
            <td valign="top"><p><strong>Descrizione</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>Criterio di coerenza</p></td>
            <td valign="top"><p>Impostare il livello di coerenza proprietà tooconfigure hello predefinito per tutte le raccolte di hello con l'account di database. È possibile eseguire l'override di livello di coerenza hello per ogni richiesta utilizzando l'intestazione della richiesta hello [x-ms-consistency-level]. <p><p>Si noti che questa proprietà si applica solo toohello <i>risorse definito dall'utente</i>. Tutte le risorse di sistema definito sono letture toosupport configurato le query con coerenza assoluta.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Chiavi di autorizzazione</p></td>
            <td valign="top"><p>Si tratta di hello primario e secondarie chiavi master e di sola lettura che forniscono amministrazione accesso tooall delle risorse di hello nell'account di database hello.</p></td>
        </tr>
    </tbody>
</table>

Si noti che in aggiunta tooprovisioning, configurazione e gestione di account del database dal portale di Azure, hello è anche a livello di programmazione possono creare e gestire gli account di database DB Cosmos utilizzando hello [API REST di Azure Cosmos DB](/rest/api/documentdb/) come nonché [client SDK](documentdb-sdk-dotnet.md).  

## <a name="databases"></a>Database
Un database Cosmos DB è un contenitore logico di uno o più raccolte e gli utenti, come illustrato nel seguente diagramma hello. È possibile creare un numero qualsiasi di database in un oggetto toooffer di DB Cosmos database account limiti.  

![Modello gerarchico di account di database e raccolte][2]  
**Un database è un contenitore logico di utenti e raccolte**

Un database può contenere risorse di archiviazione di documenti praticamente illimitate partizionate all'interno delle raccolte.

### <a name="elastic-scale-of-a-cosmos-db-database"></a>Scalabilità elastica di un database di Cosmos DB
Un database DB Cosmos è elastico per impostazione predefinita: compreso fra qualche toopetabytes GB di spazio di archiviazione SSD eseguito il documento e velocità effettiva di provisioning. 

A differenza di un database tradizionale RDBMS, un database nel database Cosmos non tooa con ambito singolo computer. Con DB Cosmos, come la scalabilità dell'applicazione deve toogrow, è possibile creare più raccolte, il database o entrambi. Molte applicazioni prodotte direttamente da Microsoft usano Cosmos DB su scala consumer, creando database Cosmos DB di dimensioni estremamente elevate, ognuno dei quali include migliaia di raccolte con terabyte di spazio di archiviazione per i documenti. È possibile aumentare o compattare un database aggiungendo o rimuovendo raccolte toomeet requisiti di scalabilità dell'applicazione. 

È possibile creare un numero qualsiasi di raccolte all'interno di un'offerta di toohello oggetto di database. Ogni raccolta dispone di spazio di archiviazione SSD eseguito e la velocità effettiva il provisioning per l'utente in base al livello di prestazioni selezionati hello.

Un database di Cosmos DB è anche un contenitore di utenti. Un utente, a sua volta, è uno spazio dei nomi logico per un set di autorizzazioni che fornisce gli allegati, documenti e con granularità fine toocollections di accesso e autorizzazione.  

Come con altre risorse nel modello di risorse hello Cosmos DB, è possono creare database, sostituito, eliminare, leggere o enumerati facilmente utilizzando entrambi hello [API REST](/rest/api/documentdb/) o una qualsiasi delle hello [client SDK](documentdb-sdk-dotnet.md). COSMOS DB garantisce la coerenza assoluta per la lettura o di una query hello nei metadati di una risorsa del database. Eliminazione di un database automaticamente assicura che è in grado di recuperare raccolte hello o utenti contenuti al suo interno.   

## <a name="collections"></a>Raccolte
Una raccolta di Cosmos DB è un contenitore per i documenti JSON. 

### <a name="elastic-ssd-backed-document-storage"></a>Archiviazione flessibile di documenti basata su unità SSD
Una raccolta è intrinsecamente flessibile, poiché le dimensioni della raccolta aumentano o si riducono in seguito all'aggiunta o alla rimozione di documenti. Le raccolte sono risorse logiche e possono comprendere una o più partizioni fisiche o server. numero di Hello delle partizioni all'interno di una raccolta è determinato dal DB Cosmos in base alle dimensioni di archiviazione hello e velocità effettiva di hello provisioning della raccolta. Ogni partizione in Cosmos DB ha una quantità fissa di archiviazione supportata da unità SSD associata e viene replicata per la disponibilità elevata. Gestione delle partizioni è completamente gestiti da Azure Cosmos DB, e non si dispone di codice complesso toowrite o gestire le partizioni. Le raccolte di Cosmos DB sono **praticamente illimitate** in termini di spazio di archiviazione e velocità effettiva. 

### <a name="automatic-indexing-of-collections"></a>Indicizzazione automatica delle raccolte
Cosmos DB è un sistema di database effettivamente privo di schema. Non presupporre o richiedere uno schema per documenti JSON hello. Come si aggiunge una raccolta di documenti tooa, DB Cosmos li indicizza automaticamente e sono disponibili per si tooquery. L'indicizzazione automatica di documenti senza la necessità di schemi o di indici secondari è una funzionalità chiave di Cosmos DB ed è resa possibile da tecniche di gestione dell'indice ottimizzate per la scrittura, prive di blocco e strutturate in log. Cosmos DB supporta un volume sostenuto di scritture estremamente veloci, gestendo al tempo stesso query coerenti. Il documento e l'indice dell'archiviazione sono stata utilizzata l'archiviazione di hello toocalculate utilizzati da ogni raccolta. È possibile controllare hello di prestazioni e archiviazione vantaggi e svantaggi associati di indicizzazione configurando i criteri di indicizzazione hello per una raccolta. 

### <a name="configuring-hello-indexing-policy-of-a-collection"></a>Configurazione dei criteri di indicizzazione hello di una raccolta
criteri di ogni raccolta di indicizzazione Hello consente toomake prestazioni e i vantaggi e svantaggi di archiviazione associati di indicizzazione. Hello sono le opzioni seguenti tooyou disponibile come parte della configurazione di indicizzazione:  

* Scegliere se la raccolta hello vengono indicizzati automaticamente tutti i documenti hello o non. Per impostazione predefinita, saranno indicizzati automaticamente tutti i documenti. È possibile scegliere tooturn disattivare l'indicizzazione automatica e aggiungere in modo selettivo solo un indice toohello documenti specifici. Al contrario, è possibile scegliere in modo selettivo tooexclude solo documenti specifici. È possibile ottenere questo risultato impostando hello proprietà automatica toobe true o false in indexingPolicy hello di una raccolta e utilizzo dell'intestazione di richiesta di hello [x-ms-indexingdirective] durante l'inserimento, sostituzione o l'eliminazione di un documento.  
* Scegliere se tooinclude o exclude percorsi specifici o modelli di documenti da hello indice. È possibile ottenere questa impostazione includedPaths ed excludedPaths in indexingPolicy hello di una raccolta rispettivamente. È anche possibile configurare hello archiviazione e sulle prestazioni dei compromessi per intervallo e hash di query per i modelli di percorso specifico. 
* Possibilità di scegliere tra aggiornamenti sincroni (coerenti) e asincroni (differiti) dell'indice. Per impostazione predefinita, l'indice di hello viene aggiornato in modo sincrono in ogni inserimento, sostituzione o eliminazione di una raccolta di toohello documento. Questo consente le query hello toohonor hello che di lettura documento hello stesso livello di coerenza. Mentre Cosmos DB è con ottimizzazione per la scrittura e supporta volumi prolungati di scritture di documento e la manutenzione degli indici sincrono e la gestione delle query coerenti, è possibile configurare determinate tooupdate raccolte relativo indice in modo differito. Questo tipo di indicizzazione migliora ulteriormente le prestazioni scrittura hello ed è ideale per gli scenari di inserimento bulk per principalmente le raccolte con intensa attività di lettura.

criteri di indicizzazione Hello può essere modificato tramite l'esecuzione di un'operazione PUT su una raccolta di hello. Può essere ottenuta tramite hello [client SDK](documentdb-sdk-dotnet.md), hello [portale Azure](https://portal.azure.com) o hello [API REST](/rest/api/documentdb/).

### <a name="querying-a-collection"></a>Esecuzione di query su una raccolta
documenti Hello all'interno di una raccolta possono avere schemi arbitrari ed è possibile eseguire una query documenti all'interno di una raccolta senza fornire informazioni dello schema o sin dall'inizio indici secondari. È possibile eseguire query di raccolta hello utilizzando hello [API DocumentDB di Azure Cosmos DB: riferimento alla sintassi SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx), che fornisce RTF gerarchici, relazionali, spaziali e gli operatori ed estendibilità tramite le UDF basate su JavaScript. Consente di grammatica JSON per la modellazione di documenti JSON come alberi con etichette come nodi dell'albero hello. Viene usata dalle tecniche di indicizzazione automatica dell'API di DocumentDB e dal dialetto SQL dell'API di DocumentDB. il linguaggio di query API DocumetDB Hello è costituita da tre aspetti principali:   

1. Un piccolo set di operazioni di query che eseguono il mapping naturalmente struttura ad albero toohello inclusi proiezioni e query gerarchiche. 
2. Un sottoinsieme di operazioni relazionali, incluse la composizione, l'applicazione di filtri, le proiezioni, le aggregazioni e i self join. 
3. Funzioni definite dall'utente pure basate su JavaScript in grado di funzionare con (1) e (2).  

modello di query Cosmos DB Hello tenta toostrike un equilibrio tra funzionalità, l'efficienza e alla semplicità. motore di database DB Cosmos Hello, in modo nativo, compila ed esegue le istruzioni di query SQL hello. È possibile eseguire query a una raccolta tramite hello [API REST](/rest/api/documentdb/) o una qualsiasi delle hello [client SDK](documentdb-sdk-dotnet.md). Hello .NET SDK include un provider LINQ.

> [!TIP]
> È possibile provare hello API DocumentDB ed eseguire query SQL nel set di dati in hello [Query Playground](https://www.documentdb.com/sql/demo).
> 
> 

## <a name="multi-document-transactions"></a>Transazioni in più documenti
Le transazioni di database offrono un modello di programmazione sicuro e prevedibile per la gestione di modifiche simultanee toohello dato. Nel sistema RDBMS e logica di business di hello modalità tradizionale toowrite è toowrite **stored procedure** e/o **trigger** e consegnare il server di database toohello per l'esecuzione transazionale. Programmatore applicazione hello RDBMS, è necessario toodeal con due diversi linguaggi di programmazione: 

* (non transazionale) Hello linguaggio di programmazione (ad esempio, JavaScript, Python, c#, Java e così via)
* T-SQL, hello transazionale linguaggio di programmazione che viene eseguito in modo nativo dal database hello

Grazie all'impegno complete tooJavaScript e JSON direttamente all'interno del motore di database hello, Cosmos DB fornisce un modello di programmazione intuitivo per JavaScript in esecuzione in base a logica dell'applicazione direttamente nelle raccolte di hello in termini di stored procedure e trigger. In questo modo per entrambe operazioni hello seguenti:

* Controllare l'implementazione efficiente di concorrenza, ripristino, l'indicizzazione di grafici di oggetti JSON hello direttamente nel motore di database hello automatico
* Naturalmente esprimere il flusso di controllo, variabili dell'ambito, l'assegnazione e integrazione di gestione delle eccezioni primitive con transazioni di database direttamente in termini di linguaggio di programmazione JavaScript hello

logica di JavaScript Hello registrata a livello di raccolta può quindi eseguire operazioni di database su documenti hello di hello fornito insieme. DB COSMOS in modo implicito hello esegue il wrapping JavaScript basati su stored procedure e trigger all'interno di un ambiente transazioni ACID con isolamento dello snapshot in documenti all'interno di una raccolta. Durante l'esecuzione, hello se hello JavaScript verrà generata un'eccezione, quindi hello dell'intera transazione viene interrotta. Hello risulta modello di programmazione è molto semplice potenti. Gli sviluppatori JavaScript ottengono un modello di programmazione "durevole", usando al tempo stesso i costrutti dei propri linguaggi preferiti e i primitivi di librerie.   

Hello possibilità tooexecute JavaScript direttamente all'interno del database hello motore in hello stesso spazio degli indirizzi del pool di buffer hello consente ad alte prestazioni e l'esecuzione transazionale di operazioni sui documenti hello del database di una raccolta. Inoltre, motore di database DB Cosmos rende toohello un impegno complete JSON e JavaScript elimina qualsiasi mancata corrispondenza tra i sistemi di tipi hello dell'applicazione e database hello.   

Dopo aver creato una raccolta, è possibile registrare le stored procedure, trigger e funzioni definite dall'utente con una raccolta tramite hello [API REST](/rest/api/documentdb/) o una qualsiasi delle hello [client SDK](documentdb-sdk-dotnet.md). Dopo la registrazione, sarà possibile farvi riferimento ed eseguire questi elementi. Prendere in considerazione hello seguente stored procedure scritta interamente in JavaScript, codice hello seguente accetta due argomenti (nome e il nome dell'autore) e crea un nuovo documento, una query per un documento e quindi aggiorna il – tutti all'interno di una transazione ACID implicita. In qualsiasi momento durante l'esecuzione di hello, se viene generata un'eccezione JavaScript, hello intera transazione si interrompe.

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();        
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            {id: name, author: author},
            function(err, documentCreated) {
                if(err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function(err, matchingDocuments) {
                        if(err) throw new Error(err.message);

                        context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don’t need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);   
                        }
                    })
            })
    };

client Hello "spedire" hello sopra database toohello logica di JavaScript per l'esecuzione transazionale tramite HTTP POST. Per altre informazioni sull'uso di metodi HTTP, vedere [RESTful interactions with Azure Cosmos DB resources](https://msdn.microsoft.com/library/azure/mt622086.aspx) (Interazioni RESTful con risorse di Azure Cosmos DB). 

    client.createStoredProcedureAsync(collection._self, {id: "CRUDProc", body: businessLogic})
       .then(function(createdStoredProcedure) {
            return client.executeStoredProcedureAsync(createdStoredProcedure.resource._self,
                "NoSQL Distilled",
                "Martin Fowler");
        })
        .then(function(result) {
            console.log(result);
        },
        function(error) {
            console.log(error);
        });


Si noti che poiché il database di hello in modo nativo riconosce JSON e JavaScript, non è non corrispondenti di sistema di tipo, "mapping OR" o chiave di generazione di codice richiesto.   

Stored procedure e trigger interagire con i documenti in una raccolta tramite un modello a oggetti ben definiti, che espone il contesto insieme corrente di hello hello e di raccolta.  

Le raccolte in hello API DocumentDB è possibile creare, eliminare, leggere o enumerati facilmente utilizzando entrambi hello [API REST](/rest/api/documentdb/) o una qualsiasi delle hello [client SDK](documentdb-sdk-dotnet.md). Hello API DocumentDB fornisce sempre coerenza assoluta per la lettura o di una query hello nei metadati di una raccolta. L'eliminazione di una raccolta automaticamente assicura che non è possibile accedere a uno qualsiasi dei documenti hello, allegati, stored procedure, trigger e funzioni definite dall'utente in esso contenuti.   

## <a name="stored-procedures-triggers-and-user-defined-functions-udf"></a>Stored procedure, trigger e funzioni definite dall'utente (UDF)
Come descritto nella sezione precedente di hello, è possibile scrivere applicazioni logica toorun direttamente all'interno di una transazione all'interno del motore di database hello. la logica dell'applicazione Hello può essere scritta interamente in JavaScript e può essere modellata come una stored procedure, trigger o una funzione definita dall'utente. Hello codice JavaScript all'interno di una stored procedure o un trigger può inserire, sostituire, eliminazione e lettura o la query documenti all'interno di una raccolta. In hello invece, non è possibile inserire, sostituire o eliminare documenti hello JavaScript all'interno di una funzione definita dall'utente. Funzioni definite dall'utente enumerare documenti hello del set di risultati di query e restituire un altro set di risultati. Per la multi-tenancy, Cosmos DB applica una rigida governance delle risorse basata sulle prenotazioni. Ogni stored procedure, trigger o una funzione definita dall'utente ottiene un quantum predefinito del sistema operativo risorse toodo il proprio lavoro. Inoltre, le stored procedure, trigger o funzioni definite dall'utente non è possibile collegare in librerie JavaScript esterne e sono disattivato se superano i budget di risorsa hello allocati toothem. È possibile registrare, annullare la registrazione di stored procedure, trigger o funzioni definite dall'utente con una raccolta usando le API REST di hello.  Durante la registrazione, una stored procedure, un trigger o una funzione UDF saranno precompilati e archiviati come codice byte, che sarà eseguito in seguito. Hello seguente sezione viene illustrato come è possibile utilizzare hello Cosmos DB JavaScript SDK tooregister, eseguire e annullare la registrazione di una stored procedure, trigger e una funzione definita dall'utente. Hello SDK per JavaScript è un semplice wrapper su hello [API REST](/rest/api/documentdb/). 

### <a name="registering-a-stored-procedure"></a>Registrazione di una stored procedure
La registrazione di una stored procedure consiste nel creare una nuova risorsa stored procedure in una raccolta tramite un metodo HTTP POST.  

    var storedProc = {
        id: "validateAndCreate",
        body: function (documentToCreate) {
            documentToCreate.id = documentToCreate.id.toUpperCase();

            var collectionManager = getContext().getCollection();
            collectionManager.createDocument(collectionManager.getSelfLink(),
                documentToCreate,
                function(err, documentCreated) {
                    if(err) throw new Error('Error while creating document: ' + err.message;
                    getContext().getResponse().setBody('success - created ' + 
                            documentCreated.name);
                });
        }
    };

    client.createStoredProcedureAsync(collection._self, storedProc)
        .then(function (createdStoredProcedure) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-stored-procedure"></a>Esecuzione di una stored procedure
Esecuzione di una stored procedure viene eseguita inviando una richiesta POST HTTP su una risorsa stored procedure esistente passando i parametri procedure toohello nel corpo della richiesta hello.

    var inputDocument = {id : "document1", author: "G. G. Marquez"};
    client.executeStoredProcedureAsync(createdStoredProcedure.resource._self, inputDocument)
        .then(function(executionResult) {
            assert.equal(executionResult, "success - created DOCUMENT1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-stored-procedure"></a>Annullamento della registrazione di una stored procedure
L'annullamento della registrazione di una stored procedure avviene tramite la semplice esecuzione di un'operazione HTTP DELETE su una risorsa stored procedure esistente.   

    client.deleteStoredProcedureAsync(createdStoredProcedure.resource._self)
        .then(function (response) {
            return;
        }, function(error) {
            console.log("Error");
        });


### <a name="registering-a-pre-trigger"></a>Registrazione di un trigger
La registrazione di un trigger è eseguita tramite la creazione di una nuova risorsa trigger in una raccolta tramite HTTP POST. È possibile specificare se i trigger di hello è una versione preliminare o un tipo di trigger e hello post dell'operazione può essere associata a (ad esempio Create, Replace, Delete o tutti).   

    var preTrigger = {
        id: "upperCaseId",
        body: function() {
                var item = getContext().getRequest().getBody();
                item.id = item.id.toUpperCase();
                getContext().getRequest().setBody(item);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.All
    }

    client.createTriggerAsync(collection._self, preTrigger)
        .then(function (createdPreTrigger) {
            console.log("Successfully created trigger");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-pre-trigger"></a>Esecuzione di un trigger
Esecuzione di un trigger viene eseguita specificando il nome di hello di un trigger esistente in fase di hello di hello di richiesta POST, PUT o eliminazione di una risorsa documento tramite l'intestazione della richiesta hello.  

    client.createDocumentAsync(collection._self, { id: "doc1", key: "Love in hello Time of Cholera" }, { preTriggerInclude: "upperCaseId" })
        .then(function(createdDocument) {
            assert.equal(createdDocument.resource.id, "DOC1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-pre-trigger"></a>Annullamento della registrazione di un trigger
L'annullamento della registrazione di un trigger avviene tramite la semplice esecuzione di un'operazione HTTP DELETE su una risorsa trigger esistente.  

    client.deleteTriggerAsync(createdPreTrigger._self);
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

### <a name="registering-a-udf"></a>Registrazione di una funzione UDF
La registrazione di una funzione UDF è eseguita tramite la creazione di una nuova risorsa UDF in una raccolta tramite HTTP POST.  

    var udf = { 
        id: "mathSqrt",
        body: function(number) {
                return Math.sqrt(number);
        },
    };
    client.createUserDefinedFunctionAsync(collection._self, udf)
        .then(function (createdUdf) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-udf-as-part-of-hello-query"></a>L'esecuzione di una funzione definita dall'utente come parte di query hello
Una funzione definita dall'utente può essere specificato come parte della query SQL hello e viene utilizzato come un core di hello tooextend modo [linguaggio di query SQL per l'API DocumentDB hello](https://msdn.microsoft.com/library/azure/dn782250.aspx).

    var filterQuery = "SELECT udf.mathSqrt(r.Age) AS sqrtAge FROM root r WHERE r.FirstName='John'";
    client.queryDocuments(collection._self, filterQuery).toArrayAsync();
        .then(function(queryResponse) {
            var queryResponseDocuments = queryResponse.feed;
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-udf"></a>Annullamento della registrazione di una funzione UDF
L'annullamento della registrazione di una funzione definita dall'utente avviene tramite la semplice esecuzione di un'operazione HTTP DELETE su una risorsa di funzione definita dall'utente esistente.  

    client.deleteUserDefinedFunctionAsync(createdUdf._self)
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

Anche se ha dimostrato hello i frammenti di codice precedente registrazione hello (POST), l'annullamento della registrazione (PUT), lettura/elenco (GET) e l'esecuzione (POST) tramite hello [JavaScript SDK](https://github.com/Azure/azure-documentdb-js), è inoltre possibile utilizzare hello [API REST](/rest/api/documentdb/) o altri [client SDK](documentdb-sdk-dotnet.md). 

## <a name="documents"></a>Documenti
È possibile inserire, sostituire, eliminare, leggere, enumerare ed eseguire query in documenti JSON arbitrari in una raccolta. COSMOS DB non implica qualsiasi schema e non richiede gli indici secondari in ordine toosupport l'esecuzione di query sui documenti in una raccolta. dimensione massima di Hello per un documento è 2 MB.   

Essendo un vero e proprio servizio di database aperto, Cosmos DB non genera tipi di dati specializzati (ad esempio, data e ora) né codifiche specifiche per i documenti JSON. Si noti che DB Cosmos non richiedono speciali JSON convenzioni toocodify hello relazioni tra i vari documenti. la sintassi SQL Hello del DB Cosmos fornisce gli operatori di query relazionale e gerarchica molto potente tooquery e progetto documenti senza annotazioni speciali o necessità toocodify relazioni tra i documenti con proprietà distinte.  

Come con tutte le altre risorse, è possono creare documenti, sostituito, eliminare, leggere, enumerati e individuato facilmente utilizzando le API REST o uno qualsiasi dei hello [client SDK](documentdb-sdk-dotnet.md). L'eliminazione di un documento immediatamente consente di liberare hello tooall corrispondente di quota di allegati hello annidato. Hello lettura a livello di coerenza dei documenti segue criteri coerenza hello account database hello. È possibile eseguire l'override di questo criterio per le singole richieste, in base ai requisiti di coerenza dei dati specifici dell'applicazione. Quando una query su documenti, hello leggere coerenza segue hello l'indicizzazione in modalità di raccolta hello. Per "coerente", questo segue i criteri di consistenza dell'account hello. 

## <a name="attachments-and-media"></a>Allegati e file multimediali
COSMOS DB consente toostore binario BLOB o dei supporti con DB Cosmos (massimo di 2 GB per ogni account) o tooyour multimediali remoti proprio archivio. Consente inoltre toorepresent hello metadati di un supporto in termini di un documento speciale denominato allegato. Allegato a un database Cosmos è un documento di (JSON) speciale che riferimenti hello multimediale/blob archiviati in un' posizione. Un allegato è semplicemente un documento speciale che acquisisce hello metadati (ad esempio percorso, autore e così via) di una media archiviato in un archivio remoto supporti. 

Si consideri un'applicazione di social networking di lettura che utilizza le annotazioni a penna toostore DB Cosmos ed evidenzia metadati comprensivo di commenti, segnalibri, classificazioni, simili/preferenze e così via associati per un e-book di un determinato utente.   

* Hello contenuto del libro hello stesso viene archiviato nell'archivio multimediale hello è disponibile come parte dell'account database DB Cosmos o un archivio remoto supporti. 
* Un'applicazione può archiviare i metadati di ogni utente come documento distinto, ad esempio i metadati di Joe per book1 saranno archiviati in un documento a cui si fa riferimento come /colls/joe/docs/book1. 
* Gli allegati che punta toohello pagine di contenuto di un libro di un utente specifico vengono archiviati nel documento corrispondente hello /colls/joe/docs/book1/chapter1 ad esempio, /colls/joe/docs/book1/chapter2 e così via. 

Si noti che gli esempi di hello elencati sopra Usa gerarchia di risorse hello tooconvey ID descrittivo. Le risorse sono accessibili tramite le API REST di hello tramite gli ID di risorsa univoca. 

Per un supporto hello che è gestito da DB Cosmos, proprietà Media hello di allegato hello farà riferimento supporti hello dal relativo URI. COSMOS DB modo supporti hello collect toogarbage quando tutti i riferimenti in attesa di hello vengono eliminati. COSMOS DB genera allegato hello quando si carica un nuovo supporto hello e popolati automaticamente hello Media toopoint toohello appena aggiunto supporto. Se si sceglie supporti hello toostore in un archivio blob remoti gestito dall'utente (ad esempio, OneDrive, l'archiviazione di Azure, DropBox e così via), è possibile utilizzare ancora media di hello tooreference allegati. In questo caso, si verrà personalizzate allegato hello e popolare la relativa proprietà Media.   

Come con tutte le altre risorse, gli allegati possono essere creati, sostituito, eliminare, leggere o enumerati facilmente utilizzando le API REST o uno qualsiasi dei client hello SDK. Con i documenti, hello lettura a livello di coerenza degli allegati di segue i criteri di verifica coerenza hello account database hello. È possibile eseguire l'override di questo criterio per le singole richieste, in base ai requisiti di coerenza dei dati specifici dell'applicazione. Quando si eseguono query per gli allegati, hello lettura coerenza segue hello l'indicizzazione in modalità di raccolta hello. Per "coerente", questo segue i criteri di consistenza dell'account hello. 
 

## <a name="users"></a>Utenti
Un utente di Cosmos DB rappresenta uno spazio dei nomi logico per il raggruppamento di autorizzazioni. Un utente DB Cosmos potrebbe corrispondere tooa utente in un sistema di gestione di identità o un ruolo applicazione predefinita. Per Cosmos DB, un utente rappresenta semplicemente un toogroup astrazione un set di autorizzazioni in un database.   

Per l'implementazione di multi-tenancy nell'applicazione, è possibile creare utenti in Cosmos DB che corrisponde a utenti effettivi tooyour o tenant hello dell'applicazione. È quindi possibile creare le autorizzazioni per un determinato utente corrispondenti toohello di controllo di accesso su varie raccolte, documenti, allegati e così via.   

Come le applicazioni devono tooscale con l'aumento delle dimensioni dell'utente, è possibile adottare diversi modi tooshard i dati. È possibile modellare ogni utente in modo che:   

* Ogni utente esegue il mapping tooa database.
* Ogni utente esegue il mapping tooa insieme. 
* Documenti corrispondenti agli utenti di toomultiple passare insieme tooa dedicato. 
* Documenti corrispondenti agli utenti di toomultiple passare tooa set di raccolte.   

Indipendentemente dalla strategia di partizionamento orizzontale specifica hello che scelta, è possibile modellare gli utenti effettivi come gli utenti di database DB Cosmos e associare utente tooeach autorizzazioni specifiche.  

![Raccolte degli utenti][3]  
**Strategie di partizionamento orizzontale e modellazione degli utenti**

Come tutte le altre risorse, gli utenti nel database Cosmos possono essere creati, sostituito, eliminati, leggere o enumerati facilmente utilizzando le API REST o uno qualsiasi dei client hello SDK. COSMOS DB fornisce sempre coerenza assoluta per la lettura o di una query hello nei metadati di una risorsa utente. È importante precisare che l'eliminazione di un utente automaticamente garantisce che non è possibile accedere autorizzazioni hello in esso contenuti. Anche se quota hello di autorizzazioni hello viene recuperato da hello DB Cosmos come parte dell'utente eliminato hello in background hello, autorizzazioni hello eliminato è disponibile immediatamente nuovamente per si toouse.  

## <a name="permissions"></a>Autorizzazioni
Dal punto di vista del controllo di accesso, le risorse quali account di database, database, utenti e autorizzazioni sono considerate come risorse *amministrative* perché necessitano di autorizzazioni amministrative. In hello altra parte, incluse le raccolte di hello, documenti, allegati, stored procedure, trigger, risorse e funzioni definite dall'utente sono con ambito in un determinato database e considerati *risorse dell'applicazione*. Corrispondente toohello due tipi di risorse e i ruoli hello accedervi (vale a dire hello amministratore e utente), il modello di autorizzazione hello definisce due tipi di *le chiavi di accesso*: *chiave master* e *chiave di risorsa*. chiave master di Hello è una parte dell'account database hello e viene fornito per sviluppatori toohello (o amministratore) che esegue il provisioning account hello del database. La chiave master utilizza la semantica di amministratore, in quanto può essere utilizzato tooauthorize accesso tooboth amministrativi e le risorse dell'applicazione. Al contrario, una chiave di risorsa è una chiave di accesso granulare che consente accesso tooa *specifico* risorsa dell'applicazione. Di conseguenza, l'acquisizione di relazione hello tra utente hello di un database e hello autorizzazioni hello utente per una risorsa specifica (ad esempio, insieme, documento, allegati, stored procedure, trigger o funzione definita dall'utente).   

Hello solo modo tooobtain che una chiave di risorsa è tramite la creazione di una risorsa di autorizzazione in un determinato utente. Si noti che nell'ordine toocreate o recuperare un'autorizzazione, una chiave master deve essere presentata nell'intestazione di autorizzazione hello. Una risorsa di autorizzazione Collega utente di risorse, l'accesso e hello hello. Dopo la creazione di una risorsa di autorizzazione, utente hello deve solo una chiave di risorsa associata toopresent hello nella risorsa pertinente toohello accesso toogain ordine. Di conseguenza, una chiave di risorsa può essere visualizzata come una rappresentazione compatta e logica della risorsa di autorizzazione hello.  

Come con tutte le altre risorse, le autorizzazioni nel database Cosmos possono essere create, sostituito, eliminare, leggere o enumerati facilmente utilizzando le API REST o uno qualsiasi dei client hello SDK. COSMOS DB fornisce sempre coerenza assoluta per la lettura o di una query hello nei metadati di un'autorizzazione. 

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'utilizzo di risorse tramite comandi HTTP, vedere [RESTful interactions with Cosmos DB resources](https://msdn.microsoft.com/library/azure/mt622086.aspx) (Interazioni di tipo RESTful con risorse di Cosmos DB).

[1]: media/documentdb-resources/resources1.png
[2]: media/documentdb-resources/resources2.png
[3]: media/documentdb-resources/resources3.png

