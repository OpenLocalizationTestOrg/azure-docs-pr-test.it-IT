---
title: aaaGet introduttiva gemelli dispositivi Azure IoT Hub (linguaggio) | Documenti Microsoft
description: "Modalità toouse IoT Hub Azure dispositivo gemelli tooadd tag e quindi utilizzare una query di IoT Hub. Utilizzare dispositivi Azure IoT hello SDK per Java tooimplement hello dispositivo app e il servizio di IoT di Azure SDK per Java tooimplement un'applicazione di servizio che consente di aggiungere tag hello ed esegue query IoT Hub hello hello."
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
ms.date: 07/04/2017
ms.author: dobett
ms.openlocfilehash: 25f6fc81471d59c62bcdc3766bb5c33f5733c930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-java"></a>Introduzione ai dispositivi gemelli (Java)

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

In questa esercitazione vengono create due app console Java:

* **add-tags-query**, un'app back-end .Java che aggiunge tag ed effettua query sui dispositivi gemelli.
* **dispositivo simulato**, un'app di dispositivo Java che che si connette l'hub IoT tooyour e i report utilizzando una proprietà segnalata la condizione di connettività.

> [!NOTE]
> articolo Hello [Azure IoT SDK](iot-hub-devguide-sdks.md) fornisce informazioni su Azure IoT SDK hello che è possibile utilizzare toobuild applicazioni back-end sia sul dispositivo.

toocomplete questa esercitazione, è necessario:

* versione più recente Hello [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Maven 3](https://maven.apache.org/install.html)
* Un account Azure attivo. Se non si dispone di un account, è possibile crearne uno [gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

Se si preferisce l'identità del dispositivo hello toocreate a livello di codice, leggere una sezione corrispondente di hello in hello [connessione hub IoT tooyour dispositivo utilizzando Java](iot-hub-java-java-getstarted.md#create-a-device-identity) articolo.

## <a name="create-hello-service-app"></a>Creare l'applicazione di servizio hello

In questa sezione si crea un'applicazione Java che aggiunge metadati percorso come una coppia di dispositivo toohello tag nell'IoT Hub è associata a **myDeviceId**. app Hello innanzitutto eseguita una query hub IoT per dispositivi che si trovano in hello Stati Uniti, quindi per i dispositivi che sono una connessione di rete cellulare.

1. Nel computer di sviluppo creare una cartella vuota denominata `iot-java-twin-getstarted`.

1. In hello `iot-java-twin-getstarted` cartella, creare un progetto di Maven denominato **aggiungere-tag-query** utilizzando hello seguente comando al prompt dei comandi. Si noti che si tratta di un lungo comando singolo:

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. Al prompt dei comandi, passare toohello `add-tags-query` cartella.

1. Utilizzando un editor di testo, aprire hello `pom.xml` file hello `add-tags-query` cartella e aggiungere hello seguente dipendenza toohello **dipendenze** nodo. Questa dipendenza consente hello toouse **client di servizi iot** pacchetto in toocommunicate l'app con l'hub IoT:

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

1. Utilizzando un editor di testo, aprire hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file.

1. Aggiungere il seguente hello **importare** file toohello istruzioni:

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. Aggiungere hello seguenti variabili a livello di classe toohello **App** classe. Sostituire `{youriothubconnectionstring}` con la stringa di connessione hub IoT è stata annotata nella hello *creare un IoT Hub* sezione:

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. Hello aggiornamento **principale** seguente hello tooinclude firma di metodo `throws` clausola:

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. Aggiungere i seguenti toohello codice hello **principale** hello toocreate metodo **DeviceTwin** e **DeviceTwinDevice** oggetti. Hello **DeviceTwin** oggetto gestisce la comunicazione con l'hub IoT hello. Hello **DeviceTwinDevice** oggetto rappresenta un doppio dispositivo hello con le proprietà e i tag:

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. Aggiungere il seguente hello `try/catch` blocco toohello **principale** metodo:

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. hello tooupdate **area** e **impianto** tag doppi dispositivo doppi del dispositivo, aggiungere hello seguente di codice hello `try` blocco:

    ```java
    // Get hello device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from hello existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create hello tags and attach them toohello DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update hello device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve hello device twin with hello tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. gemelli di dispositivo hello tooquery nell'hub IoT, aggiungere hello seguente codice toohello `try` blocco dopo il codice hello aggiunto nel passaggio precedente hello. codice Hello esegue due query. Ogni query restituisce un massimo di 100 dispositivi:

    ```java
    // Query hello device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct hello query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run hello query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct hello query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run hello query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. Salvare e chiudere hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file

1. Compilare hello **aggiungere-tag-query** app e correggere eventuali errori. Al prompt dei comandi, passare toohello `add-tags-query` cartella e hello esecuzione comando seguente:

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a>Creare un'app per dispositivi

In questa sezione si crea un'applicazione console Java che imposta un valore di proprietà restituito che viene inviato tooIoT Hub.

1. In hello `iot-java-twin-getstarted` cartella, creare un progetto di Maven denominato **dispositivo simulato** utilizzando hello seguente comando al prompt dei comandi. Si noti che si tratta di un lungo comando singolo:

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
    private static String deviceId = "myDeviceId";
    ```

    Questa app di esempio utilizza hello **protocollo** variabile quando si crea un'istanza di un **DeviceClient** oggetto. Attualmente, toouse doppi le funzionalità del dispositivo è necessario utilizzare il protocollo MQTT hello.

1. Aggiungere i seguenti toohello codice hello **principale** metodo:
    * Creare un toocommunicate di client del dispositivo con l'IoT Hub.
    * Creare un **dispositivo** toostore hello dispositivo due proprietà dell'oggetto.

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object toostore hello device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed too" + propertyValue);
      }
    };
    ```

1. Aggiungere hello seguente codice toohello **principale** toocreate metodo un **connectivityType** segnalati proprietà e inviarlo tooIoT Hub:

    ```java
    try {
      // Open hello DeviceClient and start hello device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it tooyour IoT hub.
      dataCollector.setReportedProp(new Property("connectivityType", "cellular"));
      client.sendReportedProperties(dataCollector.getReportedProp());
    }
    catch (Exception e) {
      System.out.println("On exception, shutting down \n" + " Cause: " + e.getCause() + " \n" + e.getMessage());
      dataCollector.clean();
      client.close();
      System.out.println("Shutting down...");
    }
    ```

1. Aggiungere hello successivo toohello codice alla fine di hello **principale** metodo. In attesa di hello **invio** chiave consente ora per lo stato di hello tooreport IoT Hub di operazioni di doppi hello dispositivo:

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. Salvare e chiudere hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.

1. Compilare hello **dispositivo simulato** app e correggere eventuali errori. Al prompt dei comandi, passare toohello `simulated-device` cartella e hello esecuzione comando seguente:

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a>Eseguire App hello

Si è ora pronto toorun hello console app.

1. Al prompt dei comandi in hello `add-tags-query` cartella, eseguire hello successivo comando toorun hello **aggiungere-tag-query** del servizio app:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub Java servizio app tooupdate contrassegnare valori ed eseguire query di dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    È possibile visualizzare hello **impianto** e **area** tag aggiunto toohello gemelli di dispositivo. Hello prima query restituisce il dispositivo, ma hello in secondo luogo non.

1. Al prompt dei comandi in hello `simulated-device` cartella, eseguire hello successivo comando tooadd hello **connectivityType** segnalati due dispositivi di proprietà toohello:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![client del dispositivo Hello aggiunge hello * * connectivityType * * segnalati proprietà](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. Al prompt dei comandi in hello `add-tags-query` cartella, eseguire hello successivo comando toorun hello **aggiungere-tag-query** una seconda volta del servizio app:

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub Java servizio app tooupdate contrassegnare valori ed eseguire query di dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    Ora che il dispositivo ha inviato hello **connectivityType** tooIoT proprietà Hub, seconda query hello restituisce il dispositivo.

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità. Aggiunti i metadati del dispositivo come tag da un'app di back-end e ha scritto informazioni di connettività un dispositivo app tooreport dispositivo in un doppio dispositivo hello. È stato inoltre descritto come tooquery hello informazioni doppi dispositivo usando il linguaggio di query di hello IoT Hub simile a SQL.

Hello utilizzare seguenti come risorse toolearn per:

* Inviare i dati di telemetria dai dispositivi con hello [iniziare con l'IoT Hub](iot-hub-java-java-getstarted.md) esercitazione.
* Controllare i dispositivi in modo interattivo (ad esempio l'attivazione di una ventola da un'app controllata dall'utente) con hello [utilizzare metodi diretti](iot-hub-java-java-direct-methods.md) esercitazione.

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
