---
title: Servizio remoto con Azure Service Fabric | Microsoft Docs
description: "La funzionalità remota di Service Fabric consente a client e servizi di comunicare con i servizi tramite una chiamata di procedura remota."
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: dc4a362b5737bb424ca2c196c85f4c51b6ee5e30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="3feb0-103">Servizio remoto con Reliable Services</span><span class="sxs-lookup"><span data-stu-id="3feb0-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3feb0-104">C# su Windows</span><span class="sxs-lookup"><span data-stu-id="3feb0-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="3feb0-105">Java su Linux</span><span class="sxs-lookup"><span data-stu-id="3feb0-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="3feb0-106">Il framework Reliable Services fornisce un meccanismo remoto per impostare in modo semplice e rapido una chiamata di procedura remota per i servizi.</span><span class="sxs-lookup"><span data-stu-id="3feb0-106">The Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="3feb0-107">Impostare la funzionalità remota in un servizio</span><span class="sxs-lookup"><span data-stu-id="3feb0-107">Set up remoting on a service</span></span>
<span data-ttu-id="3feb0-108">La procedura di impostazione della funzionalità remota per un servizio è costituita da due semplici passaggi.</span><span class="sxs-lookup"><span data-stu-id="3feb0-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="3feb0-109">Creare un'interfaccia per l’implementazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="3feb0-109">Create an interface for your service to implement.</span></span> <span data-ttu-id="3feb0-110">Questa interfaccia definisce i metodi che sono disponibili per una chiamata di procedura remota nel servizio</span><span class="sxs-lookup"><span data-stu-id="3feb0-110">This interface defines the methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="3feb0-111">e devono essere metodi asincroni di restituzione di attività.</span><span class="sxs-lookup"><span data-stu-id="3feb0-111">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="3feb0-112">L'interfaccia deve implementare `microsoft.serviceFabric.services.remoting.Service` per segnalare che il servizio dispone di un'interfaccia remota.</span><span class="sxs-lookup"><span data-stu-id="3feb0-112">The interface must implement `microsoft.serviceFabric.services.remoting.Service` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="3feb0-113">Usare un listener di comunicazione remota nel servizio.</span><span class="sxs-lookup"><span data-stu-id="3feb0-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="3feb0-114">Si tratta di un’implementazione `CommunicationListener` che fornisce funzionalità di accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="3feb0-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="3feb0-115">`FabricTransportServiceRemotingListener` può essere usato per creare un listener di comunicazione remota con il protocollo di trasporto predefinito per la comunicazione remota.</span><span class="sxs-lookup"><span data-stu-id="3feb0-115">`FabricTransportServiceRemotingListener` can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="3feb0-116">Ad esempio, il servizio senza stato seguente espone un metodo singolo per ottenere "Hello World" su una chiamata RPC.</span><span class="sxs-lookup"><span data-stu-id="3feb0-116">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

```java
import java.util.ArrayList;
import java.util.concurrent.CompletableFuture;
import java.util.List;
import microsoft.servicefabric.services.communication.runtime.ServiceInstanceListener;
import microsoft.servicefabric.services.remoting.Service;
import microsoft.servicefabric.services.runtime.StatelessService;

public interface MyService extends Service {
    CompletableFuture<String> helloWorldAsync();
}

class MyServiceImpl extends StatelessService implements MyService {
    public MyServiceImpl(StatelessServiceContext context) {
       super(context);
    }

    public CompletableFuture<String> helloWorldAsync() {
        return CompletableFuture.completedFuture("Hello!");
    }

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
        listeners.add(new ServiceInstanceListener((context) -> {
            return new FabricTransportServiceRemotingListener(context,this);
        }));
        return listeners;
    }
}
```

> [!NOTE]
> <span data-ttu-id="3feb0-117">Gli argomenti e i tipi restituiti nell'interfaccia del servizio possono essere semplici, complessi o personalizzati ma, in tutti i casi, devono essere serializzabili.</span><span class="sxs-lookup"><span data-stu-id="3feb0-117">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="3feb0-118">Chiamare i metodi del servizio remoto</span><span class="sxs-lookup"><span data-stu-id="3feb0-118">Call remote service methods</span></span>
<span data-ttu-id="3feb0-119">La chiamata dei metodi su un servizio mediante lo stack remoto viene eseguita usando un proxy locale al servizio tramite la classe `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` .</span><span class="sxs-lookup"><span data-stu-id="3feb0-119">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="3feb0-120">Il metodo `ServiceProxyBase` crea un proxy locale usando la stessa interfaccia implementata dal servizio.</span><span class="sxs-lookup"><span data-stu-id="3feb0-120">The `ServiceProxyBase` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="3feb0-121">Con tale proxy, è possibile semplicemente chiamare dei metodi nell'interfaccia in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="3feb0-121">With that proxy, you can simply call methods on the interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="3feb0-122">Il framework remoto propaga le eccezioni generate nel servizio al client.</span><span class="sxs-lookup"><span data-stu-id="3feb0-122">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="3feb0-123">La logica di gestione delle eccezioni nel client tramite `ServiceProxyBase` , quindi, è in grado di gestire direttamente le eccezioni generate dal servizio.</span><span class="sxs-lookup"><span data-stu-id="3feb0-123">So exception-handling logic at the client by using `ServiceProxyBase` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="3feb0-124">Durata del proxy servizio</span><span class="sxs-lookup"><span data-stu-id="3feb0-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="3feb0-125">La creazione del proxy servizio è un'operazione semplice, pertanto l'utente può creare quanti proxy desidera.</span><span class="sxs-lookup"><span data-stu-id="3feb0-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="3feb0-126">Il proxy servizio può essere usato più volte, fintanto che l'utente ne ha necessità.</span><span class="sxs-lookup"><span data-stu-id="3feb0-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="3feb0-127">L'utente può usare nuovamente lo stesso proxy in caso di eccezione.</span><span class="sxs-lookup"><span data-stu-id="3feb0-127">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="3feb0-128">Ogni ServiceProxy contiene il client di comunicazione usato per inviare messaggi sulla rete.</span><span class="sxs-lookup"><span data-stu-id="3feb0-128">Each ServiceProxy contains communication client used to send messages over the wire.</span></span> <span data-ttu-id="3feb0-129">Durante la chiamata all'API, vengono effettuati controlli interni per verificare se il client di comunicazione usato è valido.</span><span class="sxs-lookup"><span data-stu-id="3feb0-129">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="3feb0-130">In base al risultato, il client di comunicazione viene ricreato.</span><span class="sxs-lookup"><span data-stu-id="3feb0-130">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="3feb0-131">L'utente non ha pertanto necessità di ricreare il proxy servizio in caso di eccezione.</span><span class="sxs-lookup"><span data-stu-id="3feb0-131">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="3feb0-132">Durata di ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="3feb0-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="3feb0-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) è una factory che crea proxy per diverse interfacce di connessione remota.</span><span class="sxs-lookup"><span data-stu-id="3feb0-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="3feb0-134">Se si usa l'API `ServiceProxyBase.create` per la creazione del proxy, il framework crea una `FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="3feb0-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="3feb0-135">È utile per crearne una manualmente quando è necessario eseguire l'override delle proprietà [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory).</span><span class="sxs-lookup"><span data-stu-id="3feb0-135">It is useful to create one manually when you need to override [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="3feb0-136">La factory è un'operazione costosa.</span><span class="sxs-lookup"><span data-stu-id="3feb0-136">Factory is an expensive operation.</span></span> <span data-ttu-id="3feb0-137">`FabricServiceProxyFactory` gestisce la cache dei client di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="3feb0-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="3feb0-138">La procedura consigliata consiste nel mantenere `FabricServiceProxyFactory` memorizzato nella cache il più a lungo possibile.</span><span class="sxs-lookup"><span data-stu-id="3feb0-138">Best practice is to cache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="3feb0-139">Gestione delle eccezioni remote</span><span class="sxs-lookup"><span data-stu-id="3feb0-139">Remoting Exception Handling</span></span>
<span data-ttu-id="3feb0-140">Tutte le eccezioni generate dall'API del servizio vengono inviate nuovamente al client come RuntimeException o FabricException.</span><span class="sxs-lookup"><span data-stu-id="3feb0-140">All the remote exception thrown by service API, are sent back to the client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="3feb0-141">Il proxy servizio non gestisce tutte le eccezioni di failover per la partizione del servizio per la quale è stato creato.</span><span class="sxs-lookup"><span data-stu-id="3feb0-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="3feb0-142">Risolve nuovamente gli endpoint in presenza di eccezioni di failover (eccezioni non temporanee) e tenta di nuovo la chiamata con l'endpoint corretto.</span><span class="sxs-lookup"><span data-stu-id="3feb0-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="3feb0-143">Il numero di tentativi per l'eccezione di failover è indefinito.</span><span class="sxs-lookup"><span data-stu-id="3feb0-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="3feb0-144">In caso di eccezioni temporanee ritenta solo la chiamata.</span><span class="sxs-lookup"><span data-stu-id="3feb0-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="3feb0-145">Parametri di ripetizione dei tentativi predefiniti sono forniti da [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="3feb0-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="3feb0-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) L'utente può configurare questi valori passando l'oggetto OperationRetrySettings al costruttore di ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="3feb0-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3feb0-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3feb0-147">Next steps</span></span>
* [<span data-ttu-id="3feb0-148">Proteggere le comunicazioni per Reliable Services</span><span class="sxs-lookup"><span data-stu-id="3feb0-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
