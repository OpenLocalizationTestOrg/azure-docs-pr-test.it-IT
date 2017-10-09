---
title: hello aaaUnderstand linguaggio di query IoT Hub di Azure | Documenti Microsoft
description: Guida per sviluppatori - descrizione del linguaggio di query simile a SQL IoT Hub hello utilizzata tooretrieve informazioni gemelli di dispositivo e l'hub IoT dei processi.
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="b9d1a-103">Riferimento: linguaggio di query dell'hub IoT per dispositivi gemelli, processi e routing di messaggi</span><span class="sxs-lookup"><span data-stu-id="b9d1a-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="b9d1a-104">IoT Hub è un potente linguaggio simile a SQL tooretrieve relative [gemelli dispositivo] [ lnk-twins] e [processi][lnk-jobs]e [il routing dei messaggi][lnk-devguide-messaging-routes].</span><span class="sxs-lookup"><span data-stu-id="b9d1a-104">IoT Hub provides a powerful SQL-like language tooretrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="b9d1a-105">Questo articolo contiene:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-105">This article presents:</span></span>

* <span data-ttu-id="b9d1a-106">Un'introduzione toohello principali funzionalità del linguaggio di query IoT Hub, hello e</span><span class="sxs-lookup"><span data-stu-id="b9d1a-106">An introduction toohello major features of hello IoT Hub query language, and</span></span>
* <span data-ttu-id="b9d1a-107">Hello descrizione dettagliata del linguaggio hello.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-107">hello detailed description of hello language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="b9d1a-108">Introduzione alle query dei dispositivi gemelli</span><span class="sxs-lookup"><span data-stu-id="b9d1a-108">Get started with device twin queries</span></span>
<span data-ttu-id="b9d1a-109">I [dispositivi gemelli][lnk-twins] possono contenere oggetti JSON arbitrari come tag e proprietà.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="b9d1a-110">IoT Hub consente tooquery gemelli di dispositivo come un singolo documento JSON contenente tutte le informazioni di disponibilità di una copia di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-110">IoT Hub enables you tooquery device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="b9d1a-111">Supponga, ad esempio, che il gemelli di dispositivo IoT hub hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-111">Assume, for instance, that your IoT hub device twins have hello following structure:</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

<span data-ttu-id="b9d1a-112">IoT Hub espone gemelli di hello dispositivo come una raccolta di documenti denominata **dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-112">IoT Hub exposes hello device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="b9d1a-113">Pertanto hello seguente query recupera set intero di hello di gemelli di dispositivo:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-113">So hello following query retrieves hello whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="b9d1a-114">Gli [SDK dell'hub IoT][lnk-hub-sdks] supportano il paging di risultati di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="b9d1a-115">IoT Hub consente gemelli dispositivo tooretrieve filtri con condizioni arbitrarie.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-115">IoT Hub allows you tooretrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="b9d1a-116">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="b9d1a-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="b9d1a-117">Recupera hello gemelli di dispositivi con hello **location.region** tag impostato troppo**US**.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-117">retrieves hello device twins with hello **location.region** tag set too**US**.</span></span>
<span data-ttu-id="b9d1a-118">Sono supportati anche gli operatori booleani e confronti aritmetici, ad esempio</span><span class="sxs-lookup"><span data-stu-id="b9d1a-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="b9d1a-119">Recupera tutti gemelli dispositivo si trova in hello ci configurato toosend telemetria minore spesso ogni minuto.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-119">retrieves all device twins located in hello US configured toosend telemetry less often than every minute.</span></span> <span data-ttu-id="b9d1a-120">Per maggiore praticità, è anche possibile toouse costanti di matrice con hello **IN** e **/NIN** operatori (non in).</span><span class="sxs-lookup"><span data-stu-id="b9d1a-120">As a convenience, it is also possible toouse array constants with hello **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="b9d1a-121">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="b9d1a-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="b9d1a-122">recupera tutti i dispositivi gemelli che hanno segnalato una connettività WiFi o cablata.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="b9d1a-123">Si è spesso necessario tooidentify tutti gemelli di dispositivi che contengono una proprietà specifica.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-123">It is often necessary tooidentify all device twins that contain a specific property.</span></span> <span data-ttu-id="b9d1a-124">IoT Hub supporta la funzione hello `is_defined()` a questo scopo.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-124">IoT Hub supports hello function `is_defined()` for this purpose.</span></span> <span data-ttu-id="b9d1a-125">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="b9d1a-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="b9d1a-126">recuperare tutti i gemelli di dispositivo che definiscono hello `connectivity` segnalati proprietà.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-126">retrieved all device twins that define hello `connectivity` reported property.</span></span> <span data-ttu-id="b9d1a-127">Fare riferimento toohello [clausola WHERE] [ lnk-query-where] sezione per informazioni di riferimento complete hello di hello funzionalità di filtro.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-127">Refer toohello [WHERE clause][lnk-query-where] section for hello full reference of hello filtering capabilities.</span></span>

<span data-ttu-id="b9d1a-128">Sono supportati anche il raggruppamento e le aggregazioni.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="b9d1a-129">Ad esempio,</span><span class="sxs-lookup"><span data-stu-id="b9d1a-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="b9d1a-130">Restituisce il numero di hello di dispositivi hello in ogni stato di configurazione di telemetria.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-130">returns hello count of hello devices in each telemetry configuration status.</span></span>

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

<span data-ttu-id="b9d1a-131">Hello esempio precedente viene illustrata una situazione in tre dispositivi segnalati configurazione ha esito positivo, due sono comunque l'applicazione di configurazione di hello e uno ha segnalato un errore.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-131">hello preceding example illustrates a situation where three devices reported successful configuration, two are still applying hello configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="b9d1a-132">Esempio in C#</span><span class="sxs-lookup"><span data-stu-id="b9d1a-132">C# example</span></span>
<span data-ttu-id="b9d1a-133">la funzionalità di query Hello è esposto dal hello [servizio c# SDK] [ lnk-hub-sdks] in hello **RegistryManager** classe.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-133">hello query functionality is exposed by hello [C# service SDK][lnk-hub-sdks] in hello **RegistryManager** class.</span></span>
<span data-ttu-id="b9d1a-134">Ecco un esempio di una query semplice:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-134">Here is an example of a simple query:</span></span>

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

<span data-ttu-id="b9d1a-135">Si noti come hello **query** viene creata un'istanza di oggetto con una dimensione di pagina (backup too1000) e quindi più pagine possono essere recuperate tramite chiamata hello **GetNextAsTwinAsync** metodi più volte.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-135">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="b9d1a-136">Si noti che l'oggetto query hello espone più **Avanti\***, a seconda opzione deserializzazione hello necessarie hello query, ad esempio gli oggetti processo o un doppio dispositivo, o normale toobe JSON quando si utilizzano le proiezioni.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-136">Note that hello query object exposes multiple **Next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="b9d1a-137">Esempio di Node. js</span><span class="sxs-lookup"><span data-stu-id="b9d1a-137">Node.js example</span></span>
<span data-ttu-id="b9d1a-138">la funzionalità di query Hello è esposto dal hello [servizio IoT di Azure SDK per Node.js] [ lnk-hub-sdks] in hello **Registro di sistema** oggetto.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-138">hello query functionality is exposed by hello [Azure IoT service SDK for Node.js][lnk-hub-sdks] in hello **Registry** object.</span></span>
<span data-ttu-id="b9d1a-139">Ecco un esempio di una query semplice:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-139">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

<span data-ttu-id="b9d1a-140">Si noti come hello **query** viene creata un'istanza di oggetto con una dimensione di pagina (backup too1000) e quindi più pagine possono essere recuperate tramite chiamata hello **nextAsTwin** metodi più volte.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-140">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="b9d1a-141">Si noti che l'oggetto query hello espone più **Avanti\***, a seconda opzione deserializzazione hello necessarie hello query, ad esempio gli oggetti processo o un doppio dispositivo, o normale toobe JSON quando si utilizzano le proiezioni.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-141">Note that hello query object exposes multiple **next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="b9d1a-142">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="b9d1a-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b9d1a-143">Risultati della query possono contenere alcuni minuti di ritardo con i valori più recenti di toohello riguardo gemelli di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-143">Query results can have a few minutes of delay with respect toohello latest values in device twins.</span></span> <span data-ttu-id="b9d1a-144">Se la query gemelli di singoli dispositivi in base all'id, è sempre preferibile toouse hello recuperare dispositivo doppi API, che contiene i valori più recenti di hello sempre e ha limitazioni superiore.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-144">If querying individual device twins by id, it is always preferable toouse hello retrieve device twin API, which always contains hello latest values and has higher throttling limits.</span></span>

<span data-ttu-id="b9d1a-145">I confronti sono attualmente supportati solo tra tipi primitivi (non oggetti), ad esempio `... WHERE properties.desired.config = properties.reported.config` è supportato solo se tali proprietà hanno valori primitivi.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="b9d1a-146">Introduzione alle query dei processi</span><span class="sxs-lookup"><span data-stu-id="b9d1a-146">Get started with jobs queries</span></span>
<span data-ttu-id="b9d1a-147">[I processi] [ lnk-jobs] forniscono un modo tooexecute operazioni su set di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-147">[Jobs][lnk-jobs] provide a way tooexecute operations on sets of devices.</span></span> <span data-ttu-id="b9d1a-148">Ogni coppia di dispositivo contiene informazioni hello dei processi di hello di cui fa parte di una raccolta denominata di **processi**.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-148">Each device twin contains hello information of hello jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="b9d1a-149">La struttura logica è la seguente.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-149">Logically,</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

<span data-ttu-id="b9d1a-150">Questa raccolta è attualmente disponibile per query come **devices.jobs** nel linguaggio di query IoT Hub hello.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-150">Currently, this collection is queryable as **devices.jobs** in hello IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9d1a-151">Attualmente, proprietà processi hello non viene mai restituito quando si eseguono query gemelli di dispositivo (ovvero, query che contiene 'dai dispositivi').</span><span class="sxs-lookup"><span data-stu-id="b9d1a-151">Currently, hello jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="b9d1a-152">È possibile accedervi direttamente solo con le query che usano `FROM devices.jobs`.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="b9d1a-153">Ad esempio, tooget tutti i processi (ultime e pianificati) che interessano un singolo dispositivo, è possibile utilizzare hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-153">For instance, tooget all jobs (past and scheduled) that affect a single device, you can use hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="b9d1a-154">Si noti come questa query fornisce lo stato specifico del dispositivo hello (ed eventualmente risposta dirette del metodo hello) di ogni processo restituito.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-154">Note how this query provides hello device-specific status (and possibly hello direct method response) of each job returned.</span></span>
<span data-ttu-id="b9d1a-155">È inoltre possibile toofilter con condizioni Boolean arbitrarie in tutte le proprietà oggetto hello **devices.jobs** insieme.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-155">It is also possible toofilter with arbitrary Boolean conditions on all object properties in hello **devices.jobs** collection.</span></span>
<span data-ttu-id="b9d1a-156">Ad esempio, hello query riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-156">For instance, hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="b9d1a-157">recupera tutti i processi di aggiornamento del dispositivo gemello completati per il dispositivo **myDeviceId** e creati dopo settembre 2016.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="b9d1a-158">È anche risultati di ogni dispositivo hello tooretrieve possibili di un singolo processo.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-158">It is also possible tooretrieve hello per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="b9d1a-159">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="b9d1a-159">Limitations</span></span>
<span data-ttu-id="b9d1a-160">Attualmente le query su **devices.jobs** non supportano:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="b9d1a-161">Proiezioni, quindi è possibile solo `SELECT *`.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="b9d1a-162">Condizioni che fanno riferimento a un doppio dispositivo toohello nelle proprietà toojob di addizione (vedere la precedente sezione hello).</span><span class="sxs-lookup"><span data-stu-id="b9d1a-162">Conditions that refer toohello device twin in addition toojob properties (see hello preceding section).</span></span>
* <span data-ttu-id="b9d1a-163">Esecuzione di aggregazioni, ad esempio count, avg, group by.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="b9d1a-164">Introduzione a espressioni di query per route di messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="b9d1a-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="b9d1a-165">Utilizzando [route da dispositivo a cloud][lnk-devguide-messaging-routes], è possibile configurare l'IoT Hub toodispatch dispositivo a cloud messaggi endpoint toodifferent basate su espressioni valutate dai singoli messaggi.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub toodispatch device-to-cloud messages toodifferent endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="b9d1a-166">route Hello [condizione] [ lnk-query-expressions] utilizza hello stesso linguaggio di query di IoT Hub come condizioni nelle query doppi e processo.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-166">hello route [condition][lnk-query-expressions] uses hello same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="b9d1a-167">Condizioni di route vengono valutate nel corpo e intestazioni del messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-167">Route conditions are evaluated on hello message headers and body.</span></span> <span data-ttu-id="b9d1a-168">L'espressione di query routing potrebbe riguardare solo le intestazioni dei messaggi, solo corpo del messaggio hello, o entrambe le intestazioni dei messaggi e corpo del messaggio.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-168">Your routing query expression may involve only message headers, only hello message body, or both message headers and message body.</span></span> <span data-ttu-id="b9d1a-169">IoT Hub presuppone uno schema specifico per le intestazioni di hello e corpo del messaggio nei messaggi di ordine tooroute e hello le sezioni seguenti descrivono ciò che è richiesto per la route tooproperly IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-169">IoT Hub assumes a specific schema for hello headers and message body in order tooroute messages, and hello following sections describe what is required for IoT Hub tooproperly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="b9d1a-170">Routing delle intestazioni dei messaggi</span><span class="sxs-lookup"><span data-stu-id="b9d1a-170">Routing on message headers</span></span>

<span data-ttu-id="b9d1a-171">IoT Hub presuppone hello rappresentazione JSON di intestazioni di messaggio per il routing dei messaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-171">IoT Hub assumes hello following JSON representation of message headers for message routing:</span></span>

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

<span data-ttu-id="b9d1a-172">Proprietà di sistema di messaggi sono precedute da hello `'$'` simbolo.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-172">Message system properties are prefixed with hello `'$'` symbol.</span></span>
<span data-ttu-id="b9d1a-173">Alle proprietà utente si accede sempre con il relativo nome.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="b9d1a-174">Se il nome di una proprietà utente avviene toocoincide con una proprietà di sistema (ad esempio `$to`), proprietà utente hello verrà recuperato con hello `$to` espressione.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-174">If a user property name happens toocoincide with a system property (such as `$to`), hello user property will be retrieved with hello `$to` expression.</span></span>
<span data-ttu-id="b9d1a-175">È sempre possibile accedere a proprietà di sistema hello utilizzando le parentesi `{}`: ad esempio, è possibile utilizzare l'espressione hello `{$to}` tooaccess hello proprietà di sistema `to`.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-175">You can always access hello system property using brackets `{}`: for instance, you can use hello expression `{$to}` tooaccess hello system property `to`.</span></span> <span data-ttu-id="b9d1a-176">I nomi di proprietà tra parentesi quadre recuperano sempre la proprietà di sistema corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-176">Bracketed property names always retrieve hello corresponding system property.</span></span>

<span data-ttu-id="b9d1a-177">Si ricordi che nei nomi delle proprietà viene fatta distinzione tra maiuscole e minuscole.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="b9d1a-178">Tutte le proprietà dei messaggi sono stringhe.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-178">All message properties are strings.</span></span> <span data-ttu-id="b9d1a-179">Proprietà di sistema, come descritto in hello [Guida per sviluppatori][lnk-devguide-messaging-format], non sono attualmente disponibili toouse nelle query.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-179">System properties, as described in hello [developer guide][lnk-devguide-messaging-format], are currently not available toouse in queries.</span></span>
>

<span data-ttu-id="b9d1a-180">Ad esempio, se si utilizza un `messageType` proprietà, è possibile tooroute endpoint di tooone tutti i dati di telemetria ed endpoint di tooanother tutti gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-180">For example, if you use a `messageType` property, you might want tooroute all telemetry tooone endpoint, and all alerts tooanother endpoint.</span></span> <span data-ttu-id="b9d1a-181">È possibile scrivere hello telemetria di hello tooroute espressione seguente:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-181">You can write hello following expression tooroute hello telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="b9d1a-182">E hello seguendo i messaggi di avviso hello tooroute espressione:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-182">And hello following expression tooroute hello alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="b9d1a-183">Sono supportate anche le espressioni e le funzione booleane.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="b9d1a-184">Questa funzionalità consente toodistinguish tra il livello di gravità, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-184">This feature enables you toodistinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="b9d1a-185">Fare riferimento toohello [espressione e le condizioni] [ lnk-query-expressions] sezione per l'elenco completo di hello di funzioni e operatori supportati.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-185">Refer toohello [Expression and conditions][lnk-query-expressions] section for hello full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="b9d1a-186">Routing del corpo dei messaggi</span><span class="sxs-lookup"><span data-stu-id="b9d1a-186">Routing on message bodies</span></span>

<span data-ttu-id="b9d1a-187">IoT Hub è possibile instradare solo in base a corpo del messaggio contenuto se il corpo del messaggio hello viene correttamente formato JSON con codificata UTF-8, UTF-16 o UTF-32.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-187">IoT Hub can only route based on message body contents if hello message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="b9d1a-188">È necessario impostare tipo di contenuto del messaggio hello hello troppo`application/json` e hello tooone codifica del contenuto di hello supportate codifiche UTF in tooallow intestazioni di messaggio hello messaggio hello di IoT Hub tooroute basato sul contenuto del corpo hello.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-188">You must set hello content type of hello message too`application/json` and hello content encoding tooone of hello supported UTF encodings in hello message headers tooallow IoT Hub tooroute hello message based on hello body contents.</span></span> <span data-ttu-id="b9d1a-189">Se una delle intestazioni di hello viene omesso, l'IoT Hub non tenterà tooevaluate qualsiasi espressione di query che include il corpo di hello rispetto al messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-189">If either of hello headers is not specified, IoT Hub will not attempt tooevaluate any query expression involving hello body against hello message.</span></span> <span data-ttu-id="b9d1a-190">Se il messaggio non è un messaggio JSON, o se il messaggio hello non specifica il tipo di contenuto hello e la codifica del contenuto, è comunque possibile usare il messaggio hello tooroute in base alle intestazioni di messaggio hello di routing dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-190">If your message is not a JSON message, or if hello message does not specify hello content type and content encoding, you may still use message routing tooroute hello message based on hello message headers.</span></span>

<span data-ttu-id="b9d1a-191">È possibile utilizzare `$body` nel messaggio hello di hello query espressione tooroute.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-191">You can use `$body` in hello query expression tooroute hello message.</span></span> <span data-ttu-id="b9d1a-192">È possibile utilizzare un riferimento semplice corpo, riferimento a una matrice corpo o più riferimenti corpo nell'espressione di query hello.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-192">You can use a simple body reference, body array reference, or multiple body references in hello query expression.</span></span> <span data-ttu-id="b9d1a-193">L'espressione di query può anche combinare un riferimento al corpo con un riferimento all'intestazione del messaggio.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="b9d1a-194">Ad esempio, di seguito hello sono tutte le espressioni di query valida:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-194">For example, hello following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="b9d1a-195">Nozioni di base di una query dell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="b9d1a-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="b9d1a-196">Ogni query dell'hub IoT è costituita da una clausola SELECT e da una clausola FROM e dalle clausole facoltative WHERE e GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="b9d1a-197">Ogni query viene eseguita su una raccolta di documenti JSON, ad esempio dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="b9d1a-198">clausola FROM Hello indica hello documento raccolta toobe iterato su (**dispositivi** o **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="b9d1a-198">hello FROM clause indicates hello document collection toobe iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="b9d1a-199">Quindi, hello filtro hello dove clausola viene applicata.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-199">Then, hello filter in hello WHERE clause is applied.</span></span> <span data-ttu-id="b9d1a-200">Con le aggregazioni, vengono raggruppati i risultati di hello di questo passaggio come hello specificato nella clausola GROUP BY e, per ogni gruppo, viene generata una riga come specificato nella clausola SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-200">With aggregations, hello results of this step are grouped as specified in hello GROUP BY clause and, for each group, a row is generated as specified in hello SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="b9d1a-201">Clausola FROM</span><span class="sxs-lookup"><span data-stu-id="b9d1a-201">FROM clause</span></span>
<span data-ttu-id="b9d1a-202">Hello **da < from_specification >** clausola può assumere solo due valori: **dai dispositivi**, gemelli dispositivo tooquery, o **da devices.jobs**, processo tooquery per dispositivo informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-202">hello **FROM <from_specification>** clause can assume only two values: **FROM devices**, tooquery device twins, or **FROM devices.jobs**, tooquery job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="b9d1a-203">Clausola WHERE</span><span class="sxs-lookup"><span data-stu-id="b9d1a-203">WHERE clause</span></span>
<span data-ttu-id="b9d1a-204">Hello **dove < filter_condition >** clausola è facoltativa.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-204">hello **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="b9d1a-205">Specifica una o più condizioni che documenti JSON hello nella raccolta di hello FROM devono soddisfare toobe incluso come parte del risultato hello.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-205">It specifies one or more conditions that hello JSON documents in hello FROM collection must satisfy toobe included as part of hello result.</span></span> <span data-ttu-id="b9d1a-206">Deve restituire un documento JSON hello specificato condizioni troppo "true" toobe inclusa nel risultato hello.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-206">Any JSON document must evaluate hello specified conditions too"true" toobe included in hello result.</span></span>

<span data-ttu-id="b9d1a-207">Hello consentito condizioni sono descritte nella sezione [espressioni e condizioni][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="b9d1a-207">hello allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="b9d1a-208">Clausola SELECT</span><span class="sxs-lookup"><span data-stu-id="b9d1a-208">SELECT clause</span></span>
<span data-ttu-id="b9d1a-209">clausola SELECT Hello (**selezionare < select_list >**) è obbligatorio e specifica quali valori vengono recuperati dalla query hello.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-209">hello SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from hello query.</span></span> <span data-ttu-id="b9d1a-210">Specifica hello JSON valori toobe utilizzato toogenerate di nuovi oggetti JSON.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-210">It specifies hello JSON values toobe used toogenerate new JSON objects.</span></span>
<span data-ttu-id="b9d1a-211">Per ogni elemento di hello subset filtrato (e facoltativamente raggruppati) della raccolta da hello, la fase di proiezione hello genera un nuovo oggetto JSON, costruito con i valori hello specificati nella clausola SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-211">For each element of hello filtered (and optionally grouped) subset of hello FROM collection, hello projection phase generates a new JSON object, constructed with hello values specified in hello SELECT clause.</span></span>

<span data-ttu-id="b9d1a-212">Di seguito è grammatica hello della clausola SELECT hello:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-212">Following is hello grammar of hello SELECT clause:</span></span>

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

<span data-ttu-id="b9d1a-213">dove **attribute_name** fa riferimento la proprietà tooany del documento JSON hello nella raccolta di hello FROM.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-213">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span> <span data-ttu-id="b9d1a-214">Alcuni esempi di clausole SELECT sono reperibile in hello [Guida introduttiva a query doppi dispositivo] [ lnk-query-getstarted] sezione.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-214">Some examples of SELECT clauses can be found in hello [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="b9d1a-215">Attualmente le clausole di selezione diverse da **SELECT \*** sono supportate solo nelle query aggregate sui dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="b9d1a-216">Clausola GROUP BY</span><span class="sxs-lookup"><span data-stu-id="b9d1a-216">GROUP BY clause</span></span>
<span data-ttu-id="b9d1a-217">Hello **GROUP BY < group_specification >** clausola è un passaggio facoltativo che può essere eseguito dopo il filtro hello specificato in hello clausola WHERE e prima di proiezione hello specificata in hello Seleziona.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-217">hello **GROUP BY <group_specification>** clause is an optional step that can be executed after hello filter specified in hello WHERE clause, and before hello projection specified in hello SELECT.</span></span> <span data-ttu-id="b9d1a-218">Raggruppa documenti in base al valore di hello di un attributo.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-218">It groups documents based on hello value of an attribute.</span></span> <span data-ttu-id="b9d1a-219">Questi gruppi vengono utilizzati toogenerate aggregati i valori come specificato nella clausola SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-219">These groups are used toogenerate aggregated values as specified in hello SELECT clause.</span></span>

<span data-ttu-id="b9d1a-220">Ecco un esempio di query che usa GROUP BY:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="b9d1a-221">Hello formali sintassi GROUP BY è:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-221">hello formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="b9d1a-222">dove **attribute_name** fa riferimento la proprietà tooany del documento JSON hello nella raccolta di hello FROM.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-222">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span>

<span data-ttu-id="b9d1a-223">Clausola GROUP BY hello è attualmente supportata solo quando si eseguono query gemelli di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-223">Currently, hello GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="b9d1a-224">Espressioni e condizioni</span><span class="sxs-lookup"><span data-stu-id="b9d1a-224">Expressions and conditions</span></span>
<span data-ttu-id="b9d1a-225">In generale, un'*espressione*:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="b9d1a-226">Restituisce l'istanza di tooan di un tipo JSON (ad esempio, valore booleano, numero, stringa, matrice o oggetto), e</span><span class="sxs-lookup"><span data-stu-id="b9d1a-226">Evaluates tooan instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="b9d1a-227">Viene definito mediante la modifica di dati provenienti dal documento JSON di dispositivo hello e costanti utilizzando le funzioni e operatori incorporati.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-227">Is defined by manipulating data coming from hello device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="b9d1a-228">*Condizioni* sono espressioni che restituiscono tooa valore booleano.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-228">*Conditions* are expressions that evaluate tooa Boolean.</span></span> <span data-ttu-id="b9d1a-229">Una costante diversa da un valore booleano **true** viene considerato come **false** (inclusi **null**, **definito**, qualsiasi istanza di oggetto o una matrice, qualsiasi stringa e chiaramente hello booleano **false**).</span><span class="sxs-lookup"><span data-stu-id="b9d1a-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly hello Boolean **false**).</span></span>

<span data-ttu-id="b9d1a-230">sintassi di Hello per le espressioni è:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-230">hello syntax for expressions is:</span></span>

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

<span data-ttu-id="b9d1a-231">dove:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-231">where:</span></span>

| <span data-ttu-id="b9d1a-232">Simbolo</span><span class="sxs-lookup"><span data-stu-id="b9d1a-232">Symbol</span></span> | <span data-ttu-id="b9d1a-233">Definizione</span><span class="sxs-lookup"><span data-stu-id="b9d1a-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="b9d1a-234">attribute_name</span><span class="sxs-lookup"><span data-stu-id="b9d1a-234">attribute_name</span></span> | <span data-ttu-id="b9d1a-235">Qualsiasi proprietà del documento JSON hello in hello **FROM** insieme.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-235">Any property of hello JSON document in hello **FROM** collection.</span></span> |
| <span data-ttu-id="b9d1a-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="b9d1a-236">binary_operator</span></span> | <span data-ttu-id="b9d1a-237">Qualsiasi operatore binario elencati in hello [operatori](#operators) sezione.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-237">Any binary operator listed in hello [Operators](#operators) section.</span></span> |
| <span data-ttu-id="b9d1a-238">function_name</span><span class="sxs-lookup"><span data-stu-id="b9d1a-238">function_name</span></span>| <span data-ttu-id="b9d1a-239">Qualsiasi funzione elencata in hello [funzioni](#functions) sezione.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-239">Any function listed in hello [Functions](#functions) section.</span></span> |
| <span data-ttu-id="b9d1a-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="b9d1a-240">decimal_literal</span></span> |<span data-ttu-id="b9d1a-241">Float espresso in una notazione decimale.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="b9d1a-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="b9d1a-242">hexadecimal_literal</span></span> |<span data-ttu-id="b9d1a-243">Un numero espresso dalla stringa hello "0x" seguito da una stringa di cifre esadecimali.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-243">A number expressed by hello string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="b9d1a-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="b9d1a-244">string_literal</span></span> |<span data-ttu-id="b9d1a-245">I valori letterali stringa sono stringhe Unicode rappresentate da una sequenza di zero o più caratteri Unicode o sequenze di escape.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="b9d1a-246">I valori letterali stringa sono racchiusi tra virgolette singole (apostrofo: ') o virgolette doppie (virgolette inglesi: ").</span><span class="sxs-lookup"><span data-stu-id="b9d1a-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="b9d1a-247">Caratteri di escape consentiti: `\'`, `\"`, `\\`, `\uXXXX` per i caratteri Unicode definiti da 4 cifre esadecimali.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="b9d1a-248">Operatori</span><span class="sxs-lookup"><span data-stu-id="b9d1a-248">Operators</span></span>
<span data-ttu-id="b9d1a-249">Hello dopo gli operatori è supportato:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-249">hello following operators are supported:</span></span>

| <span data-ttu-id="b9d1a-250">Famiglia</span><span class="sxs-lookup"><span data-stu-id="b9d1a-250">Family</span></span> | <span data-ttu-id="b9d1a-251">Operatori</span><span class="sxs-lookup"><span data-stu-id="b9d1a-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="b9d1a-252">Aritmetico</span><span class="sxs-lookup"><span data-stu-id="b9d1a-252">Arithmetic</span></span> |<span data-ttu-id="b9d1a-253">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="b9d1a-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="b9d1a-254">Logico</span><span class="sxs-lookup"><span data-stu-id="b9d1a-254">Logical</span></span> |<span data-ttu-id="b9d1a-255">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="b9d1a-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="b9d1a-256">Confronto</span><span class="sxs-lookup"><span data-stu-id="b9d1a-256">Comparison</span></span> |<span data-ttu-id="b9d1a-257">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="b9d1a-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="b9d1a-258">Funzioni</span><span class="sxs-lookup"><span data-stu-id="b9d1a-258">Functions</span></span>
<span data-ttu-id="b9d1a-259">Quando si eseguono query gemelli e processi hello è supportato solo funzione è:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-259">When querying twins and jobs hello only supported function is:</span></span>

| <span data-ttu-id="b9d1a-260">Funzione</span><span class="sxs-lookup"><span data-stu-id="b9d1a-260">Function</span></span> | <span data-ttu-id="b9d1a-261">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b9d1a-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="b9d1a-262">IS_DEFINED(proprietà)</span><span class="sxs-lookup"><span data-stu-id="b9d1a-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="b9d1a-263">Restituisce un valore booleano che indica se è stato assegnato un valore di proprietà hello (inclusi `null`).</span><span class="sxs-lookup"><span data-stu-id="b9d1a-263">Returns a Boolean indicating if hello property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="b9d1a-264">In condizioni di route, hello funzioni matematiche seguenti è supportato:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-264">In routes conditions, hello following math functions are supported:</span></span>

| <span data-ttu-id="b9d1a-265">Funzione</span><span class="sxs-lookup"><span data-stu-id="b9d1a-265">Function</span></span> | <span data-ttu-id="b9d1a-266">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b9d1a-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="b9d1a-267">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="b9d1a-267">ABS(x)</span></span> | <span data-ttu-id="b9d1a-268">Restituisce hello assoluto (positivo) il valore di hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-268">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| <span data-ttu-id="b9d1a-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="b9d1a-269">EXP(x)</span></span> | <span data-ttu-id="b9d1a-270">Hello restituisce il valore esponenziale di hello specificato espressione numerica (e ^ x).</span><span class="sxs-lookup"><span data-stu-id="b9d1a-270">Returns hello exponential value of hello specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="b9d1a-271">POWER(x,y)</span><span class="sxs-lookup"><span data-stu-id="b9d1a-271">POWER(x,y)</span></span> | <span data-ttu-id="b9d1a-272">Valore di hello specificato di hello restituisce espressione toohello potenza specificata (x ^ y).</span><span class="sxs-lookup"><span data-stu-id="b9d1a-272">Returns hello value of hello specified expression toohello specified power (x^y).</span></span>|
| <span data-ttu-id="b9d1a-273">SQUARE(x)</span><span class="sxs-lookup"><span data-stu-id="b9d1a-273">SQUARE(x)</span></span> | <span data-ttu-id="b9d1a-274">Hello restituisce quadrato di hello specificato valore numerico.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-274">Returns hello square of hello specified numeric value.</span></span> |
| <span data-ttu-id="b9d1a-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="b9d1a-275">CEILING(x)</span></span> | <span data-ttu-id="b9d1a-276">Restituisce hello più piccolo valore integer maggiore di o uguale a, hello espressione numerica specificata.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-276">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| <span data-ttu-id="b9d1a-277">FLOOR(x)</span><span class="sxs-lookup"><span data-stu-id="b9d1a-277">FLOOR(x)</span></span> | <span data-ttu-id="b9d1a-278">Restituisce l'intero più grande hello minore o uguale toohello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-278">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| <span data-ttu-id="b9d1a-279">SIGN(x)</span><span class="sxs-lookup"><span data-stu-id="b9d1a-279">SIGN(x)</span></span> | <span data-ttu-id="b9d1a-280">Restituisce hello positivo (+ 1), zero (0) o negativo (-1) segno di hello specificato espressione numerica.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-280">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>|
| <span data-ttu-id="b9d1a-281">SQRT(x)</span><span class="sxs-lookup"><span data-stu-id="b9d1a-281">SQRT(x)</span></span> | <span data-ttu-id="b9d1a-282">Hello restituisce quadrato di hello specificato valore numerico.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-282">Returns hello square of hello specified numeric value.</span></span> |

<span data-ttu-id="b9d1a-283">In condizioni di route, hello dopo il tipo di controllo e le funzioni cast è supportato:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-283">In routes conditions, hello following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="b9d1a-284">Funzione</span><span class="sxs-lookup"><span data-stu-id="b9d1a-284">Function</span></span> | <span data-ttu-id="b9d1a-285">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b9d1a-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="b9d1a-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="b9d1a-286">AS_NUMBER</span></span> | <span data-ttu-id="b9d1a-287">Converte hello stringa di input tooa numero.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-287">Converts hello input string tooa number.</span></span> <span data-ttu-id="b9d1a-288">`noop` se l'input è un numero, `Undefined` se la stringa non rappresenta un numero.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="b9d1a-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="b9d1a-289">IS_ARRAY</span></span> | <span data-ttu-id="b9d1a-290">Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è una matrice.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-290">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span> |
| <span data-ttu-id="b9d1a-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="b9d1a-291">IS_BOOL</span></span> | <span data-ttu-id="b9d1a-292">Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è un valore booleano.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-292">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span> |
| <span data-ttu-id="b9d1a-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="b9d1a-293">IS_DEFINED</span></span> | <span data-ttu-id="b9d1a-294">Restituisce un valore booleano che indica se la proprietà hello è stata assegnata un valore.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-294">Returns a Boolean indicating if hello property has been assigned a value.</span></span> |
| <span data-ttu-id="b9d1a-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="b9d1a-295">IS_NULL</span></span> | <span data-ttu-id="b9d1a-296">Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è null.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-296">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span> |
| <span data-ttu-id="b9d1a-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="b9d1a-297">IS_NUMBER</span></span> | <span data-ttu-id="b9d1a-298">Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è un numero.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-298">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span> |
| <span data-ttu-id="b9d1a-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="b9d1a-299">IS_OBJECT</span></span> | <span data-ttu-id="b9d1a-300">Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è un oggetto JSON.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-300">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span> |
| <span data-ttu-id="b9d1a-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="b9d1a-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="b9d1a-302">Restituisce un valore booleano che indica se il tipo di hello di hello specificato espressione è una primitiva (stringa, booleano, numerico o `null`).</span><span class="sxs-lookup"><span data-stu-id="b9d1a-302">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="b9d1a-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="b9d1a-303">IS_STRING</span></span> | <span data-ttu-id="b9d1a-304">Restituisce un valore booleano che indica se il tipo di hello di hello l'espressione specificata è una stringa.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-304">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span> |

<span data-ttu-id="b9d1a-305">In condizioni di route, hello funzioni stringa seguenti è supportato:</span><span class="sxs-lookup"><span data-stu-id="b9d1a-305">In routes conditions, hello following string functions are supported:</span></span>

| <span data-ttu-id="b9d1a-306">Funzione</span><span class="sxs-lookup"><span data-stu-id="b9d1a-306">Function</span></span> | <span data-ttu-id="b9d1a-307">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b9d1a-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="b9d1a-308">CONCAT(x, …)</span><span class="sxs-lookup"><span data-stu-id="b9d1a-308">CONCAT(x, …)</span></span> | <span data-ttu-id="b9d1a-309">Restituisce una stringa che rappresenta il risultato di hello del concatenamento di due o più valori di stringa.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-309">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="b9d1a-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="b9d1a-310">LENGTH(x)</span></span> | <span data-ttu-id="b9d1a-311">Restituisce il numero di caratteri di hello hello specificato espressione stringa.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-311">Returns hello number of characters of hello specified string expression.</span></span>|
| <span data-ttu-id="b9d1a-312">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="b9d1a-312">LOWER(x)</span></span> | <span data-ttu-id="b9d1a-313">Restituisce un'espressione stringa dopo aver convertito i caratteri maiuscoli in caratteri toolowercase di dati.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-313">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| <span data-ttu-id="b9d1a-314">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="b9d1a-314">UPPER(x)</span></span> | <span data-ttu-id="b9d1a-315">Restituisce un'espressione stringa dopo la conversione toouppercase di dati carattere minuscolo.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-315">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| <span data-ttu-id="b9d1a-316">SUBSTRING (stringa, avvio [, lunghezza])</span><span class="sxs-lookup"><span data-stu-id="b9d1a-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="b9d1a-317">Restituisce parte di un'espressione stringa a partire da hello posizione in base zero del carattere specificata e continua toohello specificato, lunghezza o alla fine di toohello della stringa hello.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-317">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span> |
| <span data-ttu-id="b9d1a-318">INDEX_OF(stringa, frammento)</span><span class="sxs-lookup"><span data-stu-id="b9d1a-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="b9d1a-319">Restituisce hello a partire dalla posizione della prima occorrenza di hello della seconda espressione stringa hello all'hello prima espressione stringa specificata oppure -1 se la stringa hello non viene trovata.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-319">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>|
| <span data-ttu-id="b9d1a-320">STARTS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="b9d1a-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="b9d1a-321">Restituisce un valore booleano che indica se prima espressione di stringa hello inizia con hello secondo.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-321">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span> |
| <span data-ttu-id="b9d1a-322">ENDS_WITH(x, y)</span><span class="sxs-lookup"><span data-stu-id="b9d1a-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="b9d1a-323">Restituisce un valore booleano che indica se prima espressione di stringa hello termina con hello secondo.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-323">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span> |
| <span data-ttu-id="b9d1a-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="b9d1a-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="b9d1a-325">Restituisce un valore booleano che indica se prima espressione di stringa hello contiene hello secondo.</span><span class="sxs-lookup"><span data-stu-id="b9d1a-325">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b9d1a-326">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b9d1a-326">Next steps</span></span>
<span data-ttu-id="b9d1a-327">Informazioni su come viene eseguita una query tooexecute nelle App usando [Azure IoT SDK][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="b9d1a-327">Learn how tooexecute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
