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
# <a name="process-iot-hub-device-to-cloud-messages-java"></a><span data-ttu-id="c536c-103">Elaborare messaggi da dispositivo a cloud dell'hub IoT (Java)</span><span class="sxs-lookup"><span data-stu-id="c536c-103">Process IoT Hub device-to-cloud messages (Java)</span></span>

[!INCLUDE [iot-hub-selector-process-d2c](../../includes/iot-hub-selector-process-d2c.md)]

<span data-ttu-id="c536c-104">L'hub IoT di Azure è un servizio completamente gestito che consente comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="c536c-104">Azure IoT Hub is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="c536c-105">Altre esercitazioni ([iniziare con l'IoT Hub] e [inviare messaggi da cloud a dispositivo con l'IoT Hub][lnk-c2d]) viene illustrato come toouse hello base dispositivo a cloud e cloud a dispositivo funzionalità di messaggistica di IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c536c-105">Other tutorials ([Get started with IoT Hub] and [Send cloud-to-device messages with IoT Hub][lnk-c2d]) show you how toouse hello basic device-to-cloud and cloud-to-device messaging functionality of IoT Hub.</span></span>

<span data-ttu-id="c536c-106">In questa esercitazione si basa sul codice hello di hello [iniziare con l'IoT Hub] esercitazione e Mostra come toouse messaggio routing dei messaggi da dispositivo a cloud tooprocess in modo scalabile.</span><span class="sxs-lookup"><span data-stu-id="c536c-106">This tutorial builds on hello code shown in hello [Get started with IoT Hub] tutorial, and shows you how toouse message routing tooprocess device-to-cloud messages in a scalable way.</span></span> <span data-ttu-id="c536c-107">esercitazione Hello viene illustrato come tooprocess messaggi che richiedono un intervento immediato dalla soluzione hello back-end.</span><span class="sxs-lookup"><span data-stu-id="c536c-107">hello tutorial illustrates how tooprocess messages that require immediate action from hello solution back end.</span></span> <span data-ttu-id="c536c-108">Ad esempio, un dispositivo potrebbe inviare un messaggio di avviso che attiva l'inserimento di un ticket in un sistema CRM.</span><span class="sxs-lookup"><span data-stu-id="c536c-108">For example, a device might send an alarm message that triggers inserting a ticket into a CRM system.</span></span> <span data-ttu-id="c536c-109">Al contrario, i messaggi di punto dati vengono semplicemente inseriti in un motore di analisi.</span><span class="sxs-lookup"><span data-stu-id="c536c-109">By contrast, data-point messages simply feed into an analytics engine.</span></span> <span data-ttu-id="c536c-110">Telemetria temperatura da un dispositivo che è toobe archiviati per poterli analizzare in seguito è ad esempio, un messaggio di punto dati.</span><span class="sxs-lookup"><span data-stu-id="c536c-110">For example, temperature telemetry from a device that is toobe stored for later analysis is a data-point message.</span></span>

<span data-ttu-id="c536c-111">Alla fine di hello di questa esercitazione, si esegue tre applicazioni di console Java:</span><span class="sxs-lookup"><span data-stu-id="c536c-111">At hello end of this tutorial, you run three Java console apps:</span></span>

* <span data-ttu-id="c536c-112">**dispositivo simulato**, una versione modificata dell'applicazione hello creato in hello [iniziare con l'IoT Hub] esercitazione, invia i messaggi da dispositivo a cloud punto dati ogni secondo e messaggi di dispositivo a cloud interattivo ogni 10 secondi.</span><span class="sxs-lookup"><span data-stu-id="c536c-112">**simulated-device**, a modified version of hello app created in hello [Get started with IoT Hub] tutorial, sends data-point device-to-cloud messages every second, and interactive device-to-cloud messages every 10 seconds.</span></span> <span data-ttu-id="c536c-113">Questa app utilizza hello AMQP protocollo toocommunicate con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c536c-113">This app uses hello AMQP protocol toocommunicate with IoT Hub.</span></span>
* <span data-ttu-id="c536c-114">**i messaggi di d2c lettura** Visualizza dati di telemetria hello inviati per l'app del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c536c-114">**read-d2c-messages** displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="c536c-115">**lettura coda critico** coda i messaggi critici hello da hello Bus di servizio collegata coda toohello hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c536c-115">**read-critical-queue** de-queues hello critical messages from hello Service Bus queue attached toohello IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="c536c-116">L'hub IoT offre il supporto SDK per molte piattaforme e linguaggi, inclusi C, Java e JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c536c-116">IoT Hub has SDK support for many device platforms and languages, including C, Java, and JavaScript.</span></span> <span data-ttu-id="c536c-117">Per istruzioni su come tooreplace hello dispositivo in questa esercitazione con un dispositivo fisico, e tooconnect dispositivi tooan IoT Hub, vedere hello [Centro per sviluppatori di Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="c536c-117">For instructions on how tooreplace hello device in this tutorial with a physical device, and how tooconnect devices tooan IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="c536c-118">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c536c-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="c536c-119">Una versione completa di utilizzo di hello [iniziare con l'IoT Hub] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c536c-119">A complete working version of hello [Get started with IoT Hub] tutorial.</span></span>
* <span data-ttu-id="c536c-120">versione più recente Hello [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="c536c-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="c536c-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="c536c-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="c536c-122">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="c536c-122">An active Azure account.</span></span> <span data-ttu-id="c536c-123">Se non si dispone di un account, è possibile creare un [account di valutazione gratuita] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="c536c-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="c536c-124">È necessaria una conoscenza di base di [Archiviazione di Azure] e del [bus di servizio di Azure].</span><span class="sxs-lookup"><span data-stu-id="c536c-124">You should have some basic knowledge of [Azure Storage] and [Azure Service Bus].</span></span>

## <a name="send-interactive-messages-from-a-device-app"></a><span data-ttu-id="c536c-125">Inviare messaggi interattivi da un'app per dispositivi</span><span class="sxs-lookup"><span data-stu-id="c536c-125">Send interactive messages from a device app</span></span>
<span data-ttu-id="c536c-126">In questa sezione, si modifica hello app del dispositivo è stato creato in hello [iniziare con l'IoT Hub] toooccasionally esercitazione inviare i messaggi che richiedono l'elaborazione immediata.</span><span class="sxs-lookup"><span data-stu-id="c536c-126">In this section, you modify hello device app you created in hello [Get started with IoT Hub] tutorial toooccasionally send messages that require immediate processing.</span></span>

1. <span data-ttu-id="c536c-127">Utilizzare un file di testo dell'editor tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="c536c-127">Use a text editor tooopen hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span> <span data-ttu-id="c536c-128">Questo file contiene codice hello hello **dispositivo simulato** app è stato creato in hello [iniziare con l'IoT Hub] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c536c-128">This file contains hello code for hello **simulated-device** app you created in hello [Get started with IoT Hub] tutorial.</span></span>

2. <span data-ttu-id="c536c-129">Sostituire hello **MessageSender** classe con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="c536c-129">Replace hello **MessageSender** class with hello following code:</span></span>

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
   
    <span data-ttu-id="c536c-130">Questo metodo aggiunge in modo casuale proprietà hello `"level": "critical"` toomessages inviato dal dispositivo hello, che simula un messaggio che richiede un intervento immediato per hello applicazione back-end.</span><span class="sxs-lookup"><span data-stu-id="c536c-130">This method randomly adds hello property `"level": "critical"` toomessages sent by hello device, which simulates a message that requires immediate action by hello application back-end.</span></span> <span data-ttu-id="c536c-131">un'applicazione Hello passa le informazioni nelle proprietà di messaggio hello, anziché nel corpo del messaggio hello, in modo che l'IoT Hub può instradare destinazione dei messaggi appropriata toohello messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="c536c-131">hello application passes this information in hello message properties, instead of in hello message body, so that IoT Hub can route hello message toohello proper message destination.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c536c-132">È possibile utilizzare i messaggi tooroute di proprietà di messaggio per vari scenari, tra cui freddo-path, l'elaborazione, inoltre toohello percorso ricorrente riportato di seguito viene illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="c536c-132">You can use message properties tooroute messages for various scenarios including cold-path processing, in addition toohello hot path example shown here.</span></span>

2. <span data-ttu-id="c536c-133">Salvare e chiudere il file di simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="c536c-133">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c536c-134">Per i migliori risultati hello di semplicità, in questa esercitazione non implementa alcun criterio di tentativo.</span><span class="sxs-lookup"><span data-stu-id="c536c-134">For hello sake of simplicity, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="c536c-135">Nel codice di produzione, è necessario implementare un criterio di ripetizione, ad esempio backoff esponenziale, come indicato nell'articolo MSDN hello [gestione degli errori temporanei].</span><span class="sxs-lookup"><span data-stu-id="c536c-135">In production code, you should implement a retry policy such as exponential backoff, as suggested in hello MSDN article [Transient Fault Handling].</span></span>

3. <span data-ttu-id="c536c-136">hello toobuild **dispositivo simulato** app usando Maven, eseguire hello comando al prompt dei comandi di hello nella cartella dispositivo simulato hello seguente:</span><span class="sxs-lookup"><span data-stu-id="c536c-136">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="add-a-queue-tooyour-iot-hub-and-route-messages-tooit"></a><span data-ttu-id="c536c-137">Aggiungere una coda tooyour IoT hub e instradare i messaggi tooit</span><span class="sxs-lookup"><span data-stu-id="c536c-137">Add a queue tooyour IoT hub and route messages tooit</span></span>

<span data-ttu-id="c536c-138">In questa sezione, creare una coda di Service Bus, connetterlo hub IoT tooyour e configurare la coda IoT hub toosend messaggi toohello in base hello presenza di una proprietà nel messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="c536c-138">In this section, you create a Service Bus queue, connect it tooyour IoT hub, and configure your IoT hub toosend messages toohello queue based on hello presence of a property on hello message.</span></span> <span data-ttu-id="c536c-139">Per ulteriori informazioni su come tooprocess messaggi dalle code del Bus di servizio, vedere [iniziare con le code][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="c536c-139">For more information about how tooprocess messages from Service Bus queues, see [Get started with queues][lnk-sb-queues-java].</span></span>

1. <span data-ttu-id="c536c-140">Creare una coda del bus di servizio, come descritto in [Get started with queues][lnk-sb-queues-java] (Introduzione alle code).</span><span class="sxs-lookup"><span data-stu-id="c536c-140">Create a Service Bus queue as described in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="c536c-141">Prendere nota del nome dello spazio dei nomi e di Accodamento di hello.</span><span class="sxs-lookup"><span data-stu-id="c536c-141">Make a note of hello namespace and queue name.</span></span>

2. <span data-ttu-id="c536c-142">In hello portale di Azure, aprire l'hub IoT e fare clic su **endpoint**.</span><span class="sxs-lookup"><span data-stu-id="c536c-142">In hello Azure portal, open your IoT hub and click **Endpoints**.</span></span>

    ![Endpoint in hub IoT][30]

3. <span data-ttu-id="c536c-144">In hello **endpoint** pannello, fare clic su **Aggiungi** in hello tooadd superiore dell'hub IoT tooyour di coda.</span><span class="sxs-lookup"><span data-stu-id="c536c-144">In hello **Endpoints** blade, click **Add** at hello top tooadd your queue tooyour IoT hub.</span></span> <span data-ttu-id="c536c-145">Endpoint hello nome **CriticalQueue** e utilizzare hello elenchi a discesa tooselect **coda di Service Bus**hello dello spazio dei nomi Service Bus in cui risiede la coda e nome della coda di hello.</span><span class="sxs-lookup"><span data-stu-id="c536c-145">Name hello endpoint **CriticalQueue** and use hello drop-downs tooselect **Service Bus queue**, hello Service Bus namespace in which your queue resides, and hello name of your queue.</span></span> <span data-ttu-id="c536c-146">Al termine, fare clic su **salvare** nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="c536c-146">When you are done, click **Save** at hello bottom.</span></span>

    ![Aggiunta di un endpoint][31]

4. <span data-ttu-id="c536c-148">Fare clic su **Route** nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c536c-148">Now click **Routes** in your IoT Hub.</span></span> <span data-ttu-id="c536c-149">Fare clic su **Aggiungi** nella parte superiore di hello di hello pannello toocreate una regola di routing che instrada i messaggi toohello coda è appena aggiunto.</span><span class="sxs-lookup"><span data-stu-id="c536c-149">Click **Add** at hello top of hello blade toocreate a routing rule that routes messages toohello queue you just added.</span></span> <span data-ttu-id="c536c-150">Selezionare **DeviceTelemetry** come origine dati hello.</span><span class="sxs-lookup"><span data-stu-id="c536c-150">Select **DeviceTelemetry** as hello source of data.</span></span> <span data-ttu-id="c536c-151">Immettere `level="critical"` come condizione hello e scegliere coda hello appena aggiunto come un endpoint personalizzato come hello endpoint regola di routing.</span><span class="sxs-lookup"><span data-stu-id="c536c-151">Enter `level="critical"` as hello condition, and choose hello queue you just added as a custom endpoint as hello routing rule endpoint.</span></span> <span data-ttu-id="c536c-152">Al termine, fare clic su **salvare** nella parte inferiore di hello.</span><span class="sxs-lookup"><span data-stu-id="c536c-152">When you are done, click **Save** at hello bottom.</span></span>

    ![Aggiunta di un route][32]

    <span data-ttu-id="c536c-154">Assicurarsi di route fallback hello è troppo**ON**.</span><span class="sxs-lookup"><span data-stu-id="c536c-154">Make sure hello fallback route is set too**ON**.</span></span> <span data-ttu-id="c536c-155">Questa impostazione è una configurazione predefinita di hello di un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c536c-155">This setting is hello default configuration of an IoT hub.</span></span>

    ![Route di fallback][33]

## <a name="optional-read-from-hello-queue-endpoint"></a><span data-ttu-id="c536c-157">(Facoltativo) Lettura dall'endpoint di coda hello</span><span class="sxs-lookup"><span data-stu-id="c536c-157">(Optional) Read from hello queue endpoint</span></span>

<span data-ttu-id="c536c-158">Facoltativamente, è possibile leggere i messaggi hello dall'endpoint di coda hello seguendo le istruzioni hello [iniziare con le code][lnk-sb-queues-java].</span><span class="sxs-lookup"><span data-stu-id="c536c-158">You can optionally read hello messages from hello queue endpoint by following hello instructions in [Get started with queues][lnk-sb-queues-java].</span></span> <span data-ttu-id="c536c-159">Nome hello app **lettura coda critico**.</span><span class="sxs-lookup"><span data-stu-id="c536c-159">Name hello app **read-critical-queue**.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="c536c-160">Eseguire applicazioni hello</span><span class="sxs-lookup"><span data-stu-id="c536c-160">Run hello applications</span></span>

<span data-ttu-id="c536c-161">Si è ora pronto toorun hello e tre le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="c536c-161">Now you are ready toorun hello three applications.</span></span>

1. <span data-ttu-id="c536c-162">hello toorun **d2c-i-messaggi** applicazione, in un prompt dei comandi della shell passare toohello lettura d2c cartella ed eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c536c-162">toorun hello **read-d2c-messages** application, in a command prompt or shell navigate toohello read-d2c folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```

   ![Eseguire read-d2c-messages][readd2c]

2. <span data-ttu-id="c536c-164">hello toorun **lettura coda critico** applicazione, in un prompt dei comandi della shell esplorazione delle cartelle di lettura coda critico toohello ed esecuzione hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c536c-164">toorun hello **read-critical-queue** application, in a command prompt or shell navigate toohello read-critical-queue folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Eseguire read-critical-queue][readqueue]

3. <span data-ttu-id="c536c-166">hello toorun **dispositivo simulato** app, in un prompt dei comandi della shell passare cartella dispositivo simulato toohello ed eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c536c-166">toorun hello **simulated-device** app, in a command prompt or shell navigate toohello simulated-device folder and execute hello following command:</span></span>

   ```cmd/sh
   mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
   ```
   
   ![Eseguire simulated-device][simulateddevice]

## <a name="next-steps"></a><span data-ttu-id="c536c-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c536c-168">Next steps</span></span>

<span data-ttu-id="c536c-169">In questa esercitazione è stato descritto come tooreliably inviare i messaggi da dispositivo a cloud tramite funzionalità di routing messaggi hello dell'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="c536c-169">In this tutorial, you learned how tooreliably dispatch device-to-cloud messages by using hello message routing functionality of IoT Hub.</span></span>

<span data-ttu-id="c536c-170">Hello [come toosend cloud a dispositivo messaggi con l'IoT Hub] [ lnk-c2d] viene illustrato come toosend messaggi dispositivi tooyour la soluzione di back-end.</span><span class="sxs-lookup"><span data-stu-id="c536c-170">hello [How toosend cloud-to-device messages with IoT Hub][lnk-c2d] shows you how toosend messages tooyour devices from your solution back end.</span></span>

<span data-ttu-id="c536c-171">esempi di toosee di soluzioni end-to-end completate che usa IoT Hub, vedere [Azure IoT Suite][lnk-suite].</span><span class="sxs-lookup"><span data-stu-id="c536c-171">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite][lnk-suite].</span></span>

<span data-ttu-id="c536c-172">toolearn più sullo sviluppo di soluzioni con l'IoT Hub, vedere hello [Guida per sviluppatori di IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="c536c-172">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<span data-ttu-id="c536c-173">toolearn informazioni su routing dei messaggi nell'IoT Hub, vedere [inviare e ricevere messaggi con l'IoT Hub][lnk-devguide-messaging].</span><span class="sxs-lookup"><span data-stu-id="c536c-173">toolearn more about message routing in IoT Hub, see [Send and receive messages with IoT Hub][lnk-devguide-messaging].</span></span>

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
