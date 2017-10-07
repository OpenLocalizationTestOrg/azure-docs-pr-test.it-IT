---
title: aaaAzure DB Cosmos scala e il test delle prestazioni | Documenti Microsoft
description: "Informazioni su come applicare la scalabilità tooperform e il test delle prestazioni con Azure Cosmos DB"
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
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a>Test delle prestazioni e della scalabilità con Azure Cosmos DB
Il test delle prestazioni e della scalabilità è un passaggio chiave nello sviluppo di un'applicazione. Per molte applicazioni, il livello di database hello ha un impatto significativo sulle hello prestazioni e scalabilità e viene pertanto un componente critico delle prestazioni il test. [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) è appositamente progettato per garantire scalabilità elastica e prestazioni prevedibili ed è quindi ideale per applicazioni che richiedono un livello database con prestazioni elevate. 

Questo articolo offre informazioni di riferimento per gli sviluppatori che implementano gruppi di test delle prestazioni per i carichi di lavoro di Cosmos DB o valutano Cosmos DB per scenari di applicazioni ad alte prestazioni. Si concentra principalmente sui test delle prestazioni di tipo isolata di database hello, ma include anche le procedure consigliate per le applicazioni di produzione.

Dopo aver letto questo articolo, sarà in grado di tooanswer hello seguenti domande:   

* Dove è possibile trovare un'applicazione client .NET di esempio per i test delle prestazioni di Cosmos DB? 
* Come è possibile ottenere livelli di velocità effettiva elevati con Cosmos DB dall'applicazione client?

tooget avviato con il codice, scaricare il progetto hello da [esempio test delle prestazioni di Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark). 

> [!NOTE]
> obiettivo di Hello di questa applicazione è toodemonstrate procedure consigliate per l'estrazione di ottenere prestazioni migliori fuori DB Cosmos con un numero limitato di computer client. Questa capacità di picco toodemonstrate hello del servizio di hello, che possono essere ridimensionati limitlessly non è stata eseguita.
> 
> 

Se si sta cercando le opzioni di configurazione lato client tooimprove DB Cosmos prestazioni, vedere [suggerimenti sulle prestazioni di Azure Cosmos DB](performance-tips.md).

## <a name="run-hello-performance-testing-application"></a>Eseguire l'applicazione di test delle prestazioni di hello
Hello tooget modo più rapido avviato è toocompile e l'esempio di esecuzione hello .NET riportato di seguito, come descritto nei passaggi hello riportato di seguito. È anche possibile esaminare il codice sorgente hello e implementare applicazioni di un client tooyour configurazioni simili.

**Passaggio 1:** progetto hello Download da [esempio test delle prestazioni di Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), o repository di GitHub hello fork.

**Passaggio 2:** modificare le impostazioni di hello per EndpointUrl, AuthorizationKey, CollectionThroughput e DocumentTemplate (facoltativo) nel file app. config.

> [!NOTE]
> Prima di provisioning di raccolte con velocità effettiva elevata, consultare toohello [pagina prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/) costi hello tooestimate per ogni raccolta. DB Cosmos Azure addebita archiviazione e la velocità effettiva in modo indipendente su base oraria, pertanto è possibile salvare i costi per l'eliminazione o la riduzione della velocità effettiva hello delle raccolte DB Cosmos Azure al termine del test.
> 
> 

**Passaggio 3:** compilare ed eseguire l'applicazione console hello dalla riga di comando hello. Output dovrebbe essere simile hello seguente:

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


**Passaggio 4 (se necessario):** hello velocità effettiva segnalata (UR/sec) dallo strumento hello deve essere hello uguale o superiore alla velocità effettiva di hello provisioning della raccolta hello. In caso contrario, incremento hello DegreeOfParallelism piccoli incrementi consentono di raggiungere il limite di hello. Se avventurarci velocità effettiva di hello dall'app client, avviare più istanze dell'applicazione hello in hello stesso o diversi computer consentono di raggiungere il limite di hello il provisioning in hello istanze diverse. Se occorre assistenza per questo passaggio,, scrivere un messaggio di posta elettronica tooaskcosmosdb@microsoft.com o creare un ticket di supporto da hello [portale Azure](https://portal.azure.com).

Dopo aver creato hello app in esecuzione, è possibile provare diverse [criteri di indicizzazione](indexing-policies.md) e [livelli di coerenza](consistency-levels.md) toounderstand loro impatto sulla velocità effettiva e latenza. È anche possibile esaminare il codice sorgente hello e implementare simile configurazioni tooyour propri gruppi di test o le applicazioni di produzione.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stato illustrato come eseguire test delle prestazioni e della scalabilità con Cosmos DB usando un'app console .NET. Per ulteriori informazioni sull'utilizzo di Azure Cosmos DB, vedere toohello collegamenti riportati di seguito.

* [Esempio di test delle prestazioni di Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [Tooimprove opzioni di configurazione client DB Cosmos Azure prestazioni](performance-tips.md)
* [Partizionamento lato server in Azure Cosmos DB](partition-data.md)


