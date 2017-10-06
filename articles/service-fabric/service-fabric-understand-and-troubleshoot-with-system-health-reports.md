---
title: "aaaTroubleshoot con i report di integrità di sistema | Documenti Microsoft"
description: "Vengono descritti i report di integrità hello inviati dai componenti di Azure Service Fabric e il relativo utilizzo per la risoluzione dei problemi del cluster o i problemi dell'applicazione."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a>Utilizzare tootroubleshoot rapporti di integrità sistema
Azure Service Fabric componenti report predefinito hello in tutte le entità nel cluster hello. Hello [archivio integrità](service-fabric-health-introduction.md#health-store) crea ed Elimina le entità in base ai report di sistema hello. Le organizza anche in una gerarchia che acquisisce le interazioni delle entità.

> [!NOTE]
> concetti relativi a integrità toounderstand, leggere informazioni, vedere [il modello di integrità di Service Fabric](service-fabric-health-introduction.md).
> 
> 

I report sull'integrità del sistema forniscono la visibilità delle funzionalità del cluster e dell'applicazione e contrassegnano i problemi riscontrati tramite a livello di integrità. Per servizi e applicazioni, rapporti di integrità di sistema verificare che le entità vengono implementate e corretto dalla prospettiva di Service Fabric hello. report di Hello non forniscono alcun monitoraggio dello stato di rilevamento dei processi bloccati o logica di business hello del servizio di hello. Servizi utente possono migliorare i dati di integrità hello con logica tootheir specifici di informazioni.

> [!NOTE]
> Report sull'integrità watchdog sono visibili solo *dopo* componenti del sistema hello creano un'entità. Quando viene eliminata un'entità, dell'archivio integrità hello Elimina automaticamente tutti i report di integrità è associati. Hello stesso vale quando viene creata una nuova istanza dell'entità hello (ad esempio, viene creata una nuova istanza di replica con stato servizio persistente). Tutti i report associati con l'istanza precedente di hello vengono eliminati e rimossi dal negozio hello.
> 
> 

Hello sistema componente report sono identificati dall'origine hello, che inizia con hello "**System.**" . Watchdog non è possibile utilizzare hello stesso prefisso, per le rispettive origini, come i report con parametri non validi vengono rifiutati.
Si esamina alcuni sistema segnala toounderstand che cosa attiva li e come toocorrect hello possibili problemi che rappresentano.

> [!NOTE]
> Service Fabric continua tooadd report alle condizioni di interesse che consentono di migliorare la visibilità in ciò che avviene nell'applicazione e cluster hello. I report esistenti possono anche essere migliorati con maggiori dettagli toohelp problemi hello più velocemente.
> 
> 

## <a name="cluster-system-health-reports"></a>Report sull'integrità del sistema cluster
entità di integrità del cluster Hello viene creata automaticamente nell'archivio integrità hello. Se tutto funziona correttamente, non è disponibile un report di sistema.

### <a name="neighborhood-loss"></a>Perdita di nodi vicini
**System.Federation** segnala un errore quando rileva una perdita di nodi vicini. ID del nodo hello è incluso nel nome della proprietà hello report Hello è dai singoli nodi. Se uno di risorse verrà persi nel anello Service Fabric intera hello, è possibile che in genere due eventi (entrambi i lati della relazione di distanza hello). In caso di perdita di più nodi vicini, si verificano più eventi.

report Hello specifica il timeout di lease globale hello come ora di hello toolive. report Hello viene nuovamente inviato a ogni parte della durata TTL hello finché la condizione hello rimane attivo. evento Hello viene rimosso automaticamente dopo la scadenza. Rimuovere quando scaduto comportamento assicura che i report di hello è rimossi dall'archivio integrità hello correttamente, anche se il nodo di creazione rapporti hello è attivo.

* **SourceId**: System.Federation
* **Proprietà**: inizia con **Neighborhood** e include informazioni sul nodo
* **Passaggi successivi**: analizzare perché le risorse di hello vanno persa (ad esempio, controllo hello comunicazione tra i nodi del cluster).

## <a name="node-system-health-reports"></a>Report sull'integrità del sistema di nodi
**System.FM**, che rappresenta il servizio di gestione Failover hello, hello autorità che gestisce le informazioni sui nodi del cluster. Ogni nodo deve avere un report generato da System.FM che mostra il relativo stato. le entità di nodo Hello vengono rimosse quando viene rimosso lo stato del nodo hello (vedere [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).

### <a name="node-updown"></a>Nodo attivo/inattivo
Viene segnalato System.FM OK quando viene aggiunto a nodo hello anello hello (è attivo e in esecuzione). Viene segnalato un errore quando il nodo hello si allontana anello hello (è attivo, uno per l'aggiornamento o semplicemente perché non è riuscito). gerarchia di integrità Hello generato dall'archivio integrità hello interviene su entità distribuita in correlazione con i report del nodo System.FM. Nodo hello considera un elemento virtuale padre di tutte le entità distribuite. Se il nodo hello viene segnalato come backup per System.FM, con hello stessa istanza come istanza hello associato hello entità, entità Hello distribuito in tale nodo sono esposte tramite le query. Quando System.FM segnala tale nodo hello è inattivo o riavviato (una nuova istanza), archivio integrità hello pulizia automatica delle entità hello distribuito che possono essere presenti solo in hello verso il basso nodo o sull'istanza precedente di hello del nodo hello.

* **SourceId**: System.FM
* **Proprietà**: State
* **Passaggi successivi**: se il nodo hello è inattivo per un aggiornamento, deve disporre di eseguire il dopo che è stato aggiornato. In questo caso, lo stato di integrità hello deve passare tooOK indietro. Se non viene eseguito il ritorno nodo hello o ha esito negativo, il problema di hello deve ulteriori indagini.

Hello riportato di seguito evento System.FM hello con uno stato di integrità di OK per nodo:

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a>Scadenza dei certificati
**System.FabricNode** segnala un avviso quando i certificati utilizzati da nodo hello si avvicinano alla scadenza. Ogni nodo ha tre certificati: **Certificate_cluster**, **Certificate_server** e **Certificate_default_client**. Una volta scadenza hello almeno due settimane, lo stato di integrità report hello è OK. Una volta scadenza hello entro due settimane, il tipo di report hello è un avviso. Durata (TTL) di questi eventi è infinito, e vengono rimossi quando un nodo abbandona cluster hello.

* **SourceId**: System.FabricNode
* **Proprietà**: inizia con **certificato** e contiene ulteriori informazioni sul tipo di certificato hello
* **Passaggi successivi**: aggiornamento dei certificati di hello in tal caso prossimo alla scadenza.

### <a name="load-capacity-violation"></a>Violazione della capacità di carico
Hello bilanciamento del carico dell'infrastruttura di servizio restituisce un avviso quando rileva una violazione della capacità nodo.

* **SourceId**: System.PLB
* **Proprietà**: inizia con **Capacity**
* **Passaggi successivi**: controllo fornito capacità corrente hello metriche e visualizzare nel nodo hello.

## <a name="application-system-health-reports"></a>Report sull'integrità del sistema di applicazioni
**System.CM**, che rappresenta il servizio di gestione Cluster hello, hello autorità che gestisce le informazioni relative a un'applicazione.

### <a name="state"></a>Stato
System.CM segnala come OK quando un'applicazione hello è stata creata o aggiornata. Comunica archivio integrità hello quando un'applicazione hello è stata eliminata, in modo che può essere rimosso dall'archivio.

* **SourceId**: System.CM
* **Proprietà**: State
* **Passaggi successivi**: se un'applicazione hello è stata creata o aggiornata, deve includere il rapporto di stato gestione Cluster di hello. In caso contrario, controllare lo stato di hello di un'applicazione hello eseguendo una query (ad esempio, hello cmdlet PowerShell **ServiceFabricApplication di Get - ApplicationName *applicationName***).

Hello riportato di seguito evento dello stato di hello in hello **fabric: / WordCount** applicazione:

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a>Report sull'integrità del sistema di servizi
**System.FM**, che rappresenta il servizio di gestione Failover hello, hello autorità che gestisce le informazioni sui servizi.

### <a name="state"></a>Stato
System.FM segnala come OK quando il servizio di hello è stato creato. Elimina entità di hello dall'archivio integrità hello quando hello servizio è stato eliminato.

* **SourceId**: System.FM
* **Proprietà**: State

Hello riportato di seguito evento dello stato di hello sul servizio hello **fabric: / WordCount/WordCountWebService**:

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a>Errore di correlazione del servizio
**System.PLB** segnala un errore quando rileva che un toobe servizio correlato a un altro servizio di aggiornamento crea una catena di affinità. report Hello viene cancellato quando si verifica l'aggiornamento ha esito positivo.

* **SourceId**: System.PLB
* **Proprietà**: ServiceDescription
* **Passaggi successivi**: hello controllo correlato alle descrizioni di servizi.

## <a name="partition-system-health-reports"></a>Report sull'integrità del sistema di partizioni
**System.FM**, che rappresenta il servizio di gestione Failover hello, hello autorità che gestisce le informazioni sulle partizioni di servizio.

### <a name="state"></a>Stato
System.FM segnala come OK quando partizione hello è stata creata ed è integro. Elimina entità di hello dall'archivio integrità hello quando hello partizione viene eliminata.

Se la partizione hello è inferiore al conteggio di replica minimo hello, viene segnalato un errore. Se la partizione hello non è inferiore al conteggio di replica minimo hello, ma è inferiore al conteggio di replica di destinazione hello, viene segnalato un avviso. Se la partizione hello è perso il quorum, System.FM segnala un errore.

Altri eventi importanti includono un avviso quando la riconfigurazione di hello richiede più tempo del previsto e quando la compilazione hello richiede più tempo del previsto. tempi di Hello previsto per la compilazione hello e riconfigurazione sono configurabili in base agli scenari di servizio. Ad esempio, se un servizio è un terabyte di stato, ad esempio Database SQL, compilazione hello richiede più tempo per un servizio con una piccola quantità di stato.

* **SourceId**: System.FM
* **Proprietà**: State
* **Passaggi successivi**: se lo stato di integrità hello è OK, è possibile che alcune repliche non sono stato creato, aperto o innalzata di livello tooprimary o secondario correttamente. In molti casi, causa radice di hello è un bug del servizio aprire hello e l'implementazione di modifica ruolo.

Hello di esempio seguente viene illustrata una partizione integro:

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

Hello riportato di seguito integrità hello di una partizione che si trova sotto il numero di repliche di destinazione. passaggio successivo Hello è tooget descrizione della partizione hello, che mostra come viene configurato: **MinReplicaSetSize** è tre e **TargetReplicaSetSize** sette. Quindi ottenere il numero di hello di nodi nel cluster hello: cinque. Pertanto, in questo caso, due repliche non possono trovarsi perché il numero di destinazione hello delle repliche è superiore hello numero di nodi disponibili.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a>Violazione del vincolo di replica
**System.PLB** segnala un avviso se rileva una violazione del vincolo di replica e non può posizionare tutte le repliche della partizione. i vincoli di visualizzare i dettagli del rapporto Hello e proprietà impediscono l'inserimento di replica hello.

* **SourceId**: System.PLB
* **Proprietà**: inizia con **ReplicaConstraintViolation**

## <a name="replica-system-health-reports"></a>Report sull'integrità del sistema di repliche
**System.RA**, che rappresenta una componente Agente di riconfigurazione hello, rappresenta l'autorità di hello per lo stato della replica hello.

### <a name="state"></a>Stato
**System.RA** segnala OK quando hello replica è stata creata.

* **SourceId**: System.RA
* **Proprietà**: State

Hello di esempio seguente viene illustrata una replica integro:

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a>Stato aperto della replica
descrizione di Hello di questo rapporto di stato contiene l'ora di inizio hello (Coordinated Universal Time) quando è stata richiamata hello API chiamata.

**System.RA** segnala un avviso se replica hello open richiede più tempo periodo hello configurata (impostazione predefinita: 30 minuti). Se hello API influisce sulla disponibilità del servizio, report hello è emesso molto più veloce (un intervallo configurabile, con valore predefinito è 30 secondi). tempo Hello misurato include tempo hello per replicator hello aperto e il servizio di hello aperto. Hello proprietà modifiche tooOK se apre hello completa.

* **SourceId**: System.RA
* **Proprietà**: **ReplicaOpenStatus**
* **Passaggi successivi**: se lo stato di integrità hello non è corretta, esaminare perché replica hello open richiede più tempo del previsto.

### <a name="slow-service-api-call"></a>Chiamata API del servizio lenta
**System.RAP** e **System.Replicator** segnala un avviso se un codice del servizio chiamata toohello utente impiegato più tempo di hello configurato di. avviso di Hello viene cancellata al completamento della chiamata di hello.

* **SourceId**: System.RAP o System.Replicator
* **Proprietà**: nome hello dell'API lenta hello. descrizione di Hello fornisce ulteriori dettagli su hello ora hello API è stato in sospeso.
* **Passaggi successivi**: analizzare perché chiamata hello richiede più tempo del previsto.

Hello di esempio seguente mostra una partizione in perdita del quorum e hello analisi eseguiti passaggi toofigure motivo. Una delle repliche hello ha uno stato di integrità di avviso, per ottenere l'integrità. Viene illustrato che l'operazione del servizio hello impiega più tempo del previsto, un evento segnalato dal System.RAP. Dopo la ricezione di queste informazioni, passaggio successivo hello è toolook al codice del servizio hello e analizzare non esiste. In questo caso, hello **RunAsync** implementazione del servizio con stato hello genera un'eccezione non gestita. repliche Hello sono riciclo, in modo non sarà possibile visualizzare tutte le repliche in uno stato di avviso hello. È possibile ripetere il recupero dello stato di integrità hello e cercare eventuali differenze nell'ID di replica hello. In alcuni casi, i tentativi di hello possono fornire indicazioni.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

Quando si avvia un'applicazione hello non corretto nel debugger hello, finestre di eventi di diagnostica hello mostrano eccezione hello generata da RunAsync:

![Eventi di diagnostica di Visual Studio 2015: errore RunAsync in fabric:/HelloWorldStatefulApplication.][1]

Eventi di diagnostica di Visual Studio 2015: errore RunAsync in **fabric:/HelloWorldStatefulApplication**.

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a>Coda di replica piena
**System.Replicator** genera un avviso quando la coda di replica hello è piena. Hello primario, la coda di replica in genere diventa completa perché una o più repliche secondarie sono operazioni tooacknowledge lento. In hello secondario, questo in genere si verifica quando il servizio di hello è lenta tooapply hello operazioni. avviso di Hello viene cancellato quando la coda hello non è più completa.

* **SourceId**: System.Replicator
* **Proprietà**: **PrimaryReplicationQueueStatus** o **SecondaryReplicationQueueStatus**, a seconda del ruolo della replica hello

### <a name="slow-naming-operations"></a>Operazioni di Naming lente
**System.NamingService** segnala lo stato di integrità per la replica primaria quando un'operazione di Naming richiede più tempo di quanto sia accettabile. Esempi di operazioni di Naming sono [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) e [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync). Altri metodi sono disponibili in FabricClient, ad esempio nell'ambito dei [metodi di gestione dei servizi](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) o dei [metodi di gestione delle proprietà](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).

> [!NOTE]
> Hello Naming service risolve percorso tooa i nomi del servizio cluster hello e consente di proprietà e i nomi di servizio toomanage utenti. È un servizio permanente partizionato di Service Fabric. Una delle partizioni hello rappresenta hello Authority Owner, che contiene i metadati relativi a tutti i servizi e i nomi di Service Fabric. i nomi di Service Fabric Hello sono mappate toodifferent partizioni, chiamate partizioni nome proprietario, pertanto il servizio di hello è estensibile. Per altre informazioni, vedere [Architettura di Service Fabric](service-fabric-architecture.md).
> 
> 

Quando un'operazione di denominazione richiede più tempo del previsto, operazione hello è contrassegnata con un report di avviso su hello *replica primaria di hello partizione del servizio di denominazione che serve operazione hello*. Se il completamento dell'operazione di hello, hello avviso è deselezionato. Se hello concludere con un errore, il rapporto di stato hello include dettagli sull'errore hello.

* **SourceId**: System.NamingService
* **Proprietà**: inizia con prefisso **Duration_** e identifica operazione lenta hello e il nome di Service Fabric hello in cui hello viene applicata l'operazione. Ad esempio, se creare infrastruttura nome servizio: / MyApp/MyService impiega troppo tempo, la proprietà hello Duration_AOCreateService.fabric:/MyApp/MyService. Ruolo di toohello AO punti di hello partizione di denominazione per il nome e l'operazione.
* **Passaggi successivi**: controllo perché hello denominazione operazione ha esito negativo. A ogni operazione può corrispondere una causa radice diversa. Ad esempio, l'eliminazione di servizio potrebbe trovarsi in un nodo perché mantiene un arresto anomalo host applicazione hello in un nodo a causa di bug utente tooa nel codice del servizio hello.

Hello di esempio seguente viene illustrata un'operazione di servizio di creazione. operazione Hello ha richiesto più tempo rispetto a durata hello configurato. AO Ritenta e invia tooNO di lavoro. Nessuna operazione ultimo hello completato con Timeout. In questo caso, hello stessa replica è primaria per hello AO sia alcun ruolo.

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a>Report sull'integrità del sistema DeployedApplication
**System.Hosting** autorità hello per le entità distribuite.

### <a name="activation"></a>Activation
System.Hosting segnala come OK quando un'applicazione è stata attivata nel nodo hello. In caso contrario, restituisce un errore.

* **SourceId**: System.Hosting
* **Proprietà**: attivazione, compresa hello implementazione versione
* **Passaggi successivi**: se un'applicazione hello è integra, provare a causa dell'errore attivazione hello.

Hello seguente illustra l'attivazione:

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Scaricare
**System.Hosting** segnala un errore se si verifica un errore di download del pacchetto dell'applicazione hello.

* **SourceId**: System.Hosting
* **Proprietà**: **Download:*VersioneRollout***
* **Passaggi successivi**: analizzare perché download hello non è riuscito nel nodo hello.

## <a name="deployedservicepackage-system-health-reports"></a>Report sull'integrità del sistema DeployedServicePackage
**System.Hosting** autorità hello per le entità distribuite.

### <a name="service-package-activation"></a>Attivazione del pacchetto di servizi
System.Hosting segnala come OK se l'attivazione del pacchetto di servizio nel nodo hello hello ha esito positivo. In caso contrario, restituisce un errore.

* **SourceId**: System.Hosting
* **Proprietà**: Activation
* **Passaggi successivi**: provare a causa dell'errore attivazione hello.

### <a name="code-package-activation"></a>Attivazione del pacchetto di codice
**System.Hosting** segnala come OK per ogni pacchetto di codice se hello attivazione ha esito positivo. Se l'attivazione di hello ha esito negativo, genera un avviso in base alla configurazione. Se **CodePackage** ha esito negativo tooactivate o termina con un errore maggiore hello configurato **CodePackageHealthErrorThreshold**, hosting segnala un errore. Se un pacchetto servizio contiene più pacchetti di codice, viene generato un report sull'attivazione per ognuno.

* **SourceId**: System.Hosting
* **Proprietà**: prefisso hello utilizza **CodePackageActivation** e contiene il nome di hello del pacchetto di codice hello e il punto di ingresso hello come  **CodePackageActivation:* CodePackageName*:*SetupEntryPoint/EntryPoint** * (ad esempio, **CodePackageActivation:Code:SetupEntryPoint**)

### <a name="service-type-registration"></a>Registrazione del tipo di servizio
**System.Hosting** segnala come OK se il tipo di servizio hello è stato registrato correttamente. Viene segnalato un errore se non è stata effettuata la registrazione di hello nel tempo (in base alla configurazione utilizzando **ServiceTypeRegistrationTimeout**). Se il runtime hello è chiuso, il tipo di servizio hello è stato annullato dal nodo hello e Hosting segnala un avviso.

* **SourceId**: System.Hosting
* **Proprietà**: prefisso hello utilizza **ServiceTypeRegistration** e contiene il nome di tipo servizio hello (ad esempio, **ServiceTypeRegistration:FileStoreServiceType**)

Hello di esempio seguente viene illustrato un pacchetto del servizio distribuito integro:

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Scaricare
**System.Hosting** segnala un errore se si verifica un errore di download del pacchetto del servizio hello.

* **SourceId**: System.Hosting
* **Proprietà**: **Download:*VersioneRollout***
* **Passaggi successivi**: analizzare perché download hello non è riuscito nel nodo hello.

### <a name="upgrade-validation"></a>Convalida dell’aggiornamento
**System.Hosting** segnala un errore se la convalida durante l'aggiornamento di hello non riesce o se hello aggiornamento ha esito negativo nel nodo hello.

* **SourceId**: System.Hosting
* **Proprietà**: prefisso hello utilizza **FabricUpgradeValidation** e contiene la versione di hello aggiornamento
* **Descrizione**: punti di errore toohello

## <a name="next-steps"></a>Passaggi successivi
[Come visualizzare i report sull'integrità di Service Fabric](service-fabric-view-entities-aggregated-health.md)

[Come tooreport e controllo del servizio integrità](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Monitorare e diagnosticare servizi in locale](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Aggiornamento di un'applicazione di infrastruttura di servizi](service-fabric-application-upgrade.md)

