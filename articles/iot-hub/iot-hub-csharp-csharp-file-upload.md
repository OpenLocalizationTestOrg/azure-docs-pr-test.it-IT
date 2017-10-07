---
title: file aaaUpload da dispositivi tooAzure IoT Hub con .NET | Documenti Microsoft
description: "Modalità tooupload file da un cloud toohello dispositivo utilizzando il dispositivo IoT di Azure SDK per .NET. I file caricati vengono salvati in un contenitore BLOB di archiviazione di Azure."
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/04/2017
ms.author: elioda
ms.openlocfilehash: 07d555f6ba8b067bbd3233bc8eebaa220ad2388b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a>Caricare file dal cloud toohello dispositivo con l'IoT Hub usando .NET

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

Questa esercitazione si basa su codice hello in hello [inviare messaggi da Cloud a dispositivo con l'IoT Hub](iot-hub-csharp-csharp-c2d.md) tooshow esercitazione si come toouse hello funzionalità di caricamento di file dell'IoT Hub. Illustra le operazioni seguenti:

- Specificare in modo sicuro un dispositivo con un URI del BLOB di Azure per il caricamento di un file.
- Utilizzare l'elaborazione di tootrigger notifiche di IoT Hub file caricamento del file hello nel back-end app hello.

Hello [iniziare con l'IoT Hub](iot-hub-csharp-csharp-getstarted.md) e [inviare messaggi da Cloud a dispositivo con l'IoT Hub](iot-hub-csharp-csharp-c2d.md) le esercitazioni illustrano hello da dispositivo a cloud e cloud a dispositivo messaggistica funzionalità di base di IoT Hub. Hello [i messaggi di processo da dispositivo a Cloud](iot-hub-csharp-csharp-process-d2c.md) esercitazione viene descritto un modo tooreliably memorizza da dispositivo a cloud messaggi nel servizio di archiviazione blob di Azure. Tuttavia, in alcuni scenari è possibile mappare facilmente dati hello che i dispositivi di trasmissione in messaggi da dispositivo a cloud relativamente piccolo hello che accetta l'IoT Hub. ad esempio:

* File di grandi dimensioni che contengono immagini
* Video
* Dati di vibrazione campionati ad alta frequenza
* Qualche tipo di dati pre-elaborati

Questi file sono in genere batch elaborato nel cloud hello tramite strumenti come [Data Factory di Azure](../data-factory/index.md) o hello [Hadoop](../hdinsight/index.md) dello stack. Quando è necessario il file tooupload da un dispositivo, è possibile utilizzare ancora hello protezione e affidabilità dell'IoT Hub.

Alla fine di hello di questa esercitazione è eseguire due applicazioni di console .NET:

* **SimulatedDevice**, una versione modificata dell'applicazione hello creato in hello [inviare messaggi da Cloud a dispositivo con l'IoT Hub](iot-hub-csharp-csharp-c2d.md) esercitazione. Questa app carica toostorage un file utilizzando un URI SAS forniti per l'hub IoT.
* **ReadFileUploadNotification**riceve le notifiche di caricamento file dall'hub IoT.

> [!NOTE]
> L'hub IoT supporta numerose piattaforme e linguaggi (inclusi C, Java e Javascript) tramite gli Azure IoT SDK per dispositivi. Fare riferimento toohello [Centro per sviluppatori di Azure IoT] per istruzioni dettagliate su come tooconnect il tooAzure dispositivo IoT Hub.

toocomplete questa esercitazione, è necessario hello seguenti:

* Visual Studio 2015 o Visual Studio 2017
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>Caricare un file da un'app per dispositivi

In questa sezione, si modifica hello app del dispositivo è stato creato in [inviare messaggi da Cloud a dispositivo con l'IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive di messaggi da cloud a dispositivo dall'hub IoT hello.

1. In Visual Studio, fare doppio clic su hello **SimulatedDevice** del progetto, fare clic su **Aggiungi**, quindi fare clic su **elemento esistente**. Passare il file di immagine tooan e includerla nel progetto. Questa esercitazione si presuppone l'immagine di hello sia denominato `image.jpg`.

1. Fare doppio clic sull'immagine di hello e quindi fare clic su **proprietà**. Assicurarsi che **copiare tooOutput Directory** è troppo**Copia sempre**.

    ![][1]

1. In hello **Program.cs** file, aggiungere hello seguendo le istruzioni all'inizio di hello del file hello:

    ```csharp
    using System.IO;
    ```

1. Aggiungere hello seguente metodo toohello **programma** classe:

    ```csharp
    private static async void SendToBlobAsync()
    {
        string fileName = "image.jpg";
        Console.WriteLine("Uploading file: {0}", fileName);
        var watch = System.Diagnostics.Stopwatch.StartNew();

        using (var sourceData = new FileStream(@"image.jpg", FileMode.Open))
        {
            await deviceClient.UploadToBlobAsync(fileName, sourceData);
        }

        watch.Stop();
        Console.WriteLine("Time tooupload file: {0}ms\n", watch.ElapsedMilliseconds);
    }
    ```

    Hello `UploadToBlobAsync` (metodo) nel nome file hello e di origine del flusso di hello file toobe caricato gestisce toostorage caricamento hello. applicazione console Hello Visualizza hello tempo file hello tooupload.

1. Aggiungere al metodo in hello hello **Main** (metodo), immediatamente prima di hello `Console.ReadLine()` riga:

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> Per semplicità, in questa esercitazione non si implementa alcun criterio di nuovi tentativi. Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei].

## <a name="receive-a-file-upload-notification"></a>Ricevere la notifica di caricamento di un file

In questa sezione verrà scritta un'app console di .NET che riceve messaggi di notifica di caricamento dall'hub IoT.

1. Nella soluzione di Visual Studio hello corrente, creare un progetto Visual c# Windows utilizzando hello **applicazione Console** modello di progetto. Progetto hello nome **ReadFileUploadNotification**.

    ![Nuovo progetto in Visual Studio][2]

1. In Esplora soluzioni fare doppio clic su hello **ReadFileUploadNotification** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .

1. In hello **Gestione pacchetti NuGet** finestra, cercare **Microsoft.Azure.Devices**, fare clic su **installare**e accettare le condizioni di hello d'uso.

    Questa azione Scarica, installa e aggiunge un riferimento toohello [pacchetto NuGet SDK del servizio Azure IoT] in hello **ReadFileUploadNotification** progetto.

1. In hello **Program.cs** file, aggiungere hello seguendo le istruzioni all'inizio di hello del file hello:

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. Aggiungere i seguenti campi toohello hello **programma** classe. Sostituire il valore di segnaposto hello con stringa di connessione hub IoT hello da [iniziare con l'IoT Hub]:

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. Aggiungere hello seguente metodo toohello **programma** classe:

    ```csharp
    private async static void ReceiveFileUploadNotificationAsync()
    {
        var notificationReceiver = serviceClient.GetFileNotificationReceiver();

        Console.WriteLine("\nReceiving file upload notification from service");
        while (true)
        {
            var fileUploadNotification = await notificationReceiver.ReceiveAsync();
            if (fileUploadNotification == null) continue;

            Console.ForegroundColor = ConsoleColor.Yellow;
            Console.WriteLine("Received file upload noticiation: {0}", string.Join(", ", fileUploadNotification.BlobName));
            Console.ResetColor();

            await notificationReceiver.CompleteAsync(fileUploadNotification);
        }
    }
    ```

    Nota di questo modello di ricezione è hello stessi messaggi cloud a dispositivo tooreceive usato uno dall'app per dispositivi hello.

1. Infine, aggiungere hello seguenti righe toohello **Main** metodo:

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a>Eseguire applicazioni hello

Si è ora applicazioni hello toorun pronto.

1. In Visual Studio fare clic con il pulsante destro del mouse sulla soluzione e selezionare **Imposta progetti di avvio**. Selezionare **più progetti di avvio**, quindi selezionare hello **avviare** azione per **ReadFileUploadNotification** e **SimulatedDevice**.

1. Premere **F5**. Si avviano entrambe le applicazioni. Dovrebbe essere hello caricamento completato in un'unica console app e ricevuto dal messaggio di notifica di hello caricamento hello altre applicazione console. È possibile utilizzare hello [portale di Azure] o toocheck Esplora Server Visual Studio per la presenza di hello di hello caricamento del file nell'account di archiviazione di Azure.

    ![][50]

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è stato descritto come file hello toouse caricare le funzionalità di IoT Hub consente di caricare file toosimplify dai dispositivi. È possibile continuare tooexplore IoT hub funzionalità e scenari con hello seguenti articoli:

* [Creare un hub IoT a livello di codice][lnk-create-hub]
* [Introduzione tooC SDK][lnk-c-sdk]
* [Azure IoT SDKs][lnk-sdks] (SDK di IoT di Azure)

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Simulazione di un dispositivo con IoT Edge][lnk-iotedge]

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png

<!-- Links -->

[portale di Azure]: https://portal.azure.com/

[Centro per sviluppatori di Azure IoT]: http://www.azure.com/develop/iot

[gestione degli errori temporanei]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[pacchetto NuGet SDK del servizio Azure IoT]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md
