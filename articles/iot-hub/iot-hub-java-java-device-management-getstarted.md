---
title: aaaGet avviato con la gestione dei dispositivi Azure IoT Hub (linguaggio) | Documenti Microsoft
description: Come tooinitiate di gestione dispositivi Azure IoT Hub toouse un dispositivo remoto riavviare il computer. Usare il dispositivo di Azure IoT hello SDK per Java tooimplement un'app dispositivo simulato che include un metodo diretto e hello Azure IoT servizio SDK per Java tooimplement un'applicazione di servizio che richiama metodo diretto hello.
services: iot-hub
documentationcenter: .java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 7aaeda9d4ff7002e5c66adfd61e2dfd5bcea964f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="0f358-104">Introduzione alla gestione dei dispositivi (Java)</span><span class="sxs-lookup"><span data-stu-id="0f358-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="0f358-105">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="0f358-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="0f358-106">Utilizzare hello toocreate portale Azure un IoT Hub e creare un'identità del dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0f358-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="0f358-107">Creare un'app dispositivo simulato che implementa un dispositivo di hello tooreboot dirette del metodo.</span><span class="sxs-lookup"><span data-stu-id="0f358-107">Create a simulated device app that implements a direct method tooreboot hello device.</span></span> <span data-ttu-id="0f358-108">Diretti metodi vengono richiamati dal cloud hello.</span><span class="sxs-lookup"><span data-stu-id="0f358-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="0f358-109">Creare un'applicazione che richiama hello riavvio dirette del metodo nell'app dispositivo simulato hello tramite l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="0f358-109">Create an app that invokes hello reboot direct method in hello simulated device app through your IoT hub.</span></span> <span data-ttu-id="0f358-110">Questa app quindi monitoraggi hello proprietà segnalate da hello dispositivo toosee al termine dell'operazione di riavvio hello.</span><span class="sxs-lookup"><span data-stu-id="0f358-110">This app then monitors hello reported properties from hello device toosee when hello reboot operation is complete.</span></span>

<span data-ttu-id="0f358-111">Alla fine di hello di questa esercitazione, si dispongono di due applicazioni di console Java:</span><span class="sxs-lookup"><span data-stu-id="0f358-111">At hello end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="0f358-112">**simulated-device**.</span><span class="sxs-lookup"><span data-stu-id="0f358-112">**simulated-device**.</span></span> <span data-ttu-id="0f358-113">Questa app:</span><span class="sxs-lookup"><span data-stu-id="0f358-113">This app:</span></span>

* <span data-ttu-id="0f358-114">Collega l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="0f358-114">Connects tooyour IoT hub with hello device identity created earlier.</span></span>
* <span data-ttu-id="0f358-115">Riceve una chiamata del metodo diretto per il riavvio.</span><span class="sxs-lookup"><span data-stu-id="0f358-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="0f358-116">Simula un riavvio fisico.</span><span class="sxs-lookup"><span data-stu-id="0f358-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="0f358-117">Report hello ora dell'ultimo riavvio di hello tramite una proprietà segnalato.</span><span class="sxs-lookup"><span data-stu-id="0f358-117">Reports hello time of hello last reboot through a reported property.</span></span>

<span data-ttu-id="0f358-118">**trigger-reboot**.</span><span class="sxs-lookup"><span data-stu-id="0f358-118">**trigger-reboot**.</span></span> <span data-ttu-id="0f358-119">Questa app:</span><span class="sxs-lookup"><span data-stu-id="0f358-119">This app:</span></span>

* <span data-ttu-id="0f358-120">Chiama un metodo diretto in app dispositivo simulato hello.</span><span class="sxs-lookup"><span data-stu-id="0f358-120">Calls a direct method in hello simulated device app.</span></span>
* <span data-ttu-id="0f358-121">Visualizza chiamate dirette del metodo di hello risposta toohello inviata dal dispositivo simulato hello</span><span class="sxs-lookup"><span data-stu-id="0f358-121">Displays hello response toohello direct method call sent by hello simulated device</span></span>
* <span data-ttu-id="0f358-122">Hello Visualizza aggiornato segnalato proprietà.</span><span class="sxs-lookup"><span data-stu-id="0f358-122">Displays hello updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="0f358-123">Per informazioni su hello SDK che è possibile utilizzare toobuild toorun di applicazioni in dispositivi e la soluzione di back-end, vedere [Azure IoT SDK][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="0f358-123">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="0f358-124">toocomplete questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="0f358-124">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="0f358-125">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="0f358-125">Java SE 8.</span></span> <br/> <span data-ttu-id="0f358-126">[Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall Java per questa esercitazione su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="0f358-126">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="0f358-127">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="0f358-127">Maven 3.</span></span>  <br/> <span data-ttu-id="0f358-128">[Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall [Maven] [ lnk-maven] per questa esercitazione su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="0f358-128">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="0f358-129">[Versione di Node.js: 0.10.0 o successiva](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="0f358-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="0f358-130">Attivare un riavvio remoto nel dispositivo hello utilizzando un metodo diretto</span><span class="sxs-lookup"><span data-stu-id="0f358-130">Trigger a remote reboot on hello device using a direct method</span></span>

<span data-ttu-id="0f358-131">In questa sezione si crea un'app console Java che:</span><span class="sxs-lookup"><span data-stu-id="0f358-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="0f358-132">Richiama metodo diretto di riavvio hello in app dispositivo simulato hello.</span><span class="sxs-lookup"><span data-stu-id="0f358-132">Invokes hello reboot direct method in hello simulated device app.</span></span>
1. <span data-ttu-id="0f358-133">Visualizza la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="0f358-133">Displays hello response.</span></span>
1. <span data-ttu-id="0f358-134">Hello polling segnalato proprietà inviate da hello dispositivo toodetermine quando hello riavvio è completo.</span><span class="sxs-lookup"><span data-stu-id="0f358-134">Polls hello reported properties sent from hello device toodetermine when hello reboot is complete.</span></span>

<span data-ttu-id="0f358-135">Questa app console si connette tooyour IoT Hub tooinvoke hello dirette del metodo e lettura hello segnalati proprietà.</span><span class="sxs-lookup"><span data-stu-id="0f358-135">This console app connects tooyour IoT Hub tooinvoke hello direct method and read hello reported properties.</span></span>

1. <span data-ttu-id="0f358-136">Creare una cartella vuota denominata dm-get-started.</span><span class="sxs-lookup"><span data-stu-id="0f358-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="0f358-137">Nella cartella di avvio get dm hello, creare un progetto di Maven denominato **trigger riavvio** utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="0f358-137">In hello dm-get-started folder, create a Maven project called **trigger-reboot** using hello following command at your command prompt.</span></span> <span data-ttu-id="0f358-138">Hello seguito è riportato un comando singolo, condizione:</span><span class="sxs-lookup"><span data-stu-id="0f358-138">hello following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="0f358-139">Al prompt dei comandi, passare toohello trigger riavvio cartella.</span><span class="sxs-lookup"><span data-stu-id="0f358-139">At your command prompt, navigate toohello trigger-reboot folder.</span></span>

1. <span data-ttu-id="0f358-140">Utilizzando un editor di testo, aprire hello pom.xml file nella cartella di trigger richiede il riavvio di hello e aggiungere hello seguente dipendenza toohello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="0f358-140">Using a text editor, open hello pom.xml file in hello trigger-reboot folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="0f358-141">Questa dipendenza consente si toouse hello client di servizi iot pacchetto in toocommunicate l'app con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="0f358-141">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="0f358-142">È possibile verificare la versione più recente di hello di **client di servizi iot** utilizzando [ricerca Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="0f358-142">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="0f358-143">Aggiungere il seguente hello **compilare** nodo dopo hello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="0f358-143">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="0f358-144">Questa configurazione indica Maven toouse Java toobuild 1.8 hello app:</span><span class="sxs-lookup"><span data-stu-id="0f358-144">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. <span data-ttu-id="0f358-145">Salvare e chiudere il file di pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="0f358-145">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="0f358-146">Utilizzando un editor di testo, aprire file di origine trigger-reboot\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="0f358-146">Using a text editor, open hello trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="0f358-147">Aggiungere il seguente hello **importare** file toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="0f358-147">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwin;
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

1. <span data-ttu-id="0f358-148">Aggiungere hello seguenti variabili a livello di classe toohello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="0f358-148">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="0f358-149">Sostituire `{youriothubconnectionstring}` con la stringa di connessione hub IoT è stata annotata nella hello *creare un IoT Hub* sezione:</span><span class="sxs-lookup"><span data-stu-id="0f358-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="0f358-150">un thread che legge hello tooimplement segnalati proprietà da un doppio dispositivo hello ogni 10 secondi, aggiungere il seguente di hello annidati classe toohello **App** classe:</span><span class="sxs-lookup"><span data-stu-id="0f358-150">tooimplement a thread that reads hello reported properties from hello device twin every 10 seconds, add hello following nested class toohello **App** class:</span></span>

    ```java
    private static class ShowReportedProperties implements Runnable {
      public void run() {
        try {
          DeviceTwin deviceTwins = DeviceTwin.createFromConnectionString(iotHubConnectionString);
          DeviceTwinDevice twinDevice = new DeviceTwinDevice(deviceId);
          while (true) {
            System.out.println("Get reported properties from device twin");
            deviceTwins.getTwin(twinDevice);
            System.out.println(twinDevice.reportedPropertiesToString());
            Thread.sleep(10000);
          }
        } catch (Exception ex) {
          System.out.println("Exception reading reported properties: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="0f358-151">metodo diretto tooinvoke hello riavvio nel dispositivo simulato hello, aggiungere hello seguente codice toohello **principale** metodo:</span><span class="sxs-lookup"><span data-stu-id="0f358-151">tooinvoke hello reboot direct method on hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
      System.out.println("Invoke reboot direct method");
      MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, null);

      if(result == null)
      {
        throw new IOException("Invoke direct method reboot returns null");
      }
      System.out.println("Invoked reboot on device");
      System.out.println("Status for device:   " + result.getStatus());
      System.out.println("Message from device: " + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="0f358-152">toostart hello thread toopoll hello proprietà segnalate dal dispositivo simulato hello, aggiungere hello seguente codice toohello **principale** metodo:</span><span class="sxs-lookup"><span data-stu-id="0f358-152">toostart hello thread toopoll hello reported properties from hello simulated device, add hello following code toohello **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="0f358-153">tooenable è toostop hello app, aggiungere hello seguente codice toohello **principale** metodo:</span><span class="sxs-lookup"><span data-stu-id="0f358-153">tooenable you toostop hello app, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="0f358-154">Salvare e chiudere il file di trigger-reboot\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="0f358-154">Save and close hello trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="0f358-155">Compilare hello **trigger riavvio** app back-end e correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="0f358-155">Build hello **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="0f358-156">Al prompt dei comandi, passare toohello trigger riavvio cartella e hello esecuzione comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0f358-156">At your command prompt, navigate toohello trigger-reboot folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="0f358-157">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="0f358-157">Create a simulated device app</span></span>

<span data-ttu-id="0f358-158">In questa sezione si crea un'app console Java che simula un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0f358-158">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="0f358-159">app Hello è in attesa di una chiamata al metodo diretta hello riavvio dall'hub IoT e risponde immediatamente toothat chiamata.</span><span class="sxs-lookup"><span data-stu-id="0f358-159">hello app listens for hello reboot direct method call from your IoT hub and immediately responds toothat call.</span></span> <span data-ttu-id="0f358-160">Hello app quindi inattivo per un periodo di tempo processo di riavvio hello toosimulate prima di utilizzare un hello toonotify proprietà segnalati **trigger riavvio** app back-end che hello riavvio è stata completata.</span><span class="sxs-lookup"><span data-stu-id="0f358-160">hello app then sleeps for a while toosimulate hello reboot process before it uses a reported property toonotify hello **trigger-reboot** back-end app that hello reboot is complete.</span></span>

1. <span data-ttu-id="0f358-161">Nella cartella di avvio get dm hello, creare un progetto di Maven denominato **dispositivo simulato** utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="0f358-161">In hello dm-get-started folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="0f358-162">di seguito Hello è un comando singolo, condizione:</span><span class="sxs-lookup"><span data-stu-id="0f358-162">hello following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="0f358-163">Al prompt dei comandi, passare cartella dispositivo simulato toohello.</span><span class="sxs-lookup"><span data-stu-id="0f358-163">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="0f358-164">Utilizzando un editor di testo, di aprire file pom.xml hello nella cartella dispositivo simulato hello e aggiungere hello seguente dipendenza toohello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="0f358-164">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="0f358-165">Questa dipendenza consente si toouse hello client di servizi iot pacchetto in toocommunicate l'app con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="0f358-165">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="0f358-166">È possibile verificare la versione più recente di hello di **client di dispositivi iot** utilizzando [ricerca Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="0f358-166">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="0f358-167">Aggiungere il seguente hello **compilare** nodo dopo hello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="0f358-167">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="0f358-168">Questa configurazione indica Maven toouse Java toobuild 1.8 hello app:</span><span class="sxs-lookup"><span data-stu-id="0f358-168">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.3</version>
          <configuration>
            <source>1.8</source>
            <target>1.8</target>
          </configuration>
        </plugin>
      </plugins>
    </build>
    ```

1. <span data-ttu-id="0f358-169">Salvare e chiudere il file di pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="0f358-169">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="0f358-170">Utilizzando un editor di testo, aprire file di origine simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="0f358-170">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="0f358-171">Aggiungere il seguente hello **importare** file toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="0f358-171">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.time.LocalDateTime;
    import java.util.Scanner;
    import java.util.Set;
    import java.util.HashSet;
    ```

1. <span data-ttu-id="0f358-172">Aggiungere hello seguenti variabili a livello di classe toohello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="0f358-172">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="0f358-173">Sostituire `{yourdeviceconnectionstring}` con stringa di connessione dispositivo hello annotato nel hello *creare un'identità del dispositivo* sezione:</span><span class="sxs-lookup"><span data-stu-id="0f358-173">Replace `{yourdeviceconnectionstring}` with hello device connection string you noted in hello *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="0f358-174">tooimplement un gestore di callback per gli eventi di stato dirette del metodo, aggiungere il seguente di hello annidati classe toohello **App** classe:</span><span class="sxs-lookup"><span data-stu-id="0f358-174">tooimplement a callback handler for direct method status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="0f358-175">tooimplement un gestore di callback per gli eventi dello stato di dispositivo doppi, aggiungere il seguente di hello annidati classe toohello **App** classe:</span><span class="sxs-lookup"><span data-stu-id="0f358-175">tooimplement a callback handler for device twin status events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="0f358-176">tooimplement un gestore di callback per gli eventi di proprietà, aggiungere il seguente hello annidati classe toohello **App** classe:</span><span class="sxs-lookup"><span data-stu-id="0f358-176">tooimplement a callback handler for property events, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class PropertyCallback implements PropertyCallBack<String, String>
    {
      public void PropertyCall(String propertyKey, String propertyValue, Object context)
      {
        System.out.println("PropertyKey:     " + propertyKey);
        System.out.println("PropertyKvalue:  " + propertyKey);
      }
    }
    ```

1. <span data-ttu-id="0f358-177">tooimplement un thread toosimulate hello il riavvio del dispositivo, aggiungere il seguente hello annidati classe toohello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="0f358-177">tooimplement a thread toosimulate hello device reboot, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="0f358-178">thread di Hello rimane inattivo per cinque secondi e quindi imposta hello **lastReboot** segnalati proprietà:</span><span class="sxs-lookup"><span data-stu-id="0f358-178">hello thread sleeps for five seconds and then sets hello **lastReboot** reported property:</span></span>

    ```java
    protected static class RebootDeviceThread implements Runnable {
      public void run() {
        try {
          System.out.println("Rebooting...");
          Thread.sleep(5000);
          Property property = new Property("lastReboot", LocalDateTime.now());
          Set<Property> properties = new HashSet<Property>();
          properties.add(property);
          client.sendReportedProperties(properties);
          System.out.println("Rebooted");
        }
        catch (Exception ex) {
          System.out.println("Exception in reboot thread: " + ex.getMessage());
        }
      }
    }
    ```

1. <span data-ttu-id="0f358-179">tooimplement hello dirette del metodo sul dispositivo hello, aggiungere il seguente hello annidati classe toohello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="0f358-179">tooimplement hello direct method on hello device, add hello following nested class toohello **App** class.</span></span> <span data-ttu-id="0f358-180">Quando applicazione simulata hello riceve una chiamata toohello **riavviare** dirette del metodo, viene restituito un chiamante toohello acknowledgement e avvia un hello tooprocess thread riavviare:</span><span class="sxs-lookup"><span data-stu-id="0f358-180">When hello simulated app receives a call toohello **reboot** direct method, it returns an acknowledgement toohello caller and then starts a thread tooprocess hello reboot:</span></span>

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "reboot" :
          {
            int status = METHOD_SUCCESS;
            System.out.println("Received reboot request");
            deviceMethodData = new DeviceMethodData(status, "Started reboot");
            RebootDeviceThread rebootThread = new RebootDeviceThread();
            Thread t = new Thread(rebootThread);
            t.start();
            break;
          }
          default:
          {
            int status = METHOD_NOT_DEFINED;
            deviceMethodData = new DeviceMethodData(status, "Not defined direct method " + methodName);
          }
        }
        return deviceMethodData;
      }
    }
    ```

1. <span data-ttu-id="0f358-181">Modificare la firma hello di hello **principale** hello toothrow metodo le eccezioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0f358-181">Modify hello signature of hello **main** method toothrow hello following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="0f358-182">tooinstantiate un **DeviceClient**, aggiungere hello seguente codice toohello **principale** metodo:</span><span class="sxs-lookup"><span data-stu-id="0f358-182">tooinstantiate a **DeviceClient**, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="0f358-183">toostart in attesa di chiamate dirette del metodo, aggiungere hello seguente codice toohello **principale** metodo:</span><span class="sxs-lookup"><span data-stu-id="0f358-183">toostart listening for direct method calls, add hello following code toohello **main** method:</span></span>

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed toodirect methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="0f358-184">tooshut verso il basso il simulatore di dispositivi hello, aggiungere hello seguente codice toohello **principale** metodo:</span><span class="sxs-lookup"><span data-stu-id="0f358-184">tooshut down hello device simulator, add hello following code toohello **main** method:</span></span>

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="0f358-185">Salvare e chiudere il file di simulated-device\src\main\java\com\mycompany\app\App.java hello.</span><span class="sxs-lookup"><span data-stu-id="0f358-185">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="0f358-186">Compilare hello **dispositivo simulato** app back-end e correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="0f358-186">Build hello **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="0f358-187">Al prompt dei comandi, passare cartella dispositivo simulato toohello e hello esecuzione comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0f358-187">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="0f358-188">Eseguire App hello</span><span class="sxs-lookup"><span data-stu-id="0f358-188">Run hello apps</span></span>

<span data-ttu-id="0f358-189">Si è ora pronto toorun hello app.</span><span class="sxs-lookup"><span data-stu-id="0f358-189">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="0f358-190">Al prompt dei comandi nella cartella dispositivo simulato hello eseguire hello in ascolto per le chiamate di metodo di riavvio dall'hub IoT toobegin di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="0f358-190">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub Java simulato dispositivo app toolisten per chiamate dirette del metodo di riavvio][1]

1. <span data-ttu-id="0f358-192">Al prompt dei comandi nella cartella trigger richiede il riavvio di hello eseguire hello seguente metodo di riavvio hello toocall comando sul dispositivo simulato dall'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="0f358-192">At a command prompt in hello trigger-reboot folder, run hello following command toocall hello reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Hello toocall app del servizio di linguaggio IoT Hub dirette del metodo di riavvio][2]

1. <span data-ttu-id="0f358-194">dispositivo simulato Hello risponde chiamata al metodo diretto toohello riavvio:</span><span class="sxs-lookup"><span data-stu-id="0f358-194">hello simulated device responds toohello reboot direct method call:</span></span>

    ![IoT Hub Java dispositivo simulato app risponde chiamata al metodo diretto toohello][3]

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[1]: ./media/iot-hub-java-java-device-management-getstarted/launchsimulator.png
[2]: ./media/iot-hub-java-java-device-management-getstarted/triggerreboot.png
[3]: ./media/iot-hub-java-java-device-management-getstarted/respondtoreboot.png
<!-- Links -->

[lnk-maven]: https://maven.apache.org/what-is-maven.html

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22