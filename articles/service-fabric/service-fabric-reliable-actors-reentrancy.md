---
title: Reentrancy nei microservizi di Azure basati su attori | Documentazione Microsoft
description: Introduzione alla rientranza per Reliable Actors di Service Fabric
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
ms.openlocfilehash: 00fcccb379bf1ba3875fbaba57a05b00fa228622
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="bdf18-103">Rientranza di Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="bdf18-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="bdf18-104">Per impostazione predefinita, il runtime di Reliable Actors consente la reentrancy basata sul contesto di chiamata logico.</span><span class="sxs-lookup"><span data-stu-id="bdf18-104">The Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="bdf18-105">Ciò consente agli attori di essere rientranti se si trovano nella stessa catena del contesto di chiamata.</span><span class="sxs-lookup"><span data-stu-id="bdf18-105">This allows for actors to be reentrant if they are in the same call context chain.</span></span> <span data-ttu-id="bdf18-106">Ad esempio, l'attore A invia un messaggio all'attore B che invia un messaggio all'attore C. Durante l'elaborazione del messaggio, se l'attore C chiama l'attore A, il messaggio è rientrante e sarà quindi consentito.</span><span class="sxs-lookup"><span data-stu-id="bdf18-106">For example, Actor A sends a message to Actor B, who sends a message to Actor C. As part of the message processing, if Actor C calls Actor A, the message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="bdf18-107">Tutti gli altri messaggi che fanno parte di un contesto di chiamata diverso verranno bloccati sull'attore A fino al completamento dell'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="bdf18-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="bdf18-108">Per la reentrancy degli attori sono disponibili due opzioni, definite nell'enumerazione `ActorReentrancyMode` :</span><span class="sxs-lookup"><span data-stu-id="bdf18-108">There are two options available for actor reentrancy defined in the `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="bdf18-109">`LogicalCallContext` (comportamento predefinito)</span><span class="sxs-lookup"><span data-stu-id="bdf18-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="bdf18-110">`Disallowed` : disabilita la reentrancy</span><span class="sxs-lookup"><span data-stu-id="bdf18-110">`Disallowed` - disables reentrancy</span></span>

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
<span data-ttu-id="bdf18-111">La reentrancy può essere configurata nelle impostazioni di `ActorService`durante la registrazione.</span><span class="sxs-lookup"><span data-stu-id="bdf18-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="bdf18-112">L'impostazione si applica a tutte le istanze degli attori create nel servizio Actor.</span><span class="sxs-lookup"><span data-stu-id="bdf18-112">The setting applies to all actor instances created in the actor service.</span></span>

<span data-ttu-id="bdf18-113">L'esempio seguente illustra un servizio Actor che imposta la modalità di reentrancy su `ActorReentrancyMode.Disallowed`.</span><span class="sxs-lookup"><span data-stu-id="bdf18-113">The following example shows an actor service that sets the reentrancy mode to `ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="bdf18-114">In questo caso, se un attore invia un messaggio rientrante a un altro attore verrà generata un'eccezione di tipo `FabricException` .</span><span class="sxs-lookup"><span data-stu-id="bdf18-114">In this case, if an actor sends a reentrant message to another actor, an exception of type `FabricException` will be thrown.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="bdf18-115">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bdf18-115">Next steps</span></span>
* <span data-ttu-id="bdf18-116">Acquisire altre informazioni sulla reentrancy nella [documentazione di riferimento delle API di Actors](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span><span class="sxs-lookup"><span data-stu-id="bdf18-116">Learn more about reentrancy in the [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
