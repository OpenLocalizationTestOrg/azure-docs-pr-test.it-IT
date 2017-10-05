---
title: Elaborare messaggi da dispositivo a cloud dell'hub IoT di Azure (Java) | Microsoft Docs
description: Come elaborare i messaggi da dispositivo a cloud dell'hub IoT usando le regole di routing e gli endpoint personalizzati per inviare i messaggi agli altri servizi di back-end.
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
ms.openlocfilehash: d1aca8f39e305105d4ec9f63fbe7bee95487e294
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="d5528-103">Elaborare messaggi da dispositivo a cloud dell'hub IoT (Java)</span><span class="sxs-lookup"><span data-stu-id="d5528-103">Process IoT Hub device-to-cloud messages (Java)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="d5528-104">L'hub IoT di Azure è un servizio completamente gestito che consente comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="d5528-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="d5528-105">Altre esercitazioni, ad esempio [Get started with IoT Hub] e [Inviare messaggi da cloud a dispositivo con l'hub IoT][lnk-c2d], illustrano come usare le funzionalità di messaggistica di base da dispositivo a cloud e da cloud a dispositivo dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d5528-105">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how to use the basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="d5528-106">Questa esercitazione è basata sul codice mostrato nell'esercitazione [Get started with IoT Hub] (Introduzione all'hub IoT) e come usare il routing dei messaggi per elaborare i messaggi da dispositivo a cloud in modo scalabile.</span><span class="sxs-lookup"><span data-stu-id="d5528-106">This tutorial builds on the code shown in the [Get started with IoT Hub] tutorial, and shows you how to use message routing to process device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="d5528-107">L'esercitazione illustra come elaborare i messaggi che richiedono un intervento immediato dal back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="d5528-107">The tutorial illustrates how to process messages that require immediate action from the solution back end.</span></span> <span data-ttu-id="d5528-108">Ad esempio, un dispositivo potrebbe inviare un messaggio di avviso che attiva l'inserimento di un ticket in un sistema CRM.</span><span class="sxs-lookup"><span data-stu-id="d5528-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="d5528-109">Al contrario, i messaggi di punto dati vengono semplicemente inseriti in un motore di analisi.</span><span class="sxs-lookup"><span data-stu-id="d5528-109">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="d5528-110">Ad esempio, i dati di telemetria sulla temperatura di un dispositivo che devono essere archiviati per una successiva analisi costituiscono un messaggio di punti dati.</span><span class="sxs-lookup"><span data-stu-id="d5528-110">For example, temperature telemetry from a device that is to be stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="d5528-111">Al termine di questa esercitazione, vengono eseguite tre app console Java:</span><span class="sxs-lookup"><span data-stu-id="d5528-111">At the end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="d5528-112">**SimulatedDevice**, una versione modificata dell'app creata nell'esercitazione [Get started with IoT Hub] , che invia messaggi di punti dati da dispositivo a cloud ogni secondo e messaggi interattivi da dispositivo a cloud ogni 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="d5528-112">**simulated-device**, a modified version of the app created in the [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="d5528-113">Questa app usa il protocollo AMQP per comunicare con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d5528-113">This app uses the AMQP protocol to communicate with IoT Hub.</span></span>
* <span data-ttu-id="d5528-114">**read-d2c-messages** consente di visualizzare i dati di telemetria inviati dall'app per dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d5528-114">**read-d2c-messages** displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="d5528-115">**read-critical-queue** rimuove dalla coda i messaggi dalla coda importanti della coda del bus di servizio collegato all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d5528-115">**read-critical-queue** de-queues the critical messages from the Service Bus queue attached to the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="d5528-116">L'hub IoT offre il supporto SDK per molte piattaforme e linguaggi, inclusi C, Java e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d5528-116">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="d5528-117">Per istruzioni su come sostituire il dispositivo in questa esercitazione con un dispositivo fisico e su come connettere dispositivi a un hub IoT, fare riferimento al [Centro per sviluppatori Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="d5528-117">For instructions on how to replace the device in this tutorial with a physical device, and how to connect devices to an IoT Hub, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="d5528-118">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d5528-118">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="d5528-119">Una versione di lavoro completa dell'esercitazione di [Get started with IoT Hub] .</span><span class="sxs-lookup"><span data-stu-id="d5528-119">A complete working version of the [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="d5528-120">[Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) più recente</span><span class="sxs-lookup"><span data-stu-id="d5528-120">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="d5528-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="d5528-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="d5528-122">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="d5528-122">An active Azure account.</span></span> <span data-ttu-id="d5528-123">Se non si dispone di un account, è possibile creare un [account di valutazione gratuita] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="d5528-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="d5528-124">È necessaria una conoscenza di base di [Archiviazione di Azure] e del [bus di servizio di Azure].</span><span class="sxs-lookup"><span data-stu-id="d5528-124">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-device-app"></a><span data-ttu-id="d5528-125">Inviare messaggi interattivi da un'app per dispositivi</span><span class="sxs-lookup"><span data-stu-id="d5528-125">Send interactive messages from a device app</span></span>
<span data-ttu-id="d5528-126">In questa sezione viene modificata l'app per dispositivi creata nell'esercitazione [Get started with IoT Hub] per inviare occasionalmente messaggi che richiedono un intervento immediato.</span><span class="sxs-lookup"><span data-stu-id="d5528-126">In this section, you modify the device app you created in the [Get started with IoT Hub] tutorial to occasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="d5528-127">Usare un editor di testo per aprire il file simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="d5528-127">Use a text editor to open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="d5528-128">Questo file contiene il codice dell'app **simulated-device** creata durante l'esercitazione di [Get started with IoT Hub] .</span><span class="sxs-lookup"><span data-stu-id="d5528-128">This file contains the code for the **simulated-device** app you created in the [Get started with IoT Hub] tutorial.</span></span>

2. <span data-ttu-id="d5528-129">Sostituire la classe **MessageSender** con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d5528-129">Replace the **MessageSender** class with the following code:</span></span>

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
   
    <span data-ttu-id="d5528-130">Questo metodo aggiunge in modo casuale la proprietà `"level": "critical"` ai messaggi inviati dal dispositivo, simulando così un messaggio che richiede l'intervento immediato del back-end dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d5528-130">This method randomly adds the property `"level": "critical"` to messages sent by the device, which simulates a message that requires immediate action by the application back-end.</span></span> <span data-ttu-id="d5528-131">L'applicazione passa queste informazioni nelle proprietà del messaggio anziché nel corpo del messaggio, in modo che l'hub IoT possa indirizzare il messaggio alla destinazione messaggi appropriata.</span><span class="sxs-lookup"><span data-stu-id="d5528-131">The application passes this information in the message properties, instead of in the message body, so that IoT Hub can route the message to the proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d5528-132">È possibile usare le proprietà del messaggio per indirizzare i messaggi in diversi scenari, tra cui l'elaborazione del percorso a freddo, oltre all'esempio del percorso a caldo mostrato qui.</span><span class="sxs-lookup"><span data-stu-id="d5528-132">You can use message properties to route messages for various scenarios including cold-path processing, in addition to the hot path example shown here.</span></span>

2. <span data-ttu-id="d5528-133">Salvare e chiudere il file simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="d5528-133">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d5528-134">Per semplicità, questa esercitazione non implementa alcun criterio di ripetizione.</span><span class="sxs-lookup"><span data-stu-id="d5528-134">For the sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="d5528-135">Nel codice di produzione è consigliabile implementare criteri di ripetizione dei tentativi, ad esempio un backoff esponenziale, come indicato nell'articolo di MSDN relativo alla [Transient Fault Handling](Gestione degli errori temporanei).</span><span class="sxs-lookup"><span data-stu-id="d5528-135">In production code, you should implement a retry policy such as exponential backoff, as suggested in the MSDN article [Transient Fault Handling].</span></span>

3. <span data-ttu-id="d5528-136">Per compilare l'app **simulated-device** con Maven, eseguire questo comando al prompt dei comandi nella cartella simulated-device:</span><span class="sxs-lookup"><span data-stu-id="d5528-136">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-to-your-iot-hub-and-route-messages-to-it"></a><span data-ttu-id="d5528-137">Aggiungere una coda all'hub IoT e indirizzarvi i messaggi</span><span class="sxs-lookup"><span data-stu-id="d5528-137">Add a queue to your IoT hub and route messages to it</span></span>

<span data-ttu-id="d5528-138">In questa sezione, viene illustrato come creare una coda del bus di servizio, connetterla all'hub IoT e configurare l'hub IoT per inviare messaggi alla coda in base alla presenza di una proprietà del messaggio.</span><span class="sxs-lookup"><span data-stu-id="d5528-138">In this section, you create a Service Bus queue, connect it to your IoT hub, and configure your IoT hub to send messages to the queue based on the presence of a property on the message.</span></span> <span data-ttu-id="d5528-139">Per altre informazioni su come elaborare i messaggi dalle code del bus di servizio, vedere [Get started with queues][lnk-sb-queues-java] (Introduzione alle code).</span><span class="sxs-lookup"><span data-stu-id="d5528-139">For more information about how to process messages from Service Bus queues, see [Get started with queues][lnk-sb-queues-java].</span></span>

1. <span data-ttu-id="d5528-140">Creare una coda del bus di servizio, come descritto in [Get started with queues][lnk-sb-queues-java] (Introduzione alle code).</span><span class="sxs-lookup"><span data-stu-id="d5528-140">Create a Service Bus queue as described in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="d5528-141">Prendere nota dello spazio dei nomi e del nome della coda.</span><span class="sxs-lookup"><span data-stu-id="d5528-141">Make a note of the namespace and queue name.</span></span>

2. <span data-ttu-id="d5528-142">Nel Portale di Azure, aprire l'hub IoT e fare clic su **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="d5528-142">In the Azure portal, open your IoT hub and click **Endpoints**.</span></span>

    ![Endpoint in hub IoT][30]

3. <span data-ttu-id="d5528-144">Nel pannello **Endpoint** fare clic su **Aggiungi** in alto per aggiungere la coda all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d5528-144">In the **Endpoints** blade, click **Add** at the top to add your queue to your IoT hub.</span></span> <span data-ttu-id="d5528-145">Denominare l'endpoint **CriticalQueue** e usare il menu a discesa per selezionare **Coda del bus di servizio**, lo spazio dei nomi del bus di servizio in cui si trova la coda e il nome della coda.</span><span class="sxs-lookup"><span data-stu-id="d5528-145">Name the endpoint **CriticalQueue** and use the drop-downs to select **Service Bus queue**, the Service Bus namespace in which your queue resides, and the name of your queue.</span></span> <span data-ttu-id="d5528-146">Al termine, fare clic su **Salva** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="d5528-146">When you are done, click **Save** at the bottom.</span></span>

    ![Aggiunta di un endpoint][31]

4. <span data-ttu-id="d5528-148">Fare clic su **Route** nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d5528-148">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="d5528-149">Fare clic su **Aggiungi** nella parte superiore del pannello per creare una regola di routing che indirizzi i messaggi alla coda appena aggiunta.</span><span class="sxs-lookup"><span data-stu-id="d5528-149">Click **Add** at the top of the blade to create a routing rule that routes messages to the queue you just added.</span></span> <span data-ttu-id="d5528-150">Selezionare **DeviceTelemetry** come origine dei dati.</span><span class="sxs-lookup"><span data-stu-id="d5528-150">Select **DeviceTelemetry** as the source of data.</span></span> <span data-ttu-id="d5528-151">Immettere `level="critical"` come condizione, quindi scegliere la coda appena aggiunta come endpoint personalizzato, come endpoint della regola di routing.</span><span class="sxs-lookup"><span data-stu-id="d5528-151">Enter `level="critical"` as the condition, and choose the queue you just added as a custom endpoint as the routing rule endpoint.</span></span> <span data-ttu-id="d5528-152">Al termine, fare clic su **Salva** nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="d5528-152">When you are done, click **Save** at the bottom.</span></span>

    ![Aggiunta di un route][32]

    <span data-ttu-id="d5528-154">Assicurarsi che il route di fallback sia impostato su **ON**.</span><span class="sxs-lookup"><span data-stu-id="d5528-154">Make sure the fallback route is set to **ON**.</span></span> <span data-ttu-id="d5528-155">Questa impostazione è la configurazione predefinita dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d5528-155">This setting is the default configuration of an IoT hub.</span></span>

    ![Route di fallback][33]

## <a name="optional-read-from-the-queue-endpoint"></a><span data-ttu-id="d5528-157">(Facoltativo) Lettura dell'endpoint della coda</span><span class="sxs-lookup"><span data-stu-id="d5528-157">(Optional) Read from the queue endpoint</span></span>

<span data-ttu-id="d5528-158">È facoltativamente possibile leggere i messaggi dall'endpoint della coda seguendo le istruzioni contenute in [Get started with queues][lnk-sb-queues-java] (Introduzione alle code).</span><span class="sxs-lookup"><span data-stu-id="d5528-158">You can optionally read the messages from the queue endpoint by following the instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="d5528-159">Denominare l'app **read-critical-queue**.</span><span class="sxs-lookup"><span data-stu-id="d5528-159">Name the app **read-critical-queue**.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="d5528-160">Eseguire le applicazioni</span><span class="sxs-lookup"><span data-stu-id="d5528-160">Run the applications</span></span>

<span data-ttu-id="d5528-161">A questo punto è possibile eseguire le tre applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d5528-161">Now you are ready to run the three applications.</span></span>

1. <span data-ttu-id="d5528-162">Per eseguire l'applicazione **read-d2c-messages** in un prompt dei comandi o nella shell passare alla cartella read-d2c ed eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d5528-162">To run the **read-d2c-messages** application, in a command prompt or shell navigate to the read-d2c folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Eseguire read-d2c-messages][readd2c]

2. <span data-ttu-id="d5528-164">Per eseguire l'applicazione **read-critical-queue** in un prompt dei comandi o nella shell passare alla cartella read-critical-queue ed eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d5528-164">To run the **read-critical-queue** application, in a command prompt or shell navigate to the read-critical-queue folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Eseguire read-critical-queue][readqueue]

3. <span data-ttu-id="d5528-166">Per eseguire l'app **simulated-device**, in un prompt dei comandi o nella shell passare alla cartella simulated-device ed eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="d5528-166">To run the **simulated-device** app, in a command prompt or shell navigate to the simulated-device folder and execute the following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Eseguire simulated-device][simulateddevice]

## <a name="next-steps"></a><span data-ttu-id="d5528-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d5528-168">Next steps</span></span>

<span data-ttu-id="d5528-169">In questa esercitazione è stato descritto come inviare i messaggi da dispositivo a cloud in modo affidabile usando la funzionalità di routing dei messaggi dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="d5528-169">In this tutorial, you learned how to reliably dispatch device-to-cloud messages by using the message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="d5528-170">L'esercitazione [Come inviare messaggi da cloud a dispositivo con l'hub IoT][lnk-c2d] descrive le modalità di invio dei messaggi ai dispositivi dal back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="d5528-170">The [How to send cloud-to-device messages with IoT Hub][lnk-c2d] shows you how to send messages to your devices from your solution back end.</span></span>

<span data-ttu-id="d5528-171">Per avere esempi di soluzioni complete che usano l'hub IoT, vedere [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="d5528-171">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="d5528-172">Per altre informazioni sullo sviluppo delle soluzioni con l'hub IoT, vedere la [Guida per sviluppatori dell'hub IoT].</span><span class="sxs-lookup"><span data-stu-id="d5528-172">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<span data-ttu-id="d5528-173">Per ulteriori informazioni sul routing dei messaggi nell'hub IoT, vedere [Inviare e ricevere messaggi con l'hub IoT][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="d5528-173">To learn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

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

<span data-ttu-id="d5528-174">[Archiviazione di Azure]: https://azure.microsoft.com/documentation/services/storage/</span><span class="sxs-lookup"><span data-stu-id="d5528-174">[Azure Storage]: https://azure.microsoft.com/documentation/services/storage/</span></span>
<span data-ttu-id="d5528-175">[bus di servizio di Azure]: https://azure.microsoft.com/documentation/services/service-bus/</span><span class="sxs-lookup"><span data-stu-id="d5528-175">[Azure Service Bus]: https://azure.microsoft.com/documentation/services/service-bus/</span></span>

<span data-ttu-id="d5528-176">[Guida per sviluppatori dell'hub IoT]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="d5528-176">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
<span data-ttu-id="d5528-177">[Get started with IoT Hub]: iot-hub-java-java-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="d5528-177">[Get started with IoT Hub]: iot-hub-java-java-getstarted.md</span></span>
<span data-ttu-id="d5528-178">[Centro per sviluppatori Azure IoT]: https://azure.microsoft.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="d5528-178">[Azure IoT Developer Center]: https://azure.microsoft.com/develop/iot</span></span>
<span data-ttu-id="d5528-179">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh675232.aspx</span><span class="sxs-lookup"><span data-stu-id="d5528-179">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh675232.aspx</span></span>

<!-- Links -->
<span data-ttu-id="d5528-180">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="d5528-180">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>

[lnk-c2d]: iot-hub-java-java-c2d.md
[lnk-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
