---
title: aggiornamento del firmware aaaDevice con l'IoT Hub Azure (.NET/nodo) | Documenti Microsoft
description: Come aggiornare la gestione dei dispositivi toouse su Azure IoT Hub tooinitiate un firmware del dispositivo. Utilizzare il dispositivo di Azure IoT hello SDK per Node.js tooimplement un'app dispositivo simulato e hello Azure IoT servizio SDK per .NET tooimplement un'applicazione di servizio che attiva l'aggiornamento del firmware hello.
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
ms.date: 03/17/2017
ms.author: juanpere
ms.openlocfilehash: d48899651bcd5d67e577c971be0f9453c8f21592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-netnode"></a>Usare Gestione di dispositivi tooinitiate un aggiornamento del firmware del dispositivo (.NET/nodo)
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>Introduzione
In hello [iniziare con la gestione dei dispositivi] [ lnk-dm-getstarted] esercitazione, si è visto come hello toouse [doppi dispositivo] [ lnk-devtwin] e [diretto metodi] [ lnk-c2dmethod] tooremotely primitive riavviare un dispositivo. Questa esercitazione viene utilizzato hello stesse primitive Hub IoT e Mostra come toodo un end-to-end simulato l'aggiornamento del firmware.  Questo modello è usato nell'implementazione di aggiornamento del firmware hello per hello [esempio di implementazione dispositivo Pi Raspberry][lnk-rpi-implementation].

Questa esercitazione illustra come:

* Creare un'applicazione console .NET che chiama hello firmwareUpdate dirette del metodo nell'app dispositivo simulato hello tramite l'hub IoT.
* Creare un'app di dispositivo simulato che implementa un metodo diretto **firmwareUpdate**. Questo metodo avvia un processo a più fasi che attende l'immagine di firmware hello toodownload, scarica l'immagine del firmware hello e infine applica immagine del firmware hello. Durante ogni fase dell'aggiornamento hello hello dispositivo utilizza hello segnalato tooreport proprietà sullo stato di avanzamento.

Alla fine di hello di questa esercitazione, si dispone di un'applicazione console in Node.js dispositivo e un'applicazione back-end di console .NET (c#):

**dmpatterns_fwupdate_service.js**, che chiama un metodo diretto in app hello dispositivo simulato, Visualizza la risposta hello e periodicamente (ogni 500ms) consente di visualizzare hello aggiornato segnalati proprietà.

**TriggerFWUpdate**, che connette l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza, riceve un metodo diretto firmwareUpdate, viene eseguito tramite un processo più stati di toosimulate un aggiornamento del firmware tra: in attesa per il download dell'immagine hello Download nuova immagine hello e infine l'applicazione hello image.

toocomplete questa esercitazione, è necessario hello seguenti:

* Visual Studio 2015 o Visual Studio 2017.
* Node.js 0.12.x o versione successiva. <br/>  [Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall Node.js per questa esercitazione su Windows o Linux.
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

Seguire hello [iniziare con la gestione dei dispositivi](iot-hub-csharp-node-device-management-get-started.md) articolo toocreate l'hub IoT e ottenere la stringa di connessione IoT Hub.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>Attivare un aggiornamento del firmware remota sul dispositivo hello utilizzando un metodo diretto
In questa sezione viene creata un'app console .NET (tramite C#) che avvia un aggiornamento del firmware remoto in un dispositivo. utilizza dispositivo doppi query tooperiodically ottenere lo stato di hello dell'aggiornamento del firmware active hello app Hello utilizza un aggiornamento di hello tooinitiate dirette del metodo.

1. In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto. Progetto hello nome **TriggerFWUpdate**.

    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]

1. In Esplora soluzioni fare doppio clic su hello **TriggerFWUpdate** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .
1. In hello **Gestione pacchetti NuGet** selezionare **Sfoglia**, cercare **microsoft.azure.devices**selezionare **installare** tooinstall Hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso. Questa procedura Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.

    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
1. Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
1. Aggiungere i seguenti campi toohello hello **programma** classe. Sostituire hello hello di più valori segnaposto con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello e hello Id del dispositivo.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
1. Aggiungere hello seguente metodo toohello **programma** classe:
   
        public static async Task QueryTwinFWUpdateReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
1. Aggiungere hello seguente metodo toohello **programma** classe:

        public static async Task StartFirmwareUpdate()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("firmwareUpdate");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);
            method.SetPayloadJson(
                @"{
                    fwPackageUri : 'https://someurl'
                }");

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

1. Infine, aggiungere hello seguenti righe toohello **Main** metodo:
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartFirmwareUpdate().Wait();
        QueryTwinFWUpdateReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
1. In Esplora soluzioni hello, aprire hello **progetti di avvio impostato...**  e verificare che hello **azione** per **TriggerFWUpdate** progetto **avviare**.

1. Compilare la soluzione hello.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Eseguire App hello
Si è ora pronto toorun hello app.

1. Al prompt dei comandi di hello in hello **manageddevice** cartella, eseguire hello successivo comando toobegin in attesa di hello riavvio dirette del metodo.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. In Visual Studio, fare clic su hello **TriggerFWUpdate** projectRun toohello c# app console, selezionare **Debug** e **Avvia nuova istanza**.

3. Vedrai hello dispositivo risposta toohello metodo diretto nella console di hello.

    ![Firmware aggiornato][img-fwupdate]

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, è stato utilizzato un tootrigger dirette del metodo remota aggiornamento del firmware su un dispositivo e hello utilizzato nel report di stato di hello toofollow le proprietà di aggiornamento del firmware hello.

toolearn come tooextend il metodo di pianificazione e di soluzione IoT chiama su più dispositivi, vedere hello [pianificazione e i processi di broadcast] [ lnk-tutorial-jobs] esercitazione.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-firmware-update/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-firmware-update/createnetapp.png
[img-fwupdate]: media/iot-hub-csharp-node-firmware-update/fwupdated.png

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-rpi-implementation]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt_dm/pi_device
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/