---
title: serializzazione di oggetti raccolta in Azure Service Fabric aaaReliable | Documenti Microsoft
description: Serializzazione di un oggetto Reliable Collections di Azure Service Fabric
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 9d35374c-2d75-4856-b776-e59284641956
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/8/2017
ms.author: mcoskun
ms.openlocfilehash: 248defbe0ae6f65b4ac5dc7c74e80d8f1152ce94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="77224-103">Serializzazione di un oggetto Reliable Collections in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="77224-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="77224-104">Affidabile raccolte vengono replicate e rendere persistenti le toomake elementi siano durevoli tra gli errori di computer e interruzioni dell'alimentazione.</span><span class="sxs-lookup"><span data-stu-id="77224-104">Reliable Collections' replicate and persist their items toomake sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="77224-105">Elementi tooreplicate sia toopersist, tooserialize necessità affidabile raccolte li.</span><span class="sxs-lookup"><span data-stu-id="77224-105">Both tooreplicate and toopersist items, Reliable Collections' need tooserialize them.</span></span>

<span data-ttu-id="77224-106">Affidabile raccolte ottenere serializzatore appropriato hello per un determinato tipo dal gestore degli stati affidabile.</span><span class="sxs-lookup"><span data-stu-id="77224-106">Reliable Collections' get hello appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="77224-107">Gestore degli stati affidabile contiene i serializzatori incorporati e consente di serializzatori personalizzati toobe registrato per un determinato tipo.</span><span class="sxs-lookup"><span data-stu-id="77224-107">Reliable State Manager contains built-in serializers and allows custom serializers toobe registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="77224-108">Serializzatori predefiniti</span><span class="sxs-lookup"><span data-stu-id="77224-108">Built-in Serializers</span></span>

<span data-ttu-id="77224-109">Reliable State Manager include serializzatori predefiniti per alcuni tipi comuni, così da consentirne una serializzazione efficiente per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="77224-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="77224-110">Per altri tipi di gestore degli stati affidabile il fallback hello toouse [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="77224-110">For other types, Reliable State Manager falls back toouse hello [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="77224-111">Serializzatori incorporati risultano più efficienti perché sappiano che non è possibile modificare i relativi tipi e non devono tooinclude informazioni sul tipo di hello come il nome del tipo.</span><span class="sxs-lookup"><span data-stu-id="77224-111">Built-in serializers are more efficient since they know their types cannot change and they do not need tooinclude information about hello type like its type name.</span></span>

<span data-ttu-id="77224-112">Reliable State Manager dispone di un serializzatore predefinito per i tipi seguenti:</span><span class="sxs-lookup"><span data-stu-id="77224-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="77224-113">Guid</span><span class="sxs-lookup"><span data-stu-id="77224-113">Guid</span></span>
- <span data-ttu-id="77224-114">bool</span><span class="sxs-lookup"><span data-stu-id="77224-114">bool</span></span>
- <span data-ttu-id="77224-115">byte</span><span class="sxs-lookup"><span data-stu-id="77224-115">byte</span></span>
- <span data-ttu-id="77224-116">sbyte</span><span class="sxs-lookup"><span data-stu-id="77224-116">sbyte</span></span>
- <span data-ttu-id="77224-117">byte[]</span><span class="sxs-lookup"><span data-stu-id="77224-117">byte[]</span></span>
- <span data-ttu-id="77224-118">char</span><span class="sxs-lookup"><span data-stu-id="77224-118">char</span></span>
- <span data-ttu-id="77224-119">string</span><span class="sxs-lookup"><span data-stu-id="77224-119">string</span></span>
- <span data-ttu-id="77224-120">decimal</span><span class="sxs-lookup"><span data-stu-id="77224-120">decimal</span></span>
- <span data-ttu-id="77224-121">double</span><span class="sxs-lookup"><span data-stu-id="77224-121">double</span></span>
- <span data-ttu-id="77224-122">float</span><span class="sxs-lookup"><span data-stu-id="77224-122">float</span></span>
- <span data-ttu-id="77224-123">int</span><span class="sxs-lookup"><span data-stu-id="77224-123">int</span></span>
- <span data-ttu-id="77224-124">uint</span><span class="sxs-lookup"><span data-stu-id="77224-124">uint</span></span>
- <span data-ttu-id="77224-125">long</span><span class="sxs-lookup"><span data-stu-id="77224-125">long</span></span>
- <span data-ttu-id="77224-126">ulong</span><span class="sxs-lookup"><span data-stu-id="77224-126">ulong</span></span>
- <span data-ttu-id="77224-127">short</span><span class="sxs-lookup"><span data-stu-id="77224-127">short</span></span>
- <span data-ttu-id="77224-128">ushort</span><span class="sxs-lookup"><span data-stu-id="77224-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="77224-129">Serializzazione personalizzata</span><span class="sxs-lookup"><span data-stu-id="77224-129">Custom Serialization</span></span>

<span data-ttu-id="77224-130">Serializzatori personalizzati sono dati di hello di prestazioni o tooencrypt tooincrease comunemente utilizzati durante la trasmissione hello e su disco.</span><span class="sxs-lookup"><span data-stu-id="77224-130">Custom serializers are commonly used tooincrease performance or tooencrypt hello data over hello wire and on disk.</span></span> <span data-ttu-id="77224-131">Uno dei motivi, serializzatori personalizzati sono in genere più efficienti serializzatore generico poiché non è necessario tooserialize informazioni sul tipo hello.</span><span class="sxs-lookup"><span data-stu-id="77224-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need tooserialize information about hello type.</span></span> 

<span data-ttu-id="77224-132">[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) è tooregister usato un serializzatore personalizzato per hello dato di tipo T. La registrazione deve essere eseguito nel costruzione hello di hello StatefulServiceBase tooensure prima di avvio del recupero, tutte le raccolte affidabile necessario accedere ai dati persistenti in toohello serializzatore rilevanti tooread.</span><span class="sxs-lookup"><span data-stu-id="77224-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used tooregister a custom serializer for hello given type T. This registration should happen in hello construction of hello StatefulServiceBase tooensure that before recovery starts, all Reliable Collections have access toohello relevant serializer tooread their persisted data.</span></span>

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed tooset OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> <span data-ttu-id="77224-133">I serializzatori personalizzati hanno la precedenza su quelli predefiniti.</span><span class="sxs-lookup"><span data-stu-id="77224-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="77224-134">Ad esempio, quando viene registrato un serializzatore personalizzato per int, viene utilizzato tooserialize interi anziché serializzatore incorporato di hello per int.</span><span class="sxs-lookup"><span data-stu-id="77224-134">For example, when a custom serializer for int is registered, it is used tooserialize integers instead of hello built-in serializer for int.</span></span>

### <a name="how-tooimplement-a-custom-serializer"></a><span data-ttu-id="77224-135">Come tooimplement un serializzatore personalizzato</span><span class="sxs-lookup"><span data-stu-id="77224-135">How tooimplement a custom serializer</span></span>

<span data-ttu-id="77224-136">Un serializzatore personalizzato deve hello tooimplement [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interfaccia.</span><span class="sxs-lookup"><span data-stu-id="77224-136">A custom serializer needs tooimplement hello [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="77224-137">IStateSerializer<T> include un overload per Write e Read che accetta un T aggiuntivo chiamato valore di base.</span><span class="sxs-lookup"><span data-stu-id="77224-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="77224-138">Questa API è per la serializzazione differenziale.</span><span class="sxs-lookup"><span data-stu-id="77224-138">This API is for differential serialization.</span></span> <span data-ttu-id="77224-139">Attualmente la funzionalità di serializzazione differenziale non è esposta.</span><span class="sxs-lookup"><span data-stu-id="77224-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="77224-140">Di conseguenza, questi due overload non vengono chiamati fino a quando la serializzazione differenziale non è esposta e abilitata.</span><span class="sxs-lookup"><span data-stu-id="77224-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="77224-141">Di seguito è riportato un esempio di un tipo personalizzato denominato OrderKey che contiene quattro proprietà</span><span class="sxs-lookup"><span data-stu-id="77224-141">Following is an example custom type called OrderKey that contains four properties</span></span>

```C#
public class OrderKey : IComparable<OrderKey>, IEquatable<OrderKey>
{
    public byte Warehouse { get; set; }

    public short District { get; set; }

    public int Customer { get; set; }

    public long Order { get; set; }

    #region Object Overrides for GetHashCode, CompareTo and Equals
    #endregion
}
```

<span data-ttu-id="77224-142">Di seguito è riportato un esempio di implementazione di IStateSerializer<OrderKey>.</span><span class="sxs-lookup"><span data-stu-id="77224-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="77224-143">Si noti che gli overload Write e Read che accettano baseValue chiamano il rispettivo overload per la compatibilità di inoltro.</span><span class="sxs-lookup"><span data-stu-id="77224-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

```C#
public class OrderKeySerializer : IStateSerializer<OrderKey>
{
  OrderKey IStateSerializer<OrderKey>.Read(BinaryReader reader)
  {
      var value = new OrderKey();
      value.Warehouse = reader.ReadByte();
      value.District = reader.ReadInt16();
      value.Customer = reader.ReadInt32();
      value.Order = reader.ReadInt64();

      return value;
  }

  void IStateSerializer<OrderKey>.Write(OrderKey value, BinaryWriter writer)
  {
      writer.Write(value.Warehouse);
      writer.Write(value.District);
      writer.Write(value.Customer);
      writer.Write(value.Order);
  }
  
  // Read overload for differential de-serialization
  OrderKey IStateSerializer<OrderKey>.Read(OrderKey baseValue, BinaryReader reader)
  {
      return ((IStateSerializer<OrderKey>)this).Read(reader);
  }

  // Write overload for differential serialization
  void IStateSerializer<OrderKey>.Write(OrderKey baseValue, OrderKey newValue, BinaryWriter writer)
  {
      ((IStateSerializer<OrderKey>)this).Write(newValue, writer);
  }
}
```

## <a name="upgradability"></a><span data-ttu-id="77224-144">Aggiornamento</span><span class="sxs-lookup"><span data-stu-id="77224-144">Upgradability</span></span>
<span data-ttu-id="77224-145">In un [aggiornamento in sequenza](service-fabric-application-upgrade.md), hello aggiornamento è stato applicato tooa sottoinsieme di nodi, un dominio di aggiornamento alla volta.</span><span class="sxs-lookup"><span data-stu-id="77224-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), hello upgrade is applied tooa subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="77224-146">Durante questo processo, alcuni domini di aggiornamento sarà nella versione più recente di hello dell'applicazione, e alcuni domini di aggiornamento sarà in una versione precedente dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="77224-146">During this process, some upgrade domains will be on hello newer version of your application, and some upgrade domains will be on hello older version of your application.</span></span> <span data-ttu-id="77224-147">Durante l'implementazione di hello, hello nuova versione dell'applicazione deve essere in grado di tooread hello precedente dei dati e hello precedente versione dell'applicazione deve essere in grado di tooread hello nuova dei dati.</span><span class="sxs-lookup"><span data-stu-id="77224-147">During hello rollout, hello new version of your application must be able tooread hello old version of your data, and hello old version of your application must be able tooread hello new version of your data.</span></span> <span data-ttu-id="77224-148">Se formato dati hello non avanti e indietro aggiornamento hello compatibile, potrebbero non viene eseguito o, ancora peggio, dati potrebbe essere perso o danneggiato.</span><span class="sxs-lookup"><span data-stu-id="77224-148">If hello data format is not forward and backward compatible, hello upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="77224-149">Se si utilizza il serializzatore predefinito, tooworry sulla compatibilità non si dispone.</span><span class="sxs-lookup"><span data-stu-id="77224-149">If you are using  built-in serializer, you do not have tooworry about compatibility.</span></span>
<span data-ttu-id="77224-150">Tuttavia, se si utilizza un serializzatore personalizzato o hello DataContractSerializer, dati hello hanno toobe all'infinito con le versioni precedenti e inoltra compatibili.</span><span class="sxs-lookup"><span data-stu-id="77224-150">However, if you are using a custom serializer or hello DataContractSerializer, hello data have toobe infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="77224-151">In altre parole, ogni versione del serializzatore deve tooserialize in grado di toobe e deserializzare qualsiasi versione di hello tipo.</span><span class="sxs-lookup"><span data-stu-id="77224-151">In other words, each version of serializer needs toobe able tooserialize and de-serialize any version of hello type.</span></span>

<span data-ttu-id="77224-152">Gli utenti di contratto dati devono seguire le regole di controllo delle versioni ben definito di hello per l'aggiunta, rimozione e modifica dei campi.</span><span class="sxs-lookup"><span data-stu-id="77224-152">Data Contract users should follow hello well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="77224-153">Contratto dati è inoltre supportata per la gestione con campi sconosciuti, associazione nel processo di serializzazione e deserializzazione hello e gestiscono l'ereditarietà della classe.</span><span class="sxs-lookup"><span data-stu-id="77224-153">Data Contract also has support for dealing with unknown fields, hooking into hello serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="77224-154">Per altre informazioni, vedere [Utilizzo di contratti dati](https://msdn.microsoft.com/library/ms733127.aspx).</span><span class="sxs-lookup"><span data-stu-id="77224-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="77224-155">Gli utenti di serializzatore personalizzato devono rispettare le linee guida toohello del serializzatore hello che usano toomake sia con le versioni precedenti e successive.</span><span class="sxs-lookup"><span data-stu-id="77224-155">Custom serializer users should adhere toohello guidelines of hello serializer they are using toomake sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="77224-156">Un modo comune di supportare tutte le versioni aggiunge informazioni sulle dimensioni all'inizio di hello e solo l'aggiunta di proprietà facoltative.</span><span class="sxs-lookup"><span data-stu-id="77224-156">Common way of supporting all versions is adding size information at hello beginning and only adding optional properties.</span></span>
<span data-ttu-id="77224-157">In questo modo ogni versione è possibile leggere la maggior parte può e consente di passare parte rimanente di hello del flusso di hello.</span><span class="sxs-lookup"><span data-stu-id="77224-157">This way each version can read as much it can and jump over hello remaining part of hello stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77224-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="77224-158">Next steps</span></span>
  * [<span data-ttu-id="77224-159">Serializzazione e aggiornamento</span><span class="sxs-lookup"><span data-stu-id="77224-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="77224-160">Guida di riferimento per gli sviluppatori per Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="77224-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="77224-161">[Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md) descrive la procedura di aggiornamento di un'applicazione con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="77224-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="77224-162">[Aggiornamento di un'applicazione di Service Fabric mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) descrive la procedura di aggiornamento di un'applicazione tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77224-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="77224-163">Controllare l’aggiornamento dell'applicazione tramite [Parametri di aggiornamento](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="77224-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="77224-164">Informazioni su come toouse funzionalità avanzate durante l'aggiornamento dell'applicazione riferendosi troppo[argomenti avanzati](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="77224-164">Learn how toouse advanced functionality while upgrading your application by referring too[Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="77224-165">Risolvere i problemi comuni negli aggiornamenti dell'applicazione riferendosi passaggi toohello [risoluzione dei problemi gli aggiornamenti dell'applicazione](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="77224-165">Fix common problems in application upgrades by referring toohello steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
