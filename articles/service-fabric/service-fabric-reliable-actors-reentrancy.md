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
# <a name="reliable-actors-reentrancy"></a>Rientranza di Reliable Actors
runtime Reliable Actors Hello, per impostazione predefinita, consente la rientranza basata sul contesto di chiamata logico. In questo modo rientrante toobe attori che si trovano nella hello stessa catena del contesto di chiamata. Ad esempio, un attore invia un tooActor messaggio B, che invia un tooActor messaggio C. Come parte dell'elaborazione dei messaggi hello, se attore C chiama attore, un messaggio hello è rientrante, pertanto sarà possibile. Tutti gli altri messaggi che fanno parte di un contesto di chiamata diverso verranno bloccati sull'attore A fino al completamento dell'elaborazione.

Sono disponibili due opzioni per reentrancy attore definita in hello `ActorReentrancyMode` enum:

* `LogicalCallContext` (comportamento predefinito)
* `Disallowed` : disabilita la reentrancy

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
La reentrancy può essere configurata nelle impostazioni di `ActorService`durante la registrazione. impostazione di Hello applica le istanze di attore tooall create nel servizio actor hello.

Hello esempio seguente viene illustrato un servizio actor che imposta la modalità della reentrancy hello troppo`ActorReentrancyMode.Disallowed`. In questo caso, se un attore invia un attore tooanother messaggio rientrante, un'eccezione di tipo `FabricException` verrà generata.

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


## <a name="next-steps"></a>Passaggi successivi
* Ulteriori informazioni sulla reentrancy in hello [documentazione di riferimento API attore](https://msdn.microsoft.com/library/azure/dn971626.aspx)
