---
title: Panoramica di servizi di comunicazione aaaReliable | Documenti Microsoft
description: Panoramica di hello servizi affidabili modello di comunicazione, inclusi i listener di apertura su servizi, risolvere gli endpoint e la comunicazione tra servizi.
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
ms.openlocfilehash: 93a7017b50df0822969daa5ad78302c73e8ba641
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-reliable-services-communication-apis"></a><span data-ttu-id="6222b-103">Come toouse hello API di comunicazione tra servizi affidabili</span><span class="sxs-lookup"><span data-stu-id="6222b-103">How toouse hello Reliable Services communication APIs</span></span>
<span data-ttu-id="6222b-104">Azure Service Fabric è una piattaforma completamente indipendente dalle comunicazioni tra servizi.</span><span class="sxs-lookup"><span data-stu-id="6222b-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="6222b-105">Tutti i protocolli e gli stack sono accettabili, da tooHTTP UDP.</span><span class="sxs-lookup"><span data-stu-id="6222b-105">All protocols and stacks are acceptable, from UDP tooHTTP.</span></span> <span data-ttu-id="6222b-106">È la modalità in cui devono comunicare servizi attivo toohello servizio developer toochoose.</span><span class="sxs-lookup"><span data-stu-id="6222b-106">It's up toohello service developer toochoose how services should communicate.</span></span> <span data-ttu-id="6222b-107">Hello servizi affidabili application framework fornisce stack di comunicazione predefinita nonché API che è possibile utilizzare toobuild i componenti personalizzate di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="6222b-107">hello Reliable Services application framework provides built-in communication stacks as well as APIs that you can use toobuild your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="6222b-108">Impostare la comunicazione tra servizi</span><span class="sxs-lookup"><span data-stu-id="6222b-108">Set up service communication</span></span>
<span data-ttu-id="6222b-109">Hello affidabile API dei servizi utilizza un'interfaccia semplice per le comunicazioni di servizio.</span><span class="sxs-lookup"><span data-stu-id="6222b-109">hello Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="6222b-110">tooopen un endpoint per il servizio, è sufficiente implementare questa interfaccia:</span><span class="sxs-lookup"><span data-stu-id="6222b-110">tooopen an endpoint for your service, simply implement this interface:</span></span>

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

<span data-ttu-id="6222b-111">Aggiungere quindi l'implementazione del listener di comunicazione restituendola in un override del metodo della classe di base del servizio.</span><span class="sxs-lookup"><span data-stu-id="6222b-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="6222b-112">Per i servizi senza stato:</span><span class="sxs-lookup"><span data-stu-id="6222b-112">For stateless services:</span></span>

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

<span data-ttu-id="6222b-113">Per i servizi con stato:</span><span class="sxs-lookup"><span data-stu-id="6222b-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="6222b-114">Reliable Services con stato non è ancora supportato in Java.</span><span class="sxs-lookup"><span data-stu-id="6222b-114">Stateful reliable services are not supported in Java yet.</span></span>
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

<span data-ttu-id="6222b-115">In entrambi i casi restituire una raccolta di listener.</span><span class="sxs-lookup"><span data-stu-id="6222b-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="6222b-116">In questo modo il servizio toolisten su più endpoint, potenzialmente utilizzando protocolli diversi, utilizzando più listener.</span><span class="sxs-lookup"><span data-stu-id="6222b-116">This allows your service toolisten on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="6222b-117">Può essere ad esempio presente un listener HTTP e un listener WebSocket separato.</span><span class="sxs-lookup"><span data-stu-id="6222b-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="6222b-118">Ogni listener riceve un nome e un insieme risultante di hello di *nome: indirizzo* coppie sono rappresentate come un oggetto JSON quando un client richiede indirizzi di ascolto hello per un'istanza del servizio o una partizione.</span><span class="sxs-lookup"><span data-stu-id="6222b-118">Each listener gets a name, and hello resulting collection of *name : address* pairs are represented as a JSON object when a client requests hello listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="6222b-119">In un servizio senza stato, hello override restituisce una raccolta di ServiceInstanceListeners.</span><span class="sxs-lookup"><span data-stu-id="6222b-119">In a stateless service, hello override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="6222b-120">Oggetto `ServiceInstanceListener` toocreate una funzione contiene un `ICommunicationListener(C#) / CommunicationListener(Java)` e viene assegnato un nome.</span><span class="sxs-lookup"><span data-stu-id="6222b-120">A `ServiceInstanceListener` contains a function toocreate an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="6222b-121">Per i servizi con stati, hello override restituisce una raccolta di ServiceReplicaListeners.</span><span class="sxs-lookup"><span data-stu-id="6222b-121">For stateful services, hello override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="6222b-122">Questo è leggermente diverso rispetto alla controparte senza stata, perché un `ServiceReplicaListener` è un'opzione tooopen un `ICommunicationListener` nelle repliche secondarie.</span><span class="sxs-lookup"><span data-stu-id="6222b-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option tooopen an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="6222b-123">Ciò consente non solo di usare più listener di comunicazione in un servizio, ma anche di specificare quali listener accettano le richieste nelle repliche secondarie e quali si limitano a rimanere in ascolto sulle repliche primarie.</span><span class="sxs-lookup"><span data-stu-id="6222b-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="6222b-124">Ad esempio, un oggetto ServiceRemotingListener può gestire le chiamate RPC solo sulle repliche primarie, mentre un secondo listener personalizzato può accettare le richieste di lettura sulle repliche secondarie tramite HTTP:</span><span class="sxs-lookup"><span data-stu-id="6222b-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

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
> <span data-ttu-id="6222b-125">Quando si creano più listener per un servizio, a ogni listener **deve** essere assegnato un nome univoco.</span><span class="sxs-lookup"><span data-stu-id="6222b-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="6222b-126">Infine, descrivere l'endpoint di hello che sono necessarie per il servizio di hello in hello [manifesto del servizio](service-fabric-application-model.md) nella sezione hello sugli endpoint.</span><span class="sxs-lookup"><span data-stu-id="6222b-126">Finally, describe hello endpoints that are required for hello service in hello [service manifest](service-fabric-application-model.md) under hello section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="6222b-127">listener di comunicazione Hello possono accedere alle risorse di endpoint di hello allocate tooit da hello `CodePackageActivationContext` in hello `ServiceContext`.</span><span class="sxs-lookup"><span data-stu-id="6222b-127">hello communication listener can access hello endpoint resources allocated tooit from hello `CodePackageActivationContext` in hello `ServiceContext`.</span></span> <span data-ttu-id="6222b-128">listener Hello è quindi possibile avviare l'ascolto delle richieste quando viene aperto.</span><span class="sxs-lookup"><span data-stu-id="6222b-128">hello listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="6222b-129">Risorse endpoint sono pacchetto del servizio intero toohello comuni e vengono allocati dall'infrastruttura del servizio quando viene attivato il pacchetto di servizio hello.</span><span class="sxs-lookup"><span data-stu-id="6222b-129">Endpoint resources are common toohello entire service package, and they are allocated by Service Fabric when hello service package is activated.</span></span> <span data-ttu-id="6222b-130">Più repliche del servizio ospitate in hello stesso ServiceHost possono condividere hello stessa porta.</span><span class="sxs-lookup"><span data-stu-id="6222b-130">Multiple service replicas hosted in hello same ServiceHost may share hello same port.</span></span> <span data-ttu-id="6222b-131">Ciò significa che il listener di comunicazione hello deve supportare la condivisione delle porte.</span><span class="sxs-lookup"><span data-stu-id="6222b-131">This means that hello communication listener should support port sharing.</span></span> <span data-ttu-id="6222b-132">Hello consiglia modo di procedere per hello comunicazione listener toouse hello partizione ID e l'ID e l'istanza di replica durante la generazione di indirizzo di ascolto hello.</span><span class="sxs-lookup"><span data-stu-id="6222b-132">hello recommended way of doing this is for hello communication listener toouse hello partition ID and replica/instance ID when it generates hello listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="6222b-133">Registrazione dell'indirizzo del servizio</span><span class="sxs-lookup"><span data-stu-id="6222b-133">Service address registration</span></span>
<span data-ttu-id="6222b-134">Un servizio di sistema denominato hello *Naming Service* viene eseguito nei cluster di Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6222b-134">A system service called hello *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="6222b-135">Hello Naming Service è un programma di registrazione per servizi e i rispettivi indirizzi che ogni istanza o una replica del servizio hello è in ascolto.</span><span class="sxs-lookup"><span data-stu-id="6222b-135">hello Naming Service is a registrar for services and their addresses that each instance or replica of hello service is listening on.</span></span> <span data-ttu-id="6222b-136">Quando hello `OpenAsync(C#) / openAsync(Java)` metodo di un `ICommunicationListener(C#) / CommunicationListener(Java)` viene completato, il suo ritorno valore ottiene registrato nel servizio di denominazione hello.</span><span class="sxs-lookup"><span data-stu-id="6222b-136">When hello `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in hello Naming Service.</span></span> <span data-ttu-id="6222b-137">Valore che ottiene hello pubblicata nel servizio di denominazione è una stringa il cui valore può essere del tutto qualsiasi questo restituito.</span><span class="sxs-lookup"><span data-stu-id="6222b-137">This return value that gets published in hello Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="6222b-138">Questo valore di stringa è ciò che i client visualizzato quando si richiedono un indirizzo per il servizio di hello dal servizio di denominazione hello.</span><span class="sxs-lookup"><span data-stu-id="6222b-138">This string value is what clients see when they ask for an address for hello service from hello Naming Service.</span></span>

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

    // hello string returned here will be published in hello Naming Service.
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

    /* hello string returned here will be published in hello Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

<span data-ttu-id="6222b-139">Service Fabric fornisce API che consentono di client e altri servizi toothen chiedere per questo indirizzo dal nome del servizio.</span><span class="sxs-lookup"><span data-stu-id="6222b-139">Service Fabric provides APIs that allow clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="6222b-140">Questo è importante perché l'indirizzo del servizio hello non è statico.</span><span class="sxs-lookup"><span data-stu-id="6222b-140">This is important because hello service address is not static.</span></span> <span data-ttu-id="6222b-141">Servizi vengono spostati nel cluster hello per scopi di bilanciamento del carico e disponibilità delle risorse.</span><span class="sxs-lookup"><span data-stu-id="6222b-141">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="6222b-142">Questo è il meccanismo hello che consentono ai client hello tooresolve indirizzo per un servizio in ascolto.</span><span class="sxs-lookup"><span data-stu-id="6222b-142">This is hello mechanism that allow clients tooresolve hello listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="6222b-143">Per una procedura completa di come toowrite un listener di comunicazione, vedere [servizi API Web dell'infrastruttura del servizio con self-hosting OWIN](service-fabric-reliable-services-communication-webapi.md) per c#, mentre per Java è possibile scrivere la propria implementazione di server HTTP, vedere applicazione EchoServer esempio a https://github.com/Azure-Samples/service-fabric-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="6222b-143">For a complete walk-through of how toowrite a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="6222b-144">Comunicazione con un servizio</span><span class="sxs-lookup"><span data-stu-id="6222b-144">Communicating with a service</span></span>
<span data-ttu-id="6222b-145">Hello affidabile API dei servizi fornisce hello client toowrite di librerie che comunicano con i servizi seguenti.</span><span class="sxs-lookup"><span data-stu-id="6222b-145">hello Reliable Services API provides hello following libraries toowrite clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="6222b-146">Risoluzione degli endpoint di servizio</span><span class="sxs-lookup"><span data-stu-id="6222b-146">Service endpoint resolution</span></span>
<span data-ttu-id="6222b-147">Hello primo passaggio toocommunication con un servizio è un indirizzo dell'endpoint della partizione hello o dell'istanza del servizio hello da tootalk a tooresolve.</span><span class="sxs-lookup"><span data-stu-id="6222b-147">hello first step toocommunication with a service is tooresolve an endpoint address of hello partition or instance of hello service you want tootalk to.</span></span> <span data-ttu-id="6222b-148">Hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` classe di utilità è una primitiva di base che consente ai client di determinare endpoint hello di un servizio in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6222b-148">hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine hello endpoint of a service at runtime.</span></span> <span data-ttu-id="6222b-149">Nella terminologia di Service Fabric, hello processo di individuazione endpoint hello di un servizio è hello di cui viene fatto riferimento tooas *la risoluzione degli endpoint del servizio*.</span><span class="sxs-lookup"><span data-stu-id="6222b-149">In Service Fabric terminology, hello process of determining hello endpoint of a service is referred tooas hello *service endpoint resolution*.</span></span>

<span data-ttu-id="6222b-150">tooservices tooconnect all'interno di un cluster, ServicePartitionResolver è possibile creare usando le impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="6222b-150">tooconnect tooservices within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="6222b-151">È consigliata l'utilizzo della maggior parte dei casi hello:</span><span class="sxs-lookup"><span data-stu-id="6222b-151">This is hello recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="6222b-152">tooservices tooconnect in un cluster diverso, è possibile creare un ServicePartitionResolver con un set di endpoint di gateway di cluster.</span><span class="sxs-lookup"><span data-stu-id="6222b-152">tooconnect tooservices in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="6222b-153">Si noti che gli endpoint gateway sono endpoint diversi solo per la connessione toohello dello stesso cluster.</span><span class="sxs-lookup"><span data-stu-id="6222b-153">Note that gateway endpoints are just different endpoints for connecting toohello same cluster.</span></span> <span data-ttu-id="6222b-154">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="6222b-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="6222b-155">In alternativa, `ServicePartitionResolver` è possibile assegnare una funzione per la creazione di un `FabricClient` toouse internamente:</span><span class="sxs-lookup"><span data-stu-id="6222b-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` toouse internally:</span></span>

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

<span data-ttu-id="6222b-156">`FabricClient`è l'oggetto hello toocommunicate utilizzati con i cluster di Service Fabric hello per varie operazioni di gestione in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6222b-156">`FabricClient` is hello object that is used toocommunicate with hello Service Fabric cluster for various management operations on hello cluster.</span></span> <span data-ttu-id="6222b-157">È utile quando si vuole avere un maggiore controllo sul modo in cui un risolutore di partizioni del servizio interagisce con il cluster.</span><span class="sxs-lookup"><span data-stu-id="6222b-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="6222b-158">`FabricClient`esegue la memorizzazione nella cache internamente e viene in genere dispendiosi toocreate, pertanto è importante tooreuse `FabricClient` istanze quanto possibile.</span><span class="sxs-lookup"><span data-stu-id="6222b-158">`FabricClient` performs caching internally and is generally expensive toocreate, so it is important tooreuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="6222b-159">È un metodo di risoluzione usato tooretrieve hello un indirizzo di un servizio o una partizione del servizio per i servizi partizionati.</span><span class="sxs-lookup"><span data-stu-id="6222b-159">A resolve method is then used tooretrieve hello address of a service or a service partition for partitioned services.</span></span>

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

<span data-ttu-id="6222b-160">Indirizzo di un servizio può essere risolto facilmente utilizzando un ServicePartitionResolver, ma è necessario più lavoro hello tooensure risolta l'indirizzo può essere utilizzato correttamente.</span><span class="sxs-lookup"><span data-stu-id="6222b-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required tooensure hello resolved address can be used correctly.</span></span> <span data-ttu-id="6222b-161">Il client deve toodetect se il tentativo di connessione hello non riuscita a causa di un errore temporaneo e può essere recuperato (ad esempio, servizio spostato o è temporaneamente non disponibile), o un errore permanente (ad esempio, servizio è stato eliminato o hello risorsa richiesta non esiste più).</span><span class="sxs-lookup"><span data-stu-id="6222b-161">Your client needs toodetect whether hello connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or hello requested resource no longer exists).</span></span> <span data-ttu-id="6222b-162">Le istanze del servizio o repliche possono spostarsi dal nodo toonode in qualsiasi momento per diversi motivi.</span><span class="sxs-lookup"><span data-stu-id="6222b-162">Service instances or replicas can move around from node toonode at any time for multiple reasons.</span></span> <span data-ttu-id="6222b-163">indirizzo del servizio Hello risolto attraverso ServicePartitionResolver può essere aggiornato per il codice client tenta tooconnect tempo di hello.</span><span class="sxs-lookup"><span data-stu-id="6222b-163">hello service address resolved through ServicePartitionResolver may be stale by hello time your client code attempts tooconnect.</span></span> <span data-ttu-id="6222b-164">In tal caso nuovamente hello client deve disporre indirizzo hello toore risoluzione.</span><span class="sxs-lookup"><span data-stu-id="6222b-164">In that case again hello client needs toore-resolve hello address.</span></span> <span data-ttu-id="6222b-165">Fornendo hello precedente `ResolvedServicePartition` indica che hello nuovo resolver esigenze tootry anziché semplicemente recuperare un indirizzo memorizzato nella cache.</span><span class="sxs-lookup"><span data-stu-id="6222b-165">Providing hello previous `ResolvedServicePartition` indicates that hello resolver needs tootry again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="6222b-166">In genere, il codice client hello necessario non utilizzare hello ServicePartitionResolver direttamente.</span><span class="sxs-lookup"><span data-stu-id="6222b-166">Typically, hello client code need not work with hello ServicePartitionResolver directly.</span></span> <span data-ttu-id="6222b-167">E viene creato e passato nella factory client toocommunication in hello affidabile API dei servizi.</span><span class="sxs-lookup"><span data-stu-id="6222b-167">It is created and passed on toocommunication client factories in hello Reliable Services API.</span></span> <span data-ttu-id="6222b-168">factory Hello utilizzano resolver hello internamente toogenerate un oggetto client che può essere utilizzati toocommunicate con i servizi.</span><span class="sxs-lookup"><span data-stu-id="6222b-168">hello factories use hello resolver internally toogenerate a client object that can be used toocommunicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="6222b-169">Client e factory di comunicazione</span><span class="sxs-lookup"><span data-stu-id="6222b-169">Communication clients and factories</span></span>
<span data-ttu-id="6222b-170">libreria di factory di comunicazione Hello implementa un modello tipico di ripetere la gestione di errori che semplifica l'endpoint del servizio tooresolved connessioni nuovo tentativo.</span><span class="sxs-lookup"><span data-stu-id="6222b-170">hello communication factory library implements a typical fault-handling retry pattern that makes retrying connections tooresolved service endpoints easier.</span></span> <span data-ttu-id="6222b-171">raccolta di factory Hello fornisce il meccanismo di tentativi di hello mentre si forniscono i gestori degli errori di hello.</span><span class="sxs-lookup"><span data-stu-id="6222b-171">hello factory library provides hello retry mechanism while you provide hello error handlers.</span></span>

<span data-ttu-id="6222b-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`definisce l'interfaccia di base hello implementata da una factory di comunicazione client che produce i client che possono comunicare con il servizio di Service Fabric tooa.</span><span class="sxs-lookup"><span data-stu-id="6222b-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines hello base interface implemented by a communication client factory that produces clients that can talk tooa Service Fabric service.</span></span> <span data-ttu-id="6222b-173">Hello implementazione di hello che communicationclientfactory dipende da stack di comunicazione hello utilizzato dal servizio di Service Fabric hello in cui di desidera toocommunicate client hello.</span><span class="sxs-lookup"><span data-stu-id="6222b-173">hello implementation of hello CommunicationClientFactory depends on hello communication stack used by hello Service Fabric service where hello client wants toocommunicate.</span></span> <span data-ttu-id="6222b-174">Hello affidabile API dei servizi fornisce un `CommunicationClientFactoryBase<TCommunicationClient>`.</span><span class="sxs-lookup"><span data-stu-id="6222b-174">hello Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="6222b-175">Fornisce un'implementazione di base dell'interfaccia CommunicationClientFactory hello ed esegue attività, stack di comunicazione hello tooall comuni.</span><span class="sxs-lookup"><span data-stu-id="6222b-175">This provides a base implementation of hello CommunicationClientFactory interface and performs tasks that are common tooall hello communication stacks.</span></span> <span data-ttu-id="6222b-176">(Queste attività includono l'utilizzo di un endpoint del servizio hello toodetermine ServicePartitionResolver).</span><span class="sxs-lookup"><span data-stu-id="6222b-176">(These tasks include using a ServicePartitionResolver toodetermine hello service endpoint).</span></span> <span data-ttu-id="6222b-177">In genere, i client implementano hello astratta CommunicationClientFactoryBase classe toohandle la logica di stack di comunicazione toohello specifico.</span><span class="sxs-lookup"><span data-stu-id="6222b-177">Clients usually implement hello abstract CommunicationClientFactoryBase class toohandle logic that is specific toohello communication stack.</span></span>

<span data-ttu-id="6222b-178">client communication Hello appena riceve un indirizzo e lo usa tooconnect tooa servizio.</span><span class="sxs-lookup"><span data-stu-id="6222b-178">hello communication client just receives an address and uses it tooconnect tooa service.</span></span> <span data-ttu-id="6222b-179">client di Hello può utilizzare qualsiasi protocollo che desidera.</span><span class="sxs-lookup"><span data-stu-id="6222b-179">hello client can use whatever protocol it wants.</span></span>

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

<span data-ttu-id="6222b-180">factory Hello del client è responsabile della creazione di comunicazione client.</span><span class="sxs-lookup"><span data-stu-id="6222b-180">hello client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="6222b-181">Per i client che non mantengono una connessione permanente, ad esempio un client HTTP, factory hello deve solo toocreate e client hello restituito.</span><span class="sxs-lookup"><span data-stu-id="6222b-181">For clients that don't maintain a persistent connection, such as an HTTP client, hello factory only needs toocreate and return hello client.</span></span> <span data-ttu-id="6222b-182">Altri protocolli che mantengono una connessione permanente, ad esempio alcuni protocolli binari devono essere convalidati da hello factory toodetermine anche se la connessione hello deve toobe creato nuovamente.</span><span class="sxs-lookup"><span data-stu-id="6222b-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by hello factory toodetermine whether hello connection needs toobe re-created.</span></span>  

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

<span data-ttu-id="6222b-183">Infine, un gestore di eccezioni è responsabile di determinare quali tootake azione quando si verifica un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="6222b-183">Finally, an exception handler is responsible for determining what action tootake when an exception occurs.</span></span> <span data-ttu-id="6222b-184">Le eccezioni vengono suddivise nelle categorie **con possibilità di ritentare** e **senza possibilità di ritentare**.</span><span class="sxs-lookup"><span data-stu-id="6222b-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="6222b-185">**Non riproducibile** eccezioni semplicemente ottengano generata di nuovo indietro toohello chiamante.</span><span class="sxs-lookup"><span data-stu-id="6222b-185">**Non retryable** exceptions simply get rethrown back toohello caller.</span></span>
* <span data-ttu-id="6222b-186">Le eccezioni **con possibilità di ritentare** si suddividono a propria volta in due categorie: **temporanee** e **non temporanee**.</span><span class="sxs-lookup"><span data-stu-id="6222b-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="6222b-187">**Temporaneo** eccezioni sono quelli che è possibile ritentare semplicemente senza risolvere nuovamente l'indirizzo dell'endpoint servizio hello.</span><span class="sxs-lookup"><span data-stu-id="6222b-187">**Transient** exceptions are those that can simply be retried without re-resolving hello service endpoint address.</span></span> <span data-ttu-id="6222b-188">Ovvero problemi di rete temporanei o le risposte di errore di servizio diversi da quelli che indicano l'indirizzo dell'endpoint servizio hello non esiste.</span><span class="sxs-lookup"><span data-stu-id="6222b-188">These will include transient network problems or service error responses other than those that indicate hello service endpoint address does not exist.</span></span>
  * <span data-ttu-id="6222b-189">**Non temporaneo** eccezioni sono quelli che richiedono l'indirizzo dell'endpoint di hello servizio toobe nuovamente risolto.</span><span class="sxs-lookup"><span data-stu-id="6222b-189">**Non-transient** exceptions are those that require hello service endpoint address toobe re-resolved.</span></span> <span data-ttu-id="6222b-190">Sono incluse le eccezioni che indicano l'endpoint del servizio hello non è raggiungibile, che indica servizio hello è stato spostato tooa altro nodo.</span><span class="sxs-lookup"><span data-stu-id="6222b-190">These include exceptions that indicate hello service endpoint could not be reached, indicating hello service has moved tooa different node.</span></span>

<span data-ttu-id="6222b-191">Hello `TryHandleException` rende una decisione in una determinata eccezione.</span><span class="sxs-lookup"><span data-stu-id="6222b-191">hello `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="6222b-192">Se si **non conosce** toomake quali le decisioni relative a un'eccezione, dovrebbe restituire **false**.</span><span class="sxs-lookup"><span data-stu-id="6222b-192">If it **does not know** what decisions toomake about an exception, it should return **false**.</span></span> <span data-ttu-id="6222b-193">Se si **conoscere** toomake quali delle decisioni, deve impostare di conseguenza il risultato di hello e restituire **true**.</span><span class="sxs-lookup"><span data-stu-id="6222b-193">If it **does know** what decision toomake, it should set hello result accordingly and return **true**.</span></span>

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

        // if exceptionInformation.Exception is unknown (let hello next IExceptionHandler attempt toohandle it)
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

        /* if exceptionInformation.getException() is unknown (let hello next ExceptionHandler attempt toohandle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a><span data-ttu-id="6222b-194">Riassumendo</span><span class="sxs-lookup"><span data-stu-id="6222b-194">Putting it all together</span></span>
<span data-ttu-id="6222b-195">Con un `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, e `IExceptionHandler(C#) / ExceptionHandler(Java)` compilata in base a un protocollo di comunicazione, un `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` ne esegue il wrapping tutti insieme e fornisce la gestione di errori hello e ciclo di risoluzione indirizzi partizione del servizio per questi componenti.</span><span class="sxs-lookup"><span data-stu-id="6222b-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides hello fault-handling and service partition address resolution loop around these components.</span></span>

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with hello service using hello client.
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
      /* Communicate with hello service using hello client.
       */
   });

```

## <a name="next-steps"></a><span data-ttu-id="6222b-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6222b-196">Next steps</span></span>
* <span data-ttu-id="6222b-197">Vedere un esempio di comunicazione HTTP tra servizi in un [progetto di esempio C# in GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) o un [progetto di esempio Java in GitHub](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span><span class="sxs-lookup"><span data-stu-id="6222b-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="6222b-198">Chiamate di procedura remota con i Reliable Services remoti</span><span class="sxs-lookup"><span data-stu-id="6222b-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="6222b-199">Web API che usa OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="6222b-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="6222b-200">Comunicazione di WCF tramite Reliable Services</span><span class="sxs-lookup"><span data-stu-id="6222b-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
