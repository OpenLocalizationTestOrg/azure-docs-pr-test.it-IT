---
title: Eventi nei microservizi di Azure basati su attori | Documentazione Microsoft
description: Introduzione agli eventi per Service Fabric Reliable Actors
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
ms.openlocfilehash: d936670c548ff709fc2e935d3f28d94e4bde8a04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="actor-events"></a><span data-ttu-id="b93b5-103">Eventi relativi agli attori</span><span class="sxs-lookup"><span data-stu-id="b93b5-103">Actor events</span></span>
<span data-ttu-id="b93b5-104">Gli eventi relativi agli attori consentono l'invio di notifiche il più possibile accurate dall'attore ai client.</span><span class="sxs-lookup"><span data-stu-id="b93b5-104">Actor events provide a way to send best-effort notifications from the actor to the clients.</span></span> <span data-ttu-id="b93b5-105">Tali eventi sono stati progettati per la comunicazione tra attore e client e non è consigliabile usarli per la comunicazione tra attori.</span><span class="sxs-lookup"><span data-stu-id="b93b5-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="b93b5-106">I frammenti di codice seguenti mostrano come usare eventi relativi agli attori nella propria applicazione.</span><span class="sxs-lookup"><span data-stu-id="b93b5-106">The following code snippets show how to use actor events in your application.</span></span>

<span data-ttu-id="b93b5-107">Definire un'interfaccia che descriva gli eventi pubblicati dall'attore.</span><span class="sxs-lookup"><span data-stu-id="b93b5-107">Define an interface that describes the events published by the actor.</span></span> <span data-ttu-id="b93b5-108">Tale interfaccia deve derivare dall'interfaccia `IActorEvents` .</span><span class="sxs-lookup"><span data-stu-id="b93b5-108">This interface must be derived from the `IActorEvents` interface.</span></span> <span data-ttu-id="b93b5-109">Gli argomenti dei metodi devono essere [serializzabili in base al contratto dati](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="b93b5-109">The arguments of the methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="b93b5-110">I metodi devono restituire void, in quanto le notifiche degli eventi sono unidirezionali e sono il più accurate possibile.</span><span class="sxs-lookup"><span data-stu-id="b93b5-110">The methods must return void, as event notifications are one way and best effort.</span></span>

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
<span data-ttu-id="b93b5-111">Dichiarare gli eventi pubblicati dall'attore nella relativa interfaccia.</span><span class="sxs-lookup"><span data-stu-id="b93b5-111">Declare the events published by the actor in the actor interface.</span></span>

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
<span data-ttu-id="b93b5-112">Sul lato client implementare il gestore eventi.</span><span class="sxs-lookup"><span data-stu-id="b93b5-112">On the client side, implement the event handler.</span></span>

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

<span data-ttu-id="b93b5-113">Sul client creare il proxy per l'attore che pubblica l'evento e sottoscrivere gli eventi.</span><span class="sxs-lookup"><span data-stu-id="b93b5-113">On the client, create a proxy to the actor that publishes the event and subscribe to its events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="b93b5-114">In caso di failover, l'attore può eseguire il failover su un processo o un nodo diverso.</span><span class="sxs-lookup"><span data-stu-id="b93b5-114">In the event of failovers, the actor may fail over to a different process or node.</span></span> <span data-ttu-id="b93b5-115">Il proxy dell'attore gestisce le sottoscrizioni attive e le rieffettua in modo automatico.</span><span class="sxs-lookup"><span data-stu-id="b93b5-115">The actor proxy manages the active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="b93b5-116">È possibile controllare l'intervallo di risottoscrizione tramite l'API `ActorProxyEventExtensions.SubscribeAsync<TEvent>` .</span><span class="sxs-lookup"><span data-stu-id="b93b5-116">You can control the re-subscription interval through the `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="b93b5-117">Per annullare la sottoscrizione usare l' `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="b93b5-117">To unsubscribe, use the `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="b93b5-118">Nell'attore pubblicare semplicemente gli eventi man mano che si verificano.</span><span class="sxs-lookup"><span data-stu-id="b93b5-118">On the actor, simply publish the events as they happen.</span></span> <span data-ttu-id="b93b5-119">Se vi sono sottoscrittori dell'evento, il runtime di Actors invierà loro la notifica.</span><span class="sxs-lookup"><span data-stu-id="b93b5-119">If there are subscribers to the event, the Actors runtime will send them the notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="b93b5-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b93b5-120">Next steps</span></span>
* [<span data-ttu-id="b93b5-121">Rientranza di Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="b93b5-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="b93b5-122">Diagnostica e monitoraggio delle prestazioni per Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="b93b5-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="b93b5-123">Documentazione di riferimento delle API di Actors</span><span class="sxs-lookup"><span data-stu-id="b93b5-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="b93b5-124">Codice di esempio C#</span><span class="sxs-lookup"><span data-stu-id="b93b5-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="b93b5-125">Codice di esempio di base C# .NET</span><span class="sxs-lookup"><span data-stu-id="b93b5-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="b93b5-126">Codice di esempio Java</span><span class="sxs-lookup"><span data-stu-id="b93b5-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
