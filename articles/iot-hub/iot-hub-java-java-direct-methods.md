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
# <a name="use-direct-methods-java"></a>Usare metodi diretti (Java)

[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

In questa esercitazione vengono create due app console Java:

* **metodo direct Invoke**, un'applicazione di back-end Java che chiama un metodo in app dispositivo simulato hello e Visualizza la risposta hello.
* **dispositivo simulato**, un'applicazione Java che simula un dispositivo di connessione hub IoT tooyour con l'identità del dispositivo hello create. Questa app risponde toohello richiamato direttamente dal back-end hello.

> [!NOTE]
> Per informazioni su hello SDK che è possibile utilizzare toobuild toorun di applicazioni in dispositivi e la soluzione di back-end, vedere [Azure IoT SDK][lnk-hub-sdks].

toocomplete questa esercitazione, è necessario:

* Java SE 8. <br/> [Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall Java per questa esercitazione su Windows o Linux.
* Maven 3.  <br/> [Preparare l'ambiente di sviluppo] [ lnk-dev-setup] viene descritto come tooinstall [Maven] [ lnk-maven] per questa esercitazione su Windows o Linux.
* [Versione di Node.js: 0.10.0 o successiva](http://nodejs.org).

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Creare un'app di dispositivo simulato

In questa sezione si crea un'applicazione console Java che risponde tooa metodo chiamato dalla soluzione hello nuovamente finale.

1. Creare una cartella vuota denominata iot-java-direct-method.

1. Nella cartella metodo diretto di java iot hello, creare un progetto di Maven denominato **dispositivo simulato** utilizzando hello seguente comando al prompt dei comandi. Hello comando seguente è un comando singolo, condizione:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Al prompt dei comandi, passare cartella dispositivo simulato toohello.

1. Utilizzando un editor di testo, di aprire file pom.xml hello nella cartella dispositivo simulato hello e aggiungere hello seguente dipendenze toohello **dipendenze** nodo. Questa dipendenza consente si toouse hello client di dispositivi iot pacchetto in toocommunicate l'app con l'hub IoT:

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

1. Per aprire il file di simulated-device\src\main\java\com\mycompany\app\App.java hello, utilizzando un editor di testo.

1. Aggiungere il seguente hello **importare** file toohello istruzioni:

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. Aggiungere hello seguenti variabili a livello di classe toohello **App** classe. Sostituzione di `{youriothubname}` con il nome di hub IoT, e `{yourdevicekey}` con il valore della chiave di hello dispositivo è stato generato in hello *creare un'identità del dispositivo* sezione:

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    Questa app di esempio utilizza hello **protocollo** variabile quando si crea un'istanza di un **DeviceClient** oggetto. Attualmente, toouse diretta metodi è necessario utilizzare il protocollo MQTT hello.

1. tooreturn un hub IoT tooyour codice di stato, aggiungere il seguente hello annidati classe toohello **App** classe:

    ```java
    protected static class DirectMethodStatusCallback implements IotHubEventCallback
    {
      public void execute(IotHubStatusCode status, Object context)
      {
        System.out.println("IoT Hub responded toodevice method operation with status " + status.name());
      }
    }
    ```

1. le chiamate dirette del metodo di hello toohandle dal back-end soluzione hello, aggiungere il seguente di hello annidati classe toohello **App** classe:

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

1. toocreate un **DeviceClient** e attendere le chiamate dirette del metodo, aggiungere un **principale** metodo toohello **App** classe:

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

1. Salvare e chiudere il file di simulated-device\src\main\java\com\mycompany\app\App.java hello

1. Compilare hello **dispositivo simulato** app e correggere eventuali errori. Al prompt dei comandi, passare cartella dispositivo simulato toohello e hello esecuzione comando seguente:

    `mvn clean package -DskipTests`

## <a name="call-a-direct-method-on-a-device"></a>Chiamare un metodo diretto in un dispositivo

In questa sezione si crea un'applicazione console Java che richiama un metodo diretto e quindi Visualizza la risposta hello. Questa app console si connette tooyour IoT Hub tooinvoke hello dirette del metodo.

1. Nella cartella metodo diretto di java iot hello, creare un progetto di Maven denominato **direct-metodo invoke** utilizzando hello seguente comando al prompt dei comandi. Hello comando seguente è un comando singolo, condizione:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=invoke-direct-method -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Al prompt dei comandi, passare cartella direct-metodo invoke toohello.

1. Utilizzando un editor di testo, di aprire file pom.xml hello nella cartella di direct-metodo invoke hello e aggiungere hello seguente dipendenza toohello **dipendenze** nodo. Questa dipendenza consente si toouse hello client di servizi iot pacchetto in toocommunicate l'app con l'hub IoT:

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

1. Per aprire il file di invoke-direct-method\src\main\java\com\mycompany\app\App.java hello, utilizzando un editor di testo.

1. Aggiungere il seguente hello **importare** file toohello istruzioni:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceMethod;
    import com.microsoft.azure.sdk.iot.service.devicetwin.MethodResult;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.concurrent.TimeUnit;
    ```

1. Aggiungere hello seguenti variabili a livello di classe toohello **App** classe. Sostituire `{youriothubconnectionstring}` con la stringa di connessione hub IoT è stata annotata nella hello *creare un IoT Hub* sezione:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String methodName = "writeLine";
    public static final Long responseTimeout = TimeUnit.SECONDS.toSeconds(30);
    public static final Long connectTimeout = TimeUnit.SECONDS.toSeconds(5);
    public static final String payload = "a line toobe written";
    ```

1. metodo hello tooinvoke sul dispositivo simulato hello, aggiungere hello seguente codice toohello **principale** metodo:

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

1. Salvare e chiudere il file di invoke-direct-method\src\main\java\com\mycompany\app\App.java hello

1. Compilare hello **direct-metodo invoke** app e correggere eventuali errori. Al prompt dei comandi, passare cartella direct-metodo invoke toohello e hello esecuzione comando seguente:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Eseguire App hello

Si è ora pronto toorun hello console app.

1. Al prompt dei comandi nella cartella dispositivo simulato hello eseguire hello in attesa di chiamate al metodo dall'hub IoT toobegin di comando seguente:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub Java simulato dispositivo app toolisten per chiamate dirette del metodo][8]

1. Al prompt dei comandi nella cartella direct-metodo invoke hello eseguire hello successivo comando toocall un metodo nel dispositivo simulato dall'hub IoT:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub Java servizio app toocall un metodo diretto][7]

1. dispositivo simulato Hello risponde toohello chiamata al metodo diretta:

    ![IoT Hub Java dispositivo simulato app risponde chiamata al metodo diretto toohello][9]

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità. È stato utilizzato questo dispositivo identità tooenable hello simulato dispositivo app tooreact toomethods richiamato dal cloud hello. È stato creato anche un'applicazione che richiama metodi sul dispositivo hello e Visualizza la risposta hello dal dispositivo hello.

tooexplore altri scenari IoT, vedere [pianificare i processi su più dispositivi][lnk-devguide-jobs].

toolearn come tooextend il metodo di pianificazione e di soluzione IoT chiama su più dispositivi, vedere hello [pianificazione e i processi di broadcast] [ lnk-tutorial-jobs] esercitazione.

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
