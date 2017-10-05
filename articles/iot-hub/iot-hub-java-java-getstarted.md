---
title: Introduzione all'hub IoT di Azure (Java) | Microsoft Docs
description: Informazioni su come inviare messaggi da dispositivo a cloud all'hub IoT di Azure usando IoT SDK per Java. Creare un dispositivo simulato e app di servizio per registrare il dispositivo, inviare messaggi e leggere messaggi dall'hub IoT.
services: iot-hub
documentationcenter: java
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 70dae4a8-0e98-4c53-b5a5-9d6963abb245
ms.service: iot-hub
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 707356a49970bcd76a55ee1b8a6fbddf6a6ba390
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-device-to-your-iot-hub-using-java"></a><span data-ttu-id="940b5-104">Connettere il dispositivo all'hub IoT usando Java</span><span class="sxs-lookup"><span data-stu-id="940b5-104">Connect your device to your IoT hub using Java</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="940b5-105">Al termine di questa esercitazione si avranno tre app di console Java:</span><span class="sxs-lookup"><span data-stu-id="940b5-105">At the end of this tutorial, you have three Java console apps:</span></span>

* <span data-ttu-id="940b5-106">**create-device-identity**, che crea un'identità di dispositivo e una chiave di sicurezza associata per connettere l'app per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="940b5-106">**create-device-identity**, which creates a device identity and associated security key to connect your device app.</span></span>
* <span data-ttu-id="940b5-107">**read-d2c-messages**, che visualizza i dati di telemetria inviati dall'app per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="940b5-107">**read-d2c-messages**, which displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="940b5-108">**simulated-device**, che si connette all'hub IoT con l'identità del dispositivo creata in precedenza e invia un messaggio di telemetria ogni secondo usando il protocollo MQTT.</span><span class="sxs-lookup"><span data-stu-id="940b5-108">**simulated-device**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="940b5-109">L'articolo [Azure IoT SDK][lnk-hub-sdks] offre informazioni sui vari Azure IoT SDK che è possibile usare per compilare applicazioni da eseguire nei dispositivi e il backend della soluzione.</span><span class="sxs-lookup"><span data-stu-id="940b5-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both apps to run on devices and your solution back end.</span></span>

<span data-ttu-id="940b5-110">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="940b5-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="940b5-111">[Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) più recente</span><span class="sxs-lookup"><span data-stu-id="940b5-111">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span> 
* [<span data-ttu-id="940b5-112">Maven 3</span><span class="sxs-lookup"><span data-stu-id="940b5-112">Maven 3</span></span>](https://maven.apache.org/install.html) 
* <span data-ttu-id="940b5-113">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="940b5-113">An active Azure account.</span></span> <span data-ttu-id="940b5-114">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="940b5-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="940b5-115">Prendere infine nota del valore presente in **Chiave primaria**.</span><span class="sxs-lookup"><span data-stu-id="940b5-115">As a final step, make a note of the **Primary key** value.</span></span> <span data-ttu-id="940b5-116">Fare clic su **Endpoint** e sull'endpoint predefinito **Eventi**.</span><span class="sxs-lookup"><span data-stu-id="940b5-116">Then click **Endpoints** and the **Events** built-in endpoint.</span></span> <span data-ttu-id="940b5-117">Nel pannello **Proprietà** prendere nota del valore presente in **Nome compatibile con l'hub eventi** e dell'indirizzo **Endpoint compatibile con l'hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="940b5-117">On the **Properties** blade, make a note of the **Event Hub-compatible name** and the **Event Hub-compatible endpoint** address.</span></span> <span data-ttu-id="940b5-118">Questi tre valori sono necessari quando si crea l'app **read-d2c-messages**.</span><span class="sxs-lookup"><span data-stu-id="940b5-118">You need these three values when you create your **read-d2c-messages** app.</span></span>

![Pannello Messaggistica dell'hub IoT nel portale di Azure][6]

<span data-ttu-id="940b5-120">L'hub IoT è stato creato.</span><span class="sxs-lookup"><span data-stu-id="940b5-120">You have now created your IoT hub.</span></span> <span data-ttu-id="940b5-121">Si conoscono il nome host dell'hub IoT, la stringa di connessione dell'hub IoT, la chiave primaria dell'hub IoT, il nome e l'endpoint compatibili con l'hub eventi necessari per completare l'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="940b5-121">You have the IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need to complete this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="940b5-122">Creare un'identità del dispositivo</span><span class="sxs-lookup"><span data-stu-id="940b5-122">Create a device identity</span></span>
<span data-ttu-id="940b5-123">In questa sezione si scriverà un'app console Java che crea un'identità del dispositivo nel registro delle identità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="940b5-123">In this section, you create a Java console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="940b5-124">Un dispositivo non può connettersi all'hub IoT a meno che non abbia una voce nel registro di identità.</span><span class="sxs-lookup"><span data-stu-id="940b5-124">A device cannot connect to IoT hub unless it has an entry in the identity registry.</span></span> <span data-ttu-id="940b5-125">Per altre informazioni, vedere la sezione **Registro di identità** della [Guida per gli sviluppatori dell'hub IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="940b5-125">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="940b5-126">Quando si esegue questa app console vengono generati un ID dispositivo univoco e una chiave con cui il dispositivo può identificarsi quando invia messaggi da dispositivo a cloud all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="940b5-126">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="940b5-127">Creare una cartella vuota denominata iot-java-get-started.</span><span class="sxs-lookup"><span data-stu-id="940b5-127">Create an empty folder called iot-java-get-started.</span></span> <span data-ttu-id="940b5-128">Nella cartella iot-java-get-started creare un progetto Maven denominato **create-device-identity** usando il comando seguente al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="940b5-128">In the iot-java-get-started folder, create a Maven project called **create-device-identity** using the following command at your command prompt.</span></span> <span data-ttu-id="940b5-129">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="940b5-129">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="940b5-130">Al prompt dei comandi passare alla cartella create-device-identity.</span><span class="sxs-lookup"><span data-stu-id="940b5-130">At your command prompt, navigate to the create-device-identity folder.</span></span>

3. <span data-ttu-id="940b5-131">In un editor di testo aprire il file pom.xml nella cartella create-device-identity e aggiungere la dipendenza seguente al nodo **dependencies** .</span><span class="sxs-lookup"><span data-stu-id="940b5-131">Using a text editor, open the pom.xml file in the create-device-identity folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="940b5-132">Questa dipendenza consente di usare il pacchetto iot-service-client nell'app:</span><span class="sxs-lookup"><span data-stu-id="940b5-132">This dependency enables you to use the iot-service-client package in your app:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="940b5-133">È possibile cercare la versione più recente di **iot-service-client** usando la [ricerca di Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="940b5-133">You can check for the latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="940b5-134">Salvare e chiudere il file pom.xml.</span><span class="sxs-lookup"><span data-stu-id="940b5-134">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="940b5-135">Usando un editor di testo, aprire il file create-device-identity\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="940b5-135">Using a text editor, open the create-device-identity\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="940b5-136">Aggiungere al file le istruzioni **import** seguenti:</span><span class="sxs-lookup"><span data-stu-id="940b5-136">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="940b5-137">Aggiungere le variabili a livello di classe seguenti alla classe **App**, sostituendo **{yourhubconnectionstring}** con i valori annotati prima:</span><span class="sxs-lookup"><span data-stu-id="940b5-137">Add the following class-level variables to the **App** class, replacing **{yourhubconnectionstring}** with the value your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. <span data-ttu-id="940b5-138">Modificare la firma del metodo **main** includendo le eccezioni come segue:</span><span class="sxs-lookup"><span data-stu-id="940b5-138">Modify the signature of the **main** method to include the exceptions as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. <span data-ttu-id="940b5-139">Aggiungere il codice seguente come corpo del metodo **main** .</span><span class="sxs-lookup"><span data-stu-id="940b5-139">Add the following code as the body of the **main** method.</span></span> <span data-ttu-id="940b5-140">Questo codice crea un dispositivo denominato *javadevice* nel registro delle identità dell'hub IoT, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="940b5-140">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span></span> <span data-ttu-id="940b5-141">Quindi visualizza l'ID e la chiave del dispositivo che serviranno più avanti:</span><span class="sxs-lookup"><span data-stu-id="940b5-141">It then displays the device ID and key that you need later:</span></span>

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If the device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If the device already exists.
      try {
        device = registryManager.getDevice(deviceId);
      } catch (IotHubException iotf) {
        iotf.printStackTrace();
      }
    }

    // Display information about the
    // device you created.
    System.out.println("Device Id: " + device.getDeviceId());
    System.out.println("Device key: " + device.getPrimaryKey());
    ```

10. <span data-ttu-id="940b5-142">Salvare e chiudere il file App.java.</span><span class="sxs-lookup"><span data-stu-id="940b5-142">Save and close the App.java file.</span></span>

11. <span data-ttu-id="940b5-143">Per compilare l'app **create-device-identity** con Maven, eseguire il comando seguente al prompt dei comandi nella cartella create-device-identity:</span><span class="sxs-lookup"><span data-stu-id="940b5-143">To build the **create-device-identity** app using Maven, execute the following command at the command prompt in the create-device-identity folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. <span data-ttu-id="940b5-144">Per eseguire l'app **create-device-identity** con Maven, eseguire il comando seguente al prompt dei comandi nella cartella create-device-identity:</span><span class="sxs-lookup"><span data-stu-id="940b5-144">To run the **create-device-identity** app using Maven, execute the following command at the command prompt in the create-device-identity folder:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. <span data-ttu-id="940b5-145">Prendere nota dei valori di **Device ID** e **Device key**,</span><span class="sxs-lookup"><span data-stu-id="940b5-145">Make a note of the **Device ID** and **Device key**.</span></span> <span data-ttu-id="940b5-146">che saranno necessari più avanti quando si crea un'app che si connette all'hub IoT come dispositivo.</span><span class="sxs-lookup"><span data-stu-id="940b5-146">You need these values later when you create an app that connects to IoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="940b5-147">Il registro di identità dell'hub IoT archivia solo le identità del dispositivo per abilitare l'accesso sicuro all'hub.</span><span class="sxs-lookup"><span data-stu-id="940b5-147">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="940b5-148">Archivia le chiavi e gli ID dispositivo da usare come credenziali di sicurezza e un flag di abilitazione/disabilitazione che consente di disabilitare l'accesso per un singolo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="940b5-148">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="940b5-149">Se l'app deve archiviare altri metadati specifici del dispositivo, dovrà usare un'archiviazione specifica per app.</span><span class="sxs-lookup"><span data-stu-id="940b5-149">If your app needs to store other device-specific metadata, it should use an app-specific store.</span></span> <span data-ttu-id="940b5-150">Per altre informazioni, vedere la [Guida per gli sviluppatori dell'hub IoT][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="940b5-150">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="940b5-151">Ricezione di messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="940b5-151">Receive device-to-cloud messages</span></span>

<span data-ttu-id="940b5-152">In questa sezione si crea un'app console di Java che legge i messaggi da dispositivo a cloud dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="940b5-152">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="940b5-153">Un hub IoT espone un endpoint compatibile con l'[hub eventi][lnk-event-hubs-overview] per abilitare la lettura dei messaggi dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="940b5-153">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="940b5-154">Per semplicità, questa esercitazione crea un lettore di base non adatto per una distribuzione con velocità effettiva elevata.</span><span class="sxs-lookup"><span data-stu-id="940b5-154">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="940b5-155">L'esercitazione [Elaborare messaggi dispositivo a cloud][lnk-process-d2c-tutorial] illustra come elaborare i messaggi dispositivo a cloud su vasta scala.</span><span class="sxs-lookup"><span data-stu-id="940b5-155">The [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how to process device-to-cloud messages at scale.</span></span> <span data-ttu-id="940b5-156">L'esercitazione [Introduzione all'hub eventi][lnk-eventhubs-tutorial] offre altre informazioni su come elaborare i messaggi da hub eventi ed è applicabile agli endpoint compatibili con l'hub eventi dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="940b5-156">The [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how to process messages from Event Hubs and is applicable to the IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="940b5-157">L'endpoint compatibile con Hub eventi per la lettura di messaggi da dispositivo a cloud usa sempre il protocollo AMQP.</span><span class="sxs-lookup"><span data-stu-id="940b5-157">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>

1. <span data-ttu-id="940b5-158">Nella cartella iot-java-get-started creata nella sezione *Creare un'identità del dispositivo* creare un progetto Maven denominato **read-d2c-messages** usando il comando seguente al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="940b5-158">In the iot-java-get-started folder you created in the *Create a device identity* section, create a Maven project called **read-d2c-messages** using the following command at your command prompt.</span></span> <span data-ttu-id="940b5-159">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="940b5-159">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="940b5-160">Al prompt dei comandi passare alla cartella read-d2c-messages.</span><span class="sxs-lookup"><span data-stu-id="940b5-160">At your command prompt, navigate to the read-d2c-messages folder.</span></span>

3. <span data-ttu-id="940b5-161">In un editor di testo aprire il file pom.xml nella cartella read-d2c-messages e aggiungere la dipendenza seguente al nodo **dependencies** .</span><span class="sxs-lookup"><span data-stu-id="940b5-161">Using a text editor, open the pom.xml file in the read-d2c-messages folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="940b5-162">Questa dipendenza consente di usare il pacchetto eventhubs-client nell'app per la lettura dall'endpoint compatibile con l'hub eventi:</span><span class="sxs-lookup"><span data-stu-id="940b5-162">This dependency enables you to use the eventhubs-client package in your app to read from the Event Hub-compatible endpoint:</span></span>

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. <span data-ttu-id="940b5-163">Salvare e chiudere il file pom.xml.</span><span class="sxs-lookup"><span data-stu-id="940b5-163">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="940b5-164">Usando un editor di testo, aprire il file read-d2c-messages\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="940b5-164">Using a text editor, open the read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="940b5-165">Aggiungere al file le istruzioni **import** seguenti:</span><span class="sxs-lookup"><span data-stu-id="940b5-165">Add the following **import** statements to the file:</span></span>

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. <span data-ttu-id="940b5-166">Aggiungere la variabili a livello di classe seguente alla classe **App** .</span><span class="sxs-lookup"><span data-stu-id="940b5-166">Add the following class-level variable to the **App** class.</span></span> <span data-ttu-id="940b5-167">Sostituire **{youriothubkey}**, **{youreventhubcompatibleendpoint}** e **{youreventhubcompatiblename}** con i valori annotati in precedenza:</span><span class="sxs-lookup"><span data-stu-id="940b5-167">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with the values you noted previously:</span></span>

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. <span data-ttu-id="940b5-168">Aggiungere il metodo **receiveMessages** seguente alla **classe App**.</span><span class="sxs-lookup"><span data-stu-id="940b5-168">Add the following **receiveMessages** method to the **App** class.</span></span> <span data-ttu-id="940b5-169">Questo metodo crea un'istanza **EventHubClient** per connettersi all'endpoint compatibile con Hub eventi e quindi crea in modo asincrono un'istanza **PartitionReceiver** per la lettura da una partizione di Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="940b5-169">This method creates an **EventHubClient** instance to connect to the Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance to read from an Event Hub partition.</span></span> <span data-ttu-id="940b5-170">Esegue il ciclo ininterrottamente e stampa i dettagli del messaggio finché l'applicazione non termina.</span><span class="sxs-lookup"><span data-stu-id="940b5-170">It loops continuously and prints the message details until the app terminates.</span></span>

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed to create client: " + e.getMessage());
        System.exit(1);
      }
      try {
        // Create a receiver using the
        // default Event Hubs consumer group
        // that listens for messages from now on.
        client.createReceiver(EventHubClient.DEFAULT_CONSUMER_GROUP_NAME, partitionId, Instant.now())
          .thenAccept(new Consumer<PartitionReceiver>() {
            public void accept(PartitionReceiver receiver) {
              System.out.println("** Created receiver on partition " + partitionId);
              try {
                while (true) {
                  Iterable<EventData> receivedEvents = receiver.receive(100).get();
                  int batchSize = 0;
                  if (receivedEvents != null) {
                    System.out.println("Got some evenst");
                    for (EventData receivedEvent : receivedEvents) {
                      System.out.println(String.format("Offset: %s, SeqNo: %s, EnqueueTime: %s",
                        receivedEvent.getSystemProperties().getOffset(),
                        receivedEvent.getSystemProperties().getSequenceNumber(),
                        receivedEvent.getSystemProperties().getEnqueuedTime()));
                      System.out.println(String.format("| Device ID: %s",
                        receivedEvent.getSystemProperties().get("iothub-connection-device-id")));
                      System.out.println(String.format("| Message Payload: %s",
                        new String(receivedEvent.getBytes(), Charset.defaultCharset())));
                      batchSize++;
                    }
                  }
                  System.out.println(String.format("Partition: %s, ReceivedBatch Size: %s", partitionId, batchSize));
                }
              } catch (Exception e) {
                System.out.println("Failed to receive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed to create receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="940b5-171">Questo metodo usa un filtro quando crea il ricevitore e quindi il ricevitore legge solo i messaggi inviati all'hub IoT dopo che l'esecuzione del ricevitore è iniziata.</span><span class="sxs-lookup"><span data-stu-id="940b5-171">This method uses a filter when it creates the receiver so that the receiver only reads messages sent to IoT Hub after the receiver starts running.</span></span> <span data-ttu-id="940b5-172">Questa tecnica è utile in un ambiente di test perché consente di visualizzare il set di messaggi corrente.</span><span class="sxs-lookup"><span data-stu-id="940b5-172">This technique is useful in a test environment so you can see the current set of messages.</span></span> <span data-ttu-id="940b5-173">In un ambiente di produzione, il codice deve verificare di avere elaborato tutti i messaggi. Per altre informazioni, vedere l'esercitazione [Elaborare messaggi dispositivo a cloud dell'hub IoT][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="940b5-173">In a production environment, your code should make sure that it processes all the messages - for more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

9. <span data-ttu-id="940b5-174">Modificare la firma del metodo **main** includendo l'eccezione come segue:</span><span class="sxs-lookup"><span data-stu-id="940b5-174">Modify the signature of the **main** method to include the exception as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. <span data-ttu-id="940b5-175">Aggiungere il codice seguente al metodo **main** nella classe **App**.</span><span class="sxs-lookup"><span data-stu-id="940b5-175">Add the following code to the **main** method in the **App** class.</span></span> <span data-ttu-id="940b5-176">Questo codice crea le due istanze **EventHubClient** e **PartitionReceiver** e consente di chiudere l'app al termine dell'elaborazione dei messaggi:</span><span class="sxs-lookup"><span data-stu-id="940b5-176">This code creates the two **EventHubClient** and **PartitionReceiver** instances and enables you to close the app when you have finished processing messages:</span></span>

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER to exit.");
    System.in.read();
    try {
      client0.closeSync();
      client1.closeSync();
      System.exit(0);
    } catch (ServiceBusException sbe) {
      System.exit(1);
    }
    ```

    > [!NOTE]
    > <span data-ttu-id="940b5-177">Questo codice presuppone che l'hub IoT sia stato creato nel livello F1 gratuito.</span><span class="sxs-lookup"><span data-stu-id="940b5-177">This code assumes you created your IoT hub in the F1 (free) tier.</span></span> <span data-ttu-id="940b5-178">Un hub IoT gratuito ha due partizioni denominate "0" e "1".</span><span class="sxs-lookup"><span data-stu-id="940b5-178">A free IoT hub has two partitions named "0" and "1".</span></span>

11. <span data-ttu-id="940b5-179">Salvare e chiudere il file App.java.</span><span class="sxs-lookup"><span data-stu-id="940b5-179">Save and close the App.java file.</span></span>

12. <span data-ttu-id="940b5-180">Per compilare l'app **read-d2c-messages** con Maven, eseguire questo comando al prompt dei comandi nella cartella read-d2c-messages:</span><span class="sxs-lookup"><span data-stu-id="940b5-180">To build the **read-d2c-messages** app using Maven, execute the following command at the command prompt in the read-d2c-messages folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="940b5-181">Creare un'app per dispositivi</span><span class="sxs-lookup"><span data-stu-id="940b5-181">Create a device app</span></span>
<span data-ttu-id="940b5-182">In questa sezione si crea un'app console di Java che simula un dispositivo che invia messaggi da dispositivo a cloud a un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="940b5-182">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="940b5-183">Nella cartella iot-java-get-started creata nella sezione *Creare un'identità del dispositivo* creare un progetto Maven denominato **simulated-device** usando il comando seguente al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="940b5-183">In the iot-java-get-started folder you created in the *Create a device identity* section, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="940b5-184">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="940b5-184">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="940b5-185">Al prompt dei comandi passare alla cartella simulated-device.</span><span class="sxs-lookup"><span data-stu-id="940b5-185">At your command prompt, navigate to the simulated-device folder.</span></span>

3. <span data-ttu-id="940b5-186">In un editor di testo aprire il file pom.xml nella cartella simulated-device e aggiungere le dipendenze seguenti al nodo **dependencies** .</span><span class="sxs-lookup"><span data-stu-id="940b5-186">Using a text editor, open the pom.xml file in the simulated-device folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="940b5-187">Queste dipendenze consentono di usare il pacchetto iothub-java-client nell'app per comunicare con l'hub IoT e per serializzare gli oggetti Java in JSON:</span><span class="sxs-lookup"><span data-stu-id="940b5-187">This dependency enables you to use the iothub-java-client package in your app to communicate with your IoT hub and to serialize Java objects to JSON:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
      <version>2.3.1</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="940b5-188">È possibile cercare la versione più recente di **iot-device-client** usando la [ricerca di Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="940b5-188">You can check for the latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

4. <span data-ttu-id="940b5-189">Salvare e chiudere il file pom.xml.</span><span class="sxs-lookup"><span data-stu-id="940b5-189">Save and close the pom.xml file.</span></span>

5. <span data-ttu-id="940b5-190">Usando un editor di testo, aprire il file simulated-device\src\main\java\com\mycompany\app\App.java.</span><span class="sxs-lookup"><span data-stu-id="940b5-190">Using a text editor, open the simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="940b5-191">Aggiungere al file le istruzioni **import** seguenti:</span><span class="sxs-lookup"><span data-stu-id="940b5-191">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. <span data-ttu-id="940b5-192">Aggiungere le variabili a livello di classe seguenti alla classe **App** .</span><span class="sxs-lookup"><span data-stu-id="940b5-192">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="940b5-193">Sostituzione di **{youriothubname}** con il nome dell'hub IoT e di **{yourdevicekey}** con il valore della chiave del dispositivo generato nella sezione *Creare un'identità del dispositivo*:</span><span class="sxs-lookup"><span data-stu-id="940b5-193">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    <span data-ttu-id="940b5-194">Questa app di esempio usa la variabile **protocol** quando crea un'istanza di un oggetto **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="940b5-194">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="940b5-195">È possibile usare il protocollo MQTT, AMQP o HTTP per comunicare con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="940b5-195">You can use either the MQTT, AMQP, or HTTP protocol to communicate with IoT Hub.</span></span>

8. <span data-ttu-id="940b5-196">Aggiungere la classe **TelemetryDataPoint** annidata seguente nella classe **App** per specificare i dati di telemetria inviati dal dispositivo all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="940b5-196">Add the following nested **TelemetryDataPoint** class inside the **App** class to specify the telemetry data your device sends to your IoT hub:</span></span>

    ```java
    private static class TelemetryDataPoint {
      public String deviceId;
      public double temperature;
      public double humidity;
   
      public String serialize() {
        Gson gson = new Gson();
        return gson.toJson(this);
      }
    }
    ```
9. <span data-ttu-id="940b5-197">Aggiungere la classe **EventCallback** annidata seguente nella classe **App** per visualizzare lo stato di acknowledgement restituito dall'hub IoT quando elabora un messaggio proveniente dall'app per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="940b5-197">Add the following nested **EventCallback** class inside the **App** class to display the acknowledgement status that the IoT hub returns when it processes a message from the device app.</span></span> <span data-ttu-id="940b5-198">Questo metodo invia anche una notifica al thread principale dell'app quando il messaggio è stato elaborato:</span><span class="sxs-lookup"><span data-stu-id="940b5-198">This method also notifies the main thread in the app when the message has been processed:</span></span>
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to message with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. <span data-ttu-id="940b5-199">Aggiungere la classe **MessageSender** annidata seguente nella classe **App**.</span><span class="sxs-lookup"><span data-stu-id="940b5-199">Add the following nested **MessageSender** class inside the **App** class.</span></span> <span data-ttu-id="940b5-200">Il metodo **run** in questa classe genera dati di telemetria di esempio da inviare all'hub IoT e attende un acknowledgement prima di inviare il messaggio successivo:</span><span class="sxs-lookup"><span data-stu-id="940b5-200">The **run** method in this class generates sample telemetry data to send to your IoT hub and waits for an acknowledgement before sending the next message:</span></span>

    ```java
    private static class MessageSender implements Runnable {
      public void run()  {
        try {
          double minTemperature = 20;
          double minHumidity = 60;
          Random rand = new Random();
    
          while (true) {
            double currentTemperature = minTemperature + rand.nextDouble() * 15;
            double currentHumidity = minHumidity + rand.nextDouble() * 20;
            TelemetryDataPoint telemetryDataPoint = new TelemetryDataPoint();
            telemetryDataPoint.deviceId = deviceId;
            telemetryDataPoint.temperature = currentTemperature;
            telemetryDataPoint.humidity = currentHumidity;
    
            String msgStr = telemetryDataPoint.serialize();
            Message msg = new Message(msgStr);
            msg.setProperty("temperatureAlert", (currentTemperature > 30) ? "true" : "false");
            msg.setMessageId(java.util.UUID.randomUUID().toString()); 
            System.out.println("Sending: " + msgStr);
    
            Object lockobj = new Object();
            EventCallback callback = new EventCallback();
            client.sendEventAsync(msg, callback, lockobj);
    
            synchronized (lockobj) {
              lockobj.wait();
            }
            Thread.sleep(1000);
          }
        } catch (InterruptedException e) {
          System.out.println("Finished.");
        }
      }
    }
    ```

    <span data-ttu-id="940b5-201">Questo metodo invia un nuovo messaggio da dispositivo a cloud un secondo dopo che l'hub IoT ha riconosciuto il messaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="940b5-201">This method sends a new device-to-cloud message one second after the IoT hub acknowledges the previous message.</span></span> <span data-ttu-id="940b5-202">Il messaggio contiene un oggetto serializzato JSON con l'ID dispositivo e numeri generati casualmente per simulare un sensore temperatura e un sensore umidità.</span><span class="sxs-lookup"><span data-stu-id="940b5-202">The message contains a JSON-serialized object with the deviceId and randomly generated numbers to simulate a temperature sensor, and a humidity sensor.</span></span>

11. <span data-ttu-id="940b5-203">Sostituire il metodo **main** con il codice seguente che crea un thread per inviare messaggi da dispositivo a cloud all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="940b5-203">Replace the **main** method with the following code that creates a thread to send device-to-cloud messages to your IoT hub:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER to exit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. <span data-ttu-id="940b5-204">Salvare e chiudere il file App.java.</span><span class="sxs-lookup"><span data-stu-id="940b5-204">Save and close the App.java file.</span></span>

13. <span data-ttu-id="940b5-205">Per compilare l'app **simulated-device** con Maven, eseguire questo comando al prompt dei comandi nella cartella simulated-device:</span><span class="sxs-lookup"><span data-stu-id="940b5-205">To build the **simulated-device** app using Maven, execute the following command at the command prompt in the simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> <span data-ttu-id="940b5-206">Per semplicità, in questa esercitazione non si implementa alcun criterio di ripetizione dei tentativi.</span><span class="sxs-lookup"><span data-stu-id="940b5-206">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="940b5-207">Nel codice di produzione è consigliabile implementare criteri per i tentativi, ad esempio un backoff esponenziale, come illustrato nell'articolo di MSDN [Transient Fault Handling][lnk-transient-faults] (Gestione degli errori temporanei).</span><span class="sxs-lookup"><span data-stu-id="940b5-207">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="940b5-208">Eseguire le app</span><span class="sxs-lookup"><span data-stu-id="940b5-208">Run the apps</span></span>

<span data-ttu-id="940b5-209">A questo punto è possibile eseguire le app.</span><span class="sxs-lookup"><span data-stu-id="940b5-209">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="940b5-210">Al prompt dei comandi nella cartella read-d2c eseguire questo comando per iniziare a monitorare la prima partizione dell'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="940b5-210">At a command prompt in the read-d2c folder, run the following command to begin monitoring the first partition in your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![App del servizio hub IoT per Java per monitorare i messaggi dispositivo a cloud][7]

2. <span data-ttu-id="940b5-212">Al prompt dei comandi nella cartella simulated-device eseguire il comando seguente per iniziare a inviare i dati di telemetria all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="940b5-212">At a command prompt in the simulated-device folder, run the following command to begin sending telemetry data to your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![App del dispositivo hub IoT per Java per inviare i messaggi da dispositivo a cloud][8]

3. <span data-ttu-id="940b5-214">Il riquadro **Utilizzo** nel [portale di Azure][lnk-portal] mostra il numero di messaggi inviati all'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="940b5-214">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>

    ![Riquadro Utilizzo del portale di Azure con il numero dei messaggi inviati all'hub IoT][43]

## <a name="next-steps"></a><span data-ttu-id="940b5-216">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="940b5-216">Next steps</span></span>
<span data-ttu-id="940b5-217">In questa esercitazione è stato configurato un nuovo hub IoT nel Portale di Azure ed è stata quindi creata un'identità del dispositivo nel registro di identità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="940b5-217">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="940b5-218">Questa identità del dispositivo è stata usata per consentire all'app per dispositivi di inviare messaggi da dispositivo a cloud all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="940b5-218">You used this device identity to enable the device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="940b5-219">È stata anche creata un'app che visualizza i messaggi ricevuti dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="940b5-219">You also created an app that displays the messages received by the IoT hub.</span></span>

<span data-ttu-id="940b5-220">Per altre informazioni sulle attività iniziali con l'hub IoT e per esplorare altri scenari IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="940b5-220">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="940b5-221">[Connessione del dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="940b5-221">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="940b5-222">[Introduzione alla gestione dei dispositivi][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="940b5-222">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="940b5-223">[Introduzione ad Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="940b5-223">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="940b5-224">Per informazioni sull'estensione della soluzione IoT e l'elaborazione di messaggi dispositivo a cloud su vasta scala, vedere l'esercitazione [Elaborare messaggi dispositivo a cloud][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="940b5-224">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[6]: ./media/iot-hub-java-java-getstarted/create-iot-hub6.png
[7]: ./media/iot-hub-java-java-getstarted/runapp1.png
[8]: ./media/iot-hub-java-java-getstarted/runapp2.png
[43]: ./media/iot-hub-java-java-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-maven-service-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-device-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22
[lnk-maven-eventhubs-search]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22
