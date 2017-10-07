---
title: 'Azure Cosmos DB: API di DocumentDB | Microsoft Docs'
description: "Informazioni su come è possibile utilizzare Azure Cosmos DB toostore e query grandi volumi di documenti JSON con una latenza bassa con SQL e JavaScript."
keywords: database JSON, database di documenti
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 686cdd2b-704a-4488-921e-8eefb70d5c63
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/22/2017
ms.author: mimig
ms.openlocfilehash: c96dfa5e2685782a99d2bcaf992f88dd2bef920b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-documentdb-api"></a>Introduzione tooAzure DB Cosmos: l'API DocumentDB

[Azure Cosmos DB](introduction.md) è il servizio di database multimodello distribuito a livello globale di Microsoft per applicazioni cruciali. DB Cosmos Azure fornisce [distribuzione globale di chiavi in mano](distribute-data-globally.md), [scalabilità elastica di velocità effettiva e l'archiviazione](partition-data.md) latenze millisecondo in tutto il mondo, a una cifra a percentile 99th hello, [cinque livelli di coerenza ben definiti](consistency-levels.md)e garantisce la disponibilità elevata, tutti i backup da [SLA leader del settore](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure DB Cosmos [automaticamente i dati di indici](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) senza toodeal con la gestione dello schema e indice. Si tratta di un database multimodello che supporta modelli di dati di documenti, coppie chiave-valore, grafi e colonne. 

![API di Azure DocumentDB](./media/documentdb-introduction/cosmosdb-documentdb.png) 

Con l'API DocumentDB hello, Azure Cosmos DB fornisce rich e familiare [funzionalità di query SQL](documentdb-sql-query.md) con latenza bassa coerente sui dati JSON senza schema. In questo articolo viene fornita una panoramica di hello Azure Cosmos DB DocumentDB API e come è possibile usarlo toostore volumi notevole di dati JSON, eseguire una query all'interno di ordine di latenza millisecondi ed evolvere facilmente schema hello. 

## <a name="what-capabilities-and-key-features-does-azure-cosmos-db-offer"></a>Capacità e funzionalità chiave offerte da Azure Cosmos DB
Azure DB Cosmos, tramite l'API DocumentDB hello offre hello seguenti vantaggi e funzionalità principali:

* **Velocità effettiva altamente scalabile e archiviazione:** facilmente ridurre o aumentare verso il basso il toomeet database JSON dell'applicazione è necessario. I dati sono archiviati in unità SSD (Solid State Drive) per garantire livelli di latenza bassi e prevedibili. DB Cosmos Azure supporta i contenitori per l'archiviazione dei dati JSON chiamata raccolte che possono essere ridimensionati toovirtually le dimensioni di archiviazione senza limiti e velocità effettiva di provisioning. Azure Cosmos DB offre una semplice scalabilità elastica e prestazioni prevedibili in base alla crescita dell'applicazione. 


* **Replica di tipo multiarea:** DB Cosmos Azure vengono replicati in modo trasparente le aree di tooall dati è stata associata con l'account di Azure Cosmos DB, consentendo toodevelop applicazioni che richiedono accesso globale toodata fornendo compromessi tra la coerenza, disponibilità e prestazioni, tutte le garanzie corrispondente. DB Cosmos Azure fornisce il failover regionale trasparente con le API multihosting e velocità effettiva di scala hello possibilità tooelastically e archiviazione tutto il mondo hello. Per altre informazioni, vedere [Distribuire i dati a livello globale con Azure Cosmos DB](distribute-data-globally.md).

* **Query ad hoc con sintassi SQL familiare:** è possibile archiviare documenti JSON eterogenei ed eseguire query su di essi usando una sintassi SQL familiare. DB Cosmos Azure prevede l'utilizzo di un blocco strettamente simultaneo, gratuito, log strutturato dell'indice di indicizzazione tecnologia tooautomatically tutto il contenuto del documento. In questo modo RTF query in tempo reale senza hint di hello necessità toospecify dello schema, gli indici secondari o viste. Per altre informazioni, vedere [Query in Azure Cosmos DB](documentdb-sql-query.md). 
* **Esecuzione di JavaScript all'interno del database hello:** esprimere la logica dell'applicazione come stored procedure, trigger e funzioni definite dall'utente (UDF) utilizzando JavaScript standard. In questo modo il toooperate logica dell'applicazione sui dati senza doversi preoccupare hello mancata corrispondenza tra un'applicazione hello e lo schema del database hello. Hello API DocumentDB consente l'esecuzione transazionale completo della logica dell'applicazione JavaScript direttamente nel motore di database hello. integrazione perfetta di Hello di JavaScript consente l'esecuzione di hello di INSERT, REPLACE, DELETE e operazioni di selezione da un programma JavaScript come una transazione di tipo isolata. Ulteriori informazioni sono disponibili in [Programmazione sul lato server di DocumentDB](programming.md).

* **Livelli di coerenza ottimizzabili:** selezionare da cinque ben definita compromesso ottimale tooachieve livelli di coerenza tra prestazioni e coerenza. Per query e operazioni di lettura, Azure Cosmos DB offre cinque livelli di coerenza distinti, ovvero avanzata, con decadimento ristretto, sessione, prefisso coerente e futura. Questi livelli di coerenza granulari, ben definiti, consentono di toomake audio compromessi tra la coerenza, disponibilità e latenza. Altre informazioni, vedere [con coerenza i livelli di prestazioni e disponibilità toomaximize](consistency-levels.md).

* **Completamente gestito:** eliminare hello necessità toomanage risorse database e computer. Come servizio completamente gestito, Microsoft Azure eseguire non è necessario toomanage le macchine virtuali, distribuire e configurare il software, gestire la scalabilità o gestire gli aggiornamenti a livello di dati complessi. Il backup di ogni database è eseguito automaticamente e ogni database è protetto da errori nell'area geografica specifica. Facilmente, è possibile aggiungere un account Azure Cosmos DB e il provisioning di capacità in base alle esigenze, consentendo di toofocus nell'applicazione anziché operativo e la gestione del database. 

* **Progettazione aperta:** è possibile iniziare subito a lavorare usando le competenze e gli strumenti esistenti. Programmazione per hello API DocumentDB è semplice e accessibile e non occorre tooadopt nuovi strumenti o rispettare toocustom estensioni tooJSON o JavaScript. È possibile accedere a tutte hello funzionalità dei database inclusi CRUD, query e l'elaborazione tramite una semplice interfaccia di servizi HTTP di JavaScript. l'API DocumentDB Hello basata sul modello formati esistenti, i linguaggi e gli standard offrendo funzionalità di base, dei database di valore elevato.

* **L'indicizzazione automatica:** per impostazione predefinita, Azure Cosmos DB automaticamente gli indici di tutti i documenti hello database hello e non prevede né richiede qualsiasi schema o la creazione di indici secondari. Evitare di dover tooindex tutti gli elementi? è anche possibile [rifiutare esplicitamente i percorsi nei file JSON](indexing-policies.md).

* **Modifica feed supporto:** feed modifica fornisce un elenco ordinato di documenti all'interno di una raccolta di Azure Cosmos DB nell'ordine di hello in cui essi sono stati modificati. Questo feed può essere utilizzato toolisten per toodata modifiche nei dati tooreplicate ordine, attivare le chiamate API o eseguire l'elaborazione del flusso per gli aggiornamenti. Feed di modifica è automaticamente abilitata toouse: [ulteriori informazioni sulla modifica di feed](https://docs.microsoft.com/azure/cosmos-db/change-feed). 

## <a name="data-management"></a>Come si gestiscono i dati con l'API DocumentDB hello?
Hello API DocumentDB consente di gestire i dati JSON tramite le risorse del database ben definito. Queste risorse sono replicate per ottenere disponibilità elevata e sono indirizzabili in modo univoco da parte dei rispettivi URI logici. Hello API DocumentDB offre un semplice HTTP basato su modello di programmazione REST per tutte le risorse. 


account del database Azure Cosmos DB Hello è uno spazio dei nomi univoco che consente di accedere ai tooAzure DB Cosmos. Prima di poter creare un account di database, è necessario disporre di una sottoscrizione di Azure, che consente di accedere a tooa vasta gamma di servizi di Azure. 

Tutte le risorse disponibili in Azure Cosmos DB sono modellate e archiviate come documenti JSON. Le risorse sono gestite come elementi, ovvero documenti JSON contenenti metadati, e come feed, ovvero raccolte di elementi. Gli insiemi di elementi sono inclusi nei rispettivi feed.

immagine di Hello seguente mostra le relazioni di hello tra le risorse di Azure Cosmos DB hello:

![relazione gerarchica di Hello tra le risorse nel database di Azure Cosmos][1] 

Un account di database è costituito da un insieme di database, ognuno dei quali include più raccolte, che possono contenere stored procedure, trigger, UDF, documenti e allegati correlati. Un database anche è associati utenti, ognuno con un set di autorizzazioni tooaccess varie altre raccolte, stored procedure, trigger, funzioni definite dall'utente, documenti o gli allegati. Mentre i database, gli utenti, le autorizzazioni e le raccolte sono risorse definite dal sistema con schemi noti, i documenti, le stored procedure, i trigger, le funzioni UDF e gli allegati includono contenuto JSON arbitrario definito dagli utenti.  

> [!NOTE]
> Poiché è stato in precedenza disponibile come servizio di Azure DocumentDB hello hello API DocumentDB, è possibile continuare tooprovision, monitorare e gestire gli account creati tramite hello API REST di gestione risorse di Azure o utilizzando strumenti hello Azure DocumentDB o Azure Cosmos DB nomi delle risorse. Utilizziamo nomi hello in modo intercambiabile quando si fa riferimento toohello APIs DocumentDB di Azure. 

## <a name="develop"></a>Come è possibile sviluppare App con l'API DocumentDB hello?

Azure Cosmos DB espone risorse tramite hello API REST che possono essere chiamati da qualsiasi linguaggio in grado di effettuare richieste HTTP/HTTPS. Inoltre, offriamo librerie di programmazione per numerosi linguaggi più diffusi per hello API DocumentDB. le librerie client Hello semplificano molti aspetti dell'utilizzo di API hello gestendo i dettagli, ad esempio la memorizzazione nella cache di indirizzo, gestione delle eccezioni, tentativi automatici e così via. Le librerie sono attualmente disponibili per hello seguenti linguaggi e piattaforme:  

| Scaricare | Documentazione |
| --- | --- |
| [.NET SDK](http://go.microsoft.com/fwlink/?LinkID=402989) |[Libreria .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) |
| [Node.js SDK](http://go.microsoft.com/fwlink/?LinkID=402990) |[Libreria Node.js](http://azure.github.io/azure-documentdb-node/) |
| [SDK per Java](http://go.microsoft.com/fwlink/?LinkID=402380) |[Libreria Java](/java/api/com.microsoft.azure.documentdb) |
| [JavaScript SDK](http://go.microsoft.com/fwlink/?LinkID=402991) |[Libreria JavaScript](http://azure.github.io/azure-documentdb-js/) |
| n/d |[JavaScript SDK lato server](http://azure.github.io/azure-documentdb-js-server/) |
| [Python SDK](https://pypi.python.org/pypi/pydocumentdb) |[Libreria di Python](http://azure.github.io/azure-documentdb-python/) |
| N/D | [API per MongoDB](mongodb-introduction.md)


Utilizzo di hello [Azure Cosmos DB emulatore](local-emulator.md), è possibile sviluppare e testare l'applicazione in locale con l'API DocumentDB hello senza creare una sottoscrizione di Azure o eventuali costi. Quando si è soddisfatti delle modalità di funzionamento dell'applicazione nell'emulatore hello, è possibile passare un account Azure Cosmos DB nel cloud hello toousing.

Oltre a basic creare, leggere, aggiornare e le operazioni, l'API DocumentDB fornisce un'interfaccia di query SQL completa per il recupero di documenti JSON e supporto sul lato server per l'esecuzione transazionale JavaScript logica dell'applicazione hello di eliminazione. interfacce di esecuzione di query e script Hello sono disponibili tramite tutte le librerie di piattaforma, nonché hello API REST. 

### <a name="sql-query"></a>Query SQL
Hello API DocumentDB supporta l'esecuzione di query su documenti utilizzando un linguaggio SQL, è possibile eseguire in hello JavaScript digitare sistema e le espressioni con supporto per le query spaziali relazionale e gerarchiche. linguaggio di query di DocumentDB Hello è un campo documenti JSON tooquery interfaccia semplice e potente. linguaggio Hello supporta un sottoinsieme di grammatica SQL ANSI e aggiunge l'integrazione di oggetti, matrici, la costruzione di oggetti e chiamata di funzione JavaScript. Hello API DocumentDB fornisce il modello di query senza hint di indicizzazione o di qualsiasi schema esplicito dallo sviluppatore hello.

Funzioni definite dall'utente (UDF) possono essere registrate con l'API DocumentDB hello e farvi riferimento come parte di una query SQL, in tal modo si estende la logica dell'applicazione personalizzata hello grammatica toosupport. Queste funzioni definite dall'utente sono scritti come i programmi di JavaScript ed eseguita all'interno del database hello. 

Per gli sviluppatori di .NET, hello API DocumentDB [.NET SDK](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.aspx) offre inoltre un provider di query LINQ. 

### <a name="transactions-and-javascript-execution"></a>Transazioni ed esecuzione di JavaScript
Hello API DocumentDB consente la logica dell'applicazione toowrite come programmi denominati interamente scritti in JavaScript. Questi programmi sono registrati per una raccolta e possono eseguire operazioni di database su documenti hello all'interno di una raccolta specificata. Il codice JavaScript può essere registrato per l'esecuzione come trigger, stored procedure o funzione UDF. Stored procedure e trigger possono creare, leggere, aggiornare ed eliminare documenti mentre eseguono funzioni definite dall'utente come parte della logica di esecuzione di query hello senza accesso in scrittura toohello insieme.

Esecuzione di JavaScript all'interno di hello Cosmos DB è modellato concetti hello supportati dai sistemi di database relazionale, con JavaScript, come sostituzione moderna Transact-SQL. Tutta la logica JavaScript è eseguita in una transazione di ambiente ACID con isolamento dello snapshot. Durante l'esecuzione, hello se hello JavaScript verrà generata un'eccezione, quindi hello dell'intera transazione viene interrotta.

## <a name="are-there-any-online-courses-on-azure-cosmos-db"></a>Disponibilità di corsi online su Azure Cosmos DB

È disponibile un corso della [Microsoft Virtual Academy](https://mva.microsoft.com/en-US/training-courses/azure-documentdb-planetscale-nosql-16847) su Azure DocumentDB. 

>[!VIDEO https://mva.microsoft.com/en-US/training-courses-embed/azure-documentdb-planetscale-nosql-16847]
>
>

## <a name="next-steps"></a>Passaggi successivi
Se si ha già un account di Azure, è possibile iniziare a usare Azure Cosmos DB seguendo le [guide introduttive](../cosmos-db/create-documentdb-dotnet.md), che illustrano come creare un account e iniziare a usare Cosmos DB.

[1]: ./media/documentdb-introduction/json-database-resources1.png

