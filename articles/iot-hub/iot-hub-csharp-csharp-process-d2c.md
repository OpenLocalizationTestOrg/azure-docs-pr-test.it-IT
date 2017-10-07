---
title: i messaggi da dispositivo a cloud di IoT Hub Azure aaaProcess mediante route (.Net) | Documenti Microsoft
description: Come i messaggi da dispositivo a cloud IoT Hub utilizzando le regole di routing e gli endpoint personalizzati toodispatch tooprocess messaggi tooother servizi di back-end.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 5177bac9-722f-47ef-8a14-b201142ba4bc
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: c1dd5be04ca30c65af2be466ba6c8c1858333154
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-using-routes-net"></a>Elaborare messaggi da dispositivo a cloud dell'hub IoT usando i route (.NET)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

In questa esercitazione si basa su hello [iniziare con l'IoT Hub] esercitazione. esercitazione Hello:

* Viene illustrato come toouse routing regole messaggi da dispositivo a cloud toodispatch in modo semplice e basata sulla configurazione.
* Viene illustrato come messaggi interattivo tooisolate che richiedono un intervento immediato dalla soluzione hello back-end per un'ulteriore elaborazione. Ad esempio, un dispositivo potrebbe inviare un messaggio di avviso che attiva l'inserimento di un ticket in un sistema CRM. Al contrario, i messaggi di punto dati, come ad esempio la telemetria di temperatura, vengono semplicemente inseriti in un motore di analisi.

Alla fine di hello di questa esercitazione, si esegue tre applicazioni di console .NET:

* **SimulatedDevice**, una versione modificata dell'applicazione hello creato in hello [iniziare con l'IoT Hub] esercitazione invia i messaggi da dispositivo a cloud punto dati ogni secondo e interattivo dispositivo a cloud messaggi ogni 10 secondi.
* **ReadDeviceToCloudMessages** che consente di visualizzare hello non critici telemetria inviato per l'app del dispositivo.
* **ReadCriticalQueue** coda i messaggi critici di hello inviati per l'app del dispositivo da una coda del Bus di servizio. La coda è l'hub IoT toohello associata.

> [!NOTE]
> L'hub IoT offre il supporto SDK per molte piattaforme e linguaggi, inclusi C, Java e JavaScript. toolearn come tooreplace hello dispositivo simulato in questa esercitazione con un dispositivo fisico, vedere hello [Centro per sviluppatori di Azure IoT].

toocomplete questa esercitazione, è necessario hello seguenti:

* Visual Studio 2015 o Visual Studio 2017.
* Un account Azure attivo. <br/>Se non si ha un account, è possibile creare un [account gratuito](https://azure.microsoft.com/free/) in pochi minuti.

È necessaria una conoscenza di base di [Archiviazione di Azure] e del [bus di servizio di Azure].

## <a name="send-interactive-messages"></a>Inviare messaggi interattivi

Modificare hello app del dispositivo è stato creato in hello [iniziare con l'IoT Hub] toooccasionally esercitazione interattiva messaggi.

In Visual Studio, in hello **SimulatedDevice** del progetto, sostituire hello `SendDeviceToCloudMessagesAsync` metodo con hello seguente codice:

```csharp
private static async void SendDeviceToCloudMessagesAsync()
{
    double minTemperature = 20;
    double minHumidity = 60;
    Random rand = new Random();

    while (true)
    {
        double currentTemperature = minTemperature + rand.NextDouble() * 15;
        double currentHumidity = minHumidity + rand.NextDouble() * 20;

        var telemetryDataPoint = new
        {
            deviceId = "myFirstDevice",
            temperature = currentTemperature,
            humidity = currentHumidity
        };
        var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
        string levelValue;

        if (rand.NextDouble() > 0.7)
        {
            messageString = "This is a critical message";
            levelValue = "critical";
        }
        else
        {
            levelValue = "normal";
        }
        
        var message = new Message(Encoding.ASCII.GetBytes(messageString));
        message.Properties.Add("level", levelValue);
        
        await deviceClient.SendEventAsync(message);
        Console.WriteLine("{0} > Sent message: {1}", DateTime.Now, messageString);

        await Task.Delay(1000);
    }
}
```

Questo metodo aggiunge in modo casuale proprietà hello `"level": "critical"` toomessages inviato dal dispositivo hello, che simula un messaggio che richiede un intervento immediato per hello soluzione back-end. app per dispositivi Hello passare le informazioni nelle proprietà di messaggio hello, anziché nel corpo del messaggio hello, in modo che l'IoT Hub può instradare destinazione dei messaggi appropriata toohello messaggio hello.

> [!NOTE]
> È possibile utilizzare i messaggi tooroute di proprietà di messaggio per vari scenari, tra cui freddo-path, l'elaborazione, inoltre toohello hot-percorso riportato di seguito viene illustrato di seguito.

> [!NOTE]
> Per i migliori risultati hello di semplicità, in questa esercitazione non implementa alcun criterio di tentativo. Nel codice di produzione, è necessario implementare un criterio di ripetizione, ad esempio backoff esponenziale, come indicato nell'articolo MSDN hello [gestione degli errori temporanei].

## <a name="route-messages-tooa-queue-in-your-iot-hub"></a>Coda di tooa route dei messaggi nell'hub IoT

In questa sezione verrà illustrato come:

* Creare una coda del bus di servizio.
* La connessione hub IoT tooyour.
* Configurare la coda IoT hub toosend messaggi toohello in base hello presenza di una proprietà nel messaggio hello.

Per ulteriori informazioni su come tooprocess messaggi dalle code del Bus di servizio, vedere [iniziare con le code][Service Bus queue].

1. Creare una coda del bus di servizio, come descritto in [Get started with queues][Service Bus queue] (Introduzione alle code). deve essere coda Hello hello stessa sottoscrizione e area, come l'hub IoT. Prendere nota del nome dello spazio dei nomi e di Accodamento di hello.

    > [!NOTE]
    > Nelle code e negli argomenti del bus di servizio usati come endpoint dell'hub IoT non devono essere abilitati le **sessioni** e il **rilevamento duplicati**. Se una di queste opzioni sono abilitata, l'endpoint di hello viene visualizzato come **non raggiungibile** in hello portale di Azure.

2. In hello portale di Azure, aprire l'hub IoT e fare clic su **endpoint**.
    
    ![Endpoint in hub IoT][30]

3. In hello **endpoint** pannello, fare clic su **Aggiungi** in hello tooadd superiore dell'hub IoT tooyour di coda. Endpoint hello nome **CriticalQueue** e utilizzare hello elenchi a discesa tooselect **coda di Service Bus**hello dello spazio dei nomi Service Bus in cui risiede la coda e nome della coda di hello. Al termine, fare clic su **salvare** nella parte inferiore di hello.
    
    ![Aggiunta di un endpoint][31]
    
4. Fare clic su **Route** nell'hub IoT. Fare clic su **Aggiungi** nella parte superiore di hello di hello pannello toocreate una regola di routing che instrada i messaggi toohello coda è appena aggiunto. Selezionare **DeviceTelemetry** come origine dati hello. Immettere `level="critical"` come condizione hello e scegliere coda hello appena aggiunto come un endpoint personalizzato come hello endpoint regola di routing. Al termine, fare clic su **salvare** nella parte inferiore di hello.
    
    ![Aggiunta di un route][32]
    
    Assicurarsi di route fallback hello è troppo**ON**. Questo valore è hello predefinita per un hub IoT.
    
    ![Route di fallback][33]

## <a name="read-from-hello-queue-endpoint"></a>Lettura dall'endpoint di coda hello

In questa sezione, leggere i messaggi hello dall'endpoint di coda hello.

1. In Visual Studio, aggiungere Visual c# Windows Desktop classico toohello corrente soluzione con un progetto, tramite hello **applicazione Console (.NET Framework)** modello di progetto. Progetto hello nome **ReadCriticalQueue**.

2. In Esplora soluzioni fare doppio clic su hello **ReadCriticalQueue** del progetto e quindi fare clic su **Gestisci pacchetti NuGet**. Questa operazione consente di visualizzare hello **Gestione pacchetti NuGet** finestra.

3. Cercare **Windowsazure**, fare clic su **installare**e accettare le condizioni di hello d'uso. Questa operazione Scarica, installa e aggiunge un toohello riferimento Azure Service Bus, con tutte le relative dipendenze.

4. Aggiungere il seguente hello **utilizzando** le istruzioni nella parte superiore di hello di hello **Program.cs** file:
   
    ```csharp
    using System.IO;
    using Microsoft.ServiceBus.Messaging;
    ```

5. Infine, aggiungere hello seguenti righe toohello **Main** metodo. Sostituire la stringa di connessione hello con **ascolto** le autorizzazioni per la coda hello:
   
    ```csharp
    Console.WriteLine("Receive critical messages. Ctrl-C tooexit.\n");
    var connectionString = "{service bus listen string}";
    var queueName = "{queue name}";
    
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);

    client.OnMessage(message =>
        {
            Stream stream = message.GetBody<Stream>();
            StreamReader reader = new StreamReader(stream, Encoding.ASCII);
            string s = reader.ReadToEnd();
            Console.WriteLine(String.Format("Message body: {0}", s));
        });
        
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>Eseguire applicazioni hello
Si è ora applicazioni hello toorun pronto.

1. In Esplora soluzioni di Visual Studio fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Imposta progetti di avvio**. Selezionare **più progetti di avvio**, quindi selezionare **avviare** come azione hello per hello **ReadDeviceToCloudMessages**, **SimulatedDevice**, e **ReadCriticalQueue** progetti.
2. Premere **F5** toostart hello tre applicazioni console. Hello **ReadDeviceToCloudMessages** app ha solo i messaggi non critici inviati dal hello **SimulatedDevice** applicazione e hello **ReadCriticalQueue** dispone solo di app messaggi critici.
   
   ![Tre app console][50]

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione è stato descritto come tooreliably inviare i messaggi da dispositivo a cloud tramite funzionalità di routing messaggi hello dell'IoT Hub.

Hello [come toosend cloud a dispositivo messaggi con l'IoT Hub] [ lnk-c2d] viene illustrato come toosend messaggi dispositivi tooyour la soluzione di back-end.

esempi di toosee di soluzioni end-to-end completate che usa IoT Hub, vedere [Azure IoT Suite][lnk-suite].

toolearn più sullo sviluppo di soluzioni con l'IoT Hub, vedere hello [Guida per sviluppatori di IoT Hub].

toolearn informazioni su routing dei messaggi nell'IoT Hub, vedere [inviare e ricevere messaggi con l'IoT Hub][lnk-devguide-messaging].

<!-- Images. -->
[50]: ./media/iot-hub-csharp-csharp-process-d2c/run1.png
[30]: ./media/iot-hub-csharp-csharp-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-csharp-csharp-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-csharp-csharp-process-d2c/route-creation.png
[33]: ./media/iot-hub-csharp-csharp-process-d2c/fallback-route.png

<!-- Links -->
[Service Bus queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[Archiviazione di Azure]: https://azure.microsoft.com/documentation/services/storage/
[bus di servizio di Azure]: https://azure.microsoft.com/documentation/services/service-bus/
[Guida per sviluppatori di IoT Hub]: iot-hub-devguide.md
[iniziare con l'IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[Centro per sviluppatori di Azure IoT]: https://azure.microsoft.com/develop/iot
[gestione degli errori temporanei]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-c2d]: iot-hub-csharp-csharp-process-d2c.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
