---
title: aaaReentrancy in microservizi Azure basato su attori | Documenti Microsoft
description: Introduzione tooreentrancy per Service Fabric Reliable Actors
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: be23464a-0eea-4eca-ae5a-2e1b650d365e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 61c69bcf0f100e075d19ba155954c05789b71761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="2188f-103">Rientranza di Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="2188f-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="2188f-104">runtime Reliable Actors Hello, per impostazione predefinita, consente la rientranza basata sul contesto di chiamata logico.</span><span class="sxs-lookup"><span data-stu-id="2188f-104">hello Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="2188f-105">In questo modo rientrante toobe attori che si trovano nella hello stessa catena del contesto di chiamata.</span><span class="sxs-lookup"><span data-stu-id="2188f-105">This allows for actors toobe reentrant if they are in hello same call context chain.</span></span> <span data-ttu-id="2188f-106">Ad esempio, un attore invia un tooActor messaggio B, che invia un tooActor messaggio C. Come parte dell'elaborazione dei messaggi hello, se attore C chiama attore, un messaggio hello è rientrante, pertanto sarà possibile.</span><span class="sxs-lookup"><span data-stu-id="2188f-106">For example, Actor A sends a message tooActor B, who sends a message tooActor C. As part of hello message processing, if Actor C calls Actor A, hello message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="2188f-107">Tutti gli altri messaggi che fanno parte di un contesto di chiamata diverso verranno bloccati sull'attore A fino al completamento dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="2188f-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="2188f-108">Sono disponibili due opzioni per reentrancy attore definita in hello `ActorReentrancyMode` enum:</span><span class="sxs-lookup"><span data-stu-id="2188f-108">There are two options available for actor reentrancy defined in hello `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="2188f-109">`LogicalCallContext` (comportamento predefinito)</span><span class="sxs-lookup"><span data-stu-id="2188f-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="2188f-110">`Disallowed` : disabilita la reentrancy</span><span class="sxs-lookup"><span data-stu-id="2188f-110">`Disallowed` - disables reentrancy</span></span>

```csharp
public enum ActorReentrancyMode
{
    LogicalCallContext = 1,
    Disallowed = 2
}
```
```Java
public enum ActorReentrancyMode
{
    LogicalCallContext(1),
    Disallowed(2)
}
```
<span data-ttu-id="2188f-111">La reentrancy può essere configurata nelle impostazioni di `ActorService`durante la registrazione.</span><span class="sxs-lookup"><span data-stu-id="2188f-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="2188f-112">impostazione di Hello applica le istanze di attore tooall create nel servizio actor hello.</span><span class="sxs-lookup"><span data-stu-id="2188f-112">hello setting applies tooall actor instances created in hello actor service.</span></span>

<span data-ttu-id="2188f-113">Hello esempio seguente viene illustrato un servizio actor che imposta la modalità della reentrancy hello troppo`ActorReentrancyMode.Disallowed`.</span><span class="sxs-lookup"><span data-stu-id="2188f-113">hello following example shows an actor service that sets hello reentrancy mode too`ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="2188f-114">In questo caso, se un attore invia un attore tooanother messaggio rientrante, un'eccezione di tipo `FabricException` verrà generata.</span><span class="sxs-lookup"><span data-stu-id="2188f-114">In this case, if an actor sends a reentrant message tooanother actor, an exception of type `FabricException` will be thrown.</span></span>

```csharp
static class Program
{
    static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<Actor1>(
                (context, actorType) => new ActorService(
                    context,
                    actorType, () => new Actor1(),
                    settings: new ActorServiceSettings()
                    {
                        ActorConcurrencySettings = new ActorConcurrencySettings()
                        {
                            ReentrancyMode = ActorReentrancyMode.Disallowed
                        }
                    }))
                .GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}
```
```Java
static class Program
{
    static void Main()
    {
        try
        {
            ActorConcurrencySettings actorConcurrencySettings = new ActorConcurrencySettings();
            actorConcurrencySettings.setReentrancyMode(ActorReentrancyMode.Disallowed);

            ActorServiceSettings actorServiceSettings = new ActorServiceSettings();
            actorServiceSettings.setActorConcurrencySettings(actorConcurrencySettings);

            ActorRuntime.registerActorAsync(
                Actor1.getClass(),
                (context, actorType) -> new FabricActorService(
                    context,
                    actorType, () -> new Actor1(),
                    null,
                    stateProvider,
                    actorServiceSettings, timeout);

            Thread.sleep(Long.MAX_VALUE);
        }
        catch (Exception e)
        {
            throw e;
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="2188f-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2188f-115">Next steps</span></span>
* <span data-ttu-id="2188f-116">Ulteriori informazioni sulla reentrancy in hello [documentazione di riferimento API attore](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span><span class="sxs-lookup"><span data-stu-id="2188f-116">Learn more about reentrancy in hello [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
