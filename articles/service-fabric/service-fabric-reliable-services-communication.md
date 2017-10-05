---
title: Panoramica sulla comunicazione di Reliable Services | Microsoft Docs
description: Panoramica sul modello di comunicazione di Reliable Services, compresi i listener di apertura nei servizi, gli endpoint di risoluzione e la comunicazione tra servizi.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: 36217988-420e-409d-b0a4-e0e875b6eac8
ms.service: service-fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: b418904f50b772c12bfcdbb95beb9312c8b9fb00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-reliable-services-communication-apis"></a><span data-ttu-id="4200a-103">Come usare le API di comunicazione di Reliable Services</span><span class="sxs-lookup"><span data-stu-id="4200a-103">How to use the Reliable Services communication APIs</span></span>
<span data-ttu-id="4200a-104">Azure Service Fabric è una piattaforma completamente indipendente dalle comunicazioni tra servizi.</span><span class="sxs-lookup"><span data-stu-id="4200a-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="4200a-105">Sono accettabili tutti i protocolli e gli stack, da UDP a HTTP.</span><span class="sxs-lookup"><span data-stu-id="4200a-105">All protocols and stacks are acceptable, from UDP to HTTP.</span></span> <span data-ttu-id="4200a-106">Dipende dallo sviluppatore del servizio scegliere la modalità di comunicazione tra servizi.</span><span class="sxs-lookup"><span data-stu-id="4200a-106">It's up to the service developer to choose how services should communicate.</span></span> <span data-ttu-id="4200a-107">Il framework applicazione di Reliable Services offre gli stack di comunicazione predefiniti nonché le API che è possibile usare per creare componenti di comunicazione personalizzati.</span><span class="sxs-lookup"><span data-stu-id="4200a-107">The Reliable Services application framework provides built-in communication stacks as well as APIs that you can use to build your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="4200a-108">Impostare la comunicazione tra servizi</span><span class="sxs-lookup"><span data-stu-id="4200a-108">Set up service communication</span></span>
<span data-ttu-id="4200a-109">L'API di Reliable Services usa una semplice interfaccia per la comunicazione tra servizi.</span><span class="sxs-lookup"><span data-stu-id="4200a-109">The Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="4200a-110">Per aprire un endpoint del servizio, è sufficiente implementare questa interfaccia:</span><span class="sxs-lookup"><span data-stu-id="4200a-110">To open an endpoint for your service, simply implement this interface:</span></span>

```csharp

public interface ICommunicationListener
{
    Task<string> OpenAsync(CancellationToken cancellationToken);

    Task CloseAsync(CancellationToken cancellationToken);

    void Abort();
}

```

```java
public interface CommunicationListener {
    CompletableFuture<String> openAsync(CancellationToken cancellationToken);

    CompletableFuture<?> closeAsync(CancellationToken cancellationToken);

    void abort();
}
```

<span data-ttu-id="4200a-111">Aggiungere quindi l'implementazione del listener di comunicazione restituendola in un override del metodo della classe di base del servizio.</span><span class="sxs-lookup"><span data-stu-id="4200a-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="4200a-112">Per i servizi senza stato:</span><span class="sxs-lookup"><span data-stu-id="4200a-112">For stateless services:</span></span>

```csharp
class MyStatelessService : StatelessService
{
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        ...
    }
    ...
}
```
```java
public class MyStatelessService extends StatelessService {

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ...
    }
    ...
}
```

<span data-ttu-id="4200a-113">Per i servizi con stato:</span><span class="sxs-lookup"><span data-stu-id="4200a-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="4200a-114">Reliable Services con stato non è ancora supportato in Java.</span><span class="sxs-lookup"><span data-stu-id="4200a-114">Stateful reliable services are not supported in Java yet.</span></span>
>
>

```csharp
class MyStatefulService : StatefulService
{
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        ...
    }
    ...
}
```

<span data-ttu-id="4200a-115">In entrambi i casi restituire una raccolta di listener.</span><span class="sxs-lookup"><span data-stu-id="4200a-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="4200a-116">Ciò consente al servizio di rimanere in ascolto su più endpoint, potenzialmente tramite protocolli diversi, usando più listener.</span><span class="sxs-lookup"><span data-stu-id="4200a-116">This allows your service to listen on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="4200a-117">Può essere ad esempio presente un listener HTTP e un listener WebSocket separato.</span><span class="sxs-lookup"><span data-stu-id="4200a-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="4200a-118">Ogni listener riceve un nome e la raccolta risultante di coppie *nome : indirizzo* è rappresentata come oggetto JSON quando un client richiede gli indirizzi di ascolto per un'istanza o una partizione del servizio.</span><span class="sxs-lookup"><span data-stu-id="4200a-118">Each listener gets a name, and the resulting collection of *name : address* pairs are represented as a JSON object when a client requests the listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="4200a-119">In un servizio senza stato l'override restituisce una raccolta di ServiceInstanceListener.</span><span class="sxs-lookup"><span data-stu-id="4200a-119">In a stateless service, the override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="4200a-120">Un oggetto `ServiceInstanceListener` contiene una funzione per creare un'interfaccia `ICommunicationListener(C#) / CommunicationListener(Java)` e assegnarle un nome.</span><span class="sxs-lookup"><span data-stu-id="4200a-120">A `ServiceInstanceListener` contains a function to create an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="4200a-121">Per i servizi con stato l'override restituisce una raccolta di ServiceReplicaListener.</span><span class="sxs-lookup"><span data-stu-id="4200a-121">For stateful services, the override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="4200a-122">Questo è un comportamento leggermente diverso rispetto a quello del servizio senza stato, perché l'oggetto `ServiceReplicaListener` dispone di un'opzione per aprire l'interfaccia `ICommunicationListener` nelle repliche secondarie.</span><span class="sxs-lookup"><span data-stu-id="4200a-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option to open an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="4200a-123">Ciò consente non solo di usare più listener di comunicazione in un servizio, ma anche di specificare quali listener accettano le richieste nelle repliche secondarie e quali si limitano a rimanere in ascolto sulle repliche primarie.</span><span class="sxs-lookup"><span data-stu-id="4200a-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="4200a-124">Ad esempio, un oggetto ServiceRemotingListener può gestire le chiamate RPC solo sulle repliche primarie, mentre un secondo listener personalizzato può accettare le richieste di lettura sulle repliche secondarie tramite HTTP:</span><span class="sxs-lookup"><span data-stu-id="4200a-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[]
    {
        new ServiceReplicaListener(context =>
            new MyCustomHttpListener(context),
            "HTTPReadonlyEndpoint",
            true),

        new ServiceReplicaListener(context =>
            this.CreateServiceRemotingListener(context),
            "rpcPrimaryEndpoint",
            false)
    };
}
```

> [!NOTE]
> <span data-ttu-id="4200a-125">Quando si creano più listener per un servizio, a ogni listener **deve** essere assegnato un nome univoco.</span><span class="sxs-lookup"><span data-stu-id="4200a-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="4200a-126">Descrivere infine gli endpoint necessari per il servizio nel [manifesto del servizio](service-fabric-application-model.md) , nella sezione relativa agli endpoint.</span><span class="sxs-lookup"><span data-stu-id="4200a-126">Finally, describe the endpoints that are required for the service in the [service manifest](service-fabric-application-model.md) under the section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="4200a-127">Il listener di comunicazione può accedere alle risorse di endpoint allocate da `CodePackageActivationContext` in `ServiceContext`.</span><span class="sxs-lookup"><span data-stu-id="4200a-127">The communication listener can access the endpoint resources allocated to it from the `CodePackageActivationContext` in the `ServiceContext`.</span></span> <span data-ttu-id="4200a-128">Quando viene aperto, il listener può avviare l'ascolto delle richieste.</span><span class="sxs-lookup"><span data-stu-id="4200a-128">The listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="4200a-129">Le risorse di endpoint sono comuni all'intero pacchetto del servizio e vengono allocate da Service Fabric quando viene attivato il pacchetto del servizio.</span><span class="sxs-lookup"><span data-stu-id="4200a-129">Endpoint resources are common to the entire service package, and they are allocated by Service Fabric when the service package is activated.</span></span> <span data-ttu-id="4200a-130">Più repliche di servizio ospitate nella stessa istanza di ServiceHost possono condividere la stessa porta.</span><span class="sxs-lookup"><span data-stu-id="4200a-130">Multiple service replicas hosted in the same ServiceHost may share the same port.</span></span> <span data-ttu-id="4200a-131">Ciò significa che il listener di comunicazione deve supportare la condivisione delle porte.</span><span class="sxs-lookup"><span data-stu-id="4200a-131">This means that the communication listener should support port sharing.</span></span> <span data-ttu-id="4200a-132">Il metodo consigliato per eseguire questa operazione consiste nell'uso dell'ID partizione e dell'ID replica/istanza da parte del listener di comunicazione durante la generazione dell'indirizzo di ascolto.</span><span class="sxs-lookup"><span data-stu-id="4200a-132">The recommended way of doing this is for the communication listener to use the partition ID and replica/instance ID when it generates the listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="4200a-133">Registrazione dell'indirizzo del servizio</span><span class="sxs-lookup"><span data-stu-id="4200a-133">Service address registration</span></span>
<span data-ttu-id="4200a-134">Nei cluster di Service Fabric viene eseguito un servizio di sistema denominato *servizio Naming* .</span><span class="sxs-lookup"><span data-stu-id="4200a-134">A system service called the *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="4200a-135">Il servizio Naming è un registrar per i servizi e i relativi indirizzi su cui è in ascolto ogni istanza o replica del servizio.</span><span class="sxs-lookup"><span data-stu-id="4200a-135">The Naming Service is a registrar for services and their addresses that each instance or replica of the service is listening on.</span></span> <span data-ttu-id="4200a-136">Quando il metodo `OpenAsync(C#) / openAsync(Java)` di un oggetto `ICommunicationListener(C#) / CommunicationListener(Java)` viene completato, il valore restituito viene registrato nel servizio Naming.</span><span class="sxs-lookup"><span data-stu-id="4200a-136">When the `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in the Naming Service.</span></span> <span data-ttu-id="4200a-137">Questo valore restituito che viene pubblicato nel servizio Naming è una stringa il cui valore può essere costituito da qualsiasi valore.</span><span class="sxs-lookup"><span data-stu-id="4200a-137">This return value that gets published in the Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="4200a-138">Questo valore stringa è il valore che i client vendono quando richiedono a Naming Service un indirizzo per il servizio.</span><span class="sxs-lookup"><span data-stu-id="4200a-138">This string value is what clients see when they ask for an address for the service from the Naming Service.</span></span>

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.CodePackageActivationContext.GetEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.Port;

    this.listeningAddress = string.Format(
                CultureInfo.InvariantCulture,
                "http://+:{0}/",
                port);

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

    // the string returned here will be published in the Naming Service.
    return Task.FromResult(this.publishAddress);
}
```
```java
public CompletableFuture<String> openAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.getCodePackageActivationContext.getEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.getPort();

    this.publishAddress = String.format("http://%s:%d/", FabricRuntime.getNodeContext().getIpAddressOrFQDN(), port);

    this.webApp = new WebApp(port);
    this.webApp.start();

    /* the string returned here will be published in the Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="4200a-139">Service Fabric fornisce le API che consentono ai client e ad altri servizi di richiedere questo indirizzo in base al nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="4200a-139">Service Fabric provides APIs that allow clients and other services to then ask for this address by service name.</span></span> <span data-ttu-id="4200a-140">Questo aspetto è importante perché l'indirizzo del servizio non è statico.</span><span class="sxs-lookup"><span data-stu-id="4200a-140">This is important because the service address is not static.</span></span> <span data-ttu-id="4200a-141">I servizi vengono spostati nel cluster ai fini del bilanciamento del carico e della disponibilità delle risorse.</span><span class="sxs-lookup"><span data-stu-id="4200a-141">Services are moved around in the cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="4200a-142">Questo meccanismo consente ai client di risolvere l'indirizzo di ascolto per un servizio.</span><span class="sxs-lookup"><span data-stu-id="4200a-142">This is the mechanism that allow clients to resolve the listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="4200a-143">Per una procedura dettagliata completa di come scrivere un listener di comunicazione, vedere [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) (Servizi API Web di Service Fabric con self-hosting OWIN) per C#, mentre per Java è possibile scrivere la propria implementazione di server HTTP, vedere l'esempio di applicazione EchoServer in https://github.com/Azure-Samples/service-fabric-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="4200a-143">For a complete walk-through of how to write a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="4200a-144">Comunicazione con un servizio</span><span class="sxs-lookup"><span data-stu-id="4200a-144">Communicating with a service</span></span>
<span data-ttu-id="4200a-145">L'API di Reliable Services offre le librerie seguenti per la scrittura di client che comunicano con i servizi.</span><span class="sxs-lookup"><span data-stu-id="4200a-145">The Reliable Services API provides the following libraries to write clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="4200a-146">Risoluzione degli endpoint di servizio</span><span class="sxs-lookup"><span data-stu-id="4200a-146">Service endpoint resolution</span></span>
<span data-ttu-id="4200a-147">Il primo passaggio per la comunicazione con un servizio è risolvere un indirizzo di endpoint della partizione o dell'istanza del servizio con cui si vuole comunicare.</span><span class="sxs-lookup"><span data-stu-id="4200a-147">The first step to communication with a service is to resolve an endpoint address of the partition or instance of the service you want to talk to.</span></span> <span data-ttu-id="4200a-148">La classe di utilità `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` è una classe primitiva di base che consente ai client di determinare l'endpoint di un servizio in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="4200a-148">The `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine the endpoint of a service at runtime.</span></span> <span data-ttu-id="4200a-149">Nella terminologia di Service Fabric, il processo di determinazione dell'endpoint di un servizio è denominato *risoluzione degli endpoint di servizio*.</span><span class="sxs-lookup"><span data-stu-id="4200a-149">In Service Fabric terminology, the process of determining the endpoint of a service is referred to as the *service endpoint resolution*.</span></span>

<span data-ttu-id="4200a-150">Per connettersi ai servizi all'interno di un cluster, è possibile creare un oggetto ServicePartitionResolver usando le impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="4200a-150">To connect to services within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="4200a-151">È l'utilizzo consigliato nella maggior parte dei casi:</span><span class="sxs-lookup"><span data-stu-id="4200a-151">This is the recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="4200a-152">Per connettersi ai servizi in un cluster diverso, è possibile creare un oggetto ServicePartitionResolver con un set di endpoint del gateway del cluster.</span><span class="sxs-lookup"><span data-stu-id="4200a-152">To connect to services in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="4200a-153">Si noti che gli endpoint del gateway sono solo endpoint diversi per la connessione allo stesso cluster.</span><span class="sxs-lookup"><span data-stu-id="4200a-153">Note that gateway endpoints are just different endpoints for connecting to the same cluster.</span></span> <span data-ttu-id="4200a-154">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4200a-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="4200a-155">In alternativa, è possibile assegnare alla classe `ServicePartitionResolver` la funzione per la creazione di un oggetto `FabricClient` da usare internamente:</span><span class="sxs-lookup"><span data-stu-id="4200a-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` to use internally:</span></span>

```csharp
public delegate FabricClient CreateFabricClientDelegate();
```
```java
public FabricServicePartitionResolver(CreateFabricClient createFabricClient) {
...
}

public interface CreateFabricClient {
    public FabricClient getFabricClient();
}
```

<span data-ttu-id="4200a-156">`FabricClient` è l'oggetto usato per comunicare con il cluster di Service Fabric per varie operazioni di gestione nel cluster.</span><span class="sxs-lookup"><span data-stu-id="4200a-156">`FabricClient` is the object that is used to communicate with the Service Fabric cluster for various management operations on the cluster.</span></span> <span data-ttu-id="4200a-157">È utile quando si vuole avere un maggiore controllo sul modo in cui un risolutore di partizioni del servizio interagisce con il cluster.</span><span class="sxs-lookup"><span data-stu-id="4200a-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="4200a-158">`FabricClient` esegue la memorizzazione nella cache internamente ed è in genere dispendioso da creare, quindi è importante riusare le istanze di `FabricClient` quanto più possibile.</span><span class="sxs-lookup"><span data-stu-id="4200a-158">`FabricClient` performs caching internally and is generally expensive to create, so it is important to reuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="4200a-159">Un metodo di risoluzione viene quindi usato per recuperare l'indirizzo di un servizio o una partizione del servizio per i servizi partizionati.</span><span class="sxs-lookup"><span data-stu-id="4200a-159">A resolve method is then used to retrieve the address of a service or a service partition for partitioned services.</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();

ResolvedServicePartition partition =
    await resolver.ResolveAsync(new Uri("fabric:/MyApp/MyService"), new ServicePartitionKey(), cancellationToken);
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();

CompletableFuture<ResolvedServicePartition> partition =
    resolver.resolveAsync(new URI("fabric:/MyApp/MyService"), new ServicePartitionKey());
```

<span data-ttu-id="4200a-160">L'indirizzo di un servizio può essere risolto facilmente con ServicePartitionResolver, ma per garantire che l'indirizzo risolto possa essere usato correttamente è necessaria una procedura più complessa.</span><span class="sxs-lookup"><span data-stu-id="4200a-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required to ensure the resolved address can be used correctly.</span></span> <span data-ttu-id="4200a-161">Il client deve rilevare se il tentativo di connessione non è riuscito a causa di un errore temporaneo (ad esempio, nel caso in cui il servizio è stato spostato o è temporaneamente non disponibile) ed è quindi possibile eseguire un nuovo tentativo o a causa di un errore permanente (ad esempio, nel caso in cui il servizio è stato eliminato o la risorsa richiesta non esiste più).</span><span class="sxs-lookup"><span data-stu-id="4200a-161">Your client needs to detect whether the connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or the requested resource no longer exists).</span></span> <span data-ttu-id="4200a-162">Le istanze del servizio o le repliche possono essere spostate da un nodo all'altro in qualsiasi momento per vari motivi.</span><span class="sxs-lookup"><span data-stu-id="4200a-162">Service instances or replicas can move around from node to node at any time for multiple reasons.</span></span> <span data-ttu-id="4200a-163">L'indirizzo del servizio risolto tramite ServicePartitionResolver potrebbe essere non aggiornato quando il codice client prova a connettersi.</span><span class="sxs-lookup"><span data-stu-id="4200a-163">The service address resolved through ServicePartitionResolver may be stale by the time your client code attempts to connect.</span></span> <span data-ttu-id="4200a-164">Il client dovrà in tal caso risolvere di nuovo l'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="4200a-164">In that case again the client needs to re-resolve the address.</span></span> <span data-ttu-id="4200a-165">Fornendo l'oggetto `ResolvedServicePartition` precedente si indica che il resolver deve riprovare anziché recuperare semplicemente un indirizzo memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="4200a-165">Providing the previous `ResolvedServicePartition` indicates that the resolver needs to try again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="4200a-166">Non è necessario, in genere, che il codice client funzioni direttamente con l'oggetto ServicePartitionResolver.</span><span class="sxs-lookup"><span data-stu-id="4200a-166">Typically, the client code need not work with the ServicePartitionResolver directly.</span></span> <span data-ttu-id="4200a-167">Il codice viene creato e passato alle factory di client di comunicazione nell'API di Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="4200a-167">It is created and passed on to communication client factories in the Reliable Services API.</span></span> <span data-ttu-id="4200a-168">Le factory usano il resolver internamente per generare un oggetto client da poter usare per comunicare con i servizi.</span><span class="sxs-lookup"><span data-stu-id="4200a-168">The factories use the resolver internally to generate a client object that can be used to communicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="4200a-169">Client e factory di comunicazione</span><span class="sxs-lookup"><span data-stu-id="4200a-169">Communication clients and factories</span></span>
<span data-ttu-id="4200a-170">La libreria di factory di comunicazione implementa un tipico schema di ripetizione dei tentativi per la gestione degli errori che semplifica la ripetizione dei tentativi di connessioni agli endpoint del servizio risolti.</span><span class="sxs-lookup"><span data-stu-id="4200a-170">The communication factory library implements a typical fault-handling retry pattern that makes retrying connections to resolved service endpoints easier.</span></span> <span data-ttu-id="4200a-171">La libreria di factory fornisce il meccanismo di ripetizione dei tentativi mentre l'utente fornisce i gestori di errori.</span><span class="sxs-lookup"><span data-stu-id="4200a-171">The factory library provides the retry mechanism while you provide the error handlers.</span></span>

<span data-ttu-id="4200a-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` definisce l'interfaccia di base implementata da una factory di client di comunicazione che produce client che possono comunicare con un servizio di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4200a-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines the base interface implemented by a communication client factory that produces clients that can talk to a Service Fabric service.</span></span> <span data-ttu-id="4200a-173">L'implementazione dell'oggetto CommunicationClientFactory dipende dallo stack di comunicazione usato dal servizio di Service Fabric con cui il client vuole comunicare.</span><span class="sxs-lookup"><span data-stu-id="4200a-173">The implementation of the CommunicationClientFactory depends on the communication stack used by the Service Fabric service where the client wants to communicate.</span></span> <span data-ttu-id="4200a-174">L'API di Reliable Services include un oggetto `CommunicationClientFactoryBase<TCommunicationClient>`,</span><span class="sxs-lookup"><span data-stu-id="4200a-174">The Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="4200a-175">che offre un'implementazione di base dell'interfaccia CommunicationClientFactory e consente di eseguire attività comuni a tutti gli stack di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="4200a-175">This provides a base implementation of the CommunicationClientFactory interface and performs tasks that are common to all the communication stacks.</span></span> <span data-ttu-id="4200a-176">Tali attività includono l'uso di un ServicePartitionResolver per determinare l'endpoint di servizio.</span><span class="sxs-lookup"><span data-stu-id="4200a-176">(These tasks include using a ServicePartitionResolver to determine the service endpoint).</span></span> <span data-ttu-id="4200a-177">I client in genere implementano la classe astratta CommunicationClientFactoryBase per gestire la logica specifica dello stack di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="4200a-177">Clients usually implement the abstract CommunicationClientFactoryBase class to handle logic that is specific to the communication stack.</span></span>

<span data-ttu-id="4200a-178">Il client di comunicazione riceve solo un indirizzo e lo usa per connettersi a un servizio.</span><span class="sxs-lookup"><span data-stu-id="4200a-178">The communication client just receives an address and uses it to connect to a service.</span></span> <span data-ttu-id="4200a-179">Il client può usare qualsiasi protocollo desidera.</span><span class="sxs-lookup"><span data-stu-id="4200a-179">The client can use whatever protocol it wants.</span></span>

```csharp
class MyCommunicationClient : ICommunicationClient
{
    public ResolvedServiceEndpoint Endpoint { get; set; }

    public string ListenerName { get; set; }

    public ResolvedServicePartition ResolvedServicePartition { get; set; }
}
```
```java
public class MyCommunicationClient implements CommunicationClient {

    private ResolvedServicePartition resolvedServicePartition;
    private String listenerName;
    private ResolvedServiceEndpoint endPoint;

    /*
     * Getters and Setters
     */
}
```

<span data-ttu-id="4200a-180">La factory del client è responsabile principalmente della creazione dei client di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="4200a-180">The client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="4200a-181">Per i client che non mantengono una connessione permanente, ad esempio un client HTTP, la factory deve solo creare e restituire il client.</span><span class="sxs-lookup"><span data-stu-id="4200a-181">For clients that don't maintain a persistent connection, such as an HTTP client, the factory only needs to create and return the client.</span></span> <span data-ttu-id="4200a-182">Gli altri protocolli che mantengono una connessione permanente, ad esempio alcuni protocolli binari, devono anche essere convalidati dalla factory per determinare se la connessione deve essere ricreata.</span><span class="sxs-lookup"><span data-stu-id="4200a-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by the factory to determine whether the connection needs to be re-created.</span></span>  

```csharp
public class MyCommunicationClientFactory : CommunicationClientFactoryBase<MyCommunicationClient>
{
    protected override void AbortClient(MyCommunicationClient client)
    {
    }

    protected override Task<MyCommunicationClient> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
    {
    }

    protected override bool ValidateClient(MyCommunicationClient clientChannel)
    {
    }

    protected override bool ValidateClient(string endpoint, MyCommunicationClient client)
    {
    }
}
```
```java
public class MyCommunicationClientFactory extends CommunicationClientFactoryBase<MyCommunicationClient> {

    @Override
    protected boolean validateClient(MyCommunicationClient clientChannel) {
    }

    @Override
    protected boolean validateClient(String endpoint, MyCommunicationClient client) {
    }

    @Override
    protected CompletableFuture<MyCommunicationClient> createClientAsync(String endpoint) {
    }

    @Override
    protected void abortClient(MyCommunicationClient client) {
    }
}
```

<span data-ttu-id="4200a-183">Un gestore di eccezioni, infine, è responsabile della determinazione dell'azione da intraprendere quando si verifica un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="4200a-183">Finally, an exception handler is responsible for determining what action to take when an exception occurs.</span></span> <span data-ttu-id="4200a-184">Le eccezioni vengono suddivise nelle categorie **con possibilità di ritentare** e **senza possibilità di ritentare**.</span><span class="sxs-lookup"><span data-stu-id="4200a-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="4200a-185">Le eccezioni **senza possibilità di ritentare** vengono semplicemente restituite al chiamante.</span><span class="sxs-lookup"><span data-stu-id="4200a-185">**Non retryable** exceptions simply get rethrown back to the caller.</span></span>
* <span data-ttu-id="4200a-186">Le eccezioni **con possibilità di ritentare** si suddividono a propria volta in due categorie: **temporanee** e **non temporanee**.</span><span class="sxs-lookup"><span data-stu-id="4200a-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="4200a-187">**temporanee** sono quelle per cui è possibile ripetere il tentativo senza risolvere di nuovo l'indirizzo dell'endpoint del servizio.</span><span class="sxs-lookup"><span data-stu-id="4200a-187">**Transient** exceptions are those that can simply be retried without re-resolving the service endpoint address.</span></span> <span data-ttu-id="4200a-188">Includono problemi di rete temporanei o risposte di errore del servizio diversi da quelli che indicano che l'indirizzo dell'endpoint del servizio non esiste.</span><span class="sxs-lookup"><span data-stu-id="4200a-188">These will include transient network problems or service error responses other than those that indicate the service endpoint address does not exist.</span></span>
  * <span data-ttu-id="4200a-189">**Non-transient** sono quelle per cui è necessario risolvere di nuovo l'indirizzo dell'endpoint del servizio.</span><span class="sxs-lookup"><span data-stu-id="4200a-189">**Non-transient** exceptions are those that require the service endpoint address to be re-resolved.</span></span> <span data-ttu-id="4200a-190">Includono eccezioni che indicano che l'endpoint del servizio non è raggiungibile, ad esempio perché il servizio è stato spostato in un altro nodo.</span><span class="sxs-lookup"><span data-stu-id="4200a-190">These include exceptions that indicate the service endpoint could not be reached, indicating the service has moved to a different node.</span></span>

<span data-ttu-id="4200a-191">L'oggetto `TryHandleException` prende una decisione su una determinata eccezione.</span><span class="sxs-lookup"><span data-stu-id="4200a-191">The `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="4200a-192">Se **non sa** quali decisioni prendere in merito a un'eccezione, restituirà **false**.</span><span class="sxs-lookup"><span data-stu-id="4200a-192">If it **does not know** what decisions to make about an exception, it should return **false**.</span></span> <span data-ttu-id="4200a-193">Se **sa** quale decisione prendere, imposterà il risultato di conseguenza e restituirà **true**.</span><span class="sxs-lookup"><span data-stu-id="4200a-193">If it **does know** what decision to make, it should set the result accordingly and return **true**.</span></span>

```csharp
class MyExceptionHandler : IExceptionHandler
{
    public bool TryHandleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings, out ExceptionHandlingResult result)
    {
        // if exceptionInformation.Exception is known and is transient (can be retried without re-resolving)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, true, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;


        // if exceptionInformation.Exception is known and is not transient (indicates a new service endpoint address must be resolved)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, false, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;

        // if exceptionInformation.Exception is unknown (let the next IExceptionHandler attempt to handle it)
        result = null;
        return false;
    }
}
```
```java
public class MyExceptionHandler implements ExceptionHandler {

    @Override
    public ExceptionHandlingResult handleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings) {        

        /* if exceptionInformation.getException() is known and is transient (can be retried without re-resolving)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), true, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;


        /* if exceptionInformation.getException() is known and is not transient (indicates a new service endpoint address must be resolved)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), false, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;

        /* if exceptionInformation.getException() is unknown (let the next ExceptionHandler attempt to handle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="4200a-194">Riassumendo</span><span class="sxs-lookup"><span data-stu-id="4200a-194">Putting it all together</span></span>
<span data-ttu-id="4200a-195">Con `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` e `IExceptionHandler(C#) / ExceptionHandler(Java)` basati su un protocollo di comunicazione, un oggetto `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` esegue il wrapping di tutti gli elementi e fornisce il ciclo di risoluzione degli indirizzi della partizione del servizio e di gestione degli errori in base a tali componenti.</span><span class="sxs-lookup"><span data-stu-id="4200a-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides the fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with the service using the client.
   },
   CancellationToken.None);

```
```java
private MyCommunicationClientFactory myCommunicationClientFactory;
private URI myServiceUri;

FabricServicePartitionClient myServicePartitionClient = new FabricServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

CompletableFuture<?> result = myServicePartitionClient.invokeWithRetryAsync(client -> {
      /* Communicate with the service using the client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="4200a-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4200a-196">Next steps</span></span>
* <span data-ttu-id="4200a-197">Vedere un esempio di comunicazione HTTP tra servizi in un [progetto di esempio C# in GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) o un [progetto di esempio Java in GitHub](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span><span class="sxs-lookup"><span data-stu-id="4200a-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="4200a-198">Chiamate di procedura remota con i Reliable Services remoti</span><span class="sxs-lookup"><span data-stu-id="4200a-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="4200a-199">Web API che usa OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="4200a-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="4200a-200">Comunicazione di WCF tramite Reliable Services</span><span class="sxs-lookup"><span data-stu-id="4200a-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
