---
title: Abilitare la registrazione diagnostica per eventi di Batch - Azure | Documentazione Microsoft
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
ms.openlocfilehash: b7bc6fd9921ab0f2374ace33ea5c1ab93a78f860
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="916de-103">Registrare gli eventi per la diagnostica e il monitoraggio delle soluzioni Batch</span><span class="sxs-lookup"><span data-stu-id="916de-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="916de-104">Come per molti servizi di Azure, il servizio Batch genera eventi di log per determinate risorse durante il ciclo di vita della risorsa.</span><span class="sxs-lookup"><span data-stu-id="916de-104">As with many Azure services, the Batch service emits log events for certain resources during the lifetime of the resource.</span></span> <span data-ttu-id="916de-105">È possibile abilitare i log di diagnostica di Azure Batch per registrare gli eventi per le risorse, come attività e pool, e quindi usare i log per l'analisi e il monitoraggio diagnostici.</span><span class="sxs-lookup"><span data-stu-id="916de-105">You can enable Azure Batch diagnostic logs to record events for resources like pools and tasks, and then use the logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="916de-106">Eventi come la creazione e l'eliminazione di pool, l'avvio e il completamento di attività e di altro tipo sono inclusi nei log di diagnostica di Batch.</span><span class="sxs-lookup"><span data-stu-id="916de-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="916de-107">L'articolo illustra gli eventi di registrazione per le risorse degli account Batch, non i dati di output di attività e processi.</span><span class="sxs-lookup"><span data-stu-id="916de-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="916de-108">Per i dettagli sull'archiviazione dei dati di output di processi e attività, vedere [Salvare in modo permanente l'output dei processi e delle attività di Azure Batch](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="916de-108">For details on storing the output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="916de-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="916de-109">Prerequisites</span></span>
* [<span data-ttu-id="916de-110">Account Azure Batch</span><span class="sxs-lookup"><span data-stu-id="916de-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="916de-111">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="916de-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="916de-112">Per salvare in modo permanente i log di diagnostica di Batch, è necessario creare un account di archiviazione di Azure in cui verranno archiviati i log.</span><span class="sxs-lookup"><span data-stu-id="916de-112">To persist Batch diagnostic logs, you must create an Azure Storage account where Azure will store the logs.</span></span> <span data-ttu-id="916de-113">È possibile specificare questo account di archiviazione quando si [abilita la registrazione diagnostica](#enable-diagnostic-logging) per l'account Batch.</span><span class="sxs-lookup"><span data-stu-id="916de-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="916de-114">L'account di archiviazione specificato quando si abilita la raccolta di log non è lo stesso account di archiviazione collegato a cui si fa riferimento negli articoli relativi ai [pacchetti dell'applicazione](batch-application-packages.md) e alla [persistenza dell'output delle attività](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="916de-114">The Storage account you specify when you enable log collection is not the same as a linked storage account referred to in the [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="916de-115">Si riceverà un **addebito** per i dati archiviati nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="916de-115">You are **charged** for the data stored in your Azure Storage account.</span></span> <span data-ttu-id="916de-116">Sono inclusi i log di diagnostica descritti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="916de-116">This includes the diagnostic logs discussed in this article.</span></span> <span data-ttu-id="916de-117">Tenere presente questo aspetto quando si progetta il [criterio di conservazione dei log](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="916de-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="916de-118">Abilitare la registrazione diagnostica</span><span class="sxs-lookup"><span data-stu-id="916de-118">Enable diagnostic logging</span></span>
<span data-ttu-id="916de-119">Per impostazione predefinita, la registrazione diagnostica non è abilitata per l'account Batch.</span><span class="sxs-lookup"><span data-stu-id="916de-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="916de-120">È necessario abilitare esplicitamente la registrazione diagnostica per ogni account Batch da monitorare:</span><span class="sxs-lookup"><span data-stu-id="916de-120">You must explicitly enable diagnostic logging for each Batch account you want to monitor:</span></span>

[<span data-ttu-id="916de-121">Come abilitare la raccolta dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="916de-121">How to enable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="916de-122">È consigliabile leggere fino in fondo l'articolo [Panoramica dei log di diagnostica di Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) per comprendere non solo come abilitare la registrazione, ma anche le categorie di log supportate dai vari servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="916de-122">We recommend that you read the full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article to gain an understanding of not only how to enable logging, but the log categories supported by the various Azure services.</span></span> <span data-ttu-id="916de-123">Ad esempio, Batch di Azure supporta attualmente una categoria di log: i **log del servizio**.</span><span class="sxs-lookup"><span data-stu-id="916de-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="916de-124">Log del servizio</span><span class="sxs-lookup"><span data-stu-id="916de-124">Service Logs</span></span>
<span data-ttu-id="916de-125">I log del servizio di Azure Batch contengono gli eventi generati dal servizio Azure Batch durante il ciclo di vita di una risorsa di Batch, come un'attività o un pool.</span><span class="sxs-lookup"><span data-stu-id="916de-125">Azure Batch Service Logs contain events emitted by the Azure Batch service during the lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="916de-126">Ogni evento generato da Batch viene archiviato nell'account di archiviazione specificato nel formato JSON.</span><span class="sxs-lookup"><span data-stu-id="916de-126">Each event emitted by Batch is stored in the specified Storage account in JSON format.</span></span> <span data-ttu-id="916de-127">Ad esempio, questo è il corpo di un **evento di creazione pool** di esempio:</span><span class="sxs-lookup"><span data-stu-id="916de-127">For example, this is the body of a sample **pool create event**:</span></span>

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

<span data-ttu-id="916de-128">Ogni corpo dell'evento risiede in un file con estensione json nell'account di archiviazione di Azure specificato.</span><span class="sxs-lookup"><span data-stu-id="916de-128">Each event body resides in a .json file in the specified Azure Storage account.</span></span> <span data-ttu-id="916de-129">Per accedere direttamente ai log, si consiglia di esaminare lo [schema dei log di diagnostica nell'account di archiviazione](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span><span class="sxs-lookup"><span data-stu-id="916de-129">If you want to access the logs directly, you may wish to review the [schema of Diagnostic Logs in the storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="916de-130">Eventi del log del servizio</span><span class="sxs-lookup"><span data-stu-id="916de-130">Service Log events</span></span>
<span data-ttu-id="916de-131">Il servizio Batch attualmente emette gli eventi di log del servizio seguenti.</span><span class="sxs-lookup"><span data-stu-id="916de-131">The Batch service currently emits the following Service Log events.</span></span> <span data-ttu-id="916de-132">Questo elenco potrebbe non essere completo, poiché è possibile che eventi aggiuntivi siano stati aggiunti dopo l'ultimo aggiornamento di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="916de-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="916de-133">**Eventi del log del servizio**</span><span class="sxs-lookup"><span data-stu-id="916de-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="916de-134">[Pool create][pool_create] (Creazione del pool)</span><span class="sxs-lookup"><span data-stu-id="916de-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="916de-135">[Pool delete start][pool_delete_start] (Avvio dell'eliminazione del pool)</span><span class="sxs-lookup"><span data-stu-id="916de-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="916de-136">[Pool delete complete][pool_delete_complete] (Completamento dell'eliminazione del pool)</span><span class="sxs-lookup"><span data-stu-id="916de-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="916de-137">[Pool resize start][pool_resize_start] (Avvio del ridimensionamento del pool)</span><span class="sxs-lookup"><span data-stu-id="916de-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="916de-138">[Pool resize complete][pool_resize_complete] (Completamento del ridimensionamento del pool)</span><span class="sxs-lookup"><span data-stu-id="916de-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="916de-139">[Task start][task_start] (Avvio dell'attività)</span><span class="sxs-lookup"><span data-stu-id="916de-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="916de-140">[Task complete][task_complete] (Completamento dell'attività)</span><span class="sxs-lookup"><span data-stu-id="916de-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="916de-141">[Task fail][task_fail] (Errore dell'attività)</span><span class="sxs-lookup"><span data-stu-id="916de-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="916de-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="916de-142">Next steps</span></span>
<span data-ttu-id="916de-143">Oltre ad archiviare gli eventi dei log di diagnostica in un account di archiviazione di Azure, è possibile anche trasmettere gli eventi del log del servizio Batch a un [Hub eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md) e inviarli ad [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="916de-143">In addition to storing diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them to [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="916de-144">Trasmettere log di diagnostica di Azure a Hub eventi</span><span class="sxs-lookup"><span data-stu-id="916de-144">Stream Azure Diagnostic Logs to Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="916de-145">Trasmettere in streaming il flusso di eventi diagnostici di Batch al servizio dati in ingresso a scalabilità elevata, Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="916de-145">Stream Batch diagnostic events to the highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="916de-146">Hub eventi è in grado di inserire milioni di eventi al secondo, che è quindi possibile trasformare e archiviare tramite un qualsiasi provider di analisi in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="916de-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="916de-147">Analizzare i log di diagnostica di Azure con Log Analytics</span><span class="sxs-lookup"><span data-stu-id="916de-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="916de-148">Inviare i log diagnostici a Log Analytics, in cui è possibile analizzarli nel portale di Operations Management Suite (OMS) o esportarli per l'analisi in Excel o Power BI.</span><span class="sxs-lookup"><span data-stu-id="916de-148">Send your diagnostic logs to Log Analytics where you can analyze them in the Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
