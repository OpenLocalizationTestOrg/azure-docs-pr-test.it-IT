---
title: Introduzione ai dispositivi gemelli dell'hub IoT di Azure (Java) | Microsoft Docs
description: Come usare i dispositivi gemelli dell'hub IoT di Azure per aggiungere tag e quindi usare una query dell'hub IoT. Usare Azure IoT SDK per dispositivi per Java per implementare l'app per i dispositivi e Azure IoT SDK per servizi per Java per implementare un'app di servizio che aggiunge i tag ed esegue la query dell'hub IoT.
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
ms.openlocfilehash: 583cfcb9442c7be0a41aa1bc0f743bf8cf863665
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-device-twins-java"></a><span data-ttu-id="8a5ec-104">Introduzione ai dispositivi gemelli (Java)</span><span class="sxs-lookup"><span data-stu-id="8a5ec-104">Get started with device twins (Java)</span></span>

[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="8a5ec-105">In questa esercitazione vengono create due app console Java:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-105">In this tutorial, you create two Java console apps:</span></span>

* <span data-ttu-id="8a5ec-106">**add-tags-query**, un'app back-end .Java che aggiunge tag ed effettua query sui dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-106">**add-tags-query**, a Java back-end app that adds tags and queries device twins.</span></span>
* <span data-ttu-id="8a5ec-107">**simulated-device**, un'app per dispositivi Java che si connette all'hub IoT e segnala la condizione di connettività usando una proprietà segnalata.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-107">**simulated-device**, a Java device app that that connects to your IoT hub and reports its connectivity condition using a reported property.</span></span>

> [!NOTE]
> <span data-ttu-id="8a5ec-108">L'articolo [Azure IoT SDK](iot-hub-devguide-sdks.md) contiene informazioni sui componenti Azure IoT SDK che consentono di compilare le app back-end e per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-108">The article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>

<span data-ttu-id="8a5ec-109">Per completare questa esercitazione, sono necessari:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="8a5ec-110">[Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) più recente</span><span class="sxs-lookup"><span data-stu-id="8a5ec-110">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="8a5ec-111">Maven 3</span><span class="sxs-lookup"><span data-stu-id="8a5ec-111">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="8a5ec-112">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-112">An active Azure account.</span></span> <span data-ttu-id="8a5ec-113">Se non si dispone di un account, è possibile crearne uno [gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-113">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="8a5ec-114">Se si preferisce creare l'identità del dispositivo a livello di programmazione, leggere la sezione corrispondente nell'articolo [Connettere il dispositivo all'hub IoT usando Java](iot-hub-java-java-getstarted.md#create-a-device-identity).</span><span class="sxs-lookup"><span data-stu-id="8a5ec-114">If you prefer to create the device identity programmatically, read the corresponding section in the [Connect your device to your IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="8a5ec-115">Creare l'app di servizio</span><span class="sxs-lookup"><span data-stu-id="8a5ec-115">Create the service app</span></span>

<span data-ttu-id="8a5ec-116">In questa sezione si crea a un'app Java che aggiunge i metadati della posizione come tag al dispositivo gemello nell'hub IoT associato a **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-116">In this section, you create a Java app that adds location metadata as a tag to the device twin in IoT Hub associated with **myDeviceId**.</span></span> <span data-ttu-id="8a5ec-117">L'app esegue innanzitutto una query dell'hub IoT per i dispositivi che si trovano negli Stati Uniti, quindi per i dispositivi che segnalano una connessione di rete tramite cellulare.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-117">The app first queries IoT hub for devices located in the US, and then for devices that report a cellular network connection.</span></span>

1. <span data-ttu-id="8a5ec-118">Nel computer di sviluppo creare una cartella vuota denominata `iot-java-twin-getstarted`.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-118">On your development machine, create an empty folder called `iot-java-twin-getstarted`.</span></span>

1. <span data-ttu-id="8a5ec-119">Nella cartella `iot-java-twin-getstarted` creare un progetto Maven denominato **add-tags-query** eseguendo questo comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-119">In the `iot-java-twin-getstarted` folder, create a Maven project called **add-tags-query** using the following command at your command prompt.</span></span> <span data-ttu-id="8a5ec-120">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-120">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=add-tags-query -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="8a5ec-121">Al prompt dei comandi passare alla cartella `add-tags-query`.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-121">At your command prompt, navigate to the `add-tags-query` folder.</span></span>

1. <span data-ttu-id="8a5ec-122">In un editor di testo aprire il file `pom.xml` nella cartella `add-tags-query` e aggiungere la dipendenza seguente al nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-122">Using a text editor, open the `pom.xml` file in the `add-tags-query` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="8a5ec-123">Questa dipendenza consente di usare il pacchetto **iot-service-client** nell'app per comunicare con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-123">This dependency enables you to use the **iot-service-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="8a5ec-124">È possibile cercare la versione più recente di **iot-service-client** usando la [ricerca di Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="8a5ec-124">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="8a5ec-125">Aggiungere il nodo **build** seguente dopo il nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-125">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="8a5ec-126">Questa configurazione indica a Maven di usare Java 1.8 per compilare l'app:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-126">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="8a5ec-127">Salvare e chiudere il file `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-127">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="8a5ec-128">Aprire il file `add-tags-query\src\main\java\com\mycompany\app\App.java` in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-128">Using a text editor, open the `add-tags-query\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="8a5ec-129">Aggiungere al file le istruzioni **import** seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-129">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.devicetwin.*;
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;

    import java.io.IOException;
    import java.util.HashSet;
    import java.util.Set;
    ```

1. <span data-ttu-id="8a5ec-130">Aggiungere le variabili a livello di classe seguenti alla classe **App** .</span><span class="sxs-lookup"><span data-stu-id="8a5ec-130">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="8a5ec-131">Sostituire `{youriothubconnectionstring}` con la stringa di connessione dell'hub IoT indicata nella sezione *Creare un hub IoT*:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-131">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    public static final String region = "US";
    public static final String plant = "Redmond43";
    ```

1. <span data-ttu-id="8a5ec-132">Aggiornare la firma del metodo **main** affinché includa la clausola `throws`:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-132">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

1. <span data-ttu-id="8a5ec-133">Aggiungere il codice seguente al metodo **main** per creare gli oggetti **DeviceTwin** e **DeviceTwinDevice**.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-133">Add the following code to the **main** method to create the **DeviceTwin** and **DeviceTwinDevice** objects.</span></span> <span data-ttu-id="8a5ec-134">L'oggetto **DeviceTwin** gestisce la comunicazione con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-134">The **DeviceTwin** object handles the communication with your IoT hub.</span></span> <span data-ttu-id="8a5ec-135">L'oggetto **DeviceTwinDevice** rappresenta un dispositivo gemello con le relative proprietà e tag:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-135">The **DeviceTwinDevice** object represents the device twin with its properties and tags:</span></span>

    ```java
    // Get the DeviceTwin and DeviceTwinDevice objects
    DeviceTwin twinClient = DeviceTwin.createFromConnectionString(iotHubConnectionString);
    DeviceTwinDevice device = new DeviceTwinDevice(deviceId);
    ```

1. <span data-ttu-id="8a5ec-136">Aggiungere il blocco `try/catch` seguente al metodo **main**:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-136">Add the following `try/catch` block to the **main** method:</span></span>

    ```java
    try {
      // Code goes here
    } catch (IotHubException e) {
      System.out.println(e.getMessage());
    } catch (IOException e) {
      System.out.println(e.getMessage());
    }
    ```

1. <span data-ttu-id="8a5ec-137">Per aggiornare i tag del dispositivo gemello **region** e **plant** nel dispositivo gemello, aggiungere il codice seguente nel blocco `try`:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-137">To update the **region** and **plant** device twin tags in your device twin, add the following code in the `try` block:</span></span>

    ```java
    // Get the device twin from IoT Hub
    System.out.println("Device twin before update:");
    twinClient.getTwin(device);
    System.out.println(device);

    // Update device twin tags if they are different
    // from the existing values
    String currentTags = device.tagsToString();
    if ((!currentTags.contains("region=" + region) && !currentTags.contains("plant=" + plant))) {
      // Create the tags and attach them to the DeviceTwinDevice object
      Set<Pair> tags = new HashSet<Pair>();
      tags.add(new Pair("region", region));
      tags.add(new Pair("plant", plant));
      device.setTags(tags);

      // Update the device twin in IoT Hub
      System.out.println("Updating device twin");
      twinClient.updateTwin(device);
    }

    // Retrieve the device twin with the tag values from IoT Hub
    System.out.println("Device twin after update:");
    twinClient.getTwin(device);
    System.out.println(device);
    ```

1. <span data-ttu-id="8a5ec-138">Per eseguire una query sui dispositivi gemelli nell'hub IoT, aggiungere il codice seguente al blocco `try` dopo il codice aggiunto nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-138">To query the device twins in IoT hub, add the following code to the `try` block after the code you added in the previous step.</span></span> <span data-ttu-id="8a5ec-139">Il codice esegue due query.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-139">The code runs two queries.</span></span> <span data-ttu-id="8a5ec-140">Ogni query restituisce un massimo di 100 dispositivi:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-140">Each query returns a maximum of 100 devices:</span></span>

    ```java
    // Query the device twins in IoT Hub
    System.out.println("Devices in Redmond:");

    // Construct the query
    SqlQuery sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43'", null);

    // Run the query, returning a maximum of 100 devices
    Query twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 100);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }

    System.out.println("Devices in Redmond using a cellular network:");

    // Construct the query
    sqlQuery = SqlQuery.createSqlQuery("*", SqlQuery.FromType.DEVICES, "tags.plant='Redmond43' AND properties.reported.connectivityType = 'cellular'", null);

    // Run the query, returning a maximum of 100 devices
    twinQuery = twinClient.queryTwin(sqlQuery.getQuery(), 3);
    while (twinClient.hasNextDeviceTwin(twinQuery)) {
      DeviceTwinDevice d = twinClient.getNextDeviceTwin(twinQuery);
      System.out.println(d.getDeviceId());
    }
    ```

1. <span data-ttu-id="8a5ec-141">Salvare e chiudere il file `add-tags-query\src\main\java\com\mycompany\app\App.java`</span><span class="sxs-lookup"><span data-stu-id="8a5ec-141">Save and close the `add-tags-query\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="8a5ec-142">Compilare l'app **add-tags-query** e correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-142">Build the **add-tags-query** app and correct any errors.</span></span> <span data-ttu-id="8a5ec-143">Al prompt dei comandi passare alla cartella `add-tags-query` ed eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-143">At your command prompt, navigate to the `add-tags-query` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="8a5ec-144">Creare un'app per dispositivi</span><span class="sxs-lookup"><span data-stu-id="8a5ec-144">Create a device app</span></span>

<span data-ttu-id="8a5ec-145">In questa sezione si crea un'app console Java che imposta un valore di proprietà restituito che viene inviato all'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-145">In this section, you create a Java console app that sets a reported property value that is sent to IoT Hub.</span></span>

1. <span data-ttu-id="8a5ec-146">Nella cartella `iot-java-twin-getstarted` creare un progetto Maven denominato **simulated-device** usando il comando seguente nel prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-146">In the `iot-java-twin-getstarted` folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="8a5ec-147">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-147">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="8a5ec-148">Al prompt dei comandi passare alla cartella `simulated-device`.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-148">At your command prompt, navigate to the `simulated-device` folder.</span></span>

1. <span data-ttu-id="8a5ec-149">In un editor di testo aprire il file `pom.xml` nella cartella `simulated-device` e aggiungere le dipendenze seguenti al nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-149">Using a text editor, open the `pom.xml` file in the `simulated-device` folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="8a5ec-150">Questa dipendenza consente di usare il pacchetto **iot-device-client** nell'app per comunicare con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-150">This dependency enables you to use the **iot-device-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="8a5ec-151">È possibile cercare la versione più recente di **iot-device-client** usando la [ricerca di Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="8a5ec-151">You can check for the latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="8a5ec-152">Aggiungere il nodo **build** seguente dopo il nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-152">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="8a5ec-153">Questa configurazione indica a Maven di usare Java 1.8 per compilare l'app:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-153">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="8a5ec-154">Salvare e chiudere il file `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-154">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="8a5ec-155">Aprire il file `simulated-device\src\main\java\com\mycompany\app\App.java` in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-155">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="8a5ec-156">Aggiungere al file le istruzioni **import** seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-156">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="8a5ec-157">Aggiungere le variabili a livello di classe seguenti alla classe **App** .</span><span class="sxs-lookup"><span data-stu-id="8a5ec-157">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="8a5ec-158">Sostituzione di `{youriothubname}` con il nome dell'hub IoT e di `{yourdevicekey}` con il valore della chiave del dispositivo generato nella sezione *Creare un'identità del dispositivo*:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-158">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myDeviceId";
    ```

    <span data-ttu-id="8a5ec-159">Questa app di esempio usa la variabile **protocol** quando crea un'istanza di un oggetto **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-159">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="8a5ec-160">Attualmente per usare le funzionalità del dispositivo gemello è necessario usare il protocollo MQTT.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-160">Currently, to use device twin features you must use the MQTT protocol.</span></span>

1. <span data-ttu-id="8a5ec-161">Al metodo **main** aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-161">Add the following code to the **main** method to:</span></span>
    * <span data-ttu-id="8a5ec-162">Creare un client del dispositivo per comunicare con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-162">Create a device client to communicate with IoT Hub.</span></span>
    * <span data-ttu-id="8a5ec-163">Creare un **Device** oggetto per archiviare le proprietà dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-163">Create a **Device** object to store the device twin properties.</span></span>

    ```java
    DeviceClient client = new DeviceClient(connString, protocol);

    // Create a Device object to store the device twin properties
    Device dataCollector = new Device() {
      // Print details when a property value changes
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context) {
        System.out.println(propertyKey + " changed to " + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="8a5ec-164">Aggiungere il codice seguente al metodo **main** per creare una proprietà segnalata **connectivityType** e inviarla all'IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-164">Add the following code to the **main** method to create a **connectivityType** reported property and send it to IoT Hub:</span></span>

    ```java
    try {
      // Open the DeviceClient and start the device twin services.
      client.open();
      client.startDeviceTwin(new DeviceTwinStatusCallBack(), null, dataCollector, null);

      // Create a reported property and send it to your IoT hub.
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

1. <span data-ttu-id="8a5ec-165">Alla fine del metodo **main** aggiungere il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-165">Add the following code to the end of the **main** method.</span></span> <span data-ttu-id="8a5ec-166">Attendere che il tasto **Invio** consenta all'IoT Hub di segnalare lo stato delle operazioni del dispositivo gemello:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-166">Waiting for the **Enter** key allows time for IoT Hub to report the status of the device twin operations:</span></span>

    ```java
    System.out.println("Press any key to exit...");

    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();

    dataCollector.clean();
    client.close();
    ```

1. <span data-ttu-id="8a5ec-167">Salvare e chiudere il file `simulated-device\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-167">Save and close the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="8a5ec-168">Compilare l'app **simulated-device** e correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-168">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="8a5ec-169">Al prompt dei comandi passare alla cartella `simulated-device` ed eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-169">At your command prompt, navigate to the `simulated-device` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="8a5ec-170">Eseguire le app</span><span class="sxs-lookup"><span data-stu-id="8a5ec-170">Run the apps</span></span>

<span data-ttu-id="8a5ec-171">A questo punto è possibile eseguire le app console.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-171">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="8a5ec-172">Al prompt dei comandi nella cartella `add-tags-query` eseguire il comando seguente per eseguire l'app del servizio **add-tags-query**:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-172">At a command prompt in the `add-tags-query` folder, run the following command to run the **add-tags-query** service app:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![App del servizio hub IoT Java per aggiornare i valori dei tag ed eseguire query di dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-1.png)

    <span data-ttu-id="8a5ec-174">È possibile visualizzare i tag **plant** e **region** aggiunti al dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-174">You can see the **plant** and **region** tags added to the device twin.</span></span> <span data-ttu-id="8a5ec-175">Solo la prima query restituisce il dispositivo, non la seconda.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-175">The first query returns your device, but the second does not.</span></span>

1. <span data-ttu-id="8a5ec-176">Al prompt dei comandi nella cartella `simulated-device` eseguire il comando seguente per aggiungere la proprietà segnalata **connectivityType** al dispositivo gemello:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-176">At a command prompt in the `simulated-device` folder, run the following command to add the **connectivityType** reported property to the device twin:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Il client del dispositivo aggiunge la proprietà segnalata **connectivityType**](media/iot-hub-java-java-twin-getstarted/device-app-1.png)

1. <span data-ttu-id="8a5ec-178">Al prompt dei comandi nella cartella `add-tags-query` eseguire il comando seguente per eseguire l'app del servizio **add-tags-query** una seconda volta:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-178">At a command prompt in the `add-tags-query` folder, run the following command to run the **add-tags-query** service app a second time:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![App del servizio hub IoT Java per aggiornare i valori dei tag ed eseguire query di dispositivo](media/iot-hub-java-java-twin-getstarted/service-app-2.png)

    <span data-ttu-id="8a5ec-180">Ora che il dispositivo ha inviato la proprietà **connectivityType** all'hub IoT, la seconda query restituisce il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-180">Now your device has sent the **connectivityType** property to IoT Hub, the second query returns your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a5ec-181">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a5ec-181">Next steps</span></span>

<span data-ttu-id="8a5ec-182">In questa esercitazione è stato configurato un nuovo hub IoT nel Portale di Azure ed è stata quindi creata un'identità del dispositivo nel registro di identità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-182">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="8a5ec-183">Sono stati aggiunti i metadati del dispositivo come tag da un'app back-end ed è stata scritta un'app per dispositivo per segnalare le informazioni sulla connettività del dispositivo nel dispositivo gemello.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-183">You added device metadata as tags from a back-end app, and wrote a device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="8a5ec-184">Si è anche appreso come effettuare una query delle informazioni del dispositivo gemello usando il linguaggio di query simile a SQL dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8a5ec-184">You also learned how to query the device twin information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="8a5ec-185">Per altre informazioni, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a5ec-185">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="8a5ec-186">Per inviare dati di telemetria dai dispositivi, vedere l'esercitazione [Introduzione all'hub IoT](iot-hub-java-java-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="8a5ec-186">Send telemetry from devices with the [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="8a5ec-187">Per controllare i dispositivi in modo interattivo, ad esempio per attivare un ventilatore da un'app controllata dall'utente, vedere l'esercitazione [Usare metodi diretti](iot-hub-java-java-direct-methods.md).</span><span class="sxs-lookup"><span data-stu-id="8a5ec-187">Control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-java-java-twin-getstarted/invoke-method.png
[8]: ./media/iot-hub-java-java-twin-getstarted/device-listen.png
[9]: ./media/iot-hub-java-java-twin-getstarted/device-respond.png

<!-- Links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
