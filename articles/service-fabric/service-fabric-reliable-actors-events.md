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
# <a name="actor-events"></a><span data-ttu-id="716d6-103">Eventi relativi agli attori</span><span class="sxs-lookup"><span data-stu-id="716d6-103">Actor events</span></span>
<span data-ttu-id="716d6-104">Gli eventi di attore forniscono notifiche sforzo toosend modo dai client di toohello hello attore.</span><span class="sxs-lookup"><span data-stu-id="716d6-104">Actor events provide a way toosend best-effort notifications from hello actor toohello clients.</span></span> <span data-ttu-id="716d6-105">Tali eventi sono stati progettati per la comunicazione tra attore e client e non è consigliabile usarli per la comunicazione tra attori.</span><span class="sxs-lookup"><span data-stu-id="716d6-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="716d6-106">Mostra frammenti di codice seguente Hello come eventi attore toouse nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="716d6-106">hello following code snippets show how toouse actor events in your application.</span></span>

<span data-ttu-id="716d6-107">Definire un'interfaccia che descrive gli eventi di hello pubblicati dall'attore hello.</span><span class="sxs-lookup"><span data-stu-id="716d6-107">Define an interface that describes hello events published by hello actor.</span></span> <span data-ttu-id="716d6-108">Questa interfaccia deve essere derivata da hello `IActorEvents` interfaccia.</span><span class="sxs-lookup"><span data-stu-id="716d6-108">This interface must be derived from hello `IActorEvents` interface.</span></span> <span data-ttu-id="716d6-109">Hello argomenti dei metodi di hello devono essere [di contratto dati serializzabile](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="716d6-109">hello arguments of hello methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="716d6-110">i metodi di Hello devono restituire void, come evento le notifiche sono un modo e senza alcuna garanzia.</span><span class="sxs-lookup"><span data-stu-id="716d6-110">hello methods must return void, as event notifications are one way and best effort.</span></span>

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
<span data-ttu-id="716d6-111">Dichiarare gli eventi di hello pubblicati dall'attore hello nell'interfaccia di hello attore.</span><span class="sxs-lookup"><span data-stu-id="716d6-111">Declare hello events published by hello actor in hello actor interface.</span></span>

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
<span data-ttu-id="716d6-112">Sul lato client hello, implementare il gestore dell'evento hello.</span><span class="sxs-lookup"><span data-stu-id="716d6-112">On hello client side, implement hello event handler.</span></span>

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

<span data-ttu-id="716d6-113">Nel client hello, creare un attore toohello proxy che pubblica evento hello e sottoscrivere gli eventi tooits.</span><span class="sxs-lookup"><span data-stu-id="716d6-113">On hello client, create a proxy toohello actor that publishes hello event and subscribe tooits events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="716d6-114">In caso di hello di failover, può failover attore hello tooa altro processo o nodo.</span><span class="sxs-lookup"><span data-stu-id="716d6-114">In hello event of failovers, hello actor may fail over tooa different process or node.</span></span> <span data-ttu-id="716d6-115">proxy attore Hello gestisce le sottoscrizioni attive hello e automaticamente di nuovo le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="716d6-115">hello actor proxy manages hello active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="716d6-116">È possibile controllare l'intervallo di nuova sottoscrizione hello tramite hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="716d6-116">You can control hello re-subscription interval through hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="716d6-117">toounsubscribe, utilizzare hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="716d6-117">toounsubscribe, use hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="716d6-118">In attore hello, è sufficiente pubblicare eventi hello in tempo reale.</span><span class="sxs-lookup"><span data-stu-id="716d6-118">On hello actor, simply publish hello events as they happen.</span></span> <span data-ttu-id="716d6-119">Se sono presenti eventi toohello sottoscrittori, hello attori runtime li invia notifica hello.</span><span class="sxs-lookup"><span data-stu-id="716d6-119">If there are subscribers toohello event, hello Actors runtime will send them hello notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="716d6-120">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="716d6-120">Next steps</span></span>
* [<span data-ttu-id="716d6-121">Rientranza di Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="716d6-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="716d6-122">Diagnostica e monitoraggio delle prestazioni per Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="716d6-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="716d6-123">Documentazione di riferimento delle API di Actors</span><span class="sxs-lookup"><span data-stu-id="716d6-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="716d6-124">Codice di esempio C#</span><span class="sxs-lookup"><span data-stu-id="716d6-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="716d6-125">Codice di esempio di base C# .NET</span><span class="sxs-lookup"><span data-stu-id="716d6-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="716d6-126">Codice di esempio Java</span><span class="sxs-lookup"><span data-stu-id="716d6-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
