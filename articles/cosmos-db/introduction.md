---
title: aaaIntroduction tooAzure DB Cosmos | Documenti Microsoft
description: "Informazioni su Azure Cosmos DB. Questo database multimodello distribuito a livello globale è pensato per garantire bassa latenza, scalabilità elastica e disponibilità elevata."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: a855183f-34d4-49cc-9609-1478e465c3b7
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/14/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: f2acbe99f425b2f07a62bbbb4324aa48f1037481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="welcome-tooazure-cosmos-db"></a>Benvenuto tooAzure Cosmos DB

Azure Cosmos DB è il database multimodello distribuito a livello globale di Microsoft. Con hello di un pulsante, DB Cosmos Azure consente di tooelastically e in modo indipendente velocità effettiva di scala e archiviazione in un numero qualsiasi di aree geografiche di Azure. Assicura inoltre velocità effettiva, latenza, disponibilità e coerenza grazie a [contratti di servizio](https://aka.ms/acdbsla) (SLA, Service Level Agreement) completi, una garanzia che nessun altro servizio di database è in grado di offrire.

![Azure Cosmos DB è il servizio di database Microsoft distribuito a livello globale con scalabilità orizzontale elastica, bassa latenza garantita, cinque modelli di coerenza e contratti di servizio completi garantiti.](./media/introduction/azure-cosmos-db.png)

## <a name="solutions-that-benefit-from-azure-cosmos-db"></a>Soluzioni che traggono vantaggio da Azure Cosmos DB

Qualsiasi [web, i dispositivi mobili, giochi e applicazioni IoT](use-cases.md) che richiedono toohandle grandi quantità di letture e scritture in un [globale](distribute-data-globally.md) scalare con tempi di risposta minimo per una vasta gamma di dati sarà vantaggioso Azure Cosmos DB [garantito](https://azure.microsoft.com/support/legal/sla/cosmos-db/) disponibilità, velocità effettiva elevata, bassa latenza e la coerenza ottimizzabili.

## <a name="key-capabilities"></a>Funzionalità principali
Come servizio di database distribuita a livello globale, Azure Cosmos DB fornisce hello seguente toohelp funzionalità si compilano applicazioni scalabile e ad alte:

* **Distribuzione globale chiavi in mano**
    * È possibile [distribuire i dati](distribute-data-globally.md) numero tooany di [aree di Azure](https://azure.microsoft.com/regions/), con hello [fare clic su di un pulsante](tutorial-global-distribution-documentdb.md). In questo modo si tooput i dati in cui gli utenti, garantisce minor latenza possibile hello tooyour clienti. 
    * Utilizzo di Azure Cosmos DB API multihosting, sempre l'applicazione hello sa dove hello più vicino area è e invierà richieste toohello più vicino al centro dati. Tutto questo è possibile senza modifiche alla configurazione, si imposta l'area di scrittura e molte aree di lettura e hello rest viene gestita automaticamente.

* **Più modelli di dati e API comuni per l'accesso e le query sui dati**
    * modello di dati basate su sequenza di record atom (ARS) Hello Azure Cosmos DB viene compilato in modo nativo nel supporta più modelli di dati, inclusi, a titolo esemplificativo toodocument, grafico, chiave-valore, tabella e i modelli di dati a colonne.
    * API per hello con i modelli di dati sono supportate con SDK è disponibile in più lingue:
        * [API di DocumentDB](documentdb-introduction.md)
        * [API di MongoDB](mongodb-introduction.md)
        * [API di tabella](table-introduction.md)
        * [API Graph (Gremlin)](graph-introduction.md)
        * Altri modelli di dati saranno presto disponibili 

* **Ridimensionamento elastico della velocità effettiva e dell'archiviazione su richiesta, in tutto il mondo**
    * Possibilità di ridimensionare facilmente la velocità effettiva del database con una granularità [al secondo](request-units.md), modificandola in qualsiasi momento. 
    * Scala dimensioni di archiviazione [in modo trasparente e automatico](partition-data.md) toohandle i requisiti di dimensione, ora e forever.

* **Compilazione di applicazioni cruciali altamente reattive**
    * DB Cosmos Azure garantisce a bassa latenza end-to-end in hello ai clienti di tooits 99th percentile. 
    * Per un tipico 1 elemento KB, DB Cosmos garantisce la latenza end-to-end di letture in 10 ms e indicizzate scritture in 15 ms in percentile 99th hello, hello interno stessa regione di Azure. le latenze mediano di Hello sono notevolmente inferiore (in ms 5).

* **Disponibilità Always On**
    * Disponibilità del 99,99% all'interno di una singola area.
    * Distribuire numero tooany di [aree di Azure](https://azure.microsoft.com/regions) per una maggiore disponibilità.
    * [Simulazione di errore](regional-failover.md) di una o più aree senza perdita di dati. 

* **Scrivere le applicazioni distribuite globalmente, hello modo a destra**
    * Cinque [modelli coerenza](consistency-levels.md) offrono una gamma di coerenza assoluta di tipo SQL tutti hello coerenza finale modo tooNoSQL simile e ogni aspetto tra. 
  
* **Recupero dell'investimento**
    * I dati sono immediatamente disponibili in modo rapido, in caso contrario l'importo versato verrà rimborsato. 
    * [Contratti di servizio](https://aka.ms/acdbsla) per garantire disponibilità, latenza, velocità effettiva e coerenza. 

* **Nessuna gestione di schemi/indici di database**
    * Non è più necessario preoccuparsi di mantenere lo schema e gli indici del database sincronizzati con lo schema dell'applicazione. La soluzione è indipendente dallo schema. 
    * Il motore di database di Azure Cosmos DB è completamente indipendente dello schema: vengono indicizzate automaticamente tutti i dati di hello inserisce senza richiedere dello schema o gli indici e query fast velocissima serve. 

* **Costo di proprietà ridotto**
    * Cinque volte tooten [economicamente più vantaggioso](https://aka.ms/cosmos-db-tco-paper) rispetto a una soluzione non gestita.
    * Tre volte meno costoso di DynamoDB.

## <a name="capability-comparison"></a>Confronto delle funzionalità

Azure DB Cosmos funzionalità hello migliore dei database relazionali e non relazionali.

| Capabilities | Database relazionali   | Database non relazionali (NoSQL) |    Azure Cosmos DB |
| --- | --- | --- | --- |
| Distribuzione globale | No | No | Sì, distribuzione chiavi in mano in oltre 30 aree con le API multihosting|
| Scalabilità orizzontale | No | Sì | Sì, archiviazione e velocità effettiva sono scalabili in modo indipendente | 
| Garanzie di latenza | No | Sì | Sì, 99% delle letture in <10 ms e delle scritture in <15 ms | 
| Disponibilità elevata | No | Sì | Sì, Cosmos DB è sempre online, ha compromessi secondo il teorema PACELC e offre opzioni di failover automatico e manuale|
| Modello di dati + API | Relazionale + SQL | Multimodello + API OSS | Multimodello + SQL + API OSS (altre funzionalità presto disponibili) |
| Contratti di servizio | Sì | No | Sì, contratti di servizio completi per latenza, velocità effettiva, coerenza, disponibilità |


## <a name="next-steps"></a>Passaggi successivi
Per un'introduzione ad Azure Cosmos DB, fare riferimento alle guide introduttive seguenti:

* [Come iniziare a usare l'API DocumentDB di Azure Cosmos DB](create-documentdb-dotnet.md)
* [Come iniziare a usare l'API MongoDB di Azure Cosmos DB](create-mongodb-nodejs.md)
* [Come iniziare a usare l'API Graph di Azure Cosmos DB](create-graph-dotnet.md)
* [Come iniziare a usare l'API di tabella di Azure Cosmos DB](create-table-dotnet.md)
