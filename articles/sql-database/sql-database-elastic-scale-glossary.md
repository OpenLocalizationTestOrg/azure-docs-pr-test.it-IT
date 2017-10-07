---
title: Glossario di strumenti di Database aaaElastic | Documenti Microsoft
description: Spiegazione dei termini utilizzati per gli strumenti dei database elastici
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a>Glossario sugli strumenti di database elastici
Hello termini seguenti vengono definiti per hello [strumenti di Database elastico](sql-database-elastic-scale-introduction.md), una funzionalità di Database SQL di Azure. strumenti Hello sono utilizzati toomanage [partizione viene mappata](sql-database-elastic-scale-shard-map-management.md)e includere hello [libreria client](sql-database-elastic-database-client-library.md), hello [strumento di merge di divisione](sql-database-elastic-scale-overview-split-and-merge.md), [pool elastici](sql-database-elastic-pool.md), e [query](sql-database-elastic-query-overview.md). 

Questi termini vengono utilizzati [aggiunta di una partizione utilizzando gli strumenti di Database elastico](sql-database-elastic-scale-add-a-shard.md) e [utilizzando i problemi di mappa partizioni toofix classe RecoveryManager hello](sql-database-elastic-database-recovery-manager.md).

![Termini della scalabilità elastica][1]

**Database**: un database SQL di Azure. 

**Routing dipendente dai dati**: hello funzionalità che consente una partizione di tooa tooconnect applicazione assegnata una chiave di partizionamento orizzontale specifica. Vedere [Routing dipendente dei dati](sql-database-elastic-scale-data-dependent-routing.md). Confrontare troppo**[Query più partizioni](sql-database-elastic-scale-multishard-querying.md)**.

**Mappa partizioni globale**: hello mappa tra le chiavi di partizionamento orizzontale e i rispettive partizioni all'interno di un **set di partizioni**. mappa di partizioni globale Hello viene archiviata in hello **gestore mappe partizioni**. Confrontare troppo**mappa partizioni locali**.

**Mappa partizioni di tipo elenco**: una mappa partizioni in cui le chiavi di partizionamento orizzontale vengono mappate singolarmente. Confrontare troppo**mappa partizioni intervallo**.   

**Mappa partizioni locali**: archiviati in una partizione, mappa di partizioni locale hello contiene i mapping per gli shardlet hello che risiedono in partizioni hello.

**Query su più partizioni**: hello possibilità tooissue una query su più partizioni; vengono restituiti i set di risultati utilizzando la semantica di UNION ALL (noto anche come "query fan-out"). Confrontare troppo**routing dipendente dai dati**.

**Multi-tenant** e **Tenant singolo**: l'immagine mostra un database a tenant singolo e un database multi-tenant:

![Database a tenant singolo e multi-tenant](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

Ecco una rappresentazione di database a tenant singolo e multi-tenant **partizionati** . 

![Database a tenant singolo e multi-tenant](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

**Mappa partizioni intervallo**: una mappa partizioni in cui hello strategia di distribuzione di partizioni si basa su più intervalli di valori contigui. 

**Tabelle di riferimento**: tabelle che non vengono partizionate, ma vengono replicate tra le partizioni. I codici di avviamento postale, ad esempio, possono essere archiviati in una tabella di riferimento. 

**Partizione**: un database SQL di Azure che archivia i dati da un set di dati partizionato. 

**Elasticità partizioni**: hello possibilità tooperform entrambi **scalabilità orizzontale** e **la scalabilità verticale**.

**Tabelle partizionate**: tabelle che vengono partizionate, ovvero i cui dati vengono distribuiti tra le partizioni in base ai valori della chiave di partizionamento orizzontale. 

**Chiave di partizionamento orizzontale**: un valore di colonna che determina la modalità di distribuzione dei dati tra le partizioni. Hello tipo di valore può essere uno dei seguenti hello: **int**, **bigint**, **varbinary**, o **uniqueidentifier**. 

**Set di partizioni**: hello raccolta di partizioni che sono con attributo toohello stessa mappa partizioni nel gestore mappe partizioni di hello.  

**Shardlet**: tutti i dati di hello associati a un singolo valore di una chiave di partizionamento orizzontale in una partizione. Un shardlet è hello più piccola unità di spostamento di dati possibili quando ridistribuzione di tabelle partizionate. 

**Mappa partizioni**: hello set di mapping tra le chiavi di partizionamento orizzontale e i rispettive partizioni.

**Gestore mappe partizioni**: un archivio di oggetti e dati di gestione che contiene i mapping per uno o più set di partizioni, percorsi partizioni e alle mappe partizioni hello.

![Mapping][2]

## <a name="verbs"></a>Verbi
**Scalabilità orizzontale**: act hello della scala (o) una raccolta di partizioni, aggiungendo o rimuovendo mappa partizioni tooa di partizioni, come illustrato di seguito.

![Scalabilità orizzontale e verticale][3]

**Merge**: azione hello lo spostamento degli shardlet dalla partizione tooone due partizioni e aggiornare di conseguenza mappa partizioni hello.

**Spostamento di Shardlet**: intende hello lo spostamento di una partizione diversa di tooa singolo shardlet. 

**Partizioni**: atto hello di partizionamento orizzontale in modo identico dati strutturati tra più database in base a una chiave di partizionamento orizzontale.

**Split**: intende hello lo spostamento di shardlet diverse dalla partizione di una partizione tooanother (in genere nuovo). Una chiave di partizionamento orizzontale viene fornita dall'utente hello come punto di divisione hello.

**Scalabilità verticale**: atto hello di scalare (verticale) hello livello delle prestazioni di una singola partizione. Ad esempio, la modifica di una partizione da tooPremium Standard (che comporta più risorse di calcolo). 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

