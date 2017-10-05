---
title: Creare il primo microservizio di Azure basato su attori in Java | Documentazione Microsoft
description: Questa esercitazione illustra la procedura per la creazione, il debug e la distribuzione di un semplice servizio basato su attore usando Service Fabric Reliable Actors.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 288f1ed1016f50031065e66444d2562427194dc7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="0394f-103">Introduzione a Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="0394f-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0394f-104">C# su Windows</span><span class="sxs-lookup"><span data-stu-id="0394f-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="0394f-105">Java su Linux</span><span class="sxs-lookup"><span data-stu-id="0394f-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="0394f-106">Questo articolo illustra le nozioni fondamentali di Azure Service Fabric Reliable Actors e le procedure per creare e distribuire una semplice applicazione Reliable Actors in Java.</span><span class="sxs-lookup"><span data-stu-id="0394f-106">This article explains the basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="0394f-107">Installazione e configurazione</span><span class="sxs-lookup"><span data-stu-id="0394f-107">Installation and setup</span></span>
<span data-ttu-id="0394f-108">Prima di iniziare, assicurarsi che nel computer sia configurato l'ambiente di sviluppo di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0394f-108">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="0394f-109">Se è necessario configurarlo, andare alla [guida introduttiva per Mac](service-fabric-get-started-mac.md) o alla [guida introduttiva per Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0394f-109">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="0394f-110">Concetti di base</span><span class="sxs-lookup"><span data-stu-id="0394f-110">Basic concepts</span></span>
<span data-ttu-id="0394f-111">Per iniziare a usare Reliable Actors, è sufficiente comprendere solo alcuni concetti di base:</span><span class="sxs-lookup"><span data-stu-id="0394f-111">To get started with Reliable Actors, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="0394f-112">**Servizio attore**.</span><span class="sxs-lookup"><span data-stu-id="0394f-112">**Actor service**.</span></span> <span data-ttu-id="0394f-113">Reliable Actors viene fornito in pacchetti di servizi Reliable Services che possono essere distribuiti nell'infrastruttura Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0394f-113">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span></span> <span data-ttu-id="0394f-114">Le istanze di Actors vengono attivate in un'istanza del servizio denominata.</span><span class="sxs-lookup"><span data-stu-id="0394f-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="0394f-115">**Registrazione attore**.</span><span class="sxs-lookup"><span data-stu-id="0394f-115">**Actor registration**.</span></span> <span data-ttu-id="0394f-116">Come con Reliable Services, un servizio Reliable Actor deve essere registrato con il runtime di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0394f-116">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="0394f-117">In più, il tipo di attore deve essere registrato con il runtime di Actor.</span><span class="sxs-lookup"><span data-stu-id="0394f-117">In addition, the actor type needs to be registered with the Actor runtime.</span></span>
* <span data-ttu-id="0394f-118">**Interfaccia attore**.</span><span class="sxs-lookup"><span data-stu-id="0394f-118">**Actor interface**.</span></span> <span data-ttu-id="0394f-119">Questa interfaccia viene usata per definire l'interfaccia pubblica fortemente tipizzata di un attore.</span><span class="sxs-lookup"><span data-stu-id="0394f-119">The actor interface is used to define a strongly typed public interface of an actor.</span></span> <span data-ttu-id="0394f-120">In base alla terminologia modello di Reliable Actors, questa interfaccia definisce i tipi di messaggi che l'attore può comprendere ed eseguire.</span><span class="sxs-lookup"><span data-stu-id="0394f-120">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span></span> <span data-ttu-id="0394f-121">L'interfaccia attore viene usata da altri attori o applicazioni client per "inviare" messaggi all'attore (in modo asincrono).</span><span class="sxs-lookup"><span data-stu-id="0394f-121">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span></span> <span data-ttu-id="0394f-122">Reliable Actors può implementare più interfacce.</span><span class="sxs-lookup"><span data-stu-id="0394f-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="0394f-123">**Classe ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="0394f-123">**ActorProxy class**.</span></span> <span data-ttu-id="0394f-124">La classe ActorProxy viene usata dalle applicazioni client per richiamare i metodi esposti tramite l'interfaccia attore.</span><span class="sxs-lookup"><span data-stu-id="0394f-124">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span></span> <span data-ttu-id="0394f-125">La classe ActorProxy fornisce due funzionalità importanti:</span><span class="sxs-lookup"><span data-stu-id="0394f-125">The ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="0394f-126">Risoluzione dei nomi: la classe è in grado di individuare l'attore nel cluster, ossia trovare il nodo del cluster in cui è ospitato.</span><span class="sxs-lookup"><span data-stu-id="0394f-126">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span></span>
  * <span data-ttu-id="0394f-127">Gestione degli errori: la classe può ripetere le chiamate al metodo e risolvere nuovamente la posizione dell'attore, ad esempio dopo un errore che richiede lo spostamento dell'attore in un altro nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="0394f-127">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span></span>

<span data-ttu-id="0394f-128">È opportuno citare le regole seguenti relative alle interfacce dell'attore:</span><span class="sxs-lookup"><span data-stu-id="0394f-128">The following rules that pertain to actor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="0394f-129">I metodi di interfaccia dell'attore non possono essere sottoposti a overload.</span><span class="sxs-lookup"><span data-stu-id="0394f-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="0394f-130">I metodi di interfaccia dell'attore non accettano parametri facoltativi, out o ref.</span><span class="sxs-lookup"><span data-stu-id="0394f-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="0394f-131">Non sono supportate interfacce generiche.</span><span class="sxs-lookup"><span data-stu-id="0394f-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="0394f-132">Creare un servizio Actor</span><span class="sxs-lookup"><span data-stu-id="0394f-132">Create an actor service</span></span>
<span data-ttu-id="0394f-133">Per iniziare, creare una nuova applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0394f-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="0394f-134">Service Fabric SDK per Linux include un generatore Yeoman per la creazione dello scaffolding per un'applicazione di Service Fabric con un servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="0394f-134">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="0394f-135">Iniziare eseguendo il comando Yeoman seguente:</span><span class="sxs-lookup"><span data-stu-id="0394f-135">Start by running the following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="0394f-136">Seguire le istruzioni per creare un **servizio Actor senza stato**.</span><span class="sxs-lookup"><span data-stu-id="0394f-136">Follow the instructions to create a **Reliable Actor Service**.</span></span> <span data-ttu-id="0394f-137">Per questa esercitazione, denominare l'applicazione "HelloWorldActorApplication" e il servizio Actor "HelloWorldActor".</span><span class="sxs-lookup"><span data-stu-id="0394f-137">For this tutorial, name the application "HelloWorldActorApplication" and the actor "HelloWorldActor."</span></span> <span data-ttu-id="0394f-138">Verrà creato lo scaffolding seguente:</span><span class="sxs-lookup"><span data-stu-id="0394f-138">The following scaffolding will be created:</span></span>

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="0394f-139">Blocchi predefiniti di base di Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="0394f-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="0394f-140">I concetti fondamentali descritti in precedenza si traducono nei blocchi predefiniti di base di un servizio Reliable Actor.</span><span class="sxs-lookup"><span data-stu-id="0394f-140">The basic concepts described earlier translate into the basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="0394f-141">Interfaccia dell'attore</span><span class="sxs-lookup"><span data-stu-id="0394f-141">Actor interface</span></span>
<span data-ttu-id="0394f-142">Questo blocco include la definizione dell'interfaccia per l'attore.</span><span class="sxs-lookup"><span data-stu-id="0394f-142">This contains the interface definition for the actor.</span></span> <span data-ttu-id="0394f-143">Questa interfaccia definisce il contratto dell'attore che è condiviso dall'implementazione dell'attore e i client che chiamano l'attore, quindi è in genere opportuno definirlo in una posizione separata rispetto all'implementazione dell'attore e può essere condiviso da molti altri servizi o applicazioni client.</span><span class="sxs-lookup"><span data-stu-id="0394f-143">This interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in a place that is separate from the actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="0394f-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span><span class="sxs-lookup"><span data-stu-id="0394f-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="0394f-145">Servizio Actor</span><span class="sxs-lookup"><span data-stu-id="0394f-145">Actor service</span></span>
<span data-ttu-id="0394f-146">Questo blocco contiene l'implementazione dell'attore e il codice di registrazione dell'attore.</span><span class="sxs-lookup"><span data-stu-id="0394f-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="0394f-147">La classe dell'attore implementa l'interfaccia dell'attore.</span><span class="sxs-lookup"><span data-stu-id="0394f-147">The actor class implements the actor interface.</span></span> <span data-ttu-id="0394f-148">Questa è la posizione in cui l'attore svolge il suo lavoro.</span><span class="sxs-lookup"><span data-stu-id="0394f-148">This is where your actor does its work.</span></span>

<span data-ttu-id="0394f-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span><span class="sxs-lookup"><span data-stu-id="0394f-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a><span data-ttu-id="0394f-150">Registrazione dell'attore</span><span class="sxs-lookup"><span data-stu-id="0394f-150">Actor registration</span></span>
<span data-ttu-id="0394f-151">Il servizio Actor deve essere registrato con un tipo di servizio nel runtime di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0394f-151">The actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="0394f-152">Perché il servizio Actor possa eseguire le istanze degli attori, è necessario che anche il proprio tipo di attore sia registrato con il servizio Actor.</span><span class="sxs-lookup"><span data-stu-id="0394f-152">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span></span> <span data-ttu-id="0394f-153">Il metodo di registrazione `ActorRuntime` esegue questa attività per gli attori.</span><span class="sxs-lookup"><span data-stu-id="0394f-153">The `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="0394f-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span><span class="sxs-lookup"><span data-stu-id="0394f-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a><span data-ttu-id="0394f-155">Client di prova</span><span class="sxs-lookup"><span data-stu-id="0394f-155">Test client</span></span>
<span data-ttu-id="0394f-156">Questa è una semplice applicazione client di test che è possibile eseguire separatamente dall'applicazione di Service Fabric per testare il servizio attore.</span><span class="sxs-lookup"><span data-stu-id="0394f-156">This is a simple test client application you can run separately from the Service Fabric application to test your actor service.</span></span> <span data-ttu-id="0394f-157">Questo è un esempio della posizione in cui è possibile usare ActorProxy per attivare e comunicare con le istanze dell'attore.</span><span class="sxs-lookup"><span data-stu-id="0394f-157">This is an example of where the ActorProxy can be used to activate and communicate with actor instances.</span></span> <span data-ttu-id="0394f-158">Non viene distribuito con il servizio.</span><span class="sxs-lookup"><span data-stu-id="0394f-158">It does not get deployed with your service.</span></span>

### <a name="the-application"></a><span data-ttu-id="0394f-159">Applicazione</span><span class="sxs-lookup"><span data-stu-id="0394f-159">The application</span></span>
<span data-ttu-id="0394f-160">Infine, l'applicazione che include il servizio dell'attore e qualsiasi altro servizio aggiunto in futuro per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="0394f-160">Finally, the application packages the actor service and any other services you might add in the future together for deployment.</span></span> <span data-ttu-id="0394f-161">Contiene il file *ApplicationManifest.xml* e segnaposto per il pacchetto del servizio dell'attore.</span><span class="sxs-lookup"><span data-stu-id="0394f-161">It contains the *ApplicationManifest.xml* and place holders for the actor service package.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="0394f-162">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="0394f-162">Run the application</span></span>

<span data-ttu-id="0394f-163">Lo scaffolding Yeoman include uno script Gradle per compilare l'applicazione e script Bash per distribuire ed eliminare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0394f-163">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and remove the application.</span></span> <span data-ttu-id="0394f-164">Per distribuire l'applicazione, prima di tutto compilarla con Gradle:</span><span class="sxs-lookup"><span data-stu-id="0394f-164">To deploy the application, first build the application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="0394f-165">Si otterrà un pacchetto dell'applicazione di Service Fabric che può essere distribuito tramite gli strumenti dell'interfaccia della riga di comando di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0394f-165">This will produce a Service Fabric application package that can be deployed using Service Fabric CLI tools.</span></span>

### <a name="deploy-service-fabric-cli"></a><span data-ttu-id="0394f-166">Distribuire l'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0394f-166">Deploy Service Fabric CLI</span></span>

<span data-ttu-id="0394f-167">Lo script install.sh contiene i comandi dell'interfaccia della riga di comando di Service Fabric (sfctl) necessari per distribuire il pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0394f-167">The install.sh script contains the necessary Service Fabric CLI (sfctl) commands to deploy the application package.</span></span>
<span data-ttu-id="0394f-168">Eseguire lo script install.sh per distribuire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0394f-168">Run the install.sh script to deploy the application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="0394f-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0394f-169">Next steps</span></span>

* [<span data-ttu-id="0394f-170">Introduzione all'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0394f-170">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
