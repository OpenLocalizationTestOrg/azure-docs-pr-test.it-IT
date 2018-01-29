---
title: Modello di risorsa e concetti relativi ad Azure Cosmos DB | Microsoft Docs
description: Informazioni sul modello gerarchico di database, raccolte, funzioni definite dall'utente, documenti, autorizzazioni per gestire le risorse e altro ancora in Azure Cosmos DB.
keywords: Modello gerarchico, Cosmos DB, Azure, Microsoft Azure
services: cosmos-db
documentationcenter: 
author: rafats
manager: jhubbard
ms.assetid: ef9d5c0c-0867-4317-bb1b-98e219799fd5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: rafats
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a88f17a658987e1ff3ae0e0f38d6551c3acee1da
ms.sourcegitcommit: 0e4491b7fdd9ca4408d5f2d41be42a09164db775
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="azure-cosmos-db-hierarchical-resource-model-and-core-concepts"></a>Modello di risorsa gerarchico e concetti di base relativi ad Azure Cosmos DB

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)]

Le entità del database gestite da Azure Cosmos DB vengono chiamate **risorse**. Ogni risorsa viene identificata in modo univoco da un URI logico. È possibile interagire con le risorse utilizzando i verbi HTTP standard, le intestazioni di richiesta/risposta e i codici di stato. 

In questo articolo le risposte alle domande seguenti:

* Cos'è il modello di risorsa di Azure Cosmos DB?
* Quali sono system definito risorse anziché risorse definito dall'utente?
* Come si indirizza una risorsa?
* Come si usano le raccolte?
* Come si usano le stored procedure, i trigger e le funzioni definite dall'utente

## <a name="hierarchical-resource-model"></a>Modello di risorse gerarchico
Come illustrato nel diagramma seguente, il **modello di risorsa** gerarchico di Azure Cosmos DB è costituito da set di risorse in un account di database, ognuna indirizzabile tramite un URI logico e stabile. Un set di risorse vengono definiti un **feed** in questo articolo. 

> [!NOTE]
> DB Cosmos Azure offre un protocollo TCP altamente efficiente, è anche RESTful nel modello di comunicazione, disponibili tramite il [API client .NET SQL](sql-api-sdk-dotnet.md).
> 
> 

![Modello di risorsa gerarchico di Azure Cosmos DB][1]  
**Modello di risorse gerarchico**   

Per iniziare a usare le risorse è necessario [creare un account di database](create-sql-api-dotnet.md) usando la sottoscrizione di Azure. Un account di database può essere costituito da un set di **database**, ognuna delle quali contiene più **raccolte**, ognuna dei quali contiene a sua volta * * stored procedure, trigger, funzioni definite dall'utente, documenti e correlati  **gli allegati**. Un database è inoltre associate **utenti**, ognuno con un set di **autorizzazioni** per accedere a raccolte, le stored procedure, trigger, funzioni definite dall'utente, documenti o gli allegati. Mentre i database, gli utenti, autorizzazioni e le raccolte sono definiti dal sistema di risorse con schemi noti, documenti e allegati contengono contenuto JSON arbitrario, definiti dall'utente.  

| Risorsa | DESCRIZIONE |
| --- | --- |
| Account di database |Un account di database è associato a un set di database e a una quantità fissa di archivio BLOB per gli allegati. È possibile creare uno o più account di database usando la sottoscrizione di Azure. Per ulteriori informazioni, visitare il [pagina dei prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/). |
| Database |Un database è un contenitore logico di archiviazione documenti partizionato nelle raccolte. Un database è anche un contenitore degli utenti |
| Utente |Spazio dei nomi logico per la definizione dell'ambito delle autorizzazioni. |
| Autorizzazione |Token di autorizzazione associato a un utente per l'accesso a una risorsa specifica. |
| Raccolta |Una raccolta è un contenitore di documenti JSON e di logica dell'applicazione JavaScript associata. Una raccolta è un'entità fatturabile, in cui il [costo](performance-levels.md) è determinato dal livello di prestazioni associato alla raccolta. Le raccolte possono estendersi su più partizioni o server e possono essere ridimensionate per gestire volumi praticamente illimitati di archiviazione o di velocità effettiva. |
| Stored Procedure |Logica dell'applicazione scritta in JavaScript, viene registrata con una raccolta ed eseguita in modo transazionale all'interno del motore di database. |
| Trigger |La logica dell'applicazione scritta in JavaScript eseguite prima o dopo un inserimento, sostituire o eliminare l'operazione. |
| UDF |Logica dell'applicazione scritta in JavaScript. Funzioni definite dall'utente consentono di modellare un operatore di query personalizzata e in tal modo estendere il linguaggio di query SQL API core. |
| Documento |Contenuto JSON definito dall'utente (arbitrario). Per impostazione predefinita, non è necessario definire alcuno schema, né fornire indici secondari per tutti i documenti aggiunti a una raccolta. |
| Attachment |Un allegato è un documento speciale contenente riferimenti e metadati associati per BLOB/file multimediali esterni. Lo sviluppatore può scegliere se gestire il BLOB con Cosmos DB o archiviarlo con un provider di servizi BLOB esterno, ad esempio OneDrive, Dropbox e così via. |

## <a name="system-vs-user-defined-resources"></a>Sistema e le risorse definite dall'utente
Tutte le risorse quali account di database, database, raccolte, utenti, autorizzazioni, stored procedure, trigger e funzioni UDF hanno uno schema fisso e sono definite risorse di sistema. Al contrario, le risorse, ad esempio documenti e gli allegati non presentano restrizioni lo schema e sono riportati esempi di risorse definito dall'utente. In DB Cosmos, le risorse di sistema e definiti dall'utente vengono rappresentate e gestite come JSON conforme allo standard. Tutte le risorse, sistema o utente definito, sono le seguenti proprietà comuni:

> [!NOTE]
> Tutte le proprietà generata dal sistema in una risorsa sono precedute da un carattere di sottolineatura (_) nella rappresentazione JSON.
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
            <td valign="top"><p>Generato dal sistema, un identificatore univoco e gerarchico della risorsa</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_etag</p></td>
            <td valign="top"><p>Generata dal sistema</p></td>
            <td valign="top"><p>etag della risorsa richiesta per il controllo della concorrenza ottimistica</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_ts</p></td>
            <td valign="top"><p>Generata dal sistema</p></td>
            <td valign="top"><p>Ultimo timestamp aggiornato della risorsa</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_self</p></td>
            <td valign="top"><p>Generata dal sistema</p></td>
            <td valign="top"><p>URI univoco indirizzabile della risorsa</p></td>
        </tr>
        <tr>
            <td valign="top"><p>id</p></td>
            <td valign="top"><p>È possibile usare il</p></td>
            <td valign="top"><p>Definite dall'utente nome univoco della risorsa (con lo stesso valore chiave partizione). Se l'utente non specifica un id, un id è generata dal sistema</p></td>
        </tr>
    </tbody>
</table>

### <a name="wire-representation-of-resources"></a>Rappresentazione delle risorse
Cosmos DB non impone estensioni proprietarie o codifiche speciali allo standard JSON e funziona con i documenti JSON conformi a tale standard.  

### <a name="addressing-a-resource"></a>Indirizzamento di una risorsa
Tutte le risorse sono indirizzabili mediante URI. Il valore della proprietà **_self** di una risorsa rappresenta l'URI relativo della risorsa. Il formato dell'URI è dato dai segmenti del percorso /\<feed\>/{_rid}:  

| Valore di _self | DESCRIZIONE |
| --- | --- |
| /dbs |Feed dei database in un account di database |
| /dbs/{dbName} |Database con id corrispondente al valore {dbName} |
| /dbs/{dbName}/colls/ |Feed delle raccolte in un database |
| /dbs/{dbName}/colls/{collName} |Raccolta con un id corrispondente al valore {collName} |
| /dbs/{dbName}/colls/{collName}/docs |Feed dei documenti in una raccolta |
| /dbs/{dbName}/colls/{collName}/docs/{docId} |Documento con id corrispondente al valore {doc} |
| /dbs/{dbName}/users/ |Feed degli utenti in un database |
| /dbs/{dbName}/users/{userId} |Utente con id corrispondente al valore {user} |
| /dbs/{dbName}/users/{userId}/permissions |Feed delle autorizzazioni in un utente |
| /dbs/{dbName}/users/{userId}/permissions/{permissionId} |Autorizzazione con id corrispondente al valore {permission} |

Ogni risorsa ha un nome univoco definito dall'utente vengono esposto tramite la proprietà id. Nota: per i documenti, se l'utente non specifica un id, il SDK di genera automaticamente un id univoco per il documento. L'id è una stringa definita dall'utente, fino a 256 caratteri che è univoco all'interno del contesto di una risorsa padre specifico. 

Ogni risorsa ha anche un identificatore gerarchico generato dal sistema (chiamato anche RID), disponibile tramite la proprietà _rid. Il RID codifica l'intera gerarchia di una determinata risorsa ed è una rappresentazione interna utile da usare per imporre l'integrità referenziale secondo un metodo distribuito. Il RID è univoco all'interno di un account di database e viene usato internamente da Cosmos DB per un routing efficiente senza necessità di eseguire ricerche su più partizioni. I valori delle proprietà _self e _rid sono entrambi rappresentazioni alternate e canoniche di una risorsa. 

Le API REST supportano l'indirizzamento delle risorse e il routing delle richieste tramite l'id e le proprietà _rid.

## <a name="database-accounts"></a>Account di database
È possibile effettuare il provisioning di uno o più account di database di Cosmos DB usando la sottoscrizione di Azure.

È possibile creare e gestire gli account di database Cosmos DB tramite il portale di Azure all'indirizzo [http://portal.azure.com/](https://portal.azure.com/). Per la creazione e la gestione di un account di database è necessario l'accesso amministrativo e queste operazioni possono essere eseguite solo con una sottoscrizione di Azure. 

### <a name="database-account-properties"></a>Proprietà degli account di database
Come parte del provisioning e della gestione di un account di database, è possibile configurare e leggere le proprietà seguenti:  

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Nome proprietà</strong></p></td>
            <td valign="top"><p><strong>Descrizione</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>Criterio di coerenza</p></td>
            <td valign="top"><p>Impostare questa proprietà per configurare il livello di coerenza predefinito per tutte le raccolte nell'account di database. È possibile eseguire l'override del livello di coerenza per singole richieste usando l'intestazione di richiesta [x-ms-consistency-level]. <p><p>Questa proprietà si applica solo al <i>risorse definito dall'utente</i>. Tutte le risorse definite dal sistema sono configurate per il supporto di letture/query con coerenza assoluta.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Chiavi di autorizzazione</p></td>
            <td valign="top"><p>Le chiavi primarie e secondarie master e sola lettura che forniscono l'accesso amministrativo a tutte le risorse nell'account di database.</p></td>
        </tr>
    </tbody>
</table>

Oltre a provisioning, configurazione e gestione di account del database dal portale di Azure, è possibile anche a livello di programmazione creare e gestire account di database DB Cosmos usando il [API REST di Azure Cosmos DB](/rest/api/documentdb/) nonché [client SDK](sql-api-sdk-dotnet.md).  

## <a name="databases"></a>Database
Un database di Cosmos DB è un contenitore logico di uno o più utenti e raccolte, come illustrato nel diagramma seguente. È possibile creare un numero qualsiasi di database in un account di database Cosmos DB, a condizione di rispettare i limiti di offerta.  

![Modello gerarchico di account di database e raccolte][2]  
**Un database è un contenitore logico di utenti e raccolte**

Un database può contenere risorse di archiviazione di documenti praticamente illimitate partizionate all'interno delle raccolte.

### <a name="elastic-scale-of-an-azure-cosmos-db-database"></a>Scalabilità elastica di un database di Azure Cosmos DB
Un database di Cosmos DB è elastico per impostazione predefinita e può includere da pochi GB a diversi petabyte di spazio di archiviazione per i documenti basato su SSD e velocità effettiva con provisioning. 

A differenza di un database RDBMS tradizionale, l'ambito di un database in Cosmos DB non è limitato a un singolo computer. Con Cosmos DB, in caso di crescita delle esigenze di scalabilità dell'applicazione, sarà possibile creare più raccolte, più database o entrambi. Molte applicazioni prodotte direttamente da Microsoft usano Azure Cosmos DB su scala consumer, creando database di Azure Cosmos DB molto grandi, ognuno dei quali include migliaia di raccolte con terabyte di spazio di archiviazione per i documenti. È possibile aumentare o ridurre le dimensioni di un database aggiungendo o rimuovendo raccolte per soddisfare i requisiti di scalabilità dell'applicazione. 

Il numero di raccolte che è possibile creare in un database dipende dall'offerta. Ogni raccolta dispone di risorse di archiviazione basate su SSD e velocità effettiva di cui è stato eseguito il provisioning in base al livello di prestazioni selezionato.

Un database di Azure Cosmos DB è anche un contenitore di utenti. Un utente, a sua volta, è uno spazio dei nomi logico per un set di autorizzazioni che fornisce un'autorizzazione e l'accesso alle raccolte, documenti e allegati.  

Come con altre risorse nel modello di risorse di Azure Cosmos DB, i database possono essere creati, sostituito, eliminare, leggere o enumerare facilmente utilizzando il [API REST](/rest/api/documentdb/) o una qualsiasi del [client SDK](sql-api-sdk-dotnet.md). Azure Cosmos DB assicura una coerenza assoluta per la lettura o l'esecuzione di query sui metadati di una risorsa del database. Se si elimina un database, non sarà automaticamente più possibile accedere alle raccolte o agli utenti inclusi nel database.   

## <a name="collections"></a>Raccolte
Una raccolta di Cosmos DB è un contenitore per i documenti JSON. 

### <a name="elastic-ssd-backed-document-storage"></a>Archiviazione flessibile di documenti basata su unità SSD
Una raccolta è intrinsecamente flessibile, poiché le dimensioni della raccolta aumentano o si riducono in seguito all'aggiunta o alla rimozione di documenti. Le raccolte sono risorse logiche e possono comprendere una o più partizioni fisiche o server. Il numero di partizioni in una raccolta è determinato da Cosmos DB in base allo spazio di archiviazione e alla velocità effettiva con provisioning della raccolta. Ogni partizione in Cosmos DB ha una quantità fissa di archiviazione supportata da unità SSD associata e viene replicata per la disponibilità elevata. Le partizioni vengono completamente gestite da Azure Cosmos DB e non è necessario scrivere codice complesso o gestire le partizioni. Le raccolte di Cosmos DB sono **praticamente illimitate** in termini di spazio di archiviazione e velocità effettiva. 

### <a name="automatic-indexing-of-collections"></a>Indicizzazione automatica delle raccolte
Azure Cosmos DB è un sistema di database realmente privo di schema. Non si presuppone o richiede alcuno schema per i documenti JSON. Azure Cosmos DB indicizza automaticamente i documenti aggiunti a una raccolta e li rende disponibili per l'esecuzione di query. L'indicizzazione automatica dei documenti senza schema o gli indici secondari è una funzionalità chiave di Azure Cosmos DB ed è abilitato per le tecniche di manutenzione dell'indice con ottimizzazione per la scrittura, senza blocco e organizzato in log. Azure Cosmos DB supporta un volume elevato di scritture estremamente veloci, gestendo al tempo stesso query coerenti. L'archiviazione documenti e l'archiviazione dell'indice sono usate per calcolare le risorse di archiviazione usate da ogni raccolta. È possibile controllare i compromessi tra archiviazione e prestazioni associati all'indicizzazione tramite la configurazione di un criterio di indicizzazione per una raccolta. 

### <a name="configuring-the-indexing-policy-of-a-collection"></a>Configurazione dei criteri di indicizzazione di una raccolta
Il criterio di indicizzazione di ogni raccolta rende possibili i compromessi tra prestazioni e archiviazione associati all'indicizzazione. Le opzioni seguenti sono disponibili come parte della configurazione dell'indicizzazione:  

* Possibilità di scegliere se la raccolta indicizza automaticamente o meno tutti i documenti. Per impostazione predefinita, saranno indicizzati automaticamente tutti i documenti. È possibile scegliere di disattivare l'indicizzazione automatica e aggiungere in modo selettivo solo documenti specifici all'indice. In alternativa, è possibile scegliere di escludere in modo selettivo solo documenti specifici. È possibile ottenere questo risultato impostando la proprietà automatica sia true o false in indexingPolicy di una raccolta e utilizzando l'intestazione della richiesta [x-ms-indexingdirective] durante l'inserimento, sostituzione o l'eliminazione di un documento.  
* Possibilità di scegliere se includere o escludere percorsi o modelli specifici nei documenti dall'indice. Per ottenere questo risultato, impostare rispettivamente includedPaths e excludedPaths in indexingPolicy di una raccolta. È anche possibile configurare i compromessi relativi ad archiviazione e prestazioni per query di intervallo e hash per modelli di percorso specifici. 
* Possibilità di scegliere tra aggiornamenti sincroni (coerenti) e asincroni (differiti) dell'indice. Per impostazione predefinita, l'indice è aggiornato in modo sincrono a ogni inserimento, sostituzione o eliminazione di un documento nella raccolta. Ciò permette alle query di rispettare lo stesso livello di coerenza delle letture di documenti. Anche se Azure Cosmos DB è ottimizzato per la scrittura e supporta volumi elevati di scritture di documenti, oltre a consentire la manutenzione sincrona dell'indice e la gestione di query coerenti, è possibile configurare determinate raccolte per l'aggiornamento differito dell'indice. L'indicizzazione differita migliora ulteriormente le prestazioni di scrittura ed è ideale per scenari di inserimento in blocco per raccolte principalmente a uso intensivo di lettura.

Il criterio di indicizzazione può essere modificato tramite l'esecuzione di un'operazione PUT sulla raccolta. Può essere ottenuta tramite il [client SDK](sql-api-sdk-dotnet.md), [portale di Azure](https://portal.azure.com) o [API REST](/rest/api/documentdb/).

### <a name="querying-a-collection"></a>Esecuzione di query su una raccolta
I documenti in una raccolta possono avere schemi arbitrari ed è possibile eseguire query sui documenti in una raccolta senza fornire anticipatamente alcuno schema o alcun indice secondario. È possibile eseguire una query nella raccolta usando il [riferimento alla sintassi SQL del database Azure Cosmos](https://msdn.microsoft.com/library/azure/dn782250.aspx), che fornisce RTF gerarchici, relazionali, spaziali e gli operatori ed estendibilità tramite le UDF basate su JavaScript. La grammatica JSON permette la modellazione di documenti JSON come alberi con etichette come nodi dell'albero. Questo viene sfruttato sia dalle tecniche di indicizzazione automatica dell'API di SQL come sottolinguaggio SQL del database di Azure Cosmos. Il linguaggio di query SQL è costituita da tre aspetti principali:   

1. Un set ridotto di operazioni di query mappate in modo naturale alla struttura ad albero, che include query e proiezioni gerarchiche. 
2. Un subset di operazioni relazionali inclusi composizione, filtro, proiezioni, aggregazioni e self-join. 
3. Funzioni definite dall'utente pure basate su JavaScript in grado di funzionare con (1) e (2).  

Il modello di query di database di Azure Cosmos tenta di raggiungere un equilibrio tra semplicità, efficienza e funzionalità. Il motore di database di Azure Cosmos DB compila ed esegue in modo nativo le istruzioni di query SQL. È possibile eseguire query su una raccolta usando le [API REST](/rest/api/documentdb/) o uno degli [SDK client](sql-api-sdk-dotnet.md). In .NET SDK è disponibile un provider LINQ.

> [!TIP]
> È possibile provare l'API di SQL ed eseguire query SQL nel set di dati nel [Query Playground](https://www.documentdb.com/sql/demo).
> 
> 

## <a name="multi-document-transactions"></a>Transazioni in più documenti
Le transazioni di database offrono un modello di programmazione sicuro e prevedibile per la gestione delle modifiche simultanee ai dati. In RDBMS la logica di business è tradizionalmente scritta tramite la scrittura di **stored procedure** e/o **trigger** ed è inviata al server database per l'esecuzione transazionale. In RDBMS il programmatore di applicazioni deve gestire due linguaggi di programmazione diversi: 

* L'applicazione (non transazionale) programming language (ad esempio, JavaScript, Python, c#, Java, ecc.)
* T-SQL, il linguaggio di programmazione transazionale in modo nativo viene eseguito dal database

In virtù dell'integrazione completa di JavaScript e JSON direttamente nel motore di database, Azure Cosmos DB offre un modello di programmazione intuitivo per eseguire la logica dell'applicazione basata su JavaScript direttamente nelle raccolte in termini di stored procedure e trigger. Questo offre entrambi i vantaggi seguenti:

* Implementazione efficiente del controllo della concorrenza, ripristino e indicizzazione automatica dei grafici di oggetti JSON direttamente nel motore di database.
* Naturalmente esprimere il flusso di controllo, variabili dell'ambito, l'assegnazione e integrazione di gestione delle eccezioni primitive con transazioni di database direttamente in termini di linguaggio di programmazione JavaScript

La logica JavaScript registrata a livello di raccolta può quindi rilasciare operazioni sui documenti della raccolta specifica. Azure Cosmos DB esegue implicitamente il wrapping di stored procedure e trigger basati su JavaScript in transazioni di ambiente ACID con isolamento degli snapshot nei documenti in una raccolta. Se JavaScript genera un'eccezione durante l'esecuzione, l'intera transazione sarà interrotta. Il modello di programmazione risultante è molto semplice ma efficace. Gli sviluppatori JavaScript ottengono un modello di programmazione "durevole", usando al tempo stesso i costrutti dei propri linguaggi preferiti e i primitivi di librerie.   

La possibilità di eseguire JavaScript direttamente nel motore di database nello stesso spazio di indirizzi del pool di buffer permette l'esecuzione efficiente e transazionale di operazioni di database nei documenti di una raccolta. Poiché il motore di database di Cosmos DB adotta completamente JSON e JavaScript, elimina eventuali mancate corrispondenze di impedenza tra i sistemi di tipi dell'applicazione e del database.   

Dopo aver creato una raccolta, è possibile registrare le stored procedure, trigger e funzioni definite dall'utente con un insieme di [API REST](/rest/api/documentdb/) o una qualsiasi del [client SDK](sql-api-sdk-dotnet.md). Dopo la registrazione, sarà possibile farvi riferimento ed eseguire questi elementi. La stored procedure seguente, scritta interamente in JavaScript, accetta due argomenti (titolo del libro e nome dell'autore) e crea un nuovo documento, esegue query per un documento e quindi lo aggiorna. Tutte queste operazioni sono eseguite tramite una transazione ACID implicita. Se in un punto qualsiasi dell'esecuzione viene generata un'eccezione JavaScript, l'intera transazione viene interrotta.

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

                        // Replace the author name for all documents that satisfied the query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don’t need to execute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);   
                        }
                    })
            })
    };

Il client può "inviare" la logica JavaScript precedente al database per l'esecuzione transazionale tramite POST HTTP. Per altre informazioni sull'uso di metodi HTTP, vedere [RESTful interactions with Azure Cosmos DB resources](https://msdn.microsoft.com/library/azure/mt622086.aspx) (Interazioni RESTful con risorse di Azure Cosmos DB). 

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


Poiché il database comprende in modo nativo JSON e JavaScript, non si verificano mancate corrispondenze tra sistemi di tipi né sono necessari "mapping OR" o generazione di codice.   

Le stored procedure e i trigger interagiscono con una raccolta e con i documenti in una raccolta tramite un modello a oggetti ben definito, che espone il contesto corrente della raccolta.  

Le raccolte nell'API di SQL possono essere create, eliminate, lettura o enumerato facilmente utilizzando il [API REST](/rest/api/documentdb/) o una qualsiasi del [client SDK](sql-api-sdk-dotnet.md). L'API di SQL fornisce sempre coerenza assoluta per la lettura o di query sui metadati di una raccolta. Se si elimina una raccolta, non sarà automaticamente più possibile accedere a documenti, allegati, stored procedure, trigger e funzioni UDF inclusi nella raccolta stessa.   

## <a name="stored-procedures-triggers-and-user-defined-functions-udf"></a>Stored procedure, trigger e funzioni definita dall'utente (UDF)
Come illustrato nella sezione precedente, è possibile scrivere logica dell'applicazione per l'esecuzione direttamente in una transazione nel motore del database. La logica dell'applicazione può essere scritta interamente in JavaScript e può essere modellata come una stored procedure, trigger o una funzione definita dall'utente. Il codice JavaScript all'interno di una stored procedure o trigger possa inserire, sostituire, eliminare, leggere o eseguire query sui documenti all'interno di una raccolta. Il codice JavaScript all'interno di una funzione definita dall'utente, invece, non può inserire, sostituire o eliminare documenti. Le funzioni definite dall'utente enumerano i documenti di un set di risultati di query e producono un altro set di risultati. Per multi-tenancy, DB Cosmos Azure applica una governance delle risorse basate su riserva strict. Ogni stored procedure, trigger o una funzione definita dall'utente ottiene un quantum risorse del sistema operativo di eseguire il lavoro fisso. Inoltre, stored procedure, trigger o funzioni definite dall'utente non è possibile collegare in librerie JavaScript esterne e sono disattivato se superano i budget di risorse allocati a essi. È possibile registrare, annullare la registrazione di stored procedure, trigger o funzioni definite dall'utente con una raccolta, usando le API REST.  Durante la registrazione una stored procedure, trigger o una funzione definita dall'utente è precompilato e archiviata come codice byte, che viene eseguito in un secondo momento. Il seguente illustrateshow ssection Azure Cosmos DB JavaScript SDK consente di registrare, eseguire e annullare la registrazione di una stored procedure, trigger e una funzione definita dall'utente. JavaScript SDK è un semplice wrapper per le [API REST](/rest/api/documentdb/). 

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
L'esecuzione di una stored procedure avviene tramite l'esecuzione di un metodo HTTP POST su una risorsa stored procedure esistente passando i parametri alla procedura nel corpo della richiesta.

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
La registrazione di un trigger è eseguita tramite la creazione di una nuova risorsa trigger in una raccolta tramite HTTP POST. È possibile specificare se il trigger è una versione preliminare o un trigger di inserimento e il tipo di operazione può essere associata a (ad esempio, Create, Replace, Delete o tutti).   

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
L'esecuzione di un trigger è effettuata specificando il nome di un trigger esistente contemporaneamente all'emissione della richiesta POST/PUT/DELETE di una risorsa documento tramite l'intestazione della richiesta.  

    client.createDocumentAsync(collection._self, { id: "doc1", key: "Love in the Time of Cholera" }, { preTriggerInclude: "upperCaseId" })
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

### <a name="executing-a-udf-as-part-of-the-query"></a>Esecuzione di una funzione UDF come parte della query
Una funzione definita dall'utente può essere specificato come parte della query SQL e viene utilizzato come un modo per estendere il nucleo [il linguaggio di query SQL](sql-api-sql-query-reference.md).

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

Sebbene i frammenti di codice precedente ha dimostrato la registrazione (POST), l'annullamento della registrazione (PUT), lettura/elenco (GET) ed esecuzione (POST) tramite il [JavaScript SDK](https://github.com/Azure/azure-documentdb-js), è inoltre possibile utilizzare il [API REST](/rest/api/documentdb/) o altri [client SDK](sql-api-sdk-dotnet.md). 

## <a name="documents"></a>Documenti
È possibile inserire, sostituire, eliminare, leggere, enumerare e documenti JSON arbitrari in una raccolta di query. Azure Cosmos DB non impone alcuno schema e non richiede indici secondari per il supporto delle query sui documenti di una raccolta. Le dimensioni massime per un documento sono pari a 2 MB.   

Essendo un servizio di database aperto realmente, Azure Cosmos DB inventare non tutti i tipi di dati speciali (ad esempio, data) o codifiche specifiche per i documenti JSON. DB Cosmos Azure non richiede le convenzioni JSON speciali per codificare le relazioni tra i vari documenti. la sintassi SQL di Azure Cosmos DB fornisce molto potente relazionale e gerarchica query agli operatori di query e progetto documenti senza annotazioni speciali o necessario codificare le relazioni tra i documenti utilizzando distinguono di proprietà.  

Come con tutte le altre risorse, documenti può essere creata, sostituito, eliminare, leggere, enumerati e individuato facilmente utilizzando le API REST o uno qualsiasi del [client SDK](sql-api-sdk-dotnet.md). Se si elimina un documento, la quota corrispondente a tutti gli allegati annidati sarà resa immediatamente disponibile. Il livello di coerenza di lettura dei documenti segue i criteri di coerenza applicati all'account di database. È possibile eseguire l'override di questo criterio per le singole richieste, in base ai requisiti di coerenza dei dati specifici dell'applicazione. Durante l'esecuzione di query nei documenti, la coerenza di lettura si basa sulla modalità di indicizzazione impostata per la raccolta. Ai fini della coerenza, si basa sui criteri di coerenza dell'account. 

## <a name="attachments-and-media"></a>Allegati e file multimediali
Azure Cosmos DB consente di archiviare BLOB/file multimediali binari con Azure Cosmos DB (al massimo 2 GB per account) o nel proprio archivio multimediale remoto. Permette anche di rappresentare i metadati dei file multimediali sotto forma di un documento speciale definito allegato. Un allegato in Azure Cosmos DB è un documento speciale (JSON) che fa riferimento a file multimediali/BLOB archiviati altrove. Un allegato è semplicemente un documento speciale che acquisisce i metadati di una media archiviato in un archivio remoto supporti (ad esempio, percorso, autore e così via). 

Si consideri un'applicazione di social networking di lettura che utilizza database Cosmos di Azure per archiviare le annotazioni a penna ed evidenzia metadati comprensivo di commenti, segnalibri, classificazioni, simili/preferenze e così via associati per un e-book di un determinato utente.   

* Il contenuto del libro stesso è archiviato nell'archivio multimediale disponibile come parte dell'account di database di Azure Cosmos DB o in un archivio multimediale remoto. 
* Un'applicazione potrebbe archiviare i metadati di ogni utente come documento distinct, ad esempio, i metadati di Joe per book1 sono archiviato in un documento a cui fa riferimento /colls/joe/docs/book1. 
* Allegati che punta al contenuto di pagine di un libro di un utente specifico vengono archiviate nel documento corrispondente, ad esempio, /colls/joe/docs/book1/chapter1, /colls/joe/docs/book1/chapter2 e così via. 

Gli esempi elencati sopra usano ID descrittivo per indicare la gerarchia di risorse. L'accesso alle risorse è effettuato tramite le API REST mediante ID di risorsa univoci. 

Per i supporti che sono gestiti da Azure Cosmos DB, la proprietà Media dell'allegato fa riferimento il supporto dal relativo URI. Azure Cosmos DB assicura la procedura di Garbage Collection del file multimediale dopo il rilascio di tutti i riferimenti in sospeso. Azure Cosmos DB genera automaticamente l'allegato quando si carica il nuovo file multimediale e popola la proprietà _media in modo che faccia riferimento ai nuovi file multimediali aggiunti. Se si sceglie di conservare i supporti in un archivio blob remoti gestito dall'utente (ad esempio OneDrive archiviazione di Azure, DropBox e così via), è possibile utilizzare ancora allegati per il supporto di riferimento. In questo caso sarà necessario creare personalmente l'allegato e popolarne la proprietà _media.   

Come con tutte le altre risorse, gli allegati possono essere creati, sostituito, eliminare, leggere o enumerare facilmente utilizzando le API REST o qualsiasi client SDK. Come per i documenti, il livello di coerenza di lettura degli allegati segue i criteri di coerenza applicati all'account di database. È possibile eseguire l'override di questo criterio per le singole richieste, in base ai requisiti di coerenza dei dati specifici dell'applicazione. Durante l'esecuzione di query relative agli allegati, la coerenza di lettura si basa sulla modalità di indicizzazione impostata per la raccolta. Ai fini della coerenza, si basa sui criteri di coerenza dell'account. 
 

## <a name="users"></a>Utenti
Un utente di Azure Cosmos DB rappresenta uno spazio dei nomi logico per il raggruppamento di autorizzazioni. Un utente di Azure Cosmos DB può corrispondere a un utente in un sistema di gestione delle identità o a un ruolo applicazione predefinito. In Azure Cosmos DB un utente rappresenta semplicemente un'astrazione per raggruppare un set di autorizzazioni in un database.   

Per l'implementazione di multi-tenancy nell'applicazione, è possibile creare utenti in Azure Cosmos DB, che corrisponde all'effettivi utenti o i tenant dell'applicazione. È quindi possibile creare autorizzazioni per un utente specifico, corrispondenti al controllo di accesso su diversi documenti, raccolte, allegati e così via.   

Poiché la scalabilità delle applicazione deve essere adeguata all'incremento degli utenti, è possibile adottare modi diversi per partizionare i dati. È possibile modellare ogni utente in modo che:   

* Ogni utente venga mappato a un database.
* Ogni utente venga mappato a una raccolta. 
* I documenti corrispondenti a più utenti passino a una raccolta dedicata. 
* I documenti corrispondenti a più utenti passino a un set di raccolte.   

Indipendentemente dalla strategia di partizionamento orizzontale scelta, è possibile modellare gli utenti effettivi come utenti nel database di Azure Cosmos DB e associare autorizzazioni dettagliate a ogni utente.  

![Raccolte degli utenti][3]  
**Strategie di partizionamento orizzontale e modellazione degli utenti**

Come tutte le altre risorse, gli utenti nel database di Azure Cosmos possono essere creati, sostituito, eliminare, leggere o enumerati facilmente utilizzando le API REST o qualsiasi client SDK. Azure Cosmos DB offre sempre una coerenza assoluta per la lettura o l'esecuzione di query sui metadati di una risorsa utente. È utile segnalare che se si elimina un utente, non sarà automaticamente più possibile accedere alle autorizzazioni incluse nell'utente stesso. Anche se Azure Cosmos DB recupera la quota di autorizzazioni come parte dell'utente eliminato in background, le autorizzazioni eliminate saranno disponibili immediatamente per un nuovo uso.  

## <a name="permissions"></a>Autorizzazioni
Da una prospettiva di controllo di accesso, sono considerate risorse quali gli account di database, database, gli utenti e autorizzazioni *amministrativi* risorse poiché questi richiedono le autorizzazioni amministrative. L'ambito di risorse quali raccolte, documenti, allegati, stored procedure, trigger e funzioni UDF invece è limitato a un database specifico e queste risorse sono considerate *risorse dell'applicazione*. Il modello di autorizzazione, che corrisponde ai due tipi di risorse e ai ruoli che vi accedono, ovvero l'amministratore e l'utente, definisce due tipi di *chiavi di accesso*: *chiave master* e *chiave risorsa*. La chiave master fa parte dell'account di database ed è fornita allo sviluppatore o all'amministratore che esegue il provisioning dell'account di database. La chiave master usa semantica di amministratore, ovvero può essere usata per autorizzare l'accesso alle risorse amministrative e dell'applicazione. La chiave di risorsa, invece, è una chiave di accesso granulare che permette l'accesso a una risorsa *specifica* dell'applicazione. Di conseguenza, acquisisce la relazione tra l'utente di un database e le autorizzazioni utente per una risorsa specifica (ad esempio, insieme, documento, allegati, stored procedure, trigger o funzione definita dall'utente).   

L'unico modo per ottenere una chiave di risorsa consiste nella creazione di una risorsa di autorizzazione per un utente specifico. Si noti che per creare o recuperare un'autorizzazione è necessario presentare una chiave master nell'intestazione dell'autorizzazione. Una risorsa di autorizzazione associa la risorsa, l'accesso e l'utente. Dopo la creazione di una risorsa di autorizzazione, l'utente dovrà solo presentare la chiave di risorsa associata per ottenere l'accesso alla risorsa rilevante. Una chiave di risorsa può essere quindi considerata come una rappresentazione logica e compatta della risorsa di autorizzazione.  

Come con tutte le altre risorse, è possono creare le autorizzazioni nel database di Azure Cosmos, sostituito, eliminare, leggere o enumerare facilmente utilizzando le API REST o qualsiasi client SDK. Azure Cosmos DB offre sempre una coerenza assoluta per la lettura o l'esecuzione di query sui metadati di un'autorizzazione. 

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'uso di risorse tramite comandi HTTP, vedere [RESTful interactions with Azure Cosmos DB resources](https://msdn.microsoft.com/library/azure/mt622086.aspx) (Interazioni di tipo RESTful con risorse di Azure Cosmos DB).

[1]: media/sql-api-resources/resources1.png
[2]: media/sql-api-resources/resources2.png
[3]: media/sql-api-resources/resources3.png

