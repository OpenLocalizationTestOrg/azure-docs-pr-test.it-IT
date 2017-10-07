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
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub-using-net"></a><span data-ttu-id="7b12b-104">Caricare file dal cloud toohello dispositivo con l'IoT Hub usando .NET</span><span class="sxs-lookup"><span data-stu-id="7b12b-104">Upload files from your device toohello cloud with IoT Hub using .NET</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="7b12b-105">Questa esercitazione si basa su codice hello in hello [inviare messaggi da Cloud a dispositivo con l'IoT Hub](iot-hub-csharp-csharp-c2d.md) tooshow esercitazione si come toouse hello funzionalità di caricamento di file dell'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7b12b-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial tooshow you how toouse hello file upload capabilities of IoT Hub.</span></span> <span data-ttu-id="7b12b-106">Illustra le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7b12b-106">It shows you how to:</span></span>

- <span data-ttu-id="7b12b-107">Specificare in modo sicuro un dispositivo con un URI del BLOB di Azure per il caricamento di un file.</span><span class="sxs-lookup"><span data-stu-id="7b12b-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="7b12b-108">Utilizzare l'elaborazione di tootrigger notifiche di IoT Hub file caricamento del file hello nel back-end app hello.</span><span class="sxs-lookup"><span data-stu-id="7b12b-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="7b12b-109">Hello [iniziare con l'IoT Hub](iot-hub-csharp-csharp-getstarted.md) e [inviare messaggi da Cloud a dispositivo con l'IoT Hub](iot-hub-csharp-csharp-c2d.md) le esercitazioni illustrano hello da dispositivo a cloud e cloud a dispositivo messaggistica funzionalità di base di IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7b12b-109">hello [Get started with IoT Hub](iot-hub-csharp-csharp-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="7b12b-110">Hello [i messaggi di processo da dispositivo a Cloud](iot-hub-csharp-csharp-process-d2c.md) esercitazione viene descritto un modo tooreliably memorizza da dispositivo a cloud messaggi nel servizio di archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="7b12b-110">hello [Process Device-to-Cloud messages](iot-hub-csharp-csharp-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="7b12b-111">Tuttavia, in alcuni scenari è possibile mappare facilmente dati hello che i dispositivi di trasmissione in messaggi da dispositivo a cloud relativamente piccolo hello che accetta l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7b12b-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="7b12b-112">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="7b12b-112">For example:</span></span>

* <span data-ttu-id="7b12b-113">File di grandi dimensioni che contengono immagini</span><span class="sxs-lookup"><span data-stu-id="7b12b-113">Large files that contain images</span></span>
* <span data-ttu-id="7b12b-114">Video</span><span class="sxs-lookup"><span data-stu-id="7b12b-114">Videos</span></span>
* <span data-ttu-id="7b12b-115">Dati di vibrazione campionati ad alta frequenza</span><span class="sxs-lookup"><span data-stu-id="7b12b-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="7b12b-116">Qualche tipo di dati pre-elaborati</span><span class="sxs-lookup"><span data-stu-id="7b12b-116">Some form of preprocessed data</span></span>

<span data-ttu-id="7b12b-117">Questi file sono in genere batch elaborato nel cloud hello tramite strumenti come [Data Factory di Azure](../data-factory/index.md) o hello [Hadoop](../hdinsight/index.md) dello stack.</span><span class="sxs-lookup"><span data-stu-id="7b12b-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="7b12b-118">Quando è necessario il file tooupload da un dispositivo, è possibile utilizzare ancora hello protezione e affidabilità dell'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7b12b-118">When you need tooupload files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="7b12b-119">Alla fine di hello di questa esercitazione è eseguire due applicazioni di console .NET:</span><span class="sxs-lookup"><span data-stu-id="7b12b-119">At hello end of this tutorial you run two .NET console apps:</span></span>

* <span data-ttu-id="7b12b-120">**SimulatedDevice**, una versione modificata dell'applicazione hello creato in hello [inviare messaggi da Cloud a dispositivo con l'IoT Hub](iot-hub-csharp-csharp-c2d.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="7b12b-120">**SimulatedDevice**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial.</span></span> <span data-ttu-id="7b12b-121">Questa app carica toostorage un file utilizzando un URI SAS forniti per l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7b12b-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="7b12b-122">**ReadFileUploadNotification**riceve le notifiche di caricamento file dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7b12b-122">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="7b12b-123">L'hub IoT supporta numerose piattaforme e linguaggi (inclusi C, Java e Javascript) tramite gli Azure IoT SDK per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="7b12b-123">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="7b12b-124">Fare riferimento toohello [Centro per sviluppatori di Azure IoT] per istruzioni dettagliate su come tooconnect il tooAzure dispositivo IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7b12b-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="7b12b-125">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="7b12b-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="7b12b-126">Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="7b12b-126">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="7b12b-127">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="7b12b-127">An active Azure account.</span></span> <span data-ttu-id="7b12b-128">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="7b12b-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="7b12b-129">Caricare un file da un'app per dispositivi</span><span class="sxs-lookup"><span data-stu-id="7b12b-129">Upload a file from a device app</span></span>

<span data-ttu-id="7b12b-130">In questa sezione, si modifica hello app del dispositivo è stato creato in [inviare messaggi da Cloud a dispositivo con l'IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive di messaggi da cloud a dispositivo dall'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="7b12b-130">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="7b12b-131">In Visual Studio, fare doppio clic su hello **SimulatedDevice** del progetto, fare clic su **Aggiungi**, quindi fare clic su **elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="7b12b-131">In Visual Studio, right-click hello **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span></span> <span data-ttu-id="7b12b-132">Passare il file di immagine tooan e includerla nel progetto.</span><span class="sxs-lookup"><span data-stu-id="7b12b-132">Navigate tooan image file and include it in your project.</span></span> <span data-ttu-id="7b12b-133">Questa esercitazione si presuppone l'immagine di hello sia denominato `image.jpg`.</span><span class="sxs-lookup"><span data-stu-id="7b12b-133">This tutorial assumes hello image is named `image.jpg`.</span></span>

1. <span data-ttu-id="7b12b-134">Fare doppio clic sull'immagine di hello e quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="7b12b-134">Right-click on hello image, and then click **Properties**.</span></span> <span data-ttu-id="7b12b-135">Assicurarsi che **copiare tooOutput Directory** è troppo**Copia sempre**.</span><span class="sxs-lookup"><span data-stu-id="7b12b-135">Make sure that **Copy tooOutput Directory** is set too**Copy always**.</span></span>

    ![][1]

1. <span data-ttu-id="7b12b-136">In hello **Program.cs** file, aggiungere hello seguendo le istruzioni all'inizio di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="7b12b-136">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using System.IO;
    ```

1. <span data-ttu-id="7b12b-137">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="7b12b-137">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="7b12b-138">Hello `UploadToBlobAsync` (metodo) nel nome file hello e di origine del flusso di hello file toobe caricato gestisce toostorage caricamento hello.</span><span class="sxs-lookup"><span data-stu-id="7b12b-138">hello `UploadToBlobAsync` method takes in hello file name and stream source of hello file toobe uploaded and handles hello upload toostorage.</span></span> <span data-ttu-id="7b12b-139">applicazione console Hello Visualizza hello tempo file hello tooupload.</span><span class="sxs-lookup"><span data-stu-id="7b12b-139">hello console app displays hello time it takes tooupload hello file.</span></span>

1. <span data-ttu-id="7b12b-140">Aggiungere al metodo in hello hello **Main** (metodo), immediatamente prima di hello `Console.ReadLine()` riga:</span><span class="sxs-lookup"><span data-stu-id="7b12b-140">Add hello following method in hello **Main** method, right before hello `Console.ReadLine()` line:</span></span>

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> <span data-ttu-id="7b12b-141">Per semplicità, in questa esercitazione non si implementa alcun criterio di nuovi tentativi.</span><span class="sxs-lookup"><span data-stu-id="7b12b-141">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="7b12b-142">Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei].</span><span class="sxs-lookup"><span data-stu-id="7b12b-142">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="7b12b-143">Ricevere la notifica di caricamento di un file</span><span class="sxs-lookup"><span data-stu-id="7b12b-143">Receive a file upload notification</span></span>

<span data-ttu-id="7b12b-144">In questa sezione verrà scritta un'app console di .NET che riceve messaggi di notifica di caricamento dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="7b12b-144">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span></span>

1. <span data-ttu-id="7b12b-145">Nella soluzione di Visual Studio hello corrente, creare un progetto Visual c# Windows utilizzando hello **applicazione Console** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="7b12b-145">In hello current Visual Studio solution, create a Visual C# Windows project by using hello **Console Application** project template.</span></span> <span data-ttu-id="7b12b-146">Progetto hello nome **ReadFileUploadNotification**.</span><span class="sxs-lookup"><span data-stu-id="7b12b-146">Name hello project **ReadFileUploadNotification**.</span></span>

    ![Nuovo progetto in Visual Studio][2]

1. <span data-ttu-id="7b12b-148">In Esplora soluzioni fare doppio clic su hello **ReadFileUploadNotification** del progetto e quindi fare clic su **Gestisci pacchetti NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="7b12b-148">In Solution Explorer, right-click hello **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span></span>

1. <span data-ttu-id="7b12b-149">In hello **Gestione pacchetti NuGet** finestra, cercare **Microsoft.Azure.Devices**, fare clic su **installare**e accettare le condizioni di hello d'uso.</span><span class="sxs-lookup"><span data-stu-id="7b12b-149">In hello **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept hello terms of use.</span></span>

    <span data-ttu-id="7b12b-150">Questa azione Scarica, installa e aggiunge un riferimento toohello [pacchetto NuGet SDK del servizio Azure IoT] in hello **ReadFileUploadNotification** progetto.</span><span class="sxs-lookup"><span data-stu-id="7b12b-150">This action downloads, installs, and adds a reference toohello [Azure IoT service SDK NuGet package] in hello **ReadFileUploadNotification** project.</span></span>

1. <span data-ttu-id="7b12b-151">In hello **Program.cs** file, aggiungere hello seguendo le istruzioni all'inizio di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="7b12b-151">In hello **Program.cs** file, add hello following statements at hello top of hello file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. <span data-ttu-id="7b12b-152">Aggiungere i seguenti campi toohello hello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="7b12b-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="7b12b-153">Sostituire il valore di segnaposto hello con stringa di connessione hub IoT hello da [iniziare con l'IoT Hub]:</span><span class="sxs-lookup"><span data-stu-id="7b12b-153">Substitute hello placeholder value with hello IoT hub connection string from [Get started with IoT Hub]:</span></span>

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. <span data-ttu-id="7b12b-154">Aggiungere hello seguente metodo toohello **programma** classe:</span><span class="sxs-lookup"><span data-stu-id="7b12b-154">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="7b12b-155">Nota di questo modello di ricezione è hello stessi messaggi cloud a dispositivo tooreceive usato uno dall'app per dispositivi hello.</span><span class="sxs-lookup"><span data-stu-id="7b12b-155">Note this receive pattern is hello same one used tooreceive cloud-to-device messages from hello device app.</span></span>

1. <span data-ttu-id="7b12b-156">Infine, aggiungere hello seguenti righe toohello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="7b12b-156">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter tooexit\n");
    Console.ReadLine();
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="7b12b-157">Eseguire applicazioni hello</span><span class="sxs-lookup"><span data-stu-id="7b12b-157">Run hello applications</span></span>

<span data-ttu-id="7b12b-158">Si è ora applicazioni hello toorun pronto.</span><span class="sxs-lookup"><span data-stu-id="7b12b-158">Now you are ready toorun hello applications.</span></span>

1. <span data-ttu-id="7b12b-159">In Visual Studio fare clic con il pulsante destro del mouse sulla soluzione e selezionare **Imposta progetti di avvio**.</span><span class="sxs-lookup"><span data-stu-id="7b12b-159">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span></span> <span data-ttu-id="7b12b-160">Selezionare **più progetti di avvio**, quindi selezionare hello **avviare** azione per **ReadFileUploadNotification** e **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="7b12b-160">Select **Multiple startup projects**, then select hello **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span></span>

1. <span data-ttu-id="7b12b-161">Premere **F5**.</span><span class="sxs-lookup"><span data-stu-id="7b12b-161">Press **F5**.</span></span> <span data-ttu-id="7b12b-162">Si avviano entrambe le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="7b12b-162">Both applications should start.</span></span> <span data-ttu-id="7b12b-163">Dovrebbe essere hello caricamento completato in un'unica console app e ricevuto dal messaggio di notifica di hello caricamento hello altre applicazione console.</span><span class="sxs-lookup"><span data-stu-id="7b12b-163">You should see hello upload completed in one console app and hello upload notification message received by hello other console app.</span></span> <span data-ttu-id="7b12b-164">È possibile utilizzare hello [portale di Azure] o toocheck Esplora Server Visual Studio per la presenza di hello di hello caricamento del file nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7b12b-164">You can use hello [Azure portal] or Visual Studio Server Explorer toocheck for hello presence of hello uploaded file in your Azure Storage account.</span></span>

    ![][50]

## <a name="next-steps"></a><span data-ttu-id="7b12b-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7b12b-165">Next steps</span></span>

<span data-ttu-id="7b12b-166">In questa esercitazione è stato descritto come file hello toouse caricare le funzionalità di IoT Hub consente di caricare file toosimplify dai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="7b12b-166">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="7b12b-167">È possibile continuare tooexplore IoT hub funzionalità e scenari con hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="7b12b-167">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="7b12b-168">[Creare un hub IoT a livello di codice][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="7b12b-168">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="7b12b-169">[Introduzione tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="7b12b-169">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="7b12b-170">[Azure IoT SDKs][lnk-sdks] (SDK di IoT di Azure)</span><span class="sxs-lookup"><span data-stu-id="7b12b-170">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="7b12b-171">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="7b12b-171">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="7b12b-172">[Simulazione di un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="7b12b-172">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

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
