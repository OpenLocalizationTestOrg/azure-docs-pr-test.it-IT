---
title: aaaCreate del microservizio Azure affidabile prima in Java | Documenti Microsoft
description: Introduzione toocreating un'applicazione di Microsoft Azure Service Fabric con servizi senza stato.
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="92b27-103">Introduzione a Reliable Services</span><span class="sxs-lookup"><span data-stu-id="92b27-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="92b27-104">C# su Windows</span><span class="sxs-lookup"><span data-stu-id="92b27-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="92b27-105">Java su Linux</span><span class="sxs-lookup"><span data-stu-id="92b27-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="92b27-106">In questo articolo vengono illustrati concetti fondamentali di hello di servizi di Azure Service Fabric affidabile e viene illustrato come creare e distribuire una semplice applicazione di servizio affidabile scritta in Java.</span><span class="sxs-lookup"><span data-stu-id="92b27-106">This article explains hello basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="92b27-107">In questo video Microsoft Virtual Academy illustra anche come un servizio Reliable senza stato toocreate:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="92b27-107">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="92b27-108">Installazione e configurazione</span><span class="sxs-lookup"><span data-stu-id="92b27-108">Installation and setup</span></span>
<span data-ttu-id="92b27-109">Prima di iniziare, verificare di che aver ambiente di sviluppo di Service Fabric hello configurare nel computer.</span><span class="sxs-lookup"><span data-stu-id="92b27-109">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="92b27-110">Se è necessario tooset, configurarlo, andare troppo[introduzione su Mac](service-fabric-get-started-mac.md) o [introduzione in Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="92b27-110">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="92b27-111">Concetti di base</span><span class="sxs-lookup"><span data-stu-id="92b27-111">Basic concepts</span></span>
<span data-ttu-id="92b27-112">tooget avviato con servizi affidabili, è solo necessario toounderstand alcuni concetti di base:</span><span class="sxs-lookup"><span data-stu-id="92b27-112">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="92b27-113">**Tipo di servizio**: si tratta dell'implementazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="92b27-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="92b27-114">È definito dalla classe hello è scrivere che estende `StatelessService` e qualsiasi altro codice o dipendenze al suo interno, utilizzate insieme a un nome e un numero di versione.</span><span class="sxs-lookup"><span data-stu-id="92b27-114">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="92b27-115">**Istanza di servizio denominata**: toorun il servizio, si creano le istanze denominate del tipo di servizio, molto come si creano istanze di un oggetto di un tipo classe.</span><span class="sxs-lookup"><span data-stu-id="92b27-115">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="92b27-116">Le istanze del servizio sono, di fatto, istanze di oggetto della classe del servizio che si scrive.</span><span class="sxs-lookup"><span data-stu-id="92b27-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="92b27-117">**Host del servizio**: hello denominata è necessario toorun all'interno di un host di creare istanze del servizio.</span><span class="sxs-lookup"><span data-stu-id="92b27-117">**Service host**: hello named service instances you create need toorun inside a host.</span></span> <span data-ttu-id="92b27-118">host del servizio Hello è semplicemente un processo in cui è possono eseguire le istanze del servizio.</span><span class="sxs-lookup"><span data-stu-id="92b27-118">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="92b27-119">**Registrazione del servizio**: la registrazione raccoglie tutti gli elementi.</span><span class="sxs-lookup"><span data-stu-id="92b27-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="92b27-120">Hello tipo di servizio deve essere registrato con hello Service Fabric runtime in un servizio host tooallow Service Fabric toocreate istanze toorun.</span><span class="sxs-lookup"><span data-stu-id="92b27-120">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="92b27-121">Creare un servizio senza stato</span><span class="sxs-lookup"><span data-stu-id="92b27-121">Create a stateless service</span></span>
<span data-ttu-id="92b27-122">Iniziare a creare un'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="92b27-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="92b27-123">Hello Service Fabric SDK per Linux include un Yeoman lo scaffolding di hello tooprovide generatore di un'applicazione di Service Fabric con un servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="92b27-123">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="92b27-124">Avviare eseguendo hello seguenti Yeoman comando:</span><span class="sxs-lookup"><span data-stu-id="92b27-124">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="92b27-125">Seguire hello istruzioni toocreate un **affidabile di servizio senza stato**.</span><span class="sxs-lookup"><span data-stu-id="92b27-125">Follow hello instructions toocreate a **Reliable Stateless Service**.</span></span> <span data-ttu-id="92b27-126">Per questa esercitazione, hello e un'applicazione hello nome "HelloWorldApplication" servizio "HelloWorld".</span><span class="sxs-lookup"><span data-stu-id="92b27-126">For this tutorial, name hello application "HelloWorldApplication" and hello service "HelloWorld".</span></span> <span data-ttu-id="92b27-127">il risultato di Hello include directory per hello `HelloWorldApplication` e `HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="92b27-127">hello result includes directories for hello `HelloWorldApplication` and `HelloWorld`.</span></span>

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a><span data-ttu-id="92b27-128">Implementare il servizio hello</span><span class="sxs-lookup"><span data-stu-id="92b27-128">Implement hello service</span></span>
<span data-ttu-id="92b27-129">Aprire **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span><span class="sxs-lookup"><span data-stu-id="92b27-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="92b27-130">Questa classe definisce il tipo di servizio hello e può eseguire qualsiasi codice.</span><span class="sxs-lookup"><span data-stu-id="92b27-130">This class defines hello service type, and can run any code.</span></span> <span data-ttu-id="92b27-131">API del servizio Hello fornisce due punti di ingresso per il codice:</span><span class="sxs-lookup"><span data-stu-id="92b27-131">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="92b27-132">Un metodo del punto di ingresso aperto denominato `runAsync()`, che consente di iniziare a eseguire qualsiasi carico di lavoro, inclusi carichi di lavoro di calcolo con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="92b27-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="92b27-133">Un punto di ingresso di comunicazione a cui è possibile collegare lo stack di comunicazione desiderato.</span><span class="sxs-lookup"><span data-stu-id="92b27-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="92b27-134">In questo punto è possibile iniziare a ricevere richieste da utenti e da altri servizi.</span><span class="sxs-lookup"><span data-stu-id="92b27-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="92b27-135">In questa esercitazione è incentrata su hello `runAsync()` metodo punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="92b27-135">In this tutorial, we focus on hello `runAsync()` entry point method.</span></span> <span data-ttu-id="92b27-136">In questo punto è possibile iniziare immediatamente a eseguire il codice.</span><span class="sxs-lookup"><span data-stu-id="92b27-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="92b27-137">RunAsync</span><span class="sxs-lookup"><span data-stu-id="92b27-137">RunAsync</span></span>
<span data-ttu-id="92b27-138">piattaforma Hello chiama questo metodo quando un'istanza di un servizio è tooexecute posizionato ed è pronto.</span><span class="sxs-lookup"><span data-stu-id="92b27-138">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="92b27-139">Per un servizio senza stato, che indica semplicemente quando viene aperto l'istanza del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="92b27-139">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="92b27-140">Un token di annullamento viene fornito toocoordinate quando l'istanza del servizio deve toobe chiuso.</span><span class="sxs-lookup"><span data-stu-id="92b27-140">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="92b27-141">In Service Fabric, questo ciclo di apertura o chiusura di un'istanza del servizio può verificarsi più volte nel ciclo di vita di hello del servizio hello nel suo complesso.</span><span class="sxs-lookup"><span data-stu-id="92b27-141">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="92b27-142">Questa situazione può verificarsi per vari motivi, tra cui:</span><span class="sxs-lookup"><span data-stu-id="92b27-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="92b27-143">sistema di Hello sposta le istanze del servizio di bilanciamento delle risorse.</span><span class="sxs-lookup"><span data-stu-id="92b27-143">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="92b27-144">Si verificano errori nel codice.</span><span class="sxs-lookup"><span data-stu-id="92b27-144">Faults occur in your code.</span></span>
* <span data-ttu-id="92b27-145">un'applicazione Hello o sistema viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="92b27-145">hello application or system is upgraded.</span></span>
* <span data-ttu-id="92b27-146">hardware sottostante Hello di cui si verifichi un'interruzione del servizio.</span><span class="sxs-lookup"><span data-stu-id="92b27-146">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="92b27-147">Questa orchestrazione è gestita da Service Fabric tookeep il servizio a disponibilità elevata e bilanciato in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="92b27-147">This orchestration is managed by Service Fabric tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="92b27-148">`runAsync()` non deve bloccarsi in modo sincrono.</span><span class="sxs-lookup"><span data-stu-id="92b27-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="92b27-149">L'implementazione di runAsync deve restituire un runtime toocontinue di CompletableFuture tooallow hello.</span><span class="sxs-lookup"><span data-stu-id="92b27-149">Your implementation of runAsync should return a CompletableFuture tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="92b27-150">Se il carico di lavoro deve tooimplement un'attività a esecuzione prolungata che deve essere eseguita all'interno di hello CompletableFuture.</span><span class="sxs-lookup"><span data-stu-id="92b27-150">If your workload needs tooimplement a long running task that should be done inside hello CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="92b27-151">Annullamento</span><span class="sxs-lookup"><span data-stu-id="92b27-151">Cancellation</span></span>
<span data-ttu-id="92b27-152">Annullamento del carico di lavoro è un lavoro cooperativo orchestrato da hello fornito token di annullamento.</span><span class="sxs-lookup"><span data-stu-id="92b27-152">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="92b27-153">sistema Hello attende l'attività tooend (per il completamento, annullamento o errore) prima di spostare.</span><span class="sxs-lookup"><span data-stu-id="92b27-153">hello system waits for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="92b27-154">È importante toohonor hello annullamento token, termina qualsiasi lavoro e chiudere `runAsync()` più rapidamente possibile quando il sistema hello richiede l'annullamento.</span><span class="sxs-lookup"><span data-stu-id="92b27-154">It is important toohonor hello cancellation token, finish any work, and exit `runAsync()` as quickly as possible when hello system requests cancellation.</span></span> <span data-ttu-id="92b27-155">Hello esempio seguente viene illustrato come un evento di annullamento toohandle:</span><span class="sxs-lookup"><span data-stu-id="92b27-155">hello following example demonstrates how toohandle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a><span data-ttu-id="92b27-156">Registrazione del servizio</span><span class="sxs-lookup"><span data-stu-id="92b27-156">Service registration</span></span>
<span data-ttu-id="92b27-157">Tipi di servizio devono essere registrati con il runtime di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="92b27-157">Service types must be registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="92b27-158">tipo di servizio Hello è definito in hello `ServiceManifest.xml` e la classe di servizio che implementa `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="92b27-158">hello service type is defined in hello `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="92b27-159">La registrazione del servizio viene eseguita nel punto di ingresso principale processo hello.</span><span class="sxs-lookup"><span data-stu-id="92b27-159">Service registration is performed in hello process main entry point.</span></span> <span data-ttu-id="92b27-160">In questo esempio hello processo il punto di ingresso principale è `HelloWorldServiceHost.java`:</span><span class="sxs-lookup"><span data-stu-id="92b27-160">In this example, hello process main entry point is `HelloWorldServiceHost.java`:</span></span>

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a><span data-ttu-id="92b27-161">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="92b27-161">Run hello application</span></span>

<span data-ttu-id="92b27-162">Hello Yeoman scaffolding include un gradle script toobuild hello applicazione e bash script toodeploy e rimuovere l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="92b27-162">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="92b27-163">applicazione hello toorun, prima dell'applicazione hello compilazione con gradle:</span><span class="sxs-lookup"><span data-stu-id="92b27-163">toorun hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="92b27-164">Questa operazione genera un pacchetto dell'applicazione Service Fabric che può essere distribuito tramite l'interfaccia della riga di comando di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="92b27-164">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

### <a name="deploy-with-service-fabric-cli"></a><span data-ttu-id="92b27-165">Distribuire con l'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="92b27-165">Deploy with Service Fabric CLI</span></span>

<span data-ttu-id="92b27-166">script install.sh Hello contiene hello necessarie servizio infrastruttura CLI comandi toodeploy hello pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="92b27-166">hello install.sh script contains hello necessary Service Fabric CLI commands toodeploy hello application package.</span></span> <span data-ttu-id="92b27-167">Eseguire l'applicazione di hello install.sh toodeploy script.</span><span class="sxs-lookup"><span data-stu-id="92b27-167">Run the install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="92b27-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="92b27-168">Next steps</span></span>

* [<span data-ttu-id="92b27-169">Introduzione all'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="92b27-169">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
