---
title: aaaOverview del ciclo di vita microservizi Azure basato su attori | Documenti Microsoft
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
ms.openlocfilehash: a7926e372449048f0a579c2c58573754a4a82363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="01962-103">Ciclo di vita degli attori, Garbage Collection automatica ed eliminazione manuale</span><span class="sxs-lookup"><span data-stu-id="01962-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="01962-104">Viene attivato un attore hello prima volta che è una chiamata tooany dei relativi metodi.</span><span class="sxs-lookup"><span data-stu-id="01962-104">An actor is activated hello first time a call is made tooany of its methods.</span></span> <span data-ttu-id="01962-105">Un attore è disattivata (sottoposti a garbage collection dal runtime di attori hello) se non viene usato per un periodo di tempo configurabile.</span><span class="sxs-lookup"><span data-stu-id="01962-105">An actor is deactivated (garbage collected by hello Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="01962-106">Un attore e il relativo stato possono essere eliminati manualmente in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="01962-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="01962-107">Attivazione di un attore</span><span class="sxs-lookup"><span data-stu-id="01962-107">Actor activation</span></span>
<span data-ttu-id="01962-108">Quando viene attivato un attore, si verifica hello segue:</span><span class="sxs-lookup"><span data-stu-id="01962-108">When an actor is activated, hello following occurs:</span></span>

* <span data-ttu-id="01962-109">Quando viene effettuata una chiamata per un attore che non è ancora attivo, viene creato un nuovo attore.</span><span class="sxs-lookup"><span data-stu-id="01962-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="01962-110">Se mantiene lo stato, dello stato dell'actor Hello viene caricato.</span><span class="sxs-lookup"><span data-stu-id="01962-110">hello actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="01962-111">Hello `OnActivateAsync` (c#) o `onActivateAsync` (linguaggio) (che può essere sottoposto a override in una implementazione attore hello) viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="01962-111">hello `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span>
* <span data-ttu-id="01962-112">attore Hello a questo punto viene considerato attivo.</span><span class="sxs-lookup"><span data-stu-id="01962-112">hello actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="01962-113">Disattivazione di un attore</span><span class="sxs-lookup"><span data-stu-id="01962-113">Actor deactivation</span></span>
<span data-ttu-id="01962-114">Quando un attore è disattivato, si verifica hello segue:</span><span class="sxs-lookup"><span data-stu-id="01962-114">When an actor is deactivated, hello following occurs:</span></span>

* <span data-ttu-id="01962-115">Quando un attore non viene utilizzato per un certo periodo di tempo, viene rimosso dalla tabella attori hello.</span><span class="sxs-lookup"><span data-stu-id="01962-115">When an actor is not used for some period of time, it is removed from hello Active Actors table.</span></span>
* <span data-ttu-id="01962-116">Hello `OnDeactivateAsync` (c#) o `onDeactivateAsync` (linguaggio) (che può essere sottoposto a override in una implementazione attore hello) viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="01962-116">hello `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span> <span data-ttu-id="01962-117">Consente di cancellare tutti i timer hello per attore hello.</span><span class="sxs-lookup"><span data-stu-id="01962-117">This clears all hello timers for hello actor.</span></span> <span data-ttu-id="01962-118">Le operazioni dell'attore come le modifiche di stato non devono essere chiamate da questo metodo.</span><span class="sxs-lookup"><span data-stu-id="01962-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="01962-119">Hello attori dell'infrastruttura runtime genera alcuni [gli eventi correlati tooactor attivazione e disattivazione](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="01962-119">hello Fabric Actors runtime emits some [events related tooactor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="01962-120">che sono utili per la diagnostica e il monitoraggio delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="01962-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="01962-121">Garbage Collection degli attori</span><span class="sxs-lookup"><span data-stu-id="01962-121">Actor garbage collection</span></span>
<span data-ttu-id="01962-122">Quando un attore è disattivato, vengono rilasciati oggetto attore toohello di riferimenti e può essere sottoposto a garbage collection in genere da hello common language runtime (CLR) o il garbage collector di java virtual machine (JVM).</span><span class="sxs-lookup"><span data-stu-id="01962-122">When an actor is deactivated, references toohello actor object are released and it can be garbage collected normally by hello common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="01962-123">Operazione di Garbage collection pulizia solo oggetto attore hello. caso **non** rimuovere stato archiviato in gestore degli Stati dell'attore hello.</span><span class="sxs-lookup"><span data-stu-id="01962-123">Garbage collection only cleans up hello actor object; it does **not** remove state stored in hello actor's State Manager.</span></span> <span data-ttu-id="01962-124">Hello successiva ora hello actor viene attivato, viene creato un nuovo oggetto attore e viene ripristinato lo stato.</span><span class="sxs-lookup"><span data-stu-id="01962-124">hello next time hello actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="01962-125">Ciò che conta come "in uso" scopo hello di garbage collection e la disattivazione?</span><span class="sxs-lookup"><span data-stu-id="01962-125">What counts as “being used” for hello purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="01962-126">Ricezione di una chiamata</span><span class="sxs-lookup"><span data-stu-id="01962-126">Receiving a call</span></span>
* <span data-ttu-id="01962-127">`IRemindable.ReceiveReminderAsync`metodo richiamato (applicabile solo se attore hello utilizza promemoria)</span><span class="sxs-lookup"><span data-stu-id="01962-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if hello actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="01962-128">Se l'attore hello Usa timer e viene richiamato il callback del timer, non **non** vengono considerate come "in uso".</span><span class="sxs-lookup"><span data-stu-id="01962-128">if hello actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="01962-129">Prima di esplorare in dettaglio hello di disattivazione, è importante toodefine hello seguenti termini:</span><span class="sxs-lookup"><span data-stu-id="01962-129">Before we go into hello details of deactivation, it is important toodefine hello following terms:</span></span>

* <span data-ttu-id="01962-130">*Intervallo di analisi*.</span><span class="sxs-lookup"><span data-stu-id="01962-130">*Scan interval*.</span></span> <span data-ttu-id="01962-131">Questo è l'intervallo di hello in cui hello attori runtime cerca la tabella di attori attori che possono essere disattivati e raccolti nel Garbage Collector.</span><span class="sxs-lookup"><span data-stu-id="01962-131">This is hello interval at which hello Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="01962-132">il valore predefinito Hello per è 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="01962-132">hello default value for this is 1 minute.</span></span>
* <span data-ttu-id="01962-133">*Timeout di inattività*.</span><span class="sxs-lookup"><span data-stu-id="01962-133">*Idle timeout*.</span></span> <span data-ttu-id="01962-134">Si tratta hello quantità di tempo che un attore è tenuto tooremain inutilizzati (inattivo) prima che può essere disattivata e raccolti nel Garbage Collector.</span><span class="sxs-lookup"><span data-stu-id="01962-134">This is hello amount of time that an actor needs tooremain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="01962-135">il valore predefinito Hello per è 60 minuti.</span><span class="sxs-lookup"><span data-stu-id="01962-135">hello default value for this is 60 minutes.</span></span>

<span data-ttu-id="01962-136">In genere, non è necessario toochange queste impostazioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="01962-136">Typically, you do not need toochange these defaults.</span></span> <span data-ttu-id="01962-137">Se necessario, però, questi intervalli possono essere modificati tramite `ActorServiceSettings` durante la registrazione del [servizio Actor](service-fabric-reliable-actors-platform.md):</span><span class="sxs-lookup"><span data-stu-id="01962-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

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
<span data-ttu-id="01962-138">Per ogni attore active, hello attore runtime tiene traccia di hello periodo di tempo che è stata inattiva (ossia, non utilizzato).</span><span class="sxs-lookup"><span data-stu-id="01962-138">For each active actor, hello actor runtime keeps track of hello amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="01962-139">Hello attore runtime controlla ogni degli attori hello ogni `ScanIntervalInSeconds` toosee se garbage possono essere raccolti e raccoglie se è rimasto inattivo per `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="01962-139">hello actor runtime checks each of hello actors every `ScanIntervalInSeconds` toosee if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="01962-140">Ogni volta che viene utilizzato un attore, il tempo di inattività è too0 di reimpostazione.</span><span class="sxs-lookup"><span data-stu-id="01962-140">Anytime an actor is used, its idle time is reset too0.</span></span> <span data-ttu-id="01962-141">Successivamente, attore hello può essere sottoposto a garbage collection solo se nuovamente rimane inattivo per `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="01962-141">After this, hello actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="01962-142">Tenere presente che un attore è considerato toohave stato utilizzato se viene eseguito un metodo di interfaccia attore o un callback di promemoria attore.</span><span class="sxs-lookup"><span data-stu-id="01962-142">Recall that an actor is considered toohave been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="01962-143">Un attore fa **non** considerati toohave stato utilizzato se il callback del timer viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="01962-143">An actor is **not** considered toohave been used if its timer callback is executed.</span></span>

<span data-ttu-id="01962-144">Hello diagramma seguente mostra hello ciclo di vita di un tooillustrate singolo attore questi concetti.</span><span class="sxs-lookup"><span data-stu-id="01962-144">hello following diagram shows hello lifecycle of a single actor tooillustrate these concepts.</span></span>

![Esempio del tempo di inattività][1]

<span data-ttu-id="01962-146">esempio Hello Mostra impatto hello delle chiamate al metodo attore promemoria e timer durata hello dell'attore.</span><span class="sxs-lookup"><span data-stu-id="01962-146">hello example shows hello impact of actor method calls, reminders, and timers on hello lifetime of this actor.</span></span> <span data-ttu-id="01962-147">Hello seguenti punti sull'esempio hello è utile citare:</span><span class="sxs-lookup"><span data-stu-id="01962-147">hello following points about hello example are worth mentioning:</span></span>

* <span data-ttu-id="01962-148">ScanInterval e IdleTimeout vengono impostati too5 e 10.</span><span class="sxs-lookup"><span data-stu-id="01962-148">ScanInterval and IdleTimeout are set too5 and 10 respectively.</span></span> <span data-ttu-id="01962-149">(Unità non è rilevante in questo caso, poiché il nostro obiettivo è solo il concetto di hello tooillustrate.)</span><span class="sxs-lookup"><span data-stu-id="01962-149">(Units do not matter here, since our purpose is only tooillustrate hello concept.)</span></span>
* <span data-ttu-id="01962-150">analisi di Hello per attori toobe sottoposto a garbage collection avviene a T = 0, 5, 10, 15, 20, 25, come definito da intervallo di analisi hello pari a 5.</span><span class="sxs-lookup"><span data-stu-id="01962-150">hello scan for actors toobe garbage collected happens at T=0,5,10,15,20,25, as defined by hello scan interval of 5.</span></span>
* <span data-ttu-id="01962-151">Viene attivato un timer periodico in T=4,8,12,16,20,24 e ne viene eseguito il callback.</span><span class="sxs-lookup"><span data-stu-id="01962-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="01962-152">Tempo di inattività hello dell'attore hello non influire.</span><span class="sxs-lookup"><span data-stu-id="01962-152">It does not impact hello idle time of hello actor.</span></span>
* <span data-ttu-id="01962-153">Una chiamata al metodo attore T = 7 Reimposta too0 tempo di inattività hello e ritardi hello operazione di garbage collection attore hello.</span><span class="sxs-lookup"><span data-stu-id="01962-153">An actor method call at T=7 resets hello idle time too0 and delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="01962-154">Esegue un callback di promemoria attore in T = 14 e ulteriori ritardi hello attore hello operazione di garbage collection.</span><span class="sxs-lookup"><span data-stu-id="01962-154">An actor reminder callback executes at T=14 and further delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="01962-155">Durante la hello analisi di garbage collection T = 25, tempo di inattività dell'attore hello supera infine hello timeout di inattività di 10 e attore hello è sottoposto a garbage collection.</span><span class="sxs-lookup"><span data-stu-id="01962-155">During hello garbage collection scan at T=25, hello actor's idle time finally exceeds hello idle timeout of 10, and hello actor is garbage collected.</span></span>

<span data-ttu-id="01962-156">Un attore non viene mai sottoposto a Garbage Collection mentre è in esecuzione uno dei relativi metodi, indipendentemente dal tempo impiegato per l'esecuzione di tale metodo.</span><span class="sxs-lookup"><span data-stu-id="01962-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="01962-157">Come accennato in precedenza, esecuzione hello di metodi di interfaccia attore e i callback di promemoria impedisce operazioni di garbage collection reimpostando too0 tempo di inattività dell'attore hello.</span><span class="sxs-lookup"><span data-stu-id="01962-157">As mentioned earlier, hello execution of actor interface methods and reminder callbacks prevents garbage collection by resetting hello actor's idle time too0.</span></span> <span data-ttu-id="01962-158">esecuzione di Hello di callback del timer non reimposta too0 tempo di inattività hello.</span><span class="sxs-lookup"><span data-stu-id="01962-158">hello execution of timer callbacks does not reset hello idle time too0.</span></span> <span data-ttu-id="01962-159">Tuttavia, hello operazione di garbage collection attore hello viene posticipata finché non callback del timer hello ha completato l'esecuzione.</span><span class="sxs-lookup"><span data-stu-id="01962-159">However, hello garbage collection of hello actor is deferred until hello timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="01962-160">Eliminazione di attori e del relativo stato</span><span class="sxs-lookup"><span data-stu-id="01962-160">Deleting actors and their state</span></span>
<span data-ttu-id="01962-161">Operazione di Garbage collection di attori disattivati la pulizia solo oggetto attore hello, ma non rimuove i dati archiviati nella console di gestione dello stato dell'attore.</span><span class="sxs-lookup"><span data-stu-id="01962-161">Garbage collection of deactivated actors only cleans up hello actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="01962-162">Quando un attore viene nuovamente attivato, i dati diventa nuovamente disponibile tooit tramite hello gestore degli stati.</span><span class="sxs-lookup"><span data-stu-id="01962-162">When an actor is re-activated, its data is again made available tooit through hello State Manager.</span></span> <span data-ttu-id="01962-163">Nei casi in attori archiviare i dati nella console di gestione dello stato e sono disattivati ma mai nuovamente attivati, potrebbe essere necessario tooclean dei propri dati.</span><span class="sxs-lookup"><span data-stu-id="01962-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary tooclean up their data.</span></span>

<span data-ttu-id="01962-164">Hello [servizio Actor](service-fabric-reliable-actors-platform.md) fornisce una funzione per l'eliminazione di attori da un chiamante remoto:</span><span class="sxs-lookup"><span data-stu-id="01962-164">hello [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

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

<span data-ttu-id="01962-165">L'eliminazione di un attore è hello seguenti effetti a seconda che sia o meno attore hello attivo:</span><span class="sxs-lookup"><span data-stu-id="01962-165">Deleting an actor has hello following effects depending on whether or not hello actor is currently active:</span></span>

* <span data-ttu-id="01962-166">**Attore attivo**</span><span class="sxs-lookup"><span data-stu-id="01962-166">**Active Actor**</span></span>
  * <span data-ttu-id="01962-167">L'attore viene rimosso dall'elenco di attori attivi e viene disattivato.</span><span class="sxs-lookup"><span data-stu-id="01962-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="01962-168">Il suo stato viene eliminato definitivamente.</span><span class="sxs-lookup"><span data-stu-id="01962-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="01962-169">**Attore inattivo**</span><span class="sxs-lookup"><span data-stu-id="01962-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="01962-170">Il suo stato viene eliminato definitivamente.</span><span class="sxs-lookup"><span data-stu-id="01962-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="01962-171">Si noti che non è possibile chiamare un attore eliminare su se stesso da uno dei relativi metodi attore perché attore hello non può essere eliminato durante l'esecuzione all'interno di un contesto di chiamata attore, in cui hello runtime ha ottenuto un blocco per hello attore chiamata tooenforce accesso a thread singolo.</span><span class="sxs-lookup"><span data-stu-id="01962-171">Note that an actor cannot call delete on itself from one of its actor methods because hello actor cannot be deleted while executing within an actor call context, in which hello runtime has obtained a lock around hello actor call tooenforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01962-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="01962-172">Next steps</span></span>
* [<span data-ttu-id="01962-173">Timer e promemoria degli attori</span><span class="sxs-lookup"><span data-stu-id="01962-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="01962-174">Eventi relativi agli attori</span><span class="sxs-lookup"><span data-stu-id="01962-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="01962-175">Rientranza di Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="01962-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="01962-176">Diagnostica e monitoraggio delle prestazioni per Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="01962-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="01962-177">Documentazione di riferimento delle API di Actors</span><span class="sxs-lookup"><span data-stu-id="01962-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="01962-178">Codice di esempio C#</span><span class="sxs-lookup"><span data-stu-id="01962-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="01962-179">Codice di esempio Java</span><span class="sxs-lookup"><span data-stu-id="01962-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
