---
title: i processi di aaaSchedule con IoT Hub di Azure (.NET/nodo) | Documenti Microsoft
description: "Un IoT Hub Azure tooschedule come processo tooinvoke un metodo diretto su più dispositivi. Utilizzare il dispositivo di Azure IoT hello SDK per Node.js tooimplement hello simulato dispositivo App e servizi IoT di Azure SDK per .NET tooimplement un processo del servizio app toorun hello hello."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: juanpere
ms.openlocfilehash: f6148b67129dde4580bfe9ccceafd6400fbc5976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a>Pianificare e trasmettere processi (.NET/Node.js)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Utilizzare i processi tooschedule e tenere traccia IoT Hub di Azure che aggiornano milioni di dispositivi. Usare i processi per:

* Aggiornare le proprietà desiderate
* Aggiornare i tag
* Richiamare metodi diretti

Un processo esegue il wrapping di una di queste azioni e le tracce hello esecuzione rispetto a un set di dispositivi che è definito da una query di due dispositivi. Ad esempio, un'applicazione back-end è possibile utilizzare un tooinvoke processo un metodo diretto su 10.000 dispositivi che si riavvia dispositivi hello. È necessario specifica il set di hello di dispositivi con una query di due dispositivi e pianificare toorun processo hello in un secondo momento. avanzamento tiene traccia del processo Hello come tutti i dispositivi di hello di ricezione ed eseguire hello riavvio dirette del metodo.

toolearn informazioni su ciascuna di queste funzionalità, vedere:

* Proprietà e un doppio dispositivo: [introduzione gemelli dispositivo] [ lnk-get-started-twin] e [esercitazione: come dispositivo toouse doppio proprietà][lnk-twin-props]
* Metodi diretti: [Guida per sviluppatori dell'hub IoT - Metodi diretti][lnk-dev-methods] ed [Esercitazione: Usare metodi diretti][lnk-c2d-methods]

Questa esercitazione illustra come:

* Creare un'app di dispositivo che implementa un metodo diretto denominato **lockDoor** che può essere chiamato da app back-end hello. Hello dispositivo app riceve inoltre le modifiche alle proprietà desiderato dai hello back-end app.
* Creare un'applicazione back-end che crea un hello toocall processo **lockDoor** metodo diretto su più dispositivi. Un altro processo invia proprietà desiderata Aggiorna dispositivi toomultiple.

Alla fine di hello di questa esercitazione, si dispone di un'applicazione console in Node.js dispositivo e un'applicazione back-end di console .NET (c#):

**simDevice.js** che connette l'hub IoT tooyour, implementa hello **lockDoor** indirizzare lo si desidera metodo e gestisce le modifiche alle proprietà.

**ScheduleJob** che utilizza hello toocall processi **lockDoor** diretto (metodo) e aggiornamento hello dispositivo doppi desiderato proprietà su più dispositivi.

toocomplete questa esercitazione, è necessario hello seguenti:

* Visual Studio 2015 o Visual Studio 2017.
* Node.js 0.12.x o versione successiva. articolo Hello [preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall Node.js per questa esercitazione su Windows o Linux.
* Un account Azure attivo. Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a>Pianificare i processi per chiamare un metodo diretto e inviare gli aggiornamenti dei dispositivi gemelli

In questa sezione si crea una .NET console app (usando c#) che utilizza hello toocall processi **lockDoor** metodo diretto e inviare proprietà desiderata Aggiorna dispositivi toomultiple.

1. In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto. Progetto hello nome **ScheduleJob**.

    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createapp]

1. In Esplora soluzioni fare doppio clic su hello **ScheduleJob** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .
1. In hello **Gestione pacchetti NuGet** selezionare **Sfoglia**, cercare **microsoft.azure.devices**selezionare **installare** tooinstall Hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso. Questo passaggio Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.

    ![Finestra Gestione pacchetti NuGet][img-servicenuget]
1. Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. Aggiungere il seguente hello `using` istruzione se non è già presente nelle istruzioni di hello predefinito.

    ```csharp
    using System.Threading.Tasks;
    ```

1. Aggiungere i seguenti campi toohello hello **programma** classe. Sostituire i segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello hello.

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. Aggiungere hello seguente metodo toohello **programma** classe:

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
    }
    ```

1. Aggiungere hello seguente metodo toohello **programma** classe:

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            "deviceId='myDeviceId'",
            directMethod,
            DateTime.Now,
            10);

        Console.WriteLine("Started Method Job");
    }
    ```

1. Aggiungere hello seguente metodo toohello **programma** classe:

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        var twin = new Twin();
        twin.Properties.Desired["Building"] = "43";
        twin.Properties.Desired["Floor"] = "3";
        twin.ETag = "*";

        JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
            "deviceId='myDeviceId'",
            twin,
            DateTime.Now,
            10);

        Console.WriteLine("Started Twin Update Job");
    }
    ```

1. Infine, aggiungere hello seguenti righe toohello **Main** metodo:

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER toorun hello next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER tooexit.");
    Console.ReadLine();
    ```

1. In Esplora soluzioni hello, aprire hello **progetti di avvio impostato...**  e verificare che hello **azione** per **ScheduleJob** progetto **avviare**. Compilare la soluzione hello.

## <a name="create-a-simulated-device-app"></a>Creare un'app di dispositivo simulato

In questa sezione si crea un'applicazione console Node. js che risponde tooa dirette del metodo chiamata dal cloud hello, che attiva un riavvio del dispositivo simulato e utilizza hello segnalato proprietà tooenable doppi query tooidentify dispositivi e quando sono riavviato.

1. Creare una nuova cartella vuota chiamata **simDevice**.  In hello **simDevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi.  Accettare tutte le impostazioni predefinite hello:

    ```cmd/sh
    npm init
    ```

1. Al prompt dei comandi in hello **simDevice** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** e **mqtt azure-iot-dispositivo** pacchetti:

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. Utilizzando un editor di testo, creare un nuovo **simDevice.js** file hello **simDevice** cartella.

1. Aggiungere i seguenti hello 'richiedono' istruzioni all'inizio di hello di hello **simDevice.js** file:

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. Aggiungere un **connectionString** variabile e usarlo toocreate un **Client** istanza. Verificare i segnaposto hello tooreplace che con il programma di installazione di valori tooyour appropriato.

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. Aggiungere i seguenti hello toohandle funzione hello **lockDoor** metodo.

    ```nodejs
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```

1. Aggiungere hello seguente gestore hello tooregister del codice per hello **lockDoor** metodo.

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. Salvare e chiudere hello **simDevice.js** file.

> [!NOTE]
> cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo. Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].

## <a name="run-hello-apps"></a>Eseguire App hello

Si è ora pronto toorun hello app.

1. Al prompt dei comandi di hello in hello **simDevice** cartella, eseguire hello successivo comando toobegin in attesa di hello riavvio dirette del metodo.

    ```cmd/sh
    node simDevice.js
    ```

1. Applicazione console in esecuzione hello c# **ScheduleJob** facendo clic su hello **ScheduleJob** progetto, quindi selezionando **Debug** e **Avvia nuova istanza**.

1. Viene visualizzato l'output di hello dal dispositivo e le applicazioni back-end.

    ![Eseguire app di hello tooschedule processi][img-schedulejobs]

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è stato utilizzato un processo tooschedule un dispositivo tooa dirette del metodo e l'aggiornamento di hello delle proprietà del doppi dispositivo hello.

Guida introduttiva a modelli di gestione di IoT Hub e dispositivo, ad esempio remoto tramite l'aggiornamento del firmware di hello air, leggere toocontinue [esercitazione: come toodo un firmware aggiornare][lnk-fwupdate].

Introduzione a IoT Hub, toocontinue vedere [Guida introduttiva a bordo IoT][lnk-iot-edge].

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
