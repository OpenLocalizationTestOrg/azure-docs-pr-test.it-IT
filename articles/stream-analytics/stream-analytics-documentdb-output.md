---
title: output aaaJSON per flusso Analitica | Documenti Microsoft
description: "Informazioni su come l'analisi di flusso può usare Azure Cosmos DB per l'output JSON, consentendo l'esecuzione di query di archiviazione dei dati e a bassa latenza su dati JSON non strutturati."
keywords: Output JSON
documentationcenter: 
services: stream-analytics,documentdb
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 5d2a61a6-0dbf-4f1b-80af-60a80eb25dd1
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: fa717818c839ecd7a60fcee33d22011990fd5878
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="target-azure-cosmos-db-for-json-output-from-stream-analytics"></a>Usare Azure Cosmos DB per l'output JSON dell'analisi di flusso
L'analisi di flusso può usare [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) per l'output JSON, consentendo l'esecuzione di query di archiviazione dei dati e a bassa latenza su dati JSON non strutturati. Questo documento descrive alcune procedure consigliate per l'implementazione di questa configurazione.

Per chi ha familiarità con DB Cosmos, dare un'occhiata [il percorso di apprendimento del database di Azure Cosmos](https://azure.microsoft.com/documentation/learning-paths/documentdb/) tooget avviato. 

Nota: l'API di MongoDB basata su raccolte di Cosmos DB non è attualmente supportata. 

## <a name="basics-of-cosmos-db-as-an-output-target"></a>Nozioni di base di Cosmos DB come destinazione di output
Hello Azure Cosmos DB output nel flusso Analitica consente la scrittura del flusso di elaborazione dei risultati come output JSON in raccolte del DB Cosmos. Flusso Analitica non creare raccolte nel database, invece richiedere toocreate li sin dall'inizio. Si tratta in modo che i costi di fatturazione hello di raccolte Cosmos DB tooyou trasparente, in modo che è possibile ottimizzare le prestazioni di hello, coerenza e la capacità delle raccolte direttamente utilizzando hello [API DB Cosmos](https://msdn.microsoft.com/library/azure/dn781481.aspx). È consigliabile utilizzare un Database di DB Cosmos per il flusso di processo toologically separate le raccolte per un processo di streaming.

Alcune delle opzioni di raccolta Cosmos DB hello è illustrate di seguito.

## <a name="tune-consistency-availability-and-latency"></a>Ottimizzare coerenza, disponibilità e latenza
toomatch dei requisiti dell'applicazione, DB Cosmos consente database hello di ottimizzazione toofine e raccolte e verificare compromessi tra la coerenza, disponibilità e latenza. A seconda dei livelli di coerenza di lettura richiesti dello scenario rispetto alla latenza di lettura e scrittura, è possibile scegliere un livello di coerenza per l'account del database. Per impostazione predefinita, DB Cosmos consente inoltre l'indicizzazione sincrono in ogni raccolta di tooyour operazioni CRUD. Si tratta di hello toocontrol di un'altra opzione utile prestazioni nel database Cosmos di lettura/scrittura. Per ulteriori informazioni su questo argomento, esaminare hello [modificare i livelli di coerenza del database e query](../documentdb/documentdb-consistency-levels.md) articolo.

## <a name="upserts-from-stream-analytics"></a>Upsert di Analisi di flusso
Integrazione Analitica flusso con DB Cosmos consente tooinsert o aggiorna i record del DB Cosmos raccolta in base a una determinata colonna di ID documento. Si tratta di cui viene fatto riferimento tooas un *Upsert*.

Flusso Analitica utilizza un approccio ottimistico Upsert, in cui gli aggiornamenti sono eseguiti solo quando l'inserimento ha esito negativo a causa di conflitti di ID documento tooa. Questo aggiornamento viene eseguito da Analitica flusso come PATCH, pertanto consente documento toohello aggiornamenti parziali, ad esempio l'aggiunta di nuove proprietà o la sostituzione di che una proprietà esistente viene eseguita in modo incrementale. Si noti che le modifiche ai valori hello delle proprietà di matrice nel documento JSON provocare intera matrice hello recupero sovrascritto, vale a dire matrice hello non viene unito.

## <a name="data-partitioning-in-cosmos-db"></a>Partizionamento dei dati in Cosmos DB
COSMOS DB [partizionata raccolte](../cosmos-db/partition-data.md) sono hello consigliato approccio per il partizionamento dei dati. 

Per le raccolte di DB Cosmos singole, flusso Analitica ancora consente toopartition i dati basati sui modelli di query hello sia alle esigenze di prestazioni dell'applicazione. Ogni raccolta può contenere un massimo di too10GB dei dati (massimo) e attualmente di che non è tooscale alcun modo (o overflow) una raccolta. Per la scalabilità orizzontale, Analitica di flusso consente toowrite toomultiple raccolte con un prefisso (vedere i dettagli di utilizzo riportati di seguito). Flusso Analitica utilizza hello coerenza [Resolver partizione Hash](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.partitioning.hashpartitionresolver.aspx) strategia in base all'utente di hello fornito PartitionKey colonna toopartition relativi record di output. Hello numero di raccolte con hello all'ora di inizio del processo di streaming hello di prefisso viene utilizzato come numero di partizioni di output di hello, il processo di hello toowhich scrive tooin parallelo (raccolte DB Cosmos = le partizioni di Output). Per una singola raccolta con indicizzazione differita che esegue solo inserimenti, è prevedibile una velocità effettiva di scrittura di 0,4 MB/s. Utilizzo di più raccolte, è possibile consentire si tooachieve una velocità effettiva e maggiore capacità.

Se si intende il numero di partizioni tooincrease hello in hello future, si potrebbe essere necessario toostop il processo, repartition hello dati dalle raccolte esistenti in nuove raccolte e quindi riavviare hello Analitica flusso processo. Altre informazioni sull'uso di PartitionResolver e sul ripartizionamento, con codice di esempio, saranno incluse in un post di approfondimento. articolo Hello [partizionamento e la scalabilità in DB Cosmos](../documentdb/documentdb-partition-data.md) forniscono inoltre informazioni dettagliate su questo.

## <a name="cosmos-db-settings-for-json-output"></a>Impostazioni di Cosmos DB per l'output JSON
La creazione di Cosmos DB come output nell'analisi di flusso genera una richiesta di informazioni, come illustrato di seguito. In questa sezione viene fornita una spiegazione della definizione di proprietà hello.

Raccolta partizionata | Più raccolte a partizione singola
---|---
![documentdb analisi di flusso schermata di output](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-1.png) |  ![documentdb analisi di flusso schermata di output](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-2.png)


  
> [!NOTE]
> Hello **più raccolte di "Sola partizione"** scenario richiede una chiave di partizione e una configurazione supportata. 

* **Alias di output** – toorefer un alias per questo output nella query ASA  
* **Nome account** : hello nome o l'URI di hello account Cosmos DB dell'endpoint.  
* **Chiave account** : chiave di accesso condiviso hello per hello Cosmos DB account.  
* **Database** : nome del database DB Cosmos hello.  
* **Modello di nome raccolta** : hello raccolta o il nome relativo modello per hello raccolte toobe utilizzato. formato di nome raccolta Hello può essere costruito utilizzando token {partition} facoltativo hello, in cui le partizioni iniziano da 0. Di seguito sono riportati input di esempio validi:  
  1\) MyCollection: deve essere presente una raccolta denominata "MyCollection".  
  2\) MyCollection{partizione}: devono essere presenti le raccolte "MyCollection0", "MyCollection1", "MyCollection2" e così via.  
* **Chiave di partizione**: valore facoltativo. È necessario solo se si usa un token {partition} nel modello del nome di raccolta. nome di Hello del campo hello in output chiave hello toospecify di eventi utilizzati per il partizionamento dell'output tra raccolte. Per l'output di una singola raccolta si può usare qualsiasi colonna di output arbitraria, ad esempio PartitionId.  
* **ID documento** : valore facoltativo. nome di Hello di hello campo negli eventi di output utilizzato chiave primaria hello toospecify su quali insert o update sono basate le operazioni.  
