---
title: metadati di informazioni aaaDevice nella soluzione di monitoraggio remoto hello | Documenti Microsoft
description: Una descrizione di hello Azure IoT preconfigurato soluzione di monitoraggio remoto e la relativa architettura.
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
ms.openlocfilehash: 8387b98b8b2ae4934b0c900bc4df37dc17337c60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="90f72-103">Metadati informazioni del dispositivo nella soluzione preconfigurata di monitoraggio remoto hello</span><span class="sxs-lookup"><span data-stu-id="90f72-103">Device information metadata in hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="90f72-104">Hello Azure IoT Suite soluzione preconfigurata di monitoraggio remoto viene illustrato un approccio per la gestione dei metadati del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="90f72-104">hello Azure IoT Suite remote monitoring preconfigured solution demonstrates an approach for managing device metadata.</span></span> <span data-ttu-id="90f72-105">Questo articolo vengono illustrati l'approccio di hello questa soluzione richiede tooenable toounderstand è:</span><span class="sxs-lookup"><span data-stu-id="90f72-105">This article outlines hello approach this solution takes tooenable you toounderstand:</span></span>

* <span data-ttu-id="90f72-106">Soluzione di hello metadati quali dispositivi vengono archiviati.</span><span class="sxs-lookup"><span data-stu-id="90f72-106">What device metadata hello solution stores.</span></span>
* <span data-ttu-id="90f72-107">Come soluzione hello gestisce i metadati del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="90f72-107">How hello solution manages hello device metadata.</span></span>

## <a name="context"></a><span data-ttu-id="90f72-108">Context</span><span class="sxs-lookup"><span data-stu-id="90f72-108">Context</span></span>

<span data-ttu-id="90f72-109">Hello monitoraggio remoto preconfigurato soluzione utilizza [IoT Hub Azure] [ lnk-iot-hub] tooenable toohello di dati toosend i dispositivi cloud.</span><span class="sxs-lookup"><span data-stu-id="90f72-109">hello remote monitoring preconfigured solution uses [Azure IoT Hub][lnk-iot-hub] tooenable your devices toosend data toohello cloud.</span></span> <span data-ttu-id="90f72-110">soluzione Hello archivia informazioni sui dispositivi in tre percorsi diversi:</span><span class="sxs-lookup"><span data-stu-id="90f72-110">hello solution stores information about devices in three different locations:</span></span>

| <span data-ttu-id="90f72-111">Percorso</span><span class="sxs-lookup"><span data-stu-id="90f72-111">Location</span></span> | <span data-ttu-id="90f72-112">Informazioni archiviate</span><span class="sxs-lookup"><span data-stu-id="90f72-112">Information stored</span></span> | <span data-ttu-id="90f72-113">Implementazione</span><span class="sxs-lookup"><span data-stu-id="90f72-113">Implementation</span></span> |
| -------- | ------------------ | -------------- |
| <span data-ttu-id="90f72-114">Registro delle identità</span><span class="sxs-lookup"><span data-stu-id="90f72-114">Identity registry</span></span> | <span data-ttu-id="90f72-115">ID del dispositivo, chiavi di autenticazione, stato di abilitazione</span><span class="sxs-lookup"><span data-stu-id="90f72-115">Device id, authentication keys, enabled state</span></span> | <span data-ttu-id="90f72-116">TooIoT incorporato Hub</span><span class="sxs-lookup"><span data-stu-id="90f72-116">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="90f72-117">Dispositivi gemelli</span><span class="sxs-lookup"><span data-stu-id="90f72-117">Device twins</span></span> | <span data-ttu-id="90f72-118">Metadati: proprietà segnalate, proprietà desiderate, tag</span><span class="sxs-lookup"><span data-stu-id="90f72-118">Metadata: reported properties, desired properties, tags</span></span> | <span data-ttu-id="90f72-119">TooIoT incorporato Hub</span><span class="sxs-lookup"><span data-stu-id="90f72-119">Built in tooIoT Hub</span></span> |
| <span data-ttu-id="90f72-120">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="90f72-120">Cosmos DB</span></span> | <span data-ttu-id="90f72-121">Cronologia dei comandi e dei metodi</span><span class="sxs-lookup"><span data-stu-id="90f72-121">Command and method history</span></span> | <span data-ttu-id="90f72-122">Personalizzato per la soluzione</span><span class="sxs-lookup"><span data-stu-id="90f72-122">Custom for solution</span></span> |

<span data-ttu-id="90f72-123">IoT Hub include un [registro identità dispositivo] [ lnk-identity-registry] toomanage accedere hub IoT tooan e utilizza [gemelli dispositivo] [ lnk-device-twin] toomanage metadati del dispositivo .</span><span class="sxs-lookup"><span data-stu-id="90f72-123">IoT Hub includes a [device identity registry][lnk-identity-registry] toomanage access tooan IoT hub and uses [device twins][lnk-device-twin] toomanage device metadata.</span></span> <span data-ttu-id="90f72-124">È disponibile anche un *registro dei dispositivi* specifico della soluzione di monitoraggio remoto, che archivia la cronologia dei comandi e dei metodi.</span><span class="sxs-lookup"><span data-stu-id="90f72-124">There is also a remote monitoring solution-specific *device registry* that stores command and method history.</span></span> <span data-ttu-id="90f72-125">Hello remoto monitoraggio soluzione utilizza un [DB Cosmos] [ lnk-docdb] tooimplement database un archivio personalizzato per la cronologia del comando e il metodo.</span><span class="sxs-lookup"><span data-stu-id="90f72-125">hello remote monitoring solution uses a [Cosmos DB][lnk-docdb] database tooimplement a custom store for command and method history.</span></span>

> [!NOTE]
> <span data-ttu-id="90f72-126">Hello soluzione preconfigurata di monitoraggio remoto mantiene la sincronizzazione con le informazioni di hello del Registro di sistema di hello dispositivo identity nel database DB Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="90f72-126">hello remote monitoring preconfigured solution keeps hello device identity registry in sync with hello information in hello Cosmos DB database.</span></span> <span data-ttu-id="90f72-127">Entrambi utilizzano hello stesso dispositivo id toouniquely identificare ogni dispositivo connesso tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="90f72-127">Both use hello same device id toouniquely identify each device connected tooyour IoT hub.</span></span>

## <a name="device-metadata"></a><span data-ttu-id="90f72-128">Metadati del dispositivo</span><span class="sxs-lookup"><span data-stu-id="90f72-128">Device metadata</span></span>

<span data-ttu-id="90f72-129">IoT Hub conserva un [doppi dispositivo] [ lnk-device-twin] per ogni dispositivo simulato e fisico connessi tooa soluzione di monitoraggio remoto.</span><span class="sxs-lookup"><span data-stu-id="90f72-129">IoT Hub maintains a [device twin][lnk-device-twin] for each simulated and physical device connected tooa remote monitoring solution.</span></span> <span data-ttu-id="90f72-130">soluzione di Hello utilizza metadati del dispositivo gemelli toomanage hello associati ai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="90f72-130">hello solution uses device twins toomanage hello metadata associated with devices.</span></span> <span data-ttu-id="90f72-131">Un doppio di un dispositivo è un documento JSON mantenuto dall'IoT Hub e soluzione hello utilizza hello API dell'Hub IoT toointeract con gemelli di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="90f72-131">A device twin is a JSON document maintained by IoT Hub, and hello solution uses hello IoT Hub API toointeract with device twins.</span></span>

<span data-ttu-id="90f72-132">Un dispositivo gemello archivia tre tipi di metadati:</span><span class="sxs-lookup"><span data-stu-id="90f72-132">A device twin stores three types of metadata:</span></span>

- <span data-ttu-id="90f72-133">*Proprietà segnalati* hub IoT tooan inviati da un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="90f72-133">*Reported properties* are sent tooan IoT hub by a device.</span></span> <span data-ttu-id="90f72-134">Nella soluzione di monitoraggio remoto hello, simulati i dispositivi le inviano proprietà restituita all'avvio e in risposta troppo**modificare lo stato del dispositivo** comandi e i metodi.</span><span class="sxs-lookup"><span data-stu-id="90f72-134">In hello remote monitoring solution, simulated devices send reported properties at start-up and in response too**Change device state** commands and methods.</span></span> <span data-ttu-id="90f72-135">È possibile visualizzare le proprietà segnalate in hello **elenco dei dispositivi** e **dettagli dispositivo** nel portale di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="90f72-135">You can view reported properties in hello **Device list** and **Device details** in hello solution portal.</span></span> <span data-ttu-id="90f72-136">Le proprietà segnalate sono di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="90f72-136">Reported properties are read only.</span></span>
- <span data-ttu-id="90f72-137">*Le proprietà desiderate* vengono recuperati dall'hub IoT hello dai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="90f72-137">*Desired properties* are retrieved from hello IoT hub by devices.</span></span> <span data-ttu-id="90f72-138">È responsabilità di hello di hello dispositivo toomake modificare qualsiasi configurazione necessarie sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="90f72-138">It is hello responsibility of hello device toomake any necessary configuration change on hello device.</span></span> <span data-ttu-id="90f72-139">È anche la responsabilità di hello dell'hub di hello dispositivo tooreport hello modifica toohello indietro come proprietà segnalate.</span><span class="sxs-lookup"><span data-stu-id="90f72-139">It is also hello responsibility of hello device tooreport hello change back toohello hub as a reported property.</span></span> <span data-ttu-id="90f72-140">È possibile impostare un valore di proprietà desiderato tramite il portale di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="90f72-140">You can set a desired property value through hello solution portal.</span></span>
- <span data-ttu-id="90f72-141">*Tag* esiste solo in un doppio dispositivo hello e non vengono mai sincronizzata con un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="90f72-141">*Tags* only exist in hello device twin and are never synchronized with a device.</span></span> <span data-ttu-id="90f72-142">È possibile impostare i valori di tag nel portale di soluzione hello e possono essere utilizzati filtrare l'elenco di hello dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="90f72-142">You can set tag values in hello solution portal and use them when you filter hello list of devices.</span></span> <span data-ttu-id="90f72-143">soluzione Hello utilizza anche un toodisplay di icona hello tooidentify tag per un dispositivo nel portale di soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="90f72-143">hello solution also uses a tag tooidentify hello icon toodisplay for a device in hello solution portal.</span></span>

<span data-ttu-id="90f72-144">Esempio segnalato proprietà dai dispositivi hello simulato includono produttore, il numero di modello, latitudine e longitudine.</span><span class="sxs-lookup"><span data-stu-id="90f72-144">Example reported properties from hello simulated devices include manufacturer, model number, latitude, and longitude.</span></span> <span data-ttu-id="90f72-145">Dispositivi simulati anche restituiranno elenco hello dei metodi supportati come una proprietà segnalata.</span><span class="sxs-lookup"><span data-stu-id="90f72-145">Simulated devices also return hello list of supported methods as a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="90f72-146">Hello dispositivo simulato solo codice hello **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** hello tooupdate proprietà desiderate segnalati proprietà restituita tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="90f72-146">hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties sent back tooIoT Hub.</span></span> <span data-ttu-id="90f72-147">Tutte le altre richieste di modifica delle proprietà desiderate vengono ignorate.</span><span class="sxs-lookup"><span data-stu-id="90f72-147">All other desired property change requests are ignored.</span></span>

<span data-ttu-id="90f72-148">Un documento JSON di dispositivo informazioni dei metadati archiviato nel database di DB Cosmos hello dispositivo del Registro di sistema ha hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="90f72-148">A device information metadata JSON document stored in hello device registry Cosmos DB database has hello following structure:</span></span>

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
> <span data-ttu-id="90f72-149">Informazioni sul dispositivo possono includere anche metadati toodescribe hello telemetria hello dispositivo invia tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="90f72-149">Device information can also include metadata toodescribe hello telemetry hello device sends tooIoT Hub.</span></span> <span data-ttu-id="90f72-150">soluzione di monitoraggio remoto Hello utilizza questo toocustomize metadati telemetria la modalità di visualizzazione dashboard hello [telemetria dinamica][lnk-dynamic-telemetry].</span><span class="sxs-lookup"><span data-stu-id="90f72-150">hello remote monitoring solution uses this telemetry metadata toocustomize how hello dashboard displays [dynamic telemetry][lnk-dynamic-telemetry].</span></span>

## <a name="lifecycle"></a><span data-ttu-id="90f72-151">Ciclo di vita</span><span class="sxs-lookup"><span data-stu-id="90f72-151">Lifecycle</span></span>

<span data-ttu-id="90f72-152">Quando si crea un dispositivo nel portale di soluzione hello, soluzione hello crea una voce nel comando di toostore database DB Cosmos hello e la cronologia di metodo.</span><span class="sxs-lookup"><span data-stu-id="90f72-152">When you first create a device in hello solution portal, hello solution creates an entry in hello Cosmos DB database toostore command and method history.</span></span> <span data-ttu-id="90f72-153">A questo punto, la soluzione hello crea anche una voce per il dispositivo hello hello dispositivo identità del Registro di sistema, che genera l'errore hello chiavi hello dispositivo utilizza tooauthenticate con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="90f72-153">At this point, hello solution also creates an entry for hello device in hello device identity registry, which generates hello keys hello device uses tooauthenticate with IoT Hub.</span></span> <span data-ttu-id="90f72-154">Viene creato anche un dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="90f72-154">It also creates a device twin.</span></span>

<span data-ttu-id="90f72-155">Quando un dispositivo si connette prima soluzione toohello, invia proprietà segnalate e un messaggio di informazioni del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="90f72-155">When a device first connects toohello solution, it sends reported properties and a device information message.</span></span> <span data-ttu-id="90f72-156">Hello riportati i valori delle proprietà vengono salvati automaticamente in un doppio dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="90f72-156">hello reported property values are automatically saved in hello device twin.</span></span> <span data-ttu-id="90f72-157">Hello segnalato proprietà includono produttore del dispositivo hello, numero di modello, il numero di serie e un elenco dei metodi supportati.</span><span class="sxs-lookup"><span data-stu-id="90f72-157">hello reported properties include hello device manufacturer, model number, serial number, and a list of supported methods.</span></span> <span data-ttu-id="90f72-158">messaggio di informazioni del dispositivo Hello include elenco hello dei comandi di hello hello dispositivo supporta incluse informazioni relative a eventuali parametri di comando.</span><span class="sxs-lookup"><span data-stu-id="90f72-158">hello device information message includes hello list of hello commands hello device supports including information about any command parameters.</span></span> <span data-ttu-id="90f72-159">Quando la soluzione hello riceve questo messaggio, aggiorna le informazioni sul dispositivo hello nel database DB Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="90f72-159">When hello solution receives this message, it updates hello device information in hello Cosmos DB database.</span></span>

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a><span data-ttu-id="90f72-160">Visualizzare e modificare le informazioni sul dispositivo nel portale di soluzione hello</span><span class="sxs-lookup"><span data-stu-id="90f72-160">View and edit device information in hello solution portal</span></span>

<span data-ttu-id="90f72-161">elenco dei dispositivi nel portale di soluzione hello Hello Visualizza hello seguenti delle proprietà del dispositivo come colonne per impostazione predefinita: **stato**, **DeviceId**, **produttore**, **Numero modello**, **numero di serie**, **Firmware**, **piattaforma**, **processore**e  **RAM installata**.</span><span class="sxs-lookup"><span data-stu-id="90f72-161">hello device list in hello solution portal displays hello following device properties as columns by default: **Status**, **DeviceId**, **Manufacturer**, **Model Number**, **Serial Number**, **Firmware**, **Platform**, **Processor**, and **Installed RAM**.</span></span> <span data-ttu-id="90f72-162">È possibile personalizzare le colonne di hello facendo **editor colonna**.</span><span class="sxs-lookup"><span data-stu-id="90f72-162">You can customize hello columns by clicking **Column editor**.</span></span> <span data-ttu-id="90f72-163">proprietà del dispositivo Hello **latitudine** e **longitudine** unità posizione hello hello mappa di Bing nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="90f72-163">hello device properties **Latitude** and **Longitude** drive hello location in hello Bing Map on hello dashboard.</span></span>

![Editor di colonne nell'elenco di dispositivi][img-device-list]

<span data-ttu-id="90f72-165">In hello **dettagli dispositivo** riquadro nel portale di soluzione hello, è possibile modificare le proprietà desiderate e tag (indicato proprietà sono di sola lettura).</span><span class="sxs-lookup"><span data-stu-id="90f72-165">In hello **Device Details** pane in hello solution portal, you can edit desired properties and tags (reported properties are read only).</span></span>

![Riquadro Dettagli dispositivo][img-device-edit]

<span data-ttu-id="90f72-167">È possibile utilizzare hello soluzione portale tooremove un dispositivo dalla soluzione.</span><span class="sxs-lookup"><span data-stu-id="90f72-167">You can use hello solution portal tooremove a device from your solution.</span></span> <span data-ttu-id="90f72-168">Quando si rimuove un dispositivo, la soluzione hello rimuove la voce di dispositivo hello dal Registro di sistema di identità ed elimina un doppio dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="90f72-168">When you remove a device, hello solution removes hello device entry from identity registry and then deletes hello device twin.</span></span> <span data-ttu-id="90f72-169">soluzione Hello rimuove anche dispositivo toohello correlati di informazioni dai database DB Cosmos hello.</span><span class="sxs-lookup"><span data-stu-id="90f72-169">hello solution also removes information related toohello device from hello Cosmos DB database.</span></span> <span data-ttu-id="90f72-170">Prima di poter rimuovere un dispositivo, è necessario disabilitarlo.</span><span class="sxs-lookup"><span data-stu-id="90f72-170">Before you can remove a device, you must disable it.</span></span>

![Rimuovere un dispositivo][img-device-remove]

## <a name="device-information-message-processing"></a><span data-ttu-id="90f72-172">Elaborazione dei messaggi informativi sul dispositivo</span><span class="sxs-lookup"><span data-stu-id="90f72-172">Device information message processing</span></span>

<span data-ttu-id="90f72-173">I messaggi informativi sul dispositivo inviati da un dispositivo sono diversi dai messaggi di telemetria.</span><span class="sxs-lookup"><span data-stu-id="90f72-173">Device information messages sent by a device are distinct from telemetry messages.</span></span> <span data-ttu-id="90f72-174">I messaggi informativi dispositivo includono comandi hello a che un dispositivo può rispondere e la cronologia dei comandi.</span><span class="sxs-lookup"><span data-stu-id="90f72-174">Device information messages include hello commands a device can respond to, and any command history.</span></span> <span data-ttu-id="90f72-175">IoT Hub stessa non ha alcuna conoscenza di hello metadati contenuti in un messaggio di informazioni del dispositivo e i processi hello messaggio hello allo stesso modo elabora i messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="90f72-175">IoT Hub itself has no knowledge of hello metadata contained in a device information message and processes hello message in hello same way it processes any device-to-cloud message.</span></span> <span data-ttu-id="90f72-176">Nella soluzione, di monitoraggio remoto hello un [Azure flusso Analitica] [ lnk-stream-analytics] processo (ASA) legge messaggi hello dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="90f72-176">In hello remote monitoring solution, an [Azure Stream Analytics][lnk-stream-analytics] (ASA) job reads hello messages from IoT Hub.</span></span> <span data-ttu-id="90f72-177">Hello **DeviceInfo** analitica di flusso del processo i filtri per messaggi che contengono **"ObjectType": "DeviceInfo"** e li inoltra toohello **EventProcessorHost** host istanza in esecuzione in un processo web.</span><span class="sxs-lookup"><span data-stu-id="90f72-177">hello **DeviceInfo** stream analytics job filters for messages that contain **"ObjectType": "DeviceInfo"** and forwards them toohello **EventProcessorHost** host instance that runs in a web job.</span></span> <span data-ttu-id="90f72-178">Logica di hello **EventProcessorHost** istanza utilizza i record del dispositivo id toofind hello Cosmos DB hello per record hello dispositivo e di aggiornamento specifico hello.</span><span class="sxs-lookup"><span data-stu-id="90f72-178">Logic in hello **EventProcessorHost** instance uses hello device id toofind hello Cosmos DB record for hello specific device and update hello record.</span></span>

> [!NOTE]
> <span data-ttu-id="90f72-179">Un messaggio informativo sul dispositivo è un messaggio standard inviato dal dispositivo al cloud.</span><span class="sxs-lookup"><span data-stu-id="90f72-179">A device information message is a standard device-to-cloud message.</span></span> <span data-ttu-id="90f72-180">soluzione Hello viene fatta distinzione tra i messaggi informativi di dispositivo e i messaggi di dati di telemetria tramite query ASA.</span><span class="sxs-lookup"><span data-stu-id="90f72-180">hello solution distinguishes between device information messages and telemetry messages by using ASA queries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90f72-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="90f72-181">Next steps</span></span>

<span data-ttu-id="90f72-182">Dopo aver apprendere come personalizzare soluzioni hello preconfigurato, è possibile esplorare alcune hello altre caratteristiche e funzionalità di soluzioni di IoT Suite preconfigurato hello:</span><span class="sxs-lookup"><span data-stu-id="90f72-182">Now you've finished learning how you can customize hello preconfigured solutions, you can explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="90f72-183">[Panoramica della soluzione preconfigurata di manutenzione predittiva][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="90f72-183">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* <span data-ttu-id="90f72-184">[Domande frequenti su IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="90f72-184">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="90f72-185">[Sicurezza di IoT da hello messa a terra][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="90f72-185">[IoT security from hello ground up][lnk-security-groundup]</span></span>

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
