---
title: Pianificare processi con l'hub IoT di Azure (Java) | Microsoft Docs
description: "Come pianificare un processo dell'hub IoT di Azure per chiamare un metodo diretto e impostare una proprietà desiderata su più dispositivi. Usare Azure IoT SDK per dispositivi per Java per implementare le app per dispositivi simulate e Azure IoT SDK per servizi per Java per implementare un'app di servizio che esegue il processo."
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
ms.openlocfilehash: 003a548ef2da2921a699df1aa9f7aee366d341ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="schedule-and-broadcast-jobs-java"></a><span data-ttu-id="8f9e0-104">Pianificare e trasmettere processi (Java)</span><span class="sxs-lookup"><span data-stu-id="8f9e0-104">Schedule and broadcast jobs (Java)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="8f9e0-105">Usare l'hub IoT per pianificare e tenere traccia dei processi che aggiornano milioni di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-105">Use Azure IoT Hub to schedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="8f9e0-106">Usare i processi per:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-106">Use jobs to:</span></span>

* <span data-ttu-id="8f9e0-107">Aggiornare le proprietà desiderate</span><span class="sxs-lookup"><span data-stu-id="8f9e0-107">Update desired properties</span></span>
* <span data-ttu-id="8f9e0-108">Aggiornare i tag</span><span class="sxs-lookup"><span data-stu-id="8f9e0-108">Update tags</span></span>
* <span data-ttu-id="8f9e0-109">Richiamare metodi diretti</span><span class="sxs-lookup"><span data-stu-id="8f9e0-109">Invoke direct methods</span></span>

<span data-ttu-id="8f9e0-110">Un processo esegue il wrapping di una di queste azioni e tiene traccia dell'esecuzione rispetto a un set di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-110">A job wraps one of these actions and tracks the execution against a set of devices.</span></span> <span data-ttu-id="8f9e0-111">Una query di dispositivi gemelli definisce il set di dispositivi su cui il processo viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-111">A device twin query defines the set of devices the job executes against.</span></span> <span data-ttu-id="8f9e0-112">Ad esempio, un'applicazione back-end può usare un processo per chiamare un metodo diretto su 10.000 dispositivi che riavvia i dispositivi stessi.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-112">For example, a back-end app can use a job to invoke a direct method on 10,000 devices that reboots the devices.</span></span> <span data-ttu-id="8f9e0-113">È necessario specificare il set di dispositivi con una query di dispositivi gemelli e pianificare il processo in modo che venga eseguito in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-113">You specify the set of devices with a device twin query and schedule the job to run at a future time.</span></span> <span data-ttu-id="8f9e0-114">L'applicazione può quindi tenere traccia dell'avanzamento mentre ognuno dei dispositivi riceve ed esegue il metodo diretto di riavvio.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-114">The job tracks progress as each of the devices receive and execute the reboot direct method.</span></span>

<span data-ttu-id="8f9e0-115">Per altre informazioni su queste funzionalità, vedere:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-115">To learn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="8f9e0-116">Dispositivo gemello e proprietà: [Introduzione ai dispositivi gemelli](iot-hub-java-java-twin-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="8f9e0-116">Device twin and properties: [Get started with device twins](iot-hub-java-java-twin-getstarted.md)</span></span>
* <span data-ttu-id="8f9e0-117">Metodi diretti: [Guida per sviluppatori dell'hub IoT - Metodi diretti](iot-hub-devguide-direct-methods.md) ed [Esercitazione: Usare metodi diretti](iot-hub-java-java-direct-methods.md)</span><span class="sxs-lookup"><span data-stu-id="8f9e0-117">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](iot-hub-java-java-direct-methods.md)</span></span>

<span data-ttu-id="8f9e0-118">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-118">This tutorial shows you how to:</span></span>

* <span data-ttu-id="8f9e0-119">Creare un'app per dispositivi che implementa un metodo diretto denominato **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-119">Create a device app that implements a direct method called **lockDoor**.</span></span> <span data-ttu-id="8f9e0-120">L'app per dispositivi riceve anche le modifiche di proprietà desiderate dall'app back-end.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-120">The device app also receives desired property changes from the back-end app.</span></span>
* <span data-ttu-id="8f9e0-121">Creare un'app back-end che crea un processo per chiamare il metodo diretto **lockDoor** su più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-121">Create a back-end app that creates a job to call the **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="8f9e0-122">Un altro processo invia gli aggiornamenti di proprietà desiderati a più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-122">Another job sends desired property updates to multiple devices.</span></span>

<span data-ttu-id="8f9e0-123">Al termine dell'esercitazione saranno disponibili un'app per il dispositivo console Java e un'app back-end console Java:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-123">At the end of this tutorial, you have a java console device app and a java console back-end app:</span></span>

<span data-ttu-id="8f9e0-124">**simulated-device** che si connette all'hub IoT, implementa il metodo diretto **lockDoor** e gestisce le modifiche di proprietà desiderate.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-124">**simulated-device** that connects to your IoT hub, implements the **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="8f9e0-125">**schedule-jobs** che usa processi per chiamare il metodo diretto **lockDoor** e aggiornare le proprietà di dispositivi gemelli desiderate su più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-125">**schedule-jobs** that use jobs to call the **lockDoor** direct method and update the device twin desired properties on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="8f9e0-126">L'articolo [Azure IoT SDK](iot-hub-devguide-sdks.md) riporta informazioni sui componenti Azure IoT SDK che consentono di compilare le app back-end e per dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-126">The article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f9e0-127">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8f9e0-127">Prerequisites</span></span>

<span data-ttu-id="8f9e0-128">Per completare questa esercitazione, sono necessari:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-128">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="8f9e0-129">[Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) più recente</span><span class="sxs-lookup"><span data-stu-id="8f9e0-129">The latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="8f9e0-130">Maven 3</span><span class="sxs-lookup"><span data-stu-id="8f9e0-130">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="8f9e0-131">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-131">An active Azure account.</span></span> <span data-ttu-id="8f9e0-132">Se non si dispone di un account, è possibile crearne uno [gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-132">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="8f9e0-133">Se si preferisce creare l'identità del dispositivo a livello di programmazione, leggere la sezione corrispondente nell'articolo [Connettere il dispositivo all'hub IoT usando Java](iot-hub-java-java-getstarted.md#create-a-device-identity).</span><span class="sxs-lookup"><span data-stu-id="8f9e0-133">If you prefer to create the device identity programmatically, read the corresponding section in the [Connect your device to your IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span> <span data-ttu-id="8f9e0-134">È possibile anche usare lo strumento [iothub-explorer](https://github.com/Azure/iothub-explorer) per aggiungere un dispositivo all'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-134">You can also use the [iothub-explorer](https://github.com/Azure/iothub-explorer) tool to add a device to your IoT hub.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="8f9e0-135">Creare l'app di servizio</span><span class="sxs-lookup"><span data-stu-id="8f9e0-135">Create the service app</span></span>

<span data-ttu-id="8f9e0-136">In questa sezione si crea un'app console Java che usa i processi per:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-136">In this section, you create a Java console app that uses jobs to:</span></span>

* <span data-ttu-id="8f9e0-137">Chiamare il metodo diretto **lockDoor** su più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-137">Call the **lockDoor** direct method on multiple devices.</span></span>
* <span data-ttu-id="8f9e0-138">Inviare le proprietà desiderate a più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-138">Send desired properties to multiple devices.</span></span>

<span data-ttu-id="8f9e0-139">Per creare l'app:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-139">To create the app:</span></span>

1. <span data-ttu-id="8f9e0-140">Nel computer di sviluppo creare una cartella vuota denominata `iot-java-schedule-jobs`.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-140">On your development machine, create an empty folder called `iot-java-schedule-jobs`.</span></span>

1. <span data-ttu-id="8f9e0-141">Nella cartella `iot-java-schedule-jobs` creare un progetto Maven denominato **schedule-jobs** eseguendo il comando seguente al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-141">In the `iot-java-schedule-jobs` folder, create a Maven project called **schedule-jobs** using the following command at your command prompt.</span></span> <span data-ttu-id="8f9e0-142">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-142">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="8f9e0-143">Al prompt dei comandi passare alla cartella `schedule-jobs`.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-143">At your command prompt, navigate to the `schedule-jobs` folder.</span></span>

1. <span data-ttu-id="8f9e0-144">In un editor di testo aprire il file `pom.xml` nella cartella `schedule-jobs` e aggiungere la dipendenza seguente al nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-144">Using a text editor, open the `pom.xml` file in the `schedule-jobs` folder and add the following dependency to the **dependencies** node.</span></span> <span data-ttu-id="8f9e0-145">Questa dipendenza consente di usare il pacchetto **iot-service-client** nell'app per comunicare con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-145">This dependency enables you to use the **iot-service-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="8f9e0-146">È possibile cercare la versione più recente di **iot-service-client** usando la [ricerca di Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="8f9e0-146">You can check for the latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="8f9e0-147">Aggiungere il nodo **build** seguente dopo il nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-147">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="8f9e0-148">Questa configurazione indica a Maven di usare Java 1.8 per compilare l'app:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-148">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="8f9e0-149">Salvare e chiudere il file `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-149">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="8f9e0-150">Aprire il file `schedule-jobs\src\main\java\com\mycompany\app\App.java` in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-150">Using a text editor, open the `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="8f9e0-151">Aggiungere al file le istruzioni **import** seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-151">Add the following **import** statements to the file:</span></span>

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

1. <span data-ttu-id="8f9e0-152">Aggiungere le variabili a livello di classe seguenti alla classe **App** .</span><span class="sxs-lookup"><span data-stu-id="8f9e0-152">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="8f9e0-153">Sostituire `{youriothubconnectionstring}` con la stringa di connessione dell'hub IoT indicata nella sezione *Creare un hub IoT*:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-153">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in the *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long the job is permitted to run without
    // completing its work on the set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. <span data-ttu-id="8f9e0-154">Aggiungere il metodo seguente alla classe **App** per pianificare un processo con cui aggiornare le proprietà desiderate di **Building** e **Floor** nel dispositivo gemello:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-154">Add the following method to the **App** class to schedule a job to update the **Building** and **Floor** desired properties in the device twin:</span></span>

    ```java
    private static JobResult scheduleJobSetDesiredProperties(JobClient jobClient, String jobId) {
      DeviceTwinDevice twin = new DeviceTwinDevice(deviceId);
      Set<Pair> desiredProperties = new HashSet<Pair>();
      desiredProperties.add(new Pair("Building", 43));
      desiredProperties.add(new Pair("Floor", 3));
      twin.setDesiredProperties(desiredProperties);
      // Optimistic concurrency control
      twin.setETag("*");

      // Schedule the update twin job to run now
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

1. <span data-ttu-id="8f9e0-155">Per pianificare un processo che chiama il metodo **lockDoor**, aggiungere il metodo seguente alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-155">To schedule a job to call the **lockDoor** method, add the following method to the **App** class:</span></span>

    ```java
    private static JobResult scheduleJobCallDirectMethod(JobClient jobClient, String jobId) {
      // Schedule a job now to call the lockDoor direct method
      // against a single device. Response and connection
      // timeouts are set to 5 seconds.
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

1. <span data-ttu-id="8f9e0-156">Per monitorare un processo, aggiungere il metodo seguente alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-156">To monitor a job, add the following method to the **App** class:</span></span>

    ```java
    private static void monitorJob(JobClient jobClient, String jobId) {
      try {
        JobResult jobResult = jobClient.getJob(jobId);
        if(jobResult == null)
        {
          System.out.println("No JobResult for: " + jobId);
          return;
        }
        // Check the job result until it's completed
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

1. <span data-ttu-id="8f9e0-157">Per eseguire una query sui dettagli dei processi eseguiti, aggiungere il metodo seguente:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-157">To query for the details of the jobs you ran, add the following method:</span></span>

    ```java
    private static void queryDeviceJobs(JobClient jobClient, String start) throws Exception {
      System.out.println("\nQuery device jobs since " + start);

      // Create a jobs query using the time the jobs started
      Query deviceJobQuery = jobClient
          .queryDeviceJob(SqlQuery.createSqlQuery("*", SqlQuery.FromType.JOBS, "devices.jobs.startTimeUtc > '" + start + "'", null).getQuery());

      // Iterate over the list of jobs and print the details
      while (jobClient.hasNextJob(deviceJobQuery)) {
        System.out.println(jobClient.getNextJob(deviceJobQuery));
      }
    }
    ```

1. <span data-ttu-id="8f9e0-158">Aggiornare la firma del metodo **main** affinché includa la clausola `throws`:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-158">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. <span data-ttu-id="8f9e0-159">Per eseguire e monitorare due processi in sequenza, aggiungere il codice seguente al metodo **main**:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-159">To run and monitor two jobs sequentially, add the following code to the **main** method:</span></span>

    ```java
    // Record the start time
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

    // Run a query to show the job detail
    queryDeviceJobs(jobClient, start);

    System.out.println("Shutting down schedule-jobs app");
    ```

1. <span data-ttu-id="8f9e0-160">Salvare e chiudere il file `schedule-jobs\src\main\java\com\mycompany\app\App.java`</span><span class="sxs-lookup"><span data-stu-id="8f9e0-160">Save and close the `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="8f9e0-161">Compilare l'app **schedule-jobs** e correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-161">Build the **schedule-jobs** app and correct any errors.</span></span> <span data-ttu-id="8f9e0-162">Al prompt dei comandi passare alla cartella `schedule-jobs` ed eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-162">At your command prompt, navigate to the `schedule-jobs` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="8f9e0-163">Creare un'app per dispositivi</span><span class="sxs-lookup"><span data-stu-id="8f9e0-163">Create a device app</span></span>

<span data-ttu-id="8f9e0-164">In questa sezione si crea un'app console Java che gestisce le proprietà desiderate inviate dall'hub IoT e implementa la chiamata di metodo diretto.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-164">In this section, you create a Java console app that handles the desired properties sent from IoT Hub and implements the direct method call.</span></span>

1. <span data-ttu-id="8f9e0-165">Nella cartella `iot-java-schedule-jobs` creare un progetto Maven denominato **simulated-device** usando il comando seguente al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-165">In the `iot-java-schedule-jobs` folder, create a Maven project called **simulated-device** using the following command at your command prompt.</span></span> <span data-ttu-id="8f9e0-166">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-166">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="8f9e0-167">Al prompt dei comandi passare alla cartella `simulated-device`.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-167">At your command prompt, navigate to the `simulated-device` folder.</span></span>

1. <span data-ttu-id="8f9e0-168">In un editor di testo aprire il file `pom.xml` nella cartella `simulated-device` e aggiungere le dipendenze seguenti al nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-168">Using a text editor, open the `pom.xml` file in the `simulated-device` folder and add the following dependencies to the **dependencies** node.</span></span> <span data-ttu-id="8f9e0-169">Questa dipendenza consente di usare il pacchetto **iot-device-client** nell'app per comunicare con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-169">This dependency enables you to use the **iot-device-client** package in your app to communicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="8f9e0-170">È possibile cercare la versione più recente di **iot-device-client** usando la [ricerca di Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="8f9e0-170">You can check for the latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="8f9e0-171">Aggiungere il nodo **build** seguente dopo il nodo **dependencies**.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-171">Add the following **build** node after the **dependencies** node.</span></span> <span data-ttu-id="8f9e0-172">Questa configurazione indica a Maven di usare Java 1.8 per compilare l'app:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-172">This configuration instructs Maven to use Java 1.8 to build the app:</span></span>

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

1. <span data-ttu-id="8f9e0-173">Salvare e chiudere il file `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-173">Save and close the `pom.xml` file.</span></span>

1. <span data-ttu-id="8f9e0-174">Aprire il file `simulated-device\src\main\java\com\mycompany\app\App.java` in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-174">Using a text editor, open the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="8f9e0-175">Aggiungere al file le istruzioni **import** seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-175">Add the following **import** statements to the file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="8f9e0-176">Aggiungere le variabili a livello di classe seguenti alla classe **App** .</span><span class="sxs-lookup"><span data-stu-id="8f9e0-176">Add the following class-level variables to the **App** class.</span></span> <span data-ttu-id="8f9e0-177">Sostituzione di `{youriothubname}` con il nome dell'hub IoT e di `{yourdevicekey}` con il valore della chiave del dispositivo generato nella sezione *Creare un'identità del dispositivo*:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-177">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with the device key value you generated in the *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="8f9e0-178">Questa app di esempio usa la variabile **protocol** quando crea un'istanza di un oggetto **DeviceClient**.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-178">This sample app uses the **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="8f9e0-179">Attualmente per usare le funzionalità del dispositivo gemello è necessario usare il protocollo MQTT.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-179">Currently, to use device twin features you must use the MQTT protocol.</span></span>

1. <span data-ttu-id="8f9e0-180">Per stampare le notifiche del dispositivo gemello nella console, aggiungere la classe annidata seguente alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-180">To print device twin notifications to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to device twin operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="8f9e0-181">Per stampare le notifiche del metodo diretto nella console, aggiungere la classe annidata seguente alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-181">To print direct method notifications to the console, add the following nested class to the **App** class:</span></span>

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded to direct method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="8f9e0-182">Per gestire chiamate di metodo diretto dall'hub IoT, aggiungere la classe annidata seguente alla classe **App**:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-182">To handle direct method calls from IoT Hub, add the following nested class to the **App** class:</span></span>

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

1. <span data-ttu-id="8f9e0-183">Aggiornare la firma del metodo **main** affinché includa la clausola `throws`:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-183">Update the **main** method signature to include the following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="8f9e0-184">Al metodo **main** aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-184">Add the following code to the **main** method to:</span></span>
    * <span data-ttu-id="8f9e0-185">Creare un client del dispositivo per comunicare con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-185">Create a device client to communicate with IoT Hub.</span></span>
    * <span data-ttu-id="8f9e0-186">Creare un oggetto **Device** per archiviare le proprietà dei dispositivi gemelli.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-186">Create a **Device** object to store the device twin properties.</span></span>

    ```java
    // Create a device client
    DeviceClient client = new DeviceClient(connString, protocol);

    // An object to manage device twin desired and reported properties
    Device dataCollector = new Device() {
      @Override
      public void PropertyCall(String propertyKey, Object propertyValue, Object context)
      {
        System.out.println("Received desired property change: " + propertyKey + " " + propertyValue);
      }
    };
    ```

1. <span data-ttu-id="8f9e0-187">Per avviare i servizi client del dispositivo, aggiungere il codice seguente al metodo **main**:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-187">To start the device client services, add the following code to the **main** method:</span></span>

    ```java
    try {
      // Open the DeviceClient
      // Start the device twin services
      // Subscribe to direct method calls
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

1. <span data-ttu-id="8f9e0-188">Per attendere che l'utente prema il tasto **INVIO** prima della chiusura, aggiungere il codice seguente alla fine del metodo **main**:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-188">To wait for the user to press the **Enter** key before shutting down, add the following code to the end of the **main** method:</span></span>

    ```java
    // Close the app
    System.out.println("Press any key to exit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. <span data-ttu-id="8f9e0-189">Salvare e chiudere il file `simulated-device\src\main\java\com\mycompany\app\App.java`.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-189">Save and close the `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="8f9e0-190">Compilare l'app **simulated-device** e correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-190">Build the **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="8f9e0-191">Al prompt dei comandi passare alla cartella `simulated-device` ed eseguire il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-191">At your command prompt, navigate to the `simulated-device` folder and run the following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-the-apps"></a><span data-ttu-id="8f9e0-192">Eseguire le app</span><span class="sxs-lookup"><span data-stu-id="8f9e0-192">Run the apps</span></span>

<span data-ttu-id="8f9e0-193">A questo punto è possibile eseguire le app console.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-193">You are now ready to run the console apps.</span></span>

1. <span data-ttu-id="8f9e0-194">Al prompt dei comandi nella cartella `simulated-device` eseguire il comando seguente per avviare l'app per dispositivi che ascolta le modifiche di proprietà desiderate e le chiamate di metodo diretto:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-194">At a command prompt in the `simulated-device` folder, run the following command to start the device app listening for desired property changes and direct method calls:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![Il client per dispositivi si avvia](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. <span data-ttu-id="8f9e0-196">Al prompt dei comandi nella cartella `schedule-jobs` eseguire il comando seguente per avviare l'app di servizio **schedule-jobs** in modo da eseguire due processi.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-196">At a command prompt in the `schedule-jobs` folder, run the following command to run the **schedule-jobs** service app to run two jobs.</span></span> <span data-ttu-id="8f9e0-197">Il primo imposta i valori di proprietà desiderati, il secondo chiama il metodo diretto:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-197">The first sets the desired property values, the second calls the direct method:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![L'app di servizio dell'hub IoT Java crea due processi](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. <span data-ttu-id="8f9e0-199">L'app per dispositivi gestisce la modifica di proprietà desiderata e la chiamata di metodo diretto:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-199">The device app handles the desired property change and the direct method call:</span></span>

    ![Il client per dispositivi risponde alle modifiche](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a><span data-ttu-id="8f9e0-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8f9e0-201">Next steps</span></span>

<span data-ttu-id="8f9e0-202">In questa esercitazione è stato configurato un nuovo hub IoT nel Portale di Azure ed è stata quindi creata un'identità del dispositivo nel registro di identità dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-202">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="8f9e0-203">È stata creata un'app back-end per l'esecuzione di due processi.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-203">You created a back-end app to run two jobs.</span></span> <span data-ttu-id="8f9e0-204">Il primo processo ha impostato i valori di proprietà desiderati e il secondo processo ha chiamato un metodo diretto.</span><span class="sxs-lookup"><span data-stu-id="8f9e0-204">The first job set desired property values, and the second job called a direct method.</span></span>

<span data-ttu-id="8f9e0-205">Per altre informazioni, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="8f9e0-205">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="8f9e0-206">Per inviare dati di telemetria dai dispositivi, vedere l'esercitazione [Introduzione all'hub IoT](iot-hub-java-java-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="8f9e0-206">Send telemetry from devices with the [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="8f9e0-207">Per controllare i dispositivi in modo interattivo, ad esempio per attivare un ventilatore da un'app controllata dall'utente, vedere l'esercitazione [Usare metodi diretti](iot-hub-java-java-direct-methods.md).</span><span class="sxs-lookup"><span data-stu-id="8f9e0-207">Control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>
