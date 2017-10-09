---
title: stack di comunicazione di servizi WCF aaaReliable | Documenti Microsoft
description: Hello predefiniti WCF stack di comunicazione nell'infrastruttura del servizio fornisce la comunicazione WCF il servizio client per servizi affidabili.
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
ms.openlocfilehash: 7feebef4d46a6ae66d05129f47f9b5911e82aec9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="wcf-based-communication-stack-for-reliable-services"></a><span data-ttu-id="8775d-103">Stack di comunicazione basato su WCF per Reliable Services</span><span class="sxs-lookup"><span data-stu-id="8775d-103">WCF-based communication stack for Reliable Services</span></span>
<span data-ttu-id="8775d-104">Hello servizi affidabili framework consente dello stack comunicazione hello toochoose autori che desiderano toouse per il servizio del servizio.</span><span class="sxs-lookup"><span data-stu-id="8775d-104">hello Reliable Services framework allows service authors toochoose hello communication stack that they want toouse for their service.</span></span> <span data-ttu-id="8775d-105">Può essere inserito nello stack di comunicazione hello di loro scelta tramite hello **ICommunicationListener** restituito da hello [CreateServiceReplicaListeners o CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) metodi.</span><span class="sxs-lookup"><span data-stu-id="8775d-105">They can plug in hello communication stack of their choice via hello **ICommunicationListener** returned from hello [CreateServiceReplicaListeners or CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) methods.</span></span> <span data-ttu-id="8775d-106">framework Hello fornisce un'implementazione dello stack di comunicazione hello basati su hello Windows Communication Foundation (WCF) per gli autori del servizio che desidera toouse comunicazioni basate su WCF.</span><span class="sxs-lookup"><span data-stu-id="8775d-106">hello framework provides an implementation of hello communication stack based on hello Windows Communication Foundation (WCF) for service authors who want toouse WCF-based communication.</span></span>

## <a name="wcf-communication-listener"></a><span data-ttu-id="8775d-107">Listener di comunicazione WCF</span><span class="sxs-lookup"><span data-stu-id="8775d-107">WCF Communication Listener</span></span>
<span data-ttu-id="8775d-108">implementazione di Hello WCF specifiche di **ICommunicationListener** viene fornito da hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** classe.</span><span class="sxs-lookup"><span data-stu-id="8775d-108">hello WCF-specific implementation of **ICommunicationListener** is provided by hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** class.</span></span>

<span data-ttu-id="8775d-109">Si supponga di avere un contratto di servizio di tipo `ICalculator`</span><span class="sxs-lookup"><span data-stu-id="8775d-109">Lest say we have a service contract of type `ICalculator`</span></span>

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

<span data-ttu-id="8775d-110">È possibile creare un listener di comunicazione WCF in hello servizio hello seguente modo.</span><span class="sxs-lookup"><span data-stu-id="8775d-110">We can create a WCF communication listener in hello service hello following manner.</span></span>

```csharp

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[] { new ServiceReplicaListener((context) =>
        new WcfCommunicationListener<ICalculator>(
            wcfServiceObject:this,
            serviceContext:context,
            //
            // hello name of hello endpoint configured in hello ServiceManifest under hello Endpoints section
            // that identifies hello endpoint that hello WCF ServiceHost should listen on.
            //
            endpointResourceName: "WcfServiceEndpoint",

            //
            // Populate hello binding information that you want hello service toouse.
            //
            listenerBinding: WcfUtility.CreateTcpListenerBinding()
        )
    )};
}

```

## <a name="writing-clients-for-hello-wcf-communication-stack"></a><span data-ttu-id="8775d-111">Scrittura di client per lo stack di comunicazione WCF hello</span><span class="sxs-lookup"><span data-stu-id="8775d-111">Writing clients for hello WCF communication stack</span></span>
<span data-ttu-id="8775d-112">Per la scrittura di client toocommunicate con i servizi con WCF, il framework di hello fornisce **WcfClientCommunicationFactory**, che rappresenta l'implementazione di hello WCF specifiche di [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="8775d-112">For writing clients toocommunicate with services by using WCF, hello framework provides **WcfClientCommunicationFactory**, which is hello WCF-specific implementation of [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).</span></span>

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

<span data-ttu-id="8775d-113">il canale di comunicazione WCF Hello è possibile accedere da hello **WcfCommunicationClient** creato da hello **WcfCommunicationClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="8775d-113">hello WCF communication channel can be accessed from hello **WcfCommunicationClient** created by hello **WcfCommunicationClientFactory**.</span></span>

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

<span data-ttu-id="8775d-114">Il codice client può utilizzare hello **WcfCommunicationClientFactory** insieme hello **WcfCommunicationClient** che implementa l'interfaccia **ServicePartitionClient** toodetermine endpoint del servizio di Hello e comunicare con il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="8775d-114">Client code can use hello **WcfCommunicationClientFactory** along with hello **WcfCommunicationClient** which implements **ServicePartitionClient** toodetermine hello service endpoint and communicate with hello service.</span></span>

```csharp
// Create binding
Binding binding = WcfUtility.CreateTcpClientBinding();
// Create a partition resolver
IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();
// create a  WcfCommunicationClientFactory object.
var wcfClientFactory = new WcfCommunicationClientFactory<ICalculator>
    (clientBinding: binding, servicePartitionResolver: partitionResolver);

//
// Create a client for communicating with hello ICalculator service that has been created with the
// Singleton partition scheme.
//
var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
                wcfClientFactory,
                ServiceUri,
                ServicePartitionKey.Singleton);

//
// Call hello service tooperform hello operation.
//
var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
                client => client.Channel.Add(2, 3)).Result;

```
> [!NOTE]
> <span data-ttu-id="8775d-115">predefinito Hello ServicePartitionResolver si presuppone che il client hello è in esecuzione nel servizio hello nello stesso cluster.</span><span class="sxs-lookup"><span data-stu-id="8775d-115">hello default ServicePartitionResolver assumes that hello client is running in same cluster as hello service.</span></span> <span data-ttu-id="8775d-116">In caso non hello, creare un oggetto ServicePartitionResolver e passare gli endpoint di connessione di hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="8775d-116">If that is not hello case, create a ServicePartitionResolver object and pass in hello cluster connection endpoints.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8775d-117">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8775d-117">Next steps</span></span>
* [<span data-ttu-id="8775d-118">Chiamata di procedura remota con i Reliable Services remoti</span><span class="sxs-lookup"><span data-stu-id="8775d-118">Remote procedure call with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="8775d-119">Web API con OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="8775d-119">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="8775d-120">Proteggere le comunicazioni per Reliable Services</span><span class="sxs-lookup"><span data-stu-id="8775d-120">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)

