---
title: monitoraggio delle operazioni di Hub IoT aaaAzure | Documenti Microsoft
description: Operazioni di IoT Hub Azure toouse monitoraggio toomonitor hello come lo stato delle operazioni l'hub IoT in tempo reale.
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a299f3a5-b14d-4586-9c3b-44aea14ed013
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.openlocfilehash: a0b233ef2d9bd0827e19fa30fdbdd49b2b61b813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-operations-monitoring"></a>Monitoraggio delle operazioni dell'hub IoT

Monitoraggio delle operazioni di IoT Hub consente lo stato di hello toomonitor delle operazioni l'hub IoT in tempo reale. L'hub IoT tiene traccia degli eventi nelle diverse categorie di operazioni. È possibile scegliere di inviare gli eventi da uno o più endpoint tooan categorie dell'hub IoT per l'elaborazione. È possibile controllare i dati di hello per errori o impostare un'elaborazione più complessa basata su modelli di dati.

L'hub IoT monitora sei categorie di eventi:

* Operazioni relative alle identità dei dispositivi
* Telemetria dei dispositivi
* Messaggi da cloud a dispositivo
* Connessioni
* Caricamenti di file
* Routing dei messaggi

## <a name="how-tooenable-operations-monitoring"></a>Il monitoraggio delle operazioni tooenable

1. Creare un hub IoT. È possibile trovare istruzioni su come toocreate un hub IoT in hello [iniziare] [ lnk-get-started] Guida.

1. Aprire il pannello hello dell'hub IoT. Da qui, fare clic su **Monitoraggio operazioni**.

    ![Monitoraggio della configurazione nel portale di hello le operazioni di accesso][1]

1. Seleziona hello categorie desidera toomonitor e quindi fare clic su monitoraggio **salvare**. Hello eventi sono disponibili per la lettura dall'endpoint hello compatibile con Hub eventi elencati in **le impostazioni di monitoraggio**. Hello endpoint IoT Hub è chiamato `messages/operationsmonitoringevents`.

    ![Configurare il monitoraggio delle operazioni sull'hub IoT][2]

> [!NOTE]
> Selezione **Verbose** monitoraggio per hello **connessioni** categoria fa sì che l'IoT Hub toogenerate i messaggi di diagnostica aggiuntivi. Per tutte le altre categorie, hello **Verbose** modifiche alle impostazioni quantità hello informazioni IoT Hub sono inclusi in ogni messaggio di errore.

## <a name="event-categories-and-how-toouse-them"></a>Categorie di eventi e come toouse li

Ogni categoria di monitoraggio delle operazioni tiene traccia di un diverso tipo di interazione con l'hub IoT e ogni categoria di monitoraggio ha uno schema che definisce come sono strutturati gli eventi nella categoria stessa.

### <a name="device-identity-operations"></a>Operazioni relative alle identità dei dispositivi

categoria di operazioni identità dispositivo Hello tiene traccia degli errori che si verificano quando si tenta di toocreate, aggiornare o eliminare una voce nel Registro di sistema dell'hub del IoT identità. Il rilevamento di questa categoria è utile per gli scenari di provisioning.

```json
{
    "time": "UTC timestamp",
        "operationName": "create",
        "category": "DeviceIdentityOperations",
        "level": "Error",
        "statusCode": 4XX,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "durationMs": 1234,
        "userAgent": "userAgent",
        "sharedAccessPolicy": "accessPolicy"
}
```

### <a name="device-telemetry"></a>Telemetria dei dispositivi

categoria di dati di telemetria dispositivi Hello tiene traccia degli errori che si verificano all'hub IoT hello e sono la pipeline di telemetria correlati toohello. Questa categoria include gli errori che si verificano durante l'invio di eventi di telemetria, ad esempio la limitazione, e la ricezione di eventi di telemetria, ad esempio un lettore non autorizzato. Questa categoria non può intercettare gli errori causati da codice in esecuzione sul dispositivo hello stesso.

```json
{
        "messageSizeInBytes": 1234,
        "batching": 0,
        "protocol": "Amqp",
        "authType": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
        "time": "UTC timestamp",
        "operationName": "ingress",
        "category": "DeviceTelemetry",
        "level": "Error",
        "statusCode": 4XX,
        "statusType": 4XX001,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "EventProcessedUtcTime": "UTC timestamp",
        "PartitionId": 1,
        "EventEnqueuedUtcTime": "UTC timestamp"
}
```

### <a name="cloud-to-device-commands"></a>Comandi da cloud a dispositivo

categoria di comandi cloud a dispositivo Hello tiene traccia degli errori che si verificano all'hub IoT hello e sono pipeline messaggio cloud a dispositivo toohello correlati. Questa categoria include gli errori che si verificano durante l'invio di messaggi da cloud a dispositivo, ad esempio un mittente non autorizzato, la ricezione di messaggi da cloud a dispositivo, ad esempio il superamento del numero di recapiti, e la ricezione di commenti sui messaggi da cloud a dispositivo, ad esempio commenti scaduti. Questa categoria non rileva gli errori da un dispositivo che gestisce correttamente un messaggio da cloud a dispositivo se il messaggio hello del cloud a dispositivo è stata inviata correttamente.

```json
{
    "messageSizeInBytes": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "deliveryAcknowledgement": 0,
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "C2DCommands",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "EventProcessedUtcTime": "UTC timestamp",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": “UTC timestamp"
}
```

### <a name="connections"></a>Connessioni

categoria di connessioni Hello tiene traccia degli errori che si verificano quando i dispositivi connettono o Disconnetti da un hub IoT. Il rilevamento di questa categoria è utile per identificare i tentativi di connessione non autorizzati e per rilevare quando una connessione viene persa dai dispositivi in aree di scarsa connettività.

```json
{
    "durationMs": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID"
}
```

### <a name="file-uploads"></a>Caricamenti di file

categoria di caricamento file Hello tiene traccia degli errori che si verificano all'hub IoT hello e sono funzionalità di caricamento toofile correlati. Questa categoria include:

* Errori che si verificano con hello URI SAS, ad esempio quando scade prima che un dispositivo notifica hub hello di un caricamento completato.
* Non è stato possibile caricamenti segnalati dal dispositivo hello.
* Errori che si verificano quando un file non viene trovato nell'archivio durante la creazione del messaggio di notifica dell'hub IoT.

Questa categoria non può intercettare gli errori generati direttamente durante dispositivo hello sta caricando un file toostorage.

```json
{
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "HTTP",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "fileUpload",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "blobUri": "http//bloburi.com",
    "durationMs": 1234
}
```

### <a name="message-routing"></a>Routing dei messaggi

categoria di routing di messaggi Hello tiene traccia degli errori che si verificano durante la valutazione di route di messaggio e l'integrità di endpoint percepita dall'IoT Hub. Questa categoria include gli eventi, ad esempio quando una regola valuta troppo "undefined", quando l'IoT Hub contrassegna un endpoint come inattivi e gli errori ricevuti da un endpoint. Questa categoria non sono inclusi errori specifici relative ai messaggi hello stessi (ad esempio dispositivo errori di limitazione), che vengono segnalati nella categoria "telemetria del dispositivo" hello.

```json
{
    "messageSizeInBytes": 1234,
    "time": "UTC timestamp",
    "operationName": "ingress",
    "category": "routes",
    "level": "Error",
    "deviceId": "device-ID",
    "messageId": "ID of message",
    "routeName": "myroute",
    "endpointName": "myendpoint",
    "details": "ExternalEndpointDisabled"
}
```

## <a name="view-events"></a>Visualizzare eventi

È possibile utilizzare hello *l'hub IOT Esplora* strumento tooquickly verificare che l'hub IoT è la generazione di eventi di monitoraggio. hello tooinstall strumento, vedere le istruzioni hello hello [l'hub IOT Esplora] [ lnk-iothub-explorer] repository GitHub.

1. Verificare che hello **connessioni** monitoraggio categoria viene impostato troppo**Verbose** nel portale di hello.

1. Al prompt di comando, eseguire hello seguenti tooread comando dagli hello dell'endpoint di monitoraggio:

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. In un altro prompt dei comandi, eseguire hello successivo comando toosimulate un dispositivo l'invio di messaggi da dispositivo a cloud:

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. Hello prima della riga di comando Mostra gli eventi di monitoraggio di hello dispositivo simulato hello si connette tooyour hub IoT.

## <a name="connect-toohello-monitoring-endpoint"></a>Connettersi toohello dell'endpoint di monitoraggio

Hello monitoraggio endpoint dell'hub IoT è un endpoint compatibile con Hub eventi. È possibile utilizzare qualsiasi meccanismo che funziona con i messaggi di monitoraggio tooread gli hub di eventi da questo endpoint. Hello esempio seguente crea un lettore di base che non è adatto per una distribuzione di velocità effettiva elevata. Per ulteriori informazioni su come tooprocess messaggi dagli hub eventi, vedere hello [Introduzione agli hub di eventi] [ lnk-eventhubs-tutorial] esercitazione.

endpoint di monitoraggio toohello tooconnect, è necessario un nome di endpoint hello e di stringa di connessione. Hello alla procedura seguente viene mostrato come toofind hello valori necessari nel portale di hello:

1. Nel portale di hello passare tooyour pannello della risorsa IoT Hub.

1. Scegliere **monitoraggio delle operazioni**e prendere nota di hello **nome compatibile con Hub eventi** e **endpoint compatibile con Hub eventi** valori:

    ![Valori di Endpoint compatibile con Hub eventi][img-endpoints]

1. Scegliere **Criteri di accesso condiviso**, quindi scegliere **servizio**. Prendere nota di hello **chiave primaria** valore:

    ![Chiave primaria del servizio dei criteri di accesso condiviso][img-service-key]

Hello seguente esempio di codice c# viene eseguita da Visual Studio **Windows Desktop classico** applicazione console c#. progetto Hello è hello **Windowsazure** installato il pacchetto NuGet.

* Sostituire i segnaposto di stringa di connessione hello con una stringa di connessione che utilizza hello **endpoint compatibile con Hub eventi** e servizio **chiave primaria** sui valori annotati in precedenza, come illustrato nell'esempio hello esempio:

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* Sostituire i segnaposto nome endpoint con hello monitoraggio hello **nome compatibile con Hub eventi** valore annotato in precedenza.

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key tooexit.\n");

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, monitoringEndpointName);
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
        CancellationTokenSource cts = new CancellationTokenSource();
        var tasks = new List<Task>();

        foreach (string partition in d2cPartitions)
        {
            tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }

        Console.ReadLine();
        Console.WriteLine("Exiting...");
        cts.Cancel();
        Task.WaitAll(tasks.ToArray());
    }

    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested)
            {
                await eventHubReceiver.CloseAsync();
                break;
            }

            EventData eventData = await eventHubReceiver.ReceiveAsync(new TimeSpan(0,0,10));

            if (eventData != null)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
    }
}
```

## <a name="next-steps"></a>Passaggi successivi
toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Guida per gli sviluppatori dell'hub IoT][lnk-devguide]
* [Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]

<!-- Links and images -->
[1]: media/iot-hub-operations-monitoring/enable-OM-1.png
[2]: media/iot-hub-operations-monitoring/enable-OM-2.png
[img-endpoints]: media/iot-hub-operations-monitoring/monitoring-endpoint.png
[img-service-key]: media/iot-hub-operations-monitoring/service-key.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-diagnostic-metrics]: iot-hub-metrics.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md