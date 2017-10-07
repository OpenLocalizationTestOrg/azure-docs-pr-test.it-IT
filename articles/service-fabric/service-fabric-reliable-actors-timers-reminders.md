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
# <a name="actor-timers-and-reminders"></a>Timer e promemoria degli attori
Gli attori possono pianificare il relativo lavoro periodico registrando timer o promemoria. Questo articolo viene illustrato come toouse timer e i promemoria e vengono illustrate le differenze di hello tra di essi.

## <a name="actor-timers"></a>Timer degli attori
Timer attore forniscono un semplice wrapper tooensure un timer .NET o Java che i metodi di callback hello rispettino hello basato su concorrenza garantisce hello attori runtime fornisce.

Gli attori possono utilizzare hello `RegisterTimer`(c#) o `registerTimer`(linguaggio) e `UnregisterTimer`(c#) o `unregisterTimer`metodi (linguaggio) la base della classe tooregister e annullare la registrazione i timer. esempio Hello seguente di seguito viene illustrato l'utilizzo di hello del timer delle API. Hello API sono molto simili timer .NET di toohello o timer Java. In questo esempio, alla scadenza, timer hello hello attori runtime chiamerà hello `MoveObject`(c#) o `moveObject`(metodo) (linguaggio). metodo Hello è garantita la concorrenza toorespect hello basato su. Ciò significa che nessun altro metodo di attori o callback di timer/promemoria sarà in azione fino al completamento dell'esecuzione del callback.

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

Hello successivo periodo di timer hello viene avviata dopo il callback di hello completa l'esecuzione. Ciò implica che timer hello viene arrestato mentre è in esecuzione e viene avviata al termine di callback hello di callback hello.

runtime di attori Hello Salva le modifiche apportate gestore degli Stati dell'attore toohello al termine di callback hello. Se si verifica un errore durante il salvataggio dello stato di hello, tale oggetto attore verrà disattivato e verrà attivata una nuova istanza.

Quando viene disattivata attore hello come parte di garbage collection, vengono arrestati tutti i timer. In seguito, non viene richiamato nessun callback di timer. Inoltre, il runtime di attori hello mantengono le informazioni sui timer hello che erano in esecuzione prima della disattivazione. È attivo toohello attore tooregister qualsiasi timer necessari quando viene riattivato in hello future. Per ulteriori informazioni, vedere la sezione hello in [di garbage collection attore](service-fabric-reliable-actors-lifecycle.md).

## <a name="actor-reminders"></a>Promemoria degli attori
Promemoria sono un meccanismo tootrigger callback persistente in un attore in momenti specifici. La funzionalità è tootimers simile. Tuttavia, a differenza di timer, promemoria vengono attivati in tutte le circostanze fino a quando non in modo esplicito Annulla attore hello o attore hello viene eliminato in modo esplicito. In particolare, promemoria vengono attivati attraverso i failover e disattivazioni attore perché hello attori runtime mantiene le informazioni sui promemoria hello actor.

tooregister un promemoria, un attore chiama hello `RegisterReminderAsync` metodo fornito nella classe base hello, come illustrato nell'esempio seguente hello:

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

In questo esempio, `"Pay cell phone bill"` è il nome di promemoria hello. Questa è una stringa che utilizza attore hello toouniquely identificare un promemoria. `BitConverter.GetBytes(amountInDollars)`(C#) è il contesto hello associato promemoria hello. Verrà passato toohello indietro attore come un callback di promemoria toohello argomento, vale a dire `IRemindable.ReceiveReminderAsync`(c#) o `Remindable.receiveReminderAsync`(linguaggio).

Gli attori che utilizzano promemoria devono implementare hello `IRemindable` interfaccia, come illustrato nell'esempio hello riportato di seguito.

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

Quando viene attivato un promemoria, hello Reliable Actors runtime richiamerà hello `ReceiveReminderAsync`(c#) o `receiveReminderAsync`metodo hello attore (linguaggio). Un attore può registrare più promemoria e hello `ReceiveReminderAsync`(c#) o `receiveReminderAsync`(linguaggio) metodo viene richiamato uno qualsiasi di tali promemoria quando viene attivato. attore Hello può utilizzare hello promemoria nome è passato in toohello `ReceiveReminderAsync`(c#) o `receiveReminderAsync`(linguaggio) metodo toofigure out che è stata attivata promemoria.

runtime attori Hello Salva lo stato dell'actor hello quando hello `ReceiveReminderAsync`(c#) o `receiveReminderAsync`al completamento della chiamata (linguaggio). Se si verifica un errore durante il salvataggio dello stato di hello, tale oggetto attore verrà disattivato e verrà attivata una nuova istanza.

toounregister un promemoria, un attore chiama hello `UnregisterReminderAsync`(c#) o `unregisterReminderAsync`metodo (linguaggio), come illustrato nell'esempio hello riportato di seguito.

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

Come illustrato in precedenza, hello `UnregisterReminderAsync`(c#) o `unregisterReminderAsync`(linguaggio) metodo accetta un `IActorReminder`(c#) o `ActorReminder`interfaccia (linguaggio). Hello attore classe di base supporta un `GetReminder`(c#) o `getReminder`metodo (linguaggio) che può essere utilizzati tooretrieve hello `IActorReminder`(c#) o `ActorReminder`interfaccia (linguaggio) passando il nome di promemoria hello. Questa operazione è utile perché non è necessario toopersist hello attore hello `IActorReminder`(c#) o `ActorReminder`interfaccia (linguaggio) che è stato restituito da hello `RegisterReminder`(c#) o `registerReminder`chiamata al metodo (linguaggio).

## <a name="next-steps"></a>Passaggi successivi
Acquisire informazioni sugli eventi e sulla rientranza di Reliable Actor:
* [Eventi relativi agli attori](service-fabric-reliable-actors-events.md)
* [Rientranza di Reliable Actors](service-fabric-reliable-actors-reentrancy.md)
