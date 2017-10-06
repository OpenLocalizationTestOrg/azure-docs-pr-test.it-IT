---
title: IoT Hub Azure aaaUse diretta di metodi (.NET/.NET) | Documenti Microsoft
description: Toouse IoT Hub Azure diretto come metodi. Usare il dispositivo di Azure IoT hello SDK per .NET tooimplement un'app dispositivo simulato che include un metodo diretto e hello Azure IoT servizio SDK per .NET tooimplement un'applicazione di servizio che richiama metodo diretto hello.
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a>Usare metodi diretti (.NET/.NET)
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

In questa esercitazione, siamo corso toodevelop due applicazioni console .NET:

* **CallMethodOnDevice**, un'applicazione back-end, che chiama un metodo in app dispositivo simulato hello e Visualizza la risposta hello.
* **SimulateDeviceMethods**, un'applicazione console che simula un dispositivo di connessione hub IoT tooyour con l'identità del dispositivo hello creato in precedenza e risponde toohello metodo chiamato dal cloud hello.

> [!NOTE]
> articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] vengono fornite informazioni hello Azure IoT SDK che è possibile utilizzare toobuild toorun entrambe le applicazioni in dispositivi e la soluzione di back-end.
> 
> 

toocomplete questa esercitazione, è necessario:

* Visual Studio 2015 o Visual Studio 2017.
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Se si desidera l'identità del dispositivo hello toocreate a livello di codice in alternativa, leggere una sezione corrispondente di hello in hello [connessione hub IoT tooyour dispositivo simulato utilizzando .NET] [ lnk-device-identity-csharp] articolo.


## <a name="create-a-simulated-device-app"></a>Creare un'app di dispositivo simulato
In questa sezione si crea un'applicazione console .NET che risponde tooa metodo chiamato dalla soluzione hello nuovamente finale.

1. In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto. Progetto hello nome **SimulateDeviceMethods**.
   
    ![Nuova app per il dispositivo di Windows classico in Visual C#][img-createdeviceapp]
    
1. In Esplora soluzioni fare doppio clic su hello **SimulateDeviceMethods** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .
1. In hello **Gestione pacchetti NuGet** selezionare **Sfoglia** e cercare **microsoft.azure.devices.client**. Selezionare **installare** tooinstall hello **Microsoft.Azure.Devices.Client** pacchetto e accettare le condizioni di hello d'uso. Questa procedura Scarica, installa e aggiunge un riferimento toohello [dispositivo IoT di Azure SDK] [ lnk-nuget-client-sdk] NuGet pacchetto e le relative dipendenze.
   
    ![App client della finestra Gestione pacchetti NuGet][img-clientnuget]
1. Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. Aggiungere i seguenti campi toohello hello **programma** classe. Sostituire il valore di segnaposto hello con stringa di connessione hello dispositivo che si è preso nota nella sezione precedente hello.
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. Aggiungere hello seguente tooimplement hello dirette del metodo nel dispositivo hello:

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. Infine, aggiungere hello seguente codice toohello **Main** metodo tooopen hello tooyour IoT hub e inizializzare hello metodo listener della connessione:
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. In hello Esplora soluzioni di Visual Studio, fare doppio clic sulla soluzione e quindi fare clic su **Imposta progetti di avvio...** . Selezionare **progetto di avvio singolo**, quindi selezionare hello **SimulateDeviceMethods** progetto nel menu a discesa hello.        

> [!NOTE]
> cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo. Nel codice di produzione, è necessario implementare criteri di tentativi (ad esempio, il tentativo di connessione), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].
> 
> 

## <a name="call-a-direct-method-on-a-device"></a>Chiamare un metodo diretto in un dispositivo
In questa sezione si crea un'applicazione console .NET che chiama un metodo in app dispositivo simulato hello e quindi Visualizza la risposta hello.

1. In Visual Studio, aggiungere una soluzione di Visual c# Windows Desktop classico progetto toohello corrente utilizzando hello **applicazione Console** modello di progetto. Verificare che la versione di .NET Framework hello è 4.5.1 o versioni successive. Progetto hello nome **CallMethodOnDevice**.
   
    ![Nuovo progetto desktop di Windows classico in Visual C#][img-createserviceapp]
2. In Esplora soluzioni fare doppio clic su hello **CallMethodOnDevice** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .
3. In hello **Gestione pacchetti NuGet** selezionare **Sfoglia**, cercare **microsoft.azure.devices**selezionare **installare** tooinstall Hello **Microsoft.Azure.Devices** pacchetto e accettare le condizioni di hello d'uso. Questa procedura Scarica, installa e aggiunge un riferimento toohello [SDK di servizi di Azure IoT] [ lnk-nuget-service-sdk] NuGet pacchetto e le relative dipendenze.
   
    ![Finestra Gestione pacchetti NuGet][img-servicenuget]

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

1. In hello Esplora soluzioni di Visual Studio, fare doppio clic sulla soluzione e quindi fare clic su **Imposta progetti di avvio...** . Selezionare **progetto di avvio singolo**, quindi selezionare hello **CallMethodOnDevice** progetto nel menu a discesa hello.

## <a name="run-hello-applications"></a>Eseguire applicazioni hello
Si è ora applicazioni hello toorun pronto.

1. Eseguire app di dispositivo .NET hello **SimulateDeviceMethods**. Dovrebbe iniziare ad ascoltare le chiamate di metodo provenienti dall'IoT Hub: 

    ![Esecuzione dell'app per dispositivi][img-deviceapprun]
1. Ora che il dispositivo hello è connesso e in attesa di chiamate al metodo, eseguire hello .NET **CallMethodOnDevice** metodo hello tooinvoke di app in app dispositivo simulato hello. Dovrebbe essere scritto nella console di hello risposta del dispositivo hello.
   
    ![Esecuzione dell'app di servizio][img-serviceapprun]
1. dispositivo di Hello reagisce quindi il metodo toohello con la stampa questo messaggio:
   
    ![Dirette del metodo richiamata sul dispositivo hello][img-directmethodinvoked]

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità. È stato utilizzato questo dispositivo identità tooenable hello simulato dispositivo app tooreact toomethods richiamato dal cloud hello. È stato creato anche un'applicazione che richiama metodi sul dispositivo hello e Visualizza la risposta hello dal dispositivo hello. 

Guida introduttiva toocontinue con IoT Hub e tooexplore altri scenari IoT, vedere:

* [Introduzione all'hub IoT]
* [Pianificare processi in più dispositivi][lnk-devguide-jobs]

toolearn come tooextend il metodo di pianificazione e di soluzione IoT chiama su più dispositivi, vedere hello [pianificazione e i processi di broadcast] [ lnk-tutorial-jobs] esercitazione.

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[Introduzione all'hub IoT]: iot-hub-node-node-getstarted.md
