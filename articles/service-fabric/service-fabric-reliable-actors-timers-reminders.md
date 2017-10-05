---
title: Timer e promemoria di Reliable Actors | Microsoft Docs
description: Introduzione a timer e promemoria per Reliable Actors di Service Fabric
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
ms.openlocfilehash: 06b026ce06e0f16a77ac238de0af2263f272933c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="3bfcd-103">Timer e promemoria degli attori</span><span class="sxs-lookup"><span data-stu-id="3bfcd-103">Actor timers and reminders</span></span>
<span data-ttu-id="3bfcd-104">Gli attori possono pianificare il relativo lavoro periodico registrando timer o promemoria.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="3bfcd-105">Questo articolo illustra come usare timer e promemoria e ne spiega le differenze.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-105">This article shows how to use timers and reminders and explains the differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="3bfcd-106">Timer degli attori</span><span class="sxs-lookup"><span data-stu-id="3bfcd-106">Actor timers</span></span>
<span data-ttu-id="3bfcd-107">I timer degli attori forniscono un wrapper semplice intorno al timer .NET o Java per garantire che i metodi di callback rispettino le garanzie di concorrenza basata su turni offerte dal runtime di Actors.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-107">Actor timers provide a simple wrapper around a .NET or Java timer to ensure that the callback methods respect the turn-based concurrency guarantees that the Actors runtime provides.</span></span>

<span data-ttu-id="3bfcd-108">Per eseguire e annullare la registrazione dei timer, gli attori possono usare i metodi `RegisterTimer`(C#) o `registerTimer`(Java) e `UnregisterTimer`(C#) o `unregisterTimer`(Java) nella propria classe base.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-108">Actors can use the `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class to register and unregister their timers.</span></span> <span data-ttu-id="3bfcd-109">L'esempio seguente illustra l'uso delle API di timer,</span><span class="sxs-lookup"><span data-stu-id="3bfcd-109">The example below shows the use of timer APIs.</span></span> <span data-ttu-id="3bfcd-110">che sono molto simili al timer .NET o al timer Java.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-110">The APIs are very similar to the .NET timer or Java timer.</span></span> <span data-ttu-id="3bfcd-111">In questo esempio, quando il timer è in scadenza, il runtime di Actors chiama il metodo `MoveObject`(C#) o `moveObject`(Java).</span><span class="sxs-lookup"><span data-stu-id="3bfcd-111">In this example, when the timer is due, the Actors runtime will call the `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="3bfcd-112">Si garantisce che il metodo rispetti la concorrenza basata su turni.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-112">The method is guaranteed to respect the turn-based concurrency.</span></span> <span data-ttu-id="3bfcd-113">Ciò significa che nessun altro metodo di attori o callback di timer/promemoria sarà in azione fino al completamento dell'esecuzione del callback.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

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
            null,                           // Parameter to pass to the callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time to delay before the callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of the callback method

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
                            null,                                             // Parameter to pass to the callback method
                            Duration.ofMillis(10),                            // Amount of time to delay before the callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of the callback method
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

<span data-ttu-id="3bfcd-114">Il periodo successivo del timer inizia dopo il completamento del callback.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-114">The next period of the timer starts after the callback completes execution.</span></span> <span data-ttu-id="3bfcd-115">Pertanto, il timer viene arrestato mentre il callback è in esecuzione e viene avviato quando il callback è completato.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-115">This implies that the timer is stopped while the callback is executing and is started when the callback finishes.</span></span>

<span data-ttu-id="3bfcd-116">Il runtime di Actors salva le modifiche apportate alla gestione stati dell'attore al termine del callback.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-116">The Actors runtime saves changes made to the actor's State Manager when the callback finishes.</span></span> <span data-ttu-id="3bfcd-117">Se si verifica un errore durante il salvataggio dello stato, viene disattivato l'oggetto attore e viene attivata una nuova istanza.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-117">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="3bfcd-118">Tutti i timer vengono arrestati quando l'attore viene disattivato come parte di garbage collection.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-118">All timers are stopped when the actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="3bfcd-119">In seguito, non viene richiamato nessun callback di timer.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="3bfcd-120">Inoltre, il runtime di Actors non mantiene alcuna informazione sui timer in esecuzione prima della disattivazione.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-120">Also, the Actors runtime does not retain any information about the timers that were running before deactivation.</span></span> <span data-ttu-id="3bfcd-121">È responsabilità dell'attore registrare gli eventuali timer che saranno necessari quando verrà riattivato in futuro.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-121">It is up to the actor to register any timers that it needs when it is reactivated in the future.</span></span> <span data-ttu-id="3bfcd-122">Per ulteriori informazioni, vedere la sezione sulla [garbage collection degli attori](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="3bfcd-122">For more information, see the section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="3bfcd-123">Promemoria degli attori</span><span class="sxs-lookup"><span data-stu-id="3bfcd-123">Actor reminders</span></span>
<span data-ttu-id="3bfcd-124">I promemoria sono un meccanismo per attivare i callback persistenti su un attore in base a orari specificati.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-124">Reminders are a mechanism to trigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="3bfcd-125">La loro funzionalità è simile a quella dei timer.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-125">Their functionality is similar to timers.</span></span> <span data-ttu-id="3bfcd-126">Tuttavia, a differenza dei timer, i promemoria vengono attivati in qualsiasi circostanza finché l'attore non ne annulla la registrazione in modo esplicito o finché l'attore non viene eliminato in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-126">But unlike timers, reminders are triggered under all circumstances until the actor explicitly unregisters them or the actor is explicitly deleted.</span></span> <span data-ttu-id="3bfcd-127">In particolare, i promemoria vengono attivati anche in caso di failover e disattivazione dell'attore perché il runtime di Actors rende persistenti le informazioni sui promemoria dell'attore.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-127">Specifically, reminders are triggered across actor deactivations and failovers because the Actors runtime persists information about the actor's reminders.</span></span>

<span data-ttu-id="3bfcd-128">Per registrare un promemoria, un attore chiama il metodo `RegisterReminderAsync` fornito nella classe base, come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-128">To register a reminder, an actor calls the `RegisterReminderAsync` method provided on the base class, as shown in the following example:</span></span>

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
            dueTime,    //The amount of time to delay before firing the reminder
            period);    //The time interval between firing of reminders
}
```

<span data-ttu-id="3bfcd-129">In questo esempio `"Pay cell phone bill"` è il nome del promemoria.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-129">In this example, `"Pay cell phone bill"` is the reminder name.</span></span> <span data-ttu-id="3bfcd-130">Questa è una stringa usata dall'attore per identificare in modo univoco un promemoria.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-130">This is a string that the actor uses to uniquely identify a reminder.</span></span> <span data-ttu-id="3bfcd-131">`BitConverter.GetBytes(amountInDollars)`(C#) è il contesto associato al promemoria.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-131">`BitConverter.GetBytes(amountInDollars)`(C#) is the context that is associated with the reminder.</span></span> <span data-ttu-id="3bfcd-132">Questo contesto verrà passato all'attore come argomento per il callback di promemoria, ad esempio `IRemindable.ReceiveReminderAsync`(C#) o `Remindable.receiveReminderAsync`(Java).</span><span class="sxs-lookup"><span data-stu-id="3bfcd-132">It will be passed back to the actor as an argument to the reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="3bfcd-133">Gli attori che usano i promemoria devono implementare l'interfaccia `IRemindable` , come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-133">Actors that use reminders must implement the `IRemindable` interface, as shown in the example below.</span></span>

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

<span data-ttu-id="3bfcd-134">Quando viene attivato un promemoria, il runtime di Reliable Actors richiama il metodo `ReceiveReminderAsync`(C#) o `receiveReminderAsync`(Java) sull'Actor.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-134">When a reminder is triggered, the Reliable Actors runtime will invoke the  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on the Actor.</span></span> <span data-ttu-id="3bfcd-135">Un attore può registrare più promemoria e il metodo `ReceiveReminderAsync`(C#) o `receiveReminderAsync`(Java) viene richiamato ogni volta che tali promemoria vengono attivati.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-135">An actor can register multiple reminders, and the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="3bfcd-136">L'attore può usare il nome del promemoria che viene passato al metodo `ReceiveReminderAsync`(C#) o `receiveReminderAsync`(Java) per identificare il promemoria attivato.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-136">The actor can use the reminder name that is passed in to the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method to figure out which reminder was triggered.</span></span>

<span data-ttu-id="3bfcd-137">Il runtime di Actors salva lo stato dell'attore al termine della chiamata a `ReceiveReminderAsync`(C#) o `receiveReminderAsync`(Java).</span><span class="sxs-lookup"><span data-stu-id="3bfcd-137">The Actors runtime saves the actor's state when the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="3bfcd-138">Se si verifica un errore durante il salvataggio dello stato, viene disattivato l'oggetto attore e viene attivata una nuova istanza.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-138">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="3bfcd-139">Per annullare la registrazione di un promemoria, un attore chiama il metodo `UnregisterReminderAsync`(C#) o `unregisterReminderAsync`(Java), come illustrato nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-139">To unregister a reminder, an actor calls the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in the examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="3bfcd-140">Come mostrato in precedenza, il metodo `UnregisterReminderAsync`(C#) o `unregisterReminderAsync`(Java) accetta un'interfaccia `IActorReminder`(C#) o `ActorReminder`(Java).</span><span class="sxs-lookup"><span data-stu-id="3bfcd-140">As shown above, the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="3bfcd-141">La classe base dell'attore supporta un metodo `GetReminder`(C#) o `getReminder`(Java) che può essere usato per recuperare l'interfaccia `IActorReminder`(C#) o `ActorReminder`(Java) passando il nome del promemoria.</span><span class="sxs-lookup"><span data-stu-id="3bfcd-141">The actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used to retrieve the `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in the reminder name.</span></span> <span data-ttu-id="3bfcd-142">Questo metodo è utile perché l'attore non deve rendere persistente l'interfaccia `IActorReminder`(C#) o `ActorReminder`(Java) restituita dalla chiamata al metodo `RegisterReminder`(C#) o `registerReminder`(Java).</span><span class="sxs-lookup"><span data-stu-id="3bfcd-142">This is convenient because the actor does not need to persist the `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from the `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bfcd-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3bfcd-143">Next Steps</span></span>
<span data-ttu-id="3bfcd-144">Acquisire informazioni sugli eventi e sulla rientranza di Reliable Actor:</span><span class="sxs-lookup"><span data-stu-id="3bfcd-144">Learn about Reliable Actor events and reentrancy:</span></span>
* [<span data-ttu-id="3bfcd-145">Eventi relativi agli attori</span><span class="sxs-lookup"><span data-stu-id="3bfcd-145">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="3bfcd-146">Rientranza di Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="3bfcd-146">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
