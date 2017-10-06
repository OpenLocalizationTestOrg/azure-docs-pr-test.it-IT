---
title: le impostazioni di KVSActorStateProvider aaaChange in Azure microservizi | Documenti Microsoft
description: Informazioni sulla configurazione di attori con stato di tipo KVSActorStateProvider in Service Fabric di Azure.
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: e003512678556e68a8926b1b9c6c28d9ae3979d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--kvsactorstateprovider"></a>Configurare KVSActorStateProvider di Reliable Actors
È possibile modificare configurazione predefinita di hello di KVSActorStateProvider modificando hello Settings file che viene generato nella directory principale del pacchetto di Microsoft Visual Studio hello nella cartella Config hello per attore specificato hello.

Hello Azure Service Fabric runtime cerca i nomi di sezione predefinita nel file Settings hello e utilizza i valori di configurazione hello durante la creazione di componenti di runtime sottostante hello.

> [!NOTE]
> Eseguire **non** eliminare o modificare i nomi di sezione hello di hello seguendo le configurazioni nel file Settings hello che viene generato in hello soluzione di Visual Studio.
> 
> 

## <a name="replicator-security-configuration"></a>Configurazione della sicurezza del replicatore
Le configurazioni di sicurezza Replicator sono canale di comunicazione utilizzati toosecure hello utilizzato durante la replica. Ciò significa che i servizi non è possibile vedere di altro traffico di replica, assicurandosi che i dati hello resi altamente disponibili anche siano sicuri.
Per impostazione predefinita, una sezione di configurazione della sicurezza vuota non abilita la sicurezza della replica.

### <a name="section-name"></a>Nome della sezione
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Configurazione del replicatore
Le configurazioni di Replicator configurare replicator hello che è responsabile di garantire lo stato del Provider di stato attore hello altamente affidabile.
configurazione predefinita di Hello viene generato dal modello di Visual Studio hello e dovrebbe essere sufficiente. In questa sezione si indica ulteriori configurazioni replicator hello tootune disponibili.

### <a name="section-name"></a>Nome della sezione
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Nomi delle configurazioni
| Nome | Unità | Valore predefinito | Osservazioni |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Secondi |0,015 |Periodo di tempo per cui replicator hello in attese secondario di hello dopo la ricezione di un'operazione prima di inviare nuovamente un toohello acknowledgement primario. Altri toobe acknowledgement inviato per le operazioni di elaborazione all'interno dell'intervallo vengono inviati come una risposta. |
| ReplicatorEndpoint |N/D |Nessun valore predefinito: parametro obbligatorio |Indirizzo IP e porta hello primario o secondario. replicator utilizzerà toocommunicate con altri i servizi di replica nel set di repliche hello. Si deve fare riferimento a un endpoint TCP risorse di manifesto del servizio hello. Fare riferimento troppo[risorse manifesto del servizio](service-fabric-service-manifest-resources.md) tooread ulteriori informazioni sulla definizione delle risorse di endpoint nel manifesto del servizio hello. |
| RetryInterval |Secondi |5 |Periodo di tempo dopo replicator quali hello nuovamente trasmette un messaggio se non viene ricevuto un acknowledgement per un'operazione. |
| MaxReplicationMessageSize |Byte |50 MB |Dimensione massima dei dati di replica che è possibile trasmettere in un singolo messaggio. |
| MaxPrimaryReplicationQueueSize |Numero di operazioni |1024 |Numero massimo di operazioni in coda primaria hello. Un'operazione viene liberata dopo la replica primaria hello riceverà un acknowledgement da tutti i Replicator secondario hello. Questo valore deve essere maggiore di 64 ed essere una potenza di 2. |
| MaxSecondaryReplicationQueueSize |Numero di operazioni |2048 |Numero massimo di operazioni nella coda secondaria hello. Un'operazione viene liberata quando il relativo stato viene reso altamente disponibile tramite persistenza. Questo valore deve essere maggiore di 64 ed essere una potenza di 2. |

## <a name="store-configuration"></a>Configurazione dell'archivio
Le configurazioni di archivio sono utilizzati tooconfigure hello archivio locale che è stato hello toopersist utilizzati che viene replicato.
configurazione predefinita di Hello viene generato dal modello di Visual Studio hello e dovrebbe essere sufficiente. In questa sezione si indica ulteriori configurazioni archivio locale di hello tootune disponibili.

### <a name="section-name"></a>Nome della sezione
&lt;ActorName&gt;ServiceLocalStoreConfig

### <a name="configuration-names"></a>Nomi delle configurazioni
| Nome | Unità | Valore predefinito | Osservazioni |
| --- | --- | --- | --- |
| MaxAsyncCommitDelayInMilliseconds |Millisecondi |200 |Imposta massimo hello intervallo per l'archivio locale durevole commit di batch. |
| MaxVerPages |Numero di pagine |16384 |numero massimo di Hello di pagine della versione di hello locale archiviazione i database. Determina il numero massimo di hello di transazioni in sospeso. |

## <a name="sample-configuration-file"></a>File di configurazione di esempio
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
   </Section>
   <Section Name="MyActorServiceLocalStoreConfig">
      <Parameter Name="MaxVerPages" Value="8192" />
   </Section>
   <Section Name="MyActorServiceReplicatorSecurityConfig">
      <Parameter Name="CredentialType" Value="X509" />
      <Parameter Name="FindType" Value="FindByThumbprint" />
      <Parameter Name="FindValue" Value="9d c9 06 b1 69 dc 4f af fd 16 97 ac 78 1e 80 67 90 74 9d 2f" />
      <Parameter Name="StoreLocation" Value="LocalMachine" />
      <Parameter Name="StoreName" Value="My" />
      <Parameter Name="ProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="AllowedCommonNames" Value="My-Test-SAN1-Alice,My-Test-SAN1-Bob" />
   </Section>
</Settings>
```
## <a name="remarks"></a>Osservazioni
parametro BatchAcknowledgementInterval Hello controlla la latenza di replica. Il valore '0' comporterà hello latenza più bassa possibile, al costo di hello di velocità effettiva (come ulteriori messaggi di riconoscimento devono essere inviati e l'elaborazione, ognuno dei quali contiene un numero inferiore di riconoscimenti).
Hello valore più grande di hello per BatchAcknowledgementInterval, hello hello superiore complessiva velocità effettiva della replica, al costo di hello di latenza più elevata di operazione. Questo si traduce direttamente toohello latenza del commit delle transazioni.

