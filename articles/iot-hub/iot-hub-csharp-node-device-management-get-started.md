---
title: aaaGet avviato con la gestione dei dispositivi Azure IoT Hub (.NET/nodo) | Documenti Microsoft
description: Come tooinitiate di gestione dispositivi Azure IoT Hub toouse un dispositivo remoto riavviare il computer. Usare il dispositivo di Azure IoT hello SDK per Node.js tooimplement un'app dispositivo simulato che include un metodo diretto e hello Azure IoT servizio SDK per .NET tooimplement un'applicazione di servizio che richiama metodo diretto hello.
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: ea6d50dfac1c222d7836e3bf5503c6c9b8c89dfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-netnode"></a>Introduzione alla gestione dei dispositivi (.NET/Node)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Questa esercitazione illustra come:

* Utilizzare hello toocreate portale Azure un IoT Hub e creare un'identità del dispositivo nell'hub IoT.
* Creare un'app di dispositivo simulato contenente un metodo diretto per il riavvio del dispositivo. Diretti metodi vengono richiamati dal cloud hello.
* Creare un'applicazione console .NET che chiama hello riavvio dirette del metodo nell'app dispositivo simulato hello tramite l'hub IoT.

Alla fine di hello di questa esercitazione, si dispone di un'applicazione console in Node.js dispositivo e un'applicazione back-end di console .NET (c#):

**dmpatterns_getstarted_device.js**, che connette l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza, riceve un metodo diretto di riavvio, simula riavviare il computer fisico e segnala il tempo di hello per ultimo riavvio hello.

**TriggerReboot**, che chiama un metodo diretto in app hello dispositivo simulato, Visualizza risposta hello e consente di visualizzare hello aggiornato segnalati proprietà.

toocomplete questa esercitazione, è necessario hello seguenti:

* Visual Studio 2015 o Visual Studio 2017.
* Node.js 0.12.x o versione successiva. <br/>  [Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall Node.js per questa esercitazione su Windows o Linux.
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Attivare un riavvio remoto nel dispositivo hello utilizzando un metodo diretto
In questa sezione viene creata un'app console .NET (tramite C#) che attiva un riavvio remoto su un dispositivo usando un metodo diretto. app Hello utilizza hello toodiscover di query doppi dispositivo ora dell'ultimo riavvio del sistema per il dispositivo.

1. In Visual Studio, aggiungere una nuova soluzione tooa progetto Visual c# Windows Desktop classico utilizzando hello **applicazione Console (.NET Framework)** modello di progetto. Verificare che la versione di .NET Framework hello è 4.5.1 o versioni successive. Progetto hello nome **TriggerReboot**.

    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]

2. In Esplora soluzioni fare doppio clic su hello **TriggerReboot** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**.
3. In hello **Gestione pacchetti NuGet** selezionare **Sfoglia**, cercare **microsoft.azure.devices**selezionare **installare** tooinstall Hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso. Questa procedura Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.

    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
4. Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. Aggiungere i seguenti campi toohello hello **programma** classe. Sostituire il valore di segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello e dispositivo di destinazione hello hello.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. Aggiungere hello seguente metodo toohello **programma** classe.  Questo dispositivo gemelli di codice ottiene hello per il riavvio di dispositivo e l'output di hello hello segnalato proprietà.
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. Aggiungere hello seguente metodo toohello **programma** classe.  Questo codice avvia il riavvio di hello sul dispositivo hello utilizzando un metodo diretto.

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. Infine, aggiungere hello seguenti righe toohello **Main** metodo:
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. Compilare la soluzione hello.

## <a name="create-a-simulated-device-app"></a>Creare un'app di dispositivo simulato
Questa sezione consente di:

* Creare un'applicazione console Node. js che risponde tooa dirette del metodo chiamata dal cloud hello
* Attivare un riavvio del dispositivo simulato
* Hello utilizzare segnalati proprietà tooenable doppi query tooidentify dispositivi e quando sono riavviato

1. Creare una nuova cartella vuota denominata **manageddevice**.  In hello **manageddevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.  Accettare tutte le impostazioni predefinite hello:
   
    ```
    npm init
    ```
2. Al prompt dei comandi in hello **manageddevice** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** pacchetto SDK di dispositivo e **azure-iot-dispositivo-mqtt**pacchetto:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Utilizzando un editor di testo, creare un nuovo **dmpatterns_getstarted_device.js** file hello **manageddevice** cartella.
4. Aggiungere i seguenti hello 'richiedono' istruzioni all'inizio di hello di hello **dmpatterns_getstarted_device.js** file:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Aggiungere un **connectionString** variabile e usarlo toocreate un **Client** istanza.  Sostituire la stringa di connessione hello con la stringa di connessione del dispositivo.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Aggiungere hello seguente funzione tooimplement hello dirette del metodo nel dispositivo hello
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. Aggiungere i seguenti hello l'hub IoT tooopen hello connessione tooyour del codice e avviare il listener di un metodo diretto hello:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. Salvare e chiudere hello **dmpatterns_getstarted_device.js** file.
   
> [!NOTE]
> cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo. Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].


## <a name="run-hello-apps"></a>Eseguire App hello
Si è ora pronto toorun hello app.

1. Al prompt dei comandi di hello in hello **manageddevice** cartella, eseguire hello successivo comando toobegin in attesa di hello riavvio dirette del metodo.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. Applicazione console in esecuzione hello c# **TriggerReboot**. Pulsante destro del mouse hello **TriggerReboot** progetto, selezionare **Debug**, quindi selezionare **Avvia nuova istanza**.

3. Vedrai hello dispositivo risposta toohello metodo diretto nella console di hello.

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/