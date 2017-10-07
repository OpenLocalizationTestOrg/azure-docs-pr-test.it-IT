---
title: archiviazione in memoria XTP aaaMonitor | Documenti Microsoft
description: "Stimare e monitorare l'uso e la capacità delle risorse di archiviazione in memoria XTP e risolvere l'errore di capacità 41823"
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a>Monitorare l'archiviazione OLTP in memoria
Quando si usa [OLTP in memoria](sql-database-in-memory.md), i dati nelle tabelle con ottimizzazione per la memoria e le variabili di tabella si trovano nell'archiviazione OLTP in memoria. Ogni livello di servizio Premium ha un formato di archiviazione OLTP In memoria massimo, che è documentato in hello [articolo livelli di servizio di Database SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels). Dopo il superamento di questo limite, è possibile che le operazioni di inserimento e aggiornamento abbiano esito negativo con errore 41823. A questo punto sarà necessario tooeither Elimina dati tooreclaim memoria o aggiornare hello livello di prestazioni del database.

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a>Determinare se i dati si adattino all'interno di criteri di archiviazione in memoria hello
Determinare il limite di archiviazione hello: hello, consultare [articolo livelli di servizio di Database SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) per caps archiviazione hello di diversi livelli di servizio Premium hello.

Stimare la memoria, i requisiti per una tabella con ottimizzazione per la memoria funziona hello stesso modo per SQL Server come avviene in Database SQL di Azure. Richiedere alcuni minuti tooreview tale argomento [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).

Si noti che nella tabella hello e righe variabile di tabella, nonché gli indici, conteggiati per dimensioni dei dati utente max hello. Inoltre, ALTER TABLE è necessario sufficiente toocreate chat una nuova versione dell'intera tabella hello e i relativi indici.

## <a name="monitoring-and-alerting"></a>Monitoraggio e avviso
È possibile monitorare l'utilizzo di archiviazione in memoria come una percentuale di hello [il limite di archiviazione per il livello di prestazioni](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in hello Azure [portale](https://portal.azure.com/): 

* Nel pannello Database hello, individuare hello risorse utilizzo casella e fare clic su Modifica.
* Quindi selezionare la metrica hello `In-Memory OLTP Storage percentage`.
* tooadd un avviso, fare clic su Pannello metriche di hello utilizzo delle risorse casella tooopen hello, quindi fare clic su Aggiungi avviso.

In alternativa utilizzare hello dopo l'utilizzo di archiviazione in memoria hello tooshow query:

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a>Correggere le situazioni di memoria insufficiente - Errore 41823
Se la memoria è insufficiente, le operazioni INSERISCI, AGGIORNA e CREA avranno esito negativo con messaggio di errore 41823.

Messaggio di errore 41823 indica che le tabelle con ottimizzazione per la memoria hello e variabili di tabella hanno superato la dimensione massima di hello.

tooresolve questo errore, entrambi:

* Eliminare i dati da tabelle con ottimizzazione per la memoria hello, potenzialmente offload hello dati tootraditional, tabelle basate su disco. In alternativa,
* Aggiornare hello servizio livello tooone con sufficiente spazio di archiviazione in memoria per i dati di hello è necessario tookeep nelle tabelle con ottimizzazione per la memoria.

## <a name="next-steps"></a>Passaggi successivi
Per le linee guida sul monitoraggio, vedere [Monitoraggio del database SQL di Azure tramite le visualizzazioni di gestione dinamica](sql-database-monitoring-with-dmvs.md).
