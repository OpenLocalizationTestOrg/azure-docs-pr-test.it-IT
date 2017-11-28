---
title: un'applicazione Java di Azure Service Fabric attori affidabile in Linux aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate e distribuire un'applicazione di attori affidabile Java Service Fabric in cinque minuti.
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
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a><span data-ttu-id="bb9ae-103">Creare la prima applicazione Java Reliable Actors di Service Fabric in Linux</span><span class="sxs-lookup"><span data-stu-id="bb9ae-103">Create your first Java Service Fabric Reliable Actors application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bb9ae-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="bb9ae-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="bb9ae-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="bb9ae-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="bb9ae-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="bb9ae-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="bb9ae-107">Questa guida introduttiva consente di creare in pochi minuti la prima applicazione Java di Azure Service Fabric in un ambiente di sviluppo Linux.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-107">This quick-start helps you create your first Azure Service Fabric Java application in a Linux development environment in just a few minutes.</span></span>  <span data-ttu-id="bb9ae-108">Al termine, sarà necessario una semplice applicazione di servizio singolo Java in esecuzione nel cluster di sviluppo locale hello.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-108">When you are finished, you'll have a simple Java single-service application running on hello local development cluster.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="bb9ae-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bb9ae-109">Prerequisites</span></span>
<span data-ttu-id="bb9ae-110">Prima di iniziare, installare Service Fabric SDK hello, hello servizio infrastruttura CLI e del programma di installazione in un cluster di sviluppo del [ambiente di sviluppo di Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="bb9ae-110">Before you get started, install hello Service Fabric SDK, hello Service Fabric CLI, and setup a development cluster in your [Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="bb9ae-111">Se si usa Mac OS X, è possibile [configurare un ambiente di sviluppo Linux in una macchina virtuale usando Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="bb9ae-111">If you are using Mac OS X, you can [set up a Linux development environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="bb9ae-112">È anche possibile hello tooinstall [servizio infrastruttura CLI](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bb9ae-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md).</span></span>

### <a name="install-and-set-up-hello-generators-for-java"></a><span data-ttu-id="bb9ae-113">Installare e configurare i generatori di hello per Java</span><span class="sxs-lookup"><span data-stu-id="bb9ae-113">Install and set up hello generators for Java</span></span>
<span data-ttu-id="bb9ae-114">Service Fabric offre gli strumenti di scaffolding che consentono di creare un'applicazione Java di Service Fabric dal terminale tramite il generatore di modelli Yeoman.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric Java application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="bb9ae-115">Eseguire procedure hello sotto tooensure che aver generatore di modello yeoman hello Service Fabric per Java utilizzo nel computer.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for Java working on your machine.</span></span>
1. <span data-ttu-id="bb9ae-116">Installare nodejs e NPM nella macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="bb9ae-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="bb9ae-117">Installare il generatore di modelli [Yeoman](http://yeoman.io/) nella macchina virtuale da NPM</span><span class="sxs-lookup"><span data-stu-id="bb9ae-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="bb9ae-118">Installare generatore di applicazione di servizio Fabric Yeo Java hello da NPM</span><span class="sxs-lookup"><span data-stu-id="bb9ae-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a><span data-ttu-id="bb9ae-119">Creare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="bb9ae-119">Create hello application</span></span>
<span data-ttu-id="bb9ae-120">Un'applicazione di Service Fabric contiene uno o più servizi, ognuno con un ruolo specifico nell'offerta di funzionalità dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-120">A Service Fabric application contains one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="bb9ae-121">Generatore di Hello è installato nell'ultima sezione hello, rende facile toocreate il primo servizio e tooadd più avanti.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-121">hello generator you installed in hello last section, makes it easy toocreate your first service and tooadd more later.</span></span>  <span data-ttu-id="bb9ae-122">È anche possibile creare, compilare e distribuire applicazioni Java di Service Fabric usando un plug-in per Eclipse.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-122">You can also create, build, and deploy Service Fabric Java applications using a plugin for Eclipse.</span></span> <span data-ttu-id="bb9ae-123">Vedere [Creare e distribuire la prima applicazione Java usando Eclipse](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="bb9ae-123">See [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md).</span></span> <span data-ttu-id="bb9ae-124">Per questa Guida introduttiva usare Yeoman toocreate un'applicazione con un unico servizio che consente di archiviare e ottiene un valore del contatore.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-124">For this quick start, use Yeoman toocreate an application with a single service that stores and gets a counter value.</span></span>

1. <span data-ttu-id="bb9ae-125">In un terminale digitare ``yo azuresfjava``.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-125">In a terminal, type ``yo azuresfjava``.</span></span>
2. <span data-ttu-id="bb9ae-126">Assegnare un nome all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-126">Name your application.</span></span>
3. <span data-ttu-id="bb9ae-127">Scegliere il tipo di hello del primo servizio e il nome.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-127">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="bb9ae-128">Per questa esercitazione, scegliere un servizio Reliable Actor.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-128">For this tutorial, choose a Reliable Actor Service.</span></span> <span data-ttu-id="bb9ae-129">Per ulteriori informazioni su hello altri tipi di servizi, vedere [Cenni preliminari sul modello di programmazione di Service Fabric](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="bb9ae-129">For more information about hello other types of services, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
   <span data-ttu-id="bb9ae-130">![Generatore Yeoman di Service Fabric per Java][sf-yeoman]</span><span class="sxs-lookup"><span data-stu-id="bb9ae-130">![Service Fabric Yeoman generator for Java][sf-yeoman]</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="bb9ae-131">Compilare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="bb9ae-131">Build hello application</span></span>
<span data-ttu-id="bb9ae-132">modelli di servizio dell'infrastruttura Yeoman Hello includono uno script di compilazione per [Gradle](https://gradle.org/), che è possibile utilizzare un'applicazione hello toobuild da hello terminal.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-132">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span>
<span data-ttu-id="bb9ae-133">Le dipendenze Java di Service Fabric vengono recuperate da Maven.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-133">Service Fabric Java dependencies get fetched from Maven.</span></span> <span data-ttu-id="bb9ae-134">toobuild e attività per le applicazioni Java di infrastruttura servizio hello, è necessario tooensure che si disponga di JDK e Gradle installato.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-134">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK and Gradle installed.</span></span> <span data-ttu-id="bb9ae-135">Se non è ancora installato, è possibile eseguire hello seguito tooinstall JDK(openjdk-8-jdk) e Gradle -</span><span class="sxs-lookup"><span data-stu-id="bb9ae-135">If not yet installed, you can run hello following tooinstall JDK(openjdk-8-jdk) and Gradle -</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

<span data-ttu-id="bb9ae-136">toobuild e pacchetto applicazione hello, eseguire hello seguente:</span><span class="sxs-lookup"><span data-stu-id="bb9ae-136">toobuild and package hello application, run hello following:</span></span>

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="bb9ae-137">Distribuire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="bb9ae-137">Deploy hello application</span></span>
<span data-ttu-id="bb9ae-138">Una volta creata l'applicazione hello, è possibile distribuire cluster locale toohello.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-138">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="bb9ae-139">Connettere il cluster di Service Fabric locale toohello.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-139">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="bb9ae-140">Eseguire script di installazione di hello fornito in hello modello toocopy applicazione hello pacchetto archivio immagini toohello del cluster, registrare il tipo di applicazione hello e creare un'istanza di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-140">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="bb9ae-141">Distribuire un'applicazione hello compilato è hello stesso come qualsiasi altra applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-141">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="bb9ae-142">Vedere la documentazione di hello su [la gestione di un'applicazione di Service Fabric con hello servizio infrastruttura CLI](service-fabric-application-lifecycle-sfctl.md) per istruzioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-142">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="bb9ae-143">I parametri toothese comandi sono disponibili nei manifesti hello generato all'interno del pacchetto di applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-143">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="bb9ae-144">Dopo la distribuzione di un'applicazione hello, aprire un browser e passare a [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) in [http://localhost:19080/Esplora](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="bb9ae-144">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span>
<span data-ttu-id="bb9ae-145">Espandere quindi hello **applicazioni** nodo e notare che è ora disponibile una voce per il tipo di applicazione e un altro per hello prima istanza di quel tipo.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-145">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="bb9ae-146">Avviare il client di prova hello ed eseguire un failover</span><span class="sxs-lookup"><span data-stu-id="bb9ae-146">Start hello test client and perform a failover</span></span>
<span data-ttu-id="bb9ae-147">Gli attori non eseguire alcuna operazione in modo autonomo, richiedono un altro servizio o client di toosend tali messaggi.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-147">Actors do not do anything on their own, they require another service or client toosend them messages.</span></span> <span data-ttu-id="bb9ae-148">modello attore Hello include uno script di test semplice che è possibile utilizzare toointeract con servizio actor hello.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-148">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="bb9ae-149">Eseguire script hello utilizzando hello espressioni di controllo utilità toosee hello output del servizio actor hello.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-149">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>  <span data-ttu-id="bb9ae-150">script di test hello chiama hello `setCountAsync()` metodo hello attore tooincrement un contatore, chiama hello `getCountAsync()` metodo hello attore tooget hello nuovo valore del contatore e consente di visualizzare tale valore toohello console.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-150">hello test script calls hello `setCountAsync()` method on hello actor tooincrement a counter, calls hello `getCountAsync()` method on hello actor tooget hello new counter value, and displays that value toohello console.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. <span data-ttu-id="bb9ae-151">In Service Fabric Explorer, individuare hello nodo hosting hello replica primaria per il servizio actor hello.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-151">In Service Fabric Explorer, locate hello node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="bb9ae-152">Nella schermata di hello riportata di seguito, è il nodo 3.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-152">In hello screenshot below, it is node 3.</span></span> <span data-ttu-id="bb9ae-153">Hello servizio primario replica gestisce operazioni lettura e scrittura.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-153">hello primary service replica handles read and write operations.</span></span>  <span data-ttu-id="bb9ae-154">Modifiche di stato del servizio vengono quindi replicate out toohello repliche secondarie, in esecuzione su 0 e 1 nella schermata di hello sotto i nodi.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-154">Changes in service state are then replicated out toohello secondary replicas, running on nodes 0 and 1 in hello screen shot below.</span></span>

    ![Trovare la replica primaria hello in Service Fabric Explorer][sfx-primary]

3. <span data-ttu-id="bb9ae-156">In **nodi**, fare clic sul nodo hello è stata individuata nel passaggio precedente hello, scegliere **Deactivate (riavvio)** dal menu Azioni hello.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-156">In **Nodes**, click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="bb9ae-157">Questa azione riavvia il nodo hello esegue hello servizio primario replica e forza un tooone failover delle repliche secondarie di hello in esecuzione in un altro nodo.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-157">This action restarts hello node running hello primary service replica and forces a failover tooone of hello secondary replicas running on another node.</span></span>  <span data-ttu-id="bb9ae-158">Replica secondaria è tooprimary innalzate di livello, viene creata un'altra replica secondaria su un nodo diverso e la replica primaria hello inizia le operazioni di lettura/scrittura tootake.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-158">That secondary replica is promoted tooprimary, another secondary replica is created on a different node, and hello primary replica begins tootake read/write operations.</span></span> <span data-ttu-id="bb9ae-159">Come hello riavvii di nodo, espressioni di controllo di output di hello dalla hello client di prova e prendere nota di tale contatore hello continua tooincrement nonostante hello failover.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-159">As hello node restarts, watch hello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="remove-hello-application"></a><span data-ttu-id="bb9ae-160">Rimuovere un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="bb9ae-160">Remove hello application</span></span>
<span data-ttu-id="bb9ae-161">Utilizzare script di disinstallazione hello fornito nell'istanza di applicazione hello toodelete modello hello, annullare la registrazione del pacchetto dell'applicazione hello e rimuovere il pacchetto di applicazione hello dall'archivio di immagini del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-161">Use hello uninstall script provided in hello template toodelete hello application instance, unregister hello application package, and remove hello application package from hello cluster's image store.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="bb9ae-162">In Esplora Service Fabric è visualizzato che un'applicazione hello e tipo di applicazione non è più in hello **applicazioni** nodo.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-162">In Service Fabric explorer you see that hello application and application type no longer appear in hello **Applications** node.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="bb9ae-163">Librerie Java di Service Fabric in Maven</span><span class="sxs-lookup"><span data-stu-id="bb9ae-163">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="bb9ae-164">Le librerie Java di Service Fabric sono ospitate in Maven.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-164">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="bb9ae-165">È possibile aggiungere le dipendenze di hello in hello ``pom.xml`` o ``build.gradle`` di raccolte di Service Fabric Java toouse di progetti da **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-165">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="bb9ae-166">Actor</span><span class="sxs-lookup"><span data-stu-id="bb9ae-166">Actors</span></span>

<span data-ttu-id="bb9ae-167">Supporto di Service Fabric Reliable Actors per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-167">Service Fabric Reliable Actor support for your application.</span></span>

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

### <a name="services"></a><span data-ttu-id="bb9ae-168">Services</span><span class="sxs-lookup"><span data-stu-id="bb9ae-168">Services</span></span>

<span data-ttu-id="bb9ae-169">Supporto di servizi senza stato di Service Fabric per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-169">Service Fabric Stateless Service support for your application.</span></span>

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

### <a name="others"></a><span data-ttu-id="bb9ae-170">Altro</span><span class="sxs-lookup"><span data-stu-id="bb9ae-170">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="bb9ae-171">Trasporto</span><span class="sxs-lookup"><span data-stu-id="bb9ae-171">Transport</span></span>

<span data-ttu-id="bb9ae-172">Supporto del livello trasporto per l'applicazione Java di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-172">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="bb9ae-173">Non è necessario tooexplicitly aggiungere questa dipendenza tooyour Reliable Actor o applicazioni di servizio, a meno che la programmazione a livello di trasporto hello.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-173">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

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

#### <a name="fabric-support"></a><span data-ttu-id="bb9ae-174">Supporto di Fabric</span><span class="sxs-lookup"><span data-stu-id="bb9ae-174">Fabric support</span></span>

<span data-ttu-id="bb9ae-175">Supporto di livello di sistema per l'infrastruttura del servizio, che comunica toonative runtime di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-175">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="bb9ae-176">Non è necessario tooexplicitly aggiungere questa dipendenza tooyour Reliable Actor o applicazioni di servizio.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-176">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="bb9ae-177">Si ottiene recuperato automaticamente da Maven, quando si includono hello altre dipendenze precedente.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-177">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

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

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="bb9ae-178">La migrazione precedente toobe di applicazioni Java di infrastruttura del servizio utilizzato con Maven</span><span class="sxs-lookup"><span data-stu-id="bb9ae-178">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="bb9ae-179">È stato spostato nella librerie di Service Fabric Java recente dal repository tooMaven Service Fabric Java SDK.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-179">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="bb9ae-180">Mentre le nuove applicazioni hello generati usando Yeoman o Eclipse, genererà progetti aggiornati più recente (che saranno in grado di toowork con Maven), è possibile aggiornare l'infrastruttura esistente di servizio senza stato o applicazioni Java attore che usavano hello servizio Fabric SDK per Java in precedenza, le dipendenze di Service Fabric Java hello toouse Maven.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-180">While hello new applications you generate using Yeoman or Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="bb9ae-181">Seguire i passaggi di hello indicati [qui](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure precedente applicazione funziona con Maven.</span><span class="sxs-lookup"><span data-stu-id="bb9ae-181">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb9ae-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bb9ae-182">Next steps</span></span>

* [<span data-ttu-id="bb9ae-183">Creare la prima applicazione Java di Service Fabric in Linux usando Eclipse</span><span class="sxs-lookup"><span data-stu-id="bb9ae-183">Create your first Service Fabric Java application on Linux using Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="bb9ae-184">Altre informazioni su Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="bb9ae-184">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="bb9ae-185">Interagire con i cluster di Service Fabric usando hello servizio infrastruttura CLI</span><span class="sxs-lookup"><span data-stu-id="bb9ae-185">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="bb9ae-186">Informazioni sulle [opzioni di supporto di Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="bb9ae-186">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="bb9ae-187">Introduzione all'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bb9ae-187">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
