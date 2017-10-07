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
# <a name="polymorphism-in-hello-reliable-actors-framework"></a><span data-ttu-id="cfd13-103">Polimorfismo framework Reliable Actors hello</span><span class="sxs-lookup"><span data-stu-id="cfd13-103">Polymorphism in hello Reliable Actors framework</span></span>
<span data-ttu-id="cfd13-104">Hello Reliable Actors framework consente agli attori toobuild utilizzando molte delle hello stesse tecniche utilizzate in progettazione orientata agli oggetti.</span><span class="sxs-lookup"><span data-stu-id="cfd13-104">hello Reliable Actors framework allows you toobuild actors using many of hello same techniques that you would use in object-oriented design.</span></span> <span data-ttu-id="cfd13-105">Una di queste tecniche è il polimorfismo, che consente ai tipi e interfacce tooinherit da più generalizzato di elementi padre.</span><span class="sxs-lookup"><span data-stu-id="cfd13-105">One of those techniques is polymorphism, which allows types and interfaces tooinherit from more generalized parents.</span></span> <span data-ttu-id="cfd13-106">Ereditarietà in framework Reliable Actors hello in genere segue il modello .NET hello con alcuni vincoli aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="cfd13-106">Inheritance in hello Reliable Actors framework generally follows hello .NET model with a few additional constraints.</span></span> <span data-ttu-id="cfd13-107">In caso di Java/Linux, segue il modello di linguaggio hello.</span><span class="sxs-lookup"><span data-stu-id="cfd13-107">In case of Java/Linux, it follows hello Java model.</span></span>

## <a name="interfaces"></a><span data-ttu-id="cfd13-108">Interfacce</span><span class="sxs-lookup"><span data-stu-id="cfd13-108">Interfaces</span></span>
<span data-ttu-id="cfd13-109">framework Reliable Actors Hello richiede toodefine toobe almeno un'interfaccia implementata dal tipo attore.</span><span class="sxs-lookup"><span data-stu-id="cfd13-109">hello Reliable Actors framework requires you toodefine at least one interface toobe implemented by your actor type.</span></span> <span data-ttu-id="cfd13-110">Questa interfaccia è toogenerate utilizzata una classe proxy che può essere utilizzata da client toocommunicate con gli attori.</span><span class="sxs-lookup"><span data-stu-id="cfd13-110">This interface is used toogenerate a proxy class that can be used by clients toocommunicate with your actors.</span></span> <span data-ttu-id="cfd13-111">Le interfacce possono ereditare da altre interfacce, purché ogni interfaccia implementata da un tipo di attore e tutte le relative entità principali derivino da IActor (C#) o da Actor (Java).</span><span class="sxs-lookup"><span data-stu-id="cfd13-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span></span> <span data-ttu-id="cfd13-112">IActor(C#) e Actor(Java) sono rispettivamente hello definita dalla piattaforma interfacce di base per gli attori nel Framework di hello .NET e Java.</span><span class="sxs-lookup"><span data-stu-id="cfd13-112">IActor(C#) and Actor(Java) are hello platform-defined base interfaces for actors in hello frameworks .NET and Java respectively.</span></span> <span data-ttu-id="cfd13-113">Di conseguenza, potrebbe essere simile al seguente esempio classico polimorfismo hello utilizzando forme:</span><span class="sxs-lookup"><span data-stu-id="cfd13-113">Thus, hello classic polymorphism example using shapes might look something like this:</span></span>

![Gerarchia delle interfacce per gli attori della forma][shapes-interface-hierarchy]

## <a name="types"></a><span data-ttu-id="cfd13-115">Tipi</span><span class="sxs-lookup"><span data-stu-id="cfd13-115">Types</span></span>
<span data-ttu-id="cfd13-116">È anche possibile creare una gerarchia di tipi attore, che derivano dalla classe attore base hello fornita dalla piattaforma hello.</span><span class="sxs-lookup"><span data-stu-id="cfd13-116">You can also create a hierarchy of actor types, which are derived from hello base Actor class that is provided by hello platform.</span></span> <span data-ttu-id="cfd13-117">In caso di hello delle forme, si potrebbe disporre di una base `Shape`(c#) o `ShapeImpl`tipo (linguaggio):</span><span class="sxs-lookup"><span data-stu-id="cfd13-117">In hello case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span></span>

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

<span data-ttu-id="cfd13-118">Sottotipi di `Shape`(c#) o `ShapeImpl`(linguaggio) può eseguire l'override della base hello.</span><span class="sxs-lookup"><span data-stu-id="cfd13-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from hello base.</span></span>

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

<span data-ttu-id="cfd13-119">Hello nota `ActorService` attributo di tipo actor hello.</span><span class="sxs-lookup"><span data-stu-id="cfd13-119">Note hello `ActorService` attribute on hello actor type.</span></span> <span data-ttu-id="cfd13-120">Questo attributo indica al framework Reliable Actor hello che si desidera creare automaticamente un servizio per l'hosting di attori di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="cfd13-120">This attribute tells hello Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span></span> <span data-ttu-id="cfd13-121">In alcuni casi, potrebbe essere un tipo di base che è destinato esclusivamente per la condivisione di funzionalità con sottotipi toocreate e non sarà mai utilizzato tooinstantiate attori concreti.</span><span class="sxs-lookup"><span data-stu-id="cfd13-121">In some cases, you may wish toocreate a base type that is solely intended for sharing functionality with subtypes and will never be used tooinstantiate concrete actors.</span></span> <span data-ttu-id="cfd13-122">In questi casi, è necessario utilizzare hello `abstract` tooindicate parola chiave che non si può creare un attore basato su tale tipo.</span><span class="sxs-lookup"><span data-stu-id="cfd13-122">In those cases, you should use hello `abstract` keyword tooindicate that you will never create an actor based on that type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfd13-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cfd13-123">Next steps</span></span>
* <span data-ttu-id="cfd13-124">Vedere [come framework Reliable Actors hello sfrutta piattaforma Service Fabric hello](service-fabric-reliable-actors-platform.md) tooprovide affidabilità, scalabilità e uno stato coerente.</span><span class="sxs-lookup"><span data-stu-id="cfd13-124">See [how hello Reliable Actors framework leverages hello Service Fabric platform](service-fabric-reliable-actors-platform.md) tooprovide reliability, scalability, and consistent state.</span></span>
* <span data-ttu-id="cfd13-125">Informazioni su hello [ciclo di vita dell'attore](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="cfd13-125">Learn about hello [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span></span>

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
