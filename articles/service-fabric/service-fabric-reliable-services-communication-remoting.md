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
# <a name="service-remoting-with-reliable-services"></a>Servizio remoto con Reliable Services
Per i servizi che non sono legati tooa protocollo di comunicazione particolare o stack, ad esempio WebAPI, Windows Communication Foundation (WCF) o altri framework di servizi affidabili hello fornisce un tooquickly meccanismo di comunicazione remota e impostare facilmente la chiamata di procedura remota per i servizi.

## <a name="set-up-remoting-on-a-service"></a>Impostare la funzionalità remota in un servizio
La procedura di impostazione della funzionalità remota per un servizio è costituita da due semplici passaggi.

1. Creare un'interfaccia per tooimplement il servizio. Questa interfaccia definisce i metodi di hello che saranno disponibili per una chiamata di procedura remota nel servizio. metodi di Hello devono essere restituzione attività metodi asincroni. deve implementare l'interfaccia Hello `Microsoft.ServiceFabric.Services.Remoting.IService` toosignal che hello servizio dispone di un'interfaccia di comunicazione remota.
2. Usare un listener di comunicazione remota nel servizio. Si tratta di un’implementazione `ICommunicationListener` che fornisce funzionalità di accesso remoto. Hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` spazio dei nomi contiene un metodo di estensione,`CreateServiceRemotingListener` per stato e senza di servizi che possa essere utilizzati toocreate un listener di comunicazione remota utilizzando hello predefinito remoting protocollo di trasporto.

Nota: hello `Remoting` dello spazio dei nomi è disponibile come pacchetto nuget separato denominato`Microsoft.ServiceFabric.Services.Remoting` 

Ad esempio, hello seguente senza stato servizio espone un singolo metodo tooget "Hello World", tramite una chiamata di procedura remota.

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
> Hello argomenti e hello restituiscono tipi di interfaccia di servizio hello possono essere qualsiasi tipo semplice, complesse o personalizzate, ma devono essere serializzabili per hello .NET [DataContractSerializer](https://msdn.microsoft.com/library/ms731923.aspx).
>
>

## <a name="call-remote-service-methods"></a>Chiamare i metodi del servizio remoto
Chiamata di metodi su un servizio usando hello stack di comunicazione remota viene eseguita tramite un servizio di toohello proxy locale tramite hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` classe. Hello `ServiceProxy` metodo crea un proxy locale utilizzando la stessa interfaccia di servizio hello implementa hello. Con tale proxy, è sufficiente chiamare metodi sull'interfaccia hello in modalità remota.

```csharp

IMyService helloWorldClient = ServiceProxy.Create<IMyService>(new Uri("fabric:/MyApplication/MyHelloWorldService"));

string message = await helloWorldClient.HelloWorldAsync();

```

framework remoting Hello propaga le eccezioni generate nel client di toohello hello del servizio. La logica di gestione delle eccezioni così al client hello mediante `ServiceProxy` direttamente può gestire le eccezioni che hello servizio genera un'eccezione.

## <a name="service-proxy-lifetime"></a>Durata del proxy servizio
La creazione del proxy servizio è un'operazione semplice, pertanto l'utente può creare quanti proxy desidera. Il proxy servizio può essere usato più volte, fintanto che l'utente ne ha necessità. Utente è possibile riutilizzare hello stesso proxy in caso di eccezione. Ogni ServiceProxy contiene alla comunicazione client utilizzato toosend messaggi rete hello. Durante la chiamata API, abbiamo toosee controllo interno se il client di comunicazione utilizzato è valido. In base a tale risultato, vengono ricreate client communication hello. Utente non è pertanto necessario serviceproxy toorecreate in caso di eccezione.

### <a name="serviceproxyfactory-lifetime"></a>Durata di ServiceProxyFactory
[ServiceProxyFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.serviceproxyfactory) è una factory che crea proxy per interfacce di connessione remota diverse. Se si utilizza l'API ServiceProxy.Create per la creazione di proxy, framework crea hello singelton ServiceProxyFactory.
È utile toocreate uno manualmente quando è necessario toooverride [IServiceRemotingClientFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.remoting.client.iserviceremotingclientfactory) proprietà.
La factory è un'operazione costosa. ServiceProxyFactory gestisce la cache del client di comunicazione.
Procedura consigliata è toocache ServiceProxyFactory per maggior tempo possibile.

## <a name="remoting-exception-handling"></a>Gestione delle eccezioni remote
Tutti hello remoto eccezione dall'API del servizio, vengono inviati toohello indietro client come AggregateException. RemoteExceptions devono essere serializzabili DataContract; [ServiceException](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.serviceexception) generata toohello proxy API con errore di serializzazione hello in essa contenuti.

ServiceProxy gestire tutte le eccezioni Failover per la partizione del servizio hello viene creato per. Risolve nuovamente endpoint hello nel caso di Failover Exceptions(Non-Transient Exceptions) ed effettua chiamate hello con endpoint corretto hello. Il numero di tentativi per l'eccezione di failover è indefinito.
In caso di TransientExceptions, solo eseguire un nuovo tentativo chiamata hello.

Parametri di ripetizione dei tentativi predefiniti sono forniti da [OperationRetrySettings]. (https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.services.communication.client.operationretrysettings) Utente può configurare questi valori passando OperationRetrySettings oggetto tooServiceProxyFactory costruttore.

## <a name="next-steps"></a>Passaggi successivi
* [Web API con OWIN in Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Comunicazione di WCF con Reliable Services](service-fabric-reliable-services-communication-wcf.md)
* [Proteggere le comunicazioni per Reliable Services](service-fabric-reliable-services-secure-communication.md)
