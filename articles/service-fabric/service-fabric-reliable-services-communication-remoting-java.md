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
# <a name="service-remoting-with-reliable-services"></a>Servizio remoto con Reliable Services
> [!div class="op_single_selector"]
> * [C# su Windows](service-fabric-reliable-services-communication-remoting.md)
> * [Java su Linux](service-fabric-reliable-services-communication-remoting-java.md)
>
>

framework servizi affidabili Hello fornisce un tooquickly meccanismo di comunicazione remota e configurare facilmente la chiamata di procedura remota per i servizi.

## <a name="set-up-remoting-on-a-service"></a>Impostare la funzionalità remota in un servizio
La procedura di impostazione della funzionalità remota per un servizio è costituita da due semplici passaggi.

1. Creare un'interfaccia per tooimplement il servizio. Questa interfaccia definisce i metodi di hello disponibili per una chiamata di procedura remota nel servizio. metodi di Hello devono essere restituzione attività metodi asincroni. deve implementare l'interfaccia Hello `microsoft.serviceFabric.services.remoting.Service` toosignal che hello servizio dispone di un'interfaccia di comunicazione remota.
2. Usare un listener di comunicazione remota nel servizio. Si tratta di un’implementazione `CommunicationListener` che fornisce funzionalità di accesso remoto. `FabricTransportServiceRemotingListener`può essere un listener di comunicazione remota mediante protocollo di trasporto di comunicazione remota predefinito hello toocreate utilizzato.

Ad esempio, hello seguente senza stato servizio espone un singolo metodo tooget "Hello World", tramite una chiamata di procedura remota.

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
> Hello e argomenti hello restituiscono tipi di interfaccia di servizio hello possono essere qualsiasi tipo semplice, complesse o personalizzate, ma che devono essere serializzabili.
>
>

## <a name="call-remote-service-methods"></a>Chiamare i metodi del servizio remoto
Chiamata di metodi su un servizio usando hello stack di comunicazione remota viene eseguita tramite un servizio di toohello proxy locale tramite hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` classe. Hello `ServiceProxyBase` metodo crea un proxy locale utilizzando la stessa interfaccia di servizio hello implementa hello. Con tale proxy, è sufficiente chiamare metodi sull'interfaccia hello in modalità remota.

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

framework remoting Hello propaga le eccezioni generate nel client di toohello hello del servizio. La logica di gestione delle eccezioni così al client hello mediante `ServiceProxyBase` direttamente può gestire le eccezioni che hello servizio genera un'eccezione.

## <a name="service-proxy-lifetime"></a>Durata del proxy servizio
La creazione del proxy servizio è un'operazione semplice, pertanto l'utente può creare quanti proxy desidera. Il proxy servizio può essere usato più volte, fintanto che l'utente ne ha necessità. Utente è possibile riutilizzare hello stesso proxy in caso di eccezione. Ogni ServiceProxy contiene i messaggi di comunicazione client utilizzato toosend rete hello. Durante la chiamata API, abbiamo toosee controllo interno se il client di comunicazione utilizzato è valido. In base a tale risultato, vengono ricreate client communication hello. Utente non è pertanto necessario serviceproxy toorecreate in caso di eccezione.

### <a name="serviceproxyfactory-lifetime"></a>Durata di ServiceProxyFactory
[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) è una factory che crea proxy per diverse interfacce di connessione remota. Se si usa l'API `ServiceProxyBase.create` per la creazione del proxy, il framework crea una `FabricServiceProxyFactory`.
È utile toocreate uno manualmente quando è necessario toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) proprietà.
La factory è un'operazione costosa. `FabricServiceProxyFactory` gestisce la cache dei client di comunicazione.
Procedura consigliata è toocache `FabricServiceProxyFactory` per maggior tempo possibile.

## <a name="remoting-exception-handling"></a>Gestione delle eccezioni remote
Tutti hello remoto eccezione dall'API del servizio, vengono inviati come RuntimeException o FabricException toohello indietro client.

ServiceProxy gestire tutte le eccezioni Failover per la partizione del servizio hello viene creato per. Risolve nuovamente endpoint hello nel caso di Failover Exceptions(Non-Transient Exceptions) ed effettua chiamate hello con endpoint corretto hello. Il numero di tentativi per l'eccezione di failover è indefinito.
In caso di TransientExceptions, solo eseguire un nuovo tentativo chiamata hello.

Parametri di ripetizione dei tentativi predefiniti sono forniti da [OperationRetrySettings]. (https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Utente può configurare questi valori passando OperationRetrySettings oggetto tooServiceProxyFactory costruttore.

## <a name="next-steps"></a>Passaggi successivi
* [Proteggere le comunicazioni per Reliable Services](service-fabric-reliable-services-secure-communication.md)
