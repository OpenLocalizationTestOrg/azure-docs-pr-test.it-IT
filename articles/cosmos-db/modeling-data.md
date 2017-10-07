---
title: dati del documento per un database NoSQL aaaModeling | Documenti Microsoft
description: Informazioni sulla modellazione dei dati per i database NoSQL
keywords: modellazione di dati
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig1
documentationcenter: 
ms.assetid: 69521eb9-590b-403c-9b36-98253a4c88b5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2016
ms.author: arramac
ms.openlocfilehash: 2e388c833f204287896dfa8e6f79c88073731b6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a>Modellazione dei dati di un documento per un database NoSQL
Database privi di schema, come Azure Cosmos DB, semplificano super tooembrace modello di dati tooyour modifiche ancora dedicare alcuni tempo concepire i dati. 

Dati modalità toobe archiviati? Quali sono i dati dell'applicazione continua tooretrieve e query? L'applicazione esegue un'intensa attività di lettura o un'intensa attività di scrittura? 

Dopo aver letto questo articolo, sarà in grado di tooanswer hello seguenti domande:

* Come si deve considerare un documento in un database di documenti?
* Cos'è la modellazione dei dati e perché è importante? 
* Come viene modellare i dati in un database relazionale di database diversi tooa documento?
* Come si esprimono le relazioni tra i dati in un database non relazionale?
* Quando si incorporano dati e quando si collega toodata?

## <a name="embedding-data"></a>Incorporamento dei dati
Quando si avvia modellazione dei dati in un archivio di documento, ad esempio Azure Cosmos DB, provare a tootreat le entità come **documenti indipendenti** rappresentato in JSON.

Prima di proseguire, è meglio fare un passo indietro e pensare a come sia possibile modellare qualcosa in un database relazionale, un argomento con cui molti hanno già familiarità. Hello esempio seguente viene illustrato come una persona potrebbe essere archiviata in un database relazionale. 

![Database relazionale](./media/documentdb-modeling-data/relational-data-model.png)

Quando si lavora con i database relazionali, è state illustrate per toonormalize anni, la normalizzazione, normalizzare.

Normalizzazione dei dati in genere implica l'esecuzione di un'entità, ad esempio una persona, nonché suddividere in toodiscrete porzioni di dati. Nell'esempio hello sopra, una persona può disporre di più record di informazioni di contatto, nonché di più record di indirizzo. È possibile andare oltre e suddividere i dettagli contatto estraendo anche i campi comuni come tipo. Lo stesso per l'indirizzo: ogni record qui ha un tipo, ad esempio *Abitazione* o *Ufficio* 

Guida locale quando normalizzazione dei dati è troppo Hello**evitare di archiviare dati ridondanti** in ogni record e invece fare riferimento toodata. In questo esempio, tooread una persona, con tutti i relativi dettagli di contatto e gli indirizzi, è necessario toouse join tooeffectively aggregare i dati in fase di esecuzione.

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

Per aggiornare una singola persona con i dettagli contatto e gli indirizzi, è necessario eseguire operazioni di scrittura in più tabelle. 

Ora è possibile osservare come si sarebbe modello hello stessi dati come entità indipendenti in un database di documenti.

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "addresses": [
            {            
                "line1": "100 Some Street",
                "line2": "Unit 1",
                "city": "Seattle",
                "state": "WA",
                "zip": 98012
            }
        ],
        "contactDetails": [
            {"email: "thomas@andersen.com"},
            {"phone": "+1 555 555-5555", "extension": 5555}
        ] 
    }

Approccio hello precedente abbiamo ora **denormalizzati** hello record utente in cui è **incorporato** tutti hello informazioni relative a toothis persona, ad esempio le informazioni di contatto e indirizzi in tooa singolo Documento JSON.
Inoltre, poiché non ci stiamo limitati tooa uno schema fisso che abbiamo hello flessibilità toodo quali con i dettagli di contatto di diverse forme completamente. 

Il recupero di un record utente completo dal database hello è ora una singola operazione su una singola raccolta e di un singolo documento di lettura. Anche l'aggiornamento del record di una persona, con i dettagli contatto e gli indirizzi, richiede una sola operazione di scrittura in un solo documento.

Da denormalizzazione dei dati, l'applicazione potrebbe essere necessario tooissue meno query e aggiornamenti toocomplete operazioni comuni. 

### <a name="when-tooembed"></a>Quando tooembed
In generale, usare i modelli di dati incorporati quando:

* Esistono relazioni **contains** tra le entità.
* Esistono relazioni **one-to-few** tra le entità.
* Esistono dati incorporati che **cambiano raramente**.
* Esistono dati incorporati che non aumenteranno **senza limiti**.
* Non ci sono dati incorporati che sono **integrale** toodata in un documento.

> [!NOTE]
> I modelli di dati denormalizzati garantiscono di solito prestazioni di **lettura** più elevate.
> 
> 

### <a name="when-not-tooembed"></a>Quando non tooembed
Mentre hello regola empirica in un database di documenti è toodenormalize tutto quello che incorpora tutti i dati nel documento singolo tooa, ciò può comportare situazioni toosome che dovrebbero essere evitate.

Consideriamo questo frammento JSON.

    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

Questo potrebbe essere l'aspetto di un'entità post con commenti incorporati, se si modellasse un tipico sistema di blog, o CMS. problema con questo esempio Hello è tale hello matrice commenti è **unbounded**, non ovvero non esiste alcun toohello (pratiche) limitazione del numero dei commenti può avere qualsiasi singolo post. Dimensioni di hello del documento hello potrebbero aumentare notevolmente diventerà un problema.

Come dimensione hello di hello documento aumenta dati hello tootransmit possibilità di hello in transito hello, nonché la lettura e aggiornamento documento hello, su larga scala, sarà interessato.

In questo caso sarebbe migliore hello tooconsider seguente modello.

    Post document:
    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from hello field"},
            ...
            {"id": 99, "author": "angry", "comment": "blah angry blah angry"}
        ]
    },
    {
        "postId": "1"
        "comments": [
            {"id": 100, "author": "anon", "comment": "yet more"},
            ...
            {"id": 199, "author": "bored", "comment": "will this ever end?"}
        ]
    }

Questo modello contiene i commenti più recente di hello tre incorporati in hello post stessa, ovvero una matrice con un limite fisso in questo momento. Hello altri commenti vengono raggruppati in toobatches dei 100 commenti e archiviate in documenti distinti. dimensioni di Hello di hello batch è stato scelto come 100 perché l'applicazione fittizia consente hello 100 commenti tooload dell'utente alla volta.  

Un altro caso in cui incorporare i dati non sono una buona idea è quando hello incorporato dati vengono utilizzati spesso in documenti e verranno modificati di frequente. 

Consideriamo questo frammento JSON.

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            {
                "numberHeld": 100,
                "stock": { "symbol": "zaza", "open": 1, "high": 2, "low": 0.5 }
            },
            {
                "numberHeld": 50,
                "stock": { "symbol": "xcxc", "open": 89, "high": 93.24, "low": 88.87 }
            }
        ]
    }

Questo potrebbe essere il portafoglio azionario di una persona. Informazioni sui titoli di hello tooembed scelto nel documento portfolio tooeach. Incorporamento di dati che cambiano frequentemente in un ambiente in cui i dati correlati cambia di frequente, ad esempio un'applicazione che, in corso toomean che si sta aggiornando ogni documento portfolio costantemente ogni volta che vengono scambiate un azioni.

Il titolo *zaza* potrebbe essere scambiato diverse centinaia di volte in un solo giorno e migliaia di utenti potrebbero avere *zaza* nel portafoglio. Con un modello di dati come hello sopra sono tooupdate molte migliaia di documenti portfolio molte volte ogni giorno tooa sistema che non verrà ridimensionato molto bene. 

## <a id="Refer"></a>Dati di riferimento
L'incorporamento dei dati quindi funziona senza problemi in molti casi, ma è evidente che in altri scenari la denormalizzazione dei dati è più che altro causa di problemi. Cosa si può fare dunque? 

Database relazionali non sono unico luogo hello in cui è possibile creare relazioni tra entità. In un database di documenti è possibile disporre di informazioni in un documento che effettivamente si riferisce toodata in altri documenti. A questo punto, sono non, promuovendo anche un minuto è creare sistemi che sarebbero migliori tooa adatto di database relazionale nel database di Azure Cosmos o qualsiasi altro database di documento, ma relazioni semplici sono supportate e possono essere molto utili. 

In hello JSON seguente è stato scelto toouse hello ad esempio un portafoglio di titoli da versioni precedenti ma questa volta che viene fatto riferimento toohello magazzino nel portfolio di hello anziché incorporarlo. In questo modo, quando in magazzino hello cambiano frequentemente in tutta hello giorno hello solo documento toobe aggiornato è documento azionari singolo hello. 

    Person document:
    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            { "numberHeld":  100, "stockId": 1},
            { "numberHeld":  50, "stockId": 2}
        ]
    }

    Stock documents:
    {
        "id": "1",
        "symbol": "zaza",
        "open": 1,
        "high": 2,
        "low": 0.5,
        "vol": 11970000,
        "mkt-cap": 42000000,
        "pe": 5.89
    },
    {
        "id": "2",
        "symbol": "xcxc",
        "open": 89,
        "high": 93.24,
        "low": 88.87,
        "vol": 2970200,
        "mkt-cap": 1005000,
        "pe": 75.82
    }


Un approccio toothis immediato svantaggio, tuttavia è se l'applicazione è necessario tooshow informazioni ogni titolo che viene mantenuto per la visualizzazione di raccolte di progetti di una persona; In questo caso sarà necessario toomake più trip toohello tooload hello informazioni sul database per ogni documento predefinita. Di seguito sono stati apportati efficienza di hello tooimprove una decisione di operazioni di scrittura, che si verifica frequentemente durante il giorno hello, ma anche a sua volta su hello operazioni potenzialmente con un impatto minore sulle prestazioni di hello questo particolare sistema di lettura.

> [!NOTE]
> I modelli di dati normalizzato **può richiedere più round trip** toohello server.
> 
> 

### <a name="what-about-foreign-keys"></a>Chiavi esterne
Poiché attualmente non è disponibile alcun concetto di un vincolo, chiave esterna o in caso contrario, tutte le relazioni tra i documenti contenenti nei documenti sono effettivamente "punti deboli" e non verranno verificate dal database hello stesso. Se si desidera tooensure che hello dati che fa riferimento un documento tooactually esista, quindi è necessario toodo questo nell'applicazione o tramite l'utilizzo di hello del lato server trigger o stored procedure nel database di Azure Cosmos.

### <a name="when-tooreference"></a>Quando tooreference
In generale, usare i modelli di dati denormalizzati quando:

* Si rappresentano relazioni **uno a molti** .
* Si rappresentano relazioni **molti a molti** .
* I dati correlati **cambiano spesso**.
* È possibile che i dati a cui si fa riferimento **non siamo limitati**.

> [!NOTE]
> La normalizzazione offre di solito migliori prestazioni di **scrittura** .
> 
> 

### <a name="where-do-i-put-hello-relationship"></a>Posizionamento di relazione hello
aumento delle dimensioni Hello di relazione hello consentono di determinare in quale riferimento hello toostore del documento.

Se si esamina hello JSON seguente che modella i server di pubblicazione e la documentazione.

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over hello world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in tooAzure Cosmos DB" }

Se il numero di hello di libri hello al server di pubblicazione è ridotto con crescita limitata, può risultare utile la memorizzazione dei hello libro di riferimento interno hello publisher documento. Tuttavia, se il numero di hello di documentazione per ogni server di pubblicazione è non associato, questo modello di dati potrebbe causare toomutable, aumento delle dimensioni di matrici, come hello esempio server di pubblicazione nel documento precedente. 

Cambio di diversi elementi un bit sarebbe risultato in un modello che rappresenta ancora hello stessi dati ma ora consente di evitare questi grandi raccolte modificabile.

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over hello world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in tooAzure Cosmos DB", "pub-id": "mspress"}

In hello esempio precedente, è stato eliminato hello unbounded insieme nel documento di publisher hello. Invece è disponibile solo un server di pubblicazione di toohello riferimento nel documento di ciascun libro.

### <a name="how-do-i-model-manymany-relationships"></a>Come modellare le relazioni many:many?
In un database relazionale le relazioni *molti a molti* vengono spesso modellate con le tabelle join, che creano un join dei record delle altre tabelle. 

![Unione di tabelle](./media/documentdb-modeling-data/join-table.png)

Potrebbe essere tentati tooreplicate hello stessa operazione usando i documenti e producono un modello di dati che sembra simile toohello seguente.

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over hello world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in tooAzure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

Funzionerebbe, Tuttavia, il caricamento di entrambi un autore e la documentazione o il caricamento di un libro con autore, sempre richiede almeno due query aggiuntive hello database. Unione di documenti e quindi un'altra query toofetch hello documento effettivo da unire in join toohello di una query. 

Se la tabella join si limita a incollare insieme due gruppi di dati, allora perché non eliminarla del tutto?
Prendere in considerazione i seguenti hello.

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

A questo punto, se ci fosse un autore, posso sapere immediatamente quali libri che hanno scritto e viceversa se è stato caricato un documento di libro SO ID hello degli autori hello. Ciò consente di risparmiare intermediario query sulla tabella di join hello riducendo il numero di hello del server dell'applicazione è toomake di round trip. 

## <a id="WrapUp"></a>Modelli di dati ibridi
Come si è visto, sia l'incorporamento (o denormalizzazione) che il riferimento (o normalizzazione) ai dati presentano vantaggi e compromessi. 

L'operazione non sempre disporre di un toobe o, non essere toomix impaurito operazioni backup a breve. 

In base a modelli di utilizzo specifico e i carichi di lavoro può accadere in combinazione incorporata dell'applicazione e dati di riferimento ha senso e Impossibile logica dell'applicazione responsabile toosimpler con server meno round trip pur mantenendo un buon livello di prestazioni .

Prendere in considerazione hello seguente JSON. 

    Author documents: 
    {
        "id": "a1",
        "firstName": "Thomas",
        "lastName": "Andersen",        
        "countOfBooks": 3,
         "books": ["b1", "b2", "b3"],
        "images": [
            {"thumbnail": "http://....png"}
            {"profile": "http://....png"}
            {"large": "http://....png"}
        ]
    },
    {
        "id": "a2",
        "firstName": "William",
        "lastName": "Wakefield",
        "countOfBooks": 1,
        "books": ["b1"],
        "images": [
            {"thumbnail": "http://....png"}
        ]
    }

    Book documents:
    {
        "id": "b1",
        "name": "Azure Cosmos DB 101",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
            {"id": "a2", "name": "William Wakefield", "thumbnailUrl": "http://....png"}
        ]
    },
    {
        "id": "b2",
        "name": "Azure Cosmos DB for RDBMS Users",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
        ]
    }

Qui è stata seguita (principalmente) modello incorporato hello, in cui i dati da altre entità sono incorporati nel documento di primo livello hello, ma fa riferimento ad altri dati. 

Se si esamina il documento di libro hello, possiamo vedere alcuni interessanti campi quando si esamina la matrice hello degli autori. È presente un *id* campo campo hello utilizziamo documento di autore di toorefer tooan indietro, procedura standard in un modello normalizzato, ma è anche avere *nome* e *thumbnailUrl*. È possibile avere solo bloccato con *id* e ha lasciato tooget applicazione hello eventuali informazioni aggiuntive necessarie dal documento di autore rispettivi hello utilizzando hello "collegamento", ma poiché l'applicazione consente di visualizzare il nome dell'autore hello e un immagine di anteprima con ogni libro visualizzato per salvare un server di andata e ritorno toohello per ogni libro in un elenco da denormalizzazione **alcuni** dati da un autore hello.

Assicurarsi che, se il nome dell'autore hello modificato o volevano tooupdate le foto sono toogo un aggiornamento ogni libro viene sempre la pubblicazione, ma per l'applicazione, in base a ipotesi di hello che gli autori di non modificare i relativi nomi, molto spesso, si tratta di una progettazione accettabile decisione.  

Nell'esempio hello esistono **pre-calcolate aggregazioni** valori toosave costosa l'elaborazione in un'operazione di lettura. Nell'esempio hello, alcuni dati hello incorporati nel documento di autore hello sono dati che viene calcolati in fase di esecuzione. Ogni volta che un nuovo libro viene pubblicato, viene creato un documento di libro **e** campo countOfBooks hello è impostato un valore tooa calcolato in base al numero di hello libro di documenti esistenti per un determinato autore. Questa ottimizzazione sono utili nei sistemi pesanti letti in cui che possiamo permetterci toodo calcoli su operazioni di scrittura in ordine toooptimize legge.

Hello toohave possibilità è reso possibile un modello con campi pre-calcolati perché supporta Azure Cosmos DB **transazioni più documenti**. Molti archivi NoSQL non possono eseguire transazioni in tutti i documenti e pertanto sostenere decisioni di progettazione, ad esempio "sempre incorpora tutti gli elementi", a causa di limitazione toothis. Con Azure Cosmos DB è possibile usare trigger lato server, o stored procedure, che inseriscono i libri e aggiornano gli autori in una sola transazione ACID. Ora non sono presenti **hanno** tooembed tutti gli elementi di tooone documento toobe sufficiente Assicurarsi che i dati rimangono coerenti.

## <a name="NextSteps"></a>Passaggi successivi
informazioni chiave più grande di Hello in questo articolo è toounderstand che modellazione dei dati in un mondo privi di schema sono importanti che mai. 

Come non è presente alcun toorepresent modo solo una parte dei dati in una schermata, non è toomodel alcun modo singolo i dati. È necessario toounderstand l'applicazione e come verrà generato, utilizzare ed elaborare dati hello. Quindi, applicando alcune hello linee guida riportate qui è possono impostare sulla creazione di un modello che risponde alle esigenze immediate hello dell'applicazione. Quando le applicazioni devono toochange, è possibile sfruttare la flessibilità di hello di un tooembrace privi di schema di database che modificano ed evolvere facilmente il modello di dati. 

toolearn ulteriori informazioni su Azure Cosmos DB, fare riferimento del servizio toohello [documentazione](https://azure.microsoft.com/documentation/services/cosmos-db/) pagina. 

toounderstand come tooshard i dati tra più partizioni, fare riferimento troppo[partizionamento dei dati nel database di Azure Cosmos](documentdb-partition-data.md). 
