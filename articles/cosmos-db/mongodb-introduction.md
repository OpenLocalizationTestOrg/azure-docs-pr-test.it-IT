---
title: 'Introduzione tooAzure DB Cosmos: API per MongoDB | Documenti Microsoft'
description: Informazioni su come utilizzare Azure Cosmos DB toostore e grandi volumi di query di documenti JSON con bassa latenza hello diffusi OSS MongoDB APIs.
keywords: "che cos'è MongoDB"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 4afaf40d-c560-42e0-83b4-a64d94671f0a
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: anhoh
ms.openlocfilehash: 1eb88014cc4809332e3f5c109a44a55814194934
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-api-for-mongodb"></a>Introduzione tooAzure DB Cosmos: API per MongoDB

[Azure Cosmos DB](../cosmos-db/introduction.md) è il servizio di database multimodello distribuito a livello globale di Microsoft per applicazioni cruciali. DB Cosmos Azure fornisce [distribuzione globale di chiavi in mano](distribute-data-globally.md), [scalabilità elastica di velocità effettiva e l'archiviazione](partition-data.md) latenze millisecondo in tutto il mondo, a una cifra a percentile 99th hello, [cinque livelli di coerenza ben definiti](consistency-levels.md)e garantisce la disponibilità elevata, tutti i backup da [SLA leader del settore](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Azure DB Cosmos [automaticamente i dati di indici](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) senza toodeal con la gestione dello schema e indice. Si tratta di un database multimodello che supporta modelli di dati di documenti, coppie chiave-valore, grafi e colonne. 

![Azure Cosmos DB: API MongoDB](./media/mongodb-introduction/cosmosdb-mongodb.png) 

Database di COSMOS DB possono essere utilizzati come archivio dati hello per le applicazioni scritte per [MongoDB](https://docs.mongodb.com/manual/introduction/). Di conseguenza, usando i [driver](https://docs.mongodb.org/ecosystem/drivers/) esistenti l'applicazione scritta per MongoDB ora può comunicare con Cosmos DB e usare i database Cosmos DB invece dei database MongoDB. In molti casi, è possibile passare dall'utilizzo di MongoDB tooCosmos DB modificando semplicemente una stringa di connessione. Utilizza questa funzionalità, è possibile creare facilmente e di eseguire applicazioni di database di MongoDB in hello Azure cloud con distribuzione globale del database di Azure Cosmos e [i contratti di servizio di leader del settore completo](https://azure.microsoft.com/support/legal/sla/cosmos-db), pur continuando toouse familiare competenze e gli strumenti per MongoDB.


## <a name="what-is-hello-benefit-of-using-azure-cosmos-db-for-mongodb-applications"></a>Che cos'è hello vantaggio derivante dall'utilizzo DB Cosmos Azure per le applicazioni di MongoDB?

**Velocità effettiva altamente scalabile e archiviazione:** facilmente scalabilità verticale o verso il basso il toomeet database MongoDB l'applicazione necessita di. I dati sono archiviati in unità SSD (Solid State Drive) per garantire livelli di latenza bassi e prevedibili. COSMOS DB supporta raccolte di MongoDB adattabile toovirtually le dimensioni di archiviazione senza limiti e velocità effettiva di provisioning. Cosmos DB offre una semplice scalabilità elastica e prestazioni prevedibili in base alla crescita dell'applicazione. 

**Replica di tipo multiarea:** Cosmos DB vengono replicati in modo trasparente le aree di tooall dati è stata associata con l'account di MongoDB, consentendo toodevelop applicazioni che richiedono accesso globale toodata fornendo compromessi adeguati tra tipi la coerenza, disponibilità e prestazioni, tutte le garanzie corrispondente. COSMOS DB fornisce il failover regionale trasparente con le API multihosting e velocità effettiva di scala hello possibilità tooelastically e archiviazione tutto il mondo hello. Per altre informazioni, vedere [Distribuire i dati a livello globale](distribute-data-globally.md).

**Compatibilità con MongoDB**: è possibile sfruttare le competenze, il codice dell'applicazione e degli strumenti MongoDB esistenti. È possibile sviluppare applicazioni usando MongoDB e distribuirli tooproduction utilizzando hello completamente gestito servizio Cosmos DB distribuito in modo globale.

**Nessuna gestione server**: utente non ha toomanage e applicare la scalabilità dei database di MongoDB. COSMOS DB è un servizio completamente gestito, ovvero che non si dispone toomanage alcuna infrastruttura o macchine virtuali manualmente. Cosmos DB è disponibile in più di 30 [aree di Azure](https://azure.microsoft.com/regions/services/).

**Livelli di coerenza ottimizzabili:** selezionare da cinque ben definita compromesso ottimale tooachieve livelli di coerenza tra prestazioni e coerenza. Per query e operazioni di lettura, Cosmos DB offre cinque livelli di coerenza distinti, ovvero avanzata, con decadimento ristretto, sessione, prefisso coerente e futura. Questi livelli di coerenza granulari, ben definiti, consentono di toomake audio compromessi tra la coerenza, disponibilità e latenza. Altre informazioni, vedere [con coerenza i livelli di prestazioni e disponibilità toomaximize](consistency-levels.md).

**L'indicizzazione automatica**: per impostazione predefinita, DB Cosmos automaticamente gli indici di tutte le proprietà di hello all'interno di documenti nel database MongoDB e non prevede né richiede qualsiasi schema o la creazione di indici secondari.

**Livello aziendale** -DB Cosmos Azure supporta più repliche locali toodeliver 99,99% disponibilità e protezione dei dati in faccia hello di errori locali e internazionali. Azure Cosmos DB ha [certificazioni di conformità](https://www.microsoft.com/trustcenter) e funzionalità di sicurezza di classe enterprise. 

Per altre informazioni, guardare questo video di Azure Friday con Scott Hanselman e Kirill Gavrylyuk, responsabile principale della progettazione per Azure Cosmos DB.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Introducing-Azure-Cosmos-DB/player]
> 

## <a name="how-tooget-started"></a>La modalità di avvio tooget

Seguire hello MongoDB Guide rapide toocreate un account Cosmos DB e la migrazione il toouse di applicazione di Mongo DB DB Cosmos esistente o compilarne uno nuovo:

* [Eseguire la migrazione di un'app Web MongoDB Node.js esistente](create-mongodb-nodejs.md).
* [Creare un'app di web API MongoDB con .NET e hello portale di Azure](create-mongodb-dotnet.md)
* [Creare un'applicazione console API MongoDB con Java e hello portale di Azure](create-mongodb-java.md)

## <a name="next-steps"></a>Passaggi successivi

Informazioni sull'API di Azure Cosmos DB MongoDB sono integrate in hello documentazione Cosmos complessiva Azure DB, ma Ecco alcuni puntatori tooget, che è stato avviato:

* Seguire hello [tooa MongoDB account di connessione](connect-mongodb-account.md) esercitazione toolearn come tooget le informazioni di stringa di connessione di account.
* Seguire hello [MongoChef usare con Azure Cosmos DB](mongodb-mongochef.md) toolearn esercitazione come una connessione tra il database di Azure Cosmos database e dell'applicazione MongoDB MongoChef toocreate.
* Seguire hello [eseguire la migrazione di dati tooAzure Cosmos DB con supporto del protocollo per MongoDB](mongodb-migrate.md) tooimport esercitazione tooan i dati API per il database di MongoDB.
* Connettersi tooan API per l'utilizzo di account MongoDB [Robomongo](mongodb-robomongo.md).
* Informazioni su quanti RUs hello mediante le operazioni [GetLastRequestStatistics comando e le metriche del portale Azure hello](request-units.md#GetLastRequestStatistics).
* Informazioni su come troppo[configurare le preferenze di lettura per le applicazioni distribuite globalmente](../cosmos-db/tutorial-global-distribution-mongodb.md).
