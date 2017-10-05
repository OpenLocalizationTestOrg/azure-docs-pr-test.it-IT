---
title: Gestione dello stato di Reliable Actors | Documentazione Microsoft
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
ms.openlocfilehash: aca8cf2b94e8b746a5cac6af021c7221a29b7345
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-actors-state-management"></a><span data-ttu-id="41f68-103">Gestione dello stato di Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="41f68-103">Reliable Actors state management</span></span>
<span data-ttu-id="41f68-104">I Reliable Actors sono oggetti a thread singolo che possono incapsulare sia la logica che lo stato.</span><span class="sxs-lookup"><span data-stu-id="41f68-104">Reliable Actors are single-threaded objects that can encapsulate both logic and state.</span></span> <span data-ttu-id="41f68-105">Poiché gli attori vengono eseguiti nei servizi Reliable Services, possono mantenere lo stato in modo affidabile con gli stessi meccanismi di persistenza e replica utilizzati da Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="41f68-105">Because actors run on Reliable Services, they can maintain state reliably by using the same persistence and replication mechanisms that Reliable Services uses.</span></span> <span data-ttu-id="41f68-106">In questo modo, gli attori non perdono il proprio stato dopo gli errori, dopo la riattivazione in seguito a un'operazione di garbage collection o quando vengono spostati tra i nodi di un cluster a causa del bilanciamento delle risorse o degli aggiornamenti.</span><span class="sxs-lookup"><span data-stu-id="41f68-106">This way, actors don't lose their state after failures, upon reactivation after garbage collection, or when they are moved around between nodes in a cluster due to resource balancing or upgrades.</span></span>

## <a name="state-persistence-and-replication"></a><span data-ttu-id="41f68-107">Replica e persistenza dello stato</span><span class="sxs-lookup"><span data-stu-id="41f68-107">State persistence and replication</span></span>
<span data-ttu-id="41f68-108">Tutti i Reliable Actors vengono considerati *con stato* perché ogni istanza dell'attore è mappata a un ID univoco.</span><span class="sxs-lookup"><span data-stu-id="41f68-108">All Reliable Actors are considered *stateful* because each actor instance maps to a unique ID.</span></span> <span data-ttu-id="41f68-109">Ciò significa che le chiamate ripetute allo stesso ID attore vengono instradate alla stessa istanza dell'attore.</span><span class="sxs-lookup"><span data-stu-id="41f68-109">This means that repeated calls to the same actor ID are routed to the same actor instance.</span></span> <span data-ttu-id="41f68-110">In un sistema senza stato invece le chiamate client non vengono instradate ogni volta necessariamente allo stesso server.</span><span class="sxs-lookup"><span data-stu-id="41f68-110">In a stateless system, by contrast, client calls are not guaranteed to be routed to the same server every time.</span></span> <span data-ttu-id="41f68-111">Per questo motivo, i servizi Actor sono sempre servizi con stato.</span><span class="sxs-lookup"><span data-stu-id="41f68-111">For this reason, actor services are always stateful services.</span></span>

<span data-ttu-id="41f68-112">Anche se gli attori sono considerati con stato, non significa che devono archiviare lo stato in modo affidabile.</span><span class="sxs-lookup"><span data-stu-id="41f68-112">Even though actors are considered stateful, that does not mean they must store state reliably.</span></span> <span data-ttu-id="41f68-113">Gli attori possono scegliere il livello di replica e persistenza dello stato in base ai requisiti di archiviazione dei dati:</span><span class="sxs-lookup"><span data-stu-id="41f68-113">Actors can choose the level of state persistence and replication based on their data storage requirements:</span></span>

* <span data-ttu-id="41f68-114">**Stato persistente:** lo stato è persistente nel disco e viene replicato in almeno tre repliche.</span><span class="sxs-lookup"><span data-stu-id="41f68-114">**Persisted state**: State is persisted to disk and is replicated to 3 or more replicas.</span></span> <span data-ttu-id="41f68-115">Questa è l'opzione di archiviazione dello stato più durevole, in cui lo stato può persistere anche in caso di interruzione di un cluster completo.</span><span class="sxs-lookup"><span data-stu-id="41f68-115">This is the most durable state storage option, where state can persist through complete cluster outage.</span></span>
* <span data-ttu-id="41f68-116">**Stato volatile:** lo stato viene replicato in almeno tre repliche e viene mantenuto solo in memoria.</span><span class="sxs-lookup"><span data-stu-id="41f68-116">**Volatile state**: State is replicated to 3 or more replicas and only kept in memory.</span></span> <span data-ttu-id="41f68-117">Fornisce la resilienza in caso di errore del nodo, di errore dell'attore e durante gli aggiornamenti e il bilanciamento delle risorse.</span><span class="sxs-lookup"><span data-stu-id="41f68-117">This provides resilience against node failure and actor failure, and during upgrades and resource balancing.</span></span> <span data-ttu-id="41f68-118">Lo stato tuttavia non è persistente nel disco.</span><span class="sxs-lookup"><span data-stu-id="41f68-118">However, state is not persisted to disk.</span></span> <span data-ttu-id="41f68-119">Perciò, se vengono perse contemporaneamente tutte le repliche, si perderà anche lo stato.</span><span class="sxs-lookup"><span data-stu-id="41f68-119">So if all replicas are lost at once, the state is lost as well.</span></span>
* <span data-ttu-id="41f68-120">**Stato non persistente:** lo stato non viene replicato né viene scritto su disco.</span><span class="sxs-lookup"><span data-stu-id="41f68-120">**No persisted state**: State is not replicated or written to disk.</span></span> <span data-ttu-id="41f68-121">Questo livello è appropriato per gli attori che non devono mantenere lo stato affidabile.</span><span class="sxs-lookup"><span data-stu-id="41f68-121">This level is for actors that simply don't need to maintain state reliably.</span></span>

<span data-ttu-id="41f68-122">Ogni livello di persistenza è semplicemente un altro *provider di stato* e un'altra configurazione di *replica* del servizio.</span><span class="sxs-lookup"><span data-stu-id="41f68-122">Each level of persistence is simply a different *state provider* and *replication* configuration of your service.</span></span> <span data-ttu-id="41f68-123">La scrittura su disco dello stato dipende dal provider di stato, ovvero il componente di un servizio Reliable Services che archivia lo stato.</span><span class="sxs-lookup"><span data-stu-id="41f68-123">Whether or not state is written to disk depends on the state provider--the component in a reliable service that stores state.</span></span> <span data-ttu-id="41f68-124">La replica dipende dal numero di repliche con cui viene distribuito un servizio.</span><span class="sxs-lookup"><span data-stu-id="41f68-124">Replication depends on how many replicas a service is deployed with.</span></span> <span data-ttu-id="41f68-125">In modo analogo ai servizi Reliable Services, il provider di stato e il numero di repliche possono essere impostati manualmente con facilità.</span><span class="sxs-lookup"><span data-stu-id="41f68-125">As with Reliable Services, both the state provider and replica count can easily be set manually.</span></span> <span data-ttu-id="41f68-126">Il framework per gli attori fornisce un attributo che, quando viene usato in un attore, seleziona automaticamente un provider di stato predefinito e genera automaticamente le impostazioni per il numero di repliche in modo da ottenere una di queste tre impostazioni di persistenza.</span><span class="sxs-lookup"><span data-stu-id="41f68-126">The actor framework provides an attribute that, when used on an actor, automatically selects a default state provider and automatically generates settings for replica count to achieve one of these three persistence settings.</span></span> <span data-ttu-id="41f68-127">L'attributo StatePersistence non viene ereditato dalla classe derivata e ogni tipo di attore deve specificare il proprio livello StatePersistence.</span><span class="sxs-lookup"><span data-stu-id="41f68-127">The StatePersistence attribute is not inherited by derived class, each Actor type must provide its StatePersistence level.</span></span>

### <a name="persisted-state"></a><span data-ttu-id="41f68-128">Stato persistente</span><span class="sxs-lookup"><span data-stu-id="41f68-128">Persisted state</span></span>
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
<span data-ttu-id="41f68-129">Questa impostazione usa un provider di stato che archivia i dati su disco e imposta automaticamente il numero di repliche del servizio su 3.</span><span class="sxs-lookup"><span data-stu-id="41f68-129">This setting uses a state provider that stores data on disk and automatically sets the service replica count to 3.</span></span>

### <a name="volatile-state"></a><span data-ttu-id="41f68-130">Stato volatile</span><span class="sxs-lookup"><span data-stu-id="41f68-130">Volatile state</span></span>
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
<span data-ttu-id="41f68-131">Questa impostazione usa un provider di stato solo in memoria e imposta il numero di repliche su 3.</span><span class="sxs-lookup"><span data-stu-id="41f68-131">This setting uses an in-memory-only state provider and sets the replica count to 3.</span></span>

### <a name="no-persisted-state"></a><span data-ttu-id="41f68-132">Stato non persistente</span><span class="sxs-lookup"><span data-stu-id="41f68-132">No persisted state</span></span>
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
<span data-ttu-id="41f68-133">Questa impostazione usa un provider di stato solo in memoria e imposta il numero di repliche su 1.</span><span class="sxs-lookup"><span data-stu-id="41f68-133">This setting uses an in-memory-only state provider and sets the replica count to 1.</span></span>

### <a name="defaults-and-generated-settings"></a><span data-ttu-id="41f68-134">Impostazioni predefinite e impostazioni generate</span><span class="sxs-lookup"><span data-stu-id="41f68-134">Defaults and generated settings</span></span>
<span data-ttu-id="41f68-135">Quando si usa l'attributo `StatePersistence`, viene selezionato automaticamente un provider di stato in fase di esecuzione all'avvio del servizio attore.</span><span class="sxs-lookup"><span data-stu-id="41f68-135">When you're using the `StatePersistence` attribute, a state provider is automatically selected for you at runtime when the actor service starts.</span></span> <span data-ttu-id="41f68-136">Il numero di repliche, tuttavia, viene impostato in fase di compilazione dagli strumenti di compilazione dell'attore di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="41f68-136">The replica count, however, is set at compile time by the Visual Studio actor build tools.</span></span> <span data-ttu-id="41f68-137">Gli strumenti di compilazione generano automaticamente un *servizio predefinito* per il servizio attore in ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="41f68-137">The build tools automatically generate a *default service* for the actor service in ApplicationManifest.xml.</span></span> <span data-ttu-id="41f68-138">I parametri vengono creati per le **dimensioni minime del set di repliche** e le **dimensioni del set di repliche di destinazione**.</span><span class="sxs-lookup"><span data-stu-id="41f68-138">Parameters are created for **min replica set size** and **target replica set size**.</span></span>

<span data-ttu-id="41f68-139">È possibile cambiare questi parametri manualmente.</span><span class="sxs-lookup"><span data-stu-id="41f68-139">You can change these parameters manually.</span></span> <span data-ttu-id="41f68-140">Tuttavia, ogni volta che l'attributo `StatePersistence` viene modificato, i parametri vengono impostati sui valori predefiniti delle dimensioni del set di repliche per l'attributo `StatePersistence` selezionato, eseguendo l'override di eventuali valori precedenti.</span><span class="sxs-lookup"><span data-stu-id="41f68-140">But each time the `StatePersistence` attribute is changed, the parameters are set to the default replica set size values for the selected `StatePersistence` attribute, overriding any previous values.</span></span> <span data-ttu-id="41f68-141">In altri termini, l'override dei valori impostati in ServiceManifest.xml viene eseguito *solo* in fase di compilazione quando si modifica l'attributo `StatePersistence`.</span><span class="sxs-lookup"><span data-stu-id="41f68-141">In other words, the values that you set in ServiceManifest.xml are *only* overridden at build time when you change the `StatePersistence` attribute value.</span></span>

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

## <a name="state-manager"></a><span data-ttu-id="41f68-142">State Manager</span><span class="sxs-lookup"><span data-stu-id="41f68-142">State manager</span></span>
<span data-ttu-id="41f68-143">Ogni istanza dell'attore ha un proprio gestore di stato: una struttura di dati simile a un dizionario che archivia in modo affidabile le coppie chiave-valore.</span><span class="sxs-lookup"><span data-stu-id="41f68-143">Every actor instance has its own state manager: a dictionary-like data structure that reliably stores key/value pairs.</span></span> <span data-ttu-id="41f68-144">Il gestore di stato è un wrapper per il provider di stato.</span><span class="sxs-lookup"><span data-stu-id="41f68-144">The state manager is a wrapper around a state provider.</span></span> <span data-ttu-id="41f68-145">Può essere usato per archiviare i dati indipendentemente dall'impostazione di persistenza utilizzata.</span><span class="sxs-lookup"><span data-stu-id="41f68-145">You can use it to store data regardless of which persistence setting is used.</span></span> <span data-ttu-id="41f68-146">Non garantisce assolutamente che un servizio attore in esecuzione possa essere modificato da un'impostazione di stato volatile (solo in memoria) in un'impostazione di stato persistente tramite un aggiornamento in sequenza mantenendo al tempo stesso i dati.</span><span class="sxs-lookup"><span data-stu-id="41f68-146">It does not provide any guarantees that a running actor service can be changed from a volatile (in-memory-only) state setting to a persisted state setting through a rolling upgrade while preserving data.</span></span> <span data-ttu-id="41f68-147">Tuttavia, è possibile modificare il numero di repliche per un servizio in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="41f68-147">However, it is possible to change replica count for a running service.</span></span>

<span data-ttu-id="41f68-148">Le chiavi di gestione dello stato devono essere stringhe.</span><span class="sxs-lookup"><span data-stu-id="41f68-148">State manager keys must be strings.</span></span> <span data-ttu-id="41f68-149">I valori sono di tipo generico e possono essere di qualsiasi tipo, inclusi i tipi personalizzati.</span><span class="sxs-lookup"><span data-stu-id="41f68-149">Values are generic and can be any type, including custom types.</span></span> <span data-ttu-id="41f68-150">I valori archiviati nel gestore di stato devono essere serializzabili in base al contratto dati perché possono essere trasmessi in rete ad altri nodi durante la replica e possono essere scritti su disco, a seconda dell'impostazione di persistenza dello stato di un attore.</span><span class="sxs-lookup"><span data-stu-id="41f68-150">Values stored in the state manager must be data contract serializable because they might be transmitted over the network to other nodes during replication and might be written to disk, depending on an actor's state persistence setting.</span></span>

<span data-ttu-id="41f68-151">Il gestore di stato espone i metodi di dizionario comuni per la gestione dello stato, simili a quelli disponibili in Reliable Dictionary.</span><span class="sxs-lookup"><span data-stu-id="41f68-151">The state manager exposes common dictionary methods for managing state, similar to those found in Reliable Dictionary.</span></span>

### <a name="accessing-state"></a><span data-ttu-id="41f68-152">Accesso allo stato</span><span class="sxs-lookup"><span data-stu-id="41f68-152">Accessing state</span></span>
<span data-ttu-id="41f68-153">Lo stato è accessibile tramite il gestore di stato mediante la chiave.</span><span class="sxs-lookup"><span data-stu-id="41f68-153">State can be accessed through the state manager by key.</span></span> <span data-ttu-id="41f68-154">I metodi del gestore di stato sono tutti asincroni perché possono richiedere operazioni di I/O del disco quando gli attori hanno uno stato persistente.</span><span class="sxs-lookup"><span data-stu-id="41f68-154">State manager methods are all asynchronous because they might require disk I/O when actors have persisted state.</span></span> <span data-ttu-id="41f68-155">Al primo accesso, gli oggetti di stato vengono memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="41f68-155">Upon first access, state objects are cached in memory.</span></span> <span data-ttu-id="41f68-156">Le operazioni di accesso ripetute accedono agli oggetti direttamente dalla memoria e vengono restituite in modo sincrono senza incorrere nel sovraccarico di operazioni di I/O del disco o di cambio di contesto asincrono.</span><span class="sxs-lookup"><span data-stu-id="41f68-156">Repeat access operations access objects directly from memory and return synchronously without incurring disk I/O or asynchronous context-switching overhead.</span></span> <span data-ttu-id="41f68-157">Un oggetto di stato viene rimosso dalla cache nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="41f68-157">A state object is removed from the cache in the following cases:</span></span>

* <span data-ttu-id="41f68-158">Il metodo di un attore genera un'eccezione non gestita dopo il recupero di un oggetto dal gestore di stato.</span><span class="sxs-lookup"><span data-stu-id="41f68-158">An actor method throws an unhandled exception after it retrieves an object from the state manager.</span></span>
* <span data-ttu-id="41f68-159">Un attore viene riattivato dopo essere stato disattivato o dopo un errore.</span><span class="sxs-lookup"><span data-stu-id="41f68-159">An actor is reactivated, either after being deactivated or after failure.</span></span>
* <span data-ttu-id="41f68-160">Il provider di stato invia lo stato al disco.</span><span class="sxs-lookup"><span data-stu-id="41f68-160">The state provider pages state to disk.</span></span> <span data-ttu-id="41f68-161">Questo comportamento dipende dall'implementazione del provider di stato.</span><span class="sxs-lookup"><span data-stu-id="41f68-161">This behavior depends on the state provider implementation.</span></span> <span data-ttu-id="41f68-162">Il provider di stato predefinito per l'impostazione `Persisted` ha questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="41f68-162">The default state provider for the `Persisted` setting has this behavior.</span></span>

<span data-ttu-id="41f68-163">Lo stato può essere recuperato con un'operazione *Get* standard che genera l'eccezione `KeyNotFoundException`(C#) o `NoSuchElementException`(Java) se non esiste una voce per la chiave:</span><span class="sxs-lookup"><span data-stu-id="41f68-163">You can retrieve state by using a standard *Get* operation that throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) if an entry does not exist for the key:</span></span>

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

<span data-ttu-id="41f68-164">Lo stato può essere recuperato anche con un metodo *TryGet* che non genera alcuna eccezione se non esiste una voce per la chiave:</span><span class="sxs-lookup"><span data-stu-id="41f68-164">You can also retrieve state by using a *TryGet* method that does not throw if an entry does not exist for a key:</span></span>

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

### <a name="saving-state"></a><span data-ttu-id="41f68-165">Salvataggio dello stato</span><span class="sxs-lookup"><span data-stu-id="41f68-165">Saving state</span></span>
<span data-ttu-id="41f68-166">I metodi di recupero del gestore di stato restituiscono un riferimento a un oggetto nella memoria locale.</span><span class="sxs-lookup"><span data-stu-id="41f68-166">The state manager retrieval methods return a reference to an object in local memory.</span></span> <span data-ttu-id="41f68-167">Se questo oggetto viene modificato solo nella memoria locale non verrà salvato in modo permanente.</span><span class="sxs-lookup"><span data-stu-id="41f68-167">Modifying this object in local memory alone does not cause it to be saved durably.</span></span> <span data-ttu-id="41f68-168">Quando un oggetto viene recuperato dal gestore di stato e modificato, deve essere reinserito nel gestore di stato per essere salvato in modo permanente.</span><span class="sxs-lookup"><span data-stu-id="41f68-168">When an object is retrieved from the state manager and modified, it must be reinserted into the state manager to be saved durably.</span></span>

<span data-ttu-id="41f68-169">Lo stato può essere inserito usando un metodo *Set* non condizionale, che è l'equivalente della sintassi `dictionary["key"] = value`:</span><span class="sxs-lookup"><span data-stu-id="41f68-169">You can insert state by using an unconditional *Set*, which is the equivalent of the `dictionary["key"] = value` syntax:</span></span>

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

<span data-ttu-id="41f68-170">È possibile aggiungere lo stato tramite il metodo *Add*.</span><span class="sxs-lookup"><span data-stu-id="41f68-170">You can add state by using an *Add* method.</span></span> <span data-ttu-id="41f68-171">Questo metodo genera l'eccezione `InvalidOperationException`(C#) o `IllegalStateException`(Java) se si tenta di aggiungere una chiave già esistente.</span><span class="sxs-lookup"><span data-stu-id="41f68-171">This method throws `InvalidOperationException`(C#) or `IllegalStateException`(Java) when it tries to add a key that already exists.</span></span>

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

<span data-ttu-id="41f68-172">È possibile aggiungere lo stato anche con il metodo *TryAdd*.</span><span class="sxs-lookup"><span data-stu-id="41f68-172">You can also add state by using a *TryAdd* method.</span></span> <span data-ttu-id="41f68-173">Questo metodo non genera eccezioni se si tenta di aggiungere una chiave già esistente.</span><span class="sxs-lookup"><span data-stu-id="41f68-173">This method does not throw when it tries to add a key that already exists.</span></span>

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

<span data-ttu-id="41f68-174">Alla fine di un metodo di un attore, il gestore di stato salva automaticamente tutti i valori che sono stati aggiunti o modificati da un'operazione di inserimento o aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="41f68-174">At the end of an actor method, the state manager automatically saves any values that have been added or modified by an insert or update operation.</span></span> <span data-ttu-id="41f68-175">Un'operazione di salvataggio può includere il salvataggio su disco in modo permanente e la replica, a seconda delle impostazioni usate.</span><span class="sxs-lookup"><span data-stu-id="41f68-175">A "save" can include persisting to disk and replication, depending on the settings used.</span></span> <span data-ttu-id="41f68-176">I valori che non sono stati modificati non vengono salvati in modo permanente né replicati.</span><span class="sxs-lookup"><span data-stu-id="41f68-176">Values that have not been modified are not persisted or replicated.</span></span> <span data-ttu-id="41f68-177">Se non è stato modificato alcun valore, l'operazione di salvataggio non eseguirà alcuna azione.</span><span class="sxs-lookup"><span data-stu-id="41f68-177">If no values have been modified, the save operation does nothing.</span></span> <span data-ttu-id="41f68-178">Se il salvataggio non riesce, lo stato modificato verrà eliminato e verrà ricaricato lo stato originale.</span><span class="sxs-lookup"><span data-stu-id="41f68-178">If saving fails, the modified state is discarded and the original state is reloaded.</span></span>

<span data-ttu-id="41f68-179">Lo stato può anche essere salvato manualmente chiamando il metodo `SaveStateAsync` sulla base dell'attore:</span><span class="sxs-lookup"><span data-stu-id="41f68-179">You can also save state manually by calling the `SaveStateAsync` method on the actor base:</span></span>

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

### <a name="removing-state"></a><span data-ttu-id="41f68-180">Rimozione dello stato</span><span class="sxs-lookup"><span data-stu-id="41f68-180">Removing state</span></span>
<span data-ttu-id="41f68-181">Lo stato può essere rimosso in modo permanente dal gestore di stato di un attore chiamando il metodo *Remove*.</span><span class="sxs-lookup"><span data-stu-id="41f68-181">You can remove state permanently from an actor's state manager by calling the *Remove* method.</span></span> <span data-ttu-id="41f68-182">Questo metodo genera l'eccezione `KeyNotFoundException` (C#) o `NoSuchElementException`(Java) se si tenta di rimuovere una chiave che non esiste.</span><span class="sxs-lookup"><span data-stu-id="41f68-182">This method throws `KeyNotFoundException`(C#) or `NoSuchElementException`(Java) when it tries to remove a key that doesn't exist.</span></span>

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

<span data-ttu-id="41f68-183">È possibile rimuovere in modo permanente lo stato anche con il metodo *TryRemove*.</span><span class="sxs-lookup"><span data-stu-id="41f68-183">You can also remove state permanently by using the *TryRemove* method.</span></span> <span data-ttu-id="41f68-184">Questo metodo non genera eccezioni se si tenta di rimuovere una chiave che non esiste.</span><span class="sxs-lookup"><span data-stu-id="41f68-184">This method does not throw when it tries to remove a key that does not exist.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="41f68-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="41f68-185">Next steps</span></span>

<span data-ttu-id="41f68-186">Lo stato archiviato in Reliable Actors deve essere serializzato prima di essere scritto sul disco e replicato per la disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="41f68-186">State that's stored in Reliable Actors must be serialized before its written to disk and replicated for high availability.</span></span> <span data-ttu-id="41f68-187">Altre informazioni sulla [serializzazione del tipo di attore](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="41f68-187">Learn more about [Actor type serialization](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span>

<span data-ttu-id="41f68-188">Vedere anche [Diagnostica e monitoraggio delle prestazioni per Reliable Actors](service-fabric-reliable-actors-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="41f68-188">Next, learn more about [Actor diagnostics and performance monitoring](service-fabric-reliable-actors-diagnostics.md).</span></span>
