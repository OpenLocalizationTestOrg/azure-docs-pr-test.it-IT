---
title: aaaReliable attori in Service Fabric | Documenti Microsoft
description: "Viene descritto come Reliable Actors si basano su servizi affidabili e utilizzare le funzionalità di hello della piattaforma di Service Fabric hello."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 45839a7f-0536-46f1-ae2b-8ba3556407fb
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: ecffb54139f1171c7839b77fed0be60950881198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-reliable-actors-use-hello-service-fabric-platform"></a>Utilizzo di piattaforma Service Fabric hello Reliable Actors
In questo articolo descrive il modo Reliable Actors sulla piattaforma Azure Service Fabric hello. Reliable Actors eseguite in un framework che è ospitato in un'implementazione di un servizio affidabile con stato chiamato hello *servizio actor*. servizio actor Hello contiene tutti i ciclo di vita hello toomanage necessari componenti hello e un messaggio di invio per gli attori:

* Hello attore Runtime gestisce ciclo di vita, operazioni di garbage collection e applica l'accesso a thread singolo.
* Un listener di comunicazione remota del servizio actor accetta tooactors chiamate di accesso remoto e li invia a istanza di tooa dispatcher tooroute toohello attore appropriato.
* Provider dello stato Actor Hello esegue il wrapping di provider di stato (ad esempio, i provider di stato raccolte affidabile hello) e fornisce un adattatore per la gestione dello stato actor.

Questi framework Reliable Actor hello formano i componenti.

## <a name="service-layering"></a>Livelli del servizio
Poiché hello attore servizio è un servizio affidabile, tutti hello [modello di applicazione](service-fabric-application-model.md), ciclo di vita, [imballaggio](service-fabric-package-apps.md), [distribuzione](service-fabric-deploy-remove-applications.md), eseguire l'aggiornamento e scalabilità e concetti di Servizi affidabili applicano hello stessi servizi di tooactor modo. 

![Livelli del servizio attore][1]

Hello diagramma precedente mostra una relazione hello tra Framework di applicazioni di Service Fabric hello e codice utente. Elementi blu rappresentano framework dell'applicazione hello servizi affidabili, framework Reliable Actor hello arancione e verde rappresenta il codice utente.

In servizi affidabili, il servizio eredita hello `StatefulService` classe. Questa classe è a sua volta derivata da `StatefulServiceBase` (o `StatelessService` per i servizi senza stato). In Reliable Actors, si utilizza servizio actor hello. servizio actor Hello è un'implementazione diversa di hello `StatefulServiceBase` classe motivo implementa hello attore in cui è eseguito gli attori. Poiché servizio actor hello stesso è solo un'implementazione di `StatefulServiceBase`, è possibile scrivere il proprio servizio che deriva da `ActorService` e implementare le funzionalità di livello di servizio hello stesso modo analogo, quando si eredita `StatefulService`, ad esempio:

* Backup e ripristino del servizio.
* Funzionalità condivisa per tutti gli attori, ad esempio un interruttore.
* Nel servizio actor hello stesso e in ogni attore singole chiamate di procedura remota.

> [!NOTE]
> I servizi con stato non sono attualmente supportati in Java/Linux.

### <a name="using-hello-actor-service"></a>Utilizzo del servizio actor hello
Le istanze di attore hanno servizio actor toohello di accesso in cui sono in esecuzione. Tramite servizio actor hello, istanze attore possono ottenere a livello di codice il contesto di servizio hello. contesto del servizio Hello con ID di partizione hello, nome del servizio, nome dell'applicazione e altre informazioni specifiche della piattaforma Service Fabric:

```csharp
Task MyActorMethod()
{
    Guid partitionId = this.ActorService.Context.PartitionId;
    string serviceTypeName = this.ActorService.Context.ServiceTypeName;
    Uri serviceInstanceName = this.ActorService.Context.ServiceName;
    string applicationInstanceName = this.ActorService.Context.CodePackageActivationContext.ApplicationName;
}
```
```Java
CompletableFuture<?> MyActorMethod()
{
    UUID partitionId = this.getActorService().getServiceContext().getPartitionId();
    String serviceTypeName = this.getActorService().getServiceContext().getServiceTypeName();
    URI serviceInstanceName = this.getActorService().getServiceContext().getServiceName();
    String applicationInstanceName = this.getActorService().getServiceContext().getCodePackageActivationContext().getApplicationName();
}
```


Ad esempio tutti i servizi affidabili, servizio actor hello deve essere registrato con un tipo di servizio nel runtime di Service Fabric hello. Per hello del servizio actor toorun le istanze di attore, anche il tipo di attore deve essere registrato con il servizio actor hello. Hello `ActorRuntime` metodo di registrazione, questa operazione viene eseguita per attori. Nel caso più semplice di hello, è possibile registrare solo il tipo di attore e verrà utilizzato in modo implicito servizio actor hello con le impostazioni predefinite:

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>().GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```

In alternativa, è possibile utilizzare un'espressione lambda fornita da servizio di registrazione metodo tooconstruct hello actor hello manualmente. È possibile configurare il servizio di attore hello e costruire in modo esplicito le istanze attore, dove è possibile inserire attore tooyour dipendenze mediante il relativo costruttore:

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new ActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
static class Program
{
    private static void Main()
    {
      ActorRuntime.registerActorAsync(
              MyActor.class,
              (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
              timeout);

        Thread.sleep(Long.MAX_VALUE);
    }
}
```

### <a name="actor-service-methods"></a>Metodi del servizio attore
Hello implementa servizio Actor `IActorService` (c#) o `ActorService` (linguaggio), che a sua volta implementa `IService` (c#) o `Service` (linguaggio). Questo è l'interfaccia di hello utilizzata dalla comunicazione remota di servizi affidabili, che consente chiamate di procedure remote sui metodi di servizio. Contiene i metodi a livello di servizio che possono essere chiamati in remoto mediante la comunicazione remota del servizio.

#### <a name="enumerating-actors"></a>Enumerazione degli attori
servizio actor Hello consente al client metadati tooenumerate riguardanti gli attori hello che ospita il servizio di hello. Servizio actor hello, in quanto un servizio con stato partizionato, l'enumerazione viene eseguita per ogni partizione. In quanto ogni partizione può contenere molti attori, enumerazione hello viene restituito come un set di risultati di paging. pagine Hello vengono eseguite su fino a quando tutte le pagine vengono lette. Hello seguente esempio viene illustrato come un elenco di tutti gli attori attivi di una partizione di un servizio actor toocreate:

```csharp
IActorService actorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new List<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = await actorServiceProxy.GetActorsAsync(continuationToken, cancellationToken);

    activeActors.AddRange(page.Items.Where(x => x.IsActive));

    continuationToken = page.ContinuationToken;
}
while (continuationToken != null);
```

```Java
ActorService actorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), partitionKey);

ContinuationToken continuationToken = null;
List<ActorInformation> activeActors = new ArrayList<ActorInformation>();

do
{
    PagedResult<ActorInformation> page = actorServiceProxy.getActorsAsync(continuationToken);

    while(ActorInformation x: page.getItems())
    {
         if(x.isActive()){
              activeActors.add(x);
         }
    }

    continuationToken = page.getContinuationToken();
}
while (continuationToken != null);
```

#### <a name="deleting-actors"></a>Eliminazione di attori
servizio actor Hello offre anche una funzione per l'eliminazione di attori:

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new URI("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

Per ulteriori informazioni sull'eliminazione di attori e il relativo stato, vedere hello [documentazione del ciclo di vita attore](service-fabric-reliable-actors-lifecycle.md).

### <a name="custom-actor-service"></a>Servizio attore personalizzato
Utilizzando lambda di hello attore registrazione, è possibile registrare il proprio servizio actor personalizzata che deriva da `ActorService` (c#) e `FabricActorService` (linguaggio). In questo servizio attore personalizzato è possibile implementare funzionalità di livello di servizio scrivendo una classe di servizio che eredita `ActorService` (C#) o `FabricActorService` (Java). Un servizio actor personalizzata eredita tutte le funzionalità di runtime attore hello dalla `ActorService` (c#) o `FabricActorService` (linguaggio) e possono essere utilizzati tooimplement i propri metodi di servizio.

```csharp
class MyActorService : ActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }
}
```
```Java
class MyActorService extends FabricActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, BiFunction<FabricActorService, ActorId, ActorBase> newActor)
    {
         super(context, typeInfo, newActor);
    }
}
```

```csharp
static class Program
{
    private static void Main()
    {
        ActorRuntime.RegisterActorAsync<MyActor>(
            (context, actorType) => new MyActorService(context, actorType, () => new MyActor()))
            .GetAwaiter().GetResult();

        Thread.Sleep(Timeout.Infinite);
    }
}
```
```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
        Thread.sleep(Long.MAX_VALUE);
    }
}
```

#### <a name="implementing-actor-backup-and-restore"></a>Implementazione del backup e ripristino dell'attore
 Nell'esempio seguente di hello, servizio actor personalizzata hello espone tooback un metodo dei dati attore sfruttando del listener di comunicazione remota di hello già presenti nel `ActorService`:

```csharp
public interface IMyActorService : IService
{
    Task BackupActorsAsync();
}

class MyActorService : ActorService, IMyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<ActorBase> newActor)
        : base(context, typeInfo, newActor)
    { }

    public Task BackupActorsAsync()
    {
        return this.BackupAsync(new BackupDescription(PerformBackupAsync));
    }

    private async Task<bool> PerformBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           Directory.Delete(backupInfo.Directory, recursive: true);
        }
    }
}
```
```Java
public interface MyActorService extends Service
{
    CompletableFuture<?> backupActorsAsync();
}

class MyActorServiceImpl extends ActorService implements MyActorService
{
    public MyActorService(StatefulServiceContext context, ActorTypeInformation typeInfo, Func<FabricActorService, ActorId, ActorBase> newActor)
    {
       super(context, typeInfo, newActor);
    }

    public CompletableFuture backupActorsAsync()
    {
        return this.backupAsync(new BackupDescription((backupInfo, cancellationToken) -> performBackupAsync(backupInfo, cancellationToken)));
    }

    private CompletableFuture<Boolean> performBackupAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
    {
        try
        {
           // store hello contents of backupInfo.Directory
           return true;
        }
        finally
        {
           deleteDirectory(backupInfo.Directory)
        }
    }

    void deleteDirectory(File file) {
        File[] contents = file.listFiles();
        if (contents != null) {
            for (File f : contents) {
               deleteDirectory(f);
             }
        }
        file.delete();
    }
}
```


In questo esempio `IMyActorService` è un contratto di comunicazione remota che implementa `IService` (C#) and `Service` (Java) e viene successivamente implementato da `MyActorService`. Aggiungere questo contratto di servizi remoti, i metodi per `IMyActorService` sono ora disponibili tooa client mediante la creazione di un proxy remoto tramite `ActorServiceProxy`:

```csharp
IMyActorService myActorServiceProxy = ActorServiceProxy.Create<IMyActorService>(
    new Uri("fabric:/MyApp/MyService"), ActorId.CreateRandom());

await myActorServiceProxy.BackupActorsAsync();
```
```Java
MyActorService myActorServiceProxy = ActorServiceProxy.create(MyActorService.class,
    new URI("fabric:/MyApp/MyService"), actorId);

myActorServiceProxy.backupActorsAsync();
```

## <a name="application-model"></a>Modello di applicazione
Servizi Actor sono servizi affidabili, pertanto il modello di applicazione hello è hello stesso. Tuttavia, gli strumenti di compilazione hello attore framework generano alcuni dei file di modello di applicazione hello di.

### <a name="service-manifest"></a>Manifesto del servizio
strumenti di compilazione Hello attore framework generare automaticamente il contenuto di hello del file ServiceManifest.xml del servizio actor. Questo file include:

* Tipo del servizio attore. nome del tipo Hello viene generato in base al nome di progetto dell'attore. In base all'attributo di persistenza di hello nell'attore, hello HasPersistedState flag viene impostato anche di conseguenza.
* Pacchetto di codice.
* Pacchetto di configurazione.
* Risorse ed endpoint.

### <a name="application-manifest"></a>Manifesto dell'applicazione
strumenti di compilazione Hello attore framework creano automaticamente una definizione di servizio predefinito per il servizio actor. strumenti di compilazione Hello popolano le proprietà del servizio di hello predefinite:

* Numero di set di repliche è determinato dall'attributo persistenza hello l'attore. Ogni attributo persistenza hello ora l'attore viene modificato, numero di set di repliche hello nella definizione di servizio predefinito hello viene reimpostato di conseguenza.
* Intervallo e lo schema di partizione vengono impostati tooUniform Int64 con hello completo Int64 intervalli di chiavi.

## <a name="service-fabric-partition-concepts-for-actors"></a>Concetti relativi alla partizione di Service Fabric per gli attori
I servizi Actor sono servizi con stato partizionati. Ogni partizione di un servizio Actor contiene un set di attori. Le partizioni del servizio vengono distribuite automaticamente su più nodi in Service Fabric. Le istanze degli attori vengono distribuite di conseguenza.

![Partizionamento e distribuzione degli attori][5]

È possibile creare servizi Reliable Services con schemi di partizione e intervalli di chiavi di partizione diversi. servizio actor Hello Usa lo schema di partizionamento Int64 hello con toopartitions toomap di intervalli di chiavi di hello completo Int64 attori.

### <a name="actor-id"></a>ID attore
Ogni attore che viene creata nel servizio hello ha un ID univoco associato, rappresentato da hello `ActorId` classe. `ActorId`è un valore di ID opaco che può essere utilizzato per la distribuzione uniforme degli attori tra partizioni servizio hello tramite la generazione degli ID casuali:

```csharp
ActorProxy.Create<IMyActor>(ActorId.CreateRandom());
```
```Java
ActorProxyBase.create<MyActor>(MyActor.class, ActorId.newId());
```


Ogni `ActorId` è stato eseguito l'hashing tooan Int64. Ecco perché servizio actor hello è necessario utilizzare uno schema di partizionamento Int64 con hello completo Int64 intervalli di chiavi. È comunque possibile usare valori ID personalizzati per un `ActorID`, tra cui GUID/UUID, stringhe e Int64.

```csharp
ActorProxy.Create<IMyActor>(new ActorId(Guid.NewGuid()));
ActorProxy.Create<IMyActor>(new ActorId("myActorId"));
ActorProxy.Create<IMyActor>(new ActorId(1234));
```
```Java
ActorProxyBase.create(MyActor.class, new ActorId(UUID.randomUUID()));
ActorProxyBase.create(MyActor.class, new ActorId("myActorId"));
ActorProxyBase.create(MyActor.class, new ActorId(1234));
```

Quando si utilizza GUID/UUID e stringhe, i valori hello sono con hash tooan Int64. Tuttavia, quando si in modo esplicito forniscono un tooan Int64 `ActorId`, hello Int64 verrà eseguito il mapping direttamente tooa partizione senza ulteriore hash. È possibile utilizzare questa tecnica toocontrol cui attori hello partizione vengono inseriti in.

## <a name="next-steps"></a>Passaggi successivi
* [Gestione dello stato degli attori](service-fabric-reliable-actors-state-management.md)
* [Ciclo di vita degli attori e Garbage Collection](service-fabric-reliable-actors-lifecycle.md)
* [Documentazione di riferimento delle API di Actors](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Codice di esempio .NET](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Codice di esempio Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-platform/actor-service.png
[2]: ./media/service-fabric-reliable-actors-platform/app-deployment-scripts.png
[3]: ./media/service-fabric-reliable-actors-platform/actor-partition-info.png
[4]: ./media/service-fabric-reliable-actors-platform/actor-replica-role.png
[5]: ./media/service-fabric-reliable-actors-introduction/distribution.png
