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
# <a name="reliable-collection-object-serialization-in-azure-service-fabric"></a>Serializzazione di un oggetto Reliable Collections in Azure Service Fabric
Affidabile raccolte vengono replicate e rendere persistenti le toomake elementi siano durevoli tra gli errori di computer e interruzioni dell'alimentazione.
Elementi tooreplicate sia toopersist, tooserialize necessità affidabile raccolte li.

Affidabile raccolte ottenere serializzatore appropriato hello per un determinato tipo dal gestore degli stati affidabile.
Gestore degli stati affidabile contiene i serializzatori incorporati e consente di serializzatori personalizzati toobe registrato per un determinato tipo.

## <a name="built-in-serializers"></a>Serializzatori predefiniti

Reliable State Manager include serializzatori predefiniti per alcuni tipi comuni, così da consentirne una serializzazione efficiente per impostazione predefinita. Per altri tipi di gestore degli stati affidabile il fallback hello toouse [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer(v=vs.110).aspx).
Serializzatori incorporati risultano più efficienti perché sappiano che non è possibile modificare i relativi tipi e non devono tooinclude informazioni sul tipo di hello come il nome del tipo.

Reliable State Manager dispone di un serializzatore predefinito per i tipi seguenti: 
- Guid
- bool
- byte
- sbyte
- byte[]
- char
- string
- decimal
- double
- float
- int
- uint
- long
- ulong
- short
- ushort

## <a name="custom-serialization"></a>Serializzazione personalizzata

Serializzatori personalizzati sono dati di hello di prestazioni o tooencrypt tooincrease comunemente utilizzati durante la trasmissione hello e su disco. Uno dei motivi, serializzatori personalizzati sono in genere più efficienti serializzatore generico poiché non è necessario tooserialize informazioni sul tipo hello. 

[IReliableStateManager.TryAddStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.ireliablestatemanager.tryaddstateserializer--1?Microsoft_ServiceFabric_Data_IReliableStateManager_TryAddStateSerializer__1_Microsoft_ServiceFabric_Data_IStateSerializer___0__) è tooregister usato un serializzatore personalizzato per hello dato di tipo T. La registrazione deve essere eseguito nel costruzione hello di hello StatefulServiceBase tooensure prima di avvio del recupero, tutte le raccolte affidabile necessario accedere ai dati persistenti in toohello serializzatore rilevanti tooread.

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
> I serializzatori personalizzati hanno la precedenza su quelli predefiniti. Ad esempio, quando viene registrato un serializzatore personalizzato per int, viene utilizzato tooserialize interi anziché serializzatore incorporato di hello per int.

### <a name="how-tooimplement-a-custom-serializer"></a>Come tooimplement un serializzatore personalizzato

Un serializzatore personalizzato deve hello tooimplement [IStateSerializer<T> ](https://docs.microsoft.com/dotnet/api/microsoft.servicefabric.data.istateserializer-1) interfaccia.

> [!NOTE]
> IStateSerializer<T> include un overload per Write e Read che accetta un T aggiuntivo chiamato valore di base. Questa API è per la serializzazione differenziale. Attualmente la funzionalità di serializzazione differenziale non è esposta. Di conseguenza, questi due overload non vengono chiamati fino a quando la serializzazione differenziale non è esposta e abilitata.

Di seguito è riportato un esempio di un tipo personalizzato denominato OrderKey che contiene quattro proprietà

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

Di seguito è riportato un esempio di implementazione di IStateSerializer<OrderKey>.
Si noti che gli overload Write e Read che accettano baseValue chiamano il rispettivo overload per la compatibilità di inoltro.

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

## <a name="upgradability"></a>Aggiornamento
In un [aggiornamento in sequenza](service-fabric-application-upgrade.md), hello aggiornamento è stato applicato tooa sottoinsieme di nodi, un dominio di aggiornamento alla volta. Durante questo processo, alcuni domini di aggiornamento sarà nella versione più recente di hello dell'applicazione, e alcuni domini di aggiornamento sarà in una versione precedente dell'applicazione hello. Durante l'implementazione di hello, hello nuova versione dell'applicazione deve essere in grado di tooread hello precedente dei dati e hello precedente versione dell'applicazione deve essere in grado di tooread hello nuova dei dati. Se formato dati hello non avanti e indietro aggiornamento hello compatibile, potrebbero non viene eseguito o, ancora peggio, dati potrebbe essere perso o danneggiato.

Se si utilizza il serializzatore predefinito, tooworry sulla compatibilità non si dispone.
Tuttavia, se si utilizza un serializzatore personalizzato o hello DataContractSerializer, dati hello hanno toobe all'infinito con le versioni precedenti e inoltra compatibili.
In altre parole, ogni versione del serializzatore deve tooserialize in grado di toobe e deserializzare qualsiasi versione di hello tipo.

Gli utenti di contratto dati devono seguire le regole di controllo delle versioni ben definito di hello per l'aggiunta, rimozione e modifica dei campi. Contratto dati è inoltre supportata per la gestione con campi sconosciuti, associazione nel processo di serializzazione e deserializzazione hello e gestiscono l'ereditarietà della classe. Per altre informazioni, vedere [Utilizzo di contratti dati](https://msdn.microsoft.com/library/ms733127.aspx).

Gli utenti di serializzatore personalizzato devono rispettare le linee guida toohello del serializzatore hello che usano toomake sia con le versioni precedenti e successive.
Un modo comune di supportare tutte le versioni aggiunge informazioni sulle dimensioni all'inizio di hello e solo l'aggiunta di proprietà facoltative.
In questo modo ogni versione è possibile leggere la maggior parte può e consente di passare parte rimanente di hello del flusso di hello.

## <a name="next-steps"></a>Passaggi successivi
  * [Serializzazione e aggiornamento](service-fabric-application-upgrade-data-serialization.md)
  * [Guida di riferimento per gli sviluppatori per Reliable Collections](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
  * [Esercitazione sull'aggiornamento di un'applicazione di Service Fabric tramite Visual Studio](service-fabric-application-upgrade-tutorial.md) descrive la procedura di aggiornamento di un'applicazione con Visual Studio.
  * [Aggiornamento di un'applicazione di Service Fabric mediante PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) descrive la procedura di aggiornamento di un'applicazione tramite PowerShell.
  * Controllare l’aggiornamento dell'applicazione tramite [Parametri di aggiornamento](service-fabric-application-upgrade-parameters.md).
  * Informazioni su come toouse funzionalità avanzate durante l'aggiornamento dell'applicazione riferendosi troppo[argomenti avanzati](service-fabric-application-upgrade-advanced.md).
  * Risolvere i problemi comuni negli aggiornamenti dell'applicazione riferendosi passaggi toohello [risoluzione dei problemi gli aggiornamenti dell'applicazione](service-fabric-application-upgrade-troubleshooting.md).
