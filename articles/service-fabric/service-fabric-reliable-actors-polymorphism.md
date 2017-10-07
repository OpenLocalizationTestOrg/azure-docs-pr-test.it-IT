---
title: in framework Reliable Actors hello aaaPolymorphism | Documenti Microsoft
description: "Compilare le gerarchie di interfacce .NET e tipi di funzionalità di tooreuse framework Reliable Actors hello e le definizioni delle API."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: vturecek
ms.assetid: ef0eeff6-32b7-410d-ac69-87cba8b8fd46
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ed9ec442595bd9a5e48c9af1f6aac003439b81f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="polymorphism-in-hello-reliable-actors-framework"></a>Polimorfismo framework Reliable Actors hello
Hello Reliable Actors framework consente agli attori toobuild utilizzando molte delle hello stesse tecniche utilizzate in progettazione orientata agli oggetti. Una di queste tecniche è il polimorfismo, che consente ai tipi e interfacce tooinherit da più generalizzato di elementi padre. Ereditarietà in framework Reliable Actors hello in genere segue il modello .NET hello con alcuni vincoli aggiuntivi. In caso di Java/Linux, segue il modello di linguaggio hello.

## <a name="interfaces"></a>Interfacce
framework Reliable Actors Hello richiede toodefine toobe almeno un'interfaccia implementata dal tipo attore. Questa interfaccia è toogenerate utilizzata una classe proxy che può essere utilizzata da client toocommunicate con gli attori. Le interfacce possono ereditare da altre interfacce, purché ogni interfaccia implementata da un tipo di attore e tutte le relative entità principali derivino da IActor (C#) o da Actor (Java). IActor(C#) e Actor(Java) sono rispettivamente hello definita dalla piattaforma interfacce di base per gli attori nel Framework di hello .NET e Java. Di conseguenza, potrebbe essere simile al seguente esempio classico polimorfismo hello utilizzando forme:

![Gerarchia delle interfacce per gli attori della forma][shapes-interface-hierarchy]

## <a name="types"></a>Tipi
È anche possibile creare una gerarchia di tipi attore, che derivano dalla classe attore base hello fornita dalla piattaforma hello. In caso di hello delle forme, si potrebbe disporre di una base `Shape`(c#) o `ShapeImpl`tipo (linguaggio):

```csharp
public abstract class Shape : Actor, IShape
{
    public abstract Task<int> GetVerticeCount();

    public abstract Task<double> GetAreaAsync();
}
```
```Java
public abstract class ShapeImpl extends FabricActor implements Shape
{
    public abstract CompletableFuture<int> getVerticeCount();

    public abstract CompletableFuture<double> getAreaAsync();
}
```

Sottotipi di `Shape`(c#) o `ShapeImpl`(linguaggio) può eseguire l'override della base hello.

```csharp
[ActorService(Name = "Circle")]
[StatePersistence(StatePersistence.Persisted)]
public class Circle : Shape, ICircle
{
    public override Task<int> GetVerticeCount()
    {
        return Task.FromResult(0);
    }

    public override async Task<double> GetAreaAsync()
    {
        CircleState state = await this.StateManager.GetStateAsync<CircleState>("circle");

        return Math.PI *
            state.Radius *
            state.Radius;
    }
}
```
```Java
@ActorServiceAttribute(name = "Circle")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class Circle extends ShapeImpl implements Circle
{
    @Override
    public CompletableFuture<Integer> getVerticeCount()
    {
        return CompletableFuture.completedFuture(0);
    }

    @Override
    public CompletableFuture<Double> getAreaAsync()
    {
        return (this.stateManager().getStateAsync<CircleState>("circle").thenApply(state->{
          return Math.PI * state.radius * state.radius;
        }));
    }
}
```

Hello nota `ActorService` attributo di tipo actor hello. Questo attributo indica al framework Reliable Actor hello che si desidera creare automaticamente un servizio per l'hosting di attori di questo tipo. In alcuni casi, potrebbe essere un tipo di base che è destinato esclusivamente per la condivisione di funzionalità con sottotipi toocreate e non sarà mai utilizzato tooinstantiate attori concreti. In questi casi, è necessario utilizzare hello `abstract` tooindicate parola chiave che non si può creare un attore basato su tale tipo.

## <a name="next-steps"></a>Passaggi successivi
* Vedere [come framework Reliable Actors hello sfrutta piattaforma Service Fabric hello](service-fabric-reliable-actors-platform.md) tooprovide affidabilità, scalabilità e uno stato coerente.
* Informazioni su hello [ciclo di vita dell'attore](service-fabric-reliable-actors-lifecycle.md).

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
