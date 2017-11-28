---
title: IoT Hub Azure aaaUse diretta di metodi (linguaggio) | Documenti Microsoft
description: Toouse IoT Hub Azure diretto come metodi. Usare il dispositivo di Azure IoT hello SDK per Java tooimplement un'app dispositivo simulato che include un metodo diretto e hello Azure IoT servizio SDK per Java tooimplement un'applicazione di servizio che richiama metodo diretto hello.
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
ms.openlocfilehash: b6f2f4a64535ab649a3965cd9c5a19bebaf88eef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-java"></a><span data-ttu-id="aee50-104">Usare metodi diretti (Java)</span><span class="sxs-lookup"><span data-stu-id="aee50-104">Use direct methods (Java)</span></span>

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="aee50-105">In questa esercitazione vengono create due app console Java:</span><span class="sxs-lookup"><span data-stu-id="aee50-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="aee50-106">**metodo direct Invoke**, un'applicazione di back-end Java che chiama un metodo in app dispositivo simulato hello e Visualizza la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="aee50-106">**invoke-direct-method**, a Java back-end app that calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="aee50-107">**dispositivo simulato**, un'applicazione Java che simula un dispositivo di connessione hub IoT tooyour con l'identità del dispositivo hello create.</span><span class="sxs-lookup"><span data-stu-id="aee50-107">**simulated-device**, a Java app that simulates a device connecting tooyour IoT hub with hello device identity you create.</span></span> <span data-ttu-id="aee50-108">Questa app risponde toohello richiamato direttamente dal back-end hello.</span><span class="sxs-lookup"><span data-stu-id="aee50-108">This app responds toohello direct invoked from hello back end.</span></span>

> [!NOTE]
> <span data-ttu-id="aee50-109">Per informazioni su hello SDK che è possibile utilizzare toobuild toorun di applicazioni in dispositivi e la soluzione di back-end, vedere [Azure IoT SDK][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="aee50-109">For information about hello SDKs that you can use toobuild applications toorun on devices and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="aee50-110">toocomplete questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="aee50-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="aee50-111">Java SE 8.</span><span class="sxs-lookup"><span data-stu-id="aee50-111">Java SE 8.</span></span> <br/> <span data-ttu-id="aee50-112">[Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall Java per questa esercitazione su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="aee50-112">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Java for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="aee50-113">Maven 3.</span><span class="sxs-lookup"><span data-stu-id="aee50-113">Maven 3.</span></span>  <br/> <span data-ttu-id="aee50-114">[Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall [Maven] [ lnk-maven] per questa esercitazione su Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="aee50-114">[Prepare your development environment][lnk-dev-setup] describes how tooinstall [Maven][lnk-maven] for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="aee50-115">[Versione di Node.js: 0.10.0 o successiva](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="aee50-115">[Node.js version 0.10.0 or later](http://nodejs.org).</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="aee50-116">Creare un'app di dispositivo simulato</span><span class="sxs-lookup"><span data-stu-id="aee50-116">Create a simulated device app</span></span>

<span data-ttu-id="aee50-117">In questa sezione si crea un'applicazione console Java che risponde tooa metodo chiamato dalla soluzione hello nuovamente finale.</span><span class="sxs-lookup"><span data-stu-id="aee50-117">In this section, you create a Java console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="aee50-118">Creare una cartella vuota denominata iot-java-direct-method.</span><span class="sxs-lookup"><span data-stu-id="aee50-118">Create an empty folder called iot-java-direct-method.</span></span>

1. <span data-ttu-id="aee50-119">Nella cartella metodo diretto di java iot hello, creare un progetto di Maven denominato **dispositivo simulato** utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="aee50-119">In hello iot-java-direct-method folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="aee50-120">Hello comando seguente è un comando singolo, condizione:</span><span class="sxs-lookup"><span data-stu-id="aee50-120">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="aee50-121">Al prompt dei comandi, passare cartella dispositivo simulato toohello.</span><span class="sxs-lookup"><span data-stu-id="aee50-121">At your command prompt, navigate toohello simulated-device folder.</span></span>

1. <span data-ttu-id="aee50-122">Utilizzando un editor di testo, di aprire file pom.xml hello nella cartella dispositivo simulato hello e aggiungere hello seguente dipendenze toohello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="aee50-122">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="aee50-123">Questa dipendenza consente si toouse hello client di dispositivi iot pacchetto in toocommunicate l'app con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="aee50-123">This dependency enables you toouse hello iot-device-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="aee50-124">È possibile verificare la versione più recente di hello di **client di dispositivi iot** utilizzando [ricerca Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="aee50-124">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

1. <span data-ttu-id="aee50-125">Aggiungere il seguente hello **compilare** nodo dopo hello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="aee50-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="aee50-126">Questa configurazione indica Maven toouse Java toobuild 1.8 hello app:</span><span class="sxs-lookup"><span data-stu-id="aee50-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="aee50-127">Salvare e chiudere il file di pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="aee50-127">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="aee50-128">Per aprire il file di simulated-device\src\main\java\com\mycompany\app\App.java hello, utilizzando un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="aee50-128">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="aee50-129">Aggiungere il seguente hello **importare** file toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="aee50-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="aee50-130">Aggiungere hello seguenti variabili a livello di classe toohello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="aee50-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="aee50-131">Sostituzione di `{youriothubname}` con il nome di hub IoT, e `{yourdevicekey}` con il valore della chiave di hello dispositivo è stato generato in hello *creare un'identità del dispositivo* sezione:</span><span class="sxs-lookup"><span data-stu-id="aee50-131">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="aee50-132">Questa app di esempio utilizza hello **protocollo** variabile quando si crea un'istanza di un **DeviceClient** oggetto.</span><span class="sxs-lookup"><span data-stu-id="aee50-132">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="aee50-133">Attualmente, toouse diretta metodi è necessario utilizzare il protocollo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="aee50-133">Currently, toouse direct methods you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="aee50-134">tooreturn un hub IoT tooyour codice di stato, aggiungere il seguente hello annidati classe toohello **App** classe:</span><span class="sxs-lookup"><span data-stu-id="aee50-134">tooreturn a status code tooyour IoT hub, add hello following nested class toohello **App** class:</span></span>

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="aee50-135">le chiamate dirette del metodo di hello toohandle dal back-end soluzione hello, aggiungere il seguente di hello annidati classe toohello **App** classe:</span><span class="sxs-lookup"><span data-stu-id="aee50-135">toohandle hello direct method invocations from hello solution back end, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="aee50-136">toocreate un **DeviceClient** e attendere le chiamate dirette del metodo, aggiungere un **principale** metodo toohello **App** classe:</span><span class="sxs-lookup"><span data-stu-id="aee50-136">toocreate a **DeviceClient** and listen for direct method invocations, add a **main** method toohello **App** class:</span></span>

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
        System.out.println("Subscribed toodirect methods. Waiting...");
      }
      catch (Exception e)
      {
        System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" +  e.getMessage());
        client.close();
        System.out.println("Shutting down...");
      }

      System.out.println("Press any key tooexit...");
      Scanner scanner = new Scanner(System.in);
      scanner.nextLine();
      scanner.close();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. <span data-ttu-id="aee50-137">Salvare e chiudere il file di simulated-device\src\main\java\com\mycompany\app\App.java hello</span><span class="sxs-lookup"><span data-stu-id="aee50-137">Save and close hello simulated-device\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="aee50-138">Compilare hello **dispositivo simulato** app e correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="aee50-138">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="aee50-139">Al prompt dei comandi, passare cartella dispositivo simulato toohello e hello esecuzione comando seguente:</span><span class="sxs-lookup"><span data-stu-id="aee50-139">At your command prompt, navigate toohello simulated-device folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="aee50-140">Chiamare un metodo diretto in un dispositivo</span><span class="sxs-lookup"><span data-stu-id="aee50-140">Call a direct method on a device</span></span>

<span data-ttu-id="aee50-141">In questa sezione si crea un'applicazione console Java che richiama un metodo diretto e quindi Visualizza la risposta hello.</span><span class="sxs-lookup"><span data-stu-id="aee50-141">In this section, you create a Java console app that invokes a direct method and then displays hello response.</span></span> <span data-ttu-id="aee50-142">Questa app console si connette tooyour IoT Hub tooinvoke hello dirette del metodo.</span><span class="sxs-lookup"><span data-stu-id="aee50-142">This console app connects tooyour IoT Hub tooinvoke hello direct method.</span></span>

1. <span data-ttu-id="aee50-143">Nella cartella metodo diretto di java iot hello, creare un progetto di Maven denominato **direct-metodo invoke** utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="aee50-143">In hello iot-java-direct-method folder, create a Maven project called **invoke-direct-method** using hello following command at your command prompt.</span></span> <span data-ttu-id="aee50-144">Hello comando seguente è un comando singolo, condizione:</span><span class="sxs-lookup"><span data-stu-id="aee50-144">hello following command is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="aee50-145">Al prompt dei comandi, passare cartella direct-metodo invoke toohello.</span><span class="sxs-lookup"><span data-stu-id="aee50-145">At your command prompt, navigate toohello invoke-direct-method folder.</span></span>

1. <span data-ttu-id="aee50-146">Utilizzando un editor di testo, di aprire file pom.xml hello nella cartella di direct-metodo invoke hello e aggiungere hello seguente dipendenza toohello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="aee50-146">Using a text editor, open hello pom.xml file in hello invoke-direct-method folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="aee50-147">Questa dipendenza consente si toouse hello client di servizi iot pacchetto in toocommunicate l'app con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="aee50-147">This dependency enables you toouse hello iot-service-client package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="aee50-148">È possibile verificare la versione più recente di hello di **client di servizi iot** utilizzando [ricerca Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="aee50-148">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

1. <span data-ttu-id="aee50-149">Aggiungere il seguente hello **compilare** nodo dopo hello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="aee50-149">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="aee50-150">Questa configurazione indica Maven toouse Java toobuild 1.8 hello app:</span><span class="sxs-lookup"><span data-stu-id="aee50-150">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="aee50-151">Salvare e chiudere il file di pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="aee50-151">Save and close hello pom.xml file.</span></span>

1. <span data-ttu-id="aee50-152">Per aprire il file di invoke-direct-method\src\main\java\com\mycompany\app\App.java hello, utilizzando un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="aee50-152">Using a text editor, open hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file.</span></span>

1. <span data-ttu-id="aee50-153">Aggiungere il seguente hello **importare** file toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="aee50-153">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. <span data-ttu-id="aee50-154">Aggiungere hello seguenti variabili a livello di classe toohello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="aee50-154">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="aee50-155">Sostituire `{youriothubconnectionstring}` con la stringa di connessione hub IoT è stata annotata nella hello *creare un IoT Hub* sezione:</span><span class="sxs-lookup"><span data-stu-id="aee50-155">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. <span data-ttu-id="aee50-156">metodo hello tooinvoke sul dispositivo simulato hello, aggiungere hello seguente codice toohello **principale** metodo:</span><span class="sxs-lookup"><span data-stu-id="aee50-156">tooinvoke hello method on hello simulated device, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="aee50-157">Salvare e chiudere il file di invoke-direct-method\src\main\java\com\mycompany\app\App.java hello</span><span class="sxs-lookup"><span data-stu-id="aee50-157">Save and close hello invoke-direct-method\src\main\java\com\mycompany\app\App.java file</span></span>

1. <span data-ttu-id="aee50-158">Compilare hello **direct-metodo invoke** app e correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="aee50-158">Build hello **invoke-direct-method** app and correct any errors.</span></span> <span data-ttu-id="aee50-159">Al prompt dei comandi, passare cartella direct-metodo invoke toohello e hello esecuzione comando seguente:</span><span class="sxs-lookup"><span data-stu-id="aee50-159">At your command prompt, navigate toohello invoke-direct-method folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="aee50-160">Eseguire App hello</span><span class="sxs-lookup"><span data-stu-id="aee50-160">Run hello apps</span></span>

<span data-ttu-id="aee50-161">Si è ora pronto toorun hello console app.</span><span class="sxs-lookup"><span data-stu-id="aee50-161">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="aee50-162">Al prompt dei comandi nella cartella dispositivo simulato hello eseguire hello in attesa di chiamate al metodo dall'hub IoT toobegin di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="aee50-162">At a command prompt in hello simulated-device folder, run hello following command toobegin listening for method calls from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub Java simulato dispositivo app toolisten per chiamate dirette del metodo][8]

1. <span data-ttu-id="aee50-164">Al prompt dei comandi nella cartella direct-metodo invoke hello eseguire hello successivo comando toocall un metodo nel dispositivo simulato dall'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="aee50-164">At a command prompt in hello invoke-direct-method folder, run hello following command toocall a method on your simulated device from your IoT hub:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub Java servizio app toocall un metodo diretto][7]

1. <span data-ttu-id="aee50-166">dispositivo simulato Hello risponde toohello chiamata al metodo diretta:</span><span class="sxs-lookup"><span data-stu-id="aee50-166">hello simulated device responds toohello direct method call:</span></span>

    ![IoT Hub Java dispositivo simulato app risponde chiamata al metodo diretto toohello][9]

## <a name="next-steps"></a><span data-ttu-id="aee50-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aee50-168">Next steps</span></span>

<span data-ttu-id="aee50-169">In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità.</span><span class="sxs-lookup"><span data-stu-id="aee50-169">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="aee50-170">È stato utilizzato questo dispositivo identità tooenable hello simulato dispositivo app tooreact toomethods richiamato dal cloud hello.</span><span class="sxs-lookup"><span data-stu-id="aee50-170">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="aee50-171">È stato creato anche un'applicazione che richiama metodi sul dispositivo hello e Visualizza la risposta hello dal dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="aee50-171">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span>

<span data-ttu-id="aee50-172">tooexplore altri scenari IoT, vedere [pianificare i processi su più dispositivi][lnk-devguide-jobs].</span><span class="sxs-lookup"><span data-stu-id="aee50-172">tooexplore other IoT scenarios, see [Schedule jobs on multiple devices][lnk-devguide-jobs].</span></span>

<span data-ttu-id="aee50-173">toolearn come tooextend il metodo di pianificazione e di soluzione IoT chiama su più dispositivi, vedere hello [pianificazione e i processi di broadcast] [ lnk-tutorial-jobs] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="aee50-173">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
