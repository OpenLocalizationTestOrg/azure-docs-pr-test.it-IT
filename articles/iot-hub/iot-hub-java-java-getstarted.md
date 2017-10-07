---
title: aaaGet avviato con l'IoT Hub Azure (linguaggio) | Documenti Microsoft
description: Informazioni su come toosend dispositivo a cloud messaggi tooAzure IoT Hub tramite IoT SDK per Java. Creare dispositivo simulato e servizio App tooregister il dispositivo, inviare messaggi e leggere messaggi da hub IoT.
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 70dae4a8-0e98-4c53-b5a5-9d6963abb245
ms.service: iot-hub
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac954f0522b46ed2a5b4a819bc611c13be0b9a9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a>Connessione hub IoT tooyour dispositivo utilizzando Java
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Alla fine di hello di questa esercitazione, si dispongono di tre applicazioni di console Java:

* **identità dispositivo creare**, che consente di creare un'identità del dispositivo e protezione della chiave tooconnect l'app del dispositivo.
* **i messaggi di d2c lettura**, che consente di visualizzare dati di telemetria hello inviati per l'app del dispositivo.
* **dispositivo simulato**, che collega l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza e invia un messaggio di dati di telemetria ogni secondo utilizzando hello protocollo MQTT.

> [!NOTE]
> articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] vengono fornite informazioni hello Azure IoT SDK che è possibile utilizzare toobuild toorun entrambe le app nei dispositivi e la soluzione di back-end.

toocomplete questa esercitazione, è necessario hello seguenti:

* versione più recente Hello [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) 
* [Maven 3](https://maven.apache.org/install.html) 
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

Come passaggio finale, prendere nota di hello **chiave primaria** valore. Quindi fare clic su **endpoint** hello e **eventi** endpoint predefinito. In hello **proprietà** pannello, prendere nota dei hello **nome compatibile con Hub eventi** hello e **endpoint compatibile con Hub eventi** indirizzo. Questi tre valori sono necessari quando si crea l'app **read-d2c-messages**.

![Pannello Messaggistica dell'hub IoT nel portale di Azure][6]

L'hub IoT è stato creato. È necessario hello nome host dell'IoT Hub, la stringa di connessione IoT Hub, chiave primaria di IoT Hub, nome compatibile con Hub eventi ed endpoint compatibile con Hub eventi è necessario toocomplete in questa esercitazione.

## <a name="create-a-device-identity"></a>Creare un'identità del dispositivo
In questa sezione si crea un'applicazione console Java che crea un'identità del dispositivo nel Registro di sistema di hello identità nell'hub IoT. Un dispositivo non può connettersi tooIoT hub, a meno che non sia presente una voce nel Registro di sistema di hello identità. Per ulteriori informazioni, vedere hello **Registro di sistema di identità** sezione di hello [Guida per sviluppatori di IoT Hub][lnk-devguide-identity]. Quando si esegue questa app console, viene generato un ID univoco del dispositivo e chiave che il dispositivo può usare tooidentify stesso quando vengono inviati al dispositivo a cloud messaggi tooIoT Hub.

1. Creare una cartella vuota denominata iot-java-get-started. Nella cartella iot java-get avviato hello, creare un progetto di Maven denominato **identità dispositivo creare** utilizzando hello seguente comando al prompt dei comandi. Si noti che si tratta di un lungo comando singolo:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Al prompt dei comandi, passare cartella identità dispositivo creare toohello.

3. Utilizzando un editor di testo, di aprire file pom.xml hello nella cartella identità dispositivo creare hello e aggiungere hello seguente dipendenza toohello **dipendenze** nodo. Questa dipendenza consente si toouse hello client di servizi iot pacchetto dell'App:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > È possibile verificare la versione più recente di hello di **client di servizi iot** utilizzando [ricerca Maven][lnk-maven-service-search].

4. Salvare e chiudere il file di pom.xml hello.

5. Per aprire il file di create-device-identity\src\main\java\com\mycompany\app\App.java hello, utilizzando un editor di testo.

6. Aggiungere il seguente hello **importare** file toohello istruzioni:

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. Aggiungere hello seguenti variabili a livello di classe toohello **App** classe, sostituendo **{yourhubconnectionstring}** con hello valore l'indicato in precedenza:

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. Modificare la firma hello di hello **principale** tooinclude metodo hello eccezioni, come indicato di seguito:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. Aggiungere hello seguente di codice come corpo hello di hello **principale** metodo. Questo codice crea un dispositivo denominato *javadevice* nel registro delle identità dell'hub IoT, se non esiste già. Viene quindi visualizzato hello dispositivo ID e la chiave che è necessario in un secondo momento:

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    ```

10. Salvare e chiudere il file di App.java hello.

11. hello toobuild **identità dispositivo creare** app usando Maven, eseguire hello comando al prompt dei comandi di hello nella cartella identità dispositivo creare hello seguente:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. hello toorun **identità dispositivo creare** app usando Maven, eseguire hello comando al prompt dei comandi di hello nella cartella identità dispositivo creare hello seguente:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. Prendere nota di hello **ID dispositivo** e **chiave dispositivo**. Questi valori è necessario in un secondo momento quando si crea un'app che si connette tooIoT Hub come un dispositivo.

> [!NOTE]
> Hello del Registro di sistema di IoT Hub identità archivia solo hub IoT toohello di dispositivo identità tooenable proteggere l'accesso. Archivia toouse di chiavi e l'ID dispositivo come credenziali di sicurezza e un flag di abilitazione/disabilitazione che è possibile utilizzare toodisable accesso per un singolo dispositivo. Se l'app deve toostore altri metadati specifici del dispositivo, deve utilizzare un negozio specifico dell'applicazione. Per ulteriori informazioni, vedere hello [Guida per sviluppatori di IoT Hub][lnk-devguide-identity].

## <a name="receive-device-to-cloud-messages"></a>Ricezione di messaggi da dispositivo a cloud

In questa sezione si crea un'app console di Java che legge i messaggi da dispositivo a cloud dall'hub IoT. Un hub IoT espone un [Hub eventi][lnk-event-hubs-overview]-tooenable endpoint compatibile per i messaggi da dispositivo a cloud tooread. cose tookeep semplice, in questa esercitazione consente di creare un lettore di base che non è adatto per una distribuzione di velocità effettiva elevata. Hello [elaborare i messaggi da dispositivo a cloud] [ lnk-process-d2c-tutorial] esercitazione viene illustrato come tooprocess dispositivo a cloud messaggi su larga scala. Hello [Introduzione agli hub di eventi] [ lnk-eventhubs-tutorial] esercitazione fornisce ulteriori informazioni su come tooprocess messaggi dagli hub eventi ed è applicabile toohello gli endpoint Hub IoT Hub eventi compatibile.

> [!NOTE]
> Hello Hub eventi compatibile con l'endpoint per la lettura dei messaggi da dispositivo a cloud sempre Usa protocollo AMQP hello.

1. Nella cartella iot java-get avviato hello è stato creato in hello *creare un'identità del dispositivo* sezione, creare un progetto di Maven denominato **d2c-i-messaggi** utilizzando hello seguente comando al prompt dei comandi. Si noti che si tratta di un lungo comando singolo:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Al prompt dei comandi, passare toohello cartella di lettura-d2c-messaggi.

3. Utilizzando un editor di testo, di aprire file pom.xml hello nella cartella di lettura-d2c-messaggi hello e aggiungere hello seguente dipendenza toohello **dipendenze** nodo. Questa dipendenza consente di pacchetto di eventhubs client toouse hello in tooread l'app dall'endpoint compatibile con Hub eventi hello:

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. Salvare e chiudere il file di pom.xml hello.

5. Per aprire il file di read-d2c-messages\src\main\java\com\mycompany\app\App.java hello, utilizzando un editor di testo.

6. Aggiungere il seguente hello **importare** file toohello istruzioni:

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. Aggiungere hello seguenti a livello di classe variabile toohello **App** classe. Sostituire **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, e **{youreventhubcompatiblename}** con i valori hello è indicato in precedenza:

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. Aggiungere il seguente hello **receiveMessages** metodo toohello **App** classe. Questo metodo crea un **EventHubClient** tooconnect toohello compatibile con Hub eventi endpoint dell'istanza e quindi crea in modo asincrono un **PartitionReceiver** tooread istanza da un Hub eventi partizione. Eseguito un ciclo in modo continuo e stampa dettagli messaggio hello finché non termina l'applicazione hello.

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed toocreate client: " + e.getMessage());
        System.exit(1);
      }
      try {
        // Create a receiver using the
        // default Event Hubs consumer group
        // that listens for messages from now on.
        client.createReceiver(EventHubClient.DEFAULT_CONSUMER_GROUP_NAME, partitionId, Instant.now())
          .thenAccept(new Consumer<PartitionReceiver>() {
            public void accept(PartitionReceiver receiver) {
              System.out.println("** Created receiver on partition " + partitionId);
              try {
                while (true) {
                  Iterable<EventData> receivedEvents = receiver.receive(100).get();
                  int batchSize = 0;
                  if (receivedEvents != null) {
                    System.out.println("Got some evenst");
                    for (EventData receivedEvent : receivedEvents) {
                      System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s",
                        receivedEvent.getSystemProperties().getOffset(),
                        receivedEvent.getSystemProperties().getSequenceNumber(),
                        receivedEvent.getSystemProperties().getEnqueuedTime()));
                      System.out.println(String.format("| Device ID: %s",
                        receivedEvent.getSystemProperties().get("iothub-connection-device-id")));
                      System.out.println(String.format("| Message Payload: %s",
                        new String(receivedEvent.getBytes(), Charset.defaultCharset())));
                      batchSize++;
                    }
                  }
                  System.out.println(String.format("Partition: %s, ReceivedBatch Size: %s", partitionId, batchSize));
                }
              } catch (Exception e) {
                System.out.println("Failed tooreceive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed toocreate receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > Questo metodo utilizza un filtro durante la creazione di ricevitore hello in modo che hello ricevitore legge solo i messaggi inviati tooIoT Hub dopo ricevitore hello viene avviata l'esecuzione. Questa tecnica è utile in un ambiente di test in modo da visualizzare il set corrente di hello dei messaggi. In un ambiente di produzione, il codice deve verificare che vengano elaborati tutti i messaggi hello - per ulteriori informazioni, vedere hello [come i messaggi da dispositivo a cloud IoT Hub tooprocess] [ lnk-process-d2c-tutorial] esercitazione.

9. Modificare la firma hello di hello **principale** tooinclude metodo hello eccezione, come indicato di seguito:

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. Aggiungere i seguenti toohello codice hello **principale** metodo hello **App** classe. Questo codice crea due hello **EventHubClient** e **PartitionReceiver** istanze e consente app hello tooclose è terminata l'elaborazione dei messaggi:

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    try {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    } catch (ServiceBusException sbe) {
      System.exit(1);
    }
    ```

    > [!NOTE]
    > Questo codice presuppone che l'hub IoT creato nel livello di hello F1 (gratuito). Un hub IoT gratuito ha due partizioni denominate "0" e "1".

11. Salvare e chiudere il file di App.java hello.

12. hello toobuild **d2c-i-messaggi** app usando Maven, eseguire hello comando al prompt dei comandi di hello nella cartella di lettura-d2c-messaggi hello seguente:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a>Creare un'app per dispositivi
In questa sezione si crea un'applicazione console Java che simula un dispositivo che invia l'hub IoT tooan messaggi da dispositivo a cloud.

1. Nella cartella iot java-get avviato hello è stato creato in hello *creare un'identità del dispositivo* sezione, creare un progetto di Maven denominato **dispositivo simulato** utilizzando hello seguente comando al prompt dei comandi. Si noti che si tratta di un lungo comando singolo:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Al prompt dei comandi, passare cartella dispositivo simulato toohello.

3. Utilizzando un editor di testo, di aprire file pom.xml hello nella cartella dispositivo simulato hello e aggiungere hello seguente dipendenze toohello **dipendenze** nodo. Questa dipendenza consente si toouse hello client con l'hub IOT-java pacchetto in toocommunicate l'app con l'hub IoT e tooserialize tooJSON oggetti Java:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.3.1</version>
    </dependency>
    ```

    > [!NOTE]
    > È possibile verificare la versione più recente di hello di **client di dispositivi iot** utilizzando [ricerca Maven][lnk-maven-device-search].

4. Salvare e chiudere il file di pom.xml hello.

5. Per aprire il file di simulated-device\src\main\java\com\mycompany\app\App.java hello, utilizzando un editor di testo.

6. Aggiungere il seguente hello **importare** file toohello istruzioni:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. Aggiungere hello seguenti variabili a livello di classe toohello **App** classe. Sostituzione di **{youriothubname}** con il nome di hub IoT, e **{yourdevicekey}** con il valore della chiave di hello dispositivo è stato generato in hello *creare un'identità del dispositivo* sezione:

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    Questa app di esempio utilizza hello **protocollo** variabile quando si crea un'istanza di un **DeviceClient** oggetto. È possibile utilizzare entrambi toocommunicate protocollo hello MQTT, AMQP o HTTP con l'IoT Hub.

8. Aggiungere il seguente hello annidato **TelemetryDataPoint** classe all'interno di hello **App** classe dati di telemetria hello toospecify il dispositivo invia tooyour IoT hub:

    ```java
    private static class TelemetryDataPoint {
      public String deviceId;
      public double temperature;
      public double humidity;
   
      public String serialize() {
        Gson gson = new Gson();
        return gson.toJson(this);
      }
    }
    ```
9. Aggiungere il seguente hello annidato **EventCallback** classe all'interno di hello **App** classe toodisplay hello acknowledgement stato hello hub IoT restituisce quando elabora un messaggio hello app del dispositivo. Questo metodo notifica thread principale di hello in app hello è stato elaborato il messaggio hello:
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toomessage with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. Aggiungere il seguente hello annidato **MessageSender** classe all'interno di hello **App** classe. Hello **eseguire** metodo in questa classe genera l'errore hub IoT di esempio telemetria dati toosend tooyour e attende un acknowledgement prima di inviare il messaggio successivo hello:

    ```java
    private static class MessageSender implements Runnable {
      public void run()  {
        try {
          double minTemperature = 20;
          double minHumidity = 60;
          Random rand = new Random();
    
          while (true) {
            double currentTemperature = minTemperature + rand.nextDouble() * 15;
            double currentHumidity = minHumidity + rand.nextDouble() * 20;
            TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
            telemetryDataPoint.deviceId = deviceId;
            telemetryDataPoint.temperature = currentTemperature;
            telemetryDataPoint.humidity = currentHumidity;
    
            String msgStr = telemetryDataPoint.serialize();
            Message msg = new Message(msgStr);
            msg.setProperty("temperatureAlert", (currentTemperature > 30) ? "true" : "false");
            msg.setMessageId(java.util.UUID.randomUUID().toString()); 
            System.out.println("Sending: " + msgStr);
    
            Object lockobj = new Object();
            EventCallback callback = new EventCallback();
            client.sendEventAsync(msg, callback, lockobj);
    
            synchronized (lockobj) {
              lockobj.wait();
            }
            Thread.sleep(1000);
          }
        } catch (InterruptedException e) {
          System.out.println("Finished.");
        }
      }
    }
    ```

    Questo metodo invia un nuovo messaggio di dispositivo a cloud a un secondo dopo l'hub IoT hello invia un acknowledgement messaggio hello del precedente. messaggio Hello contiene un oggetto serializzato JSON con deviceId hello e generato in modo casuale di numeri toosimulate un sensore di temperatura e un sensore umidità.

11. Sostituire hello **principale** metodo con hello dopo il codice che crea un hub IoT tooyour di thread toosend messaggi da dispositivo a cloud:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER tooexit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. Salvare e chiudere il file di App.java hello.

13. hello toobuild **dispositivo simulato** app usando Maven, eseguire hello comando al prompt dei comandi di hello nella cartella dispositivo simulato hello seguente:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo. Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].

## <a name="run-hello-apps"></a>Eseguire App hello

Si è ora pronto toorun hello app.

1. Al prompt dei comandi nella cartella di lettura d2c hello eseguire hello successivo comando toobegin monitoraggio prima partizione nell'hub IoT di hello:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Messaggi da dispositivo a cloud toomonitor dell'IoT Hub Java servizio app][7]

2. Al prompt dei comandi nella cartella dispositivo simulato hello eseguire hello toobegin comando invio hub IoT tooyour dati di telemetria seguenti:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Messaggi da dispositivo a cloud dell'IoT Hub Java dispositivo app toosend][8]

3. Hello **utilizzo** riquadro in hello [portale di Azure] [ lnk-portal] Mostra hello numero di messaggi inviati toohello hub IoT:

    ![Azure portale utilizzo riquadro mostra il numero di messaggi inviati tooIoT Hub][43]

## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità. È stato utilizzato questo dispositivo identità tooenable hello dispositivo app toosend messaggi da dispositivo a cloud toohello hub IoT. È stato creato anche un'applicazione che consente di visualizzare i messaggi hello ricevuti dall'hub IoT hello.

Guida introduttiva toocontinue con IoT Hub e tooexplore altri scenari IoT, vedere:

* [Connessione del dispositivo][lnk-connect-device]
* [Introduzione alla gestione dei dispositivi][lnk-device-management]
* [Introduzione ad Azure IoT Edge][lnk-iot-edge]

toolearn tooextend vedere i messaggi di dispositivo a cloud processo e di soluzione IoT su larga scala, hello [elaborare i messaggi da dispositivo a cloud] [ lnk-process-d2c-tutorial] esercitazione.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[6]: ./media/iot-hub-java-java-getstarted/create-iot-hub6.png
[7]: ./media/iot-hub-java-java-getstarted/runapp1.png
[8]: ./media/iot-hub-java-java-getstarted/runapp2.png
[43]: ./media/iot-hub-java-java-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-eventhubs-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22
