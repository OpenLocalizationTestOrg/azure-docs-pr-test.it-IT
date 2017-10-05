---
title: Stack di comunicazione WCF di Reliable Services | Documentazione Microsoft
description: Lo stack di comunicazione WCF integrato in Service Fabric consente la comunicazione client-servizio di WCF per Reliable Services.
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 75516e1e-ee57-4bc7-95fe-71ec42d452b2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/07/2017
ms.author: bharatn
ms.openlocfilehash: 7037620ebdc26a9f18531064bf45d058f5060e39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="618a5-103">Stack di comunicazione basato su WCF per Reliable Services</span><span class="sxs-lookup"><span data-stu-id="618a5-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="618a5-104">Il framework di Reliable Services consente agli autori del servizio di scegliere lo stack di comunicazione da usare per il servizio,</span><span class="sxs-lookup"><span data-stu-id="618a5-104">The Reliable Services framework allows service authors to choose the communication stack that they want to use for their service.</span></span> <span data-ttu-id="618a5-105">nonché di collegarsi allo stack di comunicazione scelto tramite l'oggetto **ICommunicationListener** restituito dai metodi [CreateServiceReplicaListeners o CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="618a5-105">They can plug in the communication stack of their choice via the **ICommunicationListener** returned from the [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="618a5-106">Il framework offre un'implementazione dello stack di comunicazione basata su Windows Communication Foundation (WCF) per gli autori del servizio che intendono usare la comunicazione basata su WCF.</span><span class="sxs-lookup"><span data-stu-id="618a5-106">The framework provides an implementation of the communication stack based on the Windows Communication Foundation (WCF) for service authors who want to use WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="618a5-107">Listener di comunicazione WCF</span><span class="sxs-lookup"><span data-stu-id="618a5-107">WCF Communication Listener</span></span>
<span data-ttu-id="618a5-108">L'implementazione specifica di WCF dell'oggetto **ICommunicationListener** viene fornita dalla classe **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener**.</span><span class="sxs-lookup"><span data-stu-id="618a5-108">The WCF-specific implementation of **ICommunicationListener** is provided by the **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="618a5-109">Si supponga di avere un contratto di servizio di tipo `ICalculator`</span><span class="sxs-lookup"><span data-stu-id="618a5-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="618a5-110">È possibile creare un listener di comunicazione WCF nel servizio come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="618a5-110">We can create a WCF communication listener in the service the following manner.</span></span>

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // The name of the endpoint configured in the ServiceManifest under the Endpoints section
            // that identifies the endpoint that the WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate the binding information that you want the service to use.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-the-wcf-communication-stack"></a><span data-ttu-id="618a5-111">Scrittura di client per lo stack di comunicazione WCF</span><span class="sxs-lookup"><span data-stu-id="618a5-111">Writing clients for the WCF communication stack</span></span>
<span data-ttu-id="618a5-112">Per consentire ai client di scrittura di comunicare con i servizi usando WCF, il framework fornisce l'oggetto **WcfClientCommunicationFactory**, ovvero l'implementazione specifica di WCF di [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="618a5-112">For writing clients to communicate with services by using WCF, the framework provides **WcfClientCommunicationFactory**, which is the WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="618a5-113">Il canale di comunicazione WCF è accessibile dall'oggetto **WcfCommunicationClient** creato da **WcfCommunicationClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="618a5-113">The WCF communication channel can be accessed from the **WcfCommunicationClient** created by the **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="618a5-114">Il codice client può usare **WcfCommunicationClientFactory** insieme a **WcfCommunicationClient** che implementa **ServicePartitionClient** per determinare l'endpoint del servizio e comunicare con esso.</span><span class="sxs-lookup"><span data-stu-id="618a5-114">Client code can use the **WcfCommunicationClientFactory** along with the **WcfCommunicationClient** which implements **ServicePartitionClient** to determine the service endpoint and communicate with the service.</span></span>

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with the ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call the service to perform the operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> <span data-ttu-id="618a5-115">L'oggetto ServicePartitionResolver predefinito presuppone che il client sia in esecuzione nello stesso cluster del servizio.</span><span class="sxs-lookup"><span data-stu-id="618a5-115">The default ServicePartitionResolver assumes that the client is running in same cluster as the service.</span></span> <span data-ttu-id="618a5-116">In caso contrario, creare un oggetto ServicePartitionResolver e passare gli endpoint di connessione del cluster.</span><span class="sxs-lookup"><span data-stu-id="618a5-116">If that is not the case, create a ServicePartitionResolver object and pass in the cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="618a5-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="618a5-117">Next steps</span></span>
* [<span data-ttu-id="618a5-118">Chiamata di procedura remota con i Reliable Services remoti</span><span class="sxs-lookup"><span data-stu-id="618a5-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="618a5-119">Web API con OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="618a5-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="618a5-120">Proteggere le comunicazioni per Reliable Services</span><span class="sxs-lookup"><span data-stu-id="618a5-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

