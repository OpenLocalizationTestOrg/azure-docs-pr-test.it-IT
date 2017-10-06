---
title: IoT Hub Azure aaaUse diretta metodi (.NET/nodo) | Documenti Microsoft
description: Toouse IoT Hub Azure diretto come metodi. Usare il dispositivo di Azure IoT hello SDK per Node.js tooimplement un'app dispositivo simulato che include un metodo diretto e hello Azure IoT servizio SDK per .NET tooimplement un'applicazione di servizio che richiama metodo diretto hello.
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: f566f939be840eb308b00ffa4e05c4e5b3fefb39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnode"></a>Usare metodi diretti (.NET/Node)
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

In questa esercitazione verrà toodevelop .NET e un'applicazione console in Node.js:

* **CallMethodOnDevice.sln**, un'app di back-end .NET, che chiama un metodo in app dispositivo simulato hello e Visualizza la risposta hello.
* **SimulatedDevice.js**, un'app Node.js, che simula un dispositivo di connessione hub IoT tooyour con l'identità del dispositivo hello creato in precedenza e risponde toohello metodo chiamato dal cloud hello.

> [!NOTE]
> articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] vengono fornite informazioni hello Azure IoT SDK che è possibile utilizzare toobuild toorun entrambe le applicazioni in dispositivi e la soluzione di back-end.
> 
> 

toocomplete questa esercitazione, è necessario:

* Visual Studio 2015 o Visual Studio 2017.
* Node.js 0.10.x o versione successiva.
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Creare un'app di dispositivo simulato
In questa sezione si crea un'applicazione console Node. js che risponde tooa metodo chiamato dalla soluzione hello nuovamente finale.

1. Creare una nuova cartella vuota denominata **simulateddevice**. In hello **simulateddevice** cartella, creare un file di package. JSON usando hello seguente comando al prompt dei comandi. Accettare tutte le impostazioni predefinite hello:
   
    ```
    npm init
    ```
2. Al prompt dei comandi in hello **simulateddevice** cartella, eseguire hello successivo comando tooinstall hello **dispositivi iot di azure** e **mqtt azure-iot-dispositivo** pacchetti:
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Utilizzando un editor di testo, creare un file in hello **simulateddevice** cartella e denominarla **SimulatedDevice.js**.
4. Aggiungere il seguente hello `require` istruzioni hello iniziano hello **SimulatedDevice.js** file:
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. Aggiungere un **connectionString** variabile e usarlo toocreate un **DeviceClient** istanza. Sostituire **{stringa di connessione dispositivo}** con stringa di connessione dispositivo hello generato nel hello *creare un'identità del dispositivo* sezione:
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. Aggiungere hello seguente funzione tooimplement hello dirette del metodo nel dispositivo hello:
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Aprire l'hub IoT tooyour connessione hello e inizializzare listener per il metodo hello:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. Salvare e chiudere hello **SimulatedDevice.js** file.

> [!NOTE]
> cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo. Nel codice di produzione, è necessario implementare criteri di tentativi (ad esempio, il tentativo di connessione), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>Chiamare un metodo diretto in un dispositivo
In questa sezione si crea un'applicazione console .NET che chiama un metodo in app dispositivo simulato hello e quindi Visualizza la risposta hello.

1. In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto. Verificare che la versione di .NET Framework hello è 4.5.1 o versioni successive. Progetto hello nome **CallMethodOnDevice**.
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][10]
2. In Esplora soluzioni fare doppio clic su hello **CallMethodOnDevice** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .
3. In hello **Gestione pacchetti NuGet** selezionare **Sfoglia**, cercare **microsoft.azure.devices**selezionare **installare** tooinstall Hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso. Questa procedura Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.
   
    ![Finestra Gestione pacchetti NuGet][11]

4. Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. Aggiungere i seguenti campi toohello hello **programma** classe. Sostituire il valore di segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione precedente hello hello.
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Aggiungere hello seguente metodo toohello **programma** classe:
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    Questo metodo richiama un metodo diretto con nome `writeLine` su hello `myDeviceId` dispositivo. Quindi, viene scritto risposta hello fornita dal dispositivo hello sulla console hello. Si noti come è possibile toospecify un valore di timeout per toorespond dispositivo hello.
7. Infine, aggiungere hello seguenti righe toohello **Main** metodo:
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

## <a name="run-hello-applications"></a>Eseguire applicazioni hello
Si è ora applicazioni hello toorun pronto.

1. In hello Esplora soluzioni di Visual Studio, fare doppio clic sulla soluzione e quindi fare clic su **Imposta progetti di avvio...** . Selezionare **progetto di avvio singolo**, quindi selezionare hello **CallMethodOnDevice** progetto nel menu a discesa hello.

2. Al prompt dei comandi in hello **simulateddevice** cartella, eseguire hello in attesa di chiamate al metodo dall'IoT Hub toostart di comando seguente:
   
    ```
    node SimulatedDevice.js
    ```
   Attendere tooopen dispositivo simulato hello:![][7]
3. Ora che il dispositivo hello è connesso e in attesa di chiamate al metodo, eseguire hello .NET **CallMethodOnDevice** metodo hello tooinvoke di app in app dispositivo simulato hello. Dovrebbe essere scritto nella console di hello risposta del dispositivo hello.
   
    ![][8]
4. dispositivo di Hello reagisce quindi il metodo toohello con la stampa questo messaggio:
   
    ![][9]

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità. È stato utilizzato questo dispositivo identità tooenable hello simulato dispositivo app tooreact toomethods richiamato dal cloud hello. È stato creato anche un'applicazione che richiama metodi sul dispositivo hello e Visualizza la risposta hello dal dispositivo hello. 

Guida introduttiva toocontinue con IoT Hub e tooexplore altri scenari IoT, vedere:

* [Introduzione all'hub IoT]
* [Pianificare processi in più dispositivi][lnk-devguide-jobs]

toolearn come tooextend il metodo di pianificazione e di soluzione IoT chiama su più dispositivi, vedere hello [pianificazione e i processi di broadcast] [ lnk-tutorial-jobs] esercitazione.

<!-- Images. -->
[7]: ./media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: ./media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Introduzione all'hub IoT]: iot-hub-node-node-getstarted.md
