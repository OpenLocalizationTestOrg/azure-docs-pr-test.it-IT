---
title: Note sulla serializzazione dei tipi di attori di Reliable Actors | Documentazione Microsoft
description: Illustra i requisiti di base per la definizione delle classi serializzabili che possono essere usate per definire le interfacce e lo stato di Service Fabric Reliable Actors.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 6e50e4dc-969a-4a1c-b36c-b292d964c7e3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 4b48b893e5a3bf5620f00a336576efe1ad63def8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="75e09-103">Note sulla serializzazione dei tipi di Service Fabric Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="75e09-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="75e09-104">Gli argomenti di tutti i metodi, i tipi di risultati delle attività restituiti da ogni metodo in un'interfaccia attore e gli oggetti archiviati nel gestore di stato di un attore devono essere [serializzabili in base al contratto dati](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="75e09-104">The arguments of all methods, result types of the tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="75e09-105">Questo vale anche per gli argomenti dei metodi definiti nelle [interfacce degli eventi dell'attore](service-fabric-reliable-actors-events.md).</span><span class="sxs-lookup"><span data-stu-id="75e09-105">This also applies to the arguments of the methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="75e09-106">I metodi di interfaccia degli eventi dell'attore restituiscono sempre un valore void.</span><span class="sxs-lookup"><span data-stu-id="75e09-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="75e09-107">Tipi di dati personalizzati</span><span class="sxs-lookup"><span data-stu-id="75e09-107">Custom data types</span></span>
<span data-ttu-id="75e09-108">In questo esempio l'interfaccia attore seguente definisce un metodo che restituisce un tipo di dati personalizzato denominato `VoicemailBox`:</span><span class="sxs-lookup"><span data-stu-id="75e09-108">In this example, the following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

```csharp
public interface IVoiceMailBoxActor : IActor
{
    Task<VoicemailBox> GetMailBoxAsync();
}
```

```Java
public interface VoiceMailBoxActor extends Actor
{
    CompletableFuture<VoicemailBox> getMailBoxAsync();
}
```

<span data-ttu-id="75e09-109">L'interfaccia è implementata da un attore, che usa il gestore di stato per archiviare un oggetto `VoicemailBox`:</span><span class="sxs-lookup"><span data-stu-id="75e09-109">The interface is implemented by an actor that uses the state manager to store a `VoicemailBox` object:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
public class VoiceMailBoxActor : Actor, IVoicemailBoxActor
{
    public VoiceMailBoxActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<VoicemailBox> GetMailboxAsync()
    {
        return this.StateManager.GetStateAsync<VoicemailBox>("Mailbox");
    }
}

```

```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class VoiceMailBoxActorImpl extends FabricActor implements VoicemailBoxActor
{
    public VoiceMailBoxActorImpl(ActorService actorService, ActorId actorId)
    {
         super(actorService, actorId);
    }

    public CompletableFuture<VoicemailBox> getMailBoxAsync()
    {
         return this.stateManager().getStateAsync("Mailbox");
    }
}

```

<span data-ttu-id="75e09-110">In questo esempio l'oggetto `VoicemailBox` viene serializzato quando:</span><span class="sxs-lookup"><span data-stu-id="75e09-110">In this example, the `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="75e09-111">L'oggetto viene trasmesso tra un'istanza di un attore e un chiamante.</span><span class="sxs-lookup"><span data-stu-id="75e09-111">The object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="75e09-112">L'oggetto viene salvato nel gestore di stato in cui viene reso persistente sul disco e replicato in altri nodi.</span><span class="sxs-lookup"><span data-stu-id="75e09-112">The object is saved in the state manager where it is persisted to disk and replicated to other nodes.</span></span>

<span data-ttu-id="75e09-113">Il framework Reliable Actors usa la serializzazione di DataContract.</span><span class="sxs-lookup"><span data-stu-id="75e09-113">The Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="75e09-114">Gli oggetti dati personalizzati e i relativi membri devono quindi essere annotati con gli attributi **DataContract** e **DataMember** rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="75e09-114">Therefore, the custom data objects and their members must be annotated with the **DataContract** and **DataMember** attributes, respectively.</span></span>

```csharp
[DataContract]
public class Voicemail
{
    [DataMember]
    public Guid Id { get; set; }

    [DataMember]
    public string Message { get; set; }

    [DataMember]
    public DateTime ReceivedAt { get; set; }
}
```
```Java
public class Voicemail implements Serializable
{
    private static final long serialVersionUID = 42L;

    private UUID id;                    //getUUID() and setUUID()

    private String message;             //getMessage() and setMessage()

    private GregorianCalendar receivedAt; //getReceivedAt() and setReceivedAt()
}
```


```csharp
[DataContract]
public class VoicemailBox
{
    public VoicemailBox()
    {
        this.MessageList = new List<Voicemail>();
    }

    [DataMember]
    public List<Voicemail> MessageList { get; set; }

    [DataMember]
    public string Greeting { get; set; }
}
```
```Java
public class VoicemailBox implements Serializable
{
    static final long serialVersionUID = 42L;
    
    public VoicemailBox()
    {
        this.messageList = new ArrayList<Voicemail>();
    }

    private List<Voicemail> messageList;   //getMessageList() and setMessageList()

    private String greeting;               //getGreeting() and setGreeting()
}
```


## <a name="next-steps"></a><span data-ttu-id="75e09-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="75e09-115">Next steps</span></span>
* [<span data-ttu-id="75e09-116">Ciclo di vita degli attori e Garbage Collection</span><span class="sxs-lookup"><span data-stu-id="75e09-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="75e09-117">Timer e promemoria degli attori</span><span class="sxs-lookup"><span data-stu-id="75e09-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="75e09-118">Eventi relativi agli attori</span><span class="sxs-lookup"><span data-stu-id="75e09-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="75e09-119">Rientranza di Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="75e09-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="75e09-120">Polimorfismo dell'attore e modelli di progettazione orientati a oggetti</span><span class="sxs-lookup"><span data-stu-id="75e09-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="75e09-121">Diagnostica e monitoraggio delle prestazioni per Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="75e09-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
