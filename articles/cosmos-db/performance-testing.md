---
title: "Test delle prestazioni e della scalabilità in Azure Cosmos DB | Microsoft Docs"
description: "Informazioni sull'esecuzione di test delle prestazioni e della scalabilità con Azure Cosmos DB"
keywords: test delle prestazioni
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: b5a1edd08819e82437c5b22d8eb131665d7c9645
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a>Test delle prestazioni e della scalabilità con Azure Cosmos DB
Il test delle prestazioni e della scalabilità è un passaggio chiave nello sviluppo di un'applicazione. Per molte applicazioni, il livello del database ha un impatto significativo sulle prestazioni e sulla scalabilità globali, è pertanto un componente fondamentale del test delle prestazioni. [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) è appositamente progettato per garantire scalabilità elastica e prestazioni prevedibili ed è quindi ideale per applicazioni che richiedono un livello database con prestazioni elevate. 

Questo articolo offre informazioni di riferimento per gli sviluppatori che implementano gruppi di test delle prestazioni per i carichi di lavoro di Cosmos DB o valutano Cosmos DB per scenari di applicazioni ad alte prestazioni. Approfondisce soprattutto i test isolati delle prestazioni del database, ma include anche le procedure consigliate per le applicazioni di produzione.

Dopo la lettura di questo articolo, si potrà rispondere alle domande seguenti:   

* Dove è possibile trovare un'applicazione client .NET di esempio per i test delle prestazioni di Cosmos DB? 
* Come è possibile ottenere livelli di velocità effettiva elevati con Cosmos DB dall'applicazione client?

Per iniziare a usare il codice, scaricare il progetto dell'[esempio relativo al test delle prestazioni di Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark). 

> [!NOTE]
> L'obiettivo di questa applicazione è illustrare le procedure consigliate per ottenere prestazioni migliori da Cosmos DB con un numero ridotto di computer client. L'applicazione non è stata realizzata per dimostrare la capacità massima del servizio, che può essere aumentata senza limiti.
> 
> 

Se si è interessati alle opzioni di configurazione lato client per migliorare le prestazioni di Cosmos DB, vedere [Suggerimenti sulle prestazioni per Azure Cosmos DB](performance-tips.md).

## <a name="run-the-performance-testing-application"></a>Eseguire l'applicazione per il test delle prestazioni
Il modo più rapido per iniziare è compilare ed eseguire l'esempio .NET riportato di seguito, come descritto nella procedura seguente. È anche possibile esaminare il codice sorgente e implementare configurazioni analoghe alle applicazioni client.

**Passaggio 1**: scaricare il progetto dell'[esempio relativo al test delle prestazioni di Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark) o creare la biforcazione del repository GitHub.

**Passaggio 2** : modificare le impostazioni di EndpointUrl, AuthorizationKey, CollectionThroughput e DocumentTemplate (facoltativo) nel file App.config.

> [!NOTE]
> Prima del provisioning delle raccolte con velocità effettiva elevata, consultare la [pagina dei prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/) per stimare i costi di ogni raccolta. Poiché l'addebito dello spazio di archiviazione e della velocità effettiva per Azure Cosmos DB viene eseguito in modo indipendente su base oraria, è possibile risparmiare eliminando o riducendo la velocità effettiva delle raccolte Azure Cosmos DB al termine del test.
> 
> 

**Passaggio 3** : compilare ed eseguire l'app console dalla riga di comando. Verrà visualizzato un output simile al seguente:

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


**Passaggio 4 (se necessario)** : la velocità effettiva segnalata (UR/sec) dallo strumento deve essere analoga o superiore a quella della raccolta. In caso contrario, l'aumento di DegreeOfParallelism in incrementi ridotti può aiutare a raggiungere il limite. Se la velocità effettiva dall'app client su stabilizza, l'avvio di più istanze dell'app nelle stesse macchine o in macchine diverse consente di raggiungere il limite di provisioning tra istanze diverse. Per ottenere assistenza per questo passaggio, inviare un messaggio di posta elettronica all'indirizzo askcosmosdb@microsoft.com o creare un ticket di supporto dal [portale di Azure](https://portal.azure.com).

Quando l'app è in esecuzione, è possibile provare diversi [criteri di indicizzazione](indexing-policies.md) e [livelli di coerenza](consistency-levels.md) per comprenderne l'impatto sulla velocità effettiva e sulla latenza. È anche possibile esaminare il codice sorgente e implementare configurazioni analoghe alle suite di test o alle applicazioni di produzione.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stato illustrato come eseguire test delle prestazioni e della scalabilità con Cosmos DB usando un'app console .NET. Per altre informazioni sull'uso di Azure Cosmos DB, vedere i collegamenti seguenti.

* [Esempio di test delle prestazioni di Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [Opzioni di configurazione client per migliorare le prestazioni di Azure Cosmos DB](performance-tips.md)
* [Partizionamento lato server in Azure Cosmos DB](partition-data.md)


