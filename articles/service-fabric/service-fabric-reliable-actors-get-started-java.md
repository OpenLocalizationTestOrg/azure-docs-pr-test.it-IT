---
title: aaaCreate il primo microservizio Azure basato su attori in Java | Documenti Microsoft
description: In questa esercitazione vengono illustrati i passaggi hello di creazione, il debug e distribuzione di un servizio basato su attori semplice usando Service Fabric Reliable Actors.
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
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="d841b-103">Introduzione a Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="d841b-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d841b-104">C# su Windows</span><span class="sxs-lookup"><span data-stu-id="d841b-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="d841b-105">Java su Linux</span><span class="sxs-lookup"><span data-stu-id="d841b-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="d841b-106">In questo articolo vengono illustrati concetti fondamentali di hello di Azure Service Fabric Reliable Actors e viene illustrato come creare e distribuire una semplice applicazione Reliable Actor in Java.</span><span class="sxs-lookup"><span data-stu-id="d841b-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="d841b-107">Installazione e configurazione</span><span class="sxs-lookup"><span data-stu-id="d841b-107">Installation and setup</span></span>
<span data-ttu-id="d841b-108">Prima di iniziare, verificare di che aver ambiente di sviluppo di Service Fabric hello configurare nel computer.</span><span class="sxs-lookup"><span data-stu-id="d841b-108">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="d841b-109">Se è necessario tooset, configurarlo, andare troppo[introduzione su Mac](service-fabric-get-started-mac.md) o [introduzione in Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d841b-109">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="d841b-110">Concetti di base</span><span class="sxs-lookup"><span data-stu-id="d841b-110">Basic concepts</span></span>
<span data-ttu-id="d841b-111">tooget introduttiva Reliable Actors, è solo necessario toounderstand alcuni concetti di base:</span><span class="sxs-lookup"><span data-stu-id="d841b-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="d841b-112">**Servizio attore**.</span><span class="sxs-lookup"><span data-stu-id="d841b-112">**Actor service**.</span></span> <span data-ttu-id="d841b-113">Reliable Actors sono inclusi nei servizi affidabili che può essere distribuito nell'infrastruttura di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="d841b-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="d841b-114">Le istanze di Actors vengono attivate in un'istanza del servizio denominata.</span><span class="sxs-lookup"><span data-stu-id="d841b-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="d841b-115">**Registrazione attore**.</span><span class="sxs-lookup"><span data-stu-id="d841b-115">**Actor registration**.</span></span> <span data-ttu-id="d841b-116">Come con i servizi affidabili, un servizio Reliable Actor deve toobe registrato con il runtime di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="d841b-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="d841b-117">Inoltre, è necessario toobe registrato con il runtime di attore hello tipo attore hello.</span><span class="sxs-lookup"><span data-stu-id="d841b-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="d841b-118">**Interfaccia attore**.</span><span class="sxs-lookup"><span data-stu-id="d841b-118">**Actor interface**.</span></span> <span data-ttu-id="d841b-119">interfaccia attore Hello è toodefine utilizzata un'interfaccia pubblica fortemente tipizzata di un attore.</span><span class="sxs-lookup"><span data-stu-id="d841b-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="d841b-120">Nella terminologia dei modelli Reliable Actor hello, interfaccia attore hello definisce hello tipi di messaggi hello attore possono comprendere ed elaborare.</span><span class="sxs-lookup"><span data-stu-id="d841b-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="d841b-121">interfaccia attore Hello viene utilizzato da altri attori e le applicazioni client troppo "inviano" (in modo asincrono) attore toohello messaggi.</span><span class="sxs-lookup"><span data-stu-id="d841b-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="d841b-122">Reliable Actors può implementare più interfacce.</span><span class="sxs-lookup"><span data-stu-id="d841b-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="d841b-123">**Classe ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="d841b-123">**ActorProxy class**.</span></span> <span data-ttu-id="d841b-124">classe ActorProxy Hello viene utilizzato da client applicazioni tooinvoke hello metodi esposti tramite l'interfaccia di hello attore.</span><span class="sxs-lookup"><span data-stu-id="d841b-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="d841b-125">classe ActorProxy Hello offre due funzionalità importanti:</span><span class="sxs-lookup"><span data-stu-id="d841b-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="d841b-126">Risoluzione dei nomi: è in grado di toolocate attore di hello cluster hello (Trova hello nodo del cluster di hello in cui è ospitato).</span><span class="sxs-lookup"><span data-stu-id="d841b-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="d841b-127">Gestione degli errori: può ripetere chiamate al metodo e risolvere nuovamente il percorso di attore hello dopo, ad esempio, un errore che richiede hello attore toobe rilocato tooanother nodo cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d841b-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="d841b-128">Hello alle regole che riguardano le interfacce tooactor è utile citare:</span><span class="sxs-lookup"><span data-stu-id="d841b-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="d841b-129">I metodi di interfaccia dell'attore non possono essere sottoposti a overload.</span><span class="sxs-lookup"><span data-stu-id="d841b-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="d841b-130">I metodi di interfaccia dell'attore non accettano parametri facoltativi, out o ref.</span><span class="sxs-lookup"><span data-stu-id="d841b-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="d841b-131">Non sono supportate interfacce generiche.</span><span class="sxs-lookup"><span data-stu-id="d841b-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="d841b-132">Creare un servizio Actor</span><span class="sxs-lookup"><span data-stu-id="d841b-132">Create an actor service</span></span>
<span data-ttu-id="d841b-133">Per iniziare, creare una nuova applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d841b-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="d841b-134">Hello Service Fabric SDK per Linux include un Yeoman lo scaffolding di hello tooprovide generatore di un'applicazione di Service Fabric con un servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="d841b-134">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="d841b-135">Avviare eseguendo hello seguenti Yeoman comando:</span><span class="sxs-lookup"><span data-stu-id="d841b-135">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="d841b-136">Seguire hello istruzioni toocreate un **servizio Actor affidabile**.</span><span class="sxs-lookup"><span data-stu-id="d841b-136">Follow hello instructions toocreate a **Reliable Actor Service**.</span></span> <span data-ttu-id="d841b-137">Per questa esercitazione, denominare hello applicazione "HelloWorldActorApplication" e hello attore "HelloWorldActor".</span><span class="sxs-lookup"><span data-stu-id="d841b-137">For this tutorial, name hello application "HelloWorldActorApplication" and hello actor "HelloWorldActor."</span></span> <span data-ttu-id="d841b-138">verrà creato dopo lo scaffolding Hello:</span><span class="sxs-lookup"><span data-stu-id="d841b-138">hello following scaffolding will be created:</span></span>

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

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="d841b-139">Blocchi predefiniti di base di Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="d841b-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="d841b-140">concetti di base Hello descritti in precedenza si traducono in hello blocchi predefiniti di base di un servizio Reliable Actor.</span><span class="sxs-lookup"><span data-stu-id="d841b-140">hello basic concepts described earlier translate into hello basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="d841b-141">Interfaccia dell'attore</span><span class="sxs-lookup"><span data-stu-id="d841b-141">Actor interface</span></span>
<span data-ttu-id="d841b-142">Contiene la definizione di interfaccia hello per attore hello.</span><span class="sxs-lookup"><span data-stu-id="d841b-142">This contains hello interface definition for hello actor.</span></span> <span data-ttu-id="d841b-143">Questa interfaccia definisce contratto attore hello condiviso da implementazione attore hello e i client hello chiamata attore hello, pertanto è in genere senso toodefine in una posizione separati dall'implementazione attore hello e può essere condiviso da diversi altri servizi o applicazioni client.</span><span class="sxs-lookup"><span data-stu-id="d841b-143">This interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in a place that is separate from hello actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="d841b-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span><span class="sxs-lookup"><span data-stu-id="d841b-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="d841b-145">Servizio Actor</span><span class="sxs-lookup"><span data-stu-id="d841b-145">Actor service</span></span>
<span data-ttu-id="d841b-146">Questo blocco contiene l'implementazione dell'attore e il codice di registrazione dell'attore.</span><span class="sxs-lookup"><span data-stu-id="d841b-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="d841b-147">classe attore Hello implementa interfaccia attore hello.</span><span class="sxs-lookup"><span data-stu-id="d841b-147">hello actor class implements hello actor interface.</span></span> <span data-ttu-id="d841b-148">Questa è la posizione in cui l'attore svolge il suo lavoro.</span><span class="sxs-lookup"><span data-stu-id="d841b-148">This is where your actor does its work.</span></span>

<span data-ttu-id="d841b-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span><span class="sxs-lookup"><span data-stu-id="d841b-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

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

### <a name="actor-registration"></a><span data-ttu-id="d841b-150">Registrazione dell'attore</span><span class="sxs-lookup"><span data-stu-id="d841b-150">Actor registration</span></span>
<span data-ttu-id="d841b-151">servizio actor Hello deve essere registrato con un tipo di servizio nel runtime di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="d841b-151">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="d841b-152">Per consentire hello servizio Actor toorun le istanze di attore, il tipo di attore inoltre deve essere registrato con hello servizio Actor.</span><span class="sxs-lookup"><span data-stu-id="d841b-152">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="d841b-153">Hello `ActorRuntime` metodo di registrazione, questa operazione viene eseguita per attori.</span><span class="sxs-lookup"><span data-stu-id="d841b-153">hello `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="d841b-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span><span class="sxs-lookup"><span data-stu-id="d841b-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

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

### <a name="test-client"></a><span data-ttu-id="d841b-155">Client di prova</span><span class="sxs-lookup"><span data-stu-id="d841b-155">Test client</span></span>
<span data-ttu-id="d841b-156">Si tratta di un'applicazione client di test semplice è possibile eseguire separatamente da tootest applicazione di Service Fabric hello del servizio actor.</span><span class="sxs-lookup"><span data-stu-id="d841b-156">This is a simple test client application you can run separately from hello Service Fabric application tootest your actor service.</span></span> <span data-ttu-id="d841b-157">Questo è un esempio di dove hello ActorProxy può essere tooactivate utilizzato e comunicare con istanze attore.</span><span class="sxs-lookup"><span data-stu-id="d841b-157">This is an example of where hello ActorProxy can be used tooactivate and communicate with actor instances.</span></span> <span data-ttu-id="d841b-158">Non viene distribuito con il servizio.</span><span class="sxs-lookup"><span data-stu-id="d841b-158">It does not get deployed with your service.</span></span>

### <a name="hello-application"></a><span data-ttu-id="d841b-159">applicazione Hello</span><span class="sxs-lookup"><span data-stu-id="d841b-159">hello application</span></span>
<span data-ttu-id="d841b-160">Infine, i pacchetti di applicazione hello hello servizio actor e altri servizi che è possibile aggiungere in hello futura insieme per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d841b-160">Finally, hello application packages hello actor service and any other services you might add in hello future together for deployment.</span></span> <span data-ttu-id="d841b-161">Contiene hello *ApplicationManifest.xml* e segnaposto per il pacchetto di servizio actor hello.</span><span class="sxs-lookup"><span data-stu-id="d841b-161">It contains hello *ApplicationManifest.xml* and place holders for hello actor service package.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="d841b-162">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="d841b-162">Run hello application</span></span>

<span data-ttu-id="d841b-163">Hello Yeoman scaffolding include un gradle script toobuild hello applicazione e bash script toodeploy e rimuovere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d841b-163">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="d841b-164">applicazione hello toodeploy, prima dell'applicazione hello compilazione con gradle:</span><span class="sxs-lookup"><span data-stu-id="d841b-164">toodeploy hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="d841b-165">Si otterrà un pacchetto dell'applicazione di Service Fabric che può essere distribuito tramite gli strumenti dell'interfaccia della riga di comando di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d841b-165">This will produce a Service Fabric application package that can be deployed using Service Fabric CLI tools.</span></span>

### <a name="deploy-service-fabric-cli"></a><span data-ttu-id="d841b-166">Distribuire l'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d841b-166">Deploy Service Fabric CLI</span></span>

<span data-ttu-id="d841b-167">script install.sh Hello contiene hello necessarie servizio infrastruttura CLI (sfctl) comandi toodeploy hello pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d841b-167">hello install.sh script contains hello necessary Service Fabric CLI (sfctl) commands toodeploy hello application package.</span></span>
<span data-ttu-id="d841b-168">Eseguire un'applicazione hello hello install.sh script toodeploy.</span><span class="sxs-lookup"><span data-stu-id="d841b-168">Run hello install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="d841b-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d841b-169">Next steps</span></span>

* [<span data-ttu-id="d841b-170">Introduzione all'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d841b-170">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
