---
title: aaaAzure Analitica Batch | Documenti Microsoft
description: Riferimento per le analisi di Azure Batch.
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 462fbad1ac522b485ae18c1e8891b9d2cabd45e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="batch-analytics"></a>Batch Analytics
Negli argomenti di Hello Analitica Batch contengono informazioni di riferimento per gli eventi di hello e gli avvisi disponibili per le risorse del servizio Batch.

Per altre informazioni sull'abilitazione e sull'uso di log di diagnostica di Batch, vedere [Registrazione diagnostica di Azure Batch](https://azure.microsoft.com/documentation/articles/batch-diagnostics/).

## <a name="diagnostic-logs"></a>Log di diagnostica

servizio Azure Batch Hello genera hello dopo gli eventi di log di diagnostica nel corso della durata hello di alcune risorse di Batch.

**Eventi del log del servizio**
* [Creazione di pool](batch-pool-create-event.md)
* [Avvio dell'eliminazione di pool](batch-pool-delete-start-event.md)
* [Completamento dell'eliminazione di pool](batch-pool-delete-complete-event.md)
* [Avvio del ridimensionamento di pool](batch-pool-resize-start-event.md)
* [Completamento del ridimensionamento di pool](batch-pool-resize-complete-event.md)
* [Avvio dell'attività](batch-task-start-event.md)
* [Attività completata](batch-task-complete-event.md)
* [Errore dell'attività](batch-task-fail-event.md)