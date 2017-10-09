---
title: i processi di IoT Hub Azure aaaUnderstand | Documenti Microsoft
description: "Guida per sviluppatori - pianificazione processi toorun su più dispositivi connessi tooyour IoT hub. I processi possono aggiornare i tag e le proprietà desiderate e richiamare metodi diretti su più dispositivi."
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
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="97b15-104">Pianificare processi in più dispositivi</span><span class="sxs-lookup"><span data-stu-id="97b15-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="97b15-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="97b15-105">Overview</span></span>
<span data-ttu-id="97b15-106">Come descritto in articoli precedenti, l'hub IoT di Azure consente un numero di blocchi predefiniti ([tag e proprietà di dispositivi gemelli][lnk-twin-devguide] e [metodi diretti][lnk-dev-methods]).</span><span class="sxs-lookup"><span data-stu-id="97b15-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="97b15-107">In genere, le applicazioni back-end abilitare tooupdate amministratori e operatori di dispositivo e interagiscono con i dispositivi IoT in blocco e a un'ora pianificata.</span><span class="sxs-lookup"><span data-stu-id="97b15-107">Typically, back-end apps enable device administrators and operators tooupdate and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="97b15-108">I processi di incapsulano esecuzione hello di due aggiornamenti del dispositivo e metodi diretti rispetto a un set di dispositivi in una fase di pianificazione.</span><span class="sxs-lookup"><span data-stu-id="97b15-108">Jobs encapsulate hello execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="97b15-109">Ad esempio, un operatore utilizzerebbe un'app di back-end che avviano e tenere traccia di un tooreboot processo un set di dispositivi nella compilazione 43 e floor 3 in un momento che non sarebbe operazioni toohello comportano interruzioni del servizio di compilazione hello.</span><span class="sxs-lookup"><span data-stu-id="97b15-109">For example, an operator would use a back-end app that would initiate and track a job tooreboot a set of devices in building 43 and floor 3 at a time that would not be disruptive toohello operations of hello building.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="97b15-110">Quando toouse</span><span class="sxs-lookup"><span data-stu-id="97b15-110">When toouse</span></span>
<span data-ttu-id="97b15-111">È consigliabile utilizzare processi quando: una soluzione back-end esigenze tooschedule e tenere traccia dello stato delle seguenti attività su un set di dispositivi hello:</span><span class="sxs-lookup"><span data-stu-id="97b15-111">Consider using jobs when: a solution back end needs tooschedule and track progress any of hello following activities on a set of device:</span></span>

* <span data-ttu-id="97b15-112">Aggiornare le proprietà desiderate</span><span class="sxs-lookup"><span data-stu-id="97b15-112">Update desired properties</span></span>
* <span data-ttu-id="97b15-113">Aggiornare i tag</span><span class="sxs-lookup"><span data-stu-id="97b15-113">Update tags</span></span>
* <span data-ttu-id="97b15-114">Richiamare metodi diretti</span><span class="sxs-lookup"><span data-stu-id="97b15-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="97b15-115">Ciclo di vita dei processi</span><span class="sxs-lookup"><span data-stu-id="97b15-115">Job lifecycle</span></span>
<span data-ttu-id="97b15-116">I processi sono avviati dal back-end di soluzione hello e mantenuti dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="97b15-116">Jobs are initiated by hello solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="97b15-117">È possibile avviare un processo tramite un URI del servizio (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) ed eseguire query riguardo allo stato di avanzamento in un processo in esecuzione tramite un URI del servizio (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span><span class="sxs-lookup"><span data-stu-id="97b15-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="97b15-118">Una volta che viene avviato un processo, l'esecuzione di query per i processi consente hello app back-end toorefresh hello stato processi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="97b15-118">Once a job is initiated, querying for jobs enables hello back-end app toorefresh hello status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="97b15-119">Quando si avvia un processo, i valori e nomi di proprietà possono contenere solo US-ASCII stampabili caratteri alfanumerici, ad eccezione di quelli hello seguente insieme: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="97b15-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="97b15-120">Argomenti di riferimento:</span><span class="sxs-lookup"><span data-stu-id="97b15-120">Reference topics:</span></span>
<span data-ttu-id="97b15-121">Hello argomenti di riferimento seguenti offrono ulteriori informazioni sull'utilizzo di processi.</span><span class="sxs-lookup"><span data-stu-id="97b15-121">hello following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-tooexecute-direct-methods"></a><span data-ttu-id="97b15-122">Metodi di processi tooexecute diretti</span><span class="sxs-lookup"><span data-stu-id="97b15-122">Jobs tooexecute direct methods</span></span>
<span data-ttu-id="97b15-123">Hello Ecco i dettagli della richiesta hello HTTP 1.1 per l'esecuzione di un [metodo diretto] [ lnk-dev-methods] in un set di dispositivi tramite un processo:</span><span class="sxs-lookup"><span data-stu-id="97b15-123">hello following is hello HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

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
<span data-ttu-id="97b15-124">condizione di query Hello può anche essere in un singolo Id di dispositivo o in un elenco di ID come mostrato di seguito</span><span class="sxs-lookup"><span data-stu-id="97b15-124">hello query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="97b15-125">**esempi**</span><span class="sxs-lookup"><span data-stu-id="97b15-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="97b15-126">[Linguaggio di query dell'hub IoT][lnk-query] illustra il linguaggio di query dell'hub IoT in maggiore dettaglio.</span><span class="sxs-lookup"><span data-stu-id="97b15-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-tooupdate-device-twin-properties"></a><span data-ttu-id="97b15-127">Proprietà dei processi tooupdate dispositivi doppi</span><span class="sxs-lookup"><span data-stu-id="97b15-127">Jobs tooupdate device twin properties</span></span>
<span data-ttu-id="97b15-128">Hello Ecco i dettagli della richiesta HTTP 1.1 hello per aggiornare le proprietà di un doppio dispositivo tramite un processo:</span><span class="sxs-lookup"><span data-stu-id="97b15-128">hello following is hello HTTP 1.1 request details for updating device twin properties using a job:</span></span>

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

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="97b15-129">Esecuzione di query sull'avanzamento dei processi</span><span class="sxs-lookup"><span data-stu-id="97b15-129">Querying for progress on jobs</span></span>
<span data-ttu-id="97b15-130">Hello Ecco hello i dettagli della richiesta HTTP 1.1 per [l'esecuzione di query per i processi][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="97b15-130">hello following is hello HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="97b15-131">Hello continuationToken viene fornito dalla risposta hello.</span><span class="sxs-lookup"><span data-stu-id="97b15-131">hello continuationToken is provided from hello response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="97b15-132">Proprietà dei processi</span><span class="sxs-lookup"><span data-stu-id="97b15-132">Jobs Properties</span></span>
<span data-ttu-id="97b15-133">Hello seguito è riportato un elenco di proprietà e le descrizioni corrispondente, che possono essere utilizzate quando si eseguono query per i processi o i risultati del processo.</span><span class="sxs-lookup"><span data-stu-id="97b15-133">hello following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="97b15-134">Proprietà</span><span class="sxs-lookup"><span data-stu-id="97b15-134">Property</span></span> | <span data-ttu-id="97b15-135">Description</span><span class="sxs-lookup"><span data-stu-id="97b15-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="97b15-136">**jobId**</span><span class="sxs-lookup"><span data-stu-id="97b15-136">**jobId**</span></span> |<span data-ttu-id="97b15-137">ID dell'applicazione specificato per il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="97b15-137">Application provided ID for hello job.</span></span> |
| <span data-ttu-id="97b15-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="97b15-138">**startTime**</span></span> |<span data-ttu-id="97b15-139">Ora di avvio di applicazioni fornito (ISO 8601) per processo hello.</span><span class="sxs-lookup"><span data-stu-id="97b15-139">Application provided start time (ISO-8601) for hello job.</span></span> |
| <span data-ttu-id="97b15-140">**endTime**</span><span class="sxs-lookup"><span data-stu-id="97b15-140">**endTime**</span></span> |<span data-ttu-id="97b15-141">Data (ISO 8601) IoT Hub previste quando hello processo completato.</span><span class="sxs-lookup"><span data-stu-id="97b15-141">IoT Hub provided date (ISO-8601) for when hello job completed.</span></span> <span data-ttu-id="97b15-142">Valido solo quando il processo di hello raggiunge lo stato 'completato' hello.</span><span class="sxs-lookup"><span data-stu-id="97b15-142">Valid only after hello job reaches hello 'completed' state.</span></span> |
| <span data-ttu-id="97b15-143">**type**</span><span class="sxs-lookup"><span data-stu-id="97b15-143">**type**</span></span> |<span data-ttu-id="97b15-144">Tipi di processi:</span><span class="sxs-lookup"><span data-stu-id="97b15-144">Types of jobs:</span></span> |
| <span data-ttu-id="97b15-145">**scheduledUpdateTwin**: tooupdate un processo utilizzato un set di proprietà desiderata o i tag.</span><span class="sxs-lookup"><span data-stu-id="97b15-145">**scheduledUpdateTwin**: A job used tooupdate a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="97b15-146">**scheduledDeviceMethod**: tooinvoke un processo utilizzato un metodo di dispositivo in un set di gemelli di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="97b15-146">**scheduledDeviceMethod**: A job used tooinvoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="97b15-147">**Stato**</span><span class="sxs-lookup"><span data-stu-id="97b15-147">**status**</span></span> |<span data-ttu-id="97b15-148">Stato corrente del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="97b15-148">Current state of hello job.</span></span> <span data-ttu-id="97b15-149">Valori possibili per lo stato:</span><span class="sxs-lookup"><span data-stu-id="97b15-149">Possible values for status:</span></span> |
| <span data-ttu-id="97b15-150">**in sospeso** : pianificata e in attesa toobe prelevato dal servizio processo hello.</span><span class="sxs-lookup"><span data-stu-id="97b15-150">**pending** : Scheduled and waiting toobe picked up by hello job service.</span></span> | |
| <span data-ttu-id="97b15-151">**pianificato** : pianificata per un'ora nel futuro hello.</span><span class="sxs-lookup"><span data-stu-id="97b15-151">**scheduled** : Scheduled for a time in hello future.</span></span> | |
| <span data-ttu-id="97b15-152">**running**: processo attualmente attivo.</span><span class="sxs-lookup"><span data-stu-id="97b15-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="97b15-153">**cancelled**: processo annullato.</span><span class="sxs-lookup"><span data-stu-id="97b15-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="97b15-154">**failed**: processo non riuscito.</span><span class="sxs-lookup"><span data-stu-id="97b15-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="97b15-155">**completed**: processo completato.</span><span class="sxs-lookup"><span data-stu-id="97b15-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="97b15-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="97b15-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="97b15-157">Statistiche sull'esecuzione del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="97b15-157">Statistics about hello job's execution.</span></span> |

<span data-ttu-id="97b15-158">Proprietà **deviceJobStatistics**.</span><span class="sxs-lookup"><span data-stu-id="97b15-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="97b15-159">Proprietà</span><span class="sxs-lookup"><span data-stu-id="97b15-159">Property</span></span> | <span data-ttu-id="97b15-160">Description</span><span class="sxs-lookup"><span data-stu-id="97b15-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="97b15-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="97b15-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="97b15-162">Numero di dispositivi nel processo di hello.</span><span class="sxs-lookup"><span data-stu-id="97b15-162">Number of devices in hello job.</span></span> |
| <span data-ttu-id="97b15-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="97b15-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="97b15-164">Numero di dispositivi in cui il processo di hello non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="97b15-164">Number of devices where hello job failed.</span></span> |
| <span data-ttu-id="97b15-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="97b15-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="97b15-166">Numero di dispositivi in cui il processo di hello ha avuto esito positivo.</span><span class="sxs-lookup"><span data-stu-id="97b15-166">Number of devices where hello job succeeded.</span></span> |
| <span data-ttu-id="97b15-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="97b15-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="97b15-168">Numero di dispositivi che sono attualmente in esecuzione il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="97b15-168">Number of devices that are currently running hello job.</span></span> |
| <span data-ttu-id="97b15-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="97b15-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="97b15-170">Numero di dispositivi che sono in attesa processo hello toorun.</span><span class="sxs-lookup"><span data-stu-id="97b15-170">Number of devices that are pending toorun hello job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="97b15-171">Materiale di riferimento</span><span class="sxs-lookup"><span data-stu-id="97b15-171">Additional reference material</span></span>
<span data-ttu-id="97b15-172">Altri argomenti di riferimento nella Guida per sviluppatori di IoT Hub hello includono:</span><span class="sxs-lookup"><span data-stu-id="97b15-172">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="97b15-173">[Gli endpoint IoT Hub] [ lnk-endpoints] descrive hello vari endpoint che espone ogni hub IoT per le operazioni in fase di esecuzione e gestione.</span><span class="sxs-lookup"><span data-stu-id="97b15-173">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="97b15-174">[Limitazione delle richieste e le quote] [ lnk-quotas] descrive le quote di hello che si applicano toohello servizio IoT Hub e hello limitazione tooexpect comportamento quando si utilizza servizio hello.</span><span class="sxs-lookup"><span data-stu-id="97b15-174">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="97b15-175">[Gli SDK di dispositivi e servizi di Azure IoT] [ lnk-sdks] elenchi hello language vari SDK è possibile utilizzare quando si sviluppano applicazioni di servizio sia sul dispositivo che interagiscono con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="97b15-175">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="97b15-176">[Il linguaggio di query IoT Hub per gemelli di dispositivo, processi e il routing dei messaggi] [ lnk-query] descrive hello linguaggio di query IoT Hub è possibile utilizzare tooretrieve informazioni dall'IoT Hub sul gemelli di dispositivo e i processi.</span><span class="sxs-lookup"><span data-stu-id="97b15-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="97b15-177">[Supporto di IoT Hub MQTT] [ lnk-devguide-mqtt] fornisce ulteriori informazioni sul supporto di IoT Hub per protocollo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="97b15-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97b15-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="97b15-178">Next steps</span></span>
<span data-ttu-id="97b15-179">Se si desidera tootry alcuni dei concetti di hello descritti in questo articolo, si potrebbero essere interessati hello segue esercitazione IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="97b15-179">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="97b15-180">[Pianificare e trasmettere processi][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="97b15-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

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
