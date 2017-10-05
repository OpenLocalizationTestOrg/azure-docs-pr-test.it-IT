---
title: Creare un'applicazione Java Reliable Actors di Azure Service Fabric in Linux | Microsoft Docs
description: Informazioni su come creare e distribuire un'applicazione Java Reliable Actors di Service Fabric in cinque minuti.
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: baf948587ede31fe3d5b4f6f0981269b4cfe4d3d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a><span data-ttu-id="fa1e1-103">Creare la prima applicazione Java Reliable Actors di Service Fabric in Linux</span><span class="sxs-lookup"><span data-stu-id="fa1e1-103">Create your first Java Service Fabric Reliable Actors application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fa1e1-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="fa1e1-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="fa1e1-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="fa1e1-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="fa1e1-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="fa1e1-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="fa1e1-107">Questa guida introduttiva consente di creare in pochi minuti la prima applicazione Java di Azure Service Fabric in un ambiente di sviluppo Linux.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-107">This quick-start helps you create your first Azure Service Fabric Java application in a Linux development environment in just a few minutes.</span></span>  <span data-ttu-id="fa1e1-108">Al termine, si avrà una semplice applicazione Java con un singolo servizio in esecuzione nel cluster di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-108">When you are finished, you'll have a simple Java single-service application running on the local development cluster.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="fa1e1-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fa1e1-109">Prerequisites</span></span>
<span data-ttu-id="fa1e1-110">Prima di iniziare, installare Service Fabric SDK e l'interfaccia della riga di comando di Service Fabric e configurare un cluster di sviluppo nell'[ambiente di sviluppo Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="fa1e1-110">Before you get started, install the Service Fabric SDK, the Service Fabric CLI, and setup a development cluster in your [Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="fa1e1-111">Se si usa Mac OS X, è possibile [configurare un ambiente di sviluppo Linux in una macchina virtuale usando Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="fa1e1-111">If you are using Mac OS X, you can [set up a Linux development environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="fa1e1-112">È consigliabile installare anche l'[interfaccia della riga di comando di Service Fabric](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fa1e1-112">You will also want to install the [Service Fabric CLI](service-fabric-cli.md).</span></span>

### <a name="install-and-set-up-the-generators-for-java"></a><span data-ttu-id="fa1e1-113">Installare e configurare i generatori per Java</span><span class="sxs-lookup"><span data-stu-id="fa1e1-113">Install and set up the generators for Java</span></span>
<span data-ttu-id="fa1e1-114">Service Fabric offre gli strumenti di scaffolding che consentono di creare un'applicazione Java di Service Fabric dal terminale tramite il generatore di modelli Yeoman.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric Java application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="fa1e1-115">Seguire questa procedura per assicurarsi che nella macchina virtuale sia disponibile il generatore di modelli Yeoman di Service Fabric per Java.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-115">Please follow the steps below to ensure you have the Service Fabric yeoman template generator for Java working on your machine.</span></span>
1. <span data-ttu-id="fa1e1-116">Installare nodejs e NPM nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="fa1e1-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="fa1e1-117">Installare il generatore di modelli [Yeoman](http://yeoman.io/) nella macchina virtuale da NPM</span><span class="sxs-lookup"><span data-stu-id="fa1e1-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="fa1e1-118">Installare il generatore di applicazioni Java Yeo di Service Fabric da NPM</span><span class="sxs-lookup"><span data-stu-id="fa1e1-118">Install the Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-the-application"></a><span data-ttu-id="fa1e1-119">Creazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="fa1e1-119">Create the application</span></span>
<span data-ttu-id="fa1e1-120">Un'applicazione di Service Fabric contiene uno o più servizi, ognuno dei quali contribuisce alle funzionalità dell'applicazione con un ruolo specifico.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-120">A Service Fabric application contains one or more services, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="fa1e1-121">Il generatore installato nell'ultima sezione semplifica la creazione del primo servizio e l'aggiunta di altri servizi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-121">The generator you installed in the last section, makes it easy to create your first service and to add more later.</span></span>  <span data-ttu-id="fa1e1-122">È anche possibile creare, compilare e distribuire applicazioni Java di Service Fabric usando un plug-in per Eclipse.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-122">You can also create, build, and deploy Service Fabric Java applications using a plugin for Eclipse.</span></span> <span data-ttu-id="fa1e1-123">Vedere [Creare e distribuire la prima applicazione Java usando Eclipse](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="fa1e1-123">See [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md).</span></span> <span data-ttu-id="fa1e1-124">Per questa guida introduttiva, usare Yeoman per creare un'applicazione con un unico servizio per archiviare e ottenere un valore del contatore.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-124">For this quick start, use Yeoman to create an application with a single service that stores and gets a counter value.</span></span>

1. <span data-ttu-id="fa1e1-125">In un terminale digitare ``yo azuresfjava``.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-125">In a terminal, type ``yo azuresfjava``.</span></span>
2. <span data-ttu-id="fa1e1-126">Assegnare un nome all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-126">Name your application.</span></span>
3. <span data-ttu-id="fa1e1-127">Scegliere il tipo del primo servizio e assegnargli un nome.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-127">Choose the type of your first service and name it.</span></span> <span data-ttu-id="fa1e1-128">Per questa esercitazione, scegliere un servizio Reliable Actor.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-128">For this tutorial, choose a Reliable Actor Service.</span></span> <span data-ttu-id="fa1e1-129">Per altre informazioni sugli altri tipi di servizi, vedere [Panoramica dei modelli di programmazione di Service Fabric](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="fa1e1-129">For more information about the other types of services, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
   <span data-ttu-id="fa1e1-130">![Generatore Yeoman di Service Fabric per Java][sf-yeoman]</span><span class="sxs-lookup"><span data-stu-id="fa1e1-130">![Service Fabric Yeoman generator for Java][sf-yeoman]</span></span>

## <a name="build-the-application"></a><span data-ttu-id="fa1e1-131">Compilare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-131">Build the application</span></span>
<span data-ttu-id="fa1e1-132">I modelli Yeoman di Service Fabric includono uno script di compilazione per [Gradle](https://gradle.org/), che può essere usato per compilare l'applicazione dal terminale.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-132">The Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use to build the application from the terminal.</span></span>
<span data-ttu-id="fa1e1-133">Le dipendenze Java di Service Fabric vengono recuperate da Maven.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-133">Service Fabric Java dependencies get fetched from Maven.</span></span> <span data-ttu-id="fa1e1-134">Per compilare e usare le applicazioni Java di Service Fabric, è necessario verificare che siano installati JDK e Gradle.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-134">To build and work on the Service Fabric Java applications, you need to ensure that you have JDK and Gradle installed.</span></span> <span data-ttu-id="fa1e1-135">Se non sono ancora installati, è possibile eseguire questi comandi per installare JDK (openjdk-8-jdk) e Gradle:</span><span class="sxs-lookup"><span data-stu-id="fa1e1-135">If not yet installed, you can run the following to install JDK(openjdk-8-jdk) and Gradle -</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

<span data-ttu-id="fa1e1-136">Per compilare l'applicazione e creare il pacchetto, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="fa1e1-136">To build and package the application, run the following:</span></span>

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-the-application"></a><span data-ttu-id="fa1e1-137">Distribuire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="fa1e1-137">Deploy the application</span></span>
<span data-ttu-id="fa1e1-138">Dopo aver compilato l'applicazione, è possibile distribuirla nel cluster locale.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-138">Once the application is built, you can deploy it to the local cluster.</span></span>

1. <span data-ttu-id="fa1e1-139">Connettersi al cluster locale di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-139">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="fa1e1-140">Eseguire lo script di installazione messo a disposizione nel modello per copiare il pacchetto dell'applicazione nell'archivio immagini del cluster, registrare il tipo di applicazione e creare un'istanza dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-140">Run the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="fa1e1-141">La distribuzione dell'applicazione compilata è uguale a quella di qualsiasi altra applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-141">Deploying the built application is the same as any other Service Fabric application.</span></span> <span data-ttu-id="fa1e1-142">Per istruzioni dettagliate, vedere la documentazione sulla [gestione di un'applicazione di Service Fabric con l'interfaccia della riga di comando di Service Fabric](service-fabric-application-lifecycle-sfctl.md).</span><span class="sxs-lookup"><span data-stu-id="fa1e1-142">See the documentation on [managing a Service Fabric application with the Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="fa1e1-143">I parametri per questi comandi si trovano nei manifesti generati nel pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-143">Parameters to these commands can be found in the generated manifests inside the application package.</span></span>

<span data-ttu-id="fa1e1-144">Dopo la distribuzione dell'applicazione, aprire un browser e passare a [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) all'indirizzo [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="fa1e1-144">Once the application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span>
<span data-ttu-id="fa1e1-145">Espandere quindi il nodo **Applicazioni**, nel quale sarà ora presente una voce per il tipo di applicazione e un'altra per la prima istanza del tipo.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-145">Then, expand the **Applications** node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

## <a name="start-the-test-client-and-perform-a-failover"></a><span data-ttu-id="fa1e1-146">Avviare il client di test ed eseguire un failover</span><span class="sxs-lookup"><span data-stu-id="fa1e1-146">Start the test client and perform a failover</span></span>
<span data-ttu-id="fa1e1-147">Gli attori non eseguono alcuna operazione in modo indipendente, ma richiedono un altro servizio o client per l'invio dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-147">Actors do not do anything on their own, they require another service or client to send them messages.</span></span> <span data-ttu-id="fa1e1-148">Il modello Actor include un semplice script di test che è possibile usare per interagire con il servizio Actor.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-148">The actor template includes a simple test script that you can use to interact with the actor service.</span></span>

1. <span data-ttu-id="fa1e1-149">Eseguire lo script tramite l'utilità delle espressioni di controllo per visualizzare l'output del servizio Actor.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-149">Run the script using the watch utility to see the output of the actor service.</span></span>  <span data-ttu-id="fa1e1-150">Lo script di test chiama il metodo `setCountAsync()` nell'attore per incrementare un contatore, chiama il metodo `getCountAsync()` nell'attore per ottenere il nuovo valore del contatore e visualizza tale valore nella console.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-150">The test script calls the `setCountAsync()` method on the actor to increment a counter, calls the `getCountAsync()` method on the actor to get the new counter value, and displays that value to the console.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. <span data-ttu-id="fa1e1-151">In Service Fabric Explorer individuare il nodo che ospita la replica primaria del servizio Actor.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-151">In Service Fabric Explorer, locate the node hosting the primary replica for the actor service.</span></span> <span data-ttu-id="fa1e1-152">Nello screenshot seguente si tratta del nodo 3.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-152">In the screenshot below, it is node 3.</span></span> <span data-ttu-id="fa1e1-153">La replica di servizi primaria gestisce le operazioni di lettura e scrittura.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-153">The primary service replica handles read and write operations.</span></span>  <span data-ttu-id="fa1e1-154">Le modifiche allo stato del servizio vengono quindi replicate nelle repliche secondarie, in esecuzione nei nodi 0 e 1 nello screenshot seguente.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-154">Changes in service state are then replicated out to the secondary replicas, running on nodes 0 and 1 in the screen shot below.</span></span>

    ![Ricerca della replica primaria in Service Fabric Explorer][sfx-primary]

3. <span data-ttu-id="fa1e1-156">In **Nodi** fare clic sul nodo trovato nel passaggio precedente e quindi scegliere **Disattiva (riavvio)** dal menu Azioni.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-156">In **Nodes**, click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu.</span></span> <span data-ttu-id="fa1e1-157">Questa azione consente di riavviare il nodo che esegue la replica di servizi primaria e di forzare il failover in una delle repliche secondarie in esecuzione in un altro nodo.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-157">This action restarts the node running the primary service replica and forces a failover to one of the secondary replicas running on another node.</span></span>  <span data-ttu-id="fa1e1-158">Questa replica secondaria viene alzata di livello a primaria, un'altra replica secondaria viene creata in un nodo diverso e la replica primaria inizia a eseguire operazioni di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-158">That secondary replica is promoted to primary, another secondary replica is created on a different node, and the primary replica begins to take read/write operations.</span></span> <span data-ttu-id="fa1e1-159">Durante il riavvio del nodo, osservare l'output dal client di test e notare che l'incremento del contatore prosegue nonostante il failover.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-159">As the node restarts, watch the output from the test client and note that the counter continues to increment despite the failover.</span></span>

## <a name="remove-the-application"></a><span data-ttu-id="fa1e1-160">Rimuovere l'applicazione</span><span class="sxs-lookup"><span data-stu-id="fa1e1-160">Remove the application</span></span>
<span data-ttu-id="fa1e1-161">Usare lo script di disinstallazione incluso nel modello per eliminare l'istanza dell'applicazione, annullare la registrazione del pacchetto dell'applicazione e rimuovere tale pacchetto dall'archivio immagini del cluster.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-161">Use the uninstall script provided in the template to delete the application instance, unregister the application package, and remove the application package from the cluster's image store.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="fa1e1-162">In Service Fabric Explorer si noterà che l'applicazione e il tipo di applicazione non sono più visualizzati nel nodo **Applicazioni**.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-162">In Service Fabric explorer you see that the application and application type no longer appear in the **Applications** node.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="fa1e1-163">Librerie Java di Service Fabric in Maven</span><span class="sxs-lookup"><span data-stu-id="fa1e1-163">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="fa1e1-164">Le librerie Java di Service Fabric sono ospitate in Maven.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-164">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="fa1e1-165">È possibile aggiungere le dipendenze nel file ``pom.xml`` o ``build.gradle`` dei progetti per usare le librerie Java di Service Fabric da **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-165">You can add the dependencies in the ``pom.xml`` or ``build.gradle`` of your projects to use Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="fa1e1-166">Actor</span><span class="sxs-lookup"><span data-stu-id="fa1e1-166">Actors</span></span>

<span data-ttu-id="fa1e1-167">Supporto di Service Fabric Reliable Actors per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-167">Service Fabric Reliable Actor support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a><span data-ttu-id="fa1e1-168">Services</span><span class="sxs-lookup"><span data-stu-id="fa1e1-168">Services</span></span>

<span data-ttu-id="fa1e1-169">Supporto di servizi senza stato di Service Fabric per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-169">Service Fabric Stateless Service support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a><span data-ttu-id="fa1e1-170">Altro</span><span class="sxs-lookup"><span data-stu-id="fa1e1-170">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="fa1e1-171">Trasporto</span><span class="sxs-lookup"><span data-stu-id="fa1e1-171">Transport</span></span>

<span data-ttu-id="fa1e1-172">Supporto del livello trasporto per l'applicazione Java di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-172">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="fa1e1-173">Non è necessario aggiungere esplicitamente questa dipendenza alle applicazioni Reliable Actors o Services, a meno che non si esegua la programmazione al livello trasporto.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-173">You do not need to explicitly add this dependency to your Reliable Actor or Service applications, unless you program at the transport layer.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a><span data-ttu-id="fa1e1-174">Supporto di Fabric</span><span class="sxs-lookup"><span data-stu-id="fa1e1-174">Fabric support</span></span>

<span data-ttu-id="fa1e1-175">Supporto a livello di sistema per Service Fabric, che comunica con il runtime nativo di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-175">System level support for Service Fabric, which talks to native Service Fabric runtime.</span></span> <span data-ttu-id="fa1e1-176">Non è necessario aggiungere esplicitamente questa dipendenza alle applicazioni Reliable Actors o Services.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-176">You do not need to explicitly add this dependency to your Reliable Actor or Service applications.</span></span> <span data-ttu-id="fa1e1-177">Viene recuperata automaticamente da Maven quando si includono le altre dipendenze riportate sopra.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-177">This gets fetched automatically from Maven, when you include the other dependencies above.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```

## <a name="migrating-old-service-fabric-java-applications-to-be-used-with-maven"></a><span data-ttu-id="fa1e1-178">Migrazione di applicazioni Java di Service Fabric precedenti da usare con Maven</span><span class="sxs-lookup"><span data-stu-id="fa1e1-178">Migrating old Service Fabric Java applications to be used with Maven</span></span>
<span data-ttu-id="fa1e1-179">Le librerie Java di Service Fabric sono state recentemente spostate da Service Fabric Java SDK al repository di Maven.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-179">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK to Maven repository.</span></span> <span data-ttu-id="fa1e1-180">Benché le nuove applicazioni generate con Yeoman o Eclipse genereranno i progetti aggiornati più recenti (in grado di interagire con Maven), è possibile aggiornare le applicazioni Java esistenti di Service Fabric senza stato o actor, che in precedenza usavano Service Fabric Java SDK, in modo che usino le dipendenze Java di Service Fabric da Maven.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-180">While the new applications you generate using Yeoman or Eclipse, will generate latest updated projects (which will be able to work with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using the Service Fabric Java SDK earlier, to use the Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="fa1e1-181">Seguire la procedura riportata [qui](service-fabric-migrate-old-javaapp-to-use-maven.md) per assicurare che l'applicazione precedente funzioni con Maven.</span><span class="sxs-lookup"><span data-stu-id="fa1e1-181">Please follow the steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) to ensure your older application works with Maven.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa1e1-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fa1e1-182">Next steps</span></span>

* [<span data-ttu-id="fa1e1-183">Creare la prima applicazione Java di Service Fabric in Linux usando Eclipse</span><span class="sxs-lookup"><span data-stu-id="fa1e1-183">Create your first Service Fabric Java application on Linux using Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="fa1e1-184">Altre informazioni su Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="fa1e1-184">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="fa1e1-185">Interagire con un cluster di Service Fabric usando l'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fa1e1-185">Interact with Service Fabric clusters using the Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="fa1e1-186">Informazioni sulle [opzioni di supporto di Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="fa1e1-186">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="fa1e1-187">Introduzione all'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fa1e1-187">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
