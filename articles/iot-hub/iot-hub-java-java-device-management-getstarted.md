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
# <a name="get-started-with-device-management-java"></a>Introduzione alla gestione dei dispositivi (Java)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

Questa esercitazione illustra come:

* Utilizzare hello toocreate portale Azure un IoT Hub e creare un'identità del dispositivo nell'hub IoT.
* Creare un'app dispositivo simulato che implementa un dispositivo di hello tooreboot dirette del metodo. Diretti metodi vengono richiamati dal cloud hello.
* Creare un'applicazione che richiama hello riavvio dirette del metodo nell'app dispositivo simulato hello tramite l'hub IoT. Questa app quindi monitoraggi hello proprietà segnalate da hello dispositivo toosee al termine dell'operazione di riavvio hello.

Alla fine di hello di questa esercitazione, si dispongono di due applicazioni di console Java:

**simulated-device**. Questa app:

* Collega l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza.
* Riceve una chiamata del metodo diretto per il riavvio.
* Simula un riavvio fisico.
* Report hello ora dell'ultimo riavvio di hello tramite una proprietà segnalato.

**trigger-reboot**. Questa app:

* Chiama un metodo diretto in app dispositivo simulato hello.
* Visualizza chiamate dirette del metodo di hello risposta toohello inviata dal dispositivo simulato hello
* Hello Visualizza aggiornato segnalato proprietà.

> [!NOTE]
> Per informazioni su hello SDK che è possibile utilizzare toobuild toorun di applicazioni in dispositivi e la soluzione di back-end, vedere [Azure IoT SDK][lnk-hub-sdks].

toocomplete questa esercitazione, è necessario:

* Java SE 8. <br/> [Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall Java per questa esercitazione su Windows o Linux.
* Maven 3.  <br/> [Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall [Maven] [ lnk-maven] per questa esercitazione su Windows o Linux.
* [Versione di Node.js: 0.10.0 o successiva](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Attivare un riavvio remoto nel dispositivo hello utilizzando un metodo diretto

In questa sezione si crea un'app console Java che:

1. Richiama metodo diretto di riavvio hello in app dispositivo simulato hello.
1. Visualizza la risposta hello.
1. Hello polling segnalato proprietà inviate da hello dispositivo toodetermine quando hello riavvio è completo.

Questa app console si connette tooyour IoT Hub tooinvoke hello dirette del metodo e lettura hello segnalati proprietà.

1. Creare una cartella vuota denominata dm-get-started.

1. Nella cartella di avvio get dm hello, creare un progetto di Maven denominato **trigger riavvio** utilizzando hello seguente comando al prompt dei comandi. Hello seguito è riportato un comando singolo, condizione:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=trigger-reboot -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Al prompt dei comandi, passare toohello trigger riavvio cartella.

1. Utilizzando un editor di testo, aprire hello pom.xml file nella cartella di trigger richiede il riavvio di hello e aggiungere hello seguente dipendenza toohello **dipendenze** nodo. Questa dipendenza consente si toouse hello client di servizi iot pacchetto in toocommunicate l'app con l'hub IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > È possibile verificare la versione più recente di hello di **client di servizi iot** utilizzando [ricerca Maven][lnk-maven-service-search].

1. Aggiungere il seguente hello **compilare** nodo dopo hello **dipendenze** nodo. Questa configurazione indica Maven toouse Java toobuild 1.8 hello app:

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

1. Salvare e chiudere il file di pom.xml hello.

1. Utilizzando un editor di testo, aprire file di origine trigger-reboot\src\main\java\com\mycompany\app\App.java hello.

1. Aggiungere il seguente hello **importare** file toohello istruzioni:

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

1. Aggiungere hello seguenti variabili a livello di classe toohello **App** classe. Sostituire `{youriothubconnectionstring}` con la stringa di connessione hub IoT è stata annotata nella hello *creare un IoT Hub* sezione:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    private static final String methodName = "reboot";
    private static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    private static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    ```

1. un thread che legge hello tooimplement segnalati proprietà da un doppio dispositivo hello ogni 10 secondi, aggiungere il seguente di hello annidati classe toohello **App** classe:

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

1. metodo diretto tooinvoke hello riavvio nel dispositivo simulato hello, aggiungere hello seguente codice toohello **principale** metodo:

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

1. toostart hello thread toopoll hello proprietà segnalate dal dispositivo simulato hello, aggiungere hello seguente codice toohello **principale** metodo:

    ```java
    ShowReportedProperties showReportedProperties = new ShowReportedProperties();
    ExecutorService executor = Executors.newFixedThreadPool(1);
    executor.execute(showReportedProperties);
    ```

1. tooenable è toostop hello app, aggiungere hello seguente codice toohello **principale** metodo:

    ```java
    System.out.println("Press ENTER tooexit.");
    System.in.read();
    executor.shutdownNow();
    System.out.println("Shutting down sample...");
    ```

1. Salvare e chiudere il file di trigger-reboot\src\main\java\com\mycompany\app\App.java hello.

1. Compilare hello **trigger riavvio** app back-end e correggere eventuali errori. Al prompt dei comandi, passare toohello trigger riavvio cartella e hello esecuzione comando seguente:

    `mvn clean package -DskipTests`

## <a name="create-a-simulated-device-app"></a>Creare un'app di dispositivo simulato

In questa sezione si crea un'app console Java che simula un dispositivo. app Hello è in attesa di una chiamata al metodo diretta hello riavvio dall'hub IoT e risponde immediatamente toothat chiamata. Hello app quindi inattivo per un periodo di tempo processo di riavvio hello toosimulate prima di utilizzare un hello toonotify proprietà segnalati **trigger riavvio** app back-end che hello riavvio è stata completata.

1. Nella cartella di avvio get dm hello, creare un progetto di Maven denominato **dispositivo simulato** utilizzando hello seguente comando al prompt dei comandi. di seguito Hello è un comando singolo, condizione:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Al prompt dei comandi, passare cartella dispositivo simulato toohello.

1. Utilizzando un editor di testo, di aprire file pom.xml hello nella cartella dispositivo simulato hello e aggiungere hello seguente dipendenza toohello **dipendenze** nodo. Questa dipendenza consente si toouse hello client di servizi iot pacchetto in toocommunicate l'app con l'hub IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > È possibile verificare la versione più recente di hello di **client di dispositivi iot** utilizzando [ricerca Maven][lnk-maven-device-search].

1. Aggiungere il seguente hello **compilare** nodo dopo hello **dipendenze** nodo. Questa configurazione indica Maven toouse Java toobuild 1.8 hello app:

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

1. Salvare e chiudere il file di pom.xml hello.

1. Utilizzando un editor di testo, aprire file di origine simulated-device\src\main\java\com\mycompany\app\App.java hello.

1. Aggiungere il seguente hello **importare** file toohello istruzioni:

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

1. Aggiungere hello seguenti variabili a livello di classe toohello **App** classe. Sostituire `{yourdeviceconnectionstring}` con stringa di connessione dispositivo hello annotato nel hello *creare un'identità del dispositivo* sezione:

    ```java
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;

    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String connString = "{yourdeviceconnectionstring}";
    private static DeviceClient client;
    ```

1. tooimplement un gestore di callback per gli eventi di stato dirette del metodo, aggiungere il seguente di hello annidati classe toohello **App** classe:

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. tooimplement un gestore di callback per gli eventi dello stato di dispositivo doppi, aggiungere il seguente di hello annidati classe toohello **App** classe:

    ```java
    protected static class DeviceTwinStatusCallback implements IotHubEventCallback
    {
        public void execute(IotHubStatusCode status, Object context)
        {
            System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
        }
    }
    ```

1. tooimplement un gestore di callback per gli eventi di proprietà, aggiungere il seguente hello annidati classe toohello **App** classe:

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

1. tooimplement un thread toosimulate hello il riavvio del dispositivo, aggiungere il seguente hello annidati classe toohello **App** classe. thread di Hello rimane inattivo per cinque secondi e quindi imposta hello **lastReboot** segnalati proprietà:

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

1. tooimplement hello dirette del metodo sul dispositivo hello, aggiungere il seguente hello annidati classe toohello **App** classe. Quando applicazione simulata hello riceve una chiamata toohello **riavviare** dirette del metodo, viene restituito un chiamante toohello acknowledgement e avvia un hello tooprocess thread riavviare:

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

1. Modificare la firma hello di hello **principale** hello toothrow metodo le eccezioni seguenti:

    ```java
    public static void main(String[] args) throws IOException, URISyntaxException
    ```

1. tooinstantiate un **DeviceClient**, aggiungere hello seguente codice toohello **principale** metodo:

    ```java
    System.out.println("Starting device client sample...");
    client = new DeviceClient(connString, protocol);
    ```

1. toostart in attesa di chiamate dirette del metodo, aggiungere hello seguente codice toohello **principale** metodo:

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

1. tooshut verso il basso il simulatore di dispositivi hello, aggiungere hello seguente codice toohello **principale** metodo:

    ```java
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    scanner.close();
    client.close();
    System.out.println("Shutting down...");
    ```

1. Salvare e chiudere il file di simulated-device\src\main\java\com\mycompany\app\App.java hello.

1. Compilare hello **dispositivo simulato** app back-end e correggere eventuali errori. Al prompt dei comandi, passare cartella dispositivo simulato toohello e hello esecuzione comando seguente:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Eseguire App hello

Si è ora pronto toorun hello app.

1. Al prompt dei comandi nella cartella dispositivo simulato hello eseguire hello in ascolto per le chiamate di metodo di riavvio dall'hub IoT toobegin di comando seguente:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub Java simulato dispositivo app toolisten per chiamate dirette del metodo di riavvio][1]

1. Al prompt dei comandi nella cartella trigger richiede il riavvio di hello eseguire hello seguente metodo di riavvio hello toocall comando sul dispositivo simulato dall'hub IoT:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Hello toocall app del servizio di linguaggio IoT Hub dirette del metodo di riavvio][2]

1. dispositivo simulato Hello risponde chiamata al metodo diretto toohello riavvio:

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