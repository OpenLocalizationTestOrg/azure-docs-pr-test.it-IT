---
title: "aaa \"eventi di avvio attività di Azure Batch | Documenti di Microsoft\""
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a><span data-ttu-id="9d434-103">Evento di avvio attività</span><span class="sxs-lookup"><span data-stu-id="9d434-103">Task start event</span></span>

 <span data-ttu-id="9d434-104">Questo evento viene generato quando un'attività è stata pianificata toostart su un nodo di calcolo dall'utilità di pianificazione hello.</span><span class="sxs-lookup"><span data-stu-id="9d434-104">This event is emitted once a task has been scheduled toostart on a compute node by hello scheduler.</span></span> <span data-ttu-id="9d434-105">Si noti che se l'attività hello viene ritentata o reinserito nella coda questo evento viene emesso nuovamente per hello stessa attività, ma hello numero di tentativi e versione dell'attività del sistema verrà aggiornato di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="9d434-105">Note that if hello task is retried or requeued this event will be emitted again for hello same task, but hello retry count and system task version will be updated accordingly.</span></span>


 <span data-ttu-id="9d434-106">Hello esempio seguente viene illustrato hello corpo di un evento di inizio delle attività.</span><span class="sxs-lookup"><span data-stu-id="9d434-106">hello following example shows hello body of a task start event.</span></span>

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

|<span data-ttu-id="9d434-107">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="9d434-107">Element name</span></span>|<span data-ttu-id="9d434-108">Tipo</span><span class="sxs-lookup"><span data-stu-id="9d434-108">Type</span></span>|<span data-ttu-id="9d434-109">Note</span><span class="sxs-lookup"><span data-stu-id="9d434-109">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="9d434-110">jobId</span><span class="sxs-lookup"><span data-stu-id="9d434-110">jobId</span></span>|<span data-ttu-id="9d434-111">String</span><span class="sxs-lookup"><span data-stu-id="9d434-111">String</span></span>|<span data-ttu-id="9d434-112">id di Hello del processo di hello contenente attività hello.</span><span class="sxs-lookup"><span data-stu-id="9d434-112">hello id of hello job containing hello task.</span></span>|
|<span data-ttu-id="9d434-113">id</span><span class="sxs-lookup"><span data-stu-id="9d434-113">id</span></span>|<span data-ttu-id="9d434-114">String</span><span class="sxs-lookup"><span data-stu-id="9d434-114">String</span></span>|<span data-ttu-id="9d434-115">id di Hello dell'attività hello.</span><span class="sxs-lookup"><span data-stu-id="9d434-115">hello id of hello task.</span></span>|
|<span data-ttu-id="9d434-116">taskType</span><span class="sxs-lookup"><span data-stu-id="9d434-116">taskType</span></span>|<span data-ttu-id="9d434-117">String</span><span class="sxs-lookup"><span data-stu-id="9d434-117">String</span></span>|<span data-ttu-id="9d434-118">tipo di Hello dell'attività hello.</span><span class="sxs-lookup"><span data-stu-id="9d434-118">hello type of hello task.</span></span> <span data-ttu-id="9d434-119">Il valore può essere "JobManager" per indicare che si tratta di un'attività del gestore di processi oppure 'User' per indicare che non si tratta di un'attività del gestore di processi.</span><span class="sxs-lookup"><span data-stu-id="9d434-119">This can either be 'JobManager' indicating it is a job manager task or 'User' indicating it is not a job manager task.</span></span>|
|<span data-ttu-id="9d434-120">systemTaskVersion</span><span class="sxs-lookup"><span data-stu-id="9d434-120">systemTaskVersion</span></span>|<span data-ttu-id="9d434-121">Int32</span><span class="sxs-lookup"><span data-stu-id="9d434-121">Int32</span></span>|<span data-ttu-id="9d434-122">Si tratta di contatore dei tentativi interni hello in un'attività.</span><span class="sxs-lookup"><span data-stu-id="9d434-122">This is hello internal retry counter on a task.</span></span> <span data-ttu-id="9d434-123">Servizio Batch hello internamente possibile riprovare a eseguire un tooaccount di attività per errori temporanei.</span><span class="sxs-lookup"><span data-stu-id="9d434-123">Internally hello Batch service can retry a task tooaccount for transient issues.</span></span> <span data-ttu-id="9d434-124">Questi problemi possono includere interno pianificazione errori o tentativi toorecover da nodi di calcolo in uno stato non valido.</span><span class="sxs-lookup"><span data-stu-id="9d434-124">These issues can include internal scheduling errors or attempts toorecover from compute nodes in a bad state.</span></span>|
|[<span data-ttu-id="9d434-125">nodeInfo</span><span class="sxs-lookup"><span data-stu-id="9d434-125">nodeInfo</span></span>](#nodeInfo)|<span data-ttu-id="9d434-126">Tipo complesso</span><span class="sxs-lookup"><span data-stu-id="9d434-126">Complex Type</span></span>|<span data-ttu-id="9d434-127">Contiene informazioni sul nodo di calcolo hello in cui hello attività è stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="9d434-127">Contains information about hello compute node on which hello task ran.</span></span>|
|[<span data-ttu-id="9d434-128">multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="9d434-128">multiInstanceSettings</span></span>](#multiInstanceSettings)|<span data-ttu-id="9d434-129">Tipo complesso</span><span class="sxs-lookup"><span data-stu-id="9d434-129">Complex Type</span></span>|<span data-ttu-id="9d434-130">Specifica che l'attività hello è multi-istanza attività che richiedono più nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="9d434-130">Specifies that hello task  is Multi-Instance Task requiring multiple compute nodes.</span></span>  <span data-ttu-id="9d434-131">Per informazioni dettagliate, vedere [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task).</span><span class="sxs-lookup"><span data-stu-id="9d434-131">See [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) for details.</span></span>|
|[<span data-ttu-id="9d434-132">constraints</span><span class="sxs-lookup"><span data-stu-id="9d434-132">constraints</span></span>](#constraints)|<span data-ttu-id="9d434-133">Tipo complesso</span><span class="sxs-lookup"><span data-stu-id="9d434-133">Complex Type</span></span>|<span data-ttu-id="9d434-134">vincoli di esecuzione Hello che si applicano toothis attività.</span><span class="sxs-lookup"><span data-stu-id="9d434-134">hello execution constraints that apply toothis task.</span></span>|
|[<span data-ttu-id="9d434-135">executionInfo</span><span class="sxs-lookup"><span data-stu-id="9d434-135">executionInfo</span></span>](#executionInfo)|<span data-ttu-id="9d434-136">Tipo complesso</span><span class="sxs-lookup"><span data-stu-id="9d434-136">Complex Type</span></span>|<span data-ttu-id="9d434-137">Contiene informazioni sull'esecuzione di hello dell'attività hello.</span><span class="sxs-lookup"><span data-stu-id="9d434-137">Contains information about hello execution of hello task.</span></span>|

###  <span data-ttu-id="9d434-138"><a name="nodeInfo"></a> nodeInfo</span><span class="sxs-lookup"><span data-stu-id="9d434-138"><a name="nodeInfo"></a> nodeInfo</span></span>

|<span data-ttu-id="9d434-139">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="9d434-139">Element name</span></span>|<span data-ttu-id="9d434-140">Tipo</span><span class="sxs-lookup"><span data-stu-id="9d434-140">Type</span></span>|<span data-ttu-id="9d434-141">Note</span><span class="sxs-lookup"><span data-stu-id="9d434-141">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="9d434-142">poolId</span><span class="sxs-lookup"><span data-stu-id="9d434-142">poolId</span></span>|<span data-ttu-id="9d434-143">String</span><span class="sxs-lookup"><span data-stu-id="9d434-143">String</span></span>|<span data-ttu-id="9d434-144">Hello l'id del pool di hello in cui hello attività è stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="9d434-144">hello id of hello pool on which hello task ran.</span></span>|
|<span data-ttu-id="9d434-145">nodeId</span><span class="sxs-lookup"><span data-stu-id="9d434-145">nodeId</span></span>|<span data-ttu-id="9d434-146">String</span><span class="sxs-lookup"><span data-stu-id="9d434-146">String</span></span>|<span data-ttu-id="9d434-147">Hello l'id del nodo di hello in cui hello attività è stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="9d434-147">hello id of hello node on which hello task ran.</span></span>|

###  <span data-ttu-id="9d434-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span><span class="sxs-lookup"><span data-stu-id="9d434-148"><a name="multiInstanceSettings"></a> multiInstanceSettings</span></span>

|<span data-ttu-id="9d434-149">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="9d434-149">Element name</span></span>|<span data-ttu-id="9d434-150">Tipo</span><span class="sxs-lookup"><span data-stu-id="9d434-150">Type</span></span>|<span data-ttu-id="9d434-151">Note</span><span class="sxs-lookup"><span data-stu-id="9d434-151">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="9d434-152">numberOfInstances</span><span class="sxs-lookup"><span data-stu-id="9d434-152">numberOfInstances</span></span>|<span data-ttu-id="9d434-153">int</span><span class="sxs-lookup"><span data-stu-id="9d434-153">Int</span></span>|<span data-ttu-id="9d434-154">numero di Hello dei nodi di calcolo richiesto da attività hello.</span><span class="sxs-lookup"><span data-stu-id="9d434-154">hello number of compute nodes required by hello task.</span></span>|

###  <span data-ttu-id="9d434-155"><a name="constraints"></a> constraints</span><span class="sxs-lookup"><span data-stu-id="9d434-155"><a name="constraints"></a> constraints</span></span>

|<span data-ttu-id="9d434-156">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="9d434-156">Element name</span></span>|<span data-ttu-id="9d434-157">Tipo</span><span class="sxs-lookup"><span data-stu-id="9d434-157">Type</span></span>|<span data-ttu-id="9d434-158">Note</span><span class="sxs-lookup"><span data-stu-id="9d434-158">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="9d434-159">maxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="9d434-159">maxTaskRetryCount</span></span>|<span data-ttu-id="9d434-160">Int32</span><span class="sxs-lookup"><span data-stu-id="9d434-160">Int32</span></span>|<span data-ttu-id="9d434-161">numero massimo di tentativi di esecuzione attività hello può essere di Hello.</span><span class="sxs-lookup"><span data-stu-id="9d434-161">hello maximum number of times hello task may be retried.</span></span> <span data-ttu-id="9d434-162">servizio Batch Hello Riprova a eseguire un'attività se il codice di uscita è diverso da zero.</span><span class="sxs-lookup"><span data-stu-id="9d434-162">hello Batch service retries a task if its exit code is nonzero.</span></span><br /><br /> <span data-ttu-id="9d434-163">Si noti che questo valore controlla in particolare il numero di hello di tentativi.</span><span class="sxs-lookup"><span data-stu-id="9d434-163">Note that this value specifically controls hello number of retries.</span></span> <span data-ttu-id="9d434-164">servizio Batch Hello tenterà attività hello una sola volta e può quindi ripetere di toothis limite.</span><span class="sxs-lookup"><span data-stu-id="9d434-164">hello Batch service will try hello task once, and may then retry up toothis limit.</span></span> <span data-ttu-id="9d434-165">Ad esempio, se il numero massimo di tentativi di hello è 3, Batch tenta un'operazione di backup too4 volte (tentativo iniziale di uno e 3 tentativi).</span><span class="sxs-lookup"><span data-stu-id="9d434-165">For example, if hello maximum retry count is 3, Batch tries a task up too4 times (one initial try and 3 retries).</span></span><br /><br /> <span data-ttu-id="9d434-166">Se il numero massimo di tentativi di hello è 0, hello servizio Batch non ripetere l'attività.</span><span class="sxs-lookup"><span data-stu-id="9d434-166">If hello maximum retry count is 0, hello Batch service does not retry tasks.</span></span><br /><br /> <span data-ttu-id="9d434-167">Se il numero massimo di tentativi di hello è -1, il servizio Batch hello tentativi attività senza limiti.</span><span class="sxs-lookup"><span data-stu-id="9d434-167">If hello maximum retry count is -1, hello Batch service retries tasks without limit.</span></span><br /><br /> <span data-ttu-id="9d434-168">valore predefinito di Hello è 0 (nessun tentativo).</span><span class="sxs-lookup"><span data-stu-id="9d434-168">hello default value is 0 (no retries).</span></span>|

###  <span data-ttu-id="9d434-169"><a name="executionInfo"></a> executionInfo</span><span class="sxs-lookup"><span data-stu-id="9d434-169"><a name="executionInfo"></a> executionInfo</span></span>

|<span data-ttu-id="9d434-170">Nome dell'elemento</span><span class="sxs-lookup"><span data-stu-id="9d434-170">Element name</span></span>|<span data-ttu-id="9d434-171">Tipo</span><span class="sxs-lookup"><span data-stu-id="9d434-171">Type</span></span>|<span data-ttu-id="9d434-172">Note</span><span class="sxs-lookup"><span data-stu-id="9d434-172">Notes</span></span>|
|------------------|----------|-----------|
|<span data-ttu-id="9d434-173">retryCount</span><span class="sxs-lookup"><span data-stu-id="9d434-173">retryCount</span></span>|<span data-ttu-id="9d434-174">Int32</span><span class="sxs-lookup"><span data-stu-id="9d434-174">Int32</span></span>|<span data-ttu-id="9d434-175">numero di volte in cui è stato ripetuto attività hello dal servizio Batch hello di Hello.</span><span class="sxs-lookup"><span data-stu-id="9d434-175">hello number of times hello task has been retried by hello Batch service.</span></span> <span data-ttu-id="9d434-176">attività di Hello viene ritentata se si conclude con un codice di uscita diverso da zero, backup toohello specificato MaxTaskRetryCount</span><span class="sxs-lookup"><span data-stu-id="9d434-176">hello task is retried if it exits with a nonzero exit code, up toohello specified MaxTaskRetryCount</span></span>|
