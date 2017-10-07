---
title: Introduzione tooAzure Cosmos DB Graph API | Documenti Microsoft
description: "Informazioni su come è possibile utilizzare Azure Cosmos DB toostore, query e grafici massive incrociato con una latenza bassa utilizzando hello hello Gremlin grafico linguaggio di query di Apache TinkerPop."
services: cosmos-db
author: dennyglee
documentationcenter: 
ms.assetid: b916644c-4f28-4964-95fe-681faa6d6e08
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/21/2017
ms.author: denlee
ms.openlocfilehash: a4e79a4aa27976966baf0554928026177991ff69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-graph-api"></a>Introduzione tooAzure DB Cosmos: API Graph

[Azure DB Cosmos](introduction.md) è hello servizio di database distribuita a livello globale e più modelli da Microsoft per applicazioni di importanza strategica. DB Cosmos Azure fornisce [distribuzione globale di chiavi in mano](distribute-data-globally.md), [scalabilità elastica di velocità effettiva e l'archiviazione](partition-data.md) latenze millisecondo in tutto il mondo, a una cifra a percentile 99th hello, [cinque livelli di coerenza ben definiti](consistency-levels.md)e garantisce la disponibilità elevata, supportato da [SLA leader del settore](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure DB Cosmos [automaticamente i dati di indici](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) senza toodeal con la gestione dello schema e indice. Si tratta di un database multimodello che supporta modelli di dati di documenti, coppie chiave-valore, grafi e colonne.

![Gremlin, Graph e Azure Cosmos DB](./media/graph-introduction/graph-gremlin.png)

fornisce l'API Graph di Azure Cosmos DB Hello:

- Modellazione di grafi
- API di attraversamento
- Distribuzione globale chiavi in mano
- Scalabilità elastica di archiviazione e la velocità effettiva con meno di 10 ms, latenza di lettura e meno di 15 ms al dato percentile 99th hello
- Indicizzazione automatica con disponibilità di query immediata
- Livelli di coerenza regolabili
- Contratti di servizio completi con disponibilità al 99,99%

tooquery DB Cosmos Azure, è possibile utilizzare hello [TinkerPop Apache](http://tinkerpop.apache.org) grafico Java attraversamento [Gremlin](http://tinkerpop.apache.org/docs/current/reference/#graph-traversal-steps), o, ad esempio altri sistemi di grafico compatibili con TinkerPop [Apache Spark GraphX](spark-connector-graph.md).

In questo articolo viene fornita una panoramica dell'API Graph di Azure Cosmos DB hello e viene spiegato come è possibile usarlo toostore massive grafici con miliardi di vertici e bordi. È possibile eseguire una query con una latenza millisecondo grafici hello ed evolvere facilmente lo schema e struttura grafico hello.

## <a name="graph-database"></a>Database del grafo
Dati così come appare nel mondo reale hello naturalmente sono connesso. La modellazione di dati tradizionale si basa sul concetto di entità. Per molte applicazioni, è inoltre disponibile un toomodel necessità o toomodel relazioni ed entità naturalmente.

Un [grafo](http://mathworld.wolfram.com/Graph.html) è una struttura composta da [vertici](http://mathworld.wolfram.com/GraphVertex.html) e [bordi](http://mathworld.wolfram.com/GraphEdge.html). I vertici e gli archi possono avere un numero arbitrario di proprietà. I vertici identificano gli oggetti distinti, ad esempio una persona, un luogo o un evento. Gli archi indicano le relazioni tra i vertici. Ad esempio, una persona potrebbe conoscere un'altra persona, essere coinvolta in un evento e recentemente essersi trovata in una determinata posizione. Proprietà express informazioni sui bordi e vertici hello. Le proprietà di esempio includono un vertice con un nome, un'età e un bordo con un indicatore data e ora e/o un peso. Ufficialmente questo modello è noto come [grafo di proprietà](http://tinkerpop.apache.org/docs/current/reference/#intro). DB Cosmos Azure supporta modello di grafico proprietà hello.

Ad esempio, di esempio di grafico Mostra relazioni tra gli utenti, dispositivi mobili, interessi e sistemi operativi hello seguente.

![Database di esempio che mostra persone, dispositivi e interessi](./media/graph-introduction/sample-graph.png)

Grafici sono utili toounderstand un'ampia gamma di set di dati in informatica, la tecnologia e business. I database di grafi consentono di modellare e archiviare grafi in modo naturale e sono quindi una scelta ottimale in molti scenari. I database di grafi sono in genere database NoSQL perché questi casi di utilizzo spesso necessitano anche di un'iterazione rapida e di uno schema flessibile.

I grafi offrono una tecnica di modellazione dei dati potente e innovativa. Ma questo fatto da sola non è un toouse motivo sufficiente un database del grafico. Per molti casi di utilizzo e pattern che includono attraversamenti di grafi, questi ultimi offrono prestazioni migliori rispetto ai database NoSQL e SQL tradizionali di parecchi ordini di grandezza. Questa differenza a livello di prestazioni aumenta ulteriormente quando si attraversano più relazioni, ad esempio un amico di un amico.

È possibile combinare gli attraversamenti veloce hello che forniscono i database di grafico con gli algoritmi di grafico, come ricerca in profondità, ricerca breadth-first e all'algoritmo di Dijkstra, problemi toosolve nei vari domini come social networking, gestione dei contenuti, geospaziale, e suggerimenti.

## <a name="planet-scale-graphs-with-azure-cosmos-db"></a>Grafi a scalabilità globale con Azure Cosmos DB
DB Cosmos Azure è un database di graph completamente gestito che offre distribuzione globale, elastica scalabilità dell'archiviazione e della velocità effettiva, l'indicizzazione automatica e query, livelli di coerenza ottimizzabili e supporto per hello TinkerPop standard.  

![Architettura di grafi di Azure Cosmos DB](./media/graph-introduction/cosmosdb-graph-architecture.png)

DB Cosmos Azure offre i seguenti hello differenziata funzionalità quando vengono confrontati i database di graph tooother mercato hello:

* Archiviazione e velocità effettiva altamente scalabile

 Grafici nel mondo reale hello necessario tooscale oltrepassato la capacità di hello di un singolo server. Con Azure Cosmos DB la scalabilità dei grafi può essere ottenuta facilmente tra più server. È anche possibile ridimensionare la velocità effettiva hello del grafico in modo indipendente in base ai modelli di accesso. DB Cosmos Azure supporta i database di grafico che possono essere ridimensionati toovirtually le dimensioni di archiviazione senza limiti e velocità effettiva di provisioning.

* Replica di tipo multiarea

 DB Cosmos Azure vengono replicati in modo trasparente le aree tooall dati del grafico associato con l'account. La replica consente toodevelop applicazioni che richiedono accesso globale toodata. Esistono compromessi nelle aree di hello di coerenza, la disponibilità e prestazioni e garanzie corrispondente. Azure Cosmos DB fornisce failover regionale trasparente con API multihosting. È possibile ridimensionare elastico velocità effettiva e l'archiviazione tutto il mondo hello.

* Query rapide e attraversamenti con la sintassi Gremlin nota

 Archiviare bordi e vertici eterogenei ed eseguire query nei documenti tramite una sintassi Gremlin familiare. DB Cosmos Azure utilizza un strettamente simultanei, senza blocco, organizzato in log indicizzazione tecnologia tooautomatically indice tutto il contenuto. Questa funzionalità consente a query in tempo reale avanzate e attraversamenti senza hello necessario toospecify gli hint di schema, gli indici secondari o viste. Per altre informazioni, vedere [Eseguire query su grafi usando Gremlin](gremlin-support.md).

* Soluzione completamente gestita

 Azure DB Cosmos Elimina hello necessità toomanage risorse database e computer. Come un servizio completamente gestito di Microsoft Azure, eseguire non è necessario toomanage le macchine virtuali, distribuire e configurare il software, gestire la scalabilità o gestire gli aggiornamenti a livello di dati complessi. Il backup di ogni grafo viene eseguito automaticamente e ogni grafo è protetto da errori nell'area geografica specifica. È possibile aggiungere con facilità un account Azure Cosmos DB ed eseguire il provisioning della capacità in base alle esigenze in modo da potersi concentrare sull'applicazione anziché sul funzionamento e sulla gestione del database.

* Indicizzazione automatica

 Per impostazione predefinita, Azure Cosmos DB automaticamente gli indici di tutte le proprietà di hello all'interno di nodi e bordi nel grafico hello e non prevede né richiede qualsiasi schema o la creazione di indici secondari.

* Compatibilità con Apache TinkerPop

 In modo nativo, Azure DB Cosmos supporta hello open source TinkerPop Apache standard e può essere integrato con altri sistemi abilitato TinkerPop grafico. In questo modo, è possibile migrare con facilità da un altro database di grafi come Titan o Neo4j o usare Azure Cosmos DB con framework di analisi dei grafi come [Apache Spark GraphX](spark-connector-graph.md).

* Livelli di coerenza regolabili

 Selezionare cinque coerenza ben definiti livelli tooachieve un compromesso ottimale tra prestazioni e coerenza. Per query e operazioni di lettura, Azure Cosmos DB offre cinque livelli di coerenza distinti, ovvero avanzata, con decadimento ristretto, sessione, prefisso coerente e futura. Questi livelli di coerenza granulari, ben definiti, consentono di toomake audio compromessi coerenza, disponibilità e latenza. Altre informazioni, vedere [con coerenza livelli toomaximize disponibilità e le prestazioni in DocumentDB](consistency-levels.md).

Azure DB Cosmos inoltre possibile utilizzare più modelli, ad esempio documenti e di grafico, interno hello contenitori stessi/database. È possibile utilizzare i dati del grafico toostore insieme un documento in modo affiancato con documenti. È possibile utilizzare entrambe le query SQL su JSON e Gremlin query tooquery hello stessi dati sotto forma di grafico.

## <a name="getting-started"></a>introduttiva
È possibile utilizzare hello Azure interfaccia della riga di comando (CLI), Azure Powershell, o hello portale di Azure con il supporto per gli account di Azure Cosmos DB toocreate di graph API. Dopo aver creato gli account, hello portale di Azure fornisce un endpoint del servizio, ad esempio `https://<youraccount>.graphs.azure.com`, che fornisce un front-end di WebSocket per Gremlin. È possibile configurare gli strumenti di TinkerPop compatibile, ad esempio hello [Gremin Console](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console), tooconnect toothis endpoint e compilare applicazioni Java, Node.js o un driver client Gremlin.

Hello nella tabella seguente mostra più diffusi Gremlin i driver che è possibile utilizzare in Azure Cosmos DB:

| Scaricare | Documentazione |
| --- | --- |
| [Java](https://mvnrepository.com/artifact/com.tinkerpop.gremlin/gremlin-java) |[JavaDoc Gremlin](http://tinkerpop.apache.org/javadocs/current/full/) |
| [Node.js](https://www.npmjs.com/package/gremlin) |[Gremlin-JavaScript in Github](https://github.com/jbmusso/gremlin-javascript) |
| [Console Gremlin](https://tinkerpop.apache.org/downloads.html) |[Documenti TinkerPop](http://tinkerpop.apache.org/docs/current/reference/#gremlin-console) |

DB Cosmos Azure fornisce anche una libreria.NET che contiene i metodi di estensione Gremlin sopra hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) tramite NuGet. Questa libreria fornisce un server di Gremlin "in-process" che è possibile utilizzare tooconnect direttamente tooDocumentDB partizioni di dati.

| Scaricare | Documentazione |
| --- | --- |
| [.NET](https://www.nuget.org/packages/Microsoft.Azure.Graphs/) |[Microsoft.Azure.Graphs](https://msdn.microsoft.com/library/azure/dn948556.aspx) |

Utilizzando hello [Azure Cosmos DB emulatore](local-emulator.md), è possibile utilizzare toodevelop API Graph hello e test in locale senza creare una sottoscrizione di Azure o eventuali costi. Quando si è soddisfatti delle modalità di funzionamento dell'applicazione in hello emulatore, è possibile passare un account Azure Cosmos DB nel cloud hello toousing.

## <a name="scenarios-for-graph-support-of-azure-cosmos-db"></a>Scenari per il supporto Graph di Azure Cosmos DB
Ecco alcuni scenari in cui è possibile usare il supporto di Graph di Azure Cosmos DB:

* Social network

 Combinando i dati sui clienti e le relative interazioni con altri utenti, è possibile sviluppare esperienze personalizzate, prevedere il comportamento dei clienti o connettere gli utenti ad altri utenti con interessi simili. DB Cosmos Azure può essere utilizzato toomanage social network e tenere traccia di dati e le preferenze del cliente.

* Motore di raccomandazione

 Questo scenario viene comunemente utilizzato nel settore al dettaglio hello. Combinando informazioni su prodotti, utenti e interazioni utente come acquisti, esplorazioni o valutazioni di un elemento, è possibile generare raccomandazioni personalizzate. Hello nativo a bassa latenza e scalabilità elastica del supporto di graph di Azure Cosmos DB è ideale per le interazioni di modellazione.

* GeoSpatial

 Molte applicazioni di telecomunicazioni, logistica e pianificazione di viaggi necessario toofind un percorso di interesse all'interno di un'area o individuare l'itinerario più breve o ottimale hello tra due posizioni. Azure Cosmos DB è una scelta ideale in questi scenari.

* Internet delle cose

 Con la rete di hello e le connessioni tra i dispositivi IoT modellati come un grafico, è possibile compilare una migliore comprensione dello stato di hello i dispositivi e risorse e informazioni su come le modifiche in una parte della rete hello possono influire su un'altra parte.

## <a name="next-steps"></a>Passaggi successivi
toolearn più sul supporto del grafico in Azure Cosmos DB, vedere:

* Introduzione a hello [esercitazione graph di Azure Cosmos DB](create-graph-dotnet.md).
* Informazioni su come troppo[query grafici nel database di Azure Cosmos utilizzando Gremlin](gremlin-support.md).
