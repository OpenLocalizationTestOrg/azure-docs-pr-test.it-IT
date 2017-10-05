---
title: Caricare file dai dispositivi nell'hub IoT di Azure con Java | Microsoft Docs
description: Come caricare file da un dispositivo al cloud usando Azure IoT SDK per dispositivi per Java. I file caricati vengono salvati in un contenitore BLOB di archiviazione di Azure.
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4759d229-f856-4526-abda-414f8b00a56d
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: c917a3b3e16f1e84f202d6c87a04faf642266701
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-from-your-device-to-the-cloud-with-iot-hub"></a><span data-ttu-id="8c9d0-104">Caricare file da un dispositivo al cloud con l'hub IoT</span><span class="sxs-lookup"><span data-stu-id="8c9d0-104">Upload files from your device to the cloud with IoT Hub</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="8c9d0-105">Questa esercitazione si basa sul codice contenuto nell'esercitazione [Inviare messaggi da cloud a dispositivo con l'hub IoT](iot-hub-java-java-c2d.md) e illustra come usare le [funzionalità di caricamento dei file dell'hub IoT](iot-hub-devguide-file-upload.md) per caricare un file in [Archiviazione BLOB di Azure](../storage/index.md).</span><span class="sxs-lookup"><span data-stu-id="8c9d0-105">This tutorial builds on the code in the [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorial to show you how to use the [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) to upload a file to [Azure blob storage](../storage/index.md).</span></span> <span data-ttu-id="8c9d0-106">L'esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-106">The tutorial shows you how to:</span></span>

- <span data-ttu-id="8c9d0-107">Specificare in modo sicuro un dispositivo con un URI del BLOB di Azure per il caricamento di un file.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="8c9d0-108">Usare le notifiche di caricamento di file dell'hub IoT per attivare l'elaborazione del file nel back-end dell'app.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-108">Use the IoT Hub file upload notifications to trigger processing the file in your app back end.</span></span>

<span data-ttu-id="8c9d0-109">Le esercitazioni [Introduzione all'hub IoT](iot-hub-java-java-getstarted.md) e [Inviare messaggi da cloud a dispositivo con l'hub IoT](iot-hub-java-java-c2d.md) illustrano le funzionalità di messaggistica di base da dispositivo a cloud e da cloud a dispositivo dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-109">The [Get started with IoT Hub](iot-hub-java-java-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorials show the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="8c9d0-110">L'esercitazione [Elaborare messaggi da dispositivo a cloud](iot-hub-java-java-process-d2c.md) illustra come archiviare in modo affidabile i messaggi da dispositivo a cloud nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-110">The [Process Device-to-Cloud messages](iot-hub-java-java-process-d2c.md) tutorial describes a way to reliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="8c9d0-111">Tuttavia in alcuni scenari non è possibile mappare facilmente i dati che i dispositivi inviano in messaggi relativamente ridotti da dispositivo a cloud, che l'hub IoT accetta.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-111">However, in some scenarios you cannot easily map the data your devices send into the relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="8c9d0-112">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-112">For example:</span></span>

* <span data-ttu-id="8c9d0-113">File di grandi dimensioni che contengono immagini</span><span class="sxs-lookup"><span data-stu-id="8c9d0-113">Large files that contain images</span></span>
* <span data-ttu-id="8c9d0-114">Video</span><span class="sxs-lookup"><span data-stu-id="8c9d0-114">Videos</span></span>
* <span data-ttu-id="8c9d0-115">Dati di vibrazione campionati ad alta frequenza</span><span class="sxs-lookup"><span data-stu-id="8c9d0-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="8c9d0-116">Qualche tipo di dati pre-elaborati.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-116">Some form of preprocessed data.</span></span>

<span data-ttu-id="8c9d0-117">Questi dati in genere vengono elaborati in batch nel cloud con strumenti come [Azure Data Factory](../data-factory/index.md) o lo stack [Hadoop](../hdinsight/index.md).</span><span class="sxs-lookup"><span data-stu-id="8c9d0-117">These files are typically batch processed in the cloud using tools such as [Azure Data Factory](../data-factory/index.md) or the [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="8c9d0-118">Quando è necessario caricare file da un dispositivo, è comunque possibile usare la sicurezza e l'affidabilità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-118">When you need to upland files from a device, you can still use the security and reliability of IoT Hub.</span></span>

<span data-ttu-id="8c9d0-119">Al termine di questa esercitazione verranno eseguite due app console Java:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-119">At the end of this tutorial you run two Java console apps:</span></span>

* <span data-ttu-id="8c9d0-120">**simulated-device**, una versione modificata dell'app creata nell'esercitazione [Inviare messaggi da cloud a dispositivo con l'hub IoT].</span><span class="sxs-lookup"><span data-stu-id="8c9d0-120">**simulated-device**, a modified version of the app created in the [Send Cloud-to-Device messages with IoT Hub] tutorial.</span></span> <span data-ttu-id="8c9d0-121">Ciò consente di caricare un file nell'archivio tramite un URI con firma di accesso condiviso fornito dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-121">This app uploads a file to storage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="8c9d0-122">**read-file-upload-notification**, che riceve le notifiche di caricamento file dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-122">**read-file-upload-notification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="8c9d0-123">L'hub IoT supporta numerose piattaforme e linguaggi (inclusi C, .NET e Javascript) tramite gli Azure IoT SDK per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-123">IoT Hub supports many device platforms and languages (including C, .NET, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="8c9d0-124">Vedere il [Centro per sviluppatori di IoT di Azure] per istruzioni dettagliate su come connettere il dispositivo all'Hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-124">Refer to the [Azure IoT Developer Center] for step-by-step instructions on how to connect your device to Azure IoT Hub.</span></span>

<span data-ttu-id="8c9d0-125">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-125">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="8c9d0-126">[Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) più recente</span><span class="sxs-lookup"><span data-stu-id="8c9d0-126">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="8c9d0-127">Maven 3</span><span class="sxs-lookup"><span data-stu-id="8c9d0-127">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="8c9d0-128">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-128">An active Azure account.</span></span> <span data-ttu-id="8c9d0-129">Se non si ha un account, è possibile crearne uno [gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-129">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="8c9d0-130">Caricare un file da un'app per dispositivi</span><span class="sxs-lookup"><span data-stu-id="8c9d0-130">Upload a file from a device app</span></span>

<span data-ttu-id="8c9d0-131">In questa sezione viene modificata l'app per dispositivi creata in [Inviare messaggi da cloud a dispositivo con l'hub IoT](iot-hub-java-java-c2d.md) per caricare un file nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-131">In this section, you modify the device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) to upload a file to IoT hub.</span></span>

1. <span data-ttu-id="8c9d0-132">Copiare un file di immagine nella cartella `simulated-device` e rinominarlo `myimage.png`.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-132">Copy an image file to the `simulated-device` folder and rename it `myimage.png`.</span></span>

1. <span data-ttu-id="8c9d0-133">Aprire il file `simulated-device\src\main\java\com\mycompany\app\App.java` in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-133">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="8c9d0-134">Aggiungere la dichiarazione di variabile alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-134">Add the variable declaration to the **App** class:</span></span>

    ```java
    private static String fileName = "myimage.png";
    ```

1. <span data-ttu-id="8c9d0-135">Per elaborare i messaggi di richiamata dello stato di caricamento del file, aggiungere la classe annidata seguente alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-135">To process file upload status callback messages, add the following nested class to the **App** class:</span></span>

    ```java
    // Define a callback method to print status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to file upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="8c9d0-136">Per caricare le immagini nell'hub IoT, aggiungere il metodo seguente alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-136">To upload images to IoT Hub, add the following method to the **App** class to upload images to IoT Hub:</span></span>

    ```java
    // Use IoT Hub to upload a file asynchronously to Azure blob storage.
    private static void uploadFile(String fullFileName) throws FileNotFoundException, IOException
    {
      File file = new File(fullFileName);
      InputStream inputStream = new FileInputStream(file);
      long streamLength = file.length();

      client.uploadToBlobAsync(fileName, inputStream, streamLength, new FileUploadStatusCallBack(), null);
    }
    ```

1. <span data-ttu-id="8c9d0-137">Modificare il metodo **main** per chiamare il metodo **uploadFile** come illustrato nel frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-137">Modify the **main** method to call the **uploadFile** method as shown in the following snippet:</span></span>

    ```java
    client.open();

    try
    {
      // Get the filename and start the upload.
      String fullFileName = System.getProperty("user.dir") + File.separator + fileName;
      uploadFile(fullFileName);
      System.out.println("File upload started with success");
    }
    catch (Exception e)
    {
      System.out.println("Exception uploading file: " + e.getCause() + " \nERROR: " + e.getMessage());
    }

    MessageSender sender = new MessageSender();
    ```

1. <span data-ttu-id="8c9d0-138">Usare il comando seguente per compilare l'app **simulated-device** e verificare la presenza di eventuali errori:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-138">Use the following command to build the **simulated-device** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="8c9d0-139">Ricevere la notifica di caricamento di un file</span><span class="sxs-lookup"><span data-stu-id="8c9d0-139">Receive a file upload notification</span></span>

<span data-ttu-id="8c9d0-140">In questa sezione viene creata un'app console Java che riceve messaggi di notifica di caricamento file dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-140">In this section, you create a Java console app that receives file upload notification messages from IoT Hub.</span></span>

<span data-ttu-id="8c9d0-141">Per completare questa sezione è necessaria la stringa di connessione **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-141">You need the **iothubowner** connection string for your IoT Hub to complete this section.</span></span> <span data-ttu-id="8c9d0-142">È possibile trovare la stringa di connessione nel [portale di Azure](https://portal.azure.com/) nel pannello **Criteri di accesso condiviso**.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-142">You can find the connection string in the [Azure portal](https://portal.azure.com/) on the **Shared access policy** blade.</span></span>

1. <span data-ttu-id="8c9d0-143">Creare un progetto Maven denominato **read-file-upload-notification** usando questo comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-143">Create a Maven project called **read-file-upload-notification** using the following command at your command prompt.</span></span> <span data-ttu-id="8c9d0-144">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-144">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. <span data-ttu-id="8c9d0-145">Al prompt dei comandi passare alla nuova cartella `read-file-upload-notification`.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-145">At your command prompt, navigate to the new `read-file-upload-notification` folder.</span></span>

1. <span data-ttu-id="8c9d0-146">In un editor di testo aprire il file `pom.xml` nella cartella `read-file-upload-notification` e aggiungere la dipendenza seguente al nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-146">Using a text editor, open the `pom.xml` file in the `read-file-upload-notification` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="8c9d0-147">L'aggiunta della dipendenza consente di usare il pacchetto **iothub-java-service-client** nell'applicazione per comunicare con il servizio hub IoT:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-147">Adding the dependency enables you to use the **iothub-java-service-client** package in your application to communicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="8c9d0-148">È possibile cercare la versione più recente di **iot-service-client** usando la [ricerca di Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="8c9d0-148">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="8c9d0-149">Salvare e chiudere il file `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-149">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="8c9d0-150">Aprire il file `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-150">Using a text editor, open the `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="8c9d0-151">Aggiungere al file le istruzioni **import** seguenti:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-151">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. <span data-ttu-id="8c9d0-152">Aggiungere le variabili a livello di classe seguenti alla classe **App** :</span><span class="sxs-lookup"><span data-stu-id="8c9d0-152">Add the following class-level variables to the **App** class:</span></span>

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. <span data-ttu-id="8c9d0-153">Per stampare le informazioni relative al caricamento del file nella console, aggiungere la classe annidata seguente alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-153">To print information about the file upload to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Create a thread to receive file upload notifications.
    private static class ShowFileUploadNotifications implements Runnable {
      public void run() {
        try {
          while (true) {
            System.out.println("Recieve file upload notifications...");
            FileUploadNotification fileUploadNotification = fileUploadNotificationReceiver.receive();
            if (fileUploadNotification != null) {
              System.out.println("File Upload notification received");
              System.out.println("Device Id : " + fileUploadNotification.getDeviceId());
              System.out.println("Blob Uri: " + fileUploadNotification.getBlobUri());
              System.out.println("Blob Name: " + fileUploadNotification.getBlobName());
              System.out.println("Last Updated : " + fileUploadNotification.getLastUpdatedTimeDate());
              System.out.println("Blob Size (Bytes): " + fileUploadNotification.getBlobSizeInBytes());
              System.out.println("Enqueued Time: " + fileUploadNotification.getEnqueuedTimeUtcDate());
            }
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="8c9d0-154">Per avviare il thread che rimane in ascolto delle notifiche di caricamento del file, aggiungere il codice seguente al metodo **main**:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-154">To start the thread that listens for file upload notifications, add the following code to the **main** method:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(connectionString, protocol);

      if (serviceClient != null) {
        serviceClient.open();

        // Get a file upload notification receiver from the ServiceClient.
        fileUploadNotificationReceiver = serviceClient.getFileUploadNotificationReceiver();
        fileUploadNotificationReceiver.open();

        // Start the thread to receive file upload notifications.
        ShowFileUploadNotifications showFileUploadNotifications = new ShowFileUploadNotifications();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        executor.execute(showFileUploadNotifications);

        System.out.println("Press ENTER to exit.");
        System.in.read();
        executor.shutdownNow();
        System.out.println("Shutting down sample...");
        fileUploadNotificationReceiver.close();
        serviceClient.close();
      }
    }
    ```

1. <span data-ttu-id="8c9d0-155">Salvare e chiudere il file `read-file-upload-notification\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-155">Save and close the `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="8c9d0-156">Usare il comando seguente per compilare l'app **read-file-upload-notification** e verificare la presenza di eventuali errori:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-156">Use the following command to build the **read-file-upload-notification** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-the-applications"></a><span data-ttu-id="8c9d0-157">Eseguire le applicazioni</span><span class="sxs-lookup"><span data-stu-id="8c9d0-157">Run the applications</span></span>

<span data-ttu-id="8c9d0-158">A questo punto è possibile eseguire le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-158">Now you are ready to run the applications.</span></span>

<span data-ttu-id="8c9d0-159">Al prompt dei comandi nella cartella `read-file-upload-notification` eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-159">At a command prompt in the `read-file-upload-notification` folder, run the following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="8c9d0-160">Al prompt dei comandi nella cartella `simulated-device` eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-160">At a command prompt in the `simulated-device` folder, run the following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="8c9d0-161">Lo screenshot seguente presenta l'output dell'app **simulated-device**:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-161">The following screenshot shows the output from the **simulated-device** app:</span></span>

![Output dell'app simulated-device](media/iot-hub-java-java-upload/simulated-device.png)

<span data-ttu-id="8c9d0-163">Lo screenshot seguente presenta l'output dell'app **read-file-upload-notification**:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-163">The following screenshot shows the output from the **read-file-upload-notification** app:</span></span>

![Output dell'app read-file-upload-notification](media/iot-hub-java-java-upload/read-file-upload-notification.png)

<span data-ttu-id="8c9d0-165">Per visualizzare il file caricato nel contenitore di archiviazione configurato, è possibile usare il portale:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-165">You can use the portal to view the uploaded file in the storage container you configured:</span></span>

![File caricato](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a><span data-ttu-id="8c9d0-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8c9d0-167">Next steps</span></span>

<span data-ttu-id="8c9d0-168">In questa esercitazione si è appreso come usare le funzionalità di caricamento file dell'hub IoT per semplificare i caricamenti di file dai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8c9d0-168">In this tutorial, you learned how to use the file upload capabilities of IoT Hub to simplify file uploads from devices.</span></span> <span data-ttu-id="8c9d0-169">È possibile continuare a esplorare le funzionalità e gli scenari dell'hub IoT vedendo i seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-169">You can continue to explore IoT hub features and scenarios with the following articles:</span></span>

* <span data-ttu-id="8c9d0-170">[Creare un hub IoT a livello di codice][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="8c9d0-170">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="8c9d0-171">[Introduzione a C SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="8c9d0-171">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="8c9d0-172">[Azure IoT SDKs][lnk-sdks] (SDK di IoT di Azure)</span><span class="sxs-lookup"><span data-stu-id="8c9d0-172">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="8c9d0-173">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="8c9d0-173">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="8c9d0-174">[Simulazione di un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="8c9d0-174">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png
[3]: ./media/iot-hub-csharp-csharp-file-upload/enable-file-notifications.png

<!-- Links -->



[Centro per sviluppatori di IoT di Azure]: http://www.azure.com/develop/iot

[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure Storage]:../storage/common/storage-create-storage-account.md#create-a-storage-account
[lnk-configure-upload]: iot-hub-configure-file-upload.md
[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md


