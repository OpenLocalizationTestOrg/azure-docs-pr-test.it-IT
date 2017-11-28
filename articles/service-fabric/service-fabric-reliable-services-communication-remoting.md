---
title: comunicazione remota aaaService in Service Fabric | Documenti Microsoft
description: Comunicazione remota di Service Fabric consente ai client e servizi toocommunicate con servizi mediante una chiamata di procedura remota.
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
ms.openlocfilehash: 14682cf8671a85e04144eccf97803ab67c258875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="45da8-103">Servizio remoto con Reliable Services</span><span class="sxs-lookup"><span data-stu-id="45da8-103">Service remoting with Reliable Services</span></span>
<span data-ttu-id="45da8-104">Per i servizi che non sono legati tooa protocollo di comunicazione particolare o stack, ad esempio WebAPI, Windows Communication Foundation (WCF) o altri framework di servizi affidabili hello fornisce un tooquickly meccanismo di comunicazione remota e impostare facilmente la chiamata di procedura remota per i servizi.</span><span class="sxs-lookup"><span data-stu-id="45da8-104">For services that are not tied tooa particular communication protocol or stack, such as WebAPI, Windows Communication Foundation (WCF), or others, hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="45da8-105">Impostare la funzionalità remota in un servizio</span><span class="sxs-lookup"><span data-stu-id="45da8-105">Set up remoting on a service</span></span>
<span data-ttu-id="45da8-106">La procedura di impostazione della funzionalità remota per un servizio è costituita da due semplici passaggi.</span><span class="sxs-lookup"><span data-stu-id="45da8-106">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="45da8-107">Creare un'interfaccia per tooimplement il servizio.</span><span class="sxs-lookup"><span data-stu-id="45da8-107">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="45da8-108">Questa interfaccia definisce i metodi di hello che saranno disponibili per una chiamata di procedura remota nel servizio.</span><span class="sxs-lookup"><span data-stu-id="45da8-108">This interface defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="45da8-109">metodi di Hello devono essere restituzione attività metodi asincroni.</span><span class="sxs-lookup"><span data-stu-id="45da8-109">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="45da8-110">deve implementare l'interfaccia Hello `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal che hello servizio dispone di un'interfaccia di comunicazione remota.</span><span class="sxs-lookup"><span data-stu-id="45da8-110">hello interface must implement `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="45da8-111">Usare un listener di comunicazione remota nel servizio.</span><span class="sxs-lookup"><span data-stu-id="45da8-111">Use a remoting listener in your service.</span></span> <span data-ttu-id="45da8-112">Si tratta di un’implementazione `ICommunicationListener` che fornisce funzionalità di accesso remoto.</span><span class="sxs-lookup"><span data-stu-id="45da8-112">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="45da8-113">Hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` spazio dei nomi contiene un metodo di estensione,`CreateServiceRemotingListener` per stato e senza di servizi che possa essere utilizzati toocreate un listener di comunicazione remota utilizzando hello predefinito remoting protocollo di trasporto.</span><span class="sxs-lookup"><span data-stu-id="45da8-113">hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace contains an extension method,`CreateServiceRemotingListener` for both stateless and stateful services that can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="45da8-114">Nota: hello `Remoting` dello spazio dei nomi è disponibile come pacchetto nuget separato denominato`Microsoft.ServiceFabric.Services.Remoting`</span><span class="sxs-lookup"><span data-stu-id="45da8-114">Note: hello `Remoting` namespace is available as a seperate nuget package called `Microsoft.ServiceFabric.Services.Remoting`</span></span> 

<span data-ttu-id="45da8-115">Ad esempio, hello seguente senza stato servizio espone un singolo metodo tooget "Hello World", tramite una chiamata di procedura remota.</span><span class="sxs-lookup"><span data-stu-id="45da8-115">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

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
> <span data-ttu-id="45da8-116">Hello argomenti e hello restituiscono tipi di interfaccia di servizio hello possono essere qualsiasi tipo semplice, complesse o personalizzate, ma devono essere serializzabili per hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="45da8-116">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable by hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="45da8-117">Chiamare i metodi del servizio remoto</span><span class="sxs-lookup"><span data-stu-id="45da8-117">Call remote service methods</span></span>
<span data-ttu-id="45da8-118">Chiamata di metodi su un servizio usando hello stack di comunicazione remota viene eseguita tramite un servizio di toohello proxy locale tramite hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` classe.</span><span class="sxs-lookup"><span data-stu-id="45da8-118">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class.</span></span> <span data-ttu-id="45da8-119">Hello `ServiceProxy` metodo crea un proxy locale utilizzando la stessa interfaccia di servizio hello implementa hello.</span><span class="sxs-lookup"><span data-stu-id="45da8-119">hello `ServiceProxy` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="45da8-120">Con tale proxy, è sufficiente chiamare metodi sull'interfaccia hello in modalità remota.</span><span class="sxs-lookup"><span data-stu-id="45da8-120">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

<span data-ttu-id="45da8-121">framework remoting Hello propaga le eccezioni generate nel client di toohello hello del servizio.</span><span class="sxs-lookup"><span data-stu-id="45da8-121">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="45da8-122">La logica di gestione delle eccezioni così al client hello mediante `ServiceProxy` direttamente può gestire le eccezioni che hello servizio genera un'eccezione.</span><span class="sxs-lookup"><span data-stu-id="45da8-122">So exception-handling logic at hello client by using `ServiceProxy` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="45da8-123">Durata del proxy servizio</span><span class="sxs-lookup"><span data-stu-id="45da8-123">Service Proxy Lifetime</span></span>
<span data-ttu-id="45da8-124">La creazione del proxy servizio è un'operazione semplice, pertanto l'utente può creare quanti proxy desidera.</span><span class="sxs-lookup"><span data-stu-id="45da8-124">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="45da8-125">Il proxy servizio può essere usato più volte, fintanto che l'utente ne ha necessità.</span><span class="sxs-lookup"><span data-stu-id="45da8-125">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="45da8-126">Utente è possibile riutilizzare hello stesso proxy in caso di eccezione.</span><span class="sxs-lookup"><span data-stu-id="45da8-126">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="45da8-127">Ogni ServiceProxy contiene alla comunicazione client utilizzato toosend messaggi rete hello.</span><span class="sxs-lookup"><span data-stu-id="45da8-127">Each ServiceProxy contains communciation client used toosend messages over hello wire.</span></span> <span data-ttu-id="45da8-128">Durante la chiamata API, abbiamo toosee controllo interno se il client di comunicazione utilizzato è valido.</span><span class="sxs-lookup"><span data-stu-id="45da8-128">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="45da8-129">In base a tale risultato, vengono ricreate client communication hello.</span><span class="sxs-lookup"><span data-stu-id="45da8-129">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="45da8-130">Utente non è pertanto necessario serviceproxy toorecreate in caso di eccezione.</span><span class="sxs-lookup"><span data-stu-id="45da8-130">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="45da8-131">Durata di ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="45da8-131">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="45da8-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) è una factory che crea proxy per interfacce di connessione remota diverse.</span><span class="sxs-lookup"><span data-stu-id="45da8-132">[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="45da8-133">Se si utilizza l'API ServiceProxy.Create per la creazione di proxy, framework crea hello singelton ServiceProxyFactory.</span><span class="sxs-lookup"><span data-stu-id="45da8-133">If you use API ServiceProxy.Create for creating proxy, then framework creates hello singelton ServiceProxyFactory.</span></span>
<span data-ttu-id="45da8-134">È utile toocreate uno manualmente quando è necessario toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) proprietà.</span><span class="sxs-lookup"><span data-stu-id="45da8-134">It is useful toocreate one manually when you need toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) properties.</span></span>
<span data-ttu-id="45da8-135">La factory è un'operazione costosa.</span><span class="sxs-lookup"><span data-stu-id="45da8-135">Factory is an expensive operation.</span></span> <span data-ttu-id="45da8-136">ServiceProxyFactory gestisce la cache del client di comunicazione.</span><span class="sxs-lookup"><span data-stu-id="45da8-136">ServiceProxyFactory maintains cache of communication client.</span></span>
<span data-ttu-id="45da8-137">Procedura consigliata è toocache ServiceProxyFactory per maggior tempo possibile.</span><span class="sxs-lookup"><span data-stu-id="45da8-137">Best practice is toocache ServiceProxyFactory for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="45da8-138">Gestione delle eccezioni remote</span><span class="sxs-lookup"><span data-stu-id="45da8-138">Remoting Exception Handling</span></span>
<span data-ttu-id="45da8-139">Tutti hello remoto eccezione dall'API del servizio, vengono inviati toohello indietro client come AggregateException.</span><span class="sxs-lookup"><span data-stu-id="45da8-139">All hello remote exception thrown by service API, are sent back toohello client as AggregateException.</span></span> <span data-ttu-id="45da8-140">RemoteExceptions devono essere serializzabili DataContract; [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) generata toohello proxy API con errore di serializzazione hello in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="45da8-140">RemoteExceptions should be DataContract Serializable otherwise [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) is thrown toohello proxy API with hello serialization error in it.</span></span>

<span data-ttu-id="45da8-141">ServiceProxy gestire tutte le eccezioni Failover per la partizione del servizio hello viene creato per.</span><span class="sxs-lookup"><span data-stu-id="45da8-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="45da8-142">Risolve nuovamente endpoint hello nel caso di Failover Exceptions(Non-Transient Exceptions) ed effettua chiamate hello con endpoint corretto hello.</span><span class="sxs-lookup"><span data-stu-id="45da8-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="45da8-143">Il numero di tentativi per l'eccezione di failover è indefinito.</span><span class="sxs-lookup"><span data-stu-id="45da8-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="45da8-144">In caso di TransientExceptions, solo eseguire un nuovo tentativo chiamata hello.</span><span class="sxs-lookup"><span data-stu-id="45da8-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="45da8-145">Parametri di ripetizione dei tentativi predefiniti sono forniti da [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="45da8-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="45da8-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Utente può configurare questi valori passando OperationRetrySettings oggetto tooServiceProxyFactory costruttore.</span><span class="sxs-lookup"><span data-stu-id="45da8-146">(https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45da8-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45da8-147">Next steps</span></span>
* [<span data-ttu-id="45da8-148">Web API con OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="45da8-148">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="45da8-149">Comunicazione di WCF con Reliable Services</span><span class="sxs-lookup"><span data-stu-id="45da8-149">WCF communication with Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
* [<span data-ttu-id="45da8-150">Proteggere le comunicazioni per Reliable Services</span><span class="sxs-lookup"><span data-stu-id="45da8-150">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
