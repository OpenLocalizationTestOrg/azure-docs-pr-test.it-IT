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
# <a name="send-cloud-to-device-messages-with-iot-hub-java"></a><span data-ttu-id="28f95-104">Inviare messaggi da cloud a dispositivo con l'hub IoT (Java)</span><span class="sxs-lookup"><span data-stu-id="28f95-104">Send cloud-to-device messages with IoT Hub (Java)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

<span data-ttu-id="28f95-105">L'hub IoT di Azure è un servizio completamente gestito che consente di abilitare comunicazioni bidirezionali affidabili e sicure tra milioni di dispositivi e un back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="28f95-105">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="28f95-106">Hello [iniziare con l'IoT Hub] esercitazione viene illustrato come eseguire il provisioning di un'identità del dispositivo in essa contenuti, toocreate un hub IoT e codice di un'app dispositivo simulato che invia messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="28f95-106">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="28f95-107">Questa esercitazione si basa su [iniziare con l'IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="28f95-107">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="28f95-108">Illustra le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="28f95-108">It shows you how to:</span></span>

* <span data-ttu-id="28f95-109">Dal back-end soluzione, inviare singolo dispositivo tooa messaggi da cloud a dispositivo tramite l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="28f95-109">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="28f95-110">Ricevere messaggi da cloud a dispositivo in un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="28f95-110">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="28f95-111">Dal back-end soluzione, richiedere la conferma di recapito (*feedback*) per i messaggi inviati tooa dispositivo dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="28f95-111">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="28f95-112">Sono disponibili ulteriori informazioni sui cloud a dispositivo messaggi hello [Guida per sviluppatori di IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="28f95-112">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="28f95-113">Alla fine di hello di questa esercitazione, si esegue due applicazioni di console Java:</span><span class="sxs-lookup"><span data-stu-id="28f95-113">At hello end of this tutorial, you run two Java console apps:</span></span>

* <span data-ttu-id="28f95-114">**dispositivo simulato**, una versione modificata dell'applicazione hello creato in [iniziare con l'IoT Hub], che si connette l'hub IoT tooyour e riceve messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="28f95-114">**simulated-device**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="28f95-115">**inviare messaggi di c2d**, che invia un'app di dispositivo simulato toohello messaggio cloud a dispositivo tramite l'IoT Hub e quindi riceve la conferma di recapito.</span><span class="sxs-lookup"><span data-stu-id="28f95-115">**send-c2d-messages**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="28f95-116">L’hub IoT dispone del supporto SDK per molte piattaforme e linguaggi (inclusi C, Java e Javascript) tramite gli SDK del dispositivo IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="28f95-116">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="28f95-117">Per istruzioni dettagliate su come tooconnect l'esercitazione toothis dispositivo codice e in genere tooAzure IoT Hub, vedere hello [Centro per sviluppatori di Azure IoT].</span><span class="sxs-lookup"><span data-stu-id="28f95-117">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>

<span data-ttu-id="28f95-118">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="28f95-118">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="28f95-119">Una versione completa di utilizzo di hello [iniziare con l'IoT Hub](iot-hub-java-java-getstarted.md) o [messaggi da dispositivo a cloud IoT Hub processo](iot-hub-java-java-process-d2c.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="28f95-119">A complete working version of hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) or [Process IoT Hub device-to-cloud messages](iot-hub-java-java-process-d2c.md) tutorial.</span></span>
* <span data-ttu-id="28f95-120">versione più recente Hello [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="28f95-120">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="28f95-121">Maven 3</span><span class="sxs-lookup"><span data-stu-id="28f95-121">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="28f95-122">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="28f95-122">An active Azure account.</span></span> <span data-ttu-id="28f95-123">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="28f95-123">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="28f95-124">Ricezione di messaggi hello dispositivo simulato App</span><span class="sxs-lookup"><span data-stu-id="28f95-124">Receive messages in hello simulated device app</span></span>

<span data-ttu-id="28f95-125">In questa sezione, si modifica hello dispositivo simulato app è stato creato in [iniziare con l'IoT Hub] tooreceive di messaggi da cloud a dispositivo dall'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="28f95-125">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="28f95-126">Per aprire il file di simulated-device\src\main\java\com\mycompany\app\App.java hello, utilizzando un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="28f95-126">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

2. <span data-ttu-id="28f95-127">Aggiungere il seguente hello **MessageCallback** classe come una classe annidata all'interno di hello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="28f95-127">Add hello following **MessageCallback** class as a nested class inside hello **App** class.</span></span> <span data-ttu-id="28f95-128">Hello **eseguire** metodo viene richiamato quando il dispositivo hello riceve un messaggio dall'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="28f95-128">hello **execute** method is invoked when hello device receives a message from IoT Hub.</span></span> <span data-ttu-id="28f95-129">In questo esempio, il dispositivo hello sempre notifica hub IoT hello completamento messaggio hello:</span><span class="sxs-lookup"><span data-stu-id="28f95-129">In this example, hello device always notifies hello IoT hub that it has completed hello message:</span></span>

    ```java
    private static class AppMessageCallback implements MessageCallback {
      public IotHubMessageResult execute(Message msg, Object context) {
        System.out.println("Received message from hub: "
          + new String(msg.getBytes(), Message.DEFAULT_IOTHUB_MESSAGE_CHARSET));
    
        return IotHubMessageResult.COMPLETE;
      }
    }
    ```
3. <span data-ttu-id="28f95-130">Modificare hello **principale** metodo toocreate un **AppMessageCallback** hello istanza e chiamare **setMessageCallback** metodo prima dell'apertura client hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="28f95-130">Modify hello **main** method toocreate an **AppMessageCallback** instance and call hello **setMessageCallback** method before it opens hello client as follows:</span></span>

    ```java
    client = new DeviceClient(connString, protocol);
   
    MessageCallback callback = new AppMessageCallback();
    client.setMessageCallback(callback, null);
    client.open();
    ```

    > [!NOTE]
    > <span data-ttu-id="28f95-131">Se si Usa HTTP invece di MQTT o AMQP come trasporto hello, hello **DeviceClient** istanza verifica la presenza di messaggi dall'IoT Hub raramente (meno di 25 minuti).</span><span class="sxs-lookup"><span data-stu-id="28f95-131">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="28f95-132">Per ulteriori informazioni sulle differenze hello supporto MQTT, AMQP e HTTP e la limitazione delle richieste di Hub IoT, vedere hello [Guida per sviluppatori di IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="28f95-132">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

4. <span data-ttu-id="28f95-133">hello toobuild **dispositivo simulato** app usando Maven, eseguire hello comando al prompt dei comandi di hello nella cartella dispositivo simulato hello seguente:</span><span class="sxs-lookup"><span data-stu-id="28f95-133">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="28f95-134">Inviare un messaggio da cloud a dispositivo</span><span class="sxs-lookup"><span data-stu-id="28f95-134">Send a cloud-to-device message</span></span>

<span data-ttu-id="28f95-135">In questa sezione si crea un'applicazione console Java che invia messaggi da cloud a dispositivo toohello dispositivo simulato app.</span><span class="sxs-lookup"><span data-stu-id="28f95-135">In this section, you create a Java console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="28f95-136">È necessario hello ID dispositivo del dispositivo hello aggiunto nel hello [iniziare con l'IoT Hub] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="28f95-136">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="28f95-137">È inoltre necessario hello stringa di connessione IoT Hub per l'hub che è possibile trovare nel hello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="28f95-137">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="28f95-138">Creare un progetto di Maven denominato **inviare messaggi di c2d** utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="28f95-138">Create a Maven project called **send-c2d-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="28f95-139">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="28f95-139">Note this command is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=send-c2d-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="28f95-140">Al prompt dei comandi, passare toohello nuova cartella di trasmissione-c2d-messaggi.</span><span class="sxs-lookup"><span data-stu-id="28f95-140">At your command prompt, navigate toohello new send-c2d-messages folder.</span></span>

3. <span data-ttu-id="28f95-141">Utilizzando un editor di testo, di aprire file pom.xml hello nella cartella di trasmissione-c2d-messaggi hello e aggiungere hello seguente dipendenza toohello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="28f95-141">Using a text editor, open hello pom.xml file in hello send-c2d-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="28f95-142">Aggiunta della dipendenza hello consente hello toouse **client del servizio di linguaggio hub IOT** pacchetto in toocommunicate l'applicazione con il servizio di hub IoT:</span><span class="sxs-lookup"><span data-stu-id="28f95-142">Adding hello dependency enables you toouse hello **iothub-java-service-client** package in your application toocommunicate with your IoT hub service:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="28f95-143">È possibile verificare la versione più recente di hello di **client di servizi iot** utilizzando [ricerca Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="28f95-143">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="28f95-144">Salvare e chiudere il file di pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="28f95-144">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="28f95-145">Per aprire il file di send-c2d-messages\src\main\java\com\mycompany\app\App.java hello, utilizzando un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="28f95-145">Using a text editor, open hello send-c2d-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="28f95-146">Aggiungere il seguente hello **importare** file toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="28f95-146">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.*;
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="28f95-147">Aggiungere hello seguenti variabili a livello di classe toohello **App** classe, sostituendo **{yourhubconnectionstring}** e **{yourdeviceid}** con hello i valori del tipo indicato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="28f95-147">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** and **{yourdeviceid}** with hello values your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "{yourdeviceid}";
    private static final IotHubServiceClientProtocol protocol = IotHubServiceClientProtocol.AMQPS;
    ```

8. <span data-ttu-id="28f95-148">Sostituire hello **principale** metodo con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="28f95-148">Replace hello **main** method with hello following code.</span></span> <span data-ttu-id="28f95-149">Questo codice si connette l'hub IoT tooyour, invia un dispositivo tooyour messaggio e quindi attende un acknowledgement messaggio hello dispositivo hello ricevuti ed elaborati:</span><span class="sxs-lookup"><span data-stu-id="28f95-149">This code connects tooyour IoT hub, sends a message tooyour device, and then waits for an acknowledgment that hello device received and processed hello message:</span></span>
   
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
    > <span data-ttu-id="28f95-150">Per semplicità, in questa esercitazione non si implementa alcun criterio di nuovi tentativi.</span><span class="sxs-lookup"><span data-stu-id="28f95-150">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="28f95-151">Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei].</span><span class="sxs-lookup"><span data-stu-id="28f95-151">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>


9. <span data-ttu-id="28f95-152">hello toobuild **dispositivo simulato** app usando Maven, eseguire hello comando al prompt dei comandi di hello nella cartella dispositivo simulato hello seguente:</span><span class="sxs-lookup"><span data-stu-id="28f95-152">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="run-hello-applications"></a><span data-ttu-id="28f95-153">Eseguire applicazioni hello</span><span class="sxs-lookup"><span data-stu-id="28f95-153">Run hello applications</span></span>

<span data-ttu-id="28f95-154">Si è ora applicazioni hello toorun pronto.</span><span class="sxs-lookup"><span data-stu-id="28f95-154">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="28f95-155">Al prompt dei comandi nella cartella dispositivo simulato hello eseguire hello dopo l'invio di hub IoT di telemetria tooyour e toolisten per i messaggi da cloud a dispositivo inviati dall'hub di toobegin di comando:</span><span class="sxs-lookup"><span data-stu-id="28f95-155">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry tooyour IoT hub and toolisten for cloud-to-device messages sent from your hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Eseguire app dispositivo simulato hello][img-simulated-device]

2. <span data-ttu-id="28f95-157">Al prompt dei comandi nella cartella di trasmissione-c2d-messaggi hello eseguire hello successivo comando toosend un messaggio di cloud a dispositivo e l'attesa per un riconoscimento di commenti e suggerimenti:</span><span class="sxs-lookup"><span data-stu-id="28f95-157">At a command prompt in hello send-c2d-messages folder, run hello following command toosend a cloud-to-device message and wait for a feedback acknowledgment:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Eseguire il messaggio da cloud a dispositivo hello di hello comando toosend][img-send-command]

## <a name="next-steps"></a><span data-ttu-id="28f95-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="28f95-159">Next steps</span></span>

<span data-ttu-id="28f95-160">In questa esercitazione, si è appreso come toosend e ricevere messaggi da cloud a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="28f95-160">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="28f95-161">esempi di toosee di soluzioni end-to-end completate che usa IoT Hub, vedere [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="28f95-161">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="28f95-162">toolearn più sullo sviluppo di soluzioni con l'IoT Hub, vedere hello [Guida per sviluppatori di IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="28f95-162">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

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