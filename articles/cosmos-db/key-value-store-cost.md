---
title: 'aaaAzure DB Cosmos come archivio di valore di chiave: Cenni preliminari sul costo | Documenti Microsoft'
description: Informazioni sui costi hello dell'utilizzo di Azure Cosmos DB come archivio di valore della chiave.
keywords: archivio di valori chiave
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: 
documentationcenter: 
ms.assetid: 7f765c17-8549-4509-9475-46394fc3a218
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: mimig
ms.openlocfilehash: de7207760a8e1fca0e30f951109748835dabf4a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-as-a-key-value-store--cost-overview"></a>Azure Cosmos DB come archivio di valori chiave: Panoramica dei costi

Azure Cosmos DB è un servizio di database multimodello distribuito a livello globale che consente di compilare con facilità applicazioni su larga scala e a disponibilità elevata. Per impostazione predefinita, Azure Cosmos DB vengono indicizzati automaticamente tutti i dati di hello che inserisce, in modo efficiente. In questo modo è possibile abilitare query [SQL](documentdb-sql-query.md) (e [JavaScript](programming.md)) rapide e coerenti su qualsiasi tipo di dati. 

Questo articolo descrive costo hello Azure Cosmos DB per la scrittura semplice e operazioni di lettura quando viene utilizzato un archivio chiave-valore. Le operazioni di scrittura includono inserimenti, sostituzioni, eliminazioni e upsert di documenti. Oltre a garantire la disponibilità elevata 99,99%, offerte Azure Cosmos DB garantito < 10 ms di latenza per le letture e < latenza 15 ms per hello (indicizzato) scrive rispettivamente alla percentile 99th hello. 

## <a name="why-we-use-request-units-rus"></a>Perché usare le unità richiesta (UR)

Prestazioni di Azure Cosmos DB sono in base all'ammontare hello di provisioning [unità richiesta](request-units.md) (RU) per la partizione hello. provisioning Hello in un secondo livello di granularità e acquistato in russo/sec e russo/min ([toobe non confondere con hello fatturazione oraria](https://azure.microsoft.com/pricing/details/cosmos-db/)). RUs deve essere considerato come una valuta che semplifica il provisioning di velocità effettiva necessaria per un'applicazione hello hello. I clienti non è necessario toothink differenziare tra lettura e scrittura delle unità di capacità. modello di sola valuta Hello del servizio aggiornamento destinatari crea efficienza capacità hello provisioning tooshare tra le letture e scritture. Questo modello di provisioning di capacità consente hello servizio tooprovide una velocità effettiva coerenza e prevedibile, bassa latenza e la disponibilità elevata è garantito. Infine, utilizziamo la velocità effettiva toomodel UR ma ogni RU provisioning presenta inoltre una quantità di risorse (memoria, Core). UR/sec non si riferisce solo alle operazioni di I/O al secondo (IOPS).

Come un sistema di database distribuiti in modo globale Cosmos DB è hello solo servizio di Azure che fornisce disponibilità toohigh inoltre un contratto di servizio alla latenza, velocità effettiva e la coerenza. velocità effettiva di Hello che viene effettuato il provisioning è applicato tooeach delle regioni hello associato all'account di database DB Cosmos. Per le letture Cosmos DB offre più ben definito [livelli di coerenza](consistency-levels.md) per toochoose da. 

Hello nella tabella seguente hello svariate RUs tooperform obbligatorio lettura e scrittura delle transazioni in base alle dimensioni del documento di 1KB e 100KBs.

|Dimensioni dell'elemento|1 Lettura|1 Scrittura|
|-------------|------|-------|
|1 KB|1 UR|5 UR|
|100 KB|10 UR|50 UR|

## <a name="cost-of-reads-and-writes"></a>Costo di letture e scritture

Se si esegue il provisioning di 1.000 UR/sec, questo importi too3.6m UR/ora e comporta un costo $0,08 per ora hello (in Europa e hello Stati Uniti). Per un documento di 1 KB, ciò significa che è possibile utilizzare 3,6 milioni di letture o 0,72 milioni di scritture (3,6 m UR/5) utilizzando la velocità effettiva con provisioning. Toomillion normalizzato legge e scrive, hello costo sarebbe $0,022 /m letture ($0,08 / 3,6) e $0.111/ m scrive ($0,08 / 0,72). costo Hello milioni diventa minimo, come illustrato nella tabella hello riportata di seguito.

|Dimensioni dell'elemento|1 milione di letture|1 milione di scritture|
|-------------|-------|--------|
|1 KB|$0.022|$0.111|
|100 KB|$0.222|$1.111|


Maggior parte dei blob di base hello o oggetto archivi servizi addebito $0,40 per milioni di transazioni di lettura e 5 dollari US per ogni transazione di scrittura milioni. Se utilizzato in modo ottimale, è possibile Cosmos DB too98% più economica rispetto a queste altre soluzioni (per le transazioni di 1KB).

## <a name="next-steps"></a>Passaggi successivi

Saranno presto disponibili nuovi articoli sull'ottimizzazione del provisioning delle risorse di Azure Cosmos DB. Nel frattempo, hello ritiene toouse disponibile il nostro [calcolatrice RU](https://www.documentdb.com/capacityplanner).

