---
title: note attori aaaReliable attore digitare serializzazione | Documenti Microsoft
description: Illustra i requisiti di base per la definizione di interfacce e classi serializzabili che possono essere utilizzati toodefine stati Service Fabric Reliable Actors
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
ms.openlocfilehash: d8584e7d90fe1c68af38983e71e5d0a7554689bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="notes-on-service-fabric-reliable-actors-type-serialization"></a><span data-ttu-id="83f8d-103">Note sulla serializzazione dei tipi di Service Fabric Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="83f8d-103">Notes on Service Fabric Reliable Actors type serialization</span></span>
<span data-ttu-id="83f8d-104">Hello gli argomenti di tutti i metodi, tipi di risultati delle attività hello restituiti da ogni metodo in un'interfaccia attore, che devono essere oggetti archiviati nel gestore degli Stati dell'attore [di contratto dati serializzabile](https://msdn.microsoft.com/library/ms731923.aspx).</span><span class="sxs-lookup"><span data-stu-id="83f8d-104">hello arguments of all methods, result types of hello tasks returned by each method in an actor interface, and objects stored in an actor's state manager must be [data contract serializable](https://msdn.microsoft.com/library/ms731923.aspx).</span></span> <span data-ttu-id="83f8d-105">Questo vale anche toohello argomenti dei metodi di hello definiti nella [interfacce eventi attore](service-fabric-reliable-actors-events.md).</span><span class="sxs-lookup"><span data-stu-id="83f8d-105">This also applies toohello arguments of hello methods defined in [actor event interfaces](service-fabric-reliable-actors-events.md).</span></span> <span data-ttu-id="83f8d-106">I metodi di interfaccia degli eventi dell'attore restituiscono sempre un valore void.</span><span class="sxs-lookup"><span data-stu-id="83f8d-106">(Actor event interface methods always return void.)</span></span>

## <a name="custom-data-types"></a><span data-ttu-id="83f8d-107">Tipi di dati personalizzati</span><span class="sxs-lookup"><span data-stu-id="83f8d-107">Custom data types</span></span>
<span data-ttu-id="83f8d-108">In questo esempio hello interfaccia attore seguente definisce un metodo che restituisce un tipo di dati personalizzato denominato `VoicemailBox`:</span><span class="sxs-lookup"><span data-stu-id="83f8d-108">In this example, hello following actor interface defines a method that returns a custom data type called `VoicemailBox`:</span></span>

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

<span data-ttu-id="83f8d-109">Hello viene implementata mediante un attore che utilizza hello stato manager toostore un `VoicemailBox` oggetto:</span><span class="sxs-lookup"><span data-stu-id="83f8d-109">hello interface is implemented by an actor that uses hello state manager toostore a `VoicemailBox` object:</span></span>

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

<span data-ttu-id="83f8d-110">In questo esempio hello `VoicemailBox` viene serializzato l'oggetto quando:</span><span class="sxs-lookup"><span data-stu-id="83f8d-110">In this example, hello `VoicemailBox` object is serialized when:</span></span>

* <span data-ttu-id="83f8d-111">oggetto Hello verrà trasmessi tra un'istanza di attore e un chiamante.</span><span class="sxs-lookup"><span data-stu-id="83f8d-111">hello object is transmitted between an actor instance and a caller.</span></span>
* <span data-ttu-id="83f8d-112">oggetto Hello viene salvato nel gestore degli stati hello in cui è toodisk persistente e replicati tooother nodi.</span><span class="sxs-lookup"><span data-stu-id="83f8d-112">hello object is saved in hello state manager where it is persisted toodisk and replicated tooother nodes.</span></span>

<span data-ttu-id="83f8d-113">framework Reliable Actor Hello Usa la serializzazione di DataContract.</span><span class="sxs-lookup"><span data-stu-id="83f8d-113">hello Reliable Actor framework uses DataContract serialization.</span></span> <span data-ttu-id="83f8d-114">Pertanto, hello oggetti dati personalizzati e i relativi membri devono essere annotati con hello **DataContract** e **DataMember** rispettivamente gli attributi.</span><span class="sxs-lookup"><span data-stu-id="83f8d-114">Therefore, hello custom data objects and their members must be annotated with hello **DataContract** and **DataMember** attributes, respectively.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="83f8d-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="83f8d-115">Next steps</span></span>
* [<span data-ttu-id="83f8d-116">Ciclo di vita degli attori e Garbage Collection</span><span class="sxs-lookup"><span data-stu-id="83f8d-116">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="83f8d-117">Timer e promemoria degli attori</span><span class="sxs-lookup"><span data-stu-id="83f8d-117">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="83f8d-118">Eventi relativi agli attori</span><span class="sxs-lookup"><span data-stu-id="83f8d-118">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="83f8d-119">Rientranza di Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="83f8d-119">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="83f8d-120">Polimorfismo dell'attore e modelli di progettazione orientati a oggetti</span><span class="sxs-lookup"><span data-stu-id="83f8d-120">Actor polymorphism and object-oriented design patterns</span></span>](service-fabric-reliable-actors-polymorphism.md)
* [<span data-ttu-id="83f8d-121">Diagnostica e monitoraggio delle prestazioni per Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="83f8d-121">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
