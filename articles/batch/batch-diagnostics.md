---
title: la registrazione diagnostica per gli eventi di Batch - Azure aaaEnable | Documenti Microsoft
description: "Registrare e analizzare gli eventi di registrazione diagnostica per le risorse dell'account Azure Batch, come pool e attività."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: e14e611d-12cd-4671-91dc-bc506dc853e5
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9d03303a3e857e9303f40cc6de5c32b5a51d8f8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a>Registrare gli eventi per la diagnostica e il monitoraggio delle soluzioni Batch

Come con molti servizi di Azure, hello servizio Batch genera eventi di log per alcune risorse durante hello durata della risorsa hello. È possibile attivare gli eventi di toorecord i log di diagnostica di Azure Batch per risorse come pool e le attività e quindi utilizzare i registri di hello per il monitoraggio e diagnostica valutazione. Eventi come la creazione e l'eliminazione di pool, l'avvio e il completamento di attività e di altro tipo sono inclusi nei log di diagnostica di Batch.

> [!NOTE]
> L'articolo illustra gli eventi di registrazione per le risorse degli account Batch, non i dati di output di attività e processi. Per ulteriori informazioni sull'archiviazione dei dati di output di hello dei processi e attività, vedere [output di attività e processi Batch di Azure vengono mantenute](batch-task-output.md).
> 
> 

## <a name="prerequisites"></a>Prerequisiti
* [Account Azure Batch](batch-account-create-portal.md)
* [Account di archiviazione di Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  toopersist Batch i log di diagnostica, è necessario creare un account di archiviazione di Azure in Azure verrà archiviati i log di hello. È possibile specificare questo account di archiviazione quando si [abilita la registrazione diagnostica](#enable-diagnostic-logging) per l'account Batch. account di archiviazione specificato quando si abilita la raccolta di log Hello è non hello stesso come un hello tooin cui account di archiviazione collegati [pacchetti di applicazioni](batch-application-packages.md) e [persistenza dell'output dell'attività](batch-task-output.md) articoli.
  
  > [!WARNING]
  > Si è **addebitato** per i dati di hello archiviati nell'account di archiviazione di Azure. Sono inclusi i log di diagnostica hello descritti in questo articolo. Tenere presente questo aspetto quando si progetta il [criterio di conservazione dei log](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).
  > 
  > 

## <a name="enable-diagnostic-logging"></a>Abilitare la registrazione diagnostica
Per impostazione predefinita, la registrazione diagnostica non è abilitata per l'account Batch. È necessario abilitare esplicitamente la registrazione diagnostica per ogni account di Batch da toomonitor:

[La raccolta di tooenable di log di diagnostica](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

È consigliabile leggere hello completo [Panoramica di Azure i log di diagnostica](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) toogain articolo comprendere non solo modalità registrazione tooenable ma hello log categorie supportate da hello diversi servizi di Azure. Ad esempio, Batch di Azure supporta attualmente una categoria di log: i **log del servizio**.

## <a name="service-logs"></a>Log del servizio
I log di servizio Azure Batch contengono eventi generati dal servizio Azure Batch hello corso hello di una risorsa di Batch come un pool o un'attività. Ogni evento generato dal Batch viene archiviato in hello specificato account di archiviazione in formato JSON. Ad esempio, corrisponde hello corpo di un campione **creazione di un pool evento**:

```json
{
    "poolId": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "4",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicatedComputeNodes": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoscale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

Ogni corpo dell'evento si trova in un JSON file hello specificato l'account di archiviazione di Azure. Se si desidera tooaccess hello registri direttamente, è preferibile hello tooreview [schema del log di diagnostica nell'account di archiviazione hello](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).

## <a name="service-log-events"></a>Eventi del log del servizio
Hello servizio Batch crea attualmente hello dopo gli eventi di registro del servizio. Questo elenco potrebbe non essere completo, poiché è possibile che eventi aggiuntivi siano stati aggiunti dopo l'ultimo aggiornamento di questo articolo.

| **Eventi del log del servizio** |
| --- |
| [Pool create][pool_create] (Creazione del pool) |
| [Pool delete start][pool_delete_start] (Avvio dell'eliminazione del pool) |
| [Pool delete complete][pool_delete_complete] (Completamento dell'eliminazione del pool) |
| [Pool resize start][pool_resize_start] (Avvio del ridimensionamento del pool) |
| [Pool resize complete][pool_resize_complete] (Completamento del ridimensionamento del pool) |
| [Task start][task_start] (Avvio dell'attività) |
| [Task complete][task_complete] (Completamento dell'attività) |
| [Task fail][task_fail] (Errore dell'attività) |

## <a name="next-steps"></a>Passaggi successivi
Negli eventi di log di diagnostica toostoring aggiunta in un account di archiviazione di Azure, è inoltre possibile trasmettere Batch servizio Registro eventi tooan [Hub di eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md)e inviarle troppo[Azure Log Analitica](../log-analytics/log-analytics-overview.md).

* [Flusso i log di diagnostica Azure tooEvent hub](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  Il servizio Batch gli eventi di diagnostica toohello dati altamente scalabile in ingresso, hub eventi del flusso. Hub eventi è in grado di inserire milioni di eventi al secondo, che è quindi possibile trasformare e archiviare tramite un qualsiasi provider di analisi in tempo reale.
* [Analizzare i log di diagnostica di Azure con Log Analytics](../log-analytics/log-analytics-azure-storage.md)
  
  Inviare il tooLog i log di diagnostica Analitica in cui è possibile analizzarli nel portale di Operations Management Suite (OMS) hello o esportarli per l'analisi in Power BI o in Excel.

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
