---
title: aaaReliable attori in Service Fabric | Documenti Microsoft
description: "Viene descritto come Reliable Actors si basano su servizi affidabili e utilizzare le funzionalità di hello della piattaforma di Service Fabric hello."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 45839a7f-0536-46f1-ae2b-8ba3556407fb
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: ecffb54139f1171c7839b77fed0be60950881198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a><span data-ttu-id="d81b0-103">Utilizzo di piattaforma Service Fabric hello Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="d81b0-103">How Reliable Actors use hello Service Fabric platform</span></span>
<span data-ttu-id="d81b0-104">In questo articolo descrive il modo Reliable Actors sulla piattaforma Azure Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="d81b0-104">This article explains how Reliable Actors work on hello Azure Service Fabric platform.</span></span> <span data-ttu-id="d81b0-105">Reliable Actors eseguite in un framework che è ospitato in un'implementazione di un servizio affidabile con stato chiamato hello *servizio actor*.</span><span class="sxs-lookup"><span data-stu-id="d81b0-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called hello *actor service*.</span></span> <span data-ttu-id="d81b0-106">servizio actor Hello contiene tutti i ciclo di vita hello toomanage necessari componenti hello e un messaggio di invio per gli attori:</span><span class="sxs-lookup"><span data-stu-id="d81b0-106">hello actor service contains all hello components necessary toomanage hello lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="d81b0-107">Hello attore Runtime gestisce ciclo di vita, operazioni di garbage collection e applica l'accesso a thread singolo.</span><span class="sxs-lookup"><span data-stu-id="d81b0-107">hello Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="d81b0-108">Un listener di comunicazione remota del servizio actor accetta tooactors chiamate di accesso remoto e li invia a istanza di tooa dispatcher tooroute toohello attore appropriato.</span><span class="sxs-lookup"><span data-stu-id="d81b0-108">An actor service remoting listener accepts remote access calls tooactors and sends them tooa dispatcher tooroute toohello appropriate actor instance.</span></span>
* <span data-ttu-id="d81b0-109">Provider dello stato Actor Hello esegue il wrapping di provider di stato (ad esempio, i provider di stato raccolte affidabile hello) e fornisce un adattatore per la gestione dello stato actor.</span><span class="sxs-lookup"><span data-stu-id="d81b0-109">hello Actor State Provider wraps state providers (such as hello Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="d81b0-110">Questi framework Reliable Actor hello formano i componenti.</span><span class="sxs-lookup"><span data-stu-id="d81b0-110">These components together form hello Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="d81b0-111">Livelli del servizio</span><span class="sxs-lookup"><span data-stu-id="d81b0-111">Service layering</span></span>
<span data-ttu-id="d81b0-112">Poiché hello attore servizio è un servizio affidabile, tutti hello [modello di applicazione](service-fabric-application-model.md), ciclo di vita, [imballaggio](service-fabric-package-apps.md), [distribuzione](service-fabric-deploy-remove-applications.md), eseguire l'aggiornamento e scalabilità e concetti di Servizi affidabili applicano hello stessi servizi di tooactor modo.</span><span class="sxs-lookup"><span data-stu-id="d81b0-112">Because hello actor service itself is a reliable service, all hello [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply hello same way tooactor services.</span></span> 

![Livelli del servizio attore][1]

<span data-ttu-id="d81b0-114">Hello diagramma precedente mostra una relazione hello tra Framework di applicazioni di Service Fabric hello e codice utente.</span><span class="sxs-lookup"><span data-stu-id="d81b0-114">hello preceding diagram shows hello relationship between hello Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="d81b0-115">Elementi blu rappresentano framework dell'applicazione hello servizi affidabili, framework Reliable Actor hello arancione e verde rappresenta il codice utente.</span><span class="sxs-lookup"><span data-stu-id="d81b0-115">Blue elements represent hello Reliable Services application framework, orange represents hello Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="d81b0-116">In servizi affidabili, il servizio eredita hello `StatefulService` classe.</span><span class="sxs-lookup"><span data-stu-id="d81b0-116">In Reliable Services, your service inherits hello `StatefulService` class.</span></span> <span data-ttu-id="d81b0-117">Questa classe è a sua volta derivata da `StatefulServiceBase` (o `StatelessService` per i servizi senza stato).</span><span class="sxs-lookup"><span data-stu-id="d81b0-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="d81b0-118">In Reliable Actors, si utilizza servizio actor hello.</span><span class="sxs-lookup"><span data-stu-id="d81b0-118">In Reliable Actors, you use hello actor service.</span></span> <span data-ttu-id="d81b0-119">servizio actor Hello è un'implementazione diversa di hello `StatefulServiceBase` classe motivo implementa hello attore in cui è eseguito gli attori.</span><span class="sxs-lookup"><span data-stu-id="d81b0-119">hello actor service is a different implementation of hello `StatefulServiceBase` class that implements hello actor pattern where your actors run.</span></span> <span data-ttu-id="d81b0-120">Poiché servizio actor hello stesso è solo un'implementazione di `StatefulServiceBase`, è possibile scrivere il proprio servizio che deriva da `ActorService` e implementare le funzionalità di livello di servizio hello stesso modo analogo, quando si eredita `StatefulService`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="d81b0-120">Because hello actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features hello same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="d81b0-121">Backup e ripristino del servizio.</span><span class="sxs-lookup"><span data-stu-id="d81b0-121">Service backup and restore.</span></span>
* <span data-ttu-id="d81b0-122">Funzionalità condivisa per tutti gli attori, ad esempio un interruttore.</span><span class="sxs-lookup"><span data-stu-id="d81b0-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="d81b0-123">Nel servizio actor hello stesso e in ogni attore singole chiamate di procedura remota.</span><span class="sxs-lookup"><span data-stu-id="d81b0-123">Remote procedure calls on hello actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="d81b0-124">I servizi con stato non sono attualmente supportati in Java/Linux.</span><span class="sxs-lookup"><span data-stu-id="d81b0-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-hello-actor-service"></a><span data-ttu-id="d81b0-125">Utilizzo del servizio actor hello</span><span class="sxs-lookup"><span data-stu-id="d81b0-125">Using hello actor service</span></span>
<span data-ttu-id="d81b0-126">Le istanze di attore hanno servizio actor toohello di accesso in cui sono in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d81b0-126">Actor instances have access toohello actor service in which they are running.</span></span> <span data-ttu-id="d81b0-127">Tramite servizio actor hello, istanze attore possono ottenere a livello di codice il contesto di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d81b0-127">Through hello actor service, actor instances can programmatically obtain hello service context.</span></span> <span data-ttu-id="d81b0-128">contesto del servizio Hello con ID di partizione hello, nome del servizio, nome dell'applicazione e altre informazioni specifiche della piattaforma Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="d81b0-128">hello service context has hello partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

```csharp
Task MyActorMethod()
{
    Guid partitionId = this.ActorService.Context.PartitionId;
    string serviceTypeName = this.ActorService.Context.ServiceTypeName;
    Uri serviceInstanceName = this.ActorService.Context.ServiceName;
    string applicationInstanceName = this.ActorService.Context.CodePackageActivationContext.ApplicationName;
}
```
```Java
CompletableFuture<?> MyActorMethod()
{
    UUID partitionId = this.getActorService().getServiceContext().getPartitionId();
    String serviceTypeName = this.getActorService().getServiceContext().getServiceTypeName();
    URI serviceInstanceName = this.getActorService().getServiceContext().getServiceName();
    String applicationInstanceName = this.getActorService().getServiceContext().getCodePackageActivationContext().getApplicationName();
}
```


<span data-ttu-id="d81b0-129">Ad esempio tutti i servizi affidabili, servizio actor hello deve essere registrato con un tipo di servizio nel runtime di Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="d81b0-129">Like all Reliable Services, hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="d81b0-130">Per hello del servizio actor toorun le istanze di attore, anche il tipo di attore deve essere registrato con il servizio actor hello.</span><span class="sxs-lookup"><span data-stu-id="d81b0-130">For hello actor service toorun your actor instances, your actor type must also be registered with hello actor service.</span></span> <span data-ttu-id="d81b0-131">Hello `ActorRuntime` metodo di registrazione, questa operazione viene eseguita per attori.</span><span class="sxs-lookup"><span data-stu-id="d81b0-131">hello `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="d81b0-132">Nel caso più semplice di hello, è possibile registrare solo il tipo di attore e verrà utilizzato in modo implicito servizio actor hello con le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="d81b0-132">In hello simplest case, you can just register your actor type, and hello actor service with default settings will implicitly be used:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>().GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```

<span data-ttu-id="d81b0-133">In alternativa, è possibile utilizzare un'espressione lambda fornita da servizio di registrazione metodo tooconstruct hello actor hello manualmente.</span><span class="sxs-lookup"><span data-stu-id="d81b0-133">Alternatively, you can use a lambda provided by hello registration method tooconstruct hello actor service yourself.</span></span> <span data-ttu-id="d81b0-134">È possibile configurare il servizio di attore hello e costruire in modo esplicito le istanze attore, dove è possibile inserire attore tooyour dipendenze mediante il relativo costruttore:</span><span class="sxs-lookup"><span data-stu-id="d81b0-134">You can then configure hello actor service and explicitly construct your actor instances, where you can inject dependencies tooyour actor through its constructor:</span></span>

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new ActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
static class Program
{
    private static void Main()
    {
      ActorRuntime.registerActorAsync(
              MyActor.class,
              (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
              timeout);

        Thread.sleep(Long.MAX_VALUE);
    }
}
```

### <a name="actor-service-methods"></a><span data-ttu-id="d81b0-135">Metodi del servizio attore</span><span class="sxs-lookup"><span data-stu-id="d81b0-135">Actor service methods</span></span>
<span data-ttu-id="d81b0-136">Hello implementa servizio Actor `IActorService` (c#) o `ActorService` (linguaggio), che a sua volta implementa `IService` (c#) o `Service` (linguaggio).</span><span class="sxs-lookup"><span data-stu-id="d81b0-136">hello Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="d81b0-137">Questo è l'interfaccia di hello utilizzata dalla comunicazione remota di servizi affidabili, che consente chiamate di procedure remote sui metodi di servizio.</span><span class="sxs-lookup"><span data-stu-id="d81b0-137">This is hello interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="d81b0-138">Contiene i metodi a livello di servizio che possono essere chiamati in remoto mediante la comunicazione remota del servizio.</span><span class="sxs-lookup"><span data-stu-id="d81b0-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="d81b0-139">Enumerazione degli attori</span><span class="sxs-lookup"><span data-stu-id="d81b0-139">Enumerating actors</span></span>
<span data-ttu-id="d81b0-140">servizio actor Hello consente al client metadati tooenumerate riguardanti gli attori hello che ospita il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="d81b0-140">hello actor service allows a client tooenumerate metadata about hello actors that hello service is hosting.</span></span> <span data-ttu-id="d81b0-141">Servizio actor hello, in quanto un servizio con stato partizionato, l'enumerazione viene eseguita per ogni partizione.</span><span class="sxs-lookup"><span data-stu-id="d81b0-141">Because hello actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="d81b0-142">In quanto ogni partizione può contenere molti attori, enumerazione hello viene restituito come un set di risultati di paging.</span><span class="sxs-lookup"><span data-stu-id="d81b0-142">Because each partition might contain many actors, hello enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="d81b0-143">pagine Hello vengono eseguite su fino a quando tutte le pagine vengono lette.</span><span class="sxs-lookup"><span data-stu-id="d81b0-143">hello pages are looped over until all pages are read.</span></span> <span data-ttu-id="d81b0-144">Hello seguente esempio viene illustrato come un elenco di tutti gli attori attivi di una partizione di un servizio actor toocreate:</span><span class="sxs-lookup"><span data-stu-id="d81b0-144">hello following example shows how toocreate a list of all active actors in one partition of an actor service:</span></span>

```csharp
IActorService actorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new List<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = await actorServiceProxy.GetActorsAsync(continuationToken, cancellationToken);

    activeActors.AddRange(page.Items.Where(x => x.IsActive));

    continuationToken = page.ContinuationToken;
}
while (continuationToken != null);
```

```Java
ActorService actorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new ArrayList<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = actorServiceProxy.getActorsAsync(continuationToken);

    while(ActorInformation x: page.getItems())
    {
         if(x.isActive()){
              activeActors.add(x);
         }
    }

    continuationToken = page.getContinuationToken();
}
while (continuationToken != null);
```

#### <a name="deleting-actors"></a><span data-ttu-id="d81b0-145">Eliminazione di attori</span><span class="sxs-lookup"><span data-stu-id="d81b0-145">Deleting actors</span></span>
<span data-ttu-id="d81b0-146">servizio actor Hello offre anche una funzione per l'eliminazione di attori:</span><span class="sxs-lookup"><span data-stu-id="d81b0-146">hello actor service also provides a function for deleting actors:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="d81b0-147">Per ulteriori informazioni sull'eliminazione di attori e il relativo stato, vedere hello [documentazione del ciclo di vita attore](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="d81b0-147">For more information on deleting actors and their state, see hello [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="d81b0-148">Servizio attore personalizzato</span><span class="sxs-lookup"><span data-stu-id="d81b0-148">Custom actor service</span></span>
<span data-ttu-id="d81b0-149">Utilizzando lambda di hello attore registrazione, è possibile registrare il proprio servizio actor personalizzata che deriva da `ActorService` (c#) e `FabricActorService` (linguaggio).</span><span class="sxs-lookup"><span data-stu-id="d81b0-149">By using hello actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="d81b0-150">In questo servizio attore personalizzato è possibile implementare funzionalità di livello di servizio scrivendo una classe di servizio che eredita `ActorService` (C#) o `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="d81b0-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="d81b0-151">Un servizio actor personalizzata eredita tutte le funzionalità di runtime attore hello dalla `ActorService` (c#) o `FabricActorService` (linguaggio) e possono essere utilizzati tooimplement i propri metodi di servizio.</span><span class="sxs-lookup"><span data-stu-id="d81b0-151">A custom actor service inherits all hello actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used tooimplement your own service methods.</span></span>

```csharp
class MyActorService : ActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }
}
```
```Java
class MyActorService extends FabricActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, BiFunction<FabricActorService, ActorId, ActorBase> newActor)
    {
         super(context, typeInfo, newActor);
    }
}
```

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new MyActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
        Thread.sleep(Long.MAX_VALUE);
    }
}
```

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="d81b0-152">Implementazione del backup e ripristino dell'attore</span><span class="sxs-lookup"><span data-stu-id="d81b0-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="d81b0-153">Nell'esempio seguente di hello, servizio actor personalizzata hello espone tooback un metodo dei dati attore sfruttando del listener di comunicazione remota di hello già presenti nel `ActorService`:</span><span class="sxs-lookup"><span data-stu-id="d81b0-153">In hello following example, hello custom actor service exposes a method tooback up actor data by taking advantage of hello remoting listener already present in `ActorService`:</span></span>

```csharp
public interface IMyActorService : IService
{
    Task BackupActorsAsync();
}

class MyActorService : ActorService, IMyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }

    public Task BackupActorsAsync()
    {
        return this.BackupAsync(new BackupDescription(PerformBackupAsync));
    }

    private async Task<bool> PerformBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           Directory.Delete(backupInfo.Directory, recursive: true);
        }
    }
}
```
```Java
public interface MyActorService extends Service
{
    CompletableFuture<?> backupActorsAsync();
}

class MyActorServiceImpl extends ActorService implements MyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<FabricActorService, ActorId, ActorBase> newActor)
    {
       super(context, typeInfo, newActor);
    }

    public CompletableFuture backupActorsAsync()
    {
        return this.backupAsync(new BackupDescription((backupInfo, cancellationToken) -> performBackupAsync(backupInfo, cancellationToken)));
    }

    private CompletableFuture<Boolean> performBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           deleteDirectory(backupInfo.Directory)
        }
    }

    void deleteDirectory(File file) {
        File[] contents = file.listFiles();
        if (contents != null) {
            for (File f : contents) {
               deleteDirectory(f);
             }
        }
        file.delete();
    }
}
```


<span data-ttu-id="d81b0-154">In questo esempio `IMyActorService` è un contratto di comunicazione remota che implementa `IService` (C#) and `Service` (Java) e viene successivamente implementato da `MyActorService`.</span><span class="sxs-lookup"><span data-stu-id="d81b0-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="d81b0-155">Aggiungere questo contratto di servizi remoti, i metodi per `IMyActorService` sono ora disponibili tooa client mediante la creazione di un proxy remoto tramite `ActorServiceProxy`:</span><span class="sxs-lookup"><span data-stu-id="d81b0-155">By adding this remoting contract, methods on `IMyActorService` are now also available tooa client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

```csharp
IMyActorService myActorServiceProxy = ActorServiceProxy.Create<IMyActorService>(
    new Uri("fabric:/MyApp/MyService"), ActorId.CreateRandom());

await myActorServiceProxy.BackupActorsAsync();
```
```Java
MyActorService myActorServiceProxy = ActorServiceProxy.create(MyActorService.class,
    new URI("fabric:/MyApp/MyService"), actorId);

myActorServiceProxy.backupActorsAsync();
```

## <a name="application-model"></a><span data-ttu-id="d81b0-156">Modello di applicazione</span><span class="sxs-lookup"><span data-stu-id="d81b0-156">Application model</span></span>
<span data-ttu-id="d81b0-157">Servizi Actor sono servizi affidabili, pertanto il modello di applicazione hello è hello stesso.</span><span class="sxs-lookup"><span data-stu-id="d81b0-157">Actor services are Reliable Services, so hello application model is hello same.</span></span> <span data-ttu-id="d81b0-158">Tuttavia, gli strumenti di compilazione hello attore framework generano alcuni dei file di modello di applicazione hello di.</span><span class="sxs-lookup"><span data-stu-id="d81b0-158">However, hello actor framework build tools generate some of hello application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="d81b0-159">Manifesto del servizio</span><span class="sxs-lookup"><span data-stu-id="d81b0-159">Service manifest</span></span>
<span data-ttu-id="d81b0-160">strumenti di compilazione Hello attore framework generare automaticamente il contenuto di hello del file ServiceManifest.xml del servizio actor.</span><span class="sxs-lookup"><span data-stu-id="d81b0-160">hello actor framework build tools automatically generate hello contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="d81b0-161">Questo file include:</span><span class="sxs-lookup"><span data-stu-id="d81b0-161">This file includes:</span></span>

* <span data-ttu-id="d81b0-162">Tipo del servizio attore.</span><span class="sxs-lookup"><span data-stu-id="d81b0-162">Actor service type.</span></span> <span data-ttu-id="d81b0-163">nome del tipo Hello viene generato in base al nome di progetto dell'attore.</span><span class="sxs-lookup"><span data-stu-id="d81b0-163">hello type name is generated based on your actor's project name.</span></span> <span data-ttu-id="d81b0-164">In base all'attributo di persistenza di hello nell'attore, hello HasPersistedState flag viene impostato anche di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="d81b0-164">Based on hello persistence attribute on your actor, hello HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="d81b0-165">Pacchetto di codice.</span><span class="sxs-lookup"><span data-stu-id="d81b0-165">Code package.</span></span>
* <span data-ttu-id="d81b0-166">Pacchetto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="d81b0-166">Config package.</span></span>
* <span data-ttu-id="d81b0-167">Risorse ed endpoint.</span><span class="sxs-lookup"><span data-stu-id="d81b0-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="d81b0-168">Manifesto dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="d81b0-168">Application manifest</span></span>
<span data-ttu-id="d81b0-169">strumenti di compilazione Hello attore framework creano automaticamente una definizione di servizio predefinito per il servizio actor.</span><span class="sxs-lookup"><span data-stu-id="d81b0-169">hello actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="d81b0-170">strumenti di compilazione Hello popolano le proprietà del servizio di hello predefinite:</span><span class="sxs-lookup"><span data-stu-id="d81b0-170">hello build tools populate hello default service properties:</span></span>

* <span data-ttu-id="d81b0-171">Numero di set di repliche è determinato dall'attributo persistenza hello l'attore.</span><span class="sxs-lookup"><span data-stu-id="d81b0-171">Replica set count is determined by hello persistence attribute on your actor.</span></span> <span data-ttu-id="d81b0-172">Ogni attributo persistenza hello ora l'attore viene modificato, numero di set di repliche hello nella definizione di servizio predefinito hello viene reimpostato di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="d81b0-172">Each time hello persistence attribute on your actor is changed, hello replica set count in hello default service definition is reset accordingly.</span></span>
* <span data-ttu-id="d81b0-173">Intervallo e lo schema di partizione vengono impostati tooUniform Int64 con hello completo Int64 intervalli di chiavi.</span><span class="sxs-lookup"><span data-stu-id="d81b0-173">Partition scheme and range are set tooUniform Int64 with hello full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="d81b0-174">Concetti relativi alla partizione di Service Fabric per gli attori</span><span class="sxs-lookup"><span data-stu-id="d81b0-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="d81b0-175">I servizi Actor sono servizi con stato partizionati.</span><span class="sxs-lookup"><span data-stu-id="d81b0-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="d81b0-176">Ogni partizione di un servizio Actor contiene un set di attori.</span><span class="sxs-lookup"><span data-stu-id="d81b0-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="d81b0-177">Le partizioni del servizio vengono distribuite automaticamente su più nodi in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d81b0-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="d81b0-178">Le istanze degli attori vengono distribuite di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="d81b0-178">Actor instances are distributed as a result.</span></span>

![Partizionamento e distribuzione degli attori][5]

<span data-ttu-id="d81b0-180">È possibile creare servizi Reliable Services con schemi di partizione e intervalli di chiavi di partizione diversi.</span><span class="sxs-lookup"><span data-stu-id="d81b0-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="d81b0-181">servizio actor Hello Usa lo schema di partizionamento Int64 hello con toopartitions toomap di intervalli di chiavi di hello completo Int64 attori.</span><span class="sxs-lookup"><span data-stu-id="d81b0-181">hello actor service uses hello Int64 partitioning scheme with hello full Int64 key range toomap actors toopartitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="d81b0-182">ID attore</span><span class="sxs-lookup"><span data-stu-id="d81b0-182">Actor ID</span></span>
<span data-ttu-id="d81b0-183">Ogni attore che viene creata nel servizio hello ha un ID univoco associato, rappresentato da hello `ActorId` classe.</span><span class="sxs-lookup"><span data-stu-id="d81b0-183">Each actor that's created in hello service has a unique ID associated with it, represented by hello `ActorId` class.</span></span> <span data-ttu-id="d81b0-184">`ActorId`è un valore di ID opaco che può essere utilizzato per la distribuzione uniforme degli attori tra partizioni servizio hello tramite la generazione degli ID casuali:</span><span class="sxs-lookup"><span data-stu-id="d81b0-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across hello service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="d81b0-185">Ogni `ActorId` è stato eseguito l'hashing tooan Int64.</span><span class="sxs-lookup"><span data-stu-id="d81b0-185">Every `ActorId` is hashed tooan Int64.</span></span> <span data-ttu-id="d81b0-186">Ecco perché servizio actor hello è necessario utilizzare uno schema di partizionamento Int64 con hello completo Int64 intervalli di chiavi.</span><span class="sxs-lookup"><span data-stu-id="d81b0-186">This is why hello actor service must use an Int64 partitioning scheme with hello full Int64 key range.</span></span> <span data-ttu-id="d81b0-187">È comunque possibile usare valori ID personalizzati per un `ActorID`, tra cui GUID/UUID, stringhe e Int64.</span><span class="sxs-lookup"><span data-stu-id="d81b0-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

```csharp
ActorProxy.Create<IMyActor>(new ActorId(Guid.NewGuid()));
ActorProxy.Create<IMyActor>(new ActorId("myActorId"));
ActorProxy.Create<IMyActor>(new ActorId(1234));
```
```Java
ActorProxyBase.create(MyActor.class, new ActorId(UUID.randomUUID()));
ActorProxyBase.create(MyActor.class, new ActorId("myActorId"));
ActorProxyBase.create(MyActor.class, new ActorId(1234));
```

<span data-ttu-id="d81b0-188">Quando si utilizza GUID/UUID e stringhe, i valori hello sono con hash tooan Int64.</span><span class="sxs-lookup"><span data-stu-id="d81b0-188">When you're using GUIDs/UUIDs and strings, hello values are hashed tooan Int64.</span></span> <span data-ttu-id="d81b0-189">Tuttavia, quando si in modo esplicito forniscono un tooan Int64 `ActorId`, hello Int64 verrà eseguito il mapping direttamente tooa partizione senza ulteriore hash.</span><span class="sxs-lookup"><span data-stu-id="d81b0-189">However, when you're explicitly providing an Int64 tooan `ActorId`, hello Int64 will map directly tooa partition without further hashing.</span></span> <span data-ttu-id="d81b0-190">È possibile utilizzare questa tecnica toocontrol cui attori hello partizione vengono inseriti in.</span><span class="sxs-lookup"><span data-stu-id="d81b0-190">You can use this technique toocontrol which partition hello actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d81b0-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d81b0-191">Next steps</span></span>
* [<span data-ttu-id="d81b0-192">Gestione dello stato degli attori</span><span class="sxs-lookup"><span data-stu-id="d81b0-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="d81b0-193">Ciclo di vita degli attori e Garbage Collection</span><span class="sxs-lookup"><span data-stu-id="d81b0-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="d81b0-194">Documentazione di riferimento delle API di Actors</span><span class="sxs-lookup"><span data-stu-id="d81b0-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="d81b0-195">Codice di esempio .NET</span><span class="sxs-lookup"><span data-stu-id="d81b0-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="d81b0-196">Codice di esempio Java</span><span class="sxs-lookup"><span data-stu-id="d81b0-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
