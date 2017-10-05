---
title: Modello di dati di Azure Application Insights | Microsoft Docs
description: "Descrive le proprietà esportate da esportazione continua in JSON e usate come filtri."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: cabad41c-0518-4669-887f-3087aef865ea
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: bwren
ms.openlocfilehash: a485ddd555f65473d81896effc4a3562bda71410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-export-data-model"></a><span data-ttu-id="31c02-103">Modello di dati di esportazione di Application Insights</span><span class="sxs-lookup"><span data-stu-id="31c02-103">Application Insights Export Data Model</span></span>
<span data-ttu-id="31c02-104">Questa tabella elenca le proprietà di telemetria inviate al portale dagli SDK di [Application Insights](app-insights-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="31c02-104">This table lists the properties of telemetry sent from the [Application Insights](app-insights-overview.md) SDKs to the portal.</span></span>
<span data-ttu-id="31c02-105">Queste proprietà saranno visualizzate nell'output dei dati di [Esportazione continua](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="31c02-105">You'll see these properties in data output from [Continuous Export](app-insights-export-telemetry.md).</span></span>
<span data-ttu-id="31c02-106">Sono visibili anche nei filtri delle proprietà in [Esplora metriche](app-insights-metrics-explorer.md) e [Ricerca diagnostica](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="31c02-106">They also appear in property filters in [Metric Explorer](app-insights-metrics-explorer.md) and [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="31c02-107">Punti da notare:</span><span class="sxs-lookup"><span data-stu-id="31c02-107">Points to note:</span></span>

* <span data-ttu-id="31c02-108">`[0]` in queste tabelle indica un punto nel percorso in cui è necessario inserire un indice, ma non è sempre 0.</span><span class="sxs-lookup"><span data-stu-id="31c02-108">`[0]` in these tables denotes a point in the path where you have to insert an index; but it isn't always 0.</span></span>
* <span data-ttu-id="31c02-109">Le durate sono espresse in decimi di microsecondo, quindi 10000000 == 1 secondo.</span><span class="sxs-lookup"><span data-stu-id="31c02-109">Time durations are in tenths of a microsecond, so 10000000 == 1 second.</span></span>
* <span data-ttu-id="31c02-110">Date e ore sono in formato UTC e vengono specificate nel formato ISO `yyyy-MM-DDThh:mm:ss.sssZ`</span><span class="sxs-lookup"><span data-stu-id="31c02-110">Dates and times are UTC, and are given in the ISO format `yyyy-MM-DDThh:mm:ss.sssZ`</span></span>


## <a name="example"></a><span data-ttu-id="31c02-111">Esempio</span><span class="sxs-lookup"><span data-stu-id="31c02-111">Example</span></span>
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent to client
        "success": true, // Default == responseCode<400
        // Request id becomes the operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently the following fields are redundant:
          "count": 1.0,
          "min": 1046804.0,
          "max": 1046804.0,
          "stdDev": 0.0,
          "sampledValue": 1046804.0
        },
        "url": "/"
      }
    ],
    "internal": {
      "data": {
        "id": "7f156650-ef4c-11e5-8453-3f984b167d05",
        "documentVersion": "1.61"
      }
    },
    "context": {
      "device": { // client browser
        "type": "PC",
        "screenResolution": { },
        "roleInstance": "WFWEB14B.fabrikam.net"
      },
      "application": { },
      "location": { // derived from client ip
        "continent": "North America",
        "country": "United States",
        // last octagon is anonymized to 0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent to portal:
        "samplingRate": 100.0,
        "eventTime": "2016-03-21T10:05:45.7334717Z" // UTC
      },
      "user": {
        "isAuthenticated": false,
        "anonId": "us-tx-sn1-azr", // bot agent id
        "anonAcquisitionDate": "0001-01-01T00:00:00Z",
        "authAcquisitionDate": "0001-01-01T00:00:00Z",
        "accountAcquisitionDate": "0001-01-01T00:00:00Z"
      },
      "operation": {
        "id": "fCOhCdCnZ9I=",
        "parentId": "fCOhCdCnZ9I=",
        "name": "GET Home/Index"
      },
      "cloud": { },
      "serverDevice": { },
      "custom": { // set by custom fields of track calls
        "dimensions": [ ],
        "metrics": [ ]
      },
      "session": {
        "id": "65504c10-44a6-489e-b9dc-94184eb00d86",
        "isFirst": true
      }
    }
  <span data-ttu-id="31c02-112">}</span><span class="sxs-lookup"><span data-stu-id="31c02-112">}</span></span>

## <a name="context"></a><span data-ttu-id="31c02-113">Context</span><span class="sxs-lookup"><span data-stu-id="31c02-113">Context</span></span>
<span data-ttu-id="31c02-114">Tutti i tipi di telemetria sono accompagnati da una sezione di contesto.</span><span class="sxs-lookup"><span data-stu-id="31c02-114">All types of telemetry are accompanied by a context section.</span></span> <span data-ttu-id="31c02-115">Non tutti questi campi vengono trasmessi con ogni punto dati.</span><span class="sxs-lookup"><span data-stu-id="31c02-115">Not all of these fields are transmitted with every data point.</span></span>

| <span data-ttu-id="31c02-116">Path</span><span class="sxs-lookup"><span data-stu-id="31c02-116">Path</span></span> | <span data-ttu-id="31c02-117">Tipo</span><span class="sxs-lookup"><span data-stu-id="31c02-117">Type</span></span> | <span data-ttu-id="31c02-118">Note</span><span class="sxs-lookup"><span data-stu-id="31c02-118">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31c02-119">context.custom.dimensions [0]</span><span class="sxs-lookup"><span data-stu-id="31c02-119">context.custom.dimensions [0]</span></span> |<span data-ttu-id="31c02-120">oggetto [ ]</span><span class="sxs-lookup"><span data-stu-id="31c02-120">object [ ]</span></span> |<span data-ttu-id="31c02-121">Coppie di stringhe chiave-valore impostate dal parametro delle proprietà personalizzate.</span><span class="sxs-lookup"><span data-stu-id="31c02-121">Key-value string pairs set by custom properties parameter.</span></span> <span data-ttu-id="31c02-122">La lunghezza massima delle chiavi 100, la lunghezza massima dei valori è 1024.</span><span class="sxs-lookup"><span data-stu-id="31c02-122">Key max length 100, values max length 1024.</span></span> <span data-ttu-id="31c02-123">Più di 100 valori univoci. La proprietà può essere cercata, ma non può essere usata per la segmentazione.</span><span class="sxs-lookup"><span data-stu-id="31c02-123">More than 100 unique values, the property can be searched but cannot be used for segmentation.</span></span> <span data-ttu-id="31c02-124">Massimo 200 chiavi per ikey.</span><span class="sxs-lookup"><span data-stu-id="31c02-124">Max 200 keys per ikey.</span></span> |
| <span data-ttu-id="31c02-125">context.custom.metrics [0]</span><span class="sxs-lookup"><span data-stu-id="31c02-125">context.custom.metrics [0]</span></span> |<span data-ttu-id="31c02-126">oggetto [ ]</span><span class="sxs-lookup"><span data-stu-id="31c02-126">object [ ]</span></span> |<span data-ttu-id="31c02-127">Coppie di chiave-valore impostate dai parametri delle misurazioni personalizzate e da TrackMetrics.</span><span class="sxs-lookup"><span data-stu-id="31c02-127">Key-value pairs set by custom measurements parameter and by TrackMetrics.</span></span> <span data-ttu-id="31c02-128">La lunghezza massima delle chiavi 100, i valori possono essere numerici.</span><span class="sxs-lookup"><span data-stu-id="31c02-128">Key max length 100, values may be numeric.</span></span> |
| <span data-ttu-id="31c02-129">context.data.eventTime</span><span class="sxs-lookup"><span data-stu-id="31c02-129">context.data.eventTime</span></span> |<span data-ttu-id="31c02-130">string</span><span class="sxs-lookup"><span data-stu-id="31c02-130">string</span></span> |<span data-ttu-id="31c02-131">UTC</span><span class="sxs-lookup"><span data-stu-id="31c02-131">UTC</span></span> |
| <span data-ttu-id="31c02-132">context.data.isSynthetic</span><span class="sxs-lookup"><span data-stu-id="31c02-132">context.data.isSynthetic</span></span> |<span data-ttu-id="31c02-133">boolean</span><span class="sxs-lookup"><span data-stu-id="31c02-133">boolean</span></span> |<span data-ttu-id="31c02-134">La richiesta proviene da un robot o un test Web.</span><span class="sxs-lookup"><span data-stu-id="31c02-134">Request appears to come from a bot or web test.</span></span> |
| <span data-ttu-id="31c02-135">context.data.samplingRate</span><span class="sxs-lookup"><span data-stu-id="31c02-135">context.data.samplingRate</span></span> |<span data-ttu-id="31c02-136">number</span><span class="sxs-lookup"><span data-stu-id="31c02-136">number</span></span> |<span data-ttu-id="31c02-137">Percentuale di telemetria generata dall'SDK inviato al portale.</span><span class="sxs-lookup"><span data-stu-id="31c02-137">Percentage of telemetry generated by the SDK that is sent to portal.</span></span> <span data-ttu-id="31c02-138">L'intervallo è 0,0-100,0.</span><span class="sxs-lookup"><span data-stu-id="31c02-138">Range 0.0-100.0.</span></span> |
| <span data-ttu-id="31c02-139">context.device</span><span class="sxs-lookup"><span data-stu-id="31c02-139">context.device</span></span> |<span data-ttu-id="31c02-140">oggetto</span><span class="sxs-lookup"><span data-stu-id="31c02-140">object</span></span> |<span data-ttu-id="31c02-141">Dispositivo client</span><span class="sxs-lookup"><span data-stu-id="31c02-141">Client device</span></span> |
| <span data-ttu-id="31c02-142">context.device.browser</span><span class="sxs-lookup"><span data-stu-id="31c02-142">context.device.browser</span></span> |<span data-ttu-id="31c02-143">string</span><span class="sxs-lookup"><span data-stu-id="31c02-143">string</span></span> |<span data-ttu-id="31c02-144">IE, Chrome, ...</span><span class="sxs-lookup"><span data-stu-id="31c02-144">IE, Chrome, ...</span></span> |
| <span data-ttu-id="31c02-145">context.device.browserVersion</span><span class="sxs-lookup"><span data-stu-id="31c02-145">context.device.browserVersion</span></span> |<span data-ttu-id="31c02-146">string</span><span class="sxs-lookup"><span data-stu-id="31c02-146">string</span></span> |<span data-ttu-id="31c02-147">Chrome 48.0, ...</span><span class="sxs-lookup"><span data-stu-id="31c02-147">Chrome 48.0, ...</span></span> |
| <span data-ttu-id="31c02-148">context.device.deviceModel</span><span class="sxs-lookup"><span data-stu-id="31c02-148">context.device.deviceModel</span></span> |<span data-ttu-id="31c02-149">string</span><span class="sxs-lookup"><span data-stu-id="31c02-149">string</span></span> | |
| <span data-ttu-id="31c02-150">context.device.deviceName</span><span class="sxs-lookup"><span data-stu-id="31c02-150">context.device.deviceName</span></span> |<span data-ttu-id="31c02-151">string</span><span class="sxs-lookup"><span data-stu-id="31c02-151">string</span></span> | |
| <span data-ttu-id="31c02-152">context.device.id</span><span class="sxs-lookup"><span data-stu-id="31c02-152">context.device.id</span></span> |<span data-ttu-id="31c02-153">string</span><span class="sxs-lookup"><span data-stu-id="31c02-153">string</span></span> | |
| <span data-ttu-id="31c02-154">context.device.locale</span><span class="sxs-lookup"><span data-stu-id="31c02-154">context.device.locale</span></span> |<span data-ttu-id="31c02-155">string</span><span class="sxs-lookup"><span data-stu-id="31c02-155">string</span></span> |<span data-ttu-id="31c02-156">en-GB, de-DE, ...</span><span class="sxs-lookup"><span data-stu-id="31c02-156">en-GB, de-DE, ...</span></span> |
| <span data-ttu-id="31c02-157">context.device.network</span><span class="sxs-lookup"><span data-stu-id="31c02-157">context.device.network</span></span> |<span data-ttu-id="31c02-158">string</span><span class="sxs-lookup"><span data-stu-id="31c02-158">string</span></span> | |
| <span data-ttu-id="31c02-159">context.device.oemName</span><span class="sxs-lookup"><span data-stu-id="31c02-159">context.device.oemName</span></span> |<span data-ttu-id="31c02-160">string</span><span class="sxs-lookup"><span data-stu-id="31c02-160">string</span></span> | |
| <span data-ttu-id="31c02-161">context.device.osVersion</span><span class="sxs-lookup"><span data-stu-id="31c02-161">context.device.osVersion</span></span> |<span data-ttu-id="31c02-162">string</span><span class="sxs-lookup"><span data-stu-id="31c02-162">string</span></span> |<span data-ttu-id="31c02-163">Sistema operativo host</span><span class="sxs-lookup"><span data-stu-id="31c02-163">Host OS</span></span> |
| <span data-ttu-id="31c02-164">context.device.roleInstance</span><span class="sxs-lookup"><span data-stu-id="31c02-164">context.device.roleInstance</span></span> |<span data-ttu-id="31c02-165">string</span><span class="sxs-lookup"><span data-stu-id="31c02-165">string</span></span> |<span data-ttu-id="31c02-166">ID dell'host server</span><span class="sxs-lookup"><span data-stu-id="31c02-166">ID of server host</span></span> |
| <span data-ttu-id="31c02-167">context.device.roleName</span><span class="sxs-lookup"><span data-stu-id="31c02-167">context.device.roleName</span></span> |<span data-ttu-id="31c02-168">string</span><span class="sxs-lookup"><span data-stu-id="31c02-168">string</span></span> | |
| <span data-ttu-id="31c02-169">context.device.type</span><span class="sxs-lookup"><span data-stu-id="31c02-169">context.device.type</span></span> |<span data-ttu-id="31c02-170">string</span><span class="sxs-lookup"><span data-stu-id="31c02-170">string</span></span> |<span data-ttu-id="31c02-171">PC, Browser,...</span><span class="sxs-lookup"><span data-stu-id="31c02-171">PC, Browser, ...</span></span> |
| <span data-ttu-id="31c02-172">context.location</span><span class="sxs-lookup"><span data-stu-id="31c02-172">context.location</span></span> |<span data-ttu-id="31c02-173">oggetto</span><span class="sxs-lookup"><span data-stu-id="31c02-173">object</span></span> |<span data-ttu-id="31c02-174">Derivato da clientip.</span><span class="sxs-lookup"><span data-stu-id="31c02-174">Derived from clientip.</span></span> |
| <span data-ttu-id="31c02-175">context.location.city</span><span class="sxs-lookup"><span data-stu-id="31c02-175">context.location.city</span></span> |<span data-ttu-id="31c02-176">string</span><span class="sxs-lookup"><span data-stu-id="31c02-176">string</span></span> |<span data-ttu-id="31c02-177">Derivato da clientip, se noto</span><span class="sxs-lookup"><span data-stu-id="31c02-177">Derived from clientip, if known</span></span> |
| <span data-ttu-id="31c02-178">context.location.clientip</span><span class="sxs-lookup"><span data-stu-id="31c02-178">context.location.clientip</span></span> |<span data-ttu-id="31c02-179">string</span><span class="sxs-lookup"><span data-stu-id="31c02-179">string</span></span> |<span data-ttu-id="31c02-180">L'ultimo ottagono viene reso anonimo come 0.</span><span class="sxs-lookup"><span data-stu-id="31c02-180">Last octagon is anonymized to 0.</span></span> |
| <span data-ttu-id="31c02-181">context.location.continent</span><span class="sxs-lookup"><span data-stu-id="31c02-181">context.location.continent</span></span> |<span data-ttu-id="31c02-182">string</span><span class="sxs-lookup"><span data-stu-id="31c02-182">string</span></span> | |
| <span data-ttu-id="31c02-183">context.location.country</span><span class="sxs-lookup"><span data-stu-id="31c02-183">context.location.country</span></span> |<span data-ttu-id="31c02-184">string</span><span class="sxs-lookup"><span data-stu-id="31c02-184">string</span></span> | |
| <span data-ttu-id="31c02-185">context.location.province</span><span class="sxs-lookup"><span data-stu-id="31c02-185">context.location.province</span></span> |<span data-ttu-id="31c02-186">string</span><span class="sxs-lookup"><span data-stu-id="31c02-186">string</span></span> |<span data-ttu-id="31c02-187">Stato o provincia</span><span class="sxs-lookup"><span data-stu-id="31c02-187">State or province</span></span> |
| <span data-ttu-id="31c02-188">context.operation.id</span><span class="sxs-lookup"><span data-stu-id="31c02-188">context.operation.id</span></span> |<span data-ttu-id="31c02-189">string</span><span class="sxs-lookup"><span data-stu-id="31c02-189">string</span></span> |<span data-ttu-id="31c02-190">Gli elementi con lo stesso ID operazione vengono visualizzati come elementi correlati nel portale.</span><span class="sxs-lookup"><span data-stu-id="31c02-190">Items that have the same operation id are shown as Related Items in the portal.</span></span> <span data-ttu-id="31c02-191">In genere è l'ID richiesta.</span><span class="sxs-lookup"><span data-stu-id="31c02-191">Usually the request id.</span></span> |
| <span data-ttu-id="31c02-192">context.operation.name</span><span class="sxs-lookup"><span data-stu-id="31c02-192">context.operation.name</span></span> |<span data-ttu-id="31c02-193">string</span><span class="sxs-lookup"><span data-stu-id="31c02-193">string</span></span> |<span data-ttu-id="31c02-194">URL o nome richiesta</span><span class="sxs-lookup"><span data-stu-id="31c02-194">url or request name</span></span> |
| <span data-ttu-id="31c02-195">context.operation.parentId</span><span class="sxs-lookup"><span data-stu-id="31c02-195">context.operation.parentId</span></span> |<span data-ttu-id="31c02-196">string</span><span class="sxs-lookup"><span data-stu-id="31c02-196">string</span></span> |<span data-ttu-id="31c02-197">Consente elementi correlati annidati.</span><span class="sxs-lookup"><span data-stu-id="31c02-197">Allows nested related items.</span></span> |
| <span data-ttu-id="31c02-198">context.session.id</span><span class="sxs-lookup"><span data-stu-id="31c02-198">context.session.id</span></span> |<span data-ttu-id="31c02-199">string</span><span class="sxs-lookup"><span data-stu-id="31c02-199">string</span></span> |<span data-ttu-id="31c02-200">ID di un gruppo di operazioni con la stessa origine.</span><span class="sxs-lookup"><span data-stu-id="31c02-200">Id of a group of operations from the same source.</span></span> <span data-ttu-id="31c02-201">Un periodo di 30 minuti senza operazioni segnala la fine di una sessione.</span><span class="sxs-lookup"><span data-stu-id="31c02-201">A period of 30 minutes without an operation signals the end of a session.</span></span> |
| <span data-ttu-id="31c02-202">context.session.isFirst</span><span class="sxs-lookup"><span data-stu-id="31c02-202">context.session.isFirst</span></span> |<span data-ttu-id="31c02-203">boolean</span><span class="sxs-lookup"><span data-stu-id="31c02-203">boolean</span></span> | |
| <span data-ttu-id="31c02-204">context.user.accountAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="31c02-204">context.user.accountAcquisitionDate</span></span> |<span data-ttu-id="31c02-205">string</span><span class="sxs-lookup"><span data-stu-id="31c02-205">string</span></span> | |
| <span data-ttu-id="31c02-206">context.user.anonAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="31c02-206">context.user.anonAcquisitionDate</span></span> |<span data-ttu-id="31c02-207">string</span><span class="sxs-lookup"><span data-stu-id="31c02-207">string</span></span> | |
| <span data-ttu-id="31c02-208">context.user.anonId</span><span class="sxs-lookup"><span data-stu-id="31c02-208">context.user.anonId</span></span> |<span data-ttu-id="31c02-209">string</span><span class="sxs-lookup"><span data-stu-id="31c02-209">string</span></span> | |
| <span data-ttu-id="31c02-210">context.user.authAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="31c02-210">context.user.authAcquisitionDate</span></span> |<span data-ttu-id="31c02-211">string</span><span class="sxs-lookup"><span data-stu-id="31c02-211">string</span></span> |[<span data-ttu-id="31c02-212">Utente autenticato</span><span class="sxs-lookup"><span data-stu-id="31c02-212">Authenticated User</span></span>](app-insights-api-custom-events-metrics.md#authenticated-users) |
| <span data-ttu-id="31c02-213">context.user.isAuthenticated</span><span class="sxs-lookup"><span data-stu-id="31c02-213">context.user.isAuthenticated</span></span> |<span data-ttu-id="31c02-214">boolean</span><span class="sxs-lookup"><span data-stu-id="31c02-214">boolean</span></span> | |
| <span data-ttu-id="31c02-215">internal.data.documentVersion</span><span class="sxs-lookup"><span data-stu-id="31c02-215">internal.data.documentVersion</span></span> |<span data-ttu-id="31c02-216">string</span><span class="sxs-lookup"><span data-stu-id="31c02-216">string</span></span> | |
| <span data-ttu-id="31c02-217">internal.data.id</span><span class="sxs-lookup"><span data-stu-id="31c02-217">internal.data.id</span></span> |<span data-ttu-id="31c02-218">string</span><span class="sxs-lookup"><span data-stu-id="31c02-218">string</span></span> | |

## <a name="events"></a><span data-ttu-id="31c02-219">Eventi</span><span class="sxs-lookup"><span data-stu-id="31c02-219">Events</span></span>
<span data-ttu-id="31c02-220">Eventi personalizzati generati da [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="31c02-220">Custom events generated by [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

| <span data-ttu-id="31c02-221">Path</span><span class="sxs-lookup"><span data-stu-id="31c02-221">Path</span></span> | <span data-ttu-id="31c02-222">Tipo</span><span class="sxs-lookup"><span data-stu-id="31c02-222">Type</span></span> | <span data-ttu-id="31c02-223">Note</span><span class="sxs-lookup"><span data-stu-id="31c02-223">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31c02-224">event [0] count</span><span class="sxs-lookup"><span data-stu-id="31c02-224">event [0] count</span></span> |<span data-ttu-id="31c02-225">numero intero</span><span class="sxs-lookup"><span data-stu-id="31c02-225">integer</span></span> |<span data-ttu-id="31c02-226">100/(frequenza di[campionamento](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="31c02-226">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="31c02-227">Ad esempio, 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="31c02-227">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="31c02-228">event [0] name</span><span class="sxs-lookup"><span data-stu-id="31c02-228">event [0] name</span></span> |<span data-ttu-id="31c02-229">string</span><span class="sxs-lookup"><span data-stu-id="31c02-229">string</span></span> |<span data-ttu-id="31c02-230">Nome evento.</span><span class="sxs-lookup"><span data-stu-id="31c02-230">Event name.</span></span>  <span data-ttu-id="31c02-231">Lunghezza massima: 250.</span><span class="sxs-lookup"><span data-stu-id="31c02-231">Max length 250.</span></span> |
| <span data-ttu-id="31c02-232">event [0] url</span><span class="sxs-lookup"><span data-stu-id="31c02-232">event [0] url</span></span> |<span data-ttu-id="31c02-233">string</span><span class="sxs-lookup"><span data-stu-id="31c02-233">string</span></span> | |
| <span data-ttu-id="31c02-234">event [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="31c02-234">event [0] urlData.base</span></span> |<span data-ttu-id="31c02-235">string</span><span class="sxs-lookup"><span data-stu-id="31c02-235">string</span></span> | |
| <span data-ttu-id="31c02-236">event [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="31c02-236">event [0] urlData.host</span></span> |<span data-ttu-id="31c02-237">string</span><span class="sxs-lookup"><span data-stu-id="31c02-237">string</span></span> | |

## <a name="exceptions"></a><span data-ttu-id="31c02-238">Eccezioni</span><span class="sxs-lookup"><span data-stu-id="31c02-238">Exceptions</span></span>
<span data-ttu-id="31c02-239">Segnala le [eccezioni](app-insights-asp-net-exceptions.md) nel server e nel browser.</span><span class="sxs-lookup"><span data-stu-id="31c02-239">Reports [exceptions](app-insights-asp-net-exceptions.md) in the server and in the browser.</span></span>

| <span data-ttu-id="31c02-240">Path</span><span class="sxs-lookup"><span data-stu-id="31c02-240">Path</span></span> | <span data-ttu-id="31c02-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="31c02-241">Type</span></span> | <span data-ttu-id="31c02-242">Note</span><span class="sxs-lookup"><span data-stu-id="31c02-242">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31c02-243">basicException [0] assembly</span><span class="sxs-lookup"><span data-stu-id="31c02-243">basicException [0] assembly</span></span> |<span data-ttu-id="31c02-244">string</span><span class="sxs-lookup"><span data-stu-id="31c02-244">string</span></span> | |
| <span data-ttu-id="31c02-245">basicException [0] count</span><span class="sxs-lookup"><span data-stu-id="31c02-245">basicException [0] count</span></span> |<span data-ttu-id="31c02-246">numero intero</span><span class="sxs-lookup"><span data-stu-id="31c02-246">integer</span></span> |<span data-ttu-id="31c02-247">100/(frequenza di[campionamento](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="31c02-247">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="31c02-248">Ad esempio, 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="31c02-248">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="31c02-249">basicException [0] exceptionGroup</span><span class="sxs-lookup"><span data-stu-id="31c02-249">basicException [0] exceptionGroup</span></span> |<span data-ttu-id="31c02-250">string</span><span class="sxs-lookup"><span data-stu-id="31c02-250">string</span></span> | |
| <span data-ttu-id="31c02-251">basicException [0] exceptionType</span><span class="sxs-lookup"><span data-stu-id="31c02-251">basicException [0] exceptionType</span></span> |<span data-ttu-id="31c02-252">string</span><span class="sxs-lookup"><span data-stu-id="31c02-252">string</span></span> | |
| <span data-ttu-id="31c02-253">basicException [0] failedUserCodeMethod</span><span class="sxs-lookup"><span data-stu-id="31c02-253">basicException [0] failedUserCodeMethod</span></span> |<span data-ttu-id="31c02-254">string</span><span class="sxs-lookup"><span data-stu-id="31c02-254">string</span></span> | |
| <span data-ttu-id="31c02-255">basicException [0] failedUserCodeAssembly</span><span class="sxs-lookup"><span data-stu-id="31c02-255">basicException [0] failedUserCodeAssembly</span></span> |<span data-ttu-id="31c02-256">string</span><span class="sxs-lookup"><span data-stu-id="31c02-256">string</span></span> | |
| <span data-ttu-id="31c02-257">basicException [0] handledAt</span><span class="sxs-lookup"><span data-stu-id="31c02-257">basicException [0] handledAt</span></span> |<span data-ttu-id="31c02-258">string</span><span class="sxs-lookup"><span data-stu-id="31c02-258">string</span></span> | |
| <span data-ttu-id="31c02-259">basicException [0] hasFullStack</span><span class="sxs-lookup"><span data-stu-id="31c02-259">basicException [0] hasFullStack</span></span> |<span data-ttu-id="31c02-260">boolean</span><span class="sxs-lookup"><span data-stu-id="31c02-260">boolean</span></span> | |
| <span data-ttu-id="31c02-261">basicException [0] id</span><span class="sxs-lookup"><span data-stu-id="31c02-261">basicException [0] id</span></span> |<span data-ttu-id="31c02-262">string</span><span class="sxs-lookup"><span data-stu-id="31c02-262">string</span></span> | |
| <span data-ttu-id="31c02-263">basicException [0] method</span><span class="sxs-lookup"><span data-stu-id="31c02-263">basicException [0] method</span></span> |<span data-ttu-id="31c02-264">string</span><span class="sxs-lookup"><span data-stu-id="31c02-264">string</span></span> | |
| <span data-ttu-id="31c02-265">basicException [0] message</span><span class="sxs-lookup"><span data-stu-id="31c02-265">basicException [0] message</span></span> |<span data-ttu-id="31c02-266">string</span><span class="sxs-lookup"><span data-stu-id="31c02-266">string</span></span> |<span data-ttu-id="31c02-267">Messaggio dell'eccezione.</span><span class="sxs-lookup"><span data-stu-id="31c02-267">Exception message.</span></span> <span data-ttu-id="31c02-268">Lunghezza massima: 10 K.</span><span class="sxs-lookup"><span data-stu-id="31c02-268">Max length 10k.</span></span> |
| <span data-ttu-id="31c02-269">basicException [0] outerExceptionMessage</span><span class="sxs-lookup"><span data-stu-id="31c02-269">basicException [0] outerExceptionMessage</span></span> |<span data-ttu-id="31c02-270">string</span><span class="sxs-lookup"><span data-stu-id="31c02-270">string</span></span> | |
| <span data-ttu-id="31c02-271">basicException [0] outerExceptionThrownAtAssembly</span><span class="sxs-lookup"><span data-stu-id="31c02-271">basicException [0] outerExceptionThrownAtAssembly</span></span> |<span data-ttu-id="31c02-272">string</span><span class="sxs-lookup"><span data-stu-id="31c02-272">string</span></span> | |
| <span data-ttu-id="31c02-273">basicException [0] outerExceptionThrownAtMethod</span><span class="sxs-lookup"><span data-stu-id="31c02-273">basicException [0] outerExceptionThrownAtMethod</span></span> |<span data-ttu-id="31c02-274">string</span><span class="sxs-lookup"><span data-stu-id="31c02-274">string</span></span> | |
| <span data-ttu-id="31c02-275">basicException [0] outerExceptionType</span><span class="sxs-lookup"><span data-stu-id="31c02-275">basicException [0] outerExceptionType</span></span> |<span data-ttu-id="31c02-276">string</span><span class="sxs-lookup"><span data-stu-id="31c02-276">string</span></span> | |
| <span data-ttu-id="31c02-277">basicException [0] outerId</span><span class="sxs-lookup"><span data-stu-id="31c02-277">basicException [0] outerId</span></span> |<span data-ttu-id="31c02-278">string</span><span class="sxs-lookup"><span data-stu-id="31c02-278">string</span></span> | |
| <span data-ttu-id="31c02-279">basicException [0] parsedStack [0] assembly</span><span class="sxs-lookup"><span data-stu-id="31c02-279">basicException [0] parsedStack [0] assembly</span></span> |<span data-ttu-id="31c02-280">string</span><span class="sxs-lookup"><span data-stu-id="31c02-280">string</span></span> | |
| <span data-ttu-id="31c02-281">basicException [0] parsedStack [0] fileName</span><span class="sxs-lookup"><span data-stu-id="31c02-281">basicException [0] parsedStack [0] fileName</span></span> |<span data-ttu-id="31c02-282">string</span><span class="sxs-lookup"><span data-stu-id="31c02-282">string</span></span> | |
| <span data-ttu-id="31c02-283">basicException [0] parsedStack [0] level</span><span class="sxs-lookup"><span data-stu-id="31c02-283">basicException [0] parsedStack [0] level</span></span> |<span data-ttu-id="31c02-284">numero intero</span><span class="sxs-lookup"><span data-stu-id="31c02-284">integer</span></span> | |
| <span data-ttu-id="31c02-285">basicException [0] parsedStack [0] line</span><span class="sxs-lookup"><span data-stu-id="31c02-285">basicException [0] parsedStack [0] line</span></span> |<span data-ttu-id="31c02-286">numero intero</span><span class="sxs-lookup"><span data-stu-id="31c02-286">integer</span></span> | |
| <span data-ttu-id="31c02-287">basicException [0] parsedStack [0] method</span><span class="sxs-lookup"><span data-stu-id="31c02-287">basicException [0] parsedStack [0] method</span></span> |<span data-ttu-id="31c02-288">string</span><span class="sxs-lookup"><span data-stu-id="31c02-288">string</span></span> | |
| <span data-ttu-id="31c02-289">basicException [0] stack</span><span class="sxs-lookup"><span data-stu-id="31c02-289">basicException [0] stack</span></span> |<span data-ttu-id="31c02-290">string</span><span class="sxs-lookup"><span data-stu-id="31c02-290">string</span></span> |<span data-ttu-id="31c02-291">Lunghezza massima: 10 K.</span><span class="sxs-lookup"><span data-stu-id="31c02-291">Max length 10k</span></span> |
| <span data-ttu-id="31c02-292">basicException [0] typeName</span><span class="sxs-lookup"><span data-stu-id="31c02-292">basicException [0] typeName</span></span> |<span data-ttu-id="31c02-293">string</span><span class="sxs-lookup"><span data-stu-id="31c02-293">string</span></span> | |

## <a name="trace-messages"></a><span data-ttu-id="31c02-294">Messaggi di traccia</span><span class="sxs-lookup"><span data-stu-id="31c02-294">Trace Messages</span></span>
<span data-ttu-id="31c02-295">Inviati da [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace) e dagli [adattatori di registrazione](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="31c02-295">Sent by [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace), and by the [logging adapters](app-insights-asp-net-trace-logs.md).</span></span>

| <span data-ttu-id="31c02-296">Path</span><span class="sxs-lookup"><span data-stu-id="31c02-296">Path</span></span> | <span data-ttu-id="31c02-297">Tipo</span><span class="sxs-lookup"><span data-stu-id="31c02-297">Type</span></span> | <span data-ttu-id="31c02-298">Note</span><span class="sxs-lookup"><span data-stu-id="31c02-298">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31c02-299">message [0] loggerName</span><span class="sxs-lookup"><span data-stu-id="31c02-299">message [0] loggerName</span></span> |<span data-ttu-id="31c02-300">string</span><span class="sxs-lookup"><span data-stu-id="31c02-300">string</span></span> | |
| <span data-ttu-id="31c02-301">message [0] parameters</span><span class="sxs-lookup"><span data-stu-id="31c02-301">message [0] parameters</span></span> |<span data-ttu-id="31c02-302">string</span><span class="sxs-lookup"><span data-stu-id="31c02-302">string</span></span> | |
| <span data-ttu-id="31c02-303">message [0] raw</span><span class="sxs-lookup"><span data-stu-id="31c02-303">message [0] raw</span></span> |<span data-ttu-id="31c02-304">string</span><span class="sxs-lookup"><span data-stu-id="31c02-304">string</span></span> |<span data-ttu-id="31c02-305">Messaggio del log, lunghezza massima 10.000 caratteri.</span><span class="sxs-lookup"><span data-stu-id="31c02-305">The log message, max length 10k.</span></span> |
| <span data-ttu-id="31c02-306">message [0] severityLevel</span><span class="sxs-lookup"><span data-stu-id="31c02-306">message [0] severityLevel</span></span> |<span data-ttu-id="31c02-307">string</span><span class="sxs-lookup"><span data-stu-id="31c02-307">string</span></span> | |

## <a name="remote-dependency"></a><span data-ttu-id="31c02-308">Dipendenza remota</span><span class="sxs-lookup"><span data-stu-id="31c02-308">Remote dependency</span></span>
<span data-ttu-id="31c02-309">Inviata da TrackDependency.</span><span class="sxs-lookup"><span data-stu-id="31c02-309">Sent by TrackDependency.</span></span> <span data-ttu-id="31c02-310">Usata per segnalare le prestazioni e l'utilizzo delle [chiamate alle dipendenze](app-insights-asp-net-dependencies.md) nel server e delle chiamate AJAX nel browser.</span><span class="sxs-lookup"><span data-stu-id="31c02-310">Used to report performance and usage of [calls to dependencies](app-insights-asp-net-dependencies.md) in the server, and AJAX calls in the browser.</span></span>

| <span data-ttu-id="31c02-311">Path</span><span class="sxs-lookup"><span data-stu-id="31c02-311">Path</span></span> | <span data-ttu-id="31c02-312">Tipo</span><span class="sxs-lookup"><span data-stu-id="31c02-312">Type</span></span> | <span data-ttu-id="31c02-313">Note</span><span class="sxs-lookup"><span data-stu-id="31c02-313">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31c02-314">remoteDependency [0] async</span><span class="sxs-lookup"><span data-stu-id="31c02-314">remoteDependency [0] async</span></span> |<span data-ttu-id="31c02-315">boolean</span><span class="sxs-lookup"><span data-stu-id="31c02-315">boolean</span></span> | |
| <span data-ttu-id="31c02-316">remoteDependency [0] baseName</span><span class="sxs-lookup"><span data-stu-id="31c02-316">remoteDependency [0] baseName</span></span> |<span data-ttu-id="31c02-317">string</span><span class="sxs-lookup"><span data-stu-id="31c02-317">string</span></span> | |
| <span data-ttu-id="31c02-318">remoteDependency [0] commandName</span><span class="sxs-lookup"><span data-stu-id="31c02-318">remoteDependency [0] commandName</span></span> |<span data-ttu-id="31c02-319">string</span><span class="sxs-lookup"><span data-stu-id="31c02-319">string</span></span> |<span data-ttu-id="31c02-320">Ad esempio "home/index"</span><span class="sxs-lookup"><span data-stu-id="31c02-320">For example "home/index"</span></span> |
| <span data-ttu-id="31c02-321">remoteDependency [0] count</span><span class="sxs-lookup"><span data-stu-id="31c02-321">remoteDependency [0] count</span></span> |<span data-ttu-id="31c02-322">numero intero</span><span class="sxs-lookup"><span data-stu-id="31c02-322">integer</span></span> |<span data-ttu-id="31c02-323">100/(frequenza di[campionamento](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="31c02-323">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="31c02-324">Ad esempio, 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="31c02-324">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="31c02-325">remoteDependency [0] dependencyTypeName</span><span class="sxs-lookup"><span data-stu-id="31c02-325">remoteDependency [0] dependencyTypeName</span></span> |<span data-ttu-id="31c02-326">string</span><span class="sxs-lookup"><span data-stu-id="31c02-326">string</span></span> |<span data-ttu-id="31c02-327">HTTP, SQL...</span><span class="sxs-lookup"><span data-stu-id="31c02-327">HTTP, SQL, ...</span></span> |
| <span data-ttu-id="31c02-328">remoteDependency [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="31c02-328">remoteDependency [0] durationMetric.value</span></span> |<span data-ttu-id="31c02-329">number</span><span class="sxs-lookup"><span data-stu-id="31c02-329">number</span></span> |<span data-ttu-id="31c02-330">Tempo intercorso tra la chiamata e il completamento della risposta da parte di una dipendenza</span><span class="sxs-lookup"><span data-stu-id="31c02-330">Time from call to completion of response by dependency</span></span> |
| <span data-ttu-id="31c02-331">remoteDependency [0] id</span><span class="sxs-lookup"><span data-stu-id="31c02-331">remoteDependency [0] id</span></span> |<span data-ttu-id="31c02-332">string</span><span class="sxs-lookup"><span data-stu-id="31c02-332">string</span></span> | |
| <span data-ttu-id="31c02-333">remoteDependency [0] name</span><span class="sxs-lookup"><span data-stu-id="31c02-333">remoteDependency [0] name</span></span> |<span data-ttu-id="31c02-334">string</span><span class="sxs-lookup"><span data-stu-id="31c02-334">string</span></span> |<span data-ttu-id="31c02-335">URL.</span><span class="sxs-lookup"><span data-stu-id="31c02-335">Url.</span></span> <span data-ttu-id="31c02-336">Lunghezza massima: 250.</span><span class="sxs-lookup"><span data-stu-id="31c02-336">Max length 250.</span></span> |
| <span data-ttu-id="31c02-337">remoteDependency [0] resultCode</span><span class="sxs-lookup"><span data-stu-id="31c02-337">remoteDependency [0] resultCode</span></span> |<span data-ttu-id="31c02-338">string</span><span class="sxs-lookup"><span data-stu-id="31c02-338">string</span></span> |<span data-ttu-id="31c02-339">Dalla dipendenza HTTP</span><span class="sxs-lookup"><span data-stu-id="31c02-339">from HTTP dependency</span></span> |
| <span data-ttu-id="31c02-340">remoteDependency [0] success</span><span class="sxs-lookup"><span data-stu-id="31c02-340">remoteDependency [0] success</span></span> |<span data-ttu-id="31c02-341">boolean</span><span class="sxs-lookup"><span data-stu-id="31c02-341">boolean</span></span> | |
| <span data-ttu-id="31c02-342">remoteDependency [0] type</span><span class="sxs-lookup"><span data-stu-id="31c02-342">remoteDependency [0] type</span></span> |<span data-ttu-id="31c02-343">string</span><span class="sxs-lookup"><span data-stu-id="31c02-343">string</span></span> |<span data-ttu-id="31c02-344">HTTP, SQL...</span><span class="sxs-lookup"><span data-stu-id="31c02-344">Http, Sql,...</span></span> |
| <span data-ttu-id="31c02-345">remoteDependency [0] url</span><span class="sxs-lookup"><span data-stu-id="31c02-345">remoteDependency [0] url</span></span> |<span data-ttu-id="31c02-346">string</span><span class="sxs-lookup"><span data-stu-id="31c02-346">string</span></span> |<span data-ttu-id="31c02-347">Lunghezza massima: 2000</span><span class="sxs-lookup"><span data-stu-id="31c02-347">Max length 2000</span></span> |
| <span data-ttu-id="31c02-348">remoteDependency [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="31c02-348">remoteDependency [0] urlData.base</span></span> |<span data-ttu-id="31c02-349">string</span><span class="sxs-lookup"><span data-stu-id="31c02-349">string</span></span> |<span data-ttu-id="31c02-350">Lunghezza massima: 2000</span><span class="sxs-lookup"><span data-stu-id="31c02-350">Max length 2000</span></span> |
| <span data-ttu-id="31c02-351">remoteDependency [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="31c02-351">remoteDependency [0] urlData.hashTag</span></span> |<span data-ttu-id="31c02-352">string</span><span class="sxs-lookup"><span data-stu-id="31c02-352">string</span></span> | |
| <span data-ttu-id="31c02-353">remoteDependency [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="31c02-353">remoteDependency [0] urlData.host</span></span> |<span data-ttu-id="31c02-354">string</span><span class="sxs-lookup"><span data-stu-id="31c02-354">string</span></span> |<span data-ttu-id="31c02-355">Lunghezza massima: 200</span><span class="sxs-lookup"><span data-stu-id="31c02-355">Max length 200</span></span> |

## <a name="requests"></a><span data-ttu-id="31c02-356">Richieste</span><span class="sxs-lookup"><span data-stu-id="31c02-356">Requests</span></span>
<span data-ttu-id="31c02-357">Inviate da [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span><span class="sxs-lookup"><span data-stu-id="31c02-357">Sent by [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span></span> <span data-ttu-id="31c02-358">I moduli standard le usano per segnalare il tempo di risposta del server, calcolato nel server.</span><span class="sxs-lookup"><span data-stu-id="31c02-358">The standard modules use this to reports server response time, measured at the server.</span></span>

| <span data-ttu-id="31c02-359">Path</span><span class="sxs-lookup"><span data-stu-id="31c02-359">Path</span></span> | <span data-ttu-id="31c02-360">Tipo</span><span class="sxs-lookup"><span data-stu-id="31c02-360">Type</span></span> | <span data-ttu-id="31c02-361">Note</span><span class="sxs-lookup"><span data-stu-id="31c02-361">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31c02-362">request [0] count</span><span class="sxs-lookup"><span data-stu-id="31c02-362">request [0] count</span></span> |<span data-ttu-id="31c02-363">numero intero</span><span class="sxs-lookup"><span data-stu-id="31c02-363">integer</span></span> |<span data-ttu-id="31c02-364">100/(frequenza di[campionamento](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="31c02-364">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="31c02-365">Ad esempio, 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="31c02-365">For example: 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="31c02-366">request [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="31c02-366">request [0] durationMetric.value</span></span> |<span data-ttu-id="31c02-367">number</span><span class="sxs-lookup"><span data-stu-id="31c02-367">number</span></span> |<span data-ttu-id="31c02-368">Tempo tra l'arrivo della richiesta e la risposta.</span><span class="sxs-lookup"><span data-stu-id="31c02-368">Time from request arriving to response.</span></span> <span data-ttu-id="31c02-369">1e7 == 1 s</span><span class="sxs-lookup"><span data-stu-id="31c02-369">1e7 == 1s</span></span> |
| <span data-ttu-id="31c02-370">request [0] id</span><span class="sxs-lookup"><span data-stu-id="31c02-370">request [0] id</span></span> |<span data-ttu-id="31c02-371">string</span><span class="sxs-lookup"><span data-stu-id="31c02-371">string</span></span> |<span data-ttu-id="31c02-372">ID operazione</span><span class="sxs-lookup"><span data-stu-id="31c02-372">Operation id</span></span> |
| <span data-ttu-id="31c02-373">request [0] name</span><span class="sxs-lookup"><span data-stu-id="31c02-373">request [0] name</span></span> |<span data-ttu-id="31c02-374">string</span><span class="sxs-lookup"><span data-stu-id="31c02-374">string</span></span> |<span data-ttu-id="31c02-375">GET/POST + base URL.</span><span class="sxs-lookup"><span data-stu-id="31c02-375">GET/POST + url base.</span></span>  <span data-ttu-id="31c02-376">Lunghezza massima: 250</span><span class="sxs-lookup"><span data-stu-id="31c02-376">Max length 250</span></span> |
| <span data-ttu-id="31c02-377">request [0] responseCode</span><span class="sxs-lookup"><span data-stu-id="31c02-377">request [0] responseCode</span></span> |<span data-ttu-id="31c02-378">numero intero</span><span class="sxs-lookup"><span data-stu-id="31c02-378">integer</span></span> |<span data-ttu-id="31c02-379">Risposta HTTP inviata al client</span><span class="sxs-lookup"><span data-stu-id="31c02-379">HTTP response sent to client</span></span> |
| <span data-ttu-id="31c02-380">request [0] success</span><span class="sxs-lookup"><span data-stu-id="31c02-380">request [0] success</span></span> |<span data-ttu-id="31c02-381">boolean</span><span class="sxs-lookup"><span data-stu-id="31c02-381">boolean</span></span> |<span data-ttu-id="31c02-382">Valore predefinito == (responseCode &lt; 400)</span><span class="sxs-lookup"><span data-stu-id="31c02-382">Default == (responseCode &lt; 400)</span></span> |
| <span data-ttu-id="31c02-383">request [0] url</span><span class="sxs-lookup"><span data-stu-id="31c02-383">request [0] url</span></span> |<span data-ttu-id="31c02-384">string</span><span class="sxs-lookup"><span data-stu-id="31c02-384">string</span></span> |<span data-ttu-id="31c02-385">Host non incluso</span><span class="sxs-lookup"><span data-stu-id="31c02-385">Not including host</span></span> |
| <span data-ttu-id="31c02-386">request [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="31c02-386">request [0] urlData.base</span></span> |<span data-ttu-id="31c02-387">string</span><span class="sxs-lookup"><span data-stu-id="31c02-387">string</span></span> | |
| <span data-ttu-id="31c02-388">request [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="31c02-388">request [0] urlData.hashTag</span></span> |<span data-ttu-id="31c02-389">string</span><span class="sxs-lookup"><span data-stu-id="31c02-389">string</span></span> | |
| <span data-ttu-id="31c02-390">request [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="31c02-390">request [0] urlData.host</span></span> |<span data-ttu-id="31c02-391">string</span><span class="sxs-lookup"><span data-stu-id="31c02-391">string</span></span> | |

## <a name="page-view-performance"></a><span data-ttu-id="31c02-392">Prestazioni visualizzazioni pagina</span><span class="sxs-lookup"><span data-stu-id="31c02-392">Page View Performance</span></span>
<span data-ttu-id="31c02-393">Inviate dal browser.</span><span class="sxs-lookup"><span data-stu-id="31c02-393">Sent by the browser.</span></span> <span data-ttu-id="31c02-394">Misura il tempo necessario per elaborare una pagina, da quando l'utente avvia la richiesta al completamento della visualizzazione (escluse le chiamate AJAX asincrone).</span><span class="sxs-lookup"><span data-stu-id="31c02-394">Measures the time to process a page, from user initiating the request to display complete (excluding async AJAX calls).</span></span>

<span data-ttu-id="31c02-395">I valori del contesto indicano la versione del sistema operativo client e del browser.</span><span class="sxs-lookup"><span data-stu-id="31c02-395">Context values show client OS and browser version.</span></span>

| <span data-ttu-id="31c02-396">Path</span><span class="sxs-lookup"><span data-stu-id="31c02-396">Path</span></span> | <span data-ttu-id="31c02-397">Tipo</span><span class="sxs-lookup"><span data-stu-id="31c02-397">Type</span></span> | <span data-ttu-id="31c02-398">Note</span><span class="sxs-lookup"><span data-stu-id="31c02-398">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31c02-399">clientPerformance [0] clientProcess.value</span><span class="sxs-lookup"><span data-stu-id="31c02-399">clientPerformance [0] clientProcess.value</span></span> |<span data-ttu-id="31c02-400">numero intero</span><span class="sxs-lookup"><span data-stu-id="31c02-400">integer</span></span> |<span data-ttu-id="31c02-401">Tempo compreso tra la fine della ricezione del codice HTML e la visualizzazione della pagina.</span><span class="sxs-lookup"><span data-stu-id="31c02-401">Time from end of receiving the HTML to displaying the page.</span></span> |
| <span data-ttu-id="31c02-402">clientPerformance [0] name</span><span class="sxs-lookup"><span data-stu-id="31c02-402">clientPerformance [0] name</span></span> |<span data-ttu-id="31c02-403">string</span><span class="sxs-lookup"><span data-stu-id="31c02-403">string</span></span> | |
| <span data-ttu-id="31c02-404">clientPerformance [0] networkConnection.value</span><span class="sxs-lookup"><span data-stu-id="31c02-404">clientPerformance [0] networkConnection.value</span></span> |<span data-ttu-id="31c02-405">numero intero</span><span class="sxs-lookup"><span data-stu-id="31c02-405">integer</span></span> |<span data-ttu-id="31c02-406">Tempo necessario per stabilire una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="31c02-406">Time taken to establish a network connection.</span></span> |
| <span data-ttu-id="31c02-407">clientPerformance [0] receiveRequest.value</span><span class="sxs-lookup"><span data-stu-id="31c02-407">clientPerformance [0] receiveRequest.value</span></span> |<span data-ttu-id="31c02-408">numero intero</span><span class="sxs-lookup"><span data-stu-id="31c02-408">integer</span></span> |<span data-ttu-id="31c02-409">Tempo compreso tra la fine dell'invio della richiesta e la ricezione del codice HTML nella risposta.</span><span class="sxs-lookup"><span data-stu-id="31c02-409">Time from end of sending the request to receiving the HTML in reply.</span></span> |
| <span data-ttu-id="31c02-410">clientPerformance [0] sendRequest.value</span><span class="sxs-lookup"><span data-stu-id="31c02-410">clientPerformance [0] sendRequest.value</span></span> |<span data-ttu-id="31c02-411">numero intero</span><span class="sxs-lookup"><span data-stu-id="31c02-411">integer</span></span> |<span data-ttu-id="31c02-412">Tempo necessario per inviare la richiesta HTTP.</span><span class="sxs-lookup"><span data-stu-id="31c02-412">Time from taken to send the HTTP request.</span></span> |
| <span data-ttu-id="31c02-413">clientPerformance [0] total.value</span><span class="sxs-lookup"><span data-stu-id="31c02-413">clientPerformance [0] total.value</span></span> |<span data-ttu-id="31c02-414">numero intero</span><span class="sxs-lookup"><span data-stu-id="31c02-414">integer</span></span> |<span data-ttu-id="31c02-415">Tempo compreso tra l'inizio dell'invio della richiesta e la visualizzazione della pagina.</span><span class="sxs-lookup"><span data-stu-id="31c02-415">Time from starting to send the request to displaying the page.</span></span> |
| <span data-ttu-id="31c02-416">clientPerformance [0] url</span><span class="sxs-lookup"><span data-stu-id="31c02-416">clientPerformance [0] url</span></span> |<span data-ttu-id="31c02-417">string</span><span class="sxs-lookup"><span data-stu-id="31c02-417">string</span></span> |<span data-ttu-id="31c02-418">URL di questa richiesta</span><span class="sxs-lookup"><span data-stu-id="31c02-418">URL of this request</span></span> |
| <span data-ttu-id="31c02-419">clientPerformance [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="31c02-419">clientPerformance [0] urlData.base</span></span> |<span data-ttu-id="31c02-420">string</span><span class="sxs-lookup"><span data-stu-id="31c02-420">string</span></span> | |
| <span data-ttu-id="31c02-421">clientPerformance [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="31c02-421">clientPerformance [0] urlData.hashTag</span></span> |<span data-ttu-id="31c02-422">string</span><span class="sxs-lookup"><span data-stu-id="31c02-422">string</span></span> | |
| <span data-ttu-id="31c02-423">clientPerformance [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="31c02-423">clientPerformance [0] urlData.host</span></span> |<span data-ttu-id="31c02-424">string</span><span class="sxs-lookup"><span data-stu-id="31c02-424">string</span></span> | |
| <span data-ttu-id="31c02-425">clientPerformance [0] urlData.protocol</span><span class="sxs-lookup"><span data-stu-id="31c02-425">clientPerformance [0] urlData.protocol</span></span> |<span data-ttu-id="31c02-426">string</span><span class="sxs-lookup"><span data-stu-id="31c02-426">string</span></span> | |

## <a name="page-views"></a><span data-ttu-id="31c02-427">Visualizzazioni pagina</span><span class="sxs-lookup"><span data-stu-id="31c02-427">Page Views</span></span>
<span data-ttu-id="31c02-428">Inviate da trackPageView() o [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span><span class="sxs-lookup"><span data-stu-id="31c02-428">Sent by trackPageView() or [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span></span>

| <span data-ttu-id="31c02-429">Path</span><span class="sxs-lookup"><span data-stu-id="31c02-429">Path</span></span> | <span data-ttu-id="31c02-430">Tipo</span><span class="sxs-lookup"><span data-stu-id="31c02-430">Type</span></span> | <span data-ttu-id="31c02-431">Note</span><span class="sxs-lookup"><span data-stu-id="31c02-431">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31c02-432">view [0] count</span><span class="sxs-lookup"><span data-stu-id="31c02-432">view [0] count</span></span> |<span data-ttu-id="31c02-433">numero intero</span><span class="sxs-lookup"><span data-stu-id="31c02-433">integer</span></span> |<span data-ttu-id="31c02-434">100/(frequenza di[campionamento](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="31c02-434">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="31c02-435">Ad esempio, 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="31c02-435">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="31c02-436">view [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="31c02-436">view [0] durationMetric.value</span></span> |<span data-ttu-id="31c02-437">numero intero</span><span class="sxs-lookup"><span data-stu-id="31c02-437">integer</span></span> |<span data-ttu-id="31c02-438">Valore facoltativo impostato in trackPageView() o da startTrackPage() - stopTrackPage().</span><span class="sxs-lookup"><span data-stu-id="31c02-438">Value optionally set in trackPageView() or by startTrackPage() - stopTrackPage().</span></span> <span data-ttu-id="31c02-439">Non corrisponde ai valori di clientPerformance.</span><span class="sxs-lookup"><span data-stu-id="31c02-439">Not the same as clientPerformance values.</span></span> |
| <span data-ttu-id="31c02-440">view [0] name</span><span class="sxs-lookup"><span data-stu-id="31c02-440">view [0] name</span></span> |<span data-ttu-id="31c02-441">string</span><span class="sxs-lookup"><span data-stu-id="31c02-441">string</span></span> |<span data-ttu-id="31c02-442">Titolo della pagina.</span><span class="sxs-lookup"><span data-stu-id="31c02-442">Page title.</span></span>  <span data-ttu-id="31c02-443">Lunghezza massima: 250</span><span class="sxs-lookup"><span data-stu-id="31c02-443">Max length 250</span></span> |
| <span data-ttu-id="31c02-444">view [0] url</span><span class="sxs-lookup"><span data-stu-id="31c02-444">view [0] url</span></span> |<span data-ttu-id="31c02-445">string</span><span class="sxs-lookup"><span data-stu-id="31c02-445">string</span></span> | |
| <span data-ttu-id="31c02-446">view [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="31c02-446">view [0] urlData.base</span></span> |<span data-ttu-id="31c02-447">string</span><span class="sxs-lookup"><span data-stu-id="31c02-447">string</span></span> | |
| <span data-ttu-id="31c02-448">view [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="31c02-448">view [0] urlData.hashTag</span></span> |<span data-ttu-id="31c02-449">string</span><span class="sxs-lookup"><span data-stu-id="31c02-449">string</span></span> | |
| <span data-ttu-id="31c02-450">view [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="31c02-450">view [0] urlData.host</span></span> |<span data-ttu-id="31c02-451">string</span><span class="sxs-lookup"><span data-stu-id="31c02-451">string</span></span> | |

## <a name="availability"></a><span data-ttu-id="31c02-452">Disponibilità</span><span class="sxs-lookup"><span data-stu-id="31c02-452">Availability</span></span>
<span data-ttu-id="31c02-453">Segnala i [test Web di disponibilità](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="31c02-453">Reports [availability web tests](app-insights-monitor-web-app-availability.md).</span></span>

| <span data-ttu-id="31c02-454">Path</span><span class="sxs-lookup"><span data-stu-id="31c02-454">Path</span></span> | <span data-ttu-id="31c02-455">Tipo</span><span class="sxs-lookup"><span data-stu-id="31c02-455">Type</span></span> | <span data-ttu-id="31c02-456">Note</span><span class="sxs-lookup"><span data-stu-id="31c02-456">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31c02-457">availability [0] availabilityMetric.name</span><span class="sxs-lookup"><span data-stu-id="31c02-457">availability [0] availabilityMetric.name</span></span> |<span data-ttu-id="31c02-458">string</span><span class="sxs-lookup"><span data-stu-id="31c02-458">string</span></span> |<span data-ttu-id="31c02-459">Disponibilità</span><span class="sxs-lookup"><span data-stu-id="31c02-459">availability</span></span> |
| <span data-ttu-id="31c02-460">availability [0] availabilityMetric.value</span><span class="sxs-lookup"><span data-stu-id="31c02-460">availability [0] availabilityMetric.value</span></span> |<span data-ttu-id="31c02-461">number</span><span class="sxs-lookup"><span data-stu-id="31c02-461">number</span></span> |<span data-ttu-id="31c02-462">1,0 o 0,0</span><span class="sxs-lookup"><span data-stu-id="31c02-462">1.0 or 0.0</span></span> |
| <span data-ttu-id="31c02-463">availability [0] count</span><span class="sxs-lookup"><span data-stu-id="31c02-463">availability [0] count</span></span> |<span data-ttu-id="31c02-464">numero intero</span><span class="sxs-lookup"><span data-stu-id="31c02-464">integer</span></span> |<span data-ttu-id="31c02-465">100/(frequenza di[campionamento](app-insights-sampling.md) ).</span><span class="sxs-lookup"><span data-stu-id="31c02-465">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="31c02-466">Ad esempio, 4 =&gt; 25%.</span><span class="sxs-lookup"><span data-stu-id="31c02-466">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="31c02-467">availability [0] dataSizeMetric.name</span><span class="sxs-lookup"><span data-stu-id="31c02-467">availability [0] dataSizeMetric.name</span></span> |<span data-ttu-id="31c02-468">string</span><span class="sxs-lookup"><span data-stu-id="31c02-468">string</span></span> | |
| <span data-ttu-id="31c02-469">availability [0] dataSizeMetric.value</span><span class="sxs-lookup"><span data-stu-id="31c02-469">availability [0] dataSizeMetric.value</span></span> |<span data-ttu-id="31c02-470">numero intero</span><span class="sxs-lookup"><span data-stu-id="31c02-470">integer</span></span> | |
| <span data-ttu-id="31c02-471">availability [0] durationMetric.name</span><span class="sxs-lookup"><span data-stu-id="31c02-471">availability [0] durationMetric.name</span></span> |<span data-ttu-id="31c02-472">string</span><span class="sxs-lookup"><span data-stu-id="31c02-472">string</span></span> | |
| <span data-ttu-id="31c02-473">availability [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="31c02-473">availability [0] durationMetric.value</span></span> |<span data-ttu-id="31c02-474">number</span><span class="sxs-lookup"><span data-stu-id="31c02-474">number</span></span> |<span data-ttu-id="31c02-475">Durata del test.</span><span class="sxs-lookup"><span data-stu-id="31c02-475">Duration of test.</span></span> <span data-ttu-id="31c02-476">1e7==1 s</span><span class="sxs-lookup"><span data-stu-id="31c02-476">1e7==1s</span></span> |
| <span data-ttu-id="31c02-477">availability [0] message</span><span class="sxs-lookup"><span data-stu-id="31c02-477">availability [0] message</span></span> |<span data-ttu-id="31c02-478">string</span><span class="sxs-lookup"><span data-stu-id="31c02-478">string</span></span> |<span data-ttu-id="31c02-479">Diagnostica di errori</span><span class="sxs-lookup"><span data-stu-id="31c02-479">Failure diagnostic</span></span> |
| <span data-ttu-id="31c02-480">availability [0] result</span><span class="sxs-lookup"><span data-stu-id="31c02-480">availability [0] result</span></span> |<span data-ttu-id="31c02-481">string</span><span class="sxs-lookup"><span data-stu-id="31c02-481">string</span></span> |<span data-ttu-id="31c02-482">Esito positivo o negativo</span><span class="sxs-lookup"><span data-stu-id="31c02-482">Pass/Fail</span></span> |
| <span data-ttu-id="31c02-483">availability [0] runLocation</span><span class="sxs-lookup"><span data-stu-id="31c02-483">availability [0] runLocation</span></span> |<span data-ttu-id="31c02-484">string</span><span class="sxs-lookup"><span data-stu-id="31c02-484">string</span></span> |<span data-ttu-id="31c02-485">Origine geografica della richiesta HTTP</span><span class="sxs-lookup"><span data-stu-id="31c02-485">Geo source of http req</span></span> |
| <span data-ttu-id="31c02-486">availability [0] testName</span><span class="sxs-lookup"><span data-stu-id="31c02-486">availability [0] testName</span></span> |<span data-ttu-id="31c02-487">string</span><span class="sxs-lookup"><span data-stu-id="31c02-487">string</span></span> | |
| <span data-ttu-id="31c02-488">availability [0] testRunId</span><span class="sxs-lookup"><span data-stu-id="31c02-488">availability [0] testRunId</span></span> |<span data-ttu-id="31c02-489">string</span><span class="sxs-lookup"><span data-stu-id="31c02-489">string</span></span> | |
| <span data-ttu-id="31c02-490">availability [0] testTimestamp</span><span class="sxs-lookup"><span data-stu-id="31c02-490">availability [0] testTimestamp</span></span> |<span data-ttu-id="31c02-491">string</span><span class="sxs-lookup"><span data-stu-id="31c02-491">string</span></span> | |

## <a name="metrics"></a><span data-ttu-id="31c02-492">Metrica</span><span class="sxs-lookup"><span data-stu-id="31c02-492">Metrics</span></span>
<span data-ttu-id="31c02-493">Generata da TrackMetric().</span><span class="sxs-lookup"><span data-stu-id="31c02-493">Generated by TrackMetric().</span></span>

<span data-ttu-id="31c02-494">Il valore della metrica è disponibile in context.custom.metrics[0]</span><span class="sxs-lookup"><span data-stu-id="31c02-494">The metric value is found in context.custom.metrics[0]</span></span>

<span data-ttu-id="31c02-495">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="31c02-495">For example:</span></span>

    {
     "metric": [ ],
     "context": {
     ...
     "custom": {
        "dimensions": [
          { "ProcessId": "4068" }
        ],
        "metrics": [
          {
            "dispatchRate": {
              "value": 0.001295,
              "count": 1.0,
              "min": 0.001295,
              "max": 0.001295,
              "stdDev": 0.0,
              "sampledValue": 0.001295,
              "sum": 0.001295
            }
          }
         } ] }
    }

## <a name="about-metric-values"></a><span data-ttu-id="31c02-496">Informazioni sui valori della metrica</span><span class="sxs-lookup"><span data-stu-id="31c02-496">About metric values</span></span>
<span data-ttu-id="31c02-497">I valori della metrica, nei report della metrica e altrove, vengono segnalati con una struttura di oggetti standard.</span><span class="sxs-lookup"><span data-stu-id="31c02-497">Metric values, both in metric reports and elsewhere, are reported with a standard object structure.</span></span> <span data-ttu-id="31c02-498">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="31c02-498">For example:</span></span>

      "durationMetric": {
        "name": "contoso.org",
        "type": "Aggregation",
        "value": 468.71603053650279,
        "count": 1.0,
        "min": 468.71603053650279,
        "max": 468.71603053650279,
        "stdDev": 0.0,
        "sampledValue": 468.71603053650279
      }

<span data-ttu-id="31c02-499">Attualmente (ma la situazione potrebbe cambiare in futuro) di tutti i valori segnalati dai moduli SDK standard sono utili `count==1` e solo i campi `name` e `value`.</span><span class="sxs-lookup"><span data-stu-id="31c02-499">Currently - though this might change in the future - in all values reported from the standard SDK modules, `count==1` and only the `name` and `value` fields are useful.</span></span> <span data-ttu-id="31c02-500">L'unico caso in cui sarebbero diversi è quello in cui si scrivono chiamate TrackMetric personalizzate in cui si impostano gli altri parametri.</span><span class="sxs-lookup"><span data-stu-id="31c02-500">The only case where they would be different would be if you write your own TrackMetric calls in which you set the other parameters.</span></span>

<span data-ttu-id="31c02-501">Lo scopo degli altri campi è quello di consentire l'aggregazione della metrica nell'SDK, per ridurre il traffico verso il portale.</span><span class="sxs-lookup"><span data-stu-id="31c02-501">The purpose of the other fields is to allow metrics to be aggregated in the SDK, to reduce traffic to the portal.</span></span> <span data-ttu-id="31c02-502">È possibile, ad esempio, calcolare la media di diverse letture successive prima di inviare il report di ogni metrica.</span><span class="sxs-lookup"><span data-stu-id="31c02-502">For example, you could average several successive readings before sending each metric report.</span></span> <span data-ttu-id="31c02-503">Si calcolerà quindi la deviazione minima, massima e standard e il valore di aggregazione (somma o media) e si imposterà il conteggio sul numero di letture rappresentate dal report.</span><span class="sxs-lookup"><span data-stu-id="31c02-503">Then you would calculate the min, max, standard deviation and aggregate value (sum or average) and set count to the number of readings represented by the report.</span></span>

<span data-ttu-id="31c02-504">Nelle tabelle precedenti sono stati omessi il conteggio dei campi usati raramente, i valori minimo e massimo, stdDev e sampledValue.</span><span class="sxs-lookup"><span data-stu-id="31c02-504">In the tables above, we have omitted the rarely-used fields count, min, max, stdDev and sampledValue.</span></span>

<span data-ttu-id="31c02-505">Se è necessario ridurre il volume della telemetria, anziché aggregare in anticipo la metrica, è possibile usare il [campionamento](app-insights-sampling.md) .</span><span class="sxs-lookup"><span data-stu-id="31c02-505">Instead of pre-aggregating metrics, you can use [sampling](app-insights-sampling.md) if you need to reduce the volume of telemetry.</span></span>

### <a name="durations"></a><span data-ttu-id="31c02-506">Durate</span><span class="sxs-lookup"><span data-stu-id="31c02-506">Durations</span></span>
<span data-ttu-id="31c02-507">Se non indicato diversamente, le durate vengono espresse in decimi di microsecondo, quindi 10000000,0 corrisponde a 1 secondo.</span><span class="sxs-lookup"><span data-stu-id="31c02-507">Except where otherwise noted, durations are represented in tenths of a microsecond, so that 10000000.0 means 1 second.</span></span>

## <a name="see-also"></a><span data-ttu-id="31c02-508">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="31c02-508">See also</span></span>
* [<span data-ttu-id="31c02-509">Application Insights</span><span class="sxs-lookup"><span data-stu-id="31c02-509">Application Insights</span></span>](app-insights-overview.md)
* [<span data-ttu-id="31c02-510">Esportazione continua</span><span class="sxs-lookup"><span data-stu-id="31c02-510">Continuous Export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="31c02-511">Esempi di codice</span><span class="sxs-lookup"><span data-stu-id="31c02-511">Code samples</span></span>](app-insights-export-telemetry.md#code-samples)
