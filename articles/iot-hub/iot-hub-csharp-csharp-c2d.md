---
title: Messaggi da cloud a dispositivo con l'hub IoT di Azure (.NET) | Documentazione Microsoft
description: Come inviare messaggi da cloud a dispositivo a un dispositivo da un hub IoT di Azure usando gli SDK di Azure IoT per .NET. Si modifica un'app per dispositivi per ricevere i messaggi diretti dal cloud al dispositivo e si modifica un'app back-end per inviare i messaggi diretti dal cloud al dispositivo.
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: a31c05ed-6ec0-40f3-99ab-8fdd28b1a89a
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: df0a319cdeabef8c854d7c60c7b90ef775be3ce1
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2017
---
# <a name="send-messages-from-the-cloud-to-your-device-with-iot-hub-net"></a>Inviare messaggi dal cloud al dispositivo con Hub IoT (.NET)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>Introduzione
L'hub IoT di Azure è un servizio completamente gestito che consente di abilitare comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione. L'esercitazione [Introduzione all'hub IoT di Azure] illustra come creare un hub IoT, effettuare il provisioning dell'identità di un dispositivo al suo interno e creare il codice di un'app per dispositivi che invia messaggi dal dispositivo al cloud.

Questa esercitazione si basa su [Introduzione all'hub IoT di Azure]. Illustra le operazioni seguenti:

* Dal back-end della soluzione inviare messaggi da cloud a dispositivo a un singolo dispositivo tramite l'hub IoT.
* Ricevere messaggi da cloud a dispositivo in un dispositivo.
* Dal back-end della soluzione richiedere l'acknowledgement di recapito (*feedback*) per i messaggi inviati a un dispositivo dall'hub IoT.

Per altre informazioni sui messaggi da cloud a dispositivo, vedere la[Guida per gli sviluppatori dell'hub IoT][IoT Hub developer guide - C2D].

Al termine di questa esercitazione vengono eseguite due app console .NET:

* **SimulatedDevice**, una versione modificata dell'app creata in [Introduzione all'hub IoT di Azure], che si connette all'hub IoT e riceve messaggi da cloud a dispositivo.
* **SendCloudToDevice**, che invia un messaggio diretto dal cloud al dispositivo all'app per dispositivi tramite l'hub IoT e quindi riceve la conferma di recapito.

> [!NOTE]
> L’hub IoT dispone del supporto SDK per molte piattaforme e linguaggi, tra cui C, Java e Javascript, tramite gli [SDK del dispositivo IoT Azure]. Per istruzioni dettagliate su come connettere il dispositivo al codice dell'esercitazione e in generale all'hub IoT di Azure, vedere la [Guida per sviluppatori dell'hub IoT].
> 
> 

Per completare l'esercitazione, sono necessari gli elementi seguenti:

* Visual Studio 2015 o Visual Studio 2017
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

## <a name="receive-messages-in-the-device-app"></a>Ricevere messaggi nell'app per dispositivi
In questa sezione si modificherà l'app per dispositivi creata in [Introduzione all'hub IoT di Azure] per ricevere i messaggi diretti dal cloud al dispositivo dall'hub IoT.

1. In Visual Studio, nel progetto **SimulatedDevice** aggiungere il seguente metodo alla classe **Program**.
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud to device messages from service");
            while (true)
            {
                Message receivedMessage = await deviceClient.ReceiveAsync();
                if (receivedMessage == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received message: {0}", Encoding.ASCII.GetString(receivedMessage.GetBytes()));
                Console.ResetColor();
   
                await deviceClient.CompleteAsync(receivedMessage);
            }
        }
   
    Il metodo `ReceiveAsync` restituisce in modo asincrono il messaggio ricevuto nel momento in cui viene ricevuto dal dispositivo. Restituisce *null* dopo un periodo di timeout specificabile (in questo caso viene usato il valore predefinito di un minuto). Quando l'app riceve un valore *Null*, deve rimanere in attesa di nuovi messaggi. Questo requisito è il motivo per la riga `if (receivedMessage == null) continue`.
   
    La chiamata a `CompleteAsync()` notifica all'hub IoT che il messaggio è stato elaborato correttamente. Il messaggio può essere rimosso dalla coda del dispositivo in modo sicuro. Se si è verificato un evento che ha impedito all'app per dispositivo di completare l'elaborazione del messaggio, l'hub IoT lo recapita nuovamente. È quindi importante che la logica di elaborazione del messaggio nell'app per dispositivo sia *idempotente*, in modo che la ricezione dello stesso messaggio più volte produca lo stesso risultato. Un'applicazione può anche abbandonare temporaneamente un messaggio e, di conseguenza, l'hub IoT mantiene il messaggio nella coda per un uso futuro. In alternativa, l'applicazione può rifiutare un messaggio, rimuovendolo così definitivamente dalla coda. Per altre informazioni sul ciclo di vita del messaggio da cloud a dispositivo, vedere [Guida per gli sviluppatori dell'hub IoT][IoT Hub developer guide - C2D].
   
   > [!NOTE]
   > Quando si usa HTTPS invece di MQTT o AMQP come trasporto, il metodo `ReceiveAsync` verrà restituito immediatamente. Il modello supportato per i messaggi da cloud a dispositivo con HTTPS è rappresentato da dispositivi collegati in modo intermittente che controllano raramente la presenza di messaggi (meno di ogni 25 minuti). La generazione di altre ricezioni HTTPS comporta la limitazione delle richieste da parte dell'hub IoT. Per altre informazioni sulle differenze tra il supporto di MQTT, AMQP e HTTPS e sulla limitazione delle richieste dell'hub IoT, vedere la [Guida per gli sviluppatori dell'hub IoT][IoT Hub developer guide - C2D].
   > 
   > 
2. Aggiungere il metodo seguente al metodo **Main** immediatamente prima della riga `Console.ReadLine()`:
   
        ReceiveC2dAsync();

> [!NOTE]
> Per semplicità, in questa esercitazione non si implementa alcun criterio di nuovi tentativi. Nel codice di produzione è consigliabile implementare criteri di ripetizione dei tentativi, ad esempio un backoff esponenziale, come indicato nell'articolo di MSDN [Transient Fault Handling](Gestione degli errori temporanei).
> 
> 

## <a name="send-a-cloud-to-device-message"></a>Inviare un messaggio da cloud a dispositivo
In questa sezione viene scritta un'app console di .NET che invia messaggi da cloud a dispositivo all'app per dispositivi.

1. Nella soluzione di Visual Studio corrente creare un progetto di applicazioni desktop in Visual C# usando il modello di progetto **Applicazione console**. Denominare il progetto **SendCloudToDevice**.
   
    ![Nuovo progetto in Visual Studio][20]
2. In Esplora soluzioni fare clic con il pulsante destro del mouse sulla soluzione e quindi scegliere **Gestisci pacchetti NuGet per la soluzione**. 
   
    L'azione consente di visualizzare la finestra **Gestisci pacchetti NuGet**.
3. Cercare **Microsoft.Azure.Devices**, fare clic su **Installa** e quindi accettare le condizioni per l'uso. 
   
    Verrà quindi scaricato e installato il [pacchetto NuGet Azure IoT Service SDK] e verrà aggiunto un riferimento a tale pacchetto.

4. Aggiungere l'istruzione `using` seguente all'inizio del file **Program.cs** :
   
        using Microsoft.Azure.Devices;
5. Aggiungere i campi seguenti alla classe **Program** . Sostituire il valore del segnaposto con la stringa di connessione all'hub IoT da [Introduzione all'hub IoT di Azure]:
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Aggiungere il metodo seguente alla classe **Program** :
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud to device message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    Questo metodo invia un nuovo messaggio da cloud a dispositivo al dispositivo con ID `myFirstDevice`. Modificare questo parametro solo nel caso in cui sia stato modificato rispetto a quello usato in [Introduzione all'hub IoT di Azure].
7. Aggiungere infine le righe seguenti al metodo **Main** :
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key to send a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. In Visual Studio fare clic con il pulsante destro del mouse sulla soluzione e selezionare **Imposta progetti di avvio**. Selezionare **Progetti di avvio multipli**, quindi selezionare l'azione **Start** per **ReadDeviceToCloudMessages**, **SimulatedDevice** e **SendCloudToDevice**.
9. Premere **F5**. Devono avviarsi tutte e tre le applicazioni. Selezionare la finestra **SendCloudToDevice** e premere **INVIO**. Verrà visualizzato il messaggio ricevuto dall'app per dispositivi.
   
   ![Ricezione di un messaggio da parte dell'app][21]

## <a name="receive-delivery-feedback"></a>Ricevere feedback di recapito
È possibile richiedere la conferma della ricezione (o della scadenza) dall'hub IoT per ogni messaggio da cloud a dispositivo. Questa opzione consente al back-end della soluzione di informare facilmente la logica di ripetizione o di compensazione. Per altre informazioni sul feedback da cloud a dispositivo, vedere [Guida per gli sviluppatori dell'hub IoT][IoT Hub developer guide - C2D].

In questa sezione viene modificata l'app **SendCloudToDevice** per richiedere feedback e riceverli dall'hub IoT.

1. In Visual Studio, nel progetto **SendCloudToDevice** aggiungere il seguente metodo alla classe **Programma**.
   
        private async static void ReceiveFeedbackAsync()
        {
            var feedbackReceiver = serviceClient.GetFeedbackReceiver();
   
            Console.WriteLine("\nReceiving c2d feedback from service");
            while (true)
            {
                var feedbackBatch = await feedbackReceiver.ReceiveAsync();
                if (feedbackBatch == null) continue;
   
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine("Received feedback: {0}", string.Join(", ", feedbackBatch.Records.Select(f => f.StatusCode)));
                Console.ResetColor();
   
                await feedbackReceiver.CompleteAsync(feedbackBatch);
            }
        }
   
    Si noti che il modello di ricezione è identico a quello usato per ricevere messaggi da cloud a dispositivo dall'app per dispositivo.
2. Aggiungere il metodo seguente nel metodo **Main`serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` immediatamente dopo la riga** :
   
        ReceiveFeedbackAsync();
3. Per richiedere feedback del recapito del messaggio da cloud a dispositivo, è necessario specificare una proprietà nel metodo **SendCloudToDeviceMessageAsync** . Aggiungere la riga seguente, subito dopo la riga `var commandMessage = new Message(...);` :
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. Premere **F5**per eseguire le app. Si dovrebbero avviare tutte e tre le applicazioni. Selezionare la finestra **SendCloudToDevice** e premere **INVIO**. Verrà visualizzata la ricezione del messaggio da parte dell'app per dispositivi e, dopo alcuni secondi, la ricezione del messaggio di feedback da parte dell'applicazione **SendCloudToDevice**.
   
   ![Ricezione di un messaggio da parte dell'app][22]

> [!NOTE]
> Per semplicità, in questa esercitazione non si implementa alcun criterio di nuovi tentativi. Nel codice di produzione è consigliabile implementare criteri di ripetizione dei tentativi, ad esempio un backoff esponenziale, come indicato nell'articolo di MSDN [Transient Fault Handling](Gestione degli errori temporanei).
> 
> 

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione è stato descritto come inviare e ricevere messaggi da cloud a dispositivo. 

Per avere degli esempi di soluzioni complete che utilizzano l'hub IoT, vedere la [Azure IoT Suite].

Per altre informazioni sullo sviluppo delle soluzioni con l'hub IoT, vedere la [Guida per sviluppatori dell'hub IoT].

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[pacchetto NuGet Azure IoT Service SDK]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[Guida per sviluppatori dell'hub IoT]: iot-hub-devguide.md
[Introduzione all'hub IoT di Azure]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT Suite]: https://docs.microsoft.com/azure/iot-suite/
[SDK del dispositivo IoT Azure]: iot-hub-devguide-sdks.md