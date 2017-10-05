---
title: Creare la prima applicazione di Service Fabric in C# | Microsoft Docs
description: "Introduzione alla creazione di un’applicazione dell’infrastruttura di servizi di Microsoft Azure con i servizi con e senza stato."
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
ms.openlocfilehash: 813021d6239ae3cf79bb84b78f77e39c9e0783f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="905b3-103">Introduzione a Reliable Services</span><span class="sxs-lookup"><span data-stu-id="905b3-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="905b3-104">C# su Windows</span><span class="sxs-lookup"><span data-stu-id="905b3-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="905b3-105">Java su Linux</span><span class="sxs-lookup"><span data-stu-id="905b3-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
> 
> 

<span data-ttu-id="905b3-106">Un'applicazione di Azure Service Fabric contiene uno o più servizi che consentono l'esecuzione del codice.</span><span class="sxs-lookup"><span data-stu-id="905b3-106">An Azure Service Fabric application contains one or more services that run your code.</span></span> <span data-ttu-id="905b3-107">Questa guida illustra come creare applicazioni di Service Fabric con e senza stato con i servizi [Reliable Services](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="905b3-107">This guide shows you how to create both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span></span>  <span data-ttu-id="905b3-108">Questo video di Microsoft Virtual Academy illustra anche come creare un servizio Reliable Services senza stato: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span><span class="sxs-lookup"><span data-stu-id="905b3-108">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a><span data-ttu-id="905b3-109">Concetti di base</span><span class="sxs-lookup"><span data-stu-id="905b3-109">Basic concepts</span></span>
<span data-ttu-id="905b3-110">Per iniziare a usare Reliable Services, è sufficiente comprendere solo alcuni concetti di base:</span><span class="sxs-lookup"><span data-stu-id="905b3-110">To get started with Reliable Services, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="905b3-111">**Tipo di servizio**: si tratta dell'implementazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="905b3-111">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="905b3-112">Viene definito dalla classe scritta che estende `StatelessService` e qualsiasi altro codice o dipendenze usate, insieme al nome e al numero della versione.</span><span class="sxs-lookup"><span data-stu-id="905b3-112">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="905b3-113">**Istanza di servizio denominata**: per eseguire il servizio, si creano le istanze denominate del tipo di servizio, analogamente al modo in cui si creano le istanze di un oggetto di un tipo di classe.</span><span class="sxs-lookup"><span data-stu-id="905b3-113">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="905b3-114">Il formato del nome di un'istanza del servizio è un URI che usa lo schema "fabric:/", ad esempio "fabric:/MyApp/MyService".</span><span class="sxs-lookup"><span data-stu-id="905b3-114">A service instance has a name in the form of a URI using the "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span></span>
* <span data-ttu-id="905b3-115">**Host del servizio**: le istanze del servizio denominate che si creano devono essere eseguite in un processo host.</span><span class="sxs-lookup"><span data-stu-id="905b3-115">**Service host**: The named service instances you create need to run inside a host process.</span></span> <span data-ttu-id="905b3-116">L'host del servizio è semplicemente un processo in cui eseguire le istanze del servizio.</span><span class="sxs-lookup"><span data-stu-id="905b3-116">The service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="905b3-117">**Registrazione del servizio**: la registrazione raccoglie tutti gli elementi.</span><span class="sxs-lookup"><span data-stu-id="905b3-117">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="905b3-118">Il tipo di servizio deve essere registrato con il runtime di Service Fabric in un host del servizio per consentire a Service Fabric di creare istanze per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="905b3-118">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="905b3-119">Creare un servizio senza stato</span><span class="sxs-lookup"><span data-stu-id="905b3-119">Create a stateless service</span></span>
<span data-ttu-id="905b3-120">Il servizio senza stato è il tipo di servizio di norma presente nelle applicazioni cloud.</span><span class="sxs-lookup"><span data-stu-id="905b3-120">A stateless service is a type of service that is currently the norm in cloud applications.</span></span> <span data-ttu-id="905b3-121">Viene considerato senza stato perché il servizio stesso non contiene dati che devono essere archiviati in modo affidabile o resi a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="905b3-121">It is considered stateless because the service itself does not contain data that needs to be stored reliably or made highly available.</span></span> <span data-ttu-id="905b3-122">Se un'istanza di un servizio senza stato si arresta, il relativo stato interno viene perso.</span><span class="sxs-lookup"><span data-stu-id="905b3-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span></span> <span data-ttu-id="905b3-123">In questi tipi di servizio lo stato deve essere reso persistente mediante un archivio esterno, ad esempio tabelle di Azure o un database SQL, in modo da assicurare elevata disponibilità e affidabilità.</span><span class="sxs-lookup"><span data-stu-id="905b3-123">In this type of service, state must be persisted to an external store, such as Azure Tables or a SQL database, for it to be made highly available and reliable.</span></span>

<span data-ttu-id="905b3-124">Avviare Visual Studio 2015 o Visual Studio 2017 come amministratore e creare un nuovo progetto di applicazione di Service Fabric denominato *HelloWorld*:</span><span class="sxs-lookup"><span data-stu-id="905b3-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span></span>

![Uso della finestra di dialogo New Project per creare una nuova applicazione di Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

<span data-ttu-id="905b3-126">Creare quindi un progetto di servizio senza stato denominato *HelloWorldStateless*:</span><span class="sxs-lookup"><span data-stu-id="905b3-126">Then create a stateless service project named *HelloWorldStateless*:</span></span>

![Nella seconda finestra di dialogo creare un progetto di servizio senza stato](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

<span data-ttu-id="905b3-128">La soluzione ora contiene due progetti:</span><span class="sxs-lookup"><span data-stu-id="905b3-128">Your solution now contains two projects:</span></span>

* <span data-ttu-id="905b3-129">*HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="905b3-129">*HelloWorld*.</span></span> <span data-ttu-id="905b3-130">Si tratta del progetto *applicazione* contenente i *servizi*.</span><span class="sxs-lookup"><span data-stu-id="905b3-130">This is the *application* project that contains your *services*.</span></span> <span data-ttu-id="905b3-131">Il progetto contiene anche il manifesto dell'applicazione che descrive l'applicazione stessa, oltre ad alcuni script di PowerShell che consentono di distribuirla.</span><span class="sxs-lookup"><span data-stu-id="905b3-131">It also contains the application manifest that describes the application, as well as a number of PowerShell scripts that help you to deploy your application.</span></span>
* <span data-ttu-id="905b3-132">*HelloWorldStateless*.</span><span class="sxs-lookup"><span data-stu-id="905b3-132">*HelloWorldStateless*.</span></span> <span data-ttu-id="905b3-133">Si tratta del progetto di servizio.</span><span class="sxs-lookup"><span data-stu-id="905b3-133">This is the service project.</span></span> <span data-ttu-id="905b3-134">Il progetto contiene l'implementazione del servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="905b3-134">It contains the stateless service implementation.</span></span>

## <a name="implement-the-service"></a><span data-ttu-id="905b3-135">Implementare il servizio</span><span class="sxs-lookup"><span data-stu-id="905b3-135">Implement the service</span></span>
<span data-ttu-id="905b3-136">Aprire il file **HelloWorldStateless.cs** nel progetto del servizio.</span><span class="sxs-lookup"><span data-stu-id="905b3-136">Open the **HelloWorldStateless.cs** file in the service project.</span></span> <span data-ttu-id="905b3-137">In Service Fabric un servizio può eseguire qualsiasi tipo di logica di business.</span><span class="sxs-lookup"><span data-stu-id="905b3-137">In Service Fabric, a service can run any business logic.</span></span> <span data-ttu-id="905b3-138">L'API del servizio fornisce due punti di ingresso per il codice:</span><span class="sxs-lookup"><span data-stu-id="905b3-138">The service API provides two entry points for your code:</span></span>

* <span data-ttu-id="905b3-139">Un metodo del punto di ingresso aperto denominato *RunAsync*, che consente di iniziare a eseguire qualsiasi carico di lavoro, inclusi carichi di lavoro di calcolo con esecuzione prolungata.</span><span class="sxs-lookup"><span data-stu-id="905b3-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* <span data-ttu-id="905b3-140">Un punto di ingresso di comunicazione a cui è possibile collegare lo stack di comunicazione desiderato, come ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="905b3-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span></span> <span data-ttu-id="905b3-141">In questo punto è possibile iniziare a ricevere richieste da utenti e da altri servizi.</span><span class="sxs-lookup"><span data-stu-id="905b3-141">This is where you can start receiving requests from users and other services.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

<span data-ttu-id="905b3-142">Questa esercitazione si concentra sul metodo del punto di ingresso `RunAsync()` .</span><span class="sxs-lookup"><span data-stu-id="905b3-142">In this tutorial, we will focus on the `RunAsync()` entry point method.</span></span> <span data-ttu-id="905b3-143">In questo punto è possibile iniziare immediatamente a eseguire il codice.</span><span class="sxs-lookup"><span data-stu-id="905b3-143">This is where you can immediately start running your code.</span></span>
<span data-ttu-id="905b3-144">Il modello di progetto include un esempio di implementazione di `RunAsync()` che gestisce un conteggio incrementale.</span><span class="sxs-lookup"><span data-stu-id="905b3-144">The project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span></span>

> [!NOTE]
> <span data-ttu-id="905b3-145">Per informazioni dettagliate sull'uso di uno stack di comunicazione, vedere [Introduzione ai servizi API Web di Microsoft Azure Service Fabric con self-hosting OWIN](service-fabric-reliable-services-communication-webapi.md)</span><span class="sxs-lookup"><span data-stu-id="905b3-145">For details about how to work with a communication stack, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md)</span></span>
> 
> 

### <a name="runasync"></a><span data-ttu-id="905b3-146">RunAsync</span><span class="sxs-lookup"><span data-stu-id="905b3-146">RunAsync</span></span>
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace the following sample code with your own logic
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

<span data-ttu-id="905b3-147">La piattaforma chiama questo metodo quando si inserisce un'istanza di un servizio pronta per l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="905b3-147">The platform calls this method when an instance of a service is placed and ready to execute.</span></span> <span data-ttu-id="905b3-148">Per un servizio senza stato, la piattaforma chiama il metodo quando l'istanza del servizio viene aperta.</span><span class="sxs-lookup"><span data-stu-id="905b3-148">For a stateless service, that simply means when the service instance is opened.</span></span> <span data-ttu-id="905b3-149">Viene fornito un token di annullamento che determina quando è necessario chiudere l'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="905b3-149">A cancellation token is provided to coordinate when your service instance needs to be closed.</span></span> <span data-ttu-id="905b3-150">In Service Fabric questo ciclo di apertura e chiusura di un'istanza del servizio può verificarsi più volte per tutta la durata del servizio nel suo complesso.</span><span class="sxs-lookup"><span data-stu-id="905b3-150">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span></span> <span data-ttu-id="905b3-151">Questa situazione può verificarsi per vari motivi, tra cui:</span><span class="sxs-lookup"><span data-stu-id="905b3-151">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="905b3-152">Il sistema sposta le istanze del servizio per il bilanciamento delle risorse.</span><span class="sxs-lookup"><span data-stu-id="905b3-152">The system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="905b3-153">Si verificano errori nel codice.</span><span class="sxs-lookup"><span data-stu-id="905b3-153">Faults occur in your code.</span></span>
* <span data-ttu-id="905b3-154">Viene aggiornato il sistema o l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="905b3-154">The application or system is upgraded.</span></span>
* <span data-ttu-id="905b3-155">Si verifica un'interruzione nell'hardware sottostante.</span><span class="sxs-lookup"><span data-stu-id="905b3-155">The underlying hardware experiences an outage.</span></span>

<span data-ttu-id="905b3-156">Questa orchestrazione viene gestita dal sistema per assicurare l'elevata disponibilità e il corretto bilanciamento del servizio.</span><span class="sxs-lookup"><span data-stu-id="905b3-156">This orchestration is managed by the system to keep your service highly available and properly balanced.</span></span>

<span data-ttu-id="905b3-157">`RunAsync()` non deve bloccarsi in modo sincrono.</span><span class="sxs-lookup"><span data-stu-id="905b3-157">`RunAsync()` should not block synchronously.</span></span> <span data-ttu-id="905b3-158">L'implementazione di RunAsync deve restituire un'attività o restare in attesa in caso di operazioni a esecuzione prolungata oppure bloccate, per consentire al runtime di continuare.</span><span class="sxs-lookup"><span data-stu-id="905b3-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations to allow the runtime to continue.</span></span> <span data-ttu-id="905b3-159">Si noti che nel ciclo `while(true)` dell'esempio precedente viene usato `await Task.Delay()` per la restituzione di un'attività.</span><span class="sxs-lookup"><span data-stu-id="905b3-159">Note in the `while(true)` loop in the previous example, a Task-returning `await Task.Delay()` is used.</span></span> <span data-ttu-id="905b3-160">Se il carico di lavoro si deve bloccare in modo sincrono, è opportuno pianificare una nuova Task con `Task.Run()` nell'implementazione `RunAsync`.</span><span class="sxs-lookup"><span data-stu-id="905b3-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span></span>

<span data-ttu-id="905b3-161">L'annullamento del carico di lavoro è un'operazione cooperativa coordinata dal token di annullamento fornito.</span><span class="sxs-lookup"><span data-stu-id="905b3-161">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span></span> <span data-ttu-id="905b3-162">Il sistema attende la fine dell'attività (per esito positivo, annullamento o errore) prima di continuare.</span><span class="sxs-lookup"><span data-stu-id="905b3-162">The system will wait for your task to end (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="905b3-163">È importante rispettare il token di annullamento, completare le operazioni e chiudere `RunAsync()` il più rapidamente possibile quando viene richiesto l'annullamento dal sistema.</span><span class="sxs-lookup"><span data-stu-id="905b3-163">It is important to honor the cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when the system requests cancellation.</span></span>

<span data-ttu-id="905b3-164">In questo esempio di servizio senza stato il conteggio è archiviato in una variabile locale.</span><span class="sxs-lookup"><span data-stu-id="905b3-164">In this stateless service example, the count is stored in a local variable.</span></span> <span data-ttu-id="905b3-165">Tuttavia, poiché si tratta di un servizio senza stato, il valore archiviato esiste soltanto per il ciclo di vita corrente dell'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="905b3-165">But because this is a stateless service, the value that's stored exists only for the current lifecycle of its service instance.</span></span> <span data-ttu-id="905b3-166">Quando si posta o si riavvia il servizio, il valore viene perso.</span><span class="sxs-lookup"><span data-stu-id="905b3-166">When the service moves or restarts, the value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="905b3-167">Creare un servizio con stato</span><span class="sxs-lookup"><span data-stu-id="905b3-167">Create a stateful service</span></span>
<span data-ttu-id="905b3-168">Service Fabric introduce un nuovo tipo di servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="905b3-168">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="905b3-169">Un servizio con stato può mantenere lo stato affidabile all'interno del servizio stesso, con percorso condiviso con il codice che lo usa.</span><span class="sxs-lookup"><span data-stu-id="905b3-169">A stateful service can maintain state reliably within the service itself, co-located with the code that's using it.</span></span> <span data-ttu-id="905b3-170">L'elevata disponibilità dello stato è assicurata da Service Fabric, senza dover rendere persistente lo stato mediante un archivio esterno.</span><span class="sxs-lookup"><span data-stu-id="905b3-170">State is made highly available by Service Fabric without the need to persist state to an external store.</span></span>

<span data-ttu-id="905b3-171">Per convertire un valore del contatore da senza stato a elevata disponibilità e persistenza anche quando il servizio viene spostato o riavviato, è necessario un servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="905b3-171">To convert a counter value from stateless to highly available and persistent, even when the service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="905b3-172">Nella stessa applicazione *HelloWorld* aggiungere un nuovo servizio facendo clic con il pulsante destro del mouse sui riferimenti ai servizi nel progetto applicazione e selezionare **Aggiungi -> Nuovo servizio Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="905b3-172">In the same *HelloWorld* application, you can add a new service by right-clicking on the Services references in the application project and selecting **Add ->  New Service Fabric Service**.</span></span>

![Aggiungere un servizio all'applicazione di Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

<span data-ttu-id="905b3-174">Selezionare **Stateful Service** e assegnare il nome *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="905b3-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span></span> <span data-ttu-id="905b3-175">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="905b3-175">Click **OK**.</span></span>

![Uso della finestra di dialogo New Project per creare un nuovo servizio di Service Fabric con stato](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

<span data-ttu-id="905b3-177">A questo punto l'applicazione ha due servizi: il servizio senza stato *HelloWorldStateless* e il servizio con stato *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="905b3-177">Your application should now have two services: the stateless service *HelloWorldStateless* and the stateful service *HelloWorldStateful*.</span></span>

<span data-ttu-id="905b3-178">Un servizio con stato ha gli stessi punti di ingresso di un servizio senza stato.</span><span class="sxs-lookup"><span data-stu-id="905b3-178">A stateful service has the same entry points as a stateless service.</span></span> <span data-ttu-id="905b3-179">La differenza principale è data dalla disponibilità di un *provider di stato* che può archiviare lo stato in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="905b3-179">The main difference is the availability of a *state provider* that can store state reliably.</span></span> <span data-ttu-id="905b3-180">Service Fabric include un'implementazione del provider di stato denominata [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), che permette di creare strutture di dati replicate tramite Reliable State Manager.</span><span class="sxs-lookup"><span data-stu-id="905b3-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through the Reliable State Manager.</span></span> <span data-ttu-id="905b3-181">Un servizio Reliable Services con stato usa questo provider di stato per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="905b3-181">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="905b3-182">Aprire **HelloWorldStateful.cs** in *HelloWorldStateful*che contiene il metodo RunAsync seguente:</span><span class="sxs-lookup"><span data-stu-id="905b3-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains the following RunAsync method:</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace the following sample code with your own logic
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

            // If an exception is thrown before calling CommitAsync, the transaction aborts, all changes are
            // discarded, and nothing is saved to the secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a><span data-ttu-id="905b3-183">RunAsync</span><span class="sxs-lookup"><span data-stu-id="905b3-183">RunAsync</span></span>
<span data-ttu-id="905b3-184">`RunAsync()` funziona in modo simile sia nei servizi con stato che nei servizi senza stato.</span><span class="sxs-lookup"><span data-stu-id="905b3-184">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="905b3-185">In un servizio con stato la piattaforma esegue tuttavia operazioni aggiuntive per conto dell'utente prima di eseguire `RunAsync()`.</span><span class="sxs-lookup"><span data-stu-id="905b3-185">However, in a stateful service, the platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="905b3-186">Tali operazioni possono includere la verifica che Reliable State Manager e Reliable Collections siano pronti per l'uso.</span><span class="sxs-lookup"><span data-stu-id="905b3-186">This work can include ensuring that the Reliable State Manager and Reliable Collections are ready to use.</span></span>

### <a name="reliable-collections-and-the-reliable-state-manager"></a><span data-ttu-id="905b3-187">Reliable Collections e Reliable State Manager</span><span class="sxs-lookup"><span data-stu-id="905b3-187">Reliable Collections and the Reliable State Manager</span></span>
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

<span data-ttu-id="905b3-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) è un'implementazione di dizionario che permette di archiviare in modo affidabile lo stato nel servizio.</span><span class="sxs-lookup"><span data-stu-id="905b3-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use to reliably store state in the service.</span></span> <span data-ttu-id="905b3-189">Grazie a Service Fabric e alle raccolte Reliable Collections è possibile archiviare i dati direttamente nel servizio, senza la necessità di un archivio esterno persistente.</span><span class="sxs-lookup"><span data-stu-id="905b3-189">With Service Fabric and Reliable Collections, you can store data directly in your service without the need for an external persistent store.</span></span> <span data-ttu-id="905b3-190">Le raccolte Reliable Collections garantiscono la disponibilità elevata dei dati.</span><span class="sxs-lookup"><span data-stu-id="905b3-190">Reliable Collections make your data highly available.</span></span> <span data-ttu-id="905b3-191">A tale scopo, Service Fabric crea e gestisce automaticamente più *repliche* del servizio.</span><span class="sxs-lookup"><span data-stu-id="905b3-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="905b3-192">Offre anche un'API che consente di evitare le complessità di gestione di tali repliche e delle relative transizioni di stato.</span><span class="sxs-lookup"><span data-stu-id="905b3-192">It also provides an API that abstracts away the complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="905b3-193">Le raccolte Reliable Collections possono archiviare qualsiasi tipo .NET, inclusi quelli personalizzati, con alcuni avvertimenti:</span><span class="sxs-lookup"><span data-stu-id="905b3-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="905b3-194">Service Fabric garantisce la disponibilità elevata dello stato *replicando* lo stato nei nodi, mentre Reliable Collections archivia i dati nel disco locale a ogni replica.</span><span class="sxs-lookup"><span data-stu-id="905b3-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data to local disk on each replica.</span></span> <span data-ttu-id="905b3-195">Questo significa che tutti gli elementi archiviati in Reliable Collections devono essere *serializzabili*.</span><span class="sxs-lookup"><span data-stu-id="905b3-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span></span> <span data-ttu-id="905b3-196">Per impostazione predefinita, le raccolte Reliable Collections usano [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) per la serializzazione. Quando si usa il serializzatore predefinito, è quindi importante assicurarsi che i tipi siano [supportati dal serializzatore dei contratti dati](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="905b3-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important to make sure that your types are [supported by the Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use the default serializer.</span></span>
* <span data-ttu-id="905b3-197">Quando si esegue il commit di transazioni nelle raccolte Reliable Collections, gli oggetti vengono replicati per assicurare disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="905b3-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span></span> <span data-ttu-id="905b3-198">Gli oggetti archiviati nelle raccolte Reliable Collections vengono conservati nella memoria locale del servizio.</span><span class="sxs-lookup"><span data-stu-id="905b3-198">Objects stored in Reliable Collections are kept in local memory in your service.</span></span> <span data-ttu-id="905b3-199">Ciò significa che è presente un riferimento locale all'oggetto.</span><span class="sxs-lookup"><span data-stu-id="905b3-199">This means that you have a local reference to the object.</span></span>
  
   <span data-ttu-id="905b3-200">È importante non apportare modifiche alle istanze locali degli oggetti senza prima eseguire un'operazione di aggiornamento sulla raccolta Reliable Collections in una transazione.</span><span class="sxs-lookup"><span data-stu-id="905b3-200">It is important that you do not mutate local instances of those objects without performing an update operation on the reliable collection in a transaction.</span></span> <span data-ttu-id="905b3-201">Le modifiche apportate alle istanze locali di oggetti, infatti, non vengono replicate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="905b3-201">This is because changes to local instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="905b3-202">È necessario inserire nuovamente l'oggetto nel dizionario oppure usare uno dei metodi di *aggiornamento* nel dizionario.</span><span class="sxs-lookup"><span data-stu-id="905b3-202">You must re-insert the object back into the dictionary or use one of the *update* methods on the dictionary.</span></span>

<span data-ttu-id="905b3-203">Reliable State Manager gestisce automaticamente le raccolte Reliable Collections.</span><span class="sxs-lookup"><span data-stu-id="905b3-203">The Reliable State Manager manages Reliable Collections for you.</span></span> <span data-ttu-id="905b3-204">In qualunque momento e in qualsiasi posizione del servizio è possibile chiedere a Reliable State Manager una raccolta Reliable Collections indicandone il nome.</span><span class="sxs-lookup"><span data-stu-id="905b3-204">You can simply ask the Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="905b3-205">Reliable State Manager restituirà un riferimento.</span><span class="sxs-lookup"><span data-stu-id="905b3-205">The Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="905b3-206">Non si consiglia di salvare riferimenti alle istanze di raccolte Reliable Collections in proprietà o variabili membri di classe.</span><span class="sxs-lookup"><span data-stu-id="905b3-206">We don't recommended that you save references to reliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="905b3-207">Prestare particolare attenzione per assicurarsi che il riferimento sia sempre impostato su un'istanza durante il ciclo di vita del servizio.</span><span class="sxs-lookup"><span data-stu-id="905b3-207">Special care must be taken to ensure that the reference is set to an instance at all times in the service lifecycle.</span></span> <span data-ttu-id="905b3-208">Reliable State Manager gestisce queste operazioni automaticamente ed è ottimizzato per le visite ripetute.</span><span class="sxs-lookup"><span data-stu-id="905b3-208">The Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>

### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="905b3-209">Operazioni transazionali e asincrone</span><span class="sxs-lookup"><span data-stu-id="905b3-209">Transactional and asynchronous operations</span></span>
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

<span data-ttu-id="905b3-210">Le raccolte Reliable Collections includono molte delle operazioni corrispondenti di `System.Collections.Generic` e `System.Collections.Concurrent`, tranne LINQ.</span><span class="sxs-lookup"><span data-stu-id="905b3-210">Reliable Collections have many of the same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span></span> <span data-ttu-id="905b3-211">Le operazioni sulle raccolte Reliable Collections sono asincrone.</span><span class="sxs-lookup"><span data-stu-id="905b3-211">Operations on Reliable Collections are asynchronous.</span></span> <span data-ttu-id="905b3-212">Questo avviene perché le operazioni di scrittura sulle raccolte Reliable Collections eseguono operazioni di I/O per replicare e rendere persistenti i dati su disco.</span><span class="sxs-lookup"><span data-stu-id="905b3-212">This is because write operations with Reliable Collections perform I/O operations to replicate and persist data to disk.</span></span>

<span data-ttu-id="905b3-213">Le operazioni sulle raccolte Reliable Collections sono *transazionali*e consentono di mantenere lo stato coerente tra più raccolte Reliable Collections e operazioni.</span><span class="sxs-lookup"><span data-stu-id="905b3-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span></span> <span data-ttu-id="905b3-214">Ad esempio, è possibile rimuovere un elemento di lavoro da un oggetto ReliableQueue, eseguire un'operazione su tale elemento e salvare il risultato in un oggetto ReliableDictionary, il tutto all'interno di una singola transazione.</span><span class="sxs-lookup"><span data-stu-id="905b3-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save the result in a Reliable Dictionary, all within a single transaction.</span></span> <span data-ttu-id="905b3-215">Questa viene considerata come un'operazione atomica e garantisce la riuscita o il rollback dell'intera operazione.</span><span class="sxs-lookup"><span data-stu-id="905b3-215">This is treated as an atomic operation, and it guarantees that either the entire operation will succeed or the entire operation will roll back.</span></span> <span data-ttu-id="905b3-216">Se si verifica un errore dopo aver rimosso l'elemento dalla coda ma prima di aver salvato il risultato, viene eseguito il rollback dell'intera transazione e l'elemento rimane nella coda per l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="905b3-216">If an error occurs after you dequeue the item but before you save the result, the entire transaction is rolled back and the item remains in the queue for processing.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="905b3-217">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="905b3-217">Run the application</span></span>
<span data-ttu-id="905b3-218">Tornare all'applicazione *HelloWorld* .</span><span class="sxs-lookup"><span data-stu-id="905b3-218">We now return to the *HelloWorld* application.</span></span> <span data-ttu-id="905b3-219">È ora possibile compilare e distribuire i servizi.</span><span class="sxs-lookup"><span data-stu-id="905b3-219">You can now build and deploy your services.</span></span> <span data-ttu-id="905b3-220">Quando si preme **F5**, l'applicazione viene compilata e distribuita nel cluster locale.</span><span class="sxs-lookup"><span data-stu-id="905b3-220">When you press **F5**, your application will be built and deployed to your local cluster.</span></span>

<span data-ttu-id="905b3-221">Dopo l'avvio dell'esecuzione dei servizi, è possibile visualizzare gli eventi generati di Event Tracing for Windows (ETW) in una finestra **Eventi di diagnostica** .</span><span class="sxs-lookup"><span data-stu-id="905b3-221">After the services start running, you can view the generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span></span> <span data-ttu-id="905b3-222">Si noti che gli eventi visualizzati nell'applicazione provengono sia dal servizio senza stato sia dal servizio con stato.</span><span class="sxs-lookup"><span data-stu-id="905b3-222">Note that the events displayed are from both the stateless service and the stateful service in the application.</span></span> <span data-ttu-id="905b3-223">È possibile sospendere il flusso facendo clic sul pulsante **Pausa** .</span><span class="sxs-lookup"><span data-stu-id="905b3-223">You can pause the stream by clicking the **Pause** button.</span></span> <span data-ttu-id="905b3-224">Espandendo un messaggio è possibile esaminarne i dettagli.</span><span class="sxs-lookup"><span data-stu-id="905b3-224">You can then examine the details of a message by expanding that message.</span></span>

> [!NOTE]
> <span data-ttu-id="905b3-225">Prima di eseguire l'applicazione, assicurarsi di avere un cluster di sviluppo locale in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="905b3-225">Before you run the application, make sure that you have a local development cluster running.</span></span> <span data-ttu-id="905b3-226">Per informazioni sulla configurazione dell'ambiente locale, vedere la [guida introduttiva](service-fabric-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="905b3-226">Check out the [getting started guide](service-fabric-get-started.md) for information on setting up your local environment.</span></span>
> 
> 

![Visualizzare gli eventi di diagnostica in Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a><span data-ttu-id="905b3-228">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="905b3-228">Next steps</span></span>
[<span data-ttu-id="905b3-229">Debug dell'applicazione di Service Fabric in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="905b3-229">Debug your Service Fabric application in Visual Studio</span></span>](service-fabric-debugging-your-application.md)

[<span data-ttu-id="905b3-230">Introduzione ai servizi API Web di Service Fabric con self-hosting OWIN</span><span class="sxs-lookup"><span data-stu-id="905b3-230">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>](service-fabric-reliable-services-communication-webapi.md)

[<span data-ttu-id="905b3-231">Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="905b3-231">Learn more about Reliable Collections</span></span>](service-fabric-reliable-services-reliable-collections.md)

[<span data-ttu-id="905b3-232">Distribuire un'applicazione</span><span class="sxs-lookup"><span data-stu-id="905b3-232">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="905b3-233">Aggiornamento dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="905b3-233">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="905b3-234">Guida di riferimento per gli sviluppatori per Reliable Services</span><span class="sxs-lookup"><span data-stu-id="905b3-234">Developer reference for Reliable Services</span></span>](https://msdn.microsoft.com/library/azure/dn706529.aspx)

