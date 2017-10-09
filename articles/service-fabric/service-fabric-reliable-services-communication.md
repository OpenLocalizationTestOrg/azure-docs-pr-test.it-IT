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
# <a name="how-toouse-hello-reliable-services-communication-apis"></a>Come toouse hello API di comunicazione tra servizi affidabili
Azure Service Fabric è una piattaforma completamente indipendente dalle comunicazioni tra servizi. Tutti i protocolli e gli stack sono accettabili, da tooHTTP UDP. È la modalità in cui devono comunicare servizi attivo toohello servizio developer toochoose. Hello servizi affidabili application framework fornisce stack di comunicazione predefinita nonché API che è possibile utilizzare toobuild i componenti personalizzate di comunicazione.

## <a name="set-up-service-communication"></a>Impostare la comunicazione tra servizi
Hello affidabile API dei servizi utilizza un'interfaccia semplice per le comunicazioni di servizio. tooopen un endpoint per il servizio, è sufficiente implementare questa interfaccia:

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

Aggiungere quindi l'implementazione del listener di comunicazione restituendola in un override del metodo della classe di base del servizio.

Per i servizi senza stato:

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

Per i servizi con stato:

> [!NOTE]
> Reliable Services con stato non è ancora supportato in Java.
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

In entrambi i casi restituire una raccolta di listener. In questo modo il servizio toolisten su più endpoint, potenzialmente utilizzando protocolli diversi, utilizzando più listener. Può essere ad esempio presente un listener HTTP e un listener WebSocket separato. Ogni listener riceve un nome e un insieme risultante di hello di *nome: indirizzo* coppie sono rappresentate come un oggetto JSON quando un client richiede indirizzi di ascolto hello per un'istanza del servizio o una partizione.

In un servizio senza stato, hello override restituisce una raccolta di ServiceInstanceListeners. Oggetto `ServiceInstanceListener` toocreate una funzione contiene un `ICommunicationListener(C#) / CommunicationListener(Java)` e viene assegnato un nome. Per i servizi con stati, hello override restituisce una raccolta di ServiceReplicaListeners. Questo è leggermente diverso rispetto alla controparte senza stata, perché un `ServiceReplicaListener` è un'opzione tooopen un `ICommunicationListener` nelle repliche secondarie. Ciò consente non solo di usare più listener di comunicazione in un servizio, ma anche di specificare quali listener accettano le richieste nelle repliche secondarie e quali si limitano a rimanere in ascolto sulle repliche primarie.

Ad esempio, un oggetto ServiceRemotingListener può gestire le chiamate RPC solo sulle repliche primarie, mentre un secondo listener personalizzato può accettare le richieste di lettura sulle repliche secondarie tramite HTTP:

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
> Quando si creano più listener per un servizio, a ogni listener **deve** essere assegnato un nome univoco.
>
>

Infine, descrivere l'endpoint di hello che sono necessarie per il servizio di hello in hello [manifesto del servizio](service-fabric-application-model.md) nella sezione hello sugli endpoint.

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

listener di comunicazione Hello possono accedere alle risorse di endpoint di hello allocate tooit da hello `CodePackageActivationContext` in hello `ServiceContext`. listener Hello è quindi possibile avviare l'ascolto delle richieste quando viene aperto.

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> Risorse endpoint sono pacchetto del servizio intero toohello comuni e vengono allocati dall'infrastruttura del servizio quando viene attivato il pacchetto di servizio hello. Più repliche del servizio ospitate in hello stesso ServiceHost possono condividere hello stessa porta. Ciò significa che il listener di comunicazione hello deve supportare la condivisione delle porte. Hello consiglia modo di procedere per hello comunicazione listener toouse hello partizione ID e l'ID e l'istanza di replica durante la generazione di indirizzo di ascolto hello.
>
>

### <a name="service-address-registration"></a>Registrazione dell'indirizzo del servizio
Un servizio di sistema denominato hello *Naming Service* viene eseguito nei cluster di Service Fabric. Hello Naming Service è un programma di registrazione per servizi e i rispettivi indirizzi che ogni istanza o una replica del servizio hello è in ascolto. Quando hello `OpenAsync(C#) / openAsync(Java)` metodo di un `ICommunicationListener(C#) / CommunicationListener(Java)` viene completato, il suo ritorno valore ottiene registrato nel servizio di denominazione hello. Valore che ottiene hello pubblicata nel servizio di denominazione è una stringa il cui valore può essere del tutto qualsiasi questo restituito. Questo valore di stringa è ciò che i client visualizzato quando si richiedono un indirizzo per il servizio di hello dal servizio di denominazione hello.

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

Service Fabric fornisce API che consentono di client e altri servizi toothen chiedere per questo indirizzo dal nome del servizio. Questo è importante perché l'indirizzo del servizio hello non è statico. Servizi vengono spostati nel cluster hello per scopi di bilanciamento del carico e disponibilità delle risorse. Questo è il meccanismo hello che consentono ai client hello tooresolve indirizzo per un servizio in ascolto.

> [!NOTE]
> Per una procedura completa di come toowrite un listener di comunicazione, vedere [servizi API Web dell'infrastruttura del servizio con self-hosting OWIN](service-fabric-reliable-services-communication-webapi.md) per c#, mentre per Java è possibile scrivere la propria implementazione di server HTTP, vedere applicazione EchoServer esempio a https://github.com/Azure-Samples/service-fabric-java-getting-started.
>
>

## <a name="communicating-with-a-service"></a>Comunicazione con un servizio
Hello affidabile API dei servizi fornisce hello client toowrite di librerie che comunicano con i servizi seguenti.

### <a name="service-endpoint-resolution"></a>Risoluzione degli endpoint di servizio
Hello primo passaggio toocommunication con un servizio è un indirizzo dell'endpoint della partizione hello o dell'istanza del servizio hello da tootalk a tooresolve. Hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` classe di utilità è una primitiva di base che consente ai client di determinare endpoint hello di un servizio in fase di esecuzione. Nella terminologia di Service Fabric, hello processo di individuazione endpoint hello di un servizio è hello di cui viene fatto riferimento tooas *la risoluzione degli endpoint del servizio*.

tooservices tooconnect all'interno di un cluster, ServicePartitionResolver è possibile creare usando le impostazioni predefinite. È consigliata l'utilizzo della maggior parte dei casi hello:

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

tooservices tooconnect in un cluster diverso, è possibile creare un ServicePartitionResolver con un set di endpoint di gateway di cluster. Si noti che gli endpoint gateway sono endpoint diversi solo per la connessione toohello dello stesso cluster. ad esempio:

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

In alternativa, `ServicePartitionResolver` è possibile assegnare una funzione per la creazione di un `FabricClient` toouse internamente:

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

`FabricClient`è l'oggetto hello toocommunicate utilizzati con i cluster di Service Fabric hello per varie operazioni di gestione in cluster hello. È utile quando si vuole avere un maggiore controllo sul modo in cui un risolutore di partizioni del servizio interagisce con il cluster. `FabricClient`esegue la memorizzazione nella cache internamente e viene in genere dispendiosi toocreate, pertanto è importante tooreuse `FabricClient` istanze quanto possibile.

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

È un metodo di risoluzione usato tooretrieve hello un indirizzo di un servizio o una partizione del servizio per i servizi partizionati.

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

Indirizzo di un servizio può essere risolto facilmente utilizzando un ServicePartitionResolver, ma è necessario più lavoro hello tooensure risolta l'indirizzo può essere utilizzato correttamente. Il client deve toodetect se il tentativo di connessione hello non riuscita a causa di un errore temporaneo e può essere recuperato (ad esempio, servizio spostato o è temporaneamente non disponibile), o un errore permanente (ad esempio, servizio è stato eliminato o hello risorsa richiesta non esiste più). Le istanze del servizio o repliche possono spostarsi dal nodo toonode in qualsiasi momento per diversi motivi. indirizzo del servizio Hello risolto attraverso ServicePartitionResolver può essere aggiornato per il codice client tenta tooconnect tempo di hello. In tal caso nuovamente hello client deve disporre indirizzo hello toore risoluzione. Fornendo hello precedente `ResolvedServicePartition` indica che hello nuovo resolver esigenze tootry anziché semplicemente recuperare un indirizzo memorizzato nella cache.

In genere, il codice client hello necessario non utilizzare hello ServicePartitionResolver direttamente. E viene creato e passato nella factory client toocommunication in hello affidabile API dei servizi. factory Hello utilizzano resolver hello internamente toogenerate un oggetto client che può essere utilizzati toocommunicate con i servizi.

### <a name="communication-clients-and-factories"></a>Client e factory di comunicazione
libreria di factory di comunicazione Hello implementa un modello tipico di ripetere la gestione di errori che semplifica l'endpoint del servizio tooresolved connessioni nuovo tentativo. raccolta di factory Hello fornisce il meccanismo di tentativi di hello mentre si forniscono i gestori degli errori di hello.

`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`definisce l'interfaccia di base hello implementata da una factory di comunicazione client che produce i client che possono comunicare con il servizio di Service Fabric tooa. Hello implementazione di hello che communicationclientfactory dipende da stack di comunicazione hello utilizzato dal servizio di Service Fabric hello in cui di desidera toocommunicate client hello. Hello affidabile API dei servizi fornisce un `CommunicationClientFactoryBase<TCommunicationClient>`. Fornisce un'implementazione di base dell'interfaccia CommunicationClientFactory hello ed esegue attività, stack di comunicazione hello tooall comuni. (Queste attività includono l'utilizzo di un endpoint del servizio hello toodetermine ServicePartitionResolver). In genere, i client implementano hello astratta CommunicationClientFactoryBase classe toohandle la logica di stack di comunicazione toohello specifico.

client communication Hello appena riceve un indirizzo e lo usa tooconnect tooa servizio. client di Hello può utilizzare qualsiasi protocollo che desidera.

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

factory Hello del client è responsabile della creazione di comunicazione client. Per i client che non mantengono una connessione permanente, ad esempio un client HTTP, factory hello deve solo toocreate e client hello restituito. Altri protocolli che mantengono una connessione permanente, ad esempio alcuni protocolli binari devono essere convalidati da hello factory toodetermine anche se la connessione hello deve toobe creato nuovamente.  

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

Infine, un gestore di eccezioni è responsabile di determinare quali tootake azione quando si verifica un'eccezione. Le eccezioni vengono suddivise nelle categorie **con possibilità di ritentare** e **senza possibilità di ritentare**.

* **Non riproducibile** eccezioni semplicemente ottengano generata di nuovo indietro toohello chiamante.
* Le eccezioni **con possibilità di ritentare** si suddividono a propria volta in due categorie: **temporanee** e **non temporanee**.
  * **Temporaneo** eccezioni sono quelli che è possibile ritentare semplicemente senza risolvere nuovamente l'indirizzo dell'endpoint servizio hello. Ovvero problemi di rete temporanei o le risposte di errore di servizio diversi da quelli che indicano l'indirizzo dell'endpoint servizio hello non esiste.
  * **Non temporaneo** eccezioni sono quelli che richiedono l'indirizzo dell'endpoint di hello servizio toobe nuovamente risolto. Sono incluse le eccezioni che indicano l'endpoint del servizio hello non è raggiungibile, che indica servizio hello è stato spostato tooa altro nodo.

Hello `TryHandleException` rende una decisione in una determinata eccezione. Se si **non conosce** toomake quali le decisioni relative a un'eccezione, dovrebbe restituire **false**. Se si **conoscere** toomake quali delle decisioni, deve impostare di conseguenza il risultato di hello e restituire **true**.

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
### <a name="putting-it-all-together"></a>Riassumendo
Con un `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, e `IExceptionHandler(C#) / ExceptionHandler(Java)` compilata in base a un protocollo di comunicazione, un `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` ne esegue il wrapping tutti insieme e fornisce la gestione di errori hello e ciclo di risoluzione indirizzi partizione del servizio per questi componenti.

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

## <a name="next-steps"></a>Passaggi successivi
* Vedere un esempio di comunicazione HTTP tra servizi in un [progetto di esempio C# in GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) o un [progetto di esempio Java in GitHub](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).
* [Chiamate di procedura remota con i Reliable Services remoti](service-fabric-reliable-services-communication-remoting.md)
* [Web API che usa OWIN in Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Comunicazione di WCF tramite Reliable Services](service-fabric-reliable-services-communication-wcf.md)
