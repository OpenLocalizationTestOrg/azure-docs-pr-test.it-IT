---
title: Polimorfismo nel framework Reliable Actors | Microsoft Docs
description: "Compilare gerarchie di interfacce e tipi .NET nel framework Reliable Actors per riutilizzare le funzionalità e le definizioni delle API."
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
ms.openlocfilehash: 36a59a41b2261369a2062c76ef90aebf7e24a221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="polymorphism-in-the-reliable-actors-framework"></a><span data-ttu-id="d1c01-103">Polimorfismo nel framework Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="d1c01-103">Polymorphism in the Reliable Actors framework</span></span>
<span data-ttu-id="d1c01-104">Il framework Reliable Actors consente di creare attori usando molte delle tecniche usate per la progettazione orientata agli oggetti.</span><span class="sxs-lookup"><span data-stu-id="d1c01-104">The Reliable Actors framework allows you to build actors using many of the same techniques that you would use in object-oriented design.</span></span> <span data-ttu-id="d1c01-105">Una di queste tecniche è il polimorfismo, che consente a tipi e interfacce di ereditare da più elementi padre generalizzati.</span><span class="sxs-lookup"><span data-stu-id="d1c01-105">One of those techniques is polymorphism, which allows types and interfaces to inherit from more generalized parents.</span></span> <span data-ttu-id="d1c01-106">L'ereditarietà nel framework Reliable Actors in genere segue il modello .NET con alcuni vincoli aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="d1c01-106">Inheritance in the Reliable Actors framework generally follows the .NET model with a few additional constraints.</span></span> <span data-ttu-id="d1c01-107">In caso di Java/Linux, segue il modello Java.</span><span class="sxs-lookup"><span data-stu-id="d1c01-107">In case of Java/Linux, it follows the Java model.</span></span>

## <a name="interfaces"></a><span data-ttu-id="d1c01-108">Interfacce</span><span class="sxs-lookup"><span data-stu-id="d1c01-108">Interfaces</span></span>
<span data-ttu-id="d1c01-109">Per il framework Reliable Actors è necessario definire almeno un'interfaccia da implementare attraverso il tipo di attore.</span><span class="sxs-lookup"><span data-stu-id="d1c01-109">The Reliable Actors framework requires you to define at least one interface to be implemented by your actor type.</span></span> <span data-ttu-id="d1c01-110">Questa interfaccia viene utilizzata per generare una classe proxy che può essere utilizzata dai client per comunicare con gli attori.</span><span class="sxs-lookup"><span data-stu-id="d1c01-110">This interface is used to generate a proxy class that can be used by clients to communicate with your actors.</span></span> <span data-ttu-id="d1c01-111">Le interfacce possono ereditare da altre interfacce, purché ogni interfaccia implementata da un tipo di attore e tutte le relative entità principali derivino da IActor (C#) o da Actor (Java).</span><span class="sxs-lookup"><span data-stu-id="d1c01-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span></span> <span data-ttu-id="d1c01-112">IActor (C#) e Actor (Java) sono le interfacce di base definite dalla piattaforma per gli attori rispettivamente nei framework .NET e Java.</span><span class="sxs-lookup"><span data-stu-id="d1c01-112">IActor(C#) and Actor(Java) are the platform-defined base interfaces for actors in the frameworks .NET and Java respectively.</span></span> <span data-ttu-id="d1c01-113">Pertanto, l'esempio di polimorfismo classico che utilizza le forme può apparire nel seguente modo:</span><span class="sxs-lookup"><span data-stu-id="d1c01-113">Thus, the classic polymorphism example using shapes might look something like this:</span></span>

![Gerarchia delle interfacce per gli attori della forma][shapes-interface-hierarchy]

## <a name="types"></a><span data-ttu-id="d1c01-115">Types</span><span class="sxs-lookup"><span data-stu-id="d1c01-115">Types</span></span>
<span data-ttu-id="d1c01-116">È inoltre possibile creare una gerarchia di tipi di attore, derivati dalla classe Attore di base fornita dalla piattaforma.</span><span class="sxs-lookup"><span data-stu-id="d1c01-116">You can also create a hierarchy of actor types, which are derived from the base Actor class that is provided by the platform.</span></span> <span data-ttu-id="d1c01-117">Nel caso delle forme può essere presente un tipo `Shape` (C#) o `ShapeImpl` (Java) di base.</span><span class="sxs-lookup"><span data-stu-id="d1c01-117">In the case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span></span>

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

<span data-ttu-id="d1c01-118">I sottotipi di `Shape` (C#) o `ShapeImpl` (Java) possono eseguire l'override dei metodi dalla base.</span><span class="sxs-lookup"><span data-stu-id="d1c01-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from the base.</span></span>

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

<span data-ttu-id="d1c01-119">Si noti l’attributo `ActorService` nel tipo di attore.</span><span class="sxs-lookup"><span data-stu-id="d1c01-119">Note the `ActorService` attribute on the actor type.</span></span> <span data-ttu-id="d1c01-120">Questo attributo indica al framework Reliable Actors che deve creare automaticamente un servizio per l'hosting di attori di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="d1c01-120">This attribute tells the Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span></span> <span data-ttu-id="d1c01-121">In alcuni casi, si potrebbe creare un tipo di base progettato esclusivamente per la condivisione delle funzionalità con dei sottotipi e che non verrà mai usato per creare un'istanza di attori concreti.</span><span class="sxs-lookup"><span data-stu-id="d1c01-121">In some cases, you may wish to create a base type that is solely intended for sharing functionality with subtypes and will never be used to instantiate concrete actors.</span></span> <span data-ttu-id="d1c01-122">In questi casi, è necessario usare la parola chiave `abstract` per indicare che non si creerà mai un attore basato su quel tipo.</span><span class="sxs-lookup"><span data-stu-id="d1c01-122">In those cases, you should use the `abstract` keyword to indicate that you will never create an actor based on that type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1c01-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d1c01-123">Next steps</span></span>
* <span data-ttu-id="d1c01-124">Vedere [come il framework di Reliable Actors usufruisce della piattaforma Service Fabric](service-fabric-reliable-actors-platform.md) per fornire uno stato coerente, scalabilità e affidabilità.</span><span class="sxs-lookup"><span data-stu-id="d1c01-124">See [how the Reliable Actors framework leverages the Service Fabric platform](service-fabric-reliable-actors-platform.md) to provide reliability, scalability, and consistent state.</span></span>
* <span data-ttu-id="d1c01-125">Informazioni sul [ciclo di vita degli attori](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="d1c01-125">Learn about the [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span></span>

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
