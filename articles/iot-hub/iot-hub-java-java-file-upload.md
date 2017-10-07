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
# <a name="upload-files-from-your-device-toohello-cloud-with-iot-hub"></a>Caricare file dal cloud toohello dispositivo con l'IoT Hub

[!INCLUDE [iot-hub-file-upload-language-selector](../../includes/iot-hub-file-upload-language-selector.md)]

Questa esercitazione si basa su codice hello in hello [inviare messaggi da Cloud a dispositivo con l'IoT Hub](iot-hub-java-java-c2d.md) tooshow esercitazione si come hello toouse [file di funzionalità di caricamento dell'IoT Hub](iot-hub-devguide-file-upload.md) tooupload un file troppo[ Archiviazione blob di Azure](../storage/index.md). Hello esercitazione vengono illustrate le modalità per:

- Specificare in modo sicuro un dispositivo con un URI del BLOB di Azure per il caricamento di un file.
- Utilizzare l'elaborazione di tootrigger notifiche di IoT Hub file caricamento del file hello nel back-end app hello.

Hello [iniziare con l'IoT Hub](iot-hub-java-java-getstarted.md) e [inviare messaggi da Cloud a dispositivo con l'IoT Hub](iot-hub-java-java-c2d.md) le esercitazioni illustrano hello da dispositivo a cloud e cloud a dispositivo messaggistica funzionalità di base di IoT Hub. Hello [i messaggi di processo da dispositivo a Cloud](iot-hub-java-java-process-d2c.md) esercitazione viene descritto un modo tooreliably memorizza da dispositivo a cloud messaggi nel servizio di archiviazione blob di Azure. Tuttavia, in alcuni scenari è possibile mappare facilmente dati hello che i dispositivi di trasmissione in messaggi da dispositivo a cloud relativamente piccolo hello che accetta l'IoT Hub. ad esempio:

* File di grandi dimensioni che contengono immagini
* Video
* Dati di vibrazione campionati ad alta frequenza
* Qualche tipo di dati pre-elaborati.

Questi file sono in genere batch elaborato nel cloud hello tramite strumenti come [Data Factory di Azure](../data-factory/index.md) o hello [Hadoop](../hdinsight/index.md) dello stack. Quando è necessario tooupland file da un dispositivo, è possibile utilizzare ancora hello protezione e affidabilità dell'IoT Hub.

Alla fine di hello di questa esercitazione è eseguire due applicazioni di console Java:

* **dispositivo simulato**, una versione modificata dell'applicazione hello creato nell'esercitazione hello [messaggi trasmissione Cloud a dispositivo con l'IoT Hub]. Questa app carica toostorage un file utilizzando un URI SAS forniti per l'hub IoT.
* **read-file-upload-notification**, che riceve le notifiche di caricamento file dall'hub IoT.

> [!NOTE]
> L'hub IoT supporta numerose piattaforme e linguaggi (inclusi C, .NET e Javascript) tramite gli Azure IoT SDK per dispositivi. Fare riferimento toohello [Centro per sviluppatori di Azure IoT] per istruzioni dettagliate su come tooconnect il tooAzure dispositivo IoT Hub.

toocomplete questa esercitazione, è necessario hello seguenti:

* versione più recente Hello [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Un account Azure attivo. Se non si ha un account, è possibile crearne uno [gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.

[!INCLUDE [iot-hub-associate-storage](../../includes/iot-hub-associate-storage.md)]

## <a name="upload-a-file-from-a-device-app"></a>Caricare un file da un'app per dispositivi

In questa sezione, si modifica hello app del dispositivo è stato creato in [inviare messaggi da Cloud a dispositivo con l'IoT Hub](iot-hub-java-java-c2d.md) tooupload un hub di tooIoT file.

1. Copiare un toohello di file di immagine `simulated-device` cartella e rinominarlo `myimage.png`.

1. Utilizzando un editor di testo, aprire hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.

1. Aggiungere hello dichiarazione di variabile toohello **App** classe:

    ```java
    private static String fileName = "myimage.png";
    ```

1. tooprocess callback messaggi di stato di caricamento del file, aggiungere il seguente hello annidati classe toohello **App** classe:

    ```java
    // Define a callback method tooprint status codes from IoT Hub.
    protected static class FileUploadStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toofile upload for " + fileName
            + " operation with status " + status.name());
      }
    }
    ```

1. tooupload immagini tooIoT Hub, aggiungere hello seguente metodo toohello **App** tooupload classe immagini tooIoT Hub:

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

1. Modificare hello **principale** hello toocall metodo **uploadFile** metodo come illustrato nel seguente frammento di codice hello:

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

1. Comando che segue di hello utilizzare hello toobuild **dispositivo simulato** app e controllare gli errori:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="receive-a-file-upload-notification"></a>Ricevere la notifica di caricamento di un file

In questa sezione viene creata un'app console Java che riceve messaggi di notifica di caricamento file dall'hub IoT.

È necessario hello **iothubowner** stringa di connessione per l'IoT Hub di toocomplete in questa sezione. È possibile trovare la stringa di connessione hello in hello [portale di Azure](https://portal.azure.com/) su hello **i criteri di accesso condiviso** blade.

1. Creare un progetto di Maven denominato **notifica caricamento di file di lettura** utilizzando hello seguente comando al prompt dei comandi. Si noti che si tratta di un lungo comando singolo:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-file-upload-notification -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

1. Al prompt dei comandi, passare toohello nuova `read-file-upload-notification` cartella.

1. Utilizzando un editor di testo, aprire hello `pom.xml` file hello `read-file-upload-notification` cartella e aggiungere hello seguente dipendenza toohello **dipendenze** nodo. Aggiunta della dipendenza hello consente hello toouse **client del servizio di linguaggio hub IOT** pacchetto in toocommunicate l'applicazione con il servizio di hub IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > È possibile verificare la versione più recente di hello di **client di servizi iot** utilizzando [ricerca Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

1. Salvare e chiudere hello `pom.xml` file.

1. Utilizzando un editor di testo, aprire hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.

1. Aggiungere il seguente hello **importare** file toohello istruzioni:

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.concurrent.ExecutorService;
    import java.util.concurrent.Executors;
    ```

1. Aggiungere hello seguenti variabili a livello di classe toohello **App** classe:

    ```java
    private static final String connectionString = "{Your IoT Hub connection string}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    private static FileUploadNotificationReceiver fileUploadNotificationReceiver = null;
    ```

1. tooprint informazioni console toohello caricamento del file hello, aggiungere il seguente hello annidati classe toohello **App** classe:

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

1. thread hello toostart in attesa di notifiche di caricamento di file, aggiungere hello seguente codice toohello **principale** metodo:

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

1. Salvare e chiudere hello `read-file-upload-notification\src\main\java\com\mycompany\app\App.java` file.

1. Comando che segue di hello utilizzare hello toobuild **notifica caricamento di file di lettura** app e controllare gli errori:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Eseguire applicazioni hello

Si è ora applicazioni hello toorun pronto.

Al prompt dei comandi in hello `read-file-upload-notification` cartella, eseguire hello comando seguente:

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

Al prompt dei comandi in hello `simulated-device` cartella, eseguire hello comando seguente:

```cmd/sh
mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
```

cattura di schermata seguente Hello Mostra output di hello dalla hello **dispositivo simulato** app:

![Output dell'app simulated-device](media/iot-hub-java-java-upload/simulated-device.png)

cattura di schermata seguente Hello Mostra output di hello dalla hello **notifica caricamento di file di lettura** app:

![Output dell'app read-file-upload-notification](media/iot-hub-java-java-upload/read-file-upload-notification.png)

È possibile utilizzare hello tooview portale hello caricata file nel contenitore di archiviazione hello configurate:

![File caricato](media/iot-hub-java-java-upload/uploaded-file.png)

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


