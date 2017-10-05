---
title: Serializzazione di un oggetto Reliable Collections in Azure Service Fabric | Microsoft Docs
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
ms.openlocfilehash: c14794b71ce7340d9e90a56d781c712e247ded06
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a><span data-ttu-id="a520c-103">Serializzazione di un oggetto Reliable Collections in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a520c-103">Reliable Collection object serialization in Azure Service Fabric</span></span>
<span data-ttu-id="a520c-104">Le raccolte Reliable Collections replicano e mantengono i propri elementi per garantirne la persistenza anche in caso di errori del computer o interruzioni dell'alimentazione.</span><span class="sxs-lookup"><span data-stu-id="a520c-104">Reliable Collections' replicate and persist their items to make sure they are durable across machine failures and power outages.</span></span>
<span data-ttu-id="a520c-105">Per replicare e rendere persistenti gli elementi, le raccolte Reliable Collections devono serializzarli.</span><span class="sxs-lookup"><span data-stu-id="a520c-105">Both to replicate and to persist items, Reliable Collections' need to serialize them.</span></span>

<span data-ttu-id="a520c-106">Le raccolte Reliable Collections ottengono il serializzatore appropriato per un determinato tipo da Reliable State Manager.</span><span class="sxs-lookup"><span data-stu-id="a520c-106">Reliable Collections' get the appropriate serializer for a given type from Reliable State Manager.</span></span>
<span data-ttu-id="a520c-107">Reliable State Manager contiene serializzatori predefiniti e consente la registrazione di serializzatori personalizzati per un determinato tipo.</span><span class="sxs-lookup"><span data-stu-id="a520c-107">Reliable State Manager contains built-in serializers and allows custom serializers to be registered for a given type.</span></span>

## <a name="built-in-serializers"></a><span data-ttu-id="a520c-108">Serializzatori predefiniti</span><span class="sxs-lookup"><span data-stu-id="a520c-108">Built-in Serializers</span></span>

<span data-ttu-id="a520c-109">Reliable State Manager include serializzatori predefiniti per alcuni tipi comuni, così da consentirne una serializzazione efficiente per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="a520c-109">Reliable State Manager includes built-in serializer for some common types, so that they can be serialized efficiently by default.</span></span> <span data-ttu-id="a520c-110">Per altri tipi, Reliable State Manager esegue il fallback per l'uso di [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="a520c-110">For other types, Reliable State Manager falls back to use the [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).</span></span>
<span data-ttu-id="a520c-111">I serializzatori predefiniti risultano più efficienti perché sanno che i loro tipi non possono essere modificati e non hanno bisogno di includere informazioni sul tipo quali il nome.</span><span class="sxs-lookup"><span data-stu-id="a520c-111">Built-in serializers are more efficient since they know their types cannot change and they do not need to include information about the type like its type name.</span></span>

<span data-ttu-id="a520c-112">Reliable State Manager dispone di un serializzatore predefinito per i tipi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a520c-112">Reliable State Manager has built-in serializer for following types:</span></span> 
- <span data-ttu-id="a520c-113">Guid</span><span class="sxs-lookup"><span data-stu-id="a520c-113">Guid</span></span>
- <span data-ttu-id="a520c-114">bool</span><span class="sxs-lookup"><span data-stu-id="a520c-114">bool</span></span>
- <span data-ttu-id="a520c-115">byte</span><span class="sxs-lookup"><span data-stu-id="a520c-115">byte</span></span>
- <span data-ttu-id="a520c-116">sbyte</span><span class="sxs-lookup"><span data-stu-id="a520c-116">sbyte</span></span>
- <span data-ttu-id="a520c-117">byte[]</span><span class="sxs-lookup"><span data-stu-id="a520c-117">byte[]</span></span>
- <span data-ttu-id="a520c-118">char</span><span class="sxs-lookup"><span data-stu-id="a520c-118">char</span></span>
- <span data-ttu-id="a520c-119">string</span><span class="sxs-lookup"><span data-stu-id="a520c-119">string</span></span>
- <span data-ttu-id="a520c-120">decimal</span><span class="sxs-lookup"><span data-stu-id="a520c-120">decimal</span></span>
- <span data-ttu-id="a520c-121">double</span><span class="sxs-lookup"><span data-stu-id="a520c-121">double</span></span>
- <span data-ttu-id="a520c-122">float</span><span class="sxs-lookup"><span data-stu-id="a520c-122">float</span></span>
- <span data-ttu-id="a520c-123">int</span><span class="sxs-lookup"><span data-stu-id="a520c-123">int</span></span>
- <span data-ttu-id="a520c-124">uint</span><span class="sxs-lookup"><span data-stu-id="a520c-124">uint</span></span>
- <span data-ttu-id="a520c-125">long</span><span class="sxs-lookup"><span data-stu-id="a520c-125">long</span></span>
- <span data-ttu-id="a520c-126">ulong</span><span class="sxs-lookup"><span data-stu-id="a520c-126">ulong</span></span>
- <span data-ttu-id="a520c-127">short</span><span class="sxs-lookup"><span data-stu-id="a520c-127">short</span></span>
- <span data-ttu-id="a520c-128">ushort</span><span class="sxs-lookup"><span data-stu-id="a520c-128">ushort</span></span>

## <a name="custom-serialization"></a><span data-ttu-id="a520c-129">Serializzazione personalizzata</span><span class="sxs-lookup"><span data-stu-id="a520c-129">Custom Serialization</span></span>

<span data-ttu-id="a520c-130">I serializzatori personalizzati vengono comunemente usati per migliorare le prestazioni o per crittografare i dati in rete e su disco.</span><span class="sxs-lookup"><span data-stu-id="a520c-130">Custom serializers are commonly used to increase performance or to encrypt the data over the wire and on disk.</span></span> <span data-ttu-id="a520c-131">Tra le altre ragioni, i serializzatori personalizzati sono in genere più efficienti dei serializzatori generici poiché questi non devono serializzare le informazioni sul tipo.</span><span class="sxs-lookup"><span data-stu-id="a520c-131">Among other reasons, custom serializers are commonly more efficient than generic serializer since they don't need to serialize information about the type.</span></span> 

<span data-ttu-id="a520c-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) viene usato per registrare un serializzatore personalizzato per un tipo T specificato. Questa registrazione deve avvenire durante la costruzione di StatefulServiceBase per assicurare che, prima dell'avvio del ripristino, tutte le raccolte Reliable Collections abbiano accesso al serializzatore pertinente per leggere i dati resi persistenti.</span><span class="sxs-lookup"><span data-stu-id="a520c-132">[IReliableStateManager.TryAddStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) is used to register a custom serializer for the given type T. This registration should happen in the construction of the StatefulServiceBase to ensure that before recovery starts, all Reliable Collections have access to the relevant serializer to read their persisted data.</span></span>

```C#
public StatefulBackendService(StatefulServiceContext context)
  : base(context)
  {
    if (!this.StateManager.TryAddStateSerializer(new OrderKeySerializer()))
    {
      throw new InvalidOperationException("Failed to set OrderKey custom serializer");
    }
  }
```

> [!NOTE]
> <span data-ttu-id="a520c-133">I serializzatori personalizzati hanno la precedenza su quelli predefiniti.</span><span class="sxs-lookup"><span data-stu-id="a520c-133">Custom serializers are given precedence over built-in serializers.</span></span> <span data-ttu-id="a520c-134">Ad esempio, quando viene registrato un serializzatore personalizzato per int, tale serializzatore viene usato per serializzare i valori integer al posto del serializzatore predefinito per int.</span><span class="sxs-lookup"><span data-stu-id="a520c-134">For example, when a custom serializer for int is registered, it is used to serialize integers instead of the built-in serializer for int.</span></span>

### <a name="how-to-implement-a-custom-serializer"></a><span data-ttu-id="a520c-135">Come implementare un serializzatore personalizzato</span><span class="sxs-lookup"><span data-stu-id="a520c-135">How to implement a custom serializer</span></span>

<span data-ttu-id="a520c-136">Un serializzatore personalizzato deve implementare l'interfaccia [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1).</span><span class="sxs-lookup"><span data-stu-id="a520c-136">A custom serializer needs to implement the [IStateSerializer<T>](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interface.</span></span>

> [!NOTE]
> <span data-ttu-id="a520c-137">IStateSerializer<T> include un overload per Write e Read che accetta un T aggiuntivo chiamato valore di base.</span><span class="sxs-lookup"><span data-stu-id="a520c-137">IStateSerializer<T> includes an overload for Write and Read that takes in an additional T called base value.</span></span> <span data-ttu-id="a520c-138">Questa API è per la serializzazione differenziale.</span><span class="sxs-lookup"><span data-stu-id="a520c-138">This API is for differential serialization.</span></span> <span data-ttu-id="a520c-139">Attualmente la funzionalità di serializzazione differenziale non è esposta.</span><span class="sxs-lookup"><span data-stu-id="a520c-139">Currently differential serialization feature is not exposed.</span></span> <span data-ttu-id="a520c-140">Di conseguenza, questi due overload non vengono chiamati fino a quando la serializzazione differenziale non è esposta e abilitata.</span><span class="sxs-lookup"><span data-stu-id="a520c-140">Hence, these two overloads are not called until differential serialization is exposed and enabled.</span></span>

<span data-ttu-id="a520c-141">Di seguito è riportato un esempio di un tipo personalizzato denominato OrderKey che contiene quattro proprietà</span><span class="sxs-lookup"><span data-stu-id="a520c-141">Following is an example custom type called OrderKey that contains four properties</span></span>

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

<span data-ttu-id="a520c-142">Di seguito è riportato un esempio di implementazione di IStateSerializer<OrderKey>.</span><span class="sxs-lookup"><span data-stu-id="a520c-142">Following is an example implementation of IStateSerializer<OrderKey>.</span></span>
<span data-ttu-id="a520c-143">Si noti che gli overload Write e Read che accettano baseValue chiamano il rispettivo overload per la compatibilità di inoltro.</span><span class="sxs-lookup"><span data-stu-id="a520c-143">Note that Read and Write overloads that take in baseValue, call their respective overload for forwards compatibility.</span></span>

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

## <a name="upgradability"></a><span data-ttu-id="a520c-144">Aggiornamento</span><span class="sxs-lookup"><span data-stu-id="a520c-144">Upgradability</span></span>
<span data-ttu-id="a520c-145">In un [aggiornamento in sequenza di un'applicazione](service-fabric-application-upgrade.md)l'aggiornamento viene applicato a un subset di nodi, procedendo con un dominio di aggiornamento per volta.</span><span class="sxs-lookup"><span data-stu-id="a520c-145">In a [rolling application upgrade](service-fabric-application-upgrade.md), the upgrade is applied to a subset of nodes, one upgrade domain at a time.</span></span> <span data-ttu-id="a520c-146">Durante questo processo, alcuni domini di aggiornamento si troveranno con la versione dell'applicazione più recente e altri con quella meno recente.</span><span class="sxs-lookup"><span data-stu-id="a520c-146">During this process, some upgrade domains will be on the newer version of your application, and some upgrade domains will be on the older version of your application.</span></span> <span data-ttu-id="a520c-147">Nella fase di distribuzione, la versione dell'applicazione più recente deve essere in grado di leggere la versione dei dati meno recente e viceversa.</span><span class="sxs-lookup"><span data-stu-id="a520c-147">During the rollout, the new version of your application must be able to read the old version of your data, and the old version of your application must be able to read the new version of your data.</span></span> <span data-ttu-id="a520c-148">Se il formato dei dati non è compatibile con le versioni successive e precedenti, è possibile che l'aggiornamento abbia esito negativo o, peggio ancora, che i dati vengano persi o danneggiati.</span><span class="sxs-lookup"><span data-stu-id="a520c-148">If the data format is not forward and backward compatible, the upgrade may fail, or worse, data may be lost or corrupted.</span></span>

<span data-ttu-id="a520c-149">Se si usano serializzatori predefiniti, non esistono problemi di compatibilità.</span><span class="sxs-lookup"><span data-stu-id="a520c-149">If you are using  built-in serializer, you do not have to worry about compatibility.</span></span>
<span data-ttu-id="a520c-150">Tuttavia, se si usa un serializzatore personalizzato o DataContractSerializer, i dati devono essere compatibili all'infinito con le versioni precedenti e successive.</span><span class="sxs-lookup"><span data-stu-id="a520c-150">However, if you are using a custom serializer or the DataContractSerializer, the data have to be infinitely backwards and forwards compatible.</span></span>
<span data-ttu-id="a520c-151">In altri termini, ogni versione del serializzatore deve essere in grado di serializzare e deserializzare qualsiasi versione del tipo.</span><span class="sxs-lookup"><span data-stu-id="a520c-151">In other words, each version of serializer needs to be able to serialize and de-serialize any version of the type.</span></span>

<span data-ttu-id="a520c-152">Gli utenti del contratto di dati devono seguire regole ben definite di controllo delle versioni per l'aggiunta, la rimozione e la modifica di campi.</span><span class="sxs-lookup"><span data-stu-id="a520c-152">Data Contract users should follow the well-defined versioning rules for adding, removing, and changing fields.</span></span> <span data-ttu-id="a520c-153">Il contratto di dati supporta inoltre l'eredità delle classi, la gestione dei campi sconosciuti e l'uso di hook nel processo di serializzazione e deserializzazione.</span><span class="sxs-lookup"><span data-stu-id="a520c-153">Data Contract also has support for dealing with unknown fields, hooking into the serialization and deserialization process, and dealing with class inheritance.</span></span> <span data-ttu-id="a520c-154">Per altre informazioni, vedere [Utilizzo di contratti dati](https://msdn.microsoft.com/library/ms733127.aspx).</span><span class="sxs-lookup"><span data-stu-id="a520c-154">For more information, see [Using Data Contract](https://msdn.microsoft.com/library/ms733127.aspx).</span></span>

<span data-ttu-id="a520c-155">Gli utenti di serializzatori personalizzati devono seguire le linee guida del serializzatore in uso per verificarne la compatibilità con le versioni precedenti e successive.</span><span class="sxs-lookup"><span data-stu-id="a520c-155">Custom serializer users should adhere to the guidelines of the serializer they are using to make sure it is backwards and forwards compatible.</span></span>
<span data-ttu-id="a520c-156">Un modo comune per supportare tutte le versioni consiste nell'aggiungere le informazioni sulle dimensioni all'inizio e nell'aggiungere soltanto proprietà facoltative.</span><span class="sxs-lookup"><span data-stu-id="a520c-156">Common way of supporting all versions is adding size information at the beginning and only adding optional properties.</span></span>
<span data-ttu-id="a520c-157">In questo modo ogni versione può leggere tutto quanto è in grado di leggere, saltando la rimanente parte del flusso.</span><span class="sxs-lookup"><span data-stu-id="a520c-157">This way each version can read as much it can and jump over the remaining part of the stream.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a520c-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a520c-158">Next steps</span></span>
  * [<span data-ttu-id="a520c-159">Serializzazione e aggiornamento</span><span class="sxs-lookup"><span data-stu-id="a520c-159">Serialization and upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="a520c-160">Guida di riferimento per gli sviluppatori per Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="a520c-160">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * <span data-ttu-id="a520c-161">[Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md) descrive la procedura di aggiornamento di un'applicazione con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a520c-161">[Upgrading your Application Using Visual Studio](service-fabric-application-upgrade-tutorial.md) walks you through an application upgrade using Visual Studio.</span></span>
  * <span data-ttu-id="a520c-162">[Aggiornamento di un'applicazione di Service Fabric mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) descrive la procedura di aggiornamento di un'applicazione tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a520c-162">[Upgrading your Application Using Powershell](service-fabric-application-upgrade-tutorial-powershell.md) walks you through an application upgrade using PowerShell.</span></span>
  * <span data-ttu-id="a520c-163">Controllare l’aggiornamento dell'applicazione tramite [Parametri di aggiornamento](service-fabric-application-upgrade-parameters.md).</span><span class="sxs-lookup"><span data-stu-id="a520c-163">Control how your application upgrades by using [Upgrade Parameters](service-fabric-application-upgrade-parameters.md).</span></span>
  * <span data-ttu-id="a520c-164">Per informazioni su come usare funzionalità avanzate durante l'aggiornamento dell'applicazione, vedere [Argomenti avanzati](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="a520c-164">Learn how to use advanced functionality while upgrading your application by referring to [Advanced Topics](service-fabric-application-upgrade-advanced.md).</span></span>
  * <span data-ttu-id="a520c-165">Per informazioni su come risolvere problemi comuni negli aggiornamenti dell'applicazione, vedere i passaggi indicati in [Risoluzione dei problemi relativi agli aggiornamenti dell'applicazione](service-fabric-application-upgrade-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="a520c-165">Fix common problems in application upgrades by referring to the steps in [Troubleshooting Application Upgrades](service-fabric-application-upgrade-troubleshooting.md).</span></span>
