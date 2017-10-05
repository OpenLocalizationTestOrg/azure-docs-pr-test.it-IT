---
title: Inviare eventi a un ambiente di Azure Time Series Insights | Microsoft Docs
description: Questa esercitazione illustra la procedura per effettuare il push degli eventi all'ambiente Time Series Insights
keywords: 
services: tsi
documentationcenter: 
author: venkatgct
manager: jhubbard
editor: 
ms.assetid: 
ms.service: tsi
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: venkatja
ms.openlocfilehash: b4ef96a045393f28b3cd750068fe82a5a8411afa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="send-events-to-a-time-series-insights-environment-using-event-hub"></a><span data-ttu-id="cab11-103">Inviare eventi a un ambiente Time Series Insights tramite un hub eventi</span><span class="sxs-lookup"><span data-stu-id="cab11-103">Send events to a Time Series Insights environment using event hub</span></span>

<span data-ttu-id="cab11-104">Questa esercitazione illustra come creare e configurare un hub eventi ed eseguire un'applicazione di esempio per effettuare il push degli eventi.</span><span class="sxs-lookup"><span data-stu-id="cab11-104">This tutorial explains how to create and configure event hub and run a sample application to push events.</span></span> <span data-ttu-id="cab11-105">Se è presente un hub eventi con eventi in formato JSON, saltare questa esercitazione e visualizzare l'ambiente in [Time Series Insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cab11-105">If you have an existing event hub with events in JSON format, skip this tutorial and view your environment in [time series insights](https://insights.timeseries.azure.com).</span></span>

## <a name="configure-an-event-hub"></a><span data-ttu-id="cab11-106">Configurare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="cab11-106">Configure an event hub</span></span>
1. <span data-ttu-id="cab11-107">Per creare un hub eventi, seguire le istruzioni contenute nella [documentazione](https://docs.microsoft.com/azure/event-hubs/event-hubs-create) sugli hub eventi.</span><span class="sxs-lookup"><span data-stu-id="cab11-107">To create an event hub, follow instructions from the Event Hub [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

2. <span data-ttu-id="cab11-108">Assicurarsi di creare un gruppo di consumer usato esclusivamente dall'origine evento di Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="cab11-108">Make sure you create a consumer group that is used exclusively by your Time Series Insights event source.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="cab11-109">Verificare che questo gruppo di consumer non venga usato da altri servizi, ad esempio un processo di Analisi di flusso o un altro ambiente Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="cab11-109">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="cab11-110">Se il gruppo di consumer viene usato da altri servizi, l'operazione di lettura viene compromessa per questo ambiente e per gli altri servizi.</span><span class="sxs-lookup"><span data-stu-id="cab11-110">If consumer group is used by other services, read operation is negatively affected for this environment and the other services.</span></span> <span data-ttu-id="cab11-111">Se si usa "$Default" come gruppo di consumer, è probabile che venga usato anche da altri lettori.</span><span class="sxs-lookup"><span data-stu-id="cab11-111">If you are using “$Default” as the consumer group, it could lead to potential reuse by other readers.</span></span>

  ![Selezionare il gruppo di consumer dell'hub eventi](media/send-events/consumer-group.png)

3. <span data-ttu-id="cab11-113">Nell'hub eventi creare "MySendPolicy" che viene usato per inviare eventi nell'esempio csharp.</span><span class="sxs-lookup"><span data-stu-id="cab11-113">On the event hub, create “MySendPolicy” that is used to send events in the csharp sample.</span></span>

  ![Selezionare Criteri di accesso condiviso e fare clic sul pulsante Aggiungi](media/send-events/shared-access-policy.png)  

  ![Aggiungere nuovi criteri di accesso condiviso](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a><span data-ttu-id="cab11-116">Creare un'origine evento di Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="cab11-116">Create Time Series Insights event source</span></span>
1. <span data-ttu-id="cab11-117">Se non è ancora stata creata un'origine evento, seguire [queste istruzioni](time-series-insights-add-event-source.md) per crearne una.</span><span class="sxs-lookup"><span data-stu-id="cab11-117">If you haven't created an event source, follow [these instructions](time-series-insights-add-event-source.md) to create an event source.</span></span>

2. <span data-ttu-id="cab11-118">Specificare "deviceTimestamp" come nome della proprietà Timestamp. Questa proprietà viene usata come timestamp effettivo nell'esempio csharp.</span><span class="sxs-lookup"><span data-stu-id="cab11-118">Specify “deviceTimestamp” as the timestamp property name – this property is used as the actual timestamp in the csharp sample.</span></span> <span data-ttu-id="cab11-119">Il nome della proprietà timestamp applica la distinzione tra maiuscole e minuscole e i valori devono avere il formato __aaaa-MM-ggTHH:mm:ss.FFFFFFFK__ quando viene inviato come file JSON all'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="cab11-119">The timestamp property name is case-sensitive and values must follow the format __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ when sent as JSON to event hub.</span></span> <span data-ttu-id="cab11-120">Se la proprietà non esiste nell'evento, verrà usata l'ora in cui l'evento è stato accodato nell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="cab11-120">If the property does not exist in the event, then the event hub enqueued time is used.</span></span>

  ![Creare un'origine evento](media/send-events/event-source-1.png)

## <a name="sample-code-to-push-events"></a><span data-ttu-id="cab11-122">Codice di esempio per effettuare il push degli eventi</span><span class="sxs-lookup"><span data-stu-id="cab11-122">Sample code to push events</span></span>
1. <span data-ttu-id="cab11-123">Passare al criterio dell'hub eventi "MySendPolicy" e copiare la stringa di connessione con la chiave del criterio.</span><span class="sxs-lookup"><span data-stu-id="cab11-123">Go to the event hub policy “MySendPolicy” and copy the connection string with the policy key.</span></span>

  ![Copiare la stringa di connessione MySendPolicy](media/send-events/sample-code-connection-string.png)

2. <span data-ttu-id="cab11-125">Eseguire questo codice per inviare 600 eventi per ognuno dei tre dispositivi.</span><span class="sxs-lookup"><span data-stu-id="cab11-125">Run the following code that to send 600 events per each of the three devices.</span></span> <span data-ttu-id="cab11-126">Aggiornare `eventHubConnectionString` con la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="cab11-126">Update `eventHubConnectionString` with your connection string.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Globalization;
using System.IO;
using Microsoft.ServiceBus.Messaging;

namespace Microsoft.Rdx.DataGenerator
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var from = new DateTime(2017, 4, 20, 15, 0, 0, DateTimeKind.Utc);
            Random r = new Random();
            const int numberOfEvents = 600;

            var deviceIds = new[] { "device1", "device2", "device3" };

            var events = new List<string>();
            for (int i = 0; i < numberOfEvents; ++i)
            {
                for (int device = 0; device < deviceIds.Length; ++device)
                {
                    // Generate event and serialize as JSON object:
                    // { "deviceTimestamp": "utc timestamp", "deviceId": "guid", "value": 123.456 }
                    events.Add(
                        String.Format(
                            CultureInfo.InvariantCulture,
                            @"{{ ""deviceTimestamp"": ""{0}"", ""deviceId"": ""{1}"", ""value"": {2} }}",
                            (from + TimeSpan.FromSeconds(i * 30)).ToString("o"),
                            deviceIds[device],
                            r.NextDouble()));
                }
            }

            // Create event hub connection.
            var eventHubConnectionString = @"Endpoint=sb://...";
            var eventHubClient = EventHubClient.CreateFromConnectionString(eventHubConnectionString);

            using (var ms = new MemoryStream())
            using (var sw = new StreamWriter(ms))
            {
                // Wrap events into JSON array:
                sw.Write("[");
                for (int i = 0; i < events.Count; ++i)
                {
                    if (i > 0)
                    {
                        sw.Write(',');
                    }
                    sw.Write(events[i]);
                }
                sw.Write("]");

                sw.Flush();
                ms.Position = 0;

                // Send JSON to event hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a><span data-ttu-id="cab11-127">Forme JSON supportate</span><span class="sxs-lookup"><span data-stu-id="cab11-127">Supported JSON shapes</span></span>
### <a name="sample-1"></a><span data-ttu-id="cab11-128">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="cab11-128">Sample 1</span></span>

#### <a name="input"></a><span data-ttu-id="cab11-129">Input</span><span class="sxs-lookup"><span data-stu-id="cab11-129">Input</span></span>

<span data-ttu-id="cab11-130">Un oggetto JSON semplice.</span><span class="sxs-lookup"><span data-stu-id="cab11-130">A simple JSON object.</span></span>

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a><span data-ttu-id="cab11-131">Output: 1 evento</span><span class="sxs-lookup"><span data-stu-id="cab11-131">Output - 1 event</span></span>

|<span data-ttu-id="cab11-132">id</span><span class="sxs-lookup"><span data-stu-id="cab11-132">id</span></span>|<span data-ttu-id="cab11-133">timestamp</span><span class="sxs-lookup"><span data-stu-id="cab11-133">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="cab11-134">device1</span><span class="sxs-lookup"><span data-stu-id="cab11-134">device1</span></span>|<span data-ttu-id="cab11-135">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="cab11-135">2016-01-08T01:08:00Z</span></span>|

### <a name="sample-2"></a><span data-ttu-id="cab11-136">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="cab11-136">Sample 2</span></span>

#### <a name="input"></a><span data-ttu-id="cab11-137">Input</span><span class="sxs-lookup"><span data-stu-id="cab11-137">Input</span></span>
<span data-ttu-id="cab11-138">Una matrice JSON con due oggetti JSON.</span><span class="sxs-lookup"><span data-stu-id="cab11-138">A JSON array with two JSON objects.</span></span> <span data-ttu-id="cab11-139">Ogni oggetto JSON verrà convertito in un evento.</span><span class="sxs-lookup"><span data-stu-id="cab11-139">Each JSON object will be converted to an event.</span></span>
```json
[
    {
        "id":"device1",
        "timestamp":"2016-01-08T01:08:00Z"
    },
    {
        "id":"device2",
        "timestamp":"2016-01-17T01:17:00Z"
    }
]
```
#### <a name="output---2-events"></a><span data-ttu-id="cab11-140">Output: 2 eventi</span><span class="sxs-lookup"><span data-stu-id="cab11-140">Output - 2 Events</span></span>

|<span data-ttu-id="cab11-141">id</span><span class="sxs-lookup"><span data-stu-id="cab11-141">id</span></span>|<span data-ttu-id="cab11-142">timestamp</span><span class="sxs-lookup"><span data-stu-id="cab11-142">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="cab11-143">device1</span><span class="sxs-lookup"><span data-stu-id="cab11-143">device1</span></span>|<span data-ttu-id="cab11-144">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="cab11-144">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="cab11-145">device2</span><span class="sxs-lookup"><span data-stu-id="cab11-145">device2</span></span>|<span data-ttu-id="cab11-146">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="cab11-146">2016-01-08T01:17:00Z</span></span>|
### <a name="sample-3"></a><span data-ttu-id="cab11-147">Esempio 3</span><span class="sxs-lookup"><span data-stu-id="cab11-147">Sample 3</span></span>

#### <a name="input"></a><span data-ttu-id="cab11-148">Input</span><span class="sxs-lookup"><span data-stu-id="cab11-148">Input</span></span>

<span data-ttu-id="cab11-149">Un oggetto JSON con una matrice JSON annidata che contiene due oggetti JSON.</span><span class="sxs-lookup"><span data-stu-id="cab11-149">A JSON object with a nested JSON array containing two JSON objects.</span></span>
```json
{
    "location":"WestUs",
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z"
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z"
        }
    ]
}

```
#### <a name="output---2-events"></a><span data-ttu-id="cab11-150">Output: 2 eventi</span><span class="sxs-lookup"><span data-stu-id="cab11-150">Output - 2 Events</span></span>
<span data-ttu-id="cab11-151">Si noti che la proprietà "location" viene copiata in ogni evento.</span><span class="sxs-lookup"><span data-stu-id="cab11-151">Note that the property "location" is copied over to each of the event.</span></span>

|<span data-ttu-id="cab11-152">location</span><span class="sxs-lookup"><span data-stu-id="cab11-152">location</span></span>|<span data-ttu-id="cab11-153">events.id</span><span class="sxs-lookup"><span data-stu-id="cab11-153">events.id</span></span>|<span data-ttu-id="cab11-154">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="cab11-154">events.timestamp</span></span>|
|--------|---------------|----------------------|
|<span data-ttu-id="cab11-155">WestUs</span><span class="sxs-lookup"><span data-stu-id="cab11-155">WestUs</span></span>|<span data-ttu-id="cab11-156">device1</span><span class="sxs-lookup"><span data-stu-id="cab11-156">device1</span></span>|<span data-ttu-id="cab11-157">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="cab11-157">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="cab11-158">WestUs</span><span class="sxs-lookup"><span data-stu-id="cab11-158">WestUs</span></span>|<span data-ttu-id="cab11-159">device2</span><span class="sxs-lookup"><span data-stu-id="cab11-159">device2</span></span>|<span data-ttu-id="cab11-160">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="cab11-160">2016-01-08T01:17:00Z</span></span>|

### <a name="sample-4"></a><span data-ttu-id="cab11-161">Esempio 4</span><span class="sxs-lookup"><span data-stu-id="cab11-161">Sample 4</span></span>

#### <a name="input"></a><span data-ttu-id="cab11-162">Input</span><span class="sxs-lookup"><span data-stu-id="cab11-162">Input</span></span>

<span data-ttu-id="cab11-163">Un oggetto JSON con una matrice JSON annidata che contiene due oggetti JSON.</span><span class="sxs-lookup"><span data-stu-id="cab11-163">A JSON object with a nested JSON array containing two JSON objects.</span></span> <span data-ttu-id="cab11-164">Questo input dimostra che le proprietà globali possono essere rappresentate dall'oggetto JSON complesso.</span><span class="sxs-lookup"><span data-stu-id="cab11-164">This input demonstrates that the global properties may be represented by the complex JSON object.</span></span>

```json
{
    "location":"WestUs",
    "manufacturer":{
        "name":"manufacturer1",
        "location":"EastUs"
    },
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z",
            "data":{
                "type":"pressure",
                "units":"psi",
                "value":108.09
            }
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z",
            "data":{
                "type":"vibration",
                "units":"abs G",
                "value":217.09
            }
        }
    ]
}
```
#### <a name="output---2-events"></a><span data-ttu-id="cab11-165">Output: 2 eventi</span><span class="sxs-lookup"><span data-stu-id="cab11-165">Output - 2 Events</span></span>

|<span data-ttu-id="cab11-166">location</span><span class="sxs-lookup"><span data-stu-id="cab11-166">location</span></span>|<span data-ttu-id="cab11-167">manufacturer.name</span><span class="sxs-lookup"><span data-stu-id="cab11-167">manufacturer.name</span></span>|<span data-ttu-id="cab11-168">manufacturer.location</span><span class="sxs-lookup"><span data-stu-id="cab11-168">manufacturer.location</span></span>|<span data-ttu-id="cab11-169">events.id</span><span class="sxs-lookup"><span data-stu-id="cab11-169">events.id</span></span>|<span data-ttu-id="cab11-170">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="cab11-170">events.timestamp</span></span>|<span data-ttu-id="cab11-171">events.data.type</span><span class="sxs-lookup"><span data-stu-id="cab11-171">events.data.type</span></span>|<span data-ttu-id="cab11-172">events.data.units</span><span class="sxs-lookup"><span data-stu-id="cab11-172">events.data.units</span></span>|<span data-ttu-id="cab11-173">events.data.value</span><span class="sxs-lookup"><span data-stu-id="cab11-173">events.data.value</span></span>|
|---|---|---|---|---|---|---|---|
|<span data-ttu-id="cab11-174">WestUs</span><span class="sxs-lookup"><span data-stu-id="cab11-174">WestUs</span></span>|<span data-ttu-id="cab11-175">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="cab11-175">manufacturer1</span></span>|<span data-ttu-id="cab11-176">EastUs</span><span class="sxs-lookup"><span data-stu-id="cab11-176">EastUs</span></span>|<span data-ttu-id="cab11-177">device1</span><span class="sxs-lookup"><span data-stu-id="cab11-177">device1</span></span>|<span data-ttu-id="cab11-178">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="cab11-178">2016-01-08T01:08:00Z</span></span>|<span data-ttu-id="cab11-179">pressure</span><span class="sxs-lookup"><span data-stu-id="cab11-179">pressure</span></span>|<span data-ttu-id="cab11-180">psi</span><span class="sxs-lookup"><span data-stu-id="cab11-180">psi</span></span>|<span data-ttu-id="cab11-181">108.09</span><span class="sxs-lookup"><span data-stu-id="cab11-181">108.09</span></span>|
|<span data-ttu-id="cab11-182">WestUs</span><span class="sxs-lookup"><span data-stu-id="cab11-182">WestUs</span></span>|<span data-ttu-id="cab11-183">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="cab11-183">manufacturer1</span></span>|<span data-ttu-id="cab11-184">EastUs</span><span class="sxs-lookup"><span data-stu-id="cab11-184">EastUs</span></span>|<span data-ttu-id="cab11-185">device2</span><span class="sxs-lookup"><span data-stu-id="cab11-185">device2</span></span>|<span data-ttu-id="cab11-186">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="cab11-186">2016-01-08T01:17:00Z</span></span>|<span data-ttu-id="cab11-187">vibration</span><span class="sxs-lookup"><span data-stu-id="cab11-187">vibration</span></span>|<span data-ttu-id="cab11-188">abs G</span><span class="sxs-lookup"><span data-stu-id="cab11-188">abs G</span></span>|<span data-ttu-id="cab11-189">217.09</span><span class="sxs-lookup"><span data-stu-id="cab11-189">217.09</span></span>|

## <a name="next-steps"></a><span data-ttu-id="cab11-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cab11-190">Next steps</span></span>

* <span data-ttu-id="cab11-191">Visualizzare l'ambiente nel [portale di Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="cab11-191">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
