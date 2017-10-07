---
title: i messaggi aaaCloud al dispositivo con Azure IoT Hub (.NET) | Documenti Microsoft
description: "La modalità toosend cloud a dispositivo dei messaggi tooa dispositivo da un hub IoT di Azure usando hello Azure IoT SDK per .NET. Per modificare i messaggi di cloud a dispositivo un dispositivo app tooreceive e modificare un messaggio di cloud a dispositivo hello toosend app back-end."
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
ms.openlocfilehash: f6a7618b164d95c8ddaf28943f244aeeb568217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-messages-from-hello-cloud-tooyour-device-with-iot-hub-net"></a>Inviare messaggi da dispositivo di tooyour hello cloud con Hub IoT (.NET)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>Introduzione
L'hub IoT di Azure è un servizio completamente gestito che consente di abilitare comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione. Hello [iniziare con l'IoT Hub] esercitazione viene illustrato come eseguire il provisioning di un'identità del dispositivo in essa contenuti, toocreate un hub IoT e codice di un'app di dispositivo che invia messaggi da dispositivo a cloud.

Questa esercitazione si basa su [iniziare con l'IoT Hub]. Illustra le operazioni seguenti:

* Dal back-end soluzione, inviare singolo dispositivo tooa messaggi da cloud a dispositivo tramite l'IoT Hub.
* Ricevere messaggi da cloud a dispositivo in un dispositivo.
* Dal back-end soluzione, richiedere la conferma di recapito (*feedback*) per i messaggi inviati tooa dispositivo dall'IoT Hub.

Sono disponibili ulteriori informazioni sui cloud a dispositivo messaggi hello [Guida per sviluppatori di IoT Hub][IoT Hub developer guide - C2D].

Alla fine di hello di questa esercitazione, si esegue due applicazioni di console .NET:

* **SimulatedDevice**, una versione modificata dell'applicazione hello creato in [iniziare con l'IoT Hub], che si connette l'hub IoT tooyour e riceve messaggi da cloud a dispositivo.
* **SendCloudToDevice**, che invia un'app di dispositivo toohello messaggio cloud a dispositivo tramite l'IoT Hub e quindi riceve la conferma di recapito.

> [!NOTE]
> L’hub IoT dispone del supporto SDK per molte piattaforme e linguaggi, tra cui C, Java e Javascript, tramite gli [SDK del dispositivo IoT Azure]. Per istruzioni dettagliate su come tooconnect l'esercitazione toothis dispositivo codice e in genere tooAzure IoT Hub, vedere hello [Guida per sviluppatori di IoT Hub].
> 
> 

toocomplete questa esercitazione, è necessario hello seguenti:

* Visual Studio 2015 o Visual Studio 2017
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

## <a name="receive-messages-in-hello-device-app"></a>Ricezione di messaggi hello dispositivo App
In questa sezione, che si desidera modificare hello app del dispositivo è stato creato in [iniziare con l'IoT Hub] tooreceive di messaggi da cloud a dispositivo dall'hub IoT hello.

1. In Visual Studio, in hello **SimulatedDevice** del progetto, aggiungere hello seguente metodo toohello **programma** classe.
   
        private static async void ReceiveC2dAsync()
        {
            Console.WriteLine("\nReceiving cloud toodevice messages from service");
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
   
    Hello `ReceiveAsync` (metodo) restituisce in modo asincrono il messaggio hello ricevuto in fase di hello ricevuto dal dispositivo hello. Restituisce *null* dopo un periodo di timeout specificabile (in questo caso, viene usato predefinito hello è un minuto). Quando applicazione hello riceve un *null*, deve continuare toowait per i nuovi messaggi. Questo requisito è motivo hello hello `if (receivedMessage == null) continue` riga.
   
    Hello chiamata troppo`CompleteAsync()` notifica IoT Hub è stato elaborato il messaggio hello. messaggio Hello può essere rimossi dalla coda dispositivo hello. Se si è verificato tale app dispositivo hello ha impedito di completare l'elaborazione di hello del messaggio hello un IoT Hub recapita nuovamente. È quindi importante è il messaggio hello dispositivo App logica di elaborazione *idempotente*, in modo che la ricezione di hello stesso messaggio più volte produce hello stesso risultato. Un'applicazione può inoltre temporaneamente abbandono di un messaggio, che comporta l'hub IoT mantenendo il messaggio hello nella coda di hello per un utilizzo futuro. In alternativa, un'applicazione hello può rifiutare un messaggio, che consente di rimuovere definitivamente il messaggio hello dalla coda hello. Per ulteriori informazioni sul ciclo di vita di hello messaggio cloud a dispositivo, vedere hello [Guida per sviluppatori di IoT Hub][IoT Hub developer guide - C2D].
   
   > [!NOTE]
   > Quando si Usa HTTP invece di MQTT o AMQP come trasporto, hello `ReceiveAsync` metodo viene restituito immediatamente. modello di Hello è supportato per i messaggi da cloud a dispositivo con HTTP è occasionali per i dispositivi che consentono di controllare per i messaggi raramente (meno di 25 minuti). Emissione ulteriori HTTP riceve i risultati nelle richieste hello limitazione IoT Hub. Per ulteriori informazioni sulle differenze hello supporto MQTT, AMQP e HTTP e la limitazione delle richieste di Hub IoT, vedere hello [Guida per sviluppatori di IoT Hub][IoT Hub developer guide - C2D].
   > 
   > 
2. Aggiungere al metodo in hello hello **Main** (metodo), immediatamente prima di hello `Console.ReadLine()` riga:
   
        ReceiveC2dAsync();

> [!NOTE]
> Per semplicità, in questa esercitazione non si implementa alcun criterio di nuovi tentativi. Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei].
> 
> 

## <a name="send-a-cloud-to-device-message"></a>Inviare un messaggio da cloud a dispositivo
In questa sezione, scrivere un'applicazione console .NET che invia messaggi da cloud a dispositivo toohello dispositivo app.

1. Nella soluzione di Visual Studio hello corrente, creare un progetto di App Desktop Visual c# utilizzando hello **applicazione Console** modello di progetto. Progetto hello nome **SendCloudToDevice**.
   
    ![Nuovo progetto in Visual Studio][20]
2. In Esplora soluzioni fare doppio clic hello soluzione e quindi fare clic su **Gestisci pacchetti NuGet per la soluzione...** . 
   
    Questa azione apre hello **Gestisci pacchetti NuGet** finestra.
3. Cercare **Microsoft.Azure.Devices**, fare clic su **installare**e accettare le condizioni di hello d'uso. 
   
    Questo download, si installa e si aggiunge un riferimento toohello [pacchetto NuGet SDK del servizio Azure IoT].

4. Aggiungere il seguente hello `using` istruzione nella parte superiore di hello di hello **Program.cs** file:
   
        using Microsoft.Azure.Devices;
5. Aggiungere i seguenti campi toohello hello **programma** classe. Sostituire il valore di segnaposto hello con stringa di connessione hub IoT hello da [iniziare con l'IoT Hub]:
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Aggiungere hello seguente metodo toohello **programma** classe:
   
        private async static Task SendCloudToDeviceMessageAsync()
        {
            var commandMessage = new Message(Encoding.ASCII.GetBytes("Cloud toodevice message."));
            await serviceClient.SendAsync("myFirstDevice", commandMessage);
        }
   
    Questo metodo invia un nuovo dispositivo toohello cloud a dispositivo messaggio con ID hello, `myFirstDevice`. Modificare questo parametro solo se è stato modificato da hello quello utilizzato nel [iniziare con l'IoT Hub].
7. Infine, aggiungere hello seguenti righe toohello **Main** metodo:
   
        Console.WriteLine("Send Cloud-to-Device message\n");
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
   
        Console.WriteLine("Press any key toosend a C2D message.");
        Console.ReadLine();
        SendCloudToDeviceMessageAsync().Wait();
        Console.ReadLine();
8. In Visual Studio fare clic con il pulsante destro del mouse sulla soluzione e selezionare **Imposta progetti di avvio**. Selezionare **più progetti di avvio**, quindi selezionare hello **avviare** azione per **ReadDeviceToCloudMessages**, **SimulatedDevice**, e **SendCloudToDevice**.
9. Premere **F5**. Devono avviarsi tutte e tre le applicazioni. Seleziona hello **SendCloudToDevice** windows e premere **invio**. Verrà visualizzato il messaggio hello ricevuto dall'app per dispositivi hello.
   
   ![Ricezione di un messaggio da parte dell'app][21]

## <a name="receive-delivery-feedback"></a>Ricevere feedback di recapito
È possibile toorequest recapito (scadenza) acknowledgment o dall'IoT Hub per ogni messaggio cloud a dispositivo. Questo tooeasily di opzione Abilita hello soluzione back-end che indicano la logica di compensazione o di tentativi. Per ulteriori informazioni sui commenti cloud a dispositivo, vedere hello [Guida per sviluppatori di IoT Hub][IoT Hub developer guide - C2D].

In questa sezione, si modifica hello **SendCloudToDevice** feedback toorequest app e riceve dall'IoT Hub.

1. In Visual Studio, in hello **SendCloudToDevice** del progetto, aggiungere hello seguente metodo toohello **programma** classe.
   
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
   
    Nota di questo modello di ricezione è hello stessi messaggi cloud a dispositivo tooreceive usato uno dall'app per dispositivi hello.
2. Aggiungere al metodo in hello hello **Main** metodo subito dopo hello `serviceClient = ServiceClient.CreateFromConnectionString(connectionString)` riga:
   
        ReceiveFeedbackAsync();
3. toorequest commenti e suggerimenti per il recapito del messaggio da cloud a dispositivo hello, aver toospecify una proprietà in hello **SendCloudToDeviceMessageAsync** metodo. Aggiungere hello successiva riga, subito dopo hello `var commandMessage = new Message(...);` riga:
   
        commandMessage.Ack = DeliveryAcknowledgement.Full;
4. Eseguire App hello premendo **F5**. Si dovrebbero avviare tutte e tre le applicazioni. Seleziona hello **SendCloudToDevice** windows e premere **invio**. Dovrebbe essere hello dei messaggi ricevuti dall'app per dispositivi hello e, dopo alcuni secondi, hello messaggio commenti e suggerimenti ricevuto dal **SendCloudToDevice** dell'applicazione.
   
   ![Ricezione di un messaggio da parte dell'app][22]

> [!NOTE]
> Per semplicità, in questa esercitazione non si implementa alcun criterio di nuovi tentativi. Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei].
> 
> 

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, si è appreso come toosend e ricevere messaggi da cloud a dispositivo. 

esempi di toosee di soluzioni end-to-end completate che usa IoT Hub, vedere [Azure IoT Suite].

toolearn più sullo sviluppo di soluzioni con l'IoT Hub, vedere hello [Guida per sviluppatori di IoT Hub].

<!-- Images -->
[20]: ./media/iot-hub-csharp-csharp-c2d/create-identity-csharp1.png
[21]: ./media/iot-hub-csharp-csharp-c2d/sendc2d1.png
[22]: ./media/iot-hub-csharp-csharp-c2d/sendc2d2.png

<!-- Links -->

[pacchetto NuGet SDK del servizio Azure IoT]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[gestione degli errori temporanei]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md

[Guida per sviluppatori di IoT Hub]: iot-hub-devguide.md
[iniziare con l'IoT Hub]: iot-hub-csharp-csharp-getstarted.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure IoT Suite]: https://docs.microsoft.com/en-us/azure/iot-suite/
[SDK del dispositivo IoT Azure]: iot-hub-devguide-sdks.md