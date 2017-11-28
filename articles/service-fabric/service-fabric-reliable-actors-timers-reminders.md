---
title: aaaReliable attori timer e promemoria | Documenti Microsoft
description: Introduzione tootimers e promemoria per attori affidabile di servizio dell'infrastruttura.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 00c48716-569e-4a64-bd6c-25234c85ff4f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c5116ec1923014e131130b9f4e86dd1e133bbf7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="2d22c-103">Timer e promemoria degli attori</span><span class="sxs-lookup"><span data-stu-id="2d22c-103">Actor timers and reminders</span></span>
<span data-ttu-id="2d22c-104">Gli attori possono pianificare il relativo lavoro periodico registrando timer o promemoria.</span><span class="sxs-lookup"><span data-stu-id="2d22c-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="2d22c-105">Questo articolo viene illustrato come toouse timer e i promemoria e vengono illustrate le differenze di hello tra di essi.</span><span class="sxs-lookup"><span data-stu-id="2d22c-105">This article shows how toouse timers and reminders and explains hello differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="2d22c-106">Timer degli attori</span><span class="sxs-lookup"><span data-stu-id="2d22c-106">Actor timers</span></span>
<span data-ttu-id="2d22c-107">Timer attore forniscono un semplice wrapper tooensure un timer .NET o Java che i metodi di callback hello rispettino hello basato su concorrenza garantisce hello attori runtime fornisce.</span><span class="sxs-lookup"><span data-stu-id="2d22c-107">Actor timers provide a simple wrapper around a .NET or Java timer tooensure that hello callback methods respect hello turn-based concurrency guarantees that hello Actors runtime provides.</span></span>

<span data-ttu-id="2d22c-108">Gli attori possono utilizzare hello `RegisterTimer`(c#) o `registerTimer`(linguaggio) e `UnregisterTimer`(c#) o `unregisterTimer`metodi (linguaggio) la base della classe tooregister e annullare la registrazione i timer.</span><span class="sxs-lookup"><span data-stu-id="2d22c-108">Actors can use hello `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class tooregister and unregister their timers.</span></span> <span data-ttu-id="2d22c-109">esempio Hello seguente di seguito viene illustrato l'utilizzo di hello del timer delle API.</span><span class="sxs-lookup"><span data-stu-id="2d22c-109">hello example below shows hello use of timer APIs.</span></span> <span data-ttu-id="2d22c-110">Hello API sono molto simili timer .NET di toohello o timer Java.</span><span class="sxs-lookup"><span data-stu-id="2d22c-110">hello APIs are very similar toohello .NET timer or Java timer.</span></span> <span data-ttu-id="2d22c-111">In questo esempio, alla scadenza, timer hello hello attori runtime chiamerà hello `MoveObject`(c#) o `moveObject`(metodo) (linguaggio).</span><span class="sxs-lookup"><span data-stu-id="2d22c-111">In this example, when hello timer is due, hello Actors runtime will call hello `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="2d22c-112">metodo Hello è garantita la concorrenza toorespect hello basato su.</span><span class="sxs-lookup"><span data-stu-id="2d22c-112">hello method is guaranteed toorespect hello turn-based concurrency.</span></span> <span data-ttu-id="2d22c-113">Ciò significa che nessun altro metodo di attori o callback di timer/promemoria sarà in azione fino al completamento dell'esecuzione del callback.</span><span class="sxs-lookup"><span data-stu-id="2d22c-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

```csharp
class VisualObjectActor : Actor, IVisualObject
{
    private IActorTimer _updateTimer;

    public VisualObjectActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    protected override Task OnActivateAsync()
    {
        ...

        _updateTimer = RegisterTimer(
            MoveObject,                     // Callback method
            null,                           // Parameter toopass toohello callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time toodelay before hello callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of hello callback method

        return base.OnActivateAsync();
    }

    protected override Task OnDeactivateAsync()
    {
        if (_updateTimer != null)
        {
            UnregisterTimer(_updateTimer);
        }

        return base.OnDeactivateAsync();
    }

    private Task MoveObject(object state)
    {
        ...
        return Task.FromResult(true);
    }
}
```
```Java
public class VisualObjectActorImpl extends FabricActor implements VisualObjectActor
{
    private ActorTimer updateTimer;

    public VisualObjectActorImpl(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    @Override
    protected CompletableFuture onActivateAsync()
    {
        ...

        return this.stateManager()
                .getOrAddStateAsync(
                        stateName,
                        VisualObject.createRandom(
                                this.getId().toString(),
                                new Random(this.getId().toString().hashCode())))
                .thenApply((r) -> {
                    this.registerTimer(
                            (o) -> this.moveObject(o),                        // Callback method
                            "moveObject",
                            null,                                             // Parameter toopass toohello callback method
                            Duration.ofMillis(10),                            // Amount of time toodelay before hello callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of hello callback method
                    return null;
                });
    }

    @Override
    protected CompletableFuture onDeactivateAsync()
    {
        if (updateTimer != null)
        {
            unregisterTimer(updateTimer);
        }

        return super.onDeactivateAsync();
    }

    private CompletableFuture moveObject(Object state)
    {
        ...
        return this.stateManager().getStateAsync(this.stateName).thenCompose(v -> {
            VisualObject v1 = (VisualObject)v;
            v1.move();
            return (CompletableFuture<?>)this.stateManager().setStateAsync(stateName, v1).
                    thenApply(r -> {
                      ...
                      return null;});
        });
    }
}
```

<span data-ttu-id="2d22c-114">Hello successivo periodo di timer hello viene avviata dopo il callback di hello completa l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2d22c-114">hello next period of hello timer starts after hello callback completes execution.</span></span> <span data-ttu-id="2d22c-115">Ciò implica che timer hello viene arrestato mentre è in esecuzione e viene avviata al termine di callback hello di callback hello.</span><span class="sxs-lookup"><span data-stu-id="2d22c-115">This implies that hello timer is stopped while hello callback is executing and is started when hello callback finishes.</span></span>

<span data-ttu-id="2d22c-116">runtime di attori Hello Salva le modifiche apportate gestore degli Stati dell'attore toohello al termine di callback hello.</span><span class="sxs-lookup"><span data-stu-id="2d22c-116">hello Actors runtime saves changes made toohello actor's State Manager when hello callback finishes.</span></span> <span data-ttu-id="2d22c-117">Se si verifica un errore durante il salvataggio dello stato di hello, tale oggetto attore verrà disattivato e verrà attivata una nuova istanza.</span><span class="sxs-lookup"><span data-stu-id="2d22c-117">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="2d22c-118">Quando viene disattivata attore hello come parte di garbage collection, vengono arrestati tutti i timer.</span><span class="sxs-lookup"><span data-stu-id="2d22c-118">All timers are stopped when hello actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="2d22c-119">In seguito, non viene richiamato nessun callback di timer.</span><span class="sxs-lookup"><span data-stu-id="2d22c-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="2d22c-120">Inoltre, il runtime di attori hello mantengono le informazioni sui timer hello che erano in esecuzione prima della disattivazione.</span><span class="sxs-lookup"><span data-stu-id="2d22c-120">Also, hello Actors runtime does not retain any information about hello timers that were running before deactivation.</span></span> <span data-ttu-id="2d22c-121">È attivo toohello attore tooregister qualsiasi timer necessari quando viene riattivato in hello future.</span><span class="sxs-lookup"><span data-stu-id="2d22c-121">It is up toohello actor tooregister any timers that it needs when it is reactivated in hello future.</span></span> <span data-ttu-id="2d22c-122">Per ulteriori informazioni, vedere la sezione hello in [di garbage collection attore](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="2d22c-122">For more information, see hello section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="2d22c-123">Promemoria degli attori</span><span class="sxs-lookup"><span data-stu-id="2d22c-123">Actor reminders</span></span>
<span data-ttu-id="2d22c-124">Promemoria sono un meccanismo tootrigger callback persistente in un attore in momenti specifici.</span><span class="sxs-lookup"><span data-stu-id="2d22c-124">Reminders are a mechanism tootrigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="2d22c-125">La funzionalità è tootimers simile.</span><span class="sxs-lookup"><span data-stu-id="2d22c-125">Their functionality is similar tootimers.</span></span> <span data-ttu-id="2d22c-126">Tuttavia, a differenza di timer, promemoria vengono attivati in tutte le circostanze fino a quando non in modo esplicito Annulla attore hello o attore hello viene eliminato in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="2d22c-126">But unlike timers, reminders are triggered under all circumstances until hello actor explicitly unregisters them or hello actor is explicitly deleted.</span></span> <span data-ttu-id="2d22c-127">In particolare, promemoria vengono attivati attraverso i failover e disattivazioni attore perché hello attori runtime mantiene le informazioni sui promemoria hello actor.</span><span class="sxs-lookup"><span data-stu-id="2d22c-127">Specifically, reminders are triggered across actor deactivations and failovers because hello Actors runtime persists information about hello actor's reminders.</span></span>

<span data-ttu-id="2d22c-128">tooregister un promemoria, un attore chiama hello `RegisterReminderAsync` metodo fornito nella classe base hello, come illustrato nell'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="2d22c-128">tooregister a reminder, an actor calls hello `RegisterReminderAsync` method provided on hello base class, as shown in hello following example:</span></span>

```csharp
protected override async Task OnActivateAsync()
{
    string reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    IActorReminder reminderRegistration = await this.RegisterReminderAsync(
        reminderName,
        BitConverter.GetBytes(amountInDollars),
        TimeSpan.FromDays(3),
        TimeSpan.FromDays(1));
}
```

```Java
@Override
protected CompletableFuture onActivateAsync()
{
    String reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    ActorReminder reminderRegistration = this.registerReminderAsync(
            reminderName,
            state,
            dueTime,    //hello amount of time toodelay before firing hello reminder
            period);    //hello time interval between firing of reminders
}
```

<span data-ttu-id="2d22c-129">In questo esempio, `"Pay cell phone bill"` è il nome di promemoria hello.</span><span class="sxs-lookup"><span data-stu-id="2d22c-129">In this example, `"Pay cell phone bill"` is hello reminder name.</span></span> <span data-ttu-id="2d22c-130">Questa è una stringa che utilizza attore hello toouniquely identificare un promemoria.</span><span class="sxs-lookup"><span data-stu-id="2d22c-130">This is a string that hello actor uses toouniquely identify a reminder.</span></span> <span data-ttu-id="2d22c-131">`BitConverter.GetBytes(amountInDollars)`(C#) è il contesto hello associato promemoria hello.</span><span class="sxs-lookup"><span data-stu-id="2d22c-131">`BitConverter.GetBytes(amountInDollars)`(C#) is hello context that is associated with hello reminder.</span></span> <span data-ttu-id="2d22c-132">Verrà passato toohello indietro attore come un callback di promemoria toohello argomento, vale a dire `IRemindable.ReceiveReminderAsync`(c#) o `Remindable.receiveReminderAsync`(linguaggio).</span><span class="sxs-lookup"><span data-stu-id="2d22c-132">It will be passed back toohello actor as an argument toohello reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="2d22c-133">Gli attori che utilizzano promemoria devono implementare hello `IRemindable` interfaccia, come illustrato nell'esempio hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2d22c-133">Actors that use reminders must implement hello `IRemindable` interface, as shown in hello example below.</span></span>

```csharp
public class ToDoListActor : Actor, IToDoListActor, IRemindable
{
    public ToDoListActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task ReceiveReminderAsync(string reminderName, byte[] context, TimeSpan dueTime, TimeSpan period)
    {
        if (reminderName.Equals("Pay cell phone bill"))
        {
            int amountToPay = BitConverter.ToInt32(context, 0);
            System.Console.WriteLine("Please pay your cell phone bill of ${0}!", amountToPay);
        }
        return Task.FromResult(true);
    }
}
```
```Java
public class ToDoListActorImpl extends FabricActor implements ToDoListActor, Remindable
{
    public ToDoListActor(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture receiveReminderAsync(String reminderName, byte[] context, Duration dueTime, Duration period)
    {
        if (reminderName.equals("Pay cell phone bill"))
        {
            int amountToPay = ByteBuffer.wrap(context).getInt();
            System.out.println("Please pay your cell phone bill of " + amountToPay);
        }
        return CompletableFuture.completedFuture(true);
    }

```

<span data-ttu-id="2d22c-134">Quando viene attivato un promemoria, hello Reliable Actors runtime richiamerà hello `ReceiveReminderAsync`(c#) o `receiveReminderAsync`metodo hello attore (linguaggio).</span><span class="sxs-lookup"><span data-stu-id="2d22c-134">When a reminder is triggered, hello Reliable Actors runtime will invoke hello  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on hello Actor.</span></span> <span data-ttu-id="2d22c-135">Un attore può registrare più promemoria e hello `ReceiveReminderAsync`(c#) o `receiveReminderAsync`(linguaggio) metodo viene richiamato uno qualsiasi di tali promemoria quando viene attivato.</span><span class="sxs-lookup"><span data-stu-id="2d22c-135">An actor can register multiple reminders, and hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="2d22c-136">attore Hello può utilizzare hello promemoria nome è passato in toohello `ReceiveReminderAsync`(c#) o `receiveReminderAsync`(linguaggio) metodo toofigure out che è stata attivata promemoria.</span><span class="sxs-lookup"><span data-stu-id="2d22c-136">hello actor can use hello reminder name that is passed in toohello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method toofigure out which reminder was triggered.</span></span>

<span data-ttu-id="2d22c-137">runtime attori Hello Salva lo stato dell'actor hello quando hello `ReceiveReminderAsync`(c#) o `receiveReminderAsync`al completamento della chiamata (linguaggio).</span><span class="sxs-lookup"><span data-stu-id="2d22c-137">hello Actors runtime saves hello actor's state when hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="2d22c-138">Se si verifica un errore durante il salvataggio dello stato di hello, tale oggetto attore verrà disattivato e verrà attivata una nuova istanza.</span><span class="sxs-lookup"><span data-stu-id="2d22c-138">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="2d22c-139">toounregister un promemoria, un attore chiama hello `UnregisterReminderAsync`(c#) o `unregisterReminderAsync`metodo (linguaggio), come illustrato nell'esempio hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2d22c-139">toounregister a reminder, an actor calls hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in hello examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="2d22c-140">Come illustrato in precedenza, hello `UnregisterReminderAsync`(c#) o `unregisterReminderAsync`(linguaggio) metodo accetta un `IActorReminder`(c#) o `ActorReminder`interfaccia (linguaggio).</span><span class="sxs-lookup"><span data-stu-id="2d22c-140">As shown above, hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="2d22c-141">Hello attore classe di base supporta un `GetReminder`(c#) o `getReminder`metodo (linguaggio) che può essere utilizzati tooretrieve hello `IActorReminder`(c#) o `ActorReminder`interfaccia (linguaggio) passando il nome di promemoria hello.</span><span class="sxs-lookup"><span data-stu-id="2d22c-141">hello actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used tooretrieve hello `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in hello reminder name.</span></span> <span data-ttu-id="2d22c-142">Questa operazione è utile perché non è necessario toopersist hello attore hello `IActorReminder`(c#) o `ActorReminder`interfaccia (linguaggio) che è stato restituito da hello `RegisterReminder`(c#) o `registerReminder`chiamata al metodo (linguaggio).</span><span class="sxs-lookup"><span data-stu-id="2d22c-142">This is convenient because hello actor does not need toopersist hello `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from hello `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d22c-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d22c-143">Next Steps</span></span>
<span data-ttu-id="2d22c-144">Acquisire informazioni sugli eventi e sulla rientranza di Reliable Actor:</span><span class="sxs-lookup"><span data-stu-id="2d22c-144">Learn about Reliable Actor events and reentrancy:</span></span>
* [<span data-ttu-id="2d22c-145">Eventi relativi agli attori</span><span class="sxs-lookup"><span data-stu-id="2d22c-145">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="2d22c-146">Rientranza di Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="2d22c-146">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
