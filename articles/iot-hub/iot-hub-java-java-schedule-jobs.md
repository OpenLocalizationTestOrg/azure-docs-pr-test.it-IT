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
# <a name="schedule-and-broadcast-jobs-java"></a><span data-ttu-id="da32e-104">Pianificare e trasmettere processi (Java)</span><span class="sxs-lookup"><span data-stu-id="da32e-104">Schedule and broadcast jobs (Java)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="da32e-105">Utilizzare i processi tooschedule e tenere traccia IoT Hub di Azure che aggiornano milioni di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="da32e-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="da32e-106">Usare i processi per:</span><span class="sxs-lookup"><span data-stu-id="da32e-106">Use jobs to:</span></span>

* <span data-ttu-id="da32e-107">Aggiornare le proprietà desiderate</span><span class="sxs-lookup"><span data-stu-id="da32e-107">Update desired properties</span></span>
* <span data-ttu-id="da32e-108">Aggiornare i tag</span><span class="sxs-lookup"><span data-stu-id="da32e-108">Update tags</span></span>
* <span data-ttu-id="da32e-109">Richiamare metodi diretti</span><span class="sxs-lookup"><span data-stu-id="da32e-109">Invoke direct methods</span></span>

<span data-ttu-id="da32e-110">Un processo esegue il wrapping di una di queste azioni e le tracce hello esecuzione rispetto a un set di dispositivi.</span><span class="sxs-lookup"><span data-stu-id="da32e-110">A job wraps one of these actions and tracks hello execution against a set of devices.</span></span> <span data-ttu-id="da32e-111">Una query di un doppio dispositivo definisce il set di hello di hello processo viene eseguito su dispositivi.</span><span class="sxs-lookup"><span data-stu-id="da32e-111">A device twin query defines hello set of devices hello job executes against.</span></span> <span data-ttu-id="da32e-112">Ad esempio, un'applicazione back-end è possibile utilizzare un tooinvoke processo un metodo diretto su 10.000 dispositivi che si riavvia dispositivi hello.</span><span class="sxs-lookup"><span data-stu-id="da32e-112">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="da32e-113">È necessario specifica il set di hello di dispositivi con una query di due dispositivi e pianificare toorun processo hello in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="da32e-113">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="da32e-114">avanzamento tiene traccia del processo Hello come tutti i dispositivi di hello di ricezione ed eseguire hello riavvio dirette del metodo.</span><span class="sxs-lookup"><span data-stu-id="da32e-114">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="da32e-115">toolearn informazioni su ciascuna di queste funzionalità, vedere:</span><span class="sxs-lookup"><span data-stu-id="da32e-115">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="da32e-116">Dispositivo gemello e proprietà: [Introduzione ai dispositivi gemelli](iot-hub-java-java-twin-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="da32e-116">Device twin and properties: [Get started with device twins](iot-hub-java-java-twin-getstarted.md)</span></span>
* <span data-ttu-id="da32e-117">Metodi diretti: [Guida per sviluppatori dell'hub IoT - Metodi diretti](iot-hub-devguide-direct-methods.md) ed [Esercitazione: Usare metodi diretti](iot-hub-java-java-direct-methods.md)</span><span class="sxs-lookup"><span data-stu-id="da32e-117">Direct methods: [IoT Hub developer guide - direct methods](iot-hub-devguide-direct-methods.md) and [Tutorial: Use direct methods](iot-hub-java-java-direct-methods.md)</span></span>

<span data-ttu-id="da32e-118">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="da32e-118">This tutorial shows you how to:</span></span>

* <span data-ttu-id="da32e-119">Creare un'app per dispositivi che implementa un metodo diretto denominato **lockDoor**.</span><span class="sxs-lookup"><span data-stu-id="da32e-119">Create a device app that implements a direct method called **lockDoor**.</span></span> <span data-ttu-id="da32e-120">Hello dispositivo app riceve inoltre le modifiche alle proprietà desiderato dai hello back-end app.</span><span class="sxs-lookup"><span data-stu-id="da32e-120">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="da32e-121">Creare un'applicazione back-end che crea un hello toocall processo **lockDoor** metodo diretto su più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="da32e-121">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="da32e-122">Un altro processo invia proprietà desiderata Aggiorna dispositivi toomultiple.</span><span class="sxs-lookup"><span data-stu-id="da32e-122">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="da32e-123">Alla fine di hello di questa esercitazione, si dispone di un'applicazione console in java dispositivo e un'applicazione back-end di console java:</span><span class="sxs-lookup"><span data-stu-id="da32e-123">At hello end of this tutorial, you have a java console device app and a java console back-end app:</span></span>

<span data-ttu-id="da32e-124">**dispositivo simulato** che connette l'hub IoT tooyour, implementa hello **lockDoor** indirizzare lo si desidera metodo e gestisce le modifiche alle proprietà.</span><span class="sxs-lookup"><span data-stu-id="da32e-124">**simulated-device** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="da32e-125">**i processi di pianificazione** che usano hello toocall processi **lockDoor** diretto (metodo) e aggiornamento hello dispositivo doppi desiderato proprietà su più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="da32e-125">**schedule-jobs** that use jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="da32e-126">articolo Hello [Azure IoT SDK](iot-hub-devguide-sdks.md) fornisce informazioni su Azure IoT SDK hello che è possibile utilizzare toobuild applicazioni back-end sia sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="da32e-126">hello article [Azure IoT SDKs](iot-hub-devguide-sdks.md) provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="da32e-127">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="da32e-127">Prerequisites</span></span>

<span data-ttu-id="da32e-128">toocomplete questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="da32e-128">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="da32e-129">versione più recente Hello [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span><span class="sxs-lookup"><span data-stu-id="da32e-129">hello latest [Java SE Development Kit 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)</span></span>
* [<span data-ttu-id="da32e-130">Maven 3</span><span class="sxs-lookup"><span data-stu-id="da32e-130">Maven 3</span></span>](https://maven.apache.org/install.html)
* <span data-ttu-id="da32e-131">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="da32e-131">An active Azure account.</span></span> <span data-ttu-id="da32e-132">Se non si dispone di un account, è possibile crearne uno [gratuito](http://azure.microsoft.com/pricing/free-trial/) in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="da32e-132">(If you don't have an account, you can create a [free account](http://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="da32e-133">Se si preferisce l'identità del dispositivo hello toocreate a livello di codice, leggere una sezione corrispondente di hello in hello [connessione hub IoT tooyour dispositivo utilizzando Java](iot-hub-java-java-getstarted.md#create-a-device-identity) articolo.</span><span class="sxs-lookup"><span data-stu-id="da32e-133">If you prefer toocreate hello device identity programmatically, read hello corresponding section in hello [Connect your device tooyour IoT hub using Java](iot-hub-java-java-getstarted.md#create-a-device-identity) article.</span></span> <span data-ttu-id="da32e-134">È inoltre possibile utilizzare hello [l'hub IOT Esplora](https://github.com/Azure/iothub-explorer) strumento tooadd un hub IoT tooyour di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="da32e-134">You can also use hello [iothub-explorer](https://github.com/Azure/iothub-explorer) tool tooadd a device tooyour IoT hub.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="da32e-135">Creare l'applicazione di servizio hello</span><span class="sxs-lookup"><span data-stu-id="da32e-135">Create hello service app</span></span>

<span data-ttu-id="da32e-136">In questa sezione si crea un'app console Java che usa i processi per:</span><span class="sxs-lookup"><span data-stu-id="da32e-136">In this section, you create a Java console app that uses jobs to:</span></span>

* <span data-ttu-id="da32e-137">Chiamare hello **lockDoor** metodo diretto su più dispositivi.</span><span class="sxs-lookup"><span data-stu-id="da32e-137">Call hello **lockDoor** direct method on multiple devices.</span></span>
* <span data-ttu-id="da32e-138">Inviare i dispositivi toomultiple proprietà desiderate.</span><span class="sxs-lookup"><span data-stu-id="da32e-138">Send desired properties toomultiple devices.</span></span>

<span data-ttu-id="da32e-139">toocreate hello app:</span><span class="sxs-lookup"><span data-stu-id="da32e-139">toocreate hello app:</span></span>

1. <span data-ttu-id="da32e-140">Nel computer di sviluppo creare una cartella vuota denominata `iot-java-schedule-jobs`.</span><span class="sxs-lookup"><span data-stu-id="da32e-140">On your development machine, create an empty folder called `iot-java-schedule-jobs`.</span></span>

1. <span data-ttu-id="da32e-141">In hello `iot-java-schedule-jobs` cartella, creare un progetto di Maven denominato **pianificazione processi** utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="da32e-141">In hello `iot-java-schedule-jobs` folder, create a Maven project called **schedule-jobs** using hello following command at your command prompt.</span></span> <span data-ttu-id="da32e-142">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="da32e-142">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=schedule-jobs -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="da32e-143">Al prompt dei comandi, passare toohello `schedule-jobs` cartella.</span><span class="sxs-lookup"><span data-stu-id="da32e-143">At your command prompt, navigate toohello `schedule-jobs` folder.</span></span>

1. <span data-ttu-id="da32e-144">Utilizzando un editor di testo, aprire hello `pom.xml` file hello `schedule-jobs` cartella e aggiungere hello seguente dipendenza toohello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="da32e-144">Using a text editor, open hello `pom.xml` file in hello `schedule-jobs` folder and add hello following dependency toohello **dependencies** node.</span></span> <span data-ttu-id="da32e-145">Questa dipendenza consente hello toouse **client di servizi iot** pacchetto in toocommunicate l'app con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="da32e-145">This dependency enables you toouse hello **iot-service-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-service-client</artifactId>
      <version>1.7.23</version>
      <type>jar</type>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="da32e-146">È possibile verificare la versione più recente di hello di **client di servizi iot** utilizzando [ricerca Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="da32e-146">You can check for hello latest version of **iot-service-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-service-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="da32e-147">Aggiungere il seguente hello **compilare** nodo dopo hello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="da32e-147">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="da32e-148">Questa configurazione indica Maven toouse Java toobuild 1.8 hello app:</span><span class="sxs-lookup"><span data-stu-id="da32e-148">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="da32e-149">Salvare e chiudere hello `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="da32e-149">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="da32e-150">Utilizzando un editor di testo, aprire hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="da32e-150">Using a text editor, open hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="da32e-151">Aggiungere il seguente hello **importare** file toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="da32e-151">Add hello following **import** statements toohello file:</span></span>

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

1. <span data-ttu-id="da32e-152">Aggiungere hello seguenti variabili a livello di classe toohello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="da32e-152">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="da32e-153">Sostituire `{youriothubconnectionstring}` con la stringa di connessione hub IoT è stata annotata nella hello *creare un IoT Hub* sezione:</span><span class="sxs-lookup"><span data-stu-id="da32e-153">Replace `{youriothubconnectionstring}` with your IoT hub connection string you noted in hello *Create an IoT Hub* section:</span></span>

    ```java
    public static final String iotHubConnectionString = "{youriothubconnectionstring}";
    public static final String deviceId = "myDeviceId";

    // How long hello job is permitted toorun without
    // completing its work on hello set of devices
    private static final long maxExecutionTimeInSeconds = 30;
    ```

1. <span data-ttu-id="da32e-154">Aggiungere hello seguente metodo toohello **App** tooschedule classe un hello tooupdate processo **compilazione** e **Floor** le proprietà in un doppio dispositivo hello desiderate:</span><span class="sxs-lookup"><span data-stu-id="da32e-154">Add hello following method toohello **App** class tooschedule a job tooupdate hello **Building** and **Floor** desired properties in hello device twin:</span></span>

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

1. <span data-ttu-id="da32e-155">tooschedule un hello toocall processo **lockDoor** metodo, aggiungere hello seguente metodo toohello **App** classe:</span><span class="sxs-lookup"><span data-stu-id="da32e-155">tooschedule a job toocall hello **lockDoor** method, add hello following method toohello **App** class:</span></span>

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

1. <span data-ttu-id="da32e-156">toomonitor un processo, aggiungere hello seguente metodo toohello **App** classe:</span><span class="sxs-lookup"><span data-stu-id="da32e-156">toomonitor a job, add hello following method toohello **App** class:</span></span>

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

1. <span data-ttu-id="da32e-157">tooquery per i dettagli di hello dei processi di hello è stato eseguito, aggiungere al metodo hello:</span><span class="sxs-lookup"><span data-stu-id="da32e-157">tooquery for hello details of hello jobs you ran, add hello following method:</span></span>

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

1. <span data-ttu-id="da32e-158">Hello aggiornamento **principale** seguente hello tooinclude firma di metodo `throws` clausola:</span><span class="sxs-lookup"><span data-stu-id="da32e-158">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws Exception
    ```

1. <span data-ttu-id="da32e-159">toorun e monitoraggio di due processi in sequenza, aggiungere hello seguente codice toohello **principale** metodo:</span><span class="sxs-lookup"><span data-stu-id="da32e-159">toorun and monitor two jobs sequentially, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="da32e-160">Salvare e chiudere hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span><span class="sxs-lookup"><span data-stu-id="da32e-160">Save and close hello `schedule-jobs\src\main\java\com\mycompany\app\App.java` file</span></span>

1. <span data-ttu-id="da32e-161">Compilare hello **pianificazione processi** app e correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="da32e-161">Build hello **schedule-jobs** app and correct any errors.</span></span> <span data-ttu-id="da32e-162">Al prompt dei comandi, passare toohello `schedule-jobs` cartella e hello esecuzione comando seguente:</span><span class="sxs-lookup"><span data-stu-id="da32e-162">At your command prompt, navigate toohello `schedule-jobs` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="create-a-device-app"></a><span data-ttu-id="da32e-163">Creare un'app per dispositivi</span><span class="sxs-lookup"><span data-stu-id="da32e-163">Create a device app</span></span>

<span data-ttu-id="da32e-164">In questa sezione si crea un'applicazione console Java che gestisce le proprietà desiderate inviate da una chiamata al metodo diretto hello IoT Hub e implementa di hello.</span><span class="sxs-lookup"><span data-stu-id="da32e-164">In this section, you create a Java console app that handles hello desired properties sent from IoT Hub and implements hello direct method call.</span></span>

1. <span data-ttu-id="da32e-165">In hello `iot-java-schedule-jobs` cartella, creare un progetto di Maven denominato **dispositivo simulato** utilizzando hello seguente comando al prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="da32e-165">In hello `iot-java-schedule-jobs` folder, create a Maven project called **simulated-device** using hello following command at your command prompt.</span></span> <span data-ttu-id="da32e-166">Si noti che si tratta di un lungo comando singolo:</span><span class="sxs-lookup"><span data-stu-id="da32e-166">Note this is a single, long command:</span></span>

    `mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=simulated-device -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false`

1. <span data-ttu-id="da32e-167">Al prompt dei comandi, passare toohello `simulated-device` cartella.</span><span class="sxs-lookup"><span data-stu-id="da32e-167">At your command prompt, navigate toohello `simulated-device` folder.</span></span>

1. <span data-ttu-id="da32e-168">Utilizzando un editor di testo, aprire hello `pom.xml` file hello `simulated-device` cartella e aggiungere hello seguente dipendenze toohello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="da32e-168">Using a text editor, open hello `pom.xml` file in hello `simulated-device` folder and add hello following dependencies toohello **dependencies** node.</span></span> <span data-ttu-id="da32e-169">Questa dipendenza consente hello toouse **client di dispositivi iot** pacchetto in toocommunicate l'app con l'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="da32e-169">This dependency enables you toouse hello **iot-device-client** package in your app toocommunicate with your IoT hub:</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure.sdk.iot</groupId>
      <artifactId>iot-device-client</artifactId>
      <version>1.3.32</version>
    </dependency>
    ```

    > [!NOTE]
    > <span data-ttu-id="da32e-170">È possibile verificare la versione più recente di hello di **client di dispositivi iot** utilizzando [ricerca Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span><span class="sxs-lookup"><span data-stu-id="da32e-170">You can check for hello latest version of **iot-device-client** using [Maven search](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22iot-device-client%22%20g%3A%22com.microsoft.azure.sdk.iot%22).</span></span>

1. <span data-ttu-id="da32e-171">Aggiungere il seguente hello **compilare** nodo dopo hello **dipendenze** nodo.</span><span class="sxs-lookup"><span data-stu-id="da32e-171">Add hello following **build** node after hello **dependencies** node.</span></span> <span data-ttu-id="da32e-172">Questa configurazione indica Maven toouse Java toobuild 1.8 hello app:</span><span class="sxs-lookup"><span data-stu-id="da32e-172">This configuration instructs Maven toouse Java 1.8 toobuild hello app:</span></span>

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

1. <span data-ttu-id="da32e-173">Salvare e chiudere hello `pom.xml` file.</span><span class="sxs-lookup"><span data-stu-id="da32e-173">Save and close hello `pom.xml` file.</span></span>

1. <span data-ttu-id="da32e-174">Utilizzando un editor di testo, aprire hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="da32e-174">Using a text editor, open hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="da32e-175">Aggiungere il seguente hello **importare** file toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="da32e-175">Add hello following **import** statements toohello file:</span></span>

    ```java
    import com.microsoft.azure.sdk.iot.device.*;
    import com.microsoft.azure.sdk.iot.device.DeviceTwin.*;

    import java.io.IOException;
    import java.net.URISyntaxException;
    import java.util.Scanner;
    ```

1. <span data-ttu-id="da32e-176">Aggiungere hello seguenti variabili a livello di classe toohello **App** classe.</span><span class="sxs-lookup"><span data-stu-id="da32e-176">Add hello following class-level variables toohello **App** class.</span></span> <span data-ttu-id="da32e-177">Sostituzione di `{youriothubname}` con il nome di hub IoT, e `{yourdevicekey}` con il valore della chiave di hello dispositivo è stato generato in hello *creare un'identità del dispositivo* sezione:</span><span class="sxs-lookup"><span data-stu-id="da32e-177">Replacing `{youriothubname}` with your IoT hub name, and `{yourdevicekey}` with hello device key value you generated in hello *Create a device identity* section:</span></span>

    ```java
    private static String connString = "HostName={youriothubname}.azure-devices.net;DeviceId=myDeviceID;SharedAccessKey={yourdevicekey}";
    private static IotHubClientProtocol protocol = IotHubClientProtocol.MQTT;
    private static final int METHOD_SUCCESS = 200;
    private static final int METHOD_NOT_DEFINED = 404;
    ```

    <span data-ttu-id="da32e-178">Questa app di esempio utilizza hello **protocollo** variabile quando si crea un'istanza di un **DeviceClient** oggetto.</span><span class="sxs-lookup"><span data-stu-id="da32e-178">This sample app uses hello **protocol** variable when it instantiates a **DeviceClient** object.</span></span> <span data-ttu-id="da32e-179">Attualmente, toouse doppi le funzionalità del dispositivo è necessario utilizzare il protocollo MQTT hello.</span><span class="sxs-lookup"><span data-stu-id="da32e-179">Currently, toouse device twin features you must use hello MQTT protocol.</span></span>

1. <span data-ttu-id="da32e-180">tooprint dispositivo doppi notifiche toohello console, aggiungere il seguente hello annidati classe toohello **App** classe:</span><span class="sxs-lookup"><span data-stu-id="da32e-180">tooprint device twin notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for device twin operation notifications from IoT Hub
    protected static class DeviceTwinStatusCallBack implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodevice twin operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="da32e-181">tooprint diretta metodo notifiche toohello console, aggiungere il seguente hello annidati classe toohello **App** classe:</span><span class="sxs-lookup"><span data-stu-id="da32e-181">tooprint direct method notifications toohello console, add hello following nested class toohello **App** class:</span></span>

    ```java
    // Handler for direct method notifications from IoT Hub
    protected static class DirectMethodStatusCallback implements IotHubEventCallback {
      public void execute(IotHubStatusCode status, Object context) {
        System.out.println("IoT Hub responded toodirect method operation with status " + status.name());
      }
    }
    ```

1. <span data-ttu-id="da32e-182">chiamate dirette del metodo toohandle dall'IoT Hub, aggiungere il seguente hello annidati classe toohello **App** classe:</span><span class="sxs-lookup"><span data-stu-id="da32e-182">toohandle direct method calls from IoT Hub, add hello following nested class toohello **App** class:</span></span>

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

1. <span data-ttu-id="da32e-183">Hello aggiornamento **principale** seguente hello tooinclude firma di metodo `throws` clausola:</span><span class="sxs-lookup"><span data-stu-id="da32e-183">Update hello **main** method signature tooinclude hello following `throws` clause:</span></span>

    ```java
    public static void main( String[] args ) throws IOException, URISyntaxException
    ```

1. <span data-ttu-id="da32e-184">Aggiungere i seguenti toohello codice hello **principale** metodo:</span><span class="sxs-lookup"><span data-stu-id="da32e-184">Add hello following code toohello **main** method to:</span></span>
    * <span data-ttu-id="da32e-185">Creare un toocommunicate di client del dispositivo con l'IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="da32e-185">Create a device client toocommunicate with IoT Hub.</span></span>
    * <span data-ttu-id="da32e-186">Creare un **dispositivo** toostore hello dispositivo due proprietà dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="da32e-186">Create a **Device** object toostore hello device twin properties.</span></span>

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

1. <span data-ttu-id="da32e-187">toostart hello dispositivo client servizi, aggiungere il seguente codice toohello hello **principale** metodo:</span><span class="sxs-lookup"><span data-stu-id="da32e-187">toostart hello device client services, add hello following code toohello **main** method:</span></span>

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

1. <span data-ttu-id="da32e-188">toowait per hello di hello utente toopress **invio** chiave prima della chiusura, aggiungere hello successivo toohello codice alla fine di hello **principale** metodo:</span><span class="sxs-lookup"><span data-stu-id="da32e-188">toowait for hello user toopress hello **Enter** key before shutting down, add hello following code toohello end of hello **main** method:</span></span>

    ```java
    // Close hello app
    System.out.println("Press any key tooexit...");
    Scanner scanner = new Scanner(System.in);
    scanner.nextLine();
    dataCollector.clean();
    client.closeNow();
    scanner.close();
    ```

1. <span data-ttu-id="da32e-189">Salvare e chiudere hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span><span class="sxs-lookup"><span data-stu-id="da32e-189">Save and close hello `simulated-device\src\main\java\com\mycompany\app\App.java` file.</span></span>

1. <span data-ttu-id="da32e-190">Compilare hello **dispositivo simulato** app e correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="da32e-190">Build hello **simulated-device** app and correct any errors.</span></span> <span data-ttu-id="da32e-191">Al prompt dei comandi, passare toohello `simulated-device` cartella e hello esecuzione comando seguente:</span><span class="sxs-lookup"><span data-stu-id="da32e-191">At your command prompt, navigate toohello `simulated-device` folder and run hello following command:</span></span>

    `mvn clean package -DskipTests`

## <a name="run-hello-apps"></a><span data-ttu-id="da32e-192">Eseguire App hello</span><span class="sxs-lookup"><span data-stu-id="da32e-192">Run hello apps</span></span>

<span data-ttu-id="da32e-193">Si è ora pronto toorun hello console app.</span><span class="sxs-lookup"><span data-stu-id="da32e-193">You are now ready toorun hello console apps.</span></span>

1. <span data-ttu-id="da32e-194">Al prompt dei comandi in hello `simulated-device` cartella, eseguire hello comando toostart hello dispositivo app ascolto delle modifiche di proprietà e chiamate dirette del metodo seguente:</span><span class="sxs-lookup"><span data-stu-id="da32e-194">At a command prompt in hello `simulated-device` folder, run hello following command toostart hello device app listening for desired property changes and direct method calls:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![avvio Hello dispositivo client](media/iot-hub-java-java-schedule-jobs/device-app-1.png)

1. <span data-ttu-id="da32e-196">Al prompt dei comandi in hello `schedule-jobs` cartella, eseguire hello successivo comando toorun hello **pianificazione processi** due processi di app toorun del servizio.</span><span class="sxs-lookup"><span data-stu-id="da32e-196">At a command prompt in hello `schedule-jobs` folder, run hello following command toorun hello **schedule-jobs** service app toorun two jobs.</span></span> <span data-ttu-id="da32e-197">Hello imposta innanzitutto i valori delle proprietà hello desiderato, chiamate secondo hello hello dirette del metodo:</span><span class="sxs-lookup"><span data-stu-id="da32e-197">hello first sets hello desired property values, hello second calls hello direct method:</span></span>

    `mvn exec:java -Dexec.mainClass="com.mycompany.app.App"`

    ![L'app di servizio dell'hub IoT Java crea due processi](media/iot-hub-java-java-schedule-jobs/service-app-1.png)

1. <span data-ttu-id="da32e-199">app per dispositivi Hello gestisce hello desiderato modifica della proprietà e chiamate dirette del metodo hello:</span><span class="sxs-lookup"><span data-stu-id="da32e-199">hello device app handles hello desired property change and hello direct method call:</span></span>

    ![client del dispositivo Hello risponde toohello modifiche](media/iot-hub-java-java-schedule-jobs/device-app-2.png)

## <a name="next-steps"></a><span data-ttu-id="da32e-201">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="da32e-201">Next steps</span></span>

<span data-ttu-id="da32e-202">In questa esercitazione, è configurato un nuovo hub IoT in hello portale di Azure e quindi creata un'identità del dispositivo nel Registro di sistema dell'hub IoT hello identità.</span><span class="sxs-lookup"><span data-stu-id="da32e-202">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="da32e-203">È stato creato un'applicazione back-end toorun due processi.</span><span class="sxs-lookup"><span data-stu-id="da32e-203">You created a back-end app toorun two jobs.</span></span> <span data-ttu-id="da32e-204">primo processo Hello imposta valori di proprietà desiderati e secondo processo hello chiamato un metodo diretto.</span><span class="sxs-lookup"><span data-stu-id="da32e-204">hello first job set desired property values, and hello second job called a direct method.</span></span>

<span data-ttu-id="da32e-205">Hello utilizzare seguenti come risorse toolearn per:</span><span class="sxs-lookup"><span data-stu-id="da32e-205">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="da32e-206">Inviare i dati di telemetria dai dispositivi con hello [iniziare con l'IoT Hub](iot-hub-java-java-getstarted.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="da32e-206">Send telemetry from devices with hello [Get started with IoT Hub](iot-hub-java-java-getstarted.md) tutorial.</span></span>
* <span data-ttu-id="da32e-207">Controllare i dispositivi in modo interattivo (ad esempio l'attivazione di una ventola da un'app controllata dall'utente) con hello [utilizzare metodi diretti](iot-hub-java-java-direct-methods.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="da32e-207">Control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods](iot-hub-java-java-direct-methods.md) tutorial.</span></span>
