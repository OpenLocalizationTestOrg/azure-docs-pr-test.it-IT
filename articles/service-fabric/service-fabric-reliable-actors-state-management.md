---
title: Gestione stato attori aaaReliable | Documenti Microsoft
description: "Descrive come viene gestito lo stato di Reliable Actors, reso persistente e replicato per la disponibilità elevata."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 37cf466a-5293-44c0-a4e0-037e5d292214
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 346d92426b1890617d108a9504afb179e463bded
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-state-management"></a><span data-ttu-id="36d3c-103">Gestione dello stato di Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="36d3c-103">Reliable Actors state management</span></span>
<span data-ttu-id="36d3c-104">I Reliable Actors sono oggetti a thread singolo che possono incapsulare sia la logica che lo stato.</span><span class="sxs-lookup"><span data-stu-id="36d3c-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="36d3c-105">Poiché gli operatori eseguiti in servizi affidabili, possono mantenere in modo affidabile stato utilizzando hello stessi meccanismi di persistenza e la replica che utilizza servizi affidabili.</span><span class="sxs-lookup"><span data-stu-id="36d3c-105">Because actors run on Reliable Services, they can maintain state reliably by using hello same persistence and replication mechanisms that Reliable Services uses.</span></span> <span data-ttu-id="36d3c-106">In questo modo, gli attori non perdano il proprio stato dopo errori, alla riattivazione dopo l'operazione di garbage collection o quando vengono spostati tra i nodi in un cluster a causa di bilanciamento del carico tooresource o aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="36d3c-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due tooresource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="36d3c-107">Replica e persistenza dello stato</span><span class="sxs-lookup"><span data-stu-id="36d3c-107">State persistence and replication</span></span>
<span data-ttu-id="36d3c-108">Vengono considerati tutti gli attori affidabile *stateful* perché l'ID univoco. tooa esegue il mapping di ogni istanza attore</span><span class="sxs-lookup"><span data-stu-id="36d3c-108">All Reliable Actors are considered *stateful* because each actor instance maps tooa unique ID.</span></span> <span data-ttu-id="36d3c-109">Ciò significa che toohello chiamate ripetute lo stesso ID attore vengono instradati toohello stessa istanza dell'attore.</span><span class="sxs-lookup"><span data-stu-id="36d3c-109">This means that repeated calls toohello same actor ID are routed toohello same actor instance.</span></span> <span data-ttu-id="36d3c-110">In un sistema senza stato, al contrario, il client chiama non è garantito toobe indirizzato toohello nello stesso server ogni volta.</span><span class="sxs-lookup"><span data-stu-id="36d3c-110">In a stateless system, by contrast, client calls are not guaranteed toobe routed toohello same server every time.</span></span> <span data-ttu-id="36d3c-111">Per questo motivo, i servizi Actor sono sempre servizi con stato.</span><span class="sxs-lookup"><span data-stu-id="36d3c-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="36d3c-112">Anche se gli attori sono considerati con stato, non significa che devono archiviare lo stato in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="36d3c-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="36d3c-113">Gli attori possono scegliere il livello di hello di persistenza dello stato e la replica in base ai propri dati i requisiti di archiviazione:</span><span class="sxs-lookup"><span data-stu-id="36d3c-113">Actors can choose hello level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="36d3c-114">**Uno stato persistente**: lo stato è toodisk persistente e viene replicata too3 o più repliche.</span><span class="sxs-lookup"><span data-stu-id="36d3c-114">**Persisted state**: State is persisted toodisk and is replicated too3 or more replicas.</span></span> <span data-ttu-id="36d3c-115">Si tratta di opzione di archiviazione dello stato più durevole hello, in cui lo stato può rendere persistente tramite interruzione completa del cluster.</span><span class="sxs-lookup"><span data-stu-id="36d3c-115">This is hello most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="36d3c-116">**Stato volatile**: stato non è replicato too3 o più repliche e mantenuto solo in memoria.</span><span class="sxs-lookup"><span data-stu-id="36d3c-116">**Volatile state**: State is replicated too3 or more replicas and only kept in memory.</span></span> <span data-ttu-id="36d3c-117">Fornisce la resilienza in caso di errore del nodo, di errore dell'attore e durante gli aggiornamenti e il bilanciamento delle risorse.</span><span class="sxs-lookup"><span data-stu-id="36d3c-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="36d3c-118">Tuttavia, lo stato non è persistente toodisk.</span><span class="sxs-lookup"><span data-stu-id="36d3c-118">However, state is not persisted toodisk.</span></span> <span data-ttu-id="36d3c-119">Se in una sola volta, vengono perse tutte le repliche, lo stato di hello è perso anche.</span><span class="sxs-lookup"><span data-stu-id="36d3c-119">So if all replicas are lost at once, hello state is lost as well.</span></span>
* <span data-ttu-id="36d3c-120">**Nessuno stato persistente**: stato non replicato o scritto toodisk.</span><span class="sxs-lookup"><span data-stu-id="36d3c-120">**No persisted state**: State is not replicated or written toodisk.</span></span> <span data-ttu-id="36d3c-121">Questo livello è per attori che non sufficiente stato toomaintain in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="36d3c-121">This level is for actors that simply don't need toomaintain state reliably.</span></span>

<span data-ttu-id="36d3c-122">Ogni livello di persistenza è semplicemente un altro *provider di stato* e un'altra configurazione di *replica* del servizio.</span><span class="sxs-lookup"><span data-stu-id="36d3c-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="36d3c-123">Stato viene scritto o meno toodisk dipende dal provider di stato hello - componente hello in un servizio affidabile che archivia lo stato.</span><span class="sxs-lookup"><span data-stu-id="36d3c-123">Whether or not state is written toodisk depends on hello state provider--hello component in a reliable service that stores state.</span></span> <span data-ttu-id="36d3c-124">La replica dipende dal numero di repliche con cui viene distribuito un servizio.</span><span class="sxs-lookup"><span data-stu-id="36d3c-124">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="36d3c-125">Come per i servizi affidabili, entrambi hello provider di stato e numero di repliche può essere facilmente impostato manualmente.</span><span class="sxs-lookup"><span data-stu-id="36d3c-125">As with Reliable Services, both hello state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="36d3c-126">framework attore Hello fornisce un attributo che, quando viene utilizzata su un attore, seleziona automaticamente un provider di stato predefinito e genera automaticamente le impostazioni per la replica conteggio tooachieve una di queste tre impostazioni di persistenza.</span><span class="sxs-lookup"><span data-stu-id="36d3c-126">hello actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count tooachieve one of these three persistence settings.</span></span> <span data-ttu-id="36d3c-127">attributo StatePersistence Hello non viene ereditato dalla classe derivata, ogni tipo di attore deve fornire il proprio livello StatePersistence.</span><span class="sxs-lookup"><span data-stu-id="36d3c-127">hello StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="36d3c-128">Stato persistente</span><span class="sxs-lookup"><span data-stu-id="36d3c-128">Persisted state</span></span>
```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl  extends FabricActor implements MyActor
{
}
```  
<span data-ttu-id="36d3c-129">Questa impostazione utilizza un provider di stato che archivia i dati su disco e di imposta automaticamente hello servizio replica conteggio too3.</span><span class="sxs-lookup"><span data-stu-id="36d3c-129">This setting uses a state provider that stores data on disk and automatically sets hello service replica count too3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="36d3c-130">Stato volatile</span><span class="sxs-lookup"><span data-stu-id="36d3c-130">Volatile state</span></span>
```csharp
[StatePersistence(StatePersistence.Volatile)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Volatile)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
<span data-ttu-id="36d3c-131">Questa impostazione viene utilizzato un provider di stato in memoria-solo e set hello too3 conteggio di replica.</span><span class="sxs-lookup"><span data-stu-id="36d3c-131">This setting uses an in-memory-only state provider and sets hello replica count too3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="36d3c-132">Stato non persistente</span><span class="sxs-lookup"><span data-stu-id="36d3c-132">No persisted state</span></span>
```csharp
[StatePersistence(StatePersistence.None)]
class MyActor : Actor, IMyActor
{
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.None)
class MyActorImpl extends FabricActor implements MyActor
{
}
```
<span data-ttu-id="36d3c-133">Questa impostazione viene utilizzato un provider di stato in memoria-solo e set hello too1 conteggio di replica.</span><span class="sxs-lookup"><span data-stu-id="36d3c-133">This setting uses an in-memory-only state provider and sets hello replica count too1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="36d3c-134">Impostazioni predefinite e impostazioni generate</span><span class="sxs-lookup"><span data-stu-id="36d3c-134">Defaults and generated settings</span></span>
<span data-ttu-id="36d3c-135">Quando si utilizza hello `StatePersistence` attributo, un provider di stato viene selezionato automaticamente in fase di esecuzione all'avvio del servizio actor hello.</span><span class="sxs-lookup"><span data-stu-id="36d3c-135">When you're using hello `StatePersistence` attribute, a state provider is automatically selected for you at runtime when hello actor service starts.</span></span> <span data-ttu-id="36d3c-136">numero di repliche Hello, tuttavia, è impostata in fase di compilazione da hello attore di Visual Studio gli strumenti di compilazione.</span><span class="sxs-lookup"><span data-stu-id="36d3c-136">hello replica count, however, is set at compile time by hello Visual Studio actor build tools.</span></span> <span data-ttu-id="36d3c-137">Hello strumenti di compilazione di generano automaticamente un *servizio predefinito* per servizio actor hello in ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="36d3c-137">hello build tools automatically generate a *default service* for hello actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="36d3c-138">I parametri vengono creati per le **dimensioni minime del set di repliche** e le **dimensioni del set di repliche di destinazione**.</span><span class="sxs-lookup"><span data-stu-id="36d3c-138">Parameters are created for **min replica set size** and **target replica set size**.</span></span>

<span data-ttu-id="36d3c-139">È possibile cambiare questi parametri manualmente.</span><span class="sxs-lookup"><span data-stu-id="36d3c-139">You can change these parameters manually.</span></span> <span data-ttu-id="36d3c-140">Ma ogni hello ora `StatePersistence` attributo viene modificato, i parametri di hello vengono impostati toohello replica set di dimensioni predefinite per hello selezionato `StatePersistence` attributo, si esegue l'override di eventuali valori precedenti.</span><span class="sxs-lookup"><span data-stu-id="36d3c-140">But each time hello `StatePersistence` attribute is changed, hello parameters are set toohello default replica set size values for hello selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="36d3c-141">In altre parole, i valori hello impostati in ServiceManifest.xml sono *solo* sottoposto a override in fase di compilazione quando si modifica hello `StatePersistence` valore dell'attributo.</span><span class="sxs-lookup"><span data-stu-id="36d3c-141">In other words, hello values that you set in ServiceManifest.xml are *only* overridden at build time when you change hello `StatePersistence` attribute value.</span></span>

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application12Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="MyActorService_PartitionCount" DefaultValue="10" />
      <Parameter Name="MyActorService_MinReplicaSetSize" DefaultValue="3" />
      <Parameter Name="MyActorService_TargetReplicaSetSize" DefaultValue="3" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyActorPkg" ServiceManifestVersion="1.0.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MyActorService" GeneratedIdRef="77d965dc-85fb-488c-bd06-c6c1fe29d593|Persisted">
         <StatefulService ServiceTypeName="MyActorServiceType" TargetReplicaSetSize="[MyActorService_TargetReplicaSetSize]" MinReplicaSetSize="[MyActorService_MinReplicaSetSize]">
            <UniformInt64Partition PartitionCount="[MyActorService_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
         </StatefulService>
      </Service>
   </DefaultServices>
</ApplicationManifest>
```

## <a name="state-manager"></a><span data-ttu-id="36d3c-142">State Manager</span><span class="sxs-lookup"><span data-stu-id="36d3c-142">State manager</span></span>
<span data-ttu-id="36d3c-143">Ogni istanza dell'attore ha un proprio gestore di stato: una struttura di dati simile a un dizionario che archivia in modo affidabile le coppie chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="36d3c-143">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="36d3c-144">gestore degli stati Hello è un wrapper per un provider di stato.</span><span class="sxs-lookup"><span data-stu-id="36d3c-144">hello state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="36d3c-145">È possibile utilizzarlo toostore dati indipendentemente dall'impostazione della persistenza viene utilizzato.</span><span class="sxs-lookup"><span data-stu-id="36d3c-145">You can use it toostore data regardless of which persistence setting is used.</span></span> <span data-ttu-id="36d3c-146">Non fornisce alcuna garanzia che un servizio actor in esecuzione può essere modificato da un tooa impostazione allo stato volatile (in memoria-solo) persistente impostazione dello stato tramite un aggiornamento in sequenza, mantenendo i dati.</span><span class="sxs-lookup"><span data-stu-id="36d3c-146">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting tooa persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="36d3c-147">Tuttavia, è il numero di repliche toochange possibili per un servizio in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="36d3c-147">However, it is possible toochange replica count for a running service.</span></span>

<span data-ttu-id="36d3c-148">Le chiavi di gestione dello stato devono essere stringhe.</span><span class="sxs-lookup"><span data-stu-id="36d3c-148">State manager keys must be strings.</span></span> <span data-ttu-id="36d3c-149">I valori sono di tipo generico e possono essere di qualsiasi tipo, inclusi i tipi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="36d3c-149">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="36d3c-150">I valori archiviati nella console di gestione stato hello devono essere il contratto dati serializzabile perché potrebbe essere trasmesso su nodi tooother hello durante la replica e potrebbero essere scritti toodisk, a seconda delle impostazioni di persistenza dello stato di un attore.</span><span class="sxs-lookup"><span data-stu-id="36d3c-150">Values stored in hello state manager must be data contract serializable because they might be transmitted over hello network tooother nodes during replication and might be written toodisk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="36d3c-151">gestore degli stati Hello espone i metodi di dizionario comuni per la gestione dello stato, simile toothose trovato nel dizionario affidabile.</span><span class="sxs-lookup"><span data-stu-id="36d3c-151">hello state manager exposes common dictionary methods for managing state, similar toothose found in Reliable Dictionary.</span></span>

### <a name="accessing-state"></a><span data-ttu-id="36d3c-152">Accesso allo stato</span><span class="sxs-lookup"><span data-stu-id="36d3c-152">Accessing state</span></span>
<span data-ttu-id="36d3c-153">Stato sono accessibili tramite il gestore dello stato di hello dalla chiave.</span><span class="sxs-lookup"><span data-stu-id="36d3c-153">State can be accessed through hello state manager by key.</span></span> <span data-ttu-id="36d3c-154">I metodi del gestore di stato sono tutti asincroni perché possono richiedere operazioni di I/O del disco quando gli attori hanno uno stato persistente.</span><span class="sxs-lookup"><span data-stu-id="36d3c-154">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span></span> <span data-ttu-id="36d3c-155">Al primo accesso, gli oggetti di stato vengono memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="36d3c-155">Upon first access, state objects are cached in memory.</span></span> <span data-ttu-id="36d3c-156">Le operazioni di accesso ripetute accedono agli oggetti direttamente dalla memoria e vengono restituite in modo sincrono senza incorrere nel sovraccarico di operazioni di I/O del disco o di cambio di contesto asincrono.</span><span class="sxs-lookup"><span data-stu-id="36d3c-156">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span></span> <span data-ttu-id="36d3c-157">Un oggetto di stato viene rimosso dalla cache di hello in hello seguenti casi:</span><span class="sxs-lookup"><span data-stu-id="36d3c-157">A state object is removed from hello cache in hello following cases:</span></span>

* <span data-ttu-id="36d3c-158">Un metodo attore genera un'eccezione non gestita dopo un oggetto viene recuperato da Gestione stato hello.</span><span class="sxs-lookup"><span data-stu-id="36d3c-158">An actor method throws an unhandled exception after it retrieves an object from hello state manager.</span></span>
* <span data-ttu-id="36d3c-159">Un attore viene riattivato dopo essere stato disattivato o dopo un errore.</span><span class="sxs-lookup"><span data-stu-id="36d3c-159">An actor is reactivated, either after being deactivated or after failure.</span></span>
* <span data-ttu-id="36d3c-160">pagine del provider di stato Hello stato toodisk.</span><span class="sxs-lookup"><span data-stu-id="36d3c-160">hello state provider pages state toodisk.</span></span> <span data-ttu-id="36d3c-161">Questo comportamento dipende dall'implementazione del provider di stato hello.</span><span class="sxs-lookup"><span data-stu-id="36d3c-161">This behavior depends on hello state provider implementation.</span></span> <span data-ttu-id="36d3c-162">provider di stato predefinito di Hello per hello `Persisted` impostazione ha questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="36d3c-162">hello default state provider for hello `Persisted` setting has this behavior.</span></span>

<span data-ttu-id="36d3c-163">È possibile recuperare lo stato tramite una normale *ottenere* operazione che genera `KeyNotFoundException`(c#) o `NoSuchElementException`(linguaggio), se non esiste una voce per la chiave di hello:</span><span class="sxs-lookup"><span data-stu-id="36d3c-163">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for hello key:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<int> GetCountAsync()
    {
        return this.StateManager.GetStateAsync<int>("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().getStateAsync("MyState");
    }
}
```

<span data-ttu-id="36d3c-164">Lo stato può essere recuperato anche con un metodo *TryGet* che non genera alcuna eccezione se non esiste una voce per la chiave:</span><span class="sxs-lookup"><span data-stu-id="36d3c-164">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span></span>

```csharp
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task<int> GetCountAsync()
    {
        ConditionalValue<int> result = await this.StateManager.TryGetStateAsync<int>("MyState");
        if (result.HasValue)
        {
            return result.Value;
        }

        return 0;
    }
}
```
```Java
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture<Integer> getCountAsync()
    {
        return this.stateManager().<Integer>tryGetStateAsync("MyState").thenApply(result -> {
            if (result.hasValue()) {
                return result.getValue();
            } else {
                return 0;
            });
    }
}
```

### <a name="saving-state"></a><span data-ttu-id="36d3c-165">Salvataggio dello stato</span><span class="sxs-lookup"><span data-stu-id="36d3c-165">Saving state</span></span>
<span data-ttu-id="36d3c-166">metodi di recupero di Hello stato manager restituire un oggetto tooan di riferimento nella memoria locale.</span><span class="sxs-lookup"><span data-stu-id="36d3c-166">hello state manager retrieval methods return a reference tooan object in local memory.</span></span> <span data-ttu-id="36d3c-167">Modifica di questo oggetto nella memoria locale da solo non provoca la toobe salvati in modo durevole.</span><span class="sxs-lookup"><span data-stu-id="36d3c-167">Modifying this object in local memory alone does not cause it toobe saved durably.</span></span> <span data-ttu-id="36d3c-168">Quando un oggetto viene recuperato da Gestione stato hello e modificato, è necessario reinserito hello stato manager toobe salvati in modo durevole.</span><span class="sxs-lookup"><span data-stu-id="36d3c-168">When an object is retrieved from hello state manager and modified, it must be reinserted into hello state manager toobe saved durably.</span></span>

<span data-ttu-id="36d3c-169">È possibile inserire lo stato tramite un non condizionale *impostare*, che è hello equivalente di hello `dictionary["key"] = value` sintassi:</span><span class="sxs-lookup"><span data-stu-id="36d3c-169">You can insert state by using an unconditional *Set*, which is hello equivalent of hello `dictionary["key"] = value` syntax:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task SetCountAsync(int value)
    {
        return this.StateManager.SetStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture setCountAsync(int value)
    {
        return this.stateManager().setStateAsync("MyState", value);
    }
}
```

<span data-ttu-id="36d3c-170">È possibile aggiungere lo stato tramite il metodo *Add*.</span><span class="sxs-lookup"><span data-stu-id="36d3c-170">You can add state by using an *Add* method.</span></span> <span data-ttu-id="36d3c-171">Questo metodo genera `InvalidOperationException`(c#) o `IllegalStateException`(linguaggio) durante il tentativo di tooadd una chiave già esistente.</span><span class="sxs-lookup"><span data-stu-id="36d3c-171">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries tooadd a key that already exists.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task AddCountAsync(int value)
    {
        return this.StateManager.AddStateAsync<int>("MyState", value);
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().addOrUpdateStateAsync("MyState", value, (key, old_value) -> old_value + value);
    }
}
```

<span data-ttu-id="36d3c-172">È possibile aggiungere lo stato anche con il metodo *TryAdd*.</span><span class="sxs-lookup"><span data-stu-id="36d3c-172">You can also add state by using a *TryAdd* method.</span></span> <span data-ttu-id="36d3c-173">Questo metodo non genera durante il tentativo di tooadd una chiave già esistente.</span><span class="sxs-lookup"><span data-stu-id="36d3c-173">This method does not throw when it tries tooadd a key that already exists.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task AddCountAsync(int value)
    {
        bool result = await this.StateManager.TryAddStateAsync<int>("MyState", value);

        if (result)
        {
            // Added successfully!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture addCountAsync(int value)
    {
        return this.stateManager().tryAddStateAsync("MyState", value).thenApply((result)->{
            if(result)
            {
                // Added successfully!
            }
        });
    }
}
```

<span data-ttu-id="36d3c-174">Alla fine di hello di un metodo attore, gestore degli stati hello Salva automaticamente tutti i valori che sono stati aggiunti o modificati da un'operazione insert o update.</span><span class="sxs-lookup"><span data-stu-id="36d3c-174">At hello end of an actor method, hello state manager automatically saves any values that have been added or modified by an insert or update operation.</span></span> <span data-ttu-id="36d3c-175">"Salva" può includere toodisk mantenimento e la replica, a seconda delle impostazioni di hello utilizzato.</span><span class="sxs-lookup"><span data-stu-id="36d3c-175">A "save" can include persisting toodisk and replication, depending on hello settings used.</span></span> <span data-ttu-id="36d3c-176">I valori che non sono stati modificati non vengono salvati in modo permanente né replicati.</span><span class="sxs-lookup"><span data-stu-id="36d3c-176">Values that have not been modified are not persisted or replicated.</span></span> <span data-ttu-id="36d3c-177">Se i valori non sono stati modificati, hello operazione di salvataggio non esegue alcuna operazione.</span><span class="sxs-lookup"><span data-stu-id="36d3c-177">If no values have been modified, hello save operation does nothing.</span></span> <span data-ttu-id="36d3c-178">Se il salvataggio ha esito negativo, hello stato modificato viene rimosso e lo stato originale di hello viene ricaricato.</span><span class="sxs-lookup"><span data-stu-id="36d3c-178">If saving fails, hello modified state is discarded and hello original state is reloaded.</span></span>

<span data-ttu-id="36d3c-179">È inoltre possibile salvare manualmente lo stato dal chiamante hello `SaveStateAsync` metodo attore hello base:</span><span class="sxs-lookup"><span data-stu-id="36d3c-179">You can also save state manually by calling hello `SaveStateAsync` method on hello actor base:</span></span>

```csharp
async Task IMyActor.SetCountAsync(int count)
{
    await this.StateManager.AddOrUpdateStateAsync("count", count, (key, value) => count > value ? count : value);

    await this.SaveStateAsync();
}
```
```Java
interface MyActor {
    CompletableFuture setCountAsync(int count)
    {
        this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value).thenApply();

        this.stateManager().saveStateAsync().thenApply();
    }
}
```

### <a name="removing-state"></a><span data-ttu-id="36d3c-180">Rimozione dello stato</span><span class="sxs-lookup"><span data-stu-id="36d3c-180">Removing state</span></span>
<span data-ttu-id="36d3c-181">È possibile rimuovere lo stato in modo permanente dal gestore degli Stati dell'attore hello chiamante *rimuovere* metodo.</span><span class="sxs-lookup"><span data-stu-id="36d3c-181">You can remove state permanently from an actor's state manager by calling hello *Remove* method.</span></span> <span data-ttu-id="36d3c-182">Questo metodo genera `KeyNotFoundException`(c#) o `NoSuchElementException`(linguaggio) durante il tentativo di tooremove una chiave che non esiste.</span><span class="sxs-lookup"><span data-stu-id="36d3c-182">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries tooremove a key that doesn't exist.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task RemoveCountAsync()
    {
        return this.StateManager.RemoveStateAsync("MyState");
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().removeStateAsync("MyState");
    }
}
```

<span data-ttu-id="36d3c-183">È inoltre possibile rimuovere in modo permanente lo stato tramite hello *TryRemove* metodo.</span><span class="sxs-lookup"><span data-stu-id="36d3c-183">You can also remove state permanently by using hello *TryRemove* method.</span></span> <span data-ttu-id="36d3c-184">Questo metodo non genera durante il tentativo di tooremove una chiave che non esiste.</span><span class="sxs-lookup"><span data-stu-id="36d3c-184">This method does not throw when it tries tooremove a key that does not exist.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public async Task RemoveCountAsync()
    {
        bool result = await this.StateManager.TryRemoveStateAsync("MyState");

        if (result)
        {
            // State removed!
        }
    }
}
```
```Java
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
class MyActorImpl extends FabricActor implements  MyActor
{
    public MyActorImpl(ActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture removeCountAsync()
    {
        return this.stateManager().tryRemoveStateAsync("MyState").thenApply((result)->{
            if(result)
            {
                // State removed!
            }
        });
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="36d3c-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="36d3c-185">Next steps</span></span>

<span data-ttu-id="36d3c-186">Stato che viene archiviato in Reliable Actors deve essere serializzato prima relativo toodisk scritta e replicato per la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="36d3c-186">State that's stored in Reliable Actors must be serialized before its written toodisk and replicated for high availability.</span></span> <span data-ttu-id="36d3c-187">Altre informazioni sulla [serializzazione del tipo di attore](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="36d3c-187">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span>

<span data-ttu-id="36d3c-188">Vedere anche [Diagnostica e monitoraggio delle prestazioni per Reliable Actors](service-fabric-reliable-actors-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="36d3c-188">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span></span>
