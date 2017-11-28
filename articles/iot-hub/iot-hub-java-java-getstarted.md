---
title: aaaGet avviato con l'IoT Hub Azure (linguaggio) | Documenti Microsoft
description: Informazioni su come toosend dispositivo a cloud messaggi tooAzure IoT Hub tramite IoT SDK per Java. Creare dispositivo simulato e servizio App tooregister il dispositivo, inviare messaggi e leggere messaggi da hub IoT.
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
ms.openlocfilehash: ac954f0522b46ed2a5b4a819bc611c13be0b9a9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-java"></a><span data-ttu-id="b1111-104">Connessione hub IoT tooyour dispositivo utilizzando Java</span><span class="sxs-lookup"><span data-stu-id="b1111-104">Connect your device tooyour IoT hub using Java</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="b1111-105">Alla fine di hello di questa esercitazione, si dispongono di tre applicazioni di console Java:</span><span class="sxs-lookup"><span data-stu-id="b1111-105">At hello end of this tutorial, you have three Java console apps:</span></span>

* <span data-ttu-id="b1111-106">**identità dispositivo creare**, che consente di creare un'identità del dispositivo e protezione della chiave tooconnect l'app del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b1111-106">**create-device-identity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="b1111-107">**i messaggi di d2c lettura**, che consente di visualizzare dati di telemetria hello inviati per l'app del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b1111-107">**read-d2c-messages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="b1111-108">**dispositivo simulato**, che collega l'hub IoT tooyour con l'identità del dispositivo hello creato in precedenza e invia un messaggio di dati di telemetria ogni secondo utilizzando hello protocollo MQTT.</span><span class="sxs-lookup"><span data-stu-id="b1111-108">**simulated-device**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="b1111-109">articolo Hello [Azure IoT SDK] [ lnk-hub-sdks] vengono fornite informazioni hello Azure IoT SDK che è possibile utilizzare toobuild toorun entrambe le app nei dispositivi e la soluzione di back-end.</span><span class="sxs-lookup"><span data-stu-id="b1111-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both apps toorun on devices and your solution back end.</span></span>

<span data-ttu-id="b1111-110">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b1111-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="b1111-111">versione più recente Hello [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="b1111-111">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span> 
* [<span data-ttu-id="b1111-112">Maven 3</span><span class="sxs-lookup"><span data-stu-id="b1111-112">Maven 3</span></span>](https://maven.apache.org/install.html) 
* <span data-ttu-id="b1111-113">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="b1111-113">An active Azure account.</span></span> <span data-ttu-id="b1111-114">Se non si ha un account, è possibile creare un [account gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="b1111-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="b1111-115">Come passaggio finale, prendere nota di hello **chiave primaria** valore.</span><span class="sxs-lookup"><span data-stu-id="b1111-115">As a final step, make a note of hello **Primary key** value.</span></span> <span data-ttu-id="b1111-116">Quindi fare clic su **endpoint** hello e **eventi** endpoint predefinito.</span><span class="sxs-lookup"><span data-stu-id="b1111-116">Then click **Endpoints** and hello **Events** built-in endpoint.</span></span> <span data-ttu-id="b1111-117">In hello **proprietà** pannello, prendere nota dei hello **nome compatibile con Hub eventi** hello e **endpoint compatibile con Hub eventi** indirizzo.</span><span class="sxs-lookup"><span data-stu-id="b1111-117">On hello **Properties** blade, make a note of hello **Event Hub-compatible name** and hello **Event Hub-compatible endpoint** address.</span></span> <span data-ttu-id="b1111-118">Questi tre valori sono necessari quando si crea l'app **read-d2c-messages**.</span><span class="sxs-lookup"><span data-stu-id="b1111-118">You need these three values when you create your **read-d2c-messages** app.</span></span>

![Pannello Messaggistica dell'hub IoT nel portale di Azure][6]

<span data-ttu-id="b1111-120">L'hub IoT è stato creato.</span><span class="sxs-lookup"><span data-stu-id="b1111-120">You have now created your IoT hub.</span></span> <span data-ttu-id="b1111-121">È necessario hello nome host dell'IoT Hub, la stringa di connessione IoT Hub, chiave primaria di IoT Hub, nome compatibile con Hub eventi ed endpoint compatibile con Hub eventi è necessario toocomplete in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b1111-121">You have hello IoT Hub host name, IoT Hub connection string, IoT Hub Primary Key, Event Hub-compatible name, and Event Hub-compatible endpoint you need toocomplete this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="b1111-122">Creare un'identità del dispositivo</span><span class="sxs-lookup"><span data-stu-id="b1111-122">Create a device identity</span></span>
<span data-ttu-id="b1111-123">In questa sezione si crea un'applicazione console Java che crea un'identità del dispositivo nel Registro di sistema di hello identità nell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b1111-123">In this section, you create a Java console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="b1111-124">Un dispositivo non può connettersi tooIoT hub, a meno che non sia presente una voce nel Registro di sistema di hello identità.</span><span class="sxs-lookup"><span data-stu-id="b1111-124">A device cannot connect tooIoT hub unless it has an entry in hello identity registry.</span></span> <span data-ttu-id="b1111-125">Per ulteriori informazioni, vedere hello **Registro di sistema di identità** sezione di hello [Guida per sviluppatori di IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="b1111-125">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="b1111-126">Quando si esegue questa app console, viene generato un ID univoco del dispositivo e chiave che il dispositivo può usare tooidentify stesso quando vengono inviati al dispositivo a cloud messaggi tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b1111-126">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="b1111-127">Creare una cartella vuota denominata iot-java-get-started.</span><span class="sxs-lookup"><span data-stu-id="b1111-127">Create an empty folder called iot-java-get-started.</span></span> <span data-ttu-id="b1111-128">Nella cartella iot java-get avviato hello, creare un progetto di Maven denominato **identità dispositivo creare** utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="b1111-128">In hello iot-java-get-started folder, create a Maven project called **create-device-identity** using hello following command at your command prompt.</span></span> <span data-ttu-id="b1111-129">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="b1111-129">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=create-device-identity -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="b1111-130">Al prompt dei comandi, passare cartella identità dispositivo creare toohello.</span><span class="sxs-lookup"><span data-stu-id="b1111-130">At your command prompt, navigate toohello create-device-identity folder.</span></span>

3. <span data-ttu-id="b1111-131">Utilizzando un editor di testo, di aprire file pom.xml hello nella cartella identità dispositivo creare hello e aggiungere hello seguente dipendenza toohello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="b1111-131">Using a text editor, open hello pom.xml file in hello create-device-identity folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="b1111-132">Questa dipendenza consente si toouse hello client di servizi iot pacchetto dell'App:</span><span class="sxs-lookup"><span data-stu-id="b1111-132">This dependency enables you toouse hello iot-service-client package in your app:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="b1111-133">È possibile verificare la versione più recente di hello di **client di servizi iot** utilizzando [ricerca Maven][lnk-maven-service-search].</span><span class="sxs-lookup"><span data-stu-id="b1111-133">You can check for hello latest version of **iot-service-client** using [Maven search][lnk-maven-service-search].</span></span>

4. <span data-ttu-id="b1111-134">Salvare e chiudere il file di pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-134">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="b1111-135">Per aprire il file di create-device-identity\src\main\java\com\mycompany\app\App.java hello, utilizzando un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="b1111-135">Using a text editor, open hello create-device-identity\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="b1111-136">Aggiungere il seguente hello **importare** file toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="b1111-136">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.service.exceptions.IotHubException;
    import com.microsoft.azure.sdk.iot.service.Device;
    import com.microsoft.azure.sdk.iot.service.RegistryManager;
   
    import java.io.IOException;
    import java.net.URISyntaxException;
    ```

7. <span data-ttu-id="b1111-137">Aggiungere hello seguenti variabili a livello di classe toohello **App** classe, sostituendo **{yourhubconnectionstring}** con hello valore l'indicato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="b1111-137">Add hello following class-level variables toohello **App** class, replacing **{yourhubconnectionstring}** with hello value your noted earlier:</span></span>

    ```java
    private static final String connectionString = "{yourhubconnectionstring}";
    private static final String deviceId = "myFirstJavaDevice";
    ```
[!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

8. <span data-ttu-id="b1111-138">Modificare la firma hello di hello **principale** tooinclude metodo hello eccezioni, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b1111-138">Modify hello signature of hello **main** method tooinclude hello exceptions as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException, Exception
    ```

9. <span data-ttu-id="b1111-139">Aggiungere hello seguente di codice come corpo hello di hello **principale** metodo.</span><span class="sxs-lookup"><span data-stu-id="b1111-139">Add hello following code as hello body of hello **main** method.</span></span> <span data-ttu-id="b1111-140">Questo codice crea un dispositivo denominato *javadevice* nel registro delle identità dell'hub IoT, se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="b1111-140">This code creates a device called *javadevice* in your IoT Hub identity registry if doesn't already exist.</span></span> <span data-ttu-id="b1111-141">Viene quindi visualizzato hello dispositivo ID e la chiave che è necessario in un secondo momento:</span><span class="sxs-lookup"><span data-stu-id="b1111-141">It then displays hello device ID and key that you need later:</span></span>

    ```java
    RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);
RegistryManager registryManager = RegistryManager.createFromConnectionString(connectionString);

    // Create a device that's enabled by default, 
    // with an autogenerated key.
    Device device = Device.createFromId(deviceId, null, null);
    try {
      device = registryManager.addDevice(device);
    } catch (IotHubException iote) {
      // If hello device already exists.
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
      // If hello device already exists.
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

10. <span data-ttu-id="b1111-142">Salvare e chiudere il file di App.java hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-142">Save and close hello App.java file.</span></span>

11. <span data-ttu-id="b1111-143">hello toobuild **identità dispositivo creare** app usando Maven, eseguire hello comando al prompt dei comandi di hello nella cartella identità dispositivo creare hello seguente:</span><span class="sxs-lookup"><span data-stu-id="b1111-143">toobuild hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

12. <span data-ttu-id="b1111-144">hello toorun **identità dispositivo creare** app usando Maven, eseguire hello comando al prompt dei comandi di hello nella cartella identità dispositivo creare hello seguente:</span><span class="sxs-lookup"><span data-stu-id="b1111-144">toorun hello **create-device-identity** app using Maven, execute hello following command at hello command prompt in hello create-device-identity folder:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

13. <span data-ttu-id="b1111-145">Prendere nota di hello **ID dispositivo** e **chiave dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="b1111-145">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="b1111-146">Questi valori è necessario in un secondo momento quando si crea un'app che si connette tooIoT Hub come un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b1111-146">You need these values later when you create an app that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="b1111-147">Hello del Registro di sistema di IoT Hub identità archivia solo hub IoT toohello di dispositivo identità tooenable proteggere l'accesso.</span><span class="sxs-lookup"><span data-stu-id="b1111-147">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="b1111-148">Archivia toouse di chiavi e l'ID dispositivo come credenziali di sicurezza e un flag di abilitazione/disabilitazione che è possibile utilizzare toodisable accesso per un singolo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b1111-148">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="b1111-149">Se l'app deve toostore altri metadati specifici del dispositivo, deve utilizzare un negozio specifico dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b1111-149">If your app needs toostore other device-specific metadata, it should use an app-specific store.</span></span> <span data-ttu-id="b1111-150">Per ulteriori informazioni, vedere hello [Guida per sviluppatori di IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="b1111-150">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>

## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="b1111-151">Ricezione di messaggi da dispositivo a cloud</span><span class="sxs-lookup"><span data-stu-id="b1111-151">Receive device-to-cloud messages</span></span>

<span data-ttu-id="b1111-152">In questa sezione si crea un'app console di Java che legge i messaggi da dispositivo a cloud dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b1111-152">In this section, you create a Java console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="b1111-153">Un hub IoT espone un [Hub eventi][lnk-event-hubs-overview]-tooenable endpoint compatibile per i messaggi da dispositivo a cloud tooread.</span><span class="sxs-lookup"><span data-stu-id="b1111-153">An IoT hub exposes an [Event Hub][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="b1111-154">cose tookeep semplice, in questa esercitazione consente di creare un lettore di base che non è adatto per una distribuzione di velocità effettiva elevata.</span><span class="sxs-lookup"><span data-stu-id="b1111-154">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="b1111-155">Hello [elaborare i messaggi da dispositivo a cloud] [ lnk-process-d2c-tutorial] esercitazione viene illustrato come tooprocess dispositivo a cloud messaggi su larga scala.</span><span class="sxs-lookup"><span data-stu-id="b1111-155">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="b1111-156">Hello [Introduzione agli hub di eventi] [ lnk-eventhubs-tutorial] esercitazione fornisce ulteriori informazioni su come tooprocess messaggi dagli hub eventi ed è applicabile toohello gli endpoint Hub IoT Hub eventi compatibile.</span><span class="sxs-lookup"><span data-stu-id="b1111-156">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="b1111-157">Hello Hub eventi compatibile con l'endpoint per la lettura dei messaggi da dispositivo a cloud sempre Usa protocollo AMQP hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-157">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="b1111-158">Nella cartella iot java-get avviato hello è stato creato in hello *creare un'identità del dispositivo* sezione, creare un progetto di Maven denominato **d2c-i-messaggi** utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="b1111-158">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **read-d2c-messages** using hello following command at your command prompt.</span></span> <span data-ttu-id="b1111-159">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="b1111-159">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=read-d2c-messages -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="b1111-160">Al prompt dei comandi, passare toohello cartella di lettura-d2c-messaggi.</span><span class="sxs-lookup"><span data-stu-id="b1111-160">At your command prompt, navigate toohello read-d2c-messages folder.</span></span>

3. <span data-ttu-id="b1111-161">Utilizzando un editor di testo, di aprire file pom.xml hello nella cartella di lettura-d2c-messaggi hello e aggiungere hello seguente dipendenza toohello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="b1111-161">Using a text editor, open hello pom.xml file in hello read-d2c-messages folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="b1111-162">Questa dipendenza consente di pacchetto di eventhubs client toouse hello in tooread l'app dall'endpoint compatibile con Hub eventi hello:</span><span class="sxs-lookup"><span data-stu-id="b1111-162">This dependency enables you toouse hello eventhubs-client package in your app tooread from hello Event Hub-compatible endpoint:</span></span>

    ```xml
    <dependency> 
        <groupId>com.microsoft.azure</groupId> 
        <artifactId>azure-eventhubs</artifactId> 
        <version>0.13.0</version> 
    </dependency>
    ```

4. <span data-ttu-id="b1111-163">Salvare e chiudere il file di pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-163">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="b1111-164">Per aprire il file di read-d2c-messages\src\main\java\com\mycompany\app\App.java hello, utilizzando un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="b1111-164">Using a text editor, open hello read-d2c-messages\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="b1111-165">Aggiungere il seguente hello **importare** file toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="b1111-165">Add hello following **import** statements toohello file:</span></span>

    ```java
    import java.io.IOException;
    import com.microsoft.azure.eventhubs.*;
    import com.microsoft.azure.servicebus.*;

    import java.nio.charset.Charset;
    import java.time.*;
    import java.util.function.*;
    ```

7. <span data-ttu-id="b1111-166">Aggiungere hello seguenti a livello di classe variabile toohello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="b1111-166">Add hello following class-level variable toohello **App** class.</span></span> <span data-ttu-id="b1111-167">Sostituire **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, e **{youreventhubcompatiblename}** con i valori hello è indicato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="b1111-167">Replace **{youriothubkey}**, **{youreventhubcompatibleendpoint}**, and **{youreventhubcompatiblename}** with hello values you noted previously:</span></span>

    ```java
    private static String connStr = "Endpoint={youreventhubcompatibleendpoint};EntityPath={youreventhubcompatiblename};SharedAccessKeyName=iothubowner;SharedAccessKey={youriothubkey}";
    ```

8. <span data-ttu-id="b1111-168">Aggiungere il seguente hello **receiveMessages** metodo toohello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="b1111-168">Add hello following **receiveMessages** method toohello **App** class.</span></span> <span data-ttu-id="b1111-169">Questo metodo crea un **EventHubClient** tooconnect toohello compatibile con Hub eventi endpoint dell'istanza e quindi crea in modo asincrono un **PartitionReceiver** tooread istanza da un Hub eventi partizione.</span><span class="sxs-lookup"><span data-stu-id="b1111-169">This method creates an **EventHubClient** instance tooconnect toohello Event Hub-compatible endpoint and then asynchronously creates a **PartitionReceiver** instance tooread from an Event Hub partition.</span></span> <span data-ttu-id="b1111-170">Eseguito un ciclo in modo continuo e stampa dettagli messaggio hello finché non termina l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-170">It loops continuously and prints hello message details until hello app terminates.</span></span>

    ```java
    // Create a receiver on a partition.
    private static EventHubClient receiveMessages(final String partitionId) {
      EventHubClient client = null;
      try {
        client = EventHubClient.createFromConnectionStringSync(connStr);
      } catch (Exception e) {
        System.out.println("Failed toocreate client: " + e.getMessage());
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
                System.out.println("Failed tooreceive messages: " + e.getMessage());
              }
            }
          });
        } catch (Exception e) {
          System.out.println("Failed toocreate receiver: " + e.getMessage());
      }
      return client;
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="b1111-171">Questo metodo utilizza un filtro durante la creazione di ricevitore hello in modo che hello ricevitore legge solo i messaggi inviati tooIoT Hub dopo ricevitore hello viene avviata l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b1111-171">This method uses a filter when it creates hello receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="b1111-172">Questa tecnica è utile in un ambiente di test in modo da visualizzare il set corrente di hello dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="b1111-172">This technique is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="b1111-173">In un ambiente di produzione, il codice deve verificare che vengano elaborati tutti i messaggi hello - per ulteriori informazioni, vedere hello [come i messaggi da dispositivo a cloud IoT Hub tooprocess] [ lnk-process-d2c-tutorial] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b1111-173">In a production environment, your code should make sure that it processes all hello messages - for more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

9. <span data-ttu-id="b1111-174">Modificare la firma hello di hello **principale** tooinclude metodo hello eccezione, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="b1111-174">Modify hello signature of hello **main** method tooinclude hello exception as follows:</span></span>

    ```java
    public static void main( String[] args ) throws IOException
    ```

10. <span data-ttu-id="b1111-175">Aggiungere i seguenti toohello codice hello **principale** metodo hello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="b1111-175">Add hello following code toohello **main** method in hello **App** class.</span></span> <span data-ttu-id="b1111-176">Questo codice crea due hello **EventHubClient** e **PartitionReceiver** istanze e consente app hello tooclose è terminata l'elaborazione dei messaggi:</span><span class="sxs-lookup"><span data-stu-id="b1111-176">This code creates hello two **EventHubClient** and **PartitionReceiver** instances and enables you tooclose hello app when you have finished processing messages:</span></span>

    ```java
    // Create receivers for partitions 0 and 1.
    EventHubClient client0 = receiveMessages("0");
    EventHubClient client1 = receiveMessages("1");
    System.out.println("Press ENTER tooexit.");
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
    > <span data-ttu-id="b1111-177">Questo codice presuppone che l'hub IoT creato nel livello di hello F1 (gratuito).</span><span class="sxs-lookup"><span data-stu-id="b1111-177">This code assumes you created your IoT hub in hello F1 (free) tier.</span></span> <span data-ttu-id="b1111-178">Un hub IoT gratuito ha due partizioni denominate "0" e "1".</span><span class="sxs-lookup"><span data-stu-id="b1111-178">A free IoT hub has two partitions named "0" and "1".</span></span>

11. <span data-ttu-id="b1111-179">Salvare e chiudere il file di App.java hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-179">Save and close hello App.java file.</span></span>

12. <span data-ttu-id="b1111-180">hello toobuild **d2c-i-messaggi** app usando Maven, eseguire hello comando al prompt dei comandi di hello nella cartella di lettura-d2c-messaggi hello seguente:</span><span class="sxs-lookup"><span data-stu-id="b1111-180">toobuild hello **read-d2c-messages** app using Maven, execute hello following command at hello command prompt in hello read-d2c-messages folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="b1111-181">Creare un'app per dispositivi</span><span class="sxs-lookup"><span data-stu-id="b1111-181">Create a device app</span></span>
<span data-ttu-id="b1111-182">In questa sezione si crea un'applicazione console Java che simula un dispositivo che invia l'hub IoT tooan messaggi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="b1111-182">In this section, you create a Java console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="b1111-183">Nella cartella iot java-get avviato hello è stato creato in hello *creare un'identità del dispositivo* sezione, creare un progetto di Maven denominato **dispositivo simulato** utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="b1111-183">In hello iot-java-get-started folder you created in hello *Create a device identity* section, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="b1111-184">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="b1111-184">Note this is a single, long command:</span></span>

    ```cmd/sh
    mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

2. <span data-ttu-id="b1111-185">Al prompt dei comandi, passare cartella dispositivo simulato toohello.</span><span class="sxs-lookup"><span data-stu-id="b1111-185">At your command prompt, navigate toohello simulated-device folder.</span></span>

3. <span data-ttu-id="b1111-186">Utilizzando un editor di testo, di aprire file pom.xml hello nella cartella dispositivo simulato hello e aggiungere hello seguente dipendenze toohello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="b1111-186">Using a text editor, open hello pom.xml file in hello simulated-device folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="b1111-187">Questa dipendenza consente si toouse hello client con l'hub IOT-java pacchetto in toocommunicate l'app con l'hub IoT e tooserialize tooJSON oggetti Java:</span><span class="sxs-lookup"><span data-stu-id="b1111-187">This dependency enables you toouse hello iothub-java-client package in your app toocommunicate with your IoT hub and tooserialize Java objects tooJSON:</span></span>

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
    > <span data-ttu-id="b1111-188">È possibile verificare la versione più recente di hello di **client di dispositivi iot** utilizzando [ricerca Maven][lnk-maven-device-search].</span><span class="sxs-lookup"><span data-stu-id="b1111-188">You can check for hello latest version of **iot-device-client** using [Maven search][lnk-maven-device-search].</span></span>

4. <span data-ttu-id="b1111-189">Salvare e chiudere il file di pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-189">Save and close hello pom.xml file.</span></span>

5. <span data-ttu-id="b1111-190">Per aprire il file di simulated-device\src\main\java\com\mycompany\app\App.java hello, utilizzando un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="b1111-190">Using a text editor, open hello simulated-device\src\main\java\com\mycompany\app\App.java file.</span></span>

6. <span data-ttu-id="b1111-191">Aggiungere il seguente hello **importare** file toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="b1111-191">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.google.gson.Gson;

    import java.io.*;
    import java.net.URISyntaxException;
    import java.util.Random;
    import java.util.concurrent.Executors;
    import java.util.concurrent.ExecutorService;
    ```

7. <span data-ttu-id="b1111-192">Aggiungere hello seguenti variabili a livello di classe toohello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="b1111-192">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="b1111-193">Sostituzione di **{youriothubname}** con il nome di hub IoT, e **{yourdevicekey}** con il valore della chiave di hello dispositivo è stato generato in hello *creare un'identità del dispositivo* sezione:</span><span class="sxs-lookup"><span data-stu-id="b1111-193">Replacing **{youriothubname}** with your IoT hub name, and **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myFirstJavaDevice;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static String deviceId = "myFirstJavaDevice";
    private static DeviceClient client;
    ```
   
    <span data-ttu-id="b1111-194">Questa app di esempio utilizza hello **protocollo** variabile quando si crea un'istanza di un **DeviceClient** oggetto.</span><span class="sxs-lookup"><span data-stu-id="b1111-194">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="b1111-195">È possibile utilizzare entrambi toocommunicate protocollo hello MQTT, AMQP o HTTP con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b1111-195">You can use either hello MQTT, AMQP, or HTTP protocol toocommunicate with IoT Hub.</span></span>

8. <span data-ttu-id="b1111-196">Aggiungere il seguente hello annidato **TelemetryDataPoint** classe all'interno di hello **App** classe dati di telemetria hello toospecify il dispositivo invia tooyour IoT hub:</span><span class="sxs-lookup"><span data-stu-id="b1111-196">Add hello following nested **TelemetryDataPoint** class inside hello **App** class toospecify hello telemetry data your device sends tooyour IoT hub:</span></span>

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
9. <span data-ttu-id="b1111-197">Aggiungere il seguente hello annidato **EventCallback** classe all'interno di hello **App** classe toodisplay hello acknowledgement stato hello hub IoT restituisce quando elabora un messaggio hello app del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b1111-197">Add hello following nested **EventCallback** class inside hello **App** class toodisplay hello acknowledgement status that hello IoT hub returns when it processes a message from hello device app.</span></span> <span data-ttu-id="b1111-198">Questo metodo notifica thread principale di hello in app hello è stato elaborato il messaggio hello:</span><span class="sxs-lookup"><span data-stu-id="b1111-198">This method also notifies hello main thread in hello app when hello message has been processed:</span></span>
   
    ```java
    private static class EventCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toomessage with status: " + status.name());
   
        if (context != null) {
          synchronized (context) {
            context.notify();
          }
        }
      }
    }
    ```

10. <span data-ttu-id="b1111-199">Aggiungere il seguente hello annidato **MessageSender** classe all'interno di hello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="b1111-199">Add hello following nested **MessageSender** class inside hello **App** class.</span></span> <span data-ttu-id="b1111-200">Hello **eseguire** metodo in questa classe genera l'errore hub IoT di esempio telemetria dati toosend tooyour e attende un acknowledgement prima di inviare il messaggio successivo hello:</span><span class="sxs-lookup"><span data-stu-id="b1111-200">hello **run** method in this class generates sample telemetry data toosend tooyour IoT hub and waits for an acknowledgement before sending hello next message:</span></span>

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

    <span data-ttu-id="b1111-201">Questo metodo invia un nuovo messaggio di dispositivo a cloud a un secondo dopo l'hub IoT hello invia un acknowledgement messaggio hello del precedente.</span><span class="sxs-lookup"><span data-stu-id="b1111-201">This method sends a new device-to-cloud message one second after hello IoT hub acknowledges hello previous message.</span></span> <span data-ttu-id="b1111-202">messaggio Hello contiene un oggetto serializzato JSON con deviceId hello e generato in modo casuale di numeri toosimulate un sensore di temperatura e un sensore umidità.</span><span class="sxs-lookup"><span data-stu-id="b1111-202">hello message contains a JSON-serialized object with hello deviceId and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

11. <span data-ttu-id="b1111-203">Sostituire hello **principale** metodo con hello dopo il codice che crea un hub IoT tooyour di thread toosend messaggi da dispositivo a cloud:</span><span class="sxs-lookup"><span data-stu-id="b1111-203">Replace hello **main** method with hello following code that creates a thread toosend device-to-cloud messages tooyour IoT hub:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException {
      client = new DeviceClient(connString, protocol);
      client.open();
    
      MessageSender sender = new MessageSender();
    
      ExecutorService executor = Executors.newFixedThreadPool(1);
      executor.execute(sender);
    
      System.out.println("Press ENTER tooexit.");
      System.in.read();
      executor.shutdownNow();
      client.closeNow();
    }
    ```

12. <span data-ttu-id="b1111-204">Salvare e chiudere il file di App.java hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-204">Save and close hello App.java file.</span></span>

13. <span data-ttu-id="b1111-205">hello toobuild **dispositivo simulato** app usando Maven, eseguire hello comando al prompt dei comandi di hello nella cartella dispositivo simulato hello seguente:</span><span class="sxs-lookup"><span data-stu-id="b1111-205">toobuild hello **simulated-device** app using Maven, execute hello following command at hello command prompt in hello simulated-device folder:</span></span>

    ```cmd/sh
    mvn clean package -DskipTests
    ```

> [!NOTE]
> <span data-ttu-id="b1111-206">cose tookeep semplice, in questa esercitazione non implementa alcun criterio di tentativo.</span><span class="sxs-lookup"><span data-stu-id="b1111-206">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b1111-207">Nel codice di produzione, è necessario implementare criteri di ripetizione (ad esempio un backoff esponenziale), come indicato nell'articolo MSDN hello [gestione degli errori temporanei][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="b1111-207">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="b1111-208">Eseguire App hello</span><span class="sxs-lookup"><span data-stu-id="b1111-208">Run hello apps</span></span>

<span data-ttu-id="b1111-209">Si è ora pronto toorun hello app.</span><span class="sxs-lookup"><span data-stu-id="b1111-209">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="b1111-210">Al prompt dei comandi nella cartella di lettura d2c hello eseguire hello successivo comando toobegin monitoraggio prima partizione nell'hub IoT di hello:</span><span class="sxs-lookup"><span data-stu-id="b1111-210">At a command prompt in hello read-d2c folder, run hello following command toobegin monitoring hello first partition in your IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App"
    ```

    ![Messaggi da dispositivo a cloud toomonitor dell'IoT Hub Java servizio app][7]

2. <span data-ttu-id="b1111-212">Al prompt dei comandi nella cartella dispositivo simulato hello eseguire hello toobegin comando invio hub IoT tooyour dati di telemetria seguenti:</span><span class="sxs-lookup"><span data-stu-id="b1111-212">At a command prompt in hello simulated-device folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>

    ```cmd/sh
    mvn exec:java -Dexec.mainClass="com.mycompany.app.App" 
    ```

    ![Messaggi da dispositivo a cloud dell'IoT Hub Java dispositivo app toosend][8]

3. <span data-ttu-id="b1111-214">Hello **utilizzo** riquadro in hello [portale di Azure] [ lnk-portal] Mostra hello numero di messaggi inviati toohello hub IoT:</span><span class="sxs-lookup"><span data-stu-id="b1111-214">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Azure portale utilizzo riquadro mostra il numero di messaggi inviati tooIoT Hub][43]

## <a name="next-steps"></a><span data-ttu-id="b1111-216">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b1111-216">Next steps</span></span>
<span data-ttu-id="b1111-217">In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità.</span><span class="sxs-lookup"><span data-stu-id="b1111-217">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="b1111-218">È stato utilizzato questo dispositivo identità tooenable hello dispositivo app toosend messaggi da dispositivo a cloud toohello hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b1111-218">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="b1111-219">È stato creato anche un'applicazione che consente di visualizzare i messaggi hello ricevuti dall'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="b1111-219">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="b1111-220">Guida introduttiva toocontinue con IoT Hub e tooexplore altri scenari IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="b1111-220">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="b1111-221">[Connessione del dispositivo][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="b1111-221">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="b1111-222">[Introduzione alla gestione dei dispositivi][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="b1111-222">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="b1111-223">[Introduzione ad Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="b1111-223">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="b1111-224">toolearn tooextend vedere i messaggi di dispositivo a cloud processo e di soluzione IoT su larga scala, hello [elaborare i messaggi da dispositivo a cloud] [ lnk-process-d2c-tutorial] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b1111-224">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
