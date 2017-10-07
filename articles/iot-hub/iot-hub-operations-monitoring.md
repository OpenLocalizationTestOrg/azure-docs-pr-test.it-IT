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
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="12b6a-103">Monitoraggio delle operazioni dell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="12b6a-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="12b6a-104">Monitoraggio delle operazioni di IoT Hub consente lo stato di hello toomonitor delle operazioni l'hub IoT in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="12b6a-104">IoT Hub operations monitoring enables you toomonitor hello status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="12b6a-105">L'hub IoT tiene traccia degli eventi nelle diverse categorie di operazioni.</span><span class="sxs-lookup"><span data-stu-id="12b6a-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="12b6a-106">È possibile scegliere di inviare gli eventi da uno o più endpoint tooan categorie dell'hub IoT per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="12b6a-106">You can opt into sending events from one or more categories tooan endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="12b6a-107">È possibile controllare i dati di hello per errori o impostare un'elaborazione più complessa basata su modelli di dati.</span><span class="sxs-lookup"><span data-stu-id="12b6a-107">You can monitor hello data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="12b6a-108">L'hub IoT monitora sei categorie di eventi:</span><span class="sxs-lookup"><span data-stu-id="12b6a-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="12b6a-109">Operazioni relative alle identità dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="12b6a-109">Device identity operations</span></span>
* <span data-ttu-id="12b6a-110">Telemetria dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="12b6a-110">Device telemetry</span></span>
* <span data-ttu-id="12b6a-111">Messaggi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="12b6a-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="12b6a-112">Connessioni</span><span class="sxs-lookup"><span data-stu-id="12b6a-112">Connections</span></span>
* <span data-ttu-id="12b6a-113">Caricamenti di file</span><span class="sxs-lookup"><span data-stu-id="12b6a-113">File uploads</span></span>
* <span data-ttu-id="12b6a-114">Routing dei messaggi</span><span class="sxs-lookup"><span data-stu-id="12b6a-114">Message routing</span></span>

## <a name="how-tooenable-operations-monitoring"></a><span data-ttu-id="12b6a-115">Il monitoraggio delle operazioni tooenable</span><span class="sxs-lookup"><span data-stu-id="12b6a-115">How tooenable operations monitoring</span></span>

1. <span data-ttu-id="12b6a-116">Creare un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="12b6a-116">Create an IoT hub.</span></span> <span data-ttu-id="12b6a-117">È possibile trovare istruzioni su come toocreate un hub IoT in hello [iniziare] [ lnk-get-started] Guida.</span><span class="sxs-lookup"><span data-stu-id="12b6a-117">You can find instructions on how toocreate an IoT hub in hello [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="12b6a-118">Aprire il pannello hello dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="12b6a-118">Open hello blade of your IoT hub.</span></span> <span data-ttu-id="12b6a-119">Da qui, fare clic su **Monitoraggio operazioni**.</span><span class="sxs-lookup"><span data-stu-id="12b6a-119">From there, click **Operations monitoring**.</span></span>

    ![Monitoraggio della configurazione nel portale di hello le operazioni di accesso][1]

1. <span data-ttu-id="12b6a-121">Seleziona hello categorie desidera toomonitor e quindi fare clic su monitoraggio **salvare**.</span><span class="sxs-lookup"><span data-stu-id="12b6a-121">Select hello monitoring categories you wish toomonitor, and then click **Save**.</span></span> <span data-ttu-id="12b6a-122">Hello eventi sono disponibili per la lettura dall'endpoint hello compatibile con Hub eventi elencati in **le impostazioni di monitoraggio**.</span><span class="sxs-lookup"><span data-stu-id="12b6a-122">hello events are available for reading from hello Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="12b6a-123">Hello endpoint IoT Hub è chiamato `messages/operationsmonitoringevents`.</span><span class="sxs-lookup"><span data-stu-id="12b6a-123">hello IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![Configurare il monitoraggio delle operazioni sull'hub IoT][2]

> [!NOTE]
> <span data-ttu-id="12b6a-125">Selezione **Verbose** monitoraggio per hello **connessioni** categoria fa sì che l'IoT Hub toogenerate i messaggi di diagnostica aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="12b6a-125">Selecting **Verbose** monitoring for hello **Connections** category causes IoT Hub toogenerate additional diagnostics messages.</span></span> <span data-ttu-id="12b6a-126">Per tutte le altre categorie, hello **Verbose** modifiche alle impostazioni quantità hello informazioni IoT Hub sono inclusi in ogni messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="12b6a-126">For all other categories, hello **Verbose** setting changes hello quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-toouse-them"></a><span data-ttu-id="12b6a-127">Categorie di eventi e come toouse li</span><span class="sxs-lookup"><span data-stu-id="12b6a-127">Event categories and how toouse them</span></span>

<span data-ttu-id="12b6a-128">Ogni categoria di monitoraggio delle operazioni tiene traccia di un diverso tipo di interazione con l'hub IoT e ogni categoria di monitoraggio ha uno schema che definisce come sono strutturati gli eventi nella categoria stessa.</span><span class="sxs-lookup"><span data-stu-id="12b6a-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="12b6a-129">Operazioni relative alle identità dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="12b6a-129">Device identity operations</span></span>

<span data-ttu-id="12b6a-130">categoria di operazioni identità dispositivo Hello tiene traccia degli errori che si verificano quando si tenta di toocreate, aggiornare o eliminare una voce nel Registro di sistema dell'hub del IoT identità.</span><span class="sxs-lookup"><span data-stu-id="12b6a-130">hello device identity operations category tracks errors that occur when you attempt toocreate, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="12b6a-131">Il rilevamento di questa categoria è utile per gli scenari di provisioning.</span><span class="sxs-lookup"><span data-stu-id="12b6a-131">Tracking this category is useful for provisioning scenarios.</span></span>

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

### <a name="device-telemetry"></a><span data-ttu-id="12b6a-132">Telemetria dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="12b6a-132">Device telemetry</span></span>

<span data-ttu-id="12b6a-133">categoria di dati di telemetria dispositivi Hello tiene traccia degli errori che si verificano all'hub IoT hello e sono la pipeline di telemetria correlati toohello.</span><span class="sxs-lookup"><span data-stu-id="12b6a-133">hello device telemetry category tracks errors that occur at hello IoT hub and are related toohello telemetry pipeline.</span></span> <span data-ttu-id="12b6a-134">Questa categoria include gli errori che si verificano durante l'invio di eventi di telemetria, ad esempio la limitazione, e la ricezione di eventi di telemetria, ad esempio un lettore non autorizzato.</span><span class="sxs-lookup"><span data-stu-id="12b6a-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="12b6a-135">Questa categoria non può intercettare gli errori causati da codice in esecuzione sul dispositivo hello stesso.</span><span class="sxs-lookup"><span data-stu-id="12b6a-135">This category cannot catch errors caused by code running on hello device itself.</span></span>

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

### <a name="cloud-to-device-commands"></a><span data-ttu-id="12b6a-136">Comandi da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="12b6a-136">Cloud-to-device commands</span></span>

<span data-ttu-id="12b6a-137">categoria di comandi cloud a dispositivo Hello tiene traccia degli errori che si verificano all'hub IoT hello e sono pipeline messaggio cloud a dispositivo toohello correlati.</span><span class="sxs-lookup"><span data-stu-id="12b6a-137">hello cloud-to-device commands category tracks errors that occur at hello IoT hub and are related toohello cloud-to-device message pipeline.</span></span> <span data-ttu-id="12b6a-138">Questa categoria include gli errori che si verificano durante l'invio di messaggi da cloud a dispositivo, ad esempio un mittente non autorizzato, la ricezione di messaggi da cloud a dispositivo, ad esempio il superamento del numero di recapiti, e la ricezione di commenti sui messaggi da cloud a dispositivo, ad esempio commenti scaduti.</span><span class="sxs-lookup"><span data-stu-id="12b6a-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="12b6a-139">Questa categoria non rileva gli errori da un dispositivo che gestisce correttamente un messaggio da cloud a dispositivo se il messaggio hello del cloud a dispositivo è stata inviata correttamente.</span><span class="sxs-lookup"><span data-stu-id="12b6a-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if hello cloud-to-device message was delivered successfully.</span></span>

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

### <a name="connections"></a><span data-ttu-id="12b6a-140">Connessioni</span><span class="sxs-lookup"><span data-stu-id="12b6a-140">Connections</span></span>

<span data-ttu-id="12b6a-141">categoria di connessioni Hello tiene traccia degli errori che si verificano quando i dispositivi connettono o Disconnetti da un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="12b6a-141">hello connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="12b6a-142">Il rilevamento di questa categoria è utile per identificare i tentativi di connessione non autorizzati e per rilevare quando una connessione viene persa dai dispositivi in aree di scarsa connettività.</span><span class="sxs-lookup"><span data-stu-id="12b6a-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

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

### <a name="file-uploads"></a><span data-ttu-id="12b6a-143">Caricamenti di file</span><span class="sxs-lookup"><span data-stu-id="12b6a-143">File uploads</span></span>

<span data-ttu-id="12b6a-144">categoria di caricamento file Hello tiene traccia degli errori che si verificano all'hub IoT hello e sono funzionalità di caricamento toofile correlati.</span><span class="sxs-lookup"><span data-stu-id="12b6a-144">hello file upload category tracks errors that occur at hello IoT hub and are related toofile upload functionality.</span></span> <span data-ttu-id="12b6a-145">Questa categoria include:</span><span class="sxs-lookup"><span data-stu-id="12b6a-145">This category includes:</span></span>

* <span data-ttu-id="12b6a-146">Errori che si verificano con hello URI SAS, ad esempio quando scade prima che un dispositivo notifica hub hello di un caricamento completato.</span><span class="sxs-lookup"><span data-stu-id="12b6a-146">Errors that occur with hello SAS URI, such as when it expires before a device notifies hello hub of a completed upload.</span></span>
* <span data-ttu-id="12b6a-147">Non è stato possibile caricamenti segnalati dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="12b6a-147">Failed uploads reported by hello device.</span></span>
* <span data-ttu-id="12b6a-148">Errori che si verificano quando un file non viene trovato nell'archivio durante la creazione del messaggio di notifica dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="12b6a-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="12b6a-149">Questa categoria non può intercettare gli errori generati direttamente durante dispositivo hello sta caricando un file toostorage.</span><span class="sxs-lookup"><span data-stu-id="12b6a-149">This category cannot catch errors that directly occur while hello device is uploading a file toostorage.</span></span>

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

### <a name="message-routing"></a><span data-ttu-id="12b6a-150">Routing dei messaggi</span><span class="sxs-lookup"><span data-stu-id="12b6a-150">Message routing</span></span>

<span data-ttu-id="12b6a-151">categoria di routing di messaggi Hello tiene traccia degli errori che si verificano durante la valutazione di route di messaggio e l'integrità di endpoint percepita dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="12b6a-151">hello message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="12b6a-152">Questa categoria include gli eventi, ad esempio quando una regola valuta troppo "undefined", quando l'IoT Hub contrassegna un endpoint come inattivi e gli errori ricevuti da un endpoint.</span><span class="sxs-lookup"><span data-stu-id="12b6a-152">This category includes events such as when a rule evaluates too"undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="12b6a-153">Questa categoria non sono inclusi errori specifici relative ai messaggi hello stessi (ad esempio dispositivo errori di limitazione), che vengono segnalati nella categoria "telemetria del dispositivo" hello.</span><span class="sxs-lookup"><span data-stu-id="12b6a-153">This category does not include specific errors about hello messages themselves (such as device throttling errors), which are reported under hello "device telemetry" category.</span></span>

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

## <a name="view-events"></a><span data-ttu-id="12b6a-154">Visualizzare eventi</span><span class="sxs-lookup"><span data-stu-id="12b6a-154">View events</span></span>

<span data-ttu-id="12b6a-155">È possibile utilizzare hello *l'hub IOT Esplora* strumento tooquickly verificare che l'hub IoT è la generazione di eventi di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="12b6a-155">You can use hello *iothub-explorer* tool tooquickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="12b6a-156">hello tooinstall strumento, vedere le istruzioni hello hello [l'hub IOT Esplora] [ lnk-iothub-explorer] repository GitHub.</span><span class="sxs-lookup"><span data-stu-id="12b6a-156">tooinstall hello tool, see hello instructions in hello [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="12b6a-157">Verificare che hello **connessioni** monitoraggio categoria viene impostato troppo**Verbose** nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="12b6a-157">Make sure hello **Connections** monitoring category is set too**Verbose** in hello portal.</span></span>

1. <span data-ttu-id="12b6a-158">Al prompt di comando, eseguire hello seguenti tooread comando dagli hello dell'endpoint di monitoraggio:</span><span class="sxs-lookup"><span data-stu-id="12b6a-158">At a command-prompt, run hello following command tooread from hello monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="12b6a-159">In un altro prompt dei comandi, eseguire hello successivo comando toosimulate un dispositivo l'invio di messaggi da dispositivo a cloud:</span><span class="sxs-lookup"><span data-stu-id="12b6a-159">In another command-prompt, run hello following command toosimulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="12b6a-160">Hello prima della riga di comando Mostra gli eventi di monitoraggio di hello dispositivo simulato hello si connette tooyour hub IoT.</span><span class="sxs-lookup"><span data-stu-id="12b6a-160">hello first command-prompt shows hello monitoring events as hello simulated device connects tooyour IoT hub.</span></span>

## <a name="connect-toohello-monitoring-endpoint"></a><span data-ttu-id="12b6a-161">Connettersi toohello dell'endpoint di monitoraggio</span><span class="sxs-lookup"><span data-stu-id="12b6a-161">Connect toohello monitoring endpoint</span></span>

<span data-ttu-id="12b6a-162">Hello monitoraggio endpoint dell'hub IoT è un endpoint compatibile con Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="12b6a-162">hello monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="12b6a-163">È possibile utilizzare qualsiasi meccanismo che funziona con i messaggi di monitoraggio tooread gli hub di eventi da questo endpoint.</span><span class="sxs-lookup"><span data-stu-id="12b6a-163">You can use any mechanism that works with Event Hubs tooread monitoring messages from this endpoint.</span></span> <span data-ttu-id="12b6a-164">Hello esempio seguente crea un lettore di base che non è adatto per una distribuzione di velocità effettiva elevata.</span><span class="sxs-lookup"><span data-stu-id="12b6a-164">hello following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="12b6a-165">Per ulteriori informazioni su come tooprocess messaggi dagli hub eventi, vedere hello [Introduzione agli hub di eventi] [ lnk-eventhubs-tutorial] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="12b6a-165">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="12b6a-166">endpoint di monitoraggio toohello tooconnect, è necessario un nome di endpoint hello e di stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="12b6a-166">tooconnect toohello monitoring endpoint, you need a connection string and hello endpoint name.</span></span> <span data-ttu-id="12b6a-167">Hello alla procedura seguente viene mostrato come toofind hello valori necessari nel portale di hello:</span><span class="sxs-lookup"><span data-stu-id="12b6a-167">hello following steps show you how toofind hello necessary values in hello portal:</span></span>

1. <span data-ttu-id="12b6a-168">Nel portale di hello passare tooyour pannello della risorsa IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="12b6a-168">In hello portal, navigate tooyour IoT Hub resource blade.</span></span>

1. <span data-ttu-id="12b6a-169">Scegliere **monitoraggio delle operazioni**e prendere nota di hello **nome compatibile con Hub eventi** e **endpoint compatibile con Hub eventi** valori:</span><span class="sxs-lookup"><span data-stu-id="12b6a-169">Choose **Operations monitoring**, and make a note of hello **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![Valori di Endpoint compatibile con Hub eventi][img-endpoints]

1. <span data-ttu-id="12b6a-171">Scegliere **Criteri di accesso condiviso**, quindi scegliere **servizio**.</span><span class="sxs-lookup"><span data-stu-id="12b6a-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="12b6a-172">Prendere nota di hello **chiave primaria** valore:</span><span class="sxs-lookup"><span data-stu-id="12b6a-172">Make a note of hello **Primary key** value:</span></span>

    ![Chiave primaria del servizio dei criteri di accesso condiviso][img-service-key]

<span data-ttu-id="12b6a-174">Hello seguente esempio di codice c# viene eseguita da Visual Studio **Windows Desktop classico** applicazione console c#.</span><span class="sxs-lookup"><span data-stu-id="12b6a-174">hello following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="12b6a-175">progetto Hello è hello **Windowsazure** installato il pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="12b6a-175">hello project has hello **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="12b6a-176">Sostituire i segnaposto di stringa di connessione hello con una stringa di connessione che utilizza hello **endpoint compatibile con Hub eventi** e servizio **chiave primaria** sui valori annotati in precedenza, come illustrato nell'esempio hello esempio:</span><span class="sxs-lookup"><span data-stu-id="12b6a-176">Replace hello connection string placeholder with a connection string that uses hello **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in hello following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="12b6a-177">Sostituire i segnaposto nome endpoint con hello monitoraggio hello **nome compatibile con Hub eventi** valore annotato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="12b6a-177">Replace hello monitoring endpoint name placeholder with hello **Event Hub-compatible name** value you noted previously.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="12b6a-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="12b6a-178">Next steps</span></span>
<span data-ttu-id="12b6a-179">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="12b6a-179">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="12b6a-180">[Guida per gli sviluppatori dell'hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="12b6a-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="12b6a-181">[Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="12b6a-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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