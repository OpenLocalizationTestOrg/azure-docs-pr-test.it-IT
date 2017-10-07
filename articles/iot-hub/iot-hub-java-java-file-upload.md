---
title: file aaaUpload da dispositivi tooAzure IoT Hub con Java | Documenti Microsoft
description: "Modalità tooupload file da un cloud toohello dispositivo utilizzando il dispositivo IoT di Azure SDK per Java. I file caricati vengono salvati in un contenitore BLOB di archiviazione di Azure."
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
ms.openlocfilehash: e305fe61bf7ca0aeb2c092bc2c7efebdc78d4f68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a><span data-ttu-id="31be4-104">Caricare file dal cloud toohello dispositivo con l'IoT Hub</span><span class="sxs-lookup"><span data-stu-id="31be4-104">Upload files from your device toohello cloud with IoT Hub</span></span>

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

<span data-ttu-id="31be4-105">Questa esercitazione si basa su codice hello in hello [inviare messaggi da Cloud a dispositivo con l'IoT Hub](iot-hub-java-java-c2d.md) tooshow esercitazione si come hello toouse [file di funzionalità di caricamento dell'IoT Hub](iot-hub-devguide-file-upload.md) tooupload un file troppo[ Archiviazione blob di Azure](../storage/index.md).</span><span class="sxs-lookup"><span data-stu-id="31be4-105">This tutorial builds on hello code in hello [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorial tooshow you how toouse hello [file upload capabilities of IoT Hub](iot-hub-devguide-file-upload.md) tooupload a file too[Azure blob storage](../storage/index.md).</span></span> <span data-ttu-id="31be4-106">Hello esercitazione vengono illustrate le modalità per:</span><span class="sxs-lookup"><span data-stu-id="31be4-106">hello tutorial shows you how to:</span></span>

- <span data-ttu-id="31be4-107">Specificare in modo sicuro un dispositivo con un URI del BLOB di Azure per il caricamento di un file.</span><span class="sxs-lookup"><span data-stu-id="31be4-107">Securely provide a device with an Azure blob URI for uploading a file.</span></span>
- <span data-ttu-id="31be4-108">Utilizzare l'elaborazione di tootrigger notifiche di IoT Hub file caricamento del file hello nel back-end app hello.</span><span class="sxs-lookup"><span data-stu-id="31be4-108">Use hello IoT Hub file upload notifications tootrigger processing hello file in your app back end.</span></span>

<span data-ttu-id="31be4-109">Hello [iniziare con l'IoT Hub](iot-hub-java-java-getstarted.md) e [inviare messaggi da Cloud a dispositivo con l'IoT Hub](iot-hub-java-java-c2d.md) le esercitazioni illustrano hello da dispositivo a cloud e cloud a dispositivo messaggistica funzionalità di base di IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="31be4-109">hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) and [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tutorials show hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span> <span data-ttu-id="31be4-110">Hello [i messaggi di processo da dispositivo a Cloud](iot-hub-java-java-process-d2c.md) esercitazione viene descritto un modo tooreliably memorizza da dispositivo a cloud messaggi nel servizio di archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="31be4-110">hello [Process Device-to-Cloud messages](iot-hub-java-java-process-d2c.md) tutorial describes a way tooreliably store device-to-cloud messages in Azure blob storage.</span></span> <span data-ttu-id="31be4-111">Tuttavia, in alcuni scenari è possibile mappare facilmente dati hello che i dispositivi di trasmissione in messaggi da dispositivo a cloud relativamente piccolo hello che accetta l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="31be4-111">However, in some scenarios you cannot easily map hello data your devices send into hello relatively small device-to-cloud messages that IoT Hub accepts.</span></span> <span data-ttu-id="31be4-112">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="31be4-112">For example:</span></span>

* <span data-ttu-id="31be4-113">File di grandi dimensioni che contengono immagini</span><span class="sxs-lookup"><span data-stu-id="31be4-113">Large files that contain images</span></span>
* <span data-ttu-id="31be4-114">Video</span><span class="sxs-lookup"><span data-stu-id="31be4-114">Videos</span></span>
* <span data-ttu-id="31be4-115">Dati di vibrazione campionati ad alta frequenza</span><span class="sxs-lookup"><span data-stu-id="31be4-115">Vibration data sampled at high frequency</span></span>
* <span data-ttu-id="31be4-116">Qualche tipo di dati pre-elaborati.</span><span class="sxs-lookup"><span data-stu-id="31be4-116">Some form of preprocessed data.</span></span>

<span data-ttu-id="31be4-117">Questi file sono in genere batch elaborato nel cloud hello tramite strumenti come [Data Factory di Azure](../data-factory/index.md) o hello [Hadoop](../hdinsight/index.md) dello stack.</span><span class="sxs-lookup"><span data-stu-id="31be4-117">These files are typically batch processed in hello cloud using tools such as [Azure Data Factory](../data-factory/index.md) or hello [Hadoop](../hdinsight/index.md) stack.</span></span> <span data-ttu-id="31be4-118">Quando è necessario tooupland file da un dispositivo, è possibile utilizzare ancora hello protezione e affidabilità dell'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="31be4-118">When you need tooupland files from a device, you can still use hello security and reliability of IoT Hub.</span></span>

<span data-ttu-id="31be4-119">Alla fine di hello di questa esercitazione è eseguire due applicazioni di console Java:</span><span class="sxs-lookup"><span data-stu-id="31be4-119">At hello end of this tutorial you run two Java console apps:</span></span>

* <span data-ttu-id="31be4-120">**dispositivo simulato**, una versione modificata dell'applicazione hello creato nell'esercitazione hello [messaggi trasmissione Cloud a dispositivo con l'IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="31be4-120">**simulated-device**, a modified version of hello app created in hello [Send Cloud-to-Device messages with IoT Hub] tutorial.</span></span> <span data-ttu-id="31be4-121">Questa app carica toostorage un file utilizzando un URI SAS forniti per l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="31be4-121">This app uploads a file toostorage using a SAS URI provided by your IoT hub.</span></span>
* <span data-ttu-id="31be4-122">**read-file-upload-notification**, che riceve le notifiche di caricamento file dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="31be4-122">**read-file-upload-notification**, which receives file upload notifications from your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="31be4-123">L'hub IoT supporta numerose piattaforme e linguaggi (inclusi C, .NET e Javascript) tramite gli Azure IoT SDK per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="31be4-123">IoT Hub supports many device platforms and languages (including C, .NET, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="31be4-124">Fare riferimento toohello [Centro per sviluppatori di Azure IoT] per istruzioni dettagliate su come tooconnect il tooAzure dispositivo IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="31be4-124">Refer toohello [Azure IoT Developer Center] for step-by-step instructions on how tooconnect your device tooAzure IoT Hub.</span></span>

<span data-ttu-id="31be4-125">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="31be4-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="31be4-126">versione più recente Hello [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="31be4-126">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="31be4-127">Maven 3</span><span class="sxs-lookup"><span data-stu-id="31be4-127">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="31be4-128">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="31be4-128">An active Azure account.</span></span> <span data-ttu-id="31be4-129">Se non si ha un account, è possibile crearne uno [gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="31be4-129">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a><span data-ttu-id="31be4-130">Caricare un file da un'app per dispositivi</span><span class="sxs-lookup"><span data-stu-id="31be4-130">Upload a file from a device app</span></span>

<span data-ttu-id="31be4-131">In questa sezione, si modifica hello app del dispositivo è stato creato in [inviare messaggi da Cloud a dispositivo con l'IoT Hub](iot-hub-java-java-c2d.md) tooupload un hub di tooIoT file.</span><span class="sxs-lookup"><span data-stu-id="31be4-131">In this section, you modify hello device app you created in [Send Cloud-to-Device messages with IoT Hub](iot-hub-java-java-c2d.md) tooupload a file tooIoT hub.</span></span>

1. <span data-ttu-id="31be4-132">Copiare un toohello di file di immagine `simulated-device` cartella e rinominarlo `myimage.png`.</span><span class="sxs-lookup"><span data-stu-id="31be4-132">Copy an image file toohello `simulated-device` folder and rename it `myimage.png`.</span></span>

1. <span data-ttu-id="31be4-133">Utilizzando un editor di testo, aprire hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="31be4-133">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="31be4-134">Aggiungere hello dichiarazione di variabile toohello **App** classe:</span><span class="sxs-lookup"><span data-stu-id="31be4-134">Add hello variable declaration toohello **App** class:</span></span>

    ```java
    private static String fileName = "myimage.png";
    ```

1. <span data-ttu-id="31be4-135">tooprocess callback messaggi di stato di caricamento del file, aggiungere il seguente hello annidati classe toohello **App** classe:</span><span class="sxs-lookup"><span data-stu-id="31be4-135">tooprocess file upload status callback messages, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="31be4-136">tooupload immagini tooIoT Hub, aggiungere hello seguente metodo toohello **App** tooupload classe immagini tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="31be4-136">tooupload images tooIoT Hub, add hello following method toohello **App** class tooupload images tooIoT Hub:</span></span>

    ```java
    // Use IoT Hub tooupload a file asynchronously tooAzure blob storage.
    private static void uploadFile(String fullFileName) throws FileNotFoundException, IOException
    {
      File file = new File(fullFileName);
      InputStream inputStream = new FileInputStream(file);
      long streamLength = file.length();

      client.uploadToBlobAsync(fileName, inputStream, streamLength, new FileUploadStatusCallBack(), null);
    }
    ```

1. <span data-ttu-id="31be4-137">Modificare hello **principale** hello toocall metodo **uploadFile** metodo come illustrato nel seguente frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="31be4-137">Modify hello **main** method toocall hello **uploadFile** method as shown in hello following snippet:</span></span>

    ```java
    client.open();

    try
    {
      // Get hello filename and start hello upload.
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

1. <span data-ttu-id="31be4-138">Comando che segue di hello utilizzare hello toobuild **dispositivo simulato** app e controllare gli errori:</span><span class="sxs-lookup"><span data-stu-id="31be4-138">Use hello following command toobuild hello **simulated-device** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a><span data-ttu-id="31be4-139">Ricevere la notifica di caricamento di un file</span><span class="sxs-lookup"><span data-stu-id="31be4-139">Receive a file upload notification</span></span>

<span data-ttu-id="31be4-140">In questa sezione viene creata un'app console Java che riceve messaggi di notifica di caricamento file dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="31be4-140">In this section, you create a Java console app that receives file upload notification messages from IoT Hub.</span></span>

<span data-ttu-id="31be4-141">È necessario hello **iothubowner** stringa di connessione per l'IoT Hub di toocomplete in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="31be4-141">You need hello **iothubowner** connection string for your IoT Hub toocomplete this section.</span></span> <span data-ttu-id="31be4-142">È possibile trovare la stringa di connessione hello in hello [portale di Azure](https://portal.azure.com/) su hello **i criteri di accesso condiviso** blade.</span><span class="sxs-lookup"><span data-stu-id="31be4-142">You can find hello connection string in hello [Azure portal](https://portal.azure.com/) on hello **Shared access policy** blade.</span></span>

1. <span data-ttu-id="31be4-143">Creare un progetto di Maven denominato **notifica caricamento di file di lettura** utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="31be4-143">Create a Maven project called **read-file-upload-notification** using hello following command at your command prompt.</span></span> <span data-ttu-id="31be4-144">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="31be4-144">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. <span data-ttu-id="31be4-145">Al prompt dei comandi, passare toohello nuova `read-file-upload-notification` cartella.</span><span class="sxs-lookup"><span data-stu-id="31be4-145">At your command prompt, navigate toohello new `read-file-upload-notification` folder.</span></span>

1. <span data-ttu-id="31be4-146">Utilizzando un editor di testo, aprire hello `pom.xml` file hello `read-file-upload-notification` cartella e aggiungere hello seguente dipendenza toohello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="31be4-146">Using a text editor, open hello `pom.xml` file in hello `read-file-upload-notification` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="31be4-147">Aggiunta della dipendenza hello consente hello toouse **client del servizio di linguaggio hub IOT** pacchetto in toocommunicate l'applicazione con il servizio di hub IoT:</span><span class="sxs-lookup"><span data-stu-id="31be4-147">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="31be4-148">È possibile verificare la versione più recente di hello di **client di servizi iot** utilizzando [ricerca Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="31be4-148">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="31be4-149">Salvare e chiudere hello `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="31be4-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="31be4-150">Utilizzando un editor di testo, aprire hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="31be4-150">Using a text editor, open hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="31be4-151">Aggiungere il seguente hello **importare** file toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="31be4-151">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. <span data-ttu-id="31be4-152">Aggiungere hello seguenti variabili a livello di classe toohello **App** classe:</span><span class="sxs-lookup"><span data-stu-id="31be4-152">Add hello following class-level variables toohello **App** class:</span></span>

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. <span data-ttu-id="31be4-153">tooprint informazioni console toohello caricamento del file hello, aggiungere il seguente hello annidati classe toohello **App** classe:</span><span class="sxs-lookup"><span data-stu-id="31be4-153">tooprint information about hello file upload toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Create a thread tooreceive file upload notifications.
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

1. <span data-ttu-id="31be4-154">thread hello toostart in attesa di notifiche di caricamento di file, aggiungere hello seguente codice toohello **principale** metodo:</span><span class="sxs-lookup"><span data-stu-id="31be4-154">toostart hello thread that listens for file upload notifications, add hello following code toohello **main** method:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(connectionString, protocol);

      if (serviceClient != null) {
        serviceClient.open();

        // Get a file upload notification receiver from hello ServiceClient.
        fileUploadNotificationReceiver = serviceClient.getFileUploadNotificationReceiver();
        fileUploadNotificationReceiver.open();

        // Start hello thread tooreceive file upload notifications.
        ShowFileUploadNotifications showFileUploadNotifications = new ShowFileUploadNotifications();
        ExecutorService executor = Executors.newFixedThreadPool(1);
        executor.execute(showFileUploadNotifications);

        System.out.println("Press ENTER tooexit.");
        System.in.read();
        executor.shutdownNow();
        System.out.println("Shutting down sample...");
        fileUploadNotificationReceiver.close();
        serviceClient.close();
      }
    }
    ```

1. <span data-ttu-id="31be4-155">Salvare e chiudere hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="31be4-155">Save and close hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="31be4-156">Comando che segue di hello utilizzare hello toobuild **notifica caricamento di file di lettura** app e controllare gli errori:</span><span class="sxs-lookup"><span data-stu-id="31be4-156">Use hello following command toobuild hello **read-file-upload-notification** app and check for errors:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="31be4-157">Eseguire applicazioni hello</span><span class="sxs-lookup"><span data-stu-id="31be4-157">Run hello applications</span></span>

<span data-ttu-id="31be4-158">Si è ora applicazioni hello toorun pronto.</span><span class="sxs-lookup"><span data-stu-id="31be4-158">Now you are ready toorun hello applications.</span></span>

<span data-ttu-id="31be4-159">Al prompt dei comandi in hello `read-file-upload-notification` cartella, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="31be4-159">At a command prompt in hello `read-file-upload-notification` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="31be4-160">Al prompt dei comandi in hello `simulated-device` cartella, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="31be4-160">At a command prompt in hello `simulated-device` folder, run hello following command:</span></span>

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

<span data-ttu-id="31be4-161">cattura di schermata seguente Hello Mostra output di hello dalla hello **dispositivo simulato** app:</span><span class="sxs-lookup"><span data-stu-id="31be4-161">hello following screenshot shows hello output from hello **simulated-device** app:</span></span>

![Output dell'app simulated-device](media/iot-hub-java-java-upload/simulated-device.png)

<span data-ttu-id="31be4-163">cattura di schermata seguente Hello Mostra output di hello dalla hello **notifica caricamento di file di lettura** app:</span><span class="sxs-lookup"><span data-stu-id="31be4-163">hello following screenshot shows hello output from hello **read-file-upload-notification** app:</span></span>

![Output dell'app read-file-upload-notification](media/iot-hub-java-java-upload/read-file-upload-notification.png)

<span data-ttu-id="31be4-165">È possibile utilizzare hello tooview portale hello caricata file nel contenitore di archiviazione hello configurate:</span><span class="sxs-lookup"><span data-stu-id="31be4-165">You can use hello portal tooview hello uploaded file in hello storage container you configured:</span></span>

![File caricato](media/iot-hub-java-java-upload/uploaded-file.png)

## <a name="next-steps"></a><span data-ttu-id="31be4-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31be4-167">Next steps</span></span>

<span data-ttu-id="31be4-168">In questa esercitazione è stato descritto come file hello toouse caricare le funzionalità di IoT Hub consente di caricare file toosimplify dai dispositivi.</span><span class="sxs-lookup"><span data-stu-id="31be4-168">In this tutorial, you learned how toouse hello file upload capabilities of IoT Hub toosimplify file uploads from devices.</span></span> <span data-ttu-id="31be4-169">È possibile continuare tooexplore IoT hub funzionalità e scenari con hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="31be4-169">You can continue tooexplore IoT hub features and scenarios with hello following articles:</span></span>

* <span data-ttu-id="31be4-170">[Creare un hub IoT a livello di codice][lnk-create-hub]</span><span class="sxs-lookup"><span data-stu-id="31be4-170">[Create an IoT hub programmatically][lnk-create-hub]</span></span>
* <span data-ttu-id="31be4-171">[Introduzione tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="31be4-171">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="31be4-172">[Azure IoT SDKs][lnk-sdks] (SDK di IoT di Azure)</span><span class="sxs-lookup"><span data-stu-id="31be4-172">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="31be4-173">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="31be4-173">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="31be4-174">[Simulazione di un dispositivo con IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="31be4-174">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Images. -->

[50]: ./media/iot-hub-csharp-csharp-file-upload/run-apps1.png
[1]: ./media/iot-hub-csharp-csharp-file-upload/image-properties.png
[2]: ./media/iot-hub-csharp-csharp-file-upload/file-upload-project-csharp1.png
[3]: ./media/iot-hub-csharp-csharp-file-upload/enable-file-notifications.png

<!-- Links -->



[Centro per sviluppatori di Azure IoT]: http://www.azure.com/develop/iot

[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure Storage]:../storage/common/storage-create-storage-account.md#create-a-storage-account
[lnk-configure-upload]: iot-hub-configure-file-upload.md
[Azure IoT service SDK NuGet package]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-windows-iot-edge-simulated-device.md


