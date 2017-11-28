---
title: aaaGet avviato con l'IoT Hub Azure (nodo) | Documenti Microsoft
description: Informazioni su come toosend dispositivo a cloud messaggi tooAzure IoT Hub tramite IoT SDK per Node.js. Creare dispositivo simulato e servizio App tooregister il dispositivo, inviare messaggi e leggere messaggi da hub IoT.
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0747895365f2359a9c38ea1e85a5881d6efec0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a><span data-ttu-id="950db-104">Connessione hub IoT tooyour dispositivo simulato utilizzando nodo</span><span class="sxs-lookup"><span data-stu-id="950db-104">Connect your simulated device tooyour IoT hub using Node</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="950db-105">Alla fine di hello di questa esercitazione, si dispongono di tre applicazioni di console Node.js:</span><span class="sxs-lookup"><span data-stu-id="950db-105">At hello end of this tutorial, you have three Node.js console apps:</span></span>

* <span data-ttu-id="950db-106">**CreateDeviceIdentity.js**, che consente di creare un'identità del dispositivo e protezione della chiave tooconnect app dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="950db-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="950db-107">**ReadDeviceToCloudMessages.js**, che consente di visualizzare dati di telemetria hello inviati dall'app dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="950db-107">**ReadDeviceToCloudMessages.js**, which displays hello telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="950db-108">**SimulatedDevice.js**, che collega l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza e invia un messaggio di dati di telemetria ogni secondo utilizzando hello protocollo MQTT.</span><span class="sxs-lookup"><span data-stu-id="950db-108">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="950db-109">articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] vengono fornite informazioni hello Azure IoT SDK che è possibile utilizzare toobuild toorun entrambe le applicazioni in dispositivi e la soluzione di back-end.</span><span class="sxs-lookup"><span data-stu-id="950db-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="950db-110">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="950db-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="950db-111">Node.js 0.10.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="950db-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="950db-112">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="950db-112">An active Azure account.</span></span> <span data-ttu-id="950db-113">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="950db-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="950db-114">L'hub IoT è stato creato.</span><span class="sxs-lookup"><span data-stu-id="950db-114">You have now created your IoT hub.</span></span> <span data-ttu-id="950db-115">È necessario hello nome host dell'IoT Hub e hello stringa di connessione IoT Hub che è necessario rest hello toocomplete di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="950db-115">You have hello IoT Hub host name and hello IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="950db-116">Creare un'identità del dispositivo</span><span class="sxs-lookup"><span data-stu-id="950db-116">Create a device identity</span></span>
<span data-ttu-id="950db-117">In questa sezione si crea un'applicazione console Node.js che crea un'identità del dispositivo nel Registro di sistema di hello identità nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="950db-117">In this section, you create a Node.js console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="950db-118">Un dispositivo può connettersi solo hub tooIoT se dispone di una voce del Registro di sistema di hello identità.</span><span class="sxs-lookup"><span data-stu-id="950db-118">A device can only connect tooIoT hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="950db-119">Per ulteriori informazioni, vedere hello **Registro di sistema di identità** sezione di hello [Guida per sviluppatori di IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="950db-119">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="950db-120">Quando si esegue questa app console, viene generato un ID univoco del dispositivo e chiave che il dispositivo può usare tooidentify stesso quando vengono inviati al dispositivo a cloud messaggi tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="950db-120">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="950db-121">Creare una nuova cartella vuota denominata **createdeviceidentity**.</span><span class="sxs-lookup"><span data-stu-id="950db-121">Create a new empty folder called **createdeviceidentity**.</span></span> <span data-ttu-id="950db-122">In hello **createdeviceidentity** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="950db-122">In hello **createdeviceidentity** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="950db-123">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="950db-123">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="950db-124">Al prompt dei comandi in hello **createdeviceidentity** cartella, eseguire hello successivo comando tooinstall hello **hub IOT di azure** pacchetto SDK del servizio:</span><span class="sxs-lookup"><span data-stu-id="950db-124">At your command prompt in hello **createdeviceidentity** folder, run hello following command tooinstall hello **azure-iothub** Service SDK package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="950db-125">Utilizzando un editor di testo, creare un **CreateDeviceIdentity.js** file hello **createdeviceidentity** cartella.</span><span class="sxs-lookup"><span data-stu-id="950db-125">Using a text editor, create a **CreateDeviceIdentity.js** file in hello **createdeviceidentity** folder.</span></span>
4. <span data-ttu-id="950db-126">Aggiungere il seguente hello `require` istruzione all'inizio di hello di hello **CreateDeviceIdentity.js** file:</span><span class="sxs-lookup"><span data-stu-id="950db-126">Add hello following `require` statement at hello start of hello **CreateDeviceIdentity.js** file:</span></span>
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. <span data-ttu-id="950db-127">Aggiungere i seguenti toohello codice hello **CreateDeviceIdentity.js** file e sostituire il valore di segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello hello:</span><span class="sxs-lookup"><span data-stu-id="950db-127">Add hello following code toohello **CreateDeviceIdentity.js** file and replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello previous section:</span></span> 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="950db-128">Aggiungere hello seguente codice toocreate una definizione di dispositivo nel Registro di sistema di hello identità nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="950db-128">Add hello following code toocreate a device definition in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="950db-129">Questo codice crea un dispositivo se l'ID dispositivo hello non esiste nel Registro di sistema di hello identità, in caso contrario restituisce chiave hello del dispositivo esistente hello:</span><span class="sxs-lookup"><span data-stu-id="950db-129">This code creates a device if hello device ID does not exist in hello identity registry, otherwise it returns hello key of hello existing device:</span></span>
   
    ```
    var device = {
      deviceId: 'myFirstNodeDevice'
    }
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="950db-130">Salvare e chiudere il file **CreateDeviceIdentity.js** .</span><span class="sxs-lookup"><span data-stu-id="950db-130">Save and close **CreateDeviceIdentity.js** file.</span></span>
8. <span data-ttu-id="950db-131">hello toorun **createdeviceidentity** applicazione, eseguire hello comando al prompt dei comandi di hello nella cartella createdeviceidentity hello seguente:</span><span class="sxs-lookup"><span data-stu-id="950db-131">toorun hello **createdeviceidentity** application, execute hello following command at hello command prompt in hello createdeviceidentity folder:</span></span>
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. <span data-ttu-id="950db-132">Prendere nota di hello **ID dispositivo** e **chiave dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="950db-132">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="950db-133">Questi valori è necessario in un secondo momento quando si crea un'applicazione che si connette tooIoT Hub come un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="950db-133">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="950db-134">Hello del Registro di sistema di IoT Hub identità archivia solo hub IoT toohello di dispositivo identità tooenable proteggere l'accesso.</span><span class="sxs-lookup"><span data-stu-id="950db-134">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="950db-135">Archivia toouse di chiavi e l'ID dispositivo come credenziali di sicurezza e un flag di abilitazione/disabilitazione che è possibile utilizzare toodisable accesso per un singolo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="950db-135">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="950db-136">Se l'applicazione deve toostore altri metadati specifici del dispositivo, deve utilizzare un archivio specifici dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="950db-136">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="950db-137">Per ulteriori informazioni, vedere hello [Guida per sviluppatori di IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="950db-137">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="950db-138">Ricezione di messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="950db-138">Receive device-to-cloud messages</span></span>
<span data-ttu-id="950db-139">In questa sezione si creerà un'app console di Node.js che legge i messaggi da dispositivo a cloud dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="950db-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="950db-140">Un hub IoT espone un [hub eventi][lnk-event-hubs-overview]-tooenable endpoint compatibile per i messaggi da dispositivo a cloud tooread.</span><span class="sxs-lookup"><span data-stu-id="950db-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="950db-141">cose tookeep semplice, in questa esercitazione consente di creare un lettore di base che non è adatto per una distribuzione di velocità effettiva elevata.</span><span class="sxs-lookup"><span data-stu-id="950db-141">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="950db-142">Hello [elaborare i messaggi da dispositivo a cloud] [ lnk-process-d2c-tutorial] esercitazione viene illustrato come tooprocess dispositivo a cloud messaggi su larga scala.</span><span class="sxs-lookup"><span data-stu-id="950db-142">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="950db-143">Hello [Introduzione agli hub di eventi] [ lnk-eventhubs-tutorial] esercitazione fornisce ulteriori informazioni su come tooprocess messaggi dagli hub eventi ed è applicabile toohello gli endpoint Hub IoT Hub eventi compatibile.</span><span class="sxs-lookup"><span data-stu-id="950db-143">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="950db-144">Hello Hub eventi compatibile con l'endpoint per la lettura dei messaggi da dispositivo a cloud sempre Usa protocollo AMQP hello.</span><span class="sxs-lookup"><span data-stu-id="950db-144">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="950db-145">Creare una cartella vuota denominata **readdevicetocloudmessages**.</span><span class="sxs-lookup"><span data-stu-id="950db-145">Create an empty folder called **readdevicetocloudmessages**.</span></span> <span data-ttu-id="950db-146">In hello **readdevicetocloudmessages** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="950db-146">In hello **readdevicetocloudmessages** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="950db-147">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="950db-147">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="950db-148">Al prompt dei comandi in hello **readdevicetocloudmessages** cartella, eseguire hello successivo comando tooinstall hello **hub di eventi di azure** pacchetto:</span><span class="sxs-lookup"><span data-stu-id="950db-148">At your command prompt in hello **readdevicetocloudmessages** folder, run hello following command tooinstall hello **azure-event-hubs** package:</span></span>
   
    ```
    npm install azure-event-hubs --save
    ```
3. <span data-ttu-id="950db-149">Utilizzando un editor di testo, creare un **ReadDeviceToCloudMessages.js** file hello **readdevicetocloudmessages** cartella.</span><span class="sxs-lookup"><span data-stu-id="950db-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in hello **readdevicetocloudmessages** folder.</span></span>
4. <span data-ttu-id="950db-150">Aggiungere il seguente hello `require` istruzioni hello iniziano hello **ReadDeviceToCloudMessages.js** file:</span><span class="sxs-lookup"><span data-stu-id="950db-150">Add hello following `require` statements at hello start of hello **ReadDeviceToCloudMessages.js** file:</span></span>
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. <span data-ttu-id="950db-151">Aggiungere hello seguente dichiarazione di variabile e sostituire il valore di segnaposto hello con stringa di connessione IoT Hub per l'hub hello:</span><span class="sxs-lookup"><span data-stu-id="950db-151">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. <span data-ttu-id="950db-152">Aggiungere i seguenti due funzioni della console di output toohello stampa hello:</span><span class="sxs-lookup"><span data-stu-id="950db-152">Add hello following two functions that print output toohello console:</span></span>
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. <span data-ttu-id="950db-153">Aggiungere i seguenti hello toocreate codice hello **EventHubClient**, aprire hello connessione tooyour IoT Hub e creare un ricevitore per ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="950db-153">Add hello following code toocreate hello **EventHubClient**, open hello connection tooyour IoT Hub, and create a receiver for each partition.</span></span> <span data-ttu-id="950db-154">L'applicazione utilizza un filtro durante la creazione di un destinatario in modo che hello ricevitore legge solo i messaggi inviati tooIoT Hub dopo ricevitore hello viene avviata l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="950db-154">This application uses a filter when it creates a receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="950db-155">Questo filtro è utile in un ambiente di test in modo che solo hello set corrente di messaggi.</span><span class="sxs-lookup"><span data-stu-id="950db-155">This filter is useful in a test environment so you see just hello current set of messages.</span></span> <span data-ttu-id="950db-156">In un ambiente di produzione, il codice deve verificare che vengano elaborati tutti i messaggi hello.</span><span class="sxs-lookup"><span data-stu-id="950db-156">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="950db-157">Per ulteriori informazioni, vedere hello [come i messaggi da dispositivo a cloud IoT Hub tooprocess] [ lnk-process-d2c-tutorial] esercitazione:</span><span class="sxs-lookup"><span data-stu-id="950db-157">For more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span></span>
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. <span data-ttu-id="950db-158">Salvare e chiudere hello **ReadDeviceToCloudMessages.js** file.</span><span class="sxs-lookup"><span data-stu-id="950db-158">Save and close hello **ReadDeviceToCloudMessages.js** file.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="950db-159">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="950db-159">Create a simulated device app</span></span>
<span data-ttu-id="950db-160">In questa sezione si crea un'applicazione console Node. js che simula un dispositivo che invia l'hub IoT tooan messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="950db-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="950db-161">Creare una cartella vuota denominata **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="950db-161">Create an empty folder called **simulateddevice**.</span></span> <span data-ttu-id="950db-162">In hello **simulateddevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="950db-162">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="950db-163">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="950db-163">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="950db-164">Al prompt dei comandi in hello **simulateddevice** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** pacchetto SDK di dispositivo e **azure-iot-dispositivo-mqtt**pacchetto:</span><span class="sxs-lookup"><span data-stu-id="950db-164">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="950db-165">Utilizzando un editor di testo, creare un **SimulatedDevice.js** file hello **simulateddevice** cartella.</span><span class="sxs-lookup"><span data-stu-id="950db-165">Using a text editor, create a **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="950db-166">Aggiungere il seguente hello `require` istruzioni hello iniziano hello **SimulatedDevice.js** file:</span><span class="sxs-lookup"><span data-stu-id="950db-166">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. <span data-ttu-id="950db-167">Aggiungere un **connectionString** variabile e usarlo toocreate un **Client** istanza.</span><span class="sxs-lookup"><span data-stu-id="950db-167">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="950db-168">Sostituire **{youriothostname}** con nome hello dell'hub IoT hello creato hello *creare un IoT Hub* sezione.</span><span class="sxs-lookup"><span data-stu-id="950db-168">Replace **{youriothostname}** with hello name of hello IoT hub you created hello *Create an IoT Hub* section.</span></span> <span data-ttu-id="950db-169">Sostituire **{yourdevicekey}** con il valore della chiave di hello dispositivo è stato generato in hello *creare un'identità del dispositivo* sezione:</span><span class="sxs-lookup"><span data-stu-id="950db-169">Replace **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. <span data-ttu-id="950db-170">Aggiungere i seguenti output toodisplay funzione da un'applicazione hello hello:</span><span class="sxs-lookup"><span data-stu-id="950db-170">Add hello following function toodisplay output from hello application:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="950db-171">Creare un callback e utilizzare hello **setInterval** funzione toosend un hub IoT tooyour di messaggi al secondo:</span><span class="sxs-lookup"><span data-stu-id="950db-171">Create a callback and use hello **setInterval** function toosend a message tooyour IoT hub every second:</span></span>
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
        // Create a message and send it toohello IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
8. <span data-ttu-id="950db-172">Aprire hello connessione tooyour IoT Hub e avviare l'invio di messaggi:</span><span class="sxs-lookup"><span data-stu-id="950db-172">Open hello connection tooyour IoT Hub and start sending messages:</span></span>
   
    ```
    client.open(connectCallback);
    ```
9. <span data-ttu-id="950db-173">Salvare e chiudere hello **SimulatedDevice.js** file.</span><span class="sxs-lookup"><span data-stu-id="950db-173">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="950db-174">cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo.</span><span class="sxs-lookup"><span data-stu-id="950db-174">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="950db-175">Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="950db-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-hello-apps"></a><span data-ttu-id="950db-176">Eseguire App hello</span><span class="sxs-lookup"><span data-stu-id="950db-176">Run hello apps</span></span>
<span data-ttu-id="950db-177">Si è ora pronto toorun hello app.</span><span class="sxs-lookup"><span data-stu-id="950db-177">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="950db-178">Al prompt dei comandi in hello **readdevicetocloudmessages** cartella, eseguire hello monitoraggio l'hub IoT toobegin di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="950db-178">At a command prompt in hello **readdevicetocloudmessages** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Messaggi da dispositivo a cloud toomonitor di Node.js IoT Hub del servizio app][7]
2. <span data-ttu-id="950db-180">Al prompt dei comandi in hello **simulateddevice** cartella, eseguire hello toobegin comando invio hub IoT tooyour dati di telemetria seguenti:</span><span class="sxs-lookup"><span data-stu-id="950db-180">At a command prompt in hello **simulateddevice** folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Messaggi da dispositivo a cloud di Node.js IoT Hub dispositivo app toosend][8]
3. <span data-ttu-id="950db-182">Hello **utilizzo** riquadro in hello [portale di Azure] [ lnk-portal] Mostra hello numero di messaggi inviati toohello hub IoT:</span><span class="sxs-lookup"><span data-stu-id="950db-182">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>
   
    ![Azure portale utilizzo riquadro mostra il numero di messaggi inviati tooIoT Hub][43]

## <a name="next-steps"></a><span data-ttu-id="950db-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="950db-184">Next steps</span></span>
<span data-ttu-id="950db-185">In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità.</span><span class="sxs-lookup"><span data-stu-id="950db-185">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="950db-186">È stato utilizzato questo dispositivo identità tooenable hello simulato dispositivo app toosend messaggi da dispositivo a cloud toohello hub IoT.</span><span class="sxs-lookup"><span data-stu-id="950db-186">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="950db-187">È stato creato anche un'applicazione che consente di visualizzare i messaggi hello ricevuti dall'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="950db-187">You also created an app that displays hello messages received by hello IoT hub.</span></span> 

<span data-ttu-id="950db-188">Guida introduttiva toocontinue con IoT Hub e tooexplore altri scenari IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="950db-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="950db-189">[Connessione del dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="950db-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="950db-190">[Introduzione alla gestione dei dispositivi][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="950db-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="950db-191">[Introduzione ad Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="950db-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="950db-192">toolearn tooextend vedere i messaggi di dispositivo a cloud processo e di soluzione IoT su larga scala, hello [elaborare i messaggi da dispositivo a cloud] [ lnk-process-d2c-tutorial] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="950db-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]


<!-- Images. -->
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
