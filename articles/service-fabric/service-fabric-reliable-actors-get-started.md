---
title: aaaCreate il primo microservizio Azure basato su attori in c# | Documenti Microsoft
description: In questa esercitazione vengono illustrati i passaggi hello di creazione, il debug e distribuzione di un servizio basato su attori semplice usando Service Fabric Reliable Actors.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="cd744-103">Introduzione a Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="cd744-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cd744-104">C# su Windows</span><span class="sxs-lookup"><span data-stu-id="cd744-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="cd744-105">Java su Linux</span><span class="sxs-lookup"><span data-stu-id="cd744-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="cd744-106">In questo articolo vengono illustrati concetti fondamentali di hello di Azure Service Fabric Reliable Actors e viene illustrata la creazione, il debug e distribuzione di un'applicazione semplice Reliable Actor in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cd744-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="cd744-107">Installazione e configurazione</span><span class="sxs-lookup"><span data-stu-id="cd744-107">Installation and setup</span></span>
<span data-ttu-id="cd744-108">Prima di iniziare, assicurarsi di disporre dell'ambiente di sviluppo di Service Fabric hello configurare nel computer.</span><span class="sxs-lookup"><span data-stu-id="cd744-108">Before you start, ensure that you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="cd744-109">Se è necessario tooset, configurarlo, vedere le istruzioni dettagliate sulla [come tooset hello ambiente di sviluppo](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cd744-109">If you need tooset it up, see detailed instructions on [how tooset up hello development environment](service-fabric-get-started.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="cd744-110">Concetti di base</span><span class="sxs-lookup"><span data-stu-id="cd744-110">Basic concepts</span></span>
<span data-ttu-id="cd744-111">tooget introduttiva Reliable Actors, è solo necessario toounderstand alcuni concetti di base:</span><span class="sxs-lookup"><span data-stu-id="cd744-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="cd744-112">**Servizio attore**.</span><span class="sxs-lookup"><span data-stu-id="cd744-112">**Actor service**.</span></span> <span data-ttu-id="cd744-113">Reliable Actors sono inclusi nei servizi affidabili che può essere distribuito nell'infrastruttura di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="cd744-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="cd744-114">Le istanze di Actors vengono attivate in un'istanza del servizio denominata.</span><span class="sxs-lookup"><span data-stu-id="cd744-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="cd744-115">**Registrazione attore**.</span><span class="sxs-lookup"><span data-stu-id="cd744-115">**Actor registration**.</span></span> <span data-ttu-id="cd744-116">Come con i servizi affidabili, un servizio Reliable Actor deve toobe registrato con il runtime di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="cd744-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="cd744-117">Inoltre, è necessario toobe registrato con il runtime di attore hello tipo attore hello.</span><span class="sxs-lookup"><span data-stu-id="cd744-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="cd744-118">**Interfaccia attore**.</span><span class="sxs-lookup"><span data-stu-id="cd744-118">**Actor interface**.</span></span> <span data-ttu-id="cd744-119">interfaccia attore Hello è toodefine utilizzata un'interfaccia pubblica fortemente tipizzata di un attore.</span><span class="sxs-lookup"><span data-stu-id="cd744-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="cd744-120">Nella terminologia dei modelli Reliable Actor hello, interfaccia attore hello definisce hello tipi di messaggi hello attore possono comprendere ed elaborare.</span><span class="sxs-lookup"><span data-stu-id="cd744-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="cd744-121">interfaccia attore Hello viene utilizzato da altri attori e le applicazioni client troppo "inviano" (in modo asincrono) attore toohello messaggi.</span><span class="sxs-lookup"><span data-stu-id="cd744-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="cd744-122">Reliable Actors può implementare più interfacce.</span><span class="sxs-lookup"><span data-stu-id="cd744-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="cd744-123">**Classe ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="cd744-123">**ActorProxy class**.</span></span> <span data-ttu-id="cd744-124">classe ActorProxy Hello viene utilizzato da client applicazioni tooinvoke hello metodi esposti tramite l'interfaccia di hello attore.</span><span class="sxs-lookup"><span data-stu-id="cd744-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="cd744-125">classe ActorProxy Hello offre due funzionalità importanti:</span><span class="sxs-lookup"><span data-stu-id="cd744-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="cd744-126">Risoluzione dei nomi: è in grado di toolocate attore di hello cluster hello (Trova hello nodo del cluster di hello in cui è ospitato).</span><span class="sxs-lookup"><span data-stu-id="cd744-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="cd744-127">Gestione degli errori: può ripetere chiamate al metodo e risolvere nuovamente il percorso di attore hello dopo, ad esempio, un errore che richiede hello attore toobe rilocato tooanother nodo cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cd744-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="cd744-128">Hello alle regole che riguardano le interfacce tooactor è utile citare:</span><span class="sxs-lookup"><span data-stu-id="cd744-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="cd744-129">I metodi di interfaccia dell'attore non possono essere sottoposti a overload.</span><span class="sxs-lookup"><span data-stu-id="cd744-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="cd744-130">I metodi di interfaccia dell'attore non accettano parametri facoltativi, out o ref.</span><span class="sxs-lookup"><span data-stu-id="cd744-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="cd744-131">Non sono supportate interfacce generiche.</span><span class="sxs-lookup"><span data-stu-id="cd744-131">Generic interfaces are not supported.</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="cd744-132">Creare un nuovo progetto in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cd744-132">Create a new project in Visual Studio</span></span>
<span data-ttu-id="cd744-133">Avviare Visual Studio 2015 o Visual Studio 2017 come amministratore e creare un nuovo progetto di applicazione di Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="cd744-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span></span>

![Strumenti di Service Fabric per Visual Studio - nuovo progetto][1]

<span data-ttu-id="cd744-135">In hello successiva finestra di dialogo, è possibile scegliere il tipo di hello del progetto che si desidera toocreate.</span><span class="sxs-lookup"><span data-stu-id="cd744-135">In hello next dialog box, you can choose hello type of project that you want toocreate.</span></span>

![Modelli di progetto di Service Fabric][5]

<span data-ttu-id="cd744-137">Per il progetto HelloWorld hello, utilizziamo servizio Service Fabric Reliable Actors hello.</span><span class="sxs-lookup"><span data-stu-id="cd744-137">For hello HelloWorld project, let's use hello Service Fabric Reliable Actors service.</span></span>

<span data-ttu-id="cd744-138">Dopo aver creato la soluzione hello, dovrebbe essere hello seguente struttura:</span><span class="sxs-lookup"><span data-stu-id="cd744-138">After you have created hello solution, you should see hello following structure:</span></span>

![Struttura del progetto di Service Fabric][2]

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="cd744-140">Blocchi predefiniti di base di Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="cd744-140">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="cd744-141">Una tipica soluzione Reliable Actors è costituita da tre progetti:</span><span class="sxs-lookup"><span data-stu-id="cd744-141">A typical Reliable Actors solution is composed of three projects:</span></span>

* <span data-ttu-id="cd744-142">**progetto di applicazione Hello (MyActorApplication)**.</span><span class="sxs-lookup"><span data-stu-id="cd744-142">**hello application project (MyActorApplication)**.</span></span> <span data-ttu-id="cd744-143">Si tratta di progetto di hello che tutti i servizi di hello insieme per la distribuzione di pacchetti.</span><span class="sxs-lookup"><span data-stu-id="cd744-143">This is hello project that packages all of hello services together for deployment.</span></span> <span data-ttu-id="cd744-144">Contiene hello *ApplicationManifest.xml* e script di PowerShell per la gestione di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="cd744-144">It contains hello *ApplicationManifest.xml* and PowerShell scripts for managing hello application.</span></span>
* <span data-ttu-id="cd744-145">**progetto di interfaccia Hello (MyActor.Interfaces)**.</span><span class="sxs-lookup"><span data-stu-id="cd744-145">**hello interface project (MyActor.Interfaces)**.</span></span> <span data-ttu-id="cd744-146">Si tratta hello progetto che contiene la definizione di interfaccia hello per attore hello.</span><span class="sxs-lookup"><span data-stu-id="cd744-146">This is hello project that contains hello interface definition for hello actor.</span></span> <span data-ttu-id="cd744-147">Nel progetto MyActor.Interfaces hello, è possibile definire le interfacce di hello che verranno utilizzate da attori hello nella soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="cd744-147">In hello MyActor.Interfaces project, you can define hello interfaces that will be used by hello actors in hello solution.</span></span> <span data-ttu-id="cd744-148">Le interfacce attore possono essere definite in qualsiasi progetto con un nome qualsiasi, tuttavia l'interfaccia hello definisce contratto attore hello condiviso da implementazione attore hello e i client hello chiamata attore hello, pertanto è in genere senso toodefine in un assembly separare dall'implementazione attore hello e può essere condiviso da più altri progetti.</span><span class="sxs-lookup"><span data-stu-id="cd744-148">Your actor interfaces can be defined in any project with any name, however hello interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in an assembly that is separate from hello actor implementation and can be shared by multiple other projects.</span></span>

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* <span data-ttu-id="cd744-149">**progetto del servizio actor Hello (MyActor)**.</span><span class="sxs-lookup"><span data-stu-id="cd744-149">**hello actor service project (MyActor)**.</span></span> <span data-ttu-id="cd744-150">Si tratta di hello progetto utilizzato toodefine hello Service Fabric servizio che corso toohost hello attore.</span><span class="sxs-lookup"><span data-stu-id="cd744-150">This is hello project used toodefine hello Service Fabric service that is going toohost hello actor.</span></span> <span data-ttu-id="cd744-151">Contiene l'implementazione hello dell'attore hello.</span><span class="sxs-lookup"><span data-stu-id="cd744-151">It contains hello implementation of hello actor.</span></span> <span data-ttu-id="cd744-152">Un'implementazione attore è una classe che deriva dal tipo di base hello `Actor` e implementa hello interfacce che sono definita nel progetto MyActor.Interfaces hello.</span><span class="sxs-lookup"><span data-stu-id="cd744-152">An actor implementation is a class that derives from hello base type `Actor` and implements hello interface(s) that are defined in hello MyActor.Interfaces project.</span></span> <span data-ttu-id="cd744-153">Una classe attore deve anche implementare un costruttore che accetta un `ActorService` istanza e un `ActorId` e li passa toohello base `Actor` classe.</span><span class="sxs-lookup"><span data-stu-id="cd744-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them toohello base `Actor` class.</span></span> <span data-ttu-id="cd744-154">Ciò consente l'inserimento della dipendenza costruttore delle dipendenze della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="cd744-154">This allows for constructor dependency injection of platform dependencies.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

<span data-ttu-id="cd744-155">servizio actor Hello deve essere registrato con un tipo di servizio nel runtime di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="cd744-155">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="cd744-156">Per consentire hello servizio Actor toorun le istanze di attore, il tipo di attore inoltre deve essere registrato con hello servizio Actor.</span><span class="sxs-lookup"><span data-stu-id="cd744-156">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="cd744-157">Hello `ActorRuntime` metodo di registrazione, questa operazione viene eseguita per attori.</span><span class="sxs-lookup"><span data-stu-id="cd744-157">hello `ActorRuntime` registration method performs this work for actors.</span></span>

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="cd744-158">Se si parte da un nuovo progetto in Visual Studio e si dispone di una sola definizione attore, registrazione hello è incluso per impostazione predefinita nel codice hello generato da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cd744-158">If you start from a new project in Visual Studio and you have only one actor definition, hello registration is included by default in hello code that Visual Studio generates.</span></span> <span data-ttu-id="cd744-159">Se si definiscono altri attori nel servizio di hello, è necessario registrazione attore di hello tooadd utilizzando:</span><span class="sxs-lookup"><span data-stu-id="cd744-159">If you define other actors in hello service, you need tooadd hello actor registration by using:</span></span>

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> <span data-ttu-id="cd744-160">Hello attori di infrastruttura servizio runtime genera alcuni [gli eventi e contatori di prestazioni correlati metodi tooactor](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="cd744-160">hello Service Fabric Actors runtime emits some [events and performance counters related tooactor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span></span> <span data-ttu-id="cd744-161">che sono utili per la diagnostica e il monitoraggio delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="cd744-161">They are useful in diagnostics and performance monitoring.</span></span>
> 
> 

## <a name="debugging"></a><span data-ttu-id="cd744-162">Debug</span><span class="sxs-lookup"><span data-stu-id="cd744-162">Debugging</span></span>
<span data-ttu-id="cd744-163">strumenti di Hello Service Fabric per Visual Studio supportano il debug sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="cd744-163">hello Service Fabric tools for Visual Studio support debugging on your local machine.</span></span> <span data-ttu-id="cd744-164">È possibile avviare una sessione di debug da hello che colpisce tasto F5.</span><span class="sxs-lookup"><span data-stu-id="cd744-164">You can start a debugging session by hitting hello F5 key.</span></span> <span data-ttu-id="cd744-165">Visual Studio esegue, se necessario, la compilazione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="cd744-165">Visual Studio builds (if necessary) packages.</span></span> <span data-ttu-id="cd744-166">Inoltre, consente di distribuire un'applicazione hello nel cluster di Service Fabric locale hello e collega il debugger hello.</span><span class="sxs-lookup"><span data-stu-id="cd744-166">It also deploys hello application on hello local Service Fabric cluster and attaches hello debugger.</span></span>

<span data-ttu-id="cd744-167">Durante il processo di distribuzione di hello, è possibile visualizzare lo stato di avanzamento hello in hello **Output** finestra.</span><span class="sxs-lookup"><span data-stu-id="cd744-167">During hello deployment process, you can see hello progress in hello **Output** window.</span></span>

![Finestra di output del debug di Service Fabric][3]

## <a name="next-steps"></a><span data-ttu-id="cd744-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cd744-169">Next steps</span></span>
<span data-ttu-id="cd744-170">Altre informazioni, vedere [utilizzo di piattaforma Service Fabric hello Reliable Actors](service-fabric-reliable-actors-platform.md).</span><span class="sxs-lookup"><span data-stu-id="cd744-170">Learn more about [how Reliable Actors use hello Service Fabric platform](service-fabric-reliable-actors-platform.md).</span></span>

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
