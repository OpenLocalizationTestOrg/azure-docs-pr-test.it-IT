---
title: le impostazioni di ReliableDictionaryActorStateProvider aaaChange in Azure microservizi | Documenti Microsoft
description: Informazioni sulla configurazione di attori con stato di tipo ReliableDictionaryActorStateProvider in Service Fabric di Azure.
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: 79b48ffa-2474-4f1c-a857-3471f9590ded
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 44c85a41c90a17669ba874401d7921c94e7be9ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--reliabledictionaryactorstateprovider"></a>Configurare ReliableDictionaryActorStateProvider di Reliable Actors
È possibile modificare una configurazione predefinita di hello di ReliableDictionaryActorStateProvider modificando hello Settings file generato nella directory principale del pacchetto di Visual Studio hello nella cartella Config hello per attore specificato hello.

Hello Azure Service Fabric runtime cerca i nomi di sezione predefinita nel file Settings hello e utilizza i valori di configurazione hello durante la creazione di componenti di runtime sottostante hello.

> [!NOTE]
> Eseguire **non** eliminare o modificare i nomi di sezione hello di hello seguendo le configurazioni nel file Settings hello che viene generato in hello soluzione di Visual Studio.
> 
> 

Esistono anche impostazioni globali che interessano la configurazione di hello di ReliableDictionaryActorStateProvider.

## <a name="global-configuration"></a>Configurazione globale
configurazione globale Hello è specificata nel manifesto del cluster per cluster hello in hello KtlLogger sezione hello. Configurazione di hello condiviso log posizione e dimensioni più hello globale dei limiti di memoria utilizzata dal logger hello consente. Si noti che le modifiche nel manifesto del cluster hello influiscono su tutti i servizi che utilizzano ReliableDictionaryActorStateProvider e servizi con stati affidabili.

manifesto del cluster Hello è un unico file XML che contiene le impostazioni e configurazioni che si applicano tooall nodi e i servizi in cluster hello. file Hello viene in genere chiamato ClusterManifest.xml. È possibile vedere manifesto del cluster per il cluster con il comando di powershell Get-ServiceFabricClusterManifest hello hello.

### <a name="configuration-names"></a>Nomi delle configurazioni
| Nome | Unità | Valore predefinito | Osservazioni |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |Kilobyte |8388608 |Numero minimo di tooallocate KB in modalità kernel per il logger hello pool di memoria buffer di scrittura. Questo pool di memoria viene utilizzato per la memorizzazione nella cache le informazioni sullo stato prima della scrittura toodisk. |
| WriteBufferMemoryPoolMaximumInKB |Kilobyte |Nessun limite |Pool di memoria di dimensioni massime toowhich hello logger scrittura buffer può raggiungere. |
| SharedLogId |GUID |"" |Specifica un toouse GUID univoco per l'identificazione di hello condivisa file di log predefinito utilizzato da tutti i servizi affidabili in tutti i nodi del cluster hello che non specificano hello SharedLogId nella configurazione del servizio specifico. Se viene specificato lo SharedLogId, deve anche essere specificato lo SharedLogPath. |
| SharedLogPath |Nome di percorso completo |"" |Specifica hello il percorso completo in cui hello condiviso utilizzato da tutti i servizi affidabili in tutti i nodi del cluster hello che non specificano hello SharedLogPath nella configurazione del servizio specifico di file di log. Tuttavia, se è stato specificato SharedLogPath, lo deve essere anche SharedLogId. |
| SharedLogSizeInMB |Megabyte |8192 |Specifica il numero di hello MB di spazio su disco toostatically allocare per log condiviso hello. il valore di Hello deve essere maggiore di 2048. |

### <a name="sample-cluster-manifest-section"></a>Sezione manifesto del cluster di esempio
```xml
   <Section Name="KtlLogger">
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
     <Parameter Name="SharedLogSizeInMB" Value="16383"/>
   </Section>
```

### <a name="remarks"></a>Osservazioni
logger Hello dispone di un pool di memoria allocata dalla memoria del kernel non di paging che servizi affidabili tooall disponibile in un nodo per la memorizzazione nella cache di dati relativi allo stato prima di venire riscritti toohello log dedicato associato a una replica del servizio affidabile hello è globale. dimensioni del pool di Hello sono controllata da hello WriteBufferMemoryPoolMinimumInKB e WriteBufferMemoryPoolMaximumInKB impostazioni. WriteBufferMemoryPoolMinimumInKB specifica entrambi hello dimensioni iniziali del pool di memoria e pool di hello hello minima dimensione toowhich memoria può ridurre. WriteBufferMemoryPoolMaximumInKB è pool hello toowhich di hello massima dimensione memoria può raggiungere. Ogni replica del servizio affidabile che viene aperto può aumentare hello dimensioni del pool di memoria hello una quantità determinata di sistema di tooWriteBufferMemoryPoolMaximumInKB. Se è più richiesta per la memoria dal pool di memoria hello rispetto a quella disponibile, le richieste per la memoria verranno ritardate fino a quando non è disponibile memoria. Pertanto se è troppo piccolo per una particolare configurazione pool di memoria buffer di scrittura hello le prestazioni potrebbero risentirne.

le impostazioni di SharedLogId e SharedLogPath Hello sono sempre hello toodefine insieme utilizzati GUID e posizione per impostazione predefinita hello condivisa di log per tutti i nodi cluster hello. log condiviso di Hello predefinito viene utilizzato per tutti i servizi affidabili che non specificano le impostazioni di hello nel file settings.xml hello per servizio specifico hello. Per prestazioni ottimali, condivisi i file di log devono essere posizionati nei dischi utilizzati esclusivamente per contesa tooreduce file di log hello condiviso.

SharedLogSizeInMB specifica hello toopreallocate di spazio su disco per il log di hello predefinito condiviso in tutti i nodi.  SharedLogId e SharedLogPath toobe specificato affinché toobe SharedLogSizeInMB specificato non è necessario.

## <a name="replicator-security-configuration"></a>Configurazione della sicurezza del replicatore
Le configurazioni di sicurezza Replicator sono canale di comunicazione utilizzati toosecure hello utilizzato durante la replica. Ciò significa che servizi non è possibile vedere di altro traffico di replica, anche i dati hello per garantire che vengano reso a disponibili elevata siano sicuri.
Per impostazione predefinita, una sezione di configurazione della sicurezza vuota non abilita la sicurezza della replica.

### <a name="section-name"></a>Nome della sezione
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Configurazione del replicatore
Le configurazioni di replica sono replicator hello tooconfigure utilizzati che è responsabile per rendere lo stato del Provider di stato attore hello altamente affidabile mediante la replica e la persistenza dello stato di hello in locale.
configurazione predefinita di Hello viene generato dal modello di Visual Studio hello e dovrebbe essere sufficiente. In questa sezione si indica ulteriori configurazioni replicator hello tootune disponibili.

### <a name="section-name"></a>Nome della sezione
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Nomi delle configurazioni
| Nome | Unità | Valore predefinito | Osservazioni |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Secondi |0,015 |Periodo di tempo per cui replicator hello in attese secondario di hello dopo la ricezione di un'operazione prima di inviare nuovamente un toohello acknowledgement primario. Altri toobe acknowledgement inviato per le operazioni di elaborazione all'interno dell'intervallo vengono inviati come una risposta. |
| ReplicatorEndpoint |N/D |Nessun valore predefinito: parametro obbligatorio |Indirizzo IP e porta hello primario o secondario. replicator utilizzerà toocommunicate con altri i servizi di replica nel set di repliche hello. Si deve fare riferimento a un endpoint TCP risorse di manifesto del servizio hello. Fare riferimento troppo[risorse manifesto del servizio](service-fabric-service-manifest-resources.md) tooread ulteriori informazioni sulla definizione delle risorse di endpoint nel manifesto del servizio. |
| MaxReplicationMessageSize |Byte |50 MB |Dimensione massima dei dati di replica che è possibile trasmettere in un singolo messaggio. |
| MaxPrimaryReplicationQueueSize |Numero di operazioni |8192 |Numero massimo di operazioni in coda primaria hello. Un'operazione viene liberata dopo la replica primaria hello riceverà un acknowledgement da tutti i Replicator secondario hello. Questo valore deve essere maggiore di 64 ed essere una potenza di 2. |
| MaxSecondaryReplicationQueueSize |Numero di operazioni |16384 |Numero massimo di operazioni nella coda secondaria hello. Un'operazione viene liberata quando il relativo stato viene reso altamente disponibile tramite persistenza. Questo valore deve essere maggiore di 64 ed essere una potenza di 2. |
| CheckpointThresholdInMB |MB |200 |Quantità di spazio file di log dopo il quale viene eseguito un checkpoint stato hello. |
| MaxRecordSizeInKB |KB |1024 |Dimensione massima del record che hello replicator possono scrivere nel log di hello. Questo valore deve essere un multiplo di 4 ed essere maggiore di 16. |
| OptimizeLogForLowerDiskUsage |Boolean |true |Se è true, i log di hello è configurato in modo che hello dedicato file di log della replica viene creato utilizzando un file sparse NTFS. In questo modo viene ridotta hello effettivo spazio su disco per file hello. Se è false, i file hello viene creato con allocazioni predefinite, che offrono migliori prestazioni di scrittura hello. |
| SharedLogId |GUID |"" |Specifica un toouse guid univoco per l'identificazione di hello condivisa file di log utilizzato con questa replica. In genere, i servizi non devono usare questa impostazione. Tuttavia, se è stato specificato SharedLogId, lo deve essere anche SharedLogPath. |
| SharedLogPath |Nome di percorso completo |"" |Specifica hello il percorso completo in cui verrà creati file di log per la replica condiviso hello. In genere, i servizi non devono usare questa impostazione. Tuttavia, se è stato specificato SharedLogPath, lo deve essere anche SharedLogId. |

## <a name="sample-configuration-file"></a>Esempio file di configurazione
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="180" />
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

Hello CheckpointThresholdInMB parametro controlli hello quantità di spazio che hello replicator è possibile utilizzare le informazioni sullo stato toostore nel file di log dedicato della replica hello. Aumentando questo valore maggiore di tooa quello predefinito di hello può comportare tempi di riconfigurazione quando una nuova replica viene aggiunto toohello set. Equivale a causa di un trasferimento lo stato parziale toohello che viene eseguita a causa della disponibilità toohello della cronologia di altre operazioni nel Registro di hello. Potenzialmente aumentando il tempo di recupero di una replica hello dopo un arresto anomalo.

Se si imposta OptimizeForLowerDiskUsage tootrue, spazio file di log sarà sottoposto a un provisioning in modo che le repliche attive possono archiviare ulteriori informazioni sullo stato dei file di log, mentre le repliche inattive utilizzerà meno spazio su disco. In questo modo è possibile toohost più repliche in un nodo. Se si imposta OptimizeForLowerDiskUsage toofalse, informazioni sullo stato hello viene scritto il file di log toohello più rapidamente.

impostazione MaxRecordSizeInKB Hello definisce dimensioni massime di hello di un record che è possibile scrivere nel file di log hello dal replicatore hello. Nella maggior parte dei casi, hello record 1024 KB dimensione è ottimale. Tuttavia, se il servizio hello causa maggiore parte toobe di elementi di dati di informazioni sullo stato di hello, questo valore potrebbe essere necessario toobe aumentato. È particolarmente vantaggioso eseguendo MaxRecordSizeInKB inferiore a 1024, come record più piccoli utilizzare soltanto lo spazio di hello necessario per il record più piccolo di hello. Si prevede che questo valore dovrebbe toobe modificata solo in rari casi.

Hello SharedLogId e SharedLogPath sono sempre toomake insieme utilizzato un servizio di utilizzare un registro distinto condiviso dal log di hello predefinito condiviso per il nodo hello. Per ottenere migliori prestazioni, come molti servizi possibile specificarne hello stesso condivisa di log. Condivisi i file di log devono essere posizionati nei dischi che vengono utilizzati esclusivamente per hello condivisa file di log, contesa movimento delle testine tooreduce. È previsto che questi valori dovrebbe toobe modificata solo in rari casi.

