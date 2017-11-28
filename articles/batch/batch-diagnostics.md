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
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="422a8-103">Registrare gli eventi per la diagnostica e il monitoraggio delle soluzioni Batch</span><span class="sxs-lookup"><span data-stu-id="422a8-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="422a8-104">Come con molti servizi di Azure, hello servizio Batch genera eventi di log per alcune risorse durante hello durata della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="422a8-104">As with many Azure services, hello Batch service emits log events for certain resources during hello lifetime of hello resource.</span></span> <span data-ttu-id="422a8-105">È possibile attivare gli eventi di toorecord i log di diagnostica di Azure Batch per risorse come pool e le attività e quindi utilizzare i registri di hello per il monitoraggio e diagnostica valutazione.</span><span class="sxs-lookup"><span data-stu-id="422a8-105">You can enable Azure Batch diagnostic logs toorecord events for resources like pools and tasks, and then use hello logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="422a8-106">Eventi come la creazione e l'eliminazione di pool, l'avvio e il completamento di attività e di altro tipo sono inclusi nei log di diagnostica di Batch.</span><span class="sxs-lookup"><span data-stu-id="422a8-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="422a8-107">L'articolo illustra gli eventi di registrazione per le risorse degli account Batch, non i dati di output di attività e processi.</span><span class="sxs-lookup"><span data-stu-id="422a8-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="422a8-108">Per ulteriori informazioni sull'archiviazione dei dati di output di hello dei processi e attività, vedere [output di attività e processi Batch di Azure vengono mantenute](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="422a8-108">For details on storing hello output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="422a8-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="422a8-109">Prerequisites</span></span>
* [<span data-ttu-id="422a8-110">Account Azure Batch</span><span class="sxs-lookup"><span data-stu-id="422a8-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="422a8-111">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="422a8-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="422a8-112">toopersist Batch i log di diagnostica, è necessario creare un account di archiviazione di Azure in Azure verrà archiviati i log di hello.</span><span class="sxs-lookup"><span data-stu-id="422a8-112">toopersist Batch diagnostic logs, you must create an Azure Storage account where Azure will store hello logs.</span></span> <span data-ttu-id="422a8-113">È possibile specificare questo account di archiviazione quando si [abilita la registrazione diagnostica](#enable-diagnostic-logging) per l'account Batch.</span><span class="sxs-lookup"><span data-stu-id="422a8-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="422a8-114">account di archiviazione specificato quando si abilita la raccolta di log Hello è non hello stesso come un hello tooin cui account di archiviazione collegati [pacchetti di applicazioni](batch-application-packages.md) e [persistenza dell'output dell'attività](batch-task-output.md) articoli.</span><span class="sxs-lookup"><span data-stu-id="422a8-114">hello Storage account you specify when you enable log collection is not hello same as a linked storage account referred tooin hello [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="422a8-115">Si è **addebitato** per i dati di hello archiviati nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="422a8-115">You are **charged** for hello data stored in your Azure Storage account.</span></span> <span data-ttu-id="422a8-116">Sono inclusi i log di diagnostica hello descritti in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="422a8-116">This includes hello diagnostic logs discussed in this article.</span></span> <span data-ttu-id="422a8-117">Tenere presente questo aspetto quando si progetta il [criterio di conservazione dei log](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="422a8-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="422a8-118">Abilitare la registrazione diagnostica</span><span class="sxs-lookup"><span data-stu-id="422a8-118">Enable diagnostic logging</span></span>
<span data-ttu-id="422a8-119">Per impostazione predefinita, la registrazione diagnostica non è abilitata per l'account Batch.</span><span class="sxs-lookup"><span data-stu-id="422a8-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="422a8-120">È necessario abilitare esplicitamente la registrazione diagnostica per ogni account di Batch da toomonitor:</span><span class="sxs-lookup"><span data-stu-id="422a8-120">You must explicitly enable diagnostic logging for each Batch account you want toomonitor:</span></span>

[<span data-ttu-id="422a8-121">La raccolta di tooenable di log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="422a8-121">How tooenable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="422a8-122">È consigliabile leggere hello completo [Panoramica di Azure i log di diagnostica](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) toogain articolo comprendere non solo modalità registrazione tooenable ma hello log categorie supportate da hello diversi servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="422a8-122">We recommend that you read hello full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article toogain an understanding of not only how tooenable logging, but hello log categories supported by hello various Azure services.</span></span> <span data-ttu-id="422a8-123">Ad esempio, Batch di Azure supporta attualmente una categoria di log: i **log del servizio**.</span><span class="sxs-lookup"><span data-stu-id="422a8-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="422a8-124">Log del servizio</span><span class="sxs-lookup"><span data-stu-id="422a8-124">Service Logs</span></span>
<span data-ttu-id="422a8-125">I log di servizio Azure Batch contengono eventi generati dal servizio Azure Batch hello corso hello di una risorsa di Batch come un pool o un'attività.</span><span class="sxs-lookup"><span data-stu-id="422a8-125">Azure Batch Service Logs contain events emitted by hello Azure Batch service during hello lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="422a8-126">Ogni evento generato dal Batch viene archiviato in hello specificato account di archiviazione in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="422a8-126">Each event emitted by Batch is stored in hello specified Storage account in JSON format.</span></span> <span data-ttu-id="422a8-127">Ad esempio, corrisponde hello corpo di un campione **creazione di un pool evento**:</span><span class="sxs-lookup"><span data-stu-id="422a8-127">For example, this is hello body of a sample **pool create event**:</span></span>

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

<span data-ttu-id="422a8-128">Ogni corpo dell'evento si trova in un JSON file hello specificato l'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="422a8-128">Each event body resides in a .json file in hello specified Azure Storage account.</span></span> <span data-ttu-id="422a8-129">Se si desidera tooaccess hello registri direttamente, è preferibile hello tooreview [schema del log di diagnostica nell'account di archiviazione hello](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span><span class="sxs-lookup"><span data-stu-id="422a8-129">If you want tooaccess hello logs directly, you may wish tooreview hello [schema of Diagnostic Logs in hello storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="422a8-130">Eventi del log del servizio</span><span class="sxs-lookup"><span data-stu-id="422a8-130">Service Log events</span></span>
<span data-ttu-id="422a8-131">Hello servizio Batch crea attualmente hello dopo gli eventi di registro del servizio.</span><span class="sxs-lookup"><span data-stu-id="422a8-131">hello Batch service currently emits hello following Service Log events.</span></span> <span data-ttu-id="422a8-132">Questo elenco potrebbe non essere completo, poiché è possibile che eventi aggiuntivi siano stati aggiunti dopo l'ultimo aggiornamento di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="422a8-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="422a8-133">**Eventi del log del servizio**</span><span class="sxs-lookup"><span data-stu-id="422a8-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="422a8-134">[Pool create][pool_create] (Creazione del pool)</span><span class="sxs-lookup"><span data-stu-id="422a8-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="422a8-135">[Pool delete start][pool_delete_start] (Avvio dell'eliminazione del pool)</span><span class="sxs-lookup"><span data-stu-id="422a8-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="422a8-136">[Pool delete complete][pool_delete_complete] (Completamento dell'eliminazione del pool)</span><span class="sxs-lookup"><span data-stu-id="422a8-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="422a8-137">[Pool resize start][pool_resize_start] (Avvio del ridimensionamento del pool)</span><span class="sxs-lookup"><span data-stu-id="422a8-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="422a8-138">[Pool resize complete][pool_resize_complete] (Completamento del ridimensionamento del pool)</span><span class="sxs-lookup"><span data-stu-id="422a8-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="422a8-139">[Task start][task_start] (Avvio dell'attività)</span><span class="sxs-lookup"><span data-stu-id="422a8-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="422a8-140">[Task complete][task_complete] (Completamento dell'attività)</span><span class="sxs-lookup"><span data-stu-id="422a8-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="422a8-141">[Task fail][task_fail] (Errore dell'attività)</span><span class="sxs-lookup"><span data-stu-id="422a8-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="422a8-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="422a8-142">Next steps</span></span>
<span data-ttu-id="422a8-143">Negli eventi di log di diagnostica toostoring aggiunta in un account di archiviazione di Azure, è inoltre possibile trasmettere Batch servizio Registro eventi tooan [Hub di eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md)e inviarle troppo[Azure Log Analitica](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="422a8-143">In addition toostoring diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them too[Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="422a8-144">Flusso i log di diagnostica Azure tooEvent hub</span><span class="sxs-lookup"><span data-stu-id="422a8-144">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="422a8-145">Il servizio Batch gli eventi di diagnostica toohello dati altamente scalabile in ingresso, hub eventi del flusso.</span><span class="sxs-lookup"><span data-stu-id="422a8-145">Stream Batch diagnostic events toohello highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="422a8-146">Hub eventi è in grado di inserire milioni di eventi al secondo, che è quindi possibile trasformare e archiviare tramite un qualsiasi provider di analisi in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="422a8-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="422a8-147">Analizzare i log di diagnostica di Azure con Log Analytics</span><span class="sxs-lookup"><span data-stu-id="422a8-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="422a8-148">Inviare il tooLog i log di diagnostica Analitica in cui è possibile analizzarli nel portale di Operations Management Suite (OMS) hello o esportarli per l'analisi in Power BI o in Excel.</span><span class="sxs-lookup"><span data-stu-id="422a8-148">Send your diagnostic logs tooLog Analytics where you can analyze them in hello Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
