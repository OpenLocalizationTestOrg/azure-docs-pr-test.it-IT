---
title: "<span data-ttu-id=\"61195-101\">Funzionalità remota dei servizi in Service Fabric | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"61195-101\">Service remoting in Service Fabric | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"61195-102\">La funzionalità remota di Service Fabric consente a client e servizi di comunicare con i servizi tramite una chiamata di procedura remota.</span><span class=\"sxs-lookup\"><span data-stu-id=\"61195-102\">Service Fabric remoting allows clients and services to communicate with services by using a remote procedure call.</span></span>"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: abfaf430-fea0-4974-afba-cfc9f9f2354b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: vturecek
ms.openlocfilehash: 92a8894f24c234fbf38eda086531b524cceccfc1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="61195-103">Servizio remoto con Reliable Services</span><span class="sxs-lookup"><span data-stu-id="61195-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="61195-104">Per i servizi che non sono legati a un protocollo di comunicazione o uno stack particolare, ad esempio WebAPI, Windows Communication Foundation (WCF) o altri, il framework Reliable Services fornisce un meccanismo remoto per impostare in modo semplice e rapido una chiamata di procedura remota per i servizi.</span><span class="sxs-lookup"><span data-stu-id="61195-104">For services that are not tied to a particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, the Reliable Services framework provides a remoting mechanism to quickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="61195-105">Impostare la funzionalità remota in un servizio</span><span class="sxs-lookup"><span data-stu-id="61195-105">Set up remoting on a service</span></span>
<span data-ttu-id="61195-106">La procedura di impostazione della funzionalità remota per un servizio è costituita da due semplici passaggi.</span><span class="sxs-lookup"><span data-stu-id="61195-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="61195-107">Creare un'interfaccia per l'implementazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="61195-107">Create an interface for your service to implement.</span></span> <span data-ttu-id="61195-108">Questa interfaccia definisce i metodi che saranno disponibili per una chiamata di procedura remota nel servizio</span><span class="sxs-lookup"><span data-stu-id="61195-108">This interface defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="61195-109">e devono essere metodi asincroni di restituzione di attività.</span><span class="sxs-lookup"><span data-stu-id="61195-109">The methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="61195-110">L'interfaccia deve implementare `Microsoft.ServiceFabric.Services.Remoting.IService` per segnalare che il servizio dispone di un'interfaccia remota.</span><span class="sxs-lookup"><span data-stu-id="61195-110">The interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` to signal that the service has a remoting interface.</span></span>
2. <span data-ttu-id="61195-111">Usare un listener di comunicazione remota nel servizio.</span><span class="sxs-lookup"><span data-stu-id="61195-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="61195-112">Si tratta di un'implementazione `ICommunicationListener` che fornisce funzionalità di accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="61195-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="61195-113">Lo spazio dei nomi `Microsoft.ServiceFabric.Services.Remoting.Runtime` contiene un metodo di estensione `CreateServiceRemotingListener`, per i servizi con e senza stato, che può essere usato per creare un listener di comunicazione remota con il protocollo di trasporto predefinito per la comunicazione remota.</span><span class="sxs-lookup"><span data-stu-id="61195-113">The `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used to create a remoting listener using the default remoting transport protocol.</span></span>

<span data-ttu-id="61195-114">Nota: lo spazio dei nomi `Remoting` è disponibile come pacchetto NuGet separato denominato `Microsoft.ServiceFabric.Services.Remoting`</span><span class="sxs-lookup"><span data-stu-id="61195-114">Note: The `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="61195-115">Ad esempio, il servizio senza stato seguente espone un metodo singolo per ottenere "Hello World" su una chiamata RPC.</span><span class="sxs-lookup"><span data-stu-id="61195-115">For example, the following stateless service exposes a single method to get "Hello World" over a remote procedure call.</span></span>

```csharp
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Remoting;
using Microsoft.ServiceFabric.Services.Remoting.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

public interface IMyService : IService
{
    Task<string> HelloWorldAsync();
}

class MyService : StatelessService, IMyService
{
    public MyService(StatelessServiceContext context)
        : base (context)
    {
    }

    public Task HelloWorldAsync()
    {
        return Task.FromResult("Hello!");
    }

    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] { new ServiceInstanceListener(context =>            this.CreateServiceRemotingListener(context)) };
    }
}
```
> [!NOTE]
> <span data-ttu-id="61195-116">Gli argomenti e i tipi restituiti nell'interfaccia del servizio possono essere semplici, complessi o personalizzati ma, in tutti i casi, devono essere serializzabili mediante il serializzatore .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="61195-116">The arguments and the return types in the service interface can be any simple, complex, or custom types, but they must be serializable by the .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="61195-117">Chiamare i metodi del servizio remoto</span><span class="sxs-lookup"><span data-stu-id="61195-117">Call remote service methods</span></span>
<span data-ttu-id="61195-118">La chiamata dei metodi su un servizio mediante lo stack remoto viene eseguita usando un proxy locale al servizio tramite la classe `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` .</span><span class="sxs-lookup"><span data-stu-id="61195-118">Calling methods on a service by using the remoting stack is done by using a local proxy to the service through the `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="61195-119">Il metodo `ServiceProxy` crea un proxy locale usando la stessa interfaccia implementata dal servizio.</span><span class="sxs-lookup"><span data-stu-id="61195-119">The `ServiceProxy` method creates a local proxy by using the same interface that the service implements.</span></span> <span data-ttu-id="61195-120">Con tale proxy, è possibile semplicemente chiamare dei metodi nell'interfaccia in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="61195-120">With that proxy, you can simply call methods on the interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="61195-121">Il framework remoto propaga le eccezioni generate nel servizio al client.</span><span class="sxs-lookup"><span data-stu-id="61195-121">The remoting framework propagates exceptions thrown at the service to the client.</span></span> <span data-ttu-id="61195-122">La logica di gestione delle eccezioni nel client tramite `ServiceProxy` , quindi, è in grado di gestire direttamente le eccezioni generate dal servizio.</span><span class="sxs-lookup"><span data-stu-id="61195-122">So exception-handling logic at the client by using `ServiceProxy` can directly handle exceptions that the service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="61195-123">Durata del proxy servizio</span><span class="sxs-lookup"><span data-stu-id="61195-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="61195-124">La creazione del proxy servizio è un'operazione semplice, pertanto l'utente può creare quanti proxy desidera.</span><span class="sxs-lookup"><span data-stu-id="61195-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="61195-125">Il proxy servizio può essere usato più volte, fintanto che l'utente ne ha necessità.</span><span class="sxs-lookup"><span data-stu-id="61195-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="61195-126">L'utente può usare nuovamente lo stesso proxy in caso di eccezione.</span><span class="sxs-lookup"><span data-stu-id="61195-126">User can re-use the same proxy in case of Exception.</span></span> <span data-ttu-id="61195-127">Ogni proxy servizio contiene il client di comunicazione usato per inviare messaggi sulla rete.</span><span class="sxs-lookup"><span data-stu-id="61195-127">Each ServiceProxy contains communciation client used to send messages over the wire.</span></span> <span data-ttu-id="61195-128">Durante la chiamata all'API, vengono effettuati controlli interni per verificare se il client di comunicazione usato è valido.</span><span class="sxs-lookup"><span data-stu-id="61195-128">While invoking API, we have internal check to see if communication client used is valid.</span></span> <span data-ttu-id="61195-129">In base al risultato, il client di comunicazione viene ricreato.</span><span class="sxs-lookup"><span data-stu-id="61195-129">Based on that result, we re-create the communication client.</span></span> <span data-ttu-id="61195-130">L'utente non ha pertanto necessità di ricreare il proxy servizio in caso di eccezione.</span><span class="sxs-lookup"><span data-stu-id="61195-130">Hence user do not need to recreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="61195-131">Durata di ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="61195-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="61195-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) è una factory che crea proxy per interfacce di connessione remota diverse.</span><span class="sxs-lookup"><span data-stu-id="61195-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="61195-133">Se si usa ServiceProxy.Create API per la creazione di proxy, il framework crea la ServiceProxyFactory singleton.</span><span class="sxs-lookup"><span data-stu-id="61195-133">If you use API ServiceProxy.Create for creating proxy, then framework creates the singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="61195-134">È utile per crearne una manualmente quando è necessario eseguire l'override delle proprietà [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory).</span><span class="sxs-lookup"><span data-stu-id="61195-134">It is useful to create one manually when you need to override [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="61195-135">La factory è un'operazione costosa.</span><span class="sxs-lookup"><span data-stu-id="61195-135">Factory is an expensive operation.</span></span> <span data-ttu-id="61195-136">ServiceProxyFactory gestisce la cache del client di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="61195-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="61195-137">La procedura consigliata consiste nel memorizzare nella cache ServiceProxyFactory il più a lungo possibile.</span><span class="sxs-lookup"><span data-stu-id="61195-137">Best practice is to cache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="61195-138">Gestione delle eccezioni remote</span><span class="sxs-lookup"><span data-stu-id="61195-138">Remoting Exception Handling</span></span>
<span data-ttu-id="61195-139">Tutte le eccezioni generate dall'API del servizio vengono inviate nuovamente al client come AggregateException.</span><span class="sxs-lookup"><span data-stu-id="61195-139">All the remote exception thrown by service API, are sent back to the client as AggregateException.</span></span> <span data-ttu-id="61195-140">Le eccezioni remote devono essere serializzabili per DataContract; in caso contrario, viene generata una [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) nell'API del proxy contenente l'errore di serializzazione.</span><span class="sxs-lookup"><span data-stu-id="61195-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown to the proxy API with the serialization error in it.</span></span>

<span data-ttu-id="61195-141">Il proxy servizio non gestisce tutte le eccezioni di failover per la partizione del servizio per la quale è stato creato.</span><span class="sxs-lookup"><span data-stu-id="61195-141">ServiceProxy does handle all Failover Exception for the service partition it  is created for.</span></span> <span data-ttu-id="61195-142">Risolve nuovamente gli endpoint in presenza di eccezioni di failover (eccezioni non temporanee) e tenta di nuovo la chiamata con l'endpoint corretto.</span><span class="sxs-lookup"><span data-stu-id="61195-142">It re-resolves the endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries the call with the correct endpoint.</span></span> <span data-ttu-id="61195-143">Il numero di tentativi per l'eccezione di failover è indefinito.</span><span class="sxs-lookup"><span data-stu-id="61195-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="61195-144">In caso di eccezioni temporanee ritenta solo la chiamata.</span><span class="sxs-lookup"><span data-stu-id="61195-144">In case of TransientExceptions, it only retries the call.</span></span>

<span data-ttu-id="61195-145">Parametri di ripetizione dei tentativi predefiniti sono forniti da [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="61195-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="61195-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) L'utente può configurare questi valori passando l'oggetto OperationRetrySettings al costruttore di ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="61195-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object to ServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61195-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="61195-147">Next steps</span></span>
* [<span data-ttu-id="61195-148">Web API con OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="61195-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="61195-149">Comunicazione di WCF con Reliable Services</span><span class="sxs-lookup"><span data-stu-id="61195-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="61195-150">Proteggere le comunicazioni per Reliable Services</span><span class="sxs-lookup"><span data-stu-id="61195-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
