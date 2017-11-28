---
title: Informazioni sui processi hub IoT di Azure | Microsoft Docs
description: "Guida per sviluppatori - Pianificazione di processi da eseguire in più dispositivi connessi all'hub di IoT. I processi possono aggiornare i tag e le proprietà desiderate e richiamare metodi diretti su più dispositivi."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: abb7f80662650efa8f158f32125ebc5350cb4f62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="71dc1-104">Pianificare processi in più dispositivi</span><span class="sxs-lookup"><span data-stu-id="71dc1-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="71dc1-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="71dc1-105">Overview</span></span>
<span data-ttu-id="71dc1-106">Come descritto in articoli precedenti, l'hub IoT di Azure consente un numero di blocchi predefiniti ([tag e proprietà di dispositivi gemelli][lnk-twin-devguide] e [metodi diretti][lnk-dev-methods]).</span><span class="sxs-lookup"><span data-stu-id="71dc1-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="71dc1-107">In genere, le app back-end consentono agli amministratori dei dispositivi e agli operatori di aggiornare i dispositivi IoT in blocco e a un'ora pianificata e di interagirvi.</span><span class="sxs-lookup"><span data-stu-id="71dc1-107">Typically, back-end apps enable device administrators and operators to update and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="71dc1-108">I processi incapsulano l'esecuzione di aggiornamenti dei dispositivi gemelli e i metodi diretti rispetto a un set di dispositivi a un'ora pianificata.</span><span class="sxs-lookup"><span data-stu-id="71dc1-108">Jobs encapsulate the execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="71dc1-109">Ad esempio, un operatore userà un'app back-end avviata e terrà traccia di un processo per riavviare un set di dispositivi al terzo piano dell'edificio 43 in un orario opportuno per non interrompere le attività dell'edificio.</span><span class="sxs-lookup"><span data-stu-id="71dc1-109">For example, an operator would use a back-end app that would initiate and track a job to reboot a set of devices in building 43 and floor 3 at a time that would not be disruptive to the operations of the building.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="71dc1-110">Quando usare le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="71dc1-110">When to use</span></span>
<span data-ttu-id="71dc1-111">È consigliabile usare processi quando il back-end di una soluzione deve pianificare e tenere traccia dell'avanzamento di una qualsiasi delle attività seguenti in un set di dispositivi:</span><span class="sxs-lookup"><span data-stu-id="71dc1-111">Consider using jobs when: a solution back end needs to schedule and track progress any of the following activities on a set of device:</span></span>

* <span data-ttu-id="71dc1-112">Aggiornare le proprietà desiderate</span><span class="sxs-lookup"><span data-stu-id="71dc1-112">Update desired properties</span></span>
* <span data-ttu-id="71dc1-113">Aggiornare i tag</span><span class="sxs-lookup"><span data-stu-id="71dc1-113">Update tags</span></span>
* <span data-ttu-id="71dc1-114">Richiamare metodi diretti</span><span class="sxs-lookup"><span data-stu-id="71dc1-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="71dc1-115">Ciclo di vita dei processi</span><span class="sxs-lookup"><span data-stu-id="71dc1-115">Job lifecycle</span></span>
<span data-ttu-id="71dc1-116">I processi vengono avviati dal back-end della soluzione e mantenuti dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="71dc1-116">Jobs are initiated by the solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="71dc1-117">È possibile avviare un processo tramite un URI del servizio (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) ed eseguire query riguardo allo stato di avanzamento in un processo in esecuzione tramite un URI del servizio (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span><span class="sxs-lookup"><span data-stu-id="71dc1-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="71dc1-118">Dopo l'avvio del processo, l'esecuzione di query relative ai processi consente all'app back-end aggiornare lo stato dei processi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="71dc1-118">Once a job is initiated, querying for jobs enables the back-end app to refresh the status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="71dc1-119">Quando si avvia un processo, i valori e i nomi di proprietà possono contenere solo caratteri alfanumerici US-ASCII stampabili, ad eccezione dei seguenti: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="71dc1-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="71dc1-120">Argomenti di riferimento:</span><span class="sxs-lookup"><span data-stu-id="71dc1-120">Reference topics:</span></span>
<span data-ttu-id="71dc1-121">Gli argomenti di riferimento seguenti offrono altre informazioni sull'uso dei processi.</span><span class="sxs-lookup"><span data-stu-id="71dc1-121">The following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-to-execute-direct-methods"></a><span data-ttu-id="71dc1-122">Processi per eseguire metodi diretti</span><span class="sxs-lookup"><span data-stu-id="71dc1-122">Jobs to execute direct methods</span></span>
<span data-ttu-id="71dc1-123">Di seguito sono riportati i dettagli di una richiesta HTTP 1.1 per eseguire un [metodo diretto][lnk-dev-methods] in un set di dispositivi tramite un processo:</span><span class="sxs-lookup"><span data-stu-id="71dc1-123">The following is the HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
<span data-ttu-id="71dc1-124">La condizione di query può anche trovarsi in un ID dispositivo singolo o in un elenco di ID dispositivo, come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="71dc1-124">The query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="71dc1-125">**esempi**</span><span class="sxs-lookup"><span data-stu-id="71dc1-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="71dc1-126">[Linguaggio di query dell'hub IoT][lnk-query] illustra il linguaggio di query dell'hub IoT in maggiore dettaglio.</span><span class="sxs-lookup"><span data-stu-id="71dc1-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-to-update-device-twin-properties"></a><span data-ttu-id="71dc1-127">Processi per aggiornare le proprietà dei dispositivi gemelli</span><span class="sxs-lookup"><span data-stu-id="71dc1-127">Jobs to update device twin properties</span></span>
<span data-ttu-id="71dc1-128">Di seguito sono riportati i dettagli di una richiesta HTTP 1.1 per aggiornare le proprietà dei dispositivi gemelli tramite un processo:</span><span class="sxs-lookup"><span data-stu-id="71dc1-128">The following is the HTTP 1.1 request details for updating device twin properties using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="71dc1-129">Esecuzione di query sull'avanzamento dei processi</span><span class="sxs-lookup"><span data-stu-id="71dc1-129">Querying for progress on jobs</span></span>
<span data-ttu-id="71dc1-130">Di seguito sono riportati i dettagli di una richiesta HTTP 1.1 per [eseguire query sui processi][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="71dc1-130">The following is the HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="71dc1-131">La risposta fornisce continuationToken.</span><span class="sxs-lookup"><span data-stu-id="71dc1-131">The continuationToken is provided from the response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="71dc1-132">Proprietà dei processi</span><span class="sxs-lookup"><span data-stu-id="71dc1-132">Jobs Properties</span></span>
<span data-ttu-id="71dc1-133">Di seguito è riportato un elenco di proprietà e corrispondenti descrizioni che è possibile usare quando si eseguono query sui processi o sui relativi risultati.</span><span class="sxs-lookup"><span data-stu-id="71dc1-133">The following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="71dc1-134">Proprietà</span><span class="sxs-lookup"><span data-stu-id="71dc1-134">Property</span></span> | <span data-ttu-id="71dc1-135">Description</span><span class="sxs-lookup"><span data-stu-id="71dc1-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="71dc1-136">**jobId**</span><span class="sxs-lookup"><span data-stu-id="71dc1-136">**jobId**</span></span> |<span data-ttu-id="71dc1-137">ID fornito dall'applicazione per il processo.</span><span class="sxs-lookup"><span data-stu-id="71dc1-137">Application provided ID for the job.</span></span> |
| <span data-ttu-id="71dc1-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="71dc1-138">**startTime**</span></span> |<span data-ttu-id="71dc1-139">Ora di inizio fornita dall'applicazione (ISO 8601) per il processo.</span><span class="sxs-lookup"><span data-stu-id="71dc1-139">Application provided start time (ISO-8601) for the job.</span></span> |
| <span data-ttu-id="71dc1-140">**endTime**</span><span class="sxs-lookup"><span data-stu-id="71dc1-140">**endTime**</span></span> |<span data-ttu-id="71dc1-141">Data fornita dall'hub IoT (ISO 8601) per il completamento del processo.</span><span class="sxs-lookup"><span data-stu-id="71dc1-141">IoT Hub provided date (ISO-8601) for when the job completed.</span></span> <span data-ttu-id="71dc1-142">È valida solo quando il processo raggiunge lo stato di completamento.</span><span class="sxs-lookup"><span data-stu-id="71dc1-142">Valid only after the job reaches the 'completed' state.</span></span> |
| <span data-ttu-id="71dc1-143">**type**</span><span class="sxs-lookup"><span data-stu-id="71dc1-143">**type**</span></span> |<span data-ttu-id="71dc1-144">Tipi di processi:</span><span class="sxs-lookup"><span data-stu-id="71dc1-144">Types of jobs:</span></span> |
| <span data-ttu-id="71dc1-145">**scheduledUpdateTwin**: un processo usato per aggiornare un set di proprietà o tag desiderati.</span><span class="sxs-lookup"><span data-stu-id="71dc1-145">**scheduledUpdateTwin**: A job used to update a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="71dc1-146">**scheduledDeviceMethod**: un processo usato per richiamare un metodo di dispositivo in un set di dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="71dc1-146">**scheduledDeviceMethod**: A job used to invoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="71dc1-147">**Stato**</span><span class="sxs-lookup"><span data-stu-id="71dc1-147">**status**</span></span> |<span data-ttu-id="71dc1-148">Stato corrente del processo.</span><span class="sxs-lookup"><span data-stu-id="71dc1-148">Current state of the job.</span></span> <span data-ttu-id="71dc1-149">Valori possibili per lo stato:</span><span class="sxs-lookup"><span data-stu-id="71dc1-149">Possible values for status:</span></span> |
| <span data-ttu-id="71dc1-150">**pending**: processo pianificato e in attesa del prelievo da parte del servizio del processo.</span><span class="sxs-lookup"><span data-stu-id="71dc1-150">**pending** : Scheduled and waiting to be picked up by the job service.</span></span> | |
| <span data-ttu-id="71dc1-151">**scheduled**: processo pianificato per un'ora futura.</span><span class="sxs-lookup"><span data-stu-id="71dc1-151">**scheduled** : Scheduled for a time in the future.</span></span> | |
| <span data-ttu-id="71dc1-152">**running**: processo attualmente attivo.</span><span class="sxs-lookup"><span data-stu-id="71dc1-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="71dc1-153">**cancelled**: processo annullato.</span><span class="sxs-lookup"><span data-stu-id="71dc1-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="71dc1-154">**failed**: processo non riuscito.</span><span class="sxs-lookup"><span data-stu-id="71dc1-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="71dc1-155">**completed**: processo completato.</span><span class="sxs-lookup"><span data-stu-id="71dc1-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="71dc1-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="71dc1-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="71dc1-157">Statistiche sull'esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="71dc1-157">Statistics about the job's execution.</span></span> |

<span data-ttu-id="71dc1-158">Proprietà **deviceJobStatistics**.</span><span class="sxs-lookup"><span data-stu-id="71dc1-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="71dc1-159">Proprietà</span><span class="sxs-lookup"><span data-stu-id="71dc1-159">Property</span></span> | <span data-ttu-id="71dc1-160">Description</span><span class="sxs-lookup"><span data-stu-id="71dc1-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="71dc1-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="71dc1-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="71dc1-162">Numero di dispositivi nel processo.</span><span class="sxs-lookup"><span data-stu-id="71dc1-162">Number of devices in the job.</span></span> |
| <span data-ttu-id="71dc1-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="71dc1-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="71dc1-164">Numero di dispositivi in cui il processo non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="71dc1-164">Number of devices where the job failed.</span></span> |
| <span data-ttu-id="71dc1-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="71dc1-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="71dc1-166">Numero di dispositivi in cui il processo è riuscito.</span><span class="sxs-lookup"><span data-stu-id="71dc1-166">Number of devices where the job succeeded.</span></span> |
| <span data-ttu-id="71dc1-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="71dc1-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="71dc1-168">Numero di dispositivi in cui il processo è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="71dc1-168">Number of devices that are currently running the job.</span></span> |
| <span data-ttu-id="71dc1-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="71dc1-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="71dc1-170">Numero di dispositivi in cui il processo è in attesa.</span><span class="sxs-lookup"><span data-stu-id="71dc1-170">Number of devices that are pending to run the job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="71dc1-171">Materiale di riferimento</span><span class="sxs-lookup"><span data-stu-id="71dc1-171">Additional reference material</span></span>
<span data-ttu-id="71dc1-172">Di seguito sono indicati altri argomenti di riferimento reperibili nella Guida per gli sviluppatori dell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="71dc1-172">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="71dc1-173">[Endpoint dell'hub IoT][lnk-endpoints] illustra i diversi endpoint esposti da ogni hub IoT per operazioni della fase di esecuzione e di gestione.</span><span class="sxs-lookup"><span data-stu-id="71dc1-173">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="71dc1-174">[Quote e limitazioni][lnk-quotas] descrive le quote applicabili al servizio Hub IoT e il comportamento di limitazione previsto quando si usa il servizio.</span><span class="sxs-lookup"><span data-stu-id="71dc1-174">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="71dc1-175">[Azure IoT SDK per dispositivi e servizi][lnk-sdks] elenca gli SDK nei diversi linguaggi da usare quando si sviluppano app per dispositivi e servizi che interagiscono con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="71dc1-175">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="71dc1-176">[Il linguaggio di query dell'hub IoT per dispositivi gemelli, processi e routing di messaggi][lnk-query] descrive il linguaggio di query dell’hub IoT che è possibile usare per recuperare informazioni dall’hub IoT sui processi e i dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="71dc1-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="71dc1-177">[Supporto di MQTT nell'hub IoT][lnk-devguide-mqtt] offre altre informazioni sul supporto dell'hub IoT per il protocollo MQTT.</span><span class="sxs-lookup"><span data-stu-id="71dc1-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71dc1-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="71dc1-178">Next steps</span></span>
<span data-ttu-id="71dc1-179">Per provare alcuni dei concetti descritti in questo articolo, può essere utile l'esercitazione seguente sull'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="71dc1-179">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="71dc1-180">[Pianificare e trasmettere processi][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="71dc1-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
