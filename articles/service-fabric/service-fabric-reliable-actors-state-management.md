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
# <a name="reliable-actors-state-management"></a>Gestione dello stato di Reliable Actors
I Reliable Actors sono oggetti a thread singolo che possono incapsulare sia la logica che lo stato. Poiché gli operatori eseguiti in servizi affidabili, possono mantenere in modo affidabile stato utilizzando hello stessi meccanismi di persistenza e la replica che utilizza servizi affidabili. In questo modo, gli attori non perdano il proprio stato dopo errori, alla riattivazione dopo l'operazione di garbage collection o quando vengono spostati tra i nodi in un cluster a causa di bilanciamento del carico tooresource o aggiornamenti.

## <a name="state-persistence-and-replication"></a>Replica e persistenza dello stato
Vengono considerati tutti gli attori affidabile *stateful* perché l'ID univoco. tooa esegue il mapping di ogni istanza attore Ciò significa che toohello chiamate ripetute lo stesso ID attore vengono instradati toohello stessa istanza dell'attore. In un sistema senza stato, al contrario, il client chiama non è garantito toobe indirizzato toohello nello stesso server ogni volta. Per questo motivo, i servizi Actor sono sempre servizi con stato.

Anche se gli attori sono considerati con stato, non significa che devono archiviare lo stato in modo affidabile. Gli attori possono scegliere il livello di hello di persistenza dello stato e la replica in base ai propri dati i requisiti di archiviazione:

* **Uno stato persistente**: lo stato è toodisk persistente e viene replicata too3 o più repliche. Si tratta di opzione di archiviazione dello stato più durevole hello, in cui lo stato può rendere persistente tramite interruzione completa del cluster.
* **Stato volatile**: stato non è replicato too3 o più repliche e mantenuto solo in memoria. Fornisce la resilienza in caso di errore del nodo, di errore dell'attore e durante gli aggiornamenti e il bilanciamento delle risorse. Tuttavia, lo stato non è persistente toodisk. Se in una sola volta, vengono perse tutte le repliche, lo stato di hello è perso anche.
* **Nessuno stato persistente**: stato non replicato o scritto toodisk. Questo livello è per attori che non sufficiente stato toomaintain in modo affidabile.

Ogni livello di persistenza è semplicemente un altro *provider di stato* e un'altra configurazione di *replica* del servizio. Stato viene scritto o meno toodisk dipende dal provider di stato hello - componente hello in un servizio affidabile che archivia lo stato. La replica dipende dal numero di repliche con cui viene distribuito un servizio. Come per i servizi affidabili, entrambi hello provider di stato e numero di repliche può essere facilmente impostato manualmente. framework attore Hello fornisce un attributo che, quando viene utilizzata su un attore, seleziona automaticamente un provider di stato predefinito e genera automaticamente le impostazioni per la replica conteggio tooachieve una di queste tre impostazioni di persistenza. attributo StatePersistence Hello non viene ereditato dalla classe derivata, ogni tipo di attore deve fornire il proprio livello StatePersistence.

### <a name="persisted-state"></a>Stato persistente
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
Questa impostazione utilizza un provider di stato che archivia i dati su disco e di imposta automaticamente hello servizio replica conteggio too3.

### <a name="volatile-state"></a>Stato volatile
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
Questa impostazione viene utilizzato un provider di stato in memoria-solo e set hello too3 conteggio di replica.

### <a name="no-persisted-state"></a>Stato non persistente
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
Questa impostazione viene utilizzato un provider di stato in memoria-solo e set hello too1 conteggio di replica.

### <a name="defaults-and-generated-settings"></a>Impostazioni predefinite e impostazioni generate
Quando si utilizza hello `StatePersistence` attributo, un provider di stato viene selezionato automaticamente in fase di esecuzione all'avvio del servizio actor hello. numero di repliche Hello, tuttavia, è impostata in fase di compilazione da hello attore di Visual Studio gli strumenti di compilazione. Hello strumenti di compilazione di generano automaticamente un *servizio predefinito* per servizio actor hello in ApplicationManifest.xml. I parametri vengono creati per le **dimensioni minime del set di repliche** e le **dimensioni del set di repliche di destinazione**.

È possibile cambiare questi parametri manualmente. Ma ogni hello ora `StatePersistence` attributo viene modificato, i parametri di hello vengono impostati toohello replica set di dimensioni predefinite per hello selezionato `StatePersistence` attributo, si esegue l'override di eventuali valori precedenti. In altre parole, i valori hello impostati in ServiceManifest.xml sono *solo* sottoposto a override in fase di compilazione quando si modifica hello `StatePersistence` valore dell'attributo.

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

## <a name="state-manager"></a>State Manager
Ogni istanza dell'attore ha un proprio gestore di stato: una struttura di dati simile a un dizionario che archivia in modo affidabile le coppie chiave-valore. gestore degli stati Hello è un wrapper per un provider di stato. È possibile utilizzarlo toostore dati indipendentemente dall'impostazione della persistenza viene utilizzato. Non fornisce alcuna garanzia che un servizio actor in esecuzione può essere modificato da un tooa impostazione allo stato volatile (in memoria-solo) persistente impostazione dello stato tramite un aggiornamento in sequenza, mantenendo i dati. Tuttavia, è il numero di repliche toochange possibili per un servizio in esecuzione.

Le chiavi di gestione dello stato devono essere stringhe. I valori sono di tipo generico e possono essere di qualsiasi tipo, inclusi i tipi personalizzati. I valori archiviati nella console di gestione stato hello devono essere il contratto dati serializzabile perché potrebbe essere trasmesso su nodi tooother hello durante la replica e potrebbero essere scritti toodisk, a seconda delle impostazioni di persistenza dello stato di un attore.

gestore degli stati Hello espone i metodi di dizionario comuni per la gestione dello stato, simile toothose trovato nel dizionario affidabile.

### <a name="accessing-state"></a>Accesso allo stato
Stato sono accessibili tramite il gestore dello stato di hello dalla chiave. I metodi del gestore di stato sono tutti asincroni perché possono richiedere operazioni di I/O del disco quando gli attori hanno uno stato persistente. Al primo accesso, gli oggetti di stato vengono memorizzati nella cache. Le operazioni di accesso ripetute accedono agli oggetti direttamente dalla memoria e vengono restituite in modo sincrono senza incorrere nel sovraccarico di operazioni di I/O del disco o di cambio di contesto asincrono. Un oggetto di stato viene rimosso dalla cache di hello in hello seguenti casi:

* Un metodo attore genera un'eccezione non gestita dopo un oggetto viene recuperato da Gestione stato hello.
* Un attore viene riattivato dopo essere stato disattivato o dopo un errore.
* pagine del provider di stato Hello stato toodisk. Questo comportamento dipende dall'implementazione del provider di stato hello. provider di stato predefinito di Hello per hello `Persisted` impostazione ha questo comportamento.

È possibile recuperare lo stato tramite una normale *ottenere* operazione che genera `KeyNotFoundException`(c#) o `NoSuchElementException`(linguaggio), se non esiste una voce per la chiave di hello:

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

Lo stato può essere recuperato anche con un metodo *TryGet* che non genera alcuna eccezione se non esiste una voce per la chiave:

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

### <a name="saving-state"></a>Salvataggio dello stato
metodi di recupero di Hello stato manager restituire un oggetto tooan di riferimento nella memoria locale. Modifica di questo oggetto nella memoria locale da solo non provoca la toobe salvati in modo durevole. Quando un oggetto viene recuperato da Gestione stato hello e modificato, è necessario reinserito hello stato manager toobe salvati in modo durevole.

È possibile inserire lo stato tramite un non condizionale *impostare*, che è hello equivalente di hello `dictionary["key"] = value` sintassi:

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

È possibile aggiungere lo stato tramite il metodo *Add*. Questo metodo genera `InvalidOperationException`(c#) o `IllegalStateException`(linguaggio) durante il tentativo di tooadd una chiave già esistente.

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

È possibile aggiungere lo stato anche con il metodo *TryAdd*. Questo metodo non genera durante il tentativo di tooadd una chiave già esistente.

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

Alla fine di hello di un metodo attore, gestore degli stati hello Salva automaticamente tutti i valori che sono stati aggiunti o modificati da un'operazione insert o update. "Salva" può includere toodisk mantenimento e la replica, a seconda delle impostazioni di hello utilizzato. I valori che non sono stati modificati non vengono salvati in modo permanente né replicati. Se i valori non sono stati modificati, hello operazione di salvataggio non esegue alcuna operazione. Se il salvataggio ha esito negativo, hello stato modificato viene rimosso e lo stato originale di hello viene ricaricato.

È inoltre possibile salvare manualmente lo stato dal chiamante hello `SaveStateAsync` metodo attore hello base:

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

### <a name="removing-state"></a>Rimozione dello stato
È possibile rimuovere lo stato in modo permanente dal gestore degli Stati dell'attore hello chiamante *rimuovere* metodo. Questo metodo genera `KeyNotFoundException`(c#) o `NoSuchElementException`(linguaggio) durante il tentativo di tooremove una chiave che non esiste.

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

È inoltre possibile rimuovere in modo permanente lo stato tramite hello *TryRemove* metodo. Questo metodo non genera durante il tentativo di tooremove una chiave che non esiste.

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

## <a name="next-steps"></a>Passaggi successivi

Stato che viene archiviato in Reliable Actors deve essere serializzato prima relativo toodisk scritta e replicato per la disponibilità elevata. Altre informazioni sulla [serializzazione del tipo di attore](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).

Vedere anche [Diagnostica e monitoraggio delle prestazioni per Reliable Actors](service-fabric-reliable-actors-diagnostics.md).
