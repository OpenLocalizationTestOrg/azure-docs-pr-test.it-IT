---
title: Usare metodi diretti dell'Hub IoT di Azure (Java) | Microsoft Docs
description: Come usare metodi diretti dell'Hub IoT di Azure. Usare Azure IoT SDK per dispositivi per Java per implementare un'app per dispositivo simulato che include un metodo diretto e Azure IoT SDK per servizi per Java per implementare un'app del servizio che richiama il metodo diretto.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 6243a1a8cc971c53c797182b2beb6f594d2ac5f7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-direct-methods-java"></a><span data-ttu-id="a8c63-104">Usare metodi diretti (Java)</span><span class="sxs-lookup"><span data-stu-id="a8c63-104">Use direct methods (Java)</span></span>

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="a8c63-105">In questa esercitazione vengono create due app console Java:</span><span class="sxs-lookup"><span data-stu-id="a8c63-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="a8c63-106">**invoke-direct-method**, un'app back-end Java che chiama un metodo nell'app per dispositivo simulato e visualizza la risposta.</span><span class="sxs-lookup"><span data-stu-id="a8c63-106">**invoke-direct-method**, a Java back-end app that calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="a8c63-107">**simulated-device**, un'app Java che simula la connessione di un dispositivo all'hub IoT con l'identità del dispositivo creata.</span><span class="sxs-lookup"><span data-stu-id="a8c63-107">**simulated-device**, a Java app that simulates a device connecting to your IoT hub with the device identity you create.</span></span> <span data-ttu-id="a8c63-108">Questa app risponde al metodo diretto richiamato dal back-end.</span><span class="sxs-lookup"><span data-stu-id="a8c63-108">This app responds to the direct invoked from the back end.</span></span>

> [!NOTE]
> <span data-ttu-id="a8c63-109">Per informazioni sugli SDK che consentono di compilare le applicazioni da eseguire nei dispositivi e i back-end della soluzione, vedere [Azure IoT SDK][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="a8c63-109">For information about the SDKs that you can use to build applications to run on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="a8c63-110">Per completare questa esercitazione, sono necessari:</span><span class="sxs-lookup"><span data-stu-id="a8c63-110">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="a8c63-111">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="a8c63-111">Java SE 8.</span></span> <br/> <span data-ttu-id="a8c63-112">[Preparare l'ambiente di sviluppo][lnk-dev-setup] descrive come installare Java per questa esercitazione in Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="a8c63-112">[Prepare your development environment][lnk-dev-setup] describes how to install Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="a8c63-113">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="a8c63-113">Maven 3.</span></span>  <br/> <span data-ttu-id="a8c63-114">[Preparare l'ambiente di sviluppo][lnk-dev-setup] descrive come installare [Maven][lnk-maven] per questa esercitazione in Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="a8c63-114">[Prepare your development environment][lnk-dev-setup] describes how to install [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="a8c63-115">[Versione di Node.js: 0.10.0 o successiva](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="a8c63-115">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="a8c63-116">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="a8c63-116">Create a simulated device app</span></span>

<span data-ttu-id="a8c63-117">In questa sezione viene creata un'app console Java che risponde a un metodo chiamato dal back-end della soluzione.</span><span class="sxs-lookup"><span data-stu-id="a8c63-117">In this section, you create a Java console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="a8c63-118">Creare una cartella vuota denominata iot-java-direct-method.</span><span class="sxs-lookup"><span data-stu-id="a8c63-118">Create an empty folder called iot-java-direct-method.</span></span>

1. <span data-ttu-id="a8c63-119">Nella cartella iot-java-direct-method creare un progetto Maven denominato **simulated-device** usando il comando seguente al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="a8c63-119">In the iot-java-direct-method folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="a8c63-120">Il comando seguente è un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="a8c63-120">The following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="a8c63-121">Al prompt dei comandi passare alla cartella simulated-device.</span><span class="sxs-lookup"><span data-stu-id="a8c63-121">At your command prompt, navigate to the simulated-device folder.</span></span>

1. <span data-ttu-id="a8c63-122">In un editor di testo aprire il file pom.xml nella cartella simulated-device e aggiungere le dipendenze seguenti al nodo **dependencies** .</span><span class="sxs-lookup"><span data-stu-id="a8c63-122">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="a8c63-123">Questa dipendenza consente di usare il pacchetto iot-device-client nell'app per comunicare con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="a8c63-123">This dependency enables you to use the iot-device-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="a8c63-124">È possibile cercare la versione più recente di **iot-device-client** usando la [ricerca di Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="a8c63-124">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="a8c63-125">Aggiungere il nodo **build** seguente dopo il nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="a8c63-125">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="a8c63-126">Questa configurazione indica a Maven di usare Java 1.8 per compilare l'app:</span><span class="sxs-lookup"><span data-stu-id="a8c63-126">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="a8c63-127">Salvare e chiudere il file pom.xml.</span><span class="sxs-lookup"><span data-stu-id="a8c63-127">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="a8c63-128">Usando un editor di testo, aprire il file simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="a8c63-128">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="a8c63-129">Aggiungere al file le istruzioni **import** seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8c63-129">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="a8c63-130">Aggiungere le variabili a livello di classe seguenti alla classe **App** .</span><span class="sxs-lookup"><span data-stu-id="a8c63-130">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="a8c63-131">Sostituzione di `{youriothubname}` con il nome dell'hub IoT e di `{yourdevicekey}` con il valore della chiave del dispositivo generato nella sezione *Creare un'identità del dispositivo*:</span><span class="sxs-lookup"><span data-stu-id="a8c63-131">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="a8c63-132">Questa app di esempio usa la variabile **protocol** quando crea un'istanza di un oggetto **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="a8c63-132">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="a8c63-133">Attualmente per usare i metodi diretti è necessario usare il protocollo MQTT.</span><span class="sxs-lookup"><span data-stu-id="a8c63-133">Currently, to use direct methods you must use the MQTT protocol.</span></span>

1. <span data-ttu-id="a8c63-134">Per restituire un codice di stato all'hub IoT, aggiungere la classe annidata seguente alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="a8c63-134">To return a status code to your IoT hub, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded to device method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="a8c63-135">Per gestire le chiamate al metodo diretto dal back-end della soluzione, aggiungere la classe annidata seguente alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="a8c63-135">To handle the direct method invocations from the solution back end, add the following nested class to the **App** class:</span></span>

    ```java
    protected static class DirectMethodCallback implements com.microsoft.azure.sdk.iot.device.DeviceTwin.DeviceMethodCallback
    {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context)
      {
        DeviceMethodData deviceMethodData;
        switch (methodName)
        {
          case "writeLine" :
          {
            int status = METHOD_SUCCESS;
            System.out.println(new String((byte[])methodData));
            deviceMethodData = new DeviceMethodData(status, "Executed direct method " + methodName);
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

1. <span data-ttu-id="a8c63-136">Per creare un **DeviceClient** e rimanere in ascolto delle chiamate al metodo diretto, aggiungere un metodo **main** alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="a8c63-136">To create a **DeviceClient** and listen for direct method invocations, add a **main** method to the **App** class:</span></span>

    ```java
    public static void main(String[] args)
      throws IOException, URISyntaxException
    {
      System.out.println("Starting device sample...");

      DeviceClient client = new DeviceClient(connString, protocol);

      try
      {
        client.open();
        client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
        System.out.println("Subscribed to direct methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key to exit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="a8c63-137">Salvare e chiudere il file simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="a8c63-137">Save and close the simulated-device\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="a8c63-138">Compilare l'app **simulated-device** e correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="a8c63-138">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="a8c63-139">Al prompt dei comandi passare alla cartella simulated-device ed eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a8c63-139">At your command prompt, navigate to the simulated-device folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="a8c63-140">Chiamare un metodo diretto in un dispositivo</span><span class="sxs-lookup"><span data-stu-id="a8c63-140">Call a direct method on a device</span></span>

<span data-ttu-id="a8c63-141">In questa sezione viene creata un'app console Java che richiama un metodo diretto e quindi visualizza la risposta.</span><span class="sxs-lookup"><span data-stu-id="a8c63-141">In this section, you create a Java console app that invokes a direct method and then displays the response.</span></span> <span data-ttu-id="a8c63-142">Quest'app console si connette all'hub IoT per richiamare il metodo diretto.</span><span class="sxs-lookup"><span data-stu-id="a8c63-142">This console app connects to your IoT Hub to invoke the direct method.</span></span>

1. <span data-ttu-id="a8c63-143">Nella cartella iot-java-direct-method creare un progetto Maven denominato **invoke-direct-method** usando il comando seguente al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="a8c63-143">In the iot-java-direct-method folder, create a Maven project called **invoke-direct-method** using the following command at your command prompt.</span></span> <span data-ttu-id="a8c63-144">Il comando seguente è un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="a8c63-144">The following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="a8c63-145">Al prompt dei comandi passare alla cartella invoke-direct-method.</span><span class="sxs-lookup"><span data-stu-id="a8c63-145">At your command prompt, navigate to the invoke-direct-method folder.</span></span>

1. <span data-ttu-id="a8c63-146">In un editor di testo aprire il file pom.xml nella cartella invoke-direct-method e aggiungere la dipendenza seguente al nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="a8c63-146">Using a text editor, open the pom.xml file in the invoke-direct-method folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="a8c63-147">Questa dipendenza consente di usare il pacchetto iot-service-client nell'app per comunicare con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="a8c63-147">This dependency enables you to use the iot-service-client package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="a8c63-148">È possibile cercare la versione più recente di **iot-service-client** usando la [ricerca di Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="a8c63-148">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="a8c63-149">Aggiungere il nodo **build** seguente dopo il nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="a8c63-149">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="a8c63-150">Questa configurazione indica a Maven di usare Java 1.8 per compilare l'app:</span><span class="sxs-lookup"><span data-stu-id="a8c63-150">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="a8c63-151">Salvare e chiudere il file pom.xml.</span><span class="sxs-lookup"><span data-stu-id="a8c63-151">Save and close the pom.xml file.</span></span>

1. <span data-ttu-id="a8c63-152">In un editor di testo aprire il file invoke-direct-method\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="a8c63-152">Using a text editor, open the invoke-direct-method\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="a8c63-153">Aggiungere al file le istruzioni **import** seguenti:</span><span class="sxs-lookup"><span data-stu-id="a8c63-153">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. <span data-ttu-id="a8c63-154">Aggiungere le variabili a livello di classe seguenti alla classe **App** .</span><span class="sxs-lookup"><span data-stu-id="a8c63-154">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="a8c63-155">Sostituire `{youriothubconnectionstring}` con la stringa di connessione dell'hub IoT indicata nella sezione *Creare un hub IoT*:</span><span class="sxs-lookup"><span data-stu-id="a8c63-155">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line to be written";
    ```

1. <span data-ttu-id="a8c63-156">Per richiamare il metodo sul dispositivo simulato, aggiungere il codice seguente al metodo **main**:</span><span class="sxs-lookup"><span data-stu-id="a8c63-156">To invoke the method on the simulated device, add the following code to the **main** method:</span></span>

    ```java
    System.out.println("Starting sample...");
    DeviceMethod methodClient = DeviceMethod.createFromConnectionString(iotHubConnectionString);

    try
    {
        System.out.println("Invoke direct method");
        MethodResult result = methodClient.invoke(deviceId, methodName, responseTimeout, connectTimeout, payload);

        if(result == null)
        {
            throw new IOException("Direct method invoke returns null");
        }
        System.out.println("Status=" + result.getStatus());
        System.out.println("Payload=" + result.getPayload());
    }
    catch (IotHubException e)
    {
        System.out.println(e.getMessage());
    }

    System.out.println("Shutting down sample...");
    ```

1. <span data-ttu-id="a8c63-157">Salvare e chiudere il file invoke-direct-method\src\main\java\com\mycompany\app\App.java</span><span class="sxs-lookup"><span data-stu-id="a8c63-157">Save and close the invoke-direct-method\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="a8c63-158">Compilare l'app **invoke-direct-method** e correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="a8c63-158">Build the **invoke-direct-method** app and correct any errors.</span></span> <span data-ttu-id="a8c63-159">Al prompt dei comandi passare alla cartella invoke-direct-method ed eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a8c63-159">At your command prompt, navigate to the invoke-direct-method folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="a8c63-160">Eseguire le app</span><span class="sxs-lookup"><span data-stu-id="a8c63-160">Run the apps</span></span>

<span data-ttu-id="a8c63-161">A questo punto è possibile eseguire le app console.</span><span class="sxs-lookup"><span data-stu-id="a8c63-161">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="a8c63-162">Eseguire questo comando al prompt dei comandi nella cartella simulated-device per iniziare ad ascoltare le chiamate ai metodi dell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="a8c63-162">At a command prompt in the simulated-device folder, run the following command to begin listening for method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![App del dispositivo simulato dell'hub IoT per Java per ascoltare le chiamate al metodo diretto][8]

1. <span data-ttu-id="a8c63-164">Eseguire questo comando al prompt dei comandi nella cartella invoke-direct-method per chiamare un metodo sul dispositivo simulato dell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="a8c63-164">At a command prompt in the invoke-direct-method folder, run the following command to call a method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![App del servizio hub IoT per Java per chiamare un metodo diretto][7]

1. <span data-ttu-id="a8c63-166">Il dispositivo simulato risponde alla chiamata al metodo diretto:</span><span class="sxs-lookup"><span data-stu-id="a8c63-166">The simulated device responds to the direct method call:</span></span>

    ![L'app del dispositivo simulato dell'hub IoT per Java risponde alla chiamata al metodo diretto][9]

## <a name="next-steps"></a><span data-ttu-id="a8c63-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a8c63-168">Next steps</span></span>

<span data-ttu-id="a8c63-169">In questa esercitazione è stato configurato un nuovo hub IoT nel Portale di Azure ed è stata quindi creata un'identità del dispositivo nel registro di identità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a8c63-169">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="a8c63-170">Questa identità del dispositivo è stata usata per consentire all'app del dispositivo simulato di reagire ai metodi richiamati dal cloud.</span><span class="sxs-lookup"><span data-stu-id="a8c63-170">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="a8c63-171">È stata anche creata un'applicazione che richiama i metodi sul dispositivo e visualizza la risposta dal dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a8c63-171">You also created an app that invokes methods on the device and displays the response from the device.</span></span>

<span data-ttu-id="a8c63-172">Per esplorare altri scenari IoT, vedere [Pianificare processi in più dispositivi][lnk-devguide-jobs].</span><span class="sxs-lookup"><span data-stu-id="a8c63-172">To explore other IoT scenarios, see [Schedule jobs on multiple devices][lnk-devguide-jobs].</span></span>

<span data-ttu-id="a8c63-173">Per informazioni su come estendere la soluzione IoT e pianificare le chiamate al metodo su più dispositivi, vedere l'esercitazione [Pianificare e trasmettere processi][lnk-tutorial-jobs].</span><span class="sxs-lookup"><span data-stu-id="a8c63-173">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-direct-methods/invoke-method.png
[8]: ./media/iot-hub-java-java-direct-methods/device-listen.png
[9]: ./media/iot-hub-java-java-direct-methods/device-respond.png

<!-- Links -->
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-java/blob/master/doc/java-devbox-setup.md
[lnk-maven]: https://maven.apache.org/what-is-maven.html
[lnk-hub-sdks]: iot-hub-devguide-sdks.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
