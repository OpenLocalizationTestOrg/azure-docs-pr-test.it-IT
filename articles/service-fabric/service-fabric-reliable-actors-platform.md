---
title: Reliable Actors in Service Fabric | Documentazione Microsoft
description: "Descrive come Reliable Actors si sovrappone a Reliable Services e usa le funzionalità della piattaforma Service Fabric."
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
ms.openlocfilehash: 0a12da52b6e74c721cd25f89e7cde3c07153a396
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-reliable-actors-use-the-service-fabric-platform"></a><span data-ttu-id="4364b-103">Modalità d'uso della piattaforma Service Fabric da parte di Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="4364b-103">How Reliable Actors use the Service Fabric platform</span></span>
<span data-ttu-id="4364b-104">Questo articolo descrive il funzionamento di Reliable Actors sulla piattaforma Service Fabric di Azure.</span><span class="sxs-lookup"><span data-stu-id="4364b-104">This article explains how Reliable Actors work on the Azure Service Fabric platform.</span></span> <span data-ttu-id="4364b-105">Reliable Actors viene eseguito in un framework ospitato in un'implementazione di un servizio Reliable Services con stato denominato *servizio attore*.</span><span class="sxs-lookup"><span data-stu-id="4364b-105">Reliable Actors run in a framework that is hosted in an implementation of a stateful reliable service called the *actor service*.</span></span> <span data-ttu-id="4364b-106">Il servizio attore contiene tutti i componenti necessari per gestire il ciclo di vita e l'invio di messaggi per gli attori:</span><span class="sxs-lookup"><span data-stu-id="4364b-106">The actor service contains all the components necessary to manage the lifecycle and message dispatching for your actors:</span></span>

* <span data-ttu-id="4364b-107">Il runtime di Actors gestisce il ciclo di vita e la Garbage Collection e applica l'accesso a thread singolo.</span><span class="sxs-lookup"><span data-stu-id="4364b-107">The Actor Runtime manages lifecycle, garbage collection, and enforces single-threaded access.</span></span>
* <span data-ttu-id="4364b-108">Un listener di comunicazione remota del servizio Actor accetta chiamate di accesso remoto per gli attori e le invia a un dispatcher per l'indirizzamento all'istanza d attore appropriata.</span><span class="sxs-lookup"><span data-stu-id="4364b-108">An actor service remoting listener accepts remote access calls to actors and sends them to a dispatcher to route to the appropriate actor instance.</span></span>
* <span data-ttu-id="4364b-109">Il provider di stato degli attori esegue il wrapping dei provider di stato (come il provider di stato Reliable Collections) e fornisce un adattatore per la gestione dello stato degli attori.</span><span class="sxs-lookup"><span data-stu-id="4364b-109">The Actor State Provider wraps state providers (such as the Reliable Collections state provider) and provides an adapter for actor state management.</span></span>

<span data-ttu-id="4364b-110">Questi componenti insieme costituiscono il framework Reliable Actors.</span><span class="sxs-lookup"><span data-stu-id="4364b-110">These components together form the Reliable Actor framework.</span></span>

## <a name="service-layering"></a><span data-ttu-id="4364b-111">Livelli del servizio</span><span class="sxs-lookup"><span data-stu-id="4364b-111">Service layering</span></span>
<span data-ttu-id="4364b-112">Dato che il servizio attore stesso è un servizio Reliable Services, tutti i concetti di [modello applicativo](service-fabric-application-model.md), ciclo di vita, [creazione pacchetti](service-fabric-package-apps.md), [distribuzione](service-fabric-deploy-remove-applications.md), aggiornamento e ridimensionamento validi per Reliable Services si applicano anche ai servizi attore.</span><span class="sxs-lookup"><span data-stu-id="4364b-112">Because the actor service itself is a reliable service, all the [application model](service-fabric-application-model.md), lifecycle, [packaging](service-fabric-package-apps.md), [deployment](service-fabric-deploy-remove-applications.md), upgrade, and scaling concepts of Reliable Services apply the same way to actor services.</span></span> 

![Livelli del servizio attore][1]

<span data-ttu-id="4364b-114">Il diagramma precedente mostra la relazione tra i framework applicativi di Service Fabric e il codice utente.</span><span class="sxs-lookup"><span data-stu-id="4364b-114">The preceding diagram shows the relationship between the Service Fabric application frameworks and user code.</span></span> <span data-ttu-id="4364b-115">Gli elementi blu rappresentano il framework applicativo di Reliable Services, quelli arancioni il framework Reliable Actors e quelli verdi il codice utente.</span><span class="sxs-lookup"><span data-stu-id="4364b-115">Blue elements represent the Reliable Services application framework, orange represents the Reliable Actor framework, and green represents user code.</span></span>

<span data-ttu-id="4364b-116">In Reliable Services il servizio eredita la classe `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="4364b-116">In Reliable Services, your service inherits the `StatefulService` class.</span></span> <span data-ttu-id="4364b-117">Questa classe è a sua volta derivata da `StatefulServiceBase` (o `StatelessService` per i servizi senza stato).</span><span class="sxs-lookup"><span data-stu-id="4364b-117">This class is itself derived from `StatefulServiceBase` (or `StatelessService` for stateless services).</span></span> <span data-ttu-id="4364b-118">In Reliable Actors usare il servizio attore.</span><span class="sxs-lookup"><span data-stu-id="4364b-118">In Reliable Actors, you use the actor service.</span></span> <span data-ttu-id="4364b-119">Il servizio attore è un'implementazione diversa della classe `StatefulServiceBase` che implementa lo schema dell'attore in cui vengono eseguiti gli attori.</span><span class="sxs-lookup"><span data-stu-id="4364b-119">The actor service is a different implementation of the `StatefulServiceBase` class that implements the actor pattern where your actors run.</span></span> <span data-ttu-id="4364b-120">Dato che il servizio attore è semplicemente un'implementazione di `StatefulServiceBase`, si può scrivere il proprio servizio che deriva da `ActorService` e implementare le funzionalità a livello di servizio così come si farebbe quando si eredita `StatefulService`, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4364b-120">Because the actor service itself is just an implementation of `StatefulServiceBase`, you can write your own service that derives from `ActorService` and implement service-level features the same way you would when inheriting `StatefulService`, such as:</span></span>

* <span data-ttu-id="4364b-121">Backup e ripristino del servizio.</span><span class="sxs-lookup"><span data-stu-id="4364b-121">Service backup and restore.</span></span>
* <span data-ttu-id="4364b-122">Funzionalità condivisa per tutti gli attori, ad esempio un interruttore.</span><span class="sxs-lookup"><span data-stu-id="4364b-122">Shared functionality for all actors, for example, a circuit breaker.</span></span>
* <span data-ttu-id="4364b-123">Chiamate di routine remote sul servizio attore stesso e su ogni singolo attore.</span><span class="sxs-lookup"><span data-stu-id="4364b-123">Remote procedure calls on the actor service itself and on each individual actor.</span></span>

> [!NOTE]
> <span data-ttu-id="4364b-124">I servizi con stato non sono attualmente supportati in Java/Linux.</span><span class="sxs-lookup"><span data-stu-id="4364b-124">Stateful services are not currently supported in Java/Linux.</span></span>

### <a name="using-the-actor-service"></a><span data-ttu-id="4364b-125">Uso del servizio attore</span><span class="sxs-lookup"><span data-stu-id="4364b-125">Using the actor service</span></span>
<span data-ttu-id="4364b-126">Le istanze degli attori hanno accesso al servizio attore in cui sono in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4364b-126">Actor instances have access to the actor service in which they are running.</span></span> <span data-ttu-id="4364b-127">Tramite il servizio attore, le istanze degli attori possono ottenere il contesto del servizio a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="4364b-127">Through the actor service, actor instances can programmatically obtain the service context.</span></span> <span data-ttu-id="4364b-128">Il contesto del servizio include l'ID partizione, il nome del servizio, il nome dell'applicazione e altre informazioni specifiche sulla piattaforma Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="4364b-128">The service context has the partition ID, service name, application name, and other Service Fabric platform-specific information:</span></span>

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


<span data-ttu-id="4364b-129">Come tutti i servizi Reliable Services, il servizio attore deve essere registrato con un tipo di servizio nel runtime di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4364b-129">Like all Reliable Services, the actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="4364b-130">Perché il servizio attore possa eseguire le istanze degli attori, è necessario che anche il proprio tipo di attore sia registrato con il servizio attore.</span><span class="sxs-lookup"><span data-stu-id="4364b-130">For the actor service to run your actor instances, your actor type must also be registered with the actor service.</span></span> <span data-ttu-id="4364b-131">Il metodo di registrazione `ActorRuntime` esegue questa attività per gli attori.</span><span class="sxs-lookup"><span data-stu-id="4364b-131">The `ActorRuntime` registration method performs this work for actors.</span></span> <span data-ttu-id="4364b-132">Nel caso più semplice, è sufficiente registrare il tipo di attore e verrà usato implicitamente il servizio attore con le impostazioni predefinite:</span><span class="sxs-lookup"><span data-stu-id="4364b-132">In the simplest case, you can just register your actor type, and the actor service with default settings will implicitly be used:</span></span>

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

<span data-ttu-id="4364b-133">In alternativa, è possibile usare un'espressione lambda fornita dal metodo di registrazione per creare manualmente il servizio attore.</span><span class="sxs-lookup"><span data-stu-id="4364b-133">Alternatively, you can use a lambda provided by the registration method to construct the actor service yourself.</span></span> <span data-ttu-id="4364b-134">È possibile perciò configurare il servizio attore e costruire esplicitamente le istanze degli attori, in cui possono essere inserite le dipendenze per l'attore mediante il relativo costruttore:</span><span class="sxs-lookup"><span data-stu-id="4364b-134">You can then configure the actor service and explicitly construct your actor instances, where you can inject dependencies to your actor through its constructor:</span></span>

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

### <a name="actor-service-methods"></a><span data-ttu-id="4364b-135">Metodi del servizio attore</span><span class="sxs-lookup"><span data-stu-id="4364b-135">Actor service methods</span></span>
<span data-ttu-id="4364b-136">Il servizio attore implementa `IActorService` (C#) o `ActorService` (Java), che a sua volta implementa `IService` (C#) o `Service` (Java).</span><span class="sxs-lookup"><span data-stu-id="4364b-136">The Actor service implements `IActorService` (C#) or `ActorService` (Java), which in turn implements `IService` (C#) or `Service` (Java).</span></span> <span data-ttu-id="4364b-137">Questo è l'interfaccia usata dalla comunicazione remota di Reliable Services, che consente le chiamate RPC sui metodi del servizio.</span><span class="sxs-lookup"><span data-stu-id="4364b-137">This is the interface used by Reliable Services remoting, which allows remote procedure calls on service methods.</span></span> <span data-ttu-id="4364b-138">Contiene i metodi a livello di servizio che possono essere chiamati in remoto mediante la comunicazione remota del servizio.</span><span class="sxs-lookup"><span data-stu-id="4364b-138">It contains service-level methods that can be called remotely via service remoting.</span></span>

#### <a name="enumerating-actors"></a><span data-ttu-id="4364b-139">Enumerazione degli attori</span><span class="sxs-lookup"><span data-stu-id="4364b-139">Enumerating actors</span></span>
<span data-ttu-id="4364b-140">Il servizio attore consente al client di enumerare i metadati relativi agli attori ospitati dal servizio.</span><span class="sxs-lookup"><span data-stu-id="4364b-140">The actor service allows a client to enumerate metadata about the actors that the service is hosting.</span></span> <span data-ttu-id="4364b-141">Dato che il servizio attore è un servizio con stato partizionato, l'enumerazione viene eseguita per partizione.</span><span class="sxs-lookup"><span data-stu-id="4364b-141">Because the actor service is a partitioned stateful service, enumeration is performed per partition.</span></span> <span data-ttu-id="4364b-142">Poiché ogni partizione può contenere molti attori, l'enumerazione viene restituita come set di risultati a pagine.</span><span class="sxs-lookup"><span data-stu-id="4364b-142">Because each partition might contain many actors, the enumeration is returned as a set of paged results.</span></span> <span data-ttu-id="4364b-143">Le pagine vengono esaminate in ciclo fino a quando non vengono lette tutte.</span><span class="sxs-lookup"><span data-stu-id="4364b-143">The pages are looped over until all pages are read.</span></span> <span data-ttu-id="4364b-144">L'esempio seguente illustra come creare un elenco di tutti gli attori attivi in una partizione di un servizio Actor:</span><span class="sxs-lookup"><span data-stu-id="4364b-144">The following example shows how to create a list of all active actors in one partition of an actor service:</span></span>

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

#### <a name="deleting-actors"></a><span data-ttu-id="4364b-145">Eliminazione di attori</span><span class="sxs-lookup"><span data-stu-id="4364b-145">Deleting actors</span></span>
<span data-ttu-id="4364b-146">Il servizio attore fornisce anche una funzione per l'eliminazione degli attori:</span><span class="sxs-lookup"><span data-stu-id="4364b-146">The actor service also provides a function for deleting actors:</span></span>

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

<span data-ttu-id="4364b-147">Per altre informazioni sull'eliminazione degli attori e il relativo stato, vedere la [documentazione sul ciclo di vita degli attori](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="4364b-147">For more information on deleting actors and their state, see the [actor lifecycle documentation](service-fabric-reliable-actors-lifecycle.md).</span></span>

### <a name="custom-actor-service"></a><span data-ttu-id="4364b-148">Servizio attore personalizzato</span><span class="sxs-lookup"><span data-stu-id="4364b-148">Custom actor service</span></span>
<span data-ttu-id="4364b-149">Usando l'espressione lambda di registrazione dell'attore è possibile registrare il proprio servizio attore personalizzato che deriva da `ActorService` (C#) e `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="4364b-149">By using the actor registration lambda, you can register your own custom actor service that derives from `ActorService` (C#) and `FabricActorService` (Java).</span></span> <span data-ttu-id="4364b-150">In questo servizio attore personalizzato è possibile implementare funzionalità di livello di servizio scrivendo una classe di servizio che eredita `ActorService` (C#) o `FabricActorService` (Java).</span><span class="sxs-lookup"><span data-stu-id="4364b-150">In this custom actor service, you can implement your own service-level functionality by writing a service class that inherits `ActorService` (C#) or `FabricActorService` (Java).</span></span> <span data-ttu-id="4364b-151">Un servizio attore personalizzato eredita tutte le funzionalità di runtime dell'attore da `ActorService` (C#) o `FabricActorService` (Java) e può essere usato per implementare i propri metodi del servizio.</span><span class="sxs-lookup"><span data-stu-id="4364b-151">A custom actor service inherits all the actor runtime functionality from `ActorService` (C#) or `FabricActorService` (Java) and can be used to implement your own service methods.</span></span>

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

#### <a name="implementing-actor-backup-and-restore"></a><span data-ttu-id="4364b-152">Implementazione del backup e ripristino dell'attore</span><span class="sxs-lookup"><span data-stu-id="4364b-152">Implementing actor backup and restore</span></span>
 <span data-ttu-id="4364b-153">Nell'esempio seguente il servizio attore personalizzato espone un metodo per il backup dei dati dell'attore sfruttando il listener di comunicazione remota già presente in `ActorService`:</span><span class="sxs-lookup"><span data-stu-id="4364b-153">In the following example, the custom actor service exposes a method to back up actor data by taking advantage of the remoting listener already present in `ActorService`:</span></span>

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
           // store the contents of backupInfo.Directory
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
           // store the contents of backupInfo.Directory
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


<span data-ttu-id="4364b-154">In questo esempio `IMyActorService` è un contratto di comunicazione remota che implementa `IService` (C#) and `Service` (Java) e viene successivamente implementato da `MyActorService`.</span><span class="sxs-lookup"><span data-stu-id="4364b-154">In this example, `IMyActorService` is a remoting contract that implements `IService` (C#) and `Service` (Java), and is then implemented by `MyActorService`.</span></span> <span data-ttu-id="4364b-155">Aggiungendo questo contratto di comunicazione remota, i metodi su `IMyActorService` ora sono disponibili anche per un client attraverso la creazione di un proxy di comunicazione remota mediante `ActorServiceProxy`:</span><span class="sxs-lookup"><span data-stu-id="4364b-155">By adding this remoting contract, methods on `IMyActorService` are now also available to a client by creating a remoting proxy via `ActorServiceProxy`:</span></span>

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

## <a name="application-model"></a><span data-ttu-id="4364b-156">Modello di applicazione</span><span class="sxs-lookup"><span data-stu-id="4364b-156">Application model</span></span>
<span data-ttu-id="4364b-157">I servizi Actor sono servizi Reliable Services, per cui il modello applicativo è lo stesso.</span><span class="sxs-lookup"><span data-stu-id="4364b-157">Actor services are Reliable Services, so the application model is the same.</span></span> <span data-ttu-id="4364b-158">Tuttavia, gli strumenti di compilazione del framework attore generano automaticamente alcuni dei file del modello applicativo.</span><span class="sxs-lookup"><span data-stu-id="4364b-158">However, the actor framework build tools generate some of the application model files for you.</span></span>

### <a name="service-manifest"></a><span data-ttu-id="4364b-159">Manifesto del servizio</span><span class="sxs-lookup"><span data-stu-id="4364b-159">Service manifest</span></span>
<span data-ttu-id="4364b-160">Gli strumenti di compilazione del framework attore generano automaticamente il contenuto del file ServiceManifest.xml del servizio attore.</span><span class="sxs-lookup"><span data-stu-id="4364b-160">The actor framework build tools automatically generate the contents of your actor service's ServiceManifest.xml file.</span></span> <span data-ttu-id="4364b-161">Questo file include:</span><span class="sxs-lookup"><span data-stu-id="4364b-161">This file includes:</span></span>

* <span data-ttu-id="4364b-162">Tipo del servizio attore.</span><span class="sxs-lookup"><span data-stu-id="4364b-162">Actor service type.</span></span> <span data-ttu-id="4364b-163">Il nome del tipo viene generato in base al nome del progetto attore.</span><span class="sxs-lookup"><span data-stu-id="4364b-163">The type name is generated based on your actor's project name.</span></span> <span data-ttu-id="4364b-164">In base all'attributo di persistenza nell'attore, viene impostato anche il flag HasPersistedState.</span><span class="sxs-lookup"><span data-stu-id="4364b-164">Based on the persistence attribute on your actor, the HasPersistedState flag is also set accordingly.</span></span>
* <span data-ttu-id="4364b-165">Pacchetto di codice.</span><span class="sxs-lookup"><span data-stu-id="4364b-165">Code package.</span></span>
* <span data-ttu-id="4364b-166">Pacchetto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="4364b-166">Config package.</span></span>
* <span data-ttu-id="4364b-167">Risorse ed endpoint.</span><span class="sxs-lookup"><span data-stu-id="4364b-167">Resources and endpoints.</span></span>

### <a name="application-manifest"></a><span data-ttu-id="4364b-168">Manifesto dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="4364b-168">Application manifest</span></span>
<span data-ttu-id="4364b-169">Gli strumenti di compilazione del framework attore creano automaticamente una definizione del servizio predefinito per il servizio Actor.</span><span class="sxs-lookup"><span data-stu-id="4364b-169">The actor framework build tools automatically create a default service definition for your actor service.</span></span> <span data-ttu-id="4364b-170">Gli strumenti di compilazione popolano le proprietà del servizio predefinito:</span><span class="sxs-lookup"><span data-stu-id="4364b-170">The build tools populate the default service properties:</span></span>

* <span data-ttu-id="4364b-171">Il numero di set di repliche è determinato dall'attributo di persistenza sull'attore.</span><span class="sxs-lookup"><span data-stu-id="4364b-171">Replica set count is determined by the persistence attribute on your actor.</span></span> <span data-ttu-id="4364b-172">Ogni volta che viene modificato l'attributo di persistenza nell'attore, viene reimpostato di conseguenza il numero di set di repliche nella definizione del servizio predefinito.</span><span class="sxs-lookup"><span data-stu-id="4364b-172">Each time the persistence attribute on your actor is changed, the replica set count in the default service definition is reset accordingly.</span></span>
* <span data-ttu-id="4364b-173">Lo schema e l'intervallo della partizione vengono impostati su Uniform Int64 con l'intervallo di chiavi Int64 completo.</span><span class="sxs-lookup"><span data-stu-id="4364b-173">Partition scheme and range are set to Uniform Int64 with the full Int64 key range.</span></span>

## <a name="service-fabric-partition-concepts-for-actors"></a><span data-ttu-id="4364b-174">Concetti relativi alla partizione di Service Fabric per gli attori</span><span class="sxs-lookup"><span data-stu-id="4364b-174">Service Fabric partition concepts for actors</span></span>
<span data-ttu-id="4364b-175">I servizi Actor sono servizi con stato partizionati.</span><span class="sxs-lookup"><span data-stu-id="4364b-175">Actor services are partitioned stateful services.</span></span> <span data-ttu-id="4364b-176">Ogni partizione di un servizio Actor contiene un set di attori.</span><span class="sxs-lookup"><span data-stu-id="4364b-176">Each partition of an actor service contains a set of actors.</span></span> <span data-ttu-id="4364b-177">Le partizioni del servizio vengono distribuite automaticamente su più nodi in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4364b-177">Service partitions are automatically distributed over multiple nodes in Service Fabric.</span></span> <span data-ttu-id="4364b-178">Le istanze degli attori vengono distribuite di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="4364b-178">Actor instances are distributed as a result.</span></span>

![Partizionamento e distribuzione degli attori][5]

<span data-ttu-id="4364b-180">È possibile creare servizi Reliable Services con schemi di partizione e intervalli di chiavi di partizione diversi.</span><span class="sxs-lookup"><span data-stu-id="4364b-180">Reliable Services can be created with different partition schemes and partition key ranges.</span></span> <span data-ttu-id="4364b-181">Il servizio attore usa lo schema di partizionamento Int64 con l'intervallo di chiavi Int64 completo per mappare gli attori alle partizioni.</span><span class="sxs-lookup"><span data-stu-id="4364b-181">The actor service uses the Int64 partitioning scheme with the full Int64 key range to map actors to partitions.</span></span>

### <a name="actor-id"></a><span data-ttu-id="4364b-182">ID attore</span><span class="sxs-lookup"><span data-stu-id="4364b-182">Actor ID</span></span>
<span data-ttu-id="4364b-183">A ogni attore creato nel servizio è associato un ID univoco, rappresentato dalla classe `ActorId` .</span><span class="sxs-lookup"><span data-stu-id="4364b-183">Each actor that's created in the service has a unique ID associated with it, represented by the `ActorId` class.</span></span> <span data-ttu-id="4364b-184">`ActorId` è un valore ID opaco che può essere usato per la distribuzione uniforme degli attori nelle partizioni del servizio mediante la generazione di ID casuali:</span><span class="sxs-lookup"><span data-stu-id="4364b-184">`ActorId` is an opaque ID value that can be used for uniform distribution of actors across the service partitions by generating random IDs:</span></span>

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


<span data-ttu-id="4364b-185">Di ogni `ActorId` viene eseguito l'hashing in un Int64.</span><span class="sxs-lookup"><span data-stu-id="4364b-185">Every `ActorId` is hashed to an Int64.</span></span> <span data-ttu-id="4364b-186">Per questo motivo il servizio attore deve usare uno schema di partizionamento Int64 con l'intervallo di chiavi Int64 completo.</span><span class="sxs-lookup"><span data-stu-id="4364b-186">This is why the actor service must use an Int64 partitioning scheme with the full Int64 key range.</span></span> <span data-ttu-id="4364b-187">È comunque possibile usare valori ID personalizzati per un `ActorID`, tra cui GUID/UUID, stringhe e Int64.</span><span class="sxs-lookup"><span data-stu-id="4364b-187">However, custom ID values can be used for an `ActorID`, including GUIDs/UUIDs, strings, and Int64s.</span></span>

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

<span data-ttu-id="4364b-188">Quando si usano GUID/UUID e stringhe, viene eseguito l'hashing dei valori in un Int64.</span><span class="sxs-lookup"><span data-stu-id="4364b-188">When you're using GUIDs/UUIDs and strings, the values are hashed to an Int64.</span></span> <span data-ttu-id="4364b-189">Quando invece si fornisce esplicitamente un Int64 a un `ActorId`, l'Int64 verrà mappato direttamente a una partizione senza ulteriore hashing.</span><span class="sxs-lookup"><span data-stu-id="4364b-189">However, when you're explicitly providing an Int64 to an `ActorId`, the Int64 will map directly to a partition without further hashing.</span></span> <span data-ttu-id="4364b-190">È possibile usare questa tecnica per controllare in quale partizione vengono inseriti gli attori.</span><span class="sxs-lookup"><span data-stu-id="4364b-190">You can use this technique to control which partition the actors are placed in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4364b-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4364b-191">Next steps</span></span>
* [<span data-ttu-id="4364b-192">Gestione dello stato degli attori</span><span class="sxs-lookup"><span data-stu-id="4364b-192">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="4364b-193">Ciclo di vita degli attori e Garbage Collection</span><span class="sxs-lookup"><span data-stu-id="4364b-193">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="4364b-194">Documentazione di riferimento delle API di Actors</span><span class="sxs-lookup"><span data-stu-id="4364b-194">Actors API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="4364b-195">Codice di esempio .NET</span><span class="sxs-lookup"><span data-stu-id="4364b-195">.NET sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="4364b-196">Codice di esempio Java</span><span class="sxs-lookup"><span data-stu-id="4364b-196">Java sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
