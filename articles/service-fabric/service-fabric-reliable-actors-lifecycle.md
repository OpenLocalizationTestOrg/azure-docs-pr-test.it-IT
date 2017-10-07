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
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a>Ciclo di vita degli attori, Garbage Collection automatica ed eliminazione manuale
Viene attivato un attore hello prima volta che è una chiamata tooany dei relativi metodi. Un attore è disattivata (sottoposti a garbage collection dal runtime di attori hello) se non viene usato per un periodo di tempo configurabile. Un attore e il relativo stato possono essere eliminati manualmente in qualsiasi momento.

## <a name="actor-activation"></a>Attivazione di un attore
Quando viene attivato un attore, si verifica hello segue:

* Quando viene effettuata una chiamata per un attore che non è ancora attivo, viene creato un nuovo attore.
* Se mantiene lo stato, dello stato dell'actor Hello viene caricato.
* Hello `OnActivateAsync` (c#) o `onActivateAsync` (linguaggio) (che può essere sottoposto a override in una implementazione attore hello) viene chiamato.
* attore Hello a questo punto viene considerato attivo.

## <a name="actor-deactivation"></a>Disattivazione di un attore
Quando un attore è disattivato, si verifica hello segue:

* Quando un attore non viene utilizzato per un certo periodo di tempo, viene rimosso dalla tabella attori hello.
* Hello `OnDeactivateAsync` (c#) o `onDeactivateAsync` (linguaggio) (che può essere sottoposto a override in una implementazione attore hello) viene chiamato. Consente di cancellare tutti i timer hello per attore hello. Le operazioni dell'attore come le modifiche di stato non devono essere chiamate da questo metodo.

> [!TIP]
> Hello attori dell'infrastruttura runtime genera alcuni [gli eventi correlati tooactor attivazione e disattivazione](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters). che sono utili per la diagnostica e il monitoraggio delle prestazioni.
>
>

### <a name="actor-garbage-collection"></a>Garbage Collection degli attori
Quando un attore è disattivato, vengono rilasciati oggetto attore toohello di riferimenti e può essere sottoposto a garbage collection in genere da hello common language runtime (CLR) o il garbage collector di java virtual machine (JVM). Operazione di Garbage collection pulizia solo oggetto attore hello. caso **non** rimuovere stato archiviato in gestore degli Stati dell'attore hello. Hello successiva ora hello actor viene attivato, viene creato un nuovo oggetto attore e viene ripristinato lo stato.

Ciò che conta come "in uso" scopo hello di garbage collection e la disattivazione?

* Ricezione di una chiamata
* `IRemindable.ReceiveReminderAsync`metodo richiamato (applicabile solo se attore hello utilizza promemoria)

> [!NOTE]
> Se l'attore hello Usa timer e viene richiamato il callback del timer, non **non** vengono considerate come "in uso".
>
>

Prima di esplorare in dettaglio hello di disattivazione, è importante toodefine hello seguenti termini:

* *Intervallo di analisi*. Questo è l'intervallo di hello in cui hello attori runtime cerca la tabella di attori attori che possono essere disattivati e raccolti nel Garbage Collector. il valore predefinito Hello per è 1 minuto.
* *Timeout di inattività*. Si tratta hello quantità di tempo che un attore è tenuto tooremain inutilizzati (inattivo) prima che può essere disattivata e raccolti nel Garbage Collector. il valore predefinito Hello per è 60 minuti.

In genere, non è necessario toochange queste impostazioni predefinite. Se necessario, però, questi intervalli possono essere modificati tramite `ActorServiceSettings` durante la registrazione del [servizio Actor](service-fabric-reliable-actors-platform.md):

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
Per ogni attore active, hello attore runtime tiene traccia di hello periodo di tempo che è stata inattiva (ossia, non utilizzato). Hello attore runtime controlla ogni degli attori hello ogni `ScanIntervalInSeconds` toosee se garbage possono essere raccolti e raccoglie se è rimasto inattivo per `IdleTimeoutInSeconds`.

Ogni volta che viene utilizzato un attore, il tempo di inattività è too0 di reimpostazione. Successivamente, attore hello può essere sottoposto a garbage collection solo se nuovamente rimane inattivo per `IdleTimeoutInSeconds`. Tenere presente che un attore è considerato toohave stato utilizzato se viene eseguito un metodo di interfaccia attore o un callback di promemoria attore. Un attore fa **non** considerati toohave stato utilizzato se il callback del timer viene eseguito.

Hello diagramma seguente mostra hello ciclo di vita di un tooillustrate singolo attore questi concetti.

![Esempio del tempo di inattività][1]

esempio Hello Mostra impatto hello delle chiamate al metodo attore promemoria e timer durata hello dell'attore. Hello seguenti punti sull'esempio hello è utile citare:

* ScanInterval e IdleTimeout vengono impostati too5 e 10. (Unità non è rilevante in questo caso, poiché il nostro obiettivo è solo il concetto di hello tooillustrate.)
* analisi di Hello per attori toobe sottoposto a garbage collection avviene a T = 0, 5, 10, 15, 20, 25, come definito da intervallo di analisi hello pari a 5.
* Viene attivato un timer periodico in T=4,8,12,16,20,24 e ne viene eseguito il callback. Tempo di inattività hello dell'attore hello non influire.
* Una chiamata al metodo attore T = 7 Reimposta too0 tempo di inattività hello e ritardi hello operazione di garbage collection attore hello.
* Esegue un callback di promemoria attore in T = 14 e ulteriori ritardi hello attore hello operazione di garbage collection.
* Durante la hello analisi di garbage collection T = 25, tempo di inattività dell'attore hello supera infine hello timeout di inattività di 10 e attore hello è sottoposto a garbage collection.

Un attore non viene mai sottoposto a Garbage Collection mentre è in esecuzione uno dei relativi metodi, indipendentemente dal tempo impiegato per l'esecuzione di tale metodo. Come accennato in precedenza, esecuzione hello di metodi di interfaccia attore e i callback di promemoria impedisce operazioni di garbage collection reimpostando too0 tempo di inattività dell'attore hello. esecuzione di Hello di callback del timer non reimposta too0 tempo di inattività hello. Tuttavia, hello operazione di garbage collection attore hello viene posticipata finché non callback del timer hello ha completato l'esecuzione.

## <a name="deleting-actors-and-their-state"></a>Eliminazione di attori e del relativo stato
Operazione di Garbage collection di attori disattivati la pulizia solo oggetto attore hello, ma non rimuove i dati archiviati nella console di gestione dello stato dell'attore. Quando un attore viene nuovamente attivato, i dati diventa nuovamente disponibile tooit tramite hello gestore degli stati. Nei casi in attori archiviare i dati nella console di gestione dello stato e sono disattivati ma mai nuovamente attivati, potrebbe essere necessario tooclean dei propri dati.

Hello [servizio Actor](service-fabric-reliable-actors-platform.md) fornisce una funzione per l'eliminazione di attori da un chiamante remoto:

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

L'eliminazione di un attore è hello seguenti effetti a seconda che sia o meno attore hello attivo:

* **Attore attivo**
  * L'attore viene rimosso dall'elenco di attori attivi e viene disattivato.
  * Il suo stato viene eliminato definitivamente.
* **Attore inattivo**
  * Il suo stato viene eliminato definitivamente.

Si noti che non è possibile chiamare un attore eliminare su se stesso da uno dei relativi metodi attore perché attore hello non può essere eliminato durante l'esecuzione all'interno di un contesto di chiamata attore, in cui hello runtime ha ottenuto un blocco per hello attore chiamata tooenforce accesso a thread singolo.

## <a name="next-steps"></a>Passaggi successivi
* [Timer e promemoria degli attori](service-fabric-reliable-actors-timers-reminders.md)
* [Eventi relativi agli attori](service-fabric-reliable-actors-events.md)
* [Rientranza di Reliable Actors](service-fabric-reliable-actors-reentrancy.md)
* [Diagnostica e monitoraggio delle prestazioni per Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
* [Documentazione di riferimento delle API di Actors](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Codice di esempio C#](https://github.com/Azure/servicefabric-samples)
* [Codice di esempio Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
