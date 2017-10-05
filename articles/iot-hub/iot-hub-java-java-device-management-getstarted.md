---
title: Introduzione alla gestione dei dispositivi dell'hub IoT di Azure (Java) | Microsoft Docs
description: Come usare la gestione dei dispositivi dell'hub IoT di Azure per riavviare un dispositivo remoto. Usare Azure IoT SDK per dispositivi per Java per implementare un'app per dispositivo simulato che include un metodo diretto e Azure IoT SDK per servizi per Java per implementare un'app del servizio che richiama il metodo diretto.
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
ms.openlocfilehash: c75635f366f5ced4bf91792d1a905dd6aab8ed79
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-device-management-java"></a><span data-ttu-id="80d7f-104">Introduzione alla gestione dei dispositivi (Java)</span><span class="sxs-lookup"><span data-stu-id="80d7f-104">Get started with device management (Java)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="80d7f-105">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="80d7f-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="80d7f-106">Creare un hub IoT nel portale di Azure e un'identità del dispositivo nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="80d7f-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="80d7f-107">Creare un'app per dispositivo simulato che implementa un metodo diretto per riavviare il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="80d7f-107">Create a simulated device app that implements a direct method to reboot the device.</span></span> <span data-ttu-id="80d7f-108">I metodi diretti vengono richiamati dal cloud.</span><span class="sxs-lookup"><span data-stu-id="80d7f-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="80d7f-109">Creare un'app che richiama il metodo diretto di riavvio nell'app per dispositivo simulato tramite l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="80d7f-109">Create an app that invokes the reboot direct method in the simulated device app through your IoT hub.</span></span> <span data-ttu-id="80d7f-110">Questa app controlla quindi le proprietà segnalate dal dispositivo per vedere quando l'operazione di riavvio viene completata.</span><span class="sxs-lookup"><span data-stu-id="80d7f-110">This app then monitors the reported properties from the device to see when the reboot operation is complete.</span></span>

<span data-ttu-id="80d7f-111">Al termine di questa esercitazione si avranno due app di console Java:</span><span class="sxs-lookup"><span data-stu-id="80d7f-111">At the end of this tutorial, you have two Java console apps:</span></span>

<span data-ttu-id="80d7f-112">**simulated-device**.</span><span class="sxs-lookup"><span data-stu-id="80d7f-112">**simulated-device**.</span></span> <span data-ttu-id="80d7f-113">Questa app:</span><span class="sxs-lookup"><span data-stu-id="80d7f-113">This app:</span></span>

* <span data-ttu-id="80d7f-114">Si connette all'hub IoT con l'identità del dispositivo creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="80d7f-114">Connects to your IoT hub with the device identity created earlier.</span></span>
* <span data-ttu-id="80d7f-115">Riceve una chiamata del metodo diretto per il riavvio.</span><span class="sxs-lookup"><span data-stu-id="80d7f-115">Receives a reboot direct method call.</span></span>
* <span data-ttu-id="80d7f-116">Simula un riavvio fisico.</span><span class="sxs-lookup"><span data-stu-id="80d7f-116">Simulates a physical reboot.</span></span>
* <span data-ttu-id="80d7f-117">Segnala l'ora dell'ultimo riavvio con una proprietà segnalata.</span><span class="sxs-lookup"><span data-stu-id="80d7f-117">Reports the time of the last reboot through a reported property.</span></span>

<span data-ttu-id="80d7f-118">**trigger-reboot**.</span><span class="sxs-lookup"><span data-stu-id="80d7f-118">**trigger-reboot**.</span></span> <span data-ttu-id="80d7f-119">Questa app:</span><span class="sxs-lookup"><span data-stu-id="80d7f-119">This app:</span></span>

* <span data-ttu-id="80d7f-120">Chiama un metodo diretto nell'app per dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="80d7f-120">Calls a direct method in the simulated device app.</span></span>
* <span data-ttu-id="80d7f-121">Mostra la risposta alla chiamata del metodo diretto inviata dal dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="80d7f-121">Displays the response to the direct method call sent by the simulated device</span></span>
* <span data-ttu-id="80d7f-122">Consente di visualizzare le proprietà segnalate aggiornate.</span><span class="sxs-lookup"><span data-stu-id="80d7f-122">Displays the updated reported properties.</span></span>

> [!NOTE]
> <span data-ttu-id="80d7f-123">Per informazioni sugli SDK che consentono di compilare le applicazioni da eseguire nei dispositivi e i back-end della soluzione, vedere [Azure IoT SDK][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="80d7f-123">For information about the SDKs that you can use to build applications to run on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="80d7f-124">Per completare questa esercitazione, sono necessari:</span><span class="sxs-lookup"><span data-stu-id="80d7f-124">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="80d7f-125">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="80d7f-125">Java SE 8.</span></span> <br/> <span data-ttu-id="80d7f-126">[Preparare l'ambiente di sviluppo][lnk-dev-setup] descrive come installare Java per questa esercitazione in Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="80d7f-126">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="80d7f-127">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="80d7f-127">Maven 3.</span></span>  <br/> <span data-ttu-id="80d7f-128">[Preparare l'ambiente di sviluppo][lnk-dev-setup] descrive come installare [Maven][lnk-maven] per questa esercitazione in Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="80d7f-128">[Prepare your development environment][lnk-dev-setup] describes how to install [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="80d7f-129">[Versione di Node.js: 0.10.0 o successiva](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="80d7f-129">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="80d7f-130">Attivare un riavvio remoto nel dispositivo con un metodo diretto</span><span class="sxs-lookup"><span data-stu-id="80d7f-130">Trigger a remote reboot on the device using a direct method</span></span>

<span data-ttu-id="80d7f-131">In questa sezione si crea un'app console Java che:</span><span class="sxs-lookup"><span data-stu-id="80d7f-131">In this section, you create a Java console app that:</span></span>

1. <span data-ttu-id="80d7f-132">Richiama il metodo diretto reboot nell'app per dispositivo simulato.</span><span class="sxs-lookup"><span data-stu-id="80d7f-132">Invokes the reboot direct method in the simulated device app.</span></span>
1. <span data-ttu-id="80d7f-133">Visualizza la risposta.</span><span class="sxs-lookup"><span data-stu-id="80d7f-133">Displays the response.</span></span>
1. <span data-ttu-id="80d7f-134">Esegue il polling delle proprietà segnalate inviate dal dispositivo per determinare quando viene completato il riavvio.</span><span class="sxs-lookup"><span data-stu-id="80d7f-134">Polls the reported properties sent from the device to determine when the reboot is complete.</span></span>

<span data-ttu-id="80d7f-135">Quest'app console si connette all'hub IoT per richiamare il metodo diretto e leggere le proprietà segnalate.</span><span class="sxs-lookup"><span data-stu-id="80d7f-135">This console app connects to your IoT Hub to invoke the direct method and read the reported properties.</span></span>

1. <span data-ttu-id="80d7f-136">Creare una cartella vuota denominata dm-get-started.</span><span class="sxs-lookup"><span data-stu-id="80d7f-136">Create an empty folder called dm-get-started.</span></span>

1. <span data-ttu-id="80d7f-137">Nella cartella dm-get-started creare un progetto Maven denominato **trigger-reboot** usando il comando seguente al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="80d7f-137">In the dm-get-started folder, create a Maven project called **trigger-reboot** using the following command at your command prompt.</span></span> <span data-ttu-id="80d7f-138">L'esempio seguente mostra un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="80d7f-138">The following shows a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="80d7f-139">Al prompt dei comandi passare alla cartella trigger-reboot.</span><span class="sxs-lookup"><span data-stu-id="80d7f-139">At your command prompt, navigate to the trigger-reboot folder.</span></span>

1. <span data-ttu-id="80d7f-140">In un editor di testo aprire il file pom.xml nella cartella trigger-reboot e aggiungere la dipendenza seguente al nodo **dependencies** .</span><span class="sxs-lookup"><span data-stu-id="80d7f-140">Using a text editor, open the pom.xml file in the trigger-reboot folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="80d7f-141">Questa dipendenza consente di usare il pacchetto iot-service-client nell'app per comunicare con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="80d7f-141">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="80d7f-142">È possibile cercare la versione più recente di **iot-service-client** usando la [ricerca di Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="80d7f-142">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="80d7f-143">Aggiungere il nodo **build** seguente dopo il nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="80d7f-143">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="80d7f-144">Questa configurazione indica a Maven di usare Java 1.8 per compilare l'app:</span><span class="sxs-lookup"><span data-stu-id="80d7f-144">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="80d7f-145">Salvare e chiudere il file pom.xml.</span><span class="sxs-lookup"><span data-stu-id="80d7f-145">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="80d7f-146">Usando un editor di testo, aprire il file di origine trigger-reboot\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="80d7f-146">Using a text editor, open the trigger-reboot\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="80d7f-147">Aggiungere al file le istruzioni **import** seguenti:</span><span class="sxs-lookup"><span data-stu-id="80d7f-147">Add the following **import** statements to the file:</span></span>

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

1. <span data-ttu-id="80d7f-148">Aggiungere le variabili a livello di classe seguenti alla classe **App** .</span><span class="sxs-lookup"><span data-stu-id="80d7f-148">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="80d7f-149">Sostituire `{youriothubconnectionstring}` con la stringa di connessione dell'hub IoT indicata nella sezione *Creare un hub IoT*:</span><span class="sxs-lookup"><span data-stu-id="80d7f-149">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. <span data-ttu-id="80d7f-150">Per implementare un thread che legge le proprietà segnalate da un dispositivo gemello ogni 10 secondi, aggiungere la seguente classe nidificata alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="80d7f-150">To implement a thread that reads the reported properties from the device twin every 10 seconds, add the following nested class to the **App** class:</span></span>

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

1. <span data-ttu-id="80d7f-151">Per richiamare il metodo diretto di riavvio sul dispositivo simulato, aggiungere il codice seguente al metodo **main**:</span><span class="sxs-lookup"><span data-stu-id="80d7f-151">To invoke the reboot direct method on the simulated device, add the following code to the **main** method:</span></span>

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

1. <span data-ttu-id="80d7f-152">Per avviare il thread per eseguire il polling delle proprietà segnalate dal dispositivo simulato, aggiungere il codice seguente al metodo **main**:</span><span class="sxs-lookup"><span data-stu-id="80d7f-152">To start the thread to poll the reported properties from the simulated device, add the following code to the **main** method:</span></span>

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. <span data-ttu-id="80d7f-153">Per consentire all'utente di arrestare l'app, aggiungere il codice seguente al metodo **main**:</span><span class="sxs-lookup"><span data-stu-id="80d7f-153">To enable you to stop the app, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Press ENTER to exit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="80d7f-154">Salvare e chiudere il file trigger-reboot\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="80d7f-154">Save and close the trigger-reboot\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="80d7f-155">Compilare l'app di back-end **trigger riavvio** e correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="80d7f-155">Build the **trigger-reboot** back-end app and correct any errors.</span></span> <span data-ttu-id="80d7f-156">Al prompt dei comandi passare alla cartella trigger-reboot ed eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="80d7f-156">At your command prompt, navigate to the trigger-reboot folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="80d7f-157">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="80d7f-157">Create a simulated device app</span></span>

<span data-ttu-id="80d7f-158">In questa sezione si crea un'app console Java che simula un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="80d7f-158">In this section, you create a Java console app that simulates a device.</span></span> <span data-ttu-id="80d7f-159">L'app è in attesa della chiamata al metodo diretto di riavvio dall'hub IoT e risponde immediatamente.</span><span class="sxs-lookup"><span data-stu-id="80d7f-159">The app listens for the reboot direct method call from your IoT hub and immediately responds to that call.</span></span> <span data-ttu-id="80d7f-160">L'app viene quindi sospesa per un periodo di tempo per simulare il processo di riavvio prima di usare una proprietà segnalata per notificare all'app di back-end **trigger-reboot** il completamento del riavvio.</span><span class="sxs-lookup"><span data-stu-id="80d7f-160">The app then sleeps for a while to simulate the reboot process before it uses a reported property to notify the **trigger-reboot** back-end app that the reboot is complete.</span></span>

1. <span data-ttu-id="80d7f-161">Nella cartella dm-get-started creare un progetto Maven denominato **simulated-device** usando il comando seguente nel prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="80d7f-161">In the dm-get-started folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="80d7f-162">L'esempio seguente è un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="80d7f-162">The following is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="80d7f-163">Al prompt dei comandi passare alla cartella simulated-device.</span><span class="sxs-lookup"><span data-stu-id="80d7f-163">At your command prompt, navigate to the simulated-device folder.</span></span>

1. <span data-ttu-id="80d7f-164">In un editor di testo aprire il file pom.xml nella cartella simulated-device e aggiungere la dipendenza seguente al nodo **dependencies** .</span><span class="sxs-lookup"><span data-stu-id="80d7f-164">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="80d7f-165">Questa dipendenza consente di usare il pacchetto iot-service-client nell'app per comunicare con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="80d7f-165">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="80d7f-166">È possibile cercare la versione più recente di **iot-device-client** usando la [ricerca di Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="80d7f-166">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="80d7f-167">Aggiungere il nodo **build** seguente dopo il nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="80d7f-167">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="80d7f-168">Questa configurazione indica a Maven di usare Java 1.8 per compilare l'app:</span><span class="sxs-lookup"><span data-stu-id="80d7f-168">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="80d7f-169">Salvare e chiudere il file pom.xml.</span><span class="sxs-lookup"><span data-stu-id="80d7f-169">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="80d7f-170">Usando un editor di testo, aprire il file di origine simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="80d7f-170">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java source file.</span></span>

1. <span data-ttu-id="80d7f-171">Aggiungere al file le istruzioni **import** seguenti:</span><span class="sxs-lookup"><span data-stu-id="80d7f-171">Add the following **import** statements to the file:</span></span>

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

1. <span data-ttu-id="80d7f-172">Aggiungere le variabili a livello di classe seguenti alla classe **App** .</span><span class="sxs-lookup"><span data-stu-id="80d7f-172">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="80d7f-173">Sostituire `{yourdeviceconnectionstring}` con la stringa di connessione del dispositivo indicata nella sezione *Creare un'identità del dispositivo*:</span><span class="sxs-lookup"><span data-stu-id="80d7f-173">Replace `{yourdeviceconnectionstring}` with the device connection string you noted in the *Create a device identity* section:</span></span>

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. <span data-ttu-id="80d7f-174">Per implementare un gestore di callback per gli eventi di stato del metodo diretto, aggiungere la classe nidificata seguente alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="80d7f-174">To implement a callback handler for direct method status events, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded to device method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="80d7f-175">Per implementare un gestore di callback per gli eventi di stato del dispositivo gemello, aggiungere la classe nidificata seguente alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="80d7f-175">To implement a callback handler for device twin status events, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded to device twin operation with status " + status.name());
        }
    }
    ```

1. <span data-ttu-id="80d7f-176">Per implementare un gestore di callback per gli eventi delle proprietà, aggiungere la classe nidificata seguente alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="80d7f-176">To implement a callback handler for property events, add the following nested class to the **App** class:</span></span>

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

1. <span data-ttu-id="80d7f-177">Per implementare un thread per simulare il riavvio del dispositivo, aggiungere la classe nidificata seguente alla classe **App**.</span><span class="sxs-lookup"><span data-stu-id="80d7f-177">To implement a thread to simulate the device reboot, add the following nested class to the **App** class.</span></span> <span data-ttu-id="80d7f-178">Il thread rimane inattivo per cinque secondi e quindi imposta la proprietà segnalata **lastReboot**:</span><span class="sxs-lookup"><span data-stu-id="80d7f-178">The thread sleeps for five seconds and then sets the **lastReboot** reported property:</span></span>

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

1. <span data-ttu-id="80d7f-179">Per implementare il metodo diretto nel dispositivo, aggiungere la classe nidificata seguente alla classe **App**.</span><span class="sxs-lookup"><span data-stu-id="80d7f-179">To implement the direct method on the device, add the following nested class to the **App** class.</span></span> <span data-ttu-id="80d7f-180">Quando l'app simulata riceve una chiamata al metodo diretto di **riavvio**, restituisce una conferma al chiamante e quindi avvia un thread per elaborare il riavvio:</span><span class="sxs-lookup"><span data-stu-id="80d7f-180">When the simulated app receives a call to the **reboot** direct method, it returns an acknowledgement to the caller and then starts a thread to process the reboot:</span></span>

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

1. <span data-ttu-id="80d7f-181">Modificare la firma del metodo **main** escludendo le eccezioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="80d7f-181">Modify the signature of the **main** method to throw the following exceptions:</span></span>

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="80d7f-182">Per creare un'istanza di **DeviceClient**, aggiungere il codice seguente al metodo **main**:</span><span class="sxs-lookup"><span data-stu-id="80d7f-182">To instantiate a **DeviceClient**, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. <span data-ttu-id="80d7f-183">Per avviare l'ascolto delle chiamate al metodo diretto, aggiungere il codice seguente al metodo **main**:</span><span class="sxs-lookup"><span data-stu-id="80d7f-183">To start listening for direct method calls, add the following code to the **main** method:</span></span>

    ```java
    try
    {
      client.open();
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
      client.startDeviceTwin(new DeviceTwinStatusCallback(), null, new PropertyCallback(), null);
      System.out.println("Subscribed to direct methods and polling for reported properties. Waiting...");
    }
    catch (Exception e)
    {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="80d7f-184">Per arrestare il simulatore del dispositivo, aggiungere il codice seguente al metodo **main**:</span><span class="sxs-lookup"><span data-stu-id="80d7f-184">To shut down the device simulator, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Press any key to exit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. <span data-ttu-id="80d7f-185">Salvare e chiudere il file simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="80d7f-185">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="80d7f-186">Compilare l'app di back-end **simulated-device** e correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="80d7f-186">Build the **simulated-device** back-end app and correct any errors.</span></span> <span data-ttu-id="80d7f-187">Al prompt dei comandi passare alla cartella simulated-device ed eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="80d7f-187">At your command prompt, navigate to the simulated-device folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="80d7f-188">Eseguire le app</span><span class="sxs-lookup"><span data-stu-id="80d7f-188">Run the apps</span></span>

<span data-ttu-id="80d7f-189">A questo punto è possibile eseguire le app.</span><span class="sxs-lookup"><span data-stu-id="80d7f-189">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="80d7f-190">Eseguire questo comando al prompt dei comandi nella cartella simulated-device per iniziare ad ascoltare le chiamate ai metodi di riavvio dell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="80d7f-190">At a command prompt in the simulated-device folder, run the following command to begin listening for reboot method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![App per il dispositivo simulato dell'hub IoT per Java per ascoltare le chiamate al metodo diretto di riavvio][1]

1. <span data-ttu-id="80d7f-192">Eseguire questo comando al prompt dei comandi nella cartella trigger-reboot per chiamare un metodo di riavvio sul dispositivo simulato dell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="80d7f-192">At a command prompt in the trigger-reboot folder, run the following command to call the reboot method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![App del servizio hub IoT per Java per chiamare il metodo diretto di riavvio][2]

1. <span data-ttu-id="80d7f-194">Il dispositivo simulato risponde alla chiamata al metodo diretto di riavvio:</span><span class="sxs-lookup"><span data-stu-id="80d7f-194">The simulated device responds to the reboot direct method call:</span></span>

    ![L'app del dispositivo simulato dell'hub IoT per Java risponde alla chiamata al metodo diretto][3]

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