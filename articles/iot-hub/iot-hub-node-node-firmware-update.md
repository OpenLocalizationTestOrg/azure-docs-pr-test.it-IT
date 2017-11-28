---
title: aggiornamento del firmware aaaDevice con l'IoT Hub Azure (nodo) | Documenti Microsoft
description: "Come aggiornare la gestione dei dispositivi toouse su Azure IoT Hub tooinitiate un firmware del dispositivo. È consigliabile utilizzare hello Azure IoT SDK per Node.js tooimplement un'app dispositivo simulato e un'applicazione di servizio che attiva l'aggiornamento del firmware hello."
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
ms.openlocfilehash: 99d4b369e7aba334bf713e0c657e6e5d227fb691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="dfc78-104">Usare Gestione di dispositivi tooinitiate un aggiornamento del firmware del dispositivo (nodo)</span><span class="sxs-lookup"><span data-stu-id="dfc78-104">Use device management tooinitiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="dfc78-105">Introduzione</span><span class="sxs-lookup"><span data-stu-id="dfc78-105">Introduction</span></span>
<span data-ttu-id="dfc78-106">In hello [iniziare con la gestione dei dispositivi] [ lnk-dm-getstarted] esercitazione, si è visto come hello toouse [doppi dispositivo] [ lnk-devtwin] e [diretto metodi] [ lnk-c2dmethod] tooremotely primitive riavviare un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dfc78-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="dfc78-107">Questa esercitazione viene utilizzato hello stesse primitive IoT Hub e vengono fornite informazioni aggiuntive e Mostra come toodo un end-to-end simulato l'aggiornamento del firmware.</span><span class="sxs-lookup"><span data-stu-id="dfc78-107">This tutorial uses hello same IoT Hub primitives and provides guidance and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="dfc78-108">Questo modello è usato nell'implementazione di aggiornamento del firmware hello per: esempio hello Intel Edison dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dfc78-108">This pattern is used in hello firmware update implementation for hello Intel Edison device sample.</span></span>

<span data-ttu-id="dfc78-109">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="dfc78-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="dfc78-110">Creare un'applicazione console Node. js che chiama hello firmwareUpdate dirette del metodo nell'app dispositivo simulato hello tramite l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="dfc78-110">Create a Node.js console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="dfc78-111">Creare un'app di dispositivo simulato che implementa un metodo diretto **firmwareUpdate**.</span><span class="sxs-lookup"><span data-stu-id="dfc78-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="dfc78-112">Questo metodo avvia un processo a più fasi che attende l'immagine di firmware hello toodownload, scarica l'immagine del firmware hello e infine applica immagine del firmware hello.</span><span class="sxs-lookup"><span data-stu-id="dfc78-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="dfc78-113">Durante ogni fase dell'aggiornamento hello hello dispositivo utilizza hello segnalato tooreport proprietà sullo stato di avanzamento.</span><span class="sxs-lookup"><span data-stu-id="dfc78-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="dfc78-114">Alla fine di hello di questa esercitazione, si dispongono di due applicazioni di console Node.js:</span><span class="sxs-lookup"><span data-stu-id="dfc78-114">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="dfc78-115">**dmpatterns_fwupdate_service.js**, che chiama un metodo diretto in app hello dispositivo simulato, Visualizza la risposta hello e periodicamente (ogni 500ms) consente di visualizzare hello aggiornato segnalati proprietà.</span><span class="sxs-lookup"><span data-stu-id="dfc78-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="dfc78-116">**dmpatterns_fwupdate_device.js**, che connette l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza, riceve un metodo diretto firmwareUpdate, viene eseguito tramite un processo più stati di toosimulate un aggiornamento del firmware tra: in attesa di hello immagine di scaricare, download hello nuova immagine e infine applica immagine hello.</span><span class="sxs-lookup"><span data-stu-id="dfc78-116">**dmpatterns_fwupdate_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="dfc78-117">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="dfc78-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="dfc78-118">Node.js 0.12.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="dfc78-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="dfc78-119">[Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall Node.js per questa esercitazione su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="dfc78-119">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="dfc78-120">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="dfc78-120">An active Azure account.</span></span> <span data-ttu-id="dfc78-121">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="dfc78-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="dfc78-122">Seguire hello [iniziare con la gestione dei dispositivi](iot-hub-node-node-device-management-get-started.md) articolo toocreate l'hub IoT e ottenere la stringa di connessione IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="dfc78-122">Follow hello [Get started with device management](iot-hub-node-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="dfc78-123">Attivare un aggiornamento del firmware remota sul dispositivo hello utilizzando un metodo diretto</span><span class="sxs-lookup"><span data-stu-id="dfc78-123">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="dfc78-124">In questa sezione viene creata un'app console Node.js che avvia un aggiornamento del firmware remoto in un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="dfc78-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="dfc78-125">utilizza dispositivo doppi query tooperiodically ottenere lo stato di hello dell'aggiornamento del firmware active hello app Hello utilizza un aggiornamento di hello tooinitiate dirette del metodo.</span><span class="sxs-lookup"><span data-stu-id="dfc78-125">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="dfc78-126">Creare una cartella vuota denominata **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="dfc78-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="dfc78-127">In hello **triggerfwupdateondevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="dfc78-127">In hello **triggerfwupdateondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="dfc78-128">Accettare tutte le impostazioni predefinite hello:</span><span class="sxs-lookup"><span data-stu-id="dfc78-128">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="dfc78-129">Al prompt dei comandi in hello **triggerfwupdateondevice** cartella, eseguire hello successivo comando tooinstall hello **hub iot di azure** e **mqtt azure-iot-dispositivo** dispositivo Pacchetti SDK:</span><span class="sxs-lookup"><span data-stu-id="dfc78-129">At your command prompt in hello **triggerfwupdateondevice** folder, run hello following command tooinstall hello **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="dfc78-130">Utilizzando un editor di testo, creare un **dmpatterns_getstarted_service.js** file hello **triggerfwupdateondevice** cartella.</span><span class="sxs-lookup"><span data-stu-id="dfc78-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="dfc78-131">Aggiungere i seguenti hello 'richiedono' istruzioni all'inizio di hello di hello **dmpatterns_getstarted_service.js** file:</span><span class="sxs-lookup"><span data-stu-id="dfc78-131">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="dfc78-132">Aggiungere hello dopo le dichiarazioni di variabili e sostituire i valori segnaposto hello:</span><span class="sxs-lookup"><span data-stu-id="dfc78-132">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="dfc78-133">Aggiungere i seguenti hello funzionano toofind e visualizzare il valore di hello di hello firmwareUpdate segnalati proprietà.</span><span class="sxs-lookup"><span data-stu-id="dfc78-133">Add hello following function toofind and display hello value of hello firmwareUpdate reported property.</span></span>
   
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
7. <span data-ttu-id="dfc78-134">Aggiungere hello seguente funzione tooinvoke hello firmwareUpdate metodo tooreboot hello dispositivo di destinazione:</span><span class="sxs-lookup"><span data-stu-id="dfc78-134">Add hello following function tooinvoke hello firmwareUpdate method tooreboot hello target device:</span></span>
   
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
          console.error('Could not start hello firmware update on hello device: ' + err.message)
        } 
      });
    };
    ```
8. <span data-ttu-id="dfc78-135">Infine, seguente hello Aggiungi funzione sequenza di aggiornamento del firmware toocode toostart hello e visualizzazione periodicamente hello segnalati proprietà:</span><span class="sxs-lookup"><span data-stu-id="dfc78-135">Finally, Add hello following function toocode toostart hello firmware update sequence and start periodically showing hello reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="dfc78-136">Salvare e chiudere hello **dmpatterns_fwupdate_service.js** file.</span><span class="sxs-lookup"><span data-stu-id="dfc78-136">Save and close hello **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="dfc78-137">Eseguire App hello</span><span class="sxs-lookup"><span data-stu-id="dfc78-137">Run hello apps</span></span>
<span data-ttu-id="dfc78-138">Si è ora pronto toorun hello app.</span><span class="sxs-lookup"><span data-stu-id="dfc78-138">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="dfc78-139">Al prompt dei comandi di hello in hello **manageddevice** cartella, eseguire hello successivo comando toobegin in attesa di hello riavvio dirette del metodo.</span><span class="sxs-lookup"><span data-stu-id="dfc78-139">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="dfc78-140">Al prompt dei comandi di hello in hello **triggerfwupdateondevice** cartella, eseguire hello successivo comando tootrigger hello remoto riavviare il computer ed eseguire query per hello toofind gemelli di hello dispositivo riavviare ultima volta.</span><span class="sxs-lookup"><span data-stu-id="dfc78-140">At hello command prompt in hello **triggerfwupdateondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="dfc78-141">Vedrai hello dispositivo risposta toohello metodo diretto nella console di hello.</span><span class="sxs-lookup"><span data-stu-id="dfc78-141">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfc78-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dfc78-142">Next steps</span></span>
<span data-ttu-id="dfc78-143">In questa esercitazione, è stato utilizzato un tootrigger dirette del metodo remota aggiornamento del firmware su un dispositivo e hello utilizzato nel report di stato di hello toofollow le proprietà di aggiornamento del firmware hello.</span><span class="sxs-lookup"><span data-stu-id="dfc78-143">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="dfc78-144">toolearn come tooextend il metodo di pianificazione e di soluzione IoT chiama su più dispositivi, vedere hello [pianificazione e i processi di broadcast] [ lnk-tutorial-jobs] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="dfc78-144">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
