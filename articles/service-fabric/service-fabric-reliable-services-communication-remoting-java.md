---
title: comunicazione remota aaaService in Azure Service Fabric | Documenti Microsoft
description: Comunicazione remota di Service Fabric consente ai client e servizi toocommunicate con servizi mediante una chiamata di procedura remota.
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
ms.openlocfilehash: 1177a5ede91352dc61422f2df7424b0d5645147d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="bed92-103">Servizio remoto con Reliable Services</span><span class="sxs-lookup"><span data-stu-id="bed92-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bed92-104">C# su Windows</span><span class="sxs-lookup"><span data-stu-id="bed92-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="bed92-105">Java su Linux</span><span class="sxs-lookup"><span data-stu-id="bed92-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="bed92-106">framework servizi affidabili Hello fornisce un tooquickly meccanismo di comunicazione remota e configurare facilmente la chiamata di procedura remota per i servizi.</span><span class="sxs-lookup"><span data-stu-id="bed92-106">hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="bed92-107">Impostare la funzionalità remota in un servizio</span><span class="sxs-lookup"><span data-stu-id="bed92-107">Set up remoting on a service</span></span>
<span data-ttu-id="bed92-108">La procedura di impostazione della funzionalità remota per un servizio è costituita da due semplici passaggi.</span><span class="sxs-lookup"><span data-stu-id="bed92-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="bed92-109">Creare un'interfaccia per tooimplement il servizio.</span><span class="sxs-lookup"><span data-stu-id="bed92-109">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="bed92-110">Questa interfaccia definisce i metodi di hello disponibili per una chiamata di procedura remota nel servizio.</span><span class="sxs-lookup"><span data-stu-id="bed92-110">This interface defines hello methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="bed92-111">metodi di Hello devono essere restituzione attività metodi asincroni.</span><span class="sxs-lookup"><span data-stu-id="bed92-111">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="bed92-112">deve implementare l'interfaccia Hello `microsoft.serviceFabric.services.remoting.Service` toosignal che hello servizio dispone di un'interfaccia di comunicazione remota.</span><span class="sxs-lookup"><span data-stu-id="bed92-112">hello interface must implement `microsoft.serviceFabric.services.remoting.Service` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="bed92-113">Usare un listener di comunicazione remota nel servizio.</span><span class="sxs-lookup"><span data-stu-id="bed92-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="bed92-114">Si tratta di un’implementazione `CommunicationListener` che fornisce funzionalità di accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="bed92-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="bed92-115">`FabricTransportServiceRemotingListener`può essere un listener di comunicazione remota mediante protocollo di trasporto di comunicazione remota predefinito hello toocreate utilizzato.</span><span class="sxs-lookup"><span data-stu-id="bed92-115">`FabricTransportServiceRemotingListener` can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="bed92-116">Ad esempio, hello seguente senza stato servizio espone un singolo metodo tooget "Hello World", tramite una chiamata di procedura remota.</span><span class="sxs-lookup"><span data-stu-id="bed92-116">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="bed92-117">Hello e argomenti hello restituiscono tipi di interfaccia di servizio hello possono essere qualsiasi tipo semplice, complesse o personalizzate, ma che devono essere serializzabili.</span><span class="sxs-lookup"><span data-stu-id="bed92-117">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="bed92-118">Chiamare i metodi del servizio remoto</span><span class="sxs-lookup"><span data-stu-id="bed92-118">Call remote service methods</span></span>
<span data-ttu-id="bed92-119">Chiamata di metodi su un servizio usando hello stack di comunicazione remota viene eseguita tramite un servizio di toohello proxy locale tramite hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` classe.</span><span class="sxs-lookup"><span data-stu-id="bed92-119">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="bed92-120">Hello `ServiceProxyBase` metodo crea un proxy locale utilizzando la stessa interfaccia di servizio hello implementa hello.</span><span class="sxs-lookup"><span data-stu-id="bed92-120">hello `ServiceProxyBase` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="bed92-121">Con tale proxy, è sufficiente chiamare metodi sull'interfaccia hello in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="bed92-121">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="bed92-122">framework remoting Hello propaga le eccezioni generate nel client di toohello hello del servizio.</span><span class="sxs-lookup"><span data-stu-id="bed92-122">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="bed92-123">La logica di gestione delle eccezioni così al client hello mediante `ServiceProxyBase` direttamente può gestire le eccezioni che hello servizio genera un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="bed92-123">So exception-handling logic at hello client by using `ServiceProxyBase` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="bed92-124">Durata del proxy servizio</span><span class="sxs-lookup"><span data-stu-id="bed92-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="bed92-125">La creazione del proxy servizio è un'operazione semplice, pertanto l'utente può creare quanti proxy desidera.</span><span class="sxs-lookup"><span data-stu-id="bed92-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="bed92-126">Il proxy servizio può essere usato più volte, fintanto che l'utente ne ha necessità.</span><span class="sxs-lookup"><span data-stu-id="bed92-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="bed92-127">Utente è possibile riutilizzare hello stesso proxy in caso di eccezione.</span><span class="sxs-lookup"><span data-stu-id="bed92-127">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="bed92-128">Ogni ServiceProxy contiene i messaggi di comunicazione client utilizzato toosend rete hello.</span><span class="sxs-lookup"><span data-stu-id="bed92-128">Each ServiceProxy contains communication client used toosend messages over hello wire.</span></span> <span data-ttu-id="bed92-129">Durante la chiamata API, abbiamo toosee controllo interno se il client di comunicazione utilizzato è valido.</span><span class="sxs-lookup"><span data-stu-id="bed92-129">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="bed92-130">In base a tale risultato, vengono ricreate client communication hello.</span><span class="sxs-lookup"><span data-stu-id="bed92-130">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="bed92-131">Utente non è pertanto necessario serviceproxy toorecreate in caso di eccezione.</span><span class="sxs-lookup"><span data-stu-id="bed92-131">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="bed92-132">Durata di ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="bed92-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="bed92-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) è una factory che crea proxy per diverse interfacce di connessione remota.</span><span class="sxs-lookup"><span data-stu-id="bed92-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="bed92-134">Se si usa l'API `ServiceProxyBase.create` per la creazione del proxy, il framework crea una `FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="bed92-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="bed92-135">È utile toocreate uno manualmente quando è necessario toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) proprietà.</span><span class="sxs-lookup"><span data-stu-id="bed92-135">It is useful toocreate one manually when you need toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="bed92-136">La factory è un'operazione costosa.</span><span class="sxs-lookup"><span data-stu-id="bed92-136">Factory is an expensive operation.</span></span> <span data-ttu-id="bed92-137">`FabricServiceProxyFactory` gestisce la cache dei client di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="bed92-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="bed92-138">Procedura consigliata è toocache `FabricServiceProxyFactory` per maggior tempo possibile.</span><span class="sxs-lookup"><span data-stu-id="bed92-138">Best practice is toocache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="bed92-139">Gestione delle eccezioni remote</span><span class="sxs-lookup"><span data-stu-id="bed92-139">Remoting Exception Handling</span></span>
<span data-ttu-id="bed92-140">Tutti hello remoto eccezione dall'API del servizio, vengono inviati come RuntimeException o FabricException toohello indietro client.</span><span class="sxs-lookup"><span data-stu-id="bed92-140">All hello remote exception thrown by service API, are sent back toohello client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="bed92-141">ServiceProxy gestire tutte le eccezioni Failover per la partizione del servizio hello viene creato per.</span><span class="sxs-lookup"><span data-stu-id="bed92-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="bed92-142">Risolve nuovamente endpoint hello nel caso di Failover Exceptions(Non-Transient Exceptions) ed effettua chiamate hello con endpoint corretto hello.</span><span class="sxs-lookup"><span data-stu-id="bed92-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="bed92-143">Il numero di tentativi per l'eccezione di failover è indefinito.</span><span class="sxs-lookup"><span data-stu-id="bed92-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="bed92-144">In caso di TransientExceptions, solo eseguire un nuovo tentativo chiamata hello.</span><span class="sxs-lookup"><span data-stu-id="bed92-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="bed92-145">Parametri di ripetizione dei tentativi predefiniti sono forniti da [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="bed92-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="bed92-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Utente può configurare questi valori passando OperationRetrySettings oggetto tooServiceProxyFactory costruttore.</span><span class="sxs-lookup"><span data-stu-id="bed92-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bed92-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bed92-147">Next steps</span></span>
* [<span data-ttu-id="bed92-148">Proteggere le comunicazioni per Reliable Services</span><span class="sxs-lookup"><span data-stu-id="bed92-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
