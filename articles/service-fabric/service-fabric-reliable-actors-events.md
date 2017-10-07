---
title: aaaEvents in microservizi Azure basato su attori | Documenti Microsoft
description: Introduzione tooevents per attori affidabile di servizio dell'infrastruttura.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: aa01b0f7-8f88-403a-bfe1-5aba00312c24
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: a51e41c35441a5fea508138968b36a35f0ba6699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="actor-events"></a>Eventi relativi agli attori
Gli eventi di attore forniscono notifiche sforzo toosend modo dai client di toohello hello attore. Tali eventi sono stati progettati per la comunicazione tra attore e client e non è consigliabile usarli per la comunicazione tra attori.

Mostra frammenti di codice seguente Hello come eventi attore toouse nell'applicazione.

Definire un'interfaccia che descrive gli eventi di hello pubblicati dall'attore hello. Questa interfaccia deve essere derivata da hello `IActorEvents` interfaccia. Hello argomenti dei metodi di hello devono essere [di contratto dati serializzabile](service-fabric-reliable-actors-notes-on-actor-type-serialization.md). i metodi di Hello devono restituire void, come evento le notifiche sono un modo e senza alcuna garanzia.

```csharp
public interface IGameEvents : IActorEvents
{
    void GameScoreUpdated(Guid gameId, string currentScore);
}
```
```Java
public interface GameEvents implements ActorEvents
{
    void gameScoreUpdated(UUID gameId, String currentScore);
}
```
Dichiarare gli eventi di hello pubblicati dall'attore hello nell'interfaccia di hello attore.

```csharp
public interface IGameActor : IActor, IActorEventPublisher<IGameEvents>
{
    Task UpdateGameStatus(GameStatus status);

    Task<string> GetGameScore();
}
```
```Java
public interface GameActor extends Actor, ActorEventPublisherE<GameEvents>
{
    CompletableFuture<?> updateGameStatus(GameStatus status);

    CompletableFuture<String> getGameScore();
}
```
Sul lato client hello, implementare il gestore dell'evento hello.

```csharp
class GameEventsHandler : IGameEvents
{
    public void GameScoreUpdated(Guid gameId, string currentScore)
    {
        Console.WriteLine(@"Updates: Game: {0}, Score: {1}", gameId, currentScore);
    }
}
```

```Java
class GameEventsHandler implements GameEvents {
    public void gameScoreUpdated(UUID gameId, String currentScore)
    {
        System.out.println("Updates: Game: "+gameId+" ,Score: "+currentScore);
    }
}
```

Nel client hello, creare un attore toohello proxy che pubblica evento hello e sottoscrivere gli eventi tooits.

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

In caso di hello di failover, può failover attore hello tooa altro processo o nodo. proxy attore Hello gestisce le sottoscrizioni attive hello e automaticamente di nuovo le sottoscrizioni. È possibile controllare l'intervallo di nuova sottoscrizione hello tramite hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API. toounsubscribe, utilizzare hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.

In attore hello, è sufficiente pubblicare eventi hello in tempo reale. Se sono presenti eventi toohello sottoscrittori, hello attori runtime li invia notifica hello.

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a>Passaggi successivi
* [Rientranza di Reliable Actors](service-fabric-reliable-actors-reentrancy.md)
* [Diagnostica e monitoraggio delle prestazioni per Reliable Actors](service-fabric-reliable-actors-diagnostics.md)
* [Documentazione di riferimento delle API di Actors](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Codice di esempio C#](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Codice di esempio di base C# .NET](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [Codice di esempio Java](http://github.com/Azure-Samples/service-fabric-java-getting-started)
