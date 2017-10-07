---
title: i processi di aaaSchedule con IoT Hub di Azure (linguaggio) | Documenti Microsoft
description: "Come tooschedule un IoT Hub Azure tooinvoke un metodo diretto del processo e impostare una proprietà desiderata su più dispositivi. Utilizzare dispositivi Azure IoT hello SDK per Java tooimplement hello simulato dispositivo App e servizi IoT di Azure SDK per Java tooimplement un processo del servizio app toorun hello hello."
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dobett
ms.openlocfilehash: b1b05fa56c3ce96af0b33d4cca0dd54da0f4e927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a>Pianificare e trasmettere processi (Java)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Utilizzare i processi tooschedule e tenere traccia IoT Hub di Azure che aggiornano milioni di dispositivi. Usare i processi per:

* Aggiornare le proprietà desiderate
* Aggiornare i tag
* Richiamare metodi diretti

Un processo esegue il wrapping di una di queste azioni e le tracce hello esecuzione rispetto a un set di dispositivi. Una query di un doppio dispositivo definisce il set di hello di hello processo viene eseguito su dispositivi. Ad esempio, un'applicazione back-end è possibile utilizzare un tooinvoke processo un metodo diretto su 10.000 dispositivi che si riavvia dispositivi hello. È necessario specifica il set di hello di dispositivi con una query di due dispositivi e pianificare toorun processo hello in un secondo momento. avanzamento tiene traccia del processo Hello come tutti i dispositivi di hello di ricezione ed eseguire hello riavvio dirette del metodo.

toolearn informazioni su ciascuna di queste funzionalità, vedere:

* Dispositivo gemello e proprietà: [Introduzione ai dispositivi gemelli](iot-hub-java-java-twin-getstarted.md)
* Metodi diretti: [Guida per sviluppatori dell'hub IoT - Metodi diretti](iot-hub-devguide-direct-methods.md) ed [Esercitazione: Usare metodi diretti](iot-hub-java-java-direct-methods.md)

Questa esercitazione illustra come:

* Creare un'app per dispositivi che implementa un metodo diretto denominato **lockDoor**. Hello dispositivo app riceve inoltre le modifiche alle proprietà desiderato dai hello back-end app.
* Creare un'applicazione back-end che crea un hello toocall processo **lockDoor** metodo diretto su più dispositivi. Un altro processo invia proprietà desiderata Aggiorna dispositivi toomultiple.

Alla fine di hello di questa esercitazione, si dispone di un'applicazione console in java dispositivo e un'applicazione back-end di console java:

**dispositivo simulato** che connette l'hub IoT tooyour, implementa hello **lockDoor** indirizzare lo si desidera metodo e gestisce le modifiche alle proprietà.

**i processi di pianificazione** che usano hello toocall processi **lockDoor** diretto (metodo) e aggiornamento hello dispositivo doppi desiderato proprietà su più dispositivi.

> [!NOTE]
> articolo Hello [Azure IoT SDK](iot-hub-devguide-sdks.md) fornisce informazioni su Azure IoT SDK hello che è possibile utilizzare toobuild applicazioni back-end sia sul dispositivo.

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione, è necessario:

* versione più recente Hello [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Un account Azure attivo. Se non si dispone di un account, è possibile crearne uno [gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Se si preferisce l'identità del dispositivo hello toocreate a livello di codice, leggere una sezione corrispondente di hello in hello [connessione hub IoT tooyour dispositivo utilizzando Java](iot-hub-java-java-getstarted.md#create-a-device-identity) articolo. È inoltre possibile utilizzare hello [l'hub IOT Esplora](https://github.com/Azure/iothub-explorer) strumento tooadd un hub IoT tooyour di dispositivo.

## <a name="create-hello-service-app"></a>Creare l'applicazione di servizio hello

In questa sezione si crea un'app console Java che usa i processi per:

* Chiamare hello **lockDoor** metodo diretto su più dispositivi.
* Inviare i dispositivi toomultiple proprietà desiderate.

toocreate hello app:

1. Nel computer di sviluppo creare una cartella vuota denominata `iot-java-schedule-jobs`.

1. In hello `iot-java-schedule-jobs` cartella, creare un progetto di Maven denominato **pianificazione processi** utilizzando hello seguente comando al prompt dei comandi. Si noti che si tratta di un lungo comando singolo:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Al prompt dei comandi, passare toohello `schedule-jobs` cartella.

1. Utilizzando un editor di testo, aprire hello `pom.xml` file hello `schedule-jobs` cartella e aggiungere hello seguente dipendenza toohello **dipendenze** nodo. Questa dipendenza consente hello toouse **client di servizi iot** pacchetto in toocommunicate l'app con l'hub IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > È possibile verificare la versione più recente di hello di **client di servizi iot** utilizzando [ricerca Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

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

1. Salvare e chiudere hello `pom.xml` file.

1. Utilizzando un editor di testo, aprire hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.

1. Aggiungere il seguente hello **importare** file toohello istruzioni:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.DeviceTwinDevice;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Pair;
    import com.microsoft.azure.sdk.iot.service.devicetwin.Query;
    import com.microsoft.azure.sdk.iot.service.devicetwin.SqlQuery;
    import com.microsoft.azure.sdk.iot.service.jobs.JobClient;
    import com.microsoft.azure.sdk.iot.service.jobs.JobResult;
    import com.microsoft.azure.sdk.iot.service.jobs.JobStatus;

    import java.util.Date;
    import java.time.Instant;
    import java.util.HashSet;
    import java.util.Set;
    import java.util.UUID;
    ```

1. Aggiungere hello seguenti variabili a livello di classe toohello **App** classe. Sostituire `{youriothubconnectionstring}` con la stringa di connessione hub IoT è stata annotata nella hello *creare un IoT Hub* sezione:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. Aggiungere hello seguente metodo toohello **App** tooschedule classe un hello tooupdate processo **compilazione** e **Floor** le proprietà in un doppio dispositivo hello desiderate:

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule hello update twin job toorun now
      // against a single device
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleUpdateTwin(jobId, 
          "deviceId='" + deviceId + "'",
          twin,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling desired properties job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    }
    ```

1. tooschedule un hello toocall processo **lockDoor** metodo, aggiungere hello seguente metodo toohello **App** classe:

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now toocall hello lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set too5 seconds.
      System.out.println("Schedule job " + jobId + " for device " + deviceId);
      try {
        JobResult jobResult = jobClient.scheduleDeviceMethod(jobId,
          "deviceId='" + deviceId + "'",
          "lockDoor",
          5L, 5L, null,
          new Date(),
          maxExecutionTimeInSeconds);
        return jobResult;
      } catch (Exception e) {
        System.out.println("Exception scheduling direct method job: " + jobId);
        System.out.println(e.getMessage());
        return null;
      }
    };
    ```

1. toomonitor un processo, aggiungere hello seguente metodo toohello **App** classe:

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check hello job result until it's completed
        while(jobResult.getJobStatus() != JobStatus.completed)
        {
          Thread.sleep(100);
          jobResult = jobClient.getJob(jobId);
          System.out.println("Status " + jobResult.getJobStatus() + " for job " + jobId);
        }
        System.out.println("Final status " + jobResult.getJobStatus() + " for job " + jobId);
      } catch (Exception e) {
        System.out.println("Exception monitoring job: " + jobId);
        System.out.println(e.getMessage());
        return;
      }
    }
    ```

1. tooquery per i dettagli di hello dei processi di hello è stato eseguito, aggiungere al metodo hello:

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using hello time hello jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over hello list of jobs and print hello details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. Hello aggiornamento **principale** seguente hello tooinclude firma di metodo `throws` clausola:

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. toorun e monitoraggio di due processi in sequenza, aggiungere hello seguente codice toohello **principale** metodo:

    ```java
    // Record hello start time
    String start = Instant.now().toString();

    // Create JobClient
    JobClient jobClient = JobClient.createFromConnectionString(iotHubConnectionString);
    System.out.println("JobClient created with success");

    // Schedule twin job desired properties
    // Maximum concurrent jobs is 1 for Free and S1 tiers
    String desiredPropertiesJobId = "DPCMD" + UUID.randomUUID();
    scheduleJobSetDesiredProperties(jobClient, desiredPropertiesJobId);
    monitorJob(jobClient, desiredPropertiesJobId);

    // Schedule twin job direct method
    String directMethodJobId = "DMCMD" + UUID.randomUUID();
    scheduleJobCallDirectMethod(jobClient, directMethodJobId);
    monitorJob(jobClient, directMethodJobId);

    // Run a query tooshow hello job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. Salvare e chiudere hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file

1. Compilare hello **pianificazione processi** app e correggere eventuali errori. Al prompt dei comandi, passare toohello `schedule-jobs` cartella e hello esecuzione comando seguente:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>Creare un'app per dispositivi

In questa sezione si crea un'applicazione console Java che gestisce le proprietà desiderate inviate da una chiamata al metodo diretto hello IoT Hub e implementa di hello.

1. In hello `iot-java-schedule-jobs` cartella, creare un progetto di Maven denominato **dispositivo simulato** utilizzando hello seguente comando al prompt dei comandi. Si noti che si tratta di un lungo comando singolo:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Al prompt dei comandi, passare toohello `simulated-device` cartella.

1. Utilizzando un editor di testo, aprire hello `pom.xml` file hello `simulated-device` cartella e aggiungere hello seguente dipendenze toohello **dipendenze** nodo. Questa dipendenza consente hello toouse **client di dispositivi iot** pacchetto in toocommunicate l'app con l'hub IoT:

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > È possibile verificare la versione più recente di hello di **client di dispositivi iot** utilizzando [ricerca Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).

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

1. Salvare e chiudere hello `pom.xml` file.

1. Utilizzando un editor di testo, aprire hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.

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
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    Questa app di esempio utilizza hello **protocollo** variabile quando si crea un'istanza di un **DeviceClient** oggetto. Attualmente, toouse doppi le funzionalità del dispositivo è necessario utilizzare il protocollo MQTT hello.

1. tooprint dispositivo doppi notifiche toohello console, aggiungere il seguente hello annidati classe toohello **App** classe:

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. tooprint diretta metodo notifiche toohello console, aggiungere il seguente hello annidati classe toohello **App** classe:

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. chiamate dirette del metodo toohandle dall'IoT Hub, aggiungere il seguente hello annidati classe toohello **App** classe:

    ```java
    // Handler for direct method calls from IoT Hub
    protected static class DirectMethodCallback
        implements DeviceMethodCallback {
      @Override
      public DeviceMethodData call(String methodName, Object methodData, Object context) {
        DeviceMethodData deviceMethodData;
        switch (methodName) {
          case "lockDoor": {
            System.out.println("Executing direct method: " + methodName);
            deviceMethodData = new DeviceMethodData(METHOD_SUCCESS, "Executed direct method " + methodName);
            break;
          }
          default: {
            deviceMethodData = new DeviceMethodData(METHOD_NOT_DEFINED, "Not defined direct method " + methodName);
          }
        }
        // Notify IoT Hub of result
        return deviceMethodData;
      }
    }
    ```

1. Hello aggiornamento **principale** seguente hello tooinclude firma di metodo `throws` clausola:

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. Aggiungere i seguenti toohello codice hello **principale** metodo:
    * Creare un toocommunicate di client del dispositivo con l'IoT Hub.
    * Creare un **dispositivo** toostore hello dispositivo due proprietà dell'oggetto.

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object toomanage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. toostart hello dispositivo client servizi, aggiungere il seguente codice toohello hello **principale** metodo:

    ```java
    try {
      // Open hello DeviceClient
      // Start hello device twin services
      // Subscribe toodirect method calls
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);
      client.subscribeToDeviceMethod(new DirectMethodCallback(), null, new DirectMethodStatusCallback(), null);
    } catch (Exception e) {
      System.out.println("Exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.closeNow();
      System.out.println("Shutting down...");
    }
    ```

1. toowait per hello di hello utente toopress **invio** chiave prima della chiusura, aggiungere hello successivo toohello codice alla fine di hello **principale** metodo:

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. Salvare e chiudere hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.

1. Compilare hello **dispositivo simulato** app e correggere eventuali errori. Al prompt dei comandi, passare toohello `simulated-device` cartella e hello esecuzione comando seguente:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Eseguire App hello

Si è ora pronto toorun hello console app.

1. Al prompt dei comandi in hello `simulated-device` cartella, eseguire hello comando toostart hello dispositivo app ascolto delle modifiche di proprietà e chiamate dirette del metodo seguente:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![avvio Hello dispositivo client](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. Al prompt dei comandi in hello `schedule-jobs` cartella, eseguire hello successivo comando toorun hello **pianificazione processi** due processi di app toorun del servizio. Hello imposta innanzitutto i valori delle proprietà hello desiderato, chiamate secondo hello hello dirette del metodo:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![L'app di servizio dell'hub IoT Java crea due processi](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. app per dispositivi Hello gestisce hello desiderato modifica della proprietà e chiamate dirette del metodo hello:

    ![client del dispositivo Hello risponde toohello modifiche](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità. È stato creato un'applicazione back-end toorun due processi. primo processo Hello imposta valori di proprietà desiderati e secondo processo hello chiamato un metodo diretto.

Hello utilizzare seguenti come risorse toolearn per:

* Inviare i dati di telemetria dai dispositivi con hello [iniziare con l'IoT Hub](iot-hub-java-java-getstarted.md) esercitazione.
* Controllare i dispositivi in modo interattivo (ad esempio l'attivazione di una ventola da un'app controllata dall'utente) con hello [utilizzare metodi diretti](iot-hub-java-java-direct-methods.md) esercitazione.
