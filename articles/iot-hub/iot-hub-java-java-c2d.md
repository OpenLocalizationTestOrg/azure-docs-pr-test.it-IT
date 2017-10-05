---
title: Messaggi da cloud a dispositivo con l'hub IoT di Azure (Java) | Microsoft Docs
description: Come inviare messaggi da cloud a dispositivo a un dispositivo da un hub IoT di Azure usando Azure IoT SDK per Java. Modificare un'app per dispositivo simulato per ricevere messaggi da cloud a dispositivo e modificare un'app back-end per inviare i messaggi da cloud a dispositivo.
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
ms.openlocfilehash: f5e3ac46f4d144b12e2ab7fcfb456665ff6cc68f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a><span data-ttu-id="50813-104">Inviare messaggi da cloud a dispositivo con l'hub IoT (Java)</span><span class="sxs-lookup"><span data-stu-id="50813-104">Send cloud-to-device messages with IoT Hub (Java)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

<span data-ttu-id="50813-105">L'hub IoT di Azure è un servizio completamente gestito che consente di abilitare comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="50813-105">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="50813-106">L'esercitazione [Introduzione all'hub IoT di Azure] illustra come creare un hub IoT, effettuare il provisioning dell'identità di un dispositivo al suo interno e creare il codice di un'app per dispositivo simulato che invia messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="50813-106">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="50813-107">Questa esercitazione si basa su [Introduzione all'hub IoT di Azure].</span><span class="sxs-lookup"><span data-stu-id="50813-107">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="50813-108">Illustra le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="50813-108">It shows you how to:</span></span>

* <span data-ttu-id="50813-109">Dal back-end della soluzione inviare messaggi da cloud a dispositivo a un singolo dispositivo tramite l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="50813-109">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="50813-110">Ricevere messaggi da cloud a dispositivo in un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="50813-110">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="50813-111">Dal back-end della soluzione richiedere l'acknowledgement di recapito (*feedback*) per i messaggi inviati a un dispositivo dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="50813-111">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="50813-112">Per altre informazioni sui messaggi da cloud a dispositivo, vedere la[Guida per sviluppatori dell'hub IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="50813-112">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="50813-113">Al termine di questa esercitazione, vengono eseguite due app console Java:</span><span class="sxs-lookup"><span data-stu-id="50813-113">At the end of this tutorial, you run two Java console apps:</span></span>

* <span data-ttu-id="50813-114">**simulated-device**, una versione modificata dell'app creata in [Introduzione all'hub IoT di Azure], che si connette all'hub IoT e riceve messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="50813-114">**simulated-device**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="50813-115">**send-c2d-messages**, che invia un messaggio da cloud a dispositivo all'app per dispositivo simulato tramite l'hub IoT e riceve quindi l'acknowledgement del recapito.</span><span class="sxs-lookup"><span data-stu-id="50813-115">**send-c2d-messages**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="50813-116">L’hub IoT dispone del supporto SDK per molte piattaforme e linguaggi (inclusi C, Java e Javascript) tramite gli SDK del dispositivo IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="50813-116">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="50813-117">Per istruzioni dettagliate su come connettere il dispositivo al codice dell'esercitazione e in generale all'hub IoT di Azure, vedere il [Centro per sviluppatori Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="50813-117">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>

<span data-ttu-id="50813-118">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="50813-118">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="50813-119">Una versione di lavoro completa dell'esercitazione [Introduzione all'hub IoT](iot-hub-java-java-getstarted.md) o [Elaborare messaggi da dispositivo a cloud dell'hub IoT](iot-hub-java-java-process-d2c.md).</span><span class="sxs-lookup"><span data-stu-id="50813-119">A complete working version of the [Get started with IoT Hub](iot-hub-java-java-getstarted.md) or [Process IoT Hub device-to-cloud messages](iot-hub-java-java-process-d2c.md) tutorial.</span></span>
* <span data-ttu-id="50813-120">[Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) più recente</span><span class="sxs-lookup"><span data-stu-id="50813-120">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="50813-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="50813-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="50813-122">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="50813-122">An active Azure account.</span></span> <span data-ttu-id="50813-123">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="50813-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="50813-124">Ricevere messaggi nell'app per dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="50813-124">Receive messages in the simulated device app</span></span>

<span data-ttu-id="50813-125">In questa sezione si modificherà l'app per il dispositivo simulato creata in [Introduzione all'hub IoT di Azure] per ricevere i messaggi da cloud a dispositivo dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="50813-125">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="50813-126">Usando un editor di testo, aprire il file simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="50813-126">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

2. <span data-ttu-id="50813-127">Aggiungere la seguente classe **MessageCallback** come classe annidata all'interno della classe **App**.</span><span class="sxs-lookup"><span data-stu-id="50813-127">Add the following **MessageCallback** class as a nested class inside the **App** class.</span></span> <span data-ttu-id="50813-128">Il metodo **execute** viene richiamato quando il dispositivo riceve un messaggio dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="50813-128">The **execute** method is invoked when the device receives a message from IoT Hub.</span></span> <span data-ttu-id="50813-129">In questo esempio, il dispositivo notifica sempre all'hub IoT di aver completato il messaggio:</span><span class="sxs-lookup"><span data-stu-id="50813-129">In this example, the device always notifies the IoT hub that it has completed the message:</span></span>

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. <span data-ttu-id="50813-130">Modificare il metodo **main** per creare un'istanza di **AppMessageCallback** e chiamare il metodo **setMessageCallback** prima dell'apertura del client, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="50813-130">Modify the **main** method to create an **AppMessageCallback** instance and call the **setMessageCallback** method before it opens the client as follows:</span></span>

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > <span data-ttu-id="50813-131">Se si usa HTTP/25 invece di MQTT o AMQP per il trasporto, l'istanza di **DeviceClient** controlla raramente i messaggi provenienti dall'hub IoT (meno di 25 minuti).</span><span class="sxs-lookup"><span data-stu-id="50813-131">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="50813-132">Per altre informazioni sulle differenze tra il supporto di MQTT, AMQP e HTTP e sulla limitazione delle richieste dell'hub IoT, vedere [Guida per gli sviluppatori dell'hub IoT][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="50813-132">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

4. <span data-ttu-id="50813-133">Per compilare l'app **simulated-device** con Maven, eseguire questo comando al prompt dei comandi nella cartella simulated-device:</span><span class="sxs-lookup"><span data-stu-id="50813-133">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="50813-134">Inviare un messaggio da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="50813-134">Send a cloud-to-device message</span></span>

<span data-ttu-id="50813-135">In questa sezione si crea un'app console Java che invia messaggi da cloud a dispositivo all'app del dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="50813-135">In this section, you create a Java console app that sends cloud-to-device messages to the simulated device app.</span></span> <span data-ttu-id="50813-136">È necessario l'ID del dispositivo aggiunto nell'esercitazione [Introduzione all'hub IoT di Azure] .</span><span class="sxs-lookup"><span data-stu-id="50813-136">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="50813-137">È necessaria anche la stringa di connessione per l'hub IoT, disponibile nel [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="50813-137">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span></span>

1. <span data-ttu-id="50813-138">Creare un progetto Maven denominato **send-c2d-messages** eseguendo questo comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="50813-138">Create a Maven project called **send-c2d-messages** using the following command at your command prompt.</span></span> <span data-ttu-id="50813-139">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="50813-139">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="50813-140">Al prompt dei comandi passare alla nuova cartella send-c2d-messages.</span><span class="sxs-lookup"><span data-stu-id="50813-140">At your command prompt, navigate to the new send-c2d-messages folder.</span></span>

3. <span data-ttu-id="50813-141">In un editor di testo aprire il file pom.xml nella cartella send-c2d-messages e aggiungere la dipendenza seguente al nodo **dependencies** .</span><span class="sxs-lookup"><span data-stu-id="50813-141">Using a text editor, open the pom.xml file in the send-c2d-messages folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="50813-142">L'aggiunta della dipendenza consente di usare il pacchetto **iothub-java-service-client** nell'applicazione per comunicare con il servizio hub IoT:</span><span class="sxs-lookup"><span data-stu-id="50813-142">Adding the dependency enables you to use the **iothub-java-service-client** package in your application to communicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="50813-143">È possibile cercare la versione più recente di **iot-service-client** usando la [ricerca di Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="50813-143">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="50813-144">Salvare e chiudere il file pom.xml.</span><span class="sxs-lookup"><span data-stu-id="50813-144">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="50813-145">In un editor di testo aprire il file send-c2d-messages\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="50813-145">Using a text editor, open the send-c2d-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="50813-146">Aggiungere al file le istruzioni **import** seguenti:</span><span class="sxs-lookup"><span data-stu-id="50813-146">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="50813-147">Aggiungere le variabili a livello di classe seguenti alla classe **App**, sostituendo **{yourhubconnectionstring}** e **{yourdeviceid}** con i valori annotati prima:</span><span class="sxs-lookup"><span data-stu-id="50813-147">Add the following class-level variables to the **App** class, replacing **{yourhubconnectionstring}** and **{yourdeviceid}** with the values your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. <span data-ttu-id="50813-148">Sostituire il metodo **main** con il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="50813-148">Replace the **main** method with the following code.</span></span> <span data-ttu-id="50813-149">Il codice seguente si connette all'hub IoT, invia un messaggio al dispositivo e quindi attende un riconoscimento che il dispositivo ha ricevuto ed elaborato il messaggio:</span><span class="sxs-lookup"><span data-stu-id="50813-149">This code connects to your IoT hub, sends a message to your device, and then waits for an acknowledgment that the device received and processed the message:</span></span>
   
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
   
        Message messageToSend = new Message("Cloud to device message.");
        messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
   
        serviceClient.send(deviceId, messageToSend);
        System.out.println("Message sent to device");
   
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
    > <span data-ttu-id="50813-150">Per semplicità, in questa esercitazione non si implementa alcun criterio di nuovi tentativi.</span><span class="sxs-lookup"><span data-stu-id="50813-150">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="50813-151">Nel codice di produzione è consigliabile implementare criteri di ripetizione dei tentativi, ad esempio un backoff esponenziale, come indicato nell'articolo di MSDN [Transient Fault Handling](Gestione degli errori temporanei).</span><span class="sxs-lookup"><span data-stu-id="50813-151">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>


9. <span data-ttu-id="50813-152">Per compilare l'app **simulated-device** con Maven, eseguire questo comando al prompt dei comandi nella cartella simulated-device:</span><span class="sxs-lookup"><span data-stu-id="50813-152">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-the-applications"></a><span data-ttu-id="50813-153">Eseguire le applicazioni</span><span class="sxs-lookup"><span data-stu-id="50813-153">Run the applications</span></span>

<span data-ttu-id="50813-154">A questo punto è possibile eseguire le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="50813-154">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="50813-155">Al prompt dei comandi nella cartella simulated-device eseguire questo comando per iniziare a inviare i dati di telemetria all'hub IoT e rimanere in ascolto dei messaggi da cloud a dispositivo inviati dall'hub:</span><span class="sxs-lookup"><span data-stu-id="50813-155">At a command prompt in the simulated-device folder, run the following command to begin sending telemetry to your IoT hub and to listen for cloud-to-device messages sent from your hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Eseguire un'app di dispositivo simulato][img-simulated-device]

2. <span data-ttu-id="50813-157">A un prompt dei comandi nella cartella send-c2d-messages eseguire questo comando per inviare un messaggio da cloud a dispositivo e attendere un acknowledgment di feedback:</span><span class="sxs-lookup"><span data-stu-id="50813-157">At a command prompt in the send-c2d-messages folder, run the following command to send a cloud-to-device message and wait for a feedback acknowledgment:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Eseguire il comando per inviare il messaggio dal cloud al dispositivo][img-send-command]

## <a name="next-steps"></a><span data-ttu-id="50813-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="50813-159">Next steps</span></span>

<span data-ttu-id="50813-160">In questa esercitazione è stato descritto come inviare e ricevere messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="50813-160">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="50813-161">Per avere degli esempi di soluzioni complete che utilizzano l'hub IoT, vedere la [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="50813-161">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="50813-162">Per altre informazioni sullo sviluppo delle soluzioni con l'hub IoT, vedere la [Guida per sviluppatori dell'hub IoT].</span><span class="sxs-lookup"><span data-stu-id="50813-162">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-java-java-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-java-java-c2d/sendc2d.png
<!-- Links -->

<span data-ttu-id="50813-163">[Introduzione all'hub IoT di Azure]: iot-hub-java-java-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="50813-163">[Get started with IoT Hub]: iot-hub-java-java-getstarted.md</span></span>
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
<span data-ttu-id="50813-164">[Guida per sviluppatori dell'hub IoT]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="50813-164">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="50813-165">[Centro per sviluppatori Azure IoT]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="50813-165">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java
<span data-ttu-id="50813-166">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="50813-166">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="50813-167">[portale di Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="50813-167">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="50813-168">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span><span class="sxs-lookup"><span data-stu-id="50813-168">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span></span>
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22