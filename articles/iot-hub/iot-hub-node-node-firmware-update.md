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
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a>Usare Gestione di dispositivi tooinitiate un aggiornamento del firmware del dispositivo (nodo)
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>Introduzione
In hello [iniziare con la gestione dei dispositivi] [ lnk-dm-getstarted] esercitazione, si è visto come hello toouse [doppi dispositivo] [ lnk-devtwin] e [diretto metodi] [ lnk-c2dmethod] tooremotely primitive riavviare un dispositivo. Questa esercitazione viene utilizzato hello stesse primitive IoT Hub e vengono fornite informazioni aggiuntive e Mostra come toodo un end-to-end simulato l'aggiornamento del firmware.  Questo modello è usato nell'implementazione di aggiornamento del firmware hello per: esempio hello Intel Edison dispositivo.

Questa esercitazione illustra come:

* Creare un'applicazione console Node. js che chiama hello firmwareUpdate dirette del metodo nell'app dispositivo simulato hello tramite l'hub IoT.
* Creare un'app di dispositivo simulato che implementa un metodo diretto **firmwareUpdate**. Questo metodo avvia un processo a più fasi che attende l'immagine di firmware hello toodownload, scarica l'immagine del firmware hello e infine applica immagine del firmware hello. Durante ogni fase dell'aggiornamento hello hello dispositivo utilizza hello segnalato tooreport proprietà sullo stato di avanzamento.

Alla fine di hello di questa esercitazione, si dispongono di due applicazioni di console Node.js:

**dmpatterns_fwupdate_service.js**, che chiama un metodo diretto in app hello dispositivo simulato, Visualizza la risposta hello e periodicamente (ogni 500ms) consente di visualizzare hello aggiornato segnalati proprietà.

**dmpatterns_fwupdate_device.js**, che connette l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza, riceve un metodo diretto firmwareUpdate, viene eseguito tramite un processo più stati di toosimulate un aggiornamento del firmware tra: in attesa di hello immagine di scaricare, download hello nuova immagine e infine applica immagine hello.

toocomplete questa esercitazione, è necessario hello seguenti:

* Node.js 0.12.x o versione successiva. <br/>  [Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall Node.js per questa esercitazione su Windows o Linux.
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

Seguire hello [iniziare con la gestione dei dispositivi](iot-hub-node-node-device-management-get-started.md) articolo toocreate l'hub IoT e ottenere la stringa di connessione IoT Hub.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>Attivare un aggiornamento del firmware remota sul dispositivo hello utilizzando un metodo diretto
In questa sezione viene creata un'app console Node.js che avvia un aggiornamento del firmware remoto in un dispositivo. utilizza dispositivo doppi query tooperiodically ottenere lo stato di hello dell'aggiornamento del firmware active hello app Hello utilizza un aggiornamento di hello tooinitiate dirette del metodo.

1. Creare una cartella vuota denominata **triggerfwupdateondevice**.  In hello **triggerfwupdateondevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.  Accettare tutte le impostazioni predefinite hello:
   
    ```
    npm init
    ```
2. Al prompt dei comandi in hello **triggerfwupdateondevice** cartella, eseguire hello successivo comando tooinstall hello **hub iot di azure** e **mqtt azure-iot-dispositivo** dispositivo Pacchetti SDK:
   
    ```
    npm install azure-iothub --save
    ```
3. Utilizzando un editor di testo, creare un **dmpatterns_getstarted_service.js** file hello **triggerfwupdateondevice** cartella.
4. Aggiungere i seguenti hello 'richiedono' istruzioni all'inizio di hello di hello **dmpatterns_getstarted_service.js** file:
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. Aggiungere hello dopo le dichiarazioni di variabili e sostituire i valori segnaposto hello:
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. Aggiungere i seguenti hello funzionano toofind e visualizzare il valore di hello di hello firmwareUpdate segnalati proprietà.
   
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
7. Aggiungere hello seguente funzione tooinvoke hello firmwareUpdate metodo tooreboot hello dispositivo di destinazione:
   
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
8. Infine, seguente hello Aggiungi funzione sequenza di aggiornamento del firmware toocode toostart hello e visualizzazione periodicamente hello segnalati proprietà:
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. Salvare e chiudere hello **dmpatterns_fwupdate_service.js** file.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Eseguire App hello
Si è ora pronto toorun hello app.

1. Al prompt dei comandi di hello in hello **manageddevice** cartella, eseguire hello successivo comando toobegin in attesa di hello riavvio dirette del metodo.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. Al prompt dei comandi di hello in hello **triggerfwupdateondevice** cartella, eseguire hello successivo comando tootrigger hello remoto riavviare il computer ed eseguire query per hello toofind gemelli di hello dispositivo riavviare ultima volta.
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. Vedrai hello dispositivo risposta toohello metodo diretto nella console di hello.

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, è stato utilizzato un tootrigger dirette del metodo remota aggiornamento del firmware su un dispositivo e hello utilizzato nel report di stato di hello toofollow le proprietà di aggiornamento del firmware hello.

toolearn come tooextend il metodo di pianificazione e di soluzione IoT chiama su più dispositivi, vedere hello [pianificazione e i processi di broadcast] [ lnk-tutorial-jobs] esercitazione.

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
