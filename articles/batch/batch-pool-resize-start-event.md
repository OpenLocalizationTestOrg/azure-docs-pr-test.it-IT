---
title: Evento di avvio ridimensionamento pool di Azure Batch | Microsoft Docs
description: "Riferimento per l’evento di avvio ridimensionamento del pool di batch."
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
ms.openlocfilehash: 826cd984d26b923ba38562e05a2e75c399be9121
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="pool-resize-start-event"></a><span data-ttu-id="0ed27-103">Evento di avvio ridimensionamento pool</span><span class="sxs-lookup"><span data-stu-id="0ed27-103">Pool resize start event</span></span>

 <span data-ttu-id="0ed27-104">Questo evento viene generato quando un ridimensionamento pool è stato avviato.</span><span class="sxs-lookup"><span data-stu-id="0ed27-104">This event is emitted when a pool resize has started.</span></span> <span data-ttu-id="0ed27-105">Poiché il ridimensionamento pool è un evento asincrono, è possibile prevedere l'emissione di un evento di completamento ridimensionamento pool una volta completata l'operazione di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="0ed27-105">Since the pool resize is an asynchronous event, you can expect a pool resize complete event to be emitted once the resize operation completes.</span></span>

 <span data-ttu-id="0ed27-106">L'esempio seguente mostra il corpo di un evento di avvio ridimensionamento pool per un pool che ridimensiona da 0 a 2 nodi con un ridimensionamento manuale.</span><span class="sxs-lookup"><span data-stu-id="0ed27-106">The following example shows the body of a pool resize start event for a pool resizing from 0 to 2 nodes with a manual resize.</span></span>

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|<span data-ttu-id="0ed27-107">Elemento</span><span class="sxs-lookup"><span data-stu-id="0ed27-107">Element</span></span>|<span data-ttu-id="0ed27-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="0ed27-108">Type</span></span>|<span data-ttu-id="0ed27-109">Note</span><span class="sxs-lookup"><span data-stu-id="0ed27-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="0ed27-110">poolId</span><span class="sxs-lookup"><span data-stu-id="0ed27-110">poolId</span></span>|<span data-ttu-id="0ed27-111">String</span><span class="sxs-lookup"><span data-stu-id="0ed27-111">String</span></span>|<span data-ttu-id="0ed27-112">ID del pool.</span><span class="sxs-lookup"><span data-stu-id="0ed27-112">The id of the pool.</span></span>|
|<span data-ttu-id="0ed27-113">nodeDeallocationOption</span><span class="sxs-lookup"><span data-stu-id="0ed27-113">nodeDeallocationOption</span></span>|<span data-ttu-id="0ed27-114">String</span><span class="sxs-lookup"><span data-stu-id="0ed27-114">String</span></span>|<span data-ttu-id="0ed27-115">Specifica quando è possibile rimuovere nodi dal pool, in caso di riduzione delle dimensioni del pool.</span><span class="sxs-lookup"><span data-stu-id="0ed27-115">Specifies when nodes may be removed from the pool, if the pool size is decreasing.</span></span><br /><br /> <span data-ttu-id="0ed27-116">I valori possibili sono:</span><span class="sxs-lookup"><span data-stu-id="0ed27-116">Possible values are:</span></span><br /><br /> <span data-ttu-id="0ed27-117">**requeue**: termina le attività in esecuzione e le reinserisce nella coda.</span><span class="sxs-lookup"><span data-stu-id="0ed27-117">**requeue** – Terminate running tasks and requeue them.</span></span> <span data-ttu-id="0ed27-118">Le attività verranno eseguite di nuovo quando il processo viene abilitato.</span><span class="sxs-lookup"><span data-stu-id="0ed27-118">The tasks will run again when the job is enabled.</span></span> <span data-ttu-id="0ed27-119">I nodi vengono rimossi non appena le attività sono state terminate.</span><span class="sxs-lookup"><span data-stu-id="0ed27-119">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="0ed27-120">**terminate**: termina le attività in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0ed27-120">**terminate** – Terminate running tasks.</span></span> <span data-ttu-id="0ed27-121">Le attività non verranno più eseguite.</span><span class="sxs-lookup"><span data-stu-id="0ed27-121">The tasks will not run again.</span></span> <span data-ttu-id="0ed27-122">I nodi vengono rimossi non appena le attività sono state terminate.</span><span class="sxs-lookup"><span data-stu-id="0ed27-122">Remove nodes as soon as tasks have been terminated.</span></span><br /><br /> <span data-ttu-id="0ed27-123">**taskcompletion**: consente il completamento delle attività attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0ed27-123">**taskcompletion** – Allow currently running tasks to complete.</span></span> <span data-ttu-id="0ed27-124">Non viene pianificata alcuna nuova attività durante l'attesa.</span><span class="sxs-lookup"><span data-stu-id="0ed27-124">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="0ed27-125">I nodi vengono rimossi al completamento di tutte le attività.</span><span class="sxs-lookup"><span data-stu-id="0ed27-125">Remove nodes when all tasks have completed.</span></span><br /><br /> <span data-ttu-id="0ed27-126">**Retaineddata**: consente il completamento delle attività attualmente in esecuzione e quindi attende che scadano tutti i periodi di conservazione dei dati delle attività.</span><span class="sxs-lookup"><span data-stu-id="0ed27-126">**Retaineddata** - Allow currently running tasks to complete, then wait for all task data retention periods to expire.</span></span> <span data-ttu-id="0ed27-127">Non viene pianificata alcuna nuova attività durante l'attesa.</span><span class="sxs-lookup"><span data-stu-id="0ed27-127">Schedule no new tasks while waiting.</span></span> <span data-ttu-id="0ed27-128">I nodi vengono rimossi alla scadenza di tutti i periodi di conservazione dati delle attività.</span><span class="sxs-lookup"><span data-stu-id="0ed27-128">Remove nodes when all task retention periods have expired.</span></span><br /><br /> <span data-ttu-id="0ed27-129">Il valore predefinito è requeue.</span><span class="sxs-lookup"><span data-stu-id="0ed27-129">The default value is requeue.</span></span><br /><br /> <span data-ttu-id="0ed27-130">In caso di aumento delle dimensioni del pool, il valore è impostato su **invalid**.</span><span class="sxs-lookup"><span data-stu-id="0ed27-130">If the pool size is increasing then the value is set to **invalid**.</span></span>|
|<span data-ttu-id="0ed27-131">currentDedicated</span><span class="sxs-lookup"><span data-stu-id="0ed27-131">currentDedicated</span></span>|<span data-ttu-id="0ed27-132">Int32</span><span class="sxs-lookup"><span data-stu-id="0ed27-132">Int32</span></span>|<span data-ttu-id="0ed27-133">Numero di nodi di calcolo attualmente assegnati al pool.</span><span class="sxs-lookup"><span data-stu-id="0ed27-133">The number of compute nodes currently assigned to the pool.</span></span>|
|<span data-ttu-id="0ed27-134">targetDedicated</span><span class="sxs-lookup"><span data-stu-id="0ed27-134">targetDedicated</span></span>|<span data-ttu-id="0ed27-135">Int32</span><span class="sxs-lookup"><span data-stu-id="0ed27-135">Int32</span></span>|<span data-ttu-id="0ed27-136">Numero di nodi di calcolo richiesti per il pool.</span><span class="sxs-lookup"><span data-stu-id="0ed27-136">The number of compute nodes that are requested for the pool.</span></span>|
|<span data-ttu-id="0ed27-137">enableAutoScale</span><span class="sxs-lookup"><span data-stu-id="0ed27-137">enableAutoScale</span></span>|<span data-ttu-id="0ed27-138">Booleano</span><span class="sxs-lookup"><span data-stu-id="0ed27-138">Bool</span></span>|<span data-ttu-id="0ed27-139">Specifica se le dimensioni del pool vengono regolate automaticamente nel tempo.</span><span class="sxs-lookup"><span data-stu-id="0ed27-139">Specifies whether the pool size automatically adjusts over time.</span></span>|
|<span data-ttu-id="0ed27-140">isAutoPool</span><span class="sxs-lookup"><span data-stu-id="0ed27-140">isAutoPool</span></span>|<span data-ttu-id="0ed27-141">Booleano</span><span class="sxs-lookup"><span data-stu-id="0ed27-141">Bool</span></span>|<span data-ttu-id="0ed27-142">Specifica se il pool è stato creato tramite il meccanismo di pool automatico di un processo.</span><span class="sxs-lookup"><span data-stu-id="0ed27-142">Speficies whether the pool was created via a job's AutoPool mechanism.</span></span>|
