---
title: Panoramica del ciclo di vita dei microservizi Azure basati su attori | Documentazione Microsoft
description: Descrive il ciclo di vita di Service Fabric Reliable Actors, la Garbage Collection e l'eliminazione manuale di attori e del relativo stato
services: service-fabric
documentationcenter: .net
author: amanbha
manager: timlt
editor: vturecek
ms.assetid: b91384cc-804c-49d6-a6cb-f3f3d7d65a8e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: 75b7b77a0bef2051599a4f61183109cfb2ffff3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="f1451-103">Ciclo di vita degli attori, Garbage Collection automatica ed eliminazione manuale</span><span class="sxs-lookup"><span data-stu-id="f1451-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="f1451-104">Un attore viene attivato la prima volta che viene effettuata una chiamata a uno dei suoi metodi.</span><span class="sxs-lookup"><span data-stu-id="f1451-104">An actor is activated the first time a call is made to any of its methods.</span></span> <span data-ttu-id="f1451-105">Un attore viene disattivato (tramite Garbage Collection del runtime di Actors) se rimane inutilizzato per un periodo di tempo configurabile.</span><span class="sxs-lookup"><span data-stu-id="f1451-105">An actor is deactivated (garbage collected by the Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="f1451-106">Un attore e il relativo stato possono essere eliminati manualmente in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="f1451-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="f1451-107">Attivazione di un attore</span><span class="sxs-lookup"><span data-stu-id="f1451-107">Actor activation</span></span>
<span data-ttu-id="f1451-108">Quando un attore viene attivato, si verifica quanto segue:</span><span class="sxs-lookup"><span data-stu-id="f1451-108">When an actor is activated, the following occurs:</span></span>

* <span data-ttu-id="f1451-109">Quando viene effettuata una chiamata per un attore che non è ancora attivo, viene creato un nuovo attore.</span><span class="sxs-lookup"><span data-stu-id="f1451-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="f1451-110">Viene caricato lo stato dell'attore, se viene mantenuto.</span><span class="sxs-lookup"><span data-stu-id="f1451-110">The actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="f1451-111">Viene chiamato il metodo `OnActivateAsync` (C#) o `onActivateAsync` (Java), che può essere sottoposto a override nell'implementazione dell'attore.</span><span class="sxs-lookup"><span data-stu-id="f1451-111">The `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span></span>
* <span data-ttu-id="f1451-112">A questo punto l'attore è considerato attivo.</span><span class="sxs-lookup"><span data-stu-id="f1451-112">The actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="f1451-113">Disattivazione di un attore</span><span class="sxs-lookup"><span data-stu-id="f1451-113">Actor deactivation</span></span>
<span data-ttu-id="f1451-114">Quando un attore viene disattivato, si verifica quanto segue:</span><span class="sxs-lookup"><span data-stu-id="f1451-114">When an actor is deactivated, the following occurs:</span></span>

* <span data-ttu-id="f1451-115">Quando un attore rimane inutilizzato per un determinato periodo di tempo, viene rimosso dalla tabella degli attori attivi.</span><span class="sxs-lookup"><span data-stu-id="f1451-115">When an actor is not used for some period of time, it is removed from the Active Actors table.</span></span>
* <span data-ttu-id="f1451-116">Viene chiamato il metodo `OnDeactivateAsync` (C#) o `onDeactivateAsync` (Java), che può essere sottoposto a override nell'implementazione dell'attore.</span><span class="sxs-lookup"><span data-stu-id="f1451-116">The `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span></span> <span data-ttu-id="f1451-117">Ciò elimina tutti i timer dell'attore.</span><span class="sxs-lookup"><span data-stu-id="f1451-117">This clears all the timers for the actor.</span></span> <span data-ttu-id="f1451-118">Le operazioni dell'attore come le modifiche di stato non devono essere chiamate da questo metodo.</span><span class="sxs-lookup"><span data-stu-id="f1451-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="f1451-119">Il runtime di Fabric Actors emette alcuni [eventi relativi all'attivazione e alla disattivazione](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="f1451-119">The Fabric Actors runtime emits some [events related to actor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="f1451-120">che sono utili per la diagnostica e il monitoraggio delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="f1451-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="f1451-121">Garbage Collection degli attori</span><span class="sxs-lookup"><span data-stu-id="f1451-121">Actor garbage collection</span></span>
<span data-ttu-id="f1451-122">Quando un attore viene disattivato, i riferimenti all'oggetto corrispondente vengono rilasciati e l'attore può essere sottoposto a Garbage Collection dal garbage collector di Common Language Runtime (CLR) o di Java Virtual Machine (JVM).</span><span class="sxs-lookup"><span data-stu-id="f1451-122">When an actor is deactivated, references to the actor object are released and it can be garbage collected normally by the common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="f1451-123">L'operazione di Garbage Collection pulisce solo l'oggetto attore, ma **non** rimuove lo stato archiviato nel gestore di stato dell'attore.</span><span class="sxs-lookup"><span data-stu-id="f1451-123">Garbage collection only cleans up the actor object; it does **not** remove state stored in the actor's State Manager.</span></span> <span data-ttu-id="f1451-124">Alla successiva attivazione dell'attore viene creato un nuovo oggetto attore e viene ripristinato il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="f1451-124">The next time the actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="f1451-125">Quali criteri determinano l'uso degli attori ai fini della disattivazione e dell'operazione di Garbage Collection?</span><span class="sxs-lookup"><span data-stu-id="f1451-125">What counts as “being used” for the purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="f1451-126">Ricezione di una chiamata</span><span class="sxs-lookup"><span data-stu-id="f1451-126">Receiving a call</span></span>
* <span data-ttu-id="f1451-127">`IRemindable.ReceiveReminderAsync` (applicabile solo se l'attore usa promemoria)</span><span class="sxs-lookup"><span data-stu-id="f1451-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if the actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="f1451-128">Se l'attore usa i timer e viene eseguito il callback di timer, questa azione **non** viene considerata per determinare l'uso dell'attore.</span><span class="sxs-lookup"><span data-stu-id="f1451-128">if the actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="f1451-129">Prima di approfondire i concetti relativi alla disattivazione, è importante definire i termini seguenti:</span><span class="sxs-lookup"><span data-stu-id="f1451-129">Before we go into the details of deactivation, it is important to define the following terms:</span></span>

* <span data-ttu-id="f1451-130">*Intervallo di analisi*.</span><span class="sxs-lookup"><span data-stu-id="f1451-130">*Scan interval*.</span></span> <span data-ttu-id="f1451-131">Intervallo di tempo in cui il runtime di Actors esegue l'analisi della tabella degli attori attivi per identificare quelli che possono essere disattivati e sottoposti a Garbage Collection.</span><span class="sxs-lookup"><span data-stu-id="f1451-131">This is the interval at which the Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="f1451-132">Il valore predefinito è 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="f1451-132">The default value for this is 1 minute.</span></span>
* <span data-ttu-id="f1451-133">*Timeout di inattività*.</span><span class="sxs-lookup"><span data-stu-id="f1451-133">*Idle timeout*.</span></span> <span data-ttu-id="f1451-134">Periodo di tempo in cui un attore deve rimanere inutilizzato (inattivo) prima di poter essere disattivato e sottoposto a Garbage Collection.</span><span class="sxs-lookup"><span data-stu-id="f1451-134">This is the amount of time that an actor needs to remain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="f1451-135">Il valore predefinito è 60 minuti.</span><span class="sxs-lookup"><span data-stu-id="f1451-135">The default value for this is 60 minutes.</span></span>

<span data-ttu-id="f1451-136">Non è in genere necessario modificare questi valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="f1451-136">Typically, you do not need to change these defaults.</span></span> <span data-ttu-id="f1451-137">Se necessario, però, questi intervalli possono essere modificati tramite `ActorServiceSettings` durante la registrazione del [servizio Actor](service-fabric-reliable-actors-platform.md):</span><span class="sxs-lookup"><span data-stu-id="f1451-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        ActorRuntime.RegisterActorAsync<MyActor>((context, actorType) =>
                new ActorService(context, actorType,
                    settings:
                        new ActorServiceSettings()
                        {
                            ActorGarbageCollectionSettings =
                                new ActorGarbageCollectionSettings(10, 2)
                        }))
            .GetAwaiter()
            .GetResult();
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
    }
}
```
<span data-ttu-id="f1451-138">Per ogni attore attivo, il runtime di Actors tiene traccia del periodo di inattività.</span><span class="sxs-lookup"><span data-stu-id="f1451-138">For each active actor, the actor runtime keeps track of the amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="f1451-139">Il runtime di Actors controlla ogni attore in base alla frequenza definita da `ScanIntervalInSeconds` per verificare se può essere sottoposto a Garbage Collection e determina se l'attore è rimasto inattivo per il numero di secondi definito da `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="f1451-139">The actor runtime checks each of the actors every `ScanIntervalInSeconds` to see if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="f1451-140">Ogni volta che un attore viene usato, il periodo di inattività viene reimpostato su 0.</span><span class="sxs-lookup"><span data-stu-id="f1451-140">Anytime an actor is used, its idle time is reset to 0.</span></span> <span data-ttu-id="f1451-141">A questo punto, l'attore può essere sottoposto a Garbage Collection solo se rimane nuovamente inattivo per il numero di secondi definito da `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="f1451-141">After this, the actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="f1451-142">È importante ricordare che l'uso di un attore è determinato in base all'esecuzione di un metodo di interfaccia o di un callback di promemoria dell'attore.</span><span class="sxs-lookup"><span data-stu-id="f1451-142">Recall that an actor is considered to have been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="f1451-143">L'uso di un attore **non** è determinato in base all'esecuzione del callback dei timer.</span><span class="sxs-lookup"><span data-stu-id="f1451-143">An actor is **not** considered to have been used if its timer callback is executed.</span></span>

<span data-ttu-id="f1451-144">Il diagramma seguente mostra il ciclo di vita di un unico attore per illustrare questi concetti.</span><span class="sxs-lookup"><span data-stu-id="f1451-144">The following diagram shows the lifecycle of a single actor to illustrate these concepts.</span></span>

![Esempio del tempo di inattività][1]

<span data-ttu-id="f1451-146">Nell'esempio viene illustrato l'impatto delle chiamate ai metodi degli attori, dei promemoria e dei timer sulla durata dell'attore.</span><span class="sxs-lookup"><span data-stu-id="f1451-146">The example shows the impact of actor method calls, reminders, and timers on the lifetime of this actor.</span></span> <span data-ttu-id="f1451-147">Per questo esempio è opportuno evidenziare i punti seguenti:</span><span class="sxs-lookup"><span data-stu-id="f1451-147">The following points about the example are worth mentioning:</span></span>

* <span data-ttu-id="f1451-148">ScanInterval e IdleTimeout sono impostati rispettivamente su 5 e 10.</span><span class="sxs-lookup"><span data-stu-id="f1451-148">ScanInterval and IdleTimeout are set to 5 and 10 respectively.</span></span> <span data-ttu-id="f1451-149">(Unità non è rilevante in questo caso, poiché l’obiettivo è solo di illustrare il concetto.)</span><span class="sxs-lookup"><span data-stu-id="f1451-149">(Units do not matter here, since our purpose is only to illustrate the concept.)</span></span>
* <span data-ttu-id="f1451-150">L'analisi degli attori da sottoporre a Garbage Collection viene eseguita in T=0,5,10,15,20,25, come definito dall’intervallo di analisi di 5.</span><span class="sxs-lookup"><span data-stu-id="f1451-150">The scan for actors to be garbage collected happens at T=0,5,10,15,20,25, as defined by the scan interval of 5.</span></span>
* <span data-ttu-id="f1451-151">Viene attivato un timer periodico in T=4,8,12,16,20,24 e ne viene eseguito il callback.</span><span class="sxs-lookup"><span data-stu-id="f1451-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="f1451-152">Questo non influisce sul tempo di inattività dell'attore.</span><span class="sxs-lookup"><span data-stu-id="f1451-152">It does not impact the idle time of the actor.</span></span>
* <span data-ttu-id="f1451-153">Una chiamata a un metodo dell'attore in T=7 reimposta il tempo di inattività su 0 ritardando l'operazione di Garbage Collection dell'attore.</span><span class="sxs-lookup"><span data-stu-id="f1451-153">An actor method call at T=7 resets the idle time to 0 and delays the garbage collection of the actor.</span></span>
* <span data-ttu-id="f1451-154">Un callback di promemoria dell'attore eseguito in T=14 ritarda ulteriormente l'operazione di Garbage Collection dell'attore.</span><span class="sxs-lookup"><span data-stu-id="f1451-154">An actor reminder callback executes at T=14 and further delays the garbage collection of the actor.</span></span>
* <span data-ttu-id="f1451-155">Durante l'analisi di Garbage Collection in T=25, il tempo di inattività dell'attore supera infine il timeout di inattività di 10 e l'attore viene sottoposto a Garbage Collection.</span><span class="sxs-lookup"><span data-stu-id="f1451-155">During the garbage collection scan at T=25, the actor's idle time finally exceeds the idle timeout of 10, and the actor is garbage collected.</span></span>

<span data-ttu-id="f1451-156">Un attore non viene mai sottoposto a Garbage Collection mentre è in esecuzione uno dei relativi metodi, indipendentemente dal tempo impiegato per l'esecuzione di tale metodo.</span><span class="sxs-lookup"><span data-stu-id="f1451-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="f1451-157">Come accennato in precedenza, l'esecuzione dei metodi dell'interfaccia dell'attore e dei callback di promemoria impedisce l'operazione di Garbage Collection, reimpostando su 0 il tempo di inattività dell'attore.</span><span class="sxs-lookup"><span data-stu-id="f1451-157">As mentioned earlier, the execution of actor interface methods and reminder callbacks prevents garbage collection by resetting the actor's idle time to 0.</span></span> <span data-ttu-id="f1451-158">L'esecuzione di callback di timer non ha invece l'effetto di reimpostare su 0 il tempo di inattività.</span><span class="sxs-lookup"><span data-stu-id="f1451-158">The execution of timer callbacks does not reset the idle time to 0.</span></span> <span data-ttu-id="f1451-159">Tuttavia, l'operazione di Garbage Collection dell'attore viene rinviata finché il callback di timer non ha completato l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f1451-159">However, the garbage collection of the actor is deferred until the timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="f1451-160">Eliminazione di attori e del relativo stato</span><span class="sxs-lookup"><span data-stu-id="f1451-160">Deleting actors and their state</span></span>
<span data-ttu-id="f1451-161">L'operazione di Garbage Collection degli attori disattivati pulisce solo l'oggetto attore, ma non rimuove i dati archiviati in State Manager dell'attore.</span><span class="sxs-lookup"><span data-stu-id="f1451-161">Garbage collection of deactivated actors only cleans up the actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="f1451-162">Quando un attore viene riattivato, i suoi dati vengono nuovamente resi disponibili tramite il gestore di stato.</span><span class="sxs-lookup"><span data-stu-id="f1451-162">When an actor is re-activated, its data is again made available to it through the State Manager.</span></span> <span data-ttu-id="f1451-163">Nei casi in cui gli attori archiviano dati nel gestore di stato e vengono disattivati ma mai riattivati, può essere necessario pulire i relativi dati.</span><span class="sxs-lookup"><span data-stu-id="f1451-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary to clean up their data.</span></span>

<span data-ttu-id="f1451-164">Il [servizio Actor](service-fabric-reliable-actors-platform.md) fornisce anche una funzione per l'eliminazione di attori da un chiamante remoto:</span><span class="sxs-lookup"><span data-stu-id="f1451-164">The [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="f1451-165">L'eliminazione di un attore produce gli effetti seguenti, a seconda del fatto che l'attore sia attualmente attivo o meno:</span><span class="sxs-lookup"><span data-stu-id="f1451-165">Deleting an actor has the following effects depending on whether or not the actor is currently active:</span></span>

* <span data-ttu-id="f1451-166">**Attore attivo**</span><span class="sxs-lookup"><span data-stu-id="f1451-166">**Active Actor**</span></span>
  * <span data-ttu-id="f1451-167">L'attore viene rimosso dall'elenco di attori attivi e viene disattivato.</span><span class="sxs-lookup"><span data-stu-id="f1451-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="f1451-168">Il suo stato viene eliminato definitivamente.</span><span class="sxs-lookup"><span data-stu-id="f1451-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="f1451-169">**Attore inattivo**</span><span class="sxs-lookup"><span data-stu-id="f1451-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="f1451-170">Il suo stato viene eliminato definitivamente.</span><span class="sxs-lookup"><span data-stu-id="f1451-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="f1451-171">Si noti che un attore non può chiamare un'operazione di eliminazione su se stesso da uno dei suoi metodi attore perché l'attore non può essere eliminato mentre è in esecuzione in un contesto di chiamata attore, in cui il runtime ha ottenuto un blocco per le chiamate dell'attore per applicare l'accesso a thread singolo.</span><span class="sxs-lookup"><span data-stu-id="f1451-171">Note that an actor cannot call delete on itself from one of its actor methods because the actor cannot be deleted while executing within an actor call context, in which the runtime has obtained a lock around the actor call to enforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1451-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f1451-172">Next steps</span></span>
* [<span data-ttu-id="f1451-173">Timer e promemoria degli attori</span><span class="sxs-lookup"><span data-stu-id="f1451-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="f1451-174">Eventi relativi agli attori</span><span class="sxs-lookup"><span data-stu-id="f1451-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="f1451-175">Rientranza di Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="f1451-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="f1451-176">Diagnostica e monitoraggio delle prestazioni per Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="f1451-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="f1451-177">Documentazione di riferimento delle API di Actors</span><span class="sxs-lookup"><span data-stu-id="f1451-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="f1451-178">Codice di esempio C#</span><span class="sxs-lookup"><span data-stu-id="f1451-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="f1451-179">Codice di esempio Java</span><span class="sxs-lookup"><span data-stu-id="f1451-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
