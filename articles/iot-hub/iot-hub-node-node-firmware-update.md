---
title: Aggiornamento firmware del dispositivo con l'hub IoT di Azure (Node) | Documentazione Microsoft
description: Come usare la gestione dei dispositivi nell'hub IoT di Azure per avviare un aggiornamento del firmware del dispositivo. Usare Azure IoT SDK per Node.js per implementare un'app per dispositivo simulato e un'app di servizio che attiva l'aggiornamento del firmware.
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 350cf1cbec8847d1bbf29814435502af6f098e54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-device-management-to-initiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="d5d22-104">Usare la gestione dei dispositivi per avviare un aggiornamento del firmware del dispositivo (Node/Node)</span><span class="sxs-lookup"><span data-stu-id="d5d22-104">Use device management to initiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="d5d22-105">Introduzione</span><span class="sxs-lookup"><span data-stu-id="d5d22-105">Introduction</span></span>
<span data-ttu-id="d5d22-106">Nell'esercitazione [Introduzione alla gestione dei dispositivi][lnk-dm-getstarted] è stato illustrato come usare il [dispositivo gemello][lnk-devtwin] e le primitive dei [metodi diretti][lnk-c2dmethod] per riavviare un dispositivo in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="d5d22-106">In the [Get started with device management][lnk-dm-getstarted] tutorial, you saw how to use the [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives to remotely reboot a device.</span></span> <span data-ttu-id="d5d22-107">Questa esercitazione usa le stesse primitive dell'hub IoT, offre indicazioni e illustra come eseguire un aggiornamento del firmware simulato completo.</span><span class="sxs-lookup"><span data-stu-id="d5d22-107">This tutorial uses the same IoT Hub primitives and provides guidance and shows you how to do an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="d5d22-108">Questo schema viene usato nell'implementazione dell'aggiornamento del firmware per il dispositivo di esempio Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="d5d22-108">This pattern is used in the firmware update implementation for the Intel Edison device sample.</span></span>

<span data-ttu-id="d5d22-109">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="d5d22-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="d5d22-110">Creare un'app console Node.js che chiama il metodo diretto firmwareUpdate nell'app per dispositivo simulato tramite l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d5d22-110">Create a Node.js console app that calls the firmwareUpdate direct method in the simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="d5d22-111">Creare un'app di dispositivo simulato che implementa un metodo diretto **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="d5d22-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="d5d22-112">Questo metodo avvia un processo in più fasi che attende di scaricare l'immagine del firmware, quindi la scarica e infine la applica.</span><span class="sxs-lookup"><span data-stu-id="d5d22-112">This method initiates a multi-stage process that waits to download the firmware image, downloads the firmware image, and finally applies the firmware image.</span></span> <span data-ttu-id="d5d22-113">Durante l'esecuzione di ogni fase, il dispositivo usa le proprietà segnalate per aggiornare lo stato.</span><span class="sxs-lookup"><span data-stu-id="d5d22-113">During each stage of the update, the device uses the reported properties to report on progress.</span></span>

<span data-ttu-id="d5d22-114">Al termine di questa esercitazione si avranno due app console Node.js:</span><span class="sxs-lookup"><span data-stu-id="d5d22-114">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="d5d22-115">**dmpatterns_fwupdate_service.js**, che chiama un metodo diretto nell'app per dispositivo simulato, visualizza la risposta e visualizza regolarmente (ogni 500 ms) le proprietà segnalate aggiornate.</span><span class="sxs-lookup"><span data-stu-id="d5d22-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in the simulated device app, displays the response, and periodically (every 500ms) displays the updated reported properties.</span></span>

<span data-ttu-id="d5d22-116">**dmpatterns_fwupdate_device.js**, che connette all'hub IoT con l'identità del dispositivo creata prima, riceve un metodo diretto firmwareUpdate, esegue un processo in più stati per simulare un aggiornamento del firmware, inclusi l'attesa del download dell'immagine, il download della nuova immagine e infine l'applicazione dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="d5d22-116">**dmpatterns_fwupdate_device.js**, which connects to your IoT hub with the device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process to simulate a firmware update including: waiting for the image download, downloading the new image, and finally applying the image.</span></span>

<span data-ttu-id="d5d22-117">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d5d22-117">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="d5d22-118">Node.js 0.12.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="d5d22-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="d5d22-119">[Prepare your development environment][lnk-dev-setup] (Preparare l'ambiente di sviluppo) descrive come installare Node.js per questa esercitazione in Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="d5d22-119">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="d5d22-120">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="d5d22-120">An active Azure account.</span></span> <span data-ttu-id="d5d22-121">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="d5d22-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="d5d22-122">Vedere l'articolo [Introduzione alla gestione dei dispositivi](iot-hub-node-node-device-management-get-started.md) per creare l'hub IoT e ottenere la stringa di connessione relativa.</span><span class="sxs-lookup"><span data-stu-id="d5d22-122">Follow the [Get started with device management](iot-hub-node-node-device-management-get-started.md) article to create your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-the-device-using-a-direct-method"></a><span data-ttu-id="d5d22-123">Attivare un aggiornamento del firmware remoto nel dispositivo con un metodo diretto</span><span class="sxs-lookup"><span data-stu-id="d5d22-123">Trigger a remote firmware update on the device using a direct method</span></span>
<span data-ttu-id="d5d22-124">In questa sezione viene creata un'app console Node.js che avvia un aggiornamento del firmware remoto in un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d5d22-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="d5d22-125">L'applicazione usa un metodo diretto per avviare l'aggiornamento e usa le query di dispositivo gemello per ottenere periodicamente lo stato di aggiornamento del firmware attivo.</span><span class="sxs-lookup"><span data-stu-id="d5d22-125">The app uses a direct method to initiate the update and uses device twin queries to periodically get the status of the active firmware update.</span></span>

1. <span data-ttu-id="d5d22-126">Creare una cartella vuota denominata **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="d5d22-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="d5d22-127">Nella cartella **triggerfwupdateondevice** creare un file package.json eseguendo questo comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="d5d22-127">In the **triggerfwupdateondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="d5d22-128">Accettare tutte le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="d5d22-128">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="d5d22-129">Al prompt dei comandi nella cartella **triggerfwupdateondevice** eseguire il comando seguente per installare il pacchetto SDK per dispositivi **azure-iothub** e il pacchetto **azure-iot-device-mqtt**:</span><span class="sxs-lookup"><span data-stu-id="d5d22-129">At your command prompt in the **triggerfwupdateondevice** folder, run the following command to install the **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="d5d22-130">Con un editor di testo creare un file **dmpatterns_getstarted_service.js** nella cartella **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="d5d22-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="d5d22-131">Aggiungere le istruzioni "require" seguenti all'inizio del file **dmpatterns_getstarted_service.js**:</span><span class="sxs-lookup"><span data-stu-id="d5d22-131">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="d5d22-132">Aggiungere le dichiarazioni di variabile seguenti e sostituire i valori segnaposto:</span><span class="sxs-lookup"><span data-stu-id="d5d22-132">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="d5d22-133">Aggiungere la funzione seguente per trovare e visualizzare il valore della proprietà segnalata da firmwareUpdate.</span><span class="sxs-lookup"><span data-stu-id="d5d22-133">Add the following function to find and display the value of the firmwareUpdate reported property.</span></span>
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. <span data-ttu-id="d5d22-134">Aggiungere la funzione seguente per richiamare il metodo firmwareUpdate per riavviare il dispositivo di destinazione:</span><span class="sxs-lookup"><span data-stu-id="d5d22-134">Add the following function to invoke the firmwareUpdate method to reboot the target device:</span></span>
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start the firmware update on the device: ' + err.message)
        } 
      });
    };
    ```
8. <span data-ttu-id="d5d22-135">Aggiungere infine la funzione seguente al codice per avviare la sequenza di aggiornamento del firmware e la visualizzazione periodica delle proprietà segnalate:</span><span class="sxs-lookup"><span data-stu-id="d5d22-135">Finally, Add the following function to code to start the firmware update sequence and start periodically showing the reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="d5d22-136">Salvare e chiudere il file **dmpatterns_fwupdate_service.js**.</span><span class="sxs-lookup"><span data-stu-id="d5d22-136">Save and close the **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-the-apps"></a><span data-ttu-id="d5d22-137">Eseguire le app</span><span class="sxs-lookup"><span data-stu-id="d5d22-137">Run the apps</span></span>
<span data-ttu-id="d5d22-138">A questo punto è possibile eseguire le app.</span><span class="sxs-lookup"><span data-stu-id="d5d22-138">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="d5d22-139">Al prompt dei comandi nella cartella **manageddevice** eseguire questo comando per iniziare l'ascolto del metodo diretto di riavvio.</span><span class="sxs-lookup"><span data-stu-id="d5d22-139">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="d5d22-140">Al prompt dei comandi nella cartella **triggerfwupdateondevice** eseguire questo comando per attivare il riavvio remoto e cercare il dispositivo gemello per trovare l'ora dell'ultimo riavvio.</span><span class="sxs-lookup"><span data-stu-id="d5d22-140">At the command prompt in the **triggerfwupdateondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="d5d22-141">Nella console viene visualizzata la risposta del dispositivo al metodo diretto.</span><span class="sxs-lookup"><span data-stu-id="d5d22-141">You see the device response to the direct method in the console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5d22-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d5d22-142">Next steps</span></span>
<span data-ttu-id="d5d22-143">In questa esercitazione è stato usato un metodo diretto per attivare un aggiornamento del firmware remoto in un dispositivo e sono state usate le proprietà segnalate per conoscere lo stato del processo di aggiornamento del firmware.</span><span class="sxs-lookup"><span data-stu-id="d5d22-143">In this tutorial, you used a direct method to trigger a remote firmware update on a device and used the reported properties to follow the progress of the firmware update.</span></span>

<span data-ttu-id="d5d22-144">Per informazioni su come estendere la soluzione IoT e pianificare le chiamate al metodo su più dispositivi, vedere l'esercitazione [Pianificare e trasmettere processi][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="d5d22-144">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
