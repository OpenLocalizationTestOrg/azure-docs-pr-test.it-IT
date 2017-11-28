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
# <a name="get-started-with-device-twins-java"></a><span data-ttu-id="204d0-104">Introduzione ai dispositivi gemelli (Java)</span><span class="sxs-lookup"><span data-stu-id="204d0-104">Get started with device twins (Java)</span></span>

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="204d0-105">In questa esercitazione vengono create due app console Java:</span><span class="sxs-lookup"><span data-stu-id="204d0-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="204d0-106">**add-tags-query**, un'app back-end .Java che aggiunge tag ed effettua query sui dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="204d0-106">**add-tags-query**, a Java back-end app that adds tags and queries device twins.</span></span>
* <span data-ttu-id="204d0-107">**dispositivo simulato**, un'app di dispositivo Java che che si connette l'hub IoT tooyour e i report utilizzando una proprietà segnalata la condizione di connettività.</span><span class="sxs-lookup"><span data-stu-id="204d0-107">**simulated-device**, a Java device app that that connects tooyour IoT hub and reports its connectivity condition using a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="204d0-108">articolo Hello [Azure IoT SDK](iot-hub-devguide-sdks.md) fornisce informazioni su Azure IoT SDK hello che è possibile utilizzare toobuild applicazioni back-end sia sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="204d0-108">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

<span data-ttu-id="204d0-109">toocomplete questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="204d0-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="204d0-110">versione più recente Hello [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="204d0-110">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="204d0-111">Maven 3</span><span class="sxs-lookup"><span data-stu-id="204d0-111">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="204d0-112">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="204d0-112">An active Azure account.</span></span> <span data-ttu-id="204d0-113">Se non si dispone di un account, è possibile crearne uno [gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="204d0-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="204d0-114">Se si preferisce l'identità del dispositivo hello toocreate a livello di codice, leggere una sezione corrispondente di hello in hello [connessione hub IoT tooyour dispositivo utilizzando Java](iot-hub-java-java-getstarted.md#create-a-device-identity) articolo.</span><span class="sxs-lookup"><span data-stu-id="204d0-114">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="204d0-115">Creare l'applicazione di servizio hello</span><span class="sxs-lookup"><span data-stu-id="204d0-115">Create hello service app</span></span>

<span data-ttu-id="204d0-116">In questa sezione si crea un'applicazione Java che aggiunge metadati percorso come una coppia di dispositivo toohello tag nell'IoT Hub è associata a **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="204d0-116">In this section, you create a Java app that adds location metadata as a tag toohello device twin in IoT Hub associated with **myDeviceId**.</span></span> <span data-ttu-id="204d0-117">app Hello innanzitutto eseguita una query hub IoT per dispositivi che si trovano in hello Stati Uniti, quindi per i dispositivi che sono una connessione di rete cellulare.</span><span class="sxs-lookup"><span data-stu-id="204d0-117">hello app first queries IoT hub for devices located in hello US, and then for devices that report a cellular network connection.</span></span>

1. <span data-ttu-id="204d0-118">Nel computer di sviluppo creare una cartella vuota denominata `iot-java-twin-getstarted`.</span><span class="sxs-lookup"><span data-stu-id="204d0-118">On your development machine, create an empty folder called `iot-java-twin-getstarted`.</span></span>

1. <span data-ttu-id="204d0-119">In hello `iot-java-twin-getstarted` cartella, creare un progetto di Maven denominato **aggiungere-tag-query** utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="204d0-119">In hello `iot-java-twin-getstarted` folder, create a Maven project called **add-tags-query** using hello following command at your command prompt.</span></span> <span data-ttu-id="204d0-120">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="204d0-120">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="204d0-121">Al prompt dei comandi, passare toohello `add-tags-query` cartella.</span><span class="sxs-lookup"><span data-stu-id="204d0-121">At your command prompt, navigate toohello `add-tags-query` folder.</span></span>

1. <span data-ttu-id="204d0-122">Utilizzando un editor di testo, aprire hello `pom.xml` file hello `add-tags-query` cartella e aggiungere hello seguente dipendenza toohello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="204d0-122">Using a text editor, open hello `pom.xml` file in hello `add-tags-query` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="204d0-123">Questa dipendenza consente hello toouse **client di servizi iot** pacchetto in toocommunicate l'app con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="204d0-123">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="204d0-124">È possibile verificare la versione più recente di hello di **client di servizi iot** utilizzando [ricerca Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="204d0-124">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="204d0-125">Aggiungere il seguente hello **compilare** nodo dopo hello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="204d0-125">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="204d0-126">Questa configurazione indica Maven toouse Java toobuild 1.8 hello app:</span><span class="sxs-lookup"><span data-stu-id="204d0-126">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="204d0-127">Salvare e chiudere hello `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="204d0-127">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="204d0-128">Utilizzando un editor di testo, aprire hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="204d0-128">Using a text editor, open hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="204d0-129">Aggiungere il seguente hello **importare** file toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="204d0-129">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. <span data-ttu-id="204d0-130">Aggiungere hello seguenti variabili a livello di classe toohello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="204d0-130">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="204d0-131">Sostituire `{youriothubconnectionstring}` con la stringa di connessione hub IoT è stata annotata nella hello *creare un IoT Hub* sezione:</span><span class="sxs-lookup"><span data-stu-id="204d0-131">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. <span data-ttu-id="204d0-132">Hello aggiornamento **principale** seguente hello tooinclude firma di metodo `throws` clausola:</span><span class="sxs-lookup"><span data-stu-id="204d0-132">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. <span data-ttu-id="204d0-133">Aggiungere i seguenti toohello codice hello **principale** hello toocreate metodo **DeviceTwin** e **DeviceTwinDevice** oggetti.</span><span class="sxs-lookup"><span data-stu-id="204d0-133">Add hello following code toohello **main** method toocreate hello **DeviceTwin** and **DeviceTwinDevice** objects.</span></span> <span data-ttu-id="204d0-134">Hello **DeviceTwin** oggetto gestisce la comunicazione con l'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="204d0-134">hello **DeviceTwin** object handles hello communication with your IoT hub.</span></span> <span data-ttu-id="204d0-135">Hello **DeviceTwinDevice** oggetto rappresenta un doppio dispositivo hello con le proprietà e i tag:</span><span class="sxs-lookup"><span data-stu-id="204d0-135">hello **DeviceTwinDevice** object represents hello device twin with its properties and tags:</span></span>

    ```java
    // Get hello DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. <span data-ttu-id="204d0-136">Aggiungere il seguente hello `try/catch` blocco toohello **principale** metodo:</span><span class="sxs-lookup"><span data-stu-id="204d0-136">Add hello following `try/catch` block toohello **main** method:</span></span>

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="204d0-137">hello tooupdate **area** e **impianto** tag doppi dispositivo doppi del dispositivo, aggiungere hello seguente di codice hello `try` blocco:</span><span class="sxs-lookup"><span data-stu-id="204d0-137">tooupdate hello **region** and **plant** device twin tags in your device twin, add hello following code in hello `try` block:</span></span>

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

1. <span data-ttu-id="204d0-138">gemelli di dispositivo hello tooquery nell'hub IoT, aggiungere hello seguente codice toohello `try` blocco dopo il codice hello aggiunto nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="204d0-138">tooquery hello device twins in IoT hub, add hello following code toohello `try` block after hello code you added in hello previous step.</span></span> <span data-ttu-id="204d0-139">codice Hello esegue due query.</span><span class="sxs-lookup"><span data-stu-id="204d0-139">hello code runs two queries.</span></span> <span data-ttu-id="204d0-140">Ogni query restituisce un massimo di 100 dispositivi:</span><span class="sxs-lookup"><span data-stu-id="204d0-140">Each query returns a maximum of 100 devices:</span></span>

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

1. <span data-ttu-id="204d0-141">Salvare e chiudere hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span><span class="sxs-lookup"><span data-stu-id="204d0-141">Save and close hello `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="204d0-142">Compilare hello **aggiungere-tag-query** app e correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="204d0-142">Build hello **add-tags-query** app and correct any errors.</span></span> <span data-ttu-id="204d0-143">Al prompt dei comandi, passare toohello `add-tags-query` cartella e hello esecuzione comando seguente:</span><span class="sxs-lookup"><span data-stu-id="204d0-143">At your command prompt, navigate toohello `add-tags-query` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="204d0-144">Creare un'app per dispositivi</span><span class="sxs-lookup"><span data-stu-id="204d0-144">Create a device app</span></span>

<span data-ttu-id="204d0-145">In questa sezione si crea un'applicazione console Java che imposta un valore di proprietà restituito che viene inviato tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="204d0-145">In this section, you create a Java console app that sets a reported property value that is sent tooIoT Hub.</span></span>

1. <span data-ttu-id="204d0-146">In hello `iot-java-twin-getstarted` cartella, creare un progetto di Maven denominato **dispositivo simulato** utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="204d0-146">In hello `iot-java-twin-getstarted` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="204d0-147">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="204d0-147">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="204d0-148">Al prompt dei comandi, passare toohello `simulated-device` cartella.</span><span class="sxs-lookup"><span data-stu-id="204d0-148">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="204d0-149">Utilizzando un editor di testo, aprire hello `pom.xml` file hello `simulated-device` cartella e aggiungere hello seguente dipendenze toohello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="204d0-149">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="204d0-150">Questa dipendenza consente hello toouse **client di dispositivi iot** pacchetto in toocommunicate l'app con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="204d0-150">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="204d0-151">È possibile verificare la versione più recente di hello di **client di dispositivi iot** utilizzando [ricerca Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="204d0-151">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="204d0-152">Aggiungere il seguente hello **compilare** nodo dopo hello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="204d0-152">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="204d0-153">Questa configurazione indica Maven toouse Java toobuild 1.8 hello app:</span><span class="sxs-lookup"><span data-stu-id="204d0-153">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="204d0-154">Salvare e chiudere hello `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="204d0-154">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="204d0-155">Utilizzando un editor di testo, aprire hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="204d0-155">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="204d0-156">Aggiungere il seguente hello **importare** file toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="204d0-156">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="204d0-157">Aggiungere hello seguenti variabili a livello di classe toohello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="204d0-157">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="204d0-158">Sostituzione di `{youriothubname}` con il nome di hub IoT, e `{yourdevicekey}` con il valore della chiave di hello dispositivo è stato generato in hello *creare un'identità del dispositivo* sezione:</span><span class="sxs-lookup"><span data-stu-id="204d0-158">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    <span data-ttu-id="204d0-159">Questa app di esempio utilizza hello **protocollo** variabile quando si crea un'istanza di un **DeviceClient** oggetto.</span><span class="sxs-lookup"><span data-stu-id="204d0-159">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="204d0-160">Attualmente, toouse doppi le funzionalità del dispositivo è necessario utilizzare il protocollo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="204d0-160">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="204d0-161">Aggiungere i seguenti toohello codice hello **principale** metodo:</span><span class="sxs-lookup"><span data-stu-id="204d0-161">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="204d0-162">Creare un toocommunicate di client del dispositivo con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="204d0-162">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="204d0-163">Creare un **dispositivo** toostore hello dispositivo due proprietà dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="204d0-163">Create a **Device** object toostore hello device twin properties.</span></span>

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

1. <span data-ttu-id="204d0-164">Aggiungere hello seguente codice toohello **principale** toocreate metodo un **connectivityType** segnalati proprietà e inviarlo tooIoT Hub:</span><span class="sxs-lookup"><span data-stu-id="204d0-164">Add hello following code toohello **main** method toocreate a **connectivityType** reported property and send it tooIoT Hub:</span></span>

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

1. <span data-ttu-id="204d0-165">Aggiungere hello successivo toohello codice alla fine di hello **principale** metodo.</span><span class="sxs-lookup"><span data-stu-id="204d0-165">Add hello following code toohello end of hello **main** method.</span></span> <span data-ttu-id="204d0-166">In attesa di hello **invio** chiave consente ora per lo stato di hello tooreport IoT Hub di operazioni di doppi hello dispositivo:</span><span class="sxs-lookup"><span data-stu-id="204d0-166">Waiting for hello **Enter** key allows time for IoT Hub tooreport hello status of hello device twin operations:</span></span>

    ```java
    System.out.println("Press any key tooexit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. <span data-ttu-id="204d0-167">Salvare e chiudere hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="204d0-167">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="204d0-168">Compilare hello **dispositivo simulato** app e correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="204d0-168">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="204d0-169">Al prompt dei comandi, passare toohello `simulated-device` cartella e hello esecuzione comando seguente:</span><span class="sxs-lookup"><span data-stu-id="204d0-169">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="204d0-170">Eseguire App hello</span><span class="sxs-lookup"><span data-stu-id="204d0-170">Run hello apps</span></span>

<span data-ttu-id="204d0-171">Si è ora pronto toorun hello console app.</span><span class="sxs-lookup"><span data-stu-id="204d0-171">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="204d0-172">Al prompt dei comandi in hello `add-tags-query` cartella, eseguire hello successivo comando toorun hello **aggiungere-tag-query** del servizio app:</span><span class="sxs-lookup"><span data-stu-id="204d0-172">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub Java servizio app tooupdate contrassegnare valori ed eseguire query di dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    <span data-ttu-id="204d0-174">È possibile visualizzare hello **impianto** e **area** tag aggiunto toohello gemelli di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="204d0-174">You can see hello **plant** and **region** tags added toohello device twin.</span></span> <span data-ttu-id="204d0-175">Hello prima query restituisce il dispositivo, ma hello in secondo luogo non.</span><span class="sxs-lookup"><span data-stu-id="204d0-175">hello first query returns your device, but hello second does not.</span></span>

1. <span data-ttu-id="204d0-176">Al prompt dei comandi in hello `simulated-device` cartella, eseguire hello successivo comando tooadd hello **connectivityType** segnalati due dispositivi di proprietà toohello:</span><span class="sxs-lookup"><span data-stu-id="204d0-176">At a command prompt in hello `simulated-device` folder, run hello following command tooadd hello **connectivityType** reported property toohello device twin:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![client del dispositivo Hello aggiunge hello * * connectivityType * * segnalati proprietà](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. <span data-ttu-id="204d0-178">Al prompt dei comandi in hello `add-tags-query` cartella, eseguire hello successivo comando toorun hello **aggiungere-tag-query** una seconda volta del servizio app:</span><span class="sxs-lookup"><span data-stu-id="204d0-178">At a command prompt in hello `add-tags-query` folder, run hello following command toorun hello **add-tags-query** service app a second time:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![IoT Hub Java servizio app tooupdate contrassegnare valori ed eseguire query di dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    <span data-ttu-id="204d0-180">Ora che il dispositivo ha inviato hello **connectivityType** tooIoT proprietà Hub, seconda query hello restituisce il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="204d0-180">Now your device has sent hello **connectivityType** property tooIoT Hub, hello second query returns your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="204d0-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="204d0-181">Next steps</span></span>

<span data-ttu-id="204d0-182">In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità.</span><span class="sxs-lookup"><span data-stu-id="204d0-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="204d0-183">Aggiunti i metadati del dispositivo come tag da un'app di back-end e ha scritto informazioni di connettività un dispositivo app tooreport dispositivo in un doppio dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="204d0-183">You added device metadata as tags from a back-end app, and wrote a device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="204d0-184">È stato inoltre descritto come tooquery hello informazioni doppi dispositivo usando il linguaggio di query di hello IoT Hub simile a SQL.</span><span class="sxs-lookup"><span data-stu-id="204d0-184">You also learned how tooquery hello device twin information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="204d0-185">Hello utilizzare seguenti come risorse toolearn per:</span><span class="sxs-lookup"><span data-stu-id="204d0-185">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="204d0-186">Inviare i dati di telemetria dai dispositivi con hello [iniziare con l'IoT Hub](iot-hub-java-java-getstarted.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="204d0-186">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="204d0-187">Controllare i dispositivi in modo interattivo (ad esempio l'attivazione di una ventola da un'app controllata dall'utente) con hello [utilizzare metodi diretti](iot-hub-java-java-direct-methods.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="204d0-187">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
