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
# <a name="wcf-based-communication-stack-for-reliable-services"></a>Stack di comunicazione basato su WCF per Reliable Services
Hello servizi affidabili framework consente dello stack comunicazione hello toochoose autori che desiderano toouse per il servizio del servizio. Può essere inserito nello stack di comunicazione hello di loro scelta tramite hello **ICommunicationListener** restituito da hello [CreateServiceReplicaListeners o CreateServiceInstanceListeners](service-fabric-reliable-services-communication.md) metodi. framework Hello fornisce un'implementazione dello stack di comunicazione hello basati su hello Windows Communication Foundation (WCF) per gli autori del servizio che desidera toouse comunicazioni basate su WCF.

## <a name="wcf-communication-listener"></a>Listener di comunicazione WCF
implementazione di Hello WCF specifiche di **ICommunicationListener** viene fornito da hello **Microsoft.ServiceFabric.Services.Communication.Wcf.Runtime.WcfCommunicationListener** classe.

Si supponga di avere un contratto di servizio di tipo `ICalculator`

```csharp
[ServiceContract]
public interface ICalculator
{
    [OperationContract]
    Task<int> Add(int value1, int value2);
}
```

È possibile creare un listener di comunicazione WCF in hello servizio hello seguente modo.

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

## <a name="writing-clients-for-hello-wcf-communication-stack"></a>Scrittura di client per lo stack di comunicazione WCF hello
Per la scrittura di client toocommunicate con i servizi con WCF, il framework di hello fornisce **WcfClientCommunicationFactory**, che rappresenta l'implementazione di hello WCF specifiche di [ClientCommunicationFactoryBase](service-fabric-reliable-services-communication.md).

```csharp

public WcfCommunicationClientFactory(
    Binding clientBinding = null,
    IEnumerable<IExceptionHandler> exceptionHandlers = null,
    IServicePartitionResolver servicePartitionResolver = null,
    string traceId = null,
    object callback = null);
```

il canale di comunicazione WCF Hello è possibile accedere da hello **WcfCommunicationClient** creato da hello **WcfCommunicationClientFactory**.

```csharp

public class WcfCommunicationClient : ServicePartitionClient<WcfCommunicationClient<ICalculator>>
   {
       public WcfCommunicationClient(ICommunicationClientFactory<WcfCommunicationClient<ICalculator>> communicationClientFactory, Uri serviceUri, ServicePartitionKey partitionKey = null, TargetReplicaSelector targetReplicaSelector = TargetReplicaSelector.Default, string listenerName = null, OperationRetrySettings retrySettings = null)
           : base(communicationClientFactory, serviceUri, partitionKey, targetReplicaSelector, listenerName, retrySettings)
       {
       }
   }

```

Il codice client può utilizzare hello **WcfCommunicationClientFactory** insieme hello **WcfCommunicationClient** che implementa l'interfaccia **ServicePartitionClient** toodetermine endpoint del servizio di Hello e comunicare con il servizio di hello.

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
> predefinito Hello ServicePartitionResolver si presuppone che il client hello è in esecuzione nel servizio hello nello stesso cluster. In caso non hello, creare un oggetto ServicePartitionResolver e passare gli endpoint di connessione di hello del cluster.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* [Chiamata di procedura remota con i Reliable Services remoti](service-fabric-reliable-services-communication-remoting.md)
* [Web API con OWIN in Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Proteggere le comunicazioni per Reliable Services](service-fabric-reliable-services-secure-communication.md)

