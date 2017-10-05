---
title: Metadati di informazioni sul dispositivo nella soluzione per il monitoraggio remoto | Documentazione Microsoft
description: Descrizione della soluzione preconfigurata per il monitoraggio remoto di Azure IoT e relativa architettura.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: f8fd452806a0a0b98cf8e434c9bd55700083a6c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="device-information-metadata-in-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="21bad-103">Metadati di informazioni sul dispositivo nella soluzione preconfigurata per il monitoraggio remoto</span><span class="sxs-lookup"><span data-stu-id="21bad-103">Device information metadata in the remote monitoring preconfigured solution</span></span>

<span data-ttu-id="21bad-104">La soluzione preconfigurata per il monitoraggio remoto di Azure IoT Suite dimostra un approccio per la gestione dei metadati del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="21bad-104">The Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="21bad-105">Questo articolo delinea l'approccio adottato da questa soluzione per illustrare:</span><span class="sxs-lookup"><span data-stu-id="21bad-105">This article outlines the approach this solution takes to enable you to understand:</span></span>

* <span data-ttu-id="21bad-106">Quali metadati del dispositivo vengono archiviati dalla soluzione.</span><span class="sxs-lookup"><span data-stu-id="21bad-106">What device metadata the solution stores.</span></span>
* <span data-ttu-id="21bad-107">Come la soluzione gestisce i metadati del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="21bad-107">How the solution manages the device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="21bad-108">Context</span><span class="sxs-lookup"><span data-stu-id="21bad-108">Context</span></span>

<span data-ttu-id="21bad-109">La soluzione preconfigurata per il monitoraggio remoto usa l'[hub IoT di Azure][lnk-iot-hub] per consentire ai dispositivi di inviare dati al cloud.</span><span class="sxs-lookup"><span data-stu-id="21bad-109">The remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] to enable your devices to send data to the cloud.</span></span> <span data-ttu-id="21bad-110">La soluzione archivia le informazioni sui dispositivi in tre posizioni diverse:</span><span class="sxs-lookup"><span data-stu-id="21bad-110">The solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="21bad-111">Percorso</span><span class="sxs-lookup"><span data-stu-id="21bad-111">Location</span></span> | <span data-ttu-id="21bad-112">Informazioni archiviate</span><span class="sxs-lookup"><span data-stu-id="21bad-112">Information stored</span></span> | <span data-ttu-id="21bad-113">Implementazione</span><span class="sxs-lookup"><span data-stu-id="21bad-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="21bad-114">Registro delle identità</span><span class="sxs-lookup"><span data-stu-id="21bad-114">Identity registry</span></span> | <span data-ttu-id="21bad-115">ID del dispositivo, chiavi di autenticazione, stato di abilitazione</span><span class="sxs-lookup"><span data-stu-id="21bad-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="21bad-116">Predefinito nell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="21bad-116">Built in to IoT Hub</span></span> |
| <span data-ttu-id="21bad-117">Dispositivi gemelli</span><span class="sxs-lookup"><span data-stu-id="21bad-117">Device twins</span></span> | <span data-ttu-id="21bad-118">Metadati: proprietà segnalate, proprietà desiderate, tag</span><span class="sxs-lookup"><span data-stu-id="21bad-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="21bad-119">Predefinito nell'hub IoT</span><span class="sxs-lookup"><span data-stu-id="21bad-119">Built in to IoT Hub</span></span> |
| <span data-ttu-id="21bad-120">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="21bad-120">Cosmos DB</span></span> | <span data-ttu-id="21bad-121">Cronologia dei comandi e dei metodi</span><span class="sxs-lookup"><span data-stu-id="21bad-121">Command and method history</span></span> | <span data-ttu-id="21bad-122">Personalizzato per la soluzione</span><span class="sxs-lookup"><span data-stu-id="21bad-122">Custom for solution</span></span> |

<span data-ttu-id="21bad-123">L'hub IoT include un [registro delle identità dei dispositivi][lnk-identity-registry] per gestire l'accesso all'hub IoT e usa i [dispositivi gemelli][lnk-device-twin] per gestire i metadati del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="21bad-123">IoT Hub includes a [device identity registry][lnk-identity-registry] to manage access to an IoT hub and uses [device twins][lnk-device-twin] to manage device metadata.</span></span> <span data-ttu-id="21bad-124">È disponibile anche un *registro dei dispositivi* specifico della soluzione di monitoraggio remoto, che archivia la cronologia dei comandi e dei metodi.</span><span class="sxs-lookup"><span data-stu-id="21bad-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="21bad-125">La soluzione di monitoraggio remoto usa un database [Cosmos DB][lnk-docdb] per implementare un archivio personalizzato per la cronologia dei comandi e dei metodi.</span><span class="sxs-lookup"><span data-stu-id="21bad-125">The remote monitoring solution uses a [Cosmos DB][lnk-docdb] database to implement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="21bad-126">La soluzione preconfigurata per il monitoraggio remoto mantiene il registro delle identità dei dispositivi sincronizzato con le informazioni disponibili nel database Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="21bad-126">The remote monitoring preconfigured solution keeps the device identity registry in sync with the information in the Cosmos DB database.</span></span> <span data-ttu-id="21bad-127">Entrambi usano lo stesso ID dispositivo per identificare in modo univoco ogni dispositivo connesso all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="21bad-127">Both use the same device id to uniquely identify each device connected to your IoT hub.</span></span>

## <a name="device-metadata"></a><span data-ttu-id="21bad-128">Metadati del dispositivo</span><span class="sxs-lookup"><span data-stu-id="21bad-128">Device metadata</span></span>

<span data-ttu-id="21bad-129">L'hub IoT gestisce un [dispositivo gemello][lnk-device-twin] per ogni dispositivo simulato e fisico connesso a una soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="21bad-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected to a remote monitoring solution.</span></span> <span data-ttu-id="21bad-130">La soluzione usa i dispositivi gemelli per gestire i metadati associati ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="21bad-130">The solution uses device twins to manage the metadata associated with devices.</span></span> <span data-ttu-id="21bad-131">Un dispositivo gemello è un documento JSON gestito dall'hub IoT e la soluzione usa l'API dell'hub IoT per interagire con i dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="21bad-131">A device twin is a JSON document maintained by IoT Hub, and the solution uses the IoT Hub API to interact with device twins.</span></span>

<span data-ttu-id="21bad-132">Un dispositivo gemello archivia tre tipi di metadati:</span><span class="sxs-lookup"><span data-stu-id="21bad-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="21bad-133">Le *proprietà segnalate* vengono inviate a un hub IoT da un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="21bad-133">*Reported properties* are sent to an IoT hub by a device.</span></span> <span data-ttu-id="21bad-134">Nella soluzione di monitoraggio remoto, i dispositivi simulati inviano le proprietà all'avvio e in risposta a comandi e metodi di tipo **Change device state**.</span><span class="sxs-lookup"><span data-stu-id="21bad-134">In the remote monitoring solution, simulated devices send reported properties at start-up and in response to **Change device state** commands and methods.</span></span> <span data-ttu-id="21bad-135">È possibile visualizzare le proprietà segnalate in **Elenco dispositivi** e **Dettagli dispositivo** nel portale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="21bad-135">You can view reported properties in the **Device list** and **Device details** in the solution portal.</span></span> <span data-ttu-id="21bad-136">Le proprietà segnalate sono di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="21bad-136">Reported properties are read only.</span></span>
- <span data-ttu-id="21bad-137">Le *proprietà desiderate* vengono recuperate dall'hub IoT dai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="21bad-137">*Desired properties* are retrieved from the IoT hub by devices.</span></span> <span data-ttu-id="21bad-138">Le modifiche di configurazione necessarie nel dispositivo sono a carico del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="21bad-138">It is the responsibility of the device to make any necessary configuration change on the device.</span></span> <span data-ttu-id="21bad-139">Il dispositivo deve anche segnalare la modifica all'hub come proprietà segnalata.</span><span class="sxs-lookup"><span data-stu-id="21bad-139">It is also the responsibility of the device to report the change back to the hub as a reported property.</span></span> <span data-ttu-id="21bad-140">È possibile impostare un valore della proprietà desiderata tramite il portale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="21bad-140">You can set a desired property value through the solution portal.</span></span>
- <span data-ttu-id="21bad-141">I *tag* esistono solo nel dispositivo gemello e non vengono mai sincronizzati con un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="21bad-141">*Tags* only exist in the device twin and are never synchronized with a device.</span></span> <span data-ttu-id="21bad-142">È possibile impostare i valori dei tag nel portale della soluzione e usarli per filtrare l'elenco di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="21bad-142">You can set tag values in the solution portal and use them when you filter the list of devices.</span></span> <span data-ttu-id="21bad-143">La soluzione usa un tag anche per identificare l'icona da visualizzare per un dispositivo nel portale della soluzione.</span><span class="sxs-lookup"><span data-stu-id="21bad-143">The solution also uses a tag to identify the icon to display for a device in the solution portal.</span></span>

<span data-ttu-id="21bad-144">Le proprietà segnalate dai dispositivi simulati includono ad esempio il produttore, il numero di modello, la latitudine e la longitudine.</span><span class="sxs-lookup"><span data-stu-id="21bad-144">Example reported properties from the simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="21bad-145">I dispositivi simulati restituiscono anche l'elenco di metodi supportati come proprietà segnalata.</span><span class="sxs-lookup"><span data-stu-id="21bad-145">Simulated devices also return the list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="21bad-146">Il codice del dispositivo simulato usa le proprietà desiderate **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** soltanto per aggiornare le proprietà segnalate inviate all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="21bad-146">The simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties sent back to IoT Hub.</span></span> <span data-ttu-id="21bad-147">Tutte le altre richieste di modifica delle proprietà desiderate vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="21bad-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="21bad-148">Un documento JSON di metadati di informazioni sul dispositivo archiviato nel database Cosmos DB del registro dei dispositivi ha la struttura seguente:</span><span class="sxs-lookup"><span data-stu-id="21bad-148">A device information metadata JSON document stored in the device registry Cosmos DB database has the following structure:</span></span>

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> <span data-ttu-id="21bad-149">Le informazioni sul dispositivo possono includere anche metadati per descrivere la telemetria inviata dal dispositivo all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="21bad-149">Device information can also include metadata to describe the telemetry the device sends to IoT Hub.</span></span> <span data-ttu-id="21bad-150">La soluzione per il monitoraggio remoto usa questi metadati di telemetria per personalizzare la visualizzazione della [telemetria dinamica][lnk-dynamic-telemetry] nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="21bad-150">The remote monitoring solution uses this telemetry metadata to customize how the dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>

## <a name="lifecycle"></a><span data-ttu-id="21bad-151">Ciclo di vita</span><span class="sxs-lookup"><span data-stu-id="21bad-151">Lifecycle</span></span>

<span data-ttu-id="21bad-152">Quando si crea per la prima volta un dispositivo nel portale della soluzione, la soluzione crea una voce nel database Cosmos DB per archiviare la cronologia dei comandi e dei metodi.</span><span class="sxs-lookup"><span data-stu-id="21bad-152">When you first create a device in the solution portal, the solution creates an entry in the Cosmos DB database to store command and method history.</span></span> <span data-ttu-id="21bad-153">A questo punto la soluzione crea anche una voce per il dispositivo nel registro delle identità dei dispositivi che genera le chiavi usate dal dispositivo per l'autenticazione con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="21bad-153">At this point, the solution also creates an entry for the device in the device identity registry, which generates the keys the device uses to authenticate with IoT Hub.</span></span> <span data-ttu-id="21bad-154">Viene creato anche un dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="21bad-154">It also creates a device twin.</span></span>

<span data-ttu-id="21bad-155">Quando un dispositivo si connette per la prima volta alla soluzione, invia proprietà segnalate e un messaggio informativo sul dispositivo</span><span class="sxs-lookup"><span data-stu-id="21bad-155">When a device first connects to the solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="21bad-156">I valori delle proprietà segnalate vengono salvati automaticamente nel dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="21bad-156">The reported property values are automatically saved in the device twin.</span></span> <span data-ttu-id="21bad-157">Le proprietà segnalate includono il produttore del modello, il numero di modello, il numero di serie e un elenco di metodi supportati.</span><span class="sxs-lookup"><span data-stu-id="21bad-157">The reported properties include the device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="21bad-158">Il messaggio informativo sul dispositivo include un elenco dei comandi supportati dal dispositivo, incluse le informazioni sui parametri dei comandi.</span><span class="sxs-lookup"><span data-stu-id="21bad-158">The device information message includes the list of the commands the device supports including information about any command parameters.</span></span> <span data-ttu-id="21bad-159">Quando la soluzione riceve il messaggio, aggiorna le informazioni sui dispositivi nel database Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="21bad-159">When the solution receives this message, it updates the device information in the Cosmos DB database.</span></span>

### <a name="view-and-edit-device-information-in-the-solution-portal"></a><span data-ttu-id="21bad-160">Visualizzare e modificare informazioni sul dispositivo nel portale della soluzione</span><span class="sxs-lookup"><span data-stu-id="21bad-160">View and edit device information in the solution portal</span></span>

<span data-ttu-id="21bad-161">Per impostazione predefinita, l'elenco di dispositivi nel portale della soluzione visualizza le proprietà del dispositivo seguenti come colonne: **Stato**, **ID dispositivo**, **Produttore**, **Numero modello**, **Numero di serie**, **Firmware**, **Piattaforma**, **Processore** e **RAM installata**.</span><span class="sxs-lookup"><span data-stu-id="21bad-161">The device list in the solution portal displays the following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="21bad-162">È possibile personalizzare le colonne facendo clic su **Editor di colonne**.</span><span class="sxs-lookup"><span data-stu-id="21bad-162">You can customize the columns by clicking **Column editor**.</span></span> <span data-ttu-id="21bad-163">Le proprietà **Latitudine** e **Longitudine** del dispositivo determinano la posizione nella mappa di Bing nel dashboard.</span><span class="sxs-lookup"><span data-stu-id="21bad-163">The device properties **Latitude** and **Longitude** drive the location in the Bing Map on the dashboard.</span></span>

![Editor di colonne nell'elenco di dispositivi][img-device-list]

<span data-ttu-id="21bad-165">Nel riquadro **Dettagli dispositivo** nel portale della soluzione, è possibile modificare le proprietà desiderate e i tag. Le proprietà segnalate sono di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="21bad-165">In the **Device Details** pane in the solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![Riquadro Dettagli dispositivo][img-device-edit]

<span data-ttu-id="21bad-167">È possibile usare il portale della soluzione per rimuovere un dispositivo dalla soluzione.</span><span class="sxs-lookup"><span data-stu-id="21bad-167">You can use the solution portal to remove a device from your solution.</span></span> <span data-ttu-id="21bad-168">Quando si rimuove un dispositivo, la soluzione rimuove la voce del dispositivo dal registro delle identità e quindi elimina il dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="21bad-168">When you remove a device, the solution removes the device entry from identity registry and then deletes the device twin.</span></span> <span data-ttu-id="21bad-169">La soluzione rimuove anche le informazioni correlate al dispositivo dal database Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="21bad-169">The solution also removes information related to the device from the Cosmos DB database.</span></span> <span data-ttu-id="21bad-170">Prima di poter rimuovere un dispositivo, è necessario disabilitarlo.</span><span class="sxs-lookup"><span data-stu-id="21bad-170">Before you can remove a device, you must disable it.</span></span>

![Rimuovere un dispositivo][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="21bad-172">Elaborazione dei messaggi informativi sul dispositivo</span><span class="sxs-lookup"><span data-stu-id="21bad-172">Device information message processing</span></span>

<span data-ttu-id="21bad-173">I messaggi informativi sul dispositivo inviati da un dispositivo sono diversi dai messaggi di telemetria.</span><span class="sxs-lookup"><span data-stu-id="21bad-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="21bad-174">I messaggi informativi sul dispositivo includono i comandi a cui un dispositivo può rispondere e l'eventuale cronologia dei comandi.</span><span class="sxs-lookup"><span data-stu-id="21bad-174">Device information messages include the commands a device can respond to, and any command history.</span></span> <span data-ttu-id="21bad-175">L'hub IoT non conosce i metadati contenuti in un messaggio informativo sul dispositivo ed elabora il messaggio come qualsiasi altro messaggio inviato dal dispositivo al cloud.</span><span class="sxs-lookup"><span data-stu-id="21bad-175">IoT Hub itself has no knowledge of the metadata contained in a device information message and processes the message in the same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="21bad-176">Nella soluzione per il monitoraggio remoto, un processo di [Analisi di flusso di Azure][lnk-stream-analytics] legge i messaggi dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="21bad-176">In the remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads the messages from IoT Hub.</span></span> <span data-ttu-id="21bad-177">Il processo **DeviceInfo** di Analisi di flusso filtra i messaggi contenenti **"ObjectType": "DeviceInfo"** e li inoltra all'istanza dell'host **EventProcessorHost** in esecuzione in un processo Web.</span><span class="sxs-lookup"><span data-stu-id="21bad-177">The **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them to the **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="21bad-178">La logica nell'istanza di **EventProcessorHost** usa l'ID dispositivo per trovare il record di Cosmos DB per il dispositivo specifico e aggiorna il record.</span><span class="sxs-lookup"><span data-stu-id="21bad-178">Logic in the **EventProcessorHost** instance uses the device id to find the Cosmos DB record for the specific device and update the record.</span></span>

> [!NOTE]
> <span data-ttu-id="21bad-179">Un messaggio informativo sul dispositivo è un messaggio standard inviato dal dispositivo al cloud.</span><span class="sxs-lookup"><span data-stu-id="21bad-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="21bad-180">La soluzione distingue i messaggi informativi sul dispositivo dai messaggi di telemetria usando le query di Analisi di flusso di Azure.</span><span class="sxs-lookup"><span data-stu-id="21bad-180">The solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21bad-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="21bad-181">Next steps</span></span>

<span data-ttu-id="21bad-182">Dopo aver illustrato come personalizzare le soluzioni preconfigurate, è possibile esplorare alcune altre funzionalità e soluzioni preconfigurate di Suite IoT:</span><span class="sxs-lookup"><span data-stu-id="21bad-182">Now you've finished learning how you can customize the preconfigured solutions, you can explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="21bad-183">[Panoramica della soluzione preconfigurata di manutenzione predittiva][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="21bad-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="21bad-184">[Domande frequenti su IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="21bad-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="21bad-185">[Sicurezza IoT sin dall'inizio][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="21bad-185">[IoT security from the ground up][lnk-security-groundup]</span></span>

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
