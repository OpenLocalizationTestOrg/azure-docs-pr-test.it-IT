---
title: Monitoraggio delle operazioni dell'hub IoT di Azure | Microsoft Docs
description: Come usare il monitoraggio delle operazioni dell'hub IoT di Azure per monitorare lo stato delle operazioni nell'hub IoT in tempo reale.
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
ms.openlocfilehash: b6de5c5df5f9401a41be152bfa06eb994594e83d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="c5138-103">Monitoraggio delle operazioni dell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="c5138-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="c5138-104">Il monitoraggio delle operazioni dell'hub IoT consente di monitorare lo stato delle operazioni nel proprio hub IoT in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="c5138-104">IoT Hub operations monitoring enables you to monitor the status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="c5138-105">L'hub IoT tiene traccia degli eventi nelle diverse categorie di operazioni.</span><span class="sxs-lookup"><span data-stu-id="c5138-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="c5138-106">È possibile scegliere di impostare l'invio di eventi da una o più categorie a un endpoint del proprio hub IoT per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="c5138-106">You can opt into sending events from one or more categories to an endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="c5138-107">È possibile monitorare i dati per individuare gli errori o configurare un'elaborazione più complessa in base ai modelli di dati.</span><span class="sxs-lookup"><span data-stu-id="c5138-107">You can monitor the data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="c5138-108">L'hub IoT monitora sei categorie di eventi:</span><span class="sxs-lookup"><span data-stu-id="c5138-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="c5138-109">Operazioni relative alle identità dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="c5138-109">Device identity operations</span></span>
* <span data-ttu-id="c5138-110">Telemetria dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="c5138-110">Device telemetry</span></span>
* <span data-ttu-id="c5138-111">Messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="c5138-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="c5138-112">Connessioni</span><span class="sxs-lookup"><span data-stu-id="c5138-112">Connections</span></span>
* <span data-ttu-id="c5138-113">Caricamenti di file</span><span class="sxs-lookup"><span data-stu-id="c5138-113">File uploads</span></span>
* <span data-ttu-id="c5138-114">Routing dei messaggi</span><span class="sxs-lookup"><span data-stu-id="c5138-114">Message routing</span></span>

## <a name="how-to-enable-operations-monitoring"></a><span data-ttu-id="c5138-115">Come abilitare il monitoraggio delle operazioni</span><span class="sxs-lookup"><span data-stu-id="c5138-115">How to enable operations monitoring</span></span>

1. <span data-ttu-id="c5138-116">Creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c5138-116">Create an IoT hub.</span></span> <span data-ttu-id="c5138-117">Le istruzioni sulla creazione di un hub IoT sono disponibili nella [Guida introduttiva][lnk-get-started].</span><span class="sxs-lookup"><span data-stu-id="c5138-117">You can find instructions on how to create an IoT hub in the [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="c5138-118">Aprire il pannello dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c5138-118">Open the blade of your IoT hub.</span></span> <span data-ttu-id="c5138-119">Da qui, fare clic su **Monitoraggio operazioni**.</span><span class="sxs-lookup"><span data-stu-id="c5138-119">From there, click **Operations monitoring**.</span></span>

    ![Accedere alla configurazione del monitoraggio delle operazioni nel portale][1]

1. <span data-ttu-id="c5138-121">Selezionare le categorie di monitoraggio da controllare e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="c5138-121">Select the monitoring categories you wish to monitor, and then click **Save**.</span></span> <span data-ttu-id="c5138-122">Gli eventi sono disponibili per la lettura nell'endpoint compatibile con l'hub eventi elencato in **Impostazioni di monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="c5138-122">The events are available for reading from the Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="c5138-123">L'endpoint dell'hub IoT è chiamato `messages/operationsmonitoringevents`.</span><span class="sxs-lookup"><span data-stu-id="c5138-123">The IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![Configurare il monitoraggio delle operazioni sull'hub IoT][2]

> [!NOTE]
> <span data-ttu-id="c5138-125">La selezione del monitoraggio **Dettagliato** per la categoria **Connessioni** consente all'hub IoT di generare messaggi di diagnostica aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="c5138-125">Selecting **Verbose** monitoring for the **Connections** category causes IoT Hub to generate additional diagnostics messages.</span></span> <span data-ttu-id="c5138-126">Per tutte le altre categorie, l'impostazione **Dettagliato** modifica la quantità di informazioni che l'hub IoT include in ogni messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="c5138-126">For all other categories, the **Verbose** setting changes the quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-to-use-them"></a><span data-ttu-id="c5138-127">Categorie di eventi e modalità d'uso</span><span class="sxs-lookup"><span data-stu-id="c5138-127">Event categories and how to use them</span></span>

<span data-ttu-id="c5138-128">Ogni categoria di monitoraggio delle operazioni tiene traccia di un diverso tipo di interazione con l'hub IoT e ogni categoria di monitoraggio ha uno schema che definisce come sono strutturati gli eventi nella categoria stessa.</span><span class="sxs-lookup"><span data-stu-id="c5138-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="c5138-129">Operazioni relative alle identità dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="c5138-129">Device identity operations</span></span>

<span data-ttu-id="c5138-130">La categoria di operazioni di identità del dispositivo tiene traccia degli errori che si verificano quando si prova a creare, aggiornare o eliminare una voce nel registro delle identità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c5138-130">The device identity operations category tracks errors that occur when you attempt to create, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="c5138-131">Il rilevamento di questa categoria è utile per gli scenari di provisioning.</span><span class="sxs-lookup"><span data-stu-id="c5138-131">Tracking this category is useful for provisioning scenarios.</span></span>

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

### <a name="device-telemetry"></a><span data-ttu-id="c5138-132">Telemetria dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="c5138-132">Device telemetry</span></span>

<span data-ttu-id="c5138-133">La categoria di telemetria dei dispositivi tiene traccia degli errori che si verificano nell'hub IoT e sono correlati alla pipeline di telemetria.</span><span class="sxs-lookup"><span data-stu-id="c5138-133">The device telemetry category tracks errors that occur at the IoT hub and are related to the telemetry pipeline.</span></span> <span data-ttu-id="c5138-134">Questa categoria include gli errori che si verificano durante l'invio di eventi di telemetria, ad esempio la limitazione, e la ricezione di eventi di telemetria, ad esempio un lettore non autorizzato.</span><span class="sxs-lookup"><span data-stu-id="c5138-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="c5138-135">Questa categoria non può intercettare gli errori causati da codice in esecuzione nel dispositivo stesso.</span><span class="sxs-lookup"><span data-stu-id="c5138-135">This category cannot catch errors caused by code running on the device itself.</span></span>

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

### <a name="cloud-to-device-commands"></a><span data-ttu-id="c5138-136">Comandi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="c5138-136">Cloud-to-device commands</span></span>

<span data-ttu-id="c5138-137">La categoria di comandi da cloud a dispositivo tiene traccia degli errori che si verificano nell'hub IoT e sono correlati alla pipeline di messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c5138-137">The cloud-to-device commands category tracks errors that occur at the IoT hub and are related to the cloud-to-device message pipeline.</span></span> <span data-ttu-id="c5138-138">Questa categoria include gli errori che si verificano durante l'invio di messaggi da cloud a dispositivo, ad esempio un mittente non autorizzato, la ricezione di messaggi da cloud a dispositivo, ad esempio il superamento del numero di recapiti, e la ricezione di commenti sui messaggi da cloud a dispositivo, ad esempio commenti scaduti.</span><span class="sxs-lookup"><span data-stu-id="c5138-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="c5138-139">Questa categoria non intercetta gli errori da un dispositivo che gestisce in modo non corretto un messaggio da cloud a dispositivo, se questo è stato recapitato correttamente.</span><span class="sxs-lookup"><span data-stu-id="c5138-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if the cloud-to-device message was delivered successfully.</span></span>

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

### <a name="connections"></a><span data-ttu-id="c5138-140">Connessioni</span><span class="sxs-lookup"><span data-stu-id="c5138-140">Connections</span></span>

<span data-ttu-id="c5138-141">La categoria Connessioni tiene traccia degli errori che si verificano quando i dispositivi si connettono o disconnettono da un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c5138-141">The connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="c5138-142">Il rilevamento di questa categoria è utile per identificare i tentativi di connessione non autorizzati e per rilevare quando una connessione viene persa dai dispositivi in aree di scarsa connettività.</span><span class="sxs-lookup"><span data-stu-id="c5138-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

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

### <a name="file-uploads"></a><span data-ttu-id="c5138-143">Caricamenti di file</span><span class="sxs-lookup"><span data-stu-id="c5138-143">File uploads</span></span>

<span data-ttu-id="c5138-144">La categoria di caricamenti dei file tiene traccia degli errori che si verificano nell'hub IoT e correlati alla funzionalità di caricamento dei file.</span><span class="sxs-lookup"><span data-stu-id="c5138-144">The file upload category tracks errors that occur at the IoT hub and are related to file upload functionality.</span></span> <span data-ttu-id="c5138-145">Questa categoria include:</span><span class="sxs-lookup"><span data-stu-id="c5138-145">This category includes:</span></span>

* <span data-ttu-id="c5138-146">Errori che si verificano con l'URI di firma di accesso condiviso, ad esempio quando l'URI scade prima che un dispositivo notifichi all'hub un caricamento completato.</span><span class="sxs-lookup"><span data-stu-id="c5138-146">Errors that occur with the SAS URI, such as when it expires before a device notifies the hub of a completed upload.</span></span>
* <span data-ttu-id="c5138-147">Caricamenti non riusciti segnalati dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c5138-147">Failed uploads reported by the device.</span></span>
* <span data-ttu-id="c5138-148">Errori che si verificano quando un file non viene trovato nell'archivio durante la creazione del messaggio di notifica dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c5138-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="c5138-149">Questa categoria non può intercettare errori che si verificano direttamente mentre il dispositivo sta caricando un file in memoria.</span><span class="sxs-lookup"><span data-stu-id="c5138-149">This category cannot catch errors that directly occur while the device is uploading a file to storage.</span></span>

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

### <a name="message-routing"></a><span data-ttu-id="c5138-150">Routing dei messaggi</span><span class="sxs-lookup"><span data-stu-id="c5138-150">Message routing</span></span>

<span data-ttu-id="c5138-151">La categoria del routing dei messaggi tiene traccia degli errori che si verificano durante la valutazione del routing dei messaggi e dell'integrità dell'endpoint percepiti dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c5138-151">The message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="c5138-152">Questa categoria include eventi come ad esempio quando una regola viene valutata come "non definita", quando l'hub IoT contrassegna un endpoint come inattivo ed eventuali altri errori ricevuti da un endpoint.</span><span class="sxs-lookup"><span data-stu-id="c5138-152">This category includes events such as when a rule evaluates to "undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="c5138-153">Questa categoria non include errori specifici sui messaggi stessi, ad esempio gli errori di limitazione sui dispositivi, che vengono segnalati nella categoria "telemetria del dispositivo".</span><span class="sxs-lookup"><span data-stu-id="c5138-153">This category does not include specific errors about the messages themselves (such as device throttling errors), which are reported under the "device telemetry" category.</span></span>

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

## <a name="view-events"></a><span data-ttu-id="c5138-154">Visualizzare eventi</span><span class="sxs-lookup"><span data-stu-id="c5138-154">View events</span></span>

<span data-ttu-id="c5138-155">È possibile usare lo strumento *iothub-explorer* per verificare rapidamente che l'hub IoT stia generando eventi di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="c5138-155">You can use the *iothub-explorer* tool to quickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="c5138-156">Per installare lo strumento, vedere le istruzioni disponibili nel repository GitHub [iothub-explorer][lnk-iothub-explorer].</span><span class="sxs-lookup"><span data-stu-id="c5138-156">To install the tool, see the instructions in the [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="c5138-157">Assicurarsi che la categoria di monitoraggio **Connessioni** sia impostata su **Dettagliato** nel portale.</span><span class="sxs-lookup"><span data-stu-id="c5138-157">Make sure the **Connections** monitoring category is set to **Verbose** in the portal.</span></span>

1. <span data-ttu-id="c5138-158">Al prompt dei comandi eseguire il comando seguente per consentire la lettura dell'endpoint di monitoraggio:</span><span class="sxs-lookup"><span data-stu-id="c5138-158">At a command-prompt, run the following command to read from the monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="c5138-159">A un altro prompt dei comandi eseguire il comando seguente per simulare un dispositivo che invia messaggi da dispositivo a cloud:</span><span class="sxs-lookup"><span data-stu-id="c5138-159">In another command-prompt, run the following command to simulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="c5138-160">Il primo prompt dei comandi visualizza gli eventi di monitoraggio nel momento in cui il dispositivo simulato si connette all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c5138-160">The first command-prompt shows the monitoring events as the simulated device connects to your IoT hub.</span></span>

## <a name="connect-to-the-monitoring-endpoint"></a><span data-ttu-id="c5138-161">Connettersi all'endpoint di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="c5138-161">Connect to the monitoring endpoint</span></span>

<span data-ttu-id="c5138-162">L'endpoint di monitoraggio sull'hub IoT è un endpoint compatibile con Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c5138-162">The monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="c5138-163">Per leggere i messaggi di monitoraggio da questo endpoint, è possibile usare qualsiasi meccanismo che funzioni con l'Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="c5138-163">You can use any mechanism that works with Event Hubs to read monitoring messages from this endpoint.</span></span> <span data-ttu-id="c5138-164">L'esempio seguente crea un lettore di base non adatto per una distribuzione con velocità effettiva elevata.</span><span class="sxs-lookup"><span data-stu-id="c5138-164">The following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="c5138-165">Per altre informazioni su come elaborare i messaggi da Hub eventi, vedere l'esercitazione [Introduzione all'Hub eventi][lnk-eventhubs-tutorial].</span><span class="sxs-lookup"><span data-stu-id="c5138-165">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="c5138-166">Per connettersi all'endpoint di monitoraggio, è necessaria una stringa di connessione e il nome dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="c5138-166">To connect to the monitoring endpoint, you need a connection string and the endpoint name.</span></span> <span data-ttu-id="c5138-167">La procedura seguente mostra come trovare i valori necessari nel portale:</span><span class="sxs-lookup"><span data-stu-id="c5138-167">The following steps show you how to find the necessary values in the portal:</span></span>

1. <span data-ttu-id="c5138-168">Nel portale, passare al pannello di risorse dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c5138-168">In the portal, navigate to your IoT Hub resource blade.</span></span>

1. <span data-ttu-id="c5138-169">Scegliere **Monitoraggio operazioni** e prendere nota dei valori in **Nome compatibile con Hub eventi** e in **Endpoint compatibile con Hub eventi**:</span><span class="sxs-lookup"><span data-stu-id="c5138-169">Choose **Operations monitoring**, and make a note of the **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![Valori di Endpoint compatibile con Hub eventi][img-endpoints]

1. <span data-ttu-id="c5138-171">Scegliere **Criteri di accesso condiviso**, quindi scegliere **servizio**.</span><span class="sxs-lookup"><span data-stu-id="c5138-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="c5138-172">Prendere nota del valore presente in **Chiave primaria**:</span><span class="sxs-lookup"><span data-stu-id="c5138-172">Make a note of the **Primary key** value:</span></span>

    ![Chiave primaria del servizio dei criteri di accesso condiviso][img-service-key]

<span data-ttu-id="c5138-174">L'esempio di codice C# seguente viene preso da un'app console C# per **Desktop classico di Windows** di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c5138-174">The following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="c5138-175">Il progetto ha il pacchetto **WindowsAzure.ServiceBus** NuGet installato.</span><span class="sxs-lookup"><span data-stu-id="c5138-175">The project has the **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="c5138-176">Sostituire il placeholder della stringa di connessione con una stringa di connessione che usa i valori precedentemente annotati per l'**endpoint compatibile con Hub eventi** e il servizio **Chiave primaria** come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c5138-176">Replace the connection string placeholder with a connection string that uses the **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in the following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="c5138-177">Sostituire il placeholder del nome dell'endpoint di monitoraggio con il valore del **nome Hub eventi compatibile** annotato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c5138-177">Replace the monitoring endpoint name placeholder with the **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key to exit.\n");

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

## <a name="next-steps"></a><span data-ttu-id="c5138-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c5138-178">Next steps</span></span>
<span data-ttu-id="c5138-179">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="c5138-179">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="c5138-180">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="c5138-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="c5138-181">[Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="c5138-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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