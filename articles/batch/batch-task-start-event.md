---
title: "Evento di avvio attività di Azure Batch | Microsoft Docs"
description: "Riferimento per l'evento di avvio dell'attività batch."
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
ms.openlocfilehash: c47ab36c99dddd46a14c15018a2a46bf7f873ffa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="task-start-event"></a><span data-ttu-id="2b056-103">Evento di avvio attività</span><span class="sxs-lookup"><span data-stu-id="2b056-103">Task start event</span></span>

 <span data-ttu-id="2b056-104">Questo evento viene generato una volta che un'attività è stata pianificata per l'avvio su un nodo di calcolo dall'utilità di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="2b056-104">This event is emitted once a task has been scheduled to start on a compute node by the scheduler.</span></span> <span data-ttu-id="2b056-105">Se l'attività viene ritentata o reinserita nella coda, questo evento verrà generato nuovamente per la stessa attività, ma il numero di tentativi e la versione dell'attività di sistema verranno aggiornati di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="2b056-105">Note that if the task is retried or requeued this event will be emitted again for the same task, but the retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="2b056-106">L'esempio seguente illustra il corpo di un evento di avvio attività.</span><span class="sxs-lookup"><span data-stu-id="2b056-106">The following example shows the body of a task start event.</span></span>

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "retryCount": 0
    }
}
```

|<span data-ttu-id="2b056-107">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="2b056-107">Element name</span></span>|<span data-ttu-id="2b056-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="2b056-108">Type</span></span>|<span data-ttu-id="2b056-109">Note</span><span class="sxs-lookup"><span data-stu-id="2b056-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="2b056-110">jobId</span><span class="sxs-lookup"><span data-stu-id="2b056-110">jobId</span></span>|<span data-ttu-id="2b056-111">String</span><span class="sxs-lookup"><span data-stu-id="2b056-111">String</span></span>|<span data-ttu-id="2b056-112">ID del processo contenente l'attività.</span><span class="sxs-lookup"><span data-stu-id="2b056-112">The id of the job containing the task.</span></span>|
|<span data-ttu-id="2b056-113">id</span><span class="sxs-lookup"><span data-stu-id="2b056-113">id</span></span>|<span data-ttu-id="2b056-114">String</span><span class="sxs-lookup"><span data-stu-id="2b056-114">String</span></span>|<span data-ttu-id="2b056-115">ID dell'attività.</span><span class="sxs-lookup"><span data-stu-id="2b056-115">The id of the task.</span></span>|
|<span data-ttu-id="2b056-116">taskType</span><span class="sxs-lookup"><span data-stu-id="2b056-116">taskType</span></span>|<span data-ttu-id="2b056-117">String</span><span class="sxs-lookup"><span data-stu-id="2b056-117">String</span></span>|<span data-ttu-id="2b056-118">Tipo dell'attività.</span><span class="sxs-lookup"><span data-stu-id="2b056-118">The type of the task.</span></span> <span data-ttu-id="2b056-119">Il valore può essere "JobManager" per indicare che si tratta di un'attività del gestore di processi oppure 'User' per indicare che non si tratta di un'attività del gestore di processi.</span><span class="sxs-lookup"><span data-stu-id="2b056-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="2b056-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="2b056-120">systemTaskVersion</span></span>|<span data-ttu-id="2b056-121">Int32</span><span class="sxs-lookup"><span data-stu-id="2b056-121">Int32</span></span>|<span data-ttu-id="2b056-122">Contatore dei tentativi interni di esecuzione di un'attività.</span><span class="sxs-lookup"><span data-stu-id="2b056-122">This is the internal retry counter on a task.</span></span> <span data-ttu-id="2b056-123">Il servizio Batch può ritentare internamente l'esecuzione di un'attività in funzione di problemi transitori.</span><span class="sxs-lookup"><span data-stu-id="2b056-123">Internally the Batch service can retry a task to account for transient issues.</span></span> <span data-ttu-id="2b056-124">Questi problemi possono includere errori interni di pianificazione o tentativi di ripristino a seguito di nodi di calcolo in uno stato non valido.</span><span class="sxs-lookup"><span data-stu-id="2b056-124">These issues can include internal scheduling errors or attempts to recover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="2b056-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="2b056-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="2b056-126">Tipo complesso</span><span class="sxs-lookup"><span data-stu-id="2b056-126">Complex Type</span></span>|<span data-ttu-id="2b056-127">Contiene informazioni sul nodo di calcolo in cui è stata eseguita l'attività.</span><span class="sxs-lookup"><span data-stu-id="2b056-127">Contains information about the compute node on which the task ran.</span></span>|
|[<span data-ttu-id="2b056-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="2b056-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="2b056-129">Tipo complesso</span><span class="sxs-lookup"><span data-stu-id="2b056-129">Complex Type</span></span>|<span data-ttu-id="2b056-130">Specifica che l'attività è un'attività con istanze multiple che richiede più nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="2b056-130">Specifies that the task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="2b056-131">Per informazioni dettagliate, vedere [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task).</span><span class="sxs-lookup"><span data-stu-id="2b056-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="2b056-132">constraints</span><span class="sxs-lookup"><span data-stu-id="2b056-132">constraints</span></span>](#constraints)|<span data-ttu-id="2b056-133">Tipo complesso</span><span class="sxs-lookup"><span data-stu-id="2b056-133">Complex Type</span></span>|<span data-ttu-id="2b056-134">Vincoli di esecuzione che si applicano a questa attività.</span><span class="sxs-lookup"><span data-stu-id="2b056-134">The execution constraints that apply to this task.</span></span>|
|[<span data-ttu-id="2b056-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="2b056-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="2b056-136">Tipo complesso</span><span class="sxs-lookup"><span data-stu-id="2b056-136">Complex Type</span></span>|<span data-ttu-id="2b056-137">Contiene informazioni sull'esecuzione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="2b056-137">Contains information about the execution of the task.</span></span>|

###  <span data-ttu-id="2b056-138"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="2b056-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="2b056-139">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="2b056-139">Element name</span></span>|<span data-ttu-id="2b056-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="2b056-140">Type</span></span>|<span data-ttu-id="2b056-141">Note</span><span class="sxs-lookup"><span data-stu-id="2b056-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="2b056-142">poolId</span><span class="sxs-lookup"><span data-stu-id="2b056-142">poolId</span></span>|<span data-ttu-id="2b056-143">String</span><span class="sxs-lookup"><span data-stu-id="2b056-143">String</span></span>|<span data-ttu-id="2b056-144">ID del pool in cui viene eseguita l'attività.</span><span class="sxs-lookup"><span data-stu-id="2b056-144">The id of the pool on which the task ran.</span></span>|
|<span data-ttu-id="2b056-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="2b056-145">nodeId</span></span>|<span data-ttu-id="2b056-146">String</span><span class="sxs-lookup"><span data-stu-id="2b056-146">String</span></span>|<span data-ttu-id="2b056-147">ID del nodo in cui viene eseguita l'attività.</span><span class="sxs-lookup"><span data-stu-id="2b056-147">The id of the node on which the task ran.</span></span>|

###  <span data-ttu-id="2b056-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="2b056-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="2b056-149">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="2b056-149">Element name</span></span>|<span data-ttu-id="2b056-150">Tipo</span><span class="sxs-lookup"><span data-stu-id="2b056-150">Type</span></span>|<span data-ttu-id="2b056-151">Note</span><span class="sxs-lookup"><span data-stu-id="2b056-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="2b056-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="2b056-152">numberOfInstances</span></span>|<span data-ttu-id="2b056-153">int</span><span class="sxs-lookup"><span data-stu-id="2b056-153">Int</span></span>|<span data-ttu-id="2b056-154">Numero di nodi di calcolo richiesti dall'attività.</span><span class="sxs-lookup"><span data-stu-id="2b056-154">The number of compute nodes required by the task.</span></span>|

###  <span data-ttu-id="2b056-155"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="2b056-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="2b056-156">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="2b056-156">Element name</span></span>|<span data-ttu-id="2b056-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="2b056-157">Type</span></span>|<span data-ttu-id="2b056-158">Note</span><span class="sxs-lookup"><span data-stu-id="2b056-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="2b056-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="2b056-159">maxTaskRetryCount</span></span>|<span data-ttu-id="2b056-160">Int32</span><span class="sxs-lookup"><span data-stu-id="2b056-160">Int32</span></span>|<span data-ttu-id="2b056-161">Numero massimo di tentativi consentiti per l'attività.</span><span class="sxs-lookup"><span data-stu-id="2b056-161">The maximum number of times the task may be retried.</span></span> <span data-ttu-id="2b056-162">Il servizio Batch ripete un'attività se il relativo codice di uscita è diverso da zero.</span><span class="sxs-lookup"><span data-stu-id="2b056-162">The Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="2b056-163">Si noti che questo valore controlla specificamente il numero di tentativi.</span><span class="sxs-lookup"><span data-stu-id="2b056-163">Note that this value specifically controls the number of retries.</span></span> <span data-ttu-id="2b056-164">Il servizio Batch eseguirà l'attività una volta e quindi ripeterà l'esecuzione fino al limite di tentativi specificato.</span><span class="sxs-lookup"><span data-stu-id="2b056-164">The Batch service will try the task once, and may then retry up to this limit.</span></span> <span data-ttu-id="2b056-165">Ad esempio, se il numero massimo di tentativi è 3, il servizio Batch eseguirà l'attività 4 volte, ovvero una iniziale e 3 ulteriori tentativi.</span><span class="sxs-lookup"><span data-stu-id="2b056-165">For example, if the maximum retry count is 3, Batch tries a task up to 4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="2b056-166">Se il numero massimo di tentativi è 0, il servizio Batch non eseguirà ulteriori tentativi.</span><span class="sxs-lookup"><span data-stu-id="2b056-166">If the maximum retry count is 0, the Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="2b056-167">Se il numero massimo di tentativi è -1, il servizio Batch continuerà a eseguire tentativi senza limiti.</span><span class="sxs-lookup"><span data-stu-id="2b056-167">If the maximum retry count is -1, the Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="2b056-168">Il valore predefinito è 0, ovvero nessun tentativo.</span><span class="sxs-lookup"><span data-stu-id="2b056-168">The default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="2b056-169"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="2b056-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="2b056-170">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="2b056-170">Element name</span></span>|<span data-ttu-id="2b056-171">Tipo</span><span class="sxs-lookup"><span data-stu-id="2b056-171">Type</span></span>|<span data-ttu-id="2b056-172">Note</span><span class="sxs-lookup"><span data-stu-id="2b056-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="2b056-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="2b056-173">retryCount</span></span>|<span data-ttu-id="2b056-174">Int32</span><span class="sxs-lookup"><span data-stu-id="2b056-174">Int32</span></span>|<span data-ttu-id="2b056-175">Numero di tentativi di esecuzione dell'attività da parte del servizio Batch.</span><span class="sxs-lookup"><span data-stu-id="2b056-175">The number of times the task has been retried by the Batch service.</span></span> <span data-ttu-id="2b056-176">L'attività viene ritentata se si conclude con un codice di uscita diverso da zero, fino al limite specificato in MaxTaskRetryCount.</span><span class="sxs-lookup"><span data-stu-id="2b056-176">The task is retried if it exits with a nonzero exit code, up to the specified MaxTaskRetryCount</span></span>|
