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
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a>Ambiente di tempo serie Insights tooa di eventi tramite hub di eventi di trasmissione

In questa esercitazione viene illustrato come toocreate e configurare hub eventi e di eseguire un toopush di applicazione di esempio gli eventi. Se è presente un hub eventi con eventi in formato JSON, saltare questa esercitazione e visualizzare l'ambiente in [Time Series Insights](https://insights.timeseries.azure.com).

## <a name="configure-an-event-hub"></a>Configurare un hub eventi
1. toocreate un hub di eventi, seguire le istruzioni da hello Hub eventi [documentazione](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).

2. Assicurarsi di creare un gruppo di consumer usato esclusivamente dall'origine evento di Time Series Insights.

  > [!IMPORTANT]
  > Verificare che questo gruppo di consumer non venga usato da altri servizi, ad esempio un processo di Analisi di flusso o un altro ambiente Time Series Insights. Se il gruppo di consumer viene utilizzato da altri servizi, leggere influisce negativamente l'operazione per questo ambiente e hello altri servizi. Se si utilizza "$Default" come gruppo di consumer hello, può causare il riutilizzo toopotential dagli altri reader.

  ![Selezionare il gruppo di consumer dell'hub eventi](media/send-events/consumer-group.png)

3. Nell'hub di eventi hello, creare "MySendPolicy" toosend utilizzati gli eventi nell'esempio di hello csharp.

  ![Selezionare Criteri di accesso condiviso e fare clic sul pulsante Aggiungi](media/send-events/shared-access-policy.png)  

  ![Aggiungere nuovi criteri di accesso condiviso](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a>Creare un'origine evento di Time Series Insights
1. Se è stata creata un'origine evento, seguire [queste istruzioni](time-series-insights-add-event-source.md) toocreate un'origine evento.

2. Specificare "deviceTimestamp" come nome della proprietà timestamp hello: questa proprietà viene utilizzata come hello effettivo timestamp: esempio hello csharp. nome della proprietà timestamp Hello è tra maiuscole e minuscole e i valori devono essere conformi formato hello __AAAA-MM-ggTHH. FFFFFFFK__ quando inviato come hub tooevent JSON. Se la proprietà hello non esiste nell'evento hello, quindi hello tempo di Accodamento di hub eventi viene utilizzato.

  ![Creare un'origine evento](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a>Eventi toopush codice di esempio
1. Passare a criteri di hub eventi toohello "MySendPolicy" e copiare la stringa di connessione hello con chiave dei criteri di hello.

  ![Copiare la stringa di connessione MySendPolicy](media/send-events/sample-code-connection-string.png)

2. Eseguire hello seguente codice per ciascuna delle periferiche hello e tre gli eventi toosend 600. Aggiornare `eventHubConnectionString` con la stringa di connessione.

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
## <a name="supported-json-shapes"></a>Forme JSON supportate
### <a name="sample-1"></a>Esempio 1

#### <a name="input"></a>Input

Un oggetto JSON semplice.

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a>Output: 1 evento

|id|timestamp|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|

### <a name="sample-2"></a>Esempio 2

#### <a name="input"></a>Input
Una matrice JSON con due oggetti JSON. Ogni oggetto JSON sarà convertito tooan evento.
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
#### <a name="output---2-events"></a>Output: 2 eventi

|id|timestamp|
|--------|---------------|
|device1|2016-01-08T01:08:00Z|
|device2|2016-01-08T01:17:00Z|
### <a name="sample-3"></a>Esempio 3

#### <a name="input"></a>Input

Un oggetto JSON con una matrice JSON annidata che contiene due oggetti JSON.
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
#### <a name="output---2-events"></a>Output: 2 eventi
Si noti che la proprietà hello "location" viene copiata tooeach dell'evento hello.

|location|events.id|events.timestamp|
|--------|---------------|----------------------|
|WestUs|device1|2016-01-08T01:08:00Z|
|WestUs|device2|2016-01-08T01:17:00Z|

### <a name="sample-4"></a>Esempio 4

#### <a name="input"></a>Input

Un oggetto JSON con una matrice JSON annidata che contiene due oggetti JSON. Questo input viene illustrato che le proprietà globali hello possono essere rappresentate dall'oggetto JSON complesso hello.

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
#### <a name="output---2-events"></a>Output: 2 eventi

|location|manufacturer.name|manufacturer.location|events.id|events.timestamp|events.data.type|events.data.units|events.data.value|
|---|---|---|---|---|---|---|---|
|WestUs|manufacturer1|EastUs|device1|2016-01-08T01:08:00Z|pressure|psi|108.09|
|WestUs|manufacturer1|EastUs|device2|2016-01-08T01:17:00Z|vibration|abs G|217.09|

## <a name="next-steps"></a>Passaggi successivi

* Visualizzare l'ambiente nel [portale di Time Series Insights](https://insights.timeseries.azure.com)
