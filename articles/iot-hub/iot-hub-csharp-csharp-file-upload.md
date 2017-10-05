---
title: Caricare file dai dispositivi nell'hub IoT con .NET | Microsoft Docs
description: Come caricare file da un dispositivo al cloud usando Azure IoT SDK per dispositivi per .NET. I file caricati vengono salvati in un contenitore BLOB di archiviazione di Azure.
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
ms.openlocfilehash: b45d85d0d77cf47f36cb793bc8c0dbe2d5c12634
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="upload-files-from-your-device-to-the-cloud-with-iot-hub-using-net"></a><span data-ttu-id="aecb7-104">Eseguire l'upload di file dal dispositivo al cloud con l'hub IoT usando .NET</span><span class="sxs-lookup"><span data-stu-id="aecb7-104">Upload files from your device to the cloud with IoT Hub using .NET</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="aecb7-105">Questa esercitazione si basa sul codice dell'esercitazione [Inviare messaggi da cloud a dispositivo con l'hub IoT](iot-hub-csharp-csharp-c2d.md) che illustra come usare le funzionalità di caricamento di file dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aecb7-105">This tutorial builds on the code in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial to show you how to use the file upload capabilities of IoT Hub.</span></span> <span data-ttu-id="aecb7-106">Illustra le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="aecb7-106">It shows you how to:</span></span>

- <span data-ttu-id="aecb7-107">Specificare in modo sicuro un dispositivo con un URI del BLOB di Azure per il caricamento di un file.</span><span class="sxs-lookup"><span data-stu-id="aecb7-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="aecb7-108">Usare le notifiche di caricamento di file dell'hub IoT per attivare l'elaborazione del file nel back-end dell'app.</span><span class="sxs-lookup"><span data-stu-id="aecb7-108">Use the IoT Hub file upload notifications to trigger processing the file in your app back end.</span></span>

<span data-ttu-id="aecb7-109">Le esercitazioni [Introduzione all'hub IoT](iot-hub-csharp-csharp-getstarted.md) e [Inviare messaggi da cloud a dispositivo con l'hub IoT](iot-hub-csharp-csharp-c2d.md) illustrano le funzionalità di messaggistica di base da dispositivo a cloud e da cloud a dispositivo dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aecb7-109">The [Get started with IoT Hub](iot-hub-csharp-csharp-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorials show the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="aecb7-110">L'esercitazione [Elaborare messaggi da dispositivo a cloud](iot-hub-csharp-csharp-process-d2c.md) illustra come archiviare in modo affidabile i messaggi da dispositivo a cloud nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="aecb7-110">The [Process Device-to-Cloud messages](iot-hub-csharp-csharp-process-d2c.md) tutorial describes a way to reliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="aecb7-111">Tuttavia in alcuni scenari non è possibile mappare facilmente i dati che i dispositivi inviano in messaggi relativamente ridotti da dispositivo a cloud, che l'hub IoT accetta.</span><span class="sxs-lookup"><span data-stu-id="aecb7-111">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="aecb7-112">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="aecb7-112">For example:</span></span>

* <span data-ttu-id="aecb7-113">File di grandi dimensioni che contengono immagini</span><span class="sxs-lookup"><span data-stu-id="aecb7-113">Large files that contain images</span></span>
* <span data-ttu-id="aecb7-114">Video</span><span class="sxs-lookup"><span data-stu-id="aecb7-114">Videos</span></span>
* <span data-ttu-id="aecb7-115">Dati di vibrazione campionati ad alta frequenza</span><span class="sxs-lookup"><span data-stu-id="aecb7-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="aecb7-116">Qualche tipo di dati pre-elaborati</span><span class="sxs-lookup"><span data-stu-id="aecb7-116">Some form of preprocessed data</span></span>

<span data-ttu-id="aecb7-117">Questi dati in genere vengono elaborati in batch nel cloud con strumenti come [Azure Data Factory](../data-factory/index.md) o lo stack [Hadoop](../hdinsight/index.md).</span><span class="sxs-lookup"><span data-stu-id="aecb7-117">These files are typically batch processed in the cloud using tools such as [Azure Data Factory](../data-factory/index.md) or the [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="aecb7-118">Quando è necessario caricare i file da un dispositivo, è comunque possibile usare la sicurezza e affidabilità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aecb7-118">When you need to upload files from a device, you can still use the security and reliability of IoT Hub.</span></span>

<span data-ttu-id="aecb7-119">Al termine di questa esercitazione vengono eseguite due app console .NET:</span><span class="sxs-lookup"><span data-stu-id="aecb7-119">At the end of this tutorial you run two .NET console apps:</span></span>

* <span data-ttu-id="aecb7-120">**SimulatedDevice**, una versione modificata dell'applicazione creata nell'esercitazione [Inviare messaggi da cloud a dispositivo con l'hub IoT](iot-hub-csharp-csharp-c2d.md).</span><span class="sxs-lookup"><span data-stu-id="aecb7-120">**SimulatedDevice**, a modified version of the app created in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) tutorial.</span></span> <span data-ttu-id="aecb7-121">Ciò consente di caricare un file nell'archivio tramite un URI con firma di accesso condiviso fornito dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aecb7-121">This app uploads a file to storage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="aecb7-122">**ReadFileUploadNotification**riceve le notifiche di caricamento file dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aecb7-122">**ReadFileUploadNotification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="aecb7-123">L'hub IoT supporta numerose piattaforme e linguaggi (inclusi C, Java e Javascript) tramite gli Azure IoT SDK per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="aecb7-123">IoT Hub supports many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="aecb7-124">Vedere il [Centro per sviluppatori di IoT di Azure] per istruzioni dettagliate su come connettere il dispositivo all'Hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="aecb7-124">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span></span>

<span data-ttu-id="aecb7-125">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="aecb7-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="aecb7-126">Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="aecb7-126">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="aecb7-127">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="aecb7-127">An active Azure account.</span></span> <span data-ttu-id="aecb7-128">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="aecb7-128">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="aecb7-129">Caricare un file da un'app per dispositivi</span><span class="sxs-lookup"><span data-stu-id="aecb7-129">Upload a file from a device app</span></span>

<span data-ttu-id="aecb7-130">In questa sezione si modifica l'app per dispositivi creata in [Inviare messaggi da cloud a dispositivo con l'hub IoT](iot-hub-csharp-csharp-c2d.md) per ricevere i messaggi da cloud a dispositivo dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aecb7-130">In this section, you modify the device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-csharp-csharp-c2d.md) to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="aecb7-131">In Visual Studio fare clic con il pulsante destro del mouse sul progetto **SimulatedDevice**, scegliere **Aggiungi** e quindi **Elemento esistente**.</span><span class="sxs-lookup"><span data-stu-id="aecb7-131">In Visual Studio, right-click the **SimulatedDevice** project, click **Add**, and then click **Existing Item**.</span></span> <span data-ttu-id="aecb7-132">Passare a un file di immagine e includerlo nel progetto.</span><span class="sxs-lookup"><span data-stu-id="aecb7-132">Navigate to an image file and include it in your project.</span></span> <span data-ttu-id="aecb7-133">Nell'esercitazione si presuppone che l'immagine sia denominata `image.jpg`.</span><span class="sxs-lookup"><span data-stu-id="aecb7-133">This tutorial assumes the image is named `image.jpg`.</span></span>

1. <span data-ttu-id="aecb7-134">Fare clic con il pulsante destro del mouse sull'immagine e quindi scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="aecb7-134">Right-click on the image, and then click **Properties**.</span></span> <span data-ttu-id="aecb7-135">Controllare che **Copia nella directory di output** sia impostato su **Copia sempre**.</span><span class="sxs-lookup"><span data-stu-id="aecb7-135">Make sure that **Copy to Output Directory** is set to **Copy always**.</span></span>

    ![][1]

1. <span data-ttu-id="aecb7-136">Nel file **Program.cs** aggiungere le istruzioni seguenti all’inizio del file:</span><span class="sxs-lookup"><span data-stu-id="aecb7-136">In the **Program.cs** file, add the following statements at the top of the file:</span></span>

    ```csharp
    using System.IO;
    ```

1. <span data-ttu-id="aecb7-137">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="aecb7-137">Add the following method to the **Program** class:</span></span>

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
        Console.WriteLine("Time to upload file: {0}ms\n", watch.ElapsedMilliseconds);
    }
    ```

    <span data-ttu-id="aecb7-138">Il metodo `UploadToBlobAsync` accetta il nome del file e l'origine del flusso del file da caricare e gestisce il caricamento nell'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="aecb7-138">The `UploadToBlobAsync` method takes in the file name and stream source of the file to be uploaded and handles the upload to storage.</span></span> <span data-ttu-id="aecb7-139">Nell'app console viene visualizzato il tempo necessario per caricare il file.</span><span class="sxs-lookup"><span data-stu-id="aecb7-139">The console app displays the time it takes to upload the file.</span></span>

1. <span data-ttu-id="aecb7-140">Aggiungere il metodo seguente al metodo **Main** immediatamente prima della riga `Console.ReadLine()`:</span><span class="sxs-lookup"><span data-stu-id="aecb7-140">Add the following method in the **Main** method, right before the `Console.ReadLine()` line:</span></span>

    ```csharp
    SendToBlobAsync();
    ```

> [!NOTE]
> <span data-ttu-id="aecb7-141">Per semplicità, in questa esercitazione non si implementa alcun criterio di nuovi tentativi.</span><span class="sxs-lookup"><span data-stu-id="aecb7-141">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="aecb7-142">Nel codice di produzione è consigliabile implementare criteri di ripetizione dei tentativi, ad esempio un backoff esponenziale, come indicato nell'articolo di MSDN [Transient Fault Handling](Gestione degli errori temporanei).</span><span class="sxs-lookup"><span data-stu-id="aecb7-142">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="aecb7-143">Ricevere la notifica di caricamento di un file</span><span class="sxs-lookup"><span data-stu-id="aecb7-143">Receive a file upload notification</span></span>

<span data-ttu-id="aecb7-144">In questa sezione verrà scritta un'app console di .NET che riceve messaggi di notifica di caricamento dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="aecb7-144">In this section, you write a .NET console app that receives file upload notification messages from IoT Hub.</span></span>

1. <span data-ttu-id="aecb7-145">Nella soluzione di Visual Studio corrente creare un progetto di Windows in Visual C# usando il modello di progetto **Applicazione console** .</span><span class="sxs-lookup"><span data-stu-id="aecb7-145">In the current Visual Studio solution, create a Visual C# Windows project by using the **Console Application** project template.</span></span> <span data-ttu-id="aecb7-146">Denominare il progetto **ReadFileUploadNotification**.</span><span class="sxs-lookup"><span data-stu-id="aecb7-146">Name the project **ReadFileUploadNotification**.</span></span>

    ![Nuovo progetto in Visual Studio][2]

1. <span data-ttu-id="aecb7-148">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto **ReadFileUploadNotification** e quindi scegliere **Gestisci pacchetti NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="aecb7-148">In Solution Explorer, right-click the **ReadFileUploadNotification** project, and then click **Manage NuGet Packages...**.</span></span>

1. <span data-ttu-id="aecb7-149">Nella finestra **Gestisci pacchetti NuGet** cercare **Microsoft.Azure.Devices**, fare clic su **Installa** e accettare le condizioni per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="aecb7-149">In the **NuGet Package Manager** window, search for **Microsoft.Azure.Devices**, click **Install**, and accept the terms of use.</span></span>

    <span data-ttu-id="aecb7-150">L'azione consente di scaricare, installare e aggiungere un riferimento al [pacchetto NuGet Azure IoT Service SDK] nel progetto **ReadFileUploadNotification**.</span><span class="sxs-lookup"><span data-stu-id="aecb7-150">This action downloads, installs, and adds a reference to the [Azure IoT service SDK NuGet package] in the **ReadFileUploadNotification** project.</span></span>

1. <span data-ttu-id="aecb7-151">Nel file **Program.cs** aggiungere le istruzioni seguenti all’inizio del file:</span><span class="sxs-lookup"><span data-stu-id="aecb7-151">In the **Program.cs** file, add the following statements at the top of the file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices;
    ```

1. <span data-ttu-id="aecb7-152">Aggiungere i campi seguenti alla classe **Program** .</span><span class="sxs-lookup"><span data-stu-id="aecb7-152">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="aecb7-153">Sostituire il valore del segnaposto con la stringa di connessione all'hub IoT da [Introduzione all'hub IoT]:</span><span class="sxs-lookup"><span data-stu-id="aecb7-153">Substitute the placeholder value with the IoT hub connection string from [Get started with IoT Hub]:</span></span>

    ```csharp
    static ServiceClient serviceClient;
    static string connectionString = "{iot hub connection string}";
    ```

1. <span data-ttu-id="aecb7-154">Aggiungere il metodo seguente alla classe **Program** :</span><span class="sxs-lookup"><span data-stu-id="aecb7-154">Add the following method to the **Program** class:</span></span>

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

    <span data-ttu-id="aecb7-155">Si noti che il modello di ricezione è identico a quello usato per ricevere messaggi da cloud a dispositivo dall'app per dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aecb7-155">Note this receive pattern is the same one used to receive cloud-to-device messages from the device app.</span></span>

1. <span data-ttu-id="aecb7-156">Aggiungere infine le righe seguenti al metodo **Main** :</span><span class="sxs-lookup"><span data-stu-id="aecb7-156">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive file upload notifications\n");
    serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
    ReceiveFileUploadNotificationAsync();
    Console.WriteLine("Press Enter to exit\n");
    Console.ReadLine();
    ```

## <a name="run-the-applications"></a><span data-ttu-id="aecb7-157">Eseguire le applicazioni</span><span class="sxs-lookup"><span data-stu-id="aecb7-157">Run the applications</span></span>

<span data-ttu-id="aecb7-158">A questo punto è possibile eseguire le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="aecb7-158">Now you are ready to run the applications.</span></span>

1. <span data-ttu-id="aecb7-159">In Visual Studio fare clic con il pulsante destro del mouse sulla soluzione e selezionare **Imposta progetti di avvio**.</span><span class="sxs-lookup"><span data-stu-id="aecb7-159">In Visual Studio, right-click your solution, and select **Set StartUp projects**.</span></span> <span data-ttu-id="aecb7-160">Selezionare **Progetti di avvio multipli**, quindi selezionare l'azione **Avvia** per **ReadFileUploadNotification** e **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="aecb7-160">Select **Multiple startup projects**, then select the **Start** action for **ReadFileUploadNotification** and **SimulatedDevice**.</span></span>

1. <span data-ttu-id="aecb7-161">Premere **F5**.</span><span class="sxs-lookup"><span data-stu-id="aecb7-161">Press **F5**.</span></span> <span data-ttu-id="aecb7-162">Si avviano entrambe le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="aecb7-162">Both applications should start.</span></span> <span data-ttu-id="aecb7-163">Verrà visualizzato il messaggio di completamento del caricamento in un'applicazione console e il messaggio di notifica di caricamento ricevuto da altre applicazioni console.</span><span class="sxs-lookup"><span data-stu-id="aecb7-163">You should see the upload completed in one console app and the upload notification message received by the other console app.</span></span> <span data-ttu-id="aecb7-164">È possibile usare il [portale di Azure] o Esplora server di Visual Studio per verificare la presenza del file caricato nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="aecb7-164">You can use the [Azure portal] or Visual Studio Server Explorer to check for the presence of the uploaded file in your Azure Storage account.</span></span>

    ![][50]

## <a name="next-steps"></a><span data-ttu-id="aecb7-165">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aecb7-165">Next steps</span></span>

<span data-ttu-id="aecb7-166">In questa esercitazione si è appreso come usare le funzionalità di caricamento file dell'hub IoT per semplificare i caricamenti di file dai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="aecb7-166">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span></span> <span data-ttu-id="aecb7-167">È possibile continuare a esplorare le funzionalità e gli scenari dell'hub IoT vedendo i seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="aecb7-167">You can continue to explore IoT hub features and scenarios with the following articles:</span></span>

* <span data-ttu-id="aecb7-168">[Creare un hub IoT a livello di codice][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="aecb7-168">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="aecb7-169">[Introduzione a C SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="aecb7-169">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="aecb7-170">[Azure IoT SDKs][lnk-sdks] (SDK di IoT di Azure)</span><span class="sxs-lookup"><span data-stu-id="aecb7-170">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="aecb7-171">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="aecb7-171">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="aecb7-172">[Simulazione di un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="aecb7-172">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png

<!-- Links -->

<span data-ttu-id="aecb7-173">[portale di Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="aecb7-173">[Azure portal]: https://portal.azure.com/</span></span>

<span data-ttu-id="aecb7-174">[Centro per sviluppatori di IoT di Azure]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="aecb7-174">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>

<span data-ttu-id="aecb7-175">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="aecb7-175">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="aecb7-176">[pacchetto NuGet Azure IoT Service SDK]: https://www.nuget.org/packages/Microsoft.Azure.Devices/</span><span class="sxs-lookup"><span data-stu-id="aecb7-176">[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md
