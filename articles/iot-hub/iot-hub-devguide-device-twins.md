---
title: Informazioni sui dispositivi gemelli nell'hub IoT di Azure | Documentazione Microsoft
description: Guida per gli sviluppatori - Usare dispositivi gemelli per sincronizzare stato e dati di configurazione tra l'hub IoT e i dispositivi
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b316aa419d558547f90a914a22fb29935076de21
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="d50b0-103">Comprendere e usare dispositivi gemelli nell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="d50b0-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="d50b0-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d50b0-104">Overview</span></span>
<span data-ttu-id="d50b0-105">I *dispositivi gemelli* sono documenti JSON nei quali vengono archiviate informazioni sullo stato dei dispositivi (metadati, configurazioni e condizioni).</span><span class="sxs-lookup"><span data-stu-id="d50b0-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="d50b0-106">L'hub IoT rende permanente un dispositivo gemello per ogni dispositivo che viene connesso all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d50b0-106">IoT Hub persists a device twin for each device that you connect to IoT Hub.</span></span> <span data-ttu-id="d50b0-107">L'articolo illustra:</span><span class="sxs-lookup"><span data-stu-id="d50b0-107">This article describes:</span></span>

* <span data-ttu-id="d50b0-108">La struttura del dispositivo gemello: *tag*, proprietà *desiderate* e *segnalate*.</span><span class="sxs-lookup"><span data-stu-id="d50b0-108">The structure of the device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="d50b0-109">Le operazioni che le app per dispositivo e i back-end possono eseguire sui dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="d50b0-109">The operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="d50b0-110">Al momento i dispositivi gemelli sono accessibili solo dai dispositivi che si connettono all'hub IoT tramite il protocollo MQTT.</span><span class="sxs-lookup"><span data-stu-id="d50b0-110">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="d50b0-111">Per istruzioni su come convertire l'app per dispositivo esistente in modo che usi MQTT, vedere l'articolo [Supporto di MQTT][lnk-devguide-mqtt].</span><span class="sxs-lookup"><span data-stu-id="d50b0-111">Refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>
> 
> 

### <a name="when-to-use"></a><span data-ttu-id="d50b0-112">Quando usare le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="d50b0-112">When to use</span></span>
<span data-ttu-id="d50b0-113">Usare i dispositivi gemelli per:</span><span class="sxs-lookup"><span data-stu-id="d50b0-113">Use device twins to:</span></span>

* <span data-ttu-id="d50b0-114">Archiviare i metadati specifici del dispositivo nel cloud,</span><span class="sxs-lookup"><span data-stu-id="d50b0-114">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="d50b0-115">ad esempio il percorso di distribuzione di un distributore automatico.</span><span class="sxs-lookup"><span data-stu-id="d50b0-115">For example, the deployment location of a vending machine.</span></span>
* <span data-ttu-id="d50b0-116">Segnalare informazioni sullo stato corrente, come funzionalità disponibili e condizioni dall'app per dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d50b0-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="d50b0-117">Ad esempio, un dispositivo è connesso all'hub IoT mediante il cellulare o il Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="d50b0-117">For example, a device is connected to your IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="d50b0-118">Sincronizzare lo stato dei flussi di lavoro a esecuzione prolungata tra l'app per dispositivi e back-end,</span><span class="sxs-lookup"><span data-stu-id="d50b0-118">Synchronize the state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="d50b0-119">ad esempio quando il back-end della soluzione specifica la nuova versione del firmware da installare e l'app per dispositivo segnala le varie fasi del processo di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="d50b0-119">For example, when the solution back end specifies the new firmware version to install, and the device app reports the various stages of the update process.</span></span>
* <span data-ttu-id="d50b0-120">Eseguire query sui metadati, la configurazione o lo stato dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="d50b0-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="d50b0-121">Vedere [Indicazioni sulle comunicazioni da dispositivo a cloud][lnk-d2c-guidance] per informazioni sull'uso delle proprietà indicate, dei messaggi da dispositivo a cloud o del caricamento di file.</span><span class="sxs-lookup"><span data-stu-id="d50b0-121">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="d50b0-122">Vedere [Indicazioni sulle comunicazioni da cloud a dispositivo][lnk-c2d-guidance] per informazioni sull'uso delle proprietà specifiche, dei metodi diretti o dei messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d50b0-122">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="d50b0-123">Dispositivi gemelli</span><span class="sxs-lookup"><span data-stu-id="d50b0-123">Device twins</span></span>
<span data-ttu-id="d50b0-124">I dispositivi gemelli consentono di archiviare informazioni sul dispositivo che possono essere usate:</span><span class="sxs-lookup"><span data-stu-id="d50b0-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="d50b0-125">Dal dispositivo e dai back-end per sincronizzare condizioni e configurazione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d50b0-125">Device and back ends can use to synchronize device conditions and configuration.</span></span>
* <span data-ttu-id="d50b0-126">Dal back-end della soluzione per eseguire query e come destinazione delle operazioni a esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="d50b0-126">The solution back end can use to query and target long-running operations.</span></span>

<span data-ttu-id="d50b0-127">Il ciclo di vita di un dispositivo gemello è correlato all'[identità del dispositivo][lnk-identity] corrispondente.</span><span class="sxs-lookup"><span data-stu-id="d50b0-127">The lifecycle of a device twin is linked to the corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="d50b0-128">I dispositivi gemelli vengono creati ed eliminati implicitamente quando viene creata o eliminata una nuova identità del dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d50b0-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="d50b0-129">Un dispositivo gemello è un documento JSON che include:</span><span class="sxs-lookup"><span data-stu-id="d50b0-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="d50b0-130">**Tag**.</span><span class="sxs-lookup"><span data-stu-id="d50b0-130">**Tags**.</span></span> <span data-ttu-id="d50b0-131">Una sezione del documento JSON che il back-end della soluzione è in grado di leggere e in cui può scrivere.</span><span class="sxs-lookup"><span data-stu-id="d50b0-131">A section of the JSON document that the solution back end can read from and write to.</span></span> <span data-ttu-id="d50b0-132">I tag non sono visibili alle applicazioni per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="d50b0-132">Tags are not visible to device apps.</span></span>
* <span data-ttu-id="d50b0-133">**Proprietà desiderate**.</span><span class="sxs-lookup"><span data-stu-id="d50b0-133">**Desired properties**.</span></span> <span data-ttu-id="d50b0-134">Sono usate insieme alle proprietà segnalate per sincronizzare la configurazione o le condizioni del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d50b0-134">Used along with reported properties to synchronize device configuration or conditions.</span></span> <span data-ttu-id="d50b0-135">Le proprietà desiderate possono essere impostate solo dal back-end della soluzione e possono essere lette dall'app per dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d50b0-135">Desired properties can only be set by the solution back end and can be read by the device app.</span></span> <span data-ttu-id="d50b0-136">L'app per dispositivo può anche ricevere in tempo reale le notifiche relative alle modifiche apportate alle proprietà desiderate.</span><span class="sxs-lookup"><span data-stu-id="d50b0-136">The device app can also be notified in real time of changes in the desired properties.</span></span>
* <span data-ttu-id="d50b0-137">**Proprietà segnalate**.</span><span class="sxs-lookup"><span data-stu-id="d50b0-137">**Reported properties**.</span></span> <span data-ttu-id="d50b0-138">Sono usate insieme alle proprietà desiderate per sincronizzare la configurazione o le condizioni del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d50b0-138">Used along with desired properties to synchronize device configuration or conditions.</span></span> <span data-ttu-id="d50b0-139">Le proprietà segnalate possono essere impostate solo dall'app per dispositivo e possono essere lette e sottoposte a query dal back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="d50b0-139">Reported properties can only be set by the device app and can be read and queried by the solution back end.</span></span>

<span data-ttu-id="d50b0-140">La radice del documento JSON del dispositivo gemello, inoltre, contiene le proprietà di sola lettura dell'identità di dispositivo corrispondente archiviata nel [registro delle identità][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="d50b0-140">Additionally, the root of the device twin JSON document contains the read-only properties from the corresponding device identity stored in the [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="d50b0-141">L'esempio seguente illustra un documento JSON del dispositivo gemello:</span><span class="sxs-lookup"><span data-stu-id="d50b0-141">The following example shows a device twin JSON document:</span></span>

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

<span data-ttu-id="d50b0-142">Nell'oggetto radice si trovano le proprietà di sistema e gli oggetti contenitore per `tags` ed entrambe le proprietà `reported` e `desired`.</span><span class="sxs-lookup"><span data-stu-id="d50b0-142">In the root object, are the system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="d50b0-143">Nel contenitore `properties` sono presenti alcuni elementi di sola lettura (`$metadata`, `$etag` e `$version`) descritti nelle sezioni [Metadati del dispositivo gemello][lnk-twin-metadata] e [Concorrenza ottimistica][lnk-concurrency].</span><span class="sxs-lookup"><span data-stu-id="d50b0-143">The `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in the [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="d50b0-144">Esempio di proprietà segnalata</span><span class="sxs-lookup"><span data-stu-id="d50b0-144">Reported property example</span></span>
<span data-ttu-id="d50b0-145">Nell'esempio precedente, il dispositivo gemello contiene la proprietà `batteryLevel` che viene segnalata dall'app per dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d50b0-145">In the previous example, the device twin contains a `batteryLevel` property that is reported by the device app.</span></span> <span data-ttu-id="d50b0-146">Questa proprietà consente di eseguire una query e di far funzionare i dispositivi in base al livello di carica della batteria più recente segnalato.</span><span class="sxs-lookup"><span data-stu-id="d50b0-146">This property makes it possible to query and operate on devices based on the last reported battery level.</span></span> <span data-ttu-id="d50b0-147">Altri esempi sono l'app per dispositivo che segnala le funzionalità o le opzioni di connettività del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d50b0-147">Other examples include the device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="d50b0-148">Le proprietà segnalate semplificano gli scenari in cui il back-end della soluzione è interessato all'ultimo valore noto di una proprietà.</span><span class="sxs-lookup"><span data-stu-id="d50b0-148">Reported properties simplify scenarios where the solution back end is interested in the last known value of a property.</span></span> <span data-ttu-id="d50b0-149">Usare i [messaggi dal dispositivo al cloud][lnk-d2c] se il back-end della soluzione deve elaborare la telemetria del dispositivo in forma di sequenze di eventi con timestamp, ad esempio una serie temporale.</span><span class="sxs-lookup"><span data-stu-id="d50b0-149">Use [device-to-cloud messages][lnk-d2c] if the solution back end needs to process device telemetry in the form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="d50b0-150">Esempio di proprietà desiderata</span><span class="sxs-lookup"><span data-stu-id="d50b0-150">Desired property example</span></span>
<span data-ttu-id="d50b0-151">Nell'esempio precedente le proprietà desiderate e segnalate del dispositivo gemello `telemetryConfig` vengono usate dal back-end della soluzione e dall'app per dispositivo per sincronizzare la configurazione della telemetria per questo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d50b0-151">In the previous example, the `telemetryConfig` device twin desired and reported properties are used by the solution back end and the device app to synchronize the telemetry configuration for this device.</span></span> <span data-ttu-id="d50b0-152">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d50b0-152">For example:</span></span>

1. <span data-ttu-id="d50b0-153">Il back-end della soluzione imposta la proprietà desiderata sul valore di configurazione desiderato.</span><span class="sxs-lookup"><span data-stu-id="d50b0-153">The solution back end sets the desired property with the desired configuration value.</span></span> <span data-ttu-id="d50b0-154">Questa è la parte del documento con il set di proprietà desiderate:</span><span class="sxs-lookup"><span data-stu-id="d50b0-154">Here is the portion of the document with the desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="d50b0-155">L'applicazione per dispositivo riceve notifica della modifica immediatamente se connessa o alla prima riconnessione.</span><span class="sxs-lookup"><span data-stu-id="d50b0-155">The device app is notified of the change immediately if connected, or at the first reconnect.</span></span> <span data-ttu-id="d50b0-156">L'app segnala quindi la configurazione aggiornata o una condizione di errore riscontrata nell'uso della proprietà `status`.</span><span class="sxs-lookup"><span data-stu-id="d50b0-156">The device app then reports the updated configuration (or an error condition using the `status` property).</span></span> <span data-ttu-id="d50b0-157">Questa è la parte con le proprietà segnalate:</span><span class="sxs-lookup"><span data-stu-id="d50b0-157">Here is the portion of the reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="d50b0-158">Il back-end della soluzione può tenere traccia dei risultati dell'operazione di configurazione su più dispositivi, eseguendo [query][lnk-query] sui dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="d50b0-158">The solution back end can track the results of the configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="d50b0-159">I frammenti di codice precedenti sono esempi ottimizzati per una migliore leggibilità, di un modo per codificare una configurazione del dispositivo e il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="d50b0-159">The preceding snippets are examples, optimized for readability, of one way to encode a device configuration and its status.</span></span> <span data-ttu-id="d50b0-160">L'hub IoT non impone uno schema specifico per l'uso delle proprietà desiderate e segnalate del dispositivo gemello nei dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="d50b0-160">IoT Hub does not impose a specific schema for the device twin desired and reported properties in the device twins.</span></span>
> 
> 

<span data-ttu-id="d50b0-161">È possibile usare i gemelli per sincronizzare le operazioni a esecuzione prolungata, ad esempio gli aggiornamenti del firmware.</span><span class="sxs-lookup"><span data-stu-id="d50b0-161">You can use twins to synchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="d50b0-162">Per altre informazioni su come usare le proprietà per sincronizzare e tenere traccia dell'operazione a esecuzione prolungata sui dispositivi, vedere [Usare le proprietà desiderate per configurare i dispositivi][lnk-twin-properties].</span><span class="sxs-lookup"><span data-stu-id="d50b0-162">For more information on how to use properties to synchronize and track a long running operation across devices, see [Use desired properties to configure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="d50b0-163">Operazioni di back-end</span><span class="sxs-lookup"><span data-stu-id="d50b0-163">Back-end operations</span></span>
<span data-ttu-id="d50b0-164">Il back-end della soluzione opera sul dispositivo gemello tramite le seguenti operazioni atomiche esposte tramite HTTP:</span><span class="sxs-lookup"><span data-stu-id="d50b0-164">The solution back end operates on the device twin using the following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="d50b0-165">**Recuperare un dispositivo gemello tramite ID**. Questa operazione restituisce il documento del dispositivo gemello, inclusi tag e proprietà desiderate, segnalate e di sistema.</span><span class="sxs-lookup"><span data-stu-id="d50b0-165">**Retrieve device twin by id**. This operation returns the device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="d50b0-166">**Aggiornare parzialmente il dispositivo gemello**.</span><span class="sxs-lookup"><span data-stu-id="d50b0-166">**Partially update device twin**.</span></span> <span data-ttu-id="d50b0-167">Questa operazione consente al back-end della soluzione di aggiornare parzialmente i tag o le proprietà desiderate di un dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="d50b0-167">This operation enables the solution back end to partially update the tags or desired properties in a device twin.</span></span> <span data-ttu-id="d50b0-168">L'aggiornamento parziale è espresso come documento JSON che aggiunge o aggiorna tutte le proprietà.</span><span class="sxs-lookup"><span data-stu-id="d50b0-168">The partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="d50b0-169">Le proprietà impostate su `null` vengono rimosse.</span><span class="sxs-lookup"><span data-stu-id="d50b0-169">Properties set to `null` are removed.</span></span> <span data-ttu-id="d50b0-170">L'esempio seguente crea una nuova proprietà desiderata con valore `{"newProperty": "newValue"}`, sostituisce il valore esistente di `existingProperty` con `"otherNewValue"`, e rimuove `otherOldProperty`.</span><span class="sxs-lookup"><span data-stu-id="d50b0-170">The following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites the existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="d50b0-171">Non vengono apportate altre modifiche alle altre proprietà desiderate o ai tag esistenti:</span><span class="sxs-lookup"><span data-stu-id="d50b0-171">No other changes are made to existing desired properties or tags:</span></span>
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. <span data-ttu-id="d50b0-172">**Sostituzione di proprietà desiderate**.</span><span class="sxs-lookup"><span data-stu-id="d50b0-172">**Replace desired properties**.</span></span> <span data-ttu-id="d50b0-173">Questa operazione consente al back-end della soluzione di sovrascrivere completamente tutte le proprietà desiderate esistenti e di sostituirle con un nuovo documento JSON `properties/desired`.</span><span class="sxs-lookup"><span data-stu-id="d50b0-173">This operation enables the solution back end to completely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="d50b0-174">**Sostituzione di tag**.</span><span class="sxs-lookup"><span data-stu-id="d50b0-174">**Replace tags**.</span></span> <span data-ttu-id="d50b0-175">Questa operazione consente al back-end della soluzione di sovrascrivere completamente tutti i tag esistenti e di sostituirli con un nuovo documento JSON `tags`.</span><span class="sxs-lookup"><span data-stu-id="d50b0-175">This operation enables the solution back end to completely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
5. <span data-ttu-id="d50b0-176">**Ricezione di notifiche relative al dispositivo gemello**.</span><span class="sxs-lookup"><span data-stu-id="d50b0-176">**Receive twin notifications**.</span></span> <span data-ttu-id="d50b0-177">Questa operazione invia notifiche al back-end della soluzione a ogni modifica del dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="d50b0-177">This operation allows the solution back end to be notified when the twin is modified.</span></span> <span data-ttu-id="d50b0-178">A questo scopo, la soluzione IoT deve creare una route e impostare l'origine dati su *twinChangeEvents*.</span><span class="sxs-lookup"><span data-stu-id="d50b0-178">To do so, your IoT solution needs to create a route and to set the Data Source equal to *twinChangeEvents*.</span></span> <span data-ttu-id="d50b0-179">Per impostazione predefinita, non viene inviata alcuna notifica, ovvero queste route non sono preesistenti.</span><span class="sxs-lookup"><span data-stu-id="d50b0-179">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="d50b0-180">Se la frequenza delle modifiche è troppo elevata o per altri motivi, come un errore interno, l'hub IoT potrebbe inviare solo una notifica che contiene tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="d50b0-180">If the rate of change is too high, or for other reasons, such as internal failures, the IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="d50b0-181">Di conseguenza, se l'applicazione ha bisogno di controllo e registrazione affidabili di tutti gli stati intermedi, è consigliabile continuare a usare i messaggi D2C.</span><span class="sxs-lookup"><span data-stu-id="d50b0-181">So, if your application needs reliable auditing and logging of all intermediate states, then it is still recommended that you use D2C messages.</span></span> <span data-ttu-id="d50b0-182">Il messaggio di notifica relativo al dispositivo gemello include le proprietà e il corpo.</span><span class="sxs-lookup"><span data-stu-id="d50b0-182">The twin notification message includes properties, and body.</span></span>

    - <span data-ttu-id="d50b0-183">Proprietà</span><span class="sxs-lookup"><span data-stu-id="d50b0-183">Properties</span></span>

    | <span data-ttu-id="d50b0-184">Nome</span><span class="sxs-lookup"><span data-stu-id="d50b0-184">Name</span></span> | <span data-ttu-id="d50b0-185">Valore</span><span class="sxs-lookup"><span data-stu-id="d50b0-185">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="d50b0-186">$content-type</span><span class="sxs-lookup"><span data-stu-id="d50b0-186">$content-type</span></span> | <span data-ttu-id="d50b0-187">application/json</span><span class="sxs-lookup"><span data-stu-id="d50b0-187">application/json</span></span> |
    <span data-ttu-id="d50b0-188">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="d50b0-188">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="d50b0-189">Data e ora in cui è stata inviata la notifica</span><span class="sxs-lookup"><span data-stu-id="d50b0-189">Time when the notification was sent</span></span> |
    <span data-ttu-id="d50b0-190">$iothub-message-source</span><span class="sxs-lookup"><span data-stu-id="d50b0-190">$iothub-message-source</span></span> | <span data-ttu-id="d50b0-191">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="d50b0-191">twinChangeEvents</span></span> |
    <span data-ttu-id="d50b0-192">$content-encoding</span><span class="sxs-lookup"><span data-stu-id="d50b0-192">$content-encoding</span></span> | <span data-ttu-id="d50b0-193">utf-8</span><span class="sxs-lookup"><span data-stu-id="d50b0-193">utf-8</span></span> |
    <span data-ttu-id="d50b0-194">deviceId</span><span class="sxs-lookup"><span data-stu-id="d50b0-194">deviceId</span></span> | <span data-ttu-id="d50b0-195">ID del dispositivo</span><span class="sxs-lookup"><span data-stu-id="d50b0-195">Id of the device</span></span> |
    <span data-ttu-id="d50b0-196">hubName</span><span class="sxs-lookup"><span data-stu-id="d50b0-196">hubName</span></span> | <span data-ttu-id="d50b0-197">Nome dell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="d50b0-197">Name of IoT Hub</span></span> |
    <span data-ttu-id="d50b0-198">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="d50b0-198">operationTimestamp</span></span> | <span data-ttu-id="d50b0-199">Timestamp [ISO8601] dell'operazione</span><span class="sxs-lookup"><span data-stu-id="d50b0-199">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="d50b0-200">iothub-message-schema</span><span class="sxs-lookup"><span data-stu-id="d50b0-200">iothub-message-schema</span></span> | <span data-ttu-id="d50b0-201">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="d50b0-201">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="d50b0-202">opType</span><span class="sxs-lookup"><span data-stu-id="d50b0-202">opType</span></span> | <span data-ttu-id="d50b0-203">"replaceTwin" o "updateTwin"</span><span class="sxs-lookup"><span data-stu-id="d50b0-203">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="d50b0-204">Le proprietà di sistema del messaggio hanno come prefisso il simbolo `'$'`.</span><span class="sxs-lookup"><span data-stu-id="d50b0-204">Message system properties are prefixed with the `'$'` symbol.</span></span>

    - <span data-ttu-id="d50b0-205">Corpo</span><span class="sxs-lookup"><span data-stu-id="d50b0-205">Body</span></span>
        
    <span data-ttu-id="d50b0-206">Questa sezione include tutte le modifiche apportate al dispositivo gemello in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="d50b0-206">This section includes all the twin changes in a JSON format.</span></span> <span data-ttu-id="d50b0-207">Usa lo stesso formato di una patch, con la differenza che può contenere tutte le sezioni, ovvero tag, properties.reported e properties.desired, e che contiene gli elementi "$metadata".</span><span class="sxs-lookup"><span data-stu-id="d50b0-207">It uses the same format as a patch, with the difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains the “$metadata” elements.</span></span> <span data-ttu-id="d50b0-208">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="d50b0-208">For example,</span></span>
    ```
    {
        "properties": {
            "desired": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            },
            "reported": {
                "$metadata": {
                    "$lastUpdated": "2016-02-30T16:24:48.789Z"
                },
                "$version": 1
            }
        }
    }
    ``` 

<span data-ttu-id="d50b0-209">Tutte le operazioni precedenti supportano la [concorrenza ottimistica][lnk-concurrency] e richiedono l'autorizzazione **ServiceConnect**, come indicato nell'articolo [Sicurezza][lnk-security].</span><span class="sxs-lookup"><span data-stu-id="d50b0-209">All the preceding operations support [Optimistic concurrency][lnk-concurrency] and require the **ServiceConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="d50b0-210">Oltre a queste operazioni, il back-end della soluzione può:</span><span class="sxs-lookup"><span data-stu-id="d50b0-210">In addition to these operations, the solution back end can:</span></span>

* <span data-ttu-id="d50b0-211">Eseguire una query sui dispositivi gemelli usando il [linguaggio di query Hub IoT ][lnk-query] simile a SQL.</span><span class="sxs-lookup"><span data-stu-id="d50b0-211">Query the device twins using the SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="d50b0-212">Eseguire operazioni su set di grandi dimensioni dei dispositivi gemelli usando i [processi][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="d50b0-212">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="d50b0-213">Operazioni del dispositivo</span><span class="sxs-lookup"><span data-stu-id="d50b0-213">Device operations</span></span>
<span data-ttu-id="d50b0-214">Il dispositivo opera sul dispositivo gemello usando le seguenti operazioni atomiche:</span><span class="sxs-lookup"><span data-stu-id="d50b0-214">The device app operates on the device twin using the following atomic operations:</span></span>

1. <span data-ttu-id="d50b0-215">**Recuperare un dispositivo gemello**.</span><span class="sxs-lookup"><span data-stu-id="d50b0-215">**Retrieve device twin**.</span></span> <span data-ttu-id="d50b0-216">Questa operazione restituisce il documento del dispositivo gemello, inclusi tag e proprietà desiderate, segnalate e di sistema, del dispositivo attualmente connesso.</span><span class="sxs-lookup"><span data-stu-id="d50b0-216">This operation returns the device twin document (including tags and desired, reported and system properties) for the currently connected device.</span></span>
2. <span data-ttu-id="d50b0-217">**Aggiornamento parziale delle proprietà segnalate**.</span><span class="sxs-lookup"><span data-stu-id="d50b0-217">**Partially update reported properties**.</span></span> <span data-ttu-id="d50b0-218">Questa operazione consente l'aggiornamento parziale delle proprietà segnalate del dispositivo attualmente connesso.</span><span class="sxs-lookup"><span data-stu-id="d50b0-218">This operation enables the partial update of the reported properties of the currently connected device.</span></span> <span data-ttu-id="d50b0-219">Questa operazione usa lo stesso formato di aggiornamento JSON che il back-end della soluzione usa per un aggiornamento parziale delle proprietà desiderate.</span><span class="sxs-lookup"><span data-stu-id="d50b0-219">This operation uses the same JSON update format that the solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="d50b0-220">**Osservazione di proprietà desiderate**.</span><span class="sxs-lookup"><span data-stu-id="d50b0-220">**Observe desired properties**.</span></span> <span data-ttu-id="d50b0-221">Il dispositivo attualmente connesso può scegliere di ricevere la notifica degli aggiornamenti delle proprietà desiderate quando vengono eseguiti.</span><span class="sxs-lookup"><span data-stu-id="d50b0-221">The currently connected device can choose to be notified of updates to the desired properties when they happen.</span></span> <span data-ttu-id="d50b0-222">Il dispositivo riceve lo stesso modulo di aggiornamento che segnala la sostituzione parziale o completa eseguita dal back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="d50b0-222">The device receives the same form of update (partial or full replacement) executed by the solution back end.</span></span>

<span data-ttu-id="d50b0-223">Tutte le operazioni precedenti richiedono l'autorizzazione **DeviceConnect**, come indicato nell'articolo [Sicurezza][lnk-security].</span><span class="sxs-lookup"><span data-stu-id="d50b0-223">All the preceding operations require the **DeviceConnect** permission, as defined in the [Security][lnk-security] article.</span></span>

<span data-ttu-id="d50b0-224">[Azure IoT SDK per dispositivi][lnk-sdks] semplifica l'uso delle operazioni precedenti con linguaggi e piattaforme diversi.</span><span class="sxs-lookup"><span data-stu-id="d50b0-224">The [Azure IoT device SDKs][lnk-sdks] make it easy to use the preceding operations from many languages and platforms.</span></span> <span data-ttu-id="d50b0-225">Altre informazioni sulle primitive dell'hub IoT per la sincronizzazione delle proprietà desiderate sono reperibili nella sezione [Flusso di riconnessione del dispositivo][lnk-reconnection].</span><span class="sxs-lookup"><span data-stu-id="d50b0-225">More information on the details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="d50b0-226">Al momento i dispositivi gemelli sono accessibili solo dai dispositivi che si connettono all'hub IoT tramite il protocollo MQTT.</span><span class="sxs-lookup"><span data-stu-id="d50b0-226">Currently, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="d50b0-227">Argomenti di riferimento:</span><span class="sxs-lookup"><span data-stu-id="d50b0-227">Reference topics:</span></span>
<span data-ttu-id="d50b0-228">Gli argomenti di riferimento seguenti offrono altre informazioni sul controllo dell'accesso all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d50b0-228">The following reference topics provide you with more information about controlling access to your IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="d50b0-229">Formato di tag e proprietà</span><span class="sxs-lookup"><span data-stu-id="d50b0-229">Tags and properties format</span></span>
<span data-ttu-id="d50b0-230">I tag e le proprietà desiderate e segnalate sono oggetti JSON soggetti alle restrizioni indicate di seguito:</span><span class="sxs-lookup"><span data-stu-id="d50b0-230">Tags, desired, and reported properties are JSON objects with the following restrictions:</span></span>

* <span data-ttu-id="d50b0-231">Tutte le chiavi negli oggetti JSON sono stringhe UTF-8 UNICODE da 64 caratteri con distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="d50b0-231">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="d50b0-232">I caratteri consentiti escludono i caratteri di controllo UNICODE (segmenti C0 e C1) e `'.'`, `' '`, `'$'`.</span><span class="sxs-lookup"><span data-stu-id="d50b0-232">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="d50b0-233">Tutti i valori negli oggetti JSON possono essere dei seguenti tipi JSON: booleano, numero, stringa, oggetto.</span><span class="sxs-lookup"><span data-stu-id="d50b0-233">All values in JSON objects can be of the following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="d50b0-234">Non sono consentite le matrici.</span><span class="sxs-lookup"><span data-stu-id="d50b0-234">Arrays are not allowed.</span></span>
* <span data-ttu-id="d50b0-235">Tutti gli oggetti JSON nei tag e nelle proprietà desiderate e segnalate possono avere una profondità massima di 5.</span><span class="sxs-lookup"><span data-stu-id="d50b0-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="d50b0-236">Ad esempio, l'oggetto seguente è valido:</span><span class="sxs-lookup"><span data-stu-id="d50b0-236">For instance, the following object is valid:</span></span>

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* <span data-ttu-id="d50b0-237">Tutti i valori di stringa possono avere una lunghezza massima di 512 byte.</span><span class="sxs-lookup"><span data-stu-id="d50b0-237">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="d50b0-238">Dimensioni del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="d50b0-238">Device twin size</span></span>
<span data-ttu-id="d50b0-239">L'hub IoT impone un limite di dimensione pari a 8 KB sui valori di `tags`, `properties/desired` e `properties/reported`, a esclusione degli elementi di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="d50b0-239">IoT Hub enforces an 8KB size limitation on the values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="d50b0-240">Le dimensioni vengono calcolate contando tutti i caratteri a esclusione dei caratteri di controllo UNICODE (segmenti C0 e C1) e lo spazio `' '` quando è visualizzato al di fuori di una costante di tipo stringa.</span><span class="sxs-lookup"><span data-stu-id="d50b0-240">The size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="d50b0-241">L'hub IoT rifiuta con errore tutte le operazioni che aumentano le dimensioni dei documenti oltre il limite specificato.</span><span class="sxs-lookup"><span data-stu-id="d50b0-241">IoT Hub rejects with an error all operations that would increase the size of those documents above the limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="d50b0-242">Metadati del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="d50b0-242">Device twin metadata</span></span>
<span data-ttu-id="d50b0-243">L'hub IoT conserva il timestamp dell'ultimo aggiornamento di ogni oggetto JSON nelle proprietà desiderate e segnalate del dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="d50b0-243">IoT Hub maintains the timestamp of the last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="d50b0-244">I timestamp sono in formato UTC e codificati in formato [ISO8601]`YYYY-MM-DDTHH:MM:SS.mmmZ`.</span><span class="sxs-lookup"><span data-stu-id="d50b0-244">The timestamps are in UTC and encoded in the [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="d50b0-245">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d50b0-245">For example:</span></span>

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

<span data-ttu-id="d50b0-246">Queste informazioni vengono mantenute a ogni livello (non solo al livello foglia della struttura JSON) per conservare gli aggiornamenti che rimuovono le chiavi dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="d50b0-246">This information is kept at every level (not just the leaves of the JSON structure) to preserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="d50b0-247">Concorrenza ottimistica</span><span class="sxs-lookup"><span data-stu-id="d50b0-247">Optimistic concurrency</span></span>
<span data-ttu-id="d50b0-248">I tag e le proprietà desiderate e segnalate supportano la concorrenza ottimistica.</span><span class="sxs-lookup"><span data-stu-id="d50b0-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="d50b0-249">I tag sono dotati di un ETag, come indicato in [RFC7232], che rappresenta il JSON del tag.</span><span class="sxs-lookup"><span data-stu-id="d50b0-249">Tags have an ETag, as per [RFC7232], that represents the tag's JSON representation.</span></span> <span data-ttu-id="d50b0-250">Per garantire la coerenza è possibile usare l'ETag nelle operazioni di aggiornamento condizionale dal back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="d50b0-250">You can use ETags in conditional update operations from the solution back end to ensure consistency.</span></span>

<span data-ttu-id="d50b0-251">Le proprietà desiderate e segnalate del dispositivo gemello non sono dotate di ETags, ma hanno un valore `$version` sempre incrementale.</span><span class="sxs-lookup"><span data-stu-id="d50b0-251">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed to be incremental.</span></span> <span data-ttu-id="d50b0-252">In modo analogo a un valore ETag, la versione può essere usata dall'entità di aggiornamento per garantire la coerenza degli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="d50b0-252">Similarly to an ETag, the version can be used by the updating party to enforce consistency of updates.</span></span> <span data-ttu-id="d50b0-253">Ad esempio, un'app per dispositivo per una proprietà segnalata o la soluzione del back-end per una proprietà desiderata.</span><span class="sxs-lookup"><span data-stu-id="d50b0-253">For example, a device app for a reported property or the solution back end for a desired property.</span></span>

<span data-ttu-id="d50b0-254">Le versioni sono utili anche quando un agente di osservazione, ad esempio l'app per dispositivo che osserva le proprietà desiderate, deve riconciliare le concorrenze tra il risultato di un'operazione di recupero e una notifica di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="d50b0-254">Versions are also useful when an observing agent (such as the device app observing the desired properties) must reconcile races between the result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="d50b0-255">Altre informazioni sono reperibili nella sezione [Flusso di riconnessione del dispositivo][lnk-reconnection].</span><span class="sxs-lookup"><span data-stu-id="d50b0-255">The section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="d50b0-256">Flusso di riconnessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="d50b0-256">Device reconnection flow</span></span>
<span data-ttu-id="d50b0-257">L'hub IoT non conserva le notifiche di aggiornamento delle proprietà desiderate dei dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="d50b0-257">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="d50b0-258">Ne consegue che un dispositivo che esegue la connessione deve recuperare il documento completo delle proprietà desiderate, ed eseguire la sottoscrizione alle notifiche di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="d50b0-258">It follows that a device that is connecting must retrieve the full desired properties document, in addition to subscribing for update notifications.</span></span> <span data-ttu-id="d50b0-259">Data la possibilità di concorrenza tra le notifiche di aggiornamento e il recupero completo, deve essere assicurato il flusso seguente:</span><span class="sxs-lookup"><span data-stu-id="d50b0-259">Given the possibility of races between update notifications and full retrieval, the following flow must be ensured:</span></span>

1. <span data-ttu-id="d50b0-260">L'app per dispositivo esegue la connessione a un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d50b0-260">Device app connects to an IoT hub.</span></span>
2. <span data-ttu-id="d50b0-261">L'app per dispositivo esegue la sottoscrizione per le notifiche di aggiornamento delle proprietà desiderate.</span><span class="sxs-lookup"><span data-stu-id="d50b0-261">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="d50b0-262">L'app per dispositivo recupera il documento completo delle proprietà desiderate.</span><span class="sxs-lookup"><span data-stu-id="d50b0-262">Device app retrieves the full document for desired properties.</span></span>

<span data-ttu-id="d50b0-263">L'app per dispositivo è in grado di ignorare tutte le notifiche con il valore di `$version` minore o uguale a quello dell'intero documento recuperato.</span><span class="sxs-lookup"><span data-stu-id="d50b0-263">The device app can ignore all notifications with `$version` less or equal than the version of the full retrieved document.</span></span> <span data-ttu-id="d50b0-264">Questo approccio è possibile poiché l'hub IoT garantisce l'incremento delle versioni.</span><span class="sxs-lookup"><span data-stu-id="d50b0-264">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="d50b0-265">Questa logica è già implementata in [Azure IoT SDK per dispositivi][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="d50b0-265">This logic is already implemented in the [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="d50b0-266">La descrizione è utile solo se l'app per dispositivo non può usare un Azure IoT SDK per dispositivi e deve programmare direttamente l'interfaccia MQTT.</span><span class="sxs-lookup"><span data-stu-id="d50b0-266">This description is useful only if the device app cannot use any of Azure IoT device SDKs and must program the MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="d50b0-267">Materiale di riferimento</span><span class="sxs-lookup"><span data-stu-id="d50b0-267">Additional reference material</span></span>
<span data-ttu-id="d50b0-268">Di seguito sono indicati altri argomenti di riferimento reperibili nella Guida per gli sviluppatori dell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="d50b0-268">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="d50b0-269">L'articolo [IoT Hub endpoints][lnk-endpoints] (Endpoint dell'hub IoT) illustra i diversi endpoint esposti da ogni hub IoT per operazioni della fase di esecuzione e di gestione.</span><span class="sxs-lookup"><span data-stu-id="d50b0-269">The [IoT Hub endpoints][lnk-endpoints] article describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="d50b0-270">L'articolo [Quote e limitazioni][lnk-quotas] descrive le quote applicabili al servizio hub IoT e il comportamento di limitazione previsto quando si usa il servizio.</span><span class="sxs-lookup"><span data-stu-id="d50b0-270">The [Throttling and quotas][lnk-quotas] article describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="d50b0-271">L'articolo [Azure IoT SDK per dispositivi e servizi][lnk-sdks] elenca gli SDK nei diversi linguaggi che è possibile usare quando si sviluppano app per dispositivi e servizi che interagiscono con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d50b0-271">The [Azure IoT device and service SDKs][lnk-sdks] article lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="d50b0-272">L'articolo [Linguaggio di query dell'hub IoT per dispositivi gemelli, processi e routing di messaggi][lnk-query] descrive il linguaggio di query dell’hub IoT che è possibile usare per recuperare informazioni dall’hub IoT sui processi e i dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="d50b0-272">The [IoT Hub query language for device twins, jobs, and message routing][lnk-query] article describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="d50b0-273">L'articolo [Supporto di MQTT nell'hub IoT][lnk-devguide-mqtt] offre altre informazioni sul supporto dell'hub IoT per il protocollo MQTT.</span><span class="sxs-lookup"><span data-stu-id="d50b0-273">The [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d50b0-274">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d50b0-274">Next steps</span></span>
<span data-ttu-id="d50b0-275">In questa esercitazione si è appreso come usare i dispositivi gemelli. Altri argomenti di interesse disponibili nella Guida per sviluppatori dell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="d50b0-275">Now you have learned about device twins, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="d50b0-276">[Richiamare un metodo diretto in un dispositivo][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="d50b0-276">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="d50b0-277">[Pianificare processi in più dispositivi][lnk-jobs]</span><span class="sxs-lookup"><span data-stu-id="d50b0-277">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="d50b0-278">Per provare alcuni dei concetti descritti in questo articolo, possono essere utili le esercitazioni di hub IoT seguenti:</span><span class="sxs-lookup"><span data-stu-id="d50b0-278">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorials:</span></span>

* <span data-ttu-id="d50b0-279">[Come usare il dispositivo gemello][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="d50b0-279">[How to use the device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="d50b0-280">[Come usare le proprietà del dispositivo gemello][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="d50b0-280">[How to use device twin properties][lnk-twin-properties]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png
