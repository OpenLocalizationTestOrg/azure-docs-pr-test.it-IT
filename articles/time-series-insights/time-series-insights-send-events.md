---
title: ambiente di tempo serie Insights aaaSend eventi tooAzure | Documenti Microsoft
description: Questa esercitazione sono trattati ambiente ora serie Insights di hello passaggi toopush eventi tooyour
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
ms.openlocfilehash: dbccc23f61351a0033cd48c1a02fb3841b45d560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a><span data-ttu-id="7f405-103">Ambiente di tempo serie Insights tooa di eventi tramite hub di eventi di trasmissione</span><span class="sxs-lookup"><span data-stu-id="7f405-103">Send events tooa Time Series Insights environment using event hub</span></span>

<span data-ttu-id="7f405-104">In questa esercitazione viene illustrato come toocreate e configurare hub eventi e di eseguire un toopush di applicazione di esempio gli eventi.</span><span class="sxs-lookup"><span data-stu-id="7f405-104">This tutorial explains how toocreate and configure event hub and run a sample application toopush events.</span></span> <span data-ttu-id="7f405-105">Se è presente un hub eventi con eventi in formato JSON, saltare questa esercitazione e visualizzare l'ambiente in [Time Series Insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7f405-105">If you have an existing event hub with events in JSON format, skip this tutorial and view your environment in [time series insights](https://insights.timeseries.azure.com).</span></span>

## <a name="configure-an-event-hub"></a><span data-ttu-id="7f405-106">Configurare un hub eventi</span><span class="sxs-lookup"><span data-stu-id="7f405-106">Configure an event hub</span></span>
1. <span data-ttu-id="7f405-107">toocreate un hub di eventi, seguire le istruzioni da hello Hub eventi [documentazione](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span><span class="sxs-lookup"><span data-stu-id="7f405-107">toocreate an event hub, follow instructions from hello Event Hub [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

2. <span data-ttu-id="7f405-108">Assicurarsi di creare un gruppo di consumer usato esclusivamente dall'origine evento di Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="7f405-108">Make sure you create a consumer group that is used exclusively by your Time Series Insights event source.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7f405-109">Verificare che questo gruppo di consumer non venga usato da altri servizi, ad esempio un processo di Analisi di flusso o un altro ambiente Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="7f405-109">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="7f405-110">Se il gruppo di consumer viene utilizzato da altri servizi, leggere influisce negativamente l'operazione per questo ambiente e hello altri servizi.</span><span class="sxs-lookup"><span data-stu-id="7f405-110">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="7f405-111">Se si utilizza "$Default" come gruppo di consumer hello, può causare il riutilizzo toopotential dagli altri reader.</span><span class="sxs-lookup"><span data-stu-id="7f405-111">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

  ![Selezionare il gruppo di consumer dell'hub eventi](media/send-events/consumer-group.png)

3. <span data-ttu-id="7f405-113">Nell'hub di eventi hello, creare "MySendPolicy" toosend utilizzati gli eventi nell'esempio di hello csharp.</span><span class="sxs-lookup"><span data-stu-id="7f405-113">On hello event hub, create “MySendPolicy” that is used toosend events in hello csharp sample.</span></span>

  ![Selezionare Criteri di accesso condiviso e fare clic sul pulsante Aggiungi](media/send-events/shared-access-policy.png)  

  ![Aggiungere nuovi criteri di accesso condiviso](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a><span data-ttu-id="7f405-116">Creare un'origine evento di Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="7f405-116">Create Time Series Insights event source</span></span>
1. <span data-ttu-id="7f405-117">Se è stata creata un'origine evento, seguire [queste istruzioni](time-series-insights-add-event-source.md) toocreate un'origine evento.</span><span class="sxs-lookup"><span data-stu-id="7f405-117">If you haven't created an event source, follow [these instructions](time-series-insights-add-event-source.md) toocreate an event source.</span></span>

2. <span data-ttu-id="7f405-118">Specificare "deviceTimestamp" come nome della proprietà timestamp hello: questa proprietà viene utilizzata come hello effettivo timestamp: esempio hello csharp.</span><span class="sxs-lookup"><span data-stu-id="7f405-118">Specify “deviceTimestamp” as hello timestamp property name – this property is used as hello actual timestamp in hello csharp sample.</span></span> <span data-ttu-id="7f405-119">nome della proprietà timestamp Hello è tra maiuscole e minuscole e i valori devono essere conformi formato hello __AAAA-MM-ggTHH. FFFFFFFK__ quando inviato come hub tooevent JSON.</span><span class="sxs-lookup"><span data-stu-id="7f405-119">hello timestamp property name is case-sensitive and values must follow hello format __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ when sent as JSON tooevent hub.</span></span> <span data-ttu-id="7f405-120">Se la proprietà hello non esiste nell'evento hello, quindi hello tempo di Accodamento di hub eventi viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="7f405-120">If hello property does not exist in hello event, then hello event hub enqueued time is used.</span></span>

  ![Creare un'origine evento](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a><span data-ttu-id="7f405-122">Eventi toopush codice di esempio</span><span class="sxs-lookup"><span data-stu-id="7f405-122">Sample code toopush events</span></span>
1. <span data-ttu-id="7f405-123">Passare a criteri di hub eventi toohello "MySendPolicy" e copiare la stringa di connessione hello con chiave dei criteri di hello.</span><span class="sxs-lookup"><span data-stu-id="7f405-123">Go toohello event hub policy “MySendPolicy” and copy hello connection string with hello policy key.</span></span>

  ![Copiare la stringa di connessione MySendPolicy](media/send-events/sample-code-connection-string.png)

2. <span data-ttu-id="7f405-125">Eseguire hello seguente codice per ciascuna delle periferiche hello e tre gli eventi toosend 600.</span><span class="sxs-lookup"><span data-stu-id="7f405-125">Run hello following code that toosend 600 events per each of hello three devices.</span></span> <span data-ttu-id="7f405-126">Aggiornare `eventHubConnectionString` con la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="7f405-126">Update `eventHubConnectionString` with your connection string.</span></span>

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

                // Send JSON tooevent hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a><span data-ttu-id="7f405-127">Forme JSON supportate</span><span class="sxs-lookup"><span data-stu-id="7f405-127">Supported JSON shapes</span></span>
### <a name="sample-1"></a><span data-ttu-id="7f405-128">Esempio 1</span><span class="sxs-lookup"><span data-stu-id="7f405-128">Sample 1</span></span>

#### <a name="input"></a><span data-ttu-id="7f405-129">Input</span><span class="sxs-lookup"><span data-stu-id="7f405-129">Input</span></span>

<span data-ttu-id="7f405-130">Un oggetto JSON semplice.</span><span class="sxs-lookup"><span data-stu-id="7f405-130">A simple JSON object.</span></span>

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a><span data-ttu-id="7f405-131">Output: 1 evento</span><span class="sxs-lookup"><span data-stu-id="7f405-131">Output - 1 event</span></span>

|<span data-ttu-id="7f405-132">id</span><span class="sxs-lookup"><span data-stu-id="7f405-132">id</span></span>|<span data-ttu-id="7f405-133">timestamp</span><span class="sxs-lookup"><span data-stu-id="7f405-133">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="7f405-134">device1</span><span class="sxs-lookup"><span data-stu-id="7f405-134">device1</span></span>|<span data-ttu-id="7f405-135">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="7f405-135">2016-01-08T01:08:00Z</span></span>|

### <a name="sample-2"></a><span data-ttu-id="7f405-136">Esempio 2</span><span class="sxs-lookup"><span data-stu-id="7f405-136">Sample 2</span></span>

#### <a name="input"></a><span data-ttu-id="7f405-137">Input</span><span class="sxs-lookup"><span data-stu-id="7f405-137">Input</span></span>
<span data-ttu-id="7f405-138">Una matrice JSON con due oggetti JSON.</span><span class="sxs-lookup"><span data-stu-id="7f405-138">A JSON array with two JSON objects.</span></span> <span data-ttu-id="7f405-139">Ogni oggetto JSON sarà convertito tooan evento.</span><span class="sxs-lookup"><span data-stu-id="7f405-139">Each JSON object will be converted tooan event.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="7f405-140">Output: 2 eventi</span><span class="sxs-lookup"><span data-stu-id="7f405-140">Output - 2 Events</span></span>

|<span data-ttu-id="7f405-141">id</span><span class="sxs-lookup"><span data-stu-id="7f405-141">id</span></span>|<span data-ttu-id="7f405-142">timestamp</span><span class="sxs-lookup"><span data-stu-id="7f405-142">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="7f405-143">device1</span><span class="sxs-lookup"><span data-stu-id="7f405-143">device1</span></span>|<span data-ttu-id="7f405-144">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="7f405-144">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="7f405-145">device2</span><span class="sxs-lookup"><span data-stu-id="7f405-145">device2</span></span>|<span data-ttu-id="7f405-146">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="7f405-146">2016-01-08T01:17:00Z</span></span>|
### <a name="sample-3"></a><span data-ttu-id="7f405-147">Esempio 3</span><span class="sxs-lookup"><span data-stu-id="7f405-147">Sample 3</span></span>

#### <a name="input"></a><span data-ttu-id="7f405-148">Input</span><span class="sxs-lookup"><span data-stu-id="7f405-148">Input</span></span>

<span data-ttu-id="7f405-149">Un oggetto JSON con una matrice JSON annidata che contiene due oggetti JSON.</span><span class="sxs-lookup"><span data-stu-id="7f405-149">A JSON object with a nested JSON array containing two JSON objects.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="7f405-150">Output: 2 eventi</span><span class="sxs-lookup"><span data-stu-id="7f405-150">Output - 2 Events</span></span>
<span data-ttu-id="7f405-151">Si noti che la proprietà hello "location" viene copiata tooeach dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="7f405-151">Note that hello property "location" is copied over tooeach of hello event.</span></span>

|<span data-ttu-id="7f405-152">location</span><span class="sxs-lookup"><span data-stu-id="7f405-152">location</span></span>|<span data-ttu-id="7f405-153">events.id</span><span class="sxs-lookup"><span data-stu-id="7f405-153">events.id</span></span>|<span data-ttu-id="7f405-154">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="7f405-154">events.timestamp</span></span>|
|--------|---------------|----------------------|
|<span data-ttu-id="7f405-155">WestUs</span><span class="sxs-lookup"><span data-stu-id="7f405-155">WestUs</span></span>|<span data-ttu-id="7f405-156">device1</span><span class="sxs-lookup"><span data-stu-id="7f405-156">device1</span></span>|<span data-ttu-id="7f405-157">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="7f405-157">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="7f405-158">WestUs</span><span class="sxs-lookup"><span data-stu-id="7f405-158">WestUs</span></span>|<span data-ttu-id="7f405-159">device2</span><span class="sxs-lookup"><span data-stu-id="7f405-159">device2</span></span>|<span data-ttu-id="7f405-160">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="7f405-160">2016-01-08T01:17:00Z</span></span>|

### <a name="sample-4"></a><span data-ttu-id="7f405-161">Esempio 4</span><span class="sxs-lookup"><span data-stu-id="7f405-161">Sample 4</span></span>

#### <a name="input"></a><span data-ttu-id="7f405-162">Input</span><span class="sxs-lookup"><span data-stu-id="7f405-162">Input</span></span>

<span data-ttu-id="7f405-163">Un oggetto JSON con una matrice JSON annidata che contiene due oggetti JSON.</span><span class="sxs-lookup"><span data-stu-id="7f405-163">A JSON object with a nested JSON array containing two JSON objects.</span></span> <span data-ttu-id="7f405-164">Questo input viene illustrato che le proprietà globali hello possono essere rappresentate dall'oggetto JSON complesso hello.</span><span class="sxs-lookup"><span data-stu-id="7f405-164">This input demonstrates that hello global properties may be represented by hello complex JSON object.</span></span>

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
#### <a name="output---2-events"></a><span data-ttu-id="7f405-165">Output: 2 eventi</span><span class="sxs-lookup"><span data-stu-id="7f405-165">Output - 2 Events</span></span>

|<span data-ttu-id="7f405-166">location</span><span class="sxs-lookup"><span data-stu-id="7f405-166">location</span></span>|<span data-ttu-id="7f405-167">manufacturer.name</span><span class="sxs-lookup"><span data-stu-id="7f405-167">manufacturer.name</span></span>|<span data-ttu-id="7f405-168">manufacturer.location</span><span class="sxs-lookup"><span data-stu-id="7f405-168">manufacturer.location</span></span>|<span data-ttu-id="7f405-169">events.id</span><span class="sxs-lookup"><span data-stu-id="7f405-169">events.id</span></span>|<span data-ttu-id="7f405-170">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="7f405-170">events.timestamp</span></span>|<span data-ttu-id="7f405-171">events.data.type</span><span class="sxs-lookup"><span data-stu-id="7f405-171">events.data.type</span></span>|<span data-ttu-id="7f405-172">events.data.units</span><span class="sxs-lookup"><span data-stu-id="7f405-172">events.data.units</span></span>|<span data-ttu-id="7f405-173">events.data.value</span><span class="sxs-lookup"><span data-stu-id="7f405-173">events.data.value</span></span>|
|---|---|---|---|---|---|---|---|
|<span data-ttu-id="7f405-174">WestUs</span><span class="sxs-lookup"><span data-stu-id="7f405-174">WestUs</span></span>|<span data-ttu-id="7f405-175">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="7f405-175">manufacturer1</span></span>|<span data-ttu-id="7f405-176">EastUs</span><span class="sxs-lookup"><span data-stu-id="7f405-176">EastUs</span></span>|<span data-ttu-id="7f405-177">device1</span><span class="sxs-lookup"><span data-stu-id="7f405-177">device1</span></span>|<span data-ttu-id="7f405-178">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="7f405-178">2016-01-08T01:08:00Z</span></span>|<span data-ttu-id="7f405-179">pressure</span><span class="sxs-lookup"><span data-stu-id="7f405-179">pressure</span></span>|<span data-ttu-id="7f405-180">psi</span><span class="sxs-lookup"><span data-stu-id="7f405-180">psi</span></span>|<span data-ttu-id="7f405-181">108.09</span><span class="sxs-lookup"><span data-stu-id="7f405-181">108.09</span></span>|
|<span data-ttu-id="7f405-182">WestUs</span><span class="sxs-lookup"><span data-stu-id="7f405-182">WestUs</span></span>|<span data-ttu-id="7f405-183">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="7f405-183">manufacturer1</span></span>|<span data-ttu-id="7f405-184">EastUs</span><span class="sxs-lookup"><span data-stu-id="7f405-184">EastUs</span></span>|<span data-ttu-id="7f405-185">device2</span><span class="sxs-lookup"><span data-stu-id="7f405-185">device2</span></span>|<span data-ttu-id="7f405-186">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="7f405-186">2016-01-08T01:17:00Z</span></span>|<span data-ttu-id="7f405-187">vibration</span><span class="sxs-lookup"><span data-stu-id="7f405-187">vibration</span></span>|<span data-ttu-id="7f405-188">abs G</span><span class="sxs-lookup"><span data-stu-id="7f405-188">abs G</span></span>|<span data-ttu-id="7f405-189">217.09</span><span class="sxs-lookup"><span data-stu-id="7f405-189">217.09</span></span>|

## <a name="next-steps"></a><span data-ttu-id="7f405-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7f405-190">Next steps</span></span>

* <span data-ttu-id="7f405-191">Visualizzare l'ambiente nel [portale di Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="7f405-191">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
