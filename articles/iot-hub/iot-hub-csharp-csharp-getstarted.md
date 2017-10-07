---
title: aaaGet avviato con Azure IoT Hub (.NET) | Documenti Microsoft
description: Informazioni su come toosend dispositivo a cloud messaggi tooAzure IoT Hub tramite IoT SDK per .NET. Creare dispositivo simulato e servizio App tooregister il dispositivo, inviare messaggi e leggere messaggi da hub IoT.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: f40604ff-8fd6-4969-9e99-8574fbcf036c
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56cf14687411898ea0fa4ebb1782e18b3930809c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a>Connessione hub IoT tooyour dispositivo utilizzando .NET

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Alla fine di hello di questa esercitazione, si dispongono di tre applicazioni di console .NET:

* **CreateDeviceIdentity**, che consente di creare un'identità del dispositivo e protezione della chiave tooconnect l'app del dispositivo.
* **ReadDeviceToCloudMessages**, che consente di visualizzare dati di telemetria hello inviati per l'app del dispositivo.
* **SimulatedDevice**, che collega l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza e invia un messaggio di dati di telemetria ogni secondo tramite protocollo MQTT hello.

È possibile scaricare o clonare la soluzione di Visual Studio hello, che contiene tre app di hello da Github.

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> Per informazioni su Azure IoT SDK hello che è possibile utilizzare toobuild toorun applicazioni nei dispositivi e il back-end di soluzione, vedere [Azure IoT SDK][lnk-hub-sdks].

toocomplete questa esercitazione, è necessario hello seguenti:

* Visual Studio 2015 o Visual Studio 2017.
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

È stato creato l'hub IoT e si dispone di nome host hello e stringa di connessione IoT Hub che è necessario rest hello toocomplete di questa esercitazione.

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a>Ricezione di messaggi da dispositivo a cloud
In questa sezione si crea un'app console di .NET che legge i messaggi da dispositivo a cloud dall'hub IoT. Un hub IoT espone un [hub eventi di Azure][lnk-event-hubs-overview]-tooenable endpoint compatibile per i messaggi da dispositivo a cloud tooread. cose tookeep semplice, in questa esercitazione consente di creare un lettore di base che non è adatto per una distribuzione di velocità effettiva elevata. toolearn come tooprocess dispositivo a cloud messaggi su larga scala, vedere hello [elaborare i messaggi da dispositivo a cloud] [ lnk-process-d2c-tutorial] esercitazione. Per ulteriori informazioni su come tooprocess messaggi dagli hub eventi, vedere hello [Introduzione agli hub di eventi] [ lnk-eventhubs-tutorial] esercitazione. (Questa esercitazione è applicabile toohello evento dell'Hub IoT Hub compatibile endpoint).

> [!NOTE]
> Hello Hub eventi compatibile con l'endpoint per la lettura dei messaggi da dispositivo a cloud sempre Usa protocollo AMQP hello.

1. In Visual Studio, aggiungere Visual c# Windows Desktop classico toohello corrente soluzione con un progetto, tramite hello **applicazione Console (.NET Framework)** modello di progetto. Verificare che la versione di .NET Framework hello è 4.5.1 o versioni successive. Progetto hello nome **ReadDeviceToCloudMessages**.

    ![Nuovo progetto desktop di Windows classico in Visual C#][10a]

2. In Esplora soluzioni fare doppio clic su hello **ReadDeviceToCloudMessages** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**.

3. In hello **Gestione pacchetti NuGet** finestra, cercare **Windowsazure**selezionare **installare**e accettare le condizioni di hello d'uso. Questa procedura Scarica, installa e aggiunge un riferimento troppo[Azure Service Bus][lnk-servicebus-nuget], con tutte le relative dipendenze. Questo pacchetto consente endpoint hello applicazione tooconnect toohello Hub eventi compatibile con l'hub IoT.

4. Aggiungere il seguente hello `using` le istruzioni nella parte superiore di hello di hello **Program.cs** file:

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. Aggiungere i seguenti campi toohello hello **programma** classe. Sostituire il valore di segnaposto hello con la stringa di connessione IoT Hub hub hello creato nella sezione "Creare un hub IoT" hello hello.

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. Aggiungere hello seguente metodo toohello **programma** classe:

    ```csharp
    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested) break;
            EventData eventData = await eventHubReceiver.ReceiveAsync();
            if (eventData == null) continue;

            string data = Encoding.UTF8.GetString(eventData.GetBytes());
            Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
        }
    }
    ```

    Questo metodo utilizza un **EventHubReceiver** partizioni di ricezione di messaggi di istanza tooreceive da tutti hello IoT hub dispositivo a cloud. Si noti come passare un `DateTime.Now` parametro quando si crea hello **EventHubReceiver** dell'oggetto, in modo che riceva solo i messaggi inviati dopo l'avvio. Questo filtro è utile in un ambiente di test in modo da visualizzare il set corrente di hello dei messaggi. In un ambiente di produzione, il codice deve verificare che vengano elaborati tutti i messaggi hello. Per ulteriori informazioni, vedere l'esercitazione hello [come i messaggi da dispositivo a cloud IoT Hub tooprocess][lnk-process-d2c-tutorial].

7. Infine, aggiungere hello seguenti righe toohello **Main** metodo:

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C tooexit.\n");
    eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, iotHubD2cEndpoint);

    var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;

    CancellationTokenSource cts = new CancellationTokenSource();

    System.Console.CancelKeyPress += (s, e) =>
    {
        e.Cancel = true;
        cts.Cancel();
        Console.WriteLine("Exiting...");
    };

    var tasks = new List<Task>();
    foreach (string partition in d2cPartitions)
    {
        tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
    }  
    Task.WaitAll(tasks.ToArray());
    ```

## <a name="create-a-device-app"></a>Creare un'app per dispositivi

In questa sezione si crea un'applicazione console .NET che simula un dispositivo che invia l'hub IoT tooan messaggi da dispositivo a cloud.

1. In Visual Studio, aggiungere Visual c# Windows Desktop classico toohello corrente soluzione con un progetto, tramite hello **applicazione Console (.NET Framework)** modello di progetto. Verificare che la versione di .NET Framework hello è 4.5.1 o versioni successive. Progetto hello nome **SimulatedDevice**.

    ![Nuovo progetto desktop di Windows classico in Visual C#][10b]

2. In Esplora soluzioni fare doppio clic su hello **SimulatedDevice** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**.

3. In hello **Gestione pacchetti NuGet** selezionare **Sfoglia**, cercare **Microsoft.Azure.Devices.Client**selezionare **installare** hello tooinstall **Microsoft.Azure.Devices.Client** pacchetto e accettare le condizioni di hello d'uso. Questa procedura Scarica, installa e aggiunge un riferimento toohello [pacchetto NuGet SDK del dispositivo IoT di Azure] [ lnk-device-nuget] e le relative dipendenze.

4. Aggiungere il seguente hello `using` istruzione nella parte superiore di hello di hello **Program.cs** file:

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. Aggiungere i seguenti campi toohello hello **programma** classe. Substitute `{iot hub hostname}` con nome host dell'hub IoT hello recuperato nella sezione "Creare un hub IoT" hello. Substitute `{device key}` con chiave dispositivo hello recuperato nella sezione "Creare un'identità del dispositivo" hello.

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. Aggiungere hello seguente metodo toohello **programma** classe:

    ```csharp
    private static async void SendDeviceToCloudMessagesAsync()
    {
        double minTemperature = 20;
        double minHumidity = 60;
        int messageId = 1;
        Random rand = new Random();

        while (true)
        {
            double currentTemperature = minTemperature + rand.NextDouble() * 15;
            double currentHumidity = minHumidity + rand.NextDouble() * 20;

            var telemetryDataPoint = new
            {
                messageId = messageId++,
                deviceId = "myFirstDevice",
                temperature = currentTemperature,
                humidity = currentHumidity
            };
            var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
            var message = new Message(Encoding.ASCII.GetBytes(messageString));
            message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

            await deviceClient.SendEventAsync(message);
            Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

            await Task.Delay(1000);
        }
    }
    ```

    Questo metodo invia un nuovo messaggio da dispositivo a cloud ogni secondo. messaggio Hello contiene un oggetto JSON serializzato, con ID dispositivo hello e generato in modo casuale di numeri toosimulate un sensore di temperatura e un sensore umidità.

7. Infine, aggiungere hello seguenti righe toohello **Main** metodo:

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    Per impostazione predefinita, hello **crea** metodo in un'app .NET Framework consente di creare un **DeviceClient** istanza che utilizza hello AMQP protocollo toocommunicate con l'IoT Hub. hello toouse protocollo MQTT o HTTP, utilizzare l'override di hello del hello **crea** metodo che consente di protocollo hello toospecify. UWP e PCL usano il protocollo HTTP hello per impostazione predefinita. Se si utilizza il protocollo HTTP hello, è necessario aggiungere anche hello **webapi** hello di NuGet pacchetto tooyour progetto tooinclude **System.Net.Http.Formatting** dello spazio dei nomi.

In questa esercitazione illustra i passaggi di hello toocreate un IoT Hub app per dispositivi. È inoltre possibile utilizzare hello [servizio connesso per l'IoT Hub Azure] [ lnk-connected-service] tooyour dispositivo app di Visual Studio estensione tooadd hello codice necessario.

> [!NOTE]
> cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo. Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].

## <a name="run-hello-apps"></a>Eseguire App hello

Si è ora pronto toorun hello app.

1. In Esplora soluzioni in Visual Studio fare clic con il pulsante destro del mouse sulla soluzione e quindi scegliere **Imposta progetti di avvio**. Selezionare **più progetti di avvio**, quindi selezionare **avviare** come azione hello per entrambi hello **ReadDeviceToCloudMessages** e **SimulatedDevice** progetti.

    ![Proprietà del progetto di avvio][41]

2. Premere **F5** toostart entrambe le App in esecuzione. output della console da hello Hello **SimulatedDevice** messaggi hello di app Mostra l'app del dispositivo invia tooyour IoT hub. output della console da hello Hello **ReadDeviceToCloudMessages** app Mostra messaggi hello che riceve l'hub IoT.

    ![Output della console dalle app][42]

3. Hello **utilizzo** riquadro in hello [portale di Azure] [ lnk-portal] Mostra hello numero di messaggi inviati toohello hub IoT:

    ![Riquadro Utilizzo del portale di Azure][43]

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, è configurato un hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità. È stato utilizzato questo dispositivo identità tooenable hello dispositivo app toosend messaggi da dispositivo a cloud toohello hub IoT. È stato creato anche un'applicazione che consente di visualizzare i messaggi hello ricevuti dall'hub IoT hello.

Guida introduttiva toocontinue con IoT Hub e tooexplore altri scenari IoT, vedere:

* [Connessione del dispositivo][lnk-connect-device]
* [Introduzione alla gestione dei dispositivi][lnk-device-management]
* [Introduzione a IoT Edge][lnk-iot-edge]

toolearn tooextend vedere i messaggi di dispositivo a cloud processo e di soluzione IoT su larga scala, hello [elaborare i messaggi da dispositivo a cloud] [ lnk-process-d2c-tutorial] esercitazione.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[41]: ./media/iot-hub-csharp-csharp-getstarted/run-apps1.png
[42]: ./media/iot-hub-csharp-csharp-getstarted/run-apps2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png
[10a]: ./media/iot-hub-csharp-csharp-getstarted/create-receive-csharp1.png
[10b]: ./media/iot-hub-csharp-csharp-getstarted/create-device-csharp1.png


<!-- Links -->
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-servicebus-nuget]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-device-nuget]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-connected-service]: https://visualstudiogallery.msdn.microsoft.com/e254a3a5-d72e-488e-9bd3-8fee8e0cd1d6
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
