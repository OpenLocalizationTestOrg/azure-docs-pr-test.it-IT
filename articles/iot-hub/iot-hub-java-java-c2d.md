---
title: i messaggi aaaCloud al dispositivo con Azure IoT Hub (linguaggio) | Documenti Microsoft
description: "La modalità toosend cloud a dispositivo dei messaggi tooa dispositivo da un hub IoT di Azure utilizzando hello Azure IoT SDK per Java. Per modificare i messaggi di cloud a dispositivo un dispositivo simulato app tooreceive e modificare un messaggio di cloud a dispositivo hello toosend app back-end."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7f785ea8-e7c2-40c5-87ef-96525e9b9e1e
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: dobett
ms.openlocfilehash: 8721f18428c849ed9a04aa2e45c65605c3e38101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a>Inviare messaggi da cloud a dispositivo con l'hub IoT (Java)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

L'hub IoT di Azure è un servizio completamente gestito che consente di abilitare comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione. Hello [iniziare con l'IoT Hub] esercitazione viene illustrato come eseguire il provisioning di un'identità del dispositivo in essa contenuti, toocreate un hub IoT e codice di un'app dispositivo simulato che invia messaggi da dispositivo a cloud.

Questa esercitazione si basa su [iniziare con l'IoT Hub]. Illustra le operazioni seguenti:

* Dal back-end soluzione, inviare singolo dispositivo tooa messaggi da cloud a dispositivo tramite l'IoT Hub.
* Ricevere messaggi da cloud a dispositivo in un dispositivo.
* Dal back-end soluzione, richiedere la conferma di recapito (*feedback*) per i messaggi inviati tooa dispositivo dall'IoT Hub.

Sono disponibili ulteriori informazioni sui cloud a dispositivo messaggi hello [Guida per sviluppatori di IoT Hub][IoT Hub developer guide - C2D].

Alla fine di hello di questa esercitazione, si esegue due applicazioni di console Java:

* **dispositivo simulato**, una versione modificata dell'applicazione hello creato in [iniziare con l'IoT Hub], che si connette l'hub IoT tooyour e riceve messaggi da cloud a dispositivo.
* **inviare messaggi di c2d**, che invia un'app di dispositivo simulato toohello messaggio cloud a dispositivo tramite l'IoT Hub e quindi riceve la conferma di recapito.

> [!NOTE]
> L’hub IoT dispone del supporto SDK per molte piattaforme e linguaggi (inclusi C, Java e Javascript) tramite gli SDK del dispositivo IoT Azure. Per istruzioni dettagliate su come tooconnect l'esercitazione toothis dispositivo codice e in genere tooAzure IoT Hub, vedere hello [Centro per sviluppatori di Azure IoT].

toocomplete questa esercitazione, è necessario hello seguenti:

* Una versione completa di utilizzo di hello [iniziare con l'IoT Hub](iot-hub-java-java-getstarted.md) o [messaggi da dispositivo a cloud IoT Hub processo](iot-hub-java-java-process-d2c.md) esercitazione.
* versione più recente Hello [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Un account Azure attivo. Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.

## <a name="receive-messages-in-hello-simulated-device-app"></a>Ricezione di messaggi hello dispositivo simulato App

In questa sezione, si modifica hello dispositivo simulato app è stato creato in [iniziare con l'IoT Hub] tooreceive di messaggi da cloud a dispositivo dall'hub IoT hello.

1. Per aprire il file di simulated-device\src\main\java\com\mycompany\app\App.java hello, utilizzando un editor di testo.

2. Aggiungere il seguente hello **MessageCallback** classe come una classe annidata all'interno di hello **App** classe. Hello **eseguire** metodo viene richiamato quando il dispositivo hello riceve un messaggio dall'IoT Hub. In questo esempio, il dispositivo hello sempre notifica hub IoT hello completamento messaggio hello:

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. Modificare hello **principale** metodo toocreate un **AppMessageCallback** hello istanza e chiamare **setMessageCallback** metodo prima dell'apertura client hello come indicato di seguito:

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > Se si Usa HTTP invece di MQTT o AMQP come trasporto hello, hello **DeviceClient** istanza verifica la presenza di messaggi dall'IoT Hub raramente (meno di 25 minuti). Per ulteriori informazioni sulle differenze hello supporto MQTT, AMQP e HTTP e la limitazione delle richieste di Hub IoT, vedere hello [Guida per sviluppatori di IoT Hub][IoT Hub developer guide - C2D].

4. hello toobuild **dispositivo simulato** app usando Maven, eseguire hello comando al prompt dei comandi di hello nella cartella dispositivo simulato hello seguente:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a>Inviare un messaggio da cloud a dispositivo

In questa sezione si crea un'applicazione console Java che invia messaggi da cloud a dispositivo toohello dispositivo simulato app. È necessario hello ID dispositivo del dispositivo hello aggiunto nel hello [iniziare con l'IoT Hub] esercitazione. È inoltre necessario hello stringa di connessione IoT Hub per l'hub che è possibile trovare nel hello [portale di Azure].

1. Creare un progetto di Maven denominato **inviare messaggi di c2d** utilizzando hello seguente comando al prompt dei comandi. Si noti che si tratta di un lungo comando singolo:

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. Al prompt dei comandi, passare toohello nuova cartella di trasmissione-c2d-messaggi.

3. Utilizzando un editor di testo, di aprire file pom.xml hello nella cartella di trasmissione-c2d-messaggi hello e aggiungere hello seguente dipendenza toohello **dipendenze** nodo. Aggiunta della dipendenza hello consente hello toouse **client del servizio di linguaggio hub IOT** pacchetto in toocommunicate l'applicazione con il servizio di hub IoT:

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

5. Per aprire il file di send-c2d-messages\src\main\java\com\mycompany\app\App.java hello, utilizzando un editor di testo.

6. Aggiungere il seguente hello **importare** file toohello istruzioni:

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. Aggiungere hello seguenti variabili a livello di classe toohello **App** classe, sostituendo **{yourhubconnectionstring}** e **{yourdeviceid}** con hello i valori del tipo indicato in precedenza:

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. Sostituire hello **principale** metodo con hello seguente codice. Questo codice si connette l'hub IoT tooyour, invia un dispositivo tooyour messaggio e quindi attende un acknowledgement messaggio hello dispositivo hello ricevuti ed elaborati:
   
    ```java
    public static void main(String[] args) throws IOException,
        URISyntaxException, Exception {
      ServiceClient serviceClient = ServiceClient.createFromConnectionString(
        connectionString, protocol);
   
      if (serviceClient != null) {
        serviceClient.open();
        FeedbackReceiver feedbackReceiver = serviceClient
          .getFeedbackReceiver();
        if (feedbackReceiver != null) feedbackReceiver.open();
   
        Message messageToSend = new Message("Cloud toodevice message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent toodevice");
   
        FeedbackBatch feedbackBatch = feedbackReceiver.receive(10000);
        if (feedbackBatch != null) {
          System.out.println("Message feedback received, feedback time: "
            + feedbackBatch.getEnqueuedTimeUtc().toString());
        }
   
        if (feedbackReceiver != null) feedbackReceiver.close();
        serviceClient.close();
      }
    }
    ```

    > [!NOTE]
    > Per semplicità, in questa esercitazione non si implementa alcun criterio di nuovi tentativi. Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei].


9. hello toobuild **dispositivo simulato** app usando Maven, eseguire hello comando al prompt dei comandi di hello nella cartella dispositivo simulato hello seguente:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a>Eseguire applicazioni hello

Si è ora applicazioni hello toorun pronto.

1. Al prompt dei comandi nella cartella dispositivo simulato hello eseguire hello dopo l'invio di hub IoT di telemetria tooyour e toolisten per i messaggi da cloud a dispositivo inviati dall'hub di toobegin di comando:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Eseguire app dispositivo simulato hello][img-simulated-device]

2. Al prompt dei comandi nella cartella di trasmissione-c2d-messaggi hello eseguire hello successivo comando toosend un messaggio di cloud a dispositivo e l'attesa per un riconoscimento di commenti e suggerimenti:

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Eseguire il messaggio da cloud a dispositivo hello di hello comando toosend][img-send-command]

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, si è appreso come toosend e ricevere messaggi da cloud a dispositivo. 

esempi di toosee di soluzioni end-to-end completate che usa IoT Hub, vedere [Azure IoT Suite].

toolearn più sullo sviluppo di soluzioni con l'IoT Hub, vedere hello [Guida per sviluppatori di IoT Hub].

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

[iniziare con l'IoT Hub]: iot-hub-java-java-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[Guida per sviluppatori di IoT Hub]: iot-hub-devguide.md
[Centro per sviluppatori di Azure IoT]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
[gestione degli errori temporanei]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[portale di Azure]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22