---
title: aaaCreate la prima applicazione di Service Fabric in c# | Documenti Microsoft
description: Introduzione toocreating un'applicazione di Microsoft Azure Service Fabric con servizi senza stato.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="7588b-103">Introduzione a Reliable Services</span><span class="sxs-lookup"><span data-stu-id="7588b-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7588b-104">C# su Windows</span><span class="sxs-lookup"><span data-stu-id="7588b-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="7588b-105">Java su Linux</span><span class="sxs-lookup"><span data-stu-id="7588b-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
> 
> 

<span data-ttu-id="7588b-106">Un'applicazione di Azure Service Fabric contiene uno o più servizi che consentono l'esecuzione del codice.</span><span class="sxs-lookup"><span data-stu-id="7588b-106">An Azure Service Fabric application contains one or more services that run your code.</span></span> <span data-ttu-id="7588b-107">Questa guida illustra come toocreate state e senza applicazioni di Service Fabric con [servizi affidabili](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7588b-107">This guide shows you how toocreate both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span></span>  <span data-ttu-id="7588b-108">In questo video Microsoft Virtual Academy illustra anche come un servizio Reliable senza stato toocreate:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span><span class="sxs-lookup"><span data-stu-id="7588b-108">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a><span data-ttu-id="7588b-109">Concetti di base</span><span class="sxs-lookup"><span data-stu-id="7588b-109">Basic concepts</span></span>
<span data-ttu-id="7588b-110">tooget avviato con servizi affidabili, è solo necessario toounderstand alcuni concetti di base:</span><span class="sxs-lookup"><span data-stu-id="7588b-110">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="7588b-111">**Tipo di servizio**: si tratta dell'implementazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="7588b-111">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="7588b-112">È definito dalla classe hello è scrivere che estende `StatelessService` e qualsiasi altro codice o dipendenze al suo interno, utilizzate insieme a un nome e un numero di versione.</span><span class="sxs-lookup"><span data-stu-id="7588b-112">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="7588b-113">**Istanza di servizio denominata**: toorun il servizio, si creano le istanze denominate del tipo di servizio, molto come si creano istanze di un oggetto di un tipo classe.</span><span class="sxs-lookup"><span data-stu-id="7588b-113">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="7588b-114">Un'istanza del servizio ha un nome in formato hello di un URI usando hello "fabric: /" dello schema, ad esempio "fabric: / MyApp/MyService".</span><span class="sxs-lookup"><span data-stu-id="7588b-114">A service instance has a name in hello form of a URI using hello "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span></span>
* <span data-ttu-id="7588b-115">**Host del servizio**: hello denominata è necessario toorun all'interno di un processo host di creare istanze del servizio.</span><span class="sxs-lookup"><span data-stu-id="7588b-115">**Service host**: hello named service instances you create need toorun inside a host process.</span></span> <span data-ttu-id="7588b-116">host del servizio Hello è semplicemente un processo in cui è possono eseguire le istanze del servizio.</span><span class="sxs-lookup"><span data-stu-id="7588b-116">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="7588b-117">**Registrazione del servizio**: la registrazione raccoglie tutti gli elementi.</span><span class="sxs-lookup"><span data-stu-id="7588b-117">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="7588b-118">Hello tipo di servizio deve essere registrato con hello Service Fabric runtime in un servizio host tooallow Service Fabric toocreate istanze toorun.</span><span class="sxs-lookup"><span data-stu-id="7588b-118">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="7588b-119">Creare un servizio senza stato</span><span class="sxs-lookup"><span data-stu-id="7588b-119">Create a stateless service</span></span>
<span data-ttu-id="7588b-120">Un servizio senza stato è un tipo di servizio che è attualmente norm hello nelle applicazioni cloud.</span><span class="sxs-lookup"><span data-stu-id="7588b-120">A stateless service is a type of service that is currently hello norm in cloud applications.</span></span> <span data-ttu-id="7588b-121">Viene considerato senza stato servizio hello stesso contiene dati che devono essere toobe archiviati in modo affidabile o reso a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="7588b-121">It is considered stateless because hello service itself does not contain data that needs toobe stored reliably or made highly available.</span></span> <span data-ttu-id="7588b-122">Se un'istanza di un servizio senza stato si arresta, il relativo stato interno viene perso.</span><span class="sxs-lookup"><span data-stu-id="7588b-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span></span> <span data-ttu-id="7588b-123">In questo tipo di servizio, lo stato deve essere archivio esterno tooan persistente, ad esempio le tabelle di Azure o un database SQL, per tale toobe apportate a elevata disponibilità e affidabilità.</span><span class="sxs-lookup"><span data-stu-id="7588b-123">In this type of service, state must be persisted tooan external store, such as Azure Tables or a SQL database, for it toobe made highly available and reliable.</span></span>

<span data-ttu-id="7588b-124">Avviare Visual Studio 2015 o Visual Studio 2017 come amministratore e creare un nuovo progetto di applicazione di Service Fabric denominato *HelloWorld*:</span><span class="sxs-lookup"><span data-stu-id="7588b-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span></span>

![Utilizzare toocreate finestra di dialogo Nuovo progetto hello una nuova applicazione di Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

<span data-ttu-id="7588b-126">Creare quindi un progetto di servizio senza stato denominato *HelloWorldStateless*:</span><span class="sxs-lookup"><span data-stu-id="7588b-126">Then create a stateless service project named *HelloWorldStateless*:</span></span>

![Nella finestra di dialogo hello secondo creare un progetto di servizio senza stato](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

<span data-ttu-id="7588b-128">La soluzione ora contiene due progetti:</span><span class="sxs-lookup"><span data-stu-id="7588b-128">Your solution now contains two projects:</span></span>

* <span data-ttu-id="7588b-129">*HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="7588b-129">*HelloWorld*.</span></span> <span data-ttu-id="7588b-130">Si tratta di hello *applicazione* progetto che contiene il *servizi*.</span><span class="sxs-lookup"><span data-stu-id="7588b-130">This is hello *application* project that contains your *services*.</span></span> <span data-ttu-id="7588b-131">Contiene inoltre il manifesto dell'applicazione hello che descrive l'applicazione hello, nonché un numero di script di PowerShell che consentono di toodeploy l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7588b-131">It also contains hello application manifest that describes hello application, as well as a number of PowerShell scripts that help you toodeploy your application.</span></span>
* <span data-ttu-id="7588b-132">*HelloWorldStateless*.</span><span class="sxs-lookup"><span data-stu-id="7588b-132">*HelloWorldStateless*.</span></span> <span data-ttu-id="7588b-133">Questo è il progetto di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="7588b-133">This is hello service project.</span></span> <span data-ttu-id="7588b-134">Contiene l'implementazione del servizio senza stato hello.</span><span class="sxs-lookup"><span data-stu-id="7588b-134">It contains hello stateless service implementation.</span></span>

## <a name="implement-hello-service"></a><span data-ttu-id="7588b-135">Implementare il servizio hello</span><span class="sxs-lookup"><span data-stu-id="7588b-135">Implement hello service</span></span>
<span data-ttu-id="7588b-136">Aprire hello **HelloWorldStateless.cs** file nel progetto di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="7588b-136">Open hello **HelloWorldStateless.cs** file in hello service project.</span></span> <span data-ttu-id="7588b-137">In Service Fabric un servizio può eseguire qualsiasi tipo di logica di business.</span><span class="sxs-lookup"><span data-stu-id="7588b-137">In Service Fabric, a service can run any business logic.</span></span> <span data-ttu-id="7588b-138">API del servizio Hello fornisce due punti di ingresso per il codice:</span><span class="sxs-lookup"><span data-stu-id="7588b-138">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="7588b-139">Un metodo del punto di ingresso aperto denominato *RunAsync*, che consente di iniziare a eseguire qualsiasi carico di lavoro, inclusi carichi di lavoro di calcolo con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="7588b-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* <span data-ttu-id="7588b-140">Un punto di ingresso di comunicazione a cui è possibile collegare lo stack di comunicazione desiderato, come ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="7588b-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span></span> <span data-ttu-id="7588b-141">In questo punto è possibile iniziare a ricevere richieste da utenti e da altri servizi.</span><span class="sxs-lookup"><span data-stu-id="7588b-141">This is where you can start receiving requests from users and other services.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

<span data-ttu-id="7588b-142">In questa esercitazione, esamineremo hello `RunAsync()` metodo punto di ingresso.</span><span class="sxs-lookup"><span data-stu-id="7588b-142">In this tutorial, we will focus on hello `RunAsync()` entry point method.</span></span> <span data-ttu-id="7588b-143">In questo punto è possibile iniziare immediatamente a eseguire il codice.</span><span class="sxs-lookup"><span data-stu-id="7588b-143">This is where you can immediately start running your code.</span></span>
<span data-ttu-id="7588b-144">il modello di progetto di Hello include un esempio di implementazione di `RunAsync()` che incrementa il numero di sequenza.</span><span class="sxs-lookup"><span data-stu-id="7588b-144">hello project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span></span>

> [!NOTE]
> <span data-ttu-id="7588b-145">Per informazioni dettagliate su come toowork con una comunicazione stack, vedere [servizi API Web dell'infrastruttura del servizio con self-hosting OWIN](service-fabric-reliable-services-communication-webapi.md)</span><span class="sxs-lookup"><span data-stu-id="7588b-145">For details about how toowork with a communication stack, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md)</span></span>
> 
> 

### <a name="runasync"></a><span data-ttu-id="7588b-146">RunAsync</span><span class="sxs-lookup"><span data-stu-id="7588b-146">RunAsync</span></span>
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

<span data-ttu-id="7588b-147">piattaforma Hello chiama questo metodo quando un'istanza di un servizio è tooexecute posizionato ed è pronto.</span><span class="sxs-lookup"><span data-stu-id="7588b-147">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="7588b-148">Per un servizio senza stato, che indica semplicemente quando viene aperto l'istanza del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="7588b-148">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="7588b-149">Un token di annullamento viene fornito toocoordinate quando l'istanza del servizio deve toobe chiuso.</span><span class="sxs-lookup"><span data-stu-id="7588b-149">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="7588b-150">In Service Fabric, questo ciclo di apertura o chiusura di un'istanza del servizio può verificarsi più volte nel ciclo di vita di hello del servizio hello nel suo complesso.</span><span class="sxs-lookup"><span data-stu-id="7588b-150">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="7588b-151">Questa situazione può verificarsi per vari motivi, tra cui:</span><span class="sxs-lookup"><span data-stu-id="7588b-151">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="7588b-152">sistema di Hello sposta le istanze del servizio di bilanciamento delle risorse.</span><span class="sxs-lookup"><span data-stu-id="7588b-152">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="7588b-153">Si verificano errori nel codice.</span><span class="sxs-lookup"><span data-stu-id="7588b-153">Faults occur in your code.</span></span>
* <span data-ttu-id="7588b-154">un'applicazione Hello o sistema viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="7588b-154">hello application or system is upgraded.</span></span>
* <span data-ttu-id="7588b-155">hardware sottostante Hello di cui si verifichi un'interruzione del servizio.</span><span class="sxs-lookup"><span data-stu-id="7588b-155">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="7588b-156">Questa orchestrazione è gestita da hello sistema tookeep il servizio a disponibilità elevata e bilanciato in modo corretto.</span><span class="sxs-lookup"><span data-stu-id="7588b-156">This orchestration is managed by hello system tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="7588b-157">`RunAsync()` non deve bloccarsi in modo sincrono.</span><span class="sxs-lookup"><span data-stu-id="7588b-157">`RunAsync()` should not block synchronously.</span></span> <span data-ttu-id="7588b-158">L'implementazione di RunAsync deve restituire un'attività o await in qualsiasi runtime toocontinue di operazioni a esecuzione prolungata o blocco tooallow hello.</span><span class="sxs-lookup"><span data-stu-id="7588b-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="7588b-159">Nota in hello `while(true)` ciclo nell'esempio precedente hello, restituzione attività `await Task.Delay()` viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="7588b-159">Note in hello `while(true)` loop in hello previous example, a Task-returning `await Task.Delay()` is used.</span></span> <span data-ttu-id="7588b-160">Se il carico di lavoro si deve bloccare in modo sincrono, è opportuno pianificare una nuova Task con `Task.Run()` nell'implementazione `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="7588b-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span></span>

<span data-ttu-id="7588b-161">Annullamento del carico di lavoro è un lavoro cooperativo orchestrato da hello fornito token di annullamento.</span><span class="sxs-lookup"><span data-stu-id="7588b-161">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="7588b-162">sistema Hello attenderà per l'attività tooend (per il completamento, annullamento o errore) prima di spostare.</span><span class="sxs-lookup"><span data-stu-id="7588b-162">hello system will wait for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="7588b-163">È importante toohonor hello annullamento token, termina qualsiasi lavoro e chiudere `RunAsync()` più rapidamente possibile quando il sistema hello richiede l'annullamento.</span><span class="sxs-lookup"><span data-stu-id="7588b-163">It is important toohonor hello cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when hello system requests cancellation.</span></span>

<span data-ttu-id="7588b-164">In questo esempio di servizio senza stato, il conteggio di hello è archiviato in una variabile locale.</span><span class="sxs-lookup"><span data-stu-id="7588b-164">In this stateless service example, hello count is stored in a local variable.</span></span> <span data-ttu-id="7588b-165">Ma, poiché si tratta di un servizio senza stato, il valore hello archiviato esiste solo per hello corrente del ciclo di vita dell'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="7588b-165">But because this is a stateless service, hello value that's stored exists only for hello current lifecycle of its service instance.</span></span> <span data-ttu-id="7588b-166">Quando il servizio hello viene spostato o viene riavviato, il valore di hello viene perso.</span><span class="sxs-lookup"><span data-stu-id="7588b-166">When hello service moves or restarts, hello value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="7588b-167">Creare un servizio con stato</span><span class="sxs-lookup"><span data-stu-id="7588b-167">Create a stateful service</span></span>
<span data-ttu-id="7588b-168">Service Fabric introduce un nuovo tipo di servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="7588b-168">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="7588b-169">Un servizio con stato consente di mantenere lo stato in modo affidabile all'interno del servizio di hello, posizionato insieme ad codice hello in uso è.</span><span class="sxs-lookup"><span data-stu-id="7588b-169">A stateful service can maintain state reliably within hello service itself, co-located with hello code that's using it.</span></span> <span data-ttu-id="7588b-170">Lo stato è a disponibilità elevata grazie Service Fabric senza hello necessità toopersist tooan esterna l'archivio dello stato.</span><span class="sxs-lookup"><span data-stu-id="7588b-170">State is made highly available by Service Fabric without hello need toopersist state tooan external store.</span></span>

<span data-ttu-id="7588b-171">tooconvert un valore del contatore da toohighly senza stato persistente e disponibile, anche quando il servizio hello viene spostato o viene riavviato, è necessario un servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="7588b-171">tooconvert a counter value from stateless toohighly available and persistent, even when hello service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="7588b-172">In hello stesso *HelloWorld* applicazione, è possibile aggiungere un nuovo servizio facendo clic su riferimenti a servizi di hello in progetto di applicazione hello e selezionando **Aggiungi -> nuovo servizio Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="7588b-172">In hello same *HelloWorld* application, you can add a new service by right-clicking on hello Services references in hello application project and selecting **Add ->  New Service Fabric Service**.</span></span>

![Aggiungere un tooyour servizio applicazione di Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

<span data-ttu-id="7588b-174">Selezionare **Stateful Service** e assegnare il nome *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="7588b-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span></span> <span data-ttu-id="7588b-175">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="7588b-175">Click **OK**.</span></span>

![Utilizzare toocreate casella di dialogo Nuovo progetto hello un nuovo servizio con stato di Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

<span data-ttu-id="7588b-177">A questo punto l'applicazione deve disporre di due servizi: hello servizio senza stato *HelloWorldStateless* e il servizio con stato hello *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="7588b-177">Your application should now have two services: hello stateless service *HelloWorldStateless* and hello stateful service *HelloWorldStateful*.</span></span>

<span data-ttu-id="7588b-178">Hello dispone di un servizio con stato punti di ingresso stesso come un servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="7588b-178">A stateful service has hello same entry points as a stateless service.</span></span> <span data-ttu-id="7588b-179">la differenza principale Hello è hello di disponibilità di un *provider di stato* che possono archiviare lo stato in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="7588b-179">hello main difference is hello availability of a *state provider* that can store state reliably.</span></span> <span data-ttu-id="7588b-180">Infrastruttura del servizio viene fornito con un'implementazione del provider di stata chiamata [raccolte affidabile](service-fabric-reliable-services-reliable-collections.md), che consente di creare strutture dei dati replicati tramite hello affidabile di gestione dello stato.</span><span class="sxs-lookup"><span data-stu-id="7588b-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through hello Reliable State Manager.</span></span> <span data-ttu-id="7588b-181">Un servizio Reliable Services con stato usa questo provider di stato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="7588b-181">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="7588b-182">Aprire **HelloWorldStateful.cs** in *HelloWorldStateful*, che contiene hello RunAsync al metodo:</span><span class="sxs-lookup"><span data-stu-id="7588b-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains hello following RunAsync method:</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a><span data-ttu-id="7588b-183">RunAsync</span><span class="sxs-lookup"><span data-stu-id="7588b-183">RunAsync</span></span>
<span data-ttu-id="7588b-184">`RunAsync()` funziona in modo simile sia nei servizi con stato che nei servizi senza stato.</span><span class="sxs-lookup"><span data-stu-id="7588b-184">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="7588b-185">Tuttavia, in un servizio con stato, la piattaforma hello esegue ulteriori operazioni per conto dell'utente prima di eseguire `RunAsync()`.</span><span class="sxs-lookup"><span data-stu-id="7588b-185">However, in a stateful service, hello platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="7588b-186">Questa operazione può includere assicurandosi che hello affidabile di gestione dello stato e affidabile le raccolte sono toouse pronto.</span><span class="sxs-lookup"><span data-stu-id="7588b-186">This work can include ensuring that hello Reliable State Manager and Reliable Collections are ready toouse.</span></span>

### <a name="reliable-collections-and-hello-reliable-state-manager"></a><span data-ttu-id="7588b-187">Affidabile raccolte e hello affidabile di gestione dello stato</span><span class="sxs-lookup"><span data-stu-id="7588b-187">Reliable Collections and hello Reliable State Manager</span></span>
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

<span data-ttu-id="7588b-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) è un'implementazione di dizionario, che è possibile utilizzare tooreliably archiviare lo stato del servizio hello.</span><span class="sxs-lookup"><span data-stu-id="7588b-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use tooreliably store state in hello service.</span></span> <span data-ttu-id="7588b-189">Con Service Fabric e raccolte affidabile, è possibile archiviare i dati direttamente nel servizio senza necessità di hello di un archivio permanente esterno.</span><span class="sxs-lookup"><span data-stu-id="7588b-189">With Service Fabric and Reliable Collections, you can store data directly in your service without hello need for an external persistent store.</span></span> <span data-ttu-id="7588b-190">Le raccolte Reliable Collections garantiscono la disponibilità elevata dei dati.</span><span class="sxs-lookup"><span data-stu-id="7588b-190">Reliable Collections make your data highly available.</span></span> <span data-ttu-id="7588b-191">A tale scopo, Service Fabric crea e gestisce automaticamente più *repliche* del servizio.</span><span class="sxs-lookup"><span data-stu-id="7588b-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="7588b-192">Fornisce inoltre un'API che astrae complessità di stoccaggio hello della gestione di tali repliche e le transizioni di stato.</span><span class="sxs-lookup"><span data-stu-id="7588b-192">It also provides an API that abstracts away hello complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="7588b-193">Le raccolte Reliable Collections possono archiviare qualsiasi tipo .NET, inclusi quelli personalizzati, con alcuni avvertimenti:</span><span class="sxs-lookup"><span data-stu-id="7588b-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="7588b-194">Service Fabric rende lo stato a disponibilità elevata *replica* stato tra nodi e le raccolte affidabile archiviare disco toolocal dati in ogni replica.</span><span class="sxs-lookup"><span data-stu-id="7588b-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data toolocal disk on each replica.</span></span> <span data-ttu-id="7588b-195">Questo significa che tutti gli elementi archiviati in Reliable Collections devono essere *serializzabili*.</span><span class="sxs-lookup"><span data-stu-id="7588b-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span></span> <span data-ttu-id="7588b-196">Per impostazione predefinita, utilizzare le raccolte affidabile [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) per la serializzazione, è importante toomake assicurarsi che i tipi siano [supportati dal serializzatore dei contratti dati hello](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) quando si utilizza l'impostazione predefinita hello serializzatore.</span><span class="sxs-lookup"><span data-stu-id="7588b-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important toomake sure that your types are [supported by hello Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use hello default serializer.</span></span>
* <span data-ttu-id="7588b-197">Quando si esegue il commit di transazioni nelle raccolte Reliable Collections, gli oggetti vengono replicati per assicurare disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="7588b-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span></span> <span data-ttu-id="7588b-198">Gli oggetti archiviati nelle raccolte Reliable Collections vengono conservati nella memoria locale del servizio.</span><span class="sxs-lookup"><span data-stu-id="7588b-198">Objects stored in Reliable Collections are kept in local memory in your service.</span></span> <span data-ttu-id="7588b-199">Ciò significa che si disponga di un oggetto toohello riferimento locale.</span><span class="sxs-lookup"><span data-stu-id="7588b-199">This means that you have a local reference toohello object.</span></span>
  
   <span data-ttu-id="7588b-200">È importante non modificare le istanze locali di tali oggetti senza eseguire un'operazione di aggiornamento nella raccolta affidabile di hello in una transazione.</span><span class="sxs-lookup"><span data-stu-id="7588b-200">It is important that you do not mutate local instances of those objects without performing an update operation on hello reliable collection in a transaction.</span></span> <span data-ttu-id="7588b-201">Questo avviene perché le modifiche toolocal istanze di oggetti non verranno replicate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7588b-201">This is because changes toolocal instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="7588b-202">È necessario inserire nuovamente oggetto hello nel dizionario di hello o utilizzare uno dei hello *aggiornare* metodi nel dizionario di hello.</span><span class="sxs-lookup"><span data-stu-id="7588b-202">You must re-insert hello object back into hello dictionary or use one of hello *update* methods on hello dictionary.</span></span>

<span data-ttu-id="7588b-203">Hello affidabile di gestione dello stato gestisce raccolte affidabile per l'utente.</span><span class="sxs-lookup"><span data-stu-id="7588b-203">hello Reliable State Manager manages Reliable Collections for you.</span></span> <span data-ttu-id="7588b-204">È possibile semplicemente chiedere hello affidabile di gestione dello stato per un insieme affidabile in base al nome in qualsiasi momento e in qualsiasi punto del servizio.</span><span class="sxs-lookup"><span data-stu-id="7588b-204">You can simply ask hello Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="7588b-205">Hello affidabile di gestione dello stato consente di ottenere un riferimento nuovamente.</span><span class="sxs-lookup"><span data-stu-id="7588b-205">hello Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="7588b-206">Non è consigliabile salvare i riferimenti tooreliable raccolta istanze nelle variabili di membro di classe o proprietà.</span><span class="sxs-lookup"><span data-stu-id="7588b-206">We don't recommended that you save references tooreliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="7588b-207">È necessario prestare particolare attenzione tooensure impostato riferimento hello tooan istanza sempre hello del ciclo di vita del servizio.</span><span class="sxs-lookup"><span data-stu-id="7588b-207">Special care must be taken tooensure that hello reference is set tooan instance at all times in hello service lifecycle.</span></span> <span data-ttu-id="7588b-208">Hello affidabile di gestione dello stato gestisce questo lavoro per l'utente ed è ottimizzato per tornino.</span><span class="sxs-lookup"><span data-stu-id="7588b-208">hello Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>

### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="7588b-209">Operazioni transazionali e asincrone</span><span class="sxs-lookup"><span data-stu-id="7588b-209">Transactional and asynchronous operations</span></span>
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

<span data-ttu-id="7588b-210">Raccolte affidabile hanno molte hello stesse operazioni che i relativi `System.Collections.Generic` e `System.Collections.Concurrent` corrispondenti, ad eccezione di LINQ.</span><span class="sxs-lookup"><span data-stu-id="7588b-210">Reliable Collections have many of hello same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span></span> <span data-ttu-id="7588b-211">Le operazioni sulle raccolte Reliable Collections sono asincrone.</span><span class="sxs-lookup"><span data-stu-id="7588b-211">Operations on Reliable Collections are asynchronous.</span></span> <span data-ttu-id="7588b-212">In questo modo le operazioni di scrittura con le raccolte affidabile eseguono tooreplicate di operazioni dei / o e mantenere i dati toodisk.</span><span class="sxs-lookup"><span data-stu-id="7588b-212">This is because write operations with Reliable Collections perform I/O operations tooreplicate and persist data toodisk.</span></span>

<span data-ttu-id="7588b-213">Le operazioni sulle raccolte Reliable Collections sono *transazionali*e consentono di mantenere lo stato coerente tra più raccolte Reliable Collections e operazioni.</span><span class="sxs-lookup"><span data-stu-id="7588b-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span></span> <span data-ttu-id="7588b-214">Ad esempio, è possibile rimuovere dalla coda un elemento di lavoro da una coda affidabile, eseguire un'operazione su di esso e salvare hello risultato in un dizionario affidabile, tutti in un'unica transazione.</span><span class="sxs-lookup"><span data-stu-id="7588b-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save hello result in a Reliable Dictionary, all within a single transaction.</span></span> <span data-ttu-id="7588b-215">Viene considerato come operazione atomica e garantisce che verrà completata l'intera operazione hello o verrà eseguito il rollback dell'intera operazione hello.</span><span class="sxs-lookup"><span data-stu-id="7588b-215">This is treated as an atomic operation, and it guarantees that either hello entire operation will succeed or hello entire operation will roll back.</span></span> <span data-ttu-id="7588b-216">Se si verifica un errore dopo che di rimozione dalla coda elemento hello ma prima di salvare i risultati di hello, viene eseguito il rollback dell'intera transazione hello e hello elemento rimane nella coda di hello per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="7588b-216">If an error occurs after you dequeue hello item but before you save hello result, hello entire transaction is rolled back and hello item remains in hello queue for processing.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="7588b-217">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="7588b-217">Run hello application</span></span>
<span data-ttu-id="7588b-218">È ora restituire toohello *HelloWorld* dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7588b-218">We now return toohello *HelloWorld* application.</span></span> <span data-ttu-id="7588b-219">È ora possibile compilare e distribuire i servizi.</span><span class="sxs-lookup"><span data-stu-id="7588b-219">You can now build and deploy your services.</span></span> <span data-ttu-id="7588b-220">Quando si preme **F5**, l'applicazione sarà cluster locale tooyour compilato e distribuito.</span><span class="sxs-lookup"><span data-stu-id="7588b-220">When you press **F5**, your application will be built and deployed tooyour local cluster.</span></span>

<span data-ttu-id="7588b-221">Dopo l'esecuzione dei servizi hello, è possibile visualizzare gli eventi Event Tracing for Windows (ETW) hello generato in un **gli eventi di diagnostica** finestra.</span><span class="sxs-lookup"><span data-stu-id="7588b-221">After hello services start running, you can view hello generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span></span> <span data-ttu-id="7588b-222">Si noti che gli eventi di hello visualizzati dal servizio senza stato hello sia il servizio con stato di hello in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7588b-222">Note that hello events displayed are from both hello stateless service and hello stateful service in hello application.</span></span> <span data-ttu-id="7588b-223">È possibile sospendere un flusso di hello facendo hello **sospendere** pulsante.</span><span class="sxs-lookup"><span data-stu-id="7588b-223">You can pause hello stream by clicking hello **Pause** button.</span></span> <span data-ttu-id="7588b-224">È quindi possibile esaminare i dettagli di hello di un messaggio espandendo tale messaggio.</span><span class="sxs-lookup"><span data-stu-id="7588b-224">You can then examine hello details of a message by expanding that message.</span></span>

> [!NOTE]
> <span data-ttu-id="7588b-225">Prima di eseguire un'applicazione hello, assicurarsi di disporre di un cluster di sviluppo locale che esegue.</span><span class="sxs-lookup"><span data-stu-id="7588b-225">Before you run hello application, make sure that you have a local development cluster running.</span></span> <span data-ttu-id="7588b-226">Estrarre hello [Guida introduttiva](service-fabric-get-started.md) per informazioni su come configurare l'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="7588b-226">Check out hello [getting started guide](service-fabric-get-started.md) for information on setting up your local environment.</span></span>
> 
> 

![Visualizzare gli eventi di diagnostica in Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a><span data-ttu-id="7588b-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7588b-228">Next steps</span></span>
[<span data-ttu-id="7588b-229">Debug dell'applicazione di Service Fabric in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7588b-229">Debug your Service Fabric application in Visual Studio</span></span>](service-fabric-debugging-your-application.md)

[<span data-ttu-id="7588b-230">Introduzione ai servizi API Web di Service Fabric con self-hosting OWIN</span><span class="sxs-lookup"><span data-stu-id="7588b-230">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>](service-fabric-reliable-services-communication-webapi.md)

[<span data-ttu-id="7588b-231">Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="7588b-231">Learn more about Reliable Collections</span></span>](service-fabric-reliable-services-reliable-collections.md)

[<span data-ttu-id="7588b-232">Distribuire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="7588b-232">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="7588b-233">Aggiornamento dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="7588b-233">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="7588b-234">Guida di riferimento per gli sviluppatori per Reliable Services</span><span class="sxs-lookup"><span data-stu-id="7588b-234">Developer reference for Reliable Services</span></span>](https://msdn.microsoft.com/library/azure/dn706529.aspx)

