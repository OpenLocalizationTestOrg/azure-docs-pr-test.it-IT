---
title: Creare il primo microservizio di Azure affidabile in Java | Documentazione Microsoft
description: "Introduzione alla creazione di un’applicazione dell’infrastruttura di servizi di Microsoft Azure con i servizi con e senza stato."
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
ms.openlocfilehash: 1ebabe4844732412e04bab8c277f7ebbc4a5737c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="a58b9-103">Introduzione a Reliable Services</span><span class="sxs-lookup"><span data-stu-id="a58b9-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a58b9-104">C# su Windows</span><span class="sxs-lookup"><span data-stu-id="a58b9-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="a58b9-105">Java su Linux</span><span class="sxs-lookup"><span data-stu-id="a58b9-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="a58b9-106">Questo articolo illustra le nozioni fondamentali di Reliable Services di Azure Service Fabric e le procedure per creare e distribuire una semplice applicazione Reliable Services scritta in Java.</span><span class="sxs-lookup"><span data-stu-id="a58b9-106">This article explains the basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="a58b9-107">Questo video di Microsoft Virtual Academy illustra anche come creare un servizio Reliable Services senza stato: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="a58b9-107">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="a58b9-108">Installazione e configurazione</span><span class="sxs-lookup"><span data-stu-id="a58b9-108">Installation and setup</span></span>
<span data-ttu-id="a58b9-109">Prima di iniziare, assicurarsi che nel computer sia configurato l'ambiente di sviluppo di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a58b9-109">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="a58b9-110">Se è necessario configurarlo, andare alla [guida introduttiva per Mac](service-fabric-get-started-mac.md) o alla [guida introduttiva per Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a58b9-110">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="a58b9-111">Concetti di base</span><span class="sxs-lookup"><span data-stu-id="a58b9-111">Basic concepts</span></span>
<span data-ttu-id="a58b9-112">Per iniziare a usare Reliable Services, è sufficiente comprendere solo alcuni concetti di base:</span><span class="sxs-lookup"><span data-stu-id="a58b9-112">To get started with Reliable Services, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="a58b9-113">**Tipo di servizio**: si tratta dell'implementazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="a58b9-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="a58b9-114">Viene definito dalla classe scritta che estende `StatelessService` e qualsiasi altro codice o dipendenze usate, insieme al nome e al numero della versione.</span><span class="sxs-lookup"><span data-stu-id="a58b9-114">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="a58b9-115">**Istanza di servizio denominata**: per eseguire il servizio, si creano le istanze denominate del tipo di servizio, analogamente al modo in cui si creano le istanze di un oggetto di un tipo di classe.</span><span class="sxs-lookup"><span data-stu-id="a58b9-115">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="a58b9-116">Le istanze del servizio sono, di fatto, istanze di oggetto della classe del servizio che si scrive.</span><span class="sxs-lookup"><span data-stu-id="a58b9-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="a58b9-117">**Host del servizio**: le istanze del servizio denominate che si creano devono essere eseguite all'interno di un host.</span><span class="sxs-lookup"><span data-stu-id="a58b9-117">**Service host**: The named service instances you create need to run inside a host.</span></span> <span data-ttu-id="a58b9-118">L'host del servizio è semplicemente un processo in cui eseguire le istanze del servizio.</span><span class="sxs-lookup"><span data-stu-id="a58b9-118">The service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="a58b9-119">**Registrazione del servizio**: la registrazione raccoglie tutti gli elementi.</span><span class="sxs-lookup"><span data-stu-id="a58b9-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="a58b9-120">Il tipo di servizio deve essere registrato con il runtime di Service Fabric in un host del servizio per consentire a Service Fabric di creare istanze per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a58b9-120">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="a58b9-121">Creare un servizio senza stato</span><span class="sxs-lookup"><span data-stu-id="a58b9-121">Create a stateless service</span></span>
<span data-ttu-id="a58b9-122">Iniziare a creare un'applicazione di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a58b9-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="a58b9-123">Service Fabric SDK per Linux include un generatore Yeoman per la creazione dello scaffolding per un'applicazione di Service Fabric con un servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="a58b9-123">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="a58b9-124">Iniziare eseguendo il comando Yeoman seguente:</span><span class="sxs-lookup"><span data-stu-id="a58b9-124">Start by running the following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="a58b9-125">Seguire le istruzioni per creare un **servizio di Reliable Service senza stato**.</span><span class="sxs-lookup"><span data-stu-id="a58b9-125">Follow the instructions to create a **Reliable Stateless Service**.</span></span> <span data-ttu-id="a58b9-126">Per questa esercitazione, denominare l'applicazione "HelloWorldApplication" e il servizio "HelloWorld".</span><span class="sxs-lookup"><span data-stu-id="a58b9-126">For this tutorial, name the application "HelloWorldApplication" and the service "HelloWorld".</span></span> <span data-ttu-id="a58b9-127">Il risultato include le directory per `HelloWorldApplication` e `HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="a58b9-127">The result includes directories for the `HelloWorldApplication` and `HelloWorld`.</span></span>

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

## <a name="implement-the-service"></a><span data-ttu-id="a58b9-128">Implementare il servizio</span><span class="sxs-lookup"><span data-stu-id="a58b9-128">Implement the service</span></span>
<span data-ttu-id="a58b9-129">Aprire **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span><span class="sxs-lookup"><span data-stu-id="a58b9-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="a58b9-130">Questa classe definisce il tipo di servizio e può eseguire qualsiasi codice.</span><span class="sxs-lookup"><span data-stu-id="a58b9-130">This class defines the service type, and can run any code.</span></span> <span data-ttu-id="a58b9-131">L'API del servizio fornisce due punti di ingresso per il codice:</span><span class="sxs-lookup"><span data-stu-id="a58b9-131">The service API provides two entry points for your code:</span></span>

* <span data-ttu-id="a58b9-132">Un metodo del punto di ingresso aperto denominato `runAsync()`, che consente di iniziare a eseguire qualsiasi carico di lavoro, inclusi carichi di lavoro di calcolo con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="a58b9-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="a58b9-133">Un punto di ingresso di comunicazione a cui è possibile collegare lo stack di comunicazione desiderato.</span><span class="sxs-lookup"><span data-stu-id="a58b9-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="a58b9-134">In questo punto è possibile iniziare a ricevere richieste da utenti e da altri servizi.</span><span class="sxs-lookup"><span data-stu-id="a58b9-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="a58b9-135">Questa esercitazione si concentra sul metodo `runAsync()` del punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="a58b9-135">In this tutorial, we focus on the `runAsync()` entry point method.</span></span> <span data-ttu-id="a58b9-136">In questo punto è possibile iniziare immediatamente a eseguire il codice.</span><span class="sxs-lookup"><span data-stu-id="a58b9-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="a58b9-137">RunAsync</span><span class="sxs-lookup"><span data-stu-id="a58b9-137">RunAsync</span></span>
<span data-ttu-id="a58b9-138">La piattaforma chiama questo metodo quando si inserisce un'istanza di un servizio pronta per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a58b9-138">The platform calls this method when an instance of a service is placed and ready to execute.</span></span> <span data-ttu-id="a58b9-139">Per un servizio senza stato, la piattaforma chiama il metodo quando l'istanza del servizio viene aperta.</span><span class="sxs-lookup"><span data-stu-id="a58b9-139">For a stateless service, that simply means when the service instance is opened.</span></span> <span data-ttu-id="a58b9-140">Viene fornito un token di annullamento che determina quando è necessario chiudere l'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="a58b9-140">A cancellation token is provided to coordinate when your service instance needs to be closed.</span></span> <span data-ttu-id="a58b9-141">In Service Fabric questo ciclo di apertura e chiusura di un'istanza del servizio può verificarsi più volte per tutta la durata del servizio nel suo complesso.</span><span class="sxs-lookup"><span data-stu-id="a58b9-141">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span></span> <span data-ttu-id="a58b9-142">Questa situazione può verificarsi per vari motivi, tra cui:</span><span class="sxs-lookup"><span data-stu-id="a58b9-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="a58b9-143">Il sistema sposta le istanze del servizio per il bilanciamento delle risorse.</span><span class="sxs-lookup"><span data-stu-id="a58b9-143">The system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="a58b9-144">Si verificano errori nel codice.</span><span class="sxs-lookup"><span data-stu-id="a58b9-144">Faults occur in your code.</span></span>
* <span data-ttu-id="a58b9-145">Viene aggiornato il sistema o l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a58b9-145">The application or system is upgraded.</span></span>
* <span data-ttu-id="a58b9-146">Si verifica un'interruzione nell'hardware sottostante.</span><span class="sxs-lookup"><span data-stu-id="a58b9-146">The underlying hardware experiences an outage.</span></span>

<span data-ttu-id="a58b9-147">Questa orchestrazione viene gestita da Service Fabric per assicurare l'elevata disponibilità e il corretto bilanciamento del servizio.</span><span class="sxs-lookup"><span data-stu-id="a58b9-147">This orchestration is managed by Service Fabric to keep your service highly available and properly balanced.</span></span>

<span data-ttu-id="a58b9-148">`runAsync()` non deve bloccarsi in modo sincrono.</span><span class="sxs-lookup"><span data-stu-id="a58b9-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="a58b9-149">L'implementazione di runAsync deve restituire un valore CompletableFuture per consentire al runtime di procedere.</span><span class="sxs-lookup"><span data-stu-id="a58b9-149">Your implementation of runAsync should return a CompletableFuture to allow the runtime to continue.</span></span> <span data-ttu-id="a58b9-150">Se il carico di lavoro deve implementare un'attività a esecuzione prolungata, tale operazione deve essere completata entro il valore specificato da CompletableFuture.</span><span class="sxs-lookup"><span data-stu-id="a58b9-150">If your workload needs to implement a long running task that should be done inside the CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="a58b9-151">Annullamento</span><span class="sxs-lookup"><span data-stu-id="a58b9-151">Cancellation</span></span>
<span data-ttu-id="a58b9-152">L'annullamento del carico di lavoro è un'operazione cooperativa coordinata dal token di annullamento fornito.</span><span class="sxs-lookup"><span data-stu-id="a58b9-152">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span></span> <span data-ttu-id="a58b9-153">Il sistema attende la fine dell'attività (per esito positivo, annullamento o errore) prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="a58b9-153">The system waits for your task to end (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="a58b9-154">È importante rispettare il token di annullamento, completare le operazioni e chiudere `runAsync()` il più rapidamente possibile quando viene richiesto l'annullamento dal sistema.</span><span class="sxs-lookup"><span data-stu-id="a58b9-154">It is important to honor the cancellation token, finish any work, and exit `runAsync()` as quickly as possible when the system requests cancellation.</span></span> <span data-ttu-id="a58b9-155">L'esempio seguente mostra come gestire un evento di annullamento:</span><span class="sxs-lookup"><span data-stu-id="a58b9-155">The following example demonstrates how to handle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace the following sample code with your own logic
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

### <a name="service-registration"></a><span data-ttu-id="a58b9-156">Registrazione del servizio</span><span class="sxs-lookup"><span data-stu-id="a58b9-156">Service registration</span></span>
<span data-ttu-id="a58b9-157">I tipi del servizio devono essere registrati nel runtime di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a58b9-157">Service types must be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="a58b9-158">Il tipo di servizio è definito nel `ServiceManifest.xml` e nella classe di servizio che implementa `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="a58b9-158">The service type is defined in the `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="a58b9-159">La registrazione del servizio viene eseguita nel punto di ingresso principale del processo.</span><span class="sxs-lookup"><span data-stu-id="a58b9-159">Service registration is performed in the process main entry point.</span></span> <span data-ttu-id="a58b9-160">In questo esempio il punto di ingresso principale del processo è `HelloWorldServiceHost.java`:</span><span class="sxs-lookup"><span data-stu-id="a58b9-160">In this example, the process main entry point is `HelloWorldServiceHost.java`:</span></span>

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

## <a name="run-the-application"></a><span data-ttu-id="a58b9-161">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="a58b9-161">Run the application</span></span>

<span data-ttu-id="a58b9-162">Lo scaffolding Yeoman include uno script Gradle per compilare l'applicazione e script Bash per distribuire ed eliminare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a58b9-162">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and remove the application.</span></span> <span data-ttu-id="a58b9-163">Per eseguire l'applicazione, prima di tutto compilarla con Gradle:</span><span class="sxs-lookup"><span data-stu-id="a58b9-163">To run the application, first build the application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="a58b9-164">Questa operazione genera un pacchetto dell'applicazione Service Fabric che può essere distribuito tramite l'interfaccia della riga di comando di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a58b9-164">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

### <a name="deploy-with-service-fabric-cli"></a><span data-ttu-id="a58b9-165">Distribuire con l'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a58b9-165">Deploy with Service Fabric CLI</span></span>

<span data-ttu-id="a58b9-166">Lo script install.sh contiene i comandi dell'interfaccia della riga di comando di Service Fabric necessari per distribuire il pacchetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a58b9-166">The install.sh script contains the necessary Service Fabric CLI commands to deploy the application package.</span></span> <span data-ttu-id="a58b9-167">Eseguire lo script install.sh per distribuire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a58b9-167">Run the install.sh script to deploy the application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="a58b9-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a58b9-168">Next steps</span></span>

* [<span data-ttu-id="a58b9-169">Introduzione all'interfaccia della riga di comando di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a58b9-169">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
