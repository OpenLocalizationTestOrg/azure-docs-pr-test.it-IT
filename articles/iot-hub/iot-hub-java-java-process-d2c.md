---
title: i messaggi da dispositivo a cloud Azure IoT Hub (linguaggio) aaaProcess | Documenti Microsoft
description: Come i messaggi da dispositivo a cloud IoT Hub utilizzando le regole di routing e gli endpoint personalizzati toodispatch tooprocess messaggi tooother servizi di back-end.
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: bd9af5f9-a740-4780-a2a6-8c0e2752cf48
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.openlocfilehash: 084e84e721ca4297c4d7d6cb06a43b0bed9bce85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a>Elaborare messaggi da dispositivo a cloud dell'hub IoT (Java)

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

L'hub IoT di Azure è un servizio completamente gestito che consente comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione. Altre esercitazioni ([iniziare con l'IoT Hub] e [inviare messaggi da cloud a dispositivo con l'IoT Hub][lnk-c2d]) viene illustrato come toouse hello base dispositivo a cloud e cloud a dispositivo funzionalità di messaggistica di IoT Hub.

In questa esercitazione si basa sul codice hello di hello [iniziare con l'IoT Hub] esercitazione e Mostra come toouse messaggio routing dei messaggi da dispositivo a cloud tooprocess in modo scalabile. esercitazione Hello viene illustrato come tooprocess messaggi che richiedono un intervento immediato dalla soluzione hello back-end. Ad esempio, un dispositivo potrebbe inviare un messaggio di avviso che attiva l'inserimento di un ticket in un sistema CRM. Al contrario, i messaggi di punto dati vengono semplicemente inseriti in un motore di analisi. Telemetria temperatura da un dispositivo che è toobe archiviati per poterli analizzare in seguito è ad esempio, un messaggio di punto dati.

Alla fine di hello di questa esercitazione, si esegue tre applicazioni di console Java:

* **dispositivo simulato**, una versione modificata dell'applicazione hello creato in hello [iniziare con l'IoT Hub] esercitazione, invia i messaggi da dispositivo a cloud punto dati ogni secondo e messaggi di dispositivo a cloud interattivo ogni 10 secondi. Questa app utilizza hello AMQP protocollo toocommunicate con l'IoT Hub.
* **i messaggi di d2c lettura** Visualizza dati di telemetria hello inviati per l'app del dispositivo.
* **lettura coda critico** coda i messaggi critici hello da hello Bus di servizio collegata coda toohello hub IoT.

> [!NOTE]
> L'hub IoT offre il supporto SDK per molte piattaforme e linguaggi, inclusi C, Java e JavaScript. Per istruzioni su come tooreplace hello dispositivo in questa esercitazione con un dispositivo fisico, e tooconnect dispositivi tooan IoT Hub, vedere hello [Centro per sviluppatori di Azure IoT].

toocomplete questa esercitazione, è necessario hello seguenti:

* Una versione completa di utilizzo di hello [iniziare con l'IoT Hub] esercitazione.
* versione più recente Hello [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Un account Azure attivo. Se non si dispone di un account, è possibile creare un [account di valutazione gratuita] in pochi minuti.

È necessaria una conoscenza di base di [Archiviazione di Azure] e del [bus di servizio di Azure].

## <a name="send-interactive-messages-from-a-device-app"></a>Inviare messaggi interattivi da un'app per dispositivi
In questa sezione, si modifica hello app del dispositivo è stato creato in hello [iniziare con l'IoT Hub] toooccasionally esercitazione inviare i messaggi che richiedono l'elaborazione immediata.

1. Utilizzare un file di testo dell'editor tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java. Questo file contiene codice hello hello **dispositivo simulato** app è stato creato in hello [iniziare con l'IoT Hub] esercitazione.

2. Sostituire hello **MessageSender** classe con hello seguente codice:

    ```java
    private static class MessageSender implements Runnable {

        public void run()  {
            try {
                double minTemperature = 20;
                double minHumidity = 60;
                Random rand = new Random();

                while (true) {
                    String msgStr;
                    Message msg;
                    if (new Random().nextDouble() > 0.7) {
                        msgStr = "This is a critical message.";
                        msg = new Message(msgStr);
                        msg.setProperty("level", "critical");
                    } else {
                        double currentTemperature = minTemperature + rand.nextDouble() * 15;
                        double currentHumidity = minHumidity + rand.nextDouble() * 20; 
                        TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
                        telemetryDataPoint.deviceId = deviceId;
                        telemetryDataPoint.temperature = currentTemperature;
                        telemetryDataPoint.humidity = currentHumidity;

                        msgStr = telemetryDataPoint.serialize();
                        msg = new Message(msgStr);
                    }
                    
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
   
    Questo metodo aggiunge in modo casuale proprietà hello `"level": "critical"` toomessages inviato dal dispositivo hello, che simula un messaggio che richiede un intervento immediato per hello applicazione back-end. un'applicazione Hello passa le informazioni nelle proprietà di messaggio hello, anziché nel corpo del messaggio hello, in modo che l'IoT Hub può instradare destinazione dei messaggi appropriata toohello messaggio hello.
   
   > [!NOTE]
   > È possibile utilizzare i messaggi tooroute di proprietà di messaggio per vari scenari, tra cui freddo-path, l'elaborazione, inoltre toohello percorso ricorrente riportato di seguito viene illustrato di seguito.

2. Salvare e chiudere il file di simulated-device\src\main\java\com\mycompany\app\App.java hello.

    > [!NOTE]
    > Per i migliori risultati hello di semplicità, in questa esercitazione non implementa alcun criterio di tentativo. Nel codice di produzione, è necessario implementare un criterio di ripetizione, ad esempio backoff esponenziale, come indicato nell'articolo MSDN hello [gestione degli errori temporanei].

3. hello toobuild **dispositivo simulato** app usando Maven, eseguire hello comando al prompt dei comandi di hello nella cartella dispositivo simulato hello seguente:

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a>Aggiungere una coda tooyour IoT hub e instradare i messaggi tooit

In questa sezione, creare una coda di Service Bus, connetterlo hub IoT tooyour e configurare la coda IoT hub toosend messaggi toohello in base hello presenza di una proprietà nel messaggio hello. Per ulteriori informazioni su come tooprocess messaggi dalle code del Bus di servizio, vedere [iniziare con le code][lnk-sb-queues-java].

1. Creare una coda del bus di servizio, come descritto in [Get started with queues][lnk-sb-queues-java] (Introduzione alle code). Prendere nota del nome dello spazio dei nomi e di Accodamento di hello.

2. In hello portale di Azure, aprire l'hub IoT e fare clic su **endpoint**.

    ![Endpoint in hub IoT][30]

3. In hello **endpoint** pannello, fare clic su **Aggiungi** in hello tooadd superiore dell'hub IoT tooyour di coda. Endpoint hello nome **CriticalQueue** e utilizzare hello elenchi a discesa tooselect **coda di Service Bus**hello dello spazio dei nomi Service Bus in cui risiede la coda e nome della coda di hello. Al termine, fare clic su **salvare** nella parte inferiore di hello.

    ![Aggiunta di un endpoint][31]

4. Fare clic su **Route** nell'hub IoT. Fare clic su **Aggiungi** nella parte superiore di hello di hello pannello toocreate una regola di routing che instrada i messaggi toohello coda è appena aggiunto. Selezionare **DeviceTelemetry** come origine dati hello. Immettere `level="critical"` come condizione hello e scegliere coda hello appena aggiunto come un endpoint personalizzato come hello endpoint regola di routing. Al termine, fare clic su **salvare** nella parte inferiore di hello.

    ![Aggiunta di un route][32]

    Assicurarsi di route fallback hello è troppo**ON**. Questa impostazione è una configurazione predefinita di hello di un hub IoT.

    ![Route di fallback][33]

## <a name="optional-read-from-hello-queue-endpoint"></a>(Facoltativo) Lettura dall'endpoint di coda hello

Facoltativamente, è possibile leggere i messaggi hello dall'endpoint di coda hello seguendo le istruzioni hello [iniziare con le code][lnk-sb-queues-java]. Nome hello app **lettura coda critico**.

## <a name="run-hello-applications"></a>Eseguire applicazioni hello

Si è ora pronto toorun hello e tre le applicazioni.

1. hello toorun **d2c-i-messaggi** applicazione, in un prompt dei comandi della shell passare toohello lettura d2c cartella ed eseguire hello comando seguente:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Eseguire read-d2c-messages][readd2c]

2. hello toorun **lettura coda critico** applicazione, in un prompt dei comandi della shell esplorazione delle cartelle di lettura coda critico toohello ed esecuzione hello comando seguente:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Eseguire read-critical-queue][readqueue]

3. hello toorun **dispositivo simulato** app, in un prompt dei comandi della shell passare cartella dispositivo simulato toohello ed eseguire hello comando seguente:

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Eseguire simulated-device][simulateddevice]

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione è stato descritto come tooreliably inviare i messaggi da dispositivo a cloud tramite funzionalità di routing messaggi hello dell'IoT Hub.

Hello [come toosend cloud a dispositivo messaggi con l'IoT Hub] [ lnk-c2d] viene illustrato come toosend messaggi dispositivi tooyour la soluzione di back-end.

esempi di toosee di soluzioni end-to-end completate che usa IoT Hub, vedere [Azure IoT Suite][lnk-suite].

toolearn più sullo sviluppo di soluzioni con l'IoT Hub, vedere hello [Guida per sviluppatori di IoT Hub].

toolearn informazioni su routing dei messaggi nell'IoT Hub, vedere [inviare e ricevere messaggi con l'IoT Hub][lnk-devguide-messaging].

<!-- Images. -->
<!-- TODO: UPDATE PICTURES -->
[simulateddevice]: ./media/iot-hub-java-java-process-d2c/runsimulateddevice.png
[readd2c]: ./media/iot-hub-java-java-process-d2c/runprocessinteractive.png
[readqueue]: ./media/iot-hub-java-java-process-d2c/runprocessd2c.png

[30]: ./media/iot-hub-java-java-process-d2c/click-endpoints.png
[31]: ./media/iot-hub-java-java-process-d2c/endpoint-creation.png
[32]: ./media/iot-hub-java-java-process-d2c/route-creation.png
[33]: ./media/iot-hub-java-java-process-d2c/fallback-route.png

<!-- Links -->

[lnk-sb-queues-java]: ../service-bus-messaging/service-bus-java-how-to-use-queues.md

[Archiviazione di Azure]: https://azure.microsoft.com/documentation/services/storage/
[bus di servizio di Azure]: https://azure.microsoft.com/documentation/services/service-bus/

[Guida per sviluppatori di IoT Hub]: iot-hub-devguide.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
[iniziare con l'IoT Hub]: iot-hub-java-java-getstarted.md
[Centro per sviluppatori di Azure IoT]: https://azure.microsoft.com/develop/iot
[gestione degli errori temporanei]: https://msdn.microsoft.com/library/hh675232.aspx

<!-- Links -->
[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
