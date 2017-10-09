---
title: gemelli di dispositivi Azure IoT Hub aaaUnderstand | Documenti Microsoft
description: Guida per sviluppatori - dispositivo utilizzare gemelli toosynchronize stato e dati di configurazione tra l'IoT Hub e i dispositivi
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
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a><span data-ttu-id="341a3-103">Comprendere e usare dispositivi gemelli nell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="341a3-103">Understand and use device twins in IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="341a3-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="341a3-104">Overview</span></span>
<span data-ttu-id="341a3-105">I *dispositivi gemelli* sono documenti JSON nei quali vengono archiviate informazioni sullo stato dei dispositivi (metadati, configurazioni e condizioni).</span><span class="sxs-lookup"><span data-stu-id="341a3-105">*Device twins* are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="341a3-106">IoT Hub persiste doppi un dispositivo per ogni dispositivo che si connette tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="341a3-106">IoT Hub persists a device twin for each device that you connect tooIoT Hub.</span></span> <span data-ttu-id="341a3-107">L'articolo illustra:</span><span class="sxs-lookup"><span data-stu-id="341a3-107">This article describes:</span></span>

* <span data-ttu-id="341a3-108">struttura di un doppio dispositivo hello Hello: *tag*, *desiderato* e *segnalati proprietà*, e</span><span class="sxs-lookup"><span data-stu-id="341a3-108">hello structure of hello device twin: *tags*, *desired* and *reported properties*, and</span></span>
* <span data-ttu-id="341a3-109">operazioni di Hello che App per dispositivi e back-end possono eseguire sui gemelli di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="341a3-109">hello operations that device apps and back ends can perform on device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="341a3-110">Attualmente, gemelli di dispositivo sono accessibili solo da dispositivi che si connettono tooIoT Hub utilizzando il protocollo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="341a3-110">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="341a3-111">Fare riferimento toohello [supporto MQTT] [ lnk-devguide-mqtt] per istruzioni su come tooconvert esistente dispositivo app toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="341a3-111">Refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

### <a name="when-toouse"></a><span data-ttu-id="341a3-112">Quando toouse</span><span class="sxs-lookup"><span data-stu-id="341a3-112">When toouse</span></span>
<span data-ttu-id="341a3-113">Usare i dispositivi gemelli per:</span><span class="sxs-lookup"><span data-stu-id="341a3-113">Use device twins to:</span></span>

* <span data-ttu-id="341a3-114">Archiviare i metadati specifici del dispositivo nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="341a3-114">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="341a3-115">Salve, ad esempio, il percorso di distribuzione di una macchina distributore.</span><span class="sxs-lookup"><span data-stu-id="341a3-115">For example, hello deployment location of a vending machine.</span></span>
* <span data-ttu-id="341a3-116">Segnalare informazioni sullo stato corrente, come funzionalità disponibili e condizioni dall'app per dispositivo.</span><span class="sxs-lookup"><span data-stu-id="341a3-116">Report current state information such as available capabilities and conditions from your device app.</span></span> <span data-ttu-id="341a3-117">Ad esempio, un dispositivo è connesso tooyour IoT hub over cellulare o Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="341a3-117">For example, a device is connected tooyour IoT hub over cellular or WiFi.</span></span>
* <span data-ttu-id="341a3-118">Sincronizzazione dello stato di hello dei flussi di lavoro a esecuzione prolungata tra app per dispositivi e app back-end.</span><span class="sxs-lookup"><span data-stu-id="341a3-118">Synchronize hello state of long-running workflows between device app and back-end app.</span></span> <span data-ttu-id="341a3-119">Ad esempio, quando esegue il backup di soluzione hello fine specifica hello nuovo tooinstall di versione del firmware e hello dispositivo app report hello varie fasi del processo di aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="341a3-119">For example, when hello solution back end specifies hello new firmware version tooinstall, and hello device app reports hello various stages of hello update process.</span></span>
* <span data-ttu-id="341a3-120">Eseguire query sui metadati, la configurazione o lo stato dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="341a3-120">Query your device metadata, configuration, or state.</span></span>

<span data-ttu-id="341a3-121">Fare riferimento troppo[materiale sussidiario per la comunicazione da dispositivo a cloud] [ lnk-d2c-guidance] per istruzioni sull'uso di proprietà restituita, i messaggi da dispositivo a cloud o caricamento del file.</span><span class="sxs-lookup"><span data-stu-id="341a3-121">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] for guidance on using reported properties, device-to-cloud messages, or file upload.</span></span>
<span data-ttu-id="341a3-122">Fare riferimento troppo[indicazioni di comunicazione Cloud a dispositivo] [ lnk-c2d-guidance] per istruzioni sull'uso delle proprietà desiderate, metodi diretti o messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="341a3-122">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] for guidance on using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="device-twins"></a><span data-ttu-id="341a3-123">Dispositivi gemelli</span><span class="sxs-lookup"><span data-stu-id="341a3-123">Device twins</span></span>
<span data-ttu-id="341a3-124">I dispositivi gemelli consentono di archiviare informazioni sul dispositivo che possono essere usate:</span><span class="sxs-lookup"><span data-stu-id="341a3-124">Device twins store device-related information that:</span></span>

* <span data-ttu-id="341a3-125">Dispositivo e back end è possibile utilizzare condizioni di dispositivo toosynchronize e configurazione.</span><span class="sxs-lookup"><span data-stu-id="341a3-125">Device and back ends can use toosynchronize device conditions and configuration.</span></span>
* <span data-ttu-id="341a3-126">back-end di Hello soluzione possono utilizzare tooquery e operazioni a esecuzione prolungata di destinazione.</span><span class="sxs-lookup"><span data-stu-id="341a3-126">hello solution back end can use tooquery and target long-running operations.</span></span>

<span data-ttu-id="341a3-127">ciclo di vita di Hello di una coppia di dispositivo è collegato corrispondente toohello [identità del dispositivo][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="341a3-127">hello lifecycle of a device twin is linked toohello corresponding [device identity][lnk-identity].</span></span> <span data-ttu-id="341a3-128">I dispositivi gemelli vengono creati ed eliminati implicitamente quando viene creata o eliminata una nuova identità del dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="341a3-128">Device twins are implicitly created and deleted when a new device identity is created or deleted in IoT Hub.</span></span>

<span data-ttu-id="341a3-129">Un dispositivo gemello è un documento JSON che include:</span><span class="sxs-lookup"><span data-stu-id="341a3-129">A device twin is a JSON document that includes:</span></span>

* <span data-ttu-id="341a3-130">**Tag**.</span><span class="sxs-lookup"><span data-stu-id="341a3-130">**Tags**.</span></span> <span data-ttu-id="341a3-131">Una sezione del documento JSON hello hello soluzione back-end può leggere e scrivere.</span><span class="sxs-lookup"><span data-stu-id="341a3-131">A section of hello JSON document that hello solution back end can read from and write to.</span></span> <span data-ttu-id="341a3-132">Tag non sono visibili toodevice app.</span><span class="sxs-lookup"><span data-stu-id="341a3-132">Tags are not visible toodevice apps.</span></span>
* <span data-ttu-id="341a3-133">**Proprietà desiderate**.</span><span class="sxs-lookup"><span data-stu-id="341a3-133">**Desired properties**.</span></span> <span data-ttu-id="341a3-134">Usata con configurazione del dispositivo toosynchronize proprietà segnalato o condizioni.</span><span class="sxs-lookup"><span data-stu-id="341a3-134">Used along with reported properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="341a3-135">Le proprietà desiderate possono essere impostate solo dalla soluzione hello nuovamente finale e possono essere letto da app per dispositivi hello.</span><span class="sxs-lookup"><span data-stu-id="341a3-135">Desired properties can only be set by hello solution back end and can be read by hello device app.</span></span> <span data-ttu-id="341a3-136">Hello dispositivo app può anche ricevere notifiche in tempo reale delle modifiche nelle proprietà hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="341a3-136">hello device app can also be notified in real time of changes in hello desired properties.</span></span>
* <span data-ttu-id="341a3-137">**Proprietà segnalate**.</span><span class="sxs-lookup"><span data-stu-id="341a3-137">**Reported properties**.</span></span> <span data-ttu-id="341a3-138">Usata con configurazione del dispositivo toosynchronize proprietà desiderate o condizioni.</span><span class="sxs-lookup"><span data-stu-id="341a3-138">Used along with desired properties toosynchronize device configuration or conditions.</span></span> <span data-ttu-id="341a3-139">Proprietà restituita può essere impostata solo per app per dispositivi hello e possano leggere e query hello soluzione back-end.</span><span class="sxs-lookup"><span data-stu-id="341a3-139">Reported properties can only be set by hello device app and can be read and queried by hello solution back end.</span></span>

<span data-ttu-id="341a3-140">Radice hello hello dispositivo doppi JSON documento contiene inoltre le proprietà di sola lettura hello dall'identità periferica corrispondente hello archiviati in hello [Registro di sistema di identità][lnk-identity].</span><span class="sxs-lookup"><span data-stu-id="341a3-140">Additionally, hello root of hello device twin JSON document contains hello read-only properties from hello corresponding device identity stored in hello [identity registry][lnk-identity].</span></span>

![][img-twin]

<span data-ttu-id="341a3-141">Hello di esempio seguente viene illustrato un documento JSON un doppio di dispositivo:</span><span class="sxs-lookup"><span data-stu-id="341a3-141">hello following example shows a device twin JSON document:</span></span>

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

<span data-ttu-id="341a3-142">Nell'oggetto radice hello, è di proprietà di sistema hello e gli oggetti contenitore per `tags` e `reported` e `desired` proprietà.</span><span class="sxs-lookup"><span data-stu-id="341a3-142">In hello root object, are hello system properties, and container objects for `tags` and both `reported` and `desired` properties.</span></span> <span data-ttu-id="341a3-143">Hello `properties` contenitore contiene alcuni elementi di sola lettura (`$metadata`, `$etag`, e `$version`) descritto in hello [dispositivo doppi metadati] [ lnk-twin-metadata] e [ Concorrenza ottimistica] [ lnk-concurrency] sezioni.</span><span class="sxs-lookup"><span data-stu-id="341a3-143">hello `properties` container contains some read-only elements (`$metadata`, `$etag`, and `$version`) described in hello [Device twin metadata][lnk-twin-metadata] and [Optimistic concurrency][lnk-concurrency] sections.</span></span>

### <a name="reported-property-example"></a><span data-ttu-id="341a3-144">Esempio di proprietà segnalata</span><span class="sxs-lookup"><span data-stu-id="341a3-144">Reported property example</span></span>
<span data-ttu-id="341a3-145">Nell'esempio precedente hello doppi dispositivo hello contiene un `batteryLevel` proprietà che viene segnalato da app per dispositivi hello.</span><span class="sxs-lookup"><span data-stu-id="341a3-145">In hello previous example, hello device twin contains a `batteryLevel` property that is reported by hello device app.</span></span> <span data-ttu-id="341a3-146">Questa proprietà rende possibili tooquery e operare sui dispositivi in base al livello di batteria segnalati ultimo hello.</span><span class="sxs-lookup"><span data-stu-id="341a3-146">This property makes it possible tooquery and operate on devices based on hello last reported battery level.</span></span> <span data-ttu-id="341a3-147">Altri esempi hello dispositivo app reporting funzionalità dei dispositivi o le opzioni di connettività.</span><span class="sxs-lookup"><span data-stu-id="341a3-147">Other examples include hello device app reporting device capabilities or connectivity options.</span></span>

> [!NOTE]
> <span data-ttu-id="341a3-148">Proprietà segnalate semplificare gli scenari in cui desidera back-end di hello soluzione hello noto ultimo valore di una proprietà.</span><span class="sxs-lookup"><span data-stu-id="341a3-148">Reported properties simplify scenarios where hello solution back end is interested in hello last known value of a property.</span></span> <span data-ttu-id="341a3-149">Utilizzare [messaggi da dispositivo a cloud] [ lnk-d2c] se hello soluzione back-end deve tooprocess telemetria del dispositivo nel modulo hello di sequenze di eventi impostati i timestamp, ad esempio serie temporale.</span><span class="sxs-lookup"><span data-stu-id="341a3-149">Use [device-to-cloud messages][lnk-d2c] if hello solution back end needs tooprocess device telemetry in hello form of sequences of timestamped events, such as time series.</span></span>

### <a name="desired-property-example"></a><span data-ttu-id="341a3-150">Esempio di proprietà desiderata</span><span class="sxs-lookup"><span data-stu-id="341a3-150">Desired property example</span></span>
<span data-ttu-id="341a3-151">Nell'esempio precedente hello hello `telemetryConfig` doppi dispositivo desiderato e le proprietà segnalate vengono utilizzate da hello soluzione back-end e configurazione del dispositivo app toosynchronize hello telemetria hello per questo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="341a3-151">In hello previous example, hello `telemetryConfig` device twin desired and reported properties are used by hello solution back end and hello device app toosynchronize hello telemetry configuration for this device.</span></span> <span data-ttu-id="341a3-152">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="341a3-152">For example:</span></span>

1. <span data-ttu-id="341a3-153">back-end di Hello soluzione hello desiderato impostata con il valore di configurazione di hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="341a3-153">hello solution back end sets hello desired property with hello desired configuration value.</span></span> <span data-ttu-id="341a3-154">Di seguito è parte di hello del documento hello con set di proprietà hello desiderato:</span><span class="sxs-lookup"><span data-stu-id="341a3-154">Here is hello portion of hello document with hello desired property set:</span></span>
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. <span data-ttu-id="341a3-155">app per dispositivi Hello riceve una notifica di modifica hello immediatamente se è connesso, o in hello riconnettersi.</span><span class="sxs-lookup"><span data-stu-id="341a3-155">hello device app is notified of hello change immediately if connected, or at hello first reconnect.</span></span> <span data-ttu-id="341a3-156">Hello dispositivo app quindi segnala hello aggiornata configurazione (o una condizione di errore utilizzando hello `status` proprietà).</span><span class="sxs-lookup"><span data-stu-id="341a3-156">hello device app then reports hello updated configuration (or an error condition using hello `status` property).</span></span> <span data-ttu-id="341a3-157">Di seguito è parte di hello hello segnalati proprietà:</span><span class="sxs-lookup"><span data-stu-id="341a3-157">Here is hello portion of hello reported properties:</span></span>
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. <span data-ttu-id="341a3-158">back-end di Hello soluzione possibile tenere traccia hello risultati dell'operazione di configurazione hello su più dispositivi, da [l'esecuzione di query] [ lnk-query] gemelli di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="341a3-158">hello solution back end can track hello results of hello configuration operation across many devices, by [querying][lnk-query] device twins.</span></span>

> [!NOTE]
> <span data-ttu-id="341a3-159">frammenti di codice precedente Hello sono riportati esempi, ottimizzata per migliorare la leggibilità, di un modo tooencode una configurazione del dispositivo e il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="341a3-159">hello preceding snippets are examples, optimized for readability, of one way tooencode a device configuration and its status.</span></span> <span data-ttu-id="341a3-160">IoT Hub non è previsto uno schema specifico per un doppio dispositivo hello desiderato e segnalati proprietà gemelli dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="341a3-160">IoT Hub does not impose a specific schema for hello device twin desired and reported properties in hello device twins.</span></span>
> 
> 

<span data-ttu-id="341a3-161">È possibile utilizzare operazioni a esecuzione prolungata toosynchronize gemelli, ad esempio gli aggiornamenti del firmware.</span><span class="sxs-lookup"><span data-stu-id="341a3-161">You can use twins toosynchronize long-running operations such as firmware updates.</span></span> <span data-ttu-id="341a3-162">Per ulteriori informazioni su come toouse proprietà toosynchronize e tenere traccia di un'operazione a esecuzione prolungata su dispositivi, vedere [lo si desidera utilizzare i dispositivi di proprietà tooconfigure][lnk-twin-properties].</span><span class="sxs-lookup"><span data-stu-id="341a3-162">For more information on how toouse properties toosynchronize and track a long running operation across devices, see [Use desired properties tooconfigure devices][lnk-twin-properties].</span></span>

## <a name="back-end-operations"></a><span data-ttu-id="341a3-163">Operazioni di back-end</span><span class="sxs-lookup"><span data-stu-id="341a3-163">Back-end operations</span></span>
<span data-ttu-id="341a3-164">back-end di Hello soluzione opera su un doppio dispositivo hello hello dopo operazioni atomiche, esposte tramite HTTP utilizzando:</span><span class="sxs-lookup"><span data-stu-id="341a3-164">hello solution back end operates on hello device twin using hello following atomic operations, exposed through HTTP:</span></span>

1. <span data-ttu-id="341a3-165">**Recuperare un dispositivo gemello tramite ID**. Questa operazione restituisce hello doppi documento di periferica, inclusi i tag e lo si desidera, è stato segnalato e le proprietà di sistema.</span><span class="sxs-lookup"><span data-stu-id="341a3-165">**Retrieve device twin by id**. This operation returns hello device twin document, including tags and desired, reported, and system properties.</span></span>
2. <span data-ttu-id="341a3-166">**Aggiornare parzialmente il dispositivo gemello**.</span><span class="sxs-lookup"><span data-stu-id="341a3-166">**Partially update device twin**.</span></span> <span data-ttu-id="341a3-167">Questa operazione consente di tag di hello soluzione back-end toopartially aggiornamento hello o le proprietà desiderate in una coppia di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="341a3-167">This operation enables hello solution back end toopartially update hello tags or desired properties in a device twin.</span></span> <span data-ttu-id="341a3-168">aggiornamento parziale di Hello viene espresso come un documento JSON che aggiunge o aggiorna le proprietà.</span><span class="sxs-lookup"><span data-stu-id="341a3-168">hello partial update is expressed as a JSON document that adds or updates any property.</span></span> <span data-ttu-id="341a3-169">Le proprietà impostate troppo`null` vengono rimossi.</span><span class="sxs-lookup"><span data-stu-id="341a3-169">Properties set too`null` are removed.</span></span> <span data-ttu-id="341a3-170">Hello esempio seguente viene creata una nuova proprietà desiderata con valore `{"newProperty": "newValue"}`, sovrascrive hello valore esistente della `existingProperty` con `"otherNewValue"`e rimuove `otherOldProperty`.</span><span class="sxs-lookup"><span data-stu-id="341a3-170">hello following example creates a new desired property with value `{"newProperty": "newValue"}`, overwrites hello existing value of `existingProperty` with `"otherNewValue"`, and removes `otherOldProperty`.</span></span> <span data-ttu-id="341a3-171">Altre modifiche non vengono apportate proprietà tooexisting desiderato o i tag:</span><span class="sxs-lookup"><span data-stu-id="341a3-171">No other changes are made tooexisting desired properties or tags:</span></span>
   
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
3. <span data-ttu-id="341a3-172">**Sostituzione di proprietà desiderate**.</span><span class="sxs-lookup"><span data-stu-id="341a3-172">**Replace desired properties**.</span></span> <span data-ttu-id="341a3-173">Questo toocompletely di back-end operazione attiva hello soluzione sovrascrivere tutte le proprietà desiderate esistenti e sostituire un nuovo documento JSON per `properties/desired`.</span><span class="sxs-lookup"><span data-stu-id="341a3-173">This operation enables hello solution back end toocompletely overwrite all existing desired properties and substitute a new JSON document for `properties/desired`.</span></span>
4. <span data-ttu-id="341a3-174">**Sostituzione di tag**.</span><span class="sxs-lookup"><span data-stu-id="341a3-174">**Replace tags**.</span></span> <span data-ttu-id="341a3-175">Questo toocompletely di back-end operazione attiva hello soluzione sovrascrivere tutti i tag esistenti e sostituire un nuovo documento JSON per `tags`.</span><span class="sxs-lookup"><span data-stu-id="341a3-175">This operation enables hello solution back end toocompletely overwrite all existing tags and substitute a new JSON document for `tags`.</span></span>
5. <span data-ttu-id="341a3-176">**Ricezione di notifiche relative al dispositivo gemello**.</span><span class="sxs-lookup"><span data-stu-id="341a3-176">**Receive twin notifications**.</span></span> <span data-ttu-id="341a3-177">Questa operazione consente hello soluzione back-end toobe una notifica quando viene modificato un doppio hello.</span><span class="sxs-lookup"><span data-stu-id="341a3-177">This operation allows hello solution back end toobe notified when hello twin is modified.</span></span> <span data-ttu-id="341a3-178">toodo in tal caso, la soluzione IoT deve toocreate una route e tooset hello origine dati uguale troppo*twinChangeEvents*.</span><span class="sxs-lookup"><span data-stu-id="341a3-178">toodo so, your IoT solution needs toocreate a route and tooset hello Data Source equal too*twinChangeEvents*.</span></span> <span data-ttu-id="341a3-179">Per impostazione predefinita, non viene inviata alcuna notifica, ovvero queste route non sono preesistenti.</span><span class="sxs-lookup"><span data-stu-id="341a3-179">By default, no twin notifications are sent, that is, no such routes pre-exist.</span></span> <span data-ttu-id="341a3-180">Se la frequenza hello di modifica è troppo elevata o per altri motivi, ad esempio gli errori interni, hello IoT Hub potrebbe inviare solo una notifica che contiene tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="341a3-180">If hello rate of change is too high, or for other reasons, such as internal failures, hello IoT Hub might send only one notification that contains all changes.</span></span> <span data-ttu-id="341a3-181">Di conseguenza, se l'applicazione ha bisogno di controllo e registrazione affidabili di tutti gli stati intermedi, è consigliabile continuare a usare i messaggi D2C.</span><span class="sxs-lookup"><span data-stu-id="341a3-181">So, if your application needs reliable auditing and logging of all intermediate states, then it is still recommended that you use D2C messages.</span></span> <span data-ttu-id="341a3-182">messaggio di notifica doppi Hello include proprietà e corpo.</span><span class="sxs-lookup"><span data-stu-id="341a3-182">hello twin notification message includes properties, and body.</span></span>

    - <span data-ttu-id="341a3-183">Proprietà</span><span class="sxs-lookup"><span data-stu-id="341a3-183">Properties</span></span>

    | <span data-ttu-id="341a3-184">Nome</span><span class="sxs-lookup"><span data-stu-id="341a3-184">Name</span></span> | <span data-ttu-id="341a3-185">Valore</span><span class="sxs-lookup"><span data-stu-id="341a3-185">Value</span></span> |
    | --- | --- |
    <span data-ttu-id="341a3-186">$content-type</span><span class="sxs-lookup"><span data-stu-id="341a3-186">$content-type</span></span> | <span data-ttu-id="341a3-187">application/json</span><span class="sxs-lookup"><span data-stu-id="341a3-187">application/json</span></span> |
    <span data-ttu-id="341a3-188">$iothub-enqueuedtime</span><span class="sxs-lookup"><span data-stu-id="341a3-188">$iothub-enqueuedtime</span></span> |  <span data-ttu-id="341a3-189">Ora di invio notifica hello</span><span class="sxs-lookup"><span data-stu-id="341a3-189">Time when hello notification was sent</span></span> |
    <span data-ttu-id="341a3-190">$iothub-message-source</span><span class="sxs-lookup"><span data-stu-id="341a3-190">$iothub-message-source</span></span> | <span data-ttu-id="341a3-191">twinChangeEvents</span><span class="sxs-lookup"><span data-stu-id="341a3-191">twinChangeEvents</span></span> |
    <span data-ttu-id="341a3-192">$content-encoding</span><span class="sxs-lookup"><span data-stu-id="341a3-192">$content-encoding</span></span> | <span data-ttu-id="341a3-193">utf-8</span><span class="sxs-lookup"><span data-stu-id="341a3-193">utf-8</span></span> |
    <span data-ttu-id="341a3-194">deviceId</span><span class="sxs-lookup"><span data-stu-id="341a3-194">deviceId</span></span> | <span data-ttu-id="341a3-195">ID del dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="341a3-195">Id of hello device</span></span> |
    <span data-ttu-id="341a3-196">hubName</span><span class="sxs-lookup"><span data-stu-id="341a3-196">hubName</span></span> | <span data-ttu-id="341a3-197">Nome dell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="341a3-197">Name of IoT Hub</span></span> |
    <span data-ttu-id="341a3-198">operationTimestamp</span><span class="sxs-lookup"><span data-stu-id="341a3-198">operationTimestamp</span></span> | <span data-ttu-id="341a3-199">Timestamp [ISO8601] dell'operazione</span><span class="sxs-lookup"><span data-stu-id="341a3-199">[ISO8601] timestamp of operation</span></span> |
    <span data-ttu-id="341a3-200">iothub-message-schema</span><span class="sxs-lookup"><span data-stu-id="341a3-200">iothub-message-schema</span></span> | <span data-ttu-id="341a3-201">deviceLifecycleNotification</span><span class="sxs-lookup"><span data-stu-id="341a3-201">deviceLifecycleNotification</span></span> |
    <span data-ttu-id="341a3-202">opType</span><span class="sxs-lookup"><span data-stu-id="341a3-202">opType</span></span> | <span data-ttu-id="341a3-203">"replaceTwin" o "updateTwin"</span><span class="sxs-lookup"><span data-stu-id="341a3-203">"replaceTwin" or "updateTwin"</span></span> |

    <span data-ttu-id="341a3-204">Proprietà di sistema di messaggi sono precedute da hello `'$'` simbolo.</span><span class="sxs-lookup"><span data-stu-id="341a3-204">Message system properties are prefixed with hello `'$'` symbol.</span></span>

    - <span data-ttu-id="341a3-205">Corpo</span><span class="sxs-lookup"><span data-stu-id="341a3-205">Body</span></span>
        
    <span data-ttu-id="341a3-206">In questa sezione include tutte le modifiche di un doppio hello in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="341a3-206">This section includes all hello twin changes in a JSON format.</span></span> <span data-ttu-id="341a3-207">Usa hello stesso formato come una patch, con la differenza hello che può contenere tutte le sezioni di un doppio: tag, properties.reported, properties.desired e che contenga elementi hello "$metadata".</span><span class="sxs-lookup"><span data-stu-id="341a3-207">It uses hello same format as a patch, with hello difference that it can contain all twin sections: tags, properties.reported, properties.desired, and that it contains hello “$metadata” elements.</span></span> <span data-ttu-id="341a3-208">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="341a3-208">For example,</span></span>
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

<span data-ttu-id="341a3-209">Tutti hello precedente il supporto di operazioni [la concorrenza ottimistica] [ lnk-concurrency] e richiedono hello **ServiceConnect** autorizzazione, come definito in hello [sicurezza ] [ lnk-security] articolo.</span><span class="sxs-lookup"><span data-stu-id="341a3-209">All hello preceding operations support [Optimistic concurrency][lnk-concurrency] and require hello **ServiceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="341a3-210">Operazioni toothese, soluzione hello inoltre eseguire il backup finale può:</span><span class="sxs-lookup"><span data-stu-id="341a3-210">In addition toothese operations, hello solution back end can:</span></span>

* <span data-ttu-id="341a3-211">Eseguire una query utilizzando hello gemelli di hello dispositivo simile a SQL [il linguaggio di query di IoT Hub][lnk-query].</span><span class="sxs-lookup"><span data-stu-id="341a3-211">Query hello device twins using hello SQL-like [IoT Hub query language][lnk-query].</span></span>
* <span data-ttu-id="341a3-212">Eseguire operazioni su set di grandi dimensioni dei dispositivi gemelli usando i [processi][lnk-jobs].</span><span class="sxs-lookup"><span data-stu-id="341a3-212">Perform operations on large sets of device twins using [jobs][lnk-jobs].</span></span>

## <a name="device-operations"></a><span data-ttu-id="341a3-213">Operazioni del dispositivo</span><span class="sxs-lookup"><span data-stu-id="341a3-213">Device operations</span></span>
<span data-ttu-id="341a3-214">app per dispositivi Hello opera su un doppio dispositivo hello hello dopo operazioni atomiche utilizzando:</span><span class="sxs-lookup"><span data-stu-id="341a3-214">hello device app operates on hello device twin using hello following atomic operations:</span></span>

1. <span data-ttu-id="341a3-215">**Recuperare un dispositivo gemello**.</span><span class="sxs-lookup"><span data-stu-id="341a3-215">**Retrieve device twin**.</span></span> <span data-ttu-id="341a3-216">Questa operazione restituisce documento gemelli di hello dispositivo (inclusi i tag e lo si desidera, segnalati e le proprietà di sistema) per hello è attualmente connesso dispositivo.</span><span class="sxs-lookup"><span data-stu-id="341a3-216">This operation returns hello device twin document (including tags and desired, reported and system properties) for hello currently connected device.</span></span>
2. <span data-ttu-id="341a3-217">**Aggiornamento parziale delle proprietà segnalate**.</span><span class="sxs-lookup"><span data-stu-id="341a3-217">**Partially update reported properties**.</span></span> <span data-ttu-id="341a3-218">Questo consente di operazione hello aggiornamento parziale di hello segnalate le proprietà del dispositivo di hello attualmente connesso.</span><span class="sxs-lookup"><span data-stu-id="341a3-218">This operation enables hello partial update of hello reported properties of hello currently connected device.</span></span> <span data-ttu-id="341a3-219">Questo hello utilizza operazione aggiornare JSON stesso formato che hello soluzione back-end viene utilizzato per un aggiornamento parziale di proprietà desiderato.</span><span class="sxs-lookup"><span data-stu-id="341a3-219">This operation uses hello same JSON update format that hello solution back end uses for a partial update of desired properties.</span></span>
3. <span data-ttu-id="341a3-220">**Osservazione di proprietà desiderate**.</span><span class="sxs-lookup"><span data-stu-id="341a3-220">**Observe desired properties**.</span></span> <span data-ttu-id="341a3-221">dispositivo attualmente connesso Hello possibile toobe una notifica di proprietà desiderato toohello aggiornamenti quando si verificano.</span><span class="sxs-lookup"><span data-stu-id="341a3-221">hello currently connected device can choose toobe notified of updates toohello desired properties when they happen.</span></span> <span data-ttu-id="341a3-222">Hello riceve hello stessa forma di aggiornamento (sostituzione parziale o completa) eseguito da hello soluzione back-end.</span><span class="sxs-lookup"><span data-stu-id="341a3-222">hello device receives hello same form of update (partial or full replacement) executed by hello solution back end.</span></span>

<span data-ttu-id="341a3-223">Tutte le operazioni precedenti di hello richiedono hello **DeviceConnect** autorizzazione, come definito in hello [sicurezza] [ lnk-security] articolo.</span><span class="sxs-lookup"><span data-stu-id="341a3-223">All hello preceding operations require hello **DeviceConnect** permission, as defined in hello [Security][lnk-security] article.</span></span>

<span data-ttu-id="341a3-224">Hello [dispositivo IoT di Azure SDK] [ lnk-sdks] renderlo hello toouse semplice che precede le operazioni da numerosi linguaggi e piattaforme.</span><span class="sxs-lookup"><span data-stu-id="341a3-224">hello [Azure IoT device SDKs][lnk-sdks] make it easy toouse hello preceding operations from many languages and platforms.</span></span> <span data-ttu-id="341a3-225">Ulteriori informazioni sui dettagli di hello di primitive di IoT Hub per la sincronizzazione di proprietà desiderato sono reperibile [flusso riconnessione dispositivo][lnk-reconnection].</span><span class="sxs-lookup"><span data-stu-id="341a3-225">More information on hello details of IoT Hub primitives for desired properties synchronization can be found in [Device reconnection flow][lnk-reconnection].</span></span>

> [!NOTE]
> <span data-ttu-id="341a3-226">Attualmente, gemelli di dispositivo sono accessibili solo da dispositivi che si connettono tooIoT Hub utilizzando il protocollo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="341a3-226">Currently, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="341a3-227">Argomenti di riferimento:</span><span class="sxs-lookup"><span data-stu-id="341a3-227">Reference topics:</span></span>
<span data-ttu-id="341a3-228">Hello argomenti di riferimento seguenti offrono ulteriori informazioni su controllo hub IoT tooyour di accesso.</span><span class="sxs-lookup"><span data-stu-id="341a3-228">hello following reference topics provide you with more information about controlling access tooyour IoT hub.</span></span>

## <a name="tags-and-properties-format"></a><span data-ttu-id="341a3-229">Formato di tag e proprietà</span><span class="sxs-lookup"><span data-stu-id="341a3-229">Tags and properties format</span></span>
<span data-ttu-id="341a3-230">I tag, le proprietà desiderate e verrà segnalate sono oggetti JSON con hello seguenti restrizioni:</span><span class="sxs-lookup"><span data-stu-id="341a3-230">Tags, desired, and reported properties are JSON objects with hello following restrictions:</span></span>

* <span data-ttu-id="341a3-231">Tutte le chiavi negli oggetti JSON sono stringhe UTF-8 UNICODE da 64 caratteri con distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="341a3-231">All keys in JSON objects are case-sensitive 64 bytes UTF-8 UNICODE strings.</span></span> <span data-ttu-id="341a3-232">I caratteri consentiti escludono i caratteri di controllo UNICODE (segmenti C0 e C1) e `'.'`, `' '`, `'$'`.</span><span class="sxs-lookup"><span data-stu-id="341a3-232">Allowed characters exclude UNICODE control characters (segments C0 and C1), and `'.'`, `' '`, and `'$'`.</span></span>
* <span data-ttu-id="341a3-233">Tutti i valori negli oggetti JSON possono essere dei seguenti tipi di JSON hello: valore booleano, numero, stringa, oggetto.</span><span class="sxs-lookup"><span data-stu-id="341a3-233">All values in JSON objects can be of hello following JSON types: boolean, number, string, object.</span></span> <span data-ttu-id="341a3-234">Non sono consentite le matrici.</span><span class="sxs-lookup"><span data-stu-id="341a3-234">Arrays are not allowed.</span></span>
* <span data-ttu-id="341a3-235">Tutti gli oggetti JSON nei tag e nelle proprietà desiderate e segnalate possono avere una profondità massima di 5.</span><span class="sxs-lookup"><span data-stu-id="341a3-235">All JSON objects in tags, desired, and reported properties can have a maximum depth of 5.</span></span> <span data-ttu-id="341a3-236">Ad esempio, hello segue l'oggetto è valido:</span><span class="sxs-lookup"><span data-stu-id="341a3-236">For instance, hello following object is valid:</span></span>

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

* <span data-ttu-id="341a3-237">Tutti i valori di stringa possono avere una lunghezza massima di 512 byte.</span><span class="sxs-lookup"><span data-stu-id="341a3-237">All string values can be at most 512 bytes in length.</span></span>

## <a name="device-twin-size"></a><span data-ttu-id="341a3-238">Dimensioni del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="341a3-238">Device twin size</span></span>
<span data-ttu-id="341a3-239">IoT Hub impone un limite di dimensioni di 8KB valori hello di `tags`, `properties/desired`, e `properties/reported`, esclusione di elementi di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="341a3-239">IoT Hub enforces an 8KB size limitation on hello values of `tags`, `properties/desired`, and `properties/reported`, excluding read-only elements.</span></span>
<span data-ttu-id="341a3-240">Hello dimensioni vengono calcolate contando tutti i caratteri UNICODE escludendo controllano caratteri (segmenti C0 e C1) e lo spazio `' '` quando viene visualizzato di fuori di una costante di stringa.</span><span class="sxs-lookup"><span data-stu-id="341a3-240">hello size is computed by counting all characters excluding UNICODE control characters (segments C0 and C1) and space `' '` when it appears outside of a string constant.</span></span>
<span data-ttu-id="341a3-241">Rifiuta l'IoT Hub con un errore di tutte le operazioni che verrebbero aumenta hello tali documenti supera il limite di hello.</span><span class="sxs-lookup"><span data-stu-id="341a3-241">IoT Hub rejects with an error all operations that would increase hello size of those documents above hello limit.</span></span>

## <a name="device-twin-metadata"></a><span data-ttu-id="341a3-242">Metadati del dispositivo gemello</span><span class="sxs-lookup"><span data-stu-id="341a3-242">Device twin metadata</span></span>
<span data-ttu-id="341a3-243">IoT Hub conserva hello timestamp dell'ultimo aggiornamento di hello per ogni oggetto JSON in un doppio dispositivo desiderato e segnalati proprietà.</span><span class="sxs-lookup"><span data-stu-id="341a3-243">IoT Hub maintains hello timestamp of hello last update for each JSON object in device twin desired and reported properties.</span></span> <span data-ttu-id="341a3-244">Hello timestamp sono espressi in UTC e codificato nella hello [ISO8601] formato `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span><span class="sxs-lookup"><span data-stu-id="341a3-244">hello timestamps are in UTC and encoded in hello [ISO8601] format `YYYY-MM-DDTHH:MM:SS.mmmZ`.</span></span>
<span data-ttu-id="341a3-245">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="341a3-245">For example:</span></span>

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

<span data-ttu-id="341a3-246">Queste informazioni vengono conservate in ogni livello degli aggiornamenti toopreserve (foglie hello non solo di hello struttura JSON) per la rimozione di chiavi dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="341a3-246">This information is kept at every level (not just hello leaves of hello JSON structure) toopreserve updates that remove object keys.</span></span>

## <a name="optimistic-concurrency"></a><span data-ttu-id="341a3-247">Concorrenza ottimistica</span><span class="sxs-lookup"><span data-stu-id="341a3-247">Optimistic concurrency</span></span>
<span data-ttu-id="341a3-248">I tag e le proprietà desiderate e segnalate supportano la concorrenza ottimistica.</span><span class="sxs-lookup"><span data-stu-id="341a3-248">Tags, desired, and reported properties all support optimistic concurrency.</span></span>
<span data-ttu-id="341a3-249">Tag presentano un valore ETag, come per [RFC7232], che rappresenta una rappresentazione JSON del tag hello.</span><span class="sxs-lookup"><span data-stu-id="341a3-249">Tags have an ETag, as per [RFC7232], that represents hello tag's JSON representation.</span></span> <span data-ttu-id="341a3-250">È possibile utilizzare valori eTag nelle operazioni di aggiornamento condizionale da coerenza tooensure di hello soluzione back-end.</span><span class="sxs-lookup"><span data-stu-id="341a3-250">You can use ETags in conditional update operations from hello solution back end tooensure consistency.</span></span>

<span data-ttu-id="341a3-251">Doppi dispositivo desiderato e le proprietà dei report non dispone di eTag, ma hanno un `$version` valore di cui è garantita toobe incrementale.</span><span class="sxs-lookup"><span data-stu-id="341a3-251">Device twin desired and reported properties do not have ETags, but have a `$version` value that is guaranteed toobe incremental.</span></span> <span data-ttu-id="341a3-252">Analogamente tooan ETag, versione di hello possono essere usati da hello aggiornamento coerenza tooenforce parti degli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="341a3-252">Similarly tooan ETag, hello version can be used by hello updating party tooenforce consistency of updates.</span></span> <span data-ttu-id="341a3-253">Ad esempio, un'app di dispositivo per un segnalati proprietà o hello soluzione back-end per una proprietà desiderata.</span><span class="sxs-lookup"><span data-stu-id="341a3-253">For example, a device app for a reported property or hello solution back end for a desired property.</span></span>

<span data-ttu-id="341a3-254">Le versioni sono utili anche quando un agente di osservazione (ad esempio di app per dispositivi hello osservando le proprietà di hello desiderato) devono essere riconciliate race condition che tra il risultato di hello di un'operazione di recupero e di una notifica di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="341a3-254">Versions are also useful when an observing agent (such as hello device app observing hello desired properties) must reconcile races between hello result of a retrieve operation and an update notification.</span></span> <span data-ttu-id="341a3-255">Hello sezione [flusso riconnessione dispositivo] [ lnk-reconnection] vengono fornite ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="341a3-255">hello section [Device reconnection flow][lnk-reconnection] provides more information.</span></span>

## <a name="device-reconnection-flow"></a><span data-ttu-id="341a3-256">Flusso di riconnessione del dispositivo</span><span class="sxs-lookup"><span data-stu-id="341a3-256">Device reconnection flow</span></span>
<span data-ttu-id="341a3-257">L'hub IoT non conserva le notifiche di aggiornamento delle proprietà desiderate dei dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="341a3-257">IoT Hub does not preserve desired properties update notifications for disconnected devices.</span></span> <span data-ttu-id="341a3-258">Ne consegue che un dispositivo che esegue la connessione deve recuperare documento completo di proprietà desiderato hello, in aggiunta toosubscribing per le notifiche di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="341a3-258">It follows that a device that is connecting must retrieve hello full desired properties document, in addition toosubscribing for update notifications.</span></span> <span data-ttu-id="341a3-259">Dato il possibilità hello di race condition che tra le notifiche di aggiornamento e il recupero completo, è necessario garantire hello seguendo flusso:</span><span class="sxs-lookup"><span data-stu-id="341a3-259">Given hello possibility of races between update notifications and full retrieval, hello following flow must be ensured:</span></span>

1. <span data-ttu-id="341a3-260">App del dispositivo si connette tooan IoT hub.</span><span class="sxs-lookup"><span data-stu-id="341a3-260">Device app connects tooan IoT hub.</span></span>
2. <span data-ttu-id="341a3-261">L'app per dispositivo esegue la sottoscrizione per le notifiche di aggiornamento delle proprietà desiderate.</span><span class="sxs-lookup"><span data-stu-id="341a3-261">Device app subscribes for desired properties update notifications.</span></span>
3. <span data-ttu-id="341a3-262">App del dispositivo recupera documento completo di hello per le proprietà desiderate.</span><span class="sxs-lookup"><span data-stu-id="341a3-262">Device app retrieves hello full document for desired properties.</span></span>

<span data-ttu-id="341a3-263">app per dispositivi Hello è possibile ignorare tutte le notifiche con `$version` minore o uguale alla versione di hello del documento recuperato completo hello.</span><span class="sxs-lookup"><span data-stu-id="341a3-263">hello device app can ignore all notifications with `$version` less or equal than hello version of hello full retrieved document.</span></span> <span data-ttu-id="341a3-264">Questo approccio è possibile poiché l'hub IoT garantisce l'incremento delle versioni.</span><span class="sxs-lookup"><span data-stu-id="341a3-264">This approach is possible because IoT Hub guarantees that versions always increment.</span></span>

> [!NOTE]
> <span data-ttu-id="341a3-265">Questa logica è già implementata in hello [dispositivo IoT di Azure SDK][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="341a3-265">This logic is already implemented in hello [Azure IoT device SDKs][lnk-sdks].</span></span> <span data-ttu-id="341a3-266">Questa descrizione è utile solo se l'app del dispositivo hello non è possibile utilizzare uno dei dispositivi IoT di Azure SDK e devono essere programmati interfaccia MQTT hello direttamente.</span><span class="sxs-lookup"><span data-stu-id="341a3-266">This description is useful only if hello device app cannot use any of Azure IoT device SDKs and must program hello MQTT interface directly.</span></span>
> 
> 

## <a name="additional-reference-material"></a><span data-ttu-id="341a3-267">Materiale di riferimento</span><span class="sxs-lookup"><span data-stu-id="341a3-267">Additional reference material</span></span>
<span data-ttu-id="341a3-268">Altri argomenti di riferimento nella Guida per sviluppatori di IoT Hub hello includono:</span><span class="sxs-lookup"><span data-stu-id="341a3-268">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="341a3-269">Hello [gli endpoint IoT Hub] [ lnk-endpoints] hello descritti vari endpoint che espone ogni hub IoT per le operazioni in fase di esecuzione e gestione.</span><span class="sxs-lookup"><span data-stu-id="341a3-269">hello [IoT Hub endpoints][lnk-endpoints] article describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="341a3-270">Hello [la limitazione delle richieste e le quote] [ lnk-quotas] articolo descrive le quote di hello che si applicano toohello servizio IoT Hub e hello limitazione tooexpect comportamento quando si utilizza servizio hello.</span><span class="sxs-lookup"><span data-stu-id="341a3-270">hello [Throttling and quotas][lnk-quotas] article describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="341a3-271">Hello [Azure IoT dispositivo e il servizio SDK] [ lnk-sdks] articolo elenchi hello vari language SDK, è possibile utilizzare quando si sviluppano applicazioni di servizio sia sul dispositivo che interagiscono con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="341a3-271">hello [Azure IoT device and service SDKs][lnk-sdks] article lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="341a3-272">Hello [linguaggio di query IoT Hub per gemelli di dispositivo, processi e il routing dei messaggi] [ lnk-query] articolo viene descritto il linguaggio di query IoT Hub è possibile utilizzare tooretrieve informazioni dall'IoT Hub sul gemelli di dispositivo e i processi di hello .</span><span class="sxs-lookup"><span data-stu-id="341a3-272">hello [IoT Hub query language for device twins, jobs, and message routing][lnk-query] article describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="341a3-273">Hello [supporto IoT Hub MQTT] [ lnk-devguide-mqtt] vengono fornite ulteriori informazioni sul supporto di IoT Hub per protocollo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="341a3-273">hello [IoT Hub MQTT support][lnk-devguide-mqtt] article provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="341a3-274">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="341a3-274">Next steps</span></span>
<span data-ttu-id="341a3-275">Ora è imparato gemelli di dispositivo, potrebbero essere interessati hello seguenti argomenti della Guida per sviluppatori IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="341a3-275">Now you have learned about device twins, you may be interested in hello following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="341a3-276">[Richiamare un metodo diretto in un dispositivo][lnk-methods]</span><span class="sxs-lookup"><span data-stu-id="341a3-276">[Invoke a direct method on a device][lnk-methods]</span></span>
* <span data-ttu-id="341a3-277">[Pianificare processi in più dispositivi][lnk-jobs]</span><span class="sxs-lookup"><span data-stu-id="341a3-277">[Schedule jobs on multiple devices][lnk-jobs]</span></span>

<span data-ttu-id="341a3-278">Se si desidera tootry alcuni dei concetti di hello descritti in questo articolo, si potrebbero essere interessati hello seguenti esercitazioni IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="341a3-278">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorials:</span></span>

* <span data-ttu-id="341a3-279">[Come toouse hello gemelli di dispositivo][lnk-twin-tutorial]</span><span class="sxs-lookup"><span data-stu-id="341a3-279">[How toouse hello device twin][lnk-twin-tutorial]</span></span>
* <span data-ttu-id="341a3-280">[Come dispositivo toouse doppio proprietà][lnk-twin-properties]</span><span class="sxs-lookup"><span data-stu-id="341a3-280">[How toouse device twin properties][lnk-twin-properties]</span></span>

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
